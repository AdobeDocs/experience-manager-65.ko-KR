---
title: 애플리케이션 서버 성능 향상
seo-title: 애플리케이션 서버 성능 향상
description: 이 문서에서는 AEM Forms 응용 프로그램 서버의 성능을 개선하기 위해 구성할 수 있는 선택적 설정에 대해 설명합니다.
seo-description: 이 문서에서는 AEM Forms 응용 프로그램 서버의 성능을 개선하기 위해 구성할 수 있는 선택적 설정에 대해 설명합니다.
uuid: 88d2f96a-3b59-410d-8160-20581d27acad
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fad65765-d56d-4a9f-82d5-bcceb1758953
exl-id: 6e2f3d4c-2ead-45b3-98e7-32cacc7e2985
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1886'
ht-degree: 0%

---

# 응용 프로그램 서버 성능 개선{#enhancing-application-server-performance}

이 컨텐츠는 AEM Forms 응용 프로그램 서버의 성능을 개선하기 위해 구성할 수 있는 선택 사항에 대해 설명합니다.

## 응용 프로그램 서버 데이터 소스 구성 {#configuring-application-server-data-sources}

AEM forms에서는 AEM Forms 저장소를 데이터 소스로 사용합니다. AEM Forms 저장소는 애플리케이션 자산을 저장하고, 런타임에 서비스는 자동화된 비즈니스 프로세스를 완료하는 일부로 저장소에서 자산을 검색할 수 있습니다.

실행 중인 AEM Forms 모듈 수와 애플리케이션에 액세스하는 동시 사용자 수에 따라 데이터 소스에 대한 액세스가 중요할 수 있습니다. 연결 풀링을 사용하여 데이터 소스 액세스를 최적화할 수 있습니다. *연결* 풀링은 응용 프로그램 또는 서버 개체가 데이터베이스에 액세스해야 할 때마다 새 데이터베이스 연결을 만드는 오버헤드를 방지하기 위해 사용되는 기술입니다. 연결 풀링은 일반적으로 웹 기반 및 엔터프라이즈 응용 프로그램에서 사용되며, 애플리케이션 서버에서 처리되지만, 이에 국한되지 않습니다.

연결 풀 매개 변수를 올바르게 구성해야 연결이 부족하지 않아 응용 프로그램 성능이 저하될 수 있습니다.

연결 풀 설정을 제대로 구성하려면 응용 프로그램 서버 관리자가 하루 중 최대 시간 동안 연결 풀을 모니터링하는 것이 중요합니다. 모니터링하면 응용 프로그램 및 사용자가 항상 충분한 연결을 사용할 수 있습니다. 대부분의 애플리케이션 서버에는 모니터링 도구가 포함되어 있습니다.

WebLogic Server 관리 콘솔을 사용하여 도메인의 각 JDBC 데이터 소스 인스턴스에 대한 다양한 통계를 모니터링할 수 있습니다. 자세한 내용은 WebLogic 설명서 를 참조하십시오.

응용 프로그램 서버 관리자가 올바른 연결 풀 설정을 결정하면 해당 사용자는 이 정보를 데이터베이스 관리자에게 전달해야 합니다. 데이터베이스 연결 수가 데이터 원본에 대한 연결 풀의 연결 수와 같기 때문에 데이터베이스 관리자에게 이 정보가 필요합니다. 그런 다음 아래 설명된 대로 애플리케이션 서버와 데이터 소스 유형에 대한 연결 풀 설정을 구성하는 단계를 완료합니다.

### oracle 및 MySQL {#configure-connection-pool-settings-for-weblogic-for-oracle-and-mysql}에 대한 WebLogic에 대한 연결 풀 설정을 구성합니다.

1. 도메인 구조에서 서비스 > JDBC > 데이터 소스를 클릭하고 오른쪽 창에서 IDP_DS를 클릭합니다.
1. 다음 화면에서 구성 > 연결 풀 탭을 클릭하고 다음 상자에 값을 입력합니다.

   * 초기 용량
   * 최대 용량
   * 용량 증가
   * 문 캐시 크기

1. 저장 을 클릭한 다음 변경 사항 활성화 를 클릭합니다.
1. WebLogic 관리 서버를 다시 시작합니다.

### SQLServer {#configure-connection-pool-settings-for-weblogic-for-sqlserver}에 대한 WebLogic에 대한 연결 풀 설정을 구성합니다.

1. 변경 센터에서 잠금 및 편집을 클릭합니다.
1. 도메인 구조에서 서비스 > JDBC > 데이터 소스를 누르고 오른쪽 창에서 EDC_DS를 누릅니다.
1. 다음 화면에서 구성 > 연결 풀 탭을 클릭하고 다음 상자에 값을 입력합니다.

   * 초기 용량
   * 최대 용량
   * 용량 증가
   * 문 캐시 크기

1. 저장 을 클릭한 다음 변경 사항 활성화 를 클릭합니다.
1. WebLogic 관리 서버를 다시 시작합니다.

### DB2용 WebSphere {#configure-connection-pool-settings-for-websphere-for-db2}에 대한 연결 풀 설정을 구성합니다.

1. 탐색 트리에서 리소스 > JDBC > JDBC 공급자를 클릭합니다. 오른쪽 창에서 생성한 데이터 소스를 클릭합니다. DB2 Universal JDBC Driver Provider 또는 LiveCycle - db2 - IDP_DS입니다.
1. 추가 속성에서 데이터 소스를 클릭한 다음 IDP_DS를 선택합니다.
1. 다음 화면의 추가 속성에서 연결 풀 등록 정보를 클릭하고 최대 연결 상자 및 최소 연결 상자에 값을 입력합니다.
1. 확인 또는 적용 을 클릭한 다음 직접 저장을 클릭하여 기본 구성을 선택합니다.

### oracle {#configure-connection-pool-settings-for-websphere-for-oracle}에 대한 WebSphere 연결 풀 설정을 구성합니다.

1. 탐색 트리에서 리소스 > JDBC > JDBC 공급자를 클릭합니다. 오른쪽 창에서 생성한 Oracle JDBC 드라이버 데이터 소스를 누릅니다.
1. 추가 속성에서 데이터 소스를 클릭한 다음 IDP_DS를 선택합니다.
1. 다음 화면의 추가 속성에서 연결 풀 등록 정보를 클릭하고 최대 연결 상자 및 최소 연결 상자에 값을 입력합니다.
1. 확인 또는 적용 을 클릭한 다음 직접 저장을 클릭하여 기본 구성을 선택합니다.

### SqlServer {#configure-connection-pool-settings-for-websphere-for-sqlserver}에 대한 WebSphere 연결 풀 설정을 구성합니다.

1. 탐색 트리에서 [리소스] > [JDBC] > [JDBC 제공자]를 클릭하고 오른쪽 창에서 생성한 사용자 정의 JDBC 드라이버 데이터 소스를 누릅니다.
1. 추가 속성에서 데이터 소스를 클릭한 다음 IDP_DS를 선택합니다.
1. 다음 화면의 추가 속성에서 연결 풀 등록 정보를 클릭하고 최대 연결 상자 및 최소 연결 상자에 값을 입력합니다.
1. 확인 또는 적용 을 클릭한 다음 직접 저장을 클릭하여 기본 구성을 선택합니다.

## 인라인 문서 최적화 및 JVM 메모리에 미치는 영향 {#optimizing-inline-documents-and-impact-on-jvm-memory}

일반적으로 상대적으로 작은 크기의 문서를 처리하는 경우 문서 전송 속도 및 저장 공간과 관련된 성능을 향상시킬 수 있습니다. 이렇게 하려면 다음 AEM Forms 제품 구성을 구현하십시오.

* AEM Forms의 기본 문서 최대 인라인 크기를 늘려서 대부분의 문서 크기보다 크게 합니다.
* 대용량 파일을 처리하려면 고속 디스크 시스템 또는 RAM 디스크에 있는 스토리지 디렉토리를 지정하십시오.

최대 인라인 크기 및 저장소 디렉토리(AEM Forms 임시 파일 디렉토리 및 GDS 디렉토리)는 관리 콘솔에 구성됩니다.

### 문서 크기 및 최대 인라인 크기 {#document-size-and-maximum-inline-size}

AEM Forms에서 처리하기 위해 전송되는 문서가 기본 문서 최대 인라인 크기보다 작거나 같으면 문서는 서버 인라인에 저장되고 문서는 Adobe 문서 객체로 일련화됩니다. 문서 인라인으로 저장하면 성능이 크게 향상됩니다. 그러나 양식 워크플로우를 사용하는 경우 컨텐츠를 추적하기 위해 데이터베이스에 저장할 수도 있습니다. 따라서 최대 인라인 크기를 늘리면 데이터베이스 크기에 영향을 줄 수 있습니다.

최대 인라인 크기보다 큰 문서는 로컬 파일 시스템에 저장됩니다. 서버 및 서버 간에 전송되는 Adobe 문서 객체는 해당 파일에 대한 포인터만 갖습니다.

문서 컨텐츠가 인라인(최대 인라인 크기보다 작음)되면 컨텐츠가 문서의 직렬화 페이로드의 일부로 데이터베이스에 저장됩니다. 따라서 최대 인라인 크기를 늘리면 데이터베이스 크기에 영향을 줄 수 있습니다.

**최대 인라인 크기 변경**

1. 관리 콘솔에서 설정 > 핵심 시스템 설정 > 구성을 클릭합니다.
1. 기본 문서 최대 인라인 크기 상자에 값을 입력하고 확인을 클릭합니다.

   >[!NOTE]
   >
   >문서 최대 인라인 크기 속성 값은 JEE 환경의 AEM Forms에 대해 동일해야 하며 JEE 환경의 AEM Forms에 포함된 OSGi 번들의 AEM Forms에도 동일해야 합니다. 이 단계는 JEE 환경의 AEM Forms에 대해서만 값을 업데이트하며, OSGi 번들의 AEM Forms에 대해서는 JEE 환경의 AEM Forms에 포함되지 않습니다.

1. 다음 시스템 속성을 사용하여 응용 프로그램 서버를 다시 시작합니다.

   com.adobe.idp.defaultDocumentMaxInlineSize=`[value specified in Step 2]`

   >[!NOTE]
   >
   >위에 언급된 시스템 속성은 JEE 환경의 AEM Forms에 대해 설정된 문서 최대 인라인 크기 속성 값을 재정의하고, JEE 환경의 AEM Forms에 포함된 OSGi 번들에 있는 AEM Forms을 재정의합니다.

>[!NOTE]
>
>기본 최대 인라인 크기는 65536 바이트입니다.

### JVM 최대 heap 크기 {#jvm-maximum-heap-size}

최대 인라인 크기를 늘리면 직렬화된 문서를 저장하기 위한 메모리가 더 필요합니다. 따라서 일반적으로 JVM 최대 heap 크기를 늘려야 합니다.

많은 문서를 처리하는 로드된 시스템에서는 JVM heap 메모리를 빠르게 채울 수 있습니다. OutOfMemoryError를 방지하려면 JVM 최대 heap 크기를 인라인 문서의 크기에 해당하는 양과 일반적으로 지정된 시간에 실행되는 문서 수를 곱한 값으로 늘립니다.

JVM 최대 heap 크기 증가 = (인라인 문서 크기) x (처리된 평균 문서 수).

**JVM 최대 heap 크기 계산**

이 예에서 현재 JVM 최대 힙은 512MB로 설정되고 최대 인라인 크기는 64KB입니다. 서버는 10개의 작업이 동시에 실행되는 시나리오에 대해 구성해야 하며, 각 작업에는 9개의 입력 파일과 1개의 결과 파일(작업당 총 10개의 파일 및 100개의 파일이 동시에 처리됨)이 있습니다. 모든 파일의 크기는 512KB 미만입니다.

모든 파일을 인라인으로 저장하려면 최대 인라인 크기를 최소 512KB로 설정하십시오.

다음 방정식을 사용하여 JVM 최대 heap 크기의 필수 증가가 계산됩니다.

(512KB) x (100) = 51200 KB 또는 50MB

JVM 최대 heap 크기는 총 562MB의 경우 50MB까지 증가해야 합니다.

**힙조각화 고려**

인라인 문서의 크기를 큰 값으로 설정하면 heap 단편화가 발생할 수 있는 시스템에서 OutOfMemoryError가 발생할 수 있습니다. 문서를 인라인으로 저장하려면 JVM heap 메모리의 연속 공간이 충분해야 합니다. 일부 운영 체제, JVM 및 가비지 수집 알고리즘에서는 heap 단편화가 발생하기 쉽습니다. 단편화는 연속적인 힙의 크기를 줄이며 충분한 사용 가능한 공간이 존재하는 경우에도 OutOfMemoryError가 발생할 수 있습니다.

예를 들어, 애플리케이션 서버의 이전 작업에서 JVM 힙이 단편화된 상태로 남아 있고 가비지 수집기는 힙을 충분히 압축하여 사용 가능한 많은 공간을 다시 확보할 수 없습니다. 최대 인라인 크기 증가를 위해 JVM 최대 heap 크기를 조정했지만 OutOfMemoryError가 발생할 수 있습니다.

heap 단편화를 고려하려면 인라인 문서 크기를 총 heap 크기의 0.1%보다 높게 설정해서는 안 됩니다. 예를 들어, JVM 최대 힙크기 512MB는 512MB x 0.001 = 0.512MB 또는 512KB의 최대 인라인 크기를 지원할 수 있습니다.

## WebSphere 응용 프로그램 서버 개선 사항 {#websphere-application-server-enhancements}

이 섹션에서는 WebSphere Application Server 환경에 대한 설정을 설명합니다.

### JVM {#increasing-the-maximum-memory-allocated-to-the-jvm}에 할당된 최대 메모리 증가

구성 관리자를 실행 중이거나 명령줄 유틸리티 *ejbdeploy* 를 사용하여 EJB(Enterprise JavaBeans) 배포 코드를 생성하려고 할 경우 OutOfMemory 오류가 발생하면 JVM에 할당된 메모리 양을 늘립니다.

1. *[appserver root]*/deploytool/itp/ 디렉토리에서 ejbdeploy 스크립트를 편집합니다.

   * (Windows) `ejbdeploy.bat`
   * (Linux 및 UNIX) `ejbdeploy.sh`

1. `-Xmx256M` 매개 변수를 찾아 `-Xmx1024M` 같은 더 높은 값으로 변경합니다.
1. 파일을 저장합니다.
1. `ejbdeploy` 명령을 실행하거나 구성 관리자를 사용하여 재배포합니다.

## LDAP {#improving-windows-server-2003-performance-with-ldap}을 사용하여 Windows Server 2003 성능 개선

이 내용은 Microsoft Windows Server 2003 운영 체제 환경에 대한 설정을 설명합니다.

검색 연결에서 연결 풀링을 사용하면 필요한 포트 수가 최대 50%까지 줄어들 수 있습니다. 이 문제는 연결이 지정된 도메인에 대해 항상 동일한 자격 증명을 사용하고 컨텍스트 및 관련 개체가 명시적으로 닫히기 때문입니다.

### 연결 풀링을 위한 Windows Server 구성 {#configure-your-windows-server-for-connection-pooling}

1. 시작 > 실행 을 클릭하여 레지스트리 편집기를 시작하고 열기 상자에 `regedit` 을 입력하고 확인 을 클릭합니다.
1. 레지스트리 키 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters` 로 이동합니다.
1. 레지스트리 편집기의 오른쪽 창에서 TcpTimedWaitDelay 값 이름을 찾습니다. 이름이 나타나지 않으면 메뉴 막대에서 [편집] > [새로 만들기] > [DWORD 값]을 선택하여 이름을 추가합니다.
1. 이름 상자에 `TcpTimedWaitDelay` 을 입력합니다

   >[!NOTE]
   >
   >깜박이는 커서와 상자 내에 `New Value #`이 표시되지 않으면 오른쪽 패널 내부를 마우스 오른쪽 단추로 클릭하고 이름 바꾸기를 선택한 다음 이름 상자에 `TcpTimedWaitDelay`*.*

1. 값 이름 MaxUserPort, MaxHashTableSize 및 MaxFreeTcbs에 대해 4단계를 반복합니다.
1. 오른쪽 창 내부를 두 번 클릭하여 TcpTimedWaitDelay 값을 설정합니다. 기본(Base)에서 소수점(Decimal)을 선택하고 값(Value) 상자에 `30` 을 입력합니다.
1. 오른쪽 창 내부를 두 번 클릭하여 MaxUserPort 값을 설정합니다. 기본(Base)에서 소수점(Decimal)을 선택하고 값(Value) 상자에 `65534` 을 입력합니다.
1. 오른쪽 창 내부를 두 번 클릭하여 MaxHashTableSize 값을 설정합니다. 기본(Base)에서 소수점(Decimal)을 선택하고 값(Value) 상자에 `65536` 을 입력합니다.
1. 오른쪽 창 내부를 두 번 클릭하여 MaxFreeTcbs 값을 설정합니다. 기본(Base)에서 소수점(Decimal)을 선택하고 값(Value) 상자에 `16000` 을 입력합니다.

>[!NOTE]
>
>레지스트리 편집기를 사용하거나 다른 방법을 사용하여 레지스트리를 잘못 수정하는 경우 심각한 문제가 발생할 수 있습니다. 이러한 문제는 운영 체제를 다시 설치해야 할 수 있습니다. 위험이 있을 경우 레지스트리를 수정합니다.
