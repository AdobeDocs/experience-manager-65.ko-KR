---
title: 커뮤니티 사용자 동기화
seo-title: 커뮤니티 사용자 동기화
description: 사용자 동기화 작동 방식
seo-description: 사용자 동기화 작동 방식
uuid: 772b82bd-a66c-4c1d-b80b-dcff77c873a3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 97286c2c-f6e3-43ec-b1a9-2abb58616778
docset: aem65
role: Administrator
exl-id: ecd30f5d-ad31-4482-96d3-c92f1cf91336
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2509'
ht-degree: 0%

---

# 커뮤니티 사용자 동기화 {#communities-user-synchronization}

## 소개 {#introduction}

AEM Communities의 게시 환경(구성된 권한에 따라)에서 *사이트 방문자*&#x200B;는 *구성원*&#x200B;이 되고, *사용자 그룹*&#x200B;을 만들고, 해당 *구성원 프로필*&#x200B;을 편집할 수 있습니다.

*사용자* 데이터는  *사용자*,  *사용자 프로필 및* 사용자 그룹 *을 참조하는 데 사용되는*&#x200B;용어입니다.

** 멤버십은 작성 환경에  ** 등록된 사용자와 비교하여 게시 환경에 등록된 사용자를 참조하는 데 사용되는 용어입니다.

사용자 데이터에 대한 자세한 내용은 [사용자 및 사용자 그룹 관리](/help/communities/users.md)를 참조하십시오.

## 게시 팜 {#synchronizing-users-across-a-publish-farm}에서 사용자 동기화

계획적으로 게시 환경에서 생성된 사용자 데이터는 작성 환경에 표시되지 않습니다.

작성 환경에서 생성된 대부분의 사용자 데이터는 작성 환경에 유지되기 위한 것이며, 게시 인스턴스에 동기화되거나 복제되지 않습니다.

[토폴로지](/help/communities/topologies.md)가 [게시 팜](/help/sites-deploying/recommended-deploys.md#tarmk-farm)인 경우, 한 게시 인스턴스에서 수행한 등록 및 수정 사항은 다른 게시 인스턴스와 동기화해야 합니다. 구성원은 로그인하여 모든 게시 노드에서 해당 데이터를 볼 수 있어야 합니다.

사용자 동기화가 활성화되면 팜의 게시 인스턴스 간에 사용자 데이터가 자동으로 동기화됩니다.

### 사용자 동기화 설정 지침 {#user-sync-setup-instructions}

게시 팜 간에 동기화를 활성화하는 방법에 대한 자세한 단계별 지침은 다음을 참조하십시오.

* [사용자 동기화](/help/sites-administering/sync.md)

## 백그라운드 {#user-sync-in-the-background}에서 사용자 동기화

![sling-dist-workflow](assets/sling-dist-workflow.png)

* **vlt 패키지**

   게시자에서 수행한 모든 변경 사항의 zip 파일입니다. 이 파일은 게시자에게 배포해야 합니다. 게시자에 대한 변경 사항은 변경 이벤트 리스너에 의해 선택된 이벤트를 생성합니다. 이렇게 하면 모든 변경 사항이 포함된 vlt 패키지가 만들어집니다.

* **배포 패키지**

   여기에는 Sling에 대한 배포 정보가 포함되어 있습니다. 컨텐츠의 배포 위치와 마지막 배포 시기에 대한 정보입니다.

## .. {#what-happens-when}

### 커뮤니티 사이트 콘솔에서 사이트 게시 {#publish-site-from-communities-sites-console}

작성자의 경우, 커뮤니티 사이트가 [커뮤니티 사이트 콘솔](/help/communities/sites-console.md)에서 게시되면 그 효과는 연결된 페이지를 [복제](/help/sites-deploying/configuring.md#replication-reverse-replication-and-replication-agents)하고, Sling은 해당 구성원을 포함하여 동적으로 생성된 커뮤니티 사용자 그룹을 배포합니다.

### 사용자가 게시 {#user-is-created-or-edits-profile-on-publish}에 있는 프로필을 만들거나 편집합니다.

디자인별로, 게시 환경에서 만든 사용자 및 프로필(예: 자가 등록, 소셜 로그인, LDAP 인증)은 작성 환경에 표시되지 않습니다.

토폴로지가 [게시 팜](/help/communities/topologies.md)이고 사용자 동기화가 올바르게 구성된 경우 *사용자* 및 *사용자 프로필*&#x200B;이 Sling 배포를 사용하여 게시 팜 간에 동기화됩니다.

### 게시 {#new-community-group-is-created-on-publish}에 새 커뮤니티 그룹이 만들어집니다.

게시 인스턴스에서 시작되었지만 새 사이트 페이지와 새 사용자 그룹을 만드는 커뮤니티 그룹 만들기가 실제로 작성자 인스턴스에서 발생합니다.

프로세스의 일부로, 새 사이트 페이지가 모든 게시 인스턴스에 복제됩니다. 동적으로 생성된 커뮤니티 사용자 그룹 및 해당 멤버십은 모든 게시 인스턴스에 Sling이 배포됩니다.

### 사용자 또는 사용자 그룹은 보안 콘솔 {#users-or-user-groups-are-created-using-security-console}을 사용하여 만들어집니다.

디자인에서 게시 환경에서 만든 사용자 데이터는 작성 환경에 나타나지 않고 그 반대의 경우도 마찬가지입니다.

[사용자 관리 및 보안](/help/sites-administering/security.md) 콘솔을 사용하여 게시 환경에서 새 사용자를 추가하면 사용자 동기화는 필요한 경우 새 사용자와 해당 그룹 구성원을 다른 게시 인스턴스와 동기화합니다. 사용자 동기화는 보안 콘솔을 통해 생성된 사용자 그룹도 동기화합니다.

### 사용자가 게시 {#user-posts-content-on-publish}에 컨텐츠를 게시합니다.

UGC(사용자 생성 컨텐츠)의 경우 게시 인스턴스에 입력된 데이터는 [구성된 SRP](/help/communities/srp-config.md)을 통해 액세스합니다.

## 우수 사례 {#bestpractices}

기본적으로 사용자 동기화는 **disabled**&#x200B;입니다. 사용자 동기화를 활성화하려면 *기존* OSGi 구성을 수정해야 합니다. 사용자 동기화를 활성화한 결과로 새 구성을 추가할 필요가 없습니다.

사용자 동기화는 사용자 데이터가 작성자에 대해 만들어지지 않았더라도 작성 환경을 사용하여 사용자 데이터 배포를 관리합니다.

**전제 조건**

1. 사용자 및 사용자 그룹이 이미 하나의 게시자에서 생성된 경우 사용자 동기화를 구성 및 활성화하기 전에 [사용자 데이터를 모든 게시자에게 수동으로 동기화하는 것이 좋습니다](/help/sites-administering/sync.md#manually-syncing-users-and-user-groups).

   사용자 동기화가 활성화되면 새로 만든 사용자와 그룹만 동기화됩니다.

1. 최신 코드가 설치되어 있는지 확인합니다.

   * [AEM 플랫폼 업데이트](https://helpx.adobe.com/kr/experience-manager/kb/aem62-available-hotfixes.html)
   * [AEM Communities 업데이트](/help/communities/deploy-communities.md#latestfeaturepack)

AEM Communities에서 사용자 동기화를 활성화하려면 다음 구성이 필요합니다. Sling 컨텐츠 배포가 실패하지 않도록 이러한 구성이 올바른지 확인하십시오.

### Apache Sling Distribution Agent - Sync Agent Factory {#apache-sling-distribution-agent-sync-agents-factory}

이 구성은 게시자에서 동기화할 컨텐츠를 가져옵니다. 작성자 인스턴스에 구성이 있습니다. 작성자는 그곳에 있는 모든 게시자와 모든 정보를 동기화할 위치를 추적해야 합니다.

구성의 기본값은 단일 게시 인스턴스에 대한 것입니다. 사용자 동기화는 게시 팜과 같은 여러 게시 인스턴스를 동기화하는 데 유용하므로 구성에 추가 게시 인스턴스를 추가해야 합니다.

**컨텐츠는 어떻게 동기화됩니까?**

작성자 인스턴스가 게시자의 내보내기 끝점을 ping합니다. 특정 게시자에서 사용자가 생성되거나 업데이트될 때마다(n) 작성자는 내보내기 끝점의 컨텐츠를 가져오고 [컨텐츠를 가져오는 게시자와 분리된 다른 게시자(n-1)로 푸시합니다.](/help/communities/sync.md#main-pars-image-1413756164)

Apache Sling 동기화 에이전트 구성을 구성하려면 다음을 수행하십시오.

1. AEM 작성자 인스턴스에 대한 관리자 권한으로 로그인합니다.
1. [웹 콘솔](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html)에 액세스합니다. 예: [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. **Apache Sling Distribution Agent - Sync Agent Factory**&#x200B;를 찾습니다.

   * 편집할 기존 구성을 선택합니다(연필 아이콘).

      이름 확인:**socialpubsync**

   * **Enabled** 확인란을 선택합니다.
   * **여러 큐 사용**&#x200B;을 선택합니다.
   * **내보내기 끝점** 및 **가져오기 끝점**&#x200B;을(를) 지정합니다(내보내기 및 가져오기 끝점을 더 추가할 수 있음).

      이러한 종단점은 콘텐츠를 가져올 위치와 콘텐츠를 푸시할 위치를 정의합니다. 작성자는 지정된 내보내기 끝점의 컨텐츠를 가져오고 콘텐츠를 가져온 게시자 이외의 게시자에게 푸시합니다.
   ![sync-agent-fact](assets/sync-agent-fact.png)

### Adobe Granite 배포 - 암호화된 암호 전송 암호 공급자 {#adobe-granite-distribution-encrypted-password-transport-secret-provider}

이를 통해 작성자는 작성자의 사용자 데이터를 게시로 동기화할 수 있는 권한이 있는 인증된 사용자를 식별할 수 있습니다.

모든 게시 인스턴스에서 만든 [인증된 사용자는 게시자가 작성자와 연결하고 작성자에 대한 Sling 배포를 구성하는 데 도움이 됩니다. ](/help/sites-administering/sync.md#createauthuser) 이 승인된 사용자에게는 모든 필수 [ACL](/help/sites-administering/sync.md#howtoaddacl)이 있습니다.

게시자에서 데이터를 설치하거나 가져올 때마다 작성자는 이 구성에 설정된 자격 증명(사용자 이름 및 암호)을 사용하여 게시자와 연결합니다.

인증된 사용자를 사용하여 작성자와 게시자를 연결하려면

1. AEM 작성자 인스턴스에 대한 관리자 권한으로 로그인합니다.
1. [웹 콘솔](/help/sites-deploying/configuring-osgi.md)에 액세스합니다.

   예: [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. **Adobe Granite 배포 - 암호화된 암호 전송 암호 공급자를 찾습니다.**
1. 편집할 기존 구성을 선택합니다(연필 아이콘).

   속성 **socialpubsync** - **publishUser.** 확인

1. 사용자 이름과 암호를 [인증된 사용자](/help/sites-administering/sync.md#createauthorizeduser)로 설정합니다.

   예: **usersync - admin**

![granite-paswrd-trans](assets/granite-paswrd-trans.png)

### Apache Sling Distribution Agent - Queue Agent Factory {#apache-sling-distribution-agent-queue-agents-factory}

이 구성은 게시자 간에 동기화할 데이터를 구성하는 데 사용됩니다. 데이터가 **허용된 루트**&#x200B;에 지정된 경로에 생성/업데이트되면 &quot;var/community/distribution/diff&quot;가 활성화되고 생성된 복제기가 게시자의 데이터를 가져와 다른 게시자에 설치합니다.

동기화할 데이터(노드 경로)를 구성하려면 다음을 수행합니다.

1. 작성자 인스턴스에 대한 관리자 권한으로 로그인합니다.
1. [웹 콘솔](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html)에 액세스합니다.

   예: [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

1. **Apache Sling Distribution Agent - Queue Agent Factory**&#x200B;를 찾습니다.
1. 편집할 기존 구성을 선택합니다(연필 아이콘).

   이름 확인:**socialpubsync -reverse**

1. **활성화됨** 확인란을 선택하고 저장합니다.
1. **허용되는 루트**&#x200B;에 복제할 노드 경로를 지정합니다.
1. 각 **publish** 인스턴스에 대해 이 작업을 반복합니다.

   ![queue-agent-fact](assets/queue-agents-fact.png)

### Adobe Granite 배포 - Diff Observer Factory {#adobe-granite-distribution-diff-observer-factory}

이 구성은 게시자에서 그룹 구성원을 동기화합니다.
한 게시자에서 그룹의 구성원을 변경해도 다른 게시자에 대한 구성원 자격이 업데이트되지 않는 경우 **ref:members**&#x200B;이 **looked properties names**&#x200B;에 추가되었는지 확인하십시오.

멤버 동기화를 확인하려면

1. AEM 작성자 인스턴스에 대한 관리자 권한으로 로그인합니다.
1. [웹 콘솔](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html)에 액세스합니다.

   예: [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

1. **Granite Distribution - Diff Observer Factory**&#x200B;를 찾습니다.
1. 편집할 기존 구성을 선택합니다(연필 아이콘).

   **에이전트 이름을 확인합니다.socialpubsync -reverse**

1. **Enabled** 확인란을 선택합니다.
1. **rep:members**&#x200B;은 **looked properties names**&#x200B;에서 propertyName에 대한 설명으로 지정하고 저장합니다.

   ![diff-job](assets/diff-obs.png)

### Apache Sling 배포 트리거 - 예약된 트리거 팩토리 {#apache-sling-distribution-trigger-scheduled-triggers-factory}

이 구성을 사용하면 폴링 간격(게시자에 대해 ping을 수행하고 작성자가 변경 사항을 가져오는 시점)을 구성하여 게시자 간에 변경 사항을 동기화할 수 있습니다.

작성자는 30초(기본값)마다 게시자를 폴링합니다. `/var/sling/distribution/packages/  socialpubsync -  vlt /shared` 폴더에 패키지가 있으면 해당 패키지를 가져와서 다른 게시자에 설치합니다.

폴링 간격을 변경하려면

1. AEM 작성자 인스턴스에 대한 관리자 권한으로 로그인합니다.
1. [웹 콘솔](/help/sites-deploying/configuring-osgi.md)에 액세스합니다. 예: [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. **Apache Sling Distribution Trigger - 예약된 트리거 Factory**&#x200B;를 찾습니다.

   * 편집할 기존 구성을 선택합니다(연필 아이콘).

      **socialpubsync -scheduled-trigger** 확인

   * 간격(초)을 원하는 간격으로 설정하고 저장합니다.

   ![예약된 트리거](assets/scheduled-trigger.png)

### AEM Communities 사용자 동기화 수신기 {#aem-communities-user-sync-listener}

구독과 다음에 일치하지 않는 Sling 배포의 문제가 있으면 **AEM Communities User Sync Listener** 구성에서 다음 속성이 설정되어 있는지 확인하십시오.

* NodeTypes
* IgnorableProperties
* IgnorableNodes
* 분산 폴더

구독, 다음 및 알림을 동기화하려면

각 AEM 게시 인스턴스에서 다음을 수행합니다.

1. 관리자 권한으로 로그인합니다.
1. [웹 콘솔](/help/sites-deploying/configuring-osgi.md)에 액세스합니다. 예: [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)
1. **AEM Communities 사용자 동기화 수신기**&#x200B;를 찾습니다.
1. 편집할 기존 구성을 선택합니다(연필 아이콘).

   이름 확인:**socialpubsync-scheduled-trigger**

1. 다음 **NodeTypes**&#x200B;을 설정합니다.

   `rep:User`

   `nt:unstructured`

   `nt:resource`

   `rep:ACL`

   `sling:Folder`

   `sling:OrderedFolder`

   이 속성에 지정된 노드 유형은 동기화되며 알림 정보(블로그 및 구성 후)는 다른 게시자 간에 동기화됩니다.

1. **DistributedFolders**&#x200B;에서 동기화할 모든 폴더를 추가합니다. 예,

   `segments/scoring`

   `social/relationships`

   `activities`

1. **ignorenodes**&#x200B;를 다음과 같이 설정합니다.

   `.tokens`

   `system`

   `rep:cache` 고정 세션을 사용하므로 이 노드를 다른 게시자와 동기화할 필요가 없습니다.

   ![user-sync-listner](assets/user-sync-listner.png)

### 고유한 Sling ID {#unique-sling-id}

AEM 작성자 인스턴스는 Sling ID를 사용하여 데이터가 오고 있는 게시자와 패키지를 다시 보내야 하는 게시자를 식별합니다.

게시 팜의 모든 게시자에 고유한 Sling ID가 있는지 확인합니다. 게시 팜의 여러 게시 인스턴스에 대해 Sling ID가 동일한 경우 사용자 동기화가 실패합니다. 작성자는 패키지를 가져올 위치와 패키지를 설치할 위치를 알 수 없으므로

게시 팜에 있는 게시자의 고유한 Sling ID를 확인하려면 각 게시 인스턴스에서 다음을 수행합니다.

1. [https://_host:port_/system/console/status-slingsettings](https://localhost:4503/system/console/status-slingsettings)로 이동합니다.
1. **Sling ID** 값을 확인합니다.

   ![slingid](assets/slingid.png)

   게시 인스턴스의 Sling ID가 다른 게시 인스턴스의 Sling ID와 일치하는 경우 다음을 수행합니다.

1. 일치하는 Sling ID가 있는 게시 인스턴스 중 하나를 중지합니다.
1. `crx-quickstart/launchpad/felix` 디렉토리에서 *sling.id.file.* 파일을 검색하고 삭제합니다

   예를 들어 Linux 시스템의 경우

   `rm -i $(find . -type f -name sling.id.file)`

   예를 들어 Windows 시스템에서

   Windows 탐색기를 사용하고 `sling.id.file` 검색

1. 게시 인스턴스를 시작합니다. 시작 시 새 Sling ID가 할당됩니다.
1. 이제 **Sling ID**&#x200B;가 고유한지 확인합니다.

모든 게시 인스턴스에 고유한 Sling ID가 있을 때까지 이 단계를 반복합니다.

### 저장소 패키지 빌더 팩토리 {#vault-package-builder-factory}

업데이트가 제대로 동기화되려면 사용자 동기화를 위해 자격 증명 모음 패키지 빌더를 수정해야 합니다.
`/home/users`에 `*/rep:cache` 노드가 만들어집니다. 이 캐시는 노드의 주도자 이름에 쿼리하는 경우 이 캐시를 직접 사용할 수 있음을 찾는 데 사용됩니다.

`rep :cache` 노드가 게시자 간에 동기화되면 사용자 동기화를 중지할 수 있습니다.

게시자에서 업데이트가 제대로 동기화되도록 하려면 각 AEM 게시 인스턴스에서 다음을 수행합니다.

1. [웹 콘솔](/help/sites-deploying/configuring-osgi.md)에 액세스

   예: [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)
1. **Apache Sling Distribution Packaging - Vault Package Builder Factory**&#x200B;를 찾습니다.

   빌더 이름:socialpubsync-vlt

1. 편집 아이콘을 선택합니다.
1. 패키지 노드 필터 두 개를 추가합니다.
   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`
1. 정책 처리
   * 기존 rep:policy 노드를 새 노드로 덮어쓰려면 세 번째 패키지 필터를 추가합니다.`/home/users|+.*/rep:policy`
   * 정책이 배포되지 않도록 하려면 다음을 설정합니다.`Acl Handling: IGNORE`

   ![저장소 패키지 빌더 팩토리](assets/vault-package-builder-factory.png)

## AEM Communities {#troubleshoot-sling-distribution-in-aem-communities}의 Sling 배포 문제 해결

Sling 배포가 실패하면 다음 디버깅 단계를 시도하십시오.

1. **잘못  [추가된 구성을 확인합니다](/help/sites-administering/sync.md#improperconfig)**

   여러 구성을 추가하거나 편집하지 않고 기존 기본 구성을 편집해야 합니다.
1. **구성 확인**

   [우수 사례](/help/communities/sync.md#main-pars-header-863110628)에 설명된 대로 모든 [구성](/help/communities/sync.md#bestpractices)이 AEM 작성자 인스턴스에 적절히 설정되어 있는지 확인하십시오.

1. **인증된 사용자 권한 확인**

   패키지가 제대로 설치되지 않은 경우 첫 번째 게시 인스턴스에서 만든 [인증된 사용자](/help/sites-administering/sync.md#createauthuser)에 올바른 ACL이 있는지 확인합니다.

   유효성을 검사하려면 만든 [인증된 사용자](/help/sites-administering/sync.md#createauthuser) 대신 관리자 사용자 자격 증명을 사용하도록 작성자 인스턴스에서 [Adobe Granite Distribution - 암호화된 암호 전송 암호 공급자](/help/sites-administering/sync.md#adobegraniteencpasswrd) 구성을 변경합니다. 이제 패키지를 다시 설치해 보십시오. 사용자 동기화가 관리자 자격 증명과 잘 작동하면 생성된 게시 사용자에게 적절한 ACL이 없음을 의미합니다.

1. **Diff Observer Factory 구성 확인**

   게시 팜에서 특정 노드만 동기화되지 않는 경우(예: 그룹 구성원이 동기화되지 않는 경우) [Granite Distribution - Diff Observer Factory](/help/sites-administering/sync.md#diffobserver) 구성이 활성화되고 **rep:**&#x200B;멤버&#x200B;**가 속성 이름**&#x200B;에 설정되어 있습니다.

1. **AEM Communities 사용자 동기화 리스너 구성을 확인합니다.** 생성된 사용자가 동기화되지만 구독 및 후속 항목이 작동하지 않는 경우 AEM Communities 사용자 동기화 리스너 구성에 다음이 있는지 확인하십시오.

   * 노드 유형 - **rep:User, nt:un구조화되지 않음**, **nt:resource**, **rep:ACL**, **sling:Folder** 및 **sling:OrderedFolder**&#x200B;로 설정됩니다.
   * Ignorable 노드 - **.tokens**, **시스템** 및 **rep:cache**&#x200B;로 설정됩니다.
   * 분산 폴더 - 분배할 폴더로 설정합니다.

1. **게시 인스턴스에서 사용자 생성 시 생성된 로그를 확인합니다**

   위의 구성이 적절하게 설정되었지만 사용자 동기화가 작동하지 않는 경우 사용자 생성 시 생성된 로그를 확인하십시오.

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

디버깅하려면:

1. 사용자 동기화를 사용하지 않도록 설정합니다.
1. AEM 작성자 인스턴스에서 관리자 권한으로 로그인합니다.

   1. [웹 콘솔](/help/sites-deploying/configuring-osgi.md)에 액세스합니다. 예: [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   1. 구성 **Apache Sling Distribution Agent - Sync Agent Factory**&#x200B;를 찾습니다.
   1. **Enabled** 확인란을 선택 취소합니다.

      작성자 인스턴스에서 사용자 동기화를 사용하지 않도록 설정할 때(내보내기 및 가져오기) 종단점이 비활성화되고 작성자 인스턴스가 정적 인스턴스입니다. 작성자가 **vlt** 패키지를 ping 또는 가져오지 않습니다.

      이제 사용자가 게시 인스턴스에 작성되면 **vlt** 패키지가 */var/sling/distribution/packages/ socialpubsync - vlt /data* 노드에 생성됩니다. 그리고 이러한 패키지가 작성자가 다른 서비스에 푸시하는 경우 이 데이터를 다운로드하고 추출하여 다른 서비스에 푸시되는 모든 속성을 확인할 수 있습니다.

1. 게시자로 이동하여 게시자에 사용자를 만듭니다. 따라서 이벤트가 만들어집니다.
1. 사용자 생성 시 생성된 로그](/help/communities/sync.md#troubleshoot-sling-distribution-in-aem-communities)의 [순서를 확인합니다.
1. **vlt** 패키지가 **/var/sling/distribution/packages/socialpubsync-vlt/data**&#x200B;에 생성되었는지 확인합니다.
1. 이제 AEM 작성자 인스턴스에서 사용자 동기화를 활성화합니다.
1. 게시자에서 **Apache Sling Distribution Agent - Sync Agent Factory**에서 내보내기 또는 가져오기 종단점을 변경합니다.
패키지 데이터를 다운로드하고 추출하여 다른 게시자에게 푸시되는 모든 속성과 손실된 데이터를 확인할 수 있습니다.
