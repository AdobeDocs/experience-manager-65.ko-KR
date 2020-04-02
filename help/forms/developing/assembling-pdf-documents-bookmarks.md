---
title: 책갈피를 사용하여 PDF 문서 취합
seo-title: 책갈피를 사용하여 PDF 문서 취합
description: 'null'
seo-description: 'null'
uuid: a306d2a6-0b12-4eb3-bff4-968a33417486
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f4711a8-033c-4051-ab41-65a26838899b
translation-type: tm+mt
source-git-commit: e3f700b52446505224fa4b4688d439750a66f471

---


# 책갈피를 사용하여 PDF 문서 취합 {#assembling-pdf-documents-with-bookmarks}

책갈피가 포함된 PDF 문서를 취합할 수 있습니다. 예를 들어 책갈피를 포함하지 않는 PDF 문서가 있고 책갈피를 제공하여 수정하려고 한다고 가정합니다. Assembler 서비스를 사용하면 책갈피가 없는 PDF 문서를 전달하고 책갈피가 포함된 PDF 문서를 다시 가져올 수 있습니다.

책갈피에는 다음 속성이 포함됩니다.

* 화면에 텍스트로 표시되는 제목입니다.
* 사용자가 책갈피를 클릭할 때 수행되는 작업을 지정하는 동작입니다. 책갈피의 일반적인 동작은 다른 작업을 지정할 수 있지만 현재 문서의 다른 위치로 이동하거나 다른 PDF 문서를 여는 것입니다.

이 토론의 목적을 위해 다음 DCX 문서가 사용되었다고 가정합니다.

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
       <PDF result="FinalDoc.pdf">
          <PDF source="Loan.pdf">
             <Bookmarks source="doc2" />
          </PDF>
       </PDF>
 </DDX>
```

이 DCX 문서 내에서 source 속성에 값이 할당되어 `Loan.pdf`있습니다. 이 DDX 문서는 단일 PDF 문서를 어셈블러 서비스로 전달하도록 지정합니다. 책갈피가 있는 PDF 문서를 취합할 때는 결과 문서의 책갈피를 설명하는 책갈피 XML 문서를 지정해야 합니다. 책갈피 XML 문서를 지정하려면 DCX 문서에 `Bookmarks` 요소가 지정되어 있는지 확인합니다.

이 DCX 문서에서 `Bookmarks` 요소는 `doc2` 값으로 지정합니다. 이 값은 어셈블러 서비스로 전달된 입력 맵에 이름이 `doc2`있는 키가 포함되어 있음을 나타냅니다. 키 값은 `doc2` 책갈피 XML 문서를 나타내는 `com.adobe.idp.Document` 값입니다. 어셈블리 서비스 및 DCX [참조에서 &quot;책갈피 언어&quot;를 참조하십시오](https://www.adobe.com/go/learn_aemforms_ddx_63).

이 항목에서는 다음 XML 책갈피 언어를 사용하여 책갈피가 포함된 PDF 문서를 어셈블합니다.

```as3
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

이 책갈피 XML 문서 내에서 사용자가 책갈피를 클릭할 때 수행되는 작업을 정의하는 작업 요소를 확인합니다. 동작 요소 아래에는 NotePad와 같은 응용 프로그램을 실행하고 PDF 파일과 같은 파일을 여는 시작 요소가 있습니다. PDF 파일을 열려면 열 파일을 지정하는 파일 요소를 사용해야 합니다. 예를 들어 이 섹션에 지정된 책갈피 XML 파일에서 열려 있는 파일의 이름은 LoanDetails.pdf입니다.

>[!NOTE]
>
>지원되는 작업에 대한 자세한 내용은 어셈블러 서비스 및 DCX 참조에서 &quot; `Action` 요소&quot; [를 참조하십시오](https://www.adobe.com/go/learn_aemforms_ddx_63).

이 섹션에 지정된 DCX 문서와 XML 파일을 입력으로 책갈피로 지정한 경우 어셈블러 서비스는 다음 책갈피를 포함하는 PDF 문서를 어셈블합니다.

![aw_aw_bmark](assets/aw_aw_bmark.png)

사용자가 대출 세부 사항 *책갈피 열기를* 클릭하면 LoanDetails.pdf가 열립니다. 마찬가지로 사용자가 Launch NotePad *책갈피를 클릭하면* NotePad가 시작됩니다.

>[!NOTE]
>
>이 섹션을 읽기 전에 Assembler 서비스를 사용하여 PDF 문서를 조합하는 것에 익숙해지는 것이 좋습니다. 이 섹션에서는 입력 문서를 포함하는 컬렉션 개체를 만들거나 반환된 컬렉션 개체에서 결과를 추출하는 방법을 배우는 등의 개념에 대해서는 설명하지 않습니다. 자세한 내용은 [프로그래밍 방식으로 PDF 문서 작성을 참조하십시오](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents).

>[!NOTE]
>
>어셈블러 서비스에 대한 자세한 내용은 AEM Forms [에 대한 서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDX 문서에 대한 자세한 내용은 어셈블러 서비스 [및 DCX 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 단계 요약 {#summary-of-steps}

책갈피가 포함된 PDF 문서를 취합하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일 포함
1. PDF Assembler 클라이언트 만들기
1. 기존 DCX 문서를 참조합니다.
1. 책갈피가 추가되는 PDF 문서를 참조합니다.
1. 책갈피 XML 문서를 참조합니다.
1. PDF 문서와 책갈피 XML 문서를 Map 컬렉션에 추가합니다.
1. 런타임 옵션을 설정합니다.
1. PDF 문서 조합
1. 책갈피가 포함된 PDF 문서를 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

다음 JAR 파일을 프로젝트의 클래스 경로에 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (AEM Forms가 JBoss에 배포된 경우 필요)
* jbossall-client.jar(JBoss에 AEM Forms가 배포된 경우 필요)

aem Forms가 JBoss가 아닌 지원되는 J2EE 응용 프로그램 서버에 배포된 경우, adobe-utilities.jar 및 jbossall-client.jar 파일을 AEM Forms가 배포된 J2EE 응용 프로그램 서버에 고유한 JAR 파일로 교체해야 합니다. 모든 AEM Forms JAR 파일의 위치에 대한 자세한 내용은 AEM [Forms Java 라이브러리 파일](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)포함을 참조하십시오.

**PDF 어셈블러 클라이언트 만들기**

어셈블리 작업을 프로그래밍 방식으로 수행하려면 먼저 어셈블러 서비스 클라이언트를 만들어야 합니다.

**기존 DCX 문서 참조**

PDF 문서를 조합하려면 DCX 문서를 참조해야 합니다. 이 DDX 문서에는 책갈피가 포함된 PDF를 어셈블하는 데 필요한 `Bookmarks` 요소가 포함되어야 합니다. (예제는 이 섹션의 앞부분에 나와 있는 DCX 문서를 참조하십시오.)

**책갈피가 추가되는 PDF 문서 참조**

책갈피가 추가되는 PDF 문서를 참조합니다. 참조된 PDF 문서에 책갈피가 이미 포함되어 있는지 여부는 중요하지 않습니다. 요소가 PDF 소스 `Bookmarks` 요소의 하위 요소인 경우 책갈피는 PDF 소스에 이미 존재하는 요소를 대체합니다. 그러나 기존 책갈피를 유지하려면 PDF 소스 요소의 동위 `Bookmarks` 항목인지 확인하십시오. 예를 들어 다음 예를 생각해 보십시오.

```as3
 <PDF result="foo">
      <PDF source="inDoc"/>
      <Bookmarks source="doc2"/>
 </PDF>
```

**책갈피 XML 문서 참조**

새 책갈피가 포함된 PDF를 취합하려면 책갈피 XML 문서를 참조해야 합니다. 책갈피 XML 문서는 Map 컬렉션 개체 내의 어셈블러 서비스로 전달됩니다. (예제는 이 섹션 앞에 표시된 책갈피 XML 문서를 참조하십시오.)

>[!NOTE]
>
>어셈블리 서비스 및 DCX [참조에서 &quot;책갈피 언어&quot;를 참조하십시오](https://www.adobe.com/go/learn_aemforms_ddx_63).

**PDF 문서와 책갈피 XML 문서를 Map 컬렉션에 추가**

책갈피가 추가되는 PDF 문서와 책갈피 XML 문서를 Map 컬렉션에 모두 추가해야 합니다. 따라서 맵 컬렉션 개체에는 두 가지 요소가 포함되어 있습니다.pdf 문서 및 책갈피 XML 문서

**런타임 옵션 설정**

작업을 수행하는 동안 어셈블러 서비스의 동작을 제어하는 런타임 옵션을 설정할 수 있습니다. 예를 들어 오류가 발생하면 어셈블리 서비스에서 작업을 계속 처리하도록 하는 옵션을 설정할 수 있습니다. 설정할 수 있는 런타임 옵션에 대한 자세한 내용은 AEM Forms API 참조에서 `AssemblerOptionSpec` 클래스 [참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**PDF 문서 조합**

새 책갈피가 포함된 PDF 문서를 어셈블하려면 Assembler 서비스의 `invokeDDX` 작업을 사용합니다. 이와 같은 다른 어셈블러 서비스 작업과 반대되는 `invokeDDX` `invokeOneDocument` 작업을 사용해야 하는 이유는 어셈블러 서비스에서 Map 수집 개체 내에서 전달되는 책갈피 XML 문서가 필요하기 때문입니다. 이 개체는 `invokeDDX` 작업의 매개 변수입니다.

**책갈피가 포함된 PDF 문서 저장**

반환된 맵 개체에서 결과를 추출하고 해당 PDF 문서를 저장해야 합니다. 자세한 내용은 프로그래밍 방식으로 PDF 문서 [취합 시 &quot;결과 추출&quot;을 참조하십시오](/help/forms/developing/programmatically-assembling-pdf-documents.md).

**참고 항목**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[프로그래밍 방식으로 PDF 문서 취합](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API를 사용하여 책갈피로 PDF 문서 취합 {#assemble-pdf-documents-with-bookmarks-using-the-java-api}

Assembler Service API(Java)를 사용하여 책갈피와 함께 PDF 문서를 어셈블합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-assembler-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. PDF Assembler 클라이언트 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다. 연결 [속성](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)설정을 참조하십시오.
   * 생성자를 사용하여 객체를 전달하여 `AssemblerServiceClient` 객체를 만듭니다 `ServiceClientFactory` .

1. 기존 DCX 문서를 참조합니다.

   * 생성자를 사용하고 DCX 파일의 위치를 지정하는 문자열 값을 전달하여 DCX 문서를 나타내는 `java.io.FileInputStream` 객체를 만듭니다.
   * 생성자를 사용하여 객체를 전달하여 `com.adobe.idp.Document` 객체를 만듭니다 `java.io.FileInputStream` .

1. 책갈피가 추가되는 PDF 문서를 참조합니다.

   * 생성자를 사용하여 PDF 문서의 위치를 전달하여 `java.io.FileInputStream` 개체를 만듭니다.
   * 생성자를 사용하여 `com.adobe.idp.Document` 개체를 만들고 PDF 문서가 포함된 `java.io.FileInputStream` 개체를 전달합니다.

1. 책갈피 XML 문서를 참조합니다.

   * 생성자를 사용하여 `java.io.FileInputStream` 객체를 만들고 책갈피 XML 문서를 나타내는 XML 파일의 위치를 전달하여 객체를 만듭니다.
   * 개체를 `com.adobe.idp.Document` 만들고 PDF 문서가 포함된 `java.io.FileInputStream` 개체를 전달합니다.

1. PDF 문서와 책갈피 XML 문서를 Map 컬렉션에 추가합니다.

   * 입력 PDF 문서와 책갈피 XML 문서를 모두 저장하는 데 사용되는 `java.util.Map` 개체를 만듭니다.
   * 입력 PDF 문서를 `java.util.Map` 개체의 `put` 메서드를 호출하고 다음 인수를 전달하여 추가합니다.

      * 키 이름을 나타내는 문자열 값입니다. 이 값은 DCX 문서에 지정된 PDF 소스 요소의 값과 일치해야 합니다.
      * 입력 PDF 문서를 포함하는 `com.adobe.idp.Document` 개체입니다.
   * 개체의 `java.util.Map` `put` 메서드를 호출하고 다음 인수를 전달하여 책갈피 XML 문서를 추가합니다.

      * 키 이름을 나타내는 문자열 값입니다. 이 값은 DCX 문서에 지정된 책갈피 소스 요소의 값과 일치해야 합니다.
      * 책갈피 XML 문서를 포함하는 `com.adobe.idp.Document` 개체입니다.


1. 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 런타임 옵션을 저장하는 `AssemblerOptionSpec` 객체를 만듭니다.
   * 객체에 속하는 메서드를 호출하여 비즈니스 요구 사항을 충족하도록 런타임 옵션을 `AssemblerOptionSpec` 설정합니다. 예를 들어 오류가 발생할 때 어셈블리 서비스에서 작업을 계속 처리하도록 하려면 `AssemblerOptionSpec` 개체의 `setFailOnError` 메서드를 호출하고 전달합니다 `false`.

1. PDF 문서 조합

   객체의 `AssemblerServiceClient` `invokeDDX` 메서드를 호출하고 다음 필수 값을 전달합니다.

   * 사용할 DCX 문서를 나타내는 `com.adobe.idp.Document` 개체
   * 입력 PDF 문서와 책갈피 XML 문서를 모두 포함하는 `java.util.Map` 개체입니다.
   * 기본 글꼴 및 작업 로그 수준을 비롯한 런타임 옵션을 지정하는 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 개체
   이 `invokeDDX` `com.adobe.livecycle.assembler.client.AssemblerResult` 메서드는 작업 결과와 발생한 예외를 포함하는 개체를 반환합니다.

1. 책갈피가 포함된 PDF 문서를 저장합니다.

   새로 만든 PDF 문서를 가져오려면 다음 작업을 수행하십시오.

   * 객체의 메서드를 `AssemblerResult` 호출합니다 `getDocuments` . 이렇게 하면 `java.util.Map` 개체가 반환됩니다.
   * 결과 개체를 찾을 때까지 `java.util.Map` `com.adobe.idp.Document` 개체를 반복합니다. DCX 문서에 지정된 PDF 결과 요소를 사용하여 문서를 가져올 수 있습니다.
   * PDF 문서를 추출하려면 `com.adobe.idp.Document` 개체의 `copyToFile` 방법을 불러옵니다.

**참고 항목**

[빠른 시작(SOAP 모드):Java API 파섹](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API 파섹 {#assemble-pdf-documents-with-bookmarks-using-the-web-service-api}

Assembler Service API(웹 서비스)를 사용하여 책갈피와 함께 PDF 문서를 어셈블합니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`Adobe

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

1. 기존 DCX 문서를 참조합니다.

   * 생성자를 사용하여 `BLOB` 객체를 만듭니다. 이 `BLOB` 개체는 DCX 문서를 저장하는 데 사용됩니다.
   * 생성자를 호출하고 DCX 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * 개체의 내용을 저장하는 바이트 배열을 `System.IO.FileStream` 만듭니다. 개체의 `System.IO.FileStream` `Length` 속성을 가져와 바이트 배열의 크기를 결정할 수 있습니다.
   * 객체의 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다. `System.IO.FileStream` `Read`
   * 바이트 배열의 내용으로 해당 `BLOB` `MTOM` 필드를 할당하여 개체를 채웁니다.

1. 책갈피가 추가되는 PDF 문서를 참조합니다.

   * 생성자를 사용하여 `BLOB` 객체를 만듭니다. 이 `BLOB` 개체는 입력 PDF를 저장하는 데 사용됩니다.
   * 생성자를 호출하고 입력 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * 개체의 내용을 저장하는 바이트 배열을 `System.IO.FileStream` 만듭니다. 개체의 `System.IO.FileStream` `Length` 속성을 가져와 바이트 배열의 크기를 결정할 수 있습니다.
   * 객체의 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다. `System.IO.FileStream` `Read`
   * 바이트 배열의 내용으로 해당 `BLOB` `MTOM` 필드를 할당하여 개체를 채웁니다.

1. 책갈피 XML 문서를 참조합니다.

   * 생성자를 사용하여 `BLOB` 객체를 만듭니다. 이 `BLOB` 개체는 책갈피 XML 문서를 저장하는 데 사용됩니다.
   * 생성자를 호출하고 입력 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * 개체의 내용을 저장하는 바이트 배열을 `System.IO.FileStream` 만듭니다. 개체의 `System.IO.FileStream` `Length` 속성을 가져와 바이트 배열의 크기를 결정할 수 있습니다.
   * 객체의 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다. `System.IO.FileStream` `Read`
   * 바이트 배열의 내용으로 해당 `BLOB` `MTOM` 필드를 할당하여 개체를 채웁니다.

1. PDF 문서와 책갈피 XML 문서를 Map 컬렉션에 추가합니다.

   * 객체를 `MyMapOf_xsd_string_To_xsd_anyType` 만듭니다. 이 컬렉션 개체는 입력 PDF 문서와 책갈피 XML 문서를 저장하는 데 사용됩니다.
   * 각 입력 PDF 문서와 책갈피 XML 문서에 대해 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체를 만듭니다.
   * 키 이름을 나타내는 문자열 값을 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체의 `key` 필드에 지정합니다. 이 값은 DCX 문서에 지정된 PDF 소스 요소의 값과 일치해야 합니다.
   * PDF 문서를 저장하는 `BLOB` 개체를 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체의 `value` 필드에 할당합니다.
   * 개체에 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체를 추가합니다 `MyMapOf_xsd_string_To_xsd_anyType` . 객체의 메서드를 호출하고 `MyMapOf_xsd_string_To_xsd_anyType` `Add` `MyMapOf_xsd_string_To_xsd_anyType` 객체를 전달합니다. 각 입력 PDF 문서 및 책갈피 XML 문서에 대해 이 작업을 수행합니다.

1. 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 런타임 옵션을 저장하는 `AssemblerOptionSpec` 객체를 만듭니다.
   * 객체에 속하는 데이터 멤버에 값을 할당하여 비즈니스 요구 사항에 맞게 런타임 옵션을 설정할 수 `AssemblerOptionSpec` 있습니다. 예를 들어 오류가 발생할 때 어셈블리 서비스에서 작업을 계속 처리하도록 하려면 개체의 `false` `AssemblerOptionSpec` `failOnError` 데이터 멤버에 할당합니다.

1. PDF 문서 조합

   객체의 `AssemblerServiceClient` `invokeDDX` 메서드를 호출하고 다음 값을 전달합니다.

   * DCX 문서를 나타내는 `BLOB` 개체
   * 입력 문서를 포함하는 `MyMapOf_xsd_string_To_xsd_anyType` 배열
   * 런타임 옵션을 지정하는 `AssemblerOptionSpec` 개체
   이 `invokeDDX` 메서드는 작업 결과와 발생한 예외를 포함하는 `AssemblerResult` 객체를 반환합니다.

1. 책갈피가 포함된 PDF 문서를 저장합니다.

   새로 만든 PDF 문서를 가져오려면 다음 작업을 수행하십시오.

   * 결과 PDF 문서를 포함하는 `AssemblerResult` 개체인 개체의 `documents` `Map` 필드에 액세스합니다.
   * 결과 문서의 이름과 일치하는 키를 찾을 때까지 `Map` 개체를 반복합니다. 그런 다음 해당 어레이 멤버를 `value` a로 캐스팅합니다 `BLOB`.
   * PDF 문서를 나타내는 이진 데이터를 `BLOB` 개체 `MTOM` 필드에 액세스하여 추출합니다. PDF 파일에 쓸 수 있는 바이트 배열을 반환합니다.

**참고 항목**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
