---
title: JEE 환경 AEM Forms 강화
seo-title: JEE 환경 AEM Forms 강화
description: 회사 인트라넷에서 실행되는 JEE의 AEM Forms 보안을 강화하기 위한 다양한 보안 강화 설정을 살펴볼 수 있습니다.
seo-description: 회사 인트라넷에서 실행되는 JEE의 AEM Forms 보안을 강화하기 위한 다양한 보안 강화 설정을 살펴볼 수 있습니다.
uuid: f6c63690-6376-4fe1-9df2-a14fbfd62aff
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: 6b380e92-f90d-4875-b7a2-f3958daf2364
translation-type: tm+mt
source-git-commit: 9e1d77b8696436b392f0d9209ddcb2c9196f3c09
workflow-type: tm+mt
source-wordcount: '7698'
ht-degree: 0%

---


# JEE 환경 AEM Forms 강화 {#hardening-your-aem-forms-on-jee-environment}

회사 인트라넷에서 실행되는 JEE의 AEM Forms 보안을 강화하기 위한 다양한 보안 강화 설정을 살펴볼 수 있습니다.

이 문서에서는 JEE에서 AEM Forms을 실행하는 서버 보안을 위한 권장 사항 및 우수 사례에 대해 설명합니다. 운영 체제 및 응용 프로그램 서버에 대한 포괄적인 호스트 강화 문서가 아닙니다. 대신, 이 문서에서는 회사 인트라넷 내에서 실행 중인 JEE의 AEM Forms의 보안을 강화하기 위해 구현해야 하는 다양한 보안 강화 설정에 대해 설명합니다. 그러나 JEE 응용 프로그램 서버의 AEM Forms이 안전한지 확인하려면 보안 모니터링, 감지 및 응답 절차를 구현해야 합니다.

이 문서에서는 설치 및 구성 수명 주기 동안 다음 단계에서 적용해야 하는 보강 기술에 대해 설명합니다.

* **사전 설치:** JEE에 AEM Forms을 설치하기 전에 이러한 기술을 사용하십시오.
* **설치:** JEE 설치 과정 중에 이러한 기술을 사용하십시오.
* **설치 후:** 설치 후, 그리고 그 후에 정기적으로 이러한 기술을 사용합니다.

JEE의 AEM Forms은 사용자 지정이 가능하며 여러 환경에서 작업할 수 있습니다. 권장 사항 중 일부가 조직의 요구 사항에 맞지 않을 수 있습니다.

## 사전 설치 {#preinstallation}

JEE에 AEM Forms을 설치하기 전에 네트워크 레이어 및 운영 체제에 보안 솔루션을 적용할 수 있습니다. 이 섹션에서는 몇 가지 문제에 대해 설명하고 이러한 영역의 보안 취약점을 줄이기 위한 권장 사항을 만듭니다.

**UNIX 및 Linux에서 설치 및 구성**

루트 셸을 사용하여 JEE에 AEM Forms을 설치하거나 구성해서는 안됩니다. 기본적으로 파일은 /opt 디렉토리 아래에 설치되며 설치를 수행하는 사용자는 /opt 아래에 있는 모든 파일 권한이 필요합니다. 또는 개별 사용자의 /user 디렉토리에 이미 모든 파일 권한이 있는 경우 설치를 수행할 수 있습니다.

**Windows에서 설치 및 구성**

턴키 방법을 사용하거나 PDF Generator를 설치하는 경우 JBoss의 JEE에 AEM Forms을 설치하는 경우 Windows에서 관리자로 설치해야 합니다. 또한 기본 애플리케이션 지원을 통해 Windows에 PDF Generator를 설치할 때는 Microsoft Office를 설치한 Windows 사용자와 동일한 설치 프로그램을 실행해야 합니다. 설치 권한에 대한 자세한 내용은* 응용 프로그램 서버의 JEE*에 AEM Forms 설치 및 배포 문서를 참조하십시오.

### 네트워크 레이어 보안 {#network-layer-security}

네트워크 보안 취약점은 인터넷 접속 또는 인트라넷 기반 애플리케이션 서버에 대한 첫 번째 위협 중 하나입니다. 이 섹션에서는 이러한 취약점에 대한 네트워크의 호스트 강화 프로세스에 대해 설명합니다. 네트워크 세분화, TCP/IP(Transmission Control Protocol/Internet Protocol) 스택 보강 및 호스트 보호를 위한 방화벽 사용에 대해 다룹니다.

다음 표에서는 네트워크 보안 취약점을 줄이는 일반적인 프로세스에 대해 설명합니다.

<table> 
 <thead> 
  <tr> 
   <th><p>문제</p> </th> 
   <th><p>설명</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>비무장지대(DMZ)</p> </td> 
   <td><p>DMZ(비무장지대)에 양식 서버 배포 세그멘테이션은 내부 방화벽 뒤에 배치된 JEE에서 AEM Forms을 실행하는 데 사용되는 응용 프로그램 서버와 함께 두 개 이상의 수준에 있어야 합니다. 웹 서버가 포함된 DMZ에서 외부 네트워크를 분리하고 내부 네트워크에서 분리해야 합니다. 방화벽을 사용하여 분판 레이어를 구현합니다. 각 네트워크 레이어를 통과하는 트래픽을 분류하고 제어하여 필요한 데이터의 절대 최소값만 허용됩니다.</p> </td> 
  </tr> 
  <tr> 
   <td><p>개인 IP 주소</p> </td> 
   <td><p>AEM Forms 응용 프로그램 서버에서 RFC 1918 개인 IP 주소에 NAT(네트워크 주소 변환)를 사용하십시오. 비공개 IP 주소(10.0.0.0/8, 172.16.0.0/12 및 192.168.0.0/16)을 할당하여 공격자가 인터넷을 통해 NAT의 내부 호스트에 트래픽을 라우팅하거나 NAT의 내부 호스트에 트래픽을 라우팅하는 것을 더욱 어렵게 만듭니다.</p> </td> 
  </tr> 
  <tr> 
   <td><p>방화벽</p> </td> 
   <td><p>방화벽 솔루션을 선택하려면 다음 기준을 사용하십시오.</p> 
    <ul> 
     <li><p>단순 패킷 필터링 솔루션 대신 프록시 서버 및/또는 <em>상태 저장 검사를</em> 지원하는 방화벽을 구현할 수 있습니다.</p> </li> 
     <li><p>명시적으로 허용된 <em>보안 패러다임을 제외한 모든 서비스를</em> 거부하는 방화벽을 사용하십시오.</p> </li> 
     <li><p>이중 홈 또는 다중 홈인 방화벽 솔루션을 구현합니다. 이 아키텍처는 최고 수준의 보안 기능을 제공하며 권한이 없는 사용자가 방화벽 보안을 우회하지 못하도록 합니다.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>데이터베이스 포트</p> </td> 
   <td><p>데이터베이스에 대한 기본 의견 수렴 포트를 사용하지 마십시오(MySQL - 3306, Oracle - 1521, MS SQL - 1433). 데이터베이스 포트 변경에 대한 자세한 내용은 데이터베이스 설명서를 참조하십시오.</p> <p>다른 데이터베이스 포트를 사용하면 JEE 구성의 전체 AEM Forms에 영향을 줍니다. 기본 포트를 변경하는 경우 JEE의 AEM Forms에 대한 데이터 소스 등의 구성 다른 영역에서 해당 변경을 수행해야 합니다.</p> <p>JEE의 AEM Forms에서 데이터 소스를 구성하는 방법에 대한 자세한 내용은 JEE에서 AEM Forms 설치 및 업그레이드 또는 <a href="/help/forms/using/introduction-aem-forms.md" target="_blank">AEM Forms 사용자 가이드에서 응용 프로그램 서버의 JEE에서 AEM Forms으로 업그레이드를 참조하십시오</a>.</p> </td> 
  </tr> 
 </tbody> 
</table>

### 운영 체제 보안 {#operating-system-security}

다음 표에서는 운영 체제에서 발견된 보안 취약점을 최소화하는 몇 가지 잠재적 접근 방법을 설명합니다.

<table> 
 <thead> 
  <tr> 
   <th><p>문제</p></th> 
   <th><p>설명</p></th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>보안 패치</p></td> 
   <td><p>공급업체 보안 패치와 업그레이드가 시기 적절하게 적용되지 않는 경우 인증되지 않은 사용자가 애플리케이션 서버에 액세스할 수 있는 위험이 높아집니다. 보안 패치를 프로덕션 서버에 적용하기 전에 테스트하십시오.</p><p>또한 정기적으로 패치를 확인하고 설치할 수 있는 정책과 절차를 만듭니다.</p></td> 
  </tr> 
  <tr> 
   <td><p>바이러스 보호 소프트웨어</p></td> 
   <td><p>바이러스 스캐너는 서명을 스캔하거나 비정상적인 행동을 확인함으로써 감염된 파일을 식별할 수 있습니다. 스캐너는 바이러스 서명을 파일에 보관합니다. 파일은 보통 로컬 하드 드라이브에 저장됩니다. 새로운 바이러스가 자주 발견되기 때문에 바이러스 스캐너에서 현재 모든 바이러스를 식별하도록 이 파일을 자주 업데이트해야 합니다.</p></td> 
  </tr> 
  <tr> 
   <td><p>NTP(Network Time Protocol)</p></td> 
   <td><p>법의학적인 분석을 위해 양식 서버에 정확한 시간 유지 NTP를 사용하여 인터넷에 직접 연결된 모든 시스템의 시간을 동기화합니다.</p></td> 
  </tr> 
 </tbody> 
</table>

운영 체제에 대한 추가 보안 정보는 [&quot;운영 체제 보안 정보&quot;를 참조하십시오](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#operating_system_security_information).

## 설치 {#installation}

이 섹션에서는 AEM Forms 설치 과정에서 보안 취약점을 줄이기 위해 사용할 수 있는 기술에 대해 설명합니다. 경우에 따라 이러한 기술은 설치 프로세스의 일부인 옵션을 사용합니다. 다음 표에서는 이러한 기술에 대해 설명합니다.

<table> 
 <thead> 
  <tr> 
   <th><p>문제</p> </th> 
   <th><p>설명</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>권한</p> </td> 
   <td><p>소프트웨어 설치에 필요한 최소 권한 수를 사용하십시오. 관리자 그룹에 없는 계정을 사용하여 컴퓨터에 로그인합니다. Windows의 경우 실행 명령을 사용하여 관리 사용자로 JEE 설치 관리자에서 AEM Forms을 실행할 수 있습니다. UNIX 및 Linux 시스템의 경우 소프트웨어를 설치하는 명령 <code>sudo</code> 을 사용합니다.</p> </td> 
  </tr> 
  <tr> 
   <td><p>소프트웨어 소스</p> </td> 
   <td><p>신뢰할 수 없는 출처의 JEE에서 AEM Forms을 다운로드하거나 실행하지 마십시오.</p> <p>악성 프로그램에는 데이터 도난, 수정 및 삭제, 서비스 거부 등 다양한 방법으로 보안을 위반하는 코드가 포함될 수 있습니다. Adobe DVD 또는 신뢰할 수 있는 소스에서만 JEE에 AEM Forms을 설치합니다.</p> </td> 
  </tr> 
  <tr> 
   <td><p>디스크 파티션</p> </td> 
   <td><p>전용 디스크 파티션에 AEM Forms을 JEE에 배치합니다. 디스크 세그멘테이션은 보안을 강화하기 위해 서버의 특정 데이터를 별도의 물리적 디스크에 보관하는 프로세스입니다. 이러한 방식으로 데이터를 배열하면 디렉토리 탐색 공격의 위험이 줄어듭니다. JEE 컨텐츠 디렉토리에 AEM Forms을 설치할 수 있는 시스템 파티션과 별개인 파티션을 만들 계획입니다. Windows의 경우 시스템 파티션에 system32 디렉터리 또는 부팅 파티션이 들어 있습니다.</p> </td> 
  </tr> 
  <tr> 
   <td><p>구성 요소</p> </td> 
   <td><p>기존 서비스를 평가하고 필요하지 않은 서비스를 비활성화하거나 제거합니다. 불필요한 구성 요소 및 서비스를 설치하지 마십시오.</p> <p>응용 프로그램 서버의 기본 설치에는 사용자가 사용할 필요가 없는 서비스가 포함될 수 있습니다. 배포하기 전에 모든 불필요한 서비스를 비활성화하여 공격 시작 지점을 최소화해야 합니다. 예를 들어 JBoss에서는 META-INF/jboss-service.xml 설명자 파일에서 불필요한 서비스를 주석 처리할 수 있습니다.</p> </td> 
  </tr> 
  <tr> 
   <td><p>도메인 간 정책 파일</p> </td> 
   <td><p>서버에 <code>crossdomain.xml</code> 파일이 있으면 해당 서버가 즉시 손상될 수 있습니다. 도메인 목록을 최대한 제한하는 것이 좋습니다. 안내선을 사용할 때 개발 중에 사용된 <code>crossdomain.xml</code> 파일을 프로덕션 <em>(더 이상 사용되지 않음)으로 배치하지 마십시오</em>. 웹 서비스를 사용하는 안내서의 경우, 서비스가 가이드를 제공하는 동일한 서버에 있는 경우 <code>crossdomain.xml</code> 파일이 전혀 필요하지 않습니다. 하지만 서비스가 다른 서버에 있거나 클러스터와 관련된 경우 <code>crossdomain.xml</code> 파일이 있어야 합니다. crossdomain.xml 파일에 대한 자세한 내용은 <a href="https://kb2.adobe.com/cps/142/tn_14213.html">https://kb2.adobe.com/cps/142/tn_14213.html</a>을 참조하십시오.</p> </td> 
  </tr> 
  <tr> 
   <td><p>운영 체제 보안 설정</p> </td> 
   <td><p>Solaris 플랫폼에서 192비트 또는 256비트 XML 암호화를 사용해야 하는 경우 <code>pkcs11_softtoken_extra.so</code> 대신 설치해야 합니다 <code>pkcs11_softtoken.so</code>.</p> </td> 
  </tr> 
 </tbody> 
</table>

## 설치 후 단계 {#post-installation-steps}

JEE에 AEM Forms을 성공적으로 설치한 후에는 보안 측면에서 환경을 정기적으로 유지하는 것이 중요합니다.

다음 섹션에서는 배포된 양식 서버의 보안을 위해 권장되는 다양한 작업에 대해 자세히 설명합니다.

### AEM Forms 보안 {#aem-forms-security}

다음 권장 설정은 관리 웹 응용 프로그램 외부에 있는 JEE 서버의 AEM Forms에 적용됩니다. 서버에 대한 보안 위험을 줄이려면 JEE에 AEM Forms을 설치한 후 즉시 이 설정을 적용합니다.

**보안 패치**

공급업체 보안 패치와 업그레이드가 시기 적절하게 적용되지 않는 경우 인증되지 않은 사용자가 애플리케이션 서버에 액세스할 수 있는 위험이 높아집니다. 보안 패치를 프로덕션 서버에 적용하기 전에 테스트하여 애플리케이션의 호환성과 가용성을 보장합니다. 또한 정기적으로 패치를 확인하고 설치할 수 있는 정책과 절차를 만듭니다. JEE 업데이트에 대한 AEM Forms은 기업 제품 다운로드 사이트에 있습니다.

**서비스 계정(Windows에서만 JBoss 턴키)**

JEE의 AEM Forms은 기본적으로 LocalSystem 계정을 사용하여 서비스를 설치합니다. 기본 제공 LocalSystem 사용자 계정은 높은 접근성을 가집니다. 관리자 그룹의 일부입니다. 작업자 프로세스 ID가 LocalSystem 사용자 계정으로 실행되는 경우 해당 작업자 프로세스는 전체 시스템에 대한 전체 액세스 권한을 가집니다.

JEE에서 AEM Forms이 배포된 응용 프로그램 서버를 특정 비관리 계정을 사용하여 실행하려면 다음 지침을 따르십시오.

1. MMC(Microsoft Management Console)에서 양식 서버 서비스에 로그인할 로컬 사용자를 만듭니다.

   * [ **사용자가 암호를 변경할 수 없음]을 선택합니다**.
   * [ **구성원** ] 탭에서 **사용자** 그룹이나열되는지 확인합니다.

   >[!NOTE]
   >
   >PDF Generator에 대해 이 설정을 변경할 수 없습니다.

1. [ **시작** ] > [ **설정** ] **> [관리 도구** ] **> [서비스**]를선택합니다.
1. JEE에서 AEM Forms을 위한 JBoss를 두 번 클릭하고 서비스를 중지합니다.
1. [ **로그온** ] 탭에서 [이 계정 ****]을 선택하고 만든 사용자 계정을 찾은 후 계정의 암호를 입력합니다.
1. MMC에서 **로컬 보안 설정** 을 열고 **로컬 정책** > **사용자 권한 할당**&#x200B;을 선택합니다.
1. 양식 서버가 실행 중인 사용자 계정에 다음 권한을 할당합니다.

   * 터미널 서비스를 통해 로그온 거부
   * 로컬에서 로그온 거부
   * 서비스로 로그온(이미 설정되어야 함)

1. 새 사용자 계정에 다음 디렉토리에 대한 수정 권한을 지정합니다.
   * **GDS(Global Document Storage) 디렉토리**: GDS 디렉토리의 위치는 AEM Forms 설치 과정에서 수동으로 구성됩니다. 설치 중에 위치 설정이 비어 있는 상태로 남아 있는 경우, 위치는 응용 프로그램 서버 설치 시 `[JBoss root]/server/[type]/svcnative/DocumentStorage`
   * **CRX-Repository 디렉토리**: 기본 위치는 `[AEM-Forms-installation-location]\crx-repository`
   * **AEM Forms 임시 디렉토리**:
      * (Windows) 환경 변수에 설정된 TMP 또는 TEMP 경로
      * (AIX, Linux 또는 Solaris) 로그인한 사용자의 홈 디렉토리UNIX 기반 시스템에서 루트 이외의 사용자는 다음 디렉토리를 임시 디렉토리로 사용할 수 있습니다.
      * (Linux) /var/tmp 또는 /usr/tmp
      * (AIX) /tmp 또는 /usr/tmp
      * (Solaris) /var/tmp 또는 /usr/tmp
1. 새 사용자 계정에 다음 디렉토리에 대한 쓰기 권한을 지정합니다.
   * [JBoss-directory]\standalone\deployment
   * [JBoss-directory]\standalone\
   * [JBoss-directory]\bin\

   >[!NOTE]
   >
   > JBoss Application Server의 기본 설치 위치:
   > * Windows: C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   > * Linux: /opt/jboss/

1. 응용 프로그램 서버를 시작합니다.

**Configuration Manager 부트스트랩 서블릿 비활성화**

Configuration Manager가 응용 프로그램 서버에 배포된 서블릿을 사용하여 JEE 데이터베이스의 AEM Forms 부트스트래핑을 수행했습니다. 구성이 완료되기 전에 Configuration Manager가 이 서블릿에 액세스하므로 권한이 있는 사용자에 대한 액세스 보안이 유지되지 않고 Configuration Manager를 사용하여 JEE에서 AEM Forms을 구성한 후에는 이 서블릿에 대한 액세스를 비활성화해야 합니다.

1. adobe-livecycle-appserver[.ear 파일의 압축을]해제합니다.
1. META-INF/application.xml 파일을 엽니다.
1. adobe-bootstrapper.war 섹션을 검색합니다.

   ```as3
   <!-- bootstrapper start --> 
   <module id="WebApp_adobe_bootstrapper"> 
       <web> 
           <web-uri>adobe-bootstrapper.war</web-uri> 
           <context-root>/adobe-bootstrapper</context-root> 
       </web> 
   </module> 
   <module id="WebApp_adobe_lcm_bootstrapper_redirector"> 
       <web> 
           <web-uri>adobe-lcm-bootstrapper-redirector.war</web-uri> 
           <context-root>/adobe-lcm-bootstrapper</context-root> 
       </web> 
   </module> 
   <!-- bootstrapper end-->
   ```

1. AEM Forms 서버를 중지합니다.
1. adobe-bootstrapper.war 및 adobe-lcm-bootstrapper-redirectory에 주석을 설정합니다. 다음과 같은 전쟁 모듈입니다.

   ```as3
   <!-- bootstrapper start --> 
   <!-- 
   <module id="WebApp_adobe_bootstrapper"> 
       <web> 
           <web-uri>adobe-bootstrapper.war</web-uri> 
           <context-root>/adobe-bootstrapper</context-root> 
       </web> 
   </module> 
   <module id="WebApp_adobe_lcm_bootstrapper_redirector"> 
       <web> 
           <web-uri>adobe-lcm-bootstrapper-redirector.war</web-uri> 
           <context-root>/adobe-lcm-bootstrapper</context-root> 
       </web> 
   </module> 
   --> 
   <!-- bootstrapper end-->
   ```

1. META-INF/application.xml 파일을 저장하고 닫습니다.
1. EAR 파일을 압축하여 응용 프로그램 서버에 다시 배포합니다.
1. AEM Forms 서버를 시작합니다.
1. 아래 URL을 브라우저에 입력하여 변경 사항을 테스트하고 더 이상 작동하지 않는지 확인합니다.

   https://&lt;localhost>:&lt;port>/adobe-bootstrapper/bootstrap

**Trust Store에 대한 원격 액세스 차단**

Configuration Manager를 사용하면 JEE Trust Store의 AEM Forms에 Acrobat Reader DC 확장 자격 증명을 업로드할 수 있습니다. 즉, 원격 프로토콜(SOAP 및 EJB)을 통한 Trust Store Credential Service에 대한 액세스가 기본적으로 활성화되어 있습니다. Configuration Manager를 사용하여 Rights 자격 증명을 업로드한 후 또는 나중에 관리 콘솔을 사용하여 자격 증명을 관리하기로 결정한 경우 이 액세스 권한이 더 이상 필요하지 않습니다.

[중요하지 않은 원격 서비스 액세스 비활성화] 섹션의 단계를 수행하여 모든 Trust Store 서비스에 대한 원격 [액세스를 비활성화할 수 있습니다](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_remote_access_to_services).

**중요하지 않은 익명 액세스 비활성화**

일부 양식 서버 서비스에는 익명의 호출자가 호출할 수 있는 작업이 있습니다. 이러한 서비스에 대한 익명의 액세스가 필요하지 않은 경우, 중요하지 않은 익명 서비스 [에 대한 액세스 비활성화 단계를 수행하여 서비스를 비활성화합니다](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_anonymous_access_to_services).

#### 기본 관리자 암호 변경 {#change-the-default-administrator-password}

JEE의 AEM Forms이 설치되면 기본 암호 *를 사용하는 사용자 Super Administrator/ 로그인 ID Administrator에 대해 단일 기본 사용자 계정이 구성됩니다*. 구성 관리자를 사용하여 이 암호를 즉시 변경해야 합니다.

1. 웹 브라우저에 다음 URL을 입력합니다.

   ```as3
   https://[host name]:[port]/adminui
   ```

   기본 포트 번호는 다음 중 하나입니다.

   **JBoss:** 8080년

   **WebLogic Server:** 7001년

   **WebSphere:** 9080년.

1. [ **사용자 이름** ] 필드에 `administrator` 을 입력하고 [ **암호** ] 필드에 `password`을입력합니다.
1. 설정 **** > **사용자 관리** > **사용자 및 그룹을 클릭합니다**.
1. 찾기 `administrator` 필드 **를** 입력하고 찾기 **를**&#x200B;클릭합니다.
1. 사용자 **목록에서 수퍼** 관리자를 클릭합니다.
1. 사용자 편집 **페이지에서 암호** 변경을 클릭합니다.
1. 새 암호를 지정하고 [저장]을 **클릭합니다**.

또한 다음 단계를 수행하여 CRX 관리자의 기본 암호를 변경하는 것이 좋습니다.

1. 기본 사용자 이름/암호를 사용하여 `https://[server]:[port]/lc/libs/granite/security/content/useradmin.html` 로그인합니다.
1. 검색 필드에 관리자를 입력하고 **이동을 클릭합니다**.
1. 검색 결과 **에서 관리자를** 선택하고 사용자 인터페이스 오른쪽 아래에 있는 **편집** 아이콘을 클릭합니다.
1. 새 암호 필드에 새 암호 **를** 지정하고 암호 **필드에 이전 암호를** 지정합니다.
1. 사용자 인터페이스 오른쪽 하단에 있는 저장 아이콘을 클릭합니다.

#### WSDL 생성 비활성화 {#disable-wsdl-generation}

WSDL(Web Service Definition Language) 생성은 개발자가 클라이언트 애플리케이션을 구축하는 데 WSDL 생성을 사용하는 개발 환경에서만 활성화되어야 합니다. 서비스의 내부 세부 정보가 노출되지 않도록 프로덕션 환경에서 WSDL 생성을 비활성화할 수 있습니다.

1. 웹 브라우저에 다음 URL을 입력합니다.

   ```as3
   https://[host name]:[port]/adminui
   ```

1. 설정 **> 핵심 시스템 설정 > 구성을 클릭합니다**.
1. WSDL **활성화를 선택** 취소하고 **확인을 클릭합니다**.

### 응용 프로그램 서버 보안 {#application-server-security}

다음 표에서는 JEE 응용 프로그램의 AEM Forms이 설치된 후 응용 프로그램 서버의 보안을 유지하는 몇 가지 방법에 대해 설명합니다.

<table> 
 <thead> 
  <tr> 
   <th><p>문제</p> </th> 
   <th><p>설명</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>애플리케이션 서버 관리 콘솔</p> </td> 
   <td><p>응용 프로그램 서버의 JEE에 AEM Forms을 설치, 구성 및 배포한 후 응용 프로그램 서버 관리 콘솔에 대한 액세스를 비활성화해야 합니다. 자세한 내용은 응용 프로그램 서버 설명서를 참조하십시오.</p> </td> 
  </tr> 
  <tr> 
   <td><p>응용 프로그램 서버 쿠키 설정</p> </td> 
   <td><p>응용 프로그램 쿠키는 응용 프로그램 서버에서 제어합니다. 응용 프로그램을 배포할 때 응용 프로그램 서버 관리자는 서버 전체 또는 응용 프로그램별 기준으로 쿠키 기본 설정을 지정할 수 있습니다. 기본적으로 서버 설정이 우선합니다.</p> <p>응용 프로그램 서버에서 생성된 모든 세션 쿠키에는 속성이 포함되어야 <code>HttpOnly</code> 합니다. 예를 들어 JBoss Application Server를 사용할 때 <code>httpOnly="true"</code> 파일에서 SessionCookie 요소 <code>WEB-INF/web.xml</code> 를 수정할 수 있습니다.</p> <p>HTTPS 전용을 사용하여 쿠키를 전송할 수 있도록 제한할 수 있습니다. 따라서 HTTP를 통해 암호화되지 않은 상태로 전송됩니다. 응용 프로그램 서버 관리자는 전 세계적으로 서버에 대한 보안 쿠키를 활성화해야 합니다. 예를 들어 JBoss Application Server를 사용할 때 커넥터 요소를 파일에서 <code>secure=true</code> 수정할 수 <code>server.xml</code> 있습니다.</p> <p>쿠키 설정에 대한 자세한 내용은 응용 프로그램 서버 설명서를 참조하십시오.</p> </td> 
  </tr> 
  <tr> 
   <td><p>디렉토리 검색</p> </td> 
   <td><p>누군가 존재하지 않는 페이지를 요청하거나 디렉터의 이름을 요청할 때(요청 문자열은 슬래시(/)로 끝남), 응용 프로그램 서버는 해당 디렉토리의 내용을 반환하지 않아야 합니다. 이를 방지하기 위해 응용 프로그램 서버에서 디렉토리 탐색을 비활성화할 수 있습니다. 관리 콘솔 응용 프로그램 및 서버에서 실행 중인 다른 응용 프로그램에 대해 이렇게 해야 합니다.</p> <p>JBoss의 경우 다음 예와 같이 속성의 목록 초기화 매개변수 <code>DefaultServlet</code> 값을 web.xml 파일 <code>false</code> 에 설정합니다.</p> <p>&lt;servlet&gt;</p> <p>&lt;servlet-name&gt;default&lt;/servlet-name&gt;</p> <p>&lt;servlet-class&gt;</p> <p>org.apache.catalina.servlets.DefaultServlet</p> <p>&lt;/servlet-class&gt;</p> <p>&lt;init-param&gt;</p> <p>&lt;param-name&gt;list&lt;/param-name&gt;</p> <p>&lt;param-value&gt;false&lt;/param-value&gt;</p> <p>&lt;/init-param&gt;</p> <p>&lt;load-on-startup&gt;1&lt;/load-on-startup&gt;</p> <p>&lt;/servlet&gt;</p> <p>WebSphere의 경우 ibm-web-ext.xmi 파일의 <code>directoryBrowsingEnabled</code> 속성을 로 설정합니다 <code>false</code>.</p> <p>WebLogic의 경우 다음 예제와 같이 weblogic.xml 파일의 인덱스 디렉토리 속성 <code>false</code>을 로 설정합니다.</p> <p>&lt;container-descriptor&gt;</p> <p>&lt;index-directory-enabled&gt;false</p> <p>&lt;/index-directory-enabled&gt;</p> <p>&lt;/container-descriptor&gt;</p> </td> 
  </tr> 
 </tbody> 
</table>

### 데이터베이스 보안 {#database-security}

데이터베이스의 보안을 유지하는 경우 데이터베이스 공급업체에서 설명하는 측정을 구현해야 합니다. JEE에 대한 AEM Forms에서 사용할 수 있도록 허용된 최소 필수 데이터베이스 권한을 가진 데이터베이스 사용자를 할당해야 합니다. 예를 들어 데이터베이스 관리자 권한이 있는 계정은 사용하지 마십시오.

Oracle에서 사용하는 데이터베이스 계정에는 CONNECT, RESOURCE 및 CREATE VIEW 권한만 필요합니다. 다른 데이터베이스에 대한 유사한 요구 사항은 JEE에 [AEM Forms 설치 준비(단일 서버)를 참조하십시오](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64).

#### JBoss용 Windows에서 SQL Server에 대한 통합 보안 구성 {#configuring-integrated-security-for-sql-server-on-windows-for-jboss}

1. 다음 예와 같이 [JBOSS_HOME]\\standalone\configuration\lc_{datasource.xml} `integratedSecurity=true` 을 수정하여 연결 URL에 추가합니다.

   ```as3
    jdbc:sqlserver://<serverhost>:<port>;databaseName=<dbname>;integratedSecurity=true
   ```

1. 응용 프로그램 서버를 실행 중인 컴퓨터의 Windows 시스템 경로에 sqljdbc_auth.dll 파일을 추가합니다. sqljdbc_auth.dll 파일은 Microsoft SQL JDBC 6.2.1.0 드라이버를 설치한 상태로 있습니다.
1. 로컬 시스템에서 로그온 계정에 대한 JBoss Windows 서비스(JEE의 AEM Forms에 대한 JBoss)를 AEM Forms 데이터베이스와 최소 권한 세트가 있는 로그인 계정으로 수정합니다. Windows 서비스가 아닌 명령줄에서 JBoss를 실행하는 경우 이 단계를 수행할 필요가 없습니다.
1. SQL Server에 대한 보안 **을 혼합** 모드에서 **Windows 인증으로만**&#x200B;설정합니다.

#### Windows에서 WebLogic용 SQL Server에 대한 통합 보안 구성 {#configuring-integrated-security-for-sql-server-on-windows-for-weblogic}

1. 웹 브라우저의 URL 줄에 다음 URL을 입력하여 WebLogic Server 관리 콘솔을 시작합니다.

   ```as3
   https://[host name]:7001/console
   ```

1. 변경 센터에서 **잠금 및 편집을 클릭합니다**.
1. 도메인 구조에서 *[base_domain]* > **Services** > **JDBC** > Data Sources **** ****&#x200B;를 클릭하고 오른쪽 창에서 ClickIDP_DS를 클릭합니다.
1. 다음 화면의 **구성** 탭에서 **연결 풀** 탭 **을** 클릭하고 `integratedSecurity=true`속성상자에를입력합니다.
1. 도메인 구조에서 **[base_domain]** > **Services** > **JDBC** > **** **** Data Sources및 오른쪽 창에서 ClickBASE_DS_RM을 클릭합니다.
1. 다음 화면의 **구성** 탭에서 **연결 풀** 탭 **을** 클릭하고 `integratedSecurity=true`속성상자에를입력합니다.
1. 응용 프로그램 서버를 실행 중인 컴퓨터의 Windows 시스템 경로에 sqljdbc_auth.dll 파일을 추가합니다. sqljdbc_auth.dll 파일은 Microsoft SQL JDBC 6.2.1.0 드라이버를 설치한 상태로 있습니다.
1. SQL Server에 대한 보안 **을 혼합** 모드에서 **Windows 인증으로만**&#x200B;설정합니다.

#### WebSphere용 Windows에서 SQL Server에 대한 통합 보안 구성 {#configuring-integrated-security-for-sql-server-on-windows-for-websphere}

WebSphere에서는 WebSphere에 포함된 SQL Server JDBC 드라이버가 아닌 외부 SQL Server JDBC 드라이버를 사용하는 경우에만 통합 보안을 구성할 수 있습니다.

1. WebSphere 관리 콘솔에 로그인합니다.
1. 탐색 트리에서 **리소스** > **JDBC** > **데이터 소스** 를 **클릭하고 오른쪽 창에서 IDP_DS**&#x200B;를 클릭합니다.
1. 오른쪽 창의 추가 속성에서 **사용자 지정 속성**&#x200B;을 클릭한 다음 **새로 만들기를 클릭합니다**.
1. 이름 **** 상자 `integratedSecurity` 에 및 값 **상자에** 를 `true`입력합니다.
1. 탐색 트리에서 **리소스** > **JDBC** > **데이터 소스** 를 클릭하고 오른쪽 창에서 **RM_DS**&#x200B;를 클릭합니다.
1. 오른쪽 창의 추가 속성에서 **사용자 지정 속성**&#x200B;을 클릭한 다음 **새로 만들기를 클릭합니다**.
1. 이름 **** 상자 `integratedSecurity` 에 및 값 **상자에** 를 `true`입력합니다.
1. WebSphere가 설치된 컴퓨터에서 Windows 시스템 경로(C:\Windows)에 sqljdbc_auth.dll 파일을 추가합니다. sqljdbc_auth.dll 파일은 Microsoft SQL JDBC 1.2 드라이버 설치 위치와 동일한 위치에 있습니다(기본값은 *[InstallDir]*/sqljdbc_1.2/enu/auth/x86).
1. [ **시작** ] > **Campaign 컨트롤 패널** > **서비스**]를 선택하고 WebSphere용 Windows 서비스(IBM WebApplication Server &lt;버전> - &lt;노드>)를 마우스 오른쪽 단추로 누르고 속성 ****&#x200B;을 선택합니다.
1. 속성 대화 상자에서 **로그온** 탭을 클릭합니다.
1. 이 계정 **을** 선택하고 사용할 로그인 계정을 설정하는 데 필요한 정보를 제공합니다.
1. SQL Server의 보안을 혼합 **모드에서** Windows 인증만 **으로**&#x200B;설정합니다.

### 데이터베이스의 중요한 컨텐츠에 대한 액세스 보호 {#protecting-access-to-sensitive-content-in-the-database}

AEM Forms 데이터베이스 스키마는 시스템 구성 및 비즈니스 프로세스에 대한 민감한 정보를 포함하고 있으며 방화벽 뒤에 숨겨야 합니다. 데이터베이스가 양식 서버와 동일한 신뢰 경계 내에서 고려되어야 합니다. 비즈니스 데이터의 정보 노출 및 도난으로부터 보호하기 위해 데이터베이스 관리자(DBA)가 데이터베이스를 구성하여 권한이 있는 관리자만 액세스를 허용해야 합니다.

추가적인 예방 조치로, 데이터베이스 공급업체별 도구를 사용하여 다음 데이터가 포함된 테이블의 열을 암호화하는 것을 고려해야 합니다.

* Rights Management 문서 키
* Trust Store HSM PIN 암호화 키
* 로컬 사용자 암호 해시

공급업체별 도구에 대한 자세한 내용은 [&quot;데이터베이스 보안 정보&quot;를 참조하십시오](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#database_security_information).

### LDAP 보안 {#ldap-security}

LDAP(Lightweight Directory Access Protocol) 디렉토리는 일반적으로 기업 사용자 및 그룹 정보의 소스로 JEE의 AEM Forms에서 사용되며 암호 인증을 수행하는 수단으로 사용됩니다. LDAP 디렉토리가 SSL(Secure Socket Layer)을 사용하도록 구성되어 있고 JEE의 AEM Forms이 SSL 포트를 사용하여 LDAP 디렉토리에 액세스하도록 구성되어 있는지 확인해야 합니다.

#### LDAP 서비스 거부 {#ldap-denial-of-service}

LDAP를 사용하는 일반적인 공격에는 침입자가 고의적으로 여러 번 인증하지 못하는 문제가 발생합니다. 이렇게 하면 LDAP 디렉토리 서버가 모든 LDAP 의존적 서비스에서 사용자를 잠그는 문제가 해결됩니다.

사용자가 반복적으로 AEM Forms에 대해 인증하지 못할 때 AEM Forms이 구현하는 실패 시도 횟수 및 후속 잠금 시간 설정을 할 수 있습니다. 관리 콘솔에서 낮은 값을 선택합니다. 실패 시도 횟수를 선택할 때는 모든 시도가 끝난 후 LDAP 디렉토리 서버가 수행하기 전에 AEM Forms이 사용자를 잠그는 것을 이해해야 합니다.

#### 자동 계정 잠금 설정 {#set-automatic-account-locking}

1. 관리 콘솔에 로그인합니다.
1. 설정 **** > **사용자 관리** > **도메인 관리를 클릭합니다**.
1. 자동 계정 잠금 설정에서 **최대 연속 인증 실패** 수(예: 3)를 낮은 수로 설정합니다.
1. **저장**&#x200B;을 클릭합니다.

### 감사 및 로깅 {#auditing-and-logging}

응용 프로그램 감사 및 로깅의 적절하고 안전한 사용을 통해 가능한 한 빨리 보안 및 기타 예외 항목 이벤트를 추적하고 검색할 수 있습니다. 애플리케이션 내에서 감사 및 기록을 효과적으로 사용할 경우 로그인 성공 및 실패한 로그인 추적과 같은 항목뿐만 아니라 주요 기록의 생성 또는 삭제와 같은 주요 애플리케이션 이벤트도 포함됩니다.

감사를 사용하여 다음을 비롯한 다양한 유형의 공격을 감지할 수 있습니다.

* 무차별 암호 공격
* 서비스 거부 공격
* 스크립팅 공격의 적대적 입력 및 관련 클래스 삽입

이 표에서는 서버의 취약점을 줄이기 위해 사용할 수 있는 감사 및 로깅 기술에 대해 설명합니다.

<table> 
 <thead> 
  <tr> 
   <th><p>문제</p> </th> 
   <th><p>설명</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>로그 파일 ACL</p> </td> 
   <td><p>JEE 로그 파일 액세스 제어 목록(ACL)에 적절한 AEM Forms을 설정합니다.</p> <p>적절한 자격 증명을 설정하면 침입자가 파일을 삭제하지 못하도록 할 수 있습니다.</p> <p>로그 파일 디렉터리의 보안 권한은 관리자 및 SYSTEM 그룹에 대한 전체 제어여야 합니다. AEM Forms 사용자 계정에는 읽기 및 쓰기 권한만 있어야 합니다.</p> </td> 
  </tr> 
  <tr> 
   <td><p>로그 파일 중복성</p> </td> 
   <td><p>리소스가 허용되면 Syslog, Tivoli, Microsoft Operations Manager(MOM) Server 또는 다른 메커니즘을 사용하여 침입자가 액세스할 수 없는(쓰기 전용) 다른 서버로 로그를 실시간으로 보냅니다.</p> <p>이러한 방식으로 로그를 보호하면 무단 변경을 방지할 수 있습니다. 또한 중앙 저장소에 로그를 저장하면 상관 관계 및 모니터링이 가능해집니다. 예를 들어, 여러 개의 양식 서버를 사용하고 있고 각 컴퓨터를 암호로 쿼리하는 여러 컴퓨터에서 암호 추측 공격이 발생하는 경우)</p> </td> 
  </tr> 
 </tbody> 
</table>

### 관리자가 아닌 사용자가 PDF Generator 실행

관리자가 아닌 사용자가 PDF Generator를 사용하도록 설정할 수 있습니다. 일반적으로 관리 권한이 있는 사용자만 PDF Generator를 사용할 수 있습니다. 관리자가 아닌 사용자가 PDF Generator를 실행할 수 있도록 하려면 다음 단계를 수행하십시오.

1. 환경 변수 이름 PDFG_NON_ADMIN_ENABLED를 만듭니다.

1. 변수의 값을 TRUE로 설정합니다.

1. AEM Forms 인스턴스를 다시 시작합니다.

## 기업 외부에서 액세스할 수 있도록 JEE에 AEM Forms 구성 {#configuring-aem-forms-on-jee-for-access-beyond-the-enterprise}

JEE에 AEM Forms을 성공적으로 설치한 후에는 주기적으로 환경의 보안을 유지해야 합니다. 이 섹션에서는 JEE 프로덕션 서버에서 AEM Forms의 보안을 유지하는 데 권장되는 작업에 대해 설명합니다.

### 웹 액세스를 위한 역방향 프록시 설정 {#setting-up-a-reverse-proxy-for-web-access}

역방향 *프록시는* JEE 웹 응용 프로그램의 AEM Forms에 대한 URL 집합 중 하나를 외부 및 내부 사용자가 사용할 수 있도록 사용할 수 있습니다. 이 구성은 사용자가 JEE의 AEM Forms이 실행 중인 응용 프로그램 서버에 직접 연결할 수 있는 것보다 더 안전합니다. 역방향 프록시는 JEE에서 AEM Forms을 실행 중인 응용 프로그램 서버에 대한 모든 HTTP 요청을 수행합니다. 사용자는 역방향 프록시에 대한 네트워크 액세스 권한만 가지며 역방향 프록시가 지원하는 URL 연결만 시도할 수 있습니다.

**역방향 프록시 서버에 사용할 JEE 루트 URL의 AEM Forms**

JEE 웹 응용 프로그램의 각 AEM Forms에 대한 다음 응용 프로그램 루트 URL입니다. 최종 사용자에게 제공하려는 웹 응용 프로그램 기능에 대한 URL을 노출하도록 역방향 프록시를 구성해야 합니다.

특정 URL은 최종 사용자 지원 웹 애플리케이션으로 강조 표시됩니다. 역방향 프록시를 통해 외부 사용자에 액세스하기 위해 Configuration Manager에 대한 다른 URL이 노출되는 것을 피해야 합니다.

<table> 
 <thead> 
  <tr> 
   <th><p>루트 URL</p> </th> 
   <th><p>목적 및/또는 관련 웹 애플리케이션</p> </th> 
   <th><p>웹 기반 인터페이스</p> </th> 
   <th><p>최종 사용자 액세스</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>/ReaderExtensions/*</p> </td> 
   <td><p>PDF 문서에 사용 권한 적용을 위한 Acrobat Reader DC 익스텐션 최종 사용자 웹 애플리케이션</p> </td> 
   <td><p>예</p> </td> 
   <td><p>예</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edc/*</p> </td> 
   <td><p>Rights Management 최종 사용자 웹 응용 프로그램</p> </td> 
   <td><p>예</p> </td> 
   <td><p>예</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edcws/*</p> </td> 
   <td><p>권한 관리를 위한 웹 서비스 URL</p> </td> 
   <td><p>아니오</p> </td> 
   <td><p>예</p> </td> 
  </tr> 
  <tr> 
   <td><p>/pdfgui/*</p> </td> 
   <td><p>PDF Generator 관리 웹 애플리케이션</p> </td> 
   <td><p>예</p> </td> 
   <td><p>예</p> </td> 
  </tr> 
  <tr> 
   <td><p>/전달하는 경우/*</p> </td> 
   <td><p>작업 영역 최종 사용자 웹 애플리케이션</p> </td> 
   <td><p>예</p> </td> 
   <td><p>예</p> </td> 
  </tr> 
  <tr> 
   <td><p>/workspace-server/*</p> </td> 
   <td><p>작업 공간 클라이언트 응용 프로그램에 필요한 작업 공간 서비스 및 데이터 서비스</p> </td> 
   <td><p>예</p> </td> 
   <td><p>예</p> </td> 
  </tr> 
  <tr> 
   <td><p>/adobe-bootstrapper/*</p> </td> 
   <td><p>JEE 저장소의 AEM Forms 부트스트래핑용 서블릿</p> </td> 
   <td><p>아니오</p> </td> 
   <td><p>아니오</p> </td> 
  </tr> 
  <tr> 
   <td><p>/soap/*</p> </td> 
   <td><p>양식 서버 웹 서비스를 위한 정보 페이지</p> </td> 
   <td><p>아니오</p> </td> 
   <td><p>아니오</p> </td> 
  </tr> 
  <tr> 
   <td><p>/soap/services/*</p> </td> 
   <td><p>모든 양식 서버 서비스에 대한 웹 서비스 URL</p> </td> 
   <td><p>아니오</p> </td> 
   <td><p>아니오</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edc/admin/*</p> </td> 
   <td><p>Rights Management 관리 웹 응용 프로그램</p> </td> 
   <td><p>예</p> </td> 
   <td><p>아니오</p> </td> 
  </tr> 
  <tr> 
   <td><p>/adminui/*</p> </td> 
   <td><p>관리 콘솔 홈 페이지</p> </td> 
   <td><p>예</p> </td> 
   <td><p>아니오</p> </td> 
  </tr> 
  <tr> 
   <td><p>/TruststoreComponent/</p> <p>보안/*</p> </td> 
   <td><p>Trust Store Management 관리 페이지</p> </td> 
   <td><p>예</p> </td> 
   <td><p>아니오</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormsIVS/*</p> </td> 
   <td><p>양식 렌더링 테스트 및 디버깅을 위한 Forms IVS 애플리케이션</p> </td> 
   <td><p>예</p> </td> 
   <td><p>아니오</p> </td> 
  </tr> 
  <tr> 
   <td><p>/OutputIVS/*</p> </td> 
   <td><p>출력 서비스 테스트 및 디버깅을 위한 IVS 애플리케이션 출력</p> </td> 
   <td><p>예</p> </td> 
   <td><p>아니오</p> </td> 
  </tr> 
  <tr> 
   <td><p>/rmws/*</p> </td> 
   <td><p>권한 관리를 위한 REST URL</p> </td> 
   <td><p>아니오</p> </td> 
   <td><p>예</p> </td> 
  </tr> 
  <tr> 
   <td><p>/OutputAdmin/*</p> </td> 
   <td><p>출력 관리 페이지</p> </td> 
   <td><p>예</p> </td> 
   <td><p>아니오</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServer/*</p> </td> 
   <td><p>Forms 웹 애플리케이션 파일</p> </td> 
   <td><p>예</p> </td> 
   <td><p>아니오</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServer/GetImage</p> <p>서블릿</p> </td> 
   <td><p>HTML 변환 중 JavaScript를 가져오는 데 사용</p> </td> 
   <td><p>아니오</p> </td> 
   <td><p>아니오</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServerAdmin/*</p> </td> 
   <td><p>양식 관리 페이지</p> </td> 
   <td><p>예</p> </td> 
   <td><p>아니오</p> </td> 
  </tr> 
  <tr> 
   <td><p>/repository/*</p> </td> 
   <td><p>WebDAV(디버깅) 액세스에 대한 URL</p> </td> 
   <td><p>예</p> </td> 
   <td><p>아니오</p> </td> 
  </tr> 
  <tr> 
   <td><p>/AACComponent/*</p> </td> 
   <td><p>애플리케이션 및 서비스 사용자 인터페이스</p> </td> 
   <td><p>예</p> </td> 
   <td><p>아니오</p> </td> 
  </tr> 
  <tr> 
   <td><p>/WorkspaceAdmin/*</p> </td> 
   <td><p>작업 영역 관리 페이지</p> </td> 
   <td><p>예</p> </td> 
   <td><p>아니오</p> </td> 
  </tr> 
  <tr> 
   <td><p>/rest/*</p> </td> 
   <td><p>나머지 지원 페이지</p> </td> 
   <td><p>예</p> </td> 
   <td><p>아니오</p> </td> 
  </tr> 
  <tr> 
   <td><p>/CoreSystemConfig/*</p> </td> 
   <td><p>JEE 코어 구성 설정 페이지의 AEM Forms</p> </td> 
   <td><p>예</p> </td> 
   <td><p>아니오</p> </td> 
  </tr> 
  <tr> 
   <td><p>/um/</p> </td> 
   <td><p>사용자 관리 인증</p> </td> 
   <td><p>아니오</p> </td> 
   <td><p>예</p> </td> 
  </tr> 
  <tr> 
   <td><p>/um/*</p> </td> 
   <td><p>사용자 관리 인터페이스</p> </td> 
   <td><p>예</p> </td> 
   <td><p>아니오</p> </td> 
  </tr> 
  <tr> 
   <td><p>/DocumentManager/*</p> </td> 
   <td><p>원격 엔드포인트, SOAP WSDL 엔드포인트 및 SOAP 전송 또는 HTTP 문서를 사용하는 EJB 전송을 통해 Java SDK에 액세스할 때 처리될 문서의 업로드 및 다운로드</p> </td> 
   <td><p>예</p> </td> 
   <td><p>예</p> </td> 
  </tr> 
 </tbody> 
</table>

## 교차 사이트 요청 위조 공격으로부터 보호 {#protecting-from-cross-site-request-forgery-attacks}

CSRF(교차 사이트 요청 위조) 공격은 웹 사이트에서 사용자에 대해 보유하고 있는 트러스트를 악용하여 사용자가 인증하지 않은 명령을 전송합니다. 이 공격은 사용자가 이미 인증된 다른 사이트에 액세스하기 위해 웹 페이지에 링크나 스크립트 또는 이메일 메시지의 URL을 포함하는 것으로 설정됩니다.

예를 들어 다른 웹 사이트를 동시에 탐색하면서 관리 콘솔에 로그인할 수 있습니다. 웹 페이지 중 하나에 희생자 웹 사이트에서 서버측 스크립트를 대상으로 하는 `src` 특성이 있는 HTML 이미지 태그가 포함될 수 있습니다. 웹 브라우저가 제공하는 쿠키 기반 세션 인증 메커니즘을 활용하여 공격적인 웹 사이트는 피해 서버측 스크립트로 악성 요청을 보내 합법적 사용자로 가장할 수 있습니다. 자세한 예는 https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)#Examples을 [참조하십시오](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)#Examples).

CSRF에는 다음과 같은 특성이 일반적입니다.

* 사용자의 ID를 사용하는 사이트를 포함할 수 있습니다.
* 해당 ID에 대한 사이트의 신뢰를 활용합니다.
* 사용자 브라우저를 대상 사이트로 HTTP 요청을 보내도록 조작합니다.
* 부작용이 있는 HTTP 요청을 포함합니다.

JEE의 AEM Forms은 레퍼러 필터 기능을 사용하여 CSRF 공격을 차단합니다. 이 섹션에서는 레퍼러 필터링 메커니즘을 설명하는 데 다음 용어가 사용됩니다.

* **허용된 레퍼러:** 레퍼러는 서버에 요청을 보내는 소스 페이지의 주소입니다. JSP 페이지 또는 양식의 경우 레퍼러는 일반적으로 검색 내역에서 이전 페이지입니다. 이미지의 레퍼러는 일반적으로 이미지가 표시되는 페이지입니다. 서버 리소스에 액세스할 수 있는 레퍼러를 허용된 레퍼러 목록에 추가하여 식별할 수 있습니다.
* **허용된 레퍼러 예외:** 허용된 레퍼러 목록에서 특정 레퍼러에 대한 액세스 범위를 제한할 수 있습니다. 이 제한을 적용하려면 해당 레퍼러의 개별 경로를 허용된 레퍼러 예외 목록에 추가할 수 있습니다. 허용된 레퍼러 예외 목록의 경로에서 시작된 요청은 양식 서버의 리소스를 호출할 수 없습니다. 특정 응용 프로그램에 대해 허용되는 레퍼러 예외를 정의할 수 있으며 모든 응용 프로그램에 적용되는 글로벌 예외 목록을 사용할 수도 있습니다.
* **허용된 URI:** 레퍼러 헤더를 확인하지 않고 제공할 리소스 목록입니다. 예를 들어 서버에서 상태 변경을 발생시키지 않는 도움말 페이지를 이 목록에 추가할 수 있습니다. 허용된 URI 목록의 리소스는 레퍼러가 누구인지에 관계없이 레퍼러 필터에 의해 차단되지 않습니다.
* **Null 레퍼러:** 상위 웹 페이지에서 연결되어 있지 않거나 가져오지 않은 서버 요청은 Null 레퍼러의 요청으로 간주됩니다. 예를 들어 새 브라우저 창을 열고 주소를 입력한 다음 Enter 키를 누르면 서버에 전송된 레퍼러가 null입니다. 웹 서버에 HTTP 요청을 하는 데스크톱 응용 프로그램(.NET 또는 SWING)도 Null 레퍼러를 서버로 보냅니다.

### 레퍼러 필터링 {#referer-filtering}

레퍼러 필터링 프로세스는 다음과 같이 설명할 수 있습니다.

1. 양식 서버는 호출에 사용되는 HTTP 메서드를 확인합니다.

   1. POST인 경우 양식 서버가 레퍼러 헤더 확인을 수행합니다.
   1. GET이면 양식 서버가 레퍼러 확인을 건너뜁니다. 단, CSRF_CHECK_GETS가 *true로 설정되어 있지* 않으면 참조 헤더 확인을 수행합니다. *CSRF_CHECK* _GETS는 응용 프로그램의 *web.xml* 파일에 지정됩니다.

1. 양식 서버는 요청된 URI가에 있는지 여부를 허용 목록에 추가하다 확인합니다.

   1. URI가 허용 목록에추가된 있는 경우 서버가 요청을 수락합니다.
   1. 요청한 URI가 허용 목록에추가된 없으면 서버는 요청의 레퍼러를 검색합니다.

1. 요청에 레퍼러가 있는 경우 서버는 레퍼러가 허용된 참조인지 여부를 확인합니다. 허용되는 경우 서버는 레퍼러 예외를 확인합니다.

   1. 예외인 경우 요청이 차단됩니다.
   1. 예외가 아닌 경우 요청이 전달됩니다.

1. 요청에 레퍼러가 없으면 서버는 Null 레퍼러가 허용되는지 여부를 확인합니다.

   1. Null 레퍼러가 허용되면 요청이 전달됩니다.
   1. Null 레퍼러가 허용되지 않으면 서버는 요청된 URI가 Null 레퍼러의 예외인지 확인하고 그에 따라 요청을 처리합니다.

### 레퍼러 필터링 관리 {#managing-referer-filtering}

JEE의 AEM Forms은 레퍼러 필터를 제공하여 서버 리소스에 액세스할 수 있는 레퍼러를 지정합니다. 기본적으로 레퍼러 필터는 CSRF_CHECK_GETS가 *true로 설정되어 있지 않은 경우, 안전 HTTP 메서드를 사용하는 요청을 필터링하지* 않습니다. 허용된 레퍼러 항목의 포트 번호가 0으로 설정된 경우 JEE의 AEM Forms은 포트 번호와 관계없이 해당 호스트의 레퍼러가 있는 모든 요청을 허용합니다. 포트 번호가 지정되지 않은 경우 기본 포트 80(HTTP) 또는 포트 443(HTTPS)의 요청만 허용됩니다. 허용된 레퍼러 목록의 모든 항목이 삭제된 경우 레퍼러 필터링이 비활성화됩니다.

Document Services를 처음 설치하면 허용된 레퍼러 목록이 문서 서비스가 설치된 서버의 주소로 업데이트됩니다. 서버 항목에는 서버 이름, IPv4 주소, IPv6가 활성화된 경우 IPv6 주소, 루프백 주소 및 localhost 항목이 포함됩니다. 허용된 레퍼러 목록에 추가된 이름은 호스트 운영 체제에서 반환됩니다. 예를 들어 IP 주소가 10.40.54.187인 서버에는 다음 항목이 포함됩니다. `https://server-name:0, https://10.40.54.187:0, https://127.0.0.1:0, http://localhost:0`. 호스트 운영 체제에 의해 재조정된 비정규적인 이름(IPv4 주소, IPv6 주소 또는 정규화된 도메인 이름이 없는 이름)허용 목록에 추가하다에 대해서는 업데이트되지 않습니다. 비즈니스 환경에 맞게 허용된 레퍼러 목록을 수정합니다. 기본 허용된 레퍼러 목록으로 양식 서버를 프로덕션 환경에 배포하지 마십시오. 허용된 레퍼러, 레퍼러 예외 또는 URI를 수정한 후에는 변경 사항이 적용되도록 서버를 다시 시작해야 합니다.

**허용된 레퍼러 목록 관리**

관리 콘솔의 사용자 관리 인터페이스에서 허용된 레퍼러 목록을 관리할 수 있습니다. 사용자 관리 인터페이스는 목록을 생성, 편집 또는 삭제할 수 있는 기능을 제공합니다. 허용된 레퍼러 목록 [작업에 대한 자세한 내용은](/help/forms/using/admin-help/preventing-csrf-attacks.md)관리 도움말의 ** CSRF 공격* 방지* 섹션을 참조하십시오.

**허용된 레퍼러 예외 및 허용된 URI 목록 관리**

JEE의 AEM Forms은 허용된 레퍼러 예외 목록 및 허용된 URI 목록을 관리하기 위한 API를 제공합니다. 이러한 API를 사용하여 목록을 검색, 생성, 편집 또는 삭제할 수 있습니다. 사용 가능한 API 목록은 다음과 같습니다.

* createAllowedURIsList
* getAllowedURIsList
* updateAllowedURIsList
* deleteAllowedURIsList
* addAllowedReferrerExceptions
* getAllowedReferrerExceptions
* updateAllowedReferrerExceptions
* deleteAllowedReferrerExceptions

API에 대한 자세한 내용은 JEE API 참조*의* AEM Forms을 참조하십시오.

글로벌 수준(예: 모든 응용 프로그램에 적용되는 예외)를 정의하려면 ***LC_GLOBAL_ALLOWED_REFERRER_EXCEPTION*** 목록을 사용합니다. 이 목록에는 절대 경로(예: `/index.html`) 또는 상대 경로(예: `/sample/`). 상대적 URI 끝에 정규 표현식을 추가할 수도 있습니다(예: `/sample/(.)*`.

LC_ ***GLOBAL_ALLOWED_REFERER_EXCEPTION*** 목록 ID는 에 있는 `UMConstants` 네임스페이스의 `com.adobe.idp.um.api` 클래스에 상수로 정의됩니다 `adobe-usermanager-client.jar`. AEM Forms API를 사용하여 이 목록을 생성, 수정 또는 편집할 수 있습니다. 예를 들어, 전역 허용 레퍼러 예외 목록을 만들려면 다음을 사용합니다.

```as3
addAllowedRefererExceptions(UMConstants.LC_GLOBAL_ALLOWED_REFERER_EXCEPTION, Arrays.asList("/index.html", "/sample/(.)*"))
```

애플리케이션별 예외 ***에 CSRF_ALLOWED_REFERRER_EXCEPTIONS*** 목록을 사용하십시오.

**레퍼러 필터 비활성화**

레퍼러 필터가 양식 서버에 대한 액세스를 완전히 차단하며 허용된 레퍼러 목록을 편집할 수 없는 경우 서버 시작 스크립트를 업데이트하고 레퍼러 필터링을 비활성화할 수 있습니다.

시작 스크립트에 `-Dlc.um.csrffilter.disabled=true` JAVA 인수를 포함시키고 서버를 다시 시작합니다. 허용된 레퍼러 목록을 적절히 재구성한 후 JAVA 인수를 삭제해야 합니다.

**사용자 지정 WAR 파일에 대한 레퍼러 필터링**

비즈니스 요구 사항을 충족하기 위해 JEE에서 AEM Forms과 함께 사용할 사용자 정의 WAR 파일을 만들 수 있습니다. 사용자 정의 WAR 파일에 대한 레퍼러 필터링을 활성화하려면 WAR의 클래스 경로에 ***adobe-usermanager-client.jar*** 를 포함하고 다음 매개 변수와 함께* web.xml* 파일에 필터 항목을 포함합니다.

**CSRF_CHECK_GETS는** GET 요청에 대한 레퍼러 확인을 제어합니다. 이 매개 변수가 정의되지 않은 경우 기본값은 false로 설정됩니다. GET 요청을 필터링하려는 경우에만 이 매개 변수를 포함하십시오.

**CSRF_ALLOWED_REFERRER_EXCEPTIONS** 는 허용된 레퍼러 예외 목록의 ID입니다. 레퍼러 필터는 목록 ID로 식별된 목록의 레퍼러가 양식 서버의 리소스를 호출하지 못하도록 합니다.

**CSRF_ALLOWED_URIS_LIST** _NAME은 허용된 URI 목록의 ID입니다. 레퍼러 필터는 요청에 있는 레퍼러 헤더의 값에 상관없이 목록 ID로 식별되는 목록에 있는 리소스에 대한 요청을 차단하지 않습니다.

**CSRF_ALLOW_NULL_REFERRER는** 레퍼러가 null이거나 없을 때 레퍼러 필터 동작을 제어합니다. 이 매개 변수가 정의되지 않은 경우 기본값은 false로 설정됩니다. Null 레퍼러를 허용하려는 경우에만 이 매개 변수를 포함하십시오. null 레퍼러를 허용하면 일부 유형의 교차 사이트 요청 위조 공격이 허용될 수 있습니다.

**CSRF_NULL_REFERRER_EXCEPTIONS** 는 레퍼러가 null일 때 레퍼러 검사가 수행되지 않는 URI 목록입니다. 이 매개 변수는 *CSRF_ALLOW_NULL_REFERER가* false로 설정된 경우에만 활성화됩니다. 목록에서 여러 URI를 쉼표로 구분합니다.

다음은 *SAMPLE* WAR 파일의 web.xml ***파일에 있는 필터 항목의*** 예입니다.

```as3
<filter> 
       <filter-name> filter-name </filter-name> 
       <filter-class> com.adobe.idp.um.auth.filter.RemoteCSRFFilter </filter-class> 
     <!-- default is false --> 
     <init-param> 
      <param-name> CSRF_ALLOW_NULL_REFERER </param-name> 
      <param-value> false </param-value> 
     </init-param> 
     <!-- default is false --> 
     <init-param> 
      <param-name> CSRF_CHECK_GETS </param-name> 
      <param-value> true </param-value> 
     </init-param> 
     <!-- Optional --> 
     <init-param> 
       <param-name> CSRF_NULL_REFERER_EXCEPTIONS </param-name> 
       <param-value> /SAMPLE/login, /SAMPLE/logout  </param-value> 
     </init-param> 
     <!-- Optional --> 
     <init-param> 
      <param-name> CSRF_ALLOWED_REFERER_EXCEPTIONS </param-name> 
      <param-value> SAMPLE_ALLOWED_REF_EXP_ID </param-value> 
     </init-param> 
     <!-- Optional --> 
     <init-param> 
      <param-name> CSRF_ALLOWED_URIS_LIST_NAME </param-name> 
      <param-value> SAMPLE_ALLOWED_URI_LIST_ID     </param-value> 
     </init-param> 
</filter> 
    ........ 
    <filter-mapping> 
      <filter-name> filter-name </filter-name> 
      <url-pattern>/*</url-pattern> 
    </filter-mapping>
```

**문제 해결**

CSRF 필터에 의해 올바른 서버 요청이 차단되는 경우 다음 중 하나를 시도해 보십시오.

* 거부된 요청에 레퍼러 헤더가 있는 경우, 허용된 레퍼러 목록에 추가하는 것이 좋습니다. 신뢰하는 레퍼러만 추가합니다.
* 거부된 요청에 레퍼러 헤더가 없는 경우 레퍼러 헤더를 포함하도록 클라이언트 응용 프로그램을 수정합니다.
* 클라이언트가 브라우저에서 작동할 수 있으면 배포 모델을 사용해 보십시오.
* 마지막 방법으로 허용된 URI 목록에 리소스를 추가할 수 있습니다. 권장 설정이 아닙니다.

## 보안 네트워크 구성 {#secure-network-configuration}

이 섹션에서는 JEE의 AEM Forms에 필요한 프로토콜 및 포트를 설명하고 보안 네트워크 구성으로 JEE에 AEM Forms을 배포하기 위한 권장 사항을 제공합니다.

### JEE의 AEM Forms에서 사용하는 네트워크 프로토콜 {#network-protocols-used-by-aem-forms-on-jee}

이전 섹션에 설명된 보안 네트워크 아키텍처를 구성하는 경우 JEE의 AEM Forms과 기업 네트워크의 다른 시스템 간의 상호 작용에 다음 네트워크 프로토콜이 필요합니다.

<table> 
 <thead> 
  <tr> 
   <th><p>프로토콜</p> </th> 
   <th><p>사용</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>HTTP</p> </td> 
   <td> 
    <ul> 
     <li><p>브라우저에 구성 관리자 및 최종 사용자 웹 응용 프로그램이 표시됩니다.</p> </li> 
     <li><p>모든 SOAP 연결</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>SOAP</p> </td> 
   <td> 
    <ul> 
     <li><p>.NET 응용 프로그램과 같은 웹 서비스 클라이언트 응용 프로그램</p> </li> 
     <li><p>Adobe Reader®는 JEE 서버 웹 서비스의 AEM Forms에 SOAP를 사용합니다</p> </li> 
     <li><p>Adobe Flash® 애플리케이션은 SOAP를 사용하여 양식 서버 웹 서비스 제공</p> </li> 
     <li><p>SOAP 모드에서 사용될 경우 JEE SDK 호출 AEM Forms</p> </li> 
     <li><p>워크벤치 디자인 환경</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>RMI</p> </td> 
   <td><p>EJB(Enterprise JavaBeans) 모드에서 사용될 때 JEE SDK 호출 AEM Forms</p> </td> 
  </tr> 
  <tr> 
   <td><p>IMAP/POP3</p> </td> 
   <td> 
    <ul> 
     <li><p>서비스에 대한 이메일 기반 입력(이메일 끝점)</p> </li> 
     <li><p>이메일을 통한 사용자 작업 알림</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>UNC 파일 IO</p> </td> 
   <td><p>서비스에 대한 감시 폴더의 JEE 모니터링에 있는 AEM Forms(감시 폴더 끝점)</p> </td> 
  </tr> 
  <tr> 
   <td><p>LDAP</p> </td> 
   <td> 
    <ul> 
     <li><p>디렉토리에서 조직 사용자 및 그룹 정보의 동기화</p> </li> 
     <li><p>대화형 사용자를 위한 LDAP 인증</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>JDBC</p> </td> 
   <td> 
    <ul> 
     <li><p>JDBC 서비스를 사용하는 프로세스를 실행하는 동안 외부 데이터베이스에 대한 쿼리 및 프로시저 호출</p> </li> 
     <li><p>JEE 저장소의 내부 액세스 AEM Forms</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>WebDAV</p> </td> 
   <td><p>WebDAV 클라이언트에서 JEE 디자인 타임 저장소(양식, 조각 등)의 AEM Forms을 원격 검색할 수 있습니다.</p> </td> 
  </tr> 
  <tr> 
   <td><p>AMF</p> </td> 
   <td><p>Adobe Flash 응용 프로그램. 여기서 JEE 서버 서비스의 AEM Forms은 원격 끝점으로 구성됩니다</p> </td> 
  </tr> 
  <tr> 
   <td><p>JMX</p> </td> 
   <td><p>JEE의 AEM Forms이 JMX를 사용하여 모니터링하기 위해 MBeans를 노출함</p> </td> 
  </tr> 
 </tbody> 
</table>

### 응용 프로그램 서버용 포트 {#ports-for-application-servers}

이 섹션에서는 지원되는 각 애플리케이션 서버 유형의 기본 포트(및 대체 구성 범위)에 대해 설명합니다. JEE에서 AEM Forms을 실행하는 응용 프로그램 서버에 연결하는 클라이언트를 허용하려는 네트워크 기능에 따라 내부 방화벽에서 이 포트를 활성화하거나 비활성화해야 합니다.

>[!NOTE]
>
>기본적으로 서버가 adobe.com 네임스페이스 아래에 여러 JMX MBeans를 노출합니다. 서버 상태 모니터링에 유용한 정보만 노출됩니다. 그러나 정보가 유출되지 않도록 하려면 신뢰할 수 없는 네트워크의 호출자가 JMX MBans를 조회하고 상태 지표에 액세스하지 못하도록 해야 합니다.

**JBoss 포트**

<table> 
 <thead> 
  <tr> 
   <th><p>목적</p> </th> 
   <th><p>포트</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>웹 애플리케이션 액세스</p> </td> 
   <td><p>[JBOSS_Root]/standalone/configuration/lc_[database].xml</p> <p>HTTP/1.1 커넥터 포트 8080</p> <p>AJP 1.3 커넥터 포트 8009</p> <p>SSL/TLS 커넥터 포트 8443</p> </td> 
  </tr> 
  <tr> 
   <td><p>CORBA 지원</p> </td> 
   <td><p>[JBoss 루트]/server/all/conf/jacorb.properties</p> <p>OAPort 3528</p> <p>OASLPort 3529</p> </td> 
  </tr> 
 </tbody> 
</table>

**WebLogic 포트**

<table> 
 <thead> 
  <tr> 
   <th><p>목적</p> </th> 
   <th><p>포트</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>웹 애플리케이션 액세스</p> </td> 
   <td> 
    <ul> 
     <li><p>관리 서버 수신 포트: 기본값은 7001입니다.</p> </li> 
     <li><p>관리 서버 SSL 수신 포트: 기본값은 7002입니다.</p> </li> 
     <li><p>관리 서버에 대해 구성된 포트(예: 8001)</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>JEE의 AEM Forms에 액세스할 때 WebLogic 관리 포트가 필요하지 않음</p> </td> 
   <td> 
    <ul> 
     <li><p>관리 서버 수신 포트: 1부터 65534까지 구성 가능</p> </li> 
     <li><p>관리 서버 SSL 수신 포트: 1부터 65534까지 구성 가능</p> </li> 
     <li><p>노드 관리자 수신 포트: 기본값은 5556입니다.</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

**WebSphere 포트**

JEE의 AEM Forms에 필요한 WebSphere 포트에 대한 자세한 내용은 WebSphere Application Server UI의 포트 번호 설정으로 이동하십시오.

### SSL 구성 {#configuring-ssl}

JEE 물리적 아키텍처의 섹션 [AEM Forms에 설명된 물리적 아키텍처를](hardening-aem-forms-jee-environment.md#aem-forms-on-jee-physical-architecture)참조하려면 사용하려는 모든 연결에 대해 SSL을 구성해야 합니다. 특히 모든 SOAP 연결은 SSL을 통해 수행되어야 네트워크에서 사용자 자격 증명이 노출되지 않습니다.

JBoss, WebLogic 및 WebSphere에서 SSL을 구성하는 방법에 대한 지침은 [관리 도움말의 &quot;SSL 구성&quot;을 참조하십시오](https://www.adobe.com/go/learn_aemforms_admin_64).

AEM Forms 서버에 대해 구성된 JVM(Java Virtual Machine)으로 인증서를 가져오는 방법에 대한 지침은 [AEM Forms 워크벤치 도움말의 상호 인증 섹션을 참조하십시오](http://www.adobe.com/go/learn_aemforms_workbench_65).

### SSL 리디렉션 구성 {#configuring-ssl-redirect}

응용 프로그램 서버를 SSL을 지원하도록 구성한 후 응용 프로그램 및 서비스에 대한 모든 HTTP 트래픽이 SSL 포트를 사용하도록 적용되었는지 확인해야 합니다.

WebSphere 또는 WebLogic에 대한 SSL 리디렉션을 구성하려면 애플리케이션 서버 설명서를 참조하십시오.

1. 명령 프롬프트를 열고 /JBOSS_HOME/standalone/configuration 디렉토리로 이동한 후 다음 명령을 실행합니다.

   `keytool -genkey -alias jboss7 -keyalg RSA -keystore server.keystore -validity 10950`

1. 편집할 JBOSS_HOME/standalone/configuration/standalone.xml 파일을 엽니다.

   &lt;subsystem xmlns=&quot;urn:jboss:domain:web:1.1&quot; native=&quot;false&quot; default-virtual-server=&quot;default-host&quot;> 요소 뒤에 다음 세부 정보를 추가합니다.

   &lt;connector name=&quot;https&quot; protocol=&quot;HTTP/1.1&quot; scheme=&quot;https&quot; socket-binding=&quot;https&quot; enabled=&quot;true&quot; secure=&quot;true&quot;/>

1. https 커넥터 요소에 다음 코드를 추가합니다.

   ```
   <connector name="https" protocol="HTTP/1.1" scheme="https" socket-binding="https" secure="true" enabled="true"> 
    <ssl name="jboss7_ssl" key-alias="jboss71" password="Tibco321" certificate-key-file="../standalone/configuration/server.keystore" protocol="TLSv1"/> 
    </connector>
   ```

   standalone.xml 파일을 저장하고 닫습니다.

## Windows 전용 보안 추천 {#windows-specific-security-recommendations}

이 섹션에는 JEE에서 AEM Forms을 실행하는 데 사용될 때 Windows에만 적용되는 보안 권장 사항이 포함되어 있습니다.

### JBoss 서비스 계정 {#jboss-service-accounts}

JEE 턴키 설치의 AEM Forms은 기본적으로 로컬 시스템 계정을 사용하여 서비스 계정을 설정합니다. 기본 제공 로컬 시스템 사용자 계정은 높은 접근성을 가집니다. 관리자 그룹의 일부입니다. 작업자 프로세스 ID가 로컬 시스템 사용자 계정으로 실행되는 경우 해당 작업자 프로세스는 전체 시스템에 대한 전체 액세스 권한을 가집니다.

#### 관리자가 아닌 계정을 사용하여 응용 프로그램 서버 실행 {#run-the-application-server-using-a-non-administrative-account}

1. MMC(Microsoft Management Console)에서 양식 서버 서비스에 로그인할 로컬 사용자를 만듭니다.

   * [ **사용자가 암호를 변경할 수 없음]을 선택합니다**.
   * [ **구성원] 탭에서** [사용자] 그룹이 나열되는지 확인합니다.

1. [ **설정** ] > **[관리 도구** ] > [ **서비스]를**&#x200B;선택합니다.
1. 응용 프로그램 서버 서비스를 두 번 클릭하고 서비스를 중지합니다.
1. [ **로그온** ] 탭에서 [이 계정 ****]을 선택하고 만든 사용자 계정을 찾은 후 계정의 암호를 입력합니다.
1. 로컬 보안 설정 창의 사용자 권한 할당에서 양식 서버가 실행 중인 사용자 계정에 다음 권한을 부여합니다.

   * 터미널 서비스를 통해 로그온 거부
   * 로컬에서 로그인 거부
   * 서비스로 로그온(이미 설정되어야 함)

1. 새 사용자 계정에 다음 디렉토리에 대한 수정 권한을 지정합니다.
   * **GDS(Global Document Storage) 디렉토리**: GDS 디렉토리의 위치는 AEM Forms 설치 과정에서 수동으로 구성됩니다. 설치 중에 위치 설정이 비어 있는 상태로 남아 있는 경우, 위치는 응용 프로그램 서버 설치 시 `[JBoss root]/server/[type]/svcnative/DocumentStorage`
   * **CRX-Repository 디렉토리**: 기본 위치는 `[AEM-Forms-installation-location]\crx-repository`
   * **AEM Forms 임시 디렉토리**:
      * (Windows) 환경 변수에 설정된 TMP 또는 TEMP 경로
      * (AIX, Linux 또는 Solaris) 로그인한 사용자의 홈 디렉토리UNIX 기반 시스템에서 루트 이외의 사용자는 다음 디렉토리를 임시 디렉토리로 사용할 수 있습니다.
      * (Linux) /var/tmp 또는 /usr/tmp
      * (AIX) /tmp 또는 /usr/tmp
      * (Solaris) /var/tmp 또는 /usr/tmp
1. 새 사용자 계정에 다음 디렉토리에 대한 쓰기 권한을 지정합니다.
   * [JBoss-directory]\standalone\deployment
   * [JBoss-directory]\standalone\
   * [JBoss-directory]\bin\

   >[!NOTE]
   >
   > JBoss Application Server의 기본 설치 위치:
   > * Windows: C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   > * Linux: /opt/jboss/.


1. 응용 프로그램 서버 서비스를 시작합니다.

### 파일 시스템 보안 {#file-system-security}

JEE의 AEM Forms은 다음 방법으로 파일 시스템을 사용합니다.

* 문서 입력 및 출력을 처리하는 동안 사용되는 임시 파일을 저장합니다.
* 설치된 솔루션 구성 요소를 지원하는 데 사용되는 글로벌 아카이브 저장소에 파일을 저장합니다
* 감시 폴더에는 파일 시스템 폴더 위치에서 서비스에 입력되는 삭제된 파일이 저장됩니다

양식 서버 서비스를 통해 문서를 전송하고 수신할 수 있는 방편으로 감시 폴더를 사용하는 경우 파일 시스템 보안에 각별히 주의하십시오. 사용자가 감시 폴더의 컨텐츠를 드롭하면 해당 컨텐츠가 감시 폴더를 통해 노출됩니다. 이 경우 서비스는 실제 최종 사용자를 인증하지 않습니다. 대신 ACL 및 공유 수준 보안을 사용하여 폴더 수준에서 설정하여 서비스를 효과적으로 호출할 수 있는 사용자를 결정합니다.

## JBoss 특정 보안 추천 {#jboss-specific-security-recommendations}

이 섹션에는 JEE에서 AEM Forms을 실행하는 데 사용되는 경우 JBoss 7.0.6에 특정한 응용 프로그램 서버 구성 권장 사항이 포함됩니다.

### JBoss 관리 콘솔 및 JMX 콘솔 비활성화 {#disable-jboss-management-console-and-jmx-console}

턴키 설치 방법을 사용하여 JBoss의 JEE에 AEM Forms을 설치할 때 JBoss 관리 콘솔 및 JMX 콘솔에 대한 액세스가 이미 구성되었습니다(JMX 모니터링이 비활성화됨). 자신의 JBoss Application Server를 사용하는 경우 JBoss Management Console 및 JMX 모니터링 콘솔에 대한 액세스 보안이 유지되는지 확인하십시오. JMX 모니터링 콘솔에 대한 액세스는 jmx-invoker-service.xml이라는 JBoss 구성 파일에서 설정됩니다.

### 디렉토리 검색 비활성화 {#disable-directory-browsing}

관리 콘솔에 로그인한 후에는 URL을 수정하여 콘솔의 디렉토리 목록을 찾아볼 수 있습니다. 예를 들어 URL을 다음 URL 중 하나로 변경하면 디렉토리 목록이 나타날 수 있습니다.

```as3
https://<servername>:8080/adminui/secured/ 
https://<servername>:8080/um/
```

## WebLogic 특정 보안 추천 {#weblogic-specific-security-recommendations}

이 섹션에는 JEE에서 AEM Forms을 실행할 때 WebLogic 9.1의 보안을 유지하기 위한 응용 프로그램 서버 구성 권장 사항이 포함되어 있습니다.

### 디렉토리 검색 비활성화 {#disable_directory_browsing-1}

다음 예제와 같이 weblogic.xml 파일의 index-directories 속성 `false`을 로 설정합니다.

```as3
<container-descriptor> 
    <index-directory-enabled>false 
    </index-directory-enabled> 
</container-descriptor>
```

### WebLogic SSL 포트 사용 {#enable-weblogic-ssl-port}

기본적으로 WebLogic은 기본 SSL 수신 포트 7002를 활성화하지 않습니다. SSL을 구성하기 전에 WebLogic Server 관리 콘솔에서 이 포트를 활성화합니다.

## WebSphere 관련 보안 추천 {#websphere-specific-security-recommendations}

이 섹션에는 JEE에서 AEM Forms을 실행하는 WebSphere의 보안을 위한 애플리케이션 서버 구성 권장 사항이 포함되어 있습니다.

### 디렉토리 검색 비활성화 {#disable_directory_browsing-2}

ibm-web-ext.xml 파일의 `directoryBrowsingEnabled` 속성을 로 설정합니다 `false`.

### WebSphere 관리 보안 활성화 {#enable-websphere-administrative-security}

1. WebSphere 관리 콘솔에 로그인합니다.
1. 탐색 트리에서 **보안** > **전역 보안으로 이동합니다.**
1. 관리 **보안 활성화를 선택합니다**.
1. 애플리케이션 보안 **활성화** 및 **Java 2 보안**&#x200B;사용을 모두 선택 취소합니다.
1. 확인 **또는 적용** 을 **클릭합니다**.
1. 메시지 **상자** 에서 마스터 구성에 **직접 저장을 클릭합니다**.