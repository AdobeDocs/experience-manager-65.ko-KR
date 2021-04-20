---
title: 책갈피를 사용하여 PDF 문서 취합
seo-title: 책갈피를 사용하여 PDF 문서 취합
description: Assembler 서비스를 사용하여 Java API 및 웹 서비스 API를 사용하는 책갈피를 포함하도록 책갈피가 포함된 PDF 문서를 수정합니다.
seo-description: Assembler 서비스를 사용하여 Java API 및 웹 서비스 API를 사용하는 책갈피를 포함하도록 책갈피가 포함된 PDF 문서를 수정합니다.
uuid: a306d2a6-0b12-4eb3-bff4-968a33417486
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f4711a8-033c-4051-ab41-65a26838899b
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2589'
ht-degree: 0%

---


# 책갈피 {#assembling-pdf-documents-with-bookmarks}를 사용하여 PDF 문서 정리

**이 문서의 샘플과 예는 JEE 환경의 AEM Forms에만 해당됩니다.**

책갈피가 포함된 PDF 문서를 조합할 수 있습니다. 예를 들어 책갈피를 포함하지 않는 PDF 문서가 있고 책갈피를 제공하여 수정하려고 한다고 가정합니다. Assembler 서비스를 사용하여 책갈피가 포함되지 않은 PDF 문서를 전달하고 책갈피가 포함된 PDF 문서를 다시 가져올 수 있습니다.

책갈피에는 다음 속성이 포함됩니다.

* 화면에 텍스트로 표시되는 제목입니다.
* 사용자가 책갈피를 클릭할 때 발생하는 상황을 지정하는 작업입니다. 책갈피에 대한 일반적인 작업은 다른 작업을 지정할 수 있지만 현재 문서의 다른 위치로 이동하거나 다른 PDF 문서를 여는 것입니다.

이 토론의 목적으로 다음 DDX 문서를 사용한다고 가정합니다.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
       <PDF result="FinalDoc.pdf">
          <PDF source="Loan.pdf">
             <Bookmarks source="doc2" />
          </PDF>
       </PDF>
 </DDX>
```

이 DDX 문서 내에서 소스 속성에 `Loan.pdf` 값이 지정되어 있습니다. 이 DDX 문서는 단일 PDF 문서가 어셈블러 서비스로 전달되도록 지정합니다. 책갈피를 사용하여 PDF 문서를 취합할 때는 결과 문서의 책갈피를 설명하는 책갈피 XML 문서를 지정해야 합니다. 책갈피 XML 문서를 지정하려면 DCX 문서에 `Bookmarks` 요소가 지정되어 있는지 확인합니다.

이 DDX 문서에서 `Bookmarks` 요소는 `doc2`을 값으로 지정합니다. 이 값은 어셈블러 서비스에 전달된 입력 맵에 `doc2` 키가 포함되어 있음을 나타냅니다. `doc2` 키의 값은 책갈피 XML 문서를 나타내는 `com.adobe.idp.Document` 값입니다. ([어셈블러 서비스 및 DCX 참조](https://www.adobe.com/go/learn_aemforms_ddx_63)의 &quot;책갈피 언어&quot;를 참조하십시오.)

이 항목에서는 다음 XML 책갈피 언어를 사용하여 책갈피가 포함된 PDF 문서를 조합합니다.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <Bookmarks xmlns="https://ns.adobe.com/pdf/bookmarks" version="1.0">
       <Bookmark>
          <Action>
             <Launch NewWindow="true">
                <File Name="C:\Adobe\LoanDetails.pdf" />
             </Launch>
          </Action>
         <Title>Open the Loan document</Title>
       </Bookmark>
 <Bookmark>
          <Action>
             <Launch>
                <Win Name="C:\WINDOWS\notepad.exe" />
             </Launch>
          </Action>
     <Title>Launch NotePad</Title>
       </Bookmark>
 </Bookmarks>
```

이 책갈피 XML 문서 내에서 사용자가 책갈피를 클릭할 때 수행되는 작업을 정의하는 작업 요소를 확인합니다. [동작] 요소 아래에는 NotePad와 같은 응용 프로그램을 시작하고 PDF 파일과 같은 파일을 여는 시작 요소가 있습니다. PDF 파일을 열려면 열 파일을 지정하는 파일 요소를 사용해야 합니다. 예를 들어 이 섹션에 지정된 책갈피 XML 파일에서 연 파일의 이름은 LoanDetails.pdf입니다.

>[!NOTE]
>
>지원되는 작업에 대한 자세한 내용은 [어셈블러 서비스의 &quot; `Action` 요소&quot; 및 DCX 참조](https://www.adobe.com/go/learn_aemforms_ddx_63)를 참조하십시오.

이 섹션에 지정된 DDX 문서를 입력하고 XML 파일을 입력으로 책갈피를 지정한 경우 어셈블러 서비스는 다음 책갈피가 포함된 PDF 문서를 어셈블합니다.

![aw_aw_bmark](assets/aw_aw_bmark.png)

사용자가 *대출 세부 사항* 책갈피를 클릭하면 LoanDetails.pdf가 열립니다. 마찬가지로 사용자가 *노트 패드 시작* 책갈피를 클릭하면 노트 패드가 시작됩니다.

>[!NOTE]
>
>이 섹션을 읽기 전에 Assembler 서비스를 사용하여 PDF 문서를 취합하는 방법을 숙지하는 것이 좋습니다. 이 섹션에서는 입력 문서를 포함하는 컬렉션 개체를 만들거나 반환된 컬렉션 개체에서 결과를 추출하는 방법을 학습하는 등의 개념에 대해 다루지 않습니다. 자세한 내용은 [프로그래밍 방식으로 PDF 문서 조합](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)을 참조하십시오.

>[!NOTE]
>
>어셈블러 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

>[!NOTE]
>
>DCX 문서에 대한 자세한 내용은 [어셈블러 서비스 및 DCX 참조](https://www.adobe.com/go/learn_aemforms_ddx_63)를 참조하십시오.

## {#summary-of-steps} 단계 요약

책갈피가 포함된 PDF 문서를 취합하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일 포함
1. PDF Assembler 클라이언트를 만듭니다.
1. 기존 DCX 문서를 참조합니다.
1. 책갈피가 추가되는 PDF 문서를 참조합니다.
1. 책갈피 XML 문서를 참조하십시오.
1. PDF 문서와 책갈피 XML 문서를 맵 컬렉션에 추가합니다.
1. 런타임 옵션을 설정합니다.
1. PDF 문서를 조합합니다.
1. 책갈피가 포함된 PDF 문서를 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

다음 JAR 파일을 프로젝트의 클래스 경로에 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar (AEM Forms이 JBoss에 배포된 경우 필수)

AEM Forms이 JBoss가 아닌 지원되는 J2EE 응용 프로그램 서버에 배포되는 경우 adobe-utilities.jar 및 jbossall-client.jar 파일을 AEM Forms이 배포된 J2EE 응용 프로그램 서버에 해당하는 JAR 파일로 대체해야 합니다. 모든 AEM Forms JAR 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)을 참조하십시오.

**PDF Assembler 클라이언트 만들기**

어셈블리 작업을 프로그래밍 방식으로 수행하려면 먼저 어셈블러 서비스 클라이언트를 만들어야 합니다.

**기존 DCX 문서 참조**

PDF 문서를 조합하려면 DCX 문서를 참조해야 합니다. 이 DCX 문서에는 Assembler 서비스에 책갈피가 포함된 PDF를 조합하도록 하는 `Bookmarks` 요소가 포함되어야 합니다. (예제는 이 섹션 앞에 표시된 DCX 문서를 참조하십시오.)

**책갈피가 추가된 PDF 문서 참조**

책갈피가 추가되는 PDF 문서를 참조합니다. 참조된 PDF 문서에 이미 책갈피가 포함되어 있는지 여부는 중요하지 않습니다. `Bookmarks` 요소가 PDF 소스 요소의 하위 요소인 경우 책갈피는 PDF 원본에 이미 있는 요소를 대체합니다. 그러나 기존 책갈피를 유지하려면 `Bookmarks`이(가) PDF 소스 요소의 동위 항목인지 확인하십시오. 예를 들어 다음 예를 생각해 보십시오.

```xml
 <PDF result="foo">
      <PDF source="inDoc"/>
      <Bookmarks source="doc2"/>
 </PDF>
```

**책갈피 XML 문서 참조**

새 책갈피가 포함된 PDF를 취합하려면 책갈피 XML 문서를 참조해야 합니다. 책갈피 XML 문서는 Map 컬렉션 개체 내의 어셈블러 서비스로 전달됩니다. (예를 보려면 이 섹션 앞에 표시된 책갈피 XML 문서를 참조하십시오.)

>[!NOTE]
>
>[어셈블러 서비스 및 DCX 참조](https://www.adobe.com/go/learn_aemforms_ddx_63)의 &quot;책갈피 언어&quot;를 참조하십시오.

**PDF 문서와 책갈피 XML 문서를 맵 컬렉션에 추가**

책갈피를 추가할 PDF 문서와 책갈피 XML 문서를 맵 컬렉션에 모두 추가해야 합니다. 따라서 맵 컬렉션 개체에는 다음 두 가지 요소가 포함됩니다.PDF 문서와 책갈피 XML 문서.

**런타임 옵션 설정**

작업을 수행하는 동안 어셈블리 서비스의 동작을 제어하는 런타임 옵션을 설정할 수 있습니다. 예를 들어 오류가 발생하면 어셈블리 서비스에 작업을 계속 처리하도록 하는 옵션을 설정할 수 있습니다. 설정할 수 있는 런타임 옵션에 대한 자세한 내용은 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)의 `AssemblerOptionSpec` 클래스 참조를 참조하십시오.

**PDF 문서 조합**

새 책갈피가 포함된 PDF 문서를 어셈블하려면 Assembler 서비스의 `invokeDDX` 작업을 사용합니다. `invokeOneDocument`과 같은 다른 어셈블러 서비스 작업과 반대로 `invokeDDX` 작업을 사용해야 하는 이유는 어셈블러 서비스에 맵 컬렉션 개체 내에 전달되는 책갈피 XML 문서가 필요하기 때문입니다. 이 개체는 `invokeDDX` 작업의 매개 변수입니다.

**책갈피가 포함된 PDF 문서 저장**

반환된 맵 개체에서 결과를 추출하고 해당 PDF 문서를 저장해야 합니다. ([프로그래밍 방식으로 PDF 문서 조합](/help/forms/developing/programmatically-assembling-pdf-documents.md)의 &quot;결과 추출&quot;을 참조하십시오.)

**참고 항목**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[프로그래밍 방식으로 PDF 문서 취합](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API {#assemble-pdf-documents-with-bookmarks-using-the-java-api}를 사용하여 책갈피와 함께 PDF 문서 조합

Assembler Service API(Java)를 사용하여 책갈피와 함께 PDF 문서를 조합합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-assembler-client.jar 등의 클라이언트 JAR 파일을 포함합니다.

1. PDF Assembler 클라이언트를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다. ([연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)을 참조하십시오.)
   * 생성자를 사용하여 `AssemblerServiceClient` 개체를 만들고 `ServiceClientFactory` 개체를 전달합니다.

1. 기존 DCX 문서를 참조합니다.

   * 생성자를 사용하여 DCX 문서를 나타내는 `java.io.FileInputStream` 객체를 만들고 DCX 파일의 위치를 지정하는 문자열 값을 전달합니다.
   * 생성자를 사용하여 `com.adobe.idp.Document` 개체를 만들고 `java.io.FileInputStream` 개체를 전달합니다.

1. 책갈피가 추가되는 PDF 문서를 참조합니다.

   * 생성자를 사용하여 PDF 문서의 위치를 전달하여 `java.io.FileInputStream` 객체를 만듭니다.
   * 생성자를 사용하여 `com.adobe.idp.Document` 개체를 만들고 PDF 문서가 포함된 `java.io.FileInputStream` 개체를 전달합니다.

1. 책갈피 XML 문서를 참조하십시오.

   * 생성자를 사용하여 `java.io.FileInputStream` 객체를 만들고 책갈피 XML 문서를 나타내는 XML 파일의 위치를 전달합니다.
   * `com.adobe.idp.Document` 개체를 만들고 PDF 문서가 포함된 `java.io.FileInputStream` 개체를 전달합니다.

1. PDF 문서와 책갈피 XML 문서를 맵 컬렉션에 추가합니다.

   * 입력 PDF 문서와 책갈피 XML 문서를 모두 저장하는 데 사용되는 `java.util.Map` 개체를 만듭니다.
   * `java.util.Map` 개체의 `put` 메서드를 호출하고 다음 인수를 전달하여 입력 PDF 문서를 추가합니다.

      * 키 이름을 나타내는 문자열 값입니다. 이 값은 DCX 문서에 지정된 PDF 소스 요소의 값과 일치해야 합니다.
      * 입력 PDF 문서를 포함하는 `com.adobe.idp.Document` 객체입니다.
   * `java.util.Map` 객체의 `put` 메서드를 호출하고 다음 인수를 전달하여 책갈피 XML 문서를 추가합니다.

      * 키 이름을 나타내는 문자열 값입니다. 이 값은 DCX 문서에 지정된 책갈피 소스 요소의 값과 일치해야 합니다.
      * 책갈피 XML 문서를 포함하는 `com.adobe.idp.Document` 개체


1. 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 런타임 옵션을 저장하는 `AssemblerOptionSpec` 객체를 만듭니다.
   * `AssemblerOptionSpec` 개체에 속하는 메서드를 호출하여 비즈니스 요구 사항을 충족하도록 런타임 옵션을 설정합니다. 예를 들어 오류가 발생할 때 어셈블리 서비스에서 작업을 계속 처리하도록 하려면 `AssemblerOptionSpec` 개체의 `setFailOnError` 메서드를 호출하고 `false`를 전달합니다.

1. PDF 문서를 조합합니다.

   `AssemblerServiceClient` 객체의 `invokeDDX` 메서드를 호출하고 다음 필수 값을 전달합니다.

   * 사용할 DCX 문서를 나타내는 `com.adobe.idp.Document` 개체
   * 입력 PDF 문서와 책갈피 XML 문서를 모두 포함하는 `java.util.Map` 개체
   * 기본 글꼴 및 작업 로그 수준을 포함하여 런타임 옵션을 지정하는 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 개체

   `invokeDDX` 메서드는 작업 결과와 발생한 예외가 포함된 `com.adobe.livecycle.assembler.client.AssemblerResult` 개체를 반환합니다.

1. 책갈피가 포함된 PDF 문서를 저장합니다.

   새로 만든 PDF 문서를 얻으려면 다음 작업을 수행합니다.

   * `AssemblerResult` 객체의 `getDocuments` 메서드를 호출합니다. `java.util.Map` 객체를 반환합니다.
   * 결과 `com.adobe.idp.Document` 개체를 찾을 때까지 `java.util.Map` 개체를 반복합니다. DCX 문서에 지정된 PDF 결과 요소를 사용하여 문서를 가져올 수 있습니다.
   * `com.adobe.idp.Document` 개체의 `copyToFile` 메서드를 호출하여 PDF 문서를 추출합니다.

**참고 항목**

[빠른 시작(SOAP 모드):Java API를 사용하여 책갈피를 사용하여 PDF 문서 취합](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API {#assemble-pdf-documents-with-bookmarks-using-the-web-service-api}를 사용하여 책갈피와 함께 PDF 문서 조합

Assembler Service API(웹 서비스)를 사용하여 책갈피와 함께 PDF 문서를 조합합니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다.`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꿉니다.

1. PDF Assembler 클라이언트를 만듭니다.

   * 기본 생성자를 사용하여 `AssemblerServiceClient` 객체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `AssemblerServiceClient.Endpoint.Address` 객체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스(예: `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)에 전달합니다. `lc_version` 특성을 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.
   * `AssemblerServiceClient.Endpoint.Binding` 필드의 값을 가져와서 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`으로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`로 설정합니다. 이 값을 사용하면 MTOM이 사용됩니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * AEM 양식 사용자 이름을 `AssemblerServiceClient.ClientCredentials.UserName.UserName` 필드에 지정합니다.
      * 해당 암호 값을 `AssemblerServiceClient.ClientCredentials.UserName.Password` 필드에 지정합니다.
      * `BasicHttpBindingSecurity.Transport.ClientCredentialType` 필드에 상수 값 `HttpClientCredentialType.Basic`을 할당합니다.
      * `BasicHttpBindingSecurity.Security.Mode` 필드에 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을 할당합니다.

1. 기존 DCX 문서를 참조합니다.

   * 생성자를 사용하여 `BLOB` 객체를 만듭니다. `BLOB` 개체는 DCX 문서를 저장하는 데 사용됩니다.
   * 생성자를 호출하고 DCX 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 객체를 만듭니다.
   * `System.IO.FileStream` 객체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 객체의 `Length` 속성을 가져와 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 객체의 `Read` 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * 바이트 배열의 내용으로 `MTOM` 필드를 할당하여 `BLOB` 개체를 채웁니다.

1. 책갈피가 추가되는 PDF 문서를 참조합니다.

   * 생성자를 사용하여 `BLOB` 객체를 만듭니다. `BLOB` 개체는 입력 PDF를 저장하는 데 사용됩니다.
   * 생성자를 호출하고 입력 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 객체를 만듭니다.
   * `System.IO.FileStream` 객체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 객체의 `Length` 속성을 가져와 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 객체의 `Read` 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * 바이트 배열의 내용으로 `MTOM` 필드를 할당하여 `BLOB` 개체를 채웁니다.

1. 책갈피 XML 문서를 참조하십시오.

   * 생성자를 사용하여 `BLOB` 객체를 만듭니다. `BLOB` 개체는 책갈피 XML 문서를 저장하는 데 사용됩니다.
   * 생성자를 호출하고 입력 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 객체를 만듭니다.
   * `System.IO.FileStream` 객체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 객체의 `Length` 속성을 가져와 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 객체의 `Read` 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * 바이트 배열의 내용으로 `MTOM` 필드를 할당하여 `BLOB` 개체를 채웁니다.

1. PDF 문서와 책갈피 XML 문서를 맵 컬렉션에 추가합니다.

   * `MyMapOf_xsd_string_To_xsd_anyType` 개체를 만듭니다. 이 컬렉션 객체는 입력 PDF 문서 및 책갈피 XML 문서를 저장하는 데 사용됩니다.
   * 각 입력 PDF 문서와 책갈피 XML 문서에 대해 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체를 만듭니다.
   * 키 이름을 나타내는 문자열 값을 `MyMapOf_xsd_string_To_xsd_anyType_Item` 객체의 `key` 필드에 지정합니다. 이 값은 DCX 문서에 지정된 PDF 소스 요소의 값과 일치해야 합니다.
   * PDF 문서를 저장하는 `BLOB` 개체를 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체의 `value` 필드에 할당합니다.
   * `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체를 `MyMapOf_xsd_string_To_xsd_anyType` 개체에 추가합니다. `MyMapOf_xsd_string_To_xsd_anyType` 객체의 `Add` 메서드를 호출하고 `MyMapOf_xsd_string_To_xsd_anyType` 객체를 전달합니다. 각 입력 PDF 문서 및 책갈피 XML 문서에 대해 이 작업을 수행합니다.

1. 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 런타임 옵션을 저장하는 `AssemblerOptionSpec` 객체를 만듭니다.
   * `AssemblerOptionSpec` 개체에 속하는 데이터 멤버에 값을 할당하여 비즈니스 요구 사항에 맞게 런타임 옵션을 설정합니다. 예를 들어 오류가 발생할 때 어셈블리 서비스에서 작업을 계속 처리하도록 하려면 `false`을(를) `AssemblerOptionSpec` 개체의 `failOnError` 데이터 멤버에 할당합니다.

1. PDF 문서를 조합합니다.

   `AssemblerServiceClient` 객체의 `invokeDDX` 메서드를 호출하고 다음 값을 전달합니다.

   * DCX 문서를 나타내는 `BLOB` 개체
   * 입력 문서를 포함하는 `MyMapOf_xsd_string_To_xsd_anyType` 배열
   * 런타임 옵션을 지정하는 `AssemblerOptionSpec` 개체

   `invokeDDX` 메서드는 작업 결과와 발생한 예외가 포함된 `AssemblerResult` 개체를 반환합니다.

1. 책갈피가 포함된 PDF 문서를 저장합니다.

   새로 만든 PDF 문서를 얻으려면 다음 작업을 수행합니다.

   * 결과 PDF 문서를 포함하는 `Map` 개체인 `AssemblerResult` 개체의 `documents` 필드에 액세스합니다.
   * 결과 문서의 이름과 일치하는 키를 찾을 때까지 `Map` 개체를 반복합니다. 그런 다음 해당 배열 멤버의 `value`을(를) `BLOB`로 캐스팅합니다.
   * `BLOB` 개체의 `MTOM` 필드에 액세스하여 PDF 문서를 나타내는 이진 데이터를 추출합니다. PDF 파일에 기록할 수 있는 바이트 배열을 반환합니다.

**참고 항목**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
