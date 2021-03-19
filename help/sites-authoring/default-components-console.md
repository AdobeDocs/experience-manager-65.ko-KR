---
title: 구성 요소 콘솔
seo-title: 구성 요소 콘솔
description: 구성 요소 콘솔
seo-description: 'null'
uuid: a4e34d81-7875-4e26-8b48-4473e2905c37
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: b657f95d-7be3-4409-a31b-d47fb2bfa550
docset: aem65
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 100%

---


# 구성 요소 콘솔{#components-console}

구성 요소 콘솔에서 인스턴스에 대해 정의된 모든 구성 요소를 탐색하고 각 구성 요소에 대한 주요 정보를 볼 수 있습니다.

**도구 ->** **일반 ->** **구성 요소**&#x200B;에서 액세스할 수 있습니다. 콘솔에서 카드 및 목록 보기를 사용할 수 있습니다. 구성 요소에 대한 트리 구조가 없으므로 열 보기를 사용할 수 없습니다.

![screen-shot_2019-03-05at113145](assets/screen-shot_2019-03-05at113145.png)

>[!NOTE]
>
>[구성 요소 콘솔]은 시스템의 모든 구성 요소를 표시합니다. [구성 요소 브라우저](/help/sites-authoring/author-environment-tools.md#components-browser)는 작성자가 사용할 수 있는 구성 요소를 표시하며 마침표(`.`)로 시작하는 모든 구성 요소 그룹을 숨깁니다.

## 검색 {#searching}

**컨텐츠 전용** 아이콘(왼쪽 상단)을 사용하여 구성 요소를 검색 및/또는 필터링할 **검색** 패널을 열 수 있습니다.

![screen-shot_2019-03-05at113251](assets/screen-shot_2019-03-05at113251.png)

### 구성 요소 세부 사항 {#component-details}

특정 구성 요소에 대한 세부 사항을 보려면 필수 리소스를 탭하거나 클릭합니다. 세 탭에서 다음 정보를 제공합니다.

* **속성**

   ![screen_shot_2018-03-27at165847](assets/screen_shot_2018-03-27at165847.png)

   [속성] 탭에서 다음 작업을 수행할 수 있습니다.

   * 구성 요소의 일반 속성 확인
   * 구성 요소에 대해 [아이콘이나 약어를 정의한 방법](/help/sites-developing/components-basics.md#component-icon-in-touch-ui) 확인

      * 아이콘의 소스를 클릭하면 해당 구성 요소로 이동합니다.
   * 구성 요소에 대한 **리소스 유형** 및 **리소스 슈퍼 유형**(정의된 경우) 확인

      * [리소스 슈퍼 유형]을 클릭하면 해당 구성 요소로 이동합니다.
   >[!NOTE]
   >
   >`/apps`는 런타임 시 편집할 수 없으므로 구성 요소 콘솔은 읽기 전용입니다.

* **정책**

   ![chlimage_1-169](assets/chlimage_1-169.png)

* **라이브 사용량**

   ![chlimage_1-170](assets/chlimage_1-170.png)

   >[!CAUTION]
   >
   >이 보기에 대해 수집 중인 정보의 특성으로 인해 순서대로 구성하거나 표시하는 데 시간이 걸릴 수 있습니다.

* **설명서**

   개발자가 ](/help/sites-developing/developing-components.md#documenting-your-component)구성 요소에 대한 설명서[를 제공한 경우 **설명서** 탭에 표시됩니다. 사용 가능한 설명서가 없으면 **설명서** 탭이 표시되지 않습니다.

   ![chlimage_1-171](assets/chlimage_1-171.png)

