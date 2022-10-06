---
title: Forms 렌더링
seo-title: Rendering Forms
description: Forms 서비스를 사용하여 일반적으로 Designer에서 만든 양식을 확인, 처리, 변환 및 전달하는 대화형 데이터 캡처 클라이언트 애플리케이션을 만듭니다. 양식 작성자는 Forms 서비스가 다양한 브라우저 환경에서 PDF, SWF 또는 HTML에서 렌더링하는 단일 양식 디자인을 개발할 수 있습니다.
seo-description: Use the Forms service to create interactive data capture client applications that validate, process, transform, and deliver forms typically created in Designer. Form authors can develop a single form design that the Forms service renders in PDF, SWF, or HTML in various browser environments.
uuid: 68d7b7bc-7730-4a83-b7b9-ebe2a29d6c51
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/performing_service_operations_using_apis
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: f8749793-e53f-4812-a093-8278f480e6a8
role: Developer
exl-id: ec9ccf04-7cec-493a-91ab-0e399a905338
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---

# Forms 렌더링 {#rendering-forms}

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms용입니다.**

**Forms 서비스 정보**

Forms 서비스를 사용하면 일반적으로 Designer에서 만든 양식을 확인, 처리, 변환 및 전달하는 대화형 데이터 캡처 클라이언트 응용 프로그램을 만들 수 있습니다. 양식 작성자는 Forms 서비스가 다양한 브라우저 환경에서 PDF, SWF 또는 HTML에서 렌더링하는 단일 양식 디자인을 개발할 수 있습니다.

최종 사용자가 양식을 요청하면 클라이언트 애플리케이션은 요청을 Forms 서비스로 보내어 양식을 적절한 형식으로 반환합니다. Forms 서비스는 요청을 받는 즉시 데이터를 양식 디자인과 병합한 다음 원하는 형식으로 양식을 전달합니다. 양식 서비스 출력은 대화형 양식이며 일반적으로 PDF 문서입니다. 대화형 양식을 사용하면 양식에 있는 필드를 채울 수 있습니다.

클라이언트 응용 프로그램 유형에 따라 양식을 클라이언트 웹 브라우저에 작성하거나 PDF 파일로 저장할 수 있습니다. 웹 기반 응용 프로그램은 웹 브라우저에 양식을 작성할 수 있습니다. 데스크탑 응용 프로그램은 양식을 PDF 파일로 저장할 수 있습니다. 웹 브라우저 및 PDF 파일에 쓰는 방법을 보여주기 위해 *Forms 렌더링* 섹션은 다음과 같은 방식으로 구성됩니다.

* Java API가 강력한 입력(SOAP 모드) 예는 Java 서블릿입니다.
* 웹 서비스(Java Base64) 예제는 Java 서블릿입니다.
* 웹 서비스(MTOM) 예제는 콘솔 애플리케이션입니다(일부 빠른 시작에 MTOM 예가 있는 것은 아님).

>[!NOTE]
>
>java 서블릿을 사용하여 Forms 서비스를 호출하는 웹 애플리케이션을 만드는 방법에 대한 자세한 내용은 [Forms을 렌더링하는 웹 애플리케이션 만들기](/help/forms/developing/creating-web-applications-renders-forms.md).

다음 두 가지 방법 중 하나를 사용하여 양식 디자인(XDP 파일) 또는 PDF 문서를 Forms 서비스에 전달할 수 있습니다.

* URL 값을 사용하여 양식 디자인을 참조할 수 있습니다. 이 방법에는 `URLSpec` 개체. 컨텐츠 루트가 을 사용하여 Forms 서비스에 전달됩니다 `URLSpec` 개체 `setContentRootURI` 메서드를 사용합니다. 양식 디자인 이름( `formQuery`)가 별도의 매개 변수로 전달됩니다. 양식 디자인에 대한 절대 참조를 가져오기 위해 두 값이 연결됩니다. (대부분의 빠른 시작은 *Forms 렌더링* 섹션에서 이 접근 방식을 사용합니다.)
* 다음 정보를 `com.adobe.idp.Document` 여기에는 Forms 서비스에 대한 양식 디자인이 포함되어 있습니다. 이름이 `renderPDFForm2` 및 `renderHTMLForm2` 동의 `com.adobe.idp.Document` 양식 디자인이 포함된 객체입니다. (자세한 내용은 [Forms 서비스에 문서 전달](/help/forms/developing/passing-documents-forms-service.md)

Forms 서비스를 사용하여 다음 작업을 수행할 수 있습니다.

* 대화형 PDF forms 렌더링. (자세한 내용은 [대화형 PDF forms 렌더링](/help/forms/developing/rendering-interactive-pdf-forms.md))
* 클라이언트에서 양식을 렌더링합니다. (자세한 내용은 [클라이언트에서 Forms 렌더링](/help/forms/developing/rendering-forms-client.md))
* 조각을 기반으로 양식을 렌더링합니다. (자세한 내용은 [조각을 기반으로 Forms 렌더링](/help/forms/developing/rendering-forms-based-fragments.md))
* 권한이 활성화된 양식을 렌더링합니다. (자세한 내용은 [렌더링 권한 사용 Forms](/help/forms/developing/rendering-rights-enabled-forms.md))
* 양식을 HTML으로 렌더링합니다. (자세한 내용은 [Forms을 HTML으로 렌더링](/help/forms/developing/rendering-forms-html.md))
* 사용자 지정 CSS 파일을 사용하여 HTML Forms 렌더링([사용자 지정 CSS 파일을 사용하여 HTML Forms 렌더링](/help/forms/developing/rendering-html-forms-using-custom.md))
* 제출된 양식을 처리합니다. (자세한 내용은 [제출된 Forms 처리](/help/forms/developing/handling-submitted-forms.md))
* 제출된 XML 데이터를 사용하여 PDF 문서 만들기 (자세한 내용은 [제출된 XML 데이터를 사용하여 PDF 문서 만들기](/help/forms/developing/creating-pdf-documents-submitted-xml.md))
* 양식을 미리 채웁니다. (자세한 내용은 [유동형 레이아웃으로 Forms 미리 채우기](/help/forms/developing/prepopulating-forms-flowable-layouts.md))
* 문서 전달. (자세한 내용은 [Forms 서비스에 문서 전달](/help/forms/developing/passing-documents-forms-service.md)
* 양식 데이터를 계산합니다. (자세한 내용은 [양식 데이터 계산](/help/forms/developing/calculating-form-data.md))
* 애플리케이션을 최적화합니다. (자세한 내용은 [Forms 서비스의 성능 최적화](/help/forms/developing/optimizing-performance-forms-service.md))
