---
title: FormsService에 문서 전달
seo-title: Passing Documents to the FormsService
description: 양식 디자인이 포함된 com.adobe.idp.Document 개체를 Forms 서비스에 전달합니다. Forms 서비스는 com.adobe.idp.Document 개체에 있는 양식 디자인을 렌더링합니다.
seo-description: Pass a com.adobe.idp.Document object that contains the form design to the Forms service. The Forms service renders the form design located in the com.adobe.idp.Document object.
uuid: 841e97f3-ebb8-4340-81a9-b6db11f0ec82
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e23de3c3-f8a0-459f-801e-a0942fb1c6aa
role: Developer
exl-id: 29c7ebda-407a-464b-a9db-054163f5b737
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1684'
ht-degree: 0%

---

# Forms 서비스에 문서 전달 {#passing-documents-to-the-formsservice}

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms용입니다.**

AEM Forms 서비스는 사용자 정보를 수집하기 위해 클라이언트 장치(일반적으로 웹 브라우저)에 대화형 PDF forms을 렌더링합니다. 대화형 PDF 양식은 일반적으로 XDP 파일로 저장되고 디자이너에서 만들어지는 양식 디자인을 기반으로 합니다. AEM Forms의 경우 `com.adobe.idp.Document` Forms 서비스에 대한 양식 디자인이 포함된 객체입니다. 그런 다음 Forms 서비스는 `com.adobe.idp.Document` 개체.

A를 전달하는 이점 `com.adobe.idp.Document` Forms 서비스에 대한 개체는 다른 서비스 작업이 `com.adobe.idp.Document` 인스턴스. 즉, `com.adobe.idp.Document` 다른 서비스 작업의 인스턴스를 렌더링하고 렌더링합니다. 예를 들어, XDP 파일이 라는 컨텐츠 서비스(더 이상 사용되지 않음) 노드에 저장된다고 가정합니다. `/Company Home/Form Designs`다음 그림과 같이,

컨텐츠 서비스(더 이상 사용되지 않음)에서 Loan.xdp를 프로그래밍 방식으로 검색하고, XDP 파일을 내의 Forms 서비스에 전달할 수 있습니다 `com.adobe.idp.Document` 개체.

>[!NOTE]
>
>Forms 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

## 단계 요약 {#summary-of-steps}

컨텐츠 서비스(더 이상 사용되지 않음)에서 가져온 문서를 Forms 서비스로 전달하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. Forms 및 Document Management 클라이언트 API 개체를 만듭니다.
1. Content Services에서 양식 디자인을 검색합니다(더 이상 사용되지 않음).
1. 대화형 PDF 양식을 렌더링합니다.
1. 양식 데이터 스트림으로 작업을 수행합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함하십시오. 웹 서비스를 사용하는 경우 프록시 파일을 포함하십시오.

**Forms 및 Document Management 클라이언트 API 개체 만들기**

Forms 서비스 API 작업을 프로그래밍 방식으로 수행하려면 먼저 Forms 클라이언트 API 개체를 만드십시오. 또한 이 워크플로우는 컨텐츠 서비스에서 XDP 파일을 검색하므로(더 이상 사용되지 않음) 문서 관리 API 개체를 만듭니다.

**컨텐츠 서비스에서 양식 디자인을 검색합니다(더 이상 사용되지 않음).**

Java 또는 웹 서비스 API를 사용하여 콘텐츠 서비스에서 XDP 파일을 검색합니다(더 이상 사용되지 않음). XDP 파일은 `com.adobe.idp.Document` 인스턴스(또는 `BLOB` 인스턴스(웹 서비스를 사용하는 경우) 그런 다음 를 전달할 수 있습니다 `com.adobe.idp.Document` 인스턴스를 Forms 서비스에 추가합니다.

**대화형 PDF 양식 렌더링**

대화형 양식을 렌더링하려면 `com.adobe.idp.Document` Content Services(더 이상 사용되지 않음)에서 Forms 서비스로 반환되는 인스턴스입니다.

>[!NOTE]
>
>다음 정보를 `com.adobe.idp.Document` 여기에는 Forms 서비스에 대한 양식 디자인이 포함되어 있습니다. 이름이 `renderPDFForm2` 및 `renderHTMLForm2` 동의 `com.adobe.idp.Document` 양식 디자인이 포함된 객체입니다.

**양식 데이터 스트림으로 작업 수행**

클라이언트 응용 프로그램 유형에 따라 양식을 클라이언트 웹 브라우저에 작성하거나 양식을 PDF 파일로 저장할 수 있습니다. 웹 기반 응용 프로그램은 일반적으로 웹 브라우저에 양식을 기록합니다. 그러나 데스크톱 응용 프로그램은 일반적으로 양식을 PDF 파일로 저장합니다.

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms 서비스 API 빠른 시작](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

## Java API를 사용하여 Forms 서비스에 문서를 전달합니다 {#pass-documents-to-the-forms-service-using-the-java-api}

Forms 서비스 및 컨텐츠 서비스(더 이상 사용되지 않음) API(Java)를 사용하여 컨텐츠 서비스(더 이상 사용되지 않음)에서 가져온 문서를 전달합니다.

1. 프로젝트 파일 포함

   adobe-forms-client.jar 및 adobe-contentservices-client.jar와 같은 클라이언트 JAR 파일을 Java 프로젝트의 클래스 경로에 포함합니다.

1. Forms 및 Document Management 클라이언트 API 개체 만들기

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 객체입니다. (자세한 내용은 [연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties))
   * 만들기 `FormsServiceClient` 생성자를 사용하여 객체를 전달하고 `ServiceClientFactory` 개체.
   * 만들기 `DocumentManagementServiceClientImpl` 생성자를 사용하여 객체를 전달하고 `ServiceClientFactory` 개체.

1. 컨텐츠 서비스에서 양식 디자인을 검색합니다(더 이상 사용되지 않음).

   를 호출합니다 `DocumentManagementServiceClientImpl` 개체 `retrieveContent` 메서드를 사용하여 다음 값을 전달합니다.

   * 컨텐츠가 추가되는 저장소를 지정하는 문자열 값입니다. 기본 저장소는 다음과 같습니다. `SpacesStore`. 이 값은 필수 매개 변수입니다.
   * 검색할 컨텐츠의 정규화된 경로를 지정하는 문자열 값(예: `/Company Home/Form Designs/Loan.xdp`). 이 값은 필수 매개 변수입니다.
   * 버전을 지정하는 문자열 값입니다. 이 값은 선택적 매개 변수이며 빈 문자열을 전달할 수 있습니다. 이 경우 최신 버전이 검색됩니다.

   다음 `retrieveContent` 메서드 반환 `CRCResult` xdp 파일이 포함된 객체입니다. 획득 `com.adobe.idp.Document` 인스턴스를 호출하여 `CRCResult` 개체 `getDocument` 메서드를 사용합니다.

1. 대화형 PDF 양식 렌더링

   를 호출합니다 `FormsServiceClient` 개체 `renderPDFForm2` 메서드를 사용하여 다음 값을 전달합니다.

   * A `com.adobe.idp.Document` Content Services에서 검색한 양식 디자인이 포함된 객체입니다(더 이상 사용되지 않음).
   * A `com.adobe.idp.Document` 폼과 병합할 데이터를 포함하는 개체입니다. 데이터를 병합하지 않으려면 빈 을 전달합니다 `com.adobe.idp.Document` 개체.
   * A `PDFFormRenderSpec` 런타임 옵션을 저장하는 개체입니다. 이 값은 선택적 매개 변수이며 `null` 런타임 옵션을 지정하지 않으려는 경우
   * A `URLSpec` URI 값을 포함하는 객체입니다. 이 값은 선택적 매개 변수이며 `null`.
   * A `java.util.HashMap` 첨부 파일을 저장하는 객체입니다. 이 값은 선택적 매개 변수이며 `null` 양식에 파일을 첨부하지 않으려면

   다음 `renderPDFForm` 메서드 반환 `FormsResult` 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림을 포함하는 객체입니다.

1. 양식 데이터 스트림으로 작업 수행

   * 만들기 `com.adobe.idp.Document` 객체를 호출하여 `FormsResult` 개체 `getOutputContent` 메서드를 사용합니다.
   * 의 콘텐츠 유형 가져오기 `com.adobe.idp.Document` 객체를 호출하여 `getContentType` 메서드를 사용합니다.
   * 설정 `javax.servlet.http.HttpServletResponse` 개체의 컨텐트 유형을 호출하여 `setContentType` 메서드 및 `com.adobe.idp.Document` 개체.
   * 만들기 `javax.servlet.ServletOutputStream` 를 호출하여 클라이언트 웹 브라우저에 양식 데이터 스트림을 작성하는 데 사용되는 개체 `javax.servlet.http.HttpServletResponse` 개체 `getOutputStream` 메서드를 사용합니다.
   * 만들기 `java.io.InputStream` 객체를 호출하여 `com.adobe.idp.Document` 개체 `getInputStream` 메서드를 사용합니다.
   * 바이트 배열을 만들고 을 호출하여 양식 데이터 스트림으로 채웁니다 `InputStream` 개체 `read` 메서드를 사용합니다. 바이트 배열을 인수로 전달합니다.
   * 를 호출합니다 `javax.servlet.ServletOutputStream` 개체 `write` 양식 데이터 스트림을 클라이언트 웹 브라우저로 보내는 방법입니다. 바이트 배열을 로 전달합니다. `write` 메서드를 사용합니다.

**추가 참조**

[빠른 시작(SOAP 모드): Java API를 사용하여 Forms 서비스에 문서 전달](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API를 사용하여 Forms 서비스에 문서를 전달합니다 {#pass-documents-to-the-forms-service-using-the-web-service-api}

Forms 서비스 및 콘텐츠 서비스(더 이상 사용되지 않음) API(웹 서비스)를 사용하여 콘텐츠 서비스에서 얻은 문서를 전달합니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 이 클라이언트 응용 프로그램은 두 개의 AEM Forms 서비스를 호출하므로 두 개의 서비스 참조를 만듭니다. Forms 서비스와 연결된 서비스 참조에 대해 다음 WSDL 정의를 사용하십시오. `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   문서 관리 서비스와 연결된 서비스 참조에 대해 다음 WSDL 정의를 사용하십시오. `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   왜냐하면 `BLOB` 데이터 유형은 두 서비스 참조에 공통으로, 완전히 분류됩니다 `BLOB` 데이터 유형을 사용합니다. 해당 웹 서비스 빠른 시작에서 모두 `BLOB` 인스턴스는 완전히 검증됩니다.

   >[!NOTE]
   >
   >바꾸기 `localhost`(AEM Forms을 호스팅하는 서버의 IP 주소 사용)

1. Forms 및 Document Management 클라이언트 API 개체 만들기

   * 만들기 `FormsServiceClient` 기본 생성자를 사용하여 개체를 만듭니다.
   * 만들기 `FormsServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/FormsService?WSDL`). 를 사용할 필요가 없습니다 `lc_version` 속성을 사용합니다. 이 속성은 서비스 참조를 생성할 때 사용됩니다.)
   * 만들기 `System.ServiceModel.BasicHttpBinding` 개체의 값을 가져와서 `FormsServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스팅합니다. `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름을 지정합니다 `FormsServiceClient.ClientCredentials.UserName.UserName`.
      * 필드에 해당 암호 값을 지정합니다 `FormsServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 할당 `HttpClientCredentialType.Basic` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 상수 값 할당 `BasicHttpSecurityMode.TransportCredentialOnly` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >에 대해 다음 단계를 반복합니다 `DocumentManagementServiceClient`서비스 클라이언트.

1. 컨텐츠 서비스에서 양식 디자인을 검색합니다(더 이상 사용되지 않음).

   를 호출하여 컨텐츠를 검색합니다. `DocumentManagementServiceClient` 개체 `retrieveContent` 메서드 및 다음 값 전달:

   * 컨텐츠가 추가되는 저장소를 지정하는 문자열 값입니다. 기본 저장소는 다음과 같습니다. `SpacesStore`. 이 값은 필수 매개 변수입니다.
   * 검색할 컨텐츠의 정규화된 경로를 지정하는 문자열 값(예: `/Company Home/Form Designs/Loan.xdp`). 이 값은 필수 매개 변수입니다.
   * 버전을 지정하는 문자열 값입니다. 이 값은 선택적 매개 변수이며 빈 문자열을 전달할 수 있습니다. 이 경우 최신 버전이 검색됩니다.
   * 찾아보기 링크 값을 저장하는 문자열 출력 매개 변수입니다.
   * A `BLOB` 컨텐츠를 저장하는 출력 매개 변수입니다. 이 출력 매개 변수를 사용하여 컨텐츠를 검색할 수 있습니다.
   * A `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` 컨텐츠 속성을 저장하는 출력 매개 변수입니다.
   * A `CRCResult` 출력 매개 변수. 이 개체를 사용하는 대신 `BLOB` 컨텐츠를 가져올 출력 매개 변수입니다.

1. 대화형 PDF 양식 렌더링

   를 호출합니다 `FormsServiceClient` 개체 `renderPDFForm2` 메서드를 사용하여 다음 값을 전달합니다.

   * A `BLOB` Content Services에서 검색한 양식 디자인이 포함된 객체입니다(더 이상 사용되지 않음).
   * A `BLOB` 폼과 병합할 데이터를 포함하는 개체입니다. 데이터를 병합하지 않으려면 빈 을 전달합니다 `BLOB` 개체.
   * A `PDFFormRenderSpec` 런타임 옵션을 저장하는 개체입니다. 이 값은 선택적 매개 변수이며 `null` 런타임 옵션을 지정하지 않으려는 경우
   * A `URLSpec` URI 값을 포함하는 객체입니다. 이 값은 선택적 매개 변수이며 `null`.
   * A `Map` 첨부 파일을 저장하는 객체입니다. 이 값은 선택적 매개 변수이며 `null` 양식에 파일을 첨부하지 않으려면
   * 페이지 수를 저장하는 데 사용되는 긴 출력 매개 변수입니다.
   * 로케일 값을 저장하는 데 사용되는 문자열 출력 매개 변수입니다.
   * A `FormsResult` 상호 PDF 양식을 저장하는 데 사용되는 출력 매개 변수 `.`

   다음 `renderPDFForm2` 메서드 반환 `FormsResult` 대화형 PDF 양식을 포함하는 개체입니다.

1. 양식 데이터 스트림으로 작업 수행

   * 만들기 `BLOB` 의 값을 가져와서 양식 데이터를 포함하는 개체 `FormsResult` 개체 `outputContent` 필드.
   * 만들기 `System.IO.FileStream` 개체를 생성자로 호출하여 개체를 가져옵니다. 대화형 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 내용을 저장하는 바이트 배열을 만듭니다 `BLOB` 개체에서 검색된 개체 `FormsResult` 개체. 의 값을 가져와서 바이트 배열을 채웁니다 `BLOB` 개체 `MTOM` 데이터 멤버.
   * 만들기 `System.IO.BinaryWriter` 생성자를 호출하고 전달하여 개체를 `System.IO.FileStream` 개체.
   * 를 호출하여 PDF 파일에 바이트 배열의 내용을 씁니다. `System.IO.BinaryWriter` 개체 `Write` 메서드를 사용하여 바이트 배열을 전달합니다.

**추가 참조**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
