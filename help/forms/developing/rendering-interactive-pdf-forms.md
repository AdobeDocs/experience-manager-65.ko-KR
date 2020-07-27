---
title: 대화형 PDF forms 렌더링
seo-title: 대화형 PDF forms 렌더링
description: 'null'
seo-description: 'null'
uuid: df2a4dc8-f19e-49de-850f-85a204102631
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 3cb307ec-9b7b-4f03-b860-48553ccee746
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2442'
ht-degree: 0%

---


# 대화형 PDF forms 렌더링 {#rendering-interactive-pdf-forms}

Forms 서비스는 대화형 PDF forms을 클라이언트 장치(일반적으로 웹 브라우저)에 렌더링하여 사용자의 정보를 수집합니다. 대화형 양식이 렌더링되면 사용자는 양식 필드에 데이터를 입력하고 양식에 있는 제출 단추를 클릭하여 정보를 양식 서비스로 다시 보낼 수 있습니다. 인터랙티브한 PDF 양식을 표시하려면 클라이언트 웹 브라우저를 호스팅하는 컴퓨터에 Adobe Reader 또는 Acrobat을 설치해야 합니다.

>[!NOTE]
>
>양식 서비스를 사용하여 양식을 렌더링하려면 먼저 양식 디자인을 만듭니다. 일반적으로 양식 디자인은 Designer에서 만들어지고 XDP 파일로 저장됩니다. 양식 디자인 만들기에 대한 자세한 내용은 [양식 디자이너를 참조하십시오](https://www.adobe.com/go/learn_aemforms_designer_63).

**샘플 대출 신청**

양식 서비스가 대화형 양식을 사용하여 사용자로부터 정보를 수집하는 방법을 보여주는 샘플 대출 응용 프로그램이 도입되었습니다. 이 응용 프로그램을 사용하면 사용자가 대출 보안에 필요한 데이터로 양식을 입력한 다음 양식 서비스에 데이터를 제출할 수 있습니다. 다음 다이어그램은 대출 신청 논리 플로우를 보여줍니다.

![ri_ri_finsrv_loanapp_v1](assets/ri_ri_finsrv_loanapp_v1.png)

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
   <td><p>Java <code>GetLoanForm</code> 서블릿은 HTML 페이지에서 호출됩니다. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Java 서블릿은 Forms 서비스 클라이언트 API를 사용하여 대출 양식을 클라이언트 웹 브라우저에 렌더링합니다. <code>GetLoanForm</code> (Java <a href="#render-an-interactive-pdf-form-using-the-java-api">API를 사용하여 대화형 PDF 양식 렌더링을 참조하십시오</a>.)</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>사용자가 대출 양식을 채우고 제출 단추를 클릭하면 데이터가 <code>HandleData</code> Java 서블릿에 제출됩니다. ( <i>"대출 양식"을</i>참조하십시오.)</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Java 서블릿은 Forms 서비스 클라이언트 API를 사용하여 양식 제출 및 양식 데이터를 검색합니다. <code>HandleData</code> 그러면 데이터가 기업 데이터베이스에 저장됩니다. (제출된 <a href="/help/forms/developing/handling-submitted-forms.md#handling-submitted-forms">양식 처리를 참조하십시오</a>.)</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>확인 양식이 다시 웹 브라우저로 렌더링됩니다. 사용자의 이름과 성과 같은 데이터는 렌더링되기 전에 폼과 병합됩니다. ( <a href="/help/forms/developing/prepopulating-forms-flowable-layouts.md">순서별 레이아웃으로 양식 미리 채우기</a>참조)</p></td>
  </tr>
 </tbody>
</table>

**대출 양식**

이 대화형 대출 양식은 샘플 대출 애플리케이션의 Java 서블릿에 의해 `GetLoanForm` 렌더링됩니다.

![ri_ri_loanform](assets/ri_ri_loanform.png)

**확인 양식**

이 양식은 샘플 대출 애플리케이션의 Java 서블릿에 의해 `HandleData` 렌더링됩니다.

![ri_ri_confirm](assets/ri_ri_confirm.png)

Java 서블릿은 금액뿐만 아니라 사용자의 이름과 성으로 이 양식을 미리 채웁니다. `HandleData` 양식이 미리 채워지면 클라이언트 웹 브라우저로 전송됩니다. ( [순서별 레이아웃으로 양식 미리 채우기 참조](/help/forms/developing/prepopulating-forms-flowable-layouts.md))

**Java 서블릿**

샘플 대출 애플리케이션은 Java 서블릿으로 존재하는 Forms 서비스 애플리케이션의 예입니다. Java 서블릿은 WebSphere와 같은 J2EE 응용 프로그램 서버에서 실행되는 Java 프로그램이며 Forms 서비스 클라이언트 API 코드를 포함합니다.

다음 코드는 GetLoanForm이라는 Java 서블릿의 구문을 보여 줍니다.

```java
     public class GetLoanForm extends HttpServlet implements Servlet {
         public void doGet(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

         }
         public void doPost(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

             }
```

일반적으로 Forms 서비스 클라이언트 API 코드를 Java 서블릿 `doGet` 또는 `doPost` 메서드 내에 배치하지 않습니다. 이 코드를 별도의 클래스 내에 배치하고, 메서드(또는 메서드) 내에서 클래스를 인스턴스화하고, 적절한 메서드를 호출하는 `doPost` 것 `doGet` 을 프로그래밍하는 것이 좋습니다. 그러나 코드 간결성의 경우 이 섹션의 코드 예제는 최소로 유지되며 코드 예제는 `doPost` 메서드에 배치됩니다.

>[!NOTE]
>
>양식 서비스에 대한 자세한 내용은 AEM Forms에 대한 [서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

**단계 요약**

대화형 PDF 양식을 렌더링하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일 포함
1. Forms 클라이언트 API 개체를 만듭니다.
1. URI 값을 지정합니다.
1. 양식에 파일 첨부(선택 사항)
1. 인터랙티브한 PDF 양식 렌더링
1. 양식 데이터 스트림을 클라이언트 웹 브라우저에 씁니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Forms 클라이언트 API 개체 만들기**

Forms 서비스 클라이언트 API 작업을 프로그래밍 방식으로 수행하려면 먼저 Forms 클라이언트 API 개체를 만들어야 합니다. Java API를 사용하는 경우 `FormsServiceClient` 개체를 만듭니다. Forms 웹 서비스 API를 사용하는 경우 `FormsService` 개체를 만듭니다.

**URI 값 지정**

양식을 렌더링하는 데 필요한 URI 값을 지정할 수 있습니다. 양식 응용 프로그램의 일부로 저장된 양식 디자인은 컨텐츠 루트 URI 값을 사용하여 참조할 수 있습니다 `repository:///`. 예를 들어 FormsApplication이라는 Forms 응용 프로그램 내에 *있는 Loan.xdp* 라는 이름의 다음 양식 디자인을 *생각해 보십시오*.

![ri_ri_formrepository](assets/ri_ri_formrepository.png)

이 양식 디자인에 액세스하려면 양식 이름 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp` (메서드에 전달된 첫 번째 매개 변수)과 컨텐츠 루트 URI 값 `renderPDFForm` `repository:///` 으로 지정합니다.

>[!NOTE]
>
>워크벤치를 사용하여 Forms 응용 프로그램을 만드는 방법에 대한 자세한 내용은 [워크벤치 도움말을 참조하십시오](https://www.adobe.com/go/learn_aemforms_workbench_63).

양식 응용 프로그램에 있는 리소스의 경로는 다음과 같습니다.

`Applications/Application-name/Application-version/Folder.../Filename`

다음 값은 URI 값의 몇 가지 예를 보여 줍니다.

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

대화형 양식을 렌더링할 때 양식 데이터가 게시되는 대상 URL과 같은 URI 값을 정의할 수 있습니다. 대상 URL은 다음 방법 중 하나로 정의할 수 있습니다.

* Designer에서 양식 디자인을 디자인하는 동안 전송 단추
* Forms 서비스 클라이언트 API 사용

대상 URL이 양식 디자인 내에 정의된 경우 Forms 서비스 클라이언트 API로 덮어쓰지 마십시오. 즉, 양식 API를 사용하여 대상 URL을 설정하면 양식 디자인에서 지정된 URL이 API를 사용하여 지정된 URL로 재설정됩니다. 양식 디자인에 지정된 대상 URL에 PDF 양식을 제출하려는 경우 프로그래밍 방식으로 대상 URL을 빈 문자열로 설정합니다.

전송 단추와 계산 단추(서버에서 실행되는 해당 스크립트 포함)가 들어 있는 양식이 있는 경우 양식을 전송하여 스크립트를 실행할 수 있는 URL을 프로그래밍 방식으로 정의할 수 있습니다. 양식 디자인의 제출 단추를 사용하여 양식 데이터가 게시되는 URL을 지정합니다. 양식 데이터 [계산을 참조하십시오](/help/forms/developing/calculating-form-data.md).

>[!NOTE]
>
>XDP 파일을 참조하는 URL 값을 지정하는 대신 Forms 서비스에 인스턴스를 전달할 수도 `com.adobe.idp.Document` 있습니다. 인스턴스에는 양식 디자인이 `com.adobe.idp.Document` 포함되어 있습니다. (Forms [Service에 문서 전달을 참조하십시오](/help/forms/developing/passing-documents-forms-service.md).)

**양식에 파일 첨부**

양식에 파일을 첨부할 수 있습니다. 첨부 파일이 있는 PDF 양식을 렌더링할 때 사용자는 첨부 파일 창을 사용하여 Acrobat에서 첨부 파일을 검색할 수 있습니다. 텍스트 파일과 같은 양식이나 JPG 파일과 같은 바이너리 파일에 다양한 파일 유형을 첨부할 수 있습니다.

>[!NOTE]
>
>양식에 첨부 파일을 첨부하는 것은 선택 사항입니다.

**인터랙티브한 PDF 양식 렌더링**

양식을 렌더링하려면 Designer에서 만들고 XDP 또는 PDF 파일로 저장한 양식 디자인을 사용합니다. 또한 Acrobat을 사용하여 만들고 PDF 파일로 저장한 양식을 렌더링할 수 있습니다. 인터랙티브한 PDF 양식을 렌더링하려면 `FormsServiceClient` 개체의 `renderPDFForm` 방식이나 방법을 `renderPDFForm2` 불러옵니다.

이 `renderPDFForm` 는 `URLSpec` 개체를 사용합니다. XDP 파일의 컨텐츠 루트는 `URLSpec` 개체의 방법을 사용하여 양식 서비스로 `setContentRootURI` 전달됩니다. 양식 디자인 이름( `formQuery`)은 별도의 매개 변수 값으로 전달됩니다. 양식 디자인에 대한 절대 참조를 가져오기 위해 두 값이 연결됩니다.

이 `renderPDFForm2` `com.adobe.idp.Document` 메서드는 렌더링할 XDP 또는 PDF 문서가 들어 있는 인스턴스를 수락합니다.

>[!NOTE]
>
>입력 문서가 PDF 문서인 경우 태그 지정된 PDF 런타임 옵션을 설정할 수 없습니다. 입력 파일이 XDP 파일인 경우 태그 있는 PDF 옵션을 설정할 수 있습니다.

## Java API를 사용하여 인터랙티브한 PDF 양식 렌더링 {#render-an-interactive-pdf-form-using-the-java-api}

양식 API(Java)를 사용하여 인터랙티브한 PDF 양식을 렌더링합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-forms-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. Forms 클라이언트 API 개체 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 개체를 `FormsServiceClient` 만들고 개체를 `ServiceClientFactory` 전달합니다.

1. URI 값 지정

   * 생성자를 사용하여 URI 값을 저장하는 `URLSpec` 객체를 만듭니다.
   * 객체의 `URLSpec` `setApplicationWebRoot` 메서드를 호출하고 응용 프로그램의 웹 루트를 나타내는 문자열 값을 전달합니다.
   * 개체의 `URLSpec` `setContentRootURI` 메서드를 호출하고 콘텐츠 루트 URI 값을 지정하는 문자열 값을 전달합니다. 양식 디자인이 컨텐츠 루트 URI에 있는지 확인합니다. 그렇지 않으면 Forms 서비스에서 예외가 발생합니다. 저장소를 참조하려면 을 지정합니다 `repository:///`.
   * 개체의 `URLSpec` 메서드를 `setTargetURL` 호출하고 양식 데이터가 게시된 위치에 대상 URL 값을 지정하는 문자열 값을 전달합니다. 양식 디자인에서 대상 URL을 정의하는 경우 빈 문자열을 전달할 수 있습니다. 계산을 수행하기 위해 양식이 전송되는 URL을 지정할 수도 있습니다.

1. 양식에 파일 첨부

   * 생성자를 사용하여 첨부 파일을 저장할 `java.util.HashMap` 객체를 만듭니다.
   * 각 파일에 대해 `java.util.HashMap` 개체의 `put` 메서드를 호출하여 렌더링된 양식에 연결합니다. 다음 값을 이 메서드에 전달합니다.

      * 파일 이름 확장자를 포함하여 파일 첨부 파일의 이름을 지정하는 문자열 값입니다.
   * 첨부 파일이 포함된 `com.adobe.idp.Document` 개체입니다.

   >[!NOTE]
   >
   >양식에 첨부할 각 파일에 대해 이 단계를 반복합니다. 이 단계는 선택 사항이며 첨부 파일을 보내지 않으려는 `null` 경우 전달할 수 있습니다.

1. 인터랙티브한 PDF 양식 렌더링

   개체의 `FormsServiceClient` 메서드를 `renderPDFForm` 호출하고 다음 값을 전달합니다.

   * 파일 이름 확장자를 포함하여 양식 디자인 이름을 지정하는 문자열 값. Forms 응용 프로그램의 일부인 양식 디자인을 참조하는 경우 전체 경로를 지정해야 합니다(예: `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`).
   * 양식과 병합할 데이터가 포함된 `com.adobe.idp.Document` 개체 데이터를 병합하지 않으려면 빈 `com.adobe.idp.Document` 개체를 전달합니다.
   * 런타임 옵션을 저장하는 `PDFFormRenderSpec` 개체입니다. 이 매개 변수는 선택 사항이며 런타임 옵션을 지정하지 않으려는 `null` 경우 지정할 수 있습니다.
   * Forms 서비스에 필요한 URI 값이 포함된 `URLSpec` 개체입니다.
   * 첨부 파일을 저장하는 `java.util.HashMap` 개체입니다. 선택 매개 변수이며 양식에 파일을 첨부하지 않으려는 `null` 경우 지정할 수 있습니다.

   이 `renderPDFForm` 메서드는 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림을 포함하는 `FormsResult` 개체를 반환합니다.

1. 양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰기

   * 개체 &#39;s 메서드 `com.adobe.idp.Document` 를 호출하여 개체를 `FormsResult` 만듭니다 `getOutputContent` .
   * 해당 메서드를 호출하여 개체의 `com.adobe.idp.Document` 콘텐츠 유형을 `getContentType` 가져옵니다.
   * 해당 메서드를 호출하고 개체의 컨텐트 유형을 전달하여 `javax.servlet.http.HttpServletResponse` 개체의 컨텐트 유형을 `setContentType` `com.adobe.idp.Document` 설정합니다.
   * 개체의 메서드를 호출하여 양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰는 데 사용되는 `javax.servlet.ServletOutputStream` 개체를 `javax.servlet.http.HttpServletResponse` `getOutputStream` 만듭니다.
   * 개체 `java.io.InputStream` 의 메서드를 호출하여 `com.adobe.idp.Document` 개체를 `getInputStream` 만듭니다.
   * 바이트 배열을 만들고 `InputStream` `read` 개체의 메서드를 호출하고 바이트 배열을 인수로 전달하여 양식 데이터 스트림으로 채웁니다.
   * 개체의 `javax.servlet.ServletOutputStream` 메서드를 `write` 호출하여 양식 데이터 스트림을 클라이언트 웹 브라우저에 보냅니다. 바이트 배열을 `write` 메서드로 전달합니다.

## 웹 서비스 API를 사용하여 인터랙티브한 PDF 양식 렌더링 {#render-an-interactive-pdf-form-using-the-web-service-api}

Forms API(웹 서비스)를 사용하여 대화형 PDF 양식을 렌더링합니다.

1. 프로젝트 파일 포함

   * Forms 서비스 WSDL을 사용하는 Java 프록시 클래스를 만듭니다.
   * 클래스 경로에 Java 프록시 클래스를 포함합니다.

1. Forms 클라이언트 API 개체 만들기

   객체를 만들고 인증 값을 `FormsService` 설정합니다.

1. URI 값 지정

   * 생성자를 사용하여 URI 값을 저장하는 `URLSpec` 객체를 만듭니다.
   * 객체의 `URLSpec` `setApplicationWebRoot` 메서드를 호출하고 응용 프로그램의 웹 루트를 나타내는 문자열 값을 전달합니다.
   * 개체의 `URLSpec` `setContentRootURI` 메서드를 호출하고 콘텐츠 루트 URI 값을 지정하는 문자열 값을 전달합니다. 양식 디자인이 컨텐츠 루트 URI에 있는지 확인합니다. 그렇지 않으면 Forms 서비스에서 예외가 발생합니다. 저장소를 참조하려면 을 지정합니다 `repository:///`.
   * 개체의 `URLSpec` 메서드를 `setTargetURL` 호출하고 양식 데이터가 게시된 위치에 대상 URL 값을 지정하는 문자열 값을 전달합니다. 양식 디자인에서 대상 URL을 정의하는 경우 빈 문자열을 전달할 수 있습니다. 계산을 수행하기 위해 양식이 전송되는 URL을 지정할 수도 있습니다.

1. 양식에 파일 첨부

   * 생성자를 사용하여 첨부 파일을 저장할 `java.util.HashMap` 객체를 만듭니다.
   * 각 파일에 대해 `java.util.HashMap` 개체의 `put` 메서드를 호출하여 렌더링된 양식에 연결합니다. 다음 값을 이 메서드에 전달합니다.

      * 파일 이름 확장자를 포함하여 파일 첨부 파일의 이름을 지정하는 문자열 값
   * 첨부 파일이 포함된 `BLOB` 개체

   >[!NOTE]
   >
   >양식에 첨부할 각 파일에 대해 이 단계를 반복합니다.

1. 인터랙티브한 PDF 양식 렌더링

   개체의 `FormsService` 메서드를 `renderPDFForm` 호출하고 다음 값을 전달합니다.

   * 파일 이름 확장자를 포함하여 양식 디자인 이름을 지정하는 문자열 값. Forms 응용 프로그램의 일부인 양식 디자인을 참조하는 경우 전체 경로를 지정해야 합니다(예: `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`).
   * 양식과 병합할 데이터가 포함된 `BLOB` 개체 데이터를 병합하지 않으려면 전달하십시오 `null`.
   * 런타임 옵션을 저장하는 `PDFFormRenderSpec` 개체입니다. 이 매개 변수는 선택 사항이며 런타임 옵션을 지정하지 않으려는 `null` 경우 지정할 수 있습니다.
   * Forms 서비스에 필요한 URI 값이 포함된 `URLSpec` 개체입니다.
   * 첨부 파일을 저장하는 `java.util.HashMap` 개체입니다. 선택 매개 변수이며 양식에 파일을 첨부하지 않으려는 `null` 경우 지정할 수 있습니다.
   * 메서드로 채워지는 빈 `com.adobe.idp.services.holders.BLOBHolder` 개체입니다. 렌더링된 PDF 양식을 저장하는 데 사용됩니다.
   * 메서드로 채워지는 빈 `javax.xml.rpc.holders.LongHolder` 개체입니다. 이 인수는 양식의 페이지 수를 저장합니다.
   * 메서드로 채워지는 빈 `javax.xml.rpc.holders.StringHolder` 개체입니다. 이 인수는 로케일 값을 저장합니다.
   * 이 작업 결과를 포함할 빈 `com.adobe.idp.services.holders.FormsResultHolder` 개체입니다.

   이 `renderPDFForm` 메서드는 마지막 인수 값으로 전달되는 `com.adobe.idp.services.holders.FormsResultHolder` 개체를 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림으로 채웁니다.

1. 양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰기

   * 개체 `FormResult` 의 데이터 멤버 값을 가져와서 `com.adobe.idp.services.holders.FormsResultHolder` 개체를 `value` 만듭니다.
   * 개체의 메서드를 호출하여 양식 데이터 `BLOB` 가 포함된 `FormsResult` `getOutputContent` 개체를 만듭니다.
   * 해당 메서드를 호출하여 개체의 `BLOB` 콘텐츠 유형을 `getContentType` 가져옵니다.
   * 해당 메서드를 호출하고 개체의 컨텐트 유형을 전달하여 `javax.servlet.http.HttpServletResponse` 개체의 컨텐트 유형을 `setContentType` `BLOB` 설정합니다.
   * 개체의 메서드를 호출하여 양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰는 데 사용되는 `javax.servlet.ServletOutputStream` 개체를 `javax.servlet.http.HttpServletResponse` `getOutputStream` 만듭니다.
   * 바이트 배열을 만들고 `BLOB` 개체의 메서드를 호출하여 `getBinaryData` 채웁니다. 이 작업은 개체의 내용을 바이트 배열에 `FormsResult` 할당합니다.
   * 개체의 `javax.servlet.http.HttpServletResponse` 메서드를 `write` 호출하여 양식 데이터 스트림을 클라이언트 웹 브라우저에 보냅니다. 바이트 배열을 `write` 메서드로 전달합니다.

**양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰기**

Forms 서비스가 양식을 렌더링하면 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림을 반환합니다. 클라이언트 웹 브라우저에 작성할 때 양식이 사용자에게 표시됩니다.
