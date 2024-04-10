---
title: Oak 색인 문제 해결
description: 색인화가 느리는지 확인하고 원인을 찾아 문제를 해결하는 방법을 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
exl-id: 85981463-189c-4f50-9d21-1d2f734b960a
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '1387'
ht-degree: 0%

---

# Oak 색인 문제 해결{#troubleshooting-oak-indexes}

## 느린 리인덱싱  {#slow-re-indexing}

AEM 내부 리인덱싱 프로세스는 수행적 콘텐츠 쿼리를 지원하기 위해 저장소 데이터를 수집하고 Oak 인덱스에 저장합니다. 예외적인 상황에서는 프로세스가 느려지거나 심지어 중단될 수 있습니다. 이 페이지는 색인화가 느려지는지 식별하고 원인을 찾고 문제를 해결하는 데 도움이 되는 문제 해결 가이드 역할을 합니다.

부적절하게 긴 시간이 소요되는 리인덱싱과 방대한 양의 컨텐츠를 인덱싱하는 것이므로 긴 시간이 소요되는 리인덱싱을 구분하는 것이 중요합니다. 예를 들어 컨텐츠 크기와 함께 컨텐츠 크기를 색인화하는 데 걸리는 시간이 짧기 때문에 큰 프로덕션 리포지토리는 작은 개발 리포지토리보다 색인을 다시 지정하는 데 더 오래 걸립니다.

다음을 참조하십시오. [쿼리 및 색인화에 대한 우수 사례](/help/sites-deploying/best-practices-for-queries-and-indexing.md) 콘텐츠를 다시 인덱싱하는 시기 및 방법에 대한 추가 정보.

## 초기 감지 {#initial-detection}

초기 검색 느린 색인화를 사용하려면 `IndexStats` JMX MBean. 영향을 받는 AEM 인스턴스에서 다음을 수행합니다.

1. 웹 콘솔을 열고 JMX 탭을 클릭하거나 https://으로 이동합니다.&lt;host>:&lt;port>/system/console/jmx (예: [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)).
1. 다음 위치로 이동 `IndexStats` 음베안
1. 를 엽니다. `IndexStats` &quot;에 대한 MBean `async`&quot; 및 &quot; `fulltext-async`&quot;.

1. 두 MBean에 대해 **완료** 타임스탬프 및 **LastIndexTime** 타임스탬프는 현재 시간으로부터 45분 미만입니다.

1. 두 MBean 중 하나의 경우, 시간 값(**완료** 또는 **LastIndexedTime**)가 현재 시간에서 45분 초과인 경우 인덱스 작업이 실패하거나 너무 오래 걸립니다. 이 문제로 인해 비동기 인덱스가 오래된 상태가 됩니다.

## 강제 종료 후 인덱싱이 일시 중지되었습니다. {#indexing-is-paused-after-a-forced-shutdown}

강제 종료로 인해 AEM이 다시 시작 후 최대 30분 동안 비동기 인덱싱을 일시 중단합니다. 그리고 일반적으로 첫 번째 리인덱싱 패스를 완료하는 데 15분이 추가로 필요하며, 총 45분 정도 걸립니다(다시 연결). [초기 감지](/help/sites-deploying/troubleshooting-oak-indexes.md#initial-detection) 시간(45분). 강제 종료 후 인덱싱이 일시 중지된 경우:

1. 먼저 AEM 인스턴스가 강제 방식으로 종료되었는지(AEM 프로세스가 강제 종료되었거나 전원 오류가 발생했는지) 확인하고 나중에 다시 시작하십시오.

   * [AEM 로깅](/help/sites-deploying/configure-logging.md) 이를 위해 검토할 수 있습니다.

1. 강제 종료가 발생한 경우 다시 시작하면 AEM은 최대 30분 동안 자동으로 색인 재지정을 일시 중단합니다.
1. AEM이 일반적인 비동기 인덱싱 작업을 다시 시작할 때까지 약 45분 정도 기다립니다.

## 스레드 풀이 오버로드됨 {#thread-pool-overloaded}

>[!NOTE]
>
>AEM 6.1의 경우 다음을 확인합니다 [AEM 6.1 CFP 11](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html) 이(가) 설치되었습니다.

예외적인 상황에서는 비동기 인덱싱을 관리하는 데 사용되는 스레드 풀이 오버로드될 수 있습니다. 인덱싱 프로세스를 분리하기 위해 스레드 풀을 구성하여 다른 AEM 작업이 Oak의 적시 콘텐츠 인덱싱 기능을 방해하지 않도록 할 수 있습니다. 이 경우 다음을 수행합니다.

1. 비동기 인덱싱에 사용할 Apache Sling 스케줄러에 대해 격리된 새 스레드 풀을 정의합니다.

   * 영향을 받는 AEM 인스턴스에서 AEM OSGi 웹 콘솔>OSGi>구성>Apache Sling 스케줄러로 이동하거나 https://으로 이동합니다.&lt;host>:&lt;port>/system/console/configMgr (예: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr))
   * 값이 &quot;oak&quot;인 &quot;허용된 스레드 풀&quot; 필드에 항목을 추가합니다.
   * 변경 사항을 저장하려면 를 클릭합니다. **저장** 오른쪽 하단에 있습니다.

   ![chlimage_1-119](assets/chlimage_1-119.png)

1. 새 Apache Sling 스케줄러 스레드 풀이 등록되고 Apache Sling 스케줄러 상태 웹 콘솔에 표시되는지 확인합니다.

   * AEM OSGi 웹 콘솔>상태>Sling 스케줄러로 이동하거나 https://으로 이동합니다.&lt;host>:&lt;port>/system/console/status-slingscheduler(예: [http://localhost:4502/system/console/status-slingscheduler](http://localhost:4502/system/console/status-slingscheduler))
   * 다음 풀 항목이 있는지 확인하십시오.

      * 아파치슬링고악
      * ApacheSlingdefault

   ![chlimage_1-120](assets/chlimage_1-120.png)

## 관찰 큐가 가득 찼습니다. {#observation-queue-is-full}

짧은 시간에 너무 많은 변경 사항과 커밋이 저장소에 수행된 경우 전체 관찰 큐로 인해 인덱싱이 지연될 수 있습니다. 먼저 관찰 대기열이 가득 찼는지 확인합니다.

1. 웹 콘솔로 이동하고 JMX 탭을 클릭하거나 https://으로 이동합니다.&lt;host>:&lt;port>/system/console/jmx (예: [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
1. Oak 저장소 통계 MBean을 열고 있는지 확인합니다. `ObservationQueueMaxLength` 값이 10,000보다 큽니다.

   * 일반 작업에서 이 최대값은 항상 0으로 감소해야 합니다(특히 `per second` 섹션)을 클릭하여 `ObservationQueueMaxLength`의 초 지표는 0입니다.
   * 값이 10,000 이상이며 꾸준히 증가하는 경우 새로운 변경(커밋)이 발생하는 즉시 하나 이상의 대기열을 처리할 수 없음을 나타냅니다.
   * 각 관찰 큐에는 제한(기본적으로 10,000)이 있으며 큐가 해당 제한에 도달하면 처리가 저하됩니다.
   * MongoMK를 사용할 때 대기열 길이가 커지면 내부 Oak 캐시 성능이 저하됩니다. 이러한 상관관계는 증가한 것으로 볼 수 있다 `missRate` 대상: `DocChildren` 의 캐시 `Consolidated Cache` 통계 MBean

1. 허용 가능한 관찰 대기열 한도를 초과하지 않도록 다음 작업을 수행하는 것이 좋습니다.

   * 일정한 커밋 비율을 낮춥니다. 커밋의 짧은 스파이크는 허용되지만 상수 비율은 감소해야 합니다.
   * 크기 늘리기 `DiffCache` 에 설명된대로 [성능 조정 팁 > Mongo Storage Tuning > 문서 캐시 크기](/help/sites-deploying/configuring-performance.md).

## 중단된 리인덱싱 프로세스 식별 및 수정 {#identifying-and-remediating-a-stuck-re-indexing-process}

리인덱싱은 다음 두 가지 조건에서 &quot;완전히 중단&quot;된 것으로 간주될 수 있습니다.

* 통과하는 노드 수와 관련하여 로그 파일에 중요한 진행 상황이 보고되지 않을 정도로 리인덱싱이 느립니다.

   * 예를 들어 한 시간 동안 메시지가 없거나 진행이 너무 느려 완료하는 데 1주 이상 걸리는 경우 등이 있습니다.

* 로그 파일에 반복된 예외가 나타나면 색인 재지정이 무한 루프에 멈춥니다(예: `OutOfMemoryException`) 내의 인덱싱 스레드를 참조하십시오. 로그에 하나 이상의 동일한 예외가 반복되면 Oak가 동일한 항목을 반복적으로 색인화하려고 시도하지만 동일한 문제에서 실패함을 나타냅니다.

중단된 리인덱싱 프로세스를 식별하고 수정하려면 다음을 수행합니다.

1. 색인화가 중단된 원인을 식별하려면 다음 정보를 수집해야 합니다.

   * 5분의 스레드 덤프를 수집하고, 2초마다 하나의 스레드 덤프를 수집합니다.
   * [appenders에 대한 DEBUG 수준 및 로그 설정](/help/sites-deploying/configure-logging.md).

      * *org.apache.jackrabbit.oak.plugins.index.AsyncIndexUpdate*
      * *org.apache.jackrabbit.oak.plugins.index.IndexUpdate*

   * 비동기화에서 데이터 수집 `IndexStats` MBean:

      * AEM OSGi Web Console>Main>JMX>IndexStat>async로 이동합니다

        또는 다음으로 이동 [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats)

   * 사용 [oak-run.jar의 콘솔 모드](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run) * 아래에 있는 의 세부 정보를 수집하려면 `/:async`* 노드.
   * 다음을 사용하여 저장소 체크포인트 목록 수집 `CheckpointManager` MBean:

      * AEM OSGi 웹 콘솔>기본>JMX>CheckpointManager>listCheckpoints()

        또는 다음으로 이동 [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager)

1. 1단계에서 설명한 모든 정보를 수집한 후 AEM을 다시 시작합니다.

   * AEM을 다시 시작하면 동시 부하가 높은 경우(관찰 대기열 오버플로 등) 문제를 해결할 수 있습니다.
   * 다시 시작해도 문제가 해결되지 않으면 다음 문제를 열어 보십시오. [Adobe 고객 지원 센터](https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=home#support) 1단계에서 수집된 모든 정보를 제공합니다.

## 비동기 리인덱싱을 안전하게 중단합니다. {#safely-aborting-asynchronous-re-indexing}

리인덱싱은 를 통해 안전하게 중단(완료되기 전에 중지)할 수 있습니다. `async, async-reindex`및 f `ulltext-async` 색인화 레인( `IndexStats` Mbean). 자세한 내용은 의 Apache Oak 설명서를 참조하십시오. [리인덱싱을 중단하는 방법](https://jackrabbit.apache.org/oak/docs/query/indexing.html#abort-reindex). 또한 다음 사항을 고려하십시오.

* Lucene 및 Lucene 속성 인덱스 리인덱싱은 비동기적이므로 중단될 수 있습니다.
* Oak 속성 인덱스의 리인덱싱은 를 통해 리인덱싱이 시작된 경우에만 중단할 수 있습니다. `PropertyIndexAsyncReindexMBean`.

리인덱싱을 안전하게 중단하려면 다음 단계를 따르십시오.

1. 중지해야 하는 리인덱싱 레인을 제어하는 IndexStats MBean을 식별합니다.

   * AEM OSGi 웹 콘솔>메인>JMX 또는 https://으로 이동하여 JMX 콘솔을 통해 해당 IndexStats MBean으로 이동합니다.&lt;host>:&lt;port>/system/console/jmx (예: [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
   * 중지하려는 리인덱싱 레인을 기반으로 IndexStats MBean을 엽니다. ( `async`, `async-reindex`, 또는 `fulltext-async`)

      * 적절한 레인과 IndexStats MBean 인스턴스를 식별하려면 Oak Indexes &quot;async&quot; 속성을 참조하십시오. &quot;async&quot; 속성은 레인 이름을 포함합니다. `async`, `async-reindex`, 또는 `fulltext-async`.
      * &quot;비동기&quot; 열에서 AEM Index Manager에 액세스하여 레인을 사용할 수도 있습니다. 색인 관리자에 액세스하려면 작업>진단>색인 관리자로 이동합니다.

   ![chlimage_1-121](assets/chlimage_1-121.png)

1. 호출 `abortAndPause()` 적절한 명령 `IndexStats` MBean.
1. 색인 지정 레인이 다시 시작될 때 색인 재지정을 다시 시작하지 않도록 Oak 색인 정의를 적절하게 표시하십시오.

   * 리인덱싱 시 **기존** index, reindex 속성을 false로 설정합니다.

      * `/oak:index/someExistingIndex@reindex=false`

   * 또는 **신규** 색인:

      * 유형 속성을 비활성화로 설정

         * `/oak:index/someNewIndex@type=disabled`

      * 또는 색인 정의를 완전히 제거하십시오

   완료되면 변경 사항을 저장소에 커밋합니다.

1. 마지막으로, 중단된 인덱싱 레인에서 비동기 인덱싱을 다시 시작합니다.

   * 다음에서 `IndexStats` 을(를) 발급한 MBean `abortAndPause()` 2단계의 명령에서 `resume()`명령입니다.

## 느린 리인덱싱 방지 {#preventing-slow-re-indexing}

색인을 재지정하는 것은 조용한 기간(예: 대규모 콘텐츠 수집 중이 아님) 및 이상적으로 AEM 로드가 알려지고 제어되는 유지 관리 기간 동안 가장 좋습니다. 또한 다른 유지 관리 활동 중에 리인덱싱이 수행되지 않도록 해야 합니다.
