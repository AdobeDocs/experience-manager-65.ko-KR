---
title: PDF/A 문서 작업
description: DocConverter 서비스를 사용하여 PDF 문서가 PDF/A 문서인지 확인하고 PDF 문서를 PDF/A 문서로 변환합니다.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 966c3554-25df-4467-866e-11c43cc15b58
solution: Experience Manager, Experience Manager Forms
source-git-commit: 872e2de411f51b5f0b26a2ff47cb49f01313d39f
workflow-type: tm+mt
source-wordcount: '2331'
ht-degree: 1%

---

# PDF/A 문서 작업 {#working-with-pdf-a-documents}

**DocConverter 서비스 정보**

DocConverter 서비스는 PDF 문서를 PDA/A 문서로 변환할 수 있습니다. 이 서비스를 사용하여 다음 작업을 수행할 수 있습니다.

* PDF 문서를 PDF/A 문서로 변환합니다. (참조: [문서를 PDF/A 문서로 변환](pdf-a-documents.md#converting-documents-to-pdf-a-documents).)
* PDF 문서가 PDF/A 문서인지 확인합니다. (참조: [프로그래밍 방식으로 PDF/A 준수 여부 확인](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy).)

>[!NOTE]
>
>DocConverter 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

## 문서를 PDF/A 문서로 변환 {#converting-documents-to-pdf-a-documents}

DocConverter 서비스를 사용하여 PDF 문서를 PDF/A 문서로 변환할 수 있습니다. PDF/A는 문서 내용을 장기간 보존하기 위한 보관 형식이므로 모든 글꼴이 임베드되고 파일이 압축 해제됩니다. 따라서 PDF/A 문서는 일반적으로 표준 PDF 문서보다 큽니다. 또한 PDF/A 문서에는 오디오 및 비디오 컨텐츠가 포함되어 있지 않습니다. PDF 문서를 PDF/A 문서로 변환하려면 먼저 PDF 문서가 PDF/A 문서가 아닌지 확인합니다.

PDF/A-1 사양은 두 가지 적합성 수준, 즉 A와 B로 구성됩니다. 두 요소의 주요 차이점은 적합성 수준 B에 필요하지 않은 논리적 구조(접근성) 지원에 대한 것입니다. 적합성 수준에 관계없이 PDF/A-1은 모든 글꼴이 생성된 PDF/A 문서 내에 임베드되어 있음을 나타냅니다. 현재 유효성 검사(및 전환)에서는 PDF/A-1b만 지원됩니다.

PDF/A는 PDF 문서를 보관하는 표준이지만 표준 PDF 문서가 회사의 요구 사항을 충족하는 경우 PDF/A를 보관에 사용해야 하는 것은 아닙니다. PDF/A 표준의 목적은 장기적인 보관 및 문서 보존 요구 사항을 위한 PDF 파일을 설정하는 것입니다.

>[!NOTE]
>
>DocConverter 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary-of-steps}

PDF 문서를 PDF/A 문서로 변환하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. DocConvert 클라이언트 만들기
1. PDF 문서를 참조하여 PDF/A 문서로 변환합니다.
1. 추적 정보를 설정합니다.
1. 문서를 변환합니다.
1. PDF/A 문서를 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss 애플리케이션 서버에 배포된 경우 필요)
* jbossall-client.jar(AEM Forms이 JBoss 애플리케이션 서버에 배포된 경우 필수)

이러한 JAR 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**DocConvert 클라이언트 만들기**

DocConverter 작업을 프로그래밍 방식으로 수행하려면 먼저 DocConverter 클라이언트를 만들어야 합니다. Java API를 사용하는 경우 `DocConverterServiceClient` 개체. DocConverter 웹 서비스 API를 사용하는 경우 `DocConverterServiceService` 개체.

**PDF 문서를 참조하여 PDF/A 문서로 변환**

PDF 문서를 검색하여 PDF/A 문서로 변환합니다. Acrobat 양식과 같은 PDF 문서를 PDF/A 문서로 변환하려고 하면 예외가 발생합니다.

**추적 정보 설정**

변환 프로세스 중에 추적되는 정보의 양을 결정하는 런타임 옵션을 설정할 수 있습니다. 즉, PDF 문서를 PDF/A 문서로 변환할 때 DocConverter 서비스가 추적하는 정보의 양을 지정하는 9개의 서로 다른 수준을 설정할 수 있습니다.

**문서 변환**

DocConverter 서비스 클라이언트를 만든 후 변환할 PDF 문서를 참조하고 추적되는 정보의 양을 지정하는 런타임 옵션을 설정하면 PDF 문서를 PDF/A 문서로 변환할 수 있습니다.

**PDF/A 문서 저장**

PDF/A 문서를 PDF 파일로 저장할 수 있습니다.

**추가 참조**

[Java API를 사용하여 문서를 PDF/A 문서로 변환](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-java-api)

[웹 서비스 API를 사용하여 문서를 PDF/A 문서로 변환](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[프로그래밍 방식으로 PDF/A 준수 여부 확인](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)

### Java API를 사용하여 문서를 PDF/A 문서로 변환 {#convert-documents-to-pdf-a-documents-using-the-java-api}

Java API를 사용하여 PDF 문서를 PDF/A 문서로 변환합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-docconverter-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. DocConvert 클라이언트 만들기

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.
   * 만들기 `DocConverterServiceClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체.

1. PDF 문서를 참조하여 PDF/A 문서로 변환

   * 만들기 `java.io.FileInputStream` 생성자를 사용하고 PDF 파일의 위치를 지정하는 문자열 값을 전달하여 변환할 PDF 문서를 나타내는 개체입니다.
   * 만들기 `com.adobe.idp.Document` 개체를 생성자를 사용하고 `java.io.FileInputStream` 개체.

1. 추적 정보 설정

   * 만들기 `PDFAConversionOptionSpec` 개체를 만들 때 사용됩니다.
   * 를 호출하여 정보 추적 수준 설정 `PDFAConversionOptionSpec` 개체 `setLogLevel` 메서드 및 추적 수준을 지정하는 문자열 값 전달 예를 들어 값을 전달합니다 `FINE`. 다른 값에 대한 자세한 내용은 `setLogLevel` 의 메서드 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. 문서 변환

   를 호출하여 PDF 문서를 PDF/A 문서로 변환 `DocConverterServiceClient` 개체 `toPDFA` 메서드 및 다음 값 전달:

   * 다음 `com.adobe.idp.Document` 변환할 PDF 문서가 포함된 개체
   * 다음 `PDFAConversionOptionSpec` 추적 정보를 지정하는 개체

   다음 `toPDFA` 메서드가 을 반환합니다. `PDFAConversionResult` PDF/A 문서가 포함된 객체입니다.

1. PDF/A 문서 저장

   * 다음을 호출하여 PDF/A 문서 검색 `PDFAConversionResult` 개체 `getPDFA` 메서드를 사용합니다. 이 메서드는 `com.adobe.idp.Document` PDF/A 문서를 나타내는 개체입니다.
   * 만들기 `java.io.File` PDF/A 파일을 나타내는 개체입니다. 파일 이름 확장명이 .pdf인지 확인합니다.
   * 를 호출하여 PDF/A 데이터로 파일 채우기 `com.adobe.idp.Document` 개체 `copyToFile` 메서드 및 전달 `java.io.File` 개체.

**추가 참조**

[PDF/A 문서 작업](pdf-a-documents.md#working-with-pdf-a-documents)

[빠른 시작(SOAP 모드): Java API를 사용하여 문서를 PDF/A 문서로 변환](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-converting-a-document-to-a-pdf-a-document-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 문서를 PDF/A 문서로 변환 {#convert-documents-to-pdf-a-documents-using-the-web-service-api}

DocConverter API(웹 서비스)를 사용하여 PDF 문서를 PDF/A 문서로 변환합니다.

1. 프로젝트 파일 포함

   * DocConverter WSDL을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다.
   * Microsoft .NET 클라이언트 어셈블리를 참조합니다.

1. DocConvert 클라이언트 만들기

   * Microsoft .NET 클라이언트 어셈블리를 사용하여 `DocConverterServiceService` 기본 생성자를 호출하여 개체를 작성합니다.
   * 설정 `DocConverterServiceService` 개체 `Credentials` 이(가) 있는 데이터 멤버 `System.Net.NetworkCredential` 사용자 이름과 암호 값을 지정하는 값입니다.

1. PDF 문서를 참조하여 PDF/A 문서로 변환

   * 만들기 `BLOB` 개체를 만들 때 사용됩니다. 다음 `BLOB` 객체는 PDF/A 문서로 변환된 PDF 문서를 저장하는 데 사용됩니다.
   * 만들기 `System.IO.FileStream` PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 콘텐츠를 저장하는 바이트 배열 만들기 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채우기 `System.IO.FileStream` 개체 `Read` 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하는 방법.
   * 채우기 `BLOB` 개체 할당 `binaryData` 속성을 바이트 배열의 콘텐츠와 함께 사용합니다.

1. 추적 정보 설정

   * 만들기 `PDFAConversionOptionSpec` 개체를 만들 때 사용됩니다.
   * 추적 수준을 지정하는 값을 로 할당하여 정보 추적 수준을 설정합니다. `PDFAConversionOptionSpec` 개체 `logLevel` 데이터 구성원입니다. 예를 들어 값을 할당합니다 `FINE` 이 데이터 구성원에 연결합니다.

1. 문서 변환

   를 호출하여 PDF 문서를 PDF/A 문서로 변환 `DocConverterServiceService` 개체 `toPDFA` 메서드 및 다음 값 전달:

   * 다음 `BLOB` 변환할 PDF 문서가 포함된 개체
   * 다음 `PDFAConversionOptionSpec` 추적 정보를 지정하는 개체

   다음 `toPDFA` 메서드가 을 반환합니다. `PDFAConversionResult` PDF/A 문서가 포함된 객체입니다.

1. PDF/A 문서 저장

   * 만들기 `BLOB` 값을 가져와서 PDF/A 문서를 저장하는 객체 `PDFAConversionResult` 개체 `PDFADocument` 데이터 구성원입니다.
   * 의 콘텐츠를 저장하는 바이트 배열 만들기 `BLOB` 를 사용하여 반환된 개체 `PDFAConversionResult` 개체. 의 값을 가져와서 바이트 배열 채우기 `BLOB` 개체 `binaryData` 데이터 구성원입니다.
   * 만들기 `System.IO.FileStream` 객체를 생성합니다. 생성자를 호출하고 PDF/A 문서의 파일 위치를 나타내는 문자열 값을 전달합니다.
   * 만들기 `System.IO.BinaryWriter` 개체를 호출하고 `System.IO.FileStream` 개체.
   * 를 호출하여 바이트 배열의 내용을 PDF 파일에 씁니다 `System.IO.BinaryWriter` 개체 `Write` 메서드 및 바이트 배열 전달.

**추가 참조**

[PDF/A 문서 작업](pdf-a-documents.md#working-with-pdf-a-documents)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64 인코딩을 사용하는 .NET 클라이언트 어셈블리 만들기](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 프로그래밍 방식으로 PDF/A 준수 여부 확인 {#programmatically-determining-pdf-a-compliancy}

DocConverter 서비스를 사용하여 PDF 문서가 PDF/A를 준수하는지 여부를 확인할 수 있습니다. PDF/A 문서 및 PDF 문서를 PDF/A 문서로 변환하는 방법에 대한 자세한 내용은 [문서를 PDF/A 문서로 변환](pdf-a-documents.md#converting-documents-to-pdf-a-documents).

>[!NOTE]
>
>DocConverter 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-1}

PDF/A 준수 여부를 확인하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. DocConvert 클라이언트 만들기
1. PDF/A 준수 여부를 확인하는 데 사용되는 PDF 문서를 참조하십시오.
1. 런타임 옵션을 설정합니다.
1. PDF 문서에 대한 정보를 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss 애플리케이션 서버에 배포된 경우 필요)
* jbossall-client.jar(AEM Forms이 JBoss 애플리케이션 서버에 배포된 경우 필수)

이러한 JAR 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**DocConvert 클라이언트 만들기**

DocConverter 작업을 프로그래밍 방식으로 수행하려면 먼저 DocConverter 클라이언트를 만들어야 합니다. Java API를 사용하는 경우 `DocConverterServiceClient` 개체. DocConverter 웹 서비스 API를 사용하는 경우 `DocConverterServiceService` 개체.

**PDF/A 준수 여부를 확인하는 데 사용되는 PDF 문서 참조**

PDF 문서가 PDF/A와 호환되는지 여부를 확인하려면 PDF 문서를 참조하고 DocConverter 서비스에 전달해야 합니다.

**런타임 옵션 설정**

변환 프로세스 중에 추적되는 정보의 양을 결정하는 런타임 옵션을 설정할 수 있습니다. 즉, PDF 문서를 PDF/A 문서로 변환할 때 DocConverter 서비스가 추적하는 정보의 양을 지정하는 9개의 다른 수준을 설정할 수 있습니다.

**PDF 문서에 대한 정보 가져오기**

DocConverter 서비스 클라이언트를 만들고 PDF 문서를 참조하며 런타임 옵션을 설정한 후 PDF 문서가 PDF/A 규격 문서인지 여부를 결정할 수 있습니다.

**추가 참조**

[Java API를 사용하여 PDF/A 준수 여부 확인](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-java-api)

[웹 서비스 API를 사용하여 PDF/A 준수 여부 확인](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API를 사용하여 PDF/A 준수 여부 확인 {#determine-pdf-a-compliancy-using-the-java-api}

Java API를 사용하여 PDF/A 준수 여부 확인:

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-docconverter-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. DocConvert 클라이언트 만들기

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.
   * 만들기 `DocConverterServiceClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체.

1. PDF/A 준수 여부를 확인하는 데 사용되는 PDF 문서 참조

   * 만들기 `java.io.FileInputStream` 생성자를 사용하고 PDF 파일의 위치를 지정하는 문자열 값을 전달하여 변환할 PDF 문서를 나타내는 개체입니다.
   * 만들기 `com.adobe.idp.Document` 개체를 생성자를 사용하고 `java.io.FileInputStream` 개체.

1. 런타임 옵션 설정

   * 만들기 `PDFAValidationOptionSpec` 개체를 만들 때 사용됩니다.
   * 다음을 호출하여 규정 준수 수준 설정 `PDFAValidationOptionSpec` 개체 `setCompliance` 방법 및 전달 `PDFAValidationOptionSpec.Compliance.PDFA_1B`.
   * 를 호출하여 정보 추적 수준 설정 `PDFAValidationOptionSpec` 개체 `setLogLevel` 메서드 및 추적 수준을 지정하는 문자열 값 전달 예를 들어 값을 전달합니다 `FINE`. 다른 값에 대한 자세한 내용은 `setLogLevel` 의 메서드 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. PDF 문서에 대한 정보 가져오기

   다음을 호출하여 PDF/A 준수 여부 확인 `DocConverterServiceClient` 개체 `isPDFA` 메서드 및 다음 값 전달:

   * 다음 `com.adobe.idp.Document` PDF 문서가 포함된 객체입니다.
   * 다음 `PDFAValidationOptionSpec` 런타임 옵션을 지정하는 개체입니다.

   다음 `isPDFA` 메서드가 을 반환합니다. `PDFAValidationResult` 이 작업의 결과를 포함하는 개체입니다.

**추가 참조**

[PDF/A 문서 작업](pdf-a-documents.md#working-with-pdf-a-documents)

[빠른 시작(SOAP 모드): Java API를 사용하여 PDF/A 준수 여부 확인](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-determining-pdf-a-compliancy-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 PDF/A 준수 여부 확인 {#determine-pdf-a-compliancy-using-the-web-service-api}

웹 서비스 API를 사용하여 PDF/A 준수 여부를 확인합니다.

1. 프로젝트 파일 포함

   * DocConverter WSDL을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다.
   * Microsoft .NET 클라이언트 어셈블리를 참조합니다.

1. DocConvert 클라이언트 만들기

   * Microsoft .NET 클라이언트 어셈블리를 사용하여 `DocConverterServiceService` 기본 생성자를 호출하여 개체를 작성합니다.
   * 설정 `DocConverterServiceService` 개체 `Credentials` 이(가) 있는 데이터 멤버 `System.Net.NetworkCredential` 사용자 이름과 암호 값을 지정하는 값입니다.

1. PDF/A 준수 여부를 확인하는 데 사용되는 PDF 문서 참조

   * 만들기 `BLOB` 개체를 만들 때 사용됩니다. 다음 `BLOB` 객체는 PDF/A 문서로 변환된 PDF 문서를 저장하는 데 사용됩니다.
   * 만들기 `System.IO.FileStream` PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 콘텐츠를 저장하는 바이트 배열 만들기 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채우기 `System.IO.FileStream` 개체 `Read` 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하는 방법.
   * 채우기 `BLOB` 개체 할당 `binaryData` 속성을 바이트 배열의 콘텐츠와 함께 사용합니다.

1. 런타임 옵션 설정

   * 만들기 `PDFAValidationOptionSpec` 개체를 만들 때 사용됩니다.
   * 다음을 할당하여 준수 수준 설정 `PDFAValidationOptionSpec` 개체 `compliance` 값이 있는 데이터 멤버 `PDFAConversionOptionSpec_Compliance.PDFA_1B`.
   * 다음을 할당하여 정보 추적 수준 설정 `PDFAValidationOptionSpec` 개체 `resultLevel` 값이 있는 데이터 멤버 `PDFAValidationOptionSpec_ResultLevel.DETAILED`.

1. PDF 문서에 대한 정보 가져오기

   다음을 호출하여 PDF/A 준수 여부 확인 `DocConverterServiceService` 개체 `isPDFA` 메서드 및 다음 값 전달:

   * 다음 `BLOB` PDF 문서가 포함된 객체입니다.
   * 다음 `PDFAValidationOptionSpec` 런타임 옵션이 포함된 객체입니다.

   다음 `isPDFA` 메서드가 을 반환합니다. `PDFAValidationResult` 이 작업의 결과를 포함하는 개체입니다.

**추가 참조**

[PDF/A 문서 작업](pdf-a-documents.md#working-with-pdf-a-documents)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64 인코딩을 사용하는 .NET 클라이언트 어셈블리 만들기](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
