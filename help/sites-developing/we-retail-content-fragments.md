---
title: We.Retail에서 컨텐츠 조각 시도
seo-title: We.Retail에서 컨텐츠 조각 시도
description: 'null'
seo-description: 'null'
uuid: 66daddfe-8e98-47b6-8499-db055887ac17
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: d1326737-f378-46d0-9916-61ead4d31639
translation-type: tm+mt
source-git-commit: 759d2dd8d12861757bf7f54b77d8d3ca170887fe
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 21%

---


# We.Retail에서 컨텐츠 조각 시도{#trying-out-content-fragments-in-we-retail}

컨텐츠 조각을 사용하면 (채널별) 변형과 함께 채널 중립 컨텐츠를 만들 수 있습니다. **We.Retail** (AEM의 기본 인스턴스에서 사용 가능)은 Lofoten에서 **북극의 조각** Surfing을 기본 샘플로 제공합니다. 이를 통해 다음과 같은 현상이 나타납니다.

* AEM(Adobe Experience Manager) 컨텐츠 조각은 [페이지와 독립된 자산으로 작성 및 관리](/help/assets/content-fragments/content-fragments.md)됩니다. 변형(채널별로 가능)과 함께 이 조각을 사용하여 채널 중립적인 컨텐츠를 만들 수 있습니다.

   * We. [Retail에서 컨텐츠 조각 자산을 찾는 위치 참조](#where-to-find-content-fragments-in-we-retail)

* You can then [use these fragments, and their variations, when authoring](/help/sites-authoring/content-fragments.md) your content pages.

   * We. [Retail에서 컨텐츠 조각 사용 위치 보기](#where-content-fragments-are-used-in-we-retail)

컨텐츠 조각 만들기, 관리, 사용 및 개발에 대한 전체 문서는 다음과 같습니다.

* 자세한 [정보 보기](#further-information)

>[!NOTE]
>
>**컨텐츠 조각** 및 **[경험 조각](/help/sites-authoring/experience-fragments.md)**은 AEM 내의 다양한 기능입니다.
>
>* **컨텐츠 조각**&#x200B;은 편집 가능한 컨텐츠이며, 주로 텍스트나 관련 이미지입니다. 또한 디자인과 레이아웃이 없는 순수 컨텐츠입니다.
>* **경험 조각**&#x200B;은 전체적으로 배치된 컨텐츠, 즉 웹 페이지 조각입니다.
>
>
경험 조각은 컨텐츠 조각 형태로 컨텐츠를 포함할 수 있지만 반대로는 불가능합니다.

## We.Retail에서 컨텐츠 조각을 찾는 위치 {#where-to-find-content-fragments-in-we-retail}

We.Retail에는 몇 가지 샘플 컨텐츠 조각이 있습니다. 자산, **We.** Retail **파일**, ************ English,Experiences를 통해 이동합니다.

여기에는 관련 시각적 자산이 함께 **있는 조각, 로포텐의**&#x200B;북극 서핑이 포함됩니다.

* 자산, 파일 **,** we.Retail **을 통해**&#x200B;탐색하고, **English, ExperiencesExperiences, LightroomAtric Surfing을 통해 탐색합니다**************.

   * [http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten](http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten)

![cf-44](assets/cf-44.png)

Lofoten 조각에서 **북극 서핑을 선택하고 편집할 수** 있습니다.

* [http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten](http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten)

여기서 탭(왼쪽 패널)을 사용하여 조각을 [편집하고 관리할](/help/assets/content-fragments/content-fragments.md) 수 있습니다.

<!--![](do-not-localize/cf-45-aa.png) ![](do-not-localize/cf-45-a.png) ASSET does not exist-->

* **[마크다운을](/help/assets/content-fragments/content-fragments-variations.md)**포함한[변형](/help/assets/content-fragments/content-fragments-markdown.md)
* **[관련 컨텐츠](/help/assets/content-fragments/content-fragments-assoc-content.md)**
* **[메타데이터](/help/assets/content-fragments/content-fragments-metadata.md)**

![cf-46](assets/cf-46.png)

## We.Retail에서 컨텐츠 조각을 사용하는 위치 {#where-content-fragments-are-used-in-we-retail}

컨텐츠 조각으로 [페이지 작성을 설명하기](/help/sites-authoring/content-fragments.md) 위해 아래 몇 가지 예제 페이지가 제공됩니다. 예:

* [http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience](http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience)

예를 들어, Lofoten **의** 북극 검색 컨텐츠 조각은 사이트 페이지에서 참조됩니다.

* 사이트, **We.**.Retail **,** Language Masters **, EnglishBlacknowledgeExperience를 통해**********&#x200B;탐색합니다. Lofoten에서 **북극의 서핑은** 편집한 다음

   * [http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html](http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html)

![cf-53](assets/cf-53.png)

## 추가 정보 {#further-information}

자세한 내용은 다음을 참조하십시오.

* [콘텐츠 조각을 사용한 작업](/help/assets/content-fragments/content-fragments.md)

   * 컨텐츠 조각 자산을 생성, 편집 및 관리하는 방법을 알아봅니다.

* [컨텐츠 조각으로 페이지 작성](/help/sites-authoring/content-fragments.md)

   * 페이지를 작성할 때 컨텐츠 조각을 사용합니다.

* [AEM 개발 - 컨텐츠 조각용 구성 요소](/help/sites-developing/components-content-fragments.md)

   * 컨텐츠 조각에 대한 구성 요소 개요입니다.

* [컨텐츠 조각 개발 및 확장](/help/sites-developing/customizing-content-fragments.md)

   * 컨텐츠 조각을 개발하고 확장하는 데 도움이 되는 정보입니다.

