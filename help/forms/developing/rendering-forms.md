---
title: Forms 렌더링
seo-title: Forms 렌더링
description: Forms 서비스를 사용하여 Designer에서 일반적으로 작성된 양식을 확인, 처리, 변환 및 제공하는 대화형 데이터 캡처 클라이언트 애플리케이션을 만듭니다. 양식 작성자는 다양한 브라우저 환경에서 Forms 서비스가 PDF, SWF 또는 HTML로 렌더링하는 단일 양식 디자인을 개발할 수 있습니다.
seo-description: Forms 서비스를 사용하여 Designer에서 일반적으로 작성된 양식을 확인, 처리, 변환 및 제공하는 대화형 데이터 캡처 클라이언트 애플리케이션을 만듭니다. 양식 작성자는 다양한 브라우저 환경에서 Forms 서비스가 PDF, SWF 또는 HTML로 렌더링하는 단일 양식 디자인을 개발할 수 있습니다.
uuid: 68d7b7bc-7730-4a83-b7b9-ebe2a29d6c51
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/performing_service_operations_using_apis
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: f8749793-e53f-4812-a093-8278f480e6a8
role: 개발자
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 0%

---


# Forms {#rendering-forms} 렌더링

**이 문서의 샘플과 예는 JEE 환경의 AEM Forms에만 해당됩니다.**

**Forms 서비스 정보**

Forms 서비스를 사용하면 일반적으로 Designer에서 만든 양식을 확인하고 처리, 변환하고 전달하는 대화형 데이터 캡처 클라이언트 애플리케이션을 만들 수 있습니다. 양식 작성자는 다양한 브라우저 환경에서 Forms 서비스가 PDF, SWF 또는 HTML로 렌더링하는 단일 양식 디자인을 개발할 수 있습니다.

최종 사용자가 양식을 요청하면 클라이언트 응용 프로그램은 해당 양식을 적절한 형식으로 반환하는 요청을 Forms 서비스에 보냅니다. Forms 서비스는 요청을 받자마자 데이터를 양식 디자인과 병합한 다음 원하는 형식으로 양식을 전달합니다. 양식 서비스 출력은 일반적으로 PDF 문서인 대화형 양식입니다. 대화형 양식을 사용하면 양식에 있는 필드를 채울 수 있습니다.

클라이언트 응용 프로그램 유형에 따라 양식을 클라이언트 웹 브라우저에 작성하거나 양식을 PDF 파일로 저장할 수 있습니다. 웹 기반 응용 프로그램은 웹 브라우저에 양식을 작성할 수 있습니다. 데스크톱 응용 프로그램은 양식을 PDF 파일로 저장할 수 있습니다. 웹 브라우저와 PDF 파일에 쓰는 방법을 보여주기 위해 *Forms 렌더링* 섹션에 있는 빠른 시작은 다음과 같은 방식으로 구성됩니다.

* Java API가 강력한 입력(SOAP 모드) 예는 Java 서블릿입니다.
* 웹 서비스(Java Base64) 예는 Java 서블릿입니다.
* 웹 서비스(MTOM) 예는 콘솔 응용 프로그램입니다(일부 빠른 시작에는 MTOM 예제가 없는 경우).

>[!NOTE]
>
>Forms 서비스를 호출하는 데 java 서블릿을 사용하는 웹 응용 프로그램을 만드는 방법에 대한 자세한 내용은 [Forms](/help/forms/developing/creating-web-applications-renders-forms.md)를 렌더링하는 웹 응용 프로그램 만들기를 참조하십시오.

다음 두 가지 방법 중 하나를 사용하여 양식 디자인(XDP 파일) 또는 PDF 문서를 Forms 서비스로 전달할 수 있습니다.

* URL 값을 사용하여 양식 디자인을 참조할 수 있습니다. 이 접근 방식은 `URLSpec` 개체를 사용하는 것과 관련됩니다. 내용 루트는 `URLSpec` 개체의 `setContentRootURI` 메서드를 사용하여 Forms 서비스로 전달됩니다. 양식 디자인 이름( `formQuery`)은 별도의 매개 변수로 전달됩니다. 두 값이 연결되어 양식 디자인에 대한 절대 참조를 가져옵니다. (*Forms 렌더링* 섹션에 있는 대부분의 빠른 시작은 이 방법을 사용합니다.)
* 양식 디자인이 포함된 `com.adobe.idp.Document`을 Forms 서비스에 전달할 수 있습니다. `renderPDFForm2` 및 `renderHTMLForm2`이라는 이름의 새 두 메서드는 양식 디자인을 포함하는 `com.adobe.idp.Document` 객체를 허용합니다. ([Forms 서비스에 문서 전달](/help/forms/developing/passing-documents-forms-service.md) 참조)

Forms 서비스를 사용하여 다음 작업을 수행할 수 있습니다.

* 인터랙티브한 PDF forms 렌더링 ([대화형 PDF forms 렌더링](/help/forms/developing/rendering-interactive-pdf-forms.md)을 참조하십시오.)
* 클라이언트에서 양식을 렌더링합니다. (](/help/forms/developing/rendering-forms-client.md) 클라이언트에서 Forms 렌더링 참조)[
* 조각을 기반으로 양식 렌더링 자세한 내용은 [조각을 기준으로 Forms 렌더링](/help/forms/developing/rendering-forms-based-fragments.md)을 참조하십시오.
* 권한이 활성화된 양식을 렌더링할 수 있습니다. ([렌더링 권한 사용 Forms](/help/forms/developing/rendering-rights-enabled-forms.md)을 참조하십시오.)
* 양식을 HTML로 렌더링합니다. (HTML](/help/forms/developing/rendering-forms-html.md)로 Forms 렌더링 참조)[
* 사용자 지정 CSS 파일을 사용하여 HTML Forms 렌더링([사용자 지정 CSS 파일을 사용하여 HTML Forms 렌더링](/help/forms/developing/rendering-html-forms-using-custom.md)).
* 제출된 양식을 처리할 수 있습니다. ([제출된 Forms 처리](/help/forms/developing/handling-submitted-forms.md)를 참조하십시오.)
* 제출된 XML 데이터를 사용하여 PDF 문서 만들기. ([제출된 XML 데이터가 있는 PDF 문서 만들기](/help/forms/developing/creating-pdf-documents-submitted-xml.md)를 참조하십시오.)
* 양식 미리 채우기 ([플로우 가능한 레이아웃으로 Forms 미리 채우기](/help/forms/developing/prepopulating-forms-flowable-layouts.md)를 참조하십시오.)
* 문서 전달. ([Forms 서비스에 문서 전달](/help/forms/developing/passing-documents-forms-service.md) 참조)
* 양식 데이터를 계산합니다. ([양식 데이터 계산](/help/forms/developing/calculating-form-data.md)을 참조하십시오.)
* 애플리케이션 최적화 ([Forms 서비스의 성능 최적화](/help/forms/developing/optimizing-performance-forms-service.md)를 참조하십시오.)

   ***팁&#x200B;**:Adobe 개발자 웹 사이트에는 Forms 서비스를 호출하고 양식을 렌더링하는 ASP.NET 응용 프로그램을 만드는 방법에 대해 설명하는 다음 문서가 포함되어 있습니다. [양식 렌더링 ASP.NET 응용 프로그램 만들기](https://www.adobe.com/devnet/livecycle/articles/asp_net.html)를 참조하십시오.*

