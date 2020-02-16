---
title: 양식 서비스의 성능 최적화
seo-title: 양식 서비스의 성능 최적화
description: 'null'
seo-description: 'null'
uuid: 9040c09a-e5d0-432b-b1c5-ad46ab57c4fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f883483-b81e-42c6-a4a1-eb499dd112e7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 양식 서비스의 성능 최적화 {#optimizing-the-performance-of-theforms-service}

## 양식 서비스의 성능 최적화 {#optimizing-the-performance-of-the-forms-service}

양식을 렌더링할 때 Forms 서비스의 성능을 최적화하는 런타임 옵션을 설정할 수 있습니다. Forms 서비스의 성능을 개선하기 위해 수행할 수 있는 또 다른 작업은 저장소에 XDP 파일을 저장하는 것입니다. 그러나 이 섹션에서는 이 작업을 수행하는 방법에 대해 설명합니다. (Java [클라이언트 라이브러리를](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)사용하여 서비스 호출을 참조하십시오.)

>[!NOTE]
>
>양식 서비스에 대한 자세한 내용은 AEM Forms [에 대한 서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary-of-steps}

양식을 렌더링하는 동안 Forms 서비스의 성능을 최적화하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일 포함
1. Forms 클라이언트 API 개체를 만듭니다.
1. 성능 런타임 옵션을 설정합니다.
1. 양식을 렌더링합니다.
1. 양식 데이터 스트림을 클라이언트 웹 브라우저에 기록합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Forms 클라이언트 API 개체 만들기**

Forms 서비스 클라이언트 API 작업을 프로그래밍 방식으로 수행하려면 먼저 Forms 서비스 클라이언트를 만들어야 합니다. Java API를 사용하는 경우 `FormsServiceClient` 개체를 만듭니다. Forms 웹 서비스 API를 사용하는 경우 `FormsService` 개체를 만듭니다.

**성능 런타임 옵션 설정**

다음 성능 런타임 옵션을 설정하여 Forms 서비스의 성능을 개선할 수 있습니다.

* **양식 캐싱**:서버 캐시에서 PDF로 렌더링되는 양식을 캐싱할 수 있습니다. 각 양식은 처음 생성된 후에 캐시됩니다. 이후 렌더링에서 캐시된 양식이 양식 디자인의 타임스탬프보다 최신 경우 캐시에서 양식이 검색됩니다. 양식을 캐싱하면 저장소에서 양식 디자인을 검색할 필요가 없으므로 Forms 서비스의 성능이 향상됩니다.
* 양식 안내선(더 이상 사용되지 않음)은 다른 변형 유형보다 렌더링하는 데 더 오래 걸릴 수 있습니다. 성능 향상을 위해 양식 안내선(더 이상 사용되지 않음)을 캐시하는 것이 좋습니다.
* **독립 실행형 옵션**:양식 서비스가 서버측 계산을 수행할 필요가 없는 경우, 독립형 옵션을 로 설정하면 `true`양식의 상태 정보 없이 렌더링됩니다. 대화형 양식을 최종 사용자에게 렌더링하려는 경우 상태 정보가 필요합니다. 최종 사용자는 양식에 정보를 입력하고 양식을 다시 양식 서비스로 제출합니다. 그런 다음 양식 서비스는 계산 작업을 수행하고 양식에 표시된 결과와 함께 양식을 다시 사용자에게 렌더링합니다. 상태 정보가 없는 양식을 Forms 서비스로 다시 제출하면 XML 데이터만 사용할 수 있고 서버측 계산은 수행되지 않습니다.
* **선형화된 PDF**:선형화된 PDF 파일을 구성하여 네트워크 환경에서 증분 액세스를 효율적으로 수행할 수 있습니다. PDF 파일은 모든 면에서 유효한 PDF이며 모든 기존 뷰어 및 기타 PDF 애플리케이션과 호환됩니다. 즉, 선형화된 PDF를 다운로드하는 동안 볼 수 있습니다.
* 이 옵션은 클라이언트에서 PDF 양식을 렌더링할 때 성능을 향상시키지 않습니다.
* **GuideRSL 옵션**:런타임 공유 라이브러리를 사용하여 양식 안내서(더 이상 사용되지 않음) 생성을 활성화합니다. 즉, 첫 번째 요청은 더 작은 SWF 파일과 더 큰 공유 라이브러리가 브라우저 캐시에 저장되어 있음을 의미합니다. 자세한 내용은 Flex 설명서의 RSL을 참조하십시오.
* 클라이언트에서 양식을 렌더링하여 Forms 서비스의 성능을 향상시킬 수도 있습니다. (클라이언트에서 [양식 렌더링을 참조하십시오](/help/forms/developing/rendering-forms-client.md).)

**양식 렌더링**

성능 옵션을 설정한 후 양식을 렌더링하려면 성능 옵션 없이 양식을 렌더링하는 것과 동일한 응용 프로그램 로직을 사용합니다.

**클라이언트 웹 브라우저에 양식 데이터 스트림 작성**

양식 서비스가 양식을 렌더링하면 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림을 반환합니다. 클라이언트 웹 브라우저에 작성하면 사용자가 양식을 볼 수 있습니다.

**참고 항목**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API 빠른 시작](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[인터랙티브한 PDF 양식 렌더링](/help/forms/developing/rendering-interactive-pdf-forms.md)

[양식을 HTML로 렌더링](/help/forms/developing/rendering-forms-html.md)

[양식을 렌더링하는 웹 애플리케이션 만들기](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java API를 사용하여 성능 최적화 {#optimize-the-performance-using-the-java-api}

양식 API(Java)를 사용하여 최적화된 성능을 사용하여 양식을 렌더링합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-forms-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. Forms 클라이언트 API 개체 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 객체를 전달하여 `FormsServiceClient` 객체를 만듭니다 `ServiceClientFactory` .

1. 성능 런타임 옵션 설정

   * 생성자를 사용하여 `PDFFormRenderSpec` 객체를 만듭니다.
   * 개체의 `PDFFormRenderSpec` 메서드를 호출하고 전달하여 양식 캐시 옵션을 `setCacheEnabled` `true`설정합니다.
   * 개체의 메서드를 호출하고 전달하여 선형화된 옵션을 설정합니다. `PDFFormRenderSpec` `setLinearizedPDF``true.`

1. 양식 렌더링

   객체의 `FormsServiceClient` `renderPDFForm` 메서드를 호출하고 다음 값을 전달합니다.

   * 파일 이름 확장자를 포함하여 양식 디자인 이름을 지정하는 문자열 값입니다.
   * 양식과 병합할 데이터가 들어 있는 `com.adobe.idp.Document` 개체입니다. 데이터를 병합하지 않으려면 빈 `com.adobe.idp.Document` 개체를 전달합니다.
   * 성능을 개선하기 위해 런타임 옵션을 저장하는 `PDFFormRenderSpec` 개체입니다.
   * Forms 서비스에 필요한 URI 값이 들어 있는 `URLSpec` 개체입니다.
   * 첨부 파일을 저장하는 `java.util.HashMap` 개체입니다. 이 매개 변수는 선택 사항이며 양식에 파일을 첨부하지 않으려는 `null` 경우 지정할 수 있습니다.
   이 `renderPDFForm` 메서드는 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림을 포함하는 `FormsResult` 개체를 반환합니다.

1. 클라이언트 웹 브라우저에 양식 데이터 스트림 작성

   * 양식 데이터 스트림을 클라이언트 웹 브라우저로 전송하는 데 사용되는 `javax.servlet.ServletOutputStream` 개체를 만듭니다.
   * 개체 &#39;s `com.adobe.idp.Document` `FormsResult` `getOutputContent` 메서드를 호출하여 개체를 만듭니다.
   * 개체의 `java.io.InputStream` `com.adobe.idp.Document` `getInputStream` 메서드를 호출하여 개체를 만듭니다.
   * 바이트 배열을 만들고 `InputStream` 개체의 `read`메서드를 호출하고 바이트 배열을 인수로 전달하여 양식 데이터 스트림으로 채웁니다.
   * 양식 데이터 스트림을 클라이언트 웹 브라우저로 전송하려면 `javax.servlet.ServletOutputStream` 개체의 `write` 메서드를 호출합니다. 바이트 배열을 `write` 메서드에 전달합니다.

**참고 항목**

[빠른 시작(SOAP 모드):Java API를 사용하여 성능 최적화](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-optimizing-performance-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 성능 최적화 {#optimize-the-performance-using-the-web-service-api}

양식 API(웹 서비스)를 사용하여 최적화된 성능을 사용하여 양식을 렌더링합니다.

1. 프로젝트 파일 포함

   * Forms 서비스 WSDL을 사용하는 Java 프록시 클래스를 만듭니다.
   * 클래스 경로에 Java 프록시 클래스를 포함합니다.

1. Forms 클라이언트 API 개체 만들기

   객체를 만들고 인증 값을 `FormsService` 설정합니다.

1. 성능 런타임 옵션 설정

   * 생성자를 사용하여 `PDFFormRenderSpec` 객체를 만듭니다.
   * 객체의 메서드를 호출하고 true를 전달하여 양식 캐시 옵션을 설정합니다. `PDFFormRenderSpec` `setCacheEnabled`
   * 객체의 메서드를 호출하고 true를 전달하여 독립형 옵션을 설정합니다. `PDFFormRenderSpec` `setStandAlone`
   * 객체의 메서드를 호출하고 true를 전달하여 선형화된 옵션을 설정합니다. `PDFFormRenderSpec` `setLinearizedPDF`

1. 양식 렌더링

   객체의 `FormsService` `renderPDFForm` 메서드를 호출하고 다음 값을 전달합니다.

   * 파일 이름 확장자를 포함하여 양식 디자인 이름을 지정하는 문자열 값입니다.
   * 양식과 병합할 데이터가 들어 있는 `BLOB` 개체입니다. 데이터를 병합하지 않으려면 전달하십시오 `null`.
   * 런타임 옵션을 저장하는 `PDFFormRenderSpecc` 개체입니다.
   * Forms 서비스에 필요한 URI 값이 들어 있는 `URLSpec` 개체입니다.
   * 첨부 파일을 저장하는 `java.util.HashMap` 개체입니다. 이 매개 변수는 선택 사항이며 양식에 파일을 첨부하지 않으려는 `null` 경우 지정할 수 있습니다.
   * 메서드에 의해 채워지는 빈 `com.adobe.idp.services.holders.BLOBHolder` 개체입니다. 렌더링된 PDF 양식을 저장하는 데 사용됩니다.
   * 메서드에 의해 채워지는 빈 `javax.xml.rpc.holders.LongHolder` 개체입니다. 이 인수는 페이지의 수를 양식에 저장합니다.
   * 메서드에 의해 채워지는 빈 `javax.xml.rpc.holders.StringHolder` 개체입니다. 이 인수는 로케일 값을 저장합니다.
   * 이 작업의 결과를 포함할 빈 `com.adobe.idp.services.holders.FormsResultHolder` 개체입니다.
   이 `renderPDFForm` 메서드는 마지막 인수 값으로 전달되는 `com.adobe.idp.services.holders.FormsResultHolder` 개체를 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림으로 채웁니다.

1. 클라이언트 웹 브라우저에 양식 데이터 스트림 작성

   * 개체의 `FormResult` `com.adobe.idp.services.holders.FormsResultHolder` `value` 데이터 멤버의 값을 가져와 개체를 만듭니다.
   * 양식 데이터 스트림을 클라이언트 웹 브라우저로 전송하는 데 사용되는 `javax.servlet.ServletOutputStream` 개체를 만듭니다.
   * 개체의 `BLOB` `FormsResult` `getOutputContent` 메서드를 호출하여 양식 데이터가 포함된 개체를 만듭니다.
   * 바이트 배열을 만들어 `BLOB` 개체의 `getBinaryData` 메서드를 호출하여 채웁니다. 이 작업은 `FormsResult` 개체의 내용을 바이트 배열에 할당합니다.
   * 양식 데이터 스트림을 클라이언트 웹 브라우저로 전송하려면 `javax.servlet.http.HttpServletResponse` 개체의 `write` 메서드를 호출합니다. 바이트 배열을 `write` 메서드에 전달합니다.

**참고 항목**

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
