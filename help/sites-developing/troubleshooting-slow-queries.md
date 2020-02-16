---
title: 슬로우 쿼리 문제 해결
seo-title: 슬로우 쿼리 문제 해결
description: 'null'
seo-description: 'null'
uuid: ad09546a-c049-44b2-99a3-cb74ee68f040
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: c01e42ff-e338-46e6-a961-131ef943ea91
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# 슬로우 쿼리 문제 해결{#troubleshooting-slow-queries}

## 느린 쿼리 분류 {#slow-query-classifications}

AEM에는 심각도 별로 나열된 슬로우 쿼리의 세 가지 기본 분류가 있습니다.

1. **색인 없는 쿼리**

   * 색인으로 **확인되지** 않고 JCR의 콘텐츠를 트래버스하여 결과를 수집하는 쿼리

1. **제한적이지 않은(또는 범위 지정) 쿼리**

   * 인덱스로 확인되지만 결과를 수집하려면 모든 색인 항목을 트래버스해야 하는 쿼리

1. **큰 결과 집합 쿼리**

   * 매우 많은 결과를 반환하는 쿼리

쿼리의 처음 2개 분류(인덱스-less 및 형편없이 제한됨)는 Oak 쿼리 엔진에서 **실제** 결과 집합에 속하는 각 **잠재적** 결과(컨텐츠 노드 또는 인덱스 항목)를 검사하도록 강제하므로 속도가 느립니다.

각각의 잠재적 결과를 검사하는 행위는 트래버스라고 불리는 것입니다.

각 잠재적 결과를 검사해야 하므로 실제 결과 세트를 결정하는 비용은 잠재적인 결과 수와 함께 선형으로 증가합니다.

쿼리 제한 및 조정 색인을 추가하면 색인 데이터를 최적화된 형식으로 저장할 수 있으므로 신속하게 결과를 검색할 수 있고 잠재적 결과 집합을 선형 검사하지 않아도 됩니다.

AEM 6.3에서 기본적으로 100,000의 트래픽에 도달하면 쿼리가 실패하고 예외가 발생합니다. 이 제한은 AEM 6.3 이전 AEM 버전에서 기본적으로 존재하지 않지만 Apache Jackrabbit 쿼리 엔진 설정 OSGi 구성 및 QueryEngineSettings JMX bean(속성 LimitReads)을 통해 설정할 수 있습니다.

### 인덱스 없는 쿼리 감지 {#detecting-index-less-queries}

#### 개발 중 {#during-development}

쿼리 **모두** 설명하고 쿼리 계획에 **/&amp;ast;가 포함되어 있지 않은지 확인하십시오.그 속에 있는 설명을** 건너다. 쿼리 계획 탐색 예:

* **** 플랜: `[nt:unstructured] as [a] /* traverse "/content//*" where ([a].[unindexedProperty] = 'some value') and (isdescendantnode([a], [/content])) */`

#### 배포 후 {#post-deployment}

* 인덱스 없는 순회 쿼리를 `error.log` 모니터링합니다.

   * `*INFO* org.apache.jackrabbit.oak.query.QueryImpl Traversal query (query without index) ... ; consider creating and index`
   * 이 메시지는 사용할 수 있는 인덱스가 없고 쿼리가 여러 노드를 순회하는 경우에만 기록됩니다. 인덱스를 사용할 수 있는 경우 메시지가 기록되지 않지만 탐색 양이 작아 속도가 빠릅니다.

* AEM Query Performance [작업](/help/sites-administering/operations-dashboard.md#query-performance) 콘솔 및 [순차적](/help/sites-administering/operations-dashboard.md#explain-query) 또는 인덱스 쿼리 설명이 없는느린 쿼리 설명을 참조하십시오.

### 제한적이지 않은 쿼리 감지 {#detecting-poorly-restricted-queries}

#### 개발 중 {#during-development-1}

모든 쿼리를 설명하고 쿼리의 속성 제한에 맞게 조정된 색인으로 확인하는지 확인합니다.

* 쿼리 계획 적용은 모든 속성 제한에 `indexRules` 대한 이상적이며, 쿼리에서 속성 제한이 가장 적은 경우에 적합합니다.
* 결과를 정렬하는 쿼리는 Lucene 속성 인덱스로 확인되어야 합니다. 이 인덱스는 `orderable=true.`

#### 예를 들어 기본값에는 `cqPageLucene` `jcr:content/cq:tags`{#for-example-the-default-cqpagelucene-does-not-have-an-index-rule-for-jcr-content-cq-tags}

cq:tags 인덱스 규칙을 추가하기 전에

* **cq:태그 색인 규칙**

   * 즉시 사용 안 함

* **쿼리 빌더 쿼리**

   * 
      ```
      type=cq:Page
       property=jcr:content/cq:tags
       property.value=my:tag
      ```

* **쿼리 계획**

   * `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) *:* where [a].[jcr:content/cq:tags] = 'my:tag' */`

이 쿼리는 `cqPageLucene` 인덱스로 확인되지만, 속성 인덱스 규칙이 없거나 이 제한을 평가할 `jcr:content` 때 `cq:tags``cqPageLucene` 인덱스의 모든 레코드가 확인되어 일치 항목이 결정됩니다. 즉, 인덱스에 100만 개의 `cq:Page` 노드가 있으면 100만 개의 레코드가 확인되어 결과 세트를 결정합니다.

cq:tags 인덱스 규칙을 추가한 후

* **cq:태그 색인 규칙**

   * 
      ```
      /oak:index/cqPageLucene/indexRules/cq:Page/properties/cqTags
       @name=jcr:content/cq:tags
       @propertyIndex=true
      ```

* **쿼리 빌더 쿼리**

   * 
      ```
      type=cq:Page
       property=jcr:content/cq:tags
       property.value=myTagNamespace:myTag
      ```

* **쿼리 계획**

   * `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) jcr:content/cq:tags:my:tag where [a].[jcr:content/cq:tags] = 'my:tag' */`

인덱스에 indexRule을 추가하면 `jcr:content/cq:tags` `cqPageLucene` `cq:tags` 데이터를 최적화된 방식으로 저장할 수 있습니다.

제한이 있는 쿼리를 수행하면 인덱스는 값별로 결과를 조회할 수 있습니다. `jcr:content/cq:tags` 즉, 100 `cq:Page` 개의 노드가 `myTagNamespace:myTag` 값으로 있으면 100개의 결과만 반환되고 나머지 999,000은 제한 확인에서 제외되어 10,000배율로 성능을 향상시킵니다.

물론 추가적인 쿼리 제한 사항은 적격한 결과 집합을 줄이고 쿼리 최적화를 추가로 최적화합니다.

마찬가지로 속성에 대한 추가 인덱스 규칙이 없으면 인덱스의 결과가 모든 전체 텍스트 일치 항목을 반환하므로 전체 텍스트 쿼리도 제대로 `cq:tags` `cq:tags` 수행되지 않습니다. cq:tags에 대한 제한은 그 다음에 필터링됩니다.

색인 후 필터링의 또 다른 원인은 개발 중에 자주 누락되는 액세스 제어 목록입니다. 사용자가 액세스할 수 없는 경로를 쿼리로 반환하지 않도록 하십시오. 이러한 작업은 일반적으로 쿼리에 대한 관련 경로 제한을 제공하는 동시에 컨텐츠 구조를 개선하여 수행할 수 있습니다.

쿼리 결과로 Lucene 색인이 매우 작은 하위 집합을 반환하는 많은 결과를 반환하는 경우 DEBUG 로그를 활성화하고 인덱스에서 로드되는 문서 수를 확인하는 유용한 방법입니다. `org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex` 최종 결과 수와 로드된 문서의 수는 불균형하지 않아야 합니다. 자세한 내용은 로깅을 [참조하십시오](/help/sites-deploying/configure-logging.md).

#### 배포 후 {#post-deployment-1}

* 탐색 쿼리를 `error.log` 모니터링합니다.

   * `*WARN* org.apache.jackrabbit.oak.spi.query.Cursors$TraversingCursor Traversed ### nodes ... consider creating an index or changing the query`

* AEM 쿼리 성능 [작업](/help/sites-administering/operations-dashboard.md#query-performance) 콘솔과 [쿼리](/help/sites-administering/operations-dashboard.md#explain-query) 속성 제한을 인덱스 속성 규칙에 대한 쿼리 계획을 확인하지 않는 느린 쿼리 설명

### 큰 결과 집합 쿼리 감지 {#detecting-large-result-set-queries}

#### 개발 중 {#during-development-2}

oak.queryLimitInMemory에 대한 낮은 임계값을 설정합니다(예: 10000) 및 oak.queryLimitReads(예: 5000)&quot;쿼리가 x 노드보다 많은 노드를 읽었음을 의미하는 UnsupportedOperationException을 히트할 때 고가의 쿼리를 최적화합니다.

이렇게 하면 리소스 사용량이 많은 쿼리(예: 어떤 인덱스도 지원하지 않거나 더 적은 포함 인덱스로 뒷받침되지 않음). 예를 들어 1M 노드를 읽는 쿼리는 많은 IO를 발생시키고 전체 애플리케이션 성능에 부정적인 영향을 줍니다. 따라서 제한 이상으로 인해 실패한 모든 쿼리는 분석 및 최적화되어야 합니다.

#### 배포 후 {#post-deployment-2}

* 큰 노드 통과나 큰 더미 메모리 사용을 트리거하는 쿼리에 대한 로그를 모니터링합니다.&quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * 탐색 노드 수를 줄이기 위해 쿼리 최적화

* 큰 더미 메모리 사용을 트리거하는 쿼리에 대한 로그 모니터링:

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * Optimize the query to reduce the heap memory usage

AEM 6.0 - 6.2 버전의 경우 AEM 시작 스크립트의 JVM 매개 변수를 통해 노드 통과에 대한 임계값을 조정하여 큰 쿼리가 환경을 오버로드하지 못하도록 할 수 있습니다. 권장 값은 다음과 같습니다.

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

AEM 6.3에서 위의 2개 매개 변수는 기본적으로 미리 구성되며 OSGi QueryEngineSettings를 통해 수정할 수 있습니다.

추가 정보: [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## 쿼리 성능 조정 {#query-performance-tuning}

AEM에서 쿼리 성능 최적화의 좌우명은 다음과 같습니다.

**&quot;규제가 많을수록 좋다.&quot;**

쿼리 성능을 보장하기 위해 다음 개요를 조정하도록 권장합니다. 먼저 쿼리를 간단하게 조정한 다음 필요한 경우 색인 정의를 조정합니다.

### 쿼리 문 조정 {#adjusting-the-query-statement}

AEM에서는 다음 쿼리 언어를 지원합니다.

* QueryBuilder
* JCR-SQL2
* XPath

다음 예제에서는 AEM 개발자가 가장 많이 사용하는 쿼리 언어로 Query Builder를 사용하지만 JCR-SQL2 및 XPath에도 동일한 원칙이 적용됩니다.

1. 쿼리가 기존 Lucene 속성 색인으로 확인되도록 nodetype 제한을 추가합니다.

   * **최적화되지 않은 쿼리**

      * 
         ```
          property=jcr:content/contentType
          property.value=article-page
         ```
   * **최적화된 쿼리**

      * 
         ```
          type=cq:Page
          property=jcr:content/contentType
          property.value=article-page
         ```
   nodetype 제한이 없는 쿼리는 AEM이 nodetype을 가정하도록 `nt:base` 합니다. 이 nodetype은 AEM의 모든 노드가 하위 유형이므로 무데유형 제한이 없습니다.

   설정을 `type=cq:Page` 사용하면 이 쿼리가 `cq:Page` 노드로만 제한되고, 쿼리를 AEM의 cqPageLucene로 확인하여 AEM의 노드 하위 집합( `cq:Page` 노드만)으로 결과를 제한합니다.

1. 쿼리의 Nodetype 제한을 조정하여 쿼리가 기존 Lucene 속성 색인으로 확인되도록 합니다.

   * **최적화되지 않은 쿼리**

      * 
         ```
         type=nt:hierarchyNode
         property=jcr:content/contentType
         property.value=article-page
         ```
   * **최적화된 쿼리**

      * 
         ```
         type=cq:Page
         property=jcr:content/contentType
         property.value=article-page
         ```
   `nt:hierarchyNode` 는 상위 노드 `cq:Page`유형이며, 사용자 지정 응용 프로그램을 통해 `jcr:content/contentType=article-page` 노드에만 `cq:Page` 적용된다고 가정할 경우 이 쿼리는 `cq:Page` `jcr:content/contentType=article-page`노드(위치)만 반환합니다. 그러나 다음의 이유로 이 방법은 차선제의 제한입니다.

   * 다른 노드는 에서 상속됩니다( `nt:hierarchyNode` 예: `dam:Asset`)을 클릭합니다.
   * AEM에서 제공한 인덱스가 없지만 `nt:hierarchyNode`제공된 인덱스가 `cq:Page`있습니다.
   설정을 `type=cq:Page` 통해 이 쿼리를 `cq:Page` 노드만 제한하고 쿼리를 AEM의 cqPageLucene로 확인하여 AEM의 노드 하위 집합(cq:Page 노드만)으로 결과를 제한합니다.

1. 또는 쿼리가 기존 속성 색인으로 확인되도록 속성 제한을 조정합니다.

   * **최적화되지 않은 쿼리**

      * 
         ```
         property=jcr:content/contentType
         property.value=article-page
         ```
   * **최적화된 쿼리**

      * 
         ```
         property=jcr:content/sling:resourceType
         property.value=my-site/components/structure/article-page
         ```
   속성 제한을 `jcr:content/contentType` (사용자 지정 값)에서 잘 알려진 속성으로 변경하면 쿼리가 모든 컨텐츠를 인덱스화하는 속성 인덱스로 확인할 `sling:resourceType` 수 `slingResourceType` 있습니다 `sling:resourceType`.

   속성 인덱스(Lucene 속성 색인과 반대)는 쿼리가 nodetype으로 식별되지 않고 단일 속성 제한이 결과 집합을 지배하는 경우에 가장 적합합니다.

1. 쿼리에 가장 엄격한 경로 제한을 추가합니다. 예를 들어, `/content/my-site/us/en` 선호도가 `/content/my-site`높거나 `/content/dam` 낮습니다 `/`.

   * **최적화되지 않은 쿼리**

      * 
         ```
         type=cq:Page
         path=/content
         property=jcr:content/contentType
         property.value=article-page
         ```
   * **최적화된 쿼리**

      * 
         ```
         type=cq:Page
         path=/content/my-site/us/en
         property=jcr:content/contentType
         property.value=article-page
         ```
   경로 제한을 `path=/content`범위 `path=/content/my-site/us/en` 지정하여 색인을 통해 검사해야 하는 인덱스 항목의 수를 줄일 수 있습니다. 쿼리가 경로를 매우 잘 제한할 수 `/content` 있거나 그렇지 않을 `/content/dam`경우 인덱스가 포함되도록 하십시오 `evaluatePathRestrictions=true`.

   를 사용하면 인덱스 크기가 `evaluatePathRestrictions` 증가합니다.

1. 가능하면 다음과 같은 쿼리 함수/작업을 피하십시오.또한 `LIKE` 제한 `fn:XXXX` 기반의 결과 수에 따라 비용이 확장됩니다.

   * **최적화되지 않은 쿼리**

      * 
         ```
         type=cq:Page
         property=jcr:content/contentType
         property.operation=like
         property.value=%article%
         ```
   * **최적화된 쿼리**

      * 
         ```
         type=cq:Page
         fulltext=article
         fulltext.relPath=jcr:content/contentType
         ```
   텍스트가 와일드카드(&quot;%...&#39;)로 시작하는 경우 색인을 사용할 수 없으므로 LIKE 조건이 평가하기가 느립니다. jcr:contains 조건에서는 전체 텍스트 인덱스를 사용할 수 있으므로 선호됩니다. 이로 인해 확인된 Lucene 속성 색인이 indexRule을 `jcr:content/contentType` 포함시켜야 `analayzed=true`합니다.

   이와 같은 쿼리 함수를 사용하는 `fn:lowercase(..)` 것은 이보다 더 빠른 것이 아니기 때문에 최적화하기가 어려울 수 있습니다(복잡한 인덱스 분석기 구성 제외). 가능한 가장 작은 잠재적 결과 집합에서 함수를 작동하도록 하여 전체 쿼리 성능을 개선하기 위해 다른 범위 지정 제한을 식별하는 것이 가장 좋습니다.

1. ***이 조정은 쿼리 빌더에만 적용되며 JCR-SQL2 또는 XPath에는 적용되지 않습니다.***

   전체 [결과 세트가 **](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results) not **즉시 필요한 경우 Query Builder의 guessTotal을 사용하십시오.

   * **최적화되지 않은 쿼리**

      * 
         ```
         type=cq:Page
         path=/content
         ```
   * **최적화된 쿼리**

      * 
         ```
         type=cq:Page
         path=/content
         p.guessTotal=100
         ```
   쿼리 실행이 빠르지만 결과 수가 큰 경우 p. `guessTotal` 는 쿼리 빌더 쿼리에 대한 중요한 최적화 기능입니다.

   `p.guessTotal=100` 처음 100개의 결과만 수집하도록 쿼리 빌더에게 지시하고 하나 이상의 결과가 있는지 여부를 나타내는 부울 플래그를 설정합니다(이 수를 카운트하면 속도가 느려질 수 있으므로 더 이상 몇 개가 되지 않음). 이러한 최적화는 페이지 매김 또는 결과 하위 집합만 점진적으로 표시되는 무제한 로드 사용 사례를 능가합니다.

## 기존 인덱스 조정 {#existing-index-tuning}

1. 최적 쿼리가 속성 색인으로 확인되면 속성 인덱스가 최소로 조정 가능하므로 수행할 작업이 남아 있지 않습니다.
1. 그렇지 않으면 쿼리는 Lucene 속성 색인으로 확인되어야 합니다. 색인을 확인할 수 없으면 새 색인 만들기로 이동합니다.
1. 필요에 따라 쿼리를 XPath 또는 JCR 파섹-SQL2로 변환합니다.

   * **쿼리 빌더 쿼리**

      * 
         ```
         query type=cq:Page
         path=/content/my-site/us/en
         property=jcr:content/contentType
         property.value=article-page
         orderby=@jcr:content/publishDate
         orderby.sort=desc
         ```
   * **Query Builder 쿼리에서 생성된 XPath**

      * 
         ```
         /jcr:root/content/my-site/us/en//element(*, cq:Page)[jcr:content/@contentType = 'article-page'] order by jcr:content/@publishDate descending
         ```


1. 최적화된 Lucene 속성 색인 정의를 생성하려면 XPath(또는 JCR-SQL2) [를](https://oakutils.appspot.com/generate/index) Oak 색인 정의 생성기에 입력합니다.

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

1. 생성된 정의를 추가 방식으로 기존 Lucene 속성 인덱스에 수동으로 병합합니다. 기존 구성은 다른 쿼리를 충족하는 데 사용될 수 있으므로 제거하지 않도록 주의하십시오.

   1. cq:Page(인덱스 관리자 사용)를 포함하는 기존 Lucene 속성 인덱스를 찾습니다. 이 경우, `/oak:index/cqPageLucene`됩니다.
   1. 최적화된 인덱스 정의(4단계)와 기존 인덱스(/oak:index/cqPageLucene) 간의 구성 델타를 식별하고 최적화된 인덱스의 누락된 구성을 기존 인덱스 정의에 추가합니다.
   1. AEM의 다시 인덱싱 우수 사례에 따라 이 인덱스 구성 변경으로 기존 컨텐츠가 영향을 받는지 여부를 기준으로 새로 고침 또는 다시 색인이 순서대로 적용됩니다.

## 새 색인 만들기 {#create-a-new-index}

1. 쿼리가 기존 Lucene 속성 색인으로 확인되지 않는지 확인합니다. 이 경우 조정 및 기존 색인에 대한 위의 섹션을 참조하십시오.
1. 필요에 따라 쿼리를 XPath 또는 JCR 파섹-SQL2로 변환합니다.

   * **쿼리 빌더 쿼리**

      * 
         ```
         type=myApp:Author
         property=firstName
         property.value=ira
         ```
   * **Query Builder 쿼리에서 생성된 XPath**

      * 
         ```
         //element(*, myApp:Page)[@firstName = 'ira']
         ```


1. 최적화된 Lucene 속성 색인 정의를 생성하려면 XPath(또는 JCR-SQL2) [를](https://oakutils.appspot.com/generate/index) Oak 색인 정의 생성기에 입력합니다.

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

   Oak 인덱스 정의를 관리하는 AEM 프로젝트에 새 색인에 대해 Oak 인덱스 정의 생성기에서 제공하는 XML 정의를 추가합니다(코드에 따라 Oak 색인 정의를 코드로 처리).

   일반적인 AEM 소프트웨어 개발 라이프사이클에 따라 새 인덱스를 배포 및 테스트하고 쿼리가 색인으로 확인되고 쿼리가 성능인지 확인합니다.

   이 색인이 처음 배포되면 AEM이 필요한 데이터로 색인을 채웁니다.

## 색인 없음 및 순회 쿼리는 언제 유효합니까? {#when-index-less-and-traversal-queries-are-ok}

AEM의 유연한 콘텐츠 아키텍처로 인해 컨텐츠 구조의 순차적 변화를 예측하고 방지하는 것이 적절하지 않습니다.

따라서 경로 제한 및 nodetype 제한을 조합하여 20개 **미만의 노드가 트래버스되는 것을 보장하는 경우를 제외하고 색인이 쿼리를 만족하는지 확인합니다.**

## 쿼리 개발 도구 {#query-development-tools}

### Adobe 지원 {#adobe-supported}

* **쿼리 빌더 디버거**

   * 쿼리 빌더 쿼리를 실행하고 지원 XPath를 생성하기 위한 WebUI(쿼리 설명 또는 Oak 색인 정의 생성기에서 사용)입니다.
   * /libs/cq/search/content/querydebug.html의 AEM에 [있음](http://localhost:4502/libs/cq/search/content/querydebug.html)

* **CRXDE Lite - 쿼리 툴**

   * XPath 및 JCR 파섹
   * /crx/de/index.jsp > 도구 > [쿼리](http://localhost:4502/crx/de/index.jsp) ...의 AEM에 있습니다.

* **[쿼리 설명](/help/sites-administering/operations-dashboard.md#explain-query)**

   * 지정된 XPATH 또는 JCR-SQL2 쿼리에 대한 자세한 설명(쿼리 계획, 쿼리 시간 및 결과 수)을 제공하는 AEM 작업 대시보드

* **[느린/인기 있는 쿼리](/help/sites-administering/operations-dashboard.md#query-performance)**

   * AEM에서 실행된 최근 느리고 인기 있는 쿼리를 나열하는 AEM 작업 대시보드

* **[색인 관리자](/help/sites-administering/operations-dashboard.md#the-index-manager)**

   * AEM 인스턴스에서 인덱스를 표시하는 AEM Operations WebUI;타깃팅되거나 증강 가능한 색인을 손쉽게 파악할 수 있습니다.

* **[로깅](/help/sites-administering/operations-dashboard.md#log-messages)**

   * 쿼리 빌더 로깅

      * `DEBUG @ com.day.cq.search.impl.builder.QueryImpl`
   * Oak 쿼리 실행 로깅

      * `DEBUG @ org.apache.jackrabbit.oak.query`


* **Apache Jackrabbit 쿼리 엔진 설정 OSGi 구성**

   * 쿼리 탐색을 위한 오류 동작을 구성하는 OSGi 구성
   * AEM에 위치: [/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService](http://localhost:4502/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService)

* **NodeCounter JMX Mbean**

   * AEM의 컨텐츠 트리에서 노드 수를 예상하는 데 사용되는 JMX MBean
   * /system/console/jmx/org.apache.jackrabbit.oak%3 [Aname%3DnodeCounter%2Ctype%3DNodeCounter의 AEM에 있음](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter)

### 커뮤니티 지원 {#community-supported}

* **[Oak 색인 정의 생성기](https://oakutils.appspot.com/generate/index)**

   * XPath 또는 JCR-SQL2 쿼리 문에서 최적의 Luence 속성 인덱스를 생성합니다.

* **[AEM Chrome 플러그인](https://chrome.google.com/webstore/detail/aem-chrome-plug-in/ejdcnikffjleeffpigekhccpepplaode?hl=en-US)**

   * Google Chrome 웹 브라우저 익스텐션은 실행된 쿼리 및 해당 쿼리 계획을 포함하여 요청별 로그 데이터를 브라우저의 개발 도구 콘솔에 표시합니다.
   * AEM [에 Sling Log Tracer 1.0.2+](https://sling.apache.org/downloads.cgi) 를 설치하고 활성화해야 합니다.

