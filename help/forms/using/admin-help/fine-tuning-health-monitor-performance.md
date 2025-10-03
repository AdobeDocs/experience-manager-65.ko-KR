---
title: 상태 모니터 성능 세부 조정
description: 상태 모니터 성능을 세부 조정하는 방법을 알아봅니다. Java 설정 옵션을 사용하여 Forms 환경 성능에 영향을 미치는 시스템 통계를 제어합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 41042e08-5e14-4809-89b7-16d98a72d1b4
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '426'
ht-degree: 100%

---

# 상태 모니터 성능 세부 조정{#fine-tuning-health-monitor-performance}

상태 모니터에 채워지는 시스템 통계를 수집하는 작업은 AEM Forms 환경 성능에 어느 정도 영향을 미칩니다. 이러한 영향은 애플리케이션 서버에서 아래에 나열된 Java 옵션을 설정하여 제어할 수 있습니다.

<table>
 <thead>
  <tr>
   <th><p>속성</p></th>
   <th><p>목적</p></th>
   <th><p>기본 값</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>adobe.healthmonitor.enabled</p></td>
   <td><p>상태 모니터 스레드 켜기 또는 끄기</p></td>
   <td><p>true</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.statistics-enabled</p></td>
   <td><p>Gemfire 캐싱 켜기 또는 끄기</p></td>
   <td><p>true</p></td>
  </tr>
  <tr>
   <td><p>adobe.healthmonitor.refresh-interval</p></td>
   <td><p>상태 모니터 스레드가 통계를 수집하는 간격(밀리초)</p></td>
   <td><p>10분(600,000밀리초)</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.multicast-port</p></td>
   <td><p>분산 시스템의 다른 멤버와 통신하는 데 사용되는 멀티캐스트 포트입니다. 0으로 설정하면 멤버 검색 및 분산 모두에서 멀티캐스트가 비활성화됩니다. </p><p>참고: 분산 시스템마다 서로 다른 멀티캐스트 주소 및 포트를 선택하십시오. 서로 다른 주소만 사용하지 마십시오.</p></td>
   <td><p>기본값은 없습니다. 유효한 값의 범위는 0~65535입니다.</p></td>
  </tr>
  <tr>
   <td><p>statistic-sample-rate</p></td>
   <td><p>통계를 샘플링하는 속도(밀리초)입니다. 운영 체제 통계는 샘플을 가져올 때만 업데이트됩니다.</p></td>
   <td><p>600000</p></td>
  </tr>
  <tr>
   <td><p>adobe.workmanager.healthmonitor.enabled</p></td>
   <td><p>이 속성은 작업 또는 작업 항목 수와 같은 작업 관리자 통계 수집을 활성화하거나 비활성화합니다.</p></td>
   <td><p>true</p></td>
  </tr>
 </tbody>
</table>

## JBoss에 Java 옵션 추가 {#add-java-options-to-jboss}

1. JBoss Application Server를 중지합니다.
1. 편집기에서 *[appserver root]*/bin/run.bat(Windows) 또는 run.sh(Linux 또는 UNIX)를 열고 필요에 따라 Java 옵션을 추가합니다.
1. 서버를 다시 시작합니다.

## WebLogic에 Java 옵션 추가 {#add-java-options-to-weblogic}

1. 웹 브라우저의 URL 줄에 https://[host name]:&#39;port&#39;/console을 입력하여 WebLogic 관리 콘솔을 시작합니다.
1. WebLogic Server 도메인에 대해 만든 사용자 이름 및 암호를 입력하고 로그인을 클릭한 후 변경 센터에서 잠금 및 편집을 클릭합니다.
1. 도메인 구조에서 환경 > 서버를 클릭하고 오른쪽 창에서 관리 서버 이름을 클릭합니다.
1. 다음 화면에서 구성 탭 > 서버 시작 탭을 클릭합니다.
1. 인수 상자에서 현재 콘텐츠의 끝에 필요한 인수를 추가합니다. 예를 들어 - `Dadobe.healthmonitor.enabled=false`를 추가하면 상태 모니터가 비활성화됩니다.
1. 저장을 클릭한 후 변경 사항 활성화를 클릭합니다.
1. WebLogic 관리 서버를 다시 시작합니다.

## WebSphere에 Java 옵션 추가 {#add-java-options-to-websphere}

1. WebSphere 관리 콘솔 탐색 트리에서 애플리케이션 서버에 대해 다음 작업을 수행합니다.

   (WebSphere 6.x) 서버 > 애플리케이션 서버를 클릭합니다.

   (WebSphere 7.x) 서버 > 서버 유형 > WebSphere Application Server를 클릭합니다.

1. 오른쪽 창에서 서버 이름을 클릭합니다.
1. 서버 인프라에서 Java를 클릭하고 Forms Workflow > 프로세스 정의를 클릭합니다.
1. 추가 속성에서 Java 가상 머신을 클릭합니다.
1. 일반 JVM 인수 상자에 필요한 인수를 입력합니다.
1. 확인 또는 적용을 클릭한 후 마스터 구성에 직접 저장을 클릭합니다.
