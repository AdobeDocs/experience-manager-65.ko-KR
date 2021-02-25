---
title: Forms을 렌더링하는 웹 애플리케이션 만들기
seo-title: Forms을 렌더링하는 웹 애플리케이션 만들기
description: Forms 서비스를 호출하고 양식을 렌더링하는 데 Java 서블릿을 사용하는 웹 기반 응용 프로그램을 만듭니다. Java 서블릿은 양식을 반환하는 Forms 서비스와 클라이언트 웹 브라우저 간의 링크 역할을 합니다.
seo-description: Forms 서비스를 호출하고 양식을 렌더링하는 데 Java 서블릿을 사용하는 웹 기반 응용 프로그램을 만듭니다. Java 서블릿은 양식을 반환하는 Forms 서비스와 클라이언트 웹 브라우저 간의 링크 역할을 합니다.
uuid: 00de10c5-79bd-4d8a-ae18-32f1fd2623bf
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: f29b089e-8902-4744-81c5-15ee41ba8069
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '1915'
ht-degree: 0%

---


# Forms {#creating-web-applications-thatrenders-forms}을(를) 렌더링하는 웹 응용 프로그램 만들기

**이 문서의 샘플과 예는 JEE 환경의 AEM Forms에만 해당됩니다.**

## Forms {#creating-web-applications-that-renders-forms}을(를) 렌더링하는 웹 응용 프로그램 만들기

Forms 서비스를 호출하고 양식을 렌더링하는 데 Java 서블릿을 사용하는 웹 기반 응용 프로그램을 만들 수 있습니다. Java™ 서블릿을 사용하면 프로세스의 반환 값을 클라이언트 웹 브라우저에 작성할 수 있다는 이점이 있습니다. 즉, Java 서블릿을 양식을 반환하는 Forms 서비스와 클라이언트 웹 브라우저 간의 링크로 사용할 수 있습니다.

>[!NOTE]
>
>이 섹션에서는 Forms 서비스를 호출하고 조각을 기반으로 양식을 렌더링하는 Java 서블릿을 사용하는 웹 기반 응용 프로그램을 만드는 방법에 대해 설명합니다. 자세한 내용은 [조각을 기준으로 Forms 렌더링](/help/forms/developing/rendering-forms-based-fragments.md)을 참조하십시오.

Java 서블릿을 사용하면 고객이 데이터를 보고 양식에 입력할 수 있도록 클라이언트 웹 브라우저에 양식을 작성할 수 있습니다. 양식에 데이터를 채우고 나면 웹 사용자가 양식에 있는 제출 버튼을 클릭하여 데이터를 검색 및 처리할 수 있는 Java 서블릿으로 정보를 다시 전송합니다. 예를 들어 데이터를 다른 프로세스로 보낼 수 있습니다.

이 섹션에서는 다음 그림과 같이 사용자가 미국 기반 양식 데이터 또는 캐나다 기반 양식 데이터를 선택할 수 있도록 하는 웹 기반 응용 프로그램을 만드는 방법에 대해 설명합니다.

![cw_cw_fragmentwebclient](assets/cw_cw_fragmentwebclient.png)

렌더링되는 양식은 조각을 기반으로 하는 양식입니다. 즉, 사용자가 미국 데이터를 선택하면 반환된 양식은 미국 데이터를 기반으로 조각을 사용합니다. 예를 들어, 양식의 바닥글에는 다음 그림과 같이 미국 주소가 포함되어 있습니다.

![cw_cw_fragementformfooter](assets/cw_cw_fragementformfooter.png)

마찬가지로 사용자가 캐나다 데이터를 선택하면 반환된 양식에 다음 그림과 같이 캐나다 주소가 포함됩니다.

![cw_cw_fragementformfotercnd](assets/cw_cw_fragementformfootercnd.png)

>[!NOTE]
>
>조각을 기반으로 양식 디자인을 만드는 방법에 대한 자세한 내용은 [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)를 참조하십시오.

**샘플 파일**

이 섹션에서는 다음 위치에 위치할 수 있는 샘플 파일을 사용합니다.

&lt;>Forms Designer 설치 디렉토리&#x200B;*>/Samples/Forms/Purchase Order/Form Fragments*

여기서 &lt;*install directory*>는 설치 경로입니다. 클라이언트 응용 프로그램을 위해 Purchase Order Dynamic.xdp 파일이 이 설치 위치에서 복사되고 *Applications/FormsApplication*&#x200B;이라는 Forms 응용 프로그램에 배포되었습니다. Purchase Order Dynamic.xdp 파일은 FormsFolder라는 폴더에 저장됩니다. 마찬가지로 조각은 다음 그림과 같이 조각 폴더에 배치됩니다.

![cw_cw_fragmentsrepository](assets/cw_cw_fragmentsrepository.png)

Purchase Order Dynamic.xdp 양식 디자인에 액세스하려면 양식 이름(`renderPDFForm` 메서드에 전달된 첫 번째 매개 변수)으로 `Applications/FormsApplication/1.0/FormsFolder/Purchase Order Dynamic.xdp`, 내용 루트 URI 값으로 `repository:///`를 지정합니다.

웹 응용 프로그램에서 사용하는 XML 데이터 파일이 Data 폴더에서 `C:\Adobe`(AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버에 속하는 파일 시스템)으로 이동되었습니다. 파일 이름은 구매 주문서 *Canada.xml* 및 구매 주문서 *US.xml*&#x200B;입니다.

>[!NOTE]
>
>워크벤치를 사용하여 Forms 응용 프로그램을 만드는 방법에 대한 자세한 내용은 [워크벤치 도움말](https://www.adobe.com/go/learn_aemforms_workbench_63)을 참조하십시오.

### {#summary-of-steps} 단계 요약

조각을 기반으로 양식을 렌더링하는 웹 기반 응용 프로그램을 만들려면 다음 단계를 수행하십시오.

1. 새 웹 프로젝트를 만듭니다.
1. Java 서블릿을 나타내는 Java 애플리케이션 로직을 만듭니다.
1. 웹 응용 프로그램의 웹 페이지를 만듭니다.
1. 웹 응용 프로그램을 WAR 파일로 패키지화합니다.
1. WAR 파일을 J2EE 응용 프로그램 서버에 배포합니다.
1. 웹 애플리케이션을 테스트합니다.

>[!NOTE]
>
>이러한 단계 중 일부는 AEM Forms이 배포된 J2EE 애플리케이션에 따라 달라집니다. 예를 들어 WAR 파일을 배포하는 데 사용하는 방법은 사용 중인 J2EE 응용 프로그램 서버에 따라 다릅니다. 이 섹션에서는 AEM Forms이 JBoss®에 배포된다고 가정합니다.

### 웹 프로젝트 만들기 {#creating-a-web-project}

Forms 서비스를 호출할 수 있는 Java 서블릿을 포함하는 웹 응용 프로그램을 만드는 첫 번째 단계는 새 웹 프로젝트를 만드는 것입니다. 이 문서가 기반으로 하는 Java IDE는 Eclipse 3.3입니다. Eclipse IDE를 사용하여 웹 프로젝트를 만들고 필요한 JAR 파일을 프로젝트에 추가합니다. 마지막으로 *index.html*&#x200B;이라는 HTML 페이지와 Java 서블릿을 프로젝트에 추가합니다.

다음 목록은 웹 프로젝트에 추가해야 하는 JAR 파일을 지정합니다.

* adobe-forms-client.jar
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar

이러한 JAR 파일의 위치는 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)을 참조하십시오.

**웹 프로젝트를 만들려면:**

1. Eclipse를 시작하고 **파일** > **새 프로젝트**&#x200B;를 클릭합니다.
1. **새 프로젝트** 대화 상자에서 **웹** > **동적 웹 프로젝트**&#x200B;를 선택합니다.
1. 프로젝트 이름에 `FragmentsWebApplication`을 입력한 다음 **완료**&#x200B;를 클릭합니다.

**프로젝트에 필요한 JAR 파일을 추가하려면:**

1. 프로젝트 탐색기 창에서 `FragmentsWebApplication` 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성**&#x200B;을 선택합니다.
1. **Java 빌드 경로**&#x200B;를 클릭한 다음 **라이브러리** 탭을 클릭합니다.
1. **외부 JAR 추가** 단추를 클릭하고 포함할 JAR 파일을 찾습니다.

**프로젝트에 Java 서블릿을 추가하려면:**

1. 프로젝트 탐색기 창에서 `FragmentsWebApplication` 프로젝트를 마우스 오른쪽 단추로 클릭하고 **새로 만들기** > **기타**&#x200B;를 선택합니다.
1. **웹** 폴더를 확장하고 **서블릿**&#x200B;을 선택한 다음 **다음**&#x200B;을 클릭합니다.
1. 서블릿 만들기 대화 상자에서 서블릿 이름을 `RenderFormFragment`입력한 다음 **완료**&#x200B;를 클릭합니다.

**프로젝트에 HTML 페이지를 추가하려면:**

1. 프로젝트 탐색기 창에서 `FragmentsWebApplication` 프로젝트를 마우스 오른쪽 단추로 클릭하고 **새로 만들기** > **기타**&#x200B;를 선택합니다.
1. **웹** 폴더를 확장하고 **HTML**&#x200B;을 선택하고 **다음**&#x200B;을 클릭합니다.
1. [새 HTML] 대화 상자에서 파일 이름에 `index.html`을 입력한 다음 **완료**&#x200B;를 클릭합니다.

>[!NOTE]
>
>`RenderFormFragment` Java 서블릿을 호출하는 HTML 페이지를 만드는 방법에 대한 자세한 내용은 [웹 페이지 만들기](/help/forms/developing/rendering-forms.md#creating-the-web-page)를 참조하십시오.

### servlet {#creating-java-application-logic-for-the-servlet}에 대한 Java 응용 프로그램 논리 만들기

Java 서블릿 내에서 Forms 서비스를 호출하는 Java 애플리케이션 로직을 생성합니다. 다음 코드는 `RenderFormFragment` Java 서블릿의 구문을 보여 줍니다.

```java
     public class RenderFormFragment extends HttpServlet implements Servlet {
         public void doGet(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {
         doPost(req,resp);
 
         }
         public void doPost(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {
             //Add code here to invoke the Forms service
             }
```

일반적으로 클라이언트 코드는 Java 서블릿의 `doGet` 또는 `doPost` 메서드 내에 삽입하지 않습니다. 더 나은 프로그래밍 방법은 이 코드를 별도의 클래스 내에 배치하고 `doPost` 메서드(또는 `doGet` 메서드) 내에서 클래스를 인스턴스화하고 적절한 메서드를 호출하는 것입니다. 그러나 코드 간결성의 경우 이 섹션의 코드 예는 최소로 유지되며 코드 예제는 `doPost` 메서드에 배치됩니다.

Forms 서비스 API를 사용하여 조각을 기반으로 양식을 렌더링하려면 다음 작업을 수행합니다.

1. Java 프로젝트의 클래스 경로에 adobe-forms-client.jar 등의 클라이언트 JAR 파일을 포함합니다. 이러한 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)을 참조하십시오.
1. HTML 양식에서 제출한 라디오 단추의 값을 검색하고 미국 또는 캐나다 데이터를 사용할지 여부를 지정합니다. American이 제출되면 *Purchase Order US.xml*&#x200B;에 있는 데이터를 저장하는 `com.adobe.idp.Document`을 만듭니다. 마찬가지로 캐나다인 경우 *Purchase Order Canada.xml* 파일에 있는 데이터를 저장하는 `com.adobe.idp.Document`을 만듭니다.
1. 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다. ([연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)을 참조하십시오.)
1. 생성자를 사용하여 `FormsServiceClient` 개체를 만들고 `ServiceClientFactory` 개체를 전달합니다.
1. 생성자를 사용하여 URI 값을 저장하는 `URLSpec` 객체를 만듭니다.
1. `URLSpec` 객체의 `setApplicationWebRoot` 메서드를 호출하고 응용 프로그램의 웹 루트를 나타내는 문자열 값을 전달합니다.
1. `URLSpec` 객체의 `setContentRootURI` 메서드를 호출하고 내용 루트 URI 값을 지정하는 문자열 값을 전달합니다. 양식 디자인과 조각이 컨텐츠 루트 URI에 있는지 확인합니다. 그렇지 않은 경우 Forms 서비스에서 예외가 발생합니다. AEM Forms 리포지토리를 참조하려면 `repository://`을 지정합니다.
1. `URLSpec` 객체의 `setTargetURL` 메서드를 호출하고 양식 데이터가 게시된 위치로 대상 URL 값을 지정하는 문자열 값을 전달합니다. 양식 디자인에서 대상 URL을 정의하는 경우 빈 문자열을 전달할 수 있습니다. 계산을 수행하기 위해 양식이 전송되는 URL을 지정할 수도 있습니다.
1. `FormsServiceClient` 객체의 `renderPDFForm` 메서드를 호출하고 다음 값을 전달합니다.

   * 파일 이름 확장자를 포함하여 양식 디자인 이름을 지정하는 문자열 값입니다.
   * 양식과 병합할 데이터가 포함된 `com.adobe.idp.Document` 개체(2단계에서 생성됨).
   * 런타임 옵션을 저장하는 `PDFFormRenderSpec` 객체입니다. 자세한 내용은 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)를 참조하십시오.
   * 조각을 기반으로 양식을 렌더링하는 데 필요한 URI 값이 포함된 `URLSpec` 개체
   * 첨부 파일을 저장하는 `java.util.HashMap` 객체입니다. 이 매개 변수는 선택 사항이며, 양식에 파일을 첨부하지 않으려면 `null`을 지정할 수 있습니다.

   `renderPDFForm` 메서드는 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림을 포함하는 `FormsResult` 객체를 반환합니다.

1. `FormsResult` 개체 &#39;s `getOutputContent` 메서드를 호출하여 `com.adobe.idp.Document` 개체를 만듭니다.
1. `getContentType` 메서드를 호출하여 `com.adobe.idp.Document` 객체의 내용 유형을 가져옵니다.
1. `setContentType` 메서드를 호출하고 `com.adobe.idp.Document` 개체의 내용 유형을 전달하여 `javax.servlet.http.HttpServletResponse` 개체의 내용 유형을 설정합니다.
1. `javax.servlet.http.HttpServletResponse` 개체의 `getOutputStream` 메서드를 호출하여 양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰는 데 사용되는 `javax.servlet.ServletOutputStream` 개체를 만듭니다.
1. `com.adobe.idp.Document` 객체의 `getInputStream` 메서드를 호출하여 `java.io.InputStream` 객체를 만듭니다.
1. 바이트 배열을 만들어 `InputStream` 객체의 `read` 메서드를 호출하고 바이트 배열을 인수로 전달하여 양식 데이터 스트림으로 채웁니다.
1. 양식 데이터 스트림을 클라이언트 웹 브라우저에 보내려면 `javax.servlet.ServletOutputStream` 객체의 `write` 메서드를 호출합니다. 바이트 배열을 `write` 메서드에 전달합니다.

다음 코드 예는 Forms 서비스를 호출하고 조각을 기반으로 양식을 렌더링하는 Java 서블릿을 나타냅니다.

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.File;
 import java.io.FileInputStream;
 import java.io.IOException;
 import java.io.PrintWriter;
 
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 import java.io.InputStream;
 import java.net.URL;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class RenderFormFragment extends HttpServlet implements Servlet {
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
             doPost(req,resp);
 
     }
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
     throws ServletException, IOException {
 
 
 
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Get the value of selected radio button
             String radioValue = req.getParameter("radio");
 
             //Create an Document object to store form data
             Document oInputData = null;
 
             //The value of the radio button determines the form data to use
             //which determines which fragments used in the form
             if (radioValue.compareTo("AMERICAN") == 0)            {
                 FileInputStream myData = new FileInputStream("C:\\Adobe\Purchase Order US.xml");
                 oInputData = new Document(myData);
             }
             else if (radioValue.compareTo("CANADIAN") == 0)            {
                 FileInputStream myData = new FileInputStream("C:\\Adobe\Purchase Order Canada.xml");
                 oInputData = new Document(myData);
             }
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a FormsServiceClient object
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
             //Set the parameter values for the renderPDFForm method
             String formName = "Applications/FormsApplication/1.0/FormsFolder/Purchase Order Dynamic.xdp";
 
             //Cache the PDF form
             PDFFormRenderSpec pdfFormRenderSpec = new PDFFormRenderSpec();
             pdfFormRenderSpec.setCacheEnabled(new Boolean(true));
 
             //Specify URI values that are required to render a form
             //design based on fragments
             URLSpec uriValues = new URLSpec();
             uriValues.setApplicationWebRoot("https://'[server]:[port]'/RenderFormFragment");
             uriValues.setContentRootURI("repository:///");
             uriValues.setTargetURL("https://'[server]:[port]'/FormsServiceClientApp/HandleData");
 
             //Invoke the renderPDFForm method and write the
             //results to a client web browser
             FormsResult formOut = formsClient.renderPDFForm(
                         formName,               //formQuery
                         oInputData,             //inDataDoc
                         pdfFormRenderSpec,      //PDFFormRenderSpec
                         uriValues,                //urlSpec
                         null                    //attachments
                         );
 
             //Create a Document object that stores form data
             Document myData = formOut.getOutputContent();
 
             //Get the content type of the response and
             //set the HttpServletResponse object’s content type
             String contentType = myData.getContentType();
             resp.setContentType(contentType);
 
             //Create a ServletOutputStream object
             ServletOutputStream oOutput = resp.getOutputStream();
 
             //Create an InputStream object
             InputStream inputStream = myData.getInputStream();
 
             //Write the data stream to the web browser
             byte[] data = new byte[4096];
             int bytesRead = 0;
             while ((bytesRead = inputStream.read(data)) > 0)
             {
                 oOutput.write(data, 0, bytesRead);
             }
 
         }catch (Exception e) {
              System.out.println("The following exception occurred: "+e.getMessage());
       }
     }
 }
```

### 웹 페이지 {#creating-the-web-page} 만들기

index.html 웹 페이지는 Java 서블릿의 시작 지점을 제공하고 Forms 서비스를 호출합니다. 이 웹 페이지는 2개의 라디오 버튼과 제출 단추가 포함된 기본 HTML 양식입니다. 라디오 단추의 이름은 라디오입니다. 사용자가 제출 단추를 클릭하면 양식 데이터가 `RenderFormFragment` Java 서블릿에 게시됩니다.

Java 서블릿은 다음 Java 코드를 사용하여 HTML 페이지에서 게시되는 데이터를 캡처합니다.

```java
             Document oInputData = null;
 
             //Get the value of selected radio button
             String radioValue = req.getParameter("radio");
 
             //The value of the radio button determines the form data to use
             //which determines which fragments used in the form
             if (radioValue.compareTo("AMERICAN") == 0)            {
                 FileInputStream myData = new FileInputStream("C:\\Adobe\Purchase Order US.xml");
                 oInputData = new Document(myData);
             }
             else if (radioValue.compareTo("CANADIAN") == 0)            {
                 FileInputStream myData = new FileInputStream("C:\\Adobe\Purchase Order Canada.xml");
                 oInputData = new Document(myData);
             }
```

다음 HTML 코드는 개발 환경을 설정하는 동안 만들어진 index.html 파일에 있습니다. ([웹 프로젝트 만들기](/help/forms/developing/rendering-forms.md#creating-a-web-project)를 참조하십시오.)

```xml
 <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
 <html xmlns="https://www.w3.org/1999/xhtml">
 <head>
 <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
 <title>Untitled Document</title>
 </head>
 
 <body>
 <form name="myform" action="https://'[server]:[port]'/FragmentsWebApplication/RenderFormFragment" method="post">
      <table>
      <tr>
        <th>Forms Fragment Web Client</th>
      </tr>
      <tr>
        <td>
          <label>
          <input type="radio" name="radio" id="radio_Data" value="CANADIAN" />
          Canadian data<br />
          </label>
          <p>
            <label>
            <input type="radio" name="radio" id="radio_Data" value="AMERICAN" checked/>
            American data</label>
          </p>
        </td>
      </tr>
      <tr>
      <td>
        <label>
          <input type="submit" name="button_Submit" id="button_Submit" value="Submit" />
            </label>
            </td>
         </tr>
        </table>
      </form>
 </body>
 </html>
```

### 웹 응용 프로그램 패키징 {#packaging-the-web-application}

Forms 서비스를 호출하는 Java 서블릿을 배포하려면 웹 애플리케이션을 WAR 파일로 패키지합니다. adobe-livecycle-client.jar 및 adobe-forms-client.jar와 같이 구성 요소의 비즈니스 로직이 의존하는 외부 JAR 파일도 WAR 파일에도 포함되어 있는지 확인합니다.

**웹 응용 프로그램을 WAR 파일로 패키지하는 방법은 다음과 같습니다.**

1. **프로젝트 탐색기** 창에서 `FragmentsWebApplication` 프로젝트를 마우스 오른쪽 단추로 클릭하고 **내보내기** > **WAR 파일**&#x200B;을 선택합니다.
1. **웹 모듈** 텍스트 상자에 Java 프로젝트의 이름에 `FragmentsWebApplication`를 입력합니다.
1. **대상** 텍스트 상자에 `FragmentsWebApplication.war`**파일 이름에**&#x200B;를 입력하고 WAR 파일 위치를 지정한 다음 마침을 클릭합니다.

### J2EE 응용 프로그램 서버 {#deploying-the-war-file-to-the-j2ee-application-server}에 WAR 파일 배포

WAR 파일을 AEM Forms이 배포된 J2EE 응용 프로그램 서버에 배포할 수 있습니다. WAR 파일이 배포된 후 웹 브라우저를 사용하여 HTML 웹 페이지에 액세스할 수 있습니다.

**WAR 파일을 J2EE 응용 프로그램 서버에 배포하려면:**

* 내보내기 경로에서 `[Forms Install]\Adobe\Adobe Experience Manager Forms\jboss\server\all\deploy`(으)로 WAR 파일을 복사합니다.

### 웹 응용 프로그램 테스트 {#testing-your-web-application}

웹 응용 프로그램을 배포한 후 웹 브라우저를 사용하여 테스트할 수 있습니다. AEM Forms을 호스팅하는 컴퓨터를 사용하고 있다고 가정할 경우 다음 URL을 지정할 수 있습니다.

* http://localhost:8080/FragmentsWebApplication/index.html

   라디오 단추를 선택하고 [제출] 단추를 클릭합니다. 조각을 기반으로 하는 양식이 웹 브라우저에 표시됩니다. 문제가 발생하면 J2EE 응용 프로그램 서버의 로그 파일을 참조하십시오.

