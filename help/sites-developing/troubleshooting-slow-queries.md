---
title: 느린 쿼리 문제 해결
description: Adobe Experience Manager에서 느린 쿼리 문제를 해결하는 방법을 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 3405cdd3-3d1b-414d-9931-b7d7b63f0a6f
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '2237'
ht-degree: 0%

---

# 느린 쿼리 문제 해결{#troubleshooting-slow-queries}

## 느린 쿼리 분류 {#slow-query-classifications}

AEM에는 심각도별로 나열되는 세 가지 주요 슬로우 쿼리 분류가 있습니다.

1. **인덱스 없는 쿼리**

   * **not**&#x200B;을(를) 수행하는 쿼리는 색인으로 확인되고 JCR 콘텐츠를 통과하여 결과를 수집합니다.

1. **쿼리 제한(또는 범위 지정)이 잘못됨**

   * 인덱스로 확인되지만 결과를 수집하려면 모든 인덱스 항목을 트래버스해야 하는 쿼리

1. **큰 결과 집합 쿼리**

   * 많은 결과를 반환하는 쿼리

처음 두 분류의 쿼리(색인 없는 쿼리와 제한 수준이 낮은 쿼리)가 느립니다. 이 오류는 Oak 쿼리 엔진이 각 **잠재적** 결과(콘텐츠 노드 또는 인덱스 항목)를 검사하여 **실제** 결과 집합에 속하는 항목을 식별하도록 하므로 느립니다.

각각의 잠재적 결과를 검사하는 행위는 트래버스라고 불리는 것이다.

각각의 잠재적 결과들은 검사되어야 하기 때문에, 실제 결과 세트를 결정하기 위한 비용은 잠재적 결과들의 수에 따라 선형적으로 성장한다.

쿼리 제한 및 조정 인덱스를 추가하면 인덱스 데이터를 최적화된 형식으로 저장하여 빠른 결과 검색을 수행할 수 있으며, 잠재적 결과 세트에 대한 선형 검사 필요성을 줄이거나 없앨 수 있습니다.

AEM 6.3에서는 기본적으로 100,000개 순회에 도달하면 쿼리가 실패하고 예외가 발생합니다. 이 제한은 기본적으로 AEM 6.3 이전의 AEM 버전에는 없지만 Apache Jackrabbit 쿼리 엔진 설정 OSGi 구성 및 QueryEngineSettings JMX 빈(속성 LimitReads)을 통해 설정할 수 있습니다.

### 인덱스 없는 쿼리 검색 {#detecting-index-less-queries}

#### 개발 중 {#during-development}

**모든** 쿼리를 설명하고 쿼리 계획에 **/&ast; traverse** 설명이 포함되어 있지 않은지 확인하십시오. 쿼리 계획 트래버스 예제:

* **계획:** `[nt:unstructured] as [a] /* traverse "/content//*" where ([a].[unindexedProperty] = 'some value') and (isdescendantnode([a], [/content])) */`

#### Post-배포 {#post-deployment}

* 인덱스 없는 순회 쿼리에 대해 `error.log` 모니터링:

   * `*INFO* org.apache.jackrabbit.oak.query.QueryImpl Traversal query (query without index) ... ; consider creating and index`
   * 이 메시지는 사용할 수 있는 색인이 없고 쿼리가 잠재적으로 많은 노드를 트래버스하는 경우에만 기록됩니다. 색인을 사용할 수 있으면 메시지가 기록되지 않지만 트래버스할 양이 작아서 빠릅니다.

* AEM [쿼리 성능](/help/sites-administering/operations-dashboard.md#query-performance) 작업 콘솔과 [설명](/help/sites-administering/operations-dashboard.md#explain-query) 느린 쿼리에서 순회 또는 색인 쿼리 설명을 찾을 수 없습니다.

### 잘못 제한된 쿼리 검색 {#detecting-poorly-restricted-queries}

#### 개발 중 {#during-development-1}

모든 쿼리를 설명하고 쿼리의 속성 제한 사항과 일치하도록 조정된 색인으로 확인되도록 합니다.

* 이상적인 쿼리 계획 범위에는 모든 속성 제한에 대해 `indexRules`이(가) 있으며 쿼리에서 가장 엄격한 속성 제한에 대해 최소한으로 사용합니다.
* 결과를 정렬하는 쿼리는 `orderable=true.`을(를) 설정하는 속성별로 정렬된 속성에 대한 인덱스 규칙을 사용하여 Lucene 속성 인덱스로 확인되어야 합니다.

#### 예를들어, 기본 `cqPageLucene`에 `jcr:content/cq:tags`에 대한 인덱스 규칙이 없습니다. {#for-example-the-default-cqpagelucene-does-not-have-an-index-rule-for-jcr-content-cq-tags}

cq:tags 인덱스 규칙을 추가하기 전에

* **cq:tags 인덱스 규칙**

   * 즉시 존재하지 않습니다.

* **쿼리 빌더 쿼리**

  ```js
  type=cq:Page
  property=jcr:content/cq:tags
  property.value=my:tag
  ```

* **쿼리 계획**

  `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) *:* where [a].[jcr:content/cq:tags] = 'my:tag' */`

이 쿼리는 `cqPageLucene` 인덱스로 확인되지만 `jcr:content` 또는 `cq:tags`에 대한 속성 인덱스 규칙이 없으므로 이 제한을 평가할 때 `cqPageLucene` 인덱스의 모든 레코드가 일치하는지 확인합니다. 따라서 인덱스에 100만 개의 `cq:Page` 노드가 포함되어 있으면 100만 개의 레코드를 확인하여 결과 세트를 결정합니다.

cq:tags 인덱스 규칙을 추가한 후

* **cq:tags 인덱스 규칙**

  ```js
  /oak:index/cqPageLucene/indexRules/cq:Page/properties/cqTags
  @name=jcr:content/cq:tags
  @propertyIndex=true
  ```

* **쿼리 빌더 쿼리**

  ```js
  type=cq:Page
  property=jcr:content/cq:tags
  property.value=myTagNamespace:myTag
  ```

* **쿼리 계획**

  `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) jcr:content/cq:tags:my:tag where [a].[jcr:content/cq:tags] = 'my:tag' */`

`cqPageLucene` 인덱스에 `jcr:content/cq:tags`에 대한 indexRule을 추가하면 `cq:tags` 데이터를 최적화된 방식으로 저장할 수 있습니다.

`jcr:content/cq:tags` 제한이 있는 쿼리가 수행되면 인덱스는 값별로 결과를 조회할 수 있습니다. 즉, 100개의 `cq:Page` 노드에 값으로 `myTagNamespace:myTag`이(가) 있는 경우 해당 100개의 결과만 반환되고 나머지 999,000개는 제한 검사에서 제외되어 성능이 10,000배 향상됩니다.

더 많은 쿼리 제한 사항이 적격한 결과 세트를 줄이고 쿼리 최적화를 추가로 최적화합니다.

마찬가지로 `cq:tags` 속성에 대한 추가 인덱스 규칙이 없으면 인덱스의 결과가 모든 전체 텍스트 일치 항목을 반환하므로 `cq:tags`에 제한이 있는 전체 텍스트 쿼리도 제대로 수행되지 않습니다. cq:tags에 대한 제한은 이후 필터링됩니다.

사후 인덱스 필터링의 또 다른 원인은 개발 중에 종종 누락되는 액세스 제어 목록입니다. 쿼리가 사용자가 액세스할 수 없는 경로를 반환하지 않는지 확인하십시오. 이렇게 하려면 쿼리에 대한 관련 경로 제한 사항을 제공할 뿐만 아니라 더 나은 콘텐츠 구조를 통해 수행할 수 있습니다.

Lucene 인덱스가 작은 하위 집합을 쿼리 결과로 반환하기 위해 많은 결과를 반환하는지 여부를 식별하는 유용한 방법은 `org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex`에 대해 DEBUG 로그를 활성화하는 것입니다. 이렇게 하면 색인에서 로드되는 문서 수를 볼 수 있습니다. 최종 결과 수와 로드된 문서 수가 불균형하게 바뀌어서는 안 됩니다. 자세한 내용은 [로깅](/help/sites-deploying/configure-logging.md)을 참조하십시오.

#### Post-배포 {#post-deployment-1}

* 순회 쿼리에 대해 `error.log`을(를) 모니터링합니다.

   * `*WARN* org.apache.jackrabbit.oak.spi.query.Cursors$TraversingCursor Traversed ### nodes ... consider creating an index or changing the query`

* AEM [쿼리 성능](/help/sites-administering/operations-dashboard.md#query-performance) 작업 콘솔과 [설명](/help/sites-administering/operations-dashboard.md#explain-query) 느린 쿼리에서 쿼리 속성 제한을 색인 속성 규칙으로 해결하지 않는 쿼리 계획을 찾습니다.

### 큰 결과 집합 쿼리 감지 {#detecting-large-result-set-queries}

#### 개발 중 {#during-development-2}

oak.queryLimitInMemory(예: 10000) 및 oak.queryLimitReads(예: 5000)에 대해 낮은 임계값을 설정하고, &quot;쿼리가 x개 이상의 노드를 읽음...&quot;이라는 UnsupportedOperationException이 발생할 때 값비싼 쿼리를 최적화합니다.

낮은 임계값을 설정하면 리소스 집약적인 쿼리(즉, 색인에서 지원하지 않거나 덜 포함되는 색인에서 지원하지 않음)를 방지하는 데 도움이 됩니다. 예를 들어, 100만 개의 노드를 읽는 쿼리는 많은 IO를 유발하고 전체 애플리케이션 성능에 부정적인 영향을 줍니다. 따라서 초과 제한으로 인해 실패한 모든 쿼리를 분석하고 최적화해야 합니다.

#### Post-배포 {#post-deployment-2}

* 큰 노드 트래버스 또는 큰 힙 메모리 소비를 트리거하는 쿼리에 대해 로그를 모니터링합니다.&quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * 트래버스된 노드 수를 줄이도록 쿼리를 최적화합니다.

* 대용량 힙 메모리 소비를 트리거하는 쿼리에 대한 로그 모니터링:

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * 힙 메모리 소비를 줄일 수 있도록 쿼리를 최적화합니다.

AEM 6.0 - 6.2 버전의 경우, AEM 시작 스크립트의 JVM 매개변수를 통해 노드 트래버스에 대한 임계값을 조정하여 큰 쿼리가 환경을 오버로드할 수 없도록 할 수 있습니다. 권장되는 값은 다음과 같습니다.

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

AEM 6.3에서 위의 두 매개 변수는 기본적으로 사전 구성되어 있으며 OSGi QueryEngineSettings를 통해 수정할 수 있습니다.

추가 정보는 [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)에서 확인할 수 있습니다.

## 쿼리 성능 조정 {#query-performance-tuning}

AEM에서 쿼리 성능 최적화의 모토는 다음과 같습니다.

**&quot;제한이 많을수록 좋습니다.&quot;**

다음은 쿼리 성능을 보장하기 위한 권장 조정 방법에 대해 설명합니다. 먼저 쿼리를 조정하십시오. 즉, 덜 간섭적인 활동을 수행한 다음, 필요한 경우 색인 정의를 조정하십시오.

### 쿼리 문 조정 {#adjusting-the-query-statement}

AEM은 다음 쿼리 언어를 지원합니다.

* QueryBuilder
* JCR-SQL2
* XPath

다음 예제에서는 AEM 개발자가 사용하는 가장 일반적인 쿼리 언어이지만 JCR-SQL2와 XPath에는 동일한 원칙이 적용되므로 Query Builder를 사용합니다.

1. 쿼리가 기존 Lucene 속성 인덱스로 확인되도록 노드 유형 제한을 추가합니다.

* **최적화되지 않은 쿼리**

  ```js
  property=jcr:content/contentType
  property.value=article-page
  ```

* **최적화된 쿼리**

  ```js
  type=cq:Page
  property=jcr:content/contentType
  property.value=article-page
  ```

  노드 유형 제한이 없는 쿼리는 AEM이 `nt:base` 노드 유형을 가정하도록 합니다. 이 노드 유형은 AEM의 모든 노드가 의 하위 유형이므로 사실상 노드 유형 제한이 없습니다.

  `type=cq:Page`을(를) 설정하면 이 쿼리가 `cq:Page` 노드로만 제한되고, AEM의 cqPageLucene으로 확인되어 AEM의 노드 하위 집합(`cq:Page` 노드만)으로 결과가 제한됩니다.

1. 쿼리가 기존 Lucene 속성 인덱스로 확인되도록 쿼리의 노드 유형 제한을 조정합니다.

* **최적화되지 않은 쿼리**

  ```js
  type=nt:hierarchyNode
  property=jcr:content/contentType
  property.value=article-page
  ```

* **최적화된 쿼리**

  ```js
  type=cq:Page
  property=jcr:content/contentType
  property.value=article-page
  ```

  `nt:hierarchyNode`은(는) `cq:Page`의 상위 노드 유형입니다. `jcr:content/contentType=article-page`이(가) Adobe의 사용자 지정 응용 프로그램을 통해 `cq:Page` 노드에만 적용된다고 가정할 경우 이 쿼리는 `jcr:content/contentType=article-page`인 `cq:Page` 노드만 반환합니다. 이 흐름은 다음과 같은 이유로 인해 차선의 제한 사항이 됩니다.

   * 다른 노드는 잠재적 결과 집합에 불필요하게 추가된 `nt:hierarchyNode`(예: `dam:Asset`)에서 상속합니다.
   * `nt:hierarchyNode`에 대해 AEM 제공 인덱스가 없지만 `cq:Page`에 대해 제공된 인덱스가 있습니다.

  `type=cq:Page`을(를) 설정하면 이 쿼리가 `cq:Page` 노드로만 제한되고 AEM의 cqPageLucene으로 확인되어 AEM의 노드 하위 집합(cq:Page 노드만)으로 결과가 제한됩니다.

1. 또는 쿼리가 기존 속성 색인으로 확인되도록 속성 제한을 조정합니다.

* **최적화되지 않은 쿼리**

  ```js
  property=jcr:content/contentType
  property.value=article-page
  ```

* **최적화된 쿼리**

  ```js
  property=jcr:content/sling:resourceType
  property.value=my-site/components/structure/article-page
  ```

  속성 제한을 `jcr:content/contentType`(사용자 지정 값)에서 잘 알려진 속성 `sling:resourceType`(으)로 변경하면 쿼리가 `sling:resourceType`에 의해 모든 콘텐츠를 인덱싱하는 속성 인덱스 `slingResourceType`(으)로 확인됩니다.

  속성 인덱스(Lucene 속성 인덱스 대신)는 쿼리가 노드 유형별로 식별되지 않을 때 가장 잘 사용되며, 단일 속성 제한이 결과 집합을 압도합니다.

1. 쿼리에 가능한 가장 엄격한 경로 제한을 추가합니다. 예를 들어 `/content/my-site`보다 `/content/my-site/us/en`을 선호하거나 `/`보다 `/content/dam`을 선호합니다.

* **최적화되지 않은 쿼리**

  ```js
  type=cq:Page
  path=/content
  property=jcr:content/contentType
  property.value=article-page
  ```

* **최적화된 쿼리**

  ```js
  type=cq:Page
  path=/content/my-site/us/en
  property=jcr:content/contentType
  property.value=article-page
  ```

  경로 제한을 `path=/content`에서 `path=/content/my-site/us/en`(으)로 범위 지정하면 검사해야 하는 인덱스 항목 수를 줄일 수 있습니다. 쿼리가 경로를 `/content` 또는 `/content/dam` 이상으로 잘 제한할 수 있는 경우 인덱스에 `evaluatePathRestrictions=true`이(가) 있는지 확인하십시오.

  `evaluatePathRestrictions`을(를) 사용하면 인덱스 크기가 증가합니다.

1. 가능하면 쿼리 함수 및 `LIKE` 및 `fn:XXXX`과(와) 같은 쿼리 작업은 제한 기반 결과 수에 따라 비용이 증가하므로 피하십시오.

* **최적화되지 않은 쿼리**

  ```js
  type=cq:Page
  property=jcr:content/contentType
  property.operation=like
  property.value=%article%
  ```

* **최적화된 쿼리**

  ```js
  type=cq:Page
  fulltext=article
  fulltext.relPath=jcr:content/contentType
  ```

  텍스트가 와일드카드(&quot;%...&#39;)로 시작하는 경우 인덱스를 사용할 수 없으므로 LIKE 조건은 평가하기에 느립니다. jcr:contains 조건은 전체 텍스트 인덱스를 사용할 수 있으므로 선호됩니다. `analayzed=true`이(가) 있는 `jcr:content/contentType`에 대해 확인된 Lucene 속성 인덱스에 indexRule이 있어야 합니다.

  `fn:lowercase(..)`과(와) 같은 쿼리 함수를 사용하면 더 빠른 등가물이 없으므로 최적화하는 것이 더 어려울 수 있습니다(더 복잡하고 비간섭적인 인덱스 분석기 구성 외부). 가능한 가장 작은 잠재적 결과 세트에서 함수가 작동해야 하는 전체 쿼리 성능을 개선하기 위해 다른 범위 제한을 식별하는 것이 가장 좋습니다.

1. ***이 조정은 Query Builder에만 적용되며 JCR-SQL2 또는 XPath에는 적용되지 않습니다.***

   전체 결과 집합이 바로 필요한 경우 [Query Builder guessTotal](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results)을 사용합니다&#x200B;**not**.

   * **최적화되지 않은 쿼리**

     ```js
     type=cq:Page
     path=/content
     ```

   * **최적화된 쿼리**

     ```js
     type=cq:Page
     path=/content
     p.guessTotal=100
     ```

   쿼리 실행은 빠르지만 결과 수가 많은 경우 `guessTotal`은(는) Query Builder 쿼리에 대한 중요한 최적화입니다.

   `p.guessTotal=100`은(는) Query Builder에 처음 100개의 결과만 수집하도록 지시합니다. 또한 하나 이상의 결과가 있는지(하지만 이 숫자를 카운트하면 속도가 느려지므로 더 많은 결과는 아님) 나타내는 부울 플래그를 설정합니다. 이 최적화는 결과 하위 집합만 점진적으로 표시되는 페이지 매김 또는 무한 로드 사용 사례에 적합합니다.

## 기존 인덱스 조정 {#existing-index-tuning}

1. 최적 쿼리가 속성 인덱스로 확인되는 경우 속성 인덱스가 최소한으로 조정할 수 있으므로 수행할 작업이 없습니다.
1. 그렇지 않으면 쿼리가 Lucene 속성 인덱스로 확인되어야 합니다. 해결할 수 있는 색인이 없는 경우 색인 작성으로 이동합니다.
1. 필요에 따라 쿼리를 XPath 또는 JCR-SQL2로 변환합니다.

   * **쿼리 빌더 쿼리**

     ```js
     query type=cq:Page
     path=/content/my-site/us/en
     property=jcr:content/contentType
     property.value=article-page
     orderby=@jcr:content/publishDate
     orderby.sort=desc
     ```

   * **Query Builder 쿼리에서 생성된 XPath**

     ```js
     /jcr:root/content/my-site/us/en//element(*, cq:Page)[jcr:content/@contentType = 'article-page'] order by jcr:content/@publishDate descending
     ```

1. 최적화된 Lucene 속성 인덱스 정의를 생성할 수 있도록 XPath(또는 JCR-SQL2)를 `https://oakutils.appspot.com/generate/index`의 Oak 인덱스 정의 생성기에 제공하십시오. <!-- The above URL is 404 as of April 24, 2023 -->

   **생성된 Lucene 속성 인덱스 정의**

   ```xml
   - evaluatePathRestrictions = true
   - compatVersion = 2
   - type = "lucene"
   - async = "async"
   - jcr:primaryType = oak:QueryIndexDefinition
       + indexRules
       + cq:Page
           + properties
           + contentType
               - name = "jcr:content/contentType"
               - propertyIndex = true
           + publishDate
               - ordered = true
               - name = "jcr:content/publishDate"
   ```

1. 생성된 정의를 추가 방식으로 기존 Lucene 속성 인덱스에 수동으로 병합합니다. 기존 구성은 다른 쿼리를 충족하는 데 사용될 수 있으므로 제거하지 않도록 주의하십시오.

   1. cq:Page를 포함하는 기존 Lucene 속성 인덱스(인덱스 관리자 사용)를 찾습니다. 이 경우 `/oak:index/cqPageLucene`입니다.
   1. 최적화된 인덱스 정의(#4단계)와 기존 인덱스(/oak:index/cqPageLucene) 간의 구성 델타를 식별하고, 최적화된 인덱스에서 누락된 구성을 기존 인덱스 정의에 추가합니다.
   1. AEM의 리인덱싱 모범 사례에 따라, 기존 컨텐츠가 이 인덱스 구성 변경의 영향을 받을 수 있는지 여부를 기준으로 새로 고침 또는 리인덱싱이 순서대로 수행됩니다.

## 새 색인 만들기 {#create-a-new-index}

1. 쿼리가 기존 Lucene 속성 인덱스로 확인되지 않는지 확인합니다. 이 경우 조정 및 기존 색인에 대한 위의 섹션을 참조하십시오.
1. 필요에 따라 쿼리를 XPath 또는 JCR-SQL2로 변환합니다.

   * **쿼리 빌더 쿼리**

     ```js
     type=myApp:Author
     property=firstName
     property.value=ira
     ```

   * **Query Builder 쿼리에서 생성된 XPath**

     ```js
     //element(*, myApp:Page)[@firstName = 'ira']
     ```

1. 최적화된 Lucene 속성 인덱스 정의를 생성할 수 있도록 XPath(또는 JCR-SQL2)를 `https://oakutils.appspot.com/generate/index`의 Oak 인덱스 정의 생성기에 제공하십시오. <!-- The above URL is 404 as of April 24, 2023 -->

   **생성된 Lucene 속성 인덱스 정의**

   ```xml
   - compatVersion = 2
   - type = "lucene"
   - async = "async"
   - jcr:primaryType = oak:QueryIndexDefinition
       + indexRules
       + myApp:AuthorModel
           + properties
           + firstName
               - name = "firstName"
               - propertyIndex = true
   ```

1. 생성된 Lucene 속성 인덱스 정의를 배포합니다.

   새 색인에 대해 Oak 색인 정의 생성기에서 제공하는 XML 정의를 Oak 색인 정의를 관리하는 AEM 프로젝트에 추가합니다(코드에 따라 Oak 색인 정의가 다르므로 색인 정의를 코드로 취급해야 함).

   일반적인 AEM 소프트웨어 개발 라이프사이클에 따라 새 인덱스를 배포하고 테스트하고 쿼리가 인덱스로 확인되며 쿼리가 수행되는지 확인합니다.

   이 색인의 초기 배포 시 AEM은 필요한 데이터로 색인을 채웁니다.

## 인덱스 없는 쿼리와 트래버스 쿼리는 언제 정상입니까? {#when-index-less-and-traversal-queries-are-ok}

AEM의 유연한 콘텐츠 아키텍처로 인해, 콘텐츠 구조의 트래버스가 시간이 지남에 따라 용인할 수 없을 정도로 커지지 않도록 예측하고 보장하는 것은 어렵습니다.

따라서 경로 제한과 노드 유형 제한의 조합으로 **20개 미만의 노드가 계속 트래버스되는 경우를 제외하고 인덱스가 쿼리를 충족하는지 확인하십시오.**

## 쿼리 개발 도구 {#query-development-tools}

### Adobe 지원됨 {#adobe-supported}

* **Query Builder 디버거**

   * Query Builder 쿼리를 실행하고 지원되는 XPath를 생성하기 위한 WebUI(Explain Query 또는 Oak Index Definition Generator에 사용).
   * [/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)의 AEM에서

* **CRXDE Lite - 쿼리 도구**

   * XPath 및 JCR-SQL2 쿼리를 실행하기 위한 WebUI.
   * AEM [/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp) > 도구 > 쿼리에서...

* **[쿼리 설명](/help/sites-administering/operations-dashboard.md#explain-query)**

   * 지정된 XPATH 또는 JCR-SQL2 쿼리에 대한 자세한 설명(쿼리 계획, 쿼리 시간 및 결과 수)을 제공하는 AEM 작업 대시보드입니다.

* **[느린/자주 사용하는 쿼리](/help/sites-administering/operations-dashboard.md#query-performance)**

   * AEM에서 실행된 최근 느리고 인기 있는 쿼리를 나열하는 AEM 작업 대시보드.

* **[인덱스 관리자](/help/sites-administering/operations-dashboard.md#the-index-manager)**

   * AEM 인스턴스에 인덱스를 표시하는 AEM Operations WebUI를 통해 인덱스가 무엇인지 쉽게 파악할 수 있으며 타깃팅하거나 늘릴 수 있습니다.

* **[로깅](/help/sites-administering/operations-dashboard.md#log-messages)**

   * Query Builder 로깅

      * `DEBUG @ com.day.cq.search.impl.builder.QueryImpl`

   * Oak 쿼리 실행 로깅

      * `DEBUG @ org.apache.jackrabbit.oak.query`

* **Apache Jackrabbit 쿼리 엔진 설정 OSGi 구성**

   * 쿼리 순회를 위한 실패 동작을 구성하는 OSGi 구성입니다.
   * [/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService](http://localhost:4502/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService)의 AEM

* **NodeCounter JMX Mbean**

   * AEM의 콘텐츠 트리에 있는 노드 수를 예상하는 데 사용되는 JMX MBean입니다.
   * [/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter)의 AEM

### 지원되는 커뮤니티 {#community-supported}

* `https://oakutils.appspot.com/generate/index`**<!-- The above URL is 404 as of April 24, 2023 -->의** Oak 인덱스 정의 생성기

   * XPath 또는 JCR-SQL2 쿼리 문에서 최적의 Lucent 속성 인덱스를 생성합니다.

* **_AEM Chrome 플러그인_** <!-- For whatever reason, the URL to this extension was causing too many redirects when doing the request so it was removed entirely to get rid of the error; users can easily look up the extension in Google instead. DO NOT ADD THE URL AGAIN!-->

   * _AEM Chrome 플러그인_&#x200B;은(는) 브라우저의 개발 도구 콘솔에서 실행 쿼리 및 쿼리 계획을 포함한 요청당 로그 데이터를 표시하는 Google Chrome 웹 브라우저 확장 기능입니다.
   * AEM에 [Sling Log Tracer 1.0.2+](https://sling.apache.org/downloads.cgi)을(를) 설치하고 활성화해야 합니다.
