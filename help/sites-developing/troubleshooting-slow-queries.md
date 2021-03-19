---
title: 느린 쿼리 문제 해결
seo-title: 느린 쿼리 문제 해결
description: 느린 쿼리 문제 해결
seo-description: 'null'
uuid: ad09546a-c049-44b2-99a3-cb74ee68f040
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: c01e42ff-e338-46e6-a961-131ef943ea91
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2269'
ht-degree: 0%

---


# 느린 쿼리 문제 해결{#troubleshooting-slow-queries}

## 느린 쿼리 분류 {#slow-query-classifications}

AEM에는 심각도 별로 나열된 슬로우 쿼리의 3가지 주요 분류가 있습니다.

1. **인덱스 없는 쿼리**

   * 색인 확인 및 결과 수집을 위해 JCR의 내용을 트래버스하지 않는 **을(를) 수행하는 쿼리**

1. **제한적이지 않은(또는 범위 지정) 쿼리**

   * 색인으로 확인되지만 결과를 수집하려면 모든 색인 항목을 트래버스해야 하는 쿼리

1. **큰 결과 집합 쿼리**

   * 매우 많은 결과를 반환하는 쿼리

쿼리의 첫 번째 2개 분류(인덱스-less 및 형편없이 제한됨)는 Oak 쿼리 엔진이 각 **잠재적** 결과(컨텐트 노드 또는 색인 항목)를 검사하여 **실제** 결과 세트에 속하는 항목을 식별하도록 강제하므로 속도가 느립니다.

각각의 잠재적 결과를 검사하는 행위는 트래버스라고 불리는 것이다.

각 잠재적 결과를 검사해야 하므로 실제 결과 집합을 결정하는 비용은 잠재적인 결과 수와 함께 선형으로 증가합니다.

쿼리 제한 사항 및 조정 인덱스를 추가하면 색인 데이터를 최적화된 형식으로 저장할 수 있으므로 가능한 결과 세트에 대한 선형 검사의 필요성을 절감하거나 없앨 수 있습니다.

AEM 6.3에서는 기본적으로 100,000의 트래픽에 도달하면 쿼리가 실패하고 예외가 발생합니다. 이 제한은 AEM 6.3 이전 AEM 버전에서 기본적으로 존재하지 않지만 Apache Jackrabbit 쿼리 엔진 설정 OSGi 구성 및 QueryEngineSettings JMX 빈(속성 LimitReads)을 통해 설정할 수 있습니다.

### 인덱스 없는 쿼리 검색 중 {#detecting-index-less-queries}

#### 개발 중 {#during-development}

**모든** 쿼리를 설명하고 해당 쿼리 계획에 **/&amp;ast;가 포함되어 있지 않은지 확인하십시오.** 설명을 트래버스합니다. 쿼리 계획 탐색 예:

* **플랜:** `[nt:unstructured] as [a] /* traverse "/content//*" where ([a].[unindexedProperty] = 'some value') and (isdescendantnode([a], [/content])) */`

#### 배포 후 {#post-deployment}

* 인덱스 없는 순회 쿼리를 위해 `error.log`을(를) 모니터링합니다.

   * `*INFO* org.apache.jackrabbit.oak.query.QueryImpl Traversal query (query without index) ... ; consider creating and index`
   * 이 메시지는 사용할 수 있는 인덱스가 없고 쿼리가 여러 노드를 잠재적으로 추적하는 경우에만 기록됩니다. 색인을 사용할 수 있는 경우에는 메시지가 기록되지 않지만 탐색 양이 작으므로 빠르게 기록됩니다.

* AEM [쿼리 성능](/help/sites-administering/operations-dashboard.md#query-performance) 작업 콘솔 및 [추적이 필요하거나 색인 쿼리 설명이 없는 느린 쿼리 설명](/help/sites-administering/operations-dashboard.md#explain-query)을 방문하십시오.

### 제한적이지 않은 쿼리 검색 중 {#detecting-poorly-restricted-queries}

#### 개발 중 {#during-development-1}

모든 쿼리를 설명하고 쿼리의 속성 제한 사항과 일치하도록 조정된 색인으로 확인하는지 확인합니다.

* 이상적인 쿼리 계획 적용에는 모든 속성 제한에 대해 `indexRules`이(가) 있으며, 쿼리에서 가장 엄격한 속성 제한에 대한 최소값이 있습니다.
* 결과를 정렬하는 쿼리는 `orderable=true.`을 설정하는 속성별로 정렬되는 인덱스 규칙에 대한 Lucene 속성 색인으로 확인되어야 합니다.

#### 예를 들어 기본 `cqPageLucene`에 `jcr:content/cq:tags` {#for-example-the-default-cqpagelucene-does-not-have-an-index-rule-for-jcr-content-cq-tags}에 대한 인덱스 규칙이 없습니다.

cq:tags 인덱스 규칙을 추가하기 전

* **cq:태그 색인 규칙**

   * 즉시 사용 안 함

* **쿼리 빌더 쿼리**

   ```js
   type=cq:Page
   property=jcr:content/cq:tags
   property.value=my:tag
   ```

* **쿼리 계획**

   `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) *:* where [a].[jcr:content/cq:tags] = 'my:tag' */`

이 쿼리는 `cqPageLucene` 인덱스로 확인되지만 `jcr:content` 또는 `cq:tags`에 대한 속성 인덱스 규칙이 없으므로 이 제한을 평가할 때 `cqPageLucene` 인덱스의 모든 레코드가 확인되어 일치 항목을 결정합니다. 즉, 인덱스에 1백만 개의 `cq:Page` 노드가 있으면 1백만 개의 레코드가 확인되어 결과 세트를 결정합니다.

cq:tags 인덱스 규칙을 추가한 후

* **cq:태그 색인 규칙**

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

`jcr:content/cq:tags` 제한이 있는 쿼리가 수행되면 색인은 값별로 결과를 찾을 수 있습니다. 즉, 100 `cq:Page` 노드의 값이 `myTagNamespace:myTag`인 경우 100개의 결과만 반환되고 나머지 999,000은 제한 확인에서 제외되어 10,000배수로 성능을 향상시킵니다.

물론 추가적인 쿼리 제한 사항은 해당 결과 집합을 줄이고 쿼리 최적화를 더욱 최적화합니다.

마찬가지로 `cq:tags` 속성에 대한 추가 인덱스 규칙이 없으면 인덱스 결과가 모든 전체 텍스트 일치 항목을 반환하므로 `cq:tags`에 대한 제한이 있는 전체 텍스트 쿼리도 제대로 작동하지 않습니다. cq:tags에 대한 제한은 그 다음에 필터링됩니다.

색인 후 필터링의 또 다른 원인은 개발 중에 자주 누락되는 액세스 제어 목록입니다. 사용자가 액세스할 수 없을 수 있는 경로를 쿼리에 반환하지 않도록 하십시오. 일반적으로 쿼리에 대한 관련 경로 제한을 제공하는 것과 함께 더 나은 컨텐츠 구조로 수행할 수 있습니다.

쿼리 결과로 Lucene 색인이 매우 작은 하위 집합을 반환하기 위해 많은 결과를 반환하는지 여부를 확인하는 유용한 방법은 `org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex`에 대한 DEBUG 로그를 활성화하고 인덱스에서 로드되는 문서 수를 확인하는 것입니다. 최종 결과 수와 로드된 문서의 수는 불균형하지 않아야 합니다. 자세한 내용은 [로깅](/help/sites-deploying/configure-logging.md)을 참조하십시오.

#### 배포 후 {#post-deployment-1}

* 탐색 쿼리를 위해 `error.log`을(를) 모니터링합니다.

   * `*WARN* org.apache.jackrabbit.oak.spi.query.Cursors$TraversingCursor Traversed ### nodes ... consider creating an index or changing the query`

* AEM [쿼리 성능](/help/sites-administering/operations-dashboard.md#query-performance) 작업 콘솔 및 [쿼리](/help/sites-administering/operations-dashboard.md#explain-query)쿼리 쿼리 중 속성 규칙에 대한 쿼리 속성 제한을 해결하지 않는 쿼리 계획을 찾는 느린 쿼리를 찾습니다.

### 큰 결과 집합 쿼리 검색 중 {#detecting-large-result-set-queries}

#### 개발 중 {#during-development-2}

oak.queryLimitInMemory에 대해 낮은 임계값을 설정합니다(예: 10000) 및 oak.queryLimitReads(예: 5000) &quot;쿼리가 x 노드보다 많이 읽었습니다..&quot;라는 UnsupportedOperationException을 히트할 때 고가의 쿼리를 최적화합니다.

리소스 사용량이 많은 쿼리(예: 색인이 지원되지 않거나 덜 덮는 인덱스로 지원되지 않음). 예를 들어 1M 노드를 읽는 쿼리는 많은 IO를 발생시키고 전체 애플리케이션 성능에 부정적인 영향을 줍니다. 따라서 위의 제한으로 인해 실패한 모든 쿼리는 분석 및 최적화되어야 합니다.

#### 배포 후 {#post-deployment-2}

* 대용량 노드 순회 또는 대규모 더미 메모리 사용을 트리거하는 쿼리의 로그를 모니터링합니다.&quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * 탐색 노드 수를 줄이기 위해 쿼리 최적화

* 대량의 더미 메모리 사용을 트리거하는 쿼리의 로그를 모니터링합니다.

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * Heap 메모리 소비를 줄이기 위해 쿼리 최적화

AEM 6.0 - 6.2 버전의 경우 AEM 시작 스크립트에서 JVM 매개 변수를 통해 노드 통과에 대한 임계값을 조정하여 큰 쿼리가 환경을 오버로드하지 못하도록 할 수 있습니다. 권장 값은 다음과 같습니다.

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

AEM 6.3에서 위의 2개 매개 변수는 기본적으로 미리 구성되며 OSGi QueryEngineSettings를 통해 수정할 수 있습니다.

자세한 내용은[https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## 쿼리 성능 조정 {#query-performance-tuning}

AEM에서 쿼리 성능 최적화의 목표는 다음과 같습니다.

**&quot;규제가 많으면 많을수록 좋다.&quot;**

다음 개요를 통해 쿼리 성능을 보장하기 위해 조정을 권장합니다. 먼저 쿼리를 덜 눈에 띄는 활동인 다음 필요한 경우 색인 정의를 조정합니다.

### 쿼리 문 {#adjusting-the-query-statement} 조정

AEM에서는 다음 쿼리 언어를 지원합니다.

* QueryBuilder
* JCR-SQL2
* XPath

다음 예제에서는 AEM 개발자가 사용하는 가장 일반적인 쿼리 언어로 Query Builder를 사용하지만 JCR-SQL2 및 XPath에도 동일한 원칙을 적용할 수 있습니다.

1. 쿼리가 기존 Lucene 속성 색인으로 확인되도록 nodetype 제한을 추가합니다.

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

   nodetype 제한이 없는 쿼리는 AEM에서 AEM의 모든 노드가 하위 유형인 `nt:base` nodetype을 가정해야 하므로 사실상 nodetype 제한이 없습니다.

   `type=cq:Page`을(를) 설정하면 이 쿼리는 `cq:Page` 노드로만 제한되고 쿼리를 AEM cqPageLucene로 해결합니다. 단, 결과는 AEM의 노드 하위 집합(`cq:Page` 노드만)으로 제한됩니다.

1. 쿼리가 기존 Lucene 속성 색인으로 확인되도록 쿼리의 Nodetype 제한을 조정합니다.

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

   `nt:hierarchyNode` 은 상위 노드 유형 `cq:Page`이며, 사용자 지정 응용 프로그램 `jcr:content/contentType=article-page` 을 통해  `cq:Page` 노드에만 적용된다고 가정할 때 이 쿼리는  `cq:Page` 노드(여기서)만 반환합니다  `jcr:content/contentType=article-page` 이 제한은 다음과 같은 이유로 인해 최적의 제한 사항입니다.

   * 다른 노드는 `nt:hierarchyNode`에서 상속됩니다(예: `dam:Asset`)을 클릭합니다.
   * `nt:hierarchyNode`에 대해 AEM에서 제공하는 인덱스가 없지만 `cq:Page`에 대해 제공된 인덱스가 있습니다.
   `type=cq:Page`을(를) 설정하면 이 쿼리가 `cq:Page` 노드로만 제한되고 쿼리를 AEM cqPageLucene로 확인하여 AEM의 노드 하위 집합(cq:Page 노드만)으로 결과를 제한합니다.

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

   속성 제한을 `jcr:content/contentType`(사용자 정의 값)에서 잘 알려진 속성 `sling:resourceType`으로 변경하면 쿼리를 통해 `sling:resourceType`에 의해 모든 콘텐츠를 인덱싱하는 속성 인덱스 `slingResourceType`로 확인할 수 있습니다.

   속성 인덱스(Lucene 속성 색인과 반대)는 쿼리가 nodetype으로 구분되지 않고 단일 속성 제한이 결과 집합을 지배하는 경우에 가장 적합합니다.

1. 쿼리에 가능한 가장 긴밀한 경로 제한을 추가합니다. 예를 들어 `/content/my-site`보다 `/content/my-site/us/en`, `/`보다 `/content/dam`를 선호합니다.

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

   경로 제한을 `path=/content`에서 `path=/content/my-site/us/en`까지 범위 조정하면 색인이 검사를 받아야 하는 색인 항목의 수를 줄일 수 있습니다. 쿼리가 경로를 매우 잘 제한할 수 있는 경우, `/content` 또는 `/content/dam` 이외에 인덱스에 `evaluatePathRestrictions=true`가 있는지 확인합니다.

   `evaluatePathRestrictions`을 사용하면 인덱스 크기가 증가합니다.

1. 가능하면 다음과 같은 쿼리 함수/작업을 피하십시오.`LIKE` 및 `fn:XXXX` 값이 제한 기반 결과 수와 함께 조정됩니다.

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

   텍스트가 와일드카드(&quot;%...&#39;)로 시작하는 경우 색인을 사용할 수 없으므로 LIKE 조건이 평가 속도가 느립니다. jcr:contains 조건에서는 전체 텍스트 인덱스를 사용할 수 있으므로 권장됩니다. 이 경우 확인된 Lucene 속성 색인이 `analayzed=true`과(와) 함께 `jcr:content/contentType`에 대한 indexRule을 가져야 합니다.

   `fn:lowercase(..)`과(와) 같은 쿼리 함수를 사용하는 것은 이보다 빠른 것이 아니므로 최적화하기가 어려울 수 있습니다(보다 복잡하고 까다로운 색인 분석기 구성 제외). 잠재적인 가장 작은 결과 세트에서 작동되도록 하여 전체 쿼리 성능을 개선하기 위해 다른 범위 지정 제한을 식별하는 것이 가장 좋습니다.

1. ***이 조정은 쿼리 빌더에만 적용되며 JCR-SQL2 또는 XPath에는 적용되지 않습니다.***

   전체 결과 세트가 즉시 필요하지 않은 **인 경우 [Query Builder&#39; guessTotal](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results)을 사용하십시오.**

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
   쿼리 실행이 빠르지만 결과 수가 큰 경우, p.`guessTotal`은(는) 쿼리 빌더 쿼리에 대한 중요한 최적화입니다.

   `p.guessTotal=100` 처음 100개의 결과만 수집하도록 Query Builder에 지시하고 하나 이상의 결과가 존재하는지 여부를 나타내는 부울 플래그를 설정합니다(이 수를 카운트하면 속도가 느려집니다). 이러한 최적화는 페이지의 하위 집합만 증분적으로 표시되는 페이지 매김 또는 로드 사용 사례의 경우 탁월합니다.

## 기존 인덱스 조정 {#existing-index-tuning}

1. 최적 쿼리가 속성 색인으로 확인되면 속성 색인이 최소한으로 조정 가능하므로 수행할 작업이 남아 있지 않습니다.
1. 그렇지 않으면 쿼리는 Lucene 속성 색인으로 확인됩니다. 색인을 확인할 수 없는 경우 새 색인 만들기로 이동합니다.
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

   * **쿼리 빌더 쿼리에서 생성된 XPath**

      ```js
      /jcr:root/content/my-site/us/en//element(*, cq:Page)[jcr:content/@contentType = 'article-page'] order by jcr:content/@publishDate descending
      ```

1. 최적화된 Lucene 속성 색인 정의를 생성하려면 XPath(또는 JCR-SQL2)를 [Oak 색인 정의 생성기](https://oakutils.appspot.com/generate/index)에 입력합니다.

   **생성된 Lucene 속성 색인 정의**

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

1. 생성된 정의를 기존 Lucene 속성 색인에 추가 방식으로 수동으로 병합합니다. 다른 쿼리를 충족하는 데 사용할 수 있으므로 기존 구성을 제거하지 않도록 주의하십시오.

   1. cq:Page(색인 관리자 사용)를 포함하는 기존 Lucene 속성 인덱스를 찾습니다. 이 경우 `/oak:index/cqPageLucene`.
   1. 최적화된 색인 정의(#4 단계)와 기존 인덱스(/oak:index/cqPageLucene) 사이의 구성 델타를 식별하고 최적화된 인덱스의 누락된 구성을 기존 색인 정의에 추가합니다.
   1. AEM 색인 재지정 우수 사례에 따라 이 색인 구성 변경으로 기존 컨텐츠가 영향을 받는지 여부를 기준으로 새로 고침 또는 재색인이 순서대로 지정됩니다.

## 새 인덱스 만들기 {#create-a-new-index}

1. 쿼리가 기존 Lucene 속성 색인으로 확인되지 않는지 확인합니다. 이 경우 조정 및 기존 색인에 대한 위의 섹션을 참조하십시오.
1. 필요에 따라 쿼리를 XPath 또는 JCR-SQL2로 변환합니다.

   * **쿼리 빌더 쿼리**

      ```js
      type=myApp:Author
      property=firstName
      property.value=ira
      ```

   * **쿼리 빌더 쿼리에서 생성된 XPath**

      ```js
      //element(*, myApp:Page)[@firstName = 'ira']
      ```

1. 최적화된 Lucene 속성 색인 정의를 생성하려면 XPath(또는 JCR-SQL2)를 [Oak 색인 정의 생성기](https://oakutils.appspot.com/generate/index)에 입력합니다.

   **생성된 Lucene 속성 색인 정의**

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

1. 생성된 Lucene 속성 색인 정의를 배포합니다.

   Oak 인덱스 정의를 관리하는 AEM 프로젝트에 새 인덱스에 대해 Oak 인덱스 정의 생성기에서 제공하는 XML 정의를 추가합니다(코드가 Oak 인덱스 정의에 종속되므로 Oak 인덱스 정의를 코드로 처리).

   일반적인 AEM 소프트웨어 개발 라이프사이클에 따라 새 인덱스를 배포 및 테스트하고 쿼리가 인덱스로 확인되고 쿼리가 성능에 영향을 미치는지 확인합니다.

   이 색인이 처음 배포되면 AEM은 필요한 데이터로 색인을 채웁니다.

## 색인이 없는 순회 쿼리는 언제 정상입니까?{#when-index-less-and-traversal-queries-are-ok}

AEM의 유연한 컨텐츠 아키텍처로 인해 시간이 지남에 따라 컨텐츠 구조의 트래픽이 수용할 수 없을 정도로 확대되지 않도록 예측하여 보장하기가 어렵습니다.

따라서 경로 제한 및 노드 제한을 조합하여 **20개 미만의 노드가 트래버스되지 않도록 보장하는 경우를 제외하고 색인이 쿼리를 만족하는지 확인합니다.**

## 쿼리 개발 도구 {#query-development-tools}

### 지원되는 Adobe {#adobe-supported}

* **쿼리 빌더 디버거**

   * 쿼리 빌더 쿼리를 실행하고 지원 XPath를 생성하기 위한 WebUI입니다(쿼리 설명 또는 Oak 색인 정의 생성기에서 사용).
   * AEM 위치: [/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)

* **CRXDE Lite - 쿼리 도구**

   * XPath 및 JCR-SQL2 쿼리를 실행하기 위한 WebUI입니다.
   * [/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp) > 도구 > 쿼리...의 AEM에 있습니다.

* **[쿼리 설명](/help/sites-administering/operations-dashboard.md#explain-query)**

   * 지정된 XPATH 또는 JCR-SQL2 쿼리에 대한 자세한 설명(쿼리 계획, 쿼리 시간 및 결과 수)을 제공하는 AEM 작업 대시보드입니다.

* **[느린/자주 사용하는 쿼리](/help/sites-administering/operations-dashboard.md#query-performance)**

   * AEM Operations 대시보드에서는 AEM에서 최근에 실행된 슬로우 및 인기 있는 쿼리를 나열합니다.

* **[색인 관리자](/help/sites-administering/operations-dashboard.md#the-index-manager)**

   * AEM 인스턴스에서 인덱스를 표시하는 AEM Operations WebUI;타깃팅하거나 증강할 수 있는 색인을 손쉽게 파악할 수 있습니다.

* **[로깅](/help/sites-administering/operations-dashboard.md#log-messages)**

   * 쿼리 빌더 로깅

      * `DEBUG @ com.day.cq.search.impl.builder.QueryImpl`
   * Oak 쿼리 실행 로깅

      * `DEBUG @ org.apache.jackrabbit.oak.query`


* **Apache Jackrabbit 쿼리 엔진 설정 OSGi 구성**

   * 쿼리 탐색을 위한 오류 동작을 구성하는 OSGi 구성
   * AEM에 위치: [/system/console/configMgr#org.apache.jackrabbit.query.QueryEngineSettingsService](http://localhost:4502/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService)

* **NodeCounter JMX Mbean**

   * AEM의 컨텐츠 트리에서 노드 수를 예상하는 데 사용되는 JMX MBean입니다.
   * [/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter)의 AEM에 위치

### 커뮤니티 지원 {#community-supported}

* **[Oak 색인 정의 생성기](https://oakutils.appspot.com/generate/index)**

   * XPath 또는 JCR-SQL2 쿼리 문에서 최적의 Luence 속성 인덱스를 생성합니다.

* **[AEM Chrome 플러그인](https://chrome.google.com/webstore/detail/aem-chrome-plug-in/ejdcnikffjleeffpigekhccpepplaode?hl=en-US)**

   * 실행된 쿼리 및 해당 쿼리 계획을 포함하여 요청당 로그 데이터를 표시하는 Google Chrome 웹 브라우저 익스텐션이 브라우저의 개발 도구 콘솔에서 표시됩니다.
   * AEM에 [Sling Log Tracer 1.0.2+](https://sling.apache.org/downloads.cgi)을 설치하고 사용하도록 설정해야 합니다.
