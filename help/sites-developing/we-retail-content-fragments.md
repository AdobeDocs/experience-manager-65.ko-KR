---
title: We.Retail에서 컨텐츠 조각 시험 사용
description: We.Retail을 사용하여 Adobe Experience Manager에서 컨텐츠 조각을 사용해 보는 방법을 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 1e5d8184-7164-4984-b43e-421015e8bf52
solution: Experience Manager, Experience Manager Sites
feature: Content Fragments,Developing
role: Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 17%

---

# We.Retail에서 컨텐츠 조각 시험 사용{#trying-out-content-fragments-in-we-retail}

변형(채널별로 가능)과 함께 콘텐츠 조각을 사용하여 채널 중립적인 콘텐츠를 만들 수 있습니다. **We.Retail**(Adobe Experience Manager의 기본 인스턴스에서 사용 가능)은 Lofoten에서 **북극 서핑** 조각을 기본 샘플로 제공합니다. 이는 다음을 보여 줍니다.

* Adobe Experience Manager(AEM) 콘텐츠 조각은 [페이지에 영향을 받지 않는 자산으로 만들고 관리됩니다](/help/assets/content-fragments/content-fragments.md). 변형(채널별로 가능)과 함께 이 조각을 사용하여 채널 중립적인 콘텐츠를 만들 수 있습니다.

   * [We.Retail에서 컨텐츠 조각 자산을 찾을 위치](#where-to-find-content-fragments-in-we-retail)를 참조하십시오.

* 그런 다음 콘텐츠 페이지를 작성할 때 [이러한 조각과 해당 변형을 사용](/help/sites-authoring/content-fragments.md)할 수 있습니다.

   * [We.Retail에서 콘텐츠 조각을 사용하는 위치](#where-content-fragments-are-used-in-we-retail)를 참조하십시오.

콘텐츠 조각 생성, 관리, 사용 및 개발에 대한 전체 설명서:

* [추가 정보](#further-information)를 참조하세요.

>[!NOTE]
>
>**콘텐츠 조각** 및 **[경험 조각](/help/sites-authoring/experience-fragments.md)**&#x200B;은 AEM 내의 다양한 기능입니다.
>
>* **콘텐츠 조각**&#x200B;은(는) 편집 가능한 콘텐츠이며, 주로 텍스트이고 관련 이미지입니다. 또한 디자인과 레이아웃이 없는 순수 콘텐츠입니다.
>* **경험 조각**&#x200B;은 전체적으로 배치된 컨텐츠, 즉 웹 페이지 조각입니다.
>
>경험 조각은 콘텐츠 조각 형태로 콘텐츠를 포함할 수 있지만 반대로는 불가능합니다.

## We.Retail에서 컨텐츠 조각을 찾을 수 있는 위치 {#where-to-find-content-fragments-in-we-retail}

We.Retail에는 몇 가지 샘플 콘텐츠 조각이 있습니다. **Assets**, **파일**, **We.Retail**, **영어**, **경험**&#x200B;을 통해 탐색하십시오.

여기에는 관련 시각적 자산과 함께 조각인 **Arctic Surfing in Lofoten**&#x200B;이(가) 포함됩니다.

* **Assets**, **파일**, **We.Retail**, **영어**, **경험**, **Rofoten에서 북극 서핑** 탐색:

   * [http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten](http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten)

![cf-44](assets/cf-44.png)

**Arctic Surfing in Lofoten** 조각을 선택하고 편집할 수 있습니다.

* [http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten](http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten)

탭(왼쪽 패널)을 사용하여 조각을 [편집 및 관리](/help/assets/content-fragments/content-fragments.md)할 수 있습니다.

<!--![cf-45-aa](do-not-localize/cf-45-aa.png) ![cf-45-a](do-not-localize/cf-45-a.png) ASSET does not exist-->

* [Markdown](/help/assets/content-fragments/content-fragments-markdown.md)을 포함하는 **[변형](/help/assets/content-fragments/content-fragments-variations.md)**
* **[관련 컨텐츠](/help/assets/content-fragments/content-fragments-assoc-content.md)**
* **[메타데이터](/help/assets/content-fragments/content-fragments-metadata.md)**

![cf-46](assets/cf-46.png)

## We.Retail에서 컨텐츠 조각을 사용하는 경우 {#where-content-fragments-are-used-in-we-retail}

[컨텐츠 조각으로 페이지 작성](/help/sites-authoring/content-fragments.md)을 설명하기 위해 아래에 다음과 같은 몇 가지 예제 페이지가 제공됩니다.

* [http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience](http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience)

예를 들어 사이트 페이지에서 **Rofoten**&#x200B;의 북극 서핑 콘텐츠 조각을 참조합니다.

* **사이트**, **We.Retail**, **언어 마스터**, **영어**, **경험**&#x200B;을 통해 탐색합니다. **Arctic Surfing in Lofoten**&#x200B;을(를) 열어 편집하세요.

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
