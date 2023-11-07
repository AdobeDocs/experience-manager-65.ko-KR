---
title: 인간 중심의 장기 프로세스 호출
seo-title: Invoking Human-Centric Long-Lived Processes
description: Invocation API를 사용하는 Java 웹 기반 클라이언트 응용 프로그램, 웹 서비스를 사용하는 ASP.NET 응용 프로그램 및 원격을 사용하는 Flex으로 빌드된 클라이언트 응용 프로그램을 사용하여 Workbench에서 생성된 인간 중심의 장기 프로세스를 프로그래밍 방식으로 호출합니다.
seo-description: Programmatically invoke human-centric long-lived processes created in Workbench using a Java web-based client application that uses the Invocation API, an ASP.NET application that uses web services, and a client application built with Flex that uses Remoting.
uuid: 42269d41-a90f-4ea1-aeb9-d61337bcfa54
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 18a320b4-dce6-4c50-8864-644b0b2d6644
role: Developer
exl-id: c9ebad8b-b631-492d-99a3-094e892b2ddb
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '3695'
ht-degree: 0%

---

# 인간 중심의 장기 프로세스 호출 {#invoking-human-centric-long-lived-processes}

다음 클라이언트 애플리케이션을 사용하여 Workbench에서 생성된 인간 중심의 장기 프로세스를 프로그래밍 방식으로 호출할 수 있습니다.

* 호출 API를 사용하는 Java 웹 기반 클라이언트 애플리케이션입니다. (참조: [Java API를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-java.md)(/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)
* 웹 서비스를 사용하는 ASP.NET 응용 프로그램입니다. (참조: [웹 서비스를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)
* 원격을 사용하는 Flex으로 구축된 클라이언트 애플리케이션입니다. (참조: [(AEM Forms에서 더 이상 사용되지 않는 기능)AEM Forms 원격을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

호출되는 장기 프로세스에는 이름이 지정됩니다 *FirstAppSolution/사전 대출 프로세스*. 에 지정된 자습서에 따라 이 프로세스를 만들 수 있습니다. [첫 번째 AEM Forms 애플리케이션 만들기](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63).

인간 중심 프로세스에는 사용자가 작업 영역을 사용하여 응답할 수 있는 작업이 포함됩니다. 예를 들어 Workbench를 사용하여 은행 관리자가 대출 신청을 승인하거나 거부할 수 있는 프로세스를 생성할 수 있습니다. 다음 그림은 프로세스를 보여 줍니다 *FirstAppSolution/사전 대출 프로세스*.

다음 *FirstAppSolution/사전 대출 프로세스* 프로세스는 라는 입력 매개변수를 수락합니다. *formData* 데이터 형식이 XML인 경우 XML 데이터는 이름이 인 양식 디자인과 병합됩니다. *PreLoanForm.xdp*. 다음 그림은 대출 신청을 승인하거나 거부하기 위해 사용자에게 할당된 작업을 나타내는 양식을 보여 줍니다. 사용자는 작업 영역을 사용하여 애플리케이션을 승인하거나 거부합니다. Workspace 사용자는 다음 그림에 표시된 승인 단추를 클릭하여 대출 요청을 승인할 수 있습니다. 마찬가지로 사용자는 거부 버튼을 클릭하여 대출 요청을 거부할 수 있습니다.

장기 프로세스는 비동기적으로 호출되며 다음 요인으로 인해 동기적으로 호출할 수 없습니다.

* 프로세스는 상당한 시간에 걸쳐 있을 수 있습니다.
* 프로세스는 조직의 경계를 포괄할 수 있습니다.
* 프로세스를 완료하려면 외부 입력이 필요합니다. 예를 들어 부재 중인 관리자에게 양식을 전송하는 상황을 생각해 보겠습니다. 이 경우 관리자가 돌아와서 양식을 작성할 때까지 프로세스가 완료되지 않습니다.

장기 프로세스가 호출되면 AEM Forms은 레코드 생성의 일부로 호출 식별자 값을 생성합니다. 레코드는 장기 프로세스 상태를 추적하고 AEM Forms 데이터베이스에 저장됩니다. 호출 식별자 값을 사용하여 장기 프로세스 상태를 추적할 수 있습니다. 또한 프로세스 호출 식별자 값을 사용하여 실행 중인 프로세스 인스턴스 종료와 같은 Process Manager 작업을 수행할 수 있습니다.

>[!NOTE]
>
>AEM Forms은 단기 프로세스가 호출될 때 호출 식별자 값 또는 레코드를 만들지 않습니다.

다음 `FirstAppSolution/PreLoanProcess` 프로세스는 지원자가 XML 데이터로 표현되는 지원서를 제출할 때 호출됩니다. 입력 프로세스 변수의 이름은 입니다. `formData` 데이터 형식은 XML입니다. 이 설명을 위해 다음 XML 데이터가 의 입력으로 사용된다고 가정해 보십시오. `FirstAppSolution/PreLoanProcess` 프로세스.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <LoanApp>
 <Name>Sam White</Name>
 <LoanAmount>250000</LoanAmount>
 <PhoneOrEmail>(555)555-5555</PhoneOrEmail>
 <ApprovalStatus>PENDING APPROVAL</ApprovalStatus>
 </LoanApp>
```

프로세스에 전달된 XML 데이터는 프로세스에 사용된 양식의 필드와 일치해야 합니다. 그렇지 않으면 양식 내에 데이터가 표시되지 않습니다. 를 호출하는 모든 응용 프로그램 `FirstAppSolution/PreLoanProcess` 프로세스는 이 XML 데이터 소스를 전달해야 합니다. 에서 생성된 애플리케이션 *인간 중심의 장기 프로세스 호출* 사용자가 웹 클라이언트에 입력한 값에서 XML 데이터 소스를 동적으로 만듭니다.

클라이언트 응용 프로그램을 사용하여 *FirstAppSolution/사전 대출 프로세스* 필요한 XML 데이터를 처리합니다. 장기 프로세스는 호출 식별자 값을 반환 값으로 반환합니다. 다음 그림은*FirstAppSolution/PreLoanProcess 장기 프로세스를 호출하는 클라이언트 응용 프로그램을 보여 줍니다. 클라이언트 애플리케이션은 XML 데이터를 전송하고 호출 식별자 값을 나타내는 문자열 값을 다시 가져옵니다.

**추가 참조**

[인간 중심의 장기 프로세스를 호출하는 Java 웹 애플리케이션 만들기](invoking-human-centric-long-lived.md#creating-a-java-web-application-that-invokes-a-human-centric-long-lived-process)

[인간 중심의 장기 프로세스를 호출하는 ASP.NET 웹 애플리케이션 만들기](invoking-human-centric-long-lived.md#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process)

[인간 중심의 장기 프로세스를 호출하는 Flex으로 구축된 클라이언트 애플리케이션 만들기](invoking-human-centric-long-lived.md#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process)

## 인간 중심의 장기 프로세스를 호출하는 Java 웹 애플리케이션 만들기 {#creating-a-java-web-application-that-invokes-a-human-centric-long-lived-process}

Java 서블릿을 사용하여 를 호출하는 웹 기반 애플리케이션을 만들 수 있습니다. `FirstAppSolution/PreLoanProcess` 프로세스. Java 서블릿에서 이 프로세스를 호출하려면 Java 서블릿 내의 호출 API를 사용합니다. (참조: [Java API를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api).)

다음 그림은 이름, 전화(또는 이메일) 및 금액 값을 게시하는 웹 기반 클라이언트 응용 프로그램을 보여 줍니다. 이러한 값은 사용자가 애플리케이션 제출 버튼을 클릭하면 Java 서블릿으로 전송됩니다.

Java 서블릿은 다음 작업을 수행합니다.

* HTML 페이지에서 Java 서블릿에 게시된 값을 검색합니다.
* 에 전달할 XML 데이터 소스를 동적으로 만듭니다. *FirstAppSolution/사전 대출 프로세스* 프로세스. 이름, 전화(또는 이메일) 및 금액 값은 XML 데이터 소스에 지정됩니다.
* 호출 *FirstAppSolution/사전 대출 프로세스* AEM Forms 호출 API를 사용하여 프로세스를 수행합니다.
* 호출 식별자 값을 클라이언트 웹 브라우저에 반환합니다.

### 단계 요약 {#summary-of-steps}

를 호출하는 Java 웹 기반 응용 프로그램을 만들려면 `FirstAppSolution/PreLoanProcess` 프로세스를 진행하려면 다음 단계를 수행하십시오.

1. [웹 프로젝트 만들기](invoking-human-centric-long-lived.md#create-a-web-project).
1. [서블릿에 대한 Java 애플리케이션 논리 생성](invoking-human-centric-long-lived.md#create-java-application-logic-for-the-servlet).
1. [웹 응용 프로그램의 웹 페이지를 만듭니다.](invoking-human-centric-long-lived.md#create-the-web-page-for-the-web-application)
1. [웹 응용 프로그램을 WAR 파일에 패키징](invoking-human-centric-long-lived.md#package-the-web-application-to-a-war-file).
1. [AEM Forms을 호스팅하는 J2EE 애플리케이션 서버에 WAR 파일 배포](invoking-human-centric-long-lived.md#deploy-the-war-file-to-the-j2ee-application-server-hosting-aem-forms).
1. [웹 애플리케이션 테스트](invoking-human-centric-long-lived.md#test-your-web-application).

>[!NOTE]
>
>이러한 단계 중 일부는 AEM Forms이 배포되는 J2EE 애플리케이션에 따라 다릅니다. 예를 들어 WAR 파일을 배포하는 데 사용하는 방법은 사용 중인 J2EE 응용 프로그램 서버에 따라 다릅니다. AEM Forms이 JBoss®에 배포되어 있다고 가정합니다.

### 웹 프로젝트 만들기 {#create-a-web-project}

웹 응용 프로그램을 만드는 첫 번째 단계는 웹 프로젝트를 만드는 것입니다. 이 문서가 기반으로 하는 Java IDE는 Eclipse 3.3입니다. Eclipse IDE를 사용하여 웹 프로젝트를 만들고 필요한 JAR 파일을 프로젝트에 추가합니다. 다음 이름의 HTML 페이지 추가 *index.html*  프로젝트에 Java 서블릿을 추가합니다.

다음 목록은 웹 프로젝트에 포함할 JAR 파일을 지정합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* J2EE.jar

이러한 JAR 파일의 위치는 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

>[!NOTE]
>
>J2EE.jar 파일은 Java 서블릿에 사용되는 데이터 유형을 정의합니다. 이 JAR 파일은 AEM Forms이 배포된 J2EE 애플리케이션 서버에서 가져올 수 있습니다.

**웹 프로젝트 만들기**

1. Eclipse를 시작하고 **파일** >  **새 프로젝트**.
1. 다음에서 **새 프로젝트** 대화 상자에서 **웹** > **동적 웹 프로젝트**.
1. 유형 `InvokePreLoanProcess` 을(를) 클릭하여 프로젝트의 이름을 확인한 다음 **완료**.

**프로젝트에 필수 JAR 파일 추가**

1. 프로젝트 탐색기 창에서 마우스 오른쪽 단추 클릭 `InvokePreLoanProcess` 프로젝트 및 선택 **속성**.
1. 클릭 **Java 빌드 경로** 을(를) 클릭하고 **라이브러리** 탭.
1. 다음을 클릭합니다. **외부 JAR 추가** 버튼을 클릭하고 포함할 JAR 파일을 찾습니다.

**프로젝트에 Java 서블릿 추가**

1. 프로젝트 탐색기 창에서 마우스 오른쪽 단추 클릭 `InvokePreLoanProcess` 프로젝트 및 선택 **신규** >  **기타**.
1. 확장 **웹** 폴더, 선택 **서블릿**&#x200B;을 클릭한 다음 을 클릭합니다 **다음**.
1. Create Servlet 대화 상자에서 `SubmitXML` 서블릿 이름을 보려면 을(를) 클릭하십시오. **완료**.

**프로젝트에 HTML 페이지 추가**

1. 프로젝트 탐색기 창에서 마우스 오른쪽 단추 클릭 `InvokePreLoanProcess` 프로젝트 및 선택 **신규** > **기타**.
1. 확장 **웹** 폴더, 선택 **HTML**, 및 클릭 **다음**.
1. 새 HTML 대화 상자에서 `index.html` 파일 이름을 지정한 다음 **완료**.

>[!NOTE]
>
>SubmitXML Java 서블릿을 호출하는 HTML 컨텐츠 생성에 대한 내용은 다음을 참조하십시오. [웹 응용 프로그램의 웹 페이지를 만듭니다.](invoking-human-centric-long-lived.md#create-the-web-page-for-the-web-application).

### 서블릿에 대한 Java 애플리케이션 논리 생성 {#create-java-application-logic-for-the-servlet}

를 호출하는 Java 애플리케이션 논리 생성 `FirstAppSolution/PreLoanProcess` java 서블릿 내에서 를 처리합니다. 다음 코드는 의 구문을 보여줍니다. `SubmitXML` Java 서블릿:

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

일반적으로 Java 서블릿 내에 클라이언트 코드를 배치하지는 않습니다. `doGet` 또는 `doPost` 메서드를 사용합니다. 더 나은 프로그래밍 방법은 이 코드를 별도의 클래스 내에 배치하는 것입니다. 그런 다음 내에서 클래스를 인스턴스화합니다 `doPost` 방법(또는 `doGet` 메서드)를 클릭하고 적절한 메서드를 호출하십시오. 그러나 코드 간결성을 위해 코드 예제는 최소한으로 유지되며 `doPost` 메서드를 사용합니다.

를 호출하려면 `FirstAppSolution/PreLoanProcess` 호출 API를 사용하는 프로세스를 처리하고 다음 작업을 수행합니다.

1. Java 프로젝트의 클래스 경로에 adobe-livecycle-client.jar과 같은 클라이언트 JAR 파일을 포함합니다. 이러한 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).
1. HTML 페이지에서 제출된 이름, 전화 번호 및 금액 값을 검색합니다. 이 값을 사용하여 로 전송되는 XML 데이터 소스를 동적으로 만듭니다. `FirstAppSolution/PreLoanProcess` 프로세스. 다음을 사용할 수 있습니다. `org.w3c.dom` 클래스를 사용하여 XML 데이터 소스를 만들 수 있습니다. 이 응용 프로그램 논리는 다음 코드 예제에 나와 있습니다.
1. 만들기 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다. (참조: [연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
1. 만들기 `ServiceClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체. A `ServiceClient` 개체를 사용하면 서비스 작업을 호출할 수 있습니다. 호출 요청 찾기, 발송 및 라우팅 등의 작업을 처리합니다.
1. 만들기 `java.util.HashMap` 개체를 만들 때 사용됩니다.
1. 호출 `java.util.HashMap` 개체 `put` 각 입력 매개 변수에 대한 메서드를 long-lived 프로세스에 전달합니다. 프로세스의 입력 매개 변수 이름을 지정해야 합니다. 이유: `FirstAppSolution/PreLoanProcess` 프로세스에는 유형의 입력 매개 변수가 한 개 필요합니다. `XML` (명명된) `formData`)를 호출하기만 하면 됩니다. `put` 메서드를 한 번 호출합니다.

   ```java
    //Get the XML to pass to the FirstAppSolution/PreLoanProcess process
    org.w3c.dom.Document inXML = GetDataSource(name,phone,amount);
    
    //Create a Map object to store the parameter value
    Map params = new HashMap();
    params.put("formData", inXML);
   ```

1. 만들기 `InvocationRequest` 를 호출하여 개체 `ServiceClientFactory` 개체 `createInvocationRequest` 메서드 및 다음 값 전달:

   * 호출할 장기 프로세스의 이름을 지정하는 문자열 값입니다. 를 호출하려면 `FirstAppSolution/PreLoanProcess` 프로세스, 지정 `FirstAppSolution/PreLoanProcess`.
   * 프로세스 작업 이름을 나타내는 문자열 값입니다. 오래 지속되는 프로세스 작업의 이름은 입니다. `invoke`.
   * 다음 `java.util.HashMap` 서비스 작업에 필요한 매개 변수 값을 포함하는 개체입니다.
   * 을 지정하는 부울 값 `false`비동기 요청을 생성합니다(이 값은 수명이 긴 프로세스를 호출하는 데 적용 가능).

   >[!NOTE]
   >
   >*createInvocationRequest 메서드의 네 번째 매개 변수로 true 값을 전달하여 단기 프로세스를 호출할 수 있습니다. true 값을 전달하면 동기 요청이 만들어집니다.*

1. 다음을 호출하여 호출 요청을 AEM Forms에 보내기 `ServiceClient` 개체 `invoke` 메서드 및 전달 `InvocationRequest` 개체. 다음 `invoke` 메서드가 다음을 반환합니다. `InvocationReponse` 개체.
1. 장기 프로세스는 호출 식별 값을 나타내는 문자열 값을 반환합니다. 다음을 호출하여 이 값 검색 `InvocationReponse` 개체 `getInvocationId` 메서드를 사용합니다.

   ```java
    //Send the invocation request to the long-lived process and
    //get back an invocation response object
    InvocationResponse lcResponse = myServiceClient.invoke(lcRequest);
    String invocationId = lcResponse.getInvocationId();
   ```

1. 클라이언트 웹 브라우저에 호출 ID 값을 씁니다. 다음을 사용할 수 있습니다. `java.io.PrintWriter` 클라이언트 웹 브라우저에 이 값을 쓸 인스턴스입니다.

### 빠른 시작: 호출 API를 사용하여 장기 프로세스 호출 {#quick-start-invoking-a-long-lived-process-using-the-invocation-api}

다음 Java 코드 예는 를 호출하는 Java 서블릿을 나타냅니다. `FirstAppSolution/PreLoanProcess` 프로세스.

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
     * These JAR files are in the following path:
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
 
                 //Create a Document object
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

### 웹 응용 프로그램의 웹 페이지를 만듭니다. {#create-the-web-page-for-the-web-application}

다음 *index.html* 웹 페이지는 을 호출하는 Java 서블릿에 대한 진입점을 제공합니다. `FirstAppSolution/PreLoanProcess` 프로세스. 이 웹 페이지는 HTML 양식과 제출 단추를 포함하는 기본 HTML 양식입니다. 사용자가 제출 단추를 클릭하면 양식 데이터가 `SubmitXML` Java 서블릿.

Java 서블릿은 다음 Java 코드를 사용하여 HTML 페이지에서 게시된 데이터를 캡처합니다.

```java
 //Get the values that are passed from the Loan HTML page
 String name = request.getParameter("name");
 String phone = request.getParameter("phone");
 String amount = request.getParameter("amount");
```

다음 HTML 코드는 개발 환경을 설정하는 동안 생성된 index.html 파일을 나타냅니다. (참조: [웹 프로젝트 만들기](invoking-human-centric-long-lived.md#create-a-web-project).)

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

### 웹 응용 프로그램을 WAR 파일에 패키징 {#package-the-web-application-to-a-war-file}

를 호출하는 Java 서블릿을 배포하려면 `FirstAppSolution/PreLoanProcess` 웹 응용 프로그램을 WAR 파일로 패키지합니다. adobe-livecycle-client.jar 및 adobe-usermanager-client.jar와 같이 구성 요소의 비즈니스 논리가 종속되는 외부 JAR 파일도 WAR 파일에 포함되어야 합니다.

다음 그림은 WAR 파일로 패키지된 Eclipse 프로젝트의 콘텐츠를 보여줍니다.

>[!NOTE]
>
>이전 그림에서 JPG 파일은 모든 JPG 이미지 파일로 대체할 수 있습니다.

**웹 응용 프로그램을 WAR 파일로 패키지합니다.**

1. 다음에서 **프로젝트 탐색기** 창에서 마우스 오른쪽 단추 클릭 `InvokePreLoanProcess` 프로젝트 및 선택 **내보내기** > **WAR 파일**.
1. 다음에서 **웹 모듈** 텍스트 상자, 문자 `InvokePreLoanProcess` Java 프로젝트의 이름입니다.
1. 다음에서 **대상** 텍스트 상자, 문자 `PreLoanProcess.war`**대상:**&#x200B;파일 이름을 지정하고 WAR 파일의 위치를 지정한 다음 [마침]을 클릭합니다.

### AEM Forms을 호스팅하는 J2EE 애플리케이션 서버에 WAR 파일 배포 {#deploy-the-war-file-to-the-j2ee-application-server-hosting-aem-forms}

AEM Forms이 배포되는 J2EE 응용 프로그램 서버에 WAR 파일을 배포합니다. WAR 파일을 J2EE 응용 프로그램 서버에 배포하려면 내보내기 경로에서 WAR 파일을 `[AEM Forms Install]\Adobe\Adobe Experience Manager Forms\jboss\server\lc_turnkey\deploy`.

>[!NOTE]
>
>AEM Forms이 JBoss에 배포되지 않은 경우 AEM Forms을 호스팅하는 J2EE 애플리케이션 서버를 준수하여 WAR 파일을 배포해야 합니다.

### 웹 애플리케이션 테스트 {#test-your-web-application}

웹 응용 프로그램을 배포한 후 웹 브라우저를 사용하여 테스트할 수 있습니다. AEM Forms을 호스팅하는 동일한 컴퓨터를 사용하고 있다고 가정할 경우 다음 URL을 지정할 수 있습니다.

* http://localhost:8080/PreLoanProcess/index.html

  HTML 양식 필드에 값을 입력하고 애플리케이션 제출 버튼을 클릭합니다. 문제가 발생하면 J2EE 애플리케이션 서버의 로그 파일을 참조하십시오.

>[!NOTE]
>
>Java 애플리케이션이 프로세스를 호출했는지 확인하려면 Workspace를 시작하고 대출을 수락합니다.

## 인간 중심의 장기 프로세스를 호출하는 ASP.NET 웹 애플리케이션 만들기 {#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process}

다음을 호출하는 ASP.NET 응용 프로그램을 만들 수 있습니다. `FirstAppSolution/PreLoanProcess` 프로세스. ASP.NET 응용 프로그램에서 이 프로세스를 호출하려면 웹 서비스를 사용합니다. (참조: [웹 서비스를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)

다음 그림은 최종 사용자로부터 데이터를 가져오는 ASP.NET 클라이언트 응용 프로그램을 보여줍니다. 데이터는 XML 데이터 소스에 배치되어 `FirstAppSolution/PreLoanProcess` 사용자가 [애플리케이션 제출] 단추를 클릭할 때 진행됩니다.

프로세스가 호출되면 호출 식별자 값이 표시됩니다. 호출 식별자 값은 수명이 긴 프로세스의 상태를 추적하는 레코드의 일부로 만들어집니다.

ASP.NET 응용 프로그램은 다음 작업을 수행합니다.

* 사용자가 웹 페이지에 입력한 값을 검색합니다.
* FirstAppSolution/PreLoanProcess *프로세스에 전달되는 XML 데이터 소스를 동적으로 만듭니다. 세 값은 XML 데이터 소스에 지정됩니다.
* 웹 서비스를 사용하여* FirstAppSolution/PreLoanProcess *프로세스를 호출합니다.
* 호출 식별자 값과 장기 작동 상태를 클라이언트 웹 브라우저에 반환합니다.

### 단계 요약 {#summary_of_steps-1}

FirstAppSolution/PreLoanProcess 프로세스를 호출할 수 있는 ASP.NET 응용 프로그램을 만들려면 다음 단계를 수행합니다.

1. [ASP.NET 웹 응용 프로그램 만들기](invoking-human-centric-long-lived.md#create-an-asp-net-web-application).
1. [FirstAppSolution/PreLoanProcess를 호출하는 ASP 페이지를 만듭니다.](invoking-human-centric-long-lived.md#create-an-asp-page-that-invokes-firstappsolution-preloanprocess).
1. [ASP.NET 응용 프로그램 실행](invoking-human-centric-long-lived.md#run-the-asp-net-application).

### ASP.NET 웹 응용 프로그램 만들기 {#create-an-asp-net-web-application}

Microsoft .NET C# ASP.NET 웹 응용 프로그램을 만듭니다. 다음 그림은 ASP.NET 프로젝트의 컨텐츠를 보여줍니다. *InvokePreLoanProcess*.

서비스 참조 아래에는 두 가지 항목이 있습니다. 첫 번째 항목의 이름은* JobManager*입니다. 이 참조를 사용하면 ASP.NET 응용 프로그램에서 작업 관리자 서비스를 호출할 수 있습니다. 이 서비스는 장기 프로세스 상태에 대한 정보를 반환합니다. 예를 들어 프로세스가 현재 실행 중인 경우 이 서비스는 프로세스가 현재 실행 중임을 지정하는 숫자 값을 반환합니다. 두 번째 참조는 이름이 로 지정됩니다.*PreLoanProcess*. 이 서비스 참조는* FirstAppSolution/PreLoanProcess *프로세스에 대한 참조를 나타냅니다. 서비스 참조를 만든 후에는 .NET 프로젝트 내에서 AEM Forms 서비스와 연결된 데이터 형식을 사용할 수 있습니다.

**ASP.NET 프로젝트를 만듭니다.**

1. Microsoft Visual Studio 2008을 시작합니다.
1. 다음에서 **파일** 메뉴, 선택 **신규**, **웹 사이트**.
1. 다음에서 **템플릿** 목록, 선택 **ASP.NET 웹 사이트**.
1. 다음에서 **위치** 상자에서 프로젝트의 위치를 선택합니다. 프로젝트 이름 지정 *InvokePreLoanProcess*.
1. 다음에서 **언어** 상자에서 Visual C#
1. 확인을 클릭합니다.

**서비스 참조 추가:**

1. 프로젝트 메뉴에서 **서비스 참조 추가**.
1. 다음에서 **주소** 대화 상자에서 작업 관리자 서비스에 WSDL을 지정합니다.

   ```java
    https://hiro-xp:8080/soap/services/JobManager?WSDL&lc_version=9.0.1
   ```

1. 네임스페이스 필드에 `JobManager`.
1. 클릭 **이동**&#x200B;그런 다음 을 클릭합니다.**확인**.
1. 다음에서 **프로젝트** 메뉴, 선택 **서비스 참조 추가**.
1. 다음에서 **주소** 대화 상자에서 FirstAppSolution/PreLoanProcess 프로세스에 WSDL을 지정합니다.

   ```java
    https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?WSDL&lc_version=9.0.1
   ```

1. 네임스페이스 필드에 `PreLoanProcess`.
1. 클릭 **이동**&#x200B;그런 다음 을 클릭합니다.**확인**.

>[!NOTE]
>
>바꾸기 `hiro-xp` AEM Forms을 호스팅하는 J2EE 애플리케이션 서버의 IP 주소입니다. 다음 `lc_version` 옵션을 사용하면 MTOM과 같은 AEM Forms 기능을 사용할 수 있습니다. 을 지정하지 않고 `lc_version`옵션을 선택하면 MTOM을 사용하여 AEM Forms을 호출할 수 없습니다. (참조: [MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom).)

### FirstAppSolution/PreLoanProcess를 호출하는 ASP 페이지를 만듭니다. {#create-an-asp-page-that-invokes-firstappsolution-preloanprocess}

ASP.NET 프로젝트 내에서 대출 신청자에게 HTML 페이지 표시를 담당하는 웹 양식(ASPX 파일)을 추가합니다. 웹 폼은 `System.Web.UI.Page`. 를 호출하는 C# 응용 프로그램 논리 `FirstAppSolution/PreLoanProcess` 다음에 있음 `Button1_Click` 메서드(이 단추는 [애플리케이션 제출] 단추를 나타냅니다.)

다음 그림은 ASP.NET 응용 프로그램을 보여 줍니다

다음 표에는 이 ASP.NET 응용 프로그램의 일부인 컨트롤이 나열되어 있습니다.

<table>
 <thead>
  <tr>
   <th><p>컨트롤 이름</p></th>
   <th><p>설명</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>텍스트 상자 이름</p></td>
   <td><p>고객의 이름과 성을 지정합니다. </p></td>
  </tr>
  <tr>
   <td><p>TextBoxPhone</p></td>
   <td><p>고객의 전화 또는 이메일 주소를 지정합니다. </p></td>
  </tr>
  <tr>
   <td><p>텍스트 상자 금액</p></td>
   <td><p>대출 금액을 지정합니다.</p></td>
  </tr>
  <tr>
   <td><p>Button1</p></td>
   <td><p>[애플리케이션 제출] 단추를 나타냅니다.</p></td>
  </tr>
  <tr>
   <td><p>레이블 작업 ID</p></td>
   <td><p>호출 식별자 값의 값을 지정하는 Label 컨트롤입니다.</p></td>
  </tr>
  <tr>
   <td><p>레이블 상태</p></td>
   <td><p>작업 상태의 값을 지정하는 Label 컨트롤입니다. 이 값은 작업 관리자 서비스를 호출하여 검색됩니다. </p></td>
  </tr>
 </tbody>
</table>

ASP.NET 응용 프로그램의 일부인 응용 프로그램 논리는에 전달할 XML 데이터 소스를 동적으로 만들어야 합니다. `FirstAppSolution/PreLoanProcess` 프로세스. 지원자가 HTML 페이지에 입력한 값은 XML 데이터 소스 내에 지정해야 합니다. 이러한 데이터 값은 Workspace에서 양식을 볼 때 양식에 병합됩니다. 의 클래스 `System.Xml` 네임스페이스는 XML 데이터 소스를 만드는 데 사용됩니다.

ASP.NET 응용 프로그램에서 XML 데이터가 필요한 프로세스를 호출할 때 사용할 수 있는 XML 데이터 형식을 사용할 수 있습니다. 즉, 를 전달할 수 없습니다. `System.Xml.XmlDocument` 인스턴스를 프로세스에 추가합니다. 프로세스에 전달할 이 XML 인스턴스의 정규화된 이름은 입니다. `InvokePreLoanProcess.PreLoanProcess.XML`. 변환 `System.Xml.XmlDocument` 인스턴스 대상 `InvokePreLoanProcess.PreLoanProcess.XML`. 다음 코드를 사용하여 이 작업을 수행할 수 있습니다.

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

를 호출하는 ASP 페이지를 만들려면 `FirstAppSolution/PreLoanProcess` 을(를) 처리하고 `Button1_Click` 방법:

1. 만들기 `FirstAppSolution_PreLoanProcessClient` 기본 생성자를 사용하여 개체를 작성합니다.
1. 만들기 `FirstAppSolution_PreLoanProcessClient.Endpoint.Address` 을 사용하여 개체 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스 및 인코딩 형식에 전달합니다.

   ```java
    https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?blob=mtom
   ```

   를 사용할 필요가 없습니다. `lc_version` 특성. 이 속성은 서비스 참조를 만들 때 사용됩니다. 그러나 다음을 지정해야 합니다 `?blob=mtom`.

   >[!NOTE]
   >
   >바꾸기 `hiro-xp`* AEM Forms을 호스팅하는 J2EE 애플리케이션 서버의 IP 주소입니다. *

1. 만들기 `System.ServiceModel.BasicHttpBinding` 의 값을 가져와서 개체 `FirstAppSolution_PreLoanProcessClient.Endpoint.Binding` 데이터 구성원입니다. 반환 값을 다음으로 캐스트 `BasicHttpBinding`.
1. 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 데이터 멤버 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
1. 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

   * 데이터 멤버에 AEM Forms 사용자 이름 할당 `FirstAppSolution_PreLoanProcessClient.ClientCredentials.UserName.UserName`.
   * 해당 암호 값을 데이터 멤버에 할당 `FirstAppSolution_PreLoanProcessClient.ClientCredentials.UserName.Password`.
   * 상수 값 지정 `HttpClientCredentialType.Basic` 데이터 멤버에게 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 상수 값 지정 `BasicHttpSecurityMode.TransportCredentialOnly` 데이터 멤버에게 `BasicHttpBindingSecurity.Security.Mode`.

   다음 코드 예제에서는 이러한 작업을 보여 줍니다.

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

1. 사용자가 웹 페이지에 입력한 이름, 전화 번호 및 금액 값을 검색합니다. 이 값을 사용하여 로 전송되는 XML 데이터 소스를 동적으로 만듭니다. `FirstAppSolution/PreLoanProcess` 프로세스. 만들기 `System.Xml.XmlDocument` 프로세스에 전달할 XML 데이터 소스를 나타냅니다(이 응용 프로그램 로직은 다음 코드 예에 표시됨).
1. 변환 `System.Xml.XmlDocument` 인스턴스 대상 `InvokePreLoanProcess.PreLoanProcess.XML` (이 응용 프로그램 로직은 다음 코드 예제에 나와 있습니다.)
1. 호출 `FirstAppSolution/PreLoanProcess` 를 호출하여 프로세스를 `FirstAppSolution_PreLoanProcessClient` 개체 `invoke_Async` 메서드를 사용합니다. 이 메서드는 장기 프로세스의 호출 식별자 값을 나타내는 문자열 값을 반환합니다.
1. 만들기 `JobManagerClient` 를 사용하여 는 생성자입니다. (Job Manager 서비스에 대한 서비스 참조를 설정했는지 확인하십시오.)
1. 1~5단계를 반복합니다. 2단계에 대해 다음 URL을 지정하십시오. `https://hiro-xp:8080/soap/services/JobManager?blob=mtom`.
1. 만들기 `JobId` 개체를 만들 때 사용됩니다.
1. 설정 `JobId` 개체 `id` 반환 값이 인 데이터 멤버 `FirstAppSolution_PreLoanProcessClient` 개체 `invoke_Async` 메서드를 사용합니다.
1. 할당 `value` true to the `JobId` 개체 `persistent` 데이터 구성원입니다.
1. 만들기 `JobStatus` 를 호출하여 개체 `JobManagerService` 의 오브젝트 `getStatus` 메서드 및 전달 `JobId` 개체.
1. 의 값을 검색하여 상태 값 가져오기 `JobStatus` 개체 `statusCode` 데이터 구성원입니다.
1. 호출 식별자 값을 `LabelJobID.Text` 필드.
1. 에 상태 값 할당 `LabelStatus.Text` 필드.

### 빠른 시작: 웹 서비스 API를 사용하여 오래 지속되는 프로세스 호출 {#quick-start-invoking-a-long-lived-process-using-the-web-service-api}

다음 C# 코드 예제에서는 `FirstAppSolution/PreLoanProcess`프로세스.

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
>getJobDescription 사용자 정의 메소드의 값은 Job Manager 서비스에서 반환한 값에 해당합니다.

### ASP.NET 응용 프로그램 실행 {#run-the-asp-net-application}

ASP.NET 응용 프로그램을 컴파일하고 배포한 후 웹 브라우저를 사용하여 실행할 수 있습니다. ASP.NET 프로젝트의 이름을 다음과 같이 가정합니다. *InvokePreLoanProcess*&#x200B;웹 브라우저 내에서 다음 URL을 지정합니다.

*http://localhost:1629/InvokePreLoanProcess/*Default.aspx

여기서 localhost는 ASP.NET 프로젝트를 호스팅하는 웹 서버의 이름이고 1629는 포트 번호입니다. ASP.NET 응용 프로그램을 컴파일하고 빌드하면 Microsoft Visual Studio가 자동으로 배포합니다.

>[!NOTE]
>
>ASP.NET 응용 프로그램이 프로세스를 호출했는지 확인하려면 Workspace를 시작하고 대출을 수락합니다.

## 인간 중심의 장기 프로세스를 호출하는 Flex으로 구축된 클라이언트 애플리케이션 만들기 {#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process}

Flex으로 빌드된 클라이언트 응용 프로그램을 만들어 를 호출할 수 있습니다. *FirstAppSolution/사전 대출 프로세스* 프로세스. 이 응용 프로그램은 원격을 사용하여 *FirstAppSolution/사전 대출 프로세스* 프로세스. (참조: [(AEM Forms에서 더 이상 사용되지 않는 기능)AEM Forms 원격을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

다음 그림은 Flex으로 구축된 클라이언트 애플리케이션이 최종 사용자로부터 데이터를 수집하는 모습을 보여줍니다. 데이터는 XML 데이터 소스에 배치되어 프로세스로 전송됩니다.

프로세스가 호출되면 호출 식별자 값이 표시됩니다. 호출 식별자 값은 수명이 긴 프로세스의 상태를 추적하는 레코드의 일부로 만들어집니다.

Flex으로 구축된 클라이언트 애플리케이션은 다음 작업을 수행합니다.

* 사용자가 웹 페이지에 입력한 값을 검색합니다.
* 에 전달되는 XML 데이터 소스를 동적으로 만듭니다. *FirstAppSolution/사전 대출 프로세스* 프로세스. 세 값은 XML 데이터 소스에 지정됩니다.
* 호출 *FirstAppSolution/사전 대출 프로세스* remoting을 사용하여 처리합니다.
* 장기 프로세스의 호출 식별자 값을 반환합니다.

### 단계 요약 {#summary_of_steps-2}

FirstAppSolution/PreLoanProcess 프로세스를 호출할 수 있는 Flex으로 빌드된 클라이언트 응용 프로그램을 만들려면 다음 단계를 수행합니다.

1. 새 Flex 프로젝트를 시작합니다.
1. 프로젝트의 클래스 경로에 adobe-remoting-provider.swc 파일을 포함합니다. (참조: [AEM Forms Flex 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file).)
1. 만들기 `mx:RemoteObject` ActionScript 또는 MXML을 통한 인스턴스. (참조: [mx:RemoteObject 인스턴스 만들기](/help/forms/developing/invoking-aem-forms-using-remoting.md))
1. 설정 `ChannelSet` AEM Forms과 통신하고 인스턴스와 연결할 수 있습니다. `mx:RemoteObject` 인스턴스. (참조: [AEM Forms 채널 만들기](/help/forms/developing/invoking-aem-forms-using-remoting.md).)
1. ChannelSet 호출 `login` 서비스 방법 `setCredentials` 사용자 식별자 값 및 암호를 지정하는 방법. (참조: [SSO(Single Sign-On) 사용](/help/forms/developing/invoking-aem-forms-using-remoting.md#using-single-sign-on).)
1. 에 전달할 XML 데이터 소스를 만듭니다. `FirstAppSolution/PreLoanProcess` xml 인스턴스를 생성하여 프로세스를 수행합니다. (이 응용 프로그램 논리는 다음 코드 예제에 나와 있습니다.)
1. Object 형식의 개체를 해당 생성자를 사용하여 만듭니다. 다음 코드와 같이 프로세스의 입력 매개 변수 이름을 지정하여 객체에 XML을 지정합니다.

   ```csharp
    //Get the XML data to pass to the AEM Forms process
    var xml:XML = createXML();
    var params:Object = new Object();
    params["formData"]=xml;
   ```

1. 호출 `FirstAppSolution/PreLoanProcess` 를 호출하여 처리 `mx:RemoteObject` 인스턴스 `invoke_Async` 메서드를 사용합니다. 전달 `Object` 에 입력 매개 변수가 포함되어 있습니다. (참조: [입력 값 전달](/help/forms/developing/invoking-aem-forms-using-remoting.md).)
1. 다음 코드와 같이 장기 프로세스에서 반환되는 호출 ID 값을 검색합니다.

   ```csharp
    // Handles async call that invokes the long-lived process
    private function resultHandler(event:ResultEvent):void
    {
    ji = event.result as JobId;
    jobStatusDisplay.text = "Job Status ID: " + ji.jobId as String;
    }
   ```

### Remoting을 사용하여 오래 지속되는 프로세스 호출 {#invoking-a-long-lived-process-using-remoting}

다음 Flex 코드 예제에서는 `FirstAppSolution/PreLoanProcess` 프로세스.

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
