---
title: 커뮤니티 점수 및 배지
description: AEM Communities 채점 및 배지를 사용하면 커뮤니티 구성원을 식별하고 보상할 수 있습니다
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
tagskeywords: scoring, badging, badges, gamification
role: Admin
exl-id: 4aa857f7-d111-4548-8f03-f6d6c27acf51
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2851'
ht-degree: 2%

---

# 커뮤니티 점수 및 배지 {#communities-scoring-and-badges}

## 개요 {#overview}

AEM Communities 점수 및 배지 기능은 커뮤니티 구성원을 식별하고 보상하는 기능을 제공합니다.

채점 및 배지의 주요 측면은 다음과 같습니다.

* [배지 할당](#assign-and-revoke-badges) 커뮤니티 구성원의 역할을 식별합니다.

* [배지의 기본 상](#enable-scoring) 멤버에게 참여하도록 독려합니다(만들어진 컨텐츠의 양).

* [배지의 고급 수상](/help/communities/advanced.md) 구성원을 전문가로 식별합니다(만들어진 콘텐츠의 품질).

**참고** 배지의 수여가 [기본적으로 활성화되지 않음](/help/communities/implementing-scoring.md#main-pars-text-237875536).

>[!CAUTION]
>
>CRXDE Lite에 표시되는 구현 구조는 UI를 사용할 수 있게 되면 변경될 수 있습니다.

## 배지 {#badges}

회원들의 역할 또는 지역사회에서의 지위를 나타내기 위해 회원 이름 아래에 배지를 배치합니다. 배지는 이미지 또는 이름으로 표시될 수 있습니다. 이미지로 표시되는 경우 이 이름은 접근성을 위해 대체 텍스트로 포함됩니다.

기본적으로 배지는 저장소의 다음 위치에 있습니다.

* `/libs/settings/community/badging/images`

다른 위치에 저장되는 경우 모든 사용자가 읽을 수 있어야 합니다.

배지는 UGC에서 규칙에 따라 할당되었는지 혹은 습득되었는지에 따라 차별화된다. 현재 할당된 배지는 텍스트로 표시되고 획득한 배지는 이미지로 표시됩니다.

### 배지 관리 UI {#badge-management-ui}

커뮤니티 [배지 콘솔](/help/communities/badges.md) 획득(수상) 또는 커뮤니티에서 특정 역할을 수행할(할당) 때 멤버에 대해 표시할 수 있는 사용자 정의 배지를 추가할 수 있습니다.

### 할당된 배지 {#assigned-badges}

역할 기반 배지는 관리자가 커뮤니티에서의 역할에 따라 커뮤니티 구성원에게 할당합니다.

할당된(및 부여된) 배지는 선택한 항목에 저장됩니다. [SRP](/help/communities/srp.md) 및 은 직접 액세스할 수 없습니다. GUI를 사용할 수 있을 때까지 역할 기반 배지를 할당하는 유일한 방법은 코드 또는 cURL을 사용하는 것입니다. cURL 지침은 제목이 있는 섹션을 참조하십시오. [배지 할당 및 취소](#assign-and-revoke-badges).

릴리스에는 다음과 같은 세 가지 역할 기반 배지가 포함되어 있습니다.

* **중재자**
  `/libs/settings/community/badging/images/moderator/jcr:content/moderator.png`

* **그룹 관리자**
  `/libs/settings/community/badging/images/group-manager/jcr:content/group-manager.png`

* **권한이 있는 구성원**
  `/libs/settings/community/badging/images/privileged-member/jcr:content/privileged-member.png`

  ![할당된 배지](assets/assigned-badges.png)

### 수여된 배지 {#awarded-badges}

리워드 기반 배지는 커뮤니티 활동에서 적용된 규칙에 따라 커뮤니티 구성원에게 채점 서비스에서 부여됩니다.

배지가 활동에 대한 보상으로 나타나려면 다음 두 가지 상황이 발생해야 합니다.

* 배지는 다음과 같아야 합니다. [활성화됨](#enableforcomponent) 피쳐 컴포넌트
* 채점 및 배지 규칙은 다음과 같아야 합니다. [적용됨](#applytopage) 구성 요소가 배치된 페이지(또는 상위 항목)로 이동합니다.

이번 릴리스에는 3가지 보상 기반 배지가 포함됐다.

* **금**
  `/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

* **실버**
  `/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

* **브론즈**
  `/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

  ![수여된 배지](assets/awarded-badges.png)

>[!NOTE]
>
>부적절한 것으로 플래그가 지정된 게시물에 대해 부정적인 포인트를 할당하여 점수 값에 영향을 미치도록 채점 규칙을 구성할 수 있습니다. 그러나 배지를 획득하면 채점 점수 감소 또는 채점 규칙 변경으로 인해 자동으로 제거되지 않습니다.
>
>부여된 배지는 할당된 배지와 동일한 방식으로 해지될 수 있습니다. 다음을 참조하십시오. [배지 할당 및 취소](#assign-and-revoke-badges) 섹션. 향후 개선 사항에는 구성원의 배지를 관리하는 UI가 포함됩니다.

### 사용자 정의 배지 {#custom-badges}

사용자 정의 배지는 다음을 사용하여 설치할 수 있습니다. [배지 콘솔](/help/communities/badges.md) 및 이 할당되거나 배지 규칙에 지정됩니다.

배지 콘솔에서 설치하면 사용자 지정 배지가 게시 환경에 자동으로 복제됩니다.

## 채점 활성화 {#enable-scoring}

채점은 기본적으로 활성화되어 있지 않습니다. 채점 및 배지 수여를 설정하고 활성화하는 기본 단계는 다음과 같습니다.

* 포인트 적립에 대한 규칙 확인([채점 규칙](#scoring-rules)).
* 채점 규칙당 누적된 점수에 대해 다음을 지정합니다. [배지](#badges) ([배지 규칙](#badging-rules)).

* [커뮤니티 사이트에 채점 및 배지 규칙 적용](#apply-rules-to-content).
* [커뮤니티 기능에 대한 배지 활성화](#enable-badges-for-component).

다음을 참조하십시오. [빠른 테스트](#quick-test) 포럼 및 댓글에 대한 기본 점수 및 배지 규칙을 사용하여 커뮤니티 사이트에 대한 점수를 활성화할 수 있는 섹션입니다.

### 콘텐츠에 규칙 적용 {#apply-rules-to-content}

채점 및 배지를 활성화하려면 속성을 추가합니다 `scoringRules` 및 `badgingRules` 를 사이트의 콘텐츠 트리에 있는 모든 노드에 추가합니다.

사이트가 이미 게시된 경우 모든 규칙을 적용하고 구성 요소를 활성화한 후 사이트를 다시 게시합니다.

배지 활성화 구성 요소에 적용되는 규칙은 현재 노드 또는 해당 상위 요소에 대한 규칙입니다.

노드가 유형인 경우 `cq:Page` (권장) 그런 다음 CRXDE|Lite를 사용하여 속성에 속성을 추가합니다 `jcr:content` 노드.

| **속성** | **유형** | **설명** |
|---|---|---|
| 배지 규칙 | 문자열 | 의 배열 목록 [배지 규칙](#badging-rules) |
| scoringRules | 문자열 | 의 배열 목록 [채점 규칙](#scoring-rules) |

>[!NOTE]
>
>채점 규칙이 배지를 부여하는 데 영향을 주지 않는 것으로 표시되면 채점 규칙이 배지 규칙의 scoringRules 속성에 의해 차단되지 않았는지 확인합니다. 제목이 있는 섹션 참조 [배지 규칙](#badging-rules).

### 구성 요소에 대한 배지 활성화 {#enable-badges-for-component}

채점 및 배지 규칙은 의 구성 요소 구성을 편집하여 배지를 사용할 수 있도록 한 구성 요소 인스턴스에만 적용됩니다. [작성 모드](/help/communities/author-communities.md).

부울 속성, `allowBadges`구성 요소 인스턴스에 대한 배지 표시를 활성화/비활성화합니다. 다음에서 구성할 수 있습니다. [구성 요소 편집 대화 상자](/help/communities/author-communities.md) 포럼, QnA 및 확인란으로 레이블이 지정된 확인란을 통한 주석 구성 요소의 경우 **배지 표시**.

#### 예 : 포럼 구성 요소 인스턴스에 대한 allowBadges {#example-allowbadges-for-forum-component-instance}

![enable-badges-component](assets/enable-badges-component.png)

>[!NOTE]
>
>모든 구성 요소를 오버레이하여 포럼에 있는 HBS 코드, QnA 및 주석을 사용하여 배지를 표시할 수 있습니다.

## 채점 규칙 {#scoring-rules}

채점 규칙은 배지를 수여하기 위한 채점의 기초입니다.

각 채점 규칙은 하나 이상의 하위 규칙 목록입니다. 채점 규칙은 커뮤니티 사이트 콘텐츠에 적용되어 배지가 활성화될 때 적용할 규칙을 식별합니다.

채점 규칙은 상속되지만 가산되지는 않습니다. 예:

* page2에 채점 규칙2가 포함되어 있고 상위 page1에 채점 규칙1이 포함된 경우.
* page2 구성 요소에 대한 작업은 rule1과 rule2를 모두 호출합니다.
* 두 규칙 모두에 동일한 적용 가능한 하위 규칙이 포함된 경우 `topic/verb`:

   * rule2의 하위 규칙만 점수에 영향을 줍니다.
   * 두 하위 규칙의 점수는 추가되지 않습니다.

채점 규칙이 두 개 이상인 경우, 점수는 각 규칙마다 별도로 유지된다.

채점 규칙은 유형의 노드입니다. `cq:Page` 속성 포함 `jcr:content` 정의하는 하위 규칙 목록을 지정하는 노드입니다.

점수는 SRP에 저장됩니다.

>[!NOTE]
>
>모범 사례: 각 채점 규칙의 이름을 고유하게 지정합니다.
>
>채점 규칙 이름은 전체적으로 고유해야 하며 동일한 이름으로 끝나서는 안 됩니다.
>
>의 예 *아님* 수행 방법:
>
>/libs/settings/community/scoring/rules/site1/forums-scoring
>/libs/settings/community/scoring/rules/site2/forums-scoring

### 채점 하위 규칙 {#scoring-sub-rules}

채점 하위 규칙에는 커뮤니티에 참여하기 위한 값을 자세히 설명하는 속성이 포함됩니다.

각 채점 하위 규칙은 다음을 식별합니다.

* 어떤 활동이 추적 중입니까?
* 어떤 특정 커뮤니티 기능이 관련됩니까?
* 몇 점이 주어집니까?

하위 규칙이 콘텐츠의 소유자를 점을 받는 것으로 지정하지 않는 한 기본적으로 작업을 수행하는 멤버에 점이 부여됩니다( `forOwner`).

각 하위 규칙은 하나 이상의 채점 규칙에 포함될 수 있습니다.

하위 규칙의 이름은 일반적으로 를 사용하는 패턴을 따릅니다. *제목*, *오브젝트*, 및 *verb*. 예:

* member-comment-create
* 회원 수신 투표

하위 규칙은 유형의 노드입니다. `cq:Page` 속성 포함 `jcr:content`를 지정하는 노드 [동사와 주제](#topics-and-verbs) .

<table>
 <tbody>
  <tr>
   <th>속성</th>
   <th>유형</th>
   <th> 값 설명</th>
  </tr>
  <tr>
   <td><i><code>VERB</code></i></td>
   <td>긴</td>
   <td>
    <ul>
     <li>필수, 동사는 이벤트 작업에 해당합니다.</li>
     <li>동사 속성이 하나 이상 있어야 합니다.</li>
     <li>동사는 모두 대문자로 입력해야 합니다.</li>
     <li>여러 동사 속성이 있을 수 있지만 중복은 없습니다</li>
     <li>값은 이 이벤트에 적용할 점수입니다</li>
     <li>값은 양수이거나 음수일 수 있습니다.</li>
     <li>이번 릴리스에서 지원되는 동사 목록은 <a href="#topics-and-verbs">주제 및 동사</a> 섹션</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>topics</code></td>
   <td>문자열</td>
   <td>
    <ul>
     <li>선택 사항, 이벤트 주제별로 식별된 커뮤니티 구성 요소로 하위 규칙 제한</li>
     <li>지정된 경우 : 값이 이벤트 주제의 다중 값 문자열입니다</li>
     <li>이 릴리스의 주제 목록은 <a href="#topics-and-verbs">주제 및 동사</a> 섹션</li>
     <li>기본적으로 동사와 관련된 모든 주제에 적용됩니다</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>forOwner</code></td>
   <td>부울</td>
   <td>
    <ul>
     <li>선택 사항, 구성원이 자신이 소유한 콘텐츠를 기반으로 활동할 때 관련성이 없음</li>
     <li>true인 경우 작업 중인 콘텐츠의 소유자에게 점수를 적용합니다.</li>
     <li>false인 경우 멤버 실행 작업에 점수를 적용합니다.</li>
     <li>기본값은 false입니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>scoringType</code></td>
   <td>문자열</td>
   <td>
    <ul>
     <li>선택 사항, 채점 엔진 식별</li>
     <li>"basic"이면 수량을 기반으로 채점 엔진을 지정합니다.
      <ul>
       <li>릴리스에 포함됨</li>
      </ul> </li>
     <li>"고급"인 경우 품질 및 수량을 기반으로 채점 엔진을 지정합니다
      <ul>
       <li>을(를) 필요로 합니다. <a href="/help/communities/advanced.md">추가 패키지</a></li>
      </ul> </li>
     <li>기본값은 "기본"입니다.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 채점 규칙 및 하위 규칙 포함 {#included-scoring-rules-and-sub-rules}

릴리스에는 다음에 대한 두 가지 채점 규칙이 포함되어 있습니다. [포럼 기능](/help/communities/functions.md#forum-function) ( 포럼 기능의 포럼 및 주석 구성 요소에 대해 각각 하나씩) :

1. /libs/settings/community/scoring/rules/comments-scoring

   * 하위 규칙[] = /libs/settings/community/scoring/rules/sub-rules/member-comment-create /libs/settings/community/scoring/rules/sub-rules/member-receive-vote /libs/settings/community/scoring/rules/sub-rules/member-give-vote /libs/settings/community/scoring/rules/sub-rules/member-is-moderated

1. /libs/settings/community/scoring/rules/forums-scoring

   * 하위 규칙[] = /libs/settings/community/scoring/rules/sub-rules/member-forum-create /libs/settings/community/scoring/rules/sub-rules/member-receive-vote /libs/settings/community/scoring/rules/sub-rules/member-give-vote /libs/settings/community/scoring/rules/sub-rules/member-is-moderated

**메모:**

* 모두 `rules` 및 `sub-rules` 노드는 cq:Page 유형입니다.

* `subRules` 은(는) String 유형의 속성입니다.[] 규칙에 따라 `jcr:content` 노드.

* `sub-rules` 다양한 채점 규칙 간에 공유할 수 있습니다.
* `rules` 은(는) 모든 사람에 대한 읽기 권한이 있는 저장소 위치에 있어야 합니다.

   * 규칙 이름은 위치에 관계없이 고유해야 합니다.

### 사용자 지정 점수 규칙 활성화 {#activating-custom-scoring-rules}

작성 환경에서 수행한 채점 규칙 또는 하위 규칙에 대한 변경 또는 추가 사항은 게시에 설치해야 합니다.

## 배지 규칙 {#badging-rules}

배지 규칙은 다음을 지정하여 점수 규칙을 배지에 연결합니다.

* 채점 규칙
* 특정 배지를 수여하는 데 필요한 점수

배지 규칙은 유형의 노드입니다. `cq:Page` 속성 포함 `jcr:content` 채점 규칙을 점수 및 배지와 연관시키는 노드입니다.

배지 규칙은 필수 항목으로 구성되어 있습니다 `thresholds` 배지에 매핑된 점수의 순서가 지정된 목록입니다. 점수는 값을 늘려서 주문해야 합니다. 예:

* `1|/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

   * 브론즈 배지는 1점 획득으로 수여된다.

* `60|/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

   * 실버 배지는 60점이 누적되면 수여된다.

* `80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

   * 골드 배지는 80점이 적립되면 수여된다.

배지 규칙은 점수가 누적되는 방법을 결정하는 점수 규칙과 쌍을 이룹니다. 제목이 있는 섹션 참조 [콘텐츠에 규칙 적용](#apply-rules-to-content).

다음 `scoringRules` 배지 규칙의 속성은 해당 특정 배지 규칙과 연결할 수 있는 점수 규칙을 제한합니다.

>[!NOTE]
>
>모범 사례 : 각 AEM 사이트에 고유한 배지 이미지를 만듭니다.

![배지 규칙 구성](assets/badging-rule-configuration.png)

<table>
 <tbody>
  <tr>
   <th>속성</th>
   <th>유형</th>
   <th>값 설명</th>
  </tr>
  <tr>
   <td>임계값</td>
   <td>문자열</td>
   <td><em>(필수)</em> "숫자|경로" 형식의 다중 값 문자열
    <ul>
     <li>number = 점수</li>
     <li>| = 세로줄 문자(U+007C)</li>
     <li>경로 = 배지 이미지 리소스에 대한 전체 경로</li>
    </ul> 숫자가 점점 커지도록 문자열을 정렬해야 하며 숫자와 경로 사이에 공백이 생기지 않아야 합니다.<br /> 예제 항목 :<br /> <code>80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png</code></td>
  </tr>
  <tr>
   <td>배지 유형</td>
   <td>문자열</td>
   <td><em>(선택 사항)</em> 채점 엔진을 "기본" 또는 "고급"으로 식별합니다. 고급 채점 엔진이 필요한 경우 다음을 참조하십시오. <a href="/help/communities/advanced.md">고급 점수 및 배지</a>. 기본값은 "기본"입니다.</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>문자열</td>
   <td>(<em>선택 사항</em>) 배지 규칙을 채점 규칙으로 식별되는 채점 이벤트로 제한하는 다중 값 문자열</td>
  </tr>
 </tbody>
</table>

### 포함된 배지 규칙 {#included-badging-rules}

릴리스에는 다음과 같은 두 가지 배지 규칙이 포함되어 있습니다. [포럼 및 주석 채점 규칙](#includedscoringrules).

* `/libs/settings/community/badging/rules/comments-badging`

* `/libs/settings/community/badging/rules/forums-badging`

**메모:**

* `rules` 노드는 cq:Page 유형입니다.
* `rules` 은(는) 모든 사람에 대한 읽기 권한이 있는 저장소 위치에 있어야 합니다.

   * 규칙 이름은 위치에 관계없이 고유해야 합니다.

### 사용자 지정 배지 규칙 활성화 {#activating-custom-badging-rules}

작성 환경에서 만들어진 배지 규칙 또는 이미지에 대한 변경 사항 또는 추가 사항은 게시에 설치해야 합니다.

## 배지 할당 및 취소 {#assign-and-revoke-badges}

배지는 다음 중 하나를 사용하여 구성원에게 할당될 수 있습니다. [구성원 콘솔](/help/communities/members.md#badges-tab) 또는 프로그래밍 방식으로 cURL 명령을 사용합니다.

다음 cURL 명령은 배지 할당 및 취소를 위한 HTTP 요청에 필요한 사항을 보여 줍니다. 기본 형식은 다음과 같습니다.

cURL -i -X POST -H *머리글* -u *로그인* -F *작업* -F *배지* *member-profile-url*

*머리글* = 서버에 전달할 &quot;Accept:application/json&quot; 사용자 지정 헤더(필수)

*로그인* = administrator-id:password(예: admin:admin)

*작업* = &quot;:operation=social:assignBadge&quot; OR &quot;:operation=social:deleteBadge&quot;

*배지* = &quot;badgeContentPath=*badge-image-file*&quot;

*badge-image-file* = 저장소에서 배지 이미지 파일의 위치(예: /libs/settings/community/badging/images/moderator/jcr:content/moderator.png)

*member-profile-url* = 게시할 때 멤버 프로필의 끝점(예: https://)&lt;server>:&lt;port>/home/users/community/riley/profile.social.json

>[!NOTE]
>
>다음 *member-profile-url*:
>
>* 다음과 같은 경우 작성자 인스턴스를 참조할 수 있습니다. [터널 서비스](/help/communities/users.md#tunnel-service) 이(가) 활성화되었습니다.
>* 애매모호한 무작위 이름일 수 있음 - 다음을 참조하십시오. [보안 검사 목록](/help/sites-administering/security-checklist.md#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path) 승인 가능 ID에 대한 정보.

### 예: {#examples}

#### 중재자 배지 할당 {#assign-a-moderator-badge}

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:assignBadge" -F "badgeContentPath=/libs/settings/community/badging/images/moderator/jcr:content/moderator.png" /home/users/community/updcs9DndLEI74DB9zsB/profile.social.json
```

#### 할당된 실버 배지 취소 {#revoke-an-assigned-silver-badge}

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:deleteBadge" -F "badgeContentPath=/libs/settings/community/badging/images/silver/jcr:content/silver.png" /home/users/community/updcs9DndLEI74DB9zsB/profile.social.json
```

>[!NOTE]
>
>cURL을 사용하여 배지를 할당하거나 취소하면 모든 배지 이미지에 대해 작동하지만, 획득한 대신 할당된 경우 할당된 배지로 표시되고 그에 따라 처리됩니다.

## 사용자 지정 구성 요소에 대한 점수 및 배지 {#scoring-and-badges-for-custom-components}

구성 요소에 대해 만들어진 이벤트 주제를 동사와 연결하여 사용자 지정 구성 요소에 대한 점수 및 배지 규칙을 만들 수 있습니다.

## 주제 및 동사 {#topics-and-verbs}

구성원이 커뮤니티 기능과 상호 작용할 때 알림 및 점수와 같은 비동기 리스너를 트리거할 수 있는 이벤트가 전송됩니다.

구성 요소의 SocialEvent 인스턴스는 이벤트를 다음과 같이 기록합니다. `actions` 다음 기간 동안 발생 `topic`. SocialEvent에는 를 반환하는 메서드가 포함되어 있습니다. `verb` 작업과 연결되었습니다. 다음 항목이 있습니다. *-* 다음 사이의 관계 `actions` 및 `verbs`.

전달된 커뮤니티 구성 요소의 경우 다음 표에서는 `verbs` 각각에 대해 정의됨 `topic` 에서 사용 가능 [채점 하위 규칙](#scoring-sub-rules).

>[!NOTE]
>
>새 부울 속성, `allowBadges`구성 요소 인스턴스에 대한 배지 표시를 활성화/비활성화합니다. 업데이트에서 구성할 수 있습니다 [구성 요소 편집 대화 상자](/help/communities/author-communities.md) 레이블이 지정된 확인란을 통해 **배지 표시**.

**[달력 구성 요소](/help/communities/calendar.md)**
SocialEvent `topic`= com/adobe/cq/social/calendar

| **동사** | **설명** |
|---|---|
| POST | 구성원이 캘린더 이벤트를 만듭니다. |
| 추가 | 일정 이벤트에 대한 구성원 댓글 |
| 업데이트 | 멤버의 캘린더 이벤트 또는 댓글이 편집되었습니다. |
| 삭제 | 멤버의 캘린더 이벤트 또는 댓글이 삭제되었습니다. |

**[주석 구성 요소](/help/communities/comments.md)**
SocialEvent `topic`= com/adobe/cq/social/comment

| **동사** | **설명** |
|---|---|
| POST | 구성원이 주석을 만듭니다. |
| 추가 | 댓글에 대한 구성원 답글 |
| 업데이트 | 멤버의 주석이 편집됨 |
| 삭제 | 구성원의 댓글이 삭제되었습니다. |

**[파일 라이브러리 구성 요소](/help/communities/file-library.md)**
SocialEvent `topic`= com/adobe/cq/social/fileLibrary

| **동사** | **설명** |
|---|---|
| POST | 구성원이 폴더를 만듭니다. |
| 첨부 | 구성원이 파일을 업로드합니다. |
| 업데이트 | 구성원이 폴더 또는 파일을 업데이트합니다. |
| 삭제 | 구성원이 폴더 또는 파일을 삭제합니다. |

**[포럼 구성 요소](/help/communities/forum.md)**
SocialEvent `topic`= com/adobe/cq/social/forum

| **동사** | **설명** |
|---|---|
| POST | 구성원이 포럼 주제를 만듭니다. |
| 추가 | 포럼 주제에 대한 구성원 답글 |
| 업데이트 | 회원의 포럼 주제 또는 답글이 편집되었습니다. |
| 삭제 | 회원의 포럼 주제 또는 답글이 삭제되었습니다. |

**[저널 구성 요소](/help/communities/blog-feature.md)**
SocialEvent `topic`= com/adobe/cq/social/journal

| **동사** | **설명** |
|---|---|
| POST | 구성원이 블로그 문서를 만듭니다. |
| 추가 | 블로그 기사에 대한 구성원 댓글 |
| 업데이트 | 멤버의 블로그 문서 또는 댓글이 편집되었습니다. |
| 삭제 | 멤버의 블로그 문서나 댓글이 삭제되었습니다. |

**[QnA 구성 요소](/help/communities/working-with-qna.md)**
SocialEvent `topic` = com/adobe/cq/social/qna

| **동사** | **설명** |
|---|---|
| POST | 멤버가 QnA 질문을 만듭니다. |
| 추가 | 멤버가 QnA 답변을 만듭니다. |
| 업데이트 | 멤버의 Q&amp;A 질문 또는 답변이 편집되었습니다. |
| 선택 | 멤버의 답변이 선택됨 |
| 선택 취소 | 멤버의 답변이 선택 해제되었습니다. |
| 삭제 | 멤버의 Q&amp;A 질문 또는 답변이 삭제되었습니다. |

**[리뷰 구성 요소](/help/communities/reviews.md)**
SocialEvent `topic`= com/adobe/cq/social/review

| **동사** | **설명** |
|---|---|
| POST | 멤버가 리뷰 생성 |
| 업데이트 | 구성원의 리뷰가 편집됨 |
| 삭제 | 구성원의 검토 삭제됨 |

**[등급 구성 요소](/help/communities/rating.md)**
SocialEvent `topic`= com/adobe/cq/social/tally/rating

| **동사** | **설명** |
|---|---|
| 등급 추가 | 구성원의 콘텐츠가 등급이 올라갔습니다. |
| 등급 제거 | 멤버의 컨텐츠가 다운그레이드되었습니다. |

**[투표 구성 요소](/help/communities/voting.md)**
SocialEvent `topic`= com/adobe/cq/social/tally/voting

| **동사** | **설명** |
|---|---|
| 투표 추가 | 구성원의 콘텐츠가 투표에 부쳐졌습니다. |
| 투표 제거 | 구성원의 콘텐츠가 부결되었습니다. |

**중재 활성화 구성 요소**
SocialEvent `topic`= com/adobe/cq/social/moderation

| **동사** | **설명** |
|---|---|
| 거부 | 구성원의 콘텐츠가 거부되었습니다. |
| 부적절한 항목으로 표시 | 멤버의 컨텐츠에 플래그가 지정되었습니다. |
| 부적절한 항목으로 플래그 해제 | 멤버의 컨텐츠에 플래그가 지정되지 않음 |
| ACCEPT | 멤버의 컨텐츠가 중재자에 의해 승인됨 |
| 닫기 | 구성원이 댓글을 닫아 편집하고 답글을 남깁니다. |
| 열기 | 구성원이 주석을 다시 엽니다. |

### 사용자 지정 구성 요소 이벤트 {#custom-component-events}

사용자 지정 구성 요소의 경우 SocialEvent가 인스턴스화되어 구성 요소의 이벤트를 다음으로 기록합니다. `actions` 다음 기간 동안 발생 `topic`.

채점을 지원하려면 SocialEvent가 메서드를 재정의해야 합니다 `getVerb()` 그래서 적절한 `verb` 다음에 대해 반환됩니다 `action`. 다음 `verb` 작업에 대해 반환되는 항목은 일반적으로 사용되는 항목(예: `POST`) 또는 구성 요소용으로 특수 제작된 것(예: `ADD RATING`). 다음 항목이 있습니다. *-* 다음 사이의 관계 `actions` 및 `verbs`.

## 문제 해결 {#troubleshooting}

### 배지가 표시되지 않음 {#badges-are-not-appearing}

채점 및 배지 규칙이 웹 사이트의 콘텐츠에 적용되었지만, 배지가 활동에 대해 부여되지 않는 경우 해당 구성 요소의 인스턴스에 대해 배지가 활성화되었는지 확인하십시오.

다음을 참조하십시오 [구성 요소에 대한 배지 활성화](#enable-badges-for-component).

### 채점 규칙이 적용되지 않음 {#scoring-rule-has-no-effect}

채점 및 배지 규칙이 웹 사이트 콘텐츠에 적용되었으며 배지가 일부 작업에 대해 부여되고 있지만 다른 작업에 대해 부여되지 않은 경우 배지 규칙이 적용되는 채점 규칙을 제한하지 않았는지 확인하십시오.

다음을 참조하십시오. `scoringRules` 다음의 속성 [배지 규칙](#badging-rules).

### 대/소문자 오타 {#case-sensitive-typo}

대부분의 속성 및 값, 특히 동사는 대/소문자를 구분합니다. 채점 하위 규칙에서 동사는 모두 대문자로 사용해야 합니다.

기능이 예상대로 작동하지 않는 경우 데이터가 올바르게 입력되었는지 확인하십시오.

## 빠른 테스트 {#quick-test}

를 사용하여 채점 및 배지를 빠르게 시도할 수 있습니다. [시작 자습서](/help/communities/getting-started.md) (engage) 사이트:

* 작성자의 CRXDE Lite에 액세스합니다.
* 기본 페이지로 이동합니다.

   * /content/sites/engage/en/jcr:content

* badgingRules 속성을 추가합니다.

   * **이름**: `badgingRules`
   * **유형**: `String`
   * 선택 **다중**
   * 선택 **추가**
   * 입력 `/libs/settings/community/badging/rules/forums-badging`
   * 선택 **+**
   * 입력 `/libs/settings/community/badging/rules/comments-badging`
   * 선택 **확인**

* scoringRules 속성을 추가합니다.

   * **이름**: `scoringRules`
   * **유형**: `String`
   * 선택 **다중**
   * 선택 **추가**
   * 입력 `/libs/settings/community/scoring/rules/forums-scoring`
   * 선택 **+**
   * 입력 `/libs/settings/community/scoring/rules/comments-scoring`
   * 선택 **확인**

* 선택 **모두 저장**.

![시험 채점 배지](assets/test-scoring-badging.png)

그런 다음 포럼 및 댓글 구성 요소에서 배지를 표시할 수 있는지 확인합니다.

* 다시 CRXDE Lite 사용.
* 포럼 구성 요소 찾아보기

   * `/content/sites/engage/en/forum/jcr:content/content/primary/forum`

* 필요한 경우 allowBadges 부울 속성을 추가하고 true인지 확인합니다.

   * **이름**: `allowBadges`
   * **유형**: `Boolean`
   * **값**: `true`

![test-forum-component](assets/test-forum-component.png)

다음, [다시 게시](/help/communities/sites-console.md#publishing-the-site) 커뮤니티 사이트입니다.

마지막으로,

* 게시 인스턴스에서 구성 요소를 찾습니다.
* 커뮤니티 구성원으로 로그인합니다(예: weston.mccall@dodgit.com / 암호).
* 새 포럼 주제를 게시합니다.
* 배지를 표시하려면 페이지를 새로 고쳐야 합니다.

   * 로그아웃한 후 다른 커뮤니티 구성원으로 로그인합니다(예: aaron.mcdonald@mailinator.com/password).

* 포럼을 선택합니다.

커뮤니티 회원은 첫 번째 포럼 배지 규칙의 첫 번째 임계값이 1이기 때문에 포럼 게시물이 표시되는 브론즈 배지를 받게 됩니다.

![기관지배지](assets/bronzebadge.png)

## 추가 정보 {#additional-information}

자세한 내용은 [채점 및 배지 핵심 사항](/help/communities/configure-scoring.md) 개발자용 페이지입니다.

고급 채점 엔진에 대한 자세한 내용은 [고급 점수 및 배지](/help/communities/advanced.md).

구성 가능한 순위표 [구성 요소](/help/communities/enabling-leaderboard.md) 및 [함수](/help/communities/functions.md#leaderboard-function) 커뮤니티 사이트에 회원 및 회원 점수를 쉽게 표시할 수 있습니다.
