---
title: 배포 및 유지 관리
seo-title: 배포 및 유지 관리
description: AEM 설치를 시작하는 방법을 알아봅니다.
seo-description: AEM 설치를 시작하는 방법을 알아봅니다.
uuid: 4429ac4d-abd7-47d8-b19d-773accb7cc7a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: e48cc0ed-688c-44c8-b6d6-5f3c8593a295
docset: aem65
translation-type: tm+mt
source-git-commit: cb07e24b01084f57ad46615cb463ad5a0329c181
workflow-type: tm+mt
source-wordcount: '1833'
ht-degree: 7%

---


# 배포 및 유지 관리{#deploying-and-maintaining}

이 페이지에서는 다음과 같은 정보를 확인할 수 있습니다.

* [기본 개념](#basic-concepts)

   * [AEM 소개](#what-is-aem)
   * [일반 배포](#typical-deployment-scenarios)

      * [온-프레미스](#on-premise)
      * [Cloud Manager를 사용한 Managed Services](#managed-services-using-cloud-manager)

* [시작하기](#getting-started)

   * [전제 조건](#prerequisites)
   * [소프트웨어 다운로드](#getting-the-software)
   * [기본 로컬 설치](#default-local-install)
   * [작성자 및 게시 설치](#author-and-publish-installs)
   * [설치 디렉토리 압축 해제](#unpacked-install-directory)
   * [시작 및 중지](#starting-and-stopping)

이러한 기본 사항을 숙지하고 나면 다음 하위 페이지에서 보다 고급 세부 정보를 확인할 수 있습니다.

* [기술 요구 사항](/help/sites-deploying/technical-requirements.md)
* [권장 배포](/help/sites-deploying/recommended-deploys.md)
* [사용자 지정 독립형 설치](/help/sites-deploying/custom-standalone-install.md)
* [애플리케이션 서버 설치](/help/sites-deploying/application-server-install.md)
* [문제 해결](/help/sites-deploying/troubleshooting.md)
* [명령줄 시작 및 중지](/help/sites-deploying/command-line-start-and-stop.md)
* [구성](/help/sites-deploying/configuring.md)
* [AEM 6.5로 업그레이드](/help/sites-deploying/upgrade.md)
* [eCommerce](/help/sites-deploying/ecommerce.md)
* [구성 방법 문서](/help/sites-deploying/ht-deploy.md)
* [웹 콘솔](/help/sites-deploying/web-console.md)
* [복제 문제 해결](/help/sites-deploying/troubleshoot-rep.md)
* [우수 사례](/help/sites-deploying/best-practices.md)
* [커뮤니티 배포](/help/communities/deploy-communities.md)
* [AEM Platform 소개](/help/sites-deploying/platform.md)
* [성능 지침](/help/sites-deploying/performance-guidelines.md)
* [AEM Mobile 시작하기](/help/mobile/getting-started-aem-mobile.md)
* [AEM Screens 소개](https://docs.adobe.com/content/help/ko-KR/experience-manager-screens/user-guide/aem-screens-introduction.html)

## 기본 개념 {#basic-concepts}

### AEM 소개{#what-is-aem}

Adobe Experience Manager는 웹 사이트 및 관련 서비스를 구축, 관리 및 배포하는 웹 기반 클라이언트 서버 시스템입니다. 여러 가지 인프라 수준 및 애플리케이션 수준의 기능을 통합된 단일 패키지에 결합합니다.

인프라 수준 AEM에서는 다음을 제공합니다.

* **웹 응용 프로그램 서버**:AEM은 독립 실행형 모드(통합 Jetty 웹 서버 포함)로 배포하거나 타사 애플리케이션 서버 내에서 웹 애플리케이션으로 배포할 수 있습니다.
* **웹 응용 프로그램 프레임워크**:AEM에는 RESTful 컨텐츠 중심의 웹 애플리케이션의 작성을 간소화하는 Sling 웹 애플리케이션 프레임워크가 통합되어 있습니다.
* **컨텐츠 저장소**:AEM에는 비정형 및 반정형 데이터를 위해 특별히 고안된 계층적 데이터베이스 유형인 JCR(Java Content Repository)이 포함되어 있습니다. 저장소에는 사용자 대상 컨텐츠뿐만 아니라 응용 프로그램에서 사용하는 모든 코드, 템플릿 및 내부 데이터가 저장됩니다.

이 베이스를 기반으로 구축된 AEM은 다음을 관리할 수 있는 다양한 애플리케이션 수준 기능도 제공합니다.

* **웹 사이트**
* **모바일 애플리케이션**
* **디지털 출판**
* **양식**
* **디지털 에셋**
* **커뮤니티**
* **온라인 상거래**

마지막으로, 고객은 이러한 인프라와 애플리케이션 수준의 기본 구성 요소를 사용하여 고유한 애플리케이션을 구축하여 맞춤형 솔루션을 제작할 수 있습니다.

AEM 서버는 **Java 기반**&#x200B;이며 해당 플랫폼을 지원하는 대부분의 운영 체제에서 실행됩니다. AEM과의 모든 클라이언트 상호 작용은 **웹 브라우저**&#x200B;를 통해 수행됩니다.

### 일반적인 배포 시나리오 {#typical-deployment-scenarios}

AEM 용어에서 &quot;인스턴스&quot;는 서버에서 실행되는 AEM의 사본입니다. AEM 설치에는 대개 두 개 이상의 인스턴스가 포함되며 일반적으로 별도의 시스템에서 실행됩니다.

* **작성자**:컨텐츠를 만들고 업로드하고 편집하고 웹 사이트를 관리하는 데 사용되는 AEM 인스턴스입니다. 컨텐츠를 라이브할 준비가 되면 게시 인스턴스에 복제됩니다.
* **게시**:게시된 컨텐츠를 대중에게 제공하는 AEM 인스턴스입니다.

이러한 인스턴스는 설치된 소프트웨어에 대해 동일합니다. 구성 하나만으로 차별화됩니다. 또한 대부분의 설치에서 디스패처를 사용합니다.

* **발송자**:정적 웹 서버(Apache httpd, Microsoft IIS 등) aem 디스패처 모듈을 사용하여 추가합니다. 게시 인스턴스에서 생성한 웹 페이지를 캐시하여 성능을 향상시킵니다.

이 설정에는 많은 고급 옵션과 설명이 있지만 대부분의 배포에서 작성자, 게시 및 발송자의 기본 패턴은 가장 중요합니다. 우리는 비교적 간단한 설정에 초점을 맞추면서 시작할 것입니다. 다음 단계에 고급 배포 옵션에 대한 논의가 있을 예정입니다.

다음 섹션에서는 시나리오 모두에 대해 설명합니다.

* **온-프레미스**:기업 환경에 배포 및 관리되는 AEM

* **Managed Services - Adobe Experience Manager용 Cloud Manager**:Adobe Managed Services에서 배포 및 관리하는 AEM

### 온-프레미스 {#on-premise}

회사 환경의 서버에 AEM을 설치할 수 있습니다. 일반적인 설치 인스턴스는 다음과 같습니다.개발, 테스트 및 게시 환경. AEM 소프트웨어를 로컬에 설치하는 방법에 대한 자세한 내용은 [시작하기](/help/sites-deploying/deploy.md#getting%20started) 섹션을 참조하십시오.

일반적인 온-프레미스 배포에 대한 자세한 내용은 [권장 배포](/help/sites-deploying/recommended-deploys.md)를 참조하십시오.

### Cloud Manager를 사용하는 Managed Services {#managed-services-using-cloud-manager}

AEM Managed Services은 디지털 경험 관리를 위한 완벽한 솔루션입니다. 사내 배포의 모든 제어, 보안 및 맞춤화 기능을 그대로 유지하면서 클라우드에서 경험 전달 솔루션의 이점을 제공합니다. AEM Managed Services을 사용하면 클라우드에 배포하거나 모범 사례와 Adobe의 지원을 통해 보다 신속하게 시작할 수 있습니다. 조직 및 비즈니스 사용자는 IT에 대한 부담을 줄이면서 짧은 시간에 고객의 참여를 유도하고 시장 점유율을 높이며 혁신적인 마케팅 캠페인을 만드는 데 집중할 수 있습니다.

AEM Managed Services 고객은 다음과 같은 이점을 누릴 수 있습니다.

**출시 시간 단축: Adobe Managed Services** 의 유연한 클라우드 인프라를 사용하여 성공적인 디지털 경험을 신속하게 계획, 실행 및 최적화할 수 있습니다. Adobe은 추가 자본, 하드웨어 또는 소프트웨어 없이도 클라우드 아키텍처를 관리하며, Adobe의 고객 성공 엔지니어를 통해 AEM 아키텍처, 프로비저닝, 백엔드 앱에 연결하기 위한 맞춤화 및 go-live 모범 사례를 지원합니다.

**고성능의** 성능: 99.5%, 99.9%, 99.95% 및 99.99%의 서비스 가용성 옵션을 통해 비즈니스를 위한 안정적인 디지털 경험을 제공합니다. 또한 자동 백업 및 다중 모드 재해 복구 모델을 통해 안정성과 비상시 관리를 보장할 수 있습니다.

**최적화된 IT 비용:** 사전 예방 지침과 전문성을 통해 조직은 최신 버전의 AEM을 사용할 수 있습니다. Adobe Platinum 유지 관리 및 지원은 AMS Enterprise/Basic의 새로운 배포에 자동으로 포함되며 조직에 중요한 애플리케이션을 유지 관리할 수 있도록 기술적 전문 지식과 운영 경험을 제공합니다. 무료 기본 분석 또는 Target 기능은 특히 분석 및 개인화에 대한 요구 사항이 제한적인 중간 규모 조직의 경우 추가적인 가치를 제공합니다.

**최고 보안:** 방화벽 시스템 내부 또는 가상 비공개 클라우드 내부에 고객 애플리케이션을 호스팅하여 엔터프라이즈급 물리적, 네트워크 및 데이터 보안을 보장합니다. 강력한 데이터 스토리지 암호화, 안티바이러스 및 데이터 격리 기능을 갖춘 싱글 테넌트 방식의 가상 시스템이 포함되어 있습니다.

**클라우드 관리자**:Adobe Experience Manager Managed Services 솔루션의 일부인 Cloud Manager는 조직이 클라우드에서 Adobe Experience Manager을 직접 관리할 수 있는 셀프 서비스 포털입니다. IT 팀 및 구현 파트너가 성능 또는 보안을 손상시키지 않고 사용자 정의 또는 업데이트를 신속하게 전달할 수 있도록 해주는 최첨단 지속적인 통합 및 CI/CD(Continuous Delivery) 파이프라인이 포함되어 있습니다. Cloud Manager는 Adobe Managed Service 고객에게만 제공됩니다.

Cloud Manager 및 해당 리소스에 대한 자세한 내용은 [**클라우드 관리자 사용자 안내서**](https://docs.adobe.com/content/help/ko-KR/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)를 참조하십시오.

## 시작하기 {#getting-started}

### 전제 조건 {#prerequisites}

프로덕션 인스턴스는 일반적으로 공식적으로 지원되는 OS를 실행하는 전용 시스템에서 실행되지만([기술 요구 사항](/help/sites-deploying/technical-requirements.md) 참조), Experience Manager 서버는 실제로 [**Java Standard Edition 8**](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)을 지원하는 모든 시스템에서 실행됩니다.

익숙해지거나 AEM을 기반으로 개발하는 경우 Apple OS X 또는 데스크탑 버전의 Microsoft Windows 또는 Linux를 실행하는 로컬 시스템에 설치된 인스턴스를 사용하는 것이 일반적입니다.

클라이언트측에서 AEM은 데스크탑 및 태블릿 운영 체제 모두에서 최신 브라우저(**Microsoft Edge**, **Internet Explorer** 11, **Chrome **51+** **, **Firefox **47+, **8+)와 함께 작동합니다. .** 자세한 내용은 [지원되는 클라이언트 플랫폼](/help/sites-deploying/technical-requirements.md#supported-client-platforms)을 참조하십시오.

### 소프트웨어 {#getting-the-software} 가져오기

유효한 유지 관리 및 지원 계약을 보유한 고객은 코드가 포함된 메일 알림을 받았어야 하며, [**Adobe 라이선스 웹 사이트**](https://licensing.adobe.com/)에서 AEM을 다운로드할 수 있습니다. 비즈니스 파트너는 [**spphelp@adobe.com**](mailto:spphelp@adobe.com)&#x200B;에서 다운로드 액세스 권한을 요청할 수 있습니다.

AEM 소프트웨어 패키지는 다음과 같은 두 가지 형태로 제공됩니다.

* **cq-quickstart-6.5.0.jar:** 설치 및  ** 실행하는 데 필요한 모든 것이 포함된 독립형 실행 파일

* **cq-quickstart-6.5.0.war:** 제3 ** 자 응용 프로그램 서버에서 배포하기 위한 경고 파일입니다.

다음 섹션에서는 **독립형 설치**&#x200B;에 대해 설명합니다. 응용 프로그램 서버에서 AEM 설치에 대한 자세한 내용은 [응용 프로그램 서버 설치](/help/sites-deploying/application-server-install.md)를 참조하십시오.

### 기본 로컬 설치 {#default-local-install}

1. 로컬 컴퓨터에 설치 디렉토리를 만듭니다. 예:

   UNIX 설치 위치:**/opt/aem**

   Windows 설치 위치:**`C:\Program Files\aem`**

   마찬가지로, 데스크탑에 있는 폴더에 샘플 인스턴스를 설치하는 것이 일반적입니다. 모든 경우 이 위치를 일반적으로 다음과 같이 언급합니다.

   `<aem-install>`

   *파일 디렉토리의 경로는 미국 ASCII 문자로만 구성되어야 합니다.*

1. 다음 디렉토리에 **jar** 및 **license ** 파일을 배치합니다.

   ```shell
   <aem-install>/
       cq-quickstart-6.5.0.jar
       license.properties
   ```

   `license.properties` 파일을 제공하지 않으면 AEM은 시작 시 브라우저를 **시작** 화면으로 리디렉션하고 라이센스 키를 입력할 수 있습니다. 아직 라이센스 키가 없는 경우 Adobe에서 유효한 라이센스 키를 요청해야 합니다.

1. GUI 환경에서 인스턴스를 시작하려면 **`cq-quickstart-6.5.0.jar`** 파일을 두 번 클릭합니다.

   또는 명령줄에서 AEM을 시작할 수 있습니다. 32비트 Java VM의 경우 다음을 입력합니다.

   ```shell
       java -Xmx1024M -jar cq-quickstart-6.5.0.jar
   ```

   64비트 VM의 경우 다음을 입력합니다.

   ```shell
       java -XX:MaxPermSize=256m -Xmx1024M -jar cq-quickstart-6.5.0.jar
   ```

AEM에서 jar 파일의 압축을 풀고 직접 설치한 다음 시작하는 데 몇 분 정도 소요됩니다. 위의 절차는 다음과 같습니다.

* **AEM author** 인스턴스
* **localhost**&#x200B;에서 실행
* 포트 **4502에서**

인스턴스에 액세스하려면 브라우저에서 다음 작업을 수행하십시오.

**`https://localhost:4502`**

작성자 인스턴스의 결과는 **`localhost:4503`**&#x200B;의 **게시 인스턴스**&#x200B;에 연결하도록 자동으로 구성됩니다.

### 작성자 및 게시 설치 {#author-and-publish-installs}

**`localhost:4502`**&#x200B;의 기본 설치(**author** 인스턴스)는 처음 실행하기 전에 `jar` 파일의 이름을 바꾸기만 하면 변경할 수 있습니다. 이름 지정 패턴은 다음과 같습니다.

**`cq-<instance-type>-p<port-number>.jar`**

예를 들어 파일 이름을

**`cq-author-p4502.jar`**

그리고 이를 실행하면 작성자 인스턴스가 **`localhost:4502`**&#x200B;에서 실행됩니다.

마찬가지로 파일 이름 바꾸기 및 실행

**`cq-publish-p4503.jar`**

이 실행되면 게시 인스턴스가 **`localhost:4503`**&#x200B;에서 실행됩니다.

예를 들어 이 두 인스턴스를

`<aem-install>/author`및

**`<aem-install>/publish`**

설치 사용자 정의에 대한 자세한 내용은 다음을 참조하십시오.

* [사용자 지정 독립형 설치](/help/sites-deploying/custom-standalone-install.md)
* [실행 모드](/help/sites-deploying/configure-runmodes.md)

### 설치 디렉토리 {#unpacked-install-directory} 압축 해제

quickstart jar를 처음으로 실행하면 `crx-quickstart`이라는 새로운 하위 디렉토리 아래의 동일한 디렉토리에 자체적으로 압축을 풀게 됩니다. 다음과 같이 끝나야 합니다.

```xml
<aem-install>/
    license.properties
    cq-quickstart-6.5.0.jar
    crx-quickstart/
        app/
        bin/
        conf/
        launchpad/
        logs/
        metrics/
        monitoring/
        opt/
        repository/
        threaddumps/
        eula-de_DE.html
        eula-en_US.html
        eula-fr_FR.html
        eula-ja_JP.html
        readme.txt
```

인스턴스를 UI에서 설치한 경우 브라우저 창이 자동으로 열리고 데스크톱 응용 프로그램 창이 열리면서 인스턴스의 호스트 및 포트와 온/오프 스위치가 표시됩니다.

![화면 시작](assets/screen_shot_.png)

>[!NOTE]
>
>symlinks를 사용하는 경우 symlink](https://helpx.adobe.com/experience-manager/kb/changing-symlink.html)과(와) 관련된 [문제를 살펴보십시오.

### {#starting-and-stopping} 시작 및 중지

AEM의 압축을 풀고 처음 시작한 경우 설치 디렉토리에서 jar 파일을 두 번 클릭하기만 하면 인스턴스가 다시 시작되지 않습니다.

GUI에서 인스턴스를 중지하려면 데스크톱 응용 프로그램 창에서 **on/off** 스위치를 클릭하면 됩니다.

명령줄에서 AEM을 중지하고 시작할 수도 있습니다. 인스턴스를 처음 설치했다고 가정할 때 **명령줄 스크립트**&#x200B;는 다음 위치에 있습니다.

**`<aem-install>/crx-quickstart/bin/`**

이 폴더에는 다음 Unix bash 셸 스크립트가 포함되어 있습니다.

* **`start`**:인스턴스를 시작합니다.
* `stop`:인스턴스를 중지합니다.
* **`status`**:인스턴스의 상태를 보고합니다.
* **`quickstart`**:필요한 경우 시작 정보를 구성하는 데 사용됩니다.

또한 Windows용 **`bat`** 파일에도 해당합니다. 자세한 내용은 다음을 참조하십시오.

* [명령줄 시작 및 중지](/help/sites-deploying/command-line-start-and-stop.md)

AEM은 웹 브라우저를 적절한 페이지(일반적으로 로그인 페이지)로 자동으로 리디렉션합니다.예를 들면 다음과 같습니다.

`https://localhost:4502/`

![로그인 화면](assets/screen_shot_2019-04-08at83533am.png)

로그인하면 AEM에 액세스할 수 있습니다. 자세한 내용은 역할에 따라 다음을 참조하십시오.

* [작성](/help/sites-authoring/home.md)
* [관리](/help/sites-administering/home.md)
* [개발](/help/sites-developing/home.md)
* [관리](/help/managing/best-practices.md)

## 고급 배포 {#advanced-deployment}

위의 섹션에서는 AEM 설치에 대한 기본 사항을 잘 이해해야 합니다. 그러나 AEM의 전체 프로덕션 시스템을 설치하는 경우 복잡성이 상당히 커질 수 있습니다. 고급 설치에 대한 자세한 내용은 다음 하위 페이지를 참조하십시오.

* [기술 요구 사항](/help/sites-deploying/technical-requirements.md)
* [권장 배포](/help/sites-deploying/recommended-deploys.md)
* [사용자 지정 독립형 설치](/help/sites-deploying/custom-standalone-install.md)
* [애플리케이션 서버 설치](/help/sites-deploying/application-server-install.md)
* [문제 해결](/help/sites-deploying/troubleshooting.md)
* [명령줄 시작 및 중지](/help/sites-deploying/command-line-start-and-stop.md)
* [구성](/help/sites-deploying/configuring.md)
* [AEM 6.5로 업그레이드](/help/sites-deploying/upgrade.md)
* [eCommerce](/help/sites-deploying/ecommerce.md)
* [구성 방법 문서](/help/sites-deploying/ht-deploy.md)
* [웹 콘솔](/help/sites-deploying/web-console.md)
* [복제 문제 해결](/help/sites-deploying/troubleshoot-rep.md)
* [우수 사례](/help/sites-deploying/best-practices.md)
* [커뮤니티 배포](/help/communities/deploy-communities.md)
* [AEM Platform 소개](/help/sites-deploying/platform.md)
* [성능 지침](/help/sites-deploying/performance-guidelines.md)
* [AEM Mobile 시작하기](/help/mobile/getting-started-aem-mobile.md)
* [AEM Screens 소개](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/aem-screens-introduction.html)
