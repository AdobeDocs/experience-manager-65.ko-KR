---
title: FormsService에 문서 전달
seo-title: FormsService에 문서 전달
description: '양식 디자인이 포함된 com.adobe.idp.Document 개체를 Forms 서비스로 전달합니다. Forms 서비스는 com.adobe.idp.Document 개체에 있는 양식 디자인을 렌더링합니다. '
seo-description: 양식 디자인이 포함된 com.adobe.idp.Document 개체를 Forms 서비스로 전달합니다. Forms 서비스는 com.adobe.idp.Document 개체에 있는 양식 디자인을 렌더링합니다.
uuid: 841e97f3-ebb8-4340-81a9-b6db11f0ec82
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e23de3c3-f8a0-459f-801e-a0942fb1c6aa
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '1714'
ht-degree: 0%

---


# Forms 서비스 {#passing-documents-to-the-formsservice}에 문서 전달

**이 문서의 샘플과 예는 JEE 환경의 AEM Forms에만 해당됩니다.**

AEM Forms 서비스는 대화형 PDF forms을 클라이언트 장치(일반적으로 웹 브라우저)에 렌더링하여 사용자의 정보를 수집합니다. 인터랙티브한 PDF 양식은 일반적으로 XDP 파일로 저장되고 Designer에서 작성된 양식 디자인을 기반으로 합니다. AEM Forms의 경우 양식 디자인이 포함된 `com.adobe.idp.Document` 개체를 Forms 서비스에 전달할 수 있습니다. 그런 다음 Forms 서비스는 `com.adobe.idp.Document` 개체에 있는 양식 디자인을 렌더링합니다.

Forms 서비스에 `com.adobe.idp.Document` 개체를 전달하면 다른 서비스 작업에서 `com.adobe.idp.Document` 인스턴스를 반환한다는 이점이 있습니다. 즉, 다른 서비스 작업에서 `com.adobe.idp.Document` 인스턴스를 가져와 렌더링할 수 있습니다. 예를 들어, 다음 그림에서와 같이 XDP 파일이 `/Company Home/Form Designs`이라는 컨텐트 서비스(더 이상 사용되지 않음) 노드에 저장되어 있다고 가정합니다.

콘텐츠 서비스에서 Loan.xdp(더 이상 사용되지 않음)를 프로그래밍 방식으로 검색하고 XDP 파일을 `com.adobe.idp.Document` 개체 내에서 Forms 서비스에 전달할 수 있습니다.

>[!NOTE]
>
>Forms 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

## {#summary-of-steps} 단계 요약

컨텐트 서비스에서 얻은 문서(더 이상 사용되지 않음)를 Forms 서비스로 전달하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일 포함
1. Forms 및 Document Management Client API 객체를 만듭니다.
1. 콘텐츠 서비스에서 양식 디자인을 검색합니다(더 이상 사용되지 않음).
1. 인터랙티브한 PDF 양식을 렌더링합니다.
1. 양식 데이터 스트림으로 작업을 수행합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함하십시오.

**Forms 및 Document Management Client API 객체 만들기**

Forms 서비스 API 작업을 프로그래밍 방식으로 수행하려면 먼저 Forms Client API 개체를 만듭니다. 또한 이 워크플로우는 콘텐츠 서비스에서 XDP 파일을 검색하므로(더 이상 사용되지 않음) 문서 관리 API 객체를 만듭니다.

**콘텐츠 서비스에서 양식 디자인 검색(더 이상 사용되지 않음)**

Java 또는 웹 서비스 API를 사용하여 콘텐츠 서비스에서 XDP 파일을 검색합니다(더 이상 사용되지 않음). XDP 파일은 `com.adobe.idp.Document` 인스턴스 내에서 반환되거나 웹 서비스를 사용하는 경우 `BLOB` 인스턴스 내에서 반환됩니다. 그런 다음 `com.adobe.idp.Document` 인스턴스를 Forms 서비스에 전달할 수 있습니다.

**인터랙티브한 PDF 양식 렌더링**

대화형 양식을 렌더링하려면 컨텐트 서비스에서 반환된 `com.adobe.idp.Document` 인스턴스(더 이상 사용되지 않음)를 Forms 서비스로 전달합니다.

>[!NOTE]
>
>양식 디자인이 포함된 `com.adobe.idp.Document`을 Forms 서비스에 전달할 수 있습니다. `renderPDFForm2` 및 `renderHTMLForm2`이라는 이름의 새 두 메서드는 양식 디자인을 포함하는 `com.adobe.idp.Document` 객체를 허용합니다.

**양식 데이터 스트림으로 작업 수행**

클라이언트 응용 프로그램 유형에 따라 양식을 클라이언트 웹 브라우저에 작성하거나 양식을 PDF 파일로 저장할 수 있습니다. 웹 기반 응용 프로그램은 일반적으로 웹 브라우저에 양식을 씁니다. 그러나 데스크톱 응용 프로그램은 일반적으로 양식을 PDF 파일로 저장합니다.

**참고 항목**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms 서비스 API 빠른 시작](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

## Java API {#pass-documents-to-the-forms-service-using-the-java-api}를 사용하여 Forms 서비스에 문서 전달

Forms 서비스 및 컨텐트 서비스(더 이상 사용되지 않음) API(Java)를 사용하여 컨텐트 서비스에서 얻은 문서를 전달합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-forms-client.jar 및 adobe-contentservices-client.jar 등의 클라이언트 JAR 파일을 포함합니다.

1. Forms 및 Document Management Client API 객체 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다. ([연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)을 참조하십시오.)
   * 생성자를 사용하여 `FormsServiceClient` 개체를 만들고 `ServiceClientFactory` 개체를 전달합니다.
   * 생성자를 사용하여 `DocumentManagementServiceClientImpl` 개체를 만들고 `ServiceClientFactory` 개체를 전달합니다.

1. 콘텐츠 서비스에서 양식 디자인 검색(더 이상 사용되지 않음)

   `DocumentManagementServiceClientImpl` 객체의 `retrieveContent` 메서드를 호출하고 다음 값을 전달합니다.

   * 콘텐트가 추가되는 저장소를 지정하는 문자열 값입니다. 기본 스토어는 `SpacesStore`입니다. 이 값은 필수 매개 변수입니다.
   * 검색할 컨텐츠의 정규화된 경로를 지정하는 문자열 값(예: `/Company Home/Form Designs/Loan.xdp`). 이 값은 필수 매개 변수입니다.
   * 버전을 지정하는 문자열 값입니다. 이 값은 선택적 매개 변수이며 빈 문자열을 전달할 수 있습니다. 이 경우 최신 버전이 검색됩니다.

   `retrieveContent` 메서드는 XDP 파일을 포함하는 `CRCResult` 객체를 반환합니다. `CRCResult` 객체의 `getDocument` 메서드를 호출하여 `com.adobe.idp.Document` 인스턴스를 가져옵니다.

1. 인터랙티브한 PDF 양식 렌더링

   `FormsServiceClient` 객체의 `renderPDFForm2` 메서드를 호출하고 다음 값을 전달합니다.

   * 콘텐츠 서비스에서 검색된 양식 디자인을 포함하는 `com.adobe.idp.Document` 개체(더 이상 사용되지 않음).
   * 양식과 병합할 데이터가 포함된 `com.adobe.idp.Document` 개체 데이터를 병합하지 않으려면 빈 `com.adobe.idp.Document` 개체를 전달합니다.
   * 런타임 옵션을 저장하는 `PDFFormRenderSpec` 객체입니다. 이 값은 선택적 매개 변수이며 런타임 옵션을 지정하지 않으려면 `null`을 지정할 수 있습니다.
   * URI 값이 포함된 `URLSpec` 객체입니다. 이 값은 선택적 매개 변수이며 `null`을 지정할 수 있습니다.
   * 첨부 파일을 저장하는 `java.util.HashMap` 객체입니다. 이 값은 선택적 매개 변수입니다. 양식을 첨부하지 않으려면 `null`을 지정할 수 있습니다.

   `renderPDFForm` 메서드는 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림을 포함하는 `FormsResult` 객체를 반환합니다.

1. 양식 데이터 스트림으로 작업 수행

   * `FormsResult` 개체 &#39;s `getOutputContent` 메서드를 호출하여 `com.adobe.idp.Document` 개체를 만듭니다.
   * `getContentType` 메서드를 호출하여 `com.adobe.idp.Document` 객체의 내용 유형을 가져옵니다.
   * `setContentType` 메서드를 호출하고 `com.adobe.idp.Document` 개체의 내용 유형을 전달하여 `javax.servlet.http.HttpServletResponse` 개체의 내용 유형을 설정합니다.
   * `javax.servlet.http.HttpServletResponse` 개체의 `getOutputStream` 메서드를 호출하여 양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰는 데 사용되는 `javax.servlet.ServletOutputStream` 개체를 만듭니다.
   * `com.adobe.idp.Document` 객체의 `getInputStream` 메서드를 호출하여 `java.io.InputStream` 객체를 만듭니다.
   * 바이트 배열을 만들고 `InputStream` 객체의 `read` 메서드를 호출하여 양식 데이터 스트림으로 채웁니다. 바이트 배열을 인수로 전달합니다.
   * 양식 데이터 스트림을 클라이언트 웹 브라우저에 보내려면 `javax.servlet.ServletOutputStream` 객체의 `write` 메서드를 호출합니다. 바이트 배열을 `write` 메서드에 전달합니다.

**참고 항목**

[빠른 시작(SOAP 모드):Java API를 사용하여 Forms 서비스로 문서 전달](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API {#pass-documents-to-the-forms-service-using-the-web-service-api}를 사용하여 문서를 Forms 서비스로 전달

Forms 서비스 및 컨텐트 서비스(더 이상 사용되지 않음) API(웹 서비스)를 사용하여 컨텐트 서비스에서 얻은 문서를 전달합니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 이 클라이언트 응용 프로그램은 2개의 AEM Forms 서비스를 호출하므로 2개의 서비스 참조를 만듭니다. Forms 서비스와 연관된 서비스 참조에 대해 다음 WSDL 정의를 사용합니다.`http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   Document Management 서비스와 연결된 서비스 참조에 대해 다음 WSDL 정의를 사용합니다.`http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   `BLOB` 데이터 유형은 두 서비스 참조 모두에 공통이므로 사용 시 `BLOB` 데이터 유형을 완전히 확인합니다. 해당 웹 서비스 빠른 시작에서 모든 `BLOB` 인스턴스는 정규화된 인스턴스입니다.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꿉니다.

1. Forms 및 Document Management Client API 객체 만들기

   * 기본 생성자를 사용하여 `FormsServiceClient` 객체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `FormsServiceClient.Endpoint.Address` 객체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스(예: `http://localhost:8080/soap/services/FormsService?WSDL`)에 전달합니다. `lc_version` 특성을 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * `FormsServiceClient.Endpoint.Binding` 필드의 값을 가져와서 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`으로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`로 설정합니다. 이 값을 사용하면 MTOM이 사용됩니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * AEM 양식 사용자 이름을 `FormsServiceClient.ClientCredentials.UserName.UserName` 필드에 지정합니다.
      * 해당 암호 값을 `FormsServiceClient.ClientCredentials.UserName.Password` 필드에 지정합니다.
      * `BasicHttpBindingSecurity.Transport.ClientCredentialType` 필드에 상수 값 `HttpClientCredentialType.Basic`을 할당합니다.
   * `BasicHttpBindingSecurity.Security.Mode` 필드에 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을 할당합니다.

   >[!NOTE]
   >
   >`DocumentManagementServiceClient`서비스 클라이언트에 대해 이 단계를 반복합니다.

1. 콘텐츠 서비스에서 양식 디자인 검색(더 이상 사용되지 않음)

   `DocumentManagementServiceClient` 객체의 `retrieveContent` 메서드를 호출하고 다음 값을 전달하여 내용을 검색합니다.

   * 콘텐트가 추가되는 저장소를 지정하는 문자열 값입니다. 기본 스토어는 `SpacesStore`입니다. 이 값은 필수 매개 변수입니다.
   * 검색할 컨텐츠의 정규화된 경로를 지정하는 문자열 값(예: `/Company Home/Form Designs/Loan.xdp`). 이 값은 필수 매개 변수입니다.
   * 버전을 지정하는 문자열 값입니다. 이 값은 선택적 매개 변수이며 빈 문자열을 전달할 수 있습니다. 이 경우 최신 버전이 검색됩니다.
   * 검색 링크 값을 저장하는 문자열 출력 매개 변수입니다.
   * 내용을 저장하는 `BLOB` 출력 매개 변수입니다. 이 출력 매개 변수를 사용하여 내용을 검색할 수 있습니다.
   * 내용 특성을 저장하는 `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` 출력 매개 변수입니다.
   * `CRCResult` 출력 매개 변수입니다. 이 객체를 사용하는 대신 `BLOB` 출력 매개 변수를 사용하여 컨텐츠를 가져올 수 있습니다.

1. 인터랙티브한 PDF 양식 렌더링

   `FormsServiceClient` 객체의 `renderPDFForm2` 메서드를 호출하고 다음 값을 전달합니다.

   * 콘텐츠 서비스에서 검색된 양식 디자인을 포함하는 `BLOB` 개체(더 이상 사용되지 않음).
   * 양식과 병합할 데이터가 포함된 `BLOB` 개체 데이터를 병합하지 않으려면 빈 `BLOB` 개체를 전달합니다.
   * 런타임 옵션을 저장하는 `PDFFormRenderSpec` 객체입니다. 이 값은 선택적 매개 변수이며 런타임 옵션을 지정하지 않으려면 `null`을 지정할 수 있습니다.
   * URI 값이 포함된 `URLSpec` 객체입니다. 이 값은 선택적 매개 변수이며 `null`을 지정할 수 있습니다.
   * 첨부 파일을 저장하는 `Map` 객체입니다. 이 값은 선택적 매개 변수입니다. 양식을 첨부하지 않으려면 `null`을 지정할 수 있습니다.
   * 페이지 수를 저장하는 데 사용되는 긴 출력 매개 변수입니다.
   * 로케일 값을 저장하는 데 사용되는 문자열 출력 매개 변수입니다.
   * 대화형 PDF 양식 `.`을 저장하는 데 사용되는 `FormsResult` 출력 매개 변수

   `renderPDFForm2` 메서드는 대화형 PDF 양식이 포함된 `FormsResult` 개체를 반환합니다.

1. 양식 데이터 스트림으로 작업 수행

   * `FormsResult` 개체의 `outputContent` 필드의 값을 가져와서 양식 데이터를 포함하는 `BLOB` 개체를 만듭니다.
   * 생성자를 호출하여 `System.IO.FileStream` 객체를 만듭니다. 대화형 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * `FormsResult` 개체에서 검색한 `BLOB` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `BLOB` 객체의 `MTOM` 데이터 멤버 값을 가져와 바이트 배열을 채웁니다.
   * 생성자를 호출하고 `System.IO.FileStream` 객체를 전달하여 `System.IO.BinaryWriter` 객체를 만듭니다.
   * `System.IO.BinaryWriter` 객체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 PDF 파일에 기록합니다.

**참고 항목**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
