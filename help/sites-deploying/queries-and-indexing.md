---
title: Oak 쿼리 및 색인 지정
description: Adobe Experience Manager(AEM) 6.5에서 색인을 구성하는 방법에 대해 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/queries-and-indexing
feature: Configuring
exl-id: d9ec7728-84f7-42c8-9c80-e59e029840da
source-git-commit: db0e9d6105484b37e2e21e49bf0f95cef9da2a62
workflow-type: tm+mt
source-wordcount: '3034'
ht-degree: 1%

---

# Oak 쿼리 및 색인 지정{#oak-queries-and-indexing}

>[!NOTE]
>
>이 문서는 AEM 6에서 색인을 구성하는 방법에 대한 내용입니다. 쿼리 및 색인화 성능 최적화에 대한 우수 사례는 다음을 참조하십시오. [쿼리 및 색인 생성에 대한 우수 사례](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

## 소개 {#introduction}

Jackrabbit 2와 달리 Oak는 기본적으로 콘텐츠를 인덱싱하지 않습니다. 기존 관계형 데이터베이스와 마찬가지로 필요할 때 사용자 정의 인덱스를 만들어야 합니다. 특정 쿼리에 대한 색인이 없는 경우 많은 노드가 트래버스될 수 있습니다. 쿼리가 여전히 작동할 수 있지만 느릴 수 있습니다.

Oak에서 색인 없는 쿼리가 발견되면 경고 수준 로그 메시지가 인쇄됩니다.

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

인덱서 하나는 **속성 인덱스**&#x200B;색인 정의가 저장소 자체에 저장되는 경로입니다.

구현 **Apache Lucene** 및 **Solr** 또한 둘 다 전체 텍스트 색인화를 지원하는 기본적으로 사용할 수 있습니다.

다음 **순회 지수** 다른 인덱서를 사용할 수 없는 경우에 사용됩니다. 즉, 콘텐츠가 색인화되지 않고 콘텐츠 노드를 트래버스하여 쿼리와 일치하는 항목을 찾습니다.

쿼리에 여러 인덱서를 사용할 수 있는 경우 사용 가능한 각 인덱서는 쿼리 실행 비용을 추정합니다. 그런 다음 Oak는 예상 비용이 가장 낮은 인덱서를 선택합니다.

![chlimage_1-148](assets/chlimage_1-148.png)

위의 다이어그램은 Apache Oak의 쿼리 실행 메커니즘을 개략적으로 보여 주는 것입니다.

먼저, 쿼리를 추상 구문 트리로 구문 분석합니다. 그런 다음 쿼리를 확인하고 Oak 쿼리의 기본 언어인 SQL-2로 변환합니다.

다음으로 각 색인을 참조하여 쿼리에 대한 비용을 추정합니다. 완료되면 가장 낮은 색인의 결과가 검색됩니다. 마지막으로, 결과는 필터링되어 현재 사용자가 결과에 대한 읽기 액세스 권한을 가지고 결과가 전체 쿼리와 일치하는지 확인합니다.

## 인덱스 구성 {#configuring-the-indexes}

>[!NOTE]
>
>대규모 저장소의 경우 색인 작성에는 많은 시간이 소요됩니다. 이는 색인의 초기 생성과 색인 재지정(정의를 변경한 후 색인 재구축) 모두에 적용됩니다. 참조: [Oak 색인 문제 해결](/help/sites-deploying/troubleshooting-oak-indexes.md) 및 [느린 리인덱싱 방지](/help/sites-deploying/troubleshooting-oak-indexes.md#preventing-slow-re-indexing).

특히 MongoDB 및 전체 텍스트 색인의 경우 대규모 리포지토리에서 리색인화가 필요한 경우 텍스트 사전 추출을 고려하며, oak-run을 사용하여 초기 색인을 빌드하고 다시 색인화하는 것을 고려하십시오.

색인은 아래의 저장소에 노드로 구성됩니다. **Oak:index** 노드.

인덱스 노드의 유형은 다음과 같아야 합니다. **oak:QueryIndexDefinition.** 각 인덱서에 대해 노드 속성으로 몇 가지 구성 옵션을 사용할 수 있습니다. 자세한 내용은 아래 각 인덱서 유형에 대한 구성 세부 정보를 참조하십시오.

### 속성 색인 {#the-property-index}

속성 인덱스는 속성 제약 조건이 있지만 전체 텍스트가 아닌 쿼리에 유용합니다. 다음 절차에 따라 구성할 수 있습니다.

1. 로 이동하여 CRXDE 열기 `http://localhost:4502/crx/de/index.jsp`
1. 아래에 노드 만들기 **oak:index**
1. 노드 이름 지정 **PropertyIndex**&#x200B;을 클릭하고 노드 유형을 로 설정합니다. **oak:QueryIndexDefinition**
1. 새 노드에 대해 다음 속성을 설정합니다.

   * **유형:**  `property` (유형 문자열)
   * **속성 이름:**  `jcr:uuid` (유형 이름)

   이 특정 예는 를 색인화합니다. `jcr:uuid` 연결된 노드의 UUID(범용 고유 식별자)를 표시하는 작업이 포함된 속성입니다.

1. 변경 사항을 저장합니다.

속성 인덱스에는 다음과 같은 구성 옵션이 있습니다.

* 다음 **유형** 속성은 인덱스의 유형을 지정하며, 이 경우 로 설정해야 합니다. **속성**

* 다음 **속성 이름** 속성은 인덱스에 저장된 속성 목록을 나타냅니다. 누락된 경우 노드 이름은 속성 이름 참조 값으로 사용됩니다. 이 예에서는 **jcr:uuid** 노드의 고유 식별자(UUID)를 표시하는 작업이 포함된 속성이 인덱스에 추가됩니다.

* 다음 **고유** 로 설정된 경우 플래그 지정 **true** 속성 인덱스에 고유성 제약 조건을 추가합니다.

* 다음 **선언 노드 유형** 속성을 사용하면 인덱스만 적용되는 특정 노드 유형을 지정할 수 있습니다.
* 다음 **색인 재지정** 로 설정된 경우 플래그 지정 **true**&#x200B;는 전체 콘텐츠 색인 재지정을 트리거합니다.

### 순서가 지정된 색인 {#the-ordered-index}

Ordered 인덱스는 속성 인덱스의 확장입니다. 하지만 더 이상 사용되지 않습니다. 이 유형의 인덱스는 (으)로 대체해야 합니다. [Lucene 속성 인덱스](#the-lucene-property-index).

### Lucene 전체 텍스트 색인 {#the-lucene-full-text-index}

Apache Lucene 기반의 전체 텍스트 인덱서는 AEM 6에서 사용할 수 있습니다.

전체 텍스트 색인이 구성된 경우 색인화된 다른 조건이 있는지 여부와 경로 제한이 있는지 여부에 관계없이 전체 텍스트 조건이 있는 모든 쿼리는 전체 텍스트 색인을 사용합니다.

전체 텍스트 색인이 구성되지 않은 경우 전체 텍스트 조건이 있는 쿼리가 예상대로 작동하지 않습니다.

색인이 비동기 백그라운드 스레드를 통해 업데이트되므로 백그라운드 프로세스가 완료될 때까지 짧은 시간 동안 일부 전체 텍스트 검색을 사용할 수 없습니다.

아래 절차에 따라 Lucene 전체 텍스트 인덱스를 구성할 수 있습니다.

1. CRXDE 를 열고 아래에 노드 만들기 **oak:index**.
1. 노드 이름 지정 **LuceneIndex** 노드 유형을 로 설정합니다. **oak:QueryIndexDefinition**
1. 노드에 다음 속성을 추가합니다.

   * **유형:**  `lucene` (유형 문자열)
   * **비동기:**  `async` (유형 문자열)

1. 변경 사항을 저장합니다.

Lucene 색인에는 다음과 같은 구성 옵션이 있습니다.

* 다음 **유형** 인덱스의 형식을 지정하는 속성을 **lucene**
* 다음 **비동기** 로 설정해야 하는 속성 **비동기**. 이렇게 하면 인덱스 업데이트 프로세스가 백그라운드 스레드로 전송됩니다.
* 다음 **includePropertyTypes** 속성에 대해 설명합니다. 이 속성은 인덱스에 포함된 속성 유형의 하위 집합을 정의합니다.
* 다음 **excludePropertyName** 속성 이름 목록을 정의하는 속성 - 인덱스에서 제외해야 하는 속성.
* 다음 **색인 재지정** 으로 설정된 경우 플래그 지정 **true**&#x200B;는 전체 콘텐츠 색인 재지정을 트리거합니다.

### 전체 텍스트 검색 이해 {#understanding-fulltext-search}

이 섹션의 설명서는 PostgreSQL, SQLite 및 MySQL의 Apache Lucene, Elasticsearch 및 전체 텍스트 인덱스에 적용됩니다. 다음 예제는 AEM / Oak / Lucene입니다.

<b>인덱싱할 데이터</b>

시작점은 인덱싱해야 하는 데이터입니다. 다음 문서를 예로 들어 보겠습니다.

| <b>문서 ID</b> | <b>경로</b> | <b>전체 텍스트</b> |
| --- | --- | --- |
| 100 | /content/rubik | &quot;루빅은 핀란드의 브랜드입니다.&quot; |
| 200 | /content/rubiksCube | 루빅 큐브는 1974년에 발명되었습니다. |
| 300 | /content/cube | &quot;큐브는 3차원 개체입니다.&quot; |


<b>반전된 인덱스</b>

색인 지정 메커니즘은 전체 텍스트를 &quot;토큰&quot;이라는 단어로 분할하고 &quot;반전된 색인&quot;이라는 색인을 빌드합니다. 이 색인에는 각 단어에 대해 나타나는 문서 목록이 포함되어 있습니다.

짧고 일반적인 단어(&quot;stopwords&quot;라고도 함)는 색인화되지 않습니다. 모든 토큰은 소문자로 변환되며 형태소 분석이 적용됩니다.

다음과 같은 특수 문자 *&quot;-&quot;* 인덱싱되지 않습니다.

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

<b>검색 중</b>

다음은 쿼리의 예입니다. 모든 특수 문자(예: *&#39;*)이 공백으로 대체되었습니다.

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


Lucene는 두 목록(또는 라운드 로빈) 사이를 왔다 갔다 합니다. `n` 목록, 검색 시 `n` 단어):

* &quot;루빅&quot;에서 읽으면 첫 번째 항목을 얻습니다. 10을 찾습니다.
* 첫 번째 항목은 &quot;큐브&quot;에서 읽습니다. `>` = 10. 10개는 찾을 수 없고, 다음 것은 30개입니다.
* &quot;루빅&quot;에서 읽으면 첫 번째 항목이 생깁니다. `>` = 30: 100을 찾습니다.
* 첫 번째 항목은 &quot;큐브&quot;에서 읽습니다. `>` = 100: 200을 찾습니다.
* &quot;루빅&quot;에서 읽으면 첫 번째 항목이 생깁니다. `>` = 200. 200개를 찾았습니다. 따라서 문서 200은 두 조건에 모두 일치합니다. 기억하고 있습니다.
* 다음 항목인 1000은 &quot;루빅&quot;에서 읽으십시오.
* 첫 번째 항목은 &quot;큐브&quot;에서 읽습니다. `>` = 1000: 2000을 찾습니다.
* &quot;루빅&quot;에서 읽으면 첫 번째 항목이 생깁니다. `>` = 2000: 목록의 끝.
* 마지막으로 검색을 중단할 수 있습니다.

아래 예와 같이 두 용어가 모두 포함된 유일한 문서는 200입니다.

| 200 | /content/rubiksCube | 루빅 큐브는 1974년에 발명되었습니다. |
| --- | --- | --- |

여러 항목이 발견되면 점수별로 정렬됩니다.

### Lucene 속성 색인 {#the-lucene-property-index}

다음 이후 **Oak 1.0.8**, Lucene을 사용하여 전체 텍스트가 아닌 속성 제한을 포함하는 인덱스를 만들 수 있습니다.

Lucene 속성 색인을 만들려면 **fulltextEnabled** 속성은 항상 false로 설정해야 합니다.

다음 예제 쿼리를 사용합니다.

```xml
select * from [nt:base] where [alias] = '/admin'
```

위의 쿼리에 대한 Lucene 속성 인덱스를 정의하려면 아래에 노드를 만들어 다음 정의를 추가할 수 있습니다 **`oak:index`:**

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
>Lucene 속성 인덱스에 대한 자세한 내용은 [Apache Jackrabbit Oak Lucene 설명서 페이지](https://jackrabbit.apache.org/oak/docs/query/lucene.html).

### Lucene 분석기 {#lucene-analyzers}

버전 1.2.0 이후 Oak는 Lucene 분석기를 지원합니다.

분석기는 문서가 색인화되었을 때와 쿼리 시간에 모두 사용됩니다. 분석기가 필드의 텍스트를 검사하고 토큰 스트림을 생성합니다. Lucene 분석기는 일련의 토큰화기 및 필터 클래스로 구성됩니다.

분석기는 다음을 통해 구성할 수 있습니다. `analyzers` 노드(유형) `nt:unstructured`) 안에 있는 `oak:index` 정의.

인덱스에 대한 기본 분석기는 `default` 분석기 노드의 하위 항목입니다.

![chlimage_1-149](assets/chlimage_1-149.png)

>[!NOTE]
>
>사용 가능한 분석기 목록은 사용 중인 Lucene 버전의 API 설명서를 참조하십시오.

#### Analyzer 클래스 직접 지정 {#specifying-the-analyzer-class-directly}

기본 제공 분석기를 사용하려면 아래 절차에 따라 구성할 수 있습니다.

1. 분석기를 사용할 인덱스를 아래에서 찾습니다. `oak:index` 노드.

1. 인덱스 아래에 라는 하위 노드를 만듭니다. `default` 유형 `nt:unstructured`.

1. 다음 속성을 사용하여 기본 노드에 속성을 추가합니다.

   * **이름:** `class`
   * **유형:** `String`
   * **값:** `org.apache.lucene.analysis.standard.StandardAnalyzer`

   값은 사용할 Analyzer 클래스의 이름입니다.

   옵션을 사용하여 분석기를 특정 Lucene 버전과 함께 사용하도록 설정할 수도 있습니다 `luceneMatchVersion` 문자열 속성입니다. Lucene 4.7에서 사용할 수 있는 올바른 구문은 다음과 같습니다.

   * **이름:** `luceneMatchVersion`
   * **유형:** `String`
   * **값:** `LUCENE_47`

   If `luceneMatchVersion` 는 제공되지 않으며 Oak는 함께 제공되는 Lucene 버전을 사용합니다.

1. Analyzer 구성에 중지 단어 파일을 추가하려면 `default` 다음 속성을 가진 항목:

   * **이름:** `stopwords`
   * **유형:** `nt:file`

#### 컴포지션을 통한 분석기 만들기 {#creating-analyzers-via-composition}

분석기는 다음을 기반으로 구성할 수도 있습니다. `Tokenizers`, `TokenFilters`, 및 `CharFilters`. 이렇게 하려면 분석기를 지정하고 나열된 순서로 적용되는 선택적 토큰라이저와 필터의 하위 노드를 만들면 됩니다. 참조: [https://cwiki.apache.org/confluence/display/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema](https://cwiki.apache.org/confluence/display/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema)

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

* `org.apache.lucene.analysis.standard.StandardTokenizerFactory` 다음과 같음 `standard`

* `org.apache.lucene.analysis.charfilter.MappingCharFilterFactory` 다음과 같음 `Mapping`

* `org.apache.lucene.analysis.core.StopFilterFactory` 다음과 같음 `Stop`

팩토리에 필요한 모든 구성 매개 변수가 해당 노드의 속성으로 지정됩니다.

외부 파일의 컨텐츠를 로드해야 하는 정지어 로드와 같은 경우에는 의 하위 노드를 만들어 컨텐츠를 제공할 수 있습니다. `nt:file` 해당 파일의 이름을 입력합니다.

### Solr 인덱스 {#the-solr-index}

Solr 인덱스의 목적은 전체 텍스트 검색이지만 경로, 속성 제한 및 기본 유형 제한 사항별로 검색을 인덱싱하는 데 사용할 수도 있습니다. 즉, Oak의 Solr 인덱스를 모든 유형의 JCR 쿼리에 사용할 수 있습니다.

AEM의 통합은 저장소 수준에서 수행되므로 Solr은 AEM과 함께 제공되는 새 저장소 구현인 Oak에서 사용할 수 있는 색인 중 하나입니다.

AEM 인스턴스를 사용하여 원격 서버로 작동하도록 구성할 수 있습니다.

### 단일 원격 Solr 서버로 AEM 구성 {#configuring-aem-with-a-single-remote-solr-server}

원격 Solr 서버 인스턴스에서 작동하도록 AEM을 구성할 수도 있습니다.

1. 최신 버전의 Solr을 다운로드하여 추출하십시오. 자세한 방법은 다음을 참조하십시오. [Apache Solr 설치 설명서](https://solr.apache.org/guide/6_6/installing-solr.html).
1. 이제 두 개의 Solr 샤드를 만듭니다. 이렇게 하려면 Solr의 압축을 푼 폴더에 각 분할에 대한 폴더를 만들면 됩니다.

   * 첫 번째 분할에 대해 폴더를 만듭니다.

   `<solrunpackdirectory>\aemsolr1\node1`

   * 두 번째 분할에 대해 폴더를 만듭니다.

   `<solrunpackdirectory>\aemsolr2\node2`

1. Solr 패키지에서 예제 인스턴스를 찾습니다. &quot;&quot;라는 폴더에 있습니다. `example`패키지의 루트에 있는 &quot;&quot;입니다.
1. 예제 인스턴스에서 다음 폴더를 두 개의 공유 폴더로 복사합니다( `aemsolr1\node1` 및 `aemsolr2\node2`):

   * `contexts`
   * `etc`
   * `lib`
   * `resources`
   * `scripts`
   * `solr-webapp`
   * `webapps`
   * `start.jar`

1. &quot;&quot;라는 폴더 만들기 `cfg`&quot;각각의 공유 폴더에 있습니다.
1. Solr 및 Zookeeper 구성 파일을 새로 만든 `cfg` 개 폴더.

   >[!NOTE]
   >
   >Solr 및 ZooKeeper 구성에 대한 자세한 내용은 [Solr 구성 설명서](https://cwiki.apache.org/confluence/display/solr/ConfiguringSolr) 및 [ZooKeeper 시작 안내서](https://zookeeper.apache.org/doc/r3.1.2/zookeeperStarted.html).

1. 로 이동하여 ZooKeeper 지원을 통해 첫 번째 분할을 시작합니다. `aemsolr1\node1` 다음 명령을 실행합니다.

   ```xml
   java -Xmx2g -Dbootstrap_confdir=./cfg/oak/conf -Dcollection.configName=myconf -DzkRun -DnumShards=2 -jar start.jar
   ```

1. 로 이동하여 두 번째 분할을 시작합니다. `aemsolr2\node2` 다음 명령을 실행합니다.

   ```xml
   java -Xmx2g -Djetty.port=7574 -DzkHost=localhost:9983 -jar start.jar
   ```

1. 두 Shards가 모두 시작된 후 의 Solr 인터페이스에 연결하여 모든 것이 작동되고 실행 중인지 테스트합니다. `http://localhost:8983/solr/#/`
1. AEM을 시작하고 의 웹 콘솔로 이동합니다. `http://localhost:4502/system/console/configMgr`
1. 아래에서 다음 구성을 설정합니다. **Oak Solr 원격 서버 구성**:

   * Solr HTTP URL: `http://localhost:8983/solr/`

1. 선택 **원격 Solr** 아래의 드롭다운 목록에서 **오크 솔** 서버 공급자입니다.

1. CRXDE로 이동한 다음 관리자로 로그인합니다.
1. 라는 노드 만들기 **solrIndex** 아래에 **oak:index**&#x200B;을 클릭하고 다음 속성을 설정합니다.

   * **유형:** solr(문자열 유형의)
   * **비동기:** 비동기(String 유형)
   * **색인 재지정:** true(부울 유형)

1. 변경 사항을 저장합니다.

#### Solr에 대한 권장 구성 {#recommended-configuration-for-solr}

다음은 이 문서에 설명된 세 가지 Solr 배포 모두에서 사용할 수 있는 기본 구성의 예입니다. AEM에 이미 있는 전용 속성 인덱스를 수용하므로 다른 애플리케이션과 함께 사용하지 마십시오.

아카이브를 제대로 사용하려면 아카이브 내용을 Solr Home 디렉토리에 직접 배치해야 합니다. 다중 노드 배포가 있는 경우 각 노드의 루트 폴더 바로 아래로 이동해야 합니다.

권장 Solr 구성 파일

[파일 가져오기](assets/recommended-conf.zip)

### AEM 색인화 도구 {#aem-indexing-tools}

또한 AEM 6.1에는 Adobe 컨설팅 서비스 Commons 도구 세트의 일부로 AEM 6.0에 있는 두 개의 색인 지정 도구가 통합되어 있습니다.

1. **쿼리 설명**: 관리자가 쿼리 실행 방법을 이해하는 데 도움이 되도록 설계된 도구입니다.
1. **Oak 색인 관리자**&#x200B;기존 인덱스를 유지 관리하기 위한 웹 사용자 인터페이스입니다.

이제 다음으로 이동하여 연결할 수 있습니다. **도구 - 작업 - 대시보드 - 진단** AEM 시작 화면에서 다음을 수행합니다.

사용 방법에 대한 자세한 내용은 [작업 대시보드 설명서](/help/sites-administering/operations-dashboard.md).

#### OSGi를 통해 속성 인덱스 생성 {#creating-property-indexes-via-osgi}

ACS Commons 패키지는 속성 인덱스를 만드는 데 사용할 수 있는 OSGi 구성도 표시합니다.

웹 콘솔에서 &quot;&quot;을 검색하여 액세스할 수 있습니다.**Oak 속성 인덱스 확인**&quot;.

![chlimage_1-150](assets/chlimage_1-150.png)

### 색인 지정 문제 해결 {#troubleshooting-indexing-issues}

쿼리가 실행되는 데 시간이 오래 걸리고 일반적인 시스템 응답 시간이 느려지는 상황이 발생할 수 있습니다.

이 섹션에서는 이러한 문제의 원인을 추적하기 위해 수행해야 하는 작업과 이를 해결하는 방법에 대한 조언을 제공합니다.

#### 분석을 위한 디버깅 정보 준비 {#preparing-debugging-info-for-analysis}

실행 중인 쿼리에 필요한 정보를 얻는 가장 쉬운 방법은 [쿼리 설명 도구](/help/sites-administering/operations-dashboard.md#explain-query). 이를 통해 로그 수준 정보를 확인하지 않고도 느린 쿼리를 디버깅하는 데 필요한 정확한 정보를 수집할 수 있습니다. 디버깅 중인 쿼리를 알고 있는 경우 이 방법이 좋습니다.

어떤 이유로든 가능하지 않은 경우, 단일 파일에 인덱싱 로그를 수집하여 특정 문제를 해결하는 데 사용할 수 있습니다.

#### 로깅 활성화 {#enable-logging}

로깅을 활성화하려면 다음을 활성화해야 합니다. **디버그** oak 색인 지정 및 쿼리와 관련된 범주에 대한 레벨 로그입니다. 이러한 범주는 다음과 같습니다.

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

다음 **com.day.cq.search** 범주는 AEM에서 제공한 QueryBuilder 유틸리티를 사용하는 경우에만 적용할 수 있습니다.

>[!NOTE]
>
>문제를 해결하려는 쿼리가 실행되는 기간 동안에만 로그를 DEBUG로 설정하는 것이 중요합니다. 그렇지 않으면 시간이 지남에 따라 로그에 많은 이벤트가 생성됩니다. 이러한 이유로 필요한 로그가 수집되면 위에서 언급한 범주에 대한 INFO 수준 로깅으로 다시 전환합니다.

다음 절차에 따라 로깅을 활성화할 수 있습니다.

1. 브라우저를 가리켜서 `https://serveraddress:port/system/console/slinglog`
1. 다음을 클릭합니다. **새 로거 추가** 콘솔의 아래쪽에 있는 단추.
1. 새로 만든 행에서 위에 언급된 범주를 추가합니다. 다음을 사용할 수 있습니다. **+** 단일 로거에 두 개 이상의 카테고리를 추가하려면 로그인합니다.
1. 선택 **디버그** 다음에서 **로그 수준** 드롭다운 목록입니다.
1. 출력 파일을 다음으로 설정 `logs/queryDebug.log`. 이렇게 하면 모든 DEBUG 이벤트가 단일 로그 파일로 상호 연결됩니다.
1. 쿼리를 실행하거나 디버그하려는 쿼리를 사용하는 페이지를 렌더링합니다.
1. 쿼리를 실행한 후 로깅 콘솔로 돌아가서 새로 만든 로거의 로그 수준을 다음으로 변경합니다. **정보**.

#### 색인 구성 {#index-configuration}

쿼리가 평가되는 방식은 주로 색인 구성의 영향을 받습니다. 색인 구성을 분석하거나 지원으로 보내는 것이 중요합니다. 구성을 콘텐츠 패키지로 가져오거나 JSON 렌디션을 가져올 수 있습니다.

일반적으로 인덱싱 구성은 `/oak:index` crxde의 노드에서는 다음 위치에서 JSON 버전을 가져올 수 있습니다.

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

을 통해 통합된 JMX 출력을 제공할 수도 있습니다. `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak.tidy.3.json`. 여기에는 JSON 형식의 모든 Oak 관련 MBean 세부 사항이 포함됩니다.

#### 기타 세부 정보 {#other-details}

다음과 같은 문제를 해결하는 데 도움이 되는 추가 세부 정보를 수집할 수 있습니다.

1. 인스턴스가 실행 중인 Oak 버전입니다. CRXDE를 열고 시작 페이지의 오른쪽 아래 모서리에 있는 버전을 확인하거나 의 버전을 확인하여 이를 확인할 수 있습니다. `org.apache.jackrabbit.oak-core` 번들.
1. 문제가 있는 쿼리의 QueryBuilder 디버거 출력입니다. 디버거는 다음 위치에서 액세스할 수 있습니다. `https://serveraddress:port/libs/cq/search/content/querydebug.html`
