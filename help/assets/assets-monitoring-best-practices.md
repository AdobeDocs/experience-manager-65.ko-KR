---
title: 모니터링할 모범 사례 [!DNL Assets] 배포
description: 의 환경 및 성능을 모니터링하는 모범 사례 [!DNL Adobe Experience Manager] 배포 후 배포.
contentOwner: AG
role: Admin, Architect
feature: Asset Management
exl-id: a9e1bd6b-c768-4faa-99a3-7110693998dc
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 1%

---

# 모니터링할 모범 사례 [!DNL Adobe Experience Manager Assets] 배포 {#assets-monitoring-best-practices}

다음에서 [!DNL Experience Manager Assets] 관점에서는 모니터링에 다음 프로세스 및 기술에 대한 관찰 및 보고가 포함되어야 합니다.

* 시스템
* 시스템 메모리 사용
* 시스템 디스크 IO 및 IO 대기 시간
* 시스템 네트워크 입출력
* 힙 활용률 및 비동기 프로세스(예: 워크플로우)용 JMX MBean
* OSGi 콘솔 상태 검사

일반적으로 [!DNL Experience Manager Assets] 실시간 모니터링과 장기 모니터링, 이렇게 두 가지 방법으로 모니터링할 수 있습니다.

## 라이브 모니터링 {#live-monitoring}

개발의 성능 테스트 단계나 로드가 많은 상황에서 라이브 모니터링을 수행하여 환경의 성능 특성을 이해해야 합니다. 일반적으로 라이브 모니터링은 도구 모음을 사용하여 수행해야 합니다. 다음은 몇 가지 권장 사항입니다.

* [시각적 VM](https://visualvm.github.io/): 시각적 VM을 사용하면 CPU 사용량, Java 메모리 사용량을 포함하여 자세한 Java VM 정보를 볼 수 있습니다. 또한 배포에서 실행되는 코드를 샘플링하고 평가할 수 있도록 해줍니다.
* [상단](https://man7.org/linux/man-pages/man1/top.1.html): Top은 대시보드를 여는 Linux 명령으로 CPU, 메모리 및 IO 사용량을 포함한 사용 통계를 표시합니다. 인스턴스에서 발생하는 사항에 대한 높은 수준의 개요를 제공합니다.
* [상단](https://hisham.hm/htop/): Top은 대화형 프로세스 뷰어입니다. 탑이 제공할 수 있는 것 외에도 자세한 CPU 및 메모리 사용량을 제공합니다. Htop은 다음을 사용하여 대부분의 Linux 시스템에 설치할 수 있습니다. `yum install htop` 또는 `apt-get install htop`.

* Iotop: Iotop은 디스크 IO 사용에 대한 세부 대시보드입니다. 디스크 IO를 사용하는 프로세스와 사용되는 양을 나타내는 막대 및 미터를 표시합니다. Iotop은 다음을 사용하여 대부분의 Linux 시스템에 설치할 수 있습니다. `yum install iotop` 또는 `apt-get install iotop`.

* [Iftop](https://www.ex-parrot.com/pdw/iftop/): Iftop에 이더넷/네트워크 사용에 대한 자세한 정보가 표시됩니다. Iftop은 이더넷을 사용하는 엔터티의 통신 채널별 통계와 엔터티가 사용하는 대역폭의 양을 표시합니다. Iftop은 대부분의 Linux 시스템에 다음을 사용하여 설치할 수 있습니다 `yum install iftop` 또는 `apt-get install iftop`.

* Java Flight Recorder(JFR): 비프로덕션 환경에서 자유롭게 사용할 수 있는 Oracle의 상용 도구입니다. 자세한 내용은 [Java Flight Recorder를 사용하여 CQ 런타임 문제를 진단하는 방법](https://cq-ops.tumblr.com/post/73865704329/how-to-use-java-flight-recorder-to-diagnose-cq).
* [!DNL Experience Manager] `error.log` 파일: 다음을 조사할 수 있습니다 [!DNL Experience Manager] `error.log` 시스템에 기록된 오류에 대한 자세한 내용을 보려면 파일을 참조하십시오. 명령 사용 `tail -F quickstart/logs/error.log` 조사할 오류를 식별합니다.
* [워크플로 콘솔](/help/sites-administering/workflows.md): 워크플로우 콘솔을 활용하여 지연되거나 중단되는 워크플로우를 모니터링합니다.

일반적으로 이러한 도구를 함께 사용하여 의 성능에 대한 포괄적인 아이디어를 얻습니다. [!DNL Experience Manager] 배포.

>[!NOTE]
>
>이러한 도구는 표준 도구이며 Adobe에서 직접 지원하지 않습니다. 추가적인 라이선스가 필요하지 않습니다.

![chlimage_1-33](assets/chlimage_1-143.png)

*그림: Visual VM 도구를 사용한 라이브 모니터링*

![chlimage_1-32](assets/chlimage_1-142.png)

## 장기 모니터링 {#long-term-monitoring}

의 장기 모니터링 [!DNL Experience Manager] 배포에는 실시간으로 모니터링되는 동일한 부분을 더 오랜 기간 동안 모니터링하는 작업이 포함됩니다. 사용자 환경과 관련된 경고를 정의하는 것도 포함됩니다.

### 로그 집계 및 보고 {#log-aggregation-and-reporting}

로그를 집계하는 데 사용할 수 있는 도구로는 Splunk(TM) 및 Elastic Search, Logstash 및 Kabana(ELK)가 있습니다. 의 가동 시간을 평가하려면 [!DNL Experience Manager] 배포에서는 시스템과 관련된 로그 이벤트를 이해하고 이를 기반으로 경고를 만드는 것이 중요합니다. 개발 및 작업 사례에 대한 충분한 지식이 있으면 로그 집계 프로세스를 조정하여 중요한 경고를 생성하는 방법을 더 잘 이해할 수 있습니다.

### 환경 모니터링 {#environment-monitoring}

환경 모니터링에는 다음 모니터링이 포함됩니다.

* 네트워크 처리량
* 디스크 IO
* 메모리
* CPU 사용률
* JMX MBean
* 외부 웹 사이트

각 항목을 모니터링하려면 NewRelic(TM) 및 AppDynamics(TM)와 같은 외부 도구가 필요합니다. 이러한 도구를 사용하여 높은 시스템 사용률, 워크플로우 백업, 상태 검사 실패 또는 웹 사이트에 대한 인증되지 않은 액세스 등 시스템과 관련된 경고를 정의할 수 있습니다. Adobe은 다른 도구보다 특정 도구를 권장하지 않습니다. 자신에게 적합한 도구를 찾아 이 도구를 사용하여 논의된 항목을 모니터링합니다.

#### 내부 애플리케이션 모니터링 {#internal-application-monitoring}

내부 애플리케이션 모니터링에는 다음을 구성하는 애플리케이션 구성 요소 모니터링이 포함됩니다. [!DNL Experience Manager] JVM, 콘텐츠 저장소 및 플랫폼에 구축된 사용자 정의 애플리케이션 코드를 통한 모니터링을 포함한 스택. 일반적으로 SolarWinds(TM), HP OpenView(TM), Hyperic(TM), Zabbix(TM) 등과 같이 많은 인기 모니터링 솔루션에서 직접 모니터링할 수 있는 JMX Mbeans를 통해 수행됩니다. JMX에 대한 직접 연결을 지원하지 않는 시스템의 경우 셸 스크립트를 작성하여 JMX 데이터를 추출하고 해당 데이터를 해당 시스템에서 기본적으로 이해할 수 있는 형식으로 제공할 수 있습니다.

JMX Mbean에 대한 원격 액세스가 기본적으로 활성화되어 있지 않습니다. JMX를 통한 모니터링에 대한 자세한 내용은 [JMX 기술을 사용한 모니터링 및 관리](https://docs.oracle.com/javase/7/docs/technotes/guides/management/agent.html).

통계를 효과적으로 모니터링하려면 기준선이 필요한 경우가 많습니다. 기준선을 생성하려면 미리 결정된 기간 동안 정상 작업 조건에서 시스템을 관찰한 다음 정상 지표를 식별합니다.

**JVM 모니터링**

모든 Java 기반 애플리케이션 스택과 마찬가지로 [!DNL Experience Manager] 은(는) 기본 Java Virtual Machine을 통해 제공되는 리소스에 따라 다릅니다. JVM에 의해 노출된 Platform MXBean을 통해 이러한 리소스의 상태를 모니터링할 수 있습니다. MXBean에 대한 자세한 내용은 [Platform MBean Server 및 Platform MXBean 사용](https://docs.oracle.com/javase/7/docs/technotes/guides/management/mxbeans.html).

다음은 JVM용으로 모니터링할 수 있는 몇 가지 기준 매개 변수입니다.

메모리

* `MBean: lava.lang:type=Memory`
* URL: `/system/console/jmx/java.lang:type=Memory`
* 인스턴스: 모든 서버
* 경보 임계값: 힙 또는 비힙 메모리 사용률이 해당 최대 메모리의 75%를 초과하는 경우.
* 경보 정의: 시스템 메모리가 부족하거나 코드에 메모리 누수가 있습니다. 스레드 덤프를 분석하여 정의에 도달합니다.

>[!NOTE]
>
>이 콩이 제공하는 정보는 바이트 단위로 표현된다.

Threads

* MBean: `java.lang:type=Threading`
* URL: `/system/console/jmx/java.lang:type=Threading`
* 인스턴스: 모든 서버
* 경보 임계값: 스레드 수가 기준선의 150%보다 큰 경우.
* 경보 정의: 활성 가출 프로세스가 있거나 비효율적인 작업이 많은 양의 리소스를 소비합니다. 스레드 덤프를 분석하여 정의에 도달합니다.

**모니터링[!DNL Experience Manager]**

[!DNL Experience Manager] 또한 JMX를 통해 통계 및 작업 세트를 노출합니다. 이는 시스템 상태를 평가하고 사용자에게 영향을 미치기 전에 잠재적인 문제를 식별하는 데 도움이 될 수 있습니다. 자세한 내용은 [설명서](/help/sites-administering/jmx-console.md) 날짜 [!DNL Experience Manager] JMX MBean.

다음은 모니터링할 수 있는 몇 가지 기준선 매개 변수입니다 [!DNL Experience Manager]:

복제 에이전트

* MBean: `com.adobe.granite.replication:type=agent,id="<AGENT_NAME>"`
* URL: `/system/console/jmx/com.adobe.granite.replication:type=agent,id="<AGENT_NAME>"`
* 인스턴스: 한 명의 작성자와 모든 게시 인스턴스(플러시 에이전트의 경우)
* 경고 임계값: 다음 값 `QueueBlocked` 은(는) `true` 또는 값 `QueueNumEntries` 는 기준선의 150%보다 큽니다.

* 경고 정의: 복제 대상이 중단되었거나 연결할 수 없음을 나타내는 차단된 큐가 시스템에 있습니다. 종종 네트워크 또는 인프라 문제로 인해 과도한 항목이 큐에 올라가 시스템 성능에 부정적인 영향을 줄 수 있습니다.

>[!NOTE]
>
>MBean 및 URL 매개 변수의 경우 `<AGENT_NAME>` (모니터링할 복제 에이전트 이름 포함)

세션 카운터

* MBean: `org.apache.jackrabbit.oak:id=7,name="OakRepository Statistics",type="RepositoryStats"`
* URL: */system/console/jmx/org.apache.jackrabbit.oak:id=7,name=&quot;OakRepository Statistics&quot;,type*=&quot;RepositoryStats&quot;
* 인스턴스: 모든 서버
* 경보 임계값: 열린 세션이 기준선을 50% 넘게 초과할 때.
* 경고 정의: 세션은 코드를 통해 열릴 수 있으며 닫히지 않습니다. 이는 시간이 지남에 따라 천천히 발생할 수 있으며 결국 시스템에서 메모리 누출을 초래합니다. 세션 수는 시스템에서 변동해야 하지만 지속적으로 증가해서는 안 됩니다.

상태 검사

에서 사용할 수 있는 상태 검사 [작업 대시보드](/help/sites-administering/operations-dashboard.md#health-reports) 모니터링을 위해 해당 JMX MBean이 있습니다. 그러나 사용자 정의 상태 검사를 작성하여 추가 시스템 통계를 표시할 수 있습니다.

다음은 모니터링에 유용한 기본 상태 확인입니다.

* 시스템 확인
   * MBean: `org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * 인스턴스: 작성자 1명, 모든 게시 서버
   * 경보 임계값: 상태가 양호하지 않을 때
   * 경보 정의: 지표 중 하나의 상태가 WARN 또는 CRITICAL입니다. 문제의 원인에 대한 자세한 내용은 로그 속성을 확인하십시오.

* 복제 큐

   * MBean: `org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * 인스턴스: 작성자 1명, 모든 게시 서버
   * 경보 임계값: 상태가 양호하지 않을 때
   * 경보 정의: 지표 중 하나의 상태가 WARN 또는 CRITICAL입니다. 문제를 일으킨 큐에 대한 자세한 내용은 로그 특성을 확인하십시오.

* 응답 성능

   * MBean: `org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * 인스턴스: 모든 서버
   * 경보 기간: 상태가 양호하지 않을 때
   * 경보 정의: 지표 중 하나의 상태가 WARN 또는 CRITICAL 상태입니다. 문제를 일으킨 큐에 대한 자세한 내용은 로그 특성을 확인하십시오.

* 쿼리 성능

   * MBean: `org.apache.sling.healthcheck:name=queriesStatus,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name= queriesStatus,type=HealthCheck`
   * 인스턴스: 작성자 1명, 모든 게시 서버
   * 경보 임계값: 상태가 양호하지 않을 때
   * 경고 정의: 시스템에서 느리게 실행되는 하나 이상의 쿼리. 문제를 일으킨 쿼리에 대한 자세한 내용은 로그 속성을 확인하십시오.

* 활성 상태 번들

   * MBean: `org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * 인스턴스: 모든 서버
   * 경보 임계값: 상태가 양호하지 않을 때
   * 경고 정의: 시스템에 비활성 상태이거나 해결되지 않은 OSGi 번들이 있습니다. 문제를 일으킨 번들에 대한 자세한 내용은 로그 속성을 확인하십시오.

* 오류 로그

   * MBean: `org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * 인스턴스: 모든 서버
   * 경보 임계값: 상태가 양호하지 않을 때
   * 경보 정의: 로그 파일에 오류가 있습니다. 문제의 원인에 대한 자세한 내용은 로그 속성을 확인하십시오.

## 일반적인 문제 및 해결 방법  {#common-issues-and-resolutions}

모니터링 프로세스에서 문제가 발생하면 다음 몇 가지 문제 해결 작업을 수행하여 의 일반적인 문제를 해결할 수 있습니다. [!DNL Experience Manager] 배포:

* TarMK를 사용하는 경우 종종 Tar 압축을 실행합니다. 자세한 내용은 [저장소 유지 관리](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).
* 확인 `OutOfMemoryError` 로그. 자세한 내용은 [메모리 문제 분석](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17482.html).

* 인덱싱되지 않은 쿼리, 트리 트래버스 또는 인덱스 트래버스에 대한 참조를 로그에 확인합니다. 인덱싱되지 않은 쿼리 또는 인덱싱되지 않은 쿼리를 나타냅니다. 쿼리 및 색인화 성능 최적화에 대한 우수 사례는 다음을 참조하십시오. [쿼리 및 색인 생성에 대한 우수 사례](/help/sites-deploying/best-practices-for-queries-and-indexing.md).
* 워크플로우 콘솔을 사용하여 워크플로우가 예상대로 수행되는지 확인합니다. 가능한 경우 여러 워크플로우를 단일 워크플로우로 압축합니다.
* 라이브 모니터링을 다시 살펴보고 특정 리소스에 대한 추가 병목 현상 또는 높은 소비자를 찾아보십시오.
* 클라이언트 네트워크의 이그레스 포인트 및 인그레스 포인트를 조사합니다. [!DNL Experience Manager] dispatcher를 포함한 배포 네트워크. 병목 현상이 발생하는 경우가 많습니다. 자세한 내용은 [자산 네트워크 고려 사항](/help/assets/assets-network-considerations.md).
* 최대 크기 조정 [!DNL Experience Manager] 서버입니다. 크기가 적절하지 않습니다. [!DNL Experience Manager] 배포. Adobe 고객 지원 센터에서 서버의 용량이 부족한지 여부를 식별하는 데 도움을 줄 수 있습니다.
* 다음을 검사합니다 `access.log` 및 `error.log` 오류가 발생한 시간 이전의 항목에 대한 파일입니다. 사용자 지정 코드 예외 항목을 나타낼 수 있는 패턴을 찾으십시오. 모니터링하는 이벤트 목록에 추가합니다.
