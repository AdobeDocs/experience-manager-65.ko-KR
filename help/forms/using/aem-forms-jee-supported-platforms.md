---
title: JEE에서 AEM Forms에 대해 지원되는 플랫폼
description: JEE에 AEM Forms을 설치하는 데 필요하고 지원되는 인프라 구성 요소 목록
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin
exl-id: 74d22cf4-56b2-48f5-92d9-928eaa134866
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '3691'
ht-degree: 1%

---


# JEE에서 AEM Forms에 대해 지원되는 플랫폼 {#supported-platforms-for-aem-forms-on-jee}

## 지원되는 플랫폼 {#supported-platforms}

<div class="preview">

Adobe이 [전체 설치 관리자](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 패치 설치 프로그램과 함께 JEE의 AEM 6.5 Forms 서비스 팩 18(6.5.18.0) 전체 설치 관리자는 새 플랫폼을 지원하며 패치 설치 관리자에는 버그 수정만 포함됩니다.
새로 설치하거나 JEE의 AEM 6.5 Forms Adobe 환경에 최신 소프트웨어를 사용할 계획이라면 다음을 사용하는 것이 좋습니다. [JEE의 AEM 6.5.18.0 Forms 전체 설치 관리자](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 2019년 4월 08일에 릴리스된 AEM 6.5 Forms 설치 관리자 또는 2022년 3월 03일에 릴리스된 AEM 6.5.12 Forms 설치 관리자 대신 2023년 8월 31일에 릴리스되었습니다.

</div>

### 지원 수준 {#support-levels}

AEM Forms on JEE 서버는 지원되는 운영 체제, 애플리케이션 서버, 데이터베이스, 데이터베이스 드라이버, JDK, LDAP 서버 및 이메일 서버의 조합을 사용하여 설정할 수 있습니다.

이 문서에서는 JEE에서 AEM Forms에 대해 지원되는 클라이언트 및 서버 플랫폼을 나열합니다. Adobe은 Adobe 권장 구성 및 기타 구성 모두에 대해 여러 수준의 지원을 제공합니다. 지원되는 다른 소프트웨어와 해당 버전, 예외, 패치 정의 및 타사 소프트웨어 패치 지원 정책 목록도 제공됩니다.

>[!NOTE]
>
>- 지원되는 서버 플랫폼에 대한 전체 예외 목록은 다음을 참조하십시오. [지원되는 서버 플랫폼에 대한 예외](../../forms/using/aem-forms-jee-supported-platforms.md#p-exceptions-to-supported-server-platforms-p).
>- AEM Forms on JEE는 지원되는 운영 체제 및 애플리케이션의 영어, 프랑스어, 독일어 및 일본어 버전만 지원합니다.

### 권장 구성 {#recommendedconfigurations}

Adobe은 이러한 구성을 권장하며 표준 소프트웨어 유지 관리 계약의 일부로 전체 또는 제한된 지원을 제공합니다.

<table>
 <tbody>
  <tr>
   <th>지원 수준</th>
   <th>설명</th>
  </tr>
  <tr>
   <td>A: 지원됨<br /> </td>
   <td>Adobe은 이 구성에 대한 전체 지원 및 유지 관리 기능을 제공합니다. 이 구성은 Adobe의 품질 보증 프로세스가 다룹니다.</td>
  </tr>
  <tr>
   <td>R: 제한된 지원</td>
   <td>Adobe은 특정 전제 조건이 충족되면 이 구성을 완벽하게 지원합니다. 사전 요구 사항에 대해 알아보고 지원 요청을 제기하려면 Adobe 엔터프라이즈 지원에 문의하십시오.</td>
  </tr>
  <tr>
   <td>L: 제한된 지원</td>
   <td>Adobe은 특정 전제 조건이 충족된 후에 이 구성에 대한 전체 지원 및 유지 관리를 제공합니다. 일부 기능은 구성에서 사용할 수 없습니다. 사전 요구 사항에 대해 알아보고 지원 요청을 제기하려면 Adobe 엔터프라이즈 지원에 문의하십시오.<br /> </td>
  </tr>
 </tbody>
</table>

### 지원되지 않는 구성 {#unsupported-configurations}

| 지원 수준 | 설명 |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| E: 작동 예정 | 구성이 작동할 것으로 예상되며, 반대의 보고서는 없습니다. |
| Z: 지원되지 않음 | 구성이 지원되지 않습니다. Adobe은 구성의 작동 여부에 대해 설명하지 않으며 이를 지원하지 않습니다. |

>[!NOTE]
>
>AEM Forms 고객이 소유 비용을 절감하고, 배포 아키텍처를 단순화하고, 개발 스택을 현대화할 수 있도록 Adobe Experience Manager 엔터프라이즈 플랫폼은 독립형 OSGi 기반 배포를 위해 애플리케이션 서버 기반 배포에서 탈피하고 있습니다. Adobe은 인프라 구성 요소 매트릭스가 축소된 AEM Forms JEE 스택을 계속 지원합니다.
>
>6.5 릴리스에서는 다음과 같이 Adobe 고객 중 사용률이 가장 낮은 인프라 구성 요소가 더 이상 지원되지 않습니다.
>
>- IBM® DB2® 데이터베이스
- IBM® AIX® 및 Sun Solaris™ 운영 체제
>
새 설치의 경우, 가능한 경우 양식 데이터 모델을 사용한 모바일, 다중 채널 대화형 통신 및 백엔드 데이터 통합용 응답형 Forms에 대한 최신 혁신 기능을 사용하도록 최신 OSGi 스택에 AEM Forms을 배포하는 것이 좋습니다.
>
Adobe은 기존 사용자가 JEE 스택에 AEM Forms을 계속 배포해야 함을 인식합니다. 이러한 시나리오에서 Adobe은 이 설명서에 설명된 대로 지원되는 인프라에 AEM Forms JEE를 배포해야 합니다. AEM 6.5 Forms으로 업그레이드하고 이전 AEM Forms 릴리스에서 지원되지 않는 플랫폼을 사용하는 경우 Adobe 지원 팀에 문의하여 지원되는 플랫폼으로 업그레이드하는 데 도움을 받을 수 있습니다.

### Java™ 가상 시스템(JVM) {#java-virtual-machines-jvm}

Adobe Experience Manager Forms을 실행하려면 Java™ Virtual Machine이 필요하며, 이 시스템은 JDK(Java™ Development Kit) 배포에서 제공합니다. Adobe Experience Manager은 다음 버전의 Java™ 가상 시스템과 함께 작동합니다.

<table>
 <tbody>
  <tr>
   <th><p><strong>Platform</strong></p> </th>
   <th><p><strong>지원 수준</strong></p> </th>
   <th><p><strong>지원되는 패치 정의</strong></p> </th>
  </tr>
  <tr> 
   <td><p>Oracle Java™ SE 11(64비트) <sup> [8] </sup> </p>  </td>
   <td><p>A: 지원됨</p> </td>
   <td><p>마이너 릴리스 및 업데이트 </p> </td>
  </tr>
  <tr>
   <td>Azul Zulu OpenJDK 11 - 64비트</td>
   <td>Z: 지원되지 않음</td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td>Azul Zulu OpenJDK 8 - 64비트</td>
   <td>Z: 지원되지 않음</td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td>Oracle Java™ SE 8(64비트)</td>
   <td>A: 지원됨</td>
   <td>마이너 릴리스 및 업데이트</td>
  </tr>
  <tr>
   <td>IBM® J9 가상 시스템(빌드 2.9, JRE 1.8.0) IBM® JDK SR6-FP26<br /> </td>
   <td>A: 지원됨</td>
   <td>마이너 릴리스 및 업데이트</td>
  </tr>
  <tr>
   <td>IBM® JAVA1.8.0_291(빌드 8.0.6.30)<br /> </td>
   <td>A: 지원됨</td>
   <td>마이너 릴리스 및 업데이트</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
- Java™ 공급업체의 보안 게시판을 추적하여 프로덕션 환경의 안전과 보안을 보장하고 최신 Java™ 업데이트를 설치합니다.
- JEE의 AEM Forms은 프로덕션 환경에서 64비트 JVM만 지원합니다.

### 데이터베이스 및 CRX 지속성 {#databases-and-crx-persistence}

<table>
 <tbody>
  <tr>
   <td><p><strong>Platform</strong></p> </td>
   <td><p><strong> 설명</strong></p> </td>
   <td><p><strong>지원 수준</strong></p> </td>
  </tr>
  <tr>
   <td><p>파일 시스템</p> </td>
   <td><p>저장소 마이크로커널(TAR MK 파일)</p> </td>
   <td><p>지원됨</p> </td>
  </tr>
  <tr>
   <td><p> MongoDB Enterprise 4.4 </p> </td>
   <td><p>저장소 마이크로커널</p> </td>
   <td><p>지원됨</p> </td>
  </tr>
   <tr>
   <td>Oracle 데이터베이스 19c(Standard, RAC(Real Application Clusters) 및 Enterprise Edition) </td>
   <td>저장소 마이크로커널 </td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td><p>저장소 마이크로커널</p> </td>
   <td><p>지원됨</p> </td>
  </tr>
  <tr>
   <td><p>Microsoft® SQL Server 2019 </p> </td>
   <td><p>저장소 마이크로커널</p> </td>
   <td><p>지원됨</p> </td>
  </tr>
  <tr>
   <td>IBM® DB2® 11.1(더 이상 사용되지 않음)</td>
   <td>저장소 마이크로커널</td>
   <td>R: 제한된 지원</td>
  </tr>
  <tr>
  <tr>
   <td>MySQL 8.0.27</td>
   <td>-</td>
   <td>R: 제한된 지원</td>
  </tr>
 </tbody>
</table>

- IBM® DB2®는 새로 설치하는 경우 지원되지 않습니다. AEM 6.5 Forms으로 업그레이드하는 기존 고객에게만 지원됩니다.
- MongoDB는 타사 소프트웨어이며 AEM 라이선스 패키지에 포함되어 있지 않습니다. 자세한 내용은 [MongoDB 라이선스 정책](https://www.mongodb.org/about/licensing/).
- AEM Adobe 배포를 최대한 활용하려면 MongoDB Enterprise 버전에 라이센스를 부여하여 전문적인 지원을 받는 것이 좋습니다.
- Adobe 고객 지원 센터는 AEM에서 MongoDB 사용과 관련된 자격 부여 문제를 지원합니다. 자세한 내용은 [Adobe Experience Manager MongoDB 페이지](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager).
- &#39;파일 시스템&#39;에는 POSIX와 호환되는 블록 저장소가 포함되어 있습니다. 여기에는 네트워크 스토리지 기술이 포함됩니다. 파일 시스템 성능이 달라질 수 있으며 전체 성능에 영향을 줄 수 있습니다. 네트워크/원격 파일 시스템으로 테스트 AEM을 로드하는 것이 좋습니다.
- MongoDB 스토리지 엔진 WiredTiger만 지원됩니다.
- MongoDB 분할은 AEM에서 지원되지 않습니다.
- JEE의 AEM Forms은 RDBMK 지속성을 위한 MySQL을 지원하지 않습니다.
- Document Security 모듈은 콘텐츠 저장소를 사용하지 않습니다. 이는 Document Security만 사용하고 있고 HTML Workspace, HTML 5 양식 또는 적응형 양식을 사용할 계획이 없는 경우 컨텐츠 저장소를 설치하지 말라는 의미입니다.
- JEE의 AEM Forms은 AEM 저장소(CRX-Repository)를 지속하는 데 MySQL을 사용하는 것을 지원하지 않습니다.

### 데이터베이스 드라이버 {#database-drivers}

<table>
 <tbody>
  <tr>
   <th>데이터베이스 </th>
   <th><p><strong>Platform</strong></p> </th>
   <th><p><strong>지원되는 패치 정의</strong></p> </th>
  </tr>
  <tr>
   <td>MySQL</td>
   <td><p>MySQL 커넥터/J 5.7</p> <p>mysql-connector-java-5.1.44-bin.jar(버전 5.1.44)</p> </td>
   <td><p>JEE 설치 시 AEM Forms 제공</p> </td>
  </tr>
  <tr>
   <td>Microsoft® SQL Server<br /> </td>
   <td><p>Microsoft® SQL Server JDBC 드라이버 8.2.2<br /> </p> <p>sqljdbc8.jar</p> </td>
   <td><p>Microsoft® 웹 사이트에서 다운로드합니다.</p> </td>
  </tr>
  <tr>
   <td>Oracle</td>
   <td><p>Oracle 데이터베이스 19.3.0.0.0 JDBC 드라이버</p> <p>ojdbc8.jar(버전 19.3.0.0.0)<br /> </p> </td>
   <td><p>다음에서 다운로드 <a href="https://www.oracle.com/database/technologies/appdev/jdbc-ucp-19c-downloads.html">웹 사이트 oracle</a>.</p> </td>
  </tr>
 </tbody>
</table>

### 애플리케이션 서버 {#application-servers}

<table>
 <tbody>
  <tr>
   <td><p><strong> Platform</strong></p> </td>
   <td><p><strong>지원 수준</strong></p> </td>
   <td><p><strong>지원되는 패치 정의</strong></p> </td>
  </tr>
  <tr>
   <td>Oracle WebLogic Server 12.2.1(12c R2)(더 이상 사용되지 않음)</td>
   <td>A: 지원됨</td>
   <td>서비스 팩 및 주요 업데이트</td>
  </tr>
  <tr>
   <td>Oracle WebLogic Server 14c </td>
   <td>A: 지원됨</td>
   <td>서비스 팩 및 주요 업데이트</td>
  </tr>
  <tr>
   <td>IBM® WebSphere® Application Server 9.0.0.10 <sup>[1] [4]</sup><br /> </td>
   <td>A: 지원됨</td>
   <td>서비스 팩 및 주요 업데이트</td>
  </tr>
  <tr>
   <td><p>JBoss® EAP(Enterprise Application Platform) 7.4 <sup>[2] [3] [7]</sup> </p> </td>
   <td><p>A: 지원됨</p> </td>
   <td><p>지원되는 EAP 버전에 대한 패치 및 누적 패치</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
IBM® WebSphere® 클러스터는 Network Deployment Edition에서만 지원됩니다.

### 서버 운영 체제 {#server-operating-systems}

#### 프로덕션 환경 {#production-environments}

<table>
 <tbody>
  <tr>
   <th><p><strong> Platform</strong></p> </th>
   <th><p><strong>지원 수준</strong></p> </th>
   <th><p><strong>지원되는 패치 정의</strong></p> </th>
  </tr>
   <tr>
   <td>Microsoft® Windows Server 2019(64비트)(더 이상 사용되지 않음)</td>
   <td>A: 지원됨</td>
   <td>서비스 팩 및 주요 업데이트</td>
  </tr>
     <tr>
   <td>Microsoft® Windows Server 2022(64비트)</td>
   <td>A: 지원됨</td>
   <td>서비스 팩 및 주요 업데이트</td>
  </tr>
  <tr>
   <td>Ubuntu 20.04</td>
   <td>A: 지원됨</td>
   <td>서비스 팩 및 주요 업데이트</td>
  </tr>
  <tr>
   <td><p>Red Hat® Enterprise Linux® 8(커널 4.x)(64비트)</p> </td>
   <td><p>A: 지원됨</p> </td>
   <td><p>마이너 릴리스, 누적 업데이트 및 중요 업데이트</p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® Enterprise Linux® 7(커널 3.x)(64비트)(더 이상 사용되지 않음)</td>
   <td><p>A: 지원됨</p> </td>
   <td><p>마이너 릴리스, 누적 업데이트 및 중요 업데이트</p> </td>
  </tr>
  <tr>
   <td><p>SUSE® Linux® Enterprise Server 12(64비트)</p> </td>
   <td><p>A: 지원됨</p> </td>
   <td><p>서비스 팩, 누적 패치 및 중요 보안 업데이트</p> </td>
  </tr>
  <tr>
   <td>Oracle Linux® 7 업데이트 3(64비트)</td>
   <td>A: 지원됨</td>
   <td>서비스 팩, 누적 패치 및 중요 보안 업데이트</td>
  </tr>
  <tr>
   <td>CentOS 7(64비트)<sup> [6]</sup></td>
   <td>A: 지원됨</td>
   <td>서비스 팩, 누적 패치 및 중요 보안 업데이트</td>
  </tr>
 </tbody>
</table>

#### 가상화 환경 {#virtualized-environment}

물리적 컴퓨터 또는 가상 환경에서 JEE에서 AEM Forms을 실행할 수 있습니다. 그러나 가상 환경에서 AEM Forms에 문제가 발생하면 물리적 컴퓨터에서 문제를 복제해 보십시오. 물리적 시스템에서 문제가 지속되면 Adobe 지원 센터에 문의하여 해결 방법을 확인하십시오. 물리적 시스템에서 복제할 수 없는 문제는 가상 환경 공급업체에 문의하십시오.

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
   <td>E: 작동 예정</td>
   <td><p>서비스 팩 및 주요 업데이트</p> </td>
  </tr>
 </tbody>
</table>

### 지원되는 서버 플랫폼에 대한 예외 {#exceptions-to-supported-server-platforms}

JEE 서버에서 AEM Forms을 설정할 플랫폼을 선택할 때 다음 예외를 고려하십시오.

1. JEE의 AEM Forms은 MySQL과 함께 IBM® WebSphere®를 지원하지 않습니다.
1. JEE의 AEM Forms은 SUSE® Linux® Enterprise Server 12의 JBoss®를 지원하지 않습니다. IBM® WebSphere®만 SUSE® Linux® Enterprise Server 12에서 지원됩니다.
1. JEE의 AEM Forms은 Oracle Java™ SE 이외의 JBoss®와 함께 JDK를 지원하지 않습니다.
1. JEE의 AEM Forms은 IBM® JDK를 제외한 IBM® WebSphere®의 JDK를 지원하지 않습니다.
1. CRX-repository는 TarMK, MongoDB 및 RDBMK(관계형 데이터베이스) 유형의 지속성을 지원합니다. 애플리케이션 서버와 CRX-repository 간에 두 개의 서로 다른 데이터베이스 시스템을 사용할 수 없습니다. 그러나 JEE의 AEM Forms 환경에서는 CRX-repository와 함께 MongoMK를 사용하고 애플리케이션 서버와 함께 지원되는 관계형 데이터베이스를 사용할 수 있습니다.
1. JEE의 AEM Forms은 CentOS에서 WebSphere® 애플리케이션 서버를 지원하지 않습니다.
1. JEE의 AEM Forms은 JBoss® RBAC(역할 기반 액세스 제어)를 지원하지 않습니다.
1. AEM Forms on JEE는 애플리케이션 서버 JBoss™ EAP 7.4에만 해당하는 Oracle Java® SE 11(64비트) SDK를 지원합니다.

또한 JEE 배포에서 AEM Forms Adobe 소프트웨어를 선택할 때 다음 사항을 고려하십시오.

- AEM Forms on JEE는 지원되는 소프트웨어의 지정된 주 버전 및 부 버전 위에 업데이트, 패치 및 수정 팩을 지원합니다. 그러나 지정하지 않는 한 다음 주 버전 또는 부 버전으로의 업데이트는 지원되지 않습니다.
- 클러스터 기반 설치는 TarMK 지속성을 지원하지 않습니다. 지원되는 지속성에 대한 자세한 내용은 [AEM Forms 설치를 위한 지속성 유형 선택](/help/forms/using/choosing-persistence-type-for-aem-forms.md).
- AEM Forms on JEE는 Adobe에 따라 다양한 타사 소프트웨어를 지원합니다. [타사 소프트웨어 지원 정책](../../forms/using/aem-forms-jee-supported-platforms.md#p-third-party-patch-support-policy-p).
- 타사 공급업체에서 제공한 지원에 따라 JEE의 AEM Forms 지원 플랫폼입니다. 일부 조합은 서드파티 공급업체에서 허용하지 않을 수 있습니다. 예를 들어, 많은 공급업체가 Oracle으로 애플리케이션 서버를 인증하지 않았습니다. 따라서 JEE의 AEM Forms 또한 이러한 조합을 지원하지 않습니다. 지원되는 소프트웨어 버전을 선택하려면 서드파티 공급업체의 지원 매트릭스도 확인하십시오.
- JEE의 AEM Forms은 TarMK 콜드 대기를 지원하지 않습니다.
- JEE의 AEM Forms은 수직 클러스터링을 지원하지 않습니다.
- AEM Forms on JEE는 클러스터된 환경에서 MySQL 데이터베이스를 지원하지 않습니다.
- 제거되거나 업데이트된 플랫폼 목록은 다음을 참조하십시오. [AEM 6.5 Forms의 새로운 기능 요약](../../forms/using/whats-new.md) 문서.

### LDAP 서버(선택 사항) {#ldap-servers-optional}

<table>
 <tbody>
  <tr>
   <th><p><strong>제품(기본 버전)</strong></p> </th>
   <th><p><strong>지원되는 패치 정의</strong></p> </th>
  </tr>
  <tr>
   <td>Microsoft® Active Directory 2016(더 이상 사용되지 않음)</td>
   <td>유지 관리 릴리스 및 수정 팩</td>
  </tr>
  <tr>
   <td>Microsoft® Active Directory 2022</td>
   <td>유지 관리 릴리스 및 수정 팩</td>
  </tr>
  <tr>
   <td><p>IBM® Tivoli Directory Server 6.4</p> </td>
   <td><p>기능 팩 및 임시 수정 사항</p> </td>
  </tr>
 </tbody>
</table>

### 이메일 서버(선택 사항) {#email-servers-optional}

| 제품 |
| ----------------------- |
| Microsoft® Exchange 2013 |
| Microsoft® Office 365 |

### 콘텐츠 관리자 및 해당 커넥터 {#content-managers-and-corresponding-connectors}

<table>
 <tbody>
  <tr>
   <td><strong>제품<br /> </strong></td>
   <td><strong>버전</strong></td>
  </tr>
  <tr>
   <td>EMC Documentum®</td>
   <td>7.3</td>
  </tr>
  <tr>
   <td>IBM® 파일</td>
   <td>5.5.2</td>
  </tr>
  <tr>
   <td>IBM® Content Manager Server(더 이상 사용되지 않음) </td>
   <td>8.5 수정 팩 2</td>
  </tr>
  <tr>
   <td> IBM® Content Manager 클라이언트(더 이상 사용되지 않음)</td>
   <td>8.5 </td>
  </tr>
   <td>Microsoft® Sharepoint </td>
   <td>2019<br /> </td>
  </tr>
 </tbody>
</table>

### Cordova 지원 {#support-for-cordova}

AEM Forms 앱은 이제 Apache Cordova를 지원합니다. 지원되는 Cordova의 플랫폼별 버전은 다음과 같습니다.

- Apache Cordova 6.4.0
- Cordova iOS 4.3.0
- Cordova Android™ 6.0.0
- Cordova 윈도우 4.4.3

### PDF Generator 소프트웨어 지원 {#software-support-for-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>제품</strong></p> </th>
   <th><p><strong>PDF 전환에 지원되는 형식</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2020 클래식 트랙</a> 최신 버전</td>
   <td>XPS, 이미지 형식(BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, DWG, DXF 및 DWF</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2019</td>
   <td>DOC, DOCX, XLS, XLSX, PPT, PPTX, RTF 및 TXT</td>
  </tr>
  <tr>
   <td>워드퍼펙트 2020<br /> </td>
   <td>WP, WPD</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2019<br /> </td>
   <td>PUB</td>
  </tr>
  <tr>
   <td>오픈오피스 4.1.10</td>
   <td>ODT, ODP, ODS, ODG, ODF, SXW, SXI, SXC, SXD, XLS, XLSX, DOC, DOCX, PPT, PPTX, 이미지 형식(BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, RTF, TXT</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
PDF Generator은 지원되는 운영 체제 및 애플리케이션의 영어, 프랑스어, 독일어 및 일본어 버전만 지원합니다.
>
또한,
>
- PDF Generator에 32비트 버전 필요 [Acrobat 2020 classic track 버전 20.004.30006](https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html) 변환 수행.
- PDF Generator은 Microsoft® Office Professional Plus 및 변환에 필요한 기타 소프트웨어의 32비트 소매 버전만 지원합니다.
- PDF Generator은 Microsoft® Office 365를 지원하지 않습니다.
- OpenOffice의 PDF Generator 전환은 Windows 및 Linux®에서만 지원됩니다.
- OCR PDF, Optimize PDF 및 Export PDF 기능은 Windows에서만 지원됩니다.
- Acrobat 버전은 PDF Generator 기능을 사용할 수 있도록 AEM Forms과 번들로 제공됩니다. 번들형 버전은 AEM Forms 라이선스가 있는 동안 AEM Forms PDF Generator과 함께 사용하기 위해 AEM Forms을 통해서만 프로그래밍 방식으로 액세스해야 합니다. 자세한 내용은 배포에 따른 AEM Forms 제품 설명([On-Premise](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html) 또는 [Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html))&quot;
- PDF Generator 서비스는 Microsoft® Windows 10을 지원하지 않습니다.
-PDF Generator이 Microsoft® Visio 2019를 사용하여 파일을 변환하지 못합니다. Microsoft® Visio 2016을 계속 사용하여 .VSD 및 .VSDX 파일을 변환할 수 있습니다.
- PDF Generator이 Microsoft® Project 2019를 사용하여 파일을 변환하지 못했습니다. Microsoft® Project 2016을 계속 사용하여 .MPP 파일을 변환할 수 있습니다.
- PDF Generator이 Microsoft® Visio 2019를 사용하여 파일을 변환하지 못했습니다.
- PDF Generator이 Microsoft® Project 2019를 사용하여 파일을 변환하지 못했습니다.
>

### 접근성 지원에 대한 예외 {#exceptions-to-accessibility-support}

AEM Forms의 다음 하위 시스템은 [508](https://www.section508.gov/) 준수:

- 적응형 Forms 작성 UI
- Forms Manager 작성 UI
- 서신 관리 작성 UI
- 관리 UI(관리 콘솔 UI)

## JEE의 AEM Forms에 대한 시스템 요구 사항 {#system-requirements-for-aem-forms-on-jee}

### 최소 하드웨어 요구 사항 {#minimum-hardware-requirements}

<table>
 <tbody>
  <tr>
   <td>Platform</td>
   <td>최소 하드웨어 요구 사항</td>
  </tr>
  <tr>
   <td>Microsoft® Windows Server</td>
   <td>Intel Xeon® E5-2680, 2.4GHz 프로세서 또는 동급 제품<br /> VMWare ESX 5.1 이상<br /> RAM: 6GB(64비트 JVM 포함 64비트 OS)<br /> 사용 가능한 디스크 공간: 15GB의 임시 공간 + 22GB<br /> JEE의 AEM Forms</td>
  </tr>
  <tr>
   <td>SUSE® Linux® 엔터프라이즈 서버</td>
   <td>Intel Xeon® E5-2670v2, vCPU 1개, 2.5GHz 프로세서<br /> AWS m3.medium(3개의 ECU)<br /> RAM: 6GB(64비트 JVM 포함 64비트 OS)<br /> 사용 가능한 디스크 공간: 6GB의 임시 공간 + 22GB<br /> JEE의 AEM Forms</td>
  </tr>
  <tr>
   <td>Red Hat® Enterprise Linux®</td>
   <td>Intel Xeon® E5-2670v2, vCPU 1개, 2.5GHz 프로세서<br /> AWS m3.medium(3개의 ECU)<br /> RAM: 6GB(64비트 JVM 포함 64비트 OS)<br /> 사용 가능한 디스크 공간: 6GB의 임시 공간 + 22GB<br /> JEE의 AEM Forms<br /> </td>
  </tr>
  <tr>
   <td>소규모 운영 환경에 필요한 하드웨어 요구 사항</td>
   <td>
    <ul>
     <li><strong>인텔® 기반 환경</strong>: Intel Xeon® E5-2680, 2.4GHz 이상 듀얼 코어 프로세서를 사용하면 성능이 더욱 향상됩니다.</li>
     <li><strong>메모리: </strong>4GB <br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

추가 요구 사항은 다음을 참조하십시오.

- [JEE의 단일 서버 AEM Forms 배포에 대한 시스템 요구 사항](https://www.adobe.com/go/learn_aemforms_sysreq_single_65)
- [JEE 배포의 클러스터된 AEM Forms에 대한 시스템 요구 사항](https://www.adobe.com/go/learn_aemforms_sysreq_cluster_65)

## JEE에서 AEM Forms에 대해 지원되는 클라이언트 {#supported-clients-for-aem-forms-on-jee}

### Workbench {#workbench}

<table>
 <tbody>
  <tr>
   <th><p><strong>Platform</strong></p> </th>
   <th><p><strong>지원되는 패치 정의</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10(Enterprise, Pro, Basic)</p> <p>32비트 또는 64비트 버전</p> <p> </p> </td>
   <td>서비스 팩 및 주요 업데이트</td>
  </tr>
  <tr>
   <td>Microsoft® Windows® 2019 Server(더 이상 사용되지 않음)</td>
   <td>서비스 팩 및 주요 업데이트</td>
  </tr>
  <tr>
   <td>Microsoft® Windows® 2022 Server</td>
   <td>서비스 팩 및 주요 업데이트</td>
  </tr>
 </tbody>
</table>

- 설치할 디스크 공간: Workbench에만 1.7GB, Workbench, Designer의 전체 설치를 위해 단일 드라이브에 2.7GB, 임시 설치 디렉터리의 샘플 어셈블리 400MB - 사용자 임시 디렉터리의 경우 200MB, Windows 임시 디렉터리의 경우 200MB. 이러한 위치가 모두 단일 드라이브에 있는 경우 설치하는 동안 사용할 수 있는 공간이 1.5GB여야 합니다. 임시 디렉토리에 복사된 파일은 설치가 완료되면 삭제됩니다.

- Workbench를 실행하기 위한 메모리: 2GB RAM
- 하드웨어 요구 사항: Intel® Pentium® 4 또는 AMD® 동급, 1GHz 프로세서
- 최소 1024X768픽셀 이상의 모니터 해상도(16비트 색상 이상)
- JEE 서버의 AEM Forms에 대한 TCP/IPv4 또는 TCP/IPv6 네트워크 연결
- Windows에 Workbench를 설치하려면 관리 권한이 있어야 합니다. 관리자가 아닌 계정을 사용하여 설치하는 경우 설치 프로그램에서 적절한 계정에 대한 자격 증명을 입력하라는 메시지가 표시됩니다.

### 디자이너 {#designer}

- Microsoft® Windows® 2016 Server, Microsoft® Windows® 2019 Server 또는 Microsoft® Windows® 10
- PAE, NX 및 SSE2를 지원하는 1GHz 이상의 프로세서
- 32비트용 RAM 1GB 또는 64비트 OS용 RAM 2GB
- 32비트용 16GB 디스크 공간 또는 64비트 OS용 20GB 디스크 공간
- 그래픽 메모리 - 128MB GPU(256MB 권장)
- 2.35GB의 사용 가능한 하드 디스크 공간
- 1024 X 768 픽셀 이상의 모니터 해상도
- 비디오 하드웨어 가속(옵션)
- Acrobat Pro DC, Acrobat Standard DC 또는 Adobe Acrobat Reader DC
- Designer를 설치할 수 있는 관리 권한
- Microsoft® Visual C++ 2019(VC 14.28 이상) 32비트 런타임

### Adobe Acrobat 및 Adobe Reader {#adobe-acrobat-and-adobe-reader}

<table>
 <tbody>
  <tr>
   <th><p><strong>Acrobat 및 Adobe Reader(기본)</strong></p> </th>
   <th><p><strong>지원되는 패치 정의</strong></p> </th>
  </tr>
  <tr>
   <td>Acrobat 2020 (클래식 트랙)</td>
   <td>버전 20.004.30006 이상<br /> </td>
  </tr>

</tbody>
</table>

>[!NOTE]
>
Acrobat DC 제품군에서는 &quot;클래식&quot;과 &quot;연속&quot;이라는 서로 다른 제품인 Acrobat과 Reader에 대한 두 가지 트랙을 도입했습니다. 두 트랙에 대한 자세한 내용 및 비교는 를 참조하십시오. [https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/whatsnewdc.html](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/whatsnewdc.html).

### 브라우저 {#browsers}

#### 데스크탑 {#desktops}

<table>
 <tbody>
  <tr>
   <th><p><strong>브라우저(기본)</strong></p> </th>
   <th><p><strong>지원 수준</strong></p> </th>
   <th><p><strong>지원되는 패치 정의</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Edge (Evergreen)</p> </td>
   <td><p>A: 지원됨</p> </td>
   <td><p>서비스 팩 및 업데이트</p> </td>
  </tr>
  <tr>
   <td><p>Mozilla Firefox (Evergreen)</p> </td>
   <td><p>A: 지원됨</p> </td>
   <td>모든 업데이트</td>
  </tr>
  <tr>
   <td>Mozilla Firefox ESR</td>
   <td>E: 작동 예정</td>
   <td> 모든 업데이트</td>
  </tr>
  <tr>
   <td><p>Google Chrome(Evergreen)</p> </td>
   <td><p>A: 지원됨</p> </td>
   <td>모든 업데이트</td>
  </tr>
  <tr>
   <td>macOS의 Apple Safari</td>
   <td>A: 지원됨</td>
   <td>모든 업데이트</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
데스크탑에 대한 일부 브라우저 관련 예외는 다음과 같습니다.
>
- Safari는 Macintosh OS X에서만 지원됩니다.
- 작업 영역은 Acrobat DC 이상 버전의 Macintosh OS X 10.6 및 10.7에서 Safari 5.1을 지원합니다. Adobe Reader, Acrobat과의 Safari 5.1 호환성에 대한 자세한 내용은 [https://helpx.adobe.com/x-productkb/multi/safari-5-1-incompatible-reader.html](https://helpx.adobe.com/x-productkb/multi/safari-5-1-incompatible-reader.html).
- 관리 콘솔은 Safari에서 지원되지 않습니다.
- 서신 관리는 AEM 6.1 forms용 Windows® Internet Explorer 9.0을 지원하지 않습니다.
- Forms 포털은 접근성을 위해 Internet Explorer 11에서 JAWS 14.0 화면 판독기 소프트웨어를 지원합니다.

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
   <td>iOS 15.1 이상 버전의 Safari</td>
   <td>모든 업데이트</td>
  </tr>
  <tr>
   <td>Microsoft® Edge<br /> </td>
   <td>모든 업데이트<br /> </td>
  </tr>
  <tr>
   <td>Android™ 4.4 이상 버전의 기본 Android™ 브라우저</td>
   <td>모든 업데이트</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
- Forms 포털은 iPad의 Safari에서만 지원됩니다.

### AEM Forms 앱 {#aem-forms-workspace-app}

#### 모바일 장치 지원 {#mobile-device-support}

AEM Forms 앱은 다음 플랫폼에서 사용할 수 있습니다.

| **Platform** | **지원되는 장치** |
| ----------------- | ------------------------------------------------------------------------------------------------------------------- |
| Apple iOS | Apple iPhone, iPad, iPad Air 및 iPad mini(iOS 15.1 이상 실행) |
| Google Android™ | Android™ 5.1 이상. AEM Forms 앱은 7인치 및 10인치 삼성 갤럭시 태블릿과 인기 있는 스마트폰에서 인증을 받았습니다. |
| Microsoft® Windows | Microsoft® Microsoft® Windows 10 운영 체제를 실행하는 표면 장치, 태블릿, 노트북 및 데스크탑 |

### Microsoft® Office용 Adobe 문서 보안 확장 {#adobe-rights-management-extension-for-microsoft-office}

클릭 [여기](https://www.adobe.com/products/livecycle/rightsmanagement/extension/downloads.html) Microsoft® Office용 Adobe Document Security Extension에 대한 시스템 요구 사항을 보려면 다음을 수행하십시오.

### 클라이언트 지원에 대한 예외 {#exceptions-to-client-support}

AEM Forms on JEE는 지원되는 소프트웨어의 지정된 주 버전 및 부 버전 위에 업데이트, 패치 및 수정 팩을 지원합니다. 그러나 지정하지 않는 한 다음 주 버전 또는 부 버전으로의 업데이트는 지원되지 않습니다.

## 타사 패치 지원 정책 {#third-party-patch-support-policy}

AEM Forms on JEE에 대한 타사 소프트웨어 요구 사항은 해당 제품 문서의 &quot;시스템 요구 사항&quot; 섹션에 설명되어 있습니다. 에서 모든 설명서에 액세스 [https://adobe.com/go/learn_aemforms_documentation_65](https://adobe.com/go/learn_aemforms_documentation_65) .

JEE의 서드파티 참조 플랫폼인 AEM Forms은 JEE의 AEM Forms을 개발 및 릴리스하는 동안 현재 존재하는 서드파티 인프라의 특정 패치 수준과 JEE의 해당 버전의 AEM Forms에서 지원하는 인프라의 최소 패치/서비스 팩 수준을 설명합니다.

Adobe은 타사 공급업체가 JEE의 AEM Forms이 지원하는 버전과의 이전 버전과의 호환성을 보장한다고 가정하고 출시 시 타사 공급업체에서 발급하는 긴급 패치 또는 권장 패치를 지원합니다. Adobe은 AEM Forms on JEE 설명서에 명시된 최소 패치 수준 이후에 릴리스된 패치만 지원합니다.

경우에 따라 Adobe은 주요 기능을 변경하는 서드파티 업데이트를 지원하지 않으므로 전체 이전 버전과의 호환성을 지원하지 않습니다. 지원되는 업데이트에 대한 자세한 내용은 다음을 참조하십시오. [지원되는 패치 정의](https://helpx.adobe.com/aem-forms/aem-forms-third-party-software-patch.html) 특정 공급업체 제품 및 패치 유형 Adobe이 지원하는 경우

Adobe이 통제할 수 없는 상황에서 이전 버전과의 호환성을 주장하는 타사 패치는 Adobe 제품이나 고객 환경에 부정적인 영향을 미칠 수 있습니다. 이러한 경우, Adobe은 중요한 시스템에 적용하기 전에 제3자의 긴급 패치가 미치는 영향을 평가하도록 권장합니다. Adobe은 일반적인 Adobe 지원 프로그램을 통해 또는 제3자가 해당 패치의 문제를 수정하여 이러한 문제를 해결하기 위해 합리적인 비즈니스 노력을 사용하여 제3자와 협력합니다. 이는 Adobe이 지원할 새로 릴리스된 타사 패치가 공급업체나 JEE의 AEM Forms에서 문서화한 대로 작동함을 보장하지 않습니다.

Adobe은 JEE 릴리스의 AEM Forms에서 지원하는 타사 참조 플랫폼과 해당 시점에 지원되는 패치 정의를 변경할 수 있는 권한을 보유합니다.

타사 패치에 대한 추가 정보는 Adobe 엔터프라이즈 지원 사이트에서 제품과 관련된 기술 문서를 검색하여 찾을 수도 있습니다.

## 플랫폼 업데이트 {#platform-updates}

다음 플랫폼은 2023년 8월 31일에 AEM Forms 6.5.18.0 릴리스에서 더 이상 사용되지 않는 것으로 표시됩니다.

- Microsoft® Windows Server 2019(64비트)
- Microsoft® Active Directory 2016

다음 플랫폼은 2022년 6월 2일에 AEM Forms 6.5.13.0 릴리스에서 더 이상 사용되지 않는 것으로 표시됩니다.
- Microsoft® SharePoint 2016

다음 플랫폼은 2022년 3월 3일에 AEM Forms 6.5.12.0 릴리스에서 더 이상 사용되지 않는 것으로 표시됩니다.

- MongoDB Enterprise 4.0
- MongoDB Enterprise 4.2
- IBM® DB2® 11.1
- Oracle 데이터베이스 12c 릴리스 2
- MySQL 5.7.35
- Microsoft® SQL Server JDBC 드라이버 6.2.1.0
- JBoss® EAP(Enterprise Application Platform) 7.1.4
- IBM® Content Manager Server 8.5 수정 팩 2
- IBM® Content Manager 클라이언트 8.5
- Microsoft® SQL Server 2016

다음 플랫폼은 2021년 9월 7일에 AEM Forms 6.5.10.0 릴리스에서 더 이상 사용되지 않는 것으로 표시됩니다.

- Adobe Acrobat 2017 - [Adobe Acrobat 2017에 대한 핵심 지원은 2022년 6월 6일에 종료됩니다](https://helpx.adobe.com/support/programs/eol-matrix.html).
- Red Hat® Enterprise Linux® 7(커널 3.x)(64비트)
- Microsoft® Office 2016
- OpenOffice 4.1.2


>[!NOTE]
>
더 이상 사용되지 않는 플랫폼은 플랫폼이 제거됨으로 표시되거나 플랫폼에 대한 서드파티 공급업체 지원이 사용 수명 종료에 도달할 때까지 계속 지원을 받습니다.

## 개정 내역 {#revision-history}

- 6.5.18.0 (2023년 8월 31일)
   - **플랫폼 업데이트**: [!DNL Adobe Experience Manager Forms] jee에서 다음 플랫폼에 대한 지원이 추가되었습니다.
      - MongoDB Enterprise 4.4
      - Oracle WebLogic Server 14c
      - 내 SQL JDBC 커넥터 8
      - Active Directory
      - Microsoft® Windows Server 2022(64비트)

   - **플랫폼 업데이트**: [!DNL Adobe Experience Manager Forms] jee에서 다음 플랫폼에 대한 지원이 제거되었습니다.
      - Windows Server 2016(64비트)
      - MongoDB Enterprise 4.0
      - Oracle 데이터베이스 12c 릴리스 2 (12.2.0.1.0)
      - MySQL 5.7.35
      - Microsoft® SQL Server 2016
      - JBoss® EAP 7.1.4
      - 내 SQL JDBC 커넥터 5.1.44
      - Microsoft® SQL Server JDBC 드라이버 6.2.1.0
      - Microsoft® SQL Server JDBC 드라이버 6.2.2.0
      - SQL Server용 Microsoft® JDBC 드라이버 8.x

   - **PDF Generator 서비스용 플랫폼 업데이트**: [!DNL Adobe Experience Manager Forms] jee의 경우 PDF Generator 및 일반적으로 다음 플랫폼에 대한 지원이 제거되었습니다.
      - Microsoft® Sharepoint 2016
      - Microsoft® Office 2016
      - Microsoft® Office Visio 2016
      - Microsoft® Publisher 2016
      - Microsoft® Project 2016
      - OpenOffice 4.1.2
      - Acrobat 2017(클래식 트랙) 버전 17.011.30078 이상

- 6.5.10.0 (2022년 9월 1일)

   - 애플리케이션 서버 JBoss™ EAP 7.4에 대한 Oracle Java® SE 11(64비트) SDK에 대한 지원을 추가했습니다.

- 2022년 3월 3일

   - 다음에 대한 지원이 제거되었습니다.
      - IBM® J9 가상 시스템(빌드 2.8, JRE 1.8.0)
      - Oracle 데이터베이스 12c 릴리스 1
      - Oracle 데이터베이스 18c
      - Oracle OUD(Unified Directory) 11g 릴리스 2
      - IBM® Lotus Domino 9.0
      - IBM® FileNet 5.2
      - Adobe Flash Player

- 2021년 10월 10일

   - 지원되는 AEM Forms 앱용 iOS 버전을 iOS 15.1로 변경했습니다. 이전 버전은 iOS 12였습니다.

- 2021년 9월 07일
   - **플랫폼 업데이트**: [!DNL Adobe Experience Manager Forms] jee에서 다음 플랫폼에 대한 지원이 추가되었습니다.
      - [!DNL Adobe Acrobat 2020]
      - [!DNL Ubuntu 20.04]
      - [!DNL Open Office 4.1.10]
      - [!DNL Microsoft®® Office 2016]
      - [!DNL Microsoft®® Windows Server 2016]
      - [!DNL RHEL8]

- 2020년 12월 3일
   - 다음 플랫폼에 대한 지원이 AEM Forms 6.5.7.0 이상에서 추가되었습니다.
      - [!DNL Microsoft®® SQL Server 2019]

- 2020년 9월 9일

   - 지원되는 AEM Forms 앱용 iOS 버전을 iOS 12로 변경했습니다. 이전 버전은 iOS 11입니다.
