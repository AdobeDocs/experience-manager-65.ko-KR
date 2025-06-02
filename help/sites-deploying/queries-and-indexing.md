---
title: Oak 쿼리 및 색인화
description: Adobe Experience Manager(AEM) 6.5에서 색인을 구성하는 방법에 대해 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/queries-and-indexing
feature: Configuring
exl-id: d9ec7728-84f7-42c8-9c80-e59e029840da
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: eeeb31d81c22f8dace7a170953bf45a709f5ac73
workflow-type: tm+mt
source-wordcount: '3051'
ht-degree: 1%

---

# Oak 쿼리 및 색인화{#oak-queries-and-indexing}

>[!NOTE]
>
>이 문서는 AEM 6에서의 인덱스 구성에 대해 설명합니다. 쿼리 및 인덱싱 성능 최적화에 대한 모범 사례는 [쿼리 및 인덱싱 모범 사례](/help/sites-deploying/best-practices-for-queries-and-indexing.md)를 참조하세요.

## 소개 {#introduction}

Jackrabbit 2와 달리 Oak은 기본적으로 콘텐츠를 색인화하지 않습니다. 기존 관계형 데이터베이스와 마찬가지로 필요할 때 사용자 정의 인덱스를 만들어야 합니다. 특정 쿼리에 대한 색인이 없는 경우 많은 노드가 트래버스될 수 있습니다. 쿼리가 여전히 작동할 수 있지만 느릴 수 있습니다.

Oak에 색인 없는 쿼리가 발생하면 경고 수준 로그 메시지가 인쇄됩니다.

```xml
*WARN* Traversed 1000 nodes with filter Filter(query=select ...) consider creating an index or changing the query
```

## 지원되는 쿼리 언어 {#supported-query-languages}

Oak 쿼리 엔진은 다음 언어를 지원합니다.

* XPath(권장)
* SQL-
* SQL(사용되지 않음)
* JQOM

## 인덱서 유형 및 비용 계산 {#indexer-types-and-cost-calculation}

Apache Oak 기반 백엔드를 사용하면 서로 다른 인덱서를 저장소에 플러그인할 수 있습니다.

하나의 인덱서는 인덱스 정의가 저장소 자체에 저장되는 **Property Index**&#x200B;입니다.

**Apache Lucene** 및 **Solr**&#x200B;에 대한 구현도 기본적으로 사용할 수 있으며, 둘 다 전체 텍스트 인덱싱을 지원합니다.

사용 가능한 다른 인덱서가 없는 경우 **순회 인덱스**&#x200B;이(가) 사용됩니다. 즉, 콘텐츠가 색인화되지 않고 콘텐츠 노드를 트래버스하여 쿼리와 일치하는 항목을 찾습니다.

쿼리에 여러 인덱서를 사용할 수 있는 경우 사용 가능한 각 인덱서는 쿼리 실행 비용을 추정합니다. 그런 다음 Oak은 예상 비용이 가장 낮은 인덱서를 선택합니다.

![chlimage_1-148](assets/chlimage_1-148.png)

위의 다이어그램은 Apache Oak의 쿼리 실행 메커니즘을 개략적으로 보여 주는 것입니다.

먼저, 쿼리를 추상 구문 트리로 구문 분석합니다. 그런 다음 쿼리를 확인하고 Oak 쿼리의 기본 언어인 SQL-2로 변환합니다.

다음으로 각 색인을 참조하여 쿼리에 대한 비용을 추정합니다. 완료되면 가장 낮은 색인의 결과가 검색됩니다. 마지막으로, 결과는 필터링되어 현재 사용자가 결과에 대한 읽기 액세스 권한을 가지고 결과가 전체 쿼리와 일치하는지 확인합니다.

## 인덱스 구성 {#configuring-the-indexes}

>[!NOTE]
>
>대규모 저장소의 경우 색인 작성에는 많은 시간이 소요됩니다. 이는 색인의 초기 생성과 색인 재지정(정의를 변경한 후 색인 재구축) 모두에 적용됩니다. [Oak 인덱스 문제 해결](/help/sites-deploying/troubleshooting-oak-indexes.md) 및 [느린 리인덱싱 방지](/help/sites-deploying/troubleshooting-oak-indexes.md#preventing-slow-re-indexing)를 참조하십시오.

특히 MongoDB 및 전체 텍스트 색인의 경우 대규모 리포지토리에서 리색인화가 필요한 경우 텍스트 사전 추출을 고려하며, oak-run을 사용하여 초기 색인을 빌드하고 다시 색인화하는 것을 고려하십시오.

인덱스가 **Oak:index** 노드 아래에 리포지토리의 노드로 구성되어 있습니다.

인덱스 노드의 형식은 **oak:QueryIndexDefinition이어야 합니다.** 각 인덱서에 대해 노드 속성으로 몇 가지 구성 옵션을 사용할 수 있습니다. 자세한 내용은 아래 각 인덱서 유형에 대한 구성 세부 정보를 참조하십시오.

### 속성 색인 {#the-property-index}

속성 인덱스는 속성 제약 조건이 있지만 전체 텍스트가 아닌 쿼리에 유용합니다. 다음 절차에 따라 구성할 수 있습니다.

1. `http://localhost:4502/crx/de/index.jsp`(으)로 이동하여 CRXDE 열기
1. **oak:index** 아래에 노드 만들기
1. 노드 이름을 **PropertyIndex**(으)로 지정하고 노드 유형을 **oak:QueryIndexDefinition**(으)로 설정하십시오.
1. 새 노드에 대해 다음 속성을 설정합니다.

   * **유형:** `property`(유형 문자열)
   * **propertyNames:** `jcr:uuid`(형식 이름)

   이 예제에서는 연결된 노드의 UUID(Universally Unique Identifier)를 노출하는 작업의 `jcr:uuid` 속성을 인덱싱합니다.

1. 변경 사항을 저장합니다.

속성 인덱스에는 다음과 같은 구성 옵션이 있습니다.

* **type** 속성은 인덱스의 형식을 지정하며, 이 경우 **property**(으)로 설정해야 합니다.

* **propertyNames** 속성은 인덱스에 저장된 속성 목록을 나타냅니다. 누락된 경우 노드 이름은 속성 이름 참조 값으로 사용됩니다. 이 예에서는 노드의 UUID(고유 식별자)를 표시하는 작업이 포함된 **jcr:uuid** 속성이 인덱스에 추가됩니다.

* **true**(으)로 설정된 경우 속성 인덱스에 고유성 제약 조건을 추가하는 **unique** 플래그입니다.

* **declingNodeTypes** 속성을 사용하면 인덱스만 적용되는 특정 노드 유형을 지정할 수 있습니다.
* **true**(으)로 설정된 경우 전체 콘텐츠 다시 인덱스를 트리거하는 **reindex** 플래그.

### 순서가 지정된 색인 {#the-ordered-index}

Ordered 인덱스는 속성 인덱스의 확장입니다. 하지만 더 이상 사용되지 않습니다. 이 형식의 인덱스는 [Lucene 속성 인덱스](#the-lucene-property-index)(으)로 대체해야 합니다.

### Lucene 전체 텍스트 색인 {#the-lucene-full-text-index}

Apache Lucene 기반의 전체 텍스트 인덱서는 AEM 6에서 사용할 수 있습니다.

전체 텍스트 색인이 구성된 경우 색인화된 다른 조건이 있는지 여부와 경로 제한이 있는지 여부에 관계없이 전체 텍스트 조건이 있는 모든 쿼리는 전체 텍스트 색인을 사용합니다.

전체 텍스트 색인이 구성되지 않은 경우 전체 텍스트 조건이 있는 쿼리가 예상대로 작동하지 않습니다.

색인이 비동기 백그라운드 스레드를 통해 업데이트되므로 백그라운드 프로세스가 완료될 때까지 짧은 시간 동안 일부 전체 텍스트 검색을 사용할 수 없습니다.

아래 절차에 따라 Lucene 전체 텍스트 인덱스를 구성할 수 있습니다.

1. CRXDE를 열고 **oak:index** 아래에 노드를 만드십시오.
1. 노드 이름을 **LuceneIndex**(으)로 지정하고 노드 유형을 **oak:QueryIndexDefinition**(으)로 설정합니다.
1. 노드에 다음 속성을 추가합니다.

   * **유형:** `lucene`(유형 문자열)
   * **비동기:** `async`(유형 문자열)

1. 변경 사항을 저장합니다.

Lucene 색인에는 다음과 같은 구성 옵션이 있습니다.

* 인덱스의 형식을 지정하는 **type** 속성은 **lucene**(으)로 설정해야 합니다.
* **async**(으)로 설정해야 하는 **async** 속성입니다. 이렇게 하면 인덱스 업데이트 프로세스가 백그라운드 스레드로 전송됩니다.
* 인덱스에 포함된 속성 형식의 하위 집합을 정의하는 **includePropertyTypes** 속성입니다.
* 인덱스에서 제외해야 하는 속성 이름 목록을 정의하는 **excludePropertyNames** 속성입니다.
* **true**(으)로 설정된 경우 전체 콘텐츠 다시 인덱스를 트리거하는 **reindex** 플래그.

### 전체 텍스트 검색 이해 {#understanding-fulltext-search}

이 섹션의 설명서는 Apache Lucene, Elasticsearch 및 PostgreSQL, SQLite 및 MySQL의 전체 텍스트 인덱스에 적용됩니다. 다음 예제는 AEM / Oak / Lucene입니다.

인덱싱할 <b>데이터</b>

시작점은 인덱싱해야 하는 데이터입니다. 다음 문서를 예로 들어 보겠습니다.

| <b>문서 ID</b> | <b>경로</b> | <b>전체 텍스트</b> |
| --- | --- | --- |
| 100 | /content/rubik | &quot;루빅은 핀란드의 브랜드입니다.&quot; |
| 200 | /content/rubiksCube | 루빅 큐브는 1974년에 발명되었습니다. |
| 300 | /content/cube | &quot;큐브는 3차원 개체입니다.&quot; |


<b>인덱스 반전</b>

색인 지정 메커니즘은 전체 텍스트를 &quot;토큰&quot;이라는 단어로 분할하고 &quot;반전된 색인&quot;이라는 색인을 빌드합니다. 이 색인에는 각 단어에 대해 나타나는 문서 목록이 포함되어 있습니다.

짧고 일반적인 단어(&quot;stopwords&quot;라고도 함)는 색인화되지 않습니다. 모든 토큰은 소문자로 변환되며 형태소 분석이 적용됩니다.

*&quot;-&quot;*&#x200B;과(와) 같은 특수 문자가 인덱싱되지 않았습니다.

| <b>토큰</b> | <b>문서 ID</b> |
| --- | --- |
| 194 | 200개... |
| 브랜드 | 100개... |
| 큐브 | ..., 200, 300,... |
| 차원 | 300 |
| 마침 | 100개... |
| 발명 | 200 |
| 개체 | 300,... |
| 루비크 | ..., 100, 200,... |

문서 목록이 정렬됩니다. 쿼리할 때 편리합니다.

<b>검색</b>

다음은 쿼리의 예입니다. 모든 특수 문자(예: *&#39;*)가 공백으로 대체되었습니다.

```
/jcr:root/content//element(\*; cq:Page)`[` jcr:contains('Rubik s Cube')`]`
```

단어는 색인화할 때와 같은 방식으로 토큰화되고 필터링됩니다(예: 단일 문자 단어가 제거됨). 따라서 이 경우 검색은 다음에 대한 것입니다.

```
+:fulltext:rubik +:fulltext:cube
```

색인은 그 단어들에 대한 문서들의 목록을 참조한다. 문서가 많으면 목록이 커질 수 있습니다. 예를 들어 다음 항목이 포함되어 있다고 가정합니다.


| <b>토큰</b> | <b>문서 ID</b> |
| --- | --- |
| 루비크 | 10, 100, 200, 1000 |
| 큐브 | 30, 200, 300, 2000 |


Lucene은 `n`개의 단어를 검색할 때 두 목록(또는 라운드 로빈 `n` 목록) 간을 앞뒤로 전환합니다.

* &quot;루빅&quot;에서 읽으면 첫 번째 항목을 얻습니다. 10을 찾습니다.
* &quot;큐브&quot;에서 읽으면 첫 번째 항목 `>` = 10이 만들어집니다. 10개는 찾을 수 없고, 다음 것은 30개입니다.
* &quot;rubik&quot;에서 읽으면 첫 번째 항목 `>` = 30을 가져옵니다. 100을 찾습니다.
* &quot;큐브&quot;에서 읽으면 첫 번째 항목 `>` = 100을 가져옵니다. 200을 찾습니다.
* &quot;rubik&quot;에서 읽으면 첫 번째 항목 `>` = 200을 가져옵니다. 200개를 찾았습니다. 따라서 문서 200은 두 조건에 모두 일치합니다. 기억하고 있습니다.
* 다음 항목인 1000은 &quot;루빅&quot;에서 읽으십시오.
* &quot;큐브&quot;에서 읽으면 첫 번째 항목 `>` = 1000을 가져옵니다. 2000을 찾습니다.
* &quot;rubik&quot;에서 읽으면 첫 번째 항목이 생깁니다. `>` = 2000: 목록의 끝.
* 마지막으로 검색을 중단할 수 있습니다.

아래 예와 같이 두 용어가 모두 포함된 유일한 문서는 200입니다.

| 200 | /content/rubiksCube | 루빅 큐브는 1974년에 발명되었습니다. |
| --- | --- | --- |

여러 항목이 발견되면 점수별로 정렬됩니다.

>[!NOTE]
>
>이 섹션에서 설명하는 검색 메커니즘은 Linux `grep` 명령처럼 부분 일치가 아닌 Lucene 인덱싱을 사용합니다.

### Lucene 속성 색인 {#the-lucene-property-index}

**Oak 1.0.8**&#x200B;부터 Lucene을 사용하여 전체 텍스트가 아닌 속성 제약 조건을 포함하는 인덱스를 만들 수 있습니다.

Lucene 속성 인덱스를 만들려면 **fulltextEnabled** 속성을 항상 false로 설정해야 합니다.

다음 예제 쿼리를 사용합니다.

```xml
select * from [nt:base] where [alias] = '/admin'
```

위의 쿼리에 대해 Lucene 속성 인덱스를 정의하려면 **`oak:index`:** 아래에 노드를 만들어 다음 정의를 추가할 수 있습니다.

* **이름:** `LucenePropertyIndex`
* **유형:** `oak:QueryIndexDefinition`

노드가 생성되면 다음 속성을 추가합니다.

* **유형:**

  ```xml
  lucene (of type String)
  ```

* **비동기:**

  ```xml
  async (of type String)
  ```

* **fulltextEnabled:**

  ```xml
  false (of type Boolean)
  ```

* **includePropertyNames:** `["alias"] (of type String)`

>[!NOTE]
>
>일반 속성 인덱스와 비교하여 Lucene 속성 인덱스는 항상 비동기 모드로 구성됩니다. 따라서 색인에 의해 반환되는 결과가 항상 저장소의 최신 상태를 반영하지는 않을 수 있습니다.

>[!NOTE]
>
>Lucene 속성 인덱스에 대한 자세한 내용은 [Apache Jackrabbit Oak Lucene 설명서 페이지](https://jackrabbit.apache.org/oak/docs/query/lucene.html)를 참조하십시오.

### Lucene 분석기 {#lucene-analyzers}

버전 1.2.0 이후 Oak은 Lucene 분석기를 지원합니다.

분석기는 문서가 색인화되었을 때와 쿼리 시간에 모두 사용됩니다. 분석기가 필드의 텍스트를 검사하고 토큰 스트림을 생성합니다. Lucene 분석기는 일련의 토큰화기 및 필터 클래스로 구성됩니다.

분석기는 `oak:index` 정의 내의 `analyzers` 노드(`nt:unstructured` 유형)를 통해 구성할 수 있습니다.

인덱스의 기본 분석기가 분석기 노드의 `default` 자식에 구성되어 있습니다.

![chlimage_1-149](assets/chlimage_1-149.png)

>[!NOTE]
>
>사용 가능한 분석기 목록은 사용 중인 Lucene 버전의 API 설명서를 참조하십시오.

#### Analyzer 클래스 직접 지정 {#specifying-the-analyzer-class-directly}

기본 제공 분석기를 사용하려면 아래 절차에 따라 구성할 수 있습니다.

1. `oak:index` 노드 아래에서 분석기를 사용할 인덱스를 찾습니다.

1. 인덱스 아래에 `nt:unstructured` 형식의 `default`(이)라는 자식 노드를 만듭니다.

1. 다음 속성을 사용하여 기본 노드에 속성을 추가합니다.

   * **이름:** `class`
   * **유형:** `String`
   * **값:** `org.apache.lucene.analysis.standard.StandardAnalyzer`

   값은 사용할 Analyzer 클래스의 이름입니다.

   선택적 `luceneMatchVersion` 문자열 속성을 사용하여 특정 Lucene 버전에서 사용할 분석기를 설정할 수도 있습니다. Lucene 4.7에서 사용할 수 있는 올바른 구문은 다음과 같습니다.

   * **이름:** `luceneMatchVersion`
   * **유형:** `String`
   * **값:** `LUCENE_47`

   `luceneMatchVersion`이(가) 제공되지 않으면 Oak에서 제공되는 Lucene 버전을 사용합니다.

1. Analyzer 구성에 중지 단어 파일을 추가하려면 다음 속성을 사용하여 `default` 노드 아래에 노드를 만들 수 있습니다.

   * **이름:** `stopwords`
   * **유형:** `nt:file`

#### 컴포지션을 통한 분석기 만들기 {#creating-analyzers-via-composition}

`Tokenizers`, `TokenFilters` 및 `CharFilters`을(를) 기반으로 분석기를 구성할 수도 있습니다. 이렇게 하려면 분석기를 지정하고 나열된 순서로 적용되는 선택적 토큰라이저와 필터의 하위 노드를 만들면 됩니다. [https://cwiki.apache.org/confluence/display/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema](https://cwiki.apache.org/confluence/display/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema)도 참조하세요.

이 노드 구조를 예로 들어 보겠습니다.

* **이름:** `analyzers`

   * **이름:** `default`

      * **이름:** `charFilters`
      * **유형:** `nt:unstructured`

         * **이름:** `HTMLStrip`
         * **이름:** `Mapping`

      * **이름:** `tokenizer`

         * **속성 이름:** `name`

            * **유형:** `String`
            * **값:** `Standard`

      * **이름:** `filters`
      * **유형:** `nt:unstructured`

         * **이름:** `LowerCase`
         * **이름:** `Stop`

            * **속성 이름:** `words`

               * **유형:** `String`
               * **값:** `stop1.txt, stop2.txt`

            * **이름:** `stop1.txt`

               * **유형:** `nt:file`

            * **이름:** `stop2.txt`

               * **유형:** `nt:file`

필터 이름, charFilters 및 토큰화기는 공장 접미사를 제거하여 형성됩니다. 따라서:

* `org.apache.lucene.analysis.standard.StandardTokenizerFactory`이(가) `standard`이(가) 됨

* `org.apache.lucene.analysis.charfilter.MappingCharFilterFactory`이(가) `Mapping`이(가) 됨

* `org.apache.lucene.analysis.core.StopFilterFactory`이(가) `Stop`이(가) 됨

팩토리에 필요한 모든 구성 매개 변수가 해당 노드의 속성으로 지정됩니다.

외부 파일의 컨텐츠를 로드해야 하는 정지어 로드와 같은 경우에는 해당 파일에 대해 `nt:file` 형식의 자식 노드를 만들어 컨텐츠를 제공할 수 있습니다.

### Solr 인덱스 {#the-solr-index}

Solr 인덱스의 목적은 전체 텍스트 검색이지만 경로, 속성 제한 및 기본 유형 제한 사항별로 검색을 인덱싱하는 데 사용할 수도 있습니다. 즉, Oak의 Solr 인덱스를 모든 유형의 JCR 쿼리에 사용할 수 있습니다.

AEM의 통합은 저장소 수준에서 수행되므로 Solr은 AEM과 함께 제공되는 새로운 저장소 구현인 Oak에서 사용할 수 있는 색인 중 하나입니다.

AEM 인스턴스를 사용하여 원격 서버로 작동하도록 구성할 수 있습니다.

### 단일 원격 Solr 서버로 AEM 구성 {#configuring-aem-with-a-single-remote-solr-server}

원격 Solr 서버 인스턴스에서 작동하도록 AEM을 구성할 수도 있습니다.

1. 최신 버전의 Solr을 다운로드하여 추출하십시오. 이 작업을 수행하는 방법에 대한 자세한 내용은 [Apache Solr 설치 설명서](https://solr.apache.org/guide/6_6/installing-solr.html)를 참조하십시오.
1. 이제 두 개의 Solr 샤드를 만듭니다. 이렇게 하려면 Solr의 압축을 푼 폴더에 각 분할에 대한 폴더를 만들면 됩니다.

   * 첫 번째 분할에 대해 폴더를 만듭니다.

   `<solrunpackdirectory>\aemsolr1\node1`

   * 두 번째 분할에 대해 폴더를 만듭니다.

   `<solrunpackdirectory>\aemsolr2\node2`

1. Solr 패키지에서 예제 인스턴스를 찾습니다. 패키지 루트의 &quot; `example`&quot; 폴더에 있습니다.
1. 예제 인스턴스에서 다음 폴더를 두 개의 공유 폴더(`aemsolr1\node1` 및 `aemsolr2\node2`)에 복사합니다.

   * `contexts`
   * `etc`
   * `lib`
   * `resources`
   * `scripts`
   * `solr-webapp`
   * `webapps`
   * `start.jar`

1. 두 개의 공유 폴더 각각에 &quot; `cfg`&quot;이라는 폴더를 만듭니다.
1. Solr 및 Zookeeper 구성 파일을 새로 만든 `cfg`개 폴더에 배치합니다.

   >[!NOTE]
   >
   >Solr 및 ZooKeeper 구성에 대한 자세한 내용은 [Solr 구성 설명서](https://cwiki.apache.org/confluence/display/solr/ConfiguringSolr) 및 [ZooKeeper 시작 안내서](https://zookeeper.apache.org/doc/r3.1.2/zookeeperStarted.html)를 참조하십시오.

1. `aemsolr1\node1`(으)로 이동하여 다음 명령을 실행하여 ZooKeeper 지원을 통해 첫 번째 분할을 시작합니다.

   ```xml
   java -Xmx2g -Dbootstrap_confdir=./cfg/oak/conf -Dcollection.configName=myconf -DzkRun -DnumShards=2 -jar start.jar
   ```

1. `aemsolr2\node2`(으)로 이동하여 다음 명령을 실행하여 두 번째 분할을 시작합니다.

   ```xml
   java -Xmx2g -Djetty.port=7574 -DzkHost=localhost:9983 -jar start.jar
   ```

1. 두 Shards가 모두 시작된 후 `http://localhost:8983/solr/#/`의 Solr 인터페이스에 연결하여 모든 기능이 실행되고 있는지 테스트하십시오.
1. AEM을 시작하고 `http://localhost:4502/system/console/configMgr`의 웹 콘솔로 이동합니다.
1. **Oak Solr 원격 서버 구성**&#x200B;에서 다음 구성을 설정합니다.

   * Solr HTTP URL: `http://localhost:8983/solr/`

1. **Oak Solr** 서버 공급자의 드롭다운 목록에서 **원격 Solr**&#x200B;을(를) 선택하십시오.

1. CRXDE로 이동한 다음 관리자로 로그인합니다.
1. **oak:index** 아래에 **solrIndex** 노드를 만들고 다음 속성을 설정합니다.

   * **유형:** 문자열(유형 문자열)
   * **비동기:** 비동기(유형 문자열)
   * **다시 인덱싱:** true(부울 유형)

1. 변경 사항을 저장합니다.

#### Solr에 대한 권장 구성 {#recommended-configuration-for-solr}

다음은 이 문서에 설명된 세 가지 Solr 배포 모두에서 사용할 수 있는 기본 구성의 예입니다. AEM에 이미 있는 전용 속성 인덱스를 수용하므로 다른 애플리케이션에는 사용하지 마십시오.

아카이브를 제대로 사용하려면 아카이브 내용을 Solr Home 디렉토리에 직접 배치해야 합니다. 다중 노드 배포가 있는 경우 각 노드의 루트 폴더 바로 아래로 이동해야 합니다.

권장 Solr 구성 파일

[파일 가져오기](assets/recommended-conf.zip)

### AEM 색인화 도구 {#aem-indexing-tools}

AEM 6.1에는 Adobe Consulting Services Commons 도구 세트의 일부로 AEM 6.0에 있는 두 개의 인덱싱 도구가 통합되어 있습니다.

1. **쿼리 설명**: 관리자가 쿼리 실행 방법을 이해하는 데 도움이 되도록 디자인된 도구입니다.
1. 기존 색인을 유지 관리하기 위한 웹 사용자 인터페이스인 **Oak 색인 관리자**.

이제 AEM 시작 화면에서 **도구 - 작업 - 대시보드 - 진단**&#x200B;으로 이동하여 연결할 수 있습니다.

사용 방법에 대한 자세한 내용은 [작업 대시보드 설명서](/help/sites-administering/operations-dashboard.md)를 참조하세요.

#### OSGi를 통해 속성 인덱스 생성 {#creating-property-indexes-via-osgi}

ACS Commons 패키지는 속성 인덱스를 만드는 데 사용할 수 있는 OSGi 구성도 표시합니다.

&quot;**Oak 속성 인덱스 확인**&quot;을 검색하여 웹 콘솔에서 액세스할 수 있습니다.

![chlimage_1-150](assets/chlimage_1-150.png)

### 색인 지정 문제 해결 {#troubleshooting-indexing-issues}

쿼리가 실행되는 데 시간이 오래 걸리고 일반적인 시스템 응답 시간이 느려지는 상황이 발생할 수 있습니다.

이 섹션에서는 이러한 문제의 원인을 추적하기 위해 수행해야 하는 작업과 이를 해결하는 방법에 대한 조언을 제공합니다.

#### 분석을 위한 디버깅 정보 준비 {#preparing-debugging-info-for-analysis}

[쿼리 설명 도구](/help/sites-administering/operations-dashboard.md#explain-query)를 통해 실행 중인 쿼리에 필요한 정보를 가장 쉽게 얻을 수 있습니다. 이를 통해 로그 수준 정보를 확인하지 않고도 느린 쿼리를 디버깅하는 데 필요한 정확한 정보를 수집할 수 있습니다. 디버깅 중인 쿼리를 알고 있는 경우 이 방법이 좋습니다.

어떤 이유로든 가능하지 않은 경우, 단일 파일에 인덱싱 로그를 수집하여 특정 문제를 해결하는 데 사용할 수 있습니다.

#### 로깅 활성화 {#enable-logging}

로깅을 활성화하려면 Oak 색인화 및 쿼리와 관련된 범주에 대해 **DEBUG** 수준 로그를 활성화해야 합니다. 이러한 범주는 다음과 같습니다.

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

**com.day.cq.search** 범주는 AEM 제공 QueryBuilder 유틸리티를 사용하는 경우에만 적용할 수 있습니다.

>[!NOTE]
>
>문제를 해결하려는 쿼리가 실행되는 기간 동안에만 로그를 DEBUG로 설정하는 것이 중요합니다. 그렇지 않으면 시간이 지남에 따라 로그에 많은 이벤트가 생성됩니다. 이러한 이유로 필요한 로그가 수집되면 위에서 언급한 범주에 대한 INFO 수준 로깅으로 다시 전환합니다.

다음 절차에 따라 로깅을 활성화할 수 있습니다.

1. 브라우저를 `https://serveraddress:port/system/console/slinglog`(으)로 지정
1. 콘솔의 아래쪽에 있는 **새 로거 추가** 단추를 클릭합니다.
1. 새로 만든 행에서 위에 언급된 범주를 추가합니다. **+** 기호를 사용하여 단일 로거에 둘 이상의 범주를 추가할 수 있습니다.
1. **로그 수준** 드롭다운 목록에서 **디버그**&#x200B;를 선택합니다.
1. 출력 파일을 `logs/queryDebug.log`(으)로 설정합니다. 이렇게 하면 모든 DEBUG 이벤트가 단일 로그 파일로 상호 연결됩니다.
1. 쿼리를 실행하거나 디버그하려는 쿼리를 사용하는 페이지를 렌더링합니다.
1. 쿼리를 실행한 후에는 로깅 콘솔로 돌아가서 새로 만든 로거의 로그 수준을 **INFO**(으)로 변경하십시오.

#### 색인 구성 {#index-configuration}

쿼리가 평가되는 방식은 주로 색인 구성의 영향을 받습니다. 색인 구성을 분석하거나 지원으로 보내는 것이 중요합니다. 구성을 콘텐츠 패키지로 가져오거나 JSON 렌디션을 가져올 수 있습니다.

일반적으로 인덱싱 구성은 CRXDE의 `/oak:index` 노드에 저장되며 다음 위치에서 JSON 버전을 가져올 수 있습니다.

`https://serveraddress:port/oak:index.tidy.-1.json`

색인이 다른 위치에 구성된 경우 그에 따라 경로를 변경합니다.

#### MBean 출력 {#mbean-output}

경우에 따라 디버깅을 위해 인덱스 관련 MBean의 출력을 제공하는 것이 유용합니다. 다음을 통해 이 작업을 수행할 수 있습니다.

1. 다음 위치의 JMX 콘솔로 이동:
   `https://serveraddress:port/system/console/jmx`

1. 다음 MBean을 검색합니다.

   * Lucene 색인 통계
   * CopyOnRead 지원 통계
   * Oak 쿼리 통계
   * IndexStats

1. 성능 통계를 확인할 수 있도록 각 MBean을 클릭합니다. 지원 제출이 필요한 경우 스크린샷을 만들거나 기록해 두십시오.

다음 URL에서 이러한 통계의 JSON 변형을 가져올 수도 있습니다.

* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`

`https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak.tidy.3.json`을(를) 통해 통합 JMX 출력을 제공할 수도 있습니다. 여기에는 JSON 형식의 모든 Oak 관련 MBean 세부 사항이 포함됩니다.

#### 기타 세부 정보 {#other-details}

다음과 같은 문제를 해결하는 데 도움이 되는 추가 세부 정보를 수집할 수 있습니다.

1. 인스턴스가 실행 중인 Oak 버전입니다. CRXDE를 열고 시작 페이지의 오른쪽 아래 모서리에 있는 버전을 보거나 `org.apache.jackrabbit.oak-core` 번들의 버전을 확인하여 이를 확인할 수 있습니다.
1. 문제가 있는 쿼리의 QueryBuilder 디버거 출력입니다. 디버거는 `https://serveraddress:port/libs/cq/search/content/querydebug.html`에서 액세스할 수 있습니다.
