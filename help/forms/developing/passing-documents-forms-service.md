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

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms에 대해서만 적용됩니다.**

AEM Forms 서비스는 대화형 PDF forms을 클라이언트 장치(일반적으로 웹 브라우저)로 렌더링하여 사용자로부터 정보를 수집합니다. 대화형 PDF 양식은 일반적으로 XDP 파일로 저장되고 디자이너에서 만들어지는 양식 디자인을 기반으로 합니다. AEM Forms에서 를 전달할 수 있습니다. `com.adobe.idp.Document` Forms 서비스에 대한 양식 디자인이 포함된 객체입니다. 그런 다음 Forms 서비스는에 있는 양식 디자인을 렌더링합니다. `com.adobe.idp.Document` 개체.

를 전달할 때의 이점 `com.adobe.idp.Document` Forms 서비스의 개체는 다른 서비스 작업에서 `com.adobe.idp.Document` 인스턴스. 즉, 다음을 얻을 수 있습니다. `com.adobe.idp.Document` 다른 서비스 작업의 인스턴스를 렌더링합니다. 예를 들어 XDP 파일이 Content Services(더 이상 사용되지 않음) 노드에 저장되어 있다고 가정해 보겠습니다 `/Company Home/Form Designs`다음 그림과 같이 을 참조하십시오.

Content Services(더 이상 사용되지 않음)에서 Loan.xdp를 프로그래밍 방식으로 검색하고 XDP 파일을 내에서 Forms 서비스로 전달할 수 있습니다. `com.adobe.idp.Document` 개체.

>[!NOTE]
>
>Forms 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

## 단계 요약 {#summary-of-steps}

Content Services(더 이상 사용되지 않음)에서 가져온 문서를 Forms 서비스로 전달하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. Forms 및 Document Management 클라이언트 API 개체를 만듭니다.
1. 콘텐츠 서비스에서 양식 디자인을 검색합니다(더 이상 사용되지 않음).
1. 대화형 PDF 양식을 렌더링합니다.
1. 양식 데이터 스트림으로 작업을 수행합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함합니다.

**Forms 및 Document Management 클라이언트 API 개체 만들기**

Forms 서비스 API 작업을 프로그래밍 방식으로 수행하려면 먼저 Forms 클라이언트 API 개체를 만듭니다. 또한 이 워크플로우는 콘텐츠 서비스에서 XDP 파일을 검색하므로(더 이상 사용되지 않음) 문서 관리 API 개체를 만듭니다.

**컨텐츠 서비스에서 양식 디자인 검색(더 이상 사용되지 않음)**

Java 또는 웹 서비스 API를 사용하여 콘텐츠 서비스에서 XDP 파일을 검색합니다(더 이상 사용되지 않음). XDP 파일이 `com.adobe.idp.Document` 인스턴스(또는 a `BLOB` 웹 서비스를 사용하는 경우의 인스턴스). 그런 다음 를 전달할 수 있습니다. `com.adobe.idp.Document` Forms 서비스에 대한 인스턴스입니다.

**대화형 PDF 양식 렌더링**

대화형 양식을 렌더링하려면 `com.adobe.idp.Document` 콘텐츠 서비스(더 이상 사용되지 않음)에서 Forms 서비스로 반환된 인스턴스.

>[!NOTE]
>
>다음을 전달할 수 있습니다. `com.adobe.idp.Document` Forms 서비스에 대한 양식 디자인이 포함되어 있습니다. 이름이 인 두 개의 새 메서드 `renderPDFForm2` 및 `renderHTMLForm2` 수락 `com.adobe.idp.Document` 폼 디자인이 포함된 개체입니다.

**양식 데이터 스트림으로 작업 수행**

클라이언트 응용 프로그램의 유형에 따라 클라이언트 웹 브라우저에 양식을 작성하거나 양식을 PDF 파일로 저장할 수 있습니다. 웹 기반 응용 프로그램은 일반적으로 웹 브라우저에 양식을 기록합니다. 그러나 데스크톱 응용 프로그램은 일반적으로 양식을 PDF 파일로 저장합니다.

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms 서비스 API 빠른 시작](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

## Java API를 사용하여 Forms 서비스에 문서 전달 {#pass-documents-to-the-forms-service-using-the-java-api}

Forms 서비스 및 콘텐츠 서비스(더 이상 사용되지 않음) API(Java)를 사용하여 콘텐츠 서비스(더 이상 사용되지 않음)에서 가져온 문서를 전달합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-forms-client.jar 및 adobe-contentservices-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. Forms 및 Document Management 클라이언트 API 개체 만들기

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다. (참조: [연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * 만들기 `FormsServiceClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체.
   * 만들기 `DocumentManagementServiceClientImpl` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체.

1. 컨텐츠 서비스에서 양식 디자인 검색(더 이상 사용되지 않음)

   호출 `DocumentManagementServiceClientImpl` 개체 `retrieveContent` 메서드를 실행하고 다음 값을 전달합니다.

   * 콘텐츠가 추가되는 저장소를 지정하는 문자열 값입니다. 기본 저장소는 입니다. `SpacesStore`. 이 값은 필수 매개 변수입니다.
   * 검색할 콘텐츠의 정규화된 경로를 지정하는 문자열 값(예: `/Company Home/Form Designs/Loan.xdp`). 이 값은 필수 매개 변수입니다.
   * 버전을 지정하는 문자열 값입니다. 이 값은 선택적 매개 변수이며 빈 문자열을 전달할 수 있습니다. 이 경우 최신 버전이 검색됩니다.

   다음 `retrieveContent` 메서드가 을 반환합니다. `CRCResult` xdp 파일이 포함된 개체입니다. 획득 `com.adobe.idp.Document` 를 호출하여 인스턴스 `CRCResult` 개체 `getDocument` 메서드를 사용합니다.

1. 대화형 PDF 양식 렌더링

   호출 `FormsServiceClient` 개체 `renderPDFForm2` 메서드를 실행하고 다음 값을 전달합니다.

   * A `com.adobe.idp.Document` content Services에서 검색한 양식 디자인이 포함된 개체입니다(더 이상 사용되지 않음).
   * A `com.adobe.idp.Document` 양식과 병합할 데이터가 포함된 개체입니다. 데이터를 병합하지 않으려면 비워 둡니다. `com.adobe.idp.Document` 개체.
   * A `PDFFormRenderSpec` 런타임 옵션을 저장하는 개체입니다. 이 값은 선택적 매개 변수이며 다음을 지정할 수 있습니다 `null` 런타임 옵션을 지정하지 않으려는 경우
   * A `URLSpec` URI 값이 포함된 개체입니다. 이 값은 선택적 매개 변수이며 다음을 지정할 수 있습니다 `null`.
   * A `java.util.HashMap` 첨부 파일을 저장하는 객체입니다. 이 값은 선택적 매개 변수이며 다음을 지정할 수 있습니다 `null` 양식에 파일을 첨부하지 않으려면.

   다음 `renderPDFForm` 메서드가 을 반환합니다. `FormsResult` 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림이 포함된 개체입니다.

1. 양식 데이터 스트림으로 작업 수행

   * 만들기 `com.adobe.idp.Document` 를 호출하여 개체 `FormsResult` 개체 &#39;s `getOutputContent` 메서드를 사용합니다.
   * 의 콘텐츠 유형 가져오기 `com.adobe.idp.Document` 개체 `getContentType` 메서드를 사용합니다.
   * 설정 `javax.servlet.http.HttpServletResponse` 를 호출하여 객체의 콘텐츠 유형 `setContentType` 메서드와 의 콘텐츠 유형 전달 `com.adobe.idp.Document` 개체.
   * 만들기 `javax.servlet.ServletOutputStream` 개체를 사용하여 클라이언트 웹 브라우저에서 `javax.servlet.http.HttpServletResponse` 개체 `getOutputStream` 메서드를 사용합니다.
   * 만들기 `java.io.InputStream` 를 호출하여 개체 `com.adobe.idp.Document` 개체 `getInputStream` 메서드를 사용합니다.
   * 바이트 배열을 만들고 `InputStream` 개체 `read` 메서드를 사용합니다. 바이트 배열을 인수로 전달합니다.
   * 호출 `javax.servlet.ServletOutputStream` 개체 `write` 클라이언트 웹 브라우저에 양식 데이터 스트림을 전송하는 방법입니다. 바이트 배열을 로 전달 `write` 메서드를 사용합니다.

**추가 참조**

[빠른 시작(SOAP 모드): Java API를 사용하여 Forms 서비스에 문서 전달](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API를 사용하여 Forms 서비스에 문서 전달 {#pass-documents-to-the-forms-service-using-the-web-service-api}

Forms 서비스 및 Content Services(더 이상 사용되지 않음) API(웹 서비스)를 사용하여 Content Services(더 이상 사용되지 않음)에서 가져온 문서를 전달합니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 이 클라이언트 애플리케이션은 두 개의 AEM Forms 서비스를 호출하므로 두 개의 서비스 참조를 생성합니다. Forms 서비스와 연관된 서비스 참조에 대해 다음 WSDL 정의를 사용합니다. `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   문서 관리 서비스와 연관된 서비스 참조에 대해 다음 WSDL 정의를 사용합니다. `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   이유: `BLOB` 데이터 유형은 두 서비스 참조에 모두 공통적이므로 `BLOB` 데이터 유형(사용 시) 해당 웹 서비스 빠른 시작에서 모두 `BLOB` 인스턴스가 정규화된 상태입니다.

   >[!NOTE]
   >
   >바꾸기 `localhost`AEM Forms을 호스팅하는 서버의 IP 주소입니다.

1. Forms 및 Document Management 클라이언트 API 개체 만들기

   * 만들기 `FormsServiceClient` 기본 생성자를 사용하여 개체를 작성합니다.
   * 만들기 `FormsServiceClient.Endpoint.Address` 을 사용하여 개체 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/FormsService?WSDL`). 를 사용할 필요가 없습니다. `lc_version` 특성. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * 만들기 `System.ServiceModel.BasicHttpBinding` 의 값을 가져와서 개체 `FormsServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스트 `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름 할당 `FormsServiceClient.ClientCredentials.UserName.UserName`.
      * 해당 암호 값을 필드에 할당합니다. `FormsServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 지정 `HttpClientCredentialType.Basic` 필드에 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 상수 값 지정 `BasicHttpSecurityMode.TransportCredentialOnly` 필드에 `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >다음 단계를 반복합니다. `DocumentManagementServiceClient`서비스 클라이언트.

1. 컨텐츠 서비스에서 양식 디자인 검색(더 이상 사용되지 않음)

   를 호출하여 콘텐츠 검색 `DocumentManagementServiceClient` 개체 `retrieveContent` 메서드 및 다음 값 전달:

   * 콘텐츠가 추가되는 저장소를 지정하는 문자열 값입니다. 기본 저장소는 입니다. `SpacesStore`. 이 값은 필수 매개 변수입니다.
   * 검색할 콘텐츠의 정규화된 경로를 지정하는 문자열 값(예: `/Company Home/Form Designs/Loan.xdp`). 이 값은 필수 매개 변수입니다.
   * 버전을 지정하는 문자열 값입니다. 이 값은 선택적 매개 변수이며 빈 문자열을 전달할 수 있습니다. 이 경우 최신 버전이 검색됩니다.
   * 찾아보기 링크 값을 저장하는 문자열 출력 매개 변수입니다.
   * A `BLOB` 컨텐츠를 저장하는 출력 매개 변수입니다. 이 출력 매개 변수를 사용하여 콘텐츠를 검색할 수 있습니다.
   * A `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` 컨텐츠 속성을 저장하는 출력 매개 변수.
   * A `CRCResult` 출력 매개 변수. 이 개체를 사용하는 대신 `BLOB` 컨텐츠를 얻기 위한 출력 매개 변수입니다.

1. 대화형 PDF 양식 렌더링

   호출 `FormsServiceClient` 개체 `renderPDFForm2` 메서드를 실행하고 다음 값을 전달합니다.

   * A `BLOB` content Services에서 검색한 양식 디자인이 포함된 개체입니다(더 이상 사용되지 않음).
   * A `BLOB` 양식과 병합할 데이터가 포함된 개체입니다. 데이터를 병합하지 않으려면 비워 둡니다. `BLOB` 개체.
   * A `PDFFormRenderSpec` 런타임 옵션을 저장하는 개체입니다. 이 값은 선택적 매개 변수이며 다음을 지정할 수 있습니다 `null` 런타임 옵션을 지정하지 않으려는 경우
   * A `URLSpec` URI 값이 포함된 개체입니다. 이 값은 선택적 매개 변수이며 다음을 지정할 수 있습니다 `null`.
   * A `Map` 첨부 파일을 저장하는 객체입니다. 이 값은 선택적 매개 변수이며 다음을 지정할 수 있습니다 `null` 양식에 파일을 첨부하지 않으려면.
   * 페이지 수를 저장하는 데 사용되는 긴 출력 매개 변수입니다.
   * 로케일 값을 저장하는 데 사용되는 문자열 출력 매개 변수입니다.
   * A `FormsResult` 대화형 PDF 양식을 저장하는 데 사용되는 출력 매개 변수 `.`

   다음 `renderPDFForm2` 메서드가 을 반환합니다. `FormsResult` 인터랙티브 PDF 양식을 포함하는 객체입니다.

1. 양식 데이터 스트림으로 작업 수행

   * 만들기 `BLOB` 값을 가져와서 양식 데이터를 포함하는 개체 `FormsResult` 개체 `outputContent` 필드.
   * 만들기 `System.IO.FileStream` 해당 생성자를 호출하여 개체를 작성합니다. 대화형 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 콘텐츠를 저장하는 바이트 배열 만들기 `BLOB` 개체에서 검색됨 `FormsResult` 개체. 의 값을 가져와서 바이트 배열 채우기 `BLOB` 개체 `MTOM` 데이터 구성원입니다.
   * 만들기 `System.IO.BinaryWriter` 개체를 호출하고 `System.IO.FileStream` 개체.
   * 를 호출하여 바이트 배열의 내용을 PDF 파일에 씁니다 `System.IO.BinaryWriter` 개체 `Write` 메서드 및 바이트 배열 전달.

**추가 참조**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
