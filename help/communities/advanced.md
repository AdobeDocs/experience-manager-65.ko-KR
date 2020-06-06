---
title: 고급 점수 및 배지
seo-title: 고급 점수 및 배지
description: 고급 점수 설정
seo-description: 고급 점수 설정
uuid: 48caca57-43d3-4f2f-adf3-257428ba54d5
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: eb3d5c37-8097-46de-8c4f-804ea723f1c5
docset: aem65
translation-type: tm+mt
source-git-commit: fb7d2a3cebda86fa4d91d2ea89ae459fa4b86fa0
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 1%

---


# 고급 점수 및 배지{#advanced-scoring-and-badges}

## 개요 {#overview}

고급 점수 책정기로 구성원을 전문가로 식별할 수 있습니다. 고급 채점에서는 회원이 만든 컨텐츠의 수량 *및* 품질을 기반으로 포인트를 할당하는 반면, 기본 채점에서는 생성된 컨텐츠의 양을 기반으로 포인트를 할당합니다.

이 차이는 점수를 계산하는 데 사용된 점수 엔진 때문입니다. 기본 점수 엔진은 간단한 수학을 적용합니다. 고급 채점 엔진은 주제의 자연어 처리(NLP)를 통해 추론된 결과물로 가치가 높은 관련 컨텐츠에 기여하는 활성 멤버에게 보상하는 적응형 알고리즘입니다.

점수 알고리즘은 컨텐츠 연관성 외에도 투표 및 대답 비율과 같은 멤버 활동을 고려합니다. 기본 점수에는 양적인 기준이 포함되지만 고급 점수에서는 알고리즘에 의해 사용됩니다.

따라서, 고급 점수 엔진은 분석의 의미가 있는 데이터를 필요로 한다. 전문가가 되기 위한 성취 임계값은 알고리즘이 계속해서 생성된 컨텐츠의 양과 품질을 조정하므로 지속적으로 재평가됩니다. 회원의 이전 *지위를* 박탈하는 개념도 있다. 전문가 멤버가 전문가 자격을 얻은 관련 항목에 더 이상 참여하지 않을 경우 사전 결정된 일부 지점( [점수 지정 엔진 구성](#configurable-scoring-engine)참조)에 따라 전문가로서의 지위를 잃게 됩니다.

고급 점수 설정은 기본 점수 설정과 거의 동일합니다.

* 기본 및 고급 점수 지정 및 배지 규칙은 동일한 방식으로 컨텐츠에 [적용됩니다](/help/communities/implementing-scoring.md#apply-rules-to-content)

   * 동일한 컨텐츠에 기본 및 고급 점수 및 배지 규칙을 적용할 수 있습니다.

* [구성 요소에 대한 배지](/help/communities/implementing-scoring.md#enable-badges-for-component) 활성화

점수 지정 및 배지 규칙 설정의 차이점은 다음과 같습니다.

* 구성 가능한 고급 채점 엔진
* 고급 점수 지정 규칙:

   * `scoringType` 설정 `advanced`
   * requires `stopwords`

* 고급 배지 규칙:

   * `badgingType` 설정 `advanced`
   * `badgingLevels` 상을 받을 전문가 수준 **수로 설정**
   * 임계값에 대한 `badgingPaths` 배열 매핑 포인트가 아닌 배지 배열 필요

>[!NOTE]
>
>고급 점수 지정 및 배지 기능을 사용하려면 [전문가 식별 패키지를 설치합니다](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/social/cq-social-expert-identification-pkg).

## 구성 가능한 점수 엔진 {#configurable-scoring-engine}

고급 점수 엔진은 고급 점수 알고리즘에 영향을 주는 매개 변수를 사용하여 OSGi 구성을 제공합니다.

![chlimage_1-139](assets/chlimage_1-139.png)

* **점수 가중치**

   항목의 경우 점수를 계산할 때 가장 높은 우선 순위를 지정해야 하는 동사를 지정합니다. 하나 이상의 항목을 입력할 수 있지만 항목당 **하나의 동사로 제한됩니다**. 항목 [및 동사를 참조하십시오](/help/communities/implementing-scoring.md#topics-and-verbs).
쉼표 `topic,verb` 이스케이프된 상태로 입력됨 예:
   `/social/forum/hbs/social/forum\,ADD`
기본값은 QnA 및 포럼 구성 요소의 ADD 동사로 설정됩니다.

* **점수 범위**

   고급 점수의 범위는 이 값(가능한 최대 점수)과 0(가능한 최저 점수)으로 정의됩니다.

   기본값은 100이므로 점수 범위는 0-100입니다.

* **엔티티 붕괴 시간 간격**

   이 매개 변수는 모든 엔티티 점수가 감소하는 시간(시간)을 나타냅니다. 이는 더 이상 커뮤니티 사이트의 점수에 이전 컨텐츠를 포함하지 않아야 합니다.

   기본값은 216,000시간(24년)입니다.

* **점수 성장률**&#x200B;이것은 성장 속도가 느려져서 전문가 수를 제한하기 위해 0과 점수 범위 사이의 점수를 지정합니다.

   기본값은 50입니다.

## 고급 점수 지정 규칙 {#advanced-scoring-rules}

기초채점에선 배지 달기 양에 필요한 양을 알 수 있다.

고급 채점에서는 시스템 내 품질 데이터의 양에 따라 필요한 수량이 지속적으로 조정되고 있습니다. 점수 계산은 벨 커브와 유사한 방식으로 계속 계산됩니다.

더 이상 활성 상태가 아닌 주제에 대해 전문가 배지를 획득한 경우 시간이 지남에 따라 부패로 인해 배지를 잃을 가능성이 있습니다.

### scoringType {#scoringtype}

점수 지정 규칙은 점수 지정 하위 규칙 세트입니다. 각 규칙이 이 규칙을 선언합니다 `scoringType`.

고급 점수 지정 엔진을 호출하려면 이 엔진을 `scoringType`로 설정해야 합니다 `advanced`.

점수 [하위 규칙을 참조하십시오](/help/communities/implementing-scoring.md#scoring-sub-rules).

![chlimage_1-140](assets/chlimage_1-140.png)

### 중지 단어 {#stopwords}

고급 점수 패키지는 중지 단어 파일이 포함된 구성 폴더를 설치합니다.

* `/libs/settings/community/scoring/configuration/stopwords`

고급 점수 알고리즘은 stopwords 파일에 포함된 단어 목록을 사용하여 컨텐츠 처리 중에 무시되는 일반적인 영어 단어를 식별합니다.

이 파일을 수정할 가능성은 없습니다.

stopwords 파일이 없으면 고급 점수 지정 엔진에서 오류가 발생합니다.

## 고급 배지 규칙 {#advanced-badging-rules}

고급 배지 규칙 속성은 [기본 배지 규칙 속성과 다릅니다](/help/communities/implementing-scoring.md#badging-rules).

배지 이미지에 포인트를 연결하는 대신 허용된 전문가 수와 배지 이미지를 식별하기만 하면 됩니다.

![chlimage_1-141](assets/chlimage_1-141.png)

<table>
 <tbody>
  <tr>
   <th>속성</th>
   <th>유형</th>
   <th>값 설명</th>
  </tr>
  <tr>
   <td>배지 패스</td>
   <td>String[]</td>
   <td><em>(필수)</em> 배지 이미지의 다중 값 문자열을 배지 수준 수로 지정합니다. 배지 이미지 경로는 먼저 최고 전문가에게 부여되도록 순서가 정해져야 합니다. 배지(badgingLevels)에 지정된 배지 수보다 적은 배지가 있으면 배열의 나머지 배지가 채워집니다. 응모 예:<br /> <code>/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png</code></td>
  </tr>
  <tr>
   <td>badgingLevels</td>
   <td>긴</td>
   <td><em>(선택 사항)</em> 수여할 전문성 수준을 지정합니다. 예를 들어, an <code>expert </code>과 <code>almost expert</code> (두 개의 배지)이 있어야 하는 경우 값을 2로 설정해야 합니다. badgingLevel은 badgingPath 속성에 나열된 전문가 관련 배지 이미지 수와 일치해야 합니다. 기본값은 1입니다.</td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>문자열</td>
   <td><em>(필수)</em> 점수 엔진을 "기본" 또는 "고급"으로 식별합니다. "advanced"로 설정하면 기본값은 "basic"입니다.</td>
  </tr>
  <tr>
   <td>점수 지정 규칙</td>
   <td>String[]</td>
   <td><em>(선택 사항)</em> 나열된 점수 규칙에 의해 식별된 점수 이벤트로 배지 규칙을 제한하는 다중 값 문자열.<br /> 응모 예:<br /> <code>/libs/settings/community/scoring/rules/adv-comments-scoring</code><br /> 기본값은 제한이 없습니다.</td>
  </tr>
 </tbody>
</table>

## 포함된 규칙 및 배지 {#included-rules-and-badge}

### 포함된 배지 {#included-badge}

이 베타 릴리스에 포함된 제품 중 한 개의 보상 기반 전문가 배지:

* `expert`

   `/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png`

![chlimage_1-142](assets/chlimage_1-142.png)

활동에 대한 보상으로 전문가 배지가 나타나려면 다음을 확인하십시오.

* `Badges` 포럼 또는 QnA 구성 요소와 같은 기능에 대해 활성화됩니다.

* 고급 점수 지정 및 배지 규칙은 구성 요소가 배치된 페이지(또는 상위)에 적용됩니다

다음에 대한 기본 정보를 참조하십시오.

* [구성 요소에 대한 배지 활성화](/help/communities/implementing-scoring.md#enableforcomponent)
* [규칙 적용](/help/communities/implementing-scoring.md#applytopage)

### 포함 점수 규칙 및 하위 규칙 {#included-scoring-rules-and-sub-rules}

베타 릴리스에 포함된 두 가지 [포럼 기능](/help/communities/functions.md#forum-function) (포럼 기능의 포럼 및 주석 구성 요소에 대해 하나씩)에 대한 고급 채점 규칙은 다음과 같습니다.

1. `/libs/settings/community/scoring/rules/adv-comments-scoring`

   * `subRules[] =
/libs/settings/community/scoring/rules/sub-rules/adv-comments-rule
/libs/settings/community/scoring/rules/sub-rules/adv-voting-rule-owner
/libs/settings/community/scoring/rules/sub-rules/adv-voting-rule`

1. `/libs/settings/community/scoring/rules/adv-forums-scoring`

   * `subRules[] =
/libs/settings/community/scoring/rules/sub-rules/adv-forums-rule
/libs/settings/community/scoring/rules/sub-rules/adv-comments-rule
/libs/settings/community/scoring/rules/sub-rules/adv-voting-rule-owner`

**메모:**

* 노드 `rules`와 `sub-rules` 노드가 모두 `cq:Page`

* `subRules`은 규칙의 노드에서 문자열[] 유형의 특성입니다 `jcr:content`

* `sub-rules` 다양한 채점 규칙 간에 공유될 수 있습니다.

* `rules`저장소 위치에 모든 사용자에 대한 읽기 권한이 있어야 합니다.

   * 규칙 이름은 위치에 관계없이 고유해야 합니다.

### 배지 규칙 포함 {#included-badging-rules}

이번 릴리스에는 [고급 포럼 및 댓글 점수 규칙에 해당하는 두 가지 고급 배지 규칙이 포함되어 있습니다](#included-scoring-rules-and-sub-rules).

* `/libs/settings/community/badging/rules/adv-comments-badging`
* `/libs/settings/community/badging/rules/adv-forums-badging`

**메모:**

* `rules` nodes are of type cq:Page
* `rules` 저장소 위치에 모든 사용자에 대한 읽기 권한이 있어야 합니다.

   * 규칙 이름은 위치에 관계없이 고유해야 합니다.

