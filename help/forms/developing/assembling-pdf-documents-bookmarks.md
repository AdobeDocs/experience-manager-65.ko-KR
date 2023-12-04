---
title: 책갈피로 PDF 문서 어셈블
seo-title: Assembling PDF Documents with Bookmarks
description: 어셈블러 서비스를 사용하여 Java API 및 웹 서비스 API를 사용하여 책갈피가 포함된 PDF 문서를 수정할 수 있습니다.
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
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '2519'
ht-degree: 0%

---

# 책갈피로 PDF 문서 어셈블 {#assembling-pdf-documents-with-bookmarks}

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms에 대해서만 적용됩니다.**

책갈피가 포함된 PDF 문서를 조합할 수 있습니다. 예를 들어, 책갈피가 포함되지 않은 PDF 문서가 있고 책갈피를 제공하여 수정하려는 경우, 어셈블러 서비스를 사용하면 책갈피가 포함되지 않은 PDF 문서를 전달하고 책갈피가 포함된 PDF 문서를 다시 가져올 수 있습니다.

책갈피에는 다음 속성이 포함되어 있습니다.

* 화면에 텍스트로 표시되는 제목입니다.
* 사용자가 책갈피를 클릭할 때 수행되는 작업을 지정하는 작업입니다. 책갈피에 대한 일반적인 작업은 다른 작업을 지정할 수 있지만 현재 문서의 다른 위치로 이동하거나 다른 PDF 문서를 여는 것입니다.

이러한 논의를 위해 다음과 같은 DDX 문서가 사용된다고 가정하자.

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

이 DDX 문서 내에서 소스 속성에 값이 할당됩니다 `Loan.pdf`. 이 DDX 문서는 하나의 PDF 문서가 어셈블러 서비스에 전달되도록 지정합니다. 책갈피로 PDF 문서를 어셈블할 때는 결과 문서에 책갈피를 설명하는 책갈피 XML 문서를 지정해야 합니다. 책갈피 XML 문서를 지정하려면 `Bookmarks` 요소는 DDX 문서에 지정됩니다.

이 예제 DDX 문서에서는 `Bookmarks` 요소가 다음을 지정합니다. `doc2` 을 값으로 추가합니다. 이 값은 어셈블러 서비스에 전달된 입력 맵에 라는 키가 포함되어 있음을 나타냅니다 `doc2`. 값 `doc2` 키가 `com.adobe.idp.Document` 책갈피 XML 문서를 나타내는 값입니다. ( 의 &quot;책갈피 언어&quot; 참조) [어셈블러 서비스 및 DDX 참조](https://www.adobe.com/go/learn_aemforms_ddx_63).)

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

이 책갈피 XML 문서 내에서 사용자가 책갈피를 클릭할 때 수행되는 작업을 정의하는 Action 요소를 확인합니다. Action 요소 아래에는 NotePad와 같은 응용 프로그램을 시작하고 PDF 파일과 같은 파일을 여는 Launch 요소가 있습니다. PDF 파일을 열려면 열 파일을 지정하는 File 요소를 사용해야 합니다. 예를 들어 이 섹션에 지정된 책갈피 XML 파일에서 열려 있는 파일의 이름은 LoanDetails.pdf입니다.

>[!NOTE]
>
>지원되는 작업에 대한 자세한 내용은 &quot; `Action` 의 &quot;element&quot; [어셈블러 서비스 및 DDX 참조](https://www.adobe.com/go/learn_aemforms_ddx_63).

이 섹션에 지정된 DDX 문서와 책갈피 XML 파일을 입력하면 어셈블러 서비스는 다음 책갈피가 포함된 PDF 문서를 어셈블합니다.

![aw_aw_bmark](assets/aw_aw_bmark.png)

사용자가 *대출 세부 정보 열기* 책갈피에 LoanDetails.pdf가 열립니다. 마찬가지로, 사용자가 *메모장 실행* 책갈피, NotePad가 시작되었습니다.

>[!NOTE]
>
>이 섹션을 읽기 전에 어셈블러 서비스를 사용하는 PDF 문서 어셈블링에 익숙해지는 것이 좋습니다. 이 섹션에서는 입력 문서가 포함된 컬렉션 객체 작성이나 반환된 컬렉션 객체에서 결과를 추출하는 방법에 대한 학습과 같은 개념에 대해서는 다루지 않습니다. (참조: [프로그래밍 방식으로 PDF 문서 어셈블](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents).)

>[!NOTE]
>
>어셈블러 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDX 문서에 대한 자세한 내용은 [어셈블러 서비스 및 DDX 참조](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 단계 요약 {#summary-of-steps}

책갈피가 포함된 PDF 문서를 어셈블하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. PDF 어셈블러 클라이언트를 만듭니다.
1. 기존 DDX 문서를 참조합니다.
1. 책갈피가 추가되는 PDF 문서를 참조합니다.
1. 책갈피 XML 문서를 참조하십시오.
1. PDF 문서와 책갈피 XML 문서를 맵 컬렉션에 추가합니다.
1. 런타임 옵션을 설정합니다.
1. PDF 문서를 어셈블합니다.
1. 책갈피가 포함된 PDF 문서를 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필수)

AEM Forms이 JBoss 이외의 지원되는 J2EE 애플리케이션 서버에 배포된 경우 adobe-utilities.jar 및 jbossall-client.jar 파일을 AEM Forms이 배포된 J2EE 애플리케이션 서버에 관련된 JAR 파일로 교체해야 합니다. 모든 AEM Forms JAR 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**PDF 어셈블러 클라이언트 만들기**

어셈블러 작업을 프로그래밍 방식으로 수행하려면 먼저 어셈블러 서비스 클라이언트를 만들어야 합니다.

**기존 DDX 문서 참조**

PDF 문서를 어셈블하려면 DDX 문서를 참조해야 합니다. 이 DDX 문서에는 `Bookmarks` 요소: 어셈블러 서비스에 책갈피가 포함된 PDF을 어셈블하도록 지시합니다. (예제는 이 섹션의 앞에 표시된 DDX 문서 를 참조하십시오.)

**책갈피가 추가되는 PDF 문서 참조**

책갈피가 추가되는 PDF 문서를 참조합니다. 참조된 PDF 문서에 이미 책갈피가 포함되어 있는지 여부는 중요하지 않습니다. 다음과 같은 경우 `Bookmarks` 요소가 PDF 소스 요소의 하위 요소이면 책갈피가 PDF 소스에 이미 있는 책갈피를 대체합니다. 그러나 기존 책갈피를 유지하려면 다음을 확인하십시오 `Bookmarks` 는 PDF 소스 요소의 형제입니다. 예를 들어 다음 예를 생각해 보십시오.

```xml
 <PDF result="foo">
      <PDF source="inDoc"/>
      <Bookmarks source="doc2"/>
 </PDF>
```

**책갈피 XML 문서 참조**

새 책갈피가 포함된 PDF을 어셈블하려면 책갈피 XML 문서를 참조해야 합니다. 책갈피 XML 문서는 Map 컬렉션 개체 내의 어셈블러 서비스로 전달됩니다. 자세한 내용은 이 섹션의 앞에 표시된 책갈피 XML 문서를 참조하십시오.

>[!NOTE]
>
>에서 &quot;책갈피 언어&quot;를 참조하십시오. [어셈블러 서비스 및 DDX 참조](https://www.adobe.com/go/learn_aemforms_ddx_63).

**맵 컬렉션에 PDF 문서 및 책갈피 XML 문서 추가**

책갈피가 추가되는 PDF 문서와 책갈피 XML 문서를 모두 맵 컬렉션에 추가합니다. 따라서 맵 컬렉션 개체에는 PDF 문서와 책갈피 XML 문서의 두 요소가 포함됩니다.

**런타임 옵션 설정**

작업을 수행하는 동안 어셈블러 서비스의 동작을 제어하는 런타임 옵션을 설정할 수 있습니다. 예를 들어 오류가 발생하는 경우 어셈블러 서비스에서 작업 처리를 계속하도록 지시하는 옵션을 설정할 수 있습니다. 설정할 수 있는 런타임 옵션에 대한 자세한 내용은 `AssemblerOptionSpec` 의 클래스 참조 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**PDF 문서를 어셈블합니다.**

새 책갈피가 포함된 PDF 문서를 어셈블하려면 어셈블러 서비스의 `invokeDDX` 작업. 를 사용해야 하는 이유 `invokeDDX` 과 같은 다른 어셈블러 서비스 작업과 대조되는 작업 `invokeOneDocument` 어셈블러 서비스에는 Map 컬렉션 개체 내에 전달되는 책갈피 XML 문서가 필요하기 때문입니다. 이 개체는 의 매개 변수입니다. `invokeDDX` 작업.

**책갈피가 포함된 PDF 문서 저장**

반환된 맵 개체에서 결과를 추출하고 해당 PDF 문서를 저장합니다. (&quot;결과 추출&quot; 참조) [프로그래밍 방식으로 PDF 문서 어셈블](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[프로그래밍 방식으로 PDF 문서 어셈블](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API를 사용하여 PDF 문서를 책갈피와 조합합니다. {#assemble-pdf-documents-with-bookmarks-using-the-java-api}

어셈블러 서비스 API(Java)를 사용하여 PDF 문서를 책갈피와 어셈블합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-assembler-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. PDF 어셈블러 클라이언트를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다. (참조: [연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * 만들기 `AssemblerServiceClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체.

1. 기존 DDX 문서를 참조합니다.

   * 만들기 `java.io.FileInputStream` 생성자를 사용하고 DDX 파일의 위치를 지정하는 문자열 값을 전달하여 DDX 문서를 나타내는 개체입니다.
   * 만들기 `com.adobe.idp.Document` 개체를 생성자를 사용하고 `java.io.FileInputStream` 개체.

1. 책갈피가 추가되는 PDF 문서를 참조합니다.

   * 만들기 `java.io.FileInputStream` 을 사용하여 개체를 만들고 PDF 문서의 위치를 전달합니다.
   * 만들기 `com.adobe.idp.Document` 개체를 생성자를 사용하여 만들고 `java.io.FileInputStream` PDF 문서가 포함된 객체입니다.

1. 책갈피 XML 문서를 참조하십시오.

   * 만들기 `java.io.FileInputStream` 객체를 만들 때 해당 생성자를 사용하고 책갈피 XML 문서를 나타내는 XML 파일의 위치를 전달합니다.
   * 만들기 `com.adobe.idp.Document` 개체 및 전달 `java.io.FileInputStream` PDF 문서가 포함된 객체입니다.

1. PDF 문서와 책갈피 XML 문서를 맵 컬렉션에 추가합니다.

   * 만들기 `java.util.Map` 입력 PDF 문서와 책갈피 XML 문서를 모두 저장하는 데 사용되는 개체입니다.
   * 다음을 호출하여 입력 PDF 문서 추가 `java.util.Map` 개체 `put` 메서드 및 다음 인수 전달:

      * 키 이름을 나타내는 문자열 값입니다. 이 값은 DDX 문서에 지정된 PDF 원본 요소의 값과 일치해야 합니다.
      * A `com.adobe.idp.Document` 입력 PDF 문서가 포함된 개체입니다.

   * 를 호출하여 책갈피 XML 문서를 추가합니다. `java.util.Map` 개체 `put` 메서드 및 다음 인수 전달:

      * 키 이름을 나타내는 문자열 값입니다. 이 값은 DDX 문서에 지정된 책갈피 소스 요소의 값과 일치해야 합니다.
      * A `com.adobe.idp.Document` 책갈피 XML 문서가 포함된 개체입니다.

1. 런타임 옵션을 설정합니다.

   * 만들기 `AssemblerOptionSpec` 생성자를 사용하여 런타임 옵션을 저장하는 개체입니다.
   * 에 속한 메서드를 호출하여 비즈니스 요구 사항을 충족하도록 런타임 옵션을 설정합니다. `AssemblerOptionSpec` 개체. 예를 들어 오류가 발생할 때 어셈블러 서비스에서 작업 처리를 계속하도록 하려면 `AssemblerOptionSpec` 개체 `setFailOnError` 방법 및 통과 `false`.

1. PDF 문서를 어셈블합니다.

   호출 `AssemblerServiceClient` 개체 `invokeDDX` 메서드를 실행하고 다음 필수 값을 전달합니다.

   * A `com.adobe.idp.Document` 사용할 DDX 문서를 나타내는 개체입니다
   * A `java.util.Map` 입력 PDF 문서와 책갈피 XML 문서를 모두 포함하는 객체입니다.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 기본 글꼴 및 작업 로그 수준을 포함하여 런타임 옵션을 지정하는 개체

   다음 `invokeDDX` 메서드가 을 반환합니다. `com.adobe.livecycle.assembler.client.AssemblerResult` 작업의 결과와 발생한 예외를 포함하는 객체입니다.

1. 책갈피가 포함된 PDF 문서를 저장합니다.

   새로 만든 PDF 문서를 가져오려면 다음 작업을 수행합니다.

   * 호출 `AssemblerResult` 개체 `getDocuments` 메서드를 사용합니다. 이 값은 `java.util.Map` 개체.
   * 다음을 반복합니다. `java.util.Map` 결과를 찾을 때까지 오브젝트 `com.adobe.idp.Document` 개체. (DDX 문서에 지정된 PDF 결과 요소를 사용하여 문서를 가져올 수 있습니다.)
   * 호출 `com.adobe.idp.Document` 개체 `copyToFile` PDF 문서를 추출하는 방법입니다.

**추가 참조**

[빠른 시작(SOAP 모드): Java API를 사용하여 책갈피로 PDF 문서 어셈블](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API를 사용하여 PDF 문서를 책갈피와 조합합니다. {#assemble-pdf-documents-with-bookmarks-using-the-web-service-api}

어셈블러 서비스 API(웹 서비스)를 사용하여 PDF 문서를 책갈피와 어셈블합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용하는지 확인합니다. `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` AEM Forms을 호스팅하는 서버의 IP 주소입니다.

1. PDF 어셈블러 클라이언트를 만듭니다.

   * 만들기 `AssemblerServiceClient` 기본 생성자를 사용하여 개체를 작성합니다.
   * 만들기 `AssemblerServiceClient.Endpoint.Address` 을 사용하여 개체 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). 를 사용할 필요가 없습니다. `lc_version` 특성. 이 속성은 서비스 참조를 만들 때 사용됩니다.
   * 만들기 `System.ServiceModel.BasicHttpBinding` 의 값을 가져와서 개체 `AssemblerServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스트 `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름 할당 `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * 해당 암호 값을 필드에 할당합니다. `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 지정 `HttpClientCredentialType.Basic` 필드에 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 상수 값 지정 `BasicHttpSecurityMode.TransportCredentialOnly` 필드에 `BasicHttpBindingSecurity.Security.Mode`.

1. 기존 DDX 문서를 참조합니다.

   * 만들기 `BLOB` 개체를 만들 때 사용됩니다. 다음 `BLOB` 개체는 DDX 문서를 저장하는 데 사용됩니다.
   * 만들기 `System.IO.FileStream` 이 개체는 생성자를 호출하고 DDX 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 콘텐츠를 저장하는 바이트 배열 만들기 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채우기 `System.IO.FileStream` 개체 `Read` 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하는 방법.
   * 채우기 `BLOB` 개체 할당 `MTOM` 바이트 배열의 내용이 있는 필드입니다.

1. 책갈피가 추가되는 PDF 문서를 참조합니다.

   * 만들기 `BLOB` 개체를 만들 때 사용됩니다. 다음 `BLOB` 개체를 사용하여 입력 PDF을 저장합니다.
   * 만들기 `System.IO.FileStream` 개체를 호출하고 입력 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 콘텐츠를 저장하는 바이트 배열 만들기 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채우기 `System.IO.FileStream` 개체 `Read` 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하는 방법.
   * 채우기 `BLOB` 개체 할당 `MTOM` 바이트 배열의 내용이 있는 필드입니다.

1. 책갈피 XML 문서를 참조하십시오.

   * 만들기 `BLOB` 개체를 만들 때 사용됩니다. 다음 `BLOB` 개체를 사용하여 책갈피 XML 문서를 저장합니다.
   * 만들기 `System.IO.FileStream` 개체를 호출하고 입력 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 콘텐츠를 저장하는 바이트 배열 만들기 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채우기 `System.IO.FileStream` 개체 `Read` 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하는 방법.
   * 채우기 `BLOB` 개체 할당 `MTOM` 바이트 배열의 내용이 있는 필드입니다.

1. PDF 문서와 책갈피 XML 문서를 맵 컬렉션에 추가합니다.

   * 만들기 `MyMapOf_xsd_string_To_xsd_anyType` 개체. 이 컬렉션 개체는 입력 PDF 문서와 책갈피 XML 문서를 저장하는 데 사용됩니다.
   * 각 입력 PDF 문서 및 책갈피 XML 문서에 대해 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체.
   * 키 이름을 나타내는 문자열 값을 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체 `key` 필드. 이 값은 DDX 문서에 지정된 PDF 원본 요소의 값과 일치해야 합니다.
   * 할당 `BLOB` 에 PDF 문서를 저장하는 개체 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체 `value` 필드.
   * 추가 `MyMapOf_xsd_string_To_xsd_anyType_Item` 에 대한 오브젝트 `MyMapOf_xsd_string_To_xsd_anyType` 개체. 호출 `MyMapOf_xsd_string_To_xsd_anyType` 개체 `Add` 메서드 및 전달 `MyMapOf_xsd_string_To_xsd_anyType` 개체. 각 입력 PDF 문서 및 책갈피 XML 문서에 대해 이 작업을 수행합니다.

1. 런타임 옵션을 설정합니다.

   * 만들기 `AssemblerOptionSpec` 생성자를 사용하여 런타임 옵션을 저장하는 개체입니다.
   * 에 속한 데이터 멤버에 값을 할당하여 비즈니스 요구 사항을 충족하는 런타임 옵션을 설정합니다. `AssemblerOptionSpec` 개체. 예를 들어 오류가 발생할 때 어셈블러 서비스에서 작업 처리를 계속하도록 하려면 다음을 할당합니다 `false` (으)로 `AssemblerOptionSpec` 개체 `failOnError` 데이터 구성원입니다.

1. PDF 문서를 어셈블합니다.

   호출 `AssemblerServiceClient` 개체 `invokeDDX` 메서드를 실행하고 다음 값을 전달합니다.

   * A `BLOB` DDX 문서를 나타내는 개체입니다
   * 다음 `MyMapOf_xsd_string_To_xsd_anyType` 입력 문서가 포함된 배열
   * An `AssemblerOptionSpec` 런타임 옵션을 지정하는 개체입니다

   다음 `invokeDDX` 메서드가 다음을 반환합니다. `AssemblerResult` 작업의 결과와 발생했을 수 있는 예외를 포함하는 객체입니다.

1. 책갈피가 포함된 PDF 문서를 저장합니다.

   새로 만든 PDF 문서를 가져오려면 다음 작업을 수행합니다.

   * 액세스 `AssemblerResult` 개체 `documents` 필드: `Map` 결과 PDF 문서가 포함된 객체입니다.
   * 다음을 반복합니다. `Map` 결과 문서의 이름과 일치하는 키를 찾을 때까지 객체를 검색합니다. 그런 다음 해당 배열 멤버의 `value` (으)로 `BLOB`.
   * 에 액세스하여 PDF 문서를 나타내는 이진 데이터 추출 `BLOB` 개체 `MTOM` 필드. PDF 파일에 쓸 수 있는 바이트 배열이 반환됩니다.

**추가 참조**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
