---
title: 사용자 지정 CSS 파일을 사용하여 HTML Forms 렌더링
description: Forms 서비스를 사용하여 웹 브라우저의 HTTP 요청에 응답하여 사용자 지정 CSS 파일을 참조하여 HTML 양식을 렌더링합니다. Java API 및 웹 서비스 API를 사용하여 CSS 파일을 사용하는 HTML 양식을 렌더링할 수 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 5fa385a7-f030-4c0c-8938-0991d02ef361
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1687'
ht-degree: 0%

---

# 사용자 지정 CSS 파일을 사용하여 HTML Forms 렌더링 {#rendering-html-forms-using-custom-css-files}

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms에 대해서만 적용됩니다.**

Forms 서비스는 웹 브라우저의 HTTP 요청에 응답하여 HTML 양식을 렌더링합니다. HTML 양식을 렌더링할 때 Forms 서비스에서 사용자 지정 CSS 파일을 참조할 수 있습니다. Forms 서비스를 사용하여 HTML 양식을 렌더링할 때 비즈니스 요구 사항을 충족하는 사용자 지정 CSS 파일을 만들고 해당 CSS 파일을 참조할 수 있습니다.

Forms 서비스는 사용자 지정 CSS 파일을 자동으로 구문 분석합니다. 즉, Forms 서비스는 사용자 지정 CSS 파일이 CSS 표준을 준수하지 않는 경우 발생할 수 있는 오류를 보고하지 않습니다. 이 경우 Forms 서비스는 스타일을 무시하고 CSS 파일의 나머지 스타일을 계속 사용합니다.

다음 목록은 사용자 지정 CSS 파일에서 지원되는 스타일을 지정합니다.

* **클래스 수준 선택기 스타일 쌍**: 사용자 지정 CSS 파일에 있는 경우 HTML 양식에 클래스 스타일로 사용된 선택기가 사용됩니다. 사용하지 않는 클래스 스타일은 무시됩니다.
* **식별자 수준 선택기 스타일 쌍**: 모든 식별자 스타일은 HTML 양식에 사용되는 경우 사용됩니다.
* **요소 수준 선택기-스타일 쌍**: HTML 양식에 사용된 경우 모든 요소 스타일이 사용됩니다.
* **스타일 우선 순위**: 스타일 우선 순위(예: 중요)가 지원되며 사용자 지정 CSS 파일에서 사용할 수 있습니다.
* **미디어 유형**: 하나 이상의 선택기 스타일 쌍을 @media 스타일로 둘러싸서 미디어 유형을 정의할 수 있습니다. Forms 서비스는 지정된 미디어 유형이 지원되는지 여부를 확인하지 않습니다. 사용자 지정 CSS 파일에 지정된 미디어 유형이 HTML 양식에서 병합됩니다.

FormsIVS 응용 프로그램을 사용하여 샘플 CSS 파일을 검색할 수 있습니다. 양식을 업로드하고 테스트 양식 디자인 페이지에서 선택한 다음 생성 을 클릭합니다. 버튼을 클릭하기 전에 HTML 변환 유형을 설정할 필요가 없습니다. 그런 다음 저장 을 선택합니다. 이 CSS 파일을 편집하여 비즈니스 요구 사항을 충족할 수 있습니다.

>[!NOTE]
>
>사용자 지정 CSS 파일을 사용하는 HTML 양식을 렌더링하기 전에 HTML 양식 렌더링에 대해 깊이 있게 이해해야 합니다. (참조: [Forms을 HTML으로 렌더링](/help/forms/developing/rendering-forms-html.md).)

>[!NOTE]
>
>Forms 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

## 단계 요약 {#summary-of-steps}

CSS 파일을 사용하는 HTML 양식을 렌더링하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. Forms Java API 개체를 만듭니다.
1. CSS 파일을 참조합니다.
1. HTML 양식 렌더링
1. 양식 데이터 스트림을 클라이언트 웹 브라우저에 작성합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Forms Java API 개체 만들기**

Forms 서비스에서 지원하는 작업을 프로그래밍 방식으로 수행하려면 먼저 Forms 클라이언트 개체를 만들어야 합니다.

**CSS 파일 참조**

사용자 지정 CSS 파일을 사용하는 HTML 양식을 렌더링하려면 기존 CSS 파일을 참조해야 합니다.

**HTML 양식 렌더링**

HTML 양식을 렌더링하려면 Designer에서 작성하여 XDP 파일로 저장한 양식 디자인을 지정해야 합니다. HTML 변환 유형도 선택해야 합니다. 예를 들어 Internet Explorer 5.0 이상의 동적 HTML을 렌더링하는 HTML 변환 유형을 지정할 수 있습니다.

HTML 양식을 렌더링하려면 다른 양식 유형을 렌더링하는 데 필요한 URI 값과 같은 값도 필요합니다.

**클라이언트 웹 브라우저에 양식 데이터 스트림 작성**

Forms 서비스에서 HTML 양식을 렌더링할 때 HTML 양식을 사용자가 볼 수 있도록 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림을 반환합니다.

**추가 참조**

[Java API를 사용하여 CSS 파일을 사용하는 HTML 양식 렌더링](#render-an-html-form-that-uses-a-css-file-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms 서비스 API 빠른 시작](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[대화형 PDF forms 렌더링](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Forms을 HTML으로 렌더링](/help/forms/developing/rendering-forms-html.md)

[Forms을 렌더링하는 웹 애플리케이션 만들기](/help/forms/developing/creating-web-applications-renders-forms.md)

## Java API를 사용하여 CSS 파일을 사용하는 HTML 양식 렌더링 {#render-an-html-form-that-uses-a-css-file-using-the-java-api}

Forms API(Java)를 사용하여 사용자 지정 CSS 파일을 사용하는 HTML 양식을 렌더링합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-forms-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. Forms Java API 개체 만들기

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.
   * 만들기 `FormsServiceClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체.

1. CSS 파일 참조

   * 만들기 `HTMLRenderSpec` 개체를 만들 때 사용됩니다.
   * 사용자 지정 CSS 파일을 사용하는 HTML 양식을 렌더링하려면 `HTMLRenderSpec` 개체 `setCustomCSSURI` CSS 파일의 위치와 이름을 지정하는 문자열 값을 전달합니다.

1. HTML 양식 렌더링

   호출 `FormsServiceClient` 개체 `(Deprecated) (Deprecated) renderHTMLForm` 메서드를 실행하고 다음 값을 전달합니다.

   * 파일 이름 확장명을 포함하여 양식 디자인 이름을 지정하는 문자열 값입니다. Forms 애플리케이션의 일부인 양식 디자인을 참조하는 경우 다음과 같은 전체 경로를 지정해야 합니다. `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` HTML 환경 설정 유형을 지정하는 열거형 값입니다. 예를 들어, Internet Explorer 5.0 이상의 동적 HTML과 호환되는 HTML 양식을 렌더링하려면 다음을 지정합니다 `TransformTo.MSDHTML`.
   * A `com.adobe.idp.Document` 양식과 병합할 데이터가 포함된 개체입니다. 데이터를 병합하지 않으려면 비워 둡니다. `com.adobe.idp.Document` 개체.
   * 다음 `HTMLRenderSpec` HTML 런타임 옵션을 저장하는 개체입니다.
   * 다음을 지정하는 문자열 값 `HTTP_USER_AGENT` 헤더 값(예: ) `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * A `URLSpec` HTML 양식을 렌더링하는 데 필요한 URI 값을 저장하는 개체입니다.
   * A `java.util.HashMap` 첨부 파일을 저장하는 객체입니다. 이는 선택적 매개 변수이며 다음을 지정할 수 있습니다. `null` 양식에 파일을 첨부하지 않으려면.

   다음 `(Deprecated) renderHTMLForm` 메서드가 을 반환합니다. `FormsResult` 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림이 포함된 개체입니다.

1. 클라이언트 웹 브라우저에 양식 데이터 스트림 작성

   * 만들기 `com.adobe.idp.Document` 를 호출하여 개체 `FormsResult` 의 오브젝트 `getOutputContent` 메서드를 사용합니다.
   * 의 콘텐츠 유형 가져오기 `com.adobe.idp.Document` 개체 `getContentType` 메서드를 사용합니다.
   * 설정 `javax.servlet.http.HttpServletResponse` 를 호출하여 객체의 콘텐츠 유형 `setContentType` 메서드와 의 콘텐츠 유형 전달 `com.adobe.idp.Document` 개체.
   * 만들기 `javax.servlet.ServletOutputStream` 개체를 사용하여 클라이언트 웹 브라우저에서 `javax.servlet.h\ttp.HttpServletResponse` 개체 `getOutputStream` 메서드를 사용합니다.
   * 만들기 `java.io.InputStream` 를 호출하여 개체 `com.adobe.idp.Document` 개체 `getInputStream` 메서드를 사용합니다.
   * 바이트 배열을 만들고 `InputStream` 개체 `read` 메서드에서 바이트 배열을 인수로 전달합니다.
   * 호출 `javax.servlet.ServletOutputStream` 개체 `write` 클라이언트 웹 브라우저에 양식 데이터 스트림을 전송하는 방법입니다. 바이트 배열을 로 전달 `write` 메서드를 사용합니다.

**추가 참조**

[사용자 지정 CSS 파일을 사용하여 HTML Forms 렌더링](#rendering-html-forms-using-custom-css-files)

[빠른 시작(SOAP 모드): Java API를 사용하여 CSS 파일을 사용하는 HTML 양식 렌더링](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-that-uses-a-css-file-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API를 사용하여 CSS 파일을 사용하는 HTML 양식 렌더링 {#render-an-html-form-that-uses-a-css-file-using-the-web-service-api}

Forms API(웹 서비스)를 사용하여 사용자 지정 CSS 파일을 사용하는 HTML 양식을 렌더링합니다.

1. 프로젝트 파일 포함

   * Forms 서비스 WSDL을 사용하는 Java 프록시 클래스를 만듭니다.
   * 클래스 경로에 Java 프록시 클래스를 포함합니다.

1. Forms Java API 개체 만들기

   만들기 `FormsService` 개체로 설정하고 인증 값을 설정합니다.

1. CSS 파일 참조

   * 만들기 `HTMLRenderSpec` 개체를 만들 때 사용됩니다.
   * 사용자 지정 CSS 파일을 사용하는 HTML 양식을 렌더링하려면 `HTMLRenderSpec` 개체 `setCustomCSSURI` CSS 파일의 위치와 이름을 지정하는 문자열 값을 전달합니다.

1. HTML 양식 렌더링

   호출 `FormsService` 개체 `(Deprecated) renderHTMLForm` 메서드를 실행하고 다음 값을 전달합니다.

   * 파일 이름 확장명을 포함하여 양식 디자인 이름을 지정하는 문자열 값입니다. Forms 애플리케이션의 일부인 양식 디자인을 참조하는 경우 다음과 같은 전체 경로를 지정해야 합니다. `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` HTML 환경 설정 유형을 지정하는 열거형 값입니다. 예를 들어, Internet Explorer 5.0 이상의 동적 HTML과 호환되는 HTML 양식을 렌더링하려면 다음을 지정합니다 `TransformTo.MSDHTML`.
   * A `BLOB` 양식과 병합할 데이터가 포함된 개체입니다. 데이터를 병합하지 않으려면 를 전달합니다. `null`. (참조: [유동성 레이아웃으로 Forms 미리 채우기](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
   * 다음 `HTMLRenderSpec` HTML 런타임 옵션을 저장하는 개체입니다.
   * 다음을 지정하는 문자열 값 `HTTP_USER_AGENT` 헤더 값(예: ) `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. 이 값을 설정하지 않으려는 경우 빈 문자열을 전달할 수 있습니다.
   * A `URLSpec` HTML 양식을 렌더링하는 데 필요한 URI 값을 저장하는 개체입니다.
   * A `java.util.HashMap` 첨부 파일을 저장하는 객체입니다. 이는 선택적 매개 변수이며 다음을 지정할 수 있습니다. `null` 양식에 파일을 첨부하지 않으려면.
   * 비어 있음 `com.adobe.idp.services.holders.BLOBHolder` 로 채워지는 개체 `(Deprecated) renderHTMLForm` 메서드를 사용합니다. 이 매개 변수 값은 렌더링된 양식을 저장합니다.
   * 비어 있음 `com.adobe.idp.services.holders.BLOBHolder` 로 채워지는 개체 `(Deprecated) renderHTMLForm` 메서드를 사용합니다. 이 매개 변수는 출력 XML 데이터를 저장합니다.
   * 비어 있음 `javax.xml.rpc.holders.LongHolder` 로 채워지는 개체 `(Deprecated) renderHTMLForm` 메서드를 사용합니다. 이 인수는 양식의 페이지 수를 저장합니다.
   * 비어 있음 `javax.xml.rpc.holders.StringHolder` 로 채워지는 개체 `(Deprecated) renderHTMLForm` 메서드를 사용합니다. 이 인수는 로케일 값을 저장합니다.
   * 비어 있음 `javax.xml.rpc.holders.StringHolder` 로 채워지는 개체 `(Deprecated) renderHTMLForm` 메서드를 사용합니다. 이 인수는 사용되는 HTML 렌더링 값을 저장합니다.
   * 비어 있음 `com.adobe.idp.services.holders.FormsResultHolder` 이 작업의 결과를 포함할 개체입니다.

   다음 `(Deprecated) renderHTMLForm` 메서드는 `com.adobe.idp.services.holders.FormsResultHolder` 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림을 사용하여 마지막 인수 값으로 전달되는 개체입니다.

1. 클라이언트 웹 브라우저에 양식 데이터 스트림 작성

   * 만들기 `FormResult` 의 값을 가져와서 개체 `com.adobe.idp.services.holders.FormsResultHolder` 개체 `value` 데이터 구성원입니다.
   * 만들기 `BLOB` 를 호출하여 양식 데이터를 포함하는 개체 `FormsResult` 개체 `getOutputContent` 메서드를 사용합니다.
   * 의 콘텐츠 유형 가져오기 `BLOB` 개체 `getContentType` 메서드를 사용합니다.
   * 설정 `javax.servlet.http.HttpServletResponse` 를 호출하여 객체의 콘텐츠 유형 `setContentType` 메서드와 의 콘텐츠 유형 전달 `BLOB` 개체.
   * 만들기 `javax.servlet.ServletOutputStream` 개체를 사용하여 클라이언트 웹 브라우저에서 `javax.servlet.http.HttpServletResponse` 개체 `getOutputStream` 메서드를 사용합니다.
   * 바이트 배열을 만들고 `BLOB` 개체 `getBinaryData` 메서드를 사용합니다. 이 작업은 의 콘텐츠를 할당합니다. `FormsResult` 개체를 바이트 배열에 추가합니다.
   * 호출 `javax.servlet.http.HttpServletResponse` 개체 `write` 클라이언트 웹 브라우저에 양식 데이터 스트림을 전송하는 방법입니다. 바이트 배열을 로 전달 `write` 메서드를 사용합니다.

**추가 참조**

[사용자 지정 CSS 파일을 사용하여 HTML Forms 렌더링](#rendering-html-forms-using-custom-css-files)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
