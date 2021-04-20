---
title: 렌더링 권한 사용 Forms
seo-title: 렌더링 권한 사용 Forms
description: Forms 서비스를 사용하여 사용 권한이 적용된 양식을 렌더링합니다. Java API 및 웹 서비스 API를 사용하여 권한이 활성화된 양식을 렌더링할 수 있습니다.
seo-description: Forms 서비스를 사용하여 사용 권한이 적용된 양식을 렌더링합니다. Java API 및 웹 서비스 API를 사용하여 권한이 활성화된 양식을 렌더링할 수 있습니다.
uuid: ce5e4be6-d9b0-4989-a0e1-a8c3b98aed77
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d4c2b2f0-613a-409d-b39b-8e37fdb96eea
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1494'
ht-degree: 0%

---


# 렌더링 권한 사용 Forms {#rendering-rights-enabled-forms}

Forms 서비스는 사용 권한이 있는 양식을 렌더링할 수 있습니다. 사용 권한은 양식에 주석을 추가하거나 양식 필드를 채우고 양식을 저장하는 기능 등 Acrobat에서는 기본적으로 사용할 수 없지만 Adobe Reader에서는 사용할 수 없는 기능과 관련이 있습니다. 사용 권한이 적용된 Forms을 권한 사용 양식이라고 합니다. Adobe Reader에서 권한이 활성화된 양식을 여는 사용자는 해당 양식에 대해 활성화된 작업을 수행할 수 있습니다.

양식에 사용 권한을 적용하려면 Acrobat Reader DC 확장 서비스가 AEM 양식 설치의 일부여야 합니다. 또한 PDF 문서에 사용 권한을 적용할 수 있는 유효한 자격 증명이 있어야 합니다. 즉, 권한이 활성화된 양식을 렌더링하기 전에 Acrobat Reader DC 확장 서비스를 올바르게 구성해야 합니다. ([Acrobat Reader DC 확장 서비스 정보](/help/forms/developing/assigning-usage-rights.md#about-the-acrobat-reader-dc-extensions-service)를 참조하십시오.)

>[!NOTE]
>
>사용 권한이 있는 양식을 렌더링하려면 XDP 파일을 PDF 파일이 아닌 입력으로 사용해야 합니다. PDF 파일을 입력으로 사용하는 경우 양식은 여전히 렌더링됩니다.그러나 권한이 활성화된 양식은 아닙니다.

>[!NOTE]
>
>다음 사용 권한을 지정할 때는 XML 데이터로 양식을 미리 채울 수 없습니다.`enableComments`, `enableCommentsOnline`, `enableEmbeddedFiles` 또는 `enableDigitalSignatures`. ([플로우 가능한 레이아웃으로 Forms 미리 채우기](/help/forms/developing/prepopulating-forms-flowable-layouts.md)를 참조하십시오.)

>[!NOTE]
>
>Forms 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

## {#summary-of-steps} 단계 요약

권한이 활성화된 양식을 렌더링하려면 다음 작업을 수행합니다.

1. 프로젝트 파일 포함
1. Forms Client API 객체를 만듭니다.
1. 사용 권한 런타임 옵션을 설정합니다.
1. 권한이 활성화된 양식을 렌더링합니다.
1. 권한 사용 양식을 클라이언트 웹 브라우저에 작성합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Forms 클라이언트 API 개체 만들기**

Forms 서비스 클라이언트 API 작업을 프로그래밍 방식으로 수행하려면 먼저 Forms 서비스 클라이언트를 만들어야 합니다.

**사용 권한 런타임 옵션 설정**

권한 사용 양식을 렌더링하려면 사용 권한 런타임 옵션을 설정해야 합니다. 양식에 사용 권한을 적용하는 데 사용되는 자격 증명의 별칭을 지정해야 합니다. 별칭 값을 지정한 후 각 사용 권한을 지정하여 양식에 적용합니다.

**권한 사용 양식 렌더링**

권한 사용 양식을 렌더링하려면 사용 권한 없이 양식을 렌더링하는 것과 동일한 응용 프로그램 논리를 사용합니다. 유일한 차이점은 사용 권한 런타임 옵션이 응용 프로그램 논리에 포함되어 있는지 확인해야 한다는 것입니다.

>[!NOTE]
>
>Forms 웹 서비스 API를 사용하여 권한이 활성화된 양식을 렌더링할 때 양식에 파일을 첨부할 수 없습니다.

**양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰기**

Forms 서비스가 권한이 활성화된 양식을 렌더링하면 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림을 반환합니다. 클라이언트 웹 브라우저에 작성되면 사용자에게 양식이 표시됩니다. Adobe Reader에서 권한이 활성화된 양식을 보는 사용자는 해당 양식에 대해 활성화된 작업을 수행할 수 있습니다.

**참고 항목**

[Java API를 사용하여 권한 지원 양식 렌더링](#render-rights-enabled-forms-using-the-java-api)

[웹 서비스 API를 사용하여 권한 지원 양식 렌더링](#render-rights-enabled-forms-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms 서비스 API 빠른 시작](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[대화형 PDF forms 렌더링](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Forms을 렌더링하는 웹 애플리케이션 만들기](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java API {#render-rights-enabled-forms-using-the-java-api}을 사용하여 권한 지원 양식 렌더링

Forms API(Java)를 사용하여 권한 지원 양식을 렌더링합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-forms-client.jar 등의 클라이언트 JAR 파일을 포함합니다.

1. Forms 클라이언트 API 개체 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 `FormsServiceClient` 개체를 만들고 `ServiceClientFactory` 개체를 전달합니다.

1. 사용 권한 런타임 옵션 설정

   * 생성자를 사용하여 `ReaderExtensionSpec` 객체를 만듭니다.
   * `ReaderExtensionSpec` 개체의 `setReCredentialAlias` 메서드를 호출하여 자격 증명 별칭을 지정하고 별칭 값을 나타내는 문자열 값을 지정합니다.
   * `ReaderExtensionSpec` 객체에 속한 해당 메서드를 호출하여 각 사용 권한을 설정합니다. 그러나 참조한 자격 증명을 통해 사용할 수 있는 경우에만 사용 권한을 설정할 수 있습니다. 즉, 자격 증명에서 설정할 수 없는 경우 사용 권한을 설정할 수 없습니다. 예. 사용자가 양식 필드를 입력하고 양식을 저장할 수 있는 사용 권한을 설정하려면 `ReaderExtensionSpec` 객체의 `setReFillIn` 메서드를 호출하고 `true`를 전달합니다.

   >[!NOTE]
   >
   >`ReaderExtensionSpec` 객체의 `setReCredentialPassword` 메서드를 호출할 필요가 없습니다. 이 메서드는 Forms 서비스에서 사용되지 않습니다.

1. 권한 사용 양식 렌더링

   `FormsServiceClient` 객체의 `renderPDFFormWithUsageRights` 메서드를 호출하고 다음 값을 전달합니다.

   * 파일 이름 확장자를 포함하여 양식 디자인 이름을 지정하는 문자열 값입니다. Forms 응용 프로그램에 포함된 양식 디자인을 참조하는 경우 전체 경로(예: `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`)를 지정해야 합니다.
   * 양식과 병합할 데이터가 포함된 `com.adobe.idp.Document` 개체 데이터를 병합하지 않으려면 빈 `com.adobe.idp.Document` 개체를 전달합니다.
   * 런타임 옵션을 저장하는 `PDFFormRenderSpec` 객체입니다.
   * 사용 권한 런타임 옵션을 저장하는 `ReaderExtensionSpec` 객체입니다.
   * Forms 서비스에 필요한 URI 값이 포함된 `URLSpec` 객체입니다.

   `renderPDFFormWithUsageRights` 메서드는 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림을 포함하는 `FormsResult` 객체를 반환합니다.

1. 양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰기

   * `FormsResult` 개체 &#39;s `getOutputContent` 메서드를 호출하여 `com.adobe.idp.Document` 개체를 만듭니다.
   * `getContentType` 메서드를 호출하여 `com.adobe.idp.Document` 객체의 내용 유형을 가져옵니다.
   * `setContentType` 메서드를 호출하고 `com.adobe.idp.Document` 개체의 내용 유형을 전달하여 `javax.servlet.http.HttpServletResponse` 개체의 내용 유형을 설정합니다.
   * `javax.servlet.http.HttpServletResponse` 개체의 `getOutputStream` 메서드를 호출하여 양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰는 데 사용되는 `javax.servlet.ServletOutputStream` 개체를 만듭니다.
   * `com.adobe.idp.Document` 객체의 `getInputStream` 메서드를 호출하여 `java.io.InputStream` 객체를 만듭니다.
   * 바이트 배열을 만들어 `InputStream` 객체의 `read` 메서드를 호출하고 바이트 배열을 인수로 전달하여 양식 데이터 스트림으로 채웁니다.
   * 양식 데이터 스트림을 클라이언트 웹 브라우저에 보내려면 `javax.servlet.ServletOutputStream` 객체의 `write` 메서드를 호출합니다. 바이트 배열을 `write` 메서드에 전달합니다.

**참고 항목**

[빠른 시작(SOAP 모드):Java API를 사용하여 권한 지원 양식 렌더링](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-rights-enabled-form-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API {#render-rights-enabled-forms-using-the-web-service-api}을(를) 사용하여 권한이 활성화된 양식을 렌더링합니다.

Forms API(웹 서비스)를 사용하여 권한 지원 양식을 렌더링합니다.

1. 프로젝트 파일 포함

   * Forms 서비스 WSDL을 사용하는 Java 프록시 클래스를 만듭니다.
   * 클래스 경로에 Java 프록시 클래스를 포함합니다.

1. Forms 클라이언트 API 개체 만들기

   `FormsService` 개체를 만들고 인증 값을 설정합니다.

1. 사용 권한 런타임 옵션 설정

   * 생성자를 사용하여 `ReaderExtensionSpec` 객체를 만듭니다.
   * `ReaderExtensionSpec` 개체의 `setReCredentialAlias` 메서드를 호출하여 자격 증명 별칭을 지정하고 별칭 값을 나타내는 문자열 값을 지정합니다.
   * `ReaderExtensionSpec` 객체에 속한 해당 메서드를 호출하여 각 사용 권한을 설정합니다. 그러나 참조한 자격 증명을 통해 사용할 수 있는 경우에만 사용 권한을 설정할 수 있습니다. 즉, 자격 증명에서 설정할 수 없는 경우 사용 권한을 설정할 수 없습니다. 사용자가 양식 필드를 입력하고 양식을 저장할 수 있는 사용 권한을 설정하려면 `ReaderExtensionSpec` 객체의 `setReFillIn` 메서드를 호출하고 `true`를 전달합니다.

1. 권한 사용 양식 렌더링

   `FormsService` 객체의 `renderPDFFormWithUsageRights` 메서드를 호출하고 다음 값을 전달합니다.

   * 파일 이름 확장자를 포함하여 양식 디자인 이름을 지정하는 문자열 값입니다. Forms 응용 프로그램에 포함된 양식 디자인을 참조하는 경우 전체 경로(예: `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`)를 지정해야 합니다.
   * 양식과 병합할 데이터가 포함된 `BLOB` 개체 데이터와 양식을 병합하지 않으려면 빈 XML 데이터 소스를 기반으로 하는 `BLOB` 객체를 전달해야 합니다. null인 `BLOB` 개체는 전달할 수 없습니다.그렇지 않으면 예외가 발생합니다.
   * 런타임 옵션을 저장하는 `PDFFormRenderSpec` 객체입니다.
   * 사용 권한 런타임 옵션을 저장하는 `ReaderExtensionSpec` 객체입니다.
   * Forms 서비스에 필요한 URI 값이 포함된 `URLSpec` 객체입니다.

   `renderPDFFormWithUsageRights` 메서드는 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림을 포함하는 `FormsResult` 객체를 반환합니다.

1. 양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰기

   * `FormsResult` 개체의 `getOutputContent` 메서드를 호출하여 양식 데이터를 포함하는 `BLOB` 개체를 만듭니다.
   * `getContentType` 메서드를 호출하여 `BLOB` 객체의 내용 유형을 가져옵니다.
   * `setContentType` 메서드를 호출하고 `BLOB` 개체의 내용 유형을 전달하여 `javax.servlet.http.HttpServletResponse` 개체의 내용 유형을 설정합니다.
   * `javax.servlet.http.HttpServletResponse` 개체의 `getOutputStream` 메서드를 호출하여 양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰는 데 사용되는 `javax.servlet.ServletOutputStream` 개체를 만듭니다.
   * 바이트 배열을 만들고 `BLOB` 객체의 `getBinaryData` 메서드를 호출하여 채웁니다. 이 작업은 바이트 배열에 `FormsResult` 객체의 내용을 할당합니다.
   * 양식 데이터 스트림을 클라이언트 웹 브라우저에 보내려면 `javax.servlet.http.HttpServletResponse` 객체의 `write` 메서드를 호출합니다. 바이트 배열을 `write` 메서드에 전달합니다.

**참고 항목**

[렌더링 권한 사용 Forms](#rendering-rights-enabled-forms)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
