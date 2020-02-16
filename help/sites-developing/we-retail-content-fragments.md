---
title: We.Retail에서 콘텐츠 조각 다운로드
seo-title: We.Retail에서 콘텐츠 조각 다운로드
description: 'null'
seo-description: 'null'
uuid: 66daddfe-8e98-47b6-8499-db055887ac17
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: d1326737-f378-46d0-9916-61ead4d31639
translation-type: tm+mt
source-git-commit: dca52c05c413fc96bf7fab012a3be52f6769c2e0

---


# We.Retail에서 콘텐츠 조각 다운로드{#trying-out-content-fragments-in-we-retail}

컨텐츠 조각을 사용하면 (채널별) 변형과 함께 채널 중립 컨텐츠를 만들 수 있습니다. **We.Retail** (AEM의 특별 인스턴스에서 사용 가능)은 Lofoten에서 **기본 샘플로 북극의** 조각 Surfing을 제공합니다. 이는 다음을 보여 줍니다.

* AEM(Adobe Experience Manager) 컨텐츠 조각은 [페이지와 독립된 자산으로 작성 및 관리](/help/assets/content-fragments.md)됩니다. 변형(채널별로 가능)과 함께 이 조각을 사용하여 채널 중립적인 컨텐츠를 만들 수 있습니다.

   * We. [Retail에서 컨텐츠 조각 자산을 찾을 위치 참조](#where-to-find-content-fragments-in-we-retail)

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

## We.Retail에서 컨텐츠 조각을 찾을 위치 {#where-to-find-content-fragments-in-we-retail}

We.Retail에는 몇 가지 샘플 컨텐츠 조각이 있습니다.자산, **We.Retail**&#x200B;파일 **,** English **, CompanionExperiences**********&#x200B;를 통해 이동합니다.

이러한 기능에는 **관련된 시각적**&#x200B;자산과 함께 조각을 더한 Lofoten의 Arctic Surfing이 포함됩니다.

* 자산, **파일**, **we.Retail**, English **, Experiences**************, Loften Atertic Surfing을 통해 탐색합니다.

   * [http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten](http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten)

![cf-44](assets/cf-44.png)

Lofoten 조각에서 북극 **서핑을 선택하고 편집할 수 있습니다** .

* [http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten](http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten)

여기서 탭(왼쪽 패널)을 사용하여 조각을 [편집하고 관리할](/help/assets/content-fragments.md) 수 있습니다.

<!--![](do-not-localize/cf-45-aa.png) ![](do-not-localize/cf-45-a.png) ASSET does not exist-->

* **[마크다운](/help/assets/content-fragments-variations.md)**등[변형](/help/assets/content-fragments-markdown.md)
* **[관련 컨텐츠](/help/assets/content-fragments-assoc-content.md)**
* **[메타데이터](/help/assets/content-fragments-metadata.md)**

![cf-46](assets/cf-46.png)

## We.Retail에서 컨텐츠 조각을 사용하는 위치 {#where-content-fragments-are-used-in-we-retail}

컨텐츠 조각을 [사용하여](/help/sites-authoring/content-fragments.md) 페이지 작성을 설명하기 위해 다음과 같은 몇 가지 예제 페이지가 제공됩니다.

* [http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience](http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience)

예를 들어 Lofoten **의 북극** 서핑 컨텐츠 조각은 사이트 페이지에서 참조됩니다.

* 사이트, **We.Retail**, **Language Masters**, English **English**, ******** Cancelled Experience를 통해 탐색합니다. Lofoten **에서 북극의 서핑을 열어** 편집한 다음

   * [http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html](http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html)

![cf-53](assets/cf-53.png)

## 추가 정보 {#further-information}

자세한 내용은 다음을 참조하십시오.

* [컨텐츠 조각 작업](/help/assets/content-fragments.md)

   * 컨텐츠 조각 자산을 만들고 편집하고 관리하는 방법을 알아봅니다.

* [컨텐츠 조각으로 페이지 작성](/help/sites-authoring/content-fragments.md)

   * 페이지를 작성할 때 컨텐츠 조각을 사용합니다.

* [AEM 개발 - 컨텐츠 조각용 구성 요소](/help/sites-developing/components-content-fragments.md)

   * 컨텐츠 조각에 대한 구성 요소에 대한 개요입니다.

* [컨텐츠 조각 개발 및 확장](/help/sites-developing/customizing-content-fragments.md)

   * 컨텐츠 조각을 개발하고 확장하는 데 도움이 되는 정보입니다.

