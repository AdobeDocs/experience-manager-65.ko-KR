---
title: 양식 서비스의 성능 최적화
seo-title: 양식 서비스의 성능 최적화
description: 양식을 렌더링할 때 런타임 옵션을 설정하고 저장소에 XDP 파일을 저장해 Forms 서비스의 성능을 최적화합니다.
seo-description: 양식을 렌더링할 때 런타임 옵션을 설정하고 저장소에 XDP 파일을 저장해 Forms 서비스의 성능을 최적화합니다.
uuid: 9040c09a-e5d0-432b-b1c5-ad46ab57c4fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f883483-b81e-42c6-a4a1-eb499dd112e7
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '1445'
ht-degree: 0%

---


# Forms 서비스의 성능 최적화 {#optimizing-the-performance-of-theforms-service}

## Forms 서비스의 성능 최적화 {#optimizing-the-performance-of-the-forms-service}

양식을 렌더링할 때 Forms 서비스의 성능을 최적화하는 런타임 옵션을 설정할 수 있습니다. Forms 서비스의 성능을 개선하기 위해 수행할 수 있는 또 다른 작업은 저장소에 XDP 파일을 저장하는 것입니다. 그러나 이 섹션에서는 이 작업을 수행하는 방법에 대해 설명합니다. (Java 클라이언트 라이브러리[를 사용하여 서비스 호출을 참조하십시오.)](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

>[!NOTE]
>
>Forms 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### {#summary-of-steps} 단계 요약

양식을 렌더링하는 동안 Forms 서비스의 성능을 최적화하려면 다음 작업을 수행합니다.

1. 프로젝트 파일 포함
1. Forms Client API 객체를 만듭니다.
1. 성능 런타임 옵션을 설정합니다.
1. 양식을 렌더링합니다.
1. 양식 데이터 스트림을 클라이언트 웹 브라우저에 씁니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Forms 클라이언트 API 개체 만들기**

Forms 서비스 클라이언트 API 작업을 프로그래밍 방식으로 수행하려면 먼저 Forms 서비스 클라이언트를 만들어야 합니다. Java API를 사용하는 경우 `FormsServiceClient` 개체를 만듭니다. Forms 웹 서비스 API를 사용하는 경우 `FormsService` 개체를 만듭니다.

**성능 런타임 옵션 설정**

다음 성능 런타임 옵션을 설정하여 Forms 서비스의 성능을 개선할 수 있습니다.

* **양식 캐싱**:서버 캐시에서 PDF로 렌더링되는 양식을 캐싱할 수 있습니다. 각 양식은 처음 생성된 후 캐시됩니다. 이후 렌더링할 때 캐시된 양식이 양식 디자인의 타임스탬프보다 최신 경우 캐시에서 양식이 검색됩니다. 양식을 캐싱하면 저장소에서 양식 디자인을 검색할 필요가 없으므로 Forms 서비스의 성능이 향상됩니다.
* 양식 안내선(더 이상 사용되지 않음)은 다른 변형 유형보다 렌더링하는 데 더 오래 걸릴 수 있습니다. 성능을 개선하기 위해 양식 안내선(더 이상 사용되지 않음)을 캐시하는 것이 좋습니다.
* **독립형 옵션**:Forms 서비스에서 서버측 계산을 수행할 필요가 없는 경우 [독립형] 옵션을 로 설정하면 상태 정보 없이  `true`양식이 렌더링됩니다. 최종 사용자에게 대화형 양식을 렌더링하여 사용자가 양식에 정보를 입력하고 양식을 다시 Forms 서비스에 제출하는 경우 상태 정보가 필요합니다. 그런 다음 Forms 서비스는 계산 작업을 수행하고 양식에 표시된 결과와 함께 양식을 사용자에게 다시 렌더링합니다. 상태 정보가 없는 양식을 Forms 서비스로 다시 전송하면 XML 데이터만 사용할 수 있고 서버측 계산은 수행되지 않습니다.
* **선형화된 PDF**:선형화된 PDF 파일은 네트워크 환경에서 증분 액세스를 효율적으로 할 수 있도록 구성됩니다. PDF 파일은 모든 측면에서 유효한 PDF이며 모든 기존 뷰어 및 기타 PDF 애플리케이션과 호환됩니다. 즉, 선형화된 PDF는 다운로드하는 동안 볼 수 있습니다.
* 이 옵션은 PDF 양식을 클라이언트에서 렌더링할 때 성능을 향상시키지 않습니다.
* **안내선 RSL 옵션**:런타임 공유 라이브러리를 사용하여 양식 안내서(더 이상 사용되지 않음) 생성을 활성화합니다. 즉, 첫 번째 요청은 작은 SWF 파일과 더 큰 공유 라이브러리를 브라우저 캐시에 저장합니다. 자세한 내용은 Flex 설명서의 RSL을 참조하십시오.
* 클라이언트에서 양식을 렌더링하여 Forms 서비스의 성능을 개선할 수도 있습니다. ([ 클라이언트에서 Forms 렌더링 참조)](/help/forms/developing/rendering-forms-client.md)

**양식 렌더링**

성능 옵션을 설정한 후 양식을 렌더링하려면 성능 옵션이 없는 양식을 렌더링하는 것과 동일한 응용 프로그램 논리를 사용합니다.

**양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰기**

Forms 서비스가 양식을 렌더링하면 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림을 반환합니다. 클라이언트 웹 브라우저에 작성할 때 양식이 사용자에게 표시됩니다.

**참고 항목**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms 서비스 API 빠른 시작](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[대화형 PDF forms 렌더링](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Forms을 HTML로 렌더링](/help/forms/developing/rendering-forms-html.md)

[Forms을 렌더링하는 웹 애플리케이션 만들기](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java API {#optimize-the-performance-using-the-java-api}을 사용하여 성능 최적화

Forms API(Java)를 사용하여 최적화된 성능을 가진 양식을 렌더링합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-forms-client.jar 등의 클라이언트 JAR 파일을 포함합니다.

1. Forms 클라이언트 API 개체 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 `FormsServiceClient` 개체를 만들고 `ServiceClientFactory` 개체를 전달합니다.

1. 성능 런타임 옵션 설정

   * 생성자를 사용하여 `PDFFormRenderSpec` 객체를 만듭니다.
   * `PDFFormRenderSpec` 개체의 `setCacheEnabled` 메서드를 호출하고 `true`를 전달하여 양식 캐시 옵션을 설정합니다.
   * `PDFFormRenderSpec` 개체의 `setLinearizedPDF` 메서드를 호출하고 `true.`를 전달하여 선형화된 옵션을 설정합니다.

1. 양식 렌더링

   `FormsServiceClient` 객체의 `renderPDFForm` 메서드를 호출하고 다음 값을 전달합니다.

   * 파일 이름 확장자를 포함하여 양식 디자인 이름을 지정하는 문자열 값입니다.
   * 양식과 병합할 데이터가 포함된 `com.adobe.idp.Document` 개체 데이터를 병합하지 않으려면 빈 `com.adobe.idp.Document` 개체를 전달합니다.
   * 성능을 개선하기 위해 런타임 옵션을 저장하는 `PDFFormRenderSpec` 객체입니다.
   * Forms 서비스에 필요한 URI 값이 포함된 `URLSpec` 객체입니다.
   * 첨부 파일을 저장하는 `java.util.HashMap` 객체입니다. 이 매개 변수는 선택 사항이며, 양식에 파일을 첨부하지 않으려면 `null`을 지정할 수 있습니다.

   `renderPDFForm` 메서드는 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림을 포함하는 `FormsResult` 객체를 반환합니다.

1. 양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰기

   * 양식 데이터 스트림을 클라이언트 웹 브라우저에 보내는 데 사용되는 `javax.servlet.ServletOutputStream` 개체를 만듭니다.
   * `FormsResult` 개체 &#39;s `getOutputContent` 메서드를 호출하여 `com.adobe.idp.Document` 개체를 만듭니다.
   * `com.adobe.idp.Document` 객체의 `getInputStream` 메서드를 호출하여 `java.io.InputStream` 객체를 만듭니다.
   * 바이트 배열을 만들고 `InputStream` 객체의 `read` 메서드를 호출하고 바이트 배열을 인수로 전달하여 양식 데이터 스트림으로 채웁니다.
   * 양식 데이터 스트림을 클라이언트 웹 브라우저에 보내려면 `javax.servlet.ServletOutputStream` 객체의 `write` 메서드를 호출합니다. 바이트 배열을 `write` 메서드에 전달합니다.

**참고 항목**

[빠른 시작(SOAP 모드):Java API를 사용하여 성능 최적화](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-optimizing-performance-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API {#optimize-the-performance-using-the-web-service-api}를 사용하여 성능 최적화

Forms API(웹 서비스)를 사용하여 최적화된 성능을 가진 양식을 렌더링합니다.

1. 프로젝트 파일 포함

   * Forms 서비스 WSDL을 사용하는 Java 프록시 클래스를 만듭니다.
   * 클래스 경로에 Java 프록시 클래스를 포함합니다.

1. Forms 클라이언트 API 개체 만들기

   `FormsService` 개체를 만들고 인증 값을 설정합니다.

1. 성능 런타임 옵션 설정

   * 생성자를 사용하여 `PDFFormRenderSpec` 객체를 만듭니다.
   * `PDFFormRenderSpec` 개체의 `setCacheEnabled` 메서드를 호출하고 true를 전달하여 양식 캐시 옵션을 설정합니다.
   * `PDFFormRenderSpec` 객체의 `setStandAlone` 메서드를 호출하고 true를 전달하여 독립형 옵션을 설정합니다.
   * `PDFFormRenderSpec` 객체의 `setLinearizedPDF` 메서드를 호출하고 true를 전달하여 선형화된 옵션을 설정합니다.

1. 양식 렌더링

   `FormsService` 객체의 `renderPDFForm` 메서드를 호출하고 다음 값을 전달합니다.

   * 파일 이름 확장자를 포함하여 양식 디자인 이름을 지정하는 문자열 값입니다.
   * 양식과 병합할 데이터가 포함된 `BLOB` 개체 데이터를 병합하지 않으려면 `null`을(를) 전달합니다.
   * 런타임 옵션을 저장하는 `PDFFormRenderSpecc` 객체입니다.
   * Forms 서비스에 필요한 URI 값이 포함된 `URLSpec` 객체입니다.
   * 첨부 파일을 저장하는 `java.util.HashMap` 객체입니다. 이 매개 변수는 선택 사항이며, 양식에 파일을 첨부하지 않으려면 `null`을 지정할 수 있습니다.
   * 메서드에 의해 채워지는 빈 `com.adobe.idp.services.holders.BLOBHolder` 객체입니다. 렌더링된 PDF 양식을 저장하는 데 사용됩니다.
   * 메서드에 의해 채워지는 빈 `javax.xml.rpc.holders.LongHolder` 객체입니다. 이 인수는 양식의 페이지 수를 저장합니다.
   * 메서드에 의해 채워지는 빈 `javax.xml.rpc.holders.StringHolder` 객체입니다. 이 인수는 로케일 값을 저장합니다.
   * 이 작업의 결과를 포함할 빈 `com.adobe.idp.services.holders.FormsResultHolder` 객체입니다.

   `renderPDFForm` 메서드는 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림으로 마지막 인수 값으로 전달되는 `com.adobe.idp.services.holders.FormsResultHolder` 객체를 채웁니다.

1. 양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰기

   * `com.adobe.idp.services.holders.FormsResultHolder` 개체의 `value` 데이터 멤버의 값을 가져와 `FormResult` 개체를 만듭니다.
   * 양식 데이터 스트림을 클라이언트 웹 브라우저에 보내는 데 사용되는 `javax.servlet.ServletOutputStream` 개체를 만듭니다.
   * `FormsResult` 개체의 `getOutputContent` 메서드를 호출하여 양식 데이터를 포함하는 `BLOB` 개체를 만듭니다.
   * 바이트 배열을 만들고 `BLOB` 객체의 `getBinaryData` 메서드를 호출하여 채웁니다. 이 작업은 바이트 배열에 `FormsResult` 객체의 내용을 할당합니다.
   * 양식 데이터 스트림을 클라이언트 웹 브라우저에 보내려면 `javax.servlet.http.HttpServletResponse` 객체의 `write` 메서드를 호출합니다. 바이트 배열을 `write` 메서드에 전달합니다.

**참고 항목**

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
