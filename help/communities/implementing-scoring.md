---
title: 커뮤니티 채점 및 배지
seo-title: 커뮤니티 채점 및 배지
description: AEM Communities 채점 및 배지를 사용하여 커뮤니티 구성원을 식별하고 포상할 수 있습니다.
seo-description: AEM Communities 채점 및 배지를 사용하여 커뮤니티 구성원을 식별하고 포상할 수 있습니다.
uuid: d73683df-a413-4b3c-869c-67568bfdfcf6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ea033bb9-cb92-4c93-855f-8c902999378c
docset: aem65
tagskeywords: scoring, badging, badges, gamification
role: 관리자
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2885'
ht-degree: 2%

---


# 커뮤니티 점수 및 배지 {#communities-scoring-and-badges}

## 개요 {#overview}

AEM Communities 점수 및 배지 기능을 사용하면 커뮤니티 구성원을 식별하고 보상할 수 있습니다.

점수 및 배지의 주요 특징은 다음과 같습니다.

* [배지](#assign-and-revoke-badges) 를 할당하여 커뮤니티 구성원의 역할을 식별합니다.

* [참가를 장려하기 위해 ](#enable-scoring) 배지 구성원에 대한 기본 제공(제작된 컨텐츠의 양).

* [고급 배지 ](/help/communities/advanced.md) 수여로 구성원을 전문가(제작된 컨텐츠의 품질)로 식별할 수 있습니다.

**배지** 수여는 기본적으로  [활성화되지 않습니다](/help/communities/implementing-scoring.md#main-pars-text-237875536).

>[!CAUTION]
>
>CRXDE Lite에 표시되는 구현 구조는 UI를 사용할 수 있게 되면 변경될 수 있습니다.

## 배지 {#badges}

커뮤니티 내에서 자신의 역할이나 신분을 나타내기 위해 회원 이름 아래에 배지가 부착됩니다. 배지는 이미지 또는 이름으로 표시될 수 있습니다. 이미지로 표시되면 액세스 가능성을 위한 대체 텍스트로 이름이 포함됩니다.

기본적으로 배지는

* `/libs/settings/community/badging/images`

다른 위치에 저장된 경우 누구나 읽을 수 있습니다.

배지는 UGC에서 규칙에 따라 배지가 할당되었는지 또는 획득되었는지 여부에 따라 구분됩니다. 현재, 지정된 배지는 텍스트로 표시되고 획득 배지는 이미지로 표시됩니다.

### 배지 관리 UI {#badge-management-ui}

커뮤니티 [배지 콘솔](/help/communities/badges.md)에서는 획득(수상) 시 또는 커뮤니티(지정)에서 특정 역할을 수행할 때 회원에게 표시할 수 있는 사용자 지정 배지를 추가할 수 있습니다.

### 지정된 배지 {#assigned-badges}

역할 기반 배지는 커뮤니티 내에서 자신의 역할에 따라 커뮤니티 구성원에게 관리자가 할당합니다.

할당(및 수신) 배지는 선택한 [SRP](/help/communities/srp.md)에 저장되며 직접 액세스할 수 없습니다. GUI를 사용할 수 있을 때까지 역할 기반 배지를 할당하는 유일한 방법은 코드나 cURL을 사용하여 지정하는 것입니다. cURL 지침은 [배지 할당 및 취소](#assign-and-revoke-badges) 섹션을 참조하십시오.

이번 릴리스에는 3개의 역할 기반 배지가 포함되어 있습니다.

* **중재자**

   `/libs/settings/community/badging/images/moderator/jcr:content/moderator.png`

* **그룹 관리자**

   `/libs/settings/community/badging/images/group-manager/jcr:content/group-manager.png`

* **권한 있는 멤버**

   `/libs/settings/community/badging/images/privileged-member/jcr:content/privileged-member.png`

   ![지정된 배지](assets/assigned-badges.png)

### 수여된 배지 {#awarded-badges}

보상 기반 배지는 커뮤니티 활동에서 적용된 규칙에 따라 커뮤니티 멤버에게 채점 서비스를 통해 부여됩니다.

배지가 활동에 대한 보상으로 나타나려면 두 가지 일이 일어나야 합니다.

* 배지는 기능 구성 요소에 대해 [enabled](#enableforcomponent)여야 합니다.
* 점수 지정 및 배지 규칙은 구성 요소가 배치된 페이지(또는 상위 항목)에 [적용됨](#applytopage)이어야 합니다.

이번 릴리스에는 세 개의 보상 기반 배지가 포함되어 있습니다.

* **금색**

   `/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

* **은**

   `/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

* **청동**

   `/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

   ![수상 배지](assets/awarded-badges.png)

>[!NOTE]
>
>점수 지정 규칙은 부적절한 게시물에 대해 부정 점수를 할당하도록 구성되므로 점수 값에 영향을 줄 수 있습니다. 그러나 배지가 획득되면 점수 지정 포인트 감소 또는 채점 규칙 변경으로 인해 배지가 자동으로 제거되지 않습니다.
>
>수여된 배지는 지정된 배지와 동일한 방식으로 취소할 수 있습니다. [배지 할당 및 취소](#assign-and-revoke-badges) 섹션을 참조하십시오. UI가 개선되어 멤버의 배지를 관리할 수 있게 됩니다.

### 사용자 지정 배지 {#custom-badges}

사용자 지정 배지는 [배지 콘솔](/help/communities/badges.md)을 사용하여 설치하고 배지 규칙에 할당되거나 지정할 수 있습니다.

Badges 콘솔에서 설치하면 사용자 지정 배지가 게시 환경에 자동으로 복제됩니다.

## 점수 지정 사용 {#enable-scoring}

채점은 기본적으로 활성화되지 않습니다. 배지의 채점 및 채점을 설정하고 활성화하는 기본적인 단계는 다음과 같습니다.

* 학습 점수를 위한 규칙을 식별합니다([채점 규칙](#scoring-rules)).
* 점수 지정 규칙당 누적된 포인트의 경우 [배지](#badges)([배지 규칙](#badging-rules))를 할당합니다.

* [채점 및 배지 규칙을 커뮤니티 사이트에 적용합니다](#apply-rules-to-content).
* [커뮤니티 기능에 대한 배지](#enable-badges-for-component) 활성화

포럼 및 댓글에 대한 기본 점수 및 배지 규칙을 사용하여 커뮤니티 사이트의 점수를 매길 수 있도록 설정하려면 [빠른 테스트](#quick-test) 섹션을 참조하십시오.

### 콘텐츠에 규칙 적용 {#apply-rules-to-content}

점수 및 배지를 활성화하려면 속성 `scoringRules` 및 `badgingRules`을 사이트의 컨텐츠 트리의 노드에 추가합니다.

사이트가 이미 게시된 경우 모든 규칙을 적용하고 구성 요소를 활성화한 후 사이트를 다시 게시하십시오.

배지 사용 구성 요소에 적용되는 규칙은 현재 노드 또는 해당 조상에 대한 규칙입니다.

노드가 `cq:Page`(권장) 유형인 경우 CRXDE|Lite를 사용하여 해당 `jcr:content` 노드에 속성을 추가합니다.

| **속성** | **유형** | **설명** |
|---|---|---|
| 배지 규칙 | 문자열 | [배지 규칙](#badging-rules)의 배열 목록 |
| scoringRules | 문자열 | [채점 규칙](#scoring-rules)의 배열 목록 |

>[!NOTE]
>
>점수 지정 규칙이 배지 수여에 영향을 주지 않는 것으로 나타나면 배지 규칙의 scoringRules 속성에 의해 점수 지정 규칙이 차단되지 않았는지 확인합니다. [배지 규칙](#badging-rules)이라는 제목의 섹션을 참조하십시오.

### 구성 요소 {#enable-badges-for-component} 배지 활성화

점수 지정 및 배딩 규칙은 [작성 모드](/help/communities/author-communities.md)에서 구성 요소 구성을 편집하여 배지를 활성화한 구성 요소의 인스턴스에만 적용됩니다.

구성 요소 인스턴스에 대한 배지 표시를 활성화/비활성화하는 부울 속성 `allowBadges` 이 구성 요소는 [구성 요소 편집 대화 상자](/help/communities/author-communities.md)에서 포럼, QnA 및 주석 구성 요소에 대해 **디스플레이 배지** 확인란을 통해 구성할 수 있습니다.

#### 예:포럼 구성 요소 인스턴스 {#example-allowbadges-for-forum-component-instance}에 대한 allowBadges

![enable-badges-component](assets/enable-badges-component.png)

>[!NOTE]
>
>포럼, QnA 및 댓글에 있는 HBS 코드를 사용하여 모든 구성 요소를 오버레이하여 배지를 표시할 수 있습니다.

## 점수 지정 규칙 {#scoring-rules}

채점 규칙은 배지 수상을 위한 채점 과정이다.

매우 간단하게 각 채점 규칙은 하나 이상의 하위 규칙의 목록입니다. 배지가 활성화되면 적용할 규칙을 식별하기 위해 채점 규칙이 커뮤니티 사이트 컨텐츠에 적용됩니다.

채점 규칙은 상속되지만 가산은 아닙니다. 예:

* page2에 채점 규칙2가 포함되어 있고 해당 상위 페이지1에 채점 규칙1이 포함된 경우.
* page2 구성 요소의 작업은 rule1과 rule2를 모두 호출합니다.
* 두 규칙 모두에 동일한 `topic/verb`에 대해 적용 가능한 하위 규칙이 포함되어 있는 경우:

   * rule2의 하위 규칙만 점수에 영향을 줍니다.
   * 두 하위 규칙의 점수가 함께 추가되지 않습니다.

둘 이상의 점수 규칙이 있는 경우 각 규칙에 대해 점수가 별도로 유지됩니다.

점수 지정 규칙은 이 규칙을 정의하는 하위 규칙 목록을 지정하는 `jcr:content` 노드의 속성이 있는 `cq:Page` 유형의 노드입니다.

점수는 SRP에 저장됩니다.

>[!NOTE]
>
>모범 사례:각 채점 규칙의 이름을 고유하게 지정합니다.
>
>점수 규칙 이름은 전역적으로 고유해야 합니다.동일한 이름으로 끝나지 않아야 합니다.
>
>*이(가) 아닌*&#x200B;의 예:
>
>/libs/settings/community/scoring/rules/site1/forums-scoring
>/libs/settings/community/scoring/rules/site2/forums-scoring

### 점수 지정 하위 규칙 {#scoring-sub-rules}

점수 지정 하위 규칙에는 커뮤니티에 참여할 값을 자세히 설명하는 속성이 포함됩니다.

각 채점 하위 규칙은 다음을 식별합니다.

* 어떤 활동을 추적하고 있습니까?
* 어떤 특정 커뮤니티 기능이 관련되어 있습니까?
* 몇 점이 수여됩니까?

하위 규칙이 컨텐츠 소유자를 포인트( `forOwner`)를 수신하도록 지정하지 않는 한 기본적으로 포인트는 조치 수행 멤버에게 부여됩니다.

각 하위 규칙이 하나 이상의 점수 지정 규칙에 포함될 수 있습니다.

하위 규칙의 이름은 일반적으로 *subject* , *object* 및 *verb*&#x200B;를 사용하는 패턴을 따릅니다. 예:

* member-comment-create
* 회원 가입

하위 규칙은 [동사 및 항목](#topics-and-verbs)을 지정하는 `jcr:content`노드에 속성이 있는 `cq:Page` 유형의 노드입니다.

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
     <li>필수;동사는 이벤트 동작에 해당합니다</li>
     <li>동사 속성이 하나 이상 있어야 합니다.</li>
     <li>동사는 모두 대문자로 입력해야 합니다.</li>
     <li>여러 동사 속성이 있지만 중복은 없습니다.</li>
     <li>값은 이 이벤트에 적용할 점수입니다.</li>
     <li>값은 양수 또는 음수일 수 있습니다.</li>
     <li>릴리스에서 지원되는 동사 목록은 <a href="#topics-and-verbs">항목 및 동사</a> 섹션에 있습니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>topics</code></td>
   <td>문자열</td>
   <td>
    <ul>
     <li>선택 사항;이벤트 항목으로 식별되는 커뮤니티 구성 요소에 대한 하위 규칙을 제한합니다.</li>
     <li>지정하는 경우 :값이 이벤트 항목의 다중 값 문자열입니다.</li>
     <li>릴리스의 주제 목록은 <a href="#topics-and-verbs">항목 및 동사</a> 섹션에 있습니다.</li>
     <li>기본값은 동사와 연관된 모든 주제에 적용됩니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>forOwner</code></td>
   <td>부울</td>
   <td>
    <ul>
     <li>선택 사항;회원이 소유한 컨텐트에 대해 행동하는 경우 관련되지 않음</li>
     <li>true인 경우 작업 중인 컨텐츠 소유자에게 점수를 적용합니다.</li>
     <li>false이면 참여 중인 멤버에 점수를 적용합니다.</li>
     <li>default is false</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>scoringType</code></td>
   <td>문자열</td>
   <td>
    <ul>
     <li>선택 사항;채점 엔진을 식별합니다.</li>
     <li>"basic"인 경우 수량을 기반으로 채점 엔진을 지정합니다.
      <ul>
       <li>릴리스에 포함</li>
      </ul> </li>
     <li>"advanced"인 경우 품질과 수량에 따라 채점 엔진을 지정합니다.
      <ul>
       <li><a href="/help/communities/advanced.md">추가 패키지</a> 필요</li>
      </ul> </li>
     <li>기본값은 "basic"입니다.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 포함 점수 규칙 및 하위 규칙 {#included-scoring-rules-and-sub-rules}

이번 릴리스에 포함된 두 개의 채점 규칙은 [포럼 함수](/help/communities/functions.md#forum-function)(포럼 기능의 포럼 및 주석 구성 요소에 대해 각각 하나씩)에 대한 것입니다.

1. /libs/settings/community/scoring/rules/comments-scoring

   * subRules[] =
/libs/settings/community/scoring/rules/sub-rules/member-comment-create
/libs/settings/community/scoring/rules/sub-rules/member-receive-vot
/libs/settings/community/scoring/rules/sub-rules/member-give-voit
/libs/settings/community/scoring/rules/sub-rules/member-is-moderated

1. /libs/settings/community/scoring/rules/forums-scoring

   * subRules[] =
/libs/settings/community/scoring/rules/sub-rules/member-forum-create
/libs/settings/community/scoring/rules/sub-rules/member-receive-vot
/libs/settings/community/scoring/rules/sub-rules/member-give-voit
/libs/settings/community/scoring/rules/sub-rules/member-is-moderated

**메모:**

* `rules` 및 `sub-rules` 노드 모두 cq:Page 유형입니다.

* `subRules` 은 규칙의 노드[] 에 있는 Stringing 유형의  `jcr:content` 특성입니다.

* `sub-rules` 다양한 채점 규칙 간에 공유될 수 있습니다.
* `rules` 저장소 위치에 있어야 하며 모든 사람이 읽기 권한을 갖습니다.

   * 규칙 이름은 위치에 관계없이 고유해야 합니다.

### 사용자 지정 점수 규칙 활성화 {#activating-custom-scoring-rules}

작성 환경에서 채점 규칙 또는 하위 규칙에 대한 모든 변경 사항 또는 추가 사항은 게시 시 설치해야 합니다.

## 배지 규칙 {#badging-rules}

배지 규칙은 다음을 지정하여 점수 지정 규칙을 배지에 연결합니다.

* 채점 규칙
* 특정 배지가 표시되어야 하는 점수

배지 규칙은 점수 지정 규칙을 점수 및 배지에 상관시키는 `jcr:content` 노드의 속성이 있는 `cq:Page` 유형의 노드입니다.

배지 규칙은 배지에 매핑되는 ordered score 목록인 필수 `thresholds` 속성으로 구성됩니다. 점수는 높은 값으로 순서가 매겨져야 한다. 예:

* `1|/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

   * 1점을 얻으면 동조 배지가 나온다.

* `60|/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

   * 60점이 누적되면 실버 배지가 수여된다.

* `80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

   * 80점이 적립됐을 때 금배지를 단 사람도 있다.

배지 규칙은 포인트가 누적되는 방식을 결정하는 채점 규칙과 일치합니다. [콘텐츠에 규칙 적용](#apply-rules-to-content) 섹션을 참조하십시오.

배지 규칙의 `scoringRules` 속성은 단순히 해당 배지 규칙과 짝이 될 수 있는 채점 규칙을 제한합니다.

>[!NOTE]
>
>모범 사례:각 AEM 사이트에 고유한 배지 이미지를 만듭니다.

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
     <li>path = 배지 이미지 리소스에 대한 전체 경로</li>
    </ul> 숫자가 값에서 증가하고 번호와 경로 사이에 빈 공간이 나타나지 않도록 문자열을 정렬해야 합니다.<br /> 시작 예:<br /> <code>80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png</code></td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>문자열</td>
   <td><em>(선택 사항)</em> 채점 엔진을 "기본" 또는 "고급"으로 식별합니다. 고급 점수 지정 엔진을 원하는 경우 <a href="/help/communities/advanced.md">고급 채점 및 배지</a>를 참조하십시오. 기본값은 "기본"입니다.</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>문자열</td>
   <td>(<em>선택 사항</em>) 배지 규칙을 점수 지정 규칙에 의해 식별된 점수부여 이벤트로 제한하는 다중 값 문자열</td>
  </tr>
 </tbody>
</table>

### 배지 규칙 포함 {#included-badging-rules}

이 릴리스에 포함된 두 가지 배지 규칙은 [포럼 및 댓글 점수 지정 규칙](#includedscoringrules)에 해당합니다.

* `/libs/settings/community/badging/rules/comments-badging`

* `/libs/settings/community/badging/rules/forums-badging`

**메모:**

* `rules` nodes는 cq:Page 유형입니다.
* `rules` 저장소 위치에 있어야 하며 모든 사람이 읽기 권한을 갖습니다.

   * 규칙 이름은 위치에 관계없이 고유해야 합니다.

### 사용자 지정 배지 규칙 활성화 {#activating-custom-badging-rules}

작성 환경에서 배지 규칙 또는 이미지에 대한 변경 사항 또는 추가 사항은 게시 시 설치해야 합니다.

## 배지 할당 및 취소 {#assign-and-revoke-badges}

배지는 [멤버 콘솔](/help/communities/members.md#badges-tab)을 사용하거나 cURL 명령을 프로그래밍 방식으로 사용하여 멤버에게 할당할 수 있습니다.

다음 cURL 명령은 배지 할당 및 취소에 대한 HTTP 요청에 필요한 사항을 보여 줍니다. 기본 형식은 다음과 같습니다.

cURL -i -X POST -H *header* -u *sigin* -F *operation* -F *badge* *member-profile-url*

*header* = &quot;accept:application/json&quot; 사용자 정의 헤더를 확장하여 서버(필수) 전달

*signing* = administrator-id:password for example:관리:관리

*operation* = &quot;:operation=social:assignBadge&quot; OR &quot;:operation=social:deleteBadge&quot;

*badge* = &quot;badgeContentPath=*badge-image-file*&quot;

*badge-image-file* = 저장소에서 배지 이미지 파일의 위치입니다. 예:content/moderator.png

*member-profile-url* = 게시 시 멤버 프로필에 대한 끝점입니다. 예:https://&lt;server>:&lt;port>/home/users/community/riley/profile.social.json

>[!NOTE]
>
>*member-profile-url*:
>
>* [터널 서비스](/help/communities/users.md#tunnel-service)가 활성화된 경우 작성자 인스턴스를 참조할 수 있습니다.
>* 알 수 없는 임의 이름일 수 있습니다. 권한 가능한 ID에 대해서는 [보안 검사 목록](/help/sites-administering/security-checklist.md#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path)을 참조하십시오.


### 예: {#examples}

#### 중재자 배지 지정 {#assign-a-moderator-badge}

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:assignBadge" -F "badgeContentPath=/libs/settings/community/badging/images/moderator/jcr:content/moderator.png" /home/users/community/updcs9DndLEI74DB9zsB/profile.social.json
```

#### 할당된 실버 배지 {#revoke-an-assigned-silver-badge} 취소

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:deleteBadge" -F "badgeContentPath=/libs/settings/community/badging/images/silver/jcr:content/silver.png" /home/users/community/updcs9DndLEI74DB9zsB/profile.social.json
```

>[!NOTE]
>
>cURL을 사용하여 배지 할당 및 해지를 사용하면 배지 이미지에 사용할 수 있지만, 배지 대신 할당되면 배지로 표시되고 그에 따라 처리됩니다.

## 사용자 지정 구성 요소 {#scoring-and-badges-for-custom-components}에 대한 점수 지정 및 배지

구성 요소에 대해 만든 이벤트 항목을 동사와 연결하여 사용자 지정 구성 요소에 대해 채점 및 배지 규칙을 만들 수 있습니다.

## 항목 및 동사 {#topics-and-verbs}

구성원이 커뮤니티 기능과 상호 작용할 때 알림 및 점수 지정과 같은 비동기 리스너를 트리거할 수 있는 이벤트가 전송됩니다.

구성 요소의 SocialEvent 인스턴스는 `topic`에 대해 발생하는 `actions`으로 이벤트를 기록합니다. SocialEvent에는 작업과 연관된 `verb`을(를) 반환하는 메서드가 포함되어 있습니다. `actions`과 `verbs` 사이에 *n-1* 관계가 있습니다.

제공된 커뮤니티 구성 요소의 경우 다음 표에서는 [점수 하위 규칙](#scoring-sub-rules)에서 사용할 수 있는 각 `topic`에 대해 정의된 `verbs`에 대해 설명합니다.

>[!NOTE]
>
>구성 요소 인스턴스에 대한 배지 표시를 활성화/비활성화합니다. `allowBadges` **디스플레이 배지**&#x200B;라는 레이블이 지정된 확인란을 통해 업데이트된 [구성 요소 편집 대화 상자](/help/communities/author-communities.md)에서 구성 가능합니다.

**[달력](/help/communities/calendar.md)**
구성 요소SocialEvent  `topic`= com/adobe/cq/social/calendar

| **동사** | **설명** |
|---|---|
| POST | 구성원이 달력 이벤트를 만듭니다. |
| 추가 | 달력 이벤트의 멤버 주석 |
| 업데이트 | 구성원 달력 이벤트 또는 댓글이 편집됨 |
| 삭제 | 구성원의 달력 이벤트 또는 댓글이 삭제됨 |

**[댓글](/help/communities/comments.md)**
구성 요소SocialEvent  `topic`= com/adobe/cq/social/comment

| **동사** | **설명** |
|---|---|
| POST | 구성원이 주석을 만듭니다. |
| 추가 | 댓글에 답글 달기 |
| 업데이트 | 회원의 댓글이 편집되었습니다. |
| 삭제 | 구성원의 댓글이 삭제됨 |

**[파일 라이브러리](/help/communities/file-library.md)**
구성 요소SocialEvent  `topic`= com/adobe/cq/social/fileLibrary

| **동사** | **설명** |
|---|---|
| POST | 구성원이 폴더를 만듭니다. |
| 첨부 | 구성원이 파일을 업로드합니다. |
| 업데이트 | 구성원이 폴더 또는 파일을 업데이트합니다. |
| 삭제 | 구성원이 폴더 또는 파일을 삭제합니다. |

**[포럼](/help/communities/forum.md)**
구성 요소SocialEvent  `topic`= com/adobe/cq/social/forum

| **동사** | **설명** |
|---|---|
| POST | 포럼 주제 작성 |
| 추가 | 포럼 주제에 대한 댓글 달기 |
| 업데이트 | 회원의 포럼 주제 또는 답변이 편집되었습니다. |
| 삭제 | 회원의 포럼 주제 또는 답변이 삭제되었습니다. |

**[저널](/help/communities/blog-feature.md)**
구성 요소 소셜 이벤트  `topic`= com/adobe/cq/social/journal

| **동사** | **설명** |
|---|---|
| POST | 구성원이 블로그 아티클을 만듭니다. |
| 추가 | 블로그 아티클에 대한 구성원 의견 |
| 업데이트 | 구성원 블로그 문서 또는 댓글이 편집됨 |
| 삭제 | 구성원의 블로그 아티클 또는 댓글이 삭제됨 |

**[QnA](/help/communities/working-with-qna.md)**
ComponentSocialEvent  `topic` = com/adobe/cq/social/qna

| **동사** | **설명** |
|---|---|
| POST | 구성원이 QnA 질문을 만듭니다. |
| 추가 | 구성원이 QnA 대답을 만듭니다. |
| 업데이트 | 회원의 질문 또는 답변이 편집됨 |
| 선택 | 구성원 답변 선택 |
| 선택 취소 | 구성원 답변 선택 취소 |
| 삭제 | 회원의 QnA 질문 또는 답변이 삭제되었습니다. |

**[검토](/help/communities/reviews.md)**
구성 요소SocialEvent  `topic`= com/adobe/cq/social/review

| **동사** | **설명** |
|---|---|
| POST | 구성원 검토 만들기 |
| 업데이트 | 구성원 검토 편집 |
| 삭제 | 구성원 검토 삭제 |

**[등급](/help/communities/rating.md)**
구성 요소SocialEvent  `topic`= com/adobe/cq/social/총계/등급

| **동사** | **설명** |
|---|---|
| 등급 추가 | 회원의 콘텐츠가 평가되었습니다. |
| 등급 제거 | 회원의 콘텐츠가 평가되었습니다. |

**[투표](/help/communities/voting.md)**
구성 요소SocialEvent  `topic`= com/adobe/cq/social/tally/voting

| **동사** | **설명** |
|---|---|
| 투표 추가 | 회원의 컨텐츠가 투표되었습니다. |
| 투표 제거 | 회원의 컨텐츠가 부결됨 |

**중재가 활성화된**
구성 요소SocialEvent  `topic`= com/adobe/cq/social/moderation

| **동사** | **설명** |
|---|---|
| 거부 | 구성원 콘텐츠가 거부되었습니다. |
| 부적절한 플래그 | 구성원의 컨텐츠가 플래그 지정됨 |
| 부적절한 플래그 해제 | 구성원 컨텐츠가 플래그 지정되지 않음 |
| 수락 | 조정자가 멤버 컨텐츠를 승인함 |
| 닫기 | 회원이 편집 및 답글에 대한 댓글을 닫습니다. |
| 열기 | 구성원 주석 다시 열기 |

### 사용자 지정 구성 요소 이벤트 {#custom-component-events}

사용자 지정 구성 요소의 경우, SocialEvent가 인스턴스화되어 구성 요소의 이벤트를 `topic`에 대해 발생하는 `actions`으로 기록합니다.

점수를 지원하려면 SocialEvent가 `getVerb()` 메서드를 재정의하여 각 `action`에 대해 적절한 `verb`이(가) 반환됩니다. 작업에 대해 반환되는 `verb`은(는) 일반적으로 사용되는 하나(예: `POST`) 또는 구성 요소에 특화된 하나(예: `ADD RATING`)일 수 있습니다. `actions`과 `verbs` 사이에 *n-1* 관계가 있습니다.

## 문제 해결 {#troubleshooting}

### 배지가 {#badges-are-not-appearing}에 나타나지 않습니다.

점수 지정 및 배지 규칙이 웹 사이트의 컨텐츠에 적용되었지만 배지가 어떤 활동에도 인식되지 않는 경우 해당 구성 요소의 인스턴스에 대해 배지가 활성화되어 있는지 확인하십시오.

[구성 요소](#enable-badges-for-component)에 대한 배지 활성화를 참조하십시오.

### 점수 지정 규칙은 {#scoring-rule-has-no-effect}에 영향을 주지 않습니다.

점수 지정 및 배지 규칙이 웹 사이트의 컨텐츠에 적용되었고 배지가 일부 작업에 대해 부여되지만 다른 작업은 부여되지 않는 경우 배지 규칙이 적용되는 점수 지정 규칙을 제한하지 않았는지 확인하십시오.

[배지 규칙](#badging-rules)의 `scoringRules` 속성을 참조하십시오.

### 대/소문자 구분 유형 {#case-sensitive-typo}

대부분의 속성 및 값, 특히 동사는 대소문자를 구분합니다. 점수 지정 하위 규칙에 사용할 때는 동사가 모두 대문자로 표시되어야 합니다.

기능이 예상대로 작동하지 않으면 데이터가 올바르게 입력되었는지 확인하십시오.

## 빠른 테스트 {#quick-test}

[시작하기 자습서](/help/communities/getting-started.md)(참여) 사이트를 사용하여 점수를 매기고 배지를 빠르게 시도할 수 있습니다.

* 작성자의 CRXDE Lite 액세스
* 기본 페이지로 이동합니다.

   * /content/sites/engage/en/jcr:content

* badgingRules 속성을 추가합니다.

   * **이름**: `badgingRules`
   * **유형**: `String`
   * **다중** 선택
   * **추가** 선택
   * `/libs/settings/community/badging/rules/forums-badging` 입력
   * 선택 **+**
   * `/libs/settings/community/badging/rules/comments-badging` 입력
   * **확인** 선택

* scoringRules 속성을 추가합니다.

   * **이름**: `scoringRules`
   * **유형**: `String`
   * **다중** 선택
   * **추가** 선택
   * `/libs/settings/community/scoring/rules/forums-scoring` 입력
   * 선택 **+**
   * `/libs/settings/community/scoring/rules/comments-scoring` 입력
   * **확인** 선택

* **모두 저장**&#x200B;을 선택합니다.

![시험 점수 배지](assets/test-scoring-badging.png)

그런 다음 포럼 및 주석 구성 요소를 통해 배지가 표시되는지 확인합니다.

* 다시 CRXDE Lite 사용.
* 포럼 구성 요소 찾아보기

   * `/content/sites/engage/en/forum/jcr:content/content/primary/forum`

* 필요한 경우 allowBadges 부울 속성을 추가하고 true인지 확인합니다.

   * **이름**: `allowBadges`
   * **유형**: `Boolean`
   * **값**:  `true`

![test-forum-component](assets/test-forum-component.png)

다음으로 커뮤니티 사이트를 [다시 게시합니다.](/help/communities/sites-console.md#publishing-the-site)

마지막으로

* 게시 인스턴스의 구성 요소를 찾습니다.
* 커뮤니티 멤버로 로그인(예:weston.mccall@dodgit.com / password).
* 새 포럼 항목을 게시합니다.
* 배지가 표시되도록 페이지를 새로 고쳐야 합니다.

   * 로그아웃 및 다른 커뮤니티 구성원으로 로그인합니다(예:aaron.mcdonald@mailinator.com/password).

* 포럼을 선택합니다.

첫 번째 포럼 배지 규칙의 첫 번째 임계값이 1점이므로 포럼 게시물이 보이는 청동 배지를 커뮤니티 회원에게 제공해야 합니다.

![기관지](assets/bronzebadge.png)

## 추가 정보 {#additional-information}

개발자를 위한 [점수 지정 및 배지 필수 항목](/help/communities/configure-scoring.md) 페이지에서 자세한 내용을 확인할 수 있습니다.

고급 점수 지정 엔진에 대한 자세한 내용은 [고급 채점 및 배지](/help/communities/advanced.md)를 참조하십시오.

구성 가능한 리더보드 [구성 요소](/help/communities/enabling-leaderboard.md) 및 [함수](/help/communities/functions.md#leaderboard-function)는 커뮤니티 사이트에서 멤버 및 해당 점수의 표시를 단순화합니다.
