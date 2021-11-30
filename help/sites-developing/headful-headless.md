---
title: AEM의 헤드리스 및 헤드리스
description: AEM 프로젝트는 headful 및 headless 모델로 구현할 수 있지만 선택은 바이너리가 아닙니다. AEM은 한 프로젝트에서 두 모델의 장점을 모두 활용할 수 있는 유연성을 제공합니다.
source-git-commit: cf7e9061bac9004c7efd2f045b4900e4a92d67e9
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 0%

---

# AEM의 헤드리스 및 헤드리스 {#headful-headless}

Adobe Experience Manager 프로젝트는 제목이 많은 모델과 헤드리스 모델 모두에서 구현할 수 있지만 선택할 수 있는 것은 바이너리가 아닙니다. AEM은 한 프로젝트에서 두 모델의 장점을 모두 활용할 수 있는 유연성을 제공합니다. 이 문서에서는 다른 모델에 대한 개요를 제공하며 SPA 통합 수준을 설명합니다.

## 개요 {#overview}

AEM은 하나의 플랫폼에서 콘텐츠 만들기와 게재를 모두 관리할 수 있는 강력한 도구를 제공합니다. 이 모델은 컨텐츠 작성자와 개발자가 동일한 플랫폼에서 컨텐츠 소비자에게 경험을 전달하는 기존의 &quot;제목이 많은&quot; 컨텐츠 관리 모델입니다.

또한 AEM을 사용하여 컨텐츠를 간편하게 관리할 수 있으므로, 다른 플랫폼에서 컨텐츠를 표시하고 전달할 수 있습니다. 컨텐츠 작성자와 개발자가 다른 플랫폼에서 컨텐츠 소비자에게 경험을 제공하기 위해 작업하는 &quot;헤드리스&quot; 컨텐츠 관리 모델입니다.

하지만 이것은 이진법으로 선택할 필요는 없다. AEM은 전례 없는 유연성을 제공하므로 두 모델의 프로젝트를 활용할 수 있습니다.

![AEM 구현 모델](headless/assets/aem-implementation-models.png)

헤더 또는 전체 스택 모델에서 컨텐츠는 Java, HTL 등을 기반으로 하는 AEM 저장소 및 AEM 구성 요소에서 관리됩니다. 사용자 경험을 위한 컨텐츠를 렌더링하는 데 사용됩니다. 이 모델에서 컨텐츠를 만들고, 스타일을 지정하고, 표현하고, 전달하는 것은 모두 AEM에서 이루어집니다.

헤드리스 모델에서 컨텐츠는 AEM 리포지토리에서 관리되지만, REST 및 GraphQL과 같은 API를 통해 다른 시스템으로 전달되어 사용자 경험을 위한 컨텐츠를 렌더링합니다. 이 모델에서는 컨텐츠가 AEM에서 만들어지지만 스타일링을 하고, 표시하고 다른 플랫폼에서 실현됩니다.

단일 페이지 애플리케이션(SPA)은 종종 AEM에서 헤드리도록 제공하는 컨텐츠의 대상입니다. 그러나 이러한 SPA이 AEM에 전적으로 외부 대상일 필요는 없습니다. AEM을 사용하면 SPA이 AEM에 통합되는 정도를 결정할 수 있습니다. 예를 들어봅시다.

## 웹 스토어 예 {#web-shop-example}

SPA으로 회사를 위한 기존 웹 가게가 있다고 가정해 보겠습니다. 여기에 모든 제품 세부 사항과 이미지가 있습니다. 그런 다음 홍보 사이트, 블로그 및 캠페인 콘텐츠와 같은 마케팅 활동을 지원하기 위해 AEM을 도입합니다. 두 가지를 어떻게 통합합니까? AEM에서는 다음과 같은 다양한 옵션을 사용할 수 있습니다.

* **시스템이 독립적으로 작동할 수 있도록 허용합니다.**
* **GraphQL을 통해 AEM에서 제한된 콘텐츠를 제공하는 웹 스토어를 제공합니다.** 컨텐츠는 AEM의 작성자가 만들 수 있지만, Web Shop SPA을 통해서만 볼 수 있습니다.
* **AEM에 Web Shop SPA 포함.** 컨텐츠는 AEM의 작성자가 만들고 웹 샵의 컨텍스트에서 AEM에서 볼 수 있지만 조작되지는 않습니다.
* **AEM에 Web Shop SPA을 포함하고 편집 가능한 지점을 활성화합니다.** 컨텐츠는 AEM의 작성자가 만들고 웹 상점 컨텍스트에서 AEM에서 볼 수 있으며 작성자는 AEM 내에서 Web Shop SPA의 컨텐츠를 조작하는 제한된 기능을 갖습니다.
* **AEM에 웹 샵 SPA을 포함하고 전체 영역을 편집할 수 있도록 활성화합니다.** 컨텐츠는 AEM의 작성자가 만들고 웹 상점 컨텍스트에서 AEM에서 볼 수 있으며 작성자는 AEM 내에서 Web Shop SPA의 컨텐츠를 조작하는 제한된 기능을 갖습니다.

다음 섹션에서는 이러한 통합 수준을 자세히 설명합니다.

>[!NOTE]
>
>물론 완전히 작동하는 AEM SPA로서 web shop SPA을 다시 구현할 수도 있습니다 [AEM SPA 편집기 프레임워크 사용.](/help/sites-developing/spa-walkthrough.md) 이미 AEM이 있고 새 웹 스토어 또는 다른 SPA을 만들려는 경우 이 방법이 권장되지만 이 문서의 범위를 벗어납니다.

## SPA 통합 수준 {#integration-levels}

SPA 통합은 AEM에서 네 가지 수준의 스펙트럼에 해당합니다.

* **레벨 0: 통합 없음**
   * SPA과 AEM은 별도로 존재하며 정보를 교환하지 않습니다.
   * 컨텐츠는 두 개의 별도 시스템에서 독립적으로 생성, 관리 및 전달됩니다.
* **수준 1: 컨텐츠 조각 통합**
   * [컨텐츠 조각](/help/assets/content-fragments/content-fragments.md) AEM에서 SPA에 대한 제한된 컨텐츠를 만들고 관리하는 데 사용됩니다.
   * SPA은 AEM을 통해 이 컨텐츠를 검색합니다 [GraphQL API.](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * 일부 컨텐츠는 AEM에서 관리되고 일부는 외부 시스템에서 관리됩니다.
   * 콘텐츠는 SPA에서만 볼 수 있습니다.
* **레벨 2: AEM에 SPA 포함**
   * [컨텐츠 조각](/help/assets/content-fragments/content-fragments.md) SPA용 컨텐츠를 만들고 관리하는 데 AEM에서 사용됩니다.
   * SPA은 AEM을 통해 이 컨텐츠를 검색합니다 [GraphQL API.](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * 일부 컨텐츠는 AEM에서 관리되고 일부는 외부 시스템에서 관리됩니다.
   * 컨텐츠는 AEM 내에서 컨텍스트 내에서 볼 수 있습니다.
   * 제한된 컨텐츠는 AEM 내에서 편집할 수 있습니다.
* **레벨 3: AEM에서 SPA 포함 및 전체 활성화**
   * [컨텐츠 조각](/help/assets/content-fragments/content-fragments.md) SPA용 컨텐츠를 만들고 관리하는 데 AEM에서 사용됩니다.
   * SPA은 AEM을 통해 이 컨텐츠를 검색합니다 [GraphQL API.](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * 컨텐츠는 AEM 내에서 컨텍스트 내에서 볼 수 있습니다.
   * 대부분의 컨텐츠는 AEM 내에서 편집할 수 있습니다.

수준 1은 일반적인 헤드리스 구현의 예입니다. 그러나 컨텐츠 작성자는 SPA 내에서 컨텍스트 내의 컨텐츠만 볼 수 있습니다. AEM은 작성 도구일 뿐입니다.

AEM의 장점과 유연성은 SPA의 장점을 그대로 유지하면서 레벨 2와 3에서 두드러집니다. 컨텐츠 작성자는 AEM에서 자신의 컨텐츠를 만들 수 있지만 AEM 내에서 컨텍스트 내에서 볼 수도 있습니다. SPA은 AEM에서 작성할 수 있지만 여전히 SPA으로 배달됩니다.

## 통합 수준 구현 {#implementing}

AEM에는 선택한 통합 수준에 따라 다른 도구를 사용할 수 있습니다. 각 레벨은 이전에 사용된 도구를 기반으로 빌드합니다. 다음 목록은 관련 리소스에 연결되어 있습니다.

* **수준 1:** 컨텐츠 조각 및 [AEM 헤드리스 프레임워크](/help/sites-developing/headless/introduction.md) SPA에 AEM 컨텐츠를 전달하는 데 사용할 수 있습니다.
* **레벨 2:** 레벨 1 외에
   * [RemotePage 구성 요소](/help/sites-developing/spa-remote-page.md) AEM 컨텐츠를 컨텍스트에서 볼 수 있는 AEM에 외부 SPA을 포함하는 데 사용할 수 있습니다.
   * SPA의 특정 지점을 활성화하여 [AEM에서 제한된 편집을 허용합니다.](/help/sites-developing/spa-edit-external.md)
* **레벨 3:** 레벨 2 외에
   * SPA의 전체 영역을 활성화하여 AEM에서 포괄적인 편집을 허용할 수 있습니다.
