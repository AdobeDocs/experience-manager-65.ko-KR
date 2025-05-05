---
title: 업그레이드 중 다운타임을 줄이기 위해 오프라인 리인덱싱을 사용
description: AEM 업그레이드를 수행할 때 오프라인 리인덱싱 방식을 사용하여 시스템 다운타임을 줄이는 방법을 알아봅니다.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
feature: Upgrading
exl-id: 85bc041e-0ab1-42de-8bcc-c98a175d7494
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1306'
ht-degree: 0%

---

# 업그레이드 중 다운타임을 줄이기 위해 오프라인 리인덱싱을 사용 {#offline-reindexing-to-reduce-downtime-during-upgrades}

## 소개 {#introduction}

Adobe Experience Manager 업그레이드의 주요 문제 중 하나는 바로 내 업그레이드를 수행할 때 작성 환경과 관련된 다운타임입니다. 업그레이드 중에는 콘텐츠 작성자가 환경에 액세스할 수 없습니다. 따라서 업그레이드를 수행하는 데 소요되는 시간을 최소화하는 것이 바람직합니다. 대형 저장소, 특히 일반적으로 데이터 저장소가 많고 시간당 높은 수준의 에셋 업로드가 있는 AEM Assets 프로젝트의 경우 Oak 색인을 다시 색인화하는 데 업그레이드 시간의 상당 부분이 소요됩니다.

이 섹션에서는 Oak 실행 도구를 사용하여 업그레이드를 수행하기 전에 **먼저** 리포지토리를 다시 인덱싱함으로써 실제 업그레이드 중 다운타임을 줄이는 방법에 대해 설명합니다. 제공된 단계는 AEM 6.4 이상 버전의 [Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html) 인덱스에 적용할 수 있습니다.

## 개요 {#overview}

AEM의 새 버전에서는 기능 세트가 확장될 때 Oak 색인 정의가 변경됩니다. Oak 색인을 변경하면 AEM 인스턴스를 업그레이드할 때 강제로 다시 색인화됩니다. 리인덱싱은 에셋의 텍스트(예: pdf 파일의 텍스트)가 추출되고 인덱싱되므로 에셋 배포에 많은 비용이 소요됩니다. MongoMK 저장소를 사용하면 데이터가 네트워크를 통해 유지되므로 리인덱싱에 걸리는 시간이 더욱 늘어납니다.

업그레이드 중 대부분의 고객이 직면한 문제는 가동 중지 시간 창을 줄이는 것입니다. 해결 방법은 업그레이드 중에 리인덱싱 활동을 **건너뛰기**&#x200B;하는 것입니다. 업그레이드를 수행할 새 인데임 **이전**&#x200B;을(를) 만든 다음 업그레이드하는 동안 가져오기만 하면 됩니다.

## 접근 방식 {#approach}

![오프라인 리인덱싱 업그레이드 텍스트 추출](assets/offline-reindexing-upgrade-process.png)

업그레이드 전에 [Oak-run](/help/sites-deploying/indexing-via-the-oak-run-jar.md) 도구를 사용하여 대상 AEM 버전의 인덱스 정의에 대해 인덱스를 만드는 것이 좋습니다. 위의 다이어그램은 오프라인 리인덱싱 접근 방식을 보여 줍니다.

또한 접근 방식에 설명된 대로 단계 순서는 다음과 같습니다.

1. 바이너리의 텍스트가 먼저 추출됩니다.
2. 대상 색인 정의가 생성됨
3. 오프라인 색인이 만들어집니다.
4. 그런 다음 업그레이드 프로세스 중에 인덱스를 가져옵니다

### 텍스트 추출 {#text-extraction}

AEM에서 전체 인덱싱을 활성화하려면 PDF과 같은 바이너리의 텍스트가 추출되어 인덱스에 추가됩니다. 이는 일반적으로 인덱싱 프로세스의 많은 비용이 드는 단계입니다. 텍스트 추출은 많은 수의 바이너리를 저장할 때 자산 저장소를 리인덱싱하는 데 특히 권장되는 최적화 단계입니다.

![오프라인 리인덱싱 업그레이드 텍스트 추출](assets/offline-reindexing-upgrade-text-extraction.png)

시스템에 저장된 바이너리의 텍스트는 tika 라이브러리와 함께 oak-run 도구를 사용하여 추출할 수 있습니다. 업그레이드 전에 프로덕션 시스템의 클론을 가져와 이 텍스트 추출 프로세스에 사용할 수 있습니다. 그런 다음 다음 다음 단계를 수행하여 텍스트 저장소를 만듭니다.

**1. 저장소를 트래버스하고 이진 파일의 세부 정보를 수집합니다**

이 단계에서는 경로 및 Blob ID를 포함하는 바이너리의 튜플이 포함된 CSV 파일을 생성합니다.

인덱스를 만들려는 디렉토리에서 아래 명령을 실행합니다. 아래 예제에서는 저장소 홈 디렉터리를 가정합니다.

```
java java -jar oak-run.jar tika <nodestore path> --fds-path <datastore path> --data-file text-extraction/oak-binary-stats.csv --generate
```

여기서 `nodestore path`은(는) `mongo_ur` 또는 `crx-quickstart/repository/segmentstore/`입니다.

`–fds-path` 대신 `--fake-ds-path=temp` 매개 변수를 사용하여 프로세스 속도를 높입니다.

**2. 기존 인덱스**&#x200B;에서 사용할 수 있는 이진 텍스트 저장소를 다시 사용합니다.

기존 시스템에서 인덱스 데이터를 덤프하고 텍스트 저장소를 추출합니다.

다음 명령을 사용하여 기존 인덱스 데이터를 덤프할 수 있습니다.

```
java -jar oak-run.jar index <nodestore path> --fds-path=<datastore path> --index-dump
```

여기서 `nodestore path`은(는) `mongo_ur` 또는 `crx-quickstart/repository/segmentstore/`입니다.

그런 다음 위의 인덱스 덤프를 사용하여 스토어를 채웁니다.

```
java -jar oak-run.jar tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --index-dir ./indexing-result/index-dumps/<oak-index-name>/data populate
```

여기서 `oak-index-name`은(는) 전체 텍스트 인덱스의 이름입니다(예: &quot;lucene&quot;).

**3. 위의** 단계에서 누락된 바이너리에 대해 tika 라이브러리를 사용하여 텍스트 추출 프로세스를 실행합니다.

```
java -cp oak-run.jar:tika-app-1.21.jar org.apache.jackrabbit.oak.run.Main tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --fds-path <datastore path> extract
```

여기서 `datastore path`은(는) 이진 데이터 저장소의 경로입니다.

생성된 텍스트 저장소는 업데이트하여 향후 시나리오를 리인덱싱하는 데 재사용할 수 있습니다.

텍스트 추출 프로세스에 대한 자세한 내용은 [Oak 실행 설명서](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html)를 참조하세요.

### 오프라인 리인덱싱 {#offline-reindexing}

![오프라인 리인덱싱-업그레이드-오프라인 리인덱싱](assets/offline-reindexing-upgrade-offline-reindexing.png)

업그레이드 전에 Lucene 인덱스를 오프라인으로 만듭니다. MongoMK를 사용하는 경우 네트워크 오버헤드를 방지하므로 MongoMk 노드 중 하나에서 직접 실행하는 것이 좋습니다.

인덱스를 오프라인으로 만들려면 아래 단계를 따르십시오.

**1. 대상 AEM 버전**&#x200B;에 대한 Oak Lucene 인덱스 정의를 생성합니다.

기존 인덱스 정의를 덤프합니다. 변경된 색인 정의는 대상 AEM 버전 및 oak-run의 Adobe Granite 저장소 번들을 사용하여 생성되었습니다.

**source** AEM 인스턴스에서 인덱스 정의를 덤프하려면 다음 명령을 실행합니다.

>[!NOTE]
>
>인덱스 정의 덤프에 대한 자세한 내용은 [Oak 설명서](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#async-index-data)를 참조하세요.

```
java -jar oak-run.jar index --fds-path <datastore path> <nodestore path> --index-definitions
```

여기서 `datastore path` 및 `nodestore path`은(는) **소스** AEM 인스턴스의 것입니다.

그런 다음 대상 버전의 Granite 저장소 번들을 사용하여 **target** AEM 버전에서 색인 정의를 생성합니다.

```
java -cp oak-run.jar:bundle-com.adobe.granite.repository.jar org.apache.jackrabbit.oak.index.IndexDefinitionUpdater --in indexing-definitions_source.json --out merge-index-definitions_target.json --initializer com.adobe.granite.repository.impl.GraniteContent
```

>[!NOTE]
>
>위의 인덱스 정의 만들기 프로세스는 `oak-run-1.12.0` 버전 이상에서만 지원됩니다. 타깃팅은 Granite 저장소 번들 `com.adobe.granite.repository-x.x.xx.jar`을(를) 사용하여 수행됩니다.

위의 단계에서는 인덱스 정의인 `merge-index-definitions_target.json`이라는 JSON 파일을 만듭니다.

**2. 저장소에 검사점을 만듭니다**

수명이 긴 프로덕션 **소스** AEM 인스턴스에 검사점을 만듭니다. 이 작업은 저장소를 복제하기 전에 수행해야 합니다.

`http://serveraddress:serverport/system/console/jmx`에 있는 JMX 콘솔을 통해 `CheckpointMBean`(으)로 이동하여 충분한 수명(예: 200일)으로 검사점을 만드십시오. 이 경우 수명 기간(밀리초)에 대한 인수로 `17280000000`을(를) 사용하여 `CheckpointMBean#createCheckpoint`을(를) 호출하십시오.

이 작업이 완료되면 새로 만든 검사점 ID를 복사하고 JMX `CheckpointMBean#listCheckpoints`을(를) 사용하여 수명의 유효성을 검사합니다.

>[!NOTE]
>
>이 체크포인트는 나중에 인덱스를 가져올 때 삭제됩니다.

자세한 내용은 Oak 설명서에서 [검사점 만들기](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#out-of-band-create-checkpoint)를 참조하십시오.

**생성된 인덱스 정의에 대해 오프라인 인덱싱을 수행합니다**

Lucene 리인덱싱은 oak-run을 사용하여 오프라인으로 수행할 수 있습니다. 이 프로세스는 `indexing-result/indexes` 아래의 디스크에 인덱스 데이터를 만듭니다. 저장소에 쓰지 **않습니다**. 따라서 실행 중인 AEM 인스턴스를 중지할 필요가 없습니다. 생성된 텍스트 저장소는 다음 프로세스에 사용됩니다.

```
java -Doak.indexer.memLimitInMB=500 -jar oak-run.jar index <nodestore path> --reindex --doc-traversal-mode --checkpoint <checkpoint> --fds-path <datastore path> --index-definitions-file merge-index-definitions_target.json --pre-extracted-text-dir text-extraction/store

Sample <checkpoint> looks like r16c85700008-0-8
—fds-path: path to data store.
--pre-extracted-text-dir: Directory of pre-extracted text.
merge-index-definitions_target: JSON file having merged definitions for the target AEM instance. indexes in this file will be re-indexed.
```

`--doc-traversal-mode` 매개 변수를 사용하면 저장소 콘텐츠를 로컬 플랫 파일로 스풀링하여 색인 재지정 시간을 크게 향상시킬 수 있으므로 MongoMK 설치에 편리합니다. 그러나 저장소 크기의 두 배인 추가 디스크 공간이 필요합니다.

MongoMK가 있는 경우, 이 단계가 MongoDB 인스턴스에 더 가까운 인스턴스에서 실행되면 이 프로세스를 가속화할 수 있습니다. 동일한 시스템에서 실행되면 네트워크 오버헤드를 방지할 수 있습니다.

추가 기술 세부 정보는 [색인화를 위한 oak-run 설명서](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html)에서 찾을 수 있습니다.

### 인덱스 가져오기 {#importing-indexes}

AEM 6.4 이상 버전에서는 AEM에 시작 시퀀스 시 디스크에서 인덱스를 가져오는 기능이 내장되어 있습니다. 시작하는 동안 `<repository>/indexing-result/indexes` 폴더에서 인덱스 데이터가 있는지 확인합니다. **target** AEM jar의 새 버전으로 시작하기 전에 [업그레이드 프로세스](in-place-upgrade.md#performing-the-upgrade)를 진행하는 동안 미리 만든 인덱스를 위의 위치에 복사할 수 있습니다. AEM은 이를 저장소로 가져오고 시스템에서 해당 체크포인트를 제거합니다. 따라서 색인 재지정은 완전히 방지됩니다.

## 추가 팁 및 문제 해결 {#troubleshooting}

아래에서 몇 가지 유용한 팁과 문제 해결 지침을 확인할 수 있습니다.

### 라이브 프로덕션 시스템에 미치는 영향 감소 {#reduce-the-impact-on-the-live-production-system}

운영 시스템을 복제하고 클론을 사용하여 오프라인 인덱스를 만드는 것이 좋습니다. 이렇게 하면 운영 시스템에 미치는 잠재적 영향이 제거됩니다. 하지만 인덱스를 가져오는 데 필요한 체크포인트는 프로덕션 시스템에 있어야 합니다. 따라서 클론을 만들기 전에 체크포인트를 만드는 것은 매우 중요합니다.

### Runbook 및 평가판 실행 준비 {#prepare-a-runbook-and-trial-run}

프로덕션에서 업그레이드를 실행하기 전에 [Runbook](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/upgrade-planning.html?lang=ko#building-the-upgrade-and-rollback-runbook)을(를) 준비하고 몇 가지 시도를 수행하는 것이 좋습니다.

### 오프라인 색인화가 있는 문서 순회 모드 {#doc-traversal-mode-with-offline-indexing}

오프라인 색인화에는 전체 저장소에 대한 여러 순회가 필요합니다. MongoMK 설치를 통해 저장소는 네트워크를 통해 액세스되며 인덱싱 프로세스의 성능에 영향을 미칩니다. 한 가지 옵션은 MongoDB 복제본 자체에서 오프라인 인덱싱 프로세스를 실행하여 네트워크 오버헤드를 제거하는 것입니다. 또 다른 옵션은 문서 순회 모드 사용입니다.

오프라인 인덱싱을 위해 oak-run 명령에 명령줄 매개 변수 `—doc-traversal`을(를) 추가하여 문서 순회 모드를 적용할 수 있습니다. 이 모드는 로컬 디스크의 전체 저장소 복사본을 플랫 파일로 스풀링하고 이를 사용하여 인덱싱을 실행합니다.
