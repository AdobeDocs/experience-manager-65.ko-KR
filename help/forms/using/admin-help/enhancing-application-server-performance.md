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
translation-type: tm+mt
source-git-commit: a26bc4e4ea10370dd2fc3403500004b9e378c418

---


# 애플리케이션 서버 성능 향상{#enhancing-application-server-performance}

이 컨텐츠는 AEM Forms 응용 프로그램 서버의 성능을 개선하기 위해 구성할 수 있는 선택적 설정에 대해 설명합니다.

## 응용 프로그램 서버 데이터 소스 구성 {#configuring-application-server-data-sources}

AEM 양식은 AEM 양식 저장소를 데이터 소스로 사용합니다. AEM Forms 리포지토리는 애플리케이션 자산을 저장하고 런타임 시 서비스는 자동화된 비즈니스 프로세스를 완료하는 과정에서 저장소에서 자산을 검색할 수 있습니다.

실행 중인 AEM 양식 모듈 수와 애플리케이션에 액세스하는 동시 사용자 수에 따라 데이터 소스에 대한 액세스가 중요할 수 있습니다. 연결 풀링을 사용하여 데이터 소스 액세스를 최적화할 수 있습니다. *연결 풀링은* 응용 프로그램 또는 서버 개체가 데이터베이스에 액세스해야 할 때마다 새 데이터베이스 연결을 만드는 오버헤드를 방지하는 데 사용되는 기술입니다. 연결 풀링은 일반적으로 웹 기반 및 엔터프라이즈 애플리케이션에서 사용되며, 애플리케이션 서버에 의해 처리되지만 이에 국한되지 않습니다.

연결 풀 매개 변수를 올바르게 구성해야 연결이 부족하지 않으므로 응용 프로그램 성능이 저하될 수 있습니다.

연결 풀 설정을 제대로 구성하려면 애플리케이션 서버 관리자가 하루 중 피크 시간 동안 연결 풀을 모니터링해야 합니다. 모니터링은 애플리케이션과 사용자에게 항상 충분한 연결을 제공할 수 있도록 합니다. 대부분의 애플리케이션 서버에는 모니터링 도구가 포함되어 있습니다.

WebLogic Server 관리 콘솔을 사용하여 도메인의 각 JDBC 데이터 소스 인스턴스에 대한 다양한 통계를 모니터링할 수 있습니다. 자세한 내용은 WebLogic 설명서를 참조하십시오.

응용 프로그램 서버 관리자가 올바른 연결 풀 설정을 결정하면 해당 사용자는 이 정보를 데이터베이스 관리자에게 전달해야 합니다. 데이터베이스 연결 수는 데이터 소스의 연결 풀에 있는 연결 수와 같기 때문에 데이터베이스 관리자는 이 정보가 필요합니다. 그런 다음 아래 설명된 대로 응용 프로그램 서버 및 데이터 소스 유형에 대한 연결 풀 설정을 구성하는 단계를 완료합니다.

### Oracle 및 MySQL용 WebLogic에 대한 연결 풀 설정 구성 {#configure-connection-pool-settings-for-weblogic-for-oracle-and-mysql}

1. 도메인 구조에서 서비스 > JDBC > 데이터 소스를 클릭하고 오른쪽 창에서 IDP_DS를 클릭합니다.
1. 다음 화면에서 구성 > 연결 풀 탭을 클릭하고 다음 상자에 값을 입력합니다.

   * 초기 용량
   * 최대 용량
   * 용량 증가
   * 문 캐시 크기

1. 저장을 클릭한 다음 변경 내용 활성화를 클릭합니다.
1. WebLogic 관리 서버를 다시 시작합니다.

### SQLServer용 WebLogic의 연결 풀 설정 구성 {#configure-connection-pool-settings-for-weblogic-for-sqlserver}

1. 변경 센터에서 잠금 및 편집을 클릭합니다.
1. 도메인 구조에서 서비스 > JDBC > 데이터 소스를 클릭하고 오른쪽 창에서 EDC_DS를 클릭합니다.
1. 다음 화면에서 구성 > 연결 풀 탭을 클릭하고 다음 상자에 값을 입력합니다.

   * 초기 용량
   * 최대 용량
   * 용량 증가
   * 문 캐시 크기

1. 저장을 클릭한 다음 변경 내용 활성화를 클릭합니다.
1. WebLogic 관리 서버를 다시 시작합니다.

### DB2용 WebSphere에 대한 연결 풀 설정 구성 {#configure-connection-pool-settings-for-websphere-for-db2}

1. 탐색 트리에서 리소스 > JDBC > JDBC 공급자를 클릭합니다. 오른쪽 창에서 만든 데이터 소스(DB2 Universal JDBC 드라이버 공급자 또는 LiveCycle - db2 - IDP_DS)를 클릭합니다.
1. 추가 속성에서 데이터 소스를 클릭한 다음 IDP_DS를 선택합니다.
1. 다음 화면의 추가 속성에서 연결 풀 속성을 클릭하고 최대 연결 상자 및 최소 연결 상자에 값을 입력합니다.
1. 확인 또는 적용을 클릭한 다음 마스터 구성에 직접 저장을 클릭합니다.

### Oracle용 WebSphere 접속 풀 설정 구성 {#configure-connection-pool-settings-for-websphere-for-oracle}

1. 탐색 트리에서 리소스 > JDBC > JDBC 공급자를 클릭합니다. 오른쪽 창에서 생성한 Oracle JDBC 드라이버 데이터 소스를 누릅니다.
1. 추가 속성에서 데이터 소스를 클릭한 다음 IDP_DS를 선택합니다.
1. 다음 화면의 추가 속성에서 연결 풀 속성을 클릭하고 최대 연결 상자 및 최소 연결 상자에 값을 입력합니다.
1. 확인 또는 적용을 클릭한 다음 마스터 구성에 직접 저장을 클릭합니다.

### SqlServer용 WebSphere 연결 풀 설정 구성 {#configure-connection-pool-settings-for-websphere-for-sqlserver}

1. 탐색 트리에서 [리소스] > [JDBC] > [JDBC 공급자]를 클릭하고 오른쪽 창에서 생성한 사용자 정의 JDBC 드라이버 데이터 소스를 클릭합니다.
1. 추가 속성에서 데이터 소스를 클릭한 다음 IDP_DS를 선택합니다.
1. 다음 화면의 추가 속성에서 연결 풀 속성을 클릭하고 최대 연결 상자 및 최소 연결 상자에 값을 입력합니다.
1. 확인 또는 적용을 클릭한 다음 마스터 구성에 직접 저장을 클릭합니다.

## 인라인 문서 최적화 및 JVM 메모리에 미치는 영향 {#optimizing-inline-documents-and-impact-on-jvm-memory}

일반적으로 비교적 작은 크기의 문서를 처리하는 경우 문서 전송 속도 및 저장 공간과 관련된 성능을 향상시킬 수 있습니다. 이렇게 하려면 다음 AEM 양식 제품 구성을 구현합니다.

* AEM 양식의 기본 문서 최대 인라인 크기를 늘려서 대부분의 문서 크기보다 큽니다.
* 대용량 파일을 처리하려면 고속 디스크 시스템 또는 RAM 디스크에 있는 저장소 디렉토리를 지정하십시오.

관리 콘솔에서 최대 인라인 크기 및 저장소 디렉터리(AEM 양식 임시 파일 디렉토리 및 GDS 디렉토리)가 구성됩니다.

### 문서 크기 및 최대 인라인 크기 {#document-size-and-maximum-inline-size}

AEM 양식에 의해 처리되도록 전송된 문서가 기본 문서 최대 인라인 크기보다 작거나 같으면 문서는 서버 인라인에 저장되고 문서는 Adobe 문서 개체로 직렬화됩니다. 문서 인라인으로 저장할 경우 상당한 성능 이점을 얻을 수 있습니다. 그러나 양식 워크플로우를 사용하는 경우 추적 목적으로 데이터베이스에 컨텐츠를 저장할 수도 있습니다. 따라서 최대 인라인 크기를 늘리면 데이터베이스 크기에 영향을 줄 수 있습니다.

최대 인라인 크기보다 큰 문서는 로컬 파일 시스템에 저장됩니다. 서버와 서버로부터 전송된 Adobe 문서 객체는 해당 파일에 대한 포인터만 나타냅니다.

문서 컨텐츠가 인라인(최대 인라인 크기보다 작음)되면 컨텐츠는 문서 직렬화 페이로드의 일부로 데이터베이스에 저장됩니다. 따라서 최대 인라인 크기를 늘리면 데이터베이스 크기에 영향을 줄 수 있습니다.

**최대 인라인 크기 변경**

1. 관리 콘솔에서 설정 > 핵심 시스템 설정 > 구성을 클릭합니다.
1. [기본 문서 최대 인라인 크기] 상자에 값을 입력하고 [확인]을 클릭합니다.

   >[!NOTE]
   >
   >문서 최대 인라인 크기 속성 값은 JEE 환경의 AEM Forms와 OSGi 번들에 포함된 AEM Forms의 AEM Forms에 대해 동일해야 합니다. 이 단계는 JEE 환경의 AEM Forms에만 업데이트되었으며 OSGi 번들의 AEM Forms에는 JEE 파섹 환경에 포함된 AEM Forms에 대해서는 업데이트되지 않았습니다.

1. 다음 시스템 속성을 사용하여 응용 프로그램 서버를 다시 시작합니다.

   com.adobe.idp.defaultDocumentMaxInlineSize=`[value specified in Step 2]`

   >[!NOTE]
   >
   >위에서 언급한 시스템 속성은 JEE 환경의 AEM Forms에 대해 설정된 문서 최대 인라인 크기 속성 값을 재정의하고 OSGi 번들의 AEM Forms에는 JEE 환경에 포함된 AEM Forms가 있습니다.

>[!NOTE]
>
>기본 최대 인라인 크기는 65536바이트입니다.

### JVM 최대 더미 크기 {#jvm-maximum-heap-size}

최대 인라인 크기를 늘리면 직렬화된 문서를 저장하는 데 더 많은 메모리가 필요합니다. 따라서 일반적으로 JVM 최대 더미 크기를 늘려야 합니다.

많은 문서를 처리하는 많은 로드된 시스템에서 JVM 더미 메모리를 빠르게 채울 수 있습니다. OutOfMemoryError를 방지하려면 JVM 최대 더미 크기를 인라인 문서의 크기에 해당하는 양과 지정된 시간에 일반적으로 실행되는 문서 수를 곱합니다.

JVM 최대 더미 크기 증가 = (인라인 문서 크기) x (처리된 평균 문서 수).

**JVM 최대 더미 크기 계산**

이 예에서는 현재 JVM 최대 힙이 512MB로 설정되고 최대 인라인 크기는 64KB입니다. 10개의 작업이 동시에 실행되고 각 작업에 9개의 입력 파일과 1개의 결과 파일이 있는 시나리오에 대해 서버를 구성해야 합니다(작업당 총 10개의 파일과 동시에 처리된 100개의 파일). 모든 파일의 크기는 512KB 미만입니다.

모든 파일을 인라인으로 저장하려면 최대 인라인 크기를 최소 512KB로 설정합니다.

JVM 최대 더미 크기의 필수 증가 값은 다음 방정식을 사용하여 계산됩니다.

(512KB) x (100) = 51200KB 또는 50MB

JVM 최대 더미 크기는 총 562MB에 대해 50MB까지 증가해야 합니다.

**더미 조각화 고려**

인라인 문서의 크기를 큰 값으로 설정하면 더미 조각화가 발생하기 쉬운 시스템에서 OutOfMemoryError의 위험이 높아집니다. 문서 인라인을 저장하려면 JVM 더미 메모리의 연속 공간이 충분해야 합니다. 일부 운영 체제, JVM 및 가비지 수집 알고리즘은 단편화되어 있기 쉽습니다. 조각화는 인접한 더미 공간의 양을 감소시키고 충분한 사용 가능한 총 공간이 있어도 OutOfMemoryError를 초래할 수 있습니다.

예를 들어 애플리케이션 서버에서 이전 작업을 수행하면 JVM 힙이 조각화된 상태로 남아 있고 가비지 수집기는 힙을 충분히 압축하여 사용 가능한 큰 블록을 복구할 수 없습니다. JVM 최대 더미 크기가 최대 인라인 크기 증가를 위해 조정되었더라도 OutOfMemoryError가 발생할 수 있습니다.

더미 조각화를 고려하려면 인라인 문서 크기가 전체 더미 크기의 0.1%보다 높게 설정되어서는 안 됩니다. 예를 들어 JVM 최대 더미 크기 512MB는 최대 인라인 크기 512MB x 0.001 = 0.512MB 또는 512KB를 지원할 수 있습니다.

## 향상된 WebSphere 애플리케이션 서버 {#websphere-application-server-enhancements}

이 섹션에서는 WebSphere 응용 프로그램 서버 환경에 대한 설정에 대해 설명합니다.

### JVM에 할당된 최대 메모리 증가 {#increasing-the-maximum-memory-allocated-to-the-jvm}

Configuration Manager를 실행 중이거나 명령줄 유틸리티 *ebdeploy를 사용하여 EJB(Enterprise JavaBeans)를 생성하려고 할 때 OutOfMemory 오류가 발생하면 JVM에 할당된 메모리 양을 늘립니다* .

1. appserver root/deploytool/ *[itp/ 디렉토리에서 ejbdeploy]*&#x200B;스크립트를 편집합니다.

   * (Windows) `ejbdeploy.bat`
   * (Linux 및 UNIX) `ejbdeploy.sh`

1. 매개 변수를 `-Xmx256M` 찾아 더 높은 값(예: `-Xmx1024M`)으로 변경합니다.
1. 파일을 저장합니다.
1. Configuration Manager를 사용하여 `ejbdeploy` 명령을 실행하거나 재배포합니다.

## LDAP를 사용하여 Windows Server 2003 성능 향상 {#improving-windows-server-2003-performance-with-ldap}

이 콘텐트는 Microsoft Windows Server 2003 운영 체제 환경에 대한 설정에 대해 설명합니다.

검색 연결에서 연결 풀링을 사용하면 필요한 포트 수를 최대 50%까지 줄일 수 있습니다. 이는 해당 연결이 항상 지정된 도메인에 대해 동일한 자격 증명을 사용하고 컨텍스트 및 관련 개체가 명시적으로 닫히기 때문입니다.

### 연결 풀링을 위한 Windows Server 구성 {#configure-your-windows-server-for-connection-pooling}

1. 시작 > 실행을 클릭하여 레지스트리 편집기를 시작하고 열기 상자에 `regedit` 입력하고 확인을 클릭합니다.
1. 레지스트리 키로 이동 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters`
1. 레지스트리 편집기의 오른쪽 창에서 TcpTimedWaitDelay 값 이름을 찾습니다. 이름이 나타나지 않으면 메뉴 모음에서 편집 > 새로 만들기 > DWORD 값을 선택하여 이름을 추가합니다.
1. 이름 상자에 `TcpTimedWaitDelay`

   >[!NOTE]
   >
   >깜박이는 커서가 표시되지 않고 상자 `New Value #` 안에 있는 경우 오른쪽 패널 내부를 마우스 오른쪽 단추로 클릭하고 이름 바꾸기를 선택한 다음 이름 상자에 `TcpTimedWaitDelay`*입력합니다.*

1. 값 이름 MaxUserPort, MaxHashTableSize 및 MaxFreeTcbs에 대해 4단계를 반복합니다.
1. 오른쪽 창 내부를 두 번 클릭하여 TcpTimedWaitDelay 값을 설정합니다. [기준]에서 [십진수]를 선택하고 [값] 상자에 입력합니다 `30`.
1. 오른쪽 창 내부를 두 번 클릭하여 MaxUserPort 값을 설정합니다. [기준]에서 [십진수]를 선택하고 [값] 상자에 입력합니다 `65534`.
1. 오른쪽 창 내부를 두 번 클릭하여 MaxHashTableSize 값을 설정합니다. [기준]에서 [십진수]를 선택하고 [값] 상자에 입력합니다 `65536`.
1. 오른쪽 창 내부를 두 번 클릭하여 MaxFreeTcbs 값을 설정합니다. [기준]에서 [십진수]를 선택하고 [값] 상자에 입력합니다 `16000`.

>[!NOTE]
>
>레지스트리 편집기를 사용하거나 다른 방법을 사용하여 레지스트리를 잘못 수정하는 경우 심각한 문제가 발생할 수 있습니다. 이러한 문제는 운영 체제를 다시 설치해야 할 수 있습니다. 위험을 감수하고 레지스트리를 수정합니다.

