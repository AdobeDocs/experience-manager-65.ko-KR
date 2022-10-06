---
title: 제출된 Forms 처리
seo-title: Handling Submitted Forms
description: Forms 서비스를 사용하여 대화형 양식으로 입력된 제출된 데이터를 검색합니다. 사용자는 양식 데이터를 XML, PDF 및 URL UTF-16 형식으로 제출할 수 있습니다.
seo-description: Use the Forms service to retrieve the submitted data entered in an interactive form. The user can submit the form data in XML, PDF, and URL UTF-16 formats.
uuid: 673b28f1-f023-4da8-a6a0-c5ff921c5f5d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 3d838027-6bde-4a71-a428-4d5102f7d799
role: Developer
exl-id: 419335b2-2aae-4e83-98ff-18e61b7efa9c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2904'
ht-degree: 0%

---

# 제출된 Forms 처리 {#handling-submitted-forms}

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms용입니다.**

사용자가 대화형 양식을 채울 수 있도록 하는 웹 기반 응용 프로그램을 사용하려면 데이터를 서버에 다시 제출해야 합니다. Forms 서비스를 사용하여 사용자가 대화형 양식에 입력한 데이터를 검색할 수 있습니다. 데이터를 검색한 후 데이터를 처리하여 비즈니스 요구 사항을 충족할 수 있습니다. 예를 들어, 데이터베이스에 데이터를 저장하고, 데이터를 다른 응용 프로그램으로 보내고, 데이터를 다른 서비스로 보내고, 데이터를 양식 디자인에 병합하고, 웹 브라우저에 데이터를 표시하는 등의 작업을 수행할 수 있습니다.

양식 데이터는 Designer에서 설정된 옵션인 XML 또는 PDF 데이터로 Forms 서비스에 제출됩니다. XML로 제출된 양식을 사용하면 개별 필드 데이터 값을 추출할 수 있습니다. 즉, 사용자가 양식에 입력한 각 양식 필드의 값을 추출할 수 있습니다. PDF 데이터로 제출된 양식은 XML 데이터가 아닌 이진 데이터입니다. 양식을 PDF 파일로 저장하거나 다른 서비스로 보낼 수 있습니다. XML로 제출된 양식에서 데이터를 추출하고 양식 데이터를 사용하여 PDF 문서를 만들려면 다른 AEM Forms 작업을 호출합니다. (자세한 내용은 [제출된 XML 데이터를 사용하여 PDF 문서 만들기](/help/forms/developing/creating-pdf-documents-submitted-xml.md))

다음 다이어그램은 이름이 인 Java 서블릿에 제출되는 데이터를 보여줍니다. `HandleData` 웹 브라우저에 표시되는 대화형 양식에서

![hs_handlesubmit](assets/hs_hs_handlesubmit.png)

다음 표에서는 다이어그램의 단계에 대해 설명합니다.

<table>
 <thead>
  <tr>
   <th><p>단계</p></th>
   <th><p>설명</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>사용자가 대화형 양식을 작성하고 양식의 제출 단추를 클릭합니다.</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>데이터가 <code>HandleData</code> Java 서블릿을 XML 데이터로 포함합니다.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>다음 <code>HandleData</code> Java 서블릿에는 데이터를 검색할 애플리케이션 로직이 포함되어 있습니다.</p></td>
  </tr>
 </tbody>
</table>

## 제출된 XML 데이터 처리 {#handling-submitted-xml-data}

양식 데이터가 XML로 제출되면 제출된 데이터를 나타내는 XML 데이터를 검색할 수 있습니다. 모든 양식 필드는 XML 스키마에 노드로 표시됩니다. 노드 값은 사용자가 입력한 값에 해당합니다. 양식의 각 필드가 XML 데이터 내의 노드로 표시되는 대출 양식을 고려합니다. 각 노드의 값은 사용자가 입력하는 값에 해당합니다. 사용자가 다음 양식에 표시된 데이터로 대출 양식을 채우도록 가정해 보겠습니다.

![hs_loanformdata](assets/hs_hs_loanformdata.png)

다음 그림은 Forms 서비스 클라이언트 API를 사용하여 검색한 해당 XML 데이터를 보여줍니다.

![hs_loandata](assets/hs_hs_loandata.png)

대출 양식의 필드. 이러한 값은 Java XML 클래스를 사용하여 검색할 수 있습니다.

>[!NOTE]
>
>데이터를 XML 데이터로 전송하려면 Designer에서 양식 디자인을 올바르게 구성해야 합니다. XML 데이터를 제출하도록 양식 디자인을 올바르게 구성하려면 양식 디자인에 있는 Submit 단추가 XML 데이터를 제출하도록 설정되어 있는지 확인하십시오. XML 데이터를 제출하기 위한 제출 단추 설정에 대한 자세한 내용은 [AEM Forms 디자이너](https://www.adobe.com/go/learn_aemforms_designer_63).

## 제출된 PDF 데이터 처리 {#handling-submitted-pdf-data}

Forms 서비스를 호출하는 웹 애플리케이션을 고려합니다. Forms 서비스에서 클라이언트 웹 브라우저에 대화형 PDF 양식을 렌더링하면 사용자는 양식을 채워 다시 PDF 데이터로 제출합니다. Forms 서비스가 PDF 데이터를 받으면 PDF 데이터를 다른 서비스로 보내거나 PDF 파일로 저장할 수 있습니다. 다음 다이어그램은 응용 프로그램의 논리 플로우를 보여 줍니다.

![hs_savingforms](assets/hs_hs_savingforms.png)

다음 표에서는 이 다이어그램의 단계를 설명합니다.

<table>
 <thead>
  <tr>
   <th><p>단계</p></th>
   <th><p>설명</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>웹 페이지에는 Forms 서비스를 호출하는 Java 서블릿에 액세스하는 링크가 포함되어 있습니다.</p></td>
  </tr>
  <tr>
   <td><p>2개</p></td>
   <td><p>Forms 서비스는 대화형 PDF 양식을 클라이언트 웹 브라우저에 렌더링합니다.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>사용자가 대화형 양식을 작성하고 제출 단추를 클릭합니다. PDF 데이터로 Forms 서비스에 양식이 다시 제출됩니다. 이 옵션은 디자이너에서 설정됩니다.</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Forms 서비스는 PDF 데이터를 PDF 파일로 저장합니다. </p></td>
  </tr>
 </tbody>
</table>

## 제출된 URL UTF-16 데이터 처리 {#handling-submitted-url-utf-16-data}

양식 데이터가 URL UTF-16 데이터로 제출되면 클라이언트 컴퓨터에 Adobe Reader 또는 Acrobat 8.1 이상이 필요합니다. 또한 양식 디자인에 URL로 인코딩된 데이터(HTTP Post)가 있는 제출 단추가 있고 데이터 인코딩 옵션이 UTF-16인 경우 메모장과 같은 텍스트 편집기에서 양식 디자인을 수정해야 합니다. 인코딩 옵션을 다음 중 하나로 설정할 수 있습니다 `UTF-16LE` 또는 `UTF-16BE` 전송 단추에 사용됩니다. 디자이너는 이 기능을 제공하지 않습니다.

>[!NOTE]
>
>Forms 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

## 단계 요약 {#summary-of-steps}

제출된 양식을 처리하려면 다음 작업을 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. Forms 클라이언트 API 개체를 만듭니다.
1. 양식 데이터를 검색합니다.
1. 양식 제출 시 첨부 파일이 포함되어 있는지 확인합니다.
1. 제출된 데이터를 처리합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함하십시오. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Forms 클라이언트 API 개체 만들기**

Forms 서비스 클라이언트 API 작업을 프로그래밍 방식으로 수행하려면 먼저 Forms 서비스 클라이언트를 만들어야 합니다. Java API를 사용하는 경우 `FormsServiceClient` 개체. Forms 웹 서비스 API를 사용하는 경우 `FormsService` 개체.

**양식 데이터 검색**

제출된 양식 데이터를 검색하려면 `FormsServiceClient` 개체 `processFormSubmission` 메서드를 사용합니다. 이 메서드를 호출할 때 제출된 양식의 컨텐츠 유형을 지정해야 합니다. 클라이언트 웹 브라우저에서 Forms 서비스로 데이터를 제출하면 XML 또는 PDF 데이터로 제출할 수 있습니다. 양식 필드에 입력된 데이터를 검색하려면 데이터를 XML 데이터로 제출할 수 있습니다.

다음 런타임 옵션을 설정하여 PDF 데이터로 제출된 양식에서 양식 필드를 검색할 수도 있습니다.

* 다음 값을 `processFormSubmission` 메서드를 컨텐츠 유형 매개 변수로 사용합니다. `CONTENT_TYPE=application/pdf`.
* 설정 `RenderOptionsSpec` 개체 `PDFToXDP` 값 `true`
* 설정 `RenderOptionsSpec` 개체 `ExportDataFormat` 값 `XMLData`

을 호출할 때 제출된 양식의 콘텐츠 유형을 지정합니다 `processFormSubmission` 메서드를 사용합니다. 다음 목록은 적용 가능한 콘텐츠 유형 값을 지정합니다.

* **텍스트/xml**: PDF 양식이 양식 데이터를 XML로 제출할 때 사용할 콘텐츠 형식을 나타냅니다.
* **application/x-www-form-urlencoded**: HTML 양식에서 데이터를 XML로 제출할 때 사용할 콘텐츠 형식을 나타냅니다.
* **application/pdf**: PDF 양식이 데이터를 PDF으로 제출할 때 사용할 컨텐츠 유형을 나타냅니다.

>[!NOTE]
>
>제출된 Forms 처리 섹션과 연결된 세 개의 해당 빠른 시작이 있습니다. Java API 빠른 시작을 사용하여 PDF으로 제출된 PDF forms 처리 은 제출된 PDF 데이터를 처리하는 방법을 보여줍니다. 이 빠른 시작에 지정된 콘텐츠 유형은 다음과 같습니다. `application/pdf`. Java API 빠른 시작을 사용하여 XML로 제출된 PDF forms 처리 빠른 시작은 PDF 양식에서 제출된 XML 데이터를 처리하는 방법을 보여 줍니다. 이 빠른 시작에 지정된 콘텐츠 유형은 다음과 같습니다. `text/xml`. 마찬가지로, Java API를 사용하여 XML로 제출된 HTML 양식 처리 빠른 시작은 HTML 양식에서 제출된 XML 데이터를 처리하는 방법을 보여 줍니다. 이 빠른 시작에 지정된 컨텐츠 유형은 application/x-www-form-urlencoded입니다.

Forms 서비스에 게시된 양식 데이터를 검색하고 처리 상태를 결정합니다. 즉, 데이터가 Forms 서비스에 전송될 때 Forms 서비스가 데이터 처리를 완료하고 데이터가 처리할 준비가 되었음을 의미하지는 않습니다. 예를 들어, 계산을 수행할 수 있도록 데이터를 Forms 서비스에 제출할 수 있습니다. 계산이 완료되면 양식이 다시 사용자에게 렌더링되고 계산 결과가 표시됩니다. 제출된 데이터를 처리하기 전에 Forms 서비스에서 데이터 처리를 완료했는지 여부를 확인하는 것이 좋습니다.

Forms 서비스는 다음 값을 반환하여 데이터 처리를 완료했는지 여부를 나타냅니다.

* **0(제출):** 제출된 데이터를 처리할 준비가 되었습니다.
* **1(계산):** Forms 서비스가 데이터에 대한 계산 작업을 수행했으며 결과를 사용자에게 다시 렌더링해야 합니다.
* **2(유효성 검사):** Forms 서비스는 양식 데이터의 유효성을 검사했으며 결과를 사용자에게 다시 렌더링해야 합니다.
* **3 (다음):** 현재 페이지가 클라이언트 응용 프로그램에 작성해야 하는 결과로 변경되었습니다.
* **4 (이전)**): 현재 페이지가 클라이언트 응용 프로그램에 작성해야 하는 결과로 변경되었습니다.

>[!NOTE]
>
>계산 및 유효성 검사를 다시 사용자에게 렌더링해야 합니다. (자세한 내용은 [양식 데이터 계산](/help/forms/developing/calculating-form-data.md#calculating-form-data).

**양식 제출 시 첨부 파일이 포함되어 있는지 확인**

Forms 서비스에 제출된 Forms에는 첨부 파일이 포함될 수 있습니다. 예를 들어, 사용자는 Acrobat의 기본 제공 첨부 파일 창을 사용하여 양식과 함께 제출할 첨부 파일을 선택할 수 있습니다. 또한 사용자는 HTML 파일로 렌더링되는 HTML 도구 모음을 사용하여 첨부 파일을 선택할 수도 있습니다.

양식에 첨부 파일이 포함되어 있는지 확인한 후 데이터를 처리할 수 있습니다. 예를 들어 로컬 파일 시스템에 파일 첨부 파일을 저장할 수 있습니다.

>[!NOTE]
>
>첨부 파일을 검색하려면 양식을 PDF 데이터로 제출해야 합니다. 양식이 XML 데이터로 제출되면 첨부 파일이 제출되지 않습니다.

**제출된 데이터 처리**

제출된 데이터의 컨텐츠 유형에 따라 제출된 XML 데이터에서 개별 양식 필드 값을 추출하거나 제출된 PDF 데이터를 PDF 파일로 저장(또는 다른 서비스로 보내기)할 수 있습니다. 개별 양식 필드를 추출하려면 제출된 XML 데이터를 XML 데이터 소스로 변환한 다음 를 사용하여 XML 데이터 소스 값을 검색합니다 `org.w3c.dom` 클래스를 참조하십시오.

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms 서비스 API 빠른 시작](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Forms 서비스에 문서 전달](/help/forms/developing/passing-documents-forms-service.md)

[Forms을 렌더링하는 웹 애플리케이션 만들기](/help/forms/developing/creating-web-applications-renders-forms.md)

## Java API를 사용하여 제출된 양식 처리 {#handle-submitted-forms-using-the-java-api}

Forms API(Java)를 사용하여 제출된 양식을 처리합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-forms-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. Forms 클라이언트 API 개체 만들기

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 객체입니다.
   * 만들기 `FormsServiceClient` 생성자를 사용하여 객체를 전달하고 `ServiceClientFactory` 개체.

1. 양식 데이터 검색

   * Java 서블릿에 게시된 양식 데이터를 검색하려면 `com.adobe.idp.Document` 생성자를 사용하여 객체를 호출하고 `javax.servlet.http.HttpServletResponse` 개체 `getInputStream` 생성자 내에서 메서드를 사용합니다.
   * 만들기 `RenderOptionsSpec` 생성자를 사용하여 개체를 작성합니다. 로케일 값을 `RenderOptionsSpec` 개체 `setLocale` 메서드를 사용하여 로케일 값을 지정하는 문자열 값을 전달합니다.

   >[!NOTE]
   >
   >를 호출하여 Forms 서비스에 제출된 PDF 컨텐츠에서 XDP 또는 XML 데이터를 생성하도록 지시할 수 있습니다 `RenderOptionsSpec` 개체 `setPDF2XDP` 방법 및 전달 `true` 그리고 `setXMLData` 및 전달 `true`. 그런 다음 `FormsResult` 개체 `getOutputXML` xdp/XML 데이터에 해당하는 XML 데이터를 검색하는 메서드입니다. (다음 `FormsResult` 개체는 `processFormSubmission` 다음 하위 단계에 설명된 메서드입니다.

   * 를 호출합니다 `FormsServiceClient` 개체 `processFormSubmission` 메서드를 사용하여 다음 값을 전달합니다.

      * 다음 `com.adobe.idp.Document` 양식 데이터를 포함하는 객체입니다.
      * 모든 관련 HTTP 헤더를 포함하는 환경 변수를 지정하는 문자열 값입니다. 처리할 콘텐츠 유형을 지정합니다. XML 데이터를 처리하려면 이 매개 변수에 다음 문자열 값을 지정합니다. `CONTENT_TYPE=text/xml`. PDF 데이터를 처리하려면 이 매개 변수에 다음 문자열 값을 지정합니다. `CONTENT_TYPE=application/pdf`.
      * 를 지정하는 문자열 값 `HTTP_USER_AGENT` 헤더 값(예: ). `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. 이 매개 변수 값은 선택 사항입니다.
      * A `RenderOptionsSpec` 런타임 옵션을 저장하는 개체입니다.

      다음 `processFormSubmission` 메서드 반환 `FormsResult` 양식 제출 결과가 포함된 객체입니다.

   * 를 호출하여 Forms 서비스가 양식 데이터 처리를 완료했는지 여부를 결정합니다 `FormsResult` 개체 `getAction` 메서드를 사용합니다. 이 메서드가 값을 반환하는 경우 `0`: 데이터를 처리할 준비가 되었습니다.



1. 양식 제출 시 첨부 파일이 포함되어 있는지 확인

   * 를 호출합니다 `FormsResult` 개체 `getAttachments` 메서드를 사용합니다. 이 메서드는 `java.util.List` 폼과 함께 전송된 파일을 포함하는 개체입니다.
   * 를 통해 반복 `java.util.List` 객체를 사용하여 첨부 파일이 있는지 확인합니다. 파일 첨부 파일이 있는 경우 각 요소는 `com.adobe.idp.Document` 인스턴스. 를 호출하여 첨부 파일을 저장할 수 있습니다 `com.adobe.idp.Document` 개체 `copyToFile` 메서드 및 전달 `java.io.File` 개체.

   >[!NOTE]
   >
   >이 단계는 양식이 PDF으로 제출된 경우에만 적용됩니다.

1. 제출된 데이터 처리

   * 데이터 컨텐츠 유형이 `application/vnd.adobe.xdp+xml` 또는 `text/xml`에서는 응용 프로그램 논리를 만들어 XML 데이터 값을 검색합니다.

      * 만들기 `com.adobe.idp.Document` 객체를 호출하여 `FormsResult` 개체 `getOutputContent` 메서드를 사용합니다.
      * 만들기 `java.io.InputStream` 객체를 호출하여 `java.io.DataInputStream` 생성자 및 전달 `com.adobe.idp.Document` 개체.
      * 만들기 `org.w3c.dom.DocumentBuilderFactory` 정적 `org.w3c.dom.DocumentBuilderFactory` 개체 `newInstance` 메서드를 사용합니다.
      * 만들기 `org.w3c.dom.DocumentBuilder` 객체를 호출하여 `org.w3c.dom.DocumentBuilderFactory` 개체 `newDocumentBuilder` 메서드를 사용합니다.
      * 만들기 `org.w3c.dom.Document` 객체를 호출하여 `org.w3c.dom.DocumentBuilder` 개체 `parse` 메서드 및 전달 `java.io.InputStream` 개체.
      * XML 문서 내에서 각 노드의 값을 검색합니다. 이 작업을 수행하는 한 가지 방법은 두 개의 매개 변수를 허용하는 사용자 지정 메서드를 만드는 것입니다. a `org.w3c.dom.Document` 객체 및 검색할 값이 있는 노드의 이름입니다. 이 메서드는 노드의 값을 나타내는 문자열 값을 반환합니다. 이 프로세스를 따르는 코드 예제에서 이 사용자 지정 메서드는 라고 합니다 `getNodeText`. 이 메서드의 본문이 표시됩니다.
   * 데이터 컨텐츠 유형이 `application/pdf`, 애플리케이션 논리를 만들어 제출된 PDF 데이터를 PDF 파일로 저장합니다.

      * 만들기 `com.adobe.idp.Document` 객체를 호출하여 `FormsResult` 개체 `getOutputContent` 메서드를 사용합니다.
      * 만들기 `java.io.File` public 생성자를 사용하여 개체를 만듭니다. PDF을 파일 이름 확장자로 지정해야 합니다.
      * 를 호출하여 PDF 파일을 채웁니다 `com.adobe.idp.Document` 개체 `copyToFile` 메서드 및 전달 `java.io.File` 개체.


**추가 참조**

[빠른 시작(SOAP 모드): Java API를 사용하여 XML로 제출된 PDF forms 처리](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-xml-using-the-java-api)

[빠른 시작(SOAP 모드): Java API를 사용하여 XML로 제출된 HTML 양식 처리](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-html-forms-submitted-as-xml-using-the-java-api)

[빠른 시작(SOAP 모드): Java API를 사용하여 PDF으로 제출된 PDF forms 처리](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-pdf-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API를 사용하여 제출된 PDF 데이터를 처리합니다 {#handle-submitted-pdf-data-using-the-web-service-api}

Forms API(웹 서비스)를 사용하여 제출된 양식을 처리합니다.

1. 프로젝트 파일 포함

   * Forms 서비스 WSDL을 사용하는 Java 프록시 클래스를 만듭니다.
   * Java 프록시 클래스를 클래스 경로에 포함합니다.

1. Forms 클라이언트 API 개체 만들기

   만들기 `FormsService` 개체 및 인증 값을 설정합니다.

1. 양식 데이터 검색

   * Java 서블릿에 게시된 양식 데이터를 검색하려면 `BLOB` 생성자를 사용하여 개체를 작성합니다.
   * 만들기 `java.io.InputStream` 객체를 호출하여 `javax.servlet.http.HttpServletResponse` 개체 `getInputStream` 메서드를 사용합니다.
   * 만들기 `java.io.ByteArrayOutputStream` 생성자를 사용하여 개체의 길이를 전달하여 `java.io.InputStream` 개체.
   * 의 내용을 복사합니다. `java.io.InputStream` 개체 `java.io.ByteArrayOutputStream` 개체.
   * 를 호출하여 바이트 배열을 만듭니다 `java.io.ByteArrayOutputStream` 개체 `toByteArray` 메서드를 사용합니다.
   * 을(를) 채우기 `BLOB` 객체를 호출하여 `setBinaryData` 메서드에서 바이트 배열을 인수로 전달합니다.
   * 만들기 `RenderOptionsSpec` 생성자를 사용하여 개체를 작성합니다. 로케일 값을 `RenderOptionsSpec` 개체 `setLocale` 메서드를 사용하여 로케일 값을 지정하는 문자열 값을 전달합니다.
   * 를 호출합니다 `FormsService` 개체 `processFormSubmission` 메서드를 사용하여 다음 값을 전달합니다.

      * 다음 `BLOB` 양식 데이터를 포함하는 객체입니다.
      * 모든 관련 HTTP 헤더를 포함하는 환경 변수를 지정하는 문자열 값입니다. 처리할 콘텐츠 유형을 지정합니다. XML 데이터를 처리하려면 이 매개 변수에 다음 문자열 값을 지정합니다. `CONTENT_TYPE=text/xml`. PDF 데이터를 처리하려면 이 매개 변수에 다음 문자열 값을 지정합니다. `CONTENT_TYPE=application/pdf`.
      * 를 지정하는 문자열 값 `HTTP_USER_AGENT` 헤더 값; 예 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * A `RenderOptionsSpec` 런타임 옵션을 저장하는 개체입니다.
      * 비어 있음 `BLOBHolder` 메서드로 채워지는 개체입니다.
      * 비어 있음 `javax.xml.rpc.holders.StringHolder` 메서드로 채워지는 개체입니다.
      * 비어 있음 `BLOBHolder` 메서드로 채워지는 개체입니다.
      * 비어 있음 `BLOBHolder` 메서드로 채워지는 개체입니다.
      * 비어 있음 `javax.xml.rpc.holders.ShortHolder` 메서드로 채워지는 개체입니다.
      * 비어 있음 `MyArrayOf_xsd_anyTypeHolder` 메서드로 채워지는 개체입니다. 이 매개 변수는 양식과 함께 제출된 첨부 파일을 저장하는 데 사용됩니다.
      * 비어 있음 `FormsResultHolder` 제출된 양식으로 메서드로 채워지는 개체입니다.

      다음 `processFormSubmission` 메서드 채우기 `FormsResultHolder` 매개 변수와 함께 사용할 수 있습니다.

   * 를 호출하여 Forms 서비스가 양식 데이터 처리를 완료했는지 여부를 결정합니다 `FormsResult` 개체 `getAction` 메서드를 사용합니다. 이 메서드가 값을 반환하는 경우 `0`: 양식 데이터를 처리할 준비가 되었습니다. 당신은 `FormsResult` 개체의 값을 가져와서 `FormsResultHolder` 개체 `value` 데이터 멤버.


1. 양식 제출 시 첨부 파일이 포함되어 있는지 확인

   의 값 가져오기 `MyArrayOf_xsd_anyTypeHolder` 개체 `value` 데이터 멤버(A) `MyArrayOf_xsd_anyTypeHolder` 개체가 `processFormSubmission` 메서드). 이 데이터 멤버는 `Objects`. 내 각 요소 `Object` 배열은 `Object`이 값은 양식과 함께 제출된 파일에 해당합니다. 배열 내의 각 요소를 가져와서 `BLOB` 개체.

1. 제출된 데이터 처리

   * 데이터 컨텐츠 유형이 `application/vnd.adobe.xdp+xml` 또는 `text/xml`에서는 응용 프로그램 논리를 만들어 XML 데이터 값을 검색합니다.

      * 만들기 `BLOB` 객체를 호출하여 `FormsResult` 개체 `getOutputContent` 메서드를 사용합니다.
      * 를 호출하여 바이트 배열을 만듭니다 `BLOB` 개체 `getBinaryData` 메서드를 사용합니다.
      * 만들기 `java.io.InputStream` 객체를 호출하여 `java.io.ByteArrayInputStream` 생성자에서 바이트 배열을 전달합니다.
      * 만들기 `org.w3c.dom.DocumentBuilderFactory` 정적 `org.w3c.dom.DocumentBuilderFactory` 개체 `newInstance` 메서드를 사용합니다.
      * 만들기 `org.w3c.dom.DocumentBuilder` 객체를 호출하여 `org.w3c.dom.DocumentBuilderFactory` 개체 `newDocumentBuilder` 메서드를 사용합니다.
      * 만들기 `org.w3c.dom.Document` 객체를 호출하여 `org.w3c.dom.DocumentBuilder` 개체 `parse` 메서드 및 전달 `java.io.InputStream` 개체.
      * XML 문서 내에서 각 노드의 값을 검색합니다. 이 작업을 수행하는 한 가지 방법은 두 개의 매개 변수를 허용하는 사용자 지정 메서드를 만드는 것입니다. a `org.w3c.dom.Document` 객체 및 검색할 값이 있는 노드의 이름입니다. 이 메서드는 노드의 값을 나타내는 문자열 값을 반환합니다. 이 프로세스를 따르는 코드 예제에서 이 사용자 지정 메서드는 라고 합니다 `getNodeText`. 이 메서드의 본문이 표시됩니다.
   * 데이터 컨텐츠 유형이 `application/pdf`, 애플리케이션 논리를 만들어 제출된 PDF 데이터를 PDF 파일로 저장합니다.

      * 만들기 `BLOB` 객체를 호출하여 `FormsResult` 개체 `getOutputContent` 메서드를 사용합니다.
      * 를 호출하여 바이트 배열을 만듭니다 `BLOB` 개체 `getBinaryData` 메서드를 사용합니다.
      * 만들기 `java.io.File` public 생성자를 사용하여 개체를 만듭니다. PDF을 파일 이름 확장자로 지정해야 합니다.
      * 만들기 `java.io.FileOutputStream` 생성자를 사용하여 객체를 전달하고 `java.io.File` 개체.
      * 를 호출하여 PDF 파일을 채웁니다 `java.io.FileOutputStream` 개체 `write` 메서드를 사용하여 바이트 배열을 전달합니다.


**추가 참조**

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
