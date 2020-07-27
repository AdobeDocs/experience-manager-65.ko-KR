---
title: 인간 중심의 오랜 프로세스 호출
seo-title: 인간 중심의 오랜 프로세스 호출
description: 'null'
seo-description: 'null'
uuid: 42269d41-a90f-4ea1-aeb9-d61337bcfa54
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 18a320b4-dce6-4c50-8864-644b0b2d6644
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '3669'
ht-degree: 0%

---


# 인간 중심의 오랜 프로세스 호출 {#invoking-human-centric-long-lived-processes}

다음과 같은 클라이언트 애플리케이션을 사용하여 Workbench에서 만든 인간 중심의 긴 수명 프로세스를 프로그래밍 방식으로 호출할 수 있습니다.

* 호출 API를 사용하는 Java 웹 기반 클라이언트 응용 프로그램. ( [Java API를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-java.md)(/help/forms/developing/invoking-aem-forms-using-java.md#calling-aem-forms-using-the-java-api)을 참조하십시오.)
* 웹 서비스를 사용하는 ASP.NET 응용 프로그램입니다. (웹 서비스를 [사용하여 AEM Forms 호출을 참조하십시오](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)
* Remoting을 사용하는 Flex를 사용하여 구축한 클라이언트 애플리케이션 (AEM Forms [호출을 사용하여(AEM 양식에서 더 이상 사용되지 않음) AEM Forms Remoting을 참조하십시오](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

호출되는 긴 프로세스 이름은 *FirstAppSolution/PreLoanProcess입니다*. 첫 번째 AEM Forms 응용 프로그램 만들기에 지정된 자습서 [에 따라 이 프로세스를 만들 수 있습니다](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63).

인간 중심 프로세스에는 사용자가 작업 공간을 사용하여 응답할 수 있는 작업이 포함됩니다. 예를 들어 워크벤치를 사용하여 은행 관리자가 대출 신청을 승인하거나 거부할 수 있는 프로세스를 생성할 수 있습니다. 다음 그림은 FirstAppSolution/ *PreLoanProcess 프로세스를 보여줍니다*.

FirstAppSolution/ *PreLoanProcess* 프로세스는 데이터 유형이 XML인 *formData라는 입력 매개 변수를* 허용합니다. XML 데이터는 PreLoanForm.xdp라는 양식 디자인과 *병합됩니다*. 다음 그림은 대출 신청을 승인하거나 거부할 사용자에게 지정된 작업을 나타내는 양식입니다. 사용자는 작업 공간을 사용하여 응용 프로그램을 승인하거나 거부합니다. Workspace 사용자는 다음 그림에 표시된 승인 버튼을 클릭하여 대출 요청을 승인할 수 있습니다. 마찬가지로 사용자는 거부 버튼을 클릭하여 대출 요청을 거부할 수 있습니다.

긴 수명 프로세스는 비동기적으로 호출되며 다음 요인으로 인해 동기적으로 호출할 수 없습니다.

* 프로세스는 상당한 시간 동안 진행될 수 있습니다.
* 프로세스는 조직의 경계를 확장할 수 있습니다.
* 프로세스를 완료하려면 외부 입력이 필요합니다. 예를 들어 사무실 밖에 있는 관리자에게 양식이 전송되는 상황을 고려해 보십시오. 이 경우 관리자가 양식을 반환하고 채울 때까지 프로세스가 완료되지 않습니다.

긴 프로세스가 호출되면 AEM Forms은 레코드 만들기의 일부로 호출 식별자 값을 만듭니다. 이 레코드는 긴 프로세스 상태를 추적하고 AEM Forms 데이터베이스에 저장됩니다. 호출 식별자 값을 사용하여 긴 프로세스 상태를 추적할 수 있습니다. 또한 프로세스 호출 식별자 값을 사용하여 실행 중인 프로세스 인스턴스 종료와 같은 프로세스 관리자 작업을 수행할 수 있습니다.

>[!NOTE]
>
>AEM Forms은 짧은 기간 프로세스를 호출할 때 호출 식별자 값 또는 레코드를 만들지 않습니다.

신청자가 XML 데이터로 표시되는 응용 프로그램을 제출할 때 이 `FirstAppSolution/PreLoanProcess` 프로세스가 호출됩니다. 입력 프로세스 변수의 이름 `formData` 은 XML이고 해당 데이터 유형은 XML입니다. 이 토론의 목적을 위해 다음 XML 데이터가 `FirstAppSolution/PreLoanProcess` 프로세스에 입력되는 것으로 사용된다고 가정합니다.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <LoanApp>
 <Name>Sam White</Name>
 <LoanAmount>250000</LoanAmount>
 <PhoneOrEmail>(555)555-5555</PhoneOrEmail>
 <ApprovalStatus>PENDING APPROVAL</ApprovalStatus>
 </LoanApp>
```

프로세스에 전달된 XML 데이터는 프로세스에서 사용되는 양식에 있는 필드와 일치해야 합니다. 그렇지 않으면 데이터가 양식 내에 표시되지 않습니다. 프로세스를 호출하는 모든 응용 프로그램은 이 XML 데이터 소스를 `FirstAppSolution/PreLoanProcess` 전달해야 합니다. 인간 중심 장기 *프로세스* 호출에서 생성된 애플리케이션은 사용자가 웹 클라이언트에 입력한 값에서 XML 데이터 소스를 동적으로 생성합니다.

클라이언트 응용 프로그램을 사용하여 필요한 XML 데이터를 *FirstAppSolution/PreLoanProcess* 프로세스를 전송할 수 있습니다. 긴 프로세스는 호출 식별자 값을 반환 값으로 반환합니다. 다음 그림은 긴 수명 프로세스를 호출하는 클라이언트 응용 프로그램을 보여 줍니다. 클라이언트 응용 프로그램은 XML 데이터를 보내고 호출 식별자 값을 나타내는 문자열 값을 반환합니다.

**참고 항목**

[인간 중심의 오랜 프로세스를 불러일으키는 Java 웹 애플리케이션 제작](invoking-human-centric-long-lived.md#creating-a-java-web-application-that-invokes-a-human-centric-long-lived-process)

[인간 중심의 오랜 프로세스를 호출하는 ASP.NET 웹 응용 프로그램 만들기](invoking-human-centric-long-lived.md#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process)

[인간 중심의 오랜 프로세스를 불러일으키는 Flex를 사용하여 구축한 클라이언트 애플리케이션 제작](invoking-human-centric-long-lived.md#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process)

## 인간 중심의 오랜 프로세스를 불러일으키는 Java 웹 애플리케이션 제작 {#creating-a-java-web-application-that-invokes-a-human-centric-long-lived-process}

Java 서블릿을 사용하여 `FirstAppSolution/PreLoanProcess` 프로세스를 호출하는 웹 기반 응용 프로그램을 생성할 수 있습니다. Java 서블릿에서 이 프로세스를 호출하려면 Java 서블릿 내 호출 API를 사용하십시오. (Java [API를 사용하여 AEM Forms 호출을 참조하십시오](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api).)

다음 그림은 이름, 전화(또는 이메일) 및 금액 값을 게시하는 웹 기반 클라이언트 응용 프로그램을 보여줍니다. 이 값은 사용자가 [응용 프로그램 제출] 단추를 클릭하면 Java 서블릿으로 전송됩니다.

Java 서블릿은 다음 작업을 수행합니다.

* HTML 페이지에서 Java 서블릿으로 게시된 값을 검색합니다.
* XML 데이터 소스를 동적으로 만들어 *FirstAppSolution/PreRoanProcess* 프로세스에 전달합니다. 이름, 전화(또는 이메일) 및 금액 값은 XML 데이터 소스에 지정됩니다.
* AEM Forms 호출 API를 사용하여 *FirstAppSolution/PreLoanProcess* 프로세스를 호출합니다.
* 클라이언트 웹 브라우저에 호출 식별자 값을 반환합니다.

### 단계 요약 {#summary-of-steps}

프로세스를 호출하는 Java 웹 기반 응용 프로그램을 만들려면 `FirstAppSolution/PreLoanProcess` 다음 단계를 수행하십시오.

1. [웹 프로젝트](invoking-human-centric-long-lived.md#create-a-web-project)만들기
1. [서블릿에 대한 Java 애플리케이션 로직을 생성합니다](invoking-human-centric-long-lived.md#create-java-application-logic-for-the-servlet).
1. [웹 응용 프로그램의 웹 페이지 만들기](invoking-human-centric-long-lived.md#create-the-web-page-for-the-web-application)
1. [웹 응용 프로그램을 WAR 파일로 패키지합니다](invoking-human-centric-long-lived.md#package-the-web-application-to-a-war-file).
1. [AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버에 WAR 파일을 배포합니다](invoking-human-centric-long-lived.md#deploy-the-war-file-to-the-j2ee-application-server-hosting-aem-forms).
1. [웹 애플리케이션](invoking-human-centric-long-lived.md#test-your-web-application)테스트

>[!NOTE]
>
>이러한 단계 중 일부는 AEM Forms이 배포된 J2EE 애플리케이션에 따라 달라집니다. 예를 들어 WAR 파일을 배포하는 데 사용하는 방법은 사용 중인 J2EE 응용 프로그램 서버에 따라 다릅니다. AEM Forms이 JBoss®에 배포된다고 가정합니다.

### 웹 프로젝트 만들기 {#create-a-web-project}

웹 애플리케이션을 만드는 첫 번째 단계는 웹 프로젝트를 만드는 것입니다. 이 문서가 기반으로 하는 Java IDE는 Eclipse 3.3입니다. Eclipse IDE를 사용하여 웹 프로젝트를 만들고 필요한 JAR 파일을 프로젝트에 추가합니다. 프로젝트에 index.html *과 Java 서블릿이라는* HTML 페이지를 추가합니다.

다음 목록은 웹 프로젝트에 포함할 JAR 파일을 지정합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* J2EE.jar

이러한 JAR 파일의 위치는 AEM Forms Java 라이브러리 파일 [포함을 참조하십시오](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

>[!NOTE]
>
>J2EE.jar 파일은 Java 서블릿에 사용되는 데이터 유형을 정의합니다. AEM Forms이 배포된 J2EE 응용 프로그램 서버에서 이 JAR 파일을 가져올 수 있습니다.

**웹 프로젝트 만들기**

1. Eclipse를 시작하고 **파일** > **새 프로젝트를 클릭합니다**.
1. 새 프로젝트 **대화** 상자에서 **웹** > **동적 웹 프로젝트**&#x200B;를선택합니다.
1. 프로젝트 이름 `InvokePreLoanProcess` 을 입력한 다음 마침을 **클릭합니다**.

**프로젝트에 필요한 JAR 파일 추가**

1. 프로젝트 탐색기 창에서 프로젝트를 마우스 오른쪽 버튼으로 클릭하고 속성 `InvokePreLoanProcess` 을 선택합니다 ****.
1. Java **빌드 경로를** 클릭한 다음 **라이브러리** 탭을 클릭합니다.
1. 외부 JAR **추가** 버튼을 클릭하고 포함할 JAR 파일을 찾습니다.

**프로젝트에 Java 서블릿 추가**

1. 프로젝트 탐색기 창에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 `InvokePreLoanProcess` 새로 만들기 **>** 기타 **를 선택합니다**.
1. 웹 **폴더를** 확장하고 서블릿을 **선택한**&#x200B;다음 **을 클릭합니다**.
1. 서블릿 만들기 대화 상자에서 서블릿 이름 `SubmitXML` 을 입력한 다음 **마침을 클릭합니다**.

**프로젝트에 HTML 페이지 추가**

1. 프로젝트 탐색기 창에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 `InvokePreLoanProcess` 새로 만들기 **>** 기타 **를 선택합니다**.
1. **웹** 폴더를 확장하고 **HTML을**&#x200B;선택한 다음 **다음을**&#x200B;클릭합니다.
1. 새 HTML 대화 상자에서 파일 이름 `index.html` 을 입력한 다음 마침을 **클릭합니다**.

>[!NOTE]
>
>SubmitXML Java 서블릿을 호출하는 HTML 컨텐츠를 만드는 방법에 대한 자세한 내용은 웹 응용 [프로그램의 웹 페이지 만들기를 참조하십시오](invoking-human-centric-long-lived.md#create-the-web-page-for-the-web-application).

### 서블릿에 대한 Java 응용 프로그램 논리 생성 {#create-java-application-logic-for-the-servlet}

Java 서블릿 내에서 프로세스를 호출하는 `FirstAppSolution/PreLoanProcess` Java 애플리케이션 로직을 생성합니다. 다음 코드는 Java 서블릿의 구문을 `SubmitXML` 보여 줍니다.

```java
     public class SubmitXML extends HttpServlet implements Servlet {
         public void doGet(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {
         doPost(req,resp);
 
         }
         public void doPost(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {
             //Add code here to invoke the FirstAppSolution/PreLoanProcess process
             }
```

일반적으로 클라이언트 코드는 Java 서블릿이나 메서드 내에 배치되지 `doGet` 않습니다 `doPost` . 더 좋은 프로그래밍 방법은 이 코드를 별도의 클래스 내에 넣는 것입니다. 그런 다음 메서드(또는 메서드) 내에서 `doPost` 클래스를 `doGet` 인스턴스화하고 적절한 메서드를 호출합니다. 그러나 코드 간결성의 경우 코드 예제는 최소로 유지되며 `doPost` 메서드에 배치됩니다.

호출 API를 사용하여 `FirstAppSolution/PreLoanProcess` 프로세스를 호출하려면 다음 작업을 수행하십시오.

1. Java 프로젝트의 클래스 경로에 adobe-livecycle-client.jar와 같은 클라이언트 JAR 파일을 포함합니다. 이러한 파일의 위치에 대한 자세한 내용은 AEM Forms Java 라이브러리 파일 [포함을 참조하십시오](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).
1. HTML 페이지에서 제출한 이름, 전화 및 금액 값을 검색합니다. 이러한 값을 사용하여 프로세스에 전송되는 XML 데이터 소스를 동적으로 만들 수 `FirstAppSolution/PreLoanProcess` 있습니다. 클래스를 사용하여 XML 데이터 소스 `org.w3c.dom` 를 만들 수 있습니다(이 응용 프로그램 논리는 다음 코드 예제에서 표시됨).
1. 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다. 연결 [속성 설정을 참조하십시오](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).
1. 생성자를 사용하여 개체를 `ServiceClient` 만들고 개체를 `ServiceClientFactory` 전달합니다. 객체를 사용하면 서비스 작업을 호출할 수 `ServiceClient` 있습니다. 호출 요청 찾기, 전달 및 라우팅 등의 작업을 처리합니다.
1. 생성자를 사용하여 `java.util.HashMap` 개체를 만듭니다.
1. 각 입력 매개 변수에 대해 `java.util.HashMap` 개체의 `put` 메서드를 호출하여 오래 지속되는 프로세스로 전달합니다. 프로세스의 입력 매개변수 이름을 지정해야 합니다. 이 `FirstAppSolution/PreLoanProcess` 프로세스에는 유형 `XML` (이름)의 입력 매개 변수가 하나만 필요하므로 메서드를 한 번만 `formData``put` 호출하면 됩니다.

   ```java
    //Get the XML to pass to the FirstAppSolution/PreLoanProcess process
    org.w3c.dom.Document inXML = GetDataSource(name,phone,amount);
    
    //Create a Map object to store the parameter value
    Map params = new HashMap();
    params.put("formData", inXML);
   ```

1. 개체의 메서드를 호출하고 다음 값을 전달하여 `InvocationRequest` 개체를 `ServiceClientFactory` `createInvocationRequest` 만듭니다.

   * 호출할 긴 프로세스 이름을 지정하는 문자열 값. 프로세스를 `FirstAppSolution/PreLoanProcess` 호출하려면 을 지정합니다 `FirstAppSolution/PreLoanProcess`.
   * 프로세스 작업 이름을 나타내는 문자열 값입니다. 긴 프로세스 작업의 이름입니다 `invoke`.
   * 서비스 작업에 필요한 매개 변수 값이 포함된 `java.util.HashMap` 개체입니다.
   * 비동기 요청을 만드는 부울 값 `false`(이 값은 긴 프로세스를 호출하는 데 적용 가능)입니다.

   >[!NOTE]
   >
   >*value true를 createInvocationRequest 메서드의 네 번째 매개 변수로 전달하여 단기 프로세스를 호출할 수 있습니다. true 값을 전달하면 동기 요청이 만들어집니다.*

1. 개체의 메서드를 호출하고 개체를 전달하여 호출 요청을 AEM Forms으로 `ServiceClient` `invoke` `InvocationRequest` 보냅니다. 이 `invoke` 메서드는 `InvocationReponse` 개체를 반환합니다.
1. 긴 프로세스는 호출 식별 값을 나타내는 문자열 값을 반환합니다. 개체의 메서드를 호출하여 이 값 `InvocationReponse` 을 `getInvocationId` 검색합니다.

   ```java
    //Send the invocation request to the long-lived process and
    //get back an invocation response object
    InvocationResponse lcResponse = myServiceClient.invoke(lcRequest);
    String invocationId = lcResponse.getInvocationId();
   ```

1. 클라이언트 웹 브라우저에 호출 식별 값을 씁니다. 인스턴스를 사용하여 이 값을 클라이언트 웹 브라우저에 작성할 수 `java.io.PrintWriter` 있습니다.

### 빠른 시작: 호출 API를 사용하여 긴 프로세스 호출 {#quick-start-invoking-a-long-lived-process-using-the-invocation-api}

다음 Java 코드 예는 프로세스를 호출하는 Java 서블릿을 `FirstAppSolution/PreLoanProcess` 나타냅니다.

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-livecycle-client.jar
     * 2. adobe-usermanager-client.jar
     *
     * (Because this  quick start is implemented as a Java servlet, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     * */
 import java.io.ByteArrayOutputStream;
 import java.io.File;
 import java.io.IOException;
 import java.io.PrintWriter;
 
 import javax.servlet.ServletException;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import java.util.*;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import javax.xml.parsers.DocumentBuilder;
 import javax.xml.parsers.DocumentBuilderFactory;
 import javax.xml.transform.Transformer;
 import javax.xml.transform.TransformerFactory;
 import javax.xml.transform.dom.DOMSource;
 import javax.xml.transform.stream.StreamResult;
 
 import com.adobe.idp.dsc.InvocationRequest;
 import com.adobe.idp.dsc.InvocationResponse;
 import com.adobe.idp.dsc.clientsdk.ServiceClient;
 import org.w3c.dom.Element;
 
     public class SubmitXML extends javax.servlet.http.HttpServlet implements javax.servlet.Servlet {
       static final long serialVersionUID = 1L;
 
        public SubmitXML() {
         super();
     }
 
 
     protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
         // TODO Auto-generated method stub
         doPost(request,response);
     }
 
     protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
 
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://localhost:1099");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a ServiceClient object
             ServiceClient myServiceClient = myFactory.getServiceClient();
 
             //Get the values that are passed from the Loan HTML page
             String name = (String)request.getParameter("name");
             String phone = (String)request.getParameter("phone");
             String amount = (String)request.getParameter("amount");
 
             //Create XML to pass to the FirstAppSolution/PreLoanProcess process
             org.w3c.dom.Document inXML = GetDataSource(name,phone,amount);
 
             //Create a Map object to store the XML input parameter value
             Map params = new HashMap();
             params.put("formData", inXML);
 
             //Create an InvocationRequest object
             InvocationRequest lcRequest =  myFactory.createInvocationRequest(
                 "FirstAppSolution/PreLoanProcess", //Specify the long-lived process name
                     "invoke",           //Specify the operation name
                     params,               //Specify input values
                     false);               //Create an asynchronous request
 
             //Send the invocation request to the long-lived process and
             //get back an invocation response object
             InvocationResponse lcResponse = myServiceClient.invoke(lcRequest);
             String invocationId = lcResponse.getInvocationId();
 
             //Create a PrintWriter instance
             PrintWriter pp = response.getWriter();
 
             //Write the invocation identifier value back to the client web browser
             pp.println("The job status identifier value is: " +invocationId);
 
         }catch (Exception e) {
              System.out.println("The following exception occurred: "+e.getMessage());
       }
     }
 
 
      //Create XML data to pass to the long-lived process
      private static org.w3c.dom.Document GetDataSource(String name, String phone, String amount)
      {
             org.w3c.dom.Document document = null;
 
             try
             {
                 //Create DocumentBuilderFactory and DocumentBuilder objects
                 DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
                 DocumentBuilder builder = factory.newDocumentBuilder();
 
                 //Create a new Document object
                 document = builder.newDocument();
 
                 //Create MortgageApp - the root element in the XML
                 Element root = (Element)document.createElement("LoanApp");
                 document.appendChild(root);
 
                 //Create an XML element for Name
                 Element nameElement = (Element)document.createElement("Name");
                 nameElement.appendChild(document.createTextNode(name));
                 root.appendChild(nameElement);
 
                 //Create an XML element for Phone
                 Element phoneElement = (Element)document.createElement("PhoneOrEmail");
                 phoneElement.appendChild(document.createTextNode(phone));
                 root.appendChild(phoneElement);
 
                 //Create an XML element for amount
                 Element loanElement = (Element)document.createElement("LoanAmount");
                 loanElement.appendChild(document.createTextNode(amount));
                 root.appendChild(loanElement);
 
                 //Create an XML element for ApprovalStatus
                 Element approveElement = (Element)document.createElement("ApprovalStatus");
                 approveElement.appendChild(document.createTextNode("PENDING APPROVAL"));
                 root.appendChild(approveElement);
 
               }
          catch (Exception e) {
                   System.out.println("The following exception occurred: "+e.getMessage());
                }
         return document;
          }
         }
```

### 웹 응용 프로그램의 웹 페이지 만들기 {#create-the-web-page-for-the-web-application}

index.html *웹 페이지는* `FirstAppSolution/PreLoanProcess` 프로세스를 호출하는 Java 서블릿의 시작 지점을 제공합니다. 이 웹 페이지는 HTML 양식과 제출 단추가 포함된 기본 HTML 양식입니다. 사용자가 전송 단추를 클릭하면 양식 데이터가 `SubmitXML` Java 서블릿에 게시됩니다.

Java 서블릿은 다음 Java 코드를 사용하여 HTML 페이지에서 게시되는 데이터를 캡처합니다.

```java
 //Get the values that are passed from the Loan HTML page
 String name = request.getParameter("name");
 String phone = request.getParameter("phone");
 String amount = request.getParameter("amount");
```

다음 HTML 코드는 개발 환경을 설정하는 동안 만들어진 index.html 파일을 나타냅니다. 웹 프로젝트 [만들기를 참조하십시오](invoking-human-centric-long-lived.md#create-a-web-project).

```xml
 <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "https://www.w3.org/TR/html4/loose.dtd">
 <html>
 <head>
 <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
 <title>Insert title here</title>
 </head>
 <body>
 <table>
     <TBODY>
         <TR>
             <td><img src="financeCorpLogo.jpg" width="172" height="62"></TD>
             <td><FONT size="+2"><strong>Java Loan Application Page</strong></FONT></TD>
             <td> </TD>
             <td> </TD>
         </TR>
 
     </TBODY>
 </TABLE>
     <FORM action="https://hiro-xp:8080/PreLoanProcess/SubmitXML" method="post">
        <table>
          <TBODY>
                <TR>
                      <td><LABEL for="name">Name: </LABEL></TD>
                  <td><INPUT type="text" name="name"></TD>
                  <td><input type="submit" value="Submit Application"></TD>
                  </TR>
            <TR>
                  <td> <LABEL for="phone">Phone/Email: </LABEL></TD>
              <td><INPUT type="text" name="phone"></TD>
                  <td></TD>
              </TR>
 
            <TR>
                  <td><LABEL for="amount">Amount: </LABEL></TD>
              <td><INPUT type="text" name="amount"></TD>
                 <td></TD>
             </TR>
          </TBODY>
 </TABLE>
       </FORM>
 </body>
 </html>
```

### 웹 응용 프로그램을 WAR 파일로 패키지 {#package-the-web-application-to-a-war-file}

프로세스를 호출하는 Java 서블릿을 `FirstAppSolution/PreLoanProcess` 배포하려면 웹 응용 프로그램을 WAR 파일로 패키지합니다. 구성 요소의 비즈니스 로직이 의존하는 외부 JAR 파일도 WAR 파일에 포함되어 있는지 확인합니다(예: adobe-livecycle-client.jar 및 adobe-usermanager-client.jar).

다음 그림은 WAR 파일로 패키지된 Eclipse 프로젝트의 컨텐츠를 보여줍니다.

>[!NOTE]
>
>이전 그림에서는 JPG 파일을 모든 JPG 이미지 파일로 대체할 수 있습니다.

**웹 응용 프로그램을 WAR 파일로 패키지합니다.**

1. 프로젝트 **탐색기** 창에서 프로젝트를 마우스 오른쪽 버튼으로 클릭하고 내보내기 `InvokePreLoanProcess` > **WAR 파일** 을 **선택합니다**.
1. 웹 **모듈** 텍스트 상자에 Java 프로젝트 `InvokePreLoanProcess` 의 이름을 입력합니다.
1. [ **대상** ] 텍스트 상자에 파일 이름 `PreLoanProcess.war`**을 입력하고 WAR 파일 위치&#x200B;**를 지정한 다음 [마침]을 클릭합니다.

### AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버에 WAR 파일 배포 {#deploy-the-war-file-to-the-j2ee-application-server-hosting-aem-forms}

AEM Forms이 배포된 J2EE 응용 프로그램 서버에 WAR 파일을 배포합니다. WAR 파일을 J2EE 응용 프로그램 서버에 배포하려면 내보내기 경로에서 WAR 파일을 로 복사하십시오 `[AEM Forms Install]\Adobe\Adobe Experience Manager Forms\jboss\server\lc_turnkey\deploy`.

>[!NOTE]
>
>AEM Forms이 JBoss에 배포되지 않은 경우 AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버에 따라 WAR 파일을 배포해야 합니다.

### 웹 애플리케이션 테스트 {#test-your-web-application}

웹 애플리케이션을 배포한 후 웹 브라우저를 사용하여 테스트할 수 있습니다. AEM Forms을 호스팅하는 동일한 컴퓨터를 사용하고 있다고 가정할 경우 다음 URL을 지정할 수 있습니다.

* http://localhost:8080/PreLoanProcess/index.html

   HTML 양식 필드에 값을 입력하고 [응용 프로그램 제출] 단추를 클릭합니다. 문제가 발생하면 J2EE 응용 프로그램 서버의 로그 파일을 참조하십시오.

>[!NOTE]
>
>Java 응용 프로그램이 프로세스를 호출했는지 확인하려면 Workspace를 시작하고 대출을 수락합니다.

## 인간 중심의 오랜 프로세스를 호출하는 ASP.NET 웹 응용 프로그램 만들기 {#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process}

프로세스를 호출하는 ASP.NET 응용 프로그램을 만들 수 `FirstAppSolution/PreLoanProcess` 있습니다. ASP.NET 응용 프로그램에서 이 프로세스를 호출하려면 웹 서비스를 사용하십시오. (웹 서비스를 [사용하여 AEM Forms 호출을 참조하십시오](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)

다음 그림은 최종 사용자의 데이터를 가져오는 ASP.NET 클라이언트 응용 프로그램을 보여줍니다. 데이터는 XML 데이터 소스에 삽입되어 사용자가 [응용 프로그램 제출] 단추를 클릭하면 `FirstAppSolution/PreLoanProcess` 프로세스로 전송됩니다.

프로세스가 호출되면 호출 식별자 값이 표시됩니다. 호출 식별자 값은 긴 기간 프로세스의 상태를 추적하는 레코드의 일부로 만들어집니다.

ASP.NET 응용 프로그램은 다음 작업을 수행합니다.

* 사용자가 웹 페이지에 입력한 값을 검색합니다.
* * FirstAppSolution/PreLoanProcess *프로세스에 전달되는 XML 데이터 소스를 동적으로 생성합니다. 세 개의 값은 XML 데이터 소스에 지정됩니다.
* 웹 서비스를 사용하여* FirstAppSolution/PreLoanProcess *프로세스를 호출합니다.
* 호출 식별자 값 및 오래 지속된 작업의 상태를 클라이언트 웹 브라우저에 반환합니다.

### 단계 요약 {#summary_of_steps-1}

FirstAppSolution/PreLoanProcess 프로세스를 호출할 수 있는 ASP.NET 응용 프로그램을 만들려면 다음 단계를 수행하십시오.

1. [ASP.NET 웹 응용 프로그램을 만듭니다](invoking-human-centric-long-lived.md#create-an-asp-net-web-application).
1. [FirstAppSolution/PreLoanProcess를 호출하는 ASP 페이지를 만듭니다](invoking-human-centric-long-lived.md#create-an-asp-page-that-invokes-firstappsolution-preloanprocess).
1. [ASP.NET 응용 프로그램을 실행합니다](invoking-human-centric-long-lived.md#run-the-asp-net-application).

### ASP.NET 웹 응용 프로그램 만들기 {#create-an-asp-net-web-application}

Microsoft .NET C# ASP.NET 웹 응용 프로그램을 만듭니다. 다음 그림은 InvokePreLoanProcess라는 ASP.NET 프로젝트 *의 내용을 보여줍니다*.

서비스 참조 아래에 두 개의 항목이 있습니다. 첫 번째 항목의 이름은* JobManager*입니다. 이 참조를 사용하면 ASP.NET 응용 프로그램에서 작업 관리자 서비스를 호출할 수 있습니다. 이 서비스는 장기 프로세스 상태에 대한 정보를 반환합니다. 예를 들어 현재 프로세스가 실행 중인 경우 이 서비스는 현재 실행 중인 프로세스를 지정하는 숫자 값을 반환합니다. 두 번째 참조의 이름은&#x200B;*PreLoanProcess입니다*. 이 서비스 참조는* FirstAppSolution/PreLoanProcess *프로세스에 대한 참조를 나타냅니다. 서비스 참조를 만들면 AEM Forms 서비스와 관련된 데이터 유형을 .NET 프로젝트 내에서 사용할 수 있습니다.

**ASP.NET 프로젝트 만들기:**

1. Microsoft Visual Studio 2008을 시작합니다.
1. [ **파일** ] 메뉴에서 **새로**&#x200B;만들기, **웹 사이트**&#x200B;를선택합니다.
1. [ **템플릿** ] 목록에서 **ASP.NET 웹 사이트를 선택합니다**.
1. 위치 **상자에서** 프로젝트 위치를 선택합니다. 프로젝트의 이름을 InvokePreLoanProcess *로 지정합니다*.
1. 언어 **상자에서** Visual C#
1. 확인을 클릭합니다.

**서비스 참조 추가:**

1. 프로젝트 메뉴에서 서비스 참조 **추가를 선택합니다**.
1. 주소 **대화** 상자에서 작업 관리자 서비스에 대한 WSDL을 지정합니다.

   ```java
    https://hiro-xp:8080/soap/services/JobManager?WSDL&lc_version=9.0.1
   ```

1. 네임스페이스 필드에 입력합니다 `JobManager`.
1. **이동을**&#x200B;클릭한 다음 확인을 클릭합니다&#x200B;****.
1. [ **프로젝트** ] 메뉴에서 서비스 참조 **추가를 선택합니다**.
1. 주소 **대화** 상자에서 WSDL을 FirstAppSolution/PreLoanProcess 프로세스로 지정합니다.

   ```java
    https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?WSDL&lc_version=9.0.1
   ```

1. 네임스페이스 필드에 입력합니다 `PreLoanProcess`.
1. **이동을**&#x200B;클릭한 다음 확인을 클릭합니다&#x200B;****.

>[!NOTE]
>
>AEM Forms `hiro-xp` 를 호스팅하는 J2EE 응용 프로그램 서버의 IP 주소로 대체합니다. 이 `lc_version` 옵션은 MTOM과 같은 AEM Forms 기능을 사용할 수 있도록 합니다. 이 `lc_version`옵션을 지정하지 않으면 MTOM을 사용하여 AEM Forms을 호출할 수 없습니다. MTOM을 [사용하여 AEM Forms 호출을 참조하십시오](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom).

### FirstAppSolution/PreLoanProcess를 호출하는 ASP 페이지 만들기 {#create-an-asp-page-that-invokes-firstappsolution-preloanprocess}

ASP.NET 프로젝트 내에서 HTML 페이지를 대출 신청자에게 표시하는 책임이 있는 웹 양식(ASPX 파일)을 추가합니다. 웹 양식은 파생된 클래스를 기반으로 합니다 `System.Web.UI.Page`. 호출하는 C# 응용 프로그램 논리 `FirstAppSolution/PreLoanProcess` 는 `Button1_Click` 메서드에 있습니다(이 단추는 응용 프로그램 제출 단추를 나타냅니다).

다음 그림에서는 ASP.NET 응용 프로그램을 보여 줍니다

다음 표에는 이 ASP.NET 응용 프로그램에 포함된 컨트롤이 나열되어 있습니다.

<table>
 <thead>
  <tr>
   <th><p>컨트롤 이름</p></th>
   <th><p>설명</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>TextBoxName</p></td>
   <td><p>고객의 이름과 성을 지정합니다. </p></td>
  </tr>
  <tr>
   <td><p>TextBoxPhone</p></td>
   <td><p>고객의 전화 또는 이메일 주소를 지정합니다. </p></td>
  </tr>
  <tr>
   <td><p>TextBoxAmount</p></td>
   <td><p>대출 금액을 지정합니다.</p></td>
  </tr>
  <tr>
   <td><p>Button1</p></td>
   <td><p>응용 프로그램 제출 단추를 나타냅니다.</p></td>
  </tr>
  <tr>
   <td><p>LabelJobID</p></td>
   <td><p>호출 식별자 값의 값을 지정하는 Label 컨트롤입니다.</p></td>
  </tr>
  <tr>
   <td><p>LabelStatus</p></td>
   <td><p>작업 상태의 값을 지정하는 Label 컨트롤 이 값은 작업 관리자 서비스를 호출하여 검색됩니다. </p></td>
  </tr>
 </tbody>
</table>

ASP.NET 응용 프로그램의 일부인 응용 프로그램 논리는 프로세스에 전달할 XML 데이터 소스를 동적으로 만들어야 `FirstAppSolution/PreLoanProcess` 합니다. HTML 페이지에 입력한 값은 XML 데이터 소스 내에 지정해야 합니다. 이러한 데이터 값은 작업 공간에서 양식을 볼 때 폼으로 병합됩니다. 네임스페이스에 있는 클래스 `System.Xml` 는 XML 데이터 소스를 만드는 데 사용됩니다.

ASP.NET 응용 프로그램의 XML 데이터가 필요한 프로세스를 호출하면 XML 데이터 형식을 사용할 수 있습니다. 즉, 프로세스에 인스턴스를 전달할 수 `System.Xml.XmlDocument` 없습니다. 프로세스에 전달할 이 XML 인스턴스의 정규화된 이름은 입니다 `InvokePreLoanProcess.PreLoanProcess.XML`. 인스턴스를 `System.Xml.XmlDocument` 로 변환합니다 `InvokePreLoanProcess.PreLoanProcess.XML`. 다음 코드를 사용하여 이 작업을 수행할 수 있습니다.

```java
 //Create the XML to pass to the FirstAppSolution/PreLoanProcess process
 XmlDocument myXML = CreateXML(userName, phone, amount);
 
 //Convert the XML to a InvokePreLoanProcess.PreLoanProcess.XML instance
 StringWriter sw = new StringWriter();
 XmlTextWriter xw = new XmlTextWriter(sw);
 myXML.WriteTo(xw);
 
 InvokePreLoanProcess.PreLoanProcess.XML inXML = new XML();
 inXML.document = sw.ToString();
```

프로세스를 호출하는 ASP 페이지를 만들려면 `FirstAppSolution/PreLoanProcess` 메서드에서 다음 작업을 `Button1_Click` 수행하십시오.

1. 기본 생성자를 사용하여 `FirstAppSolution_PreLoanProcessClient` 개체를 만듭니다.
1. 생성자를 사용하여 `FirstAppSolution_PreLoanProcessClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스 및 인코딩 유형으로 전달합니다.

   ```java
    https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?blob=mtom
   ```

   속성을 사용할 필요는 `lc_version` 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다. 그러나 반드시 지정해야 합니다 `?blob=mtom`.

   >[!NOTE]
   >
   >AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버의 IP 주소 `hiro-xp`*로 바꿉니다. *

1. 데이터 `System.ServiceModel.BasicHttpBinding` 멤버의 값을 가져와 개체를 `FirstAppSolution_PreLoanProcessClient.Endpoint.Binding` 만듭니다. 반환 값을 다음으로 캐스팅합니다 `BasicHttpBinding`.
1. 개체의 `System.ServiceModel.BasicHttpBinding` 데이터 `MessageEncoding` 멤버를 로 설정합니다 `WSMessageEncoding.Mtom`. 이 값을 사용하면 MTOM이 사용됩니다.
1. 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

   * AEM 양식 사용자 이름을 데이터 멤버에 할당합니다 `FirstAppSolution_PreLoanProcessClient.ClientCredentials.UserName.UserName`.
   * 해당 암호 값을 데이터 멤버에 할당합니다 `FirstAppSolution_PreLoanProcessClient.ClientCredentials.UserName.Password`.
   * 데이터 멤버 `HttpClientCredentialType.Basic` 에 상수 값을 지정합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 데이터 멤버 `BasicHttpSecurityMode.TransportCredentialOnly` 에 상수 값을 지정합니다 `BasicHttpBindingSecurity.Security.Mode`.

   다음 코드 예는 이러한 작업을 보여줍니다.

   ```as3
    //Enable BASIC HTTP authentication
    BasicHttpBinding b = (BasicHttpBinding)mortgageClient.Endpoint.Binding;
    b.MessageEncoding = WSMessageEncoding.Mtom;
    mortgageClient.ClientCredentials.UserName.UserName = "administrator";
    mortgageClient.ClientCredentials.UserName.Password = "password";
    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
    b.MaxReceivedMessageSize = 2000000;
    b.MaxBufferSize = 2000000;
    b.ReaderQuotas.MaxArrayLength = 2000000;
   ```

1. 사용자가 웹 페이지에 입력한 이름, 전화 및 금액 값을 검색합니다. 이러한 값을 사용하여 프로세스에 전송되는 XML 데이터 소스를 동적으로 만들 수 `FirstAppSolution/PreLoanProcess` 있습니다. 프로세스에 전달할 XML 데이터 소스를 `System.Xml.XmlDocument` 나타내는 코드를 만듭니다(이 응용 프로그램 논리는 다음 코드 예제에서 표시됨).
1. 인스턴스를 변환할 `System.Xml.XmlDocument` 수 `InvokePreLoanProcess.PreLoanProcess.XML` 있습니다(이 애플리케이션 로직은 다음 코드 예제에서 표시됨).
1. 개체의 `FirstAppSolution/PreLoanProcess` 메서드를 호출하여 `FirstAppSolution_PreLoanProcessClient` 프로세스를 `invoke_Async` 호출합니다. 이 메서드는 긴 기간 프로세스의 호출 식별자 값을 나타내는 문자열 값을 반환합니다.
1. is 생성자를 사용하여 `JobManagerClient` 만듭니다. (작업 관리자 서비스에 대한 서비스 참조를 설정했는지 확인하십시오.)
1. 1-5단계를 반복합니다. 2단계에 대해 다음 URL을 지정합니다. `https://hiro-xp:8080/soap/services/JobManager?blob=mtom`.
1. 생성자를 사용하여 `JobId` 개체를 만듭니다.
1. 개체의 `JobId` 데이터 `id` 멤버를 `FirstAppSolution_PreLoanProcessClient` 개체 메서드의 반환 값으로 `invoke_Async` 설정합니다.
1. 객체의 데이터 멤버 `value` 에 true를 `JobId` 할당합니다 `persistent` .
1. 개체 `JobStatus` 의 메서드를 호출하고 `JobManagerService` `getStatus` `JobId` 개체를 전달하여 개체를 만듭니다.
1. 개체 데이터 멤버의 값을 검색하여 상태 값 `JobStatus` 을 `statusCode` 가져옵니다.
1. 필드에 호출 식별자 값을 `LabelJobID.Text` 지정합니다.
1. 필드에 상태 값을 `LabelStatus.Text` 지정합니다.

### 빠른 시작: 웹 서비스 API를 사용하여 긴 기간 프로세스 호출 {#quick-start-invoking-a-long-lived-process-using-the-web-service-api}

다음 C# 코드 예제에서는 `FirstAppSolution/PreLoanProcess`프로세스를 호출합니다.

```csharp
 ???/**
     * Ensure that you create a .NET project that uses
     * MS Visual Studio 2008 and version 3.5 of the .NET
     * framework. This is required to invoke a
     * AEM Forms service using MTOM.
 
 
 using System;
 using System.Collections;
 using System.Configuration;
 using System.Data;
 using System.Linq;
 using System.Web;
 using System.ServiceModel;
 using System.Web.Security;
 using System.Web.UI;
 using System.Web.UI.HtmlControls;
 using System.Web.UI.WebControls;
 using System.Web.UI.WebControls.WebParts;
 using System.Xml.Linq;
 using System.Xml;
 using System.IO;
 
 //A reference to FirstAppSolution/PreLoanProcess
 using InvokePreLoanProcess.PreLoanProcess;
 
 //A reference to JobManager service
 using InvokePreLoanProcess.JobManager;
 
 
 namespace InvokePreLoanProcess
 {
        public partial class _Default : System.Web.UI.Page
        {
            //This method is called when the Submit Application button is
            //Clicked
            protected void Button1_Click(object sender, EventArgs e)
            {
                //Create a FirstAppSolution_PreLoanProcessClient object
                FirstAppSolution_PreLoanProcessClient mortgageClient = new FirstAppSolution_PreLoanProcessClient();
                mortgageClient.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?blob=mtom");
 
                //Enable BASIC HTTP authentication
                BasicHttpBinding b = (BasicHttpBinding)mortgageClient.Endpoint.Binding;
                b.MessageEncoding = WSMessageEncoding.Mtom;
                mortgageClient.ClientCredentials.UserName.UserName = "administrator";
                mortgageClient.ClientCredentials.UserName.Password = "password";
                b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
                b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
                b.MaxReceivedMessageSize = 2000000;
                b.MaxBufferSize = 2000000;
                b.ReaderQuotas.MaxArrayLength = 2000000;
 
                //Retrieve values that user entered into the web page
                String userName = TextBoxName.Text;
                String phone = TextBoxPhone.Text;
                String amount = TextBoxAmount.Text;
 
                //Create the XML to pass to the FirstAppSolution/PreLoanProcess process
                XmlDocument myXML = CreateXML(userName, phone, amount);
 
                StringWriter sw = new StringWriter();
                XmlTextWriter xw = new XmlTextWriter(sw);
                myXML.WriteTo(xw);
 
                InvokePreLoanProcess.PreLoanProcess.XML inXML = new XML();
                inXML.document = sw.ToString();
 
                //INvoke the FirstAppSolution/PreLoanProcess process
                String invocationID =  mortgageClient.invoke_Async(inXML);
 
                //Create a JobManagerClient object to obtain the status of the long-lived operation
                JobManagerClient jobManager = new JobManagerClient();
                jobManager.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://hiro-xp:8080/soap/services/JobManager?blob=mtom");
 
                //Enable BASIC HTTP authentication
                BasicHttpBinding b1 = (BasicHttpBinding)jobManager.Endpoint.Binding;
                b1.MessageEncoding = WSMessageEncoding.Mtom;
                jobManager.ClientCredentials.UserName.UserName = "administrator";
                jobManager.ClientCredentials.UserName.Password = "password";
                b1.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
                b1.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
                b1.MaxReceivedMessageSize = 2000000;
                b1.MaxBufferSize = 2000000;
                b1.ReaderQuotas.MaxArrayLength = 2000000;
 
 
                //Create a JobID object that represents the status of the
                //long-lived operation
                JobId jobId = new JobId();
                jobId.id = invocationID;
                jobId.persistent = true;
                JobStatus jobStatus = jobManager.getStatus(jobId);
                System.Int16 val2 = jobStatus.statusCode;
                LabelJobID.Text = "The job status identifier value is " + invocationID;
                LabelStatus.Text = "The status of the long-lived operation is " + getJobDescription(val2);
 
            }
 
            private static XmlDocument CreateXML(String name, String phone, String amount)
            {
                //This method dynamically creates a DDX document
                //to pass to the FirstAppSolution/PreLoanProcess process
                XmlDocument xmlDoc = new XmlDocument();
 
                //Create the root element and append it to the XML DOM
                System.Xml.XmlElement root = xmlDoc.CreateElement("LoanApp");
                xmlDoc.AppendChild(root);
 
                //Create the Name element
                XmlElement nameElement = xmlDoc.CreateElement("Name");
                nameElement.AppendChild(xmlDoc.CreateTextNode(name));
                root.AppendChild(nameElement);
 
                //Create the LoanAmount element
                XmlElement LoanAmount = xmlDoc.CreateElement("LoanAmount");
                LoanAmount.AppendChild(xmlDoc.CreateTextNode(amount));
                root.AppendChild(LoanAmount);
 
                //Create the PhoneOrEmail element
                XmlElement PhoneOrEmail = xmlDoc.CreateElement("PhoneOrEmail");
                PhoneOrEmail.AppendChild(xmlDoc.CreateTextNode(phone));
                root.AppendChild(PhoneOrEmail);
 
                //Create the ApprovalStatus element
                XmlElement ApprovalStatus = xmlDoc.CreateElement("ApprovalStatus");
                ApprovalStatus.AppendChild(xmlDoc.CreateTextNode("PENDING APPROVAL"));
                root.AppendChild(ApprovalStatus);
 
                //Return the XmlElement instance
                return xmlDoc;
            }
 
 
            //Returns the String value of the Job Manager status code
            private String getJobDescription(int val)
            {
                switch(val)
                {
                    case 0:
                        return "JOB_STATUS_UNKNOWN";
 
                    case 1:
                        return "JOB_STATUS_QUEUED";
 
                    case 2:
                        return "JOB_STATUS_RUNNING";
 
                    case 3:
                        return "JOB_STATUS_COMPLETED";
 
                    case 4:
                        return "JOB_STATUS_FAILED";
 
                     case 5:
                        return "JOB_STATUS_COMPLETED";
 
                    case 6:
                        return "JOB_STATUS_SUSPENDED";
 
                    case 7:
                        return "JOB_STATUS_COMPLETE_REQUESTED";
 
                    case 8:
                        return "JOB_STATUS_TERMINATE_REQUESTED";
 
                     case 9:
                        return "JOB_STATUS_SUSPEND_REQUESTED";
 
                       case 10:
                        return "JOB_STATUS_RESUME_REQUESTED";
                }
 
                return "";
            }
       }
 }
 
```

>[!NOTE]
>
>getJobDescription 사용자 정의 메서드에 있는 값은 작업 관리자 서비스에서 반환한 값에 해당합니다.

### ASP.NET 응용 프로그램 실행 {#run-the-asp-net-application}

ASP.NET 응용 프로그램을 컴파일하고 배포한 후 웹 브라우저를 사용하여 실행할 수 있습니다. ASP.NET 프로젝트의 이름이 *InvokePreLoanProcess라고 가정할*&#x200B;경우 웹 브라우저 내에서 다음 URL을 지정합니다.

*http://localhost:1629/InvokePreLoanProcess/*Default.aspx

여기서 localhost는 ASP.NET 프로젝트를 호스팅하는 웹 서버의 이름이고 1629는 포트 번호입니다. ASP.NET 응용 프로그램을 컴파일하고 빌드하면 Microsoft Visual Studio가 이를 자동으로 배포합니다.

>[!NOTE]
>
>ASP.NET 응용 프로그램이 프로세스를 호출했는지 확인하려면 Workspace를 시작하고 대출을 수락합니다.

## 인간 중심의 오랜 프로세스를 불러일으키는 Flex를 사용하여 구축한 클라이언트 애플리케이션 제작 {#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process}

Flex로 제작한 클라이언트 애플리케이션을 제작하여 *FirstAppSolution/PreLoanProcess 프로세스를 호출할 수* 있습니다. 이 응용 프로그램은 Remoting을 사용하여 *FirstAppSolution/PreLoanProcess 프로세스를* 호출합니다. (AEM Forms [호출을 사용하여(AEM 양식에서 더 이상 사용되지 않음) AEM Forms Remoting을 참조하십시오](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

다음 그림은 최종 사용자의 데이터를 수집하는 Flex를 사용하여 구축한 클라이언트 애플리케이션을 보여줍니다. 데이터는 XML 데이터 소스에 삽입되어 프로세스로 전송됩니다.

프로세스가 호출되면 호출 식별자 값이 표시됩니다. 호출 식별자 값은 긴 기간 프로세스의 상태를 추적하는 레코드의 일부로 만들어집니다.

Flex로 구축한 클라이언트 애플리케이션은 다음 작업을 수행합니다.

* 사용자가 웹 페이지에 입력한 값을 검색합니다.
* FirstAppSolution/PreLoanProcess 프로세스에 전달되는 *XML 데이터 소스를 동적으로* 만듭니다. 세 개의 값은 XML 데이터 소스에 지정됩니다.
* Remoting을 사용하여 *FirstAppSolution/PreLoanProcess* 프로세스를 호출합니다.
* 긴 기간 프로세스의 호출 식별자 값을 반환합니다.

### 단계 요약 {#summary_of_steps-2}

FirstAppSolution/PreLoanProcess 프로세스를 호출할 수 있는 Flex를 사용하여 구축한 클라이언트 애플리케이션을 만들려면 다음 단계를 수행하십시오.

1. 새로운 Flex 프로젝트 시작
1. 프로젝트의 클래스 경로에 adobe-remoting-provider.swc 파일을 포함합니다. AEM Forms Flex [라이브러리 파일 포함을 참조하십시오](/help/forms/developing/invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file).
1. ActionScript 또는 MXML을 통해 `mx:RemoteObject` 인스턴스를 만듭니다. (mx: [RemoteObject 인스턴스 만들기 참조](/help/forms/developing/invoking-aem-forms-using-remoting.md))
1. AEM Forms과 통신하고 인스턴스에 연결할 인스턴스를 `ChannelSet` `mx:RemoteObject` 설정합니다. AEM Forms [에 채널 만들기를 참조하십시오](/help/forms/developing/invoking-aem-forms-using-remoting.md).
1. 사용자 식별자 값 및 암호를 지정하려면 ChannelSet의 `login` 메서드 또는 서비스 `setCredentials` 메서드를 호출합니다. (Single [Sign-On 사용을 참조하십시오](/help/forms/developing/invoking-aem-forms-using-remoting.md#using-single-sign-on).)
1. XML 인스턴스를 만들어 프로세스에 `FirstAppSolution/PreLoanProcess` 전달할 XML 데이터 소스를 만듭니다. 이 응용 프로그램 논리는 다음 코드 예제에서 볼 수 있습니다.
1. 생성자를 사용하여 Object 유형의 개체를 만듭니다. 다음 코드와 같이 프로세스의 입력 매개 변수의 이름을 지정하여 객체에 XML을 할당합니다.

   ```csharp
    //Get the XML data to pass to the AEM Forms process
    var xml:XML = createXML();
    var params:Object = new Object();
    params["formData"]=xml;
   ```

1. 인스턴스의 `FirstAppSolution/PreLoanProcess` 메서드를 호출하여 `mx:RemoteObject` 프로세스를 `invoke_Async` 호출합니다. 입력 매개 변수 `Object` 가 포함된 항목을 전달합니다. (입력 값 [전달을 참조하십시오](/help/forms/developing/invoking-aem-forms-using-remoting.md).)
1. 다음 코드와 같이 긴 기간 프로세스에서 반환되는 호출 식별 값을 검색합니다.

   ```csharp
    // Handles async call that invokes the long-lived process
    private function resultHandler(event:ResultEvent):void
    {
    ji = event.result as JobId;
    jobStatusDisplay.text = "Job Status ID: " + ji.jobId as String;
    }
   ```

### Remoting을 사용하여 오래 지속된 프로세스 호출 {#invoking-a-long-lived-process-using-remoting}

다음 Flex 코드 예제에서는 `FirstAppSolution/PreLoanProcess` 프로세스를 호출합니다.

```java
 <?xml version="1.0" encoding="utf-8"?>
 
 <mx:Application  xmlns="*" backgroundColor="#FFFFFF"
      creationComplete="initializeChannelSet();">
 
 <mx:Script>
          <![CDATA[
 
             import mx.controls.Alert;
             import mx.rpc.events.FaultEvent;
             import mx.rpc.events.ResultEvent;
             import flash.net.navigateToURL;
             import mx.messaging.ChannelSet;
             import mx.messaging.channels.AMFChannel;
             import mx.collections.ArrayCollection;
             import mx.rpc.livecycle.JobId;
             import mx.rpc.livecycle.JobStatus;
             import mx.rpc.livecycle.DocumentReference;
             import mx.formatters.NumberFormatter;
 
             // Holds the job ID returned by LC.JobManager
             private var ji:JobId;
 
             private function initializeChannelSet():void
              {
              var cs:ChannelSet= new ChannelSet();
         cs.addChannel(new AMFChannel("remoting-amf", "https://hiro-xp:8080/remoting/messagebroker/amf"));
         LC_MortgageApp.setCredentials("tblue", "password");
         LC_MortgageApp.channelSet = cs;
              }
 
            private function submitApplication():void
             {
             //Get the XML data to pass to the AEM Forms process
             var xml:XML = createXML();
             var params:Object = new Object();
             params["formData"]=xml;
             LC_MortgageApp.invoke_Async(params);
             }
 
             // Handles async call that invokes the long-lived process
             private function resultHandler(event:ResultEvent):void
             {
                ji = event.result as JobId;
                jobStatusDisplay.text = "Job Status ID: " + ji.jobId as String;
             }
 
             private function createXML():XML
             {
                //Calculate the Mortgage value to place in the XML data
                var propertyPrice:String = txtAmount.text ;
                var name:String = txtName.text ;
                var phone:String = txtPhone.text ;;
 
                var model:XML =
 
                  <LoanApp>
                           <Name>{name}</Name>
                           <LoanAmount>{propertyPrice}</LoanAmount>
                           <PhoneOrEmail>{phone}</PhoneOrEmail>
                           <ApprovalStatus>PENDING APPROVAL</ApprovalStatus>
                  </LoanApp>
 
              return model;
             }
 
 
          ]]>
       </mx:Script>
 
       <!-- Declare the RemoteObject and set its destination to the mortgage-app remoting endpoint defined in AEM Forms. -->
       <mx:RemoteObject id="LC_MortgageApp" destination="FirstAppSolution/PreLoanProcess" result="resultHandler(event);">
          <mx:method name="invoke_Async" result="resultHandler(event)"/>
      </mx:RemoteObject>
 
 
     <mx:Grid x="229" y="186">
         <mx:GridRow width="100%" height="100%">
             <mx:GridItem width="100%" height="100%">
                 <mx:Image>
                     <mx:source>file:///D|/LiveCycle_9/FirstApp/financeCorpLogo.jpg</mx:source>
                 </mx:Image>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:Label text="Flex Loan Application Page" fontSize="20"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
             </mx:GridItem>
         </mx:GridRow>
         <mx:GridRow width="100%" height="100%">
             <mx:GridItem width="100%" height="100%">
                 <mx:Label text="Name:" fontSize="12" fontWeight="bold"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:TextInput id="txtName"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:Button label="Submit Application" click="submitApplication()"/>
             </mx:GridItem>
         </mx:GridRow>
         <mx:GridRow width="100%" height="100%">
             <mx:GridItem width="100%" height="100%">
                 <mx:Label text="Phone/Email:" fontSize="12" fontWeight="bold"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:TextInput id="txtPhone"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
             </mx:GridItem>
         </mx:GridRow>
         <mx:GridRow width="100%" height="100%">
             <mx:GridItem width="100%" height="100%">
                 <mx:Label text="Amount:" fontSize="12" fontWeight="bold"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:TextInput id="txtAmount"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
             </mx:GridItem>
         </mx:GridRow>
         <mx:GridRow width="100%" height="100%">
             <mx:GridItem width="100%" height="100%">
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:Label text="Label" id="jobStatusDisplay" enabled="true" fontSize="12" fontWeight="bold"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
             </mx:GridItem>
         </mx:GridRow>
     </mx:Grid>
 
 </mx:Application>
 
```

