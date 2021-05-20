---
title: 캐싱 및 성능
description: GraphQL 및 콘텐츠 캐싱을 사용하여 상거래 구현 성능을 최적화하는 데 사용할 수 있는 다양한 구성에 대해 알아봅니다.
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 1%

---

# 캐싱 및 성능 {#caching}

## 구성 요소 및 GraphQL 응답 캐싱 {#graphql}

AEM CIF 코어 구성 요소는 이미 개별 구성 요소에 대한 GraphQL 응답 캐싱을 기본 지원합니다. 이 기능을 사용하여 큰 요인으로 GraphQL 백엔드 호출 수를 줄일 수 있습니다. 탐색 구성 요소에 대한 카테고리 트리를 검색하거나 제품 검색 및 카테고리 페이지에 표시되는 사용 가능한 모든 합계/패싯 값을 가져오는 등의 반복 쿼리에 효과적인 캐싱을 수행할 수 있습니다.

AEM CIF 코어 구성 요소의 경우 캐싱은 구성 요소 기반으로 구성되므로 각 구성 요소에 대해 GraphQL 요청/응답이 캐시되는지(및 기간)를 제어할 수 있습니다. GraphQL 클라이언트를 사용하여 OSGi 서비스에 대한 캐싱 동작을 정의할 수도 있습니다.

### 구성

지정된 구성 요소에 대해 구성되면 캐시는 각 캐시 구성 항목에 정의된 대로 GraphQL 쿼리 및 응답을 저장하기 시작합니다. 캐시 크기 및 각 항목의 캐싱 기간은 프로젝트 단위로 정의됩니다. 예를 들어 카탈로그 데이터가 변경되는 빈도, 구성 요소가 항상 가능한 최신 데이터를 표시하는 중요성 등에 따라 정의됩니다. 캐시 무효화가 없으므로 캐시 기간을 설정할 때 주의하십시오.

구성 요소에 대해 캐싱을 구성할 때 캐시 이름은 프로젝트에서 정의하는 **proxy** 구성 요소의 이름이어야 합니다.

클라이언트가 GraphQL 요청을 보내기 전에 **exact** 동일한 GraphQL 요청이 이미 캐시되어 있는지 확인하고 캐시된 응답을 반환할 수 있습니다. 일치시키려면 GraphQL 요청이 정확히 일치해야 합니다. 쿼리, 작업 이름(있는 경우), 변수(있는 경우)는 모두 캐시된 요청과 같아야 하며 HTTP를 설정할 수 있는 모든 사용자 지정 헤더도 같아야 합니다. 예를 들어 Magento `Store` 헤더가 일치해야 합니다.

### 예

제품 검색 및 카테고리 페이지에 표시되는 모든 사용 가능한 집계/패싯 값을 가져오는 검색 서비스에 대해 일부 캐싱을 구성하는 것이 좋습니다. 이러한 값은 일반적으로 새 속성(예: 제품에 추가된 경우에만 변경되므로 제품 속성 세트가 자주 변경되지 않는 경우 이 캐시 항목의 기간은 &quot;큰&quot;일 수 있습니다. 프로젝트별로 다르겠지만, 프로젝트 개발 단계에서 몇 분, 안정적인 프로덕션 시스템에서 몇 시간 동안의 값을 추천합니다.

일반적으로 다음 캐시 항목으로 구성됩니다.

```
com.adobe.cq.commerce.core.search.services.SearchFilterService:true:10:3600
```

GraphQl 캐싱 기능을 사용하는 것이 권장되는 다른 예제 시나리오는 모든 페이지에서 동일한 GraphQL 쿼리를 보내기 때문에 탐색 구성 요소입니다. 이 경우 캐시 항목은 일반적으로 다음과 같이 설정됩니다.

```
venia/components/structure/navigation:true:10:600
```

[Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)가 사용됨을 고려할 때 구성 요소 프록시 이름 `venia/components/structure/navigation` 및 CIF 탐색 구성 요소의 이름(`core/cif/components/structure/navigation/v1/navigation`)이 아닌 **을 사용하십시오.**

다른 구성 요소에 대한 캐싱은 일반적으로 Dispatcher 수준에서 구성된 캐싱과 함께 프로젝트 기반으로 정의해야 합니다. 이러한 캐시의 활성 무효화가 없으므로 캐싱 기간을 신중하게 설정해야 합니다. 가능한 모든 프로젝트 및 사용 사례와 일치하는 &quot;모든 값에 맞는 단일 크기&quot;가 없습니다. 프로젝트의 요구 사항에 가장 잘 맞는 프로젝트 수준에서 캐싱 전략을 정의해야 합니다.

## Dispatcher 캐싱 {#dispatcher}

[AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ko-KR)의 AEM 페이지 또는 조각을 캐시하는 것은 모든 AEM 프로젝트에 가장 좋습니다. 일반적으로, AEM에서 변경된 모든 컨텐츠가 Dispatcher에서 제대로 업데이트되도록 하는 무효화 기술에 의존합니다. AEM Dispatcher 캐싱 전략의 핵심 기능입니다.

순수 AEM 관리 컨텐츠 CIF 외에도 페이지는 일반적으로 GraphQL을 통해 Magento에서 동적으로 가져오는 상거래 데이터를 표시할 수 있습니다. 페이지 구조 자체는 변경되지 않을 수 있지만 일부 제품 데이터(예: 이름 또는 가격)가 Magento에서 변경되는 경우 상거래 콘텐츠가 변경될 수 있습니다.

AEM Dispatcher에서 제한된 시간 동안 CIF 페이지를 캐시할 수 있도록 하려면 AEM Dispatcher에서 CIF 페이지를 캐싱할 때 [시간 기반 캐시 무효화](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-time-based-cache-invalidation-enablettl)(TTL 기반 캐싱이라고도 함)를 사용하는 것이 좋습니다. 이 기능은 추가 [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/) 패키지를 사용하여 AEM에서 구성할 수 있습니다.

TTL 기반 캐싱을 사용하는 개발자는 일반적으로 선택한 AEM 페이지에 대해 하나 이상의 캐싱 기간을 정의합니다. 이렇게 하면 CIF 페이지가 구성된 기간까지 AEM Dispatcher에서만 캐시되며 컨텐츠가 자주 업데이트됩니다.

>[!NOTE]
>
>AEM Dispatcher에서 서버측 데이터를 캐시할 수 있는 반면, `product`, `productlist` 및 `searchresults` 구성 요소와 같은 일부 CIF 구성 요소는 일반적으로 페이지가 로드될 때 클라이언트측 브라우저 요청에서 제품 가격을 다시 가져옵니다. 이렇게 하면 페이지 로드 시 중요한 동적 콘텐츠를 항상 가져올 수 있습니다.

## 추가 리소스

- [Venia 참조 저장소](https://github.com/adobe/aem-cif-guides-venia)
- [GraphQL 캐싱 구성](https://github.com/adobe/commerce-cif-graphql-client#caching)
- [AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html)
