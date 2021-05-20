---
title: 상태 모니터 성능 미세 조정
seo-title: 상태 모니터 성능 미세 조정
description: 상태 모니터 성능 세부 조정 방법 알아보기
seo-description: 상태 모니터 성능 세부 조정 방법 알아보기
uuid: 770b10cb-065f-41b5-9594-a291e4311151
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b8f8bddc-0d38-4d5e-b33f-978f04bc16c6
exl-id: 41042e08-5e14-4809-89b7-16d98a72d1b4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 1%

---

# 상태 모니터 성능 미세 조정{#fine-tuning-health-monitor-performance}

상태 모니터를 채우는 시스템 통계를 수집하면 AEM Forms 환경의 성능에 일부 영향을 줍니다. 이 영향은 애플리케이션 서버에서 아래 나열된 Java 옵션을 설정하여 제어할 수 있습니다.

<table>
 <thead>
  <tr>
   <th><p>속성</p></th>
   <th><p>목적</p></th>
   <th><p>기본값</p></th>
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
   <td><p>상태 모니터 스레드가 통계를 수집하는 간격(밀리초)입니다</p></td>
   <td><p>10분(60만 밀리초)</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.multicast-port</p></td>
   <td><p>분산 시스템의 다른 구성원과 통신하는 데 사용되는 멀티캐스트 포트입니다. 0으로 설정하면 멤버 검색 및 배포 모두에 대해 멀티캐스트를 사용할 수 없습니다. </p><p>참고:서로 다른 분산 시스템에 대해 서로 다른 멀티캐스트 주소와 포트를 선택하십시오. 다른 주소만 사용하지 마십시오.</p></td>
   <td><p>기본값이 없습니다. 유효한 값의 범위는 0~65535.</p></td>
  </tr>
  <tr>
   <td><p>통계-샘플-비율</p></td>
   <td><p>통계가 샘플링되는 비율(밀리초)입니다. 운영 체제 통계는 샘플을 가져올 때만 업데이트됩니다.</p></td>
   <td><p>600000</p></td>
  </tr>
  <tr>
   <td><p>adobe.workmanager.healthmonitor.enabled</p></td>
   <td><p>이 등록 정보는 작업 또는 작업 항목 수와 같은 Work Manager 통계 수집을 활성화하거나 비활성화합니다.</p></td>
   <td><p>true</p></td>
  </tr>
 </tbody>
</table>

## JBoss {#add-java-options-to-jboss}에 Java 옵션 추가

1. JBoss 애플리케이션 서버를 중지합니다.
1. 편집기에서 *[appserver root]*/bin/run.bat (Windows) 또는 run.sh(Linux 또는 UNIX)를 열고 필요에 따라 Java 옵션을 추가합니다.
1. 서버를 다시 시작합니다.

## WebLogic {#add-java-options-to-weblogic}에 Java 옵션 추가

1. 웹 브라우저의 URL 행에 https://[호스트 이름]:&#39;port&#39;/console을 입력하여 WebLogic 관리 콘솔을 시작합니다.
1. WebLogic Server 도메인에 대해 만든 사용자 이름과 암호를 입력하고 변경 센터에서 로그를 클릭한 다음 잠금 및 편집을 클릭합니다.
1. 도메인 구조에서 환경 > 서버 를 클릭하고 오른쪽 창에서 관리 서버 이름을 클릭합니다.
1. 다음 화면에서 구성 탭 > 서버 시작 탭을 클릭합니다.
1. 인수 상자에서 현재 컨텐츠의 끝에 필요한 인수를 추가합니다. 예를 들어, 추가 - `Dadobe.healthmonitor.enabled=false` 는 상태 모니터를 비활성화합니다.
1. 저장 을 클릭한 다음 변경 사항 활성화 를 클릭합니다.
1. WebLogic 관리 서버를 다시 시작합니다.

## WebSphere {#add-java-options-to-websphere}에 Java 옵션 추가

1. WebSphere 관리 콘솔 탐색 트리에서 응용 프로그램 서버에 대해 다음을 수행합니다.

   (WebSphere 6.x) Server > Application Server 를 클릭합니다.

   (WebSphere 7.x) Server > Server Types > WebSphere Application Server 클릭

1. 오른쪽 창에서 서버 이름을 클릭합니다.
1. 서버 인프라에서 Java 및 양식 워크플로우 > 프로세스 정의를 클릭합니다.
1. 추가 속성에서 Java 가상 컴퓨터를 클릭합니다.
1. 일반 JVM 인수 상자에 필요한 인수를 입력합니다.
1. 확인 또는 적용을 클릭한 다음 마스터 구성에 직접 저장을 클릭합니다.
