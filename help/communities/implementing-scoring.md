---
title: 커뮤니티 점수 및 배지
seo-title: Communities Scoring and Badges
description: AEM Communities 점수 및 배지를 통해 커뮤니티 구성원을 식별하고 포상할 수 있습니다
seo-description: AEM Communities scoring and badges lets you identify and reward community members
uuid: d73683df-a413-4b3c-869c-67568bfdfcf6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ea033bb9-cb92-4c93-855f-8c902999378c
docset: aem65
tagskeywords: scoring, badging, badges, gamification
role: Admin
exl-id: 4aa857f7-d111-4548-8f03-f6d6c27acf51
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '2868'
ht-degree: 2%

---

# 커뮤니티 점수 및 배지 {#communities-scoring-and-badges}

## 개요 {#overview}

AEM Communities 점수 및 배지 기능은 커뮤니티 구성원을 식별하고 포상하는 기능을 제공합니다.

점수부여 및 배지의 주요 특징은 다음과 같습니다.

* [배지 할당](#assign-and-revoke-badges) 커뮤니티에서 구성원의 역할을 식별하는 데 사용됩니다.

* [기본 배지 훈장](#enable-scoring) 참여도를 유도하기 위해(생성된 컨텐츠의 수량)

* [고급 배지 훈장](/help/communities/advanced.md) 구성원을 전문가로 식별하기 위해(생성된 컨텐츠의 품질)

**참고** 그 배지는 [기본적으로 활성화되지 않음](/help/communities/implementing-scoring.md#main-pars-text-237875536).

>[!CAUTION]
>
>CRXDE Lite에 표시되는 구현 구조는 UI를 사용할 수 있게 되면 변경될 수 있습니다.

## 배지 {#badges}

배지를 회원명부에 올려놓고 회원들의 역할이나 지역 사회 내 지위를 나타내는 배지도 있다. 배지는 이미지 또는 이름으로 표시될 수 있습니다. 이미지로 표시되면 액세스 가능성이 있는 대체 텍스트로 이름이 포함됩니다.

기본적으로 배지는 다음 리포지토리에 있습니다.

* `/libs/settings/community/badging/images`

다른 위치에 저장된 경우 모든 사람이 읽을 수 있어야 합니다.

배지는 UGC에서 할당된 배지 또는 받은 배지가 규칙에 따라 차별화된다. 현재, 지정된 배지는 텍스트로 표시되고 획득된 배지는 이미지로 나타납니다.

### 배지 관리 UI {#badge-management-ui}

커뮤니티 [배지 콘솔](/help/communities/badges.md) 은(는) 획득할 때(수상) 또는 커뮤니티에서 특정 역할을 수행할 때(지정된) 회원에게 표시할 수 있는 사용자 지정 배지를 추가할 수 있는 기능을 제공합니다.

### 지정된 배지 {#assigned-badges}

역할 기반 배지는 관리자가 커뮤니티에서 자신의 역할에 따라 커뮤니티 구성원에게 지정합니다.

지정된(및 꺼진) 배지는 선택한 위치에 저장됩니다 [SRP](/help/communities/srp.md) 및에 직접 액세스할 수 없습니다. GUI를 사용할 수 있을 때까지 역할 기반 배지를 할당하는 유일한 방법은 코드나 cURL을 사용하여 할당하는 것입니다. cURL 지침은 [배지 할당 및 취소](#assign-and-revoke-badges).

이번 릴리스에는 세 가지 역할 기반 배지가 포함되어 있습니다.

* **중재자**

   `/libs/settings/community/badging/images/moderator/jcr:content/moderator.png`

* **그룹 관리자**

   `/libs/settings/community/badging/images/group-manager/jcr:content/group-manager.png`

* **권한 있는 멤버**

   `/libs/settings/community/badging/images/privileged-member/jcr:content/privileged-member.png`

   ![지정된 배지](assets/assigned-badges.png)

### 수상 배지 {#awarded-badges}

보상 기반 배지는 지역 사회의 활동에 적용된 규칙에 따라 지역 사회 구성원들에게 점수 부여 서비스에 의해 수여됩니다.

배지가 활동에 대한 보상으로 나타나게 하려면, 일어나야 하는 두 가지 사항이 있습니다.

* 배지가 있어야 합니다. [활성화됨](#enableforcomponent) 피쳐 구성 요소에 사용할 수 있습니다.
* 점수부여 및 배지 규칙은 [적용됨](#applytopage) 를 구성 요소가 배치된 페이지(또는 상위 페이지)에 추가합니다.

이번 릴리스에는 세 가지 현상금이 걸려 있습니다.

* **금**

   `/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

* **은**

   `/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

* **청동**

   `/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

   ![수상 배지](assets/awarded-badges.png)

>[!NOTE]
>
>점수 규칙은 부적절한 것으로 플래그가 지정된 게시물에 대해 음수를 할당하도록 구성되어 있어서 점수 값에 영향을 줄 수 있습니다. 그러나 배지가 획득되면 점수 포인트 감소 또는 점수 규칙 변경 때문에 배지가 자동으로 제거되지 않습니다.
>
>수여된 배지는 지정된 배지와 동일한 방식으로 취소할 수 있습니다. 자세한 내용은 [배지 할당 및 취소](#assign-and-revoke-badges) 섹션을 참조하십시오. 향후 개선 사항에는 구성원의 배지를 관리할 UI가 포함됩니다.

### 사용자 지정 배지 {#custom-badges}

사용자 지정 배지는 [배지 콘솔](/help/communities/badges.md) 및 을 배지 규칙에 할당하거나 지정합니다.

Badge 콘솔에서 설치되면 사용자 지정 배지가 게시 환경에 자동으로 복제됩니다.

## 점수 책정 활성화 {#enable-scoring}

기본적으로 점수는 활성화되지 않습니다. 배지 점수 책정 및 수상을 위한 기본 단계는 다음과 같습니다.

* 소득 포인트에 대한 규칙 식별([점수 규칙](#scoring-rules)).
* 점수 규칙당 누적된 포인트에 대해, 지정 [배지](#badges) ([배지 규칙](#badging-rules)).

* [커뮤니티 사이트에 점수 및 배지 규칙 적용](#apply-rules-to-content).
* [커뮤니티 기능에 대한 배지 활성화](#enable-badges-for-component).

자세한 내용은 [빠른 테스트](#quick-test) 포럼 및 댓글에 대한 기본 점수 및 배지 규칙을 사용하여 커뮤니티 사이트에 대한 점수 책정 활성화 섹션을 참조하십시오.

### 컨텐츠에 규칙 적용 {#apply-rules-to-content}

점수부여 및 배지를 활성화하려면 속성을 추가합니다 `scoringRules` 및 `badgingRules` 을 눌러 사이트에 대한 컨텐츠 트리의 임의의 노드에 추가합니다.

사이트가 이미 게시되어 있는 경우, 모든 규칙을 적용하고 구성 요소를 활성화한 후 사이트를 다시 게시하십시오.

배지 사용 구성 요소에 적용되는 규칙은 현재 노드 또는 해당 조상에 대한 규칙입니다.

노드가 유형인 경우 `cq:Page` (권장) 그런 다음 CRXDE|Lite를 사용하여 속성을 해당 속성에 추가합니다 `jcr:content` 노드 아래에 있어야 합니다.

| **속성** | **유형** | **설명** |
|---|---|---|
| 배지 규칙 | 문자열 | 배열 목록 [배지 규칙](#badging-rules) |
| scoringRules | 문자열 | 배열 목록 [점수 규칙](#scoring-rules) |

>[!NOTE]
>
>점수 규칙이 배지 수여에 영향을 주지 않는 것으로 나타나면 배지 규칙의 scoringRules 속성에 의해 점수 규칙이 차단되지 않았는지 확인합니다. 제목이 있는 섹션을 참조하십시오. [배지 규칙](#badging-rules).

### 구성 요소에 대한 배지 활성화 {#enable-badges-for-component}

점수부여 및 배지 규칙은 구성 요소의에서 구성 요소 구성을 편집하여 배지를 활성화한 구성 요소의 인스턴스에만 적용됩니다 [작성 모드](/help/communities/author-communities.md).

부울 속성, `allowBadges`에서는 구성 요소 인스턴스에 대한 배지 표시를 활성화/비활성화합니다. 구성 가능한 템플릿은 [구성 요소 편집 대화 상자](/help/communities/author-communities.md) 포럼, QnA 및 아래에 레이블이 지정된 확인란을 통해 구성 요소 설명 **배지 표시**.

#### 예 : 포럼 구성 요소 인스턴스에 대한 allowBadge {#example-allowbadges-for-forum-component-instance}

![enable-badge-component](assets/enable-badges-component.png)

>[!NOTE]
>
>포럼, QnA 및 댓글에 있는 HBS 코드를 사용하여 배지를 표시하도록 구성 요소를 오버레이할 수 있습니다.

## 점수 규칙 {#scoring-rules}

채점 규칙은 배지 수상을 위한 채점의 기초입니다.

매우 간단하게, 각 점수 규칙은 하나 이상의 하위 규칙 목록입니다. 배지가 활성화될 때 적용할 규칙을 식별하기 위해 커뮤니티 사이트 콘텐츠에 점수부여 규칙이 적용됩니다.

점수 규칙은 상속되지만 첨가제는 아닙니다. 예:

* page2에 점수 규칙2가 포함되어 있고 해당 상위 페이지1에 점수 규칙1이 포함되어 있는 경우.
* page2 구성 요소에 대한 작업은 rule1과 rule2를 모두 호출합니다.
* 두 규칙에 동일한 규칙에 적용 가능한 하위 규칙이 포함되어 있는 경우 `topic/verb`:

   * rule2의 하위 규칙만 점수에 영향을 줍니다.
   * 두 하위 규칙의 점수는 함께 추가되지 않습니다.

둘 이상의 점수 규칙이 있는 경우 각 규칙에 대해 점수가 별도로 유지됩니다.

점수 규칙은 유형의 노드입니다 `cq:Page` 속성을 `jcr:content` 정의하는 하위 규칙 목록을 지정하는 노드입니다.

점수는 SRP에 저장됩니다.

>[!NOTE]
>
>우수 사례: 각 점수 규칙의 이름을 고유하게 지정합니다.
>
>점수 규칙 이름은 전역적으로 고유해야 합니다. 같은 이름으로 끝나면 안 됩니다.
>
>예 *not* 다음을 수행합니다.
>
>/libs/settings/community/scoring/rules/site1/forums-scoring
>/libs/settings/community/scoring/rules/site2/forums-scoring

### 점수 하위 규칙 {#scoring-sub-rules}

점수 하위 규칙에는 커뮤니티에 참여할 값을 자세히 설명하는 속성이 포함됩니다.

각 점수 하위 규칙은 다음을 식별합니다.

* 어떤 활동을 추적하고 있습니까?
* 어떤 특정 커뮤니티 기능이 포함되어 있습니까?
* 몇 점이 수여되나요?

기본적으로 하위 규칙이 컨텐츠의 소유자를 수신 포인트로 지정하지 않는 한 조치 수행 멤버에게 점수가 부여됩니다( `forOwner`).

각 하위 규칙은 하나 이상의 점수 규칙에 포함될 수 있습니다.

하위 규칙의 이름은 일반적으로 *주제* , *개체* 및 *동사*. 예:

* member-comment-create
* 회원 가입 투표

하위 규칙은 유형의 노드입니다 `cq:Page` 속성을 `jcr:content`지정할 노드 [동사 및 주제](#topics-and-verbs) .

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
     <li>필수 여부 동사는 이벤트 작업에 해당합니다</li>
     <li>동사 속성이 하나 이상 있어야 합니다.</li>
     <li>동사는 모두 대문자로 입력해야 합니다.</li>
     <li>여러 동사 속성이 있지만 중복은 없습니다</li>
     <li>값은 이 이벤트에 적용할 점수입니다</li>
     <li>값은 양수 또는 음수일 수 있습니다</li>
     <li>릴리스에서 지원되는 동사 목록은 <a href="#topics-and-verbs">항목 및 동사</a> 섹션</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>topics</code></td>
   <td>문자열</td>
   <td>
    <ul>
     <li>선택 사항; 하위 규칙을 이벤트 항목으로 식별된 커뮤니티 구성 요소로 제한</li>
     <li>지정된 경우 : 값은 이벤트 항목의 다중 값 문자열입니다</li>
     <li>릴리스의 주제 목록은 <a href="#topics-and-verbs">항목 및 동사</a> 섹션</li>
     <li>기본값은 동사와 연관된 모든 주제에 적용됩니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>forOwner</code></td>
   <td>부울</td>
   <td>
    <ul>
     <li>선택 사항; 구성원이 소유한 컨텐츠에 대해 행동하는 경우에는 중요하지 않음</li>
     <li>true일 경우 조치 중인 컨텐츠 소유자에게 점수를 적용합니다</li>
     <li>false이면 멤버 수행 작업에 점수를 적용합니다.</li>
     <li>기본값은 false입니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>scoringType</code></td>
   <td>문자열</td>
   <td>
    <ul>
     <li>선택 사항; 점수 엔진 식별</li>
     <li>"basic"이면, 수량 기준으로 점수 엔진을 지정합니다
      <ul>
       <li>릴리스에 포함됨</li>
      </ul> </li>
     <li>"advanced"이면 품질 및 수량을 기준으로 점수 엔진을 지정합니다
      <ul>
       <li>를 사용하려면 <a href="/help/communities/advanced.md">추가 패키지</a></li>
      </ul> </li>
     <li>기본값은 "기본"입니다.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 점수 규칙 및 하위 규칙 포함 {#included-scoring-rules-and-sub-rules}

릴리스에 포함된 값은 [포럼 함수](/help/communities/functions.md#forum-function) (포럼 기능의 포럼 및 댓글 구성 요소에 대해 각각 하나씩) :

1. /libs/settings/community/scoring/rules/comments/scoring

   * subRules[] = /libs/settings/community/scoring/rules/sub-conment-create /libs/settings/community/scoring/rules/sub-rules/member-receive-voit/libs/settings/community/scoring/rules/sub-rules/member-give-voke/libs/settings/community/scoring/rules/sub-rules/member-is-advertising-consioning

1. /libs/settings/community/scoring/rules/forums/scoring

   * subRules[] = /libs/settings/community/scoring/rules/sub-rules-create /libs/settings/community/scoring/rules/sub-rules/member-receive-voit/libs/settings/community/scoring/rules/sub-rules/member-give-voke/libs/settings/community/scoring/rules/sub-rules/member-is-moderation

**메모:**

* 둘 다 `rules` 및 `sub-rules` 노드는 cq:Page 유형입니다.

* `subRules` 는 String 유형의 속성입니다.[] 규칙 `jcr:content` 노드 아래에 있어야 합니다.

* `sub-rules` 다양한 점수 규칙 간에 공유할 수 있습니다.
* `rules` 모든 사용자가 읽기 권한을 가진 저장소 위치에 있어야 합니다.

   * 규칙 이름은 위치에 관계없이 고유해야 합니다.

### 사용자 지정 점수 규칙 활성화 {#activating-custom-scoring-rules}

작성 환경에서 수행한 점수 규칙 또는 하위 규칙에 대한 변경 사항이나 추가 사항은 게시에 설치해야 합니다.

## 배지 규칙 {#badging-rules}

배지 규칙은 다음을 지정하여 점수 책정 규칙을 배지에 연결합니다.

* 점수 규칙
* 특정 배지에 표시되어야 하는 점수

배지 규칙은 유형의 노드입니다 `cq:Page` 속성을 `jcr:content` 점수 및 배지에 점수 규칙을 상관 관계가 있는 노드입니다.

배지 규칙은 필수 항목으로 구성됩니다 `thresholds` 배지에 매핑된 점수의 순서가 지정된 속성입니다. 점수에 대해서는 값을 더 높게 매겨야 한다. 예:

* `1|/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

   * 청동 배지는 1점을 얻으면 착용한다.

* `60|/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

   * 60점이 적립되면 은 배지가 주어진다.

* `80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

   * 80점이 쌓여 금 배지를 만들기도 한다.

배지 규칙은 점수가 누적되는 방식을 결정하는 점수 규칙과 쌍을 이루었습니다. 제목이 있는 섹션을 참조하십시오. [컨텐츠에 규칙 적용](#apply-rules-to-content).

다음 `scoringRules` 배지 규칙의 속성은 특정 배지 규칙과 연결할 수 있는 점수 규칙을 제한합니다.

>[!NOTE]
>
>우수 사례 : 각 AEM 사이트에 고유한 배지 이미지를 만듭니다.

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
   <td><em>(필수)</em> 'number|path' 형식의 다중 값 문자열
    <ul>
     <li>number = 점수</li>
     <li>| = 세로 줄 문자(U+007C)</li>
     <li>path = 배지 이미지 리소스의 전체 경로</li>
    </ul> 숫자가 값에서 증가하고 숫자 및 경로 사이에 빈 공백이 표시되지 않도록 문자열 순서를 지정해야 합니다.<br /> 시작 예 :<br /> <code>80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png</code></td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>문자열</td>
   <td><em>(선택 사항)</em> 점수 엔진을 "기본" 또는 "고급"으로 식별합니다. 고급 점수 엔진이 필요한 경우 다음을 참조하십시오 <a href="/help/communities/advanced.md">고급 점수 및 배지</a>. 기본값은 "기본"입니다.</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>문자열</td>
   <td>(<em>옵션</em>) 배지 규칙을 점수 규칙으로 식별된 점수 이벤트로 제한하는 다중 값 문자열입니다</td>
  </tr>
 </tbody>
</table>

### 배지 규칙 포함 {#included-badging-rules}

릴리스에 포함된 두 가지 배지 규칙은 [포럼 및 댓글 점수 규칙](#includedscoringrules).

* `/libs/settings/community/badging/rules/comments-badging`

* `/libs/settings/community/badging/rules/forums-badging`

**메모:**

* `rules` 노드는 cq:Page 유형입니다.
* `rules` 모든 사용자가 읽기 권한을 가진 저장소 위치에 있어야 합니다.

   * 규칙 이름은 위치에 관계없이 고유해야 합니다.

### 사용자 지정 배지 규칙 활성화 {#activating-custom-badging-rules}

배지 규칙 또는 작성 환경에서 수행된 이미지에 대한 모든 변경 사항 또는 추가 사항은 게시에 설치해야 합니다.

## 배지 할당 및 취소 {#assign-and-revoke-badges}

배지는 [구성원 콘솔](/help/communities/members.md#badges-tab) 프로그래밍 방식으로 cURL 명령을 사용할 수도 있습니다.

다음 cURL 명령은 배지를 할당하고 취소하는 HTTP 요청에 필요한 사항을 보여 줍니다. 기본 형식은 다음과 같습니다.

cURL -i -X POST -H *헤더* -u *서명* -F *작업* -F *배지* *member-profile-url*

*헤더* = &quot;Accept:application/json&quot; 사용자 지정 헤더에서 서버로 전달됨(필수)

*서명* = administrator-id:password 예: admin:admin

*작업* = &quot;:operation=social:assignBadge&quot; OR &quot;:operation=social:deleteBadge&quot;

*배지* = &quot;badgeContentPath=*badge-image-file*&quot;

*badge-image-file* = 저장소에서 배지 이미지 파일의 위치(예: : content/moderator.png

*member-profile-url* = 게시할 때 멤버의 프로필에 대한 종단점입니다(예: ). https://&lt;server>:&lt;port>/home/users/community/riley/profile.social.json

>[!NOTE]
>
>다음 *member-profile-url*:
>
>* 다음 경우에 작성자 인스턴스를 참조할 수 있습니다. [터널 서비스](/help/communities/users.md#tunnel-service) 이 활성화되어 있습니다.
>* 알 수 없는 임의 이름일 수 있습니다. [Security 검사 목록](/help/sites-administering/security-checklist.md#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path) 인증 가능한 ID에 대한 정보입니다.


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
>cURL을 사용하여 배지 할당 및 해제가 모든 배지 이미지에 작동하지만, 배지 대신 할당되면 배지로 표시되고 그에 따라 처리됩니다.

## 사용자 지정 구성 요소에 대한 점수 및 배지 {#scoring-and-badges-for-custom-components}

구성 요소에 대해 생성된 이벤트 항목을 동사와 연결하여 사용자 지정 구성 요소에 대해 점수 및 배지 규칙을 만들 수 있습니다.

## 항목 및 동사 {#topics-and-verbs}

구성원이 커뮤니티 기능과 상호 작용할 때 알림 및 점수 책정 등의 비동기 수신기를 트리거할 수 있는 이벤트가 전송됩니다.

구성 요소의 SocialEvent 인스턴스가 이벤트를 `actions` 그것은 `topic`. SocialEvent에는 `verb` 관련 작업을 수행한 후, 다음 항목이 있습니다 *n-1* 관계 간 `actions` 및 `verbs`.

제공된 커뮤니티 구성 요소의 경우 다음 표에서는 `verbs` 각 `topic` 사용 가능 [하위 규칙 점수 책정](#scoring-sub-rules).

>[!NOTE]
>
>새 부울 속성, `allowBadges`에서는 구성 요소 인스턴스에 대한 배지 표시를 활성화/비활성화합니다. 업데이트 시 구성할 수 있습니다 [구성 요소 편집 대화 상자](/help/communities/author-communities.md) 확인란을 통해 **배지 표시**.

**[달력 구성 요소](/help/communities/calendar.md)**
SocialEvent `topic`= com/adobe/cq/social/calendar

| **동사** | **설명** |
|---|---|
| POST | 구성원이 달력 이벤트를 만듭니다. |
| 추가 | 달력 이벤트에 대한 구성원 댓글 |
| 업데이트 | 구성원의 달력 이벤트 또는 댓글이 편집됨 |
| 삭제 | 구성원의 달력 이벤트 또는 주석이 삭제됩니다. |

**[댓글 구성 요소](/help/communities/comments.md)**
SocialEvent `topic`= com/adobe/cq/social/comment

| **동사** | **설명** |
|---|---|
| POST | 멤버가 주석 만들기 |
| 추가 | 댓글 달기 |
| 업데이트 | 구성원의 댓글이 편집되었습니다. |
| 삭제 | 구성원 주석이 삭제되었습니다. |

**[파일 라이브러리 구성 요소](/help/communities/file-library.md)**
SocialEvent `topic`= com/adobe/cq/social/fileLibrary

| **동사** | **설명** |
|---|---|
| POST | 구성원이 폴더를 만듭니다. |
| 첨부 | 구성원이 파일을 업로드합니다. |
| 업데이트 | 구성원이 폴더 또는 파일을 업데이트합니다 |
| 삭제 | 구성원이 폴더 또는 파일을 삭제합니다. |

**[포럼 구성 요소](/help/communities/forum.md)**
SocialEvent `topic`= com/adobe/cq/social/forum

| **동사** | **설명** |
|---|---|
| POST | 구성원이 포럼 주제 작성 |
| 추가 | 포럼 주제에 대한 회신 |
| 업데이트 | 구성원의 포럼 주제 또는 응답이 편집됨 |
| 삭제 | 구성원의 포럼 주제 또는 응답이 삭제됨 |

**[분개 구성 요소](/help/communities/blog-feature.md)**
SocialEvent `topic`= com/adobe/cq/social/journal

| **동사** | **설명** |
|---|---|
| POST | 구성원이 블로그 문서를 만듭니다. |
| 추가 | 블로그 문서에 대한 구성원 댓글 |
| 업데이트 | 구성원의 블로그 기사 또는 댓글이 편집됨 |
| 삭제 | 구성원의 블로그 문서 또는 댓글이 삭제됨 |

**[QnA 구성 요소](/help/communities/working-with-qna.md)**
SocialEvent `topic` = com/adobe/cq/social/qna

| **동사** | **설명** |
|---|---|
| POST | 구성원이 QnA 질문을 만듭니다. |
| 추가 | 멤버가 QnA 응답을 생성합니다. |
| 업데이트 | 구성원의 QnA 질문 또는 답변이 편집됨 |
| 선택 | 멤버 답변 선택 |
| 선택 취소 | 멤버 응답 선택 취소 |
| 삭제 | 구성원의 QnA 질문 또는 답변이 삭제됩니다. |

**[구성 요소 검토](/help/communities/reviews.md)**
SocialEvent `topic`= com/adobe/cq/social/review

| **동사** | **설명** |
|---|---|
| POST | 멤버 검토 만들기 |
| 업데이트 | 구성원 검토 편집 |
| 삭제 | 구성원 검토 삭제 |

**[등급 구성 요소](/help/communities/rating.md)**
SocialEvent `topic`= com/adobe/cq/social/tally/rating

| **동사** | **설명** |
|---|---|
| 등급 추가 | 구성원의 콘텐츠가 평가되었습니다. |
| 등급 제거 | 구성원의 콘텐츠가 다운되었습니다. |

**[투표 구성 요소](/help/communities/voting.md)**
SocialEvent `topic`= com/adobe/cq/social/tally/voting

| **동사** | **설명** |
|---|---|
| 투표 추가 | 회원의 컨텐츠가 투표되었다 |
| 투표 제거 | 회원의 컨텐츠가 부결되었다 |

**중재 사용 구성 요소**
SocialEvent `topic`= com/adobe/cq/social/moderation

| **동사** | **설명** |
|---|---|
| 거부 | 구성원의 콘텐츠가 거부됨 |
| 기가 부적절한 | 구성원의 컨텐츠에 플래그가 지정됩니다. |
| 부적절한 플래그 지정 | 구성원의 컨텐츠가 플래그가 지정되지 않았습니다. |
| 수락 | 조정자가 회원 콘텐츠를 승인함 |
| 닫기 | 구성원이 편집 및 회신에 대한 댓글 닫기 |
| 열기 | 구성원 주석 다시 열기 |

### 사용자 지정 구성 요소 이벤트 {#custom-component-events}

사용자 지정 구성 요소의 경우 SocialEvent가 인스턴스화하여 구성 요소의 이벤트를 `actions` 그것은 `topic`.

점수를 지원하려면 SocialEvent가 메서드를 재정의해야 합니다 `getVerb()` 그래서 적절한 `verb` 에 대해 반환됨 `action`. 다음 `verb` 작업에 대해 반환되는 것은 일반적으로 사용되는 것(예: `POST`) 또는 각 구성 요소의 전문( 예: `ADD RATING`). 다음 항목이 있습니다 *n-1* 관계 간 `actions` 및 `verbs`.

## 문제 해결 {#troubleshooting}

### 배지가 표시되지 않습니다. {#badges-are-not-appearing}

웹 사이트의 콘텐츠에 점수 및 배지 규칙이 적용되었지만 배지가 없는 경우 해당 구성 요소의 인스턴스에 대해 배지가 활성화되어 있는지 확인하십시오.

자세한 내용은 [구성 요소에 대한 배지 활성화](#enable-badges-for-component).

### 점수 규칙은 영향을 주지 않습니다 {#scoring-rule-has-no-effect}

웹 사이트의 콘텐츠에 점수부여 및 배지 규칙이 적용되었으며 배지가 일부 작업에 대해 수여되지만 다른 것은 아닌 경우 배지 규칙이 적용되는 점수 규칙을 제한하지 않았는지 확인하십시오.

자세한 내용은 `scoringRules` 속성 [배지 규칙](#badging-rules).

### 대/소문자 구분 입력 {#case-sensitive-typo}

대부분의 속성과 값, 특히 동사는 대/소문자를 구분합니다. 점수 하위 규칙에서 사용할 경우 동사는 모두 대문자로 사용해야 합니다.

기능이 예상대로 작동하지 않으면 데이터가 올바르게 입력되었는지 확인하십시오.

## 빠른 테스트 {#quick-test}

점수를 매기고 배지를 할 때는 [시작하기 자습서](/help/communities/getting-started.md) (참여) 사이트 :

* 작성자에 대한 CRXDE Lite에 액세스합니다.
* 기본 페이지로 이동합니다.

   * /content/sites/engage/en/jcr:content

* badgingRules 속성을 추가합니다.

   * **이름**: `badgingRules`
   * **유형**: `String`
   * 선택 **다중**
   * 선택 **추가**
   * Enter 키 `/libs/settings/community/badging/rules/forums-badging`
   * 선택 **+**
   * Enter 키 `/libs/settings/community/badging/rules/comments-badging`
   * 선택 **확인**

* scoringRules 등록 정보를 추가합니다.

   * **이름**: `scoringRules`
   * **유형**: `String`
   * 선택 **다중**
   * 선택 **추가**
   * Enter 키 `/libs/settings/community/scoring/rules/forums-scoring`
   * 선택 **+**
   * Enter 키 `/libs/settings/community/scoring/rules/comments-scoring`
   * 선택 **확인**

* 선택 **모두 저장**.

![테스트 점수 배지](assets/test-scoring-badging.png)

그런 다음 포럼 및 주석 구성 요소를 통해 배지를 표시할 수 있는지 확인합니다.

* 다시 CRXDE Lite 사용.
* 포럼 구성 요소로 이동합니다

   * `/content/sites/engage/en/forum/jcr:content/content/primary/forum`

* 필요한 경우 allowBadge 부울 속성을 추가하고 true인지 확인합니다.

   * **이름**: `allowBadges`
   * **유형**: `Boolean`
   * **값**: `true`

![test-forum-component](assets/test-forum-component.png)

다음, [다시 게시](/help/communities/sites-console.md#publishing-the-site) 커뮤니티 사이트입니다.

마지막으로

* 게시 인스턴스에서 구성 요소를 찾습니다.
* 커뮤니티 구성원으로 로그인(예: weston.mccall@dodgit.com / password).
* 새 포럼 항목을 게시합니다.
* 배지가 표시되려면 페이지를 새로 고쳐야 합니다.

   * 다른 커뮤니티 구성원으로 로그아웃하고 로그인합니다(예: aaron.mcdonald@mailinator.com/password).

* 포럼을 선택합니다.

이렇게 하면 첫 번째 포럼 배지 규칙의 첫 번째 임계값이 1로 인해 커뮤니티 멤버가 포럼 게시물에 표시되는 청동 배지를 받게 됩니다.

![bronzebadge](assets/bronzebadge.png)

## 추가 정보 {#additional-information}

자세한 내용은 [점수 책정 및 배지 핵심 사항](/help/communities/configure-scoring.md) 개발자를 위한 페이지입니다.

고급 점수 엔진에 대한 자세한 내용은 [고급 점수 및 배지](/help/communities/advanced.md).

구성 가능한 리드보드 [구성 요소](/help/communities/enabling-leaderboard.md) 및 [함수](/help/communities/functions.md#leaderboard-function) 커뮤니티 사이트에서 구성원 및 해당 점수를 간편하게 표시할 수 있습니다.
