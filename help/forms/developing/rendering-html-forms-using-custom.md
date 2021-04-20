---
title: 사용자 지정 CSS 파일을 사용하여 HTML Forms 렌더링
seo-title: 사용자 지정 CSS 파일을 사용하여 HTML Forms 렌더링
description: 웹 브라우저에서 HTTP 요청에 응답하여 HTML 양식을 렌더링하려면 Forms 서비스를 사용하여 사용자 정의 CSS 파일을 참조합니다. Java API 및 웹 서비스 API를 사용하여 CSS 파일을 사용하는 HTML 양식을 렌더링할 수 있습니다.
seo-description: 웹 브라우저에서 HTTP 요청에 응답하여 HTML 양식을 렌더링하려면 Forms 서비스를 사용하여 사용자 정의 CSS 파일을 참조합니다. Java API 및 웹 서비스 API를 사용하여 CSS 파일을 사용하는 HTML 양식을 렌더링할 수 있습니다.
uuid: a44e96f1-001d-48a2-8c96-15cb9d0c71b3
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8fe7c072-7df0-44b7-92d0-bf39dc1e688a
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1739'
ht-degree: 0%

---


# 사용자 지정 CSS 파일 {#rendering-html-forms-using-custom-css-files}을(를) 사용하여 HTML Forms 렌더링

**이 문서의 샘플과 예는 JEE 환경의 AEM Forms에만 해당됩니다.**

Forms 서비스는 웹 브라우저에서 HTTP 요청에 응답하여 HTML 양식을 렌더링합니다. HTML 양식을 렌더링할 때 Forms 서비스는 사용자 지정 CSS 파일을 참조할 수 있습니다. 사용자 정의 CSS 파일을 만들어 비즈니스 요구 사항을 충족하고 Forms 서비스를 사용하여 HTML 양식을 렌더링할 때 해당 CSS 파일을 참조할 수 있습니다.

Forms 서비스는 사용자 지정 CSS 파일을 자동으로 파싱합니다. 즉, Forms 서비스는 사용자 지정 CSS 파일이 CSS 표준을 준수하지 않을 경우 발생할 수 있는 오류를 보고하지 않습니다. 이러한 경우 Forms 서비스는 스타일을 무시하고 CSS 파일에 있는 나머지 스타일을 계속 사용합니다.

다음 목록은 사용자 지정 CSS 파일에서 지원되는 스타일을 지정합니다.

* **클래스 수준 선택기 스타일 쌍**:사용자 지정 CSS 파일에 있는 경우 HTML 양식에서 클래스 스타일로 사용되는 선택기가 사용됩니다. 사용되지 않은 클래스 스타일은 무시됩니다.
* **식별자 수준 선택기 스타일 쌍**:모든 식별자 스타일은 HTML 양식에서 사용되는 경우 사용됩니다.
* **요소 수준 선택기 스타일 쌍**:모든 요소 스타일은 HTML 양식에 사용될 경우 사용됩니다.
* **스타일 우선 순위**:스타일 우선 순위(중요)가 지원되며 사용자 지정 CSS 파일에서 사용할 수 있습니다.
* **미디어 유형**:하나 이상의 선택기 스타일 쌍을 @media 스타일로 둘러싸서 미디어 유형을 정의할 수 있습니다. Forms 서비스는 지정된 미디어 유형이 지원되는지 여부를 확인하지 않습니다. 사용자 지정 CSS 파일에 지정된 미디어 유형은 HTML 양식으로 병합됩니다.

FormsIVS 응용 프로그램을 사용하여 샘플 CSS 파일을 검색할 수 있습니다. 양식을 업로드하고 [양식 디자인 테스트] 페이지에서 양식을 선택한 다음 [CSS 생성]을 클릭합니다. 단추를 클릭하기 전에 HTML 변형 유형을 설정할 필요는 없습니다. 그런 다음 저장을 선택합니다. 비즈니스 요구 사항에 맞게 이 CSS 파일을 편집할 수 있습니다.

>[!NOTE]
>
>사용자 지정 CSS 파일을 사용하는 HTML 양식을 렌더링하기 전에 HTML 양식 렌더링에 대한 명확한 이해가 있어야 합니다. (HTML](/help/forms/developing/rendering-forms-html.md)로 Forms 렌더링 참조)[

>[!NOTE]
>
>Forms 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

## {#summary-of-steps} 단계 요약

CSS 파일을 사용하는 HTML 양식을 렌더링하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일 포함
1. Forms Java API 객체를 만듭니다.
1. CSS 파일을 참조하십시오.
1. HTML 양식을 렌더링합니다.
1. 양식 데이터 스트림을 클라이언트 웹 브라우저에 씁니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Forms Java API 객체 만들기**

Forms 서비스에서 지원되는 작업을 프로그래밍 방식으로 수행하려면 먼저 Forms 클라이언트 개체를 만들어야 합니다.

**CSS 파일 참조**

사용자 지정 CSS 파일을 사용하는 HTML 양식을 렌더링하려면 기존 CSS 파일을 참조해야 합니다.

**HTML 양식 렌더링**

HTML 양식을 렌더링하려면 Designer에서 만들고 XDP 파일로 저장한 양식 디자인을 지정해야 합니다. HTML 변형 유형도 선택해야 합니다. 예를 들어 Internet Explorer 5.0 이상의 동적 HTML을 렌더링하는 HTML 변형 유형을 지정할 수 있습니다.

HTML 양식을 렌더링하려면 다른 양식 유형을 렌더링하는 데 필요한 URI 값과 같은 값이 필요합니다.

**양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰기**

Forms 서비스는 HTML 양식을 렌더링할 때 HTML 양식을 사용자에게 표시하려면 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림을 반환합니다.

**참고 항목**

[Java API를 사용하여 CSS 파일을 사용하는 HTML 양식 렌더링](#render-an-html-form-that-uses-a-css-file-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms 서비스 API 빠른 시작](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[대화형 PDF forms 렌더링](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Forms을 HTML로 렌더링](/help/forms/developing/rendering-forms-html.md)

[Forms을 렌더링하는 웹 애플리케이션 만들기](/help/forms/developing/creating-web-applications-renders-forms.md)

## Java API {#render-an-html-form-that-uses-a-css-file-using-the-java-api}를 사용하여 CSS 파일을 사용하는 HTML 양식을 렌더링합니다.

Forms API(Java)를 사용하여 사용자 지정 CSS 파일을 사용하는 HTML 양식을 렌더링합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-forms-client.jar 등의 클라이언트 JAR 파일을 포함합니다.

1. Forms Java API 객체 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 `FormsServiceClient` 개체를 만들고 `ServiceClientFactory` 개체를 전달합니다.

1. CSS 파일 참조

   * 생성자를 사용하여 `HTMLRenderSpec` 객체를 만듭니다.
   * 사용자 지정 CSS 파일을 사용하는 HTML 양식을 렌더링하려면 `HTMLRenderSpec` 객체의 `setCustomCSSURI` 메서드를 호출하고 CSS 파일의 위치와 이름을 지정하는 문자열 값을 전달합니다.

1. HTML 양식 렌더링

   `FormsServiceClient` 객체의 `(Deprecated) (Deprecated) renderHTMLForm` 메서드를 호출하고 다음 값을 전달합니다.

   * 파일 이름 확장자를 포함하여 양식 디자인 이름을 지정하는 문자열 값입니다. Forms 응용 프로그램에 포함된 양식 디자인을 참조하는 경우 전체 경로(예: `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`)를 지정해야 합니다.
   * HTML 환경 설정 유형을 지정하는 `TransformTo` 열거형 값. 예를 들어 Internet Explorer 5.0 이상의 동적 HTML과 호환되는 HTML 양식을 렌더링하려면 `TransformTo.MSDHTML`을 지정합니다.
   * 양식과 병합할 데이터가 포함된 `com.adobe.idp.Document` 개체 데이터를 병합하지 않으려면 빈 `com.adobe.idp.Document` 개체를 전달합니다.
   * HTML 런타임 옵션을 저장하는 `HTMLRenderSpec` 객체입니다.
   * `HTTP_USER_AGENT` 헤더 값(예: `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`)을 지정하는 문자열 값입니다.
   * HTML 양식을 렌더링하는 데 필요한 URI 값을 저장하는 `URLSpec` 객체입니다.
   * 첨부 파일을 저장하는 `java.util.HashMap` 객체입니다. 선택적 매개 변수입니다. 양식을 첨부하지 않으려면 `null`을 지정할 수 있습니다.

   `(Deprecated) renderHTMLForm` 메서드는 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림을 포함하는 `FormsResult` 객체를 반환합니다.

1. 양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰기

   * `FormsResult` 개체 &#39;s `getOutputContent` 메서드를 호출하여 `com.adobe.idp.Document` 개체를 만듭니다.
   * `getContentType` 메서드를 호출하여 `com.adobe.idp.Document` 객체의 내용 유형을 가져옵니다.
   * `setContentType` 메서드를 호출하고 `com.adobe.idp.Document` 개체의 내용 유형을 전달하여 `javax.servlet.http.HttpServletResponse` 개체의 내용 유형을 설정합니다.
   * `javax.servlet.h\ttp.HttpServletResponse` 개체의 `getOutputStream` 메서드를 호출하여 양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰는 데 사용되는 `javax.servlet.ServletOutputStream` 개체를 만듭니다.
   * `com.adobe.idp.Document` 객체의 `getInputStream` 메서드를 호출하여 `java.io.InputStream` 객체를 만듭니다.
   * 바이트 배열을 만들고 `InputStream` 객체의 `read` 메서드를 호출하고 바이트 배열을 인수로 전달하여 양식 데이터 스트림으로 채웁니다.
   * 양식 데이터 스트림을 클라이언트 웹 브라우저에 보내려면 `javax.servlet.ServletOutputStream` 객체의 `write` 메서드를 호출합니다. 바이트 배열을 `write` 메서드에 전달합니다.

**참고 항목**

[사용자 지정 CSS 파일을 사용하여 HTML Forms 렌더링](#rendering-html-forms-using-custom-css-files)

[빠른 시작(SOAP 모드):Java API를 사용하여 CSS 파일을 사용하는 HTML 양식 렌더링](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-that-uses-a-css-file-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API {#render-an-html-form-that-uses-a-css-file-using-the-web-service-api}를 사용하여 CSS 파일을 사용하는 HTML 양식을 렌더링합니다.

Forms API(웹 서비스)를 사용하여 사용자 지정 CSS 파일을 사용하는 HTML 양식을 렌더링합니다.

1. 프로젝트 파일 포함

   * Forms 서비스 WSDL을 사용하는 Java 프록시 클래스를 만듭니다.
   * 클래스 경로에 Java 프록시 클래스를 포함합니다.

1. Forms Java API 객체 만들기

   `FormsService` 개체를 만들고 인증 값을 설정합니다.

1. CSS 파일 참조

   * 생성자를 사용하여 `HTMLRenderSpec` 객체를 만듭니다.
   * 사용자 지정 CSS 파일을 사용하는 HTML 양식을 렌더링하려면 `HTMLRenderSpec` 객체의 `setCustomCSSURI` 메서드를 호출하고 CSS 파일의 위치와 이름을 지정하는 문자열 값을 전달합니다.

1. HTML 양식 렌더링

   `FormsService` 객체의 `(Deprecated) renderHTMLForm` 메서드를 호출하고 다음 값을 전달합니다.

   * 파일 이름 확장자를 포함하여 양식 디자인 이름을 지정하는 문자열 값입니다. Forms 응용 프로그램에 포함된 양식 디자인을 참조하는 경우 전체 경로(예: `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`)를 지정해야 합니다.
   * HTML 환경 설정 유형을 지정하는 `TransformTo` 열거형 값. 예를 들어 Internet Explorer 5.0 이상의 동적 HTML과 호환되는 HTML 양식을 렌더링하려면 `TransformTo.MSDHTML`을 지정합니다.
   * 양식과 병합할 데이터가 포함된 `BLOB` 개체 데이터를 병합하지 않으려면 `null`을(를) 전달합니다. ([플로우 가능한 레이아웃으로 Forms 미리 채우기](/help/forms/developing/prepopulating-forms-flowable-layouts.md)를 참조하십시오.)
   * HTML 런타임 옵션을 저장하는 `HTMLRenderSpec` 객체입니다.
   * `HTTP_USER_AGENT` 헤더 값(예: `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`)을 지정하는 문자열 값입니다. 이 값을 설정하지 않으려는 경우 빈 문자열을 전달할 수 있습니다.
   * HTML 양식을 렌더링하는 데 필요한 URI 값을 저장하는 `URLSpec` 객체입니다.
   * 첨부 파일을 저장하는 `java.util.HashMap` 객체입니다. 선택적 매개 변수입니다. 양식을 첨부하지 않으려면 `null`을 지정할 수 있습니다.
   * `(Deprecated) renderHTMLForm` 메서드로 채워진 빈 `com.adobe.idp.services.holders.BLOBHolder` 객체입니다. 이 매개 변수 값은 렌더링된 양식을 저장합니다.
   * `(Deprecated) renderHTMLForm` 메서드로 채워진 빈 `com.adobe.idp.services.holders.BLOBHolder` 객체입니다. 이 매개 변수는 출력 XML 데이터를 저장합니다.
   * `(Deprecated) renderHTMLForm` 메서드로 채워진 빈 `javax.xml.rpc.holders.LongHolder` 객체입니다. 이 인수는 양식의 페이지 수를 저장합니다.
   * `(Deprecated) renderHTMLForm` 메서드로 채워진 빈 `javax.xml.rpc.holders.StringHolder` 객체입니다. 이 인수는 로케일 값을 저장합니다.
   * `(Deprecated) renderHTMLForm` 메서드로 채워진 빈 `javax.xml.rpc.holders.StringHolder` 객체입니다. 이 인수는 사용되는 HTML 렌더링 값을 저장합니다.
   * 이 작업의 결과를 포함할 빈 `com.adobe.idp.services.holders.FormsResultHolder` 객체입니다.

   `(Deprecated) renderHTMLForm` 메서드는 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림으로 마지막 인수 값으로 전달되는 `com.adobe.idp.services.holders.FormsResultHolder` 객체를 채웁니다.

1. 양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰기

   * `com.adobe.idp.services.holders.FormsResultHolder` 개체의 `value` 데이터 멤버의 값을 가져와 `FormResult` 개체를 만듭니다.
   * `FormsResult` 개체의 `getOutputContent` 메서드를 호출하여 양식 데이터를 포함하는 `BLOB` 개체를 만듭니다.
   * `getContentType` 메서드를 호출하여 `BLOB` 객체의 내용 유형을 가져옵니다.
   * `setContentType` 메서드를 호출하고 `BLOB` 개체의 내용 유형을 전달하여 `javax.servlet.http.HttpServletResponse` 개체의 내용 유형을 설정합니다.
   * `javax.servlet.http.HttpServletResponse` 개체의 `getOutputStream` 메서드를 호출하여 양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰는 데 사용되는 `javax.servlet.ServletOutputStream` 개체를 만듭니다.
   * 바이트 배열을 만들고 `BLOB` 객체의 `getBinaryData` 메서드를 호출하여 채웁니다. 이 작업은 바이트 배열에 `FormsResult` 객체의 내용을 할당합니다.
   * 양식 데이터 스트림을 클라이언트 웹 브라우저에 보내려면 `javax.servlet.http.HttpServletResponse` 객체의 `write` 메서드를 호출합니다. 바이트 배열을 `write` 메서드에 전달합니다.

**참고 항목**

[사용자 지정 CSS 파일을 사용하여 HTML Forms 렌더링](#rendering-html-forms-using-custom-css-files)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
