---
title: PDF 유틸리티 작업
seo-title: PDF 유틸리티 작업
description: PDF 유틸리티 서비스를 사용하여 PDF와 XDP 파일 포맷 간을 변환하거나 PDF 문서 속성을 설정 및 검색하고 XMP 메타데이터를 조작할 수 있습니다.
seo-description: PDF 유틸리티 서비스를 사용하여 PDF와 XDP 파일 포맷 간을 변환하거나 PDF 문서 속성을 설정 및 검색하고 XMP 메타데이터를 조작할 수 있습니다.
uuid: a2ea2359-c547-4f1b-b6ca-f276f816e36a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d816bf2e-5236-4084-b7c4-c32b72cdff97
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2607'
ht-degree: 1%

---


# PDF 유틸리티 작업 {#working-with-pdf-utilities}

**이 문서의 샘플과 예는 JEE 환경의 AEM Forms에만 해당됩니다.**

**PDF 유틸리티 서비스 정보**

PDF 유틸리티 서비스는 PDF와 XDP 파일 포맷 간을 변환하거나 PDF 문서 속성을 설정 및 검색하고 XMP 메타데이터를 조작할 수 있습니다. 예를 들어 PDF 문서를 다른 형식으로 변환하기 전에 해당 속성을 검사하여 변환에 대해 호출할 서비스 작업을 결정하는 것이 유용합니다.

PDF 유틸리티 서비스를 사용하여 다음 작업을 수행할 수 있습니다.

* PDF 문서를 XDP 문서로 변환
* XDP 문서를 PDF 문서로 변환 ([XDP 문서를 PDF 문서로 변환](pdf-utilities.md#converting-xdp-documents-into-pdf-documents) 참조)
* PDF 문서 속성 검색 ([PDF 문서 속성 검색](pdf-utilities.md#retrieving-pdf-document-properties)을 참조하십시오.)
* PDF 문서를 저장하고 웹을 빠르게 볼 수 있도록 최적화합니다. ([PDF 문서 저장 모드 설정](pdf-utilities.md#setting-pdf-document-save-modes)을 참조하십시오.)

>[!NOTE]
>
>PDF 유틸리티 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

## PDF 문서를 XDP 문서로 변환 {#converting-pdf-documents-into-xdp-documents}

PDF 유틸리티 Java 및 웹 서비스 API를 사용하여 PDF 문서를 프로그래밍 방식으로 XDP 문서로 변환할 수 있습니다.

>[!NOTE]
>
>PDF 유틸리티 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### {#summary-of-steps} 단계 요약

PDF 문서를 XDP 문서로 변환하려면 다음 단계를 수행합니다.

1. 프로젝트 파일 포함
1. PDFUftyService 클라이언트를 만듭니다.
1. PDF를 XDP로 변환 작업을 호출합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**PDFUftyService 클라이언트 만들기**

PDF 유틸리티 작업을 프로그래밍 방식으로 수행하려면 먼저 PDFUftyService 클라이언트를 만들어야 합니다. Java API를 사용하면 `PDFUtilityServiceClient` 개체를 만들어 이 작업을 수행할 수 있습니다. 웹 서비스 API를 사용하면 `PDFUtilityServiceService` 개체를 사용하여 이 작업을 수행할 수 있습니다.

**PDF를 XDP로 변환 작업 호출**

서비스 클라이언트를 만든 후 PDF를 XDP로 변환 작업을 호출할 수 있습니다.

**참고 항목**

[Java API를 사용하여 PDF 문서를 XDP 문서로 변환](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[웹 서비스 API를 사용하여 PDF 문서를 XDP 문서로 변환](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API {#convert-pdf-documents-into-xdp-documents-using-the-java-api}를 사용하여 PDF 문서를 XDP 문서로 변환

PDF 유틸리티 API를 사용하여 PDF 문서를 XDP 문서로 변환(Java):

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-pdfility-client.jar 등의 클라이언트 JAR 파일을 포함합니다.

1. PDFUftyService 클라이언트 만들기

   해당 생성자를 사용하고 연결 속성이 포함된 `ServiceClientFactory` 객체를 전달하여 `PDFUtilityServiceClient` 객체를 만듭니다.

1. PDF를 XDP로 변환 작업 호출

   변환을 수행하려면 `PDFUtilityServiceClient` 객체의 `convertPDFtoXDP` 메서드를 호출하고 PDF 파일을 나타내는 `com.adobe.idp.Document` 객체를 전달합니다. 이 메서드는 새로 만든 XDP 파일을 나타내는 `com.adobe.idp.Document` 객체를 반환합니다.

**참고 항목**

[PDF 문서를 XDP 문서로 변환](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API {#convert-pdf-documents-into-xdp-documents-using-the-web-service-api}를 사용하여 PDF 문서를 XDP 문서로 변환

PDF 유틸리티 API(웹 서비스)를 사용하여 PDF 문서를 XDP 문서로 변환:

1. 프로젝트 파일 포함

   * PDF 유틸리티 서비스 WSDL 파일을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다.
   * Microsoft .NET 클라이언트 어셈블리를 참조하십시오.

1. PDFUftyService 클라이언트 만들기

   프록시 클래스 생성자를 사용하여 `PDFUtilityServiceService` 개체를 만듭니다.

1. PDF를 XDP로 변환 작업 호출

   `PDFUtilityServiceService` 개체의 `convertPDFtoXDP` 메서드를 호출하고 PDF 파일을 나타내는 `BLOB` 개체를 전달합니다. 이 메서드는 새로 만든 XDP 파일을 나타내는 `BLOB` 객체를 반환합니다.

**참고 항목**

[PDF 문서를 XDP 문서로 변환](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64 인코딩을 사용하는 .NET 클라이언트 어셈블리 만들기](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## XDP 문서를 PDF 문서로 변환 {#converting-xdp-documents-into-pdf-documents}

PDF 유틸리티 Java 및 웹 서비스 API를 사용하여 XDP 문서를 프로그래밍 방식으로 PDF 문서로 변환할 수 있습니다.

>[!NOTE]
>
>PDF 유틸리티 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### {#summary_of_steps-1} 단계 요약

XDP 문서를 PDF 문서로 변환하려면 다음 단계를 수행합니다.

1. 프로젝트 파일 포함
1. PDFUftyService 클라이언트를 만듭니다.
1. XDP를 PDF로 변환 작업을 호출합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**PDFUftyService 클라이언트 만들기**

PDF 유틸리티 작업을 프로그래밍 방식으로 수행하려면 먼저 PDFUftyService 클라이언트를 만들어야 합니다. Java API를 사용하면 `PDFUtilityServiceClient` 개체를 만들어 이 작업을 수행할 수 있습니다. 웹 서비스 API를 사용하면 `PDFUtilityServiceService` 개체를 사용하여 이 작업을 수행할 수 있습니다.

**XDP를 PDF로 변환 작업 호출**

서비스 클라이언트를 만든 후 XDP를 PDF로 변환 작업을 호출할 수 있습니다.

**참고 항목**

[Java API를 사용하여 XDP 문서를 PDF 문서로 변환](pdf-utilities.md#convert-xdp-documents-into-pdf-documents-using-the-java-api)

[웹 서비스 API를 사용하여 XDP 문서를 PDF 문서로 변환](pdf-utilities.md#converting-xdp-documents-into-pdf-documents-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API {#convert-xdp-documents-into-pdf-documents-using-the-java-api}를 사용하여 XDP 문서를 PDF 문서로 변환

PDF 유틸리티 API(Java)를 사용하여 XDP 문서를 PDF 문서로 변환:

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-pdfility-client.jar 등의 클라이언트 JAR 파일을 포함합니다.

1. PDFUftyService 클라이언트 만들기

   해당 생성자를 사용하고 연결 속성이 포함된 `ServiceClientFactory` 객체를 전달하여 `PDFUtilityServiceClient` 객체를 만듭니다.

1. XDP를 PDF로 변환 작업 호출

   변환을 수행하려면 `PDFUtilityServiceClient` 객체의 `convertXDPtoPDF` 메서드를 호출하고 XDP 파일을 나타내는 `com.adobe.idp.Document` 객체를 전달합니다. 이 메서드는 새로 만든 PDF 파일을 나타내는 `com.adobe.idp.Document` 객체를 반환합니다.

**참고 항목**

[XDP 문서를 PDF 문서로 변환](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API {#converting-xdp-documents-into-pdf-documents-using-the-web-service-api}를 사용하여 XDP 문서를 PDF 문서로 변환

PDF 유틸리티 API(웹 서비스 API)를 사용하여 XDP 문서를 PDF 문서로 변환:

1. 프로젝트 파일 포함

   * PDF 유틸리티 서비스 WSDL 파일을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다.
   * Microsoft .NET 클라이언트 어셈블리를 참조하십시오.

1. PDFUftyService 클라이언트 만들기

   프록시 클래스 생성자를 사용하여 `PDFUtilityServiceService` 개체를 만듭니다.

1. XDP를 PDF로 변환 작업 호출

   변환을 수행하려면 `PDFUtilityServiceService` 객체의 `convertXDPtoPDF` 메서드를 호출하고 XDP 파일을 나타내는 `BLOB` 객체를 전달합니다. 이 메서드는 새로 만든 PDF 파일을 나타내는 `BLOB` 객체를 반환합니다.

**참고 항목**

[XDP 문서를 PDF 문서로 변환](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64 인코딩을 사용하는 .NET 클라이언트 어셈블리 만들기](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## PDF 문서 속성 검색 중 {#retrieving-pdf-document-properties}

PDF 유틸리티 Java 및 웹 서비스 API를 사용하여 문서를 읽는 데 필요한 최소 Acrobat 버전인지 여부 등 PDF 문서 속성을 프로그래밍 방식으로 검색할 수 있습니다.

>[!NOTE]
>
>PDF 유틸리티 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### {#summary_of_steps-2} 단계 요약

PDF 문서 속성을 검색하려면 다음 단계를 수행합니다.

1. 프로젝트 파일 포함
1. PDFUftyService 클라이언트를 만듭니다.
1. 속성 검색 작업을 호출합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**PDFUftyService 클라이언트 만들기**

PDF 유틸리티 작업을 프로그래밍 방식으로 수행하려면 먼저 PDFUftyService 클라이언트를 만들어야 합니다. Java API를 사용하면 `PDFUtilityServiceClient` 개체를 만들어 이 작업을 수행할 수 있습니다. 웹 서비스 API를 사용하면 `PDFUtilityServiceService` 개체를 사용하여 완료됩니다.

**속성 검색 작업 호출**

서비스 클라이언트를 만든 후 속성 검색 작업을 호출할 수 있습니다.

**참고 항목**

[Java API를 사용하여 PDF 문서 속성 검색](pdf-utilities.md#retrieve-pdf-document-properties-using-the-java-api)

[웹 서비스 API를 사용하여 PDF 문서 속성 검색](pdf-utilities.md#retrieve-pdf-document-properties-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API {#retrieve-pdf-document-properties-using-the-java-api}을 사용하여 PDF 문서 속성 검색

PDF 유틸리티 API(Java)를 사용하여 PDF 문서 속성 검색:

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-pdfility-client.jar 등의 클라이언트 JAR 파일을 포함합니다.

1. PDFUftyService 클라이언트 만들기

   해당 생성자를 사용하고 연결 속성이 포함된 `ServiceClientFactory` 객체를 전달하여 `PDFUtilityServiceClient` 객체를 만듭니다.

1. 속성 검색 작업 호출

   변환을 수행하려면 `PDFUtilityServiceClient` 객체의 `getPDFProperties` 메서드를 호출하고 다음을 전달합니다.

   * PDF 문서를 나타내는 `com.adobe.idp.Document` 개체
   * 평가할 속성이 포함된 `PDFPropertiesOptionSpec` 객체입니다.

   이 메서드는 쿼리 결과를 포함하는 `PDFPropertiesResult` 객체를 반환합니다.

**참고 항목**

[PDF 문서 속성 검색](pdf-utilities.md#retrieving-pdf-document-properties)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API {#retrieve-pdf-document-properties-using-the-web-service-api}를 사용하여 PDF 문서 속성 검색

PDF 유틸리티 웹 서비스 API를 사용하여 PDF 문서 속성 검색:

1. 프로젝트 파일 포함

   * PDF 유틸리티 서비스 WSDL 파일을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다.
   * Microsoft .NET 클라이언트 어셈블리를 참조하십시오.

1. PDFUftyService 클라이언트 만들기

   프록시 클래스 생성자를 사용하여 `PDFUtilityServiceService` 개체를 만듭니다.

1. 속성 검색 작업 호출

   변환을 수행하려면 `PDFUtilityServiceService` 객체의 `getPDFProperties` 메서드를 호출하고 다음을 전달합니다.

   * PDF 문서를 나타내는 `BLOB` 개체
   * 평가할 속성이 포함된 `PDFPropertiesOptionSpec` 객체입니다.

   이 메서드는 쿼리 결과를 포함하는 `PDFPropertiesResult` 객체를 반환합니다.

**참고 항목**

[PDF 문서 속성 검색](pdf-utilities.md#retrieving-pdf-document-properties)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64 인코딩을 사용하는 .NET 클라이언트 어셈블리 만들기](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## PDF 문서 저장 모드 설정 {#setting-pdf-document-save-modes}

PDF 유틸리티 서비스 Java 및 웹 서비스 API를 사용하여 프로그래밍 방식으로 PDF 문서에 대한 저장 모드를 설정할 수 있습니다. PDF 유틸리티 서비스를 사용하여 저장 모드를 설정할 때 PDF 유틸리티 서비스는 저장 모드만 설정하고 실제로 PDF 문서를 저장하지 않습니다. PDF 문서가 다른 서비스 작업으로 전달되면 저장됩니다. 예를 들어 PDF 유틸리티 서비스를 사용하여 특정 저장 모드를 설정한 다음 암호화 서비스에 전달하면 PDF 문서가 실제로 저장되고 암호화됩니다.

>[!NOTE]
>
>PDF 유틸리티 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### {#summary_of_steps-3} 단계 요약

PDF 문서에 대한 저장 옵션을 설정하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. PDFUftyService 클라이언트를 만듭니다.
1. 저장 모드를 설정합니다.
1. 저장 작업을 호출합니다.
1. PDF 문서를 다른 작업으로 전달합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**PDFUftyService 클라이언트 만들기**

PDF 유틸리티 작업을 프로그래밍 방식으로 수행하려면 먼저 PDFUftyService 클라이언트를 만들어야 합니다. Java API를 사용하면 `PDFUtilityServiceClient` 개체를 만들어 이러한 작업을 수행할 수 있습니다. 웹 서비스 API를 사용하면 `PDFUtilityServiceService` 개체를 사용하여 완료됩니다.

**저장 모드 설정**

다음 저장 옵션 중 하나를 선택할 수 있습니다.

* `INCREMENTAL`:점진적으로 비용을 절감하여 비용 절감
* `FAST_WEB_VIEW`:빠른 웹 보기용으로 저장
* `FULL`:전체 저장(최적화 안 함)을 사용하여 저장하려면

**스타일 저장 작업 호출**

서비스 클라이언트를 만든 후 속성 검색 작업을 호출할 수 있습니다.

**PDF 문서를 다른 AEM Forms 작업으로 전달**

PDF 유틸리티 서비스가 지정된 저장 모드를 설정하면 PDF 문서를 다른 AEM Forms 작업에 전달합니다. 해당 작업에서 반환되면 PDF 문서가 지정된 모드로 저장됩니다. 예를 들어 PDF 유틸리티 서비스를 사용하여 `FAST_WEB_VIEW` 모드를 설정한 다음 PDF 문서를 암호화 서비스의 `encryptUsingPassword` 작업에 전달하는 경우 반환된 PDF 문서는 암호로 암호화되어 `FAST_WEB_VIEW` 모드로 저장됩니다.

>[!NOTE]
>
>이 섹션과 연관된 빠른 시작은 `FAST_WEB_VIEW` 모드를 설정한 다음 PDF 문서를 암호화 서비스의 `encryptUsingPassword` 작업에 전달합니다.

**참고 항목**

[Java API를 사용하여 PDF 문서 저장 옵션 설정](pdf-utilities.md#set-pdf-document-save-options-using-the-java-api)

[웹 서비스 API를 사용하여 PDF 문서 저장 옵션 설정](pdf-utilities.md#set-pdf-document-save-options-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[암호로 PDF 문서 암호화](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Java API {#set-pdf-document-save-options-using-the-java-api}을 사용하여 PDF 문서 저장 옵션 설정

PDF 유틸리티 API(Java)를 사용하여 PDF 문서 저장 옵션을 설정합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-pdfility-client.jar 등의 클라이언트 JAR 파일을 포함합니다.

1. PDFUftyService 클라이언트 만들기

   해당 생성자를 사용하고 연결 속성이 포함된 `ServiceClientFactory` 객체를 전달하여 `PDFUtilityServiceClient` 객체를 만듭니다.

1. 저장 모드 설정

   * 생성자를 사용하여 `PDFUtilitySaveMode` 객체를 만듭니다.
   * `PDFUtilitySaveMode` 객체의 `setSaveStyle` 메서드를 호출하고 저장 모드를 지정하는 문자열 값을 전달하여 저장 모드를 설정합니다. 예를 들어 빠른 웹 보기를 위해 저장하려면 `FAST_WEB_VIEW`을 전달합니다.

1. 스타일 저장 작업 호출

   `PDFUtilityServiceClient` 객체의 `setSaveMode` 메서드를 호출하고 다음 값을 전달합니다.

   * PDF 문서를 나타내는 `com.adobe.idp.Document` 개체
   * 사용할 저장 스타일이 포함된 `PDFUtilitySaveMode` 객체입니다.
   * 이전 설정을 재정의할지 여부를 결정하는 데 사용되는 부울 값입니다.

   이 메서드는 지정된 저장 스타일을 사용하여 형식이 지정된 `com.adobe.idp.Document` 개체를 반환합니다.

1. PDF 문서를 다른 AEM Forms 작업으로 전달

   * 반환된 `com.adobe.idp.Document` 개체를 다른 AEM Forms 작업에 전달합니다.

**참고 항목**

[PDF 문서 저장 모드 설정](pdf-utilities.md#setting-pdf-document-save-modes)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API {#set-pdf-document-save-options-using-the-web-service-api}을 사용하여 PDF 문서 저장 옵션 설정

PDF 유틸리티 AP(웹 서비스)를 사용하여 PDF 문서 저장 옵션을 설정합니다.

1. 프로젝트 파일 포함

   * PDF 유틸리티 서비스 WSDL 파일을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다.
   * Microsoft .NET 클라이언트 어셈블리를 참조하십시오.

1. PDFUftyService 클라이언트 만들기

   프록시 클래스 생성자를 사용하여 `PDFUtilityServiceService` 개체를 만듭니다.

1. 저장 모드 설정

   * 생성자를 사용하여 `PDFUtilitySaveMode` 객체를 만듭니다.
   * 저장 모드를 지정하는 `PDFUtilitySaveMode` 객체의 `saveStyle` 메서드에 문자열 값을 할당하여 저장 모드를 설정합니다. 예를 들어 빠른 웹 보기를 위해 저장하려면 `FAST_WEB_VIEW`을 지정합니다.

1. 스타일 저장 작업 호출

   `PDFUtilityServiceService` 객체의 `setSaveMode` 메서드를 호출하고 다음 값을 전달합니다.

   * PDF 문서를 나타내는 `BLOB` 개체
   * 사용할 저장 스타일이 포함된 `PDFUtilitySaveMode` 객체입니다.
   * 이전 설정을 재정의할지 여부를 결정하는 데 사용되는 부울 값입니다.

   이 메서드는 지정된 저장 스타일을 사용하여 형식이 지정된 `BLOB` 개체를 반환합니다. 그런 다음 해당 개체를 PDF 문서로 저장할 수 있습니다.

1. PDF 문서를 다른 Forms 작업으로 전달

   * 반환된 `BLOB` 개체를 다른 AEM Forms 작업에 전달합니다.

**참고 항목**

[PDF 문서 저장 모드 설정](pdf-utilities.md#setting-pdf-document-save-modes)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64 인코딩을 사용하는 .NET 클라이언트 어셈블리 만들기](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## PDF 문서 기밀 정보 가리기 {#sanitizing-pdf-documents}

PDF 유틸리티 Java API를 사용하여 PDF 문서를 프로그래밍 방식으로 XDP 문서로 변환할 수 있습니다.

>[!NOTE]
>
>PDF 유틸리티 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### {#summary_of_steps-4} 단계 요약

PDF 문서의 기밀 정보를 정리하려면 다음 단계를 수행합니다.

1. 프로젝트 파일 포함
1. PDFUftyService 클라이언트를 만듭니다.
1. 문서의 기밀 정보 가리기 작업을 호출합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 애플리케이션을 만들려면 필요한 JAR 파일을 포함합니다.

**PDFUftyService 클라이언트 만들기**

문서의 기밀 정보 가리기 작업을 프로그래밍 방식으로 수행하려면 먼저 PDFUftyService 클라이언트를 만들어야 합니다. Java API를 사용하면 `PDFUtilityServiceClient` 개체를 만들어 이러한 작업을 수행할 수 있습니다.

**PDF를 XDP로 변환 작업 호출**

서비스 클라이언트를 만든 후 문서의 기밀 정보 가리기 작업을 호출할 수 있습니다.

**참고 항목**

[Java API를 사용하여 PDF 문서를 XDP 문서로 변환](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[웹 서비스 API를 사용하여 PDF 문서를 XDP 문서로 변환](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API {#sanitize-pdf-documents-using-the-java-api}를 사용하여 PDF 문서의 기밀 정보 가리기

PDF 유틸리티 API를 사용하여 문서의 기밀 정보 가리기(Java):

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-pdfility-client.jar 등의 클라이언트 JAR 파일을 포함합니다.

1. PDFUftyService 클라이언트 만들기

   해당 생성자를 사용하고 연결 속성이 포함된 `ServiceClientFactory` 객체를 전달하여 `PDFUtilityServiceClient` 객체를 만듭니다.

1. PDF를 XDP로 변환 작업 호출

   변환을 수행하려면 `PDFUtilityServiceClient` 객체의 `convertPDFtoXDP` 메서드를 호출하고 PDF 파일을 나타내는 `com.adobe.idp.Document` 객체를 전달합니다. 이 메서드는 새로 만든 XDP 파일을 나타내는 `com.adobe.idp.Document` 객체를 반환합니다.

**참고 항목**

[PDF 문서 기밀 정보 가리기](/help/forms/developing/pdf-utilities-service-java-api.md#quick-start-soap-mode-sanitizing-pdf-documents)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
