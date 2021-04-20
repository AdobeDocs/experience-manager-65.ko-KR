---
title: Postscript를 PDF 문서로 변환
seo-title: Postscript를 PDF 문서로 변환
description: Distiller 서비스를 사용하여 네트워크를 통해 PostScript®, EPS(Encapsulated PostScript) 및 PRN 파일을 용량이 작고 안정적이며 보다 안전한 PDF 파일로 변환할 수 있습니다. Distiller 서비스는 Java API 및 웹 서비스 API를 사용하는 송장 및 명세서 등의 대량의 인쇄 문서를 전자 문서로 변환합니다.
seo-description: Distiller 서비스를 사용하여 네트워크를 통해 PostScript®, EPS(Encapsulated PostScript) 및 PRN 파일을 용량이 작고 안정적이며 보다 안전한 PDF 파일로 변환할 수 있습니다. Distiller 서비스는 Java API 및 웹 서비스 API를 사용하는 송장 및 명세서 등의 대량의 인쇄 문서를 전자 문서로 변환합니다.
uuid: 2143f406-1fdd-4551-a738-1a8388f8d478
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 06ad343a-f74d-41f5-b3c8-b85bb723ceeb
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1380'
ht-degree: 0%

---


# Postscript를 PDF 문서로 변환 {#converting-postscript-to-pdf-documents}

**이 문서의 샘플과 예는 JEE 환경의 AEM Forms에만 해당됩니다.**

## Distiller 서비스 {#about-the-distiller-service} 정보

Distiller® 서비스는 네트워크를 통해 PostScript®, EPS(Encapsulated PostScript) 및 PRN 파일을 용량이 작고 안정적이며 보다 안전한 PDF 파일로 변환합니다. Distiller 서비스는 대량의 인쇄 문서를 송장 및 명세서 같은 전자 문서로 변환하는 데 자주 사용됩니다. 또한 문서를 PDF로 변환하면 기업은 고객에게 종이 버전과 전자 버전의 문서를 보낼 수 있습니다.

>[!NOTE]
>
>Distiller 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

## PostScript를 PDF 문서 {#converting-postscript-to-pdf-documents-inner} 변환

이 항목에서는 Distiller 서비스 API(Java 및 웹 서비스)를 사용하여 PostScript(PS), EPS(Encapsulated PostScript) 및 PRN 파일을 프로그래밍 방식으로 PDF 문서로 변환하는 방법에 대해 설명합니다.

>[!NOTE]
>
>Distiller 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

>[!NOTE]
>
>PostScript 파일을 PDF 문서로 변환하려면 AEM Forms을 호스팅하는 서버에 다음 중 하나를 설치해야 합니다.Acrobat 9 또는 Microsoft Visual C++ 2005 재배포 가능 패키지.

### {#summary-of-steps} 단계 요약

지원되는 형식을 PDF 문서로 변환하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. Distiller 서비스 클라이언트를 만듭니다.
1. 변환할 파일을 검색합니다.
1. PDF 만들기 작업을 호출합니다.
1. PDF 문서를 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Distiller 서비스 클라이언트 만들기**

Distiller 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 Distiller 서비스 클라이언트를 만들어야 합니다. Java API를 사용하는 경우 `DistillerServiceClient` 개체를 만듭니다. 웹 서비스 API를 사용하는 경우 `DistillerServiceService` 개체를 만듭니다.

**변환할 파일 검색**

변환할 파일을 검색해야 합니다. 예를 들어 PS 파일을 PDF 문서로 변환하려면 PS 파일을 검색해야 합니다.

**PDF 만들기 작업 호출**

서비스 클라이언트를 만든 후 PDF 작성 작업을 호출할 수 있습니다. 이 작업을 수행하려면 대상 문서의 경로를 포함하여 변환할 문서에 대한 정보가 필요합니다.

**PDF 문서 저장**

PDF 문서를 PDF 파일로 저장할 수 있습니다.

**참고 항목**

[Java API를 사용하여 PostScript 파일을 PDF로 변환](converting-postscript-pdf-documents.md#convert-a-postscript-file-to-pdf-using-the-java-api)

[웹 서비스 API를 사용하여 PostScript 파일을 PDF로 변환](converting-postscript-pdf-documents.md#converting-a-postscript-file-to-pdf-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[출력 서비스 API 빠른 시작](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java API {#convert-a-postscript-file-to-pdf-using-the-java-api}를 사용하여 PostScript 파일을 PDF로 변환

Distiller 서비스 API(Java)를 사용하여 PostScript 파일을 PDF 문서로 변환:

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-distiller-client.jar 등의 클라이언트 JAR 파일을 포함합니다.

1. Distiller 서비스 클라이언트를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 `DistillerServiceClient` 개체를 만들고 `ServiceClientFactory` 개체를 전달합니다.

1. 변환할 파일을 검색합니다.

   * 생성자를 사용하고 파일 위치를 지정하는 문자열 값을 전달하여 변환할 파일을 나타내는 `java.io.FileInputStream` 객체를 만듭니다.
   * 생성자를 사용하여 `com.adobe.idp.Document` 개체를 만들고 `java.io.FileInputStream` 개체를 전달합니다.

1. PDF 만들기 작업을 호출합니다.

   `DistillerServiceClient` 객체의 `createPDF` 메서드를 호출하고 다음 값을 전달합니다.

   * 변환할 PS, EPS 또는 PRN 파일을 나타내는 `com.adobe.idp.Document` 개체
   * 변환할 파일의 이름을 포함하는 `java.lang.String` 개체
   * 사용할 Adobe PDF 설정의 이름을 포함하는 `java.lang.String` 개체
   * 사용할 보안 설정의 이름을 포함하는 `java.lang.String` 개체
   * PDF 문서를 생성하는 동안 적용할 설정이 포함된 선택적 `com.adobe.idp.Document` 개체
   * PDF 문서에 적용할 메타데이터 정보를 포함하는 선택적 `com.adobe.idp.Document` 개체

   `createPDF` 메서드는 새 PDF 문서를 포함하는 `CreatePDFResult` 개체와 생성할 수 있는 로그 파일을 반환합니다. 로그 파일에는 일반적으로 전환 요청으로 생성된 오류 또는 경고 메시지가 포함됩니다.

1. PDF 문서를 저장합니다.

   새로 만든 PDF 문서를 얻으려면 다음 작업을 수행합니다.

   * `CreatePDFResult` 객체의 `getCreatedDocument` 메서드를 호출합니다. `com.adobe.idp.Document` 객체를 반환합니다.
   * `com.adobe.idp.Document` 개체의 `copyToFile` 메서드를 호출하여 PDF 문서를 추출합니다.

   마찬가지로 로그 문서를 얻으려면 다음 작업을 수행합니다.

   * `CreatePDFResult` 객체의 `getLogDocument` 메서드를 호출합니다. `com.adobe.idp.Document` 객체를 반환합니다.
   * `com.adobe.idp.Document` 객체의 `copyToFile` 메서드를 호출하여 로그 문서를 추출합니다.


**참고 항목**

[단계 요약](converting-postscript-pdf-documents.md#summary-of-steps)

[빠른 시작(SOAP 모드):Java API를 사용하여 PostScript 파일을 PDF 문서로 변환](/help/forms/developing/distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API {#converting-a-postscript-file-to-pdf-using-the-web-service-api}을 사용하여 PostScript 파일을 PDF로 변환

Distiller 서비스 API(웹 서비스)를 사용하여 PostScript 파일을 PDF 문서로 변환:

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다.`http://localhost:8080/soap/services/DistillerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꿉니다.

1. Distiller 서비스 클라이언트를 만듭니다.

   * 기본 생성자를 사용하여 `DistillerServiceClient` 객체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `DistillerServiceClient.Endpoint.Address` 객체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/DistillerService?blob=mtom`). `lc_version` 특성을 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다. 그러나 MTOM을 사용하려면 `?blob=mtom`을 지정합니다.
   * `DistillerServiceClient.Endpoint.Binding` 필드의 값을 가져와서 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`으로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`로 설정합니다. 이 값을 사용하면 MTOM이 사용됩니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * AEM 양식 사용자 이름을 `DistillerServiceClient.ClientCredentials.UserName.UserName` 필드에 지정합니다.
      * 해당 암호 값을 `DistillerServiceClient.ClientCredentials.UserName.Password` 필드에 지정합니다.
      * `BasicHttpBindingSecurity.Transport.ClientCredentialType` 필드에 상수 값 `HttpClientCredentialType.Basic`을 할당합니다.
      * `BasicHttpBindingSecurity.Security.Mode` 필드에 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을 할당합니다.

1. 변환할 파일을 검색합니다.

   * 생성자를 사용하여 `BLOB` 객체를 만듭니다. 이 `BLOB` 개체는 PDF 문서로 변환할 파일을 저장하는 데 사용됩니다.
   * 생성자를 호출하고 파일을 열 모드와 파일 위치 및 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 객체를 만듭니다.
   * `System.IO.FileStream` 객체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 객체의 `Length` 속성을 가져와 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 객체의 `Read` 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * 바이트 배열의 내용으로 `MTOM` 속성을 할당하여 `BLOB` 객체를 채웁니다.

1. PDF 만들기 작업을 호출합니다.

   `DistillerServiceService` 객체의 `CreatePDF2` 메서드를 호출하고 다음 필수 값을 전달합니다.

   * 변환할 PS 파일을 나타내는 `BLOB` 개체
   * 변환할 파일의 경로 이름을 포함하는 문자열
   * 사용할 Adobe PDF 설정을 포함하는 문자열 개체(예: `Standard`)
   * 사용할 보안 설정을 포함하는 문자열 개체(예: `No Securit`y)
   * PDF 문서를 생성하는 동안 적용할 설정이 포함된 선택적 `BLOB` 개체
   * PDF 문서에 적용할 메타데이터 정보를 포함하는 선택적 `BLOB` 개체
   * PDF 문서를 저장하는 데 사용되는 `BLOB` 출력 매개 변수
   * 로그를 저장하는 데 사용되는 `BLOB` 출력 매개 변수

1. PDF 문서를 저장합니다.

   * 생성자를 호출하여 `System.IO.FileStream` 객체를 만듭니다. 서명된 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * `CreatePDF2` 메서드(출력 매개 변수)에 의해 반환된 `BLOB` 객체의 내용을 저장하는 바이트 배열을 만듭니다. `BLOB` 객체의 `MTOM` 데이터 멤버 값을 가져와 바이트 배열을 채웁니다.
   * 생성자를 호출하고 `System.IO.FileStream` 객체를 전달하여 `System.IO.BinaryWriter` 객체를 만듭니다.
   * `System.IO.BinaryWriter` 객체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 PDF 파일에 기록합니다.

**참고 항목**

[단계 요약](converting-postscript-pdf-documents.md#summary-of-steps)

<!-- UNRESOLVED LINKS
[Quick Start (MTOM): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7f01.2)

[Quick Start (SwaRef): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7eff.2)
-->

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
