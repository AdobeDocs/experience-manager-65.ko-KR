---
title: OSGi에서 Forms 중심 워크플로우 설치 및 구성
description: AEM Forms Interactive Communications를 설치 및 구성하여 비즈니스 서신, 문서, 명세서, 혜택 공지, 마케팅 이메일, 청구서 및 시작 키트를 만듭니다.
topic-tags: installing
docset: aem65
role: Admin, User, Developer
exl-id: 4b24a38a-c1f0-4c81-bb3a-39ce2c4892b1
solution: Experience Manager, Experience Manager Forms
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1624'
ht-degree: 4%

---

# OSGi에서 Forms 중심 워크플로우 설치 및 구성{#installing-and-configuring-forms-centric-workflow-on-osgi}

## 소개 {#introduction}

기업은 여러 양식, 백엔드 시스템 및 기타 데이터 소스에서 데이터를 수집하고 처리합니다. 데이터 처리에는 검토 및 승인 절차, 반복적인 작업 및 데이터 보관 포함됩니다. 예를 들어, 양식을 검토하고 PDF 문서로 변환할 수 있습니다. 수동으로 수행하면 반복적인 작업에 많은 시간과 많은 리소스가 소요될 수 있습니다.

OSGi](../../forms/using/aem-forms-workflow.md)에서 Forms 중심의 작업 과정 워크플로우를 사용하여 [적응형 양식 기반 워크플로우를 신속하게 빌드 할 수 있습니다. 이러한 워크플로는 검토 및 승인 워크플로, 비즈니스 프로세스 워크플로 및 기타 반복적인 작업을 자동화하는 데 도움이 될 수 있습니다. 이러한 작업 과정은 또한 문서를 처리하고(PDF 문서 작성, 조합, 배포 및 보관, 문서에 대한 액세스를 제한하는 디지털 서명 추가, 바코드 양식 디코딩 등) 양식 및 문서에서 Adobe Sign 서명 작업 과정을 사용하는 데 도움이 됩니다.

설정이 완료되면 이러한 워크플로우를 수동으로 트리거하여 정의된 프로세스를 완료하거나 사용자가 양식 또는 대화형 통신을 제출할 때 프로그래밍 방식으로 실행할 수 있습니다. 이 기능은 AEM Forms 추가 기능 패키지에 포함되어 있습니다.

AEM Forms은 강력한 엔터프라이즈급 플랫폼입니다. OSGi에서의 Forms 중심 워크플로우는 AEM Forms의 기능 중 하나일 뿐입니다. 전체 기능 목록은 다음을 참조하십시오. [AEM Forms 소개](introduction-aem-forms.md).

>[!NOTE]
>
>OSGi의 Forms 중심 워크플로우를 사용하면 JEE 스택에 완전한 프로세스 관리 기능을 설치하지 않고도 OSGi 스택에서 다양한 작업을 위한 워크플로우를 빠르게 빌드하고 배포할 수 있습니다. 참조: [비교](capabilities-osgi-jee-workflows.md) OSGi의 Forms 중심 AEM 워크플로우 및 JEE의 프로세스 관리를 통해 기능의 차이점과 유사점을 알아보십시오.
>
>비교 후 JEE 스택에 프로세스 관리 기능을 설치하도록 선택하는 경우 다음을 참조하십시오. [JEE에 AEM Forms 설치 또는 업그레이드](/help/forms/using/introduction-aem-forms.md) jee 스택 설치 및 구성 및 프로세스 관리 기능에 대한 자세한 내용은 을 참조하십시오.

## 배포 토폴로지 {#deployment-topology}

AEM Forms 추가 기능 패키지는 AEM에 배포된 애플리케이션입니다. OSGi 기능에서 Forms 중심 워크플로우를 실행하려면 최소 하나의 AEM 작성자 또는 처리 인스턴스(프로덕션 작성자)만 필요합니다. 처리 인스턴스는 [경화 AEM 작성자](/help/forms/using/hardening-securing-aem-forms-environment.md) 인스턴스. 프로덕션 작성자에서 워크플로우 또는 적응형 양식 작성과 같은 실제 작성을 수행하지 마십시오.

다음 토폴로지는 OSGi 기능에서 AEM Forms 대화형 통신, 서신 관리, AEM Forms 데이터 캡처 및 Forms 중심 워크플로우를 실행하는 토폴로지 입니다. 토폴로지에 대한 자세한 내용은 [AEM Forms의 아키텍처 및 배포 토폴로지](/help/forms/using/aem-forms-architecture-deployment.md).

![recommended-topology](assets/recommended-topology.png)

OSGi의 AEM Forms Forms 중심 워크플로우는 AEM Forms의 작성자 인스턴스에서 AEM 받은 편지함 및 AEM 워크플로 모델 생성 UI를 실행합니다.

## 시스템 요구 사항 {#system-requirements}

>[!NOTE]
>
>다음으로 건너뛰기 [다음 단계](../../forms/using/installing-configuring-forms-centric-workflow-on-osgi.md#next-steps) 문서의 섹션에 설명된 대로 OSGi에 AEM Forms을 이미 설치한 경우 [데이터 캡처 기능 설치 및 구성](../../forms/using/installing-configuring-aem-forms-osgi.md) 기사.

OSGi에서 Forms 중심 워크플로를 설치하고 구성하기 전에 다음을 확인하십시오.

* 하드웨어 및 소프트웨어 인프라가 구축되어 있습니다. 지원되는 하드웨어 및 소프트웨어에 대한 자세한 목록은 [기술 요구 사항](/help/sites-deploying/technical-requirements.md).

* AEM 인스턴스의 설치 경로에 공백이 포함되어 있지 않습니다.
* AEM 인스턴스가 실행 중입니다. AEM 용어에서 &quot;인스턴스&quot;는 작성자 또는 게시 모드의 서버에서 실행되는 AEM의 사본입니다. OSGi에서 Forms 중심 워크플로우를 실행하려면 하나 이상의 AEM 인스턴스(작성자 또는 처리)가 필요합니다.

   * **작성자**: 콘텐츠를 만들고, 업로드하고, 편집하고, 웹 사이트를 관리하는 데 사용되는 AEM 인스턴스입니다. 콘텐츠를 실행할 준비가 되면 게시 인스턴스에 복제됩니다.
   * **처리 중:** 처리 인스턴스는 [경화 AEM 작성자](/help/forms/using/hardening-securing-aem-forms-environment.md) 인스턴스. 작성자 인스턴스를 설정하고 설치를 수행한 후 인스턴스를 강화할 수 있습니다.

   * **게시**: 인터넷 또는 내부 네트워크를 통해 게시된 콘텐츠를 일반에게 제공하는 AEM 인스턴스.

* 메모리 요구 사항이 충족됩니다. AEM Forms 추가 기능 패키지를 사용하려면 다음 작업을 수행해야 합니다.

   * Microsoft Windows 기반 설치용 15GB의 임시 공간.
   * UNIX 기반 설치의 경우 6GB의 임시 공간이 필요합니다.

* UNIX 기반 시스템에 대한 추가 요구 사항: UNIX 기반 운영 체제를 사용하는 경우 해당 운영 체제의 설치 미디어에서 다음 패키지를 설치합니다.

<table>
 <tbody>
  <tr>
   <td>지수</td>
   <td>libxcb</td>
   <td>자유 형식</td>
   <td>libXau</td>
  </tr>
  <tr>
   <td>libSM</td>
   <td>즐리브</td>
   <td>libice</td>
   <td>리부uid</td>
  </tr>
  <tr>
   <td>아교</td>
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

AEM Forms 추가 기능 패키지는 AEM에 배포된 애플리케이션입니다. 이 패키지에는 OSGi 및 기타 기능의 Forms 중심 워크플로가 포함되어 있습니다. 추가 기능 패키지를 설치하려면 다음 단계를 수행하십시오.

1. [소프트웨어 배포](https://experience.adobe.com/downloads)를 엽니다. 소프트웨어 배포에 로그인하려면 Adobe ID가 필요합니다.
1. 선택 **[!UICONTROL Adobe Experience Manager]** 헤더 메뉴에서 사용할 수 있습니다.
1. 다음에서 **[!UICONTROL 필터]** 섹션:
   1. 선택 **[!UICONTROL Forms]** 다음에서 **[!UICONTROL 솔루션]** 드롭다운 목록입니다.
   2. 패키지의 버전 및 유형을 선택합니다. 다음을 사용할 수도 있습니다 **[!UICONTROL 다운로드 검색]** 옵션을 사용하여 결과를 필터링할 수 있습니다.
1. 운영 체제에 적용할 수 있는 패키지 이름을 선택하고 **[!UICONTROL EULA 약관 동의]**, 및 선택 **[!UICONTROL 다운로드]**.
1. 열기 [패키지 관리자](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)  및 클릭 **[!UICONTROL 패키지 업로드]** 패키지를 업로드합니다.
1. 패키지를 선택하고 **[!UICONTROL 설치]**&#x200B;를 클릭합니다.

   AEM Forms 릴리스](https://helpx.adobe.com/kr/aem-forms/kb/aem-forms-releases.html) 문서에 나열된 [직접 링크 를 통해 패키지를 다운로드 할 수도 있습니다.

1. 패키지가 설치되면 AEM 인스턴스 다시 시작하라는 메시지가 표시됩니다. **서버를 즉시 다시 시작하지 마십시오.** AEM Forms 서버를 중지하기 전에 ServiceEvent REGISTERED 및 ServiceEvent UNREGISTERED 메시지가 AEM-Installation-Directory]/crx-quickstart/logs/error.로그 파일에 [표시되지 않고 로그가 안정될 때까지 기다립니다.

   >[!NOTE]
   >
   > SDK를 다시 시작하려면 &#39;Ctrl + C&#39; 명령을 사용하는 것이 좋습니다. Java 프로세스 중지와 같은 대체 방법을 사용하여 AEM SDK를 다시 시작하면 AEM 개발 환경에서 불일치가 발생할 리드 있습니다.

1. 모든 Author 및 Publish 인스턴스에서 1~7단계를 반복합니다.

## 설치 후 구성 {#post-installation-configurations}

AEM Forms에는 몇 가지 필수 구성과 선택적 구성이 있습니다. 필수 구성에는 BouncyCastle 라이브러리 및 직렬화 에이전트 구성이 포함됩니다. 선택적 구성에는 Dispatcher 및 Adobe Target 구성이 포함됩니다.

### 필수 사후 설치 구성 {#mandatory-post-installation-configurations}

#### RSA 및 BouncyCastle 라이브러리 구성  {#configure-rsa-and-bouncycastle-libraries}

모든 작성자 및 게시 인스턴스에서 다음 단계를 수행하여 라이브러리를 부팅합니다.

1. 기본 AEM 인스턴스를 중지합니다.
1. 를 엽니다. [AEM 설치 디렉토리]편집할 \crx-quickstart\conf\sling.properties 파일입니다.

   을 사용한 경우 [AEM 설치 디렉토리]\crx-quickstart\bin\start.bat 를 사용하여 AEM을 시작한 다음, 다음 위치에 있는 sling.properties를 편집합니다. [AEM_root]\crx-quickstart\.

1. sling.properties 파일에 다음 속성을 추가합니다.

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. 파일을 저장하고 닫은 다음 AEM 인스턴스를 시작합니다.
1. 모든 Author 및 Publish 인스턴스에서 1~4단계를 반복합니다.

#### 직렬화 에이전트 구성 {#configure-the-serialization-agent}

모든 작성자 및 게시 인스턴스에서 다음 단계를 수행하여 패키지를 허용 목록에 추가하다에 추가합니다.

1. 브라우저 창에서 AEM 구성 관리자를 엽니다. 기본 URL은 https://&#39;입니다.[server]:[포트]&#39;/system/console/configMgr.
1. 검색 및 열기 **역직렬화 방화벽 구성**.
1. 추가 **sun.util.calendar** 패키지 대상 **허용 목록** 필드. 저장을 클릭합니다.
1. 모든 Author 및 Publish 인스턴스에서 1~3단계를 반복합니다.

### 설치 후 구성 옵션 {#optional-post-installation-configurations}

#### Dispatcher 구성 {#configure-dispatcher}

Dispatcher가 AEM용 캐싱 및 로드 밸런싱 도구를 제공합니다. AEM Dispatcher는 또한 공격으로부터 AEM 서버를 보호하는 데 도움이 됩니다. Dispatcher를 엔터프라이즈급 웹 서버와 함께 사용하여 AEM 인스턴스의 보안을 강화할 수 있습니다. 를 사용하는 경우 [디스패처](https://helpx.adobe.com/kr/experience-manager/dispatcher/using/dispatcher-configuration.html)를 실행한 다음 AEM Forms에 대해 다음 구성을 수행합니다.

1. AEM Forms에 대한 액세스 구성:

   편집할 dispatcher.any 파일을 엽니다. 필터 섹션으로 이동하고 필터 섹션에 다음 필터를 추가합니다.

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   파일을 저장하고 닫습니다. 필터에 대한 자세한 내용은 [Dispatcher 설명서](https://helpx.adobe.com/kr/experience-manager/dispatcher/using/dispatcher-configuration.html).

1. 레퍼러 필터 서비스를 구성합니다.

   Apache Felix 구성 관리자에 관리자로 로그인합니다. 구성 관리자의 기본 URL은 https://&#39;server&#39;입니다.[port_number]/system/console/configMgr. 다음에서 **구성** 메뉴에서 **Apache Sling Referrer 필터** 옵션을 선택합니다. 호스트 허용 필드에 레퍼러로 허용할 Dispatcher의 호스트 이름을 입력하고 을 클릭합니다 **저장**. 항목의 형식은 다음과 같습니다. `https://'[server]:[port]'`.

#### 캐시 구성 {#configure-cache}

캐싱은 데이터 액세스 시간을 단축하고, 지연을 줄이고, 입출력(I/O) 속도를 향상시키는 메커니즘입니다. 적응형 양식 캐시는 미리 채워진 데이터를 저장하지 않고 적응형 양식의 HTML 컨텐츠 및 JSON 구조만 저장합니다. 적응형 양식을 렌더링하는 데 필요한 시간을 줄이는 데 도움이 됩니다.

* 적응형 양식 캐시를 사용할 때 다음을 사용합니다. [AEM 디스패처](https://helpx.adobe.com/kr/experience-manager/dispatcher/using/dispatcher-configuration.html) 를 클릭하여 적응형 양식의 클라이언트 라이브러리(CSS 및 JavaScript)를 캐시합니다.
* 사용자 지정 구성 요소를 개발하는 동안 개발에 사용되는 서버에서 적응형 양식 캐시를 비활성화 상태로 유지합니다.

다음 단계를 수행하여 적응형 양식 캐시를 구성합니다.

1. 에서 AEM 웹 콘솔 구성 관리자로 이동합니다. `https://'[server]:[port]'/system/console/configMgr`.
1. 클릭 **[!UICONTROL 적응형 양식 및 대화형 통신 웹 채널 구성]** 구성 값을 편집하려면 다음을 수행하십시오. 구성 값 편집 대화 상자에서 AEM Forms 서버 인스턴스가 캐시할 수 있는 최대 양식 또는 문서 수를 지정합니다. **적응형 Forms 수** 필드. 기본값은 100입니다. **저장**&#x200B;을 클릭합니다.

   >[!NOTE]
   >
   >캐시를 비활성화하려면 적응형 Forms 수 필드의 값을 다음으로 설정하십시오. **0**. 캐시 구성을 비활성화하거나 변경하면 캐시가 재설정되고 모든 양식 및 문서가 캐시에서 제거됩니다.

#### Adobe Sign 구성 {#configure-adobe-sign}

Adobe Sign은 적응형 양식용 전자 서명 워크플로를 가능하게 합니다. 전자 서명은 법무, 판매, 임금, 인적 자원 관리 등의 다양한 분야에서 문서를 처리하는 워크플로를 개선합니다.

OSGi 시나리오의 일반적인 Adobe Sign 및 Forms 중심 워크플로우에서 사용자는 다음에 대한 적응형 양식을 작성합니다. **서비스 신청**. 신용 카드 신청 양식과 시민 혜택 양식을 예로 들 수 있습니다. 사용자가 신청 양식에 정보를 입력하고 이를 제출한 뒤 서명하면 승인/거부 워크플로가 시작됩니다. 서비스 공급자는 AEM 받은 편지함에서 애플리케이션을 검토하고 Adobe Sign을 사용하여 애플리케이션에 전자 서명합니다. Adobe Sign을 AEM Forms과 통합하여 유사한 전자 서명 워크플로를 활성화할 수 있습니다.

AEM Forms에서 Adobe Sign을 사용하려면, [Adobe Sign과 AEM Forms 통합](../../forms/using/adobe-sign-integration-adaptive-forms.md).

## 다음 단계 {#next-steps}

OSGi 기능에서 Forms 중심 워크플로를 사용하도록 환경을 구성했습니다. 이제 기능을 사용하는 단계는 다음과 같습니다.

* [OSGi에서 Forms 중심 워크플로우 사용](../../forms/using/aem-forms-workflow.md)
* [워크플로 단계 참조](/help/sites-developing/workflows-step-ref.md)
* [편지 및 대화형 커뮤니케이션의 사후 처리](../../forms/using/submit-letter-topostprocess.md)
