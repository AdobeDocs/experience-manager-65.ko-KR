---
title: 값별 양식 렌더링
seo-title: 값별 양식 렌더링
description: 'null'
seo-description: 'null'
uuid: b932cc54-662f-40ae-94e0-20ac82845f3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ddbb2b82-4c57-4845-a5be-2435902d312b
translation-type: tm+mt
source-git-commit: 66bfd6870b4c09dc2ca1b66058e0b9e040a71507

---


# 값별 양식 렌더링 {#rendering-forms-by-value}

일반적으로 Designer에서 만든 양식 디자인은 Forms 서비스를 기준으로 전달됩니다. 양식 디자인은 클 수 있으며, 그 결과 양식 디자인 바이트를 값별로 마샬링하지 않아도 되기 위해 참조할 수 있도록 보다 효율적으로 전달할 수 있습니다. 또한 양식 서비스는 양식 디자인을 캐시하여 캐시할 때 양식 디자인을 계속 읽을 필요가 없습니다.

양식 디자인에 UUID 속성이 있으면 캐시됩니다. UUID 값은 모든 양식 디자인에 대해 고유하며 양식을 고유하게 식별하는 데 사용됩니다. 양식을 값별로 렌더링할 때는 반복적으로 사용할 때만 양식을 캐시해야 합니다. 그러나 양식이 반복적으로 사용되지 않고 고유해야 하는 경우 AEM Forms API를 사용하여 설정된 캐싱 옵션을 사용하여 양식을 캐싱하지 않을 수 있습니다.

양식 서비스는 양식 디자인 내에서 링크된 컨텐츠의 위치를 확인할 수도 있습니다. 예를 들어, 양식 디자인 내에서 참조되는 연결된 이미지는 상대 URL입니다. 연결된 컨텐츠는 항상 양식 디자인 위치를 기준으로 간주됩니다. 따라서 링크된 컨텐츠를 해결하는 것은 절대 양식 디자인 위치에 상대 경로를 적용하여 해당 위치를 결정하는 문제입니다.

양식 디자인을 참조로 전달하는 대신 값별로 양식 디자인을 전달할 수 있습니다. 양식 디자인을 동적으로 만들 때 값별로 양식 디자인을 전달하는 것이 효율적입니다.즉, 클라이언트 응용 프로그램이 런타임 동안 양식 디자인을 만드는 XML을 생성할 때 이러한 경우 양식 디자인은 메모리에 저장되므로 물리적 저장소에 저장되지 않습니다. 런타임에 양식 디자인을 동적으로 만들어 값을 기준으로 전달하면 양식을 캐싱하고 양식 서비스의 성능을 향상시킬 수 있습니다.

**값별 양식 전달의 제한 사항**

다음 제한 사항은 양식 디자인이 값으로 전달될 때 적용됩니다.

* 양식 디자인에는 상대적 링크 컨텐츠가 없을 수 있습니다. 모든 이미지와 조각은 양식 디자인 내에 삽입되거나 절대적으로 참조되어야 합니다.
* 양식을 렌더링한 후에는 서버측 계산을 수행할 수 없습니다. 양식을 양식 서비스로 다시 제출하면 데이터를 추출하여 서버측 계산 없이 반환됩니다.
* HTML은 런타임 시 연결된 이미지만 사용할 수 있으므로 임베디드 이미지가 있는 HTML을 생성할 수 없습니다. 이는 Forms 서비스가 참조된 양식 디자인에서 이미지를 검색하여 HTML이 포함된 이미지를 지원하기 때문입니다. 값에 의해 전달된 양식 디자인에는 참조된 위치가 없으므로 HTML 페이지를 표시할 때 포함된 이미지를 추출할 수 없습니다. 따라서 이미지 참조는 HTML로 렌더링할 절대 경로여야 합니다.

>[!NOTE]
>
>다양한 유형의 양식을 값별로 렌더링할 수 있지만(예: 사용 권한이 있는 HTML 양식 또는 양식) 이 섹션에서는 대화형 PDF 양식 렌더링에 대해 설명합니다.

>[!NOTE]
>
>양식 서비스에 대한 자세한 내용은 AEM Forms [에 대한 서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

## 단계 요약 {#summary-of-steps}

값을 기준으로 양식을 렌더링하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. Forms 클라이언트 API 개체를 만듭니다.
1. 양식 디자인을 참조합니다.
1. 값을 기준으로 양식을 렌더링합니다.
1. 양식 데이터 스트림을 클라이언트 웹 브라우저에 기록합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Forms 클라이언트 API 개체 만들기**

프로그래밍 방식으로 데이터를 PDF 양식 클라이언트 API로 가져오려면 먼저 데이터 통합 서비스 클라이언트를 만들어야 합니다. 서비스 클라이언트를 만들 때 서비스를 호출하는 데 필요한 연결 설정을 정의합니다.

**양식 디자인 참조**

값을 기준으로 양식을 렌더링할 때는 렌더링할 양식 디자인이 포함된 `com.adobe.idp.Document` 개체를 만들어야 합니다. 기존 XDP 파일을 참조하거나 런타임에 양식 디자인을 동적으로 만들어 `com.adobe.idp.Document` 해당 데이터로 채울 수 있습니다.

>[!NOTE]
>
>이 섹션 및 해당 빠른 시작은 기존 XDP 파일을 참조합니다.

**값별 양식 렌더링**

양식을 값별로 렌더링하려면, 양식 디자인이 포함된 `com.adobe.idp.Document` 인스턴스를 렌더링 메서드의 `inDataDoc` 매개 변수( `FormsServiceClient``renderPDFForm`등 `(Deprecated) renderHTMLForm`객체의 렌더링 방법 중 하나일 수 있음)로 전달합니다. 이 매개 변수 값은 일반적으로 양식과 병합된 데이터에 대해 예약됩니다. 마찬가지로 빈 문자열 값을 `formQuery` 매개 변수에 전달합니다. 일반적으로 이 매개 변수에는 양식 디자인의 이름을 지정하는 문자열 값이 필요합니다.

>[!NOTE]
>
>양식 내에서 데이터를 표시하려면 `xfa:datasets` 요소 내에서 데이터를 지정해야 합니다. XFA 아키텍처에 대한 자세한 내용은 https://partners.adobe.com/public/developer/xml/index_arch.html을 [참조하십시오](https://partners.adobe.com/public/developer/xml/index_arch.html).

**클라이언트 웹 브라우저에 양식 데이터 스트림 작성**

Forms 서비스가 양식을 값별로 렌더링하면 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림을 반환합니다. 클라이언트 웹 브라우저에 작성하면 사용자가 양식을 볼 수 있습니다.

**참고 항목**

[Java API를 사용하여 값을 기준으로 양식 렌더링](#render-a-form-by-value-using-the-java-api)

[웹 서비스 API 파섹](#render-a-form-by-value-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API 빠른 시작](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Forms 서비스에 문서 전달](/help/forms/developing/passing-documents-forms-service.md)

[양식을 렌더링하는 웹 애플리케이션 만들기](/help/forms/developing/creating-web-applications-renders-forms.md)

## Java API를 사용하여 값을 기준으로 양식 렌더링 {#render-a-form-by-value-using-the-java-api}

양식 API(Java)를 사용하여 값을 기준으로 양식을 렌더링합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-forms-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. Forms 클라이언트 API 개체 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 객체를 전달하여 `FormsServiceClient` 객체를 만듭니다 `ServiceClientFactory` .

1. 양식 디자인 참조

   * 생성자를 사용하여 렌더링할 양식 디자인을 나타내는 `java.io.FileInputStream` 개체를 만들고 XDP 파일의 위치를 지정하는 문자열 값을 전달합니다.
   * 생성자를 사용하여 객체를 전달하여 `com.adobe.idp.Document` 객체를 만듭니다 `java.io.FileInputStream` .

1. 값별 양식 렌더링

   객체의 `FormsServiceClient` `renderPDFForm` 메서드를 호출하고 다음 값을 전달합니다.

   * 빈 문자열 값입니다. (일반적으로 이 매개 변수에는 양식 디자인의 이름을 지정하는 문자열 값이 필요합니다.)
   * 양식 디자인이 포함된 `com.adobe.idp.Document` 개체입니다. 일반적으로 이 매개 변수 값은 양식과 병합된 데이터에 대해 예약됩니다.
   * 런타임 옵션을 저장하는 `PDFFormRenderSpec` 개체입니다. 이 매개 변수는 선택 사항이며 런타임 옵션을 지정하지 않을 `null` 경우 지정할 수 있습니다.
   * Forms 서비스에 필요한 URI 값이 들어 있는 `URLSpec` 개체입니다.
   * 첨부 파일을 저장하는 `java.util.HashMap` 개체입니다. 이 매개 변수는 선택 사항이며 양식에 파일을 첨부하지 않으려는 `null` 경우 지정할 수 있습니다.
   이 `renderPDFForm` 메서드는 클라이언트 웹 브라우저에 쓸 수 있는 양식 데이터 스트림을 포함하는 `FormsResult` 개체를 반환합니다.

1. 클라이언트 웹 브라우저에 양식 데이터 스트림 작성

   * 개체 &#39;s `com.adobe.idp.Document` `FormsResult` `getOutputContent` 메서드를 호출하여 개체를 만듭니다.
   * 해당 `com.adobe.idp.Document` `getContentType` 메서드를 호출하여 개체의 콘텐츠 형식을 가져옵니다.
   * 해당 `javax.servlet.http.HttpServletResponse` 메서드를 호출하고 `setContentType` `com.adobe.idp.Document` 개체의 콘텐츠 형식을 전달하여 개체의 콘텐츠 형식을 설정합니다.
   * 개체의 `javax.servlet.ServletOutputStream` `javax.servlet.http.HttpServletResponse` `getOutputStream` 메서드를 호출하여 양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰는 데 사용되는 개체를 만듭니다.
   * 개체의 `java.io.InputStream` `com.adobe.idp.Document` `getInputStream` 메서드를 호출하여 개체를 만듭니다.
   * 바이트 배열을 만들고 `InputStream` 개체의 크기를 할당합니다. 객체의 `InputStream` 메서드를 호출하여 `available` `InputStream` 객체의 크기를 가져옵니다.
   * 개체의 `InputStream` `read`메서드를 호출하고 바이트 배열을 인수로 전달하여 바이트 배열을 양식 데이터 스트림으로 채웁니다.
   * 양식 데이터 스트림을 클라이언트 웹 브라우저로 전송하려면 `javax.servlet.ServletOutputStream` 개체의 `write` 메서드를 호출합니다. 바이트 배열을 `write` 메서드에 전달합니다.

**참고 항목**

[값별 양식 렌더링](/help/forms/developing/rendering-forms.md)

[빠른 시작(SOAP 모드):Java API를 사용한 값별 렌더링](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-by-value-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API 파섹 {#render-a-form-by-value-using-the-web-service-api}

양식 API(웹 서비스)를 사용하여 값을 기준으로 양식을 렌더링합니다.

1. 프로젝트 파일 포함

   * Forms 서비스 WSDL을 사용하는 Java 프록시 클래스를 만듭니다.
   * 클래스 경로에 Java 프록시 클래스를 포함합니다.

1. Forms 클라이언트 API 개체 만들기

   객체를 만들고 인증 값을 `FormsService` 설정합니다.

1. 양식 디자인 참조

   * 생성자를 사용하여 `java.io.FileInputStream` 객체를 만듭니다. XDP 파일의 위치를 지정하는 문자열 값을 전달합니다.
   * 생성자를 사용하여 `BLOB` 객체를 만듭니다. 이 `BLOB` 개체는 암호로 암호화된 PDF 문서를 저장하는 데 사용됩니다.
   * 개체의 내용을 저장하는 바이트 배열을 `java.io.FileInputStream` 만듭니다. 바이트 배열의 크기는 해당 메서드를 사용하여 `java.io.FileInputStream` 개체의 크기를 가져와서 결정할 수 `available` 있습니다.
   * 객체의 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열을 스트림 데이터로 채웁니다. `java.io.FileInputStream` `read`
   * 해당 `BLOB` `setBinaryData` 메서드를 호출하고 바이트 배열을 전달하여 객체를 채웁니다.

1. 값별 양식 렌더링

   객체의 `FormsService` `renderPDFForm` 메서드를 호출하고 다음 값을 전달합니다.

   * 빈 문자열 값입니다. (일반적으로 이 매개 변수에는 양식 디자인의 이름을 지정하는 문자열 값이 필요합니다.)
   * 양식 디자인이 포함된 `BLOB` 개체입니다. 일반적으로 이 매개 변수 값은 양식과 병합된 데이터에 대해 예약됩니다.
   * 런타임 옵션을 저장하는 `PDFFormRenderSpec` 개체입니다. 이 매개 변수는 선택 사항이며 런타임 옵션을 지정하지 않을 `null` 경우 지정할 수 있습니다.
   * Forms 서비스에 필요한 URI 값이 들어 있는 `URLSpec` 개체입니다.
   * 첨부 파일을 저장하는 `java.util.HashMap` 개체입니다. 이 매개 변수는 선택 사항이며 양식에 파일을 첨부하지 않으려는 `null` 경우 지정할 수 있습니다.
   * 메서드에 의해 채워지는 빈 `com.adobe.idp.services.holders.BLOBHolder` 개체입니다. 렌더링된 PDF 양식을 저장하는 데 사용됩니다.
   * 메서드에 의해 채워지는 빈 `javax.xml.rpc.holders.LongHolder` 개체입니다. 이 인수는 페이지의 수를 양식에 저장합니다.
   * 메서드에 의해 채워지는 빈 `javax.xml.rpc.holders.StringHolder` 개체입니다. 이 인수는 로케일 값을 저장합니다.
   * 이 작업의 결과를 포함할 빈 `com.adobe.idp.services.holders.FormsResultHolder` 개체입니다.
   이 `renderPDFForm` 메서드는 마지막 인수 값으로 전달되는 `com.adobe.idp.services.holders.FormsResultHolder` 개체를 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림으로 채웁니다.

1. 클라이언트 웹 브라우저에 양식 데이터 스트림 작성

   * 개체의 `FormResult` `com.adobe.idp.services.holders.FormsResultHolder` `value` 데이터 멤버의 값을 가져와 개체를 만듭니다.
   * 개체의 `BLOB` `FormsResult` `getOutputContent` 메서드를 호출하여 양식 데이터가 포함된 개체를 만듭니다.
   * 해당 `BLOB` `getContentType` 메서드를 호출하여 개체의 콘텐츠 형식을 가져옵니다.
   * 해당 `javax.servlet.http.HttpServletResponse` 메서드를 호출하고 `setContentType` `BLOB` 개체의 콘텐츠 형식을 전달하여 개체의 콘텐츠 형식을 설정합니다.
   * 개체의 `javax.servlet.ServletOutputStream` `javax.servlet.http.HttpServletResponse` `getOutputStream` 메서드를 호출하여 양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰는 데 사용되는 개체를 만듭니다.
   * 바이트 배열을 만들어 `BLOB` 개체의 `getBinaryData` 메서드를 호출하여 채웁니다. 이 작업은 `FormsResult` 개체의 내용을 바이트 배열에 할당합니다.
   * 양식 데이터 스트림을 클라이언트 웹 브라우저로 전송하려면 `javax.servlet.http.HttpServletResponse` 개체의 `write` 메서드를 호출합니다. 바이트 배열을 `write` 메서드에 전달합니다.

**참고 항목**

[값별 양식 렌더링](#rendering-forms-by-value)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
