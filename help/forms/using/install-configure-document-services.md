---
title: 문서 서비스 설치 및 구성
seo-title: Installing and configuring document services
description: AEM Forms 문서 서비스를 설치하여 PDF 문서를 작성, 조합, 배포, 아카이빙하고 디지털 서명을 추가하여 문서에 대한 액세스를 제한하고 Barcoded Forms을 디코딩할 수 있습니다.
seo-description: Install AEM Forms document services to create, assemble, distribute, archive PDF documents, add digital signatures to limit access to documents, and decode barcoded forms.
uuid: 908806a9-b0d4-42d3-9fe4-3eae44cf4326
topic-tags: installing
discoiquuid: b53eae8c-16ba-47e7-9421-7c33e141d268
role: Admin
exl-id: 5d48e987-16c2-434b-8039-c82181d2e028
source-git-commit: 26fbf8629715c983ccae9dcdee1defb279849107
workflow-type: tm+mt
source-wordcount: '5461'
ht-degree: 2%

---

# 문서 서비스 설치 및 구성 {#installing-and-configuring-document-services}

AEM Forms은 다양한 문서 수준 작업을 수행하기 위한 일련의 OSGi 서비스를 제공합니다. 예를 들어, PDF 문서를 작성, 조합, 배포 및 아카이빙하고, 문서에 대한 액세스를 제한하는 디지털 서명을 추가하고, Barcoded Forms을 디코딩하는 서비스를 제공합니다. 이러한 서비스는 AEM Forms 추가 기능 패키지에 포함되어 있습니다. 이러한 서비스를 문서 서비스라고 합니다. 사용 가능한 문서 서비스 및 주요 기능 목록은 다음과 같습니다.

* **어셈블러 서비스:** PDF 및 XDP 문서를 결합, 재정렬 및 확장하고 PDF 문서에 대한 정보를 얻을 수 있습니다. 또한 PDF 문서를 PDF/A 표준으로 변환 및 확인하고, PDF forms, XML 양식 및 PDF forms을 PDF/A-1b, PDF/A-2b 및 PDFA/A-3b로 변환하는 데에도 도움이 됩니다. 자세한 내용은 [어셈블러 서비스](/help/forms/using/assembler-service.md).

* **ConvertPDF 서비스:** PDF 문서를 PostScript 또는 이미지 파일(JPEG, JPEG 2000, PNG 및 TIFF)으로 변환할 수 있습니다. 자세한 내용은 [ConvertPDF 서비스](/help/forms/using/using-convertpdf-service.md).

* **Barcoded Forms 서비스:** 바코드의 전자 이미지에서 데이터를 추출할 수 있습니다. 이 서비스는 하나 이상의 바코드를 입력으로 포함하는 TIFF 및 PDF 파일을 승인하고 바코드 데이터를 추출합니다. 자세한 내용은 [Barcoded Forms 서비스](/help/forms/using/using-barcoded-forms-service.md).

* **DocAssurance 서비스:** 문서를 암호화 및 해독 하고, 추가 사용 권한으로 Adobe Reader의 기능을 확장하고, 문서에 디지털 서명을 추가할 수 있습니다. Doc Assurance 서비스에는 다음 세 가지 서비스가 포함됩니다. 서명, 암호화 및 reader 확장 자세한 내용은 [DocAssurance 서비스](/help/forms/using/overview-aem-document-services.md).

* **암호화 서비스:** 문서를 암호화하고 해독할 수 있습니다. 문서가 암호화되면 문서의 내용을 읽을 수 없게 됩니다. 권한이 있는 사용자는 문서를 해독하여 해당 내용에 대한 액세스 권한을 얻을 수 있습니다. 자세한 내용은 [암호화 서비스](/help/forms/using/overview-aem-document-services.md#encryption-service).

* **Forms 서비스:** 일반적으로 Forms Designer에서 만든 양식을 유효성 검사, 처리, 변환 및 전달하는 대화형 데이터 캡처 클라이언트 응용 프로그램을 만들 수 있습니다. Forms 서비스는 사용자가 개발하는 모든 양식 디자인을 PDF 문서로 렌더링합니다. 자세한 내용은 [Forms 서비스](/help/forms/using/forms-service.md).

* **출력 서비스:** PDF, 레이저 프린터 형식 및 레이블 프린터 형식을 포함하여 다양한 형식으로 문서를 만들 수 있습니다. 레이저 프린터 형식은 PostScript 및 PCL(Printer Control Language)입니다. 자세한 내용은 [출력 서비스](/help/forms/using/output-service.md).

* **PDF 생성기 서비스:** PDF 생성기 서비스는 기본 파일 형식을 PDF으로 변환하는 API를 제공합니다. 또한 PDF을 다른 파일 형식으로 변환하고 PDF 문서의 크기를 최적화합니다. 자세한 내용은 [PDF 생성기 서비스](aem-document-services-programmatically.md#pdfgeneratorservice).

* **Reader 확장 서비스:** 사용 권한을 추가하여 Adobe Reader의 기능을 확장하여 대화형 PDF 문서를 쉽게 공유할 수 있습니다. 이 서비스는 Adobe Reader을 사용하여 PDF 문서를 열 때 사용할 수 없는 기능(문서에 주석 추가, 양식 채우기, 문서 저장 등)을 활성화합니다. 자세한 내용은 [Reader 확장 서비스](/help/forms/using/overview-aem-document-services.md#reader-extension-service).

* **서명 서비스:** AEM 서버에서 디지털 서명 및 문서를 사용하여 작업할 수 있습니다. 예를 들어 서명 서비스는 일반적으로 다음 상황에서 사용됩니다.

   * AEM 서버는 Acrobat 또는 Adobe Reader을 사용하여 열기 위해 사용자에게 전송하기 전에 양식을 인증합니다.
   * AEM 서버는 Acrobat 또는 Adobe Reader을 사용하여 양식에 추가된 서명을 확인합니다.
   * AEM 서버는 공증인을 대신하여 양식에 서명한다.

   서명 서비스는 신뢰 저장소에 저장된 인증서 및 자격 증명에 액세스합니다. 자세한 내용은 [서명 서비스](/help/forms/using/aem-document-services-programmatically.md).

AEM Forms은 강력한 엔터프라이즈급 플랫폼이며 문서 서비스는 AEM Forms의 기능 중 하나뿐입니다. 전체 기능 목록에 대해서는 다음을 참조하십시오 [AEM Forms 소개](/help/forms/using/introduction-aem-forms.md).

## 배포 토폴로지 {#deployment-topology}

AEM Forms 추가 기능 패키지는 AEM에 배포된 애플리케이션입니다. 일반적으로 AEM Forms 문서 서비스를 실행하려면 하나의 AEM 인스턴스(작성자 또는 게시)만 필요합니다. AEM Forms 문서 서비스를 실행하려면 다음 토폴로지를 사용하는 것이 좋습니다. 토폴로지에 대한 자세한 내용은 [AEM Forms을 위한 아키텍처 및 배포 토폴로지](/help/forms/using/aem-forms-architecture-deployment.md).

![AEM Forms을 위한 아키텍처 및 배포 토폴로지](do-not-localize/document-services.png)

>[!NOTE]
>
>AEM Forms을 통해 단일 서버에서 모든 기능을 설정 및 실행할 수 있지만 용량 계획, 로드 밸런싱 및 프로덕션 환경의 특정 기능에 대한 전용 서버를 설정해야 합니다. 예를 들어 PDF 생성기 서비스를 사용하여 하루에 수천 개의 페이지를 변환하고 여러 적응형 양식을 사용하여 데이터를 캡처하는 환경의 경우 PDF 생성기 서비스 및 적응형 양식 기능에 대해 별도의 AEM Forms 서버를 설정합니다. 최적의 성능을 제공하고 서로 독립적으로 서버를 확장할 수 있습니다.

## 시스템 요구 사항 {#system-requirements}

AEM Forms 문서 서비스 설치 및 구성을 시작하기 전에 다음을 확인하십시오.

* 하드웨어 및 소프트웨어 인프라가 제대로 구축되어 있습니다. 지원되는 하드웨어 및 소프트웨어에 대한 자세한 내용은 [기술 요구 사항](/help/sites-deploying/technical-requirements.md).

* AEM 인스턴스의 설치 경로에 공백이 들어 있지 않습니다.
* AEM 인스턴스가 실행 중입니다. AEM 용어에서 &quot;인스턴스&quot;는 작성자 또는 게시 모드에서 서버에서 실행되는 AEM의 사본입니다. 일반적으로 AEM Forms 문서 서비스를 실행하려면 하나의 AEM 인스턴스(작성자 또는 게시)만 필요합니다.

   * **작성자**: 컨텐츠를 작성, 업로드 및 편집하고 웹 사이트를 관리하는 데 사용되는 AEM 인스턴스입니다. 컨텐츠가 라이브로 전환될 준비가 되면 게시 인스턴스에 복제됩니다.
   * **게시**: 인터넷 또는 내부 네트워크를 통해 대중에게 게시된 컨텐츠를 제공하는 AEM 인스턴스입니다.

* 메모리 요구 사항이 충족되었습니다. AEM Forms 추가 기능 패키지에는 다음이 필요합니다.

   * Microsoft® Windows 기반 설치를 위한 15GB의 임시 공간.
   * UNIX 기반 설치를 위한 6GB의 임시 공간.

* Microsoft® Windows 및 Linux®에서 PDF 생성기에서 변환을 수행하는 데 필요한 클라이언트 소프트웨어가 설치됩니다.

   * **Microsoft® Windows**: 설치 [Microsoft® Office](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p) 또는 [Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator)
   * **Linux®**: 설치 [Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p)

>[!NOTE]
>
>* Microsoft® Windows에서 PDF 생성기는 WebKit, Acrobat WebCapture 및 PhantomJS 전환 경로를 지원하여 HTML 파일을 PDF 문서로 변환합니다.
>* UNIX 기반 운영 체제에서 PDF 생성기는 WebKit 및 PhantomJS 변환 경로를 지원하여 HTML 파일을 PDF 문서로 변환합니다.
>


### UNIX 기반 운영 체제에 대한 추가 요구 사항 {#extrarequirements}

UNIX 기반 운영 체제를 사용하는 경우 각 운영 체제의 설치 미디어에서 다음 패키지를 설치합니다.

<table>
 <tbody>
  <tr>
   <td>
    <ul>
     <li>expand</li>
    </ul> </td>
   <td>
    <ul>
     <li>libxcb</li>
    </ul> </td>
   <td>
    <ul>
     <li>freetype</li>
    </ul> </td>
   <td>
    <ul>
     <li>libXau</li>
    </ul> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li>libSM</li>
    </ul> </td>
   <td>
    <ul>
     <li>zlib</li>
    </ul> </td>
   <td>
    <ul>
     <li>libICE</li>
    </ul> </td>
   <td>
    <ul>
     <li>libuuid</li>
    </ul> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li>글라이치</li>
    </ul> </td>
   <td>
    <ul>
     <li>libXext</li>
    </ul> </td>
   <td>
    <ul>
     <li>nss-softokn-freebl</li>
    </ul> </td>
   <td>
    <ul>
     <li>fontconfig</li>
    </ul> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li>libX11</li>
    </ul> </td>
   <td>
    <ul>
     <li>libXrender</li>
    </ul> </td>
   <td>
    <ul>
     <li>libXrandr</li>
    </ul> </td>
   <td>
    <ul>
     <li>libXinerama</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

* **(PDF 생성기만 해당)**) 32비트 버전의 libcurl, libcrypto 및 libssl 라이브러리를 설치하고 아래 symlink를 만듭니다. symlink는 각 라이브러리의 최신 버전을 가리킵니다.

   * /usr/lib/libcurl.so
   * /usr/lib/libcrypto.so
   * /usr/lib/libssl.so

* **(PDF 생성기만)** PDF 생성기 서비스는 HTML 파일을 PDF 문서로 변환하기 위한 WebKit 및 PhantomJS 경로를 지원합니다. PhantomJS 경로에 대해 전환을 사용하려면 아래에 나열된 64비트 라이브러리를 설치합니다. 일반적으로 이러한 라이브러리는 이미 설치되어 있습니다. 라이브러리가 누락된 경우 수동으로 설치합니다.

   * linux-gate.so.1
   * libz.so.1
   * libfontconfig.so.1
   * libfreetype.so.6
   * libdl.so.2
   * librt.so.1
   * libpthread.so.0
   * libstdc++.so.6
   * libm.so.6
   * libgcc_s.so.1
   * libc.so.6
   * ld-linux.so.2
   * libexpat.so.1

## 사전 설치 구성 {#preinstallationconfigurations}

설치 전 구성 섹션에 나열된 구성은 PDF 생성기 서비스에만 적용할 수 있습니다. PDF 생성기 서비스를 구성하지 않으면 설치 전 구성 섹션을 건너뛸 수 있습니다.

### Adobe Acrobat 및 타사 애플리케이션 설치 {#install-adobe-acrobat-and-third-party-applications}

PDF 생성기 서비스를 사용하여 Microsoft® Word, Microsoft® Excel, Microsoft® PowerPoint, OpenOffice, WordPerfect X7 및 Adobe Acrobat과 같은 기본 파일 형식을 문서에서 PDF 문서로 변환하려면 이러한 애플리케이션이 AEM Forms 서버에 설치되어 있는지 확인하십시오.

>[!NOTE]
>
>* AEM Forms 서버가 오프라인 또는 보안 환경에 있고 Adobe Acrobat을 활성화하는 데 인터넷을 사용할 수 없는 경우 다음을 참조하십시오 [오프라인 활성화](https://exception.licenses.adobe.com/aoes/aoes/v1/t1?locale=en) 를 참조하십시오.
>* Adobe Acrobat, Microsoft® Word, Excel 및 Powerpoint는 Microsoft® Windows에서만 사용할 수 있습니다. UNIX 기반 운영 체제를 사용하는 경우 OpenOffice를 설치하여 리치 텍스트 파일과 지원되는 Microsoft® Office 파일을 PDF 문서로 변환합니다.
>* PDF 생성기 서비스를 사용하도록 구성된 모든 사용자에 대해 Adobe Acrobat 및 타사 소프트웨어를 설치한 후 표시되는 모든 대화 상자를 닫습니다.
>* 설치된 모든 소프트웨어를 한 번 이상 시작합니다. PDF 생성기 서비스를 사용하도록 구성된 모든 사용자의 대화 상자를 닫습니다.
>* [Adobe Acrobat 일련 번호의 만료 날짜를 확인합니다](https://helpx.adobe.com/enterprise/kb/volume-license-expiration-check.html) 라이센스를 업데이트하거나 [일련 번호 마이그레이션](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number) 만료 날짜를 기준으로 합니다.


Acrobat을 설치한 후 Microsoft® Word를 엽니다. 설정 **Acrobat** 탭, **PDF 만들기** 컴퓨터에서 사용할 수 있는 .doc 또는 .docx 파일을 PDF 문서로 변환합니다. 전환이 성공적으로 수행되면 AEM Forms에서는 PDF 생성기 서비스와 함께 Acrobat을 사용할 준비가 되었습니다.

### 환경 변수 설정 {#setup-environment-variables}

32비트 및 64비트 Java Development Kit, 타사 애플리케이션 및 Adobe Acrobat에 대한 환경 변수를 설정합니다. 환경 변수에는 해당 애플리케이션을 시작하는 데 사용되는 실행 파일의 절대 경로가 포함되어야 합니다. 예를 들어 아래 표에는 몇 가지 애플리케이션에 대한 환경 변수가 나와 있습니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>애플리케이션</strong></p> </td>
   <td><p><strong>환경 변수</strong></p> </td>
   <td><p><strong>예</strong></p> </td>
  </tr>
  <tr>
   <td><p><strong>JDK(64비트)</strong></p> </td>
   <td><p>JAVA_HOME</p> </td>
   <td><p>C:\Program Files\Java\jdk1.8.0_74</p> </td>
  </tr>
  <tr>
   <td><p><strong>Adobe Acrobat</strong></p> </td>
   <td><p>Acrobat_PATH</p> </td>
   <td><p>C:\Program Files (x86)\Adobe\Acrobat 2015\Acrobat\Acrobat.exe</p> </td>
  </tr>
  <tr>
   <td><p><strong>메모장</strong></p> </td>
   <td><p>메모장_PATH</p> </td>
   <td><p>C:\WINDOWS\notepad.exe<br /> <strong></strong></p> </td>
  </tr>
  <tr>
   <td><p><strong>OpenOffice</strong></p> </td>
   <td><p>OpenOffice_PATH</p> </td>
   <td><p>C:\Program Files (x86)\OpenOffice.org4</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* 모든 환경 변수와 각 경로는 대/소문자를 구분합니다.
>* JAVA_HOME, JAVA_HOME_32 및 Acrobat_PATH(Windows 전용)는 필수 환경 변수입니다.
>* 환경 변수 OpenOffice_PATH가 실행 파일의 경로 대신 설치 폴더로 설정됩니다.
>* Word, PowerPoint, Excel 및 Project와 같은 Microsoft® Office 응용 프로그램이나 AutoCAD용 환경 변수를 설정하지 마십시오. 이러한 응용 프로그램이 서버에 설치되어 있으면 PDF 생성 서비스가 이러한 응용 프로그램을 자동으로 시작합니다.
>* UNIX 기반 플랫폼에서 OpenOffice를 /root로 설치합니다. OpenOffice가 루트로 설치되어 있지 않으면 PDF 생성기 서비스가 OpenOffice 문서를 PDF 문서로 변환하지 못합니다. 루트가 아닌 사용자로 OpenOffice를 설치하고 실행해야 하는 경우 루트가 아닌 사용자에게 sudo 권한을 제공합니다.
>* UNIX 기반 플랫폼에서 OpenOffice를 사용하는 경우 다음 명령을 실행하여 경로 변수를 설정합니다.
>
> `export OpenOffice_PATH=/opt/openoffice.org4`

### (IBM® WebSphere®에만 해당) IBM® SSL 소켓 공급자를 구성합니다 {#only-for-ibm-websphere-configure-ibm-ssl-socket-provider}

IBM® SSL 소켓 공급자를 구성하려면 다음 단계를 수행하십시오.

1. java.security 파일의 복사본을 만듭니다. 파일의 기본 위치는 다음과 같습니다 `[WebSphere_installation_directory]\Appserver\java_[version]\jre\lib\security`.
1. 편집할 복사된 java.security 파일을 엽니다.
1. 기본 IBM® WebSphere® 공장 대신 JSSE2 팩토리를 사용하도록 기본 SSL 소켓 팩토리를 변경합니다.

   **기본 컨텐트입니다:**

   ```shell
   #ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
   #ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
   #WebSphere socket factories (in cryptosf.jar)
   ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
   ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
   ```

   **수정된 콘텐츠:**

   ```shell
   ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
   ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
   
   #WebSphere socket factories (in cryptosf.jar)
   #ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
   #ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
   ```

1. AEM Forms 서버가 AEM Forms 서버를 시작하는 동안 업데이트된 java.security 파일을 사용할 수 있도록 하려면 다음 java 인수를 추가하십시오.

   `-Djava.security.properties= [path of newly created Java.security file].`

### (Windows만 해당) 설치 잉크 및 필기 서비스 구성 {#configure-install-ink-and-handwriting-service}

Microsoft® Windows Server를 실행 중인 경우 잉크 및 필기 서비스를 구성합니다. Microsoft® Office의 링크 기능을 사용하는 Microsoft® PowerPoint 파일을 여는 데 이 서비스가 필요합니다.

1. 서버 관리자를 엽니다. 을(를) 클릭합니다. **[!UICONTROL 서버 관리자]** ( 빠른 실행 트레이에 있는) 아이콘을 클릭합니다.
1. 클릭 **[!UICONTROL 기능 추가]** 에서 **[!UICONTROL 기능]** 메뉴 아래의 제품에서 사용할 수 있습니다. 을(를) 선택합니다 **[!UICONTROL 잉크 및 필기 서비스]** 확인란을 선택합니다.
1. **[!UICONTROL 기능 선택]** 대화 상자 **[!UICONTROL 잉크 및 필기 서비스]** 선택됨. 클릭 **[!UICONTROL 설치]** 서비스가 설치되어 있습니다.

### (Windows 전용) Microsoft® Office의 파일 블록 설정을 구성합니다 {#configure-the-file-block-settings-for-microsoft-office}

Microsoft® Office 트러스트 센터 설정을 변경하여 PDF 생성기 서비스가 이전 버전의 Microsoft® Office로 만든 파일을 변환할 수 있도록 합니다.

1. Microsoft® Office 응용 프로그램을 엽니다. 예: Microsoft® Word. 다음으로 이동 **[!UICONTROL 파일]**> **[!UICONTROL 옵션]**. 옵션 대화 상자가 나타납니다.

1. 클릭 **[!UICONTROL Trust Center]**&#x200B;를 클릭하고 **[!UICONTROL 트러스트 센터 설정]**.
1. 에서 **[!UICONTROL 트러스트 센터 설정]**&#x200B;를 클릭합니다. **[!UICONTROL 파일 블록 설정]**.
1. 에서 **[!UICONTROL 파일 유형]** 목록, 선택 취소 **[!UICONTROL 열기]** PDF 생성기 서비스가 PDF 문서로 변환할 수 있어야 하는 파일 형식의 경우

### (Windows만 해당) 프로세스 수준 토큰 바꾸기 권한을 부여합니다 {#grant-the-replace-a-process-level-token-privilege}

애플리케이션 서버를 시작하는 데 사용되는 사용자 계정에는 **프로세스 수준 토큰 바꾸기** 권한. 로컬 시스템 계정에는 **프로세스 수준 토큰 바꾸기** 권한은 기본적으로 사용됩니다. 로컬 관리자 그룹의 사용자와 함께 실행 중인 서버의 경우 권한을 명시적으로 부여해야 합니다. 권한을 부여하려면 다음 단계를 수행하십시오.

1. Microsoft® Windows용 그룹 정책 편집기를 엽니다. 그룹 정책 편집기를 열려면 **[!UICONTROL 시작]**, 유형 **gedit.msc** 검색 시작 상자에서 **[!UICONTROL 그룹 정책 편집기]**.
1. 다음으로 이동 **[!UICONTROL 로컬 컴퓨터 정책]** > **[!UICONTROL 컴퓨터 구성]** > **[!UICONTROL Windows 설정]** > **[!UICONTROL 보안 설정]** > **[!UICONTROL 로컬 정책]** > **[!UICONTROL 사용자 권한 할당]** 및 편집 **[!UICONTROL 프로세스 수준 토큰 바꾸기]** 정책 및 관리자 그룹을 포함합니다.
1. 프로세스 수준 토큰 바꾸기 항목에 사용자를 추가합니다.

### (Windows 전용) 관리자가 아닌 사용자를 위해 PDF 생성기 서비스를 사용하도록 설정 {#enable-the-pdf-generator-service-for-non-administrators}

관리자가 아닌 사용자가 PDF 생성기 서비스를 사용할 수 있도록 설정할 수 있습니다. 일반적으로 관리자 권한이 있는 사용자만 서비스를 사용할 수 있습니다.

1. 환경 변수 PDFG_NON_ADMIN_ENABLED를 생성합니다.
1. 환경 변수의 값을 TRUE로 설정합니다.
1. AEM Forms 인스턴스를 다시 시작합니다.

### (Windows 전용) 사용자 계정 컨트롤 사용 안 함(UAC) {#disable-user-account-control-uac}

1. 시스템 구성 유틸리티에 액세스하려면 다음 위치로 이동하십시오. **[!UICONTROL 시작 > 실행]** 그런 다음 를 입력합니다. **[!UICONTROL MSCONFIG]**.
1. 을(를) 클릭합니다. **[!UICONTROL 도구]** 탭을 선택하고 아래로 스크롤한 다음 선택합니다. **[!UICONTROL UAC 설정 변경]**. 클릭 **[!UICONTROL Launch]** 새 창에서 명령을 실행하려면
1. 슬라이더를 [알림 안 함] 수준으로 조정합니다. 완료되면 명령 창을 닫고 시스템 구성 창을 닫습니다.
1. UAC에 대한 레지스트리 설정이 0으로 설정되어 있는지 확인합니다. 확인하려면 다음 단계를 수행하십시오.

   1. Microsoft®은 레지스트리를 수정하기 전에 이 레지스트리를 백업하는 것을 권장합니다. 자세한 단계는 [Windows에서 레지스트리를 백업 및 복원하는 방법](https://support.microsoft.com/en-us/help/322756).
   1. Microsoft® Windows 레지스트리 편집기를 엽니다. 레지스트리 편집기를 열려면 시작 > 실행으로 이동하여 regedit를 입력한 다음 확인을 클릭합니다.
   1. 다음으로 이동 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`. EnableLUA 값이 0으로 설정되어 있는지 확인합니다.
   1. 값 확인 **EnableLUA** 이 0으로 설정되어 있습니다. 값이 0이 아니면 값을 0으로 변경합니다. 레지스트리 편집기를 닫습니다.

1. 컴퓨터를 다시 시작합니다.

### (Windows 전용) 오류 보고 서비스 사용 안 함 {#disable-error-reporting-service}

Windows Server에서 PDF 생성기 서비스를 사용하여 문서를 PDF으로 변환하는 동안 경우에 따라 Windows Server에서 실행 파일에 문제가 발생하여 닫아야 한다고 보고합니다. 하지만 백그라운드에서 계속 진행되므로 PDF 변환에는 영향을 주지 않습니다.

오류를 수신하지 않으려면 Windows 오류 보고를 비활성화할 수 있습니다. 오류 보고 비활성화에 대한 자세한 내용은 [https://technet.microsoft.com/en-us/library/cc754364.aspx](https://technet.microsoft.com/en-us/library/cc754364.aspx).

### (Windows만 해당) HTML-PDF 변환 구성 {#configure-html-to-pdf-conversion}

PDF 생성기 서비스는 HTML 파일을 PDF 문서로 변환하는 WebKit, WebCapture 및 PhantomJS 경로 또는 메서드를 제공합니다. Windows에서 WebKit 및 Acrobat WebCapture 경로에 대한 변환을 사용하려면 유니코드 글꼴을 %windir%\fonts 디렉토리에 복사합니다.

>[!NOTE]
>
>글꼴 폴더에 새 글꼴을 설치할 때마다 AEM Forms 인스턴스를 다시 시작합니다.

### (UNIX 기반 플랫폼만 해당) HTML-PDF 변환을 위한 추가 구성  {#extra-configurations-for-html-to-pdf-conversion}

UNIX 기반 플랫폼에서 PDF 생성기 서비스는 HTML 파일을 PDF 문서로 변환하기 위해 WebKit 및 PhantomJS 경로를 지원합니다. HTML에서 PDF으로 변환을 활성화하려면 기본 전환 경로에 적용할 수 있는 다음 구성을 수행합니다.

### (UNIX 기반 플랫폼만 해당) 유니코드 글꼴에 대한 지원을 활성화합니다(WebKit만 해당). {#enable-support-for-unicode-fonts-webkit-only}

시스템에 적합한 다음 디렉토리에 유니코드 글꼴을 복사합니다.

* /usr/lib/X11/fonts/TrueType
* /usr/share/fonts/default/TrueType
* /usr/X11R6/lib/X11/fonts/ttf
* /usr/X11R6/lib/X11/fonts/truetype
* /usr/X11R6/lib/X11/fonts/TrueType
* /usr/X11R6/lib/X11/fonts/TTF
* /usr/openwin/lib/X11/fonts/TrueType(Solaris™)

>[!NOTE]
>
>* Red Hat® Enterprise Linux® 6.x 이상에서는 Courier 글꼴을 사용할 수 없습니다. Courier 글꼴을 설치하려면 font-ibm-type1-1.0.3.zip 아카이브를 다운로드합니다. /usr/share/fonts에서 아카이브를 추출합니다. /usr/share/X11/fonts에서 /usr/share/fonts로 심볼 링크를 만듭니다.
>* Html2PdfSvc/bin 및 /usr/share/fonts 디렉토리에서 모든 .lst 글꼴 캐시 파일을 삭제합니다.
>* /usr/lib/X11/fonts 및 /usr/share/fonts 디렉토리가 있는지 확인합니다. 디렉토리가 없는 경우 ln 명령을 사용하여 /usr/share/X11/fonts에서 /usr/lib/X11/fonts로 심볼 링크를 만들고 /usr/share/fonts에서 /usr/share/X11/fonts로 다른 심볼 링크를 만듭니다. 또한 Courier 글꼴은 /usr/lib/X11/fonts에서 사용할 수 있는지 확인하십시오.
>* /usr/share/fonts 또는 /usr/share/X11/fonts 디렉터리에서 모든 글꼴(유니코드 및 비유니코드)을 사용할 수 있는지 확인합니다.
>* 루트가 아닌 사용자로 PDF 생성기 서비스를 실행할 때 루트가 아닌 사용자가 모든 글꼴 디렉터리에 대한 읽기 및 쓰기 액세스 권한을 제공합니다.
>* 글꼴 폴더에 새 글꼴을 설치할 때마다 AEM Forms 인스턴스를 다시 시작합니다.
>


## AEM Forms 추가 기능 패키지 설치 {#install-aem-forms-add-on-package}

AEM Forms 추가 기능 패키지는 AEM에 배포된 애플리케이션입니다. 이 패키지에는 AEM Forms 문서 서비스 및 기타 AEM Forms 기능이 포함되어 있습니다. 패키지를 설치하려면 다음 단계를 수행하십시오.

1. [소프트웨어 배포](https://experience.adobe.com/downloads)를 엽니다. 소프트웨어 배포에 로그인하려면 Adobe ID가 필요합니다.
1. 헤더 메뉴에 제공된 **[!UICONTROL Adobe Experience Manager]**&#x200B;를 누릅니다.
1. 에서 **[!UICONTROL 필터]** 섹션:
   1. 선택 **[!UICONTROL Forms]** 에서 **[!UICONTROL 솔루션]** 드롭다운 목록.
   2. 패키지의 버전 및 유형을 선택합니다. 를 사용할 수도 있습니다 **[!UICONTROL 다운로드 검색]** 결과를 필터링하는 옵션.
1. 운영 체제에 해당하는 패키지 이름을 탭하고 **[!UICONTROL EULA 약관 동의]**, 탭 **[!UICONTROL 다운로드]**.
1. [패키지 관리자](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)를 열고 **[!UICONTROL 패키지 업로드]**&#x200B;를 클릭하여 패키지를 업로드합니다.
1. 패키지를 선택하고 **[!UICONTROL 설치]**&#x200B;를 클릭합니다.

   에 나열된 직접 링크를 통해 패키지를 다운로드할 수도 있습니다 [AEM Forms 릴리스](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 문서.

1. 패키지가 설치되면 AEM 인스턴스를 다시 시작하라는 메시지가 표시됩니다. **서버를 즉시 중지하지 마십시오.** AEM Forms Server를 중지하기 전에 ServiceEvent REGISTERED 및 ServiceEvent UNREGISTERED 메시지가 `[AEM-Installation-Directory]/crx-quickstart/logs/error`.log 파일과 로그 모두 안정적입니다.

## 설치 후 구성 {#post-installation-configurations}

### RSA/BouncyCastle 라이브러리에 대한 부팅 위임 구성  {#configure-boot-delegation-for-rsa-bouncycastle-libraries}

1. AEM 인스턴스를 중지합니다. 로 이동합니다 [AEM 설치 디렉토리]\crx-quickstart\conf\ folder 편집할 sling.properties 파일을 엽니다.

   만약 `[AEM installation directory]\crx-quickstart\bin\start.bat` AEM 인스턴스를 시작하려면 의 sling.properties를 편집합니다 `[AEM_root]\crx-quickstart\`.

1. sling.properties 파일에 다음 속성을 추가합니다.

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   ```

1. (AIX®만 해당) sling.properties 파일에 다음 속성을 추가합니다.

   ```shell
   sling.bootdelegation.xerces=org.apache.xerces.*
   ```

1. 파일을 저장하고 닫습니다.

### 글꼴 관리자 서비스 구성  {#configuring-the-font-manager-service}

1. 에 로그인합니다. [AEM 구성 관리자](http://localhost:4502/system/console/configMgr) 관리자로.
1. 을(를) 찾아 엽니다. **[!UICONTROL CQ-DAM-Handler-Gibson 글꼴 관리자]** 서비스. 시스템 글꼴, Adobe 서버 글꼴 및 고객 글꼴 디렉토리의 경로를 지정합니다. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

   >[!NOTE]
   >
   >Adobe 이외의 당사자가 제공하는 글꼴을 사용할 수 있는 권리는 해당 글꼴이 있는 해당 당사자가 제공한 사용권 계약에 따라 다르며, Adobe 소프트웨어를 사용할 수 있는 라이센스에 따라 적용되지 않습니다. Adobe은 Adobe 소프트웨어와 함께 비Adobe 글꼴을 사용하기 전에, 특히 서버 환경에서 글꼴의 사용과 관련하여 해당 비Adobe 사용권 계약을 모두 검토하고 준수하도록 권장합니다.
   > 글꼴 폴더에 새 글꼴을 설치하면 AEM Forms 인스턴스를 다시 시작합니다.

### PDF 생성기 서비스를 실행하도록 로컬 사용자 계정 구성  {#configure-a-local-user-account-to-run-the-pdf-generator-service}

PDF 생성기 서비스를 실행하려면 로컬 사용자 계정이 필요합니다. 로컬 사용자를 만드는 단계는 [Windows에서 사용자 계정 만들기](https://support.microsoft.com/en-us/help/13951/windows-create-user-account) 또는 UNIX 기반 플랫폼에서 사용자 계정을 만듭니다.

1. 를 엽니다. [AEM Forms PDF 생성기 구성](http://localhost:4502/libs/fd/pdfg/config/ui.html) 페이지.

1. 에서 **[!UICONTROL 사용자 계정]** 탭에서 로컬 사용자 계정의 자격 증명을 제공하고 **[!UICONTROL 제출]**. Microsoft® Windows에서 사용자에게 액세스를 허용할 것인지 묻는 메시지가 나타나면 성공적으로 추가되면 구성된 사용자가 **[!UICONTROL 사용자 계정]** 의 섹션 **[!UICONTROL 사용자 계정]** 탭.

### 시간 초과 설정 구성 {#configure-the-time-out-settings}

1. in [AEM 구성 관리자](http://localhost:4502/system/console/configMgr)를 찾은 후 엽니다. **[!UICONTROL Jacorb ORB 공급자]** 서비스.

   다음 내용을 **[!UICONTROL Custom Properties.name]** 필드를 입력하고 **[!UICONTROL 저장]**. 보류 중인 회신 시간 초과(CORBA 클라이언트 시간 초과라고도 함)를 600초로 설정합니다.

   `jacorb.connection.client.pending_reply_timeout=600000`

1. AEM 작성자 인스턴스에 로그인하고 다음 위치로 이동합니다. **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 도구]** > **[!UICONTROL Forms]** > **[!UICONTROL PDF 생성기 구성]**. 기본 URL은 <http://localhost:4502/libs/fd/pdfg/config/ui.html>.

   를 엽니다. **[!UICONTROL 일반 구성]** 탭하고 환경에 대해 다음 필드의 값을 수정합니다.

<table>
 <tbody>
  <tr>
   <td>필드</td>
   <td>설명</td>
   <td>기본 값</td>
  </tr>
  <tr>
   <td>서버 변환 시간 제한</td>
   <td>PDFG 변환은 서버 변환 시간 초과에 정의된 초 수 동안 활성 상태를 유지합니다</td>
   <td>270초<br /> </td>
  </tr>
  <tr>
   <td>PDFG 정리 스캔(초)</td>
   <td>변환 후 작업을 수행하는 데 필요한 시간(초)입니다.<br /> </td>
   <td>3600초</td>
  </tr>
  <tr>
   <td>작업 만료 초</td>
   <td>PDF 생성기 서비스가 전환을 실행할 수 있는 기간입니다. 작업 만료 초 값이 PDFG 정리 검사 초 값보다 커야 합니다.</td>
   <td>7200초</td>
  </tr>
 </tbody>
</table>

### (Windows 전용) PDF 생성기 서비스용 Acrobat 구성 {#configure-acrobat-for-the-pdf-generator-service}

Microsoft® Windows에서 PDF 생성기 서비스는 Adobe Acrobat을 사용하여 지원되는 파일 형식을 PDF 문서로 변환합니다. PDF 생성기 서비스용 Adobe Acrobat을 구성하려면 다음 단계를 수행하십시오.

1. Acrobat을 열고 을 선택합니다. **[!UICONTROL 편집]**> **[!UICONTROL 기본 설정]**> **[!UICONTROL Updater]**. 업데이트 확인에서 선택을 취소합니다 **[!UICONTROL 업데이트 자동 설치]**&#x200B;를 클릭하고 **[!UICONTROL 확인]**. Acrobat을 닫습니다.
1. 시스템에서 PDF 문서를 두 번 클릭합니다. Acrobat이 처음 시작되면 로그인, 시작 화면 및 EULA의 대화 상자가 나타납니다. PDF 생성기를 사용하도록 구성된 모든 사용자에 대해 이러한 대화 상자를 닫습니다.
1. PDF 생성기 유틸리티 배치 파일을 실행하여 PDF 생성기 서비스용 Acrobat을 구성합니다.

   1. 열기 [AEM 패키지 관리자](http://localhost:4502/crx/packmgr/index.jsp) 다운로드 `adobe-aemfd-pdfg-common-pkg-[version].zip` 파일을 생성할 수 있습니다.
   1. 다운로드한 .zip 파일의 압축을 해제합니다. 관리자 권한으로 명령 프롬프트를 엽니다.
   1. 로 이동합니다 [추출된 zip 파일]`\jcr_root\etc\packages\day\cq60\fd\adobe-aemds-common-pkg-[version]\jcr_root\etc\packages\day\cq60\fd\adobe-aemfd-pdfg-common-pkg-[version]\jcr_root\libs\fd\pdfg\tools\adobe-aemfd-pdfg-utilities-[version]` 디렉토리. 다음 배치 파일을 실행합니다.

      `Acrobat_for_PDFG_Configuration.bat`

      Acrobat은 PDF 생성기 서비스로 실행되도록 구성되어 있습니다.

1. 실행 [시스템 준비 도구(SRT)](#SRT) Acrobat 설치의 유효성을 검사하려면 다음을 수행하십시오.

### (Windows만 해당) HTML-PDF 변환을 위한 기본 경로를 구성합니다 {#configure-primary-route-for-html-to-pdf-conversion-windows-only}

PDF 생성기 서비스는 HTML 파일을 PDF 문서로 변환하는 여러 경로를 제공합니다. Webkit, Acrobat WebCapture(Windows 전용) 및 PhantomJS. PhantomJS 경로는 동적 컨텐츠를 처리할 수 있는 기능이 있고 32비트 라이브러리, 32비트 JDK에 대한 종속성이 없거나 추가 글꼴이 필요 없으므로 PhantomJS 경로를 사용하는 것이 좋습니다. 또한 PhantomJS 경로에는 전환을 실행하기 위한 하위 액세스나 루트 액세스가 필요하지 않습니다.

HTML-PDF 변환의 기본 경로는 Webkit입니다. 변환 경로를 변경하려면

1. AEM 작성자 인스턴스에서 **[!UICONTROL 도구]**> **[!UICONTROL Forms]**> **[!UICONTROL PDF 생성기 구성]**.

1. 에서 **[!UICONTROL 일반 구성]** 탭의 기본 변환 경로를 선택합니다 **[!UICONTROL HTML-PDF 변환을 위한 기본 경로]** 드롭다운.

### 글로벌 트러스트 저장소 초기화 {#intialize-global-trust-store}

Trust Store Management를 사용하여 디지털 서명 및 인증서 인증 확인을 위해 서버에서 신뢰하는 인증서를 가져오고 편집하고 삭제할 수 있습니다. 인증서를 원하는 수만큼 가져오고 내보낼 수 있습니다. 인증서를 가져온 후 트러스트 설정 및 트러스트 저장소 유형을 편집할 수 있습니다. 트러스트 저장소를 초기화하려면 다음 단계를 수행합니다.

1. 관리자로 AEM Forms 인스턴스에 로그인합니다.
1. 이동  **[!UICONTROL 도구]** >  **[!UICONTROL 보안]** >  **[!UICONTROL Trust Store]**.
1. 클릭  **[!UICONTROL TrustStore 만들기]**. 암호 설정 및 탭 **[!UICONTROL 저장]**.

### Reader 확장 및 암호화 서비스에 대한 인증서 설정 {#set-up-certificates-for-reader-extension-and-encryption-service}

DocAssurance 서비스는 PDF 문서에 사용 권한을 적용할 수 있습니다. 사용 권한을 PDF 문서에 적용하려면 인증서를 구성합니다.

인증서를 설정하기 전에 다음 내용이 있는지 확인하십시오.

* 인증서 파일(.pfx)

* 인증서와 함께 제공된 개인 키 암호입니다.

* 개인 키 별칭. Java 키 도구 명령을 실행하여 개인 키 별칭을 볼 수 있습니다.
   `keytool -list -v -keystore [keystore-file] -storetype pkcs12`

* 키 저장소 파일 암호입니다. Adobe의 Reader 확장 인증서를 사용하는 경우 키 저장소 파일 암호는 항상 개인 키 암호와 동일합니다.

다음 단계를 수행하여 인증서를 구성합니다.

1. 관리자로 AEM 작성자 인스턴스에 로그인합니다. 이동 **[!UICONTROL 도구]** > **[!UICONTROL 보안]** > **[!UICONTROL 사용자]**.
1. 을(를) 클릭합니다. **[!UICONTROL 이름]** 사용자 계정 필드입니다. 다음 **[!UICONTROL 사용자 설정 편집]** 페이지가 열립니다. AEM 작성자 인스턴스에서 인증서는 KeyStore에 있습니다. 이전에 KeyStore를 만들지 않은 경우 **[!UICONTROL 키 저장소 만들기]** KeyStore에 새 암호를 설정합니다. 서버에 이미 KeyStore가 있는 경우 이 단계를 건너뜁니다.  Adobe의 Reader 확장 인증서를 사용하는 경우 키 저장소 파일 암호는 항상 개인 키 암호와 동일합니다.
1. 설정 **[!UICONTROL 사용자 설정 편집]** 페이지에서 을 선택합니다 **[!UICONTROL KeyStore]** 탭. 를 확장합니다. **[!UICONTROL 키 저장소 파일에서 개인 키 추가]** 옵션을 선택하고 별칭을 제공합니다. 별칭은 확장 Reader 작업을 수행하는 데 사용됩니다.
1. 인증서 파일을 업로드하려면 **[!UICONTROL 키 저장소 파일 선택]** 업로드하고 &lt;filename>.pfx 파일.

   추가 **[!UICONTROL 키 저장소 암호]**, **[!UICONTROL 개인 키 암호]**, 및 **[!UICONTROL 개인 키 별칭]** 인증서 및 각 필드와 연결됩니다. 클릭 **[!UICONTROL 제출]**.

   >[!NOTE]
   >
   >프로덕션 환경에서 평가 자격 증명을 프로덕션 자격 증명으로 바꿉니다. 만료되었거나 평가 자격 증명을 업데이트하기 전에 이전 Reader 확장 자격 증명을 삭제했는지 확인하십시오.

1. 클릭 **[!UICONTROL 저장 및 닫기]** on **[!UICONTROL 사용자 설정 편집]** 페이지.

### AES-256 사용 {#enable-aes}

PDF 파일에 AES 256 암호화를 사용하려면 JCE(Java Cryptography Extension) Unlimited Strength Shrance Policy 파일을 가져와 설치합니다. jre/lib/security 폴더에서 local_policy.jar 및 US_export_policy.jar 파일을 대체합니다. 예를 들어 Sun JDK를 사용하는 경우 다운로드한 파일을 `[JAVA_HOME]/jre/lib/security` 폴더를 입력합니다.

어셈블러 서비스는 Reader 확장 서비스, 서명 서비스, Forms 서비스 및 출력 서비스에 따라 다릅니다. 다음 단계를 수행하여 필요한 서비스가 작동 중인지 확인합니다.

1. URL에 로그인 `https://'[server]:[port]'/system/console/bundles` 관리자로.
1. 다음 서비스를 검색하고 서비스가 작동 중인지 확인합니다.

<table>
 <tbody>
  <tr>
   <th>서비스 이름</th>
   <th>번들 이름</th>
  </tr>
  <tr>
   <td>서명 서비스</td>
   <td>adobe-aemfd-signatures</td>
  </tr>
  <tr>
   <td>Reader 확장 서비스</td>
   <td>com.adobe.aemfd.adobe-aemfd-readerextensions<br /> </td>
  </tr>
  <tr>
   <td>Forms 서비스</td>
   <td>com.adobe.livecycle.adobe-lc-forms-bedrock-connector<br /> </td>
  </tr>
  <tr>
   <td>출력 서비스</td>
   <td>com.adobe.livecycle.adobe-lc-forms-bedrock-connector</td>
  </tr>
 </tbody>
</table>

## 알려진 문제 및 문제 해결 {#known-issues-and-troubleshooting}

* 압축된 입력 파일에 파일 이름에 더블바이트 문자가 있는 HTML 파일이 포함된 경우 PDF으로 HTML 변환이 실패합니다. 이 문제를 방지하려면 HTML 파일의 이름을 지정할 때 더블바이트 문자를 사용하지 마십시오.

* UNIX 기반 운영 체제에서 누락된 라이브러리를 찾으려면 다음을 수행하십시오.

1. 다음으로 이동 `[crx-repository]/bedrock/svcnative/HtmlToPdfSvc/bin/`.

1. 다음 명령을 실행하여 PhantomJS에서 HTML-PDF 변환에 필요한 모든 라이브러리를 나열합니다.

   `ldd phantomjs`

   다음 명령을 실행하여 누락된 라이브러리를 나열합니다.

   `ldd phantomjs | grep not`

1. 누락된 라이브러리를 수동으로 설치합니다.

## 시스템 준비 도구(SRT) {#SRT}

시스템 준비 도구는 시스템이 PDF 생성기 전환을 실행하도록 제대로 구성되어 있는지 확인합니다. 지정된 경로에서 보고서가 생성됩니다. 도구를 실행하려면

1. 명령 프롬프트를 엽니다. 로 이동합니다 `[extracted-adobe-aemfd-pdfg-common-pkg]\jcr_root\libs\fd\pdfg\tools` 폴더를 입력합니다.

1. 명령 프롬프트에서 다음 명령을 실행합니다.

   `java -jar forms-srt-[version].jar [Path_of_reports_folder] en`

   명령은 보고서를 생성하고 srt_config.yaml 파일도 생성합니다.

   >[!NOTE]
   >
   > * 시스템 준비 도구에서 Acrobat 플러그인 폴더에서 pdfgen.api 파일을 사용할 수 없다고 보고하는 경우 의 pdfgen.api 파일을 복사합니다 `[extracted-adobe-aemfd-pdfg-common-pkg]\jcr_root\libs\fd\pdfg\tools\adobe-aemfd-pdfg-utilities-[version]\plugins\x86_win32` 디렉토리 `[Acrobat_root]\Acrobat\plug_ins` 디렉토리.
   >
   > * srt_config.yaml 파일을 사용하여 의 다양한 설정을 구성할 수 있습니다. 파일의 형식은 다음과 같습니다.

       # SRT 구성
       
       # 참고 - 구문 분석 오류를 방지하려면 올바른 형식을 따르십시오
       
       예: &lt;param name=&quot;&quot;>:&lt;space>&lt;param value=&quot;&quot;>
       
       #locale: (필수 필드)SRT에 사용할 로케일입니다. 지원되는 로케일 [en/fr/de/ja].
       로케일: en
       
       #aemTempDir: AEM Temp 디렉토리
       aemTempDir:
       
       #users: PDFG 변환 사용자 목록 제공
       #users:
       # - user1
       # - user2
       사용자:
       
       #profile: 프로파일을 선택하여 특정 검사를 실행합니다. [LCM]에서 선택하십시오. 더 많은 항목이 곧 추가됩니다
       프로필:
       
       #outputDir: 출력 파일을 저장할 디렉토리
       outputDir:
   >
1. 다음으로 이동 `[Path_of_reports_folder]`. SystemReadinessTool.html 파일을 엽니다. 보고서를 확인하고 언급된 문제를 수정합니다.

## 문제 해결

SRT 도구에서 보고한 모든 문제를 수정한 후에도 문제가 발생하는 경우 다음 검사를 수행하십시오.

다음 검사를 수행하기 전에 [시스템 준비 도구](#SRT) 오류를 보고하지 않습니다.

+++ Adobe Acrobat

* 만 확인 [지원되는 버전](aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator) Microsoft® Office(32비트) 및 Adobe Acrobat이 설치되고 열기 대화 상자가 취소됩니다.
* Adobe Acrobat 업데이트 서비스가 비활성화되어 있는지 확인하십시오.
* 다음을 확인합니다. [Acrobat_for_PDFG_Configuration.bat](#configure-acrobat-for-the-pdf-generator-service) 관리자 권한으로 배치 파일을 실행했습니다.
* PDF 생성기 사용자가 PDF 구성 UI에 추가되었는지 확인합니다.
* 다음을 확인합니다. [프로세스 수준 토큰 바꾸기](#grant-the-replace-a-process-level-token-privilege) PDF 생성기 사용자에 대한 권한이 추가되었습니다.
* Microsoft Office 응용 프로그램에 Acrobat PDFMaker Office COM Addin이 활성화되어 있는지 확인합니다.

+++

+++OpenOffice

**Microsoft® Windows**

* 32비트 [지원되는 버전 ](aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator) Microsoft Office의 대화 상자가 설치되고 모든 응용 프로그램에 대해 열기 대화 상자가 취소됩니다.
* PDF 생성기 사용자가 PDF 구성 UI에 추가되었는지 확인합니다.
* PDF 생성기 사용자가 관리자 그룹의 구성원이고 [프로세스 수준 토큰 바꾸기](#grant-the-replace-a-process-level-token-privilege) 사용자에 대해 권한이 설정됩니다.
* 사용자가 PDF 생성기 UI에 구성되어 있는지 확인하고 다음 작업을 수행하십시오.
   1. PDF 생성기 사용자를 사용하여 Microsoft® Windows에 로그인합니다.
   1. Microsoft® Office 또는 OpenOffice 응용 프로그램을 열고 모든 대화 상자를 취소합니다.
   1. AdobePDF를 기본 프린터로 설정합니다.
   1. Acrobat을 PDF 파일에 대한 기본 프로그램으로 설정합니다.
   1. Microsoft Office 응용 프로그램에서 파일 > 인쇄 및 Acrobat 리본 옵션을 사용하여 수동 변환을 수행하고 모든 대화 상자를 취소합니다.
   1. winword.exe, powerpoint.exe 및 excel.exe와 같은 변환과 관련된 모든 프로세스를 종료합니다.
   1. AEM Forms 서버를 다시 시작합니다.

**Linux®**

* 설치 [지원되는 버전](aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator) OpenOffice의 URL 섹션을 참조하십시오. AEM Forms은 32비트 및 64비트 버전을 모두 지원합니다. 설치 후 OpenOffice 응용 프로그램을 모두 열고 대화 상자 창을 모두 취소하고 응용 프로그램을 닫습니다. 응용 프로그램을 다시 열고 OpenOffice 응용 프로그램을 열 때 대화 상자가 표시되지 않도록 합니다.

* 환경 변수 만들기 `OpenOffice_PATH` OpenOffice 설치는 [콘솔](https://linuxize.com/post/how-to-set-and-list-environment-variables-in-linux/) 또는 dt(장치 트리) 프로필을 참조하십시오.
* OpenOffice 설치에 문제가 있는 경우 [32비트 라이브러리](#extrarequirements) OpenOffice 설치에 필요한 를 사용할 수 있습니다.

+++

+++HTML-PDF 변환 문제

* Generator 구성 UI에 글꼴 디렉토리가 추가되어 있는지 확인합니다.

**Linux 및 Solaris(PhantomJS 변환 경로)**

* Webkit 기반 HTMLToPDF 변환용 32비트 라이브러리(libicudata.so.42)와 64비트(libicudata.so.42 libs)가 PhantomJS 기반 HTMLToPDF 변환에 사용 가능한지 확인합니다.

* phantomjs에 대한 누락된 라이브러리를 나열하려면 다음 명령을 실행하십시오.

   ```
   ldd phantomjs | grep not
   ```

* JAVA_HOME_32 환경 변수가 올바른 위치를 가리키는지 확인합니다.

**Linux® 및 Solaris™(WebKit 변환 경로)**

* 디렉토리 확인 `/usr/lib/X11/fonts` 및 `/usr/share/fonts` 존재 디렉터리가 없는 경우 `/usr/share/X11/fonts` to `/usr/lib/X11/fonts` 그리고 또 다른 심볼 링크 `/usr/share/fonts` to `/usr/share/X11/fonts`.

   ```
   ln -s /usr/share/fonts /usr/share/X11/fonts
   
   ln -s /usr/share/X11/fonts /usr/lib/X11/fonts
   ```

* IBM 글꼴이 사용자/공유/글꼴로 복사되었는지 확인합니다.
* 유령 취약성 수정 glibc가 컴퓨터에서 사용 가능한지 확인하십시오. 기본 패키지 관리자를 사용하여 최신 버전의 glibc로 업데이트하십시오. 여기에는 유령 취약성 수정이 포함됩니다.
* 32비트 lib curl, libcrypto 및 libssl 라이브러리의 최신 버전이 시스템에 설치되어 있는지 확인하십시오. symlink도 만듭니다 `/usr/lib/libcurl.so` (또는 libcurl.a for AIX®), `/usr/lib/libcrypto.so` (또는 libcrypto.a for AIX®) 및 `/usr/lib/libssl.so` (또는 AIX®용 libssl.a)에서 각 라이브러리의 최신 버전(32비트)을 가리킵니다.

* IBM® SSL 소켓 공급자에 대해 다음 단계를 수행하십시오.
   1. 다음 위치에서 java.security 파일 복사 `<WAS_Installed_JAVA>\jre\lib\security` AEM Forms 서버에 있는 모든 위치에 연결할 수 있습니다. 기본 위치는 Default Location입니다. = `<WAS_Installed>\Appserver\java_[version]\jre\lib\security`.

   1. 복사된 위치에서 java.security 파일을 편집하고 JSSE2 팩토리가 있는 기본 SSL 소켓 팩토리를 변경합니다(WebSphere® 대신 JSSE2 팩토리를 사용).

      다음 기본 JSSE 소켓 팩토리를 변경합니다.

      ```
      #ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
      #ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
      WebSphere socket factories (in cryptosf.jar)
      ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
      ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
      ```

      with

      ```
      ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
      ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
      WebSphere socket factories (in cryptosf.jar)
      #ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
      #ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
      ```

+++

+++ PDFG(PDF 생성기) 사용자를 추가할 수 없습니다.

* Windows에 Microsoft® Visual C++ 2012 x86 및 Microsoft® Visual C++ 2013 x86(32비트) 재배포 가능 패키지가 설치되어 있는지 확인합니다.

+++

+++자동화 테스트 실패

* Microsoft® Office 및 OpenOffice의 경우 전환 중에 대화 상자가 나타나지 않도록 각 사용자와 마찬가지로 하나 이상의 전환을 수동으로 수행하십시오. 대화 상자가 나타나면 해제합니다. 자동화된 변환 중에는 이러한 대화 상자가 표시되지 않아야 합니다.

* OSGi 환경의 AEM Forms에서 자동화를 실행하기 전에 테스트 패키지가 설치되고 활성화되어 있는지 확인합니다.

+++

+++여러 사용자 변환 실패

* 서버 로그를 확인하여 특정 사용자에 대해 변환이 실패하는지 확인합니다.프로세스 탐색기는 다른 사용자에 대해 실행 중인 프로세스를 확인하는 데 도움이 될 수 있습니다.

* PDF 생성기에 대해 구성된 사용자에게 로컬 관리자 권한이 있는지 확인합니다.

* PDF 생성기 사용자에게 LC 임시 및 PDFG 임시 사용자에 대한 읽기, 쓰기 및 실행 권한이 있는지 확인합니다.

* Microsoft® Office 및 OpenOffice의 경우 전환 중에 대화 상자가 나타나지 않도록 각 사용자와 마찬가지로 하나 이상의 전환을 수동으로 수행하십시오. 대화 상자가 나타나면 해제합니다. 자동화된 변환 중에는 이러한 대화 상자가 표시되지 않아야 합니다.

* 샘플 변환을 수행합니다.

+++

+++AEM Forms 서버에 설치된 Adobe Acrobat 라이센스가 만료됩니다

* Adobe Acrobat의 기존 라이센스가 있고 만료되면 [최신 버전의 Adobe Application Manager 다운로드](https://helpx.adobe.com/in/creative-suite/kb/aam-troubleshoot-download-install.html), 및 일련 번호 마이그레이션. 전 [일련 번호 마이그레이션](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number).

   * 다음 명령을 사용하여 prov.xml을 생성하고 prov.xml 파일을 사용하여 기존 설치를 재직렬화하십시오. [일련 번호 마이그레이션](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number) 번호 문서.

          &quot;
          
          adobe_prtk —tool=VolumeSerialize —generate —serial=&lt;serialnum> [—leid=&lt;leid>] [—regsuppress=ss] [—eulasuppress] [—locales=제한된 로케일 목록 xx_XX 형식 또는 ALL>] [—profile=&lt;absolute path=&quot;&quot; to=&quot;&quot; prov.xml=&quot;&quot;>]
          
          &quot;
      
   * 볼륨을 사용하여 패키지를 serialize(prov.xml 파일과 새 일련 번호를 사용하여 기존 설치를 다시 serialize)합니다. PRTK 설치 폴더에서 관리자로 다음 명령을 실행하여 클라이언트 컴퓨터에서 배포된 패키지를 serialize 및 활성화합니다.

          &quot;
          adobe_prtk —tool=VolumeSerialize —profile=C:\prov.xml -stream
          
          &quot;
      
* 대규모 설치의 경우 [Acrobat Customization Wizard](https://www.adobe.com/devnet-docs/acrobatetk/tools/Wizard/index.html) 이전 버전의 Reader 및 Acrobat을 제거하려면 다음을 수행하십시오. 설치 관리자를 사용자 지정하고 조직의 모든 컴퓨터에 배포합니다.

+++

+++ AEM Forms Server는 오프라인 또는 보안 환경에 있으며 Acrobat을 활성화하기 위해 인터넷을 사용할 수 없습니다.

* Adobe 제품을 처음 실행한 후 7일 이내에 온라인으로 이동하여 온라인 활성화 및 등록을 완료하거나 인터넷 사용 장치 및 제품의 일련 번호를 사용하여 이 프로세스를 완료할 수 있습니다. 자세한 지침은 [오프라인 활성화](https://exception.licenses.adobe.com/aoes/aoes/v1/t1?locale=en).

+++

## 다음 단계 {#next-steps}

작동하는 AEM Forms 문서 서비스 환경이 있습니다. 문서 서비스는 다음을 통해 사용할 수 있습니다.

* [OSGi에서 양식 중심의 워크플로우](/help/forms/using/aem-forms-workflow.md)
* [감시 폴더](/help/forms/using/watched-folder-in-aem-forms.md)
* [문서 서비스 API](/help/forms/using/aem-document-services-programmatically.md)
