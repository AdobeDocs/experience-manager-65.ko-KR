---
title: Oak 색인 문제 해결
seo-title: Troubleshooting Oak Indexes
description: 느린 재색인을 감지하고 수정하는 방법입니다.
uuid: 6567ddae-128c-4302-b7e8-8befa66b1f43
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: ea70758f-6726-4634-bfb4-a957187baef0
exl-id: 85981463-189c-4f50-9d21-1d2f734b960a
source-git-commit: 9defa6d1843007e9375d839f72f6993c691a37c0
workflow-type: tm+mt
source-wordcount: '1474'
ht-degree: 2%

---

# Oak 색인 문제 해결{#troubleshooting-oak-indexes}

## 느린 다시 인덱싱  {#slow-re-indexing}

AEM 내부 재인덱싱 프로세스는 저장소 데이터를 수집하여 Oak 인덱스에 저장하여 컨텐츠 쿼리 성능을 지원합니다. 예외적인 상황에서 그 과정은 느리거나 막히게 될 수 있다. 이 페이지는 색인화가 느리는지 식별하고 원인을 찾고 문제를 해결하는 데 도움이 되는 문제 해결 가이드 역할을 합니다.

많은 양의 컨텐츠를 색인화하고 있기 때문에 적절하지 않게 오랜 시간이 걸리는 재색인화와 많은 시간이 걸리는 재색인화 간에 구별하는 것이 중요합니다. 예를 들어 컨텐츠를 인덱싱하는 데 걸리는 시간은 컨텐츠 크기에 따라 조정되므로 대규모 프로덕션 리포지토리는 작은 개발 저장소보다 재색인화하는 데 시간이 오래 걸립니다.

자세한 내용은 [쿼리 및 색인 생성에 대한 우수 사례](/help/sites-deploying/best-practices-for-queries-and-indexing.md) 컨텐츠를 다시 색인화하는 시기 및 방법에 대한 추가 정보.

## 초기 감지 {#initial-detection}

초기 감지 느린 색인화를 위해서는 `IndexStats` JMX MBeans입니다. 영향을 받는 AEM 인스턴스에서 다음을 수행합니다.

1. 웹 콘솔을 열고 JMX 탭을 클릭하거나 https://으로 이동합니다.&lt;host>:&lt;port>/system/console/jmx(예: [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)).
1. 로 이동합니다 `IndexStats` Mbeans.
1. 를 엽니다. `IndexStats` &quot; `async`&quot; 및 &quot; `fulltext-async`&quot;.

1. 두 MBean의 경우 **완료** 타임스탬프 및 **LastIndexTime** 타임스탬프는 현재 시간에서 45분 미만입니다.

1. 두 MBean의 경우, 시간 값(**완료** 또는 **LastIndexedTime**)가 현재 시간으로부터 45분 이상인 경우 인덱스 작업이 실패하거나 너무 오래 걸립니다. 이 문제로 인해 비동기 인덱스가 부실하게 됩니다.

## 강제 종료 후 색인이 일시 중지되었습니다. {#indexing-is-paused-after-a-forced-shutdown}

강제 종료로 인해 AEM에서 다시 시작한 후 최대 30분 동안 비동기 색인화가 일시 중단됩니다. 그리고 일반적으로 첫 번째 재색인화 패스를 완료하는 데 15분이 더 필요합니다. 총 45분 동안(다시 연결함) [초기 감지](/help/sites-deploying/troubleshooting-oak-indexes.md#initial-detection) 45분). 강제 종료 후 인덱싱이 일시 중지된 경우:

1. 먼저 AEM 인스턴스가 강제 방식으로 종료되었는지(AEM 프로세스가 강제로 종료되었는지 또는 전원 장애가 발생했는지) 확인하고 나중에 다시 시작되었는지 확인합니다.

   * [AEM 로깅](/help/sites-deploying/configure-logging.md) 이 목적을 위해 검토할 수 있습니다.

1. 강제 종료가 발생한 경우 다시 시작 시 AEM은 최대 30분 동안 재색인을 자동으로 일시 중단합니다.
1. AEM이 일반적인 비동기 색인 작업을 다시 시작할 때까지 약 45분을 기다립니다.

## 스레드 풀이 오버로드됨 {#thread-pool-overloaded}

>[!NOTE]
>
>AEM 6.1의 경우 [AEM 6.1 CFP 11](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ko-KR) 가 설치되어 있습니다.

특히 비동기 색인 관리에 사용되는 스레드 풀이 오버로드될 수 있습니다. 인덱싱 프로세스를 격리하기 위해 다른 AEM 작업이 Oak의 컨텐츠 인덱싱 기능을 적시에 방해하지 않도록 스레드 풀을 구성할 수 있습니다. 이 경우 다음을 수행합니다.

1. 비동기 색인화에 사용할 Apache Sling Scheduler에 대해 격리된 새 스레드 풀을 정의합니다.

   * 영향을 받는 AEM 인스턴스에서 AEM OSGi Web Console>OSGi>구성>Apache Sling Scheduler로 이동하거나 https://으로 이동합니다.&lt;host>:&lt;port>/system/console/configMgr(예: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr))
   * &quot;oak&quot; 값을 사용하여 &quot;허용된 스레드 풀&quot; 필드에 항목을 추가합니다.
   * 변경 사항을 저장하려면 **저장** 오른쪽 아래에 있습니다.

   ![chlimage_1-119](assets/chlimage_1-119.png)

1. 새 Apache Sling Scheduler 스레드 풀이 등록되어 Apache Sling Scheduler 상태 웹 콘솔에 표시되는지 확인합니다.

   * AEM OSGi 웹 콘솔>상태>Sling 스케줄러로 이동하거나 https:// 로 이동합니다.&lt;host>:&lt;port>/system/console/status-slingscheduler(예: [http://localhost:4502/system/console/status-slingscheduler](http://localhost:4502/system/console/status-slingscheduler))
   * 다음 풀 항목이 있는지 확인합니다.

      * ApacheSlingoak
      * ApacheSlingdefault

   ![chlimage_1-120](assets/chlimage_1-120.png)

## 감시 큐가 가득 찼습니다. {#observation-queue-is-full}

너무 많은 변경 및 커밋이 짧은 시간 내에 저장소에 수행된 경우 전체 관찰 큐로 인해 색인화가 지연될 수 있습니다. 먼저 관찰큐가 가득 찼는지 확인합니다.

1. 웹 콘솔로 이동하고 JMX 탭을 클릭하거나 https://으로 이동합니다.&lt;host>:&lt;port>/system/console/jmx(예: [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
1. Oak 저장소 통계 MBean을 열고 있는지 확인합니다. `ObservationQueueMaxLength` 값이 10,000보다 큼.

   * 일반 작업에서는 이 최대값이 항상 0으로 감소해야 합니다(특히 `per second` 섹션)을 입력하여 `ObservationQueueMaxLength`의 초 지표는 0입니다.
   * 값이 10,000 이상이고 값이 꾸준히 증가하면 새 변경(커밋)이 발생하는 것처럼 하나 이상의 큐를 빠르게 처리할 수 없음을 나타냅니다.
   * 각 관찰 대기열에는 제한(기본적으로 10,000개)이 있으며, 큐가 이 제한을 초과하는 경우 해당 처리는 저하됩니다.
   * MongoMK를 사용할 때, 큐 길이가 크게 늘어나면 내부 Oak 캐시 성능이 저하됩니다. 이러한 상관 관계는 증가된 위치에서 볼 수 있습니다 `missRate` 대상 `DocChildren` 의 캐시 `Consolidated Cache` 통계 MBean.

1. 허용 가능한 관찰 큐 제한을 초과하지 않도록 하려면 다음을 수행하는 것이 좋습니다.

   * 커밋 상수 비율을 낮춥니다. 커밋 의 짧은 스파이크는 허용되지만 상수 속도를 줄여야 합니다.
   * 의 크기를 늘립니다 `DiffCache` 에 설명된 대로 [성능 조정 팁 > Mongo Storage 조정 > 문서 캐시 크기](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/configuring/configuring-performance.html?lang=ko-KR).

## 중단된 재인덱싱 프로세스 식별 및 수정 {#identifying-and-remediating-a-stuck-re-indexing-process}

재색인화는 다음 두 가지 조건에서 &quot;완전히 정지&quot;로 간주될 수 있습니다.

* 재색인화는 느리며, 통과 중인 노드 수와 관련하여 로그 파일에 중요한 진행 상태가 보고되지 않는 지점까지 느려집니다.

   * 예를 들어 한 시간 동안 메시지가 없거나 진행 속도가 너무 느려서 완료하는 데 1주일 이상 걸리는 경우

* 로그 파일에 반복되는 예외가 나타나면 재색인화가 무한 루프에 남습니다(예: `OutOfMemoryException`)을 포함합니다. 로그에 동일한 하나 이상의 예외가 반복되면 Oak가 동일한 항목을 반복적으로 색인화하려고 하지만 동일한 문제에 대해 실패합니다.

중단된 재인덱싱 프로세스를 식별하고 수정하려면 다음을 수행합니다.

1. 색인화가 중단된 원인을 식별하려면 다음 정보를 수집해야 합니다.

   * 스레드 덤프 5분, 스레드 덤프 1개를 2초마다 수집합니다.
   * [응용 프로그램에 대한 DEBUG 수준 및 로그 설정](/help/sites-deploying/configure-logging.md).

      * *org.apache.jackrabbit.oak.plugins.index.AsyncIndexUpdate*
      * *org.apache.jackrabbit.oak.plugins.index.IndexUpdate*
   * 비동기에서 데이터 수집 `IndexStats` MBean:

      * AEM OSGi Web Console>Main>JMX>IndexStat>async로 이동합니다.

         또는 [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats)
   * 사용 [oak-run.jar의 콘솔 모드](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run) * 아래에 있는 사항에 대한 세부 정보를 수집하려면 `/:async`* 노드 아래에 나열됩니다.
   * 를 사용하여 저장소 체크포인트 목록을 수집합니다 `CheckpointManager` MBean:

      * AEM OSGi 웹 콘솔>주>JMX>CheckpointManager>listCheckpoints()

         또는 [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager)



1. 1단계에서 설명한 모든 정보를 수집한 후 AEM을 다시 시작합니다.

   * AEM을 다시 시작하면 동시 로드가 높은 경우(관찰 큐 오버플로우 또는 유사한) 문제를 해결할 수 있습니다.
   * 다시 시작해도 문제가 해결되지 않으면 [고객 지원 Adobe](https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=home#support) 및 는 1단계에서 수집된 모든 정보를 제공합니다.

## 비동기 재색인화를 안전하게 중단합니다. {#safely-aborting-asynchronous-re-indexing}

재색인은 를 통해 안전하게 중단(완료되기 전에 중지)할 수 있습니다. `async, async-reindex`및 f `ulltext-async` 인덱싱 레인( `IndexStats` Mbean). 자세한 내용은 다음 문서를 참조하십시오. [재인덱싱 중단 방법](https://jackrabbit.apache.org/oak/docs/query/indexing.html#abort-reindex). 또한 다음 사항을 고려하십시오.

* Lucene 및 Lucene 속성 인덱스의 재색인화는 자연스럽게 비동기적이므로 중단될 수 있습니다.
* Oak 속성 인덱스의 재색인화는 를 통해 재색인화가 시작된 경우에만 중단할 수 있습니다 `PropertyIndexAsyncReindexMBean`.

재색인을 안전하게 중단하려면 다음 단계를 수행합니다.

1. 중지해야 하는 재인덱싱 레인을 제어하는 IndexStats MBean을 식별합니다.

   * AEM OSGi Web Console>Main>JMX 또는 https:// 로 이동하여 JMX 콘솔을 통해 적절한 IndexStats MBean으로 이동합니다.&lt;host>:&lt;port>/system/console/jmx(예: [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
   * 중지할 재인덱싱 레인( `async`, `async-reindex`, 또는 `fulltext-async`)

      * 적절한 레인을 식별하고 따라서 IndexStats MBean 인스턴스를 식별하려면 Oak 인덱스 &quot;async&quot; 속성을 확인합니다. &quot;async&quot; 속성에 레인 이름이 포함되어 있습니다. `async`, `async-reindex`, 또는 `fulltext-async`.
      * 레인은 &quot;비동기&quot; 열의 AEM 색인 관리자에 액세스하여 사용할 수도 있습니다. 인덱스 관리자에 액세스하려면 작업>진단>색인 관리자로 이동합니다.

   ![chlimage_1-121](assets/chlimage_1-121.png)

1. 를 호출합니다 `abortAndPause()` 적절한 명령 `IndexStats` MBean.
1. 인덱싱 레인이 다시 시작될 때 재색인화를 다시 시작하지 않도록 Oak 색인 정의를 적절하게 표시합니다.

   * 색인화를 다시 수행할 때 **기존** index, reindex 속성을 false로 설정합니다.

      * `/oak:index/someExistingIndex@reindex=false`
   * 또는 기타, **새** 인덱스.

      * 형식 속성을 사용하지 않도록 설정합니다.

         * `/oak:index/someNewIndex@type=disabled`
      * 인덱스 정의를 완전히 제거하거나

   완료되면 변경 사항을 저장소에 커밋합니다.

1. 마지막으로 중단된 인덱싱 레인에 대한 비동기 색인 지정을 다시 시작합니다.

   * 에서 `IndexStats` 를 발행한 MBean `abortAndPause()` 2단계의 명령을 사용하여 `resume()`명령.

## 느린 다시 인덱싱 방지 {#preventing-slow-re-indexing}

AEM 로드가 알려지고 제어될 때 유지 관리 기간 중에(예: 큰 컨텐츠 수집 중에는 아님) 조용한 동안 재색인화하는 것이 가장 좋습니다. 또한 다른 유지 관리 작업 중에 재색인화가 발생하지 않도록 하십시오.
