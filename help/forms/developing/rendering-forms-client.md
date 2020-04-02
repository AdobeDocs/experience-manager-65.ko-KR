---
title: 클라이언트에서 양식 렌더링
seo-title: 클라이언트에서 양식 렌더링
description: 'null'
seo-description: 'null'
uuid: 09bcc23d-28b0-473a-87f1-bc17e87620f4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 08d36e9f-cafc-478e-9781-8fc29ac6262e
translation-type: tm+mt
source-git-commit: ab401a8007f6ea85c0e52169091ce7a38b3dbe5c

---


# 클라이언트에서 양식 렌더링 {#rendering-forms-at-the-client}

## 클라이언트에서 양식 렌더링 {#rendering-forms-at-the-client-inner}

Acrobat 또는 Adobe Reader의 클라이언트측 렌더링 기능을 사용하여 PDF 컨텐츠 전달을 최적화하고 Forms 서비스의 네트워크 부하를 처리할 수 있는 기능을 향상시킬 수 있습니다. 이 프로세스는 클라이언트에서 양식을 렌더링하는 것으로 알려져 있습니다. 클라이언트에서 양식을 렌더링하려면 클라이언트 장치(일반적으로 웹 브라우저)가 Acrobat 7.0 또는 Adobe Reader 7.0 이상을 사용해야 합니다.

서버측 스크립트 실행으로 인한 폼의 변경 사항은 루트 하위 양식에 설정된 `restoreState` 특성이 포함되어 있지 않으면 클라이언트에서 렌더링되는 양식에 반영되지 않습니다 `auto`. 이 속성에 대한 자세한 내용은 양식 [디자이너를 참조하십시오.](https://www.adobe.com/go/learn_aemforms_designer_63)

>[!NOTE]
>
>양식 서비스에 대한 자세한 내용은 AEM Forms [에 대한 서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary-of-steps}

클라이언트에서 양식을 렌더링하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일 포함
1. Forms 클라이언트 API 개체를 만듭니다.
1. 클라이언트 렌더링 런타임 옵션을 설정합니다.
1. 클라이언트에서 양식을 렌더링합니다.
1. 클라이언트 웹 브라우저에 양식을 작성합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Forms 클라이언트 API 개체 만들기**

Forms 서비스 클라이언트 API 작업을 프로그래밍 방식으로 수행하려면 먼저 Forms 서비스 클라이언트를 만들어야 합니다. Java API를 사용하는 경우 `FormsServiceClient` 개체를 만듭니다. Forms 웹 서비스 API를 사용하는 경우 `FormsService` 개체를 만듭니다.

**클라이언트 렌더링 런타임 옵션 설정**

클라이언트에서 양식을 렌더링하려면 `RenderAtClient` 런타임 옵션을 로 설정하여 클라이언트 렌더링 런타임 옵션을 설정해야 합니다 `true`. 이렇게 하면 양식이 렌더링되는 클라이언트 장치로 전달됩니다. 이 `RenderAtClient` 값(기본값) `auto` 이면 양식 디자인이 양식을 클라이언트에서 렌더링할지 여부를 결정합니다. 양식 디자인은 플로우 가능한 레이아웃이 있는 양식 디자인이어야 합니다.

옵션 중 하나를 설정할 수 있는 런타임 옵션을 `SeedPDF` 선택합니다. 이 `SeedPDF` 옵션은 PDF 컨테이너(시드 PDF 문서)와 양식 디자인 및 XML 데이터를 결합합니다. 양식 디자인과 XML 데이터는 모두 Acrobat 또는 Adobe Reader로 전달되며, 여기서 양식은 렌더링됩니다. 이 `SeedPDF` 옵션은 클라이언트 컴퓨터에 양식에 사용된 글꼴이 없는 경우(예: 양식 소유자가 사용할 수 있도록 라이센스를 받은 글꼴을 최종 사용자에게 제공하지 않은 경우) 사용할 수 있습니다.

Designer를 사용하여 시드 PDF 파일로 사용할 간단한 동적 PDF 파일을 만들 수 있습니다. 이 작업을 수행하려면 다음 단계가 필요합니다.

1. 시드 PDF 파일에 글꼴을 포함할지 여부를 결정합니다. 시드 PDF 파일에는 렌더링되는 양식에 필요한 추가 글꼴이 있어야 합니다. 시드 PDF 파일에 글꼴을 임베드하는 경우 글꼴 라이센스 계약을 위반하지 않아야 합니다. Designer에서 글꼴을 합법적으로 임베드할 수 있는지 여부를 결정할 수 있습니다. 양식에 포함할 수 없는 글꼴이 있는 경우 Designer는 포함할 수 없는 글꼴을 나열하는 메시지를 표시합니다. 이 메시지는 정적 PDF 문서의 경우 Designer에 표시되지 않습니다.
1. Designer에서 시드 PDF 파일을 만드는 경우 메시지가 포함된 텍스트 필드를 최소한 추가하는 것이 좋습니다. 이전 버전의 Adobe Reader 사용자에게 문서를 보려면 Acrobat 7.0 이상 또는 Adobe Reader 7.0 이상이 필요하다는 메시지를 전달해야 합니다.
1. 시드 PDF 파일을 PDF 파일 이름 확장자로 동적 PDF 파일로 저장합니다.

>[!NOTE]
>
>클라이언트에서 양식을 렌더링하기 위해 시드 PDF 런타임 옵션을 정의할 필요는 없습니다. 시드 PDF를 지정하지 않으면 Forms 서비스는 셸 pdf를 만들어 COS 개체를 포함하지 않지만 실제 XDP 컨텐츠가 포함된 PDF 래퍼를 포함합니다. 이 섹션의 단계에서는 시드 PDF 런타임 옵션을 설정하지 않습니다. COS 개체에 대한 자세한 내용은 Adobe PDF Reference 안내서를 참조하십시오.

**클라이언트에서 양식 렌더링**

클라이언트에서 양식을 렌더링하려면 양식을 렌더링하기 위해 클라이언트 렌더링 런타임 옵션이 응용 프로그램 논리에 포함되어 있는지 확인해야 합니다.

**클라이언트 웹 브라우저에 양식 데이터 스트림 작성**

Forms 서비스는 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림을 만듭니다. 클라이언트 웹 브라우저에 작성할 때 양식은 Acrobat 7.0 또는 Adobe Reader 7.0 이상에서 렌더링되어 사용자에게 표시됩니다.

**참고 항목**

[Java API를 사용하여 클라이언트에서 양식 렌더링](#render-a-form-at-the-client-using-the-java-api)

[웹 서비스 API를 사용하여 클라이언트에서 양식 렌더링](#render-a-form-at-the-client-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API 빠른 시작](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Forms 서비스에 문서 전달](/help/forms/developing/passing-documents-forms-service.md)

[양식을 렌더링하는 웹 애플리케이션 만들기](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java API를 사용하여 클라이언트에서 양식 렌더링 {#render-a-form-at-the-client-using-the-java-api}

양식 API(Java)를 사용하여 클라이언트에서 양식을 렌더링합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-forms-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. Forms 클라이언트 API 개체 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 객체를 전달하여 `FormsServiceClient` 객체를 만듭니다 `ServiceClientFactory` .

1. 클라이언트 렌더링 런타임 옵션 설정

   * 생성자를 사용하여 `PDFFormRenderSpec` 객체를 만듭니다.
   * 개체의 `RenderAtClient` 메서드를 호출하고 열거형 값을 전달하여 런타임 옵션을 `PDFFormRenderSpec` `setRenderAtClient` `RenderAtClient.Yes`설정합니다.

1. 클라이언트에서 양식 렌더링

   객체의 `FormsServiceClient` `renderPDFForm` 메서드를 호출하고 다음 값을 전달합니다.

   * 파일 이름 확장자를 포함하여 양식 디자인 이름을 지정하는 문자열 값입니다. AEM Forms 응용 프로그램에 포함된 양식 디자인을 참조하는 경우 전체 경로(예: `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`예:
   * 양식과 병합할 데이터가 들어 있는 `com.adobe.idp.Document` 개체입니다. 데이터를 병합하지 않으려면 빈 `com.adobe.idp.Document` 개체를 전달합니다.
   * 클라이언트에서 양식을 렌더링하는 데 필요한 런타임 옵션을 저장하는 `PDFFormRenderSpec` 개체입니다.
   * 양식을 렌더링하는 데 필요한 URI 값이 들어 있는 `URLSpec` 개체입니다.
   * 첨부 파일을 저장하는 `java.util.HashMap` 개체입니다. 이 매개 변수는 선택 사항이며 양식에 파일을 첨부하지 않으려는 `null` 경우 지정할 수 있습니다.
   이 `renderPDFForm` 메서드는 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림을 포함하는 `FormsResult` 개체를 반환합니다.

1. 클라이언트 웹 브라우저에 양식 데이터 스트림 작성

   * 개체 &#39;s `com.adobe.idp.Document` `FormsResult` `getOutputContent` 메서드를 호출하여 개체를 만듭니다.
   * 해당 `com.adobe.idp.Document` `getContentType` 메서드를 호출하여 개체의 콘텐츠 형식을 가져옵니다.
   * 해당 `javax.servlet.http.HttpServletResponse` 메서드를 호출하고 `setContentType` `com.adobe.idp.Document` 개체의 콘텐츠 형식을 전달하여 개체의 콘텐츠 형식을 설정합니다.
   * 개체의 `javax.servlet.ServletOutputStream` `javax.servlet.http.HttpServletResponse` `getOutputStream` 메서드를 호출하여 양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰는 데 사용되는 개체를 만듭니다.
   * 개체의 `java.io.InputStream` `com.adobe.idp.Document` `getInputStream` 메서드를 호출하여 개체를 만듭니다.
   * 바이트 배열을 만들고 `InputStream` 개체의 `read` 메서드를 호출하고 바이트 배열을 인수로 전달하여 양식 데이터 스트림으로 채웁니다.
   * 양식 데이터 스트림을 클라이언트 웹 브라우저로 전송하려면 `javax.servlet.ServletOutputStream` 개체의 `write` 메서드를 호출합니다. 바이트 배열을 `write` 메서드에 전달합니다.

**참고 항목**

[빠른 시작(SOAP 모드):클라이언트에서 Java API를 사용하여 양식 렌더링](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 클라이언트에서 양식 렌더링 {#render-a-form-at-the-client-using-the-web-service-api}

Forms API(웹 서비스)를 사용하여 클라이언트에서 양식을 렌더링합니다.

1. 프로젝트 파일 포함

   * Forms 서비스 WSDL을 사용하는 Java 프록시 클래스를 만듭니다.
   * 클래스 경로에 Java 프록시 클래스를 포함합니다.

1. Forms 클라이언트 API 개체 만들기

   객체를 만들고 인증 값을 `FormsService` 설정합니다.

1. 클라이언트 렌더링 런타임 옵션 설정

   * 생성자를 사용하여 `PDFFormRenderSpec` 객체를 만듭니다.
   * 객체의 `RenderAtClient` 메서드를 호출하고 문자열 값을 전달하여 런타임 옵션을 `PDFFormRenderSpec` `setRenderAtClient` `RenderAtClient.Yes`설정합니다.

1. 클라이언트에서 양식 렌더링

   객체의 `FormsService` `renderPDFForm` 메서드를 호출하고 다음 값을 전달합니다.

   * 파일 이름 확장자를 포함하여 양식 디자인 이름을 지정하는 문자열 값입니다. Forms 응용 프로그램에 포함된 양식 디자인을 참조하는 경우 전체 경로(예: `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`예:
   * 양식과 병합할 데이터가 들어 있는 `BLOB` 개체입니다. 데이터를 병합하지 않으려면 전달하십시오 `null`. 자세한 내용은 [플로우 가능한 레이아웃으로 양식 미리 채우기를 참조하십시오](/help/forms/developing/prepopulating-forms-flowable-layouts.md).
   * 클라이언트에서 양식을 렌더링하는 데 필요한 런타임 옵션을 저장하는 `PDFFormRenderSpec` 개체입니다.
   * Forms 서비스에 필요한 URI 값이 들어 있는 `URLSpec` 개체입니다.
   * 첨부 파일을 저장하는 `java.util.HashMap` 개체입니다. 이 매개 변수는 선택 사항이며 양식에 파일을 첨부하지 않으려는 `null` 경우 지정할 수 있습니다.
   * 메서드에 의해 채워지는 빈 `com.adobe.idp.services.holders.BLOBHolder` 개체입니다. 이 매개 변수는 렌더링된 PDF 양식을 저장하는 데 사용됩니다.
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

[클라이언트에서 양식 렌더링](#rendering-forms-at-the-client)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
