---
title: Oak-run.jar 인덱싱 사용 사례
seo-title: Oak-run.jar 인덱싱 사용 사례
description: Oak-run 도구를 사용하여 색인 작업을 수행하기 위한 다양한 사용자 사례에 대해 알아봅니다.
seo-description: Oak-run 도구를 사용하여 색인 작업을 수행하기 위한 다양한 사용자 사례에 대해 알아봅니다.
uuid: 3c50080d-1e0d-4886-8d37-269f06881eb4
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 084075b8-826d-4f27-9342-35f33368f24f
noindex: true
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1392'
ht-degree: 0%

---


# Oak-run.jar 인덱싱 사용 사례{#oak-run-jar-indexing-use-cases}

Oak-run은 AEM JMX 콘솔을 통해 이러한 사용 사례 실행을 오케스트레이션하지 않고도 명령줄에서 인덱싱 사용 사례를 지원합니다.

Oak 인덱스 관리를 위해 oak-run.jar index 명령 접근 방식을 사용하면 다음과 같은 이점을 얻을 수 있습니다.

1. Oak-run index 명령은 AEM 6.4용 새로운 인덱싱 도구 세트를 제공합니다.
1. Oak-run은 더 큰 저장소에서 색인 재지정 시간을 단축시켜 줍니다.
1. Oak-run은 AEM에서 다시 인덱싱하는 동안 리소스 사용량을 줄여 전반적인 시스템 성능을 향상시킵니다.
1. Oak-run은 대역외 재색인 기능을 제공하고 프로덕션을 사용할 수 있어야 하며 재색인에 필요한 유지 관리 또는 다운타임을 허용할 수 없는 상황을 지원합니다.

아래 섹션은 샘플 명령을 제공합니다. oak-run index 명령은 모든 NodeStore 및 BlobStore 설정을 지원합니다. 아래에 제공된 예는 FileDataStore 및 SegmentNodeStore가 있는 설정에 대해 설명합니다.

## 사용 사례 1 - 색인 일관성 검사 {#usercase1indexconsistencycheck}

색인 부패와 관련된 사용 사례입니다. 어떤 색인이 손상되었는지를 확인할 수 없는 경우도 있었다. 따라서 Adobe은 다음과 같은 도구를 제공했습니다.

1. 모든 색인에 대해 색인 일관성 검사를 수행하고 인덱스가 유효하고 유효하지 않은 보고서를 제공합니다.
1. AEM에 액세스할 수 없는 경우에도 도구를 사용할 수 있습니다.
1. 사용하기 쉽습니다.

손상된 인덱스는 `--index-consistency-check` 작업을 통해 확인할 수 있습니다.

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-consistency-check
```

이렇게 하면 `indexing-result/index-consistency-check-report.txt`에 보고서가 생성됩니다. 샘플 보고서는 아래를 참조하십시오.

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

### 혜택 {#uc1benefits}

지원 및 시스템 관리자가 이 도구를 사용하여 어떤 색인이 손상되었는지를 신속하게 확인하고 다시 색인화할 수 있습니다.

## 사용 사례 2 - 색인 통계 {#usecase2indexstatistics}

쿼리 성능 Adobe에 대한 일부 사례를 진단하려면 종종 기존 색인 정의가 필요하므로 고객 설정에서 색인 관련 통계가 필요합니다. 지금까지 이 정보는 여러 자원에 걸쳐 분산되었다. 문제 해결을 보다 쉽게 하기 위해 Adobe은 다음과 같은 도구를 만들었습니다.

1. 시스템에 있는 모든 인덱스 정의를 단일 JSON 파일로 덤프;

1. 기존 인덱스에서 중요한 통계 덤프

1. 오프라인 분석을 위해 색인 내용 덤프;

1. AEM에 액세스할 수 없는 경우에도 사용할 수 있습니다.

이제 다음 작업 인덱스 명령을 통해 위의 작업을 수행할 수 있습니다.

* `--index-info` - 색인과 관련된 다양한 통계 수집 및 덤프

* `--index-definitions` - 색인 정의 수집 및 덤프

* `--index-dump` - 색인 컨텐츠 덤프

명령이 실제로 작동하는 방법의 예는 아래를 참조하십시오.

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-info --index-definitions --index-dump
```

보고서는 `indexing-result/index-info.txt` 및 `indexing-result/index-definitions.json`에서 생성됩니다.

또한 웹 콘솔을 통해 동일한 세부 정보가 제공되며 구성 덤프 zip의 일부가 됩니다. 다음 위치에서 액세스할 수 있습니다.

`https://serverhost:serverport/system/console/status-oak-index-defn`

### 혜택 {#uc2benefits}

이 툴을 사용하면 색인 작성 또는 쿼리 문제와 관련된 모든 필수 세부 사항을 신속하게 수집할 수 있으며 이 정보를 추출하는 데 소요되는 시간을 줄일 수 있습니다.

## 사용 사례 3 - {#usecase3reindexing} 다시 색인화

[scenarios](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing)에 따라 일부 경우에는 다시 색인화해야 합니다. 현재 색인 재지정 작업은 CRXDE를 통해 또는 Index Manager 사용자 인터페이스를 통해 색인 정의 노드에서 `reindex` 플래그를 `true`로 설정하여 수행됩니다. 플래그가 설정되면 다시 색인화가 비동기적으로 수행됩니다.

다시 색인화에 대해 주목할 점이 있습니다.

* 모든 컨텐츠가 로컬인 `SegmentNodeStore` 설정과 비교하여 `DocumentNodeStore` 설정에서 색인 재지정 속도가 훨씬 느립니다.

* 현재 디자인을 사용하는 동안 다시 인덱싱하면 비동기 인덱서가 차단되고 다른 모든 비동기 인덱스가 부실 상태가 되며 색인 기간 동안 업데이트를 받지 않습니다. 이로 인해 시스템이 사용 중인 경우 사용자에게 최신 결과가 표시되지 않을 수 있습니다.
* 색인 재지정 작업에는 AEM 설정에 높은 부하를 적용하고 최종 사용자 경험에 영향을 줄 수 있는 전체 저장소 트래픽이 포함됩니다.
* 다시 인덱싱하는 데 상당한 시간이 걸릴 수 있는 `DocumentNodeStore` 설치의 경우 작업 중에 Mongo 데이터베이스에 대한 연결이 실패할 경우 인덱싱을 처음부터 다시 시작해야 합니다.

* 텍스트 추출 때문에 색인 재지정 작업이 오래 걸릴 수 있습니다. 이 기능은 주로 많은 PDF 파일이 있는 설정에 주로 사용되며 텍스트 추출에 소요되는 시간이 인덱싱 시간에 영향을 줄 수 있습니다.

이러한 목표를 충족하기 위해 오크 실행 색인 툴은 필요에 따라 재색인화를 위한 다양한 모드를 지원합니다. oak-run index 명령은 다음과 같은 이점을 제공합니다.

* **대역외 재인덱싱**  - oak-run 재색인은 실행 중인 AEM 설정과 별도로 수행할 수 있으므로 사용 중인 AEM 인스턴스에 미치는 영향을 최소화합니다.

* **즉시 색인 재지정**  - 색인 작업에 영향을 주지 않고 재색인이 수행됩니다. 이것은 비동기 인덱서가 계속해서 다른 인덱스를 인덱싱할 수 있음을 의미합니다.

* **DocumentNodeStore 설치에 대한 간소화된 재색인**  -  `DocumentNodeStore` 설치의 경우 단일 명령으로 다시 색인화를 수행할 수 있으므로 최적의 방식으로 다시 색인화할 수 있습니다.

* **색인 정의 업데이트 및 새로운 색인 정의 소개 지원**

### 다시 색인 - DocumentNodeStore {#reindexdocumentnodestore}

`DocumentNodeStore` 설치 재인덱스는 단일 oak-run 명령을 통해 수행할 수 있습니다.

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore mongodb://server:port/aem
```

다음과 같은 이점이 있습니다

* AEM 인스턴스 실행에 미치는 영향을 최소화합니다. 대부분의 읽기는 보조 서버에서 수행할 수 있으며 AEM 캐시 실행은 다시 인덱싱하는 데 필요한 모든 트래픽으로 인해 겹치는 영향을 받지 않습니다.
* 또한 사용자는 `--index-definitions-file` 옵션을 통해 새 색인 또는 업데이트된 색인의 JSON을 제공할 수 있습니다.

### 다시 색인 - SegmentNodeStore {#reindexsegmentnodestore}

`SegmentNodeStore` 설치 재색인화는 다음 방법 중 하나로 수행할 수 있습니다.

#### 온라인 다시 색인 - SegmentNodeStore {#onlinereindexsegmentnodestore}

`reindex` 플래그 설정을 통해 색인 재설정이 수행되는 기존 방법을 따릅니다.

#### 온라인 다시 인덱스 - SegmentNodeStore - AEM 인스턴스가 {#onlinereindexsegmentnodestoretheaeminstanceisrunning}을(를) 실행 중입니다.

`SegmentNodeStore` 설치의 경우 한 프로세스만 읽기-쓰기 모드에서 세그먼트 파일에 액세스할 수 있습니다. 이러한 참화 실행 인덱스에서 일부 작업을 수행하려면 추가적인 수동 단계가 필요합니다.

여기에는 다음이 포함됩니다.

1. 단계 텍스트
1. `oak-run`을(를) 읽기 전용 모드에서 AEM에서 사용하는 동일한 저장소에 연결하고 색인을 수행합니다. 이를 실현하는 방법에 대한 예:

   ```shell
   java -jar oak-run-1.7.6.jar index --fds-path=/Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/datastore/ --checkpoint 26b7da38-a699-45b2-82fb-73aa2f9af0e2 --reindex --index-paths=/oak:index/lucene /Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/segmentstore/
   ```

1. 마지막으로, 상기 명령을 실행한 후 Oak-run이 색인 파일을 저장한 경로에서 `IndexerMBean#importIndex` 작업을 통해 생성된 인덱스 파일을 가져옵니다.

이 시나리오에서는 AEM 서버를 중지하거나 새 인스턴스를 프로비저닝할 필요가 없습니다. 하지만 색인화에는 전체 저장소의 트래픽이 포함되므로 설치 시 I/O 로드가 증가하여 런타임 성능에 부정적인 영향을 줍니다.

#### 온라인 다시 인덱스 - SegmentNodeStore - AEM 인스턴스가 {#onlinereindexsegmentnodestoreaeminstanceisdown} 종료됩니다.

`SegmentNodeStore` 설치 재인덱스는 단일 oak-run 명령을 통해 수행할 수 있습니다. 하지만 AEM 인스턴스를 종료해야 합니다.

다음 명령을 사용하여 다시 색인화를 트리거할 수 있습니다.

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore  /path/to/segmentstore/
```

이 방법과 위에 설명한 방법 간의 차이는 체크포인트 생성과 색인 가져오기가 자동으로 수행된다는 점입니다. 단점은 AEM이 그 과정 동안 다운되어야 한다는 것이다.

#### 대역 외 재색인 - SegmentNodeStore {#outofbandreindexsegmentnodestore}

이 경우 복제된 설정에 대해 다시 색인화를 수행하여 실행 중인 AEM 인스턴스에 미치는 영향을 최소화할 수 있습니다.

1. JMX 작업을 통해 체크포인트를 만듭니다. 이 작업은 [JMX 콘솔](/help/sites-administering/jmx-console.md)으로 이동하여 `CheckpointManager`를 검색하여 수행할 수 있습니다. 그런 다음 만료에 높은 값을 사용하여 **createCheckpoint(long p1)** 작업을 초 단위로 클릭합니다(예: **2592000**).
1. `crx-quickstart` 폴더를 새 컴퓨터에 복사
1. oak-run index 명령을 통해 다시 색인 수행

1. 생성된 인덱스 파일을 AEM 서버로 복사

1. JMX를 통해 인덱스 파일을 가져옵니다.

이 사용 사례에서는 `FileDataStore`이(가) EBS와 같은 클라우드 기반 스토리지 솔루션에 배치된 경우 가능하지 않은 다른 인스턴스에서 데이터 저장소에 액세스할 수 있다고 가정합니다. 여기에는 `FileDataStore`이(가) 복제되는 시나리오가 제외됩니다. 인덱스 정의가 전체 텍스트 인덱싱을 수행하지 않으면 `DataStore`에 액세스할 필요가 없습니다.

## 사용 사례 4 - 색인 정의 업데이트 {#usecase4updatingindexdefinitions}

현재, [ACS 인덱스 확인](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) 패키지를 통해 색인 정의 변경 사항을 전달할 수 있습니다. 이를 통해 나중에 `reindex` 플래그를 `true`로 설정하여 다시 색인화해야 하는 콘텐츠 패키지를 통해 색인 정의를 전달할 수 있습니다.

이렇게 하면 다시 색인화하는 데 시간이 오래 걸리지 않는 작은 설치에서도 잘 작동합니다. 그러나 매우 큰 리포지토리의 경우 재색인 작업은 상당히 많은 시간 내에 수행됩니다. 이러한 경우 참나무 실행 색인 도구를 사용할 수 있습니다.

Oak-run은 이제 JSON 형식으로 색인 정의 제공 및 라이브 인스턴스에서 변경 사항이 수행되지 않는 대역 외 모드에서 인덱스 생성을 지원합니다.

이 사용 사례를 고려해야 하는 프로세스는 다음과 같습니다.

1. 개발자는 로컬 인스턴스의 인덱스 정의를 업데이트한 다음 `--index-definitions` 옵션을 통해 색인 정의 JSON 파일을 생성합니다

1. 업데이트된 JSON은 시스템 관리자에게 제공됩니다
1. 시스템 관리자는 대역 외 접근 방식을 따르고 다른 설치 시 색인을 준비합니다
1. 이 작업이 완료되면 생성된 인덱스 파일을 실행 중인 AEM 설치 시 가져옵니다.

