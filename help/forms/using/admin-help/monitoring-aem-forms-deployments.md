---
title: AEM Forms 배포 모니터링
seo-title: AEM Forms 배포 모니터링
description: 시스템 수준과 내부 수준 모두에서 AEM Forms 배포를 모니터링할 수 있습니다. 이 문서에서 AEM Forms 배포 모니터링에 대해 자세히 알아보십시오.
seo-description: 시스템 수준과 내부 수준 모두에서 AEM Forms 배포를 모니터링할 수 있습니다. 이 문서에서 AEM Forms 배포 모니터링에 대해 자세히 알아보십시오.
uuid: 032b7a93-3069-4ad5-a8c6-4c160f290669
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b3e7bca0-5aaf-4f28-bddb-fd7e8ed72ee8
exl-id: 931e8095-5c7c-4c1f-b95b-75ac2827d4f3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---

# AEM Forms 배포 모니터링 {#monitoring-aem-forms-deployments}

시스템 수준과 내부 수준 모두에서 AEM Forms 배포를 모니터링할 수 있습니다. HP OpenView, IBM Tivoli, CA UniCenter와 같은 전문가 관리 도구와 *JConsole*&#x200B;이라는 타사 JMX 모니터를 사용하여 Java 활동을 특별히 모니터링할 수 있습니다. 모니터링 전략을 구현하면 AEM Forms 배포의 가용성, 안정성 및 성능이 향상됩니다.

AEM Forms 배포 모니터링에 대한 자세한 내용은 [AEM Forms 배포를 모니터링하기 위한 기술 안내서](https://www.adobe.com/devnet/livecycle/pdfs/lc_monitoring_wp_ue.pdf)를 참조하십시오.

## MBeans {#monitoring-using-mbeans} 를 사용하여 모니터링

AEM Forms에서는 탐색 및 통계 정보를 제공하는 두 개의 등록된 MBeans를 제공합니다. 통합 및 검사를 위해 지원되는 유일한 MBeans입니다.

* **ServiceStatistics:**  이 MBean은 서비스 이름 및 해당 버전에 대한 정보를 제공합니다.
* **작업 통계:** 이 MBean은 모든 Forms 서버의 서비스 통계를 제공합니다. 여기에서 관리자는 호출 시간, 오류 수 등과 같은 특정 서비스에 대한 정보를 얻을 수 있습니다.

### ServiceStatisticsMbean 공용 인터페이스 {#servicestatisticmbean-public-interfaces}

ServiceStatistics MBean의 이러한 공용 인터페이스는 테스트 목적으로 액세스할 수 있습니다.

```java
 public String getServiceId();
 public int getMajorVersion();
 public int getMinorVersion();
```

### OperationStatisticsMbean 공용 인터페이스 {#operationstatisticmbean-public-interfaces}

OperationStatistic MBean의 이러한 공용 인터페이스는 테스트 목적으로 액세스할 수 있습니다.

```java
 // InvocationCount: The number of times the method is invoked.
 public long getInvocationCount();
 // InvocationStartTime: The time at which the method started to execute.
 public long getInvocationStartTime();
 // InvocationEndTime: The time at which the method finished execution.
 public long getInvocationEndTime();
 // InvocationTime: The time taken for the execution of the method.
 public long getInvocationTime();
 // LastSamplingDateTime: Convert InvocationStartTime to a formatted string
 public String getLastSamplingDateTime();
 // MaxInvocationTime: The maximum time taken for the execution of the method.
 public long getMaxInvocationTime();
 // MinInvocationTime: The minimum time taken for the execution of the method.
 public long getMinInvocationTime();
 // AverageInvocationTime: the averege execution time taken for the execution of the method.
 public double getAverageInvocationTime();
 // ExceptionCount: The number of times the method has thrown an Exception.
 public long getExceptionCount();
 // ExceptionMessage: The message of the last exception occurred.
 public String getExeptionMessage();
 public void setExceptionMessage(String errorMessage);
```

### MBean 트리 및 작업 통계 {#mbean-tree-operation-statistics}

JMX 콘솔(JConsole)을 사용하여 OperationStatistics MBean의 통계를 사용할 수 있습니다. 이러한 통계는 MBean의 속성이며 다음 계층 트리 아래에서 탐색할 수 있습니다.

**MBean 트리**

**Adobe 도메인 이름:** 애플리케이션 서버에 따라 다릅니다. Application Server에서 도메인을 정의하지 않으면 기본값은 adobe.com입니다.

**ServiceType:** AdobeService는 모든 서비스를 나열하는 데 사용되는 이름입니다.

**AdobeServiceName:**  서비스 이름 또는 서비스 ID입니다.

**버전:** 서비스 버전입니다.

**작업 통계**

**호출 시간:**  메서드 실행에 걸리는 시간입니다. 요청이 직렬화되거나, 클라이언트에서 서버로 전송되거나, 역직렬화되는 시간은 포함되지 않습니다.

**호출 수:** 서비스가 호출된 횟수입니다.

**평균 호출 시간:**  서버가 시작된 후 실행된 모든 호출의 평균 시간입니다.

**최대 호출 시간:**  서버가 시작된 후 실행된 가장 긴 호출의 기간입니다.

**최소 호출 시간:**  서버가 시작된 후 실행된 가장 짧은 호출의 기간입니다.

**예외 수:** 실패의 원인이 된 호출 수입니다.

**예외 메시지:**  발생한 마지막 예외의 오류 메시지입니다.

**마지막 샘플링 날짜 시간:**  마지막 호출의 날짜입니다.

**시간 단위:** 기본값은 밀리초입니다.

JMX 모니터링을 사용하려면 일반적으로 애플리케이션 서버에 몇 가지 구성이 필요합니다. 세부 사항은 애플리케이션 서버 설명서 를 참조하십시오.

### 열린 JMX 액세스 {#examples-of-how-to-set-up-open-jmx-access} 설정 방법의 예

**JBoss 4.0.3/4.2.0 - JVM 시작 구성**

JConsole에서 MBeans를 보려면 JBoss 애플리케이션 서버의 JVM 시작 매개변수를 구성합니다. JBoss가 run.bat/sh 파일에서 시작되었는지 확인합니다.

1. InstallJBoss/bin 아래에 있는 run.bat 파일을 편집합니다.
1. JAVA_OPTS 줄을 찾아 다음을 추가합니다.

   ```shell
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

**WebLogic 9.2 /10 - JVM 시작 구성**

1. `[WebLogic home]/user_projects/domains/Adobe_Live_Cycle/bin` 아래에 있는 startWebLogic.bat 파일을 편집합니다.
1. JAVA_OPTS 줄을 찾아 다음을 추가합니다.

   ```shell
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

1. WebLogic을 다시 시작합니다.

>[!NOTE]
>
>WebLogic의 경우 원격 또는 IIOP를 사용하여 MBean에 액세스할 수 있습니다.

**원격으로 MBean 액세스**

1. 새 연결을 위해 JConsole을 실행하고 원격 탭을 클릭합니다.
1. 호스트 이름 및 포트(9088, JVM 시작 옵션 중 지정한 숫자)를 입력합니다.

**Websphere 6.1 - JVM 시작 구성**

1. 관리 콘솔(애플리케이션 서버 > 서버1 > 프로세스 정의 > JVM)에서 일반 JVM 인수의 필드에 다음 라인을 추가합니다.

   ```shell
    -Djavax.management.builder.initial= -Dcom.sun.management.jmxremote
   ```

1. /opt/IBM/WebSphere/AppServer/java/jre/lib/management/management.properties 파일(또는 &lt;Your Websphere JRE>/ lib/management/management.properties)에 다음 세 줄을 추가하거나 주석 처리를 취소합니다.

   ```shell
    com.sun.management.jmxremote.port=9999 //any port you like, but make sure you use this port when you connect
    com.sun.management.jmxremote.authenticate=false
    com.sun.management.jmxremote.ssl=false
   ```

1. WebSphere를 다시 시작합니다.
