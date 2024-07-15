---
title: 커뮤니티 사용자 동기화
description: Adobe Experience Manager 커뮤니티에서 사용자 동기화가 작동하는 방식을 알아봅니다.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: ecd30f5d-ad31-4482-96d3-c92f1cf91336
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2403'
ht-degree: 0%

---

# 커뮤니티 사용자 동기화 {#communities-user-synchronization}

## 소개 {#introduction}

Adobe Experience Manager(AEM) 커뮤니티에서 Publish 환경(구성된 권한에 따라)의 *사이트 방문자*&#x200B;는 *구성원*&#x200B;이 되고, *사용자 그룹*&#x200B;을 만들고, *구성원 프로필*&#x200B;을 편집할 수 있습니다.

*사용자 데이터*&#x200B;이(가) *사용자*, *사용자 프로필* 및 *사용자 그룹*&#x200B;을(를) 참조합니다.

*구성원*&#x200B;은(는) 작성 환경에 등록된 사용자와 반대로 Publish 환경에 등록된 *사용자*&#x200B;을(를) 참조합니다.

사용자 데이터에 대한 자세한 내용을 보려면 [사용자 및 사용자 그룹 관리](/help/communities/users.md)를 방문하세요.

## Publish 팜 전체에서 사용자 동기화 {#synchronizing-users-across-a-publish-farm}

Publish 환경에서 만든 사용자 데이터는 작성자 환경에 표시되지 않습니다.

작성자 환경에서 생성된 대부분의 사용자 데이터는 작성자 환경에 남아 있도록 만들어지며 동기화되거나 Publish 인스턴스에 복제되지 않습니다.

[토폴로지](/help/communities/topologies.md)이(가) [게시 팜](/help/sites-deploying/recommended-deploys.md#tarmk-farm)인 경우 한 Publish 인스턴스에서 수행한 등록 및 수정 내용은 다른 Publish 인스턴스와 동기화되어야 합니다. 구성원은 모든 Publish 노드에 로그인하고 해당 데이터를 볼 수 있어야 합니다.

사용자 동기화가 활성화되면 팜의 Publish 인스턴스 간에 사용자 데이터가 자동으로 동기화됩니다.

### 사용자 동기화 설정 지침 {#user-sync-setup-instructions}

게시 팜에서 동기화를 활성화하는 방법에 대한 자세한 단계별 지침은 [사용자 동기화](/help/sites-administering/sync.md)를 참조하십시오.

## 백그라운드에서 사용자 동기화 {#user-sync-in-the-background}

![sling-dist-workflow](assets/sling-dist-workflow.png)

* **vlt 패키지**

  게시자에서 수행한 모든 변경 사항의 zip 파일이며 게시자 간에 배포되어야 합니다. 게시자의 변경 사항은 변경 이벤트 리스너가 선택하는 이벤트를 생성합니다. 이렇게 하면 모든 변경 사항이 포함된 vlt 패키지가 만들어집니다.

* **배포 패키지**

  여기에는 Sling에 대한 배포 정보가 포함되어 있습니다. 콘텐츠가 배포되어야 하는 위치와 마지막으로 배포된 시기에 대한 정보입니다.

## 다음의 경우 발생하는 일... {#what-happens-when}

### 커뮤니티 사이트 콘솔의 Publish 사이트 {#publish-site-from-communities-sites-console}

작성자의 경우 커뮤니티 사이트가 [커뮤니티 사이트 콘솔](/help/communities/sites-console.md)에서 게시되면 관련 페이지를 [복제](/help/sites-deploying/configuring.md#replication-reverse-replication-and-replication-agents)하고 Sling에서 구성원 자격을 포함하여 동적으로 만든 커뮤니티 사용자 그룹을 배포하는 효과가 있습니다.

### Publish에서 사용자가 만들어지거나 프로필을 편집합니다. {#user-is-created-or-edits-profile-on-publish}

기본적으로 Publish 환경에서 만든 사용자 및 프로필(예: 자가 등록, 소셜 로그인, LDAP 인증)은 작성자 환경에 표시되지 않습니다.

토폴로지가 [게시 팜](/help/communities/topologies.md)이고 사용자 동기화가 올바르게 구성된 경우 *사용자* 및 *사용자 프로필*&#x200B;이(가) Sling 배포를 사용하여 게시 팜 전반에서 동기화됩니다.

### Publish에 새 커뮤니티 그룹이 생성됨 {#new-community-group-is-created-on-publish}

Publish 인스턴스에서 시작되지만 새 사이트 페이지 및 새 사용자 그룹을 생성하는 커뮤니티 그룹 생성이 실제로 작성자 인스턴스에서 발생합니다.

프로세스의 일부로 새 사이트 페이지가 모든 Publish 인스턴스에 복제됩니다. 동적으로 생성된 커뮤니티 사용자 그룹과 해당 멤버십은 모든 Publish 인스턴스에 배포되는 Sling입니다.

### 사용자 또는 사용자 그룹은 보안 콘솔을 사용하여 만들어집니다 {#users-or-user-groups-are-created-using-security-console}

기본적으로 게시 환경에서 생성된 사용자 데이터는 작성자 환경에 표시되지 않으며 이와 반대로 표시됩니다.

[사용자 관리 및 보안](/help/sites-administering/security.md) 콘솔을 사용하여 게시 환경에 새 사용자를 추가하면 사용자 동기화는 필요한 경우 새 사용자와 해당 그룹 구성원을 다른 게시 인스턴스와 동기화합니다. 또한 사용자 동기화는 보안 콘솔을 통해 만든 사용자 그룹을 동기화합니다.

### 사용자가 Publish에 콘텐츠를 게시함 {#user-posts-content-on-publish}

UGC(사용자 생성 콘텐츠)의 경우 게시 인스턴스에 입력된 데이터는 [구성된 SRP](/help/communities/srp-config.md)를 통해 액세스됩니다.

## 모범 사례 {#bestpractices}

기본적으로 사용자 동기화는 **사용 안 함**&#x200B;입니다. 사용자 동기화를 활성화하면 *기존* OSGi 구성을 수정하는 작업이 포함됩니다. 사용자 동기화를 활성화한 결과 새 구성을 추가하지 않아야 합니다.

사용자 데이터는 작성자에 작성되지 않더라도 사용자 동기화는 작성자 환경에 의존하여 사용자 데이터 배포를 관리합니다.

**전제 조건**

1. 사용자 및 사용자 그룹이 한 게시자에서 이미 만들어진 경우 사용자 동기화를 구성하고 활성화하기 전에 사용자 데이터를 모든 게시자에게 [수동으로 동기화](/help/sites-administering/sync.md#manually-syncing-users-and-user-groups)하는 것이 좋습니다.

   사용자 동기화가 활성화되면 새로 생성된 사용자 및 그룹만 동기화 됩니다.

1. 최신 코드가 설치되었는지 확인합니다.

   * [AEM 플랫폼 업데이트](https://helpx.adobe.com/kr/experience-manager/kb/aem62-available-hotfixes.html)
   * [AEM Communities 업데이트](/help/communities/deploy-communities.md#latestfeaturepack)

AEM Communities에서 사용자 동기화를 활성화하려면 다음 구성이 필요합니다. 슬링 컨텐츠 배포가 실패하지 않도록 이러한 구성이 올바른지 확인하십시오.

### Apache Sling 배포 에이전트 - 동기화 에이전트 팩토리 {#apache-sling-distribution-agent-sync-agents-factory}

이 구성은 게시자 간에 동기화할 콘텐츠를 가져옵니다. 구성은 작성자 인스턴스에 있습니다. Author는 거기에 있는 모든 게시자와 모든 정보를 동기화할 위치를 추적해야 합니다.

구성의 기본값은 단일 게시 인스턴스에 대한 것입니다. 사용자 동기화는 게시 팜의 경우와 같이 여러 게시 인스턴스를 동기화하는 데 유용하므로 구성에 추가 게시 인스턴스를 추가해야 합니다.

**컨텐츠가 어떻게 동기화됩니까?**

작성자 인스턴스가 게시자의 내보내기 끝점을 ping합니다. 특정 게시자(n)에서 사용자가 만들어지거나 업데이트될 때마다 작성자는 내보내기 끝점에서 콘텐츠를 가져오고 [콘텐츠를 다른 게시자(콘텐츠를 가져오는 게시자와 떨어진 n-1)로 ](/help/communities/sync.md#main-pars-image-1413756164)을(를) 푸시합니다.

Apache Sling 동기화 에이전트 구성을 구성하려면 다음 작업을 수행하십시오.

1. AEM 작성자 인스턴스에 대한 관리자 권한으로 로그인합니다.
1. [웹 콘솔](/help/sites-deploying/configuring-osgi.md)에 액세스합니다. 예: [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. **Apache Sling 배포 에이전트 - 동기화 에이전트 팩토리**&#x200B;를 찾습니다.

   * 편집을 위해 열 기존 구성을 선택합니다(연필 아이콘).

     이름 확인: **socialpubsync.**

   * **활성화** 확인란을 선택합니다.
   * **여러 큐 사용**&#x200B;을 선택합니다.
   * **내보내기 끝점** 및 **가져오기 끝점**&#x200B;을 지정하십시오(더 많은 내보내기 및 가져오기 끝점을 추가할 수 있음).

     이러한 엔드포인트는 콘텐츠를 가져올 위치와 콘텐츠를 푸시할 위치를 정의합니다. 작성자는 지정된 내보내기 끝점의 콘텐츠를 가져오고 해당 콘텐츠를 가져온 게시자가 아닌 게시자에게 푸시합니다.

   ![sync-agent-fact](assets/sync-agent-fact.png)

### Adobe Granite 배포 - 암호화된 암호 전송 비밀 공급자 {#adobe-granite-distribution-encrypted-password-transport-secret-provider}

이를 통해 작성자는 승인된 사용자를 식별하고, 사용자 데이터를 작성자에서 게시로 동기화할 수 있는 권한을 갖습니다.

모든 게시 인스턴스에서 [인증된 사용자가 만들어짐](/help/sites-administering/sync.md#createauthuser)을 통해 게시자는 작성자와 연결하고 작성자의 Sling 배포를 구성할 수 있습니다. 이 권한이 부여된 사용자는 모든 필수 [ACL](/help/sites-administering/sync.md#howtoaddacl)을(를) 가지고 있습니다.

게시자에 데이터를 설치하거나 게시자로부터 가져올 때마다 작성자는 이 구성에 설정된 자격 증명(사용자 이름 및 암호)을 사용하여 게시자와 연결합니다.

인증된 사용자를 사용하여 작성자와 게시자를 연결하려면:

1. AEM 작성자 인스턴스에 대한 관리자 권한으로 로그인합니다.
1. [웹 콘솔](/help/sites-deploying/configuring-osgi.md)에 액세스합니다.

   예: [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. **Adobe Granite 배포 - 암호화된 암호 전송 비밀 공급자를 찾습니다.**
1. 편집을 위해 열 기존 구성을 선택합니다(연필 아이콘).

   **socialpubsync** 속성 확인 - **publishUser.**

1. 사용자 이름과 암호를 [인증된 사용자](/help/sites-administering/sync.md#createauthorizeduser)(으)로 설정합니다.

   예: **usersync - admin**

![granite-paswrd-trans](assets/granite-paswrd-trans.png)

### Apache Sling 배포 에이전트 - 큐 에이전트 팩토리 {#apache-sling-distribution-agent-queue-agents-factory}

이 구성은 게시자 간에 동기화할 데이터를 구성하는 데 사용됩니다. **허용된 루트**&#x200B;에 지정된 경로에 데이터가 생성/업데이트되면 &quot;var/community/distribution/diff&quot;가 활성화되고 생성된 복제기가 게시자의 데이터를 가져와서 다른 게시자에 설치합니다.

동기화할 데이터(노드 경로)를 구성하려면 다음을 수행합니다.

1. 게시 인스턴스에 대한 관리자 권한으로 로그인합니다.
1. [웹 콘솔](/help/sites-deploying/configuring-osgi.md)에 액세스합니다.

   예: [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

1. **Apache Sling 배포 에이전트 - 큐 에이전트 팩터리**&#x200B;를 찾습니다.
1. 편집을 위해 열 기존 구성을 선택합니다(연필 아이콘).

   이름 확인: **socialpubsync -reverse**

1. **사용** 확인란을 선택하고 저장합니다.
1. **허용된 루트**&#x200B;에서 복제할 노드 경로를 지정하십시오.
1. 각 **게시** 인스턴스에 대해 이 작업을 반복합니다.

   ![queue-agents-fact](assets/queue-agents-fact.png)

### Adobe Granite 배포 - 차이점 옵저버 팩토리 {#adobe-granite-distribution-diff-observer-factory}

이 구성은 게시자 간 그룹 멤버십을 동기화합니다.
한 게시자의 그룹 구성원을 변경해도 다른 게시자의 그룹 구성원이 업데이트되지 않으면 **ref :members**&#x200B;이(가) **보이는 속성 이름**&#x200B;에 추가되었는지 확인하십시오.

멤버 동기화를 보장하려면 다음을 수행합니다.

1. 게시 인스턴스에 대한 관리자 권한으로 로그인합니다.
1. [웹 콘솔](/help/sites-deploying/configuring-osgi.md)에 액세스합니다.

   예: [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

1. **Adobe Granite 배포 - 비교 옵저버 팩토리**&#x200B;를 찾습니다.
1. 편집을 위해 열 기존 구성을 선택합니다(연필 아이콘).

   **에이전트 이름: socialpubsync -reverse**&#x200B;를 확인합니다.

1. **활성화** 확인란을 선택합니다.
1. **보이는 속성 이름**&#x200B;에서 **rep:members**&#x200B;을(를) propertyName에 대한 설명으로 지정하고 저장합니다.

   ![diff-obs](assets/diff-obs.png)

### Apache Sling 배포 트리거 - 예약된 트리거 팩토리 {#apache-sling-distribution-trigger-scheduled-triggers-factory}

이 구성을 사용하면 게시자 간에 변경 사항을 동기화하기 위해 폴링 간격(게시자를 핑하고 작성자가 변경 사항을 끌어온 후)을 구성할 수 있습니다.

작성자는 30초마다(기본값) 게시자를 폴링합니다. `/var/sling/distribution/packages/  socialpubsync -  vlt /shared` 폴더에 패키지가 있으면 해당 패키지를 가져와서 다른 게시자에 설치합니다.

폴링 간격을 변경하려면:

1. AEM 작성자 인스턴스에 대한 관리자 권한으로 로그인합니다.
1. [웹 콘솔](/help/sites-deploying/configuring-osgi.md)에 액세스(예: [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr))
1. **Apache Sling 배포 트리거 - 예약된 트리거 팩토리**&#x200B;를 찾습니다.

   * 편집을 위해 열 기존 구성을 선택합니다(연필 아이콘).

     **socialpubsync -scheduled-trigger** 확인

   * 간격(초)을 원하는 간격으로 설정하고 저장합니다.

   ![예약된 트리거](assets/scheduled-trigger.png)

### AEM Communities 사용자 동기화 수신기 {#aem-communities-user-sync-listener}

구독과 다음에 불일치가 있는 Sling 배포의 문제에 대해 **AEM Communities 사용자 동기화 수신기** 구성의 다음 속성이 설정되었는지 확인하십시오.

* 노드 유형
* Ignorable 속성
* IgnorableNodes
* 분산 폴더

구독, 팔로우 및 알림을 동기화하려면

각 AEM 게시 인스턴스에서 다음을 수행합니다.

1. 관리자 권한으로 로그인합니다.
1. [웹 콘솔](/help/sites-deploying/configuring-osgi.md)에 액세스합니다. 예: [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).
1. **AEM Communities 사용자 동기화 수신기**&#x200B;를 찾습니다.
1. 편집을 위해 열 기존 구성 선택(연필 아이콘)

   이름 확인: **socialpubsync -scheduled-trigger**

1. 다음 **NodeTypes**&#x200B;을(를) 설정합니다.

   `rep:User`

   `nt:unstructured`

   `nt:resource`

   `rep:ACL`

   `sling:Folder`

   `sling:OrderedFolder`

   이 속성에 지정된 노드 유형은 동기화되며 알림 정보(블로그 및 구성 추종)는 서로 다른 게시자 간에 동기화됩니다.

1. **DistributedFolders**&#x200B;에서 동기화할 모든 폴더를 추가하십시오. 예:

   `segments/scoring`

   `social/relationships`

   `activities`

1. **ignorablenodes**&#x200B;을(를) 다음으로 설정:

   `.tokens`

   `system`

   `rep:cache`(고정 세션이 사용되므로 이 노드를 다른 게시자와 동기화할 필요가 없습니다.)

   ![user-sync-listner](assets/user-sync-listner.png)

### 고유 Sling ID {#unique-sling-id}

AEM 작성자 인스턴스는 Sling ID를 사용하여 데이터가 들어오는 위치와 패키지를 다시 전송해야 하는(또는 전송할 필요가 없는) 게시자를 식별합니다.

게시 팜의 모든 게시자에 고유한 Sling ID가 있는지 확인하십시오. 게시 팜의 여러 게시 인스턴스에 대해 Sling ID가 동일하면 사용자 동기화가 실패합니다. 작성자는 어디에서 패키지를 가져올 수 있고 패키지를 설치할 수 있는 위치를 알 수 없습니다.

게시 팜에 있는 게시자의 고유한 Sling ID를 각 Publish 인스턴스에서 확인하려면 다음을 수행하십시오.

1. [https://_host:port_/system/console/status-slingsettings](https://localhost:4503/system/console/status-slingsettings)(으)로 이동합니다.
1. **Sling ID**&#x200B;의 값을 확인하십시오.

   ![slingid](assets/slingid.png)

   Publish 인스턴스의 Sling ID가 다른 Publish 인스턴스의 Sling ID와 일치하는 경우 다음을 수행합니다.

1. Sling ID가 일치하는 Publish 인스턴스 중 하나를 중지합니다.
1. `crx-quickstart/launchpad/felix` 디렉터리에서 이름이 *sling.id.file.*&#x200B;인 파일을 검색하고 삭제합니다.

   예를 들어 Linux 시스템의 경우:

   `rm -i $(find . -type f -name sling.id.file)`

   예를 들어 Windows 시스템의 경우:

   Windows 탐색기를 사용하여 `sling.id.file` 검색

1. Publish 인스턴스를 시작합니다. 시작 시 새 Sling ID가 할당됩니다.
1. **Sling ID**&#x200B;이(가) 이제 고유한지 확인합니다.

모든 Publish 인스턴스에 고유한 Sling ID가 있을 때까지 이 단계를 반복합니다.

### Vault 패키지 빌더 팩토리 {#vault-package-builder-factory}

업데이트가 제대로 동기화되려면 사용자 동기화를 위해 저장소 패키지 빌더를 수정해야 합니다.
`/home/users`에서 `*/rep:cache` 노드가 만들어집니다. 노드의 주체 이름을 쿼리하는 경우 이 캐시를 직접 사용할 수 있음을 찾는 데 사용되는 캐시입니다.

게시자 간에 `rep :cache`개의 노드가 동기화되는 경우 사용자 동기화를 중지할 수 있습니다.

게시자 간에 각 AEM Publish 인스턴스에서 업데이트가 제대로 동기화되도록 하려면 다음을 수행하십시오.

1. [웹 콘솔 액세스](/help/sites-deploying/configuring-osgi.md)

   예: [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).
1. **Apache Sling 배포 패키징 - Vault 패키지 빌더 팩토리**&#x200B;를 찾습니다.

   빌더 이름: socialpubsync-vlt.

1. 편집 아이콘을 선택합니다.
1. 두 개의 패키지 노드 필터 추가:
   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`
1. 정책 처리
   * 기존 rep:policy 노드를 새 노드로 덮어쓰려면 세 번째 패키지 필터 `/home/users|+.*/rep:policy`을(를) 추가합니다.
   * 정책이 배포되지 않도록 하려면 다음을 설정하십시오. `Acl Handling: IGNORE`

   ![자격 증명 모음 패키지 빌더 팩터리](assets/vault-package-builder-factory.png)

## AEM Communities의 Sling 배포 문제 해결 {#troubleshoot-sling-distribution-in-aem-communities}

Sling 배포가 실패하면 다음 디버깅 단계를 시도해 보십시오.

1. **잘못 추가된 구성 [확인](/help/sites-administering/sync.md#improperconfig)**

   여러 구성이 추가되거나 편집되지 않았는지 확인하고, 대신 기존 기본 구성을 편집해야 합니다.
1. **구성 확인**

   [모범 사례](/help/communities/sync.md#main-pars-header-863110628)에서 설명한 대로 모든 [구성](/help/communities/sync.md#bestpractices)이 AEM 작성자 인스턴스에 적절히 설정되어 있는지 확인하십시오.

1. **인증된 사용자 권한 확인**

   패키지가 제대로 설치되지 않은 경우 첫 번째 Publish 인스턴스에서 만든 [승인된 사용자](/help/sites-administering/sync.md#createauthuser)에 올바른 ACL이 있는지 확인합니다.

   이를 확인하려면 [생성된 권한 있는 사용자](/help/sites-administering/sync.md#createauthuser) 대신 관리자 사용자 자격 증명을 사용하도록 작성자 인스턴스에서 [Adobe Granite 배포 - 암호화된 암호 전송 비밀 공급자](/help/sites-administering/sync.md#adobegraniteencpasswrd) 구성을 변경합니다. 이제 패키지를 다시 설치해 보십시오. 사용자 동기화가 관리자 자격 증명으로 제대로 작동하는 경우 생성된 게시 사용자에게 적절한 ACL이 없음을 의미합니다.

1. **비교 관찰자 팩터리 구성 확인**

   게시 팜 전체에서 특정 노드만 동기화되지 않는 경우(예: 그룹 멤버가 동기화되지 않는 경우) [Adobe Granite 배포 - 비교 관찰자 팩터리](/help/sites-administering/sync.md#diffobserver) 구성이 활성화되어 있고 **rep: members**&#x200B;이 **보이는 속성 이름**&#x200B;에 설정되어 있는지 확인하십시오.

1. **AEM Communities 사용자 동기화 수신기 구성을 확인하십시오.** 생성된 사용자가 동기화되었지만 구독과 다음이 작동하지 않는 경우 AEM Communities 사용자 동기화 수신기 구성에 다음이 있는지 확인하십시오.

   * 노드 유형- **rep:User, nt:unstructured**, **nt:resource**, **rep:ACL**, **sling:Folder** 및 **sling:OrderedFolder**(으)로 설정됩니다.
   * Ignorable 노드- **.tokens**, **system** 및 **rep :cache**(으)로 설정됩니다.
   * 분산 폴더 - 분산할 폴더로 설정합니다.

1. **Publish 인스턴스에서 사용자 생성 시 생성된 로그 확인**

   위의 구성이 적절히 설정되었지만 사용자 동기화가 작동하지 않는 경우 사용자 생성 시 생성된 로그를 확인합니다.

   다음과 같이 로그 순서가 동일한지 확인합니다.

   ```shell
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7422] com.adobe.cq.social.sync.impl.PublisherSyncServiceImpl Handing these paths to the distribution subsystem: [/home/users/C, /home/users/C/Cw-5avWqilmqsNn5hCvK]
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7422] org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync-reverse] REQUEST-START DSTRQ2: ADD paths=[/home/users/C, /home/users/C/Cw-5avWqilmqsNn5hCvK], user=communities-user-admin
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7431] com.adobe.cq.social.sync.impl.PublisherSyncServiceImpl Handing these paths to the distribution subsystem: [/home/users/C/Cw-5avWqilmqsNn5hCvK, /home/users/C/Cw-5avWqilmqsNn5hCvK/profile, /home/users/C/Cw-5avWqilmqsNn5hCvK/rep:policy]
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7431] org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync-reverse] REQUEST-START DSTRQ3: ADD paths=[/home/users/C/Cw-5avWqilmqsNn5hCvK, /home/users/C/Cw-5avWqilmqsNn5hCvK/profile, /home/users/C/Cw-5avWqilmqsNn5hCvK/rep:policy], user=communities-user-admin
   15.05.2016 18:33:01.757 *INFO* [sling-oak-observation-7431] org.apache.jackrabbit.vault.packaging.impl.JcrPackageDefinitionImpl unwrapping package sling/distribution:socialpubsync-vlt_1463337181554_ebb27ad9-a861-4405-9342-d64c916654e2:0.0.1
   15.05.2016 18:33:01.820 *INFO* [sling-oak-observation-7422] org.apache.jackrabbit.vault.packaging.impl.JcrPackageDefinitionImpl unwrapping package sling/distribution:socialpubsync-vlt_1463337181554_58811273-5861-48fe-95d2-4aff367b99c3:0.0.1
   15.05.2016 18:33:02.023 *INFO* [sling-oak-observation-7430] com.adobe.cq.social.sync.impl.PublisherSyncServiceImpl Handing these paths to the distribution subsystem: [/home/users/C/Cw-5avWqilmqsNn5hCvK/profile]
   15.05.2016 18:33:02.023 *INFO* [sling-oak-observation-7430] org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync-reverse] REQUEST-START DSTRQ4: ADD paths=[/home/users/C/Cw-5avWqilmqsNn5hCvK/profile], user=communities-user-admin
   15.05.2016 18:33:02.273 *INFO* [sling-oak-observation-7430] org.apache.jackrabbit.vault.packaging.impl.JcrPackageDefinitionImpl unwrapping package sling/distribution:socialpubsync-vlt_1463337182039_f34f4fa6-10b9-42eb-8740-4da9d4d38f99:0.0.1
   ```

디버그하려면:

1. 사용자 동기화 비활성화:
1. AEM 작성자 인스턴스에서 관리자 권한으로 로그인합니다.

   1. [웹 콘솔](/help/sites-deploying/configuring-osgi.md)에 액세스합니다. 예: [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. **Apache Sling 배포 에이전트 - 동기화 에이전트 팩토리** 구성을 찾습니다.
   1. **사용** 확인란의 선택을 취소하십시오.

      작성자 인스턴스(내보내기 및 가져오기) 엔드포인트에서 사용자 동기화를 비활성화하면 비활성화되고 작성자 인스턴스가 정적입니다. 작성자가 **vlt** 패키지를 ping하거나 가져오지 않았습니다.

      이제 게시 인스턴스에 사용자가 만들어지면 **vlt** 패키지가 */var/sling/distribution/packages/ socialpubsync - vlt /data* 노드에 만들어집니다. 그리고 작성자가 이러한 패키지를 다른 서비스로 푸시하는 경우. 이 데이터를 다운로드하고 추출하여 다른 서비스에 푸시된 모든 속성이 무엇인지 확인할 수 있습니다.

1. 게시자로 이동하여 게시자에서 사용자를 만듭니다. 그 결과 이벤트가 생성됩니다.
1. 사용자 생성 시 생성된 [로그 순서](/help/communities/sync.md#troubleshoot-sling-distribution-in-aem-communities)를 확인하십시오.
1. **/var/sling/distribution/packages/socialpubsync-vlt/data**&#x200B;에 **vlt** 패키지가 만들어졌는지 확인하십시오.
1. 이제 AEM 작성자 인스턴스에서 사용자 동기화를 활성화합니다.
1. 게시자의 경우 **Apache Sling 배포 에이전트 - 동기화 에이전트 팩토리**에서 내보내기 또는 가져오기 끝점을 변경합니다.
패키지 데이터를 다운로드하고 추출하여 다른 게시자에게 푸시된 모든 속성과 손실된 데이터를 확인할 수 있습니다.
