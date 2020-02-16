---
title: Oak 인덱스 문제 해결
seo-title: Oak 인덱스 문제 해결
description: 느린 다시 인덱싱을 감지하고 수정하는 방법입니다.
seo-description: 느린 다시 인덱싱을 감지하고 수정하는 방법입니다.
uuid: 6567ddae-128c-4302-b7e8-8befa66b1f43
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: ea70758f-6726-4634-bfb4-a957187baef0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Oak 인덱스 문제 해결{#troubleshooting-oak-indexes}

## 느린 다시 인덱싱 {#slow-re-indexing}

AEM의 내부 재인덱싱 프로세스는 저장소 데이터를 수집하고 Oak 인덱스에 저장하여 컨텐츠 쿼리를 지원합니다. 예외적인 상황에서는 프로세스가 느려지거나 고정될 수 있습니다. 이 페이지는 인덱싱 속도가 느리는지 확인하고 원인을 찾고 문제를 해결하는 문제 해결 가이드 역할을 합니다.

부적절하게 오랜 시간이 소요되는 재인덱스와 방대한 양의 컨텐츠를 인덱싱하고 있기 때문에 오랜 시간이 걸리는 재색인 작성 간을 구별하는 것이 중요합니다. 예를 들어 컨텐츠를 인덱스화하는 데 걸리는 시간이 컨텐츠 양에 따라 크기 조정되므로 대규모 프로덕션 리포지토리는 작은 개발 리포지토리에 비해 재인덱스화하는 데 더 오래 걸립니다.

컨텐츠를 [다시 색인화하는 시기와 방법에 대한 자세한](/help/sites-deploying/best-practices-for-queries-and-indexing.md) 내용은 쿼리 및 색인화에 대한 우수 사례를 참조하십시오.

## 초기 감지 {#initial-detection}

초기 감지 느린 인덱싱을 사용하려면 JMX MBeans를 `IndexStats` 검토해야 합니다. 영향을 받는 AEM 인스턴스에서 다음을 수행합니다.

1. 웹 콘솔을 열고 JMX 탭을 클릭하거나 https://&lt;host>:&lt;port>/system/console/jmx(예: http://localhost:4502/system/console/jmx [](http://localhost:4502/system/console/jmx))로 이동합니다.
1. Mbeans로 `IndexStats` 이동합니다.
1. &quot;&quot; `IndexStats` `async``fulltext-async`및 &quot;&quot;에 대한 MBeans를 엽니다.

1. 두 MBeans의 경우 **Done** 타임스탬프와 LastIndexTime **타임스탬프가** 현재 시간으로부터 45분 미만인지 확인합니다.

1. MBean에 대해 시간 값(**Done** 또는 LastIndexedTime **)이 현재 시간에서 45분**&#x200B;이상인 경우 인덱스 작업이 실패하거나 너무 오래 걸립니다. 이렇게 하면 비동기 인덱스가 오래됩니다.

## 강제 종료 후 색인이 일시 중지됩니다. {#indexing-is-paused-after-a-forced-shutdown}

강제 종료하면 AEM에서 다시 시작한 후 최대 30분 동안 비동기 인덱싱을 일시 중단하게 되며, 일반적으로 첫 번째 다시 인덱싱 패스를 완료하는 데 15분이 추가로 필요하며, 이는 약 45분 동안(초기 감지 [시간보다](/help/sites-deploying/troubleshooting-oak-indexes.md#initial-detection) 45분). 강제 종료 후 인덱싱이 일시 중지된 것으로 의심되는 경우:

1. 먼저, AEM 인스턴스가 강제로 종료되었는지(AEM 프로세스가 강제로 종료되었는지 또는 전원 장애가 발생했는지) 확인하고 나중에 다시 시작되었는지 확인합니다.

   * [AEM 로깅은](/help/sites-deploying/configure-logging.md) 이 용도로 검토할 수 있습니다.

1. 강제 종료가 발생한 경우 다시 시작할 때 AEM은 최대 30분 동안 재인덱싱을 자동으로 일시 중단합니다.
1. AEM이 일반적인 비동기 인덱싱 작업을 다시 시작할 때까지 약 45분 정도 기다립니다.

## 스레드 풀 오버로드 {#thread-pool-overloaded}

>[!NOTE]
>
>AEM 6.1의 경우 AEM [6.1 CFP 11이](https://helpx.adobe.com/experience-manager/release-notes-aem-6-1-cumulative-fix-pack.html) 설치되어 있는지 확인합니다.

예외적인 상황에서는 연속 인덱싱을 관리하는 데 사용된 스레드 풀이 오버로드될 수 있습니다. 색인 프로세스를 격리하기 위해 다른 AEM 작업이 Oak의 컨텐츠 색인 지정 기능을 적시에 방해하지 않도록 스레드 풀을 구성할 수 있습니다. 이렇게 하려면 다음을 수행해야 합니다.

1. 비동기 인덱싱에 사용할 Apache Sling 스케줄러에 대한 새로운 분리된 스레드 풀을 정의합니다.

   * 영향을 받는 AEM 인스턴스에서 AEM OSGi Web Console>OSGi>Configuration>Apache Sling 스케줄러로 이동하거나 https://&lt;host>:&lt;port>/system/console/configMgr(예: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr))로 이동합니다.
   * &quot;Allowed Thread Pools&quot; 필드에 &quot;oak&quot; 값으로 항목을 추가합니다.
   * 오른쪽 하단에 있는 저장을 클릭하여 변경 사항을 저장합니다.
   ![chlimage_1-119](assets/chlimage_1-119.png)

1. 새 Apache Sling 스케줄러 스레드 풀이 등록되어 Apache Sling 스케줄러 상태 웹 콘솔에 표시되는지 확인합니다.

   * AEM OSGi 웹 콘솔>상태>스링 스케줄러로 이동하거나 https://&lt;host>:&lt;port>/system/console/status-slingscheduler(예: http://localhost:4502/system/console/status-slingscheduler [](http://localhost:4502/system/console/status-slingscheduler))로 이동합니다.
   * 다음 풀 항목이 있는지 확인합니다.

      * ApacheSlingoak
      * ApacheSlingdefault
   ![chlimage_1-120](assets/chlimage_1-120.png)

## 관측 큐가 꽉 찼습니다. {#observation-queue-is-full}

너무 많은 변경 사항 및 커밋이 짧은 시간 내에 저장소에 수행된 경우 전체 관찰 대기열로 인해 인덱싱을 지연시킬 수 있습니다. 먼저, 관측 큐가 가득 찼는지 확인합니다.

1. 웹 콘솔로 이동하여 JMX 탭을 클릭하거나 https://&lt;host>:&lt;port>/system/console/jmx(예: http://localhost:4502/system/console/jmx [](http://localhost:4502/system/console/jmx))로 이동합니다.
1. Oak 저장소 통계 MBean을 열고 값이 10,000보다 큰지 `ObservationQueueMaxLength` 확인합니다.

   * 일반적인 작업에서 이 최대값은 항상 0(특히 `per second` 섹션에서)으로 감소해야 하므로 `ObservationQueueMaxLength`의 초 지표가 0인지 확인합니다.
   * 값이 10,000개 이상이고 계속 증가하면 새 변경(커밋)이 발생하는 만큼 하나 이상의 대기열을 빠르게 처리할 수 없음을 나타냅니다.
   * 각 관측 대기열에는 제한(기본적으로 10,000개)이 있으며, 대기열 히트가 그 제한을 초과할 경우 처리 등급이 낮아집니다.
   * MongoMK를 사용하는 경우 큐 길이가 길수록 내부 Oak 캐시 성능이 저하됩니다. 이 상관 관계는 통계 MBean `missRate` 의 캐시에 대한 증가된 `DocChildren` 데이터에서 볼 수 `Consolidated Cache` 있습니다.

1. 허용 가능한 관측 대기열 제한을 초과하지 않도록 하려면 다음을 권장합니다.

   * 커밋의 상수 속도를 낮춥니다. 약도의 짧은 스파이크는 허용되지만 상수 속도를 줄여야 합니다.
   * 성능 조정 팁 > Mongo Storage `DiffCache` Tuning > Document Cache 크기에 [](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html#main-pars_text_3)설명된 대로 크기를 늘립니다.

## 중단된 재인덱싱 프로세스 확인 및 수정 {#identifying-and-remediating-a-stuck-re-indexing-process}

재인덱스는 다음 두 가지 조건 하에서 &quot;완전히 막힘&quot;으로 간주될 수 있습니다.

* 색인 재지정 속도가 매우 느리므로 탐색된 노드 수와 관련하여 로그 파일에 중요한 진행이 보고되지 않습니다.

   * 예를 들어 한 시간 동안 메시지가 없거나 진행 속도가 너무 느린 경우 완료하는 데 1주일 이상 걸립니다.

* 색인 스레드의 로그 파일(예: `OutOfMemoryException`)에 반복 예외가 나타날 경우 다시 인덱스는 무한 루프에 고정됩니다. 로그에서 동일한 예외를 반복하면 Oak가 동일한 항목을 반복적으로 색인화하려고 하지만 동일한 문제에 대해서는 실패함을 나타냅니다.

멈춘 재인덱싱 프로세스를 식별하고 수정하려면 다음을 수행합니다.

1. 색인 작업이 중단된 원인을 식별하려면 다음 정보를 수집해야 합니다.

   * 스레드 덤프의 5분, 2초마다 스레드 덤프를 하나씩 수집할 수 있습니다.
   * [응용 프로그램에 대한 DEBUG 수준 및 로그를 설정합니다](/help/sites-deploying/configure-logging.md).

      * *org.apache.jackrabbit.oak.plugins.index.AsyncIndexUpdate*
      * *org.apache.jackrabbit.oak.plugins.index.IndexUpdate*
   * 비동기 MBean에서 데이터 `IndexStats` 수집:

      * AEM OSGi 웹 콘솔>기본>JMX>IndexStat>async로 이동합니다.

         또는 http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats으로 [이동](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats)
   * oak-run.jar의 [콘솔 모드를](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run) 사용하여 * `/:async`* 노드 아래에 있는 항목에 대한 세부 정보를 수집합니다.
   * MBean을 사용하여 저장소 체크포인트 목록을 `CheckpointManager` 수집합니다.

      * AEM OSGi 웹 콘솔>기본>JMX>체크포인트 관리자>listCheckpoint()

         또는 http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager으로 [이동](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager)



1. 1단계에서 설명한 모든 정보를 수집한 후 AEM을 다시 시작합니다.

   * AEM을 다시 시작하면 동시 로드가 높은 경우(관측 대기열 오버플로우 등) 문제를 해결할 수 있습니다.
   * 다시 시작해도 문제가 해결되지 않는 경우 Adobe 고객 지원 센터에 [문제를](https://helpx.adobe.com/marketing-cloud/contact-support.html) 열어 1단계에서 수집한 모든 정보를 제공합니다.

## 비동기 다시 색인 작업을 안전하게 중단합니다. {#safely-aborting-asynchronous-re-indexing}

색인 재지정(Mbean)은 색인 레인과 f `async, async-reindex`및 `ulltext-async` 레인을 통해 안전하게 취소(완료 전에 중지)할 수 `IndexStats` 있습니다. 자세한 내용은 Apache Oak 설명서를 참조하십시오. [](https://jackrabbit.apache.org/oak/docs/query/indexing.html#abort-reindex) 또한, 다음 사항을 고려하십시오.

* Lucene 및 Lucene 속성 인덱스의 재인덱스는 원래 시간순으로 유지되므로 중단할 수 있습니다.
* Oak 속성 인덱스의 재인덱스는 를 통해 다시 색인화된 경우에만 중단할 수 `PropertyIndexAsyncReindexMBean`있습니다.

다시 인덱싱을 안전하게 중단하려면 다음 단계를 따르십시오.

1. 중지해야 하는 다시 인덱싱 레인을 제어하는 IndexStats MBean을 식별합니다.

   * AEM OSGi Web Console>Main>JMX 또는 https://&lt;host>:&lt;port>/system/console/jmx(예: [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))로 이동하여 JMX 콘솔을 통해 해당 IndexStats MBean으로 이동합니다.
   * 중지할 색인 레인(, `async``async-reindex`또는 `fulltext-async`)을 기반으로 IndexStats MBean을 엽니다.

      * 적절한 레인과 IndexStats MBean 인스턴스를 식별하려면 Oak 인덱스 &quot;async&quot; 속성을 확인합니다. &quot;async&quot; 속성에는 레인 이름이 포함됩니다. `async`또는 `async-reindex`를 `fulltext-async`선택합니다.
      * 레인은 &quot;비동기&quot; 열에서 AEM의 인덱스 관리자에 액세스하여 사용할 수도 있습니다. 색인 관리자에 액세스하려면 작업>진단>색인 관리자로 이동합니다.
   ![chlimage_1-121](assets/chlimage_1-121.png)

1. 해당 MBean에서 `abortAndPause()` 명령을 `IndexStats` 불러옵니다.
1. 색인 레인이 다시 시작될 때 다시 색인화를 다시 시작하지 않도록 Oak 인덱스 정의를 적절하게 표시합니다.

   * 다시 색인을 **기존** 색인으로 지정할 때 다시 인덱스 속성을 false로 설정합니다

      * `/oak:index/someExistingIndex@reindex=false`
   * 또는 **새** 인덱스의 경우 다음 중 하나를 수행합니다.

      * type 속성을 disabled로 설정

         * `/oak:index/someNewIndex@type=disabled`
      * 또는 색인 정의를 완전히 제거
   완료되면 변경 내용을 저장소에 커밋합니다.

1. 마지막으로, 중단된 인덱싱 레인에 대해 시간순으로 색인 지정을 다시 시작합니다.

   * 2단계에서 `IndexStats` 명령을 `abortAndPause()` 실행한 MBean에서 `resume()`명령을 호출합니다.

## 느린 다시 인덱싱 방지 {#preventing-slow-re-indexing}

대규모 컨텐츠 인제스트 중에는 물론, 조용한 기간 동안(예: 큰 컨텐츠 인제스트 중에는 제외), 그리고 AEM의 로드가 알려져 제어될 경우 유지 관리 기간 중에 이상적으로 다시 색인화하는 것이 가장 좋습니다. 또한 다른 유지 관리 작업 중에는 다시 색인화가 발생하지 않도록 하십시오.
