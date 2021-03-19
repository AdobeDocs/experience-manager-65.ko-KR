---
title: 클라이언트에서 Forms 렌더링
seo-title: 클라이언트에서 Forms 렌더링
description: Acrobat 또는 Adobe Reader의 클라이언트측 렌더링 기능을 사용하여 PDF 컨텐츠 전달 최적화 및 네트워크 부하를 처리할 수 있는 Forms 서비스 기능 향상
seo-description: Acrobat 또는 Adobe Reader의 클라이언트측 렌더링 기능을 사용하여 PDF 컨텐츠 전달 최적화 및 네트워크 부하를 처리할 수 있는 Forms 서비스 기능 향상
uuid: 09bcc23d-28b0-473a-87f1-bc17e87620f4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 08d36e9f-cafc-478e-9781-8fc29ac6262e
role: 개발자
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1731'
ht-degree: 0%

---


# 클라이언트 {#rendering-forms-at-the-client}에서 Forms 렌더링

**이 문서의 샘플과 예는 JEE 환경의 AEM Forms에만 해당됩니다.**

## 클라이언트 {#rendering-forms-at-the-client-inner}에서 Forms 렌더링

Acrobat 또는 Adobe Reader의 클라이언트측 렌더링 기능을 사용하여 PDF 컨텐츠 전달을 최적화하고 네트워크 부하를 처리할 수 있는 Forms 서비스의 기능을 향상시킬 수 있습니다. 이 프로세스를 클라이언트에서 양식을 렌더링하는 과정이라고 합니다. 클라이언트에서 양식을 렌더링하려면 클라이언트 장치(일반적으로 웹 브라우저)가 Acrobat 7.0 또는 Adobe Reader 7.0 이상을 사용해야 합니다.

루트 하위 양식에 `restoreState` 특성이 `auto`으로 설정된 경우 서버측 스크립트 실행으로 인한 양식 변경 사항은 클라이언트에서 렌더링되는 양식에 반영되지 않습니다. 이 특성에 대한 자세한 내용은 [Forms Designer.](https://www.adobe.com/go/learn_aemforms_designer_63)

>[!NOTE]
>
>Forms 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### {#summary-of-steps} 단계 요약

클라이언트에서 양식을 렌더링하려면 다음 작업을 수행합니다.

1. 프로젝트 파일 포함
1. Forms Client API 객체를 만듭니다.
1. 클라이언트 렌더링 런타임 옵션을 설정합니다.
1. 클라이언트에서 양식을 렌더링합니다.
1. 클라이언트 웹 브라우저에 양식을 작성합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Forms 클라이언트 API 개체 만들기**

Forms 서비스 클라이언트 API 작업을 프로그래밍 방식으로 수행하려면 먼저 Forms 서비스 클라이언트를 만들어야 합니다. Java API를 사용하는 경우 `FormsServiceClient` 개체를 만듭니다. Forms 웹 서비스 API를 사용하는 경우 `FormsService` 개체를 만듭니다.

**클라이언트 렌더링 런타임 옵션 설정**

클라이언트에서 양식을 렌더링하려면 클라이언트 렌더링 런타임 옵션을 `RenderAtClient` 런타임 옵션을 `true`으로 설정해야 합니다. 그러면 양식이 렌더링되는 클라이언트 장치에 전달됩니다. `RenderAtClient`이(가) `auto`(기본값)인 경우 양식 디자인이 양식을 클라이언트에서 렌더링할지 여부를 결정합니다. 양식 디자인은 플로우 가능한 레이아웃이 있는 양식 디자인이어야 합니다.

선택적 런타임 옵션은 `SeedPDF` 옵션입니다. `SeedPDF` 옵션은 PDF 컨테이너(시드 PDF 문서)와 양식 디자인 및 XML 데이터를 결합합니다. 양식 디자인과 XML 데이터 모두 양식이 렌더링되는 Acrobat 또는 Adobe Reader에 전달됩니다. `SeedPDF` 옵션은 클라이언트 컴퓨터에 양식에 사용된 글꼴이 없는 경우에 사용할 수 있습니다. 예를 들어 최종 사용자가 양식 소유자에게 사용권이 허가된 글꼴을 사용할 수 있는 라이선스를 부여받지 않은 경우입니다.

Designer를 사용하여 간단한 동적 PDF 파일을 시드 PDF 파일로 사용할 수 있습니다. 이 작업을 수행하려면 다음 단계가 필요합니다.

1. 시드 PDF 파일에 글꼴을 포함할지 여부를 결정합니다. 시드 PDF 파일은 렌더링되는 양식에 필요한 추가 글꼴을 포함해야 합니다. 시드 PDF 파일에 글꼴을 포함할 때는 글꼴 라이선스 계약을 위반하지 않아야 합니다. Designer에서 글꼴을 합법적으로 임베드할 수 있는지 여부를 결정할 수 있습니다. 저장할 때 양식에 포함할 수 없는 글꼴이 있는 경우 디자이너는 포함할 수 없는 글꼴을 나열하는 메시지를 표시합니다. 이 메시지는 Designer에서 정적 PDF 문서에 표시되지 않습니다.
1. Designer에서 시드 PDF 파일을 만드는 경우에는 메시지가 포함된 텍스트 필드를 최소한 추가하는 것이 좋습니다. 이 메시지는 문서를 보려면 Acrobat 7.0 이상 또는 Adobe Reader 7.0 이상이 필요하다는 이전 버전의 Adobe Reader 사용자에게 전달되어야 합니다.
1. PDF 파일 이름 확장자를 사용하여 시드 PDF 파일을 동적 PDF 파일로 저장합니다.

>[!NOTE]
>
>클라이언트에서 양식을 렌더링하기 위해 시드 PDF 런타임 옵션을 정의할 필요는 없습니다. 시드 PDF를 지정하지 않으면 Forms 서비스는 COS 개체를 포함하지 않지만 실제 XDP 내용이 포함된 PDF 래퍼를 포함하는 셸 pdf를 만듭니다. 이 섹션의 단계에서는 시드 PDF 런타임 옵션을 설정하지 않습니다. COS 개체에 대한 자세한 내용은 Adobe PDF 참조 안내서를 참조하십시오.

**클라이언트에서 양식 렌더링**

클라이언트에서 양식을 렌더링하려면 양식을 렌더링하기 위해 클라이언트 렌더링 런타임 옵션이 응용 프로그램 논리에 포함되어 있는지 확인해야 합니다.

**양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰기**

Forms 서비스는 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림을 만듭니다. 클라이언트 웹 브라우저에 작성할 때 양식은 Acrobat 7.0 또는 Adobe Reader 7.0 이상에서 렌더링되어 사용자에게 표시됩니다.

**참고 항목**

[Java API를 사용하여 클라이언트에서 양식 렌더링](#render-a-form-at-the-client-using-the-java-api)

[웹 서비스 API를 사용하여 클라이언트에서 양식 렌더링](#render-a-form-at-the-client-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms 서비스 API 빠른 시작](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Forms 서비스에 문서 전달](/help/forms/developing/passing-documents-forms-service.md)

[Forms을 렌더링하는 웹 애플리케이션 만들기](/help/forms/developing/creating-web-applications-renders-forms.md)

### 클라이언트에서 Java API {#render-a-form-at-the-client-using-the-java-api}를 사용하여 양식을 렌더링합니다.

Forms API(Java)를 사용하여 클라이언트에서 양식을 렌더링합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-forms-client.jar 등의 클라이언트 JAR 파일을 포함합니다.

1. Forms 클라이언트 API 개체 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 `FormsServiceClient` 개체를 만들고 `ServiceClientFactory` 개체를 전달합니다.

1. 클라이언트 렌더링 런타임 옵션 설정

   * 생성자를 사용하여 `PDFFormRenderSpec` 객체를 만듭니다.
   * `PDFFormRenderSpec` 개체의 `setRenderAtClient` 메서드를 호출하고 열거형 값 `RenderAtClient.Yes`을(를) 전달하여 `RenderAtClient` 런타임 옵션을 설정합니다.

1. 클라이언트에서 양식 렌더링

   `FormsServiceClient` 객체의 `renderPDFForm` 메서드를 호출하고 다음 값을 전달합니다.

   * 파일 이름 확장자를 포함하여 양식 디자인 이름을 지정하는 문자열 값입니다. AEM Forms 응용 프로그램에 포함된 양식 디자인을 참조하는 경우 전체 경로(예: `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`)를 지정해야 합니다.
   * 양식과 병합할 데이터가 포함된 `com.adobe.idp.Document` 개체 데이터를 병합하지 않으려면 빈 `com.adobe.idp.Document` 개체를 전달합니다.
   * 클라이언트에서 양식을 렌더링하는 데 필요한 런타임 옵션을 저장하는 `PDFFormRenderSpec` 객체입니다.
   * 양식을 렌더링하는 데 Forms 서비스에 필요한 URI 값이 포함된 `URLSpec` 객체입니다.
   * 첨부 파일을 저장하는 `java.util.HashMap` 객체입니다. 이 매개 변수는 선택 사항이며, 양식에 파일을 첨부하지 않으려면 `null`을 지정할 수 있습니다.

   `renderPDFForm` 메서드는 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림을 포함하는 `FormsResult` 객체를 반환합니다.

1. 양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰기

   * `FormsResult` 개체 &#39;s `getOutputContent` 메서드를 호출하여 `com.adobe.idp.Document` 개체를 만듭니다.
   * `getContentType` 메서드를 호출하여 `com.adobe.idp.Document` 객체의 내용 유형을 가져옵니다.
   * `setContentType` 메서드를 호출하고 `com.adobe.idp.Document` 개체의 내용 유형을 전달하여 `javax.servlet.http.HttpServletResponse` 개체의 내용 유형을 설정합니다.
   * `javax.servlet.http.HttpServletResponse` 개체의 `getOutputStream` 메서드를 호출하여 양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰는 데 사용되는 `javax.servlet.ServletOutputStream` 개체를 만듭니다.
   * `com.adobe.idp.Document` 객체의 `getInputStream` 메서드를 호출하여 `java.io.InputStream` 객체를 만듭니다.
   * 바이트 배열을 만들고 `InputStream` 객체의 `read` 메서드를 호출하고 바이트 배열을 인수로 전달하여 양식 데이터 스트림으로 채웁니다.
   * 양식 데이터 스트림을 클라이언트 웹 브라우저에 보내려면 `javax.servlet.ServletOutputStream` 객체의 `write` 메서드를 호출합니다. 바이트 배열을 `write` 메서드에 전달합니다.

**참고 항목**

[빠른 시작(SOAP 모드):Java API를 사용하여 클라이언트에서 양식 렌더링](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API {#render-a-form-at-the-client-using-the-web-service-api}를 사용하여 클라이언트에서 양식 렌더링

Forms API(웹 서비스)를 사용하여 클라이언트에서 양식을 렌더링합니다.

1. 프로젝트 파일 포함

   * Forms 서비스 WSDL을 사용하는 Java 프록시 클래스를 만듭니다.
   * 클래스 경로에 Java 프록시 클래스를 포함합니다.

1. Forms 클라이언트 API 개체 만들기

   `FormsService` 개체를 만들고 인증 값을 설정합니다.

1. 클라이언트 렌더링 런타임 옵션 설정

   * 생성자를 사용하여 `PDFFormRenderSpec` 객체를 만듭니다.
   * `PDFFormRenderSpec` 객체의 `setRenderAtClient` 메서드를 호출하고 문자열 값 `RenderAtClient.Yes`을 전달하여 `RenderAtClient` 런타임 옵션을 설정합니다.

1. 클라이언트에서 양식 렌더링

   `FormsService` 객체의 `renderPDFForm` 메서드를 호출하고 다음 값을 전달합니다.

   * 파일 이름 확장자를 포함하여 양식 디자인 이름을 지정하는 문자열 값입니다. Forms 응용 프로그램에 포함된 양식 디자인을 참조하는 경우 전체 경로(예: `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`)를 지정해야 합니다.
   * 양식과 병합할 데이터가 포함된 `BLOB` 개체 데이터를 병합하지 않으려면 `null`을(를) 전달합니다. ([플로우 가능한 레이아웃으로 Forms 미리 채우기](/help/forms/developing/prepopulating-forms-flowable-layouts.md)를 참조하십시오.)
   * 클라이언트에서 양식을 렌더링하는 데 필요한 런타임 옵션을 저장하는 `PDFFormRenderSpec` 객체입니다.
   * Forms 서비스에 필요한 URI 값이 포함된 `URLSpec` 객체입니다.
   * 첨부 파일을 저장하는 `java.util.HashMap` 객체입니다. 이 매개 변수는 선택 사항이며, 양식에 파일을 첨부하지 않으려면 `null`을 지정할 수 있습니다.
   * 메서드에 의해 채워지는 빈 `com.adobe.idp.services.holders.BLOBHolder` 객체입니다. 이 매개 변수는 렌더링된 PDF 양식을 저장하는 데 사용됩니다.
   * 메서드에 의해 채워지는 빈 `javax.xml.rpc.holders.LongHolder` 객체입니다. 이 인수는 양식의 페이지 수를 저장합니다.
   * 메서드에 의해 채워지는 빈 `javax.xml.rpc.holders.StringHolder` 객체입니다. 이 인수는 로케일 값을 저장합니다.
   * 이 작업의 결과를 포함할 빈 `com.adobe.idp.services.holders.FormsResultHolder` 객체입니다.

   `renderPDFForm` 메서드는 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림으로 마지막 인수 값으로 전달되는 `com.adobe.idp.services.holders.FormsResultHolder` 객체를 채웁니다.

1. 양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰기

   * `com.adobe.idp.services.holders.FormsResultHolder` 개체의 `value` 데이터 멤버의 값을 가져와 `FormResult` 개체를 만듭니다.
   * `FormsResult` 개체의 `getOutputContent` 메서드를 호출하여 양식 데이터를 포함하는 `BLOB` 개체를 만듭니다.
   * `getContentType` 메서드를 호출하여 `BLOB` 객체의 내용 유형을 가져옵니다.
   * `setContentType` 메서드를 호출하고 `BLOB` 개체의 내용 유형을 전달하여 `javax.servlet.http.HttpServletResponse` 개체의 내용 유형을 설정합니다.
   * `javax.servlet.http.HttpServletResponse` 개체의 `getOutputStream` 메서드를 호출하여 양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰는 데 사용되는 `javax.servlet.ServletOutputStream` 개체를 만듭니다.
   * 바이트 배열을 만들고 `BLOB` 객체의 `getBinaryData` 메서드를 호출하여 채웁니다. 이 작업은 바이트 배열에 `FormsResult` 객체의 내용을 할당합니다.
   * 양식 데이터 스트림을 클라이언트 웹 브라우저에 보내려면 `javax.servlet.http.HttpServletResponse` 객체의 `write` 메서드를 호출합니다. 바이트 배열을 `write` 메서드에 전달합니다.

**참고 항목**

[클라이언트에서 Forms 렌더링](#rendering-forms-at-the-client)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
