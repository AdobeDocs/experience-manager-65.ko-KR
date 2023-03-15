---
title: 사용자 및 사용자 그룹 관리
seo-title: Managing Users and User Groups
description: AEM Communities 사용자는 프로필을 자가 등록하고 편집할 수 있습니다
seo-description: Users of AEM Communities can self-register and edit their profiles
uuid: aeba424e-ea7e-4da5-b94f-ea8af4caa7d2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 774c2553-b629-456b-afa7-5713490f4a0a
role: Admin
exl-id: 4237085a-d70d-41de-975d-153f58336daa
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '2168'
ht-degree: 0%

---

# 사용자 및 사용자 그룹 관리 {#managing-users-and-user-groups}

## 개요 {#overview}

AEM Communities의 게시 환경에서 사용자는 프로필을 자체 등록하고 편집할 수 있습니다. 적절한 권한이 주어지면 다음과 같은 작업도 수행할 수 있습니다.

* 커뮤니티 사이트 내에 하위 커뮤니티 만들기(참조) [커뮤니티 그룹](creating-groups.md)).

* [중재](moderation.md) 사용자 생성 컨텐츠(UGC).

* Be [지원 리소스](resources.md) 연락처.

* Be [권한이 부여됨](#privileged-members-group) 블로그, 캘린더, QnA 및 포럼에 대한 항목을 만들 수 있습니다.

게시 환경에 등록된 사용자를 일반적으로 라고 합니다. *커뮤니티 구성원(구성원)* 이들을 구별하다 *사용자* 작성 환경에서 사용할 수 있습니다.

권한은 구성원을 다음 중 하나에 할당하여 부여됩니다. [구성원(사용자) 그룹](#publish-group-roles) 커뮤니티 사이트가 다음과 같을 때 동적으로 생성됨 [생성됨](sites-console.md) 또는 [수정됨](sites-console.md#modifying-site-properties) 작성자 환경에서. 작성 환경에서 작업할 때 멤버는 를 통해 게시 환경에서 볼 수 있습니다. [터널 업무](#tunnel-service).

기본적으로 게시 환경에서 만든 구성원 및 구성원 그룹은 작성 환경에 표시되지 않아야 합니다. 작성 환경에서 생성된 사용자 및 사용자 그룹은 마찬가지로 작성 환경에 남아 있도록 설계되었습니다.

작성자 및 게시의 멤버가 동일한 LDAP 디렉토리에서 동기화되는 등 동일한 사용자 목록에서 온 경우 작성자 및 게시 환경 모두에서 동일한 권한 및 그룹 구성원을 가진 동일한 사용자로 간주되지 않습니다. 구성원 및 사용자의 역할은 게시 및 작성자에 적절하게 별도로 설정되어야 합니다.

의 경우 [팜 게시](topologies.md), 한 게시 인스턴스에서 동일한 사용자 데이터에 액세스하려면 한 게시 인스턴스에서 수행한 등록 및 수정 사항을 다른 게시 인스턴스와 동기화해야 합니다. 자세한 내용은 다음을 참조하십시오. [사용자 동기화](sync.md): 설명하는 섹션을 포함합니다 [다음 경우에 발생하는 작업...](sync.md#what-happens-when).

### 기여도 제한 {#contribution-limits}

스팸으로부터 보호하기 위해 회원들의 콘텐츠 게시 빈도를 제한할 수 있다. 나아가, 신규 가입된 회원들의 출연금을 자동으로 제한할 수 있다.

자세한 내용은 [구성원 기여도 제한](limits.md).

### 동적으로 생성된 사용자 그룹 {#dynamically-created-user-groups}

새 커뮤니티 사이트가 생성되면 작성자 환경에서 커뮤니티 사이트를 관리하는 데 필요한 다양한 관리 기능에 적합한 고유 ID(uid) 및 권한을 사용하여 새 사용자 그룹이 동적으로 만들어집니다(참조) [작성자 그룹 역할](#author-group-roles)) 또는 게시 환경( 참조 [게시 그룹 역할](#publish-group-roles)).

그룹 이름은 다음 기간 동안 사이트에 지정된 이름에서 생성됩니다 [커뮤니티 사이트 생성](sites-console.md#step13asitetemplate). 고유 ID는 동일한 서버의 비슷한 이름의 커뮤니티 사이트 및 커뮤니티 그룹에 대한 이름 충돌을 방지합니다.

예를 들어 사이트 이름이 &quot;*참여*&quot;We.Retail Engage&quot;라는 사이트의 경우 생성된 사용자 그룹 중 하나는 다음과 같습니다.

* 커뮤니티 *참여* 구성원

## 작성 환경 {#author-environment}

### 터널 서비스 {#tunnel-service}

작성 환경을 사용하여 다음과 같은 작업을 수행하는 경우 [사이트 생성](sites-console.md), [사이트 속성 수정](sites-console.md#modifying-site-properties) 및 [커뮤니티 구성원 및 구성원 그룹 관리](members.md), 게시 환경에 등록된 사용자 및 사용자 그룹에 액세스해야 합니다.

터널 서비스는 작성자의 복제 에이전트를 사용하여 이 액세스를 제공합니다.

* 자세한 내용은 [구성 지침](deploy-communities.md#tunnel-service-on-author) 배포 페이지에서 확인할 수 있습니다.

다음 [커뮤니티 구성원 및 그룹 콘솔](members.md) 는 게시 환경에만 등록된 사용자(구성원) 및 사용자 그룹(구성원 그룹)을 관리하는 유일한 목적입니다.

작성 환경에 등록된 사용자 및 사용자 그룹을 관리하려면 [보안 콘솔](../../help/sites-administering/security.md)

### 작성자 그룹 역할 {#author-group-roles}

| 그룹의 멤버인 경우... | 기본 역할 |
|---|---|
| 관리자 | 관리자 그룹은 커뮤니티 관리자의 모든 기능과 커뮤니티 관리자 그룹을 관리할 수 있는 기능을 가진 시스템 관리자로 구성됩니다. |
| 커뮤니티 관리자 | 커뮤니티 관리자 그룹은 자동으로 모든 커뮤니티 사이트 및 사이트에서 만든 모든 커뮤니티 그룹의 구성원이 됩니다. 커뮤니티 관리자 그룹의 초기 멤버는 관리자 그룹입니다. 작성 환경에서 커뮤니티 관리자는 커뮤니티 사이트를 만들고, 사이트를 관리하고, 구성원을 관리하고(커뮤니티에서 구성원을 금지할 수 있음), 콘텐츠를 중재할 수 있습니다. |
| 커뮤니티 &lt;*사이트 이름*> 사이트 컨텐츠 관리자 | 커뮤니티 사이트 콘텐츠 관리자는 커뮤니티 사이트에 대한 기존 AEM 작성, 콘텐츠 작성 및 페이지 수정을 수행할 수 있습니다. |
| 커뮤니티 지원 관리자 | Community Enablement Managers 그룹은 커뮤니티 사이트의 Enablement Managers 그룹을 관리하기 위해 할당할 수 있는 사용자로 구성됩니다. |
| 커뮤니티 &lt;*사이트 이름* > Siteenablementmanager | Community Site Enablement Manager 그룹은 커뮤니티 사이트의 활성화를 관리하도록 할당된 사용자로 구성됩니다 [리소스](resources.md). |
| 없음 | 익명 사이트 방문자는 작성 환경에 액세스할 수 없습니다. |

### 시스템 관리자 {#system-administrators}

관리자 그룹의 멤버는 작성 및 게시 환경 모두에 대해 AEM 설치의 초기 설정을 수행할 수 있는 시스템 관리자입니다.

데모 및 개발을 위해 관리자 그룹에는 사용자 ID가 인 구성원이 있습니다. *admin* 및 암호는 *admin*.

프로덕션 환경의 경우 기본 관리자 그룹을 수정해야 합니다.

다음 사항을 따르십시오. [보안 검사 목록](../../help/sites-administering/security-checklist.md).

## 게시 환경 {#publish-environment}

### 구성원 되기 {#becoming-a-member}

게시 환경에서 [설정](sites-console.md#user-management) 커뮤니티 사이트의 사이트 방문자는 커뮤니티 회원이 될 수 있습니다.

* 커뮤니티 사이트가 비공개인 경우(폐쇄됨):
   * 초대에 의해
   * 관리자의 작업

* 커뮤니티 사이트가 공개(공개)인 경우:
   * 자가 등록으로
   * facebook 및 Twitter을 사용하여 소셜 로그인

>[!NOTE]
>
>사이트 방문자가 하나의 열린 커뮤니티 사이트의 구성원으로 등록하면 동일한 게시 환경에서 자동으로 다른 열린 커뮤니티 사이트의 구성원이 됩니다.

### 게시 그룹 역할 {#publish-group-roles}

| 그룹의 멤버인 경우... | 기본 역할 |
|---|---|
| 커뮤니티 &lt;*사이트 이름*> 구성원 | 커뮤니티 사이트 회원은 등록된 사용자입니다. 사용자는 로그인하고, 프로필을 수정하고, 열린 커뮤니티 그룹에 참여하고, 커뮤니티에 콘텐츠를 게시하고, 다른 구성원에게 메시지를 보내고, 사이트 활동을 팔로우할 수 있습니다. |
| 커뮤니티 &lt;*사이트 이름*> 중재자 | 커뮤니티 사이트 중재자는 컨텐츠가 게시된 페이지에서 중재 콘솔을 사용하여 일괄 중재하거나 컨텍스트 내에서 UGC를 중재할 수 있는 신뢰할 수 있는 커뮤니티 구성원입니다. |
| 커뮤니티 &lt;*사이트 이름*> &lt;*그룹 이름*> 구성원 | 커뮤니티 그룹 구성원은 열린 커뮤니티 그룹에 가입하거나 폐쇄된 커뮤니티 그룹에 초대된 커뮤니티 구성원입니다. 이 사용자는 사이트 내에서 해당 커뮤니티 그룹에 대한 구성원의 능력이 있습니다. |
| 커뮤니티 &lt;*사이트 이름*> 그룹 관리자 | 커뮤니티 사이트 그룹 관리자는 커뮤니티 사이트 내에서 하위 커뮤니티(그룹)를 만들고 관리하도록 할당된 신뢰할 수 있는 커뮤니티 구성원입니다. 컨텍스트 내 중재 기능을 제공합니다. |
| *권한이 있는 구성원 보안 그룹* | 콘텐츠 생성을 제한할 목적으로 수동으로 생성 및 유지 관리되는 사용자 그룹. 다음을 참조하십시오 [권한이 있는 구성원 그룹](#privileged-members-group). |
| 없음 | 사이트를 발견하는 익명 사이트 방문자는 익명 액세스를 허용하는 커뮤니티 사이트를 보고 검색할 수 있습니다. 참여하고 콘텐츠를 게시하려면 사용자가 직접 등록하고(허용된 경우) 커뮤니티 회원이 되어야 합니다. |

### 게시 그룹 역할에 구성원 할당 {#assigning-members-to-publish-group-roles}

날짜 [커뮤니티 사이트 만들기](sites-console.md) 작성 환경 또는 [사이트 속성 수정,](sites-console.md#modifying-site-properties) 구성원에는 중재자, 그룹 관리자, 리소스 연락처 또는 권한이 있는 구성원과 같이 게시 환경에서 수행되는 다양한 역할이 할당될 수 있습니다.

[터널 서비스 활성화](sync.md#accessingpublishusersfromauthor) 을(를) 작성자의 사용자 대신 게시의 멤버로부터 할당 선택 사항이 표시됩니다.

선택한 멤버는에 자동으로 할당됩니다. [적절한 그룹](#publish-group-roles) 커뮤니티 사이트를 (재)게시할 때 및 해당 멤버십이 포함됩니다.

### 권한이 있는 구성원 그룹 {#privileged-members-group}

권한이 있는 구성원 보안 그룹의 목적은 특정 커뮤니티 기능에 대한 콘텐츠 생성을 커뮤니티 사이트 구성원의 권한이 있는 하위 집합으로 제한하는 것입니다.

권한이 있는 구성원 그룹은 [커뮤니티 그룹 콘솔](members.md).

권한이 있는 구성원 그룹을 만든 후 [터널 서비스 활성화됨](sync.md#accessingpublishusersfromauthor)기존 커뮤니티 사이트의 구조는 [수정됨](sites-console.md#modify-structure) 커뮤니티 기능의 구성을 &#39;권한이 있는 구성원 허용&#39;으로 편집하고 만든 그룹을 추가합니다.

하나 이상의 권한이 있는 구성원 그룹을 지정할 수 있는 커뮤니티 기능은 다음과 같습니다.

* [블로그 기능](functions.md#blog-function) - 새 문서 만들기를 제한합니다.
* [Calendar 함수](functions.md#calendar-function) - 새 이벤트 생성을 제한합니다.
* [포럼 기능](functions.md#forum-function) - 새 주제 생성을 제한합니다.
* [QnA 기능](functions.md#qna-function) - 새 질문 생성을 제한합니다.

커뮤니티 기능이 할당되지 않은 경우(권한이 있는 구성원 그룹이 할당되지 않음) 모든 커뮤니티 사이트 구성원이 기능 콘텐츠(문서, 이벤트, 주제, 질문)를 만들 수 있습니다.

>[!NOTE]
>
>커뮤니티 사이트의 권한이 있는 구성원 그룹에 사용자를 추가하면 해당 사용자가 동일한 커뮤니티 사이트의 구성원일 경우에만 만들기 권한이 부여됩니다.

## 커뮤니티 구성원 만들기 {#creating-community-members}

### 저장소 위치 {#repository-location}

특정 기능이 제대로 작동하려면 적절한 권한을 가진 사용자 및 사용자 그룹을 만들어야 합니다.

멤버를에서 만들 때 `/home/users/community`, 멤버의 프로필에 읽기 권한을 제공하는 적절한 ACL을 상속합니다.

마찬가지로 사용자 정의 커뮤니티 사용자 그룹(예: 권한이 있는 구성원 그룹)은 `/home/groups/community`.

사용 [커뮤니티 구성원 및 그룹 콘솔](members.md) 이(가) 이러한 경로에 사용자 및 그룹을 생성합니다.

사용자 지정 경로를 지정하려면 다음에서 액세스할 수 있는 클래식 보안 UI를 사용해야 합니다. [https://&lt;server>:&lt;port>/useradmin](http://localhost:4503/useradmin).

사용자 정의 멤버 경로에 대한 읽기 권한을 부여하려면 모든 게시 인스턴스에서 다음과 유사한 ACL을 설정합니다. `/home/users/community`:

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

모든 게시 인스턴스에서 /home/groups/mycompany와 같은 사용자 지정 구성원 그룹 경로에 대해 적절한 권한을 부여하려면 다음과 유사한 ACL을 설정합니다. `/home/groups/community`:

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

### 커뮤니티 지원 관리자 역할 {#community-enablement-manager-role}

사이트 방문자가 자체 등록하는 기능은 일반적으로 [지원 커뮤니티](overview.md#enablement-community) 각 멤버와 관련된 비용이 있습니다. 지원 학습자 및 리소스는 할당된 사용자가 관리합니다. [역할](#author-group-roles) / `enablement manager` [사이트 생성 중](sites-console.md#enablement) 작성자(그룹의 구성원으로 추가됨) `Community <site-name> Siteenablementmanagers`). 다음 `enablement manager` 은(는) 또한 다음의 책임이 있습니다. [학습 리소스 할당](resources.md) 작성자의 커뮤니티 구성원에게 보냅니다.

전역 멤버인 사용자만 `Community Enablement Managers` 다음 항목으로 그룹을 선택할 수 있습니다. `enablement manager` 특정 커뮤니티 사이트용.

다음의 역할을 할당할 수 있는 사용자를 만들려면 `Community Site Enablement Manager`, 클래식 UI 보안 콘솔을 사용하여 경로를 지정합니다.

작성자 인스턴스에서 다음을 수행합니다.

1. 관리자 권한으로 로그인하면 클래식 UI 보안 콘솔로 이동합니다.

   예를 들어, [http://localhost:4502/useradmin](http://localhost:4502/useradmin)

2. 편집 메뉴에서 **[!UICONTROL 사용자 만들기]**.
3. 다음을 입력합니다. `Create User` 대화 상자.
   * 경로는 다음과 같아야 합니다. `/home/users/community`.
4. **[!UICONTROL 만들기]**&#x200B;를 선택합니다.

   ![커뮤니티 사용자 만들기](assets/create-community-user.png)

* 왼쪽 창에서 새로 생성된 사용자를 검색하고 오른쪽 창에 표시하도록 선택합니다.

   ![community-user](assets/view-community-user.png)

왼쪽 창에

1. 검색 상자를 지우고 를 선택합니다. **[!UICONTROL 사용자 숨기기]**.
2. 찾아 드래그 `community-enablementmanagers` (으)로 **[!UICONTROL 그룹]** 오른쪽 창에 표시되는 새 사용자의 탭.

   ![assign-group](assets/assign-group.png)

### 커뮤니티 관리자 역할 {#community-administrators-role}

에 명시된 대로 [작성자 그룹 역할](#author-group-roles) 차트, 커뮤니티 관리자 그룹의 구성원은 커뮤니티 사이트를 만들고, 사이트를 관리하고, 구성원을 관리하고(커뮤니티에서 구성원을 금지할 수 있음), 콘텐츠를 중재할 수 있습니다.

사용자를 만들고 역할에 할당하는 것과 동일한 단계를 수행합니다. [지원 관리자](#communitysiteenablementmanagerrole), 하지만 c 추가 `ommunity-administrators` 사용자의 그룹 탭 아래에 있는 그룹입니다.

### LDAP 통합 {#ldap-integration}

AEM은 사용자 계정 생성뿐만 아니라 사용자 인증을 위한 LDAP 사용을 지원합니다. 이에 자세히 설명되어 있습니다. [AEM 6을 사용하여 LDAP 구성](../../help/sites-administering/ldap-config.md).

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

이를 통해 사용자는 자동으로 커뮤니티 사이트의 구성원 그룹에 할당되고 저장소 위치는 다음과 같이 됩니다. `/home/users/community` 및 `/home/groups/community`서로의 프로필을 볼 수 있는 적절한 사용 권한을 상속합니다.

* 다음 `User auto membership` 값은 다음이어야 합니다. `rep:authorizableId` 속성이 아님 `givenName` (표시 이름) 을 입력합니다.

## AEM 인스턴스 간 사용자 동기화 {#synchronizing-users-among-aem-instances}

사용 시 [팜 게시](topologies.md), 사용자를 먼저 하나의 인스턴스로 가져와서 사용자가 각 게시 인스턴스에서 동일한 경로를 갖도록 합니다. [사용자 동기화 활성화](sync.md) Sling에서 사용자를 다른 게시 인스턴스로 배포합니다.

사용자 그룹을 가져오는 경우 각 게시 인스턴스에서 사용자 그룹의 경로가 동일하도록 하려면 한 인스턴스로 가져온 다음 [패키지 만들기](../../help/sites-administering/package-manager.md#creating-a-new-package) 내보내기를 위해 다른 모든 게시 인스턴스에 해당 패키지를 설치합니다.

사용자 동기화를 통한 사용자 그룹 동기화가 향후 릴리스에 포함되지만 현재는 *멤버십* 의 사용자 그룹은 사용자 동기화가 실행될 때 동기화됩니다.

## 커뮤니티 그룹 기본 정보 {#about-community-groups}

그룹에 대해 논의할 때 두 가지 서로 다른 주제가 있습니다.

* **[커뮤니티 그룹](overview.md#communitygroups)**

   커뮤니티 그룹은 커뮤니티 그룹 만들기를 지원하는 커뮤니티 사이트에 대한 게시 환경에서 만들 수 있는 하위 커뮤니티입니다. 커뮤니티 그룹을 만들면 웹 사이트에 페이지가 더 추가되고 상위 커뮤니티 사이트와 유사한 방식으로 관리됩니다. 자세한 내용은 다음을 참조하십시오. [커뮤니티 그룹 기본 사항](essentials-groups.md) 개발자 및 [커뮤니티 그룹](creating-groups.md) 작성자용.

* **[구성원 그룹](../../help/sites-administering/security.md)**

   구성원 그룹은 구성원이 속할 수 있는 그룹이며 그룹 콘솔을 통해 관리됩니다. 이 페이지에 대한 논의의 상당 부분은 회원들에게 할애되어 왔다. 커뮤니티 사이트에 대해 멤버 그룹이 자동으로 생성되며 접두사가 붙습니다. *`Community`*&#x200B;는 커뮤니티 그룹이라고 할 수 있으므로 논의의 맥락을 고려해야 합니다.
