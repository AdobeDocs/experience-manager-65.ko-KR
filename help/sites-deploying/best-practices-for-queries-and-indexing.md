---
title: 쿼리 및 색인 작성 우수 사례
seo-title: 쿼리 및 색인 작성 우수 사례
description: 이 문서에서는 색인 및 쿼리를 최적화하는 방법에 대한 지침을 제공합니다.
seo-description: 이 문서에서는 색인 및 쿼리를 최적화하는 방법에 대한 지침을 제공합니다.
uuid: 0609935a-4a72-4b8e-a28e-daede9fc05f4
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 3f06f7a1-bdf0-4700-8a7f-1d73151893ba
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# 쿼리 및 색인 작성 우수 사례{#best-practices-for-queries-and-indexing}

AEM 6의 Oak로의 전환과 함께 쿼리 및 색인이 관리되는 방식에 몇 가지 주요 변경 사항이 적용되었습니다. Jackrabbit 2에서 모든 컨텐츠는 기본적으로 인덱싱되었으며 자유롭게 쿼리할 수 있었습니다. Oak에서 인덱스는 `oak:index` 노드 아래에 수동으로 만들어야 합니다. 쿼리가 인덱스 없이 실행될 수 있지만 큰 데이터 집합의 경우 매우 느리게 실행되거나 중단됩니다.

이 문서에서는 색인을 만들 때뿐만 아니라 색인이 필요하지 않은 시기, 쿼리가 필요하지 않은 경우 쿼리를 사용하지 않는 기법 및 최적으로 수행하기 위한 지표 및 쿼리를 최적화하기 위한 팁을 설명합니다.

또한 쿼리 및 색인 작성에 [대한 Oak 설명서를 읽어야](/help/sites-deploying/queries-and-indexing.md)합니다. AEM 6의 새로운 개념인 색인뿐만 아니라, 이전 AEM 설치에서 코드를 마이그레이션할 때 고려해야 하는 Oak 쿼리에도 구문 차이가 있습니다.

## 쿼리 사용 시기 {#when-to-use-queries}

### 저장소 및 분류 디자인 {#repository-and-taxonomy-design}

저장소의 분류 체계를 디자인할 때 몇 가지 요인을 고려해야 합니다. 여기에는 액세스 제어, 로컬라이제이션, 구성 요소 및 페이지 속성 상속이 포함됩니다.

이러한 문제를 해결하는 택소노미를 디자인하는 동안 색인 디자인의 &quot;순차적 가능성&quot;도 고려해야 합니다. 이러한 상황에서 순회 기능은 경로를 기반으로 컨텐츠를 예측 가능하게 액세스할 수 있는 분류법의 기능입니다. 이렇게 하면 많은 쿼리를 실행해야 하는 시스템보다 유지 관리가 더 쉬워집니다.

또한 분류법을 디자인할 때 주문 중요성이 있는지 고려해야 합니다. 명시적 순서가 필요하지 않고 많은 수의 동기 노드가 예상될 경우 `sling:Folder` 또는 `oak:Unstructured`과 같이 순서가 지정되지 않은 노드 유형을 사용하는 것이 좋습니다. 주문이 필요한 경우 `nt:unstructured` 보다 `sling:OrderedFolder` 적절할 수 있습니다.

### 구성 요소의 쿼리 {#queries-in-components}

쿼리는 AEM 시스템에서 수행되는 보다 많은 과세 작업 중 하나일 수 있으므로 구성 요소에서 쿼리를 사용하지 않는 것이 좋습니다. 페이지가 렌더링될 때마다 여러 개의 쿼리가 실행되면 시스템의 성능이 저하될 수 있습니다. 구성 요소를 렌더링할 때 쿼리를 실행하지 않도록 다음 두 가지 전략을 사용할 수 있습니다.노드 **탐색** 및 **프리페치 결과**.

#### 노드 탐색 {#traversing-nodes}

저장소가 필요한 데이터의 위치를 미리 알 수 있도록 설계된 경우 필요한 경로에서 이 데이터를 검색하는 코드는 쿼리를 실행하지 않고 배포할 수 있습니다.

예를 들어 특정 카테고리 내에 맞는 컨텐츠를 렌더링할 수 있습니다. 카테고리의 항목을 표시하는 구성 요소를 채울 수 있도록 쿼리할 수 있는 카테고리 속성을 사용하여 컨텐츠를 구성하는 한 가지 방법이 있습니다.

더 나은 방법은 이 컨텐츠를 범주별로 구조화하여 수동으로 검색할 수 있도록 하는 것입니다.

예를 들어 컨텐츠가 다음과 유사한 분류법에 저장되어 있는 경우

```xml
/content/myUnstructuredContent/parentCategory/childCategory/contentPiece
```

노드를 간단히 검색할 수 있으며, `/content/myUnstructuredContent/parentCategory/childCategory` 노드의 하위 노드를 구문 분석하여 구성 요소를 렌더링하는 데 사용할 수 있습니다.

또한 작은 결과 세트 또는 단일 결과 세트를 처리할 때 쿼리를 작성하여 동일한 결과 세트를 반환하는 대신 저장소를 트래버스하고 필요한 노드를 수집하는 것이 더 빨라질 수 있습니다. 일반적으로 쿼리는 가능한 경우 사용하지 않아야 합니다.

#### 프리페치 결과 {#prefetching-results}

경우에 따라 구성 요소에 대한 컨텐트 또는 요구 사항에서는 필요한 데이터를 검색하는 방법으로 노드 통과의 사용을 허용하지 않습니다. 이러한 경우, 최종 사용자에 대해 최적의 성능을 보장하도록 구성 요소를 렌더링하기 전에 필요한 쿼리를 실행해야 합니다.

구성 요소에 필요한 결과를 작성 시 계산할 수 있고 컨텐츠가 변경될 기대 상태가 없는 경우 작성자가 대화 상자에 설정을 적용할 때 쿼리를 실행할 수 있습니다.

데이터나 컨텐츠가 정기적으로 변경되는 경우, 기본 데이터에 대한 업데이트를 위해 일정 또는 수신기를 통해 쿼리를 실행할 수 있습니다. 그런 다음 결과를 저장소의 공유 위치에 작성할 수 있습니다. 그런 다음 이 데이터가 필요한 모든 구성 요소는 런타임 시 쿼리를 실행하지 않고도 이 단일 노드에서 값을 가져올 수 있습니다.

## 쿼리 최적화 {#query-optimization}

인덱스를 사용하지 않는 쿼리를 실행하면 노드 통과에 대한 경고가 기록됩니다. 이 쿼리가 자주 실행될 경우 인덱스를 만들어야 합니다. 특정 쿼리가 사용 중인 인덱스를 확인하려면 쿼리 [설명 도구를](/help/sites-administering/operations-dashboard.md#explain-query) 사용하는 것이 좋습니다. 자세한 내용은 관련 검색 API에 대해 DEBUG 로깅을 활성화할 수 있습니다.

>[!NOTE]
>
>색인 정의를 수정한 후 인덱스를 다시 작성(다시 인덱스)해야 합니다. 인덱스 크기에 따라 완료하는 데 시간이 걸릴 수 있습니다.

복잡한 쿼리를 실행할 때 쿼리를 여러 개의 작은 쿼리로 분류하고 팩트 후에 코드를 통해 데이터를 연결하는 경우가 있을 수 있습니다. 이러한 경우에 대한 권장 사항은 두 접근 방식의 성능을 비교하여 해당 사용 사례에 더 적합한 옵션을 결정하는 것입니다.

AEM에서는 다음 세 가지 방법 중 하나로 쿼리를 작성할 수 있습니다.

* QueryBuilder [API를](/help/sites-developing/querybuilder-api.md) 통해(권장)
* XPath 사용(권장)
* SQL2 사용

모든 쿼리가 실행되기 전에 SQL2로 변환되지만 쿼리 변환 오버헤드가 최소화되므로 쿼리 언어를 선택할 때 가장 큰 문제는 개발 팀에서 가독성과 편안한 수준이 될 것입니다.

>[!NOTE]
>
>QueryBuilder를 사용할 때 기본적으로 결과 수가 결정되며, 이전 버전의 Jackrabbit에 비해 Oak에서 더 느려집니다. 이를 보상하려면 guessTotal 매개 변수를 [](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results)사용할 수 있습니다.

### 쿼리 설명 도구 {#the-explain-query-tool}

쿼리 언어와 마찬가지로 쿼리를 최적화하는 첫 번째 단계는 쿼리를 실행하는 방법을 이해하는 것입니다. 이 활동을 활성화하려면 작업 대시보드의 [일부인 쿼리 설명 도구를](/help/sites-administering/operations-dashboard.md#explain-query) 사용할 수 있습니다. 이 도구를 사용하면 쿼리를 연결하여 설명할 수 있습니다. 쿼리로 인해 실행 시간 및 인덱스가 사용될 경우 큰 저장소 문제 뿐만 아니라 문제가 발생할 경우 경고가 표시됩니다. 또한 이 도구는 설명 및 최적화할 수 있는 느리고 자주 사용되는 쿼리 목록을 로드할 수 있습니다.

### 쿼리에 대한 디버그 로깅 {#debug-logging-for-queries}

Oak에서 사용할 인덱스를 선택하는 방법과 쿼리 엔진이 실제로 쿼리를 실행하는 방법에 대한 자세한 내용을 보려면 **다음** 패키지에 대한 DEBUG 로깅 구성을 추가할 수 있습니다.

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

쿼리 디버깅이 완료되면 이 로거를 제거해야 합니다. 이렇게 하면 많은 작업이 출력되고 로그 파일로 디스크를 채울 수 있습니다.

이 방법에 대한 자세한 내용은 로깅 [설명서를](/help/sites-deploying/configure-logging.md)참조하십시오.

### 색인 통계 {#index-statistics}

Lucene은 각 인덱스에 있는 문서의 크기 및 수를 비롯하여 인덱싱된 컨텐츠에 대한 세부 정보를 제공하는 JMX bean을 등록합니다.

JMX Console에서 `https://server:port/system/console/jmx`

JMX 콘솔에 로그인하고 나면 Lucene Index **통계를** 검색하여 찾습니다. 다른 인덱스 통계는 IndexStats MBean에서 찾을 **수** 있습니다.

쿼리 통계에 대해 Oak 쿼리 통계라는 MBean을 **살펴보십시오**.

Luke와 같은 도구를 사용하여 색인을 [파지하려면](https://code.google.com/p/luke/)Oak 콘솔을 사용하여 색인을 파일 시스템 `NodeStore` 디렉토리로 덤프해야 합니다. 이 방법에 대한 지침은 Lucene 설명서를 [참조하십시오](https://jackrabbit.apache.org/oak/docs/query/lucene.html).

시스템에서 JSON 형식으로 색인을 추출할 수도 있습니다. 이렇게 하려면 `https://server:port/oak:index.tidy.-1.json`

### 쿼리 제한 {#query-limits}

**개발 중**

에 대해 낮은 임계값 설정 `oak.queryLimitInMemory` (예: 1000) 및 oak `queryLimitReads` (예: 5000)&quot;쿼리가 x 노드보다 많은 노드를 읽었음을 의미하는 UnsupportedOperationException을 히트할 때 고가의 쿼리를 최적화합니다.

이렇게 하면 리소스 사용량이 많은 쿼리(예: 어떤 인덱스도 지원하지 않거나 더 적은 포함 인덱스로 뒷받침되지 않음). 예를 들어 100만 개의 노드를 읽는 쿼리는 입출력을 증가시키고 전체 애플리케이션 성능에 부정적인 영향을 줍니다. 위의 제한으로 인해 실패한 모든 쿼리는 분석 및 최적화되어야 합니다.

#### **배포 후**{#post-deployment}

* 큰 노드 통과나 큰 더미 메모리 사용을 트리거하는 쿼리에 대한 로그를 모니터링합니다.&quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * 탐색 노드 수를 줄이기 위해 쿼리 최적화

* 큰 더미 메모리 사용을 트리거하는 쿼리에 대한 로그 모니터링:

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * Optimize the query to reduce the heap memory usage

AEM 6.0 - 6.2 버전의 경우 AEM 시작 스크립트의 JVM 매개 변수를 통해 노드 통과에 대한 임계값을 조정하여 큰 쿼리가 환경을 오버로드하지 못하도록 할 수 있습니다.

권장 값은 다음과 같습니다.

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

AEM 6.3에서 위의 2개 매개 변수는 미리 구성된 OOTB이며 OSGi QueryEngineSettings를 통해 유지될 수 있습니다.

추가 정보: [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## 효율적인 인덱스 작성을 위한 팁 {#tips-for-creating-efficient-indexes}

### 인덱스를 만들어야 합니까? {#should-i-create-an-index}

색인을 만들거나 최적화할 때 묻는 첫 번째 질문은 해당 상황에서 색인이 실제로 필요한지 여부입니다. 해당 쿼리를 한 번 또는 한 번만 실행하려는 경우 일괄 처리를 통해 시스템의 사용량이 적은 시간에 실행하는 것이 좋습니다.

색인을 만든 후 인덱싱된 데이터가 업데이트될 때마다 색인도 업데이트해야 합니다. 이 경우 시스템에 성능에 영향을 주므로 인덱스가 실제로 필요한 경우에만 색인을 만들어야 합니다.

또한 색인은 인덱스 내에 포함된 데이터가 충분히 고유한 경우에만 유용합니다. 책의 색인과 이 책의 주제를 고려해 보십시오. 텍스트의 주제 집합을 색인화하면 일반적으로 수백 또는 수천 개의 항목이 표시되므로 원하는 정보를 빠르게 찾을 수 있는 페이지 하위 집합으로 빠르게 이동할 수 있습니다. 해당 색인에 2~3개의 응모만 있으면 각각 수백 개의 페이지를 가리키는 색인은 별로 유용하지 않습니다. 이와 동일한 개념이 데이터베이스 인덱스에 적용됩니다. 고유 값이 두 개만 있는 경우 색인은 매우 유용하지 않습니다. 즉, 색인이 너무 커서 유용할 수 없다는 것이다. 인덱스 통계를 보려면 위의 [인덱스 통계를](/help/sites-deploying/best-practices-for-queries-and-indexing.md#index-statistics) 참조하십시오.

### Lucene 또는 속성 인덱스? {#lucene-or-property-indexes}

Lucene 색인은 Oak 1.0.9에서 도입되었으며 AEM 6의 초기 실행 시 도입된 속성 색인에 비해 몇 가지 강력한 최적화를 제공합니다. Lucene 색인이나 속성 색인을 사용할지 여부를 결정할 때는 다음 사항을 고려하십시오.

* Lucene 색인은 속성 색인보다 많은 기능을 제공합니다. 예를 들어 속성 색인은 단일 속성만 색인화할 수 있고 Lucene 색인은 여러 개를 포함할 수 있습니다. Lucene 색인에서 사용 가능한 모든 기능에 대한 자세한 내용은 [설명서를](https://jackrabbit.apache.org/oak/docs/query/lucene.html)참조하십시오.
* Lucene 색인은 비동기적입니다. 이 기능은 상당한 성능 향상을 제공하지만, 데이터를 저장소에 기록하는 시기와 색인이 업데이트되는 시기 사이에 지연을 유발할 수도 있습니다. 쿼리가 100% 정확한 결과를 반환하도록 해야 하는 경우 속성 인덱스가 필요합니다.
* 비동기적 관계로 Lucene 색인은 고유성 제약 조건을 적용할 수 없습니다. 필요한 경우 속성 색인을 배치해야 합니다.

일반적으로 속성 색인을 사용해야 하는 특별한 필요가 없는 한 Lucene 색인을 사용하는 것이 좋습니다. 그러면 더 높은 성능과 유연성을 얻을 수 있습니다.

### 솔루션 인덱싱 {#solr-indexing}

AEM에서는 기본적으로 솔루션 인덱싱을 지원합니다. 전체 텍스트 검색을 지원하는 데 주로 사용되지만 모든 유형의 JCR 쿼리를 지원하는 데 사용할 수도 있습니다. AEM 인스턴스에 동시 사용자가 많은 검색 기반 웹 사이트와 같은 검색 중심 배포에 필요한 쿼리 수를 처리할 수 있는 CPU 용량이 없는 경우를 고려해야 합니다. 또는 Solr를 크롤러 기반 접근 방식으로 구현하여 플랫폼의 일부 고급 기능을 활용할 수 있습니다.

솔루션 색인은 개발 환경을 위해 AEM 서버에 임베드된 상태로 실행하도록 구성하거나 원격 인스턴스로 오프로드하여 프로덕션 및 스테이징 환경에서 검색 확장성을 향상시킬 수 있습니다. 검색을 오프로드하면 확장성이 향상되지만 지연이 발생합니다. 따라서 필요한 경우가 아니면 권장되지 않습니다. Solr 통합을 구성하는 방법과 Solr 인덱스를 만드는 방법에 대한 자세한 내용은 Oak Queries and [Indexing 설명서를](/help/sites-deploying/queries-and-indexing.md#the-solr-index)참조하십시오.

>[!NOTE]
>
>통합된 Solr 검색 방법을 사용하면 Solr 서버에 색인 로드를 해제할 수 있습니다. Solr 서버의 고급 기능이 Crawler 기반 접근 방식을 통해 사용되는 경우 추가 구성 작업이 필요합니다. Headwire는 이러한 유형의 구현을 가속화하기 위해 [오픈 소스 커넥터를](https://www.aemsolrsearch.com/#/) 만들었습니다.

이 접근 방법의 단점은 기본적으로 AEM 쿼리는 ACL을 존중하므로 사용자가 액세스할 수 없는 결과를 숨김하므로 Solr 서버에 대한 검색을 외부화하면 이 기능이 지원되지 않는다는 것입니다. 이러한 방식으로 검색이 외부화되려면 사용자에게 표시되지 않아야 하는 결과가 표시되지 않도록 각별히 주의해야 합니다.

이 접근 방식이 적절할 수 있는 잠재적인 사용 사례는 여러 소스의 검색 데이터를 집계해야 할 수 있습니다. 예를 들어, AEM에서 호스팅되는 사이트와 타사 플랫폼에서 호스팅되는 두 번째 사이트가 있을 수 있습니다. 두 사이트의 컨텐츠를 크롤하고 집계된 인덱스에 저장하도록 솔루션을 구성할 수 있습니다. 이를 통해 사이트 간 검색을 수행할 수 있습니다.

### 디자인 고려 사항 {#design-considerations}

Lucene 색인에 대한 Oak 설명서에는 색인을 디자인할 때 고려해야 할 몇 가지 사항이 나열되어 있습니다.

* 쿼리에서 다른 경로 제한을 사용하는 경우 를 `evaluatePathRestrictions`사용합니다. 이렇게 하면 쿼리가 지정된 경로 아래의 결과 하위 집합을 반환한 다음 쿼리를 기반으로 필터링할 수 있습니다. 그렇지 않으면 쿼리는 저장소의 쿼리 매개 변수와 일치하는 모든 결과를 검색한 다음 경로를 기반으로 필터링합니다.
* 쿼리에서 정렬을 사용하는 경우 정렬된 속성에 대한 명시적인 속성 정의를 `ordered` 가지고 `true` 이에 대해 설정합니다. 이렇게 하면 결과가 인덱스와 같이 정렬되고 쿼리 실행 시 비용이 많이 드는 정렬 작업을 저장할 수 있습니다.

* 필요한 것만 색인에 넣어주세요 불필요한 기능 또는 속성을 추가하면 인덱스가 커지고 성능이 저하됩니다.
* 속성 인덱스에서 고유한 속성 이름을 갖는 것은 인덱스의 크기를 줄이는 데 도움이 되지만 Lucene 인덱스의 경우, 응집적인 색인을 얻기 위해 를 사용하고 `nodeTypes` 있어야 `mixins` 합니다. 특정 `nodeType` 또는 특정 쿼리 `mixin` 작업은 쿼리하는 것보다 더 많은 성능이 `nt:base`됩니다. 이 방법을 사용할 때는 `indexRules` 해당 `nodeTypes` 항목에 대해 정의합니다.

* 쿼리가 특정 경로에서만 실행되는 경우 해당 경로 아래에 해당 인덱스를 만듭니다. 인덱스는 저장소의 루트에서 라이브할 필요가 없습니다.
* 인덱싱되는 모든 속성이 기본적으로 Lucene이 가능한 많은 속성 제한을 평가할 수 있도록 하려면 단일 인덱스를 사용하는 것이 좋습니다. 또한 조인을 수행하는 경우에도 쿼리는 하나의 색인만 사용합니다.

### CopyOnRead {#copyonread}

In case `NodeStore` is stored remote, the option called `CopyOnRead` can be enabled. 이 옵션을 선택하면 원격 인덱스가 로컬 파일 시스템에 기록됩니다. 이렇게 하면 이러한 원격 인덱스에 대해 종종 실행되는 쿼리의 성능을 개선하는 데 도움이 될 수 있습니다.

LuceneIndexProvider 서비스 아래의 OSGi 콘솔에서 구성할 수 **있으며** 기본적으로 Oak 1.0.13으로 활성화됩니다.

### 인덱스 제거 {#removing-indexes}

인덱스를 제거할 때는 항상 속성을 로 설정하고 실제로 삭제하기 전에 응용 프로그램이 제대로 작동하는지 확인하기 위해 테스트를 수행하여 인덱스를 일시적으로 비활성화하는 것이 좋습니다. `type` `disabled` 색인은 비활성화되어 있는 동안 업데이트되지 않으므로, 다시 활성화되고 색인을 다시 설정해야 하는 경우 올바른 내용이 없을 수 있습니다.

TarMK 인스턴스에서 속성 인덱스를 제거한 후 사용 중인 디스크 공간을 다시 확보하기 위해 컴포지션을 실행해야 합니다. Lucene 인덱스의 경우 실제 인덱스 컨텐츠는 BlobStore에 있으므로 데이터 저장소 가비지 수집이 필요합니다.

MongoDB 인스턴스에서 인덱스를 제거하면 삭제 비용이 인덱스의 노드 수에 비례합니다. 큰 인덱스를 삭제하면 문제가 발생할 수 있으므로 유지 관리 기간 중에만 **oak-mongo.js와 같은 도구를 사용하여 인덱스를 비활성화하고 삭제하는 것이 좋습니다**. 이 방법은 데이터 불일치를 도입할 수 있으므로 일반 노드 컨텐츠에 사용해서는 안 됩니다.

>[!NOTE]
>
>oak-mongo.js에 대한 자세한 내용은 Oak [설명서의 명령줄 도구 섹션을](https://jackrabbit.apache.org/oak/docs/command_line.html) 참조하십시오.

## 다시 인덱싱 {#re-indexing}

이 섹션에서는 Oak 색인을 다시 색인화할 수 있는 **이유만** 간략히 설명합니다.

아래에 설명된 이유 외에도 Oak 색인의 재색인을 시작하는 것은 동작을 변경하거나 문제를 해결하지 **않으며** AEM의 로드를 일시적으로 늘립니다.

Oak 색인의 재인덱스는 아래 표에 있는 이유로 설명되지 않는 한 회피됩니다.

>[!NOTE]
>
>색인화를 확인하기 위해 아래 표를 살펴보기 전에 유용한 정보를 확인하십시오.*** 항상 **verify:
>
>* 쿼리가 올바르다
>* 쿼리가 필요한 인덱스로 확인됩니다(쿼리 [설명 사용](/help/sites-administering/operations-dashboard.md#diagnosis-tools)).
>* 색인 프로세스가 완료되었습니다.
>



### Oak 인덱스 구성 변경 사항 {#oak-index-configuration-changes}

Oak 색인의 재색인에 대해 허용되는 유일한 예외 조건은 Oak 인덱스의 구성이 변경된 경우입니다.

*재인덱스는 항상 AEM의 전체 성능에 미치는 영향을 적절히 고려하여 접근해야 하며, 활동이 낮거나 유지 관리 기간이 낮은 기간 동안 수행해야 합니다.*

다음과 같은 세부 사항이 해상도와 함께 발생할 수 있습니다.

* [속성 인덱스 정의 변경](#property-index-definition-change)
* [Lucene 색인 정의 변경](#lucene-index-definition-change)

#### 속성 인덱스 정의 변경 {#property-index-definition-change}

* 적용 대상/조건:

   * 모든 Oak 버전
   * 속성 [색인만](https://jackrabbit.apache.org/oak/docs/query/property-index.html)

* 증상:

   * 속성 인덱스의 정의 업데이트 이전에 존재하는 노드가 결과에서 누락되었습니다.

* 확인 방법:

   * 업데이트된 인덱스 정의를 배포하기 전에 누락된 노드가 만들어졌는지/수정되었는지 확인합니다.
   * 인덱스의 수정된 시간에 대해 누락된 노드의 `jcr:created` 또는 `jcr:lastModified` 속성을 확인합니다.

* 해결 방법:

   * [lucene 색인의 다시](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-re-index) 색인을 지정합니다.
   * 또는 누락된 노드에 대해 터치(양성 쓰기 작업 수행)합니다.

      * 수동 수정 또는 사용자 정의 코드 필요
      * 누락된 노드 집합을 알려야 합니다.
      * 노드의 속성을 변경해야 합니다.

#### Lucene 색인 정의 변경 {#lucene-index-definition-change}

* 적용 대상/조건:

   * 모든 Oak 버전
   * Lucene [색인만](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* 증상:

   * Lucene 색인에 예상 결과가 없습니다.
   * 쿼리 결과는 인덱스 정의의 예상 동작을 반영하지 않습니다.
   * 인덱스 정의에 따라 쿼리 계획이 예상 출력을 보고하지 않음

* 확인 방법:

   * Lucene Index 통계 JMX Mbean(LuceneIndex) 메서드를 사용하여 인덱스 정의가 변경되었는지 `diffStoredIndexDefinition`확인합니다.

* 해결 방법:

   * 1.6 이전 Oak 버전:

      * [lucene 색인의 다시](#how-to-re-index) 색인을 지정합니다.
   * Oak 버전 1.6+

      * 기존 컨텐츠가 변경 사항으로 영향을 받지 않으면 새로 고침만 필요합니다.

         * [oak](https://jackrabbit.apache.org/oak/docs/query/lucene.html#stored-index-definition) :queryIndexDefinition@refresh=true를 설정하여 [lucene 인덱스를 새로 고칩니다].
      * 그렇지 않은 경우 [lucene 색인을 다시](#how-to-re-index) 색인화합니다.

         * 참고:마지막 올바른 다시 인덱싱(또는 초기 인덱싱)의 인덱스 상태는 새로운 다시 인덱싱을 트리거할 때까지 사용됩니다



### 예외 및 적용 {#erring-and-exceptional-situations}

다음 표에서는 Oak 색인을 다시 색인화하면 문제가 해결되는 허용 가능한 예외 상황만 설명합니다.

아래 설명된 기준과 일치하지 않는 AEM에 문제가 발생하면 문제를 해결하지 않으므로 색인을 다시 색인화하지 **마십시오** .

다음과 같은 세부 사항이 해상도와 함께 발생할 수 있습니다.

* [Lucene 인덱스 바이너리가 없습니다.](#lucene-index-binary-is-missing)
* [Lucene 인덱스 바이너리가 손상되었습니다.](#lucene-index-binary-is-corrupt)

#### Lucene 인덱스 바이너리가 없습니다. {#lucene-index-binary-is-missing}

* 적용 대상/조건:

   * 모든 Oak 버전
   * Lucene [색인만](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* 증상:

   * Lucene 색인에 예상 결과가 없습니다.

* 확인 방법:

   * 오류 로그 파일에 Lucene 인덱스의 바이너리가 누락되었다는 예외가 있습니다.

* 해결 방법:

   * 저장소 검사 탐색 수행;예를 들면 다음과 같습니다.

      [http://localhost:4502/system/console/repositorycheck](http://localhost:4502/system/console/repositorycheck)

      저장소 탐색을 통해 다른 이진 파일(lucene 파일 제외)이 누락되었는지 확인합니다.

   * lucene 인덱스 이외의 바이너리가 없는 경우 백업에서 복원
   * 그렇지 않은 경우 [모든](#how-to-re-index) Lucene 색인을 다시 색인화합니다 ** .
   * 메모:

      이 조건은 ANY 바이너리(예: 자산 이진 파일)이 없습니다.

      이 경우 마지막으로 알려진 저장소 올바른 버전으로 복원하여 누락된 모든 바이너리를 복구합니다.

#### Lucene 인덱스 바이너리가 손상되었습니다. {#lucene-index-binary-is-corrupt}

* 적용 대상/조건:

   * 모든 Oak 버전
   * Lucene [색인만](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* 증상:

   * Lucene 색인에 예상 결과가 없습니다.

* 확인 방법:

   * error.log에서 예외가 발생하여 `AsyncIndexUpdate` (매 5초)가 실패합니다.

      `...a Lucene index file is corrupt...`

* 해결 방법:

   * lucene 인덱스의 로컬 복사본 제거

      1. AEM 중지
      1. lucene 색인의 로컬 복사본을 삭제합니다. `crx-quickstart/repository/index`
      1. AEM 다시 시작
   * 이 경우 문제가 해결되지 않고 예외가 `AsyncIndexUpdate` 지속되는 경우:

      1. [참조 색인 다시](#how-to-re-index) 색인
      1. Adobe 지원 [티켓](https://helpx.adobe.com/support.html) 파일


### 다시 색인화하는 방법 {#how-to-re-index}

>[!NOTE]
>
>AEM 6.5에서 [oak-run.jar는 MongoMK 또는 RDBMK 저장소에서 재인덱싱을 위해 지원되는 유일한 방법입니다](/help/sites-deploying/indexing-via-the-oak-run-jar.md#reindexingapproachdecisiontree) .

#### 속성 인덱스 다시 인덱싱 {#re-indexing-property-indexes}

* oak-run.jar [](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) 를 사용하여 속성 색인을 다시 색인화합니다.
* 속성 인덱스에서 async-reindex 속성을 true로 설정합니다.

   * `[oak:queryIndexDefinition]@reindex-async=true`

* PropertyIndexAsyncReindex MBean을 통해 웹 콘솔을 사용하여 **속성** 인덱스를 비동기식으로 다시 인덱싱합니다.

   예,

   [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex)

#### Lucene 속성 인덱스 다시 인덱싱 {#re-indexing-lucene-property-indexes}

* oak- [run.jar를 사용하여 Lucene 속성 색인을 다시 색인화합니다](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) .
* lucene 속성 인덱스에서 async-reindex 속성을 true로 설정합니다.

   * `[oak:queryIndexDefinition]@reindex-async=true`

>[!NOTE]
>
>위의 섹션에서는 AEM 컨텍스트에서 Apache Oak [설명서의](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing) Oak 색인 지침을 요약하고 프레임을 만듭니다.

### 바이너리의 텍스트 사전 추출 {#text-pre-extraction-of-binaries}

텍스트 사전 추출은 분리된 프로세스를 통해 데이터 저장소에서 바로 바이너리에서 텍스트를 추출하고 처리한 다음 추출된 텍스트를 Oak 인덱스의 후속 다시 색인에 직접 노출시키는 프로세스입니다.

* 추출할 수 있는 텍스트(예: PDF, Word 문서, PPT, TXT 등) 배포되는 Oak 색인을 통해 전체 텍스트 검색을 수행할 수 있습니다.예를 `/oak:index/damAssetLucene`들면 다음과 같습니다.
* 속성 색인은 바이너리에서 텍스트를 추출하지 않으므로 텍스트 사전 추출은 Lucene 색인과 NOT Oak 속성 색인의 재정의에만 도움이 됩니다.
* 텍스트 사전 추출은 텍스트가 많은 바이너리(PDF, 문서, TXT 등)의 전체 텍스트 재인덱싱을 수행할 때 긍정적인 영향을 주므로 이미지 저장소로서 추출 가능한 텍스트를 포함하지 않으므로 동일한 효율성을 경험할 수 없습니다.
* 텍스트 사전 추출을 사용하면 전체 텍스트 검색 관련 텍스트를 보다 효율적으로 추출할 수 있으며 Oak 재작성 프로세스에 텍스트를 노출하여 매우 효율적으로 사용할 수 있습니다.

#### CAN text pre-extraction be used? {#when-can-text-pre-extraction-be-used}

이진 추출이 활성화된 **기존** Lucene 인덱스 다시 인덱싱

* 저장소의 **모든** 후보 컨텐츠를 다시 인덱싱 처리하며전체 텍스트를 추출할 바이너리가 많거나 복잡하면 전체 텍스트 추출을 수행하기 위한 계산 부담이 AEM에 배치됩니다. 텍스트 사전 추적은 AEM의 오버헤드 및 리소스 경합을 방지하여 텍스트 추출을 &quot;계산 시 비용이 많이 드는 작업&quot;하는 분리된 프로세스로 이동합니다.

이진 추출이 활성화된 **새** Lucene 색인을 AEM에 배포 지원

* 이진 추출을 사용하는 새 인덱스가 AEM에 배포되면 Oak는 다음 비동기 전체 텍스트 인덱스 실행에 대한 모든 후보 컨텐츠를 자동으로 인덱싱합니다. 위의 다시 색인화에 설명된 동일한 이유로 AEM에서 과도하게 로드될 수 있습니다.

#### 텍스트 사전 추출 기능은 언제 사용할 수 있습니까? {#when-can-text-pre-extraction-not-be-used}

저장소에 추가된 새 컨텐츠에는 텍스트 사전 추출을 사용할 수 없거나 사용할 필요가 없습니다.

새 컨텐츠가 저장소에 추가되면 비동기 전체 텍스트 인덱싱 프로세스(기본적으로 5초마다)에 의해 자연적으로 그리고 점진적으로 인덱스화됩니다.

웹 UI를 통해 자산을 업로드하거나 자산의 프로그래머틱 인제스트를 통해 AEM의 정상적인 작업 아래에서 AEM은 자동으로 그리고 점진적으로 새로운 바이너리 컨텐츠에 전체 텍스트 인덱스를 만듭니다. 데이터의 양이 증가하여 비교적 작으므로(약 5초 후에 보관될 수 있는 데이터의 양), AEM은 전체 시스템 성능에 영향을 주지 않고 색인 작성 중에 바이너리에서 전체 텍스트 추출을 수행할 수 있습니다.

#### 텍스트 사전 추출 사용을 위한 사전 요구 사항 {#prerequisites-to-using-text-pre-extraction}

* 전체 텍스트 이진 추출을 수행하는 lucene 인덱스를 다시 인덱싱하거나 기존 컨텐츠의 전체 텍스트 인덱스 바이너리를 수행하는 새 인덱스를 배포하게 됩니다
* 사전 추출할 텍스트가 저장소에 있어야 합니다.
* CSV 파일을 생성하고 최종 다시 색인을 수행하기 위한 유지 관리 창
* Oak 버전:1.0.18+, 1.2.3+
* [oak-run.](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)jarversion 1.7.4+
* 인덱싱 AEM 인스턴스에서 액세스할 수 있는 추출된 텍스트를 저장할 파일 시스템 폴더/공유

   * 텍스트 사전 추출 OSGi 구성은 압축을 푼 텍스트 파일에 대한 파일 시스템 경로가 필요하므로 AEM 인스턴스(로컬 드라이브 또는 파일 공유 마운트)에서 직접 액세스할 수 있어야 합니다

#### 텍스트 사전 추출 수행 방법 {#how-to-perform-text-pre-extraction}

>[!NOTE]
>
>***아래에 설명된 oak-run.jar 명령은 https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html에 모두 열거되어[있습니다.](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html)***
>
>아래 다이어그램과 단계에서는 Apache Oak 설명서에 나와 있는 기술 텍스트 사전 추출 단계를 설명하고 칭찬합니다.

![텍스트 사전 추출 프로세스 흐름](assets/chlimage_1-139.png)

**사전 추출할 컨텐츠 목록 생성**

*이 작업 중에 노드 스토어가 탐색되어 있을 때 유지 관리 기간/소용 기간 동안 단계 1(a-b)을 실행하면 시스템에 상당한 로드가 발생할 수 있습니다.*

1a. 텍스트를 미리 추출할 노드 목록을 `oak-run.jar --generate` 생성하려면 실행합니다.

1b. 노드 목록(1a)은 파일 시스템에 CSV 파일로 저장됩니다.

전체 노드 스토어는 실행될 때마다(oak-run 명령의 경로에 의해 지정된 대로) `--generate` 탐색되며 **새** CSV 파일이 만들어집니다. CSV 파일은 텍스트 사전 추출 프로세스의 개별 실행 간에 다시 사용되지 **않습니다** (단계 1 - 2).

**파일 시스템에 텍스트 사전 추출**

*2(a-c)단계는 데이터 스토어와만 상호 작용하므로 AEM의 정상적인 작업 중에 실행할 수 있습니다.*

2a. (1 `oak-run.jar --tika` b)에서 생성된 CSV 파일에 열거된 이진 노드에 대한 사전 추출 텍스트를 실행합니다.

2b. (2a)에서 시작된 프로세스는 데이터 저장소의 CSV에 정의된 이진 노드에 직접 액세스하여 텍스트를 추출합니다.

2c.  추출된 텍스트는 Oak 재인덱싱 프로세스(3a)에서 인제스트할 수 있는 형식으로 파일 시스템에 저장됩니다

사전 추출된 텍스트는 CSV에서 이진 지문으로 식별됩니다. 이진 파일이 같은 경우 AEM 인스턴스 전체에서 사전 추출된 동일한 텍스트를 사용할 수 있습니다. AEM 게시는 일반적으로 AEM 작성자의 하위 집합이므로 AEM 작성자의 사전 압축 해제된 텍스트를 사용하여 AEM 게시도 다시 색인화할 수 있습니다(AEM 게시에 압축을 푼 텍스트 파일에 대한 파일 시스템 액세스 권한이 있다고 가정).

미리 추출된 텍스트는 시간 경과에 따라 점진적으로 추가할 수 있습니다. 텍스트 사전 추출은 이전에 추출된 바이너리에 대해 추출 작업을 생략하므로, 추출된 컨텐츠가 절대 확장되지 않는다고 가정할 때 나중에 다시 색인화해야 하는 경우에 대비하여 사전 추출된 텍스트를 유지하는 것이 좋습니다. 이 경우 텍스트가 잘 압축되므로 중간에 있는 콘텐츠의 지퍼를 평가하십시오.

**추출된 텍스트 파일에서 전체 텍스트 소싱, Oak 인덱스 다시 인덱스**

*이 작업 중에 노드 스토어가 탐색되는 동안 유지 관리/저사용 기간 동안 다시 인덱싱(3a-b 단계)을 실행하면 시스템에 상당한 로드가 발생할 수 있습니다.*

3a. [AEM에서 Lucene 색인의 다시 색인이](#how-to-re-index) 호출됩니다.

3b. Apache Jackrabbit Oak DataStore PreExtractedTextProvider OSGi 구성(파일 시스템 경로를 통해 추출된 텍스트를 가리키도록 구성)은 Oak가 추출된 파일에서 전체 텍스트 소스를 공급하도록 지시하고 저장소에 저장된 데이터를 직접 히트하고 처리하지 않습니다.

