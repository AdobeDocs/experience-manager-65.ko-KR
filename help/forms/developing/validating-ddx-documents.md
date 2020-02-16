---
title: DCX 문서 유효성 확인
seo-title: DCX 문서 유효성 확인
description: 'null'
seo-description: 'null'
uuid: da668170-d2e9-4fff-aef5-432a856bd0bd
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 693859b0-a0c3-43f1-95c0-be48a90d7d8d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# DCX 문서 유효성 확인 {#validating-ddx-documents}

어셈블리 서비스에서 사용하는 DDX 문서의 유효성을 프로그래밍 방식으로 검사할 수 있습니다. 즉, Assembler 서비스 API를 사용하여 DDX 문서의 유효성을 확인할 수 있습니다. 예를 들어, 이전 AEM Forms 버전에서 업그레이드한 경우 DDX 문서가 유효한지 확인하려면 Assembler 서비스 API를 사용하여 유효성을 검사할 수 있습니다.

>[!NOTE]
>
>어셈블러 서비스에 대한 자세한 내용은 AEM Forms [에 대한 서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDX 문서에 대한 자세한 내용은 어셈블러 서비스 [및 DCX 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 단계 요약 {#summary-of-steps}

DCX 문서의 유효성을 확인하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일 포함
1. 어셈블러 클라이언트를 만듭니다.
1. 기존 DCX 문서를 참조합니다.
1. 런타임 옵션을 설정하여 DCX 문서의 유효성을 확인합니다.
1. 유효성 검사를 수행합니다.
1. 확인 결과를 로그 파일에 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

다음 JAR 파일을 프로젝트의 클래스 경로에 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (AEM Forms가 JBoss에 배포된 경우 필요)
* jbossall-client.jar(JBoss에 AEM Forms가 배포된 경우 필요)

aem Forms가 JBoss가 아닌 지원되는 J2EE 응용 프로그램 서버에 배포된 경우, adobe-utilities.jar 및 jbossall-client.jar 파일을 AEM Forms가 배포된 J2EE 응용 프로그램 서버에 고유한 JAR 파일로 교체해야 합니다.

**PDF 어셈블러 클라이언트 만들기**

어셈블리 작업을 프로그래밍 방식으로 수행하려면 먼저 어셈블러 서비스 클라이언트를 만들어야 합니다.

**기존 DCX 문서 참조**

DCX 문서의 유효성을 확인하려면 기존 DCX 문서를 참조해야 합니다.

**런타임 옵션을 설정하여 DCX 문서의 유효성 검사**

DDX 문서의 유효성을 검사할 때 어셈블리 서비스에서 DCX 문서를 실행하는 대신 유효성을 검사하도록 하는 특정 런타임 옵션을 설정해야 합니다. 또한 어셈블러 서비스가 로그 파일에 쓰는 정보의 양을 늘릴 수 있습니다.

**유효성 검사 수행**

Assembler 서비스 클라이언트를 만들고 DCX 문서를 참조하고 런타임 옵션을 설정한 후 작업을 호출하여 DCX 문서의 유효성을 검사할 수 있습니다. `invokeDDX` DDX 문서의 유효성을 검사할 때 맵 매개 변수로 전달할 수 있습니다(이 매개 변수는 일반적으로 어셈블러가 DCX 문서에 지정된 작업을 수행하는 데 필요한 PDF 문서를 저장합니다). `null`

유효성 검사에 실패하면 예외가 발생하고 로그 파일에 DCX 문서를 인스턴스에서 가져올 수 있는 이유를 설명하는 세부 정보가 포함되어 `OperationException` 있습니다. 기본 XML 구문 분석 및 스키마 검사를 통과하면 DCX 사양에 대한 유효성 검사가 수행됩니다. DCX 문서에 있는 모든 오류는 로그에 지정됩니다.

**확인 결과를 로그 파일에 저장**

어셈블러 서비스는 XML 로그 파일에 쓸 수 있는 유효성 검사 결과를 반환합니다. 어셈블러 서비스가 로그 파일에 쓰는 세부 정보의 양은 사용자가 설정한 런타임 옵션에 따라 다릅니다.

**참고 항목**

[Java API 파섹](#validate-a-ddx-document-using-the-java-api)

[웹 서비스 API 파섹](#validate-a-ddx-document-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[프로그래밍 방식으로 PDF 문서 취합](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API 파섹 {#validate-a-ddx-document-using-the-java-api}

Assembler Service API(Java)를 사용하여 DCX 문서의 유효성을 확인합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-assembler-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. PDF Assembler 클라이언트 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 객체를 전달하여 `AssemblerServiceClient` 객체를 만듭니다 `ServiceClientFactory` .

1. 기존 DCX 문서를 참조합니다.

   * 생성자를 사용하고 DCX 파일의 위치를 지정하는 문자열 값을 전달하여 DCX 문서를 나타내는 `java.io.FileInputStream` 객체를 만듭니다.
   * 생성자를 사용하여 객체를 전달하여 `com.adobe.idp.Document` 객체를 만듭니다 `java.io.FileInputStream` .

1. 런타임 옵션을 설정하여 DCX 문서의 유효성을 확인합니다.

   * 생성자를 사용하여 런타임 옵션을 저장하는 `AssemblerOptionSpec` 객체를 만듭니다.
   * 개체의 setValidateOnly 메서드를 호출하고 전달하여 어셈블리 서비스에서 DDX 문서의 유효성을 검사하도록 하는 런타임 옵션을 `AssemblerOptionSpec` `true`설정합니다.
   * 개체의 메서드를 호출하고 문자열 값을 전달하여 Assembler 서비스가 로그 파일에 쓰는 정보의 양을 요구 사항에 맞게 설정합니다. `AssemblerOptionSpec` `getLogLevel` DCX 문서의 유효성을 검사할 때 유효성 검사 프로세스를 지원하는 로그 파일에 자세한 내용을 기록해야 합니다. 따라서 값 `FINE` 또는 을 전달할 수 `FINER`있습니다.

1. 유효성 검사를 수행합니다.

   객체의 `AssemblerServiceClient` `invokeDDX` 메서드를 호출하고 다음 값을 전달합니다.

   * DCX 문서를 나타내는 `com.adobe.idp.Document` 개체입니다.
   * 일반적으로 PDF 문서를 저장하는 java.io.Map 개체의 `null` 값입니다.
   * 런타임 옵션을 지정하는 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 개체입니다.
   이 `invokeDDX` 메서드는 DCX 문서의 유효성 여부를 지정하는 정보가 포함된 `AssemblerResult` 객체를 반환합니다.

1. 확인 결과를 로그 파일에 저장합니다.

   * 객체를 만들고 파일 이름 확장자가 .xml인지 확인합니다. `java.io.File`
   * 객체의 메서드를 `AssemblerResult` 호출합니다 `getJobLog` . 이 메서드는 유효성 검사 정보를 포함하는 `com.adobe.idp.Document` 인스턴스를 반환합니다.
   * 객체의 메서드를 호출하여 `com.adobe.idp.Document` `copyToFile` `com.adobe.idp.Document` 객체의 내용을 파일에 복사합니다.
   >[!NOTE]
   >
   >DCX 문서가 유효하지 않으면 `OperationException` 가 발생합니다. catch 문 내에서 `OperationException` 개체의 `getJobLog` 메서드를 호출할 수 있습니다.

**참고 항목**

[DCX 문서 유효성 확인](#validating-ddx-documents)

[빠른 시작(SOAP 모드):Java API를 사용하여 DCX 문서](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api) 유효성 검사(SOAP 모드)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API 파섹 {#validate-a-ddx-document-using-the-web-service-api}

Assembler Service API(웹 서비스)를 사용하여 DCX 문서의 유효성을 확인합니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`Adobe

   >[!NOTE]
   >
   >localhost를 양식 서버의 IP 주소로 바꿉니다.

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
   * 생성자를 호출하고 DCX 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 객체를 만듭니다.
   * 개체의 내용을 저장하는 바이트 배열을 `System.IO.FileStream` 만듭니다. 개체의 `System.IO.FileStream` `Length` 속성을 가져와 바이트 배열의 크기를 결정할 수 있습니다.
   * 객체의 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다. `System.IO.FileStream` `Read`
   * 바이트 배열의 컨텐츠로 해당 `BLOB` `MTOM` 속성을 할당하여 객체를 채웁니다.

1. 런타임 옵션을 설정하여 DCX 문서의 유효성을 확인합니다.

   * 생성자를 사용하여 런타임 옵션을 저장하는 `AssemblerOptionSpec` 객체를 만듭니다.
   * 개체의 데이터 멤버에 true 값을 할당하여 어셈블리 서비스가 DDX 문서의 유효성을 확인하도록 하는 런타임 옵션을 `AssemblerOptionSpec` 설정합니다 `validateOnly` .
   * 어셈블리 서비스가 `AssemblerOptionSpec` 개체의 `logLevel` 데이터 멤버에 문자열 값을 할당하여 로그 파일에 쓰는 정보의 양을 설정합니다. 메서드를 사용하여 DCX 문서의 유효성을 검사할 때 유효성 검사 프로세스를 지원하는 로그 파일에 자세한 내용을 기록해야 합니다. 따라서 값 `FINE` 또는 을 지정할 수 `FINER`있습니다. 설정할 수 있는 런타임 옵션에 대한 자세한 내용은 AEM Forms API 참조에서 `AssemblerOptionSpec` 클래스 [참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. 유효성 검사를 수행합니다.

   객체의 `AssemblerServiceClient` `invokeDDX` 메서드를 호출하고 다음 값을 전달합니다.

   * DCX 문서를 나타내는 `BLOB` 개체입니다.
   * 일반적으로 PDF 문서를 저장하는 `null` `Map` 개체의 값입니다.
   * 런타임 옵션을 지정하는 `AssemblerOptionSpec` 객체입니다.
   이 `invokeDDX` 메서드는 DCX 문서의 유효성 여부를 지정하는 정보가 포함된 `AssemblerResult` 객체를 반환합니다.

1. 확인 결과를 로그 파일에 저장합니다.

   * 생성자를 호출하고 로그 파일의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다. 파일 이름 확장자가 .xml인지 확인합니다.
   * 개체의 `BLOB` `AssemblerResult` `jobLog` 데이터 멤버의 값을 가져와 로그 정보를 저장하는 개체를 만듭니다.
   * 개체의 내용을 저장하는 바이트 배열을 `BLOB` 만듭니다. 개체 필드의 값을 가져와 바이트 배열을 `BLOB` 채웁니다 `MTOM` .
   * 생성자를 호출하고 객체를 전달하여 `System.IO.BinaryWriter` `System.IO.FileStream` 객체를 만듭니다.
   * 개체의 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 PDF 파일에 씁니다. `System.IO.BinaryWriter` `Write`
   >[!NOTE]
   >
   >DCX 문서가 유효하지 않으면 `OperationException` 가 발생합니다. catch 문 내에서 `OperationException` 개체 `jobLog` 멤버의 값을 가져올 수 있습니다.

**참고 항목**

[DCX 문서 유효성 확인](#validating-ddx-documents)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
