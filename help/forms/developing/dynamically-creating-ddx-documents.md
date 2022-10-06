---
title: 동적으로 DDX 문서 만들기
seo-title: Dynamically Creating DDX Documents
description: Java API 및 웹 서비스 API를 사용하여 동적으로 DDX 문서를 만듭니다. DDX 문서를 동적으로 만들면 런타임 중에 얻은 DDX 문서의 값을 사용할 수 있습니다.
seo-description: Create a DDX document dynamically using the Java API and Web Service API. Dynamically creating a DDX document enables you to use values in the DDX document that are obtained during run-time.
uuid: b73e8069-6c9f-4517-a0ae-f3d503191d2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2ad227de-68a8-446f-8c4f-a33a6f95bec8
role: Developer
exl-id: b3c19c82-e26f-4dc8-b846-6aec705cee08
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2163'
ht-degree: 0%

---

# 동적으로 DDX 문서 만들기 {#dynamically-creating-ddx-documents}

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms용입니다.**

어셈블러 작업을 수행하는 데 사용할 수 있는 DDX 문서를 동적으로 만들 수 있습니다. DDX 문서를 동적으로 만들면 런타임 중에 얻은 DDX 문서의 값을 사용할 수 있습니다. DDX 문서를 동적으로 만들려면 사용 중인 프로그래밍 언어에 속하는 클래스를 사용합니다. 예를 들어, Java를 사용하여 클라이언트 응용 프로그램을 개발하는 경우에는 `org.w3c.dom.*`패키지. 마찬가지로 Microsoft .NET을 사용하는 경우에는 `System.Xml` 네임스페이스.

DDX 문서를 어셈블러 서비스로 전달하려면 먼저 XML을 `org.w3c.dom.Document` 인스턴스에 대한 인스턴스 `com.adobe.idp.Document` 인스턴스. 웹 서비스를 사용하는 경우 XML을 만드는 데 사용되는 데이터 유형에서 XML을 변환합니다(예: `XmlDocument`) `BLOB` 인스턴스.

이 논의에서는 다음 DDX 문서가 동적으로 작성되었다고 가정합니다.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

이 DDX 문서는 PDF 문서를 분해합니다. PDF 문서 디스어셈블리는 잘 알고 있는 것이 좋습니다.

>[!NOTE]
>
>어셈블러 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDX 문서에 대한 자세한 내용은 [어셈블러 서비스 및 DDX 참조](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 단계 요약 {#summary-of-steps}

동적으로 생성된 DDX 문서를 사용하여 PDF 문서를 분해하려면 다음 작업을 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. PDF 어셈블러 클라이언트를 만듭니다.
1. DDX 문서를 만듭니다.
1. DDX 문서를 변환합니다.
1. 런타임 옵션을 설정합니다.
1. PDF 문서를 분해합니다.
1. 분해된 PDF 문서를 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함하십시오. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms이 JBoss에 배포되는 경우 필요)

**PDF 어셈블러 클라이언트 만들기**

프로그래밍 방식으로 어셈블러 작업을 수행하려면 먼저 어셈블러 서비스 클라이언트를 만듭니다.

**DDX 문서 만들기**

사용 중인 프로그래밍 언어를 사용하여 DDX 문서를 만듭니다. PDF 문서를 디스어셈블하는 DDX 문서를 만들려면 DDX 문서에 `PDFsFromBookmarks` 요소를 생성하지 않습니다. DDX 문서를 만드는 데 사용되는 데이터 유형을 `com.adobe.idp.Document` Java API를 사용하는 경우 인스턴스. 웹 서비스를 사용하는 경우 데이터 형식을 `BLOB` 인스턴스.

**DDX 문서 변환**

를 사용하여 만든 DDX 문서 `org.w3c.dom` 클래스는 `com.adobe.idp.Document` 개체. Java API를 사용할 때 이 작업을 수행하려면 Java XML 변환 클래스를 사용합니다. 웹 서비스를 사용하는 경우 DDX 문서를 `BLOB` 개체.

**디스어셈블할 PDF 문서 참조**

PDF 문서를 분해하려면 분해할 PDF 문서를 나타내는 PDF 파일을 참조합니다. 어셈블러 서비스에 전달되면 문서의 각 수준 1 책갈피에 대해 별도의 PDF 문서가 반환됩니다.

**런타임 옵션 설정**

작업을 수행하는 동안 어셈블러 서비스의 동작을 제어하는 런타임 옵션을 설정할 수 있습니다. 예를 들어 오류가 발생하면 어셈블러 서비스에 작업을 계속 처리하도록 지시하는 옵션을 설정할 수 있습니다. 런타임 옵션을 설정하려면 `AssemblerOptionSpec` 개체.

**PDF 문서 분해**

를 호출하여 PDF 문서 분해 `invokeDDX` 작업. 동적으로 생성된 DDX 문서를 전달합니다. 어셈블러 서비스는 컬렉션 개체 내에서 분해된 PDF 문서를 반환합니다.

**분해된 PDF 문서를 저장합니다**

어셈블된 모든 PDF 문서는 컬렉션 개체 내에서 반환됩니다. 수집 객체를 반복하고 각 PDF 문서를 PDF 파일로 저장합니다.

**추가 참조**

[Java API를 사용하여 DDX 문서를 동적으로 만듭니다](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[웹 서비스 API를 사용하여 DDX 문서를 동적으로 만듭니다](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[프로그래밍 방식으로 PDF 문서 분해](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Java API를 사용하여 DDX 문서를 동적으로 만듭니다 {#dynamically-create-a-ddx-document-using-the-java-api}

DDX 문서를 동적으로 생성하고 Assembler Service API(Java)를 사용하여 PDF 문서를 디스어셈블합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-assembler-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. PDF 어셈블러 클라이언트를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 객체입니다.
   * 만들기 `AssemblerServiceClient` 생성자를 사용하여 객체를 전달하고 `ServiceClientFactory` 개체.

1. DDX 문서를 만듭니다.

   * Java 만들기 `DocumentBuilderFactory` 를 호출하여 개체를 `DocumentBuilderFactory` class&#39; `newInstance` 메서드를 사용합니다.
   * Java 만들기 `DocumentBuilder` 를 호출하여 개체를 `DocumentBuilderFactory` 개체 `newDocumentBuilder` 메서드를 사용합니다.
   * 호출 `DocumentBuilder` 개체 `newDocument` 인스턴스화 방법 `org.w3c.dom.Document` 개체.
   * DDX 문서의 루트 요소를 `org.w3c.dom.Document` 개체 `createElement` 메서드를 사용합니다. 이 메서드는 `Element` 루트 요소를 나타내는 개체입니다. 요소의 이름을 나타내는 문자열 값을 `createElement` 메서드를 사용합니다. 반환 값을 다음으로 캐스팅합니다. `Element`. 그런 다음 하위 요소의 값을 `setAttribute` 메서드를 사용합니다. 마지막으로, 헤더 요소의 `appendChild` 메서드를 사용하여 자식 요소 개체를 인수로 전달합니다. 다음 코드 줄은 이 응용 프로그램 논리를 보여 줍니다.
      ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * 만들기 `PDFsFromBookmarks` 요소를 호출하여 `Document` 개체 `createElement` 메서드를 사용합니다. 요소의 이름을 나타내는 문자열 값을 `createElement` 메서드를 사용합니다. 반환 값을 다음으로 캐스팅합니다. `Element`. 에 대한 값 설정 `PDFsFromBookmarks` 요소를 호출하여 `setAttribute` 메서드를 사용합니다. 추가 `PDFsFromBookmarks` 요소를 `DDX` DDX 요소의 `appendChild` 메서드를 사용합니다. 전달 `PDFsFromBookmarks` 요소 개체를 인수로 사용합니다. 다음 코드 줄은 이 응용 프로그램 논리를 보여 줍니다.

      ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * 만들기 `PDF` 요소를 호출하여 `Document` 개체 `createElement` 메서드를 사용합니다. 요소의 이름을 나타내는 문자열 값을 전달합니다. 반환 값을 다음으로 캐스팅합니다. `Element`. 에 대한 값 설정 `PDF` 요소를 호출하여 `setAttribute` 메서드를 사용합니다. 추가 `PDF` 요소를 `PDFsFromBookmarks` 요소를 호출하여 `PDFsFromBookmarks` 요소 `appendChild` 메서드를 사용합니다. 전달 `PDF` 요소 개체를 인수로 사용합니다. 다음 코드 줄은 이 응용 프로그램 논리를 보여 줍니다.

      ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. DDX 문서를 변환합니다.

   * 만들기 `javax.xml.transform.Transformer` 객체를 호출하여 `javax.xml.transform.Transformer` 개체의 정적 `newInstance` 메서드를 사용합니다.
   * 만들기 `Transformer` 객체를 호출하여 `TransformerFactory` 개체 `newTransformer` 메서드를 사용합니다.
   * 만들기 `ByteArrayOutputStream` 생성자를 사용하여 개체를 작성합니다.
   * 만들기 `javax.xml.transform.dom.DOMSource` 생성자를 사용하여 개체를 작성합니다. 전달 `org.w3c.dom.Document` DDX 문서를 나타내는 객체입니다.
   * 만들기 `javax.xml.transform.dom.DOMSource` 생성자를 사용하여 객체를 전달하고 `ByteArrayOutputStream` 개체.
   * Java 채우기 `ByteArrayOutputStream` 객체를 호출하여 `javax.xml.transform.Transformer` 개체 `transform` 메서드를 사용합니다. 전달 `javax.xml.transform.dom.DOMSource` 그리고 `javax.xml.transform.stream.StreamResult` 개체.
   * 바이트 배열을 만들고 크기를 할당합니다 `ByteArrayOutputStream` 개체를 바이트 배열에 추가합니다.
   * 를 호출하여 바이트 배열을 채웁니다 `ByteArrayOutputStream` 개체 `toByteArray` 메서드를 사용합니다.
   * 만들기 `com.adobe.idp.Document` 생성자를 사용하여 바이트 배열을 전달합니다.

1. 분해할 PDF 문서를 참조합니다.

   * 만들기 `java.util.Map` 입력 PDF 문서를 저장하는 데 사용되는 개체 `HashMap` 생성자입니다.
   * 만들기 `java.io.FileInputStream` 생성자를 사용하여 PDF 문서의 위치를 전달하여 디스어셈블할 수 있습니다.
   * 만들기 `com.adobe.idp.Document` 개체. 전달 `java.io.FileInputStream` 분해할 PDF 문서가 포함된 객체입니다.
   * 에 항목 추가 `java.util.Map` 객체를 호출하여 `put` 메서드와 다음 인수를 전달합니다.

      * 키 이름을 나타내는 문자열 값입니다. 이 값은 DDX 문서에 지정된 PDF 소스 요소의 값과 일치해야 합니다. 동적으로 생성되는 DDX 문서에서 값은 `AssemblerResultPDF.pdf`)
      * A `com.adobe.idp.Document` 분해할 PDF 문서가 포함된 객체입니다.

1. 런타임 옵션을 설정합니다.

   * 만들기 `AssemblerOptionSpec` 생성자를 사용하여 런타임 옵션을 저장하는 개체입니다.
   * 에 속한 메서드를 호출하여 비즈니스 요구 사항을 충족하도록 런타임 옵션을 설정합니다. `AssemblerOptionSpec` 개체. 예를 들어 오류가 발생할 때 어셈블러 서비스에서 작업을 계속 처리하도록 하려면 `AssemblerOptionSpec` 개체 `setFailOnError` 메서드 및 전달 `false`.

1. PDF 문서를 분해합니다.

   를 호출합니다 `AssemblerServiceClient` 개체 `invokeDDX` 메서드를 사용하여 다음 값을 전달합니다.

   * A `com.adobe.idp.Document` 동적으로 생성된 DDX 문서를 나타내는 객체
   * A `java.util.Map` 디스어셈블할 PDF 문서가 포함된 객체
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 기본 글꼴과 작업 로그 레벨을 포함하여 런타임 옵션을 지정하는 객체

   다음 `invokeDDX` 메서드 반환 `com.adobe.livecycle.assembler.client.AssemblerResult` 디스어셈블된 PDF 문서와 발생한 예외를 포함하는 객체입니다.

1. 분해된 PDF 문서를 저장합니다.

   분해된 PDF 문서를 가져오려면 다음 작업을 수행하십시오.

   * 를 호출합니다 `AssemblerResult` 개체 `getDocuments` 메서드를 사용합니다. 이 메서드는 `java.util.Map` 개체.
   * 를 통해 반복 `java.util.Map` 결과를 찾을 때까지 객체 `com.adobe.idp.Document` 개체.
   * 를 호출합니다 `com.adobe.idp.Document` 개체 `copyToFile` PDF 문서를 추출하는 방법입니다.

**추가 참조**

[빠른 시작(SOAP 모드): Java API를 사용하여 DDX 문서를 동적으로 생성](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API를 사용하여 DDX 문서를 동적으로 만듭니다 {#dynamically-create-a-ddx-document-using-the-web-service-api}

DDX 문서를 동적으로 만들고 어셈블러 서비스 API(웹 서비스)를 사용하여 PDF 문서를 디스어셈블합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 서비스 참조를 설정할 때 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` (AEM Forms을 호스팅하는 서버의 IP 주소 사용)

1. PDF 어셈블러 클라이언트를 만듭니다.

   * 만들기 `AssemblerServiceClient` 기본 생성자를 사용하여 개체를 만듭니다.
   * 만들기 `AssemblerServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). 를 사용할 필요가 없습니다 `lc_version` 속성을 사용합니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.
   * 만들기 `System.ServiceModel.BasicHttpBinding` 개체의 값을 가져와서 `AssemblerServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스팅합니다. `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름을 지정합니다 `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * 필드에 해당 암호 값을 지정합니다 `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 할당 `HttpClientCredentialType.Basic` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 상수 값 할당 `BasicHttpSecurityMode.TransportCredentialOnly` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Security.Mode`.

1. DDX 문서를 만듭니다.

   * 만들기 `System.Xml.XmlElement` 생성자를 사용하여 개체를 작성합니다.
   * DDX 문서의 루트 요소를 `XmlElement` 개체 `CreateElement` 메서드를 사용합니다. 이 메서드는 `Element` 루트 요소를 나타내는 개체입니다. 요소의 이름을 나타내는 문자열 값을 `CreateElement` 메서드를 사용합니다. DDX 요소의 값을 `SetAttribute` 메서드를 사용합니다. 마지막으로, `XmlElement` 개체 `AppendChild` 메서드를 사용합니다. DDX 개체를 인수로 전달합니다. 다음 코드 줄은 이 응용 프로그램 논리를 보여 줍니다.

      ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * DDX 문서 만들기 `PDFsFromBookmarks` 요소를 호출하여 `XmlElement` 개체 `CreateElement` 메서드를 사용합니다. 요소의 이름을 나타내는 문자열 값을 `CreateElement` 메서드를 사용합니다. 다음으로, 요소를 호출하여 요소의 값을 설정합니다 `SetAttribute` 메서드를 사용합니다. 추가 `PDFsFromBookmarks` 를 호출하여 루트 요소에 대한 요소 `DDX` 요소 `AppendChild` 메서드를 사용합니다. 전달 `PDFsFromBookmarks` 요소 개체를 인수로 사용합니다. 다음 코드 줄은 이 응용 프로그램 논리를 보여 줍니다.

      ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * DDX 문서 만들기 `PDF` 요소를 호출하여 `XmlElement` 개체 `CreateElement` 메서드를 사용합니다. 요소의 이름을 나타내는 문자열 값을 `CreateElement` 메서드를 사용합니다. 그런 다음 하위 요소의 값을 `SetAttribute` 메서드를 사용합니다. 추가 `PDF` 요소를 `PDFsFromBookmarks` 요소를 호출하여 `PDFsFromBookmarks` 요소 `AppendChild` 메서드를 사용합니다. 전달 `PDF` 요소 개체를 인수로 사용합니다. 다음 코드 줄은 이 응용 프로그램 논리를 보여 줍니다.

      ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. DDX 문서를 변환합니다.

   * 만들기 `System.IO.MemoryStream` 생성자를 사용하여 개체를 작성합니다.
   * 을(를) 채우기 `MemoryStream` DDX 문서를 사용하여 개체를 작성합니다 `XmlElement` DDX 문서를 나타내는 객체입니다. 를 호출합니다 `XmlElement` 개체 `Save` 메서드 및 전달 `MemoryStream` 개체.
   * 바이트 배열을 만들어 `MemoryStream` 개체. 다음 코드는 이 응용 프로그램 논리를 보여 줍니다.

      ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * 만들기 `BLOB` 개체. 바이트 배열을 `BLOB` 개체 `MTOM` 필드.

1. 분해할 PDF 문서를 참조합니다.

   * 만들기 `BLOB` 생성자를 사용하여 개체를 작성합니다. 다음 `BLOB` 개체는 입력 PDF 문서를 저장하는 데 사용됩니다. 이 `BLOB` 개체가 `invokeOneDocument` 논쟁으로.
   * 만들기 `System.IO.FileStream` 개체를 생성자로 호출하여 개체를 가져옵니다. 입력 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 내용을 저장하는 바이트 배열을 만듭니다 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성을 사용합니다.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채웁니다 `System.IO.FileStream` 개체 `Read` 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하는 메서드와 전달
   * 을(를) 채우기 `BLOB` 개체를 할당하여 개체를 개체 개체 `MTOM` 속성은 바이트 배열의 내용을 나타냅니다.

1. 런타임 옵션을 설정합니다.

   * 만들기 `AssemblerOptionSpec` 생성자를 사용하여 런타임 옵션을 저장하는 개체입니다.
   * 비즈니스 요구 사항에 맞게 런타임 옵션을 설정하려면 `AssemblerOptionSpec` 개체. 예를 들어 오류가 발생할 때 어셈블러 서비스에서 작업을 계속 처리하도록 지시하려면 을 할당합니다. `false` 변환 후 `AssemblerOptionSpec` 개체 `failOnError` 데이터 멤버.

1. PDF 문서를 분해합니다.

   를 호출합니다 `AssemblerServiceClient` 개체 `invokeDDX` 메서드를 사용하여 다음 값을 전달합니다.

   * A `BLOB` 동적으로 생성된 DDX 문서를 나타내는 객체
   * 다음 `mapItem` 입력 PDF 문서가 포함된 배열
   * An `AssemblerOptionSpec` 런타임 옵션을 지정하는 객체

   다음 `invokeDDX` 메서드 반환 `AssemblerResult` 작업의 결과와 발생한 예외를 포함하는 객체입니다.

1. 분해된 PDF 문서를 저장합니다.

   새로 만든 PDF 문서를 가져오려면 다음 작업을 수행하십시오.

   * 액세스 권한 `AssemblerResult` 개체 `documents` 필드, 즉 `Map` 분해된 PDF 문서를 포함하는 객체입니다.
   * 를 통해 반복 `Map` 각 결과 문서를 가져올 객체입니다. 그런 다음 해당 어레이 멤버의 `value` 변환 후 `BLOB`.
   * PDF 문서에 액세스하여 이진 데이터를 추출합니다 `BLOB` 개체 `MTOM` 속성을 사용합니다. PDF 파일에 쓸 수 있는 바이트 배열을 반환합니다.

**추가 참조**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
