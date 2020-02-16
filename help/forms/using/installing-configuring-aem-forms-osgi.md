---
title: 데이터 캡처 기능 설치 및 구성
seo-title: 데이터 캡처 기능 설치 및 구성
description: 적응형 양식, PDF 양식 및 HTML5 양식 설치 및 구성 적응형 양식용 Adobe Analytics와 Adobe Target을 구성하여 양식 사용을 분석하고 프로파일을 기반으로 사용자를 타깃팅합니다.
seo-description: 적응형 양식, PDF 양식 및 HTML5 양식 설치 및 구성 적응형 양식용 Adobe Analytics와 Adobe Target을 구성하여 양식 사용을 분석하고 프로파일을 기반으로 사용자를 타깃팅합니다.
uuid: 5d49032a-4dea-4f21-9dad-a7a30c5872ea
topic-tags: installing
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dfc473eb-6091-4f5d-a5a0-789972c513a9
docset: aem65
translation-type: tm+mt
source-git-commit: 5831c173114a5a6f741e0721b55d85a583e52f78

---


# 데이터 캡처 기능 설치 및 구성{#install-and-configure-data-capture-capabilities}

## 소개 {#introduction}

AEM Forms는 최종 사용자로부터 데이터를 얻기 위한 양식 세트를 제공합니다.적응형 양식, HTML5 양식 및 PDF 양식 또한 웹 페이지에 사용 가능한 모든 양식을 나열하고, 양식 사용을 분석하고, 프로필을 기반으로 사용자를 타깃팅하는 도구를 제공합니다. 이러한 기능은 AEM Forms 추가 기능 패키지에 포함되어 있습니다. Add-on 패키지는 AEM의 작성자 또는 게시 인스턴스에 배포됩니다.

**** 적응형 양식:이러한 양식은 장치의 화면 크기에 따라 모양이 변경되며, 매력적이고 인터랙티브한 요소가 됩니다. 적응형 양식은 Adobe Analytics, Adobe Sign 및 Adobe Target과 통합할 수 있습니다. 이를 통해 사용자의 인구 통계와 기타 기능을 기반으로 개인화된 양식과 프로세스 중심의 경험을 제공할 수 있습니다. 또한 적응형 양식을 Adobe Sign과 통합할 수 있습니다.

**PDF** 양식은 픽셀 하나까지 완벽한 인쇄 및 디지털 정보 캡처에 적합합니다. 디지털 아바타에서는 Adobe Acrobat 또는 Acrobat Reader를 사용하여 이러한 양식을 채울 수 있습니다. 웹 사이트에서 이러한 양식을 호스팅하거나 양식 포털을 사용하여 AEM 사이트에 이러한 양식을 나열할 수 있습니다. 이러한 양식을 다른 사람에게 첨부 파일로 이메일로 보낼 수도 있습니다. 이러한 양식은 데스크탑 환경에 가장 적합합니다.

**HTML5** Forms는 브라우저와 유사한 PDF Forms 버전입니다. HTML5 Forms는 PDF 플러그인을 지원하지 않는 환경에 적합합니다. HTML5 양식을 사용하면 XFA 기반 PDF가 지원되지 않는 모바일 디바이스 및 데스크탑 브라우저에서 XFA 기반 양식을 렌더링할 수 있습니다. 이러한 양식은 태블릿 및 데스크탑 환경에 가장 적합합니다.

AEM Forms는 강력한 엔터프라이즈급 플랫폼이며 데이터 캡처(적응형 양식, PDF 양식 및 HTML5 양식)는 AEM Forms 기능 중 하나에 불과합니다. 전체 기능 목록은 AEM Forms [소개를 참조하십시오](/help/forms/using/introduction-aem-forms.md).

## 배포 토폴로지 {#deployment-topology}

AEM Forms Add-on 패키지는 AEM에 배포된 애플리케이션입니다. AEM Forms 데이터 캡처 기능을 실행하려면 최소 하나의 AEM 작성자 및 AEM 게시 인스턴스만 필요합니다. 다음 토폴로지는 AEM Forms AEM Forms 데이터 캡처 기능을 실행하는 것이 좋습니다. 토폴로지에 대한 자세한 내용은 AEM Forms [용 아키텍처 및 배포 토폴로지를 참조하십시오](/help/forms/using/aem-forms-architecture-deployment.md).

![권장 토폴로지](assets/recommended-topology.png)

## 시스템 요구 사항 {#system-requirements}

AEM Forms의 데이터 캡처 기능을 설치하고 구성하기 전에 다음을 확인하십시오.

* 하드웨어 및 소프트웨어 인프라가 적소에 있습니다. 지원되는 하드웨어 및 소프트웨어에 대한 자세한 목록은 [기술 요구 사항을](/help/sites-deploying/technical-requirements.md)참조하십시오.

* AEM 인스턴스의 설치 경로에 공백이 없습니다.
* AEM 인스턴스가 실행 중입니다. AEM 용어에서 &quot;인스턴스&quot;는 작성자 또는 게시 모드에서 서버에서 실행되는 AEM의 복사본입니다. AEM Forms 데이터 캡처 기능을 실행하려면 최소 두 개의 [AEM 인스턴스(작성자 및 게시](/help/sites-deploying/deploy.md) )가 필요합니다.

   * **작성자**:컨텐츠를 작성, 업로드 및 편집하고 웹 사이트를 관리하는 데 사용되는 AEM 인스턴스입니다. 컨텐츠를 라이브할 준비가 되면 게시 인스턴스에 복제됩니다.
   * **게시**:인터넷 또는 내부 네트워크를 통해 게시된 컨텐츠를 대중에게 제공하는 AEM 인스턴스입니다.

* 메모리 요구 사항이 충족되었습니다. AEM Forms Add-on 패키지에 필요한 사항:

   * Microsoft Windows 기반 설치를 위한 15GB의 임시 공간.
   * UNIX 기반 설치를 위한 6GB의 임시 공간.

* 작성자 및 게시 인스턴스에 대한 복제 및 역 복제가 설정됩니다. 자세한 내용은 복제를 [참조하십시오](/help/sites-deploying/replication.md).
* UNIX 기반 시스템의 경우:

   * 설치 미디어에서 다음 32비트 패키지를 설치합니다.

<table>
 <tbody>
  <tr>
   <td>expat</td>
   <td>fontconfig</td>
   <td>freetype</td>
   <td>글리시</td>
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
>* OpenSSL이 서버에 이미 설치되어 있는 경우 최신 버전으로 업그레이드하십시오.
>* libcurl.so, libcrypto.so 및 libssl.so 심링크를 각각 최신 버전의 libcurl, libcrypto 및 libssl 라이브러리를 가리킵니다.
>



* 설치 미디어에서 다음 64비트 패키지를 설치합니다.

   * libicu

## Install AEM Forms add-on package {#install-aem-forms-add-on-package}

AEM Forms Add-on 패키지는 AEM에 배포된 애플리케이션입니다. 이 패키지에는 AEM Forms 데이터 캡처 및 기타 기능이 포함되어 있습니다. Add-on 패키지를 설치하려면 다음 단계를 수행하십시오.

1. AEM 서버에 [](https://localhost:4502) 관리자로 로그인하고 [패키지 공유를](https://localhost:4502/crx/packageshare)엽니다. 패키지 공유에 로그인하려면 Adobe ID가 필요합니다.
1. AEM [패키지 공유에서](https://localhost:4502/crx/packageshare/login.html)AEM **6.5 Forms 추가 기능 패키지를**&#x200B;검색하고 운영 체제에 적용 가능한 패키지를 클릭한 다음 다운로드를 **클릭합니다**. 라이센스 계약을 읽고 동의한 다음 확인을 **클릭합니다**. 다운로드가 시작됩니다. 다운로드하면 패키지 **옆에** 다운로드된 단어가 나타납니다.

   버전 번호를 사용하여 추가 기능 패키지를 검색할 수도 있습니다. 최신 패키지의 버전 번호는 AEM Forms 릴리스 [문서를](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) 참조하십시오.

1. 다운로드가 완료되면 [다운로드됨]을 **클릭합니다**. 패키지 관리자로 리디렉션됩니다. 패키지 관리자에서 다운로드한 패키지를 검색하고 설치를 **클릭합니다**.

   AEM Forms 릴리스 [문서에 나열된 직접 링크를 통해 패키지를 수동으로 다운로드하는 경우 패키지](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) 관리자에 **로그인하고 패키지 업로드를**&#x200B;클릭한 다음다운로드한 패키지를 선택하고 업로드를 클릭합니다. 패키지가 업로드되면 패키지 이름을 클릭하고 설치를 **클릭합니다.**

1. 패키지가 설치되면 AEM 인스턴스를 다시 시작하라는 메시지가 표시됩니다. **서버를 즉시 다시 시작하지 마십시오.** AEM Forms 서버를 중지하기 전에 ServiceEvent REGISTERED 및 ServiceEvent UNREGISTERED 메시지가 `[AEM-Installation-Directory]/crx-quickstart/logs/error.log` 파일에 나타나지 않고 로그가 안정될 때까지 기다립니다.
1. 모든 작성자 및 게시 인스턴스에 대해 1-4단계를 반복합니다.

## 설치 후 구성 {#post-installation-configurations}

AEM Forms에는 몇 가지 필수 구성 및 선택 사항이 있습니다. 필수 구성에는 BouncyCastle 라이브러리 및 직렬화 에이전트 구성이 포함됩니다. 선택적인 구성에는 디스패처 구성, 양식 포털, Adobe Sign, Adobe Analytics 및 Adobe Target이 포함됩니다.

### 필수 설치 후 구성 {#mandatory-post-installation-configurations}

#### RSA 및 BouncyCastle 라이브러리 구성 {#configure-rsa-and-bouncycastle-libraries}

모든 작성자 및 게시 인스턴스에 대해 다음 단계를 수행하여 라이브러리를 부트합니다.

1. 기본 AEM 인스턴스를 중지합니다.
1. AEM [설치 디렉토리]\crx-quickstart\conf\sling.properties 파일을 열어 편집합니다.

   AEM [설치 디렉토리]\crx-quickstart\bin\start.bat을 사용하여 AEM을 시작한 경우 AEM_root [\crx-quickstart\폴더에 있는 sling.]properties를 편집합니다.

1. sling.properties 파일에 다음 속성을 추가합니다.

   ```
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.*
   ```

1. 파일을 저장하고 닫고 AEM 인스턴스를 시작합니다.
1. 모든 작성자 및 게시 인스턴스에 대해 1-4단계를 반복합니다.

#### 직렬화 에이전트 구성 {#configure-the-serialization-agent}

모든 작성자 및 게시 인스턴스에 대해 다음 단계를 수행하여 패키지를 화이트리스트합니다.

1. 브라우저 창에서 AEM 구성 관리자를 엽니다. 기본 URL은 `https://[server]:[port]/system/console/configMgr`입니다.
1. com.adobe.cq.deserfw.impl. **DeserializationFirewallImpl.name** 을 검색하고 구성을 엽니다.
1. sun.util.calendar **패키지를** 화이트리스트 **** 필드에 추가합니다. **저장**&#x200B;을 클릭합니다.
1. 모든 작성자 및 게시 인스턴스에 대해 1-3단계를 반복합니다.

### 설치 후 구성(옵션) {#optional-post-installation-configurations}

#### 발송자 구성 {#configure-dispatcher}

디스패처가 AEM에 대한 캐싱 및 로드 밸런싱 도구를 사용하고 있습니다. AEM Dispatcher는 AEM 서버를 공격으로부터 보호하는 데에도 도움이 됩니다. 엔터프라이즈급 웹 서버와 함께 Dispatcher를 사용하여 AEM 인스턴스의 보안을 강화할 수 있습니다. Dispatcher를 사용하는 [경우](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)AEM Forms에 대해 다음 구성을 수행하십시오.

1. AEM Forms에 대한 액세스 권한 구성:

   편집하기 위해 dispatcher.any 파일을 엽니다. 필터 섹션으로 이동하여 필터 섹션에 다음 필터를 추가합니다.

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   파일을 저장하고 닫습니다. 필터에 대한 자세한 내용은 Dispatcher [설명서를](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)참조하십시오.

1. 레퍼러 필터 서비스를 구성합니다.

   Apache Felix 구성 관리자에 관리자로 로그인합니다. 구성 관리자의 기본 URL은 https://[server]:[port_number]/system/console/configMgr입니다. **구성 **메뉴에서 Apache Sling 레퍼러 **필터** 옵션을 선택합니다. 호스트 허용 필드에 디스패처의 호스트 이름을 입력하여 레퍼러로 허용하고 저장을 **클릭합니다**. 항목의 형식은 https://[server]:[port]입니다.

#### 캐시 구성 {#configure-cache}

캐싱은 데이터 액세스 시간을 단축하고 지연 시간을 줄이며 입출력 속도를 향상시키는 메커니즘입니다. 적응형 양식 캐시는 사전 채워진 데이터를 저장하지 않고 적응형 양식의 HTML 컨텐츠 및 JSON 구조만 저장합니다. 적응형 양식을 렌더링하는 데 필요한 시간을 줄이는 데 도움이 됩니다.

* 적응형 양식 캐시 사용 시 AEM [Dispatcher를](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html) 사용하여 적응형 양식의 클라이언트 라이브러리(CSS 및 JavaScript)를 캐시합니다.
* 사용자 정의 구성 요소를 개발하는 동안 개발에 사용되는 서버에서 응용 양식 캐시를 사용하지 않도록 설정하십시오.

적응형 양식 캐시를 구성하려면 다음 단계를 수행하십시오.

1. https://의 AEM 웹 콘솔 구성[관리자로 이동합니다].[port]/system/console/configMgr.
1. 적응형 **양식 및 대화형 통신 웹 채널 구성을** 클릭하여 구성 값을 편집합니다. 구성 값 편집 대화 상자에서 적응형 양식 수 필드에 AEM Forms 서버의 인스턴스가 캐싱할 수 있는 최대 양식 또는 문서 **수를 지정합니다** . 기본값은 100입니다. **저장**&#x200B;을 클릭합니다.

   >[!NOTE]
   >
   >캐시를 비활성화하려면 [적응형 양식 수] 필드의 값을 **0으로 설정합니다**. 캐시는 재설정되고 캐시 구성을 비활성화하거나 변경하면 모든 양식과 문서가 캐시에서 제거됩니다.

#### 양식 데이터 모델에 대한 SSL 통신 구성 {#configure-ssl-communcation-for-form-data-model}

양식 데이터 모델에 대해 SSL 통신을 활성화할 수 있습니다. 양식 데이터 모델에 대해 SSL 통신을 활성화하려면 AEM Forms 인스턴스를 시작하기 전에 모든 인스턴스의 Java Trust Store에 인증서를 추가하십시오. 아래 명령을 실행하여 인증서를 추가할 수 있습니다.&quot;

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

#### Adobe Sign 구성 {#configure-adobe-sign}

Adobe Sign을 사용하면 적응형 양식을 위한 전자 서명 워크플로우를 수행할 수 있습니다. 전자 서명은 법률, 영업, 급여, 인사 관리 등 다양한 분야의 문서를 처리하는 워크플로우를 향상시켜 줍니다.

일반적인 Adobe Sign 및 적응형 양식 시나리오에서 사용자는 적응형 양식을 채워 서비스에 ****&#x200B;적용합니다. 예를 들어 신용 카드 신청서와 시민 혜택 양식이 있습니다. 사용자가 애플리케이션 양식을 채우고 제출 및 서명하면 추가 작업을 위해 양식이 서비스 공급업체에 전송됩니다. 서비스 제공업체는 애플리케이션을 검토하고 Adobe Sign을 사용하여 애플리케이션을 승인했음을 표시합니다. 유사한 전자 서명 워크플로우를 사용하려면 AEM Forms와 Adobe Sign을 통합할 수 있습니다.

AEM Forms에서 Adobe Sign을 사용하려면 [AEM Forms와 Adobe Sign을 통합하십시오](/help/forms/using/adobe-sign-integration-adaptive-forms.md).

#### Adobe Analytics 구성 {#configure-adobe-analytics}

AEM Forms는 게시된 양식 및 문서에 대한 성능 지표를 캡처하고 추적할 수 있는 Adobe Analytics와 통합되어 있습니다. 이러한 지표를 분석하기 위한 목표는 양식이나 문서를 보다 유용하게 만드는 데 필요한 변경 사항에 대한 데이터를 기반으로 현명한 결정을 내리는 것입니다.

AEM Forms에서 Adobe Analytics를 사용하려면 분석 [및 보고서](/help/forms/using/configure-analytics-forms-documents.md)구성을 참조하십시오.

#### Adobe Target 통합 {#integrate-adobe-target}

고객이 제공하는 경험이 매력적이지 않으면 양식을 버릴 수 있습니다. 고객의 당혹스러운 마음을 사로잡는 동시에 조직의 지원 볼륨 및 비용을 높일 수 있습니다. 전환율을 높일 수 있는 적합한 고객 경험을 찾아 제공하는 것은 물론 매우 중요합니다. AEM 양식에서 이 문제의 열쇠를 쥐고 있습니다.

AEM 양식은 Adobe Marketing Cloud 솔루션인 Adobe Target과 통합되어 개인화되고 매력적인 고객 경험을 다양한 디지털 채널에 전달할 수 있습니다. Adobe Target을 A/B에서 적응형 양식을 테스트하려면 AEM Forms [와 Adobe Target을 통합하십시오](/help/forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms).

## 다음 단계 {#next-steps}

AEM Forms 데이터 캡처 기능을 사용하도록 환경을 구성했습니다. 이제 기능 사용을 위한 다음 단계는 다음과 같습니다.

* [간단한 적응형 양식 만들기](/help/forms/using/create-your-first-adaptive-form.md)
* [간단한 PDF 양식 작성](http://www.adobe.com/go/learn_aemforms_designer_quick_start_65)
* [HTML5 양식 소개](/help/forms/using/introduction.md)

