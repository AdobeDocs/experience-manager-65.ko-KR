---
title: Oak-run.jar 색인화 사용 사례
description: Oak-run 도구를 사용하여 색인화를 수행하는 다양한 사용자 사례에 대해 알아봅니다.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
noindex: true
exl-id: d25e3070-080a-4594-8fdb-9f09164135fc
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1380'
ht-degree: 0%

---

# Oak-run.jar 색인화 사용 사례{#oak-run-jar-indexing-use-cases}

Oak-run은 AEM JMX 콘솔을 통해 이러한 사용 사례의 실행을 오케스트레이션하지 않고도 명령줄에서 인덱싱 사용 사례를 지원합니다.

oak 색인 관리에 oak-run.jar index 명령 접근 방식을 사용하면 다음과 같은 중요한 이점이 있습니다.

1. Oak-run index 명령은 AEM 6.4에 대한 새로운 인덱싱 도구 세트를 제공합니다.
1. Oak-run은 색인 재지정 시간을 줄여 더 큰 저장소에서 색인 재지정 시간을 줄입니다.
1. Oak-run은 AEM에서 리인덱싱하는 동안 리소스 소비를 줄여 전반적인 시스템 성능을 향상시킵니다.
1. Oak-run은 대역 외 리인덱싱을 제공하여 프로덕션을 사용할 수 있어야 하는 상황을 지원하고, 리인덱싱하는 데 필요한 유지 관리 또는 다운타임을 허용할 수 없습니다.

아래 섹션에서는 샘플 명령을 제공합니다. Oak-run index 명령은 모든 NodeStore 및 BlobStore 설정을 지원합니다. 아래에 제공된 예제는 FileDataStore 및 SegmentNodeStore가 있는 설정에 관한 것입니다.

## 사용 사례 1 - 색인 일관성 검사 {#usercase1indexconsistencycheck}

이는 색인 손상과 관련된 사용 사례입니다. 어떤 색인이 손상되었는지 확인할 수 없는 경우가 있었습니다. 따라서 Adobe은 다음과 같은 도구를 제공합니다.

1. 모든 인덱스에 대해 인덱스 일관성 검사를 수행하고, 유효한 인덱스와 유효하지 않은 인덱스를 보고합니다.
1. 이 도구는 AEM에 액세스할 수 없는 경우에도 사용할 수 있습니다.
1. 사용하기 쉽습니다.

손상된 인덱스 확인은 다음을 통해 수행할 수 있습니다. `--index-consistency-check` 작업:

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-consistency-check
```

다음에서 보고서를 생성합니다. `indexing-result/index-consistency-check-report.txt`. 샘플 보고서는 아래를 참조하십시오.

```
Valid indexes :
        - /content/oak:index/enablementResourceName
        - /oak:index/cqProjectLucene
        - /oak:index/cqTagLucene
        - /oak:index/lucene
        - /oak:index/ntBaseLucene
        - /oak:index/socialLucene
    Invalid indexes :
        - /oak:index/atDamIndex
        - /oak:index/atIndex
        - /oak:index/cqPageLucene
        - /oak:index/damAssetLucene
        - /oak:index/groups
        - /oak:index/slingeventJob
        - /oak:index/users
        - /oak:index/workflowDataLucene
    Ignored indexes as these are not of type lucene:
        - /oak:index/acPrincipalName
        - /oak:index/active
```

### 이점 {#uc1benefits}

이제 지원 센터 및 시스템 관리자가 이 도구를 사용하여 손상된 색인을 신속하게 확인한 다음 다시 색인화할 수 있습니다.

## 사용 사례 2 - 색인 통계 {#usecase2indexstatistics}

쿼리 성능 Adobe과 관련된 일부 사례를 진단하기 위해 종종 기존 색인 정의, 고객 설정의 색인 관련 통계가 필요합니다. 지금까지 이 정보는 여러 자원에 분산되어 있었습니다. 보다 쉽게 문제를 해결할 수 있도록 Adobe은 다음과 같은 도구를 만들었습니다.

1. 시스템에 있는 모든 인덱스 정의를 단일 JSON 파일로 덤프합니다.

1. 기존 인덱스에서 중요한 통계를 덤프합니다.

1. 오프라인 분석을 위한 색인 콘텐츠 덤프

1. AEM에 액세스할 수 없는 경우에도 사용 가능

이제 다음 작업 인덱스 명령을 사용하여 위의 작업을 수행할 수 있습니다.

* `--index-info` - 인덱스와 관련된 다양한 통계를 수집하고 덤프합니다.

* `--index-definitions` - 색인 정의를 수집하고 덤프합니다.

* `--index-dump` - 색인 콘텐츠 덤프

실제로 명령이 작동하는 방식에 대한 예는 아래를 참조하십시오.

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-info --index-definitions --index-dump
```

보고서는에서 생성됩니다. `indexing-result/index-info.txt` 및 `indexing-result/index-definitions.json`

또한 웹 콘솔을 통해 동일한 세부 정보가 제공되며 구성 덤프 zip의 일부가 됩니다. 다음 위치에서 액세스할 수 있습니다.

`https://serverhost:serverport/system/console/status-oak-index-defn`

### 이점 {#uc2benefits}

이 도구를 사용하면 인덱싱 또는 쿼리 문제와 관련된 모든 필수 세부 정보를 빠르게 수집할 수 있으며 이 정보를 추출하는 데 소요되는 시간을 줄일 수 있습니다.

## 사용 사례 3 - 리인덱싱 {#usecase3reindexing}

에 따라 [시나리오](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing), 경우에 따라 리인덱싱을 수행해야 합니다. 현재, 리인덱싱은 `reindex` 플래그 지정 대상 `true` CRXDE 또는 Index Manager 사용자 인터페이스를 통해 색인 정의 노드 플래그가 설정되면 리인덱싱이 비동기적으로 수행됩니다.

리인덱싱과 관련하여 몇 가지 주의할 사항:

* 리인덱싱이 훨씬 느립니다. `DocumentNodeStore` 과 비교한 설정 `SegmentNodeStore` 모든 컨텐츠가 로컬인 설정

* 현재 디자인에서는 리인덱싱이 발생하는 동안 비동기 인덱서가 차단되고 다른 모든 비동기 인덱스가 부실해지며 인덱싱 중에 업데이트되지 않습니다. 이러한 이유로 시스템이 사용 중이면 사용자에게 최신 결과가 표시되지 않을 수 있습니다.
* 리인덱싱에는 AEM 설정에 높은 부하를 줄 수 있으므로 최종 사용자 경험에 영향을 줄 수 있는 전체 저장소 순회가 포함됩니다.
* 의 경우 `DocumentNodeStore` 리인덱싱하는 데 상당한 시간이 소요될 수 있는 설치 작업 중에 Mongo 데이터베이스 연결에 실패하면 인덱싱을 처음부터 다시 시작해야 합니다.

* 경우에 따라 텍스트 추출로 인해 리인덱싱하는 데 시간이 오래 걸릴 수 있습니다. 이는 텍스트 추출에 소요된 시간이 인덱싱 시간에 영향을 줄 수 있는 PDF 파일이 많은 설정에 적용됩니다.

이러한 목표를 달성하기 위해 oak-run 인덱스 툴은 필요에 따라 사용할 수 있는 다양한 리인덱싱 모드를 지원합니다. oak-run index 명령은 다음과 같은 이점을 제공합니다.

* **대역 외 리인덱싱** - oak-run 리인덱싱은 실행 중인 AEM 설정과 별도로 수행할 수 있으므로 사용 중인 AEM 인스턴스에 미치는 영향을 최소화합니다.

* **경로 외 리인덱싱** - 리인덱싱은 인덱싱 작업에 영향을 주지 않고 수행됩니다. 즉, 비동기 인덱서가 계속해서 다른 인덱스를 인덱싱할 수 있습니다.

* **DocumentNodeStore 설치에 대한 간소화된 색인 재지정** - 대상 `DocumentNodeStore` 설치, 리인덱싱은 리인덱싱이 가장 최적의 방식으로 이루어지도록 하는 단일 명령으로 수행할 수 있습니다.

* **색인 정의 업데이트 및 새로운 색인 정의 도입을 지원합니다.**

### 색인 재지정 - DocumentNodeStore {#reindexdocumentnodestore}

대상 `DocumentNodeStore` 설치 리인덱싱은 단일 oak-run 명령을 통해 수행할 수 있습니다.

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore mongodb://server:port/aem
```

이를 통해 다음과 같은 이점이 있습니다

* 실행 중인 AEM 인스턴스에 미치는 영향을 최소화합니다. 대부분의 읽기는 보조 서버에서 수행할 수 있으며 실행 중인 AEM 캐시는 리인덱싱에 필요한 모든 순회로 인해 부정적인 영향을 받지 않습니다.
* 사용자는 를 통해 새 인덱스 또는 업데이트된 인덱스의 JSON을 제공할 수도 있습니다. `--index-definitions-file` 옵션을 선택합니다.

### 색인 재지정 - SegmentNodeStore {#reindexsegmentnodestore}

대상 `SegmentNodeStore` 설치 리인덱싱은 다음 방법 중 하나로 수행할 수 있습니다.

#### 온라인 색인 재지정 - SegmentNodeStore {#onlinereindexsegmentnodestore}

재색인화가 설정의 방식으로 수행되는 기존 방법을 따르십시오. `reindex` 플래그.

#### 온라인 색인 재지정 - SegmentNodeStore - AEM 인스턴스가 실행 중입니다. {#onlinereindexsegmentnodestoretheaeminstanceisrunning}

대상 `SegmentNodeStore` 설치에서는 하나의 프로세스만 읽기/쓰기 모드에서 세그먼트 파일에 액세스할 수 있습니다. 이로 인해 oak-run 인덱싱의 일부 작업에는 추가 수동 단계를 수행해야 합니다.

여기에는 다음과 같은 항목이 포함됩니다.

1. 단계 텍스트
1. 연결 `oak-run` 읽기 전용 모드로 AEM에서 사용하는 동일한 리포지토리에 액세스하고 인덱싱을 수행합니다. 이를 수행하는 방법의 예:

   ```shell
   java -jar oak-run-1.7.6.jar index --fds-path=/Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/datastore/ --checkpoint 26b7da38-a699-45b2-82fb-73aa2f9af0e2 --reindex --index-paths=/oak:index/lucene /Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/segmentstore/
   ```

1. 마지막으로, 를 사용하여 생성된 인덱스 파일을 가져옵니다. `IndexerMBean#importIndex` 위의 명령을 실행한 후 oak-run이 색인 파일을 저장한 경로의 작업입니다.

이 시나리오에서는 AEM 서버를 중지하거나 새 인스턴스를 프로비저닝할 필요가 없습니다. 그러나 인덱싱에는 전체 저장소 순회가 포함되므로 설치 시 I/O 로드가 증가하여 런타임 성능에 부정적인 영향을 줍니다.

#### 온라인 색인 재지정 - SegmentNodeStore - AEM 인스턴스가 종료됨 {#onlinereindexsegmentnodestoreaeminstanceisdown}

대상 `SegmentNodeStore` 설치, 리인덱싱은 단일 oak-run 명령을 통해 수행할 수 있습니다. 단, AEM 인스턴스를 종료해야 합니다.

다음 명령을 사용하여 리인덱싱을 트리거할 수 있습니다.

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore  /path/to/segmentstore/
```

이 접근 방식과 위에서 설명한 접근 방식의 차이점은 체크포인트 생성과 인덱스 가져오기가 자동으로 수행된다는 것입니다. 단점은 이 과정에서 AEM이 다운돼야 한다는 점이다.

#### 대역 외 리인덱스 - SegmentNodeStore {#outofbandreindexsegmentnodestore}

이 사용 사례에서는 복제된 설정에서 리인덱싱을 수행하여 실행 중인 AEM 인스턴스에 미치는 영향을 최소화할 수 있습니다.

1. JMX 작업을 통해 체크포인트를 만듭니다. 다음 위치로 이동하여 이 작업을 수행할 수 있습니다. [JMX 콘솔](/help/sites-administering/jmx-console.md) 및 검색 `CheckpointManager`. 그런 다음 **createCheckpoint(long p1)** 초 단위의 만료에 높은 값을 사용하는 작업(예: **2592000**).
1. 다음을 복사합니다. `crx-quickstart` 새 컴퓨터에 폴더 추가
1. oak-run index 명령을 사용하여 색인 재지정 수행

1. 생성된 인덱스 파일을 AEM 서버에 복사

1. JMX를 통해 인덱스 파일을 가져옵니다.

이 사용 사례에서는 다음과 같은 경우에는 불가능한 다른 인스턴스에서 데이터 저장소에 액세스할 수 있다고 가정합니다. `FileDataStore` 는 EBS와 같은 클라우드 기반 스토리지 솔루션에 배치됩니다. 다음의 시나리오는 제외됩니다. `FileDataStore` 또한 복제됩니다. 인덱스 정의가 전체 텍스트 색인화를 수행하지 않으면 다음에 액세스합니다. `DataStore` 은 필수가 아닙니다.

## 사용 사례 4 - 색인 정의 업데이트 {#usecase4updatingindexdefinitions}

현재 다음을 통해 색인 정의 변경 사항을 전달할 수 있습니다. [ACS 인덱스 확인](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) 패키지. 이렇게 하면 콘텐츠 패키지를 통해 색인 정의를 전달할 수 있으며 나중에 색인 재지정을 설정하여 수행해야 합니다. `reindex` 플래그 지정 대상 `true`.

이 기능은 리인덱싱하는 데 시간이 오래 걸리지 않는 소규모 설치에 적합합니다. 그러나 큰 저장소의 경우 리인덱싱은 훨씬 더 많은 시간 내에 수행됩니다. 이러한 경우 이제 oak-run 인덱스 도구를 사용할 수 있습니다.

Oak-run은 이제 JSON 형식으로 색인 정의를 제공하고 라이브 인스턴스에서 변경 사항이 수행되지 않는 대역 외 모드에서 색인 생성을 지원합니다.

이 사용 사례에서 고려해야 할 프로세스는 다음과 같습니다.

1. 개발자는 로컬 인스턴스에서 색인 정의를 업데이트한 다음 를 통해 색인 정의 JSON 파일을 생성합니다. `--index-definitions` 옵션

1. 그런 다음 업데이트된 JSON이 시스템 관리자에게 제공됩니다
1. 시스템 관리자는 대역외 접근 방식을 따르고 다른 설치에서 인덱스를 준비합니다
1. 이 작업이 완료되면 생성된 인덱스 파일을 실행 중인 AEM 설치 시 가져옵니다.
