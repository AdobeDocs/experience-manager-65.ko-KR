---
title: 파일 형식과 PDF 간 변환
seo-title: Converting Between File Formats and PDF
description: PDF 생성 서비스를 사용하여 기본 파일 형식을 PDF으로 변환합니다. 또한 PDF 서비스 생성 은 PDF을 다른 파일 형식으로 변환하고 PDF 문서의 크기를 최적화합니다.
seo-description: Use the Generate PDF service to convert native file formats to PDF. Generate PDF service also converts PDF to other file formats and optimizes the size of PDF documents.
uuid: f72ad603-c996-4d48-9bfc-bed7bf776af6
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 180cac3f-6378-42bc-9a47-60f9f08a7103
role: Developer
exl-id: 10535740-e3c2-4347-a88f-86706ad699b4
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '7850'
ht-degree: 0%

---

# 파일 형식과 PDF 간 변환 {#converting-between-file-formatsand-pdf}

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms에 대해서만 적용됩니다.**

**PDF 서비스 생성 정보**

PDF 생성 서비스는 기본 파일 형식을 PDF으로 변환합니다. 또한 PDF을 다른 파일 형식으로 변환하고 PDF 문서의 크기를 최적화합니다.

PDF 생성 서비스는 기본 응용 프로그램을 사용하여 다음 파일 형식을 PDF으로 변환합니다. 달리 명시되지 않은 경우 이러한 응용 프로그램의 독일어, 프랑스어, 영어 및 일본어 버전만 지원됩니다. *Windows에만 해당* 는 Windows Server® 2003 및 Windows Server 2008에 대한 지원만 나타냅니다.

* DOC, DOCX, RTF, TXT, XLS, XLSX, PPT, PPTX, VSD, MPP, MPPX, XPS 및 PUB를 변환하는 Microsoft Office 2003 및 2007(Windows에만 해당)

>[!NOTE]
>
>Microsoft XPS 형식을 PDF으로 변환하려면 Acrobat® 9.2 이상이 필요합니다.

* Autodesk AutoCAD 2005, 2006, 2007, 2008 및 2009에서 DWF, DWG 및 DXW 변환(영어만 해당)
* Corel WordPerfect 12 및 X4를 사용하여 WPD, QPW, SHW(영어만 해당) 변환
* OpenOffice 2.0, 2.4, 3.0.1 및 3.1을 사용하여 ODT, ODS, ODP, ODG, ODF, SXW, SXI, SXC, SXD, DOC, DOCX, RTF, TXT, XLS, XLSX, PPT, PPTX, VSD, MPP, MPPX 및 PUB 변환

>[!NOTE]
>
>PDF 생성 서비스는 64비트 버전의 OpenOffice를 지원하지 않습니다.

* Adobe Photoshop® CS2를 사용하여 PSD 변환(Windows에만 해당)

>[!NOTE]
>
>Photoshop CS3 및 CS4는 Windows Server 2003 또는 Windows Server 2008을 지원하지 않으므로 지원되지 않습니다.

* Adobe FrameMaker® 7.2 및 8을 사용하여 FM 변환(Windows에만 해당)
* Adobe PageMaker® 7.0을 사용하여 PMD, PM6, P65 및 PM 변환(Windows에만 해당)
* 타사 응용 프로그램에서 지원하는 기본 형식(해당 응용 프로그램용 설치 파일을 개발해야 함)(Windows에만 해당)

PDF 생성 서비스는 다음 표준 기반 파일 형식을 PDF으로 변환합니다.

* 비디오 형식: SWF, FLV(Windows에만 해당)
* 이미지 형식: JPEG, JPG, JP2, J2Kí, JPC, J2C, GIF, BMP, TIFF, TIF, PNG, JPF
* HTML(Windows, Sun™ Solaris™ 및 Linux®)

PDF 생성 서비스는 PDF을 다음 파일 형식으로 변환합니다(Windows에만 해당).

* 캡슐화된 포스트스크립트(EPS)
* HTML3.2
* HTML 4.01(CSS 1.0 포함)
* DOC (Microsoft Word 형식)
* RTF
* 텍스트(액세스 가능 및 일반 모두)
* XML
* DeviceRGB 색상 공간만 사용하는 PDF/A-1a
* DeviceRGB 색상 공간만 사용하는 PDF/A-1b

PDF 생성 서비스를 사용하려면 다음 관리 작업을 수행해야 합니다.

* AEM Forms을 호스팅하는 컴퓨터에 필요한 기본 응용 프로그램을 설치합니다.
* AEM Forms을 호스팅하는 컴퓨터에 Adobe Acrobat Professional 또는 Acrobat Pro Extended 9.2 설치
* 설치 후 설정 작업 수행

이러한 작업은 JBoss 턴키를 사용하여 AEM 양식 설치 및 배포에 설명되어 있습니다.

PDF 생성 서비스를 사용하여 다음 작업을 수행할 수 있습니다.

* 기본 파일 형식에서 PDF으로 변환합니다.
* HTML 문서를 PDF 문서로 변환합니다.
* PDF 문서를 파일 형식으로 변환합니다.

>[!NOTE]
>
>PDF 생성 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

## Word 문서를 PDF 문서로 변환 {#converting-word-documents-to-pdf-documents}

이 섹션에서는 PDF 생성 API를 사용하여 Microsoft Word 문서를 PDF 문서로 프로그래밍 방식으로 변환하는 방법에 대해 설명합니다.

>[!NOTE]
>
>추가 파일 형식에 대한 자세한 내용은 [추가 기본 파일 형식에 대한 지원 추가](converting-file-formats-pdf.md#adding-support-for-additional-native-file-formats).

>[!NOTE]
>
>PDF 생성 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary-of-steps}

Microsoft Word 문서를 PDF 문서로 변환하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. PDF 클라이언트 생성을 참조하십시오.
1. 파일을 검색하여 PDF 문서로 변환합니다.
1. 파일을 PDF 문서로 변환합니다.
1. 결과를 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**PDF 클라이언트 생성**

PDF 생성 작업을 프로그래밍 방식으로 수행하려면 먼저 PDF 서비스 클라이언트 생성을 참조하십시오. Java API를 사용하는 경우 `GeneratePdfServiceClient` 개체. 웹 서비스 API를 사용하는 경우 `GeneratePDFServiceService` 개체.

**파일을 검색하여 PDF 문서로 변환**

Microsoft Word 문서를 검색하여 PDF 문서로 변환합니다.

**파일을 PDF 문서로 변환**

PDF 서비스 클라이언트 생성을 생성한 후 `createPDF2` 메서드를 사용합니다. 이 메서드에는 파일 확장명을 포함하여 변환할 문서에 대한 정보가 필요합니다.

**결과 검색**

파일이 PDF 문서로 변환된 후 결과를 검색할 수 있습니다. 예를 들어 Word 파일을 PDF 문서로 변환한 후 PDF 문서를 검색하여 저장할 수 있습니다.

**추가 참조**

[Java API를 사용하여 Word 문서를 PDF 문서로 변환](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-java-api)

[웹 서비스 API를 사용하여 Word 문서를 PDF 문서로 변환](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF 서비스 API 빠른 시작 생성](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Java API를 사용하여 Word 문서를 PDF 문서로 변환 {#convert-word-documents-to-pdf-documents-using-the-java-api}

Java(PDF 생성 API)를 사용하여 Microsoft Word 문서를 PDF 문서로 변환합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-generatepdf-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. PDF 클라이언트 생성을 참조하십시오.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.
   * 만들기 `GeneratePdfServiceClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체.

1. 파일을 검색하여 PDF 문서로 변환합니다.

   * 만들기 `java.io.FileInputStream` 생성자를 사용하여 변환할 Word 파일을 나타내는 개체입니다. 파일 위치를 지정하는 문자열 값을 전달합니다.
   * 만들기 `com.adobe.idp.Document` 개체를 생성자를 사용하고 `java.io.FileInputStream` 개체.

1. 파일을 PDF 문서로 변환합니다.

   를 호출하여 파일을 PDF 문서로 변환 `GeneratePdfServiceClient` 개체 `createPDF2` 메서드 및 다음 값 전달:

   * A `com.adobe.idp.Document` 변환할 파일을 나타내는 개체입니다.
   * A `java.lang.String` 파일 확장명이 포함된 개체입니다.
   * A `java.lang.String` 변환에 사용할 파일 형식 설정을 포함하는 개체입니다. 파일 형식 설정은 .doc 또는 .xls와 같은 다양한 파일 형식에 대한 변환 설정을 제공합니다.
   * A `java.lang.String` 사용할 PDF 설정의 이름이 포함된 개체입니다. 예를 들어 다음을 지정할 수 있습니다 `Standard`.
   * A `java.lang.String` 사용할 보안 설정의 이름이 포함된 개체입니다.
   * 선택 사항입니다 `com.adobe.idp.Document` PDF 문서를 생성하는 동안 적용할 설정이 포함된 객체입니다.
   * 선택 사항입니다 `com.adobe.idp.Document` PDF 문서에 적용할 메타데이터 정보가 포함된 객체입니다.

   다음 `createPDF2` 메서드가 을 반환합니다. `CreatePDFResult` 새 PDF 문서 및 로그 정보가 포함된 개체입니다. 로그 파일에는 일반적으로 전환 요청으로 생성된 오류 또는 경고 메시지가 포함되어 있습니다.

1. 결과를 검색합니다.

   PDF 문서를 가져오려면 다음 작업을 수행합니다.

   * 호출 `CreatePDFResult` 개체 `getCreatedDocument` 메서드, 반환 `com.adobe.idp.Document` 개체.
   * 호출 `com.adobe.idp.Document` 개체 `copyToFile` 이전 단계에서 만든 객체에서 PDF 문서를 추출하는 방법입니다.

   를 사용한 경우 `createPDF2` 로그 문서를 가져오는 메서드(HTML 전환에는 적용되지 않음)에서 다음 작업을 수행합니다.

   * 호출 `CreatePDFResult` 개체 `getLogDocument` 메서드를 사용합니다. 이 값은 `com.adobe.idp.Document` 개체.
   * 호출 `com.adobe.idp.Document` 개체 `copyToFile` 로그 문서를 추출하는 메서드입니다.


**추가 참조**

[단계 요약](converting-file-formats-pdf.md#summary-of-steps)

[빠른 시작(SOAP 모드): Java API를 사용하여 Microsoft Word 문서를 PDF 문서로 변환](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-a-microsoft-word-document-to-a-pdf-document-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 Word 문서를 PDF 문서로 변환 {#convert-word-documents-to-pdf-documents-using-the-web-service-api}

PDF API 생성(웹 서비스)을 사용하여 Microsoft Word 문서를 PDF 문서로 변환합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용하는지 확인합니다. `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` AEM Forms을 호스팅하는 서버의 IP 주소입니다.

1. PDF 클라이언트 생성을 참조하십시오.

   * 만들기 `GeneratePDFServiceClient` 기본 생성자를 사용하여 개체를 작성합니다.
   * 만들기 `GeneratePDFServiceClient.Endpoint.Address` 을 사용하여 개체 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`.) 를 사용할 필요가 없습니다. `lc_version` 특성. 단, 을 지정합니다. `?blob=mtom`.
   * 만들기 `System.ServiceModel.BasicHttpBinding` 의 값을 가져와서 개체 `GeneratePDFServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스트 `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름 할당 `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`.
      * 해당 암호 값을 필드에 할당합니다. `GeneratePDFServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 지정 `HttpClientCredentialType.Basic` 필드에 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 상수 값 지정 `BasicHttpSecurityMode.TransportCredentialOnly` 필드에 `BasicHttpBindingSecurity.Security.Mode`.

1. 파일을 검색하여 PDF 문서로 변환합니다.

   * 만들기 `BLOB` 개체를 만들 때 사용됩니다. 다음 `BLOB` 개체는 PDF 문서로 변환할 파일을 저장하는 데 사용됩니다.
   * 만들기 `System.IO.FileStream` 해당 생성자를 호출하여 개체를 작성합니다. 변환할 파일의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 콘텐츠를 저장하는 바이트 배열 만들기 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채우기 `System.IO.FileStream` 개체 `Read` 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하는 방법.
   * 채우기 `BLOB` 에 할당하여 오브젝트 `MTOM` 속성을 바이트 배열의 내용으로 지정합니다.

1. 파일을 PDF 문서로 변환합니다.

   를 호출하여 파일을 PDF 문서로 변환 `GeneratePDFServiceService` 개체 `CreatePDF2` 메서드 및 다음 값 전달:

   * A `BLOB` 변환할 파일을 나타내는 개체입니다.
   * 파일 확장명을 포함하는 문자열입니다.
   * A `java.lang.String` 변환에 사용할 파일 형식 설정을 포함하는 개체입니다. 파일 형식 설정은 .doc 또는 .xls와 같은 다양한 파일 형식에 대한 변환 설정을 제공합니다.
   * 사용할 PDF 설정을 포함하는 문자열 개체입니다. 다음을 지정할 수 있습니다. `Standard`.
   * 사용할 보안 설정이 포함된 문자열 개체입니다. 다음을 지정할 수 있습니다. `No Security`.
   * 선택 사항입니다 `BLOB` PDF 문서를 생성하는 동안 적용할 설정이 포함된 객체입니다.
   * 선택 사항입니다 `BLOB` PDF 문서에 적용할 메타데이터 정보가 포함된 객체입니다.
   * 유형의 출력 매개 변수 `BLOB` 이 채우는 사람: `CreatePDF2` 메서드를 사용합니다. 다음 `CreatePDF2` 메서드는 변환된 문서로 이 개체를 채웁니다. (이 매개 변수 값은 웹 서비스 호출에만 필요합니다.)
   * 유형의 출력 매개 변수 `BLOB` 이 채우는 사람: `CreatePDF2` 메서드를 사용합니다. 다음 `CreatePDF2` 메서드는 이 개체를 로그 문서로 채웁니다. (이 매개 변수 값은 웹 서비스 호출에만 필요합니다.)

1. 결과를 검색합니다.

   * 를 할당하여 변환된 PDF 문서 검색 `BLOB` 개체 `MTOM` 필드를 바이트 배열로 바꿉니다. 바이트 배열은 변환된 PDF 문서를 나타냅니다. 다음을 사용하십시오. `BLOB` 의 출력 매개 변수로 사용되는 개체입니다 `createPDF2` 메서드를 사용합니다.
   * 만들기 `System.IO.FileStream` 개체를 호출하고 변환된 PDF 문서의 파일 위치를 나타내는 문자열 값을 전달합니다.
   * 만들기 `System.IO.BinaryWriter` 개체를 호출하고 `System.IO.FileStream` 개체.
   * 를 호출하여 바이트 배열의 내용을 PDF 파일에 씁니다 `System.IO.BinaryWriter` 개체 `Write` 메서드 및 바이트 배열 전달.

**추가 참조**

[단계 요약](converting-file-formats-pdf.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## HTML 문서를 PDF 문서로 변환 {#converting-html-documents-to-pdf-documents}

이 섹션에서는 PDF 생성 API를 사용하여 HTML 문서를 PDF 문서로 프로그래밍 방식으로 변환하는 방법에 대해 설명합니다.

>[!NOTE]
>
>PDF 생성 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-1}

HTML 문서를 PDF 문서로 변환하려면 다음 작업을 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. PDF 클라이언트 생성을 참조하십시오.
1. HTML 콘텐츠를 검색하여 PDF 문서로 변환합니다.
1. HTML 콘텐츠를 PDF 문서로 변환합니다.
1. 결과를 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**PDF 클라이언트 생성**

PDF 생성 작업을 프로그래밍 방식으로 수행하려면 먼저 PDF 서비스 생성 클라이언트를 만들어야 합니다. Java API를 사용하는 경우 `GeneratePdfServiceClient` 개체. 웹 서비스 API를 사용하는 경우 `GeneratePDFServiceService`.

**HTML 콘텐츠를 검색하여 PDF 문서로 변환**

PDF 문서로 변환할 HTML 콘텐츠를 참조합니다. URL을 사용하여 액세스할 수 있는 HTML 파일 또는 HTML 컨텐츠와 같은 HTML 컨텐츠를 참조할 수 있습니다.

**HTML 콘텐츠를 PDF 문서로 변환**

서비스 클라이언트를 만든 후 적절한 PDF 만들기 작업을 호출할 수 있습니다. 이 작업에는 대상 문서에 대한 경로를 포함하여 변환할 문서에 대한 정보가 필요합니다.

**결과 검색**

HTML 콘텐츠가 PDF 문서로 변환된 후 결과를 검색하고 PDF 문서를 저장할 수 있습니다.

**추가 참조**

[Java API를 사용하여 HTML 컨텐츠를 PDF 문서로 변환](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-java-api)

[웹 서비스 API를 사용하여 HTML 콘텐츠를 PDF 문서로 변환](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF 서비스 API 빠른 시작 생성](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Java API를 사용하여 HTML 컨텐츠를 PDF 문서로 변환 {#convert-html-content-to-a-pdf-document-using-the-java-api}

PDF API 생성(Java)을 사용하여 HTML 문서를 PDF 문서로 변환합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-generatepdf-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. PDF 클라이언트 생성을 참조하십시오.

   만들기 `GeneratePdfServiceClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.

1. HTML 콘텐츠를 검색하여 PDF 문서로 변환합니다.

   문자열 변수를 만들고 HTML 콘텐츠를 가리키는 URL을 할당하여 HTML 콘텐츠를 검색합니다.

1. HTML 콘텐츠를 PDF 문서로 변환합니다.

   호출 `GeneratePdfServiceClient` 개체 `htmlToPDF2` 메서드를 실행하고 다음 값을 전달합니다.

   * A `java.lang.String` 변환할 HTML 파일의 URL이 포함된 개체입니다.
   * A `java.lang.String` 변환에 사용할 파일 형식 설정을 포함하는 개체입니다. 파일 유형 설정에는 스파이더 수준이 포함될 수 있습니다.
   * A `java.lang.String` 사용할 보안 설정의 이름이 포함된 개체입니다.
   * 선택 사항입니다 `com.adobe.idp.Document` PDF 문서를 생성하는 동안 적용할 설정이 포함된 객체입니다. 이 정보가 제공되지 않으면 이전 세 매개 변수를 기반으로 설정이 자동으로 선택됩니다.
   * 선택 사항입니다 `com.adobe.idp.Document` PDF 문서에 적용할 메타데이터 정보가 포함된 객체입니다.

1. 결과를 검색합니다.

   다음 `htmlToPDF2` 메서드가 다음을 반환합니다. `HtmlToPdfResult` 생성된 새 PDF 문서가 포함된 개체입니다. 새로 만든 PDF 문서를 가져오려면 다음 작업을 수행합니다.

   * 호출 `HtmlToPdfResult` 개체 `getCreatedDocument` 메서드를 사용합니다. 이 값은 `com.adobe.idp.Document` 개체.
   * 호출 `com.adobe.idp.Document` 개체 `copyToFile` 이전 단계에서 만든 객체에서 PDF 문서를 추출하는 방법입니다.

**추가 참조**

[HTML 문서를 PDF 문서로 변환](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[빠른 시작(SOAP 모드): Java API를 사용하여 HTML 콘텐츠를 PDF 문서로 변환](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[빠른 시작(SOAP 모드): Java API를 사용하여 HTML 콘텐츠를 PDF 문서로 변환](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 HTML 콘텐츠를 PDF 문서로 변환 {#convert-html-content-to-a-pdf-document-using-the-web-service-api}

PDF API 생성(웹 서비스)을 사용하여 HTML 컨텐츠를 PDF 문서로 변환합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용하는지 확인합니다. `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` AEM Forms을 호스팅하는 서버의 IP 주소입니다.

1. PDF 클라이언트 생성을 참조하십시오.

   * 만들기 `GeneratePDFServiceClient` 기본 생성자를 사용하여 개체를 작성합니다.
   * 만들기 `GeneratePDFServiceClient.Endpoint.Address` 을 사용하여 개체 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`.) 를 사용할 필요가 없습니다. `lc_version` 특성. 단, 을 지정합니다. `?blob=mtom`.
   * 만들기 `System.ServiceModel.BasicHttpBinding` 의 값을 가져와서 개체 `GeneratePDFServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스트 `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름 할당 `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`.
      * 해당 암호 값을 필드에 할당합니다. `GeneratePDFServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 지정 `HttpClientCredentialType.Basic` 필드에 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 상수 값 지정 `BasicHttpSecurityMode.TransportCredentialOnly` 필드에 `BasicHttpBindingSecurity.Security.Mode`.

1. HTML 콘텐츠를 검색하여 PDF 문서로 변환합니다.

   문자열 변수를 만들고 HTML 콘텐츠를 가리키는 URL을 할당하여 HTML 콘텐츠를 검색합니다.

1. HTML 콘텐츠를 PDF 문서로 변환합니다.

   를 호출하여 HTML 콘텐츠를 PDF 문서로 변환합니다. `GeneratePDFServiceService` 개체 `HtmlToPDF2` 메서드를 실행하고 다음 값을 전달합니다.

   * 변환할 HTML 콘텐츠가 포함된 문자열입니다.
   * A `java.lang.String` 변환에 사용할 파일 형식 설정을 포함하는 개체입니다.
   * 사용할 보안 설정이 포함된 문자열 개체입니다.
   * 선택 사항입니다 `BLOB` PDF 문서를 생성하는 동안 적용할 설정이 포함된 객체입니다.
   * 선택 사항입니다 `BLOB` PDF 문서에 적용할 메타데이터 정보가 포함된 객체입니다.
   * 유형의 출력 매개 변수 `BLOB` 이 채우는 사람: `CreatePDF2` 메서드를 사용합니다. 다음 `CreatePDF2` 메서드는 변환된 문서로 이 개체를 채웁니다. (이 매개 변수 값은 웹 서비스 호출에만 필요합니다.)

1. 결과를 검색합니다.

   * 를 할당하여 변환된 PDF 문서 검색 `BLOB` 개체 `MTOM` 필드를 바이트 배열로 바꿉니다. 바이트 배열은 변환된 PDF 문서를 나타냅니다. 다음을 사용하십시오. `BLOB` 의 출력 매개 변수로 사용되는 개체입니다 `HtmlToPDF2` 메서드를 사용합니다.
   * 만들기 `System.IO.FileStream` 개체를 호출하고 변환된 PDF 문서의 파일 위치를 나타내는 문자열 값을 전달합니다.
   * 만들기 `System.IO.BinaryWriter` 개체를 호출하고 `System.IO.FileStream` 개체.
   * 를 호출하여 바이트 배열의 내용을 PDF 파일에 씁니다 `System.IO.BinaryWriter` 개체 `Write` 메서드 및 바이트 배열 전달.

**추가 참조**

[HTML 문서를 PDF 문서로 변환](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## PDF 문서를 이미지가 아닌 형식으로 변환 {#converting-pdf-documents-to-non-image-formats}

이 단원에서는 PDF Java API 및 웹 서비스 API 생성 을 사용하여 PDF 문서를 프로그래밍 방식으로 이미지가 아닌 형식의 예인 RTF 파일로 변환하는 방법에 대해 설명합니다. 이미지가 아닌 다른 형식에는 HTML, 텍스트, DOC 및 EPS이 포함됩니다. PDF 문서를 RTF로 변환할 때는 PDF 문서에 제출 단추와 같은 양식 요소가 포함되어 있지 않은지 확인하십시오. 양식 요소는 변환되지 않습니다.

>[!NOTE]
>
>PDF 생성 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-2}

PDF 문서를 지원되는 유형으로 변환하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. PDF 클라이언트 생성을 참조하십시오.
1. 변환할 PDF 문서를 검색합니다.
1. PDF 문서를 변환합니다.
1. 변환된 파일을 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**PDF 클라이언트 생성**

PDF 생성 작업을 프로그래밍 방식으로 수행하려면 먼저 PDF 서비스 생성 클라이언트를 만들어야 합니다. Java API를 사용하는 경우 `GeneratePdfServiceClient` 개체. 웹 서비스 API를 사용하는 경우 `GeneratePDFServiceService` 개체.

**변환할 PDF 문서 검색**

PDF 문서를 검색하여 이미지가 아닌 형식으로 변환합니다.

**PDF 문서 변환**

서비스 클라이언트를 만든 후 PDF 내보내기 작업을 호출할 수 있습니다. 이 작업에는 대상 문서에 대한 경로를 포함하여 변환할 문서에 대한 정보가 필요합니다.

**변환된 파일을 저장합니다.**

변환된 파일을 저장합니다. 예를 들어 PDF 문서를 RTF 파일로 변환하는 경우 변환된 문서를 RTF 파일로 저장합니다.

**추가 참조**

[Java API를 사용하여 PDF 문서를 RTF 파일로 변환](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-java-api)

[웹 서비스 API를 사용하여 PDF 문서를 RTF 파일로 변환](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF 서비스 API 빠른 시작 생성](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Java API를 사용하여 PDF 문서를 RTF 파일로 변환 {#convert-a-pdf-document-to-a-rtf-file-using-the-java-api}

PDF API 생성(Java)을 사용하여 PDF 문서를 RTF 파일로 변환:

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-generatepdf-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. PDF 클라이언트 생성을 참조하십시오.

   만들기 `GeneratePdfServiceClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.

1. 변환할 PDF 문서를 검색합니다.

   * 만들기 `java.io.FileInputStream` 생성자를 사용하여 변환할 PDF 문서를 나타내는 개체입니다. PDF 문서의 위치를 지정하는 문자열 값을 전달합니다.
   * 만들기 `com.adobe.idp.Document` 개체를 생성자를 사용하고 `java.io.FileInputStream` 개체.

1. PDF 문서를 변환합니다.

   호출 `GeneratePdfServiceClient` 개체 `exportPDF2` 메서드를 실행하고 다음 값을 전달합니다.

   * A `com.adobe.idp.Document` 변환할 PDF 파일을 나타내는 개체입니다.
   * A `java.lang.String` 변환할 파일의 이름이 포함된 개체입니다.
   * A `java.lang.String` Adobe PDF 설정의 이름이 포함된 개체입니다.
   * A `ConvertPDFFormatType` 변환할 대상 파일 형식을 지정하는 개체입니다.
   * 선택 사항입니다 `com.adobe.idp.Document` PDF 문서를 생성하는 동안 적용할 설정이 포함된 객체입니다.

   다음 `exportPDF2` 메서드가 다음을 반환합니다. `ExportPDFResult` 변환된 파일을 포함하는 개체입니다.

1. PDF 문서를 변환합니다.

   새로 만든 파일을 가져오려면 다음 작업을 수행합니다.

   * 호출 `ExportPDFResult` 개체 `getConvertedDocument` 메서드를 사용합니다. 이 값은 `com.adobe.idp.Document` 개체.
   * 호출 `com.adobe.idp.Document` 개체 `copyToFile` 메서드를 사용하여 새 문서를 추출할 수 있습니다.

**추가 참조**

[단계 요약](converting-file-formats-pdf.md#summary-of-steps)

[빠른 시작(SOAP 모드): Java API를 사용하여 HTML 콘텐츠를 PDF 문서로 변환](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 PDF 문서를 RTF 파일로 변환 {#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api}

PDF API 생성(웹 서비스)을 사용하여 PDF 문서를 RTF 파일로 변환:

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용하는지 확인합니다. `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` AEM Forms을 호스팅하는 서버의 IP 주소입니다.

1. PDf 클라이언트 생성을 참조하십시오.

   * 만들기 `GeneratePDFServiceClient` 기본 생성자를 사용하여 개체를 작성합니다.
   * 만들기 `GeneratePDFServiceClient.Endpoint.Address` 을 사용하여 개체 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`.) 를 사용할 필요가 없습니다. `lc_version` 특성. 단, 을 지정합니다. `?blob=mtom`.
   * 만들기 `System.ServiceModel.BasicHttpBinding` 의 값을 가져와서 개체 `GeneratePDFServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스트 `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름 할당 `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`.
      * 해당 암호 값을 필드에 할당합니다. `GeneratePDFServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 지정 `HttpClientCredentialType.Basic` 필드에 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 상수 값 지정 `BasicHttpSecurityMode.TransportCredentialOnly` 필드에 `BasicHttpBindingSecurity.Security.Mode`.

1. 변환할 PDF 문서를 검색합니다.

   * 만들기 `BLOB` 개체를 만들 때 사용됩니다. 다음 `BLOB` 객체는 변환된 PDF 문서를 저장하는 데 사용됩니다.
   * 만들기 `System.IO.FileStream` PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 콘텐츠를 저장하는 바이트 배열 만들기 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채우기 `System.IO.FileStream` 개체 `Read` 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하는 방법.
   * 채우기 `BLOB` 에 할당하여 오브젝트 `MTOM` 속성을 바이트 배열의 내용으로 지정합니다.

1. PDF 문서를 변환합니다.

   호출 `GeneratePDFServiceServiceWse` 개체 `ExportPDF2` 메서드를 실행하고 다음 값을 전달합니다.

   * A `BLOB` 변환할 PDF 파일을 나타내는 개체입니다.
   * 변환할 파일의 경로 이름이 포함된 문자열입니다.
   * A `java.lang.String` 파일 위치를 지정하는 개체입니다.
   * 변환의 대상 파일 유형을 지정하는 문자열 객체입니다. 지정 `RTF`.
   * 선택 사항입니다 `BLOB` PDF 문서를 생성하는 동안 적용할 설정이 포함된 객체입니다.
   * 유형의 출력 매개 변수 `BLOB` 이 채우는 사람: `ExportPDF2` 메서드를 사용합니다. 다음 `ExportPDF2` 메서드는 변환된 문서로 이 개체를 채웁니다. (이 매개 변수 값은 웹 서비스 호출에만 필요합니다.)

1. 변환된 파일을 저장합니다.

   * 를 할당하여 변환된 RTF 문서 검색 `BLOB` 개체 `MTOM` 필드를 바이트 배열로 바꿉니다. 바이트 배열은 변환된 RTF 문서를 나타냅니다. 다음을 사용하십시오. `BLOB` 의 출력 매개 변수로 사용되는 개체입니다 `ExportPDF2` 메서드를 사용합니다.
   * 만들기 `System.IO.FileStream` 해당 생성자를 호출하여 개체를 작성합니다. RTF 파일의 위치를 나타내는 문자열 값을 전달합니다.
   * 만들기 `System.IO.BinaryWriter` 개체를 호출하고 `System.IO.FileStream` 개체.
   * RTF 파일에 바이트 배열의 내용을 `System.IO.BinaryWriter` 개체 `Write` 메서드 및 바이트 배열 전달.

**추가 참조**

[단계 요약](converting-file-formats-pdf.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 추가 기본 파일 형식에 대한 지원 추가 {#adding-support-for-additional-native-file-formats}

이 섹션에서는 추가 기본 파일 형식에 대한 지원을 추가하는 방법에 대해 설명합니다. 이 비디오에서는 PDF 생성 서비스와 이 서비스가 기본 파일 형식을 PDF으로 변환하는 데 사용하는 기본 애플리케이션 간의 상호 작용에 대한 개요를 제공합니다.

이 섹션에서는 다음 사항에 대해서도 설명합니다.

* 이 제품이 이미 기본 파일 형식을 PDF으로 변환하는 데 사용하는 기본 애플리케이션에 PDF 생성 서비스가 제공하는 응답을 수정하는 방법
* PDF 생성 서비스, AppMon(PDF 서비스 응용 프로그램 모니터 생성) 구성 요소 및 Microsoft Word와 같은 기본 응용 프로그램 간의 상호 작용
* XML 문법이 이러한 상호 작용 시 수행하는 역할

### 구성 요소 상호 작용 {#component-interactions}

PDF 생성 서비스는 파일 형식과 연관된 응용 프로그램을 호출한 다음 기본 프린터를 사용하여 문서를 인쇄하기 위해 응용 프로그램과 상호 작용하여 기본 파일 형식을 변환합니다. 기본 프린터를 Adobe PDF 프린터로 설정해야 합니다.

이 그림은 기본 애플리케이션 지원과 관련된 구성 요소 및 드라이버를 보여 줍니다. 또한 상호 작용에 영향을 미치는 XML 문법에 대해서도 언급하고 있다.

기본 파일 변환을 위한 구성 요소 상호 작용

이 문서에서는 다음 용어를 사용합니다 *기본 애플리케이션* Microsoft Word와 같은 기본 파일 형식을 생성하는 데 사용되는 응용 프로그램을 나타냅니다.

*AppMon* 는 사용자가 기본 애플리케이션에서 제공하는 대화 상자를 탐색하는 것과 같은 방식으로 기본 애플리케이션과 상호 작용하는 엔터프라이즈 구성 요소입니다. AppMon에서 Microsoft Word와 같은 애플리케이션에 이러한 순차적 작업이 포함된 파일을 열고 인쇄하도록 지시하는 데 사용되는 XML 문법입니다.

1. 파일 > 열기를 선택하여 파일 열기
1. 열기(Open) 대화상자가 나타나는지 확인하고 나타나지 않으면 오류를 처리합니다.
1. 파일 이름 필드에 파일 이름을 입력한 다음 열기 버튼 클릭
1. 파일이 실제로 열리는지 확인
1. [파일] > [인쇄]를 선택하여 [인쇄] 대화 상자 열기
1. 인쇄 대화 상자가 나타나는지 확인합니다.

AppMon은 표준 Win32 API를 사용하여 서드파티 애플리케이션과 상호 작용하여 키-스트로크 및 마우스 클릭과 같은 UI 이벤트를 전송하므로 이러한 애플리케이션을 제어하여 PDF 파일을 생성하는 데 유용합니다.

이러한 Win32 API의 제한으로 인해 AppMon은 이러한 UI 이벤트를 부동 메뉴 막대(TextPad와 같은 일부 응용 프로그램에 있음) 및 Win32 API를 사용하여 콘텐츠를 검색할 수 없는 특정 종류의 대화 상자와 같은 일부 특정 종류의 창에 발송할 수 없습니다.

부동 메뉴 모음을 시각적으로 쉽게 식별할 수 있지만 시각적 검사만으로 특수 유형의 대화 상자를 식별할 수는 없습니다. Microsoft Spy++(Microsoft Visual C++ 개발 환경의 일부) 또는 이와 동등한 WinID(다음에서 무료로 다운로드할 수 있음)와 같은 타사 애플리케이션이 필요합니다. [https://www.dennisbabkin.com/php/download.php?what=WinID](https://www.dennisbabkin.com/php/download.php?what=WinID)) 대화 상자를 검사하여 AppMon이 표준 Win32 API를 사용하여 상호 작용할 수 있는지 확인합니다.

WinID가 텍스트, 하위 창, 창 클래스 ID 등과 같은 대화 상자 콘텐츠를 추출할 수 있는 경우 AppMon도 동일한 작업을 수행할 수 있습니다.

이 표에는 기본 파일 형식 인쇄에 사용되는 정보 유형이 나열되어 있습니다.

<table>
 <thead>
  <tr>
   <th><p>정보 유형</p></th>
   <th><p>설명</p></th>
   <th><p>네이티브 파일과 관련된 항목 수정/만들기 </p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>관리 설정 </p></td>
   <td><p>PDF 설정, 보안 설정 및 파일 유형 설정을 포함합니다. </p><p>파일 형식 설정은 파일 이름 확장자를 해당 기본 응용 프로그램과 연결합니다. 파일 형식 설정은 기본 파일을 인쇄하는 데 사용되는 기본 응용 프로그램 설정도 지정합니다. </p></td>
   <td><p>이미 지원되는 기본 응용 프로그램의 설정을 변경하려면 시스템 관리자가 관리 콘솔에서 파일 유형 설정을 설정합니다. </p><p>새 기본 파일 형식에 대한 지원을 추가하려면 파일을 수동으로 편집해야 합니다. (참조: <a href="converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format">기본 파일 형식에 대한 지원 추가 또는 수정</a>.) </p></td>
  </tr>
  <tr>
   <td><p>스크립트 </p></td>
   <td><p>PDF 생성 서비스와 기본 응용 프로그램 간의 상호 작용을 지정합니다. 이러한 상호 작용은 일반적으로 애플리케이션이 Adobe PDF 드라이버에 파일을 인쇄하도록 합니다. </p><p>스크립트에는 기본 응용 프로그램에서 특정 대화 상자를 열고 해당 대화 상자의 필드 및 단추에 특정 응답을 제공하는 지침이 포함되어 있습니다. </p></td>
   <td><p>PDF 생성 서비스에는 지원되는 모든 기본 응용 프로그램에 대한 스크립트 파일이 포함되어 있습니다. XML 편집 응용 프로그램을 사용하여 이러한 파일을 수정할 수 있습니다.</p><p>새 기본 응용 프로그램에 대한 지원을 추가하려면 새 스크립트 파일을 만들어야 합니다. (참조: <a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">기본 응용 프로그램에 대한 추가 대화 상자 XML 파일 생성 또는 수정</a>.) </p></td>
  </tr>
  <tr>
   <td><p>일반 대화 상자 지침 </p></td>
   <td><p>여러 응용 프로그램에 공통되는 대화 상자에 응답하는 방법을 지정합니다. 이러한 대화 상자는 운영 체제, 도우미 응용 프로그램(예: PDFMaker) 및 드라이버에 의해 생성됩니다. </p><p>이 정보가 포함된 파일은 appmon.global.en_US.xml입니다.</p></td>
   <td><p>이 파일을 수정하지 마십시오. </p></td>
  </tr>
  <tr>
   <td><p>애플리케이션별 대화 상자 지침</p></td>
   <td><p>응용 프로그램별 대화 상자에 응답하는 방법을 지정합니다. </p><p>이 정보가 포함된 파일은 appmon입니다.<i>"[appname]"</i>.dialog.<i>"[locale]"</i>.xml (예: appmon.word.en_US.xml)</p></td>
   <td><p>이 파일을 수정하지 마십시오. </p><p>새 기본 응용 프로그램에 대한 대화 상자 지침을 추가하려면 <a href="converting-file-formats-pdf.md#creating_or_modifying_an_additional_dialog_xml_file_for_a_native_application">기본 응용 프로그램에 대한 추가 대화 상자 XML 파일 생성 또는 수정</a>.</p></td>
  </tr>
  <tr>
   <td><p>애플리케이션별 추가 대화 상자 지침 </p></td>
   <td><p>응용 프로그램별 대화 상자 지침에 대한 재정의 및 추가 사항을 지정합니다. 섹션에는 이러한 정보의 예가 나와 있습니다. </p><p>이 정보가 포함된 파일은 appmon입니다.<i>"[appname]"</i>.addition.<i>"[locale]"</i>.xml. 예로는 appmon.addition.en_US.xml이 있습니다.</p></td>
   <td><p>이 유형의 파일은 XML 편집 응용 프로그램을 사용하여 만들고 수정할 수 있습니다. (참조: <a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">기본 응용 프로그램에 대한 추가 대화 상자 XML 파일 생성 또는 수정</a>.) </p><p><strong>중요 사항</strong>: 서버에서 지원할 각 기본 애플리케이션에 대한 추가 애플리케이션별 대화 상자 지침을 만들어야 합니다. </p></td>
  </tr>
 </tbody>
</table>

### 스크립트 및 대화 상자 XML 파일 정보 {#about-the-script-and-dialog-xml-files}

스크립트 XML 파일은 사용자가 응용 프로그램 대화 상자를 탐색하는 것과 같은 방식으로 PDF 생성 서비스에 응용 프로그램 대화 상자를 탐색하도록 지시합니다. 또한 스크립트 XML 파일은 단추 누름, 확인란 선택 또는 선택 해제, 메뉴 항목 선택 등의 작업을 수행하여 PDF 생성 서비스가 대화 상자에 응답하도록 합니다.

반면 대화 상자 XML 파일은 스크립트 XML 파일에 사용된 것과 동일한 유형의 작업이 있는 대화 상자에 응답합니다.

#### 대화 상자 및 창 요소 용어 {#dialog-box-and-window-element-terminology}

이 섹션과 다음 섹션에서는 설명하는 관점에 따라 대화 상자와 대화 상자에 포함된 구성 요소에 대해 서로 다른 용어를 사용합니다. 대화 상자 구성 요소는 단추, 필드 및 콤보 상자와 같은 항목입니다.

이 섹션과 다음 섹션에서 사용자의 관점에서 대화상자와 해당 구성 요소를 설명할 때 다음과 같은 용어가 사용됩니다. *대화 상자*, *단추*, *필드*, 및 *콤보 상자* 를 사용합니다.

이 섹션과 다음 섹션에서 내부 표현의 관점에서 대화상자와 해당 구성 요소를 설명할 때 *창 요소* 를 사용합니다. 창 요소의 내부 표현은 계층입니다. 여기서 각 창 요소 인스턴스는 레이블로 식별됩니다. window 요소 인스턴스는 해당 실제 특성과 비헤이비어도 설명합니다.

사용자의 관점에서 볼 때 대화 상자와 해당 구성 요소는 서로 다른 동작을 보여 주며, 일부 대화 상자 요소는 활성화될 때까지 숨겨집니다. 내부 재현의 관점에서 보면, 그러한 행동 문제는 존재하지 않는다. 예를 들어, 대화 상자의 내부 표현은 대화 상자 내에서 컴포넌트가 중첩된다는 점을 제외하면 포함된 컴포넌트의 내부 표현과 유사합니다.

이 섹션에서는 AppMon에 지침을 제공하는 XML 요소에 대해 설명합니다. 이러한 요소에는 다음과 같은 이름이 있습니다 `dialog` 요소 및 `window` 요소를 생성하지 않습니다. 이 문서에서는 XML 요소를 구별하기 위해 고정 폭 글꼴을 사용합니다. 다음 `dialog` 요소는 XML 스크립트 파일이 의도적으로 또는 실수로 표시될 수 있는 대화 상자를 식별합니다. 다음 `window` 요소는 창 요소(대화 상자 또는 대화 상자의 구성 요소)를 식별합니다.

#### 계층 {#hierarchy}

이 다이어그램은 스크립트와 대화 상자 XML의 계층 구조를 보여 줍니다. 스크립트 XML 파일은 window.xsd 스키마를 포함하는(XML 의미의) script.xsd 스키마를 준수합니다. 마찬가지로 대화 상자 XML 파일은 window.xsd 스키마도 포함하는 dialogs.xsd 스키마를 따릅니다.

![as_as_xml_hierarchy](assets/as_as_xml_hierarchy.png)

스크립트 및 대화 상자 XML 계층

#### 스크립트 XML 파일 {#script-xml-files}

A *스크립트 XML 파일* 기본 응용 프로그램이 특정 창 요소로 이동한 다음 해당 요소에 대한 응답을 제공하도록 지정하는 일련의 단계를 지정합니다. 대부분의 응답은 사용자가 해당 대화 상자의 필드, 콤보 상자 또는 단추에 제공하는 입력에 해당하는 텍스트 또는 키 입력입니다.

PDF 생성 서비스의 스크립트 XML 파일 지원 목적은 기본 응용 프로그램이 기본 파일을 인쇄하도록 하는 것입니다. 그러나 스크립트 XML 파일을 사용하여 사용자가 기본 애플리케이션의 대화 상자와 상호 작용할 때 수행할 수 있는 모든 작업을 수행할 수 있습니다.

스크립트 XML 파일의 단계는 분기 없이 순서대로 실행됩니다. 지원되는 유일한 조건부 테스트는 시간 초과/다시 시도에 대한 것으로, 특정 기간 내에 및 특정 재시도 횟수 후에 단계가 성공적으로 완료되지 않으면 스크립트가 종료됩니다.

단계들이 순차적인 것 외에도, 단계 내의 명령어들은 또한 순서대로 실행된다. 단계 및 지침이 사용자가 동일한 단계를 수행하는 순서를 반영하는지 확인해야 합니다.

스크립트 XML 파일의 각 단계는 해당 단계의 명령이 성공적으로 수행될 경우 표시될 것으로 예상되는 창 요소를 식별합니다. 스크립트 단계를 실행하는 동안 예기치 않은 대화 상자가 나타나면 PDF 생성 서비스는 다음 섹션에 설명된 대로 대화 상자 XML 파일을 검색합니다.

#### 대화 상자 XML 파일 {#dialog-xml-files}

기본 응용 프로그램을 실행하면 기본 응용 프로그램이 표시 모드인지 또는 보이지 않는 모드인지에 관계없이 표시되는 서로 다른 대화 상자가 표시됩니다. 대화 상자는 운영 체제 또는 응용 프로그램 자체에서 생성할 수 있습니다. 기본 응용 프로그램이 PDF 생성 서비스의 제어로 실행될 때 시스템 및 기본 응용 프로그램 대화 상자가 보이지 않는 창에 표시됩니다.

A *대화 상자 XML 파일* PDF 서비스 생성이 시스템 또는 기본 응용 프로그램 대화 상자에 응답하는 방식을 지정합니다. 대화 상자 XML 파일을 사용하면 PDF 생성 서비스가 전환 프로세스를 용이하게 하는 방식으로 메시지가 표시되지 않는 대화 상자에 응답할 수 있습니다.

시스템 또는 기본 응용 프로그램에 현재 실행 중인 스크립트 XML 파일이 처리하지 않는 대화 상자가 표시되면 PDF 생성 서비스는 대화 상자 XML 파일을 이 순서로 검색하여 일치하는 항목을 찾으면 중지합니다.

* appmon.`[appname]`.additional.`[locale]`.xml
* appmon.`[appname]`.`[locale]`.xml (이 파일을 수정하지 마십시오.)
* appmon.global.`[locale]`.xml (이 파일을 수정하지 마십시오.)

PDF 생성 서비스가 대화 상자에 대해 일치하는 항목을 찾으면 대화 상자에 대해 지정된 키 입력이나 기타 작업을 보내어 이를 무시합니다. 대화 상자에 대한 지침이 중단 메시지를 지정하면 PDF 생성 서비스는 현재 실행 중인 작업을 종료하고 오류 메시지를 생성합니다. 이러한 중단 메시지는 다음에서 지정됩니다. `abortMessage` 요소를 스크립트 XML 문법에 포함합니다.

PDF 생성 서비스에 이전에 나열된 파일에서 설명되지 않은 대화 상자가 나타나면 PDF 생성 서비스는 대화 상자의 캡션을 로그 파일 항목에 통합합니다. 현재 실행 중인 작업이 결국 시간 초과됩니다. 그런 다음 로그 파일의 정보를 사용하여 기본 응용 프로그램에 대한 추가 대화 상자 XML 파일에 새 명령을 작성할 수 있습니다.

### 기본 파일 형식에 대한 지원 추가 또는 수정 {#adding-or-modifying-support-for-a-native-file-format}

이 섹션에서는 다른 기본 파일 형식을 지원하거나 이미 지원되는 기본 파일 형식에 대한 지원을 수정하기 위해 수행해야 하는 작업에 대해 설명합니다.

지원을 추가하거나 수정하려면 먼저 다음 작업을 완료해야 합니다.

#### 창 요소 식별을 위한 도구 선택 {#choosing-a-tool-for-identifying-window-elements}

대화 상자 및 스크립트 XML 파일을 사용하려면 대화 상자나 스크립트 요소가 응답하는 창 요소(대화 상자, 필드 또는 기타 대화 요소)를 식별해야 합니다. 예를 들어 스크립트가 기본 응용 프로그램에 대한 메뉴를 호출한 후 스크립트는 해당 메뉴에서 키 입력이나 작업을 적용할 창 요소를 식별해야 합니다.

제목 표시줄에 표시되는 캡션을 사용하여 대화 상자를 쉽게 식별할 수 있습니다. 그러나 하위 수준의 창 요소를 식별하려면 Microsoft Spy++와 같은 도구를 사용해야 합니다. 하위 수준의 창 요소는 명확하지 않은 다양한 속성을 통해 식별할 수 있습니다. 추가적으로, 각각의 네이티브 애플리케이션은 그 윈도우 요소를 상이하게 식별할 수 있다. 따라서 창 요소를 식별하는 방법에는 여러 가지가 있습니다. 다음은 창 요소 식별을 고려하는 제안된 순서입니다.

1. 고유한 경우 캡션 자체
1. 제공된 대화 상자에 대해 고유하거나 고유하지 않을 수 있는 컨트롤 ID
1. 클래스 이름(고유하거나 고유하지 않을 수 있음)

이 세 가지 속성 중 어느 하나 또는 이들의 조합을 이용하여 창을 식별할 수 있다.

속성이 캡션을 식별하지 못하는 경우 대신 상위와 관련된 인덱스를 사용하여 창 요소를 식별할 수 있습니다. An *index* 형제 창 요소를 기준으로 창 요소의 위치를 지정합니다. 색인이 콤보 상자를 식별하는 유일한 방법인 경우가 많습니다.

다음 문제를 숙지하십시오.

* Microsoft Spy++는 앰퍼샌드(&amp;)를 사용하여 캡션의 바로 가기 키를 식별하여 캡션을 표시합니다. 예를 들어 Spy++는 하나의 인쇄 대화 상자에 대한 캡션을 다음과 같이 표시합니다. `Pri&nt`: 핫키가 *n*. 스크립트 및 대화 상자 XML 파일의 캡션 제목에는 앰퍼샌드를 생략해야 합니다.
* 일부 캡션에는 줄 바꿈이 포함됩니다. PDF 생성 서비스에서 줄 바꿈을 식별할 수 없습니다. 캡션에 줄 바꿈이 포함된 경우 캡션을 충분히 포함시켜 다른 메뉴 항목과 구분한 다음 생략된 부분에 정규 표현식을 사용합니다. 예: ( `^Long caption title$`). (참조: [캡션 속성에서 정규 표현식 사용](converting-file-formats-pdf.md#using-regular-expressions-in-caption-attributes).)
* 예약된 XML 문자에 문자 엔티티(이스케이프 시퀀스라고도 함)를 사용합니다. 예를 들어, `&` 앰퍼샌드의 경우 `<` 및 `>` 보다 작음 및 보다 큼 기호에 대해 `&apos;` 아포스트로피 `&quot;` 따옴표의 경우.

대화 상자 또는 스크립트 XML 파일에서 작업하려는 경우 응용 프로그램 Microsoft Spy++를 설치해야 합니다.

#### 대화 상자 및 스크립트 파일 패키징 해제 {#unpackaging-the-dialog-and-script-files}

대화 상자 및 스크립트 파일은 appmondata.jar 파일에 있습니다. 이러한 파일을 수정하거나 새 스크립트 또는 대화 상자 파일을 추가하기 전에 이 JAR 파일의 패키지를 해제해야 합니다. 예를 들어 EditPlus 응용 프로그램에 대한 지원을 추가하려고 한다고 가정합니다. appmon.editplus.script.en_US.xml 및 appmon.editplus.script.addition.en_US.xml이라는 두 개의 XML 파일을 만듭니다. 이러한 XML 스크립트는 아래에 지정된 대로 두 위치의 adobe-appmondata.jar 파일에 추가해야 합니다.

* adobe-livecycle-native-jboss-x86_win32.ear > adobe-Native2PDFSvc.war\WEB-INF\lib > adobe-native.jar > Native2PDFSvc-native.jar\bin > adobe-appmondata.jar\com\adobe\appmon. adobe-livecycle-native-jboss-x86_win32.ear 파일은 의 내보내기 폴더에 있습니다. `[AEM forms install directory]\configurationManager`. (AEM Forms이 다른 J2EE 애플리케이션 서버에 배포된 경우 adobe-livecycle-native-jboss-x86_win32.ear 파일을 J2EE 애플리케이션 서버에 해당하는 EAR 파일로 바꿉니다.)
* adobe-generatepdf-dsc.jar > adobe-appmondata.jar\com\adobe\appmon (adobe-appmondata.jar 파일은 adobe-generatepdf-dsc.jar 파일 내에 있음). adobe-generatepdf-dsc.jar 파일은 `[AEM forms install directory]\deploy` 폴더를 삭제합니다.

이러한 XML 파일을 adobe-appmondata.jar 파일에 추가한 후 GeneratePDF 구성 요소를 다시 배포해야 합니다. 대화 상자 및 스크립트 XML 파일을 adobe-appmondata.jar 파일에 추가하려면 다음 작업을 수행합니다.

1. WinZip 또는 WinRAR과 같은 도구를 사용하여 adobe-livecycle-native-jboss-x86_win32.earfile > adobe-Native2PDFSvc.war\WEB-INF\lib > adobe-native.jar > Native2PDFSvc-native.jar\bin > adobe-appmondata.jar 파일을 엽니다.
1. 대화 상자 및 스크립트 XML 파일을 appmondata.jar 파일에 추가하거나 이 파일의 기존 XML 파일을 수정합니다. (참조: [기본 응용 프로그램에 대한 스크립트 XML 파일 생성 또는 수정](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)및 [기본 응용 프로그램에 대한 추가 대화 상자 XML 파일 생성 또는 수정](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application).)
1. WinZip 또는 WinRAR과 같은 도구를 사용하여 adobe-generatepdf-dsc.jar > adobe-appmondata.jar을 엽니다.
1. 대화 상자 및 스크립트 XML 파일을 appmondata.jar 파일에 추가하거나 이 파일의 기존 XML 파일을 수정합니다. (참조: [기본 응용 프로그램에 대한 스크립트 XML 파일 생성 또는 수정](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)및 [기본 응용 프로그램에 대한 추가 대화 상자 XML 파일 생성 또는 수정](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application).) XML 파일을 adobe-appmondata.jar 파일에 추가한 후 새 adobe-appmondata.jar 파일을 adobe-generatepdf-dsc.jar 파일에 넣습니다.
1. 추가 기본 파일 형식에 대한 지원을 추가한 경우 응용 프로그램의 경로를 제공하는 시스템 환경 변수를 만듭니다(참조) [기본 응용 프로그램을 찾기 위한 환경 변수 만들기](converting-file-formats-pdf.md#creating-an-environment-variable-to-locate-the-native-application).)

**GeneratePDF 구성 요소를 재배포하려면**

1. 워크벤치에 로그인합니다.
1. 선택 **창** > **보기 표시** > **구성 요소**. 이 작업을 수행하면 구성 요소 보기가 Workbench에 추가됩니다.
1. GeneratePDF 구성 요소를 마우스 오른쪽 단추로 클릭하고 **구성 요소 중지**.
1. 구성 요소가 중지되면 마우스 오른쪽 단추를 클릭하고 구성 요소 제거 를 선택하여 제거합니다.
1. 마우스 오른쪽 단추 클릭 **구성 요소** 아이콘 및 선택 **구성 요소 설치**.
1. 수정된 adobe-generatepdf-dsc.jar 파일을 찾아 선택한 다음 열기 를 클릭합니다. GeneratePDF 구성 요소 옆에 빨간색 사각형이 표시됩니다.
1. GeneratePDF 구성 요소를 확장하고 Service Descriptors 를 선택한 다음 GeneratePDFservice 를 마우스 오른쪽 단추로 클릭하고 Activate Service 를 선택합니다.
1. 표시되는 구성 대화 상자에서 적용 가능한 구성 값을 입력합니다. 이 값을 비워 두면 기본 구성 값이 사용됩니다.
1. GeneratePDF를 마우스 오른쪽 단추로 클릭하고 구성 요소 시작을 선택합니다.
1. Active Services 를 확장합니다. 실행 중인 경우 서비스 이름 옆에 녹색 화살표가 나타납니다. 그렇지 않으면 서비스가 중지된 상태입니다.
1. 서비스가 중지된 상태인 경우 서비스 이름을 마우스 오른쪽 단추로 클릭하고 서비스 시작을 선택합니다.

### 기본 응용 프로그램에 대한 스크립트 XML 파일 생성 또는 수정 {#creating-or-modifying-a-script-xml-file-for-a-native-application}

파일을 새 기본 응용 프로그램으로 보내려면 해당 응용 프로그램에 대한 스크립트 XML 파일을 만들어야 합니다. PDF 생성 서비스가 이미 지원되는 기본 응용 프로그램과 상호 작용하는 방법을 수정하려면 해당 응용 프로그램의 스크립트를 수정해야 합니다.

스크립트에는 기본 애플리케이션의 창 요소를 탐색하고 해당 요소에 특정 응답을 제공하는 지침이 포함되어 있습니다. 이 정보가 포함된 파일은 다음과 같습니다. `appmon.`[appname]&quot; `.script.`[로케일]`.xml`. 예를 들어 appmon.notepad.script.en_US.xml이 있습니다.

#### 스크립트가 실행해야 하는 단계 식별 {#identifying-steps-the-script-must-execute}

기본 응용 프로그램을 사용하여 탐색해야 하는 창 요소와 문서를 인쇄하기 위해 수행해야 하는 각 응답을 결정합니다. 모든 응답에서 나타나는 대화 상자를 확인합니다. 단계는 다음 단계와 유사합니다.

1. [파일] > [열기]를 선택합니다.
1. 경로를 지정한 다음 [열기]를 클릭합니다.
1. 메뉴 표시줄에서 파일 > 인쇄를 선택합니다.
1. 프린터에 필요한 속성을 지정합니다.
1. 인쇄를 선택하고 다른 이름으로 저장 대화 상자가 나타날 때까지 기다립니다. 다른 이름으로 저장 대화 상자는 PDF 생성 서비스에서 PDF 파일의 대상을 지정하는 데 필요합니다.

#### 캡션 속성에 지정된 대화 상자 식별 {#identifying-the-dialogs-specified-in-caption-attributes}

Microsoft Spy++를 사용하여 기본 애플리케이션에서 창 요소 속성의 ID를 가져옵니다. 스크립트를 작성하려면 이러한 ID가 있어야 합니다.

#### 캡션 속성에서 정규 표현식 사용 {#using-regular-expressions-in-caption-attributes}

캡션 사양에 정규 표현식을 사용할 수 있습니다. PDF 생성 서비스에서는 `java.util.regex.Matcher` 클래스에서 정규식을 지원합니다. 해당 유틸리티는에 설명된 정규 표현식을 지원합니다. `java.util.regex.Pattern`.

**메모장 배너에서 메모장 앞에 오는 파일 이름을 포함하는 정규 표현식**

```xml
 <!-- The regular expression ".*Notepad" means any number of non-terminating characters followed by Notepad. -->
 <step>
     <expectedWindow>
         <window caption=".*Notepad"/>
     </expectedWindow>
 </step>
```

**인쇄와 인쇄 설정을 구분하는 정규 표현식**

```xml
 <!-- This regular expression differentiates the Print dialog box from the Print Setup dialog box. The "^" specifies the beginning of the line, and the "$" specifies the end of the line. -->
 <windowList>
     <window controlID="0x01" caption="^Print$" action="press"/>
 </windowList>
```

#### window 및 windowList 요소 순서 지정 {#ordering-the-window-and-windowlist-elements}

주문해야 합니다. `window` 및 `windowList` 요소를 다음과 같이 지정합니다.

* 여러 개인 경우 `window` 요소는 다음에 하위 요소로 표시됩니다. `windowList` 또는 `dialog` 요소, 순서 지정 `window` 요소(내림차순, 길이 포함) `caption` 순서대로 위치를 나타내는 이름.
* 여러 개인 경우 `windowList` 요소에 나타나는 문자 `window` 요소, 순서 지정 `windowList` 요소(내림차순, 길이 포함) `caption` 첫 번째 속성 `indexes/`순서에서 위치를 나타내는 요소입니다.

**대화 상자 파일에서 창 요소 순서 지정**

```xml
 <!-- The caption attribute in the following window element is 40 characters long. It is the longest caption in this example, so its parent window element appears before the others. -->
 <window caption="Unexpected Failure in DebugActiveProcess">
     <…>
 </window>

 <!-- Caption length is 33 characters. -->
 <window caption="Adobe Acrobat - License Agreement">
     <…>
 </window>

 <!-- Caption length is 33 characters. -->
 <window caption="Microsoft Visual.*Runtime Library">
     <…>
 </window>

 <!-- The caption attribute in the following window element is 28 characters long. It is the shortest caption in this example, so its parent window element appears after the others. -->
 <window caption="Adobe Acrobat - Registration">
     <…>
 </window>
```

**windowList 요소 내에서 창 요소 순서 지정**

```xml
 <!-- The caption attribute in the following indexes element is 56 characters long. It is the longest caption in this example, so its parent window element appears before the others. -->
 <windowList>
     <window caption="Can&apos;t exit design mode because.* cannot be created"/>
     <window className="Button" caption="OK" action="press"/>
 </windowList>
 <windowList>
     <window caption="Do you want to continue loading the project?"/>
     <window className="Button" caption="No" action="press"/>
 </windowList>
 <windowList>
     <window caption="The macros in this project are disabled"/>
     <window className="Button" caption="OK" action="press"/>
 </windowList>
```

### 기본 응용 프로그램에 대한 추가 대화 상자 XML 파일 생성 또는 수정 {#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application}

이전에 지원되지 않았던 기본 응용 프로그램에 대한 스크립트를 만드는 경우 해당 응용 프로그램에 대한 추가 대화 상자 XML 파일도 만들어야 합니다. AppMon에서 사용하는 모든 기본 응용 프로그램에는 추가 대화 상자 XML 파일이 하나만 있어야 합니다. 요청하지 않은 대화 상자가 없는 경우에도 추가 대화 상자 XML 파일이 필요합니다. 추가 대화 상자에는 하나 이상의 대화 상자가 있어야 합니다. `window` 요소, 있더라도 `window` 요소는 자리 표시자에 불과합니다.

>[!NOTE]
>
>이 맥락에서 &#39;추가&#39;라는 용어는 다음의 내용을 의미한다 `appmon.[applicationname].addition.[locale].xml` 파일. 이러한 파일은 대화 상자 XML 파일에 대한 재정의 및 추가 사항을 지정합니다.

다음과 같은 목적으로 기본 응용 프로그램에 대한 추가 대화 상자 XML 파일을 수정할 수도 있습니다.

* 다른 응답을 사용하는 응용 프로그램의 대화 상자 XML 파일을 재정의하려면
* 해당 응용 프로그램의 대화 상자 XML 파일에서 언급되지 않은 대화 상자에 응답을 추가하려면

추가 dialogXML 파일을 식별하는 파일 이름은 입니다. `appmon.[appname].addition.[locale].xml`. 예로는 appmon.excel.addition.en_US.xml이 있습니다.

추가 대화 상자 XML 파일의 이름은 형식을 사용해야 합니다 `appmon.[applicationname].addition.[locale].xml`, 여기서 *applicationname* 는 XML 구성 파일 및 스크립트에 사용된 애플리케이션 이름과 정확히 일치해야 합니다.

>[!NOTE]
>
>native2pdfconfig.xml 구성 파일에 지정된 일반 응용 프로그램에 기본 대화 상자 XML 파일이 없습니다. 섹션 [기본 파일 형식에 대한 지원 추가 또는 수정](converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format) 에서는 이러한 세부 항목에 대해 설명합니다.

주문해야 합니다. `windowList` 에서 하위 요소로 표시되는 요소 `window` 요소를 생성하지 않습니다. (참조: [window 및 windowList 요소 순서 지정](converting-file-formats-pdf.md#ordering-the-window-and-windowlist-elements).)

### 일반 대화 상자 XML 파일 수정 {#modifying-the-general-dialog-xml-file}

일반 대화 상자 XML 파일을 수정하여 시스템에서 생성한 대화 상자에 응답하거나 여러 응용 프로그램에 공통되는 대화 상자에 응답할 수 있습니다.

#### XML 구성 파일에 파일 유형 항목 추가 {#adding-a-filetype-entry-in-the-xml-configuration-file}

이 절차에서는 파일 유형을 기본 응용 프로그램과 연결하기 위해 PDF 서비스 생성 구성 파일을 업데이트하는 방법을 설명합니다. 이 구성 파일을 업데이트하려면 관리 콘솔을 사용하여 구성 데이터를 파일로 내보내야 합니다. 구성 데이터의 기본 파일 이름은 native2pdfconfig.xml입니다.

**PDF 서비스 생성 구성 파일 업데이트**

1. 선택 **홈** > **서비스** > **Adobe PDF Generator** > **구성 파일**&#x200B;을 선택한 다음 을 선택합니다 **구성 내보내기**.
1. 수정 `filetype-settings` 필요한 경우 native2pdfconfig.xml 파일의 요소입니다.
1. 선택 **홈** > **서비스** > **Adobe PDF Generator** >**구성 파일**&#x200B;을 선택한 다음 을 선택합니다 **구성 가져오기**. 구성 데이터를 PDF 생성 서비스로 가져와서 이전 설정을 바꿉니다.

>[!NOTE]
>
>응용 프로그램의 이름은 `GenericApp` 요소 `name` 특성. 이 값은 해당 응용 프로그램에 대해 개발하는 스크립트에 지정된 해당 이름과 정확히 일치해야 합니다. 마찬가지로 `GenericApp` 요소 `displayName` 속성은 해당 스크립트와 정확히 일치해야 합니다. `expectedWindow` 창 캡션입니다. 이와 같은 등가성은 다음에 나타나는 정규 표현식을 해결한 후 평가됩니다. `displayName` 또는 `caption` 속성.

이 예제에서는 PDF 생성 서비스와 함께 제공된 기본 구성 데이터를 수정하여 메모장(Microsoft Word 아님)을 사용하여 확장명이 .txt인 파일을 처리하도록 했습니다. 이 수정 전에 Microsoft Word가 이러한 파일을 처리해야 하는 기본 애플리케이션으로 지정되었습니다.

**텍스트 파일을 메모장으로 보내기 위한 수정 사항(native2pdfconfig.xml)**

```xml
 <filetype-settings>

 <!-- Some native app file types were omitted for brevity. -->
 <!-- The following GenericApp element specifies Notepad as the native application that should be used to process files that have a txt file name extension. -->
             <GenericApp
                 extensions="txt"
                 name="Notepad" displayName=".*Notepad"/>
             <GenericApp
                 extensions="wpd"
                 name="WordPerfect" displayName="Corel WordPerfect"/>
             <GenericApp extensions="pmd,pm6,p65,pm"
                 name="PageMaker" displayName="Adobe PageMaker"/>
             <GenericApp extensions="fm"
                 name="FrameMaker" displayName="Adobe FrameMaker"/>
             <GenericApp extensions="psd"
                 name="Photoshop" displayName="Adobe Photoshop"/>
         </settings>
     </filetype-settings>
```

#### 기본 응용 프로그램을 찾기 위한 환경 변수 만들기 {#creating-an-environment-variable-to-locate-the-native-application}

기본 응용 프로그램 실행 파일의 위치를 지정하는 환경 변수를 만듭니다. 변수는 형식을 사용해야 합니다. `[applicationname]_PATH`, 여기서 *applicationname* 은(는) XML 구성 파일 및 스크립트에 사용된 애플리케이션 이름과 정확히 일치해야 하며, 여기서 경로에는 큰따옴표로 된 실행 파일의 경로가 포함됩니다. 이러한 환경 변수의 예는 다음과 같습니다. `Photoshop_PATH`.

새 환경 변수를 만든 후에는 PDF 생성 서비스가 배포된 서버를 다시 시작해야 합니다.

**Windows XP 환경에서 시스템 변수 만들기**

1. 선택 **Campaign 컨트롤 패널 > 시스템**.
1. 시스템 등록 정보 대화 상자에서 **고급** tab을 누른 다음 **환경 변수**.
1. 환경 변수 대화 상자의 시스템 변수에서 **신규**.
1. 새 시스템 변수 대화 상자의 **변수 이름** 상자에 형식을 사용하는 이름을 입력합니다 `[applicationname]_PATH`.
1. 다음에서 **변수 값** 상자에 응용 프로그램 실행 파일의 전체 경로와 파일 이름을 입력한 다음 **확인**. 예를 들어, 다음을 입력합니다. `c:\windows\Notepad.exe`
1. 환경 변수 대화 상자에서 **확인**.

**명령줄에서 시스템 변수 만들기**

1. 명령줄 창에서 다음 형식을 사용하여 변수 정의를 입력합니다.

   ```shell
            [applicationname]_PATH=[Full path name]
   ```

   예를 들어, 다음을 입력합니다. `NotePad_PATH=C:\WINDOWS\NOTEPAD.EXE`

1. 시스템 변수를 적용하려면 새 명령줄 프롬프트를 시작하십시오.

#### 파일 {#xml-files}

AEM Forms에는 PDF 생성 서비스에서 메모장을 사용하여 파일 확장명이 .txt인 파일을 처리하도록 하는 샘플 XML 파일이 포함되어 있습니다. 이 코드는 이 섹션에 포함되어 있습니다. 또한 이 섹션에 설명된 다른 사항을 수정해야 합니다.

#### 추가 대화 상자 XML 파일 {#additional-dialog-xml-file}

이 예에는 메모장 응용 프로그램에 대한 추가 대화 상자가 포함되어 있습니다. 이러한 대화 상자는 PDF 생성 서비스에서 지정한 대화 상자 외에 추가할 수 있습니다.

**메모장 대화 상자(appmon.notepad.addition.en_US.xml)**

```xml
 <dialogs app="Notepad" locale="en_US" version="7.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="dialogs.xsd">
     <window caption="Caption Title">
         <windowList>
             <window className="Button" caption="OK" action="press"/>
         </windowList>
     </window>
 </dialogs>
```

#### 스크립트 XML 파일 {#script-xml-file}

이 예제에서는 Adobe PDF 프린터를 사용하여 파일을 인쇄하기 위해 PDF 생성 서비스가 메모장과 상호 작용하는 방법을 지정합니다.

**메모장 스크립트 XML 파일(appmon.notepad.script.en_US.xml)**

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<!--
*
* ADOBE CONFIDENTIAL
* ___________________
* Copyright 2004 - 2005 Adobe Systems Incorporated
* All Rights Reserved.
*
* NOTICE:  All information contained herein is, and remains
* the property of Adobe Systems Incorporated and its suppliers,
* if any.  The intellectual and technical concepts contained
* herein are proprietary to Adobe Systems Incorporated and its
* suppliers and may be covered by U.S. and Foreign Patents,
* patents in process, and are protected by trade secret or copyright law.
* Dissemination of this information or reproduction of this material
* is strictly forbidden unless prior written permission is obtained
* from Adobe Systems Incorporated.
*-->

<!-- This file automates printing of text files via notepad to Adobe PDF printer. In order to see the complete hierarchy we recommend using the Microsoft Spy++ which details the properties of windows necessary to write scripts. In this sample there are total of eight steps-->

<application name="Notepad" version="9.0" locale="en_US" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="scripts.xsd">

    <!-- In this step we wait for the application window to appear -->
    <step>
        <expectedWindow>
            <window caption=".*Notepad"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the application window and send File->Open menu bar, menu item commands and the expectation is the windows Open dialog-->
    <step>
        <acquiredWindow>
            <window caption=".*Notepad">
                <virtualInput>
                    <menuBar>
                        <selection>
                            <name>File</name>
                        </selection>
                        <selection>
                            <name>Open...</name>
                        </selection>
                    </menuBar>
                </virtualInput>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Open"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the Open window and then select the 'Edit' widget and input the source path followed by clicking on the 'Open' button . The expectation of this 'action' is that the Open dialog will disappear -->
    <step>
        <acquiredWindow>
            <window caption="Open">
                <windowList>
                    <window className="ComboBoxEx32">
                        <windowList>
                            <window className="ComboBox">
                                <windowList>
                                <window className="Edit" action="inputSourcePath"/>
                                </windowList>
                            </window>
                        </windowList>
                    </window>
                </windowList>
                <windowList>
                    <window className="Button" caption="Open" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Open" action="disappear"/>
        </expectedWindow>
        <pause value="30"/>
    </step>

    <!-- In this step, we acquire the application window and send File->Print menu bar, menu item commands and the expectation is the windows Print dialog-->
    <step>
        <acquiredWindow>
            <window caption=".*Notepad">
                <virtualInput>
                    <menuBar>
                        <selection>
                            <name>File</name>
                        </selection>
                        <selection>
                            <name>Print...</name>
                        </selection>
                    </menuBar>
                </virtualInput>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Print">
        </window>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the Print dialog and click on the 'Preferences' button and the expected window in this case is the dialog with the caption '"Printing Preferences' -->
    <step>
        <acquiredWindow>
            <window caption="Print">
                <windowList>
                    <window caption="General">
                        <windowList>
                            <window className="Button" caption="Preferences" action="press"/>
                        </windowList>
                    </window>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Printing Preferences"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the dialog "Printing Preferences' and select the combo box which is the 10th child of window with caption '"Adobe PDF Settings' and select the first index. (Note: All indeces start with 0.) Besides this we uncheck the box which  has the caption '"View Adobe PDF results' and we click on the button OK. The expectation is that 'Printing Preferences' dialog disappears. -->
    <step>
        <acquiredWindow>
            <window caption="Printing Preferences">
                <windowList>
                    <window caption="Adobe PDF Settings">
                        <windowList>
                            <window className="Button" caption="View Adobe PDF results" action="uncheck"/>
                        </windowList>
                        <windowList>
                            <window className="Button" caption="Ask to Replace existing PDF file" action="uncheck"/>
                        </windowList>
                    </window>
                </windowList>
                <windowList>
                    <window className="Button" caption="OK" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Printing Preferences" action="disappear"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the 'Print' dialog and click on the Print button. The expectation is that the dialog with caption 'Print' disappears. In this case we use the regular expression '^Print$' for specifying the caption given there could be multiple dialogs with caption that includes the word Print. -->
    <step>
        <acquiredWindow>
            <window caption="Print">
                <windowList>
                    <window caption="General"/>
                    <window className="Button" caption="^Print$" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Print" action="disappear"/>
        </expectedWindow>
    </step>
    <step>
        <expectedWindow>
            <window caption="Save PDF File As"/>
        </expectedWindow>
    </step>
    <!-- Finally in this step, we acquire the dialog with caption "Save PDF File As" and in the Edit widget type the destination path for the output PDF file and click on the Save button. The expectation is that the dialog disappears-->
    <step>
        <acquiredWindow>
            <window caption="Save PDF File As">
                <windowList>
                    <window className="Edit" action="inputDestinationPath"/>
                </windowList>
                <windowList>
                    <window className="Button" caption="Save" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Save PDF File As" action="disappear"/>
        </expectedWindow>
    </step>

    <!-- We can always set a retry count or a maximum time for a step. In case we surpass these limitations, PDF Generator generates this abort message and terminates processing. -->
    <abortMessage msg="15078"/>
</application>
```
