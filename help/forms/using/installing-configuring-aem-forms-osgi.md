---
title: 데이터 캡처 기능 설치 및 구성
seo-title: 데이터 캡처 기능 설치 및 구성
description: 적응형 양식, PDF forms 및 HTML5 Forms을 설치 및 구성합니다. 적응형 양식에 대해 Adobe Analytics 및 Adobe Target을 구성하여 양식 사용을 분석하고 프로필을 기반으로 사용자를 타깃팅할 수 있습니다.
seo-description: 적응형 양식, PDF forms 및 HTML5 Forms을 설치 및 구성합니다. 적응형 양식에 대해 Adobe Analytics 및 Adobe Target을 구성하여 양식 사용을 분석하고 프로필을 기반으로 사용자를 타깃팅할 수 있습니다.
uuid: 5d49032a-4dea-4f21-9dad-a7a30c5872ea
topic-tags: installing
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dfc473eb-6091-4f5d-a5a0-789972c513a9
docset: aem65
role: Administrator
exl-id: 19b5765e-50bc-4fed-8af5-f6bb464516c8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1910'
ht-degree: 5%

---

# 데이터 캡처 기능 설치 및 구성{#install-and-configure-data-capture-capabilities}

## 소개 {#introduction}

AEM Forms은 최종 사용자의 데이터를 가져오는 양식 세트를 제공합니다.적응형 양식, HTML5 Forms 및 PDF forms. 또한 웹 페이지에 사용 가능한 모든 양식을 나열하고 양식의 사용을 분석하며 프로필을 기반으로 사용자를 타깃팅하는 도구를 제공합니다. 이러한 기능은 AEM Forms 추가 기능 패키지에 포함되어 있습니다. 추가 기능 패키지는 AEM의 작성자 또는 게시 인스턴스에 배포됩니다.

**적응형 양식:** 이러한 양식은 장치의 화면 크기에 따라 모양은 변경되며, 매력적이며, 자연에서 상호 작용합니다. 적용형 Forms은 Adobe Analytics, Adobe Sign 및 Adobe Target과 통합할 수도 있습니다. Adobe Campaign을 사용하면 인구 통계학 및 기타 기능을 기반으로 사용자에게 개인화된 양식 및 프로세스 중심의 경험을 제공할 수 있습니다. 적응형 양식을 Adobe Sign과 통합할 수도 있습니다.

**PDF 양식** 은 PDF 문서 내에서 픽셀 단위의 완벽한 인쇄 및 디지털 정보 캡처에 적합합니다. 디지털 아바타에서는 Adobe Acrobat 또는 Acrobat Reader을 사용하여 이러한 양식을 채울 수 있습니다. 웹 사이트에서 이러한 양식을 호스팅하거나 forms 포털을 사용하여 AEM 사이트에 이러한 양식을 나열할 수 있습니다. 이러한 양식을 다른 사용자에게 이메일로 첨부 파일로 보낼 수도 있습니다. 이러한 양식은 데스크톱 환경에 가장 적합합니다.

**HTML5** 형식은 브라우저에 친숙한 PDF forms 버전입니다. HTML5 Forms은 PDF 플러그인을 지원하지 않는 환경에 적합합니다. HTML5 Forms을 사용하면 XFA 기반 PDF가 지원되지 않는 모바일 장치 및 데스크탑 브라우저에서 XFA 기반 양식을 렌더링할 수 있습니다. 이러한 양식은 태블릿 및 데스크탑 환경에 가장 적합합니다.

AEM Forms은 강력한 엔터프라이즈급 플랫폼이며 데이터 캡처(적응형 양식, PDF forms 및 HTML5 Forms)은 AEM Forms의 기능 중 하나입니다. 전체 기능 목록에 대해서는 [AEM Forms 소개](/help/forms/using/introduction-aem-forms.md)를 참조하십시오.

## 배포 토폴로지 {#deployment-topology}

AEM Forms 추가 기능 패키지는 AEM에 배포된 애플리케이션입니다. AEM Forms 데이터 캡처 기능을 실행하려면 최소 1개의 AEM 작성자 및 AEM 게시 인스턴스만 필요합니다. AEM Forms AEM Forms 데이터 캡처 기능을 실행하려면 다음 토폴로지를 사용하는 것이 좋습니다. 토폴로지에 대한 자세한 내용은 [AEM Forms용 아키텍처 및 배포 토폴로지](/help/forms/using/aem-forms-architecture-deployment.md)를 참조하십시오.

![권장 토폴로지](assets/recommended-topology.png)

## 시스템 요구 사항 {#system-requirements}

AEM Forms의 데이터 캡처 기능을 설치 및 구성하기 전에 다음을 확인하십시오.

* 하드웨어 및 소프트웨어 인프라가 제대로 구축되어 있습니다. 지원되는 하드웨어 및 소프트웨어의 자세한 목록은 [기술 요구 사항](/help/sites-deploying/technical-requirements.md)을 참조하십시오.

* AEM 인스턴스의 설치 경로에 공백이 들어 있지 않습니다.
* AEM 인스턴스가 실행 중입니다. Windows 사용자의 경우 관리자 권한 모드로 AEM 인스턴스를 설치합니다. AEM 용어에서 &quot;인스턴스&quot;는 작성자 또는 게시 모드에서 서버에서 실행되는 AEM의 사본입니다. AEM Forms 데이터 캡처 기능을 실행하려면 두 개 이상의 [AEM 인스턴스(작성자 및 게시 한 개)가 필요합니다.](/help/sites-deploying/deploy.md)

   * **작성자**:컨텐츠를 작성, 업로드 및 편집하고 웹 사이트를 관리하는 데 사용되는 AEM 인스턴스입니다. 컨텐츠가 라이브로 전환될 준비가 되면 게시 인스턴스에 복제됩니다.
   * **게시**:인터넷 또는 내부 네트워크를 통해 대중에게 게시된 컨텐츠를 제공하는 AEM 인스턴스입니다.

* 메모리 요구 사항이 충족되었습니다. AEM Forms 추가 기능 패키지에는 다음이 필요합니다.

   * Microsoft Windows 기반 설치를 위한 15GB의 임시 공간.
   * UNIX 기반 설치를 위한 6GB의 임시 공간.

* 작성자 및 게시 인스턴스에 대한 복제 및 역방향 복제가 설정됩니다. 자세한 내용은 [복제](/help/sites-deploying/replication.md)를 참조하십시오.
* UNIX 기반 시스템의 경우:

   * 설치 미디어에서 다음 32비트 패키지를 설치합니다.

<table>
 <tbody>
  <tr>
   <td>expand</td>
   <td>fontconfig</td>
   <td>freetype</td>
   <td>글라이치</td>
  </tr>
  <tr>
   <td>libcurl</td>
   <td>libICE</td>
   <td>libicu</td>
   <td>libSM</td>
  </tr>
  <tr>
   <td>libuuid</td>
   <td>libX11</td>
   <td><p>libXau</p> </td>
   <td>libxcb</td>
  </tr>
  <tr>
   <td>libXext</td>
   <td>libXinerama</td>
   <td>libXrandr</td>
   <td>libXrender</td>
  </tr>
  <tr>
   <td>nss-softokn-freebl</td>
   <td>OpenSSL</td>
   <td>zlib</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* 서버에 OpenSSL이 이미 설치되어 있다면 최신 버전으로 업그레이드하십시오.
>* libcurl.so, libcrypto.so 및 libssl.so를 각각 최신 버전의 libcurl, libcrypto 및 libssl 라이브러리를 가리킵니다.

>



* 설치 미디어에서 다음 64비트 패키지를 설치합니다.

   * libicu

## AEM Forms 추가 기능 패키지 설치 {#install-aem-forms-add-on-package}

AEM Forms 추가 기능 패키지는 AEM에 배포된 애플리케이션입니다. 이 패키지에는 AEM Forms 데이터 캡처 및 기타 기능이 포함되어 있습니다. 추가 기능 패키지를 설치하려면 다음 단계를 수행하십시오.

1. [소프트웨어 배포](https://experience.adobe.com/downloads)를 엽니다. 소프트웨어 배포에 로그인하려면 Adobe ID가 필요합니다.
1. 헤더 메뉴에 제공된 **[!UICONTROL Adobe Experience Manager]**&#x200B;를 누릅니다.
1. **[!UICONTROL 필터]** 섹션에서 다음을 수행합니다.
   1. **[!UICONTROL 솔루션]** 드롭다운 목록에서 **[!UICONTROL Forms]**&#x200B;을 선택합니다.
   2. 패키지의 버전 및 유형을 선택합니다. **[!UICONTROL 다운로드 검색]** 옵션을 사용하여 결과를 필터링할 수도 있습니다.
1. 운영 체제에 해당하는 패키지 이름을 탭하고 **[!UICONTROL EULA 약관 동의]**&#x200B;를 선택한 다음 **[!UICONTROL 다운로드]**&#x200B;를 탭합니다.
1. [패키지 관리자](https://docs.adobe.com/content/help/ko-KR/experience-manager-65/administering/contentmanagement/package-manager.html)를 열고 **[!UICONTROL 패키지 업로드]**&#x200B;를 클릭하여 패키지를 업로드합니다.
1. 패키지를 선택하고 **[!UICONTROL 설치]**&#x200B;를 클릭합니다.

   [AEM Forms 릴리스](https://helpx.adobe.com/kr/aem-forms/kb/aem-forms-releases.html) 문서에 나열된 직접 링크를 통해 패키지를 다운로드할 수도 있습니다.
1. 패키지가 설치되면 AEM 인스턴스를 다시 시작하라는 메시지가 표시됩니다. **서버를 즉시 다시 시작하지 마십시오.** AEM Forms 서버를 중지하기 전에 ServiceEvent REGISTERED 및 ServiceEvent UNREGISTERED 메시지가 파일에 표시되지 않고 로그 `[AEM-Installation-Directory]/crx-quickstart/logs/error.log` 가 안정적일 때까지 기다리십시오.
1. 모든 작성자 및 게시 인스턴스에 대해 1-7단계를 반복합니다.

### (Windows 전용) Visual Studio 재배포용 파일 자동 설치 {#automatic-installation-visual-studio-redistributables}

상위 모드에서 AEM 인스턴스를 설치하면 AEM Forms 추가 기능 패키지를 설치하는 동안 누락된 Visual Studio 재배포용 변수가 자동으로 설치됩니다.

Visual Studio 재배포용 파일이 자동으로 설치되어 있는지 확인하려면 `/crx-repository/logs/` 디렉터리에서 사용 가능한 `error.log` 파일을 엽니다. 로그에는 다음 메시지가 포함됩니다.

`Redist <service name> already installed on system, will not attempt re-installation`

재배포용 파일을 설치하지 못하면 로그에 다음 메시지가 포함됩니다.

`Current user does not have elevated privileges, aborting installation of redist <service name>`

이 문제를 해결하려면 AEM 서버를 다시 시작하고, 높은 모드로 AEM을 설치한 다음 AEM Forms 추가 기능 패키지를 설치하십시오.

권한 검사가 실패하면 로그에 다음 메시지가 포함됩니다.

`Privilege escalation check failed with error: <error message>`

## 설치 후 구성 {#post-installation-configurations}

AEM Forms에는 몇 가지 필수 및 선택적 구성이 있습니다. 필수 구성에는 BoundcyCastle 라이브러리 및 직렬화 에이전트 구성이 포함됩니다. 선택적 구성에는 Dispatcher 구성, Forms 포털, Adobe Sign, Adobe Analytics 및 Adobe Target 구성이 포함됩니다.

### 필수 설치 후 구성 {#mandatory-post-installation-configurations}

#### RSA 및 BouncyCastle 라이브러리 구성 {#configure-rsa-and-bouncycastle-libraries}

라이브러리를 부팅하려면 모든 작성자 및 게시 인스턴스에서 다음 단계를 수행하십시오.

1. 기본 AEM 인스턴스를 중지합니다.
1. 편집할 `[AEM installation directory]\crx-quickstart\conf\sling.properties` 파일을 엽니다.

   `[AEM installation directory]\crx-quickstart\bin\start.bat` 을 사용하여 AEM을 시작하는 경우 `[AEM_root]\crx-quickstart\`에 있는 sling.properties를 편집합니다.

1. sling.properties 파일에 다음 속성을 추가합니다.

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. 파일을 저장하고 닫고 AEM 인스턴스를 시작합니다.
1. 모든 작성자 및 게시 인스턴스에서 1-4단계를 반복합니다.

#### 직렬화 에이전트 {#configure-the-serialization-agent} 구성

모든 작성자 및 게시 인스턴스에서 다음 단계를 수행하여 패키지를 페이지에 허용 목록에 추가하다 추가합니다.

1. 브라우저 창에서 AEM 구성 관리자를 엽니다. 기본 URL은 `https://'[server]:[port]'/system/console/configMgr`.
1. **com.adobe.cq.deservfw.impl.DeserializationFirewallImpl.name**&#x200B;을(를) 검색하고 구성을 엽니다.
1. **sun.util.calendar** 패키지를 **허용 목록에 추가하다** 필드에 추가합니다. **저장**&#x200B;을 클릭합니다.
1. 모든 작성자 및 게시 인스턴스에서 1-3단계를 반복합니다.

### 설치 후 구성 옵션 {#optional-post-installation-configurations}

#### Dispatcher 구성 {#configure-dispatcher}

Dispatcher는 엔터프라이즈급 웹 서버와 함께 사용할 수 있는 Adobe Experience Manager의 캐싱 및/또는 로드 밸런싱 도구입니다. [Dispatcher](https://helpx.adobe.com/kr/experience-manager/dispatcher/using/dispatcher-configuration.html을 참조하십시오.)를 사용하는 경우 AEM Forms에 대해 다음 구성을 수행하십시오.

1. AEM Forms에 대한 액세스 구성:

   편집할 dispatcher.any 파일을 엽니다. 필터 섹션으로 이동하고 필터 섹션에 다음 필터를 추가합니다.

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   파일을 저장하고 닫습니다. 필터에 대한 자세한 내용은 [Dispatcher 설명서](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)를 참조하십시오.

1. 레퍼러 필터 서비스를 구성합니다.

   관리자로 Apache Felix 구성 관리자에 로그인합니다. 구성 관리자의 기본 URL은 `https://[server]:[port_number]/system/console/configMgr`입니다. **구성** 메뉴에서 **Apache Sling 레퍼러 필터** 옵션을 선택합니다. 호스트 허용 필드에 디스패처의 호스트 이름을 입력하여 레퍼러로 허용하고 **저장**&#x200B;을 클릭합니다. 항목의 형식은 &#39;https://[server]:[port]&#39;입니다.

#### 캐시 구성 {#configure-cache}

캐싱은 데이터 액세스 시간을 단축하고, 지연을 줄이고, 입출력(I/O) 속도를 향상시키는 메커니즘입니다. 적응형 양식 캐시는 사전 채워진 데이터를 저장하지 않고 적응형 양식의 HTML 콘텐츠 및 JSON 구조만 저장합니다. 적응형 양식을 렌더링하는 데 필요한 시간을 줄이는 데 도움이 됩니다.

* 적응형 양식 캐시를 사용하는 경우 [AEM Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)를 사용하여 적응형 양식의 클라이언트 라이브러리(CSS 및 JavaScript)를 캐시합니다.
* 사용자 지정 구성 요소를 개발하는 동안 개발에 사용되는 서버에서 적응형 양식 캐시를 사용하지 않도록 설정하십시오.

적응형 양식 캐시를 구성하려면 다음 단계를 수행하십시오.

1. https://&#39;[server]:[port]&#39;/system/console/configMgr에서 AEM 웹 콘솔 구성 관리자로 이동합니다.
1. **적응형 양식 및 대화형 통신 웹 채널 구성**&#x200B;을 클릭하여 구성 값을 편집합니다. 구성 값 편집 대화 상자에서 AEM Forms 서버의 인스턴스가 캐시할 수 있는 최대 양식 또는 문서 수를 **적응형 Forms** 수 필드에 지정합니다. 기본값은 100입니다. **저장**&#x200B;을 클릭합니다.

   >[!NOTE]
   >
   >캐시를 비활성화하려면 적응형 Forms 수 필드의 값을 **0**&#x200B;로 설정하십시오. 캐시 구성을 비활성화하거나 변경하면 캐시가 재설정되고 모든 양식 및 문서가 캐시에서 제거됩니다.

#### 양식 데이터 모델 {#configure-ssl-communcation-for-form-data-model}에 대한 SSL 통신 구성

양식 데이터 모델에 대해 SSL 통신을 활성화할 수 있습니다. 양식 데이터 모델에 대해 SSL 통신을 사용하려면 AEM Forms 인스턴스를 시작하기 전에 모든 인스턴스의 Java Trust Store에 인증서를 추가하십시오. 아래 명령을 실행하여 인증서를 추가할 수 있습니다.&quot;

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

#### Adobe Sign 구성 {#configure-adobe-sign}

Adobe Sign을 사용하면 적응형 양식에 전자 서명 워크플로우를 사용할 수 있습니다. 전자 서명은 법률, 영업, 급여, 인적 자원 관리 및 기타 여러 분야에 대한 문서를 처리하기 위한 워크플로우를 개선합니다.

일반적인 Adobe Sign 및 적응형 양식 시나리오에서 사용자는 적응형 양식을 **서비스**&#x200B;에 적용합니다. 예를 들어, 신용카드 신청서와 시민 혜택 양식입니다. 사용자가 애플리케이션 양식을 작성, 제출 및 서명하면 추가 작업을 위해 양식이 서비스 공급자에게 전송됩니다. 서비스 제공업체는 애플리케이션을 검토하고 Adobe Sign을 사용하여 승인된 애플리케이션을 표시합니다. 유사한 전자 서명 워크플로우를 활성화하기 위해 Adobe Sign을 AEM Forms과 통합할 수 있습니다.

Adobe Sign을 AEM Forms과 함께 사용하려면 [Adobe Sign을 AEM Forms과 통합](/help/forms/using/adobe-sign-integration-adaptive-forms.md).

#### Adobe Analytics 구성 {#configure-adobe-analytics}

AEM Forms은 게시된 양식 및 문서에 대한 성능 지표를 캡처하고 추적할 수 있도록 Adobe Analytics과 통합됩니다. 이러한 지표를 분석하기 위한 목적은 양식이나 문서를 보다 유용하게 사용할 수 있도록 하는 데 필요한 변경 사항에 대한 데이터를 기반으로 현명한 결정을 내리는 것입니다.

AEM Forms에서 Adobe Analytics을 사용하려면 [분석 및 보고서 구성](/help/forms/using/configure-analytics-forms-documents.md)을 참조하십시오.

#### Adobe Target 통합 {#integrate-adobe-target}

고객이 이 기능을 제공하지 않는 경험을 통해 양식을 포기할 가능성이 높습니다. 고객에게 좌절감을 주지만 조직에 대한 지원 볼륨과 비용을 늘릴 수도 있습니다. 전환율을 높일 수 있는 올바른 고객 경험을 식별 및 제공하기 어려운 것도 중요합니다. AEM forms는 이 문제의 주요 해결방법을 제공합니다.

AEM Forms는 Adobe Marketing Cloud 솔루션인 Adobe Target과 통합되어 있으며, 여러 디지털 채널에서 개인화되고 매력적인 고객 경험을 제공할 수 있습니다. Adobe Target을 사용하여 A/B 테스트 적응형 양식을 사용하려면 [Adobe Target을 AEM Forms과 통합](/help/forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms).

## 다음 단계 {#next-steps}

AEM Forms 데이터 캡처 기능을 사용하는 환경을 구성했습니다. 이제 기능을 사용하기 위한 다음 단계는 다음과 같습니다.

* [첫 번째 적응형 양식 만들기](/help/forms/using/create-your-first-adaptive-form.md)
* [첫 번째 PDF 양식 만들기](http://www.adobe.com/go/learn_aemforms_designer_quick_start_65)
* [HTML5 Forms 소개](/help/forms/using/introduction.md)
