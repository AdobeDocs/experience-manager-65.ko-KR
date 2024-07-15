---
title: 고급 점수 및 배지
description: 배지를 수여하여 구성원을 전문가로 식별할 수 있도록 고급 점수를 설정하는 방법을 알아봅니다.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: d3bb6664-6c01-4bcf-840c-072fc491fc99
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 0%

---

# 고급 점수 및 배지{#advanced-scoring-and-badges}

## 개요 {#overview}

고급 채점을 통해 배지를 수여하여 구성원을 전문가로 식별할 수 있습니다. 고급 점수는 구성원이 만든 콘텐츠의 품질 *과(와)*&#x200B;을(를) 기준으로 점수를 할당하는 반면 기본 점수는 만든 콘텐츠의 품질을 기준으로 점수를 할당합니다.

이러한 차이는 점수를 계산하는 데 사용되는 채점 엔진에 기인합니다. 기본 채점 엔진은 간단한 수학을 적용합니다. 고급 채점 엔진은 주제의 자연어 처리(NLP)를 통해 추론된 가치 있고 관련 있는 콘텐츠에 기여하는 활동적인 구성원에게 보상을 주는 적응형 알고리즘입니다.

채점 알고리즘은 콘텐츠 관련성 외에도 투표 및 답변 비율과 같은 멤버 활동을 처리합니다. 기본 채점이 양적으로 포함하는 반면, 고급 채점은 알고리즘적으로 활용한다.

따라서 고급 채점 엔진은 분석을 의미 있게 하기에 충분한 데이터가 필요합니다. 알고리즘이 만들어지는 콘텐츠의 양과 품질에 지속적으로 조정되기 때문에 전문가가 되기 위한 성취 임계값은 지속적으로 재평가된다. 구성원의 이전 게시물에 대한 *decay* 개념도 있습니다. 전문가 멤버가 전문가 상태를 얻은 주제에 더 이상 참여하지 않을 경우 미리 결정된 시점([채점 엔진 구성](#configurable-scoring-engine) 참조)에 전문가 상태를 잃을 수 있습니다.

고급 채점을 설정하는 것은 사실상 기본 채점과 동일합니다.

* 기본 및 고급 채점 및 배지 규칙이 동일한 방식으로 [콘텐츠에 적용됨](/help/communities/implementing-scoring.md#apply-rules-to-content).

   * 기본 및 고급 채점 및 배지 규칙이 동일한 콘텐츠에 적용될 수 있습니다.

* [구성 요소에 대한 배지를 사용](/help/communities/implementing-scoring.md#enable-badges-for-component)하는 것이 일반적입니다.

채점 및 배지 규칙 설정의 차이점은 다음과 같습니다.

* 구성 가능한 고급 채점 엔진
* 고급 채점 규칙:

   * `scoringType`이(가) `advanced`(으)로 설정됨
   * `stopwords` 필요

* 고급 배지 규칙:

   * `badgingType`이(가) `advanced`(으)로 설정됨
   * `badgingLevels`을(를) **제공할 전문가 수준 수**(으)로 설정
   * 임계값에 대한 배열 매핑 지점 대신 `badgingPaths` 배지 배열이 필요합니다.

>[!NOTE]
>
>고급 채점 및 배지 기능을 사용하려면 [전문가 식별 패키지](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq610%2Fsocial%2Ffeaturepack%2Fcq-social-expert-identification-pkg)를 설치하십시오.

## 구성 가능한 점수 엔진 {#configurable-scoring-engine}

고급 채점 엔진은 고급 채점 알고리즘에 영향을 주는 매개 변수와 함께 OSGi 구성을 제공합니다.

![고급 채점 엔진](assets/advanced-scoring-engine.png)

* **점수 가중치**

  주제의 경우 점수를 계산할 때 가장 높은 우선 순위를 부여해야 하는 동사를 지정합니다. 하나 이상의 주제를 입력할 수 있지만 **주제당 하나의 동사**&#x200B;로 제한됩니다. [주제 및 동사](/help/communities/implementing-scoring.md#topics-and-verbs)를 참조하세요.
쉼표가 이스케이프된 `topic,verb`(으)로 입력되었습니다. 예:
  `/social/forum/hbs/social/forum\,ADD`
기본값은 QnA 및 포럼 구성 요소의 ADD 동사로 설정되어 있습니다.

* **채점 범위**

  고급 점수의 범위는 이 값(최대 점수)과 0(가능한 가장 낮은 점수)으로 정의됩니다.

  기본값은 100이므로 채점 범위는 0-100입니다.

* **엔터티 감소 시간 간격**

  이 매개 변수는 모든 엔티티 점수가 감소된 시간 수를 나타냅니다. 커뮤니티 사이트에 대한 점수에 더 이상 이전 콘텐츠를 포함하지 않는 것이 필요합니다.

  기본값은 216000시간(~24년)입니다.

* **점수 증가율**
이는 0점 범위 사이의 점수를 지정하며, 이 범위를 초과하면 성장이 느려져 전문가 수가 제한됩니다.

  기본값은 50입니다.

## 고급 채점 규칙 {#advanced-scoring-rules}

기본 점수에서는 배지를 획득하는데 필요한 수량이 알려져 있다.

고급 채점에서는 필요한 수량이 시스템 내의 품질 데이터의 양에 따라 지속적으로 조정됩니다. 채점은 종 곡선과 유사한 방식으로 계속 계산됩니다.

구성원이 더 이상 활동하지 않는 주제에 대해 전문가 배지를 획득하면 시간이 지남에 따라 부패로 인해 배지를 잃을 가능성이 있다.

### scoringType {#scoringtype}

채점 규칙은 각각 `scoringType`을(를) 선언하는 채점 하위 규칙 집합입니다.

고급 채점 엔진을 호출하려면 `scoringType`을(를) `advanced`(으)로 설정해야 합니다.

[채점 하위 규칙](/help/communities/implementing-scoring.md#scoring-sub-rules)을(를) 참조하십시오.

![고급 채점 유형](assets/advanced-scoring-type.png)

### 정지어 {#stopwords}

고급 채점 패키지는 중지 단어 파일이 포함된 구성 폴더를 설치합니다.

* `/libs/settings/community/scoring/configuration/stopwords`

고급 채점 알고리즘은 stopwords 파일에 포함된 단어 목록을 사용하여 콘텐츠 처리 중에 무시되는 일반적인 영어 단어를 식별합니다.

이 파일이 수정될 것으로 예상되지 않습니다.

중지 단어 파일이 누락된 경우 고급 채점 엔진이 오류를 표시합니다.

## 고급 배지 규칙 {#advanced-badging-rules}

고급 배지 규칙 속성이 [기본 배지 규칙 속성](/help/communities/implementing-scoring.md#badging-rules)과(와) 다릅니다.

점수를 배지 이미지와 연관시키는 대신, 허용된 전문가 수와 수여할 배지 이미지를 식별하기만 하면 됩니다.

![고급 배지 규칙](assets/advanced-badging-rules.png)

<table>
 <tbody>
  <tr>
   <th>속성</th>
   <th>유형</th>
   <th>값 설명</th>
  </tr>
  <tr>
   <td>배지 경로</td>
   <td>String[]</td>
   <td><em>(필수)</em> 배지 이미지의 다중 값 문자열이 배지 수준 수에 도달했습니다. 배지 이미지 경로의 순서를 지정해야 하므로 첫 번째 경로가 가장 높은 전문가에게 수여됩니다. badgingLevels에서 표시된 것보다 배지가 적은 경우 배열의 마지막 배지가 나머지 배열을 채웁니다. 예제 항목:<br /> <code>/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png</code></td>
  </tr>
  <tr>
   <td>배지 레벨</td>
   <td>Long</td>
   <td><em>(선택 사항)</em> 수여할 전문 지식 수준을 지정합니다. 예를 들어 <code>expert </code>과(와) <code>almost expert</code>(배지 2개)이 있어야 하는 경우 값을 2로 설정해야 합니다. 배지 수준은 badgingPath 속성에 대해 나열된 전문가 관련 배지 이미지 수와 일치해야 합니다. 기본값은 1입니다.</td>
  </tr>
  <tr>
   <td>배지 유형</td>
   <td>문자열</td>
   <td><em>(필수)</em> 채점 엔진을 "기본" 또는 "고급"으로 식별합니다. "고급"으로 설정하거나 기본값이 "기본"입니다.</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>String[]</td>
   <td><em>(선택 사항)</em> 나열된 하나 이상의 채점 규칙에 의해 식별된 채점 이벤트로 배지 규칙을 제한하는 다중 값 문자열입니다.<br /> 예제 항목:<br /> <code>/libs/settings/community/scoring/rules/adv-comments-scoring</code><br /> 기본값은 제한이 없습니다.</td>
  </tr>
 </tbody>
</table>

## 포함된 규칙 및 배지 {#included-rules-and-badge}

### 포함된 배지 {#included-badge}

이 베타 릴리스에는 보상 기반 전문가 배지 1개가 포함됩니다.

* `expert`

  `/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png`

![전문가 배지](assets/included-badge.png)

전문가 배지가 활동에 대한 보상으로 표시되도록 하려면 다음을 확인하십시오.

* `Badges`이(가) 포럼 또는 QnA 구성 요소와 같은 기능에 대해 활성화되어 있습니다.

* 고급 채점 및 배지 규칙은 구성 요소가 배치된 페이지(또는 상위 항목)에 적용됩니다

다음에 대한 기본 정보를 참조하십시오.

* [구성 요소에 대한 배지 활성화](/help/communities/implementing-scoring.md#enableforcomponent)
* [규칙 적용](/help/communities/implementing-scoring.md#applytopage)

### 채점 규칙 및 하위 규칙 포함 {#included-scoring-rules-and-sub-rules}

Beta 릴리스에는 [포럼 기능](/help/communities/functions.md#forum-function)에 대한 두 가지 고급 채점 규칙(포럼 및 포럼 기능의 주석 구성 요소에 대해 각각 하나씩)이 포함되어 있습니다.

1. `/libs/settings/community/scoring/rules/adv-comments-scoring`

   ```
   subRules[] =
   /libs/settings/community/scoring/rules/sub-rules/adv-comments-rule
   /libs/settings/community/scoring/rules/sub-rules/adv-voting-rule-owner
   /libs/settings/community/scoring/rules/sub-rules/adv-voting-rule
   ```

1. `/libs/settings/community/scoring/rules/adv-forums-scoring`

   ```
   subRules[] =
   /libs/settings/community/scoring/rules/sub-rules/adv-forums-rule
   /libs/settings/community/scoring/rules/sub-rules/adv-comments-rule
   /libs/settings/community/scoring/rules/sub-rules/adv-voting-rule-owner
   ```

**메모:**

* `rules` 및 `sub-rules` 노드가 모두 `cq:Page` 유형입니다.
* `subRules`은(는) 규칙의 `jcr:content` 노드에 있는 String`[]` 형식의 특성입니다.
* `sub-rules`은(는) 다양한 채점 규칙 간에 공유될 수 있습니다.
* `rules`은(는) 모든 사용자에 대한 읽기 권한이 있는 저장소 위치에 있어야 합니다.
* 규칙 이름은 위치에 관계없이 고유해야 합니다.

### 포함된 배지 규칙 {#included-badging-rules}

릴리스에는 [고급 포럼 및 댓글 채점 규칙](#included-scoring-rules-and-sub-rules)에 해당하는 2개의 고급 배지 규칙이 포함되어 있습니다.

* `/libs/settings/community/badging/rules/adv-comments-badging`
* `/libs/settings/community/badging/rules/adv-forums-badging`

**메모:**

* `rules`개 노드가 cq:Page 유형입니다.
* `rules`은(는) 모든 사용자에 대한 읽기 권한이 있는 저장소 위치에 있어야 합니다.
* 규칙 이름은 위치에 관계없이 고유해야 합니다.
