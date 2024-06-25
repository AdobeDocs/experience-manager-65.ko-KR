---
title: 바코드 형식을 사용한 작업
description: Java API 및 웹 서비스 API를 사용하여 바코드가 포함된 PDF 양식 또는 이미지의 데이터를 디코딩합니다.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: dd32808e-b773-48a2-90e1-7a277d349493
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations,Barcoded Forms
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1911'
ht-degree: 0%

---

# 바코드 형식을 사용한 작업 {#working-with-barcoded-forms}

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms에 대해서만 적용됩니다.**

## 바코드 양식 서비스 정보 {#about-the-barcoded-forms-service}

바코드 양식 서비스는 작성 및 인쇄 양식의 데이터 캡처를 자동화하고 캡처된 정보를 조직의 핵심 IT 시스템에 통합합니다.

바코드 양식 서비스를 사용하여 대화형 PDF forms에 1차원 및 2차원 바코드를 추가할 수 있습니다. 그런 다음 바코드 양식을 웹 사이트에 게시하거나 이메일 또는 CD로 배포할 수 있습니다. 사용자가 Adobe Reader, Acrobat Professional 또는 Acrobat Standard을 사용하여 바코드 양식을 채울 경우 바코드가 자동으로 업데이트되어 사용자가 제공한 양식 데이터를 인코딩합니다. 사용자는 양식을 전자적으로 제출하거나 종이에 인쇄하여 우편, 팩스, 손으로 제출할 수 있다. 나중에 사용자 제공 데이터를 자동화된 워크플로의 일부로 추출하여 승인 프로세스와 비즈니스 시스템 간에 데이터를 라우팅할 수 있습니다.

바코드 양식 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

## 바코드 형식 데이터 디코딩 {#decoding-barcoded-form-data}

바코드 양식 서비스 API를 사용하여 PDF 양식 또는 바코드가 포함된 이미지에서 데이터를 디코딩할 수 있습니다. 양식 데이터를 디코딩하는 것은 바코드에 들어 있는 데이터를 추출하는 것을 의미한다. PDF 양식(또는 이미지)에서 데이터를 디코딩하려면 먼저 사용자가 양식을 데이터로 채워야 합니다.

>[!NOTE]
>
>바코드 양식 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary-of-steps}

PDF 양식에서 데이터를 디코딩하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. barcoded formsClient API 개체를 만듭니다.
1. 바코드 데이터가 포함된 PDF 양식을 가져옵니다.
1. PDF 양식에서 데이터를 디코딩합니다.
1. 데이터를 XML 데이터 소스로 변환합니다.
1. 디코딩된 데이터를 처리합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 생성하는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-barcodedforms-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar (AEM Forms이 JBoss에 배포된 경우 필수)
* xercesImpl.jar(in &lt;install directory=&quot;&quot;>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs\thirdparty)

AEM Forms이 JBOSS가 아닌 지원되는 J2EE 애플리케이션 서버에 배포된 경우 adobe-utilities.jar 및 jbossall-client.jar을 AEM Forms이 배포된 J2EE 애플리케이션 서버에 관련된 JAR 파일로 교체해야 합니다. 모든 AEM Forms JAR 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**바코드된 양식 클라이언트 API 개체 만들기**

바코드 형식 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 바코드 Forms 서비스 클라이언트를 만들어야 합니다. Java API를 사용하는 경우 `BarcodedFormsServiceClient` 개체. 바코드 양식 웹 서비스 API를 사용하는 경우 `BarcodedFormsServiceService` 개체.

**바코드 데이터가 포함된 PDF 양식 받기**

사용자 데이터로 채워진 바코드가 포함된 PDF 양식을 가져옵니다.

**PDF 양식에서 데이터 디코딩**

바코드가 포함된 PDF 양식(또는 이미지)을 가져온 후 데이터를 디코딩할 수 있습니다. Barcoded Forms 서비스는 다음 유형의 바코드를 지원합니다.

* PDF417 바코드.
* 데이터 매트릭스 바코드.
* QR 코드 바코드.
* 코다바 바코드요
* 코드 128 바코드.
* 코드 39 바코드.
* EAN-13 바코드.
* EAN-8 바코드.

decode API에서 16진수로 입력된 문자 집합은 바코드의 콘텐츠가 16진수 문자열로 인코딩됨을 의미합니다. 예를 들어 UTF-8이 형식으로 문자 인코딩으로 지정되고 16진수가 디코딩 작업에서 지정된 경우 바코드의 콘텐츠는 &lt; `xb:content`> 요소를 디코딩한 출력입니다. 클라이언트 응용 프로그램에서 응용 프로그램 논리를 만들어 이 16진수 값을 변환하여 원래 콘텐츠를 가져올 수 있습니다.

**데이터를 XML 데이터 소스로 변환**

양식 데이터를 디코딩한 후 XDP 또는 XFDF 데이터로 변환할 수 있습니다. 예를 들어 데이터를 다른 양식으로 가져오려고 한다고 가정해 보겠습니다. 데이터를 XFA 양식으로 가져오려면 데이터를 XDP 데이터로 변환해야 합니다. 자세한 내용은 [양식 데이터 가져오기](/help/forms/developing/importing-exporting-data.md#importing-form-data).

**디코딩된 데이터 처리**

비즈니스 요구 사항을 충족하도록 변환된 데이터를 처리할 수 있습니다. 예를 들어 데이터를 디코딩하고 변환한 후 파일에 저장하고 엔터프라이즈 데이터베이스에 저장하고 다른 양식을 채우는 등의 작업을 수행할 수 있습니다. 이 섹션에서는 변환된 데이터를 XML 파일로 저장하는 방법에 대해 설명합니다.

>[!NOTE]
>
>줄 구분 기호와 필드 구분 기호 매개 변수의 값이 동일한 경우 바코드 양식 서비스가 바코드 데이터를 디코딩하지 못했습니다

**추가 참조**

[Java API를 사용하여 바코드 형식 데이터 디코딩](barcoded-forms.md#decode-barcoded-form-data-using-the-java-api)

[웹 서비스 API를 사용하여 바코드 형식 데이터 디코딩](barcoded-forms.md#decode-barcoded-form-data-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API를 사용하여 바코드 형식 데이터 디코딩 {#decode-barcoded-form-data-using-the-java-api}

Java(barcoded forms API)를 사용하여 양식 데이터를 디코딩합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 클라이언트 JAR 파일을 포함합니다.

1. 바코드된 양식 클라이언트 API 개체 만들기

   만들기 `BarcodedFormsServiceClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.

1. 바코드 데이터가 포함된 PDF 양식 받기

   * 만들기 `java.io.FileInputStream` 해당 생성자를 사용하고 PDF 문서의 위치를 지정하는 문자열 값을 전달하여 바코드 처리된 데이터가 포함된 PDF 양식을 나타내는 개체입니다.
   * 만들기 `com.adobe.idp.Document` 개체를 생성자를 사용하고 `java.io.FileInputStream` 개체.

1. PDF 양식에서 데이터 디코딩

   를 호출하여 양식 데이터 디코딩 `BarcodedFormsServiceClient` 개체 `decode` 메서드 및 다음 값 전달:

   * 다음 `com.adobe.idp.Document` PDF 양식을 포함하는 객체입니다.
   * A `java.lang.Boolean` PDF417 바코드를 디코딩할지 여부를 지정하는 개체입니다.
   * A `java.lang.Boolean` data matrix 바코드를 디코딩할지 여부를 지정하는 개체입니다.
   * A `java.lang.Boolean` QR 코드 바코드를 디코딩할지 여부를 지정하는 개체입니다.
   * A `java.lang.Boolean` 코드 바코드를 디코딩할지 여부를 지정하는 개체입니다.
   * A `java.lang.Boolean` 코드 128 바코드를 디코딩할지 여부를 지정하는 개체입니다.
   * A `java.lang.Boolean` 코드 39 바코드를 디코딩할지 여부를 지정하는 개체입니다.
   * A `java.lang.Boolean` ean-13 바코드를 디코딩할지 여부를 지정하는 개체입니다.
   * A `java.lang.Boolean` ean-8 바코드를 디코딩할지 여부를 지정하는 개체입니다.
   * A `com.adobe.livecycle.barcodedforms.CharSet` 바코드에 사용되는 문자 집합 인코딩 값을 지정하는 열거형 값입니다.

   다음 `decode` 메서드가 다음을 반환합니다. `org.w3c.dom.Document` 디코딩된 양식 데이터를 포함하는 개체입니다.

1. 데이터를 XML 데이터 소스로 변환

   를 호출하여 디코딩된 데이터를 XDP 또는 XFDF 데이터로 변환 `BarcodedFormsServiceClient` 개체 `extractToXML` 메서드 및 다음 값 전달:

   * 다음 `org.w3c.dom.Document` 디코딩된 데이터가 포함된 개체 `decode` 메서드의 반환 값)입니다.
   * A `com.adobe.livecycle.barcodedforms.Delimiter` 줄 구분 기호를 지정하는 열거형 값입니다. 다음을 지정하는 것이 좋습니다. `Delimiter.Carriage_Return`.
   * A `com.adobe.livecycle.barcodedforms.Delimiter` 필드 구분 기호를 지정하는 열거형 값입니다. 예를 들어 을 지정합니다 `Delimiter.Tab`.
   * A `com.adobe.livecycle.barcodedforms.XMLFormat` 바코드 데이터를 XDP 또는 XFDF XML 데이터로 변환할지 여부를 지정하는 열거형 값입니다. 예를 들어 을 지정합니다 `XMLFormat.XDP` 를 클릭하여 데이터를 XDP 데이터로 변환합니다.

   >[!NOTE]
   >
   >줄 구분 기호 및 필드 구분 기호 매개 변수에 동일한 값을 지정하지 마십시오.

   다음 `extractToXML` 메서드가 을 반환합니다. `java.util.List` 각 요소가 다음에 있는 개체 `org.w3c.dom.Document` 개체. 양식에 있는 각 바코드에는 별도의 요소가 있습니다. 즉, 형식에 4개의 바코드가 있는 경우 반환되는 요소에 4개의 요소가 있습니다 `java.util.List` 개체.

1. 디코딩된 데이터 처리

   * 다음을 반복합니다. `java.util.List` 각각 가져올 개체 `org.w3c.dom.Document` 목록에 있는 개체입니다.
   * 목록의 각 요소에 대해 `org.w3c.dom.Document` 에 대한 오브젝트 `com.adobe.idp.Document` 개체. (를 변환하는 애플리케이션 논리 `org.w3c.dom.Document` 에 오브젝트 추가 `com.adobe.idp.Document` 객체는 Java API 예를 사용하여 바코드 처리된 양식 데이터 디코딩에 표시됩니다).
   * 를 호출하여 XML 데이터를 XML 파일로 저장 `com.adobe.idp.Document` 개체 `copyToFile`를 클릭하고 XML 파일을 나타내는 File 개체를 전달합니다.

**추가 참조**

[빠른 시작(SOAP 모드): Java API를 사용하여 바코드 형식 데이터 디코딩](/help/forms/developing/barcoded-forms-service-java-api.md#quick-start-soap-mode-decoding-barcoded-form-data-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 바코드 형식 데이터 디코딩 {#decode-barcoded-form-data-using-the-web-service-api}

바코드 양식 API(웹 서비스)를 사용하여 양식 데이터 디코딩:

1. 프로젝트 파일 포함

   * 바코드 형식 서비스 WSDL을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다. 자세한 내용은 [Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).
   * Microsoft .NET 클라이언트 어셈블리를 참조합니다. 자세한 내용은 의 &quot;.NET 클라이언트 어셈블리 참조&quot;를 참조하십시오 [Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).

1. 바코드된 양식 클라이언트 API 개체 만들기

   바코드 형식 서비스 WSDL을 사용하는 Microsoft .NET 클라이언트 어셈블리를 사용하여 `BarcodedFormsServiceService` 기본 생성자를 호출하여 개체를 작성합니다.

1. 바코드 데이터가 포함된 PDF 양식 받기

   * 만들기 `BLOB` 개체를 만들 때 사용됩니다. 다음 `BLOB` 개체는 바코드가 포함된 PDF 문서를 저장하는 데 사용됩니다.
   * 만들기 `System.IO.FileStream` PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 콘텐츠를 저장하는 바이트 배열 만들기 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채우기 `System.IO.FileStream` 개체 `Read` 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하는 방법.
   * 채우기 `BLOB` 개체 할당 `binaryData` 속성을 바이트 배열의 콘텐츠와 함께 사용합니다.

1. PDF 양식에서 데이터 디코딩

   를 호출하여 양식 데이터 디코딩 `BarcodedFormsServiceService` 개체 `decode` 메서드 및 다음 값 전달:

   * 다음 `BLOB` PDF 양식을 포함하는 객체입니다.
   * A `Boolean` PDF417 바코드를 디코딩할지 여부를 지정하는 개체입니다.
   * A `Boolean` data matrix 바코드를 디코딩할지 여부를 지정하는 개체입니다.
   * A `Boolean` QR 코드 바코드를 디코딩할지 여부를 지정하는 개체입니다.
   * A `Boolean` 코드 바코드를 디코딩할지 여부를 지정하는 개체입니다.
   * A `Boolean` 코드 128 바코드를 디코딩할지 여부를 지정하는 개체입니다.
   * A `Bolean` 코드 39 바코드를 디코딩할지 여부를 지정하는 개체입니다.
   * A `Boolean` ean-13 바코드를 디코딩할지 여부를 지정하는 개체입니다.
   * A `Boolean` ean-8 바코드를 디코딩할지 여부를 지정하는 개체입니다.
   * A `CharSet` 바코드에 사용되는 문자 집합 인코딩 값을 지정하는 열거형 값입니다.

   다음 `decode` 메서드는 디코딩된 양식 데이터를 포함하는 문자열 값을 반환합니다.

1. 데이터를 XML 데이터 소스로 변환

   를 호출하여 디코딩된 데이터를 XDP 또는 XFDF 데이터로 변환 `BarcodedFormsServiceService` 개체 `extractToXML` 메서드 및 다음 값 전달:

   * 디코딩된 데이터를 포함하는 문자열 값 (다음을 사용하는지 확인) `decode` 메서드의 반환 값)입니다.
   * A `Delimiter` 줄 구분 기호를 지정하는 열거형 값입니다. 다음을 지정하는 것이 좋습니다. `Delimiter.Carriage_Return`.
   * A `Delimiter` 필드 구분 기호를 지정하는 열거형 값입니다. 예를 들어 을 지정합니다 `Delimiter.Tab`.
   * A `XMLFormat` 바코드 데이터를 XDP 또는 XFDF XML 데이터로 변환할지 여부를 지정하는 열거형 값입니다. 예를 들어 을 지정합니다 `XMLFormat.XDP` 를 클릭하여 데이터를 XDP 데이터로 변환합니다.

   >[!NOTE]
   >
   >줄 구분 기호 및 필드 구분 기호 매개 변수에 동일한 값을 지정하지 마십시오.

   다음 `extractToXML` 메서드가 다음을 반환합니다. `Object` 각 요소가 `BLOB` 인스턴스. 양식에 있는 각 바코드에는 별도의 요소가 있습니다. 즉, 형식에 4개의 바코드가 있는 경우 반환되는 요소에 4개의 요소가 있습니다 `Object` 배열입니다.

1. 디코딩된 데이터 처리

   * 만들기 `System.IO.FileStream` 해당 생성자를 호출하고 보안 PDF 문서의 파일 위치를 나타내는 문자열 값을 전달하여 객체를 생성합니다.
   * 의 데이터 콘텐츠를 저장하는 바이트 배열 만들기 `BLOB` 에서 반환한 개체 `encryptPDFUsingPassword` 메서드를 사용합니다. 의 값을 가져와서 바이트 배열 채우기 `BLOB` 개체 `binaryData` 데이터 구성원입니다.
   * 만들기 `System.IO.BinaryWriter` 개체를 호출하고 `System.IO.FileStream` 개체.
   * 를 호출하여 바이트 배열의 내용을 PDF 파일에 씁니다 `System.IO.BinaryWriter` 개체 `Write` 메서드 및 바이트 배열 전달.

**추가 참조**

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
