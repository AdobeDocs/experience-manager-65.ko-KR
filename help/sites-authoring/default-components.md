---
title: 기본 구성 요소
description: Adobe Experience Manager에는 웹 사이트 작성자에게 포괄적인 기능을 제공하는 다양하고 특별한 구성 요소가 포함되어 있습니다.
uuid: 55caeec3-add7-4d05-a620-07e33901adb7
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 53c37f8c-eb75-4134-9f91-8adb0a574360
exl-id: 85463610-8461-4c1f-bfe7-72229a31ea40
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 24%

---

# 구성 요소{#components}

Adobe Experience Manager(AEM)에는 웹 사이트 작성자에게 포괄적인 기능을 제공하는 다양한 기본 구성 요소가 포함되어 있습니다. [페이지를 편집](/help/sites-authoring/editing-content.md)하고 기본 기능 영역(구성 요소 그룹이라고 함)별로 그룹화할 때 사용하면 필터링에 도움이 됩니다.

구성 요소는 다음과 같은 경우에 사용할 수 있습니다. [페이지 편집](/help/sites-authoring/editing-content.md). 필터링을 지원하기 위해 구성 요소는 기본 기능 영역(즉, 구성 요소 그룹)별로 그룹화됩니다.

>[!NOTE]
>
>이 섹션에서는 표준 AEM 설치에서 즉시 사용할 수 있는 구성 요소에 대해서만 설명합니다.
>
>사용자 인스턴스에 따라 사용자 요구 사항에 맞게 명시적으로 개발된 구성 요소를 사용자 정의했을 수 있습니다. 이들은 심지어 여기서 논의되는 구성 요소 중 일부와 동일한 이름을 가질 수 있다.

## 일반 사용 {#general-usage}

구성 요소는에서 사용할 수 있습니다. **구성 요소** 다음과 같은 경우 페이지 편집기의 측면 패널에 있는 탭 [페이지 편집](/help/sites-authoring/editing-content.md).

구성 요소를 선택하여 페이지에서 필요한 위치로 드래그할 수 있습니다. 그런 다음 다음을 사용하여 편집할 수 있습니다.

* [속성 구성](/help/sites-authoring/editing-page-properties.md)
* [콘텐츠 편집](/help/sites-authoring/editing-content.md)

* [콘텐츠 편집 - 전체 화면 모드](/help/sites-authoring/editing-content.md#edit-content-full-screen-mode)

페이지에 구성 요소를 추가하는 방법에 대한 자세한 내용은 [페이지 콘텐츠 편집](/help/sites-authoring/editing-content.md) 문서를 참조하십시오.
구성 요소는 구성 요소 그룹이라는 다양한 범주에 따라 정렬됩니다. 이러한 구성 요소 그룹의 예는 다음과 같습니다.

* **We.Retail**: 와 함께 사용하기 위해 프록시화된 핵심 구성 요소를 포함합니다. [We.Retail 참조 구현](/help/sites-developing/we-retail.md).

* **We.Retail 상거래**: 장바구니 및 제품 그리드와 같은 상거래 구성 요소를 포함합니다

* **일반**: 레이아웃 컨테이너 및 경험 조각을 포함합니다.

## 모든 구성 요소 개요 {#overview-of-all-components}

다음 [구성 요소 콘솔](/help/sites-authoring/default-components-console.md) 는 AEM 설치에서 제공하는 구성 요소 그룹 및 구성 요소에 대한 개요를 제공합니다. 개별 구성 요소 및 해당 사용법에 대한 주요 정보를 볼 수 있습니다.

## 구성 요소 - 주요 영역 {#components-major-areas}

다음 페이지는 구성 요소에 대한 몇 가지 중요한 추가 정보에 대한 링크를 제공합니다.

* [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ko) - 핵심 구성 요소는 페이지를 작성하는 데 필요한 콘텐츠 유형을 제공하는 유연하고 다양한 작성 기능을 제공합니다.

* [커뮤니티](/help/communities/author-communities.md) - 구성 요소는 포럼 및 댓글과 같은 웹 사이트에 대화형 기능을 제공합니다. 다음과 같은 경우 이러한 구성 요소 대부분이 포함됩니다. [커뮤니티 사이트](/help/communities/overview.md) 이(가) 만들어졌습니다.

* [전자 상거래](/help/commerce/cif-classic/administering/ecommerce.md) - AEM 내의 eCommerce 기능에도 다양한 구성 요소가 포함됩니다. 실제 사용은 사용 중인 상거래 엔진에 따라 달라질 수 있습니다.

### 구성 요소 구성 {#configuring-components}

작성자가 표준 설치에서 액세스할 수 있는 구성 요소 외에도 다양한 다른 구성 요소를 사용할 수 있습니다.

* 페이지가 권장되는 편집 가능한 현대적 템플릿을 기반으로 하는 경우 [템플릿을 편집](/help/sites-authoring/templates.md)하여 특정 구성 요소에 대해 이들 템플릿을 활성화/비활성화하고 매개변수를 편집할 수 있습니다.
* 페이지가 정적 템플릿을 기반으로 하는 경우 [디자인 모드](/help/sites-authoring/default-components-designmode.md#enable-disable-components) 특정 구성 요소에 대해 이러한 매개 변수를 활성화/비활성화하고 매개변수를 편집합니다.
