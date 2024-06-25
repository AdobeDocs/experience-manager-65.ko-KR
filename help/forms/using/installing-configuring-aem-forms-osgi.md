---
title: 데이터 캡처 기능 설치 및 구성
description: 적응형 양식, PDF forms 및 HTML5 Forms을 설치하고 구성합니다. 적응형 양식에 대한 Adobe Analytics 및 Adobe Target을 구성하여 양식 사용을 분석하고 프로필을 기반으로 사용자를 타겟팅합니다.
topic-tags: installing
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
role: Admin, User, Developer
exl-id: 19b5765e-50bc-4fed-8af5-f6bb464516c8
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on OSGi
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1882'
ht-degree: 4%

---

# 데이터 캡처 기능 설치 및 구성{#install-and-configure-data-capture-capabilities}

## 소개 {#introduction}

AEM Forms은 최종 사용자로부터 데이터를 가져오기 위한 적응형 양식, HTML 5 Forms 및 PDF forms 양식 세트를 제공합니다. 또한 웹 페이지에 사용 가능한 모든 양식을 나열하고 양식 사용을 분석하며 프로필을 기반으로 사용자를 타깃팅하는 도구를 제공합니다. 이러한 기능은 AEM Forms 추가 기능 패키지에 포함되어 있습니다. 추가 기능 패키지는 AEM의 작성자 또는 Publish 인스턴스에 배포됩니다.

**적응형 양식:** 이러한 형태는 장치의 화면 크기에 따라 모양을 변경하고, 매력적인 형태이며, 본질적으로 대화형입니다. 적응형 Forms은 Adobe Analytics, Adobe Sign 및 Adobe Target과도 통합할 수 있습니다. 이를 통해 인구 통계학 및 기타 기능을 기반으로 개인화된 양식 및 프로세스 지향 경험을 사용자에게 제공할 수 있습니다. 적응형 양식을 Adobe Sign과 통합할 수도 있습니다.

**PDF forms** PDF 문서 내에서 픽셀 단위 인쇄 및 디지털 정보 캡처에 적합합니다. 디지털 아바타에서는 Adobe Acrobat 또는 Acrobat Reader을 사용하여 이러한 양식을 채울 수 있습니다. 웹 사이트에서 이러한 양식을 호스팅하거나 양식 포털을 사용하여 AEM 사이트에 이러한 양식을 나열할 수 있습니다. 이러한 양식을 다른 사용자에게 첨부 파일로 전자 메일로 보낼 수도 있습니다. 이러한 양식은 데스크탑 환경에 가장 적합합니다.

**HTML5 FORMS** 는 브라우저에 친숙한 PDF forms 버전입니다. HTML5 Forms은 PDF 플러그인을 지원하지 않는 환경에 적합합니다. HTML5 Forms을 사용하면 XFA 기반 PDF이 지원되지 않는 모바일 장치 및 데스크탑 브라우저에서 XFA 기반 양식을 렌더링할 수 있습니다. 이러한 양식은 태블릿과 데스크탑 환경에 가장 적합합니다.

AEM Forms은 강력한 엔터프라이즈급 플랫폼이며 데이터 캡처(적응형 양식, PDF forms 및 HTML5 Forms)는 AEM Forms의 기능 중 하나에 불과합니다. 전체 기능 목록은 다음을 참조하십시오. [AEM Forms 소개](/help/forms/using/introduction-aem-forms.md).

## 배포 토폴로지 {#deployment-topology}

AEM Forms 추가 기능 패키지는 AEM에 배포된 애플리케이션입니다. AEM Forms 데이터 캡처 기능을 실행하려면 AEM Author 및 AEM Publish 인스턴스가 최소 한 개 이상 있어야 합니다. AEM Forms AEM Forms 데이터 캡처 기능을 실행하려면 다음 토폴로지를 사용하는 것이 좋습니다. 토폴로지에 대한 자세한 내용은 [AEM Forms의 아키텍처 및 배포 토폴로지](/help/forms/using/aem-forms-architecture-deployment.md).

![recommended-topology](assets/recommended-topology.png)

## 시스템 요구 사항 {#system-requirements}

AEM Forms의 데이터 캡처 기능을 설치하고 구성하기 전에 다음을 확인하십시오.

* 하드웨어 및 소프트웨어 인프라가 구축되어 있습니다. 지원되는 하드웨어 및 소프트웨어에 대한 자세한 목록은 [기술 요구 사항](/help/sites-deploying/technical-requirements.md).

* AEM 인스턴스의 설치 경로에 공백이 포함되어 있지 않습니다.
* AEM 인스턴스가 실행 중입니다. Windows 사용자의 경우 관리자 모드로 AEM 인스턴스를 설치합니다. AEM 용어에서 &quot;인스턴스&quot;는 작성자 또는 게시 모드의 서버에서 실행되는 AEM의 사본입니다. 최소 두 개가 필요합니다. [AEM 인스턴스(작성자 1명 및 Publish 1명)](/help/sites-deploying/deploy.md) AEM Forms 데이터 캡처 기능을 실행하려면 다음 작업을 수행하십시오.

   * **작성자**: 콘텐츠를 만들고, 업로드하고, 편집하고, 웹 사이트를 관리하는 데 사용되는 AEM 인스턴스입니다. 콘텐츠를 실행할 준비가 되면 게시 인스턴스에 복제됩니다.
   * **게시**: 인터넷 또는 내부 네트워크를 통해 게시된 콘텐츠를 일반에게 제공하는 AEM 인스턴스.

* 메모리 요구 사항이 충족됩니다. AEM Forms 추가 기능 패키지를 사용하려면 다음 작업을 수행해야 합니다.

   * Microsoft Windows 기반 설치용 15GB의 임시 공간.
   * UNIX 기반 설치의 경우 6GB의 임시 공간이 필요합니다.

* 작성자 및 게시 인스턴스에 대한 복제 및 역방향 복제가 설정되었습니다. 자세한 내용은 [복제](/help/sites-deploying/replication.md).
* UNIX 기반 시스템의 경우:

   * 설치 미디어에서 다음 32비트 패키지를 설치합니다.

<table>
 <tbody>
  <tr>
   <td>지수</td>
   <td>fontconfig</td>
   <td>자유 형식</td>
   <td>아교</td>
  </tr>
  <tr>
   <td>라이브컬</td>
   <td>libice</td>
   <td>리비쿠</td>
   <td>libSM</td>
  </tr>
  <tr>
   <td>리부uid</td>
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
   <td>Openssl</td>
   <td>즐리브</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* OpenSSL이 서버에 이미 설치되어 있는 경우 최신 버전으로 업그레이드합니다.
>* libcurl, libcrypto.so 및 libssl.so의 최신 버전을 각각 지정하는 심볼릭 링크를 만듭니다.
>

* 설치 미디어에서 다음 64비트 패키지를 설치합니다.

   * 리비쿠

* 설치 [Microsoft Visual Studio 2019 32비트 재배포 가능](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170).


## AEM Forms 추가 기능 패키지 설치 {#install-aem-forms-add-on-package}

AEM Forms 추가 기능 패키지는 AEM에 배포된 애플리케이션입니다. 이 패키지에는 AEM Forms 데이터 캡처 및 기타 기능이 포함되어 있습니다. 추가 기능 패키지를 설치하려면 다음 단계를 수행하십시오.

1. [소프트웨어 배포](https://experience.adobe.com/downloads)를 엽니다. 소프트웨어 배포에 로그인하려면 Adobe ID가 필요합니다.
1. 선택 **[!UICONTROL Adobe Experience Manager]** 헤더 메뉴에서 사용할 수 있습니다.
1. 다음에서 **[!UICONTROL 필터]** 섹션:
   1. 선택 **[!UICONTROL Forms]** 다음에서 **[!UICONTROL 솔루션]** 드롭다운 목록입니다.
   2. 패키지의 버전 및 유형을 선택합니다. 다음을 사용할 수도 있습니다 **[!UICONTROL 다운로드 검색]** 옵션을 사용하여 결과를 필터링할 수 있습니다.
1. 운영 체제에 적용할 수 있는 패키지 이름을 선택하고 **[!UICONTROL EULA 약관 동의]**, 및 선택 **[!UICONTROL 다운로드]**.
1. 열기 [패키지 관리자](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)  및 클릭 **[!UICONTROL 패키지 업로드]** 패키지를 업로드합니다.
1. 패키지를 선택하고 **[!UICONTROL 설치]**&#x200B;를 클릭합니다.

   에 나열된 직접 링크를 통해 패키지를 다운로드할 수도 있습니다. [AEM Forms 릴리스](https://helpx.adobe.com/kr/aem-forms/kb/aem-forms-releases.html) 기사.
1. 패키지를 설치한 후 AEM 인스턴스를 다시 시작하라는 메시지가 표시됩니다. **서버를 즉시 다시 시작하지 마십시오.** AEM Forms 서버를 중지하기 전에 ServiceEvent REGISTERED 및 ServiceEvent UNREGISTERED 메시지가 `[AEM-Installation-Directory]/crx-quickstart/logs/error.log` 파일이 있고 로그가 안정적입니다.

   >[!NOTE]
   >
   > SDK를 다시 시작하려면 &#39;Ctrl + C&#39; 명령을 사용하는 것이 좋습니다. Java 프로세스 중지와 같은 대체 방법을 사용하여 AEM SDK를 다시 시작하면 AEM 개발 환경이 일치하지 않을 수 있습니다.

1. 모든 Author 및 Publish 인스턴스에서 1~7단계를 반복합니다.

### (Windows만 해당) Visual Studio 재배포용 파일 자동 설치 {#automatic-installation-visual-studio-redistributables}

관리자 모드로 AEM 인스턴스를 설치하는 경우 AEM Forms 추가 기능 패키지를 설치하는 동안 32비트 Visual Studio 재배포 가능 패키지가 자동으로 설치됩니다.

Visual Studio 재배포용 파일을 자동으로 설치했는지 평가하려면 `error.log` 에서 사용할 수 있는 파일 `/crx-repository/logs/` 디렉토리. 로그에는 다음 메시지가 포함됩니다.

`Redist <service name> already installed on system, will not attempt re-installation`

재배포 가능 패키지를 설치하지 못하면 로그에 다음 메시지가 포함됩니다.

`Current user does not have elevated privileges, aborting installation of redist <service name>`

이 문제를 해결하려면 AEM 서버를 다시 시작하고 관리자 모드로 AEM을 설치한 다음 AEM Forms 추가 기능 패키지를 설치하십시오.

권한 검사에 실패하면 로그에는 다음 메시지가 포함됩니다.

`Privilege escalation check failed with error: <error message>`

## 설치 후 구성 {#post-installation-configurations}

AEM Forms에는 몇 가지 필수 구성과 선택적 구성이 있습니다. 필수 구성에는 BouncyCastle 라이브러리 및 직렬화 에이전트 구성이 포함됩니다. 선택적 구성에는 Dispatcher, Forms 포털, Adobe Sign, Adobe Analytics 및 Adobe Target 구성이 포함됩니다.

### 필수 사후 설치 구성 {#mandatory-post-installation-configurations}

#### RSA 및 BouncyCastle 라이브러리 구성  {#configure-rsa-and-bouncycastle-libraries}

모든 작성자 및 게시 인스턴스에서 다음 단계를 수행하여 라이브러리를 부팅합니다.

1. 기본 AEM 인스턴스를 중지합니다.
1. 편집할 `[AEM installation directory]\crx-quickstart\conf\sling.properties` 페이지를 엽니다.

   을 사용한 경우 `[AEM installation directory]\crx-quickstart\bin\start.bat` AEM을 시작한 다음, 의 sling.properties를 편집합니다. `[AEM_root]\crx-quickstart\`.

1. sling.properties 파일에 다음 속성을 추가합니다.

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. 파일을 저장하고 닫은 다음 AEM 인스턴스를 시작합니다.
1. 모든 Author 및 Publish 인스턴스에서 1~4단계를 반복합니다.

#### 직렬화 에이전트 구성 {#configure-the-serialization-agent}

모든 작성자 및 Publish 인스턴스에서 다음 단계를 수행하여 패키지를 허용 목록에 추가하다에 추가합니다.

1. 브라우저 창에서 AEM 구성 관리자를 엽니다. 기본 URL은 `https://'[server]:[port]'/system/console/configMgr`.
1. 검색 대상 **com.adobe.cq.deserfw.impl.DeserializationFirewallImpl.name** 구성을 엽니다.
1. 추가 **sun.util.calendar** 패키지 대상 **허용 목록** 필드. **저장**&#x200B;을 클릭합니다.
1. 모든 Author 및 Publish 인스턴스에서 1~3단계를 반복합니다.

### 설치 후 구성 옵션 {#optional-post-installation-configurations}

#### Dispatcher 구성 {#configure-dispatcher}

Dispatcher는 엔터프라이즈급 웹 서버와 함께 사용할 수 있는 Adobe Experience Manager의 캐싱 및/또는 로드 밸런싱 도구입니다. 를 사용하는 경우 [디스패처](https://helpx.adobe.com/kr/experience-manager/dispatcher/using/dispatcher-configuration.html)를 실행한 다음 AEM Forms에 대해 다음 구성을 수행합니다.

1. AEM Forms에 대한 액세스 구성:

   편집할 dispatcher.any 파일을 엽니다. 필터 섹션으로 이동하고 필터 섹션에 다음 필터를 추가합니다.

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   파일을 저장하고 닫습니다. 필터에 대한 자세한 내용은 [Dispatcher 설명서](https://helpx.adobe.com/kr/experience-manager/dispatcher/using/dispatcher-configuration.html).

1. 레퍼러 필터 서비스를 구성합니다.

   Apache Felix 구성 관리자에 관리자로 로그인합니다. 구성 관리자의 기본 URL은 `https://[server]:[port_number]/system/console/configMgr`. 다음에서 **구성** 메뉴에서 **Apache Sling Referrer 필터** 옵션을 선택합니다. 호스트 허용 필드에 레퍼러로 허용할 Dispatcher의 호스트 이름을 입력하고 을 클릭합니다 **저장**. 항목의 형식은 다음과 같습니다. `https://[server]:[port]`.

#### 캐시 구성 {#configure-cache}

캐싱은 데이터 액세스 시간을 단축하고, 지연을 줄이고, 입출력(I/O) 속도를 향상시키는 메커니즘입니다. 적응형 양식 캐시는 미리 채워진 데이터를 저장하지 않고 적응형 양식의 HTML 컨텐츠 및 JSON 구조만 저장합니다. 적응형 양식을 렌더링하는 데 필요한 시간을 줄이는 데 도움이 됩니다.

* 적응형 양식 캐시를 사용할 때 다음을 사용합니다. [AEM 디스패처](https://helpx.adobe.com/kr/experience-manager/dispatcher/using/dispatcher-configuration.html) 를 클릭하여 적응형 양식의 클라이언트 라이브러리(CSS 및 JavaScript)를 캐시합니다.
* 사용자 지정 구성 요소를 개발하는 동안 개발에 사용되는 서버에서 적응형 양식 캐시를 비활성화 상태로 유지합니다.

다음 단계를 수행하여 적응형 양식 캐시를 구성합니다.

1. https://&#39;에서 AEM 웹 콘솔 구성 관리자로 이동합니다.[server]:[포트]&#39;/system/console/configMgr.
1. 클릭 **적응형 양식 및 대화형 통신 웹 채널 구성** 구성 값을 편집하려면 다음을 수행하십시오. 구성 값 편집 대화 상자에서 AEM Forms 서버 인스턴스가 캐시할 수 있는 최대 양식 또는 문서 수를 지정합니다. **적응형 Forms 수** 필드. 기본값은 100입니다. **저장**&#x200B;을 클릭합니다.

   >[!NOTE]
   >
   >캐시를 비활성화하려면 적응형 Forms 수 필드의 값을 다음으로 설정하십시오. **0**. 캐시 구성을 비활성화하거나 변경하면 캐시가 재설정되고 모든 양식 및 문서가 캐시에서 제거됩니다.

#### 양식 데이터 모델에 대한 SSL 통신 구성 {#configure-ssl-communcation-for-form-data-model}

양식 데이터 모델에 대해 SSL 통신을 활성화할 수 있습니다. 양식 데이터 모델에 대해 SSL 통신을 활성화하려면 AEM Forms 인스턴스를 시작하기 전에 모든 인스턴스의 Java Trust Store에 인증서를 추가합니다. 아래 명령을 실행하여 인증서를 추가할 수 있습니다. &quot;

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

#### Adobe Sign 구성 {#configure-adobe-sign}

Adobe Sign은 적응형 양식용 전자 서명 워크플로를 가능하게 합니다. 전자 서명은 법무, 판매, 임금, 인적 자원 관리 등의 다양한 분야에서 문서를 처리하는 워크플로를 개선합니다.

일반적인 Adobe Sign 및 적응형 양식 시나리오에서 사용자는 적응형 양식을 다음으로 채웁니다. **서비스 신청**. 신용 카드 신청 양식과 시민 혜택 양식을 예로 들 수 있습니다. 사용자가 신청 양식에 정보를 입력하고 이를 제출한 뒤 서명하면, 이후의 액션이 가능하도록 양식이 서비스 제공자에게 전달됩니다. 서비스 공급자는 애플리케이션을 검토하고 Adobe Sign을 사용하여 애플리케이션을 승인된 것으로 표시합니다. Adobe Sign을 AEM Forms과 통합하여 유사한 전자 서명 워크플로를 활성화할 수 있습니다.

AEM Forms에서 Adobe Sign을 사용하려면, [Adobe Sign과 AEM Forms 통합](/help/forms/using/adobe-sign-integration-adaptive-forms.md).

#### Adobe Analytics 구성 {#configure-adobe-analytics}

AEM Forms은 Adobe Analytics과 통합되어 게시된 양식 및 문서에 대한 성능 지표를 캡처하고 추적할 수 있습니다. 이러한 지표를 분석하는 목표는 양식이나 문서를 보다 유용하게 만드는 데 필요한 변경 사항에 대한 데이터를 기반으로 정보에 입각한 결정을 내리는 것입니다.

AEM Forms과 함께 Adobe Analytics을 사용하려면 다음을 참조하십시오. [분석 및 보고서 구성](/help/forms/using/configure-analytics-forms-documents.md).

#### Adobe Target 통합 {#integrate-adobe-target}

고객이 제공하는 경험이 매력적이지 않을 경우 양식을 포기할 가능성이 높습니다. 고객에게는 번거로운 일이지만, 조직의 지원 규모와 비용도 증가할 수 있습니다. 전환율을 높이는 올바른 고객 경험을 파악하고 제공하는 것은 중요하고 어려운 일입니다. AEM forms가 이 문제의 키를 쥐고 있습니다.

AEM forms는 Adobe Marketing Cloud 솔루션인 Adobe Target과 통합되어 여러 디지털 채널에서 개인화되고 매력적인 고객 경험을 제공합니다. Adobe Target을 사용하여 A/B 테스트 적응형 양식을 만들려면 [Adobe Target과 AEM Forms 통합](/help/forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms).

## 다음 단계 {#next-steps}

AEM Forms 데이터 캡처 기능을 사용할 환경을 구성했습니다. 이제 기능을 사용하기 위한 다음 단계는 다음과 같습니다.

* [첫 번째 적응형 양식 만들기](/help/forms/using/create-your-first-adaptive-form.md)
* [첫 번째 PDF 양식 만들기](https://www.adobe.com/go/learn_aemforms_designer_quick_start_65)
* [HTML5 Forms 소개](/help/forms/using/introduction.md)
