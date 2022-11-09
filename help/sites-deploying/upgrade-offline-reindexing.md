---
title: 오프라인 재색인화를 사용하여 업그레이드 중 다운타임 감소
description: AEM 업그레이드를 수행할 때 오프라인 재인덱싱 방법을 사용하여 시스템 다운타임을 줄이는 방법을 알아봅니다.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
feature: Upgrading
exl-id: 85bc041e-0ab1-42de-8bcc-c98a175d7494
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 오프라인 재색인화를 사용하여 업그레이드 중 다운타임 감소 {#offline-reindexing-to-reduce-downtime-during-upgrades}

## 소개 {#introduction}

Adobe Experience Manager 업그레이드의 주요 문제 중 하나는 즉석 업그레이드가 수행될 때 작성 환경과 연결된 다운타임입니다. 컨텐츠 작성자는 업그레이드 중에 환경에 액세스할 수 없습니다. 따라서 업그레이드를 수행하는 데 걸리는 시간을 최소화하는 것이 좋습니다. 대형 저장소, 특히 일반적으로 큰 데이터 스토어와 시간당 높은 수준의 자산 업로드가 있는 AEM Assets 프로젝트의 경우 Oak 인덱스의 재색인화는 업그레이드 시간의 상당한 비율이 필요합니다.

이 섹션에서는 Oak-run 도구를 사용하여 리포지토리를 다시 색인화하는 방법을 설명합니다 **이전** 업그레이드를 수행하므로 실제 업그레이드 중에 다운타임이 줄어듭니다. 제공된 단계는 [루센](https://jackrabbit.apache.org/oak/docs/query/lucene.html) AEM 6.4 이상의 버전에 대한 인덱스.

## 개요 {#overview}

AEM의 새 버전에서는 기능 세트가 확장되면 Oak 색인 정의에 변경 사항이 적용됩니다. Oak 인덱스를 변경하면 AEM 인스턴스를 업그레이드할 때 강제로 다시 색인화가 수행됩니다. 재색인화는 자산의 텍스트(예: pdf 파일의 텍스트)가 추출되고 색인화되므로 자산 배포에 비용이 많이 듭니다. MongoMK 리포지토리를 사용하면 데이터가 네트워크를 통해 유지되므로 재색인화하는 데 걸리는 시간이 더 늘어납니다.

업그레이드 과정에서 대부분의 고객이 직면하는 문제는 다운타임 기간을 줄이는 것입니다. 해결 방법은 다음과 같습니다 **건너뛰기** 업그레이드 중에 재인덱싱 활동. 이 작업은 새 indecs를 만들어 수행할 수 있습니다 **이전** 업그레이드를 수행하려면 업그레이드 중에 가져오기만 하면 됩니다.

## 접근 방법 {#approach}

![offline-reindexing-upgrade-text-extraction](assets/offline-reindexing-upgrade-process.png)

업그레이드 전에 를 사용하여 target AEM 버전의 색인 정의에 대해 인덱스를 만드는 것이 좋습니다. [Oak-run](/help/sites-deploying/indexing-via-the-oak-run-jar.md) 도구. 위의 다이어그램은 오프라인 재인덱싱 방법을 보여줍니다.

또한 방법에 설명된 단계 순서입니다.

1. 바이너리의 텍스트가 먼저 추출됩니다
2. Target 인덱스 정의가 만들어집니다
3. 오프라인 인덱스가 만들어집니다
4. 그런 다음 업그레이드 프로세스 중에 인덱스를 가져옵니다

### 텍스트 추출 {#text-extraction}

AEM에서 전체 색인을 활성화하기 위해 PDF과 같은 바이너리 파일의 텍스트가 추출되어 인덱스에 추가됩니다. 이는 일반적으로 색인 생성 프로세스에서 값비싼 단계입니다. 텍스트 추출은 많은 바이너리를 저장하므로 자산 리포지토리를 재색인화하는 데 특히 도움이 되는 최적화 단계입니다.

![offline-reindexing-upgrade-text-extraction](assets/offline-reindexing-upgrade-text-extraction.png)

tika 라이브러리와 함께 oak-run 도구를 사용하여 시스템에 저장된 바이너리의 텍스트를 추출할 수 있습니다. 업그레이드 전에 운영 시스템의 클론을 가져와 이 텍스트 추출 프로세스에 사용할 수 있습니다. 그런 다음 다음 다음 단계를 수행하여 텍스트 저장소를 만듭니다.

**1. 저장소를 트래버스하고 바이너리 세부 정보를 수집합니다**

이 단계에서는 경로 및 Blob ID가 포함된 이진 파일이 포함된 CSV 파일을 생성합니다.

인덱스를 만들 디렉토리에서 아래 명령을 실행합니다. 아래 예에서는 저장소 홈 디렉토리를 가정합니다.

```
java java -jar oak-run.jar tika <nodestore path> --fds-path <datastore path> --data-file text-extraction/oak-binary-stats.csv --generate
```

위치 `nodestore path` 은 `mongo_ur` 또는 `crx-quickstart/repository/segmentstore/`

를 사용하십시오 `--fake-ds-path=temp` 매개 변수 대신 `–fds-path` 작업 속도를 높이기 위해

**2. 기존 인덱스에서 사용할 수 있는 이진 텍스트 저장소를 다시 사용합니다**

기존 시스템에서 인덱스 데이터를 덤프하고 텍스트 저장소를 추출합니다.

다음 명령을 사용하여 기존 인덱스 데이터를 덤프할 수 있습니다.

```
java -jar oak-run.jar index <nodestore path> --fds-path=<datastore path> --index-dump
```

위치 `nodestore path` 은 `mongo_ur` 또는 `crx-quickstart/repository/segmentstore/`

그런 다음 위의 인덱스 덤프를 사용하여 스토어를 채웁니다.

```
java -jar oak-run.jar tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --index-dir ./indexing-result/index-dumps/<oak-index-name>/data populate
```

위치 `oak-index-name` 는 전체 텍스트 인덱스의 이름입니다(예: &quot;lucene&quot;).

**3. 위의 단계에서 누락된 바이너리에 대한 tika 라이브러리를 사용하여 텍스트 추출 프로세스를 실행합니다**

```
java -cp oak-run.jar:tika-app-1.21.jar org.apache.jackrabbit.oak.run.Main tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --fds-path <datastore path> extract
```

위치 `datastore path` 는 이진 데이터 저장소의 경로입니다.

생성된 텍스트 저장소는 나중에 다시 색인화하는 시나리오에 대해 업데이트 및 재사용할 수 있습니다.

텍스트 추출 프로세스에 대한 자세한 내용은 [Oak-run 설명서](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html).

### 오프라인 다시 인덱싱 {#offline-reindexing}

![offline-reindexing-upgrade-offline-reindexing](assets/offline-reindexing-upgrade-offline-reindexing.png)

업그레이드 전에 Lucene 인덱스를 오프라인으로 만듭니다. MongoMK를 사용하는 경우, 네트워크 오버헤드가 발생하지 않으므로 MongoMk 노드 중 하나에서 직접 실행하는 것이 좋습니다.

인덱스를 오프라인으로 만들려면 아래 단계를 수행하십시오.

**1. target AEM 버전에 대한 Oak Lucene 인덱스 정의를 생성합니다.**

기존 인덱스 정의를 덤프합니다. 대상 AEM 버전 및 oak-run의 Adobe Granite 저장소 번들을 사용하여 변경된 색인 정의를 생성했습니다.

인덱스 정의를 **소스** AEM 인스턴스에서 다음 명령을 실행합니다.

>[!NOTE]
>
>덤핑 인덱스 정의에 대한 자세한 내용은 [Oak 설명서](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#async-index-data).

```
java -jar oak-run.jar index --fds-path <datastore path> <nodestore path> --index-definitions
```

위치 `datastore path` 및 `nodestore path` 다음에서 **소스** AEM 인스턴스.

그런 다음 **target** target 버전의 Granite 저장소 번들을 사용하는 AEM 버전입니다.

```
java -cp oak-run.jar:bundle-com.adobe.granite.repository.jar org.apache.jackrabbit.oak.index.IndexDefinitionUpdater --in indexing-definitions_source.json --out merge-index-definitions_target.json --initializer com.adobe.granite.repository.impl.GraniteContent
```

>[!NOTE]
>
>위의 인덱스 정의 작성 프로세스는 `oak-run-1.12.0` 버전 섹션을 참조하십시오. Granite 저장소 번들을 사용하여 타깃팅이 수행됩니다 `com.adobe.granite.repository-x.x.xx.jar`.

위의 단계에서 라는 JSON 파일을 만듭니다. `merge-index-definitions_target.json` 인덱스 정의입니다.

**2. 저장소에서 체크포인트 만들기**

프로덕션에서 체크포인트 만들기 **소스** 라이프타임이 긴 AEM 인스턴스. 이 작업은 리포지토리를 복제하기 전에 수행해야 합니다.

에 있는 JMX 콘솔을 통해 `http://serveraddress:serverport/system/console/jmx`, 이동 `CheckpointMBean` 그리고 충분히 긴 수명(예: 200일)을 가진 체크포인트를 만듭니다. 이렇게 하려면 `CheckpointMBean#createCheckpoint` with `17280000000` 을 밀리초 단위의 라이프타임 기간에 대한 인수입니다.

이렇게 하면 새로 만든 체크포인트 ID를 복사하고 JMX를 사용하여 라이프타임의 유효성을 확인합니다 `CheckpointMBean#listCheckpoints`.

>[!NOTE]
>
>이 체크포인트는 인덱스를 나중에 가져올 때 삭제됩니다.

자세한 내용은 [체크포인트 생성](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#out-of-band-create-checkpoint) Oak 설명서에서 링크를 클릭하십시오.

**생성된 인덱스 정의에 대해 오프라인 색인을 수행합니다**

Lucene 재색인화는 oak-run을 사용하여 오프라인으로 수행할 수 있습니다. 이 프로세스는 다음 디스크의 인덱스 데이터를 만듭니다 `indexing-result/indexes`. 그렇습니다 **not** 저장소에 쓰기 때문에 실행 중인 AEM 인스턴스를 중지할 필요가 없습니다. 생성된 텍스트 저장소를 이 프로세스에 가져옵니다.

```
java -Doak.indexer.memLimitInMB=500 -jar oak-run.jar index <nodestore path> --reindex --doc-traversal-mode --checkpoint <checkpoint> --fds-path <datastore path> --index-definitions-file merge-index-definitions_target.json --pre-extracted-text-dir text-extraction/store

Sample <checkpoint> looks like r16c85700008-0-8
—fds-path: path to data store.
--pre-extracted-text-dir: Directory of pre-extracted text.
merge-index-definitions_target: JSON file having merged definitions for the target AEM instance. indexes in this file will be re-indexed.
```

사용 `--doc-traversal-mode` 매개 변수는 저장소 컨텐츠를 로컬 플랫 파일로 스풀링하여 재인덱스 시간을 크게 향상하므로 MongoMK 설치에 유용합니다. 그러나 저장소 크기의 두 배의 추가 디스크 공간이 필요합니다.

MongoMK의 경우, 이 단계가 MongoDB 인스턴스에 가까운 인스턴스에서 실행되는 경우 이 프로세스를 가속화할 수 있습니다. 동일한 컴퓨터에서 실행되는 경우 네트워크 오버헤드를 방지할 수 있습니다.

자세한 기술 정보는 [색인화를 위한 oak-run 설명서](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html).

### 인덱스 가져오기 {#importing-indexes}

AEM 6.4 이상 버전을 사용하는 AEM에는 시작 시퀀스에서 디스크에서 인덱스를 가져오는 기능이 내장되어 있습니다. 폴더 `<repository>/indexing-result/indexes` 는 시작하는 동안 인덱스 데이터가 있는지 관찰합니다. 미리 만들어진 인덱스를 [업그레이드 프로세스](in-place-upgrade.md#performing-the-upgrade) 의 새 버전으로 시작하기 전에 **target** AEM jar. AEM은 이를 저장소로 가져오고 시스템에서 해당 체크포인트를 제거합니다. 따라서 재색인은 완전히 피된다.

## 추가 팁 및 문제 해결 {#troubleshooting}

다음은 몇 가지 유용한 팁과 문제 해결 지침입니다.

### 라이브 프로덕션 시스템에 미치는 영향 감소 {#reduce-the-impact-on-the-live-production-system}

운영 시스템을 복제하고 클론을 사용하여 오프라인 인덱스를 생성하는 것이 좋습니다. 따라서 운영 시스템에 미치는 잠재적 영향을 모두 제거합니다. 그러나 인덱스를 가져오는 데 필요한 체크포인트가 프로덕션 시스템에 있어야 합니다. 따라서 클론을 생성하기 전에 체크포인트를 생성하는 것이 중요합니다.

### Runbook 및 평가판 실행 준비 {#prepare-a-runbook-and-trial-run}

을 준비하는 것이 좋습니다 [runbook](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/upgrade-planning.html#building-the-upgrade-and-rollback-runbook) 프로덕션 환경에서 업그레이드를 실행하기 전에 몇 가지 테스트를 수행합니다.

### 오프라인 색인화가 있는 문서 순회 모드 {#doc-traversal-mode-with-offline-indexing}

오프라인 색인화를 사용하려면 전체 리포지토리의 여러 순번이 필요합니다. MongoMK 설치를 통해 저장소에는 인덱싱 프로세스의 성능에 영향을 주는 네트워크를 통해 액세스할 수 있습니다. 한 가지 옵션은 MongoDB 복제본 자체에서 오프라인 인덱싱 프로세스를 실행하여 네트워크 오버헤드를 제거하는 것입니다. 또 다른 옵션은 문서 순회 모드 사용입니다.

명령줄 매개 변수를 추가하여 문서 순회 모드를 적용할 수 있습니다 `—doc-traversal` 오프라인 색인화를 위해 oak-run 명령을 실행합니다. 이 모드에서는 로컬 디스크에 있는 전체 리포지토리의 복사본을 플랫 파일로 저장하고 이를 사용하여 색인을 실행합니다.
