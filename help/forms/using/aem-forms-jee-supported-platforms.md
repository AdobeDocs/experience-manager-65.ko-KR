---
title: JEE에서 AEM Forms에 대해 지원되는 플랫폼
seo-title: JEE에서 AEM Forms에 대해 지원되는 플랫폼
description: JEE에 AEM Forms 설치를 위해 필수 및 지원되는 인프라 구성 요소 목록
seo-description: JEE에 AEM Forms 설치를 위해 필수 및 지원되는 인프라 구성 요소 목록
uuid: 777f943b-4cb4-444e-a036-8032b9fce5be
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: f777865e-d4a8-40ef-87b0-130c19eb1b91
docset: aem65
role: Administrator
exl-id: 74d22cf4-56b2-48f5-92d9-928eaa134866
source-git-commit: 1cef6f87fa66fd78d439c23e6ac907f9531b8fd6
workflow-type: tm+mt
source-wordcount: '3309'
ht-degree: 1%

---

# JEE{#supported-platforms-for-aem-forms-on-jee}에서 AEM Forms에 대해 지원되는 플랫폼

## 지원되는 플랫폼 {#supported-platforms}

### 지원 수준 {#support-levels}

JEE 서버의 AEM Forms은 지원되는 운영 체제, 애플리케이션 서버, 데이터베이스, 데이터베이스 드라이버, JDK, LDAP 서버 및 이메일 서버의 조합을 사용하여 설정할 수 있습니다.

이 문서에서는 JEE에서 AEM Forms에 대해 지원되는 클라이언트 및 서버 플랫폼을 나열합니다. Adobe은 권장 구성과 기타 구성에 대해 여러 수준의 지원을 제공합니다. 또한 이 문서에서는 지원되는 다른 소프트웨어 및 해당 버전, 예외, 패치 정의 및 타사 소프트웨어 패치 지원 정책을 나열합니다.

>[!NOTE]
>
>* 지원되는 서버 플랫폼에 대한 전체 예외 목록은 [지원되는 서버 플랫폼에 대한 예외](../../forms/using/aem-forms-jee-supported-platforms.md#p-exceptions-to-supported-server-platforms-p)를 참조하십시오.
>* AEM Forms on JEE는 지원되는 운영 체제 및 응용 프로그램의 영어, 프랑스어, 독일어 및 일본어 버전만 지원합니다.
>



### 권장 구성 {#recommendedconfigurations}

Adobe은 이러한 구성을 권장하며 표준 소프트웨어 유지 관리 계약의 일부로 전체 또는 제한된 지원을 제공합니다.

<table>
 <tbody>
  <tr>
   <th>지원 수준</th>
   <th>설명</th>
  </tr>
  <tr>
   <td>A:지원됨<br /> </td>
   <td>Adobe은 이 구성에 대한 모든 지원 및 유지 관리를 제공합니다. 이 구성은 Adobe의 품질 보증 프로세스에서 다룹니다.</td>
  </tr>
  <tr>
   <td>R:제한된 지원</td>
   <td>Adobe은 특정 사전 요구 사항을 충족한 후 이 구성에 대한 모든 지원을 제공합니다. 사전 요구 사항에 대해 알아보고 지원 요청을 제기하려면 Adobe 엔터프라이즈 지원에 문의하십시오.</td>
  </tr>
  <tr>
   <td>L:제한된 지원</td>
   <td>Adobe은 특정 사전 요구 사항을 충족한 후 이 구성에 대한 모든 지원 및 유지 관리를 제공합니다. 일부 기능은 구성에서 사용할 수 없습니다. 전제 조건에 대한 자세한 내용을 알고 지원을 요청하려면 Adobe 엔터프라이즈 지원에 문의하십시오.<br /> </td>
  </tr>
 </tbody>
</table>

### 지원되지 않는 구성 {#unsupported-configurations}

| 지원 수준 | 설명 |
|---|---|
| E:작동해야 함 | 구성이 작동될 것으로 예상되며, 반대의 보고는 없습니다. |
| Z:지원되지 않음 | 구성이 지원되지 않습니다. Adobe은 구성 작동 여부에 대한 설명을 만들지 않으며 구성을 지원하지 않습니다. |

>[!NOTE]
>
>AEM Forms 고객이 TCO 절감, 배포 아키텍처 간소화 및 개발 스택 현대화를 수행할 수 있도록 지원하기 위해 Adobe Experience Manager 엔터프라이즈 플랫폼은 독립 실행형 OSGi 기반 배포를 위해 애플리케이션 서버 기반 배포에서 벗어납니다. Adobe은 인프라 구성 요소의 매트릭스 감소된 상태로 AEM Forms JEE 스택을 계속 지원합니다.
>
>6.5 릴리스를 통해 고객 중 사용량이 가장 적은 인프라 구성 요소는 다음과 같이 더 이상 지원되지 않습니다.
>・ IBM DB2 데이터베이스
>・ IBM AIX 및 Sun Solaris 운영 체제
>
>새로운 설치의 경우 양식 데이터 모델을 사용하여 모바일, 다중 채널 인터랙티브 통신 및 백엔드 데이터 통합을 위한 응답형 Forms을 활용하는 데 최신 혁신을 위해 최신 OSGi 스택에 AEM Forms을 배포하는 것이 좋습니다.
>
>기존 사용자가 JEE 스택에 AEM Forms을 계속 배포해야 한다는 것을 알고 있습니다. 이러한 시나리오에서 Adobe은 이 설명서에 설명된 대로 지원되는 인프라에 AEM Forms JEE를 배포해야 합니다. AEM 6.5 Forms으로 업그레이드하고 이전 AEM Forms 릴리스에서 지원되지 않는 플랫폼을 사용하는 경우 Adobe 지원 센터에 문의하여 지원되는 플랫폼으로 업그레이드하는 방법에 대한 도움말을 볼 수 있습니다.

### Java Virtual Machine(JVM) {#java-virtual-machines-jvm}

Adobe Experience Manager Forms을 사용하려면 JDK(Java Development Kit) 배포에서 제공하는 Java Virtual Machine을 실행해야 합니다. Adobe Experience Manager은 다음 버전의 Java Virtual Machine을 사용하여 작동합니다.

<table>
 <tbody>
  <tr>
   <th><p><strong>플랫폼</strong></p> </th>
   <th><p><strong>지원 수준</strong></p> </th>
   <th><p><strong>지원되는 패치 정의</strong></p> </th>
  </tr>
  <tr>
   <td><p>Oracle Java™ SE 11(64비트)</p> </td>
   <td><p>Z:지원되지 않음</p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td>Oracle Java™ SE 8(64비트)</td>
   <td>A:지원됨</td>
   <td>사소한 릴리스 및 업데이트</td>
  </tr>
  <tr>
   <td>IBM® J9 가상 컴퓨터(빌드 2.8, JRE 1.8.0)</td>
   <td>A:지원됨</td>
   <td>사소한 릴리스 및 업데이트</td>
  </tr>
  <tr>
   <td>IBM® J9 가상 컴퓨터(빌드 2.9, JRE 1.8.0)<br /> </td>
   <td>A:지원됨</td>
   <td>사소한 릴리스 및 업데이트</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* 프로덕션 환경의 안전과 보안을 유지하고 최신 Java 업데이트를 설치하려면 Java 공급업체에서 제공하는 보안 게시판을 추적하는 것이 좋습니다.
>* AEM Forms on JEE는 프로덕션 환경에서 64비트 JVM만 지원합니다.


### 데이터베이스 및 CRX 지속성 {#databases-and-crx-persistence}

<table>
 <tbody>
  <tr>
   <td><p><strong>플랫폼</strong></p> </td>
   <td><p><strong> 설명</strong></p> </td>
   <td><p><strong>지원 수준</strong></p> </td>
  </tr>
  <tr>
   <td><p>파일 시스템</p> </td>
   <td><p>저장소 마이크로커널(TAR MK 파일)</p> </td>
   <td><p>지원됨</p> </td>
  </tr>
  <tr>
   <td><p>MongoDB Enterprise 4.0 </p> </td>
   <td><p>저장소 마이크로커널</p> </td>
   <td><p>지원됨</p> </td>
  </tr>
  <tr>
   <td><p>Oracle 데이터베이스 12c 릴리스 1</p> </td>
   <td><p>저장소 마이크로커널</p> </td>
   <td><p>지원됨</p> </td>
  </tr>
   <tr>
   <td><p>Oracle 데이터베이스 12c 릴리스 2(12.2.0.1.0)</p> </td>
   <td><p>저장소 마이크로커널</p> </td>
   <td><p>지원됨</p> </td>
  </tr>
  <tr>
   <td>Oracle 데이터베이스 18c </td>
   <td>저장소 마이크로커널</td>
   <td>지원됨</td>
  </tr> 
   <tr>
   <td>Oracle 데이터베이스 19c(표준, RAC(Real Application Clusters) 및 Enterprise 버전) </td>
   <td>리포지토리 마이크로커널 </td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td><p>Microsoft SQL Server 2016</p> </td>
   <td><p>저장소 마이크로커널</p> </td>
   <td><p>지원됨</p> </td>
  </tr>
  <tr>
   <td><p>Microsoft SQL Server 2019</p> </td>
   <td><p>저장소 마이크로커널</p> </td>
   <td><p>지원됨</p> </td>
  </tr>
  <tr>
   <td>IBM DB2 11.1</td>
   <td>저장소 마이크로커널</td>
   <td>R:제한된 지원</td>
  </tr>
    <tr>
   <td>MySQL 5.7.19 </td>
   <td>-</td>
   <td>R:제한된 지원</td>
  </tr>
 </tbody>
</table>

* IBM DB2는 새로 설치할 때 지원되지 않습니다. AEM 6.5 Forms으로 업그레이드하는 기존 고객에게만 지원됩니다.
* MongoDB는 타사 소프트웨어이며 AEM 라이선스 패키지에 포함되어 있지 않습니다. 자세한 내용은 [MongoDB 라이선스 정책](https://www.mongodb.org/about/licensing/) 페이지를 참조하십시오.
* AEM을 최대한 활용하려면 MongoDB Enterprise 버전의 라이센스를 취득하여 전문 지원을 받는 것이 좋습니다.
* Adobe 고객 지원 팀은 AEM에서 MongoDB 사용과 관련된 자격 있는 문제를 지원합니다. 자세한 내용은 [Adobe Experience Manager용 MongoDB 페이지](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)를 참조하십시오.
* &#39;파일 시스템&#39;에는 POSIX 호환 블록 저장소가 포함됩니다. 여기에는 네트워크 스토리지 기술이 포함됩니다. 파일 시스템 성능은 다를 수 있으며 전체 성능에 영향을 줄 수 있습니다. 네트워크/원격 파일 시스템과 함께 테스트 AEM을 로드하는 것이 좋습니다.
* MongoDB 스토리지 엔진 WiredTiger만 지원됩니다.
* MongoDB 공유는 AEM에서 지원되지 않습니다.
* JEE의 AEM Forms은 RDBMK 지속성에 대한 MySQL을 지원하지 않습니다.
* 문서 보안 모듈은 콘텐츠 저장소를 사용하지 않습니다. 즉, 문서 보안만 사용하고 HTML 작업 공간, HTML5 양식 또는 적응형 양식을 사용할 계획이 없는 경우 컨텐츠 저장소를 설치하지 마십시오.
* JEE의 AEM Forms은 AEM 저장소 유지를 위한 MySQL 사용을 지원하지 않습니다(CRX-Repository).


### 데이터베이스 드라이버 {#database-drivers}

<table>
 <tbody>
  <tr>
   <th>데이터베이스 </th>
   <th><p><strong>플랫폼</strong></p> </th>
   <th><p><strong>지원되는 패치 정의</strong></p> </th>
  </tr>
  <tr>
   <td>MySQL</td>
   <td><p>MySQL Connector/J 5.7</p> <p>mysql-connector-java-5.1.44-bin.jar(버전 5.1.44)</p> </td>
   <td><p>JEE 설치 시 AEM Forms과 함께 제공됨</p> </td>
  </tr>
  <tr>
   <td>Microsoft SQL Server<br /> </td>
   <td><p>Microsoft® SQL Server JDBC 드라이버 6.2.1.0<br /> </p> <p>sqljdbc6.jar</p> </td>
   <td><p>JEE 설치 시 AEM Forms과 함께 제공됩니다.</p> </td>
  </tr>
  <tr>
   <td>Microsoft SQL Server<br /> </td>
   <td><p>Microsoft® SQL Server JDBC 드라이버 8.2.2<br /> </p> <p>sqljdbc8.jar</p> </td>
   <td><p>Microsoft 웹 사이트에서 다운로드.</p> </td>
  </tr>
  <tr>
   <td>Oracle</td>
   <td><p>Oracle 데이터베이스 19.3.0.0.0 JDBC 드라이버</p> <p>ojdbc8.jar(버전 19.3.0.0.0)<br /> </p> </td>
   <td><p><a href="https://www.oracle.com/technetwork/database/features/jdbc/jdbc-ucp-122-3110062.html">Oracle 웹 사이트</a>에서 다운로드합니다.</p> </td>
  </tr>
 </tbody>
</table>

### 응용 프로그램 서버 {#application-servers}

<table>
 <tbody>
  <tr>
   <td><p><strong> 플랫폼</strong></p> </td>
   <td><p><strong>지원 수준</strong></p> </td>
   <td><p><strong>지원되는 패치 정의</strong></p> </td>
  </tr>
  <tr>
   <td>Oracle WebLogic Server 12.2.1(12c R2)</td>
   <td>A:지원됨</td>
   <td>서비스 팩 및 중요 업데이트</td>
  </tr>
  <tr>
   <td>IBM® WebSphere® Application Server 9.0 <sup>[1] [4]</sup><br /> </td>
   <td>A:지원됨</td>
   <td>서비스 팩 및 중요 업데이트</td>
  </tr>
  <tr>
   <td><p>JBoss® EAP(엔터프라이즈 응용 프로그램 플랫폼) 7.1.4 <sup>[2] [3] [7]</sup></p> </td>
   <td><p>A:지원됨</p> </td>
   <td><p>지원되는 EAP 버전에 대한 패치 및 누적 패치</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>IBM® WebSphere® 클러스터는 Network Deployment Edition에서만 지원됩니다.

### 서버 운영 체제 {#server-operating-systems}

#### 프로덕션 환경 {#production-environments}

<table>
 <tbody>
  <tr>
   <th><p><strong> 플랫폼</strong></p> </th>
   <th><p><strong>지원 수준</strong></p> </th>
   <th><p><strong>지원되는 패치 정의</strong></p> </th>
  </tr>
  <tr>
   <td>Microsoft Windows Server 2016(64비트)</td>
   <td>A:지원됨</td>
   <td>서비스 팩 및 중요 업데이트</td>
  </tr>
  <tr>
   <td><p>Red Hat Enterprise Linux 7(커널 3.x)(64비트)</br><b>참고:</b> <a href="https://access.redhat.com/articles/4665701">Red Hat Enterprise Linux 6</a>은 유지 관리 단계의 끝에 도달하고, 2020년 11월 30일에 확장 수명 주기 지원 단계로 전환합니다. Adobe은 업그레이드 및 새 설치에 Red Hat Enterprise Linux 7을 권장합니다. 기존 설치에서는 Extended Life Cycle Support 단계 동안 Red Hat Enterprise Linux 6을 사용할 수 있습니다.</p> </td>
   <td><p>A:지원됨</p> </td>
   <td><p>사소한 릴리스, 누적 업데이트 및 중요 업데이트</p> </td>
  </tr>
  <tr>
   <td><p>SUSE® Linux® Enterprise Server 12(64비트)</p> </td>
   <td><p>A:지원됨</p> </td>
   <td><p>서비스 팩, 누적 패치 및 중요 보안 업데이트</p> </td>
  </tr>
  <tr>
   <td>Oracle Linux® 7 업데이트 3(64비트)</td>
   <td>A:지원됨</td>
   <td>서비스 팩, 누적 패치 및 중요 보안 업데이트</td>
  </tr>
  <tr>
   <td>CentOS 7(64비트)<sup> [6]</sup></td>
   <td>A:지원됨</td>
   <td>서비스 팩, 누적 패치 및 중요 보안 업데이트</td>
  </tr>
 </tbody>
</table>

#### 가상화 환경 {#virtualized-environment}

물리적 컴퓨터 또는 가상 환경에서 JEE에서 AEM Forms을 실행할 수 있습니다. 그러나 가상 환경에서 AEM Forms에 문제가 발생하면 실제 컴퓨터에서 해당 문제를 복제해 보십시오. 실제 컴퓨터에서 문제가 계속 발생하면 Adobe 지원 센터에 문의하여 해결 방법을 확인하십시오. 물리적 시스템에서 복제할 수 없는 문제는 가상 환경 공급업체에 문의하십시오.

#### 개발 환경 {#development-environments}

<table>
 <tbody>
  <tr>
   <th><p><strong>플랫폼(기본 버전)</strong></p> </th>
   <th>지원 수준</th>
   <th><p><strong>지원되는 패치 정의</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10 64비트</p> </td>
   <td>E:작동해야 함</td>
   <td><p>서비스 팩 및 중요 업데이트</p> </td>
  </tr>
 </tbody>
</table>

### 지원되는 서버 플랫폼에 대한 예외 {#exceptions-to-supported-server-platforms}

JEE 서버에서 AEM Forms을 설정할 플랫폼을 선택하는 동안 다음 예외를 고려하십시오.

1. JEE의 AEM Forms은 MySQL을 사용하는 IBM® WebSphere®를 지원하지 않습니다.
1. JEE의 AEM Forms은 SUSE Linux Enterprise Server 12의 JBoss 및 를 지원하지 않습니다. SUSE Linux Enterprise Server 12에서는 IBM WebSphere만 지원됩니다.
1. JEE의 AEM Forms은 Oracle Java™ SE 이외의 JBoss®를 사용하는 JDK를 지원하지 않습니다.
1. JEE의 AEM Forms은 IBM® JDK 이외의 IBM® WebSphere®를 사용하는 JDK를 지원하지 않습니다.
1. CRX 리포지토리는 TarMK, MongoDB 및 관계형 데이터베이스(RDBMK)의 지속성을 지원합니다. 애플리케이션 서버와 CRX 저장소 간에 두 개의 다른 데이터베이스 시스템을 가질 수 없습니다. 그러나 JEE 환경의 AEM Forms에서는 CRX 리포지토리와 함께 MongoMK 및 애플리케이션 서버와 함께 지원되는 관계형 데이터베이스를 사용할 수 있습니다.
1. JEE의 AEM Forms은 CentOS의 WebSphere 애플리케이션 서버를 지원하지 않습니다.
1. JEE의 AEM Forms은 RBAC(JBoss 역할 기반 액세스 제어)를 지원하지 않습니다.

또한 JEE 배포에서 AEM Forms Adobe 소프트웨어를 선택할 때 다음 사항을 고려하십시오.

* JEE의 AEM Forms은 지원되는 주요 버전 및 부 버전의 소프트웨어 위에 있는 업데이트, 패치 및 수정 팩을 지원합니다. 그러나 다음 주요 버전 또는 부 버전으로 업데이트는 명시하지 않는 한 지원되지 않습니다.
* 클러스터 기반 설치에서는 TarMK 지속성을 지원하지 않습니다. 지원되는 지속성에 대한 자세한 내용은 [AEM Forms 설치에 대한 지속성 유형 선택](/help/forms/using/choosing-persistence-type-for-aem-forms.md)을 참조하십시오.
* JEE의 AEM Forms은 [타사 소프트웨어 지원 정책](../../forms/using/aem-forms-jee-supported-platforms.md#p-third-party-patch-support-policy-p)에 따라 다양한 타사 소프트웨어를 지원합니다.
* JEE의 AEM Forms은 타사 공급업체가 제공하는 지원에 따라 플랫폼을 지원합니다. 일부 조합은 타사 공급업체에서 허용하지 않을 수 있습니다. 예를 들어, 많은 공급업체가 Oracle을 사용하여 애플리케이션 서버를 인증하지 않았습니다. 따라서 JEE의 AEM Forms도 이러한 조합을 지원하지 않습니다. 지원되는 소프트웨어 버전을 선택하려면 타사 공급업체의 지원 매트릭스도 확인하십시오.
* JEE의 AEM Forms은 TarMK Cold Standby를 지원하지 않습니다.
* JEE의 AEM Forms은 수직 클러스터링을 지원하지 않습니다.
* JEE의 AEM Forms은 클러스터된 환경에서 MySQL 데이터베이스를 지원하지 않습니다.
* 제거되었거나 업데이트된 플랫폼 목록에 대해서는 [AEM 6.5 Forms 새 기능 요약](../../forms/using/whats-new.md) 문서를 참조하십시오.

### LDAP 서버(선택 사항) {#ldap-servers-optional}

<table>
 <tbody>
  <tr>
   <th><p><strong>제품(기본 버전)</strong></p> </th>
   <th><p><strong>지원되는 패치 정의</strong></p> </th>
  </tr>
  <tr>
   <td>Oracle UD(Unified Directory) 11g 릴리스 2</td>
   <td>서비스 팩</td>
  </tr>
  <tr>
   <td>Microsoft Active Directory 2016</td>
   <td>유지 관리 릴리스 및 수정 팩</td>
  </tr>
  <tr>
   <td><p>IBM® Tivoli Directory Server 6.4</p> </td>
   <td><p>기능 팩 및 임시 수정 사항</p> </td>
  </tr>
 </tbody>
</table>

### 전자 메일 서버(선택 사항) {#email-servers-optional}

| 제품 |
|---|
| IBM Lotus Domino 9.0 |
| Microsoft Exchange 2013 |
| Microsoft Office 365 |

### 컨텐츠 관리자 및 해당 커넥터 {#content-managers-and-corresponding-connectors}

<table>
 <tbody>
  <tr>
   <td><strong>제품<br /> </strong></td>
   <td><strong>버전</strong></td>
  </tr>
  <tr>
   <td>EMC Documentum</td>
   <td>7.3</td>
  </tr>
  <tr>
   <td>IBM Filenet</td>
   <td>5.2</td>
  </tr>
  <tr>
   <td>IBM Filenet</td>
   <td>5.5.2</td>
  </tr>
  <tr>
   <td>IBM Content Manager Server</td>
   <td>8.5 수정 팩 2</td>
  </tr>
  <tr>
   <td>IBM Content Manager 클라이언트</td>
   <td>8.5 </td>
  </tr>
  <tr>
   <td>Microsoft Sharepoint</td>
   <td>2016<br /> </td>
  </tr>
 </tbody>
</table>

### Cordova {#support-for-cordova} 지원

AEM Forms 앱은 이제 Apache Cordova를 지원합니다. 다음은 지원되는 Cordova 플랫폼별 버전입니다.

* Apache Cordova 6.4.0
* Cordova iOS 4.3.0
* Cordova Android 6.0.0
* Cordova Windows 4.4.3

### PDF Generator에 대한 소프트웨어 지원 {#software-support-for-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>제품</strong></p> </th>
   <th><p><strong>PDF로 변환할 수 있는 지원되는 형식</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2017 classic </a> tracklatest 버전</td>
   <td>XPS, 이미지 형식(BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, DWG, DXF 및 DWF</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2016</td>
   <td>DOC, DOCX, XLS, XLSX, PPT, PPTX, RTF 및 TXT</td>
  </tr>
  <tr>
   <td>WordPerfect X7</td>
   <td>WP, WPD</td>
  </tr>
  <tr>
   <td>Microsoft® Office Visio 2016<br /> </td>
   <td>VSD, VSDX</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2016<br /> </td>
   <td>PUB</td>
  </tr>
  <tr>
   <td>Microsoft® Project 2016<br /> </td>
   <td>MPP</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.2</td>
   <td>ODT, ODP, ODS, ODG, SXW, SXW, SXD, XLS, XLSX, DOC, DOCX, PPT, PPTX, IMAGE 형식(BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPX, JPF, J2K, J2C, RTF, HTML, HTML, RTF, HTML, HTML, HTML, HTML, JTXC, HTML, XC, HTML, RTF 및 TXT</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>PDF Generator는 지원되는 운영 체제 및 응용 프로그램의 영어, 프랑스어, 독일어 및 일본어 버전만 지원합니다.
>
>또한
>
>* PDF Generator를 사용하려면 전환을 수행하려면 32비트 버전의 [Acrobat 2017 Classic 트랙 버전 17.011.30078 이상](https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html)이 필요합니다.
>* PDF Generator는 변환에 필요한 32비트 Retail 버전의 Microsoft Office Professional Plus와 기타 소프트웨어만 지원합니다.
>* PDF Generator는 Microsoft Office 365를 지원하지 않습니다.
>* OpenOffice용 PDF Generator 변환은 Windows 및 Linux에서만 지원됩니다.
>* OCR PDF, Optimize PDF 및 Export PDF 기능은 Windows에서만 지원됩니다.
>* Acrobat 버전은 PDF Generator 기능을 활성화하기 위해 AEM Forms과 번들로 제공됩니다. AEM Forms PDF Generator에서 사용할 수 있도록 번들로 제공되는 버전은 AEM Forms 라이센스 기간 동안 AEM Forms을 통해서만 프로그래밍 방식으로 액세스할 수 있습니다. 자세한 내용은 배포에 대한 AEM Forms 제품 설명([On-Premise](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html) 또는 [Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html))&quot;을 참조하십시오
   >
   >
* PDF Generator 서비스는 Microsoft Windows 10을 지원하지 않습니다.
>



### 액세스 가능성 지원 예외 {#exceptions-to-accessibility-support}

AEM Forms의 다음 하위 시스템은 [508](https://www.section508.gov/) 규격이 아닙니다.

* 적응형 Forms 작성 UI
* Forms Manager 작성 UI
* 서신 관리 작성 UI
* 관리 UI(관리 콘솔 UI)

## JEE의 AEM Forms 시스템 요구 사항 {#system-requirements-for-aem-forms-on-jee}

### 최소 하드웨어 요구 사항 {#minimum-hardware-requirements}

<table>
 <tbody>
  <tr>
   <td>플랫폼</td>
   <td>최소 하드웨어 요구 사항</td>
  </tr>
  <tr>
   <td>Microsoft Windows Server</td>
   <td>Intel® Xeon® E5-2680, 2.4GHz 프로세서 또는 동급<br /> VMWare ESX 5.1 이상<br /> RAM:6GB(64비트 JVM이 있는 64비트 OS)<br /> 사용 가능한 디스크 공간:15GB의 임시 공간 + JEE의 AEM Forms용 22GB<br /></td>
  </tr>
  <tr>
   <td>SUSE Linux Enterprise Server</td>
   <td>Intel Xeon E5-2670v2, 1vCPU, 2.5GHz 프로세서<br /> AWS m3.medium(3ECU)<br /> RAM:6GB(64비트 JVM이 있는 64비트 OS)<br /> 사용 가능한 디스크 공간:6GB의 임시 공간 + JEE의 AEM Forms용 22GB<br /></td>
  </tr>
  <tr>
   <td>Red Hat Enterprise Linux</td>
   <td>Intel Xeon E5-2670v2, 1vCPU, 2.5GHz 프로세서<br /> AWS m3.medium(3ECU)<br /> RAM:6GB(64비트 JVM이 있는 64비트 OS)<br /> 사용 가능한 디스크 공간:6GB의 임시 공간 + JEE의 AEM Forms용 22GB<br /><br /> </td>
  </tr>
  <tr>
   <td>소규모 운영 환경을 위한 하드웨어 요구 사항</td>
   <td>
    <ul>
     <li><strong>인텔 기반 환경</strong>:Intel® Xeon® E5-2680, 2.4GHz 이상 듀얼 코어 프로세서를 사용하면 성능이 더욱 향상됩니다</li>
     <li><strong>메모리: </strong>4GB  <br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

추가 요구 사항은 다음을 참조하십시오.

* [JEE 배포에서 단일 서버 AEM Forms을 위한 시스템 요구 사항](https://www.adobe.com/go/learn_aemforms_sysreq_single_63)
* [JEE 배포에서 클러스터된 AEM Forms에 대한 시스템 요구 사항](https://www.adobe.com/go/learn_aemforms_sysreq_cluster_63)

## JEE에서 AEM Forms에 대해 지원되는 클라이언트 {#supported-clients-for-aem-forms-on-jee}

### Workbench {#workbench}

<table>
 <tbody>
  <tr>
   <th><p><strong>플랫폼</strong></p> </th>
   <th><p><strong>지원되는 패치 정의</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10(Enterprise, Pro, Basic)</p> <p>32비트 또는 64비트 버전</p> <p> </p> </td>
   <td>서비스 팩 및 중요 업데이트</td>
  </tr>
  <tr>
   <td>Microsoft® Windows® 2016 Server</td>
   <td>서비스 팩 및 중요 업데이트</td>
  </tr>
 </tbody>
</table>

* 설치 디스크 공간:Workbench 전용 1.7GB, Workbench, Designer 및 임시 설치 디렉토리의 경우 샘플 어셈블리 400MB(사용자 temp 디렉토리의 경우 200MB, Windows 임시 디렉토리의 경우 200MB) 이러한 모든 위치가 단일 드라이브에 있는 경우 설치 중에 1.5GB의 공간이 있어야 합니다. 설치가 완료되면 임시 디렉토리에 복사된 파일이 삭제됩니다.

* Workbench를 실행하는 메모리:2GB RAM
* 하드웨어 요구 사항:Intel® Pentium® 4 또는 AMD 동급 프로세서, 1GHz 프로세서
* 최소 1024 X 768픽셀 이상(16비트 색상 이상) 모니터 해상도
* JEE 서버의 AEM Forms에 대한 TCP/IPv4 또는 TCP/IPv6 네트워크 연결
* Windows에 Workbench를 설치하려면 관리 권한이 있어야 합니다. 관리자가 아닌 계정을 사용하여 설치하는 경우 설치 관리자에서 적절한 계정에 대한 자격 증명을 입력하라는 메시지를 표시합니다.

### 디자이너 {#designer}

* Microsoft® Windows® 2016 Server, Microsoft® Windows® 2019 Server 또는 Microsoft® Windows® 10
* PAE, NX 및 SSE2를 지원하는 1GHz 이상의 프로세서
* 64비트 OS용 32비트 또는 2GB RAM의 경우 1GB
* 32비트 또는 64비트 OS용 20GB 디스크 공간의 경우 16GB 디스크 공간
* 그래픽 메모리 - 128MB GPU(256MB 권장)
* 2.35GB의 사용 가능한 하드 디스크 공간
* 1024 X 768픽셀 이상의 모니터 해상도
* 비디오 하드웨어 가속(옵션)
* Acrobat Pro DC, Acrobat Standard DC 또는 Adobe Acrobat Reader DC.
* 디자이너를 설치할 관리 권한.

### Adobe Acrobat 및 Adobe Reader {#adobe-acrobat-and-adobe-reader}

<table>
 <tbody>
  <tr>
   <th><p><strong>Acrobat 및 Adobe Reader(기본)</strong></p> </th>
   <th><p><strong>지원되는 패치 정의</strong></p> </th>
  </tr>
  <tr>
   <td>Acrobat 2017(클래식 트랙)</td>
   <td>버전 17.011.30078 이상<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Acrobat DC 제품군에서는 기본적으로 다른 제품인 Acrobat과 Reader 모두에 대한 두 가지 트랙을 소개합니다.&quot;Classic&quot; 및 &quot;Continuous.&quot; 두 트랙에 대한 자세한 내용과 비교는 [https://www.adobe.com/go/acrobatdctracks.](https://www.adobe.com/go/acrobatdctracks)

### 브라우저 {#browsers}

#### 데스크톱 {#desktops}

<table>
 <tbody>
  <tr>
   <th><p><strong>브라우저(기본)</strong></p> </th>
   <th><p><strong>지원 수준</strong></p> </th>
   <th><p><strong>지원되는 패치 정의</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft Edge(에버그린)</p> </td>
   <td><p>A:지원됨</p> </td>
   <td><p>서비스 팩 및 업데이트</p> </td>
  </tr>
  <tr>
   <td><p>Mozilla Firefox(Evergreen)</p> </td>
   <td><p>A:지원됨</p> </td>
   <td>모든 업데이트</td>
  </tr>
  <tr>
   <td>Microsoft Firefox ESR</td>
   <td>E:작동해야 함</td>
   <td> 모든 업데이트</td>
  </tr>
  <tr>
   <td><p>Google Chrome(Evergreen)</p> </td>
   <td><p>A:지원됨</p> </td>
   <td>모든 업데이트</td>
  </tr>
  <tr>
   <td>MAC OS X의 Google Chrome 및 Firefox</td>
   <td>A:지원되는 <br /> <br /> </td>
   <td>모든 업데이트</td>
  </tr>
  <tr>
   <td>Apple Safari 11.x</td>
   <td>A:지원됨</td>
   <td>모든 업데이트</td>
  </tr>
  <tr>
   <td>Apple Safari 12.x<br /> <br /> </td>
   <td>A:지원됨</td>
   <td>모든 업데이트</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>데스크탑에 대한 일부 브라우저 관련 예외는 다음과 같습니다.
>
>* 대부분의 최신 브라우저는 더 이상 NPAPI 기반 플러그인을 지원하지 않습니다. AEM Forms 애플리케이션 및 워크플로우에 영향을 주는 방법에 대한 자세한 내용은 [NPAPI 브라우저 플러그인의 중단 및 그 영향](https://helpx.adobe.com/aem-forms/kb/discontinuation-of-npapi-plugins-impact-on-aem-forms.html)을 참조하십시오.
>* Safari는 Macintosh OS X에서만 지원됩니다.
>* Workspace는 Acrobat DC 이상 버전과 함께 Macintosh OS X 10.6 및 10.7에서 Safari 5.1을 지원합니다. Safari 5.1 Adobe Reader, Acrobat과의 호환성에 대한 자세한 내용은 [https://helpx.adobe.com/x-productkb/multi/safari-5-1-incompatible-reader.html](https://helpx.adobe.com/x-productkb/multi/safari-5-1-incompatible-reader.html)을 참조하십시오.
>* Safari에서는 관리 콘솔이 지원되지 않습니다.
>* 서신 관리는 AEM 6.1 Forms용 Windows® Internet Explorer 9.0을 지원하지 않습니다.
>* Forms 포털은 Internet Explorer 11에서 접근성을 위해 JAWS 14.0 화면 판독기 소프트웨어를 지원합니다.
>



#### 모바일 클라이언트 {#mobile-clients}

<table>
 <tbody>
  <tr>
   <th><p><strong>브라우저(기본)</strong></p> </th>
   <th><p><strong>지원되는 패치 정의</strong></p> </th>
  </tr>
  <tr>
   <td><p>Android™ 4.1.2 이상의 Chrome</p> </td>
   <td><p>모든 업데이트</p> </td>
  </tr>
  <tr>
   <td>iOS 11.0 이상의 Safari</td>
   <td>모든 업데이트</td>
  </tr>
  <tr>
   <td>Microsoft Edge<br /> </td>
   <td>모든 업데이트<br /> </td>
  </tr>
  <tr>
   <td>Android™ 4.4 이상의 기본 Android 브라우저</td>
   <td>모든 업데이트</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* Forms Portal은 iPad의 Safari에서만 지원됩니다.
>



### AEM Forms 앱 {#aem-forms-workspace-app}

#### 모바일 장치 지원 {#mobile-device-support}

AEM Forms 앱은 다음 플랫폼에서 사용할 수 있습니다.

| **플랫폼** | **지원되는 장치** |
|---|---|
| Apple iOS | iOS 12 이상을 실행하는 Apple iPhone, iPad, iPad Air, iPad mini. |
| Google Android | Android 5.1 이상. AEM Forms 앱은 7, 10인치 삼성 갤럭시 태블릿과 인기 스마트폰으로 인증됐다. |
| Microsoft Windows | Microsoft Windows 10 운영 체제를 실행하는 Microsoft Surface 장치, 태블릿, 노트북 및 데스크톱 |

### Adobe Flash Player {#adobe-flash-player}

<table>
 <tbody>
  <tr>
   <th><p><strong>Flash Player(기본)</strong></p> </th>
   <th><p><strong>지원되는 패치 정의</strong></p> </th>
  </tr>
  <tr>
   <td><p>최신 버전 Flash Player</p> </td>
   <td><p>부 버전 및 업데이트</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Adobe은 [2020년 말에 Flash Player 업데이트 및 배포를 중지합니다](https://theblog.adobe.com/adobe-flash-update/).

### Microsoft Office용 Adobe 문서 보안 확장 {#adobe-rights-management-extension-for-microsoft-office}

Microsoft® Office용 문서 보안 확장 Adobe에 대한 시스템 요구 사항을 보려면 [여기](https://www.adobe.com/products/livecycle/rightsmanagement/extension/downloads.html)를 클릭하십시오.

### 클라이언트 지원 예외 {#exceptions-to-client-support}

JEE의 AEM Forms은 지원되는 주요 버전 및 부 버전의 소프트웨어 위에 있는 업데이트, 패치 및 수정 팩을 지원합니다. 그러나 다음 주요 버전 또는 부 버전으로 업데이트는 명시하지 않는 한 지원되지 않습니다.

## 타사 패치 지원 정책 {#third-party-patch-support-policy}

JEE의 AEM Forms에 대한 타사 소프트웨어 요구 사항은 해당 제품 문서의 &quot;시스템 요구 사항&quot; 섹션에 설명되어 있습니다. 모든 설명서는 [https://adobe.com/go/learn_aemforms_documentation_65](https://adobe.com/go/learn_aemforms_documentation_65)에서 액세스할 수 있습니다.

JEE의 타사 참조 플랫폼에 있는 AEM Forms은 JEE에서 AEM Forms을 개발 및 릴리스하는 동안 최신 상태인 타사 인프라의 특정 패치 수준과 JEE에서 해당 버전의 AEM Forms에서 지원하는 인프라의 최소 패치/서비스 팩 수준에서 명시합니다.

Adobe은 타사 공급업체가 AEM Forms on JEE에서 지원하는 버전과의 이전 호환성을 보장한다고 가정할 경우, 해당 릴리스 시 타사 공급업체가 발행한 긴급 또는 권장 패치를 지원합니다. Adobe은 JEE 설명서의 AEM Forms에 명시된 최소 패치 수준 이후에 릴리스된 패치만 지원합니다.

경우에 따라 Adobe은 주요 기능을 변경하는 타사 업데이트를 지원하지 않으므로 전체 이전 버전과의 호환성을 지원하지 않습니다. 지원되는 업데이트에 대한 자세한 내용은 특정 공급업체 제품 및 패치 유형 Adobe이 지원하는 경우 [지원되는 패치 정의](https://helpx.adobe.com/aem-forms/aem-forms-third-party-software-patch.html)를 참조하십시오.

Adobe의 제어 이외의 상황에서 이전 버전과의 호환성을 주장하는 타사 패치는 Adobe 제품이나 고객 환경에 부정적인 영향을 줄 수 있습니다. 이러한 경우, Adobe은 고객이 중요한 시스템에 적용하기 전에 타사에서 제공한 긴급 패치가 미치는 영향을 평가할 것을 권장합니다. Adobe은 일반적인 Adobe 지원 프로그램을 통해 또는 제3자가 패치의 문제를 수정함으로써 이러한 문제를 해결하기 위한 합리적인 비즈니스 노력을 이용하여 타사와 협력합니다. 이는 Adobe에서 지원하는 새로 릴리스된 타사 패치가 공급업체가 설명한 대로 또는 JEE의 AEM Forms에서 작동하는 것을 보장하지 않습니다.

Adobe은 JEE 릴리스에서 AEM Forms이 지원하는 타사 참조 플랫폼 및 지원되는 패치 정의를 지정된 시점에서 변경할 수 있는 권한을 갖습니다.

타사 패치에 대한 추가 정보는 Adobe 엔터프라이즈 지원 사이트에서 제품과 관련된 기술 자료를 검색하여 찾을 수도 있습니다.

## 개정 내역 {#revision-history}

* 2020년 9월 9일
   * AEM Forms 앱용 iOS의 지원되는 버전을 iOS 12로 변경했습니다. 이전 버전은 iOS 11입니다.
