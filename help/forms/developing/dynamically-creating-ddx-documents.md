---
title: 동적으로 DCX 문서 만들기
seo-title: 동적으로 DCX 문서 만들기
description: 'null'
seo-description: 'null'
uuid: b73e8069-6c9f-4517-a0ae-f3d503191d2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2ad227de-68a8-446f-8c4f-a33a6f95bec8
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 동적으로 DCX 문서 만들기 {#dynamically-creating-ddx-documents}

어셈블러 작업을 수행하는 데 사용할 수 있는 DCX 문서를 동적으로 만들 수 있습니다. DCX 문서를 동적으로 만들면 런타임 동안 얻어진 DCX 문서의 값을 사용할 수 있습니다. DCX 문서를 동적으로 만들려면 사용 중인 프로그래밍 언어에 속하는 클래스를 사용합니다. 예를 들어 Java를 사용하여 클라이언트 애플리케이션을 개발하는 경우 `org.w3c.dom.*`패키지에 속한 클래스를 사용합니다. 마찬가지로 Microsoft .NET을 사용하는 경우 `System.Xml` 네임스페이스에 속하는 클래스를 사용합니다.

DDX 문서를 어셈블러 서비스로 전달하려면 먼저 XML을 `org.w3c.dom.Document` 인스턴스에서 `com.adobe.idp.Document` 인스턴스로 변환합니다. 웹 서비스를 사용하는 경우 XML(예: XML)을 만드는 데 사용되는 데이터 유형에서 `XmlDocument`인스턴스로 XML을 `BLOB` 변환합니다.

이 토론의 경우 다음 DCX 문서가 동적으로 작성되었다고 가정합니다.

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

이 DCX 문서는 PDF 문서를 분해합니다. PDF 문서 분리에 익숙해지는 것이 좋습니다.

>[!NOTE]
>
>어셈블러 서비스에 대한 자세한 내용은 AEM Forms [에 대한 서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDX 문서에 대한 자세한 내용은 어셈블러 서비스 [및 DCX 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 단계 요약 {#summary-of-steps}

동적으로 생성된 DCX 문서를 사용하여 PDF 문서를 분해하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일 포함
1. PDF Assembler 클라이언트 만들기
1. DCX 문서를 만듭니다.
1. DCX 문서를 변환합니다.
1. 런타임 옵션을 설정합니다.
1. PDF 문서를 분해합니다.
1. 분해된 PDF 문서를 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

다음 JAR 파일을 프로젝트의 클래스 경로에 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (AEM Forms가 JBoss에 배포된 경우 필요)
* jbossall-client.jar(JBoss에 AEM Forms가 배포된 경우 필요)

**PDF 어셈블러 클라이언트 만들기**

어셈블리 작업을 프로그래밍 방식으로 수행하려면 먼저 어셈블러 서비스 클라이언트를 만듭니다.

**DCX 문서 만들기**

사용 중인 프로그래밍 언어를 사용하여 DCX 문서를 만듭니다. PDF 문서를 분해하는 DCX 문서를 만들려면 `PDFsFromBookmarks` 요소에 요소가 포함되어 있는지 확인합니다. Java API를 사용하는 경우 DCX 문서를 만드는 데 사용되는 데이터 유형을 `com.adobe.idp.Document` 인스턴스로 변환합니다. 웹 서비스를 사용하는 경우 데이터 유형을 `BLOB` 인스턴스로 변환합니다.

**DCX 문서 변환**

클래스를 사용하여 만든 DCX 문서는 `org.w3c.dom` 개체로 변환되어야 합니다 `com.adobe.idp.Document` . Java API를 사용할 때 이 작업을 수행하려면 Java XML 변형 클래스를 사용합니다. 웹 서비스를 사용하는 경우 DCX 문서를 `BLOB` 개체로 변환합니다.

**분해할 PDF 문서 참조**

PDF 문서를 분해하려면 분해할 PDF 문서를 나타내는 PDF 파일을 참조하십시오. 어셈블러 서비스에 전달되면 문서의 각 수준 1 책갈피에 대해 별도의 PDF 문서가 반환됩니다.

**런타임 옵션 설정**

작업을 수행하는 동안 어셈블러 서비스의 동작을 제어하는 런타임 옵션을 설정할 수 있습니다. 예를 들어 오류가 발생하면 어셈블리 서비스에서 작업을 계속 처리하도록 하는 옵션을 설정할 수 있습니다. 런타임 옵션을 설정하려면 `AssemblerOptionSpec` 개체를 사용합니다.

**PDF 문서 분해**

작업을 호출하여 PDF 문서를 `invokeDDX` 분해합니다. 동적으로 생성된 DCX 문서를 전달합니다. 어셈블러 서비스는 컬렉션 개체 내에서 분해된 PDF 문서를 반환합니다.

**분해된 PDF 문서 저장**

분해된 모든 PDF 문서는 컬렉션 개체 내에서 반환됩니다. 컬렉션 개체를 반복하고 각 PDF 문서를 PDF 파일로 저장할 수 있습니다.

**참고 항목**

[Java API를 사용하여 DCX 문서를 동적으로 만들기](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[웹 서비스 API를 사용하여 DCX 문서를 동적으로 만들기](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[프로그래밍 방식으로 PDF 문서 분리](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Java API를 사용하여 DCX 문서를 동적으로 만들기 {#dynamically-create-a-ddx-document-using-the-java-api}

Assembler Service API(Java)를 사용하여 DCX 문서를 동적으로 만들고 PDF 문서를 분해합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-assembler-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. PDF Assembler 클라이언트 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 객체를 전달하여 `AssemblerServiceClient` 객체를 만듭니다 `ServiceClientFactory` .

1. DCX 문서를 만듭니다.

   * 클래스의 `DocumentBuilderFactory` `DocumentBuilderFactory` `newInstance` 메서드를 호출하여 Java 개체를 만듭니다.
   * 개체의 `DocumentBuilder` `DocumentBuilderFactory` `newDocumentBuilder` 메서드를 호출하여 Java 개체를 만듭니다.
   * 객체의 메서드를 호출하여 `DocumentBuilder` `newDocument` `org.w3c.dom.Document` 객체를 인스턴스화합니다.
   * 개체의 `org.w3c.dom.Document` `createElement` 메서드를 호출하여 DCX 문서의 루트 요소를 만듭니다. 이 메서드는 루트 요소를 나타내는 `Element` 객체를 만듭니다. 요소의 이름을 나타내는 문자열 값을 `createElement` 메서드에 전달합니다. 반환 값을 로 `Element`캐스팅합니다. 그런 다음 자식 요소의 `setAttribute` 메서드를 호출하여 값을 설정합니다. 마지막으로 헤더 요소의 메서드를 호출하여 요소를 헤더 요소에 추가하고 자식 요소 개체를 인수로 전달합니다. `appendChild` 다음 코드 줄은 이 응용 프로그램 논리를 보여 줍니다.
      ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * 개체의 `PDFsFromBookmarks` `Document` `createElement` 메서드를 호출하여 요소를 만듭니다. 요소의 이름을 나타내는 문자열 값을 `createElement` 메서드에 전달합니다. 반환 값을 로 `Element`캐스팅합니다. 해당 `PDFsFromBookmarks` `setAttribute` 메서드를 호출하여 요소의 값을 설정합니다. DCX 요소의 `PDFsFromBookmarks` 메서드를 호출하여 요소를 `DDX` 요소에 추가합니다 `appendChild` . 요소 객체를 인수로 `PDFsFromBookmarks` 전달합니다. 다음 코드 줄은 이 응용 프로그램 논리를 보여 줍니다.

      ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * 개체의 `PDF` `Document` `createElement` 메서드를 호출하여 요소를 만듭니다. 요소의 이름을 나타내는 문자열 값을 전달합니다. 반환 값을 로 `Element`캐스팅합니다. 해당 `PDF` `setAttribute` 메서드를 호출하여 요소의 값을 설정합니다. 요소의 `PDF` `PDFsFromBookmarks` `PDFsFromBookmarks` `appendChild` 메서드를 호출하여 요소를 요소에 추가합니다. 요소 객체를 인수로 `PDF` 전달합니다. 다음 코드 줄은 이 응용 프로그램 논리를 보여줍니다.

      ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. DCX 문서를 변환합니다.

   * 개체의 정적 `javax.xml.transform.Transformer` `javax.xml.transform.Transformer` `newInstance` 메서드를 호출하여 개체를 만듭니다.
   * 개체의 `Transformer` `TransformerFactory` `newTransformer` 메서드를 호출하여 개체를 만듭니다.
   * 생성자를 사용하여 `ByteArrayOutputStream` 객체를 만듭니다.
   * 생성자를 사용하여 `javax.xml.transform.dom.DOMSource` 객체를 만듭니다. DCX 문서를 나타내는 `org.w3c.dom.Document` 객체를 전달합니다.
   * 생성자를 사용하여 객체를 전달하여 `javax.xml.transform.dom.DOMSource` 객체를 만듭니다 `ByteArrayOutputStream` .
   * 객체의 `ByteArrayOutputStream` `javax.xml.transform.Transformer` `transform` 메서드를 호출하여 Java 객체를 채웁니다. 및 `javax.xml.transform.dom.DOMSource` 개체를 `javax.xml.transform.stream.StreamResult` 전달합니다.
   * 바이트 배열을 만들고 `ByteArrayOutputStream` 개체의 크기를 바이트 배열에 할당합니다.
   * 개체의 `ByteArrayOutputStream` `toByteArray` 메서드를 호출하여 바이트 배열을 채웁니다.
   * 생성자를 사용하여 바이트 배열을 전달하여 `com.adobe.idp.Document` 개체를 만듭니다.

1. PDF 문서를 참조하여 분해합니다.

   * 생성자를 사용하여 입력 PDF 문서를 저장하는 데 사용되는 `java.util.Map` 개체를 `HashMap` 만듭니다.
   * 생성자를 사용하여 `java.io.FileInputStream` 개체를 만들고 분해할 PDF 문서의 위치를 전달하여 개체를 만듭니다.
   * 객체를 `com.adobe.idp.Document` 만듭니다. PDF 문서가 포함된 `java.io.FileInputStream` 개체를 전달하여 분해합니다.
   * 해당 `java.util.Map` `put` 메서드를 호출하고 다음 인수를 전달하여 개체에 항목을 추가합니다.

      * 키 이름을 나타내는 문자열 값입니다. 이 값은 DCX 문서에 지정된 PDF 소스 요소의 값과 일치해야 합니다. 동적으로 생성된 DCX 문서에서 값은 `AssemblerResultPDF.pdf`입니다.
      * 분해할 PDF 문서를 포함하는 `com.adobe.idp.Document` 오브젝트입니다.

1. 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 런타임 옵션을 저장하는 `AssemblerOptionSpec` 객체를 만듭니다.
   * 객체에 속하는 메서드를 호출하여 비즈니스 요구 사항을 충족하도록 런타임 옵션을 `AssemblerOptionSpec` 설정합니다. 예를 들어 오류가 발생할 때 어셈블리 서비스에서 작업을 계속 처리하도록 하려면 `AssemblerOptionSpec` 개체의 `setFailOnError` 메서드를 호출하고 전달합니다 `false`.

1. PDF 문서를 분해합니다.

   객체의 `AssemblerServiceClient` `invokeDDX` 메서드를 호출하고 다음 값을 전달합니다.

   * 동적으로 생성된 DCX 문서를 나타내는 `com.adobe.idp.Document` 개체
   * 분해할 PDF 문서를 포함하는 `java.util.Map` 개체
   * 기본 글꼴 및 작업 로그 수준을 포함하여 런타임 옵션을 지정하는 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 개체
   이 `invokeDDX` 메서드는 분해된 PDF 문서와 발생한 모든 예외가 포함된 `com.adobe.livecycle.assembler.client.AssemblerResult` 개체를 반환합니다.

1. 분해된 PDF 문서를 저장합니다.

   분해된 PDF 문서를 얻으려면 다음 작업을 수행하십시오.

   * 객체의 메서드를 `AssemblerResult` 호출합니다 `getDocuments` . 이 메서드는 `java.util.Map` 개체를 반환합니다.
   * 결과 개체를 찾을 때까지 `java.util.Map` `com.adobe.idp.Document` 개체를 반복합니다.
   * PDF 문서를 추출하려면 `com.adobe.idp.Document` 개체의 `copyToFile` 방법을 불러옵니다.

**참고 항목**

[빠른 시작(SOAP 모드):동적으로 Java API를 사용하여 DCX 문서 만들기](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API를 사용하여 DCX 문서를 동적으로 만들기 {#dynamically-create-a-ddx-document-using-the-web-service-api}

Assembler Service API(웹 서비스)를 사용하여 DCX 문서를 동적으로 만들고 PDF 문서를 분해합니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 서비스 참조를 설정할 때 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`Adobe

   >[!NOTE]
   >
   >AEM `localhost` Forms를 호스팅하는 서버의 IP 주소로 대체합니다.

1. PDF Assembler 클라이언트 만들기

   * 기본 생성자를 사용하여 `AssemblerServiceClient` 객체를 만듭니다.
   * 생성자를 사용하여 `AssemblerServiceClient.Endpoint.Address` 객체를 만듭니다 `System.ServiceModel.EndpointAddress` . WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). 속성을 사용할 필요는 `lc_version` 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.
   * 필드의 값을 가져와 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다 `AssemblerServiceClient.Endpoint.Binding` . 반환 값을 로 `BasicHttpBinding`캐스팅합니다.
   * 개체 `System.ServiceModel.BasicHttpBinding` 필드를 로 설정합니다 `MessageEncoding` . `WSMessageEncoding.Mtom` 이 값을 사용하면 MTOM이 사용됩니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * AEM 양식 사용자 이름을 필드에 `AssemblerServiceClient.ClientCredentials.UserName.UserName`지정합니다.
      * 필드에 해당 암호 값을 지정합니다 `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * 필드에 상수 값을 `HttpClientCredentialType.Basic` 지정합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 필드에 상수 값을 `BasicHttpSecurityMode.TransportCredentialOnly` 지정합니다 `BasicHttpBindingSecurity.Security.Mode`.

1. DCX 문서를 만듭니다.

   * 생성자를 사용하여 `System.Xml.XmlElement` 객체를 만듭니다.
   * 개체의 `XmlElement` `CreateElement` 메서드를 호출하여 DCX 문서의 루트 요소를 만듭니다. 이 메서드는 루트 요소를 나타내는 `Element` 객체를 만듭니다. 요소의 이름을 나타내는 문자열 값을 `CreateElement` 메서드에 전달합니다. DCX 요소의 `SetAttribute` 메서드를 호출하여 값을 설정합니다. 마지막으로, `XmlElement` 개체의 `AppendChild` 메서드를 호출하여 DCX 문서에 요소를 추가합니다. DDX 개체를 인수로 전달합니다. 다음 코드 줄은 이 응용 프로그램 논리를 보여 줍니다.

      ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * 개체의 `PDFsFromBookmarks` `XmlElement` `CreateElement` 메서드를 호출하여 DCX 문서의 요소를 만듭니다. 요소의 이름을 나타내는 문자열 값을 `CreateElement` 메서드에 전달합니다. 그런 다음 해당 `SetAttribute` 메서드를 호출하여 요소의 값을 설정합니다. 요소의 `PDFsFromBookmarks` `DDX` `AppendChild` 메서드를 호출하여 요소를 루트 요소에 추가합니다. 요소 객체를 인수로 `PDFsFromBookmarks` 전달합니다. 다음 코드 줄은 이 응용 프로그램 논리를 보여 줍니다.

      ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * 개체의 `PDF` `XmlElement` `CreateElement` 메서드를 호출하여 DCX 문서의 요소를 만듭니다. 요소의 이름을 나타내는 문자열 값을 `CreateElement` 메서드에 전달합니다. 그런 다음 자식 요소의 `SetAttribute` 메서드를 호출하여 값을 설정합니다. 요소의 `PDF` `PDFsFromBookmarks` `PDFsFromBookmarks` `AppendChild` 메서드를 호출하여 요소를 요소에 추가합니다. 요소 객체를 인수로 `PDF` 전달합니다. 다음 코드 줄은 이 응용 프로그램 논리를 보여줍니다.

      ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. DCX 문서를 변환합니다.

   * 생성자를 사용하여 `System.IO.MemoryStream` 객체를 만듭니다.
   * DCX `MemoryStream` 문서를 나타내는 `XmlElement` 개체를 사용하여 개체를 DCX 문서로 채웁니다. 객체의 메서드를 호출하고 `XmlElement` `Save` `MemoryStream` 객체를 전달합니다.
   * 바이트 배열을 만들어 `MemoryStream` 개체에 있는 데이터로 채웁니다. 다음 코드는 이 응용 프로그램 논리를 보여 줍니다.

      ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * 객체를 `BLOB` 만듭니다. 바이트 배열을 `BLOB` 개체의 `MTOM` 필드에 할당합니다.

1. PDF 문서를 참조하여 분해합니다.

   * 생성자를 사용하여 `BLOB` 객체를 만듭니다. 이 `BLOB` 개체는 입력 PDF 문서를 저장하는 데 사용됩니다. 이 `BLOB` 개체는 `invokeOneDocument` 인수로 전달됩니다.
   * 생성자를 호출하여 `System.IO.FileStream` 객체를 만듭니다. 입력 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 개체의 내용을 저장하는 바이트 배열을 `System.IO.FileStream` 만듭니다. 개체의 `System.IO.FileStream` `Length` 속성을 가져와 바이트 배열의 크기를 결정할 수 있습니다.
   * 객체의 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다. `System.IO.FileStream` `Read`
   * 바이트 배열의 내용에 해당 `BLOB` `MTOM` 속성을 할당하여 개체를 채웁니다.

1. 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 런타임 옵션을 저장하는 `AssemblerOptionSpec` 객체를 만듭니다.
   * 객체에 속하는 데이터 멤버에 값을 할당하여 비즈니스 요구 사항에 맞게 런타임 옵션을 설정할 수 `AssemblerOptionSpec` 있습니다. 예를 들어 오류가 발생할 때 어셈블리 서비스에서 작업을 계속 처리하도록 하려면 개체의 `false` `AssemblerOptionSpec` `failOnError` 데이터 멤버에 할당합니다.

1. PDF 문서를 분해합니다.

   객체의 `AssemblerServiceClient` `invokeDDX` 메서드를 호출하고 다음 값을 전달합니다.

   * 동적으로 생성된 DCX 문서를 나타내는 `BLOB` 개체
   * 입력 PDF 문서를 포함하는 `mapItem` 배열
   * 런타임 옵션을 지정하는 `AssemblerOptionSpec` 개체
   이 `invokeDDX` `AssemblerResult` 메서드는 작업 결과와 발생한 예외를 포함하는 개체를 반환합니다.

1. 분해된 PDF 문서를 저장합니다.

   새로 만든 PDF 문서를 가져오려면 다음 작업을 수행하십시오.

   * 분해된 PDF 문서를 포함하는 `AssemblerResult` 개체인 개체의 `documents` `Map` 필드에 액세스합니다.
   * 객체를 반복하여 각 결과 문서를 가져옵니다. `Map` 그런 다음 해당 어레이 멤버를 `value` a로 캐스팅합니다 `BLOB`.
   * PDF 문서의 `BLOB` 개체 `MTOM` 속성에 액세스하여 이진 데이터를 추출합니다. PDF 파일에 쓸 수 있는 바이트 배열을 반환합니다.

**참고 항목**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
