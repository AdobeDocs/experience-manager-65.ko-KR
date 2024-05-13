---
title: 문서 서비스 설치 및 구성
description: AEM Forms 문서 서비스를 설치하여 PDF 문서를 만들고, 조합하고, 배포하고, 보관하고, 디지털 서명을 추가하여 문서에 대한 액세스를 제한하고, 바코드 Forms을 디코딩합니다.
topic-tags: installing
role: Admin, User, Developer
solution: Experience Manager, Experience Manager Forms
source-git-commit: acb023caf0a7e64fea9cf5d9198d672ee14c8d88
workflow-type: tm+mt
source-wordcount: '5703'
ht-degree: 1%

---


# 문서 서비스 설치 및 구성 {#installing-and-configuring-document-services}

AEM Forms은 다양한 문서 수준 작업을 수행하기 위한 일련의 OSGi 서비스를 제공합니다. 예를 들어 PDF 문서를 작성, 조합, 배포 및 보관하고, 디지털 서명을 추가하여 문서에 대한 액세스를 제한하고, Barcoded Forms을 디코딩하는 서비스를 들 수 있습니다. 이러한 서비스는 AEM Forms 추가 기능 패키지에 포함되어 있습니다. 이러한 서비스를 통칭하여 문서 서비스라고 합니다. 사용 가능한 문서 서비스 및 주요 기능 목록은 다음과 같습니다.

* **어셈블러 서비스:** PDF 및 XDP 문서를 결합하고, 재배열하고, 보강하고, PDF 문서에 대한 정보를 얻을 수 있습니다. 또한 PDF 문서를 PDF/A 표준으로 변환 및 검증하고, PDF forms, XML 양식 및 PDF forms을 PDF/A-1b, PDF/A-2b 및 PDFA/A-3b로 변환합니다. 자세한 내용은 [어셈블러 서비스](/help/forms/using/assembler-service.md).

* **ConvertPDF 서비스:** PDF 문서를 PostScript 또는 이미지 파일(JPEG, JPEG 2000, PNG 및 TIFF)로 변환할 수 있습니다. 자세한 내용은 [ConvertPDF 서비스](/help/forms/using/using-convertpdf-service.md).

* **바코드 Forms 서비스:** 바코드의 전자 이미지에서 데이터를 추출할 수 있습니다. 이 서비스는 하나 이상의 바코드가 포함된 TIFF 및 PDF 파일을 입력으로 받아 바코드 데이터를 추출합니다. 자세한 내용은 [바코드 Forms 서비스](/help/forms/using/using-barcoded-forms-service.md).

* **DocAssurance 서비스:** 문서를 암호화 및 해독하고, 추가 사용 권한으로 Adobe Reader의 기능을 확장하며, 문서에 디지털 서명을 추가할 수 있습니다. Doc Assurance 서비스에는 서명, 암호화 및 리더 확장의 세 가지 서비스가 포함됩니다. 자세한 내용은 [DocAssurance 서비스](/help/forms/using/overview-aem-document-services.md).

* **암호화 서비스:** 문서를 암호화하고 해독할 수 있습니다. 문서가 암호화되면 해당 내용을 읽을 수 없게 됩니다. 승인된 사용자는 문서의 내용을 해독하여 콘텐츠에 액세스할 수 있습니다. 자세한 내용은 [암호화 서비스](/help/forms/using/overview-aem-document-services.md#encryption-service).

* **Forms 서비스:** 일반적으로 Forms Designer에서 만든 양식을 확인, 처리, 변환 및 제공하는 대화형 데이터 캡처 클라이언트 애플리케이션을 만들 수 있습니다. Forms 서비스는 PDF 문서로 개발하는 모든 양식 디자인을 렌더링합니다. 자세한 내용은 [Forms 서비스](/help/forms/using/forms-service.md).

* **출력 서비스:** PDF, 레이저 프린터 형식, 라벨 프린터 형식 등 다양한 형식의 문서를 만들 수 있습니다. 레이저 프린터 형식은 PostScript 및 PCL(Printer Control Language)입니다. 자세한 내용은 [출력 서비스](/help/forms/using/output-service.md).

* **PDF Generator 서비스:** PDF Generator 서비스는 기본 파일 형식을 PDF으로 변환하는 API를 제공합니다. 또한 PDF을 다른 파일 형식으로 변환하고 PDF 문서의 크기를 최적화합니다. 자세한 내용은 [PDF Generator 서비스](aem-document-services-programmatically.md#pdfgeneratorservice).

* **Reader 확장 서비스:** 추가 사용 권한으로 Adobe Reader의 기능을 확장하여 조직에서 대화형 PDF 문서를 쉽게 공유할 수 있도록 합니다. 이 서비스는 Adobe Reader을 사용하여 PDF 문서를 열 때 문서에 주석 추가, 양식 채우기, 문서 저장 등과 같은 사용할 수 없는 기능을 활성화합니다. 자세한 내용은 [Reader 확장 서비스](/help/forms/using/overview-aem-document-services.md#reader-extension-service).

* **서명 서비스:** AEM 서버에서 디지털 서명과 문서를 사용하여 작업할 수 있습니다. 예를 들어 서명 서비스는 일반적으로 다음과 같은 경우에 사용됩니다.

   * AEM 서버는 Acrobat 또는 Adobe Reader을 사용하여 열도록 사용자에게 전송되기 전에 양식을 인증합니다.
   * AEM 서버는 Acrobat 또는 Adobe Reader을 사용하여 양식에 추가된 서명을 확인합니다.
   * AEM 서버는 공증인을 대신하여 양식에 서명합니다.

  서명 서비스는 신뢰 저장소에 저장된 인증서 및 자격 증명에 액세스합니다. 자세한 내용은 [서명 서비스](/help/forms/using/aem-document-services-programmatically.md).

AEM Forms은 강력한 엔터프라이즈급 플랫폼이며 문서 서비스는 AEM Forms의 기능 중 하나에 불과합니다. 전체 기능 목록은 다음을 참조하십시오. [AEM Forms 소개](/help/forms/using/introduction-aem-forms.md).

## 배포 토폴로지 {#deployment-topology}

AEM Forms 추가 기능 패키지는 AEM에 배포된 애플리케이션입니다. 일반적으로 AEM Forms 문서 서비스를 실행하려면 AEM 인스턴스(작성자 또는 게시)가 하나만 필요합니다. AEM Forms 문서 서비스를 실행하려면 다음 토폴로지를 사용하는 것이 좋습니다. 토폴로지에 대한 자세한 내용은 [AEM Forms의 아키텍처 및 배포 토폴로지](/help/forms/using/aem-forms-architecture-deployment.md).

![AEM Forms의 아키텍처 및 배포 토폴로지](do-not-localize/document-services.png)

>[!NOTE]
>
>AEM Forms을 사용하면 단일 서버에서 모든 기능을 설정하고 실행할 수 있지만 프로덕션 환경에서는 특정 기능에 대해 용량 계획, 로드 밸런싱 및 전용 서버 설정을 수행해야 합니다. 예를 들어, PDF Generator 서비스를 사용하여 하루에 수천 페이지의 데이터를 변환하고 여러 적응형 양식을 사용하여 데이터를 캡처하는 환경의 경우, PDF Generator 서비스 및 적응형 양식 기능을 위해 별도의 AEM Forms 서버를 설정하십시오. 최적의 성능을 제공하고 서로 독립적으로 서버를 확장할 수 있습니다.

## 시스템 요구 사항 {#system-requirements}

AEM Forms 문서 서비스 설치 및 구성을 시작하기 전에 다음을 확인하십시오.

* 하드웨어 및 소프트웨어 인프라가 구축되어 있습니다. 지원되는 하드웨어 및 소프트웨어에 대한 자세한 목록은 [기술 요구 사항](/help/sites-deploying/technical-requirements.md).

* AEM 인스턴스의 설치 경로에 공백이 포함되어 있지 않습니다.
* AEM 인스턴스가 실행 중입니다. AEM 용어에서 &quot;인스턴스&quot;는 작성자 또는 게시 모드의 서버에서 실행되는 AEM의 사본입니다. 일반적으로 AEM Forms 문서 서비스를 실행하려면 하나의 AEM 인스턴스(작성자 또는 게시)만 필요합니다.

   * **작성자**: 콘텐츠를 만들고, 업로드하고, 편집하고, 웹 사이트를 관리하는 데 사용되는 AEM 인스턴스입니다. 콘텐츠를 실행할 준비가 되면 게시 인스턴스에 복제됩니다.
   * **게시**: 인터넷 또는 내부 네트워크를 통해 게시된 콘텐츠를 일반에게 제공하는 AEM 인스턴스.

* 메모리 요구 사항이 충족됩니다. AEM Forms 추가 기능 패키지를 사용하려면 다음 작업을 수행해야 합니다.

   * Microsoft® Windows 기반 설치용 15GB의 임시 공간.
   * UNIX 기반 설치의 경우 6GB의 임시 공간이 필요합니다.

* Microsoft® Windows 및 Linux®에서 PDF 생성기가 변환을 수행하는 데 필요한 클라이언트 소프트웨어가 설치되어 있습니다.

   * **Microsoft® Windows**: 설치 [Microsoft® Office](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p) 또는 [아파치 오픈오피스](/help/forms/using/aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator)
   * **Linux®**: 설치 [아파치 오픈오피스](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p)

>[!NOTE]
>
>* Microsoft® Windows에서 PDF Generator은 HTML 파일을 PDF 문서로 변환하기 위한 WebKit, Acrobat WebCapture 및 PhantomJS 변환 경로를 지원합니다.
>* UNIX 기반 운영 체제에서 PDF Generator은 HTML 파일을 PDF 문서로 변환하기 위한 WebKit 및 PhantomJS 변환 경로를 지원합니다.
>

### UNIX 기반 운영 체제에 대한 추가 요구 사항 {#extrarequirements}

UNIX 기반 운영 체제를 사용하는 경우 해당 운영 체제의 설치 미디어에서 다음 32비트 패키지를 설치합니다.
<table>
 <tbody>
  <tr>
   <td>
    <ul>
     <li>지수</li>
    </ul> </td>
   <td>
    <ul>
     <li>libxcb</li>
    </ul> </td>
   <td>
    <ul>
     <li>자유 형식</li>
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
     <li>즐리브</li>
    </ul> </td>
   <td>
    <ul>
     <li>libice</li>
    </ul> </td>
   <td>
    <ul>
     <li>리부uid</li>
    </ul> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li>아교</li>
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

* **(PDF Generator 전용**) 32비트 버전의 libcurl, libcrypto 및 libssl 라이브러리를 설치하고 아래 심볼릭 링크를 만듭니다. 심볼릭 링크는 해당 라이브러리의 최신 버전을 가리킵니다.

   * /usr/lib/libcurl.so
   * /usr/lib/libcrypto.so
   * /usr/lib/libssl.so

* **(PDF Generator 전용)** PDF Generator 서비스는 HTML 파일을 PDF 문서로 변환하기 위한 WebKit 및 PhantomJS 경로를 지원합니다. PhantomJS 경로에 대한 변환을 활성화하려면 아래에 나열된 64비트 라이브러리를 설치합니다. 일반적으로 이러한 라이브러리는 이미 설치되어 있습니다. 라이브러리가 누락된 경우 수동으로 설치합니다.

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

사전 설치 구성 섹션에 나열된 구성은 PDF Generator 서비스에만 적용됩니다. PDF Generator 서비스를 구성하지 않는 경우 사전 설치 구성 섹션을 건너뛸 수 있습니다.

### Adobe Acrobat 및 서드파티 애플리케이션 설치 {#install-adobe-acrobat-and-third-party-applications}

PDF Generator 서비스를 사용하여 Microsoft® Word, Microsoft® Excel, Microsoft® PowerPoint, OpenOffice, WordPerfect X7 및 Adobe Acrobat과 같은 기본 파일 형식을 PDF 문서로 변환하려는 경우 이러한 애플리케이션이 AEM Forms 서버에 설치되어 있는지 확인하십시오.

>[!NOTE]
>
>* AEM Forms 서버가 오프라인 또는 보안 환경에 있고 인터넷을 사용하여 Adobe Acrobat을 활성화할 수 없는 경우 다음을 참조하십시오. [오프라인 활성화](https://exception.licenses.adobe.com/aoes/aoes/v1/t1?locale=en) Adobe Acrobat의 이러한 인스턴스를 활성화하는 방법에 대해 설명합니다.
>* Adobe Acrobat, Microsoft® Word, Excel 및 Powerpoint는 Microsoft® Windows에서만 사용할 수 있습니다. UNIX 기반 운영 체제를 사용하는 경우 OpenOffice를 설치하여 리치 텍스트 파일과 지원되는 Microsoft® Office 파일을 PDF 문서로 변환합니다.
>* PDF Generator 서비스를 사용하도록 구성된 모든 사용자에 대해 Adobe Acrobat 및 타사 소프트웨어를 설치한 후 표시되는 모든 대화 상자를 닫습니다.
>* 설치된 모든 소프트웨어를 한 번 이상 시작합니다. PDF Generator 서비스를 사용하도록 구성된 모든 사용자의 대화 상자를 모두 닫습니다.
>* [Adobe Acrobat 일련 번호의 만료 날짜 확인](https://helpx.adobe.com/enterprise/kb/volume-license-expiration-check.html) 라이선스 업데이트 또는 [일련 번호 마이그레이션](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number) 만료일 기준.

Acrobat을 설치한 후 Microsoft® Word를 엽니다. 다음에서 **Acrobat** 탭을 클릭하고 **PDF 만들기** 컴퓨터에서 사용할 수 있는 .doc 또는 .docx 파일을 PDF 문서로 변환합니다. 전환이 성공하면 AEM Forms은 PDF Generator 서비스와 함께 Acrobat을 사용할 준비가 되었습니다.

### 환경 변수 설정 {#setup-environment-variables}

64비트 Java Development Kit, 서드파티 애플리케이션 및 Adobe Acrobat에 대한 환경 변수를 설정합니다. 환경 변수에는 해당 응용 프로그램을 시작하는 데 사용되는 실행 파일의 절대 경로가 포함되어야 합니다. 예를 들어 아래 표에는 몇 가지 응용 프로그램에 대한 환경 변수가 나와 있습니다.

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
   <td><p>Acrobat 경로</p> </td>
   <td><p>C:\Program Files (x86)\Adobe\Acrobat 2015\Acrobat\Acrobat.exe</p> </td>
  </tr>
  <tr>
   <td><p><strong>메모장</strong></p> </td>
   <td><p>메모장 경로</p> </td>
   <td><p>C:\WINDOWS\notepad.exe<br /> <strong></strong></p> </td>
  </tr>
  <tr>
   <td><p><strong>OpenOffice</strong></p> </td>
   <td><p>OpenOffice PATH</p> </td>
   <td><p>C:\Program Files (x86)\OpenOffice.org4</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* 모든 환경 변수와 해당 경로는 대/소문자를 구분합니다.
>* JAVA_HOME 및 Acrobat_PATH(Windows에만 해당)는 필수 환경 변수입니다.
>* 환경 변수 OpenOffice_PATH가 실행 파일의 경로 대신 설치 폴더로 설정됩니다.
>* Word, PowerPoint, Excel, 프로젝트 등 Microsoft® Office 애플리케이션이나 AutoCAD에 대한 환경 변수는 설정하지 마십시오. 이러한 응용 프로그램이 서버에 설치된 경우 PDF 생성 서비스가 이러한 응용 프로그램을 자동으로 시작합니다.
>* UNIX 기반 플랫폼에서 OpenOffice를 /root로 설치합니다. OpenOffice가 루트로 설치되지 않은 경우 PDF Generator 서비스가 OpenOffice 문서를 PDF 문서로 변환하지 못합니다. 루트가 아닌 사용자로 OpenOffice를 설치하고 실행해야 하는 경우 루트가 아닌 사용자에게 sudo 권한을 제공합니다.
>* UNIX 기반 플랫폼에서 OpenOffice를 사용하는 경우 다음 명령을 실행하여 경로 변수를 설정합니다.
>
>  `export OpenOffice_PATH=/opt/openoffice.org4`

### (IBM® WebSphere®에만 해당) IBM® SSL 소켓 공급자 구성 {#only-for-ibm-websphere-configure-ibm-ssl-socket-provider}

IBM® SSL 소켓 공급자를 구성하려면 다음 단계를 수행하십시오.

1. java.security 파일의 복사본을 만듭니다. 파일의 기본 위치는 입니다. `[WebSphere_installation_directory]\Appserver\java_[version]\jre\lib\security`.
1. 복사한 java.security 파일을 열어 편집합니다.
1. 기본 IBM® WebSphere® 공장 대신 JSSE2 공장을 사용하도록 기본 SSL 소켓 공장을 변경합니다.

   **기본 컨텐츠:**

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

1. AEM Forms 서버를 시작하는 동안 AEM Forms 서버가 업데이트된 java.security 파일을 사용할 수 있도록 하려면 다음 java 인수를 추가합니다.

   `-Djava.security.properties= [path of newly created Java.security file].`

### (Windows 전용) Microsoft® Office용 파일 블록 설정 구성 {#configure-the-file-block-settings-for-microsoft-office}

Microsoft® Office 트러스트 센터 설정을 변경하여 PDF Generator 서비스가 이전 버전의 Microsoft® Office로 만든 파일을 변환할 수 있도록 합니다.

1. Microsoft® Office 애플리케이션을 엽니다. 예를 들어 Microsoft® Word입니다. 다음으로 이동 **[!UICONTROL 파일]**> **[!UICONTROL 옵션]**. 옵션 대화 상자가 나타납니다.

1. 클릭 **[!UICONTROL 트러스트 센터]**, 및 클릭 **[!UICONTROL 트러스트 센터 설정]**.
1. 다음에서 **[!UICONTROL 트러스트 센터 설정]**, 클릭 **[!UICONTROL 파일 차단 설정]**.
1. 다음에서 **[!UICONTROL 파일 유형]** 목록, 선택 해제 **[!UICONTROL 열기]** PDF Generator 서비스가 PDF 문서로 변환할 수 있도록 허용해야 하는 파일 유형입니다.

### (Windows 전용) 프로세스 수준 토큰 바꾸기 권한을 부여합니다. {#grant-the-replace-a-process-level-token-privilege}

응용 프로그램 서버를 시작하는 데 사용되는 사용자 계정에는 **프로세스 수준 토큰 바꾸기** 권한. 로컬 시스템 계정에는 **프로세스 수준 토큰 바꾸기** 기본적으로 권한입니다. 로컬 관리자 그룹의 사용자로 실행 중인 서버의 경우 권한을 명시적으로 부여해야 합니다. 권한을 부여하려면 다음 단계를 수행하십시오.

1. Microsoft® Windows용 그룹 정책 편집기를 엽니다. 그룹 정책 편집기를 열려면 **[!UICONTROL 시작]**, 유형 **gpedit.msc** 검색 시작 상자에서 **[!UICONTROL 그룹 정책 편집기]**.
1. 다음으로 이동 **[!UICONTROL 로컬 컴퓨터 정책]** > **[!UICONTROL 컴퓨터 구성]** > **[!UICONTROL Windows 설정]** > **[!UICONTROL 보안 설정]** > **[!UICONTROL 로컬 정책]** > **[!UICONTROL 사용자 권한 할당]** 및 편집 **[!UICONTROL 프로세스 수준 토큰 바꾸기]** 정책을 참조하고 Administrators 그룹을 포함합니다.
1. 프로세스 수준 토큰 바꾸기 항목에 사용자를 추가합니다.

>[!NOTE]
>
> AEM 서버가 LSA에서 서비스로 실행 중인 경우 이 권한을 사용자에게 명시적으로 할당할 필요가 없을 수 있으며, 이는 VM의 PDFG에 필요한 애플리케이션/구성 요소 외에 다른 애플리케이션/구성 요소가 설치되어 있지 않은 경우 **프로세스 수준 토큰 오른쪽 바꾸기** 로컬 서비스 및 네트워크 서비스 계정만 권한을 가져야 합니다.

### (Windows 전용) 관리자가 아닌 사용자를 위해 PDF Generator 서비스를 사용하도록 설정합니다. {#enable-the-pdf-generator-service-for-non-administrators}

관리자가 아닌 사용자가 PDF Generator 서비스를 사용할 수 있도록 설정할 수 있습니다. 일반적으로 관리 권한이 있는 사용자만 서비스를 사용할 수 있습니다.

1. 환경 변수 PDFG_NON_ADMIN_ENABLED를 만듭니다.
1. 환경 변수의 값을 TRUE로 설정합니다.
1. AEM Forms 인스턴스를 다시 시작합니다.

>[!NOTE]
>
> SDK를 다시 시작하려면 &#39;Ctrl + C&#39; 명령을 사용하는 것이 좋습니다. Java 프로세스 중지와 같은 대체 방법을 사용하여 AEM SDK를 다시 시작하면 AEM 개발 환경이 일치하지 않을 수 있습니다.

### (Windows만 해당) 사용자 계정 컨트롤(UAC) 비활성화 {#disable-user-account-control-uac}

1. 시스템 구성 유틸리티에 액세스하려면 **[!UICONTROL 시작 > 실행]** 입력한 다음 **[!UICONTROL MSCONFIG]**.
1. 다음을 클릭합니다. **[!UICONTROL 도구]** 탭을 누르고 아래로 스크롤한 다음 선택 **[!UICONTROL UAC 설정 변경]**. 클릭 **[!UICONTROL 시작]** 새 창에서 명령을 실행합니다.
1. 슬라이더를 알림 안 함 레벨로 조정합니다. 완료되면 명령 창을 닫고 시스템 구성 창을 닫습니다.
1. UAC에 대한 레지스트리 설정이 0으로 설정되어 있는지 확인하십시오. 다음 단계를 수행하여 확인합니다.

   1. Microsoft®는 레지스트리를 수정하기 전에 백업하는 것을 권장합니다. 자세한 단계는 를 참조하십시오. [Windows에서 레지스트리를 백업 및 복원하는 방법](https://support.microsoft.com/en-us/help/322756).
   1. Microsoft® Windows 레지스트리 편집기를 엽니다. 레지스트리 편집기를 열려면 시작 > 실행으로 이동하고 regedit 를 입력한 다음 확인 을 클릭합니다.
   1. 다음으로 이동 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`. EnableLUA 값이 0으로 설정되어 있는지 확인합니다.
   1. 값 확인 **EnableLUA** 0으로 설정되어 있습니다. 값이 0이 아니면 값을 0으로 변경합니다. 레지스트리 편집기를 닫습니다.

1. 컴퓨터를 다시 시작합니다.

### (Windows만 해당) 오류 보고 서비스 비활성화 {#disable-error-reporting-service}

Windows Server에서 PDF Generator 서비스를 사용하여 문서를 PDF으로 변환하는 동안 Windows Server에서 실행 파일에 문제가 발생하여 닫아야 한다고 보고하는 경우가 있습니다. 하지만 백그라운드에서 계속되므로 PDF 전환에는 영향을 주지 않습니다.

오류를 수신하지 않도록 Windows 오류 보고를 비활성화할 수 있습니다. 오류 보고 비활성화에 대한 자세한 내용은 [https://technet.microsoft.com/en-us/library/cc754364.aspx](https://technet.microsoft.com/en-us/library/cc754364.aspx).

### (Windows만 해당) HTML에서 PDF 전환으로 구성 {#configure-html-to-pdf-conversion}

PDF Generator 서비스는 HTML 파일을 PDF 문서로 변환하는 WebKit, WebCapture 및 PhantomJS 경로 또는 메서드를 제공합니다. Windows에서 WebKit 및 Acrobat WebCapture 경로에 대한 변환을 활성화하려면 유니코드 글꼴을 %windir%\fonts 디렉터리에 복사합니다.

>[!NOTE]
>
>fonts 폴더에 새 글꼴을 설치할 때마다 AEM Forms 인스턴스를 다시 시작합니다.

### (UNIX 기반 플랫폼만 해당) HTML-PDF 변환을 위한 추가 구성  {#extra-configurations-for-html-to-pdf-conversion}

UNIX 기반 플랫폼에서 PDF Generator 서비스는 HTML 파일을 PDF 문서로 변환하기 위한 WebKit 및 PhantomJS 경로를 지원합니다. HTML-PDF 변환을 활성화하려면 원하는 변환 경로에 적용할 수 있는 다음 구성을 수행합니다.

### (UNIX 기반 플랫폼만 해당) 유니코드 글꼴 지원 활성화(WebKit만 해당) {#enable-support-for-unicode-fonts-webkit-only}

유니코드 글꼴을 시스템에 적합한 다음 디렉토리에 복사합니다.

* /usr/lib/X11/fonts/TrueType
* /usr/share/fonts/default/TrueType
* /usr/X11R6/lib/X11/fonts/ttf
* /usr/X11R6/lib/X11/fonts/truetype
* /usr/X11R6/lib/X11/fonts/TrueType
* /usr/X11R6/lib/X11/fonts/TTF
* /usr/openwin/lib/X11/fonts/TrueType (Solaris™)

>[!NOTE]
>
>* Red Hat® Enterprise Linux® 6.x 이상에서는 courier 글꼴을 사용할 수 없습니다. courier 글꼴을 설치하려면 font-ibm-type1-1.0.3.zip 아카이브를 다운로드합니다. /usr/share/fonts에서 아카이브를 추출합니다. /usr/share/X11/fonts에서 /usr/share/fonts로 심볼 링크를 만듭니다.
>* Html2PdfSvc/bin 및 /usr/share/fonts 디렉토리에서 모든 .lst 글꼴 캐시 파일을 삭제합니다.
>* /usr/lib/X11/fonts 디렉토리와 /usr/share/fonts 디렉토리가 있는지 확인합니다. 디렉토리가 없으면 ln 명령을 사용하여 /usr/share/X11/fonts에서 /usr/lib/X11/fonts로 심볼 링크를 생성하고 /usr/share/fonts에서 /usr/share/X11/fonts로 심볼 링크를 생성합니다. 또한 courier 글꼴이 /usr/lib/X11/fonts에서 사용 가능한지 확인하십시오.
>* /usr/share/fonts 또는 /usr/share/X11/fonts 디렉토리에서 유니코드와 비유니코드를 모두 사용할 수 있는지 확인합니다.
>* 루트가 아닌 사용자로 PDF Generator 서비스를 실행할 때 루트가 아닌 사용자에게 모든 글꼴 디렉터리에 대한 읽기 및 쓰기 액세스 권한을 제공합니다.
>* fonts 폴더에 새 글꼴을 설치할 때마다 AEM Forms 인스턴스를 다시 시작합니다.
>

## AEM Forms 추가 기능 패키지 설치 {#install-aem-forms-add-on-package}

AEM Forms 추가 기능 패키지는 AEM에 배포된 애플리케이션입니다. 이 패키지에는 AEM Forms 문서 서비스 및 기타 AEM Forms 기능이 포함되어 있습니다. 패키지를 설치하려면 다음 단계를 수행하십시오.

1. [소프트웨어 배포](https://experience.adobe.com/downloads)를 엽니다. 소프트웨어 배포에 로그인하려면 Adobe ID가 필요합니다.
1. 선택 **[!UICONTROL Adobe Experience Manager]** 헤더 메뉴에서 사용할 수 있습니다.
1. 다음에서 **[!UICONTROL 필터]** 섹션:
   1. 선택 **[!UICONTROL Forms]** 다음에서 **[!UICONTROL 솔루션]** 드롭다운 목록입니다.
   2. 패키지의 버전 및 유형을 선택합니다. 다음을 사용할 수도 있습니다 **[!UICONTROL 다운로드 검색]** 옵션을 사용하여 결과를 필터링할 수 있습니다.
1. 운영 체제에 적용할 수 있는 패키지 이름을 선택하고 **[!UICONTROL EULA 약관 동의]**, 및 선택 **[!UICONTROL 다운로드]**.
1. 열기 [패키지 관리자](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)  및 클릭 **[!UICONTROL 패키지 업로드]** 패키지를 업로드합니다.
1. 패키지를 선택하고 **[!UICONTROL 설치]**&#x200B;를 클릭합니다.

   에 나열된 직접 링크를 통해 패키지를 다운로드할 수도 있습니다. [AEM Forms 릴리스](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 기사.

1. 패키지를 설치한 후 AEM 인스턴스를 다시 시작하라는 메시지가 표시됩니다. **서버를 즉시 중지하지 마십시오.** AEM Forms 서버를 중지하기 전에 ServiceEvent REGISTERED 및 ServiceEvent UNREGISTERED 메시지가 `[AEM-Installation-Directory]/crx-quickstart/logs/error`.log 파일 및 로그가 안정적입니다.

## 설치 후 구성 {#post-installation-configurations}

### RSA/BouncyCastle 라이브러리에 대한 부트 위임 구성  {#configure-boot-delegation-for-rsa-bouncycastle-libraries}

1. AEM 인스턴스를 중지합니다. 다음 위치로 이동 [AEM 설치 디렉토리]\crx-quickstart\conf\ 폴더. 편집할 sling.properties 파일을 엽니다.

   를 사용하는 경우 `[AEM installation directory]\crx-quickstart\bin\start.bat` AEM 인스턴스를 시작하려면에 있는 sling.properties를 편집합니다. `[AEM_root]\crx-quickstart\`.

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

1. 에 로그인 [AEM 구성 관리자](http://localhost:4502/system/console/configMgr) 관리자입니다.
1. 을(를) 찾아 엽니다. **[!UICONTROL CQ-DAM-Handler-Gibson 글꼴 관리자]** 서비스. 시스템 글꼴, Adobe 서버 글꼴 및 고객 글꼴 디렉토리의 경로를 지정합니다. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

   >[!NOTE]
   >
   >Adobe 이외의 당사자가 제공한 글꼴을 사용할 권리는 해당 글꼴과 함께 그러한 당사자가 제공한 라이선스 계약에 의해 적용되며, Adobe 소프트웨어 사용 라이선스에 따라 적용되지 않습니다. Adobe은 특히 서버 환경에서의 Adobe 사용에 관하여 Adobe 소프트웨어에서 비 Adobe 글꼴을 사용하기 전에 적용 가능한 모든 비 라이선스 계약을 검토하고 준수하는지 확인할 것을 권장합니다.
   >fonts 폴더에 새 글꼴을 설치하면 AEM Forms 인스턴스를 다시 시작합니다.
   >

### PDF Generator 서비스를 실행하도록 로컬 사용자 계정 구성  {#configure-a-local-user-account-to-run-the-pdf-generator-service}

PDF Generator 서비스를 실행하려면 로컬 사용자 계정이 필요합니다. 로컬 사용자를 만드는 단계는 [Windows에서 사용자 계정 만들기](https://support.microsoft.com/en-us/help/13951/windows-create-user-account) 또는 UNIX 기반 플랫폼에서 사용자 계정을 만들 수 있습니다.

1. 를 엽니다. [AEM Forms PDF Generator 구성](http://localhost:4502/libs/fd/pdfg/config/ui.html) 페이지를 가리키도록 업데이트하는 중입니다.

1. 다음에서 **[!UICONTROL 사용자 계정]** 탭에서 로컬 사용자 계정의 자격 증명을 제공하고 **[!UICONTROL 제출]**. Microsoft® Windows에 메시지가 표시되면 사용자에 대한 액세스를 허용합니다. 성공적으로 추가되면 구성된 사용자가 **[!UICONTROL 사용자 계정]** 의 섹션 **[!UICONTROL 사용자 계정]** 탭.

### 시간 초과 설정 구성 {#configure-the-time-out-settings}

1. 위치 [AEM 구성 관리자](http://localhost:4502/system/console/configMgr)를 찾아 엽니다. **[!UICONTROL Jacorb ORB 공급자]** 서비스.

   다음에 추가 **[!UICONTROL 사용자 지정 속성.이름]** 필드 및 클릭 **[!UICONTROL 저장]**. 보류 중인 응답 시간 제한(CORBA 클라이언트 시간 제한이라고도 함)을 600초로 설정합니다.

   `jacorb.connection.client.pending_reply_timeout=600000`

1. AEM 작성자 인스턴스에 로그인하고 다음으로 이동합니다. **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 도구]** > **[!UICONTROL Forms]** > **[!UICONTROL 구성 PDF Generator]**. 기본 URL은 <http://localhost:4502/libs/fd/pdfg/config/ui.html>.

   를 엽니다. **[!UICONTROL 일반 구성]** 을(를) 탭하고 환경에 대해 다음 필드의 값을 수정합니다.

<table>
 <tbody>
  <tr>
   <td>필드</td>
   <td>설명</td>
   <td>기본 값</td>
  </tr>
  <tr>
   <td>서버 변환 시간 제한</td>
   <td>PDFG 변환은 서버 변환 시간 초과에 정의된 시간(초) 동안 활성 상태로 유지됩니다</td>
   <td>270초<br /> </td>
  </tr>
  <tr>
   <td>PDFG 정리 스캔(초)</td>
   <td>전환 후 작업을 수행하는 데 필요한 시간(초)입니다.<br /> </td>
   <td>3600초</td>
  </tr>
  <tr>
   <td>작업 만료 초</td>
   <td>PDF Generator 서비스에서 변환을 실행할 수 있는 기간입니다. 작업 만료 초 값이 PDFG 정리 스캔 초 값보다 큰지 확인합니다.</td>
   <td>7200초</td>
  </tr>
 </tbody>
</table>

### (Windows만 해당) PDF Generator 서비스를 위한 Acrobat 구성 {#configure-acrobat-for-the-pdf-generator-service}

Microsoft® Windows에서 PDF Generator 서비스는 Adobe Acrobat을 사용하여 지원되는 파일 형식을 PDF 문서로 변환합니다. PDF Generator 서비스를 위한 Adobe Acrobat을 구성하려면 다음 단계를 수행하십시오.

1. Acrobat을 열고 다음을 선택합니다. **[!UICONTROL 편집]**> **[!UICONTROL 환경 설정]**> **[!UICONTROL Updater]**. 업데이트 확인에서 선택을 취소합니다 **[!UICONTROL 업데이트 자동 설치]**, 및 클릭 **[!UICONTROL 확인]**. Acrobat을 닫습니다.
1. 시스템에서 PDF 문서를 두 번 클릭합니다. Acrobat이 처음 시작되면 로그인, 시작 화면 및 EULA에 대한 대화 상자가 나타납니다. PDF Generator을 사용하도록 구성된 모든 사용자에 대해 이 대화 상자를 닫습니다.
1. PDF Generator 유틸리티 배치 파일을 실행하여 PDF Generator 서비스에 대해 Acrobat을 구성합니다.

   1. 열기 [AEM 패키지 관리자](http://localhost:4502/crx/packmgr/index.jsp) 및 다운로드 `adobe-aemfd-pdfg-common-pkg-[version].zip` 패키지 관리자에서 파일을 가져옵니다.
   1. 다운로드한 .zip 파일의 압축을 해제합니다. 관리자 권한으로 명령 프롬프트를 엽니다.
   1. 다음 위치로 이동 `[extracted-zip-file]\jcr_root\etc\packages\day\cq60\fd\adobe-aemds-common-pkg-[version]\jcr_root\etc\packages\day\cq60\fd\`
   1. 압축 풀기 `adobe-aemfd-pdfg-common-pkg-[version]`.
   1. 다음 위치로 이동 `[downloaded-adobe-aemfd-pdfg-common-pkg]\jcr_root\libs\fd\pdfg\tools\adobe-aemfd-pdfg-utilities-[version]` 디렉토리. 다음 배치 파일을 실행합니다.

      `Acrobat_for_PDFG_Configuration.bat`

      Acrobat은 PDF Generator 서비스로 실행되도록 구성되어 있습니다.

1. 실행 [시스템 준비 도구(SRT)](#SRT) Acrobat 설치 여부를 확인합니다.

### (Windows만 해당) HTML-PDF 변환을 위한 기본 경로 구성 {#configure-primary-route-for-html-to-pdf-conversion-windows-only}

PDF Generator 서비스는 HTML 파일을 PDF 문서로 변환하는 여러 경로(Webkit, Acrobat WebCapture(Windows에만 해당) 및 PhantomJS)를 제공합니다. Adobe은 동적 콘텐츠를 처리할 수 있고 32비트 라이브러리에 대한 종속성이 없거나 추가 글꼴이 필요 없으므로 PhantomJS 라우트를 사용하는 것이 좋습니다. 또한 PhantomJS 경로는 변환을 실행하기 위해 sudo 또는 root 액세스가 필요하지 않습니다.

HTML-PDF 전환의 기본 기본 기본 경로는 Webkit입니다. 변환 경로를 변경하려면:

1. AEM 작성자 인스턴스에서 **[!UICONTROL 도구]**> **[!UICONTROL Forms]**> **[!UICONTROL 구성 PDF Generator]**.

1. 다음에서 **[!UICONTROL 일반 구성]** 탭에서 원하는 변환 경로를 선택합니다. **[!UICONTROL HTML에서 PDF 전환에 대한 기본 경로]** 드롭다운.

### 글로벌 Trust Store 초기화 {#intialize-global-trust-store}

Trust Store Management를 사용하면 디지털 서명 및 인증서 인증의 유효성 검사를 위해 서버에서 신뢰할 수 있는 인증서를 가져오고 편집하고 삭제할 수 있습니다. 여러 인증서를 가져오고 내보낼 수 있습니다. 인증서를 가져온 후에는 트러스트 설정 및 트러스트 저장소 유형을 편집할 수 있습니다. Trust Store를 초기화하려면 다음 단계를 수행하십시오.

1. 관리자로 AEM Forms 인스턴스에 로그인합니다.
1. 다음으로 이동  **[!UICONTROL 도구]** >  **[!UICONTROL 보안]** >  **[!UICONTROL Trust Store]**.
1. 클릭  **[!UICONTROL TrustStore 만들기]**. 암호 설정 및 선택 **[!UICONTROL 저장]**.

### Reader 확장 및 암호화 서비스에 대한 인증서 설정 {#set-up-certificates-for-reader-extension-and-encryption-service}

DocAssurance 서비스는 PDF 문서에 사용 권한을 적용할 수 있습니다. PDF 문서에 사용 권한을 적용하려면 인증서를 구성합니다.

인증서를 설정하기 전에 다음을 확인하십시오.

* 인증서 파일(.pfx).

* 인증서와 함께 제공된 개인 키 암호.

* 개인 키 별칭. Java keytool 명령을 실행하여 개인 키 별칭을 볼 수 있습니다.
  `keytool -list -v -keystore [keystore-file] -storetype pkcs12`

* 키 저장소 파일 암호입니다. Adobe의 Reader 확장 인증서를 사용하는 경우 Keystore 파일 암호는 항상 개인 키 암호와 동일합니다.

인증서를 구성하려면 다음 단계를 수행하십시오.

1. 관리자로 AEM 작성자 인스턴스에 로그인합니다. 다음으로 이동 **[!UICONTROL 도구]** > **[!UICONTROL 보안]** > **[!UICONTROL 사용자]**.
1. 다음을 클릭합니다. **[!UICONTROL 이름]** 사용자 계정의 필드입니다. 다음 **[!UICONTROL 사용자 설정 편집]** 페이지가 열립니다. AEM 작성자 인스턴스에서 인증서는 KeyStore에 있습니다. 이전에 KeyStore를 만들지 않은 경우 **[!UICONTROL KeyStore 만들기]** 및 KeyStore에 대한 새 암호를 설정합니다. 서버에 이미 KeyStore가 있는 경우 이 단계를 건너뜁니다.  Adobe의 Reader 확장 인증서를 사용하는 경우 Keystore 파일 암호는 항상 개인 키 암호와 동일합니다.
1. 다음에서 **[!UICONTROL 사용자 설정 편집]** 페이지에서 **[!UICONTROL KeyStore]** 탭. 확장 **[!UICONTROL 키 저장소 파일의 개인 키 추가]** 을 선택하고 별칭을 제공합니다. 별칭은 Reader 확장 작업을 수행하는 데 사용됩니다.
1. 인증서 파일을 업로드하려면 **[!UICONTROL 키 저장소 파일 선택]** 및 업로드 &lt;filename>.pfx 파일.

   추가 **[!UICONTROL 키 저장소 암호]**, **[!UICONTROL 개인 키 암호]**, 및 **[!UICONTROL 개인 키 별칭]** 인증서와 각 필드에 연결됩니다. **[!UICONTROL 제출]**&#x200B;을 클릭합니다.

   >[!NOTE]
   >
   >프로덕션 환경에서 평가 자격 증명을 프로덕션 자격 증명으로 바꿉니다. 만료 또는 평가 자격 증명을 업데이트하기 전에 이전 Reader 확장 자격 증명을 삭제해야 합니다.

1. 클릭 **[!UICONTROL 저장 및 닫기]** 다음에 있음 **[!UICONTROL 사용자 설정 편집]** 페이지를 가리키도록 업데이트하는 중입니다.

### AES-256 활성화 {#enable-aes}

PDF 파일에 AES 256 암호화를 사용하려면 JCE(Java Cryptography Extension) 무제한 강도 관할 정책 파일을 가져와 설치하십시오. jre/lib/security 폴더에서 local_policy.jar 및 US_export_policy.jar 파일을 바꿉니다. 예를 들어 Sun JDK를 사용하는 경우 다운로드한 파일을 `[JAVA_HOME]/jre/lib/security` 폴더를 삭제합니다.

어셈블러 서비스는 Reader 확장 서비스, 서명 서비스, Forms 서비스 및 출력 서비스에 따라 다릅니다. 다음 단계를 수행하여 필요한 서비스가 실행 중인지 확인합니다.

1. URL에 로그인 `https://'[server]:[port]'/system/console/bundles` 관리자입니다.
1. 다음 서비스를 검색하고 서비스가 실행 중인지 확인하십시오.

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

### (Windows만 해당) Microsoft® 프로젝트에 대한 레지스트리 항목 구성 {#configure-registry-entry-for-microsoft-project}

시스템에 AEM Forms 추가 기능 및 Microsoft® 프로젝트를 설치한 후 64비트 위치에서 Microsoft® 프로젝트에 대한 항목을 등록합니다. 이를 통해 프로젝트-PDFG 전환 테스트 실행을 용이하게 합니다. 다음은 레지스트리 항목 프로세스에 대한 개요입니다.

1. Microsoft® Windows 레지스트리 편집기(regedit)를 열고 레지스트리 편집기를 열려면 시작 > 실행으로 이동하고 regedit를 입력한 다음 확인 을 클릭합니다.
1. 다음으로 이동 `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Adobe\Acrobat PDFMaker\<version>\Office\SupportedApp`및 새로 만들기 **이진 값** 레지스트리 및 이름 바꾸기 **프로젝트**.
1. 작성된 이진 레지스트리의 데이터 값을 01로 수정하고 [확인]을 클릭합니다.
1. 레지스트리 항목을 닫습니다.


## 알려진 문제 및 문제 해결 {#known-issues-and-troubleshooting}

* 압축된 입력 파일에 파일 이름에 2바이트 문자가 있는 HTML 파일이 포함된 경우 HTML-PDF 변환이 실패합니다. 이 문제를 방지하려면 HTML 파일 이름을 지정할 때 더블바이트 문자를 사용하지 마십시오.

* UNIX 기반 운영 체제에서는 누락된 라이브러리를 찾으려면 다음을 수행합니다.

1. 다음으로 이동 `[crx-repository]/bedrock/svcnative/HtmlToPdfSvc/bin/`.

1. 다음 명령을 실행하여 PhantomJS에서 HTML으로 PDF 전환하는 데 필요한 모든 라이브러리를 나열합니다.

   `ldd phantomjs`

   다음 명령을 실행하여 누락된 라이브러리를 나열합니다.

   `ldd phantomjs | grep not`

1. 누락된 라이브러리를 수동으로 설치합니다.

## 시스템 준비 도구(SRT) {#SRT}

다음 [시스템 준비 도구](#srt-configuration) 시스템이 PDF Generator 전환을 실행하도록 올바르게 구성되었는지 확인합니다. 이 도구는 지정된 경로에서 보고서를 생성합니다. 도구를 실행하려면:

1. 명령 프롬프트를 엽니다. `[extracted-adobe-aemfd-pdfg-common-pkg]\jcr_root\libs\fd\pdfg\tools` 폴더로 이동합니다.

1. 명령 프롬프트에서 다음 명령을 실행합니다.

   `java -jar forms-srt-[version].jar [Path_of_reports_folder] en`

   이 명령은 보고서를 생성하고 srt_config.yaml 파일도 생성합니다. 이 옵션을 사용하여 SRT 도구에 대한 옵션을 구성할 수 있습니다. SRT 도구에 대한 옵션을 구성하는 것은 선택 사항입니다.

   >[!NOTE]
   >
   >* 시스템 준비 도구에서 pdfgen.api 파일을 Acrobat 플러그인 폴더에서 사용할 수 없다고 보고하면 `[extracted-adobe-aemfd-pdfg-common-pkg]\jcr_root\libs\fd\pdfg\tools\adobe-aemfd-pdfg-utilities-[version]\plugins\x86_win32` 디렉토리 대상: `[Acrobat_root]\Acrobat\plug_ins` 디렉토리.

1. 다음으로 이동 `[Path_of_reports_folder]`. SystemReadinessTool.html 파일을 엽니다. 보고서를 확인하고 언급된 문제를 해결합니다.

### SRT 도구에 대한 옵션 구성 {#srt-configuration}

srt_config.yaml 파일을 사용하여 SRT 도구에 대한 다양한 설정을 구성할 수 있습니다. 파일 형식은 다음과 같습니다.

```shell
   # =================================================================
   # SRT Configuration
   # =================================================================
   #Note - follow correct format to avoid parsing failures
   #for example, <param name>:<space><param value> 
   #locale: (mandatory field)Locale to be used for SRT. Supported locales [en/fr/de/ja].
   locale: en
   
   #aemTempDir: AEM Temp direcotry
   aemTempDir:
   
   #users: provide PDFG converting users list
   #users:
   # - user1
   # - user2
   users:
   
   #profile: select profile to run specific checks. Choose from [LCM], more will be added soon 
   profile:
   
   #outputDir: directory where output files will be saved
   outputDir:
```

* **로케일:** 필수 매개 변수입니다. 영어(en), 독일어(de), 프랑스어(fr) 및 일본어(ja)를 지원합니다. 기본값은 en입니다. OSGi의 AEM Forms에서 실행되는 PDF Generator 서비스에는 영향을 주지 않습니다.
* **aemTempDir:** 선택적 매개 변수입니다. Adobe Experience Manager의 임시 저장소 위치를 지정합니다.
* **사용자:** 선택적 매개 변수입니다. 사용자에게 PDF Generator을 실행하는 데 필요한 디렉터리에 대한 읽기/쓰기 권한과 필요한 권한이 있는지 확인할 사용자를 지정할 수 있습니다. 사용자를 지정하지 않으면 사용자별 검사를 건너뛰고 보고서에 실패로 표시됩니다.
* **outputDir:** SRT 보고서를 저장할 위치를 지정합니다. 기본 위치는 SRT 도구의 현재 작업 디렉토리입니다.

## 문제 해결

SRT 도구에서 보고한 모든 문제를 해결한 후에도 문제가 발생하면 다음 검사를 수행하십시오.

다음 검사를 수행하기 전에 다음을 확인하십시오 [시스템 준비 도구](#SRT) 오류를 보고하지 않습니다.

+++ Adobe Acrobat

* 확인만 [지원되는 버전](aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator) Microsoft® Office(32비트) 및 Adobe Acrobat이 설치되고 대화 상자 열기가 취소됩니다.
* Adobe Acrobat 업데이트 서비스가 비활성화되어 있는지 확인합니다.
* 다음을 확인합니다. [Acrobat_for_PDFG_Configuration.bat](#configure-acrobat-for-the-pdf-generator-service) 배치 파일이 관리자 권한으로 실행되었습니다.
* PDF 구성 UI에 PDF Generator 사용자가 추가되었는지 확인합니다.
* 다음을 확인합니다. [프로세스 수준 토큰 바꾸기](#grant-the-replace-a-process-level-token-privilege) PDF Generator 사용자에 대한 권한이 추가됩니다.
* Microsoft Office 애플리케이션에 Acrobat PDFMaker Office COM 추가 기능을 사용할 수 있는지 확인합니다.

+++

+++오픈오피스

**Microsoft® Windows**

* 32비트 [지원되는 버전](aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator) 의 Microsoft Office가 설치되고 모든 애플리케이션에 대한 대화 상자 열기가 취소되었습니다.
* PDF 구성 UI에 PDF Generator 사용자가 추가되었는지 확인합니다.
* PDF Generator 사용자가 관리자 그룹의 구성원인지 확인하고 [프로세스 수준 토큰 바꾸기](#grant-the-replace-a-process-level-token-privilege) 사용자에 대한 권한이 설정됩니다.
* 사용자가 PDF Generator UI에 구성되어 있고 다음 작업을 수행하는지 확인합니다.
   1. PDF Generator 사용자로 Microsoft® Windows에 로그인합니다.
   1. Microsoft® Office 또는 OpenOffice 애플리케이션을 열고 모든 대화 상자를 취소합니다.
   1. AdobePDF를 기본 프린터로 설정합니다.
   1. Acrobat을 PDF 파일의 기본 프로그램으로 설정합니다.
   1. Microsoft Office 애플리케이션에서 파일 > 인쇄 및 Acrobat 리본 옵션을 사용하여 수동 변환을 수행하고 모든 대화 상자를 취소합니다.
   1. winword.exe, powerpoint.exe 및 excel.exe와 같은 변환과 관련된 모든 프로세스를 종료합니다.
   1. AEM Forms 서버를 다시 시작합니다.

**Linux®**

* 설치 [지원되는 버전](aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator) 오픈오피스 AEM Forms은 32비트 및 64비트 버전을 모두 지원합니다. 설치 후 모든 OpenOffice 응용 프로그램을 열고 대화 상자 창을 모두 취소한 다음 응용 프로그램을 닫습니다. 응용 프로그램을 다시 열고 OpenOffice 응용 프로그램을 열 때 대화 상자가 표시되지 않도록 합니다.

* 환경 변수 만들기 `OpenOffice_PATH` 및 를 설정하는 대신 OpenOffice 설치가 [콘솔](https://linuxize.com/post/how-to-set-and-list-environment-variables-in-linux/) 또는 dt (Device Tree) 프로파일
* OpenOffice를 설치하는 데 문제가 있는 경우 [32비트 라이브러리](#extrarequirements) OpenOffice 설치에 필요합니다.

+++

+++HTML-PDF 전환 문제

* PDF Generator 구성 UI에 글꼴 디렉터리가 추가되었는지 확인합니다.

**Linux 및 Solaris(PhantomJS 변환 경로)**

* Webkit 기반 HTMLToPDF 변환에 32비트 라이브러리(libicudata.so.42)를 사용할 수 있고 PhantomJS 기반 HTMLToPDF 변환에 64비트 라이브러리(libicudata.so.42 lib)를 사용할 수 있는지 확인합니다.

* 다음 명령을 실행하여 phantomjs에 대해 누락된 라이브러리를 나열합니다.

  ```
  ldd phantomjs | grep not
  ```

**Linux® 및 Solaris™(WebKit 전환 경로)**

* 디렉터리가 `/usr/lib/X11/fonts` 및 `/usr/share/fonts` 존재합니다. 디렉터리가 없는 경우 다음 위치에서 심볼 링크를 만듭니다. `/usr/share/X11/fonts` 끝 `/usr/lib/X11/fonts` 및 의 또 다른 심볼 링크 `/usr/share/fonts` 끝 `/usr/share/X11/fonts`.

  ```
  ln -s /usr/share/fonts /usr/share/X11/fonts
  
  ln -s /usr/share/X11/fonts /usr/lib/X11/fonts
  ```

* IBM 글꼴이 usr/share/fonts 아래에 복사되었는지 확인합니다.
* 컴퓨터에서 유령 취약성 수정 glibc를 사용할 수 있는지 확인합니다. 기본 패키지 관리자를 사용하여 최신 버전의 glibc로 업데이트합니다. 유령 취약성 수정 사항이 포함되어 있습니다.
* 최신 버전의 32비트 lib curl, libcrypto 및 libssl 라이브러리가 시스템에 설치되어 있는지 확인합니다. 심볼릭 링크 만들기 `/usr/lib/libcurl.so` (또는 libcurl.a for AIX®), `/usr/lib/libcrypto.so` (또는 AIX®용 libcrypto.a) 및 `/usr/lib/libssl.so` (또는 AIX®용 libssl.a) 각 라이브러리의 최신 버전(32비트)을 가리킵니다.

* IBM® SSL 소켓 공급자에 대해 다음 단계를 수행합니다.
   1. 에서 java.security 파일 복사 `<WAS_Installed_JAVA>\jre\lib\security` AEM Forms 서버의 모든 위치에 기본 위치는 기본 위치입니다 = `<WAS_Installed>\Appserver\java_[version]\jre\lib\security`.

   1. 복사된 위치에서 java.security 파일을 편집하고 기본 SSL 소켓 팩터리를 JSSE2 팩터리로 변경합니다(WebSphere® 대신 JSSE2 팩터리를 사용).

      다음 기본 JSSE 소켓 팩토리를 변경합니다.

      ```
      #ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
      #ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
      WebSphere socket factories (in cryptosf.jar)
      ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
      ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
      ```

      포함

      ```
      ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
      ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
      WebSphere socket factories (in cryptosf.jar)
      #ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
      #ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
      ```

+++

+++ PDF Generator(PDFG) 사용자를 추가할 수 없음

* Microsoft® Visual C++ 2012 x86 및 Microsoft® Visual C++ 2013 x86(32비트) 재배포 가능 패키지가 Windows에 설치되어 있는지 확인합니다.

+++

+++자동화 테스트 실패

* Microsoft® Office 및 OpenOffice의 경우 전환 중에 대화 상자가 나타나지 않도록 각 사용자별로 적어도 한 번 이상의 전환을 수동으로 수행하십시오. 대화 상자가 나타나면 해당 대화 상자를 닫습니다. 자동화된 변환 중에는 이러한 대화 상자가 나타나지 않아야 합니다.

* OSGi 환경의 AEM Forms에서 자동화를 실행하기 전에 테스트 패키지가 설치되고 활성 상태인지 확인하십시오.

+++

+++여러 사용자 전환 실패

* 서버 로그를 확인하여 특정 사용자에 대한 전환이 실패하는지 확인합니다.(프로세스 탐색기를 사용하여 다양한 사용자에 대한 실행 중인 프로세스를 확인할 수 있습니다.)

* PDF Generator에 대해 구성된 사용자에게 로컬 관리자 권한이 있는지 확인합니다.

* PDF Generator 사용자에게 LC 임시 사용자와 PDFG 임시 사용자에 대한 읽기, 쓰기 및 실행 권한이 있는지 확인합니다.

* Microsoft® Office 및 OpenOffice의 경우 전환 중에 대화 상자가 나타나지 않도록 각 사용자별로 적어도 한 번 이상의 전환을 수동으로 수행하십시오. 대화 상자가 나타나면 해당 대화 상자를 닫습니다. 자동화된 변환 중에는 이러한 대화 상자가 나타나지 않아야 합니다.

* 샘플 변환을 수행합니다.

+++

+++AEM Forms Server에 설치된 Adobe Acrobat 라이선스 만료

* Adobe Acrobat의 기존 라이센스가 있고 만료된 경우 [최신 버전의 Adobe Application Manager 다운로드](https://helpx.adobe.com/in/creative-suite/kb/aam-troubleshoot-download-install.html), 및 일련 번호 마이그레이션 다음 이전 [시리얼 번호 마이그레이션](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number).

   * 다음 명령을 사용하여 prov.xml을 생성하고 여기에 제공된 명령 대신 prov.xml 파일을 사용하여 기존 설치를 예약합니다 [시리얼 번호 마이그레이션](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number) 번호 문서.

         &quot;
         
         adobe_prtk —tool=VolumeSerialize —generate —serial=&lt;serialnum> [—leid=&lt;leid>] [—regsuppress=ss] [—eulasuppress] [—locales=limited list of locales in xx_XX format or ALL>] [—provfile=&lt;absolute path=&quot;&quot; to=&quot;&quot; prov.xml=&quot;&quot;>]
         
         &quot;
     
   * 볼륨 패키지 직렬화(prov.xml 파일 및 새 일련번호를 사용하여 기존 설치를 다시 직렬화): PRTK 설치 폴더에서 다음 명령을 관리자로 실행하여 클라이언트 컴퓨터에서 배포된 패키지를 직렬화하고 활성화합니다.

         &quot;
         adobe_prtk —tool=VolumeSerialize —provfile=C:\prov.xml -stream
         
         &quot;
     
* 대규모 설치의 경우 [Acrobat Customization Wizard](https://www.adobe.com/devnet-docs/acrobatetk/tools/Wizard/index.html) 이전 버전의 Reader 및 Acrobat을 제거합니다. 설치 관리자를 사용자 지정하고 조직의 모든 컴퓨터에 배포합니다.

+++

+++ AEM Forms Server는 오프라인 또는 보안 환경에 있으며, 인터넷을 사용하여 Acrobat을 활성화할 수 없습니다.

* Adobe 제품을 처음 출시한 후 7일 이내에 온라인으로 전환하여 온라인 활성화 및 등록을 완료하거나 인터넷 지원 장치와 제품 일련 번호를 사용하여 이 프로세스를 완료할 수 있습니다. 자세한 지침은 [오프라인 활성화](https://exception.licenses.adobe.com/aoes/aoes/v1/t1?locale=en).

+++

+++ Windows Server에서 Word 또는 Excel 파일을 PDF으로 변환할 수 없음

사용자가 Microsoft Windows Server에서 Word 또는 Excel 파일을 PDF으로 변환하려고 할 때 다음과 같은 오류가 발생합니다.

*기본 변환기의 오류 메시지: ALC-PDG-015-003-시스템이 입력 파일을 열 수 없습니다. 파일을 다시 제출하거나 시스템 관리자에게 문의하십시오.*

문제를 해결하려면 다음을 참조하십시오. [Windows Server에서 Word 또는 Excel 파일을 PDF으로 변환할 수 없음](/help/forms/using/disable-uac-for-pdfgconfiguration.md).

+++

+++ Windows Server 2019에서 Excel 파일을 PDF으로 변환할 수 없습니다.

Microsoft Excel 2019를 Microsoft Windows Server 2019에서 PDF으로 변환할 때 다음을 확인해야 합니다.

* PDF Generator 서비스를 사용하는 동안 Windows 컴퓨터에 AEM 서버(Windows RDP 세션)와 활성 원격 연결이 없어야 합니다.
* 기본 프린터를 Adobe PDF으로 설정해야 합니다.

  >[!NOTE]
  >* Apple macOS 및 Ubuntu OS의 경우, 위의 설정을 구성할 필요가 없습니다.

+++

+++ XPS 파일을 PDF으로 변환할 수 없음

문제를 해결하려면 [windows에서 기능별 레지스트리 키 만들기](https://helpx.adobe.com/in/acrobat/kb/unable-convert-xps-to-pdfs.html).

+++


## 다음 단계 {#next-steps}

AEM Forms 문서 서비스 환경이 작동하고 있습니다. 다음을 통해 문서 서비스를 사용할 수 있습니다.

* [OSGi의 양식 중심 워크플로](/help/forms/using/aem-forms-workflow.md)
* [감시 폴더](/help/forms/using/watched-folder-in-aem-forms.md)
* [문서 서비스 API](/help/forms/using/aem-document-services-programmatically.md)
