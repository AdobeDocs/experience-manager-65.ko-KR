---
title: Query Builder API
seo-title: 쿼리 빌더 API
description: 자산 공유 쿼리 빌더의 기능은 Java API 및 REST API를 통해 노출됩니다.
seo-description: 자산 공유 쿼리 빌더의 기능은 Java API 및 REST API를 통해 노출됩니다.
uuid: 6928c3e9-96a1-44ad-9785-350d95f1869a
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 7965b7ef-dec4-441a-a012-daf1d60df0fb
pagetitle: Query Builder API
tagskeywords: querybuilder
translation-type: tm+mt
source-git-commit: a491d4e9bd9ffc68c4ba7cac3149f48cf7576ee8
workflow-type: tm+mt
source-wordcount: '2350'
ht-degree: 0%

---


# Query Builder API{#query-builder-api}

[자산 공유 쿼리 빌더](/help/assets/assets-finder-editor.md)의 기능은 Java API 및 REST API를 통해 노출됩니다. 이 섹션에서는 이러한 API에 대해 설명합니다.

서버측 쿼리 빌더( [`QueryBuilder`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html))는 쿼리 설명을 수락하고, XPath 쿼리를 만들어 실행하고, 선택적으로 결과 세트를 필터링하고, 필요한 경우 패싯을 추출합니다.

쿼리 설명은 단순히 예측자 집합([`Predicate`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/Predicate.html))입니다. 예에는 XPath의 `jcr:contains()` 함수에 해당하는 전체 텍스트 술어가 포함됩니다.

각 조건자 유형에 대해 XPath, 필터링 및 패싯 추출에 대한 특정 조건자를 처리하는 방법을 알고 있는 평가기 구성 요소([`PredicateEvaluator`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html))가 있습니다. OSGi 구성 요소 런타임을 통해 연결되는 사용자 정의 평가기를 만드는 것은 매우 쉽습니다.

REST API는 JSON에서 전송되는 응답과 함께 HTTP를 통해 정확히 동일한 기능에 대한 액세스 권한을 제공합니다.

>[!NOTE]
>
>QueryBuilder API는 JCR API를 사용하여 빌드됩니다. OSGi 번들 내에서 JCR API를 사용하여 Adobe Experience Manager JCR을 쿼리할 수도 있습니다. 자세한 내용은 [JCR API](https://helpx.adobe.com/experience-manager/using/querying-experience-manager-data-using1.html)를 사용하여 Adobe Experience Manager 데이터 쿼리를 참조하십시오.

## Gem 세션 {#gem-session}

[AEM ](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-index.html) Gemsis는 Adobe 전문가가 전달하는 Adobe Experience Manager에 대한 일련의 기술 심층 잠입을 말합니다. 쿼리 빌더 전용 이 세션은 도구를 개요 및 사용하는 데 매우 유용합니다.

>[!NOTE]
>
>쿼리 빌더에 대한 자세한 개요는 AEM Gem 세션 [AEM QueryBuilder](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-search-forms-using-querybuilder.html)에서 손쉽게 만든 검색 양식을 참조하십시오.

## 샘플 쿼리 {#sample-queries}

이러한 샘플은 Java 속성 스타일 표기법으로 제공됩니다. Java API와 함께 사용하려면 다음에 나오는 API 샘플에서와 같이 Java `HashMap`을 사용하십시오.

`QueryBuilder` JSON 서블릿의 경우, 각 예제는 로컬 CQ 설치(기본 위치: `http://localhost:4502`)에 대한 링크를 포함합니다. 이러한 링크를 사용하려면 먼저 CQ 인스턴스에 로그인해야 합니다.

>[!CAUTION]
>
>기본적으로 쿼리 빌더 json 서블릿은 최대 10개의 히트를 표시합니다.
>
>다음 매개 변수를 추가하면 서블릿이 모든 쿼리 결과를 표시할 수 있습니다.
>
>**`p.limit=-1`**

>[!NOTE]
>
>브라우저에서 반환된 JSON 데이터를 보려면 Firefox용 JSONView와 같은 플러그인을 사용해야 합니다.

### 모든 결과 반환{#returning-all-results}

다음 쿼리는 **10개의 결과**&#x200B;를 반환하지만(또는 최대 10개의 히트 수를 정해서) 실제로 사용할 수 있는 **히트 수를 알려줍니다.**

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=foundation/components/text
1_property.operation=like
orderby=path
```

동일한 쿼리(매개 변수 `p.limit=-1` 포함)가 **모든 결과**&#x200B;를 반환합니다(인스턴스에 따라 높은 숫자가 될 수 있음).

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.limit=-1&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=foundation/components/text
1_property.operation=like
p.limit=-1
orderby=path
```

### p.guessTotal을 사용하여 결과 {#using-p-guesstotal-to-return-the-results} 반환

`p.guessTotal` 매개 변수의 목적은 최소 실행 가능한 p.offset 및 p.limit 값을 결합하여 표시할 수 있는 적절한 수의 결과를 반환하는 것입니다. 이 매개 변수를 사용하면 큰 결과 집합에서 성능이 개선됩니다. 따라서 전체 합계(예: result.getSize() 호출) 계산 및 OAK 엔진 및 색인까지 최적화되고 전체 결과 집합 읽기를 피합니다. 실행 시간 및 메모리 사용량 모두 10만 개의 결과가 있을 경우 이 차이가 크게 날 수 있습니다.

매개 변수에 대한 단점은 사용자가 정확한 합계를 보지 못한다는 것입니다. 그러나 p.guessTotal=1000과 같은 최소 수를 설정할 수 있으므로 항상 최대 1000까지 읽을 수 있으므로 더 작은 결과 집합에 대한 정확한 합계를 얻을 수 있지만 더 큰 경우 &quot;and more&quot;만 표시할 수 있습니다.

아래 쿼리에 `p.guessTotal=true`을(를) 추가하여 어떻게 작동하는지 확인합니다.

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.guessTotal=true&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=foundation/components/text
1_property.operation=like
p.guessTotal=true
orderby=path
```

쿼리는 `0` 오프셋이 있는 `10` 결과의 `p.limit` 기본값을 반환합니다.

```xml
"success": true,
"results": 10,
"total": 10,
"more": true,
"offset": 0,
```

AEM 6.0 SP2의 경우 숫자 값을 사용하여 최대 사용자 지정 최대 결과 수를 계산할 수도 있습니다. 위와 동일한 쿼리를 사용하지만 `p.guessTotal`의 값을 `50`으로 변경하십시오.

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.guessTotal=50&orderby=path`

이 오퍼는 오프셋이 0인 동일한 기본값 제한 10을 반환하지만 최대 50개의 결과만 표시합니다.

```xml
"success": true,
"results": 10,
"total": 50,
"more": true,
"offset": 0,
```

### 페이지 매김 구현 {#implementing-pagination}

기본적으로 쿼리 빌더는 히트 수도 제공합니다. 결과 크기에 따라 정확한 카운트를 결정하려면 액세스 제어를 위해 모든 결과를 확인하는 데 시간이 오래 걸릴 수 있습니다. 대부분 합계는 최종 사용자 UI에 대한 페이지 매김을 구현하는 데 사용됩니다. 정확한 수를 결정할 때 페이지 매김을 구현하려면 guessTotal 기능을 사용하는 것이 좋습니다.

예를 들어 UI는 다음 방법을 적용할 수 있습니다.

* 총 히트 수([SearchResult.getTotalMatches()](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/result/SearchResult.html#gettotalmatches) 또는 total in the querybuilder.json response)가 100개 미만이거나 같습니다.
* 쿼리 빌더를 호출하는 동안 `guessTotal`을 100으로 설정합니다.

* 응답에는 다음 결과가 있을 수 있습니다.

   * `total=43`,  `more=false` - 총 히트 수가 43개임을 나타냅니다. UI는 첫 번째 페이지의 일부로 최대 10개의 결과를 표시할 수 있으며 다음 세 페이지에 대한 페이지 매김을 제공합니다. 또한 이 구현을 사용하여 **&quot;43 results found&quot;**&#x200B;과 같은 설명 텍스트를 표시할 수도 있습니다.
   * `total=100`,  `more=true` - 총 히트 수가 100개 이상이고 정확한 수를 알 수 없음을 나타냅니다. UI는 첫 번째 페이지의 일부로 최대 10개까지 표시할 수 있으며 다음 10페이지에 대한 페이지 매김을 제공합니다. 이 항목을 사용하여 **&quot;100개 이상의 결과 발견&quot;**&#x200B;과 같은 텍스트를 표시할 수도 있습니다. 사용자가 Query Builder에 대한 다음 페이지 호출로 이동할 때 `guessTotal` 및 `offset` 및 `limit` 매개 변수의 제한이 증가합니다.

`guessTotal` 쿼리 빌더가 정확한 히트 수를 확인하지 않도록 UI에서 무한 스크롤을 사용해야 하는 경우에도 사용해야 합니다.

### jar 파일을 찾아 최신 {#find-jar-files-and-order-them-newest-first} 순으로 정렬합니다.

`http://localhost:4502/bin/querybuilder.json?type=nt:file&nodename=*.jar&orderby=@jcr:content/jcr:lastModified&orderby.sort=desc`

```xml
type=nt:file
nodename=*.jar
orderby=@jcr:content/jcr:lastModified
orderby.sort=desc
```

### 모든 페이지를 찾아 마지막으로 수정한 {#find-all-pages-and-order-them-by-last-modified}까지 주문

`http://localhost:4502/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
```

### 모든 페이지를 찾아 마지막으로 수정한 후 내림차순 {#find-all-pages-and-order-them-by-last-modified-but-descending}

`http://localhost:4502/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified&orderby.sort=desc]`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
orderby.sort=desc
```

### 전체 텍스트 검색, 점수 {#fulltext-search-ordered-by-score} 순

`http://localhost:4502/bin/querybuilder.json?fulltext=Management&orderby=@jcr:score&orderby.sort=desc`

```xml
fulltext=Management
orderby=@jcr:score
orderby.sort=desc
```

### 특정 태그가 지정된 페이지 검색{#search-for-pages-tagged-with-a-certain-tag}

&#39;http://localhost:4502/bin/querybuilder.json?type=cq:Page&amp;tagid=marketing:interest/product&amp;tagid.property=jcr:content/cq:tags&#39;

```xml
type=cq:Page
tagid=marketing:interest/product
tagid.property=jcr:content/cq:tags
```

명시적 태그 ID를 알고 있는 경우 예제와 같이 `tagid` 조건자를 사용하십시오.

태그 제목 경로(공백 없이)에 `tag` 조건자를 사용하십시오.

이전 예제에서 페이지( `cq:Page` 노드)를 검색하고 있으므로 해당 노드의 상대 경로를 `tagid.property` 조건자(`jcr:content/cq:tags`)에 사용해야 합니다. 기본적으로 `tagid.property`은(는) 단순히 `cq:tags`입니다.

### 여러 경로(그룹 사용) {#search-under-multiple-paths-using-groups} 아래에서 검색

`http://localhost:4502/bin/querybuilder.json?fulltext=Management&group.1_path=/content/geometrixx/en/company/management&group.2_path=/content/geometrixx/en/company/bod&group.p.or=true`

```xml
fulltext=Management
group.p.or=true
group.1_path=/content/geometrixx/en/company/management
group.2_path=/content/geometrixx/en/company/bod
```

이 쿼리는 더 많은 표준 표기법에서 괄호 안의 경우와 마찬가지로 쿼리 내에서 하위 표현식을 구분하는 데 사용되는 *group*(&quot; `group`&quot;)을 사용합니다. 예를 들어, 이전 쿼리는 다음과 같이 보다 친숙한 스타일로 표시될 수 있습니다.

`"Management" and ("/content/geometrixx/en/company/management" or "/content/geometrixx/en/company/bod")`

예제의 그룹 내부에서 `path` 조건자가 여러 번 사용됩니다. 조건자의 두 인스턴스를 구분하고 순서를 지정하려면(일부 예측자의 경우 순서가 필요), 조건자 앞에 *N* `_ where`*N*&#x200B;이(가) 순서 색인으로 접두사를 붙여야 합니다. 이전 예에서 결과 예측자는 `1_path` 및 `2_path`입니다.

`p.or`의 `p`은 다음 사항(이 경우 `or`)이 `1_path`와 같은 그룹의 하위 술어가 아닌 그룹의 *매개 변수*&#x200B;임을 나타내는 특수 구분 기호입니다.

`p.or`이(가) 주어지지 않으면 모든 예측자가 함께 ANDed가 됩니다. 즉, 각 결과는 모든 예측자를 만족시켜야 합니다.

>[!NOTE]
>
>하나의 쿼리에 동일한 숫자 접두사를 사용할 수 없으며 서로 다른 예측자에 대해서도 사용할 수 없습니다.

### 속성 검색 {#search-for-properties}

여기서 `cq:template` 속성을 사용하여 지정된 템플릿의 모든 페이지를 검색합니다.

`http://localhost:4502/bin/querybuilder.json?property=cq%3atemplate&property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&type=cq%3aPageContent`

```xml
type=cq:PageContent
property=cq:template
property.value=/apps/geometrixx/templates/homepage
```

페이지 자체가 아닌 페이지의 `jcr:content` 노드가 반환되는 단점이 있습니다. 이 문제를 해결하려면 상대 경로로 검색할 수 있습니다.

`http://localhost:4502/bin/querybuilder.json?property=jcr%3acontent%2fcq%3atemplate&property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&type=cq%3aPage`

```xml
type=cq:Page
property=jcr:content/cq:template
property.value=/apps/geometrixx/templates/homepage
```

### 여러 속성 {#search-for-multiple-properties} 검색

속성 조건자를 여러 번 사용할 때는 번호 접두사를 다시 추가해야 합니다.

`http://localhost:4502/bin/querybuilder.json?1_property=jcr%3acontent%2fcq%3atemplate&1_property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&2_property=jcr%3acontent%2fjcr%3atitle&2_property.value=English&type=cq%3aPage`

```xml
type=cq:Page
1_property=jcr:content/cq:template
1_property.value=/apps/geometrixx/templates/homepage
2_property=jcr:content/jcr:title
2_property.value=English
```

### 여러 속성 값 {#search-for-multiple-property-values} 검색

속성( `"A" or "B" or "C"`)의 여러 값을 검색할 때 큰 그룹을 피하려면 `property` 조건자에 여러 값을 제공할 수 있습니다.

`http://localhost:4502/bin/querybuilder.json?property=jcr%3atitle&property.1_value=Products&property.2_value=Square&property.3_value=Events`

```xml
property=jcr:title
property.1_value=Products
property.2_value=Square
property.3_value=Events
```

다중 값 속성의 경우 여러 값이 일치해야 합니다( `"A" and "B" and "C"`).

`http://localhost:4502/bin/querybuilder.json?property=jcr%3atitle&property.and=true&property.1_value=test&property.2_value=foo&property.3_value=bar`

```xml
property=jcr:title
property.and=true
property.1_value=test
property.2_value=foo
property.3_value=bar
```

## 반환되는 항목 수정 {#refining-what-is-returned}

기본적으로 QueryBuilder JSON 서블릿은 검색 결과의 각 노드에 대한 기본 속성 세트를 반환합니다(예: 경로, 이름, 제목 등). 반환되는 속성을 제어하려면 다음 중 하나를 수행할 수 있습니다.

지정

```
p.hits=full
```

이 경우 각 노드에 대해 모든 속성이 포함됩니다.

`http://localhost:4502/bin/querybuilder.json?p.hits=full&property=jcr%3atitle&property.value=Triangle`

```xml
property=jcr:title
property.value=Triangle
p.hits=full
```

사용

```
p.hits=selective
```

및 가져올 속성을 지정합니다.

```
p.properties
```

공백으로 구분:

`http://localhost:4502/bin/querybuilder.json?p.hits=selective&property=jcr%3atitle&property.value=Triangle`

[ `http://localhost:4502/bin/querybuilder.json?`](http://localhost:4502/bin/querybuilder.json?p.hits=selective&amp;p.properties=sling%3aresourceType%20jcr%3aprimaryType&amp;property=jcr%3atitle&amp;property.value=Triangle) [p.hits=selective&amp;](http://localhost:4502/bin/querybuilder.json?p.hits=selective&amp;p.nodedepth=5&amp;p.properties=sling%3aresourceType%20jcr%3apath&amp;property=jcr%3atitle&amp;property.value=Triangle)p.properties=sling%3aresourceType%20jcr%3aprimaryType&amp;property=jcr%3atitle&amp;property.value=triangle

```xml
property=jcr:title
property.value=Triangle
p.hits=selective
p.properties=sling:resourceType jcr:primaryType
```

QueryBuilder 응답에 하위 노드를 포함할 수도 있습니다. 이렇게 하려면

```
p.nodedepth=n
```

여기서 `n`은 쿼리를 반환할 수준 수입니다. 하위 노드를 반환하려면 속성 선택기로 지정해야 합니다

```
p.hits=full
```

예:

`http://localhost:4502/bin/querybuilder.json?p.hits=full&p.nodedepth=5&property=jcr%3atitle&property.value=Triangle`

```xml
property=jcr:title
property.value=Triangle
p.hits=full
p.nodedepth=5
```

## 추가 설명 {#morepredicates}

추가 설명을 보려면 [쿼리 빌더 설명 참조 페이지](/help/sites-developing/querybuilder-predicate-reference.md)를 참조하십시오.

[Javadoc에서 `PredicateEvaluator` 클래스](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html)를 확인할 수도 있습니다. 이러한 클래스에 대한 Java에는 사용할 수 있는 속성 목록이 포함되어 있습니다.

클래스 이름의 접두사(예: [`SimilarityPredicateEvaluator`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/SimilarityPredicateEvaluator.html)의 &quot; `similar`&quot;)는 클래스의 *principal property*&#x200B;입니다. 이 속성은 쿼리에 사용할 술어의 이름이기도 합니다(소문자).

이러한 주체 속성의 경우 쿼리를 줄이고 정규화된 변형 &quot; `similar.similar=/content/en`&quot; 대신 &quot; `similar=/content/en`&quot;을 사용할 수 있습니다. 정규화된 양식은 클래스의 모든 비주체 속성에 사용해야 합니다.

## 쿼리 빌더 API 사용 예 {#example-query-builder-api-usage}

```java
   String fulltextSearchTerm = "Geometrixx";

    // create query description as hash map (simplest way, same as form post)
    Map<String, String> map = new HashMap<String, String>();

// create query description as hash map (simplest way, same as form post)
    map.put("path", "/content");
    map.put("type", "cq:Page");
    map.put("group.p.or", "true"); // combine this group with OR
    map.put("group.1_fulltext", fulltextSearchTerm);
    map.put("group.1_fulltext.relPath", "jcr:content");
    map.put("group.2_fulltext", fulltextSearchTerm);
    map.put("group.2_fulltext.relPath", "jcr:content/@cq:tags");

    // can be done in map or with Query methods
    map.put("p.offset", "0"); // same as query.setStart(0) below
    map.put("p.limit", "20"); // same as query.setHitsPerPage(20) below

    Query query = builder.createQuery(PredicateGroup.create(map), session);
    query.setStart(0);
    query.setHitsPerPage(20);

    SearchResult result = query.getResult();

    // paging metadata
    int hitsPerPage = result.getHits().size(); // 20 (set above) or lower
    long totalMatches = result.getTotalMatches();
    long offset = result.getStartIndex();
    long numberOfPages = totalMatches / 20;

    //Place the results in XML to return to client
    DocumentBuilderFactory factory =     DocumentBuilderFactory.newInstance();
    DocumentBuilder builder = factory.newDocumentBuilder();
    Document doc = builder.newDocument();

    //Start building the XML to pass back to the AEM client
    Element root = doc.createElement( "results" );
    doc.appendChild( root );

    // iterating over the results
    for (Hit hit : result.getHits()) {
       String path = hit.getPath();

      //Create a result element
      Element resultel = doc.createElement( "result" );
      root.appendChild( resultel );

      Element pathel = doc.createElement( "path" );
      pathel.appendChild( doc.createTextNode(path ) );
      resultel.appendChild( pathel );
    }
```

>[!NOTE]
>
>QueryBuilder API를 사용하고 해당 OSGi 번들을 Adobe Experience Manager 애플리케이션 내에서 사용하는 OSGi 번들을 사용하는 방법에 대해 알아보려면 쿼리 빌더 AP[을 사용하는 Adobe CQ OSGi 번들 만들기를 참조하십시오.](https://helpx.adobe.com/experience-manager/using/using-query-builder-api.html)

JSON(Query Builder) 서블릿을 사용하여 HTTP를 통해 실행되는 동일한 쿼리:

`http://localhost:4502/bin/querybuilder.json?path=/content&type=cq:Page&group.p.or=true&group.1_fulltext=Geometrixx&group.1_fulltext.relPath=jcr:content&group.2_fulltext=Geometrixx&group.2_fulltext.relPath=jcr:content/@cq:tags&p.offset=0&p.limit=20`

## 쿼리 저장 및 로드 {#storing-and-loading-queries}

나중에 사용할 수 있도록 쿼리를 저장소에 저장할 수 있습니다. `QueryBuilder`은 다음 서명을 사용하여 &quot;`storeQuery` 메서드를 제공합니다.

```java
void storeQuery(Query query, String path, boolean createFile, Session session) throws RepositoryException, IOException;
```

[ `QueryBuilder#storeQuery`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html#storequerycomdaycqsearchqueryjavalangstringbooleanjavaxjcrsession) 메서드를 사용할 때 주어진 `Query`이 파일 또는 `createFile` 인수 값에 따라 저장소로 저장됩니다. 다음 예제에서는 `Query` 경로를 파일로 저장하는 방법을 보여 줍니다.`/mypath/getfiles`

```java
builder.storeQuery(query, "/mypath/getfiles", true, session);
```

이전에 저장한 모든 쿼리는 [`QueryBuilder#loadQuery`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html#loadqueryjavalangstringjavaxjcrsession) 메서드를 사용하여 저장소에서 로드할 수 있습니다.

```java
Query loadQuery(String path, Session session) throws RepositoryException, IOException
```

예를 들어 다음 코드 조각에서 `/mypath/getfiles` 경로에 저장된 `Query`을 로드할 수 있습니다.

```java
Query loadedQuery = builder.loadQuery("/mypath/getfiles", session);
```

## 테스트 및 디버깅 {#testing-and-debugging}

QueryBuilder 쿼리를 재생하고 디버깅하려면

`http://localhost:4502/libs/cq/search/content/querydebug.html`

또는 다음 위치에서 querybuilder json 서블릿

`http://localhost:4502/bin/querybuilder.json?path=/tmp`

( `path=/tmp`은(는) 예일 뿐입니다.)

### 일반 디버깅 Recommendations {#general-debugging-recommendations}

### 로깅 {#obtain-explain-able-xpath-via-logging}을 통해 설명 가능한 XPath 받기

대상 인덱스 세트에 대해 개발 주기 동안 **모든** 쿼리를 설명하십시오.

* QueryBuilder에 대한 DEBUG 로그를 사용하여 설명 가능한 기본 XPath 쿼리를 얻을 수 있습니다.

   * https://&lt;serveraddress>:&lt;serverport>/system/console/slinglog로 이동합니다. **DEBUG**&#x200B;에서 `com.day.cq.search.impl.builder.QueryImpl`에 대한 새 로거를 만듭니다.

* 위의 클래스에 대해 DEBUG가 활성화되면 로그에 Query Builder에서 생성된 XPath가 표시됩니다.
* 연결된 QueryBuilder 쿼리의 로그 항목에서 XPath 쿼리를 복사합니다. 예:

   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "Geometrixx") or jcr:contains(jcr:content/@cq:tags, "Geometrixx"))]`

* XPath 쿼리를 [Explain Query](/help/sites-administering/operations-dashboard.md#explain-query)에 붙여 넣어 쿼리 계획을 확인합니다.

### Query Builder 디버거 {#obtain-explain-able-xpath-via-the-query-builder-debugger}를 통해 설명 가능한 XPath 가져오기

* AEM QueryBuilder 디버거를 사용하여 설명 가능한 XPath 쿼리를 생성합니다.

대상 인덱스 세트에 대해 개발 주기 동안 **모든** 쿼리를 설명하십시오.

**로깅(logging)을 통해 설명 가능한 XPath 받기**

* QueryBuilder에 대한 DEBUG 로그를 사용하여 설명 가능한 기본 XPath 쿼리를 얻을 수 있습니다.

   * https://&lt;serveraddress>:&lt;serverport>/system/console/slinglog로 이동합니다. **DEBUG**&#x200B;에서 `com.day.cq.search.impl.builder.QueryImpl`에 대한 새 로거를 만듭니다.

* 위의 클래스에 대해 DEBUG가 활성화되면 로그에 Query Builder에서 생성된 XPath가 표시됩니다.
* 연결된 QueryBuilder 쿼리의 로그 항목에서 XPath 쿼리를 복사합니다. 예:

   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "Geometrixx") or jcr:contains(jcr:content/@cq:tags, "Geometrixx"))]`

* 쿼리 계획을 얻으려면 XPath 쿼리를 [Explain Query](/help/sites-administering/operations-dashboard.md#explain-query)을 XPath로 붙여넣으십시오

**Query Builder 디버거를 통해 설명 가능한 XPath 가져오기**

* AEM QueryBuilder 디버거를 사용하여 설명 가능한 XPath 쿼리를 생성합니다.

![chlimage_1-66](assets/chlimage_1-66a.png)

1. 쿼리 빌더 디버거에 쿼리 빌더 쿼리 쿼리 제공
1. 검색 실행
1. 생성된 XPath 가져오기
1. 쿼리 계획을 얻으려면 XPath 쿼리를 XPath로 설명

>[!NOTE]
>
>쿼리 설명이 없는 빌더 쿼리(XPath, JCR-SQL2)는 쿼리 설명에 직접 제공할 수 있습니다.

QueryBuilder를 사용하여 쿼리를 디버깅하는 방법에 대한 자세한 내용은 아래 비디오를 참조하십시오.

>[!NOTE]
>
>[https://www.youtube.com/watch?v=BnyXjhRKYKc](https://www.youtube.com/watch?v=BnyXjhRKYKc)

## 로깅 {#debugging-queries-with-logging}을 사용하여 쿼리 디버깅

>[!NOTE]
>
>로거 구성은 [Creating Your Own Loggers and Writer](/help/sites-deploying/configure-logging.md#creating-your-own-loggers-and-writers) 섹션에 설명되어 있습니다.

테스트 및 디버깅에 설명된 쿼리를 실행할 때 쿼리 빌더 구현의 로그 출력(INFO 수준):

```xml
com.day.cq.search.impl.builder.QueryImpl executing query (predicate tree):
null=group: limit=20, offset=0[
    {group=group: or=true[
        {1_fulltext=fulltext: fulltext=Geometrixx, relPath=jcr:content}
        {2_fulltext=fulltext: fulltext=Geometrixx, relPath=jcr:content/@cq:tags}
    ]}
    {path=path: path=/content}
    {type=type: type=cq:Page}
]
com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "Geometrixx") or jcr:contains(jcr:content/@cq:tags, "Geometrixx"))]
com.day.cq.search.impl.builder.QueryImpl no filtering predicates
com.day.cq.search.impl.builder.QueryImpl query execution took 69 ms
```

비교자별로 사용자 지정 순서를 사용하는 조건자 평가자를 사용하는 쿼리가 있는 경우 이 쿼리는 쿼리에 기록됩니다.

```xml
com.day.cq.search.impl.builder.QueryImpl executing query (predicate tree):
null=group: [
    {nodename=nodename: nodename=*.jar}
    {orderby=orderby: orderby=@jcr:content/jcr:lastModified}
    {type=type: type=nt:file}
]
com.day.cq.search.impl.builder.QueryImpl custom order by comparator: jcr:content/jcr:lastModified
com.day.cq.search.impl.builder.QueryImpl XPath query: //element(*, nt:file)
com.day.cq.search.impl.builder.QueryImpl filtering predicates: {nodename=nodename: nodename=*.jar}
com.day.cq.search.impl.builder.QueryImpl query execution took 272 ms
```

## Javadoc 링크 {#javadoc-links}

| **Javadoc** | **설명** |
|---|---|
| [com.day.cq.search](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/package-summary.html) | 기본 QueryBuilder 및 쿼리 API |
| [com.day.cq.search.result](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/result/package-summary.html) | 결과 API |
| [com.day.cq.search.facets](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/package-summary.html) | 패싯 |
| [com.day.cq.search.facets.bucks](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/buckets/package-summary.html) | 버킷(패싯에 포함) |
| [com.day.cq.search.eval](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/package-summary.html) | 설명 평가자 |
| [com.day.cq.search.facets.extractor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/extractors/package-summary.html) | 패싯 추출기(평가자용) |
| [com.day.cq.search.writer](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/writer/package-summary.html) | QueryBuilder 서블릿용 JSON 결과 히트 기록기(/bin/querybuilder.json) |

