---
title: 바코드 양식 작업
seo-title: 바코드 양식 작업
description: Java API 및 웹 서비스 API를 사용하여 바코드가 포함된 PDF 양식 또는 이미지의 데이터를 디코딩합니다.
seo-description: Java API 및 웹 서비스 API를 사용하여 바코드가 포함된 PDF 양식 또는 이미지의 데이터를 디코딩합니다.
uuid: e56c3c94-384d-401f-b418-dd34cdc57eda
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: eb28ac30-265c-4611-8247-1f4bc826f254
role: 개발자
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1946'
ht-degree: 0%

---


# 바코드 양식 작업 {#working-with-barcoded-forms}

**이 문서의 샘플과 예는 JEE 환경의 AEM Forms에만 해당됩니다.**

## 바코드 양식 서비스 {#about-the-barcoded-forms-service} 정보

바코드 양식 서비스는 채우기 및 인쇄 양식의 데이터 캡처를 자동화하고 캡처한 정보를 조직의 핵심 IT 시스템에 통합합니다.

바코드 양식 서비스를 사용하여 1차원 바코드를 대화형 PDF forms에 추가할 수 있습니다. 그런 다음 바코드 양식을 웹 사이트에 게시하거나 이메일 또는 CD로 배포할 수 있습니다. 사용자가 Adobe Reader, Acrobat Professional 또는 Acrobat Standard을 사용하여 바코드된 양식을 채우면 바코드가 자동으로 업데이트되어 사용자가 제공한 양식 데이터를 인코딩합니다. 사용자는 양식을 전자적으로 제출하거나 종이에 인쇄하여 우편, 팩스 또는 손으로 제출할 수 있습니다. 나중에 자동화된 워크플로우의 일부로 사용자가 제공한 데이터를 추출하여 승인 프로세스와 비즈니스 시스템 간에 데이터를 라우팅할 수 있습니다.

바코드 양식 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

## 바코드 양식 데이터 {#decoding-barcoded-form-data} 디코딩

바코드 양식 서비스 API를 사용하여 PDF 양식 또는 바코드가 포함된 이미지의 데이터를 디코딩할 수 있습니다. 양식 데이터를 디코딩하는 것은 바코드에 있는 데이터를 추출하는 것을 의미합니다. 데이터를 PDF 양식(또는 이미지)에서 디코딩하기 전에 사용자가 데이터로 양식을 채워야 합니다.

>[!NOTE]
>
>바코드 양식 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### {#summary-of-steps} 단계 요약

PDF 양식의 데이터를 디코딩하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. 바코드 formsClient API 객체를 만듭니다.
1. 바코드 데이터가 포함된 PDF 양식을 가져올 수 있습니다.
1. PDF 양식의 데이터를 디코딩합니다.
1. 데이터를 XML 데이터 소스로 변환합니다.
1. 디코딩된 데이터를 처리합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

다음 JAR 파일을 프로젝트의 클래스 경로에 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-barcodedforms-client.jar
* adobe-utilities.jar(AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필수)
* xercesImpl.jar(&lt;설치 디렉토리>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs\thirdparty에 있음)

AEM Forms이 JBOSS가 아닌 지원되는 J2EE 응용 프로그램 서버에 배포되는 경우 adobe-utilities.jar 및 jbossall-client.jar를 AEM Forms이 배포된 J2EE 응용 프로그램 서버에 해당하는 JAR 파일로 대체해야 합니다. 모든 AEM Forms JAR 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)을 참조하십시오.

**바코드 양식 클라이언트 API 개체 만들기**

바코드 양식 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 Barcoded Forms 서비스 클라이언트를 만들어야 합니다. Java API를 사용하는 경우 `BarcodedFormsServiceClient` 개체를 만듭니다. 바코드 양식 웹 서비스 API를 사용하는 경우 `BarcodedFormsServiceService` 개체를 만듭니다.

**바코드 데이터가 포함된 PDF 양식 가져오기**

사용자 데이터로 채워진 바코드가 포함된 PDF 양식을 받아야 합니다.

**PDF 양식의 데이터 디코딩**

바코드가 포함된 PDF 양식(또는 이미지)을 가져온 후 데이터를 디코딩할 수 있습니다. Barcoded Forms 서비스는 다음과 같은 유형의 바코드를 지원합니다.

* PDF417 바코드를 참조하십시오.
* 데이터 매트릭스 바코드를 참조하십시오.
* QR 코드 바코드를 참조하십시오.
* 코다바 바코드.
* 코드 128 바코드.
* 코드 39 바코드.
* EAN-13 바코드.
* EAN-8 바코드.

디코드 API에서 문자 집합 입력은 바코드 내용이 16진수 문자열로 인코딩됨을 의미합니다. 예를 들어 UTF-8이 양식의 문자 인코딩으로 지정되고 Hex가 디코딩 작업에 지정되면 코드 코드의 내용은 디코딩된 출력의 &lt; `xb:content` 요소에 Hex 문자열로 인코딩됩니다. 클라이언트 응용 프로그램에서 응용 프로그램 논리를 만들어 이 16진수 값을 변환하여 원래 콘텐츠를 가져올 수 있습니다.

**데이터를 XML 데이터 소스로 변환**

양식 데이터를 디코딩한 후 XDP 또는 XFDF 데이터로 변환할 수 있습니다. 예를 들어 데이터를 다른 형식으로 가져오려고 한다고 가정합니다. 데이터를 XFA 양식으로 가져오려면 데이터를 XDP 데이터로 변환해야 합니다. 자세한 내용은 [양식 데이터 가져오기](/help/forms/developing/importing-exporting-data.md#importing-form-data)를 참조하십시오.

**디코딩된 데이터 처리**

변환된 데이터를 처리하여 비즈니스 요구 사항을 충족할 수 있습니다. 예를 들어 데이터를 디코딩하고 변환한 후 파일에 저장하여 엔터프라이즈 데이터베이스에 저장하고 다른 양식을 채우는 등의 작업을 수행할 수 있습니다. 이 섹션에서는 변환된 데이터를 XML 파일로 저장하는 방법을 설명합니다.

>[!NOTE]
>
>줄 구분 기호 및 필드 구분 기호 매개 변수가 같은 값을 갖는 경우 바코딩된 양식 서비스가 바코드 데이터를 디코딩하지 못합니다

**참고 항목**

[Java API를 사용하여 바코드 양식 데이터 디코딩](barcoded-forms.md#decode-barcoded-form-data-using-the-java-api)

[웹 서비스 API를 사용하여 바코드 양식 데이터 디코딩](barcoded-forms.md#decode-barcoded-form-data-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API {#decode-barcoded-form-data-using-the-java-api}를 사용하여 바코드 양식 데이터 디코딩

바코드 양식 API(Java)를 사용하여 양식 데이터를 디코딩합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 클라이언트 JAR 파일을 포함합니다.

1. 바코드 양식 클라이언트 API 개체 만들기

   해당 생성자를 사용하고 연결 속성이 포함된 `ServiceClientFactory` 객체를 전달하여 `BarcodedFormsServiceClient` 객체를 만듭니다.

1. 바코드 데이터가 포함된 PDF 양식 가져오기

   * 생성자를 사용하여 PDF 문서의 위치를 지정하는 문자열 값을 전달하여 바코드된 데이터가 포함된 PDF 양식을 나타내는 `java.io.FileInputStream` 객체를 만듭니다.
   * 생성자를 사용하여 `com.adobe.idp.Document` 개체를 만들고 `java.io.FileInputStream` 개체를 전달합니다.

1. PDF 양식의 데이터 디코딩

   `BarcodedFormsServiceClient` 객체의 `decode` 메서드를 호출하고 다음 값을 전달하여 양식 데이터를 디코딩합니다.

   * PDF 양식이 포함된 `com.adobe.idp.Document` 개체
   * PDF417 바코드를 디코딩할지 여부를 지정하는 `java.lang.Boolean` 개체
   * 데이터 행렬 바코드를 디코딩할지 여부를 지정하는 `java.lang.Boolean` 객체입니다.
   * QR 코드 바코드를 디코딩할지 여부를 지정하는 `java.lang.Boolean` 객체입니다.
   * 코드 바코드를 디코딩할지 여부를 지정하는 `java.lang.Boolean` 객체입니다.
   * 코드 128 바코드를 디코딩할지 여부를 지정하는 `java.lang.Boolean` 객체입니다.
   * 코드 39 바코드를 디코딩할지 여부를 지정하는 `java.lang.Boolean` 객체입니다.
   * EAN-13 바코드를 디코딩할지 여부를 지정하는 `java.lang.Boolean` 객체입니다.
   * EAN-8 바코드를 디코딩할지 여부를 지정하는 `java.lang.Boolean` 객체입니다.
   * 바코드에 사용된 문자 집합 인코딩 값을 지정하는 `com.adobe.livecycle.barcodedforms.CharSet` 열거형 값.

   `decode` 메서드는 디코딩된 양식 데이터를 포함하는 `org.w3c.dom.Document` 객체를 반환합니다.

1. 데이터를 XML 데이터 소스로 변환

   디코딩된 데이터를 `BarcodedFormsServiceClient` 개체의 `extractToXML` 메서드를 호출하고 다음 값을 전달하여 XDP 또는 XFDF 데이터로 변환합니다.

   * 디코딩된 데이터가 포함된 `org.w3c.dom.Document` 개체입니다(`decode` 메서드의 반환 값을 사용하는지 확인).
   * 줄 구분 기호를 지정하는 `com.adobe.livecycle.barcodedforms.Delimiter` 열거형 값입니다. `Delimiter.Carriage_Return`을 지정하는 것이 좋습니다.
   * 필드 구분 기호를 지정하는 `com.adobe.livecycle.barcodedforms.Delimiter` 열거형 값입니다. 예를 들어 `Delimiter.Tab`을 지정합니다.
   * 바코드 데이터를 XDP 또는 XFDF XML 데이터로 변환할지 여부를 지정하는 `com.adobe.livecycle.barcodedforms.XMLFormat` 열거형 값입니다. 예를 들어 데이터를 XDP 데이터로 변환하려면 `XMLFormat.XDP`을 지정합니다.

   >[!NOTE]
   >
   >줄 구분 기호 및 필드 구분 기호 매개 변수에 동일한 값을 지정하지 마십시오.

   `extractToXML` 메서드는 각 요소가 `org.w3c.dom.Document` 개체인 `java.util.List` 객체를 반환합니다. 양식에 있는 각 바코드에 별도의 요소가 있습니다. 즉, 양식에 4개의 바코드가 있으면 반환된 `java.util.List` 개체에 4개의 요소가 있습니다.

1. 디코딩된 데이터 처리

   * 목록에 있는 각 `org.w3c.dom.Document` 개체를 가져오려면 `java.util.List` 개체를 반복합니다.
   * 목록의 각 요소에 대해 `org.w3c.dom.Document` 개체를 `com.adobe.idp.Document` 개체로 변환합니다. (`org.w3c.dom.Document` 개체를 `com.adobe.idp.Document` 개체로 변환하는 응용 프로그램 로직은 Java API 예제를 사용하여 디코딩 양식 데이터에 표시됩니다.)
   * `com.adobe.idp.Document` 객체의 `copyToFile`을 호출하고 XML 파일을 나타내는 File 객체를 전달하여 XML 데이터를 XML 파일로 저장합니다.

**참고 항목**

[빠른 시작(SOAP 모드):Java API를 사용하여 바코드 양식 데이터 디코딩](/help/forms/developing/barcoded-forms-service-java-api.md#quick-start-soap-mode-decoding-barcoded-form-data-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API {#decode-barcoded-form-data-using-the-web-service-api}를 사용하여 바코드 양식 데이터 디코딩

바코드 양식 API(웹 서비스)를 사용하여 양식 데이터를 디코딩합니다.

1. 프로젝트 파일 포함

   * 바코드 양식 서비스 WSDL을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다. 자세한 내용은 [Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)을 참조하십시오.
   * Microsoft .NET 클라이언트 어셈블리를 참조하십시오. 자세한 내용은 [Base64 인코딩](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)을 사용하여 AEM Forms 호출의 &quot;Referencing the .NET client assembly&quot;를 참조하십시오.

1. 바코드 양식 클라이언트 API 개체 만들기

   바코드 양식 서비스 WSDL을 사용하는 Microsoft .NET 클라이언트 어셈블리를 사용하여 기본 생성자를 호출하여 `BarcodedFormsServiceService` 객체를 만듭니다.

1. 바코드 데이터가 포함된 PDF 양식 가져오기

   * 생성자를 사용하여 `BLOB` 객체를 만듭니다. `BLOB` 개체는 바코드가 포함된 PDF 문서를 저장하는 데 사용됩니다.
   * 생성자를 호출하고 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 객체를 만듭니다.
   * `System.IO.FileStream` 객체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 객체의 `Length` 속성을 가져와 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 객체의 `Read` 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * 바이트 배열의 내용으로 `binaryData` 속성을 할당하여 `BLOB` 객체를 채웁니다.

1. PDF 양식의 데이터 디코딩

   `BarcodedFormsServiceService` 객체의 `decode` 메서드를 호출하고 다음 값을 전달하여 양식 데이터를 디코딩합니다.

   * PDF 양식이 포함된 `BLOB` 개체
   * PDF417 바코드를 디코딩할지 여부를 지정하는 `Boolean` 개체
   * 데이터 행렬 바코드를 디코딩할지 여부를 지정하는 `Boolean` 객체입니다.
   * QR 코드 바코드를 디코딩할지 여부를 지정하는 `Boolean` 객체입니다.
   * 코드 바코드를 디코딩할지 여부를 지정하는 `Boolean` 객체입니다.
   * 코드 128 바코드를 디코딩할지 여부를 지정하는 `Boolean` 객체입니다.
   * 코드 39 바코드를 디코딩할지 여부를 지정하는 `Bolean` 객체입니다.
   * EAN-13 바코드를 디코딩할지 여부를 지정하는 `Boolean` 객체입니다.
   * EAN-8 바코드를 디코딩할지 여부를 지정하는 `Boolean` 객체입니다.
   * 바코드에 사용된 문자 집합 인코딩 값을 지정하는 `CharSet` 열거형 값.

   `decode` 메서드는 디코딩된 양식 데이터를 포함하는 문자열 값을 반환합니다.

1. 데이터를 XML 데이터 소스로 변환

   디코딩된 데이터를 `BarcodedFormsServiceService` 개체의 `extractToXML` 메서드를 호출하고 다음 값을 전달하여 XDP 또는 XFDF 데이터로 변환합니다.

   * 디코딩된 데이터를 포함하는 문자열 값입니다(`decode` 메서드의 반환 값을 사용해야 함).
   * 줄 구분 기호를 지정하는 `Delimiter` 열거형 값입니다. `Delimiter.Carriage_Return`을 지정하는 것이 좋습니다.
   * 필드 구분 기호를 지정하는 `Delimiter` 열거형 값입니다. 예를 들어 `Delimiter.Tab`을 지정합니다.
   * 바코드 데이터를 XDP 또는 XFDF XML 데이터로 변환할지 여부를 지정하는 `XMLFormat` 열거형 값입니다. 예를 들어 데이터를 XDP 데이터로 변환하려면 `XMLFormat.XDP`을 지정합니다.

   >[!NOTE]
   >
   >줄 구분 기호 및 필드 구분 기호 매개 변수에 동일한 값을 지정하지 마십시오.

   `extractToXML` 메서드는 각 요소가 `BLOB` 인스턴스인 `Object` 배열을 반환합니다. 양식에 있는 각 바코드에 별도의 요소가 있습니다. 즉, 양식에 4개의 바코드가 있으면 반환된 `Object` 배열에 4개의 요소가 있습니다.

1. 디코딩된 데이터 처리

   * 생성자를 호출하고 보안 PDF 문서의 파일 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 객체를 만듭니다.
   * `encryptPDFUsingPassword` 메서드에서 반환된 `BLOB` 객체의 데이터 내용을 저장하는 바이트 배열을 만듭니다. `BLOB` 객체의 `binaryData` 데이터 멤버 값을 가져와 바이트 배열을 채웁니다.
   * 생성자를 호출하고 `System.IO.FileStream` 객체를 전달하여 `System.IO.BinaryWriter` 객체를 만듭니다.
   * `System.IO.BinaryWriter` 객체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 PDF 파일에 기록합니다.

**참고 항목**

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
