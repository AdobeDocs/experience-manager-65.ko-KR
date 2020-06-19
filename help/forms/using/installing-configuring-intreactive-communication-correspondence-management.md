---
title: 대화형 통신 설치 및 구성
seo-title: 대화형 통신 설치 및 구성
description: 기업 관련 문의 사항, 문서, 명세서, 혜택 통지, 마케팅 메일, 청구서 및 환영 키트를 만들 수 있는 AEM Forms 인터랙티브 커뮤니케이션을 설치하고 구성합니다.
seo-description: 기업 관련 문의 사항, 문서, 명세서, 혜택 통지, 마케팅 메일, 청구서 및 환영 키트를 만들 수 있는 AEM Forms 인터랙티브 커뮤니케이션을 설치하고 구성합니다.
uuid: 8acb7f68-0b52-4acd-97e2-af31c9408e8d
topic-tags: installing
discoiquuid: 225f2bc1-6842-4c79-a66d-8024a29325c0
docset: aem65
translation-type: tm+mt
source-git-commit: b703c59d7d913fc890c713c6e49e7d89211fd998
workflow-type: tm+mt
source-wordcount: '1490'
ht-degree: 2%

---


# 대화형 통신 설치 및 구성{#install-and-configure-interactive-communications}

## 소개 {#introduction}

AEM Form은 보안 및 인터랙티브한 문서(예: 비즈니스 서신, 문서, 명세서, 혜택 통지, 마케팅 메일, 청구서 및 환영 키트)의 작성, 수집, 관리 및 전달을 중앙에서 관리할 수 있는 기능을 제공합니다. 이 기능을 대화형 통신이라고 합니다. 이 기능은 AEM Forms 추가 기능 패키지에 포함되어 있습니다. Add-on 패키지는 AEM의 작성자 또는 게시 인스턴스에 배포됩니다.

인터랙티브한 커뮤니케이션 기능을 사용하여 다양한 포맷의 커뮤니케이션을 제작할 수 있습니다. 예: 웹 및 PDF. 인터랙티브한 커뮤니케이션을 AEM Workflow와 통합하여 고객이 원하는 채널을 통해 조합된 커뮤니케이션을 처리하고 고객에게 전달할 수 있습니다. 예를 들어, 이메일을 통해 최종 사용자에게 통신을 보냅니다.

이전 버전에서 업그레이드하고 통신비 관리에 이미 투자한 경우 [호환성 패키지를](../../forms/using/installing-configuring-intreactive-communication-correspondence-management.md#install-compatibility-package) 설치하여 통신비 관리를 계속 사용할 수 있습니다. 상호 작용 통신 및 통신 관리 간의 차이점에 대한 자세한 내용은 [대화형 통신 개요를 참조하십시오](/help/forms/using/interactive-communications-overview.md#interactive-communications-vs-correspondence-management).

AEM Forms은 강력한 엔터프라이즈급 플랫폼입니다. 인터랙티브 커뮤니케이션은 AEM Forms의 기능 중 하나에 불과합니다. 전체 기능 목록은 AEM Forms [소개를 참조하십시오](../../forms/using/introduction-aem-forms.md).

## 배포 토폴로지 {#deployment-topology}

AEM Forms 추가 기능 패키지는 AEM에 배포된 애플리케이션입니다. Interactive Communications 기능을 실행하려면 최소 하나의 AEM Author 및 처리 인스턴스만 필요합니다. 다음 토폴로지는 OSGi 기능에서 AEM Forms 인터랙티브 커뮤니케이션, 통신 관리, AEM Forms 데이터 캡처 및 양식 중심의 워크플로우를 실행하기 위한 토폴로지를 나타냅니다. 토폴로지에 대한 자세한 내용은 AEM Forms용 [아키텍처 및 배포 토폴로지를 참조하십시오](/help/forms/using/aem-forms-architecture-deployment.md).

![권장 토폴로지](assets/recommended-topology.png)

AEM Forms Interactive Communications는 AEM Forms의 작성자 인스턴스에서 관리, 작성 및 에이전트 사용자 인터페이스를 실행합니다. 게시 인스턴스는 최종 사용자가 사용할 수 있는 인터랙티브 커뮤니케이션의 최종 버전을 호스팅합니다.

## 시스템 요구 사항 {#system-requirements}

AEM Forms의 상호 작용 통신 및 통신 관리 기능을 설치하고 구성하기 전에 다음을 확인하십시오.

* 하드웨어 및 소프트웨어 인프라를 갖추고 있습니다. 지원되는 하드웨어 및 소프트웨어에 대한 자세한 목록은 [기술 요구 사항을 참조하십시오](/help/sites-deploying/technical-requirements.md).

* AEM 인스턴스의 설치 경로에 공백이 없습니다.
* AEM 인스턴스가 실행 중입니다. AEM 용어에서 &quot;인스턴스&quot;는 작성 또는 게시 모드에서 서버에서 실행 중인 AEM의 사본입니다. AEM Forms 대화형 통신 및 통신 관리 기능을 실행하려면 하나 이상의 AEM 인스턴스(작성자 또는 처리)가 필요합니다.

   * **작성자**: 컨텐츠를 생성, 업로드 및 편집하고 웹 사이트를 관리하는 데 사용되는 AEM 인스턴스입니다. 컨텐츠가 라이브될 준비가 되면 게시 인스턴스에 복제됩니다.
   * **처리:** 처리 인스턴스는 [딱딱한 AEM Author](/help/forms/using/hardening-securing-aem-forms-environment.md) 인스턴스입니다. 작성 인스턴스를 설정하고 설치를 수행한 후 이를 취소할 수 있습니다.

   * **게시**: 인터넷 또는 내부 네트워크를 통해 대중에게 게시된 컨텐츠를 제공하는 AEM 인스턴스입니다.

* 메모리 요구 사항이 충족되었습니다. AEM Forms 추가 패키지 필요:

   * Microsoft Windows 기반 설치를 위한 15GB의 임시 공간.
   * UNIX 기반 설치를 위한 6GB의 임시 공간.

* UNIX 기반 시스템의 추가 요구 사항: UNIX 기반 운영 체제를 사용하는 경우 해당 운영 체제의 설치 미디어에서 다음 패키지를 설치합니다.

<table>
 <tbody>
  <tr>
   <td>xat</td>
   <td>libxcb</td>
   <td>자유 문자</td>
   <td>libXau</td>
  </tr>
  <tr>
   <td>libSM</td>
   <td>zlib</td>
   <td>libICE</td>
   <td>libuuid</td>
  </tr>
  <tr>
   <td>글리시</td>
   <td>libXext</td>
   <td><p>nss-softokn-freebl</p> </td>
   <td>fontconfig</td>
  </tr>
  <tr>
   <td>libX11</td>
   <td>libXrender</td>
   <td>libXrandr</td>
   <td>libXinerama</td>
  </tr>
 </tbody>
</table>

## AEM Forms 추가 기능 패키지 설치 {#install-aem-forms-add-on-package}

AEM Forms 추가 기능 패키지는 AEM에 배포된 애플리케이션입니다. 이 패키지에는 AEM Forms 대화형 통신, 통신 관리 및 기타 기능이 들어 있습니다. Add-on 패키지를 설치하려면 다음 단계를 수행하십시오.

1. 관리자로 [AEM 서버에](https://localhost:4502) 로그인하고 [패키지 공유를 엽니다](https://localhost:4502/crx/packageshare). 패키지 공유에 로그인하려면 Adobe ID이 필요합니다.
1. AEM [패키지 공유](https://localhost:4502/crx/packageshare/login.html)에서 **AEM 6.5 Forms Add-on 패키지** 또는 **최신 서비스**&#x200B;팩을 검색하고, 운영 체제에 해당하는 패키지를 클릭하고, 다운로드 **를**&#x200B;클릭합니다. 사용권 계약을 읽고 동의한 다음 **확인을 클릭합니다**. 다운로드가 시작됩니다. 다운로드되면 패키지 옆에 **다운로드됨** 단어가 나타납니다.

   버전 번호를 사용하여 추가 기능 패키지를 검색할 수도 있습니다. 최신 패키지의 버전 번호는 [AEM Forms 릴리스 문서를](https://helpx.adobe.com/kr/aem-forms/kb/aem-forms-releases.html) 참조하십시오.

1. 다운로드가 완료되면 **다운로드를 클릭합니다**. 패키지 관리자로 리디렉션됩니다. 패키지 관리자에서 다운로드한 패키지를 검색하고 [설치]를 **클릭합니다**.

   AEM Forms 릴리스 [문서에 나열된 직접 링크를 통해 패키지를 수동으로 다운로드하는 경우 패키지 관리자에 로그인하여 패키지](https://helpx.adobe.com/kr/aem-forms/kb/aem-forms-releases.html) 업로드 ****&#x200B;를 클릭하고 다운로드한 패키지를 선택한 다음 업로드를 클릭합니다. 패키지가 업로드된 후 패키지 이름을 클릭하고 [ **설치]를 클릭합니다.**

1. 패키지가 설치되면 AEM 인스턴스를 다시 시작하라는 메시지가 표시됩니다. **서버를 즉시 다시 시작하지 마십시오.** AEM Forms 서버를 중지하기 전에 AEM-Installation-Directory /crx-quickstart/logs/error.log 파일에 ServiceEvent REGISTERED 및 ServiceEvent UNREGISTERED 메시지가 [나타나지 않고]로그가 안정될 때까지 기다립니다.
1. 모든 작성자 및 게시 인스턴스에 대해 1-4단계를 반복합니다.

## 설치 후 구성 {#post-installation-configurations}

AEM Forms에는 몇 가지 필수 구성 및 선택 구성이 있습니다. 필수 구성에는 BouncyCastle 라이브러리 및 직렬화 에이전트 구성이 포함됩니다. 선택적 구성에는 디스패처 및 Adobe Target 구성이 포함됩니다.

### 필수 설치 후 구성 {#mandatory-post-installation-configurations}

#### RSA 및 BouncyCastle 라이브러리 구성  {#configure-rsa-and-bouncycastle-libraries}

라이브러리를 부트하려면 모든 작성자 및 게시 인스턴스에 대해 다음 단계를 수행하십시오.

1. 기본 AEM 인스턴스를 중지합니다.
1. 편집할 [AEM 설치 디렉토리]\crx-quickstart\conf\sling.properties 파일을 엽니다.

   AEM [설치 디렉토리]\crx-quickstart\bin\start.bat을 사용하여 AEM을 시작한 경우 [AEM_root]\crx-quickstart\에 있는 sling.properties를편집합니다.

1. sling.properties 파일에 다음 속성을 추가합니다.

   ```
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.*
   ```

1. 파일을 저장하고 닫고 AEM 인스턴스를 시작합니다.
1. 모든 작성자 및 게시 인스턴스에 대해 1-4단계를 반복합니다.

#### 직렬화 에이전트 구성 {#configure-the-serialization-agent}

모든 작성자 및 게시 인스턴스에 대해 다음 단계를 수행하여 패키지를 허용 목록에 추가합니다.

1. 브라우저 창에서 AEM Configuration Manager를 엽니다. 기본 URL은 https://&#39;[server]:[port]&#39;/system/console/configMgr입니다.
1. 방화벽 **구성을 검색하고 엽니다**.
1. allowlist **필드에** sun.util.calendar **패키지를** 추가합니다. [저장]을 클릭합니다.
1. 모든 작성자 및 게시 인스턴스에 대해 1-3단계를 반복합니다.

### 설치 후 구성(선택 사항) {#optional-post-installation-configurations}

#### 호환성 패키지 설치 {#install-compatibility-package}

인터랙티브한 커뮤니케이션은 AEM 6.5 Forms에서 고객 커뮤니케이션을 만드는 데 기본적으로 권장됩니다. 이전 버전에서 업그레이드하거나 마이그레이션한 경우 문자(통신 관리)를 계속 사용할 계획인 경우 [AEMFD 호환성 패키지를 설치합니다](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/fd/AEM-FORMS-6.4-COMPAT).

AEM Compatibility 패키지는 AEM 6.4 양식, AEM 6.3 양식 및 AEM 6.5 양식에 있는 AEM 6.2 양식의 다음 자산을 사용할 수 있도록 해줍니다.

* 문서 조각
* 편지
* 데이터 사전
* 응용 양식 더 이상 사용되지 않는 템플릿 및 페이지

#### Dispatcher 구성 {#configure-dispatcher}

Dispatcher이 AEM에 대한 캐싱 및 로드 밸런싱 도구를 사용하고 있습니다. AEM Dispatcher은 AEM 서버를 공격으로부터 보호하는 데에도 도움이 됩니다. 엔터프라이즈급 웹 서버와 함께 Dispatcher을 사용하여 AEM 인스턴스의 보안을 강화할 수 있습니다. Dispatcher을 사용하는 경우 [AEM Forms](https://helpx.adobe.com/kr/experience-manager/dispatcher/using/dispatcher-configuration.html을 참조하십시오.)에 대해 다음 구성을 수행합니다.

1. AEM Forms에 대한 액세스 권한 구성:

   편집할 dispatcher.any 파일을 엽니다. 필터 섹션으로 이동하여 필터 섹션에 다음 필터를 추가합니다.

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   파일을 저장하고 닫습니다. 필터에 대한 자세한 내용은 [Dispatcher 설명서를 참조하십시오](https://helpx.adobe.com/kr/experience-manager/dispatcher/using/dispatcher-configuration.html을 참조하십시오.).

1. 레퍼러 필터 서비스를 구성합니다.

   Apache Felix 구성 관리자에 관리자로 로그인합니다. 구성 관리자의 기본 URL은 https://&#39;server&#39;:[port_number]/system/console/configMgr입니다. [ **구성** ] 메뉴에서 [ **아파치 슬링 레퍼러 필터** ] 옵션을 선택합니다. 호스트 허용 필드에서 디스패처의 호스트 이름을 입력하여 레퍼러로 허용하고 저장을 **클릭합니다**. 항목의 형식은 https://&#39;[server]:[port]&#39;입니다.

#### Adobe Target 통합 {#integrate-adobe-target}

고객이 제공하는 경험에 매료되지 않으면 인터랙티브한 커뮤니케이션을 포기하게 됩니다. 고객이 불만스러워할 수는 있지만 조직의 지원 볼륨 및 비용을 높일 수도 있습니다. 전환율을 높일 수 있는 적합한 고객 경험을 식별하고 제공하는 것은 매우 중요하며 어렵습니다. AEM Forms가 이 문제에 대한 키를 가지고 있습니다.

AEM Forms는 Adobe Marketing Cloud 솔루션인 Adobe Target과 통합되어 다양한 디지털 채널에 개인화되고 매력적인 고객 경험을 제공합니다. Adobe Target을 사용하여 인터랙티브한 커뮤니케이션을 개인화하려면 Adobe Target [를 AEM Forms과 통합하십시오](../../forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms).

#### 양식 데이터 모델에 대한 SSL 통신 구성  {#configure-ssl-communcation-for-form-data-model}

양식 데이터 모델에 대해 SSL 통신을 활성화할 수 있습니다. 양식 데이터 모델에 대해 SSL 통신을 활성화하려면 AEM Forms 인스턴스를 시작하기 전에 모든 인스턴스의 Java Trust Store에 인증서를 추가하십시오. 아래 명령을 실행하여 인증서를 추가할 수 있습니다.

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

## 다음 단계 {#next-steps}

대화형 통신 및 통신 관리 기능을 사용할 환경을 구성했습니다. 이제 기능을 사용하기 위한 단계는 다음과 같습니다.

* [통신 관리 개요](/help/forms/using/interactive-communications-overview.md)

* [인터랙티브한 커뮤니케이션 제작](../../forms/using/create-interactive-communication.md)

* [서신 관리 서신 만들기](../../forms/using/create-letter.md)

