---
title: 제출된 Forms 처리
seo-title: 제출된 Forms 처리
description: Forms 서비스를 사용하여 제출된 데이터를 대화형 형식으로 검색합니다. 사용자는 양식 데이터를 XML, PDF 및 URL UTF-16 형식으로 제출할 수 있습니다.
seo-description: Forms 서비스를 사용하여 제출된 데이터를 대화형 형식으로 검색합니다. 사용자는 양식 데이터를 XML, PDF 및 URL UTF-16 형식으로 제출할 수 있습니다.
uuid: 673b28f1-f023-4da8-a6a0-c5ff921c5f5d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 3d838027-6bde-4a71-a428-4d5102f7d799
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2936'
ht-degree: 0%

---


# 제출된 Forms 처리 {#handling-submitted-forms}

**이 문서의 샘플과 예는 JEE 환경의 AEM Forms에만 해당됩니다.**

사용자가 대화형 양식을 채울 수 있는 웹 기반 응용 프로그램은 데이터를 서버에 다시 제출해야 합니다. Forms 서비스를 사용하여 사용자가 대화형 양식에 입력한 데이터를 검색할 수 있습니다. 데이터를 검색한 후 데이터를 처리하여 비즈니스 요구 사항을 충족할 수 있습니다. 예를 들어 데이터를 데이터베이스에 저장하고, 데이터를 다른 응용 프로그램으로 보내고, 데이터를 다른 서비스로 보내고, 데이터를 양식 디자인으로 병합하고, 웹 브라우저에 데이터를 표시하는 등의 작업을 수행할 수 있습니다.

양식 데이터는 Designer에서 설정하는 옵션인 XML 또는 PDF 데이터로 Forms 서비스에 제출됩니다. XML로 제출된 양식을 사용하여 개별 필드 데이터 값을 추출할 수 있습니다. 즉, 사용자가 양식에 입력한 각 양식 필드의 값을 추출할 수 있습니다. PDF 데이터로 제출된 양식은 XML 데이터가 아니라 이진 데이터입니다. 양식을 PDF 파일로 저장하거나 다른 서비스로 보낼 수 있습니다. XML로 제출한 양식에서 데이터를 추출하고 양식 데이터를 사용하여 PDF 문서를 만들려면 다른 AEM Forms 작업을 호출합니다. ([제출된 XML 데이터가 있는 PDF 문서 만들기](/help/forms/developing/creating-pdf-documents-submitted-xml.md) 참조)

다음 다이어그램은 웹 브라우저에 표시된 대화형 양식에서 `HandleData`이라는 Java 서블릿에 제출하는 데이터를 보여줍니다.

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
   <td><p>사용자가 대화형 양식을 채우고 양식의 제출 단추를 클릭합니다.</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>데이터는 <code>HandleData</code> Java 서블릿에 XML 데이터로 제출됩니다.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p><code>HandleData</code> Java 서블릿에는 데이터를 검색할 응용 프로그램 논리가 포함되어 있습니다.</p></td>
  </tr>
 </tbody>
</table>

## 제출된 XML 데이터 {#handling-submitted-xml-data} 처리

양식 데이터가 XML로 제출되면 제출된 데이터를 나타내는 XML 데이터를 검색할 수 있습니다. 모든 양식 필드는 XML 스키마에 노드로 표시됩니다. 노드 값은 사용자가 입력한 값에 해당합니다. 양식의 각 필드가 XML 데이터 내의 노드로 표시되는 대출 양식을 고려하십시오. 각 노드의 값은 사용자가 채우는 값에 해당합니다. 사용자가 다음 양식에 표시된 데이터로 대출 양식을 채우라고 가정합니다.

![hs_loanformdata](assets/hs_hs_loanformdata.png)

다음 그림은 Forms 서비스 클라이언트 API를 사용하여 검색한 해당 XML 데이터를 보여줍니다.

![hs_hs_loandata](assets/hs_hs_loandata.png)

대출 양식의 들판. 이러한 값은 검색할 수 있습니다.
Java XML 클래스 사용.

>[!NOTE]
>
>데이터를 XML 데이터로 전송하려면 양식 디자인을 Designer에서 올바르게 구성해야 합니다. 양식 디자인이 XML 데이터를 전송하도록 제대로 구성하려면 양식 디자인에 있는 [제출] 단추가 XML 데이터를 전송하도록 설정되어 있는지 확인하십시오. 제출 단추를 설정하여 XML 데이터를 제출하는 방법에 대한 자세한 내용은 [AEM Forms 디자이너](https://www.adobe.com/go/learn_aemforms_designer_63)를 참조하십시오.

## 제출된 PDF 데이터 처리 {#handling-submitted-pdf-data}

Forms 서비스를 호출하는 웹 애플리케이션을 고려합니다. Forms 서비스가 대화형 PDF 양식을 클라이언트 웹 브라우저에 렌더링하면 사용자는 양식을 채우고 PDF 데이터로 다시 제출합니다. Forms 서비스는 PDF 데이터를 받으면 PDF 데이터를 다른 서비스로 보내거나 PDF 파일로 저장할 수 있습니다. 다음 다이어그램은 응용 프로그램의 논리 흐름을 보여줍니다.

![hs_hs_saving 양식](assets/hs_hs_savingforms.png)

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
   <td><p>3</p></td>
   <td><p>웹 페이지에는 Forms 서비스를 호출하는 Java 서블릿에 액세스하는 링크가 포함되어 있습니다.</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Forms 서비스는 대화형 PDF 양식을 클라이언트 웹 브라우저에 렌더링합니다.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>사용자가 대화형 양식을 채우고 제출 단추를 클릭합니다. 양식은 PDF 데이터로 Forms 서비스에 다시 제출됩니다. 이 옵션은 Designer에서 설정합니다.</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Forms 서비스는 PDF 데이터를 PDF 파일로 저장합니다. </p></td>
  </tr>
 </tbody>
</table>

## 제출된 URL UTF-16 데이터 처리 {#handling-submitted-url-utf-16-data}

양식 데이터가 URL UTF-16 데이터로 제출되면 클라이언트 컴퓨터에 Adobe Reader 또는 Acrobat 8.1 이상이 필요합니다. 또한 양식 디자인에 URL 인코딩된 데이터(HTTP 게시물)가 있는 전송 단추가 있고 데이터 인코딩 옵션이 UTF-16인 경우 메모장과 같은 텍스트 편집기에서 양식 디자인을 수정해야 합니다. 전송 단추에 대해 인코딩 옵션을 `UTF-16LE` 또는 `UTF-16BE`으로 설정할 수 있습니다. 디자이너는 이 기능을 제공하지 않습니다.

>[!NOTE]
>
>Forms 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

## {#summary-of-steps} 단계 요약

제출된 양식을 처리하려면 다음 작업을 수행합니다.

1. 프로젝트 파일 포함
1. Forms Client API 객체를 만듭니다.
1. 양식 데이터를 검색합니다.
1. 양식 제출 시 첨부 파일이 포함되어 있는지 확인합니다.
1. 제출된 데이터를 처리합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Forms 클라이언트 API 개체 만들기**

Forms 서비스 클라이언트 API 작업을 프로그래밍 방식으로 수행하려면 먼저 Forms 서비스 클라이언트를 만들어야 합니다. Java API를 사용하는 경우 `FormsServiceClient` 개체를 만듭니다. Forms 웹 서비스 API를 사용하는 경우 `FormsService` 개체를 만듭니다.

**양식 데이터 검색**

제출된 양식 데이터를 검색하려면 `FormsServiceClient` 객체의 `processFormSubmission` 메서드를 호출합니다. 이 메서드를 호출할 때 제출된 양식의 내용 유형을 지정해야 합니다. 클라이언트 웹 브라우저에서 Forms 서비스로 데이터를 전송할 때 XML 또는 PDF 데이터로 전송할 수 있습니다. 양식 필드에 입력된 데이터를 검색하려면 데이터를 XML 데이터로 제출할 수 있습니다.

다음 런타임 옵션을 설정하여 PDF 데이터로 제출된 양식에서 양식 필드를 검색할 수도 있습니다.

* 다음 값을 내용 유형 매개 변수로 `processFormSubmission` 메서드에 전달합니다.`CONTENT_TYPE=application/pdf`.
* `RenderOptionsSpec` 개체의 `PDFToXDP` 값을 `true`로 설정합니다.
* `RenderOptionsSpec` 개체의 `ExportDataFormat` 값을 `XMLData`로 설정합니다.

`processFormSubmission` 메서드를 호출할 때 제출된 양식의 내용 유형을 지정합니다. 다음 목록은 적용 가능한 컨텐츠 유형 값을 지정합니다.

* **text/xml**:PDF 양식이 양식 데이터를 XML로 제출할 때 사용할 내용 유형을 나타냅니다.
* **application/x-www-form-urlencoded**:HTML 양식이 데이터를 XML로 제출할 때 사용할 내용 유형을 나타냅니다.
* **application/pdf**:PDF 양식이 데이터를 PDF로 제출할 때 사용할 내용 유형을 나타냅니다.

>[!NOTE]
>
>제출된 Forms 처리 섹션에 해당하는 빠른 시작 3개가 있음을 알 수 있습니다. Java API 빠른 시작을 사용하여 PDF로 제출된 처리 PDF forms은 제출된 PDF 데이터를 처리하는 방법을 보여 줍니다. 이 빠른 시작 부분에 지정된 콘텐츠 유형은 `application/pdf`입니다. Java API 빠른 시작을 사용하여 XML로 제출된 처리 PDF forms은 PDF 양식에서 제출한 제출된 XML 데이터를 처리하는 방법을 보여 줍니다. 이 빠른 시작 부분에 지정된 콘텐츠 유형은 `text/xml`입니다. 마찬가지로 Java API 빠른 시작을 사용하여 XML로 제출된 HTML 양식 처리는 HTML 양식에서 제출한 제출된 XML 데이터를 처리하는 방법을 보여 줍니다. 이 빠른 시작 부분에 지정된 컨텐츠 유형은 application/x-www-form-urlencoded입니다.

Forms 서비스에 게시된 양식 데이터를 검색하고 처리 상태를 결정합니다. 즉, 데이터가 Forms 서비스에 전송될 때 Forms 서비스가 데이터 처리를 완료하고 데이터를 처리할 준비가 되었다는 의미가 아닙니다. 예를 들어 계산을 수행할 수 있도록 데이터를 Forms 서비스에 제출할 수 있습니다. 계산이 완료되면 양식이 다시 사용자에게 렌더링되고 계산 결과가 표시됩니다. 제출된 데이터를 처리하기 전에 Forms 서비스가 데이터 처리를 완료했는지 여부를 확인하는 것이 좋습니다.

Forms 서비스는 데이터 처리를 완료했는지 여부를 나타내기 위해 다음 값을 반환합니다.

* **0(제출):** 제출된 데이터를 처리할 준비가 되었습니다.
* **1(계산):** Forms 서비스가 데이터에 대해 계산 작업을 수행했으며 결과를 사용자에게 다시 렌더링해야 합니다.
* **2(유효성):** Forms 서비스는 양식 데이터의 유효성을 검사하여 결과를 사용자에게 다시 렌더링해야 합니다.
* **3(다음):** 현재 페이지가 클라이언트 응용 프로그램에 작성해야 하는 결과로 변경되었습니다.
* **4(이전**):현재 페이지가 클라이언트 응용 프로그램에 작성해야 하는 결과로 변경되었습니다.

>[!NOTE]
>
>계산 및 유효성 검사를 다시 사용자에게 렌더링해야 합니다. ([양식 데이터 계산](/help/forms/developing/calculating-form-data.md#calculating-form-data)을 참조하십시오.)

**양식 제출 시 첨부 파일이 포함되어 있는지 확인**

Forms 서비스에 제출된 Forms에는 첨부 파일이 포함될 수 있습니다. 예를 들어 Acrobat의 내장된 첨부 창을 사용하면 양식과 함께 제출할 첨부 파일을 선택할 수 있습니다. 또한 사용자는 HTML 파일로 렌더링되는 HTML 도구 모음을 사용하여 첨부 파일을 선택할 수도 있습니다.

양식에 첨부 파일이 포함되어 있는지 확인한 후 데이터를 처리할 수 있습니다. 예를 들어 로컬 파일 시스템에 첨부 파일을 저장할 수 있습니다.

>[!NOTE]
>
>첨부 파일을 검색하려면 양식을 PDF 데이터로 제출해야 합니다. 양식이 XML 데이터로 제출되면 첨부 파일이 전송되지 않습니다.

**제출된 데이터 처리**

제출된 데이터의 컨텐츠 유형에 따라 제출된 XML 데이터에서 개별 양식 필드 값을 추출하거나 제출된 PDF 데이터를 PDF 파일로 저장(또는 다른 서비스로 보내기)할 수 있습니다. 개별 양식 필드를 추출하려면 제출된 XML 데이터를 XML 데이터 소스로 변환한 다음 `org.w3c.dom` 클래스를 사용하여 XML 데이터 소스 값을 검색합니다.

**참고 항목**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms 서비스 API 빠른 시작](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Forms 서비스에 문서 전달](/help/forms/developing/passing-documents-forms-service.md)

[Forms을 렌더링하는 웹 애플리케이션 만들기](/help/forms/developing/creating-web-applications-renders-forms.md)

## Java API {#handle-submitted-forms-using-the-java-api}를 사용하여 제출된 양식을 처리합니다.

Forms API(Java)를 사용하여 제출된 양식을 처리합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-forms-client.jar 등의 클라이언트 JAR 파일을 포함합니다.

1. Forms 클라이언트 API 개체 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 `FormsServiceClient` 개체를 만들고 `ServiceClientFactory` 개체를 전달합니다.

1. 양식 데이터 검색

   * Java 서블릿에 게시된 양식 데이터를 검색하려면 생성자를 사용하고 생성자 내에서 `javax.servlet.http.HttpServletResponse` 객체의 `getInputStream` 메서드를 호출하여 `com.adobe.idp.Document` 객체를 만듭니다.
   * 생성자를 사용하여 `RenderOptionsSpec` 객체를 만듭니다. `RenderOptionsSpec` 객체의 `setLocale` 메서드를 호출하고 로케일 값을 지정하는 문자열 값을 전달하여 로케일 값을 설정합니다.

   >[!NOTE]
   >
   >`RenderOptionsSpec` 개체의 `setPDF2XDP` 메서드를 호출하고 `true`를 호출하고 `setXMLData`을(를) 호출하고 `true`를 전달하여 제출된 PDF 내용에서 XDP 또는 XML 데이터를 만들도록 Forms 서비스에 지시할 수 있습니다. 그런 다음 `FormsResult` 객체의 `getOutputXML` 메서드를 호출하여 XDP/XML 데이터에 해당하는 XML 데이터를 검색할 수 있습니다. `FormsResult` 개체는 다음 하위 단계에서 설명하는 `processFormSubmission` 메서드에서 반환됩니다.

   * `FormsServiceClient` 객체의 `processFormSubmission` 메서드를 호출하고 다음 값을 전달합니다.

      * 양식 데이터를 포함하는 `com.adobe.idp.Document` 객체입니다.
      * 모든 관련 HTTP 헤더를 포함하는 환경 변수를 지정하는 문자열 값입니다. 처리할 콘텐츠 유형을 지정합니다. XML 데이터를 처리하려면 이 매개 변수에 대해 다음 문자열 값을 지정합니다.`CONTENT_TYPE=text/xml`. PDF 데이터를 처리하려면 이 매개 변수에 대해 다음 문자열 값을 지정합니다.`CONTENT_TYPE=application/pdf`.
      * `HTTP_USER_AGENT` 헤더 값을 지정하는 문자열 값(예: .) `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. 이 매개 변수 값은 선택 사항입니다.
      * 런타임 옵션을 저장하는 `RenderOptionsSpec` 객체입니다.

      `processFormSubmission` 메서드는 양식 제출 결과를 포함하는 `FormsResult` 객체를 반환합니다.

   * Forms 서비스가 `FormsResult` 개체의 `getAction` 메서드를 호출하여 양식 데이터 처리를 완료했는지 여부를 확인합니다. 이 메서드가 `0` 값을 반환하면 데이터를 처리할 수 있습니다.



1. 양식 제출 시 첨부 파일이 포함되어 있는지 확인

   * `FormsResult` 객체의 `getAttachments` 메서드를 호출합니다. 이 메서드는 폼과 함께 전송된 파일을 포함하는 `java.util.List` 객체를 반환합니다.
   * `java.util.List` 개체를 반복하여 첨부 파일이 있는지 확인합니다. 첨부 파일이 있는 경우 각 요소는 `com.adobe.idp.Document` 인스턴스입니다. `com.adobe.idp.Document` 개체의 `copyToFile` 메서드를 호출하고 `java.io.File` 개체를 전달하여 첨부 파일을 저장할 수 있습니다.

   >[!NOTE]
   >
   >이 단계는 양식이 PDF로 제출된 경우에만 적용됩니다.

1. 제출된 데이터 처리

   * 데이터 내용 유형이 `application/vnd.adobe.xdp+xml` 또는 `text/xml`이면 응용 프로그램 논리를 만들어 XML 데이터 값을 검색합니다.

      * `FormsResult` 객체의 `getOutputContent` 메서드를 호출하여 `com.adobe.idp.Document` 객체를 만듭니다.
      * `java.io.DataInputStream` 생성자를 호출하고 `com.adobe.idp.Document` 객체를 전달하여 `java.io.InputStream` 객체를 만듭니다.
      * 정적 `org.w3c.dom.DocumentBuilderFactory` 객체의 `newInstance` 메서드를 호출하여 `org.w3c.dom.DocumentBuilderFactory` 객체를 만듭니다.
      * `org.w3c.dom.DocumentBuilderFactory` 객체의 `newDocumentBuilder` 메서드를 호출하여 `org.w3c.dom.DocumentBuilder` 객체를 만듭니다.
      * `org.w3c.dom.DocumentBuilder` 객체의 `parse` 메서드를 호출하고 `java.io.InputStream` 객체를 전달하여 `org.w3c.dom.Document` 객체를 만듭니다.
      * XML 문서 내에서 각 노드의 값을 검색합니다. 이 작업을 수행하는 한 가지 방법은 두 개의 매개 변수를 허용하는 사용자 지정 메서드를 만드는 것입니다.`org.w3c.dom.Document` 개체와 값을 검색할 노드의 이름입니다. 이 메서드는 노드의 값을 나타내는 문자열 값을 반환합니다. 이 프로세스를 따르는 코드 예제에서 이 사용자 지정 메서드를 `getNodeText`이라고 합니다. 이 메서드의 본문이 표시됩니다.
   * 데이터 콘텐트 유형이 `application/pdf`이면 응용 프로그램 논리를 만들어 제출된 PDF 데이터를 PDF 파일로 저장합니다.

      * `FormsResult` 객체의 `getOutputContent` 메서드를 호출하여 `com.adobe.idp.Document` 객체를 만듭니다.
      * 공용 생성자를 사용하여 `java.io.File` 객체를 만듭니다. PDF를 파일 이름 확장자로 지정해야 합니다.
      * `com.adobe.idp.Document` 개체의 `copyToFile` 메서드를 호출하고 `java.io.File` 개체를 전달하여 PDF 파일을 채웁니다.


**참고 항목**

[빠른 시작(SOAP 모드):Java API를 사용하여 XML로 제출된 PDF forms 처리](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-xml-using-the-java-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 XML로 제출된 HTML 양식 처리](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-html-forms-submitted-as-xml-using-the-java-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 PDF로 제출된 PDF forms 처리](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-pdf-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API {#handle-submitted-pdf-data-using-the-web-service-api}를 사용하여 제출된 PDF 데이터를 처리합니다.

Forms API(웹 서비스)를 사용하여 제출된 양식을 처리합니다.

1. 프로젝트 파일 포함

   * Forms 서비스 WSDL을 사용하는 Java 프록시 클래스를 만듭니다.
   * 클래스 경로에 Java 프록시 클래스를 포함합니다.

1. Forms 클라이언트 API 개체 만들기

   `FormsService` 개체를 만들고 인증 값을 설정합니다.

1. 양식 데이터 검색

   * Java 서블릿에 게시된 양식 데이터를 검색하려면 해당 생성자를 사용하여 `BLOB` 객체를 만듭니다.
   * `javax.servlet.http.HttpServletResponse` 객체의 `getInputStream` 메서드를 호출하여 `java.io.InputStream` 객체를 만듭니다.
   * 생성자를 사용하여 `java.io.ByteArrayOutputStream` 개체를 만들고 `java.io.InputStream` 객체의 길이를 전달합니다.
   * `java.io.InputStream` 개체의 내용을 `java.io.ByteArrayOutputStream` 개체에 복사합니다.
   * `java.io.ByteArrayOutputStream` 객체의 `toByteArray` 메서드를 호출하여 바이트 배열을 만듭니다.
   * `setBinaryData` 메서드를 호출하고 바이트 배열을 인수로 전달하여 `BLOB` 객체를 채웁니다.
   * 생성자를 사용하여 `RenderOptionsSpec` 객체를 만듭니다. `RenderOptionsSpec` 객체의 `setLocale` 메서드를 호출하고 로케일 값을 지정하는 문자열 값을 전달하여 로케일 값을 설정합니다.
   * `FormsService` 객체의 `processFormSubmission` 메서드를 호출하고 다음 값을 전달합니다.

      * 양식 데이터를 포함하는 `BLOB` 객체입니다.
      * 모든 관련 HTTP 헤더를 포함하는 환경 변수를 지정하는 문자열 값입니다. 처리할 콘텐츠 유형을 지정합니다. XML 데이터를 처리하려면 이 매개 변수에 대해 다음 문자열 값을 지정합니다.`CONTENT_TYPE=text/xml`. PDF 데이터를 처리하려면 이 매개 변수에 대해 다음 문자열 값을 지정합니다.`CONTENT_TYPE=application/pdf`.
      * `HTTP_USER_AGENT` 헤더 값을 지정하는 문자열 값;예: `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`
      * 런타임 옵션을 저장하는 `RenderOptionsSpec` 객체입니다.
      * 메서드에 의해 채워지는 빈 `BLOBHolder` 객체입니다.
      * 메서드에 의해 채워지는 빈 `javax.xml.rpc.holders.StringHolder` 객체입니다.
      * 메서드에 의해 채워지는 빈 `BLOBHolder` 객체입니다.
      * 메서드에 의해 채워지는 빈 `BLOBHolder` 객체입니다.
      * 메서드에 의해 채워지는 빈 `javax.xml.rpc.holders.ShortHolder` 객체입니다.
      * 메서드에 의해 채워지는 빈 `MyArrayOf_xsd_anyTypeHolder` 객체입니다. 이 매개 변수는 양식과 함께 제출된 첨부 파일을 저장하는 데 사용됩니다.
      * 제출된 폼으로 메서드에 의해 채워진 빈 `FormsResultHolder` 객체입니다.

      `processFormSubmission` 메서드는 `FormsResultHolder` 매개 변수를 양식 제출 결과로 채웁니다.

   * Forms 서비스가 `FormsResult` 개체의 `getAction` 메서드를 호출하여 양식 데이터 처리를 완료했는지 여부를 확인합니다. 이 메서드가 `0` 값을 반환하면 양식 데이터를 처리할 수 있습니다. `FormsResultHolder` 개체의 `value` 데이터 멤버의 값을 가져와 `FormsResult` 개체를 가져올 수 있습니다.


1. 양식 제출 시 첨부 파일이 포함되어 있는지 확인

   `MyArrayOf_xsd_anyTypeHolder` 개체의 `value` 데이터 멤버(`MyArrayOf_xsd_anyTypeHolder` 개체가 `processFormSubmission` 메서드에 전달됨)의 값을 가져옵니다. 이 데이터 멤버는 `Objects` 배열을 반환합니다. `Object` 배열 내의 각 요소는 양식과 함께 제출된 파일에 해당하는 `Object`입니다. 배열 내의 각 요소를 가져와 `BLOB` 객체에 캐스팅할 수 있습니다.

1. 제출된 데이터 처리

   * 데이터 내용 유형이 `application/vnd.adobe.xdp+xml` 또는 `text/xml`이면 응용 프로그램 논리를 만들어 XML 데이터 값을 검색합니다.

      * `FormsResult` 객체의 `getOutputContent` 메서드를 호출하여 `BLOB` 객체를 만듭니다.
      * `BLOB` 객체의 `getBinaryData` 메서드를 호출하여 바이트 배열을 만듭니다.
      * `java.io.ByteArrayInputStream` 생성자를 호출하고 바이트 배열을 전달하여 `java.io.InputStream` 객체를 만듭니다.
      * 정적 `org.w3c.dom.DocumentBuilderFactory` 객체의 `newInstance` 메서드를 호출하여 `org.w3c.dom.DocumentBuilderFactory` 객체를 만듭니다.
      * `org.w3c.dom.DocumentBuilderFactory` 객체의 `newDocumentBuilder` 메서드를 호출하여 `org.w3c.dom.DocumentBuilder` 객체를 만듭니다.
      * `org.w3c.dom.DocumentBuilder` 객체의 `parse` 메서드를 호출하고 `java.io.InputStream` 객체를 전달하여 `org.w3c.dom.Document` 객체를 만듭니다.
      * XML 문서 내에서 각 노드의 값을 검색합니다. 이 작업을 수행하는 한 가지 방법은 두 개의 매개 변수를 허용하는 사용자 지정 메서드를 만드는 것입니다.`org.w3c.dom.Document` 개체와 값을 검색할 노드의 이름입니다. 이 메서드는 노드의 값을 나타내는 문자열 값을 반환합니다. 이 프로세스를 따르는 코드 예제에서 이 사용자 지정 메서드를 `getNodeText`이라고 합니다. 이 메서드의 본문이 표시됩니다.
   * 데이터 콘텐트 유형이 `application/pdf`이면 응용 프로그램 논리를 만들어 제출된 PDF 데이터를 PDF 파일로 저장합니다.

      * `FormsResult` 객체의 `getOutputContent` 메서드를 호출하여 `BLOB` 객체를 만듭니다.
      * `BLOB` 객체의 `getBinaryData` 메서드를 호출하여 바이트 배열을 만듭니다.
      * 공용 생성자를 사용하여 `java.io.File` 객체를 만듭니다. PDF를 파일 이름 확장자로 지정해야 합니다.
      * 생성자를 사용하여 `java.io.FileOutputStream` 개체를 만들고 `java.io.File` 개체를 전달합니다.
      * `java.io.FileOutputStream` 객체의 `write` 메서드를 호출하고 바이트 배열을 전달하여 PDF 파일을 채웁니다.


**참고 항목**

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)