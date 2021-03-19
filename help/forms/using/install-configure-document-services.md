---
title: 문서 서비스 설치 및 구성
seo-title: 문서 서비스 설치 및 구성
description: AEM Forms 다큐멘트 서비스를 설치하여 PDF 문서를 작성, 조합, 배포, 보관하고 디지털 서명을 추가하여 문서에 대한 액세스를 제한하고 바코드 양식을 디코딩할 수 있습니다.
seo-description: AEM Forms 다큐멘트 서비스를 설치하여 PDF 문서를 작성, 조합, 배포, 보관하고 디지털 서명을 추가하여 문서에 대한 액세스를 제한하고 바코드 양식을 디코딩할 수 있습니다.
uuid: 908806a9-b0d4-42d3-9fe4-3eae44cf4326
topic-tags: installing
discoiquuid: b53eae8c-16ba-47e7-9421-7c33e141d268
role: 관리자
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '4296'
ht-degree: 3%

---


# 문서 서비스 {#installing-and-configuring-document-services} 설치 및 구성

AEM Forms은 PDF 문서를 작성, 조합, 배포 및 보관하는 서비스, 문서에 대한 액세스를 제한하는 디지털 서명 추가, 바코드 양식 디코딩과 같이 다양한 문서 수준 작업을 수행하는 다양한 OSGi 서비스를 제공합니다. 이러한 서비스는 AEM Forms Add-on 패키지에 포함되어 있습니다. 이러한 서비스를 문서 서비스라고 합니다. 사용 가능한 문서 서비스 및 주요 기능 목록은 다음과 같습니다.

* **Assembler 서비스:** PDF 및 XDP 문서를 결합, 재정렬 및 추가하고 PDF 문서에 대한 정보를 얻을 수 있습니다. 또한 PDF 문서를 PDF/A 표준으로 변환 및 확인할 수 있고 PDF forms, XML 양식 및 PDF forms을 PDF/A-1b, PDF/A-2b 및 PDFA/A-3b로 변환할 수 있습니다. 자세한 내용은 [어셈블러 서비스](/help/forms/using/assembler-service.md)를 참조하십시오.

* **ConvertPDF 서비스:** PDF 문서를 PostScript 또는 이미지 파일(JPEG, JPEG 2000, PNG 및 TIFF)로 변환할 수 있습니다. 자세한 내용은 [ConvertPDF 서비스](/help/forms/using/using-convertpdf-service.md)를 참조하십시오.

* **바코드 Forms 서비스:** 바코드의 전자 이미지에서 데이터를 추출할 수 있습니다. 이 서비스는 하나 이상의 바코드가 포함된 TIFF 및 PDF 파일을 입력으로 받아 바코드 데이터를 추출합니다. 자세한 내용은 [바코드 Forms 서비스](/help/forms/using/using-barcoded-forms-service.md)를 참조하십시오.

* **DocAssurance 서비스:** 문서를 암호화 및 해독하고, Adobe Reader의 기능을 사용 권한으로 확장하며 문서에 디지털 서명을 추가할 수 있습니다. 문서 보증 서비스에는 다음과 같은 세 가지 서비스가 있습니다.서명, 암호화 및 reader 확장 자세한 내용은 [DocAssurance 서비스](/help/forms/using/overview-aem-document-services.md)를 참조하십시오.

* **암호화 서비스:** 문서를 암호화하고 해독할 수 있습니다. 문서가 암호화되면 해당 내용이 읽을 수 없게 됩니다. 권한이 있는 사용자는 문서의 내용을 해독하여 액세스할 수 있습니다. 자세한 내용은 [암호화 서비스](/help/forms/using/overview-aem-document-services.md#encryption-service)를 참조하십시오.

* **Forms 서비스:** 일반적으로 Forms Designer에서 만든 양식을 확인하고 처리, 변환하고 전달하는 대화형 데이터 캡처 클라이언트 애플리케이션을 만들 수 있습니다. Forms 서비스는 사용자가 개발한 모든 양식 디자인을 PDF 문서로 렌더링합니다. 자세한 내용은 [Forms 서비스](/help/forms/using/forms-service.md)를 참조하십시오.

* **출력 서비스:** PDF, 레이저 프린터 포맷, 프린터 레이블 지정 등 다양한 형식의 문서를 만들 수 있습니다. 레이저 프린터 형식은 PostScript 및 프린터 제어 언어(PCL)입니다. 자세한 내용은 [출력 서비스](/help/forms/using/output-service.md)를 참조하십시오.

* **PDF Generator 서비스:** PDF Generator 서비스는 API를 제공하여 기본 파일 형식을 PDF로 변환합니다. 또한 PDF를 다른 파일 포맷으로 변환하고 PDF 문서의 크기를 최적화합니다. 자세한 내용은 [PDF Generator 서비스](aem-document-services-programmatically.md#pdfgeneratorservice)를 참조하십시오.

* **Reader 익스텐션 서비스:** 추가 사용 권한과 함께 Adobe Reader의 기능을 확장하여 대화형 PDF 문서를 쉽게 공유할 수 있습니다. 이 서비스는 Adobe Reader을 사용하여 PDF 문서를 열 때 사용할 수 없는 기능(예: 문서에 주석 추가, 양식 채우기, 문서 저장)을 활성화합니다. 자세한 내용은 [Reader 확장 서비스](/help/forms/using/overview-aem-document-services.md#reader-extension-service)를 참조하십시오.

* **서명 서비스:** AEM 서버에서 디지털 서명 및 문서를 사용하여 작업할 수 있습니다. 예를 들어 서명 서비스는 일반적으로 다음과 같은 경우에 사용됩니다.

   * AEM 서버는 Acrobat 또는 Adobe Reader을 사용하여 열도록 사용자에게 전송하기 전에 양식을 인증합니다.
   * AEM 서버는 Acrobat 또는 Adobe Reader을 사용하여 양식에 추가된 서명을 확인합니다.
   * AEM 서버는 공공증인을 대신하여 양식에 서명한다.

   서명 서비스는 신뢰 저장소에 저장된 인증서 및 자격 증명에 액세스합니다. 자세한 내용은 [서명 서비스](/help/forms/using/aem-document-services-programmatically.md)를 참조하십시오.

AEM Forms은 강력한 엔터프라이즈급 플랫폼이며 문서 서비스는 AEM Forms의 기능 중 하나에 불과합니다. 전체 기능 목록을 보려면 [AEM Forms 소개](/help/forms/using/introduction-aem-forms.md)을 참조하십시오.

## 배포 토폴로지 {#deployment-topology}

AEM Forms Add-on 패키지는 AEM에 배포되는 애플리케이션입니다. 일반적으로 AEM Forms 문서 서비스를 실행하려면 AEM 인스턴스(작성자 또는 게시)가 하나만 필요합니다. AEM Forms 문서 서비스를 실행하려면 다음 토폴로지가 권장됩니다. 토폴로지에 대한 자세한 내용은 [AEM Forms용 아키텍처 및 배포 토폴로지](/help/forms/using/aem-forms-architecture-deployment.md)를 참조하십시오.

![AEM Forms을 위한 아키텍처 및 배포 토폴로지](do-not-localize/document-services.png)

>[!NOTE]
>
>AEM Forms을 사용하면 단일 서버에서 모든 기능을 설정 및 실행할 수 있지만, 용량 계획, 로드 밸런싱 및 운영 환경의 특정 기능에 대한 전용 서버를 설정해야 합니다. 예를 들어 PDF Generator 서비스를 사용하여 하루에 수천 페이지를 변환하고 여러 적응형 양식을 사용하여 데이터를 캡처하는 환경의 경우 PDF Generator 서비스 및 적응형 양식 기능을 위해 별도의 AEM Forms 서버를 설정할 수 있습니다. 최적의 성능을 제공하고 서로 독립적으로 서버를 확장할 수 있습니다.

## 시스템 요구 사항 {#system-requirements}

AEM Forms 다큐멘트 서비스를 설치하고 구성하기 전에 다음 사항을 확인하십시오.

* 하드웨어 및 소프트웨어 인프라가 적절한 위치에 있습니다. 지원되는 하드웨어 및 소프트웨어에 대한 자세한 목록은 [기술 요구 사항](/help/sites-deploying/technical-requirements.md)을 참조하십시오.

* AEM 인스턴스의 설치 경로에 공백이 없습니다.
* AEM 인스턴스가 실행 중입니다. AEM 용어에서 &quot;인스턴스&quot;는 작성자 또는 게시 모드에서 서버에서 실행되는 AEM의 사본입니다. 일반적으로 AEM Forms 문서 서비스를 실행하려면 AEM 인스턴스(작성자 또는 게시)만 필요합니다.

   * **작성자**:컨텐츠를 만들고 업로드 및 편집하고 웹 사이트를 관리하는 데 사용되는 AEM 인스턴스입니다. 컨텐츠를 라이브할 준비가 되면 게시 인스턴스에 복제됩니다.
   * **게시**:인터넷 또는 내부 네트워크를 통해 게시된 컨텐츠를 일반 사용자에게 제공하는 AEM 인스턴스입니다.

* 메모리 요구 사항이 충족되었습니다. AEM Forms Add-on 패키지의 요구 사항:

   * Microsoft Windows 기반 설치를 위한 15GB의 임시 공간.
   * UNIX 기반 설치를 위한 6GB의 임시 공간.

* Microsoft Windows 및 Linux에서 PDF 생성기를 변환하기 위해 필요한 클라이언트 소프트웨어가 설치되어 있습니다.

   * **Microsoft Windows**:Microsoft  [Office ](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p)또는  [Apache OpenOffice 설치](/help/forms/using/aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator)
   * **Linux**:Apache  [OpenOffice 설치](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p)

>[!NOTE]
>
>* Microsoft Windows에서 PDF Generator는 WebKit, Acrobat WebCapture 및 PhantomJS 변환 경로를 지원하여 HTML 파일을 PDF 문서로 변환합니다.
>* UNIX 기반 운영 체제에서 PDF Generator는 WebKit 및 PhantomJS 변환 경로를 지원하여 HTML 파일을 PDF 문서로 변환합니다.

>



### UNIX 기반 운영 체제에 대한 추가 요구 사항 {#extrarequirements}

UNIX 기반 운영 체제를 사용하는 경우 해당 운영 체제의 설치 미디어에서 다음 패키지를 설치합니다.

<table> 
 <tbody> 
  <tr> 
   <td> 
    <ul> 
     <li>expat</li> 
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
     <li>글리시</li> 
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

* **(PDF Generator 전용**) 32비트 버전의 libcurl, libcrypto 및 libssl 라이브러리를 설치하고 아래 심볼을 만듭니다. symlinks는 각 라이브러리의 최신 버전을 가리킵니다.

   * /usr/lib/libcurl.so
   * /usr/lib/libcrypto.so
   * /usr/lib/libssl.so

* **(PDF Generator 전용)** PDF Generator 서비스는 HTML 파일을 PDF 문서로 변환하는 WebKit 및 PhantomJS 경로를 지원합니다. PhantomJS 경로에 대한 변환을 활성화하려면 아래 나열된 64비트 라이브러리를 설치하십시오. 일반적으로 이러한 라이브러리는 이미 설치되어 있습니다. 라이브러리가 없는 경우 수동으로 설치합니다.

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

사전 설치 구성 섹션에 나열된 구성은 PDF Generator 서비스에만 적용됩니다. PDF Generator 서비스를 구성하지 않으면 사전 설치 구성 섹션을 건너뛸 수 있습니다.

### Adobe Acrobat 및 타사 응용 프로그램 설치 {#install-adobe-acrobat-and-third-party-applications}

PDF Generator 서비스를 사용하여 Microsoft Word, Microsoft Excel, Microsoft PowerPoint, OpenOffice, WordPerfect X7 및 Adobe Acrobat과 같은 기본 파일 형식을 PDF 문서로 변환하는 경우 이러한 애플리케이션이 AEM Forms 서버에 설치되어 있는지 확인하십시오.

>[!NOTE]
>
>* Adobe Acrobat, Microsoft Word, Excel 및 Powerpoint는 Microsoft Windows에서만 사용할 수 있습니다. UNIX 기반 운영 체제를 사용하는 경우 OpenOffice를 설치하여 리치 텍스트 파일과 지원되는 Microsoft Office 파일을 PDF 문서로 변환합니다.
>* PDF Generator 서비스를 사용하도록 구성된 모든 사용자를 위해 Adobe Acrobat 및 타사 소프트웨어를 설치한 후 표시되는 대화 상자를 모두 종료합니다.
>* 설치된 모든 소프트웨어를 최소 한 번 시작합니다. PDF Generator 서비스를 사용하도록 구성된 모든 사용자의 대화 상자를 닫습니다.

>



Acrobat을 설치한 후 Microsoft Word를 엽니다. **Acrobat**&#x200B;탭에서 **PDF 만들기**&#x200B;를 클릭하고 컴퓨터에서 사용할 수 있는 .doc 또는 .docx 파일을 PDF 문서로 변환합니다. 변환이 성공하면 AEM Forms에서 PDF Generator 서비스를 사용하여 Acrobat을 사용할 수 있습니다.

### 환경 변수 {#setup-environment-variables} 설정

32비트 및 64비트 Java 개발 키트, 타사 애플리케이션 및 Adobe Acrobat에 대한 환경 변수를 설정합니다. 환경 변수에는 해당 애플리케이션을 시작하는 데 사용되는 실행 파일의 절대 경로가 포함되어야 합니다. 예를 들어 아래 표에는 몇 가지 애플리케이션에 대한 환경 변수가 나열되어 있습니다.

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
   <td><p><strong>JDK(32비트)</strong></p> </td> 
   <td><p>JAVA_HOME_32</p> </td> 
   <td><p>C:\Program Files (x86)\Java\jdk1.8.0_74</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>Adobe Acrobat</strong></p> </td> 
   <td><p>Acrobat_PATH</p> </td> 
   <td><p>C:\Program Files (x86)\Adobe\Acrobat 2015\Acrobat\Acrobat.exe</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>메모장</strong></p> </td> 
   <td><p>메모장_경로</p> </td> 
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
>* 모든 환경 변수와 해당 경로는 대/소문자를 구분합니다.
>* JAVA_HOME, JAVA_HOME_32 및 Acrobat_PATH(Windows 전용)는 필수 환경 변수입니다.
>* 환경 변수 OpenOffice_PATH는 실행 파일의 경로 대신 설치 폴더로 설정됩니다.
>* Word, PowerPoint, Excel 및 Project와 같은 Microsoft Office 애플리케이션이나 AutoCAD용 환경 변수를 설정하지 마십시오. 이러한 응용 프로그램이 서버에 설치되어 있는 경우 PDF 생성 서비스는 이러한 응용 프로그램을 자동으로 시작합니다.
>* UNIX 기반 플랫폼에서 OpenOffice를 /root로 설치합니다. OpenOffice가 루트로 설치되지 않은 경우 PDF Generator 서비스가 OpenOffice 문서를 PDF 문서로 변환하지 못합니다. 루트가 아닌 사용자로 OpenOffice를 설치하고 실행해야 하는 경우 루트가 아닌 사용자에게 sudo 권한을 제공합니다.
>* UNIX 기반 플랫폼에서 OpenOffice를 사용하는 경우 다음 명령을 실행하여 path 변수를 설정합니다.

>
>  
`export OpenOffice_PATH=/opt/openoffice.org4`

### (IBM WebSphere에만 해당) IBM SSL 소켓 공급자 {#only-for-ibm-websphere-configure-ibm-ssl-socket-provider} 구성

IBM SSL 소켓 공급자를 구성하려면 다음 단계를 수행하십시오.

1. java.security 파일의 복사본을 만듭니다. 파일의 기본 위치는 `[WebSphere_installation_directory]\Appserver\java_[version]\jre\lib\security`입니다.
1. 편집할 복사된 java.security 파일을 엽니다.
1. 기본 IBM WebSphere 공장 대신 JSSE2 팩토리를 사용하도록 기본 SSL 소켓 팩토리를 변경합니다.

   **기본 컨텐트입니다:**

   ```shell
   #ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
   #ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
   #WebSphere socket factories (in cryptosf.jar)
   ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
   ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
   ```

   **수정된 내용:**

   ```shell
   ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
   ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
   
   #WebSphere socket factories (in cryptosf.jar)
   #ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
   #ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
   ```

1. AEM Forms 서버가 AEM Forms 서버를 시작하는 동안 업데이트된 java.security 파일을 사용하도록 설정하려면 다음 java 인수를 추가하십시오.

   `-Djava.security.properties= [path of newly created Java.security file].`

### (Windows 전용) 설치 잉크 및 필기 서비스 구성 {#configure-install-ink-and-handwriting-service}

Microsoft Windows Server를 실행하는 경우 잉크 및 필기 서비스를 구성합니다. Microsoft Office의 연결 기능을 사용하는 Microsoft PowerPoint 파일을 여는 데 이 서비스가 필요합니다.

1. 서버 관리자를 엽니다. 빠른 실행 트레이에서 **[!UICONTROL 서버 관리자]** 아이콘을 클릭합니다.
1. **[!UICONTROL 기능]** 메뉴에서 **[!UICONTROL 기능 추가]**&#x200B;를 클릭합니다. **[!UICONTROL 잉크 및 필기 서비스]** 확인란을 선택합니다.
1. **[!UICONTROL []** 잉크] 및 [ **[!UICONTROL 필기 서비스]를 선택한 상태에서 [기능] 대화]** 상자를 선택합니다. **[!UICONTROL 설치]**&#x200B;를 클릭하면 서비스가 설치됩니다.

### (Windows 전용) Microsoft Office {#configure-the-file-block-settings-for-microsoft-office}에 대한 파일 블록 설정을 구성합니다.

PDF Generator 서비스가 이전 버전의 Microsoft Office로 만든 파일을 변환할 수 있도록 Microsoft Office Trust Center 설정을 변경합니다.

1. Microsoft Office 응용 프로그램을 엽니다. 예: Microsoft Word. **[!UICONTROL 파일]** **[!UICONTROL 옵션]**&#x200B;으로 이동합니다. 옵션 대화 상자가 나타납니다.

1. **[!UICONTROL Trust Center]**&#x200B;를 클릭하고 **[!UICONTROL Trust Center 설정]**&#x200B;을 클릭합니다.
1. **[!UICONTROL 신뢰 센터 설정]**&#x200B;에서 **[!UICONTROL 파일 블록 설정]**&#x200B;을 클릭합니다.
1. PDF Generator 서비스가 PDF 문서로 변환할 수 있도록 허용해야 하는 파일 유형을 보려면 **[!UICONTROL 파일 유형]** 목록에서 **[!UICONTROL 열기]**&#x200B;를 선택 취소합니다.

### (Windows 전용) 프로세스 수준 토큰 교체 권한 {#grant-the-replace-a-process-level-token-privilege}

응용 프로그램 서버를 시작하는 데 사용되는 사용자 계정에는 **프로세스 수준 토큰 대체** 권한이 필요합니다. 로컬 시스템 계정에는 기본적으로 **프로세스 수준 토큰 대체** 권한이 있습니다. 로컬 관리자 그룹 사용자와 함께 실행 중인 서버의 경우 권한을 명시적으로 부여해야 합니다. 권한을 부여하려면 다음 단계를 수행합니다.

1. Microsoft Windows용 그룹 정책 편집기를 엽니다. 그룹 정책 편집기를 열려면 **[!UICONTROL 시작]**&#x200B;을 클릭하고 [검색 시작] 상자에 **gpedit.msc**&#x200B;을 입력한 다음 **[!UICONTROL 그룹 정책 편집기]**&#x200B;를 클릭합니다.
1. **[!UICONTROL 로컬 컴퓨터 정책]** > **[!UICONTROL 컴퓨터 구성]** > **[!UICONTROL Windows 설정]** > **[!UICONTROL 보안 설정]** > **[!UICONTROL 로컬 정책]** > **[!UICONTROL 사용자 권한 할당&lt;a111**[!UICONTROL &#x200B;프로세스 수준 토큰 바꾸기&#x200B;]**정책을 편집하고 관리자 그룹을 포함합니다.]**
1. 프로세스 수준 토큰 교체 항목에 사용자를 추가합니다.

### (Windows만 해당) 관리자가 아닌 사용자에 대해 PDF 생성기 서비스를 활성화합니다 {#enable-the-pdf-generator-service-for-non-administrators}

관리자가 아닌 사용자가 PDF Generator 서비스를 사용하도록 설정할 수 있습니다. 일반적으로 관리 권한이 있는 사용자만 서비스를 사용할 수 있습니다.

1. 환경 변수 PDFG_NON_ADMIN_ENABLED를 만듭니다.
1. 환경 변수의 값을 TRUE로 설정합니다.
1. AEM Forms 인스턴스를 다시 시작합니다.

### (Windows 전용) 사용자 계정 컨트롤 비활성화(UAC) {#disable-user-account-control-uac}

1. 시스템 구성 유틸리티에 액세스하려면 **[!UICONTROL 시작 > 실행]**&#x200B;으로 이동한 다음 **[!UICONTROL MSCONFIG]**&#x200B;를 입력합니다.
1. **[!UICONTROL 도구]** 탭을 클릭하고 아래로 스크롤하고 **[!UICONTROL UAC 설정 변경]**&#x200B;을 선택합니다. **[!UICONTROL 실행]**&#x200B;을 클릭하여 새 창에서 명령을 실행합니다.
1. 슬라이더를 알림 안 함 수준으로 조정합니다. 완료되면 명령 창을 닫고 시스템 구성 창을 닫습니다.
1. UAC에 대한 레지스트리 설정이 0(영)으로 설정되어 있는지 확인합니다. 다음 단계를 수행하여 확인합니다.

   1. 레지스트리를 수정하기 전에 백업하는 것이 좋습니다. 자세한 단계는 Windows](https://support.microsoft.com/en-us/help/322756)에서 레지스트리를 백업 및 복원하는 방법을 참조하십시오.[
   1. Microsoft Windows 레지스트리 편집기를 엽니다. 레지스트리 편집기를 열려면 시작 > 실행으로 이동하여 regedit를 입력한 다음 확인을 클릭합니다.
   1. 다음으로 이동 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`. EnableLUA 값이 0(영)으로 설정되어 있는지 확인합니다.
   1. **EnableLUA** 값이 0(영)으로 설정되어 있는지 확인합니다. 값이 0이 아닌 경우 값을 0으로 변경합니다. 레지스트리 편집기를 닫습니다.

1. 컴퓨터를 다시 시작합니다.

### (Windows 전용) 오류 보고 서비스 {#disable-error-reporting-service} 비활성화

Windows Server의 PDF Generator 서비스를 사용하여 문서를 PDF로 변환하는 동안 Windows Server에서 실행 파일에 문제가 발생하여 닫아야 한다고 보고합니다. 그러나 백그라운드에서 계속 진행되는 PDF 변환에는 영향을 주지 않습니다.

오류가 수신되지 않도록 하려면 Windows 오류 보고를 비활성화할 수 있습니다. 오류 보고 비활성화에 대한 자세한 내용은 [https://technet.microsoft.com/en-us/library/cc754364.aspx](https://technet.microsoft.com/en-us/library/cc754364.aspx)을 참조하십시오.

### (Windows 전용) HTML을 PDF로 변환 구성 {#configure-html-to-pdf-conversion}

PDF Generator 서비스는 HTML 파일을 PDF 문서로 변환하는 방법 또는 WebKit, WebCapture 및 PhantomJS 경로를 제공합니다. Windows의 경우 WebKit 및 Acrobat WebCapture 경로에 대한 변환을 활성화하려면 유니코드 글꼴을 %windir%\fonts 디렉토리에 복사합니다.

>[!NOTE]
>
>글꼴 폴더에 새 글꼴을 설치할 때마다 AEM Forms 인스턴스를 다시 시작합니다.

### (UNIX 기반 플랫폼에만 해당) HTML을 PDF로 변환하기 위한 추가 구성 {#extra-configurations-for-html-to-pdf-conversion}

UNIX 기반 플랫폼에서 PDF Generator 서비스는 WebKit 및 PhantomJS 경로를 지원하여 HTML 파일을 PDF 문서로 변환합니다. HTML을 PDF로 변환하려면 원하는 변환 경로에 해당하는 다음 구성을 수행합니다.

### (UNIX 기반 플랫폼에만 해당) 유니코드 글꼴 지원 활성화(WebKit에만 해당) {#enable-support-for-unicode-fonts-webkit-only}

시스템에 적합한 다음 디렉토리에 유니코드 글꼴을 복사합니다.

* /usr/lib/X11/fonts/TrueType
* /usr/share/fonts/default/TrueType
* /usr/X11R6/lib/X11/fonts/ttf
* /usr/X11R6/lib/X11/fonts/truetype
* /usr/X11R6/lib/X11/fonts/TrueType
* /usr/X11R6/lib/X11/fonts/TTF
* /usr/openwin/lib/X11/fonts/TrueType(Solaris)

>[!NOTE]
>
>* RedHat Enterprise Linux 6.x 이상에서는 Courier 글꼴을 사용할 수 없습니다. Courier 글꼴을 설치하려면 font-ibm-type1-1.0.3.zip 아카이브를 다운로드합니다. /usr/share/fonts에서 아카이브를 추출합니다. /usr/share/X11/fonts에서 /usr/share/fonts로 심볼 링크를 만듭니다.
>* Html2PdfSvc/bin 및 /usr/share/fonts 디렉토리에서 모든 .lst 글꼴 캐시 파일을 삭제합니다.
>* /usr/lib/X11/fonts 및 /usr/share/fonts 디렉토리가 있는지 확인합니다. 디렉토리가 없는 경우 ln 명령을 사용하여 /usr/share/X11/fonts에서 /usr/lib/X11/fonts로 심볼 링크를 만들고 /usr/share/fonts에서 /usr/share/X11/fonts로 다른 심볼 링크를 만듭니다. 또한 Courier 글꼴은 /usr/lib/X11/fonts에서 사용할 수 있는지 확인합니다.
>* /usr/share/fonts 또는 /usr/share/X11/fonts 디렉토리에서 모든 글꼴(유니코드 및 비유니코드)을 사용할 수 있는지 확인합니다.
>* 루트가 아닌 사용자로 PDF Generator 서비스를 실행하는 경우 루트가 아닌 사용자가 모든 글꼴 디렉토리에 대한 읽기 및 쓰기 액세스 권한을 제공합니다.
>* 글꼴 폴더에 새 글꼴을 설치할 때마다 AEM Forms 인스턴스를 다시 시작합니다.

>



## AEM Forms 추가 기능 패키지 설치 {#install-aem-forms-add-on-package}

AEM Forms Add-on 패키지는 AEM에 배포되는 애플리케이션입니다. 이 패키지에는 AEM Forms 문서 서비스와 기타 AEM Forms 기능이 포함되어 있습니다. 패키지를 설치하려면 다음 단계를 수행하십시오.

1. [소프트웨어 배포](https://experience.adobe.com/downloads)를 엽니다. 소프트웨어 배포에 로그인하려면 Adobe ID가 필요합니다.
1. 헤더 메뉴에 제공된 **[!UICONTROL Adobe Experience Manager]**&#x200B;를 누릅니다.
1. **[!UICONTROL 필터]** 섹션에서 다음을 수행합니다.
   1. **[!UICONTROL 솔루션]** 드롭다운 목록에서 **[!UICONTROL Forms]**&#x200B;을 선택합니다.
   2. 패키지의 버전과 유형을 선택합니다. **[!UICONTROL 다운로드 검색]** 옵션을 사용하여 결과를 필터링할 수도 있습니다.
1. 운영 체제에 해당하는 패키지 이름을 누르고 **[!UICONTROL EULA 약관 동의]**&#x200B;를 선택한 다음 **[!UICONTROL 다운로드]**&#x200B;를 누릅니다.
1. [패키지 관리자](https://docs.adobe.com/content/help/ko-KR/experience-manager-65/administering/contentmanagement/package-manager.html)를 열고 **[!UICONTROL 패키지 업로드]**&#x200B;를 클릭하여 패키지를 업로드합니다.
1. 패키지를 선택하고 **[!UICONTROL 설치]**&#x200B;를 클릭합니다.

   [AEM Forms 릴리스](https://helpx.adobe.com/kr/aem-forms/kb/aem-forms-releases.html) 문서에 나열된 직접 링크를 통해 패키지를 다운로드할 수도 있습니다.

1. 패키지가 설치되면 AEM 인스턴스를 다시 시작하라는 메시지가 표시됩니다. **서버를 즉시 중지하지 마십시오.** AEM Forms 서버를 중지하기 전에 ServiceEvent REGISTERED 및 ServiceEvent UNREGISTED 메시지가  `[AEM-Installation-Directory]/crx-quickstart/logs/error`.log 파일에 나타나지 않고 로그가 안정될 때까지 기다립니다.

## 설치 후 구성 {#post-installation-configurations}

### RSA/BouncyCastle 라이브러리에 대한 부팅 위임 구성 {#configure-boot-delegation-for-rsa-bouncycastle-libraries}

1. AEM 인스턴스를 중지합니다. [AEM 설치 디렉토리]\crx-quickstart\conf\ folder으로 이동합니다. 편집할 sling.properties 파일을 엽니다.

   `[AEM installation directory]\crx-quickstart\bin\start.bat`을 사용하여 AEM 인스턴스를 시작하는 경우 `[AEM_root]\crx-quickstart\`에 있는 sling.properties를 편집합니다.

1. sling.properties 파일에 다음 속성을 추가합니다.

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   ```

1. (AIX에만 해당) sling.properties 파일에 다음 속성을 추가합니다.

   ```shell
   sling.bootdelegation.xerces=org.apache.xerces.*
   ```

1. 파일을 저장하고 닫습니다.

### 글꼴 관리자 서비스 {#configuring-the-font-manager-service} 구성

1. [AEM Configuration Manager](http://localhost:4502/system/console/configMgr)에 관리자로 로그인합니다.
1. **[!UICONTROL CQ-DAM-Handler-Gibson Font Managers]** 서비스를 찾아 엽니다. 시스템 글꼴, Adobe 서버 글꼴 및 고객 글꼴 디렉토리의 경로를 지정합니다. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

   >[!NOTE]
   >
   >Adobe 이외의 타사에서 제공한 글꼴을 사용할 수 있는 권리는 해당 글꼴이 있는 타사에서 제공한 라이센스 계약에 따르며, Adobe 소프트웨어 사용에 대한 라이센스에는 적용되지 않습니다. Adobe은 Adobe 소프트웨어에 Adobe이 아닌 글꼴을 사용하기 전에, 특히 서버 환경에서 글꼴을 사용하는 것과 관련하여 Adobe이 아닌 글꼴을 사용하기 전에 해당 이외의 모든 사용권 계약을 검토하고 이에 부합하도록 권장합니다.
   > 글꼴 폴더에 새 글꼴을 설치하면 AEM Forms 인스턴스를 다시 시작합니다.

### PDF Generator 서비스 {#configure-a-local-user-account-to-run-the-pdf-generator-service} 실행을 위한 로컬 사용자 계정 구성

PDF Generator 서비스를 실행하려면 로컬 사용자 계정이 필요합니다. 로컬 사용자를 만드는 단계는 [Windows](https://support.microsoft.com/en-us/help/13951/windows-create-user-account)에서 사용자 계정 만들기 또는 [UNIX 기반 플랫폼](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/4/html/Step_by_Step_Guide/s1-starting-create-account.html)에서 사용자 계정 만들기를 참조하십시오.

1. [AEM Forms PDF 생성기 구성](http://localhost:4502/libs/fd/pdfg/config/ui.html) 페이지를 엽니다.

1. **[!UICONTROL 사용자 계정]** 탭에서 로컬 사용자 계정의 자격 증명을 입력하고 **[!UICONTROL 제출]**&#x200B;을 클릭합니다. Microsoft Windows에서 메시지가 표시되면 사용자에 대한 액세스를 허용합니다. 성공적으로 추가되면 구성된 사용자가 **[!UICONTROL 사용자 계정]** 탭의 **[!UICONTROL 사용자 계정]** 섹션 아래에 표시됩니다.

### 시간 초과 설정 {#configure-the-time-out-settings} 구성

1. [AEM 구성 관리자](http://localhost:4502/system/console/configMgr)에서 **[!UICONTROL Jacorb ORB 공급자]** 서비스를 찾아 엽니다.

   **[!UICONTROL 사용자 지정 속성.name]** 필드에 다음을 추가하고 **[!UICONTROL 저장]**&#x200B;을 클릭합니다. 보류 중인 응답 시간 초과(CORBA 클라이언트 시간 초과라고도 함)를 600초로 설정합니다.

   `jacorb.connection.client.pending_reply_timeout=600000`

1. AEM 작성자 인스턴스에 로그인하고 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 도구]** > **[!UICONTROL Forms]** > **[!UICONTROL PDF Generator 구성]**&#x200B;으로 이동합니다. 기본 URL은 http://localhost:4502/libs/fd/pdfg/config/ui.html입니다.

   **[!UICONTROL 일반 구성]** 탭을 열고 환경에 대해 다음 필드의 값을 수정합니다.

<table> 
 <tbody> 
  <tr> 
   <td>필드</td> 
   <td>설명</td> 
   <td>기본 값</td> 
  </tr> 
  <tr> 
   <td>서버 변환 시간 제한</td> 
   <td>PDFG 변환은 서버 변환 시간 초과에 정의된 시간(초) 동안 활성 상태를 유지합니다.</td> 
   <td>270초<br /> </td> 
  </tr> 
  <tr> 
   <td>PDFG 정리 스캔(초)</td> 
   <td>전환 후 작업을 수행하는 데 필요한 시간(초)입니다.<br /> </td> 
   <td>3600초</td> 
  </tr> 
  <tr> 
   <td>작업 만료 초</td> 
   <td>PDF Generator 서비스가 변환을 실행할 수 있는 기간입니다. 작업 만료 초 값이 PDFG 정리 검색 초 값보다 큰지 확인합니다.</td> 
   <td>7200초</td> 
  </tr> 
 </tbody> 
</table>

### (Windows 전용) PDF Generator 서비스 {#configure-acrobat-for-the-pdf-generator-service}용 Acrobat 구성

Microsoft Windows의 경우 PDF Generator 서비스는 Adobe Acrobat을 사용하여 지원되는 파일 형식을 PDF 문서로 변환합니다. 다음 단계를 수행하여 PDF Generator 서비스용 Adobe Acrobat을 구성합니다.

1. Acrobat을 열고 **[!UICONTROL 편집]** **[!UICONTROL 환경 설정]** **[!UICONTROL 업데이터]**&#x200B;를 선택합니다. [업데이트 확인]에서 **[!UICONTROL 업데이트 자동 설치]**&#x200B;를 선택 취소하고 **[!UICONTROL 확인]**&#x200B;을 클릭합니다. Acrobat을 닫습니다.
1. 시스템에서 PDF 문서를 두 번 클릭합니다. Acrobat이 처음 시작되면 로그인, 시작 화면 및 EULA에 대한 대화 상자가 나타납니다. PDF Generator를 사용하도록 구성한 모든 사용자에 대해 이 대화 상자를 닫습니다.
1. PDF Generator 유틸리티 일괄 처리 파일을 실행하여 PDF Generator 서비스용 Acrobat을 구성합니다.

   1. [AEM Package Manager](http://localhost:4502/crx/packmgr/index.jsp)를 열고 패키지 관리자에서 `adobe-aemfd-pdfg-common-pkg-[version].zip` 파일을 다운로드합니다.
   1. 다운로드한 .zip 파일의 압축을 해제합니다. 관리자 권한으로 명령 프롬프트를 엽니다.
   1. `[extracted-zip-file]\jcr_root\etc\fd\pdfg\tools\adobe-aemfd-pdfg-utilities-[version]-win.zip\scripts` 디렉토리로 이동합니다. 다음 배치 파일을 실행합니다.

      `Acrobat_for_PDFG_Configuration.bat`

      Acrobat은 PDF Generator 서비스에서 실행되도록 구성되어 있습니다.

1. SRT(시스템 준비 도구)를 실행하여 Acrobat 설치를 확인합니다. 이 도구는 시스템이 PDF Generator 변환을 실행하도록 제대로 구성되어 있는지 확인하고 지정된 경로에서 보고서를 생성합니다.

   1. 명령 프롬프트를 엽니다. `[extracted-adobe-aemfd-pdfg-common-pkg]\jcr_root\etc\fd\ pdfg\tools\adobe-aemfd-pdfg-utilities-[version]-win.zip\srt` 폴더로 이동합니다. 명령 프롬프트에서 다음 명령을 실행합니다.

      `cscript SystemReadinessTool.vbs [Path_of_reports_folder] en`

      >[!NOTE]
      >
      >시스템 준비 도구가 acrobat 플러그인 폴더에서 pdfgen.api 파일을 사용할 수 없다고 보고하면 pdfgen.api 파일을 `[extracted-adobe-aemfd-pdfg-common-pkg]\plugins\x86_win32` 디렉토리의 `[Acrobat_root]\Acrobat\plug_ins` 디렉토리로 복사합니다.

   1. 다음으로 이동 `[Path_of_reports_folder]`. SystemReadyTool.html 파일을 엽니다. 보고서를 확인하고 언급된 문제를 수정합니다.

### (Windows만 해당) HTML에서 PDF로 변환하는 기본 경로 구성 {#configure-primary-route-for-html-to-pdf-conversion-windows-only}

PDF Generator 서비스는 HTML 파일을 PDF 문서로 변환하는 다양한 경로를 제공합니다.Webkit, Acrobat WebCapture(Windows 전용) 및 PhantomJS입니다. 동적 컨텐츠를 처리할 수 있고 32비트 라이브러리, 32비트 JDK에 대한 종속성이 없거나 추가 글꼴이 필요 없으므로 PhantomJS 라우트를 사용하는 것이 좋습니다. 또한 PhantomJS 경로에는 변환을 실행하기 위한 sudo 또는 루트 액세스가 필요하지 않습니다.

HTML을 PDF로 변환하는 기본 경로는 Webkit입니다. 전환 경로를 변경하려면:

1. AEM 작성자 인스턴스의 경우 **[!UICONTROL 도구]****[!UICONTROL Forms]** **[!UICONTROL PDF Generator 구성]**&#x200B;으로 이동합니다.

1. **[!UICONTROL 일반 구성]** 탭의 HTML을 PDF로 변환할 기본 경로&#x200B;]**드롭다운에서 기본 전환 경로를 선택합니다.**[!UICONTROL 

### 전역 트러스트 저장소 {#intialize-global-trust-store} 초기화

Trust Store Management를 사용하여 디지털 서명 및 인증서 인증의 확인을 위해 서버에서 신뢰하는 인증서를 가져오거나 편집 및 삭제할 수 있습니다. 원하는 수의 인증서를 가져오거나 내보낼 수 있습니다. 인증서를 가져온 후 트러스트 설정 및 신뢰 저장소 유형을 편집할 수 있습니다. 신뢰 저장소를 초기화하려면 다음 단계를 수행하십시오.

1. AEM Forms 인스턴스에 관리자로 로그인합니다.
1. **[!UICONTROL 도구]** > **[!UICONTROL 보안]** > **[!UICONTROL Trust Store]**&#x200B;로 이동합니다.
1. **[!UICONTROL TrustStore 만들기]**&#x200B;를 클릭합니다. 암호를 설정하고 **[!UICONTROL 저장]**&#x200B;을 누릅니다.

### Reader 확장 및 암호화 서비스 {#set-up-certificates-for-reader-extension-and-encryption-service}에 대한 인증서를 설정합니다.

DocAssurance 서비스는 PDF 문서에 사용 권한을 적용할 수 있습니다. PDF 문서에 사용 권한을 적용하려면 인증서를 구성합니다.

인증서를 설정하기 전에 다음 내용이 있는지 확인하십시오.

* 인증서 파일(.pfx).

* 개인 키 암호가 인증서와 함께 제공되었습니다.

* 개인 키 별칭. Java 키 도구 명령을 실행하여 개인 키 별칭을 볼 수 있습니다.
   `keytool -list -v -keystore [keystore-file] -storetype pkcs12`

* Keystore 파일 암호. Adobe의 Reader 확장 인증서를 사용하는 경우 Keystore 파일 암호는 항상 개인 키 암호와 동일합니다.

인증서를 구성하려면 다음 단계를 수행하십시오.

1. AEM 작성자 인스턴스에 관리자로 로그인합니다. **[!UICONTROL 도구]** > **[!UICONTROL 보안]** > **[!UICONTROL 사용자]**&#x200B;로 이동합니다.
1. 사용자 계정의 **[!UICONTROL 이름]** 필드를 클릭합니다. **[!UICONTROL 사용자 설정 편집]** 페이지가 열립니다. AEM 작성자 인스턴스에서 인증서는 KeyStore에 상주합니다. 이전에 KeyStore를 만들지 않은 경우 **[!UICONTROL Create KeyStore]**&#x200B;를 클릭하고 KeyStore에 대한 새 암호를 설정합니다. 서버에 이미 KeyStore가 포함되어 있으면 이 단계를 건너뜁니다.  Adobe의 Reader 확장 인증서를 사용하는 경우 Keystore 파일 암호는 항상 개인 키 암호와 동일합니다.
1. **[!UICONTROL 사용자 설정 편집]** 페이지에서 **[!UICONTROL KeyStore]** 탭을 선택합니다. **[!UICONTROL 키 저장소 파일]** 옵션에서 개인 키 추가 옵션을 확장하고 별칭을 제공합니다. 별칭은 Reader 확장 작업을 수행하는 데 사용됩니다.
1. 인증서 파일을 업로드하려면 **[!UICONTROL 키 저장소 파일 선택]**&#x200B;을 클릭하고 &lt;filename>.pfx 파일을 업로드합니다.

   각각의 필드에 인증서에 연결된 **[!UICONTROL 키 저장소 암호]**, **[!UICONTROL 개인 키 암호]** 및 **[!UICONTROL 개인 키 별칭]**&#x200B;을 추가합니다. **[!UICONTROL 제출]**&#x200B;을 클릭합니다.

   >[!NOTE]
   >
   >프로덕션 환경에서 평가 자격 증명을 프로덕션 자격 증명으로 바꿉니다. 만료되거나 평가 자격 증명을 업데이트하기 전에 이전 Reader 확장 자격 증명을 삭제해야 합니다.

1. **[!UICONTROL 사용자 설정 편집]** 페이지에서 **[!UICONTROL 저장 및 닫기]**&#x200B;를 클릭합니다.

### AES-256 {#enable-aes} 사용

PDF 파일에 대해 AES 256 암호화를 사용하려면 JCE(Java Cryptography Extension) 무제한 강도 관할 구역 정책 파일을 입수하고 설치합니다. jre/lib/security 폴더에서 local_policy.jar 및 US_export_policy.jar 파일을 교체합니다. 예를 들어 Sun JDK를 사용하는 경우 다운로드한 파일을 `[JAVA_HOME]/jre/lib/security` 폴더에 복사합니다.

어셈블러 서비스는 Reader 확장 서비스, 서명 서비스, Forms 서비스 및 출력 서비스에 따라 달라집니다. 다음 단계를 수행하여 필요한 서비스가 실행 중인지 확인합니다.

1. URL `https://'[server]:[port]'/system/console/bundles`에 관리자로 로그인합니다.
1. 다음 서비스를 검색하여 서비스가 실행 중인지 확인하십시오.

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

* 압축된 입력 파일에 파일 이름에 더블바이트 문자가 포함된 HTML 파일이 포함된 경우 HTML을 PDF로 변환할 수 없습니다. 이 문제를 방지하려면 HTML 파일의 이름을 지정할 때 더블바이트 문자를 사용하지 마십시오.

* UNIX 기반 운영 체제에서 누락된 라이브러리를 찾으려면 다음을 수행합니다.

1. 다음으로 이동 `[crx-repository]/bedrock/svcnative/HtmlToPdfSvc/bin/`.

1. 다음 명령을 실행하여 PhantomJS에서 HTML에서 PDF로 변환하는 데 필요한 모든 라이브러리를 나열합니다.

   `ldd phantomjs`

   다음 명령을 실행하여 누락된 라이브러리를 나열합니다.

   `ldd phantomjs | grep not`

1. 누락된 라이브러리를 수동으로 설치합니다.

## 다음 단계 {#next-steps}

작업 중인 AEM Forms 다큐멘트 서비스 환경이 있습니다. 다음 방법을 통해 문서 서비스를 사용할 수 있습니다.

* [OSGi 기반의 양식 중심 워크플로우](/help/forms/using/aem-forms-workflow.md)
* [감시 폴더](/help/forms/using/watched-folder-in-aem-forms.md)
* [문서 서비스 API](/help/forms/using/aem-document-services-programmatically.md)

