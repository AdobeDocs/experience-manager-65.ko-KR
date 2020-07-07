---
title: 양식 렌더링
seo-title: 양식 렌더링
description: 'null'
seo-description: 'null'
uuid: 68d7b7bc-7730-4a83-b7b9-ebe2a29d6c51
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/performing_service_operations_using_apis
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: f8749793-e53f-4812-a093-8278f480e6a8
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---


# 양식 렌더링 {#rendering-forms}

**Forms 서비스 정보**

Forms 서비스를 사용하면 Designer에서 일반적으로 만든 양식의 유효성을 확인하고 처리, 변환하고 전달하는 대화형 데이터 캡처 클라이언트 응용 프로그램을 만들 수 있습니다. 양식 작성자는 Forms 서비스가 다양한 브라우저 환경에서 PDF, SWF 또는 HTML로 렌더링하는 단일 양식 디자인을 개발할 수 있습니다.

최종 사용자가 양식을 요청하면 클라이언트 응용 프로그램은 해당 양식을 적합한 형식으로 반환하는 요청을 Forms 서비스에 보냅니다. 양식 서비스는 요청을 받자마자 데이터를 양식 디자인과 병합한 다음 원하는 형식으로 양식을 전달합니다. 양식 서비스 출력은 일반적으로 PDF 문서인 대화형 양식입니다. 대화형 양식을 사용하면 사용자가 양식에 있는 필드를 채울 수 있습니다.

클라이언트 애플리케이션 유형에 따라 양식을 클라이언트 웹 브라우저에 작성하거나 양식을 PDF 파일로 저장할 수 있습니다. 웹 기반 응용 프로그램은 양식을 웹 브라우저에 작성할 수 있습니다. 데스크탑 애플리케이션에서 양식을 PDF 파일로 저장할 수 있습니다. 웹 브라우저와 PDF 파일에 쓰는 방법을 보여주기 위해 [ *렌더링 양식* ] 섹션에 있는 빠른 시작은 다음과 같은 방법으로 구성됩니다.

* Java API가 강력한 입력(SOAP 모드) 예는 Java 서블릿입니다.
* 웹 서비스(Java Base64) 예는 Java 서블릿입니다.
* 웹 서비스(MTOM) 예는 콘솔 응용 프로그램입니다(일부 빠른 시작 시 MTOM 예제가 있는 것은 아님).

>[!NOTE]
>
>java 서블릿을 사용하여 양식 서비스를 호출하는 웹 응용 프로그램 만들기에 대한 자세한 내용은 [양식을 렌더링하는 웹 응용 프로그램 만들기를 참조하십시오](/help/forms/developing/creating-web-applications-renders-forms.md).

다음 두 가지 방법 중 하나를 사용하여 양식 디자인(XDP 파일) 또는 PDF 문서를 Forms 서비스에 전달할 수 있습니다.

* URL 값을 사용하여 양식 디자인을 참조할 수 있습니다. 이 접근 방식에는 `URLSpec` 개체 사용이 포함됩니다. 컨텐츠 루트는 `URLSpec` 개체의 방법을 사용하여 양식 서비스로 `setContentRootURI` 전달됩니다. 양식 디자인 이름( `formQuery`)은 별도의 매개 변수로 전달됩니다. 양식 디자인에 대한 절대 참조를 가져오기 위해 두 값이 연결됩니다. [양식 렌더링] 섹션에 있는 대부분의 빠른 시작 *은* 이 방법을 사용합니다.
* 양식 디자인이 `com.adobe.idp.Document` 포함된 양식을 양식 서비스로 전달할 수 있습니다. 양식 디자인이 포함된 개체 `renderPDFForm2` 를 `renderHTMLForm2` 수용하고 이름이 `com.adobe.idp.Document` 지정된 두 가지 새로운 메서드입니다. (Forms [Service에 문서 전달 참조](/help/forms/developing/passing-documents-forms-service.md)

양식 서비스를 사용하여 이러한 작업을 수행할 수 있습니다.

* 인터랙티브한 PDF forms 렌더링 (대화형 [PDF forms 렌더링을 참조하십시오](/help/forms/developing/rendering-interactive-pdf-forms.md).)
* 클라이언트에서 양식 렌더링 클라이언트 [에서 양식 렌더링을 참조하십시오](/help/forms/developing/rendering-forms-client.md).
* 조각을 기반으로 양식 렌더링 조각 기반 [양식 렌더링을 참조하십시오](/help/forms/developing/rendering-forms-based-fragments.md).
* 권한 부여 양식을 렌더링합니다. (권한 [사용 양식 렌더링을 참조하십시오](/help/forms/developing/rendering-rights-enabled-forms.md).)
* 양식을 HTML로 렌더링 양식 [렌더링을 HTML로 참조하십시오](/help/forms/developing/rendering-forms-html.md).
* 사용자 지정 CSS 파일을 사용하여 HTML 양식 렌더링(사용자 지정 CSS 파일을[사용하여 HTML 양식 렌더링](/help/forms/developing/rendering-html-forms-using-custom.md))
* 제출된 양식을 처리할 수 있습니다. (제출된 [양식 처리를 참조하십시오](/help/forms/developing/handling-submitted-forms.md).)
* 제출된 XML 데이터를 사용하여 PDF 문서 만들기. ( [제출된 XML 데이터를 사용하여 PDF 문서 만들기를 참조하십시오](/help/forms/developing/creating-pdf-documents-submitted-xml.md).)
* 양식 미리 채우기 ( [순서별 레이아웃으로 양식 미리 채우기](/help/forms/developing/prepopulating-forms-flowable-layouts.md)참조)
* 문서 전달. (Forms [Service에 문서 전달 참조](/help/forms/developing/passing-documents-forms-service.md)
* 양식 데이터를 계산합니다. 양식 데이터 [계산을 참조하십시오](/help/forms/developing/calculating-form-data.md).
* 애플리케이션 최적화 (양식 [서비스의 성능 최적화를 참조하십시오](/help/forms/developing/optimizing-performance-forms-service.md).)

   ***팁&#x200B;**: Adobe 개발자 웹 사이트에는 Forms 서비스를 호출하고 양식을 렌더링하는 ASP.NET 응용 프로그램을 만드는 방법에 대해 설명하는 다음 문서가 포함되어 있습니다. 양식[렌더링 ASP.NET 응용 프로그램 만들기를 참조하십시오](https://www.adobe.com/devnet/livecycle/articles/asp_net.html).*

