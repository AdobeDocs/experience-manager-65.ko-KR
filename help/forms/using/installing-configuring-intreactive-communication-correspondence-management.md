---
title: 대화형 통신 설치 및 구성
seo-title: Install and configure Interactive Communications
description: 비즈니스 서신, 문서, 명세서, 혜택 공지, 마케팅 이메일, 청구서 및 환영 키트를 만들도록 AEM Forms Interactive Communications를 설치 및 구성합니다.
seo-description: Install and configure AEM Forms Interactive Communications to create business correspondences, documents, statements, benefit notices, marketing mails, bills, and welcome kits.
uuid: 8acb7f68-0b52-4acd-97e2-af31c9408e8d
topic-tags: installing
discoiquuid: 225f2bc1-6842-4c79-a66d-8024a29325c0
docset: aem65
role: Admin
exl-id: 37fcfad9-2f84-4f0c-aed8-e4a5a3303a06
source-git-commit: 18cfefb794382b5314b18a62645f1fba28d314a2
workflow-type: tm+mt
source-wordcount: '1382'
ht-degree: 8%

---

# 대화형 통신 설치 및 구성{#install-and-configure-interactive-communications}

## 소개 {#introduction}

AEM Form은 비즈니스 서신, 문서, 명세서, 혜택 공지, 마케팅 메일, 청구서 및 환영 키트와 같은 안전하고 인터랙티브한 문서의 작성, 수집, 관리 및 전달을 중앙 집중화할 수 있는 기능을 제공합니다. 이 기능을 대화형 통신이라고 합니다. 이 기능은 AEM Forms 추가 기능 패키지에 포함되어 있습니다. 추가 기능 패키지는 AEM의 작성자 또는 게시 인스턴스에 배포됩니다.

대화형 통신 기능을 사용하여 여러 형식으로 커뮤니케이션을 생성할 수 있습니다. 예를 들어 웹 및 PDF이 있습니다. AEM Workflow와 대화형 커뮤니케이션을 통합하여 고객이 원하는 채널에서 조합된 커뮤니케이션을 처리하고 고객에게 제공할 수 있습니다. 예를 들어 이메일을 통해 최종 사용자에게 커뮤니케이션을 전송하는 경우가 있습니다.

이전 버전에서 업그레이드하고 이미 서신 관리에 투자한 경우 를 설치할 수 있습니다 [호환성 패키지](../../forms/using/installing-configuring-intreactive-communication-correspondence-management.md#install-compatibility-package) 서신 관리를 계속 사용하려면 대화형 커뮤니케이션과 서신 관리 간의 차이에 대한 자세한 내용은 [대화형 통신 개요](/help/forms/using/interactive-communications-overview.md#interactive-communications-vs-correspondence-management).

AEM Forms은 강력한 엔터프라이즈급 플랫폼입니다. 대화형 커뮤니케이션은 AEM Forms의 기능 중 하나입니다. 전체 기능 목록에 대해서는 다음을 참조하십시오 [AEM Forms 소개](../../forms/using/introduction-aem-forms.md).

## 배포 토폴로지 {#deployment-topology}

AEM Forms 추가 기능 패키지는 AEM에 배포된 애플리케이션입니다. 대화형 통신 기능을 실행하려면 최소 1개의 AEM 작성자 및 처리 인스턴스만 필요합니다. 다음 토폴로지는 OSGi 기능에서 AEM Forms Interactive Communications, Correspondence Management, AEM Forms 데이터 캡처 및 Forms 중심의 워크플로우를 실행하기 위한 토폴로지를 나타냅니다. 토폴로지에 대한 자세한 내용은 [AEM Forms을 위한 아키텍처 및 배포 토폴로지](/help/forms/using/aem-forms-architecture-deployment.md).

![권장 토폴로지](assets/recommended-topology.png)

AEM Forms Interactive Communications는 AEM Forms의 작성자 인스턴스에서 관리, 작성 및 에이전트 사용자 인터페이스를 실행합니다. 게시 인스턴스는 최종 사용자가 사용할 수 있는 최종 버전의 대화형 커뮤니케이션을 호스팅합니다.

## 시스템 요구 사항 {#system-requirements}

AEM Forms의 대화형 통신 및 서신 관리 기능을 설치 및 구성하기 전에 다음을 확인하십시오.

* 하드웨어 및 소프트웨어 인프라가 제대로 구축되어 있습니다. 지원되는 하드웨어 및 소프트웨어에 대한 자세한 내용은 [기술 요구 사항](/help/sites-deploying/technical-requirements.md).

* AEM 인스턴스의 설치 경로에 공백이 들어 있지 않습니다.
* AEM 인스턴스가 실행 중입니다. AEM 용어에서 &quot;인스턴스&quot;는 작성자 또는 게시 모드에서 서버에서 실행되는 AEM의 사본입니다. AEM Forms 대화형 통신 및 서신 관리 기능을 실행하려면 하나 이상의 AEM 인스턴스(작성자 또는 처리)가 필요합니다.

   * **작성자**: 컨텐츠를 작성, 업로드 및 편집하고 웹 사이트를 관리하는 데 사용되는 AEM 인스턴스입니다. 컨텐츠가 라이브로 전환될 준비가 되면 게시 인스턴스에 복제됩니다.
   * **처리 중:** 처리 인스턴스는 [경화된 AEM 작성자](/help/forms/using/hardening-securing-aem-forms-environment.md) 인스턴스. 설치를 수행한 후 작성자 인스턴스를 설정하고 이를 취소할 수 있습니다.

   * **게시**: 인터넷 또는 내부 네트워크를 통해 대중에게 게시된 컨텐츠를 제공하는 AEM 인스턴스입니다.

* 메모리 요구 사항이 충족되었습니다. AEM Forms 추가 기능 패키지에는 다음이 필요합니다.

   * Microsoft® Windows 기반 설치를 위한 15GB의 임시 공간.
   * UNIX 기반 설치를 위한 6GB의 임시 공간.

* UNIX 기반 시스템에 대한 추가 요구 사항: UNIX 기반 운영 체제를 사용하는 경우 각 운영 체제의 설치 미디어에서 다음 패키지를 설치합니다.

<table>
 <tbody>
  <tr>
   <td>expand</td>
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
   <td>글라이치</td>
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

AEM Forms 추가 기능 패키지는 AEM에 배포된 애플리케이션입니다. 이 패키지에는 AEM Forms 대화형 통신, 서신 관리 및 기타 기능이 들어 있습니다. 추가 기능 패키지를 설치하려면 다음 단계를 수행하십시오.

1. [소프트웨어 배포](https://experience.adobe.com/downloads)를 엽니다. 소프트웨어 배포에 로그인하려면 Adobe ID가 필요합니다.
1. 헤더 메뉴에 제공된 **[!UICONTROL Adobe Experience Manager]**&#x200B;를 누릅니다.
1. 에서 **[!UICONTROL 필터]** 섹션:
   1. 선택 **[!UICONTROL Forms]** 에서 **[!UICONTROL 솔루션]** 드롭다운 목록.
   2. 패키지의 버전 및 유형을 선택합니다. 를 사용할 수도 있습니다 **[!UICONTROL 다운로드 검색]** 결과를 필터링하는 옵션.
1. 운영 체제에 해당하는 패키지 이름을 탭하고 **[!UICONTROL EULA 약관 동의]**, 탭 **[!UICONTROL 다운로드]**.
1. [패키지 관리자](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)를 열고 **[!UICONTROL 패키지 업로드]**&#x200B;를 클릭하여 패키지를 업로드합니다.
1. 패키지를 선택하고 **[!UICONTROL 설치]**&#x200B;를 클릭합니다.

   에 나열된 직접 링크를 통해 패키지를 다운로드할 수도 있습니다 [AEM Forms 릴리스](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ko) 문서.

1. 패키지가 설치되면 AEM 인스턴스를 다시 시작하라는 메시지가 표시됩니다. **서버를 즉시 다시 시작하지 마십시오.** AEM Forms Server를 중지하기 전에 ServiceEvent REGISTERED 및 ServiceEvent UNREGISTERED 메시지가 [AEM-Installation-Directory]/crx-quickstart/logs/error.log 파일 및 로그는 안정합니다.
1. 모든 작성자 및 게시 인스턴스에 대해 1-7단계를 반복합니다.

## 설치 후 구성 {#post-installation-configurations}

AEM Forms에는 몇 가지 필수 및 선택적 구성이 있습니다. 필수 구성에는 BoundcyCastle 라이브러리 및 직렬화 에이전트 구성이 포함됩니다. 선택적 구성에는 Dispatcher 및 Adobe Target 구성이 포함됩니다.

### 필수 설치 후 구성 {#mandatory-post-installation-configurations}

#### RSA 및 BouncyCastle 라이브러리 구성  {#configure-rsa-and-bouncycastle-libraries}

라이브러리를 부팅하려면 모든 작성자 및 게시 인스턴스에서 다음 단계를 수행하십시오.

1. 기본 AEM 인스턴스를 중지합니다.
1. 를 엽니다. [AEM 설치 디렉토리]\crx-quickstart\conf\sling.properties 파일을 편집할 수 있습니다.

   만약 [AEM 설치 디렉토리]\crx-quickstart\bin\start.bat에서 AEM을 시작한 다음 sling.properties를 편집합니다. [AEM_root]\crx-quickstart\.

1. sling.properties 파일에 다음 속성을 추가합니다.

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   ```

1. 파일을 저장하고 닫고 AEM 인스턴스를 시작합니다.
1. 모든 작성자 및 게시 인스턴스에 대해 1-4단계를 반복합니다.

#### 직렬화 에이전트 구성 {#configure-the-serialization-agent}

모든 작성자 및 게시 인스턴스에서 다음 단계를 수행하여 패키지를 페이지에 허용 목록에 추가하다 추가합니다.

1. 브라우저 창에서 AEM 구성 관리자를 엽니다. 기본 URL은 https://&#39; 입니다.[server]:[포트]&#39;/system/console/configMgr.
1. 검색 및 열기 **Deserialization 방화벽 구성**.
1. 추가 **sun.util.calendar** 패키지 **허용 목록에 추가하다** 필드. 저장을 클릭합니다.
1. 모든 작성자 및 게시 인스턴스에 대해 1-3단계를 반복합니다.

### 설치 후 구성 옵션 {#optional-post-installation-configurations}

#### 호환성 패키지 설치 {#install-compatibility-package}

대화형 커뮤니케이션은 AEM 6.5 Forms에서 고객 커뮤니케이션을 만드는 기본적이고 권장되는 방법입니다. 이전 버전에서 업그레이드하거나 마이그레이션한 후 편지(서신 관리)를 계속 사용할 계획이라면 [AEMFD 호환성 패키지](https://experienceleague.adobe.com/docs/experience-manager-65/forms/upgrade-aem-forms/aem-forms-osgi-upgrade/compatibility-package.html?lang=en).

AEMFD 호환성 패키지를 사용하면 AEM 6.5 Forms에 있는 AEM 6.4 Forms, AEM 6.3 Forms 및 AEM 6.2 Forms의 다음 자산을 사용할 수 있습니다.

* 문서 조각
* 편지
* 데이터 사전
* 사용되지 않는 적응형 양식 템플릿 및 페이지

#### Dispatcher 구성 {#configure-dispatcher}

Dispatcher는 엔터프라이즈급 웹 서버와 함께 사용하는 Adobe Experience Manager의 캐싱 및 로드 밸런싱 도구입니다. 만약 [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=ko-KR)그런 다음 AEM Forms에 대해 다음 구성을 수행합니다.

1. AEM Forms에 대한 액세스 구성:

   편집할 dispatcher.any 파일을 엽니다. 필터 섹션으로 이동하고 필터 섹션에 다음 필터를 추가합니다.

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   파일을 저장하고 닫습니다. 필터에 대한 자세한 내용은 [Dispatcher 설명서](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=ko-KR).

1. 레퍼러 필터 서비스를 구성합니다.

   관리자로 Apache Felix 구성 관리자에 로그인합니다. 구성 관리자의 기본 URL은 https://&#39;server&#39;입니다.[port_number]/system/console/configMgr. 에서 **구성** 메뉴에서 **Apache Sling 레퍼러 필터** 선택 사항입니다. 호스트 허용 필드에 Dispatcher의 호스트 이름을 입력하여 레퍼러로 허용하고 를 클릭합니다 **저장**. 항목의 형식은 https://&#39;입니다.[server]:[포트]&#39;

#### Adobe Target 통합 {#integrate-adobe-target}

고객이 매력적인 경험을 하지 않을 경우 대화형 커뮤니케이션을 포기할 수 있습니다. 고객에게 좌절감을 주지만 조직에 대한 지원 볼륨과 비용도 증가합니다. 전환율을 높일 수 있는 올바른 고객 경험을 식별하고 제공하기 위해서는 매우 중요하며 쉽지 않습니다. AEM forms는 이 문제의 주요 해결방법을 제공합니다.

AEM Forms는 Adobe Experience Cloud 솔루션인 Adobe Target과 통합되어 있으며, 여러 디지털 채널에서 개인화되고 매력적인 고객 경험을 제공할 수 있습니다. Adobe Target을 사용하여 대화형 커뮤니케이션을 개인화하려면, [Adobe Target과 AEM Forms 통합](../../forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms).

#### 양식 데이터 모델에 대한 SSL 통신 구성  {#configure-ssl-communcation-for-form-data-model}

양식 데이터 모델에 대해 SSL 통신을 활성화할 수 있습니다. 양식 데이터 모델에 대해 SSL 통신을 사용하려면 AEM Forms 인스턴스를 시작하기 전에 모든 인스턴스의 Java™ Trust Store에 인증서를 추가하십시오. 아래 명령을 실행하여 인증서를 추가할 수 있습니다.

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

## 다음 단계 {#next-steps}

대화형 통신 및 서신 관리 기능을 사용할 환경을 구성했습니다. 이제 기능을 사용하는 단계는 다음과 같습니다.

* [서신 관리 개요](/help/forms/using/interactive-communications-overview.md)

* [대화형 통신 만들기](../../forms/using/create-interactive-communication.md)

* [서신 관리 편지 만들기](../../forms/using/create-letter.md)
