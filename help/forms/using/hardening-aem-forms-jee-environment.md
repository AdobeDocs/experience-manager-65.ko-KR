---
title: JEE 환경에서 AEM Forms 강화
description: 회사 인트라넷에서 실행되는 JEE의 AEM Forms 보안을 강화하기 위한 다양한 보안 강화 설정에 대해 알아봅니다.
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
role: Admin,User
exl-id: 6fb260f9-d0f8-431e-8d4e-535b451e4124
solution: Experience Manager, Experience Manager Forms
feature: Security, Adaptive Forms
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '7608'
ht-degree: 1%

---

# JEE 환경에서 AEM Forms 강화 {#hardening-your-aem-forms-on-jee-environment}

회사 인트라넷에서 실행되는 JEE의 AEM Forms 보안을 강화하기 위한 다양한 보안 강화 설정에 대해 알아봅니다.

이 문서에서는 JEE에서 AEM Forms을 실행하는 서버 보안을 위한 권장 사항 및 모범 사례에 대해 설명합니다. 이 문서는 운영 체제 및 애플리케이션 서버에 대한 포괄적인 호스트 강화 문서가 아닙니다. 대신, 이 문서에서는 회사 인트라넷 내에서 실행 중인 JEE의 AEM Forms 보안을 강화하기 위해 구현해야 하는 다양한 보안 강화 설정에 대해 설명합니다. 그러나 JEE 애플리케이션 서버의 AEM Forms이 안전하게 유지되게 하려면 보안 모니터링, 감지 및 응답 절차도 구현해야 합니다.

이 문서에서는 설치 및 구성 수명 주기 동안 다음 단계 동안 적용해야 하는 경화 기술에 대해 설명합니다.

* **사전 설치:** JEE에 AEM Forms을 설치하기 전에 다음 기술을 사용하십시오.
* **설치:** AEM Forms on JEE 설치 프로세스 중에 이러한 기술을 사용합니다.
* **설치 후:** 설치 후 및 그 이후에 정기적으로 이러한 기술을 사용하십시오.

AEM Forms on JEE는 사용자 정의가 용이하며 다양한 환경에서 작업할 수 있습니다. 일부 권장 사항은 조직의 요구 사항에 맞지 않을 수 있습니다.

## 사전 설치 {#preinstallation}

JEE에 AEM Forms을 설치하기 전에 보안 솔루션을 네트워크 계층 및 운영 체제에 적용할 수 있습니다. 이 섹션에서는 몇 가지 문제에 대해 설명하고 이러한 영역의 보안 취약점을 줄이기 위한 권장 사항을 제공합니다.

**UNIX 및 Linux의 설치 및 구성**

루트 쉘을 사용하여 JEE에 AEM Forms을 설치하거나 구성해서는 안 됩니다. 기본적으로 파일은 /opt 디렉터리 아래에 설치되며 설치를 수행하는 사용자는 /opt 아래에 있는 모든 파일 권한이 필요합니다. 또는 이미 모든 파일 권한이 있는 개별 사용자의 /user 디렉토리에서 설치를 수행할 수 있습니다.

**Windows의 설치 및 구성**

턴키 방식을 사용하여 JBoss의 JEE에 AEM Forms을 설치하거나 PDF Generator을 설치하는 경우 Windows에서 관리자 자격으로 설치를 수행해야 합니다. 또한 기본 응용 프로그램 지원을 사용하여 Windows에 PDF Generator을 설치할 때 Microsoft Office를 설치한 동일한 Windows 사용자로 설치를 실행해야 합니다. 설치 권한에 대한 자세한 내용은 사용 중인 애플리케이션 서버용* JEE에 AEM Forms 설치 및 배포* 문서를 참조하십시오.

### 네트워크 계층 보안 {#network-layer-security}

네트워크 보안 취약성은 모든 인터넷 연결 또는 인트라넷 연결 응용 프로그램 서버에 가장 먼저 위협됩니다. 이 섹션에서는 이러한 취약점에 대해 네트워크의 호스트를 강화하는 프로세스에 대해 설명합니다. 네트워크 세그멘테이션, TCP/IP(Transmission Control Protocol/Internet Protocol) 스택 강화 및 호스트 보호를 위한 방화벽 사용을 해결합니다.

다음 표에서는 네트워크 보안 취약성을 줄이는 일반적인 프로세스를 설명합니다.

<table> 
 <thead> 
  <tr> 
   <th><p>문제</p> </th> 
   <th><p>설명</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>비무장 지대(DMZ)</p> </td> 
   <td><p>DMZ(Demilitarized Zone) 내에 양식 서버를 배포합니다. 세그먼테이션은 내부 방화벽 뒤에 배치된 JEE에서 AEM Forms을 실행하는 데 사용되는 애플리케이션 서버와 최소 두 가지 수준에 있어야 합니다. 웹 서버를 포함하는 DMZ에서 외부 네트워크를 분리하여 내부 네트워크와 분리해야 합니다. 방화벽을 사용하여 분리 레이어를 구현합니다. 각 네트워크 계층을 통과하는 트래픽을 분류하고 제어하여 필요한 데이터의 절대 최소값만 허용되도록 합니다.</p> </td> 
  </tr> 
  <tr> 
   <td><p>비공개 IP 주소</p> </td> 
   <td><p>AEM Forms 애플리케이션 서버에서 RFC 1918 개인 IP 주소와 함께 NAT(Network Address Translation)를 사용합니다. 전용 IP 주소(10.0.0.0/8, 172.16.0.0/12 및 192.168.0.0/16)를 할당하면 공격자가 인터넷을 통해 NAT 내부 호스트로/에서 트래픽을 라우팅하는 것이 더 어려워집니다.</p> </td> 
  </tr> 
  <tr> 
   <td><p>방화벽</p> </td> 
   <td><p>다음 기준을 사용하여 방화벽 솔루션을 선택합니다.</p> 
    <ul> 
     <li><p>프록시 서버를 지원하는 방화벽 구현 및/또는 <em>상태 검사</em> 단순한 패킷 필터링 솔루션 대신</p> </li> 
     <li><p>을 지원하는 방화벽 사용 <em>명시적으로 허용된 서비스를 제외한 모든 서비스 거부</em> 보안 패러다임.</p> </li> 
     <li><p>이중 홈 또는 다중 홈 방화벽 솔루션 구현 이 아키텍처는 가장 높은 수준의 보안을 제공하고 승인되지 않은 사용자가 방화벽 보안을 무시하는 것을 방지합니다.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>데이터베이스 포트</p> </td> 
   <td><p>데이터베이스에 기본 수신 포트를 사용하지 마십시오(MySQL - 3306, Oracle - 1521, MS SQL - 1433). 데이터베이스 포트 변경에 대한 자세한 내용은 데이터베이스 설명서를 참조하십시오.</p> <p>다른 데이터베이스 포트를 사용하는 것은 JEE의 전체 AEM Forms 구성에 영향을 줍니다. 기본 포트를 변경하는 경우 JEE의 AEM Forms에 대한 데이터 소스와 같은 다른 구성 영역에서 해당 사항을 수정해야 합니다.</p> <p>JEE의 AEM Forms에서 데이터 소스를 구성하는 방법에 대한 자세한 내용은 JEE의 AEM Forms 설치 및 업그레이드 또는 애플리케이션 서버에 대한 JEE의 AEM Forms으로 업그레이드 를 참조하십시오. <a href="/help/forms/using/introduction-aem-forms.md" target="_blank">AEM Forms 사용 안내서</a>.</p> </td> 
  </tr> 
 </tbody> 
</table>

### 운영 체제 보안 {#operating-system-security}

다음 표에서는 운영 체제에서 발견된 보안 취약점을 최소화하는 몇 가지 잠재적인 접근 방식에 대해 설명합니다.

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
   <td><p>공급업체 보안 패치 및 업그레이드가 적시에 적용되지 않을 경우 권한이 없는 사용자가 애플리케이션 서버에 액세스할 수 있는 위험이 증가합니다. 보안 패치를 프로덕션 서버에 적용하기 전에 테스트합니다.</p><p>또한 규칙적으로 패치를 확인하고 설치하는 정책 및 절차를 만듭니다.</p></td> 
  </tr> 
  <tr> 
   <td><p>바이러스 보호 소프트웨어</p></td> 
   <td><p>바이러스 스캐너는 서명을 스캔하거나 비정상적인 행동을 관찰하여 감염된 파일을 식별할 수 있습니다. 스캐너는 보통 로컬 하드 드라이브에 저장되어 있는 파일에 바이러스 서명을 보관합니다. 새로운 바이러스가 자주 발견되므로 바이러스 스캐너용으로 이 파일을 자주 업데이트하여 현재 바이러스를 모두 식별해야 합니다.</p></td> 
  </tr> 
  <tr> 
   <td><p>NTP(Network Time Protocol)</p></td> 
   <td><p>법의학적 분석을 위해 Forms 서버에서 정확한 시간을 유지합니다. NTP를 사용하여 인터넷에 직접 연결된 모든 시스템의 시간을 동기화합니다.</p></td> 
  </tr> 
 </tbody> 
</table>

운영 체제에 대한 추가 보안 정보는 [&quot;운영 체제 보안 정보&quot;](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#operating_system_security_information).

## 설치 {#installation}

이 섹션에서는 보안 취약점을 줄이기 위해 AEM Forms 설치 프로세스 중에 사용할 수 있는 기술에 대해 설명합니다. 경우에 따라 이러한 기술은 설치 프로세스의 일부인 옵션을 사용합니다. 다음 표에서는 이러한 기술에 대해 설명합니다.

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
   <td><p>소프트웨어를 설치하는 데 필요한 최소한의 권한을 사용합니다. 관리자 그룹에 없는 계정을 사용하여 컴퓨터에 로그인합니다. Windows에서는 실행 명령을 사용하여 AEM Forms on JEE 설치 관리자를 관리 사용자로 실행할 수 있습니다. UNIX 및 Linux 시스템에서 다음 명령을 사용합니다. <code>sudo</code> 소프트웨어를 설치합니다.</p> </td> 
  </tr> 
  <tr> 
   <td><p>소프트웨어 소스</p> </td> 
   <td><p>신뢰할 수 없는 소스에서 JEE에서 AEM Forms을 다운로드하거나 실행하지 마십시오.</p> <p>악성 프로그램에는 데이터 도용, 수정 및 삭제, 서비스 거부 등 여러 방법으로 보안을 침해하는 코드가 포함될 수 있다. Adobe DVD에서 또는 신뢰할 수 있는 소스에서만 JEE에 AEM Forms을 설치합니다.</p> </td> 
  </tr> 
  <tr> 
   <td><p>디스크 파티션</p> </td> 
   <td><p>전용 디스크 파티션에 JEE의 AEM Forms을 배치합니다. 디스크 세그먼테이션은 보안을 강화하기 위해 서버의 특정 데이터를 별도의 실제 디스크에 보관하는 프로세스입니다. 이러한 방식으로 데이터를 정렬하면 디렉토리 순회 공격의 위험이 줄어듭니다. JEE 콘텐츠 디렉터리에 AEM Forms을 설치할 수 있는 시스템 파티션과 별개인 파티션을 만들 계획입니다. (Windows에서 시스템 파티션에는 system32 디렉터리 또는 부팅 파티션이 들어 있습니다.)</p> </td> 
  </tr> 
  <tr> 
   <td><p>구성 요소</p> </td> 
   <td><p>기존 서비스를 평가하고 필요하지 않은 서비스는 비활성화하거나 제거합니다. 불필요한 구성 요소 및 서비스를 설치하지 마십시오.</p> <p>응용 프로그램 서버의 기본 설치에는 사용자의 사용에 필요하지 않은 서비스가 포함될 수 있습니다. 공격에 대한 시작 지점을 최소화하려면 배포 전에 모든 불필요한 서비스를 비활성화해야 합니다. 예를 들어 JBoss에서 META-INF/jboss-service.xml 설명자 파일에서 불필요한 서비스를 주석 처리할 수 있습니다.</p> </td> 
  </tr> 
  <tr> 
   <td><p>도메인 간 정책 파일</p> </td> 
   <td><p>의 존재 <code>crossdomain.xml</code> 서버에 있는 파일이 해당 서버를 즉시 약화시킬 수 있습니다. 도메인 목록을 가능한 제한적으로 만드는 것이 좋습니다. 을(를) 배치하지 마십시오 <code>crossdomain.xml</code> 안내서를 사용할 때 프로덕션으로 개발하는 동안 사용된 파일 <em>(사용하지 않음)</em>. 웹 서비스를 사용하는 안내서의 경우 해당 서비스가 안내서를 제공했던 서버에 있는 경우 <code>crossdomain.xml</code> 파일이 전혀 필요하지 않습니다. 그러나 서비스가 다른 서버에 있거나 클러스터가 포함된 경우 <code>crossdomain.xml</code> 파일이 필요합니다. 을(를) 참조하십시오 <a href="https://kb2.adobe.com/cps/142/tn_14213.html">https://kb2.adobe.com/cps/142/tn_14213.html</a>를 참조하십시오.</p> </td> 
  </tr> 
  <tr> 
   <td><p>운영 체제 보안 설정</p> </td> 
   <td><p>Solaris 플랫폼에서 192비트 또는 256비트 XML 암호화를 사용해야 하는 경우 다음을 설치해야 합니다 <code>pkcs11_softtoken_extra.so</code> 대신 <code>pkcs11_softtoken.so</code>.</p> </td> 
  </tr> 
 </tbody> 
</table>

## 설치 후 단계 {#post-installation-steps}

JEE에 AEM Forms을 성공적으로 설치한 후에는 보안 관점에서 환경을 주기적으로 유지 관리하는 것이 중요합니다.

다음 섹션에서는 배포된 Forms 서버의 보안을 유지하는 데 권장되는 다양한 작업에 대해 자세히 설명합니다.

### AEM Forms 보안 {#aem-forms-security}

다음 권장 설정은 관리 웹 애플리케이션 외부의 JEE의 AEM Forms 서버에 적용됩니다. 서버에 대한 보안 위험을 줄이려면 JEE에 AEM Forms을 설치한 후 즉시 이러한 설정을 적용하십시오.

**보안 패치**

공급업체 보안 패치 및 업그레이드가 적시에 적용되지 않을 경우 권한이 없는 사용자가 애플리케이션 서버에 액세스할 수 있는 위험이 증가합니다. 보안 패치를 프로덕션 서버에 적용하기 전에 테스트하여 애플리케이션의 호환성과 가용성을 보장합니다. 또한 규칙적으로 패치를 확인하고 설치하는 정책 및 절차를 만듭니다. AEM Forms on JEE 업데이트는 엔터프라이즈 제품 다운로드 사이트에 있습니다.

**서비스 계정(Windows의 경우 JBoss 턴키)**

AEM Forms on JEE는 기본적으로 LocalSystem 계정을 사용하여 서비스를 설치합니다. 기본 제공 LocalSystem 사용자 계정은 Administrators 그룹의 일부로 높은 수준의 접근성을 가집니다. 작업자 프로세스 ID가 LocalSystem 사용자 계정으로 실행되는 경우 해당 작업자 프로세스는 전체 시스템에 대한 전체 액세스 권한을 갖습니다.

특정 비관리 계정을 사용하여 JEE의 AEM Forms이 배포된 응용 프로그램 서버를 실행하려면 다음 지침을 따르십시오.

1. MMC(Microsoft Management Console)에서 다음과 같이 로그인할 Forms Server 서비스에 대한 로컬 사용자를 작성합니다.

   * 선택 **사용자가 암호를 변경할 수 없음**.
   * 다음에서 **구성원** 탭에서 다음을 확인합니다. **사용자** 그룹이 나열됩니다.

   >[!NOTE]
   >
   >PDF Generator에 대해 이 설정을 변경할 수 없습니다.

1. 선택 **시작** > **설정** > **관리 도구** > **서비스**.
1. JEE의 AEM Forms용 JBoss를 두 번 클릭하고 서비스를 중지합니다.
1. 다음에서 **로그온** 탭, 선택 **이 계정**&#x200B;를 클릭하고 생성한 사용자 계정을 찾은 다음 계정 암호를 입력합니다.
1. MMC에서 를 엽니다. **로컬 보안 설정** 및 선택 **로컬 정책** > **사용자 권한 할당**.
1. Forms 서버가 실행 중인 사용자 계정에 다음 권한을 할당합니다.

   * 터미널 서비스를 통한 로그온 거부
   * 로컬에서 로그온 거부
   * 서비스로 로그온(이미 설정되어야 함)

1. 새 사용자 계정에 다음 디렉터리에 대한 수정 권한을 부여합니다.
   * **GDS(전역 문서 저장소) 디렉터리**: AEM Forms 설치 프로세스 중에 GDS 디렉토리 위치가 수동으로 구성됩니다. 설치하는 동안 위치 설정이 비어 있으면 기본적으로 다음 위치에 애플리케이션 서버가 설치되는 디렉토리가 사용됩니다. `[JBoss root]/server/[type]/svcnative/DocumentStorage`
   * **CRX-Repository 디렉토리**: 기본 위치는 입니다. `[AEM-Forms-installation-location]\crx-repository`
   * **AEM Forms 임시 디렉터리**:
      * (Windows) 환경 변수에 설정된 TMP 또는 TEMP 경로
      * (AIX, Linux 또는 Solaris) 로그인한 사용자의 홈 디렉토리 UNIX 기반 시스템에서 루트가 아닌 사용자는 다음 디렉토리를 임시 디렉토리로 사용할 수 있습니다.
      * (Linux) /var/tmp 또는 /usr/tmp
      * (AIX) /tmp 또는 /usr/tmp
      * (Solaris) /var/tmp 또는 /usr/tmp
1. 새 사용자 계정에 다음 디렉터리에 대한 쓰기 권한을 부여합니다.
   * [JBoss-directory]\standalone\deployment
   * [JBoss-directory]\standalone\
   * [JBoss-directory]\bin\

   >[!NOTE]
   >
   >JBoss Application Server의 기본 설치 위치:
   >
   >* Windows: C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   >* Linux: /opt/jboss/

1. 응용 프로그램 서버를 시작합니다.

**Configuration Manager 부트스트랩 서블릿 비활성화**

Configuration Manager는 애플리케이션 서버에 배포된 서블릿을 사용하여 JEE 데이터베이스의 AEM Forms 부트스트래핑을 수행합니다. Configuration Manager는 구성이 완료되기 전에 이 서블릿에 액세스하므로 권한이 부여된 사용자에 대해 액세스 권한이 보호되지 않았으며, Configuration Manager를 사용하여 JEE에서 AEM Forms을 구성한 후에는 비활성화해야 합니다.

1. adobe-livecycle 압축 풀기-[appserver].ear 파일입니다.
1. META-INF/application.xml 파일을 엽니다.
1. adobe-bootstrapper.war 섹션을 검색합니다.

   ```java
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
1. adobe-bootstrapper.war 및 adobe-lcm-bootstrapper-redirectory에 대한 설명을 추가합니다. 다음과 같은 war 모듈:

   ```java
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
1. EAR 파일을 압축하고 애플리케이션 서버에 다시 배포합니다.
1. AEM Forms 서버를 시작합니다.
1. 변경 사항을 테스트하고 더 이상 작동하지 않는지 확인하려면 브라우저에 아래 URL을 입력합니다.

   https://&lt;localhost>:&lt;port>/adobe-bootstrapper/bootstrap

**Trust Store에 대한 원격 액세스 차단**

Configuration Manager를 사용하면 Acrobat Reader DC 확장 자격 증명을 JEE 신뢰 저장소의 AEM Forms에 업로드할 수 있습니다. 즉, 원격 프로토콜(SOAP 및 EJB)을 통한 Trust Store 자격 증명 서비스에 대한 액세스가 기본적으로 사용하도록 설정되었습니다. Configuration Manager를 사용하여 권한 자격 증명을 업로드한 후 또는 나중에 관리 콘솔을 사용하여 자격 증명을 관리하기로 한 경우에는 이 액세스가 더 이상 필요하지 않습니다.

섹션의 단계에 따라 모든 Trust Store 서비스에 대한 원격 액세스를 비활성화할 수 있습니다 [서비스에 대한 필수적이지 않은 원격 액세스 비활성화](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_remote_access_to_services).

**필수적이지 않은 모든 익명 액세스 비활성화**

일부 Forms 서버 서비스에는 익명 호출자가 호출할 수 있는 작업이 있습니다. 이러한 서비스에 대한 익명 액세스가 필요하지 않은 경우 의 단계에 따라 비활성화하십시오. [서비스에 대한 필수적이지 않은 익명 액세스 비활성화](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_anonymous_access_to_services).

#### 기본 관리자 암호 변경 {#change-the-default-administrator-password}

JEE의 AEM Forms이 설치되면 기본 암호가 인 수퍼 관리자/ 로그인 ID 관리자에 대해 단일 기본 사용자 계정이 구성됩니다. *암호*. 구성 관리자를 사용하여 즉시 이 암호를 변경해야 합니다.

1. 웹 브라우저에 다음 URL을 입력합니다.

   ```java
   https://[host name]:[port]/adminui
   ```

   기본 포트 번호는 다음 중 하나입니다.

   **JBos:** 8080

   **WebLogic 서버:** 7001

   **WebSphere:** 9080.

1. 다음에서 **사용자 이름** 필드, 유형 `administrator` 및, **암호** 필드, 유형 `password`.
1. 클릭 **설정** > **사용자 관리** > **사용자 및 그룹**.
1. 유형 `administrator` 다음에서 **찾기** 필드 및 클릭 **찾기**.
1. 클릭 **수퍼 관리자** 을 클릭합니다.
1. 클릭 **암호 변경** (사용자 편집 페이지)
1. 새 암호를 지정하고 **저장**.

또한 다음 단계를 수행하여 CRX 관리자의 기본 암호를 변경하는 것이 좋습니다.

1. 에 로그인 `https://[server]:[port]/lc/libs/granite/security/content/useradmin.html` 기본 사용자 이름/암호 사용.
1. 검색 필드에 Administrator를 입력하고 **이동**.
1. 선택 **관리자** 검색 결과에서 **편집** 사용자 인터페이스의 오른쪽 하단에 있는 아이콘입니다.
1. 에서 새 암호 지정 **새 암호** 필드 및 의 이전 암호 **내 암호** 필드.
1. 사용자 인터페이스의 오른쪽 하단에 있는 저장 아이콘을 클릭합니다.

#### WSDL 생성 비활성화 {#disable-wsdl-generation}

WSDL(웹 서비스 정의 언어) 생성은 개발자가 클라이언트 응용 프로그램을 빌드하는 데 사용하는 개발 환경에 대해서만 활성화해야 합니다. 서비스의 내부 세부 정보가 노출되지 않도록 프로덕션 환경에서 WSDL 생성을 비활성화하도록 선택할 수 있습니다.

1. 웹 브라우저에 다음 URL을 입력합니다.

   ```java
   https://[host name]:[port]/adminui
   ```

1. 선택 **설정 > 핵심 시스템 설정 > 구성**.
1. 선택 취소 **WSDL 활성화**&#x200B;을 선택한 다음 을 선택합니다. **확인**.

### 애플리케이션 서버 보안 {#application-server-security}

다음 표에서는 JEE용 AEM Forms 애플리케이션이 설치된 후 애플리케이션 서버를 보호하는 몇 가지 기술에 대해 설명합니다.

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
   <td><p>애플리케이션 서버의 JEE에 AEM Forms을 설치, 구성 및 배포한 후에는 애플리케이션 서버 관리 콘솔에 대한 액세스를 비활성화해야 합니다. 자세한 내용은 애플리케이션 서버 설명서를 참조하십시오.</p> </td> 
  </tr> 
  <tr> 
   <td><p>애플리케이션 서버 쿠키 설정</p> </td> 
   <td><p>애플리케이션 쿠키는 애플리케이션 서버에 의해 제어됩니다. 응용 프로그램을 배포할 때 응용 프로그램 서버 관리자는 서버 전체 또는 응용 프로그램별로 쿠키 기본 설정을 지정할 수 있습니다. 기본적으로 서버 설정이 기본 설정됩니다.</p> <p>애플리케이션 서버에서 생성한 모든 세션 쿠키에는 <code>HttpOnly</code> 특성. 예를 들어 JBoss 애플리케이션 서버를 사용하는 경우 SessionCookie 요소를 로 수정할 수 있습니다. <code>httpOnly="true"</code> 다음에서 <code>WEB-INF/web.xml</code> 파일.</p> <p>HTTPS만 사용하여 전송되는 쿠키를 제한할 수 있습니다. 따라서 HTTP를 통해 암호화되지 않은 상태로 전송되지 않습니다. 애플리케이션 서버 관리자는 전 세계적으로 서버에 대해 보안 쿠키를 활성화해야 합니다. 예를 들어 JBoss Application Server를 사용하는 경우 커넥터 요소를 로 수정할 수 있습니다 <code>secure=true</code> 다음에서 <code>server.xml</code> 파일.</p> <p>쿠키 설정에 대한 자세한 내용은 애플리케이션 서버 설명서를 참조하십시오.</p> </td> 
  </tr> 
  <tr> 
   <td><p>디렉터리 검색</p> </td> 
   <td><p>존재하지 않는 페이지를 요청하거나 디렉터 이름을 요청할 때(요청 문자열은 슬래시(/)로 끝남) 애플리케이션 서버는 해당 디렉터리의 내용을 반환해서는 안 됩니다. 이를 방지하기 위해 응용 프로그램 서버에서 디렉터리 검색을 비활성화할 수 있습니다. 이 작업은 관리 콘솔 응용 프로그램 및 서버에서 실행 중인 다른 응용 프로그램에 대해 수행해야 합니다.</p> <p>JBoss의 경우 목록 초기화 매개변수의 값을 설정합니다. <code>DefaultServlet</code> 다음으로 속성: <code>false</code> 다음 예제와 같이 web.xml 파일에서</p> <p>&lt;servlet&gt;</p> <p>&lt;servlet-name&gt;기본값&lt;/servlet-name&gt;</p> <p>&lt;servlet-class&gt;</p> <p>org.apache.catalina.servlets.DefaultServlet</p> <p>&lt;/servlet-class&gt;</p> <p>&lt;init-param&gt;</p> <p>&lt;param-name&gt;목록&lt;/param-name&gt;</p> <p>&lt;param-value&gt;false&lt;/param-value&gt;</p> <p>&lt;/init-param&gt;</p> <p>&lt;load-on-startup&gt;1&lt;/load-on-startup&gt;</p> <p>&lt;/servlet&gt;</p> <p>WebSphere의 경우 <code>directoryBrowsingEnabled</code> ibm-web-ext.xmi 파일의 속성 <code>false</code>.</p> <p>WebLogic의 경우 weblogic.xml 파일의 index-directories 속성을 다음으로 설정합니다. <code>false</code>을 참조하십시오.</p> <p>&lt;container-descriptor&gt;</p> <p>&lt;index-directory-enabled&gt;false</p> <p>&lt;/index-directory-enabled&gt;</p> <p>&lt;/container-descriptor&gt;</p> </td> 
  </tr> 
 </tbody> 
</table>

### 데이터베이스 보안 {#database-security}

데이터베이스 보안을 설정할 때는 데이터베이스 공급업체에서 설명한 측정값을 구현해야 합니다. JEE의 AEM Forms에서 사용할 수 있도록 부여된 최소 필수 데이터베이스 권한으로 데이터베이스 사용자를 할당해야 합니다. 예를 들어 데이터베이스 관리자 권한이 있는 계정은 사용하지 마십시오.

oracle 시 사용하는 데이터베이스 계정에는 CONNECT, RESOURCE 및 CREATE VIEW 권한만 있으면 됩니다. 다른 데이터베이스에 대한 유사한 요구 사항은 다음을 참조하십시오. [JEE(단일 서버)에 AEM Forms 설치 준비](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64).

#### JBoss용 Windows에서 SQL Server에 대한 통합 보안 구성 {#configuring-integrated-security-for-sql-server-on-windows-for-jboss}

1. 수정 [JBOSS_HOME]추가할 \\standalone\configuration\lc_{datasource.xml} `integratedSecurity=true` 다음 예제와 같이 연결 URL에 연결합니다.

   ```java
    jdbc:sqlserver://<serverhost>:<port>;databaseName=<dbname>;integratedSecurity=true
   ```

1. 응용 프로그램 서버를 실행 중인 컴퓨터의 Windows 시스템 경로에 sqljdbc_auth.dll 파일을 추가합니다. sqljdbc_auth.dll 파일은 Microsoft SQL JDBC 6.2.1.0 드라이버 설치와 함께 있습니다.
1. 로컬 시스템에서 다음으로 로그인에 대한 JBoss Windows 서비스(JEE의 AEM Forms용 JBoss) 속성을 AEM Forms 데이터베이스와 최소 권한 세트가 있는 로그인 계정으로 수정합니다. 명령줄에서 Windows 서비스 대신 JBoss를 실행하는 경우에는 이 단계를 수행할 필요가 없습니다.
1. 다음에서 SQL Server 보안 설정 **혼합** 모드: **Windows 인증만**.

#### WebLogic용 Windows에서 SQL Server에 대한 통합 보안 구성 {#configuring-integrated-security-for-sql-server-on-windows-for-weblogic}

1. 웹 브라우저의 URL 행에 다음 URL을 입력하여 WebLogic Server 관리 콘솔을 시작합니다.

   ```java
   https://[host name]:7001/console
   ```

1. 변경 센터에서 **잠금 및 편집**.
1. 도메인 구조에서 *[base_domain]* > **서비스** > **JDBC** > **데이터 소스** 오른쪽 창에서 **IDP_DS**.
1. 다음 화면의 **구성** 탭을 클릭하고 **연결 풀** 탭 및, **속성** 상자, 유형 `integratedSecurity=true`.
1. 도메인 구조에서 **[base_domain]** > **서비스** > **JDBC** > **데이터 소스** 오른쪽 창에서 **RM_DS**.
1. 다음 화면의 **구성** 탭을 클릭하고 **연결 풀** 탭 및, **속성** 상자, 유형 `integratedSecurity=true`.
1. 응용 프로그램 서버를 실행 중인 컴퓨터의 Windows 시스템 경로에 sqljdbc_auth.dll 파일을 추가합니다. sqljdbc_auth.dll 파일은 Microsoft SQL JDBC 6.2.1.0 드라이버 설치와 함께 있습니다.
1. 다음에서 SQL Server 보안 설정 **혼합** 모드: **Windows 인증만**.

#### WebSphere용 Windows에서 SQL Server에 대한 통합 보안 구성 {#configuring-integrated-security-for-sql-server-on-windows-for-websphere}

WebSphere에서는 WebSphere에 포함된 SQL Server JDBC 드라이버가 아닌 외부 SQL Server JDBC 드라이버를 사용하는 경우에만 통합 보안을 구성할 수 있습니다.

1. WebSphere 관리 콘솔에 로그인합니다.
1. 탐색 트리에서 **리소스** > **JDBC** > **데이터 소스** 오른쪽 창에서 **IDP_DS**.
1. 오른쪽 창의 추가 속성에서 **사용자 지정 속성**&#x200B;을 클릭한 다음 을 클릭합니다 **신규**.
1. 다음에서 **이름** 상자, 유형 `integratedSecurity` 및, **값** 상자, 유형 `true`.
1. 탐색 트리에서 **리소스** > **JDBC** > **데이터 소스** 오른쪽 창에서 **RM_DS**.
1. 오른쪽 창의 추가 속성에서 **사용자 지정 속성**&#x200B;을 클릭한 다음 을 클릭합니다 **신규**.
1. 다음에서 **이름** 상자, 유형 `integratedSecurity` 및, **값** 상자, 유형 `true`.
1. WebSphere가 설치된 컴퓨터에서 sqljdbc_auth.dll 파일을 Windows 시스템 경로(C:\Windows)에 추가합니다. sqljdbc_auth.dll 파일이 Microsoft SQL JDBC 1.2 드라이버 설치와 동일한 위치에 있습니다(기본값: *[InstallDir]*/sqljdbc_1.2/enu/auth/x86).
1. 선택 **시작** > **Campaign 컨트롤 패널** > **서비스** WebSphere(IBM WebSphere Application Server)용 Windows 서비스를 마우스 오른쪽 단추로 클릭 &lt;version> - &lt;node>) 및 선택 **속성**.
1. Properties 대화 상자에서 **로그온** 탭.
1. 선택 **이 계정** 사용할 로그인 계정을 설정하는 데 필요한 정보를 제공합니다.
1. 다음에서 SQL Server 보안 설정 **혼합** 모드: **Windows 인증만**.

### 데이터베이스의 중요한 콘텐츠에 대한 액세스 보호 {#protecting-access-to-sensitive-content-in-the-database}

AEM Forms 데이터베이스 스키마에는 시스템 구성 및 비즈니스 프로세스에 대한 중요한 정보가 포함되어 있으므로 방화벽 뒤에 숨겨야 합니다. 데이터베이스는 Forms 서버와 동일한 신뢰 범위 내에서 고려되어야 합니다. 정보 공개 및 비즈니스 데이터 도난을 방지하려면 승인된 관리자만 액세스할 수 있도록 DBA(데이터베이스 관리자)가 데이터베이스를 구성해야 합니다.

또한 데이터베이스 공급업체별 도구를 사용하여 다음 데이터가 포함된 테이블의 열을 암호화하는 것도 고려해야 합니다.

* Rights Management 문서 키
* Trust Store HSM PIN 암호화 키
* 로컬 사용자 암호 해시

공급업체별 도구에 대한 자세한 내용은 [&quot;데이터베이스 보안 정보&quot;](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#database_security_information).

### LDAP 보안 {#ldap-security}

LDAP(Lightweight Directory Access Protocol) 디렉토리는 일반적으로 AEM Forms on JEE에서 엔터프라이즈 사용자 및 그룹 정보의 소스이자 비밀번호 인증을 수행하는 수단으로 사용됩니다. LDAP 디렉토리가 SSL(Secure Socket Layer)을 사용하도록 구성되어 있고 JEE의 AEM Forms이 SSL 포트를 사용하여 LDAP 디렉토리에 액세스하도록 구성되어 있는지 확인해야 합니다.

#### LDAP 서비스 거부 {#ldap-denial-of-service}

LDAP를 사용하는 일반적인 공격에는 공격자가 의도적으로 여러 번 인증하지 못하는 경우가 포함됩니다. 이렇게 하면 LDAP 디렉토리 서버가 모든 LDAP 종속 서비스에서 사용자를 잠급니다.

사용자가 AEM Forms 인증에 반복적으로 실패할 때 AEM Forms이 구현하는 실패 시도 횟수와 후속 잠금 시간을 설정할 수 있습니다. 관리 콘솔에서 낮은 값을 선택합니다. 실패 시도 횟수를 선택할 때는 모든 시도가 수행된 후 LDAP 디렉터리 서버가 시도하기 전에 AEM Forms이 사용자를 잠그는 것을 이해하는 것이 중요합니다.

#### 자동 계정 잠금 설정 {#set-automatic-account-locking}

1. 관리 콘솔에 로그인합니다.
1. 클릭 **설정** > **사용자 관리** > **도메인 관리**.
1. 자동 계정 잠금 설정에서 을 설정합니다. **최대 연속 인증 실패** 낮은 숫자로 변환(예: 3).
1. **저장**&#x200B;을 클릭합니다.

### 감사 및 로깅 {#auditing-and-logging}

응용 프로그램 감사 및 로깅을 적절하고 안전하게 사용하면 보안 및 기타 비정상적인 이벤트가 가능한 한 빨리 추적 및 검색되도록 할 수 있습니다. 응용 프로그램 내에서 감사 및 로깅을 효과적으로 사용하는 방법에는 성공 및 실패한 로그인 추적과 같은 항목 및 키 레코드 생성이나 삭제와 같은 주요 응용 프로그램 이벤트가 포함됩니다.

감사를 사용하여 다음을 포함한 다양한 유형의 공격을 감지할 수 있습니다.

* 암호 공격 차단
* 서비스 거부 공격
* 적대적 입력 및 관련 클래스의 스크립팅 공격 삽입

이 표에서는 서버의 취약성을 줄이는 데 사용할 수 있는 감사 및 로깅 기술에 대해 설명합니다.

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
   <td><p>JEE 로그 파일 액세스 제어 목록(ACL)에서 적절한 AEM Forms을 설정합니다.</p> <p>적절한 자격 증명을 설정하면 공격자가 파일을 삭제하지 못하도록 합니다.</p> <p>로그 파일 디렉터리에 대한 보안 권한은 관리자 및 SYSTEM 그룹에 대한 모든 권한이어야 합니다. AEM Forms 사용자 계정에는 읽기 및 쓰기 권한만 있어야 합니다.</p> </td> 
  </tr> 
  <tr> 
   <td><p>로그 파일 중복</p> </td> 
   <td><p>리소스가 허용하는 경우 Syslog, Tivoli, Microsoft Operations Manager(MOM) 서버 또는 다른 메커니즘을 사용하여 공격자가 액세스할 수 없는(쓰기 전용) 실시간으로 다른 서버로 로그를 보냅니다.</p> <p>이러한 방식으로 로그를 보호하면 변조를 방지할 수 있습니다. 또한 중앙 저장소에 로그를 저장하면 상관 관계 및 모니터링에 도움이 됩니다(예: 여러 Forms 서버가 사용 중이고 각 컴퓨터에 암호를 쿼리하는 여러 컴퓨터에서 암호 추측 공격이 발생하는 경우).</p> </td> 
  </tr> 
 </tbody> 
</table>

### 관리자가 아닌 사용자가 PDF Generator을 실행할 수 있도록 설정

관리자가 아닌 사용자가 PDF Generator을 사용할 수 있도록 설정할 수 있습니다. 일반적으로 관리 권한이 있는 사용자만 PDF Generator을 사용할 수 있습니다. 관리자가 아닌 사용자가 PDF Generator을 실행할 수 있도록 하려면 다음 단계를 수행하십시오.

1. 환경 변수 이름 PDFG_NON_ADMIN_ENABLED를 생성합니다.

1. 변수의 값을 TRUE로 설정합니다.

1. AEM Forms 인스턴스를 다시 시작합니다.

>[!NOTE]
>
> SDK를 다시 시작하려면 &#39;Ctrl + C&#39; 명령을 사용하는 것이 좋습니다. Java 프로세스 중지와 같은 대체 방법을 사용하여 AEM SDK를 다시 시작하면 AEM 개발 환경이 일치하지 않을 수 있습니다.

## 기업 외부 액세스를 위해 JEE에서 AEM Forms 구성 {#configuring-aem-forms-on-jee-for-access-beyond-the-enterprise}

JEE에 AEM Forms을 성공적으로 설치한 후에는 환경 보안을 정기적으로 유지하는 것이 중요합니다. 이 섹션에서는 JEE 프로덕션 서버에서 AEM Forms의 보안을 유지 관리하는 데 권장되는 작업에 대해 설명합니다.

### 웹 액세스에 대한 역방향 프록시 설정 {#setting-up-a-reverse-proxy-for-web-access}

A *역방향 프록시* 는 JEE 웹 애플리케이션에서 AEM Forms용 URL 세트 하나를 외부 및 내부 사용자 모두가 사용할 수 있도록 하는 데 사용할 수 있습니다. 이 구성은 사용자가 JEE의 AEM Forms이 실행 중인 애플리케이션 서버에 직접 연결할 수 있는 것보다 더 안전합니다. 역방향 프록시는 JEE에서 AEM Forms을 실행 중인 애플리케이션 서버에 대해 모든 HTTP 요청을 수행합니다. 사용자는 역방향 프록시에 대한 네트워크 액세스 권한만 가지며 역방향 프록시가 지원하는 URL 연결만 시도할 수 있습니다.

**역방향 프록시 서버에 사용할 AEM Forms on JEE 루트 URL**

JEE 웹 애플리케이션의 각 AEM Forms에 대한 다음 애플리케이션 루트 URL. 최종 사용자에게 제공하려는 웹 애플리케이션 기능에 대한 URL을 노출하기 위해서만 역방향 프록시를 구성해야 합니다.

특정 URL은 최종 사용자 대면 웹 애플리케이션으로 강조 표시됩니다. 역방향 프록시를 통해 외부 사용자에 액세스하기 위해 Configuration Manager에 대한 다른 URL은 노출하지 않아야 합니다.

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
   <td><p>PDF 문서에 사용 권한을 적용하기 위한 Acrobat Reader DC 확장 최종 사용자 웹 애플리케이션</p> </td> 
   <td><p>예</p> </td> 
   <td><p>예</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edc/*</p> </td> 
   <td><p>최종 사용자 웹 애플리케이션 Rights Management</p> </td> 
   <td><p>예</p> </td> 
   <td><p>예</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edcws/*</p> </td> 
   <td><p>Rights Management을 위한 웹 서비스 URL</p> </td> 
   <td><p>아니요</p> </td> 
   <td><p>예</p> </td> 
  </tr> 
  <tr> 
   <td><p>/pdfgui/*</p> </td> 
   <td><p>PDF Generator 관리 웹 애플리케이션</p> </td> 
   <td><p>예</p> </td> 
   <td><p>예</p> </td> 
  </tr> 
  <tr> 
   <td><p>/workspace/*</p> </td> 
   <td><p>작업 영역 최종 사용자 웹 애플리케이션</p> </td> 
   <td><p>예</p> </td> 
   <td><p>예</p> </td> 
  </tr> 
  <tr> 
   <td><p>/workspace-server/*</p> </td> 
   <td><p>Workspace 클라이언트 응용 프로그램에 필요한 Workspace 서블릿 및 데이터 서비스</p> </td> 
   <td><p>예</p> </td> 
   <td><p>예</p> </td> 
  </tr> 
  <tr> 
   <td><p>/adobe-bootstrapper/*</p> </td> 
   <td><p>JEE 저장소의 AEM Forms 부트스트래핑용 서블릿</p> </td> 
   <td><p>아니요</p> </td> 
   <td><p>아니요</p> </td> 
  </tr> 
  <tr> 
   <td><p>/soap/*</p> </td> 
   <td><p>Forms Server 웹 서비스에 대한 정보 페이지</p> </td> 
   <td><p>아니요</p> </td> 
   <td><p>아니요</p> </td> 
  </tr> 
  <tr> 
   <td><p>/soap/services/*</p> </td> 
   <td><p>모든 Forms 서버 서비스의 웹 서비스 URL</p> </td> 
   <td><p>아니요</p> </td> 
   <td><p>아니요</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edc/admin/*</p> </td> 
   <td><p>Rights Management 관리 웹 애플리케이션</p> </td> 
   <td><p>예</p> </td> 
   <td><p>아니요</p> </td> 
  </tr> 
  <tr> 
   <td><p>/adminui/*</p> </td> 
   <td><p>관리 콘솔 홈 페이지</p> </td> 
   <td><p>예</p> </td> 
   <td><p>아니요</p> </td> 
  </tr> 
  <tr> 
   <td><p>/TruststoreComponent/</p> <p>보안/*</p> </td> 
   <td><p>Trust Store 관리 페이지</p> </td> 
   <td><p>예</p> </td> 
   <td><p>아니요</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormsIVS/*</p> </td> 
   <td><p>양식 렌더링 테스트 및 디버깅을 위한 Forms IVS 애플리케이션</p> </td> 
   <td><p>예</p> </td> 
   <td><p>아니요</p> </td> 
  </tr> 
  <tr> 
   <td><p>/OutputIVS/*</p> </td> 
   <td><p>출력 서비스 테스트 및 디버깅을 위한 출력 IVS 응용 프로그램</p> </td> 
   <td><p>예</p> </td> 
   <td><p>아니요</p> </td> 
  </tr> 
  <tr> 
   <td><p>/rmws/*</p> </td> 
   <td><p>Rights Management의 REST URL</p> </td> 
   <td><p>아니요</p> </td> 
   <td><p>예</p> </td> 
  </tr> 
  <tr> 
   <td><p>/OutputAdmin/*</p> </td> 
   <td><p>출력 관리 페이지</p> </td> 
   <td><p>예</p> </td> 
   <td><p>아니요</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServer/*</p> </td> 
   <td><p>Forms 웹 애플리케이션 파일</p> </td> 
   <td><p>예</p> </td> 
   <td><p>아니요</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServer/GetImage</p> <p>서블릿</p> </td> 
   <td><p>HTML 변환 중 JavaScript를 가져오는 데 사용됨</p> </td> 
   <td><p>아니요</p> </td> 
   <td><p>아니요</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServerAdmin/*</p> </td> 
   <td><p>Forms 관리 페이지</p> </td> 
   <td><p>예</p> </td> 
   <td><p>아니요</p> </td> 
  </tr> 
  <tr> 
   <td><p>/repository/*</p> </td> 
   <td><p>WebDAV(디버깅) 액세스용 URL</p> </td> 
   <td><p>예</p> </td> 
   <td><p>아니요</p> </td> 
  </tr> 
  <tr> 
   <td><p>/AACComponent/*</p> </td> 
   <td><p>애플리케이션 및 서비스 사용자 인터페이스</p> </td> 
   <td><p>예</p> </td> 
   <td><p>아니요</p> </td> 
  </tr> 
  <tr> 
   <td><p>/WorkspaceAdmin/*</p> </td> 
   <td><p>작업 영역 관리 페이지</p> </td> 
   <td><p>예</p> </td> 
   <td><p>아니요</p> </td> 
  </tr> 
  <tr> 
   <td><p>/rest/*</p> </td> 
   <td><p>나머지 지원 페이지</p> </td> 
   <td><p>예</p> </td> 
   <td><p>아니요</p> </td> 
  </tr> 
  <tr> 
   <td><p>/CoreSystemConfig/*</p> </td> 
   <td><p>JEE의 AEM Forms 코어 구성 설정 페이지</p> </td> 
   <td><p>예</p> </td> 
   <td><p>아니요</p> </td> 
  </tr> 
  <tr> 
   <td><p>/um/</p> </td> 
   <td><p>사용자 관리 인증</p> </td> 
   <td><p>아니요</p> </td> 
   <td><p>예</p> </td> 
  </tr> 
  <tr> 
   <td><p>/um/*</p> </td> 
   <td><p>사용자 관리 관리 인터페이스</p> </td> 
   <td><p>예</p> </td> 
   <td><p>아니요</p> </td> 
  </tr> 
  <tr> 
   <td><p>/DocumentManager/*</p> </td> 
   <td><p>HTTP 문서가 활성화된 SOAP 전송 또는 EJB 전송을 통해 원격 끝점, SOAP WSDL 끝점 및 Java SDK에 액세스할 때 처리할 문서 업로드 및 다운로드.</p> </td> 
   <td><p>예</p> </td> 
   <td><p>예</p> </td> 
  </tr> 
 </tbody> 
</table>

## 크로스 사이트 요청 위조 공격으로부터 보호 {#protecting-from-cross-site-request-forgery-attacks}

CSRF(Cross-Site Request Forgery) 공격은 웹 사이트가 사용자에게 갖는 신뢰를 이용하여 사용자가 승인하지 않고 의도하지 않은 명령을 전송합니다. 공격은 사용자가 이미 인증된 다른 사이트에 액세스하기 위해 웹 페이지에 링크 또는 스크립트를 포함하거나 이메일 메시지에 URL을 포함하여 설정됩니다.

예를 들어 다른 웹 사이트를 동시에 탐색하면서 Administration Console에 로그인할 수 있습니다. 웹 페이지 중 하나는 다음과 같은 HTML 이미지 태그를 포함할 수 있습니다. `src` 희생된 웹 사이트의 서버측 스크립트를 대상으로 하는 속성입니다. 웹 브라우저에서 제공하는 쿠키 기반 세션 인증 메커니즘을 사용하여 공격 웹 사이트는 정당한 사용자로 가장하여 이 피해자 서버측 스크립트에 악의적인 요청을 보낼 수 있습니다. 자세한 예는 를 참조하십시오. [https://owasp.org/www-community/attacks/csrf#Examples](https://owasp.org/www-community/attacks/csrf#Examples).

CSRF에는 다음과 같은 특성이 일반적입니다.

* 사용자의 ID를 사용하는 사이트를 포함합니다.
* 해당 ID에 대한 사이트의 신뢰를 활용합니다.
* 사용자의 브라우저를 속여 HTTP 요청을 대상 사이트로 보냅니다.
* 부작용이 있는 HTTP 요청을 포함합니다.

JEE의 AEM Forms은 레퍼러 필터 기능을 사용하여 CSRF 공격을 차단합니다. 이 섹션에서는 레퍼러 필터링 메커니즘을 설명하기 위해 다음 용어를 사용합니다.

* **허용된 레퍼러:** 레퍼러는 서버에 요청을 보내는 소스 페이지의 주소입니다. JSP 페이지 또는 양식의 경우 레퍼러는 일반적으로 검색 기록의 이전 페이지입니다. 이미지의 레퍼러는 일반적으로 이미지가 표시되는 페이지입니다. 서버 리소스를 허용된 레퍼러 목록에 추가하여 해당 리소스에 대한 액세스가 허용된 레퍼러를 식별할 수 있습니다.
* **허용된 레퍼러 예외:** 허용된 레퍼러 목록에서 특정 레퍼러에 대한 액세스 범위를 제한할 수 있습니다. 이 제한을 적용하려면 해당 레퍼러의 개별 경로를 허용된 레퍼러 예외 목록에 추가할 수 있습니다. 허용된 레퍼러 예외 목록의 경로에서 시작된 요청은 Forms 서버에서 리소스를 호출하지 못합니다. 특정 애플리케이션에 대해 허용된 레퍼러 예외를 정의하고 모든 애플리케이션에 적용되는 전체 예외 목록을 사용할 수도 있습니다.
* **허용된 URI:** 레퍼러 헤더를 확인하지 않고 제공할 리소스 목록입니다. 서버에서 상태를 변경하지 않는 리소스(예: 도움말 페이지)를 이 목록에 추가할 수 있습니다. 허용된 URI 목록의 리소스는 레퍼러가 누구인지에 관계없이 레퍼러 필터에 의해 차단되지 않습니다.
* **Null 레퍼러:** 상위 웹 페이지와 관련이 없거나 상위 웹 페이지에서 발생하지 않는 서버 요청은 Null 레퍼러의 요청으로 간주됩니다. 예를 들어 새 브라우저 창을 열고 주소를 입력한 다음 Enter 키를 누르면 서버로 전송된 레퍼러가 null입니다. 웹 서버에 HTTP 요청을 하는 데스크톱 응용 프로그램(.NET 또는 SWING)도 서버에 Null 레퍼러를 보냅니다.

### 레퍼러 필터링 {#referer-filtering}

레퍼러 필터링 프로세스는 다음과 같이 설명할 수 있습니다.

1. Forms 서버는 호출에 사용된 HTTP 메서드를 확인합니다.

   1. POST 상태인 경우 Forms 서버가 레퍼러 헤더 검사를 수행합니다.
   1. GET 상태인 경우 Forms 서버는 다음이 아닌 경우 레퍼러 검사를 우회합니다 *CSRF_CHECK_GETS* 가 true로 설정되어 있으면 레퍼러 헤더 검사를 수행합니다. *CSRF_CHECK_GETS* 는에 지정됩니다. *web.xml* 응용 프로그램용 파일입니다.

1. Forms 서버는 요청된 URI가 허용 목록에 추가하다에 있는지 확인합니다.

   1. URI가 허용 목록에추가된인 경우 서버가 요청을 수락합니다.
   1. 요청한 URI가 허용 목록에추가된이 아닌 경우 서버는 요청의 레퍼러를 검색합니다.

1. 요청에 레퍼러가 있는 경우 서버는 허용된 레퍼러인지 여부를 확인합니다. 허용되면 서버는 레퍼러 예외를 확인합니다.

   1. 예외인 경우 요청이 차단됩니다.
   1. 예외가 아닌 경우 요청이 전달됩니다.

1. 요청에 레퍼러가 없으면 서버는 Null 레퍼러가 허용되는지 여부를 확인합니다.

   1. Null 레퍼러가 허용되면 요청이 전달됩니다.
   1. Null 레퍼러가 허용되지 않는 경우 서버는 요청된 URI가 Null 레퍼러에 대한 예외인지 여부를 확인하고 그에 따라 요청을 처리합니다.

### 레퍼러 필터링 관리 {#managing-referer-filtering}

AEM Forms on JEE는 서버 리소스에 대한 액세스가 허용되는 레퍼러를 지정하는 레퍼러 필터를 제공합니다. 기본적으로 레퍼러 필터는 안전한 HTTP 메서드(예: GET)를 사용하는 요청을 필터링하지 않습니다. *CSRF_CHECK_GETS* 가 true로 설정되어 있는 경우 허용된 레퍼러 항목에 대한 포트 번호가 0으로 설정된 경우 JEE의 AEM Forms은 포트 번호에 관계없이 해당 호스트의 레퍼러가 있는 모든 요청을 허용합니다. 포트 번호를 지정하지 않으면 기본 포트 80(HTTP) 또는 포트 443(HTTPS)에서의 요청만 허용됩니다. 허용된 레퍼러 목록의 모든 항목이 삭제되면 레퍼러 필터링이 비활성화됩니다.

문서 서비스를 처음 설치하면 허용된 레퍼러 목록이 문서 서비스가 설치된 서버 주소로 업데이트됩니다. 서버의 항목에는 서버 이름, IPv4 주소, IPv6이 활성화된 경우 IPv6 주소, 루프백 주소 및 localhost 항목이 포함됩니다. 허용된 레퍼러 목록에 추가된 이름은 호스트 운영 체제에서 반환됩니다. 예를 들어 IP 주소가 10.40.54.187인 서버에는 다음 항목이 포함됩니다. `https://server-name:0, https://10.40.54.187:0, https://127.0.0.1:0, http://localhost:0`. 호스트 운영 체제에서 반환된 정규화되지 않은 이름(IPv4 주소, IPv6 주소 또는 정규화된 도메인 이름이 없는 이름)의 경우 허용 목록에 추가하다 주소가 업데이트되지 않습니다. 비즈니스 환경에 맞게 허용된 레퍼러 목록을 수정합니다. 기본 허용된 레퍼러 목록이 있는 프로덕션 환경에 Forms 서버를 배포하지 마십시오. 허용된 레퍼러, 레퍼러 예외 또는 URI를 수정한 후에는 서버를 다시 시작하여 변경 사항을 적용해야 합니다.

**허용된 레퍼러 목록 관리**

관리 콘솔의 사용자 관리 인터페이스에서 허용된 레퍼러 목록을 관리할 수 있습니다. 사용자 관리 인터페이스는 목록을 생성, 편집 또는 삭제하는 기능을 제공합니다. *를 참조하십시오. [CSRF 공격 방지](/help/forms/using/admin-help/preventing-csrf-attacks.md)* 섹션 *관리 도움말* 를 참조하십시오.

**허용된 레퍼러 예외 및 허용된 URI 목록 관리**

AEM Forms on JEE는 허용된 레퍼러 예외 목록과 허용된 URI 목록을 관리하기 위한 API를 제공합니다. 이러한 API를 사용하여 목록을 검색, 생성, 편집 또는 삭제할 수 있습니다. 다음은 사용 가능한 API 목록입니다.

* createAllowedURIsList
* getAllowedURIsList
* updateAllowedURIsList
* deleteAllowedURIsList
* addAllowedRefererExceptions
* getAllowedRefererException
* updateAllowedRefererExceptions
* deleteAllowedRefererException

AEM Forms API에 대한 자세한 내용은* JEE API 설명서* 를 참조하십시오.

사용 ***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION*** 글로벌 수준의 허용된 레퍼러 예외 목록(모든 애플리케이션에 적용 가능한 예외 정의) 이 목록에는 절대 경로가 있는 URI만 포함됩니다(예: `/index.html`) 또는 상대 경로(예: `/sample/`). 예를 들어 상대 URI의 끝에 정규 표현식을 추가할 수도 있습니다. `/sample/(.)*`.

다음 ***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION*** 목록 ID는 `UMConstants` 클래스 `com.adobe.idp.um.api` 네임스페이스, 다음 위치: `adobe-usermanager-client.jar`. AEM Forms API를 사용하여 이 목록을 만들거나 수정하거나 편집할 수 있습니다. 예를 들어 허용된 글로벌 레퍼러 예외 목록을 만들려면 다음을 사용합니다.

```java
addAllowedRefererExceptions(UMConstants.LC_GLOBAL_ALLOWED_REFERER_EXCEPTION, Arrays.asList("/index.html", "/sample/(.)*"))
```

사용 ***CSRF_ALLOWED_REFERER_EXCEPTION*** 응용 프로그램별 예외 목록을 표시합니다.

**레퍼러 필터 비활성화**

레퍼러 필터가 Forms 서버에 대한 액세스를 완전히 차단하며 허용된 레퍼러 목록을 편집할 수 없는 경우 서버 시작 스크립트를 업데이트하고 레퍼러 필터링을 비활성화할 수 있습니다.

포함 `-Dlc.um.csrffilter.disabled=true` 시작 스크립트에서 JAVA 인수를 사용하고 서버를 다시 시작합니다. 허용된 레퍼러 목록을 적절하게 재구성한 후 JAVA 인수를 삭제해야 합니다.

**사용자 지정 WAR 파일에 대한 레퍼러 필터링**

비즈니스 요구 사항을 충족하기 위해 JEE에서 AEM Forms과 작업하기 위해 사용자 정의 WAR 파일을 생성했을 수 있습니다. 사용자 지정 WAR 파일에 대한 레퍼러 필터링을 활성화하려면 다음을 포함합니다. ***adobe-usermanager-client.jar*** WAR의 클래스 경로에서 다음 매개 변수와 함께* web.xml* 파일의 필터 항목을 포함합니다.

**CSRF_CHECK_GETS** 는 GET 요청에 대한 레퍼러 검사를 제어합니다. 이 매개 변수가 정의되지 않으면 기본값이 false로 설정됩니다. GET 요청을 필터링하려는 경우에만 이 매개 변수를 포함하십시오.

**CSRF_ALLOWED_REFERER_EXCEPTION** 는 허용된 레퍼러 예외 목록의 ID입니다. 레퍼러 필터는 목록 ID로 식별되는 목록의 레퍼러에서 시작된 요청이 Forms 서버의 리소스를 호출하지 못하도록 합니다.

**CSRF_ALLOWED_URIS_LIST_NAME** 는 허용된 URI 목록의 ID입니다. 레퍼러 필터는 요청의 레퍼러 헤더 값에 관계없이 목록 ID로 식별되는 목록의 리소스에 대한 요청을 차단하지 않습니다.

**CSRF_ALLOW_NULL_REFERER** 레퍼러가 null이거나 존재하지 않을 때 레퍼러 필터 동작을 제어합니다. 이 매개 변수가 정의되지 않으면 기본값이 false로 설정됩니다. Null 레퍼러를 허용하려는 경우에만 이 매개 변수를 포함하십시오. Null 레퍼러를 허용하면 일부 유형의 사이트 간 요청 위조 공격을 허용할 수 있습니다.

**CSRF_NULL_REFERER_EXCEPTION** 는 레퍼러가 null일 때 레퍼러 검사가 수행되지 않는 URI 목록입니다. 이 매개 변수는 다음과 같은 경우에만 활성화됩니다. *CSRF_ALLOW_NULL_REFERER* false로 설정되어 있습니다. 목록에서 여러 URI는 쉼표로 구분하십시오.

다음은 의 필터 항목 예입니다. *web.xml* 파일용 ***샘플*** WAR 파일

```java
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

CSRF 필터에 의해 적합한 서버 요청이 차단되는 경우 다음 중 하나를 시도해 보십시오.

* 거부된 요청에 레퍼러 헤더가 있는 경우 허용된 레퍼러 목록에 추가하는 것이 좋습니다. 신뢰할 수 있는 레퍼러만 추가합니다.
* 거부된 요청에 레퍼러 헤더가 없는 경우 레퍼러 헤더를 포함하도록 클라이언트 애플리케이션을 수정합니다.
* 클라이언트에서 브라우저에서 작업할 수 있는 경우 해당 배포 모델을 시도하십시오.
* 마지막 수단으로 리소스를 허용 URI 목록에 추가할 수 있습니다. 이 설정은 권장되지 않습니다.

## 보안 네트워크 구성 {#secure-network-configuration}

이 섹션에서는 JEE의 AEM Forms에 필요한 프로토콜 및 포트에 대해 설명하고 보안 네트워크 구성에서 JEE의 AEM Forms을 배포하기 위한 권장 사항을 제공합니다.

### JEE의 AEM Forms에서 사용하는 네트워크 프로토콜 {#network-protocols-used-by-aem-forms-on-jee}

이전 섹션에서 설명한 대로 보안 네트워크 아키텍처를 구성할 때 JEE의 AEM Forms과 엔터프라이즈 네트워크의 다른 시스템 간의 상호 작용을 위해서는 다음 네트워크 프로토콜이 필요합니다.

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
     <li><p>브라우저에 Configuration Manager 및 최종 사용자 웹 애플리케이션 표시</p> </li> 
     <li><p>모든 SOAP 연결</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>SOAP</p> </td> 
   <td> 
    <ul> 
     <li><p>.NET 응용 프로그램과 같은 웹 서비스 클라이언트 응용 프로그램</p> </li> 
     <li><p>Adobe Reader®는 JEE 서버 웹 서비스에서 AEM Forms용 SOAP을 사용합니다</p> </li> 
     <li><p>Adobe Flash® 응용 프로그램은 SOAP for Forms Server 웹 서비스를 사용합니다</p> </li> 
     <li><p>SOAP 모드에서 사용 시 JEE의 AEM Forms SDK 호출</p> </li> 
     <li><p>Workbench 디자인 환경</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>RMI</p> </td> 
   <td><p>EJB(Enterprise JavaBeans) 모드에서 사용 시 JEE의 AEM Forms SDK 호출</p> </td> 
  </tr> 
  <tr> 
   <td><p>IMAP / POP3</p> </td> 
   <td> 
    <ul> 
     <li><p>서비스에 대한 이메일 기반 입력(이메일 엔드포인트)</p> </li> 
     <li><p>이메일을 통한 사용자 작업 알림</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>UNC 파일 IO</p> </td> 
   <td><p>AEM Forms on JEE가 서비스(감시 폴더 끝점) 입력을 위한 감시 폴더 모니터링</p> </td> 
  </tr> 
  <tr> 
   <td><p>LDAP</p> </td> 
   <td> 
    <ul> 
     <li><p>디렉토리에서 조직 사용자 및 그룹 정보 동기화</p> </li> 
     <li><p>대화형 사용자를 위한 LDAP 인증</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>JDBC</p> </td> 
   <td> 
    <ul> 
     <li><p>JDBC 서비스를 사용하여 프로세스를 실행하는 동안 외부 데이터베이스에 대해 수행된 쿼리 및 프로시저 호출</p> </li> 
     <li><p>JEE 저장소의 AEM Forms 내부 액세스</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>WebDAV</p> </td> 
   <td><p>모든 WebDAV 클라이언트에서 JEE의 디자인 타임 저장소(양식, 조각 등)에서 AEM Forms을 원격으로 검색할 수 있도록 합니다.</p> </td> 
  </tr> 
  <tr> 
   <td><p>AMF</p> </td> 
   <td><p>JEE 서버 서비스의 AEM Forms이 원격 끝점으로 구성된 Adobe Flash 응용 프로그램</p> </td> 
  </tr> 
  <tr> 
   <td><p>JMX</p> </td> 
   <td><p>JEE의 AEM Forms은 JMX를 사용하여 모니터링할 MBean을 노출합니다.</p> </td> 
  </tr> 
 </tbody> 
</table>

### 애플리케이션 서버용 포트 {#ports-for-application-servers}

이 섹션에서는 지원되는 각 애플리케이션 서버 유형에 대한 기본 포트 및 대체 구성 범위를 설명합니다. 이러한 포트는 JEE에서 AEM Forms을 실행하는 응용 프로그램 서버에 연결하는 클라이언트에 허용하려는 네트워크 기능에 따라 내부 방화벽에서 활성화하거나 비활성화해야 합니다.

>[!NOTE]
>
>기본적으로 서버는 adobe.com 네임스페이스 아래에 여러 JMX MBean을 노출합니다. 서버 상태 모니터링에 유용한 정보만 표시됩니다. 그러나 정보가 공개되지 않도록 하려면 신뢰할 수 없는 네트워크의 호출자가 JMX MBean을 조회하고 상태 지표에 액세스하지 못하도록 해야 합니다.

**JBoss 포트**

<table> 
 <thead> 
  <tr> 
   <th><p>용도</p> </th> 
   <th><p>포트</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>웹 애플리케이션에 액세스</p> </td> 
   <td><p>[JBOSS_Root]/standalone/configuration/lc_[database].xml</p> <p>HTTP/1.1 Connector 포트 8080</p> <p>AJP 1.3 Connector 포트 8009</p> <p>SSL/TLS 커넥터 포트 8443</p> </td> 
  </tr> 
  <tr> 
   <td><p>CORBA 지원</p> </td> 
   <td><p>[JBoss root]/server/all/conf/jacorb.properties</p> <p>오포트</p> <p>OASSLPort 3529</p> </td> 
  </tr> 
 </tbody> 
</table>

**WebLogic 포트**

<table> 
 <thead> 
  <tr> 
   <th><p>용도</p> </th> 
   <th><p>포트</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>웹 애플리케이션에 액세스</p> </td> 
   <td> 
    <ul> 
     <li><p>관리 서버 수신 포트: 기본값은 7001입니다.</p> </li> 
     <li><p>관리 서버 SSL 수신 포트: 기본값은 7002입니다.</p> </li> 
     <li><p>관리 서버에 대해 구성된 포트(예: 8001)</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>JEE의 AEM Forms에 액세스하는 데 WebLogic 관리 포트가 필요하지 않음</p> </td> 
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

JEE의 AEM Forms에 필요한 WebSphere 포트에 대한 자세한 내용을 보려면 WebSphere Application Server UI의 포트 번호 설정으로 이동하십시오.

### SSL 구성 {#configuring-ssl}

섹션에 설명된 물리적 아키텍처 참조 [AEM Forms on JEE 물리적 아키텍처](hardening-aem-forms-jee-environment.md#aem-forms-on-jee-physical-architecture), 사용하려는 모든 연결에 대해 SSL을 구성해야 합니다. 특히, 네트워크에서 사용자 자격 증명이 노출되지 않도록 모든 SOAP 연결을 SSL을 통해 수행해야 합니다.

JBoss, WebLogic 및 WebSphere에서 SSL을 구성하는 방법에 대한 지침은 의 &quot;SSL 구성&quot;을 참조하십시오. [관리 도움말](https://www.adobe.com/go/learn_aemforms_admin_64).

AEM Forms 서버에 대해 구성된 JVM(Java Virtual Machine)으로 인증서를 가져오는 방법에 대한 지침은 의 상호 인증 섹션을 참조하십시오. [AEM Forms Workbench 도움말](https://www.adobe.com/go/learn_aemforms_workbench_65).

### SSL 리디렉션 구성 {#configuring-ssl-redirect}

SSL을 지원하도록 애플리케이션 서버를 구성한 후에는 애플리케이션 및 서비스에 대한 모든 HTTP 트래픽이 SSL 포트를 사용하도록 강제 적용되는지 확인해야 합니다.

WebSphere 또는 WebLogic에 대한 SSL 리디렉션을 구성하려면 애플리케이션 서버 설명서를 참조하십시오.

1. 명령 프롬프트를 열고 /JBOSS_HOME/standalone/configuration 디렉토리로 이동한 후 다음 명령을 실행합니다.

   `keytool -genkey -alias jboss7 -keyalg RSA -keystore server.keystore -validity 10950`

1. 편집할 JBOSS_HOME/standalone/configuration/standalone.xml 파일을 엽니다.

   다음 이후 &lt;subsystem xmlns=&quot;urn&lt;span id=&quot; translate=&quot;no&quot; />도메인:web:1.1&quot; native=&quot;false&quot; default-virtual-server=&quot;default-host&quot;> 요소, 다음 세부 정보를 추가합니다.:jboss:

   &lt;connector name=&quot;https&quot; protocol=&quot;HTTP/1.1&quot; scheme=&quot;https&quot; socket-binding=&quot;https&quot; enabled=&quot;true&quot; secure=&quot;true&quot;/>

1. https 커넥터 요소에 다음 코드를 추가합니다.

   ```xml
   <connector name="https" protocol="HTTP/1.1" scheme="https" socket-binding="https" secure="true" enabled="true"> 
    <ssl name="jboss7_ssl" key-alias="jboss71" password="Tibco321" certificate-key-file="../standalone/configuration/server.keystore" protocol="TLSv1"/> 
    </connector>
   ```

   standalone.xml 파일을 저장하고 닫습니다.

## Windows별 보안 권장 사항 {#windows-specific-security-recommendations}

이 섹션에는 JEE에서 AEM Forms을 실행하는 데 사용할 때 Windows와 관련된 보안 권장 사항이 포함되어 있습니다.

### JBoss 서비스 계정 {#jboss-service-accounts}

AEM Forms on JEE 턴키 설치는 기본적으로 로컬 시스템 계정을 사용하여 서비스 계정을 설정합니다. 기본 제공 로컬 시스템 사용자 계정은 관리자 그룹의 일부로 높은 수준의 접근성을 가집니다. 작업자 프로세스 ID가 로컬 시스템 사용자 계정으로 실행되는 경우 해당 작업자 프로세스는 전체 시스템에 대한 전체 액세스 권한을 갖습니다.

#### 비관리 계정을 사용하여 애플리케이션 서버 실행 {#run-the-application-server-using-a-non-administrative-account}

1. MMC(Microsoft Management Console)에서 다음과 같이 로그인할 Forms Server 서비스에 대한 로컬 사용자를 작성합니다.

   * 선택 **사용자가 암호를 변경할 수 없음**.
   * 다음에서 **구성원** 탭에서 사용자 그룹이 나열되어 있는지 확인합니다.

1. 선택 **설정** > **관리 도구** > **서비스**.
1. 응용 프로그램 서버 서비스를 두 번 클릭하고 서비스를 중지합니다.
1. 다음에서 **로그온** 탭, 선택 **이 계정**&#x200B;를 클릭하고 생성한 사용자 계정을 찾은 다음 계정 암호를 입력합니다.
1. 로컬 보안 설정 창의 사용자 권한 할당에서 Forms 서버가 실행 중인 사용자 계정에 다음 권한을 부여합니다.

   * 터미널 서비스를 통한 로그온 거부
   * 로컬에서 로그 거부 xx
   * 서비스로 로그온(이미 설정되어야 함)

1. 새 사용자 계정에 다음 디렉터리에 대한 수정 권한을 부여합니다.
   * **GDS(전역 문서 저장소) 디렉터리**: AEM Forms 설치 프로세스 중에 GDS 디렉토리 위치가 수동으로 구성됩니다. 설치하는 동안 위치 설정이 비어 있으면 기본적으로 다음 위치에 애플리케이션 서버가 설치되는 디렉토리가 사용됩니다. `[JBoss root]/server/[type]/svcnative/DocumentStorage`
   * **CRX-Repository 디렉토리**: 기본 위치는 입니다. `[AEM-Forms-installation-location]\crx-repository`
   * **AEM Forms 임시 디렉터리**:
      * (Windows) 환경 변수에 설정된 TMP 또는 TEMP 경로
      * (AIX, Linux 또는 Solaris) 로그인한 사용자의 홈 디렉토리 UNIX 기반 시스템에서 루트가 아닌 사용자는 다음 디렉토리를 임시 디렉토리로 사용할 수 있습니다.
      * (Linux) /var/tmp 또는 /usr/tmp
      * (AIX) /tmp 또는 /usr/tmp
      * (Solaris) /var/tmp 또는 /usr/tmp
1. 새 사용자 계정에 다음 디렉터리에 대한 쓰기 권한을 부여합니다.
   * [JBoss-directory]\standalone\deployment
   * [JBoss-directory]\standalone\
   * [JBoss-directory]\bin\

   >[!NOTE]
   >
   >JBoss Application Server의 기본 설치 위치:
   >
   >* Windows: C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   >* Linux: /opt/jboss/.

1. 응용 프로그램 서버 서비스를 시작합니다.

### 파일 시스템 보안 {#file-system-security}

AEM Forms on JEE는 다음과 같은 방법으로 파일 시스템을 사용합니다.

* 문서 입력 및 출력을 처리하는 동안 사용되는 임시 파일을 저장합니다.
* 설치된 솔루션 구성 요소를 지원하는 데 사용되는 파일을 글로벌 아카이브 저장소에 저장합니다.
* 감시 폴더는 파일 시스템 폴더 위치에서 서비스 입력으로 사용되는 드롭된 파일을 저장합니다

Forms Server 서비스를 사용하여 문서를 보내고 받는 방법으로 감시 폴더를 사용할 때는 파일 시스템 보안에 각별한 주의를 기울여야 합니다. 사용자가 감시 폴더에 컨텐츠를 놓으면 해당 컨텐츠가 감시 폴더를 통해 노출됩니다. 이 경우 서비스는 실제 최종 사용자를 인증하지 않습니다. 대신 ACL 및 공유 수준 보안을 폴더 수준에서 설정하여 누가 서비스를 효과적으로 호출할 수 있는지 결정합니다.

## JBoss 관련 보안 권장 사항 {#jboss-specific-security-recommendations}

이 섹션에는 JEE에서 AEM Forms을 실행하는 데 사용되는 경우 JBoss 7.0.6과 관련된 애플리케이션 서버 구성 권장 사항이 포함되어 있습니다.

### JBoss 관리 콘솔 및 JMX 콘솔 비활성화 {#disable-jboss-management-console-and-jmx-console}

턴키 설치 방법을 사용하여 JBoss의 JEE에 AEM Forms을 설치할 때 JBoss 관리 콘솔 및 JMX 콘솔에 대한 액세스가 이미 구성되었습니다(JMX 모니터링이 비활성화됨). 고유한 JBoss 애플리케이션 서버를 사용하는 경우 JBoss 관리 콘솔 및 JMX 모니터링 콘솔에 대한 액세스가 안전한지 확인합니다. JMX 모니터링 콘솔에 대한 액세스는 jmx-invoker-service.xml이라는 JBoss 구성 파일에서 설정됩니다.

### 디렉터리 검색 사용 안 함 {#disable-directory-browsing}

Administration Console에 로그인한 후 URL을 수정하여 콘솔의 디렉토리 목록을 검색할 수 있습니다. 예를 들어 URL을 다음 URL 중 하나로 변경하면 디렉터리 목록이 나타날 수 있습니다.

```java
https://<servername>:8080/adminui/secured/ 
https://<servername>:8080/um/
```

## WebLogic별 보안 권장 사항 {#weblogic-specific-security-recommendations}

이 섹션에는 JEE에서 AEM Forms을 실행할 때 WebLogic 9.1을 보호하기 위한 애플리케이션 서버 구성 권장 사항이 포함되어 있습니다.

### 디렉터리 검색 사용 안 함 {#disable_directory_browsing-1}

weblogic.xml 파일의 index-directories 속성을 다음으로 설정 `false`을 참조하십시오.

```xml
<container-descriptor> 
    <index-directory-enabled>false 
    </index-directory-enabled> 
</container-descriptor>
```

### WebLogic SSL 포트 활성화 {#enable-weblogic-ssl-port}

기본적으로 WebLogic은 기본 SSL 수신 포트 7002를 활성화하지 않습니다. SSL을 구성하기 전에 WebLogic Server 관리 콘솔에서 이 포트를 활성화하십시오.

## WebSphere 관련 보안 권장 사항 {#websphere-specific-security-recommendations}

이 섹션에는 JEE에서 AEM Forms을 실행하는 WebSphere 보안을 위한 애플리케이션 서버 구성 권장 사항이 포함되어 있습니다.

### 디렉터리 검색 사용 안 함 {#disable_directory_browsing-2}

설정 `directoryBrowsingEnabled` ibm-web-ext.xml 파일의 속성 `false`.

### WebSphere 관리 보안 활성화 {#enable-websphere-administrative-security}

1. WebSphere 관리 콘솔에 로그인합니다.
1. 탐색 트리에서 로 이동합니다. **보안** > **전역 보안**
1. 선택 **관리 보안 활성화**.
1. 둘 다 선택 해제 **애플리케이션 보안 활성화** 및 **Java 2 보안 사용**.
1. 클릭 **확인** 또는 **적용**.
1. 다음에서 **메시지** 상자, 클릭 **마스터 구성에 직접 저장**.
