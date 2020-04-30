---
title: '[!DNL Adobe Experience Manager Assets] 배포를 모니터링하는 모범 사례'
description: 배포 후 [!DNL Adobe Experience Manager] 배포의 환경 및 성능을 모니터링하기 위한 모범 사례
contentOwner: AG
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# Best practices to monitor [!DNL Adobe Experience Manager Assets] deployment {#assets-monitoring-best-practices}

모니터링은 [!DNL Experience Manager Assets] 측면에서 다음 프로세스 및 기술에 대한 관찰과 보고를 포함해야 합니다.

* 시스템 CPU
* 시스템 메모리 사용
* 시스템 디스크 IO 및 IO 대기 시간
* 시스템 네트워크 IO
* JMX MBeans를 사용하여 작업 과정과 같은 비동기 프로세스를 수행할 수 있습니다.
* OSGi 콘솔 상태 검사

일반적으로 실시간 모니터링과 장기 모니터링이라는 두 가지 방법으로 모니터링할 [!DNL Experience Manager Assets] 수 있습니다.

## 실시간 모니터링 {#live-monitoring}

개발 단계나 고부하 상황에서 실시간 모니터링을 수행하여 환경의 성능 특성을 이해해야 합니다. 일반적으로 라이브 모니터링은 도구 모음을 사용하여 수행해야 합니다. 다음은 권장 사항입니다.

* [시각적 VM](https://visualvm.java.net/):Visual VM을 사용하면 CPU 사용량, Java 메모리 사용을 비롯한 자세한 Java VM 정보를 볼 수 있습니다. 또한 배포에서 실행되는 코드를 샘플링하고 평가할 수 있습니다.
* [위쪽](https://man7.org/linux/man-pages/man1/top.1.html):맨 위에는 CPU, 메모리 및 IO 사용을 비롯한 사용 통계를 표시하는 대시보드를 여는 Linux 명령입니다. 인스턴스에서 발생하는 상황에 대한 고급 개요를 제공합니다.
* [상단](https://hisham.hm/htop/):상단은 대화형 프로세스 뷰어입니다. Top이 제공할 수 있는 기능 외에 자세한 CPU 및 메모리 사용량을 제공합니다. Top은 `yum install htop` 또는 를 사용하여 대부분의 Linux 시스템에 설치할 수 `apt-get install htop`있습니다.

* [위쪽](https://guichaz.free.fr/iotop/):Iotop은 디스크 IO 사용을 위한 세부 대시보드입니다. 여기에는 디스크 IO를 사용하는 프로세스와 해당 프로세스가 사용하는 양을 나타내는 막대와 미터가 표시됩니다. Linux에서는 `yum install iotop` 또는 을 사용하여 대부분의 시스템에 Iotop을 설치할 수 `apt-get install iotop`있습니다.

* [이벤트](https://www.ex-parrot.com/pdw/iftop/):Iftop에 이더넷/네트워크 사용에 대한 자세한 정보가 표시됩니다. 이때에는 이더넷을 사용하는 엔티티의 통신 채널 통계당 및 그들이 사용하는 대역폭 수치를 표시합니다. Iftop은 `yum install iftop` 또는 를 사용하여 대부분의 Linux 시스템에 설치할 수 `apt-get install iftop`있습니다.

* JFR(Java Flight Recorder):비프로덕션 환경에서 자유롭게 사용할 수 있는 Oracle의 상업용 도구입니다. 자세한 내용은 Java [플라이트 레코더를 사용하여 CQ 런타임 문제 진단을 참조하십시오](https://cq-ops.tumblr.com/post/73865704329/how-to-use-java-flight-recorder-to-diagnose-cq).
* [!DNL Experience Manager] 파일: `error.log` 시스템에 기록된 오류에 대한 세부 정보를 [!DNL Experience Manager] 확인하려면 `error.log` 파일을 조사할 수 있습니다. 이 명령을 `tail -F quickstart/logs/error.log` 사용하여 오류를 찾아 보십시오.
* [워크플로우 콘솔](/help/sites-administering/workflows.md):워크플로우 콘솔을 사용하여 지연 또는 중단되는 워크플로우를 모니터링할 수 있습니다.

일반적으로 이러한 도구를 함께 사용하여 [!DNL Experience Manager] 배포 성능에 대한 포괄적인 아이디어를 얻을 수 있습니다.

>[!NOTE]
>
>이러한 도구는 Adobe에서 직접 지원하지 않는 표준 도구입니다. 추가 라이선스는 필요하지 않습니다.

![chlimage_1-33](assets/chlimage_1-143.png)

*그림:Visual VM 도구를 사용한 실시간 모니터링*

![chlimage_1-32](assets/chlimage_1-142.png)

## 장기 모니터링 {#long-term-monitoring}

배포에 대한 장기 모니터링에는 [!DNL Experience Manager] 모니터링되는 동일한 부분을 장기간 모니터링해야 합니다. 또한 환경에 대한 경고를 정의합니다.

### 로그 집계 및 보고 {#log-aggregation-and-reporting}

Splunk(TM) 및 Elastic Search, Logstash 및 Kabana(ELK)와 같은 로그를 집계하는 데 사용할 수 있는 몇 가지 도구가 있습니다. 배포의 가동 시간을 평가하려면 [!DNL Experience Manager] 시스템 관련 로그 이벤트를 파악하고 이를 기반으로 경고를 생성해야 합니다. 개발 및 운영 사례에 대한 충분한 지식이 있으면 로그 수집 프로세스를 조정하여 중요한 경고를 생성하는 방법을 보다 잘 이해할 수 있습니다.

### 환경 모니터링 {#environment-monitoring}

환경 모니터링에는 다음 모니터링이 포함됩니다.

* 네트워크 처리량
* 디스크 IO
* 메모리
* CPU 사용률
* JMX MBeans
* 외부 웹 사이트

각 항목을 모니터링하려면 NewRelic(TM) 및 AppDynamics(TM)와 같은 외부 도구가 필요합니다. 이러한 도구를 사용하여 시스템 사용률, 워크플로우 백업, 상태 점검 실패 또는 웹 사이트에 대한 인증되지 않은 액세스 등과 같은 시스템 특정 경고를 정의할 수 있습니다. Adobe는 다른 도구에 비해 특정 도구를 권장하지 않습니다. 사용자에게 적합한 툴을 찾아 이를 활용하여 설명한 항목을 모니터링할 수 있습니다.

#### 내부 애플리케이션 모니터링 {#internal-application-monitoring}

내부 애플리케이션 모니터링에는 JVM, 컨텐츠 저장소 등 [!DNL Experience Manager] 스택을 구성하는 애플리케이션 구성 요소 모니터링과 플랫폼에 내장된 사용자 정의 애플리케이션 코드를 통한 모니터링이 포함됩니다. 일반적으로 JMX Mbeans를 통해 수행되며, SolarWinds(TM), HP OpenView(TM), Hyperic(TM), Zabbix(TM) 등과 같이 널리 사용되는 많은 모니터링 솔루션에서 직접 모니터링할 수 있습니다. JMX에 대한 직접 연결을 지원하지 않는 시스템의 경우 셸 스크립트를 작성하여 JMX 데이터를 추출하고 이러한 시스템에 기본적으로 이해할 수 있는 형식으로 표시할 수 있습니다.

JMX Mbeans에 대한 원격 액세스는 기본적으로 활성화되어 있지 않습니다. JMX를 통한 모니터링에 대한 자세한 내용은 JMX [기술을 사용한 모니터링 및 관리를 참조하십시오](https://docs.oracle.com/javase/7/docs/technotes/guides/management/agent.html).

대부분의 경우 통계를 효과적으로 모니터링하려면 기준선이 필요합니다. 기준선을 만들려면 미리 결정된 기간 동안 정상적인 작업 조건에서 시스템을 관찰한 다음 일반 지표를 식별합니다.

**JVM 모니터링**

Java 기반 애플리케이션 스택과 마찬가지로 기본 Java 가상 시스템을 통해 제공되는 리소스에 [!DNL Experience Manager] 따라 달라집니다. JVM에 의해 노출되는 플랫폼 MXBeans를 통해 이러한 리소스 중 많은 수의 상태를 모니터링할 수 있습니다. MXBeans에 대한 자세한 내용은 플랫폼 MBean [서버 및 플랫폼 MXBeans 사용을 참조하십시오](https://docs.oracle.com/javase/7/docs/technotes/guides/management/mxbeans.html).

다음은 JVM에 대해 모니터링할 수 있는 몇 가지 기준 매개 변수입니다.

메모리

* `MBean: lava.lang:type=Memory`
* URL: `/system/console/jmx/java.lang:type=Memory`
* 인스턴스:모든 서버
* 경고 임계값:더미 또는 비더미 메모리 사용률이 해당 최대 메모리의 75%를 초과하는 경우
* 경고 정의:시스템 메모리가 부족하거나 코드에 메모리 누수가 있습니다. 스레드 덤프를 분석하여 정의에 도달합니다.

>[!Note]
>
>이 Bean에서 제공하는 정보는 바이트 단위로 표시됩니다.

스레드

* MBean: `java.lang:type=Threading`
* URL: `/system/console/jmx/java.lang:type=Threading`
* 인스턴스:모든 서버
* 경고 임계값:스레드 수가 기준선의 150%보다 큰 경우
* 경고 정의:적극적인 진행 과정이나 비효율적인 작업이 많은 양의 자원을 소비한다. 스레드 덤프를 분석하여 정의에 도달합니다.

**모니터[!DNL Experience Manager]**

[!DNL Experience Manager] 또한 JMX를 통해 통계 및 작업 세트를 표시합니다. 이러한 기능은 시스템 상태를 평가하고 사용자에게 영향을 미치기 전에 잠재적인 문제를 식별하는 데 도움이 될 수 있습니다. 자세한 내용은 JMX MBeans에 대한 [설명서를](/help/sites-administering/jmx-console.md) 참조하십시오 [!DNL Experience Manager] .

다음은 모니터링할 수 있는 몇 가지 기준 매개 변수입니다. [!DNL Experience Manager]

복제 에이전트

* MBean: `com.adobe.granite.replication:type=agent,id=”<AGENT_NAME>”`
* URL: `/system/console/jmx/com.adobe.granite.replication:type=agent,id=”<AGENT_NAME>"`
* 인스턴스:작성자 및 모든 게시 인스턴스 1개(플러시 에이전트)
* 경고 임계값:값이 `QueueBlocked` 기준선 `true` 150%보다 크거나 같은 `QueueNumEntries` 경우.

* 경고 정의:시스템에서 복제 대상이 다운되었거나 액세스할 수 없음을 나타내는 차단된 큐가 있습니다. 네트워크 또는 인프라 문제로 인해 과도한 항목이 큐에 올라가 시스템 성능에 부정적인 영향을 줄 수 있는 경우가 많습니다.

>[!Note]
>
>MBean 및 URL 매개 변수의 경우 모니터링할 복제 에이전트의 `<AGENT_NAME>` 이름으로 대체합니다.

세션 카운터

* MBean: `org.apache.jackrabbit.oak:id=7,name="OakRepository Statistics",type="RepositoryStats"`
* URL: */system/console/jmx/org.apache.jackrabbit.oak:id=7,name=&quot;OakRepository Statistics&quot;,type*=&quot;RepositoryStats&quot;
* 인스턴스:모든 서버
* 경고 임계값:열려 있는 세션이 기준선을 50% 이상 초과하는 경우
* 경고 정의:세션은 코드 일부를 통해 열 수 있으며 닫히지 않습니다. 이것은 시간이 지남에 따라 천천히 발생할 수 있으며 결국 시스템의 메모리 누수를 일으킬 수 있습니다. 시스템에서 세션 수가 변동해야 하지만 지속적으로 증가해서는 안 됩니다.

상태 검사

작업 대시보드에서 [](/help/sites-administering/operations-dashboard.md#health-reports) 사용할 수 있는 상태 확인에는 모니터링에 해당하는 JMX MBeans가 있습니다. 그러나 사용자 정의 상태 검사를 작성하여 추가 시스템 통계를 표시할 수 있습니다.

다음은 모니터링에 유용한 몇 가지 기본 상태 확인입니다.

* 시스템 확인
   * MBean: `org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * 인스턴스:작성자 1명, 모든 게시 서버
   * 경고 임계값:상태가 좋지 않을 때
   * 경고 정의:지표 중 하나의 상태는 WARN 또는 CRITICAL입니다. 문제의 원인에 대한 자세한 내용은 log 속성을 확인하십시오.

* 복제 큐

   * MBean: `org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck `
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * 인스턴스:작성자 1명, 모든 게시 서버
   * 경고 임계값:상태가 좋지 않을 때
   * 경고 정의:지표 중 하나의 상태는 WARN 또는 CRITICAL입니다. 문제를 일으킨 큐에 대한 자세한 내용은 로그 속성을 확인하십시오.

* 응답 성능

   * MBean: `org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * 인스턴스:모든 서버
   * 경고 지속 시간:상태가 좋지 않을 때
   * 경고 정의:지표 중 하나의 상태는 WARN 또는 CRITICAL 상태입니다. 문제를 일으킨 큐에 대한 자세한 내용은 로그 속성을 확인하십시오.

* 쿼리 성능

   * MBean: `org.apache.sling.healthcheck:name=queriesStatus,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name= queriesStatus,type=HealthCheck`
   * 인스턴스:작성자 1명, 모든 게시 서버
   * 경고 임계값:상태가 좋지 않을 때
   * 경고 정의:시스템에서 하나 이상의 쿼리가 느리게 실행됩니다. 문제를 일으킨 쿼리에 대한 자세한 내용은 log 속성을 확인하십시오.

* 활성 상태 번들

   * MBean: `org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * 인스턴스:모든 서버
   * 경고 임계값:상태가 좋지 않을 때
   * 경고 정의:시스템에 비활성 또는 해결되지 않은 OSGi 번들이 있습니다. 문제를 일으킨 번들에 대한 자세한 내용은 log 속성을 확인하십시오.

* 오류 로그

   * MBean: `org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * 인스턴스:모든 서버
   * 경고 임계값:상태가 좋지 않을 때
   * 경고 정의:로그 파일에 오류가 있습니다. 문제의 원인에 대한 자세한 내용은 log 속성을 확인하십시오.

## 일반적인 문제 및 해결 방법 {#common-issues-and-resolutions}

모니터링 과정에서 문제가 발생하면 [!DNL Experience Manager] 배포 관련 일반적인 문제를 해결하기 위해 수행할 수 있는 몇 가지 문제 해결 작업이 있습니다.

* TarMK를 사용하는 경우 Tar 컴포지션을 자주 실행합니다. 자세한 내용은 저장소 [관리를](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)참조하십시오.
* 로그를 `OutOfMemoryError` 확인합니다. 자세한 내용은 메모리 문제 [분석을](https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html)참조하십시오.

* 인덱스되지 않은 쿼리, 트리 탐색 또는 색인 탐색에 대한 참조가 있는지 로그를 확인합니다. 이 항목은 인덱싱되지 않은 쿼리 또는 불충분한 인덱싱된 쿼리를 나타냅니다. 쿼리 및 인덱싱 성능 최적화에 대한 우수 사례는 쿼리 및 [색인화에](/help/sites-deploying/best-practices-for-queries-and-indexing.md)대한 우수 사례를 참조하십시오.
* 워크플로우 콘솔을 사용하여 워크플로우가 예상대로 작동하는지 확인합니다. 가능하면 여러 워크플로우를 하나의 워크플로우로 통합합니다.
* 실시간 모니터링을 다시 방문하여 추가 병목 현상 또는 특정 리소스의 높은 소비자에 대해 살펴봅니다.
* 클라이언트 네트워크의 송신 지점 및 디스패처를 포함한 배포 네트워크의 수신 지점을 [!DNL Experience Manager] 조사합니다. 이러한 경우가 종종 병목 영역입니다. 자세한 내용은 자산 [네트워크 고려 사항을](/help/assets/assets-network-considerations.md)참조하십시오.
* 서버 크기 [!DNL Experience Manager] 상향 조정 배포 크기가 적절하지 않을 수 [!DNL Experience Manager] 있습니다. Adobe 고객 지원 센터는 서버 크기가 작은지 여부를 확인하는 데 도움이 됩니다.
* 문제가 발생했을 때 `access.log` 및 `error.log` 파일에서 항목을 검사합니다. 사용자 지정 코드 예외 항목을 나타낼 수 있는 패턴을 찾습니다. 모니터링하는 이벤트 목록에 추가합니다.
