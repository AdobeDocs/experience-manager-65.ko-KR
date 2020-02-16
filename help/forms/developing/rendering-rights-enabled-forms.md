---
title: 렌더링 권한 사용 양식
seo-title: 렌더링 권한 사용 양식
description: 'null'
seo-description: 'null'
uuid: ce5e4be6-d9b0-4989-a0e1-a8c3b98aed77
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d4c2b2f0-613a-409d-b39b-8e37fdb96eea
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# 렌더링 권한 사용 양식 {#rendering-rights-enabled-forms}

양식 서비스는 사용 권한이 적용된 양식을 렌더링할 수 있습니다. 사용 권한은 Acrobat에서는 기본적으로 사용할 수 있지만 Adobe Reader에서는 사용할 수 없는 기능(예: 양식에 주석을 추가하거나 양식 필드를 채우고 양식을 저장하는 기능)과 관련이 있습니다. 사용 권한이 적용된 양식을 권한 사용 가능한 양식이라고 합니다. Adobe Reader에서 권한이 활성화된 양식을 여는 사용자는 해당 양식에 대해 활성화된 작업을 수행할 수 있습니다.

양식에 사용 권한을 적용하려면 Acrobat Reader DC 확장 서비스가 AEM 양식 설치의 일부여야 합니다. 또한 PDF 문서에 사용 권한을 적용할 수 있는 유효한 자격 증명이 있어야 합니다. 즉, 권한이 활성화된 양식을 렌더링하기 전에 Acrobat Reader DC 확장 서비스를 제대로 구성해야 합니다. (Acrobat [Reader DC 확장 서비스 정보를 참조하십시오](/help/forms/developing/assigning-usage-rights.md#about-the-acrobat-reader-dc-extensions-service).)

>[!NOTE]
>
>사용 권한이 있는 양식을 렌더링하려면 XDP 파일을 PDF 파일이 아닌 입력으로 사용해야 합니다. PDF 파일을 입력으로 사용하는 경우 양식은 계속 렌더링됩니다.그러나 권한이 활성화된 양식은 아닙니다.

>[!NOTE]
>
>다음 사용 권한을 지정할 때 XML 데이터로 양식을 채울 수 없습니다. `enableComments``enableCommentsOnline`, `enableEmbeddedFiles`또는 `enableDigitalSignatures`기타 자세한 내용은 [플로우 가능한 레이아웃으로 양식 미리 채우기를 참조하십시오](/help/forms/developing/prepopulating-forms-flowable-layouts.md).

>[!NOTE]
>
>양식 서비스에 대한 자세한 내용은 AEM Forms [에 대한 서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

## 단계 요약 {#summary-of-steps}

권한이 활성화된 양식을 렌더링하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일 포함
1. Forms 클라이언트 API 개체를 만듭니다.
1. 사용 권한 런타임 옵션을 설정합니다.
1. 권한 사용 양식을 렌더링합니다.
1. 권한 사용 양식을 클라이언트 웹 브라우저에 작성합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Forms 클라이언트 API 개체 만들기**

Forms 서비스 클라이언트 API 작업을 프로그래밍 방식으로 수행하려면 먼저 Forms 서비스 클라이언트를 만들어야 합니다.

**사용 권한 런타임 옵션 설정**

권한 사용 양식을 렌더링하려면 사용 권한 런타임 옵션을 설정해야 합니다. 양식에 사용 권한을 적용하는 데 사용되는 자격 증명의 별칭도 지정해야 합니다. 별칭 값을 지정한 후 양식에 적용할 각 사용 권한을 지정합니다.

**권한 사용 양식 렌더링**

권한 사용 양식을 렌더링하려면 사용 권한 없이 양식을 렌더링하는 것과 동일한 응용 프로그램 논리를 사용합니다. 유일한 차이점은 사용 권한 런타임 옵션이 응용 프로그램 논리에 포함되어 있는지 확인해야 한다는 것입니다.

>[!NOTE]
>
>Forms 웹 서비스 API를 사용하여 권한이 활성화된 양식을 렌더링할 때 양식에 파일을 첨부할 수 없습니다.

**클라이언트 웹 브라우저에 양식 데이터 스트림 작성**

Forms 서비스가 권한이 활성화된 양식을 렌더링하면 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림을 반환합니다. 클라이언트 웹 브라우저에 작성하면 사용자가 양식을 볼 수 있습니다. Adobe Reader에서 권한이 활성화된 양식을 보는 사용자는 해당 양식에 대해 활성화된 작업을 수행할 수 있습니다.

**참고 항목**

[Java API를 사용하여 권한 지원 양식 렌더링](#render-rights-enabled-forms-using-the-java-api)

[웹 서비스 API 파섹](#render-rights-enabled-forms-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API 빠른 시작](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[인터랙티브한 PDF 양식 렌더링](/help/forms/developing/rendering-interactive-pdf-forms.md)

[양식을 렌더링하는 웹 애플리케이션 만들기](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java API를 사용하여 권한 지원 양식 렌더링 {#render-rights-enabled-forms-using-the-java-api}

양식 API(Java)를 사용하여 권한 지원 양식을 렌더링합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-forms-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. Forms 클라이언트 API 개체 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 객체를 전달하여 `FormsServiceClient` 객체를 만듭니다 `ServiceClientFactory` .

1. 사용 권한 런타임 옵션 설정

   * 생성자를 사용하여 `ReaderExtensionSpec` 객체를 만듭니다.
   * 개체의 `ReaderExtensionSpec` `setReCredentialAlias` 메서드를 호출하여 자격 증명의 별칭을 지정하고 별칭 값을 나타내는 문자열 값을 지정합니다.
   * 개체에 속하는 해당 메서드를 호출하여 각 사용 권한을 `ReaderExtensionSpec` 설정합니다. 그러나 참조한 자격 증명에서만 사용 권한을 설정할 수 있습니다. 즉, 자격 증명으로 설정할 수 없는 경우 사용 권한을 설정할 수 없습니다. 예. 사용자가 양식 필드를 입력하고 양식을 저장할 수 있는 사용 권한을 설정하려면 `ReaderExtensionSpec` 개체의 `setReFillIn` 메서드를 호출하고 전달하십시오 `true`.
   >[!NOTE]
   >
   >객체의 `ReaderExtensionSpec` `setReCredentialPassword` 메서드를 호출할 필요는 없습니다. 이 메서드는 Forms 서비스에서 사용하지 않습니다.

1. 권한 사용 양식 렌더링

   객체의 `FormsServiceClient` `renderPDFFormWithUsageRights` 메서드를 호출하고 다음 값을 전달합니다.

   * 파일 이름 확장자를 포함하여 양식 디자인 이름을 지정하는 문자열 값입니다. Forms 응용 프로그램에 포함된 양식 디자인을 참조하는 경우 전체 경로(예: `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`예:
   * 양식과 병합할 데이터가 들어 있는 `com.adobe.idp.Document` 개체입니다. 데이터를 병합하지 않으려면 빈 `com.adobe.idp.Document` 개체를 전달합니다.
   * 런타임 옵션을 저장하는 `PDFFormRenderSpec` 개체입니다.
   * 사용 권한 런타임 옵션을 저장하는 `ReaderExtensionSpec` 개체입니다.
   * Forms 서비스에 필요한 URI 값이 들어 있는 `URLSpec` 개체입니다.
   이 `renderPDFFormWithUsageRights` 메서드는 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림을 포함하는 `FormsResult` 개체를 반환합니다.

1. 클라이언트 웹 브라우저에 양식 데이터 스트림 작성

   * 개체 &#39;s `com.adobe.idp.Document` `FormsResult` `getOutputContent` 메서드를 호출하여 개체를 만듭니다.
   * 해당 `com.adobe.idp.Document` `getContentType` 메서드를 호출하여 개체의 콘텐츠 형식을 가져옵니다.
   * 해당 `javax.servlet.http.HttpServletResponse` 메서드를 호출하고 `setContentType` `com.adobe.idp.Document` 개체의 콘텐츠 형식을 전달하여 개체의 콘텐츠 형식을 설정합니다.
   * 개체의 `javax.servlet.ServletOutputStream` `javax.servlet.http.HttpServletResponse` `getOutputStream` 메서드를 호출하여 양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰는 데 사용되는 개체를 만듭니다.
   * 개체의 `java.io.InputStream` `com.adobe.idp.Document` `getInputStream` 메서드를 호출하여 개체를 만듭니다.
   * 바이트 배열을 만들어 `InputStream` 개체의 `read` 메서드를 호출하고 바이트 배열을 인수로 전달하여 양식 데이터 스트림으로 채웁니다.
   * 양식 데이터 스트림을 클라이언트 웹 브라우저로 전송하려면 `javax.servlet.ServletOutputStream` 개체의 `write` 메서드를 호출합니다. 바이트 배열을 `write` 메서드에 전달합니다.

**참고 항목**

[빠른 시작(SOAP 모드):Java API를 사용하여 권한 지원 양식 렌더링](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-rights-enabled-form-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API 파섹 {#render-rights-enabled-forms-using-the-web-service-api}

Forms API(웹 서비스)를 사용하여 권한 지원 양식을 렌더링합니다.

1. 프로젝트 파일 포함

   * Forms 서비스 WSDL을 사용하는 Java 프록시 클래스를 만듭니다.
   * 클래스 경로에 Java 프록시 클래스를 포함합니다.

1. Forms 클라이언트 API 개체 만들기

   객체를 만들고 인증 값을 `FormsService` 설정합니다.

1. 사용 권한 런타임 옵션 설정

   * 생성자를 사용하여 `ReaderExtensionSpec` 객체를 만듭니다.
   * 개체의 `ReaderExtensionSpec` `setReCredentialAlias` 메서드를 호출하여 자격 증명의 별칭을 지정하고 별칭 값을 나타내는 문자열 값을 지정합니다.
   * 개체에 속하는 해당 메서드를 호출하여 각 사용 권한을 `ReaderExtensionSpec` 설정합니다. 그러나 참조한 자격 증명에서만 사용 권한을 설정할 수 있습니다. 즉, 자격 증명으로 설정할 수 없는 경우 사용 권한을 설정할 수 없습니다. 사용자가 양식 필드를 입력하고 양식을 저장할 수 있는 사용 권한을 설정하려면 `ReaderExtensionSpec` 개체의 `setReFillIn` 메서드를 호출하고 전달하십시오 `true`.

1. 권한 사용 양식 렌더링

   객체의 `FormsService` `renderPDFFormWithUsageRights` 메서드를 호출하고 다음 값을 전달합니다.

   * 파일 이름 확장자를 포함하여 양식 디자인 이름을 지정하는 문자열 값입니다. Forms 응용 프로그램에 포함된 양식 디자인을 참조하는 경우 전체 경로(예: `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`예:
   * 양식과 병합할 데이터가 들어 있는 `BLOB` 개체입니다. 데이터를 양식과 병합하지 않으려면 빈 XML 데이터 소스를 기반으로 하는 `BLOB` 개체를 전달해야 합니다. null인 `BLOB` 개체는 전달할 수 없습니다.그렇지 않으면 예외가 발생합니다.
   * 런타임 옵션을 저장하는 `PDFFormRenderSpec` 개체입니다.
   * 사용 권한 런타임 옵션을 저장하는 `ReaderExtensionSpec` 개체입니다.
   * Forms 서비스에 필요한 URI 값이 들어 있는 `URLSpec` 개체입니다.
   이 `renderPDFFormWithUsageRights` 메서드는 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림을 포함하는 `FormsResult` 개체를 반환합니다.

1. 클라이언트 웹 브라우저에 양식 데이터 스트림 작성

   * 개체의 `BLOB` `FormsResult` `getOutputContent` 메서드를 호출하여 양식 데이터가 포함된 개체를 만듭니다.
   * 해당 `BLOB` `getContentType` 메서드를 호출하여 개체의 콘텐츠 형식을 가져옵니다.
   * 해당 `javax.servlet.http.HttpServletResponse` 메서드를 호출하고 `setContentType` `BLOB` 개체의 콘텐츠 형식을 전달하여 개체의 콘텐츠 형식을 설정합니다.
   * 개체의 `javax.servlet.ServletOutputStream` `javax.servlet.http.HttpServletResponse` `getOutputStream` 메서드를 호출하여 양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰는 데 사용되는 개체를 만듭니다.
   * 바이트 배열을 만들어 `BLOB` 개체의 `getBinaryData` 메서드를 호출하여 채웁니다. 이 작업은 `FormsResult` 개체의 내용을 바이트 배열에 할당합니다.
   * 양식 데이터 스트림을 클라이언트 웹 브라우저로 전송하려면 `javax.servlet.http.HttpServletResponse` 개체의 `write` 메서드를 호출합니다. 바이트 배열을 `write` 메서드에 전달합니다.

**참고 항목**

[렌더링 권한 사용 양식](#rendering-rights-enabled-forms)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
