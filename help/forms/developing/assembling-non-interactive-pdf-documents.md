---
title: 비대화형 PDF 문서 조합
seo-title: 비대화형 PDF 문서 조합
description: 비대화형 PDF 양식을 입력으로 사용하여 Java API 및 웹 서비스 API를 사용하여 비대화형 PDF 문서를 조합합니다.
seo-description: 비대화형 PDF 양식을 입력으로 사용하여 Java API 및 웹 서비스 API를 사용하여 비대화형 PDF 문서를 조합합니다.
uuid: 0c7adeb4-9a3a-4ec5-ba33-c3642928d4ea
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8a75c201-bd88-4809-be08-69de94656489
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1801'
ht-degree: 0%

---


# 비대화형 PDF 문서 정리 {#assembling-non-interactive-pdf-documents}

대화형 PDF 양식을 입력으로 사용할 때 비대화형 PDF 문서를 조합할 수 있습니다. 즉, 사용자가 필드에 데이터를 입력하는 데 사용할 수 있는 양식이 있다고 가정합니다. 이 양식을 어셈블러 서비스에 전달하면 Assembler 서비스에서 사용자가 필드에 데이터를 입력할 수 없는 PDF 문서를 반환할 수 있습니다. 이 문서는 비대화형 PDF 양식입니다. 예를 들어 다음 그림은 대화형 양식을 나타내는 융자 응용 프로그램을 보여줍니다.

이 토론의 목적으로 다음 DDX 문서를 사용한다고 가정합니다.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDF result="out.pdf">
        <PDF source="inDoc"/>
        <NoXFA/>
      </PDF>
 </DDX>
```

이 DDX 문서 내에서 소스 속성에 `inDoc` 값이 지정되어 있습니다. 입력 PDF 문서가 어셈블러 서비스로 한 개만 전달되고 하나의 PDF 문서가 반환되고 `invokeOneDocument` 작업을 호출하면 PDF 소스 속성에 `inDoc` 값을 할당합니다. `invokeOneDocument` 작업을 호출할 때 `inDoc` 값은 DCX 문서에 지정해야 하는 사전 정의된 키입니다.

반면 입력 PDF 문서를 2개 이상 어셈블러 서비스로 전달할 때 `invokeDDX` 작업을 호출할 수 있습니다. 이 경우 입력 PDF 문서의 파일 이름을 `source` 속성에 할당합니다.

이 DCX 문서에는 Assembler 서비스에 비대화형 PDF 문서를 반환하도록 하는 `NoXFA` 요소가 포함되어 있습니다.

입력 PDF 문서가 Acrobat 양식 또는 정적 XFA 양식을 기반으로 하는 경우 Assembler 서비스는 출력 서비스가 AEM 양식 설치에 포함되지 않은 비대화형 PDF 문서를 조합할 수 있습니다. 그러나 입력 PDF 문서가 동적 XFA 양식인 경우 출력 서비스는 AEM 양식 설치의 일부여야 합니다. 동적 XFA 양식이 어셈블될 때 출력 서비스가 AEM 양식 설치에 포함되지 않은 경우 예외가 발생합니다. [문서 출력 스트림 만들기](/help/forms/developing/creating-document-output-streams.md)를 참조하십시오.

>[!NOTE]
>
>이 섹션을 읽기 전에 Assembler 서비스를 사용하여 PDF 문서를 취합하는 방법을 숙지하는 것이 좋습니다. 이 섹션에서는 입력 문서를 포함하는 컬렉션 개체를 만들거나 반환된 컬렉션 개체에서 결과를 추출하는 방법을 학습하는 등의 개념에 대해 다루지 않습니다. 자세한 내용은 [프로그래밍 방식으로 PDF 문서 조합](/help/forms/developing/programmatically-assembling-pdf-documents.md)을 참조하십시오.

>[!NOTE]
>
>어셈블러 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

>[!NOTE]
>
>DCX 문서에 대한 자세한 내용은 [어셈블러 서비스 및 DCX 참조](https://www.adobe.com/go/learn_aemforms_ddx_63)를 참조하십시오.

## {#summary-of-steps} 단계 요약

비대화형 PDF 문서를 조합하려면 다음 작업을 수행합니다.

1. 프로젝트 파일 포함
1. PDF Assembler 클라이언트를 만듭니다.
1. 기존 DCX 문서를 참조합니다.
1. 인터랙티브한 PDF 문서를 참조합니다.
1. 런타임 옵션을 설정합니다.
1. PDF 문서를 조합합니다.
1. 비대화형 PDF 문서를 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

다음 JAR 파일을 프로젝트의 클래스 경로에 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar (AEM Forms이 JBoss에 배포된 경우 필수)

AEM Forms이 JBoss가 아닌 지원되는 J2EE 응용 프로그램 서버에 배포되는 경우 adobe-utilities.jar 및 jbossall-client.jar 파일을 AEM Forms이 배포된 J2EE 응용 프로그램 서버에 해당하는 JAR 파일로 대체해야 합니다.

**어셈블러 클라이언트 만들기**

어셈블리 작업을 프로그래밍 방식으로 수행하려면 먼저 어셈블러 서비스 클라이언트를 만들어야 합니다.

**기존 DCX 문서 참조**

PDF 문서를 조합하려면 DCX 문서를 참조해야 합니다. 이 DDX 문서에는 `NoXFA` 요소가 포함되어야 합니다. 이 요소는 어셈블러 서비스에서 비대화형 PDF 문서를 반환하도록 지시합니다.

**인터랙티브한 PDF 문서 참조**

대화형 PDF 문서를 참조하고 어셈블리 서비스로 전달하여 비대화형 PDF 문서를 복구해야 합니다.

**런타임 옵션 설정**

작업을 수행하는 동안 어셈블리 서비스의 동작을 제어하는 런타임 옵션을 설정할 수 있습니다. 예를 들어 오류가 발생하면 어셈블리 서비스에 작업을 계속 처리하도록 하는 옵션을 설정할 수 있습니다.

**PDF 문서 조합**

Assembler 서비스 클라이언트를 만들고, DCX 문서를 참조하고, 대화형 PDF 문서를 참조하고, 런타임 옵션을 설정한 후 `invokeOneDocument` 작업을 호출할 수 있습니다. 입력 PDF 문서가 한 개만 어셈블러 서비스로 전달되고 단일 문서가 반환되기 때문에 `invokeDDX` 작업이 아닌 `invokeOneDocument` 작업을 사용할 수 있습니다.

**비대화형 PDF 문서 저장**

하나의 PDF 문서만 Assembler 서비스로 전달되면 Assembler 서비스는 컬렉션 개체 대신 단일 문서를 반환합니다. 즉, `invokeOneDocument` 작업을 호출하면 단일 문서가 반환됩니다. 이 섹션에서 참조되는 DCX 문서에는 비대화형 PDF 문서를 만드는 지침이 포함되어 있으므로 어셈블러 서비스는 PDF 파일로 저장할 수 있는 비대화형 PDF 문서를 반환합니다.

**참고 항목**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[프로그래밍 방식으로 PDF 문서 취합](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API {#assemble-a-non-interactive-pdf-document-using-the-java-api}를 사용하여 비대화형 PDF 문서 조합

Assembler Service API(Java)를 사용하여 비대화형 PDF 문서를 조합합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-assembler-client.jar 등의 클라이언트 JAR 파일을 포함합니다.

1. 어셈블러 클라이언트를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 `AssemblerServiceClient` 개체를 만들고 `ServiceClientFactory` 개체를 전달합니다.

1. 기존 DCX 문서를 참조합니다.

   * 생성자를 사용하여 DCX 문서를 나타내는 `java.io.FileInputStream` 객체를 만들고 DCX 파일의 위치를 지정하는 문자열 값을 전달합니다.
   * 생성자를 사용하여 `com.adobe.idp.Document` 개체를 만들고 `java.io.FileInputStream` 개체를 전달합니다.

1. 인터랙티브한 PDF 문서를 참조합니다.

   * 생성자를 사용하여 대화형 PDF 문서의 위치를 전달하여 `java.io.FileInputStream` 개체를 만듭니다.
   * `com.adobe.idp.Document` 개체를 만들고 PDF 문서가 포함된 `java.io.FileInputStream` 개체를 전달합니다. 이 `com.adobe.idp.Document` 개체는 `invokeOneDocument` 메서드에 전달됩니다.

1. 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 런타임 옵션을 저장하는 `AssemblerOptionSpec` 객체를 만듭니다.
   * `AssemblerOptionSpec` 개체에 속하는 메서드를 호출하여 비즈니스 요구 사항을 충족하도록 런타임 옵션을 설정합니다. 예를 들어 오류가 발생할 때 어셈블리 서비스에서 작업을 계속 처리하도록 하려면 `AssemblerOptionSpec` 개체의 `setFailOnError` 메서드를 호출하고 `false`를 전달합니다.

1. PDF 문서를 조합합니다.

   `AssemblerServiceClient` 객체의 `invokeOneDocument` 메서드를 호출하고 다음 값을 전달합니다.

   * DCX 문서를 나타내는 `com.adobe.idp.Document` 객체입니다. 이 DCX 문서에 PDF 소스 요소의 `inDoc` 값이 포함되어 있는지 확인합니다.
   * 대화형 PDF 문서를 포함하는 `com.adobe.idp.Document` 개체입니다.
   * 기본 글꼴 및 작업 로그 수준을 포함하여 런타임 옵션을 지정하는 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 객체입니다.

   `invokeOneDocument` 메서드는 비대화형 PDF 문서를 포함하는 `com.adobe.idp.Document` 개체를 반환합니다.

1. 비대화형 PDF 문서를 저장합니다.

   * `java.io.File` 개체를 만들고 파일 이름 확장자가 .pdf인지 확인합니다.
   * `Document` 객체의 `copyToFile` 메서드를 호출하여 `Document` 객체의 내용을 파일에 복사합니다. `invokeOneDocument` 메서드가 반환한 `Document` 객체를 사용해야 합니다.

* &quot;빠른 시작(SOAP 모드):Java API를 사용하여 비대화형 PDF 문서 취합&quot;

## 웹 서비스 API {#assemble-a-non-interactive-pdf-document-using-the-web-service-api}를 사용하여 비대화형 PDF 문서 조합

Assembler Service API(웹 서비스)를 사용하여 비대화형 PDF 문서를 조합합니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다.`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꿉니다.

1. 어셈블러 클라이언트를 만듭니다.

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
   * 생성자를 호출하고 DCX 문서의 파일 위치 및 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 객체를 만듭니다.
   * `System.IO.FileStream` 객체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 객체의 `Length` 속성을 가져와 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 객체의 `Read` 메서드를 호출하여 바이트 배열을 스트림 데이터로 채웁니다. 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달합니다.
   * 바이트 배열의 내용으로 `MTOM` 필드를 할당하여 `BLOB` 개체를 채웁니다.

1. 인터랙티브한 PDF 문서를 참조합니다.

   * 생성자를 사용하여 `BLOB` 객체를 만듭니다. `BLOB` 개체는 입력 PDF 문서를 저장하는 데 사용됩니다. 이 `BLOB` 개체는 `invokeOneDocument`에 인수로 전달됩니다.
   * 생성자를 호출하고 입력 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 객체를 만듭니다.
   * `System.IO.FileStream` 객체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 객체의 `Length` 속성을 가져와 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 객체의 `Read` 메서드를 호출하여 바이트 배열을 스트림 데이터로 채웁니다. 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달합니다.
   * 바이트 배열의 내용으로 `MTOM` 필드를 할당하여 `BLOB` 개체를 채웁니다.

1. 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 런타임 옵션을 저장하는 `AssemblerOptionSpec` 객체를 만듭니다.
   * `AssemblerOptionSpec` 개체에 속하는 데이터 멤버에 값을 할당하여 비즈니스 요구 사항에 맞게 런타임 옵션을 설정합니다. 예를 들어 오류가 발생할 때 어셈블리 서비스에서 작업을 계속 처리하도록 하려면 `false`을(를) `AssemblerOptionSpec` 개체의 `failOnError` 데이터 멤버에 할당합니다.

1. PDF 문서를 조합합니다.

   `AssemblerServiceClient` 객체의 `invokeOneDocument` 메서드를 호출하고 다음 값을 전달합니다.

   * DCX 문서를 나타내는 `BLOB` 개체
   * 대화형 PDF 문서를 나타내는 `BLOB` 개체
   * 런타임 옵션을 지정하는 `AssemblerOptionSpec` 개체

   `invokeOneDocument` 메서드는 비대화형 PDF 문서를 포함하는 `BLOB` 개체를 반환합니다.

1. 비대화형 PDF 문서를 저장합니다.

   * 생성자를 호출하고 비대화형 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 객체를 만듭니다.
   * `invokeOneDocument` 메서드가 반환한 `BLOB` 객체의 내용을 저장하는 바이트 배열을 만듭니다. `BLOB` 객체의 `MTOM` 필드 값을 가져와 바이트 배열을 채웁니다.
   * 생성자를 호출하고 `System.IO.FileStream` 객체를 전달하여 `System.IO.BinaryWriter` 객체를 만듭니다.
   * `System.IO.BinaryWriter` 객체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 PDF 파일에 기록합니다.

* &quot;빠른 시작(MTOM):웹 서비스 API를 사용하여 비대화형 PDF 문서를 조합합니다.&quot;

**참고 항목**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
