---
title: Oak 쿼리 및 색인 지정
seo-title: Oak Queries and Indexing
description: AEM에서 인덱스를 구성하는 방법을 알아봅니다.
seo-description: Learn how to configure indexes in AEM.
uuid: a1233d2e-1320-43e0-9b18-cd6d1eeaad59
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 492741d5-8d2b-4a81-8f21-e621ef3ee685
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/queries-and-indexing
feature: Configuring
exl-id: d9ec7728-84f7-42c8-9c80-e59e029840da
source-git-commit: b27a7a1cc2295b1640520dcb56be4f3eb4851499
workflow-type: tm+mt
source-wordcount: '2674'
ht-degree: 2%

---

# Oak 쿼리 및 색인 지정{#oak-queries-and-indexing}

>[!NOTE]
>
>이 문서는 AEM 6의 인덱스 구성에 대한 것입니다. 쿼리 및 색인 지정 성능 최적화에 대한 우수 사례가 필요하면 를 참조하십시오 [쿼리 및 색인 생성에 대한 우수 사례](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

## 소개 {#introduction}

Jackrabbit 2와 달리 Oak는 기본적으로 컨텐츠를 색인화하지 않습니다. 기존 관계형 데이터베이스와 마찬가지로 필요한 경우 사용자 정의 인덱스를 만들어야 합니다. 특정 쿼리에 대한 인덱스가 없는 경우 많은 노드가 트래버스될 수 있습니다. 쿼리는 여전히 작동하지만 속도가 매우 느릴 수 있습니다.

Oak에 색인 없이 쿼리가 나타나면 WARN 수준 로그 메시지가 인쇄됩니다.

```xml
*WARN* Traversed 1000 nodes with filter Filter(query=select ...) consider creating an index or changing the query
```

## 지원되는 쿼리 언어 {#supported-query-languages}

Oak 쿼리 엔진은 다음 언어를 지원합니다.

* XPath(권장)
* SQL-2
* SQL(사용 중지)
* JQOM

## 인덱서 유형 및 비용 계산 {#indexer-types-and-cost-calculation}

Apache Oak 기반 백엔드를 사용하면 다양한 인덱서를 리포지토리에 연결할 수 있습니다.

색인은 **속성 인덱스**- 저장소 자체에 인덱스 정의가 저장되는 위치입니다.

용 구현 **Apache Lucene** 및 **Solr** 전체 텍스트 색인을 지원하는 기본값에서도 사용할 수 있습니다.

다음 **순회 인덱스** 다른 색인을 사용할 수 없는 경우 사용됩니다. 즉, 컨텐츠가 인덱싱되지 않고 컨텐츠 노드가 검색되어 쿼리에 일치하는 항목을 찾습니다.

쿼리에 여러 인덱서를 사용할 수 있는 경우 사용 가능한 각 인덱서는 쿼리를 실행하는 비용을 예측합니다. 그러면 Oak가 예상 비용이 가장 낮은 인덱서를 선택합니다.

![chlimage_1-148](assets/chlimage_1-148.png)

위의 다이어그램은 Apache Oak의 쿼리 실행 메커니즘에 대한 높은 수준의 표현입니다.

먼저 쿼리가 추상 구문 트리로 구문 분석됩니다. 그런 다음 쿼리를 확인하고 Oak 쿼리의 기본 언어인 SQL-2로 변환됩니다.

다음으로, 각 색인이 질의 비용을 예상하기 위해 상담됩니다. 일단 그것이 완료되면, 가장 싼 색인의 결과가 검색됩니다. 마지막으로, 결과가 필터링되어 현재 사용자가 결과에 대한 읽기 권한을 가지고 있고 결과가 전체 쿼리와 일치하는지 확인합니다.

## 인덱스 구성 {#configuring-the-indexes}

>[!NOTE]
>
>대규모 저장소의 경우 인덱스를 만드는 작업은 시간이 많이 걸립니다. 인덱스를 처음 만들고 다시 인덱싱(정의를 변경한 후 인덱스를 다시 구축)에 대해 모두 적용됩니다. 참조 - [Oak 색인 문제 해결](/help/sites-deploying/troubleshooting-oak-indexes.md) 및 [느린 재인덱싱 방지](/help/sites-deploying/troubleshooting-oak-indexes.md#preventing-slow-re-indexing).

매우 큰 저장소에서 재색인화가 필요한 경우, 특히 MongoDB를 사용하고 전체 텍스트 인덱스의 경우 텍스트 사전 추출을 고려하고 oak-run을 사용하여 초기 인덱스를 작성하고 다시 색인화합니다.

인덱스는 저장소 아래의 노드로 구성됩니다 **oak:index** 노드 아래에 있어야 합니다.

인덱스 노드의 유형은 다음과 같아야 합니다. **oak:QueryIndexDefinition.** 각 인덱서는 노드 속성으로 몇 가지 구성 옵션을 사용할 수 있습니다. 자세한 내용은 아래의 각 인덱서 유형에 대한 구성 세부 정보를 참조하십시오.

### 속성 인덱스 {#the-property-index}

속성 인덱스는 일반적으로 속성 제약 조건이 있지만 전체 텍스트가 아닌 쿼리에 유용합니다. 다음 절차에 따라 구성할 수 있습니다.

1. 로 이동하여 CRXDE를 엽니다. `http://localhost:4502/crx/de/index.jsp`
1. 아래에 새 노드 만들기 **oak:index**
1. 노드 이름을 지정합니다 **PropertyIndex**, 그리고 노드 유형을 로 설정합니다. **oak:QueryIndexDefinition**
1. 새 노드에 대해 다음 속성을 설정합니다.

   * **유형:**  `property` (문자열 유형)
   * **propertyNames:**  `jcr:uuid` (유형 이름)

   이 특정 예는 `jcr:uuid` 속성이 연결된 노드의 UUID(Universally Unique Identifier)를 표시하는 작업입니다.

1. 변경 사항을 저장합니다.

속성 색인에는 다음 구성 옵션이 있습니다.

* 다음 **유형** 속성은 인덱스 유형을 지정하고 이 경우 **속성**

* 다음 **propertyNames** 속성은 인덱스에 저장할 속성 목록을 나타냅니다. 누락된 경우 노드 이름이 속성 이름 참조 값으로 사용됩니다. 이 예에서 **jcr:uuid** 노드의 고유 식별자(UUID)를 노출하는 작업이 있는 속성이 인덱스에 추가됩니다.

* 다음 **고유** 플래그 지정 **true** 속성 인덱스에 고유성 제약 조건을 추가합니다.

* 다음 **선언NodeTypes** 속성을 사용하면 색인이 적용될 특정 노드 유형을 지정할 수 있습니다.
* 다음 **다시 색인화** 로 설정된 경우 **true**&#x200B;은(는) 전체 컨텐츠 재색인을 트리거합니다.

### 순차 인덱스 {#the-ordered-index}

Ordered 색인은 속성 인덱스의 확장입니다. 하지만 더 이상 사용되지 않습니다. 이 형식의 인덱스를 [Lucene 속성 색인](#the-lucene-property-index).

### Lucene 전체 텍스트 인덱스 {#the-lucene-full-text-index}

AEM 6에서는 Apache Lucene을 기반으로 하는 전체 텍스트 인덱서를 사용할 수 있습니다.

전체 텍스트 인덱스를 구성하는 경우 전체 텍스트 조건이 있는 모든 쿼리는 인덱싱된 다른 조건이 있는지 여부와 경로 제한이 있더라도 전체 텍스트 인덱스를 사용합니다.

전체 텍스트 인덱스를 구성하지 않으면 전체 텍스트 조건이 있는 쿼리가 예상대로 작동하지 않습니다.

인덱스가 비동기 백그라운드 스레드를 통해 업데이트되므로 백그라운드 프로세스가 완료될 때까지 작은 기간 동안 일부 전체 텍스트 검색을 사용할 수 없습니다.

아래 절차에 따라 Lucene 전체 텍스트 인덱스를 구성할 수 있습니다.

1. CRXDE를 열고 아래에 새 노드를 만듭니다 **oak:index**.
1. 노드 이름을 지정합니다 **LuceneIndex** 노드 유형을 로 설정하고 **oak:QueryIndexDefinition**
1. 노드에 다음 속성을 추가합니다.

   * **유형:**  `lucene` (문자열 유형)
   * **비동기:**  `async` (문자열 유형)

1. 변경 사항을 저장합니다.

Lucene 색인에는 다음과 같은 구성 옵션이 있습니다.

* 다음 **유형** 인덱스 유형을 지정할 속성을 **루센**
* 다음 **비동기** 로 설정해야 하는 속성 **비동기**. 그러면 인덱스 업데이트 프로세스가 백그라운드 스레드에 전송됩니다.
* 다음 **includePropertyTypes** 인덱스에 포함할 속성 유형의 하위 집합을 정의하는 속성입니다.
* 다음 **excludePropertyNames** 속성 이름 목록을 정의하는 속성입니다. 인덱스에서 제외해야 하는 속성입니다.
* 다음 **다시 색인화** 로 설정할 때 플래그 지정 **true**&#x200B;에서 전체 컨텐츠 다시 색인을 트리거합니다.

### Lucene 속성 인덱스 {#the-lucene-property-index}

이후 **Oak 1.0.8**, Lucene 을 사용하여 전체 텍스트가 아닌 속성 제약 조건을 포함하는 인덱스를 만들 수 있습니다.

Lucene 속성 인덱스를 얻으려면 **fulltextEnabled** 속성은 항상 false로 설정해야 합니다.

다음 예제 쿼리를 수행합니다.

```xml
select * from [nt:base] where [alias] = '/admin'
```

위의 쿼리에 대한 Lucene 속성 인덱스를 정의하려면 아래에 새 노드를 만들어 다음 정의를 추가할 수 있습니다 **oak:index:**

* **이름:** `LucenePropertyIndex`
* **유형:** `oak:QueryIndexDefinition`

노드가 만들어지면 다음 속성을 추가합니다.

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
>일반 속성 색인과 비교하여 Lucene 속성 색인은 항상 비동기 모드로 구성됩니다. 따라서 색인에 의해 반환된 결과가 항상 리포지토리의 최신 상태를 반영하지는 않을 수 있습니다.

>[!NOTE]
>
>Lucene 속성 인덱스에 대한 자세한 내용은 [Apache Jackrabbit Oak Lucene 설명서 페이지](https://jackrabbit.apache.org/oak/docs/query/lucene.html).

### Lucene Analyzers {#lucene-analyzers}

버전 1.2.0부터 Oak는 Lucene 분석기를 지원합니다.

분석기는 문서가 인덱스될 때와 쿼리 시간에 모두 사용됩니다. 분석기는 필드 텍스트를 검사하고 토큰 스트림을 생성합니다. Lucene 분석기는 일련의 토큰기 및 필터 클래스로 구성됩니다.

분석기는 `analyzers` 노드(유형) `nt:unstructured`) 내의 `oak:index` 정의.

인덱스에 대한 기본 분석기는 `default` 분석기 노드의 하위 노드입니다.

![chlimage_1-149](assets/chlimage_1-149.png)

>[!NOTE]
>
>사용 가능한 분석기 목록을 보려면 사용 중인 Lucene 버전의 API 설명서를 참조하십시오.

#### Analyzer 클래스 직접 지정 {#specifying-the-analyzer-class-directly}

즉시 사용 가능한 분석기를 사용하려면 아래 절차에 따라 구성할 수 있습니다.

1. 아래의 분석기를 사용할 인덱스를 찾습니다. `oak:index` 노드 아래에 있어야 합니다.

1. 인덱스 아래에서 `default` 유형 `nt:unstructured`.

1. 다음 속성을 사용하여 기본 노드에 속성을 추가합니다.

   * **이름:** `class`
   * **유형:** `String`
   * **값:** `org.apache.lucene.analysis.standard.StandardAnalyzer`

   값은 사용할 Analyzer 클래스의 이름입니다.

   옵션을 사용하여 특정 lucene 버전과 함께 사용할 분석기를 설정할 수도 있습니다 `luceneMatchVersion` 문자열 속성입니다. Lucene 4.7과 함께 사용할 수 있는 올바른 동기화는 다음과 같습니다.

   * **이름:** `luceneMatchVersion`
   * **유형:** `String`
   * **값:** `LUCENE_47`

   If `luceneMatchVersion` 이 제공되지 않으면 Oak는 함께 제공되는 Lucene 버전을 사용합니다.

1. Analyzer 구성에 Stopwords 파일을 추가하려면 `default` 다음 속성이 있는 하나:

   * **이름:** `stopwords`
   * **유형:** `nt:file`

#### 컴포지션을 통해 분석기 만들기 {#creating-analyzers-via-composition}

또한 분석기는 `Tokenizers`, `TokenFilters` 및 `CharFilters`. 분석기를 지정하고 나열된 순서로 적용할 선택적 토큰기 및 필터의 하위 노드를 만들어 이 작업을 수행할 수 있습니다. 참조 - [https://wiki.apache.org/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema](https://wiki.apache.org/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema)

이 노드 구조를 예로 간주하십시오.

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





필터, charFilters 및 tokenizer의 이름은 공장 접미사를 제거하여 형성됩니다. 따라서

* `org.apache.lucene.analysis.standard.StandardTokenizerFactory` 다음과 같이 `standard`

* `org.apache.lucene.analysis.charfilter.MappingCharFilterFactory` 다음과 같이 `Mapping`

* `org.apache.lucene.analysis.core.StopFilterFactory` 다음과 같이 `Stop`

팩토리에 필요한 구성 매개변수는 해당 코드의 속성으로 지정됩니다.

외부 파일의 컨텐츠를 로드해야 하는 중지 단어를 로드하는 등의 경우 의 하위 노드를 만들어 컨텐츠를 제공할 수 있습니다 `nt:file` 해당 파일의 유형을 입력합니다.

### Solr 인덱스 {#the-solr-index}

Solr 인덱스의 목적은 주로 전체 텍스트 검색이지만 경로, 속성 제한 및 기본 유형 제한 사항별로 검색을 인덱싱하는 데 사용할 수도 있습니다. 즉, Oak의 Solr 색인은 모든 유형의 JCR 쿼리에 사용할 수 있습니다.

AEM의 통합은 저장소 수준에서 진행되므로 Solr이 AEM과 함께 제공된 새 저장소 구현인 Oak에서 사용할 수 있는 인덱스 중 하나입니다.

AEM 인스턴스를 사용하여 원격 서버로 작동하도록 구성할 수 있습니다.

### 단일 원격 솔루션 서버로 AEM 구성 {#configuring-aem-with-a-single-remote-solr-server}

원격 Solr 서버 인스턴스에서 작동하도록 AEM을 구성할 수도 있습니다.

1. 최신 버전의 Solr를 다운로드하여 추출합니다. 이 작업을 수행하는 방법에 대한 자세한 내용은 [Apache Solr 설치 설명서](https://cwiki.apache.org/confluence/display/solr/Installing+Solr).
1. 이제 두 개의 Solr 섀드를 만듭니다. 이렇게 하려면 Solr이 압축을 푼 폴더에서 각 공유 폴더에 대해 폴더를 만들면 됩니다.

   * 첫 번째 공유의 경우 폴더를 만듭니다.

   `<solrunpackdirectory>\aemsolr1\node1`

   * 두 번째 공유의 경우 폴더를 만듭니다.

   `<solrunpackdirectory>\aemsolr2\node2`

1. 솔루션 패키지에서 예제 인스턴스를 찾습니다. 일반적으로 &quot; 폴더에 있습니다. `example`&quot; 를 클릭합니다.
1. 예제 인스턴스에서 다음 폴더를 두 개의 공유 폴더로 복사합니다( `aemsolr1\node1` 및 `aemsolr2\node2`):

   * `contexts`
   * `etc`
   * `lib`
   * `resources`
   * `scripts`
   * `solr-webapp`
   * `webapps`
   * `start.jar`

1. 새 폴더 만들기(&quot;) `cfg`&quot; 두 개의 공유 폴더 각각에 표시됩니다.
1. Solr 및 Zookeeper 구성 파일을 새로 만든 파일에 배치합니다 `cfg` 폴더.

   >[!NOTE]
   >
   >Solr 및 동물원은 Keeper 구성에 대한 자세한 내용은 [솔루션 구성 설명서](https://wiki.apache.org/solr/ConfiguringSolr) 그리고 [동물원은 시작 안내서](https://zookeeper.apache.org/doc/r3.1.2/zookeeperStarted.html).

1. 로 이동하여 동물원은 Supermeer를 지원하여 첫 번째 샤드를 시작합니다 `aemsolr1\node1` 및 다음 명령을 실행합니다.

   ```xml
   java -Xmx2g -Dbootstrap_confdir=./cfg/oak/conf -Dcollection.configName=myconf -DzkRun -DnumShards=2 -jar start.jar
   ```

1. 다음으로 이동하여 두 번째 분할을 시작합니다. `aemsolr2\node2` 및 다음 명령을 실행합니다.

   ```xml
   java -Xmx2g -Djetty.port=7574 -DzkHost=localhost:9983 -jar start.jar
   ```

1. 두 단계가 모두 시작되면 의 Solr 인터페이스에 연결하여 모든 것이 작동 중인지 테스트합니다. `http://localhost:8983/solr/#/`
1. AEM을 시작하고 웹 콘솔로 이동합니다. `http://localhost:4502/system/console/configMgr`
1. 에서 다음 구성을 설정합니다. **Oak Solr 원격 서버 구성**:

   * 솔루션 HTTP URL: `http://localhost:8983/solr/`

1. 선택 **원격 솔루션** 아래의 드롭다운 목록에서 **Oak Solr** 서버 공급자.

1. CRXDE로 이동하고 관리자로 로그인합니다.
1. 새 노드를 만듭니다. **solrIndex** 아래에 **oak:index**&#x200B;를 설정하고 다음 속성을 설정합니다.

   * **유형:** solr(문자열 유형)
   * **비동기:** async(문자열 유형)
   * **다시 색인화:** true(부울 유형)

1. 변경 사항을 저장합니다.

#### 솔루션에 대한 권장 구성 {#recommended-configuration-for-solr}

다음은 이 문서에 설명된 세 가지 솔루션 배포와 함께 사용할 수 있는 기본 구성의 예입니다. AEM에 이미 있는 전용 속성 인덱스를 수용하며 다른 응용 프로그램과 함께 사용해서는 안 됩니다.

제대로 사용하려면 아카이브의 컨텐츠를 Solr Home 디렉토리에 직접 배치해야 합니다. 다중 노드 배포의 경우 각 노드의 루트 폴더 바로 아래에 있어야 합니다.

권장되는 솔루션 구성 파일

[파일 가져오기](assets/recommended-conf.zip)

### AEM 색인 지정 도구 {#aem-indexing-tools}

AEM 6.1은 또한 Adobe Consulting Services Commons 도구 세트의 일부로서 AEM 6.0에 있는 두 개의 색인 도구를 통합합니다.

1. **쿼리 설명**, 관리자가 쿼리가 실행되는 방식을 이해하는 데 도움이 되는 도구입니다.
1. **Oak 색인 관리자**&#x200B;기존 인덱스를 유지 관리하는 웹 사용자 인터페이스입니다.

이제 로 이동하여 연락이 가능합니다 **도구 - 작업 - 대시보드 - 진단** AEM 시작 화면에서 클릭합니다.

사용 방법에 대한 자세한 내용은 [Operations Dashboard 설명서](/help/sites-administering/operations-dashboard.md).

#### OSGi를 통해 속성 인덱스 만들기 {#creating-property-indexes-via-osgi}

또한 ACS Commons 패키지는 속성 인덱스를 만드는 데 사용할 수 있는 OSGi 구성을 노출합니다.

웹 콘솔에서 &quot;**Oak 속성 색인 확인**&quot;.

![chlimage_1-150](assets/chlimage_1-150.png)

### 색인 문제 해결 {#troubleshooting-indexing-issues}

쿼리가 실행되는 데 시간이 오래 걸리고 일반 시스템 응답 시간이 느린 경우 상황이 발생할 수 있습니다.

이 섹션에서는 이러한 문제의 원인을 추적하고 이를 해결하는 방법에 대한 조언을 얻기 위해 수행해야 하는 작업에 대한 일련의 권장 사항을 제공합니다.

#### 분석을 위한 디버깅 정보 준비 {#preparing-debugging-info-for-analysis}

실행 중인 쿼리에 필요한 정보를 가져오는 가장 쉬운 방법은 [쿼리 도구 설명](/help/sites-administering/operations-dashboard.md#explain-query). 이렇게 하면 로그 수준 정보를 참조하지 않고도 느린 쿼리를 디버깅하는 데 필요한 정확한 정보를 수집할 수 있습니다. 디버깅 중인 쿼리를 알고 있는 경우에는 이 작업이 좋습니다.

어떤 이유로든 이렇게 할 수 없는 경우 인덱싱 로그를 단일 파일로 취합하여 특정 문제를 해결하는 데 사용할 수 있습니다.

#### 로깅 활성화 {#enable-logging}

로깅을 사용하려면 **디버그** Oak 색인 및 쿼리와 관련된 카테고리에 대한 수준 로그입니다. 이러한 카테고리는 다음과 같습니다.

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

다음 **com.day.cq.search** 범주는 AEM에서 제공한 QueryBuilder 유틸리티를 사용하는 경우에만 적용할 수 있습니다.

>[!NOTE]
>
>문제를 해결하려는 쿼리가 실행되는 동안 로그가 DEBUG로만 설정되어 있어야 합니다. 그렇지 않으면 시간에 따라 로그에 많은 이벤트가 생성됩니다. 따라서 필요한 로그가 수집되면 위에 언급된 카테고리에 대한 INFO 수준 로깅으로 다시 전환합니다.

다음 절차에 따라 로깅을 활성화할 수 있습니다.

1. 브라우저를 `https://serveraddress:port/system/console/slinglog`
1. 을(를) 클릭합니다. **새 로거 추가** 콘솔 아래쪽에 있는 단추.
1. 새로 만든 행에서 위에 언급된 카테고리를 추가합니다. 를 사용할 수 있습니다 **+** 단일 로거에 두 개 이상의 카테고리를 추가하려면 로그인합니다.
1. 선택 **디버그** 에서 **로그 수준** 드롭다운 목록
1. 출력 파일을 로 설정합니다. `logs/queryDebug.log`. 이렇게 하면 모든 DEBUG 이벤트가 단일 로그 파일에 상호 연결됩니다.
1. 쿼리를 실행하거나 디버그하려는 쿼리를 사용하는 페이지를 렌더링합니다.
1. 쿼리를 실행했으면 로깅 콘솔로 돌아가서 새로 만든 로거의 로그 레벨을 로 변경합니다. **정보**.

#### 인덱스 구성 {#index-configuration}

쿼리가 평가되는 방식은 인덱스 구성에 의해 크게 영향을 받습니다. 분석하거나 지원하기 위해 전송하려면 인덱스 구성을 가져오는 것이 중요합니다. 구성을 컨텐츠 패키지로 가져오거나 JSON 변환을 가져올 수 있습니다.

대부분의 경우 색인 구성은 `/oak:index` 노드 아래에 JSON 버전이 있습니다.

`https://serveraddress:port/oak:index.tidy.-1.json`

인덱스가 다른 위치에 구성되어 있으면 그에 따라 경로를 변경합니다.

#### MBean 출력 {#mbean-output}

경우에 따라 디버깅에 인덱스 관련 MBans의 출력을 제공하는 것이 도움이 됩니다. 다음을 통해 이 작업을 수행할 수 있습니다.

1. 다음 위치에서 JMX 콘솔로 이동합니다.
   `https://serveraddress:port/system/console/jmx`

1. 다음 MBean을 검색합니다.

   * Lucene 인덱스 통계
   * CopyOnRead 지원 통계
   * Oak 쿼리 통계
   * IndexStats

1. 각 MBeans를 클릭하여 성능 통계를 가져옵니다. 지원하려면 스크린샷을 만들거나 제출해야 하는 경우에 이를 기록해 둡니다.

다음 URL에서 이러한 통계의 JSON 변형을 가져올 수도 있습니다.

* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`

를 통해 통합 JMX 출력을 제공할 수도 있습니다 `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak.tidy.3.json`. 여기에는 JSON 형식으로 모든 Oak 관련 MBean 세부 사항이 포함됩니다.

#### 기타 세부 정보 {#other-details}

다음과 같이 문제를 해결하는 데 도움이 되도록 추가 세부 정보를 수집할 수 있습니다.

1. 인스턴스가 실행 중인 Oak 버전입니다. CRXDE를 열고 시작 페이지의 오른쪽 아래 모서리에서 버전을 확인하거나 버전을 선택하여 이 버전을 볼 수 있습니다 `org.apache.jackrabbit.oak-core` 번들입니다.
1. 문제 쿼리의 QueryBuilder 디버거 출력입니다. 디버거는 다음 위치에서 액세스할 수 있습니다. `https://serveraddress:port/libs/cq/search/content/querydebug.html`
