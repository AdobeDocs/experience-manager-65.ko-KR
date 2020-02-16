---
title: Oak 쿼리 및 색인
seo-title: Oak 쿼리 및 색인
description: AEM에서 색인을 구성하는 방법을 알아봅니다.
seo-description: AEM에서 색인을 구성하는 방법을 알아봅니다.
uuid: a1233d2e-1320-43e0-9b18-cd6d1eeaad59
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 492741d5-8d2b-4a81-8f21-e621ef3ee685
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/queries-and-indexing
translation-type: tm+mt
source-git-commit: 1f7a45adc73b407c402a51b061632e72d97ca306

---


# Oak 쿼리 및 색인{#oak-queries-and-indexing}

>[!NOTE]
>
>이 문서는 AEM 6에서 색인을 구성하는 방법에 대해 설명합니다. 쿼리 및 색인 성능 최적화에 대한 우수 사례는 쿼리 및 [색인화에 대한 우수 사례를 참조하십시오](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

## 소개 {#introduction}

Jackrabbit 2와 달리 Oak은 기본적으로 컨텐츠를 색인화하지 않습니다. 기존 관계형 데이터베이스와 마찬가지로 필요한 경우 사용자 정의 인덱스를 만들어야 합니다. 특정 쿼리에 대한 인덱스가 없는 경우 많은 노드가 검색될 수 있습니다. 쿼리는 여전히 작동하지만 매우 느릴 수 있습니다.

Oak에서 인덱스 없이 쿼리가 발견되면 WARN 수준 로그 메시지가 인쇄됩니다.

```xml
*WARN* Traversed 1000 nodes with filter Filter(query=select ...) consider creating an index or changing the query
```

## 지원되는 쿼리 언어 {#supported-query-languages}

Oak 쿼리 엔진은 다음 언어를 지원합니다.

* XPath(권장)
* SQL-2
* SQL(더 이상 사용되지 않음)
* JQOM

## 인덱서 유형 및 비용 계산 {#indexer-types-and-cost-calculation}

Apache Oak 기반 백엔드를 사용하여 저장소에 서로 다른 인덱서를 연결할 수 있습니다.

인덱서 하나는 **속성**&#x200B;인덱스로, 인덱스 정의가 저장소 자체에 저장됩니다.

Apache **Lucene** 및 Solr에 대한 **** 구현도 기본적으로 사용할 수 있으며, 둘 다 전체 텍스트 인덱싱을 지원합니다.

사용 **가능한 다른 인덱서가** 없는 경우 순회 인덱스가 사용됩니다. 즉, 컨텐츠가 인덱싱되지 않고 컨텐츠 노드는 쿼리에 일치하는 항목을 찾기 위해 탐색됩니다.

쿼리에 여러 인덱서를 사용할 수 있는 경우 사용 가능한 각 인덱서는 쿼리 실행 비용을 예측합니다. 그러면 Oak가 예상 비용이 가장 낮은 인덱서를 선택합니다.

![chlimage_1-148](assets/chlimage_1-148.png)

위 다이어그램은 Apache Oak의 쿼리 실행 메커니즘에 대한 높은 수준의 표현입니다.

먼저 쿼리를 추상 구문 트리로 구문 분석합니다. 그런 다음 쿼리가 확인되고 Oak 쿼리의 기본 언어인 SQL-2로 변환됩니다.

그런 다음 각 색인이 참조에 대한 비용을 예측하도록 협의됩니다. 일단 그것이 완성되면, 가장 싼 색인의 결과가 검색된다. 마지막으로, 결과를 필터링하여 현재 사용자가 결과에 대한 읽기 액세스 권한을 가지고 있고 결과가 전체 쿼리와 일치하는지 확인합니다.

## 인덱스 구성 {#configuring-the-indexes}

>[!NOTE]
>
>대규모 저장소의 경우 인덱스를 작성하는 작업은 시간이 많이 걸립니다. 인덱스의 초기 생성과 다시 색인 작성(정의를 변경한 후 인덱스 다시 작성)에 모두 적용됩니다. Oak [인덱스 문제 해결](/help/sites-deploying/troubleshooting-oak-indexes.md) 및 [느린 다시 인덱싱](/help/sites-deploying/troubleshooting-oak-indexes.md#preventing-slow-re-indexing)방지를 참조하십시오.

MongoDB를 사용하는 경우와 전체 텍스트 색인에 대해 다시 색인화가 필요한 경우 텍스트 사전 추출 및 oak-run을 사용하여 초기 색인을 작성하고 다시 색인화하십시오.

인덱스는 **oak:index** 노드 아래의 저장소에서 노드로 구성됩니다.

인덱스 노드의 유형은 **oak:QueryIndexDefinition이어야 합니다.** 각 인덱서에는 노드 속성으로 몇 가지 구성 옵션을 사용할 수 있습니다. 자세한 내용은 아래 각 인덱서 유형에 대한 구성 세부 사항을 참조하십시오.

### 속성 색인 {#the-property-index}

속성 인덱스는 일반적으로 속성 제한이 있지만 전체 텍스트가 아닌 쿼리에 유용합니다. 다음 절차에 따라 구성할 수 있습니다.

1. 다음으로 이동하여 CRXDE 열기 `http://localhost:4502/crx/de/index.jsp`
1. oak:index 아래에 새 **노드 만들기**
1. 노드 이름을 PropertyIndex **로**&#x200B;지정하고 노드 유형을 **oak:QueryIndexDefinition으로 설정합니다.**
1. 새 노드에 대해 다음 속성을 설정합니다.

   * **** type: `property` (문자열 유형)
   * **** propertyNames: `jcr:uuid` (이름 유형)
   이 특정 예제는 속성이 연결되어 있는 노드의 UUID(Universal Unique Identifier)를 표시하는 `jcr:uuid` 속성을 인덱싱합니다.

1. 변경 사항을 저장합니다.

속성 색인에는 다음 구성 옵션이 있습니다.

* type **** 속성은 인덱스 유형을 지정하며, 이 경우 **속성으로 설정해야 합니다**

* propertyNames **** 속성은 인덱스에 저장할 속성 목록을 나타냅니다. 누락된 경우 노드 이름이 속성 이름 참조 값으로 사용됩니다. 이 예에서는 **작업이 노드의 고유 식별자(UUID)를 표시하는 jcr:uuid** 속성이 인덱스에 추가됩니다.

* true로 설정된 경우 **속성** 인덱스에 고유성 제약 조건을 추가하는 **고유한** 플래그.

* decoringNodeTypes **속성을** 사용하면 인덱스가 적용되는 특정 노드 유형을 지정할 수 있습니다.
* true로 설정된 경우 **전체** 컨텐츠 다시 색인을 트리거하는 다시 인덱스 ****&#x200B;플래그입니다.

### 순서가 지정된 색인 {#the-ordered-index}

Ordered 색인은 속성 인덱스의 확장입니다. 그러나 더 이상 사용되지 않습니다. 이 유형의 인덱스를 Lucene 속성 [인덱스로 바꿔야 합니다](#the-lucene-property-index).

### Lucene 전체 텍스트 인덱스 {#the-lucene-full-text-index}

Apache Lucene을 기반으로 하는 전체 텍스트 인덱서는 AEM 6에서 사용할 수 있습니다.

전체 텍스트 인덱스를 구성한 경우 전체 텍스트 조건이 있는 모든 쿼리는 인덱싱된 다른 조건이 있거나 경로 제한이 있더라도 전체 텍스트 인덱스를 사용합니다.

전체 텍스트 색인이 구성되지 않은 경우 전체 텍스트 조건이 있는 쿼리는 예상대로 작동하지 않습니다.

인덱스가 비동기 배경 스레드를 통해 업데이트되므로 백그라운드 프로세스가 완료될 때까지 작은 기간 동안 일부 전체 텍스트 검색을 사용할 수 없습니다.

아래 절차에 따라 Lucene 전체 텍스트 인덱스를 구성할 수 있습니다.

1. CRXDE를 열고 **oak:index**&#x200B;아래에 새 노드를 만듭니다.
1. 노드 이름을 LuceneIndex **로** 지정하고 노드 유형을 **oak:QueryIndexDefinition으로 설정합니다.**
1. 노드에 다음 속성을 추가합니다.

   * **** type: `lucene` (문자열 유형)
   * **** async: `async` (문자열 유형)

1. 변경 사항을 저장합니다.

Lucene 색인에는 다음 구성 옵션이 있습니다.

* 인덱스 유형을 지정할 **type** 속성은 **lucene으로 설정해야 합니다**
* **async** 로 설정해야 하는 async ****&#x200B;속성입니다. 그러면 색인 업데이트 프로세스가 배경 스레드로 전송됩니다.
* 인덱스에 포함할 속성 **** 유형의 하위 집합을 정의하는 includePropertyTypes 속성입니다.
* 속성 **이름의** 블랙 리스트(인덱스에서 제외해야 하는 속성)를 정의하는 excludePropertyNames 속성입니다.
* true로 **설정되면** 전체 컨텐츠 다시 색인을 트리거하는 다시 인덱스 ****&#x200B;플래그입니다.

### Lucene 속성 색인 {#the-lucene-property-index}

Oak **1.0.8부터** Lucene을 사용하여 전체 텍스트가 아닌 속성 제약 조건을 포함하는 인덱스를 만들 수 있습니다.

Lucene 속성 색인을 만들려면 **fulltextEnabled** 속성을 항상 false로 설정해야 합니다.

다음 예제 쿼리를 수행합니다.

```xml
select * from [nt:base] where [alias] = '/admin'
```

위의 쿼리에 대한 Lucene 속성 인덱스를 정의하려면 **oak:index 아래에 새 노드를 만들어 다음 정의를 추가할 수 있습니다.**

* **이름:** `LucenePropertyIndex`
* **유형:** `oak:QueryIndexDefinition`

노드가 만들어지면 다음 속성을 추가합니다.

* **유형:**

   ```
   lucene (of type String)
   ```

* **비동기:**

   ```
   async (of type String)
   ```

* **fulltextEnabled:**

   ```
   false (of type Boolean)
   ```

* **** includePropertyNames: `["alias"] (of type String)`

>[!NOTE]
>
>일반 속성 색인과 비교하여 Lucene 속성 색인은 항상 비동기 모드로 구성됩니다. 따라서 인덱스로 반환되는 결과가 항상 저장소의 최신 상태를 반영하지는 않을 수 있습니다.

>[!NOTE]
>
>Lucene 속성 색인에 대한 자세한 내용은 Apache Jackrabbit Oak [Lucene 설명서 페이지를](https://jackrabbit.apache.org/oak/docs/query/lucene.html)참조하십시오.

### Lucene Analyzers {#lucene-analyzers}

버전 1.2.0부터 Oak는 Lucene 분석을 지원합니다.

분석기는 문서가 인덱스될 때와 쿼리 시간에 모두 사용됩니다. 분석기가 필드 텍스트를 검사하고 토큰 스트림을 생성합니다. Lucene 분석기는 일련의 토큰기 및 필터 클래스로 구성됩니다.

분석기는 `analyzers` 정의 내의 노드(유형 `nt:unstructured``oak:index` )를 통해 구성할 수 있습니다.

인덱스에 대한 기본 분석기가 분석 노드의 `default` 하위 요소에 구성됩니다.

![chlimage_1-149](assets/chlimage_1-149.png)

>[!NOTE]
>
>사용 가능한 분석기의 목록은 사용 중인 Lucene 버전의 API 설명서를 참조하십시오.

#### Analyzer 클래스 직접 지정 {#specifying-the-analyzer-class-directly}

즉시 사용 가능한 분석기를 사용하려면 아래 절차에 따라 구성할 수 있습니다.

1. 노드 아래에 있는 분석기를 사용할 인덱스를 `oak:index` 찾습니다.

1. 인덱스 아래에서 `default` 유형이라는 하위 노드를 `nt:unstructured`만듭니다.

1. 다음 속성을 사용하여 기본 노드에 속성을 추가합니다.

   * **이름:** `class`
   * **유형:** `String`
   * **** 값: `org.apache.lucene.analysis.standard.StandardAnalyzer`
   값은 사용할 분석기 클래스의 이름입니다.

   선택적 `luceneMatchVersion` 문자열 속성을 사용하여 분석기를 특정 루킨 버전과 함께 사용하도록 설정할 수도 있습니다. Lucene 4.7과 함께 사용할 수 있는 동기화는 다음과 같습니다.

   * **이름:** `luceneMatchVersion`
   * **유형:** `String`
   * **** 값: `LUCENE_47`
   제공되지 `luceneMatchVersion` 않는 경우 Oak는 함께 제공되는 Lucene 버전을 사용합니다.

1. Analyzer 구성에 중지 단어 파일을 추가하려면 다음 속성을 사용하여 `default` 하나 아래에 새 노드를 만들 수 있습니다.

   * **이름:** `stopwords`
   * **유형:** `nt:file`

#### 컴포지션을 통해 분석 만들기 {#creating-analyzers-via-composition}

또한 분석기는 `Tokenizers`및 `TokenFilters` 를 기반으로 구성할 수 `CharFilters`있습니다. Analyzer를 지정하고 선택적인 토큰화 및 필터를 목록 순서대로 적용하여 하위 노드를 만들면 됩니다. 참조: https://wiki.apache.org/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema [](https://wiki.apache.org/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema)

이 노드 구조를 예로 생각해 보십시오.

* **이름:** `analyzers`

   * **이름:** `default`

      * **이름:** `charFilters`
      * **유형:** `nt:unstructured`

         * **이름:** `HTMLStrip`
         * **이름:** `Mapping`
      * **이름:** `tokenizer`

         * **속성 이름:** `name`

            * **유형:** `String`
            * **** 값: `Standard`
      * **이름:** `filters`
      * **유형:** `nt:unstructured`

         * **이름:** `LowerCase`
         * **이름:** `Stop`

            * **** 속성 이름: `words`

               * **유형:** `String`
               * **** 값: `stop1.txt, stop2.txt`
            * **이름:** `stop1.txt`

               * **유형:** `nt:file`
            * **이름:** `stop2.txt`

               * **유형:** `nt:file`





필터, charFilters 및 tokenizers의 이름은 팩토리 접미어를 제거하여 만듭니다. 따라서:

* `org.apache.lucene.analysis.standard.StandardTokenizerFactory` behance `standard`

* `org.apache.lucene.analysis.charfilter.MappingCharFilterFactory` behance `Mapping`

* `org.apache.lucene.analysis.core.StopFilterFactory` behance `Stop`

팩터리에 필요한 구성 매개 변수는 해당 코드의 속성으로 지정됩니다.

외부 파일의 컨텐츠를 로드해야 하는 중지 단어 등의 경우 해당 파일의 `nt:file` 유형의 하위 노드를 만들어 컨텐츠를 제공할 수 있습니다.

### The Solr Index {#the-solr-index}

Solr 인덱스의 용도는 주로 전체 텍스트 검색이지만 경로, 속성 제한 및 기본 유형 제한별로 검색을 인덱싱하는 데 사용할 수도 있습니다. 즉, Oak의 Solr 색인은 모든 유형의 JCR 쿼리에 사용할 수 있습니다.

AEM의 통합은 저장소 수준에서 발생하므로 Solr가 AEM과 함께 제공되는 새 저장소 구현인 Oak에서 사용할 수 있는 가능한 인덱스 중 하나입니다.

AEM 인스턴스가 포함된 서버로 또는 원격 서버로 작동하도록 구성할 수 있습니다.

### 임베디드 Solr 서버를 사용하여 AEM 구성 {#configuring-aem-with-an-embedded-solr-server}

>[!CAUTION]
>
>프로덕션 환경에서 임베드된 Solr 서버를 사용하지 마십시오. 개발 환경에서만 사용해야 합니다.

AEM은 웹 콘솔을 통해 구성할 수 있는 내장 Solr 서버와 함께 사용할 수 있습니다. 이 경우 Solr 서버는 임베드된 AEM 인스턴스와 동일한 JVM에서 실행됩니다.

포함된 Solr 서버를 다음 방법으로 구성할 수 있습니다.

1. 웹 콘솔 `https://serveraddress:4502/system/console/configMgr`
1. &quot;Oak Solr **서버 공급자**&quot;를 검색합니다.
1. 편집 단추를 누르고 다음 창에서 서버 유형을 **드롭다운 목록에서 임베드된** 솔로로 설정합니다.

1. 그런 다음 &quot;**Oak Solr embedded server configuration**&quot;을 편집하고 구성을 만듭니다. 구성 옵션에 대한 자세한 내용은 Apache Solr 웹 [사이트를](https://lucene.apache.org/solr/documentation.html)참조하십시오.

   >[!NOTE]
   >
   >Solr 홈 디렉토리(solr.home.path) 구성은 AEM 설치 폴더에서 동일한 이름의 폴더를 찾습니다.

1. CRXDE를 열고 관리자로 로그인합니다.
1. oak: **oak:QueryIndexDefinition** 유형의 **solrndex라는** 노드를 **다음 속성과 함께** 추가합니다.

   * **** type: `solr`(문자열 유형)
   * **** async: `async`(문자열 유형)
   * **** reindex: `true`(부울 유형)

1. 변경 사항을 저장합니다.

### 단일 원격 솔루션 서버를 사용하여 AEM 구성 {#configuring-aem-with-a-single-remote-solr-server}

또한 AEM은 원격 Solr 서버 인스턴스로 작동하도록 구성할 수 있습니다.

1. 최신 버전의 Solr을 다운로드하여 추출합니다. 이 방법에 대한 자세한 내용은 Apache Solr [설치 설명서를](https://cwiki.apache.org/confluence/display/solr/Installing+Solr)참조하십시오.
1. 이제 두 개의 Solr 섀드를 만듭니다. 이렇게 하려면 Solr이 업로드된 폴더의 각 공유 폴더에 폴더를 만들면 됩니다.

   * 첫 번째 공유 폴더의 경우 폴더를 만듭니다.
   `<solrunpackdirectory>\aemsolr1\node1`

   * 두 번째 공유의 경우 폴더를 만듭니다.
   `<solrunpackdirectory>\aemsolr2\node2`

1. Solr 패키지에서 예제 인스턴스를 찾습니다. 일반적으로 패키지의 루트에 있는 &quot; `example`&quot;라는 폴더에 있습니다.
1. 예제 인스턴스의 다음 폴더를 두 개의 공유 폴더( `aemsolr1\node1` 및 `aemsolr2\node2`)로 복사합니다.

   * `contexts`
   * `etc`
   * `lib`
   * `resources`
   * `scripts`
   * `solr-webapp`
   * `webapps`
   * `start.jar`

1. 두 공유 폴더 각각에 &quot; `cfg`&quot;라는 새 폴더를 만듭니다.
1. Solr 및 Zookeeper 구성 파일을 새로 만든 `cfg` 폴더에 배치합니다.

   >[!NOTE]
   >
   >Solr 및 ZooKeeper 구성에 대한 자세한 내용은 Solr [구성 설명서](https://wiki.apache.org/solr/ConfiguringSolr) 및 ZooKeeper [시작 안내서를 참조하십시오](https://zookeeper.apache.org/doc/r3.1.2/zookeeperStarted.html).

1. 다음 명령으로 이동하여 실행하여 ZooKeeper 지원으로 첫 번째 `aemsolr1\node1` 공유를 시작합니다.

   ```xml
   java -Xmx2g -Dbootstrap_confdir=./cfg/oak/conf -Dcollection.configName=myconf -DzkRun -DnumShards=2 -jar start.jar
   ```

1. 다음 명령으로 이동하여 `aemsolr2\node2` 실행하여 두 번째 공유를 시작합니다.

   ```xml
   java -Xmx2g -Djetty.port=7574 -DzkHost=localhost:9983 -jar start.jar
   ```

1. 두 섀드가 모두 시작된 후 솔루션 인터페이스에 연결하여 모든 것이 실행되고 있는지 테스트하십시오. `http://localhost:8983/solr/#/`
1. AEM을 시작하고 웹 콘솔의 `http://localhost:4502/system/console/configMgr`
1. Oak Solr **원격 서버 구성**&#x200B;아래에서 다음 구성을 설정합니다.

   * 솔루션 HTTP URL: `http://localhost:8983/solr/`

1. Oak **Solr** 서버 공급자 아래의 드롭다운 목록에서 **Remote Solr를** 선택합니다.

1. CRXDE 파섹
1. oak:index **아래에** solrIndex라는 ****&#x200B;새 노드를 만들고 다음 속성을 설정합니다.

   * **** type:solr(문자열 유형)
   * **** async:async(문자열 유형의 경우)
   * **** reindex:true(부울 유형)

1. 변경 사항을 저장합니다.

#### Solr 권장 구성 {#recommended-configuration-for-solr}

다음은 이 문서에 설명된 세 가지 솔루션 배포 모두에서 사용할 수 있는 기본 구성의 예입니다. AEM에 이미 있는 전용 속성 인덱스를 수용하며 다른 애플리케이션과 함께 사용해서는 안 됩니다.

제대로 사용하려면 아카이브의 컨텐츠를 Solr Home 디렉토리에 직접 배치해야 합니다. 다중 노드 배포의 경우 각 노드의 루트 폴더 바로 아래에 있어야 합니다.

권장 솔루션 구성 파일

[파일 가져오기](assets/recommended-conf.zip)

### AEM 인덱싱 도구 {#aem-indexing-tools}

AEM 6.1은 AEM 6.0에 있는 두 개의 인덱싱 도구를 Adobe Consulting Services Commons 도구 세트의 일부로 통합합니다.

1. **관리자가 쿼리가**&#x200B;실행되는 방법을 이해하는 데 도움이 되는 도구인 쿼리 설명;
1. **Oak 색인**&#x200B;관리자 - 기존 인덱스를 유지 관리하는 웹 사용자 인터페이스

이제 AEM 시작 화면에서 도구 - 작업 **- 대시보드** 진단으로 이동할 수 있습니다.

사용 방법에 대한 자세한 내용은 작업 대시보드 [설명서를](/help/sites-administering/operations-dashboard.md)참조하십시오.

#### OSGi를 통해 속성 인덱스 만들기 {#creating-property-indexes-via-osgi}

또한 ACS Commons 패키지는 속성 인덱스를 만드는 데 사용할 수 있는 OSGi 구성을 노출합니다.

&quot;Ensure Oak 속성 인덱스&quot;를 검색하여 웹 콘솔에서&#x200B;**액세스할 수 있습니다**.

![chlimage_1-150](assets/chlimage_1-150.png)

### 색인 문제 해결 {#troubleshooting-indexing-issues}

쿼리를 실행하는 데 시간이 오래 걸리고 일반 시스템 응답 시간이 느려지는 경우가 발생할 수 있습니다.

이 섹션에서는 이러한 문제의 원인을 추적하기 위해 수행해야 하는 사항에 대한 권장 사항 및 해결 방법에 대한 조언을 제공합니다.

#### 분석을 위한 디버깅 정보 준비 {#preparing-debugging-info-for-analysis}

실행되는 쿼리에 대한 필수 정보를 얻는 가장 쉬운 방법은 쿼리 설명 [도구를](/help/sites-administering/operations-dashboard.md#explain-query)사용하는 것입니다. 이렇게 하면 로그 수준 정보를 참조하지 않고도 느린 쿼리를 디버깅하는 데 필요한 정확한 정보를 수집할 수 있습니다. 디버깅 중인 쿼리를 알고 있는 경우 유용합니다.

어떤 이유로든 이렇게 할 수 없는 경우 단일 파일에 색인 로그를 수집하여 특정 문제를 해결하는 데 사용할 수 있습니다.

#### 로깅 사용 {#enable-logging}

로깅을 사용하려면 Oak 인덱싱 및 **쿼리와** 관련된 범주에 대한 DEBUG 수준 로그를 활성화해야 합니다. 이러한 범주는 다음과 같습니다.

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

com.day.cq.se **검색** 카테고리는 AEM 제공 QueryBuilder 유틸리티를 사용하는 경우에만 해당됩니다.

>[!NOTE]
>
>문제 해결하려는 쿼리가 실행되는 동안 로그가 DEBUG로만 설정되어 있어야 하며, 그렇지 않으면 시간에 따라 로그에 많은 이벤트가 생성됩니다. 따라서 필요한 로그가 수집되면 위에 언급된 카테고리에 대한 정보 수준 로깅으로 다시 전환됩니다.

다음 절차에 따라 로깅을 활성화할 수 있습니다.

1. 브라우저에서 `https://serveraddress:port/system/console/slinglog`
1. 콘솔 **아래쪽에 있는 Add new** Logger 버튼을 클릭합니다.
1. 새로 만든 행에서 위에 언급된 카테고리를 추가합니다. + **기호를 사용하여** 단일 로거에 두 개 이상의 카테고리를 추가할 수 있습니다.
1. 로그 **수준** 드롭다운 목록에서 **디버그를** 선택합니다.
1. 출력 파일을 로 `logs/queryDebug.log`설정합니다. 이렇게 하면 모든 DEBUG 이벤트가 하나의 로그 파일에 상호 연결됩니다.
1. 쿼리를 실행하거나 디버깅할 쿼리를 사용하는 페이지를 렌더링합니다.
1. 쿼리를 실행한 후 로깅 콘솔로 돌아가 새로 만든 로거의 로그 수준을 INFO로 **변경합니다**.

#### 색인 구성 {#index-configuration}

쿼리가 평가되는 방식은 인덱스 구성의 영향을 받습니다. 분석하거나 지원을 위해 전송하려면 색인 구성을 가져오는 것이 중요합니다. 구성을 콘텐츠 패키지로 가져오거나 JSON 변환을 가져올 수 있습니다.

대부분의 경우 색인 구성은 CRXDE의 `/oak:index` 노드 아래에 저장되므로 JSON 버전을 다음 위치에 가져올 수 있습니다.

`https://serveraddress:port/oak:index.tidy.-1.json`

인덱스가 다른 위치에 구성된 경우 그에 따라 경로를 변경합니다.

#### MBean 출력 {#mbean-output}

경우에 따라 디버깅을 위해 색인 관련 MBeans의 출력을 제공하는 것이 유용합니다. 다음을 통해 이 작업을 수행할 수 있습니다.

1. 다음 JMX 콘솔로 이동합니다.
   `https://serveraddress:port/system/console/jmx`

1. 다음 MBeans를 검색합니다.

   * Lucene Index 통계
   * CopyOnRead 지원 통계
   * Oak 쿼리 통계
   * IndexStats

1. 각 MBeans를 클릭하여 성능 통계를 가져옵니다. 스크린샷을 만들거나 지원이 필요한 경우 아래에 적어 둡니다.

다음 URL에서 이러한 통계의 JSON 변형을 가져올 수도 있습니다.

* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`

또한 를 통해 통합된 JMX 출력을 제공할 수 `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak.tidy.3.json`있습니다. 여기에는 JSON 포맷의 모든 Oak 관련 MBean 정보가 포함됩니다.

#### 기타 세부 사항 {#other-details}

다음과 같은 문제를 해결하는 데 도움이 되도록 추가 세부 정보를 수집할 수 있습니다.

1. 인스턴스가 실행 중인 Oak 버전입니다. CRXDE를 열고 시작 페이지의 오른쪽 아래에 있는 버전을 보거나 `org.apache.jackrabbit.oak-core` 번들 버전을 확인하면 이를 확인할 수 있습니다.
1. 문제 쿼리의 QueryBuilder 디버거 출력입니다. 디버거에 액세스할 수 있는 위치: `https://serveraddress:port/libs/cq/search/content/querydebug.html`

