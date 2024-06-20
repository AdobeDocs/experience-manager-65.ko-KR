---
title: 렌더링 권한이 활성화된 Forms
description: Forms 서비스를 사용하여 사용 권한이 적용된 양식을 렌더링합니다. Java API 및 웹 서비스 API를 사용하여 권한이 활성화된 양식을 렌더링할 수 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 012a3a9f-542c-4ed1-a092-572bfccbdf21
solution: Experience Manager, Experience Manager Forms
source-git-commit: 872e2de411f51b5f0b26a2ff47cb49f01313d39f
workflow-type: tm+mt
source-wordcount: '1447'
ht-degree: 0%

---

# 렌더링 권한이 활성화된 Forms {#rendering-rights-enabled-forms}

Forms 서비스는 사용 권한이 적용된 양식을 렌더링할 수 있습니다. 사용 권한은 양식에 주석을 추가하거나 양식 필드를 채우고 양식을 저장하는 기능과 같이 Acrobat에서 기본적으로 사용할 수 있지만 Adobe Reader에서는 사용할 수 없는 기능과 관련이 있습니다. 사용 권한이 적용된 Forms을 권한 사용 양식이라고 합니다. Adobe Reader에서 권한이 활성화된 양식을 여는 사용자는 해당 양식에 대해 활성화된 작업을 수행할 수 있습니다.

양식에 사용 권한을 적용하려면 Acrobat Reader DC 확장 서비스가 AEM Forms 설치에 포함되어야 합니다. 또한 PDF 문서에 사용 권한을 적용할 수 있는 유효한 자격 증명이 있어야 합니다. 즉, 권한이 활성화된 양식을 렌더링하려면 먼저 Acrobat Reader DC 확장 서비스를 제대로 구성해야 합니다. (참조: [Acrobat Reader DC 확장 서비스 정보](/help/forms/developing/assigning-usage-rights.md#about-the-acrobat-reader-dc-extensions-service).)

>[!NOTE]
>
>사용 권한이 포함된 양식을 렌더링하려면 PDF 파일이 아닌 XDP 파일을 입력으로 사용해야 합니다. PDF 파일을 입력으로 사용하는 경우에도 양식이 렌더링되지만 권한이 활성화된 양식은 아닙니다.

>[!NOTE]
>
>다음 사용 권한을 지정할 때는 XML 데이터로 양식을 미리 채울 수 없습니다. `enableComments`, `enableCommentsOnline`, `enableEmbeddedFiles`, 또는 `enableDigitalSignatures`. (참조: [유동성 레이아웃으로 Forms 미리 채우기](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)

>[!NOTE]
>
>Forms 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

## 단계 요약 {#summary-of-steps}

권한이 활성화된 양식을 렌더링하려면 다음 작업을 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. Forms 클라이언트 API 개체를 만듭니다.
1. 사용 권한 런타임 옵션을 설정합니다.
1. 권한이 활성화된 양식을 렌더링합니다.
1. 권한이 활성화된 양식을 클라이언트 웹 브라우저에 작성하십시오.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Forms 클라이언트 API 개체 만들기**

Forms 서비스 클라이언트 API 작업을 프로그래밍 방식으로 수행하려면 먼저 Forms 서비스 클라이언트를 만들어야 합니다.

**사용 권한 런타임 옵션 설정**

사용 권한 런타임 옵션을 설정하여 권한이 활성화된 양식을 렌더링합니다. 양식에 사용 권한을 적용하는 데 사용되는 자격 증명의 별칭을 지정합니다. 별칭 값을 지정한 후 양식에 적용할 각 사용 권한을 지정합니다.

**권한이 활성화된 양식 렌더링**

권한이 활성화된 양식을 렌더링하려면 사용 권한이 없는 양식을 렌더링하는 것과 동일한 응용 프로그램 논리를 사용합니다. 유일한 차이점은 사용 권한 런타임 옵션이 응용 프로그램 논리에 포함되어 있는지 확인해야 한다는 것입니다.

>[!NOTE]
>
>Forms 웹 서비스 API를 사용하여 권한이 활성화된 양식을 렌더링할 때 양식에 파일을 첨부할 수 없습니다.

**클라이언트 웹 브라우저에 양식 데이터 스트림 작성**

Forms 서비스에서 권한이 활성화된 양식을 렌더링하면 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림이 반환됩니다. 클라이언트 웹 브라우저에 작성되면 양식이 사용자에게 표시됩니다. Adobe Reader에서 권한이 활성화된 양식을 보는 사용자는 해당 양식에 대해 활성화된 작업을 수행할 수 있습니다.

**추가 참조**

[Java API를 사용하여 권한이 활성화된 양식 렌더링](#render-rights-enabled-forms-using-the-java-api)

[웹 서비스 API를 사용하여 권한이 활성화된 양식 렌더링](#render-rights-enabled-forms-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms 서비스 API 빠른 시작](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[대화형 PDF forms 렌더링](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Forms을 렌더링하는 웹 애플리케이션 만들기](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java API를 사용하여 권한이 활성화된 양식 렌더링 {#render-rights-enabled-forms-using-the-java-api}

Forms API(Java)를 사용하여 권한이 활성화된 양식을 렌더링합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-forms-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. Forms 클라이언트 API 개체 만들기

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.
   * 만들기 `FormsServiceClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체.

1. 사용 권한 런타임 옵션 설정

   * 만들기 `ReaderExtensionSpec` 개체를 만들 때 사용됩니다.
   * 다음을 호출하여 자격 증명의 별칭 지정 `ReaderExtensionSpec` 개체 `setReCredentialAlias` 메서드, 별칭 값을 나타내는 문자열 값을 지정합니다.
   * 에 속한 해당 메서드를 호출하여 각 사용 권한을 설정합니다. `ReaderExtensionSpec` 개체. 하지만 참조하는 자격 증명을 통해 사용할 수 있는 경우에만 사용 권한을 설정할 수 있습니다. 즉, 자격 증명을 통해 설정하지 않은 경우 사용 권한을 설정할 수 없습니다. 예. 사용자가 양식 필드를 채우고 양식을 저장할 수 있는 사용 권한을 설정하려면 `ReaderExtensionSpec` 개체 `setReFillIn` 방법 및 통과 `true`.

   >[!NOTE]
   >
   >를 호출할 필요가 없습니다. `ReaderExtensionSpec` 개체 `setReCredentialPassword` 메서드를 사용합니다. 이 메서드는 Forms 서비스에서 사용되지 않습니다.

1. 권한이 활성화된 양식 렌더링

   호출 `FormsServiceClient` 개체 `renderPDFFormWithUsageRights` 메서드를 실행하고 다음 값을 전달합니다.

   * 파일 이름 확장명을 포함하여 양식 디자인 이름을 지정하는 문자열 값입니다. Forms 애플리케이션의 일부인 양식 디자인을 참조하는 경우 다음과 같은 전체 경로를 지정해야 합니다. `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `com.adobe.idp.Document` 양식과 병합할 데이터가 포함된 개체입니다. 데이터를 병합하지 않으려면 비워 둡니다. `com.adobe.idp.Document` 개체.
   * A `PDFFormRenderSpec` 런타임 옵션을 저장하는 개체입니다.
   * A `ReaderExtensionSpec` 사용 권한 런타임 옵션을 저장하는 개체입니다.
   * A `URLSpec` Forms 서비스에 필요한 URI 값을 포함하는 개체입니다.

   다음 `renderPDFFormWithUsageRights` 메서드가 을 반환합니다. `FormsResult` 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림이 포함된 개체입니다.

1. 클라이언트 웹 브라우저에 양식 데이터 스트림 작성

   * 만들기 `com.adobe.idp.Document` 를 호출하여 개체 `FormsResult` 의 오브젝트 `getOutputContent` 메서드를 사용합니다.
   * 의 콘텐츠 유형 가져오기 `com.adobe.idp.Document` 개체 `getContentType` 메서드를 사용합니다.
   * 설정 `javax.servlet.http.HttpServletResponse` 를 호출하여 객체의 콘텐츠 유형 `setContentType` 메서드와 의 콘텐츠 유형 전달 `com.adobe.idp.Document` 개체.
   * 만들기 `javax.servlet.ServletOutputStream` 개체를 사용하여 클라이언트 웹 브라우저에서 `javax.servlet.http.HttpServletResponse` 개체 `getOutputStream` 메서드를 사용합니다.
   * 만들기 `java.io.InputStream` 를 호출하여 개체 `com.adobe.idp.Document` 개체 `getInputStream` 메서드를 사용합니다.
   * 바이트 배열을 만들어 양식 데이터 스트림으로 채웁니다. `InputStream` 개체 `read` 메서드에서 바이트 배열을 인수로 전달합니다.
   * 호출 `javax.servlet.ServletOutputStream` 개체 `write` 클라이언트 웹 브라우저에 양식 데이터 스트림을 전송하는 방법입니다. 바이트 배열을 로 전달 `write` 메서드를 사용합니다.

**추가 참조**

[빠른 시작(SOAP 모드): Java API를 사용하여 권한이 활성화된 양식 렌더링](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-rights-enabled-form-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API를 사용하여 권한이 활성화된 양식 렌더링 {#render-rights-enabled-forms-using-the-web-service-api}

Forms API(웹 서비스)를 사용하여 권한이 활성화된 양식을 렌더링합니다.

1. 프로젝트 파일 포함

   * Forms 서비스 WSDL을 사용하는 Java 프록시 클래스를 만듭니다.
   * 클래스 경로에 Java 프록시 클래스를 포함합니다.

1. Forms 클라이언트 API 개체 만들기

   만들기 `FormsService` 개체로 설정하고 인증 값을 설정합니다.

1. 사용 권한 런타임 옵션 설정

   * 만들기 `ReaderExtensionSpec` 개체를 만들 때 사용됩니다.
   * 다음을 호출하여 자격 증명의 별칭 지정 `ReaderExtensionSpec` 개체 `setReCredentialAlias` 메서드, 별칭 값을 나타내는 문자열 값을 지정합니다.
   * 에 속한 해당 메서드를 호출하여 각 사용 권한을 설정합니다. `ReaderExtensionSpec` 개체. 하지만 참조하는 자격 증명을 통해 사용할 수 있는 경우에만 사용 권한을 설정할 수 있습니다. 즉, 자격 증명을 통해 설정하지 않은 경우 사용 권한을 설정할 수 없습니다. 사용자가 양식 필드를 채우고 양식을 저장할 수 있는 사용 권한을 설정하려면 `ReaderExtensionSpec` 개체 `setReFillIn` 방법 및 통과 `true`.

1. 권한이 활성화된 양식 렌더링

   호출 `FormsService` 개체 `renderPDFFormWithUsageRights` 메서드를 실행하고 다음 값을 전달합니다.

   * 파일 이름 확장명을 포함하여 양식 디자인 이름을 지정하는 문자열 값입니다. Forms 애플리케이션의 일부인 양식 디자인을 참조하는 경우 다음과 같은 전체 경로를 지정해야 합니다. `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `BLOB` 양식과 병합할 데이터가 포함된 개체입니다. 데이터를 양식과 병합하지 않으려면 `BLOB` 빈 XML 데이터 소스를 기반으로 하는 개체입니다. 를 전달할 수 없습니다. `BLOB` null인 개체입니다. 그렇지 않으면 예외가 throw됩니다.
   * A `PDFFormRenderSpec` 런타임 옵션을 저장하는 개체입니다.
   * A `ReaderExtensionSpec` 사용 권한 런타임 옵션을 저장하는 개체입니다.
   * A `URLSpec` Forms 서비스에 필요한 URI 값을 포함하는 개체입니다.

   다음 `renderPDFFormWithUsageRights` 메서드가 을 반환합니다. `FormsResult` 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림이 포함된 개체입니다.

1. 클라이언트 웹 브라우저에 양식 데이터 스트림 작성

   * 만들기 `BLOB` 를 호출하여 양식 데이터를 포함하는 개체 `FormsResult` 개체 `getOutputContent` 메서드를 사용합니다.
   * 의 콘텐츠 유형 가져오기 `BLOB` 개체 `getContentType` 메서드를 사용합니다.
   * 설정 `javax.servlet.http.HttpServletResponse` 를 호출하여 객체의 콘텐츠 유형 `setContentType` 메서드와 의 콘텐츠 유형 전달 `BLOB` 개체.
   * 만들기 `javax.servlet.ServletOutputStream` 개체를 사용하여 클라이언트 웹 브라우저에서 `javax.servlet.http.HttpServletResponse` 개체 `getOutputStream` 메서드를 사용합니다.
   * 바이트 배열을 만들고 `BLOB` 개체 `getBinaryData` 메서드를 사용합니다. 이 작업은 의 콘텐츠를 할당합니다. `FormsResult` 개체를 바이트 배열에 추가합니다.
   * 호출 `javax.servlet.http.HttpServletResponse` 개체 `write` 클라이언트 웹 브라우저에 양식 데이터 스트림을 전송하는 방법입니다. 바이트 배열을 로 전달 `write` 메서드를 사용합니다.

**추가 참조**

[렌더링 권한이 활성화된 Forms](#rendering-rights-enabled-forms)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
