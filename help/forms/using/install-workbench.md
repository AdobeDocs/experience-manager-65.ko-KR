---
title: Workbench 설치
description: AEM Forms Workbench를 설치, 제거, 구성, 관리 또는 배포하는 방법에 대해 알아봅니다.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
role: Admin
exl-id: d530dbb9-f95e-4329-9665-37faf8f7931b
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2184'
ht-degree: 0%

---

# Workbench 설치 {#install-workbench}

이 문서에서는 AEM Forms Workbench 설치 및 구성에 대한 지침을 제공합니다. 설치 프로그램은 Forms Designer도 설치합니다.

## 누가 이 문서를 읽어야 합니까? {#who-should-read-this-doc}

이 문서는 Workbench의 설치, 구성, 관리 또는 배포를 담당하는 관리자 또는 개발자를 위한 것입니다. 업그레이드된 AEM Forms 프로세스를 지원하도록 시스템을 구성하는 정보도 포함되어 있습니다. 제공된 정보는 이 문서를 읽는 모든 사람이 Microsoft® Windows® 운영 체제에 익숙하다는 가정을 기반으로 합니다.

## 추가 정보 {#additional-information}

이 표의 리소스는 AEM Forms에 대해 자세히 알아보고 사용을 시작하는 데 도움이 될 수 있습니다.
<table>
 <tbody>
  <tr>
   <td><p><strong>다음에 대한</strong></p> </td>
   <td><p><strong>자세한 내용은</strong></p> </td>
  </tr>
  <tr>
   <td><p>Workbench에 대한 절차 정보</p> </td>
   <td><p><a href="https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf">Workbench 도움말</a><br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>AEM Forms 및 다른 Adobe 제품과 통합하는 방법에 대한 일반 정보</p> </td>
   <td><p><a href="https://experienceleague.adobe.com/docs/experience-manager-65/forms/getting-started/introduction-aem-forms.html?lang=en">AEM Forms 개요</a><br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>AEM Forms에 사용할 수 있는 모든 설명서</p> </td>
   <td><p><a href="https://experienceleague.adobe.com/docs/experience-manager-65/forms/getting-started/introduction-aem-forms.html?lang=en">AEM Forms 설명서</a><br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>이 제품 버전에 대한 패치 업데이트, 기술 참고 사항 및 추가 정보</p> </td>
   <td><p>Adobe 엔터프라이즈 지원 문의</a><br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Flex Workspace는 AEM Forms에서 더 이상 사용되지 않습니다. AEM Forms 릴리스에서 사용할 수 있습니다.

## 설치하기 전에 {#before-you-install}

### Workbench 설치 개요 {#workbench-installation-overview}

Workbench는 개발자와 양식 작성자가 자동화된 비즈니스 프로세스 및 양식을 만드는 데 사용하는 통합 개발 환경(IDE)입니다. 프로세스 및 양식에서 사용하는 리소스 및 서비스를 관리하는 데에도 사용됩니다.

다음 그림은 다음을 포함한 Workbench 설치를 보여 줍니다.
* Workbench를 사용한 프로세스 디자인
* 디자이너를 사용한 양식 디자인

>[!NOTE]
>
>AEM Forms 서버에는 별도의 설치 프로그램이 필요합니다. 자세한 내용은 AEM Forms on JEE 설치 설명서를 참조하십시오.

![default-render-form](assets/installing-workbench.png)

## 시스템 사전 요구 사항 {#system-prerequisites}

이 섹션에서는 하드웨어 및 소프트웨어 요구 사항과 지원되는 플랫폼에 대해 간략히 설명합니다.

### 최소 하드웨어 및 소프트웨어 요구 사항 {#minimum-hardware-software-requirements}

**Workbench**
최소 요구 사항은 다음과 같습니다. 설치를 위한 디스크 공간:
* 680MB(Workbench 전용)
* Workbench, Designer 및 샘플 어셈블리의 전체 설치를 위해 단일 드라이브에 2.15GB가 제공됩니다.
* 임시 설치 디렉토리의 경우 400MB - 사용자 \temp 디렉토리의 경우 200MB, Windows 임시 디렉토리의 경우 200MB입니다.

>[!NOTE]
>
>이러한 위치가 모두 단일 드라이브에 있는 경우 설치하는 동안 1.5GB의 공간을 사용할 수 있어야 합니다. 임시 디렉토리에 복사된 파일은 설치가 완료되면 삭제됩니다.

* 하드웨어 요구 사항: Intel® Pentium® 4 또는 AMD® 동급 1GHz 프로세서
* JRE(Java™ Runtime Environment) 7.0 업데이트 51 이상 7.0 업데이트.
* 최소 1024X768픽셀 이상의 모니터 해상도(16비트 색상 이상)
* AEM Forms 서버에 대한 TCP/IPv4 또는 TCP/IPv6 네트워크 연결입니다.
* Visual C++ 재배포 가능 런타임 패키지 2012 32비트를 설치합니다.
* Visual C++ 재배포 가능 런타임 패키지 2013 32비트를 설치합니다.

>[!NOTE]
>
>Workbench를 설치하려면 관리 권한이 있어야 합니다. 관리자가 아닌 계정을 사용하여 설치하는 경우 설치 프로그램에서 적절한 계정에 대한 자격 증명을 입력하라는 메시지가 표시됩니다.

### 지원되는 플랫폼 {#supported-platforms}

Workbench에서 지원되는 플랫폼의 전체 목록을 참조하십시오. [AEM Forms 지원 플랫폼](https://www.adobe.com/go/learn_aemforms_supportedplatforms_65).

## 디자이너 설치 고려 사항 {#designer-installation-considerations}

기본적으로 Workbench 설치에는 해당 영어 전용 버전의 Designer가 포함되어 있습니다. Workbench 설치 응용 프로그램에서 컴퓨터에 있는 기존 버전의 디자이너를 검색하면 설치가 종료될 수 있으며, 계속하려면 현재 버전의 디자이너를 제거해야 합니다.
아래 표에는 Workbench를 설치할 때 발생할 수 있는 가능한 Designer 설치 시나리오와 수행해야 하는 모든 작업의 전체 목록이 나와 있습니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>현재 설치된 Designer 버전</strong></p> </td>
   <td><p><strong>필수 작업</strong></p> </td>
  </tr>
  <tr>
   <td><p>Acrobat Pro 또는 Acrobat Pro Extended(Designer 포함)</p> </td>
   <td><p>없음.<br /> 
Workbench 설치는 Acrobat Pro 또는 Acrobat Pro Extended와 함께 설치된 컴퓨터에서 Designer 인스턴스를 검색합니다.<br />
Workbench 6.4용 Designer 6.4.x 및 Workbench 6.5용 Designer 6.5.0.x와 같은 동일한 시스템에 서로 다른 버전의 Designer가 함께 사용할 수 있습니다. Acrobat 10 Pro 또는 Acrobat 10 Pro Extended 이상과 함께 설치된 Designer 버전은 제거할 필요가 없습니다.
<br /></p> </td>
  </tr>
  <tr>
   <td><p>디자이너(독립형)</p> </td>
   <td><p>없음. <br />Workbench에 포함된 Designer 버전은 영어로만 사용할 수 있습니다. <br />Workbench 설치 관리자는 새 버전의 디자이너를 다시 설치하지 않습니다. 대신 Workbench 설치 프로그램과 번들로 제공되는 업데이트된 버전이 패치됩니다. 또한 Workbench 내에서 현지화된 버전의 디자이너를 사용할 수 있습니다.<br /> </p> </td>
  </tr>
 </tbody>
</table>

### Windows 10에서 Designer(독립 실행형)를 제거하려면 {#uninstall-designer-standalone-windows10}

1. 다음으로 이동 **Campaign 컨트롤 패널 > 프로그램 > 프로그램 및 기능**
1. 현재 설치된 프로그램 목록에서 **Adobe 디자이너**.
1. 클릭 **제거** 그런 다음 을 클릭합니다. **예**.

## Workbench 설치 {#installing-workbench}

이 장에서는 Workbench를 설치하는 방법을 설명합니다.

### Workbench 설치 및 실행 {#installing-and-running-workbench}

Workbench를 설치하기 전에 환경에 Workbench를 실행하는 데 필요한 소프트웨어 및 하드웨어가 포함되어 있는지 확인해야 합니다( 섹션 참조). **설치하기 전에**).

**Workbench를 설치하고 실행하려면**

1. 다음 작업 중 하나를 수행합니다.
   * 설치 미디어에서 \workbench 디렉터리로 이동하고 run_windows_installer.bat 파일을 두 번 클릭합니다.
   * 파일 시스템에 Workbench를 다운로드하고 압축을 풉니다. 다운로드한 후 \workbench 디렉토리로 이동하고 run_windows_installer.bat 파일을 두 번 클릭합니다.

   >[!IMPORTANT]
   >
   >Workbench 설치 관리자는 로컬 드라이브에서만 실행됩니다. 원격 사이트에서 실행할 수 없습니다.

   >[!NOTE]
   >
   >&quot;Java™ 가상 컴퓨터를 만들 수 없습니다.&quot; 오류가 발생하면 값이 -Xmx512M인 _JAVA_VARIABLES라는 환경 OPTIONS을 만들고 설치 관리자를 실행합니다.

1. 소개 화면에서 다음을 클릭합니다.
1. 제품 사용권 계약을 읽고 I accept the terms of the License Agreement 를 선택한 후 Next 를 클릭합니다.
1. (선택 사항) 양식을 만들고 수정하는 데 이 도구가 필요한 경우 Adobe 디자이너 설치를 선택합니다.

   >[!NOTE]
   >
   >이 옵션을 선택 취소하여 Acrobat 10과 함께 설치된 디자이너를 계속 사용할 수 있습니다.

1. 나열된 기본 디렉터리를 그대로 사용하거나 [선택]을 클릭하고 Workbench를 설치할 디렉터리로 이동한 후 [다음]을 클릭합니다.

   >[!NOTE]
   >
   >설치 디렉토리 경로에는 #(파운드) 및 $(달러) 문자를 사용할 수 없습니다.

1. 사전 설치 요약을 검토하고 설치 를 클릭합니다. 설치 프로그램에 설치 진행률이 표시됩니다.
1. 설치 요약을 검토합니다. AEM Forms Workbench 시작을 선택하여 Workbench를 시작한 후 다음을 클릭합니다.
1. 릴리스 정보를 검토하고 완료 를 클릭합니다.
1. 이제 다음 항목이 컴퓨터에 설치됩니다.
   * **Workbench**: 시작 메뉴에서 Workbench를 실행하려면 모든 프로그램 > AEM Forms > Workbench를 선택합니다(바로 가기 폴더를 여기에 저장하기로 선택한 경우). 자세한 내용은 <a href="https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf">Workbench 사용</a> 설명서를 참조하십시오.
   * **디자이너**: Workbench 내에서 Designer에 액세스할 수 있습니다. 자세한 내용은 의 시작하기 항목을 참조하십시오. <a href="https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/using-designer.pdf">디자이너 도움말</a>.
   * **AEM FORMS SDK**: SDK 사용에 대한 자세한 내용은 다음을 참조하십시오. <a href="https://helpx.adobe.com/pdf/aem-forms/6-3/programming-with-aem-forms.pdf">AEM Forms을 사용한 프로그래밍</a>.

## 프로세스 업그레이드 {#upgrading-processes}

업그레이드 마법사를 사용하여 AEM Forms on JEE 프로세스를 AEM Forms 애플리케이션으로 업그레이드할 수 있습니다. 자세한 내용은 Workbench 도움말의 기존 객체 업그레이드 설명서 를 참조하십시오.

### 서버 구성 및 로그인 {#configuring-and-logging-server}

Workbench를 사용하려면 일반적으로 별도의 컴퓨터에서 실행 중인 AEM Forms 인스턴스가 있어야 합니다. AEM Forms에 로그온하려면 사용자 이름 및 암호와 서버 위치에 대한 세부 정보가 있어야 합니다.

>[!NOTE]
>
>EMC Documentum® 또는 IBM® FileNet Repository Provider를 사용하도록 AEM Forms을 구성한 경우 AEM Forms 관리 콘솔에서 기본값으로 구성된 저장소 이외의 저장소에 로그인하려면 사용자 이름을 username@Repository으로 입력합니다.

### 시간 초과 설정 구성 {#configuring-timeout-settings}

기본적으로 Workbench는 활동 또는 비활동에 관계없이 2시간 후에 시간 초과됩니다. 시간 초과 설정을 편집하려면 다음에서 &quot;사용자 관리 구성 > 고급 시스템 속성 구성&quot;을 참조하십시오. <a href="https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/configure-user-management/configure-advanced-system-attributes.html">관리 콘솔 도움말</a>.

### HTTPS를 통해 연결하도록 Workbench 구성 {#configuring-workbench-to-connect-over-HTTPS}

HTTPS를 통해 Workbench를 AEM Forms 서버에 연결하려면 공개 키를 발급한 인증 기관(CA)이 Workbench에서 신뢰되는 것으로 인식되는지 확인해야 합니다. 인증서가 신뢰할 수 있는 소스에서 온 것으로 인식되지 않는 경우 [Workbench_HOME]/workbench/jre/lib/security 디렉터리.

>[!NOTE]
>
>[Workbench_HOME] Workbench를 설치한 디렉토리를 나타냅니다. 기본 위치는 C:\Program Files (x86)\Adobe Experience Manager forms Workbench입니다.

인증서에 지정된 이름을 사용하여 HTTPS에 연결해야 합니다. 이 이름은 일반적으로 정규화된 호스트 이름입니다.

**cacert 파일을 업데이트하려면**:
1. SSL(Secure Sockets Layer) 인증서 사본이 있는지 확인합니다. SSL 서버를 구성한 관리자에게 문의하거나 웹 브라우저를 사용하여 인증서를 내보냅니다.

   >[!NOTE]
   >
   >인증서를 내보내려면 웹 브라우저를 열고 관리 콘솔에 로그인합니다. 브라우저에 인증서를 설치한 다음 브라우저에서 임시 저장소 위치로(또는 로 직접) 인증서를 내보냅니다. [Workbench_HOME]/workbench/jre/lib/security directory).

1. 에 인증서 복사 [Workbench_HOME]/workbench/jre/lib/security 디렉터리.

1. 명령 프롬프트 창을 열고 다음으로 이동 [Workbench_HOME]/workbench/jre/bin을 클릭한 후 다음 명령을 입력합니다.
   `keytool -import -storepass changeit -file [Workbench_HOME]\workbench\jre\lib\security\ssl_cert_for_certname.cer -keystore [Workbench_HOME]\workbench\jre\lib\security\cacerts -alias example`
위치:
   * `changeit` 는 cacerts 키 저장소의 기본 암호입니다.
   * certname은 1단계에서 선택한 인증서입니다.
   * 인증서에 대해 선택하는 별칭을 예로 들 수 있습니다. 이 값은 변경할 수 있습니다.

1. 인증서를 신뢰하라는 메시지가 표시되면 Yes 를 입력하고 Enter 키를 누릅니다. keytool은 cacerts 파일을 [Workbench_HOME]/workbench/jre/lib/security 디렉터리.

1. 워크벤치를 닫고 다시 시작하여 변경 사항을 적용합니다.

### 동적으로 생성된 템플릿에 대한 캐시 설정 구성 {#configuring-cache-settings-for-dynamically-generated-templates}

애플리케이션이 XFA 콘텐츠를 자동으로 업데이트하여 즉석으로 고유 템플릿을 생성하는 경우 캐시 작업의 다음 측면을 고려해야 합니다. 실제로 각 트랜잭션은 새로운 고유 템플릿을 사용합니다.

양식 생성기 또는 출력에서 특정 양식 서식 파일에 대한 캐시의 항목을 검색하거나 업데이트할 때 여러 키 값을 사용하여 액세스된 특정 캐시 항목을 찾습니다.

* **템플릿 파일 이름**: 캐시된 양식의 기본 고유 식별자로 사용되는 템플릿의 위치 및 파일 이름입니다.
* **타임스탬프**: 템플릿 파일에는 양식의 마지막 업데이트 시간을 결정하는 데 사용되는 타임스탬프가 포함되어 있습니다.
* **템플릿 UUID**: 디자이너가 양식 및 해당 버전에 대한 고유 식별자(UUID)를 각 템플릿에 삽입합니다. 양식이 업데이트될 때마다 임베드된 UUID가 업데이트됩니다. 예를 들어 XDP 템플릿은 다음 콘텐츠를 표시할 수 있습니다.

  `<?xml version="1.0" encoding="UTF-8"?>`
  `<?xfa generator="AdobeAEM formsDesignerES_V8.2" APIVersion="2.6.7185.0"?><xdp:xdp xmlns:xdp=https://ns.adobe.com/xdp/ timeStamp="2008-07-29T21:22:12Z" uuid="823e538f-ff6c-4961-b759-f7626978a223"><template xmlns="https://www.xfa.org/schema/xfa-template/2.6/">`

* **렌더링 옵션**: 렌더링된 양식 캐시 내에서 캐시 콘텐츠는 각각의 고유한 렌더링 옵션 세트에 대해 별도로 저장됩니다.


Forms 서비스는 파일 이름 또는 저장소 위치를 참조하거나 값을 기준으로 메모리의 XML 객체로 템플릿을 수신합니다.

* **참조로 전달된 템플릿**: 컨텐츠 루트와 양식 이름을 사용합니다. 이 방법을 사용하여 모든 요청에서 파일 이름이 다른 고유한 템플릿을 전달하면 디스크 캐시가 끊임없이 증가하며 재사용되지 않습니다. 이를 방지하려면 고유한 템플릿을 동일한 파일 이름으로 전달하여 모든 요청에 대해 동일한 캐시가 업데이트되도록 해야 합니다.
* **값으로 전달된 템플릿**: inDataDoc 매개 변수를 사용하여 데이터와 함께 전달된 템플릿 바이트를 사용합니다. 다른 UUID를 사용하는 고유한 템플릿이 이 방법으로 전달되면 디스크 캐시가 계속 증가하여 재사용되지 않습니다. 이를 방지하려면 템플릿에 대한 캐시가 생성되지 않도록 모든 템플릿에서 UUID 속성을 제거해야 합니다. 또는 null이 아닌 동일한 UUID를 전달하면 캐시 개체를 만들 수 있지만 각 요청에서 동일한 캐시가 업데이트되도록 합니다.

캐시가 끝없이 증가하지 않도록 하려면 새로운 AEM Forms API, renderHTMLForm2 및 renderPDFForm2를 사용하여 동적으로 생성된 템플릿을 렌더링하기 위한 다음 요소를 고려하십시오.

새 API를 사용할 때 템플릿은 문서 개체로 전달되며, 수동화되었는지 여부에 따라 Forms 서비스에서 처리됩니다.

UUID 및 콘텐츠 루트가 캐시 키로 사용되는 수동 문서의 경우 다음 측면을 고려하십시오.

* 캐시는 UUID가 없는 수동 입력 템플릿에 대해 생성되지 않습니다.
* 동일한 UUID 및 컨텐츠 루트를 가진 두 개 이상의 수동 입력 템플릿이 전달되면 동일한 캐시를 덮어씁니다.

파일 이름과 컨텐츠 루트가 캐시 키로 사용되는 부동화되지 않은 문서의 경우 다음 측면을 고려하십시오.

* 수동화되지 않은 입력 템플릿의 경우 캐싱은 문서가 생성된 컨텐츠 루트와 파일 이름에 따라 다릅니다.
동일한 캐시는 콘텐츠 루트 및 템플릿 파일 이름이 동일한 요청에만 사용됩니다.
다음 모범 사례에서는 동적으로 생성된 템플릿을 Forms 서비스에 전달할 때 캐시가 끊임없이 증가하지 않도록 합니다.
   * 동적으로 생성된 모든 템플릿에서 UUID를 삭제하거나 동일한 UUID를 전달합니다.
   * 템플릿 바이트 또는 디스크의 동일한 파일 이름에서 문서를 생성합니다.

### Workbench 제거 {#uninstalling-workbench}

제거 프로그램을 시작할 수 있도록 Campaign 컨트롤 패널에서 프로그램 추가/제거 기능을 사용하십시오. Workbench 및 Designer 응용 프로그램에는 별도의 제거 프로그램이 있습니다.

## AEM Forms XDC 편집기 구성 {#configuring-aem-forms-xdc-editor}

네트워크 프린터 관리자는 XDC 편집기를 사용하여 XML Forms 아키텍처 XDC(장치 구성) 파일을 만들고 수정할 수 있습니다. XDC 파일은 프린터 언어 또는 용지 크기와 용지함 위치 간의 상관 관계와 같은 프린터의 기능을 설명합니다.

네트워크 프린터 관리자가 XDC 편집기를 사용하기 전에 샘플 XDC 파일을 재배치하고 XDC 편집기를 사용하여 장치 프로필 만들기 를 참조하십시오.

**샘플 XDC 파일을 가져오려면**:

1. AEM Forms 서버에서 의 XDC 폴더를 찾습니다. [AEM Forms 루트]\sdk\samples\Output\IVS입니다.
1. 이 폴더의 내용을 Workbench 또는 Eclipse 시스템에서 액세스할 수 있는 디렉토리에 복사합니다.

**XDC 편집기 도움말을 보려면**:

1. AEM Forms 설명서 웹 사이트로 이동합니다.
1. 다음을 클릭합니다. **개발** 를 탭하고 XDC 편집기를 사용하여 장치 프로필 만들기 로 이동합니다. xdc_editor_help_web.zip 파일을 다운로드하고 Readme 파일에 제공된 지침에 따라 도움말 파일을 설치합니다.
