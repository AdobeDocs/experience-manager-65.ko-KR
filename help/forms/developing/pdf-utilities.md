---
title: PDF 유틸리티 작업
description: PDF 유틸리티 서비스를 사용하여 PDF 및 XDP 파일 형식 간에 변환하고 PDF 문서 속성을 설정 및 검색하며 XMP 메타데이터를 조작합니다.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: e4b204ee-7261-42b8-8db8-a92aa9fd0a28
solution: Experience Manager, Experience Manager Forms
source-git-commit: 872e2de411f51b5f0b26a2ff47cb49f01313d39f
workflow-type: tm+mt
source-wordcount: '2549'
ht-degree: 1%

---

# PDF 유틸리티 작업 {#working-with-pdf-utilities}

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms에 대해서만 적용됩니다.**

**PDF 유틸리티 서비스 정보**

PDF 유틸리티 서비스는 PDF 및 XDP 파일 형식 간에 변환하고 PDF 문서 속성을 설정 및 검색하며 XMP 메타데이터를 조작할 수 있습니다. 예를 들어 PDF 문서를 다른 형식으로 변환하기 전에 해당 속성을 검사하여 변환을 위해 호출할 서비스 작업을 결정하는 것이 유용합니다.

PDF 유틸리티 서비스를 사용하여 다음 작업을 수행할 수 있습니다.

* PDF 문서를 XDP 문서로 변환합니다.
* XDP 문서를 PDF 문서로 변환합니다. (참조: [XDP 문서를 PDF 문서로 변환](pdf-utilities.md#converting-xdp-documents-into-pdf-documents).)
* PDF 문서 속성을 검색합니다. (참조: [PDF 문서 속성 검색](pdf-utilities.md#retrieving-pdf-document-properties).)
* 빠른 웹 보기를 위해 PDF 문서를 저장하고 최적화합니다. (참조: [PDF 문서 저장 모드 설정](pdf-utilities.md#setting-pdf-document-save-modes).)

>[!NOTE]
>
>PDF 유틸리티 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

## PDF 문서를 XDP 문서로 변환 {#converting-pdf-documents-into-xdp-documents}

PDF 유틸리티 Java 및 웹 서비스 API를 사용하여 PDF 문서를 프로그래밍 방식으로 XDP 문서로 변환할 수 있습니다.

>[!NOTE]
>
>PDF 유틸리티 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary-of-steps}

PDF 문서를 XDP 문서로 변환하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. PDFUutilityService 클라이언트를 만듭니다.
1. PDF에서 XDP로 변환 작업을 호출합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**PDFutilityService 클라이언트 만들기**

PDF 유틸리티 작업을 프로그래밍 방식으로 수행하려면 먼저 PDFUutilityService 클라이언트를 만들어야 합니다. Java API를 사용하면 다음을 만들 수 있습니다. `PDFUtilityServiceClient` 개체. 웹 서비스 API를 사용하면 다음을 사용하여 이 작업을 수행할 수 있습니다 `PDFUtilityServiceService` 개체.

**XDP로 PDF 변환 작업 호출**

서비스 클라이언트를 만든 후 XDP에 대한 PDF 변환 작업을 호출할 수 있습니다.

**추가 참조**

[Java API를 사용하여 PDF 문서를 XDP 문서로 변환](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[웹 서비스 API를 사용하여 PDF 문서를 XDP 문서로 변환](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API를 사용하여 PDF 문서를 XDP 문서로 변환 {#convert-pdf-documents-into-xdp-documents-using-the-java-api}

PDF 유틸리티 API(Java)를 사용하여 PDF 문서를 XDP 문서로 변환:

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-pdfutility-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. PDFutilityService 클라이언트 만들기

   만들기 `PDFUtilityServiceClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.

1. XDP로 PDF 변환 작업 호출

   변환을 수행하려면 `PDFUtilityServiceClient` 개체 `convertPDFtoXDP` 방법 및 전달 `com.adobe.idp.Document` PDF 파일을 나타내는 개체입니다. 이 메서드는 `com.adobe.idp.Document` 새로 만든 XDP 파일을 나타내는 개체입니다.

**추가 참조**

[PDF 문서를 XDP 문서로 변환](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 PDF 문서를 XDP 문서로 변환 {#convert-pdf-documents-into-xdp-documents-using-the-web-service-api}

PDF 유틸리티 API(웹 서비스)를 사용하여 PDF 문서를 XDP 문서로 변환합니다.

1. 프로젝트 파일 포함

   * PDF 유틸리티 서비스 WSDL 파일을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다.
   * Microsoft .NET 클라이언트 어셈블리를 참조합니다.

1. PDFutilityService 클라이언트 만들기

   만들기 `PDFUtilityServiceService` 프록시 클래스 생성자를 사용하여 개체를 작성합니다.

1. XDP로 PDF 변환 작업 호출

   호출 `PDFUtilityServiceService` 개체 `convertPDFtoXDP` 방법 및 전달 `BLOB` PDF 파일을 나타내는 개체입니다. 이 메서드는 `BLOB` 새로 만든 XDP 파일을 나타내는 개체입니다.

**추가 참조**

[PDF 문서를 XDP 문서로 변환](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64 인코딩을 사용하는 .NET 클라이언트 어셈블리 만들기](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## XDP 문서를 PDF 문서로 변환 {#converting-xdp-documents-into-pdf-documents}

PDF 유틸리티 Java 및 웹 서비스 API를 사용하여 XDP 문서를 프로그래밍 방식으로 PDF 문서로 변환할 수 있습니다.

>[!NOTE]
>
>PDF 유틸리티 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-1}

XDP 문서를 PDF 문서로 변환하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. PDFUutilityService 클라이언트를 만듭니다.
1. XDP를 PDF으로 변환 작업을 호출합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**PDFutilityService 클라이언트 만들기**

PDF 유틸리티 작업을 프로그래밍 방식으로 수행하려면 먼저 PDFUutilityService 클라이언트를 만들어야 합니다. Java API를 사용하면 다음을 만들 수 있습니다. `PDFUtilityServiceClient` 개체. 웹 서비스 API를 사용하면 다음을 사용하여 이 작업을 수행할 수 있습니다 `PDFUtilityServiceService` 개체.

**XDP에서 PDF으로 변환 작업 호출**

서비스 클라이언트를 만든 후 XDP를 호출하여 PDF 변환 작업을 수행할 수 있습니다.

**추가 참조**

[Java API를 사용하여 XDP 문서를 PDF 문서로 변환](pdf-utilities.md#convert-xdp-documents-into-pdf-documents-using-the-java-api)

[웹 서비스 API를 사용하여 XDP 문서를 PDF 문서로 변환](pdf-utilities.md#converting-xdp-documents-into-pdf-documents-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API를 사용하여 XDP 문서를 PDF 문서로 변환 {#convert-xdp-documents-into-pdf-documents-using-the-java-api}

PDF 유틸리티 API(Java)를 사용하여 XDP 문서를 PDF 문서로 변환합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-pdfutility-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. PDFutilityService 클라이언트 만들기

   만들기 `PDFUtilityServiceClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.

1. XDP에서 PDF으로 변환 작업 호출

   변환을 수행하려면 `PDFUtilityServiceClient` 개체 `convertXDPtoPDF` 방법 및 전달 `com.adobe.idp.Document` xdp 파일을 나타내는 개체입니다. 이 메서드는 `com.adobe.idp.Document` 새로 만든 PDF 파일을 나타내는 개체입니다.

**추가 참조**

[XDP 문서를 PDF 문서로 변환](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 XDP 문서를 PDF 문서로 변환 {#converting-xdp-documents-into-pdf-documents-using-the-web-service-api}

PDF 유틸리티 API(웹 서비스 API)를 사용하여 XDP 문서를 PDF 문서로 변환합니다.

1. 프로젝트 파일 포함

   * PDF 유틸리티 서비스 WSDL 파일을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다.
   * Microsoft .NET 클라이언트 어셈블리를 참조합니다.

1. PDFutilityService 클라이언트 만들기

   만들기 `PDFUtilityServiceService` 프록시 클래스 생성자를 사용하여 개체를 작성합니다.

1. XDP에서 PDF으로 변환 작업 호출

   변환을 수행하려면 `PDFUtilityServiceService` 개체 `convertXDPtoPDF` 방법 및 전달 `BLOB` xdp 파일을 나타내는 개체입니다. 이 메서드는 `BLOB` 새로 만든 PDF 파일을 나타내는 개체입니다.

**추가 참조**

[XDP 문서를 PDF 문서로 변환](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64 인코딩을 사용하는 .NET 클라이언트 어셈블리 만들기](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## PDF 문서 속성 검색 {#retrieving-pdf-document-properties}

PDF 유틸리티 Java 및 웹 서비스 API를 사용하여 문서가 입력 가능한 양식인지 또는 문서를 읽는 데 필요한 최소 Acrobat 버전인지 여부와 같은 PDF 문서 속성을 프로그래밍 방식으로 검색할 수 있습니다.

>[!NOTE]
>
>PDF 유틸리티 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)

### 단계 요약 {#summary_of_steps-2}

PDF 문서 등록 정보를 검색하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. PDFUutilityService 클라이언트를 만듭니다.
1. 속성 검색 작업을 호출합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**PDFutilityService 클라이언트 만들기**

PDF 유틸리티 작업을 프로그래밍 방식으로 수행하려면 먼저 PDFUutilityService 클라이언트를 만들어야 합니다. Java API를 사용하면 다음을 만들 수 있습니다. `PDFUtilityServiceClient` 개체. 웹 서비스 API를 사용하면 다음을 사용하여 작업을 수행할 수 있습니다 `PDFUtilityServiceService` 개체.

**속성 검색 작업 호출**

서비스 클라이언트를 만든 후 속성 검색 작업을 호출할 수 있습니다.

**추가 참조**

[Java API를 사용하여 PDF 문서 속성 검색](pdf-utilities.md#retrieve-pdf-document-properties-using-the-java-api)

[웹 서비스 API를 사용하여 PDF 문서 속성 검색](pdf-utilities.md#retrieve-pdf-document-properties-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API를 사용하여 PDF 문서 속성 검색 {#retrieve-pdf-document-properties-using-the-java-api}

PDF 유틸리티 API(Java)를 사용하여 PDF 문서 속성을 검색합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-pdfutility-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. PDFutilityService 클라이언트 만들기

   만들기 `PDFUtilityServiceClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.

1. 속성 검색 작업 호출

   변환을 수행하려면 `PDFUtilityServiceClient` 개체 `getPDFProperties` 메서드를 호출하고 다음을 전달합니다.

   * A `com.adobe.idp.Document` PDF 문서를 나타내는 개체입니다.
   * A `PDFPropertiesOptionSpec` 평가할 속성이 포함된 개체입니다.

   이 메서드는 `PDFPropertiesResult` 쿼리 결과를 포함하는 개체입니다.

**추가 참조**

[PDF 문서 속성 검색](pdf-utilities.md#retrieving-pdf-document-properties)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 PDF 문서 속성 검색 {#retrieve-pdf-document-properties-using-the-web-service-api}

PDF 유틸리티 웹 서비스 API를 사용하여 PDF 문서 속성을 검색합니다.

1. 프로젝트 파일 포함

   * PDF 유틸리티 서비스 WSDL 파일을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다.
   * Microsoft .NET 클라이언트 어셈블리를 참조합니다.

1. PDFutilityService 클라이언트 만들기

   만들기 `PDFUtilityServiceService` 프록시 클래스 생성자를 사용하여 개체를 작성합니다.

1. 속성 검색 작업 호출

   변환을 수행하려면 `PDFUtilityServiceService` 개체 `getPDFProperties` 메서드를 호출하고 다음을 전달합니다.

   * A `BLOB` PDF 문서를 나타내는 개체입니다.
   * A `PDFPropertiesOptionSpec` 평가할 속성이 포함된 개체입니다.

   이 메서드는 `PDFPropertiesResult` 쿼리 결과를 포함하는 개체입니다.

**추가 참조**

[PDF 문서 속성 검색](pdf-utilities.md#retrieving-pdf-document-properties)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64 인코딩을 사용하는 .NET 클라이언트 어셈블리 만들기](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## PDF 문서 저장 모드 설정 {#setting-pdf-document-save-modes}

PDF 유틸리티 서비스 Java 및 웹 서비스 API를 사용하여 PDF 문서에 대한 저장 모드를 프로그래밍 방식으로 설정할 수 있습니다. PDF 유틸리티 서비스를 사용하여 저장 모드를 설정할 때 PDF 유틸리티 서비스는 저장 모드만 설정하고 PDF 문서를 실제로 저장하지 않습니다. PDF 문서는 다른 서비스 작업으로 전달될 때 저장됩니다. 예를 들어, PDF 유틸리티 서비스를 사용하여 특정 저장 모드를 설정하고 이를 PDF 문서가 실제로 저장되고 암호화되는 암호화 서비스로 전달할 수 있습니다.

>[!NOTE]
>
>PDF 유틸리티 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-3}

PDF 문서에 대해 저장 옵션을 설정하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. PDFUutilityService 클라이언트를 만듭니다.
1. 저장 모드를 설정합니다.
1. 저장 작업을 호출합니다.
1. PDF 문서를 다른 작업에 전달합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**PDFutilityService 클라이언트 만들기**

PDF 유틸리티 작업을 프로그래밍 방식으로 수행하려면 먼저 PDFUutilityService 클라이언트를 만들어야 합니다. Java API를 사용하면 다음을 만들 수 있습니다. `PDFUtilityServiceClient` 개체. 웹 서비스 API를 사용하면 다음을 사용하여 작업을 수행할 수 있습니다 `PDFUtilityServiceService` 개체.

**저장 모드 설정**

다음 저장 옵션 중 하나를 선택할 수 있습니다.

* `INCREMENTAL`: 저장하는 데 필요한 시간을 줄이기 위해 증분 저장
* `FAST_WEB_VIEW`: 신속한 웹 보기를 위해 저장
* `FULL`: 전체 저장을 사용하여 저장(최적화 안 함)

**스타일 저장 작업 호출**

서비스 클라이언트를 만든 후 속성 검색 작업을 호출할 수 있습니다.

**다른 AEM Forms 작업에 PDF 문서 전달**

PDF 유틸리티 서비스에서 지정된 저장 모드를 설정한 후 PDF 문서를 다른 AEM Forms 작업에 전달합니다. 해당 작업에서 반환되면 PDF 문서가 지정된 모드로 저장됩니다. 예를 들어 PDF 유틸리티 서비스를 사용하여 `FAST_WEB_VIEW` 을(를) 설정한 다음 PDF 문서를 `encryptUsingPassword` 그러면 반환된 PDF 문서가 암호로 암호화되어 `FAST_WEB_VIEW` 모드.

>[!NOTE]
>
>이 섹션과 연결된 빠른 시작은 `FAST_WEB_VIEW` 을(를) 설정한 다음 PDF 문서를 `encryptUsingPassword` 작업.

**추가 참조**

[Java API를 사용하여 PDF 문서 저장 옵션 설정](pdf-utilities.md#set-pdf-document-save-options-using-the-java-api)

[웹 서비스 API를 사용하여 PDF 문서 저장 옵션 설정](pdf-utilities.md#set-pdf-document-save-options-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[암호로 PDF 문서 암호화](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Java API를 사용하여 PDF 문서 저장 옵션 설정 {#set-pdf-document-save-options-using-the-java-api}

PDF 유틸리티 API(Java)를 사용하여 PDF 문서 저장 옵션을 설정합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-pdfutility-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. PDFutilityService 클라이언트 만들기

   만들기 `PDFUtilityServiceClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.

1. 저장 모드 설정

   * 만들기 `PDFUtilitySaveMode` 개체를 만들 때 사용됩니다.
   * 를 호출하여 저장 모드 설정 `PDFUtilitySaveMode` 개체 `setSaveStyle` 메서드 및 저장 모드를 지정하는 문자열 값 전달 예를 들어, 빠른 웹 보기를 위해 저장하려면 을 전달합니다 `FAST_WEB_VIEW`.

1. 스타일 저장 작업 호출

   호출 `PDFUtilityServiceClient` 개체 `setSaveMode` 메서드를 실행하고 다음 값을 전달합니다.

   * A `com.adobe.idp.Document` PDF 문서를 나타내는 개체입니다.
   * A `PDFUtilitySaveMode` 사용할 저장 스타일이 포함된 개체입니다.
   * 이전 설정을 재정의할지 여부를 결정하는 데 사용되는 부울 값.

   이 메서드는 `com.adobe.idp.Document` 지정된 저장 스타일을 사용하여 형식이 지정된 개체입니다.

1. 다른 AEM Forms 작업에 PDF 문서 전달

   * 반환된 을 전달합니다. `com.adobe.idp.Document` 다른 AEM Forms 작업에 대한 개체입니다.

**추가 참조**

[PDF 문서 저장 모드 설정](pdf-utilities.md#setting-pdf-document-save-modes)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 PDF 문서 저장 옵션 설정 {#set-pdf-document-save-options-using-the-web-service-api}

PDF 유틸리티 AP(웹 서비스)를 사용하여 PDF 문서 저장 옵션을 설정합니다.

1. 프로젝트 파일 포함

   * PDF 유틸리티 서비스 WSDL 파일을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다.
   * Microsoft .NET 클라이언트 어셈블리를 참조합니다.

1. PDFutilityService 클라이언트 만들기

   만들기 `PDFUtilityServiceService` 프록시 클래스 생성자를 사용하여 개체를 작성합니다.

1. 저장 모드 설정

   * 만들기 `PDFUtilitySaveMode` 개체를 만들 때 사용됩니다.
   * 문자열 값을 로 할당하여 저장 모드 설정 `PDFUtilitySaveMode` 개체 `saveStyle` 저장 모드를 지정하는 메서드. 예를 들어, 빠른 웹 보기를 위해 저장하려면 을 지정합니다 `FAST_WEB_VIEW`.

1. 스타일 저장 작업 호출

   호출 `PDFUtilityServiceService` 개체 `setSaveMode` 메서드를 실행하고 다음 값을 전달합니다.

   * A `BLOB` PDF 문서를 나타내는 개체입니다.
   * A `PDFUtilitySaveMode` 사용할 저장 스타일이 포함된 개체입니다.
   * 이전 설정을 재정의할지 여부를 결정하는 데 사용되는 부울 값.

   이 메서드는 `BLOB` 지정된 저장 스타일을 사용하여 형식이 지정된 개체입니다. 그런 다음 해당 개체를 PDF 문서로 저장할 수 있습니다.

1. 다른 Forms 작업에 PDF 문서 전달

   * 반환된 을 전달합니다. `BLOB` 다른 AEM Forms 작업에 대한 개체입니다.

**추가 참조**

[PDF 문서 저장 모드 설정](pdf-utilities.md#setting-pdf-document-save-modes)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64 인코딩을 사용하는 .NET 클라이언트 어셈블리 만들기](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## PDF 문서 정리 {#sanitizing-pdf-documents}

PDF 유틸리티 Java API를 사용하여 PDF 문서를 프로그래밍 방식으로 XDP 문서로 변환할 수 있습니다.

>[!NOTE]
>
>PDF 유틸리티 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-4}

PDF 문서를 소독하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. PDFUutilityService 클라이언트를 만듭니다.
1. 정리 작업을 호출합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 작성하려면 필요한 JAR 파일을 포함합니다.

**PDFutilityService 클라이언트 만들기**

정리 작업을 프로그래밍 방식으로 수행하려면 먼저 PDFUutilityService 클라이언트를 만들어야 합니다. Java API를 사용하면 다음을 만들 수 있습니다. `PDFUtilityServiceClient` 개체.

**XDP로 PDF 변환 작업 호출**

서비스 클라이언트를 만든 후 정리 작업을 호출할 수 있습니다.

**추가 참조**

[Java API를 사용하여 PDF 문서를 XDP 문서로 변환](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[웹 서비스 API를 사용하여 PDF 문서를 XDP 문서로 변환](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API를 사용하여 PDF 문서 삭제 {#sanitize-pdf-documents-using-the-java-api}

PDF 유틸리티 API(Java)를 사용하여 문서를 정리합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-pdfutility-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. PDFutilityService 클라이언트 만들기

   만들기 `PDFUtilityServiceClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.

1. XDP로 PDF 변환 작업 호출

   변환을 수행하려면 `PDFUtilityServiceClient` 개체 `convertPDFtoXDP` 방법 및 전달 `com.adobe.idp.Document` PDF 파일을 나타내는 개체입니다. 이 메서드는 `com.adobe.idp.Document` 새로 만든 XDP 파일을 나타내는 개체입니다.

**추가 참조**

[PDF 문서 정리](/help/forms/developing/pdf-utilities-service-java-api.md#quick-start-soap-mode-sanitizing-pdf-documents)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
