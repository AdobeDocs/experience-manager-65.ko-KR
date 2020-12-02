---
title: 조각을 기반으로 Forms 렌더링
seo-title: 조각을 기반으로 Forms 렌더링
description: 'null'
seo-description: 'null'
uuid: 9c9a730d-f970-41f8-afed-4e6b6d3d393d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: a65c5303-0ebd-43a9-a777-401042d8fcad
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7
workflow-type: tm+mt
source-wordcount: '2187'
ht-degree: 0%

---


# 조각 {#rendering-forms-based-on-fragments}에 따라 Forms 렌더링

## 조각 {#rendering-forms-based-on-fragments-inner}에 따라 Forms 렌더링

Forms 서비스는 Designer를 사용하여 만드는 조각을 기반으로 양식을 렌더링할 수 있습니다. *조각*&#x200B;은 양식의 재사용 가능한 부분으로서, 여러 양식 디자인에 삽입할 수 있는 별도의 XDP 파일로 저장됩니다. 예를 들어, 조각에 주소 블록 또는 법적 텍스트가 포함될 수 있습니다.

조각을 사용하면 다수의 양식을 간단하게 만들고 유지 관리할 수 있습니다. 새 양식을 만들 때 필요한 조각에 대한 참조를 삽입하면 해당 조각이 양식에 나타납니다. 조각 참조에는 물리적 XDP 파일을 가리키는 하위 양식이 포함되어 있습니다. 조각을 기반으로 양식 디자인을 만드는 방법에 대한 자세한 내용은 [Forms 디자이너](https://www.adobe.com/go/learn_aemforms_designer_63)를 참조하십시오.

조각에는 선택 하위 폼 세트로 둘러싸인 여러 하위 양식이 포함될 수 있습니다. 선택 하위 폼 세트는 데이터 연결에서의 데이터 흐름을 기준으로 하위 폼의 표시를 제어합니다. 조건문을 사용하여 제공된 양식에 있는 세트 내에서 어떤 하위 양식이 나타나는지 결정합니다. 예를 들어 세트의 각 하위 폼에는 특정 지리적 위치에 대한 정보가 포함될 수 있으며 표시되는 하위 폼은 사용자의 위치에 따라 결정될 수 있습니다.

*스크립트 조각*&#x200B;에는 날짜 파서 또는 웹 서비스 호출과 같은 특정 개체와 별도로 저장되는 재사용 가능한 JavaScript 함수 또는 값이 포함되어 있습니다. 이러한 조각에는 [계층] 팔레트에서 변수의 자식으로 표시되는 단일 스크립트 개체가 포함됩니다. 유효성 검사, 계산 또는 초기화와 같은 이벤트 스크립트와 같은 다른 개체의 속성인 스크립트에서 조각을 만들 수 없습니다.

조각을 사용하면 다음과 같은 이점이 있습니다.

* **컨텐츠 재사용**:조각을 사용하여 여러 양식 디자인에 컨텐츠를 재사용할 수 있습니다. 여러 양식에 동일한 컨텐츠 중 일부를 사용해야 하는 경우 컨텐츠를 복사하거나 다시 만드는 것보다 조각을 사용하는 것이 빠르고 간단합니다. 조각을 사용하면 양식 디자인의 자주 사용되는 부분이 모든 참조 양식에 일관된 내용과 모양이 유지되도록 할 수 있습니다.
* **전역 업데이트**:조각을 사용하면 하나의 파일에서 여러 양식에 대한 전체 변경을 한 번만 수행할 수 있습니다. 조각에서 컨텐츠, 스크립트 객체, 데이터 바인딩, 레이아웃 또는 스타일을 변경할 수 있으며 조각을 참조하는 모든 XDP 양식은 변경 사항을 반영합니다.
* 예를 들어 여러 양식에 있는 공통 요소는 해당 국가의 드롭다운 목록 개체를 포함하는 주소 블록일 수 있습니다. 드롭다운 목록 개체의 값을 업데이트해야 하는 경우 많은 양식을 열어 변경해야 합니다. 조각의 주소 블록을 포함하는 경우 한 조각 파일만 열어 변경하면 됩니다.
* PDF 양식의 조각을 업데이트하려면 Designer에서 양식을 다시 저장해야 합니다.
* **공유 양식 작성**:조각을 사용하여 여러 리소스 간에 양식 작성을 공유할 수 있습니다. 스크립팅 또는 Designer의 기타 고급 기능에 대한 전문 지식이 있는 양식 개발자는 스크립팅과 동적 속성을 활용하는 조각을 개발하고 공유할 수 있습니다. 양식 디자이너는 이러한 파편을 사용하여 양식 디자인의 레이아웃을 작성할 수 있고 여러 사람이 디자인한 여러 양식에 걸쳐 양식의 모든 부분이 일관된 모양과 기능을 유지할 수 있습니다.

### 조각 {#assembling-a-form-design-assembled-using-fragments}을(를) 사용하여 어셈블된 양식 디자인 취합

양식 디자인을 취합하여 여러 조각을 기반으로 Forms 서비스로 전달할 수 있습니다. 여러 조각을 어셈블하려면 어셈블러 서비스를 사용하십시오. 다른 Forms 서비스(출력 서비스)에서 사용하는 양식 디자인을 만들기 위해 조합 서비스를 사용하는 예를 보려면 [조각을 사용하여 PDF 문서 만들기](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)를 참조하십시오. 출력 서비스를 사용하는 대신 Forms 서비스를 사용하여 동일한 워크플로우를 수행할 수 있습니다.

어셈블러 서비스를 사용할 때 조각을 사용하여 어셈블된 양식 디자인을 전달합니다. 만들어진 양식 디자인이 다른 조각을 참조하지 않습니다. 반면 이 항목에서는 다른 조각을 Forms 서비스에 참조하는 양식 디자인 전달에 대해 설명합니다. 그러나 양식 디자인이 어셈블러에서 어셈블리되지 않았습니다. 디자이너에 의해 제작되었습니다.

>[!NOTE]
>
>Forms 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

>[!NOTE]
>
>조각을 기반으로 양식을 렌더링하는 웹 기반 응용 프로그램을 만드는 방법에 대한 자세한 내용은 [Forms을 렌더링하는 웹 응용 프로그램 만들기](/help/forms/developing/creating-web-applications-renders-forms.md)를 참조하십시오.

### {#summary-of-steps} 단계 요약

조각을 기반으로 양식을 렌더링하려면 다음 작업을 수행합니다.

1. 프로젝트 파일 포함
1. Forms 클라이언트 API 개체를 만듭니다.
1. URI 값을 지정합니다.
1. 양식을 렌더링합니다.
1. 양식 데이터 스트림을 클라이언트 웹 브라우저에 씁니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Forms 클라이언트 API 개체 만들기**

Forms 서비스 클라이언트 API 작업을 프로그래밍 방식으로 수행하려면 먼저 Forms 서비스 클라이언트를 만들어야 합니다.

**URI 값 지정**

조각을 기반으로 양식을 성공적으로 렌더링하려면, Forms 서비스가 양식 디자인이 참조하는 양식과 조각(XDP 파일)을 모두 찾을 수 있는지 확인해야 합니다. 예를 들어 양식의 이름이 PO.xdp이고 이 양식에서는 FooterUS.xdp 및 FooterCanada.xdp라는 두 개의 조각을 사용한다고 가정합니다. 이러한 경우 Forms 서비스는 세 개의 XDP 파일을 모두 찾을 수 있어야 합니다.

한 위치에 양식을 배치하고 다른 위치에 조각을 배치하여 양식과 해당 조각을 구성하거나 모든 XDP 파일을 동일한 위치에 배치할 수 있습니다. 이 섹션의 목적에 따라 모든 XDP 파일이 AEM Forms 저장소에 있다고 가정합니다. AEM Forms 저장소에 XDP 파일 배치에 대한 자세한 내용은 [리소스 작성](/help/forms/developing/aem-forms-repository.md#writing-resources)을 참조하십시오.

조각을 기반으로 양식을 렌더링할 때는 조각 자체만 참조하고 조각 자체는 참조하지 않아야 합니다. 예를 들어 FooterUS.xdp 또는 FooterCanada.xdp가 아닌 PO.xdp를 참조해야 합니다. 파편을 Forms 서비스가 파편을 찾을 수 있는 위치에 배치합니다.

**양식 렌더링**

조각에 기반한 양식은 조각화되지 않은 양식과 동일한 방식으로 렌더링할 수 있습니다. 즉, 양식을 PDF, HTML 또는 양식 안내선으로 렌더링할 수 있습니다(더 이상 사용되지 않음). 이 섹션의 예에서는 조각을 기반으로 하는 양식을 인터랙티브한 PDF 양식으로 렌더링합니다. ([대화형 PDF forms 렌더링](/help/forms/developing/rendering-interactive-pdf-forms.md)을 참조하십시오.)

**양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰기**

Forms 서비스가 양식을 렌더링하면 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림을 반환합니다. 클라이언트 웹 브라우저에 작성할 때 양식이 사용자에게 표시됩니다.

**참고 항목**

[Java API를 사용하여 조각을 기반으로 양식 렌더링](#render-forms-based-on-fragments-using-the-java-api)

[웹 서비스 API를 사용하여 조각을 기반으로 양식 렌더링](#render-forms-based-on-fragments-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms 서비스 API 빠른 시작](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[대화형 PDF forms 렌더링](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Forms을 렌더링하는 웹 애플리케이션 만들기](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java API {#render-forms-based-on-fragments-using-the-java-api}를 사용하여 조각을 기반으로 양식 렌더링

Forms API(Java)를 사용하여 조각을 기반으로 양식을 렌더링합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-forms-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. Forms 클라이언트 API 개체 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 `FormsServiceClient` 개체를 만들고 `ServiceClientFactory` 개체를 전달합니다.

1. URI 값 지정

   * 생성자를 사용하여 URI 값을 저장하는 `URLSpec` 개체를 만듭니다.
   * `URLSpec` 개체의 `setApplicationWebRoot` 메서드를 호출하고 응용 프로그램의 웹 루트를 나타내는 문자열 값을 전달합니다.
   * `URLSpec` 개체의 `setContentRootURI` 메서드를 호출하고 콘텐츠 루트 URI 값을 지정하는 문자열 값을 전달합니다. 양식 디자인과 조각이 컨텐츠 루트 URI에 있는지 확인합니다. 그렇지 않을 경우 Forms 서비스는 예외를 throw합니다. 리포지토리를 참조하려면 `repository://`을 지정합니다.
   * `URLSpec` 개체의 `setTargetURL` 메서드를 호출하고 양식 데이터가 게시된 위치에 대상 URL 값을 지정하는 문자열 값을 전달합니다. 양식 디자인에서 대상 URL을 정의하는 경우 빈 문자열을 전달할 수 있습니다. 계산을 수행하기 위해 양식이 전송되는 URL을 지정할 수도 있습니다.

1. 양식 렌더링

   `FormsServiceClient` 개체의 `renderPDFForm` 메서드를 호출하고 다음 값을 전달합니다.

   * 파일 이름 확장자를 포함하여 양식 디자인 이름을 지정하는 문자열 값. Forms 응용 프로그램의 일부인 양식 디자인을 참조하는 경우 전체 경로를 지정해야 합니다(예: `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`).
   * 양식과 병합할 데이터가 포함된 `com.adobe.idp.Document` 개체입니다. 데이터를 병합하지 않으려면 빈 `com.adobe.idp.Document` 개체를 전달합니다.
   * 런타임 옵션을 저장하는 `PDFFormRenderSpec` 개체입니다.
   * 조각을 기반으로 양식을 렌더링하는 데 필요한 URI 값이 포함된 `URLSpec` 개체
   * 첨부 파일을 저장하는 `java.util.HashMap` 개체입니다. 이 매개 변수는 선택 사항이며, 양식에 파일을 첨부하지 않으려는 경우 `null`을 지정할 수 있습니다.

   `renderPDFForm` 메서드는 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림을 포함하는 `FormsResult` 개체를 반환합니다.

1. 양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰기

   * `FormsResult` 개체 &#39;s `getOutputContent` 메서드를 호출하여 `com.adobe.idp.Document` 개체를 만듭니다.
   * `getContentType` 메서드를 호출하여 `com.adobe.idp.Document` 개체의 콘텐츠 유형을 가져옵니다.
   * `setContentType` 메서드를 호출하고 `com.adobe.idp.Document` 개체의 콘텐츠 형식을 전달하여 `javax.servlet.http.HttpServletResponse` 개체의 콘텐츠 형식을 설정합니다.
   * `javax.servlet.http.HttpServletResponse` 개체의 `getOutputStream` 메서드를 호출하여 양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰는 데 사용되는 `javax.servlet.ServletOutputStream` 개체를 만듭니다.
   * `com.adobe.idp.Document` 개체의 `getInputStream` 메서드를 호출하여 `java.io.InputStream` 개체를 만듭니다.
   * 바이트 배열을 만들면 `InputStream` 개체의 `read` 메서드를 호출하고 바이트 배열을 인수로 전달하여 양식 데이터 스트림으로 이 배열을 채웁니다.
   * 양식 데이터 스트림을 클라이언트 웹 브라우저에 보내려면 `javax.servlet.ServletOutputStream` 개체의 `write` 메서드를 호출합니다. 바이트 배열을 `write` 메서드에 전달합니다.

**참고 항목**

[조각을 기반으로 Forms 렌더링](#rendering-forms-based-on-fragments)

[빠른 시작(SOAP 모드):Java API를 사용하여 조각을 기반으로 양식 렌더링](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-based-on-fragments-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API {#render-forms-based-on-fragments-using-the-web-service-api}를 사용하여 조각을 기반으로 양식 렌더링

Forms API(웹 서비스)를 사용하여 조각을 기반으로 양식을 렌더링합니다.

1. 프로젝트 파일 포함

   * Forms 서비스 WSDL을 사용하는 Java 프록시 클래스를 만듭니다.
   * 클래스 경로에 Java 프록시 클래스를 포함합니다.

1. Forms 클라이언트 API 개체 만들기

   `FormsService` 개체를 만들고 인증 값을 설정합니다.

1. URI 값 지정

   * 생성자를 사용하여 URI 값을 저장하는 `URLSpec` 개체를 만듭니다.
   * `URLSpec` 개체의 `setApplicationWebRoot` 메서드를 호출하고 응용 프로그램의 웹 루트를 나타내는 문자열 값을 전달합니다.
   * `URLSpec` 개체의 `setContentRootURI` 메서드를 호출하고 콘텐츠 루트 URI 값을 지정하는 문자열 값을 전달합니다. 양식 디자인이 컨텐츠 루트 URI에 있는지 확인합니다. 그렇지 않을 경우 Forms 서비스는 예외를 throw합니다. 리포지토리를 참조하려면 `repository://`을 지정합니다.
   * `URLSpec` 개체의 `setTargetURL` 메서드를 호출하고 양식 데이터가 게시된 위치에 대상 URL 값을 지정하는 문자열 값을 전달합니다. 양식 디자인에서 대상 URL을 정의하는 경우 빈 문자열을 전달할 수 있습니다. 계산을 수행하기 위해 양식이 전송되는 URL을 지정할 수도 있습니다.

1. 양식 렌더링

   `FormsService` 개체의 `renderPDFForm` 메서드를 호출하고 다음 값을 전달합니다.

   * 파일 이름 확장자를 포함하여 양식 디자인 이름을 지정하는 문자열 값. Forms 응용 프로그램의 일부인 양식 디자인을 참조하는 경우 전체 경로를 지정해야 합니다(예: `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`).
   * 양식과 병합할 데이터가 포함된 `BLOB` 개체입니다. 데이터를 병합하지 않으려면 `null`을 전달합니다.
   * 런타임 옵션을 저장하는 `PDFFormRenderSpec` 개체입니다. 입력 문서가 PDF 문서인 경우 태그 지정된 PDF 옵션을 설정할 수 없습니다. 입력 파일이 XDP 파일인 경우 태그 있는 PDF 옵션을 설정할 수 있습니다.
   * Forms 서비스에 필요한 URI 값을 포함하는 `URLSpec` 개체
   * 첨부 파일을 저장하는 `java.util.HashMap` 개체입니다. 이 매개 변수는 선택 사항이며, 양식에 파일을 첨부하지 않으려는 경우 `null`을 지정할 수 있습니다.
   * 메서드로 채워진 빈 `com.adobe.idp.services.holders.BLOBHolder` 개체입니다. 이 매개 변수는 렌더링된 양식을 저장하는 데 사용됩니다.
   * 메서드로 채워진 빈 `javax.xml.rpc.holders.LongHolder` 개체입니다. 이 인수는 양식의 페이지 수를 저장합니다.
   * 메서드로 채워진 빈 `javax.xml.rpc.holders.StringHolder` 개체입니다. 이 인수는 로케일 값을 저장합니다.
   * 이 작업의 결과를 포함하는 빈 `com.adobe.idp.services.holders.FormsResultHolder` 개체입니다.

   `renderPDFForm` 메서드는 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림으로 마지막 인수 값으로 전달되는 `com.adobe.idp.services.holders.FormsResultHolder` 개체를 채웁니다.

1. 양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰기

   * `com.adobe.idp.services.holders.FormsResultHolder` 개체의 `value` 데이터 멤버의 값을 가져와 `FormResult` 개체를 만듭니다.
   * `FormsResult` 개체의 `getOutputContent` 메서드를 호출하여 양식 데이터를 포함하는 `BLOB` 개체를 만듭니다.
   * `getContentType` 메서드를 호출하여 `BLOB` 개체의 콘텐츠 유형을 가져옵니다.
   * `setContentType` 메서드를 호출하고 `BLOB` 개체의 콘텐츠 형식을 전달하여 `javax.servlet.http.HttpServletResponse` 개체의 콘텐츠 형식을 설정합니다.
   * `javax.servlet.http.HttpServletResponse` 개체의 `getOutputStream` 메서드를 호출하여 양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰는 데 사용되는 `javax.servlet.ServletOutputStream` 개체를 만듭니다.
   * 바이트 배열을 만들고 `BLOB` 개체의 `getBinaryData` 메서드를 호출하여 채웁니다. 이 작업은 바이트 배열에 `FormsResult` 개체의 내용을 할당합니다.
   * 양식 데이터 스트림을 클라이언트 웹 브라우저에 보내려면 `javax.servlet.http.HttpServletResponse` 개체의 `write` 메서드를 호출합니다. 바이트 배열을 `write` 메서드에 전달합니다.

**참고 항목**

[조각을 기반으로 Forms 렌더링](#rendering-forms-based-on-fragments)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
