---
title: 'AEM 6.5 Sites용 헤드리스 개발 '
description: 컨텐츠 모델, 컨텐츠 조각 및 GraphQL API와 같은 AEM 6.5의 강력한 헤드리스 기능이 함께 작동하여 경험을 중앙에서 관리하고 여러 채널에서 제공하는 방법을 살펴볼 수 있습니다.
source-git-commit: 03285545d8cc04d97513fb5fee3b3c616551ccdc
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 2%

---


# AEM 6.5 Sites용 헤드리스 개발 {#headless-development}

컨텐츠 모델, 컨텐츠 조각 및 GraphQL API와 같은 AEM 6.5의 강력한 헤드리스 기능이 함께 작동하여 경험을 중앙에서 관리하고 여러 채널에서 제공하는 방법을 살펴볼 수 있습니다.

## 개요 {#overview}

헤드리스 구현은 어디에 있든 채널에 관계없이 고객에게 경험을 전달하는 데 점점 중요해지고 있습니다.

헤드리스 구현은 전체 스택 및 하이브리드 솔루션에서 일반적으로 페이지 및 구성 요소 관리를 수행하고 채널 중립적이고 재사용 가능한 컨텐츠 조각 및 채널 간 전달을 만드는 데 중점을 둡니다. 웹 경험을 구현하기 위한 현대적이고 동적 개발 패턴입니다.

![AEM 구현 모델](assets/aem-implementation-models.png)

## 헤드리스 및 헤드리스 비교 {#headful-headless}

이 문서는 AEM의 헤드리스 전체 구현 모델에 중점을 둡니다. 하지만 headful과 headless는 AEM에서 이진 선택이 될 필요가 없습니다. 헤드리스 기능을 사용하여 콘텐츠를 관리하고 다양한 종단점으로 전달하면서 콘텐츠 작성자가 단일 페이지 애플리케이션을 편집할 수도 있습니다. 모두 AEM에서

<!-- HM-Links
>[!TIP]
>
>See the document [Headful and Headless in AEM](/help/implementing/developing/headful-headless.md) for more information.
-->

## AEM 6.5 및 헤드리스 {#aem-headless}

AEM 6.5는 세 가지 강력한 서비스를 제공하여 헤드리스 구현 모델을 위한 유연한 도구입니다.

1. 컨텐츠 모델
   * 컨텐츠 모델은 컨텐츠의 구조화된 표현입니다.
   * 이는 AEM 컨텐츠 조각 모델 편집기의 정보 설계자에 의해 정의됩니다.
   * 컨텐츠 모델은 컨텐츠 조각의 기반이 됩니다.
1. 콘텐츠 조각
   * 컨텐츠 조각은 컨텐츠 모델을 인스턴스화합니다.
   * 이러한 템플릿은 AEM 컨텐츠 조각 편집기를 사용하여 컨텐츠 작성자가 만듭니다.
   * AEM Assets에 저장되고 Assets 관리 UI에서 관리됩니다.
1. 게재용 컨텐츠 API
   * AEM GraphQL API는 컨텐츠 조각 전달을 지원합니다.
   * AEM Assets REST API는 컨텐츠 조각 CRUD 작업을 지원합니다.
   * 또한 [컨텐츠 조각 코어 구성 요소의 JSON 내보내기.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)

## AEM 헤드리스를 사용한 첫 번째 단계 {#first-steps}

AEM 헤드리스 기능을 시작할 수 있는 리소스는 많습니다. 이 기능은 서로 다른 사용 사례를 위해 작성되었지만, 모두 AEM 헤드리스 기능에 대한 구체적인 개요를 제공합니다.

| 리소스 | 설명 | 유형 | 속성을 확인하는 | 설정. 시간 |
|---|---|---|---|---|
| [AEM Headless 실습 자습서 시작하기](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) | **실습 방법을 선호하며 AEM에 익숙하다면**, 이 자습서에서는 간단한 헤드리스 프로젝트를 제작하기 위해 바로 안내합니다. | 튜토리얼 | 개발자 | 2시간 |

<!-- HM-Links
|Resource|Description|Type|Audience|Est. Time|
|---|---|---|---|---|
|[Headless Developer Journey](/help/journey-headless/developer/overview.md)|**For users new to AEM and headless** technologies, start here for a comprehensive introduction to AEM and its headless features from the theory of headless through going live with your first headless project.|Guide|Developers **new to AEM and headless**|1 hour|
|[Headless Getting Started Guide](/help/implementing/developing/headless/getting-started/introduction.md)|**For experienced AEM users** who need a short summary of the key AEM headless features, check out this quick start overview.|Quick Start|Developers, Administrators **with AEM experience**|20 minutes|
|[Getting Started with AEM Headless hands-on tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html)|**If you prefer a hands-on approach and are familiar with AEM**, this tutorial dives directly into creating a simple headless project.|Tutorial|Developers|2 hours|
-->
