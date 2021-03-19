---
title: We.Retail에서 컨텐츠 조각 시험 사용
seo-title: We.Retail에서 컨텐츠 조각 시험 사용
description: We.Retail에서 컨텐츠 조각 시험 사용
seo-description: 'null'
uuid: 66daddfe-8e98-47b6-8499-db055887ac17
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: d1326737-f378-46d0-9916-61ead4d31639
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 27%

---


# We.Retail에서 컨텐츠 조각 시험 사용{#trying-out-content-fragments-in-we-retail}

컨텐츠 조각을 사용하면 채널 중립적인 컨텐츠(채널별 다를 수 있음)를 변형하여 만들 수 있습니다. **We.Retail** (AEM의 기본 인스턴스에서 사용 가능)은 Lofotenas에서  **단편** 북극 서핑을 기본 샘플로제공합니다. 이를 통해 다음과 같은 이점이 있습니다.

* AEM(Adobe Experience Manager) 컨텐츠 조각은 [페이지와 독립된 자산으로 작성 및 관리](/help/assets/content-fragments/content-fragments.md)됩니다. 변형(채널별로 가능)과 함께 이 조각을 사용하여 채널 중립적인 컨텐츠를 만들 수 있습니다.

   * We.Retail에서 [컨텐츠 조각 자산을 찾을 위치](#where-to-find-content-fragments-in-we-retail) 참조

* 그런 다음 [컨텐츠 페이지를 작성할 때 이러한 조각과 해당 변형을 사용할 수 있습니다.](/help/sites-authoring/content-fragments.md)

   * [We.Retail에서 컨텐츠 조각을 사용하는 위치](#where-content-fragments-are-used-in-we-retail) 참조

컨텐츠 조각 만들기, 관리, 사용 및 개발에 대한 전체 문서를 보려면 다음을 수행하십시오.

* [추가 정보](#further-information) 참조

>[!NOTE]
>
>**컨텐츠 조각** 및 **[경험 조각](/help/sites-authoring/experience-fragments.md)**&#x200B;은 AEM 내의 다양한 기능입니다.
>
>* **컨텐츠 조각**&#x200B;은 편집 가능한 컨텐츠이며, 주로 텍스트나 관련 이미지입니다. 또한 디자인과 레이아웃이 없는 순수 컨텐츠입니다.
>* **경험 조각**&#x200B;은 전체적으로 배치된 컨텐츠, 즉 웹 페이지 조각입니다.

>
>
경험 조각은 컨텐츠 조각 형태로 컨텐츠를 포함할 수 있지만 반대로는 불가능합니다.

## We.Retail {#where-to-find-content-fragments-in-we-retail}에서 컨텐츠 조각을 찾는 위치

We.Retail에는 몇 가지 샘플 컨텐츠 조각이 있습니다.**자산**, **파일**, **We.Retail**, **영어**, **경험**&#x200B;을 통해 탐색합니다.

여기에는 **Lofoten의 북극 서핑**&#x200B;이 포함되며, 조각은 관련 시각적 자산과 함께 사용됩니다.

* **자산**, **파일**, **We.Retail**, **영어**, **경험**, **Artic Surfing in Loging**:

   * [http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten](http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten)

![cf-44](assets/cf-44.png)

Lofoten **조각에서**&#x200B;북극 서핑을 선택하고 편집할 수 있습니다.

* [http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten](http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten)

여기에서 탭(왼쪽 패널)을 사용하여 [조각](/help/assets/content-fragments/content-fragments.md)을 편집하고 관리할 수 있습니다.

<!--![](do-not-localize/cf-45-aa.png) ![](do-not-localize/cf-45-a.png) ASSET does not exist-->

* **[마크다운](/help/assets/content-fragments/content-fragments-variations.md)** 포함  [변수](/help/assets/content-fragments/content-fragments-markdown.md)
* **[관련 컨텐츠](/help/assets/content-fragments/content-fragments-assoc-content.md)**
* **[메타데이터](/help/assets/content-fragments/content-fragments-metadata.md)**

![cf-46](assets/cf-46.png)

## We.Retail {#where-content-fragments-are-used-in-we-retail}에서 컨텐츠 조각을 사용하는 위치

컨텐트 조각](/help/sites-authoring/content-fragments.md)을 사용하여 [페이지 작성을 설명하기 위해 다음과 같이 몇 가지 예제 페이지가 제공됩니다.

* [http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience](http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience)

예를 들어 Lofoten **컨텐트 조각의**&#x200B;북극 검색이 사이트 페이지에서 참조됩니다.

* **사이트**, **We.Retail**, **언어 마스터**, **영어**, **경험**&#x200B;을 통해 탐색합니다. 그런 다음 편집을 위해 **Lofoten**&#x200B;의 북극권 서핑을 엽니다.

   * [http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html](http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html)

![cf-53](assets/cf-53.png)

## 추가 정보 {#further-information}

자세한 내용은 다음을 참조하십시오.

* [콘텐츠 조각을 사용한 작업](/help/assets/content-fragments/content-fragments.md)

   * 컨텐츠 조각 자산을 생성, 편집 및 관리하는 방법을 알아봅니다.

* [컨텐츠 조각으로 페이지 작성](/help/sites-authoring/content-fragments.md)

   * 페이지를 작성할 때 컨텐츠 조각을 사용합니다.

* [AEM 개발 - 컨텐츠 조각용 구성 요소](/help/sites-developing/components-content-fragments.md)

   * 컨텐츠 조각에 대한 구성 요소 개요.

* [컨텐츠 조각 개발 및 확장](/help/sites-developing/customizing-content-fragments.md)

   * 컨텐츠 조각을 개발하고 확장하는 데 도움이 되는 정보입니다.

