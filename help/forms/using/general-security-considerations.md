---
title: JEE의 AEM Forms에 대한 일반 보안 고려 사항
description: JEE 환경에서 AEM Forms을 강화하기 위해 준비하는 방법에 대해 알아봅니다.
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
docset: aem65
role: Admin
exl-id: 3f150dd5-f486-4f16-9de9-035cde53b034
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1030'
ht-degree: 1%

---

# JEE의 AEM Forms에 대한 일반 보안 고려 사항{#general-security-considerations-for-aem-forms-on-jee}

이 문서에서는 AEM Forms 환경을 강화하기 위해 준비하는 데 도움이 되는 소개 정보를 제공합니다. 여기에는 JEE의 AEM Forms, 운영 체제, 애플리케이션 서버 및 데이터베이스 보안에 대한 사전 요구 사항 정보가 포함되어 있습니다. 환경 잠금을 계속하기 전에 이 정보를 검토하십시오.

## 공급업체별 보안 정보 {#vendor-specific-security-information}

이 섹션에는 AEM Forms on JEE 솔루션에 통합된 운영 체제, 애플리케이션 서버 및 데이터베이스에 대한 보안 관련 정보가 포함되어 있습니다.

이 섹션의 링크를 사용하여 운영 체제, 데이터베이스 및 애플리케이션 서버에 대한 공급업체별 보안 정보를 확인하십시오.

### 운영 체제 보안 정보 {#operating-system-security-information}

운영 체제를 보호할 때는 다음을 포함하여 운영 체제 공급업체에서 설명한 조치를 이행하는 것이 좋습니다.

* 사용자, 롤 및 권한 정의 및 제어
* 로그 및 감사 추적 모니터링
* 불필요한 서비스 및 응용 프로그램 제거
* 파일 백업

AEM Forms on JEE가 지원하는 운영 체제에 대한 보안 정보는 다음 표의 리소스를 참조하십시오.

<table>
 <thead>
  <tr>
   <th><p>운영 체제</p> </th>
   <th><p>보안 리소스</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>IBM® AIX® 7.2</p> </td>
   <td><p><a href="https://www.ibm.com/support/knowledgecenter/ssw_aix_72/com.ibm.aix.security/security-kickoff.htm" target="_blank">IBM® AIX® 보안의 이점</a></p> </td>
  </tr>
  <tr>
   <td><p>Microsoft® Windows Server® 2016 </p> </td>
   <td><p><a href="https://cloudblogs.microsoft.com/windowsserver/2017/08/22/now-available-windows-server-2016-security-guide/">Windows Server 2016 보안 안내서</a></p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® Linux® AP 또는 ES</p> </td>
   <td><p><a href="https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/pdf/security_guide/Red_Hat_Enterprise_Linux-7-Security_Guide-en-US.pdf" target="_blank">Red Hat® Enterprise Linux® 보안 안내서</a></p> </td>
  </tr>
  <tr>
   <td><p>Sun Solaris™ 11</p> </td>
   <td><p><a href="https://docs.oracle.com/cd/E53394_01/html/E54807/index.html" target="_blank">보안 및 강화 지침</a></p> </td>
  </tr>
  <tr>
   <td>Oracle Linux® 7 업데이트 3</td>
   <td><a href="https://docs.oracle.com/en/operating-systems/oracle-linux/7/security/" target="_blank">릴리스 7에 대한 보안 안내서</a><br /> </td>
  </tr>
  <tr>
   <td>센트OS 7<sup> </sup></td>
   <td><a href="https://wiki.centos.org/HowTos/OS_Protection" target="_blank">보호 설명서</a></td>
  </tr>
 </tbody>
</table>

### 응용 프로그램 서버 보안 정보 {#application-server-security-information}

애플리케이션 서버의 보안을 설정할 때는 다음을 포함하여 서버 공급업체에서 설명한 조치를 구현하는 것을 신중하게 고려하십시오.

* 명확하지 않은 관리자 사용자 이름 사용
* 불필요한 서비스 비활성화
* 콘솔 관리자 보호
* 보안 쿠키 활성화
* 불필요한 포트 닫기
* IP 주소 또는 도메인으로 클라이언트 제한
* Java™ Security Manager를 사용하여 권한을 프로그래밍 방식으로 제한

JEE의 AEM Forms이 지원하는 애플리케이션 서버에 대한 보안 정보는 이 표의 리소스를 참조하십시오.

<table>
 <thead>
  <tr>
   <th><p>응용 프로그램 서버</p> </th>
   <th><p>보안 리소스</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Oracle WebLogic®</p> </td>
   <td><p>에서 WebLogic 보안 이해 검색 <a href="https://docs.oracle.com/">https://docs.oracle.com/</a>.</p> </td>
  </tr>
  <tr>
   <td><p>IBM® WebSphere®</p> </td>
   <td><p><a href="https://www.ibm.com/developerworks/websphere/zones/was/security/" target="_blank">애플리케이션 및 환경 보호</a></p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® JBoss®</p> </td>
   <td><p><a href="https://docs.jboss.org/author/display/AS7/Security%20subsystem%20configuration.html">보안 하위 시스템 구성</a></p> </td>
  </tr>
 </tbody>
</table>

### 데이터베이스 보안 정보 {#database-security-information}

데이터베이스 보안을 설정할 때는 다음을 포함하여 데이터베이스 공급업체에서 설명한 조치를 구현하는 것이 좋습니다.

* ACL(액세스 제어 목록)을 사용하여 작업 제한
* 비표준 포트 사용
* 방화벽 뒤에 데이터베이스 숨기기
* 중요한 데이터를 데이터베이스에 쓰기 전에 암호화(데이터베이스 제조업체의 설명서 참조)

JEE의 AEM Forms이 지원하는 데이터베이스에 대한 보안 정보는 이 표의 리소스를 참조하십시오.

<table>
 <thead>
  <tr>
   <th><p>데이터베이스</p> </th>
   <th><p>보안 리소스</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>IBM® DB2® 11.1</p> </td>
   <td><p><a href="https://www-01.ibm.com/software/data/db2/library/">DB2® 제품군 라이브러리</a></p> </td>
  </tr>
  <tr>
   <td><p>Microsoft® SQL Server 2016</p> </td>
   <td>웹에서 "SQL Server 2016: 보안"을 검색합니다.</td>
  </tr>
  <tr>
   <td><p>내 SQL 5</p> </td>
   <td><p><a href="https://dev.mysql.com/doc/refman/5.0/en/security.html">MySQL 5.0 일반 보안 문제</a></p> <p><a href="https://dev.mysql.com/doc/refman/5.1/en/security.html">MySQL 5.1 일반 보안 문제</a></p> </td>
  </tr>
  <tr>
   <td><p>Oracle® 12c</p> </td>
   <td><p>의 보안 챕터를 참조하십시오. <a href="https://docs.oracle.com/database/121/TDPSG/GUID-6E2F4E53-5D87-4FCD-9C9C-6792217D7014.htm#TDPSG94426" target="_blank">Oracle 12g 설명서</a></p> </td>
  </tr>
 </tbody>
</table>

이 표에서는 JEE에서 AEM Forms 구성 프로세스 중에 열어야 하는 기본 포트에 대해 설명합니다. https를 통해 연결하는 경우 그에 따라 포트 정보와 IP 주소를 조정합니다. 포트 구성에 대한 자세한 내용은 *JEE에 AEM Forms 설치 및 배포* 애플리케이션 서버용 문서입니다.

<table>
 <thead>
  <tr>
   <th><p>제품 또는 서비스</p> </th>
   <th><p>포트 번호</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>JBoss®</p> </td>
   <td><p>8080</p> </td>
  </tr>
  <tr>
   <td><p>WebLogic</p> </td>
   <td><p>7001</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>WebLogic 관리 서버</p> </td>
   <td><p>구성 중에 관리자가 설정</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>WebSphere®</p> </td>
   <td><p>9060, 글로벌 보안이 활성화된 경우 기본 SSL 포트 값은 9043입니다.</p> <p>9080</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>BAM 서버</p> </td>
   <td><p>7001</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>SOAP</p> </td>
   <td><p>8880</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>MySQL</p> </td>
   <td><p>3306</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>Oracle</p> </td>
   <td><p>1521</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>DB2®</p> </td>
   <td><p>50000</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>SQL 서버</p> </td>
   <td><p>1433</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>LDAP</p> </td>
   <td><p>LDAP 서버가 실행 중인 포트입니다. 기본 포트는 일반적으로 389입니다. 그러나 SSL 옵션을 선택하는 경우 기본 포트는 일반적으로 636입니다. 지정할 포트를 LDAP 관리자에게 확인합니다.</p> </td>
  </tr>
 </tbody>
</table>

### 기본이 아닌 HTTP 포트를 사용하도록 JBoss® 구성 {#configuring-jboss-to-use-a-non-default-http-port}

JBoss® Application Server는 8080을 기본 HTTP 포트로 사용합니다. JBoss®에는 jboss-service.xml 파일에 주석 처리된 사전 구성된 포트 8180, 8280 및 8380도 있습니다. 컴퓨터에 이미 이 포트를 사용하는 응용 프로그램이 있는 경우 다음 단계에 따라 JEE의 AEM Forms에서 사용하는 포트를 변경하십시오.

1. 편집할 다음 파일을 엽니다.

   단일 서버 설치: [JBoss® 루트]/standalone/configuration/standalone.xml

   클러스터 설치: [JBoss® 루트]/domain/configuration/domain.xml

1. 값 변경 **포트** 의 속성 **&lt;socket-binding>** 사용자 지정 포트 번호로 태그 지정합니다. 예를 들어, 다음은 포트 8090을 사용합니다.

   &lt;socket-binding name=&quot;http&quot; port=&quot;8090&quot;/>

1. 파일을 저장하고 닫습니다.
1. JBoss® 응용 프로그램 서버를 다시 시작합니다.

>[!NOTE]
>
> SDK를 다시 시작하려면 &#39;Ctrl + C&#39; 명령을 사용하는 것이 좋습니다. Java 프로세스 중지와 같은 대체 방법을 사용하여 AEM SDK를 다시 시작하면 AEM 개발 환경이 일치하지 않을 수 있습니다.

## JEE의 AEM Forms 보안 고려 사항 {#aem-forms-on-jee-security-considerations}

이 섹션에서는 알아야 하는 JEE별 보안 문제에 대한 일부 AEM Forms에 대해 설명합니다.

### 데이터베이스에서 이메일 자격 증명이 암호화되지 않음 {#email-credentials-not-encrypted-in-database}

애플리케이션이 저장하는 이메일 자격 증명은 AEM Forms on JEE 데이터베이스에 저장되기 전에 암호화되지 않습니다. 전자 메일을 사용하도록 서비스 끝점을 구성할 때 해당 끝점 구성의 일부로 사용되는 모든 암호 정보는 데이터베이스에 저장될 때 암호화되지 않습니다.

### 데이터베이스의 Rights Management에 대한 중요 콘텐츠 {#sensitive-content-for-rights-management-in-the-database}

AEM Forms on JEE는 AEM Forms on JEE 데이터베이스를 사용하여 중요한 문서 키 정보와 정책 문서에 사용되는 기타 암호화 자료를 저장합니다. 침입으로부터 데이터베이스를 보호하면 이러한 중요한 정보를 보호할 수 있습니다.

### 일반 텍스트 형식의 암호 {#password-in-clear-text-format-in-adobe-ds-xml}

JEE에서 AEM Forms을 실행하는 데 사용되는 애플리케이션 서버에는 애플리케이션 서버에 구성된 데이터 소스를 통해 데이터베이스에 액세스하기 위한 자체 구성이 필요합니다. 응용 프로그램 서버가 데이터 소스 구성 파일의 일반 텍스트로 데이터베이스 암호를 노출하지 않도록 합니다.

lc_[데이터베이스].xml 파일에는 일반 텍스트 형식의 암호를 사용할 수 없습니다. 애플리케이션 서버의 암호를 암호화하는 방법에 대해서는 애플리케이션 서버 공급업체에 문의하십시오.

>[!NOTE]
>
>AEM Forms on JEE JBoss® 턴키 설치 관리자가 데이터베이스 암호를 암호화합니다.

IBM® WebSphere® Application Server 및 Oracle WebLogic Server는 기본적으로 데이터 소스 암호를 암호화할 수 있습니다. 하지만 애플리케이션 서버 설명서에 확인하여 제대로 작동하는지 확인해야 합니다.

### Trust Store에 저장된 개인 키 보호 {#protecting-the-private-key-stored-in-trust-store}

Trust Store에서 가져온 개인 키 또는 자격 증명은 AEM Forms on JEE 데이터베이스에 저장됩니다. 데이터베이스를 보호하고 지정된 관리자에게만 액세스를 제한하려면 적절한 예방 조치를 취하십시오.
