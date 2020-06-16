---
title: 커뮤니티 점수 및 배지
seo-title: 커뮤니티 점수 및 배지
description: AEM Communities 채점 및 배지를 사용하면 커뮤니티 구성원을 식별하고 포상할 수 있습니다
seo-description: AEM Communities 채점 및 배지를 사용하면 커뮤니티 구성원을 식별하고 포상할 수 있습니다
uuid: d73683df-a413-4b3c-869c-67568bfdfcf6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ea033bb9-cb92-4c93-855f-8c902999378c
docset: aem65
tagskeywords: scoring, badging, badges, gamification
translation-type: tm+mt
source-git-commit: df59879cfa6b0bc7eba13f679e833fabbcbe92f2
workflow-type: tm+mt
source-wordcount: '2897'
ht-degree: 2%

---


# 커뮤니티 점수 및 배지 {#communities-scoring-and-badges}

## 개요 {#overview}

AEM Communities 채점 및 배지 기능을 사용하면 커뮤니티 구성원을 식별하고 보상할 수 있습니다.

점수 및 배지의 주요 특징은 다음과 같다.

* [커뮤니티에서 구성원의 역할을 식별하는 배지](#assign-and-revoke-badges) 할당에

* [참가자의 참여를 유도하기 위해 구성원에 대한 배지의](#enable-scoring) 기본 제공(제작된 컨텐츠의 수량)
* [구성원을 전문가(콘텐츠 품질)로 식별하기 위한 고급 배지](/help/communities/advanced.md) 제공

**배지** 수여는 기본적으로 [활성화되지 않습니다](/help/communities/implementing-scoring.md#main-pars-text-237875536).

>[!CAUTION]
>
>CRXDE Lite에 표시되는 구현 구조는 UI를 사용할 수 있게 되면 변경될 수 있습니다.


## 배지 {#badges}

커뮤니티 내에서 자신의 역할이나 신분을 나타내기 위해 회원 이름 아래에 배지를 부착합니다. 배지는 이미지 또는 이름으로 표시될 수 있습니다. 이미지로 표시되면 액세스 가능성을 위한 대체 텍스트로 이름이 포함됩니다.

기본적으로 배지는

* `/libs/settings/community/badging/images`

다른 위치에 저장된 경우 누구나 읽을 수 있습니다.

배지는 UGC에서 규칙에 따라 배지가 할당되었는지 또는 획득되었는지 구별됩니다. 현재, 지정된 배지는 텍스트로 표시되고 획득 배지는 이미지로 표시됩니다.

### 배지 관리 UI {#badge-management-ui}

커뮤니티 [배지 콘솔은](/help/communities/badges.md) 획득(수상)시 또는 커뮤니티(지정)에서 특정 역할을 수행할 때 회원에게 표시될 수 있는 사용자 지정 배지를 추가하는 기능을 제공합니다.

### 지정된 배지 {#assigned-badges}

역할 기반 배지는 커뮤니티 내에서 자신의 역할에 따라 관리자가 커뮤니티 구성원에게 할당됩니다.

할당(및 고정) 배지는 선택한 SRP에 저장되며 [직접](/help/communities/srp.md) 액세스할 수 없습니다. GUI를 사용할 수 있을 때까지 역할 기반 배지를 할당하는 유일한 방법은 코드 또는 cURL을 사용하여 지정하는 것입니다. cURL 지침은 배지 할당 및 [폐지 섹션을 참조하십시오](#assign-and-revoke-badges).

이번 릴리스에는 세 가지 역할 기반 배지가 포함되어 있습니다.

* **중재자**
   `/libs/settings/community/badging/images/moderator/jcr:content/moderator.png`

* **그룹 관리자**
   `/libs/settings/community/badging/images/group-manager/jcr:content/group-manager.png`

* **권한 있는 멤버**
   `/libs/settings/community/badging/images/privileged-member/jcr:content/privileged-member.png`

![chlimage_1-98](assets/chlimage_1-98.png)

### 수상 배지 {#awarded-badges}

보상 기반 배지는 커뮤니티 활동에서 적용되는 규칙에 따라 커뮤니티 회원에게 점수 부여 서비스에 의해 수여됩니다.

배지가 활동에 대한 보상으로 나타나려면 두 가지가 이루어져야 합니다.

* 기능 구성 요소에 대해 배지가 [활성화되어](#enableforcomponent) 있어야 합니다.
* 점수 지정 및 배지 규칙은 구성 요소가 배치된 페이지(또는 상위 페이지)에 [적용되어야](#applytopage) 합니다.

이번 릴리스에는 세 개의 보상 기반 배지가 포함되어 있습니다.

* **금**
   `/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

* **은**
   `/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

* **청동**
   `/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

![chlimage_1-99](assets/chlimage_1-99.png)

>[!NOTE]
>
>점수 지정 규칙은 부적절한 게시물에 대해 부정 점수를 할당하도록 구성되므로 점수 값에 영향을 줄 수 있습니다. 그러나 배지가 획득되면 점수 지정 포인트 감소 또는 점수 지정 규칙이 변경되어 배지가 자동으로 제거되지 않습니다.
>
>배지는 지정된 배지와 동일한 방식으로 취소될 수 있습니다. 배지 [지정 및 폐지 섹션을](#assign-and-revoke-badges) 참조하십시오. UI가 개선되어 멤버의 배지를 관리할 수 있게 됩니다.


### 사용자 지정 배지 {#custom-badges}

사용자 지정 배지는 [배지 콘솔을](/help/communities/badges.md) 사용하여 설치하고 배지 규칙에 할당하거나 지정할 수 있습니다.

Badges 콘솔에서 설치하면 사용자 지정 배지가 게시 환경에 자동으로 복제됩니다.

## 점수 지정 사용 {#enable-scoring}

기본적으로 점수 지정이 활성화되지 않습니다. 배지의 점수 지정 및 수여를 설정하고 활성화하는 기본적인 단계는 다음과 같습니다.

* 학습 포인트에 대한 규칙([점수 규칙](#scoring-rules))을 식별합니다.
* 점수 규칙당 누적된 포인트의 경우 [배지](#badges) ([배지 규칙](#badging-rules))를 할당합니다.

* [채점 및 배지 규칙을 커뮤니티 사이트에 적용합니다](#apply-rules-to-content).
* [커뮤니티 기능 배지 활성화](#enable-badges-for-component).

포럼 및 댓글에 대한 기본 점수 및 배지 규칙을 사용하여 커뮤니티 사이트에 대한 점수 지정을 활성화하려면 [빠른 테스트](#quick-test) 섹션을 참조하십시오.

### 컨텐츠에 규칙 적용 {#apply-rules-to-content}

점수 지정 및 배지 `scoringRules` 를 활성화하려면 사이트의 컨텐츠 트리 `badgingRules` 에 있는 모든 노드에 속성 및 속성을 추가합니다.

사이트가 이미 게시된 경우 모든 규칙을 적용하고 구성 요소를 활성화한 후 사이트를 다시 게시합니다.

배지 사용 구성 요소에 적용되는 규칙은 현재 노드 또는 해당 조상에 대한 규칙입니다.

노드가 유형 `cq:Page` (권장)인 경우 CRXDE|Lite를 사용하여 해당 `jcr:content` 노드에 속성을 추가합니다.

| **속성** | **유형** | **설명** |
|---|---|---|
| 배지 규칙 | String[] | 배지 규칙 [배열 목록](#badging-rules) |
| 점수 지정 규칙 | String[] | 점수 [규칙 배열 목록](#scoring-rules) |

>[!NOTE]
>
>점수 지정 규칙이 배지 수여에 영향을 주지 않는 것으로 나타나면 배지 규칙의 scoringRules 속성으로 점수 지정 규칙이 차단되지 않았는지 확인합니다. 배지 규칙 [이라는 섹션을 참조하십시오](#badging-rules).


### 구성 요소에 대한 배지 활성화 {#enable-badges-for-component}

점수 지정 및 배지 규칙은 [작성 모드에서 구성 요소 구성을 편집하여 배지 지정을 활성화한 구성 요소의 인스턴스에만 적용됩니다](/help/communities/author-communities.md).

구성 요소 인스턴스 `allowBadges`에 대한 배지 표시를 활성화/비활성화하는 부울 속성입니다. 포럼, QnA 및 주석 구성 요소에 대한 [구성 요소 편집 대화](/help/communities/author-communities.md) 상자에서 디스플레이 배지 **라는 확인란을 통해 구성 요소를 구성할 수 있습니다**.

#### 예: 포럼 구성 요소 인스턴스에 대한 allowBadges {#example-allowbadges-for-forum-component-instance}

![chlimage_1-100](assets/chlimage_1-100.png)

>[!NOTE]
>
>포럼, QnA 및 댓글에 있는 HBS 코드를 사용하여 배지 표시를 위해 구성 요소를 오버레이할 수 있습니다.


## 점수 지정 규칙 {#scoring-rules}

채점 규칙은 배지 수상을 위한 채점 과정이다.

매우 간단하게 각 점수 규칙은 하나 이상의 하위 규칙의 목록입니다. 배지가 활성화되면 적용할 규칙을 식별하기 위해 점수 지정 규칙이 커뮤니티 사이트 컨텐츠에 적용됩니다.

점수 규칙은 상속되지만 첨가하지는 않습니다. 예:

* page2에 점수 지정 규칙2가 포함되어 있고 상위 page1에 점수 지정 규칙1이 포함되어 있는 경우.
* page2 구성 요소의 작업은 rule1과 rule2를 모두 호출합니다.
* 두 규칙 모두에 동일한 규칙에 대한 적용 가능한 하위 규칙이 포함되어 있는 경우 `topic/verb`:

   * rule2의 하위 규칙만 점수에 영향을 줍니다.
   * 두 하위 규칙의 점수가 함께 추가되지 않습니다.

둘 이상의 점수 규칙이 있는 경우 각 규칙에 대해 점수가 별도로 유지됩니다.

점수 지정 규칙은 해당 노드 `cq:Page` 에 속성이 있는 유형 `jcr:content` 의 노드로서 이를 정의하는 하위 규칙 목록을 지정합니다.

점수는 SRP에 저장됩니다.

>[!NOTE]
>
>모범 사례: 각 점수 규칙에 이름을 고유하게 지정합니다.
>
>점수 규칙 이름은 전체적으로 고유해야 합니다. 같은 이름으로 끝나서는 안 됩니다.
>
>하지 *않을* 작업의 예:
>/libs/settings/community/scoring/rules/site1/forums-scoring
>/libs/settings/community/scoring/rules/site2/forums-scoring


### 점수 하위 규칙 {#scoring-sub-rules}

점수 지정 하위 규칙에는 커뮤니티에 참여할 값을 자세히 설명하는 속성이 포함됩니다.

각 점수 하위 규칙은 다음을 식별합니다.

* 어떤 활동을 추적하고 있습니까?
* 어떤 특정 커뮤니티 기능이 관련되어 있습니까?
* 몇 점이 수여됩니까?

하위 규칙이 컨텐츠 소유자를 포인트()를 수신함에 따라 지정하지 않는 한 기본적으로 포인트는 조치 수행 멤버에게 부여됩니다. `forOwner`

각 하위 규칙은 하나 이상의 점수 규칙에 포함될 수 있습니다.

하위 규칙의 이름은 일반적으로 *subject* , *object* 및 *동사*&#x200B;를 사용하는 패턴을 따릅니다. 예:

* member-comment-create
* 회원 승인

하위 규칙은 동사 및 항목을 지정하는 해당 `cq:Page` 노드 `jcr:content`에 속성이 있는 유형 [](#topics-and-verbs) 노드입니다.

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
     <li>필수; 동사는 이벤트 동작에 해당합니다</li>
     <li>동사 속성이 하나 이상 있어야 합니다.</li>
     <li>동사는 모두 대문자로 입력해야 합니다.</li>
     <li>여러 동사 속성이 있지만 중복되지 않습니다.</li>
     <li>값은 이 이벤트에 적용할 점수입니다.</li>
     <li>값은 양수 또는 음수일 수 있습니다.</li>
     <li>릴리스에서 지원되는 동사 목록은 <a href="#topics-and-verbs">항목 및 동사 섹션에 있습니다</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>topics</code></td>
   <td>String[]</td>
   <td>
    <ul>
     <li>선택 사항; 이벤트 항목별로 식별된 커뮤니티 구성 요소에 대한 하위 규칙을 제한합니다.</li>
     <li>specified : 값이 이벤트 항목의 다중 값 문자열입니다.</li>
     <li>릴리스의 주제 목록은 항목 및 <a href="#topics-and-verbs">동사 섹션에 있습니다</a></li>
     <li>기본값은 동사와 연관된 모든 주제에 적용됩니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>forOwner</code></td>
   <td>부울</td>
   <td>
    <ul>
     <li>선택 사항; 멤버가 소유한 컨텐츠를 사용하는 경우 관련 없음</li>
     <li>true인 경우 작업 중인 컨텐츠 소유자에게 점수를 적용합니다.</li>
     <li>false이면 멤버 작업 시 점수를 적용합니다.</li>
     <li>default is false</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>scoringType</code></td>
   <td>문자열</td>
   <td>
    <ul>
     <li>선택 사항; 점수 지정 엔진 식별</li>
     <li>"basic"인 경우 수량을 기준으로 점수 지정 엔진을 지정합니다.
      <ul>
       <li>릴리스에 포함됨</li>
      </ul> </li>
     <li>"advanced"인 경우, 품질 및 수량을 기준으로 점수 지정 엔진을 지정합니다.
      <ul>
       <li>추가 패키지 <a href="/help/communities/advanced.md">필요</a></li>
      </ul> </li>
     <li>default is "basic"</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 포함 점수 규칙 및 하위 규칙 {#included-scoring-rules-and-sub-rules}

이번 릴리스에는 [포럼 기능에 대한 두 개의 채점 규칙](/help/communities/functions.md#forum-function) (포럼 기능의 포럼 및 주석 구성 요소에 대해 각각 하나씩)이 포함되어 있습니다.

1. /libs/settings/community/scoring/rules/comments-scoring

   * subRules[] =/libs/settings/community/scoring/rules/sub-comment/settings/community/scoring/rules/sub-scoring/rules/sub-advertising/libs/settings/community/scoring/rules/members-give-vocal/libs/community/scoring/rules/sub-is-advertissed-advertising-advertising-adminising-settings

1. /libs/settings/community/scoring/rules/forums-scoring

   * subRules[] =/libs/settings/community/scoring/rules/sub-forum-create/libs/settings/community/scoring/rules/sub-scoring/rules/sub-review/settings/community/scoring/rules/members-give-voke/libs/community/scoring/rules/sub-is-advertising-advertising-ading-advertisized-adminisized-ading-advertising-settings

**메모:**

* 노드 `rules` 와 `sub-rules` 는 모두 cq:Page 형식입니다.

* `subRules` 은 규칙의 노드에서 문자열[] 유형의 `jcr:content` 속성입니다.

* `sub-rules` 다양한 점수 규칙 간에 공유될 수 있습니다.
* `rules` 는 모든 사람이 읽을 수 있는 권한이 있는 저장소 위치에 있어야 합니다.

   * 규칙 이름은 위치에 관계없이 고유해야 합니다.

### 사용자 지정 점수 규칙 활성화 {#activating-custom-scoring-rules}

작성 환경에서 수행한 점수 지정 규칙 또는 하위 규칙의 변경 사항 또는 추가 사항은 게시에 설치해야 합니다.

## 배지 규칙 {#badging-rules}

배지 규칙은 다음을 지정하여 점수 지정 규칙을 배지에 연결합니다.

* 점수 지정 규칙.
* 특정 배지를 표시하기 위해 필요한 점수입니다.

배지 규칙은 점수 및 배지 `cq:Page` 와 점수 규칙을 상관시키는 해당 `jcr:content` 노드의 속성이 있는 유형 노드입니다.

배지 규칙은 배지에 매핑된 등급 목록이 정렬된 필수 `thresholds` 속성으로 구성됩니다. 점수는 높은 값으로 순서가 정해져야 한다. 예:

* `1|/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

   * 1점을 획득하기 위해서 청동 배지가 준비되었습니다.

* `60|/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

   * 60점이 적립되면 은빛 배지를 수여한다.

* `80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

   * 80점이 적립됐을 때 금배지를 단 사람도 나왔다.

배지 규칙은 포인트가 누적되는 방식을 결정하는 점수 지정 규칙과 일치합니다. 컨텐츠에 규칙 [적용이라는 섹션을 참조하십시오](#apply-rules-to-content).

배지 규칙의 `scoringRules` 속성은 단순히 어떤 점수 규칙이 해당 배지 규칙과 쌍을 이루어야 하는지 제한합니다.

>[!NOTE]
>
>모범 사례: 각 AEM 사이트에 고유한 배지 이미지를 만듭니다.


![chlimage_1-101](assets/chlimage_1-101.png)

<table>
 <tbody>
  <tr>
   <th>속성</th>
   <th>유형</th>
   <th>값 설명</th>
  </tr>
  <tr>
   <td>임계값</td>
   <td>String[]</td>
   <td><em>(필수)</em> 'number|path' 형식의 다중 값 문자열
    <ul>
     <li>number = 점수</li>
     <li>| = 세로 줄 문자(U+007C)</li>
     <li>path = 배지 이미지 리소스에 대한 전체 경로</li>
    </ul> 숫자가 값을 늘리고 숫자와 경로 사이에 빈 공백이 없어야 하도록 문자열을 정렬해야 합니다.<br /> 응모 예:<br /> <code>80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png</code></td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>문자열</td>
   <td><em>(선택 사항)</em> 점수 엔진을 "기본" 또는 "고급"으로 식별합니다. 고급 점수 지정 엔진을 원하는 경우 <a href="/help/communities/advanced.md">고급 점수 지정 및 배지를 참조하십시오</a>. 기본값은 "basic"입니다.</td>
  </tr>
  <tr>
   <td>점수 지정 규칙</td>
   <td>String[]</td>
   <td>(<em>선택</em>사항) 점수 지정 규칙에 의해 식별된 점수 이벤트로 배지 규칙을 제한하는 다중 값 문자열</td>
  </tr>
 </tbody>
</table>

### 배지 규칙 포함 {#included-badging-rules}

이번 릴리스에 포함된 두 가지 배지 규칙은 포럼 및 [댓글 점수 규칙에 해당됩니다](#includedscoringrules).

* /libs/settings/community/badging/rules/comments-badging

* /libs/settings/community/badging/rules/forums-badging

**메모:**

* `rules` nodes는 cq:Page 형식입니다.
* `rules` 는 모든 사람이 읽을 수 있는 권한이 있는 저장소 위치에 있어야 합니다.

   * 규칙 이름은 위치에 관계없이 고유해야 합니다.

### 사용자 지정 배지 규칙 활성화 {#activating-custom-badging-rules}

작성 환경에서 배지 규칙 또는 이미지에 대한 변경 사항 또는 추가 사항은 게시에 설치해야 합니다.

## 배지 할당 및 취소 {#assign-and-revoke-badges}

멤버 콘솔을 사용하거나 cURL 명령을 사용하여 프로그래밍 방식으로 [멤버](/help/communities/members.md#badges-tab) 배지를 할당할 수 있습니다.

다음 cURL 명령은 배지 할당 및 취소에 대한 HTTP 요청에 필요한 사항을 보여줍니다. 기본 형식은 다음과 같습니다.

cURL -i -X POST -H *header**-u* signin *-F* operation ** -F *badgeFMember-profile-url*

*header* = &quot;Accept:application/json&quot; 사용자 정의 헤더를 전달하여 서버를 통과합니다(필수).

*signing* = administrator-id:passwordfor example: 관리:관리자

*operation* = &quot;:operation=social:assignBadge&quot; OR &quot;:operation=social:deleteBadge&quot;

*badge* = &quot;badgeContentPath=*badge-image-file*&quot;

*badge-image-file* = 저장소의 배지 이미지 파일 위치입니다. 예: content/moderator.png

*member-profile-url* = 게시할 때 멤버 프로필에 대한 끝점입니다. 예: https://&lt;server>:&lt;port>/home/users/community/riley/profile.social.json

>[!NOTE]
>
>멤버 프로필 *URL*:
>
>* 터널 서비스가 활성화된 경우 [작성자 인스턴스를 참조할](/help/communities/users.md#tunnel-service) 수 있습니다.
>* 잘 알려지지 않은 임의 이름일 수 있습니다. 권한 부여 가능한 ID에 대한 [보안 체크리스트를](/help/sites-administering/security-checklist.md#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path) 참조하십시오.
>



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
>배지 할당 및 취소 배지는 배지 이미지에 대해 작동하지만 배지 대신 할당되면 지정된 배지로 표시되고 그에 따라 처리됩니다.

## 사용자 지정 구성 요소에 대한 점수 및 배지 {#scoring-and-badges-for-custom-components}

구성 요소에 대해 만든 이벤트 항목을 동사와 연결하여 사용자 지정 구성 요소에 대해 점수 지정 및 배지 규칙을 만들 수 있습니다.

## 항목 및 동사 {#topics-and-verbs}

구성원이 커뮤니티 기능과 상호 작용하면 알림 및 점수 지정과 같은 비동기 수신기를 트리거할 수 있는 이벤트가 전송됩니다.

구성 요소의 SocialEvent 인스턴스는 이벤트에 대해 발생하는 대로 이벤트 `actions` 를 기록합니다 `topic`. SocialEvent에는 동작과 `verb` 연관된 항목을 반환하는 메서드가 포함되어 있습니다. 와 *는 1* 대 `actions` 의 관계가 있다 `verbs`.

제공된 커뮤니티 구성 요소의 경우 다음 표에서는 `verbs` 점수 지정 하위 규칙에 사용할 수 `topic` 있는 각 구성 요소에 대해 [설명합니다](#scoring-sub-rules).

>[!NOTE]
>
>구성 요소 인스턴스에 대한 배지 표시 `allowBadges`를 활성화/비활성화하는 새로운 부울 속성입니다. 디스플레이 배지로 레이블이 지정된 확인란을 통해 업데이트된 [구성 요소 편집 대화](/help/communities/author-communities.md) 상자에서 구성 **가능합니다**.


**[달력 구성 요소](/help/communities/calendar.md)**SocialEvent`topic`= com/adobe/cq/social/calendar

| **동사** | **설명** |
|---|---|
| POST | 구성원이 달력 이벤트를 만듭니다. |
| 추가 | 달력 이벤트의 멤버 주석 |
| 업데이트 | 구성원의 달력 이벤트 또는 댓글이 편집됨 |
| 삭제 | 구성원의 달력 이벤트 또는 댓글이 삭제됨 |

**[댓글 구성 요소](/help/communities/comments.md)**SocialEvent`topic`= com/adobe/cq/social/comment

| **동사** | **설명** |
|---|---|
| POST | 구성원이 댓글을 만듭니다. |
| 추가 | 댓글 달기 |
| 업데이트 | 구성원 댓글이 편집됨 |
| 삭제 | 구성원 댓글이 삭제됨 |

**[파일 라이브러리 구성 요소](/help/communities/file-library.md)**SocialEvent`topic`= com/adobe/cq/social/fileLibrary

| **동사** | **설명** |
|---|---|
| POST | 구성원이 폴더를 만듭니다. |
| 첨부 | 구성원이 파일을 업로드합니다. |
| 업데이트 | 구성원이 폴더 또는 파일을 업데이트합니다. |
| 삭제 | 구성원이 폴더 또는 파일을 삭제합니다. |

**[포럼 구성 요소](/help/communities/forum.md)**SocialEvent`topic`= com/adobe/cq/social/forum

| **동사** | **설명** |
|---|---|
| POST | 포럼 주제 작성 |
| 추가 | 포럼 주제에 대한 댓글 달기 |
| 업데이트 | 회원의 포럼 주제 또는 답변이 편집됨 |
| 삭제 | 회원의 포럼 주제 또는 답글이 삭제됨 |

**[저널 구성 요소](/help/communities/blog-feature.md)**SocialEvent`topic`= com/adobe/cq/social/journal

| **동사** | **설명** |
|---|---|
| POST | 구성원이 블로그 아티클을 만듭니다. |
| 추가 | 블로그 아티클에 대한 구성원 의견 |
| 업데이트 | 구성원의 블로그 기사 또는 댓글이 편집됨 |
| 삭제 | 멤버의 블로그 아티클 또는 댓글이 삭제됨 |

**[QnA 구성 요소](/help/communities/working-with-qna.md)**SocialEvent`topic`= com/adobe/cq/social/qna

| **동사** | **설명** |
|---|---|
| POST | 구성원이 QnA 질문을 만듭니다. |
| 추가 | 구성원이 QnA 응답을 만듭니다. |
| 업데이트 | 구성원의 QnA 질문이나 답변이 편집됨 |
| 선택 | 구성원 답변 선택 |
| 선택 취소 | 구성원 답변 선택 취소 |
| 삭제 | 구성원의 QnA 질문 또는 답변이 삭제되었습니다. |

**[검토 구성 요소](/help/communities/reviews.md)**SocialEvent`topic`= com/adobe/cq/social/review

| **동사** | **설명** |
|---|---|
| POST | 구성원 검토 생성 |
| 업데이트 | 구성원 검토 편집 |
| 삭제 | 구성원 검토 삭제 |

**[등급 구성 요소](/help/communities/rating.md)**SocialEvent`topic`= com/adobe/cq/social/tally/rating

| **동사** | **설명** |
|---|---|
| 등급 추가 | 회원의 컨텐츠가 등급 상승되었습니다. |
| 등급 제거 | 회원의 컨텐츠가 평점을 받지 못했습니다. |

**[투표 구성 요소](/help/communities/voting.md)**SocialEvent`topic`= com/adobe/cq/social/tally/voting

| **동사** | **설명** |
|---|---|
| 투표 추가 | 회원의 컨텐츠가 투표되었다 |
| 투표 제거 | 회원의 컨텐츠가 부결되었다 |

**중재 사용 구성 요소** SocialEvent `topic`= com/adobe/cq/social/moderation

| **동사** | **설명** |
|---|---|
| 거부 | 구성원 컨텐트가 거부됨 |
| 기가 부적절한 | 구성원의 컨텐츠가 플래그 지정됨 |
| 부적절한 플래그 해제 | 구성원 컨텐츠의 플래그가 지정되지 않음 |
| 수락 | 조정자가 회원에게 콘텐트를 승인함 |
| 닫기 | 구성원, 편집 및 답글에 댓글 닫기 |
| OPEN | 구성원 주석 다시 열기 |

### 사용자 지정 구성 요소 이벤트 {#custom-component-events}

사용자 지정 구성 요소의 경우, SocialEvent가 인스턴스화되고 구성 요소의 이벤트 `actions` `topic`가

점수를 지원하려면 SocialEvent가 메서드를 재정의하여 각 `getVerb()` 에 대해 적절한 값 `verb` 을 반환해야 합니다 `action`. 작업에 대해 `verb` 반환되는 값은 일반적으로 사용되는 작업(예: `POST`) 또는 구성 요소에 대한 전문 작업(예: `ADD RATING`) 중 하나일 수 있습니다. 와 *는 1* 대 `actions` 의 관계가 있다 `verbs`.

## 문제 해결 {#troubleshooting}

### 배지가 표시되지 않습니다. {#badges-are-not-appearing}

점수 지정 및 배지 규칙이 웹 사이트의 컨텐츠에 적용되었지만 배지가 어떤 활동에도 인식되지 않는 경우 해당 구성 요소의 인스턴스에 대해 배지가 활성화되었는지 확인하십시오.

구성 [요소에 대한 배지 활성화를 참조하십시오](#enable-badges-for-component).

### 점수 지정 규칙은 영향을 주지 않습니다. {#scoring-rule-has-no-effect}

점수 지정 및 배지 규칙이 웹 사이트의 컨텐츠에 적용되었으며 배지가 일부 작업에 대해 부여되지만 다른 작업은 부여되지 않는 경우 배지 규칙이 적용되는 점수 규칙을 제한하지 않았는지 확인하십시오.

배지 규칙 `scoringRules` 의 [속성을 참조하십시오](#badging-rules).

### 대/소문자 구분 오타 {#case-sensitive-typo}

대부분의 속성과 값, 특히 동사는 대/소문자를 구분합니다. 점수 하위 규칙에 사용할 때는 동사가 모두 대문자로 표시되어야 합니다.

기능이 예상대로 작동하지 않으면 데이터가 올바르게 입력되었는지 확인하십시오.

## 빠른 테스트 {#quick-test}

시작하기 자습서(참여) 사이트를 사용하여 점수 [와 배지](/help/communities/getting-started.md) 작업을 신속하게 시도할 수 있습니다.

* 작성자의 CRXDE Lite에 액세스
* 기본 페이지로 이동합니다.

   * /content/sites/engage/en/jcr:content

* badgingRules 속성을 추가합니다.

   * **이름**: `badgingRules`
   * **유형**: `String`
   * 다중 **선택**
   * 추가 **선택**
   * Enter `/libs/settings/community/badging/rules/forums-badging`
   * 선택 **+**
   * Enter `/libs/settings/community/badging/rules/comments-badging`
   * 확인 **선택**

* scoringRules 속성을 추가합니다.

   * **이름**: `scoringRules`
   * **유형**: `String`
   * 다중 **선택**
   * 추가 **선택**
   * Enter `/libs/settings/community/scoring/rules/forums-scoring`
   * 선택 **+**
   * Enter `/libs/settings/community/scoring/rules/comments-scoring`
   * 확인 **선택**

* 모두 **저장을 선택합니다**.

![chlimage_1-102](assets/chlimage_1-102.png)

그런 다음 포럼 및 주석 구성 요소를 통해 배지가 표시되는지 확인합니다.

* 다시 CRXDE Lite를 사용합니다.
* 포럼 구성 요소 찾아보기

   * `/content/sites/engage/en/forum/jcr:content/content/primary/forum`

* 필요한 경우 allowBadges 부울 속성을 추가하고 true인지 확인합니다.

   * **이름**: `allowBadges`
   * **유형**: `Boolean`
   * **값**: `true`

![chlimage_1-103](assets/chlimage_1-103.png)

그런 다음 [커뮤니티 사이트를 다시](/help/communities/sites-console.md#publishing-the-site) 게시합니다.

마지막으로

* 게시 인스턴스의 구성 요소를 찾습니다.
* 커뮤니티 구성원으로 로그인(예: weston.mccall@dodgit.com / password).
* 새 포럼 주제를 게시합니다.
* 배지가 표시되도록 페이지를 새로 고쳐야 합니다.

   * 로그아웃 및 다른 커뮤니티 구성원으로 로그인(예: aaron.mcdonald@mailinator.com/password).

* 포럼을 선택합니다.

첫 번째 포럼 배지 규칙의 첫 번째 임계값이 1점이므로 포럼 게시물과 함께 보이는 브론즈 배지가 커뮤니티 회원에게 주어져야 합니다.

![기관지](assets/bronzebadge.png)

## 추가 정보 {#additional-information}

개발자를 위한 [점수 지정 및 배지 필수](/help/communities/configure-scoring.md) 사항 페이지에서 자세한 내용을 확인할 수 있습니다.

고급 점수 지정 엔진에 대한 자세한 내용은 [고급 점수 및 배지를 참조하십시오](/help/communities/advanced.md).

구성 가능한 Leaderboard [구성 요소](/help/communities/enabling-leaderboard.md) 및 [기능을](/help/communities/functions.md#leaderboard-function) 사용하면 커뮤니티 사이트에서 멤버 및 스코어의 표시를 간소화할 수 있습니다.
