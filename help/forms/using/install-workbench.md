---
title: 설치 워크벤치
seo-title: 설치 워크벤치
description: 설치 워크벤치.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '2246'
ht-degree: 0%

---


# 설치 워크벤치 {#install-workbench}

이 문서에서는 AEM Forms 워크벤치 설치 및 구성에 대한 지침을 제공합니다. 설치 프로그램은 Forms Designer도 설치합니다.

## 누가 이 문서를 읽어야 합니까?{#who-should-read-this-doc}

이 문서는 워크벤치 설치, 구성, 관리 또는 배포를 담당하는 관리자 또는 개발자를 위한 것입니다. 업그레이드된 AEM Forms 프로세스를 지원하도록 시스템을 구성하는 데 필요한 정보도 포함되어 있습니다. 제공된 정보는 이 문서를 읽는 사람이 Microsoft® Windows® 운영 체제에 익숙하다는 가정을 기반으로 합니다.

## 추가 정보 {#additional-information}

이 표의 리소스는 AEM Forms에 대해 자세히 알아보고 시작하는 데 도움이 됩니다.
<table>
 <tbody>
  <tr>
   <td><p><strong>자세한 내용은</strong></p> </td>
   <td><p><strong>자세한 내용은</strong></p> </td>
  </tr>
  <tr>
   <td><p>워크벤치를 위한 절차 정보</p> </td>
   <td><p><a href="https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf">워크벤치 도움말</a><br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>AEM Forms에 대한 일반 정보 및 다른 Adobe 제품과 통합하는 방법</p> </td>
   <td><p><a href="http://adobe.com/go/learn_aemforms_introduction_65">AEM Forms 개요</a><br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>AEM Forms에 사용할 수 있는 모든 설명서</p> </td>
   <td><p><a href="http://adobe.com/go/learn_aemforms_introduction_65">AEM Forms 설명서</a><br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>이 제품 버전에 대한 패치 업데이트, 기술 정보 및 추가 정보</p> </td>
   <td><p>Adobe Enterprise 지원 문의</a><br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Flex 작업 영역은 AEM Forms에서 더 이상 사용되지 않습니다. AEM Forms 릴리스에서 사용할 수 있습니다.

## {#before-you-install} 설치 전

### 워크벤치 설치 개요 {#workbench-installation-overview}

Workbench는 개발자와 양식 작성자가 자동화된 비즈니스 프로세스와 양식을 만드는 데 사용하는 통합 개발 환경(IDE)입니다. 또한 프로세스와 양식에서 사용하는 리소스 및 서비스를 관리하는 데 사용됩니다.

다음 그림은 다음과 같은 워크벤치 설치를 보여 줍니다.
* 워크벤치를 사용한 프로세스 디자인
* 디자이너를 사용한 양식 디자인

>[!NOTE]
>
>AEM Forms 서버에는 별도의 설치 프로그램이 필요합니다. 자세한 내용은 JEE 설치 설명서에 대한 AEM Forms을 참조하십시오.

![default-render-form](assets/installing-workbench.png)

## 시스템 사전 요구 사항 {#system-prerequisites}

이 섹션에서는 하드웨어 및 소프트웨어 요구 사항과 지원되는 플랫폼에 대해 간략하게 설명합니다.

### 최소 하드웨어 및 소프트웨어 요구 사항 {#minimum-hardware-software-requirements}

**Workbench**
최소 요구 사항은 다음과 같습니다.설치를 위한 디스크 공간:
* 워크벤치의 경우 680MB만 해당합니다.
* Workbench, Designer 및 samples 어셈블리의 전체 설치를 위한 단일 드라이브의 2.15GB입니다.
* 임시 설치 디렉토리의 경우 400MB - 사용자 \temp 디렉토리의 경우 200MB, Windows 임시 디렉토리의 경우 200MB.

>[!NOTE]
>
>이러한 모든 위치가 단일 드라이브에 있을 경우 설치 중에 1.5GB의 공간을 사용할 수 있어야 합니다. 설치가 완료되면 임시 디렉토리에 복사된 파일이 삭제됩니다.

* 하드웨어 요구 사항:Intel® Pentium® 4 또는 AMD 동급 프로세서, 1GHz 프로세서.
* JRE(Java™ Runtime Environment) 7.0 업데이트 51 이상 버전이 7.0으로 업데이트됩니다.
* 16비트 컬러 이상의 최소 1024 X 768픽셀 이상의 모니터 해상도를 제공합니다.
* AEM Forms 서버에 대한 TCP/IPv4 또는 TCP/IPv6 네트워크 연결
* Visual C++ 재배포 가능 런타임 패키지 2012 32비트를 설치합니다.
* Visual C++ 재배포 가능 런타임 패키지 2013 32비트를 설치합니다.

>[!NOTE]
>
>워크벤치를 설치하려면 관리 권한이 있어야 합니다. 관리자가 아닌 계정을 사용하여 설치하는 경우 설치 관리자에서 해당 계정에 대한 자격 증명을 입력하라는 메시지를 표시합니다.

### 지원되는 플랫폼 {#supported-platforms}

[AEM Forms 지원 플랫폼](http://adobe.com/go/learn_aemforms_supportedplatforms_65)에서 워크벤치에 대해 지원되는 전체 플랫폼 목록을 참조하십시오.

## 디자이너 설치 고려 사항 {#designer-installation-considerations}

기본적으로 Workbench 설치에는 해당 영어 전용 버전의 Designer가 포함되어 있습니다. Workbench 설치 응용 프로그램이 컴퓨터에 있는 기존 버전의 Designer를 감지하는 경우 설치가 종료될 수 있으며, 계속하려면 현재 버전의 Designer를 제거해야 합니다.
아래 표에는 Workbench를 설치할 때 수행해야 하는 모든 작업 및 발생할 수 있는 Designer 설치 시나리오의 전체 목록이 나와 있습니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>현재 설치된 Designer 버전</strong></p> </td>
   <td><p><strong>필요한 작업</strong></p> </td>
  </tr>
  <tr>
   <td><p>Acrobat Pro 또는 Acrobat Pro Extended(Designer 포함)</p> </td>
   <td><p>없음.<br /> 
워크벤치 설치는 Acrobat Pro 또는 Acrobat Pro Extended와 함께 설치된 컴퓨터에서 Designer 인스턴스를 감지합니다.<br />
Workbench 6.4용 Designer 6.4.x와 Workbench 6.5용 Designer 6.5.0.x와 같이 서로 다른 버전의 Designer가 동일한 시스템에서 사용될 수 있습니다. Acrobat 10 Pro 또는 Acrobat 10 Pro Extended 등과 함께 설치된 Designer 버전을 제거할 필요는 없습니다.
<br /></p> </td>
  </tr>
  <tr>
   <td><p>디자이너(독립 실행형)</p> </td>
   <td><p>없음. <br />Workbench에 포함된 Designer 버전은 영어로만 제공됩니다. <br />워크벤치 설치 프로그램은 새 버전의 Designer를 다시 설치하지 않습니다. 대신 Workbench 설치 관리자에 번들로 포함된 업데이트된 버전이 패치됩니다. 또한 워크벤치 내에서 지역화된 버전의 Designer를 사용할 수 있습니다.<br /> </p> </td>
  </tr>
 </tbody>
</table>

### Windows 10에서 디자이너(독립 실행형)를 제거하려면 {#uninstall-designer-standalone-windows10}

1. **Campaign 컨트롤 패널 > 프로그램 > 프로그램 및 기능**&#x200B;으로 이동합니다.
1. 현재 설치된 프로그램 목록에서 **Adobe 디자이너**&#x200B;를 선택합니다.
1. **제거**&#x200B;를 클릭한 다음 **예**&#x200B;를 클릭합니다.

## Workbench {#installing-workbench} 설치

이 장에서는 워크벤치 설치 방법에 대해 설명합니다.

### 워크벤치 {#installing-and-running-workbench} 설치 및 실행

워크벤치를 설치하기 전에 환경에 워크벤치를 실행하는 데 필요한 소프트웨어와 하드웨어가 포함되어 있는지 확인해야 합니다(섹션 참조:**설치 전**).

**워크벤치를 설치 및 실행하려면:**

1. 다음 작업 중 하나를 수행합니다.
   * 설치 미디어의 \workbench 디렉토리로 이동하고 run_windows_installer.bat 파일을 두 번 클릭합니다.
   * 워크벤치를 다운로드하여 파일 시스템에 압축을 해제합니다. 다운로드된 후 \workbench 디렉토리로 이동하고 run_windows_installer.bat 파일을 두 번 클릭합니다.

   >[!IMPORTANT]
   >
   >워크벤치 설치 프로그램은 로컬 드라이브에서만 실행됩니다. 원격 사이트에서 실행할 수 없습니다.

   >[!NOTE]
   >
   >&quot;Java 가상 컴퓨터를 만들 수 없습니다.&quot;라는 오류가 발생하면 값 -Xmx512M의 _JAVA_OPTIONS라는 환경 변수를 만들고 설치 관리자를 실행합니다.

1. [소개] 화면에서 [다음]을 클릭합니다.
1. 제품 라이센스 계약을 읽고, 동의함을 선택한 후, 다음을 클릭합니다.
1. (선택 사항) 이 도구를 사용하여 양식을 만들고 수정해야 하는 경우 Adobe 디자이너 설치를 선택합니다.

   >[!NOTE]
   >
   >Acrobat 10과 함께 설치된 Designer는 이 옵션을 선택 해제한 상태로 그대로 계속 사용할 수 있습니다.

1. 목록에 있는 기본 디렉토리를 그대로 사용하거나   워크벤치를 설치할 디렉토리를 선택하고 [다음]을 클릭합니다.

   >[!NOTE]
   >
   >설치 디렉토리 경로는 #(파운드) 및 $(달러) 문자를 포함할 수 없습니다.

1. 사전 설치 요약을 검토하고 설치를 클릭합니다. 설치 프로그램에 설치 진행 상태가 표시됩니다.
1. 설치 요약을 검토합니다. AEM Forms 워크벤치 시작을 선택하여 워크벤치를 실행하고 다음을 클릭합니다.
1. 릴리스 노트를 검토하고 완료를 클릭합니다.
1. 이제 컴퓨터에 다음 항목이 설치됩니다.
   * **워크벤치**:시작 메뉴에서 워크벤치를 실행하려면 바로 가기 폴더를 저장하도록 선택한 경우 모든 프로그램 > AEM Forms > 워크벤치를 선택합니다. 자세한 내용은   <a href="https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf">워크벤치 사용</a> 설명서를 참조하십시오.
   * **디자이너**:Workbench 내에서 Designer에 액세스할 수 있습니다. 자세한 내용은 <a href="https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/using-designer.pdf">디자이너 도움말</a>의 시작하기 항목을 참조하십시오.
   * **AEM Forms SDK**:SDK 사용에 대한 자세한 내용은 AEM Forms <a href="http://www.adobe.com/go/learn_aemforms_programming_65">를 사용한 프로그래밍을 참조하십시오</a>.

## 프로세스 {#upgrading-processes} 업그레이드

업그레이드 마법사를 사용하여 JEE 기반의 AEM Forms 프로세스를 AEM Forms 애플리케이션으로 업그레이드할 수 있습니다. 자세한 내용은 워크벤치 도움말의 기존 객체 설명서 업그레이드를 참조하십시오.

### 서버 {#configuring-and-logging-server} 구성 및 로그인

Workbench를 사용하려면 일반적으로 별도의 컴퓨터에서 실행되는 AEM Forms 인스턴스가 있어야 합니다. AEM Forms에 로그인하려면 사용자 이름 및 암호와 서버 위치에 대한 세부 정보가 있어야 합니다.

>[!NOTE]
>
>EMC Documentum 또는 IBM FileNet 저장소 공급자를 사용하도록 AEM Forms을 구성한 경우 AEM Forms 관리 콘솔에서 기본값으로 구성된 저장소 이외의 저장소에 로그인하려면 사용자 이름을 username@Repository으로 입력합니다.

### 시간 초과 설정 구성 {#configuring-timeout-settings}

기본적으로 Workbench는 활동이나 비활동과는 관계 없이 2시간 후 시간을 초과합니다. 시간 초과 설정을 편집하려면 <a href="https://docs.adobe.com/content/help/en/experience-manager-65/forms/administrator-help/configure-user-management/configure-advanced-system-attributes.html">관리 콘솔 도움말</a>의 &quot;사용자 관리 구성 > 고급 시스템 특성 구성&quot;을 참조하십시오.

### HTTPS {#configuring-workbench-to-connect-over-HTTPS}를 통해 연결하도록 워크벤치 구성

HTTPS를 통해 AEM Forms 서버에 워크벤치를 연결하려면 공개 키를 발행한 인증 기관(CA)이 워크벤치에서 신뢰하는 것으로 인식되어야 합니다. 인증서가 신뢰할 수 있는 소스에서 온 것으로 인식되지 않으면 [Workbench_HOME]/workbench/jre/lib/security 디렉토리에 있는 cacert 파일을 업데이트해야 합니다.

>[!NOTE]
>
>[Workbench_] HOME워크벤치를 설치한 디렉토리를 나타냅니다. 기본 위치는 C:\Program Files (x86)\Adobe Experience Manager forms Workbench입니다.

인증서에 지정된 이름을 사용하여 HTTPS에 연결해야 합니다. 이 이름은 일반적으로 정규화된 호스트 이름입니다.

**캐시 파일을 업데이트하려면**:
1. SSL(Secure Sockets Layer) 인증서 복사본이 있는지 확인합니다. SSL 서버를 구성한 관리자에게 문의하거나 웹 브라우저를 사용하여 인증서를 내보냅니다.

   >[!NOTE]
   >
   >인증서를 내보내려면 웹 브라우저를 열고 관리 콘솔에 로그인하고, 브라우저에서 인증서를 설치한 다음, 인증서를 브라우저에서 임시 저장 위치로 내보내십시오(또는 [Workbench_HOME]/workbench/jre/lib/security 디렉토리).

1. 인증서를 [Workbench_HOME]/workbench/jre/lib/security 디렉토리로 복사합니다.

1. 명령 프롬프트 창을 열고 [Workbench_HOME]/workbench/jre/bin으로 이동한 다음 다음 다음 명령을 입력합니다.
   `keytool -import -storepass changeit -file [Workbench_HOME]\workbench\jre\lib\security\ssl_cert_for_certname.cer -keystore [Workbench_HOME]\workbench\jre\lib\security\cacerts -alias example`
위치:
   * changes는 cacerts keystore에 대한 기본 암호입니다.
   * certname은 1단계에서 선택한 인증서입니다.
   * 예를 들어 인증서에 대해 선택하는 별칭이 있습니다. 이 값은 변경할 수 있습니다.

1. 인증서를 신뢰하라는 메시지가 표시되면 예를 입력하고 Enter 키를 누릅니다. 이 keytool은 캐시 파일을 [Workbench_HOME]/workbench/jre/lib/security 디렉토리로 가져오기 시작합니다.

1. 변경 사항을 적용하려면 워크벤치를 닫고 다시 시작하십시오.

### 동적으로 생성된 템플릿 {#configuring-cache-settings-for-dynamically-generated-templates}에 대한 캐시 설정 구성

응용 프로그램에서 XFA 컨텐츠를 자동으로 업데이트하여 고유한 템플릿을 즉석에서 생성하는 경우 캐시 작업의 다음 측면을 고려해야 합니다. 실제로 각 트랜잭션은 고유한 새 템플릿을 사용합니다.

양식 생성기 또는 출력으로 특정 양식 템플릿의 캐시에 있는 항목을 검색하거나 업데이트할 때 몇 가지 키 값을 사용하여 액세스할 특정 캐시 항목을 찾습니다.

* **템플릿 파일 이름**:캐시된 양식의 기본 고유 식별자로 사용되는 템플릿의 위치 및 파일 이름입니다.
* **타임스탬프**:템플릿 파일에는 양식의 마지막 업데이트 시간을 결정하는 데 사용되는 타임스탬프가 포함되어 있습니다.
* **템플릿 UUID**:디자이너는 각 템플릿에 양식 및 해당 버전에 대한 고유 식별자(UUID)를 삽입합니다. 양식이 업데이트될 때마다 포함된 UUID가 업데이트됩니다. 예를 들어 XDP 템플릿에 다음 컨텐츠가 표시될 수 있습니다.

   `<?xml version="1.0" encoding="UTF-8"?>`
   `<?xfa generator="AdobeAEM formsDesignerES_V8.2" APIVersion="2.6.7185.0"?><xdp:xdp xmlns:xdp=http://ns.adobe.com/xdp/ timeStamp="2008-07-29T21:22:12Z" uuid="823e538f-ff6c-4961-b759-f7626978a223"><template xmlns="http://www.xfa.org/schema/xfa-template/2.6/">`

* **렌더링 옵션**:렌더링된 양식 캐시 내에서 캐시 내용은 각 고유 렌더링 옵션 집합에 대해 별도로 저장됩니다.


Forms 서비스는 파일 이름 또는 저장소 위치에 대한 참조나 메모리에 있는 XML 객체로 값별로 템플릿을 수신합니다.
* **참조로 전달된 템플릿**:컨텐츠 루트와 양식 이름을 사용합니다. 이 방법을 사용하여 파일 이름이 다른 고유한 템플릿이 모든 요청에 전달되면 디스크 캐시는 끝없이 확장되어 다시 사용되지 않습니다. 이를 방지하려면 고유한 템플릿을 동일한 파일 이름으로 전달하여 모든 요청에 대해 동일한 캐시를 업데이트해야 합니다.
* **값으로 전달된 템플릿**:inDataDoc 매개 변수를 사용하여 데이터와 함께 전달된 템플릿 바이트를 사용합니다. 이 방법을 사용하여 서로 다른 UUID의 고유한 템플릿이 전달되면 디스크 캐시는 끝없이 확장되어 다시 사용할 수 없습니다. 이를 방지하려면 UUID 속성을 모든 템플릿에서 제거하여 템플릿에 대한 캐시가 만들어지지 않도록 해야 합니다. 또는 null이 아닌 동일한 UUID를 전달하면 캐시 객체를 만들 수 있지만 각 요청에 대해 동일한 캐시가 업데이트되도록 할 수 있습니다.

캐시가 끝없이 확장되지 않도록 하려면 renderHTMLForm2 및 renderPDFForm2를 사용하여 동적으로 생성된 템플릿을 렌더링하는 데 다음 요인을 고려하십시오.

새 API를 사용할 때 템플릿은 문서 객체로 전달되며, 이 객체는 수동이 이루어지는지 여부를 기준으로 Forms 서비스에서 처리됩니다.

UUID 및 컨텐츠 루트가 캐시 키로 사용되는 수동적인 문서의 경우 다음 측면을 고려하십시오.
* UUID가 없는 수동적인 입력 템플릿에 대해 캐시가 생성되지 않습니다.
* 동일한 UUID 및 컨텐츠 루트를 가진 두 개 이상의 수동적인 입력 템플릿이 전달되면 동일한 캐시를 덮어씁니다.

파일 이름 및 컨텐츠 루트가 캐시 키로 사용되는 비수동적인 문서의 경우 다음 측면을 고려하십시오.
* 수동적인 입력 템플릿의 경우 캐싱은 문서가 생성된 컨텐츠 루트 및 파일 이름에 따라 달라집니다.
동일한 캐시는 동일한 컨텐츠 루트 및 템플릿 파일 이름을 가진 요청에만 사용됩니다.
다음 우수 사례는 동적으로 생성된 템플릿이 Forms 서비스로 전달될 때 캐시가 지속적으로 증가하지 않도록 합니다.
   * UUID를 분리하거나 동적으로 생성된 모든 템플릿에 동일한 UUID를 전달합니다.
   * 템플릿 바이트 또는 디스크의 동일한 파일 이름에서 문서를 생성합니다.

### 워크벤치 제거 중 {#uninstalling-workbench}

Campaign 컨트롤 패널의 프로그램 추가/제거 기능을 사용하여 제거 프로그램을 시작합니다. Workbench 및 Designer 응용 프로그램에는 별도의 제거 프로그램이 있습니다.

## AEM Forms XDC 편집기 구성 {#configuring-aem-forms-xdc-editor}

네트워크 프린터 관리자는 XDC 편집기를 사용하여 XDC(XML Forms Architecture Device Configuration) 파일을 만들고 수정할 수 있습니다. XDC 파일은 프린터 언어 또는 용지 크기와 트레이 위치 간의 상관 관계와 같은 프린터 기능을 설명합니다.

네트워크 프린터 관리자가 XDC 편집기를 사용하기 전에 샘플 XDC 파일 위치를 지정하고 XDC 편집기를 사용하여 장치 프로파일 만들기를 참조하십시오.

**샘플 XDC 파일을 가져오려면 다음을 수행하십시오**.
1. AEM Forms 서버의 [AEM Forms 루트]\sdk\samples\Output\IVS폴더에서 XDC 폴더를 찾습니다.
1. 워크벤치 또는 Eclipse 시스템에서 액세스할 수 있는 디렉토리로 이 폴더의 컨텐츠를 복사합니다.

**XDC 편집기 도움말을 얻으려면 다음을 수행하십시오**.
1. AEM Forms 설명서 웹 사이트로 이동합니다.
1. **현상** 탭을 클릭하고 XDC 편집기를 사용하여 장치 프로파일 만들기로 이동합니다. xdc_editor_help_web.zip 파일을 다운로드하고 Readme 파일의 지침에 따라 도움말 파일을 설치합니다.

