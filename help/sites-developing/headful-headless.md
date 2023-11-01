---
title: AEM Headful 및 Headless
description: AEM 프로젝트는 Headful 및 Headless model 모델에서 구현될 수 있지만 양자택일은 아닙니다. AEM은 하나의 프로젝트에서 두 모델의 장점을 모두 활용할 수 있는 유연성을 제공합니다.
exl-id: c9597c78-be05-42ff-84fe-f7451119e83d
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 98%

---

# AEM Headful 및 Headless {#headful-headless}

Adobe Experience Manager 프로젝트는 Headful 및 Headless model 모델 모두에서 구현될 수 있지만 양자택일은 아닙니다. AEM은 하나의 프로젝트에서 두 모델의 장점을 모두 활용할 수 있는 유연성을 제공합니다. 이 문서에서는 다양한 모델에 대한 개요를 제공하고 SPA 통합 수준에 대해 설명합니다.

## 개요 {#overview}

AEM은 한 개의 플랫폼에서 콘텐츠 생성과 게재를 모두 관리할 수 있는 강력한 도구를 제공합니다. 이는 콘텐츠 관리의 기존 “Headful” 모델로서 콘텐츠 작성자와 개발자는 동일한 플랫폼에서 작업하여 콘텐츠 소비자에게 경험을 제공할 수 있습니다.

AEM을 사용하여 간단히 콘텐츠를 관리할 수도 있고, 다른 플랫폼에서 관리할 콘텐츠를 표시하고 게재할 수 있습니다. 이는 콘텐츠 관리의 기존 “Headless” 모델로서 콘텐츠 작성자와 개발자는 서로 다른 플랫폼에서 작업하여 콘텐츠 소비자에게 경험을 제공할 수 있습니다.

그러나 양자택일이 될 필요는 없습니다. AEM은 프로젝트에 두 모델의 장점을 모두 활용할 수 있는 유연성을 제공합니다.

![AEM 구현 모델](/help/sites-developing/headless/getting-started/assets/aem-implementation-models.png)

Headful 또는 전체 스택 모델에서 콘텐츠는 Java, HTL 등을 기반으로 하는 AEM 저장소와 AEM 구성 요소에서 관리합니다. 사용자 경험에 필요한 콘텐츠를 렌더링하는 데 사용됩니다. 이 모델에서는 콘텐츠 생성, 스타일 지정, 프레젠테이션과 게재가 모두 AEM에서 이뤄집니다.

Headless 모델에서 콘텐츠는 AEM 저장소에서 관리되지만 REST와 GraphQL 등 API를 통해 다른 시스템에 게재되어 사용자 경험에 필요한 콘텐츠를 렌더링합니다. 이 모델에서 콘텐츠는 AEM에서 생성되지만 스타일 지정, 프레젠테이션과 게재는 모두 다른 플랫폼에서 이뤄집니다.

단일 페이지 애플리케이션(SPA)은 종종 AEM에서 Headless 방식으로 게재되는 콘텐츠의 대상이기도 합니다. 단, 해당 SPA는 완전히 AEM 외부에 있을 필요는 없습니다. AEM을 통해 SPA가 AEM에 통합되는 정도를 파악할 수 있습니다. 예를 살펴보겠습니다.

## 웹 샵 예 {#web-shop-example}

회사에 대한 기존 웹 샵이 SPA로서 존재하고 있다고 가정해 보겠습니다. 여기에 모든 제품 세부 정보와 이미지가 있습니다. 그런 다음 AEM을 소개하고 프로모션 사이트, 블로그와 캠페인 콘텐츠 등 마케팅 활동을 홍보합니다. 두 가지를 통합하려면 어떻게 합니까? AEM은 옵션 스펙트럼을 활성화합니다.

* **시스템은 서로 독립적으로 작동할 수 있습니다.**
* **GraphQL을 통해 AEM의 제한된 콘텐츠를 웹 샵에 제공합니다.** 콘텐츠는 작성자에 의해 AEM에서 생성할 수 있지만 웹 샵 SPA를 통해서만 볼 수 있습니다.
* **AEM에 웹 샵 SPA를 임베드합니다.** 콘텐츠는 작성자에 의해 AEM에서 생성하고 웹 샵의 컨텍스트 내 AEM에서 볼 수 있지만 조작할 수는 없습니다.
* **AEM에 웹 샵 SPA를 임베드하고 편집 가능한 포인트를 활성화합니다.** 콘텐츠는 작성자에 의해 AEM에서 생성하고 웹 샵의 컨텍스트 내 AEM에서 볼 수 있습니다. 작성자는 제한된 기능으로 AEM 내부 웹 샵의 콘텐츠를 조작할 수 있습니다.
* **AEM에 웹 샵 SPA를 임베드하고 전체 편집 영역을 활성화합니다.** 콘텐츠는 작성자에 의해 AEM에서 생성하고 웹 샵의 컨텍스트 내 AEM에서 볼 수 있습니다. 작성자는 제한된 기능으로 AEM 내부 웹 샵의 콘텐츠를 조작할 수 있습니다.

다음 섹션에서는 해당 통합 수준에 대해 자세히 살펴봅니다.

>[!NOTE]
>
>물론, [AEM SPA 편집기 프레임워크를 사용하여 웹 샵 SPA를 완전히 기능하는 AEM SPA로 다시 구현할 수도 있습니다.](/help/sites-developing/spa-walkthrough.md) 이미 AEM이 있고 새 웹 샵이나 다른 SPA를 생성하는 경우 이는 권장되는 메서드이지만 이 문서의 범위에 적용되지 않습니다.

## SPA 통합 수준 {#integration-levels}

SPA 통합은 AEM에서 네 가지 수준의 스펙트럼에 속합니다.

* **수준 0: 통합 없음**
   * SPA와 AEM은 별도로 존재하고 정보를 교환하지 않습니다.
   * 콘텐츠는 두 개의 시스템에서 독립적으로 생성, 관리 및 게재됩니다.
* **수준 1: 콘텐츠 조각 통합**
   * [콘텐츠 조각](/help/assets/content-fragments/content-fragments.md)을 사용하여 AEM에서 SPA의 제한된 콘텐츠를 만들고 관리합니다.
   * SPA는 AEM의 [GraphQL API.](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md)를 통해 이 콘텐츠를 검색합니다.
   * 일부 콘텐츠는 AEM에서 관리되고, 일부 콘텐츠는 외부 시스템에서 관리됩니다.
   * 콘텐츠는 SPA에서만 볼 수 있습니다.
* **수준 2: AEM에 SPA 임베드**
   * [콘텐츠 조각](/help/assets/content-fragments/content-fragments.md)을 사용하여 AEM에서 SPA의 콘텐츠를 만들고 관리합니다.
   * SPA는 AEM의 [GraphQL API.](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md)를 통해 이 콘텐츠를 검색합니다.
   * 일부 콘텐츠는 AEM에서 관리되고, 일부 콘텐츠는 외부 시스템에서 관리됩니다.
   * 콘텐츠는 AEM 내 컨텍스트에서 볼 수 있습니다.
   * 제한된 콘텐츠는 AEM 내에서 편집할 수 있습니다.
* **수준 3: AEM의 SPA 임베드 및 전체 활성화**
   * [콘텐츠 조각](/help/assets/content-fragments/content-fragments.md)을 사용하여 AEM에서 SPA의 콘텐츠를 만들고 관리합니다.
   * SPA는 AEM의 [GraphQL API.](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md)를 통해 이 콘텐츠를 검색합니다.
   * 콘텐츠는 AEM 내 컨텍스트에서 볼 수 있습니다.
   * 대부분의 콘텐츠는 AEM 내에서 편집할 수 있습니다.

수준 1은 일반적인 Headless 구현의 예입니다. 단, 콘텐츠 작성자는 SPA 내 컨텍스트 내에서만 콘텐츠를 볼 수 있습니다. AEM은 작성 도구일 뿐입니다.

SPA 장점을 계속 유지하면서 AEM의 장점과 유연성을 수준 2와 3에 표시합니다. 콘텐츠 작성자는 AEM에서 콘텐츠를 생성하고 AEM 내 컨텍스트에서 확인할 수도 있습니다. SPA는 AEM에서 작성될 수 있지만 여전히 SPA로 게재됩니다.

## 통합 수준 구현 {#implementing}

선택한 통합 수준에 따라 AEM에서 다양한 도구를 사용할 수 있습니다. 각 수준은 이전 수준에서 사용되는 도구를 기반으로 빌드됩니다. 다음 목록은 관련 리소스에 연결됩니다.

* **수준 1:** 콘텐츠 조각과 [AEM Headless 프레임워크](/help/sites-developing/headless/introduction.md)를 사용하여 AEM 콘텐츠를 SPA에 게재할 수 있습니다.
* **수준 2:** 수준 1 외에:
   * [RemotePage 구성 요소](/help/sites-developing/spa-remote-page.md)를 사용하여 외부 SPA를 AEM에 임베드하여 컨텍스트 내에서 AEM 콘텐츠를 볼 수 있습니다.
   * SPA의 특정 지점을 활성화하여 [AEM에서 제한적으로 편집할 수도 있습니다.](/help/sites-developing/spa-edit-external.md)
* **수준 3:** 수준 2 외에:
   * AEM에서 종합적인 편집을 수행하도록 전체 SPA 영역을 활성화할 수 있습니다.
