---
title: 캐싱 및 성능
description: GraphQL 및 콘텐츠 캐싱을 활성화하여 상거래 구현의 성능을 최적화하는 데 사용할 수 있는 다양한 구성에 대해 알아봅니다.
exl-id: ecce64bf-5960-4ddb-b6e3-dad401038c11
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 0%

---

# 캐싱 및 성능 {#caching}

## 구성 요소 및 GraphQL 응답 캐싱 {#graphql}

AEM CIF 핵심 구성 요소에는 이미 개별 구성 요소에 대한 GraphQL 응답을 캐시하는 기능이 내장되어 있습니다. 이 기능을 사용하면 GraphQL 백엔드 호출 수를 크게 줄일 수 있습니다. 특히 탐색 구성 요소에 대한 범주 트리를 검색하거나 제품 검색 및 범주 페이지에 표시된 모든 사용 가능한 집계/패싯 값을 가져오는 등의 반복 쿼리에 효과적인 캐싱을 수행할 수 있습니다.

AEM CIF 핵심 구성 요소의 경우 캐싱이 구성 요소 기반으로 구성되므로 각 구성 요소에 대해 GraphQL 요청/응답이 캐시되는지 여부(및 기간)를 제어할 수 있습니다. GraphQL 클라이언트를 사용하여 OSGi 서비스에 대한 캐싱 동작을 정의할 수도 있습니다.

### 구성

지정된 구성 요소에 대해 구성된 캐시는 각 캐시 구성 항목으로 정의된 대로 GraphQL 쿼리 및 응답 저장을 시작합니다. 예를 들어, 카탈로그 데이터가 변경되는 빈도, 구성 요소에 가능한 최신 데이터가 항상 표시되는 것이 얼마나 중요한지 등에 따라, 각 항목의 캐시 크기 및 캐싱 기간을 프로젝트 단위로 정의합니다. 캐시 무효화는 없으므로 캐시 지속 시간을 설정할 때 주의하십시오.

구성 요소에 대한 캐싱을 구성할 때 캐시 이름은 의 이름이어야 합니다. **프록시** 프로젝트에서 정의하는 구성 요소입니다.

클라이언트가 GraphQL 요청을 보내기 전에 **정확** 동일한 GraphQL 요청이 이미 캐시되었으며 캐시된 응답을 반환할 수 있습니다. 일치시키려면 GraphQL 요청이 정확히 일치해야 합니다. 즉, 쿼리, 작업 이름(있는 경우), 변수(있는 경우)가 모두 캐시된 요청과 동일해야 하며, 설정할 수 있는 모든 사용자 지정 HTTP 헤더도 동일해야 합니다. (예: Adobe Commerce) `Store` 헤더가 일치해야 합니다.

### 예

제품 검색 및 카테고리 페이지에 표시된 사용 가능한 모든 집계/패싯 값을 가져오는 검색 서비스에 대한 일부 캐싱을 구성하는 것이 좋습니다. 이러한 값은 일반적으로 새 속성(예: 제품)이 추가될 때만 변경되므로, 제품 속성 세트가 자주 변경되지 않는 경우 이 캐시 항목의 지속 시간이 &quot;큼&quot;일 수 있습니다. 프로젝트에 따라 다르지만 Adobe은 프로젝트 개발 단계에서 몇 분, 안정적인 프로덕션 시스템에서 몇 시간의 값을 권장합니다.

일반적으로 다음 캐시 항목으로 구성됩니다.

```
com.adobe.cq.commerce.core.search.services.SearchFilterService:true:10:3600
```

GraphQl 캐싱 기능을 사용하는 것이 권장되는 다른 예제 시나리오는 모든 페이지에서 동일한 GraphQL 쿼리를 보내기 때문에 탐색 구성 요소입니다. 이 경우 캐시 항목은 일반적으로 다음과 같이 설정됩니다.

```
venia/components/structure/navigation:true:10:600
```

다음 사항을 고려하는 경우 [Venia 참조 저장소](https://github.com/adobe/aem-cif-guides-venia) 를 사용합니다. 구성 요소 프록시 이름의 사용을 확인합니다. `venia/components/structure/navigation`, 및 **아님** CIF 탐색 구성 요소의 이름(`core/cif/components/structure/navigation/v1/navigation`).

다른 구성 요소에 대한 캐싱은 일반적으로 Dispatcher 수준에서 구성된 캐싱과 함께 프로젝트 기반으로 정의되어야 합니다. 이러한 캐시에 대한 활성 무효화가 없으므로 캐싱 기간을 신중하게 설정해야 합니다. 가능한 모든 프로젝트 및 사용 사례와 일치하는 &quot;한 가지 크기가 모두 맞춤&quot; 값은 없습니다. 프로젝트의 요구 사항과 가장 일치하는 프로젝트 수준에서 캐싱 전략을 정의해야 합니다.

## Dispatcher 캐싱 {#dispatcher}

에서 AEM 페이지 또는 조각 캐싱 [AEM 디스패처](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html) 는 모든 AEM 프로젝트에 대한 우수 사례입니다. 일반적으로 AEM에서 변경된 모든 콘텐츠가 Dispatcher에서 제대로 업데이트되는지 확인하는 무효화 기술에 의존합니다. 이는 AEM Dispatcher 캐싱 전략의 핵심 기능입니다.

순수 AEM 관리 컨텐츠 CIF 외에도 페이지는 일반적으로 GraphQL을 통해 Adobe Commerce에서 동적으로 가져오는 상거래 데이터를 표시할 수 있습니다. 페이지 구조 자체는 변경되지 않지만, 일부 제품 데이터(예: 이름 또는 가격)가 Adobe Commerce에서 변경되는 경우 상거래 콘텐츠가 변경될 수 있습니다.

AEM Dispatcher에서 제한된 시간 동안 CIF 페이지를 캐시할 수 있도록 하려면 를 사용하는 것이 좋습니다. [시간 기반 캐시 무효화](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring-time-based-cache-invalidation-enablettl) AEM Dispatcher에서 CIF 페이지를 캐싱할 때 TTL 기반 캐싱이라고도 합니다. 이 기능은 추가 기능을 사용하여 AEM에서 구성할 수 있습니다 [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/) 패키지.

TTL 기반 캐싱을 사용하여 개발자는 일반적으로 선택한 AEM 페이지에 대해 하나 이상의 캐싱 기간을 정의합니다. 이렇게 하면 CIF 페이지가 구성된 기간까지 AEM Dispatcher에 캐시되고 콘텐츠가 자주 업데이트됩니다.

>[!NOTE]
>
>서버측 데이터는 AEM Dispatcher에 의해 캐시될 수 있지만 일부 CIF 구성 요소는 다음과 같습니다. `product`, `productlist`, 및 `searchresults` 일반적으로 구성 요소는 페이지가 로드될 때 클라이언트측 브라우저 요청에서 항상 제품 가격을 다시 가져옵니다. 이렇게 하면 페이지 로드 시 중요한 동적 콘텐츠를 항상 가져올 수 있습니다.

## 추가 리소스

- [Venia 참조 저장소](https://github.com/adobe/aem-cif-guides-venia)
- [GraphQL 캐싱 구성](https://github.com/adobe/commerce-cif-graphql-client#caching)
- [AEM 디스패처](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html)
