---
title: 컨텐츠 조각에서 참조 사용에 대해 알아봅니다
description: 컨텐츠 조각, 컨텐츠, 기타 조각 및 기타 자산(미디어)에 대한 참조를 사용하는 방법에 대해 알아봅니다. 헤드리스 CMS 작성을 위한 중첩된 조각의 필요성 및 역학을 소개합니다.
index: true
hide: false
hidefromtoc: false
source-git-commit: 9661061a98c31fbb74bd0716dbedc7abef298f44
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 4%

---

# 컨텐츠 조각에서 참조 사용에 대해 알아봅니다 {#author-headless-references}

## 지금까지 이야기 {#story-so-far}

의 시작 [AEM Headless Content Author 여정](overview.md) a [소개](introduction.md) 헤드리스용 작성과 관련된 기본 개념 및 용어를 다룹니다.

AEMaaCS를 사용한 작성 및 특히 컨텐츠 조각 작성에 대한 소개와 함께 헤드리스 CMS 작성에 대한 기본 사항을 배웠습니다.

이 문서는 이러한 단원을 기반으로 작성되므로 참조를 사용하여 AEM 헤드리스 프로젝트에 대한 자체 콘텐츠를 작성하는 방법을 이해합니다.

## 목표 {#objective}

* **Audience**: 고급
* **목표**: 헤드리스 CMS 작성에 대한 참조를 도입합니다. 어떤 종류의 참조를 사용할 수 있으며 그 목적은 무엇입니까?

   * 컨텐츠 참조
   * 자산/미디어 참조
   * 조각 참조
   * 텍스트 블록 내에서 Ad Hoc 참조

## 참조란 무엇입니까? {#what-are-references}

참조는 단순히 리소스, 다른 컨텐츠, 자산(이미지 등) 또는 기타 조각에 연결하는 메커니즘입니다. 비슷하긴 하지만 몇 가지 차이점이 있습니다.

일부 참조에는 전용 데이터 유형(예: 컨텐츠 참조 및 조각 참조)이 있지만, 다른 참조는 텍스트 블록 내의 참조로도 추가됩니다(자산 참조 및 임시 참조).

![컨텐츠 조각 - 참조](/help/journey-headless/author/assets/headless-journey-author-references-01.png)

## 컨텐츠 참조 {#content-references}

컨텐츠 참조는 다른 컨텐츠를 참조할 수 있도록 해줍니다. 이렇게 하면 컨텐츠 항목을 선택할 수 있는 브라우저가 열립니다.

## 자산/미디어 참조 {#assets-media-references}

자산(예: 이미지 또는 미디어)은 **자산 삽입** 선택 사항입니다. 이렇게 하면 자산을 선택할 수 있는 브라우저가 열립니다.

![컨텐츠 조각 - 자산 삽입](/help/journey-headless/author/assets/headless-journey-author-references-02.png)

## 조각 참조 {#fragment-references}

조각 참조는 다른 조각을 참조할 수 있도록 해줍니다. 이것이 중요한 이유는 좀 더 많은 설명이 필요합니다.

예를 들어 다음 컨텐츠 조각 모델이 정의되어 있을 수 있습니다.

* 도시
* 회사
* 개인
* 수상

매우 간단해 보이지만, 회사에는 CEO와 직원들이 모두 있습니다..그리고 이들은 모두 사람들이며, 각각 사람으로 정의되었습니다.

또한 사람은 상을 받을 수 있습니다(또는 둘 중 하나).

* 내 회사 - 회사
   * CEO - 개인
   * 직원 - 개인
      * Personal Award - Award

그리고 그것은 단지 시작자들을 위한 것입니다. 복잡성에 따라 시상식은 회사별 또는 회사가 특정 도시에 본점을 둘 수 있습니다.

이러한 상호 관계를 나타내는 것은 조각 참조 로 수행할 수 있습니다. 조각 참조는 사용자(작성자)와 헤드리스 애플리케이션에서 모두 이해할 수 있습니다.

작성자는 이러한 관계를 정의할 책임이 없습니다(컨텐츠 조각 모델을 만들 때 Content Architect에서 수행). 그러나 참조를 인식하고 편집하는 방법을 알고 있어야 합니다.

### 중첩 조각을 작성하는 방법 {#author-nested-fragment}

조각 참조를 작성하는 것은 매우 간단합니다(하지만 일반적으로 필드에 **조각 참조**). 참조를 직접 입력하거나(그럴 가능성이 높음) 폴더 아이콘을 선택하여 필요한 조각을 탐색하고 선택할 수 있는 브라우저를 열 수 있습니다.

![컨텐츠 조각 - 참조](/help/journey-headless/author/assets/headless-journey-author-references-03.png)

컨텐츠 조각 모델 컨트롤의 정의:

* 여러 참조를 추가하도록 선택할 수 있는지 여부
* 선택할 수 있는 컨텐츠 조각의 모델 유형입니다. 컨텐츠 조각 모델은 참조에 허용된 조각 모델을 정의하므로 AEM은 해당 모델을 기반으로 하는 조각만 표시합니다.

### 중첩된 조각을 탐색하는 방법 {#navigate-nested-fragment}

사용 **구조 트리** 컨텐츠 조각 편집기의 탭에서는 조각에서 참조한 조각을 탐색한 다음, 조각이 포함할 수 있는 참조를 통해 이동할 수 있습니다. 참조를 선택하면 해당 조각이 편집을 위해 열립니다.

>[!NOTE]
>
>기본 패널에서 탐색 표시를 사용하여 시작 지점으로 다시 이동할 수 있습니다.

![컨텐츠 조각 구조 트리](/help/assets/content-fragments/assets/cfm-structuretree-02.png)

## 애드혹 참조 {#adhoc-references}

임시 참조는 텍스트 블록 내에 단순 링크로 추가할 수 있습니다.

![컨텐츠 조각 - Ad Hoc 참조](/help/journey-headless/author/assets/headless-journey-author-references-04.png)

## 다음은 무엇입니까? {#whats-next}

컨텐츠 조각에서 참조 및 구조에 대해 배웠으므로 다음 단계는 다음과 같습니다 [메타데이터 및 태깅에 대해 알아보기](metadata-tagging.md). 컨텐츠 조각에 대한 메타데이터 및 태그를 정의하는 방법을 소개하고 설명합니다.

## 추가 리소스 {#additional-resources}

* [컨텐츠 조각을 사용한 작업](/help/assets/content-fragments/content-fragments.md)

   * [컨텐츠 조각 관리](/help/assets/content-fragments/content-fragments-managing.md)

      * [자산 폴더에 구성 적용](/help/assets/content-fragments/content-fragments-configuration-browser.md#apply-the-configuration-to-your-assets-folder)

      * [컨텐츠 조각 만들기](/help/assets/content-fragments/content-fragments-managing.md#creating-a-content-fragment)
   * [변형 - 컨텐츠 조각 작성](/help/assets/content-fragments/content-fragments-variations.md)

   * [컨텐츠 조각 모델](/help/assets/content-fragments/content-fragments-models.md)

      * [컨텐츠 조각 모델 - 데이터 유형](/help/assets/content-fragments/content-fragments-models.md#data-types)

      * [컨텐츠 조각 모델 - 속성](/help/assets/content-fragments/content-fragments-models.md#properties)


* 시작 안내서
   * [자산 폴더 헤드리스 빠른 시작 안내서 만들기](/help/sites-developing/headless/getting-started/create-assets-folder.md)

* [AEM Headless Content Architect 여정](/help/journey-headless/architect/overview.md)

* [AEM 헤드리스 번역 여정](/help/journey-headless/translation/overview.md)
