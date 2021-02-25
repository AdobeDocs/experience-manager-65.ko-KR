---
title: 파일 포맷과 PDF 간 변환
seo-title: 파일 포맷과 PDF 간 변환
description: PDF 생성 서비스를 사용하여 기본 파일 형식을 PDF로 변환할 수 있습니다. 또한 PDF 생성 서비스는 PDF를 다른 파일 포맷으로 변환하고 PDF 문서의 크기를 최적화합니다.
seo-description: PDF 생성 서비스를 사용하여 기본 파일 형식을 PDF로 변환할 수 있습니다. 또한 PDF 생성 서비스는 PDF를 다른 파일 포맷으로 변환하고 PDF 문서의 크기를 최적화합니다.
uuid: f72ad603-c996-4d48-9bfc-bed7bf776af6
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 180cac3f-6378-42bc-9a47-60f9f08a7103
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '7912'
ht-degree: 0%

---


# 파일 형식과 PDF {#converting-between-file-formatsand-pdf} 간 변환

**이 문서의 샘플과 예는 JEE 환경의 AEM Forms에만 해당됩니다.**

**PDF 서비스 생성 정보**

PDF 생성 서비스는 기본 파일 형식을 PDF로 변환합니다. 또한 PDF를 다른 파일 포맷으로 변환하고 PDF 문서의 크기를 최적화합니다.

PDF 생성 서비스는 기본 애플리케이션을 사용하여 다음 파일 형식을 PDF로 변환합니다. 별도로 명시되어 있지 않는 한 이러한 애플리케이션의 독일어, 프랑스어, 영어 및 일본어 버전만 지원됩니다. *Windows* 는 Windows Server® 2003 및 Windows Server 2008에만 대한 지원을 나타냅니다.

* Microsoft Office 2003 및 2007을 사용하여 DOC, DOCX, RTF, TXT, XLS, XLSX, PPT, PPTX, VSD, MPP, MPPX, XPS 및 PUB(Windows 전용) 변환

>[!NOTE]
>
>Microsoft XPS 형식을 PDF로 변환하려면 Acrobat® 9.2 이상이 필요합니다.

* DWF, DWG 및 DXW를 변환할 수 있는 Autodesk AutoCAD 2005, 2006, 2007, 2008 및 2009(영어로만 제공)
* Corel WordPerfect 12 및 X4를 사용하여 WPD, QPW, SHW 변환(영어로만 제공)
* OpenOffice 2.0, 2.4, 3.0.1 및 3.1을 변환하여 ODT, ODP, ODG, ODF, SXW, SXW, SXC, SXD, DOC, DOCX, RTF, TXT, XLS, XLSX, PPT, PPT PPTX, VSD, MPP, MPPX 및 PUB

>[!NOTE]
>
>PDF 생성 서비스는 64비트 버전의 OpenOffice를 지원하지 않습니다.

* Adobe Photoshop® CS2를 사용하여 PSD 변환(Windows 전용)

>[!NOTE]
>
>Photoshop CS3 및 CS4는 Windows Server 2003 또는 Windows Server 2008을 지원하지 않으므로 지원되지 않습니다.

* FM 변환 Adobe FrameMaker® 7.2 및 8(Windows 전용)
* PMD, PM6, P65 및 PM을 변환하는 Adobe PageMaker® 7.0(Windows 전용)
* 제3자 응용 프로그램에서 지원되는 기본 형식(응용 프로그램별 설정 파일 개발 필요)(Windows만 해당)

PDF 생성 서비스는 다음과 같은 표준 기반 파일 형식을 PDF로 변환합니다.

* 비디오 형식:SWF, FLV(Windows 전용)
* 이미지 형식:JPEG, JPG, JP2, J2Ki, JPC, J2C, GIF, BMP, TIFF, TIF, PNG, JPF
* HTML(Windows, Sun™ Solaris™ 및 Linux®)

PDF 생성 서비스는 PDF를 다음 파일 형식으로 변환합니다(Windows만 해당).

* 캡슐화된 포스트스크립트(EPS)
* HTML3.2
* CSS 1.0이 있는 HTML 4.01
* DOC(Microsoft Word 형식)
* RTF
* 텍스트(액세스 가능 및 일반)
* XML
* DeviceRGB 색상 공간만 사용하는 PDF/A-1a
* DeviceRGB 색상 공간만 사용하는 PDF/A-1b

PDF 생성 서비스를 사용하려면 다음과 같은 관리 작업을 수행해야 합니다.

* AEM Forms을 호스팅하는 컴퓨터에 필요한 기본 응용 프로그램 설치
* AEM Forms을 호스팅하는 컴퓨터에 Adobe Acrobat Professional 또는 Acrobat Pro Extended 9.2 설치
* 설치 후 설정 작업 수행

이러한 작업은 JBoss 턴키를 사용하여 AEM 양식 설치 및 배포에 설명되어 있습니다.

PDF 생성 서비스를 사용하여 다음 작업을 수행할 수 있습니다.

* 기본 파일 포맷에서 PDF로 변환
* HTML 문서를 PDF 문서로 변환
* PDF 문서를 파일 포맷으로 변환

>[!NOTE]
>
>PDF 생성 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

## Word 문서를 PDF 문서 {#converting-word-documents-to-pdf-documents} 변환

이 섹션에서는 PDF 생성 API를 사용하여 프로그래밍 방식으로 Microsoft Word 문서를 PDF 문서로 변환하는 방법을 설명합니다.

>[!NOTE]
>
>추가 파일 형식에 대한 자세한 내용은 [추가 기본 파일 형식에 대한 지원 추가](converting-file-formats-pdf.md#adding-support-for-additional-native-file-formats)를 참조하십시오.

>[!NOTE]
>
>PDF 생성 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### {#summary-of-steps} 단계 요약

Microsoft Word 문서를 PDF 문서로 변환하려면 다음 작업을 수행합니다.

1. 프로젝트 파일 포함
1. PDF 생성 클라이언트 만들기
1. PDF 문서로 변환할 파일을 검색합니다.
1. 파일을 PDF 문서로 변환합니다.
1. 결과를 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**PDF 생성 클라이언트 만들기**

PDF 생성 작업을 프로그래밍 방식으로 수행하려면 먼저 PDF 생성 서비스 클라이언트를 만듭니다. Java API를 사용하는 경우 `GeneratePdfServiceClient` 개체를 만듭니다. 웹 서비스 API를 사용하는 경우 `GeneratePDFServiceService` 개체를 만듭니다.

**PDF 문서로 변환할 파일 검색**

Microsoft Word 문서를 검색하여 PDF 문서로 변환할 수 있습니다.

**파일을 PDF 문서로 변환**

PDF 생성 서비스 클라이언트를 만든 후 `createPDF2` 메서드를 호출할 수 있습니다. 이 메서드는 파일 확장자를 포함하여 변환할 문서에 대한 정보가 필요합니다.

**결과 검색**

파일을 PDF 문서로 변환한 후 결과를 가져올 수 있습니다. 예를 들어 Word 파일을 PDF 문서로 변환한 후 PDF 문서를 검색하고 저장할 수 있습니다.

**참고 항목**

[Java API를 사용하여 Word 문서를 PDF 문서로 변환](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-java-api)

[웹 서비스 API를 사용하여 Word 문서를 PDF 문서로 변환](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF 서비스 API 빠른 시작 생성](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Java API {#convert-word-documents-to-pdf-documents-using-the-java-api}를 사용하여 Word 문서를 PDF 문서로 변환

PDF 생성 API(Java)를 사용하여 Microsoft Word 문서를 PDF 문서로 변환:

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-generatepdf-client.jar 등의 클라이언트 JAR 파일을 포함합니다.

1. PDF 생성 클라이언트 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 `GeneratePdfServiceClient` 개체를 만들고 `ServiceClientFactory` 개체를 전달합니다.

1. PDF 문서로 변환할 파일을 검색합니다.

   * 생성자를 사용하여 변환할 Word 파일을 나타내는 `java.io.FileInputStream` 객체를 만듭니다. 파일 위치를 지정하는 문자열 값을 전달합니다.
   * 생성자를 사용하여 `com.adobe.idp.Document` 개체를 만들고 `java.io.FileInputStream` 개체를 전달합니다.

1. 파일을 PDF 문서로 변환합니다.

   `GeneratePdfServiceClient` 객체의 `createPDF2` 메서드를 호출하고 다음 값을 전달하여 파일을 PDF 문서로 변환합니다.

   * 변환할 파일을 나타내는 `com.adobe.idp.Document` 객체입니다.
   * 파일 확장명을 포함하는 `java.lang.String` 객체입니다.
   * 변환에 사용할 파일 형식 설정이 포함된 `java.lang.String` 개체 파일 유형 설정은 .doc 또는 .xls와 같은 다양한 파일 유형에 대한 변환 설정을 제공합니다.
   * 사용할 PDF 설정의 이름을 포함하는 `java.lang.String` 개체 예를 들어 `Standard`을(를) 지정할 수 있습니다.
   * 사용할 보안 설정의 이름을 포함하는 `java.lang.String` 개체
   * PDF 문서를 생성하는 동안 적용할 설정이 포함된 선택적 `com.adobe.idp.Document` 객체입니다.
   * PDF 문서에 적용할 메타데이터 정보를 포함하는 선택적 `com.adobe.idp.Document` 객체입니다.

   `createPDF2` 메서드는 새 PDF 문서와 로그 정보가 포함된 `CreatePDFResult` 개체를 반환합니다. 로그 파일에는 일반적으로 전환 요청으로 생성된 오류 또는 경고 메시지가 포함됩니다.

1. 결과를 검색합니다.

   PDF 문서를 얻으려면 다음 작업을 수행합니다.

   * `CreatePDFResult` 객체의 `getCreatedDocument` 메서드를 호출하여 `com.adobe.idp.Document` 객체를 반환합니다.
   * 이전 단계에서 만든 객체에서 PDF 문서를 추출하려면 `com.adobe.idp.Document` 객체의 `copyToFile` 메서드를 호출합니다.

   `createPDF2` 메서드를 사용하여 로그 문서를 얻은 경우(HTML 변환에는 해당되지 않음) 다음 작업을 수행합니다.

   * `CreatePDFResult` 객체의 `getLogDocument` 메서드를 호출합니다. `com.adobe.idp.Document` 객체를 반환합니다.
   * `com.adobe.idp.Document` 객체의 `copyToFile` 메서드를 호출하여 로그 문서를 추출합니다.


**참고 항목**

[단계 요약](converting-file-formats-pdf.md#summary-of-steps)

[빠른 시작(SOAP 모드):Java API를 사용하여 Microsoft Word 문서를 PDF 문서로 변환](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-a-microsoft-word-document-to-a-pdf-document-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API {#convert-word-documents-to-pdf-documents-using-the-web-service-api}를 사용하여 Word 문서를 PDF 문서로 변환

PDF 생성 API(웹 서비스)를 사용하여 Microsoft Word 문서를 PDF 문서로 변환:

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다.`http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꿉니다.

1. PDF 생성 클라이언트 만들기

   * 기본 생성자를 사용하여 `GeneratePDFServiceClient` 객체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `GeneratePDFServiceClient.Endpoint.Address` 객체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`). `lc_version` 특성을 사용할 필요가 없습니다. 그러나 `?blob=mtom`을 지정합니다.
   * `GeneratePDFServiceClient.Endpoint.Binding` 필드의 값을 가져와서 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`으로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`로 설정합니다. 이 값을 사용하면 MTOM이 사용됩니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * AEM 양식 사용자 이름을 `GeneratePDFServiceClient.ClientCredentials.UserName.UserName` 필드에 지정합니다.
      * 해당 암호 값을 `GeneratePDFServiceClient.ClientCredentials.UserName.Password` 필드에 지정합니다.
      * `BasicHttpBindingSecurity.Transport.ClientCredentialType` 필드에 상수 값 `HttpClientCredentialType.Basic`을 할당합니다.
      * `BasicHttpBindingSecurity.Security.Mode` 필드에 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을 할당합니다.

1. PDF 문서로 변환할 파일을 검색합니다.

   * 생성자를 사용하여 `BLOB` 객체를 만듭니다. `BLOB` 개체는 PDF 문서로 변환할 파일을 저장하는 데 사용됩니다.
   * 생성자를 호출하여 `System.IO.FileStream` 객체를 만듭니다. 변환할 파일의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * `System.IO.FileStream` 객체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 객체의 `Length` 속성을 가져와 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 객체의 `Read` 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * 바이트 배열의 내용을 `MTOM` 속성에 할당하여 `BLOB` 객체를 채웁니다.

1. 파일을 PDF 문서로 변환합니다.

   `GeneratePDFServiceService` 객체의 `CreatePDF2` 메서드를 호출하고 다음 값을 전달하여 파일을 PDF 문서로 변환합니다.

   * 변환할 파일을 나타내는 `BLOB` 객체입니다.
   * 파일 확장명을 포함하는 문자열입니다.
   * 변환에 사용할 파일 형식 설정이 포함된 `java.lang.String` 개체 파일 유형 설정은 .doc 또는 .xls와 같은 다양한 파일 유형에 대한 변환 설정을 제공합니다.
   * 사용할 PDF 설정이 포함된 문자열 객체입니다. `Standard`을(를) 지정할 수 있습니다.
   * 사용할 보안 설정이 포함된 문자열 객체입니다. `No Security`을(를) 지정할 수 있습니다.
   * PDF 문서를 생성하는 동안 적용할 설정이 포함된 선택적 `BLOB` 객체입니다.
   * PDF 문서에 적용할 메타데이터 정보를 포함하는 선택적 `BLOB` 객체입니다.
   * `CreatePDF2` 메서드로 채워지는 `BLOB` 유형의 출력 매개 변수입니다. `CreatePDF2` 메서드는 이 개체를 변환된 문서로 채웁니다. (이 매개 변수 값은 웹 서비스 호출에만 필요합니다.)
   * `CreatePDF2` 메서드로 채워지는 `BLOB` 유형의 출력 매개 변수입니다. `CreatePDF2` 메서드는 이 객체를 로그 문서로 채웁니다. (이 매개 변수 값은 웹 서비스 호출에만 필요합니다.)

1. 결과를 검색합니다.

   * 바이트 배열에 `BLOB` 개체의 `MTOM` 필드를 할당하여 변환된 PDF 문서를 검색합니다. 바이트 배열은 변환된 PDF 문서를 나타냅니다. `createPDF2` 메서드의 출력 매개 변수로 사용되는 `BLOB` 객체를 사용해야 합니다.
   * 생성자를 호출하고 변환된 PDF 문서의 파일 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 객체를 만듭니다.
   * 생성자를 호출하고 `System.IO.FileStream` 객체를 전달하여 `System.IO.BinaryWriter` 객체를 만듭니다.
   * `System.IO.BinaryWriter` 객체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 PDF 파일에 기록합니다.

**참고 항목**

[단계 요약](converting-file-formats-pdf.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## HTML 문서를 PDF 문서로 변환 {#converting-html-documents-to-pdf-documents}

이 섹션에서는 PDF 생성 API를 사용하여 HTML 문서를 프로그래밍 방식으로 PDF 문서로 변환하는 방법을 설명합니다.

>[!NOTE]
>
>PDF 생성 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### {#summary_of_steps-1} 단계 요약

HTML 문서를 PDF 문서로 변환하려면 다음 작업을 수행합니다.

1. 프로젝트 파일 포함
1. PDF 생성 클라이언트 만들기
1. HTML 내용을 검색하여 PDF 문서로 변환할 수 있습니다.
1. HTML 내용을 PDF 문서로 변환합니다.
1. 결과를 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**PDF 생성 클라이언트 만들기**

PDF 생성 작업을 프로그래밍 방식으로 수행하려면 먼저 PDF 생성 서비스 클라이언트를 만들어야 합니다. Java API를 사용하는 경우 `GeneratePdfServiceClient` 개체를 만듭니다. 웹 서비스 API를 사용하는 경우 `GeneratePDFServiceService`을(를) 만드십시오.

**PDF 문서로 변환할 HTML 내용 검색**

PDF 문서로 변환할 HTML 컨텐츠를 참조합니다. URL을 사용하여 액세스할 수 있는 HTML 파일 또는 HTML 컨텐츠와 같은 HTML 컨텐츠를 참조할 수 있습니다.

**HTML 컨텐츠를 PDF 문서로 변환**

서비스 클라이언트를 만든 후 적절한 PDF 작성 작업을 호출할 수 있습니다. 이 작업을 수행하려면 대상 문서의 경로를 포함하여 변환할 문서에 대한 정보가 필요합니다.

**결과 검색**

HTML 내용이 PDF 문서로 변환되면 결과를 검색하여 PDF 문서를 저장할 수 있습니다.

**참고 항목**

[Java API를 사용하여 HTML 컨텐츠를 PDF 문서로 변환](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-java-api)

[웹 서비스 API를 사용하여 HTML 컨텐츠를 PDF 문서로 변환](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF 서비스 API 빠른 시작 생성](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Java API {#convert-html-content-to-a-pdf-document-using-the-java-api}를 사용하여 HTML 컨텐츠를 PDF 문서로 변환

PDF 생성 API(Java)를 사용하여 HTML 문서를 PDF 문서로 변환:

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-generatepdf-client.jar 등의 클라이언트 JAR 파일을 포함합니다.

1. PDF 생성 클라이언트 만들기

   해당 생성자를 사용하고 연결 속성이 포함된 `ServiceClientFactory` 객체를 전달하여 `GeneratePdfServiceClient` 객체를 만듭니다.

1. HTML 내용을 검색하여 PDF 문서로 변환할 수 있습니다.

   문자열 변수를 만들고 HTML 컨텐츠를 가리키는 URL을 지정하여 HTML 컨텐츠를 검색합니다.

1. HTML 내용을 PDF 문서로 변환합니다.

   `GeneratePdfServiceClient` 객체의 `htmlToPDF2` 메서드를 호출하고 다음 값을 전달합니다.

   * 변환할 HTML 파일의 URL을 포함하는 `java.lang.String` 객체입니다.
   * 변환에 사용할 파일 형식 설정이 포함된 `java.lang.String` 개체 파일 유형 설정에는 할당 수준이 포함될 수 있습니다.
   * 사용할 보안 설정의 이름을 포함하는 `java.lang.String` 개체
   * PDF 문서를 생성하는 동안 적용할 설정이 포함된 선택적 `com.adobe.idp.Document` 객체입니다. 이 정보를 제공하지 않으면 이전 3개의 매개 변수를 기반으로 설정이 자동으로 선택됩니다.
   * PDF 문서에 적용할 메타데이터 정보를 포함하는 선택적 `com.adobe.idp.Document` 객체입니다.

1. 결과를 검색합니다.

   `htmlToPDF2` 메서드는 생성된 새 PDF 문서를 포함하는 `HtmlToPdfResult` 개체를 반환합니다. 새로 만든 PDF 문서를 얻으려면 다음 작업을 수행합니다.

   * `HtmlToPdfResult` 객체의 `getCreatedDocument` 메서드를 호출합니다. `com.adobe.idp.Document` 객체를 반환합니다.
   * 이전 단계에서 만든 객체에서 PDF 문서를 추출하려면 `com.adobe.idp.Document` 객체의 `copyToFile` 메서드를 호출합니다.

**참고 항목**

[HTML 문서를 PDF 문서로 변환](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[빠른 시작(SOAP 모드):Java API를 사용하여 HTML 내용을 PDF 문서로 변환](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 HTML 내용을 PDF 문서로 변환](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API {#convert-html-content-to-a-pdf-document-using-the-web-service-api}를 사용하여 HTML 내용을 PDF 문서로 변환

PDF 생성 API(웹 서비스)를 사용하여 HTML 컨텐츠를 PDF 문서로 변환:

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다.`http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꿉니다.

1. PDF 생성 클라이언트 만들기

   * 기본 생성자를 사용하여 `GeneratePDFServiceClient` 객체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `GeneratePDFServiceClient.Endpoint.Address` 객체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`). `lc_version` 특성을 사용할 필요가 없습니다. 그러나 `?blob=mtom`을 지정합니다.
   * `GeneratePDFServiceClient.Endpoint.Binding` 필드의 값을 가져와서 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`으로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`로 설정합니다. 이 값을 사용하면 MTOM이 사용됩니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * AEM 양식 사용자 이름을 `GeneratePDFServiceClient.ClientCredentials.UserName.UserName` 필드에 지정합니다.
      * 해당 암호 값을 `GeneratePDFServiceClient.ClientCredentials.UserName.Password` 필드에 지정합니다.
      * `BasicHttpBindingSecurity.Transport.ClientCredentialType` 필드에 상수 값 `HttpClientCredentialType.Basic`을 할당합니다.
      * `BasicHttpBindingSecurity.Security.Mode` 필드에 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을 할당합니다.

1. HTML 내용을 검색하여 PDF 문서로 변환할 수 있습니다.

   문자열 변수를 만들고 HTML 컨텐츠를 가리키는 URL을 지정하여 HTML 컨텐츠를 검색합니다.

1. HTML 내용을 PDF 문서로 변환합니다.

   `GeneratePDFServiceService` 개체의 `HtmlToPDF2` 메서드를 호출하여 HTML 내용을 PDF 문서로 변환하고 다음 값을 전달합니다.

   * 변환할 HTML 내용이 포함된 문자열입니다.
   * 변환에 사용할 파일 형식 설정이 포함된 `java.lang.String` 개체
   * 사용할 보안 설정이 포함된 문자열 객체입니다.
   * PDF 문서를 생성하는 동안 적용할 설정이 포함된 선택적 `BLOB` 객체입니다.
   * PDF 문서에 적용할 메타데이터 정보를 포함하는 선택적 `BLOB` 객체입니다.
   * `CreatePDF2` 메서드로 채워지는 `BLOB` 유형의 출력 매개 변수입니다. `CreatePDF2` 메서드는 이 개체를 변환된 문서로 채웁니다. (이 매개 변수 값은 웹 서비스 호출에만 필요합니다.)

1. 결과를 검색합니다.

   * 바이트 배열에 `BLOB` 개체의 `MTOM` 필드를 할당하여 변환된 PDF 문서를 검색합니다. 바이트 배열은 변환된 PDF 문서를 나타냅니다. `HtmlToPDF2` 메서드의 출력 매개 변수로 사용되는 `BLOB` 객체를 사용해야 합니다.
   * 생성자를 호출하고 변환된 PDF 문서의 파일 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 객체를 만듭니다.
   * 생성자를 호출하고 `System.IO.FileStream` 객체를 전달하여 `System.IO.BinaryWriter` 객체를 만듭니다.
   * `System.IO.BinaryWriter` 객체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 PDF 파일에 기록합니다.

**참고 항목**

[HTML 문서를 PDF 문서로 변환](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## PDF 문서를 이미지가 아닌 형식 {#converting-pdf-documents-to-non-image-formats}으로 변환

이 섹션에서는 [PDF Java API 생성] 및 웹 서비스 API를 사용하여 프로그래밍 방식으로 PDF 문서를 이미지가 아닌 형식의 예인 RTF 파일로 변환하는 방법을 설명합니다. 이미지 형식이 아닌 다른 형식으로는 HTML, 텍스트, DOC 및 EPS가 있습니다. PDF 문서를 RTF로 변환할 때 PDF 문서에 전송 단추와 같은 양식 요소가 포함되어 있지 않은지 확인합니다. 양식 요소는 변환되지 않습니다.

>[!NOTE]
>
>PDF 생성 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### {#summary_of_steps-2} 단계 요약

PDF 문서를 지원되는 유형으로 변환하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. PDF 생성 클라이언트 만들기
1. 변환할 PDF 문서를 검색합니다.
1. PDF 문서를 변환합니다.
1. 변환된 파일을 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**PDF 생성 클라이언트 만들기**

PDF 생성 작업을 프로그래밍 방식으로 수행하려면 먼저 PDF 생성 서비스 클라이언트를 만들어야 합니다. Java API를 사용하는 경우 `GeneratePdfServiceClient` 개체를 만듭니다. 웹 서비스 API를 사용하는 경우 `GeneratePDFServiceService` 개체를 만듭니다.

**변환할 PDF 문서 검색**

PDF 문서를 검색하여 이미지가 아닌 형식으로 변환합니다.

**PDF 문서 변환**

서비스 클라이언트를 만든 후 PDF 내보내기 작업을 호출할 수 있습니다. 이 작업을 수행하려면 대상 문서의 경로를 포함하여 변환할 문서에 대한 정보가 필요합니다.

**변환된 파일 저장**

변환된 파일을 저장합니다. 예를 들어 PDF 문서를 RTF 파일로 변환하는 경우 변환된 문서를 RTF 파일로 저장합니다.

**참고 항목**

[Java API를 사용하여 PDF 문서를 RTF 파일로 변환](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-java-api)

[웹 서비스 API를 사용하여 PDF 문서를 RTF 파일로 변환](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF 서비스 API 빠른 시작 생성](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Java API {#convert-a-pdf-document-to-a-rtf-file-using-the-java-api}를 사용하여 PDF 문서를 RTF 파일로 변환

PDF 생성 API(Java)를 사용하여 PDF 문서를 RTF 파일로 변환:

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-generatepdf-client.jar 등의 클라이언트 JAR 파일을 포함합니다.

1. PDF 생성 클라이언트 만들기

   해당 생성자를 사용하고 연결 속성이 포함된 `ServiceClientFactory` 객체를 전달하여 `GeneratePdfServiceClient` 객체를 만듭니다.

1. 변환할 PDF 문서를 검색합니다.

   * 생성자를 사용하여 변환할 PDF 문서를 나타내는 `java.io.FileInputStream` 객체를 만듭니다. PDF 문서의 위치를 지정하는 문자열 값을 전달합니다.
   * 생성자를 사용하여 `com.adobe.idp.Document` 개체를 만들고 `java.io.FileInputStream` 개체를 전달합니다.

1. PDF 문서를 변환합니다.

   `GeneratePdfServiceClient` 객체의 `exportPDF2` 메서드를 호출하고 다음 값을 전달합니다.

   * 변환할 PDF 파일을 나타내는 `com.adobe.idp.Document` 개체
   * 변환할 파일의 이름을 포함하는 `java.lang.String` 객체입니다.
   * Adobe PDF 설정의 이름을 포함하는 `java.lang.String` 객체입니다.
   * 변환의 대상 파일 유형을 지정하는 `ConvertPDFFormatType` 개체
   * PDF 문서를 생성하는 동안 적용할 설정이 포함된 선택적 `com.adobe.idp.Document` 객체입니다.

   `exportPDF2` 메서드는 변환된 파일을 포함하는 `ExportPDFResult` 객체를 반환합니다.

1. PDF 문서를 변환합니다.

   새로 만든 파일을 가져오려면 다음 작업을 수행합니다.

   * `ExportPDFResult` 객체의 `getConvertedDocument` 메서드를 호출합니다. `com.adobe.idp.Document` 객체를 반환합니다.
   * `com.adobe.idp.Document` 객체의 `copyToFile` 메서드를 호출하여 새 문서를 추출합니다.

**참고 항목**

[단계 요약](converting-file-formats-pdf.md#summary-of-steps)

[빠른 시작(SOAP 모드):Java API를 사용하여 HTML 내용을 PDF 문서로 변환](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API {#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api}를 사용하여 PDF 문서를 RTF 파일로 변환

PDF 생성 API(웹 서비스)를 사용하여 PDF 문서를 RTF 파일로 변환:

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다.`http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꿉니다.

1. PDF 생성 클라이언트 만들기

   * 기본 생성자를 사용하여 `GeneratePDFServiceClient` 객체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `GeneratePDFServiceClient.Endpoint.Address` 객체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`). `lc_version` 특성을 사용할 필요가 없습니다. 그러나 `?blob=mtom`을 지정합니다.
   * `GeneratePDFServiceClient.Endpoint.Binding` 필드의 값을 가져와서 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`으로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`로 설정합니다. 이 값을 사용하면 MTOM이 사용됩니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * AEM 양식 사용자 이름을 `GeneratePDFServiceClient.ClientCredentials.UserName.UserName` 필드에 지정합니다.
      * 해당 암호 값을 `GeneratePDFServiceClient.ClientCredentials.UserName.Password` 필드에 지정합니다.
      * `BasicHttpBindingSecurity.Transport.ClientCredentialType` 필드에 상수 값 `HttpClientCredentialType.Basic`을 할당합니다.
      * `BasicHttpBindingSecurity.Security.Mode` 필드에 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을 할당합니다.

1. 변환할 PDF 문서를 검색합니다.

   * 생성자를 사용하여 `BLOB` 객체를 만듭니다. `BLOB` 개체는 변환된 PDF 문서를 저장하는 데 사용됩니다.
   * 생성자를 호출하고 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 객체를 만듭니다.
   * `System.IO.FileStream` 객체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 객체의 `Length` 속성을 가져와 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 객체의 `Read` 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * 바이트 배열의 내용을 `MTOM` 속성에 할당하여 `BLOB` 객체를 채웁니다.

1. PDF 문서를 변환합니다.

   `GeneratePDFServiceServiceWse` 객체의 `ExportPDF2` 메서드를 호출하고 다음 값을 전달합니다.

   * 변환할 PDF 파일을 나타내는 `BLOB` 개체
   * 변환할 파일의 경로 이름을 포함하는 문자열입니다.
   * 파일 위치를 지정하는 `java.lang.String` 객체입니다.
   * 변환의 대상 파일 유형을 지정하는 문자열 객체입니다. 지정 `RTF`.
   * PDF 문서를 생성하는 동안 적용할 설정이 포함된 선택적 `BLOB` 객체입니다.
   * `ExportPDF2` 메서드로 채워지는 `BLOB` 유형의 출력 매개 변수입니다. `ExportPDF2` 메서드는 이 개체를 변환된 문서로 채웁니다. (이 매개 변수 값은 웹 서비스 호출에만 필요합니다.)

1. 변환된 파일을 저장합니다.

   * 변환된 RTF 문서를 검색하여 `BLOB` 개체의 `MTOM` 필드를 바이트 배열에 할당합니다. 바이트 배열은 변환된 RTF 문서를 나타냅니다. `ExportPDF2` 메서드의 출력 매개 변수로 사용되는 `BLOB` 객체를 사용해야 합니다.
   * 생성자를 호출하여 `System.IO.FileStream` 객체를 만듭니다. RTF 파일의 위치를 나타내는 문자열 값을 전달합니다.
   * 생성자를 호출하고 `System.IO.FileStream` 객체를 전달하여 `System.IO.BinaryWriter` 객체를 만듭니다.
   * `System.IO.BinaryWriter` 객체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 RTF 파일에 씁니다.

**참고 항목**

[단계 요약](converting-file-formats-pdf.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 추가 기본 파일 형식 지원 추가 {#adding-support-for-additional-native-file-formats}

이 섹션에서는 추가 기본 파일 형식에 대한 지원을 추가하는 방법을 설명합니다. PDF 생성 서비스와 이 서비스가 기본 파일 형식을 PDF로 변환하는 데 사용하는 기본 애플리케이션 간의 상호 작용에 대한 개요를 제공합니다.

이 섹션에서는 다음 사항도 설명합니다.

* PDF 생성 서비스가 이 제품이 기본 파일 형식을 PDF로 변환하는 데 이미 사용하는 기본 애플리케이션에 제공하는 응답을 수정하는 방법
* PDF 생성 서비스, AppMon(PDF 서비스 애플리케이션 모니터) 구성 요소 및 Microsoft Word와 같은 기본 애플리케이션 간의 상호 작용
* 이러한 상호 작용에서 XML 그램이 수행하는 역할

### 구성 요소 상호 작용 {#component-interactions}

PDF 생성 서비스는 파일 형식과 관련된 응용 프로그램을 호출한 다음 기본 프린터를 사용하여 문서를 인쇄하기 위해 응용 프로그램과 상호 작용하여 기본 파일 형식을 변환합니다. 기본 프린터는 Adobe PDF 프린터로 설정해야 합니다.

이 그림은 기본 애플리케이션 지원과 관련된 구성 요소 및 드라이버를 보여줍니다. 또한 상호 작용에 영향을 주는 XML 문법에 대해서도 언급합니다.

기본 파일 변환을 위한 구성 요소 상호 작용

이 문서에서는 *기본 응용 프로그램*&#x200B;이라는 용어를 사용하여 Microsoft Word와 같은 기본 파일 형식을 만드는 데 사용되는 응용 프로그램을 나타냅니다.

*AppMonis* 는 사용자가 해당 애플리케이션에서 제공하는 대화 상자를 탐색하는 것과 동일한 방식으로 기본 애플리케이션과 상호 작용하는 기업 구성 요소입니다. AppMon이 Microsoft Word와 같은 응용 프로그램을 열어 인쇄하는 데 사용하는 XML 그램은 다음과 같은 순차적 작업을 포함합니다.

1. 파일 > 열기를 선택하여 파일 열기
1. [열기] 대화 상자가 나타나는지 확인합니다.그렇지 않은 경우 오류 처리
1. 파일 이름 필드에 파일 이름을 입력한 다음 열기 단추를 클릭합니다.
1. 파일이 실제로 열리는지 확인
1. 파일 > 인쇄를 선택하여 인쇄 대화 상자 열기
1. 인쇄 대화 상자가 나타나는지 확인

AppMon은 표준 Win32 API를 사용하여 타사 애플리케이션과 상호 작용하여 키 획 및 마우스 클릭과 같은 UI 이벤트를 전송하며, 이러한 애플리케이션을 제어하여 PDF 파일을 해당 애플리케이션에서 생성하는 데 유용합니다.

이러한 Win32 API의 제한 사항으로 인해 AppMon은 이러한 UI 이벤트를 부동 메뉴 막대(텍스트 패드와 같은 일부 응용 프로그램에서 찾음)와 Win32 API를 사용하여 내용을 검색할 수 없는 특정 유형의 대화 상자와 같은 특정 유형의 윈도우에 전달할 수 없습니다.

부동 메뉴 막대를 시각적으로 손쉽게 식별할 수 있습니다.하지만 시각적인 검사만으로 특별한 유형의 대화 상자를 식별할 수는 없을 수도 있습니다. 대화 상자를 검사하여 AppMon이 표준 Win32 API를 사용하여 상호 작용할 수 있는지 확인하기 위해 Microsoft Spy++(Microsoft Visual C++ 개발 환경의 일부) 또는 이에 상응하는 WinID([https://www.dennisbabkin.com/php/download.php?what=WinID](https://www.dennisbabkin.com/php/download.php?what=WinID)에서 무료로 다운로드할 수 있음)와 같은 타사 응용 프로그램이 필요합니다.

WinID가 텍스트, 하위 창, 윈도우 클래스 ID 등과 같은 대화 상자 내용을 추출할 수 있는 경우 AppMon도 동일한 작업을 수행할 수 있습니다.

이 표에는 기본 파일 형식을 인쇄하는 데 사용되는 정보 유형이 나열됩니다.

<table>
 <thead>
  <tr>
   <th><p>정보 유형</p></th>
   <th><p>설명</p></th>
   <th><p>기본 파일과 관련된 항목 수정/만들기 </p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>관리 설정 </p></td>
   <td><p>PDF 설정, 보안 설정 및 파일 유형 설정이 포함되어 있습니다. </p><p>파일 유형 설정은 파일 이름 확장자를 해당 기본 응용 프로그램과 연결합니다. 파일 유형 설정은 기본 파일을 인쇄하는 데 사용되는 기본 응용 프로그램 설정도 지정합니다. </p></td>
   <td><p>이미 지원되는 기본 응용 프로그램에 대한 설정을 변경하려면 시스템 관리자가 관리 콘솔에서 파일 유형 설정을 설정합니다. </p><p>새 기본 파일 형식에 대한 지원을 추가하려면 파일을 수동으로 편집해야 합니다. (기본 파일 형식</a>에 대한 지원 추가 또는 수정을 참조하십시오.)<a href="converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format"> </a></p></td>
  </tr>
  <tr>
   <td><p>스크립트 </p></td>
   <td><p>PDF 생성 서비스와 기본 애플리케이션 간의 상호 작용을 지정합니다. 이러한 상호 작용은 일반적으로 응용 프로그램이 파일을 Adobe PDF 드라이버으로 인쇄하도록 합니다. </p><p>이 스크립트에는 기본 응용 프로그램이 특정 대화 상자를 열도록 지시하고 해당 대화 상자의 필드 및 단추에 대한 특정 응답을 제공하는 지침이 들어 있습니다. </p></td>
   <td><p>PDF 생성 서비스에는 지원되는 모든 기본 애플리케이션에 대한 스크립트 파일이 포함됩니다. XML 편집 응용 프로그램을 사용하여 이러한 파일을 수정할 수 있습니다.</p><p>새 기본 응용 프로그램에 대한 지원을 추가하려면 새 스크립트 파일을 만들어야 합니다. (기본 응용 프로그램</a>에 대한 추가 대화 상자 XML 파일 만들기 또는 수정을 참조하십시오.)<a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application"> </a></p></td>
  </tr>
  <tr>
   <td><p>일반 대화 상자 지침 </p></td>
   <td><p>여러 응용 프로그램에 공통으로 사용되는 대화 상자에 응답하는 방법을 지정합니다. 이러한 대화 상자는 운영 체제, 보조 애플리케이션(예: PDFMaker) 및 드라이버에 의해 생성됩니다. </p><p>이 정보가 포함된 파일은 appmon.global.en_US.xml입니다.</p></td>
   <td><p>이 파일을 수정하지 마십시오. </p></td>
  </tr>
  <tr>
   <td><p>애플리케이션별 대화 상자 지침</p></td>
   <td><p>응용 프로그램별 대화 상자에 응답하는 방법을 지정합니다. </p><p>이 정보가 포함된 파일이 적용됩니다.<i>'[appname]'</i>.dialog.<i>'[locale]'</i>.xml(예: appmon.word.en_US.xml).</p></td>
   <td><p>이 파일을 수정하지 마십시오. </p><p>새 기본 응용 프로그램에 대한 대화 상자 지침을 추가하려면 기본 응용 프로그램</a>에 대한 추가 대화 상자 XML 파일 만들기 또는 수정을 참조하십시오.<a href="converting-file-formats-pdf.md#creating_or_modifying_an_additional_dialog_xml_file_for_a_native_application"></a></p></td>
  </tr>
  <tr>
   <td><p>추가 애플리케이션별 대화 상자 지침 </p></td>
   <td><p>응용 프로그램별 대화 상자 지침에 대한 무시 및 추가 항목을 지정합니다. 이 섹션에는 이러한 정보의 예가 나와 있습니다. </p><p>이 정보가 포함된 파일이 적용됩니다.<i>'[appname]'</i>.addition.<i>'[locale]'</i>.xml. 예를 들면 appmon.addition.en_US.xml이 있습니다.</p></td>
   <td><p>이 유형의 파일은 XML 편집 응용 프로그램을 사용하여 만들고 수정할 수 있습니다. (기본 응용 프로그램</a>에 대한 추가 대화 상자 XML 파일 만들기 또는 수정을 참조하십시오.)<a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application"> </a></p><p><strong>중요</strong>:서버에서 지원할 각 기본 응용 프로그램에 대해 응용 프로그램별 대화 상자 지침을 추가로 만들어야 합니다. </p></td>
  </tr>
 </tbody>
</table>

### 스크립트 및 대화 상자 XML 파일 {#about-the-script-and-dialog-xml-files} 정보

스크립트 XML 파일은 사용자가 응용 프로그램 대화 상자를 탐색하는 것과 동일한 방식으로 PDF 생성 서비스에서 응용 프로그램 대화 상자를 탐색하도록 지시합니다. 또한 스크립트 XML 파일은 PDF 생성 서비스가 버튼 누르기, 확인란 선택 또는 선택 취소, 메뉴 항목 선택 등의 작업을 수행하여 대화 상자에 응답하도록 합니다.

반대로 대화 상자 XML 파일은 스크립트 XML 파일에 사용되는 것과 동일한 유형의 액션을 사용하여 대화 상자에 응답합니다.

#### 대화 상자 및 윈도우 요소 용어 {#dialog-box-and-window-element-terminology}

이 섹션 및 다음 섹션에서는 설명하는 원근에 따라 대화 상자와 대화 상자에 포함된 구성 요소에 대해 서로 다른 용어를 사용합니다. 대화 상자 구성 요소는 단추, 필드 및 콤보 상자와 같은 항목입니다.

이 섹션 및 다음 섹션에서 사용자의 관점에서 대화 상자와 해당 구성 요소를 설명하는 경우 *대화 상자*, *버튼*, *필드* 및 *콤보 상자*&#x200B;와 같은 용어가 사용됩니다.

이 섹션 및 다음 섹션에서 내부 표현의 관점에서 대화 상자와 해당 구성 요소를 설명하는 경우 *window 요소*&#x200B;라는 용어가 사용됩니다. 윈도우 요소의 내부 표시는 각 윈도우 요소 인스턴스가 레이블로 식별되는 계층입니다. window 요소 인스턴스는 또한 물리적인 특성 및 비헤이비어를 설명합니다.

대화 상자와 해당 구성 요소는 활성화될 때까지 일부 대화 상자 요소가 숨겨지는 서로 다른 동작을 보여 줍니다. 내부 표현 관점에서 이러한 행동 문제는 존재하지 않습니다. 예를 들어 대화 상자의 내부 표현은 구성 요소가 대화 상자에 중첩되어 있다는 점을 제외하고 대화 상자에 포함된 구성 요소의 내부 표현과 비슷합니다.

이 섹션에서는 AppMon에 지침을 제공하는 XML 요소에 대해 설명합니다. 이러한 요소에는 `dialog` 요소 및 `window` 요소와 같은 이름이 있습니다. 이 문서에서는 고정 폭 글꼴을 사용하여 XML 요소를 구별합니다. `dialog` 요소는 XML 스크립트 파일이 의도적이거나 의도치 않게 표시될 수 있는 대화 상자를 식별합니다. `window` 요소는 윈도우 요소(대화 상자 또는 대화 상자의 구성 요소)를 식별합니다.

#### 계층 구조 {#hierarchy}

이 다이어그램은 스크립트와 대화 상자 XML의 계층 구조를 보여 줍니다. 스크립트 XML 파일은 window.xsd 스키마를 포함하는 script.xsd 스키마를 따릅니다. XML의 경우) 마찬가지로 대화 상자 XML 파일은 window.xsd 스키마를 포함하는 dialogs.xsd 스키마를 따릅니다.

![as_as_xml_hierarchy](assets/as_as_xml_hierarchy.png)

스크립트 및 대화 상자 XML 계층 구조

#### 스크립트 XML 파일 {#script-xml-files}

*스크립트 XML 파일*&#x200B;은 기본 응용 프로그램이 특정 윈도우 요소로 이동한 다음 해당 요소에 대한 응답을 제공하도록 하는 일련의 단계를 지정합니다. 대부분의 응답은 사용자가 해당 대화 상자의 필드, 콤보 상자 또는 단추에 제공하는 입력에 해당하는 텍스트 또는 키 입력입니다.

PDF 생성 서비스에서 스크립트 XML 파일을 지원한다는 목적은 기본 응용 프로그램이 기본 파일을 인쇄하도록 지시하는 것입니다. 그러나 스크립트 XML 파일을 사용하여 기본 응용 프로그램의 대화 상자를 상호 작용할 때 사용자가 수행할 수 있는 모든 작업을 수행할 수 있습니다.

스크립트 XML 파일의 단계는 분기 기회 없이 순서대로 실행됩니다. 지원되는 유일한 조건부 테스트는 시간 초과/재시도뿐입니다. 이 경우 특정 시간 내에 단계가 성공적으로 완료되지 않고 특정 재시도 횟수 후에 스크립트가 종료됩니다.

순차적 단계를 수행하는 것 외에도 단계 내의 명령도 순서대로 실행됩니다. 단계 및 지침이 사용자가 동일한 단계를 수행하는 순서를 반영하도록 해야 합니다.

스크립트 XML 파일의 각 단계는 단계 명령이 성공적으로 수행되는 경우 표시될 윈도우 요소를 식별합니다. 스크립트 단계를 실행하는 동안 예기치 않은 대화 상자가 나타나면 PDF 생성 서비스는 다음 섹션에 설명된 대로 대화 상자 XML 파일을 검색합니다.

#### 대화 상자 XML 파일 {#dialog-xml-files}

기본 응용 프로그램을 실행하면 기본 응용 프로그램이 표시 또는 보이지 않는 모드에 있는지 여부에 관계없이 나타나는 서로 다른 대화 상자가 표시됩니다. 대화 상자는 운영 체제나 응용 프로그램 자체에 의해 생성할 수 있습니다. 기본 응용 프로그램이 [PDF 생성] 서비스의 제어하에 실행되고 있으면 시스템 및 기본 응용 프로그램 대화 상자가 보이지 않는 창에 표시됩니다.

*대화 상자 XML 파일*&#x200B;은 PDF 생성 서비스가 시스템 또는 기본 응용 프로그램 대화 상자에 응답하는 방식을 지정합니다. 대화 상자 XML 파일을 사용하면 변환 프로세스를 용이하게 하는 방식으로 PDF 생성 서비스가 메시지가 표시되지 않는 대화 상자에 응답할 수 있습니다.

시스템 또는 기본 응용 프로그램에서 현재 실행 중인 스크립트 XML 파일에서 처리되지 않는 대화 상자를 표시하는 경우 [PDF 생성] 서비스는 일치 항목을 찾을 때 정지하여 이 순서대로 대화 상자 XML 파일을 검색합니다.

* appmon을 참조하십시오.`[appname]`추가.`[locale]`.xml
* appmon을 참조하십시오.`[appname]`.`[locale]`.xml(이 파일을 수정하지 마십시오.)
* appmon.global.`[locale]`.xml(이 파일을 수정하지 마십시오.)

[PDF 생성] 서비스에서 대화 상자에 대한 일치 항목을 찾으면 대화 상자에 지정된 키 또는 기타 작업을 전송하여 대화 상자를 닫습니다. 대화 상자에 대한 지시에서 중단 메시지를 지정하면 PDF 생성 서비스는 현재 실행 중인 작업을 종료하고 오류 메시지를 생성합니다. 이러한 중단 메시지는 스크립트 XML 문법의 `abortMessage` 요소에 지정됩니다.

[PDF 생성] 서비스에 이전에 나열된 파일에 설명되어 있지 않은 대화 상자가 나타나면 [PDF 생성] 서비스는 대화 상자의 캡션을 로그 파일 항목에 통합합니다. 현재 실행 중인 작업은 시간이 초과됩니다. 그런 다음 로그 파일의 정보를 사용하여 기본 응용 프로그램의 추가 대화 상자 XML 파일에 새 지침을 작성할 수 있습니다.

### 기본 파일 형식 {#adding-or-modifying-support-for-a-native-file-format}에 대한 지원 추가 또는 수정

이 섹션에서는 다른 기본 파일 형식을 지원하거나 이미 지원되는 기본 파일 형식에 대한 지원을 수정하기 위해 수행해야 하는 작업에 대해 설명합니다.

지원을 추가하거나 수정하려면 먼저 다음 작업을 완료해야 합니다.

#### 윈도우 요소 {#choosing-a-tool-for-identifying-window-elements} 식별을 위한 도구 선택

대화 상자 및 스크립트 XML 파일을 사용하려면 대화 상자 또는 스크립트 요소가 응답하는 윈도우 요소(대화 상자, 필드 또는 기타 대화 상자 구성 요소)를 식별해야 합니다. 예를 들어, 스크립트에서 기본 애플리케이션에 대한 메뉴를 호출한 후 스크립트는 키 입력이나 동작을 적용할 해당 메뉴의 윈도우 요소를 식별해야 합니다.

대화 상자가 제목 표시줄에 표시되는 캡션으로 대화 상자를 손쉽게 식별할 수 있습니다. 그러나 Microsoft Spy++와 같은 도구를 사용하여 더 낮은 수준의 창 요소를 식별해야 합니다. 하위의 창 요소는 다양한 특성을 통해 식별할 수 있으며, 이것은 분명하지 않습니다. 또한 각 기본 응용 프로그램은 윈도우 요소를 다르게 식별할 수 있습니다. 따라서 윈도우 요소를 식별하는 여러 가지 방법이 있습니다. 윈도우 요소 식별을 고려하기 위해 제안된 주문은 다음과 같습니다.

1. 고유한 경우 캡션 자체
1. 지정된 대화 상자에 대해 고유하거나 고유하지 않을 수 있는 컨트롤 ID
1. 고유한 클래스 이름

이러한 세 가지 속성의 하나 또는 조합을 사용하여 창을 식별할 수 있습니다.

특성이 캡션을 식별하지 못하는 경우 대신 상위에 대한 인덱스를 사용하여 윈도우 요소를 식별할 수 있습니다. *index*&#x200B;는 동위 창 요소를 기준으로 윈도우 요소의 위치를 지정합니다. 콤보 상자를 식별할 수 있는 유일한 방법은 인덱스입니다.

다음 문제에 주의하십시오.

* Microsoft Spy++는 앰퍼샌드(&amp;)를 사용하여 캡션의 핫키를 식별하여 캡션을 표시합니다. 예를 들어 Spy++는 하나의 [인쇄] 대화 상자에 대한 캡션을 `Pri&nt`(핫키가 *n*&#x200B;임을 나타냅니다. 스크립트 및 대화 상자 XML 파일의 캡션 제목에는 앰퍼샌드를 생략해야 합니다.
* 일부 캡션에는 행 분리가 포함됩니다. PDF 생성 서비스는 줄바꿈을 식별할 수 없습니다. 캡션에 줄 바꿈이 포함되어 있는 경우 캡션을 충분히 포함시켜 다른 메뉴 항목과 구분한 다음 누락된 부분에 정규 표현식을 사용합니다. 예로는 ( `^Long caption title$`)이 있습니다. ([캡션 특성에서 일반 표현식 사용](converting-file-formats-pdf.md#using-regular-expressions-in-caption-attributes)을 참조하십시오.)
* 예약된 XML 문자에 문자 엔티티(이스케이프 시퀀라고도 함)를 사용합니다. 예를 들어 앰퍼샌드(`&`)는 `<`, `>` 는 기호에, &lt; a3/> 는 아포스트로피를, `&quot;`는 따옴표를 사용합니다.`&apos;`

대화 상자에서 작업하거나 XML 파일을 스크립팅하려면 Microsoft Spy++ 응용 프로그램을 설치해야 합니다.

#### 대화 상자 및 스크립트 파일 {#unpackaging-the-dialog-and-script-files} 패키징 취소

대화 상자와 스크립트 파일은 appmondata.jar 파일에 있습니다. 이러한 파일을 수정하거나 새 스크립트 또는 대화 상자 파일을 추가하려면 먼저 이 JAR 파일의 패키지를 해제해야 합니다. 예를 들어 EditPlus 응용 프로그램에 대한 지원을 추가한다고 가정합니다. appmon.editplus.script.en_US.xml 및 appmon.editplus.script.addition.en_US.xml이라는 두 개의 XML 파일을 만듭니다. 아래 지정된 대로 두 위치의 adobe-appmondata.jar 파일에 이러한 XML 스크립트를 추가해야 합니다.

* adobe-livecycle-native-jboss-x86_win32.ear > adobe-Native2PDFSvc.war\WEB-INF\lib > adobe-native.jar > Native2PDFSvc-native.jar\bin > adobe-appmondata.jar\com\adobe\appmon adobe-livecycle-native-jboss-x86_win32.ear 파일은 `[AEM forms install directory]\configurationManager`의 내보내기 폴더에 있습니다. AEM Forms이 다른 J2EE 응용 프로그램 서버에 배포되는 경우 adobe-livecycle-native-jboss-x86_win32.ear 파일을 J2EE 응용 프로그램 서버에 해당하는 EAR 파일로 바꿉니다.
* adobe-generatepdf-dsc.jar > adobe-appmondata.jar\com\adobe\appmon (adobe-appmondata.jar 파일은 adobe-generatepdf-dsc.jar 파일에 있습니다.) adobe-generatepdf-dsc.jar 파일은 `[AEM forms install directory]\deploy` 폴더에 있습니다.

이러한 XML 파일을 adobe-appmondata.jar 파일에 추가한 후 GeneratePDF 구성 요소를 다시 배포해야 합니다. 대화 상자 및 스크립트 XML 파일을 adobe-appmondata.jar 파일에 추가하려면 다음 작업을 수행합니다.

1. WinZip 또는 WinRAR와 같은 도구를 사용하여 adobe-livecycle-native-jboss-x86_win32.earfile > adobe-Native2PDFSvc.war\WEB-INF\lib > adobe-native.jar > Native2PDFSvcvc_native.jar\bin > adobe-appmondata.jar 파일을 엽니다.
1. 대화 상자 및 스크립트 XML 파일을 appmondata.jar 파일에 추가하거나 이 파일에서 기존 XML 파일을 수정합니다. (기본 응용 프로그램](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)및 [기본 응용 프로그램에 대한 추가 대화 상자 XML 파일 만들기 또는 수정을 참조하십시오](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application).)[
1. WinZip 또는 WinRAR와 같은 도구를 사용하여 adobe-generatepdf-dsc.jar > adobe-appmondata.jar를 엽니다.
1. 대화 상자 및 스크립트 XML 파일을 appmondata.jar 파일에 추가하거나 이 파일에서 기존 XML 파일을 수정합니다. (기본 응용 프로그램](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)및 [기본 응용 프로그램에 대한 추가 대화 상자 XML 파일 만들기 또는 수정을 참조하십시오](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application).) [ adobe-appmondata.jar 파일에 XML 파일을 추가한 후 새 adobe-appmondata.jar 파일을 adobe-generatepdf-dsc.jar 파일에 배치합니다.
1. 추가 기본 파일 형식에 대한 지원을 추가한 경우 응용 프로그램의 경로를 제공하는 시스템 환경 변수를 만드십시오(기본 응용 프로그램](converting-file-formats-pdf.md#creating-an-environment-variable-to-locate-the-native-application)을 찾으려면 환경 변수 만들기를 참조하십시오.)[

**GeneratePDF 구성 요소를 재배포하려면**

1. Workbench에 로그인합니다.
1. **Window** > **보기 표시** > **구성 요소**&#x200B;를 선택합니다. 이 작업을 수행하면 구성 요소 보기가 워크벤치에 추가됩니다.
1. GeneratePDF 구성 요소를 마우스 오른쪽 단추로 클릭한 다음 **구성 요소 중지**&#x200B;를 선택합니다.
1. 구성 요소가 중지되면 마우스 오른쪽 단추를 클릭하고 [구성 요소 제거]를 선택하여 제거합니다.
1. **구성 요소** 아이콘을 마우스 오른쪽 단추로 클릭하고 **구성 요소 설치**&#x200B;를 선택합니다.
1. 수정된 adobe-generatepdf-dsc.jar 파일을 찾아 선택한 다음 [열기]를 클릭합니다. GeneratePDF 구성 요소 옆에 빨간색 사각형이 표시됩니다.
1. GeneratePDF 구성 요소를 확장하고 서비스 설명자를 선택한 다음 GeneratePDF 서비스를 마우스 오른쪽 버튼으로 클릭하고 서비스 활성화를 선택합니다.
1. 표시되는 구성 대화 상자에 적용 가능한 구성 값을 입력합니다. 이 값을 비워 두면 기본 구성 값이 사용됩니다.
1. [PDF 생성]을 마우스 오른쪽 단추로 클릭하고 [시작 구성 요소]를 선택합니다.
1. 활성 서비스를 확장합니다. 실행 중인 경우 서비스 이름 옆에 녹색 화살표가 나타납니다. 그렇지 않으면 서비스가 중지된 상태입니다.
1. 서비스가 중지 상태인 경우 서비스 이름을 마우스 오른쪽 단추로 클릭하고 [서비스 시작]을 선택합니다.

### 기본 응용 프로그램 {#creating-or-modifying-a-script-xml-file-for-a-native-application}에 대한 스크립트 XML 파일 만들기 또는 수정

새 기본 응용 프로그램으로 파일을 인도하려면 해당 응용 프로그램의 스크립트 XML 파일을 만들어야 합니다. PDF 생성 서비스가 이미 지원되는 기본 애플리케이션과 상호 작용하는 방식을 수정하려면 해당 애플리케이션에 대한 스크립트를 수정해야 합니다.

스크립트에는 기본 응용 프로그램의 윈도우 요소를 탐색하고 해당 요소에 대한 특정 응답을 제공하는 지침이 들어 있습니다. 이 정보를 포함하는 파일은 `appmon.`[appname]&quot;`.script.`[로케일]`.xml`입니다. 예제는 appmon.notepad.script.en_US.xml입니다.

#### 스크립트가 {#identifying-steps-the-script-must-execute}을(를) 실행해야 하는 단계를 식별합니다.

기본 응용 프로그램을 사용하여 탐색해야 하는 창 요소와 문서를 인쇄하기 위해 수행해야 하는 각 응답을 결정합니다. 응답으로 인한 대화 상자를 확인합니다. 이 단계는 다음 단계와 유사합니다.

1. 파일 > 열기를 선택합니다.
1. 경로를 지정한 다음 열기를 클릭합니다.
1. 메뉴 모음에서 파일 > 인쇄를 선택합니다.
1. 프린터에 필요한 속성을 지정합니다.
1. 인쇄를 선택하고 다른 이름으로 저장 대화 상자가 나타날 때까지 기다립니다. [PDF 생성] 서비스에서 PDF 파일의 대상을 지정하려면 [다른 이름으로 저장] 대화 상자가 필요합니다.

#### 캡션 특성 {#identifying-the-dialogs-specified-in-caption-attributes}에 지정된 대화 상자 식별

Microsoft Spy++를 사용하여 기본 응용 프로그램에서 윈도우 요소 속성의 ID를 가져옵니다. 스크립트를 작성하려면 이러한 ID가 있어야 합니다.

#### 캡션 특성에서 일반 표현식 사용 {#using-regular-expressions-in-caption-attributes}

캡션 사양에 정규 표현식을 사용할 수 있습니다. PDF 생성 서비스는 `java.util.regex.Matcher` 클래스를 사용하여 정규 표현식을 지원합니다. 이 유틸리티는 `java.util.regex.Pattern`에 설명된 일반 표현식을 지원합니다. (Java 웹 사이트([https://java.sun.com/j2se/1.4.2/docs/api/java/util/regex/Pattern.html](https://java.sun.com/j2se/1.4.2/docs/api/java/util/regex/Pattern.html))로 이동합니다.)

**메모장 배너의 메모장 앞에 있는 파일 이름을 허용하는 정규 표현식**

```xml
 <!-- The regular expression ".*Notepad" means any number of non-terminating characters followed by Notepad. -->
 <step>
     <expectedWindow>
         <window caption=".*Notepad"/>
     </expectedWindow>
 </step>
```

**인쇄 설정과 인쇄물을 구분하는 정규 표현식**

```xml
 <!-- This regular expression differentiates the Print dialog box from the Print Setup dialog box. The "^" specifies the beginning of the line, and the "$" specifies the end of the line. -->
 <windowList>
     <window controlID="0x01" caption="^Print$" action="press"/>
 </windowList>
```

#### 윈도우 및 windowList 요소 순서 지정 {#ordering-the-window-and-windowlist-elements}

다음과 같이 `window` 및 `windowList` 요소를 주문해야 합니다.

* `windowList` 또는 `dialog` 요소에서 여러 `window` 요소가 자식으로 표시되는 경우 순서에 있는 위치를 나타내는 `caption` 이름의 길이를 사용하여 해당 `window` 요소를 내림차순으로 정렬합니다.
* `window` 요소에 `windowList` 요소가 여러 개 나타나는 경우 해당 `windowList` 요소를 내림차순으로 정렬합니다(순서의 위치를 나타내는 첫 번째 `indexes/` 요소의 `caption` 특성 길이).

**대화 상자 파일에서 윈도우 요소 순서 지정**

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

**윈도우 요소 순서 지정목록 요소**

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

### 기본 응용 프로그램 {#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application}에 대한 추가 대화 상자 XML 파일 만들기 또는 수정

이전에 지원되지 않았던 기본 응용 프로그램의 스크립트를 만드는 경우 해당 응용 프로그램에 대한 추가 대화 상자 XML 파일도 만들어야 합니다. AppMon이 사용하는 모든 기본 응용 프로그램에는 하나의 추가 대화 상자 XML 파일만 있어야 합니다. 요청되지 않은 대화 상자가 없더라도 추가 대화 상자 XML 파일이 필요합니다. 추가 대화 상자에는 `window` 요소가 자리 표시자에 불과하더라도 `window` 요소가 하나 이상 있어야 합니다.

>[!NOTE]
>
>이러한 컨텍스트에서 추가 용어는 `appmon.[applicationname].addition.[locale]`.xml&#39; 파일의 내용을 의미합니다. 이러한 파일은 대화 상자 XML 파일에 대한 재정의 및 추가 사항을 지정합니다.

다음과 같은 용도로 기본 응용 프로그램에 대한 추가 대화 상자 XML 파일을 수정할 수도 있습니다.

* 다른 응답을 가진 응용 프로그램의 대화 상자 XML 파일을 재정의하려면
* 해당 응용 프로그램의 대화 상자 XML 파일에서 해결되지 않은 대화 상자에 응답을 추가하려면

추가 dialogXML 파일을 식별하는 파일 이름은 `appmon.[appname].addition.[locale].xml`입니다. 예를 들면 appmon.excel.addition.en_US.xml이 있습니다.

추가 대화 상자 XML 파일의 이름은 `appmon.[applicationname].addition.[locale].xml` 형식을 사용해야 합니다. 여기서 *applicationname*&#x200B;은 XML 구성 파일 및 스크립트에서 사용되는 응용 프로그램 이름과 정확히 일치해야 합니다.

>[!NOTE]
>
>native2pdfconfig.xml 구성 파일에 지정된 일반 응용 프로그램에 기본 대화 상자 XML 파일이 없습니다. 기본 파일 형식](converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format)에 대한 지원 추가 또는 수정 섹션에서는 이러한 사양에 대해 설명합니다.[

`window` 요소에 자식으로 표시되는 `windowList` 요소를 주문해야 합니다. 자세한 내용은 [창 및 windowList 요소 순서 지정](converting-file-formats-pdf.md#ordering-the-window-and-windowlist-elements)을 참조하십시오.

### 일반 대화 상자 XML 파일 {#modifying-the-general-dialog-xml-file} 수정

일반 대화 상자 XML 파일을 수정하여 시스템에서 생성된 대화 상자에 응답하거나 여러 응용 프로그램에서 일반적으로 사용되는 대화 상자에 응답할 수 있습니다.

#### XML 구성 파일 {#adding-a-filetype-entry-in-the-xml-configuration-file}에 파일 유형 항목 추가

이 절차에서는 파일 유형을 기본 응용 프로그램과 연결하도록 PDF 서비스 구성 파일을 업데이트하는 방법에 대해 설명합니다. 이 구성 파일을 업데이트하려면 관리 콘솔을 사용하여 구성 데이터를 파일로 내보내야 합니다. 구성 데이터의 기본 파일 이름은 native2pdfconfig.xml입니다.

**PDF 서비스 생성 구성 파일 업데이트**

1. **홈** > **서비스** > **Adobe PDF Generator** > **구성 파일**&#x200B;을 선택한 다음 **구성 내보내기**&#x200B;를 선택합니다.
1. 필요에 따라 native2pdfconfig.xml 파일의 `filetype-settings` 요소를 수정합니다.
1. **홈** > **서비스** > **Adobe PDF Generator** >**구성 파일**&#x200B;을 선택한 다음 **구성 가져오기**&#x200B;를 선택합니다. 구성 데이터를 PDF 생성 서비스로 가져와 이전 설정을 대체합니다.

>[!NOTE]
>
>응용 프로그램의 이름은 `GenericApp` 요소의 `name` 속성 값으로 지정됩니다. 이 값은 해당 응용 프로그램에 대해 개발한 스크립트에 지정된 해당 이름과 정확히 일치해야 합니다. 마찬가지로 `GenericApp` 요소의 `displayName` 속성은 해당 스크립트의 `expectedWindow` 창 캡션과 정확히 일치해야 합니다. 이러한 등가는 `displayName` 또는 `caption` 속성에 나타나는 일반 표현식을 확인한 후 평가됩니다.

이 예제에서는 파일 이름 확장명이 .txt인 파일을 처리하는 데 메모장(Microsoft Word가 아님)을 사용하도록 PDF 생성 서비스와 함께 제공된 기본 구성 데이터를 수정했습니다. 이 수정 전에 Microsoft Word가 이러한 파일을 처리해야 하는 기본 응용 프로그램으로 지정되었습니다.

**텍스트 파일을 메모장으로 이동하는 수정(native2pdfconfig.xml)**

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

#### 기본 응용 프로그램 {#creating-an-environment-variable-to-locate-the-native-application}을(를) 찾기 위한 환경 변수 만들기

기본 응용 프로그램 실행 파일의 위치를 지정하는 환경 변수를 만듭니다. 이 변수는 `[applicationname]_PATH` 형식을 사용해야 합니다. 여기서 *applicationname*&#x200B;은(는) XML 구성 파일 및 스크립트에서 사용되는 응용 프로그램 이름과 정확히 일치해야 하며, 경로에는 두 개의 따옴표로 실행 파일의 경로가 포함되어 있습니다. 이러한 환경 변수의 예는 `Photoshop_PATH`입니다.

새 환경 변수를 만든 후 PDF 생성 서비스가 배포된 서버를 다시 시작해야 합니다.

**Windows XP 환경에서 시스템 변수 만들기**

1. **Campaign 컨트롤 패널 > 시스템**&#x200B;을 선택합니다.
1. 시스템 속성 대화 상자에서 **고급** 탭을 클릭한 다음 **환경 변수**&#x200B;를 클릭합니다.
1. 환경 변수 대화 상자의 시스템 변수에서 **새로 만들기**&#x200B;를 클릭합니다.
1. 새 시스템 변수 대화 상자의 **변수 이름** 상자에 `[applicationname]_PATH` 형식을 사용하는 이름을 입력합니다.
1. **변수 값** 상자에 응용 프로그램 실행 파일의 전체 경로와 파일 이름을 입력한 다음 **확인**&#x200B;을 클릭합니다. 예를 들어 다음을 입력합니다.`c:\windows\Notepad.exe`
1. 환경 변수 대화 상자에서 **확인**&#x200B;을 클릭합니다.

**명령줄에서 시스템 변수 만들기**

1. 명령줄 창에서 다음 형식을 사용하여 변수 정의를 입력합니다.

   ```shell
            [applicationname]_PATH=[Full path name]
   ```

   예를 들어 다음을 입력합니다.`NotePad_PATH=C:\WINDOWS\NOTEPAD.EXE`

1. 시스템 변수가 적용되도록 새 명령줄 프롬프트를 시작합니다.

#### XML 파일 {#xml-files}

AEM Forms에는 [PDF 생성] 서비스에서 [메모장]을 사용하여 파일 이름 확장명이 .txt인 모든 파일을 처리하도록 하는 샘플 XML 파일이 포함되어 있습니다. 이 코드는 이 섹션에 포함되어 있습니다. 또한 이 섹션에 설명된 다른 사항을 수정해야 합니다.

#### 추가 대화 상자 XML 파일 {#additional-dialog-xml-file}

이 예에는 메모장 응용 프로그램의 추가 대화 상자가 포함되어 있습니다. 이러한 대화 상자는 PDF 생성 서비스에서 지정한 대화 상자 외에 추가할 수 있습니다.

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

이 예에서는 Adobe PDF 프린터를 사용하여 파일을 인쇄하기 위해 PDF 생성 서비스가 메모장과 상호 작용하는 방법을 지정합니다.

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

