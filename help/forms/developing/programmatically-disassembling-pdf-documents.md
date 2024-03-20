---
title: 프로그래밍 방식으로 PDF 문서 디스어셈블
description: 어셈블러 서비스를 사용하여 Java API 및 웹 서비스 API를 사용하여 단일 PDF 문서를 여러 PDF 문서로 디스어셈블합니다.
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: c5e712e0-5c3f-48cd-91cf-fd347222a6b2
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1749'
ht-degree: 0%

---

# 프로그래밍 방식으로 PDF 문서 디스어셈블 {#programmatically-disassembling-pdf-documents}

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms에 대해서만 적용됩니다.**

PDF 문서를 어셈블러 서비스에 전달하여 디스어셈블할 수 있습니다. 일반적으로 이 작업은 명령문 모음과 같은 여러 개별 문서에서 PDF 문서를 원래 만든 경우에 유용합니다. 다음 그림에서 DocA는 여러 결과 문서로 나뉩니다. 여기서 페이지의 첫 번째 레벨 1 책갈피는 새 결과 문서의 시작을 나타냅니다.

![pd_pd_pdfsfrombookmark](assets/pd_pd_pdfsfrombookmarks.png)

PDF 문서를 디스어셈블하려면 `PDFsFromBookmarks` 요소가 DDX 문서에 있습니다. 다음 `PDFsFromBookmarks` element는 결과 요소이며 의 자식 요소일 수 있습니다. `DDX` 요소를 생성하지 않습니다. 에는 가 없습니다. `result` 여러 문서가 생성될 수 있으므로 특성입니다.

다음 `PDFsFromBookmarks` 요소를 사용하면 소스 문서의 레벨 1 책갈피마다 단일 문서가 생성됩니다.

이 논의에서 다음과 같은 DDX 문서가 사용된다고 가정해 보겠습니다.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

>[!NOTE]
>
>이 섹션을 읽기 전에 어셈블러 서비스를 사용하여 PDF 문서를 어셈블하는 방법을 잘 알고 있는 것이 좋습니다. (참조: [프로그래밍 방식으로 PDF 문서 어셈블](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

>[!NOTE]
>
>어셈블러 서비스에 단일 PDF 문서를 전달하고 단일 문서를 다시 가져올 때 `invokeOneDocument` 작업. 그러나 PDF 문서를 디스어셈블하려면 `invokeDDX` 한 개의 입력 PDF 문서가 어셈블러 서비스에 전달되더라도 어셈블러 서비스는 하나 이상의 문서가 포함된 컬렉션 개체를 반환하므로 작업이 수행됩니다.

>[!NOTE]
>
>어셈블러 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDX 문서에 대한 자세한 내용은 [어셈블러 서비스 및 DDX 참조](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 단계 요약 {#summary-of-steps}

PDF 문서를 디스어셈블하려면 다음 작업을 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. PDF 어셈블러 클라이언트를 만듭니다.
1. 기존 DDX 문서를 참조합니다.
1. 분해하려면 PDF 문서를 참조합니다.
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

AEM Forms이 JBoss가 아닌 지원되는 J2EE 애플리케이션 서버에 배포된 경우 adobe-utilities.jar 및 jbossall-client.jar을 AEM Forms이 배포된 J2EE 애플리케이션 서버에 관련된 JAR 파일로 교체해야 합니다.

**PDF 어셈블러 클라이언트 만들기**

어셈블러 작업을 프로그래밍 방식으로 수행하려면 먼저 어셈블러 서비스 클라이언트를 만들어야 합니다.

**기존 DDX 문서 참조**

PDF 문서를 디스어셈블하려면 DDX 문서를 참조해야 합니다. 이 DDX 문서에는 `PDFsFromBookmarks` 요소를 생성하지 않습니다.

**분해할 PDF 문서 참조**

PDF 문서를 디스어셈블하려면 디스어셈블할 PDF 문서를 나타내는 PDF 파일을 참조합니다. 어셈블러 서비스로 전달되면 문서의 레벨 1 책갈피마다 별도의 PDF 문서가 반환됩니다.

**런타임 옵션 설정**

작업을 수행하는 동안 어셈블러 서비스의 동작을 제어하는 런타임 옵션을 설정할 수 있습니다. 예를 들어 오류가 발생하는 경우 어셈블러 서비스에서 작업 처리를 계속하도록 지시하는 옵션을 설정할 수 있습니다.

**PDF 문서를 디스어셈블합니다.**

어셈블러 서비스 클라이언트를 만들고, DDX 문서를 참조하고, PDF PDF 문서를 참조하여 디스어셈블하고, 런타임 옵션을 설정한 후에는 `invokeDDX` 메서드를 사용합니다. DDX 문서에 PDF 문서를 디스어셈블하는 지침이 포함되어 있으면 어셈블러 서비스는 컬렉션 개체 내에서 디스어셈블된 PDF 문서를 반환합니다.

**분해된 PDF 문서를 저장합니다.**

분해된 모든 PDF 문서는 컬렉션 개체 내에서 반환됩니다. 컬렉션 객체를 반복하고 각 PDF 문서를 PDF 파일로 저장합니다.

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[프로그래밍 방식으로 PDF 문서 어셈블](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API를 사용하여 PDF 문서 디스어셈블 {#disassemble-a-pdf-document-using-the-java-api}

어셈블러 서비스 API(Java)를 사용하여 PDF 문서를 디스어셈블합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-assembler-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. PDF 어셈블러 클라이언트를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.
   * 만들기 `AssemblerServiceClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체.

1. 기존 DDX 문서를 참조합니다.

   * 만들기 `java.io.FileInputStream` 생성자를 사용하고 DDX 파일의 위치를 지정하는 문자열 값을 전달하여 DDX 문서를 나타내는 개체입니다.
   * 만들기 `com.adobe.idp.Document` 개체를 생성자를 사용하고 `java.io.FileInputStream` 개체.

1. 분해하려면 PDF 문서를 참조합니다.

   * 만들기 `java.util.Map` 개체를 사용하여 입력 PDF 문서를 저장하는 데 사용됩니다 `HashMap` 생성자입니다.
   * 만들기 `java.io.FileInputStream` 개체를 만들 때 PDF 문서의 위치를 전달하여 어셈블리를 분리합니다.
   * 만들기 `com.adobe.idp.Document` 개체 및 전달 `java.io.FileInputStream` 분해할 PDF 문서가 포함된 객체입니다.
   * 에 항목 추가 `java.util.Map` 개체 `put` 메서드 및 다음 인수 전달:

      * 키 이름을 나타내는 문자열 값입니다. 이 값은 DDX 문서에 지정된 PDF 원본 요소의 값과 일치해야 합니다.
      * A `com.adobe.idp.Document` 분해할 PDF 문서가 포함된 객체입니다.

1. 런타임 옵션을 설정합니다.

   * 만들기 `AssemblerOptionSpec` 생성자를 사용하여 런타임 옵션을 저장하는 개체입니다.
   * 에 속한 메서드를 호출하여 비즈니스 요구 사항을 충족하도록 런타임 옵션을 설정합니다. `AssemblerOptionSpec` 개체. 예를 들어 오류가 발생할 때 어셈블러 서비스에서 작업 처리를 계속하도록 하려면 `AssemblerOptionSpec` 개체 `setFailOnError` 방법 및 통과 `false`.

1. PDF 문서를 디스어셈블합니다.

   호출 `AssemblerServiceClient` 개체 `invokeDDX` 메서드를 실행하고 다음 필수 값을 전달합니다.

   * A `com.adobe.idp.Document` 사용할 DDX 문서를 나타내는 개체입니다
   * A `java.util.Map` 분해할 PDF 문서가 포함된 개체
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 기본 글꼴 및 작업 로그 수준을 포함하여 런타임 옵션을 지정하는 개체입니다.

   다음 `invokeDDX` 메서드가 을 반환합니다. `com.adobe.livecycle.assembler.client.AssemblerResult` 분해된 PDF 문서 및 발생한 예외가 포함된 객체입니다.

1. 분해된 PDF 문서를 저장합니다.

   분해된 PDF 문서를 가져오려면 다음 작업을 수행합니다.

   * 호출 `AssemblerResult` 개체 `getDocuments` 메서드를 사용합니다. 이 값은 `java.util.Map` 개체.
   * 다음을 반복합니다. `java.util.Map` 결과를 찾을 때까지 오브젝트 `com.adobe.idp.Document` 개체.
   * 호출 `com.adobe.idp.Document` 개체 `copyToFile` PDF 문서를 추출하는 방법입니다.

**추가 참조**

[프로그래밍 방식으로 PDF 문서 디스어셈블](#programmatically-disassembling-pdf-documents)

[빠른 시작(SOAP 모드): Java API를 사용하여 PDF 문서 분해](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-disassembling-a-pdf-document-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API를 사용하여 PDF 문서 디스어셈블 {#disassemble-a-pdf-document-using-the-web-service-api}

어셈블러 서비스 API(웹 서비스)를 사용하여 PDF 문서를 디스어셈블합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 서비스 참조를 설정할 때 다음 WSDL 정의를 사용하는지 확인합니다. `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

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
   * 만들기 `System.IO.FileStream` 해당 생성자를 호출하여 개체를 작성합니다. DDX 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 콘텐츠를 저장하는 바이트 배열 만들기 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채우기 `System.IO.FileStream` 개체 `Read` 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하는 방법.
   * 채우기 `BLOB` 개체 할당 `MTOM` 속성을 바이트 배열의 콘텐츠와 함께 사용합니다.

1. 분해하려면 PDF 문서를 참조합니다.

   * 만들기 `BLOB` 개체를 만들 때 사용됩니다. 다음 `BLOB` 객체는 입력 PDF 문서를 저장하는 데 사용됩니다. 이 `BLOB` 개체가 로 전달됨 `invokeOneDocument` as a argument인수 .
   * 만들기 `System.IO.FileStream` 개체를 호출하고 입력 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 콘텐츠를 저장하는 바이트 배열 만들기 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채우기 `System.IO.FileStream` 개체 `Read` 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하는 방법.
   * 채우기 `BLOB` 개체 할당 `MTOM` 바이트 배열의 내용을 입력합니다.
   * 만들기 `MyMapOf_xsd_string_To_xsd_anyType` 개체. 이 컬렉션 개체는 분해할 PDF을 저장하는 데 사용됩니다.
   * 만들기 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체.
   * 키 이름을 나타내는 문자열 값을 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체 `key` 필드. 이 값은 DDX 문서에 지정된 PDF 원본 요소의 값과 일치해야 합니다.
   * 할당 `BLOB` 에 PDF 문서를 저장하는 개체 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체 `value` 필드.
   * 추가 `MyMapOf_xsd_string_To_xsd_anyType_Item` 에 대한 오브젝트 `MyMapOf_xsd_string_To_xsd_anyType` 개체. 호출 `MyMapOf_xsd_string_To_xsd_anyType` 오브젝트&#39; `Add` 메서드 및 전달 `MyMapOf_xsd_string_To_xsd_anyType` 개체.

1. 런타임 옵션을 설정합니다.

   * 만들기 `AssemblerOptionSpec` 생성자를 사용하여 런타임 옵션을 저장하는 개체입니다.
   * 에 속한 데이터 멤버에 값을 할당하여 비즈니스 요구 사항을 충족하는 런타임 옵션을 설정합니다. `AssemblerOptionSpec` 개체. 예를 들어 오류가 발생할 때 어셈블러 서비스에서 작업 처리를 계속하도록 하려면 다음을 할당합니다 `false` (으)로 `AssemblerOptionSpec` 개체 `failOnError` 필드.

1. PDF 문서를 디스어셈블합니다.

   호출 `AssemblerServiceClient` 개체 `invokeDDX` 메서드를 실행하고 다음 값을 전달합니다.

   * A `BLOB` PDF 문서를 디스어셈블하는 DDX 문서를 나타내는 개체입니다
   * 다음 `MyMapOf_xsd_string_To_xsd_anyType` 분해할 PDF 문서가 포함된 개체
   * An `AssemblerOptionSpec` 런타임 옵션을 지정하는 개체입니다

   다음 `invokeDDX` 메서드가 다음을 반환합니다. `AssemblerResult` 작업 결과와 발생한 예외를 포함하는 객체입니다.

1. 분해된 PDF 문서를 저장합니다.

   새로 생성된 PDF 문서를 가져오려면 다음 작업을 수행합니다.

   * 액세스 `AssemblerResult` 개체 `documents` 필드: `Map` 분해된 PDF 문서가 포함된 객체입니다.
   * 다음을 반복합니다. `Map` 객체를 사용하여 각 결과 문서를 가져올 수 있습니다. 그런 다음 해당 배열 멤버의 `value` (으)로 `BLOB`.
   * 에 액세스하여 PDF 문서를 나타내는 이진 데이터 추출 `BLOB` 개체 `MTOM` 속성. PDF 파일에 쓸 수 있는 바이트 배열이 반환됩니다.

**추가 참조**

[프로그래밍 방식으로 PDF 문서 디스어셈블](#programmatically-disassembling-pdf-documents)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
