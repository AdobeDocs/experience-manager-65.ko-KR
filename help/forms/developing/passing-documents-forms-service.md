---
title: FormsService에 문서 전달
seo-title: FormsService에 문서 전달
description: 'null'
seo-description: 'null'
uuid: 841e97f3-ebb8-4340-81a9-b6db11f0ec82
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e23de3c3-f8a0-459f-801e-a0942fb1c6aa
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# Forms 서비스에 문서 전달 {#passing-documents-to-the-formsservice}

AEM Forms 서비스는 대화형 PDF 양식을 클라이언트 장치(일반적으로 웹 브라우저)에 렌더링하여 사용자의 정보를 수집합니다. 인터랙티브한 PDF 양식은 일반적으로 XDP 파일로 저장되고 Designer에서 작성된 양식 디자인을 기반으로 합니다. AEM Forms에서 양식 디자인이 포함된 `com.adobe.idp.Document` 개체를 Forms 서비스에 전달할 수 있습니다. 그런 다음 양식 서비스는 `com.adobe.idp.Document` 개체에 있는 양식 디자인을 렌더링합니다.

Forms 서비스에 개체를 전달하면 다른 서비스 작업에서 `com.adobe.idp.Document` `com.adobe.idp.Document` 인스턴스를 반환한다는 이점이 있습니다. 즉, 다른 서비스 작업에서 `com.adobe.idp.Document` 인스턴스를 가져와 렌더링할 수 있습니다. 예를 들어 다음 그림과 같이 XDP 파일이 이름이 지정된 컨텐츠 서비스(더 이상 사용되지 않음) 노드에 저장되어 `/Company Home/Form Designs`있다고 가정합니다.

Content Services(더 이상 사용되지 않음)에서 Loan.xdp를 프로그래밍 방식으로 검색하고 XDP 파일을 `com.adobe.idp.Document` 개체 내의 Forms 서비스로 전달할 수 있습니다.

>[!NOTE]
>
>양식 서비스에 대한 자세한 내용은 AEM Forms [에 대한 서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

## 단계 요약 {#summary-of-steps}

Content Services(더 이상 사용되지 않음)에서 얻은 문서를 Forms 서비스로 전달하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일 포함
1. 양식 및 문서 관리 클라이언트 API 개체를 만듭니다.
1. Content Services에서 양식 디자인을 검색합니다(더 이상 사용되지 않음).
1. 인터랙티브한 PDF 양식을 렌더링할 수 있습니다.
1. 양식 데이터 스트림으로 작업을 수행합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함합니다.

**양식 및 문서 관리 클라이언트 API 개체 만들기**

Forms 서비스 API 작업을 프로그래밍 방식으로 수행하려면 먼저 Forms 클라이언트 API 개체를 만듭니다. 또한 이 워크플로우는 Content Services(더 이상 사용되지 않음)에서 XDP 파일을 검색하므로 문서 관리 API 개체를 만듭니다.

**콘텐츠 서비스에서 양식 디자인 검색(더 이상 사용되지 않음)**

Java 또는 웹 서비스 API 파섹 XDP 파일은 `com.adobe.idp.Document` 인스턴스(또는 웹 서비스를 사용하는 경우 `BLOB` 인스턴스) 내에서 반환됩니다. 그런 다음 `com.adobe.idp.Document` 인스턴스를 양식 서비스로 전달할 수 있습니다.

**인터랙티브한 PDF 양식 렌더링**

대화형 양식을 렌더링하려면 Content Services(더 이상 사용되지 않음)에서 반환된 `com.adobe.idp.Document` 인스턴스를 Forms 서비스로 전달합니다.

>[!NOTE]
>
>양식 디자인이 `com.adobe.idp.Document` 들어 있는 Forms 서비스를 전달하면 됩니다. 양식 디자인이 포함된 개체를 `renderPDFForm2` 사용하여 `renderHTMLForm2` `com.adobe.idp.Document` 두 가지 새로운 메서드를 사용합니다.

**양식 데이터 스트림으로 작업 수행**

클라이언트 애플리케이션 유형에 따라 양식을 클라이언트 웹 브라우저에 작성하거나 양식을 PDF 파일로 저장할 수 있습니다. 웹 기반 응용 프로그램은 일반적으로 웹 브라우저에 양식을 씁니다. 그러나 데스크톱 응용 프로그램은 일반적으로 양식을 PDF 파일로 저장합니다.

**참고 항목**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API 빠른 시작](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

## Java API를 사용하여 Forms 서비스에 문서 전달 {#pass-documents-to-the-forms-service-using-the-java-api}

Forms 서비스 및 컨텐츠 서비스(더 이상 사용되지 않음) API(Java)를 사용하여 Content Services에서 얻은 문서를 전달합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-forms-client.jar 및 adobe-content-services-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. 양식 및 문서 관리 클라이언트 API 개체 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다. 연결 [속성](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)설정을 참조하십시오.
   * 생성자를 사용하여 객체를 전달하여 `FormsServiceClient` 객체를 만듭니다 `ServiceClientFactory` .
   * 생성자를 사용하여 객체를 전달하여 `DocumentManagementServiceClientImpl` 객체를 만듭니다 `ServiceClientFactory` .

1. 콘텐츠 서비스에서 양식 디자인 검색(더 이상 사용되지 않음)

   객체의 `DocumentManagementServiceClientImpl` `retrieveContent` 메서드를 호출하고 다음 값을 전달합니다.

   * 컨텐츠가 추가되는 스토어를 지정하는 문자열 값. 기본 스토어는 `SpacesStore`입니다. 이 값은 필수 매개 변수입니다.
   * 검색할 컨텐츠의 정규화된 경로(예: `/Company Home/Form Designs/Loan.xdp`)를 지정하는 문자열 값. 이 값은 필수 매개 변수입니다.
   * 버전을 지정하는 문자열 값입니다. 이 값은 선택적 매개 변수이며 빈 문자열을 전달할 수 있습니다. 이러한 경우 최신 버전이 검색됩니다.
   이 `retrieveContent` 메서드는 XDP 파일이 포함된 `CRCResult` 객체를 반환합니다. 객체의 `com.adobe.idp.Document` `CRCResult` `getDocument` 메서드를 호출하여 인스턴스를 가져옵니다.

1. 인터랙티브한 PDF 양식 렌더링

   객체의 `FormsServiceClient` `renderPDFForm2` 메서드를 호출하고 다음 값을 전달합니다.

   * Content Services에서 검색한 양식 디자인이 포함된 `com.adobe.idp.Document` 개체(더 이상 사용되지 않음)
   * 양식과 병합할 데이터가 들어 있는 `com.adobe.idp.Document` 개체입니다. 데이터를 병합하지 않으려면 빈 `com.adobe.idp.Document` 개체를 전달합니다.
   * 런타임 옵션을 저장하는 `PDFFormRenderSpec` 개체입니다. 이 값은 선택적 매개 변수이며 런타임 옵션을 지정하지 않으려는 `null` 경우 지정할 수 있습니다.
   * URI 값이 들어 있는 `URLSpec` 개체입니다. 이 값은 선택적 매개 변수이며 지정할 수 `null`있습니다.
   * 첨부 파일을 저장하는 `java.util.HashMap` 개체입니다. 이 값은 선택적 매개 변수이며 양식에 파일을 첨부하지 않으려는 `null` 경우 지정할 수 있습니다.
   이 `renderPDFForm` 메서드는 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림을 포함하는 `FormsResult` 개체를 반환합니다.

1. 양식 데이터 스트림으로 작업 수행

   * 개체 &#39;s `com.adobe.idp.Document` `FormsResult` `getOutputContent` 메서드를 호출하여 개체를 만듭니다.
   * 해당 `com.adobe.idp.Document` `getContentType` 메서드를 호출하여 개체의 콘텐츠 형식을 가져옵니다.
   * 해당 `javax.servlet.http.HttpServletResponse` 메서드를 호출하고 `setContentType` `com.adobe.idp.Document` 개체의 콘텐츠 형식을 전달하여 개체의 콘텐츠 형식을 설정합니다.
   * 개체의 `javax.servlet.ServletOutputStream` `javax.servlet.http.HttpServletResponse` `getOutputStream` 메서드를 호출하여 양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰는 데 사용되는 개체를 만듭니다.
   * 개체의 `java.io.InputStream` `com.adobe.idp.Document` `getInputStream` 메서드를 호출하여 개체를 만듭니다.
   * 바이트 배열을 만들고 `InputStream` 개체의 `read` 메서드를 호출하여 양식 데이터 스트림으로 채웁니다. 바이트 배열을 인수로 전달합니다.
   * 양식 데이터 스트림을 클라이언트 웹 브라우저로 전송하려면 `javax.servlet.ServletOutputStream` 개체의 `write` 메서드를 호출합니다. 바이트 배열을 `write` 메서드에 전달합니다.

**참고 항목**

[빠른 시작(SOAP 모드):Java API를 사용하여 Forms 서비스에 문서 전달](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API 파섹 {#pass-documents-to-the-forms-service-using-the-web-service-api}

Forms 서비스 및 컨텐츠 서비스(더 이상 사용되지 않음) API(웹 서비스)를 사용하여 Content Services에서 얻은 문서를 전달합니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 이 클라이언트 응용 프로그램은 두 개의 AEM Forms 서비스를 호출하므로 두 개의 서비스 참조를 만듭니다. Forms 서비스와 관련된 서비스 참조에 대해 다음 WSDL 정의를 사용합니다. `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`Adobe

   문서 관리 서비스와 관련된 서비스 참조에 대해 다음 WSDL 정의를 사용합니다. `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`Adobe

   데이터 `BLOB` 유형은 두 서비스 참조 모두에서 일반적이므로 데이터 유형을 사용할 때 해당 `BLOB` 데이터 유형을 완전히 분류합니다. 해당 웹 서비스 빠른 시작에서는 모든 `BLOB` 인스턴스가 정규화된 인스턴스입니다.

   >[!NOTE]
   >
   >AEM `localhost`Forms를 호스팅하는 서버의 IP 주소로 대체합니다.

1. 양식 및 문서 관리 클라이언트 API 개체 만들기

   * 기본 생성자를 사용하여 `FormsServiceClient` 객체를 만듭니다.
   * 생성자를 사용하여 `FormsServiceClient.Endpoint.Address` 객체를 만듭니다 `System.ServiceModel.EndpointAddress` . WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/FormsService?WSDL`). 속성을 사용할 필요는 `lc_version` 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * 필드의 값을 가져와 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다 `FormsServiceClient.Endpoint.Binding` . 반환 값을 로 `BasicHttpBinding`캐스팅합니다.
   * 개체 `System.ServiceModel.BasicHttpBinding` 필드를 로 설정합니다 `MessageEncoding` . `WSMessageEncoding.Mtom` 이 값을 사용하면 MTOM이 사용됩니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * AEM 양식 사용자 이름을 필드에 `FormsServiceClient.ClientCredentials.UserName.UserName`지정합니다.
      * 필드에 해당 암호 값을 지정합니다 `FormsServiceClient.ClientCredentials.UserName.Password`.
      * 필드에 상수 값을 `HttpClientCredentialType.Basic` 지정합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 필드에 상수 값을 `BasicHttpSecurityMode.TransportCredentialOnly` 지정합니다 `BasicHttpBindingSecurity.Security.Mode`.
   >[!NOTE]
   >
   >서비스 `DocumentManagementServiceClient`클라이언트에 대해 다음 단계를 반복합니다.

1. 콘텐츠 서비스에서 양식 디자인 검색(더 이상 사용되지 않음)

   객체의 `DocumentManagementServiceClient` `retrieveContent` 메서드를 호출하고 다음 값을 전달하여 컨텐츠를 검색합니다.

   * 컨텐츠가 추가되는 스토어를 지정하는 문자열 값. 기본 스토어는 `SpacesStore`입니다. 이 값은 필수 매개 변수입니다.
   * 검색할 컨텐츠의 정규화된 경로(예: `/Company Home/Form Designs/Loan.xdp`)를 지정하는 문자열 값. 이 값은 필수 매개 변수입니다.
   * 버전을 지정하는 문자열 값입니다. 이 값은 선택적 매개 변수이며 빈 문자열을 전달할 수 있습니다. 이러한 경우 최신 버전이 검색됩니다.
   * 검색 링크 값을 저장하는 문자열 출력 매개 변수입니다.
   * 컨텐츠를 저장하는 `BLOB` 출력 매개 변수입니다. 이 출력 매개 변수를 사용하여 컨텐츠를 검색할 수 있습니다.
   * 컨텐츠 속성을 저장하는 `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` 출력 매개 변수입니다.
   * 출력 `CRCResult` 매개 변수입니다. 이 객체를 사용하는 대신 `BLOB` 출력 매개 변수를 사용하여 컨텐츠를 가져올 수 있습니다.

1. 인터랙티브한 PDF 양식 렌더링

   객체의 `FormsServiceClient` `renderPDFForm2` 메서드를 호출하고 다음 값을 전달합니다.

   * Content Services에서 검색한 양식 디자인이 포함된 `BLOB` 개체(더 이상 사용되지 않음)
   * 양식과 병합할 데이터가 들어 있는 `BLOB` 개체입니다. 데이터를 병합하지 않으려면 빈 `BLOB` 개체를 전달합니다.
   * 런타임 옵션을 저장하는 `PDFFormRenderSpec` 개체입니다. 이 값은 선택적 매개 변수이며 런타임 옵션을 지정하지 않으려는 `null` 경우 지정할 수 있습니다.
   * URI 값이 들어 있는 `URLSpec` 개체입니다. 이 값은 선택적 매개 변수이며 지정할 수 `null`있습니다.
   * 첨부 파일을 저장하는 `Map` 개체입니다. 이 값은 선택적 매개 변수이며 양식에 파일을 첨부하지 않으려는 `null` 경우 지정할 수 있습니다.
   * 페이지 개수를 저장하는 데 사용되는 긴 출력 매개 변수입니다.
   * 로케일 값을 저장하는 데 사용되는 문자열 출력 매개 변수입니다.
   * 인터랙티브한 PDF 양식을 저장하는 데 사용되는 `FormsResult` 출력 매개 변수 `.`
   이 `renderPDFForm2` 메서드는 대화형 PDF 양식이 포함된 `FormsResult` 개체를 반환합니다.

1. 양식 데이터 스트림으로 작업 수행

   * 개체 `BLOB` `FormsResult` `outputContent` 필드의 값을 가져와 양식 데이터가 포함된 개체를 만듭니다.
   * 생성자를 호출하여 `System.IO.FileStream` 객체를 만듭니다. 대화형 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 개체에서 검색한 `BLOB` 개체의 내용을 저장하는 바이트 배열을 `FormsResult` 만듭니다. 개체 데이터 멤버의 값을 가져와 바이트 배열을 `BLOB` 채웁니다 `MTOM` .
   * 생성자를 호출하고 객체를 전달하여 `System.IO.BinaryWriter` `System.IO.FileStream` 객체를 만듭니다.
   * 개체의 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 PDF 파일에 씁니다. `System.IO.BinaryWriter` `Write`

**참고 항목**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
