---
title: 동적으로 DDX 문서 만들기
description: Java API 및 웹 서비스 API를 사용하여 동적으로 DDX 문서를 만듭니다. 동적으로 DDX 문서를 만들면 런타임 중에 얻은 DDX 문서의 값을 사용할 수 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: b3c19c82-e26f-4dc8-b846-6aec705cee08
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2153'
ht-degree: 0%

---

# 동적으로 DDX 문서 만들기 {#dynamically-creating-ddx-documents}

**이 문서의 샘플과 예제는 JEE 환경의 AEM Forms에 대해서만 적용됩니다.**

어셈블러 작업을 수행하는 데 사용할 수 있는 DDX 문서를 동적으로 만들 수 있습니다. 동적으로 DDX 문서를 만들면 런타임 중에 얻은 DDX 문서의 값을 사용할 수 있습니다. DDX 문서를 동적으로 만들려면 사용 중인 프로그래밍 언어에 속하는 클래스를 사용합니다. 예를 들어 Java를 사용하여 클라이언트 응용 프로그램을 개발하는 경우 `org.w3c.dom.*` 패키지에 속하는 클래스를 사용합니다. 마찬가지로 Microsoft .NET을 사용하는 경우 `System.Xml` 네임스페이스에 속하는 클래스를 사용합니다.

DDX 문서를 어셈블러 서비스에 전달하려면 먼저 XML을 `org.w3c.dom.Document` 인스턴스에서 `com.adobe.idp.Document` 인스턴스로 변환합니다. 웹 서비스를 사용하는 경우 XML을 만드는 데 사용되는 데이터 형식(예: `XmlDocument`)에서 `BLOB` 인스턴스로 XML을 변환합니다.

여기서는 다음 DDX 문서가 동적으로 만들어진다고 가정해 보겠습니다.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

이 DDX 문서는 PDF 문서를 디스어셈블합니다. PDF 문서 분해에 익숙해지는 것이 좋습니다.

>[!NOTE]
>
>어셈블러 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

>[!NOTE]
>
>DDX 문서에 대한 자세한 내용은 [어셈블러 서비스 및 DDX 참조](https://www.adobe.com/go/learn_aemforms_ddx_63)를 참조하십시오.

## 단계 요약 {#summary-of-steps}

동적으로 생성된 DDX 문서를 사용하여 PDF 문서를 분해하려면 다음 작업을 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. PDF 어셈블러 클라이언트를 만듭니다.
1. DDX 문서를 만듭니다.
1. DDX 문서를 변환합니다.
1. 런타임 옵션을 설정합니다.
1. PDF 문서를 디스어셈블합니다.
1. 분해된 PDF 문서를 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필수)

**PDF 어셈블러 클라이언트 만들기**

어셈블러 작업을 프로그래밍 방식으로 수행하려면 먼저 어셈블러 서비스 클라이언트를 만듭니다.

**DDX 문서 만들기**

사용 중인 프로그래밍 언어를 사용하여 DDX 문서를 만듭니다. PDF 문서를 디스어셈블하는 DDX 문서를 만들려면 `PDFsFromBookmarks` 요소가 포함되어 있는지 확인하십시오. Java API를 사용하는 경우 DDX 문서를 만드는 데 사용되는 데이터 형식을 `com.adobe.idp.Document` 인스턴스로 변환합니다. 웹 서비스를 사용하는 경우 데이터 형식을 `BLOB` 인스턴스로 변환합니다.

**DDX 문서 변환**

`org.w3c.dom` 클래스를 사용하여 만든 DDX 문서는 `com.adobe.idp.Document` 개체로 변환해야 합니다. Java API를 사용할 때 이 작업을 수행하려면 Java XML 변환 클래스를 사용합니다. 웹 서비스를 사용하는 경우 DDX 문서를 `BLOB` 개체로 변환하십시오.

**디스어셈블할 PDF 문서 참조**

PDF 문서를 디스어셈블하려면 디스어셈블할 PDF 문서를 나타내는 PDF 파일을 참조합니다. 어셈블러 서비스로 전달되면 문서의 레벨 1 책갈피마다 별도의 PDF 문서가 반환됩니다.

**런타임 옵션 설정**

작업을 수행하는 동안 어셈블러 서비스의 동작을 제어하는 런타임 옵션을 설정할 수 있습니다. 예를 들어 오류가 발생하는 경우 어셈블러 서비스에서 작업 처리를 계속하도록 지시하는 옵션을 설정할 수 있습니다. 런타임 옵션을 설정하려면 `AssemblerOptionSpec` 개체를 사용합니다.

**PDF 문서를 디스어셈블합니다**

`invokeDDX` 작업을 호출하여 PDF 문서를 디스어셈블합니다. 동적으로 생성된 DDX 문서를 전달합니다. 어셈블러 서비스는 컬렉션 개체 내에서 분해된 PDF 문서를 반환합니다.

**분해된 PDF 문서를 저장합니다**

분해된 모든 PDF 문서는 컬렉션 개체 내에서 반환됩니다. 컬렉션 객체를 반복하고 각 PDF 문서를 PDF 파일로 저장합니다.

**추가 참조**

[Java API를 사용하여 동적으로 DDX 문서 만들기](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[웹 서비스 API를 사용하여 동적으로 DDX 문서 만들기](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[프로그래밍 방식으로 PDF 문서 디스어셈블](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Java API를 사용하여 동적으로 DDX 문서 만들기 {#dynamically-create-a-ddx-document-using-the-java-api}

어셈블러 서비스 API(Java)를 사용하여 동적으로 DDX 문서를 만들고 PDF 문서를 디스어셈블합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-assembler-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. PDF 어셈블러 클라이언트를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하고 `ServiceClientFactory` 개체를 전달하여 `AssemblerServiceClient` 개체를 만듭니다.

1. DDX 문서를 만듭니다.

   * `DocumentBuilderFactory` 클래스의 `newInstance` 메서드를 호출하여 Java `DocumentBuilderFactory` 개체를 만듭니다.
   * `DocumentBuilderFactory` 개체의 `newDocumentBuilder` 메서드를 호출하여 Java `DocumentBuilder` 개체를 만듭니다.
   * `org.w3c.dom.Document` 개체를 인스턴스화하려면 `DocumentBuilder` 개체의 `newDocument` 메서드를 호출하십시오.
   * `org.w3c.dom.Document` 개체의 `createElement` 메서드를 호출하여 DDX 문서의 루트 요소를 만듭니다. 이 메서드는 루트 요소를 나타내는 `Element` 개체를 만듭니다. 요소의 이름을 나타내는 문자열 값을 `createElement` 메서드에 전달합니다. 반환 값을 `Element`(으)로 캐스팅합니다. 그런 다음 `setAttribute` 메서드를 호출하여 자식 요소의 값을 설정하십시오. 마지막으로, 헤더 요소의 `appendChild` 메서드를 호출하여 요소를 헤더 요소에 추가하고 자식 요소 개체를 인수로 전달합니다. 다음 코드 행은 이 응용 프로그램 논리를 보여 줍니다.
     ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * `Document` 개체의 `createElement` 메서드를 호출하여 `PDFsFromBookmarks` 요소를 만듭니다. 요소의 이름을 나타내는 문자열 값을 `createElement` 메서드에 전달합니다. 반환 값을 `Element`(으)로 캐스팅합니다. `setAttribute` 메서드를 호출하여 `PDFsFromBookmarks` 요소의 값을 설정하십시오. DDX 요소의 `appendChild` 메서드를 호출하여 `PDFsFromBookmarks` 요소를 `DDX` 요소에 추가하십시오. `PDFsFromBookmarks` 요소 개체를 인수로 전달합니다. 다음 코드 행은 이 응용 프로그램 논리를 보여 줍니다.

     ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * `Document` 개체의 `createElement` 메서드를 호출하여 `PDF` 요소를 만듭니다. 요소의 이름을 나타내는 문자열 값을 전달합니다. 반환 값을 `Element`(으)로 캐스팅합니다. `setAttribute` 메서드를 호출하여 `PDF` 요소의 값을 설정하십시오. `PDFsFromBookmarks` 요소의 `appendChild` 메서드를 호출하여 `PDF` 요소를 `PDFsFromBookmarks` 요소에 추가하십시오. `PDF` 요소 개체를 인수로 전달합니다. 다음 코드 행은 이 애플리케이션 논리를 보여 줍니다.

     ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. DDX 문서를 변환합니다.

   * `javax.xml.transform.Transformer` 개체의 정적 `newInstance` 메서드를 호출하여 `javax.xml.transform.Transformer` 개체를 만듭니다.
   * `TransformerFactory` 개체의 `newTransformer` 메서드를 호출하여 `Transformer` 개체를 만듭니다.
   * 해당 생성자를 사용하여 `ByteArrayOutputStream` 개체를 만듭니다.
   * 해당 생성자를 사용하여 `javax.xml.transform.dom.DOMSource` 개체를 만듭니다. DDX 문서를 나타내는 `org.w3c.dom.Document` 개체를 전달합니다.
   * 생성자를 사용하고 `ByteArrayOutputStream` 개체를 전달하여 `javax.xml.transform.dom.DOMSource` 개체를 만듭니다.
   * `javax.xml.transform.Transformer` 개체의 `transform` 메서드를 호출하여 Java `ByteArrayOutputStream` 개체를 채웁니다. `javax.xml.transform.dom.DOMSource` 및 `javax.xml.transform.stream.StreamResult` 개체를 전달합니다.
   * 바이트 배열을 만들고 `ByteArrayOutputStream` 개체의 크기를 바이트 배열에 할당합니다.
   * `ByteArrayOutputStream` 개체의 `toByteArray` 메서드를 호출하여 바이트 배열을 채웁니다.
   * 해당 생성자를 사용하고 바이트 배열을 전달하여 `com.adobe.idp.Document` 개체를 만듭니다.

1. 분해하려면 PDF 문서를 참조합니다.

   * `HashMap` 생성자를 사용하여 입력 PDF 문서를 저장하는 데 사용되는 `java.util.Map` 개체를 만듭니다.
   * 생성자를 사용하고 디스어셈블할 PDF 문서의 위치를 전달하여 `java.io.FileInputStream` 개체를 만듭니다.
   * `com.adobe.idp.Document` 개체를 만듭니다. 디스어셈블할 PDF 문서가 포함된 `java.io.FileInputStream` 개체를 전달합니다.
   * `put` 메서드를 호출하고 다음 인수를 전달하여 `java.util.Map` 개체에 항목을 추가합니다.

      * 키 이름을 나타내는 문자열 값입니다. 이 값은 DDX 문서에 지정된 PDF 원본 요소의 값과 일치해야 합니다. 동적으로 만들어진 DDX 문서에서 값은 `AssemblerResultPDF.pdf`입니다.
      * 디스어셈블할 PDF 문서가 포함된 `com.adobe.idp.Document` 개체입니다.

1. 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 런타임 옵션을 저장하는 `AssemblerOptionSpec` 개체를 만듭니다.
   * `AssemblerOptionSpec` 개체에 속하는 메서드를 호출하여 비즈니스 요구 사항을 충족하도록 런타임 옵션을 설정하십시오. 예를 들어 오류가 발생할 때 어셈블러 서비스에서 작업 처리를 계속하도록 하려면 `AssemblerOptionSpec` 개체의 `setFailOnError` 메서드를 호출하고 `false`을(를) 전달합니다.

1. PDF 문서를 디스어셈블합니다.

   `AssemblerServiceClient` 개체의 `invokeDDX` 메서드를 호출하고 다음 값을 전달하십시오.

   * 동적으로 생성된 DDX 문서를 나타내는 `com.adobe.idp.Document` 개체입니다.
   * 디스어셈블할 PDF 문서가 포함된 `java.util.Map` 개체
   * 기본 글꼴 및 작업 로그 수준을 포함하여 런타임 옵션을 지정하는 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 개체입니다.

   `invokeDDX` 메서드가 분해된 PDF 문서와 발생한 모든 예외를 포함하는 `com.adobe.livecycle.assembler.client.AssemblerResult` 개체를 반환합니다.

1. 분해된 PDF 문서를 저장합니다.

   분해된 PDF 문서를 가져오려면 다음 작업을 수행합니다.

   * `AssemblerResult` 개체의 `getDocuments` 메서드를 호출합니다. 이 메서드는 `java.util.Map` 개체를 반환합니다.
   * 결과 `com.adobe.idp.Document` 개체가 발견될 때까지 `java.util.Map` 개체를 반복합니다.
   * `com.adobe.idp.Document` 개체의 `copyToFile` 메서드를 호출하여 PDF 문서를 추출하십시오.

**추가 참조**

[빠른 시작(SOAP 모드): Java API를 사용하여 동적으로 DDX 문서 만들기](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API를 사용하여 동적으로 DDX 문서 만들기 {#dynamically-create-a-ddx-document-using-the-web-service-api}

어셈블러 서비스 API(웹 서비스)를 사용하여 동적으로 DDX 문서를 만들고 PDF 문서를 디스어셈블합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 서비스 참조를 설정할 때 다음 WSDL 정의를 사용하는지 확인하십시오. `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꾸십시오.

1. PDF 어셈블러 클라이언트를 만듭니다.

   * 기본 생성자를 사용하여 `AssemblerServiceClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `AssemblerServiceClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). `lc_version` 특성은 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.
   * `AssemblerServiceClient.Endpoint.Binding` 필드의 값을 가져와 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`(으)로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * `AssemblerServiceClient.ClientCredentials.UserName.UserName` 필드에 AEM Forms 사용자 이름을 지정하십시오.
      * 필드 `AssemblerServiceClient.ClientCredentials.UserName.Password`에 해당 암호 값을 지정하십시오.
      * 상수 값 `HttpClientCredentialType.Basic`을(를) 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.
      * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을(를) 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. DDX 문서를 만듭니다.

   * 해당 생성자를 사용하여 `System.Xml.XmlElement` 개체를 만듭니다.
   * `XmlElement` 개체의 `CreateElement` 메서드를 호출하여 DDX 문서의 루트 요소를 만듭니다. 이 메서드는 루트 요소를 나타내는 `Element` 개체를 만듭니다. 요소의 이름을 나타내는 문자열 값을 `CreateElement` 메서드에 전달합니다. `SetAttribute` 메서드를 호출하여 DDX 요소의 값을 설정하십시오. 마지막으로 `XmlElement` 개체의 `AppendChild` 메서드를 호출하여 요소를 DDX 문서에 추가합니다. DDX 개체를 인수로 전달합니다. 다음 코드 행은 이 응용 프로그램 논리를 보여 줍니다.

     ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * `XmlElement` 개체의 `CreateElement` 메서드를 호출하여 DDX 문서의 `PDFsFromBookmarks` 요소를 만듭니다. 요소의 이름을 나타내는 문자열 값을 `CreateElement` 메서드에 전달합니다. 그런 다음 해당 `SetAttribute` 메서드를 호출하여 요소의 값을 설정하십시오. `DDX` 요소의 `AppendChild` 메서드를 호출하여 `PDFsFromBookmarks` 요소를 루트 요소에 추가합니다. `PDFsFromBookmarks` 요소 개체를 인수로 전달합니다. 다음 코드 행은 이 응용 프로그램 논리를 보여 줍니다.

     ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * `XmlElement` 개체의 `CreateElement` 메서드를 호출하여 DDX 문서의 `PDF` 요소를 만듭니다. 요소의 이름을 나타내는 문자열 값을 `CreateElement` 메서드에 전달합니다. 그런 다음 `SetAttribute` 메서드를 호출하여 자식 요소의 값을 설정하십시오. `PDFsFromBookmarks` 요소의 `AppendChild` 메서드를 호출하여 `PDF` 요소를 `PDFsFromBookmarks` 요소에 추가하십시오. `PDF` 요소 개체를 인수로 전달합니다. 다음 코드 행은 이 애플리케이션 논리를 보여 줍니다.

     ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. DDX 문서를 변환합니다.

   * 해당 생성자를 사용하여 `System.IO.MemoryStream` 개체를 만듭니다.
   * DDX 문서를 나타내는 `XmlElement` 개체를 사용하여 `MemoryStream` 개체를 DDX 문서로 채웁니다. `XmlElement` 개체의 `Save` 메서드를 호출하고 `MemoryStream` 개체를 전달하십시오.
   * 바이트 배열을 만들어 `MemoryStream` 개체의 데이터로 채웁니다. 다음 코드는 이 애플리케이션 논리를 보여 줍니다.

     ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * `BLOB` 개체를 만듭니다. 바이트 배열을 `BLOB` 개체의 `MTOM` 필드에 할당합니다.

1. 분해하려면 PDF 문서를 참조합니다.

   * 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 입력 PDF 문서를 저장하는 데 사용됩니다. 이 `BLOB` 개체는 `invokeOneDocument`에 인수로 전달됩니다.
   * 해당 생성자를 호출하여 `System.IO.FileStream` 개체를 만듭니다. 입력 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * 해당 `MTOM` 속성을 바이트 배열의 내용으로 할당하여 `BLOB` 개체를 채웁니다.

1. 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 런타임 옵션을 저장하는 `AssemblerOptionSpec` 개체를 만듭니다.
   * `AssemblerOptionSpec` 개체에 속하는 데이터 멤버에 값을 할당하여 비즈니스 요구 사항에 맞게 런타임 옵션을 설정하십시오. 예를 들어 오류가 발생할 때 어셈블러 서비스에서 작업 처리를 계속하도록 하려면 `AssemblerOptionSpec` 개체의 `failOnError` 데이터 멤버에 `false`을(를) 할당합니다.

1. PDF 문서를 디스어셈블합니다.

   `AssemblerServiceClient` 개체의 `invokeDDX` 메서드를 호출하고 다음 값을 전달하십시오.

   * 동적으로 생성된 DDX 문서를 나타내는 `BLOB` 개체입니다.
   * 입력 PDF 문서를 포함하는 `mapItem` 배열
   * 런타임 옵션을 지정하는 `AssemblerOptionSpec` 개체

   `invokeDDX` 메서드가 작업 결과와 발생한 모든 예외를 포함하는 `AssemblerResult` 개체를 반환합니다.

1. 분해된 PDF 문서를 저장합니다.

   새로 생성된 PDF 문서를 가져오려면 다음 작업을 수행합니다.

   * 분해된 PDF 문서가 포함된 `Map` 개체인 `AssemblerResult` 개체의 `documents` 필드에 액세스합니다.
   * `Map` 개체를 반복하여 각 결과 문서를 가져옵니다. 그런 다음 해당 배열 멤버의 `value`을(를) `BLOB`(으)로 캐스팅합니다.
   * `BLOB` 개체의 `MTOM` 속성에 액세스하여 PDF 문서를 나타내는 이진 데이터를 추출합니다. PDF 파일에 쓸 수 있는 바이트 배열이 반환됩니다.

**추가 참조**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
