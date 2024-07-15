---
title: PDF을 Postscript 및 이미지 파일로 변환
description: PDF 변환 서비스를 사용하여 PDF 문서를 Java API 및 웹 서비스 API를 사용하여 PostScript 및 여러 이미지 형식(JPEG, JPEG 2000, PNG 및 TIFF)으로 변환합니다.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 31730c24-46c3-4111-9391-ccd4342740e9
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2774'
ht-degree: 0%

---

# PDF을 포스트스크립트 및 이미지 파일로 변환 {#converting-pdf-to-postscript-andimage-files}

**이 문서의 샘플과 예제는 JEE 환경의 AEM Forms에 대해서만 적용됩니다.**

**변환 PDF 서비스 정보**

PDF 변환 서비스는 PDF 문서를 PostScript 및 여러 이미지 형식(JPEG, JPEG 2000, PNG 및 TIFF)으로 변환합니다. PDF 문서를 PostScript으로 변환하면 PostScript 프린터에서 무인 서버 기반 인쇄에 유용합니다. PDF 문서를 다중 페이지 TIFF 파일로 변환하는 것은 PDF 문서를 지원하지 않는 컨텐츠 관리 시스템에 문서를 보관할 때 실용적입니다.

PDF 변환 서비스를 사용하여 다음 작업을 수행할 수 있습니다.

* PDF 문서를 PostScript으로 변환합니다.
* PDF 문서를 이미지 형식으로 변환합니다.

>[!NOTE]
>
>PDF 변환 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

## PDF 문서를 PostScript으로 변환 {#converting-pdf-documents-to-postscript}

이 항목에서는 PDF 서비스 API(Java 및 웹 서비스) 변환을 사용하여 PDF 문서를 프로그래밍 방식으로 PostScript 파일로 변환하는 방법에 대해 설명합니다. PostScript 파일로 변환되는 PDF 문서는 비대화형 PDF 문서여야 합니다. 즉, 대화형 PDF 문서를 PostScript 파일로 변환하려고 하면 예외가 발생합니다.

>[!NOTE]
>
>PDF 변환 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary-of-steps}

PDF 문서를 PostScript 파일로 변환하려면 다음 단계를 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. 변환 PDF 서비스 클라이언트를 만듭니다.
1. PDF 문서를 참조하여 PostScript 파일로 변환합니다.
1. 전환 런타임 옵션을 설정합니다.
1. PDF 문서를 PostScript 파일로 변환합니다.
1. PostScript 파일을 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**변환 PDF 클라이언트 만들기**

PDF 서비스 변환 작업을 프로그래밍 방식으로 수행하려면 먼저 PDF 서비스 변환 클라이언트를 만들어야 합니다. Java API를 사용하는 경우 `ConvertPdfServiceClient` 개체를 만듭니다. 웹 서비스 API를 사용하는 경우 `ConvertPDFServiceService` 개체를 만듭니다.

이 섹션에서는 AEM Forms에 도입된 웹 서비스 기능을 사용합니다. 새 기능에 액세스하려면 `lc_version` 특성을 사용하여 프록시 개체를 구성해야 합니다. [웹 서비스를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)에서 &quot;웹 서비스를 사용하여 새 기능 액세스&quot;를 참조하십시오.

**PostScript 파일로 변환하려면 PDF 문서를 참조합니다**

PostScript 파일로 변환할 PDF 문서를 참조합니다. 이 항목의 앞부분에서 언급했듯이 PDF 문서는 비대화형 PDF 문서여야 합니다. 대화형 PDF 문서를 PostScript 파일로 변환하려고 하면 예외가 발생합니다.

**전환 실행 시간 옵션 설정**

PDF 문서를 PostScript 파일로 변환할 때 생성되는 PostScript 유형을 지정하는 런타임 옵션을 정의할 수 있습니다. 예를 들어 레벨 3 PostScript 파일을 정의할 수 있습니다.

일반적으로 생성된 PostScript 파일은 입력 PDF 문서의 크기를 반영합니다. `ShrinkToFit` 옵션을 선택하면(PostScript 파일의 출력을 페이지에 맞게 축소) 입력 PDF 문서와 생성된 PostScript 파일 간에 차이가 나타나지 않습니다. `ShrinkToFit` 옵션은 입력 PDF 문서보다 작은 페이지 크기로 인쇄하도록 선택한 경우에만 적용됩니다. 더 작은 페이지 크기를 선택하려면 `PageSize` 옵션을 정의합니다. 또한 올바른 PostScript 출력을 가져오려면 `RotateAndCenter` 옵션을 `true`(으)로 설정하는 것이 좋습니다.

마찬가지로 `ExpandToFit` 옵션을 선택하면(페이지에 맞게 PostScript 파일의 출력이 확장됨) 입력 PDF 문서보다 더 큰 페이지 크기로 인쇄하도록 선택한 경우에만 적용됩니다. 더 큰 페이지 크기를 선택하려면 `PageSize` 옵션을 정의합니다. 또한 올바른 PostScript 출력을 가져오려면 `RotateAndCenter` 옵션을 `true`(으)로 설정하는 것이 좋습니다.

>[!NOTE]
>
>설정할 수 있는 런타임 값에 대한 자세한 내용은 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)의 `ToPSOptionsSpec` 클래스 참조를 참조하십시오.

**PDF 문서를 PostScript 파일로 변환**

서비스 클라이언트를 만들고 런타임 옵션을 설정한 후 PostScript 변환 작업을 호출할 수 있습니다. 이 작업에는 대상 문서에 대한 기본 PostScript 수준을 포함하여 변환할 문서에 대한 정보가 필요합니다.

**PostScript 파일 저장**

PDF 문서를 PostScript으로 변환한 후 출력을 PostScript 파일로 저장할 수 있습니다.

**추가 참조**

[Java API를 사용하여 PDF 문서를 PS로 변환](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-java-api)

[웹 서비스 API를 사용하여 PDF 문서를 PS로 변환](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF 서비스 API 빠른 시작 전환](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Java API를 사용하여 PDF 문서를 PS로 변환 {#convert-a-pdf-document-to-ps-using-the-java-api}

Java(PDF 서비스 API) 변환을 사용하여 PDF 문서를 PostScript으로 변환합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-convertpdf-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. 변환 PDF 클라이언트를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하고 `ServiceClientFactory` 개체를 전달하여 `ConvertPdfServiceClient` 개체를 만듭니다.

1. PDF 문서를 참조하여 PostScript 파일로 변환합니다.

   * 생성자를 사용하여 `java.io.FileInputStream` 개체를 만들고 변환할 PDF 문서의 위치를 지정하는 문자열 값을 전달합니다.
   * `com.adobe.idp.Document` 생성자를 사용하여 PDF 문서를 저장하는 `com.adobe.idp.Document` 개체를 만듭니다. PDF 문서가 포함된 `java.io.FileInputStream` 개체를 전달합니다.

1. 전환 런타임 옵션을 설정합니다.

   * 해당 생성자를 호출하여 `ToPSOptionsSpec` 개체를 만듭니다.
   * `ToPSOptionsSpec` 개체에 속하는 적절한 메서드를 호출하여 런타임 옵션을 설정하십시오. 예를들어, 만들어지는 PostScript 수준을 정의하려면 `ToPSOptionsSpec` 개체의 `setPsLevel` 메서드를 호출하고 PostScript 수준을 지정하는 `PSLevel` 열거형 값을 전달합니다. 설정할 수 있는 모든 런타임 값에 대한 자세한 내용은 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)의 `ToPSOptionsSpec` 클래스 참조를 참조하십시오.

1. PDF 문서를 PostScript 파일로 변환합니다.

   `ConvertPdfServiceClient`개체의 `toPS2` 메서드를 호출하고 다음 값을 전달하십시오.

   * PostScript 파일로 변환할 PDF 문서를 나타내는 `com.adobe.idp.Document` 개체입니다.
   * PostScript 런타임 옵션을 지정하는 `ToPSOptionsSpec` 개체입니다.

   `toPS2` 메서드가 새 PostScript 문서를 포함하는 `Document` 개체를 반환합니다.

1. PostScript 파일을 저장합니다.

   * `java.io.File` 개체를 만들고 파일 이름 확장명이 .ps인지 확인하십시오.
   * `Document` 개체의 `copyToFile` 메서드를 호출하여 `Document` 개체의 내용을 파일에 복사합니다(`toPS2` 메서드에서 반환된 `Document` 개체를 사용하는지 확인).

**추가 참조**

[단계 요약](converting-pdf-postscript-image-files.md#summary-of-steps)

[빠른 시작(SOAP 모드): Java API를 사용하여 PDF 문서를 PostScript으로 변환](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 PDF 문서를 PS로 변환 {#convert-a-pdf-document-to-ps-using-the-web-service-api}

PDF 서비스 API 변환(웹 서비스)을 사용하여 PDF 문서를 PostScript으로 변환합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. WSDL 정의 `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`을(를) 사용하는지 확인하십시오.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꾸십시오.

1. 변환 PDF 클라이언트를 만듭니다.

   * 기본 생성자를 사용하여 `ConvertPdfServiceClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `ConvertPdfServiceClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`). `lc_version` 특성은 사용할 필요가 없습니다. 그러나 `?blob=mtom`을(를) 지정하십시오.
   * `ConvertPdfServiceClient.Endpoint.Binding` 필드의 값을 가져와 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`(으)로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * `ConvertPdfServiceClient.ClientCredentials.UserName.UserName` 필드에 AEM Forms 사용자 이름을 지정하십시오.
      * 필드 `ConvertPdfServiceClient.ClientCredentials.UserName.Password`에 해당 암호 값을 지정하십시오.
      * 상수 값 `HttpClientCredentialType.Basic`을(를) 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.
      * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을(를) 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. PDF 문서를 참조하여 PostScript 파일로 변환합니다.

   * 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 PostScript 파일로 변환된 PDF 문서를 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하고 변환할 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하고 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * 해당 `MTOM` 필드를 바이트 배열의 내용으로 할당하여 `BLOB` 개체를 채웁니다.

1. 전환 런타임 옵션을 설정합니다.

   * 해당 생성자를 호출하여 `ToPSOptionsSpec` 개체를 만듭니다.
   * `ToPSOptionsSpec` 개체의 데이터 멤버에 값을 할당하여 런타임 옵션을 설정합니다. 예를 들어, 만들어지는 PostScript 수준을 정의하려면 `ToPSOptionsSpec` 개체의 `psLevel` 데이터 멤버에 `PSLevel` 열거형 값을 할당합니다.

1. PDF 문서를 PostScript 파일로 변환합니다.

   `GeneratePDFServiceService` 개체의 `toPS2` 메서드를 호출하고 다음 값을 전달하십시오.

   * PostScript 파일로 변환할 PDF 문서를 나타내는 `BLOB` 개체입니다
   * 런타임 옵션을 지정하는 `ToPSOptionsSpec` 개체

   변환이 완료되면 `BLOB` 개체의 `MTOM` 속성에 액세스하여 PostScript 문서를 나타내는 이진 데이터를 추출하십시오. PostScript 파일에 쓸 수 있는 바이트 배열이 반환됩니다.

1. PostScript 파일을 저장합니다.

   * 해당 생성자를 호출하여 `System.IO.FileStream` 개체를 만듭니다. PS 파일의 파일 위치를 나타내는 문자열 값을 전달합니다.
   * `encryptPDFUsingPassword` 메서드에서 반환된 `BLOB` 개체의 데이터 내용을 저장하는 바이트 배열을 만듭니다. `BLOB` 개체의 `MTOM` 필드 값을 가져와서 바이트 배열을 채웁니다.
   * 해당 생성자를 호출하고 `System.IO.FileStream` 개체를 전달하여 `System.IO.BinaryWriter` 개체를 만듭니다.
   * `System.IO.BinaryWriter` 개체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 PostScript 파일에 씁니다.

**추가 참조**

[단계 요약](converting-pdf-postscript-image-files.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## PDF 문서를 이미지 형식으로 변환 {#converting-pdf-documents-to-image-formats}

PDF 변환 서비스를 사용하여 PDF 문서를 프로그래밍 방식으로 JPEG, JPEG 2000, TIFF 및 PNG를 포함하는 이미지 형식으로 변환할 수 있습니다. PDF 문서를 이미지 파일로 변환하면 PDF 문서를 이미지 파일로 사용할 수 있습니다. 예를 들어, 이미지를 스토리지를 위한 엔터프라이즈 컨텐츠 관리 시스템에 배치할 수 있습니다.

PDF 문서를 이미지로 변환할 때 PDF 변환 서비스는 문서의 각 페이지에 대해 별도의 이미지를 만듭니다. 즉, 문서에 20페이지가 있으면 PDF 변환 서비스에서 20개의 이미지 파일을 만듭니다. PDF 문서를 이미지 형식으로 변환할 때 PDF 문서 내의 각 페이지에 대해 개별 이미지를 만들거나 전체 PDF 문서에 대해 단일 이미지 파일을 만들 수 있습니다.

>[!NOTE]
>
>PDF 변환 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary_of_steps-1}

PDF 문서를 지원되는 유형으로 변환하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. 변환 PDF 서비스 클라이언트를 만듭니다.
1. 변환할 PDF 문서를 검색합니다.
1. 런타임 옵션을 설정합니다.
1. PDF을 이미지로 변환합니다.
1. 컬렉션에서 이미지 파일을 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**변환 PDF 클라이언트 만들기**

PDF 서비스 변환 작업을 프로그래밍 방식으로 수행하려면 먼저 PDF 서비스 변환 클라이언트를 만들어야 합니다. Java API를 사용하는 경우 `ConvertPdfServiceClient` 개체를 만듭니다. 웹 서비스 API를 사용하는 경우 `ConvertPDFServiceService` 개체를 만듭니다.

**변환할 PDF 문서 검색**

PDF 문서를 검색하여 이미지로 변환합니다. 대화형 PDF 문서를 이미지로 변환할 수 없습니다. 그렇게 하려고 하면 예외가 발생합니다. 대화형 PDF 문서를 이미지 파일로 변환하려면 변환하기 전에 PDF 문서를 병합해야 합니다. ([PDF 문서 병합](/help/forms/developing/creating-document-output-streams.md#flattening-pdf-documents)을(를) 참조하십시오.)

**런타임 옵션 설정**

이미지 형식 및 해상도 값과 같은 런타임 옵션을 설정합니다. 런타임 값에 대한 자세한 내용은 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)의 `ToImageOptionsSpec` 클래스 참조를 참조하십시오.

**PDF을 이미지로 변환**

서비스 클라이언트를 만들고 런타임 옵션을 설정한 후 PDF 문서를 이미지로 변환할 수 있습니다. 이미지가 포함된 컬렉션 개체가 반환됩니다.

**컬렉션에서 이미지 파일 검색**

PDF 변환 서비스가 반환하는 컬렉션 개체에서 이미지 파일을 검색할 수 있습니다. 컬렉션의 각 요소는 JPG 파일과 같은 이미지 파일로 저장할 수 있는 `com.adobe.idp.Document` 인스턴스(또는 웹 서비스를 사용하는 경우 `BLOB` 인스턴스)입니다.

이미지 파일의 형식은 `ImageConvertFormat` 런타임 옵션에 따라 다릅니다. 즉, `ImageConvertFormat` 런타임 옵션을 `ImageConvertFormat.JPEG`(으)로 설정하면 이미지 파일을 JPG 파일로 저장할 수 있습니다.

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF 서비스 API 빠른 시작 전환](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Java API를 사용하여 PDF 문서를 이미지 파일로 변환 {#convert-a-pdf-document-to-image-files-using-the-java-api}

Java(PDF 서비스 API 변환)를 사용하여 PDF 문서를 이미지 형식으로 변환합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-convertpdf-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. 변환 PDF 클라이언트를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하고 `ServiceClientFactory` 개체를 전달하여 `ConvertPdfServiceClient` 개체를 만듭니다.

1. 변환할 PDF 문서를 검색합니다.

   * 생성자를 사용하고 PDF 문서의 위치를 지정하는 문자열 값을 전달하여 변환할 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만듭니다.
   * 생성자를 사용하고 `java.io.FileInputStream` 개체를 전달하여 `com.adobe.idp.Document` 개체를 만듭니다.

1. 런타임 옵션을 설정합니다.

   * 해당 생성자를 사용하여 `ToImageOptionsSpec` 개체를 만듭니다.
   * 필요에 따라 이 개체에 속하는 메서드를 호출합니다. 예를 들어 `setImageConvertFormat` 메서드를 호출하고 형식 유형을 지정하는 `ImageConvertFormat` 열거형 값을 전달하여 이미지 형식을 설정합니다.

   >[!NOTE]
   >
   >`ImageConvertFormat` 열거형 값은 필수입니다.

1. PDF을 이미지로 변환합니다.

   `ConvertPdfServiceClient` 개체의 `toImage2` 메서드를 호출하고 다음 값을 전달하십시오.

   * 변환할 PDF 파일을 나타내는 `com.adobe.idp.Document` 개체입니다.
   * 대상 이미지 형식에 대한 다양한 환경 설정이 포함된 `com.adobe.livecycle.converpdfservice.client.ToImageOptionsSpec` 개체입니다.

   `toImage2` 메서드가 이미지를 포함하는 `java.util.List` 개체를 반환합니다. 컬렉션의 각 요소는 `com.adobe.idp.Document` 인스턴스입니다.

1. 컬렉션에서 이미지 파일을 검색합니다.

   `java.util.List` 개체를 반복하여 이미지가 있는지 확인합니다. 각 요소는 `com.adobe.idp.Document` 인스턴스입니다. `com.adobe.idp.Document` 개체의 `copyToFile` 메서드를 호출하고 `java.io.File` 개체를 전달하여 이미지를 저장합니다.

**추가 참조**

[빠른 시작(SOAP 모드): Java API를 사용하여 PDF 문서를 JPEG 파일로 변환](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api)

### 웹 서비스 API를 사용하여 PDF 문서를 이미지 파일로 변환 {#convert-a-pdf-document-to-image-files-using-the-web-service-api}

PDF 서비스 API(웹 서비스) 변환을 사용하여 PDF 문서를 이미지 형식으로 변환합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. WSDL 정의 `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`을(를) 사용하는지 확인하십시오.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꾸십시오.

1. 변환 PDF 클라이언트를 만듭니다.

   * 기본 생성자를 사용하여 `ConvertPdfServiceClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `ConvertPdfServiceClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`). `lc_version` 특성은 사용할 필요가 없습니다. 그러나 `?blob=mtom`을(를) 지정하십시오.
   * `ConvertPdfServiceClient.Endpoint.Binding` 필드의 값을 가져와 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`(으)로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * `ConvertPdfServiceClient.ClientCredentials.UserName.UserName` 필드에 AEM Forms 사용자 이름을 지정하십시오.
      * 필드 `ConvertPdfServiceClient.ClientCredentials.UserName.Password`에 해당 암호 값을 지정하십시오.
      * 상수 값 `HttpClientCredentialType.Basic`을(를) 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.
      * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을(를) 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. 변환할 PDF 문서를 검색합니다.

   * 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다. 이 `BLOB` 개체는 PDF 양식을 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하여 `System.IO.FileStream` 개체를 만듭니다. PDF 폼의 위치와 파일을 열 모드를 지정하는 문자열 값을 전달합니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정합니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하여 바이트 배열을 스트림 데이터로 채웁니다. 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 해당 `MTOM` 필드를 바이트 배열의 내용으로 할당하여 `BLOB` 개체를 채웁니다.

1. 런타임 옵션을 설정합니다.

   * 해당 생성자를 사용하여 `ToImageOptionsSpec` 개체를 만듭니다.
   * 필요에 따라 이 개체에 속하는 메서드를 호출합니다. 예를들어 `setImageConvertFormat` 메서드를 호출하고 형식 형식을 지정하는 `ImageConvertFormat` 열거형 값을 전달하여 이미지 형식을 설정합니다.

   >[!NOTE]
   >
   >`ImageConvertFormat` 열거형 값은 필수입니다.

1. PDF을 이미지로 변환합니다.

   `ConvertPDFServiceService` 개체의 `toImage2` 메서드를 호출하고 다음 값을 전달하십시오.

   * 변환할 파일을 나타내는 `BLOB` 개체입니다
   * 대상 이미지 형식에 대한 다양한 환경 설정이 포함된 `ToImageOptionsSpec` 개체

   `toImage2` 메서드가 새로 만든 이미지 파일을 포함하는 `MyArrayOfBLOB` 개체를 반환합니다.

1. 컬렉션에서 이미지 파일을 검색합니다.

   * `Count` 필드의 값을 가져와서 `MyArrayOfBLOB` 개체의 요소 수를 결정합니다. 각 요소는 이미지를 포함하는 `BLOB` 개체입니다.
   * `MyArrayOfBLOB` 개체를 반복하고 각 이미지 파일을 저장합니다.

**추가 참조**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
