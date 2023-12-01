---
title: GraphQL 쿼리 최적화
description: Headless 콘텐츠 전달을 위해 Adobe Experience Manager as a Cloud Service에서 콘텐츠 조각을 필터링, 페이징 및 정렬할 때 GraphQL 쿼리를 최적화하는 방법에 대해 알아봅니다.
exl-id: 47d0570b-224e-4109-b94e-ccc369d7ac5f
source-git-commit: 5e56441d2dc9b280547c91def8d971e7b1dfcfe3
workflow-type: tm+mt
source-wordcount: '1965'
ht-degree: 58%

---

# GraphQL 쿼리 최적화 {#optimizing-graphql-queries}

>[!NOTE]
>
>이러한 최적화 권장 사항을 적용하기 전에 다음을 고려하십시오 [GraphQL 필터링에서 페이징 및 정렬을 위한 콘텐츠 조각 업데이트](/help/sites-developing/headless/graphql-api/graphql-optimized-filtering-content-update.md) 최상의 성능을 제공합니다.

이 지침은 GraphQL 쿼리와 관련된 성능 문제를 방지하기 위해 제공됩니다.

## GraphQL 검사 목록 {#graphql-checklist}

다음 체크리스트는 Adobe Experience Manager(AEM as a Cloud Service)에서 GraphQL의 구성 및 사용을 최적화하는 데 도움이 되는 것입니다.

### 첫 번째 원칙 {#first-principles}

#### 지속 GraphQL 쿼리 사용 {#use-persisted-graphql-queries}

**추천**

지속 GraphQL 쿼리를 사용하는 것이 좋습니다.

지속 GraphQL 쿼리는 CDN(Content Delivery Network)을 활용하여 쿼리 실행 성능을 줄이는 데 도움이 됩니다. 클라이언트 애플리케이션은 빠른 에지 지원 실행을 위해 GET 요청과 함께 지속 쿼리를 요청합니다.

**추가 참조**

다음을 참조하십시오.

* [지속 GraphQL 쿼리](/help/sites-developing/headless/graphql-api/persisted-queries.md).
* [AEM을 통해 GraphQL을 사용하는 방법 알아보기 - 샘플 콘텐츠 및 쿼리](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md)

#### GraphQL 색인 패키지 설치 {#install-graphql-index-package}

**추천**

GraphQL을 사용하는 고객 *필수* GraphQL 색인 패키지를 사용하여 Experience Manager 콘텐츠 조각을 설치합니다. 이렇게 하면 필요한 인덱스 정의가 실제로 사용하는 기능을 기반으로 추가할 수 있습니다. 이 패키지를 설치하지 않으면 GraphQL 쿼리가 느려지거나 실패할 수 있습니다.

서비스 팩에 적합한 버전에 대한 릴리스 정보를 참조하십시오. 예를 들어 최신 서비스 팩의 경우 다음을 참조하십시오. [Experience Manager 콘텐츠 조각용 GraphQL 인덱스 패키지 설치](/help/release-notes/release-notes.md#install-aem-graphql-index-add-on-package) .

>[!NOTE]
>
>이 패키지는 인스턴스당 한 번만 설치하십시오. 모든 서비스 팩으로 다시 설치할 필요는 없습니다.

**추가 참조**
다음을 참조하십시오.

* [Experience Manager 콘텐츠 조각용 GraphQL 인덱스 패키지 설치](/help/release-notes/release-notes.md#install-aem-graphql-index-add-on-package)

### 캐시 전략 {#cache-strategy}

최적화를 위해 다양한 캐싱 방법을 사용할 수도 있습니다.

#### AEM Dispatcher 캐싱 활성화 {#enable-aem-dispatcher-caching}

**추천**

[AEM 디스패처](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html) 는 AEM 서비스 내에서 CDN 캐시 이전의 첫 번째 수준 캐시입니다.

**추가 참조**

다음을 참조하십시오.

* [GraphQL 지속 쿼리 - Dispatcher에서 캐싱 활성화](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#graphql-persisted-queries-enabling-caching-dispatcher)

#### CDN(Content Delivery Network) 사용 {#use-cdn}

**추천**

GraphQL 쿼리 및 해당 JSON 응답은 타깃팅한 경우 캐시될 수 있습니다. `GET` cdn 사용 시 요청. 반대로 캐시되지 않은 요청은 매우 (리소스) 비용이 많이 들고 처리 속도가 느릴 수 있으며, 이로 인해 원본 리소스에 추가 해로운 영향을 미칠 수 있습니다.

**추가 참조**

다음을 참조하십시오.

* [AEM에서 CDN 사용](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ko#using-dispatcher-with-a-cdn)

#### HTTP 캐시 제어 헤더 설정 {#set-http-cache-control-headers}

**추천**

CDN과 함께 지속 GraphQL 쿼리를 사용하는 경우 적절한 HTTP 캐시 제어 헤더를 설정하는 것이 좋습니다.

각 지속 쿼리에는 고유한 캐시 제어 헤더 집합이 있을 수 있습니다. 머리글은 다음에 대해 설정할 수 있습니다. [GRAPHQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md).

다음을 사용하여 설정할 수도 있습니다. **cURL** 명령줄 도구입니다. 예: `PUT` 캐시 제어를 사용하여 래핑된 일반 쿼리를 만들도록 요청합니다.

```shell
$ curl -X PUT \
    -H 'authorization: Basic YWRtaW46YWRtaW4=' \
    -H "Content-Type: application/json" \
    "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
    -d \
'{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
```

<!-- or the [AEM GraphiQL IDE](/help/sites-developing/headless/graphql-api/graphiql-ide.md#managing-cache). 
-->

**추가 참조**

다음을 참조하십시오.

* [지속 쿼리 캐싱](/help/sites-developing/headless/graphql-api/persisted-queries.md#caching-persisted-queries)
* [GraphQL 쿼리를 지속하는 방법](/help/sites-developing/headless/graphql-api/persisted-queries.md#how-to-persist-query)
<!--
* [Managing cache for your persisted queries](/help/sites-developing/headless/graphql-api/graphiql-ide.md#managing-cache)
-->

<!--
#### Use AEM GraphQL pre-caching {#use-aem-graphql-pre-caching}

**Recommendation**

This capability allows AEM to further cache content within the scope of GraphQL queries that can then be assembled as blocks in JSON output rather than line by line. 

**Further Reference**

Contact Adobe to enable this capability for your AEM Cloud Service program and environments. 
-->

### GraphQL 쿼리 최적화 {#graphql-query-optimization}

동일한 모델을 공유하는 콘텐츠 조각이 많은 AEM 인스턴스에서는 리소스 측면에서 GraphQL 목록 쿼리에 비용이 많이 들 수 있습니다.

GraphQL 쿼리 내에서 사용되는 모델을 공유하는 *모든* 조각은 메모리에 로드되어야 하기 때문입니다. 이때 시간과 메모리가 모두 소요됩니다. (최종) 결과 세트의 항목 수를 줄여 줄 수 있는 필터링은 전체 결과 세트를 메모리에 로드한 **후에만** 적용할 수 있습니다.

이 때문에 결과 세트가 작더라도 성능이 저하된다는 인상을 줄 수 있습니다. 그러나 실제로는 초기 결과 세트의 크기가 속도 저하의 원인입니다. 필터링 적용이 가능하기에 앞서 내부에서 초기 결과 세트를 처리해야 하기 때문입니다.

성능 및 메모리 문제를 줄이려면 이 초기 결과 세트를 최대한 작게 유지해야 합니다.

AEM은 GraphQL 쿼리를 최적화하는 데 2가지 접근 방식을 제공합니다.

* [하이브리드 필터링](#use-aem-graphql-hybrid-filtering)
* [페이징](#use-aem-graphql-pagination) (또는 페이지 매김)

   * [정렬](#use-graphql-sorting)은 최적화와 직접적인 관련은 없지만 페이징과 관련이 있음

각 접근 방식에는 독자적인 사용 사례와 제한 사항이 있습니다. 이 섹션에서는 하이브리드 필터링 및 페이징에 대한 정보와 함께 [우수 사례](#best-practices) GraphQL 쿼리 최적화에 사용됩니다.

#### AEM GraphQL 하이브리드 필터링 사용 {#use-aem-graphql-hybrid-filtering}

**추천**

하이브리드 필터링은 JCR 필터링과 AEM 필터링을 결합한 것입니다.

JCR 필터(쿼리 제한 형식)를 적용한 후에 AEM 필터링을 위해 결과 세트를 메모리에 로드합니다. 목적은 메모리에 로드되는 결과 세트를 줄이는 것으로, JCR 필터가 로드에 앞서 불필요한 결과를 제거해 주기 때문입니다.

>[!NOTE]
>
>기술적인 이유로(예: 유연성, 조각 중첩) AEM은 전체 필터링을 JCR에 위임할 수 없습니다.

이 기법에서는 GraphQL 필터의 유연성을 유지하면서 최대한 많은 필터링을 JCR에 위임합니다.

>[!NOTE]
>
>AEM 하이브리드 필터링을 사용하려면 기존 콘텐츠 조각을 업데이트해야 합니다

**추가 참조**

다음을 참조하십시오.

* [GraphQL 필터링에서 페이징 및 정렬을 위한 콘텐츠 조각 업데이트](/help/sites-developing/headless/graphql-api/graphql-optimized-filtering-content-update.md)
* [_태그 ID별로 필터링하고 변형을 제외하는 샘플 쿼리](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-filtering-tag-not-variations)

#### GraphQL 페이지 매김 사용 {#use-aem-graphql-pagination}

**추천**

GraphQL 표준인 페이지 매김을 사용하여 응답을 청크로 세분화함으로써, 결과 세트가 큰 복잡한 쿼리의 응답 시간을 향상시킬 수 있습니다.

AEM의 GraphQL은 두 가지 유형의 페이지 매김을 지원합니다.

* [limit/offset 기반 페이지 매김](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#list-offset-limit)
목록 쿼리에 사용되며 다음으로 끝납니다. `List`; 예, `articleList`.
이 페이지 매김을 사용하려면 반환할 첫 번째 항목의 위치(`offset`)와 반환할 항목 수(`limit` 또는 페이지 크기)를 제공해야 합니다.

* [커서 기반 페이지 매김](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#paginated-first-after)(`first` 및 `after`로 표시)
각 항목에 대한 고유 ID(커서라고도 함)를 제공합니다.
쿼리에서 사용자가 이전 페이지 마지막 항목의 커서와 페이지 크기(반환할 최대 항목 수)를 지정합니다.

  커서 기반 페이지 매김은 목록 기반 쿼리의 데이터 구조에 맞지 않기 때문에 AEM은 `Paginated` 쿼리 유형(예: `articlePaginated`)을 도입했습니다. 사용되는 데이터 구조 및 매개변수는 [GraphQL 커서 연결 사양](https://relay.dev/graphql/connections.htm)을 따릅니다.

  >[!NOTE]
  >
  >AEM은 현재 정방향 페이징(`after`/`first` 매개변수 사용)을 지원합니다.
  >
  >역방향 페이징(`before`/`last` 매개변수 사용)은 지원되지 않습니다.

**추가 참조**

다음을 참조하십시오.

* [첫 번째 및 그 다음 페이지를 사용하는 샘플 페이지 매김 쿼리](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-pagination-first-after)

#### GraphQL 정렬 사용 {#use-graphql-sorting}

**추천**

또한 GraphQL 표준인 정렬을 통해 클라이언트는 정렬된 순서대로 JSON 콘텐츠를 수신할 수 있습니다. 이를 통해 클라이언트에 대한 추가 처리 필요성을 줄일 수 있습니다.

정렬은 모든 정렬 기준이 최상위 조각과 관련된 경우에만 효율적입니다.

중첩 조각에 있는 필드가 정렬 순서에 하나 이상 포함되어 있으면 최상위 모델을 공유하는 모든 조각을 메모리에 로드해야 합니다. 이때 성능에 부정적인 영향이 미칠 수 있습니다.

>[!NOTE]
>
>최상위 필드에 대한 정렬도 (크지는 않지만) 성능에 영향을 미칩니다.

**추가 참조**

다음을 참조하십시오.

* [태그 ID별로 필터링하고 변형을 제외한 샘플 쿼리 및 이름별 정렬](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-filtering-tag-not-variations)

## 모범 사례 {#best-practices}

모든 최적화 권장 사항의 주요 목표는 초기 결과 세트를 줄이는 것입니다. 아래에 나열된 모범 사례는 그 방법을 소개합니다. 모범 사례는 결합할 수 있으며, 또 결합해야 합니다.

### 최상위 속성만 필터링 {#filter-top-level-properties-only}

현재 JCR 수준의 필터링은 최상위 조각에 대해서만 가능합니다.

필터가 중첩 조각의 필드를 처리하는 경우 AEM은 기본 모델을 공유하는 모든 조각을 (메모리에) 로드하는 것으로 폴백해야 합니다.

다만 [AND 연산자](#logical-operations-in-filter-expressions)로 최상위 조각의 필드에 대한 필터 표현식과 중첩된 조각의 필드에 대한 필터 표현식을 결합하여 그러한 GraphQL 쿼리를 최적화할 수 있습니다.

### 콘텐츠 구조 사용 {#use-content-structure}

AEM에서는 일반적으로 저장소 구조를 사용하여 처리할 콘텐츠의 범위를 좁히는 것이 모범 사례로 간주됩니다.

GraphQL 쿼리에도 이 접근 방식을 적용해야 합니다.

이를 위해서는 최상위 조각의 `_path` 필드에 필터를 적용하면 됩니다.

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

중첩된 조각을 필터링하거나 정렬하는 경우 AEM이 여전히 더 많은 양의 조각을 메모리에 로드해야 할 수 있으므로 페이지가 매겨진 쿼리가 여전히 느릴 수 있습니다. 따라서 필터링과 페이징을 결합한다면 필터링 규칙(위에서 언급)을 고려하십시오.

페이징의 경우 페이지가 매겨진 결과가 명시적으로든 암시적으로든 항상 정렬되므로 정렬도 마찬가지로 중요합니다.

주로 처음 몇 페이지만 검색하는 데 관심이 있는 경우 `...List` 쿼리를 사용하는 것과 `...Paginated` 쿼리를 사용하는 것 사이에 크게 차이가 없습니다. 그러나 애플리케이션에서 단순히 한두 페이지가 아닌 그 이상의 페이지를 읽는 데 관심이 있는 경우 `...Paginated` 쿼리를 고려해야 합니다. 뒤쪽 페이지로 갈수록 성능이 확연히 향상되기 때문입니다.

### 필터 표현식의 논리 연산 {#logical-operations-in-filter-expressions}

중첩 조각을 필터링하는 경우 `AND` 연산자를 사용하여 결합된 최상위 필드에 동반 필터를 제공하여 JCR 필터링을 계속 적용할 수 있습니다.

일반적인 사용 사례는 최상위 수준 조각의 `_path` 필드에 필터를 사용하여 쿼리 범위를 제한한 다음 최상위 수준 또는 중첩된 조각에 있을 수 있는 추가 필드를 필터링하는 것입니다.

이 경우 서로 다른 필터 표현식이 `AND`와 결합됩니다. 따라서 `_path`에 대한 필터가 초기 결과 세트를 효과적으로 제한할 수 있습니다. 최상위 필드의 다른 모든 필터는 `AND`와 결합하기만 한다면 초기 결과 세트를 줄이는 데 도움이 될 수 있습니다.

`OR`과 결합된 필터 표현식은 중첩 조각이 관련된 경우 최적화할 수 없습니다. `OR` 표현식은 관련된 중첩 조각이 *없을* 때만 최적화할 수 있습니다.

### 여러 줄 텍스트 필드에 대한 필터링 방지 {#avoid-filtering-multiline-textfields}

여러 줄 텍스트 필드(html, 마크다운, 일반 텍스트, json)의 필드는 JCR 쿼리를 통해 필터링할 수 없습니다. 이러한 필드의 내용은 즉시 계산되어야 하기 때문입니다.

여전히 여러 줄 텍스트 필드에서 필터링해야 하는 경우 추가 필터 표현식을 추가하고 이를 `AND`와 결합하여 초기 결과 세트의 크기를 제한하는 것을 고려하십시오. `_path` 필드에 대해 필터링하여 범위를 제한하는 것도 좋은 접근 방식입니다.

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

* `NOT_AT` 연산자를 사용하는 `Calendar`, `Date` 또는 `Time` 값에 대한 필터 표현식.

### 콘텐츠 조각 중첩 최소화 {#minimize-content-fragment-nesting}

콘텐츠 조각 중첩은 사용자 지정 콘텐츠 구조를 모델링하는 좋은 방법입니다. 중첩된 조각이 있고, ... 등이 있는 중첩된 조각이 있는 조각을 가질 수도 있습니다.

그러나 GraphQL이 중첩된 모든 콘텐츠 조각의 전체 계층 구조를 통과해야 하므로 수준이 너무 많은 구조를 만들면 GraphQL 쿼리의 처리 시간이 늘어날 수 있습니다.

딥중첩은 콘텐츠 거버넌스에 악영향을 줄 수도 있습니다. 일반적으로 콘텐츠 조각 중첩을 5개 또는 6개 수준 이하로 제한하는 것이 좋습니다.

### 모든 형식 출력 안 함(여러 줄 텍스트 요소) {#do-not-output-all-formats}

AEM GraphQL은 다음에서 작성된 텍스트를 반환할 수 있습니다. **[여러 줄 텍스트](/help/assets/content-fragments/content-fragments-models.md#data-types)** 데이터 유형(리치 텍스트, 단순 텍스트 및 Markdown 등 다양한 형식).

세 형식을 모두 출력하면 JSON의 텍스트 출력 크기가 3배율로 증가합니다. 따라서 매우 광범위한 쿼리의 일반적으로 큰 결과 세트와 함께 매우 큰 JSON 응답을 생성할 수 있으므로 계산하는 데 시간이 오래 걸립니다. 콘텐츠를 렌더링하는 데 필요한 텍스트 형식으로만 출력을 제한하는 것이 좋습니다.

### 컨텐츠 조각 수정 {#modifying-content-fragments}

AEM UI 또는 API를 사용하여 콘텐츠 조각 및 해당 리소스만 수정합니다. JCR에서 직접 수정하지 마십시오.

### 쿼리 테스트 {#test-your-queries}

GraphQL 쿼리 처리는 검색 쿼리 처리와 유사하며 단순한 GET 전체 컨텐츠 API 요청보다 훨씬 더 복잡합니다.

제어된 비프로덕션 환경에서 쿼리를 신중하게 계획, 테스트 및 최적화하는 것은 프로덕션에서 사용할 때 추후 성공을 위한 핵심입니다.
