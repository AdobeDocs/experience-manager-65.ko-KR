---
title: 기술 요구 사항
description: Adobe Experience Manager에 대해 지원되는 클라이언트 및 서버 플랫폼 목록입니다.
topic-tags: platform
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
exl-id: 47529b9a-c4e5-434f-ac26-b01714ff863b
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '3534'
ht-degree: 5%

---

# 기술 요구 사항{#technical-requirements}

Adobe은 이 문서의 다음 정보에 설명된 대로 플랫폼에서 (AEM) Adobe Experience Manager을 지원합니다.

플랫폼과 관련된 모든 문제는 플랫폼 공급업체에 문의하십시오.

>[!NOTE]
>
>AEM을 설치하는 플랫폼에 따라 사용자 관리에 대한 요구 사항 세트가 다를 수 있습니다.

## 사전 요구 사항 {#prerequisites}

Adobe Experience Manager 설치를 위한 최소 요구 사항:

* 설치된 Java™ Platform, Standard Edition JDK 또는 기타 지원되는 [Java™ 가상 컴퓨터](#java-virtual-machines)
* Experience Manager Quickstart 파일(독립형 JAR 또는 웹 애플리케이션 배포 WAR)

### 최소 크기 조정 요구 사항 {#minimum-sizing-requirements}

Adobe Experience Manager 실행을 위한 최소 요구 사항:

* 설치 디렉토리의 사용 가능한 디스크 공간 5GB
* 2GB 메모리

>[!NOTE]
>
>* 디지털 자산 사용 사례에는 더 많은 기본 메모리가 필요합니다. 자세한 내용은 [배포 및 유지 관리](/help/sites-deploying/deploy.md#default-local-install)를 참조하십시오.
>* [AEM Forms 추가 기능 패키지](/help/forms/using/installing-configuring-aem-forms-osgi.md)에는 15GB의 임시 공간이 필요합니다.
>

자세한 내용은 [하드웨어 크기 조정 지침](/help/managing/hardware-sizing-guidelines.md)을 참조하십시오.

### 지원 수준 {#support-levels}

이 문서에서는 Adobe Experience Manager에 대해 지원되는 클라이언트 및 서버 플랫폼을 나열합니다. Adobe은 권장 구성과 기타 구성 모두에 대해 여러 수준의 지원을 제공합니다.

### 지원되는 구성 {#supported-configurations}

Adobe은 이러한 구성을 권장하며 표준 소프트웨어 유지 관리 계약의 일부로 모든 지원을 제공합니다.

<table>
 <tbody>
  <tr>
   <td>지원 수준</td>
   <td>설명<br /> </td>
  </tr>
  <tr>
   <td><strong>A: 지원됨</strong></td>
   <td>Adobe는 이 구성에 대한 전체 지원과 유지 관리를 제공합니다. 이 구성은 Adobe 품질 보증 프로세스에 따라 처리됩니다.</td>
  </tr>
  <tr>
   <td><strong>R: 제한된 지원</strong></td>
   <td>고객의 프로젝트 성공을 보장하기 위해 Adobe은 제한된 지원 프로그램 내에서 모든 지원을 제공하며 이를 위해서는 특정 조건이 충족되어야 합니다. R 레벨 지원에는 공식적인 고객 요청 및 Adobe의 확인이 필요합니다. 자세한 내용은 Adobe 고객 지원에 문의하십시오.</td>
  </tr>
 </tbody>
</table>

### 지원되지 않는 구성 {#unsupported-configurations}

| 지원 수준 | 설명 |
|---|---|
| **Z: 지원되지 않음** | 구성이 지원되지 않습니다. Adobe에서는 해당 구성이 작동하는지 여부에 대해 언급하지 않으며 이를 지원하지 않습니다. |

## 지원되는 플랫폼 {#supported-platforms}

### Java™ 가상 시스템 {#java-virtual-machines}

응용 프로그램을 실행하려면 Java™ Virtual Machine이 필요하며, 이 시스템은 JDK(Java™ Development Kit) 배포에서 제공합니다.

Adobe Experience Manager은 다음 버전의 Java™ 가상 시스템과 함께 작동합니다.

>[!CAUTION]
>
>Java™ 공급업체에서 보안 게시판을 추적합니다. 이렇게 하면 프로덕션 환경의 안전과 보안이 보장됩니다. 또한 항상 최신 Java™ 업데이트를 설치합니다.

| **플랫폼** | **지원 수준** | **링크** |
|---|---|---|
| Oracle Java™ SE 21 JDK | Z: 지원되지 않는 `[1]` |  |
| Oracle Java™ SE 17 JDK | Z: 지원되지 않는 `[1]` |  |
| Oracle Java™ SE 11 JDK - 64비트 | A: 지원되는 `[1]` | [다운로드](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+11*&orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&orderby.sort=desc&layout=list&p.offset=0&p.limit=24<td>) |
| Oracle Java™ SE 10 JDK | Z: 지원되지 않는 `[1]` |  |
| Oracle Java™ SE 9 JDK | Z: 지원되지 않는 `[1]` |  |
| Oracle Java™ SE 8 JDK - 64비트 | A: 지원되는 `[1]` | [다운로드](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+8*&orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&orderby.sort=desc&layout=list&p.offset=0&p.limit=10) |
| IBM® J9 VM - 빌드 2.9, JRE 1.8.0 | A: 지원되는 `[2]` |  |
| IBM® J9 VM - 빌드 2.8, JRE 1.8.0 | A: 지원되는 `[2]` |  |
| Azul Zulu OpenJDK 11 - 64비트 | A: 지원되는 `[3]` | |
| Azul Zulu OpenJDK 8 - 64비트 | A: 지원되는 `[3]` | |

1. Oracle이 Oracle Java™ SE 제품에 대한 &quot;장기 지원&quot;(LTS) 모델로 전환했습니다. Java™ 9, Java™ 10 및 Java™ 12는 Oracle에서 제공하는 비 LTS 릴리스입니다([Oracle Java™ SE 지원 로드맵](https://www.oracle.com/technetwork/java/eol-135779.html) 참조). 프로덕션 환경에 AEM을 배포하기 위해 Adobe은 Java™의 LTS 릴리스에 대해서만 지원을 제공합니다. 공개 업데이트 종료 이후의 LTS 릴리스의 모든 유지 관리 업데이트를 포함하여 Oracle Java™ SE JDK의 지원 및 배포는 Oracle Java™ SE 기술을 사용하는 모든 AEM 고객을 위해 Adobe에서 직접 지원합니다. Adobe Experience Manager에 대한 [Java™ 지원 정책](assets/Java_Policy_for_Adobe_Experience_Manager.pdf)을 참조하세요.
   **중요: Oracle Java™ 11은 최소한 2026년 9월까지 지원됩니다. Oracle Java™ 17 및 21은 [AEM 6.5 LTS](https://experienceleague.adobe.com/en/docs/experience-manager-65-lts/content/implementing/deploying/introduction/technical-requirements)에서 지원됩니다.**

1. IBM® JRE는 WebSphere® Application Server와만 지원됩니다.

1. Azul Zulu OpenJDK LTS 버전은 버전 6.5 SP9부터 온-프레미스 AEM 배포에 대해 지원됩니다. Azul Zulu JDK LTS 버전의 지원 및 배포는 Adobe 고객이 Azul에서 직접 라이선스를 받아야 합니다.


### 스토리지 및 지속성 {#storage-persistence}

Adobe Experience Manager 저장소를 배포하기 위한 다양한 옵션이 있습니다. 지원되는 기술 및 스토리지 옵션에 대해서는 다음 목록을 참조하십시오.

| **플랫폼** | **설명** | **지원 수준** |
|---|---|---|
| **TAR 파일이 있는 파일 시스템** `[1]` | 저장소 | A: 지원됨 |
| **데이터 저장소가 있는 파일 시스템** `[1]` | 바이너리 | A: 지원됨 |
| 파일 시스템 `[1]`의 TAR 파일에 바이너리 저장 | 바이너리 | Z: 프로덕션에 지원되지 않음 |
| Amazon | 바이너리 | A: 지원됨 |
| Microsoft® Azure Blob 저장소 | 바이너리 | A: 지원됨 |
| MongoDB Enterprise 8.0 | 저장소 | A: 지원되는 `[3, 4]` |
| MongoDB Enterprise 7.0 | 저장소 | A: 지원되는 `[3, 4]` |
| MongoDB Enterprise 6.0 | 저장소 | A: 지원되는 `[3, 4]` |
| MongoDB Enterprise 5.0 | 저장소 | A: 지원되는 `[3, 4]` |
| MongoDB Enterprise 4.4 | 저장소 | A: 지원되는 `[2, 3, 4, 7]` |
| MongoDB Enterprise 4.2 | 저장소 | A: 지원되는 `[2, 3, 4, 7]` |
| MongoDB Enterprise 4.0 | 저장소 | Z: 지원되지 않음 |
| MongoDB Enterprise 3.6 | 저장소 | Z: 지원되지 않음 |
| MongoDB Enterprise 3.4 | 저장소 | Z: 지원되지 않음 |
| IBM® DB2® 10.5 | 저장소 및 Forms 데이터베이스 | R: 제한된 지원 `[5]` |
| Oracle 데이터베이스 12c (12.1.x) | 저장소 및 Forms 데이터베이스 | R: 제한된 지원 |
| Oracle 데이터베이스 19c | 저장소 및 Forms 데이터베이스 | R: 제한된 지원 |
| Microsoft® SQL Server 2016 | Forms 데이터베이스 | A: 지원됨 |
| Microsoft® SQL Server 2019(더 이상 사용되지 않음) | Forms 데이터베이스 | A: 지원됨 |
| Microsoft® SQL Server 2022 | Forms 데이터베이스 | A: 지원됨 |
| **Apache Lucene(빠른 시작 기본 제공)** | 검색 서비스 | A: 지원됨 |
| Apache Solr | 검색 서비스 | A: 지원됨 |

1. &#39;파일 시스템&#39;에는 POSIX와 호환되는 블록 저장소가 포함되어 있습니다. 네트워크 스토리지 기술을 포함합니다. 파일 시스템 성능이 달라질 수 있으며 전체 성능에 영향을 줄 수 있습니다. 네트워크/원격 파일 시스템으로 AEM을 로드합니다.
2. MongoDB Enterprise 버전 4.2 및 4.4에는 AEM 6.5 SP9 이상이 필요합니다.
3. MongoDB 분할은 AEM에서 지원되지 않습니다.
4. MongoDB 스토리지 엔진 WiredTiger는 만 지원됩니다.
5. AEM Forms 업그레이드 고객을 위해 지원됩니다. 새 설치에서는 지원되지 않습니다.
6. AEM Forms에만 적용 가능:
   * Oracle Database 12c에 대한 지원이 제거되었으며 Oracle Database 19c에 대한 지원이 추가되었습니다.
   * Microsoft® SQL Server 2016에 대한 지원이 제거되었으며 Microsoft® SQL Server 2019 및 Microsoft® SQL Server 2022에 대한 지원이 추가되었습니다.

>[!NOTE]
>
>AEM Communities 기능에 대한 자세한 내용은 [커뮤니티 배포](/help/communities/deploy-communities.md)를 참조하십시오.

>[!NOTE]
>
>MongoDB는 타사 소프트웨어 프로그램이며 AEM 라이선스 패키지에 포함되어 있지 않습니다. 자세한 내용은 [MongoDB 라이선스 정책](https://www.mongodb.com/licensing/server-side-public-license/faq) 페이지를 참조하십시오.
>
>MongoDB를 통해 AEM 배포를 최대한 활용하려면 Adobe에서 MongoDB Enterprise 버전에 라이선스를 부여하여 전문적인 지원을 받는 것이 좋습니다. 자세한 내용은 [권장 배포](/help/sites-deploying/recommended-deploys.md#prerequisites-and-recommendations-when-deploying-aem-with-mongomk)를 참조하십시오.
>
>라이센스에는 작성자 또는 게시 배포에 사용할 수 있는 하나의 기본 인스턴스와 두 개의 보조 인스턴스로 구성된 표준 복제본 세트가 포함되어 있습니다.
>
>MongoDB에서 작성자와 게시를 모두 실행하려는 경우 두 개의 별도 라이선스를 구입해야 합니다.
>
>Adobe 고객 지원 센터는 AEM에서의 MongoDB 사용과 관련된 자격 부여 문제를 지원합니다.
>
>자세한 내용은 [Adobe Experience Manager용 MongoDB 페이지](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)를 참조하세요.

<!--
>[!NOTE]
>
>Supported relational databases as listed above are third-party software and are not included in the AEM licensing package.
>
>To run AEM 6.5 with a supported relational database, a separate support contract with a database vendor is required. Adobe Customer Care assists qualifying issues related to the usage of relational databases with AEM 6.5.
>
>**Most relational databases are currently supported within Level-R on AEM 6.5, which comes with support criteria and a support program as stated in the Level-R description above.**-->

### 서블릿 엔진 / 애플리케이션 서버 {#servlet-engines-application-servers}

Adobe Experience Manager은 독립형 서버(quickstart JAR 파일)로 실행하거나 타사 애플리케이션 서버(WAR 파일) 내의 웹 애플리케이션으로 실행할 수 있습니다.

필요한 최소 서블릿 API 버전은 서블릿 3.1입니다.

| Platform | 지원 수준 |
|---|---|
| **Quickstart 기본 제공 서블릿 엔진(Jetty 9.4)** | A: 지원됨 |
| Oracle WebLogic Server 12.2(12cR2) | Z: 지원되지 않음 |
| 웹 프로필 7.0 및 IBM® JRE 1.8을 사용한 IBM® WebSphere® Application Server Continuous Delivery(LibertyProfile) | R: 새 계약에 대한 지원이 제한됨 `[2]` |
| IBM® WebSphere® Application Server 9.0 및 IBM® JRE 1.8 | R: 새 계약에 대한 지원이 제한됨 `[1]` `[2]` |
| IBM® WebSphere® 응용 프로그램 서버 9.0.0.10 | R: 새 계약에 대한 지원이 제한됨 `[1]` `[2]` |
| Apache Tomcat 8.5.x | R: 새 계약에 대한 지원이 제한됨 `[2]` |
| JBoss® 애플리케이션 서버와 JBoss® EAP 7.2.x | Z: 지원되지 않음 |
| JBoss® 애플리케이션 서버와 JBoss® EAP 7.1.4 | R: 새 계약에 대한 지원이 제한됨 `[1]` `[2]` |
| JBoss® 애플리케이션 서버와 JBoss® EAP 7.0.x | Z: 지원되지 않음 |
| JBoss® EAP 7.4(JBoss® Application Server 포함) <sup>[2] [3] [7] | A: 지원됨 |

1. AEM Forms을 사용하는 배포에 권장됩니다.
2. 애플리케이션 서버에서 AEM 6.5 배포를 시작하면 제한된 지원으로 이동합니다. 기존 고객은 AEM 6.5로 업그레이드하고 애플리케이션 서버를 계속 사용할 수 있습니다. 신규 고객의 경우 위의 Level-R 설명에 명시된 대로 지원 기준 및 지원 프로그램을 제공합니다.
3. 적용 가능한 AEM Forms만:
   * JBoss® EAP 7.1.4에 대한 지원을 제거하고 JBoss® EAP 7.4.10에 대한 지원을 추가했습니다.

### 서버 운영 체제 {#server-operating-systems}

Adobe Experience Manager은 프로덕션 환경을 위해 다음 서버 플랫폼과 함께 작동합니다.

| **플랫폼** | **지원 수준** |
|---|---|
| **Linux®, Red Hat® 배포 기반** | A: 지원되는 `[1]` `[3]` |
| Debian 배포 기반 Linux®에는 다음이 포함됩니다. 우분투 | A: 지원되는 `[1]` `[2]` |
| Linux®, SUSE® 배포 기반 | A: 지원되는 `[1]` |
| Microsoft® 윈도우 서버 2022 | R: 제한된 지원 |
| Microsoft® Windows Server 2019 `[4]`(더 이상 사용되지 않음) | R: 새 계약에 대한 지원이 제한됨 `[5]` |
| Microsoft® Windows Server 2016 `[4]` | R: 새 계약에 대한 지원이 제한됨 `[5]` |
| Microsoft® Windows Server 2012 R2 | Z: 지원되지 않음 |
| Oracle Solaris™ 11 | Z: 지원되지 않음 |
| IBM® AIX® 7.2 | Z: 지원되지 않음 |

1. Linux® 커널 2.6, 3. x, 4. x, 5. x, 6. x 와 9. x에는 Red Hat® Enterprise Linux®, Oracle Linux® 및 Amazon Linux®를 포함하여 Red Hat® 배포판의 파생물이 포함되어 있습니다. AEM Forms 추가 기능 기능은 Red Hat® Enterprise Linux® 8 및 Red Hat® Enterprise Linux® 9에서만 지원됩니다.
2. AEM Forms은 Ubuntu 20.04 및 SUSE® Linux® Enterprise Server 15 SP6(64비트)에서 지원됩니다.
3. Adobe Managed Services에서 지원하는 Linux® 배포.

   >[!NOTE]
   >
   >Linux 기반 서버(OSGI 및 JEE 스택)의 경우 AEM Forms 추가 기능에는 다음과 같은 런타임 종속성이 필요합니다.
   >* glibc.x86_64 (2.17-196)
   >* libX11.x86_64 (1.6.7-4)
   >* zlib.x86-64 (1.2.7-17)
   >* libxcb.x86_64 (1.13-1.el7)
   >* libXau.x86_64 (1.0.8-2.1.el7)
   >* glibc-locale.x86_64 (2.17 이상)
   >* OpenSSL 3(OS의 기본 위치에 필요).

   *OpenSSL 3 설치의 경우: 라이브러리 libcrypto.so.3 및 libssl.so.3은 LD_LIBRARY_PATH 환경 변수가 나타내는 기본 라이브러리 경로에서 사용할 수 있어야 합니다. 비표준 위치에 설치된 경우 서버를 시작하기 전에 이 경로가 LD_LIBRARY_PATH에 추가되었는지 확인하십시오.*

4. Microsoft® Windows 프로덕션 배포는 6.5로 업그레이드하는 고객 및 비프로덕션 사용을 위해 지원됩니다. 새 배포는 AEM Sites 및 Assets에 대한 온디맨드 요청입니다.
5. AEM Forms은 지원 수준 R 제한 없이 Microsoft® Window Server에서 지원됩니다.
6. AEM Forms에서 Microsoft® Windows Server 2016에 대한 지원이 제거되었습니다.

>[!NOTE]
>
>AEM Forms 6.5를 설치하는 경우 다음 32비트 Microsoft® Visual C++ 재배포 가능 패키지를 설치했는지 확인하십시오.
>
>* Microsoft® Visual C++ 2008 재배포 가능
>* Microsoft® Visual C++ 2010 재배포 가능
>* Microsoft® Visual C++ 2012 재배포 가능
>* Microsoft® Visual C++ 2013 재배포 가능
>* Microsoft® Visual C++ 2019(VC14.28 이상) 재배포 가능

### 가상 및 클라우드 컴퓨팅 환경 {#virtual-cloud-computing-environments}

Adobe Experience Manager은 클라우드 컴퓨팅 환경의 가상 컴퓨터에서 실행될 수 있습니다. 이러한 환경에는 이 페이지에 나열된 기술 요구 사항을 준수하고 Adobe의 표준 지원 약관에 따라 실행되는 Microsoft® Azure 및 Amazon Web Services(AWS)가 포함됩니다.

클라우드 기반 환경의 경우 AEM 제품 라인의 최신 오퍼링인 Adobe Experience Manager as a Cloud Service을 검토하십시오. 자세한 내용은 [Adobe Experience Manager as a Cloud Service 설명서](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=ko-KR)를 참조하세요.

또한 Adobe은 Adobe Managed Services을 제공하여 Azure 또는 AWS에 AEM을 배포합니다. Adobe Managed Services은 이러한 클라우드 컴퓨팅 환경에서 AEM을 배포하고 운영하는 경험과 기술을 전문가에게 제공합니다. [Adobe Managed Services에 대한 추가 설명서](https://business.adobe.com/products/experience-manager/managed-services.html?aemClk=t)를 참조하세요.

Azure나 AWS 또는 기타 클라우드 컴퓨팅 환경에서 AEM을 배포하는 다른 모든 경우에는 Adobe의 지원이 가상 컴퓨팅 환경에 포함됩니다. 해당 가상 환경은 이 페이지에 나열된 기술 사양을 준수하여 실행되어야 합니다. 이러한 클라우드 환경에서 실행되는 AEM과 관련하여 보고된 문제는 클라우드 컴퓨팅 환경과 관련된 모든 클라우드 서비스와 별도로 재현할 수 있어야 합니다. 즉, Azure Blob 저장 공간 또는 AWS S3 등 이 페이지에 나열된 기술 요구 사항의 일부로 클라우드 서비스가 지원되지 않는 경우.

Adobe Managed Services 외부의 Azure 또는 AWS에 AEM을 배포하는 방법에 대한 권장 사항을 알려면 Adobe에서 직접 클라우드 공급자와 작업하는 것이 좋습니다. 또는 선택한 클라우드 환경에서 AEM의 배포를 지원하는 Adobe 파트너와 협력합니다. 선택한 클라우드 공급업체 또는 파트너는 특정 성능, 로드, 확장성 및 보안 요구 사항을 충족하도록 아키텍처 크기 조정 사양, 설계 및 구현을 담당합니다.

### Dispatcher 플랫폼(웹 서버) {#dispatcher-platforms-web-servers}

Dispatcher은 캐싱 및 로드 밸런싱 구성 요소입니다. [최신 Dispatcher 버전을 다운로드합니다](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html). Experience Manager 6.5를 사용하려면 Dispatcher 버전 4.3.2 이상이 필요합니다.

Dispatcher 버전 4.3.2에서 사용할 수 있는 웹 서버는 다음과 같습니다.

| Platform | 지원 수준 |
|---|---|
| **Apache httpd 2.4.x** `[1,2]` | A: 지원됨 |
| Microsoft® IIS 10(Internet Information Server) | A: 지원됨 |
| Microsoft® IIS 8.5(Internet Information Server) | Z: 지원되지 않음 |

1. Apache httpd 소스 코드를 기반으로 구축된 웹 서버는 기반이 되는 httpd 버전만큼 많은 지원을 제공합니다. 확실하지 않은 경우 Adobe에 각 서버 제품과 관련된 지원 수준을 확인하도록 요청하십시오. 다음과 같은 경우:

   1. HTTP 서버는 공식 Apache 소스 배포만 사용하여 빌드되었습니다. 또는
   1. HTTP 서버는 실행 중인 운영 체제의 일부로 전달되었습니다. 예: IBM® HTTP Server, Oracle HTTP Server

1. Dispatcher은 Windows 운영 체제용 Apache 2.4.x에서 사용할 수 없습니다.

## 지원되는 클라이언트 플랫폼 {#supported-client-platforms}

### 사용자 인터페이스 작성에 지원되는 브라우저 {#supported-browsers-for-authoring-user-interface}

Adobe Experience Manager 사용자 인터페이스는 다음 클라이언트 플랫폼에서 작동합니다. 모든 브라우저는 기본 플러그인 및 추가 기능 세트에 대한 테스트를 완료했습니다.

AEM 사용자 인터페이스는 더 큰 화면(일반적으로 노트북 및 데스크탑 컴퓨터)과 태블릿 폼 팩터(예: Apple iPad 또는 Microsoft® 표면)에 최적화되어 있습니다. 휴대폰 폼 팩터는 지원되지 않습니다.

>[!NOTE]
>
>**릴리스 주기가 빠른 브라우저 지원:**
>
>Mozilla Firefox, Google Chrome 및 Microsoft® Edge 릴리스 업데이트는 몇 개월마다 업데이트됩니다. Adobe은 이러한 브라우저의 향후 버전에 따라 아래에 명시된 대로 지원 수준을 유지하기 위해 Adobe Experience Manager에 대한 업데이트를 제공하기로 약속했습니다.

<table>
 <tbody>
  <tr>
   <td><strong>브라우저</strong></td>
   <td><strong>UI 지원<br /> </strong></td>
   <td><strong>클래식 UI 지원</strong></td>
  </tr>
  <tr>
   <td><strong>Google Chrome (Evergreen)</strong></td>
   <td>A: 지원됨</td>
   <td>A: 지원됨</td>
  </tr>
  <tr>
   <td>Microsoft® Edge(에버그린)</td>
   <td>A: 지원됨</td>
   <td>A: 지원됨</td>
  </tr>
  <tr>
   <td>Microsoft® Internet Explorer 11</td>
   <td>Z: 지원되지 않음</td>
   <td>Z: 지원되지 않음</td>
  </tr>
  <tr>
   <td>Mozilla Firefox (Evergreen)</td>
   <td>A: 지원됨</td>
   <td>A: 지원됨</td>
  </tr>
  <tr>
   <td>Mozilla Firefox 마지막 ESR [1]</td>
   <td>A: 지원됨</td>
   <td>A: 지원됨</td>
  </tr>
  <tr>
   <td>macOS의 Apple Safari(Evergreen)</td>
   <td>A: 지원됨</td>
   <td>A: 지원됨</td>
  </tr>
  <tr>
   <td>macOS의 Apple Safari 11.x</td>
   <td>Z: 지원되지 않음</td>
   <td>Z: 지원되지 않음</td>
  </tr>
  <tr>
   <td>iOS 12.x의 Apple Safari</td>
   <td>A: 지원됨 [2]</td>
   <td>Z: 지원되지 않음</td>
  </tr>
  <tr>
   <td>iOS 11.x의 Apple Safari</td>
   <td>Z: 지원되지 않음</td>
   <td>Z: 지원되지 않음</td>
  </tr>
 </tbody>
</table>

1. Firefox의 확장 지원 릴리스 [mozilla.org에 대해 자세히 알아보기](https://www.mozilla.org/en-US/firefox/enterprise/)
1. Apple iPad 지원

### 웹 사이트에 지원되는 브라우저 {#supported-browsers-for-websites}

일반적으로 AEM Sites에서 렌더링하는 웹 사이트에 대한 브라우저 지원은 AEM 페이지 템플릿, 디자인 및 구성 요소 출력의 구현에 따라 다르며, 따라서 이러한 부분을 구현하는 당사자의 통제 하에 있습니다.

### WebDAV 클라이언트 {#webdav-clients}

**Microsoft® Windows 7+**

Microsoft® Windows 7+를 SSL로 보호되지 않는 AEM 인스턴스에 연결할 경우 Windows에서 비보안 네트워크를 통한 기본 인증을 활성화해야 합니다. WebClient의 Windows 레지스트리를 변경해야 합니다.

1. 레지스트리 하위 키를 찾습니다.

   * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters

1. 2 이상의 값을 사용하여 BasicAuthLevel 레지스트리 항목을 이 하위 키에 추가합니다.

## 추가 플랫폼 노트 {#additional-platform-notes}

이 섹션에서는 Adobe Experience Manager 및 해당 추가 기능 실행에 대한 특수 참고 사항과 보다 자세한 정보를 제공합니다.

### IPv4 및 IPv6 {#ipv-and-ipv}

Adobe Experience Manager의 모든 요소(예: Dispatcher)는 IPv4 및 IPv6 네트워크 모두에 설치할 수 있습니다.

특별한 구성이 필요하지 않아 원활한 작업이 가능합니다. 필요한 경우 네트워크 유형에 적합한 형식을 사용하여 IP 주소를 지정합니다.

IP 주소를 지정해야 하는 경우 다음 중에서 선택할 수 있습니다(필요에 따라).

* IPv6 주소입니다. 예, `https://[ab12::34c5:6d7:8e90:1234]:4502`

* IPv4 주소입니다. 예, `https://123.1.1.4:4502`

* 서버 이름. 예, `https://www.yourserver.com:4502`

* `localhost`의 기본 대/소문자는 IPv4 및 IPv6 네트워크 설치 모두에 대해 해석됩니다. 예, `https://localhost:4502`

### AEM Dynamic Media 추가 기능 요구 사항 {#requirements-for-aem-dynamic-media-add-on}

AEM Dynamic Media는 기본적으로 비활성화되어 있습니다. [Dynamic Media를 사용](/help/assets/config-dynamic.md#enabling-dynamic-media)하려면 여기를 참조하십시오.

Dynamic Media가 활성화되면 다음 추가 기술 요구 사항이 적용됩니다.

>[!NOTE]
>
>이러한 시스템 요구 사항 **전용**&#x200B;은(는) Dynamic Media - 하이브리드 모드를 사용하는 경우에 적용됩니다. Dynamic Media - 하이브리드 모드에는 특정 운영 체제에서만 인증되는 포함된 이미지 서버가 있습니다.
>
>Dynamic Media - Scene7 모드(즉, **dynamicmedia_scene7** 실행 모드)를 실행하는 Dynamic Media 고객의 경우 추가적인 시스템 요구 사항은 없으며, AEM과 동일한 시스템 요구 사항만 있습니다. Dynamic Media - Scene7 모드 아키텍처는 AEM에 포함된 서비스가 아닌 클라우드 기반 이미지 서비스를 사용합니다.

#### 하드웨어 {#hardware}

Linux® 및 Windows 모두에 다음 하드웨어 요구 사항을 적용할 수 있습니다.

* Intel Xeon® 또는 AMD® Opteron CPU(최소 4개 코어)
* 최소 16GB RAM

#### Linux® {#linux}

Linux®에서 Dynamic Media를 사용하는 경우 다음 사전 요구 사항을 충족해야 합니다.

* Red Hat® Enterprise 8 이상 및 최신 수정 패치
* 비트 운영 체제
* 스와핑 비활성화됨(권장)
* SELinux가 비활성화되었습니다(다음 참고 사항 참조)

>[!NOTE]
>
>LC_CTYPE이 `en_US.UTF-8`과(와) 같지 않도록 로캘을 설정하면 Dynamic Media가 작동하지 않습니다. 해당 값이 무엇인지 보려면 명령 프롬프트에서 &quot;locale&quot;을 입력하십시오. 제대로 설정되지 않은 경우 AEM을 실행하기 전에 &quot;export LC_CTYPE=&quot;을 입력하여 LC_CTYPE 환경 변수를 빈 문자열로 설정합니다.

>[!NOTE]
>
>**SELinux 사용 안 함:** 이미지 서비스 제공이 SELinux를 켠 상태로 작동하지 않습니다. 이 옵션은 기본적으로 활성화되어 있습니다. 이 문제를 해결하려면 **/etc/selinux/config** 파일을 편집하고 다음 위치에서 SELinux 값을 변경하십시오.
>
>`SELINUX=enforcing` **~** `SELINUX=disabled`

>[!NOTE]
>
>**NUMA 아키텍처:** AMD64 및 Intel® EM64T를 지원하는 프로세서가 탑재된 시스템은 일반적으로 NUMA(Non-Uniform Memory Architecture) 플랫폼으로 구성됩니다. 즉, 커널은 하나의 메모리 노드를 구성하는 것이 아니라 부트 시에 여러 개의 메모리 노드를 구성한다.
>
>다중 노드 구성은 다른 노드가 소진되기 전에 하나 이상의 노드에서 메모리 소진을 초래할 수 있다. 메모리 소진이 발생하면 커널은 사용 가능한 메모리가 있더라도 프로세스(예: 이미지 서버 또는 플랫폼 서버)를 종료하기로 결정할 수 있습니다.
>
>따라서 Adobe에서는 커널이 이러한 프로세스를 중단하지 않도록 **numa=off** 부팅 옵션을 사용하여 NUMA를 해제하는 시스템을 실행하는 것이 좋습니다.

>[!NOTE]
>
>**서버 호스트 이름을 확인해야 합니다.** 서버의 호스트 이름을 IP 주소로 확인할 수 있는지 확인하십시오. 불가능한 경우 정규화된 호스트 이름과 IP 주소를 **/etc/hosts**&#x200B;에 추가하십시오.
>
>`<ip address> <fully qualified hostname>`

#### Windows {#windows}

* Microsoft® 윈도우 서버 2016
* 물리적 메모리(RAM)의 최소 두 배 정도의 공간 교체

Windows에서 Dynamic Media를 사용하려면 Microsoft® Visual Studio 2010, 2013 및 2015 x64 및 x86용 재배포 가능 패키지를 설치하십시오.

Windows x64의 경우

* [https://www.microsoft.com/en-us/download/details.aspx?id=26999](https://www.microsoft.com/en-us/download/details.aspx?id=26999)에서 Microsoft® Visual Studio 2010 재배포 가능 패키지를 가져옵니다.
* [https://www.microsoft.com/en-us/download/details.aspx?id=40784](https://www.microsoft.com/en-us/download/details.aspx?id=40784)에서 Microsoft® Visual Studio 2013 재배포 가능 패키지를 가져옵니다.
* [https://www.microsoft.com/en-us/download/details.aspx?id=48145](https://www.microsoft.com/en-us/download/details.aspx?id=48145)에서 Microsoft® Visual Studio 2015 재배포 가능 패키지를 가져옵니다.

Windows x86의 경우:

* [https://www.microsoft.com/en-us/download/details.aspx?id=26999](https://www.microsoft.com/en-us/download/details.aspx?id=26999)에서 Microsoft® Visual Studio 2010 재배포 가능 패키지를 가져옵니다.
* [https://www.microsoft.com/en-in/download/details.aspx?id=40769](https://www.microsoft.com/en-in/download/details.aspx?id=40769)에서 Microsoft® Visual Studio 2013 재배포 가능 패키지를 가져옵니다.
* [https://www.microsoft.com/en-us/download/details.aspx?id=52685](https://www.microsoft.com/en-us/download/details.aspx?id=52685)에서 Microsoft® Visual Studio 2015 재배포 가능 패키지를 가져옵니다.

#### macOS {#macos}

* 10.9.x 이상
* 체험판 및 데모 목적으로만 지원됨

### PDF Generator에 대한 고려 사항 {#software-support-for-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>제품</strong></p> </th>
   <th><p><strong>PDF으로 전환하기 위해 지원되는 형식</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat Pro DC</a> 최신 버전</td>
   <td>XPS, 이미지 형식(BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML 및 HTM</td>
  </tr>

<tr>
   <td>Microsoft® Office 2021 Professional Plus, 소매 및 볼륨 라이선스</td>
   <td>DOC, DOCX, XLS, XLSX, PPT, PPTX, RTF 및 TXT</td>
  </tr>
  <tr>
   <td>
    <strong>OpenOffice 4.1.15</strong>   </td>
   <td>
    ODT, ODP, ODS, ODG, ODF, SXW, SXI, SXC, SXD, XLS, XLSX, DOC, DOCX, PPT, PPTX, 이미지 형식(BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, RTF, TXT<br>

</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* PDF Generator은 지원되는 운영 체제 및 애플리케이션의 영어, 프랑스어, 독일어 및 일본어 버전만 지원합니다.
>* PDF Generator에서 변환을 수행하려면 Adobe Acrobat Pro DC(32비트)가 필요합니다.
>* PDF Generator은 변환에 필요한 Microsoft® Office Professional Plus 및 기타 소프트웨어의 32비트 버전만 지원합니다.
>* 볼륨 라이선스가 있는 설치가 지정된 기간 내에 KMS 호스트를 찾을 수 없는 것과 같은 이유로 Microsoft® Office 설치가 비활성화되거나 사용이 허가되지 않는 경우, 설치 라이선스를 다시 취득하고 다시 활성화하기 전까지 전환이 실패할 수 있습니다.
>* PDF Generator은 Microsoft® Office 365를 지원하지 않습니다.
>* OpenOffice용 PDF Generator 전환은 Windows 및 Linux®에서만 지원됩니다.
>* OCR PDF, PDF 최적화 및 Export PDF 기능은 Windows에서만 지원됩니다.
>* Acrobat 버전은 PDF Generator 기능을 사용할 수 있도록 AEM Forms과 번들로 제공됩니다. 번들 버전은 AEM Forms PDF Generator에서만 사용할 수 있도록 AEM Forms 라이선스가 있는 동안 AEM Forms을 사용하여 프로그래밍 방식으로 액세스해야 합니다. 자세한 내용은 배포에 따른 AEM Forms 제품 설명([On-Premise](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html) 또는 [Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html))을 참조하십시오.
>* PDF Generator 서비스는 Microsoft® Windows 11을 지원하지 않습니다.

### AEM Forms Designer 요구 사항 {#requirements-for-aem-forms-designer}

* Microsoft® Windows® 2016 Server, Microsoft® Windows® 2019 Server, Microsoft® Windows® 10 또는 Windows® 11
* PAE, NX 및 SSE2를 지원하는 1GHz 이상의 프로세서
* 32비트용 RAM 1GB 또는 64비트 OS용 RAM 2GB
* 32비트용 16GB 디스크 공간 또는 64비트 OS용 20GB 디스크 공간
* 그래픽 메모리 - 128MB GPU(256MB 권장)
* 2.35GB의 사용 가능한 하드 디스크 공간
* 1024 X 768 픽셀 이상의 모니터 해상도
* 비디오 하드웨어 가속(옵션)
* Acrobat Pro DC, Acrobat Standard DC 또는 Adobe Acrobat Reader DC
* Designer을 설치할 수 있는 관리 권한
* 32비트 AEM Forms Designer용 Microsoft Visual C++ 2019(VC 14.28 이상) 32비트 런타임
* 64비트 AEM Forms Designer용 Microsoft Visual C++ 2019(VC 14.28 이상) 64비트 런타임(OSGI 및 JEE 스택 모두 해당)

[AEM Forms 디자이너 설치 및 구성](/help/forms/using/installing-configuring-designer.md)

### AEM Assets XMP 메타데이터 쓰기 되돌리기 요구 사항 {#requirements-for-aem-assets-xmp-metadata-write-back}

XMP 다시 쓰기는 다음 플랫폼 및 파일 형식에 대해 지원 및 활성화됩니다.

* **운영 체제:**

   * Linux®(64비트 시스템에서 32비트 및 32비트 애플리케이션 지원)

   * Windows Server
   * macOS X (64비트)

* **파일 형식**: JPEG, PNG, TIFF, PDF, INDD, AI 및 EPS.

### AEM Assets이 Linux에서 메타데이터가 많은 에셋을 처리하기 위한 요구 사항입니다® {#assetsonlinux}

XMPFilesProcessor 프로세스가 작동하려면 GLIBC_2.14 라이브러리가 필요합니다. GLIBC_2.14가 포함된 Linux® 커널을 사용합니다(예: Linux® 커널 버전 3.1.x). PSD 파일과 같이 대량의 메타데이터가 포함된 에셋을 처리하는 경우 성능이 향상됩니다. 이전 버전의 GLIBC를 사용하면 `com.day.cq.dam.core.impl.handler.xmp.NCommXMPHandler Failed to read XMP`(으)로 시작하는 로그에 오류가 발생합니다.
