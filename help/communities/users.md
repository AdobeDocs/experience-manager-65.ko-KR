---
title: 사용자 및 사용자 그룹 관리
seo-title: 사용자 및 사용자 그룹 관리
description: AEM Communities 사용자는 자신의 프로필을 직접 등록 및 편집할 수 있습니다.
seo-description: AEM Communities 사용자는 자신의 프로필을 직접 등록 및 편집할 수 있습니다.
uuid: aeba424e-ea7e-4da5-b94f-ea8af4caa7d2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 774c2553-b629-456b-afa7-5713490f4a0a
translation-type: tm+mt
source-git-commit: c190d5f223c85f6c49fea1391d8a3d2baff20192
workflow-type: tm+mt
source-wordcount: '2183'
ht-degree: 0%

---


# Managing Users and User Groups {#managing-users-and-user-groups}

## 개요 {#overview}

AEM Communities의 게시 환경에서 사용자는 자신의 프로필을 직접 등록하고 편집할 수 있습니다. 적절한 권한이 주어지면 다음과 같은 경우도 있습니다.

* 커뮤니티 사이트 내에서 하위 커뮤니티를 만듭니다( [커뮤니티 그룹](creating-groups.md)참조).

* [UGC](moderation.md) (사용자 생성 콘텐츠)를 중재합니다.

* 역량 [강화 리소스](resources.md) 연락처

* 블로그, 달력, QnA 및 포럼 [에 대한 항목을 만들 수 있는 권한을](#privileged-members-group) 부여받을 수 있습니다.

게시 환경에 등록된 사용자는 일반적으로 작성 환경의 *사용자와* 구별하기 위해 ** 커뮤니티 구성원(구성원)이라고 합니다.

커뮤니티 사이트를 [만들거나](#publish-group-roles) [수정할](sites-console.md) 때 동적으로 만든 구성원(사용자) 그룹 [중 하나에 구성원을 할당하여](sites-console.md#modifying-site-properties) 권한을 부여할 수 있습니다. 작성 환경에서 작업할 때 멤버는 [터널 서비스를 통해 게시 환경에서 볼 수 있습니다](#tunnel-service).

디자인 작업에서는 게시 환경에서 만든 구성원 및 구성원 그룹이 작성 환경에 나타나지 않아야 합니다. 작성 환경에서 만들어진 사용자 및 사용자 그룹은 작성 환경에 그대로 유지하려는 경우가 많습니다.

게시의 작성자 및 구성원이 동일한 LDAP 디렉토리에서 동기화된 것과 같은 동일한 사용자 목록에서 오는 경우 작성자 및 게시 환경 모두에서 동일한 권한 및 그룹 구성원을 가진 사용자로 간주되지 않습니다. 게시 및 작성자에 대해 적절한 방식으로 구성원 및 사용자의 역할을 별도로 설정해야 합니다.

게시 팜의 경우 [동일한 사용자 데이터에 액세스할 수 있도록 한 게시 인스턴스에서](topologies.md)수행한 등록 및 수정 사항을 다른 게시 인스턴스와 동기화해야 합니다. 자세한 내용은 [사용자 동기화](sync.md)를 참조하십시오. 여기에는 [다음 경우에 발생하는 상황에 대해 설명하는 섹션이 포함됩니다.](sync.md#what-happens-when).

### 기여도 제한 {#contribution-limits}

스팸으로부터 보호하기 위해 멤버의 게시 빈도를 제한할 수 있습니다. 또한 새로 등록한 멤버의 기부는 자동으로 제한할 수 있습니다.

자세한 내용은 [구성원 기여도 제한을 참조하십시오](limits.md).

### 동적으로 생성된 사용자 그룹 {#dynamically-created-user-groups}

새 커뮤니티 사이트를 만들면 새 사용자 그룹이 작성자 환경(작성자 그룹 역할 [참조) 또는 게시 환경(](#author-group-roles)게시 그룹 역할 [](#publish-group-roles)참조)에서 커뮤니티 사이트를 관리하는 데 필요한 다양한 관리 기능에 적합한 고유한 ID(uid)와 권한을 사용하여 동적으로 생성됩니다.

그룹 이름은 [커뮤니티 사이트를 만드는 동안 사이트에 제공된 이름에서 생성됩니다](sites-console.md#step13asitetemplate). 고유 ID는 동일한 서버에서 유사한 이름의 커뮤니티 사이트 및 커뮤니티 그룹에 대한 이름 충돌을 방지합니다.

예를 들어 &quot;We.Retail Engage&quot;라는 이름의 사이트에 대해 사이트 이름이 &quot;*참여*&quot;인 경우, 만들어진 사용자 그룹 중 하나가 다음과 같습니다.

* 커뮤니티 *참여* 회원

## 작성 환경 {#author-environment}

### 터널 서비스 {#tunnel-service}

작성 환경을 사용하여 사이트 [를](sites-console.md)만들고, 사이트 속성을 [수정하고](sites-console.md#modifying-site-properties) , 커뮤니티 구성원 및 구성원 그룹을 [관리할](members.md)때는 게시 환경에 등록된 사용자 및 사용자 그룹에 액세스해야 합니다.

터널 서비스는 작성자의 복제 에이전트를 사용하여 이 액세스를 제공합니다.

* 자세한 내용은 배포 페이지의 [구성 지침을](deploy-communities.md#tunnel-service-on-author) 참조하십시오.

[ [커뮤니티 구성원 및 그룹] 콘솔은](members.md) 게시 환경에서만 등록된 사용자(구성원) 및 사용자 그룹(구성원 그룹)을 관리하는 유일한 용도로만 사용됩니다.

작성 환경에 등록된 사용자 및 사용자 그룹을 관리하려면 [보안 콘솔을 사용하십시오](../../help/sites-administering/security.md)

### 작성자 그룹 역할 {#author-group-roles}

| 그룹의 구성원.. | 기본 역할 |
|---|---|
| 관리자 | 관리자 그룹은 커뮤니티 관리자의 모든 기능과 커뮤니티 관리자 그룹을 관리하는 기능을 가진 시스템 관리자로 구성됩니다. |
| 커뮤니티 관리자 | 커뮤니티 관리자 그룹은 자동으로 모든 커뮤니티 사이트 및 사이트에서 생성된 모든 커뮤니티 그룹의 구성원이 됩니다. 커뮤니티 관리자 그룹의 초기 구성원은 관리자 그룹입니다. 작성 환경에서 커뮤니티 관리자는 커뮤니티 사이트를 만들고, 사이트를 관리하고, 구성원을 관리하고(커뮤니티의 구성원을 금지할 수 있음), 컨텐츠를 중재할 수 있습니다. |
| 커뮤니티 &lt;*사이트 이름*> Siteontentmanager | 커뮤니티 사이트 컨텐츠 관리자는 커뮤니티 사이트에 대한 기존의 AEM 작성, 컨텐츠 작성 및 페이지 수정을 수행할 수 있습니다. |
| 커뮤니티 활성화 관리자 | 커뮤니티 활성 관리자 그룹은 커뮤니티 사이트의 활성 관리자 그룹을 관리하기 위해 할당할 수 있는 사용자로 구성됩니다. |
| 커뮤니티 &lt;*사이트 이름* > 사이트 활성화 관리자 | 커뮤니티 사이트 활성 관리자 그룹은 커뮤니티 사이트의 활성 [리소스를 관리하기 위해 지정된 사용자로 구성됩니다](resources.md). |
| 없음 | 익명의 사이트 방문자는 작성 환경에 액세스할 수 없습니다. |

### 시스템 관리자 {#system-administrators}

관리자 그룹의 구성원은 작성자 및 게시 환경 모두에 대해 AEM 설치의 초기 설정을 수행할 수 있는 시스템 관리자입니다.

데모 및 개발을 위해 관리자 그룹에는 admin *이고* 암호는 *admin*&#x200B;인 구성원이 있습니다.

프로덕션 환경의 경우 기본 관리자 그룹을 수정해야 합니다.

보안 체크리스트를 [반드시](../../help/sites-administering/security-checklist.md)따르십시오.

## 게시 환경 {#publish-environment}

### 회원이 되기 {#becoming-a-member}

게시 환경에서는 커뮤니티 사이트의 [설정에](sites-console.md#user-management) 따라 사이트 방문자가 커뮤니티 멤버가 될 수 있습니다.

* 커뮤니티 사이트가 비공개(폐쇄됨)인 경우:
   * 초대장
   * 관리자의 작업

* 커뮤니티 사이트가 공개(개방됨)인 경우:
   * 자가 등록
   * Facebook 및 Twitter를 통한 소셜 로그인

>[!NOTE]
>
>사이트 방문자가 하나의 개방형 커뮤니티 사이트의 구성원으로 등록하는 경우 동일한 게시 환경에서 다른 개방형 커뮤니티 사이트의 구성원이 자동으로 됩니다.


### 그룹 역할 게시 {#publish-group-roles}

| 그룹의 구성원.. | 기본 역할 |
|---|---|
| 커뮤니티 &lt;*사이트 이름*> 구성원 | 커뮤니티 사이트 멤버는 등록된 사용자입니다. 로그인, 프로필 수정, 열린 커뮤니티 그룹 참여, 커뮤니티에 컨텐츠 게시, 다른 구성원에게 메시지 보내기, 사이트 활동 팔로우 등이 가능합니다. |
| 커뮤니티 &lt;*사이트 이름*> 중재자 | 커뮤니티 사이트 중재자는 컨텐츠가 게시된 페이지에서 UGC를 일괄적으로, 중재 콘솔을 사용하거나 컨텍스트에서 중재할 수 있는 신뢰할 수 있는 커뮤니티 멤버입니다. |
| 커뮤니티 &lt;*사이트 이름*> &lt;*그룹 이름*> 구성원 | 커뮤니티 그룹 구성원은 공개 커뮤니티 그룹에 가입했거나 폐쇄된 커뮤니티 그룹에 초대된 커뮤니티 멤버입니다. 사이트 내의 해당 커뮤니티 그룹에 대한 구성원의 능력이 있습니다. |
| 커뮤니티 &lt;*사이트 이름*> 그룹 관리자 | 커뮤니티 사이트 그룹 관리자는 커뮤니티 사이트 내에서 하위 커뮤니티(그룹)를 만들고 관리하기 위해 할당된 신뢰할 수 있는 커뮤니티 멤버입니다. 컨텍스트 내 조정을 제공하는 기능이 포함되어 있습니다. |
| *권한이 있는 구성원 보안 그룹* | 컨텐츠 생성을 제한하기 위해 수동으로 만들고 유지 관리하는 사용자 그룹입니다. 권한 [있는 구성원 그룹을 참조하십시오](#privileged-members-group). |
| 없음 | 사이트를 검색하는 익명의 사이트 방문자는 익명 액세스를 허용하는 커뮤니티 사이트를 보고 검색할 수 있습니다. 콘텐트에 참여하고 게시하려면 사용자가 직접 등록(허용된 경우)하고 커뮤니티 멤버가 되어야 합니다. |

### 게시 그룹 역할에 구성원 할당 {#assigning-members-to-publish-group-roles}

작성 환경에서 커뮤니티 사이트 [를](sites-console.md) 만들거나 사이트 속성을 [수정할 때](sites-console.md#modifying-site-properties) 중재자, 그룹 관리자, 리소스 연락처 또는 권한 있는 멤버 등 게시 환경에서 수행되는 다양한 역할이 구성될 수 있습니다.

[터널 서비스를](sync.md#accessingpublishusersfromauthor) 활성화하면 작성자의 사용자가 아닌 게시 시 구성원이 할당 선택 항목을 보게 됩니다.

선택한 구성원은 자동으로 [해당 그룹에](#publish-group-roles) 할당되고 커뮤니티 사이트가 (re)게시될 때 해당 멤버십이 포함됩니다.

### 권한이 있는 구성원 그룹 {#privileged-members-group}

권한 있는 구성원 보안 그룹의 목적은 특정 커뮤니티 기능에 대한 컨텐츠 생성을 커뮤니티 사이트 구성원의 권한 하위 집합으로 제한하는 것입니다.

권한 있는 구성원 그룹은 커뮤니티 그룹 콘솔을 사용하여 만들고 관리하는 [구성원 그룹입니다](members.md).

권한이 있는 구성원 그룹을 만들고 [터널 서비스를 활성화한](sync.md#accessingpublishusersfromauthor)후 기존 커뮤니티 사이트의 구조를 수정하여 [](sites-console.md#modify-structure) 커뮤니티 기능의 구성을 &#39;권한이 있는 구성원 허용&#39;으로 편집하고 생성된 그룹을 추가할 수 있습니다.

하나 이상의 권한이 있는 구성원 그룹의 사양을 허용하는 커뮤니티 기능은 다음과 같습니다.

* [블로그 함수](functions.md#blog-function) - 새 아티클 만들기를 제한합니다.
* [달력 함수](functions.md#calendar-function) - 새 이벤트 만들기를 제한합니다.
* [포럼 함수](functions.md#forum-function) - 새 항목 생성을 제한하려면
* [QnA 함수](functions.md#qna-function) - 새 질문의 생성을 제한하려면

커뮤니티 기능에 보안이 설정되지 않은 경우(권한이 있는 구성원 그룹이 할당되지 않음) 모든 커뮤니티 사이트 구성원이 기능 컨텐츠(아티클, 이벤트, 주제, 질문)를 만들 수 있습니다.

>[!NOTE]
>
>커뮤니티 사이트의 권한 있는 구성원 그룹에 사용자를 추가하면 해당 사용자가 동일한 커뮤니티 사이트의 구성원일 경우에만 만들기 권한을 부여합니다.


## 커뮤니티 구성원 만들기 {#creating-community-members}

### 저장소 위치 {#repository-location}

특정 기능이 제대로 작동하려면 해당 권한이 있는 사용자 및 사용자 그룹을 만들어야 합니다.

구성원을 만들 때 `/home/users/community`는 멤버의 프로필에 읽기 권한을 부여하는 적절한 ACL을 상속받습니다.

마찬가지로 사용자 지정 커뮤니티 사용자 그룹(권한 있는 구성원 그룹 등)도 `/home/groups/community`

커뮤니티 [구성원 및 그룹 콘솔을](members.md) 사용하면 이러한 경로에서 사용자와 그룹을 만듭니다.

사용자 지정 경로를 지정하려면 https://&lt;server>:&lt;port>/useradmin에서 액세스할 수 있는 클래식 보안 UI를 [사용해야 합니다](http://localhost:4503/useradmin).

사용자 지정 멤버 경로에 대한 읽기 권한을 부여하려면 모든 게시 인스턴스에서 다음과 유사한 ACL을 설정합니다. `/home/users/community`

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

모든 게시 인스턴스에서 /home/groups/mycompany와 같은 사용자 지정 멤버 그룹 경로에 대한 적절한 권한을 부여하려면 다음과 유사한 ACL을 설정합니다. `/home/groups/community`

```xml
<allow
  jcr:primaryType="rep:GrantACE"
  rep:principalName="community-administrators"
  rep:privileges="{Name}[jcr:read]"  />
```

### 콘솔 {#consoles}

작성 환경에서만 사용할 수 있는 별도의 콘솔은 네 가지가 있습니다.

| console | 도구, 보안, 사용자 | 도구, 보안, 그룹 | 커뮤니티, 구성원 | 커뮤니티, 그룹 |
|----------|-----------------------|------------------------|------------------------------------------------------------|------------------------------------------------------------|
| 관리 | 작성자 사용자 | 작성자의 사용자 그룹 | 게시되는 구성원 | 게시 시 멤버 그룹 |
| required | 관리자 권한 | 관리자 권한 | 관리자 권한, 터널 서비스, 게시팜에 대한 사용자 동기화 | 관리자 권한, 터널 서비스, 게시팜에 대한 사용자 동기화 |

### 커뮤니티 활성화 관리자 역할 {#community-enablement-manager-role}

각 멤버와 관련된 비용이 있기 때문에 사이트 방문자가 직접 등록할 수 있는 기능은 [활성 커뮤니티에](overview.md#enablement-community) 대해 허용되지 않습니다. 역량 강화 학습자와 리소스는 작성자에 대한 사이트 작성 [](#author-group-roles) 중 `enablement manager` 의 역할 [을](sites-console.md#enablement) `Community <site-name> Siteenablementmanagers`할당한 사용자가 관리합니다(그룹의 구성원으로 추가). 또한 `enablement manager` 는 작성자의 커뮤니티 [구성원에게 학습 리소스를](resources.md) 할당할 책임이 있습니다.

글로벌 `Community Enablement Managers` 그룹의 구성원인 사용자만 특정 커뮤니티 사이트 `enablement manager` 의 구성원으로 선택할 수 있습니다.

의 역할을 할당할 수 있는 사용자를 만들려면 `Community Site Enablement Manager`클래식 UI 보안 콘솔을 사용하여 경로를 지정합니다.

작성 인스턴스에서:

1. 관리자 권한으로 로그인하면 클래식 UI 보안 콘솔로 이동합니다.

   예: [http://localhost:4502/useradmin](http://localhost:4502/useradmin)

2. 편집 메뉴에서 사용자 **[!UICONTROL 만들기를 선택합니다]**.
3. 대화 상자를 `Create User` 채웁니다.
   * 경로는 필수입니다 `/home/users/community`.
4. **[!UICONTROL 만들기]**&#x200B;를 선택합니다.

   ![create-community-user](assets/create-community-user.png)

* 왼쪽 창에서 새로 만든 사용자를 검색하고 오른쪽 창에 표시되도록 선택합니다.

   ![community-user](assets/view-community-user.png)

왼쪽 창에

1. 검색 상자를 지우고 사용자 **[!UICONTROL 숨기기를 선택합니다]**.
2. 오른쪽 창 `community-enablementmanagers` 에 표시된 새 사용자의 **[!UICONTROL 그룹]** 탭으로 끌어다 놓습니다.

   ![assign-group](assets/assign-group.png)

### 커뮤니티 관리자 역할 {#community-administrators-role}

작성자 그룹 역할 [](#author-group-roles) 차트에 명시된 대로 커뮤니티 관리자 그룹의 구성원은 커뮤니티 사이트를 만들고 사이트를 관리하며 구성원을 관리하고(커뮤니티의 구성원을 금지할 수 있음) 컨텐츠를 중재할 수 있습니다.

사용자를 만들고 활성 관리자 [역할에 할당하는 것과 같은 단계를 따르되, 사용자의 그룹 탭 아래에 c](#communitysiteenablementmanagerrole)`ommunity-administrators` 그룹을 추가합니다.

### LDAP 통합 {#ldap-integration}

AEM에서는 사용자 인증뿐만 아니라 사용자 계정 생성을 위해 LDAP를 사용할 수 있습니다. 이 내용은 AEM 6과 함께 [LDAP 구성에 자세히 설명되어 있습니다](../../help/sites-administering/ldap-config.md).

다음은 커뮤니티 구성원 및 구성원 그룹에 대한 일부 구성 세부 정보입니다.

1. 각 AEM 게시 인스턴스에 대해 LDAP를 구성합니다.
2. [LDAP ID 공급자](../../help/sites-administering/ldap-config.md#configuring-the-ldap-identity-provider)

   * 특별 지침 없음

3. [동기화 처리기](../../help/sites-administering/ldap-config.md#configuring-the-synchronization-handler)

   * 다음 속성을 설정합니다.

      * **[!UICONTROL 사용자 자동 멤버십]**: `community-<site name>-<uid>-members`
      * **[!UICONTROL 사용자 경로 접두사]**: `/community`
      * **[!UICONTROL 그룹 경로 접두사]**: `/community`

4. [외부 로그인 모듈](../../help/sites-administering/ldap-config.md#the-external-login-module)

   * 특별한 지시 사항 없음

그러면 사용자가 커뮤니티 사이트의 구성원 그룹 및 저장소 위치에 자동으로 할당되어 다른 사람의 프로필을 볼 수 `/home/users/community` 있는 적절한 권한을 `/home/groups/community`상속받게 됩니다.

* 이 `User auto membership` 값은 프로필의 `rep:authorizableId` (표시 이름)가 아닌 `givenName` 속성이어야 합니다.

## AEM 인스턴스 간 사용자 동기화 {#synchronizing-users-among-aem-instances}

게시 팜 [사용 시 사용자를 먼저 한 인스턴스로 가져와서 사용자가 동일한 경로를 각 게시 인스턴스에](topologies.md)갖고 있는지 확인하고 Sling에 사용자 동기화를 [](sync.md) 활성화하면 다른 게시 인스턴스에 사용자를 배포할 수 있습니다.

사용자 그룹을 가져오는 경우 사용자 그룹이 각 게시 인스턴스에 동일한 경로를 가지도록 하려면 한 인스턴스로 가져온 다음 내보낼 패키지를 [만들고](../../help/sites-administering/package-manager.md#creating-a-new-package) 다른 모든 게시 인스턴스에 해당 패키지를 설치합니다.

사용자 동기화를 통한 사용자 그룹 동기화는 향후 릴리스에 포함되지만 현재 사용자 동기화가 실행되면 사용자 그룹의 *멤버십만* 동기화됩니다.

## 커뮤니티 그룹 정보 {#about-community-groups}

그룹을 논의할 때 서로 다른 두 가지 주제가 있습니다.

* **[커뮤니티 그룹](overview.md#communitygroups)**

   커뮤니티 그룹은 커뮤니티 그룹 생성을 지원하는 커뮤니티 사이트의 게시 환경에서 만들 수 있는 하위 커뮤니티입니다. 커뮤니티 그룹을 만들면 웹 사이트에 더 많은 페이지가 추가되고 상위 커뮤니티 사이트와 유사한 방식으로 관리됩니다. 자세한 내용은 [Community Group Essentials](essentials-groups.md) for developers 및 [Community Group for authors](creating-groups.md) 를참조하십시오.

* **[구성원 그룹](../../help/sites-administering/security.md)**

   구성원 그룹은 구성원이 속해 있을 수 있고 그룹 콘솔을 통해 관리되는 그룹입니다. 이 페이지에 대한 논의의 상당 부분이 구성원 그룹에 할애되었습니다. 커뮤니티 사이트에 대해 자동으로 생성되는 멤버 그룹을 커뮤니티 그룹이라고 *`Community`*&#x200B;할 수 있으므로 토론의 컨텍스트를 고려해야 합니다.
