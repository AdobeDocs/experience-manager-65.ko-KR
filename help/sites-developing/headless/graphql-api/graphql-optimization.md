---
title: GraphQL 쿼리 최적화
description: Headless 콘텐츠 전달을 위해 Adobe Experience Manager as a Cloud Service에서 콘텐츠 조각을 필터링, 페이징 및 정렬할 때 GraphQL 쿼리를 최적화하는 방법에 대해 알아봅니다.
source-git-commit: 1481d613783089046b44d4652d38f7b4b16acc4d
workflow-type: tm+mt
source-wordcount: '1186'
ht-degree: 58%

---


# GraphQL 쿼리 최적화 {#optimizing-graphql-queries}

>[!NOTE]
>
>이러한 최적화 권장 사항을 적용하기 전에 다음을 고려하십시오 [GraphQL 필터링에서 페이징 및 정렬을 위한 콘텐츠 조각 업데이트](/help/sites-developing/headless/graphql-api/graphql-optimized-filtering-content-update.md) 최상의 성능을 제공합니다.

동일한 모델이 공유하는 콘텐츠 조각이 많은 AEM 인스턴스에서 GraphQL 목록 쿼리는 리소스 측면에서 많은 비용이 발생할 수 있습니다.

이유는 *모두* GraphQL 쿼리 내에서 사용 중인 모델을 공유하는 조각은 메모리에 로드되어야 합니다. 그렇게 하면 시간과 기억력이 모두 소모된다. (최종) 결과 세트의 항목 수를 줄여 줄 수 있는 필터링은 전체 결과 세트를 메모리에 로드한 **후에만** 적용할 수 있습니다.

이러한 과정은 작은 결과 집합(can)도 나쁜 성과로 이어진다는 인상을 줄 수 있다. 하지만 필터링 적용 전에 내부적으로 처리해야 하기 때문에 실제로는 초기 결과 집합의 크기에 의해 느려지게 된다.

성능 및 메모리 문제를 줄이려면 이 초기 결과 세트를 최대한 작게 유지해야 합니다.

AEM은 GraphQL 쿼리를 최적화하는 데 2가지 접근 방식을 제공합니다.

* [하이브리드 필터링](#hybrid-filtering)
* [페이징](#paging) (또는 페이지 매김)

   * [정렬](#sorting)은 최적화와 직접적인 관련은 없지만 페이징과 관련이 있음

각 접근 방식에는 독자적인 사용 사례와 제한 사항이 있습니다. 이 문서는 하이브리드 필터링 및 페이징에 대한 정보와 함께 GraphQL 쿼리 최적화의 일부 [모범 사례](#best-practices)를 제공합니다.

## 하이브리드 필터링 {#hybrid-filtering}

하이브리드 필터링은 JCR 필터링과 AEM 필터링을 결합한 것입니다.

JCR 필터(쿼리 제한 형식)를 적용한 후에 AEM 필터링을 위해 결과 세트를 메모리에 로드합니다. 이 프로세스는 JCR 필터가 불필요한 결과를 미리 제거하기 때문에 메모리에 로드된 결과 세트를 줄이기 위한 것입니다.

>[!NOTE]
>
>기술적인 이유(예: 유연성, 조각 중첩)로 인해 AEM은 전체 필터링을 JCR에 위임할 수 없습니다.

이 기법에서는 GraphQL 필터의 유연성을 유지하면서 최대한 많은 필터링을 JCR에 위임합니다.

## 페이징 {#paging}

AEM의 GraphQL은 두 가지 유형의 페이지 매김을 지원합니다.

* [limit/offset 기반 페이지 매김](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#list-offset-limit)
이 유형의 페이지 매김은 목록 쿼리에 사용되며 이러한 쿼리는 다음으로 끝납니다. 
`List`로 끝납니다(예: `articleList`).
이 페이지 매김을 사용하려면 반환할 첫 번째 항목의 위치(`offset`)와 반환할 항목 수(`limit` 또는 페이지 크기)를 제공해야 합니다.

* [커서 기반 페이지 매김](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#paginated-first-after) (다음으로 표시: `first`및 `after`) 이 페이지 매김 유형은 커서라고도 하는 각 항목에 대한 고유한 ID를 제공합니다.
쿼리에서 사용자가 이전 페이지 마지막 항목의 커서와 페이지 크기(반환할 최대 항목 수)를 지정합니다.

   커서 기반 페이지 매김은 목록 기반 쿼리의 데이터 구조에 맞지 않기 때문에 AEM은 `Paginated` 쿼리 유형(예: `articlePaginated`)을 도입했습니다. 사용되는 데이터 구조 및 매개변수는 [GraphQL 커서 연결 사양](https://relay.dev/graphql/connections.htm)을 따릅니다.

   >[!NOTE]
   >
   >AEM은 현재 정방향 페이징(`after`/`first` 매개변수 사용)을 지원합니다.
   >
   >역방향 페이징(`before`/`last` 매개변수 사용)은 지원되지 않습니다.

## 정렬 {#sorting}

정렬은 모든 정렬 기준이 최상위 조각과 관련된 경우에만 효율적입니다.

정렬 순서에 중첩된 조각에 있는 하나 이상의 필드가 포함된 경우 최상위 모델을 공유하는 모든 조각이 메모리에 로드되어야 합니다. 이 흐름은 성능에 부정적인 영향을 줍니다.

>[!NOTE]
>
>최상위 필드에 대한 정렬도 (크지는 않지만) 성능에 영향을 미칩니다.

## 모범 사례 {#best-practices}

모든 최적화의 주요 목표는 초기 결과 세트를 줄이는 것입니다. 아래에 나열된 모범 사례는 그 방법을 소개합니다. 모범 사례는 결합할 수 있으며, 또 결합해야 합니다.

### 최상위 속성만 필터링 {#filter-top-level-properties-only}

현재 JCR 수준의 필터링은 최상위 조각에 대해서만 가능합니다.

필터가 중첩 조각의 필드를 처리하는 경우 AEM은 기본 모델을 공유하는 모든 조각을 (메모리에) 로드하는 것으로 폴백해야 합니다.

최상위 수준의 조각 필드 및 중첩된 조각 필드의 필터 표현식을 와 결합하여 이러한 GraphQL 쿼리를 최적화할 수 있습니다. [AND 연산자](#logical-operations-in-filter-expressions).

### 콘텐츠 구조 사용 {#use-content-structure}

AEM에서는 저장소 구조를 사용하여 처리할 컨텐츠의 범위를 좁히는 것이 좋습니다.

에서 필터를 적용하여 GraphQL 쿼리에 이 접근 방식을 적용합니다. `_path` 최상위 조각의 필드:

```graphql
{
  someList(filter: {
    _path: {
      _expressions: [ 
        {
          value: "/content/dam/some/sub/path/",
          _operator: STARTS_WITH
        }
      ]
    }
  }) {
    items {
      # ...
    }
  }
}
```

>[!NOTE]
>
>최고의 성능을 달성하려면 `value`에 후행 `/`가 필요합니다.

### 페이징 사용 {#use-paging}

페이징을 사용하여 초기 결과 세트를 줄일 수도 있습니다(특히 요청이 필터링 및 정렬을 사용하지 않는 경우).

중첩된 조각을 필터링하거나 정렬하는 경우 AEM에서 더 많은 양의 조각을 메모리에 로드해야 하므로 페이지가 매겨진 쿼리는 여전히 느릴 수 있습니다. 따라서 필터링과 페이징을 결합한다면 필터링 규칙(위에서 언급)을 고려하십시오.

페이징의 경우 페이지가 매겨진 결과가 명시적으로든 암시적으로든 항상 정렬되므로 정렬도 마찬가지로 중요합니다.

주로 처음 몇 페이지만 검색하는 데 관심이 있는 경우 `...List` 쿼리를 사용하는 것과 `...Paginated` 쿼리를 사용하는 것 사이에 크게 차이가 없습니다. 그러나 애플리케이션에서 단순히 한두 페이지가 아닌 그 이상의 페이지를 읽는 데 관심이 있는 경우 `...Paginated` 쿼리를 고려해야 합니다. 뒤쪽 페이지로 갈수록 성능이 확연히 향상되기 때문입니다.

### 필터 표현식의 논리 연산 {#logical-operations-in-filter-expressions}

중첩된 조각에서 필터링하는 경우 를 사용하여 결합되는 최상위 수준 필드에 관련 필터를 제공하여 JCR 필터링을 적용할 수 있습니다. `AND` 연산자.

일반적인 사용 사례는에서 필터를 사용하여 쿼리 범위를 제한하는 것입니다. `_path` 최상위 조각의 필드입니다. 그런 다음 최상위 수준이나 중첩된 조각에 있을 수 있는 추가 필드를 필터링합니다.

이 경우 서로 다른 필터 표현식이 `AND`와 결합됩니다. 따라서 `_path`에 대한 필터가 초기 결과 세트를 효과적으로 제한할 수 있습니다. 최상위 필드의 다른 모든 필터는 `AND`와 결합하기만 한다면 초기 결과 세트를 줄이는 데 도움이 될 수 있습니다.

`OR`과 결합된 필터 표현식은 중첩 조각이 관련된 경우 최적화할 수 없습니다. 다음과 같음 `OR` 표현식은 다음 경우에만 최적화할 수 있습니다. *아니요* 중첩된 조각이 포함됩니다.

### 여러 줄 텍스트 필드에 대한 필터링 방지 {#avoid-filtering-multiline-textfields}

여러 줄 텍스트 필드의 필드(html, markdown, plaintext, json)는 JCR 쿼리를 통해 필터링할 수 없습니다. 이러한 필드의 콘텐츠는 즉시 계산되어야 합니다.

여러 줄 텍스트 필드를 필터링해야 하는 경우 필터 표현식을 추가하여 초기 결과 세트의 크기를 제한하고 와 결합하십시오. `AND`. `_path` 필드에 대해 필터링하여 범위를 제한하는 것도 좋은 접근 방식입니다.

### 가상 필드에 대한 필터링 방지 {#avoid-filtering-virtual-fields}

가상 필드(`_`로 시작하는 대부분의 필드)는 GraphQL 쿼리가 실행되는 동안 계산되므로 JCR 기반 필터링 범위를 벗어납니다.

한 가지 중요한 예외는 `_path` 필드인데, 이 필드는 초기 결과 세트의 크기를 줄이는 데 효과적으로 사용할 수 있습니다. 단, 콘텐츠가 적절히 구조화되어 있어야 합니다([콘텐츠 구조 사용](#use-content-structure) 참조).

### 필터링: 제외 {#filtering-exclusions}

필터 표현식을 JCR 수준에서 평가할 수 없는 (따라서 최상의 성능을 달성하려면 피해야 하는) 몇 가지 다른 상황이 있습니다.

* `_sensitiveness` 필터 옵션을 사용하며 `_sensitiveness`가 `0.0`으로 설정되어 있지 않은 `Float` 값에 대한 필터 표현식.

* `_ignoreCase` 필터 옵션을 사용하는 `String` 값에 대한 필터 표현식.

* `null` 값에 대한 필터링.

* 배열에 대한 `_apply: ALL_OR_EMPTY` 사용 필터링.

* 배열에 대한 `_apply: INSTANCES`, `_instances: 0` 사용 필터링.

* `CONTAINS_NOT` 연산자를 사용한 필터 표현식.

* 다음에 대한 표현식 필터링 `Calendar`, `Date`, 또는 `Time` 를 사용하는 값 `NOT_AT` 연산자.
