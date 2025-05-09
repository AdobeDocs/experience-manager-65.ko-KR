---
title: 사용자 및 사용자 그룹 관리
description: AEM Communities 사용자는 프로필을 자가 등록하고 편집할 수 있습니다
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 4237085a-d70d-41de-975d-153f58336daa
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1910'
ht-degree: 0%

---

# 사용자 및 사용자 그룹 관리 {#managing-users-and-user-groups}

## 개요 {#overview}

AEM Communities의 게시 환경에서 사용자는 프로필을 자체 등록하고 편집할 수 있습니다. 적절한 권한이 주어지면 다음과 같은 작업도 수행할 수 있습니다.

* 커뮤니티 사이트에 하위 커뮤니티를 만듭니다([커뮤니티 그룹](creating-groups.md) 참조).

* UGC(사용자 생성 컨텐츠)를 [중재](moderation.md)합니다.

* 블로그, 일정, QnA 및 포럼에 대한 항목을 만들려면 [권한](#privileged-members-group)이 있어야 합니다.

게시 환경에 등록된 사용자를 일반적으로 *커뮤니티 구성원(구성원)*(으)로 지칭하여 작성자 환경의 *사용자*&#x200B;와(과) 구별합니다.

커뮤니티 사이트가 작성자 환경에서 [생성](sites-console.md) 또는 [수정](sites-console.md#modifying-site-properties)될 때 동적으로 만들어진 [구성원(사용자) 그룹](#publish-group-roles) 중 하나에 구성원을 할당하여 권한이 부여됩니다. 작성 환경에서 작업할 때 구성원은 [터널 서비스](#tunnel-service)를 통해 게시 환경에서 볼 수 있습니다.

기본적으로 게시 환경에서 만든 구성원 및 구성원 그룹은 작성 환경에 표시되지 않아야 합니다. 작성 환경에서 생성된 사용자 및 사용자 그룹은 마찬가지로 작성 환경에 남아 있도록 설계되었습니다.

작성자 및 게시의 멤버가 동일한 LDAP 디렉토리에서 동기화되는 등 동일한 사용자 목록에서 온 경우 작성자 및 게시 환경 모두에서 동일한 권한 및 그룹 구성원을 가진 동일한 사용자로 간주되지 않습니다. 구성원 및 사용자의 역할은 게시 및 작성자에 적절하게 별도로 설정되어야 합니다.

[게시 팜](topologies.md)의 경우 한 게시 인스턴스에서 수행한 등록 및 수정 사항을 다른 게시 인스턴스와 동기화해야 동일한 사용자 데이터에 액세스할 수 있습니다. 자세한 내용은 [사용자 동기화](sync.md)를 참조하십시오. 이 섹션에는 [다음 경우에 발생하는 일..](sync.md#what-happens-when)을 설명하는 섹션이 포함되어 있습니다.

### 기여도 제한 {#contribution-limits}

스팸으로부터 보호하기 위해 회원들의 콘텐츠 게시 빈도를 제한할 수 있다. 나아가, 신규 가입된 회원들의 출연금을 자동으로 제한할 수 있다.

자세한 내용은 [구성원 기여도 제한](limits.md)을 참조하세요.

### 동적으로 생성된 사용자 그룹 {#dynamically-created-user-groups}

새 커뮤니티 사이트가 만들어지면 작성자 환경([작성자 그룹 역할](#author-group-roles) 참조) 또는 게시 환경([Publish 그룹 역할](#publish-group-roles) 참조)에서 커뮤니티 사이트를 관리하는 데 필요한 다양한 관리 기능에 적합한 uid(고유 ID) 및 권한을 사용하여 새 사용자 그룹이 동적으로 만들어집니다.

그룹 이름은 [커뮤니티 사이트를 만드는 동안](sites-console.md#step13asitetemplate) 사이트에 지정된 이름에서 생성됩니다. 고유 ID는 동일한 서버의 비슷한 이름의 커뮤니티 사이트 및 커뮤니티 그룹에 대한 이름 충돌을 방지합니다.

예를 들어 사이트 이름이 &quot;&lbrace;Engage&quot; 사이트에 대해 &quot;*engage*&quot;이면 만들어진 사용자 그룹 중 하나는 다음과 같습니다.

* 커뮤니티 *참여* 구성원

## 작성 환경 {#author-environment}

### 터널 서비스 {#tunnel-service}

작성자 환경을 사용하여 [사이트를 만들고](sites-console.md), [사이트 속성을 수정하고](sites-console.md#modifying-site-properties), [커뮤니티 구성원 및 구성원 그룹을 관리합니다](members.md). 게시 환경에 등록된 사용자 및 사용자 그룹에 액세스해야 합니다.

터널 서비스는 작성자의 복제 에이전트를 사용하여 이 액세스를 제공합니다.

* 자세한 내용은 배포 페이지에서 [구성 지침](deploy-communities.md#tunnel-service-on-author)을 참조하세요.

[커뮤니티 구성원 및 그룹 콘솔](members.md)은(는) 게시 환경에만 등록된 사용자(구성원) 및 사용자 그룹(구성원 그룹)을 관리하기 위한 용도로만 사용됩니다.

작성 환경에 등록된 사용자 및 사용자 그룹을 관리하려면 [보안 콘솔](../../help/sites-administering/security.md)을 사용하십시오.

### 작성자 그룹 역할 {#author-group-roles}

| 그룹의 멤버인 경우... | 기본 역할 |
|---|---|
| 관리자 | 관리자 그룹은 커뮤니티 관리자의 모든 기능과 커뮤니티 관리자 그룹을 관리할 수 있는 기능을 가진 시스템 관리자로 구성됩니다. |
| 커뮤니티 관리자 | 커뮤니티 관리자 그룹은 자동으로 모든 커뮤니티 사이트 및 사이트에서 만든 모든 커뮤니티 그룹의 구성원이 됩니다. 커뮤니티 관리자 그룹의 초기 멤버는 관리자 그룹입니다. 작성 환경에서 커뮤니티 관리자는 커뮤니티 사이트를 만들고, 사이트를 관리하고, 구성원을 관리하고(커뮤니티에서 구성원을 금지할 수 있음), 콘텐츠를 중재할 수 있습니다. |
| 커뮤니티 &lt;*사이트 이름*> 사이트 컨텐츠 관리자 | 커뮤니티 사이트 콘텐츠 관리자는 커뮤니티 사이트에 대한 기존 AEM 작성, 콘텐츠 작성 및 페이지 수정을 수행할 수 있습니다. |
| 없음 | 익명 사이트 방문자는 작성 환경에 액세스할 수 없습니다. |

### 시스템 관리자 {#system-administrators}

관리자 그룹의 멤버는 작성 및 게시 환경 모두에 대해 AEM 설치의 초기 설정을 수행할 수 있는 시스템 관리자입니다.

데모 및 개발을 위해 관리자 그룹에는 사용자 ID가 *admin*&#x200B;이고 암호가 *admin*&#x200B;인 구성원이 있습니다.

프로덕션 환경의 경우 기본 관리자 그룹을 수정해야 합니다.

[보안 검사 목록](../../help/sites-administering/security-checklist.md)을 따르세요.

## 게시 환경 {#publish-environment}

### 구성원 되기 {#becoming-a-member}

게시 환경에서 커뮤니티 사이트의 [설정](sites-console.md#user-management)에 따라 사이트 방문자는 커뮤니티 구성원이 될 수 있습니다.

* 커뮤니티 사이트가 비공개인 경우(폐쇄됨):
   * 초대에 의해
   * 관리자의 작업

* 커뮤니티 사이트가 공개(공개)인 경우:
   * 자가 등록으로
   * facebook 및 Twitter을 사용하여 소셜 로그인

>[!NOTE]
>
>사이트 방문자가 하나의 열린 커뮤니티 사이트의 구성원으로 등록하면 동일한 게시 환경에서 자동으로 다른 열린 커뮤니티 사이트의 구성원이 됩니다.

### Publish 그룹 역할 {#publish-group-roles}

| 그룹의 멤버인 경우... | 기본 역할 |
|---|---|
| 커뮤니티 &lt;*사이트 이름*> 구성원 | 커뮤니티 사이트 회원은 등록된 사용자입니다. 사용자는 로그인하고, 프로필을 수정하고, 열린 커뮤니티 그룹에 참여하고, 커뮤니티에 콘텐츠를 게시하고, 다른 구성원에게 메시지를 보내고, 사이트 활동을 팔로우할 수 있습니다. |
| 커뮤니티 &lt;*사이트 이름*> 중재자 | 커뮤니티 사이트 중재자는 컨텐츠가 게시된 페이지에서 중재 콘솔을 사용하여 일괄 중재하거나 컨텍스트 내에서 UGC를 중재할 수 있는 신뢰할 수 있는 커뮤니티 구성원입니다. |
| 커뮤니티 &lt;*사이트 이름*> &lt;*그룹 이름*> 구성원 | 커뮤니티 그룹 구성원은 열린 커뮤니티 그룹에 가입하거나 폐쇄된 커뮤니티 그룹에 초대된 커뮤니티 구성원입니다. 이 사용자는 사이트 내에서 해당 커뮤니티 그룹에 대한 구성원의 능력이 있습니다. |
| 커뮤니티 &lt;*사이트 이름*> Groupadministrators | 커뮤니티 사이트 그룹 관리자는 커뮤니티 사이트 내에서 하위 커뮤니티(그룹)를 만들고 관리하도록 할당된 신뢰할 수 있는 커뮤니티 구성원입니다. 컨텍스트 내 중재 기능을 제공합니다. |
| *권한이 있는 구성원 보안 그룹* | 콘텐츠 생성을 제한할 목적으로 수동으로 생성 및 유지 관리되는 사용자 그룹. [권한이 있는 구성원 그룹](#privileged-members-group)을 참조하세요. |
| 없음 | 사이트를 발견하는 익명 사이트 방문자는 익명 액세스를 허용하는 커뮤니티 사이트를 보고 검색할 수 있습니다. 참여하고 콘텐츠를 게시하려면 사용자가 직접 등록하고(허용된 경우) 커뮤니티 회원이 되어야 합니다. |

### Publish 그룹 역할에 구성원 할당 {#assigning-members-to-publish-group-roles}

작성자 환경에서 [커뮤니티 사이트를 만들거나](sites-console.md)사이트 속성을 수정하는 경우[&#128279;](sites-console.md#modifying-site-properties)명의 구성원에게 중재자, 그룹 관리자, 리소스 연락처 또는 권한이 있는 구성원 등 게시 환경에서 수행되는 다양한 역할이 할당될 수 있습니다.

[터널 서비스를 사용하도록 설정](sync.md#accessingpublishusersfromauthor)하면 작성자의 사용자 대신 게시의 구성원으로부터 할당 선택 항목이 표시됩니다.

선택한 구성원은 [해당 그룹](#publish-group-roles)에 자동으로 할당되며 커뮤니티 사이트를 (재)게시할 때 해당 구성원이 포함됩니다.

### 권한이 있는 구성원 그룹 {#privileged-members-group}

권한이 있는 구성원 보안 그룹의 목적은 특정 커뮤니티 기능에 대한 콘텐츠 생성을 커뮤니티 사이트 구성원의 권한이 있는 하위 집합으로 제한하는 것입니다.

권한이 있는 구성원 그룹은 [커뮤니티 그룹 콘솔](members.md)을 사용하여 만들고 관리하는 구성원 그룹입니다.

권한이 있는 구성원 그룹을 만든 후 [터널 서비스를 사용](sync.md#accessingpublishusersfromauthor)하면 기존 커뮤니티 사이트의 구조를 [수정](sites-console.md#modify-structure)하여 커뮤니티 기능의 구성을 &#39;권한이 있는 구성원 허용&#39;으로 편집하고 만든 그룹을 추가할 수 있습니다.

하나 이상의 권한이 있는 구성원 그룹을 지정할 수 있는 커뮤니티 기능은 다음과 같습니다.

* [블로그 기능](functions.md#blog-function) - 새 기사 만들기를 제한합니다.
* [Calendar 함수](functions.md#calendar-function) - 새 이벤트 만들기를 제한합니다.
* [포럼 함수](functions.md#forum-function) - 새 주제 만들기를 제한합니다.
* [QnA 함수](functions.md#qna-function) - 새 질문 만들기를 제한합니다.

커뮤니티 기능이 할당되지 않은 경우(권한이 있는 구성원 그룹이 할당되지 않음) 모든 커뮤니티 사이트 구성원이 기능 콘텐츠(문서, 이벤트, 주제, 질문)를 만들 수 있습니다.

>[!NOTE]
>
>커뮤니티 사이트의 권한이 있는 구성원 그룹에 사용자를 추가하면 해당 사용자가 동일한 커뮤니티 사이트의 구성원일 경우에만 만들기 권한이 부여됩니다.

## 커뮤니티 구성원 만들기 {#creating-community-members}

### 저장소 위치 {#repository-location}

특정 기능이 제대로 작동하려면 적절한 권한을 가진 사용자 및 사용자 그룹을 만들어야 합니다.

`/home/users/community`에서 구성원을 만들면 구성원의 프로필에 읽기 권한을 부여하는 적절한 ACL을 상속합니다.

마찬가지로 사용자 지정 커뮤니티 사용자 그룹(예: 권한이 있는 구성원 그룹)은 `/home/groups/community`에 만들어야 합니다.

[커뮤니티 구성원 및 그룹 콘솔](members.md)을 사용하면 이러한 경로에 사용자 및 그룹이 만들어집니다.

사용자 지정 경로를 지정하려면 [https://&lt;server>:&lt;port>/useradmin](http://localhost:4503/useradmin)에서 액세스할 수 있는 클래식 보안 UI를 사용해야 합니다.

사용자 지정 멤버 경로에 대한 읽기 권한을 부여하려면 모든 게시 인스턴스에서 `/home/users/community`과(와) 유사한 ACL을 설정합니다.

```xml
<allow
  jcr:primaryType="rep:GrantACE"
  rep:principalName="everyone"
  rep:privileges="{Name}[jcr:read]" >
  <rep:restrictions
    jcr:primaryType="rep:Restrictions"
    rep:glob="*/profile*" />
</allow>
```

모든 게시 인스턴스에서 /home/groups/mycompany와 같은 사용자 지정 구성원 그룹 경로에 대해 적절한 권한을 부여하려면 `/home/groups/community`과(와) 유사한 ACL을 설정합니다.

```xml
<allow
  jcr:primaryType="rep:GrantACE"
  rep:principalName="community-administrators"
  rep:privileges="{Name}[jcr:read]"  />
```

### 콘솔 {#consoles}

작성자 환경에서만 사용할 수 있는 네 개의 별도 콘솔이 있습니다.

| 콘솔 | 도구, 보안, 사용자 | 도구, 보안, 그룹 | 커뮤니티, 구성원 | 커뮤니티, 그룹 |
|----------|-----------------------|------------------------|------------------------------------------------------------|------------------------------------------------------------|
| 관리 | 작성자의 사용자 | 작성자의 사용자 그룹 | 게시의 구성원 | 게시의 구성원 그룹 |
| 필수 | 관리자 권한 | 관리자 권한 | 게시 팜에 대한 관리자 권한, 터널 서비스, 사용자 동기화 | 게시 팜에 대한 관리자 권한, 터널 서비스, 사용자 동기화 |

### 커뮤니티 관리자 역할 {#community-administrators-role}

[작성자 그룹 역할](#author-group-roles) 차트에 나와 있는 대로 커뮤니티 관리자 그룹의 구성원은 커뮤니티 사이트를 만들고, 사이트를 관리하고, 구성원을 관리하며(커뮤니티의 구성원 참여를 금지할 수 있음), 콘텐츠를 조정할 수 있습니다.

사용자를 만들고 지원 관리자 역할에 할당하는 것과 동일한 단계를 따르되 사용자의 그룹 탭 아래에 c `ommunity-administrators` 그룹을 추가하십시오.

### LDAP 통합 {#ldap-integration}

AEM은 사용자 인증 및 사용자 계정 생성을 위한 LDAP 사용을 지원합니다. 자세한 내용은 [AEM 6을 사용하여 LDAP 구성](../../help/sites-administering/ldap-config.md)을 참조하십시오.

다음은 커뮤니티 구성원과 구성원 그룹에 대한 몇 가지 구성 세부 정보입니다.

1. 각 AEM 게시 인스턴스에 대해 LDAP를 구성합니다.
2. [LDAP ID 공급자](../../help/sites-administering/ldap-config.md#configuring-the-ldap-identity-provider)

   * 특별한 지침 없음

3. [동기화 핸들러](../../help/sites-administering/ldap-config.md#configuring-the-synchronization-handler)

   * 다음 속성을 설정합니다.

      * **[!UICONTROL 사용자 자동 멤버십]**: `community-<site name>-<uid>-members`
      * **[!UICONTROL 사용자 경로 접두사]**: `/community`
      * **[!UICONTROL 그룹 경로 접두사]**: `/community`

4. [외부 로그인 모듈](../../help/sites-administering/ldap-config.md#the-external-login-module)

   * 특별한 지침 없음

이렇게 하면 사용자가 커뮤니티 사이트의 구성원 그룹에 자동으로 할당되고 저장소 위치는 `/home/users/community` 및 `/home/groups/community`이(가) 되므로 다른 사용자의 프로필을 볼 수 있는 적절한 권한을 상속합니다.

* `User auto membership` 값은 프로필의 `givenName`(표시 이름)이 아니라 `rep:authorizableId` 속성이어야 합니다.

## AEM 인스턴스 간 사용자 동기화 {#synchronizing-users-among-aem-instances}

[게시 팜](topologies.md)을 사용하는 경우 사용자를 먼저 하나의 인스턴스로 가져오고 Sling에 대한 [사용자 동기화를 활성화](sync.md)하여 사용자를 다른 게시 인스턴스로 배포하여 사용자가 각 게시 인스턴스에서 동일한 경로를 갖도록 하십시오.

사용자 그룹을 가져오는 경우 각 게시 인스턴스에서 사용자 그룹의 경로가 동일한지 확인하려면 한 인스턴스로 가져온 다음 [내보낼 패키지를 만들고](../../help/sites-administering/package-manager.md#creating-a-new-package) 다른 모든 게시 인스턴스에 해당 패키지를 설치합니다.

사용자 동기화를 통한 사용자 그룹 동기화가 향후 릴리스에 포함되지만 현재 사용자 동기화가 실행될 때 사용자 그룹의 *멤버십*&#x200B;만 동기화됩니다.

## 커뮤니티 그룹 기본 정보 {#about-community-groups}

그룹에 대해 논의할 때 두 가지 서로 다른 주제가 있습니다.

* **[커뮤니티 그룹](overview.md#communitygroups)**

  커뮤니티 그룹은 커뮤니티 그룹 만들기를 지원하는 커뮤니티 사이트에 대한 게시 환경에서 만들 수 있는 하위 커뮤니티입니다. 커뮤니티 그룹을 만들면 웹 사이트에 페이지가 더 추가되고 상위 커뮤니티 사이트와 유사한 방식으로 관리됩니다. 자세한 내용은 개발자를 위한 [커뮤니티 그룹 필수 구성 요소](essentials-groups.md) 및 작성자를 위한 [커뮤니티 그룹](creating-groups.md)을 참조하세요.

* **[구성원 그룹](../../help/sites-administering/security.md)**

  구성원 그룹은 구성원이 속할 수 있는 그룹이며 그룹 콘솔을 통해 관리됩니다. 이 페이지에 대한 논의의 상당 부분은 회원들에게 할애되어 왔다. 커뮤니티 사이트에 대해 자동으로 만들어진 구성원 그룹(*`Community`* 접두사 포함)은 커뮤니티 그룹이라고 할 수 있으므로 토론 컨텍스트를 고려해야 합니다.
