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
role: 관리자
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2510'
ht-degree: 0%

---


# 커뮤니티 사용자 동기화 {#communities-user-synchronization}

## 소개 {#introduction}

AEM Communities의 게시 환경에서(구성된 권한에 따라) *사이트 방문자*&#x200B;는 *구성원*&#x200B;이 될 수 있으며 *사용자 그룹*&#x200B;을 만들고 *멤버 프로필*&#x200B;을 편집할 수 있습니다.

*사용자* 데이터는  *사용자*,  *사용자 프로필 및* 사용자 그룹을 참조하는 데 사용되는  ** 용어입니다.

*멤버* 는 작성 환경에  ** 등록된 사용자와 달리 게시 환경에 등록된 사용자를 참조하는 데 사용되는 용어입니다.

사용자 데이터에 대한 자세한 내용은 [사용자 및 사용자 그룹 관리](/help/communities/users.md)를 참조하십시오.

## 게시 팜 {#synchronizing-users-across-a-publish-farm}에서 사용자 동기화

기본적으로 게시 환경에서 만든 사용자 데이터는 작성 환경에 나타나지 않습니다.

작성 환경에서 만들어진 대부분의 사용자 데이터는 작성 환경에 유지되도록 되어 있으며, 인스턴스를 게시하도록 동기화되거나 복제되지 않습니다.

[토폴로지](/help/communities/topologies.md)가 [게시 팜](/help/sites-deploying/recommended-deploys.md#tarmk-farm)인 경우 한 게시 인스턴스에서 수행된 등록 및 수정 사항은 다른 게시 인스턴스와 동기화해야 합니다. 멤버는 로그인하여 게시 노드에서 해당 데이터를 볼 수 있어야 합니다.

사용자 동기화가 활성화되면 팜의 게시 인스턴스 간에 사용자 데이터가 자동으로 동기화됩니다.

### 사용자 동기화 설정 지침 {#user-sync-setup-instructions}

게시 팜에서 동기화를 활성화하는 방법에 대한 자세한 단계별 지침은 다음을 참조하십시오.

* [사용자 동기화](/help/sites-administering/sync.md)

## 백그라운드 {#user-sync-in-the-background}에서 사용자 동기화

![sling-dist-workflow](assets/sling-dist-workflow.png)

* **vlt 패키지**

   게시자에서 수행된 모든 변경 사항의 zip 파일로, 게시자 간에 배포해야 합니다. 게시자를 변경하면 변경 이벤트 리스너가 선택하는 이벤트가 생성됩니다. 이렇게 하면 모든 변경 사항이 포함된 vlt 패키지가 만들어집니다.

* **배포 패키지**

   여기에는 Sling에 대한 배포 정보가 포함되어 있습니다. 컨텐츠가 배포되어야 하는 위치와 마지막으로 배포된 시기에 대한 정보입니다.

## .. {#what-happens-when} 시 발생하는 작업

### 커뮤니티 사이트 콘솔에서 사이트 게시 {#publish-site-from-communities-sites-console}

작성자의 경우 커뮤니티 사이트가 [커뮤니티 사이트 콘솔](/help/communities/sites-console.md)에서 게시되면 연관된 페이지를 [복제할 수 있으며 Sling은 멤버십을 포함하여 동적으로 생성된 커뮤니티 사용자 그룹을 배포합니다.](/help/sites-deploying/configuring.md#replication-reverse-replication-and-replication-agents)

### 사용자가 작성되었거나 게시 {#user-is-created-or-edits-profile-on-publish}에서 프로필을 편집합니다.

직접 등록, 소셜 로그인, LDAP 인증 등의 게시 환경에서 만들어진 사용자 및 프로필은 작성 환경에 표시되지 않습니다.

토폴로지가 [게시 팜](/help/communities/topologies.md)이고 사용자 동기화가 올바르게 구성된 경우 *사용자* 및 *사용자 프로필*&#x200B;이 Sling 배포를 사용하여 게시 팜에서 동기화됩니다.

### 게시 {#new-community-group-is-created-on-publish}에 새 커뮤니티 그룹이 만들어집니다.

게시 인스턴스에서 시작되지만 커뮤니티 그룹 만들기는 새 사이트 페이지와 새 사용자 그룹을 만듭니다. 이 작업은 작성자 인스턴스에서 실제로 발생합니다.

프로세스의 일부로 새 사이트 페이지가 모든 게시 인스턴스에 복제됩니다. 동적으로 생성된 커뮤니티 사용자 그룹 및 해당 멤버십은 모든 게시 인스턴스에 Sling이 배포됩니다.

### 사용자 또는 사용자 그룹은 보안 콘솔 {#users-or-user-groups-are-created-using-security-console}을(를) 사용하여 만들어집니다.

기본적으로 게시 환경에서 만든 사용자 데이터는 작성 환경에 나타나지 않고 그 반대의 경우도 마찬가지입니다.

[사용자 관리 및 보안](/help/sites-administering/security.md) 콘솔을 사용하여 게시 환경에서 새 사용자를 추가하는 경우 사용자 동기화는 필요한 경우 새 사용자와 해당 그룹 구성원을 다른 게시 인스턴스와 동기화합니다. 사용자 동기화는 보안 콘솔을 통해 만든 사용자 그룹도 동기화합니다.

### 사용자가 게시 {#user-posts-content-on-publish}에 컨텐츠를 게시합니다.

사용자가 생성한 콘텐츠(UGC)의 경우, 게시 인스턴스에 입력된 데이터는 [구성된 SRP](/help/communities/srp-config.md)을 통해 액세스합니다.

## 우수 사례 {#bestpractices}

기본적으로 사용자 동기화는 **disabled**&#x200B;입니다. 사용자 동기화 활성화에는 *기존* OSGi 구성을 수정하는 작업이 포함됩니다. 사용자 동기화를 활성화한 결과로 새 구성을 추가할 필요가 없습니다.

사용자 동기화는 작성 환경에 의존하여 사용자 데이터가 작성자에 만들어지지 않더라도 사용자 데이터 배포를 관리합니다.

**전제 조건**

1. 사용자 및 사용자 그룹이 한 게시자에 이미 만들어져 있는 경우 사용자 동기화를 구성하고 활성화하기 전에 사용자 데이터를 모든 게시자에게 [수동으로 동기화](/help/sites-administering/sync.md#manually-syncing-users-and-user-groups)하는 것이 좋습니다.

   사용자 동기화가 활성화되면 새로 만든 사용자 및 그룹만 동기화됩니다.

1. 최신 코드가 설치되었는지 확인합니다.

   * [AEM 플랫폼 업데이트](https://helpx.adobe.com/experience-manager/kb/aem62-available-hotfixes.html)
   * [AEM Communities 업데이트](/help/communities/deploy-communities.md#latestfeaturepack)

AEM Communities에서 사용자 동기화를 사용하려면 다음 구성이 필요합니다. 이러한 구성이 정확한지 확인하여 컨텐츠 배포 실패가 발생하지 않도록 하십시오.

### Apache Sling 배포 에이전트 - 동기화 에이전트 팩토리 {#apache-sling-distribution-agent-sync-agents-factory}

이 구성은 발행자 간에 동기화할 컨텐츠를 가져옵니다. 구성은 작성자 인스턴스에 있습니다. 작성자는 그곳에 있는 모든 게시자와 모든 정보를 동기화할 위치를 추적해야 합니다.

구성의 기본값은 단일 게시 인스턴스용입니다. 사용자 동기화는 게시 팜과 같은 여러 게시 인스턴스를 동기화하는 데 유용하므로 구성에 추가 게시 인스턴스를 추가해야 합니다.

**컨텐츠는 어떻게 동기화됩니까?**

작성자 인스턴스가 게시자의 내보내기 끝점을 호출합니다. 특정 게시자에 대해 사용자가 작성되거나 업데이트될 때마다(n) 작성자는 내보내기 끝점에서 컨텐츠를 가져오고 [컨텐트](/help/communities/sync.md#main-pars-image-1413756164)를 다른 게시자(컨텐츠를 가져오는 게시자와 별개의 n-1)로 푸시합니다.

Apache Sling 동기화 에이전트 구성을 구성하려면:

1. AEM 작성자 인스턴스에서 관리자 권한으로 로그인합니다.
1. [웹 콘솔](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html)에 액세스합니다. 예: [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. **Apache Sling Distribution Agent - Sync Agents Factory**&#x200B;를 찾습니다.

   * 편집할 기존 구성을 선택합니다(연필 아이콘).

      이름 확인:**socialpubsync**

   * **활성화됨** 확인란을 선택합니다.
   * **여러 큐 사용**&#x200B;을 선택합니다.
   * **내보내기 끝점** 및 **가져오기 끝점**&#x200B;을(를) 지정합니다. 내보내기 및 가져오기 끝점을 더 추가할 수 있습니다.

      이러한 끝점은 콘텐츠를 가져올 위치와 콘텐츠를 푸시할 위치를 정의합니다. 작성자는 지정된 내보내기 끝점의 컨텐츠를 가져오고 해당 컨텐츠를 게시자(컨텐츠를 가져온 게시자 제외)로 푸시합니다.
   ![sync-agent-fact](assets/sync-agent-fact.png)

### Adobe Granite 배포 - 암호화된 암호 전송 암호 공급자 {#adobe-granite-distribution-encrypted-password-transport-secret-provider}

작성자가 작성자의 사용자 데이터를 동기화하여 게시할 수 있는 권한이 있으므로 권한이 있는 사용자를 식별할 수 있습니다.

모든 게시 인스턴스에 대해 [권한이 있는 사용자가 ](/help/sites-administering/sync.md#createauthuser)을(를) 작성자와 연결하고 작성자에 대한 Sling 배포를 구성하는 데 도움이 됩니다. 이 인가된 사용자는 모든 필수 [ACL](/help/sites-administering/sync.md#howtoaddacl)을(를) 가지고 있습니다.

게시자에서 데이터를 설치하거나 가져올 때마다 작성자는 이 구성에서 설정된 자격 증명(사용자 이름 및 암호)을 사용하여 게시자와 연결됩니다.

권한이 있는 사용자를 사용하여 작성자를 게시자와 연결하려면:

1. AEM 작성자 인스턴스에서 관리자 권한으로 로그인합니다.
1. [웹 콘솔](/help/sites-deploying/configuring-osgi.md)에 액세스합니다.

   예: [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. **Adobe Granite Distribution - 암호화된 암호 전송 비밀 공급자를 찾습니다.**
1. 편집할 기존 구성을 선택합니다(연필 아이콘).

   속성 **socialpubsync** - **publishUser.**

1. 사용자 이름 및 암호를 [승인된 사용자](/help/sites-administering/sync.md#createauthorizeduser)로 설정합니다.

   예: **usersync - admin**

![granite-paswrd-trans](assets/granite-paswrd-trans.png)

### Apache Sling 배포 에이전트 - 큐 에이전트 팩토리 {#apache-sling-distribution-agent-queue-agents-factory}

이 구성은 게시자 간에 동기화할 데이터를 구성하는 데 사용됩니다. **허용되는 루트**&#x200B;에 지정된 경로에 데이터가 생성/업데이트되면 &quot;var/community/distribution/diff&quot;가 활성화되고 생성된 복제기가 게시자의 데이터를 가져와서 다른 게시자에 설치합니다.

동기화할 데이터(노드 경로)를 구성하려면:

1. 작성자 인스턴스에서 관리자 권한으로 로그인합니다.
1. [웹 콘솔](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html)에 액세스합니다.

   예: [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

1. **Apache Sling Distribution Agent - Queue Agent Factory**&#x200B;를 찾습니다.
1. 편집할 기존 구성을 선택합니다(연필 아이콘).

   이름 확인:**socialpubsync -reverse**

1. **활성화됨** 확인란을 선택하고 저장합니다.
1. **허용되는 루트**&#x200B;에서 복제할 노드 경로를 지정합니다.
1. 각 **publish** 인스턴스에 대해 반복합니다.

   ![queue-agent-fact](assets/queue-agents-fact.png)

### Adobe Granite Distribution - Diff Observer Factory {#adobe-granite-distribution-diff-observer-factory}

이 구성은 게시자 간에 그룹 구성원을 동기화합니다.
한 게시자에서 그룹 멤버십을 변경하면 다른 게시자에 대한 멤버십이 업데이트되지 않는 경우 **ref:members**&#x200B;이(가) **look 속성 이름**&#x200B;에 추가되었는지 확인하십시오.

멤버 동기화를 확인하려면 다음을 수행하십시오.

1. AEM 작성자 인스턴스에서 관리자 권한으로 로그인합니다.
1. [웹 콘솔](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html)에 액세스합니다.

   예: [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

1. **Adobe Granite Distribution - Diff Observer Factory**&#x200B;를 찾습니다.
1. 편집할 기존 구성을 선택합니다(연필 아이콘).

   **에이전트 이름 확인:socialpubsync -reverse**.

1. **활성화됨** 확인란을 선택합니다.
1. **rep:members**&#x200B;은 **looked 속성 이름** 및 [저장]에서 propertyName에 대한 설명으로 지정합니다.

   ![diff 작업](assets/diff-obs.png)

### Apache Sling 배포 트리거 - 예약된 트리거 팩토리 {#apache-sling-distribution-trigger-scheduled-triggers-factory}

이 구성을 사용하여 폴링 간격(게시자를 핑하고 작성자가 변경 사항을 가져오는 시간)을 구성하여 게시자 간의 변경 사항을 동기화할 수 있습니다.

작성자는 30초마다 게시자를 폴링합니다(기본값). `/var/sling/distribution/packages/  socialpubsync -  vlt /shared` 폴더에 패키지가 있으면 해당 패키지를 가져와 다른 게시자에 설치합니다.

폴링 간격을 변경하려면:

1. AEM 작성자 인스턴스에서 관리자 권한으로 로그인합니다.
1. [웹 콘솔](/help/sites-deploying/configuring-osgi.md)액세스(예: [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr))
1. **Apache Sling 배포 트리거 - 예약된 트리거 팩토리** 찾기

   * 편집할 기존 구성을 선택합니다(연필 아이콘).

      **socialpubsync -scheduled-trigger** 확인

   * 간격(초)을 원하는 간격으로 설정하고 저장합니다.

   ![예약 트리거](assets/scheduled-trigger.png)

### AEM Communities 사용자 동기화 수신기 {#aem-communities-user-sync-listener}

구독 및 다음에 차이가 있는 Sling 배포의 문제는 **AEM Communities 사용자 동기화 리스너** 구성에서 다음 속성이 설정되어 있는지 확인하십시오.

* NodeTypes
* IgnorableProperties
* IgnorableNodes
* DistributedFolders

구독, 팔로우 및 알림을 동기화하려면

각 AEM 게시 인스턴스에서:

1. 관리자 권한으로 로그인합니다.
1. [웹 콘솔](/help/sites-deploying/configuring-osgi.md)에 액세스합니다. 예: [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).
1. **AEM Communities 사용자 동기화 리스너**&#x200B;를 찾습니다.
1. 편집할 기존 구성을 선택합니다(연필 아이콘).

   이름 확인:**socialpubsync -scheduled-trigger**

1. 다음 **NodeTypes**&#x200B;을 설정합니다.

   `rep:User`

   `nt:unstructured`

   `nt:resource`

   `rep:ACL`

   `sling:Folder`

   `sling:OrderedFolder`

   이 속성에 지정된 노드 유형은 동기화되고 알림 정보(블로그 및 구성 후)는 다른 게시자 간에 동기화됩니다.

1. 동기화할 모든 폴더를 **DistributedFolders**&#x200B;에 추가합니다. 예,

   `segments/scoring`

   `social/relationships`

   `activities`

1. **ignorable**&#x200B;을(를) 다음으로 설정합니다.

   `.tokens`

   `system`

   `rep:cache` 고정 세션을 사용하기 때문에 이 노드를 다른 게시자와 동기화할 필요가 없습니다.

   ![user-sync-listener](assets/user-sync-listner.png)

### 고유 슬링 ID {#unique-sling-id}

AEM 작성자 인스턴스는 Sling ID를 사용하여 데이터가 들어오는 위치와 패키지를 다시 보내야 하는 게시자를 식별할 수 있습니다(또는 그렇지 않음).

게시 팜의 모든 게시자에 고유한 Sling ID가 있는지 확인합니다. 게시 팜의 여러 게시 인스턴스에 대해 Sling ID가 동일한 경우 사용자 동기화가 실패합니다. 작성자는 패키지를 가져올 위치 및 패키지를 설치할 위치를 알 수 없으므로

게시 팜에 있는 게시자의 고유한 Sling ID를 확인하려면 각 게시 인스턴스에서 다음을 수행합니다.

1. [https://_host:port_/system/console/status-slingsettings](https://localhost:4503/system/console/status-slingsettings)로 이동합니다.
1. **Sling ID**&#x200B;의 값을 확인합니다.

   ![slingid](assets/slingid.png)

   게시 인스턴스의 Sling ID가 다른 게시 인스턴스의 Sling ID와 일치하는 경우 다음을 수행합니다.

1. 일치하는 Sling ID가 있는 게시 인스턴스 중 하나를 중지합니다.
1. `crx-quickstart/launchpad/felix` 디렉토리에서 *sling.id.file.* 파일을 검색하고 삭제합니다.

   예를 들어 Linux 시스템에서 다음을 수행합니다.

   `rm -i $(find . -type f -name sling.id.file)`

   예를 들어 Windows 시스템에서 다음을 수행합니다.

   Windows 탐색기를 사용하고 `sling.id.file` 검색

1. 게시 인스턴스를 시작합니다. 시작할 때 새 Sling ID가 할당됩니다.
1. **Sling ID**&#x200B;가 이제 고유한지 확인합니다.

모든 게시 인스턴스에 고유한 Sling ID가 있을 때까지 이 단계를 반복합니다.

### 저장소 패키지 빌더 팩토리 {#vault-package-builder-factory}

업데이트를 제대로 동기화하려면 사용자 동기화를 위해 자격 증명 모음 패키지 빌더를 수정해야 합니다.
`/home/users`에서 `*/rep:cache` 노드가 만들어집니다. 노드의 주체 이름에 쿼리하면 이 캐시를 직접 사용할 수 있음을 찾는 데 사용되는 캐시입니다.

게시자 간에 `rep :cache` 노드가 동기화되면 사용자 동기화를 중지할 수 있습니다.

업데이트가 발행자 간에 제대로 동기화되도록 하려면 각 AEM 게시 인스턴스에서 다음을 수행합니다.

1. [웹 콘솔](/help/sites-deploying/configuring-osgi.md)에 액세스

   예: [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).
1. **Apache Sling 배포 패키징 - Vault 패키지 빌더 팩토리**&#x200B;를 찾습니다.

   빌더 이름:socialpubsync-vlt

1. 편집 아이콘을 선택합니다.
1. 2개의 패키지 노드 필터 추가:
   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`
1. 정책 처리
   * 기존 rep:policy 노드를 새 것으로 덮어쓰려면 세 번째 패키지 필터를 추가합니다.`/home/users|+.*/rep:policy`
   * 정책이 배포되지 않도록 하려면 다음을 설정합니다.`Acl Handling: IGNORE`

   ![저장소 패키지 빌더 팩토리](assets/vault-package-builder-factory.png)

## AEM Communities {#troubleshoot-sling-distribution-in-aem-communities}의 Sling 배포 문제 해결

Sling 배포가 실패할 경우 다음 디버깅 단계를 시도하십시오.

1. **부적절하게  [추가된 구성 확인](/help/sites-administering/sync.md#improperconfig)**

   여러 구성을 추가 또는 편집하지 않고 기존 기본 구성을 편집해야 합니다.
1. **구성 확인**

   [우수 사례](/help/communities/sync.md#main-pars-header-863110628)에 명시된 대로 모든 [구성](/help/communities/sync.md#bestpractices)이(가) AEM 작성자 인스턴스에서 적절히 설정되어 있는지 확인합니다.

1. **권한이 있는 사용자 권한 확인**

   패키지가 제대로 설치되지 않은 경우 첫 번째 게시 인스턴스에서 만든 [승인된 사용자](/help/sites-administering/sync.md#createauthuser)에 올바른 ACL이 있는지 확인하십시오.

   이 유효성을 확인하려면 [만든 권한이 있는 사용자](/help/sites-administering/sync.md#createauthuser) 대신 관리자 사용자 자격 증명을 사용하도록 작성자 인스턴스에서 [Adobe Granite Distribution - Encrypted Password Transport Secret 공급자](/help/sites-administering/sync.md#adobegraniteencpasswrd) 구성을 변경하십시오. 이제 패키지를 다시 설치해 보십시오. 사용자 동기화가 관리자 자격 증명과 제대로 작동하면 만든 게시 사용자에게 적절한 ACL이 없음을 의미합니다.

1. **비교 옵서버 팩토리 구성 확인**

   게시 팜에서 특정 노드만 동기화되지 않는 경우(예: 그룹 구성원이 동기화되지 않은 경우) [Adobe Granite Distribution - Diff Observer Factory](/help/sites-administering/sync.md#diffobserver) 구성이 활성화되어 있고 **rep:멤버**&#x200B;은 **looked 속성 이름**&#x200B;에 설정됩니다.

1. **AEM Communities 사용자 동기화 리스너 구성을 확인합니다.** 생성된 사용자가 동기화되지만 구독과 다음 항목이 작동하지 않는 경우 AEM Communities User Sync Listener 구성에 다음이 있는지 확인하십시오.

   * 노드 유형 - **rep:User, nt:unstructured**, **nt:resource**, **rep:ACL**, **sling:Folder** 및 **sling:OrderedFolder**&#x200B;로 설정됩니다.
   * 무시할 수 있는 노드 - **.tokens**, **시스템** 및 **rep:cache**&#x200B;로 설정됩니다.
   * 분산 폴더 - 배포할 폴더로 설정됩니다.

1. **게시 인스턴스에서 사용자 생성 시 생성된 로그 확인**

   위의 구성이 적절하게 설정되었지만 사용자 동기화가 작동하지 않으면 사용자 생성 시 생성된 로그를 확인하십시오.

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

1. 사용자 동기화 비활성화:
1. AEM 작성자 인스턴스에서 관리자 권한으로 로그인합니다.

   1. [웹 콘솔](/help/sites-deploying/configuring-osgi.md)에 액세스합니다. 예: [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. **Apache Sling Distribution Agent - Sync Agents Factory** 구성을 찾습니다.
   1. **Enabled** 확인란을 선택 취소합니다.

      작성자 인스턴스에서 사용자 동기화를 사용하지 않도록 설정하면(내보내기 및 가져오기) 끝점이 비활성화되고 작성자 인스턴스가 정적입니다. 작성자가 **vlt** 패키지를 핑하거나 가져오지 않습니다.

      이제 사용자가 게시 인스턴스에 작성되면 **vlt** 패키지가 */var/sling/distribution/packages/ socialpubsync - vlt /data* 노드에 만들어집니다. 작성자가 이러한 패키지를 다른 서비스로 푸시할 수 있습니다. 이 데이터를 다운로드하고 추출하여 다른 서비스로 푸시되는 모든 속성을 확인할 수 있습니다.

1. 게시자로 이동하여 게시자에 사용자를 만듭니다. 따라서 이벤트가 만들어집니다.
1. 사용자 생성 시 만든 로그](/help/communities/sync.md#troubleshoot-sling-distribution-in-aem-communities)의 [순서를 확인합니다.
1. **vlt** 패키지가 **/var/sling/distribution/packages/socialpubsync-vlt/data**&#x200B;에 생성되었는지 확인합니다.
1. 이제 AEM 작성자 인스턴스에서 사용자 동기화를 활성화합니다.
1. 게시자의 경우 **Apache Sling Distribution Agent - Sync Agents Factory**에서 내보내기 또는 가져오기 끝점을 변경합니다.
패키지 데이터를 다운로드 및 추출하여 다른 게시자에게 푸시되는 모든 속성과 유실된 데이터를 확인할 수 있습니다.
