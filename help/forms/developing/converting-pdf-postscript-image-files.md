---
title: PDF을 Postscript 및 이미지 파일로 변환
description: PDF 변환 서비스를 사용하여 PDF 문서를 Java API 및 웹 서비스 API를 사용하여 PostScript와 여러 이미지 형식(JPEG, JPEG 2000, PNG 및 TIFF)으로 변환합니다.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 31730c24-46c3-4111-9391-ccd4342740e9
solution: Experience Manager, Experience Manager Forms
source-git-commit: 872e2de411f51b5f0b26a2ff47cb49f01313d39f
workflow-type: tm+mt
source-wordcount: '2774'
ht-degree: 0%

---

# PDF을 포스트스크립트 및 이미지 파일로 변환 {#converting-pdf-to-postscript-andimage-files}

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms에 대해서만 적용됩니다.**

**변환 PDF 서비스 정보**

PDF 변환 서비스는 PDF 문서를 PostScript와 여러 이미지 형식(JPEG, JPEG 2000, PNG 및 TIFF)으로 변환합니다. PDF 문서를 PostScript로 변환하면 모든 PostScript 프린터에서 무인 서버 기반 인쇄에 유용합니다. PDF 문서를 다중 페이지 TIFF 파일로 변환하는 것은 PDF 문서를 지원하지 않는 컨텐츠 관리 시스템에 문서를 보관할 때 실용적입니다.

PDF 변환 서비스를 사용하여 다음 작업을 수행할 수 있습니다.

* PDF 문서를 PostScript로 변환합니다.
* PDF 문서를 이미지 형식으로 변환합니다.

>[!NOTE]
>
>PDF 변환 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

## PDF 문서를 포스트스크립트로 변환 {#converting-pdf-documents-to-postscript}

이 항목에서는 Convert PDF 서비스 API(Java 및 웹 서비스)를 사용하여 PDF 문서를 프로그래밍 방식으로 PostScript 파일로 변환하는 방법에 대해 설명합니다. PostScript 파일로 변환되는 PDF 문서는 비대화형 PDF 문서여야 합니다. 즉, 대화형 PDF 문서를 PostScript 파일로 변환하려고 하면 예외가 발생합니다.

>[!NOTE]
>
>PDF 변환 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

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

PDF 서비스 변환 작업을 프로그래밍 방식으로 수행하려면 먼저 PDF 서비스 변환 클라이언트를 만들어야 합니다. Java API를 사용하는 경우 `ConvertPdfServiceClient` 개체. 웹 서비스 API를 사용하는 경우 `ConvertPDFServiceService` 개체.

이 섹션에서는 AEM Forms에 도입된 웹 서비스 기능을 사용합니다. 새 기능에 액세스하려면 다음을 사용하여 프록시 개체를 구성해야 합니다. `lc_version` 특성. (&quot;웹 서비스를 사용하여 새 기능 액세스&quot; 참조) [웹 서비스를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)

**PDF 문서를 참조하여 PostScript 파일로 변환**

PostScript 파일로 변환할 PDF 문서를 참조합니다. 이 항목의 앞부분에서 언급했듯이 PDF 문서는 비대화형 PDF 문서여야 합니다. 대화형 PDF 문서를 PostScript 파일로 변환하려고 하면 예외가 발생합니다.

**전환 런타임 옵션 설정**

PDF 문서를 PostScript 파일로 변환할 때 생성되는 PostScript 유형을 지정하는 런타임 옵션을 정의할 수 있습니다. 예를 들어 레벨 3 PostScript 파일을 정의할 수 있습니다.

일반적으로 생성된 PostScript 파일은 입력 PDF 문서의 크기를 반영합니다. 을(를) 선택하는 경우 `ShrinkToFit` 옵션(페이지에 맞게 PostScript 파일의 출력을 축소함)을 사용하면 입력 PDF 문서와 생성된 PostScript 파일 간에 차이가 나타나지 않습니다. 다음 `ShrinkToFit` 옵션은 입력 PDF 문서보다 작은 페이지 크기로 인쇄하도록 선택한 경우에만 적용됩니다. 더 작은 페이지 크기를 선택하려면 `PageSize` 옵션을 선택합니다. 또한 다음을 설정하는 것이 좋습니다. `RotateAndCenter` 옵션 대상 `true` 올바른 PostScript 출력을 가져옵니다.

마찬가지로, `ExpandToFit` 옵션(PostScript 파일의 출력을 페이지에 맞게 확장)은 입력 PDF 문서보다 큰 페이지 크기로 인쇄하도록 선택하는 경우에만 적용됩니다. 더 큰 페이지 크기를 선택하려면 다음을 정의합니다. `PageSize` 옵션을 선택합니다. 또한 다음을 설정하는 것이 좋습니다. `RotateAndCenter` 옵션 대상 `true` 올바른 PostScript 출력을 가져옵니다.

>[!NOTE]
>
>설정할 수 있는 런타임 값에 대한 자세한 내용은 `ToPSOptionsSpec` 의 클래스 참조 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**PDF 문서를 PostScript 파일로 변환**

서비스 클라이언트를 만들고 런타임 옵션을 설정한 후 PostScript 변환 작업을 호출할 수 있습니다. 이 작업에는 대상 문서에 대한 기본 PostScript 수준을 포함하여 변환할 문서에 대한 정보가 필요합니다.

**PostScript 파일 저장**

PDF 문서를 PostScript로 변환한 후 출력을 PostScript 파일로 저장할 수 있습니다.

**추가 참조**

[Java API를 사용하여 PDF 문서를 PS로 변환](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-java-api)

[웹 서비스 API를 사용하여 PDF 문서를 PS로 변환](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF 서비스 API 빠른 시작 전환](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Java API를 사용하여 PDF 문서를 PS로 변환 {#convert-a-pdf-document-to-ps-using-the-java-api}

Java(PDF 서비스 API 변환)를 사용하여 PDF 문서를 PostScript로 변환합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-convertpdf-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. 변환 PDF 클라이언트를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.
   * 만들기 `ConvertPdfServiceClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체.

1. PDF 문서를 참조하여 PostScript 파일로 변환합니다.

   * 만들기 `java.io.FileInputStream` 개체를 생성자를 사용하여 변환하고 변환할 PDF 문서의 위치를 지정하는 문자열 값을 전달합니다.
   * 만들기 `com.adobe.idp.Document` 를 사용하여 PDF 문서를 저장하는 개체 `com.adobe.idp.Document` 생성자입니다. 전달 `java.io.FileInputStream` PDF 문서가 포함된 객체입니다.

1. 전환 런타임 옵션을 설정합니다.

   * 만들기 `ToPSOptionsSpec` 해당 생성자를 호출하여 개체를 작성합니다.
   * 에 속한 적절한 메서드를 호출하여 런타임 옵션을 설정합니다. `ToPSOptionsSpec` 개체. 예를 들어 생성되는 PostScript 수준을 정의하려면 `ToPSOptionsSpec` 개체 `setPsLevel` 방법 및 전달 `PSLevel` PostScript 수준을 지정하는 열거형 값입니다. 설정할 수 있는 모든 런타임 값에 대한 자세한 내용은 `ToPSOptionsSpec` 의 클래스 참조 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. PDF 문서를 PostScript 파일로 변환합니다.

   호출 `ConvertPdfServiceClient`개체 `toPS2` 메서드를 실행하고 다음 값을 전달합니다.

   * A `com.adobe.idp.Document` PostScript 파일로 변환할 PDF 문서를 나타내는 개체입니다.
   * A `ToPSOptionsSpec` postScript 런타임 옵션을 지정하는 개체입니다.

   다음 `toPS2` 메서드가 을 반환합니다. `Document` 새 PostScript 문서가 포함된 개체입니다.

1. PostScript 파일을 저장합니다.

   * 만들기 `java.io.File` 개체를 클릭하고 파일 이름 확장명이 .ps인지 확인하십시오.
   * 호출 `Document` 개체 `copyToFile` 콘텐츠 복사 방법 `Document` 파일에 대한 개체(를 사용해야 함) `Document` 에서 반환한 개체 `toPS2` 메서드).

**추가 참조**

[단계 요약](converting-pdf-postscript-image-files.md#summary-of-steps)

[빠른 시작(SOAP 모드): Java API를 사용하여 PDF 문서를 PostScript로 변환](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 PDF 문서를 PS로 변환 {#convert-a-pdf-document-to-ps-using-the-web-service-api}

PDF 서비스 API(웹 서비스) 변환을 사용하여 PDF 문서를 PostScript로 변환합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용하는지 확인합니다. `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` AEM Forms을 호스팅하는 서버의 IP 주소입니다.

1. 변환 PDF 클라이언트를 만듭니다.

   * 만들기 `ConvertPdfServiceClient` 기본 생성자를 사용하여 개체를 작성합니다.
   * 만들기 `ConvertPdfServiceClient.Endpoint.Address` 을 사용하여 개체 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`.) 를 사용할 필요가 없습니다. `lc_version` 특성. 단, 을 지정합니다. `?blob=mtom`.
   * 만들기 `System.ServiceModel.BasicHttpBinding` 의 값을 가져와서 개체 `ConvertPdfServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스트 `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름 할당 `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * 해당 암호 값을 필드에 할당합니다. `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 지정 `HttpClientCredentialType.Basic` 필드에 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 상수 값 지정 `BasicHttpSecurityMode.TransportCredentialOnly` 필드에 `BasicHttpBindingSecurity.Security.Mode`.

1. PDF 문서를 참조하여 PostScript 파일로 변환합니다.

   * 만들기 `BLOB` 개체를 만들 때 사용됩니다. 다음 `BLOB` 객체는 PostScript 파일로 변환된 PDF 문서를 저장하는 데 사용됩니다.
   * 만들기 `System.IO.FileStream` 변환할 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 콘텐츠를 저장하는 바이트 배열 만들기 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채우기 `System.IO.FileStream` 개체 `Read` 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달하는 메서드입니다.
   * 채우기 `BLOB` 개체 할당 `MTOM` 바이트 배열의 내용이 있는 필드입니다.

1. 전환 런타임 옵션을 설정합니다.

   * 만들기 `ToPSOptionsSpec` 해당 생성자를 호출하여 개체를 작성합니다.
   * 에 값을 할당하여 런타임 옵션 설정 `ToPSOptionsSpec` 개체의 데이터 멤버입니다. 예를 들어 생성되는 PostScript 수준을 정의하려면 `PSLevel` 열거형 값 `ToPSOptionsSpec` 개체 `psLevel` 데이터 구성원입니다.

1. PDF 문서를 PostScript 파일로 변환합니다.

   호출 `GeneratePDFServiceService` 개체 `toPS2` 메서드를 실행하고 다음 값을 전달합니다.

   * A `BLOB` PostScript 파일로 변환할 PDF 문서를 나타내는 개체
   * A `ToPSOptionsSpec` 런타임 옵션을 지정하는 개체입니다

   전환이 완료되면 다음에 액세스하여 PostScript 문서를 나타내는 이진 데이터를 추출합니다 `BLOB` 개체 `MTOM` 속성. PostScript 파일에 쓸 수 있는 바이트 배열이 반환됩니다.

1. PostScript 파일을 저장합니다.

   * 만들기 `System.IO.FileStream` 해당 생성자를 호출하여 개체를 작성합니다. PS 파일의 파일 위치를 나타내는 문자열 값을 전달합니다.
   * 의 데이터 콘텐츠를 저장하는 바이트 배열 만들기 `BLOB` 에서 반환한 개체 `encryptPDFUsingPassword` 메서드를 사용합니다. 의 값을 가져와서 바이트 배열 채우기 `BLOB` 개체 `MTOM` 필드.
   * 만들기 `System.IO.BinaryWriter` 개체를 호출하고 `System.IO.FileStream` 개체.
   * 를 호출하여 바이트 배열의 내용을 PostScript 파일에 씁니다 `System.IO.BinaryWriter` 개체 `Write` 메서드 및 바이트 배열 전달.

**추가 참조**

[단계 요약](converting-pdf-postscript-image-files.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## PDF 문서를 이미지 형식으로 변환 {#converting-pdf-documents-to-image-formats}

PDF 변환 서비스를 사용하여 PDF 문서를 프로그래밍 방식으로 JPEG, JPEG 2000, TIFF 및 PNG를 포함하는 이미지 형식으로 변환할 수 있습니다. PDF 문서를 이미지 파일로 변환하면 PDF 문서를 이미지 파일로 사용할 수 있습니다. 예를 들어, 이미지를 스토리지를 위한 엔터프라이즈 컨텐츠 관리 시스템에 배치할 수 있습니다.

PDF 문서를 이미지로 변환할 때 PDF 변환 서비스는 문서의 각 페이지에 대해 별도의 이미지를 만듭니다. 즉, 문서에 20페이지가 있으면 PDF 변환 서비스에서 20개의 이미지 파일을 만듭니다. PDF 문서를 이미지 형식으로 변환할 때 PDF 문서 내의 각 페이지에 대해 개별 이미지를 만들거나 전체 PDF 문서에 대해 단일 이미지 파일을 만들 수 있습니다.

>[!NOTE]
>
>PDF 변환 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

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

PDF 서비스 변환 작업을 프로그래밍 방식으로 수행하려면 먼저 PDF 서비스 변환 클라이언트를 만들어야 합니다. Java API를 사용하는 경우 `ConvertPdfServiceClient` 개체. 웹 서비스 API를 사용하는 경우 `ConvertPDFServiceService` 개체.

**변환할 PDF 문서 검색**

PDF 문서를 검색하여 이미지로 변환합니다. 대화형 PDF 문서를 이미지로 변환할 수 없습니다. 그렇게 하려고 하면 예외가 발생합니다. 대화형 PDF 문서를 이미지 파일로 변환하려면 변환하기 전에 PDF 문서를 병합해야 합니다. (참조: [PDF 문서 병합](/help/forms/developing/creating-document-output-streams.md#flattening-pdf-documents).)

**런타임 옵션 설정**

이미지 형식 및 해상도 값과 같은 런타임 옵션을 설정합니다. 런타임 값에 대한 자세한 내용은 `ToImageOptionsSpec` 의 클래스 참조 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**PDF을 이미지로 변환**

서비스 클라이언트를 만들고 런타임 옵션을 설정한 후 PDF 문서를 이미지로 변환할 수 있습니다. 이미지가 포함된 컬렉션 개체가 반환됩니다.

**컬렉션에서 이미지 파일 검색**

PDF 변환 서비스가 반환하는 컬렉션 개체에서 이미지 파일을 검색할 수 있습니다. 컬렉션의 각 요소는 `com.adobe.idp.Document` 인스턴스(또는 a `BLOB` 인스턴스: 웹 서비스를 사용하는 경우) JPG 파일과 같은 이미지 파일로 저장할 수 있습니다.

이미지 파일의 형식은 다음에 따라 다릅니다. `ImageConvertFormat` 런타임 옵션입니다. 즉, `ImageConvertFormat` 런타임 옵션 대상 `ImageConvertFormat.JPEG`, 이미지 파일을 JPG 파일로 저장할 수 있습니다.

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF 서비스 API 빠른 시작 전환](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Java API를 사용하여 PDF 문서를 이미지 파일로 변환 {#convert-a-pdf-document-to-image-files-using-the-java-api}

Java(PDF 서비스 API 변환)를 사용하여 PDF 문서를 이미지 형식으로 변환합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-convertpdf-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. 변환 PDF 클라이언트를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.
   * 만들기 `ConvertPdfServiceClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체.

1. 변환할 PDF 문서를 검색합니다.

   * 만들기 `java.io.FileInputStream` 생성자를 사용하고 PDF 문서의 위치를 지정하는 문자열 값을 전달하여 변환할 PDF 문서를 나타내는 개체입니다.
   * 만들기 `com.adobe.idp.Document` 개체를 생성자를 사용하고 `java.io.FileInputStream` 개체.

1. 런타임 옵션을 설정합니다.

   * 만들기 `ToImageOptionsSpec` 개체를 만들 때 사용됩니다.
   * 필요에 따라 이 개체에 속하는 메서드를 호출합니다. 예를 들어, `setImageConvertFormat` 방법 및 전달 `ImageConvertFormat` 형식 유형을 지정하는 열거형 값입니다.

   >[!NOTE]
   >
   >설정 `ImageConvertFormat` 열거형 값은 필수입니다.

1. PDF을 이미지로 변환합니다.

   호출 `ConvertPdfServiceClient` 개체 `toImage2` 메서드를 실행하고 다음 값을 전달합니다.

   * A `com.adobe.idp.Document` 변환할 PDF 파일을 나타내는 개체입니다.
   * A `com.adobe.livecycle.converpdfservice.client.ToImageOptionsSpec` 대상 이미지 형식에 대한 다양한 환경 설정이 포함된 개체입니다.

   다음 `toImage2` 메서드가 을 반환합니다. `java.util.List` 이미지가 포함된 객체입니다. 컬렉션의 각 요소는 `com.adobe.idp.Document` 인스턴스.

1. 컬렉션에서 이미지 파일을 검색합니다.

   다음을 반복합니다. `java.util.List` 이미지 존재 여부를 확인하는 개체입니다. 각 요소는 `com.adobe.idp.Document` 인스턴스. 를 호출하여 이미지를 저장합니다. `com.adobe.idp.Document` 개체 `copyToFile` 방법 및 전달 `java.io.File` 개체.

**추가 참조**

[빠른 시작(SOAP 모드): Java API를 사용하여 PDF 문서를 JPEG 파일로 변환](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api)

### 웹 서비스 API를 사용하여 PDF 문서를 이미지 파일로 변환 {#convert-a-pdf-document-to-image-files-using-the-web-service-api}

PDF 서비스 API(웹 서비스) 변환을 사용하여 PDF 문서를 이미지 형식으로 변환합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용하는지 확인합니다. `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` AEM Forms을 호스팅하는 서버의 IP 주소입니다.

1. 변환 PDF 클라이언트를 만듭니다.

   * 만들기 `ConvertPdfServiceClient` 기본 생성자를 사용하여 개체를 작성합니다.
   * 만들기 `ConvertPdfServiceClient.Endpoint.Address` 을 사용하여 개체 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`.) 를 사용할 필요가 없습니다. `lc_version` 특성. 단, 을 지정합니다. `?blob=mtom`.
   * 만들기 `System.ServiceModel.BasicHttpBinding` 의 값을 가져와서 개체 `ConvertPdfServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스트 `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름 할당 `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * 해당 암호 값을 필드에 할당합니다. `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 지정 `HttpClientCredentialType.Basic` 필드에 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 상수 값 지정 `BasicHttpSecurityMode.TransportCredentialOnly` 필드에 `BasicHttpBindingSecurity.Security.Mode`.

1. 변환할 PDF 문서를 검색합니다.

   * 만들기 `BLOB` 개체를 만들 때 사용됩니다. 이 `BLOB` 개체를 사용하여 PDF 양식을 저장합니다.
   * 만들기 `System.IO.FileStream` 해당 생성자를 호출하여 개체를 작성합니다. PDF 폼의 위치와 파일을 열 모드를 지정하는 문자열 값을 전달합니다.
   * 의 콘텐츠를 저장하는 바이트 배열 만들기 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정합니다. `System.IO.FileStream` 개체 `Length` 속성.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채우기 `System.IO.FileStream` 개체 `Read` 메서드를 사용합니다. 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 채우기 `BLOB` 개체 할당 `MTOM` 바이트 배열의 내용이 있는 필드입니다.

1. 런타임 옵션을 설정합니다.

   * 만들기 `ToImageOptionsSpec` 개체를 만들 때 사용됩니다.
   * 필요에 따라 이 개체에 속하는 메서드를 호출합니다. 예를 들어, `setImageConvertFormat` 방법 및 전달 `ImageConvertFormat` 형식 유형을 지정하는 열거형 값입니다.

   >[!NOTE]
   >
   >설정 `ImageConvertFormat` 열거형 값은 필수입니다.

1. PDF을 이미지로 변환합니다.

   호출 `ConvertPDFServiceService` 개체 `toImage2` 메서드를 실행하고 다음 값을 전달합니다.

   * A `BLOB` 변환할 파일을 나타내는 개체
   * A `ToImageOptionsSpec` 대상 이미지 형식에 대한 다양한 환경 설정이 포함된 개체

   다음 `toImage2` 메서드가 을 반환합니다. `MyArrayOfBLOB` 새로 만든 이미지 파일이 포함된 객체입니다.

1. 컬렉션에서 이미지 파일을 검색합니다.

   * 에서 요소의 수를 결정합니다. `MyArrayOfBLOB` 의 값을 가져와서 개체 `Count` 필드. 각 요소는 `BLOB` 이미지가 포함된 객체입니다.
   * 다음을 반복합니다. `MyArrayOfBLOB` 개체를 만들고 각 이미지 파일을 저장합니다.

**추가 참조**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
