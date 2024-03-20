---
title: We.Retail에서 컨텐츠 조각 시험 사용
description: We.Retail을 사용하여 Adobe Experience Manager에서 컨텐츠 조각을 사용해 보는 방법을 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 1e5d8184-7164-4984-b43e-421015e8bf52
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 17%

---

# We.Retail에서 컨텐츠 조각 시험 사용{#trying-out-content-fragments-in-we-retail}

변형(채널별로 가능)과 함께 콘텐츠 조각을 사용하여 채널 중립적인 콘텐츠를 만들 수 있습니다. **We.Retail** (Adobe Experience Manager의 기본 인스턴스에서 사용 가능한 경우) 조각을 제공합니다 **로포텐의 북극 서핑** 를 기본 샘플로 사용하십시오. 이는 다음을 보여 줍니다.

* Adobe Experience Manager(AEM) 콘텐츠 조각은 [페이지 독립적 자산으로 생성 및 관리됨](/help/assets/content-fragments/content-fragments.md). 변형(채널별로 가능)과 함께 이 조각을 사용하여 채널 중립적인 콘텐츠를 만들 수 있습니다.

   * 다음을 참조하십시오 [We.Retail에서 컨텐츠 조각 자산을 찾을 수 있는 위치](#where-to-find-content-fragments-in-we-retail)

* 그런 다음 [작성 시 이러한 조각과 해당 변형 사용](/help/sites-authoring/content-fragments.md) 콘텐츠 페이지.

   * 다음을 참조하십시오 [We.Retail에서 컨텐츠 조각을 사용하는 경우](#where-content-fragments-are-used-in-we-retail)

콘텐츠 조각 생성, 관리, 사용 및 개발에 대한 전체 설명서:

* 다음을 참조하십시오 [추가 정보](#further-information)

>[!NOTE]
>
>**콘텐츠 조각** 및 **[경험 조각](/help/sites-authoring/experience-fragments.md)**&#x200B;은 AEM 내의 다양한 기능입니다.
>
>* **컨텐츠 조각** 는 편집 가능한 컨텐츠이며, 주로 텍스트나 관련 이미지입니다. 또한 디자인과 레이아웃이 없는 순수 콘텐츠입니다.
>* **경험 조각**&#x200B;은 전체적으로 배치된 컨텐츠, 즉 웹 페이지 조각입니다.
>
>경험 조각은 콘텐츠 조각 형태로 콘텐츠를 포함할 수 있지만 반대로는 불가능합니다.

## We.Retail에서 컨텐츠 조각을 찾을 수 있는 위치 {#where-to-find-content-fragments-in-we-retail}

We.Retail에는 몇 가지 샘플 콘텐츠 조각이 있습니다. 다음을 통해 이동 **에셋**, **파일**, **We.Retail**, **영어**, **경험**.

여기에는 다음이 포함됩니다. **로포텐의 북극 서핑**: 관련 시각적 에셋과 함께 제공되는 조각:

* 다음을 통해 탐색 **에셋**, **파일**, **We.Retail**, **영어**, **경험**, **로포텐의 북극 서핑**:

   * [http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten](http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten)

![cf-44](assets/cf-44.png)

을(를) 선택하고 편집할 수 있습니다 **로포텐의 북극 서핑** 조각:

* [http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten](http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten)

여기에서 다음을 수행할 수 있습니다 [편집 및 관리](/help/assets/content-fragments/content-fragments.md) 탭을 사용하는 조각(왼쪽 패널):

<!--![cf-45-aa](do-not-localize/cf-45-aa.png) ![cf-45-a](do-not-localize/cf-45-a.png) ASSET does not exist-->

* **[변형](/help/assets/content-fragments/content-fragments-variations.md)** 포함 [Markdown](/help/assets/content-fragments/content-fragments-markdown.md)
* **[관련 컨텐츠](/help/assets/content-fragments/content-fragments-assoc-content.md)**
* **[메타데이터](/help/assets/content-fragments/content-fragments-metadata.md)**

![cf-46](assets/cf-46.png)

## We.Retail에서 컨텐츠 조각을 사용하는 경우 {#where-content-fragments-are-used-in-we-retail}

예시 [컨텐츠 조각으로 페이지 작성](/help/sites-authoring/content-fragments.md) 아래에 제공된 몇 가지 예제 페이지가 있습니다. 예를 들면 다음과 같습니다.

* [http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience](http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience)

예를 들어 **로포텐의 북극 서핑** 사이트 페이지에서 컨텐츠 조각을 참조합니다.

* 탐색 수단 **사이트**, **We.Retail**, **언어 마스터**, **영어**, **경험**. 그런 다음 열기 **로포텐의 북극 서핑** 편집용:

   * [http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html](http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html)

![cf-53](assets/cf-53.png)

## 추가 정보 {#further-information}

자세한 내용은 다음을 참조하십시오.

* [콘텐츠 조각을 사용하여 작업](/help/assets/content-fragments/content-fragments.md)

   * 콘텐츠 조각 에셋을 만들고, 편집하고, 관리하는 방법을 알아봅니다.

* [컨텐츠 조각으로 페이지 작성](/help/sites-authoring/content-fragments.md)

   * 페이지를 작성할 때 콘텐츠 조각을 사용합니다.

* [AEM 개발 - 콘텐츠 조각용 구성 요소](/help/sites-developing/components-content-fragments.md)

   * 콘텐츠 조각용 구성 요소에 대한 개요입니다.

* [컨텐츠 조각 개발 및 확장](/help/sites-developing/customizing-content-fragments.md)

   * 콘텐츠 조각 개발 및 확장에 도움이 되는 정보입니다.
