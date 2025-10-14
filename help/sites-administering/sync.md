---
title: 사용자 동기화
description: AEM에서 사용자 동기화의 내부 작업에 대해 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
docset: aem65
exl-id: 89f55598-e749-42b8-8f2a-496f45face66
feature: Security
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '2433'
ht-degree: 1%

---


# 사용자 동기화{#user-synchronization}

## 소개 {#introduction}

배포가 [게시 팜](/help/sites-deploying/recommended-deploys.md#tarmk-farm)인 경우 구성원은 모든 Publish 노드에 로그인하고 해당 데이터를 볼 수 있어야 합니다.

게시 환경에서 만든 사용자 및 사용자 그룹(사용자 데이터)은 작성 환경에서 필요하지 않습니다.

작성 환경에서 생성된 대부분의 사용자 데이터는 작성 환경에 남아 Publish 인스턴스로 복사되지 않도록 설계되었습니다.

하나의 Publish 인스턴스에서 수행한 등록 및 수정 사항을 다른 Publish 인스턴스와 동기화하여 동일한 사용자 데이터에 액세스할 수 있도록 해야 합니다.

AEM 6.1부터는 사용자 동기화가 활성화되면 사용자 데이터가 팜의 Publish 인스턴스 간에 자동으로 동기화되며 작성자에서 생성되지 않습니다.

## Sling 배포 {#sling-distribution}

사용자 데이터는 [ACL](/help/sites-administering/security.md)과(와) 함께 Oak JCR 아래 계층인 [Oak Core](/help/sites-deploying/platform.md)에 저장되고 [Oak API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/jackrabbit/oak/api/package-tree.html)를 사용하여 액세스됩니다. 자주 업데이트하지 않으면 [Sling 콘텐츠 배포](https://github.com/apache/sling-old-svn-mirror/blob/trunk/contrib/extensions/distribution/README.md)(Sling 배포)를 사용하여 사용자 데이터를 다른 Publish 인스턴스와 동기화하는 것이 좋습니다.

Sling 배포를 사용하여 기존 복제와 비교하여 사용자 동기화의 이점은 다음과 같습니다.

* Publish에서 만든 *사용자*, *사용자 프로필* 및 *사용자 그룹*&#x200B;은(는) 작성자에 만들어지지 않습니다

* Sling 배포는 jcr 이벤트에 속성을 설정하므로 무한 복제 루프에 대한 걱정 없이 게시측 이벤트 리스너 내에서 작업할 수 있습니다
* Sling 배포는 사용자 데이터를 비원본 Publish 인스턴스로만 보내어 불필요한 트래픽을 제거합니다
* 사용자 노드에 설정된 [ACL](/help/sites-administering/security.md)이(가) 동기화에 포함됩니다.

>[!NOTE]
>
>세션이 필요한 경우 SSO 솔루션을 사용하거나 고정 세션을 사용하여 고객이 다른 Publish 인스턴스로 전환되면 로그인하도록 하는 것이 좋습니다.

>[!CAUTION]
>
>사용자 동기화가 활성화된 경우에도 **관리자** 그룹의 동기화가 지원되지 않습니다. 대신, &#39;차이점 가져오기&#39; 실패가 오류 로그에 기록됩니다.
>
>따라서 배포가 게시 팜인 경우 사용자가 **관리자** 그룹에 추가되거나 그룹에서 제거되면 각 Publish 인스턴스에서 수동으로 수정해야 합니다.

## 사용자 동기화 활성화 {#enable-user-sync}

>[!NOTE]
>
>기본적으로 사용자 동기화는 `disabled`입니다.
>
>사용자 동기화를 활성화하면 *기존* OSGi 구성을 수정하는 작업이 포함됩니다.
>
>사용자 동기화를 활성화한 결과 새 구성을 추가하지 않아야 합니다.

사용자 데이터는 작성자에 작성되지 않더라도 사용자 동기화는 작성자 환경에 의존하여 사용자 데이터 배포를 관리합니다. 모두는 아니지만 대부분의 구성은 작성 환경에서 수행되며 각 단계에서는 작성자 또는 Publish에서 수행되는지 여부를 명확하게 식별합니다.

다음은 사용자 동기화를 활성화하는 데 필요한 단계이며 [문제 해결](#troubleshooting) 섹션이 뒤따릅니다.

### 사전 요구 사항 {#prerequisites}

1. 하나의 Publish 인스턴스에서 사용자와 사용자 그룹을 이미 만든 경우 사용자 동기화를 구성하고 활성화하기 전에 모든 Publish 인스턴스에 사용자 데이터를 [수동으로 동기화](#manually-syncing-users-and-user-groups)하는 것이 좋습니다.

사용자 동기화가 활성화되면 새로 생성된 사용자와 그룹만 동기화됩니다.

1. 최신 코드가 설치되어 있는지 확인합니다.

* [AEM 플랫폼 업데이트](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=ko)
* [AEM Communities 업데이트](/help/communities/deploy-communities.md#latestfeaturepack)

### 1. Apache Sling 배포 에이전트 - 동기화 에이전트 팩토리 {#apache-sling-distribution-agent-sync-agents-factory}

**사용자 동기화 사용**

* 작성자의 **&#x200B;**

   * 관리자 권한으로 로그인
   * [웹 콘솔에 액세스](/help/sites-deploying/configuring-osgi.md)

      * 예: [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

   * `Apache Sling Distribution Agent - Sync Agents Factory` 찾기

      * 편집할 수 있도록 기존 구성을 선택합니다(연필 아이콘)
`name` 확인: **`socialpubsync`**

      * `Enabled` 확인란 선택
      * `Save` 선택

![Apache Sling 배포 에이전트](assets/chlimage_1-20.png)

### 2. 인증된 사용자 만들기 {#createauthuser}

**권한 구성**

승인된 사용자는 3단계에서 작성자에 대한 Sling 배포를 구성하는 데 사용됩니다.

* 각 Publish 인스턴스의 **개**

   * 관리자 권한으로 로그인
   * [보안 콘솔에 액세스](/help/sites-administering/security.md)

      * 예: [https://localhost:4503/useradmin](https://localhost:4503/useradmin)

   * 사용자 만들기

      * 예: `usersync-admin`

   * **`administrators`** 사용자 그룹에 이 사용자 추가
   * [/home에 이 사용자에 대한 ACL 추가](#howtoaddacl)

      * `rep:glob=*/activities/*` 제한이 있는 `Allow jcr:all`

>[!CAUTION]
>
>새 사용자를 만들어야 합니다.
>
>* 할당된 기본 사용자는 **`admin`**&#x200B;입니다.
>* `communities-user-admin user.` 사용 안 함
>

#### ACL을 추가하는 방법 {#addacls}

* 액세스 CRXDE Lite

   * 예: [https://localhost:4503/crx/de](https://localhost:4503/crx/de)

* `/home` 노드 선택
* 오른쪽 창에서 `Access Control` 탭을 선택합니다.
* ACL 항목을 추가하려면 `+` 단추를 선택하십시오.

   * **사용자**: *사용자 동기화를 위해 만들어진 사용자 검색*
   * **유형**: `Allow`
   * **권한**: `jcr:all`
   * **제한** `rep:glob`: `*/activities/*`
   * **확인** 선택

* **모두 저장** 선택

![ACL 창 추가](assets/chlimage_1-21.png)

추가 참조

* [액세스 권한 관리](/help/sites-administering/user-group-ac-admin.md#access-right-management)
* [응답을 처리하는 동안 작업 예외 수정](#modify-operation-exception-during-response-processing) 섹션의 문제를 해결합니다.

### 3. Adobe Granite 배포 - 암호화된 암호 전송 비밀 공급자 {#adobegraniteencpasswrd}

**권한 구성**

**`administrators`** 사용자 그룹의 구성원인 인증된 사용자가 모든 Publish 인스턴스에서 만들어지면 인증된 사용자가 작성자에서 사용자 데이터를 작성자에서 Publish으로 동기화할 권한이 있는 것으로 식별되어야 합니다.

* 작성자의 **명**

   * 관리자 권한으로 로그인
   * [웹 콘솔에 액세스](/help/sites-deploying/configuring-osgi.md)

      * 예: [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

   * `com.adobe.granite.distribution.core.impl.CryptoDistributionTransportSecretProvider.name` 찾기
   * 편집을 위해 열려면 기존 구성(연필 아이콘)을 선택합니다
`property name` 확인: **`socialpubsync-publishUser`**

   * 사용자 이름과 암호를 2단계에서 Publish에서 만든 [승인된 사용자](#createauthuser)(으)로 설정합니다.

      * 예: `usersync-admin`

![암호화된 전송 비밀 공급자](assets/chlimage_1-22.png)

### 4. Apache Sling 배포 에이전트 - 큐 에이전트 팩토리 {#apache-sling-distribution-agent-queue-agents-factory}

**사용자 동기화 사용**

* **각 Publish 인스턴스에서**:

   * 관리자 권한으로 로그인
   * [웹 콘솔에 액세스](/help/sites-deploying/configuring-osgi.md)

      * 예: [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

   * `Apache Sling Distribution Agent - Queue Agents Factory` 찾기

      * 편집을 위해 열려면 기존 구성(연필 아이콘)을 선택합니다
`Name` 확인: `socialpubsync-reverse`

      * `Enabled` 확인란 선택
      * `Save` 선택

   * 각 Publish 인스턴스에 대해 **반복**

![큐 에이전트 팩터리](assets/chlimage_1-23.png)

### 5. Adobe Social 동기화 - 차이점 옵저버 팩토리 {#diffobserver}

**그룹 동기화 사용**

* **각 Publish 인스턴스에서**:

   * 관리자 권한으로 로그인
   * [웹 콘솔에 액세스](/help/sites-deploying/configuring-osgi.md)

      * 예: [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

   * **`Adobe Social Sync - Diff Observer Factory`** 찾기

      * 편집을 위해 열려면 기존 구성(연필 아이콘)을 선택합니다

        `agent name` 확인: `socialpubsync-reverse`

      * `Enabled` 확인란 선택
      * `Save` 선택

![비교 관찰자 팩터리](assets/screen-shot_2019-05-24at090809.png)

### 6. Apache Sling 배포 트리거 - 예약된 트리거 팩토리 {#apache-sling-distribution-trigger-scheduled-triggers-factory}

**(선택 사항) 폴링 간격 수정**

기본적으로 작성자는 30초마다 변경 사항을 폴링합니다. 이 간격을 변경하려면:

* 작성자의 **명**

   * 관리자 권한으로 로그인
   * [웹 콘솔에 액세스](/help/sites-deploying/configuring-osgi.md)

      * 예: [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

   * `Apache Sling Distribution Trigger - Scheduled Triggers Factory` 찾기

      * 편집을 위해 열려면 기존 구성(연필 아이콘)을 선택합니다

         * `Name` 확인: `socialpubsync-scheduled-trigger`

      * `Interval in Seconds`을(를) 원하는 간격으로 설정합니다.
      * `Save` 선택

![예약된 트리거 팩터리](assets/chlimage_1-24.png)

## 여러 Publish 인스턴스에 대한 구성 {#configure-for-multiple-publish-instances}

기본 구성은 단일 Publish 인스턴스에 대한 것입니다. 사용자 동기화를 활성화하는 이유는 게시 팜의 경우와 같이 여러 Publish 인스턴스를 동기화하기 위함이므로 추가 Publish 인스턴스를 동기화 에이전트 팩토리에 추가해야 합니다.

### 7. Apache Sling 배포 에이전트 - 동기화 에이전트 팩토리 {#apache-sling-distribution-agent-sync-agents-factory-1}

**Publish 인스턴스 추가:**

* 작성자의 **명**

   * 관리자 권한으로 로그인
   * [웹 콘솔에 액세스](/help/sites-deploying/configuring-osgi.md)

      * 예: [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

   * `Apache Sling Distribution Agent - Sync Agents Factory` 찾기

      * 편집을 위해 열려면 기존 구성(연필 아이콘)을 선택합니다
`Name` 확인: `socialpubsync`

![동기화 에이전트 팩터리](assets/chlimage_1-25.png)

* **내보내기 끝점**
각 Publish 인스턴스에 대한 내보내기 종단점이 있어야 합니다. 예를 들어 2개의 Publish 인스턴스인 localhost:4503과 4504가 있는 경우 두 개의 항목이 있어야 합니다.

   * `https://localhost:4503/libs/sling/distribution/services/exporters/socialpubsync-reverse`
   * `https://localhost:4504/libs/sling/distribution/services/exporters/socialpubsync-reverse`

* **가져오기 끝점**
각 Publish 인스턴스에 대한 가져오기 종단점이 있어야 합니다. 예를 들어 2개의 Publish 인스턴스인 localhost:4503과 4504가 있는 경우 두 개의 항목이 있어야 합니다.

   * `https://localhost:4503/libs/sling/distribution/services/importers/socialpubsync`
   * `https://localhost:4504/libs/sling/distribution/services/importers/socialpubsync`

* `Save` 선택

### 8. AEM Communities 사용자 동기화 수신기 {#aem-communities-user-sync-listener}

**(선택 사항) 추가 JCR 노드 동기화**

여러 Publish 인스턴스 간에 동기화할 사용자 지정 데이터가 있는 경우 다음을 수행합니다.

* **각 Publish 인스턴스에서**:

   * 관리자 권한으로 로그인
   * [웹 콘솔에 액세스](/help/sites-deploying/configuring-osgi.md)

      * 예: `https://localhost:4503/system/console/configMgr`

   * `AEM Communities User Sync Listener` 찾기
   * 편집을 위해 열려면 기존 구성(연필 아이콘)을 선택합니다
`Name` 확인: `socialpubsync-scheduled-trigger`

![AEM Communities 사용자 동기화 수신기](assets/chlimage_1-26.png)

* **노드 유형**
동기화된 노드 유형 목록입니다. sling:Folder 이외의 모든 노드 유형은 여기에 나열되어야 합니다(sling:folder는 별도로 처리됨).
동기화할 노드 유형의 기본 목록:

   * rep:User
   * nt:unstructured
   * nt:resource

* **Ignorable 속성**
변경 사항이 감지되면 무시되는 속성 목록입니다. 이러한 속성에 대한 변경 사항은 다른 변경 사항의 부작용으로 동기화될 수 있지만(동기화는 항상 노드 수준에 있으므로) 이러한 속성에 대한 변경 사항 자체로는 동기화를 트리거하지 않습니다.
무시할 기본 속성:

   * cq:lastModified

* **Ignorable 노드**
동기화 중에 무시되는 하위 경로입니다. 이러한 하위 경로의 아무 것도 동기화되지 않습니다.
무시할 기본 노드:

   * .tokens
   * 시스템

* **분산 폴더**
동기화가 필요하지 않으므로 대부분의 sling:폴더가 무시됩니다. 몇 가지 예외가 여기에 나열됩니다.
동기화할 기본 폴더

   * 세그먼트/점수
   * 소셜/관계
   * 활동

### 9. 고유 Sling ID {#unique-sling-id}

>[!CAUTION]
>
>Sling ID가 둘 이상의 Publish 인스턴스 간에 일치하는 경우 사용자 그룹 동기화에 실패합니다.

게시 팜의 여러 Publish 인스턴스에 대해 Sling ID가 동일한 경우 사용자 그룹은 동기화되지 않습니다.

각 Publish 인스턴스에서 모든 Sling ID 값이 다른지 확인하려면 다음을 수행하십시오.

1. `http://<host>:<port>/system/console/status-slingsettings`(으)로 이동
1. **Sling ID**&#x200B;의 값을 확인하십시오.

![Sling ID의 값을 확인하는 중](assets/chlimage_1-27.png)

Publish 인스턴스의 Sling ID가 다른 Publish 인스턴스의 Sling ID와 일치하는 경우 다음을 수행합니다.

1. sling ID가 일치하는 Publish 인스턴스 중 하나를 중지합니다
1. crx-quickstart/launchpad/felix 디렉터리에서

   * 이름이 *sling.id.file*&#x200B;인 파일을 검색하고 삭제합니다.

      * 예를 들어 Linux® 시스템의 경우:

        `rm -i $(find . -type f -name sling.id.file)`

      * 예를 들어 Windows 시스템의 경우:

        `use windows explorer and search for *sling.id.file*`

1. Publish 인스턴스 시작

   * 시작 시 새 Sling ID가 할당됩니다.

1. **Sling ID**&#x200B;이(가) 이제 고유한지 확인

모든 Publish 인스턴스에 고유한 Sling ID가 있을 때까지 이 단계를 반복합니다.

## Vault 패키지 빌더 팩토리 {#vault-package-builder-factory}

업데이트가 제대로 동기화되려면 사용자 동기화를 위해 자격 증명 모음 패키지 빌더를 수정해야 합니다.

* 각 AEM Publish 인스턴스에서
* [웹 콘솔에 액세스](/help/sites-deploying/configuring-osgi.md)

   * 예: [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* `Apache Sling Distribution Packaging - Vault Package Builder Factory` 찾기

   * `Builder name: socialpubsync-vlt`

* 편집 아이콘 선택
* 두 개의 `Package Node Filters` 추가:

   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`

* 정책 처리:

   * 기존 rep:policy 노드를 새 노드로 덮어쓰려면 세 번째 패키지 필터를 추가합니다.

      * `/home/users|+.*/rep:policy`

   * 정책이 배포되지 않도록 하려면 다음을 설정하십시오.

      * `Acl Handling:` `IGNORE`

![자격 증명 모음 패키지 빌더 팩터리](assets/vault-package-builder-factory.png)

## 다음의 경우 발생하는 일... {#what-happens-when}

### 사용자가 Publish에서 직접 등록 또는 편집 프로필 {#user-self-registers-or-edits-profile-on-publish}

기본적으로 게시 환경(자가 등록)에서 생성된 사용자 및 프로필은 작성 환경에 표시되지 않습니다.

토폴로지가 [게시 팜](/help/sites-deploying/recommended-deploys.md#tarmk-farm)이고 사용자 동기화가 올바르게 구성된 경우 *사용자* 및 *사용자 프로필*&#x200B;이(가) Sling 배포를 사용하여 게시 팜 전반에서 동기화됩니다.

### 사용자 또는 사용자 그룹은 보안 콘솔을 사용하여 만들어집니다 {#users-or-user-groups-are-created-using-security-console}

기본적으로 게시 환경에서 생성된 사용자 데이터는 작성 환경에 표시되지 않으며 그 반대로 표시됩니다.

[사용자 관리 및 보안](/help/sites-administering/security.md) 콘솔을 사용하여 게시 환경에 새 사용자를 추가하면 사용자 동기화는 필요한 경우 새 사용자와 해당 그룹 구성원을 다른 Publish 인스턴스와 동기화합니다. 또한 사용자 동기화는 보안 콘솔을 통해 만든 사용자 그룹을 동기화합니다.

## 문제 해결 {#troubleshooting}

### 사용자 동기화를 오프라인 상태로 만드는 방법 {#how-to-take-user-sync-offline}

사용자 동기화를 오프라인으로 전환하려면 [Publish 인스턴스를 제거](#how-to-remove-a-publish-instance) 또는 [수동으로 데이터 동기화](#manually-syncing-users-and-user-groups)하려면 배포 큐가 비어 있고 조용해야 합니다.

분배 대기열의 상태를 확인하려면:

* 작성자:

   * [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) 사용

      * `/var/sling/distribution/packages`에서 항목을 찾습니다.

         * 이름이 `distrpackage_*` 패턴으로 지정된 폴더 노드

   * [패키지 관리자](/help/sites-administering/package-manager.md) 사용

      * 보류 중인 패키지 찾기(아직 설치되지 않음)

         * 이름이 `socialpubsync-vlt*` 패턴으로 지정되었습니다.
         * 만든 사람: `communities-user-admin`

배포 큐가 비어 있는 경우 사용자 동기화를 비활성화합니다.

* 작성자

   * *선택 취소 *[Apache Sling 배포 에이전트 - 동기화 에이전트 팩토리](#apache-sling-distribution-agent-sync-agents-factory)에 대한 `Enabled` 확인란

작업이 완료되면 사용자 동기화를 다시 활성화하려면 다음을 수행하십시오.

* 작성자

   * [Apache Sling 배포 에이전트 - 동기화 에이전트 팩토리](#apache-sling-distribution-agent-sync-agents-factory)에 대한 `Enabled` 확인란을 선택하십시오.

### 사용자 동기화 진단 {#user-sync-diagnostics}

사용자 동기화 진단 은 구성을 확인하고 문제를 파악하기 위한 도구입니다.

작성자의 경우 **도구, 작업, 진단, 사용자 동기화 진단을 통해 기본 콘솔에서 이동하기만 하면 됩니다.**

User Sync Diagnostics 콘솔로 들어오면 결과가 표시됩니다.

사용자 동기화가 활성화되지 않은 경우 표시되는 항목은 다음과 같습니다.

![사용자 동기화 진단을 사용할 수 없다는 경고](assets/chlimage_1-28.png)

#### Publish 인스턴스에 대한 진단을 실행하는 방법 {#how-to-run-diagnostics-for-publish-instances}

작성자 환경에서 진단을 실행하면 합격/실패 결과에 확인을 위해 구성된 Publish 인스턴스 목록을 표시하는 [INFO] 섹션이 포함됩니다.

해당 인스턴스에 대한 진단을 실행하는 각 Publish 인스턴스의 URL이 목록에 포함됩니다. URL 매개 변수 `syncUser`이(가) 진단 URL에 추가되고 해당 값은 [2단계](#createauthuser)에서 만든 *승인된 동기화 사용자*(으)로 설정됩니다.

**참고**: URL을 시작하기 전에 *승인된 동기화 사용자*&#x200B;가 해당 Publish 인스턴스에 이미 로그인되어 있어야 합니다.

![Publish 인스턴스에 대한 진단](assets/chlimage_1-29.png)

### 구성이 잘못 추가됨 {#configuration-improperly-added}

사용자 동기화가 작동하지 않을 때 가장 일반적인 문제는 추가 구성이 *추가*&#x200B;되었다는 것입니다. 대신 *기존 *기본 구성은 *편집*&#x200B;되어야 합니다.

다음은 편집된 기본 구성이 웹 콘솔에 표시되는 방식을 보여 주는 보기입니다. 인스턴스가 두 개 이상 나타나면 추가된 구성을 제거해야 합니다.

#### (작성자) Apache Sling 배포 에이전트 1개 - 동기화 에이전트 팩토리 {#author-one-apache-sling-distribution-agent-sync-agents-factory}

![웹 콘솔에서 편집된 기본 구성 보기](assets/chlimage_1-30.png)

#### (작성자) Apache Sling 배포 전송 자격 증명 - 사용자 자격 증명 기반 배포TransportSecretProvider {#author-one-apache-sling-distribution-transport-credentials-user-credentials-based-distributiontransportsecretprovider}

![웹 콘솔에서 편집된 기본 구성 보기](assets/chlimage_1-31.png)

#### (Publish) Apache Sling 배포 에이전트 1개 - 큐 에이전트 팩토리 {#publish-one-apache-sling-distribution-agent-queue-agents-factory}

![웹 콘솔에서 편집된 기본 구성 보기](assets/chlimage_1-32.png)

#### (Publish) 하나의 Adobe Social 동기화 - 차이점 옵저버 팩토리 {#publish-one-adobe-social-sync-diff-observer-factory}

![웹 콘솔에서 편집된 기본 구성 보기](assets/chlimage_1-33.png)

#### (작성자) Apache Sling 배포 트리거 1개 - 예약된 트리거 팩토리 {#author-one-apache-sling-distribution-trigger-scheduled-triggers-factory}

![웹 콘솔에서 편집된 기본 구성 보기](assets/chlimage_1-34.png)

### 응답을 처리하는 동안 작업 예외 수정 {#modify-operation-exception-during-response-processing}

다음 항목이 로그에 표시되는 경우:

`org.apache.sling.servlets.post.impl.operations.ModifyOperation Exception during response processing.`

`java.lang.IllegalStateException: This tree does not exist`

그런 다음 섹션 [2을(를) 확인합니다. 인증된 사용자 &#x200B;](#createauthuser) 만들기가 제대로 수행되었습니다.

이 섹션에서는 모든 Publish 인스턴스에 존재하는 인증된 사용자를 만들고, 작성자의 &#39;비밀 공급자&#39; OSGi 구성에서 해당 사용자를 식별하는 방법에 대해 설명합니다. 기본적으로 사용자는 `admin`입니다.

권한이 부여된 사용자는 **`administrators`** 사용자 그룹의 구성원이 되어야 하며 해당 그룹에 대한 권한을 변경해서는 안 됩니다.

승인된 사용자는 모든 Publish 인스턴스에 대해 명시적으로 다음 권한 및 제한을 보유해야 합니다.

| **path** | **jcr:all** | **rep:glob** |
|---|---|---|
| /home | X | &#42;/활동/&#42; |
| /home/users | X | &#42;/활동/&#42; |
| /home/groups | X | &#42;/활동/&#42; |

`administrators` 그룹의 구성원으로서 권한이 있는 사용자는 모든 Publish 인스턴스에 대해 다음 권한을 가져야 합니다.

| **path** | **jcr:all** | **jcr:read** | **rep:write** |
|---|---|---|---|
| /etc/packages/sling/distribution |  |  | X |
| /libs/sling/distribution |  | X |  |
| /var |  |  | X |
| /var/eventing |  | X | X |
| /var/sling/distribution |  | X | X |

### 사용자 그룹 동기화 실패 {#user-group-sync-failed}

Sling ID가 둘 이상의 Publish 인스턴스 간에 일치하는 경우 사용자 그룹 동기화에 실패합니다.

섹션 [9을(를) 참조하세요. 고유 Sling ID](#unique-sling-id)

### 사용자 및 사용자 그룹 수동 동기화 {#manually-syncing-users-and-user-groups}

* 사용자 및 사용자 그룹이 있는 Publish 인스턴스에서 다음을 수행합니다.

   * [활성화된 경우 사용자 동기화 비활성화](#how-to-take-user-sync-offline)
   * [패키지 만들기](/help/sites-administering/package-manager.md#creating-a-new-package)/`/home`

      * 패키지 편집 시

         * 필터 탭: 필터 추가: 루트 경로: `/home`
         * 고급 탭: AC 처리: `Overwrite`

   * [패키지 내보내기](/help/sites-administering/package-manager.md#downloading-packages-to-your-file-system)

* 다른 Publish 인스턴스에서 다음을 수행합니다.

   * [패키지 가져오기](/help/sites-administering/package-manager.md#installing-packages)

사용자 동기화를 구성하거나 사용하려면 1단계로 이동하십시오. [Apache Sling 배포 에이전트 - 동기화 에이전트 팩토리](#apache-sling-distribution-agent-sync-agents-factory)

### Publish 인스턴스를 사용할 수 없게 되는 경우 {#when-a-publish-instance-becomes-unavailable}

Publish 인스턴스를 사용할 수 없게 되면 나중에 다시 온라인으로 돌아올 경우 제거하지 말아야 합니다. 변경 사항은 Publish 인스턴스에 대해 큐에 올라가며 다시 온라인 상태가 되면 변경 사항이 처리됩니다.

Publish 인스턴스가 다시 온라인으로 돌아오지 않는 경우, 영구적으로 오프라인인 경우, 작성자 환경에서 대기열 축적이 눈에 띄는 디스크 공간 사용을 초래하므로 해당 인스턴스를 제거해야 합니다.

Publish 인스턴스가 작동 중지되면 작성자 로그에는 다음과 유사한 예외가 발생합니다.

```
28.01.2016 15:57:48.475 ERROR
 [pool-12-thread-34-org_apache_sling_distribution_queue_socialpubsync_endpoint1
 (org/apache/sling/distribution/queue/socialpubsync/endpoint1)]
 org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync] could not deliver package distrpackage_1454014575838_a2b45ec8-0400-42f3-bed8-ae09b66381cb
 org.apache.sling.distribution.packaging.DistributionPackageImportException: failed in importing package ...
```

### Publish 인스턴스를 제거하는 방법 {#how-to-remove-a-publish-instance}

[Apache Sling 배포 에이전트 - 동기화 에이전트 팩터리](#apache-sling-distribution-agent-sync-agents-factory)에서 Publish 인스턴스를 제거하려면 배포 큐가 비어 있고 조용해야 합니다.

* 작성자:

   * [사용자 동기화를 오프라인으로 전환](#how-to-take-user-sync-offline)
   * [7단계](#apache-sling-distribution-agent-sync-agents-factory)를 따라 두 서버 목록에서 Publish 인스턴스를 제거합니다.

      * `Exporter Endpoints`
      * `Importer Endpoints`

   * 사용자 동기화 다시 활성화

      * [Apache Sling 배포 에이전트 - 동기화 에이전트 팩토리](#apache-sling-distribution-agent-sync-agents-factory)에 대한 `Enabled` 확인란을 선택하십시오.
