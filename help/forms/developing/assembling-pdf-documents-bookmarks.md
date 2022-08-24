---
title: 책갈피를 사용하여 PDF 문서 조립
seo-title: Assembling PDF Documents with Bookmarks
description: 어셈블러 서비스를 사용하여 Java API 및 웹 서비스 API를 사용하여 책갈피를 포함하도록 책갈피가 포함된 PDF 문서를 수정합니다.
seo-description: Use the Assembler service to modify a PDF document that does contain bookmarks to include bookmarks using the Java API and the Web Service API.
uuid: a306d2a6-0b12-4eb3-bff4-968a33417486
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f4711a8-033c-4051-ab41-65a26838899b
role: Developer
exl-id: 2b938410-f51b-420b-b5d4-2ed13ec29c5a
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '2558'
ht-degree: 0%

---

# 책갈피를 사용하여 PDF 문서 조립 {#assembling-pdf-documents-with-bookmarks}

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms용입니다.**

책갈피가 포함된 PDF 문서를 어셈블할 수 있습니다. 예를 들어 책갈피를 포함하지 않는 PDF 문서가 있고 책갈피를 제공하여 수정하려고 한다고 가정합니다. 어셈블러 서비스를 사용하여 책갈피가 포함되지 않은 PDF 문서에 전달하고 책갈피가 포함된 PDF 문서를 다시 가져올 수 있습니다.

책갈피에는 다음 속성이 포함됩니다.

* 화면에 텍스트로 표시되는 제목입니다.
* 사용자가 책갈피를 클릭할 때 발생하는 작업을 지정하는 작업입니다. 책갈피에 대한 일반적인 작업은 다른 작업을 지정할 수 있지만 현재 문서의 다른 위치로 이동하거나 다른 PDF 문서를 여는 것입니다.

이 토론을 위해 다음 DDX 문서가 사용된다고 가정하십시오.

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

이 DDX 문서 내에서 소스 속성에 값이 할당되었음을 알 수 있습니다 `Loan.pdf`. 이 DDX 문서는 단일 PDF 문서가 어셈블러 서비스로 전달되도록 지정합니다. PDF 문서를 책갈피로 어셈블할 때는 결과 문서의 책갈피를 설명하는 책갈피 XML 문서를 지정해야 합니다. 책갈피 XML 문서를 지정하려면 `Bookmarks` 요소가 DDX 문서에 지정됩니다.

이 DDX 문서에서, `Bookmarks` 요소 지정 `doc2` 를 값으로 채우는 방법을 설명합니다. 이 값은 어셈블러 서비스에 전달된 입력 맵에 이름이 지정된 키가 포함되어 있음을 나타냅니다 `doc2`. 의 값 `doc2` 키는 `com.adobe.idp.Document` 책갈피 XML 문서를 나타내는 값입니다. 자세한 내용은 [어셈블러 서비스 및 DDX 참조](https://www.adobe.com/go/learn_aemforms_ddx_63))

이 항목에서는 다음 XML 책갈피 언어를 사용하여 책갈피가 포함된 PDF 문서를 어셈블합니다.

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

이 책갈피 XML 문서 내에서 사용자가 책갈피를 클릭할 때 수행되는 작업을 정의하는 작업 요소를 확인합니다. Action 요소 아래에 NotePad와 같은 응용 프로그램을 시작하고 PDF 파일과 같은 파일을 여는 Launch 요소가 있습니다. PDF 파일을 열려면 열 파일을 지정하는 File 요소를 사용해야 합니다. 예를 들어 이 섹션에 지정된 책갈피 XML 파일에서 열리는 파일의 이름은 LoanDetails.pdf입니다.

>[!NOTE]
>
>지원되는 작업에 대한 자세한 내용은 &quot; `Action` 요소의&quot; [어셈블러 서비스 및 DDX 참조](https://www.adobe.com/go/learn_aemforms_ddx_63).

이 섹션에 지정된 DDX 문서를 입력하고 XML 파일을 입력으로 책갈피로 지정하여 어셈블러 서비스는 다음 책갈피를 포함하는 PDF 문서를 어셈블합니다.

![aw_aw_bmark](assets/aw_aw_bmark.png)

사용자가 를 클릭하면 *대출 상세내역 열기* 책갈피에서 LoanDetails.pdf가 열립니다. 마찬가지로 사용자가 를 클릭할 때에도 *노트 패드 시작* 책갈피이면 NotePad가 시작됩니다.

>[!NOTE]
>
>이 섹션을 읽기 전에 어셈블러 서비스를 사용하여 PDF 문서 조립에 익숙해지는 것이 좋습니다. 이 섹션에서는 입력 문서가 포함된 컬렉션 개체를 만들거나 반환된 수집 개체에서 결과를 추출하는 방법을 학습하는 등의 개념을 다루지 않습니다. (자세한 내용은 [프로그래밍 방식으로 PDF 문서 조립](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents))

>[!NOTE]
>
>어셈블러 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDX 문서에 대한 자세한 내용은 [어셈블러 서비스 및 DDX 참조](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 단계 요약 {#summary-of-steps}

책갈피가 포함된 PDF 문서를 어셈블하려면 다음 작업을 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. PDF 어셈블러 클라이언트를 만듭니다.
1. 기존 DDX 문서를 참조합니다.
1. 책갈피가 추가되는 PDF 문서를 참조합니다.
1. 책갈피 XML 문서를 참조합니다.
1. PDF 문서와 책갈피 XML 문서를 Map 컬렉션에 추가합니다.
1. 런타임 옵션을 설정합니다.
1. PDF 문서를 어셈블합니다.
1. 책갈피가 포함된 PDF 문서를 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함하십시오. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms이 JBoss에 배포되는 경우 필요)

AEM Forms이 JBoss 이외의 지원되는 J2EE 애플리케이션 서버에 배포된 경우, adobe-utilities.jar 및 jbossall-client.jar 파일을 AEM Forms이 배포된 J2EE 애플리케이션 서버에 고유한 JAR 파일로 바꾸어야 합니다. 모든 AEM Forms JAR 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**PDF 어셈블러 클라이언트 만들기**

어셈블러 작업을 프로그래밍 방식으로 수행하려면 먼저 어셈블러 서비스 클라이언트를 만들어야 합니다.

**기존 DDX 문서 참조**

PDF 문서를 어셈블하려면 DDX 문서를 참조해야 합니다. 이 DDX 문서에는 `Bookmarks` 책갈피가 포함된 PDF을 어셈블하도록 어셈블러 서비스에 지시하는 요소입니다. 예를 보려면 이 섹션의 앞부분에 표시된 DDX 문서를 참조하십시오.

**책갈피가 추가되는 PDF 문서를 참조합니다**

책갈피가 추가되는 PDF 문서를 참조합니다. 참조된 PDF 문서에 책갈피가 이미 포함되어 있는지 여부는 중요하지 않습니다. 만약 `Bookmarks` 요소가 PDF 소스 요소의 하위 요소인 경우 책갈피는 PDF 소스에 이미 있는 책갈피를 대체합니다. 그러나 기존 책갈피를 유지하려면 `Bookmarks` 는 PDF 소스 요소의 동위 멤버입니다. 예를 들어 다음 예를 생각해 보십시오.

```xml
 <PDF result="foo">
      <PDF source="inDoc"/>
      <Bookmarks source="doc2"/>
 </PDF>
```

**책갈피 XML 문서 참조**

새 책갈피가 포함된 PDF을 어셈블하려면 책갈피 XML 문서를 참조해야 합니다. 책갈피 XML 문서가 맵 수집 개체 내의 어셈블러 서비스에 전달됩니다. 예를 보려면 이 섹션 앞에 표시된 책갈피 XML 문서를 참조하십시오.

>[!NOTE]
>
>에서 &quot;책갈피 언어&quot;를 참조하십시오 [어셈블러 서비스 및 DDX 참조](https://www.adobe.com/go/learn_aemforms_ddx_63).

**PDF 문서와 책갈피 XML 문서를 맵 컬렉션에 추가합니다**

책갈피가 추가되는 PDF 문서와 책갈피 XML 문서를 모두 맵 컬렉션에 추가해야 합니다. 따라서 맵 컬렉션 개체에는 두 가지 요소가 포함됩니다. PDF 문서와 책갈피 XML 문서입니다.

**런타임 옵션 설정**

작업을 수행하는 동안 어셈블러 서비스의 동작을 제어하는 런타임 옵션을 설정할 수 있습니다. 예를 들어 오류가 발생하면 어셈블러 서비스에 작업을 계속 처리하도록 지시하는 옵션을 설정할 수 있습니다. 설정할 수 있는 런타임 옵션에 대한 자세한 내용은 `AssemblerOptionSpec` 클래스 참조 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**PDF 문서 조합**

새 책갈피가 포함된 PDF 문서를 어셈블하려면 어셈블러 서비스의 `invokeDDX` 작업. 다음을 사용해야 하는 이유 `invokeDDX` 작업(예: `invokeOneDocument` 어셈블러 서비스에는 맵 수집 개체 내에 전달되는 책갈피 XML 문서가 필요하기 때문입니다. 이 개체는 `invokeDDX` 작업.

**책갈피가 포함된 PDF 문서를 저장합니다**

반환된 맵 개체에서 결과를 추출하고 해당 PDF 문서를 저장해야 합니다. 자세한 내용은 &quot;결과 추출&quot;을 참조하십시오. [프로그래밍 방식으로 PDF 문서 조립](/help/forms/developing/programmatically-assembling-pdf-documents.md))

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[프로그래밍 방식으로 PDF 문서 조립](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API를 사용하여 책갈피로 PDF 문서 조합 {#assemble-pdf-documents-with-bookmarks-using-the-java-api}

어셈블러 서비스 API(Java)를 사용하여 책갈피로 PDF 문서를 어셈블합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-assembler-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. PDF 어셈블러 클라이언트를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 객체입니다. (자세한 내용은 [연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties))
   * 만들기 `AssemblerServiceClient` 생성자를 사용하여 객체를 전달하고 `ServiceClientFactory` 개체.

1. 기존 DDX 문서를 참조합니다.

   * 만들기 `java.io.FileInputStream` 생성자를 사용하고 DDX 파일의 위치를 지정하는 문자열 값을 전달하여 DDX 문서를 나타내는 개체입니다.
   * 만들기 `com.adobe.idp.Document` 생성자를 사용하여 객체를 전달하고 `java.io.FileInputStream` 개체.

1. 책갈피가 추가되는 PDF 문서를 참조합니다.

   * 만들기 `java.io.FileInputStream` 생성자를 사용하여 PDF 문서의 위치를 전달하여 개체를 가져옵니다.
   * 만들기 `com.adobe.idp.Document` 생성자를 사용하여 객체를 전달하고 `java.io.FileInputStream` PDF 문서를 포함하는 객체입니다.

1. 책갈피 XML 문서를 참조합니다.

   * 만들기 `java.io.FileInputStream` 객체(object)를 생성자로 사용하여 책갈피 XML 문서를 나타내는 XML 파일의 위치를 전달합니다.
   * 만들기 `com.adobe.idp.Document` 개체 및 전달 `java.io.FileInputStream` PDF 문서를 포함하는 객체입니다.

1. PDF 문서와 책갈피 XML 문서를 Map 컬렉션에 추가합니다.

   * 만들기 `java.util.Map` 입력 PDF 문서와 책갈피 XML 문서를 모두 저장하는 데 사용되는 개체입니다.
   * 을 호출하여 입력 PDF 문서를 추가합니다 `java.util.Map` 개체 `put` 메서드와 다음 인수를 전달합니다.

      * 키 이름을 나타내는 문자열 값입니다. 이 값은 DDX 문서에 지정된 PDF 소스 요소의 값과 일치해야 합니다.
      * A `com.adobe.idp.Document` 입력 PDF 문서를 포함하는 객체입니다.
   * 책갈피 XML 문서를 `java.util.Map` 개체 `put` 메서드와 다음 인수를 전달합니다.

      * 키 이름을 나타내는 문자열 값입니다. 이 값은 DDX 문서에 지정된 책갈피 원본 요소의 값과 일치해야 합니다.
      * A `com.adobe.idp.Document` 책갈피 XML 문서가 포함된 객체입니다.


1. 런타임 옵션을 설정합니다.

   * 만들기 `AssemblerOptionSpec` 생성자를 사용하여 런타임 옵션을 저장하는 개체입니다.
   * 에 속한 메서드를 호출하여 비즈니스 요구 사항을 충족하도록 런타임 옵션을 설정합니다. `AssemblerOptionSpec` 개체. 예를 들어 오류가 발생할 때 어셈블러 서비스에서 작업을 계속 처리하도록 하려면 `AssemblerOptionSpec` 개체 `setFailOnError` 메서드 및 전달 `false`.

1. PDF 문서를 어셈블합니다.

   를 호출합니다 `AssemblerServiceClient` 개체 `invokeDDX` 메서드를 사용하여 다음 필수 값을 전달합니다.

   * A `com.adobe.idp.Document` 사용할 DDX 문서를 나타내는 객체
   * A `java.util.Map` 입력 PDF 문서와 책갈피 XML 문서를 모두 포함하는 객체입니다.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 기본 글꼴 및 작업 로그 레벨을 포함하여 런타임 옵션을 지정하는 객체

   다음 `invokeDDX` 메서드 반환 `com.adobe.livecycle.assembler.client.AssemblerResult` 작업의 결과와 발생한 예외를 포함하는 객체입니다.

1. 책갈피가 포함된 PDF 문서를 저장합니다.

   새로 만든 PDF 문서를 가져오려면 다음 작업을 수행하십시오.

   * 를 호출합니다 `AssemblerResult` 개체 `getDocuments` 메서드를 사용합니다. 이는 를 반환합니다 `java.util.Map` 개체.
   * 를 통해 반복 `java.util.Map` 결과를 찾을 때까지 객체 `com.adobe.idp.Document` 개체. DDX 문서에 지정된 PDF 결과 요소를 사용하여 문서를 가져올 수 있습니다.
   * 를 호출합니다 `com.adobe.idp.Document` 개체 `copyToFile` PDF 문서를 추출하는 방법입니다.

**추가 참조**

[빠른 시작(SOAP 모드): Java API를 사용하여 PDF 문서를 책갈피로 어셈블하기](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API를 사용하여 책갈피로 PDF 문서 조합 {#assemble-pdf-documents-with-bookmarks-using-the-web-service-api}

어셈블러 서비스 API(웹 서비스)를 사용하여 책갈피로 PDF 문서를 어셈블합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

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

1. 기존 DDX 문서를 참조합니다.

   * 만들기 `BLOB` 생성자를 사용하여 개체를 작성합니다. 다음 `BLOB` 객체는 DDX 문서를 저장하는 데 사용됩니다.
   * 만들기 `System.IO.FileStream` 객체를 사용하여 해당 생성자를 호출하고 DDX 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 내용을 저장하는 바이트 배열을 만듭니다 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성을 사용합니다.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채웁니다 `System.IO.FileStream` 개체 `Read` 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하는 메서드와 전달
   * 을(를) 채우기 `BLOB` 개체를 할당하여 개체를 개체 개체 `MTOM` 바이트 배열의 내용을 포함하는 필드입니다.

1. 책갈피가 추가되는 PDF 문서를 참조합니다.

   * 만들기 `BLOB` 생성자를 사용하여 개체를 작성합니다. 다음 `BLOB` 입력 PDF을 저장하는 데 개체가 사용됩니다.
   * 만들기 `System.IO.FileStream` 객체를 사용하여 생성자를 호출하고 입력 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 내용을 저장하는 바이트 배열을 만듭니다 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성을 사용합니다.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채웁니다 `System.IO.FileStream` 개체 `Read` 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하는 메서드와 전달
   * 을(를) 채우기 `BLOB` 개체를 할당하여 개체를 개체 개체 `MTOM` 바이트 배열의 내용을 포함하는 필드입니다.

1. 책갈피 XML 문서를 참조합니다.

   * 만들기 `BLOB` 생성자를 사용하여 개체를 작성합니다. 다음 `BLOB` 책갈피 XML 문서를 저장하는 데 사용됩니다.
   * 만들기 `System.IO.FileStream` 객체를 사용하여 생성자를 호출하고 입력 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 내용을 저장하는 바이트 배열을 만듭니다 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성을 사용합니다.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채웁니다 `System.IO.FileStream` 개체 `Read` 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하는 메서드와 전달
   * 을(를) 채우기 `BLOB` 개체를 할당하여 개체를 개체 개체 `MTOM` 바이트 배열의 내용을 포함하는 필드입니다.

1. PDF 문서와 책갈피 XML 문서를 Map 컬렉션에 추가합니다.

   * 만들기 `MyMapOf_xsd_string_To_xsd_anyType` 개체. 이 수집 객체는 입력 PDF 문서와 책갈피 XML 문서를 저장하는 데 사용됩니다.
   * 각 입력 PDF 문서 및 책갈피 XML 문서에 대해 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체.
   * 키 이름을 나타내는 문자열 값을 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체 `key` 필드. 이 값은 DDX 문서에 지정된 PDF 소스 요소의 값과 일치해야 합니다.
   * 을(를) 지정합니다. `BLOB` PDF 문서를 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체 `value` 필드.
   * 추가 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체 `MyMapOf_xsd_string_To_xsd_anyType` 개체. 를 호출합니다 `MyMapOf_xsd_string_To_xsd_anyType` 개체 `Add` 메서드 및 전달 `MyMapOf_xsd_string_To_xsd_anyType` 개체. 각 입력 PDF 문서 및 책갈피 XML 문서에 대해 이 작업을 수행합니다.

1. 런타임 옵션을 설정합니다.

   * 만들기 `AssemblerOptionSpec` 생성자를 사용하여 런타임 옵션을 저장하는 개체입니다.
   * 비즈니스 요구 사항에 맞게 런타임 옵션을 설정하려면 `AssemblerOptionSpec` 개체. 예를 들어 오류가 발생할 때 어셈블러 서비스에서 작업을 계속 처리하도록 지시하려면 을 할당합니다. `false` 변환 후 `AssemblerOptionSpec` 개체 `failOnError` 데이터 멤버.

1. PDF 문서를 어셈블합니다.

   를 호출합니다 `AssemblerServiceClient` 개체 `invokeDDX` 메서드를 사용하여 다음 값을 전달합니다.

   * A `BLOB` DDX 문서를 나타내는 객체
   * 다음 `MyMapOf_xsd_string_To_xsd_anyType` 입력 문서가 포함된 배열
   * An `AssemblerOptionSpec` 런타임 옵션을 지정하는 객체

   다음 `invokeDDX` 메서드 반환 `AssemblerResult` 작업의 결과와 발생한 예외를 포함하는 객체입니다.

1. 책갈피가 포함된 PDF 문서를 저장합니다.

   새로 만든 PDF 문서를 가져오려면 다음 작업을 수행하십시오.

   * 액세스 권한 `AssemblerResult` 개체 `documents` 필드, 즉 `Map` 결과 PDF 문서를 포함하는 객체입니다.
   * 를 통해 반복 `Map` 결과 문서의 이름과 일치하는 키를 찾을 때까지 객체를 선택합니다. 그런 다음 해당 어레이 멤버의 `value` 변환 후 `BLOB`.
   * PDF 문서에 액세스하여 이진 데이터를 추출합니다 `BLOB` 개체 `MTOM` 필드. PDF 파일에 쓸 수 있는 바이트 배열을 반환합니다.

**추가 참조**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
