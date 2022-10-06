---
title: Postscript를 PDF 문서로 변환
seo-title: Converting Postscript to PDF Documents
description: Distiller 서비스를 사용하여 PostScript®, Encapsulated PostScript(EPS) 및 PRN 파일을 네트워크를 통해 작고 안정적이며 안전한 PDF 파일로 변환합니다. Distiller 서비스는 많은 양의 인쇄 문서를 Java API 및 웹 서비스 API를 사용하는 송장 및 명세서 등의 전자 문서로 변환합니다.
seo-description: Use the Distiller service to convert PostScript®, Encapsulated PostScript (EPS), and PRN files to compact, reliable, and more secure PDF files over a network. The Distiller service converts large volumes of print documents to electronic documents, such as invoices and statements using the Java API and Web Service API.
uuid: 2143f406-1fdd-4551-a738-1a8388f8d478
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 06ad343a-f74d-41f5-b3c8-b85bb723ceeb
role: Developer
exl-id: 744df8b2-0c61-410f-89e9-20b8adddbf45
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1325'
ht-degree: 0%

---

# Postscript를 PDF 문서로 변환 {#converting-postscript-to-pdf-documents}

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms용입니다.**

## Distiller 서비스 정보 {#about-the-distiller-service}

Distiller® 서비스는 PostScript®, Encapsulated PostScript(EPS) 및 PRN 파일을 네트워크를 통해 작고 안정적이며 안전한 PDF 파일로 변환합니다. Distiller 서비스는 대량의 인쇄 문서를 송장 및 명세서 등의 전자 문서로 변환하는 데 자주 사용됩니다. 또한 문서를 PDF으로 변환하여 고객에게 종이 버전 및 문서 전자 버전을 보낼 수 있습니다.

>[!NOTE]
>
>Distiller 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

## PostScript를 PDF 문서로 변환 {#converting-postscript-to-pdf-documents-inner}

이 항목에서는 Distiller 서비스 API(Java 및 웹 서비스)를 사용하여 PS(PostScript), Encapsulated PostScript(EPS) 및 PRN 파일을 프로그래밍 방식으로 PDF 문서로 변환하는 방법에 대해 설명합니다.

>[!NOTE]
>
>Distiller 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>PostScript 파일을 PDF 문서로 변환하려면 AEM Forms을 호스팅하는 서버에 다음 중 하나를 설치해야 합니다. Acrobat 9 또는 Microsoft Visual C++ 2005 재배포 가능 패키지

### 단계 요약 {#summary-of-steps}

지원되는 형식을 PDF 문서로 변환하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. Distiller 서비스 클라이언트를 만듭니다.
1. 변환할 파일을 검색합니다.
1. PDF 만들기 작업을 호출합니다.
1. PDF 문서를 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함하십시오. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Distiller 서비스 클라이언트 만들기**

Distiller 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 Distiller 서비스 클라이언트를 만들어야 합니다. Java API를 사용하는 경우 `DistillerServiceClient` 개체. 웹 서비스 API를 사용하는 경우 `DistillerServiceService` 개체.

**변환할 파일 검색**

변환할 파일을 읽어와야 합니다. 예를 들어, PS 파일을 PDF 문서로 변환하려면 PS 파일을 검색해야 합니다.

**PDF 만들기 작업 호출**

서비스 클라이언트를 만든 후 PDF 생성 작업을 호출할 수 있습니다. 이 작업을 수행하려면 대상 문서의 경로를 포함하여 변환할 문서에 대한 정보가 필요합니다.

**PDF 문서를 저장합니다**

PDF 문서를 PDF 파일로 저장할 수 있습니다.

**추가 참조**

[Java API를 사용하여 PostScript 파일을 PDF으로 변환](converting-postscript-pdf-documents.md#convert-a-postscript-file-to-pdf-using-the-java-api)

[웹 서비스 API를 사용하여 PostScript 파일을 PDF으로 변환](converting-postscript-pdf-documents.md#converting-a-postscript-file-to-pdf-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[출력 서비스 API 빠른 시작](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java API를 사용하여 PostScript 파일을 PDF으로 변환 {#convert-a-postscript-file-to-pdf-using-the-java-api}

Distiller 서비스 API(Java)를 사용하여 PostScript 파일을 PDF 문서로 변환합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-distiller-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. Distiller 서비스 클라이언트를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 객체입니다.
   * 만들기 `DistillerServiceClient` 생성자를 사용하여 객체를 전달하고 `ServiceClientFactory` 개체.

1. 변환할 파일을 검색합니다.

   * 만들기 `java.io.FileInputStream` 생성자를 사용하여 변환할 파일을 나타내고 파일의 위치를 지정하는 문자열 값을 전달하는 개체입니다.
   * 만들기 `com.adobe.idp.Document` 생성자를 사용하여 객체를 전달하고 `java.io.FileInputStream` 개체.

1. PDF 만들기 작업을 호출합니다.

   를 호출합니다 `DistillerServiceClient` 개체 `createPDF` 메서드를 사용하여 다음 값을 전달합니다.

   * 다음 `com.adobe.idp.Document` 변환할 PS, EPS 또는 PRN 파일을 나타내는 개체입니다
   * A `java.lang.String` 변환할 파일의 이름을 포함하는 개체
   * A `java.lang.String` 사용할 Adobe PDF 설정의 이름을 포함하는 개체
   * A `java.lang.String` 사용할 보안 설정의 이름을 포함하는 객체입니다
   * 선택 사항입니다 `com.adobe.idp.Document` PDF 문서를 생성하는 동안 적용할 설정이 포함된 객체입니다.
   * 선택 사항입니다 `com.adobe.idp.Document` PDF 문서에 적용할 메타데이터 정보를 포함하는 객체입니다.

   다음 `createPDF` 메서드 반환 `CreatePDFResult` 새 PDF 문서와 생성될 수 있는 로그 파일을 포함하는 객체입니다. 로그 파일에는 일반적으로 전환 요청으로 생성된 오류 또는 경고 메시지가 포함됩니다.

1. PDF 문서를 저장합니다.

   새로 만든 PDF 문서를 가져오려면 다음 작업을 수행하십시오.

   * 를 호출합니다 `CreatePDFResult` 개체 `getCreatedDocument` 메서드를 사용합니다. 이는 를 반환합니다 `com.adobe.idp.Document` 개체.
   * 를 호출합니다 `com.adobe.idp.Document` 개체 `copyToFile` PDF 문서를 추출하는 방법입니다.

   마찬가지로 로그 문서를 가져오려면 다음 작업을 수행합니다.

   * 를 호출합니다 `CreatePDFResult` 개체 `getLogDocument` 메서드를 사용합니다. 이는 를 반환합니다 `com.adobe.idp.Document` 개체.
   * 를 호출합니다 `com.adobe.idp.Document` 개체 `copyToFile` 로그 문서를 추출하는 방법입니다.


**추가 참조**

[단계 요약](converting-postscript-pdf-documents.md#summary-of-steps)

[빠른 시작(SOAP 모드): Java API를 사용하여 PostScript 파일을 PDF 문서로 변환](/help/forms/developing/distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 PostScript 파일을 PDF으로 변환 {#converting-a-postscript-file-to-pdf-using-the-web-service-api}

Distiller 서비스 API(웹 서비스)를 사용하여 PostScript 파일을 PDF 문서로 변환합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/DistillerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` (AEM Forms을 호스팅하는 서버의 IP 주소 사용)

1. Distiller 서비스 클라이언트를 만듭니다.

   * 만들기 `DistillerServiceClient` 기본 생성자를 사용하여 개체를 만듭니다.
   * 만들기 `DistillerServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/DistillerService?blob=mtom`) 를 사용할 필요가 없습니다 `lc_version` 속성을 사용합니다. 이 속성은 서비스 참조를 만들 때 사용됩니다. 하지만, `?blob=mtom` MTOM을 사용하려면 다음을 수행하십시오.
   * 만들기 `System.ServiceModel.BasicHttpBinding` 개체의 값을 가져와서 `DistillerServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스팅합니다. `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름을 지정합니다 `DistillerServiceClient.ClientCredentials.UserName.UserName`.
      * 필드에 해당 암호 값을 지정합니다 `DistillerServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 할당 `HttpClientCredentialType.Basic` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 상수 값 할당 `BasicHttpSecurityMode.TransportCredentialOnly` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Security.Mode`.

1. 변환할 파일을 검색합니다.

   * 만들기 `BLOB` 생성자를 사용하여 개체를 작성합니다. 이 `BLOB` 개체를 사용하여 PDF 문서로 변환할 파일을 저장합니다.
   * 만들기 `System.IO.FileStream` 객체를 사용하여 해당 생성자를 호출하고 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 내용을 저장하는 바이트 배열을 만듭니다 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성을 사용합니다.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채웁니다 `System.IO.FileStream` 개체 `Read` 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하는 메서드와 전달
   * 을(를) 채우기 `BLOB` 개체를 할당하여 개체를 개체 개체 `MTOM` 바이트 배열의 내용을 포함하는 속성입니다.

1. PDF 만들기 작업을 호출합니다.

   를 호출합니다 `DistillerServiceService` 개체 `CreatePDF2` 메서드를 사용하여 다음 필수 값을 전달합니다.

   * 다음 `BLOB` 변환할 PS 파일을 나타내는 개체
   * 변환할 파일의 경로 이름을 포함하는 문자열입니다
   * 사용할 Adobe PDF 설정을 포함하는 문자열 개체(예: `Standard`)
   * 사용할 보안 설정을 포함하는 문자열 개체(예: `No Securit`y)
   * 선택 사항입니다 `BLOB` PDF 문서를 생성하는 동안 적용할 설정이 포함된 객체입니다.
   * 선택 사항입니다 `BLOB` PDF 문서에 적용할 메타데이터 정보를 포함하는 객체입니다.
   * A `BLOB` PDF 문서를 저장하는 데 사용되는 출력 매개 변수
   * A `BLOB` 로그를 저장하는 데 사용되는 출력 매개 변수

1. PDF 문서를 저장합니다.

   * 만들기 `System.IO.FileStream` 개체를 생성자로 호출하여 개체를 가져옵니다. 서명된 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 내용을 저장하는 바이트 배열을 만듭니다 `BLOB` 반환되는 개체 `CreatePDF2` 메서드(출력 매개 변수) 의 값을 가져와서 바이트 배열을 채웁니다 `BLOB` 개체 `MTOM` 데이터 멤버.
   * 만들기 `System.IO.BinaryWriter` 생성자를 호출하고 전달하여 개체를 `System.IO.FileStream` 개체.
   * 를 호출하여 PDF 파일에 바이트 배열의 내용을 씁니다. `System.IO.BinaryWriter` 개체 `Write` 메서드를 사용하여 바이트 배열을 전달합니다.

**추가 참조**

[단계 요약](converting-postscript-pdf-documents.md#summary-of-steps)

<!-- UNRESOLVED LINKS
[Quick Start (MTOM): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7f01.2)

[Quick Start (SwaRef): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7eff.2)
-->

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
