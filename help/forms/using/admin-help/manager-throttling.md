---
title: 작업 관리자 및 제한
description: 이 문서에서는 작업 관리자에 대한 배경 정보와 작업 관리자 제한 옵션을 구성하는 방법에 대한 지침을 제공합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1f765de2-1362-4318-9302-c5036e6fa7d6
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '1042'
ht-degree: 100%

---

# 작업 관리자 및 제한{#work-manager-and-throttling}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

AEM Forms(및 이전 버전)는 JMS 대기열을 사용하여 작업을 비동기적으로 실행했습니다. AEM Forms에서는 JMS 대기열이 작업 관리자로 대체되었습니다. 이 문서에서는 작업 관리자에 대한 배경 정보와 작업 관리자 제한 옵션을 구성하는 방법에 대한 지침을 제공합니다.

## 장기(비동기) 작업 정보 {#about-long-lived-asynchronous-operations}

AEM Forms에서 서비스가 수행하는 작업은 단기(동기) 작업이거나 장기(비동기) 작업일 수 있습니다. 단기 작업은 호출된 동일한 스레드에서 동기적으로 완료됩니다. 해당 작업은 계속 진행하기 전에 응답을 기다립니다.

장기 작업은 여러 시스템에 걸쳐 이루어지거나 조직 외부로까지 확대될 수 있습니다. 예를 들어 고객이 여러 자동화 작업과 인력 작업을 통합하는 대규모 솔루션의 일부로 대출 신청서를 작성하고 제출해야 하는 경우가 있습니다. 이러한 작업은 응답을 기다리는 동안에도 계속 진행되어야 합니다. 장기 작업은 기본 작업을 비동기적으로 수행하므로 완료될 때까지 기다리는 동안 리소스를 다른 작업에 활용할 수 있도록 합니다. 작업 관리자는 단기 작업과 달리 장기 작업을 호출한 후에는 해당 작업이 완료된 것으로 간주하지 않습니다. 동일한 서비스에서 다른 작업을 요청하는 시스템이나 양식을 제출하는 사용자와 같은 외부 트리거가 발생해야 해당 작업이 완료됩니다.

## 작업 관리자 정보 {#about-work-manager}

AEM Forms(및 이전 버전)는 JMS 대기열을 사용하여 작업을 비동기적으로 실행했습니다. AEM Forms는 작업 관리자를 사용하여 관리되는 스레드를 통해 비동기 작업을 예약하고 실행합니다.

비동기 작업은 다음과 같은 방식으로 처리됩니다.

1. 작업 관리자가 실행할 작업 항목을 받습니다.
1. 작업 관리자가 작업 항목을 데이터베이스 테이블에 저장하고 작업 항목에 고유 식별자를 할당합니다. 데이터베이스 레코드에는 작업 항목을 실행하는 데 필요한 모든 정보가 포함되어 있습니다.
1. 작업 관리자 스레드가 유휴 상태가 되면 해당 스레드에서 작업 항목을 가져옵니다. 작업 항목을 가져오기 전에 스레드는 필요한 서비스가 시작되었는지, 다음 작업 항목을 가져오기에 충분한 힙 크기가 있는지, 작업 항목을 처리하기에 충분한 CPU 주기가 있는지 여부를 확인할 수 있습니다. 작업 관리자는 작업 항목 실행을 예약할 때 해당 작업 항목의 속성(예: 우선순위)도 평가합니다.

AEM Forms 관리자는 상태 모니터를 사용하여 대기열에 있는 작업 항목 수 및 해당 상태와 같은 작업 관리자 통계를 확인할 수 있습니다. 상태 모니터를 사용하여 작업 항목을 일시 중지하거나, 다시 시작하거나, 재시도하거나, 삭제할 수도 있습니다. ([작업 관리자와 관련된 통계 보기](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager)를 참조하십시오.)

## 작업 관리자 제한 옵션 구성 {#configuring-work-manager-throttling-options}

작업 관리자에 대한 제한을 구성하여 충분한 메모리 리소스를 사용할 수 있을 때만 작업 항목이 예약되도록 할 수 있습니다. 애플리케이션 서버에서 다음과 같은 JVM 옵션을 설정하여 제한을 구성합니다.

<table>
 <thead>
  <tr>
   <th><p>속성</p></th>
   <th><p>설명</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><code> adobe.work-manager.queue-refill-interval</code></td>
   <td><p>작업 관리자가 대기열에 새 항목이 있는지 확인할 때 사용하는 시간 간격(밀리초)을 지정합니다.</p><p>이 옵션의 값은 정수입니다. 기본값은 <code>1000</code>밀리초(1초)입니다. </p><p>비동기 호출 볼륨이 적으면 이 값을 높일 수 있습니다. 예를 들어 2,000~5,000(2~5초)으로 높일 수 있습니다. </p><p>비동기 호출 볼륨이 많으면 기본값으로도 충분하지만, 필요한 경우 더 낮은 값을 사용할 수 있습니다. 이 값을 너무 많이 낮추면(예를 들어 50 미만으로 낮추면 초당 20회의 폴링 빈도가 됨) 시스템에 상당한 오버헤드가 발생합니다.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.debug-mode-enabled</code></td>
   <td><p>디버그 모드를 활성화하려면 이 옵션을 <code>true</code>로 설정하고 비활성화하려면 false로 설정합니다. </p><p>디버그 모드에서는 작업 관리자 정책 위반 및 작업 관리자 일시 중지/다시 시작 작업과 관련된 메시지가 기록됩니다. 문제 해결 시에만 이 옵션을 true로 설정합니다.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.enabled</code></td>
   <td><p>아래 설명된 메모리 제어 설정에 따라 제한을 활성화하려면 이 옵션을 <code>true</code>로 설정하고 제한을 비활성화하려면 <code>false</code>로 설정합니다.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.high-limit</code></td>
   <td><p>작업 관리자가 수신 작업을 제한하기 전에 사용할 수 있는 최대 메모리 비율을 지정합니다.</p><p>이 옵션의 기본값은 <code>95</code>입니다. 이 값은 대부분의 시스템에 적합합니다. 시스템이 최대 용량까지 작동해야 하는 경우에만 이 값을 높이십시오. 하지만 이 값을 높일수록 메모리 부족 문제가 발생할 위험도 커집니다.</p><p>클러스터링된 환경에서 AEM Forms를 실행하는 경우 클러스터의 각 노드에서 메모리 제어 제한 설정을 서로 다르게 지정하는 것이 좋습니다. 예를 들어 로드 밸런서에 대화형 작업을 위해 프로그래밍된 노드 A와 B에 상한을 더 낮게 설정할 수 있습니다. 로드 밸런서에서 사용되지 않고 비동기 작업에 예약된 노드 C와 D에 상한을 더 높게 설정할 수도 있습니다.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.low-limit</code></td>
   <td><p>작업 관리자가 수신 작업 제한을 중지하기 전에 사용할 수 있는 최대 메모리 비율을 지정합니다.</p><p>이 옵션의 기본값은 <code>20</code>입니다. 이 값은 대부분의 시스템에 적합합니다.</p></td>
  </tr>
  <tr>
   <td><code>Dadobe.workmanager.allocate.max-batch-size</code></td>
   <td><p>WorkManager의 최대 배치 크기를 지정합니다. 기본 배치 크기는 10입니다.</p><p>작업이 완료된 후에도 WorkManager의 프로세스 상태가 업데이트되지 않으면 배치 크기를 1로 설정합니다.</p></td>
  </tr>
 </tbody>
</table>

**JBoss에 Java 옵션 추가**

1. JBoss Application Server를 중지합니다.
1. 편집기에서 *[appserver root]*/bin/run.bat(Windows) 또는 run.sh(Linux 또는 UNIX)를 열고 필요에 따라 Java 옵션을 `-Dproperty=value` 형식으로 추가합니다.
1. 서버를 다시 시작합니다.

**WebLogic에 Java 옵션 추가**

1. 웹 브라우저에 `https://[host name]:[port]/console`을 입력하여 WebLogic 관리 콘솔을 시작합니다.
1. WebLogic Server 도메인에 대해 만든 사용자 이름 및 암호를 입력하고 로그인을 클릭한 후 변경 센터에서 잠금 및 편집을 클릭합니다.
1. 도메인 구조에서 환경 > 서버를 클릭하고 오른쪽 창에서 관리 서버 이름을 클릭합니다.
1. 다음 화면에서 구성 탭 > 서버 시작 탭을 클릭합니다.
1. 인수 상자에서 현재 콘텐츠의 끝에 필요한 인수를 추가합니다. 예를 들어 상태 모니터를 비활성화하려면 다음을 추가합니다.

   `-Dadobe.healthmonitor.enabled=false`는 상태 모니터를 비활성화합니다.

1. 저장을 클릭한 후 변경 사항 활성화를 클릭합니다.
1. WebLogic 관리 서버를 다시 시작합니다.

**WebSphere에 Java 옵션 추가**

1. WebSphere 관리 콘솔 탐색 트리에서 서버 > 서버 유형 > WebSphere Application Server를 클릭합니다.
1. 오른쪽 창에서 서버 이름을 클릭합니다.
1. 서버 인프라에서 Java를 클릭하고 Forms Workflow > 프로세스 정의를 클릭합니다.
1. 추가 속성에서 Java 가상 머신을 클릭합니다.
1. 일반 JVM 인수 상자에 필요한 인수를 입력합니다.
1. 확인 또는 적용을 클릭한 후 마스터 구성에 직접 저장을 클릭합니다.
