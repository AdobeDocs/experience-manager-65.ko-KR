---
title: 기술 요구 사항
seo-title: Technical Requirements
description: AEM에 대해 지원되는 클라이언트 및 서버 플랫폼 목록입니다.
seo-description: A list of the supported client and server platforms for AEM.
content-type: reference
topic-tags: platform
exl-id: 47529b9a-c4e5-434f-ac26-b01714ff863b
source-git-commit: 72ed4ceee560839c6573461cb5d4d6cbccfd696f
workflow-type: tm+mt
source-wordcount: '3525'
ht-degree: 1%

---

# 기술 요구 사항{#technical-requirements}

Adobe은 이 문서의 다음 정보에 자세히 설명된 대로 플랫폼에서 Adobe Experience Manager(AEM)을 지원합니다.

플랫폼과 특별히 관련된 문제는 플랫폼 공급업체에 문의하십시오.

>[!NOTE]
>
>AEM을 설치하는 플랫폼에 따라 사용자 관리를 위한 다양한 요구 사항 세트가 있을 수 있습니다.

## 사전 요구 사항 {#prerequisites}

Adobe Experience Manager 설치를 위한 최소 요구 사항:

* 설치된 Java Platform, Standard Edition JDK 또는 기타 지원 [Java 가상 컴퓨터](#java-virtual-machines)
* Experience Manager 빠른 시작 파일(독립 실행형 JAR 또는 웹 애플리케이션 배포 WAR)

### 최소 크기 조정 요구 사항 {#minimum-sizing-requirements}

Adobe Experience Manager 실행을 위한 최소 요구 사항:

* 설치 디렉터리에서 5GB의 사용 가능한 디스크 공간
* 2GB 메모리

>[!NOTE]
>
>* 디지털 자산 사용 사례에는 더 많은 기본 메모리가 필요합니다. 자세한 내용은 [배포 및 유지 관리](/help/sites-deploying/deploy.md#default-local-install) 자세한 내용
>* [AEM Forms 추가 기능 패키지](/help/forms/using/installing-configuring-aem-forms-osgi.md) 15GB의 임시 공간이 필요합니다.
>


자세한 내용은 [하드웨어 크기 조정 지침](/help/managing/hardware-sizing-guidelines.md).

### 지원 수준 {#support-levels}

이 문서에서는 Adobe Experience Manager에 대해 지원되는 클라이언트 및 서버 플랫폼을 나열합니다. Adobe은 권장 구성 및 기타 구성을 위해 몇 가지 수준의 지원을 제공합니다.

### 지원되는 구성 {#supported-configurations}

Adobe은 이러한 구성을 권장하며 표준 소프트웨어 유지 관리 계약의 일부로 전체 지원을 제공합니다.

<table>
 <tbody>
  <tr>
   <td>지원 수준</td>
   <td>설명<br />을 따르지 않는 경우입니다 </td>
  </tr>
  <tr>
   <td><strong>A: 지원됨</strong></td>
   <td>Adobe은 이 구성에 대한 모든 지원 및 유지 관리를 제공합니다. 이 구성은 Adobe의 품질 보증 프로세스에서 다룹니다.</td>
  </tr>
  <tr>
   <td><strong>R: 제한된 지원</strong></td>
   <td>고객이 프로젝트를 성공적으로 수행할 수 있도록 하기 위해 Adobe은 제한된 지원 프로그램 내에서 특정 조건을 충족해야 합니다. R 수준 지원은 공식 고객 요청과 Adobe 확인을 필요로 합니다. 자세한 내용은 Adobe 고객 지원 센터에 문의하십시오.</td>
  </tr>
 </tbody>
</table>

### 지원되지 않는 구성 {#unsupported-configurations}

| 지원 수준 | 설명 |
|---|---|
| **Z: 지원되지 않음** | 구성이 지원되지 않습니다. Adobe은 구성 작동 여부에 대한 설명을 만들지 않으며 구성을 지원하지 않습니다. |

## 지원되는 플랫폼 {#supported-platforms}

### Java 가상 컴퓨터 {#java-virtual-machines}

이 응용 프로그램을 사용하려면 JDK(Java Development Kit) 배포에서 제공하는 Java Virtual Machine을 실행해야 합니다.

Adobe Experience Manager은 다음 버전의 Java Virtual Machine을 사용하여 작동합니다.

>[!CAUTION]
>
>프로덕션 환경의 안전과 보안을 보장하고 최신 Java 업데이트를 설치하려면 Java 공급업체의 보안 게시판을 추적하는 것이 좋습니다.

| **플랫폼** | **지원 수준** | **링크** |
|---|---|---|
| Oracle Java SE 11 JDK - 64비트 | A: 지원됨 `[1]` | [다운로드](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+11*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=24&lt;td>) |
| Oracle Java SE 10 JDK | Z: 지원되지 않음 `[1]` |
| Oracle Java SE 9 JDK | Z: 지원되지 않음 `[1]` |
| Oracle Java SE 8 JDK - 64비트 | A: 지원됨 `[1]` | [다운로드](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+8*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=10) |
| IBM J9 VM - 빌드 2.9, JRE 1.8.0 | A: 지원됨 `[2]` |
| IBM J9 VM - 빌드 2.8, JRE 1.8.0 | A: 지원됨 `[2]` |
| 아줄 줄루 오픈JDK 11 - 64비트 | A: 지원됨 `[3]` |  |
| 아줄 줄루 오픈JDK 8 - 64비트 | A: 지원됨 `[3]` |  |

1. Oracle은 Oracle Java SE 제품에 대한 &quot;장기 지원&quot;(LTS) 모델로 이동되었습니다. Java 9, Java 10 및 Java 12는 Oracle에 의한 비 LTS 릴리스입니다(참조) [Oracle Java SE 지원 로드맵](https://www.oracle.com/technetwork/java/eol-135779.html)). 프로덕션 환경에 AEM을 배포하기 위해 Adobe은 Java의 LTS 릴리스에 대해서만 지원을 제공합니다. 공개 업데이트 종료 이후 LTS 릴리스의 모든 유지 관리 업데이트를 포함하여 Oracle Java SE JDK의 지원 및 배포는 Oracle Java SE 기술을 사용하는 모든 AEM 고객을 위해 Adobe에서 직접 지원합니다. 자세한 내용은 [Adobe Experience Manager에 대한 Java 지원 정책](assets/Java_Policy_for_Adobe_Experience_Manager.pdf) 추가 정보.


1. IBM JRE는 WebSphere Application Server에서만 지원됩니다.

1. Azul Zulu OpenJDK LTS 버전은 버전 6.5 SP9부터 온-프레미스 AEM 배포에 지원됩니다. Azul Zulu JDK LTS 버전에 대한 지원 및 배포 시 고객이 Azul에서 직접 라이센스를 받아야 합니다.


### 스토리지 및 지속성 {#storage-persistence}

Adobe Experience Manager 리포지토리를 배포하는 다양한 옵션이 있습니다. 지원되는 기술 및 스토리지 옵션에 대해서는 다음 목록을 참조하십시오.

| **플랫폼** | **설명** | **지원 수준** |
|---|---|---|
| **TAR 파일이 있는 파일 시스템** `[1]` | 저장소 | A: 지원됨 |
| **데이터 저장소가 있는 파일 시스템** `[1]` | 바이너리 | A: 지원됨 |
| 파일 시스템의 TAR 파일에 바이너리 저장 `[1]` | 바이너리 | Z: 프로덕션에서 지원되지 않음 |
| Amazon S3 | 바이너리 | A: 지원됨 |
| Microsoft Azure Blob 저장소 | 바이너리 | A: 지원됨 |
| MongoDB Enterprise 4.2 | 저장소 | A: 지원됨 `[2, 3, 4]` |
| MongoDB Enterprise 4.0 | 저장소 | Z: 지원되지 않음 |
| MongoDB Enterprise 3.6 | 저장소 | Z: 지원되지 않음 |
| MongoDB Enterprise 3.4 | 저장소 | Z: 지원되지 않음 |
| IBM DB2 10.5 | 저장소 및 Forms 데이터베이스 | R: 제한된 지원 `[5]` |
| Oracle 데이터베이스 12c(12.1.x) | 저장소 및 Forms 데이터베이스 | R: 제한된 지원 |
| Microsoft SQL Server 2016 | Forms 데이터베이스 | A: 지원됨 |
| **Apache Lucene(Quickstart 기본 제공)** | 검색 서비스 | A: 지원됨 |
| Apache 솔루션 | 검색 서비스 | A: 지원됨 |

1. &#39;파일 시스템&#39;에는 POSIX 호환 블록 저장소가 포함됩니다. 여기에는 네트워크 스토리지 기술이 포함됩니다. 파일 시스템 성능은 다를 수 있으며 전체 성능에 영향을 줄 수 있습니다. 네트워크/원격 파일 시스템과 함께 테스트 AEM을 로드하는 것이 좋습니다.
1. MongoDB Enterprise 4.2를 사용하려면 최소 AEM 6.5 SP9가 필요합니다.
1. MongoDB 공유는 AEM에서 지원되지 않습니다.
1. MongoDB Storage Engine WiredTiger만 지원됩니다.
1. AEM Forms 업그레이드 고객을 지원합니다. 새 설치에는 지원되지 않습니다.

>[!NOTE]
>
>자세한 내용은 [커뮤니티 배포](/help/communities/deploy-communities.md) AEM Communities 기능에 대한 추가 정보입니다.

>[!NOTE]
>
>MongoDB는 타사 소프트웨어이며 AEM 라이선스 패키지에 포함되어 있지 않습니다. 자세한 내용은 [MongoDB 라이선스 정책](https://www.mongodb.org/about/licensing/) 페이지.
>
>MongoDB를 통해 AEM 배포를 최대한 활용하려면 MongoDB Enterprise 버전의 라이센스를 취득하여 전문 지원을 제공하는 것이 좋습니다. 자세한 내용은 [권장 배포](/help/sites-deploying/recommended-deploys.md#prerequisites-and-recommendations-when-deploying-aem-with-mongomk) 추가 정보.
>
>라이센스에는 작성자나 게시 배포에 사용할 수 있는 하나의 기본 인스턴스와 두 개의 보조 인스턴스로 구성된 표준 복제 세트가 포함되어 있습니다.
>
>MongoDB에서 작성자와 게시를 모두 실행하려면 두 개의 별도 라이센스를 구입해야 합니다.
>
>Adobe 고객 지원 팀은 AEM에서 MongoDB 사용과 관련된 자격 있는 문제를 지원합니다.
>
>자세한 내용은 [Adobe Experience Manager용 MongoDB 페이지](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager).

>[!NOTE]
>
>위에 나열된 지원되는 관계형 데이터베이스는 타사 소프트웨어이며 AEM 라이선스 패키지에 포함되어 있지 않습니다.
>
>지원되는 관계형 데이터베이스로 AEM 6.5를 실행하려면 데이터베이스 공급업체와의 별도의 지원 계약이 필요합니다. Adobe 고객 지원 팀은 AEM 6.5에서 관계형 데이터베이스 사용과 관련된 자격 있는 문제를 지원합니다.
>
>**대부분의 관계형 데이터베이스는 현재 AEM 6.5의 Level-R 내에서 지원되며, 위의 Level-R 설명에 명시된 지원 기준 및 지원 프로그램과 함께 제공됩니다.**

### 서블릿 엔진/애플리케이션 서버 {#servlet-engines-application-servers}

Adobe Experience Manager은 독립형 서버(quickstart JAR 파일)나 타사 애플리케이션 서버(WAR 파일)에서 웹 애플리케이션으로 실행할 수 있습니다.

필요한 최소 서블릿 API 버전은 서블릿 3.1입니다.

| 플랫폼 | 지원 수준 |
|---|---|
| **빠른 시작 내장 서블릿 엔진(Jetty 9.4)** | A: 지원됨 |
| Oracle WebLogic Server 12.2(12cR2) | Z: 지원되지 않음 |
| IBM WebSphere Application Server Continuous Delivery(LibertyProfile)(웹 프로필 7.0 및 IBM JRE 1.8 포함) | R: 신규 계약에 대한 제한된 지원 `[2]` |
| IBM WebSphere Application Server 9.0 및 IBM JRE 1.8 | R: 신규 계약에 대한 제한된 지원 `[1]` `[2]` |
| Apache Tomcat 8.5.x | R: 신규 계약에 대한 제한된 지원 `[2]` |
| JBoss 애플리케이션 서버를 사용하는 JBoss EAP 7.2.x | Z: 지원되지 않음 |
| JBoss 애플리케이션 서버를 사용하는 JBoss EAP 7.1.4 | R: 신규 계약에 대한 제한된 지원 `[1]` `[2]` |
| JBoss Application Server가 포함된 JBoss EAP 7.0.x | Z: 지원되지 않음 |

1. AEM Forms을 사용한 배포에 권장됩니다.
1. 애플리케이션 서버에 대한 AEM 6.5 배포를 시작하면 제한된 지원으로 이동합니다. 기존 고객은 AEM 6.5로 업그레이드하고 애플리케이션 서버를 계속 사용할 수 있습니다. 신규 고객의 경우 위의 수준-R 설명에 나와 있는 지원 기준과 지원 프로그램을 함께 제공합니다.

### 서버 운영 체제 {#server-operating-systems}

Adobe Experience Manager은 프로덕션 환경에 대해 다음 서버 플랫폼에서 작동합니다.

| **플랫폼** | **지원 수준** |
|---|---|
| **Red Hat 배포 기반 Linux** | A: 지원됨 `[1]` `[3]` |
| Debian 배포 incl 기반 Linux. 우분투 | A: 지원됨 `[1]` `[2]` |
| Linux, SUSE 배포 기반 | A: 지원됨 `[1]` |
| Microsoft Windows Server 2019 `[4]` | R: 신규 계약에 대한 제한된 지원 `[5]` |
| Microsoft Windows Server 2016 `[4]` | R: 신규 계약에 대한 제한된 지원 `[5]` |
| Microsoft Windows Server 2012 R2 | Z: 지원되지 않음 |
| Oracle Solaris 11 | Z: 지원되지 않음 |
| IBM AIX 7.2 | Z: 지원되지 않음 |

1. Linux Kernel 2.6, 3.x, 4.x 및 5.x에는 Red Hat Enterprise Linux, CentOS, Oracle Linux 및 Amazon Linux를 포함한 Red Hat 배포의 파생물이 포함되어 있습니다. AEM Forms 추가 기능 기능은 CentOS 7, Red Hat Enterprise Linux 7 및 Red Hat Enterprise Linux 8에서만 지원됩니다.
1. AEM Forms은 Ubuntu 20.04 LTS에서 지원됩니다.
1. Adobe Managed Services에서 지원하는 Linux 배포.
1. Microsoft Windows 프로덕션 배포는 6.5로 업그레이드하고 비프로덕션 사용을 위해 지원됩니다. 새로운 배포는 AEM Sites 및 Assets에 대한 요청 시 제공됩니다.
1. AEM Forms은 지원 수준 R 제한 없이 Microsoft Window Server에서 지원됩니다.

>[!NOTE]
>
>AEM Forms 6.5를 설치하는 경우 다음 32비트 Microsoft Visual C++ 재배포용 파일을 설치했는지 확인하십시오.
>
>* Microsoft Visual C++ 2008 재배포 가능
>* Microsoft Visual C++ 2010 재배포 가능
>* Microsoft Visual C++ 2012 재배포 가능
>* Microsoft Visual C++ 2013 재배포 가능(6.5 기준)



### 가상 및 클라우드 컴퓨팅 환경 {#virtual-cloud-computing-environments}

Adobe Experience Manager은 이 페이지에 나열된 기술 요구 사항 및 Adobe의 표준 지원 약관에 따라 Microsoft Azure 및 Amazon Web Services(AWS)과 같은 클라우드 컴퓨팅 환경의 가상 컴퓨터에서 실행되는 것을 지원합니다.

클라우드 기반의 환경의 경우 AEM 제품 라인에서 최신 서비스를 검토하십시오. Adobe Experience Manager as a Cloud Service. 자세한 내용은 [Adobe Experience Manager as a Cloud Service 설명서](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=en) 자세한 내용

또한 Adobe은 Azure 또는 AWS에 AEM을 배포할 Adobe Managed Services를 제공합니다. Adobe Managed Services는 이러한 클라우드 컴퓨팅 환경에서 AEM을 배포하고 운영하는 경험과 기술을 전문가에게 제공합니다. 자세한 내용은 [Adobe Managed Services에 대한 추가 설명서](https://www.adobe.com/marketing-cloud/enterprise-content-management/managed-services-cloud-platform.html?aemClk=t).

Azure 또는 AWS에 AEM을 배포하거나 기타 모든 클라우드 컴퓨팅 환경에서 배포하는 다른 모든 경우에는 이 페이지에 나열된 기술 사양을 준수하는 Adobe의 지원이 가상 컴퓨팅 환경에 포함됩니다. 이러한 클라우드 환경에서 실행되는 AEM과 관련하여 보고된 모든 문제는 클라우드 서비스가 이 페이지에 나열된 기술 요구 사항(예: Azure Blob 저장 공간 또는 AWS S3)의 일부로 특별히 지원되지 않는 한 클라우드 컴퓨팅 환경과 관련된 모든 클라우드 서비스와 독립적으로 재현할 수 있어야 합니다.

Adobe Managed Services 외부의 Azure 또는 AWS에서 AEM을 배포하는 방법에 대한 권장 사항을 위해 Adobe은 클라우드 환경에서 AEM을 배포하도록 지원하는 클라우드 제공업체 또는 Adobe 파트너와 직접 작업하는 것이 좋습니다. 선택한 클라우드 제공업체 또는 파트너는 특정 성능, 로드, 확장성 및 보안 요구 사항을 충족하기 위해 아키텍처의 크기 조정 사양, 디자인 및 구현을 담당합니다.

### Dispatcher 플랫폼(웹 서버) {#dispatcher-platforms-web-servers}

Dispatcher는 캐싱 및 로드 밸런싱 구성 요소입니다. [최신 Dispatcher 버전을 다운로드합니다](https://helpx.adobe.com/experience-manager/dispatcher/release-notes.html). Experience Manager 6.5를 사용하려면 Dispatcher 버전 4.3.2 이상이 필요합니다.

다음 웹 서버는 Dispatcher 버전 4.3.2에서 사용할 수 있습니다.

| 플랫폼 | 지원 수준 |
|---|---|
| **Apache httpd 2.4.x** `[1,2]` | A: 지원됨 |
| Microsoft IIS 10(인터넷 정보 서버) | A: 지원됨 |
| Microsoft IIS 8.5(인터넷 정보 서버) | Z: 지원되지 않음 |

1. Apache httpd 소스 코드를 기반으로 구축된 웹 서버는 httpd가 기반으로 하는 버전과 동일한 지원 수준을 갖게 됩니다. 확실하지 않은 경우 Adobe에게 각 서버 제품과 관련된 지원 수준을 확인하도록 요청하십시오. 다음과 같은 경우:

   1. HTTP 서버는 공식 Apache 소스 배포만 사용하여 구축되었습니다. 또는
   1. HTTP 서버가 실행 중인 운영 체제의 일부로 전달되었습니다. 예: IBM HTTP Server, Oracle HTTP Server

1. Windows 운영 체제용 Apache 2.4.x에는 Dispatcher를 사용할 수 없습니다.

## 지원되는 클라이언트 플랫폼 {#supported-client-platforms}

### 사용자 인터페이스 작성을 위해 지원되는 브라우저 {#supported-browsers-for-authoring-user-interface}

Adobe Experience Manager 사용자 인터페이스는 다음 클라이언트 플랫폼에서 작동합니다. 모든 브라우저는 기본 플러그인 및 추가 기능으로 테스트됩니다.

AEM 사용자 인터페이스는 더 큰 화면(일반적으로 노트북 및 데스크탑 컴퓨터) 및 태블릿 폼 팩터(예: Apple iPad 또는 Microsoft Surface)에 맞게 최적화되어 있습니다. 휴대폰 폼 팩터는 지원되지 않습니다.

>[!NOTE]
>
>**릴리스 주기가 빠른 브라우저 지원:**
>
>Mozilla Firefox, Google Chrome 및 Microsoft Edge 릴리스는 몇 개월마다 업데이트됩니다. Adobe은 향후 출시될 버전의 이러한 브라우저에서 아래에 명시된 지원 수준을 유지하기 위해 Adobe Experience Manager에 대한 업데이트를 제공하기 위해 노력하고 있습니다.

<table>
 <tbody>
  <tr>
   <td><strong>브라우저</strong></td>
   <td><strong>UI 지원<br /> </strong></td>
   <td><strong>클래식 UI 지원</strong></td>
  </tr>
  <tr>
   <td><strong>Google Chrome(Evergreen)</strong></td>
   <td>A: 지원됨</td>
   <td>A: 지원됨</td>
  </tr>
  <tr>
   <td>Microsoft Edge(에버그린)</td>
   <td>A: 지원됨</td>
   <td>A: 지원됨</td>
  </tr>
  <tr>
   <td>Microsoft Internet Explorer 11</td>
   <td>Z: 지원되지 않음</td>
   <td>Z: 지원되지 않음</td>
  </tr>
  <tr>
   <td>Mozilla Firefox(Evergreen)</td>
   <td>A: 지원됨</td>
   <td>A: 지원됨</td>
  </tr>
  <tr>
   <td>Mozilla Firefox 마지막 ESR [1]</td>
   <td>A: 지원됨</td>
   <td>A: 지원됨</td>
  </tr>
  <tr>
   <td>macOS의 Apple Safari(에버그린)</td>
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
   <td>A: 지원되는 [2]</td>
   <td>Z: 지원되지 않음</td>
  </tr>
  <tr>
   <td>iOS 11.x의 Apple Safari</td>
   <td>Z: 지원되지 않음</td>
   <td>Z: 지원되지 않음</td>
  </tr>
 </tbody>
</table>

1. Firefox의 확장 지원 릴리스 [mozilla.org에서 이에 대해 자세히 알아보십시오](https://www.mozilla.org/en-US/firefox/organizations/faq/)
1. Apple iPad 지원

### 웹 사이트에 대해 지원되는 브라우저 {#supported-browsers-for-websites}

일반적으로 AEM Sites에서 렌더링하는 웹 사이트에 대한 브라우저 지원은 AEM 페이지 템플릿 구현, 디자인 및 구성 요소 출력에 따라 다르므로 이러한 부분을 구현하는 당사자가 제어합니다.

### WebDAV 클라이언트 {#webdav-clients}

**Microsoft Windows 7+**

Microsoft Windows 7+와 SSL을 사용하여 보안이 설정되지 않은 AEM 인스턴스에 연결하려면 Windows에서 비보안 네트워크에 대한 기본 인증을 사용하도록 설정해야 합니다. WebClient의 Windows 레지스트리를 변경해야 합니다.

1. 레지스트리 하위 키를 찾습니다.

   * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters

1. 2 이상의 값을 사용하여 이 하위 키에 BasicAuthLevel 레지스트리 항목을 추가합니다.

Windows에서 WebDav 클라이언트의 응답성을 개선하려면 다음을 참조하십시오. [Microsoft 지원 KB 2445570](https://support.microsoft.com/kb/2445570)

## 추가 플랫폼 정보 {#additional-platform-notes}

이 섹션에서는 Adobe Experience Manager 및 해당 추가 기능 실행에 대한 특수 노트 및 자세한 정보를 제공합니다.

### IPv4 및 IPv6 {#ipv-and-ipv}

Adobe Experience Manager(인스턴스, Dispatcher)의 모든 요소는 IPv4 및 IPv6 네트워크 모두에 설치할 수 있습니다.

별도의 구성이 필요 없으므로 작업이 원활하게 수행됩니다. 필요한 경우 네트워크 유형에 적합한 형식을 사용하여 IP 주소를 지정할 수 있습니다.

즉, IP 주소를 지정해야 할 경우에는 다음 중에서 선택할 수 있습니다.

* 예를 들어 IPv6 주소 `https://[ab12::34c5:6d7:8e90:1234]:4502`

* 예를 들어 IPv4 주소 `https://123.1.1.4:4502`

* 서버 이름(예: `https://www.yourserver.com:4502`

* 기본 사례 `localhost` 은 예를 들어, IPv4 및 IPv6 네트워크 설치에 대해 해석됩니다. `https://localhost:4502`

### AEM Dynamic Media 추가 기능 요구 사항 {#requirements-for-aem-dynamic-media-add-on}

AEM Dynamic Media은 기본적으로 비활성화됩니다. 다음 작업을 보려면 여기를 참조하십시오. [Dynamic Media 활성화](/help/assets/config-dynamic.md#enabling-dynamic-media).

Dynamic Media이 활성화되면 다음과 같은 추가 기술 요구 사항이 적용됩니다.

>[!NOTE]
>
>이러한 시스템 요구 사항 **전용** Dynamic Media - 하이브리드 모드를 사용하는 경우 적용; Dynamic Media - 하이브리드 모드에서는 특정 운영 체제에서만 인증되는 내장 이미지 서버가 있습니다.
>
>Dynamic Media - Scene7 모드(즉, **dynamic media_scene7** runmode)를 사용할 경우 추가적인 시스템 요구 사항이 없습니다. AEM과 동일한 시스템 요구 사항만 해당됩니다. Dynamic Media - Scene7 모드 아키텍처는 AEM에 포함된 서비스가 아니라 클라우드 기반 이미지 서비스를 사용합니다.

#### 하드웨어 {#hardware}

다음 하드웨어 요구 사항은 Linux와 Windows 모두에 적용됩니다.

* 4개 이상의 코어가 있는 Intel Xeon 또는 AMD Opteron CPU
* 적어도 16GB RAM

#### Linux {#linux}

Linux에서 Dynamic Media을 사용하는 경우 다음 사전 요구 사항을 충족해야 합니다.

* RedHat Enterprise 7 또는 CentOS 7 이상(최신 수정 패치 포함)
* 64비트 운영 체제
* 사용 안 함 교환(권장)
* SELinux가 비활성화됨(다음 참고 참조)

>[!NOTE]
>
>로캘이 설정되어 있으면 LC_CTYPE이 다음과 같지 않습니다 `en_US.UTF-8`로 설정되면 Dynamic Media이 작동하지 않습니다. 해당 값이 무엇인지 확인하려면 명령 프롬프트에서 &quot;locale&quot;을 입력합니다. 설정되지 않은 경우 AEM을 실행하기 전에 &quot;export LC_CTYPE=&quot;를 입력하여 LC_CTYPE 환경 변수를 빈 문자열로 설정하십시오.

>[!NOTE]
>
>**SELinux 비활성화:** 이미지 제공이 SELinux를 켜면 작동하지 않습니다. 이 옵션은 기본적으로 활성화되어 있습니다. 이 문제를 해결하려면 **/etc/selinux/config** 파일 및 SELinux 값을 다음으로 변경합니다.
>
>`SELINUX=enforcing` **끝** `SELINUX=disabled`

>[!NOTE]
>
>**NUMA 아키텍처:** AMD64 및 Intel EM64T을 지원하는 프로세서가 있는 시스템은 일반적으로 NUMA(Non-Uniform Memory Architecture) 플랫폼으로 구성되며, 이는 커널이 단일 메모리 노드를 구성하는 대신 부팅 시 여러 메모리 노드를 구성함을 의미합니다.
>
>다중 노드 구문은 다른 노드가 소진되기 전에 하나 이상의 노드에서 메모리 소진을 일으킬 수 있습니다. 메모리 소모가 발생하면 커널에서 사용 가능한 메모리가 있더라도 프로세스(예: 이미지 서버 또는 플랫폼 서버)를 종료하도록 결정할 수 있습니다.
>
>따라서 Adobe은 이러한 시스템을 실행하는 경우 NUMA를 사용하여 끌 것을 권장합니다 **numa=off** 커널에서 이러한 프로세스를 종료하지 않도록 부팅 옵션을 사용합니다.

>[!NOTE]
>
>**서버 호스트 이름을 확인해야 합니다.** 서버의 호스트 이름을 IP 주소로 확인할 수 있는지 확인합니다. 불가능한 경우 정규화된 호스트 이름과 IP 주소를 **/etc/hosts**:
>
>`<ip address> <fully qualified hostname>`

#### Windows {#windows}

* Microsoft Windows Server 2016
* 공간을 실제 메모리(RAM)의 두 배 이상으로 바꿉니다.

Windows에서 Dynamic Media을 사용하려면 x64 및 x86용 Microsoft Visual Studio 2010, 2013 및 2015 재배포용 파일을 설치하십시오.

Windows x64의 경우:

* 에서 Microsoft Visual Studio 2010 재배포 가능 패키지를 가져옵니다. [https://www.microsoft.com/en-us/download/details.aspx?id=13523](https://www.microsoft.com/en-us/download/details.aspx?id=13523)
* 에서 Microsoft Visual Studio 2013 재배포 가능 패키지를 가져옵니다. [https://www.microsoft.com/en-us/download/details.aspx?id=40784](https://www.microsoft.com/en-us/download/details.aspx?id=40784)
* 에서 Microsoft Visual Studio 2015 재배포 가능 패키지를 가져옵니다. [https://www.microsoft.com/en-us/download/details.aspx?id=48145](https://www.microsoft.com/en-us/download/details.aspx?id=48145)

Windows x86의 경우:

* 에서 Microsoft Visual Studio 2010 재배포 가능 패키지를 가져옵니다. [https://www.microsoft.com/en-in/download/details.aspx?id=5555](https://www.microsoft.com/en-in/download/details.aspx?id=5555)
* 에서 Microsoft Visual Studio 2013 재배포 가능 패키지를 가져옵니다. [https://www.microsoft.com/en-in/download/details.aspx?id=40769](https://www.microsoft.com/en-in/download/details.aspx?id=40769)
* 에서 Microsoft Visual Studio 2015 재배포 가능 패키지를 가져옵니다. [https://www.microsoft.com/en-us/download/details.aspx?id=52685](https://www.microsoft.com/en-us/download/details.aspx?id=52685)

#### macOS {#macos}

* 10.9.x 이상
* 평가판 및 데모 용으로만 지원됩니다

### AEM Forms PDF 생성기 요구 사항 {#requirements-for-aem-forms-pdf-generator}

### PDF 생성기를 위한 소프트웨어 지원 {#software-support-for-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>제품</strong></p> </th>
   <th><p><strong>PDF으로 변환을 위한 지원되는 형식</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2020 클래식 트랙</a> 최신 버전</td>
   <td>XPS, 이미지 형식(BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, DWG, DXF 및 DWF)</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2017 클래식 트랙</a> 최신 버전(더 이상 사용되지 않음)</td>
   <td>XPS, 이미지 형식(BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, DWG, DXF 및 DWF)</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2019</td>
   <td>DOC, DOCX, XLS, XLSX, PPT, PPTX, RTF 및 TXT</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2016(지원 중단됨)</td>
   <td>DOC, DOCX, XLS, XLSX, PPT, PPTX, RTF 및 TXT</td>
  </tr>
  <tr>
   <td>WordPerfect 2020<br /> </td>
   <td>WP, WPD</td>
  </tr>
  <tr>
   <td>Microsoft® Office Visio 2016(지원 중단됨)<br /> </td>
   <td>VSD, VSDX</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2019<br /> </td>
   <td>PUB</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2016(지원 중단됨)<br /> </td>
   <td>PUB</td>
  </tr>
  <tr>
   <td>Microsoft® Project 2016(지원 중단됨)<br /> </td>
   <td>MPP</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.10</td>
   <td>ODT, ODP, ODS, ODG, SXW, SXW, SXD, SXD, XLS, DOC, DOCX, PPT, PPTX, PPTX, 이미지 형식(BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPX, JPX, JPX, JPC2, J2C, JPC, RTF, TXT, RTF, TXT, TXT, TXT, RTF, TXT, TXT, RTF, TXT, RTF, TXT, TXT, RTF, RTF</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.2(사용 중지)</td>
   <td>ODT, ODP, ODS, ODG, SXW, SXW, SXD, SXD, XLS, DOC, DOCX, PPT, PPTX, PPTX, 이미지 형식(BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPX, JPX, JPX, JPC2, J2C, JPC, RTF, TXT, RTF, TXT, TXT, TXT, RTF, TXT, TXT, RTF, TXT, RTF, TXT, TXT, RTF, RTF</td>
  </tr>  
 </tbody>
</table>

>[!NOTE]
>
>PDF 생성기는 지원되는 운영 체제 및 응용 프로그램의 영어, 프랑스어, 독일어 및 일본어 버전만 지원합니다.
>
>또한
>
>* PDF 생성기를 사용하려면 32비트 버전의 [Acrobat 2020 classic track 버전 20.004.30006](https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html) 또는 Acrobat 2017 버전 17.011.30078에서 전환을 수행합니다.
>* OpenOffice용 PDF 생성기 전환은 Windows 및 Linux에서만 지원됩니다.
>* PDF 생성기는 Microsoft Office Professional Plus의 32비트 소매 버전과 Windows 운영 체제에서 변환하는 데 필요한 기타 소프트웨어만 지원합니다.
>* PDF 생성기는 Linux 운영 체제에서 32비트 및 64비트 버전의 OpenOffice를 지원합니다.
>* PDF 생성기는 Microsoft Office 365를 지원하지 않습니다.
>* OCR PDF, Optimize PDF 및 Export PDF 기능은 Windows에서만 지원됩니다.
>* Acrobat 버전은 PDF 생성기 기능을 활성화하기 위해 AEM Forms과 번들로 제공됩니다. AEM Forms PDF Generator에서 사용하기 위해 번들로 제공되는 버전은 AEM Forms 라이센스 기간 동안 AEM Forms을 통해서만 프로그래밍 방식으로 액세스할 수 있습니다. 자세한 내용은 배포에 따라 AEM Forms 제품 설명([On-Premise](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html) 또는 [Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html))
>* PDF 생성기 서비스는 Microsoft Windows 10을 지원하지 않습니다.
>* PDF 생성기가 Microsoft Visio 2019를 사용하여 파일을 변환하지 못했습니다. Microsoft Visio 2016을 사용하여 .VSD 및 .VSDX 파일을 계속 변환할 수 있습니다.
>* PDF 생성기가 Microsoft Project 2019를 사용하여 파일을 변환하지 못했습니다. Microsoft Project 2016을 사용하여 .VSD 및 .VSDX 파일을 계속 변환할 수 있습니다.
>


### AEM Forms 디자이너 요구 사항 {#requirements-for-aem-forms-designer}

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

### AEM Assets XMP 메타데이터 쓰기 되돌리기 요구 사항 {#requirements-for-aem-assets-xmp-metadata-write-back}

XMP Write-back은 다음 플랫폼 및 파일 형식에 대해 지원되고 활성화됩니다.

* **운영 체제:**

   * Linux(64비트 시스템에서 32비트 및 32비트 애플리케이션 지원) 32비트 클라이언트 라이브러리를 설치하는 단계는 다음을 참조하십시오 [64비트 RedHat Linux에서 XMP 추출 및 쓰기 응답을 활성화하는 방법](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).

   * Windows Server
   * Mac OS X(64비트)

* **파일 형식**: JPEG, PNG, TIFF, PDF, INDD, AI 및 EPS

### Linux에서 메타데이터가 많은 자산을 처리하는 AEM Assets 요구 사항 {#assetsonlinux}

XMPFilesProcessor 프로세스를 사용하려면 라이브러리 GLIBC_2.14가 필요합니다. Linux 커널 버전 3.1.x와 같이 GLIBC_2.14가 포함된 Linux 커널을 사용합니다. PSD 파일과 같은 대량의 메타데이터를 포함하는 자산을 처리하는 데 대한 성능을 개선합니다. 이전 버전의 GLIBC를 사용하면 `com.day.cq.dam.core.impl.handler.xmp.NCommXMPHandler Failed to read XMP`.
