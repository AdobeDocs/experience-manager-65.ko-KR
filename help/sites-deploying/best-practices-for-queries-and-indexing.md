---
title: 쿼리 및 색인 생성에 대한 우수 사례
seo-title: Best Practices for Queries and Indexing
description: 이 문서에서는 인덱스 및 쿼리를 최적화하는 방법에 대한 지침을 제공합니다.
seo-description: This article provides guidelines on how to optimize your indexes and queries.
uuid: 0609935a-4a72-4b8e-a28e-daede9fc05f4
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 3f06f7a1-bdf0-4700-8a7f-1d73151893ba
exl-id: 6dfaa14d-5dcf-4e89-993a-8d476a36d668
source-git-commit: 52c8d4c425213718678543e9e9e8e5a4c2af4f95
workflow-type: tm+mt
source-wordcount: '4684'
ht-degree: 0%

---

# 쿼리 및 색인 생성에 대한 우수 사례{#best-practices-for-queries-and-indexing}

AEM 6의 Oak로 전환하는 것과 함께 쿼리 및 인덱스가 관리되는 방식에 몇 가지 주요 변경 사항이 수행되었습니다. Jackrabbit 2에서 모든 콘텐츠는 기본적으로 인덱싱되었으며 자유롭게 쿼리할 수 있습니다. Oak에서 인덱스는 `oak:index` 노드 아래에 있어야 합니다. 쿼리는 인덱스 없이 실행될 수 있지만 큰 데이터 세트의 경우 매우 느리게 실행되거나 중단됩니다.

이 문서에서는 색인을 작성할 때뿐만 아니라 색인이 필요하지 않은 시기, 쿼리가 필요하지 않은 경우 쿼리를 사용하지 않도록 하는 트릭 및 가능한 한 최적으로 수행하기 위해 색인과 쿼리를 최적화하는 팁에 대해 설명합니다.

또한 를 반드시 읽어 보십시오 [쿼리 및 색인 작성에 대한 Oak 설명서](/help/sites-deploying/queries-and-indexing.md). AEM 6에서 새로운 개념인 인덱스 외에도 이전 AEM 설치에서 코드를 마이그레이션할 때 고려해야 하는 Oak 쿼리에는 구문 차이가 있습니다.

## 쿼리를 사용해야 하는 경우 {#when-to-use-queries}

### 저장소 및 분류 체계 디자인 {#repository-and-taxonomy-design}

저장소의 분류 체계를 디자인할 때 몇 가지 요소를 고려해야 합니다. 여기에는 액세스 제어, 로컬라이제이션, 구성 요소 및 페이지 속성 상속이 포함됩니다.

이러한 문제를 해결하는 분류법을 디자인하는 동안 색인 설계의 &quot;순회 기능&quot;을 고려해야 합니다. 이 컨텍스트에서 순회 기능은 경로를 기반으로 컨텐츠를 예측 가능하게 액세스할 수 있는 분류법의 기능입니다. 이렇게 하면 많은 쿼리를 실행해야 하는 것보다 쉽게 유지 관리할 수 있는 성능 시스템이 향상됩니다.

또한 분류법을 디자인할 때는 순서 지정이 중요한지 고려해야 합니다. 명시적 순서가 필요하지 않고 동위 노드의 수가 많은 경우 다음과 같이 순서가 지정되지 않은 노드 유형을 사용하는 것이 좋습니다 `sling:Folder` 또는 `oak:Unstructured`. 주문이 필요한 경우, `nt:unstructured` 및 `sling:OrderedFolder` 더 적절할 것 같습니다

### 구성 요소의 쿼리 {#queries-in-components}

쿼리는 AEM 시스템에서 수행되는 더 많은 과세 작업 중 하나일 수 있으므로 구성 요소에서 쿼리를 피하는 것이 좋습니다. 페이지를 렌더링할 때마다 몇 개의 쿼리가 실행되면 시스템의 성능이 저하될 수 있습니다. 구성 요소를 렌더링할 때 쿼리를 실행하지 않도록 하는 두 가지 전략이 있습니다. **탐색 노드** 및 **프리페치 결과**.

#### 노드 탐색 {#traversing-nodes}

저장소가 필요한 데이터의 위치를 미리 알 수 있도록 설계된 경우 필요한 경로에서 이 데이터를 검색하는 코드를 배포하기 위해 쿼리를 실행하지 않고도 배포할 수 있습니다.

특정 카테고리에 맞는 콘텐츠를 렌더링하는 것이 예시입니다. 한 가지 방법은 컨텐츠를 카테고리의 항목을 표시하는 구성 요소를 채우기 위해 쿼리할 수 있는 카테고리 속성으로 구성하는 것입니다.

보다 나은 접근 방법은 이 컨텐츠를 카테고리별로 분류하여 수동으로 검색할 수 있도록 구성하는 것입니다.

예를 들어 다음과 유사한 분류법에 컨텐츠가 저장되는 경우

```xml
/content/myUnstructuredContent/parentCategory/childCategory/contentPiece
```

a `/content/myUnstructuredContent/parentCategory/childCategory` 노드를 간단히 검색할 수 있으며, 해당 하위 노드를 구문 분석하여 구성 요소를 렌더링하는 데 사용할 수 있습니다.

또한 작은 결과 세트 또는 균일한 결과 세트를 처리하는 경우 동일한 결과 세트를 반환하도록 쿼리를 만드는 대신 리포지토리를 트래버스하고 필요한 노드를 수집하는 것이 더 빠를 수 있습니다. 일반적으로 쿼리는 가능한 곳에서 피해야 합니다.

#### 프리페치 결과 {#prefetching-results}

경우에 따라 구성 요소에 대한 컨텐츠 또는 요구 사항에 따라 필요한 데이터를 검색하는 방법으로 노드 순회를 사용할 수 없습니다. 이 경우 최종 사용자에게 최적의 성능을 보장하기 위해 구성 요소를 렌더링하기 전에 필요한 쿼리를 실행해야 합니다.

구성 요소에 필요한 결과를 작성 시 계산할 수 있고 컨텐츠가 변경될 가능성이 없는 경우 작성자가 대화 상자에서 설정을 적용할 때 쿼리를 실행할 수 있습니다.

데이터 또는 컨텐츠가 정기적으로 변경되는 경우 기본 데이터에 대한 업데이트를 위해 일정 또는 수신기를 통해 쿼리를 실행할 수 있습니다. 그런 다음 리포지토리의 공유 위치에 결과를 쓸 수 있습니다. 이 데이터가 필요한 모든 구성 요소는 런타임 시 쿼리를 실행할 필요 없이 이 단일 노드에서 값을 가져올 수 있습니다.

## 쿼리 최적화 {#query-optimization}

인덱스를 사용하지 않는 쿼리를 실행하면 노드 순서와 관련하여 경고가 기록됩니다. 자주 실행되는 쿼리인 경우 인덱스를 만들어야 합니다. 주어진 쿼리에서 사용할 인덱스를 확인하려면 [쿼리 도구 설명](/help/sites-administering/operations-dashboard.md#explain-query) 이 권장됩니다. 자세한 내용은 관련 검색 API에 대해 DEBUG 로깅을 활성화할 수 있습니다.

>[!NOTE]
>
>인덱스 정의를 수정한 후 인덱스를 다시 작성(다시 인덱싱)해야 합니다. 인덱스 크기에 따라 완료하는 데 시간이 걸릴 수 있습니다.

복잡한 쿼리를 실행할 때 쿼리를 여러 개의 작은 쿼리로 분류하고 팩트가 더 뛰어난 성능을 발휘한 후 코드를 통해 데이터를 연결하는 경우가 있을 수 있습니다. 이러한 경우에 대한 권장 사항은 두 가지 접근 방식의 성능을 비교하여 해당 사용 사례에 더 적합한 옵션을 결정하는 것입니다.

AEM에서는 다음 세 가지 방법 중 하나로 쿼리를 쓸 수 있습니다.

* 를 통해 [QueryBuilder API](/help/sites-developing/querybuilder-api.md) (권장)
* XPath 사용(권장)
* SQL2 사용

모든 쿼리가 실행되기 전에 SQL2로 변환되지만 쿼리 변환의 오버헤드가 최소화되므로 쿼리 언어를 선택할 때 가장 큰 문제는 개발 팀에서 가독성과 편안함 수준입니다.

>[!NOTE]
>
>QueryBuilder를 사용할 때 기본적으로 결과 카운트가 결정되며, 이전 버전의 Jackrabbit에 비해 Oak에서는 더 느려집니다. 이를 보완하려면 [guessTotal 매개 변수](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results).

### 쿼리 설명 도구 {#the-explain-query-tool}

모든 쿼리 언어와 마찬가지로 쿼리를 최적화하는 첫 번째 단계는 쿼리 실행 방법을 이해하는 것입니다. 이 활동을 활성화하려면 [쿼리 도구 설명](/help/sites-administering/operations-dashboard.md#explain-query) 작업 대시보드의 일부입니다. 이 도구를 사용하면 쿼리를 연결하고 설명할 수 있습니다. 쿼리가 실행 시간 및 사용할 색인뿐만 아니라 큰 저장소에 문제가 발생하는지 여부를 묻는 경고가 표시됩니다. 또한 이 도구는 설명하고 최적화할 수 있는 느리고 자주 사용하는 쿼리 목록을 로드할 수 있습니다.

### 쿼리에 대한 디버그 로깅 {#debug-logging-for-queries}

Oak에서 사용할 인덱스를 선택하는 방법과 쿼리 엔진이 실제로 쿼리를 실행하는 방법에 대한 추가 정보를 보려면 **디버그** 다음 패키지에 대해 로깅 구성을 추가할 수 있습니다.

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

쿼리 디버깅을 완료하면 많은 작업이 출력되고 결과적으로 로그 파일로 디스크를 채울 수 있으므로 이 로거를 제거해야 합니다.

이 작업을 수행하는 방법에 대한 자세한 내용은 [로깅 설명서](/help/sites-deploying/configure-logging.md).

### 인덱스 통계 {#index-statistics}

Lucene은 각 인덱스에 있는 문서의 크기 및 수를 비롯하여 인덱싱된 컨텐츠에 대한 세부 정보를 제공하는 JMX Bean을 등록합니다.

에 있는 JMX 콘솔에 액세스하면 여기에 도달할 수 있습니다 `https://server:port/system/console/jmx`

JMX 콘솔에 로그인하고 나면 다음을 검색합니다. **Lucene 인덱스 통계** 찾기 위해서 다른 인덱스 통계는 **IndexStats** MBean.

쿼리 통계를 보려면 이름이 인 MBean을 참조하십시오. **Oak 쿼리 통계**.

와 같은 도구를 사용하여 인덱스를 검색하려면 [루크](https://code.google.com/p/luke/)를 채울 때는 Oak 콘솔을 사용하여 색인을 `NodeStore` 파일 시스템 디렉토리에 추가합니다. 이 작업을 수행하는 방법에 대한 지침은 [Lucene 설명서](https://jackrabbit.apache.org/oak/docs/query/lucene.html).

시스템의 인덱스를 JSON 형식으로 추출할 수도 있습니다. 이를 수행하려면 다음을 수행해야 합니다 `https://server:port/oak:index.tidy.-1.json`

### 쿼리 제한 {#query-limits}

**개발 중**

에 대한 낮은 임계값 설정 `oak.queryLimitInMemory` (예: 10000)과 oak가 포함된 URL이 있는지 확인합니다. `queryLimitReads` (예: 5000)을 사용하여 &quot;쿼리가 x 노드보다 많이 읽었습니다..&quot;라는 UnsupportedOperationException을 누를 때 고가의 쿼리를 최적화할 수 있습니다.

이렇게 하면 리소스 집약적인 쿼리(예: 어떤 인덱스도 지원하지 않거나 더 적은 커버 인덱스로 백업되지 않음) 예를 들어, 100만 개의 노드를 읽는 쿼리는 입출력을 높이고 전체 애플리케이션 성능에 부정적인 영향을 줍니다. 위의 제한으로 인해 실패하는 모든 쿼리는 분석 및 최적화되어야 합니다.

#### **배포 후** {#post-deployment}

* 큰 노드 순회 또는 큰 힙메모리 소비를 트리거하는 쿼리에 대한 로그를 모니터링합니다. &quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * 쿼리를 최적화하여 탐색 노드 수를 줄입니다

* 큰 힙메모리 소비를 트리거하는 쿼리에 대한 로그를 모니터링합니다.

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * 쿼리를 최적화하여 힙메모리 소비를 줄입니다.

AEM 6.0 - 6.2 버전의 경우, AEM 시작 스크립트에서 JVM 매개 변수를 통해 노드 순번의 임계값을 조정하여 큰 쿼리가 환경을 오버로드하지 못하도록 할 수 있습니다.

권장되는 값은 입니다.

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

AEM 6.3에서 위의 2개 매개 변수는 사전 구성된 OOTB이며 OSGi QueryEngineSettings 를 통해 유지할 수 있습니다.

다음에서 추가 정보를 사용할 수 있습니다. [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## 효율적인 인덱스를 만드는 팁 {#tips-for-creating-efficient-indexes}

### 인덱스를 만들어야 합니까? {#should-i-create-an-index}

인덱스를 만들거나 최적화할 때 가장 먼저 묻는 질문은 주어진 상황에서 색인이 실제로 필요한지 여부입니다. 일괄 처리 프로세스를 통해 시스템에 대해 한 번 또는 한 번 또는 한 번 또는 가끔 그리고 비스파이크 시간에만 해당 쿼리를 실행하려는 경우 인덱스를 전혀 만들지 않는 것이 좋습니다.

인덱스를 만든 후에는 인덱싱된 데이터가 업데이트될 때마다 색인도 업데이트해야 합니다. 이 경우 시스템에 성능 영향을 주므로 실제로 필요한 경우에만 인덱스를 만들어야 합니다.

또한 색인은 색인에 포함된 데이터가 충분히 고유한 경우에만 유용합니다. 책의 색인과 이 책의 주제를 고려하십시오. 텍스트에서 주제 집합을 인덱싱할 때 일반적으로 수백 또는 수천 개의 항목이 있으며, 이를 통해 페이지 하위 집합으로 빠르게 이동하여 찾고 있는 정보를 빠르게 찾을 수 있습니다. 해당 색인에 2~3개의 항목만 포함되어 있으면 각각 수백 페이지를 가리키면 색인이 별로 유용하지 않을 것입니다. 이러한 개념은 데이터베이스 인덱스에 적용됩니다. 두 개의 고유한 값만 있는 경우 색인은 매우 유용하지 않습니다. 즉, 색인이 너무 커서 유용할 수 없다는 것이다. 인덱스 통계를 확인하려면 [인덱스 통계](/help/sites-deploying/best-practices-for-queries-and-indexing.md#index-statistics) 위에 표시됩니다.

### Lucene 또는 속성 인덱스? {#lucene-or-property-indexes}

Lucene 인덱스는 Oak 1.0.9에서 도입되었으며 AEM 6의 초기 시작 시 도입된 속성 인덱스에 대해 몇 가지 강력한 최적화를 제공합니다. Lucene 인덱스 또는 속성 인덱스를 사용할지 결정할 때 다음 사항을 고려하십시오.

* Lucene 색인은 속성 색인보다 많은 기능을 제공합니다. 예를 들어 속성 인덱스는 단일 속성만 색인화할 수 있고 Lucene 인덱스는 여러 항목을 포함할 수 있습니다. Lucene 색인에서 사용할 수 있는 모든 기능에 대한 자세한 내용은 [설명서](https://jackrabbit.apache.org/oak/docs/query/lucene.html).
* Lucene 인덱스는 비동기적입니다. 이렇게 하면 상당한 성능 향상을 제공할 수 있지만, 데이터를 리포지토리에 쓰는 시간과 인덱스를 업데이트하는 시점 사이에 지연을 초래할 수도 있습니다. 쿼리에서 100% 정확한 결과를 반환해야 하는 경우에는 속성 인덱스가 필요합니다.
* 비동기성을 통해 Lucene 인덱스는 고유성 제약 조건을 적용할 수 없습니다. 필요한 경우 속성 인덱스를 제자리에 두어야 합니다.

일반적으로 높은 성능과 유연성을 얻을 수 있도록 속성 인덱스를 사용해야 할 특별한 필요가 없는 한 Lucene 인덱스를 사용하는 것이 좋습니다.

### 솔루션 색인 지정 {#solr-indexing}

AEM에서는 기본적으로 솔루션 색인화를 지원합니다. 주로 전체 텍스트 검색을 지원하는 데 활용되지만, 모든 유형의 JCR 쿼리를 지원하는 데 사용할 수도 있습니다. 동시 사용자가 많은 검색 기반 웹 사이트와 같이 검색 집약적인 배포에 필요한 쿼리 수를 처리할 CPU 용량이 AEM 인스턴스에 없는 경우 문제를 고려해야 합니다. 또는 Solr을 Crawler 기반 접근 방식으로 구현하여 플랫폼의 일부 고급 기능을 활용할 수 있습니다.

솔루션 인덱스는 개발 환경을 위해 AEM 서버에 임베디드 상태로 실행하도록 구성하거나 원격 인스턴스에 오프로드하여 프로덕션 및 스테이징 환경에서 검색 확장성을 향상시킬 수 있습니다. 검색을 오프로드하면 확장성이 향상되지만 지연이 발생하고 있으므로 필수가 아닌 한 권장되지 않습니다. Solr 통합을 구성하는 방법 및 Solr 인덱스를 만드는 방법에 대한 자세한 내용은 [Oak 쿼리 및 색인 지정 설명서](/help/sites-deploying/queries-and-indexing.md#the-solr-index).

>[!NOTE]
>
>통합 Solr 검색 방법을 사용하면 Solr 서버에 대한 색인을 해제할 수 있습니다. Crawler 기반 접근 방식을 통해 Solr 서버의 고급 기능을 사용하는 경우 추가 구성 작업이 필요합니다. 헤드와이어는 [오픈 소스 커넥터](https://www.aemsolrsearch.com/#/) 를 사용하면 이러한 유형의 구현을 가속화할 수 있습니다.

이 방법을 사용하는 데는 기본적으로 AEM 쿼리가 ACL을 준수하므로 사용자가 액세스할 수 없는 결과를 숨기므로 Solr 서버에 대한 검색을 외부화하면 이 기능이 지원되지 않는다는 단점이 있습니다. 이러한 방식으로 검색을 외부화하려면 사용자가 표시되지 않아야 하는 결과가 표시되지 않도록 추가 조치를 취해야 합니다.

이 접근 방식이 적절할 수 있는 잠재적인 사용 사례는 여러 소스의 검색 데이터를 집계해야 하는 경우입니다. 예를 들어 AEM에서 호스팅되는 사이트와 타사 플랫폼에서 호스팅되는 두 번째 사이트가 있을 수 있습니다. 두 사이트의 컨텐츠를 크롤링하고 집계된 인덱스에 저장하도록 솔러를 구성할 수 있습니다. 이렇게 하면 사이트 간 검색이 허용됩니다.

### 디자인 고려 사항 {#design-considerations}

Lucene 인덱스에 대한 Oak 설명서는 인덱스를 디자인할 때 고려해야 할 몇 가지 고려 사항을 나열합니다.

* 쿼리에서 다른 경로 제한을 사용하는 경우 `evaluatePathRestrictions`. 이렇게 하면 쿼리에서 지정된 경로 아래에 결과의 하위 집합을 반환한 다음 쿼리를 기준으로 필터링할 수 있습니다. 그렇지 않으면 쿼리에서 저장소의 쿼리 매개 변수와 일치하는 모든 결과를 검색한 다음 경로를 기준으로 필터링합니다.
* 쿼리에서 정렬을 사용하는 경우 정렬된 속성에 대한 명시적 속성 정의를 지정하고 설정합니다 `ordered` to `true` 활성화해줄 수 있습니다. 이렇게 하면 인덱스의 결과와 같은 순서로 결과를 정렬하고 쿼리 실행 시 비용이 많이 드는 정렬 작업을 저장할 수 있습니다.

* 필요한 것만 색인에 넣어주세요 필요하지 않은 기능 또는 속성을 추가하면 색인이 커지고 성능이 저하됩니다.
* 속성 인덱스에서 고유한 속성 이름을 갖는 는 인덱스의 크기를 줄이는 데 도움이 되지만 Lucene 인덱스의 경우 `nodeTypes` 및 `mixins` 응집력 있는 색인을 달성하기 위해 만들어져야 한다. 특정 쿼리 `nodeType` 또는 `mixin` 쿼리보다 성능이 더 뛰어납니다 `nt:base`. 이 방법을 사용하는 경우 `indexRules` 대상 `nodeTypes` 문제.

* 쿼리가 특정 경로에서만 실행되는 경우 해당 경로 아래에 해당 인덱스를 만듭니다. 인덱스가 저장소의 루트에 있을 필요는 없습니다.
* 인덱싱되는 모든 속성이 Lucene에서 기본적으로 가능한 한 많은 속성 제한을 평가할 수 있도록 관련 있는 경우 단일 인덱스를 사용하는 것이 좋습니다. 또한 조인을 수행할 때에도 쿼리는 하나의 색인만 사용합니다.

### CopyOnRead {#copyonread}

다음의 경우 `NodeStore` 원격 저장 후 `CopyOnRead` 사용할 수 있습니다. 이 옵션을 선택하면 원격 인덱스가 로컬 파일 시스템에 기록되어 읽기가 수행됩니다. 이렇게 하면 이러한 원격 인덱스에 대해 자주 실행되는 쿼리의 성능을 개선하는 데 도움이 될 수 있습니다.

OSGi 콘솔에서 다음과 같이 구성할 수 있습니다. **LuceneIndexProvider** Oak 1.0.13부터 서비스 및 가 기본적으로 활성화되어 있습니다.

### 인덱스 제거 {#removing-indexes}

인덱스를 제거할 때는 항상 `type` 속성 대상 `disabled` 및 를 테스트하여 실제로 삭제하기 전에 애플리케이션이 올바르게 작동하는지 확인합니다. 색인은 비활성화된 상태에서 업데이트되지 않으므로 다시 활성화한 경우 올바른 컨텐츠가 없을 수 있으며 다시 색인화해야 할 수도 있습니다.

TarMK 인스턴스에서 속성 인덱스를 제거한 후 압축을 실행하여 사용 중인 디스크 공간을 다시 확보해야 합니다. Lucene 인덱스의 경우 실제 인덱스 컨텐츠는 BlobStore에 있으므로 데이터 저장소 가비지 수집이 필요합니다.

MongoDB 인스턴스에서 인덱스를 제거할 때 삭제 비용은 인덱스의 노드 수에 비례합니다. 큰 인덱스를 삭제하면 문제가 발생할 수 있으므로, 다음과 같은 도구를 사용하여 유지 관리 기간 동안에만 인덱스를 비활성화하고 삭제하는 것이 좋습니다 **oak-mongo.js**. 이 접근 방식은 데이터 불일치를 초래할 수 있으므로 일반 노드 컨텐츠에 사용하지 않아야 합니다.

>[!NOTE]
>
>oak-mongo.js에 대한 자세한 내용은 [명령줄 도구 섹션](https://jackrabbit.apache.org/oak/docs/command_line.html) Oak 설명서

### JCR 쿼리 치트 시트 {#jcrquerycheatsheet}

효율적인 JCR 쿼리 및 색인 정의 만들기를 지원하려면 [JCR 쿼리 치트 시트|assets/JCR_query_cheatsheet-v1.0.pdf] 는 개발 중에 다운로드하여 참조로 사용할 수 있습니다. 여기에는 쿼리 성능 측면에서 다르게 동작하는 여러 시나리오를 다루는 QueryBuilder, XPath 및 SQL-2에 대한 샘플 쿼리가 포함되어 있습니다. 또한 Oak 인덱스를 작성하거나 사용자 지정하는 방법에 대한 권장 사항을 제공합니다. 이 치트 시트의 내용은 AEM 6.5 및 AEM as a Cloud Service에 적용됩니다.

## 색인 재지정 {#re-indexing}

이 섹션에서는 **전용** Oak 색인을 다시 색인화하는 데 적합한 이유입니다.

아래에 요약된 이유 외에 Oak 인덱스의 재색인을 시작하면 **not** 동작을 변경하거나 문제를 해결하고 AEM의 로드를 일시적으로 늘립니다.

아래 표에 있는 이유로 다루지 않는 한 Oak 인덱스의 재색인화를 방지합니다.

>[!NOTE]
>
>아래 표를 참조하여 색인화를 다시 정의하는 것이 유용하며, 항상 **를 확인하십시오.
>
>* 쿼리가 올바릅니다
>* 쿼리가 예상 인덱스로 확인됩니다. [쿼리 설명](/help/sites-administering/operations-dashboard.md#diagnosis-tools))
>* 인덱싱 프로세스가 완료되었습니다.

>


### Oak 색인 구성 변경 사항 {#oak-index-configuration-changes}

Oak 색인 재색인에 대해 허용되는 유일한 비참조 조건은 Oak 색인 구성이 변경된 경우입니다.

*재색인화는 AEM 전체 성능에 미치는 영향에 대해 항상 적절한 고려와 함께 접근해야 하며, 낮은 활동이나 유지 관리 기간 동안 수행해야 합니다.*

해결 방법과 함께 발생할 수 있는 다음과 같은 세부 문제를 설명합니다.

* [속성 인덱스 정의 변경](#property-index-definition-change)
* [Lucene 인덱스 정의 변경](#lucene-index-definition-change)

#### 속성 인덱스 정의 변경 {#property-index-definition-change}

* 적용 대상/대상:

   * 모든 Oak 버전
   * 전용 [속성 인덱스](https://jackrabbit.apache.org/oak/docs/query/property-index.html)

* 증상:

   * 속성 인덱스의 정의 업데이트 이전의 기존 노드가 결과에서 누락되었습니다.

* 확인 방법:

   * 업데이트된 인덱스 정의를 배포하기 전에 누락된 노드가 생성/수정되었는지 확인합니다.
   * 확인 `jcr:created` 또는 `jcr:lastModified` 인덱스의 수정 시간에 대해 누락된 노드의 속성

* 해결 방법:

   * [다시 색인화](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-re-index) 루센 인덱스
   * 또는 누락된 노드에 터치(양호한 쓰기 작업 수행)합니다

      * 수동 수정 또는 사용자 지정 코드 필요
      * 누락된 노드 집합을 알고 있어야 합니다.
      * 노드의 속성을 변경해야 합니다.

#### Lucene 인덱스 정의 변경 {#lucene-index-definition-change}

* 적용 대상/대상:

   * 모든 Oak 버전
   * 전용 [lucene 인덱스](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* 증상:

   * Lucene 색인에 예상 결과가 없습니다.
   * 쿼리 결과는 인덱스 정의의 예상 동작을 반영하지 않습니다
   * 인덱스 정의에 따라 쿼리 계획이 예상 출력을 보고하지 않습니다

* 확인 방법:

   * Lucene 인덱스 통계 JMX Mbean(LuceneIndex) 메서드를 사용하여 인덱스 정의가 변경되었는지 확인합니다. `diffStoredIndexDefinition`.

* 해결 방법:

   * 1.6 이전의 Oak 버전:

      * [다시 색인화](#how-to-re-index) 루센 인덱스
   * Oak 버전 1.6+

      * 기존 컨텐츠가 변경 사항으로 적용되지 않으면 새로 고침만 필요합니다

         * [새로 고침](https://jackrabbit.apache.org/oak/docs/query/lucene.html#stored-index-definition) 를 설정하여 lucene 인덱스 [oak:queryIndexDefinition]@refresh=true
      * Else, [다시 색인화](#how-to-re-index) 루센 인덱스

         * 참고: 새로운 재색인화가 트리거될 때까지 마지막 양호한 재인덱싱(또는 초기 색인)의 인덱스 상태가 사용됩니다



### 예외 및 예외 상황 {#erring-and-exceptional-situations}

다음 표에서는 Oak 인덱스를 다시 인덱싱하면 문제가 해결되는 허용 가능한 예외 및 예외 상황만 설명합니다.

AEM에서 아래에 설명된 기준과 일치하지 않는 문제가 발생하는 경우 다음을 수행하십시오. **not** 문제가 해결되지 않으므로 모든 인덱스를 다시 색인화합니다.

해결 방법과 함께 발생할 수 있는 다음과 같은 세부 문제를 설명합니다.

* [Lucene 인덱스 바이너리가 없습니다.](#lucene-index-binary-is-missing)
* [Lucene 인덱스 바이너리가 손상되었습니다.](#lucene-index-binary-is-corrupt)

#### Lucene 인덱스 바이너리가 없습니다. {#lucene-index-binary-is-missing}

* 적용 대상/대상:

   * 모든 Oak 버전
   * 전용 [lucene 인덱스](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* 증상:

   * Lucene 색인에 예상 결과가 없습니다.

* 확인 방법:

   * 오류 로그 파일에 Lucene 인덱스의 바이너리가 누락되었다는 예외가 있습니다

* 해결 방법:

   * 탐색 저장소 검사를 수행합니다. 예:

      [http://localhost:4502/system/console/repositorycheck](http://localhost:4502/system/console/repositorycheck)

      저장소 탐색은 lucene 파일 외에 다른 바이너리가 누락되었는지 확인합니다

   * lucene 인덱스 이외의 바이너리가 누락된 경우 백업에서 복원
   * 그렇지 않으면, [다시 색인화](#how-to-re-index) *모두* lucene 인덱스
   * 메모:

      이 조건은 ANY 바이너리(예: 자산 바이너리)가 누락되었습니다.

      이 경우 누락된 모든 바이너리를 복구하려면 리포지토리의 마지막으로 알려진 양호한 버전으로 복원합니다.

#### Lucene 인덱스 바이너리가 손상되었습니다. {#lucene-index-binary-is-corrupt}

* 적용 대상/대상:

   * 모든 Oak 버전
   * 전용 [lucene 인덱스](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* 증상:

   * Lucene 색인에 예상 결과가 없습니다.

* 확인 방법:

   * 다음 `AsyncIndexUpdate` (5초마다) error.log에 예외가 발생하여 실패합니다.

      `...a Lucene index file is corrupt...`

* 해결 방법:

   * lucene 인덱스의 로컬 복사본 제거

      1. AEM 중지
      1. lucene 인덱스 로컬 복사본 삭제 위치 `crx-quickstart/repository/index`
      1. AEM 다시 시작
   * 이 경우 및 `AsyncIndexUpdate` 다음에 예외가 지속됩니다.

      1. [다시 색인화](#how-to-re-index) 참조 인덱스
      1. 파일도 [Adobe 지원](https://helpx.adobe.com/support.html) 티켓


### 다시 색인화하는 방법 {#how-to-re-index}

>[!NOTE]
>
>AEM 6.5에서, [oak-run.jar는 ONLY 지원 메서드입니다.](/help/sites-deploying/indexing-via-the-oak-run-jar.md#reindexingapproachdecisiontree) MongoMK 또는 RDBMK 리포지토리에서 재색인화를 위해

#### 속성 인덱스 다시 인덱싱 {#re-indexing-property-indexes}

* 사용 [oak-run.jar](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) 속성 인덱스를 다시 색인화하려면
* 속성 인덱스에서 async-reindex 속성을 true로 설정합니다.

   * `[oak:queryIndexDefinition]@reindex-async=true`

* 를 통해 웹 콘솔을 사용하여 속성 인덱스를 비동기식으로 다시 색인화 **PropertyIndexAsyncReindex** MBean;

   예,

   [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex)

#### Lucene 속성 인덱스 다시 인덱싱 {#re-indexing-lucene-property-indexes}

* 사용 [oak-run.jar를 다시 색인화하십시오.](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) Lucene 속성 색인입니다.
* lucene 속성 인덱스에서 async-reindex 속성을 true로 설정합니다.

   * `[oak:queryIndexDefinition]@reindex-async=true`

>[!NOTE]
>
>위의 섹션에서는 및 를 요약하고 Oak 색인 재지정 지침을 [Apache Oak 설명서](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing) 를 입력합니다.

### 바이너리 사전 추출 텍스트 {#text-pre-extraction-of-binaries}

텍스트 사전 추출은 분리된 프로세스를 통해 데이터 저장소에서 직접 바이너리에서 텍스트를 추출하고 처리하고 추출된 텍스트를 Oak 인덱스의 후속 재인덱스로 직접 노출하는 프로세스입니다.

* 추출할 수 있는 텍스트(예: PDF, Word 문서, PPT, TXT 등 배포된 Oak 인덱스를 통해 전체 텍스트 검색에 적합합니다. 예 `/oak:index/damAssetLucene`.
* 속성 인덱스가 바이너리에서 텍스트를 추출하지 않으므로 텍스트 사전 추출은 Lucene 인덱스 및 NOT Oak 속성 인덱스의 재색인에만 도움이 됩니다.
* 텍스트 사전 추출은 텍스트 중심의 바이너리(PDF, 문서, TXT 등)의 전체 텍스트 재색인화를 수행할 때 긍정적인 영향을 많이 받습니다. 여기서 이미지 저장소는 추출 가능한 텍스트를 포함하지 않으므로 동일한 효율성을 제공하지 않습니다.
* 텍스트 사전 추출을 사용하면 전체 텍스트 검색 관련 텍스트를 매우 효율적으로 추출할 수 있으며, Oak 재인덱싱 프로세스에 표시하여 매우 효율적으로 사용할 수 있습니다.

#### 언제 텍스트 사전 추출을 사용할 수 있습니까? {#when-can-text-pre-extraction-be-used}

색인 재지정 **기존** 이진 추출이 활성화된 lucene 인덱스

* 재인덱싱 처리 **모두** 저장소의 후보 컨텐츠 전체 텍스트를 추출할 바이너리가 많거나 복잡하면 전체 텍스트 추출을 수행하는 데 드는 계산 부담이 AEM에 배치됩니다. 텍스트 사전 추출은 AEM에서 오버헤드 및 리소스 경합을 방지하기 위해 텍스트 추출의 &quot;컴퓨터 비용이 많이 드는 작업&quot;을 AEM Data Store에 직접 액세스하는 분리된 프로세스로 이동합니다.

의 배포 지원 **새** 이진 추출이 활성화된 AEM의 lucene 색인

* 새 인덱스(이진 추출을 사용할 수 있음)가 AEM에 배포되면 Oak는 다음 비동기 전체 텍스트 인덱스 실행에서 모든 후보 콘텐츠를 자동으로 인덱싱합니다. 위의 색인 재지정에 설명된 동일한 이유로 AEM에 과도하게 로드될 수 있습니다.

#### 언제 텍스트 사전 추출을 사용할 수 있습니까? {#when-can-text-pre-extraction-not-be-used}

저장소에 추가된 새 컨텐츠에 텍스트 사전 추출을 사용할 수도 없고, 필요할 수도 없습니다.

리포지토리에 새 컨텐츠가 추가되면 비동기 전체 텍스트 인덱싱 프로세스(기본적으로 5초마다)에 의해 자연스럽게 증분 인덱싱됩니다.

웹 UI를 통해 자산을 업로드하거나 자산의 프로그래밍 방식 수집과 같은 AEM의 정상적인 운영에서는 AEM이 자동으로 새로운 이진 컨텐츠에 대한 전체 텍스트 인덱스를 점진적으로 만듭니다. 데이터 양이 증가분 및 비교적 작으므로(5초 후에 리포지토리에 유지할 수 있는 데이터 양 대략), AEM은 전체 시스템 성능에 영향을 주지 않고 인덱싱 중에 바이너리에서 전체 텍스트 추출을 수행할 수 있습니다.

#### 텍스트 사전 추출 사용을 위한 사전 요구 사항 {#prerequisites-to-using-text-pre-extraction}

* 전체 텍스트 이진 추출을 수행하는 lucene 인덱스를 다시 인덱싱하거나 기존 컨텐츠의 전체 텍스트 인덱스 바이너리를 수행하는 새 인덱스를 배포합니다
* 텍스트를 미리 추출할 컨텐츠(바이너리)는 저장소에 있어야 합니다
* CSV 파일을 생성하고 최종 재색인을 수행하기 위한 유지 관리 창
* Oak 버전: 1.0.18+, 1.2.3+
* [oak-run.jar](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)버전 1.7.4+
* 인덱싱 AEM 인스턴스에서 액세스할 수 있는 추출된 텍스트를 저장할 파일 시스템 폴더/공유

   * 텍스트 사전 추출 OSGi 구성은 추출된 텍스트 파일에 대한 파일 시스템 경로가 필요하므로 AEM 인스턴스(로컬 드라이브 또는 파일 공유 마운트)에서 직접 액세스할 수 있어야 합니다

#### 텍스트 사전 추출을 수행하는 방법 {#how-to-perform-text-pre-extraction}

>[!NOTE]
>
>***아래에 요약된 oak-run.jar 명령은 [https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html)***
>
>위의 다이어그램과 단계는 Apache Oak 설명서에 설명된 기술 텍스트 사전 추출 단계를 설명하고 보완합니다.

![텍스트 사전 추출 프로세스 흐름](assets/chlimage_1-139.png)

**사전 추출할 컨텐츠 목록 생성**

*이 작업 중에 노드 저장소가 이동되므로 유지 관리 기간/저사용 기간 동안 1단계(a-b)를 실행하면 시스템에 상당한 로드가 발생할 수 있습니다.*

1a. 실행 `oak-run.jar --generate` 텍스트를 미리 추출할 노드 목록을 만들려면

1b. 노드 목록(1a)은 파일 시스템에 CSV 파일로 저장됩니다

전체 노드 저장소는 oak-run 명령의 경로에 지정된 대로 항상 트래버스됩니다 `--generate` 가 실행되면 **새** CSV 파일이 생성됩니다. CSV 파일은 다음과 같습니다 **not** 텍스트 사전 추출 프로세스의 개별 실행 간에 다시 사용됩니다(단계 1 - 2).

**파일 시스템에 텍스트 사전 추출**

*2단계(a-c)는 데이터 스토어와만 상호 작용하므로 AEM의 정상적인 작업 중에 실행할 수 있습니다.*

2a. 실행 `oak-run.jar --tika` (1b)에서 생성된 CSV 파일에 열거된 바이너리 노드의 텍스트를 미리 추출하려면

2 b. (2a)에서 시작된 프로세스는 데이터 저장소의 CSV에 정의된 이진 노드에 직접 액세스하여 텍스트를 추출합니다.

2c.  추출된 텍스트는 Oak 재인덱싱 프로세스(3a)에서 수집되는 형식으로 파일 시스템에 저장됩니다

사전 추출된 텍스트는 CSV에서 이진 지문으로 식별됩니다. 이진 파일이 동일한 경우 AEM 인스턴스에서 미리 추출된 동일한 텍스트를 사용할 수 있습니다. AEM Publish는 일반적으로 AEM Author의 하위 세트이므로 AEM Author에서 미리 추출한 텍스트를 사용하여 AEM Publish를 다시 색인화할 수 있습니다(AEM Publish에서 추출된 텍스트 파일에 대한 파일 시스템 액세스 권한이 있다고 가정).

미리 추출된 텍스트는 시간에 따라 점진적으로 추가할 수 있습니다. 텍스트 사전 추출은 이전에 추출된 바이너리에 대한 추출을 건너뛰므로, 이후에 다시 색인화가 발생할 경우 사전 추출된 텍스트를 유지하는 것이 좋습니다(추출된 컨텐츠가 그리 크지 않다고 가정할 경우). 그럴 경우 텍스트가 잘 압축되므로 중간에 있는 내용물의 압축을 평가하십시오.

**추출된 텍스트 파일에서 전체 텍스트를 소싱하는 Oak 인덱스 다시 색인화**

*이 작업 중에 노드 저장소가 탐색됨에 따라 유지 관리/저사용 기간 동안 재인덱싱(3a-b단계)을 실행하면 시스템에 상당한 로드가 발생할 수 있습니다.*

3a. [다시 색인화](#how-to-re-index) Lucene 인덱스 중 하나가 AEM에서 호출됩니다.

3b. Apache Jackrabbit Oak DataStore PreExtrutedTextProvider OSGi 구성(파일 시스템 경로를 통해 추출된 텍스트를 가리키도록 구성됨)은 Oak에게 추출된 파일에서 전체 텍스트 텍스트를 소스에 전달하도록 지시하고 저장소에 저장된 데이터를 직접 히트하고 처리하지 않도록 합니다.
