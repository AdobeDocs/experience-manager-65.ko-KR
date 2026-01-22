---
title: 배포 및 유지 관리
description: AEM 설치를 시작하는 방법에 대해 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
docset: aem65
exl-id: 3df0662a-0768-4b56-8b94-c517657b4bd9
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: 36cb540cda7faeca5949028c9c14ab2ecf860402
workflow-type: tm+mt
source-wordcount: '1779'
ht-degree: 7%

---

# 배포 및 유지 관리{#deploying-and-maintaining}

이 페이지에서는 다음 정보를 찾을 수 있습니다.

* [기본 개념](#basic-concepts)

   * [AEM란?](#what-is-aem)
   * [일반 배포](#typical-deployment-scenarios)

      * [온프레미스](#on-premise)
      * [Cloud Manager을 사용한 Managed Services](#managed-services-using-cloud-manager)

* [시작하기](#getting-started)

   * [사전 요구 사항](#prerequisites)
   * [소프트웨어 가져오기](#getting-the-software)
   * [기본 로컬 설치](#default-local-install)
   * [작성자 및 게시 설치](#author-and-publish-installs)
   * [압축을 푼 설치 디렉토리](#unpacked-install-directory)
   * [시작 및 중지](#starting-and-stopping)

이러한 기본 사항을 숙지하면 다음 하위 페이지에서 보다 고급 세부 정보를 찾을 수 있습니다.

* [기술 요구 사항](/help/sites-deploying/technical-requirements.md)
* [권장 배포](/help/sites-deploying/recommended-deploys.md)
* [사용자 정의 독립 실행형 설치](/help/sites-deploying/custom-standalone-install.md)
* [애플리케이션 서버 설치](/help/sites-deploying/application-server-install.md)
* [문제 해결](/help/sites-deploying/troubleshooting.md)
* [명령줄 시작 및 중지](/help/sites-deploying/command-line-start-and-stop.md)
* [구성](/help/sites-deploying/configuring.md)
* [AEM 6.5로 업그레이드](/help/sites-deploying/upgrade.md)
* [전자 상거래](/help/commerce/cif-classic/deploying/ecommerce.md)
* [구성 방법 문서](/help/sites-deploying/ht-deploy.md)
* [웹 콘솔](/help/sites-deploying/web-console.md)
* [복제 문제 해결](/help/sites-deploying/troubleshoot-rep.md)
* [모범 사례](/help/sites-deploying/best-practices.md)
* [커뮤니티 배포](/help/communities/deploy-communities.md)
* [AEM 플랫폼 소개](/help/sites-deploying/platform.md)
* [성능 지침](/help/sites-deploying/performance-guidelines.md)
* [AEM Mobile 시작하기](/help/mobile/getting-started-aem-mobile.md)
* [AEM Screens이란?](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html)

## 기본 개념 {#basic-concepts}

### AEM란? {#what-is-aem}

Adobe Experience Manager은 상업용 웹 사이트 및 관련 서비스를 구축, 관리 및 배포하기 위한 웹 기반 클라이언트 서버 시스템입니다. 여러 인프라 수준 및 애플리케이션 수준 기능을 하나의 통합 패키지로 결합합니다.

인프라 수준에서 AEM은 다음을 제공합니다.

* **웹 응용 프로그램 서버**: AEM은 독립 실행형 모드(통합 Jetty 웹 서버 포함)로 배포하거나 타사 응용 프로그램 서버 내의 웹 응용 프로그램으로 배포할 수 있습니다.
* **웹 응용 프로그램 프레임워크**: AEM은 RESTful의 콘텐츠 지향 웹 응용 프로그램 작성을 단순화하는 Sling 웹 응용 프로그램 프레임워크를 통합합니다.
* **콘텐츠 저장소**: AEM에는 구조화되지 않은 데이터 및 반구조화 데이터를 위해 특별히 설계된 계층형 데이터베이스 유형인 JCR(Java™ Content Repository)이 포함되어 있습니다. 저장소는 사용자 대면 콘텐츠뿐만 아니라 애플리케이션에서 사용하는 모든 코드, 템플릿 및 내부 데이터를 저장합니다.

이 기반을 기반으로 구축된 AEM은 또한 관리를 위한 여러 애플리케이션 수준 기능을 제공합니다.

* **웹 사이트**
* **모바일 응용 프로그램**
* **디지털 발행물**
* **Forms 및 문서**
* **디지털 Assets**
* **커뮤니티**
* **온라인 Commerce**

마지막으로, 고객은 이러한 인프라와 애플리케이션 수준의 구성 요소를 사용하여 자체 애플리케이션을 구축함으로써 맞춤형 솔루션을 만들 수 있습니다.

AEM 서버는 **Java 기반**&#x200B;이며 해당 플랫폼을 지원하는 대부분의 운영 체제에서 실행됩니다. AEM과의 모든 클라이언트 상호 작용은 **웹 브라우저**&#x200B;를 통해 수행됩니다.

>[!NOTE]
>
>AEM 6.5 빠른 시작에서 사용할 수 있는 적응형 Forms 기능은 탐색 및 평가 목적으로만 설계되었습니다. 프로덕션 용도로 사용하려면 적응형 양식 기능에 적절한 라이선싱이 필요하므로 AEM Forms에 대해 유효한 라이선스를 확보해야 합니다.

### 일반적인 배포 시나리오 {#typical-deployment-scenarios}

AEM 용어에서 &quot;인스턴스&quot;는 서버에서 실행되는 AEM의 사본입니다. AEM 설치에는 일반적으로 별도의 컴퓨터에서 실행되는 최소 두 개의 인스턴스가 포함됩니다.

* **작성자**: 콘텐츠를 만들고, 업로드하고, 편집하고, 웹 사이트를 관리하는 데 사용되는 AEM 인스턴스입니다. 콘텐츠를 실행할 준비가 되면 게시 인스턴스에 복제됩니다.
* **게시**: 게시된 콘텐츠를 일반에게 제공하는 AEM 인스턴스입니다.

이러한 인스턴스는 설치된 소프트웨어 측면에서 동일합니다. 구성 단위로만 구분됩니다. 또한 대부분의 설치에서는 Dispatcher을 사용합니다.

* **Dispatcher**: AEM Dispatcher 모듈로 보강된 정적 웹 서버(Apache httpd, Microsoft® IIS 등)입니다. 게시 인스턴스에서 생성된 웹 페이지를 캐시하여 성능을 개선합니다.

이 설정에는 많은 고급 옵션과 정교함이 있지만 대부분의 배포에서 작성자, 게시 및 Dispatcher의 기본 패턴이 핵심입니다. 간단한 설정에 초점을 맞추어 시작하겠습니다. 고급 배포 옵션에 대한 논의는 다음과 같습니다.

다음 섹션에서는 두 가지 시나리오를 설명합니다.

* **온-프레미스**: AEM이 회사 환경에 배포되고 관리됩니다.

* **Managed Services - Adobe Experience Manager용 Cloud Manager**: Adobe Managed Services에서 배포하고 관리하는 AEM.

### 온프레미스 {#on-premise}

회사 환경의 서버에 AEM을 설치할 수 있습니다. 일반적인 설치 인스턴스는 개발, 테스트 및 게시 환경을 포함합니다. AEM 소프트웨어를 로컬에 설치하는 방법에 대한 기본 정보는 [시작하기](/help/sites-deploying/deploy.md#getting%20started)를 참조하십시오.

일반적인 온-프레미스 배포에 대한 자세한 내용은 [권장 배포](/help/sites-deploying/recommended-deploys.md)를 참조하세요.

### Cloud Manager을 사용한 Managed Services {#managed-services-using-cloud-manager}

AEM Managed Services은 디지털 환경 관리를 위한 완전한 솔루션입니다. 온-프레미스 배포의 모든 제어, 보안 및 사용자 지정 이점을 유지하면서 클라우드에서 경험 전달 솔루션의 이점을 제공합니다. AEM Managed Services을 사용하면 클라우드에 배포하고 Adobe의 모범 사례 및 지원에 의존하여 고객이 보다 빠르게 시작할 수 있습니다. 조직 및 비즈니스 사용자는 최소의 시간에 고객을 참여시키고 시장 점유율을 높이며 IT 부담을 줄이면서 혁신적인 마케팅 캠페인을 창출하는 데 집중할 수 있습니다.

AEM Managed Services 고객은 다음과 같은 이점을 실현할 수 있습니다.

**출시 기간 단축:** Adobe Managed Services의 유연한 클라우드 인프라를 통해 조직은 성공적인 디지털 경험을 신속하게 계획, 출시 및 최적화할 수 있습니다. Adobe은 추가적인 자본, 하드웨어 또는 소프트웨어 필요 없이 클라우드 아키텍처를 관리하고 Adobe의 고객 솔루션 엔지니어는 AEM 아키텍처, 프로비저닝, 백엔드 앱에 연결하기 위한 사용자 정의 및 Go-Live 모범 사례를 지원합니다.

**더 높은 성능:** 비즈니스에 안정적인 디지털 환경을 제공합니다. 4가지 서비스 가용성 옵션 99.5%, 99.9%, 99.95% 및 99.99%. 또한 자동 백업 및 다중 모드 재해 복구 모델을 통해 안정성과 비상 상황을 관리할 수 있습니다.

**최적화된 IT 비용:** 사전 예방적 지침 및 전문 지식은 조직이 최신 버전의 AEM을 최신 상태로 유지할 수 있도록 지원합니다. Adobe Platinum 유지 관리 및 지원은 AMS Enterprise/Basic의 새로운 배포에 자동으로 포함되며, 조직의 미션 크리티컬 애플리케이션 유지 관리를 위한 기술 전문 지식 및 운영 경험을 제공합니다. 무료 기본 Analytics 또는 Target 기능은 분석 및 개인화에 대한 요구 사항이 제한된 중간 시장 조직에 특히 더 많은 가치를 제공합니다.

**최고 보안:** 제한된 액세스 시설, 방화벽 시스템 뒤 또는 가상 사설 클라우드 내에서 고객 응용 프로그램을 호스팅하여 엔터프라이즈급 물리적, 네트워크 및 데이터 보안을 보장합니다. 여기에는 강력한 데이터 스토리지 암호화, 항바이러스성 및 데이터 격리를 갖춘 단일 테넌트 가상 시스템이 포함됩니다.

**Cloud Manager**: Adobe Experience Manager Managed Services 서비스의 일부인 Cloud Manager은 조직에서 클라우드에서 Adobe Experience Manager을 자체 관리할 수 있도록 해주는 셀프서비스 포털입니다. 여기에는 IT 팀 및 구현 파트너가 성능 또는 보안을 손상하지 않고 맞춤화 또는 업데이트 제공 속도를 높일 수 있는 최신 CI/CD(지속적 통합 및 지속적 배포) 파이프라인이 포함되어 있습니다. Cloud Manager은 Adobe Managed Service 고객만 사용할 수 있습니다.

Cloud Manager 및 해당 리소스에 대한 자세한 내용은 [**Cloud Manager 사용 안내서**](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html)를 참조하세요.

## 시작하기 {#getting-started}

### 사전 요구 사항 {#prerequisites}

프로덕션 인스턴스는 공식적으로 지원되는 OS를 실행하는 전용 컴퓨터에서 실행되지만([기술 요구 사항](/help/sites-deploying/technical-requirements.md) 참조), Experience Manager 서버는 실제로 [**Java™ Standard Edition 8**](https://www.oracle.com/java/technologies/downloads/#java8)을 지원하는 모든 시스템에서 실행됩니다.

AEM에 익숙해지고 개발하기 위해 Apple OS X를 실행하는 로컬 시스템이나 Microsoft® Windows 또는 Linux®의 데스크탑 버전을 실행하는 로컬 시스템에 설치된 인스턴스를 사용하는 것이 일반적입니다.

클라이언트측에서 AEM은 데스크톱 및 태블릿 운영 체제에서 모든 최신 브라우저(**Microsoft® Edge**, **Internet Explorer** 11, **Chrome &#x200B;** 51+**&#x200B; **, **Firefox &#x200B;** 47+, **Safari** 8+)에서 작동합니다. 자세한 내용은 [지원되는 클라이언트 플랫폼](/help/sites-deploying/technical-requirements.md#supported-client-platforms)을 참조하십시오.

### 소프트웨어 가져오기 {#getting-the-software}

유효한 유지 관리 및 지원 계약을 보유한 고객은 코드가 포함된 메일 알림을 받았어야 하며 [**Adobe 라이선스 웹 사이트**](https://licensing.adobe.com/)에서 AEM을 다운로드할 수 있습니다. 비즈니스 파트너는 [**spphelp@adobe.com**](mailto:spphelp@adobe.com)&#x200B;에서 다운로드 액세스를 요청할 수 있습니다.

AEM 소프트웨어 패키지는 두 가지 형태로 제공됩니다.

* **cq-quickstart-6.5.0.jar:** 실행해야 하는 모든 내용이 포함된 독립 실행형 실행 파일 *jar*.

* **cq-quickstart-6.5.0.war:** 타사 응용 프로그램 서버에 배포할 *war* 파일입니다.

다음 섹션에서는 **독립 실행형 설치**&#x200B;에 대해 설명합니다. 응용 프로그램 서버에 AEM을 설치하는 방법에 대한 자세한 내용은 [응용 프로그램 서버 설치](/help/sites-deploying/application-server-install.md)를 참조하십시오.

### 기본 로컬 설치 {#default-local-install}

1. 로컬 컴퓨터에 설치 디렉터리를 만듭니다. 예:

   UNIX® 설치 위치: **/opt/aem**

   Windows 설치 위치: **`C:\aem`**

   마찬가지로, 바탕 화면의 오른쪽 폴더에 샘플 인스턴스를 설치하는 것이 일반적입니다. 어떤 경우든 Adobe은 일반적으로 이 위치를 다음과 같이 참조합니다.

   `<aem-install>`

   *파일 디렉터리의 경로는 미국 ASCII 문자로만 구성되어야 합니다.*

1. **jar** 및 **license** 파일을 이 디렉터리에 배치합니다.

   ```shell
   <aem-install>/
       cq-quickstart-6.5.0.jar
       license.properties
   ```

   `license.properties` 파일을 제공하지 않으면 AEM에서 브라우저를 시작할 때 라이선스 키를 입력할 수 있는 **시작** 화면으로 리디렉션합니다. 아직 라이센스 키가 없는 경우 Adobe에 유효한 라이센스 키를 요청해야 합니다.

1. GUI 환경에서 인스턴스를 시작하려면 **`cq-quickstart-6.5.0.jar`** 파일을 두 번 클릭하십시오.

   또는 명령줄에서 AEM을 시작할 수 있습니다.

   ```shell
       java -Xmx1024M -jar cq-quickstart-6.5.0.jar
   ```

AEM에서 jar 파일의 압축을 풀고 직접 설치하고 시작하는 데 몇 분이 소요됩니다. 위의 절차를 수행하면 다음과 같은 결과가 발생합니다.

* **AEM 작성자** 인스턴스
* **localhost**&#x200B;에서 실행 중
* 포트 **4502**&#x200B;에서

인스턴스에 액세스하려면 브라우저가 다음을 수행하도록 합니다.

**`https://localhost:4502`**

작성자 인스턴스의 결과는 **의**&#x200B;게시 인스턴스&#x200B;**`localhost:4503`**&#x200B;에 연결하도록 자동으로 구성됩니다.

### 작성자 및 게시 설치 {#author-and-publish-installs}

기본 설치(**의**&#x200B;작성자&#x200B;**`localhost:4502`** 인스턴스)를 처음 시작하기 전에 `jar` 파일의 이름을 바꾸는 것만으로 변경할 수 있습니다. 이름 지정 패턴은 다음과 같습니다.

**`cq-<instance-type>-p<port-number>.jar`**

예를 들어 파일 이름을 로 바꾸는 경우

**`cq-author-p4502.jar`**

이 인스턴스를 실행하면 작성자 인스턴스가 **`localhost:4502`**&#x200B;에서 실행됩니다.

마찬가지로 파일 이름 바꾸기 및 실행

**`cq-publish-p4503.jar`**

**`localhost:4503`**&#x200B;에서 게시 인스턴스가 실행되고 있습니다.

예를 들어에 이 두 인스턴스를 설치합니다

`<aem-install>/author`및

**`<aem-install>/publish`**

설치 사용자 정의에 대한 자세한 내용은 다음을 참조하십시오.

* [사용자 정의 독립 실행형 설치](/help/sites-deploying/custom-standalone-install.md)
* [실행 모드](/help/sites-deploying/configure-runmodes.md)

### 압축을 푼 설치 디렉토리 {#unpacked-install-directory}

quickstart jar를 처음 실행하면 새 하위 디렉터리(`crx-quickstart`)의 동일한 디렉터리에 자동으로 압축이 풀립니다. 다음이 필요합니다.

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

인스턴스가 UI에서 설치된 경우 브라우저 창이 자동으로 열리고 인스턴스의 호스트 및 포트와 온/오프 스위치를 표시하는 데스크탑 애플리케이션 창도 열립니다.

![시작 화면](assets/screen_shot_.png)

### 시작 및 중지 {#starting-and-stopping}

AEM의 압축을 풀고 처음 시작한 후 설치 디렉토리에서 jar 파일을 두 번 클릭하면 인스턴스가 시작되고 재설치되지 않습니다.

GUI에서 인스턴스를 중지하려면 데스크톱 응용 프로그램 창에서 **켜기/끄기** 스위치를 클릭하십시오.

명령줄에서 AEM을 중지하고 시작할 수도 있습니다. 인스턴스를 처음 설치했다고 가정할 경우 **명령줄 스크립트**&#x200B;가 여기에 있습니다.

**`<aem-install>/crx-quickstart/bin/`**

이 폴더에는 다음과 같은 UNIX® bash 셸 스크립트가 포함되어 있습니다.

* **`start`**: 인스턴스를 시작합니다.
* `stop`: 인스턴스를 중지합니다.
* **`status`**: 인스턴스의 상태를 보고합니다.
* **`quickstart`**: 필요한 경우 시작 정보를 구성하는 데 사용됩니다.

Windows용 **`bat`**&#x200B;개 파일도 있습니다. 자세한 내용은 다음을 참조하십시오.

* [명령줄 시작 및 중지](/help/sites-deploying/command-line-start-and-stop.md)

AEM은 웹 브라우저를 시작하고 자동으로 적절한 페이지(일반적으로 로그인 페이지)로 리디렉션합니다. 예를 들면 다음과 같습니다.

`https://localhost:4502/`

![로그인 화면](assets/screen_shot_2019-04-08at83533am.png)

로그인하면 AEM에 액세스할 수 있습니다. 자세한 내용은 역할에 따라 다음을 참조하십시오.

* [작성](/help/sites-authoring/first-steps.md)
* [관리](/help/sites-administering/home.md)
* [개발](/help/sites-developing/getting-started.md)
* [관리](/help/managing/best-practices.md)

## 고급 배포 {#advanced-deployment}

위의 섹션에서는 AEM 설치의 기본 사항을 잘 이해할 수 있습니다. 그러나 AEM의 전체 프로덕션 시스템을 설치하면 훨씬 더 복잡해질 수 있습니다. 고급 설치에 대한 전체 내용은 다음 하위 페이지를 참조하십시오.

* [기술 요구 사항](/help/sites-deploying/technical-requirements.md)
* [권장 배포](/help/sites-deploying/recommended-deploys.md)
* [사용자 정의 독립 실행형 설치](/help/sites-deploying/custom-standalone-install.md)
* [애플리케이션 서버 설치](/help/sites-deploying/application-server-install.md)
* [문제 해결](/help/sites-deploying/troubleshooting.md)
* [명령줄 시작 및 중지](/help/sites-deploying/command-line-start-and-stop.md)
* [구성](/help/sites-deploying/configuring.md)
* [AEM 6.5로 업그레이드](/help/sites-deploying/upgrade.md)
* [전자 상거래](/help/commerce/cif-classic/deploying/ecommerce.md)
* [구성 방법 문서](/help/sites-deploying/ht-deploy.md)
* [웹 콘솔](/help/sites-deploying/web-console.md)
* [복제 문제 해결](/help/sites-deploying/troubleshoot-rep.md)
* [모범 사례](/help/sites-deploying/best-practices.md)
* [커뮤니티 배포](/help/communities/deploy-communities.md)
* [AEM 플랫폼 소개](/help/sites-deploying/platform.md)
* [성능 지침](/help/sites-deploying/performance-guidelines.md)
* [AEM Mobile 시작하기](/help/mobile/getting-started-aem-mobile.md)
* [AEM Screens이란?](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html)
