---
title: OSGi에서 양식 중심의 워크플로우 설치 및 구성
seo-title: OSGi에서 양식 중심의 워크플로우 설치 및 구성
description: AEM Forms Interactive Communications를 설치 및 구성하여 비즈니스 연락처, 문서, 명세서, 혜택 공지, 마케팅 이메일, 청구서 및 환영 키트를 만듭니다.
seo-description: AEM Forms Interactive Communications를 설치 및 구성하여 비즈니스 연락처, 문서, 명세서, 혜택 공지, 마케팅 이메일, 청구서 및 환영 키트를 만듭니다.
uuid: 1ceae822-215a-4b83-a562-4609a09c3a54
topic-tags: installing
discoiquuid: de292a19-07db-4ed3-b13a-7a2f1cd9e0dd
docset: aem65
translation-type: tm+mt
source-git-commit: 3226edb575de3d9f8bff53f5ca81e2957f37c544

---


# OSGi에서 양식 중심의 워크플로우 설치 및 구성{#installing-and-configuring-forms-centric-workflow-on-osgi}

## 소개 {#introduction}

기업은 여러 양식, 백엔드 시스템 및 기타 데이터 소스에서 데이터를 수집하고 처리합니다. 데이터 처리에는 검토 및 승인 절차, 반복 작업 및 데이터 보관이 포함됩니다. 예를 들어 양식을 검토하고 PDF 문서로 변환할 수 있습니다. 수동으로 작업을 수행하면 반복적인 작업에 많은 시간과 리소스가 소요될 수 있습니다.

OSGi [에서 양식 중심의 워크플로우를](../../forms/using/aem-forms-workflow.md) 사용하여 적응형 양식 기반 워크플로우를 신속하게 구축할 수 있습니다. 이러한 워크플로우를 통해 검토 및 승인 워크플로우, 비즈니스 프로세스 워크플로우 및 기타 반복적인 작업을 자동화할 수 있습니다. 또한 이러한 워크플로우를 통해 문서 처리(PDF 문서 작성, 조합, 배포 및 보관, 디지털 서명 추가, 문서 액세스 제한, 바코드 양식 디코딩 등)와 양식 및 문서에서 Adobe Sign 서명 워크플로우를 사용할 수 있습니다.

설정되면 이러한 워크플로우를 수동으로 트리거하여 정의된 프로세스를 완료하거나 사용자가 양식이나 대화형 통신을 제출할 때 프로그래밍 방식으로 실행할 수 있습니다. 이 기능은 AEM Forms 추가 기능 패키지에 포함되어 있습니다.

AEM Forms는 강력한 엔터프라이즈급 플랫폼입니다. OSGi의 양식 중심 워크플로우는 AEM Forms 기능 중 하나에 불과합니다. 전체 기능 목록은 AEM Forms [소개를 참조하십시오](../../forms/using/introduction-aem-forms.md).

>[!NOTE]
>
>OSGi의 양식 중심 워크플로우를 사용하면 JEE 스택에 완벽한 프로세스 관리 기능을 설치하지 않고도 OSGi 스택에서 다양한 작업을 위한 워크플로우를 신속하게 구축 및 배포할 수 있습니다. OSGi 및 JEE의 프로세스 관리에 대한 양식 중심의 AEM 워크플로우를 [비교한](../../forms/using/capabilities-osgi-jee-workflows.md) 내용을 통해 기능의 차이점과 유사점을 살펴볼 수 있습니다.
>
>비교 후 JEE 스택에 프로세스 관리 기능을 설치하도록 선택한 경우 JEE [스택 및 프로세스 관리](/help/forms/home.md) 기능의 설치 및 구성에 대한 자세한 내용은 JEE에서 AEM Forms 설치 또는 업그레이드를 참조하십시오.

## 배포 토폴로지 {#deployment-topology}

AEM Forms Add-on 패키지는 AEM에 배포된 애플리케이션입니다. OSGi 기능에서 양식 중심의 워크플로우를 실행하려면 최소 하나의 AEM 작성자 또는 처리 인스턴스(프로덕션 작성자)만 있으면 됩니다. 처리 인스턴스는 [견고한 AEM 작성자](/help/forms/using/hardening-securing-aem-forms-environment.md) 인스턴스입니다. 프로덕션 작성자에서 워크플로우 또는 적응형 양식 작성과 같은 실제 저작을 수행하지 마십시오.

다음 토폴로지는 AEM Forms 대화형 통신, 통신 관리, AEM Forms 데이터 캡처 및 OSGi 기능에서 양식 중심의 워크플로우를 실행하기 위한 표시 토폴로지입니다. 토폴로지에 대한 자세한 내용은 AEM Forms [용 아키텍처 및 배포 토폴로지를 참조하십시오](/help/forms/using/aem-forms-architecture-deployment.md).

![권장 토폴로지](assets/recommended-topology.png)

OSGi의 AEM 양식 중심 워크플로우는 AEM Forms 작성자 인스턴스에서 AEM 받은 편지함 및 AEM 워크플로우 모델 생성 UI를 실행합니다.

## 시스템 요구 사항 {#system-requirements}

>[!NOTE]
>
>OSGi에 이미 AEM [Forms를 설치한 경우](../../forms/using/installing-configuring-forms-centric-workflow-on-osgi.md#next-steps) 설치 및 구성 데이터 캡처 기능 [문서에 설명된 대로 문서의 다음 단계](../../forms/using/installing-configuring-aem-forms-osgi.md) 섹션으로 건너뜁니다.

OSGi에서 양식 중심의 워크플로우를 설치 및 구성하기 전에 다음을 확인하십시오.

* 하드웨어 및 소프트웨어 인프라가 적소에 있습니다. 지원되는 하드웨어 및 소프트웨어에 대한 자세한 목록은 [기술 요구 사항을](/help/sites-deploying/technical-requirements.md)참조하십시오.

* AEM 인스턴스의 설치 경로에 공백이 없습니다.
* AEM 인스턴스가 실행 중입니다. AEM 용어에서 &quot;인스턴스&quot;는 작성자 또는 게시 모드에서 서버에서 실행되는 AEM의 복사본입니다. OSGi에서 양식 중심의 워크플로우를 실행하려면 하나 이상의 AEM 인스턴스(작성자 또는 처리)가 필요합니다.

   * **작성자**:컨텐츠를 작성, 업로드 및 편집하고 웹 사이트를 관리하는 데 사용되는 AEM 인스턴스입니다. 컨텐츠를 라이브할 준비가 되면 게시 인스턴스에 복제됩니다.
   * **** 처리 중:처리 인스턴스는 [견고한 AEM 작성자](/help/forms/using/hardening-securing-aem-forms-environment.md) 인스턴스입니다. 작성 인스턴스를 설정하고 설치를 수행한 후에 이를 취소할 수 있습니다.

   * **게시**:인터넷 또는 내부 네트워크를 통해 대중에게 게시된 컨텐츠를 제공하는 AEM 인스턴스입니다.

* 메모리 요구 사항이 충족되었습니다. AEM Forms Add-on 패키지에 필요한 사항:

   * Microsoft Windows 기반 설치를 위한 15GB의 임시 공간.
   * UNIX 기반 설치를 위한 6GB의 임시 공간.

* UNIX 기반 시스템에 대한 추가 요구 사항:UNIX 기반 운영 체제를 사용하는 경우 해당 운영 체제의 설치 미디어에서 다음 패키지를 설치합니다.

<table>
 <tbody>
  <tr>
   <td>expat</td>
   <td>libxcb</td>
   <td>freetype</td>
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

## Install AEM Forms add-on package {#install-aem-forms-add-on-package}

AEM Forms Add-on 패키지는 AEM에 배포된 애플리케이션입니다. 이 패키지에는 OSGi 및 기타 기능에 대한 양식 중심의 워크플로우가 포함되어 있습니다. Add-on 패키지를 설치하려면 다음 단계를 수행하십시오.

1. AEM 서버에 [](https://localhost:4502) 관리자로 로그인하고 [패키지 공유를](https://localhost:4502/crx/packageshare)엽니다. 패키지 공유에 로그인하려면 Adobe ID가 필요합니다.
1. AEM [패키지 공유에서](https://localhost:4502/crx/packageshare/login.html)**AEM 6.5 Forms Add-on 패키지**&#x200B;또는&#x200B;**최신 서비스**&#x200B;팩을 **검색하고 운영 체제에 해당하는 패키지를 클릭한 후 다운로드**&#x200B;완료를 클릭합니다. 라이센스 계약을 읽고 동의한 다음 확인을 **클릭합니다**. 다운로드가 시작됩니다. 다운로드하면 패키지 **옆에** 다운로드된 단어가 나타납니다.

   버전 번호를 사용하여 추가 기능 패키지를 검색할 수도 있습니다. 최신 패키지의 버전 번호는 AEM Forms 릴리스 [문서를](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) 참조하십시오.

1. 다운로드가 완료되면 [다운로드됨]을 **클릭합니다**. 패키지 관리자로 리디렉션됩니다. 패키지 관리자에서 다운로드한 패키지를 검색하고 설치를 **클릭합니다**.

   AEM Forms 릴리스 [문서에 나열된 직접 링크를 통해 패키지를 수동으로 다운로드하는 경우 패키지](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) 관리자에 **로그인하고 패키지 업로드를**&#x200B;클릭한 다음다운로드한 패키지를 선택하고 업로드를 클릭합니다. 패키지가 업로드되면 패키지 이름을 클릭하고 설치를 **클릭합니다.**

1. 패키지가 설치되면 AEM 인스턴스를 다시 시작하라는 메시지가 표시됩니다. **서버를 즉시 다시 시작하지 마십시오.** AEM Forms 서버를 중지하기 전에 AEM-Installation-Directory /crx-quickstart/logs/error.log 파일에 ServiceEvent REGISTERED 및 ServiceEvent UNREGISTERED [메시지가]나타나지 않고 로그가 안정적일 때까지 기다립니다.
1. 모든 작성자 및 게시 인스턴스에 대해 1-4단계를 반복합니다.

## 설치 후 구성 {#post-installation-configurations}

AEM Forms에는 몇 가지 필수 구성 및 선택 사항이 있습니다. 필수 구성에는 BouncyCastle 라이브러리 및 직렬화 에이전트 구성이 포함됩니다. 선택적인 구성에는 디스패처 및 Adobe Target 구성이 포함됩니다.

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

1. 브라우저 창에서 AEM 구성 관리자를 엽니다. 기본 URL은 https://[server]:[port]/system/console/configMgr입니다.
1. Deserialization 방화벽 **구성을 검색하고 엽니다**.
1. sun.util.calendar **패키지를** 화이트리스트 **** 필드에 추가합니다. [저장]을 클릭합니다.
1. 모든 작성자 및 게시 인스턴스에 대해 1-3단계를 반복합니다.

### 설치 후 구성(옵션) {#optional-post-installation-configurations}

#### 발송자 구성 {#configure-dispatcher}

디스패처가 AEM에 대한 캐싱 및 로드 밸런싱 도구를 사용하고 있습니다. AEM Dispatcher는 AEM 서버를 공격으로부터 보호하는 데에도 도움이 됩니다. 엔터프라이즈급 웹 서버와 함께 Dispatcher를 사용하여 AEM 인스턴스의 보안을 강화할 수 있습니다. Dispatcher를 사용하는 [경우](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)AEM Forms에 대해 다음 구성을 수행하십시오.

1. AEM Forms에 대한 액세스 권한 구성:

   편집하기 위해 dispatcher.any 파일을 엽니다. 필터 섹션으로 이동하여 필터 섹션에 다음 필터를 추가합니다.

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   파일을 저장하고 닫습니다. 필터에 대한 자세한 내용은 Dispatcher [설명서를](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)참조하십시오.

1. 레퍼러 필터 서비스를 구성합니다.

   Apache Felix 구성 관리자에 관리자로 로그인합니다. 구성 관리자의 기본 URL은 https://[server]:[port_number]/system/console/configMgr입니다. [ **구성** ] 메뉴에서 [Apache Sling Referrer **필터] 옵션을** 선택합니다. 호스트 허용 필드에 디스패처의 호스트 이름을 입력하여 레퍼러로 허용하고 저장을 **클릭합니다**. 항목의 형식은 `https://[server]:[port]`입니다.

#### 캐시 구성 {#configure-cache}

캐싱은 데이터 액세스 시간을 단축하고 지연 시간을 줄이며 입출력 속도를 향상시키는 메커니즘입니다. 적응형 양식 캐시는 사전 채워진 데이터를 저장하지 않고 적응형 양식의 HTML 컨텐츠 및 JSON 구조만 저장합니다. 적응형 양식을 렌더링하는 데 필요한 시간을 줄이는 데 도움이 됩니다.

* 적응형 양식 캐시 사용 시 AEM [Dispatcher를](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html) 사용하여 적응형 양식의 클라이언트 라이브러리(CSS 및 JavaScript)를 캐시합니다.
* 사용자 정의 구성 요소를 개발하는 동안 개발에 사용되는 서버에서 응용 양식 캐시를 사용하지 않도록 설정하십시오.

적응형 양식 캐시를 구성하려면 다음 단계를 수행하십시오.

1. 의 AEM 웹 콘솔 구성 관리자로 이동합니다 `https://[server]:[port]/system/console/configMgr`.
1. 적응형 **양식 구성** 서비스를 클릭하여 구성 값을 편집합니다. 구성 값 편집 대화 상자에서 적응형 양식 수 필드에 AEM Forms 서버의 인스턴스가 캐싱할 수 있는 최대 양식 또는 문서 **수를 지정합니다** . 기본값은 100입니다. **저장**&#x200B;을 클릭합니다.

   >[!NOTE]
   >
   >캐시를 비활성화하려면 [적응형 양식 수] 필드의 값을 **0으로 설정합니다**. 캐시는 재설정되고 캐시 구성을 비활성화하거나 변경하면 모든 양식과 문서가 캐시에서 제거됩니다.

#### Adobe Sign 구성 {#configure-adobe-sign}

Adobe Sign을 사용하면 적응형 양식을 위한 전자 서명 워크플로우를 수행할 수 있습니다. 전자 서명은 법률, 영업, 급여, 인사 관리 등 다양한 분야의 문서를 처리하는 워크플로우를 향상시켜 줍니다.

OSGi 시나리오의 일반적인 Adobe Sign 및 양식 중심 워크플로우에서 사용자는 적응형 양식을 작성하여 서비스에 ****&#x200B;적용합니다. 예를 들어 신용 카드 신청서와 시민 혜택 양식이 있습니다. 사용자가 애플리케이션 양식을 채우고 제출 및 서명하면 승인/거부 워크플로우가 시작됩니다. 서비스 공급업체는 AEM 받은 편지함에서 애플리케이션을 검토하고 Adobe Sign을 사용하여 응용 프로그램에 전자 서명합니다. 유사한 전자 서명 워크플로우를 사용하려면 AEM Forms와 Adobe Sign을 통합할 수 있습니다.

AEM Forms에서 Adobe Sign을 사용하려면 [AEM Forms와 Adobe Sign을 통합하십시오](../../forms/using/adobe-sign-integration-adaptive-forms.md).

## 다음 단계 {#next-steps}

OSGi 기능에서 양식 중심의 워크플로우를 사용하도록 환경을 구성했습니다. 이제 기능 사용을 위한 단계는 다음과 같습니다.

* [OSGi에서 양식 중심의 워크플로우 사용](../../forms/using/aem-forms-workflow.md)
* [워크플로우 단계 참조](/help/sites-developing/workflows-step-ref.md)
* [서신 및 인터랙티브한 커뮤니케이션의 게시 처리](../../forms/using/submit-letter-topostprocess.md)

