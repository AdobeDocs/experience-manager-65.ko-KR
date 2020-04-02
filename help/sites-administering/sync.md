---
title: 사용자 동기화
seo-title: 사용자 동기화
description: AEM에서의 사용자 동기화에 대해 알아봅니다.
seo-description: AEM에서의 사용자 동기화에 대해 알아봅니다.
uuid: 0a519daf-21b7-4adc-b419-eeb8c404c54f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: c061b358-8c0d-40d3-8090-dc9800309ab3
docset: aem65
translation-type: tm+mt
source-git-commit: c9edac158bc6a00637f8be5aac70a2a249e11d59

---


# 사용자 동기화{#user-synchronization}

## 소개 {#introduction}

배포가 [게시 팜인](/help/sites-deploying/recommended-deploys.md#tarmk-farm)경우 구성원은 로그인하여 모든 게시 노드에서 자신의 데이터를 볼 수 있어야 합니다.

게시 환경에서 만들어진 사용자 및 사용자 그룹(사용자 데이터)은 작성 환경에서 필요하지 않습니다.

작성 환경에서 생성된 대부분의 사용자 데이터는 작성 환경에 그대로 유지되며 게시 인스턴스에 복사되지 않습니다.

하나의 게시 인스턴스에서 수행한 등록 및 수정 사항을 다른 게시 인스턴스와 동기화하여 동일한 사용자 데이터에 액세스해야 합니다.

AEM 6.1부터 사용자 동기화가 활성화되면 사용자 데이터는 팜의 게시 인스턴스 간에 자동으로 동기화되고 작성자에 만들어지지 않습니다.

## Sling 배포 {#sling-distribution}

사용자 데이터는 ACL과 함께 [Oak](/help/sites-administering/security.md)Core [에](/help/sites-deploying/platform.md)저장되고 Oak JCR 아래에 [있으며 Oak API를 사용하여](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/oak/api/package-tree.html)액세스합니다. 자주 업데이트되는 경우 사용자 데이터가 Sling 컨텐츠 배포(Sling 배포)를 사용하여 다른 게시 인스턴스와 [동기화하는 것이](https://github.com/apache/sling/blob/trunk/contrib/extensions/distribution/README.md) 적절합니다.

기존 복제와 비교하여 Sling 배포를 사용한 사용자 동기화 이점은 다음과 같습니다.

* *사용자*, *사용자 프로필* 및 ** 게시 시 만든 사용자 그룹이 작성자에 만들어지지 않음

* Sling 배포는 jcr 이벤트에 속성을 설정하므로 무한 복제 루프에 대한 걱정 없이 게시 측 이벤트 리스너 내에서 작동할 수 있습니다.
* Sling 배포는 사용자 데이터를 원본 게시 인스턴스가 아닌 게시 인스턴스에만 전송하여 불필요한 트래픽을 제거합니다.
* [사용자](/help/sites-administering/security.md) 노드에 설정된 ACL은 동기화에 포함됩니다.

>[!NOTE]
>
>세션이 필요한 경우 SSO 솔루션을 사용하거나 고정 세션을 사용하여 고객이 다른 게시자로 전환되면 로그인하도록 하는 것이 좋습니다.

>[!CAUTION]
>
>사용자 동기화가 활성화된 경우에도 ***관리자*** 그룹의 동기화는 지원되지 않습니다. 대신 &#39;비교 가져오기&#39; 오류가 오류 로그에 기록됩니다.
>
>따라서 배포가 게시 팜인 경우 사용자가 ***관리자** 그룹에 추가되거나 제거되면 각 게시 인스턴스에서 수동으로 수정해야 합니다.

## 사용자 동기화 활성화 {#enable-user-sync}

>[!NOTE]
>
>기본적으로 사용자 동기화는 `disabled`입니다.
>
>사용자 동기화 활성화에는 *기존* OSGi 구성을 수정하는 작업이 포함됩니다.
>
>사용자 동기화를 활성화한 결과로 새 구성을 추가할 필요가 없습니다.

사용자 동기화는 작성 환경에 의존하여 사용자 데이터가 작성자에 만들어지지 않더라도 사용자 데이터 배포를 관리합니다. 작성 환경에서 전체 구성 중 많은 것은 아니지만 작성 환경에서 수행되며 각 단계에서는 작성 시 수행할지 또는 게시에서 수행할지를 명확하게 파악합니다.

다음은 사용자 동기화를 활성화하는 데 필요한 단계이며 문제 해결 [섹션을](#troubleshooting) 따릅니다.

### 전제 조건 {#prerequisites}

1. 사용자 및 사용자 그룹이 한 게시자에서 이미 만들어진 경우 사용자 동기화를 구성하고 활성화하기 전에 사용자 데이터를 모든 게시자에게 [수동으로 동기화하는](#manually-syncing-users-and-user-groups) 것이 좋습니다.

사용자 동기화가 활성화되면 새로 만든 사용자와 그룹만 동기화됩니다.

1. 최신 코드가 설치되었는지 확인합니다.

* [AEM 플랫폼 업데이트](https://helpx.adobe.com/experience-manager/kb/aem62-available-hotfixes.html)
* [AEM Communities 업데이트](/help/communities/deploy-communities.md#latestfeaturepack)

### 1.Apache Sling Distribution Agent - Sync Agents Factory {#apache-sling-distribution-agent-sync-agents-factory}

**사용자 동기화 활성화**

* **작성자**

   * 관리자 권한으로 로그인
   * 웹 [콘솔 액세스](/help/sites-deploying/configuring-osgi.md)

      * 예: [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * locate `Apache Sling Distribution Agent - Sync Agents Factory`

      * 편집할 기존 구성을 선택합니다(연필 아이콘)확인 `name`: **`socialpubsync`**

      * 확인란 선택 `Enabled`
      * select `Save`


![](assets/chlimage_1-20.png)

### 2.인증된 사용자 만들기 {#createauthuser}

**권한**&#x200B;구성 이 권한이 있는 사용자는 3단계에서 작성자에 대한 Sling 배포를 구성하는 데 사용됩니다.

* **각 게시 인스턴스**

   * 관리자 권한으로 로그인
   * 보안 [콘솔 액세스](/help/sites-administering/security.md)

      * 예: [https://localhost:4503/useradmin](https://localhost:4503/useradmin)
   * 새 사용자 만들기

      * for example, `usersync-admin`
   * 이 사용자를 사용자 그룹에 **`administrators`** 추가
   * [/home에 이 사용자에 대한 ACL 추가](#howtoaddacl)

      * `Allow jcr:all` 제한 `rep:glob=*/activities/*`



>[!CAUTION]
>
>새 사용자를 만들어야 합니다.
>
>* 할당된 기본 사용자는 **`admin`**&#x200B;입니다.
>* 사용 안 함 `communities-user-admin user.`
>



#### ACL 추가 방법 {#addacls}

* crxde Lite 액세스

   * 예: [https://localhost:4503/crx/de](https://localhost:4503/crx/de)

* select `/home` node
* 오른쪽 창에서 `Access Control` 탭을 선택합니다
* ACL 항목을 추가할 `+` 단추 선택

   * **주체**:사용자 동기화를 위해 만든 사용자 *검색*
   * **유형**: `Allow`
   * **권한**: `jcr:all`
   * **제한 사항** 표현:glob: `*/activities/*`
   * 확인 **선택**

* 모두 **저장 선택**

![](assets/chlimage_1-21.png)

참고 항목

* [액세스 권한 관리](/help/sites-administering/user-group-ac-admin.md#access-right-management)
* 문제 해결 섹션 [응답 처리 중 작업 예외 수정](#modify-operation-exception-during-response-processing).

### 3.Apache Sling 배포 전송 자격 증명 - 사용자 자격 증명 기반 DistributionTransportSecretProvider {#adobegraniteencpasswrd}

**권한 구성**

권한이 있는 사용자 **`administrators`**사용자 그룹의 구성원이 모든 게시 인스턴스에 만들어지면 작성자가 작성자로부터 게시로 사용자 데이터를 동기화할 수 있는 권한이 있는 권한이 있는 권한이 작성자가 해당 권한을 식별해야 합니다.

* **작성자**

   * 관리자 권한으로 로그인
   * 웹 [콘솔 액세스](/help/sites-deploying/configuring-osgi.md)

      * 예: [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * locate `Apache Sling Distribution Transport Credentials - User Credentials based DistributionTransportSecretProvider`
   * 편집할 기존 구성을 선택합니다(연필 아이콘)확인 `property name`: **`socialpubsync-publishUser`**

   * 2단계에서 게시 시 생성된 [인증된 사용자에게](#createauthuser) 사용자 이름과 암호를 설정합니다.

      * for example, `usersync-admin`


![](assets/chlimage_1-22.png)

### 4.Apache Sling Distribution Agent - Queue Agent Factory {#apache-sling-distribution-agent-queue-agents-factory}

**사용자 동기화 활성화**

* **게시**&#x200B;시:

   * 관리자 권한으로 로그인
   * 웹 [콘솔 액세스](/help/sites-deploying/configuring-osgi.md)

      * 예: [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)
   * locate `Apache Sling Distribution Agent - Queue Agents Factory`

      * 편집할 기존 구성을 선택합니다(연필 아이콘)확인 `Name`: `socialpubsync-reverse`

      * 확인란 선택 `Enabled`
      * select `Save`
   * 각 게시 인스턴스에 대해 **반복



![](assets/chlimage_1-23.png)

### 5.Adobe Social 동기화 - Diff Observer Factory {#diffobserver}

**그룹 동기화 사용**

* **각 게시 인스턴스에**&#x200B;대해 다음을 수행합니다.

   * 관리자 권한으로 로그인
   * 웹 [콘솔 액세스](/help/sites-deploying/configuring-osgi.md)

      * 예: [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)
   * locate **`Adobe Social Sync - Diff Observer Factory`**

      * 편집할 기존 구성 선택(연필 아이콘)

         확인 `agent name`: `socialpubsync-reverse`

      * 확인란 선택 `Enabled`
      * select `Save`


![](assets/screen-shot_2019-05-24at090809.png)

### 6.Apache Sling 배포 트리거 - 예약된 트리거 팩토리 {#apache-sling-distribution-trigger-scheduled-triggers-factory}

**(선택 사항) 폴링 간격 수정**

기본적으로 작성자는 30초마다 변경 사항을 폴링합니다. 이 간격을 변경하려면:

* **작성자**

   * 관리자 권한으로 로그인
   * 웹 [콘솔 액세스](/help/sites-deploying/configuring-osgi.md)

      * 예: [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * locate `Apache Sling Distribution Trigger - Scheduled Triggers Factory`

      * 편집할 기존 구성 선택(연필 아이콘)

         * 확인 `Name`: `socialpubsync-scheduled-trigger`
      * 원하는 `Interval in Seconds` 간격으로 설정
      * select `Save`



![](assets/chlimage_1-24.png)

## 여러 게시 인스턴스에 대한 구성 {#configure-for-multiple-publish-instances}

기본 구성은 단일 게시 인스턴스용입니다. 사용자 동기화를 활성화하는 이유는 게시 팜과 같은 여러 게시 인스턴스를 동기화하기 위해서이므로 추가 게시 인스턴스를 동기화 에이전트 팩터리에 추가해야 합니다.

### 7.Apache Sling Distribution Agent - Sync Agents Factory {#apache-sling-distribution-agent-sync-agents-factory-1}

**게시 인스턴스 추가:**

* **작성자**

   * 관리자 권한으로 로그인
   * 웹 [콘솔 액세스](/help/sites-deploying/configuring-osgi.md)

      * 예: [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * locate `Apache Sling Distribution Agent - Sync Agents Factory`

      * 편집할 기존 구성을 선택합니다(연필 아이콘)확인 `Name`: `socialpubsync`


![](assets/chlimage_1-25.png)

* **내보내기 끝점**&#x200B;각 게시자에 대한 내보내기 끝점이 있어야 합니다. 예를 들어, 2개의 발행자(localhost:4503 및 4504)가 있는 경우 2개의 항목이 있어야 합니다.

   * `https://localhost:4503/libs/sling/distribution/services/exporters/socialpubsync-reverse`
   * `https://localhost:4504/libs/sling/distribution/services/exporters/socialpubsync-reverse`

* **가져오기 끝점**&#x200B;각 게시자에 대한 가져오기 끝점이 있어야 합니다. 예를 들어, 2개의 발행자(localhost:4503 및 4504)가 있는 경우 2개의 항목이 있어야 합니다.

   * `https://localhost:4503/libs/sling/distribution/services/importers/socialpubsync`
   * `https://localhost:4504/libs/sling/distribution/services/importers/socialpubsync`

* select `Save`

### 8.AEM Communities 사용자 동기화 리스너 {#aem-communities-user-sync-listener}

**(선택 사항) 추가 JCR 노드 동기화**

여러 게시 인스턴스에서 동기화하려는 사용자 지정 데이터가 있는 경우 다음을 수행합니다.

* **각 게시 인스턴스에**&#x200B;대해 다음을 수행합니다.

   * 관리자 권한으로 로그인
   * 웹 [콘솔 액세스](/help/sites-deploying/configuring-osgi.md)

      * for example, `https://localhost:4503/system/console/configMgr`
   * locate `AEM Communities User Sync Listener`
   * 편집할 기존 구성을 선택합니다(연필 아이콘)확인 `Name`: `socialpubsync-scheduled-trigger`


![](assets/chlimage_1-26.png)

* **노드**유형 동기화할 노드 유형 목록입니다. sling:Folder 이외의 모든 노드 유형은 여기에 나열되어야 합니다(sling:folder는 별도로 처리됨).
동기화할 노드 유형의 기본 목록:

   * rep:사용자
   * nt:unstructured
   * nt:resource

* **무시**가능 속성 변경 사항이 감지되면 무시되는 속성 목록입니다. 이러한 속성에 대한 변경 사항은 다른 변경 사항의 부작용으로 동기화될 수 있지만(동기화는 항상 노드 수준에 있으므로) 이러한 속성에 대한 변경 사항은 동기화를 트리거하지 않습니다.
무시할 기본 속성:

   * cq:lastModified

* **Ignorable Nodes**동기화 중에 완전히 무시되는 하위 경로. 이러한 하위 경로 아래의 어떤 부분도 동기화되지 않습니다.
무시할 기본 노드:

   * .tokens
   * 시스템

* **Distributed Folders**Most sling:Folders는 동기화가 필요하지 않으므로 무시됩니다. 몇 가지 예외가 여기에 나열되어 있습니다.
동기화할 기본 폴더

   * 세그먼트/점수
   * 소셜/관계
   * 활동

### 9.고유 슬링 ID {#unique-sling-id}

>[!CAUTION]
>
>둘 이상의 게시 인스턴스 간에 Sling ID가 일치하면 사용자 그룹 동기화가 실패합니다.

게시 팜의 여러 게시 인스턴스에 대해 Sling ID가 동일한 경우 사용자 그룹이 동기화되지 않습니다.

각 게시 인스턴스에서 모든 Sling ID 값이 다른지 확인하려면:

1. 찾아보기 `http://<host>:<port>/system/console/status-slingsettings`
1. sling ID 값을 **확인합니다.**

![](assets/chlimage_1-27.png)

게시 인스턴스의 Sling ID가 다른 게시 인스턴스의 Sling ID와 일치하는 경우 다음을 수행합니다.

1. 일치하는 Sling ID가 있는 게시 인스턴스 중 하나를 중지합니다.
1. crx-quickstart/launchpad/felix 디렉토리에서

   * sling.id.file이라는 파일 검색 및 *삭제*

      * 예를 들어 Linux 시스템에서 다음을 수행합니다.
         `rm -i $(find . -type f -name sling.id.file)`

      * 예를 들어 Windows 시스템에서 다음을 수행합니다.
         `use windows explorer and search for *sling.id.file*`

1. 게시 인스턴스 시작

   * 시작할 때 새 Sling ID가 할당됩니다.

1. sling ID **가** 이제 고유한지 확인

모든 게시 인스턴스에 고유한 Sling ID가 있을 때까지 이 단계를 반복합니다.

## 저장소 패키지 빌더 팩토리 {#vault-package-builder-factory}

업데이트가 제대로 동기화되려면 사용자 동기화를 위해 자격 증명 모음 패키지 빌더를 수정해야 합니다.

* 각 AEM 게시 인스턴스에서
* 웹 [콘솔 액세스](/help/sites-deploying/configuring-osgi.md)

   * 예: [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* locate `Apache Sling Distribution Packaging - Vault Package Builder Factory`

   * `Builder name: socialpubsync-vlt`

* 편집 아이콘 선택
* 다음 두 가지 `Package Node Filters`추가:

   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`

* 정책 처리:

   * 기존 rep:policy 노드를 새 노드로 덮어쓰려면 세 번째 패키지 필터를 추가합니다.

      * `/home/users|+.*/rep:policy`
   * 정책이 배포되지 않도록

      * `Acl Handling:` `IGNORE`


![저장소 패키지 빌더 팩토리](assets/vault-package-builder-factory.png)

## ... {#what-happens-when}

### 사용자가 게시할 때 직접 등록 또는 편집 프로필 {#user-self-registers-or-edits-profile-on-publish}

디자인 작업에서는 게시 환경에서 만든 사용자 및 프로필(자가 등록)이 작성 환경에 나타나지 않습니다.

토폴로지가 [게시 팜이고](/help/sites-deploying/recommended-deploys.md#tarmk-farm) 사용자 동기화가 올바르게 구성된 경우 *사용자 *와 *사용자 프로필은* Sling 배포를 사용하여 게시 팜 전체에서 동기화됩니다.

### 사용자 또는 사용자 그룹은 보안 콘솔을 사용하여 만들어집니다. {#users-or-user-groups-are-created-using-security-console}

디자인 측면에서 게시 환경에서 만든 사용자 데이터는 작성 환경에 나타나지 않고 그 반대의 경우도 마찬가지입니다.

사용자 [관리 및 보안](/help/sites-administering/security.md) 콘솔을 사용하여 게시 환경에서 새 사용자를 추가하는 경우 사용자 동기화는 필요한 경우 새 사용자와 해당 그룹 구성원을 다른 게시 인스턴스와 동기화합니다. 사용자 동기화는 보안 콘솔을 통해 생성된 사용자 그룹도 동기화합니다.

## 문제 해결 {#troubleshooting}

### 사용자 동기화를 오프라인으로 전환하는 방법 {#how-to-take-user-sync-offline}

사용자 동기화를 오프라인으로 전환하려면 게시자를 [](#how-to-remove-a-publisher) 제거하거나 데이터를 [](#manually-syncing-users-and-user-groups)수동으로 동기화하려면 배포 큐가 비어 있어야 합니다.

배포 큐의 상태를 확인하려면

* 작성자:

   * crxde [Lite 사용](/help/sites-developing/developing-with-crxde-lite.md)

      * 의 항목 찾기 `/var/sling/distribution/packages`

         * 패턴으로 명명된 폴더 노드 `distrpackage_*`
   * 패키지 [관리자 사용](/help/sites-administering/package-manager.md)

      * 보류 중인 패키지(아직 설치되지 않음)를 찾습니다.

         * 패턴으로 이름 지정 `socialpubsync-vlt*`
         * created by `communities-user-admin`


배포 큐가 비어 있으면 사용자 동기화를 비활성화합니다.

* 작성자

   * *Apache Sling Distribution Agent - Sync `Enabled` [Agents Factory의 확인란 선택 취소](#apache-sling-distribution-agent-sync-agents-factory)

작업이 완료되면 사용자 동기화를 다시 활성화합니다.

* 작성자

   * apache Sling `Enabled` [Distribution Agent - Sync Agent Factory의 확인란을 선택합니다.](#apache-sling-distribution-agent-sync-agents-factory)

### 사용자 동기화 진단 {#user-sync-diagnostics}

사용자 동기화 진단은 구성을 확인하고 문제를 식별하는 도구입니다.

작성자는 기본 콘솔에서 도구, 작업, 진단, 사용자 **동기화 진단을 통해 탐색하면 됩니다.**

사용자 동기화 진단 콘솔을 입력하면 결과가 표시됩니다.

사용자 동기화를 활성화하지 않은 경우 다음과 같이 표시됩니다.

![](assets/chlimage_1-28.png)

#### 게시자에 대한 진단 실행 방법 {#how-to-run-diagnostics-for-publishers}

작성자 환경에서 진단 프로그램이 실행되면 통과/실패 결과에 확인을 위해 구성된 게시 [인스턴스] 목록을 표시하는 정보 섹션이 포함됩니다.

목록에 포함된 URL은 해당 인스턴스에 대한 진단을 실행하는 각 게시 인스턴스의 URL입니다. URL 매개 변수는 진단 URL에 `syncUser` 추가되며 이 값은 2단계에서 만든 *인증된 동기화 사용자에게* 설정됩니다 [](#createauthuser).

**참고**:url을 실행하기 전에 *인증된 동기화 사용자가* 이미 해당 게시 인스턴스에 로그인해야 합니다.

![](assets/chlimage_1-29.png)

### 구성이 부적절하게 추가됨 {#configuration-improperly-added}

사용자 동기화가 작동하지 않을 때 가장 일반적인 문제는 추가 구성이 *추가되었다는*&#x200B;것입니다. 대신 기존 *기본 구성을 *편집해야*&#x200B;합니다.

다음은 편집된 기본 구성이 웹 콘솔에 어떻게 표시되어야 하는지에 대한 보기입니다. 두 개 이상의 인스턴스가 나타나면 추가된 구성을 제거해야 합니다.

#### (작성자: Apache Sling Distribution Agent 1개 - Sync Agents Factory {#author-one-apache-sling-distribution-agent-sync-agents-factory}

![](assets/chlimage_1-30.png)

#### (author) 1개의 Apache Sling 배포 전송 자격 증명 - DistributionTransportSecretProvider 기반 사용자 자격 증명 {#author-one-apache-sling-distribution-transport-credentials-user-credentials-based-distributiontransportsecretprovider}

![](assets/chlimage_1-31.png)

#### (게시) Apache Sling Distribution Agent 1개 - Queue Agent Factory {#publish-one-apache-sling-distribution-agent-queue-agents-factory}

![](assets/chlimage_1-32.png)

#### (게시) 하나의 Adobe Social 동기화 - Diff Observer Factory {#publish-one-adobe-social-sync-diff-observer-factory}

![](assets/chlimage_1-33.png)

#### (author) 1개의 Apache Sling 배포 트리거 - 예약된 트리거 공장 {#author-one-apache-sling-distribution-trigger-scheduled-triggers-factory}

![](assets/chlimage_1-34.png)

### 응답 처리 중 작업 예외 수정 {#modify-operation-exception-during-response-processing}

로그에 다음 내용이 표시되는 경우:

`org.apache.sling.servlets.post.impl.operations.ModifyOperation Exception during response processing.`

`java.lang.IllegalStateException: This tree does not exist`

그런 다음 섹션 [2를 확인합니다. 승인된 사용자](#createauthuser) 만들기가 제대로 수행되었습니다.

이 섹션에서는 모든 게시 인스턴스에 존재하는 인증된 사용자를 만들고 작성자의 &#39;비밀 공급자&#39; OSGi 구성에서 이들을 식별하는 방법에 대해 설명합니다. 기본적으로 사용자는 `admin`입니다.

허가된 사용자는 사용자 그룹의 구성원이 되어야 하며 해당 그룹에 대한 권한은 **`administrators`** 변경하지 않아야 합니다.

허가된 사용자는 명시적으로 모든 게시 인스턴스에 대해 다음 권한 및 제한을 가져야 합니다.

| **경로** | **jcr:all** | **rep:glob** |
|---|---|---|
| /home | X | */활동/* |
| /home/users | X | */활동/* |
| /home/groups | X | */활동/* |

그룹의 구성원으로서 권한이 있는 사용자는 모든 게시 인스턴스에 대해 다음 권한을 가져야 합니다. `administrators`

| **경로** | **jcr:all** | **jcr:read** | **rep:쓰기** |
|---|---|---|---|
| /etc/packages/sling/distribution |  |  | X |
| /libs/sling/distribution |  | X |  |
| /var |  |  | X |
| /var/events |  | X | X |
| /var/sling/distribution |  | X | X |

### 사용자 그룹 동기화 실패 {#user-group-sync-failed}

둘 이상의 게시 인스턴스 간에 Sling ID가 일치하면 사용자 그룹 동기화가 실패합니다.

제 [9조를 참조하십시오. 고유 슬링 ID](#unique-sling-id)

### 사용자 및 사용자 그룹 수동 동기화 {#manually-syncing-users-and-user-groups}

* 사용자 및 사용자 그룹이 있는 게시자에서 다음을 수행합니다.

   * [활성화되면 사용자 동기화 비활성화](#how-to-take-user-sync-offline)
   * [패키지](/help/sites-administering/package-manager.md#creating-a-new-package) 만들기 `/home`

      * 패키지 편집 시

         * 필터 탭:필터 추가:루트 경로: `/home`
         * 고급 탭:AC 처리: `Overwrite`
   * [패키지 내보내기](/help/sites-administering/package-manager.md#downloading-packages-to-your-file-system)


* 다른 게시 인스턴스에 대해 다음을 수행합니다.

   * [패키지 가져오기](/help/sites-administering/package-manager.md#installing-packages)

사용자 동기화를 구성하거나 활성화하려면 1단계로 이동합니다.Apache [Sling Distribution Agent - Sync Agents Factory](#apache-sling-distribution-agent-sync-agents-factory)

### 게시자를 사용할 수 없게 되는 경우 {#when-a-publisher-becomes-unavailable}

게시 인스턴스를 사용할 수 없게 되면 나중에 다시 온라인 상태가 될 경우 해당 인스턴스를 제거하지 마십시오. 변경 내용이 게시자에 대해 대기열에 추가되고, 다시 온라인 상태가 되면 변경 사항이 처리됩니다.

게시 인스턴스가 온라인으로 다시 돌아가지 않는 경우, 게시 인스턴스가 영구적으로 오프라인 상태인 경우, 큐 증가로 인해 작성 환경에서 눈에 띄는 디스크 공간 사용이 발생하므로 해당 인스턴스를 제거해야 합니다.

게시자가 다운되면 작성자 로그에는 다음과 유사한 예외가 발생합니다.

```
28.01.2016 15:57:48.475 ERROR
 [pool-12-thread-34-org_apache_sling_distribution_queue_socialpubsync_endpoint1
 (org/apache/sling/distribution/queue/socialpubsync/endpoint1)]
 org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync] could not deliver package distrpackage_1454014575838_a2b45ec8-0400-42f3-bed8-ae09b66381cb
 org.apache.sling.distribution.packaging.DistributionPackageImportException: failed in importing package ...
```

### 게시자를 제거하는 방법 {#how-to-remove-a-publisher}

Apache Sling Distribution Agent - Sync [Agents Factory에서](#apache-sling-distribution-agent-sync-agents-factory)게시자를 제거하려면 배포 큐가 비어 있어야 합니다.

* 작성자:

   * [오프라인으로 사용자 동기화](#how-to-take-user-sync-offline)
   * 두 서버 목록에서 게시자를 제거하려면 [7단계를 수행합니다](#apache-sling-distribution-agent-sync-agents-factory) .

      * `Exporter Endpoints`
      * `Importer Endpoints`
   * 사용자 동기화 다시 활성화

      * apache Sling `Enabled` [Distribution Agent - Sync Agent Factory의 확인란을 선택합니다.](#apache-sling-distribution-agent-sync-agents-factory)
