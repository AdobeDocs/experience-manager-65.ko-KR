---
title: 값별 Forms 렌더링
description: Forms API(Java)를 사용하여 Java API 및 웹 서비스 API를 사용하여 값별로 양식을 렌더링합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: a3a6a06d-ec90-4147-a5f0-e776a086ee12
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1822'
ht-degree: 0%

---

# 값별 Forms 렌더링 {#rendering-forms-by-value}

**이 문서의 샘플과 예제는 JEE 환경의 AEM Forms에 대해서만 적용됩니다.**

일반적으로 Designer에서 만든 양식 디자인은 Forms 서비스를 참조하여 전달됩니다. 양식 디자인은 크기가 클 수 있으므로 값별로 양식 디자인 바이트를 마샬링하지 않도록 참조로 전달하는 것이 더 효율적입니다. Forms 서비스는 양식 디자인을 캐시할 수 있으므로 캐시될 때 양식 디자인을 계속 읽을 필요가 없습니다.

양식 디자인에 UUID 속성이 포함된 경우 캐시됩니다. UUID 값은 모든 양식 디자인에 대해 고유하며 양식을 고유하게 식별하는 데 사용됩니다. 값으로 양식을 렌더링할 때 양식이 반복적으로 사용될 때만 캐시되어야 합니다. 그러나 양식이 반복적으로 사용되지 않고 고유해야 하는 경우 AEM Forms API를 사용하여 설정된 캐싱 옵션을 사용하여 양식을 캐싱하지 않아도 됩니다.

Forms 서비스를 통해 양식 디자인 내에서 연결된 콘텐츠의 위치를 확인할 수도 있습니다. 예를 들어 양식 디자인 내에서 참조되는 연결된 이미지는 상대 URL입니다. 연결된 콘텐츠는 항상 양식 디자인 위치를 기준으로 합니다. 따라서 링크되는 콘텐츠를 해결하는 것은 절대적 형태 설계 위치에 상대적 경로를 적용하여 그 위치를 결정하는 문제이다.

양식 디자인을 참조로 전달하는 대신 값으로 전달할 수 있습니다. 양식 디자인을 동적으로 만들 때(즉, 클라이언트 응용 프로그램에서 런타임 중에 양식 디자인을 만드는 XML을 생성할 때) 값별로 양식 디자인을 전달하는 것이 효율적입니다. 이 경우 양식 디자인은 메모리에 저장되므로 물리적 저장소에 저장되지 않습니다. 런타임 시 동적으로 양식 디자인을 만들어 값에 전달할 때 양식을 캐시하고 Forms 서비스의 성능을 향상시킬 수 있습니다.

**값으로 양식을 전달할 수 없는 제한 사항**

양식 디자인을 값으로 전달할 때 다음 제한이 적용됩니다.

* 양식 디자인 내에 상대 연결된 콘텐츠가 있을 수 없습니다. 모든 이미지와 조각은 양식 디자인 내부에 삽입되거나 절대적으로 참조되어야 합니다.
* 양식을 렌더링한 후에는 서버측 계산을 수행할 수 없습니다. 양식을 Forms 서비스에 다시 제출하면 서버측 계산 없이 데이터가 추출되고 반환됩니다.
* HTML은 런타임에 연결된 이미지만 사용할 수 있으므로 포함된 이미지가 있는 HTML을 생성할 수 없습니다. 이는 Forms 서비스가 참조된 양식 디자인에서 이미지를 검색하여 HTML이 포함된 이미지를 지원하기 때문입니다. 값으로 전달된 양식 디자인에는 참조된 위치가 없으므로 HTML 페이지가 표시되면 포함된 이미지를 추출할 수 없습니다. 따라서 이미지 참조는 HTML에서 렌더링할 절대 경로여야 합니다.

>[!NOTE]
>
>다양한 유형의 양식을 값별로 렌더링할 수 있지만(예: HTML 양식 또는 사용 권한이 포함된 양식) 이 섹션에서는 대화형 PDF forms 렌더링에 대해 설명합니다.

>[!NOTE]
>
>Forms 서비스에 대한 자세한 내용은 AEM Forms용 [서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

## 단계 요약 {#summary-of-steps}

값을 기준으로 양식을 렌더링하려면 다음 단계를 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. Forms 클라이언트 API 개체를 만듭니다.
1. 양식 디자인을 참조합니다.
1. 값으로 양식을 렌더링합니다.
1. 양식 데이터 스트림을 클라이언트 웹 브라우저에 작성합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 생성하는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Forms 클라이언트 API 개체 만들기**

프로그래밍 방식으로 PDF 양식 클라이언트 API로 데이터를 가져오려면 먼저 데이터 통합 서비스 클라이언트를 만들어야 합니다. 서비스 클라이언트를 만들 때 서비스를 호출하는 데 필요한 연결 설정을 정의합니다.

**양식 디자인 참조**

값으로 양식을 렌더링할 때는 렌더링할 양식 디자인이 포함된 `com.adobe.idp.Document` 개체를 만들어야 합니다. 기존 XDP 파일을 참조하거나 런타임에 양식 디자인을 동적으로 만들고 해당 데이터로 `com.adobe.idp.Document`을(를) 채울 수 있습니다.

>[!NOTE]
>
>이 섹션과 해당 빠른 시작은 기존 XDP 파일을 참조합니다.

**값으로 양식 렌더링**

값을 기준으로 양식을 렌더링하려면 양식 디자인이 포함된 `com.adobe.idp.Document` 인스턴스를 렌더링 메서드의 `inDataDoc` 매개 변수에 전달합니다(`renderPDFForm`, `(Deprecated) renderHTMLForm` 등과 같은 `FormsServiceClient` 개체의 렌더링 메서드 중 하나일 수 있음). 이 매개 변수 값은 일반적으로 양식과 병합되는 데이터에 예약되어 있습니다. 마찬가지로 빈 문자열 값을 `formQuery` 매개 변수에 전달합니다. 일반적으로 이 매개 변수에는 양식 디자인의 이름을 지정하는 문자열 값이 필요합니다.

>[!NOTE]
>
>양식 내에 데이터를 표시하려면 데이터를 `xfa:datasets` 요소 내에 지정해야 합니다. XFA 아키텍처에 대한 자세한 내용을 보려면 [https://www.pdfa.org/norm-refs/XFA-3_3.pdf](https://www.pdfa.org/norm-refs/XFA-3_3.pdf)(으)로 이동하십시오.

**클라이언트 웹 브라우저에 양식 데이터 스트림 작성**

Forms 서비스에서 값별로 양식을 렌더링하면 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림이 반환됩니다. 클라이언트 웹 브라우저에 작성되면 양식이 사용자에게 표시됩니다.

**추가 참조**

[Java API를 사용하여 값별 양식 렌더링](#render-a-form-by-value-using-the-java-api)

[웹 서비스 API를 사용하여 값별 양식 렌더링](#render-a-form-by-value-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms 서비스 API 빠른 시작](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Forms 서비스에 문서 전달](/help/forms/developing/passing-documents-forms-service.md)

[Forms을 렌더링하는 웹 애플리케이션 만들기](/help/forms/developing/creating-web-applications-renders-forms.md)

## Java API를 사용하여 값별 양식 렌더링 {#render-a-form-by-value-using-the-java-api}

Forms API(Java)를 사용하여 값별 양식 렌더링:

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-forms-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. Forms 클라이언트 API 개체 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하고 `ServiceClientFactory` 개체를 전달하여 `FormsServiceClient` 개체를 만듭니다.

1. 양식 디자인 참조

   * 해당 생성자를 사용하고 XDP 파일의 위치를 지정하는 문자열 값을 전달하여 렌더링할 양식 디자인을 나타내는 `java.io.FileInputStream` 개체를 만듭니다.
   * 생성자를 사용하고 `java.io.FileInputStream` 개체를 전달하여 `com.adobe.idp.Document` 개체를 만듭니다.

1. 값으로 양식 렌더링

   `FormsServiceClient` 개체의 `renderPDFForm` 메서드를 호출하고 다음 값을 전달하십시오.

   * 빈 문자열 값입니다. (일반적으로 이 매개 변수에는 양식 디자인의 이름을 지정하는 문자열 값이 필요합니다.)
   * 양식 디자인이 포함된 `com.adobe.idp.Document` 개체입니다. 일반적으로 이 매개 변수 값은 양식과 병합되는 데이터용으로 예약되어 있습니다.
   * 런타임 옵션을 저장하는 `PDFFormRenderSpec` 개체입니다. 선택적 매개 변수이며 런타임 옵션을 지정하지 않으려면 `null`을(를) 지정할 수 있습니다.
   * Forms 서비스에 필요한 URI 값을 포함하는 `URLSpec` 개체입니다.
   * 첨부 파일을 저장하는 `java.util.HashMap` 개체입니다. 선택적 매개 변수이며, 양식에 파일을 첨부하지 않으려면 `null`을(를) 지정할 수 있습니다.

   `renderPDFForm` 메서드는 클라이언트 웹 브라우저에 쓸 수 있는 양식 데이터 스트림이 포함된 `FormsResult` 개체를 반환합니다.

1. 클라이언트 웹 브라우저에 양식 데이터 스트림 작성

   * `FormsResult` 개체의 `getOutputContent` 메서드를 호출하여 `com.adobe.idp.Document` 개체를 만듭니다.
   * 해당 `getContentType` 메서드를 호출하여 `com.adobe.idp.Document` 개체의 콘텐츠 형식을 가져옵니다.
   * `setContentType` 메서드를 호출하고 `com.adobe.idp.Document` 개체의 콘텐츠 형식을 전달하여 `javax.servlet.http.HttpServletResponse` 개체의 콘텐츠 형식을 설정합니다.
   * `javax.servlet.http.HttpServletResponse` 개체의 `getOutputStream` 메서드를 호출하여 양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰는 데 사용되는 `javax.servlet.ServletOutputStream` 개체를 만듭니다.
   * `com.adobe.idp.Document` 개체의 `getInputStream` 메서드를 호출하여 `java.io.InputStream` 개체를 만듭니다.
   * 바이트 배열을 만들고 `InputStream` 개체의 크기를 할당합니다. `InputStream` 개체의 크기를 가져오려면 `InputStream` 개체의 `available` 메서드를 호출하십시오.
   * `InputStream` 개체의 `read` 메서드를 호출하고 바이트 배열을 인수로 전달하여 바이트 배열을 양식 데이터 스트림으로 채웁니다.
   * `javax.servlet.ServletOutputStream` 개체의 `write` 메서드를 호출하여 양식 데이터 스트림을 클라이언트 웹 브라우저로 보냅니다. 바이트 배열을 `write` 메서드에 전달합니다.

**추가 참조**

[값별 Forms 렌더링](/help/forms/developing/rendering-forms.md)

[빠른 시작(SOAP 모드): Java API를 사용하여 값별 렌더링](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-by-value-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API를 사용하여 값별 양식 렌더링 {#render-a-form-by-value-using-the-web-service-api}

Forms API(웹 서비스)를 사용하여 값별로 양식을 렌더링합니다.

1. 프로젝트 파일 포함

   * Forms 서비스 WSDL을 사용하는 Java 프록시 클래스를 만듭니다.
   * 클래스 경로에 Java 프록시 클래스를 포함합니다.

1. Forms 클라이언트 API 개체 만들기

   `FormsService` 개체를 만들고 인증 값을 설정하십시오.

1. 양식 디자인 참조

   * 해당 생성자를 사용하여 `java.io.FileInputStream` 개체를 만듭니다. XDP 파일의 위치를 지정하는 문자열 값을 전달합니다.
   * 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 암호로 암호화된 PDF 문서를 저장하는 데 사용됩니다.
   * `java.io.FileInputStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `available` 메서드를 사용하여 `java.io.FileInputStream` 개체의 크기를 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `java.io.FileInputStream` 개체의 `read` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * 해당 `setBinaryData` 메서드를 호출하고 바이트 배열을 전달하여 `BLOB` 개체를 채웁니다.

1. 값으로 양식 렌더링

   `FormsService` 개체의 `renderPDFForm` 메서드를 호출하고 다음 값을 전달하십시오.

   * 빈 문자열 값입니다. (일반적으로 이 매개 변수에는 양식 디자인의 이름을 지정하는 문자열 값이 필요합니다.)
   * 양식 디자인이 포함된 `BLOB` 개체입니다. 일반적으로 이 매개 변수 값은 양식과 병합되는 데이터용으로 예약되어 있습니다.
   * 런타임 옵션을 저장하는 `PDFFormRenderSpec` 개체입니다. 선택적 매개 변수이며 런타임 옵션을 지정하지 않으려면 `null`을(를) 지정할 수 있습니다.
   * Forms 서비스에 필요한 URI 값을 포함하는 `URLSpec` 개체입니다.
   * 첨부 파일을 저장하는 `java.util.HashMap` 개체입니다. 선택적 매개 변수이며, 양식에 파일을 첨부하지 않으려면 `null`을(를) 지정할 수 있습니다.
   * 메서드로 채워진 빈 `com.adobe.idp.services.holders.BLOBHolder` 개체입니다. 렌더링된 PDF 양식을 저장하는 데 사용됩니다.
   * 메서드로 채워진 빈 `javax.xml.rpc.holders.LongHolder` 개체입니다. (이 인수는 양식의 페이지 수를 저장합니다.)
   * 메서드로 채워진 빈 `javax.xml.rpc.holders.StringHolder` 개체입니다. 이 인수는 로케일 값을 저장합니다.
   * 이 작업의 결과를 포함할 빈 `com.adobe.idp.services.holders.FormsResultHolder` 개체입니다.

   `renderPDFForm` 메서드는 마지막 인수 값으로 전달된 `com.adobe.idp.services.holders.FormsResultHolder` 개체를 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림으로 채웁니다.

1. 클라이언트 웹 브라우저에 양식 데이터 스트림 작성

   * `com.adobe.idp.services.holders.FormsResultHolder` 개체의 `value` 데이터 멤버의 값을 가져와서 `FormResult` 개체를 만듭니다.
   * `FormsResult` 개체의 `getOutputContent` 메서드를 호출하여 양식 데이터를 포함하는 `BLOB` 개체를 만듭니다.
   * 해당 `getContentType` 메서드를 호출하여 `BLOB` 개체의 콘텐츠 형식을 가져옵니다.
   * `setContentType` 메서드를 호출하고 `BLOB` 개체의 콘텐츠 형식을 전달하여 `javax.servlet.http.HttpServletResponse` 개체의 콘텐츠 형식을 설정합니다.
   * `javax.servlet.http.HttpServletResponse` 개체의 `getOutputStream` 메서드를 호출하여 양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰는 데 사용되는 `javax.servlet.ServletOutputStream` 개체를 만듭니다.
   * 바이트 배열을 만들고 `BLOB` 개체의 `getBinaryData` 메서드를 호출하여 바이트 배열을 채웁니다. 이 작업은 `FormsResult` 개체의 콘텐츠를 바이트 배열에 할당합니다.
   * `javax.servlet.http.HttpServletResponse` 개체의 `write` 메서드를 호출하여 양식 데이터 스트림을 클라이언트 웹 브라우저로 보냅니다. 바이트 배열을 `write` 메서드에 전달합니다.

**추가 참조**

[값별 Forms 렌더링](#rendering-forms-by-value)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
