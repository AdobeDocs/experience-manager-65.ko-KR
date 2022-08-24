---
title: 비대화형 PDF 문서 정리
seo-title: Assembling Non-Interactive PDF Documents
description: 비대화형 PDF 양식을 입력으로 사용하여 Java API 및 웹 서비스 API를 사용하여 비대화형 PDF 문서를 어셈블합니다.
seo-description: Use a non-interactive PDF form as input to assemble a non-interactive PDF document using the Java API and Web Service API.
uuid: 0c7adeb4-9a3a-4ec5-ba33-c3642928d4ea
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8a75c201-bd88-4809-be08-69de94656489
role: Developer
exl-id: 4677b9e5-3811-4de3-b4f4-9574b5898486
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '1775'
ht-degree: 0%

---

# 비대화형 PDF 문서 정리 {#assembling-non-interactive-pdf-documents}

대화형 PDF 양식을 입력으로 사용할 때 비대화형 PDF 문서를 어셈블할 수 있습니다. 즉, 사용자가 해당 필드에 데이터를 입력하는 데 사용할 수 있는 양식이 있다고 가정합니다. 이 양식을 어셈블러 서비스에 전달하면 어셈블러 서비스가 사용자가 해당 필드에 데이터를 입력할 수 없도록 하는 PDF 문서를 반환합니다. 이 문서는 비대화형 PDF 양식입니다. 예를 들어, 다음 그림은 대화형 양식을 나타내는 모기지 애플리케이션을 보여 줍니다.

이 토론을 위해 다음 DDX 문서가 사용된다고 가정하십시오.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDF result="out.pdf">
        <PDF source="inDoc"/>
        <NoXFA/>
      </PDF>
 </DDX>
```

이 DDX 문서 내에서 소스 속성에 값이 할당되었음을 알 수 있습니다 `inDoc`. 하나의 입력 PDF 문서만 어셈블러 서비스에 전달되고 하나의 PDF 문서가 반환되는 경우 `invokeOneDocument` 작업, 값 할당 `inDoc` 를 PDF 소스 속성에 추가합니다. 를 호출할 때 `invokeOneDocument` 작업, `inDoc` 값은 DDX 문서에 지정해야 하는 사전 정의된 키입니다.

반면 입력 PDF 문서를 어셈블러 서비스에 두 개 이상 전달할 때 `invokeDDX` 작업. 이 경우 입력 PDF 문서의 파일 이름을 `source` 속성을 사용합니다.

이 DDX 문서에는 `NoXFA` 요소 - 어셈블러 서비스에서 비대화형 PDF 문서를 반환하도록 지시합니다.

입력 PDF 문서가 Acrobat 양식 또는 정적 XFA 양식을 기반으로 하는 경우 어셈블러 서비스는 출력 서비스가 AEM Forms 설치에 포함되지 않은 비대화형 PDF 문서를 어셈블할 수 있습니다. 그러나 입력 PDF 문서가 동적 XFA 양식인 경우 출력 서비스가 AEM Forms 설치의 일부여야 합니다. 동적 XFA 양식을 어셈블할 때 출력 서비스가 AEM Forms 설치의 일부가 아닌 경우 예외가 발생합니다. 자세한 내용은 [문서 출력 스트림 만들기](/help/forms/developing/creating-document-output-streams.md).

>[!NOTE]
>
>이 섹션을 읽기 전에 어셈블러 서비스를 사용하여 PDF 문서 조립에 익숙해지는 것이 좋습니다. 이 섹션에서는 입력 문서가 포함된 컬렉션 개체를 만들거나 반환된 수집 개체에서 결과를 추출하는 방법을 학습하는 등의 개념을 다루지 않습니다. (자세한 내용은 [프로그래밍 방식으로 PDF 문서 조립](/help/forms/developing/programmatically-assembling-pdf-documents.md))

>[!NOTE]
>
>어셈블러 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDX 문서에 대한 자세한 내용은 [어셈블러 서비스 및 DDX 참조](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 단계 요약 {#summary-of-steps}

비대화형 PDF 문서를 어셈블하려면 다음 작업을 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. PDF 어셈블러 클라이언트를 만듭니다.
1. 기존 DDX 문서를 참조합니다.
1. 대화형 PDF 문서를 참조합니다.
1. 런타임 옵션을 설정합니다.
1. PDF 문서를 어셈블합니다.
1. 비대화형 PDF 문서를 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함하십시오. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms이 JBoss에 배포되는 경우 필요)

AEM Forms이 JBoss 이외의 지원되는 J2EE 애플리케이션 서버에 배포된 경우, adobe-utilities.jar 및 jbossall-client.jar 파일을 AEM Forms이 배포된 J2EE 애플리케이션 서버에 고유한 JAR 파일로 바꾸어야 합니다.

**어셈블러 클라이언트 만들기**

어셈블러 작업을 프로그래밍 방식으로 수행하려면 먼저 어셈블러 서비스 클라이언트를 만들어야 합니다.

**기존 DDX 문서 참조**

PDF 문서를 어셈블하려면 DDX 문서를 참조해야 합니다. 이 DDX 문서에는 `NoXFA` 요소 - 어셈블러 서비스에서 비대화형 PDF 문서를 반환하도록 지시합니다.

**대화형 PDF 문서 참조**

대화형 PDF 문서를 참조하고 어셈블러 서비스로 전달하여 비대화형 PDF 문서를 다시 가져와야 합니다.

**런타임 옵션 설정**

작업을 수행하는 동안 어셈블러 서비스의 동작을 제어하는 런타임 옵션을 설정할 수 있습니다. 예를 들어 오류가 발생하면 어셈블러 서비스에 작업을 계속 처리하도록 지시하는 옵션을 설정할 수 있습니다.

**PDF 문서 조합**

어셈블러 서비스 클라이언트를 만들고 DDX 문서를 참조하고 대화형 PDF 문서를 참조하며 런타임 옵션을 설정한 후에는 `invokeOneDocument` 작업. 하나의 입력 PDF 문서만 어셈블러 서비스에 전달되고 하나의 문서가 반환되므로 `invokeOneDocument` 그 작전과는 반대로 `invokeDDX` 작업.

**비대화형 PDF 문서를 저장합니다**

단일 PDF 문서만 어셈블러 서비스에 전달되면 어셈블러 서비스는 수집 객체 대신 단일 문서를 반환합니다. 즉, `invokeOneDocument` 작업을 수행하면 단일 문서가 반환됩니다. 이 섹션에서 참조되는 DDX 문서에는 비대화형 PDF 문서를 만드는 지침이 포함되어 있으므로 어셈블러 서비스는 PDF 파일로 저장할 수 있는 비대화형 PDF 문서를 반환합니다.

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[프로그래밍 방식으로 PDF 문서 조립](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API를 사용하여 비대화형 PDF 문서 조합 {#assemble-a-non-interactive-pdf-document-using-the-java-api}

어셈블러 서비스 API(Java)를 사용하여 비대화형 PDF 문서를 어셈블합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-assembler-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. 어셈블러 클라이언트를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 객체입니다.
   * 만들기 `AssemblerServiceClient` 생성자를 사용하여 객체를 전달하고 `ServiceClientFactory` 개체.

1. 기존 DDX 문서를 참조합니다.

   * 만들기 `java.io.FileInputStream` 생성자를 사용하고 DDX 파일의 위치를 지정하는 문자열 값을 전달하여 DDX 문서를 나타내는 개체입니다.
   * 만들기 `com.adobe.idp.Document` 생성자를 사용하여 객체를 전달하고 `java.io.FileInputStream` 개체.

1. 대화형 PDF 문서를 참조합니다.

   * 만들기 `java.io.FileInputStream` 생성자를 사용하여 대화형 PDF 문서의 위치를 전달하여 개체를 가져옵니다.
   * 만들기 `com.adobe.idp.Document` 개체 및 전달 `java.io.FileInputStream` PDF 문서를 포함하는 객체입니다. 이 `com.adobe.idp.Document` 개체가 `invokeOneDocument` 메서드를 사용합니다.

1. 런타임 옵션을 설정합니다.

   * 만들기 `AssemblerOptionSpec` 생성자를 사용하여 런타임 옵션을 저장하는 개체입니다.
   * 에 속한 메서드를 호출하여 비즈니스 요구 사항을 충족하도록 런타임 옵션을 설정합니다. `AssemblerOptionSpec` 개체. 예를 들어 오류가 발생할 때 어셈블러 서비스에서 작업을 계속 처리하도록 하려면 `AssemblerOptionSpec` 개체 `setFailOnError` 메서드 및 전달 `false`.

1. PDF 문서를 어셈블합니다.

   를 호출합니다 `AssemblerServiceClient` 개체 `invokeOneDocument` 메서드를 사용하여 다음 값을 전달합니다.

   * A `com.adobe.idp.Document` DDX 문서를 나타내는 객체입니다. 이 DDX 문서에 값이 포함되어 있는지 확인합니다. `inDoc` PDF 소스 요소에 사용됩니다.
   * A `com.adobe.idp.Document` 대화형 PDF 문서를 포함하는 객체입니다.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 기본 글꼴 및 작업 로그 수준을 포함하여 런타임 옵션을 지정하는 개체입니다.

   다음 `invokeOneDocument` 메서드 반환 `com.adobe.idp.Document` 비대화형 PDF 문서를 포함하는 개체입니다.

1. 비대화형 PDF 문서를 저장합니다.

   * 만들기 `java.io.File` 개체 및 파일 이름 확장명이 .pdf인지 확인합니다.
   * 를 호출합니다 `Document` 개체 `copyToFile` 컨텐츠의 내용 복사 방법 `Document` 개체를 파일로 가져올 수 있습니다. 를 사용해야 합니다 `Document` 개체를 `invokeOneDocument` 메서드가 반환되었습니다.

* &quot;빠른 시작(SOAP 모드): Java API를 사용하여 비대화형 PDF 문서 정리&quot;

## 웹 서비스 API를 사용하여 비대화형 PDF 문서 조합 {#assemble-a-non-interactive-pdf-document-using-the-web-service-api}

어셈블러 서비스 API(웹 서비스)를 사용하여 비대화형 PDF 문서를 어셈블합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` (AEM Forms을 호스팅하는 서버의 IP 주소 사용)

1. 어셈블러 클라이언트를 만듭니다.

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
   * 만들기 `System.IO.FileStream` 개체의 생성자를 호출하고 DDX 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 개체를 엽니다.
   * 의 내용을 저장하는 바이트 배열을 만듭니다 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성을 사용합니다.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채웁니다 `System.IO.FileStream` 개체 `Read` 메서드를 사용합니다. 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 을(를) 채우기 `BLOB` 개체를 할당하여 개체를 개체 개체 `MTOM` 바이트 배열의 내용을 포함하는 필드입니다.

1. 대화형 PDF 문서를 참조합니다.

   * 만들기 `BLOB` 생성자를 사용하여 개체를 작성합니다. 다음 `BLOB` 개체는 입력 PDF 문서를 저장하는 데 사용됩니다. 이 `BLOB` 개체가 `invokeOneDocument` 논쟁으로.
   * 만들기 `System.IO.FileStream` 객체를 사용하여 생성자를 호출하고 입력 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 내용을 저장하는 바이트 배열을 만듭니다 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성을 사용합니다.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채웁니다 `System.IO.FileStream` 개체 `Read` 메서드를 사용합니다. 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 을(를) 채우기 `BLOB` 개체를 할당하여 개체를 개체 개체 `MTOM` 바이트 배열의 내용을 포함하는 필드입니다.

1. 런타임 옵션을 설정합니다.

   * 만들기 `AssemblerOptionSpec` 생성자를 사용하여 런타임 옵션을 저장하는 개체입니다.
   * 비즈니스 요구 사항에 맞게 런타임 옵션을 설정하려면 `AssemblerOptionSpec` 개체. 예를 들어 오류가 발생할 때 어셈블러 서비스에서 작업을 계속 처리하도록 지시하려면 을 할당합니다. `false` 변환 후 `AssemblerOptionSpec` 개체 `failOnError` 데이터 멤버.

1. PDF 문서를 어셈블합니다.

   를 호출합니다 `AssemblerServiceClient` 개체 `invokeOneDocument` 메서드를 사용하여 다음 값을 전달합니다.

   * A `BLOB` DDX 문서를 나타내는 객체
   * A `BLOB` 대화형 PDF 문서를 나타내는 개체
   * An `AssemblerOptionSpec` 런타임 옵션을 지정하는 객체

   다음 `invokeOneDocument` 메서드 반환 `BLOB` 비대화형 PDF 문서를 포함하는 개체입니다.

1. 비대화형 PDF 문서를 저장합니다.

   * 만들기 `System.IO.FileStream` 개체의 생성자를 호출하고 비대화형 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 개체를 엽니다.
   * 의 내용을 저장하는 바이트 배열을 만듭니다 `BLOB` 개체를 `invokeOneDocument` 메서드가 반환되었습니다. 의 값을 가져와서 바이트 배열을 채웁니다 `BLOB` 개체 `MTOM` 필드.
   * 만들기 `System.IO.BinaryWriter` 생성자를 호출하고 전달하여 개체를 `System.IO.FileStream` 개체.
   * 를 호출하여 PDF 파일에 바이트 배열의 내용을 씁니다. `System.IO.BinaryWriter` 개체 `Write` 메서드를 사용하여 바이트 배열을 전달합니다.

* &quot;빠른 시작(MTOM): 웹 서비스 API를 사용하여 비대화형 PDF 문서를 어셈블하는 중&quot;.

**추가 참조**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
