---
title: 값별 Forms 렌더링
seo-title: 값별 Forms 렌더링
description: Java API 및 웹 서비스 API를 사용하여 값별로 양식을 렌더링하려면 Forms API(Java)를 사용합니다.
seo-description: Java API 및 웹 서비스 API를 사용하여 값별로 양식을 렌더링하려면 Forms API(Java)를 사용합니다.
uuid: b932cc54-662f-40ae-94e0-20ac82845f3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ddbb2b82-4c57-4845-a5be-2435902d312b
role: Developer
exl-id: a3a6a06d-ec90-4147-a5f0-e776a086ee12
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1862'
ht-degree: 0%

---

# 값별 Forms 렌더링 {#rendering-forms-by-value}

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms용입니다.**

일반적으로 디자이너에서 만든 양식 디자인은 Forms 서비스를 참조하여 전달됩니다. 양식 디자인은 클 수 있으며, 따라서 양식 디자인 바이트를 값별로 마샬링하지 않아도 되도록 참조로 전달하는 것이 더 효율적입니다. Forms 서비스는 양식 디자인을 캐시하여 캐시할 때 양식 디자인을 계속 읽을 필요가 없습니다.

양식 디자인에 UUID 속성이 포함되어 있으면 해당 속성이 캐시됩니다. UUID 값은 모든 양식 디자인에 대해 고유하며 양식을 고유하게 식별하는 데 사용됩니다. 값별로 양식을 렌더링할 때는 양식을 반복적으로 사용할 때만 캐시해야 합니다. 그러나 양식이 반복적으로 사용되지 않고 고유해야 하는 경우 AEM Forms API를 사용하여 설정된 캐싱 옵션을 사용하여 양식을 캐싱하지 않도록 할 수 있습니다.

Forms 서비스는 양식 디자인 내에서 연결된 컨텐츠의 위치를 확인할 수도 있습니다. 예를 들어, 양식 디자인 내에서 참조되는 연결된 이미지는 상대 URL입니다. 연결된 컨텐츠는 항상 양식 디자인 위치를 기준으로 가정됩니다. 따라서, 링크된 컨텐츠의 위치는 절대 양식 디자인 위치에 상대 경로를 적용하여 결정하는 문제입니다.

양식 디자인을 참조에 의해 전달하는 대신 값을 기준으로 양식 디자인을 전달할 수 있습니다. 양식 디자인을 동적으로 만들 때 값을 기준으로 양식 디자인을 전달하는 것이 효율적입니다.즉, 클라이언트 응용 프로그램이 런타임 중에 양식 디자인을 만드는 XML을 생성하는 경우 이 경우 양식 디자인은 메모리에 저장되므로 물리적 저장소에 저장되지 않습니다. 런타임에 양식 디자인을 동적으로 만들어 값별로 전달할 때 양식을 캐시하고 Forms 서비스의 성능을 향상시킬 수 있습니다.

**값별 양식 전달 제한 사항**

다음 제한 사항은 양식 디자인이 값으로 전달될 때 적용됩니다.

* 양식 디자인 내에 연결된 상대적 컨텐츠가 없습니다. 모든 이미지와 조각은 양식 디자인 내에 포함되거나 절대적으로 참조되어야 합니다.
* 양식을 렌더링한 후에는 서버측 계산을 수행할 수 없습니다. 양식을 Forms 서비스로 다시 제출하면 데이터가 추출되어 서버측 계산 없이 반환됩니다.
* HTML은 런타임에 연결된 이미지만 사용할 수 있으므로 포함된 이미지가 있는 HTML을 생성할 수 없습니다. Forms 서비스는 참조된 양식 디자인에서 이미지를 검색하여 HTML로 포함된 이미지를 지원하기 때문입니다. 값으로 전달되는 양식 디자인에는 참조된 위치가 없으므로 HTML 페이지를 표시할 때 포함된 이미지를 추출할 수 없습니다. 따라서 HTML로 렌더링하려면 이미지 참조가 절대 경로여야 합니다.

>[!NOTE]
>
>값별로 다른 유형의 양식을 렌더링할 수 있지만(예: 사용 권한이 포함된 HTML 양식 또는 양식) 이 섹션에서는 대화형 PDF forms 렌더링에 대해 설명합니다.

>[!NOTE]
>
>Forms 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

## 단계 요약 {#summary-of-steps}

값을 기준으로 양식을 렌더링하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. Forms 클라이언트 API 개체를 만듭니다.
1. 양식 디자인을 참조합니다.
1. 값을 기준으로 양식을 렌더링합니다.
1. 양식 데이터 스트림을 클라이언트 웹 브라우저에 작성합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Forms 클라이언트 API 개체 만들기**

프로그래밍 방식으로 데이터를 Client API의 PDF로 가져오려면 먼저 Data Integration 서비스 클라이언트를 만들어야 합니다. 서비스 클라이언트를 만들 때 서비스를 호출하는 데 필요한 연결 설정을 정의합니다.

**양식 디자인 참조**

값을 기준으로 양식을 렌더링할 때 렌더링할 양식 디자인이 포함된 `com.adobe.idp.Document` 개체를 만들어야 합니다. 기존 XDP 파일을 참조하거나 런타임에 양식 디자인을 동적으로 만들고 `com.adobe.idp.Document` 을 해당 데이터로 채울 수 있습니다.

>[!NOTE]
>
>이 섹션 및 해당 빠른 시작은 기존 XDP 파일을 참조합니다.

**값을 기준으로 양식 렌더링**

양식을 값으로 렌더링하려면 양식 디자인이 포함된 `com.adobe.idp.Document` 인스턴스를 렌더링 메서드의 `inDataDoc` 매개 변수(`renderPDFForm`, `(Deprecated) renderHTMLForm` 등과 같은 `FormsServiceClient` 개체의 렌더링 메서드 중 하나일 수 있음)에 전달합니다. 이 매개 변수 값은 일반적으로 양식과 병합된 데이터에 대해 예약됩니다. 마찬가지로 빈 문자열 값을 `formQuery` 매개 변수에 전달합니다. 일반적으로 이 매개 변수에는 양식 디자인의 이름을 지정하는 문자열 값이 필요합니다.

>[!NOTE]
>
>양식 내에 데이터를 표시하려면 `xfa:datasets` 요소 내에 데이터를 지정해야 합니다. XFA 아키텍처에 대한 자세한 내용은 [https://partners.adobe.com/public/developer/xml/index_arch.html](https://partners.adobe.com/public/developer/xml/index_arch.html)로 이동하십시오.

**클라이언트 웹 브라우저에 양식 데이터 스트림 쓰기**

Forms 서비스에서 양식을 값으로 렌더링하면 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림을 반환합니다. 클라이언트 웹 브라우저에 작성하면 사용자가 양식을 볼 수 있습니다.

**참고 항목**

[Java API를 사용하여 값으로 양식 렌더링](#render-a-form-by-value-using-the-java-api)

[웹 서비스 API를 사용하여 값으로 양식 렌더링](#render-a-form-by-value-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms 서비스 API 빠른 시작](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Forms 서비스에 문서 전달](/help/forms/developing/passing-documents-forms-service.md)

[Forms을 렌더링하는 웹 애플리케이션 만들기](/help/forms/developing/creating-web-applications-renders-forms.md)

## Java API {#render-a-form-by-value-using-the-java-api}를 사용하여 값으로 양식을 렌더링합니다.

Forms API(Java)를 사용하여 값으로 양식을 렌더링합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-forms-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. Forms 클라이언트 API 개체 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 `FormsServiceClient` 개체를 만들고 `ServiceClientFactory` 개체를 전달합니다.

1. 양식 디자인 참조

   * 생성자를 사용하여 렌더링할 양식 디자인을 나타내는 `java.io.FileInputStream` 개체를 만들고 XDP 파일의 위치를 지정하는 문자열 값을 전달합니다.
   * 생성자를 사용하여 `com.adobe.idp.Document` 개체를 만들고 `java.io.FileInputStream` 개체를 전달합니다.

1. 값을 기준으로 양식 렌더링

   `FormsServiceClient` 개체의 `renderPDFForm` 메서드를 호출하고 다음 값을 전달합니다.

   * 빈 문자열 값입니다. 일반적으로 이 매개 변수에는 양식 디자인의 이름을 지정하는 문자열 값이 필요합니다.
   * 양식 디자인을 포함하는 `com.adobe.idp.Document` 개체입니다. 일반적으로 이 매개 변수 값은 양식과 병합된 데이터에 대해 예약됩니다.
   * 런타임 옵션을 저장하는 `PDFFormRenderSpec` 개체입니다. 이 매개 변수는 선택 사항이며 런타임 옵션을 지정하지 않으려는 경우 `null`을 지정할 수 있습니다.
   * Forms 서비스에 필요한 URI 값을 포함하는 `URLSpec` 개체입니다.
   * 첨부 파일을 저장하는 `java.util.HashMap` 개체입니다. 선택적 매개 변수이며 양식에 파일을 첨부하지 않으려는 경우 `null`을 지정할 수 있습니다.

   `renderPDFForm` 메서드는 클라이언트 웹 브라우저에 쓸 수 있는 양식 데이터 스트림을 포함하는 `FormsResult` 개체를 반환합니다.

1. 클라이언트 웹 브라우저에 양식 데이터 스트림 쓰기

   * `FormsResult` 개체 &#39;s `getOutputContent` 메서드를 호출하여 `com.adobe.idp.Document` 개체를 만듭니다.
   * `getContentType` 메서드를 호출하여 `com.adobe.idp.Document` 개체의 콘텐츠 형식을 가져옵니다.
   * `setContentType` 메서드를 호출하고 `com.adobe.idp.Document` 개체의 콘텐츠 형식을 전달하여 `javax.servlet.http.HttpServletResponse` 개체의 콘텐츠 형식을 설정합니다.
   * `javax.servlet.http.HttpServletResponse` 개체의 `getOutputStream` 메서드를 호출하여 클라이언트 웹 브라우저에 양식 데이터 스트림을 쓰는 데 사용되는 `javax.servlet.ServletOutputStream` 개체를 만듭니다.
   * `com.adobe.idp.Document` 개체의 `getInputStream` 메서드를 호출하여 `java.io.InputStream` 개체를 만듭니다.
   * 바이트 배열을 만들고 `InputStream` 개체의 크기를 할당합니다. `InputStream` 개체의 `available` 메서드를 호출하여 `InputStream` 개체 크기를 가져옵니다.
   * `InputStream` 개체의 `read` 메서드를 호출하고 바이트 배열을 인수로 전달하여 바이트 배열을 양식 데이터 스트림으로 채웁니다.
   * `javax.servlet.ServletOutputStream` 개체의 `write` 메서드를 호출하여 양식 데이터 스트림을 클라이언트 웹 브라우저로 보냅니다. 바이트 배열을 `write` 메서드에 전달합니다.

**참고 항목**

[값별 Forms 렌더링](/help/forms/developing/rendering-forms.md)

[빠른 시작(SOAP 모드):Java API를 사용하여 값별 렌더링](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-by-value-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API {#render-a-form-by-value-using-the-web-service-api}를 사용하여 값으로 양식을 렌더링합니다.

Forms API(웹 서비스)를 사용하여 값별로 양식을 렌더링합니다.

1. 프로젝트 파일 포함

   * Forms 서비스 WSDL을 사용하는 Java 프록시 클래스를 만듭니다.
   * Java 프록시 클래스를 클래스 경로에 포함합니다.

1. Forms 클라이언트 API 개체 만들기

   `FormsService` 개체를 만들고 인증 값을 설정합니다.

1. 양식 디자인 참조

   * 생성자를 사용하여 `java.io.FileInputStream` 개체를 만듭니다. XDP 파일의 위치를 지정하는 문자열 값을 전달합니다.
   * 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 암호로 암호화된 PDF 문서를 저장하는 데 사용됩니다.
   * `java.io.FileInputStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `available` 메서드를 사용하여 `java.io.FileInputStream` 개체의 크기를 가져와 바이트 배열의 크기를 결정할 수 있습니다.
   * `java.io.FileInputStream` 개체의 `read` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * `setBinaryData` 메서드를 호출하고 바이트 배열을 전달하여 `BLOB` 개체를 채웁니다.

1. 값을 기준으로 양식 렌더링

   `FormsService` 개체의 `renderPDFForm` 메서드를 호출하고 다음 값을 전달합니다.

   * 빈 문자열 값입니다. 일반적으로 이 매개 변수에는 양식 디자인의 이름을 지정하는 문자열 값이 필요합니다.
   * 양식 디자인을 포함하는 `BLOB` 개체입니다. 일반적으로 이 매개 변수 값은 양식과 병합된 데이터에 대해 예약됩니다.
   * 런타임 옵션을 저장하는 `PDFFormRenderSpec` 개체입니다. 이 매개 변수는 선택 사항이며 런타임 옵션을 지정하지 않으려는 경우 `null`을 지정할 수 있습니다.
   * Forms 서비스에 필요한 URI 값을 포함하는 `URLSpec` 개체입니다.
   * 첨부 파일을 저장하는 `java.util.HashMap` 개체입니다. 선택적 매개 변수이며 양식에 파일을 첨부하지 않으려는 경우 `null`을 지정할 수 있습니다.
   * 메서드로 채워지는 빈 `com.adobe.idp.services.holders.BLOBHolder` 개체입니다. 렌더링된 PDF 양식을 저장하는 데 사용됩니다.
   * 메서드로 채워지는 빈 `javax.xml.rpc.holders.LongHolder` 개체입니다. (이 인수는 양식에 페이지 수를 저장합니다.)
   * 메서드로 채워지는 빈 `javax.xml.rpc.holders.StringHolder` 개체입니다. 이 인수는 로케일 값을 저장합니다.
   * 이 작업의 결과가 포함될 빈 `com.adobe.idp.services.holders.FormsResultHolder` 개체입니다.

   `renderPDFForm` 메서드는 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림으로 마지막 인수 값으로 전달되는 `com.adobe.idp.services.holders.FormsResultHolder` 개체를 채웁니다.

1. 클라이언트 웹 브라우저에 양식 데이터 스트림 쓰기

   * `com.adobe.idp.services.holders.FormsResultHolder` 개체의 `value` 데이터 멤버의 값을 가져와서 `FormResult` 개체를 만듭니다.
   * `FormsResult` 개체의 `getOutputContent` 메서드를 호출하여 양식 데이터가 포함된 `BLOB` 개체를 만듭니다.
   * `getContentType` 메서드를 호출하여 `BLOB` 개체의 콘텐츠 형식을 가져옵니다.
   * `setContentType` 메서드를 호출하고 `BLOB` 개체의 콘텐츠 형식을 전달하여 `javax.servlet.http.HttpServletResponse` 개체의 콘텐츠 형식을 설정합니다.
   * `javax.servlet.http.HttpServletResponse` 개체의 `getOutputStream` 메서드를 호출하여 클라이언트 웹 브라우저에 양식 데이터 스트림을 쓰는 데 사용되는 `javax.servlet.ServletOutputStream` 개체를 만듭니다.
   * 바이트 배열을 만들고 `BLOB` 개체의 `getBinaryData` 메서드를 호출하여 채웁니다. 이 작업은 `FormsResult` 개체의 콘텐츠를 바이트 배열에 할당합니다.
   * `javax.servlet.http.HttpServletResponse` 개체의 `write` 메서드를 호출하여 양식 데이터 스트림을 클라이언트 웹 브라우저로 보냅니다. 바이트 배열을 `write` 메서드에 전달합니다.

**참고 항목**

[값별 Forms 렌더링](#rendering-forms-by-value)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
