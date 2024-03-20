---
title: 작업 관리자 및 제한
description: 이 문서에서는 Work Manager에 대한 배경 정보와 Work Manager 전송률 조절 옵션 구성에 대한 지침을 제공합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1f765de2-1362-4318-9302-c5036e6fa7d6
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1030'
ht-degree: 0%

---

# 작업 관리자 및 제한{#work-manager-and-throttling}

AEM forms(및 이전 버전)에서는 JMS 대기열을 사용하여 작업을 비동기적으로 실행했습니다. AEM Forms에서 JMS 대기열이 Work Manager로 대체되었습니다. 이 문서에서는 Work Manager에 대한 배경 정보와 Work Manager 전송률 조절 옵션 구성에 대한 지침을 제공합니다.

## 장기(비동기) 작업 기본 정보 {#about-long-lived-asynchronous-operations}

AEM Forms에서 서비스에 의해 수행되는 작업은 단기(동기) 또는 장기(비동기)일 수 있습니다. 단기 작업은 호출된 스레드와 동일한 스레드에서 동기적으로 완료됩니다. 이러한 작업은 계속하기 전에 응답을 기다립니다.

오랜 기간 동안 운영되는 운영은 시스템에 걸쳐 있거나, 고객이 여러 자동화 및 인적 작업을 통합하는 대규모 솔루션의 일부로 대출 신청서를 작성 및 제출해야 하는 경우와 같이 조직 범위를 넘어서까지 확장될 수 있습니다. 이러한 작업은 응답을 기다리는 동안 계속되어야 합니다. 장기 작업은 기본 작업을 비동기적으로 수행하므로 완료 대기 중에 리소스를 다른 방식으로 사용할 수 있습니다. Work Manager는 단기 작업과 달리 장기 작업이 호출되면 완료된 것으로 간주하지 않습니다. 작업을 완료하려면 동일한 서비스에서 다른 작업을 요청하는 시스템이나 양식을 제출하는 사용자와 같은 외부 트리거가 발생해야 합니다.

## 작업 관리자 정보 {#about-work-manager}

AEM forms(및 이전 버전)에서는 JMS 대기열을 사용하여 작업을 비동기적으로 실행했습니다. AEM forms는 작업 관리자를 사용하여 관리되는 스레드를 통해 비동기 작업을 예약하고 실행합니다.

비동기 작업은 다음 방식으로 처리됩니다.

1. Work Manager는 실행할 작업 항목을 수신합니다.
1. 작업 관리자는 작업 항목을 데이터베이스 테이블에 저장하고 작업 항목에 고유 식별자를 지정합니다. 데이터베이스 레코드에는 작업 항목을 실행하는 데 필요한 모든 정보가 들어 있습니다.
1. 스레드가 비어 있으면 Work Manager 스레드가 작업 항목을 가져옵니다. 작업 항목을 가져오기 전에 스레드는 필요한 서비스가 시작되었는지, 다음 작업 항목을 가져올 수 있는 힙 크기가 충분한지, 작업 항목을 처리할 수 있는 CPU 주기가 충분한지 여부를 확인할 수 있습니다. 또한 Work Manager는 작업 항목의 실행을 예약할 때 작업 항목의 속성(예: 우선 순위)을 평가합니다.

AEM forms 관리자는 상태 모니터를 사용하여 대기열의 작업 항목 수 및 상태 등 작업 관리자 통계를 확인할 수 있습니다. 상태 모니터를 사용하여 작업 항목을 일시 중지, 다시 시작, 다시 시도 또는 삭제할 수도 있습니다. (참조: [Work Manager 관련 통계 보기](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager).)

## Work Manager 전송률 조절 옵션 구성 {#configuring-work-manager-throttling-options}

사용 가능한 메모리 리소스가 충분한 경우에만 작업 항목이 예약되도록 작업 관리자에 대한 제한을 구성할 수 있습니다. 애플리케이션 서버에서 다음 JVM 옵션을 설정하여 제한을 구성합니다.

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
   <td><p>Work Manager가 대기열에서 새 항목을 확인할 때 사용하는 시간 간격(밀리초)을 지정합니다.</p><p>이 옵션의 값은 정수입니다. 기본값은 입니다. <code>1000</code> 밀리초(1초). </p><p>비동기 호출의 볼륨이 낮으면 이 값을 높일 수 있습니다. 예를 들어 2000과 5000 사이의 값(2~5초)으로 늘릴 수 있습니다. </p><p>비동기 호출량이 많은 경우 기본값이 충분해야 하지만 필요한 경우 더 낮은 값을 사용할 수 있습니다. 이 값을 너무 많이 낮추면(예: 초당 20회의 폴링 빈도가 발생하는 50 이하) 시스템에 상당한 오버헤드가 발생합니다.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.debug-mode-enabled</code></td>
   <td><p>이 옵션을 다음으로 설정 <code>true</code> 디버그 모드를 활성화하려면 false를 사용하고 비활성화하려면 false를 사용합니다. </p><p>디버그 모드에서는 작업 관리자 정책 위반 및 작업 관리자 일시 중지/다시 시작 작업에 대한 메시지가 기록됩니다. 문제 해결 시에만 이 옵션을 true로 설정하십시오.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.enabled</code></td>
   <td><p>이 옵션을 다음으로 설정 <code>true</code> 아래 설명된 메모리 제어 설정에 따라 전송률 조절 기능을 활성화하려면 다음을 수행합니다. <code>false</code> 전송률 조절을 비활성화합니다.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.high-limit</code></td>
   <td><p>Work Manager가 수신 작업을 제한하기 전에 사용할 수 있는 최대 메모리 비율을 지정합니다.</p><p>이 옵션의 기본값은 입니다. <code>95</code>. 이 값은 대부분의 시스템에 적합합니다. 시스템이 최대 용량까지 확장해야 하는 경우에만 확장하십시오. 그러나 이 값을 늘리면 메모리 부족 문제의 위험도 증가합니다.</p><p>클러스터된 환경에서 AEM Forms를 실행하는 경우 클러스터의 여러 노드에서 메모리 제어 제한 설정을 다르게 설정할 수 있습니다. 예를 들어 대화형 작업을 위해 로드 밸런서에 프로그래밍된 노드 A와 B에 대한 상한이 낮아질 수 있습니다. 또한 로드 밸런서에서 사용되지 않고 비동기 작업을 위해 예약된 노드 C 및 D에 높은 제한을 설정할 수 있습니다.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.low-limit</code></td>
   <td><p>Work Manager가 들어오는 작업의 제한을 중지하기 전에 사용할 수 있는 최대 메모리 비율을 지정합니다.</p><p>이 옵션의 기본값은 입니다. <code>20</code>. 이 값은 대부분의 시스템에 적합합니다.</p></td>
  </tr>
  <tr>
   <td><code>Dadobe.workmanager.allocate.max-batch-size</code></td>
   <td><p>workmanager의 최대 배치 크기를 지정합니다. 기본 배치 크기는 10입니다.</p><p>작업이 완료된 후에도 작업 관리자의 프로세스 상태가 업데이트되지 않으면 배치 크기를 1로 설정합니다.</p></td>
  </tr>
 </tbody>
</table>

**JBoss에 Java 옵션 추가**

1. JBoss 애플리케이션 서버를 중지합니다.
1. 를 엽니다. *[appserver 루트]*&#x200B;편집기에서 /bin/run.bat (Windows) 또는 run.sh (Linux 또는 UNIX) 를 실행하고 필요에 따라 형식으로 Java 옵션을 추가합니다. `-Dproperty=value`.
1. 서버를 다시 시작합니다.

**WebLogic에 Java 옵션 추가**

1. 다음을 입력하여 WebLogic 관리 콘솔을 시작합니다. `https://[host name]:[port]/console` 웹 브라우저에서.
1. WebLogic Server 도메인에 대해 생성한 사용자 이름과 암호를 입력하고 Log(로그) 를 클릭합니다. Change Center(변경 센터)에서 Lock &amp; Edit(잠금 및 편집)를 클릭합니다.
1. 도메인 구조에서 환경 > 서버 를 클릭하고 오른쪽 창에서 관리 대상 서버 이름을 클릭합니다.
1. 다음 화면에서 구성 탭 > 서버 시작 탭을 클릭합니다.
1. 인수 상자에서 현재 컨텐츠의 끝에 필요한 인수를 추가합니다. 예를 들어 상태 모니터를 비활성화하려면 다음을 추가합니다.

   `-Dadobe.healthmonitor.enabled=false` 상태 모니터를 사용하지 않도록 설정합니다.

1. 저장 을 클릭한 다음 변경 내용 활성화 를 클릭합니다.
1. WebLogic 관리 서버를 다시 시작합니다.

**WebSphere에 Java 옵션 추가**

1. WebSphere 관리 콘솔 탐색 트리에서 서버 > 서버 유형 > WebSphere 애플리케이션 서버를 클릭합니다.
1. 오른쪽 창에서 서버 이름을 클릭합니다.
1. 서버 인프라에서 Java and forms workflow > Process Definition을 클릭합니다.
1. 추가 속성에서 Java Virtual Machine을 클릭합니다.
1. 일반 JVM 인수 상자에 필요한 인수를 입력합니다.
1. 확인 또는 적용을 클릭한 다음 마스터 구성에 직접 저장을 클릭합니다.
