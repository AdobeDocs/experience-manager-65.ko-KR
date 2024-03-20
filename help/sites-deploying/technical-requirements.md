---
title: 기술 요구 사항
description: Adobe Experience Manager에 대해 지원되는 클라이언트 및 서버 플랫폼 목록입니다.
topic-tags: platform
exl-id: 47529b9a-c4e5-434f-ac26-b01714ff863b
solution: Experience Manager, Experience Manager Sites
source-git-commit: d3822f4dee1b0d571aa06142f4a4f6e27874cf53
workflow-type: tm+mt
source-wordcount: '3652'
ht-degree: 1%

---

# 기술 요구 사항{#technical-requirements}

Adobe은 이 문서의 다음 정보에 자세히 설명된 대로 플랫폼에서 (AEM) Adobe Experience Manager을 지원합니다.

플랫폼과 관련된 모든 문제는 플랫폼 공급업체에 문의하십시오.

>[!NOTE]
>
>AEM을 설치하는 플랫폼에 따라 사용자 관리에 대한 요구 사항 세트가 다를 수 있습니다.

## 사전 요구 사항 {#prerequisites}

Adobe Experience Manager 설치를 위한 최소 요구 사항:

* 설치된 Java™ Platform, Standard Edition JDK 또는 기타 지원 [Java™ 가상 시스템](#java-virtual-machines)
* Experience Manager Quickstart 파일(독립형 JAR 또는 웹 애플리케이션 배포 WAR)

### 최소 크기 조정 요구 사항 {#minimum-sizing-requirements}

Adobe Experience Manager 실행을 위한 최소 요구 사항:

* 설치 디렉토리의 사용 가능한 디스크 공간 5GB
* 2GB 메모리

>[!NOTE]
>
>* 디지털 자산 사용 사례에는 더 많은 기본 메모리가 필요합니다. 다음을 참조하십시오 [배포 및 유지 관리](/help/sites-deploying/deploy.md#default-local-install) 을 참조하십시오.
>* [AEM Forms 추가 기능 패키지](/help/forms/using/installing-configuring-aem-forms-osgi.md) 15GB의 임시 공간이 필요합니다.
>

자세한 내용은 [하드웨어 크기 조정 지침](/help/managing/hardware-sizing-guidelines.md).

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
   <td>Adobe은 이 구성에 대한 전체 지원 및 유지 관리 기능을 제공합니다. 이 구성은 Adobe의 품질 보증 프로세스가 다룹니다.</td>
  </tr>
  <tr>
   <td><strong>R: 제한된 지원</strong></td>
   <td>고객의 프로젝트 성공을 보장하기 위해 Adobe은 제한된 지원 프로그램 내에서 모든 지원을 제공하며 이는 특정 조건이 충족되어야 합니다. R 레벨 지원에는 공식적인 고객 요청 및 Adobe 확인이 필요합니다. 자세한 내용은 Adobe 고객 지원 센터에 문의하십시오.</td>
  </tr>
 </tbody>
</table>

### 지원되지 않는 구성 {#unsupported-configurations}

| 지원 수준 | 설명 |
|---|---|
| **Z: 지원되지 않음** | 구성이 지원되지 않습니다. Adobe은 구성의 작동 여부에 대해 설명하지 않으며 이를 지원하지 않습니다. |

## 지원되는 플랫폼 {#supported-platforms}

### Java™ 가상 시스템 {#java-virtual-machines}

응용 프로그램을 실행하려면 Java™ Virtual Machine이 필요하며, 이 시스템은 JDK(Java™ Development Kit) 배포에서 제공합니다.

Adobe Experience Manager은 다음 버전의 Java™ 가상 시스템과 함께 작동합니다.

>[!CAUTION]
>
>Java™ 공급업체에서 보안 게시판을 추적합니다. 이렇게 하면 프로덕션 환경의 안전과 보안이 보장됩니다. 또한 항상 최신 Java™ 업데이트를 설치합니다.

| **플랫폼** | **지원 수준** | **링크** |
|---|---|---|
| Oracle Java™ SE 17 JDK | Z: 지원되지 않음 `[1]` |
| Oracle Java™ SE 11 JDK - 64비트 | A: 지원됨 `[1]` | [다운로드](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+11*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=24&lt;td>) |
| Oracle Java™ SE 10 JDK | Z: 지원되지 않음 `[1]` |
| Oracle Java™ SE 9 JDK | Z: 지원되지 않음 `[1]` |
| Oracle Java™ SE 8 JDK - 64비트 | A: 지원됨 `[1]` | [다운로드](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+8*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=10) |
| IBM® J9 VM - 빌드 2.9, JRE 1.8.0 | A: 지원됨 `[2]` |
| IBM® J9 VM - 빌드 2.8, JRE 1.8.0 | A: 지원됨 `[2]` |
| Azul Zulu OpenJDK 11 - 64비트 | A: 지원됨 `[3]` | |
| Azul Zulu OpenJDK 8 - 64비트 | A: 지원됨 `[3]` | |

1. Oracle이 Oracle Java™ SE 제품에 대한 &quot;장기 지원&quot;(LTS) 모델로 전환되었습니다. Java™ 9, Java™ 10 및 Java™ 12는 Oracle에 의한 비 LTS 릴리스입니다(참조) [Oracle Java™ SE 지원 로드맵](https://www.oracle.com/technetwork/java/eol-135779.html)). 프로덕션 환경에 AEM을 배포하기 위해 Adobe은 Java™의 LTS 릴리스에 대해서만 지원을 제공합니다. 공개 업데이트 종료 이후의 LTS 릴리스의 모든 유지 관리 업데이트를 포함하여 Oracle Java™ SE JDK의 지원 및 배포는 Oracle Java™ SE 기술을 사용하는 모든 AEM 고객을 위해 Adobe이 직접 지원합니다. 다음을 참조하십시오. [Adobe Experience Manager에 대한 Java™ 지원 정책](assets/Java_Policy_for_Adobe_Experience_Manager.pdf).
   **중요: Java™ 11 Oracle은 2026년 9월까지 최소 지원됩니다. oracle Java™ 17에 대한 지원이 준비중입니다.**

1. IBM® JRE는 WebSphere® Application Server와만 지원됩니다.

1. Azul Zulu OpenJDK LTS 버전은 버전 6.5 SP9부터 온-프레미스 AEM 배포에 대해 지원됩니다. Azul Zulu JDK LTS 버전의 지원 및 배포는 Adobe 고객이 Azul에서 직접 라이선스를 받아야 합니다.


### 스토리지 및 지속성 {#storage-persistence}

Adobe Experience Manager 저장소를 배포하기 위한 다양한 옵션이 있습니다. 지원되는 기술 및 스토리지 옵션에 대해서는 다음 목록을 참조하십시오.

| **플랫폼** | **설명** | **지원 수준** |
|---|---|---|
| **TAR 파일이 포함된 파일 시스템** `[1]` | 저장소 | A: 지원됨 |
| **데이터 스토어가 있는 파일 시스템** `[1]` | 바이너리 | A: 지원됨 |
| 파일 시스템의 TAR 파일에 바이너리 저장 `[1]` | 바이너리 | Z: 프로덕션에 지원되지 않음 |
| Amazon S3 | 바이너리 | A: 지원됨 |
| Microsoft® Azure Blob 저장소 | 바이너리 | A: 지원됨 |
| MongoDB Enterprise 6.0 | 저장소 | A: 지원됨 `[3, 4]` |
| MongoDB Enterprise 5.0 | 저장소 | A: 지원됨 `[3, 4]` |
| MongoDB Enterprise 4.4 | 저장소 | A: 지원됨 `[2, 3, 4, 7]` |
| MongoDB Enterprise 4.2 | 저장소 | A: 지원됨 `[2, 3, 4, 7]` |
| MongoDB Enterprise 4.0 | 저장소 | Z: 지원되지 않음 |
| MongoDB Enterprise 3.6 | 저장소 | Z: 지원되지 않음 |
| MongoDB Enterprise 3.4 | 저장소 | Z: 지원되지 않음 |
| IBM® DB2® 10.5 | 저장소 및 Forms 데이터베이스 | R: 제한된 지원 `[5]` |
| Oracle 데이터베이스 12c (12.1.x) | 저장소 및 Forms 데이터베이스 | R: 제한된 지원 |
| Microsoft® SQL Server 2016 | Forms 데이터베이스 | A: 지원됨 |
| **Apache Lucene(Quickstart 내장)** | 검색 서비스 | A: 지원됨 |
| Apache Solr | 검색 서비스 | A: 지원됨 |

1. &#39;파일 시스템&#39;에는 POSIX와 호환되는 블록 저장소가 포함되어 있습니다. 네트워크 스토리지 기술을 포함합니다. 파일 시스템 성능이 달라질 수 있으며 전체 성능에 영향을 줄 수 있습니다. 네트워크/원격 파일 시스템으로 테스트 AEM을 로드합니다.
1. MongoDB Enterprise 버전 4.2 및 4.4에는 AEM 6.5 SP9 이상이 필요합니다.
1. MongoDB 분할은 AEM에서 지원되지 않습니다.
1. MongoDB 스토리지 엔진 WiredTiger는 만 지원됩니다.
1. AEM Forms 업그레이드 고객을 위해 지원됩니다. 새 설치에서는 지원되지 않습니다.
1. AEM Forms에만 적용 가능:
   * oracle 데이터베이스 12c에 대한 지원이 제거되었으며 Oracle 데이터베이스 19c에 대한 지원이 추가되었습니다.
   * Microsoft® SQL Server 2016에 대한 지원이 제거되었으며 Microsoft® SQL Server 2019에 대한 지원이 추가되었습니다.
1. AEM Forms에서는 지원되지 않습니다.

>[!NOTE]
>
>다음을 참조하십시오 [커뮤니티 배포](/help/communities/deploy-communities.md) AEM Communities 기능에 대한 추가 정보.

>[!NOTE]
>
>MongoDB는 타사 소프트웨어 프로그램이며 AEM 라이센스 패키지에는 포함되어 있지 않습니다. 자세한 내용은 [MongoDB 라이선스 정책](https://www.mongodb.com/licensing/server-side-public-license/faq) 페이지를 가리키도록 업데이트하는 중입니다.
>
>MongoDB를 사용하여 AEM Adobe 배포를 최대한 활용하려면 MongoDB Enterprise 버전에 라이선스를 부여하여 전문적인 지원을 받는 것이 좋습니다. 다음을 참조하십시오 [권장 배포](/help/sites-deploying/recommended-deploys.md#prerequisites-and-recommendations-when-deploying-aem-with-mongomk) 추가 정보.
>
>라이센스에는 작성자 또는 게시 배포에 사용할 수 있는 하나의 기본 인스턴스와 두 개의 보조 인스턴스로 구성된 표준 복제본 세트가 포함되어 있습니다.
>
>MongoDB에서 작성자와 게시를 모두 실행하려는 경우 두 개의 별도 라이선스를 구입해야 합니다.
>
>Adobe 고객 지원 센터는 AEM에서 MongoDB 사용과 관련된 자격 부여 문제를 지원합니다.
>
>자세한 내용은 Adobe Experience Manager 페이지](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)용 MongoDB를 [참조하세요.

>[!NOTE]
>
>위에 나열된 대로 지원되는 관계형 데이터베이스는 서드파티 소프트웨어이며 AEM 라이선싱 패키지에 포함되어 있지 않습니다.
>
>지원되는 관계형 데이터베이스로 AEM 6.5를 실행하려면 데이터베이스 공급업체와의 별도의 지원 계약이 필요합니다. Adobe 고객 지원 센터는 AEM 6.5에서 관계형 데이터베이스 사용과 관련된 자격 문제를 지원합니다.
>
>**대부분의 관계형 데이터베이스는 현재 AEM 6.5의 Level-R 내에서 지원되며, 위의 Level-R 설명에 나와 있는 대로 지원 기준과 지원 프로그램이 제공됩니다.**

### 서블릿 엔진 / 애플리케이션 서버 {#servlet-engines-application-servers}

Adobe Experience Manager은 독립형 서버(quickstart JAR 파일)로 실행하거나 타사 애플리케이션 서버(WAR 파일) 내의 웹 애플리케이션으로 실행할 수 있습니다.

필요한 최소 서블릿 API 버전은 서블릿 3.1입니다.

| Platform | 지원 수준 |
|---|---|
| **Quickstart 내장 서블릿 엔진(Jetty 9.4)** | A: 지원됨 |
| Oracle WebLogic Server 12.2(12cR2) | Z: 지원되지 않음 |
| 웹 프로필 7.0 및 IBM® JRE 1.8을 사용한 IBM® WebSphere® Application Server Continuous Delivery(LibertyProfile) | R: 신규 계약에 대한 제한된 지원 `[2]` |
| IBM® WebSphere® Application Server 9.0 및 IBM® JRE 1.8 | R: 신규 계약에 대한 제한된 지원 `[1]` `[2]` |
| Apache Tomcat 8.5.x | R: 신규 계약에 대한 제한된 지원 `[2]` |
| JBoss® 애플리케이션 서버와 JBoss® EAP 7.2.x | Z: 지원되지 않음 |
| JBoss® 애플리케이션 서버와 JBoss® EAP 7.1.4 | R: 신규 계약에 대한 제한된 지원 `[1]` `[2]` |
| JBoss® 애플리케이션 서버와 JBoss® EAP 7.0.x | Z: 지원되지 않음 |

1. AEM Forms을 사용하는 배포에 권장됩니다.
1. 애플리케이션 서버에서 AEM 6.5 배포를 시작하면 제한된 지원으로 이동합니다. 기존 고객은 AEM 6.5로 업그레이드하고 애플리케이션 서버를 계속 사용할 수 있습니다. 신규 고객의 경우 위의 Level-R 설명에 명시된 대로 지원 기준 및 지원 프로그램을 제공합니다.
1. 적용 가능한 AEM Forms만:
   * JBoss® EAP 7.1.4에 대한 지원을 제거하고 JBoss® EAP 7.4.10에 대한 지원을 추가했습니다.

### 서버 운영 체제 {#server-operating-systems}

Adobe Experience Manager은 프로덕션 환경을 위해 다음 서버 플랫폼과 함께 작동합니다.

| **플랫폼** | **지원 수준** |
|---|---|
| **Linux®, Red Hat® 배포 기반** | A: 지원됨 `[1]` `[3]` |
| Debian 배포 기반 Linux®에는 다음이 포함됩니다. 우분투 | A: 지원됨 `[1]` `[2]` |
| Linux®, SUSE® 배포 기반 | A: 지원됨 `[1]` |
| Microsoft® Windows Server 2019 `[4]` | R: 신규 계약에 대한 제한된 지원 `[5]` |
| Microsoft® 윈도우 서버 2016 `[4]` | R: 신규 계약에 대한 제한된 지원 `[5]` |
| Microsoft® Windows Server 2012 R2 | Z: 지원되지 않음 |
| Oracle Solaris™ 11 | Z: 지원되지 않음 |
| IBM® AIX® 7.2 | Z: 지원되지 않음 |

1. Linux® 커널 2.6, 3. x, 4. x, 5. x와 6. x에는 Red Hat® Enterprise Linux®, CentOS, Oracle Linux® 및 Amazon Linux®를 비롯한 Red Hat 배포판의 파생물이 포함되어 ®. AEM Forms 추가 기능 기능은 CentOS 7, Red Hat® Enterprise Linux® 7, Red Hat® Enterprise Linux® 8 및 Red Hat® Enterprise Linux® 9에서만 지원됩니다.
1. AEM Forms은 Ubuntu 20.04 LTS에서 지원됩니다.
1. Adobe Managed Services에서 지원하는 Linux® 배포.

   >[!NOTE]
   >
   >Linux 기반 서버(OSGI 및 JEE 스택)의 경우 AEM Forms 추가 기능에는 다음과 같은 런타임 종속성이 필요합니다.
   >* glibc.x86_64 (2.17-196)
   >* libX11.x86_64 (1.6.7-4)
   >* zlib.x86-64 (1.2.7-17)
   >* libxcb.x86_64(1.13-1.el7)
   >* libXau.x86_64(1.0.8-2.1.el7)

1. Microsoft® Windows 프로덕션 배포는 6.5로 업그레이드하는 고객 및 비프로덕션 사용을 위해 지원됩니다. AEM Sites 및 자산에 대한 새 배포는 요청 시 수행됩니다.
1. AEM Forms은 지원 수준 R 제한 없이 Microsoft® Window Server에서 지원됩니다.
1. AEM Forms에서 Microsoft® Windows Server 2016에 대한 지원이 제거되었습니다.

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

클라우드 기반 환경의 경우 AEM 제품 라인의 최신 오퍼링인 Adobe Experience Manager as a Cloud Service을 검토하십시오. 다음을 참조하십시오 [Adobe Experience Manager as a Cloud Service 설명서](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=ko-KR) 을 참조하십시오.

또한 Adobe은 Azure 또는 AWS에 AEM을 배포할 수 있는 Adobe Managed Services을 제공합니다. Adobe Managed Services은 이러한 클라우드 컴퓨팅 환경에서 AEM을 배포하고 운영하는 경험과 기술을 전문가에게 제공합니다. 다음을 참조하십시오 [Managed Services Adobe에 대한 추가 설명서](https://business.adobe.com/products/experience-manager/managed-services.html?aemClk=t).

Azure나 AWS 또는 기타 클라우드 컴퓨팅 환경에 AEM을 배포하는 다른 모든 경우에는 Adobe의 지원이 가상 컴퓨팅 환경에 포함됩니다. 해당 가상 환경은 이 페이지에 나열된 기술 사양을 준수하여 실행되어야 합니다. 이러한 클라우드 환경에서 실행되는 AEM과 관련하여 보고된 문제는 클라우드 컴퓨팅 환경과 관련된 클라우드 서비스와 별도로 재현할 수 있어야 합니다. 즉, Azure Blob 저장 공간 또는 AWS S3 등 이 페이지에 나열된 기술 요구 사항의 일부로 클라우드 서비스가 지원되지 않는 경우.

Adobe Managed Services 외부에 있는 Azure 또는 AWS에 AEM을 배포하는 방법에 대한 권장 사항의 경우 Adobe은 클라우드 공급자와 직접 작업하는 것을 권장합니다. 또는 선택한 클라우드 환경에서의 AEM 배포를 지원하는 Adobe 파트너와 협력합니다. 선택한 클라우드 공급업체 또는 파트너는 특정 성능, 로드, 확장성 및 보안 요구 사항을 충족하도록 아키텍처 크기 조정 사양, 설계 및 구현을 담당합니다.

### Dispatcher 플랫폼(웹 서버) {#dispatcher-platforms-web-servers}

Dispatcher는 캐싱 및 로드 밸런싱 구성 요소입니다. [최신 Dispatcher 버전 다운로드](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html). Experience Manager 6.5에는 Dispatcher 버전 4.3.2 이상이 필요합니다.

다음 웹 서버는 Dispatcher 버전 4.3.2에서 사용할 수 있습니다.

| Platform | 지원 수준 |
|---|---|
| **Apache httpd 2.4.x** `[1,2]` | A: 지원됨 |
| Microsoft® IIS 10(인터넷 정보 서버) | A: 지원됨 |
| Microsoft® IIS 8.5(인터넷 정보 서버) | Z: 지원되지 않음 |

1. Apache httpd 소스 코드를 기반으로 구축된 웹 서버는 기반이 되는 httpd 버전만큼 많은 지원을 제공합니다. 확실하지 않은 경우 Adobe에게 각 서버 제품과 관련된 지원 수준을 확인하도록 요청하십시오. 다음과 같은 경우:

   1. HTTP 서버는 공식 Apache 소스 배포만 사용하여 빌드되었습니다. 또는
   1. HTTP 서버는 실행 중인 운영 체제의 일부로 전달되었습니다. 예: IBM® HTTP 서버, Oracle HTTP 서버

1. Dispatcher는 Windows 운영 체제용 Apache 2.4.x에서 사용할 수 없습니다.

## 지원되는 클라이언트 플랫폼 {#supported-client-platforms}

### 사용자 인터페이스 작성에 지원되는 브라우저 {#supported-browsers-for-authoring-user-interface}

Adobe Experience Manager 사용자 인터페이스는 다음 클라이언트 플랫폼에서 작동합니다. 모든 브라우저는 기본 플러그인 및 추가 기능 세트로 테스트됩니다.

AEM 사용자 인터페이스는 더 큰 화면(일반적으로 노트북 및 데스크탑 컴퓨터)과 태블릿 폼 팩터(예: Apple iPad 또는 Microsoft® 표면)에 최적화되어 있습니다. 휴대폰 폼 팩터는 지원되지 않습니다.

>[!NOTE]
>
>**빠른 릴리스 주기를 사용하는 브라우저 지원:**
>
>Mozilla Firefox, Google Chrome 및 Microsoft® Edge 릴리스 업데이트는 몇 개월마다 업데이트됩니다. Adobe은 이러한 브라우저의 향후 버전에 대해 아래에 명시된 대로 지원 수준을 유지하기 위해 Adobe Experience Manager에 대한 업데이트를 제공하기로 약속했습니다.

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
   <td>Microsoft® Edge (Evergreen)</td>
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

1. Firefox [의 확장 지원 릴리스 mozilla.org 에서 더 알아보기](https://www.mozilla.org/en-US/firefox/enterprise/)
1. Apple iPad 지원

### 웹 사이트에 대해 지원되는 브라우저 {#supported-browsers-for-websites}

일반적으로 AEM Sites에서 렌더링하는 웹 사이트에 대한 브라우저 지원은 AEM 페이지 템플릿, 디자인 및 구성 요소 출력의 구현에 따라 다르며, 따라서 이러한 부분을 구현하는 당사자의 통제 하에 있습니다.

### WebDAV 클라이언트 {#webdav-clients}

**Microsoft® Windows 7+**

SSL로 보호되지 않는 AEM 인스턴스에 Microsoft® Windows 7+를 연결할 때 Windows에서 비보안 네트워크를 통한 기본 인증을 활성화해야 합니다. WebClient의 Windows 레지스트리를 변경해야 합니다.

1. 레지스트리 하위 키를 찾습니다.

   * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters

1. 2 이상의 값을 사용하여 BasicAuthLevel 레지스트리 항목을 이 하위 키에 추가합니다.

## 추가 플랫폼 노트 {#additional-platform-notes}

이 섹션에서는 Adobe Experience Manager 및 해당 추가 기능 실행에 대한 특수 참고 사항과 보다 자세한 정보를 제공합니다.

### IPv4 및 IPv6 {#ipv-and-ipv}

Adobe Experience Manager의 모든 요소(인스턴스, Dispatcher)는 IPv4 및 IPv6 네트워크 모두에 설치할 수 있습니다.

특별한 구성이 필요하지 않으므로 작동이 원활합니다. 필요한 경우 네트워크 유형에 적합한 포맷 사용을 사용하여 IP 주소를 지정합니다.

IP 주소를 지정해야 하는 경우 필요에 따라 다음 중에서 선택할 수 있습니다.

* IPv6 주소입니다. 예, `https://[ab12::34c5:6d7:8e90:1234]:4502`

* IPv4 주소입니다. 예, `https://123.1.1.4:4502`

* 서버 이름. 예, `https://www.yourserver.com:4502`

* 의 기본 대/소문자 `localhost` 는 IPv4 및 IPv6 네트워크 설치 모두에 대해 해석됩니다. 예, `https://localhost:4502`

### AEM Dynamic Media 추가 기능 요구 사항 {#requirements-for-aem-dynamic-media-add-on}

AEM Dynamic Media은 기본적으로 비활성화되어 있습니다. 자세한 내용은 여기 를 참조하십시오 [Dynamic Media 활성화](/help/assets/config-dynamic.md#enabling-dynamic-media).

Dynamic Media이 활성화되면 다음과 같은 추가 기술 요구 사항이 적용됩니다.

>[!NOTE]
>
>이러한 시스템 요구 사항 **전용** Dynamic Media - 하이브리드 모드를 사용하는 경우 적용하십시오. Dynamic Media - 하이브리드 모드에는 특정 운영 체제에서만 인증되는 내장 이미지 서버가 있습니다.
>
>Dynamic Media - Scene7 모드를 실행하는 Dynamic Media 고객의 경우 (즉, **dynamicmedia_scene7** 실행 모드), 추가적인 시스템 요구 사항은 없으며, AEM과 동일한 시스템 요구 사항만 있습니다. Dynamic Media - Scene7 모드 아키텍처는 AEM에 임베드된 서비스가 아닌 클라우드 기반 이미지 서비스를 사용합니다.

#### 하드웨어 {#hardware}

Linux® 및 Windows 모두에 다음 하드웨어 요구 사항을 적용할 수 있습니다.

* Intel Xeon® 또는 AMD® Opteron CPU(최소 4개 코어)
* 최소 16GB RAM

#### Linux® {#linux}

Linux®에서 Dynamic Media을 사용하는 경우 다음 전제 조건을 충족해야 합니다.

* Red Hat® Enterprise 7 이상(최신 수정 패치 포함)
* 비트 운영 체제
* 스와핑 비활성화됨(권장)
* SELinux가 비활성화되었습니다(다음 참고 사항 참조)

>[!NOTE]
>
>로케일이 LC_CTYPE이 다음과 같지 않도록 설정된 경우 `en_US.UTF-8`: Dynamic Media이 작동하지 않습니다. 해당 값이 무엇인지 보려면 명령 프롬프트에서 &quot;locale&quot;을 입력하십시오. 제대로 설정되지 않은 경우 AEM을 실행하기 전에 &quot;export LC_CTYPE=&quot;을 입력하여 LC_CTYPE 환경 변수를 빈 문자열로 설정합니다.

>[!NOTE]
>
>**SELinux 비활성화:** SELinux가 켜져 있으면 이미지 제공이 작동하지 않습니다. 이 옵션은 기본적으로 활성화되어 있습니다. 이 문제를 해결하려면 **/etc/selinux/config** 파일을 만들고 SELinux 값을 다음 위치에서 변경합니다.
>
>`SELINUX=enforcing` **끝** `SELINUX=disabled`

>[!NOTE]
>
>**NUMA 아키텍처:** AMD64 및 Intel® EM64T를 특징으로 하는 프로세서가 있는 시스템은 일반적으로 NUMA(Non-Uniform Memory Architecture) 플랫폼으로 구성됩니다. 즉, 커널은 하나의 메모리 노드를 구성하는 것이 아니라 부트 시에 여러 개의 메모리 노드를 구성한다.
>
>다중 노드 구성은 다른 노드가 소진되기 전에 하나 이상의 노드에서 메모리 소진을 초래할 수 있다. 메모리 소진이 발생하면 커널은 사용 가능한 메모리가 있더라도 프로세스(예: 이미지 서버 또는 플랫폼 서버)를 종료하기로 결정할 수 있습니다.
>
>Adobe Systems따라서 이러한 시스템을 실행하는 경우 커널이 이러한 프로세스를 종료하지 않도록 numa=off **부팅 옵션을 사용하여** NUMA를 끄는 것이 좋습니다.

>[!NOTE]
>
>**서버 호스트 이름을 확인해야 함:** 서버의 호스트 이름을 IP 주소로 확인할 수 있는지 확인하십시오. 가능하지 않은 경우 정규화된 호스트 이름과 IP 주소를 /etc/hosts에 **추가합니다.**
>
>`<ip address> <fully qualified hostname>`

#### Windows {#windows}

* 마이크로소프트® 윈도우 서버 2016
* 실제 메모리(RAM) 양의 두 배 이상에 해당하는 스왑 공간

Windows에서 Dynamic Media을 사용하려면 x64 및 x86용 Microsoft® Visual Studio 2010, 2013 및 2015 재배포 가능 패키지를 설치하십시오.

Windows x64의 경우

* https://www.microsoft.com/en-us/download/details.aspx?id=26999 에서 [Microsoft® Visual Studio 2010 재배포 가능 패키지 받기](https://www.microsoft.com/en-us/download/details.aspx?id=26999)
* https://www.microsoft.com/en-us/download/details.aspx?id=40784 에서 [Microsoft® Visual Studio 2013 재배포 가능 패키지 받기](https://www.microsoft.com/en-us/download/details.aspx?id=40784)
* https://www.microsoft.com/en-us/download/details.aspx?id=48145 에서 [Microsoft® Visual Studio 2015 재배포 가능 패키지 받기](https://www.microsoft.com/en-us/download/details.aspx?id=48145)

Windows x86의 경우:

* 다음에서 Microsoft® Visual Studio 2010 재배포 가능 패키지를 가져옵니다. [https://www.microsoft.com/en-us/download/details.aspx?id=26999](https://www.microsoft.com/en-us/download/details.aspx?id=26999)
* Microsoft® Visual Studio 2013 재배포 가능 위치: [https://www.microsoft.com/en-in/download/details.aspx?id=40769](https://www.microsoft.com/en-in/download/details.aspx?id=40769)
* https://www.microsoft.com/en-us/download/details.aspx?id=52685 에서 [Microsoft® Visual Studio 2015 재배포 가능 패키지 받기](https://www.microsoft.com/en-us/download/details.aspx?id=52685)

#### macOS {#macos}

* 10.9.x 이상
* 체험판 및 데모 목적으로만 지원됨

### AEM Forms PDF Generator 요구 사항 {#requirements-for-aem-forms-pdf-generator}

### PDF Generator 소프트웨어 지원 {#software-support-for-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>제품</strong></p> </th>
   <th><p><strong>PDF로 변환하기 위해 지원되는 형식</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2020 클래식 트랙</a> 최신 버전</td>
   <td>XPS, 이미지 형식(BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, DWG, DXF 및 DWF</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2017 클래식 트랙</a> 최신 버전(더 이상 사용되지 않음)</td>
   <td>XPS, 이미지 형식(BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, DWG, DXF 및 DWF</td>
  </tr>
  <tr>
   <td>마이크로소프트® 오피스 2019</td>
   <td>DOC, DOCX, XLS, XLSX, PPT, PPTX, RTF 및 TXT</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2016(더 이상 사용되지 않음)</td>
   <td>DOC, DOCX, XLS, XLSX, PPT, PPTX, RTF 및 TXT</td>
  </tr>
  <tr>
   <td>워드퍼펙트 2020<br /> </td>
   <td>WP, WPD</td>
  </tr>
  <tr>
   <td>Microsoft® Office Visio 2016(더 이상 사용되지 않음)<br /> </td>
   <td>VSD, VSDX</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2019<br /> </td>
   <td>PUB</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2016(더 이상 사용되지 않음)<br /> </td>
   <td>PUB</td>
  </tr>
  <tr>
   <td>Microsoft® Project 2016(더 이상 사용되지 않음)<br /> </td>
   <td>MPP</td>
  </tr>
  <tr>
   <td>오픈오피스 4.1.10</td>
   <td>ODT, ODP, ODS, ODG, ODF, SXW, SXI, SXC, SXD, XLS, XLSX, DOC, DOCX, PPT, PPTX, 이미지 형식(BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, RTF, TXT</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.2(더 이상 사용되지 않음)</td>
   <td>ODT, ODP, ODS, ODG, ODF, SXW, SXI, SXC, SXD, XLS, XLSX, DOC, DOCX, PPT, PPTX, 이미지 형식(BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, RTF, TXT</td>
  </tr>  
 </tbody>
</table>

>[!NOTE]
>
>PDF Generator은 지원되는 운영 체제 및 애플리케이션의 영어, 프랑스어, 독일어 및 일본어 버전만 지원합니다.
>
>또한,
>
>* PDF Generator을 사용하려면 32비트 버전의 [Acrobat 2020 classic track 버전 20.004.30006](https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html) 또는 Acrobat 2017 버전 17.011.30078을 사용하여 변환을 수행할 수 있습니다.
>* OpenOffice의 PDF Generator 전환은 Windows 및 Linux®에서만 지원됩니다.
>* PDF Generator은 Microsoft® Office Professional Plus의 32비트 정품 버전 및 Windows 운영 체제에서 전환하는 데 필요한 기타 소프트웨어만 지원합니다.
>* PDF Generator은 Linux® 운영 체제에서 32비트 및 64비트 버전의 OpenOffice를 지원합니다.
>* PDF Generator은 Microsoft® Office 365를 지원하지 않습니다.
>* OCR PDF, Optimize PDF 및 Export PDF 기능은 Windows에서만 지원됩니다.
>* Acrobat 버전은 PDF Generator 기능을 사용할 수 있도록 AEM Forms과 번들로 제공됩니다. AEM Forms 라이선스가 있는 동안 프로그래밍 방식으로 AEM Forms에서만 번들 버전에 액세스하여 AEM Forms PDF Generator과 함께 사용합니다. 자세한 내용은 배포에 따른 AEM Forms 제품 설명([On-Premise](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html) 또는 [Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html))
>* PDF Generator 서비스는 Microsoft® Windows 10을 지원하지 않습니다.
>* PDF Generator이 Microsoft® Visio 2019를 사용하여 파일을 변환하지 못했습니다. Microsoft® Visio 2016을 계속 사용하여 변환할 수 있습니다 `.VSD` 및 `.VSDX` 파일.
>* PDF Generator이 Microsoft® Project 2019를 사용하여 파일을 변환하지 못했습니다. Microsoft® Project 2016을 계속 사용하여 변환할 수 있습니다 `.VSD` 및 `.VSDX` 파일.
>

### AEM Forms Designer 요구 사항 {#requirements-for-aem-forms-designer}

* Microsoft® Windows® 2016 Server, Microsoft® Windows® 2019 Server, Microsoft® Windows® 10 또는 Windows® 11
* PAE, NX 및 SSE2를 지원하는 1GHz 이상의 프로세서.
* 32비트 OS의 경우 1GB RAM 또는 64비트 OS의 경우 2GB RAM
* 32비트의 경우 16GB 디스크 공간 또는 64비트 OS의 경우 20GB 디스크 공간
* 그래픽 메모리 - 128MB GPU(256MB 권장)
* 2.35GB의 사용 가능한 하드 디스크 공간
* 1024 X 768픽셀 이상의 모니터 해상도
* 비디오 하드웨어 가속(선택 사항)
* Acrobat Pro DC, Acrobat Standard DC 또는 Adobe Acrobat Reader DC
* Designer를 설치하기 위한 관리자 권한
* 32비트 AEM Forms Designer용 Microsoft Visual C++ 2019(VC 14.28 이상) 32비트 런타임
* 64비트 AEM Forms Designer용 Microsoft Visual C++ 2019(VC 14.28 이상) 64비트 런타임(OSGI 및 JEE 스택 모두 해당)

[AEM Forms 디자이너 설치 및 구성](/help/forms/using/installing-configuring-designer.md)

### AEM Assets XMP 메타데이터 쓰기 되돌리기 요구 사항 {#requirements-for-aem-assets-xmp-metadata-write-back}

XMP 원본에 쓰기 지원되며 다음 플랫폼 및 파일 형식에 사용할 수 있습니다.

* **운영 체제:**

   * Linux®(64비트 시스템에서 32비트 및 32비트 애플리케이션 지원) 32비트 클라이언트 라이브러리를 설치하는 단계는 [64비트 Red Hat® Linux®에서 XMP 추출 및 다시 쓰기를 활성화하는 방법](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).

   * Windows Server
   * macOS X (64비트)

* **파일 형식**: JPEG, PNG, TIFF, PDF, INDD, AI 및 EPS.

### Linux®에서 메타데이터가 많은 자산을 처리하기 위한 AEM Assets 요구 사항 {#assetsonlinux}

XMPFilesProcessor 프로세스가 작동하려면 GLIBC_2.14 라이브러리가 필요합니다. GLIBC_2.14가 포함된 Linux® 커널을 사용합니다(예: Linux® 커널 버전 3.1.x). PSD 파일과 같이 대량의 메타데이터가 포함된 에셋을 처리하는 경우 성능이 향상됩니다. 이전 버전의 GLIBC를 사용하면 로 시작하는 로그에 오류가 발생합니다. `com.day.cq.dam.core.impl.handler.xmp.NCommXMPHandler Failed to read XMP`.
