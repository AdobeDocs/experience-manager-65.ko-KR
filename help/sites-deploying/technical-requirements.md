---
title: 기술 요구 사항
seo-title: 기술 요구 사항
description: AEM에서 지원되는 클라이언트 및 서버 플랫폼 목록입니다.
seo-description: AEM에서 지원되는 클라이언트 및 서버 플랫폼 목록입니다.
uuid: 597f8fc1-9ac7-458d-a7c1-f576dd0f189b
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
discoiquuid: 16c7a97d-884a-447e-9aad-18a2db1bda1d
docset: aem65
translation-type: tm+mt
source-git-commit: 7065a6b984afb18c188acd848b9b77da7da67749
workflow-type: tm+mt
source-wordcount: '3118'
ht-degree: 1%

---


# 기술 요구 사항{#technical-requirements}

Adobe은 이 문서의 다음 정보에 따라 플랫폼에서 Adobe Experience Manager(AEM)을 지원합니다.

플랫폼과 관련된 문제는 플랫폼 공급업체에 문의하십시오.

>[!NOTE]
>
>AEM을 설치하는 플랫폼에 따라 사용자 관리에 대한 다양한 요구 사항 세트가 있을 수 있습니다.

## 전제 조건 {#prerequisites}

Adobe Experience Manager 설치를 위한 최소 요구 사항:

* 설치된 Java Platform, Standard Edition JDK 또는 기타 지원 [Java Virtual Machines](#java-virtual-machines)
* Experience Manager 빠른 시작 파일(독립 실행형 JAR 또는 웹 애플리케이션 배포 WAR)

### 최소 크기 지정 요구 사항 {#minimum-sizing-requirements}

Adobe Experience Manager 실행을 위한 최소 요구 사항:

* 설치 디렉토리의 5GB의 여유 디스크 공간
* 2GB 메모리

>[!NOTE]
>
>* 디지털 자산 사용 사례에는 더 많은 기본 메모리가 필요합니다. 자세한 내용은 [배포 및 유지 관리](/help/sites-deploying/deploy.md#default-local-install)를 참조하십시오.
>* [AEM Forms Add-](/help/forms/using/installing-configuring-aem-forms-osgi.md) On 패키지의 경우 15GB의 임시 공간이 필요합니다.

>



자세한 내용은 [하드웨어 크기 조정 지침](/help/managing/hardware-sizing-guidelines.md)을 참조하십시오.

### 지원 수준 {#support-levels}

이 문서에는 Adobe Experience Manager에 대해 지원되는 클라이언트 및 서버 플랫폼이 나와 있습니다. Adobe은 권장 구성 및 기타 구성을 위해 여러 수준의 지원을 제공합니다.

### 지원되는 구성 {#supported-configurations}

Adobe은 이러한 구성을 권장하며 표준 소프트웨어 유지 관리 계약의 일부로 완벽한 지원을 제공합니다.

<table>
 <tbody>
  <tr>
   <td>지원 수준</td>
   <td>설명<br /> </td>
  </tr>
  <tr>
   <td><strong>A:지원됨</strong></td>
   <td>Adobe은 이 구성에 대한 모든 지원 및 유지 관리를 제공합니다. 이 구성은 Adobe의 품질 보증 프로세스로 다룹니다.</td>
  </tr>
  <tr>
   <td><strong>R:제한된 지원</strong></td>
   <td>고객의 성공적인 프로젝트 진행을 위해 Adobe은 특정 조건이 충족되어야 하는 제한된 지원 프로그램 내에서 모든 지원을 제공합니다. R 수준 지원은 공식적인 고객 요청과 Adobe의 확인을 필요로 합니다. 자세한 내용은 Adobe 고객 지원 센터에 문의하십시오.</td>
  </tr>
 </tbody>
</table>

### 지원되지 않는 구성 {#unsupported-configurations}

| 지원 수준 | 설명 |
|---|---|
| **Z:지원되지 않음** | 구성이 지원되지 않습니다. Adobe은 구성이 작동되는지 여부에 대해 아무런 설명을 하지 않으며, 지원하지 않습니다. |

## 지원되는 플랫폼 {#supported-platforms}

### Java 가상 컴퓨터 {#java-virtual-machines}

응용 프로그램을 실행하려면 Java Virtual Machine이 필요하며, JDK(Java Development Kit) 배포에서 제공됩니다.

Adobe Experience Manager은 다음 버전의 Java 가상 시스템으로 작동합니다.

>[!CAUTION]
>
>프로덕션 환경의 안전과 보안을 보장하고 최신 Java 업데이트를 설치하려면 Java 공급업체의 보안 게시판을 추적하는 것이 좋습니다.

<table>
 <tbody>
  <tr>
   <td>플랫폼</td>
   <td>지원 수준</td>
  </tr>
  <tr>
   <td>Oracle Java SE 12 JDK [1]</td>
   <td>Z:지원되지 않음 </td>
  </tr>
  <tr>
   <td><strong>Oracle Java SE 11 JDK - 64비트</strong></td>
   <td>A:지원됨</td>
  </tr>
  <tr>
   <td>Oracle Java SE 10 JDK [1]</td>
   <td>Z:지원되지 않음 </td>
  </tr>
  <tr>
   <td>Oracle Java SE 9 JDK [1]</td>
   <td>Z:지원되지 않음</td>
  </tr>
  <tr>
   <td>Oracle Java SE 8 JDK - 64비트</td>
   <td>A:지원되는 [3]</td>
  </tr>
  <tr>
   <td>IBM J9 VM - 빌드 2.9, JRE 1.8.0 [2]</td>
   <td>A:지원됨</td>
  </tr>
  <tr>
   <td>IBM J9 VM - 빌드 2.8, JRE 1.8.0 [2]</td>
   <td>A:지원됨</td>
  </tr>
 </tbody>
</table>

1. Oracle은 Oracle Java SE 제품에 대한 &quot;장기 지원&quot;(LTS) 모델로 이동되었습니다. Java 9, Java 10 및 Java 12는 Oracle이 출시한 LTS가 아닌 버전입니다([Oracle Java SE 지원 로드맵](https://www.oracle.com/technetwork/java/eol-135779.html) 참조). 프로덕션 환경에서 AEM을 배포하기 위해 Adobe은 Java의 LTS 릴리스에 대해서만 지원을 제공합니다.

1. IBM JRE는 WebSphere Application Server와 함께 지원됩니다.
1. 공개 업데이트가 종료된 이후에도 LTS 릴리스의 모든 유지 관리 업데이트를 비롯한 Oracle Java SE JDK의 지원 및 배포는 Oracle Java SE 기술을 사용하는 모든 AEM 고객을 위해 Adobe에서 직접 지원됩니다. 자세한 내용은 Adobe Experience Manager Q&amp;A](assets/adobe-oracle-java-license-agreement.pdf)에 대한 [Oracle Java 지원을 참조하십시오.

### 저장 및 지속성 {#storage-persistence}

Adobe Experience Manager 저장소를 배포하는 다양한 옵션이 있습니다. 지원되는 기술 및 스토리지 옵션은 다음 목록을 참조하십시오.

| **플랫폼** | **설명** | **지원 수준** |
|---|---|---|
| **TAR 파일이 있는 파일 시스템** `[1]` | 저장소 | A:지원됨 |
| **데이터 저장소가 있는 파일 시스템** `[1]` | 이진 파일 | A:지원됨 |
| 파일 시스템 `[1]`의 TAR 파일에 바이너리 저장 | 이진 파일 | Z:프로덕션에서 지원되지 않음 |
| Amazon S3 | 이진 파일 | A:지원됨 |
| Microsoft Azure Blob 저장소 | 이진 파일 | A:지원됨 |
| MongoDB Enterprise 4.0 | 저장소 | A:지원되는 `[2, 3]` |
| MongoDB Enterprise 3.6 | 저장소 | Z:지원되지 않음 |
| MongoDB Enterprise 3.4 | 저장소 | Z:지원되지 않음 |
| IBM DB2 10.5 | 저장소 및 Forms 데이터베이스 | R:제한된 지원 `[4]` |
| Oracle 데이터베이스 12c(12.1.x) | 저장소 및 Forms 데이터베이스 | R:제한된 지원 |
| Microsoft SQL Server 2016 | Forms 데이터베이스 | A:지원됨 |
| **Apache Lucene(Quickstart 내장)** | 검색 서비스 | A:지원됨 |
| Apache Solr | 검색 서비스 | A:지원됨 |

1. &#39;파일 시스템&#39;에는 POSIX 호환 블록 스토리지가 포함됩니다. 여기에는 네트워크 스토리지 기술이 포함됩니다. 파일 시스템 성능은 다를 수 있으며 전반적인 성능에 영향을 미칠 수 있습니다. 네트워크/원격 파일 시스템과 함께 테스트 AEM을 로드하는 것이 좋습니다.
1. MongoDB Sharding은 AEM에서 지원되지 않습니다.
1. MongoDB Storage Engine WiredTiger만 지원됩니다.
1. AEM Forms 업그레이드 고객을 위한 지원 새 설치에는 지원되지 않습니다.

>[!NOTE]
>
>AEM Communities 기능에 대한 자세한 내용은 [커뮤니티 배포](/help/communities/deploy-communities.md)를 참조하십시오.

>[!NOTE]
>
>MongoDB는 타사 소프트웨어이며 AEM 라이선스 패키지에 포함되어 있지 않습니다. 자세한 내용은 [MongoDB 라이선스 정책](https://www.mongodb.org/about/licensing/) 페이지를 참조하십시오.
>
>MongoDB를 사용하여 AEM 배포를 최대한 활용하려면 MongoDB Enterprise 버전의 라이선스를 라이선싱하여 전문가 지원을 받을 것을 권장합니다. 자세한 내용은 [권장 배포](/help/sites-deploying/recommended-deploys.md#prerequisites-and-recommendations-when-deploying-aem-with-mongomk)를 참조하십시오.
>
>라이센스에는 표준 복제본 세트가 포함되어 있으며, 이는 작성자 또는 게시 배포에 사용할 수 있는 1개의 기본 인스턴스와 2개의 보조 인스턴스로 구성됩니다.
>
>MongoDB에서 작성자와 게시를 모두 실행하려면 별도의 두 개의 라이선스를 구입해야 합니다.
>
>Adobe 고객 지원 센터는 AEM에서 MongoDB 사용과 관련된 자격 있는 문제를 지원합니다.
>
>자세한 내용은 Adobe Experience Manager용 [MongoDB 페이지](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)를 참조하십시오.

>[!NOTE]
>
>위에 나열된 지원 관계형 데이터베이스는 타사 소프트웨어이며 AEM 라이선스 패키지에 포함되어 있지 않습니다.
>
>지원되는 관계형 데이터베이스를 사용하여 AEM 6.5를 실행하려면 데이터베이스 공급업체와의 별도의 지원 계약이 필요합니다. Adobe 고객 지원 센터는 AEM 6.5에서 관계형 데이터베이스 사용과 관련된 자격 있는 문제를 해결합니다.
>
>**대부분의 관계형 데이터베이스는 현재 AEM 6.5의 Level-R에서 지원됩니다. Level-R 설명에 언급된 지원 기준과 지원 프로그램이 포함되어 있습니다.**

### 서블릿 엔진/응용 프로그램 서버 {#servlet-engines-application-servers}

Adobe Experience Manager은 독립 실행형 서버(quickstart JAR 파일)로 실행하거나 타사 애플리케이션 서버(WAR 파일)에서 웹 애플리케이션으로 실행할 수 있습니다.

필요한 최소 서블릿 API 버전은 Servlet 3.1입니다.

| 플랫폼 | 지원 수준 |
|---|---|
| **Quickstart 내장된 Servlet Engine(Jetty 9.4)** | A:지원됨 |
| Oracle WebLogic Server 12.2(12cR2) | Z:지원되지 않음 |
| 웹 프로필 7.0 및 IBM JRE 1.8이 포함된 IBM WebSphere Application Server Continuous Delivery(LibertyProfile) | R:새 계약에 대한 제한된 지원 `[2]` |
| IBM WebSphere Application Server 9.0 및 IBM JRE 1.8 | R:새 계약에 대한 제한된 지원 `[1]` `[2]` |
| Apache Tomcat 8.5.x | R:새 계약에 대한 제한된 지원 `[2]` |
| JBoss 애플리케이션 서버가 있는 JBoss EAP 7.2.x | Z:지원되지 않음 |
| JBoss 응용 프로그램 서버가 있는 JBoss EAP 7.1.4 | R:새 계약에 대한 제한된 지원 `[1]` `[2]` |
| JBoss 애플리케이션 서버가 있는 JBoss EAP 7.0.x | Z:지원되지 않음 |

1. AEM Forms과 함께 배포하는 경우 권장됩니다.
1. 응용 프로그램 서버에 AEM 6.5 배포를 시작하면 제한된 지원으로 이동합니다. 기존 고객은 AEM 6.5로 업그레이드하여 애플리케이션 서버를 계속 사용할 수 있습니다. 신규 고객의 경우 위의 Level-R 설명에 명시된 지원 기준과 지원 프로그램을 함께 받게 됩니다.

### 서버 운영 체제 {#server-operating-systems}

Adobe Experience Manager은 프로덕션 환경에서 다음과 같은 서버 플랫폼과 연동됩니다.

| **플랫폼** | **지원 수준** |
|---|---|
| **Linux, Red Hat 배포 기반** | A:지원되는 `[1]` `[3]` |
| Linux, Debian 배포 기반 우분투 | A:지원되는 `[2]` |
| Linux, SUSE 배포 기반 | A:지원됨 |
| Microsoft Windows Server 2019 `[4]` | R:새로운 계약에 대한 제한된 지원 |
| Microsoft Windows Server 2016 `[4]` | R:새 계약에 대한 제한된 지원 `[5]` |
| Microsoft Windows Server 2012 R2 | Z:지원되지 않음 |
| Oracle Solaris 11 | Z:지원되지 않음 |
| IBM AIX 7.2 | Z:지원되지 않음 |

1. Linux Kernel 2.6, 3.x 및 4.x에는 Red Hat Enterprise Linux, CentOS, Oracle Linux, Amazon Linux 등 Red Hat 배포판에서의 파생물이 포함됩니다. AEM Forms 추가 기능은 CentOS 7 및 Red Hat Enterprise Linux 7에서만 지원됩니다.
1. AEM Forms은 Ubuntu 16.04에서만 지원됩니다.
1. Adobe Managed Services에서 지원되는 Linux 배포
1. Microsoft Windows 제작 배포는 6.5로 업그레이드하고 제작 과정 이외의 다른 사용자도 사용할 수 있습니다. 새로운 배포는 AEM Sites 및 자산에 대한 요청 시 가능합니다.
1. AEM Forms은 지원 수준 R 제한 없이 Microsoft Windows Server에서 지원됩니다.

### 가상 및 클라우드 컴퓨팅 환경 {#virtual-cloud-computing-environments}

Adobe Experience Manager은 Microsoft Azure 및 Amazon 웹 서비스(AWS)와 같은 클라우드 컴퓨팅 환경의 가상 컴퓨터에서 이 페이지에 나열된 기술 요구 사항을 준수하고 Adobe 표준 지원 약관에 따라 실행됩니다.

Adobe은 Azure 또는 AWS에 AEM을 배포하기 위해 Adobe Managed Services를 사용하는 것이 좋습니다. Adobe Managed Services는 이러한 클라우드 컴퓨팅 환경에서 AEM을 배포 및 운영하는 경험과 기술을 전문가에게 제공합니다. Adobe Managed Services[에 대한 추가 설명서를 참조하십시오.](https://www.adobe.com/marketing-cloud/enterprise-content-management/managed-services-cloud-platform.html?aemClk=t)

Azure 또는 AWS 또는 기타 클라우드 컴퓨팅 환경에 AEM을 배포하는 다른 모든 경우 Adobe의 지원이 이 페이지에 나열된 기술 사양에 따라 가상 컴퓨팅 환경에 포함됩니다. 클라우드 서비스가 Azure Blob 스토리지 또는 AWS S3와 같이 이 페이지에 나열된 기술 요구 사항의 일부로 특별히 지원되지 않는 한, 이러한 클라우드 환경에서 실행되는 AEM과 관련된 보고된 문제는 클라우드 컴퓨팅 환경 관련 클라우드 서비스와 독립적으로 재생산되어야 합니다.

Azure 또는 AWS에 AEM을 배포하는 방법에 대한 권장 사항은 Adobe Managed Services 외부에 있습니다. Adobe은 원하는 클라우드 환경에서 AEM 배포를 지원하는 클라우드 공급자나 Adobe 파트너와 직접 작업하는 것이 좋습니다. 선택한 클라우드 제공업체 또는 파트너는 고객의 특정 성능, 로드, 확장성 및 보안 요구 사항을 충족하기 위해 아키텍처의 크기 지정, 설계 및 구현에 대한 책임을 집니다.

### 발송자 플랫폼(웹 서버) {#dispatcher-platforms-web-servers}

디스패처는 캐싱 및 로드 밸런싱 구성 요소입니다. [최신 Dispatcher 버전을 다운로드합니다](https://helpx.adobe.com/experience-manager/dispatcher/release-notes.html). Experience Manager 6.5를 사용하려면 Dispatcher 버전 4.3.2 이상이 필요합니다.

다음 웹 서버는 Dispatcher 버전 4.3.2에서 사용할 수 있습니다.

| 플랫폼 | 지원 수준 |
|---|---|
| **Apache httpd 2.4.x** `[1,2]` | A:지원됨 |
| Microsoft IIS 10(인터넷 정보 서버) | A:지원됨 |
| Microsoft IIS 8.5(인터넷 정보 서버) | Z:지원되지 않음 |

1. Apache httpd 소스 코드를 기반으로 구축된 웹 서버는 해당 서버가 기반으로 하는 httpd 버전과 동일한 지원 수준을 갖게 됩니다. 확실하지 않은 경우 Adobe에 해당 서버 제품과 관련된 지원 수준의 확인을 요청하십시오. 다음 경우:

   1. HTTP 서버는 공식 Apache 소스 배포만을 사용하여 구축되었습니다.
   1. HTTP 서버가 실행 중인 운영 체제의 일부로 배달되었습니다. 예:IBM HTTP Server, Oracle HTTP Server

1. Dispatcher는 Windows 운영 체제용 Apache 2.4.x에서 사용할 수 없습니다.

## 지원되는 클라이언트 플랫폼 {#supported-client-platforms}

### 사용자 인터페이스 작성에 지원되는 브라우저 {#supported-browsers-for-authoring-user-interface}

Adobe Experience Manager 사용자 인터페이스는 다음 클라이언트 플랫폼에서 작동합니다. 모든 브라우저는 기본 플러그인 및 애드온으로 테스트됩니다.

AEM 사용자 인터페이스는 더 큰 스크린(일반적으로 노트북 및 데스크탑 컴퓨터) 및 태블릿 폼 팩터(예: Apple iPad 또는 Microsoft Surface)에 맞게 최적화되어 있습니다. 휴대폰 폼 팩터는 지원되지 않습니다.

>[!NOTE]
>
>**빠른 릴리스 주기 기반의 브라우저 지원:**
>
>Mozilla Firefox, Google Chrome 및 Microsoft Edge 릴리스는 몇 개월마다 업데이트됩니다. Adobe은 이러한 브라우저의 차기 버전과 함께 아래에 명시된 지원 수준을 유지하기 위해 Adobe Experience Manager에 대한 업데이트를 제공하기 위해 노력하고 있습니다.

<table>
 <tbody>
  <tr>
   <td><strong>브라우저</strong></td>
   <td><strong>UI 지원<br /> </strong></td>
   <td><strong>클래식 UI 지원</strong></td>
  </tr>
  <tr>
   <td><strong>Google Chrome(Evergreen)</strong></td>
   <td>A:지원됨</td>
   <td>A:지원됨</td>
  </tr>
  <tr>
   <td>Microsoft Edge(Evergreen)</td>
   <td>A:지원됨</td>
   <td>A:지원됨</td>
  </tr>
  <tr>
   <td>Microsoft Internet Explorer 11</td>
   <td>Z:지원되지 않음</td>
   <td>Z:지원되지 않음</td>
  </tr>
  <tr>
   <td>Mozilla Firefox(Evergreen)</td>
   <td>A:지원됨</td>
   <td>A:지원됨</td>
  </tr>
  <tr>
   <td>Mozilla Firefox 마지막 ESR [1]</td>
   <td>A:지원됨</td>
   <td>A:지원됨</td>
  </tr>
  <tr>
   <td>macOS 기반의 Apple Safari(Evergreen)</td>
   <td>A:지원됨</td>
   <td>A:지원됨</td>
  </tr>
  <tr>
   <td>macOS 기반의 Apple Safari 11.x</td>
   <td>Z:지원되지 않음</td>
   <td>Z:지원되지 않음</td>
  </tr>
  <tr>
   <td>iOS 12.x의 Apple Safari</td>
   <td>A:지원되는 [2]</td>
   <td>Z:지원되지 않음</td>
  </tr>
  <tr>
   <td>iOS 11.x의 Apple Safari</td>
   <td>Z:지원되지 않음</td>
   <td>Z:지원되지 않음</td>
  </tr>
 </tbody>
</table>

1. Firefox [의 ESR(Extended Support Release)에 대한 자세한 내용을 mozilla.org](https://www.mozilla.org/en-US/firefox/organizations/faq/)
1. Apple iPad 지원

### 지원되는 웹 사이트 브라우저 {#supported-browsers-for-websites}

일반적으로 AEM Sites에서 렌더링하는 웹 사이트에 대한 브라우저 지원은 AEM 페이지 템플릿, 디자인 및 구성 요소 출력 구현에 따라 다르므로 이러한 부분을 구현하는 당사자가 제어합니다.

### WebDAV 클라이언트 {#webdav-clients}

**Microsoft Windows 7+**

Microsoft Windows 7+와 SSL을 통해 보안이 유지되지 않는 AEM 인스턴스에 성공적으로 연결하려면 Windows에서 보안되지 않은 네트워크에 대한 기본 인증이 활성화되어 있어야 합니다. 이렇게 하려면 WebClient의 Windows 레지스트리를 변경해야 합니다.

1. 레지스트리 하위 키를 찾습니다.

   * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters

1. 2개 이상의 값을 사용하여 이 하위 키에 BasicAuthLevel 레지스트리 항목을 추가합니다.

Windows에서 WebDav 클라이언트의 응답을 향상시키려면 [Microsoft 지원 KB 2445570](https://support.microsoft.com/kb/2445570)을 참조하십시오.

## 추가 플랫폼 노트 {#additional-platform-notes}

이 섹션에서는 Adobe Experience Manager 및 Add-Ons 실행에 대한 특수 메모와 자세한 정보를 제공합니다.

### IPv4 및 IPv6 {#ipv-and-ipv}

Adobe Experience Manager(인스턴스, 발송자)의 모든 요소는 IPv4 및 IPv6 네트워크 모두에 설치할 수 있습니다.

특별한 구성이 필요하지 않으므로 작업이 매끄러워집니다. 필요한 경우 네트워크 유형에 적합한 형식을 사용하여 IP 주소를 간단히 지정할 수 있습니다.

즉, IP 주소를 지정해야 할 경우 다음 중에서 선택할 수 있습니다.

* IPv6 주소
예: `https://[ab12::34c5:6d7:8e90:1234]:4502`

* IPv4 주소
예: `https://123.1.1.4:4502`

* 서버 이름
예를 들어 `https://www.yourserver.com:4502`

* `localhost`의 기본 대/소문자 구분은 IPv4 및 IPv6 네트워크 설치에 대해 해석됩니다.
예를 들어 `https://localhost:4502`

### AEM Dynamic Media Add-on {#requirements-for-aem-dynamic-media-add-on} 요구 사항

AEM Dynamic Media는 기본적으로 비활성화됩니다. [다이내믹 미디어 활성화](/help/assets/config-dynamic.md#enabling-dynamic-media)를 보려면 여기를 참조하십시오.

Dynamic Media가 활성화되면 다음과 같은 추가 기술 요구 사항이 적용됩니다.

>[!NOTE]
>
>이러한 시스템 요구 사항 **만 동적 미디어 - 하이브리드 모드를 사용하는 경우 적용다이내믹 미디어 - 하이브리드 모드에는 포함된 이미지 서버가 있으며, 이는 특정 운영 체제에서만 인증됩니다.**
>
>동적 미디어 - Scene7 모드(즉, **dynamicmedia_scene7** 실행 모드)를 실행하는 다이내믹 미디어 고객의 경우 추가 시스템 요구 사항이 없습니다.aem과 동일한 시스템 요구 사항만 해당합니다. 다이내믹 미디어 - Scene7 모드 아키텍처는 AEM에 임베드된 서비스가 아니라 클라우드 기반 이미지 서비스를 사용합니다.

#### 하드웨어 {#hardware}

다음 하드웨어 요구 사항은 Linux 및 Windows 모두에 적용됩니다.

* 4개 이상의 코어가 있는 Intel Xeon 또는 AMD Opteron CPU
* 최소 16GB RAM

#### Linux {#linux}

Linux에서 Dynamic Media를 사용하는 경우 다음 전제 조건을 충족해야 합니다.

* RedHat Enterprise 7 또는 CentOS 7 이상(최신 수정 패치 포함)
* 64비트 운영 체제
* 비활성화된 전환(권장)
* SELinux가 비활성화되었습니다(다음 참고 참조).

>[!NOTE]
>
>LC_CTYPE이 `en_US.UTF-8`과(와) 같지 않도록 로케일이 설정된 경우 동적 미디어가 작동하지 않습니다. 명령 프롬프트에서 해당 값이 &quot;locale&quot;이라는 유형을 확인합니다. 이 값을 설정하지 않은 경우 AEM을 실행하기 전에 &quot;export LC_CTYPE=&quot;를 입력하여 LC_CTYPE 환경 변수를 빈 문자열로 설정합니다.

>[!NOTE]
>
>**SELinux:** 이미지 제공 기능이 SELinux를 켜는 경우 작동하지 않습니다. 이 옵션은 기본적으로 활성화되어 있습니다. 이 문제를 해결하려면 **/etc/seleclinux/config** 파일을 편집하고 SELinux 값을 다음 위치에서 변경하십시오.
>
>`SELINUX=enforcing` **끝** `SELINUX=disabled`

>[!NOTE]
>
>**NUMA 아키텍처:** AMD64 및 Intel EM64T를 지원하는 프로세서가 있는 시스템은 일반적으로 NUMA(비균일 메모리 아키텍처) 플랫폼으로 구성되며, 이는 커널이 단일 메모리 노드를 구성하는 대신 부팅 시 여러 메모리 노드를 구성한다는 것을 의미합니다.
>
>다중 노드 구문은 다른 노드가 소진되기 전에 하나 이상의 노드에서 메모리를 소진할 수 있습니다. 메모리 소모가 발생하는 경우 커널은 사용 가능한 메모리가 있어도 프로세스를 종료하기로 결정할 수 있습니다(예: 이미지 서버 또는 플랫폼 서버).
>
>따라서 Adobe은 시스템을 실행 중인 경우 커널이 이러한 프로세스를 죽이는 것을 방지하기 위해 **numa=off** 부트 옵션을 사용하여 NUMA를 끄는 것이 좋습니다.

>[!NOTE]
>
>**서버 호스트 이름이** 해결되어야 합니다.서버의 호스트 이름이 IP 주소로 확인되는지 확인하십시오. 그렇지 않을 경우 정규화된 호스트 이름과 IP 주소를 **/etc/hosts**&#x200B;에 추가하십시오.
>
>`<ip address> <fully qualified hostname>`

#### Windows {#windows}

* Microsoft Windows Server 2016
* 실제 메모리(RAM)의 최소 2배까지 공간 교체

Windows에서 Dynamic Media를 사용하려면 x64 및 x86용 Microsoft Visual Studio 2010, 2013 및 2015 재배포용 파일을 설치합니다.

Windows x64의 경우:

* [https://www.microsoft.com/en-us/download/details.aspx?id=13523](https://www.microsoft.com/en-us/download/details.aspx?id=13523)에서 Microsoft Visual Studio 2010 재배포 가능 버전을 다운로드하십시오.
* [https://www.microsoft.com/en-us/download/details.aspx?id=40784](https://www.microsoft.com/en-us/download/details.aspx?id=40784)에서 Microsoft Visual Studio 2013 재배포 가능 버전을 다운로드하십시오.
* [https://www.microsoft.com/en-us/download/details.aspx?id=48145](https://www.microsoft.com/en-us/download/details.aspx?id=48145)에서 Microsoft Visual Studio 2015 재배포 가능 버전을 다운로드하십시오.

Windows x86의 경우:

* [https://www.microsoft.com/en-in/download/details.aspx?id=5555](https://www.microsoft.com/en-in/download/details.aspx?id=5555)에서 Microsoft Visual Studio 2010 재배포 가능 버전을 다운로드하십시오.
* [https://www.microsoft.com/en-in/download/details.aspx?id=40769](https://www.microsoft.com/en-in/download/details.aspx?id=40769)에서 Microsoft Visual Studio 2013 재배포 가능 버전을 다운로드하십시오.
* [https://www.microsoft.com/en-us/download/details.aspx?id=52685](https://www.microsoft.com/en-us/download/details.aspx?id=52685)에서 Microsoft Visual Studio 2015 재배포 가능 버전을 다운로드하십시오.

#### MacOS {#macos}

* 10.9.x 이상
* 시험버전 및 데모 용도로만 지원

### AEM Forms PDF Generator 요구 사항 {#requirements-for-aem-forms-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>제품</strong></p> </th>
   <th><p><strong>PDF로 변환 지원 포맷</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2017 classic </a> tracklatest 버전</td>
   <td>XPS, 이미지 형식(BMP, GIF, JPEG, JPG, TIF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, DWG, DXF 및 DWF</td>
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
   <td>ODT, ODP, ODS, ODF, SXW, SXI, SXC, SXD, XLS, XLSX, DOC, DOCX, PPT, PPTX, 이미지 형식(BMP, GIF, JPEG, JPG, TIF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, RTF 및 TXT</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>PDF Generator는 지원되는 운영 체제 및 애플리케이션의 영어, 프랑스어, 독일어 및 일본어 버전만 지원합니다.
>
>추가:
>
>* PDF Generator를 사용하려면 32비트 버전의 [Acrobat 2017 클래식 트랙 버전 17.011.30078 이상](https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html)이 필요합니다.
>* PDF Generator는 변환에 필요한 32비트 Microsoft Office Professional Plus 및 기타 소프트웨어만 지원합니다.
>* PDF Generator는 Microsoft Office 365를 지원하지 않습니다.
>* OpenOffice용 PDF Generator 변환은 Windows 및 Linux에서만 지원됩니다.
>* OCR PDF, Optimize PDF 및 Export PDF 기능은 Windows에서만 지원됩니다.
>* Acrobat 버전은 PDF Generator 기능을 사용하도록 AEM Forms에 번들로 포함되어 있습니다. 번들로 제공되는 버전은 AEM Forms 라이선스 기간 동안 AEM Forms PDF Generator와 함께 사용할 수 있는 AEM Forms에서만 프로그램 방식으로 액세스해야 합니다. 자세한 내용은 배포에 따라 AEM Forms 제품 설명을 참조하십시오([온-프레미스](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html) 또는 [Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html))&quot;

   >
   >
* PDF Generator 서비스는 Microsoft Windows 10을 지원하지 않습니다.

>



### AEM Assets XMP 메타데이터 쓰기 되돌리기 요구 사항 {#requirements-for-aem-assets-xmp-metadata-write-back}

XMP 쓰기가 지원되고 다음 플랫폼 및 파일 포맷에 대해 활성화됩니다.

* **운영 체제:**

   * Linux(64비트 시스템에서 32비트 및 32비트 애플리케이션 지원). 32비트 클라이언트 라이브러리를 설치하는 단계는 64비트 RedHat Linux[에서 XMP 추출 및 다시 쓰기를 활성화하는 방법을 참조하십시오.](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html)

   * Windows Server
   * Mac OS X(64비트)

* **파일 형식**:JPEG, PNG, TIFF, PDF, INDD, AI 및 EPS.

### Linux {#assetsonlinux}에서 메타데이터가 많은 에셋을 처리하기 위한 AEM Assets 요구 사항

XMPFilesProcessor 프로세스를 사용하려면 라이브러리 GLIBC_2.14가 필요합니다. GLIBC_2.14를 포함하는 Linux 커널(예: Linux 커널 버전 3.1.x)을 사용합니다.PSD 파일과 같은 많은 양의 메타데이터가 포함된 에셋 처리 성능이 향상됩니다. 이전 버전의 GLIBC를 사용하면 `com.day.cq.dam.core.impl.handler.xmp.NCommXMPHandler Failed to read XMP`으로 시작하는 로그에 오류가 발생합니다.
