---
title: 캐싱 및 성능
description: GraphQL 및 컨텐츠 캐싱을 사용하여 상거래 구현 성능을 최적화하는 데 사용할 수 있는 다양한 구성에 대해 알아봅니다.
translation-type: tm+mt
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 1%

---

# 캐싱 및 성능 {#caching}

## 구성 요소 및 그래프QL 응답 캐싱 {#graphql}

AEM CIF 핵심 구성 요소는 이미 개별 구성 요소에 대한 GraphQL 응답 캐싱에 대한 내장된 지원을 제공합니다. 이 기능을 사용하여 GraphQL 백엔드 호출 수를 큰 요인으로 줄일 수 있습니다. 탐색 구성 요소에 대한 카테고리 트리 검색 또는 제품 검색 및 카테고리 페이지에 표시된 모든 사용 가능한 집계/패싯 값을 가져오는 것과 같은 반복 질의에 대해 효과적인 캐싱을 수행할 수 있습니다.

AEM CIF 핵심 구성 요소의 경우 캐싱은 구성 요소 기반으로 구성되므로 각 구성 요소에 대해 GraphQL 요청/응답이 캐시되는지 여부(및 시간)를 제어할 수 있습니다. GraphQL 클라이언트를 사용하여 OSGi 서비스에 대한 캐싱 동작을 정의할 수도 있습니다.

### 구성

지정된 구성 요소에 대해 구성된 캐시는 각 캐시 구성 항목에 의해 정의된 대로 GraphQL 쿼리 및 응답을 저장하기 시작합니다. 캐시 크기 및 각 항목의 캐싱 기간은 프로젝트를 기준으로 정의됩니다. 예를 들어 카탈로그 데이터가 변경될 수 있는 빈도, 구성 요소가 항상 가능한 최신 데이터를 표시하는 것이 얼마나 중요한지 등에 따라 결정됩니다. 캐시 무효화가 없으므로 캐시 기간을 설정할 때는 주의하십시오.

구성 요소에 대해 캐싱을 구성할 때 캐시 이름은 프로젝트에서 정의하는 **proxy** 구성 요소의 이름이어야 합니다.

클라이언트가 GraphQL 요청을 보내기 전에 **exact** 동일한 GraphQL 요청이 이미 캐시되었는지 확인하고 캐시된 응답을 반환할 수 있습니다. 일치하려면 GraphQL 요청이 정확히 일치해야 합니다. 쿼리, 작업 이름(있는 경우), 변수(있는 경우)는 모두 캐시된 요청과 같아야 하며 HTTP로 설정될 수 있는 모든 사용자 지정 HTTP 헤더도 같아야 합니다. 예를 들어 Magento `Store` 헤더는 일치해야 합니다.

### 예

제품 검색 및 카테고리 페이지에 표시되는 모든 사용 가능한 집계/패싯 값을 가져오는 검색 서비스에 대해 일부 캐시를 구성하는 것이 좋습니다. 이러한 값은 일반적으로 새 속성(예: 제품에 추가된 경우)만 변경되므로 제품 특성 세트가 자주 변경되지 않는 경우 이 캐시 항목의 지속 시간은 &quot;large&quot;가 될 수 있습니다. 프로젝트별로 설명하지만 프로젝트 개발 단계에서 몇 분, 안정적인 프로덕션 시스템에서 몇 시간의 값을 갖는 것이 좋습니다.

이것은 일반적으로 다음 캐시 항목으로 구성됩니다.

```
com.adobe.cq.commerce.core.search.services.SearchFilterService:true:10:3600
```

GraphQl 캐싱 기능을 사용하는 것이 권장되는 다른 예제 시나리오는 모든 페이지에서 동일한 GraphQL 쿼리를 보내기 때문에 탐색 구성 요소입니다. 이 경우 캐시 항목은 일반적으로 다음과 같이 설정됩니다.

```
venia/components/structure/navigation:true:10:600
```

[Venia Reference store](https://github.com/adobe/aem-cif-guides-venia)가 사용됨을 고려할 때 구성 요소 프록시 이름 `venia/components/structure/navigation` 및 CIF 탐색 구성 요소의 이름(`core/cif/components/structure/navigation/v1/navigation`)이 아닌 **의 사용을 참고하십시오.**

다른 구성 요소에 대한 캐싱은 일반적으로 발송자 수준에서 구성된 캐싱과 함께 프로젝트 기준으로 정의해야 합니다. 이러한 캐시의 활성 무효화가 없으므로 캐싱 기간을 신중하게 설정해야 합니다. 가능한 모든 프로젝트 및 사용 사례와 일치하는 &quot;모든 프로젝트에 맞는 하나의&quot; 값이 없습니다. 프로젝트의 요구 사항에 가장 적합한 프로젝트 수준에서 캐싱 전략을 정의해야 합니다.

## 발송자 캐싱 {#dispatcher}

AEM 페이지 또는 조각을 [AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ko-KR)에 캐시하는 것은 모든 AEM 프로젝트에 가장 좋은 방법입니다. 일반적으로 AEM에서 변경된 컨텐츠가 디스패처에서 올바르게 업데이트되도록 하는 무효화 기술에 의존합니다. 이는 AEM Dispatcher 캐싱 전략의 핵심 기능입니다.

순수 AEM 관리 컨텐츠 CIF 외에도 페이지는 일반적으로 GraphQL을 통해 Magento에서 동적으로 가져오는 상거래 데이터를 표시할 수 있습니다. 페이지 구조 자체는 변경되지 않지만, 예를 들어 Magento에서 일부 제품 데이터(이름 또는 가격 등)가 변경되는 경우 상거래 컨텐츠가 변경될 수 있습니다.

AEM Dispatcher에서 한정된 기간 동안 CIF 페이지를 캐시할 수 있도록 하기 위해 AEM Dispatcher에서 CIF 페이지를 캐싱할 때 [시간 기반 캐시 무효화](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-time-based-cache-invalidation-enablettl)(TTL 기반 캐싱이라고도 함)을 사용하는 것이 좋습니다. 이 기능은 추가 [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/) 패키지를 사용하여 AEM에서 구성할 수 있습니다.

TTL 기반 캐싱을 사용하는 개발자는 일반적으로 선택한 AEM 페이지에 대해 하나 이상의 캐싱 기간을 정의합니다. 이렇게 하면 CIF 페이지가 구성된 기간까지만 AEM Dispatcher에 캐시되고 컨텐츠가 자주 업데이트됩니다.

>[!NOTE]
>
>서버측 데이터는 AEM Dispatcher에서 캐시될 수 있지만, `product`, `productlist` 및 `searchresults` 구성 요소와 같은 일부 CIF 구성 요소는 일반적으로 페이지가 로드될 때 항상 클라이언트측 브라우저 요청에서 제품 가격을 다시 페치합니다. 따라서 페이지 로드 시 중요한 동적 컨텐츠를 항상 가져올 수 있습니다.

## 추가 리소스

- [Venia Reference store](https://github.com/adobe/aem-cif-guides-venia)
- [GraphQL 캐싱 구성](https://github.com/adobe/commerce-cif-graphql-client#caching)
- [AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html)
