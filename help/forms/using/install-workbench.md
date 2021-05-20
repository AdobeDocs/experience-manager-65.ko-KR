---
title: Workbench 설치
seo-title: Workbench 설치
description: Workbench를 설치합니다.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
role: Administrator
exl-id: d530dbb9-f95e-4329-9665-37faf8f7931b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2246'
ht-degree: 0%

---

# Workbench {#install-workbench} 설치

이 문서에서는 AEM Forms Workbench 설치 및 구성에 대한 지침을 제공합니다. 설치 프로그램은 Forms Designer도 설치합니다.

## 누가 이 문서를 읽어야 합니까?{#who-should-read-this-doc}

이 문서는 Workbench 설치, 구성, 관리 또는 배포를 담당하는 관리자 또는 개발자를 위한 것입니다. 업그레이드된 AEM Forms 프로세스를 지원하도록 시스템을 구성하는 데 필요한 정보가 포함되어 있습니다. 제공된 정보는 이 문서를 읽는 사람이 Microsoft® Windows® 운영 체제를 잘 알고 있다는 가정을 기반으로 합니다.

## 추가 정보 {#additional-information}

이 테이블의 리소스를 통해 AEM Forms에 대해 자세히 알아보고 사용할 수 있습니다.
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
   <td><p><a href="http://adobe.com/go/learn_aemforms_introduction_65">AEM Forms 개요</a><br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>AEM Forms에 사용할 수 있는 모든 설명서</p> </td>
   <td><p><a href="http://adobe.com/go/learn_aemforms_introduction_65">AEM Forms 설명서</a><br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>이 제품 버전에 대한 패치 업데이트, 기술 정보 및 추가 정보</p> </td>
   <td><p>Adobe 엔터프라이즈 지원에 문의</a><br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Flex Workspace는 AEM Forms에서 더 이상 사용되지 않습니다. AEM Forms 릴리스에서 사용할 수 있습니다.

## {#before-you-install} 설치 전

### Workbench 설치 개요 {#workbench-installation-overview}

Workbench는 개발자와 양식 작성자가 자동화된 비즈니스 프로세스와 양식을 만드는 데 사용하는 IDE(통합 개발 환경)입니다. 또한 프로세스와 양식에서 사용하는 리소스 및 서비스를 관리하는 데에도 사용됩니다.

다음 그림은 다음과 같은 Workbench 설치를 설명합니다.
* Workbench를 사용한 프로세스 디자인
* 디자이너를 사용한 양식 디자인

>[!NOTE]
>
>AEM Forms 서버에는 별도의 설치 프로그램이 필요합니다. 자세한 내용은 JEE의 AEM Forms 설치 설명서를 참조하십시오.

![default-render-form](assets/installing-workbench.png)

## 시스템 사전 요구 사항 {#system-prerequisites}

이 섹션에서는 하드웨어 및 소프트웨어 요구 사항과 지원되는 플랫폼에 대해 설명합니다.

### 최소 하드웨어 및 소프트웨어 요구 사항 {#minimum-hardware-software-requirements}

****
Workbench최소 요구 사항은 다음과 같습니다.설치 디스크 공간:
* 680MB(Workbench 전용)
* Workbench, Designer 및 샘플 어셈블리를 완전히 설치하려면 단일 드라이브에 2.15GB가 있습니다.
* 임시 설치 디렉터리의 경우 400MB - 사용자 \temp 디렉터리에 200MB, Windows 임시 디렉터리에 200MB입니다.

>[!NOTE]
>
>이러한 모든 위치가 단일 드라이브에 있는 경우 설치 중에 1.5GB의 공간이 있어야 합니다. 설치가 완료되면 임시 디렉토리에 복사된 파일이 삭제됩니다.

* 하드웨어 요구 사항:Intel® Pentium® 4 또는 AMD 동급 프로세서 1GHz 프로세서
* Java™ Runtime Environment(JRE) 7.0 은 51 이상을 업데이트하여 7.0으로 업데이트합니다.
* 최소 1024 X 768픽셀 이상(16비트 색상 이상) 모니터 해상도
* AEM Forms 서버에 대한 TCP/IPv4 또는 TCP/IPv6 네트워크 연결입니다.
* Visual C++ 재배포 가능 런타임 패키지 2012 32비트를 설치합니다.
* Visual C++ 재배포 가능 런타임 패키지 2013 32비트를 설치합니다.

>[!NOTE]
>
>Workbench를 설치하려면 관리 권한이 있어야 합니다. 관리자가 아닌 계정을 사용하여 설치하는 경우 설치 관리자에서 적절한 계정에 대한 자격 증명을 입력하라는 메시지를 표시합니다.

### 지원되는 플랫폼 {#supported-platforms}

[AEM Forms 지원 플랫폼](http://adobe.com/go/learn_aemforms_supportedplatforms_65)에서 Workbench에 대해 지원되는 플랫폼 전체 목록을 참조하십시오.

## 디자이너 설치 고려 사항 {#designer-installation-considerations}

기본적으로 Workbench 설치에는 해당 영어 전용 버전의 Designer가 포함되어 있습니다. Workbench 설치 응용 프로그램에서 컴퓨터의 기존 버전의 Designer를 감지하면 설치가 종료될 수 있으며, 계속하려면 현재 버전의 Designer를 제거해야 합니다.
아래 표에는 Workbench 설치 시 수행해야 하는 작업과 발생할 수 있는 Designer 설치 시나리오의 전체 목록이 나와 있습니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>현재 설치된 Designer 버전</strong></p> </td>
   <td><p><strong>필수 작업</strong></p> </td>
  </tr>
  <tr>
   <td><p>Acrobat Pro 또는 Acrobat Pro Extended(디자이너 포함)</p> </td>
   <td><p>없음.<br /> 
Workbench 설치에서 Acrobat Pro 또는 Acrobat Pro Extended와 함께 설치된 컴퓨터의 디자이너 인스턴스를 검색합니다.<br />
Workbench 6.4용 Designer 6.4.x 및 Workbench 6.5용 Designer 6.5.0.x와 같은 다른 버전의 설계자가 동일한 시스템에 공존할 수 있습니다. Acrobat 10 Pro 또는 Acrobat 10 Pro Extended 이상에 설치된 Designer 버전을 제거할 필요는 없습니다.
<br /></p> </td>
  </tr>
  <tr>
   <td><p>디자이너(독립형)</p> </td>
   <td><p>없음. <br />Workbench에 포함된 디자이너 버전은 영어 전용입니다. <br />Workbench 설치 프로그램은 새 버전의 Designer를 다시 설치하지 않습니다. 대신 Workbench 설치 프로그램과 함께 번들로 제공된 업데이트된 버전이 패치됩니다. Workbench에서 현지화된 버전의 디자이너를 사용할 수도 있습니다.<br /> </p> </td>
  </tr>
 </tbody>
</table>

### Windows 10에서 디자이너(독립형)를 제거하려면 {#uninstall-designer-standalone-windows10}

1. **Campaign 컨트롤 패널 > 프로그램 > 프로그램 및 기능**&#x200B;으로 이동합니다.
1. 현재 설치된 프로그램 목록에서 **Adobe 디자이너**&#x200B;를 선택합니다.
1. **제거**&#x200B;를 클릭한 다음 **예**&#x200B;를 클릭합니다.

## Workbench {#installing-workbench} 설치

이 장에서는 Workbench 설치 방법에 대해 설명합니다.

### Workbench {#installing-and-running-workbench} 설치 및 실행

Workbench를 설치하기 전에 환경에 Workbench를 실행하는 데 필요한 소프트웨어 및 하드웨어가 포함되어 있는지 확인해야 합니다(섹션 참조:**설치하기 전에**).

**Workbench를 설치하고 실행하려면**

1. 다음 작업 중 하나를 수행합니다.
   * 설치 미디어의 \workbench 디렉토리로 이동하고 run_windows_installer.bat 파일을 두 번 클릭합니다.
   * 워크벤치를 다운로드하여 파일 시스템에 압축을 해제합니다. 다운로드한 후 \workbench 디렉토리로 이동하고 run_windows_installer.bat 파일을 두 번 클릭합니다.

   >[!IMPORTANT]
   >
   >Workbench 설치 프로그램은 로컬 드라이브에서만 실행됩니다. 원격 사이트에서 실행할 수 없습니다.

   >[!NOTE]
   >
   >&quot;Java 가상 컴퓨터를 만들 수 없습니다.&quot; 오류가 발생하면 -Xmx512M 값을 사용하여 _JAVA_OPTIONS라는 환경 변수를 만들고 설치 관리자를 실행합니다.

1. 소개 화면에서 다음을 클릭합니다.
1. Product License Agreement(제품 사용권 계약)를 읽고 I accept the terms of the License Agreement(사용권 계약 약관에 동의함)를 선택한 다음 Next(다음)를 클릭합니다.
1. (선택 사항) 양식을 만들고 수정하는 데 이 도구가 필요한 경우 Adobe 디자이너 설치 를 선택합니다.

   >[!NOTE]
   >
   >이 옵션을 선택 취소하여 Acrobat 10과 함께 설치된 디자이너를 계속 사용할 수 있습니다.

1. 기본 디렉토리를 나열하거나   을 클릭하고 Workbench를 설치할 디렉토리로 이동한 다음 다음을 클릭합니다.

   >[!NOTE]
   >
   >설치 디렉터리 경로에는 #(파운드)과 $(달러)를 사용할 수 없습니다.

1. 사전 설치 요약을 검토하고 설치를 클릭합니다. 설치 프로그램이 설치 진행 상황을 표시합니다.
1. 설치 요약을 검토합니다. AEM Forms Workbench 시작 을 선택하여 Workbench를 실행하고 다음 을 클릭합니다.
1. 릴리스 노트를 검토하고 완료를 클릭합니다.
1. 이제 컴퓨터에 다음 항목이 설치됩니다.
   * **Workbench**:시작 메뉴에서 Workbench를 실행하려면 바로 가기 폴더를 저장하도록 선택한 경우 모든 프로그램 > AEM Forms > 워크벤치를 선택합니다. 자세한 내용은   <a href="https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf">Workbench</a> 사용 설명서를 참조하십시오.
   * **디자이너**:Workbench 내에서 디자이너에 액세스할 수 있습니다. 자세한 내용은 <a href="https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/using-designer.pdf">디자이너 도움말</a>의 시작 항목을 참조하십시오.
   * **AEM Forms SDK**:SDK 사용에 대한 자세한 내용은  <a href="http://www.adobe.com/go/learn_aemforms_programming_65">AEM Forms을 사용하여 프로그래밍</a>을 참조하십시오.

## 업그레이드 프로세스 {#upgrading-processes}

업그레이드 마법사를 사용하여 JEE의 AEM Forms 프로세스를 AEM Forms 응용 프로그램으로 업그레이드할 수 있습니다. 자세한 내용은 Workbench 도움말의 이전 객체 설명서 업그레이드 를 참조하십시오.

### 서버 {#configuring-and-logging-server} 구성 및 로그인

Workbench를 사용하려면 일반적으로 별도의 컴퓨터에서 실행되는 AEM Forms 인스턴스가 있어야 합니다. AEM Forms에 로그인하려면 사용자 이름 및 암호와 서버 위치에 대한 세부 사항이 있어야 합니다.

>[!NOTE]
>
>EMC Documentum 또는 IBM FileNet 저장소 공급자를 사용하도록 AEM Forms을 구성한 경우 AEM Forms 관리 콘솔에서 기본값으로 구성된 저장소 이외의 저장소에 로그인하려면 사용자 이름을 username@Repository으로 지정하십시오.

### 시간 초과 설정 구성 {#configuring-timeout-settings}

기본적으로 Workbench는 활동 또는 비활동과 관계없이 2시간 후에 시간 초과됩니다. 시간 초과 설정을 편집하려면 <a href="https://docs.adobe.com/content/help/en/experience-manager-65/forms/administrator-help/configure-user-management/configure-advanced-system-attributes.html">관리 콘솔 도움말</a>에서 &quot;사용자 관리 구성 > 고급 시스템 속성 구성&quot;을 참조하십시오.

### HTTPS {#configuring-workbench-to-connect-over-HTTPS}에서 연결하도록 Workbench 구성

HTTPS를 통해 Workbench를 AEM Forms 서버에 연결하려면 공개 키를 발급한 CA(인증 기관)가 Workbench에서 신뢰할 수 있는 것으로 인식되는지 확인해야 합니다. 인증서가 신뢰할 수 있는 소스에서 온 것으로 인식되지 않으면 [Workbench_HOME]/workbench/jre/lib/security 디렉토리에 있는 캐시 파일을 업데이트해야 합니다.

>[!NOTE]
>
>[Workbench_] HOMEWorkbench를 설치한 디렉토리를 나타냅니다. 기본 위치는 C:\Program Files (x86)\Adobe Experience Manager forms Workbench입니다.

인증서에 지정된 이름을 사용하여 HTTPS에 연결해야 합니다. 이 이름은 일반적으로 정규화된 호스트 이름입니다.

**캐시 파일을 업데이트하려면**:
1. SSL(Secure Sockets Layer) 인증서 사본이 있는지 확인합니다. SSL 서버를 구성한 관리자에게 문의하거나 웹 브라우저를 사용하여 인증서를 내보냅니다.

   >[!NOTE]
   >
   >인증서를 내보내려면 웹 브라우저를 열고 관리 콘솔에 로그인하고, 브라우저에 인증서를 설치한 다음 인증서를 임시 저장소 위치(또는 [Workbench_HOME]/workbench/jre/lib/security 디렉토리)로 내보냅니다.

1. 인증서를 [Workbench_HOME]/workbench/jre/lib/security 디렉토리에 복사합니다.

1. 명령 프롬프트 창을 열고 [Workbench_HOME]/workbench/jre/bin으로 이동한 다음 명령을 입력합니다.
   `keytool -import -storepass changeit -file [Workbench_HOME]\workbench\jre\lib\security\ssl_cert_for_certname.cer -keystore [Workbench_HOME]\workbench\jre\lib\security\cacerts -alias example`
위치:
   * changeit는 캐시 키 저장소에 대한 기본 암호입니다.
   * certname은 1단계에서 선택한 인증서입니다.
   * 예제는 인증서에 대해 선택하는 별칭입니다. 이 값을 변경할 수 있습니다

1. 인증서를 신뢰하라는 메시지가 표시되면 예 를 입력하고 Enter 키를 누릅니다. 키 도구가 계속해서 [Workbench_HOME]/workbench/jre/lib/security 디렉토리에 캐시 파일을 가져옵니다.

1. 변경 사항을 적용하려면 Workbench를 닫았다가 다시 시작하십시오.

### 동적으로 생성된 템플릿에 대한 캐시 설정 구성 {#configuring-cache-settings-for-dynamically-generated-templates}

애플리케이션에서 XFA 컨텐츠를 자동으로 업데이트하여 즉시 고유한 템플릿을 생성하는 경우 캐시 작업의 다음 측면을 고려해야 합니다. 실제로 각 트랜잭션은 고유한 새로운 템플릿을 사용합니다.

Forms 생성기 또는 출력으로 특정 양식 서식 파일의 캐시 항목을 검색하거나 업데이트할 때 몇 가지 키 값을 사용하여 액세스할 특정 캐시 항목을 찾습니다.

* **템플릿 파일 이름**:캐시된 양식의 기본 고유 식별자로 사용되는 템플릿의 위치 및 파일 이름입니다.
* **타임스탬프**:템플릿 파일에 양식의 마지막 업데이트 시간을 확인하는 데 사용되는 타임스탬프가 포함되어 있습니다.
* **템플릿 UUID**:디자이너는 각 템플릿에 양식 및 해당 버전에 대한 고유 식별자(UUID)를 삽입합니다. 양식이 업데이트될 때마다 포함된 UUID가 업데이트됩니다. 예를 들어 XDP 템플릿에 다음 컨텐츠가 표시될 수 있습니다.

   `<?xml version="1.0" encoding="UTF-8"?>`
   `<?xfa generator="AdobeAEM formsDesignerES_V8.2" APIVersion="2.6.7185.0"?><xdp:xdp xmlns:xdp=http://ns.adobe.com/xdp/ timeStamp="2008-07-29T21:22:12Z" uuid="823e538f-ff6c-4961-b759-f7626978a223"><template xmlns="http://www.xfa.org/schema/xfa-template/2.6/">`

* **렌더링 옵션**:렌더링된 양식 캐시 내에서 캐시 컨텐츠는 각 고유한 렌더링 옵션 세트에 대해 별도로 저장됩니다.


Forms 서비스는 파일 이름 또는 저장소 위치를 참조하거나 또는 메모리의 XML 개체로 값별로 템플릿을 수신합니다.
* **참조에 의해 전달된 템플릿**:컨텐츠 루트와 양식 이름을 사용합니다. 이 방법을 사용하여 모든 요청에서 파일 이름이 다른 고유한 템플릿이 전달되면 디스크 캐시가 지속적으로 확장되어 다시 사용되지 않습니다. 이를 방지하려면 동일한 파일 이름으로 고유한 템플릿을 전달하여 모든 요청에 대해 동일한 캐시가 업데이트되도록 해야 합니다.
* **값으로 전달된 템플릿**:inDataDoc 매개 변수를 사용하여 데이터와 함께 전달된 템플릿 바이트를 사용합니다. 이 방법을 사용하여 UUID가 다른 고유한 템플릿을 전달하면 디스크 캐시가 지속적으로 확장되어 재사용되지 않습니다. 이를 방지하려면 UUID 속성을 모든 템플릿에서 제거하여 템플릿에 대한 캐시가 만들어지지 않도록 해야 합니다. 또는 null이 아닌 동일한 UUID를 전달하면 캐시 개체를 만들 수 있지만 각 요청마다 동일한 캐시가 업데이트되도록 합니다.

캐시가 지속적으로 늘어나지 않도록 하려면 새로운 AEM Forms API, renderHTMLForm2 및 renderPDFForm2를 사용하여 동적으로 생성된 템플릿을 렌더링하기 위해 다음 요소를 고려하십시오.

새 API를 사용할 때 템플릿은 문서 개체로 전달됩니다. 이 문서 개체는 패시베이션되었는지 여부에 따라 Forms 서비스에서 처리됩니다.

UUID 및 컨텐츠 루트가 캐시 키로 사용되는 패시화된 문서의 경우 다음 측면을 고려하십시오.
* UUID가 없는 패시화된 입력 템플릿에 대해 캐시가 생성되지 않습니다.
* 동일한 UUID 및 컨텐츠 루트가 있는 수동된 입력 템플릿이 두 개 이상 전달되면 동일한 캐시를 덮어씁니다.

파일 이름 및 컨텐츠 루트가 캐시 키로 사용되는 비패시테이션된 문서의 경우 다음 측면을 고려하십시오.
* 수동되지 않은 입력 템플릿의 경우 캐싱은 문서가 생성된 컨텐츠 루트와 파일 이름에 따라 달라집니다.
동일한 캐시는 동일한 컨텐츠 루트와 템플릿 파일 이름을 사용하는 요청에만 사용됩니다.
다음 우수 사례는 동적으로 생성된 템플릿을 Forms 서비스에 전달할 때 캐시가 지속적으로 증가하지 않도록 합니다.
   * 동적으로 생성된 모든 템플릿에서 UUID를 제거하거나 동일한 UUID를 전달합니다.
   * 템플릿 바이트 또는 디스크의 동일한 파일 이름에서 문서를 생성합니다.

### Workbench {#uninstalling-workbench} 제거

Campaign 컨트롤 패널에서 프로그램 추가 또는 제거 기능을 사용하여 설치 해제 기능을 시작합니다. Workbench 및 Designer 응용 프로그램에는 별도의 제거 프로그램이 있습니다.

## AEM Forms XDC 편집기 구성{#configuring-aem-forms-xdc-editor}

네트워크 프린터 관리자는 XDC 편집기를 사용하여 XML Forms XDC(Architecture Device Configuration) 파일을 만들고 수정할 수 있습니다. XDC 파일은 프린터 언어 또는 용지 크기와 트레이 위치 간의 상관 관계 등과 같은 프린터 기능을 설명합니다.

네트워크 프린터 관리자가 XDC 편집기를 사용하기 전에 샘플 XDC 파일의 위치를 변경하고 XDC 편집기를 사용하여 장치 프로필 만들기를 참조하십시오.

**샘플 XDC 파일을 가져오려면 다음을 수행하십시오**.
1. AEM Forms 서버의 [AEM Forms 루트]\sdk\samples\Output\IVS에서 XDC 폴더를 찾습니다.
1. 이 폴더의 컨텐츠를 Workbench 또는 Eclipse 시스템에서 액세스할 수 있는 디렉토리에 복사합니다.

**XDC 편집기 도움말을 확인하려면 다음을 수행하십시오**.
1. AEM Forms 설명서 웹 사이트로 이동합니다.
1. **개발** 탭을 클릭하고 XDC 편집기를 사용하여 장치 프로필 만들기로 이동합니다. xdc_editor_help_web.zip 파일을 다운로드하고 Readme 파일에 제공된 지침에 따라 도움말 파일을 설치합니다.
