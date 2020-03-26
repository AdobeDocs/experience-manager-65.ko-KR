---
title: JEE에서 지원되는 AEM Forms 플랫폼
seo-title: JEE에서 지원되는 AEM Forms 플랫폼
description: JEE 파섹
seo-description: JEE 파섹
uuid: 777f943b-4cb4-444e-a036-8032b9fce5be
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: f777865e-d4a8-40ef-87b0-130c19eb1b91
docset: aem65
translation-type: tm+mt
source-git-commit: 6cf69dc86ce70a43e77b00d6b3986fa40ae0a4ec

---


# JEE에서 지원되는 AEM Forms 플랫폼{#supported-platforms-for-aem-forms-on-jee}

## 지원되는 플랫폼 {#supported-platforms}

### 지원 수준 {#support-levels}

JEE 서버의 AEM Forms는 지원되는 운영 체제, 응용 프로그램 서버, 데이터베이스, 데이터베이스 드라이버, JDK, LDAP 서버 및 이메일 서버를 조합하여 설정할 수 있습니다.

이 문서에서는 JEE에서 AEM Forms에 대해 지원되는 클라이언트 및 서버 플랫폼을 나열합니다. Adobe는 권장 구성과 기타 구성에 대해 여러 수준의 지원을 제공합니다. 또한 지원되는 다른 소프트웨어 및 해당 버전, 예외 사항, 패치 정의 및 타사 소프트웨어 패치 지원 정책을 나열합니다.

>[!NOTE]
>
>* 지원되는 서버 플랫폼에 대한 전체 예외 목록은 지원되는 서버 [플랫폼에](../../forms/using/aem-forms-jee-supported-platforms.md#p-exceptions-to-supported-server-platforms-p)대한 예외를 참조하십시오.
>* JEE의 AEM Forms는 지원되는 운영 체제 및 애플리케이션의 영어, 프랑스어, 독일어 및 일본어 버전만 지원합니다.
>



### 권장 구성 {#recommendedconfigurations}

Adobe는 이러한 구성을 권장하며 표준 소프트웨어 유지 관리 계약의 일부로 전체 또는 제한된 지원을 제공합니다.

<table>
 <tbody>
  <tr>
   <th>지원 수준</th>
   <th>설명</th>
  </tr>
  <tr>
   <td>A:지원됨<br /> </td>
   <td>Adobe는 이 구성에 대한 완벽한 지원 및 유지 관리를 제공합니다. 이 구성에는 Adobe의 품질 보증 프로세스가 적용됩니다.</td>
  </tr>
  <tr>
   <td>R:제한된 지원</td>
   <td>Adobe는 특정 사전 요구 사항을 충족한 후 이 구성에 대한 모든 지원을 제공합니다. 사전 요구 사항에 대한 자세한 내용을 살펴보려면 Adobe 엔터프라이즈 지원에 문의하십시오.</td>
  </tr>
  <tr>
   <td>L:제한된 지원</td>
   <td>Adobe는 특정 사전 요구 사항을 충족한 후 이 구성에 대한 완벽한 지원 및 유지 관리를 제공합니다. 구성에서 일부 기능을 사용할 수 있는 것은 아닙니다. 사전 요구 사항에 대한 자세한 내용을 살펴보려면 Adobe 엔터프라이즈 지원에 문의하십시오.<br /> </td>
  </tr>
 </tbody>
</table>

### 지원되지 않는 구성 {#unsupported-configurations}

| 지원 수준 | 설명 |
|---|---|
| E:작동해야 함 | 구성이 작동될 것으로 예상되며 이에 대한 보고가 없습니다. |
| Z:지원되지 않음 | 구성이 지원되지 않습니다. Adobe는 구성이 작동되는지 여부에 대해 어떠한 언급도 하지 않으며, 지원하지 않습니다. |

>[!NOTE]
>
>AEM Forms 고객이 소유 비용을 절감하고 배포 아키텍처를 간소화하며 개발 스택을 현대화할 수 있도록 Adobe Experience Manager 엔터프라이즈 플랫폼은 독립 실행형 OSGi 기반 배포를 위해 애플리케이션 서버 기반 배포에서 벗어납니다. Adobe는 인프라 구성 요소 축소가 있는 AEM Forms JEE 스택을 계속 지원합니다.
>
>6.5 릴리스를 통해 Adobe 고객의 사용량이 가장 낮은 인프라 구성 요소는 다음과 같이 더 이상 지원되지 않습니다.
>・ Oracle WebLogic 애플리케이션 서버
>・ IBM DB2 데이터베이스
>・ IBM AIX 및 Sun Solaris 운영 체제
>
>새로운 설치의 경우 AEM Forms를 최신 OSGi 스택에 배포할 수 있으므로 양식 데이터 모델을 사용하여 반응형 모바일, 멀티채널 인터랙티브 커뮤니케이션 및 백엔드 데이터 통합에 대한 혁신적인 최신 기능을 활용할 수 있습니다.
>
>기존 사용자가 JEE 스택에 AEM Forms를 계속 배포해야 한다는 것을 알고 있습니다. 이러한 시나리오에서 Adobe는 이 설명서에 설명된 대로 지원되는 인프라에 AEM Forms JEE를 배포해야 합니다. AEM 6.5 Forms로 업그레이드하고 이전 AEM Forms 릴리스에서 지원되지 않는 플랫폼을 사용하는 경우 Adobe 지원에 문의하여 지원되는 플랫폼으로 업그레이드하는 방법에 대한 도움말을 확인할 수 있습니다.

### JVM(Java Virtual Machines) {#java-virtual-machines-jvm}

Adobe Experience Manager Forms를 사용하려면 Java Virtual Machine이 실행되고 JDK(Java Development Kit) 배포에서 제공됩니다. Adobe Experience Manager는 다음 버전의 Java Virtual Machines와 연동됩니다.

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
   <td>IBM® J9 Virtual Machine(빌드 2.8, JRE 1.8.0)</td>
   <td>A:지원됨</td>
   <td>사소한 릴리스 및 업데이트</td>
  </tr>
  <tr>
   <td>IBM® J9 Virtual Machine(빌드 2.9, JRE 1.8.0)<br /> </td>
   <td>A:지원됨</td>
   <td>사소한 릴리스 및 업데이트</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* JEE의 AEM Forms는 프로덕션 환경에서 64비트 JVM만 지원합니다.
>* 프로덕션 환경의 안전과 보안을 유지하고 최신 Java 업데이트를 설치하려면 Java 공급업체의 보안 게시판을 추적하는 것이 좋습니다.
>



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
   <td><p>Oracle Database 12c 릴리스 1</p> </td>
   <td><p>저장소 마이크로커널</p> </td>
   <td><p>지원됨</p> </td>
  </tr>
  <tr>
   <td>Oracle 데이터베이스 18c </td>
   <td>저장소 마이크로커널</td>
   <td>지원됨</td>
  </tr>

<tr>
   <td>Oracle 데이터베이스 19c </td>
   <td>보관소</td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td><p>Microsoft SQL Server 2016</p> </td>
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

* IBM DB2는 새로 설치할 수 없습니다. AEM 6.5 Forms로 업그레이드하는 기존 고객에게만 지원됩니다.
* MongoDB 파섹 자세한 내용은 MongoDB [라이선스 정책](https://www.mongodb.org/about/licensing/) 페이지를 참조하십시오.
* AEM 배포를 최대한 활용하려면 Adobe에서 전문 지원을 받으려면 MongoDB Enterprise 버전의 라이선스를 부여하는 것이 좋습니다.
* Adobe 고객 지원 센터는 AEM에서 MongoDB 사용과 관련된 자격 조건을 갖춘 문제를 지원합니다. 자세한 내용은 Adobe Experience Manager [용 MongoDB 페이지를](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)참조하십시오.
* &#39;File System&#39;에는 POSIX 호환 블록 스토리지가 포함됩니다. 여기에는 네트워크 스토리지 기술이 포함됩니다. 파일 시스템 성능이 다를 수 있으며 전체 성능에 영향을 줄 수 있습니다. 네트워크/원격 파일 시스템과 함께 테스트 AEM을 로드하는 것이 좋습니다.
* MongoDB 스토리지 엔진 WiredTiger만 지원됩니다.
* MongoDB 공유는 AEM에서 지원되지 않습니다.
* JEE의 AEM Forms는 RDBMK 지속성에 대한 MySQL을 지원하지 않습니다.
* Document Security 모듈은 Content Repository를 사용하지 않습니다. 이는 Document Security만 사용하고 HTML Workspace, HTML5 양식 또는 적응형 양식을 사용하지 않을 계획인 경우 컨텐츠 저장소를 설치하지 않음을 의미합니다.
* JEE의 AEM Forms는 AEM Repository(CRX-Repository)를 지속하기 위한 MySQL 사용을 지원하지 않습니다.


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
   <td><p>JEE 설치 시 AEM Forms와 함께 제공</p> </td>
  </tr>
  <tr>
   <td>Microsoft SQL Server<br /> </td>
   <td><p>Microsoft® SQL Server JDBC 드라이버 6.2.1.0<br /> </p> <p>sqljdbc6.jar</p> </td>
   <td><p>JEE 설치 시 AEM Forms와 함께 제공됩니다.</p> </td>
  </tr>
  <tr>
   <td>Oracle</td>
   <td><p>Oracle Database 19.3.0.0.0 JDBC 드라이버</p> <p>ojdbc8.jar (버전 19.3.0.0.0)<br /> </p> </td>
   <td><p>Oracle Website <a href="https://www.oracle.com/technetwork/database/features/jdbc/jdbc-ucp-122-3110062.html">에서 다운로드합니다</a>.</p> </td>
  </tr>
 </tbody>
</table>

### 애플리케이션 서버 {#application-servers}

<table>
 <tbody>
  <tr>
   <td><p><strong> 플랫폼</strong></p> </td>
   <td><p><strong>지원 수준</strong></p> </td>
   <td><p><strong>지원되는 패치 정의</strong></p> </td>
  </tr>
  <tr>
   <td>IBM® WebSphere® Application Server 9.0 <sup>[1] [4]</sup><br /> </td>
   <td>A:지원됨</td>
   <td>서비스 팩 및 중요 업데이트</td>
  </tr>
  <tr>
   <td><p>JBoss® 엔터프라이즈 애플리케이션 플랫폼(EAP) 7.1.4 <sup>[2] [3] [7]</sup></p> </td>
   <td><p>A:지원됨</p> </td>
   <td><p>지원되는 EAP 버전에 대한 패치 및 누적 패치</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>IBM® WebSphere® 클러스터는 네트워크 배포 에디션에서만 지원됩니다.

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
   <td><p>Red Hat Enterprise Linux 7(커널 3.x)(64비트)</p> </td>
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

물리적 시스템 또는 가상 환경에서 JEE에서 AEM Forms를 실행할 수 있습니다. 그러나 가상 환경에서 AEM Forms에 문제가 발생하면 물리적 컴퓨터에서 해당 문제를 복제해 보십시오. 실제 컴퓨터에서 문제가 지속되는 경우 Adobe 지원 팀에 해결 방법을 문의하십시오. 물리적 시스템에서 복제할 수 없는 문제는 가상 환경 공급업체에 문의하십시오.

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

JEE 서버에서 AEM Forms를 설정할 플랫폼을 선택할 때 다음 예외를 고려하십시오.

1. JEE의 AEM Forms는 MySQL과 함께 IBM® WebSphere®를 지원하지 않습니다.
1. JEE의 AEM Forms는 SUSE Linux Enterprise Server 12에서 JBoss를 지원하지 않습니다. SUSE Linux Enterprise Server 12에서는 IBM WebSphere만 지원됩니다.
1. JEE의 AEM Forms는 Oracle Java™ SE 이외의 JBoss®가 있는 JDK를 지원하지 않습니다.
1. JEE의 AEM Forms는 IBM® JDK가 아닌 IBM® WebSphere®가 있는 JDK를 지원하지 않습니다.
1. CRX-repository는 TarMK, MongoDB, 관계형 데이터베이스(RDBMK)의 지속성을 지원합니다. 응용 프로그램 서버와 CRX 저장소 사이에 두 개의 다른 데이터베이스 시스템을 가질 수 없습니다. 그러나 JEE 환경의 AEM Forms에서는 MongoMK를 CRX 리포지토리와 애플리케이션 서버가 있는 지원되는 관계형 데이터베이스를 함께 사용할 수 있습니다.
1. JEE 파섹
1. JEE의 AEM Forms는 RBAC(JBoss 역할 기반 액세스 제어)를 지원하지 않습니다.

또한 JEE 배포에서 Adobe AEM Forms용 소프트웨어를 선택할 때 다음 사항을 고려하십시오.

* JEE의 AEM Forms는 지원되는 주요 버전 및 보조 버전의 지정된 소프트웨어 위에 있는 업데이트, 패치 및 수정 팩을 지원합니다. 하지만 다음 주 또는 부 버전으로 업데이트할 수 있는 경우는 구체적으로 명시되지 않습니다.
* 클러스터 기반 설치에서는 TarMK 지속성을 지원하지 않습니다. 지원되는 지속성에 대한 자세한 내용은 AEM [Forms 설치에](/help/forms/using/choosing-persistence-type-for-aem-forms.md)대한 지속성 유형 선택을 참조하십시오.
* JEE의 AEM Forms는 서드 파티 소프트웨어 지원 정책에 따라 다양한 서드 파티 [소프트웨어를 지원합니다](../../forms/using/aem-forms-jee-supported-platforms.md#p-third-party-patch-support-policy-p).
* JEE의 AEM Forms는 타사 공급업체의 지원에 따라 플랫폼을 지원합니다. 일부 조합은 타사 공급업체에서 허용하지 않을 수 있습니다. 예를 들어, 많은 벤더가 Oracle을 사용하여 애플리케이션 서버를 인증하지 않았습니다. 따라서 JEE의 AEM Forms도 이러한 조합을 지원하지 않습니다. 지원되는 소프트웨어 버전을 선택하려면 타사 공급업체의 지원 매트릭스를 확인하십시오.
* JEE의 AEM Forms는 TarMK Cold Standby를 지원하지 않습니다.
* JEE의 AEM Forms는 수직 클러스터링을 지원하지 않습니다.
* JEE의 AEM Forms는 클러스터된 환경에서 MySQL 데이터베이스를 지원하지 않습니다.
* 제거되거나 업데이트된 플랫폼 목록은 AEM 6.5 양식 [새 기능 요약 문서를 참조하십시오](../../forms/using/whats-new.md) .

### LDAP 서버(선택 사항) {#ldap-servers-optional}

<table>
 <tbody>
  <tr>
   <th><p><strong>제품(기본 버전)</strong></p> </th>
   <th><p><strong>지원되는 패치 정의</strong></p> </th>
  </tr>
  <tr>
   <td>Oracle OOD(Unified Directory) 11g 릴리스 2</td>
   <td>서비스 팩</td>
  </tr>
  <tr>
   <td>Microsoft Active Directory 2016</td>
   <td>유지 관리 릴리스 및 수정 팩</td>
  </tr>
  <tr>
   <td><p>IBM® Tivoli Directory Server 6.4</p> </td>
   <td><p>기능 팩 및 중간 수정</p> </td>
  </tr>
 </tbody>
</table>

### 이메일 서버(선택 사항) {#email-servers-optional}

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
   <td>IBM 파일 이름</td>
   <td>5.2</td>
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

### Cordova 지원 {#support-for-cordova}

이제 AEM Forms 앱에서 Apache Cordova를 지원합니다. 지원되는 플랫폼별 Cordova 버전은 다음과 같습니다.

* Apache Cordova 6.4.0
* Cordova iOS 4.3.0
* Cordova Android 6.0.0
* Cordova Windows 4.4.3

### PDF Generator 소프트웨어 지원 {#software-support-for-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>제품</strong></p> </th>
   <th><p><strong>PDF로 변환할 수 있는 지원되는 형식</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2017 클래식 트랙</a> 최신 버전</td>
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
   <td>ODT, ODP, ODS, ODG, ODF, SXW, SXI, SXC, SXD, XLS, XLSX, DOC, DOCX, PPT, PPTX, 이미지 형식(BMP, GIF, JPEG, JPG, TIF, TIFF, TIFF, TIFF PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, RTF 및 TXT</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>PDF Generator는 지원되는 운영 체제 및 애플리케이션의 영어, 프랑스어, 독일어 및 일본어 버전만 지원합니다.
>
>추가:
>
>* PDF Generator를 변환하려면 32비트 버전의 [Acrobat 2017 클래식 트랙 버전 17.011.30078 이상이](https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html) 필요합니다.
>* PDF Generator는 Microsoft Office Professional Plus의 32비트 소매 버전과 변환에 필요한 기타 소프트웨어만 지원합니다.
>* PDF Generator는 Microsoft Office 365를 지원하지 않습니다.
>* OpenOffice용 PDF Generator 변환은 Windows 및 Linux에서만 지원됩니다.
>* OCR PDF, PDF 최적화 및 PDF 내보내기 기능은 Windows에서만 지원됩니다.
>* Acrobat 버전은 AEM Forms와 함께 번들로 제공되므로 PDF Generator 기능을 사용할 수 있습니다. 번들로 제공되는 버전은 AEM Forms 라이선스의 기간 동안 AEM Forms PDF Generator와 함께 사용할 경우에만 프로그래밍 방식으로 액세스해야 합니다. 자세한 내용은 배포에 따라 AEM Forms 제품 설명을 참조하십시오(온프레미스 또는[Managed](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html) Services [)](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html)&quot;
   >
   >
* PDF Generator 서비스는 Microsoft Windows 10을 지원하지 않습니다.
>



### 액세서빌러티 지원에 대한 예외 {#exceptions-to-accessibility-support}

AEM Forms의 다음 하위 시스템은 508 [을 준수하지 않습니다](https://www.section508.gov/) .

* 적응형 양식 작성 UI
* Forms Manager 작성 UI
* 통신 관리 작성 UI
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
   <td>Intel® Xeon® E5-2680, 2.4GHz 프로세서 또는 동급<br /> VMWare ESX 5.1 이상<br /> RAM:6GB(64비트 JVM이 있는 64비트 OS)<br /> 디스크 여유 공간:15GB의 임시 공간 및 JEE에서 AEM<br /> Forms를 위한 22GB</td>
  </tr>
  <tr>
   <td>SUSE Linux Enterprise Server</td>
   <td>Intel Xeon E5-2670v2, vCPU 1개, 2.5GHz 프로세서<br /> AWS m3.medium(3ECU)<br /> RAM:6GB(64비트 JVM이 있는 64비트 OS)<br /> 디스크 여유 공간:6GB의 임시 공간 및 JEE에서 AEM<br /> Forms를 위한 22GB</td>
  </tr>
  <tr>
   <td>Red Hat Enterprise Linux</td>
   <td>Intel Xeon E5-2670v2, vCPU 1개, 2.5GHz 프로세서<br /> AWS m3.medium(3ECU)<br /> RAM:6GB(64비트 JVM이 있는 64비트 OS)<br /> 디스크 여유 공간:6GB의 임시 공간 및 JEE에서 AEM<br /> Forms를 위한 22GB<br /> </td>
  </tr>
  <tr>
   <td>소규모 프로덕션 환경을 위한 하드웨어 요구 사항</td>
   <td>
    <ul>
     <li><strong>Intel 기반 환경</strong>:Intel® Xeon® E5-2680, 2.4GHz 이상 듀얼 코어 프로세서를 사용하면 성능이 더욱 향상됩니다</li>
     <li><strong>메모리: </strong>4GB <br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

추가 요구 사항은 다음을 참조하십시오.

* [JEE 배포 시 단일 서버 AEM Forms 시스템 요구 사항](https://www.adobe.com/go/learn_aemforms_sysreq_single_63)
* [JEE 배포 시 클러스터된 AEM Forms에 대한 시스템 요구 사항
   ](https://www.adobe.com/go/learn_aemforms_sysreq_cluster_63)

## JEE에서 AEM Forms에 지원되는 클라이언트 {#supported-clients-for-aem-forms-on-jee}

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

* 설치를 위한 디스크 공간:워크벤치의 경우 1.7GB, Workbench, Designer 및 임시 설치 디렉토리의 경우 단일 드라이브의 경우 2.7GB, 임시 설치 디렉토리의 경우 샘플 어셈블리 400MB - 사용자 임시 디렉토리의 경우 200MB, Windows 임시 디렉토리의 경우 200MB 이러한 위치가 모두 단일 드라이브에 있는 경우 설치 중에 1.5GB의 공간을 사용할 수 있어야 합니다. 설치가 완료되면 임시 디렉토리에 복사된 파일이 삭제됩니다.

* 워크벤치 실행을 위한 메모리:2GB RAM
* 하드웨어 요구 사항:Intel® Pentium® 4 또는 AMD 동급 프로세서, 1GHz 프로세서
* 최소 1024 X 768 픽셀 이상의 모니터 해상도(16비트 컬러 이상)
* JEE 서버의 AEM Forms에 대한 TCP/IPv4 또는 TCP/IPv6 네트워크 연결
* Windows에 워크벤치를 설치하려면 관리 권한이 있어야 합니다. 관리자가 아닌 계정을 사용하여 설치하는 경우 설치 관리자가 적절한 계정에 대한 자격 증명을 입력하라는 메시지를 표시합니다.

### 디자이너 {#designer}

**참고:** Windows에 Designer를 설치하려면 관리자 권한으로 설치 프로그램을 실행합니다.

* Microsoft® Windows® 2016 Server, Microsoft Windows 10

   * PAGE, NX 및 SSE2를 지원하는 1GHz 프로세서 이상
   * 32비트 RAM의 경우 1GB 또는 64비트 OS의 경우 2GB RAM
   * 32비트 또는 64비트 OS용 20GB의 디스크 공간 16GB

* 그래픽 메모리 - 128MB GPU(256MB 권장)
* 2.35GB의 하드 디스크 여유 공간
* DVD-ROM 드라이브
* Internet Explorer 10 또는 11Firefox 45.x
* 1024 X 768픽셀 이상의 모니터 해상도
* 비디오 하드웨어 가속(선택 사항)
* Acrobat Pro DC, Acrobat Standard DC 또는 Adobe Acrobat Reader DC.

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
>Acrobat DC 제품군은 기본적으로 다른 Acrobat과 Reader 모두에 대해 두 개의 트랙을 제공합니다.&quot;Classic&quot; 및 &quot;Continuous.&quot; 두 트랙에 대한 자세한 내용 및 비교는 https://www.adobe.com/go/acrobatdctracks을 [참조하십시오.](https://www.adobe.com/go/acrobatdctracks)

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
   <td><p>Microsoft Edge(Evergreen)</p> </td>
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
   <td>A:지원됨<br /><br /> </td>
   <td>모든 업데이트</td>
  </tr>
  <tr>
   <td>Apple Safari 11.x</td>
   <td>A:지원됨</td>
   <td>모든 업데이트</td>
  </tr>
  <tr>
   <td>Apple Safari 12.x<br /><br /> </td>
   <td>A:지원됨</td>
   <td>모든 업데이트</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>데스크탑에 대한 일부 브라우저 관련 예외는 다음과 같습니다.
>
>* 대부분의 최신 브라우저는 더 이상 NPAPI 기반 플러그인을 지원하지 않습니다. AEM Forms 애플리케이션 및 워크플로우에 미치는 영향에 대한 자세한 내용은 NPAPI [브라우저 플러그인 폐지 및 그 효과를](https://helpx.adobe.com/aem-forms/kb/discontinuation-of-npapi-plugins-impact-on-aem-forms.html)참조하십시오.
>* Safari는 Macintosh OS X에서만 지원됩니다.
>* 작업 영역은 Acrobat DC 이상 버전과 함께 Macintosh OS X 10.6 및 10.7에서 Safari 5.1을 지원합니다. Safari 5.1 Adobe Reader, Acrobat과의 호환성에 대한 자세한 내용은 https://helpx.adobe.com/x-productkb/multi/safari-5-1-incompatible-reader.html을 [참조하십시오](https://helpx.adobe.com/x-productkb/multi/safari-5-1-incompatible-reader.html).
>* 관리 콘솔은 Safari에서 지원되지 않습니다.
>* 통신 관리에서는 AEM 6.1 양식용 Windows® Internet Explorer 9.0을 지원하지 않습니다.
>* 양식 포털은 Internet Explorer 11에서 액세스 가능성을 위해 JAWS 14.0 화면 판독기 소프트웨어를 지원합니다.
>



#### 모바일 클라이언트 {#mobile-clients}

<table>
 <tbody>
  <tr>
   <th><p><strong>브라우저(기본)</strong></p> </th>
   <th><p><strong>지원되는 패치 정의</strong></p> </th>
  </tr>
  <tr>
   <td><p>Android™ 4.1.2 이상 버전의 Chrome</p> </td>
   <td><p>모든 업데이트</p> </td>
  </tr>
  <tr>
   <td>iOS 11.0 이상 버전의 Safari</td>
   <td>모든 업데이트</td>
  </tr>
  <tr>
   <td>Microsoft Edge<br /> </td>
   <td>모든 업데이트<br /> </td>
  </tr>
  <tr>
   <td>Android™ 4.4 이상 버전의 기본 Android 브라우저</td>
   <td>모든 업데이트</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* Forms 포털은 iPad의 Safari에서만 지원됩니다.
>



### AEM Forms app {#aem-forms-workspace-app}

#### 모바일 디바이스 지원 {#mobile-device-support}

AEM Forms 앱은 다음 플랫폼에서 사용할 수 있습니다.

| **플랫폼** | **지원되는 디바이스** |
|---|---|
| Apple iOS | iOS 11 이상 버전을 실행하는 Apple iPhone, iPad, iPad Air 및 iPad mini. |
| Google Android | Android 5.1 이상. AEM Forms 앱은 7~10인치 삼성 갤럭시 태블릿과 인기 있는 스마트폰에서 인증되었습니다. |
| Microsoft Windows | Microsoft Windows 10 운영 체제를 실행하는 Microsoft Surface 디바이스, 태블릿, 랩탑 및 데스크탑 |

### Adobe Flash Player {#adobe-flash-player}

<table>
 <tbody>
  <tr>
   <th><p><strong>Flash Player(기본)</strong></p> </th>
   <th><p><strong>지원되는 패치 정의</strong></p> </th>
  </tr>
  <tr>
   <td><p>Flash Player 최신 버전</p> </td>
   <td><p>보조 버전 및 업데이트</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Adobe는 2020년 말에 Flash Player 업데이트 및 배포를 [중단할 예정입니다](https://theblog.adobe.com/adobe-flash-update/).

### Adobe Document Security Extension for Microsoft Office {#adobe-rights-management-extension-for-microsoft-office}

Adobe Document Security Extension for Microsoft® Office의 시스템 요구 사항을 확인하려면 [여기를](https://www.adobe.com/products/livecycle/rightsmanagement/extension/downloads.html) 클릭하십시오.

### 클라이언트 지원에 대한 예외 {#exceptions-to-client-support}

JEE의 AEM Forms는 지원되는 주요 버전 및 보조 버전의 지정된 소프트웨어 위에 있는 업데이트, 패치 및 수정 팩을 지원합니다. 하지만 다음 주 또는 부 버전으로 업데이트할 수 있는 경우는 구체적으로 명시되지 않습니다.

## 타사 패치 지원 정책 {#third-party-patch-support-policy}

JEE에서 AEM Forms에 대한 타사 소프트웨어 요구 사항은 해당 제품 문서의 &quot;시스템 요구 사항&quot; 섹션에 설명되어 있습니다. 모든 설명서는 https://adobe.com/go/learn_aemforms_documentation_65에서 액세스할 수 [있습니다](https://adobe.com/go/learn_aemforms_documentation_65) .

JEE의 타사 참조 플랫폼의 AEM Forms에는 JEE에서 AEM Forms를 개발 및 배포하는 동안, 그리고 JEE에서 해당 버전의 AEM Forms에서 지원하는 인프라의 최소 패치/서비스 팩 수준에서 최신 상태에 있었던 타사 인프라의 특정 패치 수준이 표시됩니다.

Adobe는 JEE에서 지원하는 AEM Forms 버전과의 역방향 호환성을 보장한다는 가정 하에 타사 공급업체의 릴리스 시 발행되는 긴급 패치 또는 권장 패치를 지원합니다. Adobe는 JEE 설명서의 AEM Forms에 명시된 최소 패치 수준 이후에 릴리스된 패치만 지원합니다.

경우에 따라 Adobe는 주요 기능을 변경하는 타사 업데이트를 지원하지 않으므로 이전 버전과의 완벽한 호환성을 지원하지 않습니다. 지원되는 업데이트에 대한 자세한 내용은 특정 공급업체 [제품에 대한 지원 패치 정의](https://helpx.adobe.com/aem-forms/aem-forms-third-party-software-patch.html) 및 Adobe에서 지원하는 패치 유형을 참조하십시오.

Adobe의 통제 밖에 있는 상황에서 이전 버전과의 호환성을 주장하는 타사 패치는 Adobe 제품 또는 고객 환경에 부정적인 영향을 줄 수 있습니다. 이러한 경우, Adobe는 고객이 중요한 시스템에 적용하기 전에 타사의 긴급 패치가 미치는 영향을 평가할 것을 권장합니다. Adobe는 일반적인 Adobe 지원 프로그램을 통해 또는 제3자가 패치에서 문제를 수정함으로써 이러한 문제를 해결하기 위해 합리적인 사업 노력을 기울인 타사와 협력할 것입니다. 이는 Adobe에서 지원할 새롭게 릴리스된 타사 패치가 벤더 또는 JEE의 AEM Forms에 의해 문서화된 대로 작동한다는 것을 보장하지 않습니다.

Adobe는 JEE 릴리스에서 AEM Forms가 지원하는 타사 참조 플랫폼과 지원되는 패치 정의를 특정 시점에 변경할 수 있는 권한을 가집니다.

타사 패치에 대한 추가 정보는 Adobe 엔터프라이즈 지원 사이트에서 제품과 관련된 기술 자료 문서를 검색하여 찾을 수 있습니다.

[지원 문의](https://www.adobe.com/account/sign-in.supportportal.html)
