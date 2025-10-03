---
title: 애플리케이션 서버 성능 향상
description: 이 문서에서는 AEM Forms 애플리케이션 서버 성능을 향상하기 위해 구성할 수 있는 옵션 설정을 설명합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6e2f3d4c-2ead-45b3-98e7-32cacc7e2985
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '1882'
ht-degree: 100%

---

# 애플리케이션 서버 성능 향상{#enhancing-application-server-performance}

이 콘텐츠에서는 AEM Forms 애플리케이션 서버 성능을 향상하기 위해 구성할 수 있는 옵션 설정을 설명합니다.

## 애플리케이션 서버 데이터 소스 구성 {#configuring-application-server-data-sources}

AEM Forms는 AEM Forms 저장소를 데이터 소스로 사용합니다. AEM Forms 저장소는 애플리케이션 자산을 저장하고 런타임 시 서비스는 자동화된 비즈니스 프로세스를 완료하기 위한 작업의 일부로 저장소에서 자산을 가져올 수 있습니다.

데이터 소스에 대한 액세스는 실행 중인 AEM Forms 모듈 수와 애플리케이션에 동시에 액세스하는 사용자 수에 따라 중요할 수 있습니다. 연결 풀링을 사용하여 데이터 소스 액세스를 최적화할 수 있습니다. *연결 풀링*&#x200B;은 애플리케이션이나 서버 오브젝트가 데이터베이스에 액세스해야 할 때마다 새로운 데이터베이스 연결을 만드는 오버헤드를 피하기 위해 사용되는 기술입니다. 연결 풀링은 일반적으로 웹 기반 및 엔터프라이즈 애플리케이션에서 사용되며 보통 애플리케이션 서버에서 처리되지만 이에 국한되지는 않습니다.

연결 풀 매개변수를 올바르게 구성하는 것은 연결이 부족해지지 않도록 하는 데 중요하며, 연결이 부족할 경우 애플리케이션 성능이 저하될 수 있습니다.

연결 풀 설정을 올바르게 구성하려면 애플리케이션 서버 관리자가 하루 중 사용량이 가장 많은 시간에 연결 풀을 모니터링하는 것이 중요합니다. 모니터링을 통해 애플리케이션과 사용자에게 항상 충분한 연결이 제공되는지 확인합니다. 대부분의 애플리케이션 서버에는 모니터링 도구가 포함되어 있습니다.

WebLogic Server 관리 콘솔을 사용하면 도메인에 있는 각 JDBC 데이터 소스 인스턴스에 대한 다양한 통계를 모니터링할 수 있습니다. 자세한 내용은 WebLogic 설명서를 참조하십시오.

애플리케이션 서버 관리자가 올바른 연결 풀 설정을 결정하면 이 정보를 데이터베이스 관리자에게 전달해야 합니다. 데이터베이스 관리자에게 해당 정보가 필요한 이유는 데이터베이스 연결 수가 데이터 소스의 연결 풀에 있는 연결 수와 같기 때문입니다. 그런 다음, 아래 설명된 대로 애플리케이션 서버와 데이터 소스 유형에 대해 연결 풀 설정을 구성하는 단계를 완료합니다.

### Oracle 및 MySQL용 WebLogic에 대한 연결 풀 설정 구성 {#configure-connection-pool-settings-for-weblogic-for-oracle-and-mysql}

1. 도메인 구조에서 서비스 > JDBC > 데이터 소스를 클릭하고 오른쪽 창에서 IDP_DS를 클릭합니다.
1. 다음 화면에서 구성 > 연결 풀 탭을 클릭하고 다음 상자에 값을 입력합니다.

   * 초기 용량
   * 최대 용량
   * 용량 증분
   * 문 캐시 크기

1. 저장을 클릭한 후 변경 사항 활성화를 클릭합니다.
1. WebLogic 관리 서버를 다시 시작합니다.

### SQLServer용 WebLogic에 대한 연결 풀 설정 구성 {#configure-connection-pool-settings-for-weblogic-for-sqlserver}

1. 변경 센터에서 잠금 및 편집을 클릭합니다.
1. 도메인 구조에서 서비스 > JDBC > 데이터 소스를 클릭하고 오른쪽 창에서 EDC_DS를 클릭합니다.
1. 다음 화면에서 구성 > 연결 풀 탭을 클릭하고 다음 상자에 값을 입력합니다.

   * 초기 용량
   * 최대 용량
   * 용량 증분
   * 문 캐시 크기

1. 저장을 클릭한 후 변경 사항 활성화를 클릭합니다.
1. WebLogic 관리 서버를 다시 시작합니다.

### DB2용 WebSphere에 대한 연결 풀 설정 구성 {#configure-connection-pool-settings-for-websphere-for-db2}

1. 탐색 트리에서 리소스 > JDBC > JDBC 공급자를 클릭합니다. 오른쪽 창에서 생성한 데이터 소스인 DB2 Universal JDBC 드라이버 공급자 또는 LiveCycle - db2 - IDP_DS를 클릭합니다.
1. 추가 속성에서 데이터 소스를 클릭한 후 IDP_DS를 선택합니다.
1. 다음 화면의 추가 속성에서 연결 풀 속성을 클릭하고 최대 연결 수 상자와 최소 연결 수 상자에 값을 입력합니다.
1. 확인 또는 적용을 클릭한 후 마스터 구성에 직접 저장을 클릭합니다.

### Oracle용 WebSphere에 대한 연결 풀 설정 구성 {#configure-connection-pool-settings-for-websphere-for-oracle}

1. 탐색 트리에서 리소스 > JDBC > JDBC 공급자를 클릭합니다. 오른쪽 창에서 생성한 Oracle JDBC 드라이버 데이터 소스를 클릭합니다.
1. 추가 속성에서 데이터 소스를 클릭한 후 IDP_DS를 선택합니다.
1. 다음 화면의 추가 속성에서 연결 풀 속성을 클릭하고 최대 연결 수 상자와 최소 연결 수 상자에 값을 입력합니다.
1. 확인 또는 적용을 클릭한 후 마스터 구성에 직접 저장을 클릭합니다.

### SQLServer용 WebSphere에 대한 연결 풀 설정 구성 {#configure-connection-pool-settings-for-websphere-for-sqlserver}

1. 탐색 트리에서 리소스 > JDBC > JDBC 공급자를 클릭하고 오른쪽 창에서 생성한 사용자 정의 JDBC 드라이버 데이터 소스를 클릭합니다.
1. 추가 속성에서 데이터 소스를 클릭한 후 IDP_DS를 선택합니다.
1. 다음 화면의 추가 속성에서 연결 풀 속성을 클릭하고 최대 연결 수 상자와 최소 연결 수 상자에 값을 입력합니다.
1. 확인 또는 적용을 클릭한 후 마스터 구성에 직접 저장을 클릭합니다.

## 인라인 문서 최적화 및 JVM 메모리에 미치는 영향 {#optimizing-inline-documents-and-impact-on-jvm-memory}

일반적으로 비교적 작은 크기의 문서를 처리하는 경우 문서 전송 속도 및 저장 공간과 관련된 성능을 향상할 수 있습니다. 이를 위해 다음과 같은 AEM Forms 제품 구성을 구현합니다.

* AEM Forms의 기본 문서 최대 인라인 크기를 대부분의 문서 크기보다 크게 늘립니다.
* 더 큰 파일을 처리하려면 고속 디스크 시스템이나 RAM 디스크에 있는 저장 디렉터리를 지정합니다.

최대 인라인 크기와 저장 디렉터리(AEM Forms 임시 파일 디렉터리와 GDS 디렉터리)는 관리 콘솔에서 구성됩니다.

### 문서 크기 및 최대 인라인 크기 {#document-size-and-maximum-inline-size}

AEM Forms에서 처리를 위해 전송한 문서가 기본 문서 최대 인라인 크기보다 작거나 같으면 해당 문서는 서버에 인라인으로 저장되고 Adobe Document 오브젝트로 직렬화됩니다. 문서를 인라인으로 저장하면 성능이 크게 향상될 수 있습니다. 그러나 Forms Workflow를 사용하는 경우 추적 목적으로 콘텐츠가 데이터베이스에 저장될 수도 있습니다. 따라서 최대 인라인 크기를 늘리면 데이터베이스 크기에 영향을 미칠 수 있습니다.

최대 인라인 크기보다 큰 문서는 로컬 파일 시스템에 저장됩니다. 서버와 주고받는 Adobe Document 오브젝트는 해당 파일을 가리키는 포인터일 뿐입니다.

문서 콘텐츠가 인라인된 경우(즉, 최대 인라인 크기보다 작은 경우) 해당 콘텐츠는 문서의 직렬화 페이로드의 일부로 데이터베이스에 저장됩니다. 따라서 최대 인라인 크기를 늘리면 데이터베이스 크기에 영향을 미칠 수 있습니다.

**최대 인라인 크기 변경**

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

1. 관리 콘솔에서 설정 > 핵심 시스템 설정 > 구성을 클릭합니다.
1. 기본 문서 최대 인라인 크기 상자에 값을 입력하고 확인을 클릭합니다.

   >[!NOTE]
   >
   >JEE 환경의 AEM Forms와 JEE 환경의 AEM Forms에 포함된 OSGi 번들의 AEM Forms에 대한 문서 최대 인라인 크기 속성 값은 동일해야 합니다. 이 단계에서는 JEE 환경의 AEM Forms에 대해서만 값을 업데이트하고 JEE 환경의 AEM Forms에 포함된 OSGi 번들의 AEM Forms에 대해서는 값을 업데이트하지 않습니다.

1. 다음과 같은 시스템 속성으로 애플리케이션 서버를 다시 시작합니다.

   com.adobe.idp.defaultDocumentMaxInlineSize=`[value specified in Step 2]`

   >[!NOTE]
   >
   >위에 언급된 시스템 속성은 JEE 환경의 AEM Forms와 JEE 환경의 AEM Forms에 포함된 OSGi 번들의 AEM Forms에 설정된 문서 최대 인라인 크기 속성 값을 재정의합니다.

>[!NOTE]
>
>기본 최대 인라인 크기는 65536바이트입니다.

### JVM 최대 힙 크기 {#jvm-maximum-heap-size}

최대 인라인 크기를 늘리려면 직렬화된 문서를 저장하는 데 더 많은 메모리가 필요합니다. 따라서 일반적으로 JVM 최대 힙 크기도 늘려야 합니다.

많은 문서를 처리하는 과부하 시스템은 JVM 힙 메모리를 빠르게 포화시킬 수 있습니다. OutOfMemoryError를 방지하려면 일반적으로 지정된 시간에 실행되는 문서 수에 인라인 문서 크기를 곱한 값만큼 JVM 최대 힙 크기를 늘립니다.

JVM 최대 힙 크기 증가 = (인라인 문서 크기) x (처리된 평균 문서 수)

**JVM 최대 힙 크기 계산**

이 예에서 현재 JVM 최대 힙은 512MB로 설정되어 있고 최대 인라인 크기는 64KB입니다. 작업 10개가 동시에 실행되고 각 작업에 입력 파일 9개와 결과 파일 1개가 있는 시나리오(작업당 총 10개의 파일, 파일 100개가 동시에 처리됨)에 맞게 서버를 구성해야 합니다. 모든 파일의 크기는 512KB 미만입니다.

모든 파일을 인라인으로 저장하려면 최대 인라인 크기를 최소 512KB로 설정합니다.

JVM 최대 힙 크기에 필요한 증가량은 다음 방정식을 사용하여 계산됩니다.

(512KB) x (100) = 51200KB 또는 50MB

JVM 최대 힙 크기를 50MB만큼 늘려 총 562MB가 되도록 설정해야 합니다.

**힙 조각화 고려**

인라인 문서 크기를 큰 값으로 설정하면 힙 조각화가 일어나기 쉬운 시스템에서 OutOfMemoryError가 발생할 위험이 높아집니다. 문서를 인라인으로 저장하려면 JVM 힙 메모리에 충분한 연속 공간이 있어야 합니다. 일부 운영 체제, JVM, 가비지 수집 알고리즘에서는 힙 조각화가 발생하기 쉽습니다. 조각화로 인해 연속된 힙 공간의 양이 줄어들고 전체 여유 공간이 충분하더라도 OutOfMemoryError가 발생할 수 있습니다.

예를 들어 애플리케이션 서버에서 수행된 이전 작업으로 인해 JVM 힙이 조각난 상태로 남아 있고 가비지 수집기가 힙을 충분히 압축하여 큰 블록의 여유 공간을 회복할 수 없습니다. 최대 인라인 크기 증가에 맞게 JVM 최대 힙 크기를 조정했더라도 OutOfMemoryError가 발생할 수 있습니다.

힙 조각화를 고려하려면 인라인 문서 크기를 전체 힙 크기의 0. 1%보다 높게 설정해서는 안 됩니다. 예를 들어 JVM 최대 힙 크기가 512MB이면 최대 인라인 크기인 512MB x 0.001 = 0.512MB 또는 512KB를 지원할 수 있습니다.

## WebSphere Application Server 개선 사항 {#websphere-application-server-enhancements}

이 섹션에서는 WebSphere Application Server 환경에만 적용되는 설정을 설명합니다.

### JVM에 할당된 최대 메모리 증가 {#increasing-the-maximum-memory-allocated-to-the-jvm}

Configuration Manager를 실행 중이거나 명령줄 유틸리티 *ejbdeploy*&#x200B;를 사용하여 EJB(Enterprise JavaBeans) 배포 코드를 생성하려고 할 때 OutOfMemory 오류가 발생하면 JVM에 할당된 메모리 양을 늘립니다.

1. *[appserver root]*/deploytool/itp/ 디렉터리에서 ejbdeploy 스크립트를 편집합니다.

   * (Windows) `ejbdeploy.bat`
   * (Linux 및 UNIX) `ejbdeploy.sh`

1. `-Xmx256M` 매개변수를 찾아 `-Xmx1024M`과 같이 더 높은 값으로 변경합니다.
1. 파일을 저장합니다.
1. `ejbdeploy` 명령을 실행하거나 Configuration Manager를 사용하여 다시 배포합니다.

## LDAP를 사용하여 Windows Server 2003 성능 향상 {#improving-windows-server-2003-performance-with-ldap}

이 콘텐츠에서는 Microsoft Windows Server 2003 운영 체제 환경에만 적용되는 설정을 설명합니다.

검색 연결에 연결 풀링을 사용하면 필요한 포트 수를 최대 50%까지 줄일 수 있습니다. 해당 연결이 항상 지정된 도메인에 대해 동일한 자격 증명을 사용하고 컨텍스트와 관련 오브젝트가 명시적으로 닫히기 때문에 가능합니다.

### 연결 풀링을 위한 Windows Server 구성 {#configure-your-windows-server-for-connection-pooling}

1. 시작 > 실행을 클릭하여 레지스트리 편집기를 시작하고 열기 상자에 `regedit`을 입력한 후 확인을 클릭합니다.
1. 레지스트리 키 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters`로 이동합니다.
1. 레지스트리 편집기의 오른쪽 창에서 TcpTimedWaitDelay 값 이름을 찾습니다. 이름이 나타나지 않으면 메뉴 모음에서 편집 > 새로 만들기 > DWORD 값을 선택하여 이름을 추가합니다.
1. 이름 상자에 `TcpTimedWaitDelay`를 입력합니다.

   >[!NOTE]
   >
   >상자 안에 깜박이는 커서와 `New Value #`가 표시되지 않으면 오른쪽 패널 내부를 마우스 오른쪽 버튼으로 클릭하고 이름 바꾸기를 선택한 후 이름 상자에 `TcpTimedWaitDelay`*를 입력합니다.*

1. MaxUserPort, MaxHashTableSize, MaxFreeTcbs 값 이름에 대해 4단계를 반복합니다.
1. 오른쪽 창 내부를 두 번 클릭하여 TcpTimedWaitDelay 값을 설정합니다. 기본에서 10진수를 선택하고 값 상자에 `30`을 입력합니다.
1. 오른쪽 창 내부를 두 번 클릭하여 MaxUserPort 값을 설정합니다. 기본에서 10진수를 선택하고 값 상자에 `65534`를 입력합니다.
1. 오른쪽 창 내부를 두 번 클릭하여 MaxHashTableSize 값을 설정합니다. 기본에서 10진수를 선택하고 값 상자에 `65536`을 입력합니다.
1. 오른쪽 창 내부를 두 번 클릭하여 MaxFreeTcbs 값을 설정합니다. 기본에서 10진수를 선택하고 값 상자에 `16000`을 입력합니다.

>[!NOTE]
>
>레지스트리 편집기나 다른 방법을 사용하여 레지스트리를 잘못 수정하면 심각한 문제가 발생할 수 있습니다. 이러한 문제가 발생하면 운영 체제를 다시 설치해야 할 수도 있습니다. 레지스트리를 수정하는 모든 책임은 사용자에게 있습니다.
