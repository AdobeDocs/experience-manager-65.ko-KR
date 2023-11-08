---
title: DDX 문서 검증
seo-title: Validating DDX Documents
description: Java API 및 웹 서비스 API를 사용하여 프로그래밍 방식으로 DDX 문서의 유효성을 검사합니다.
seo-description: Validate a DDX document programmatically using the Java API and the Web Service API.
uuid: da668170-d2e9-4fff-aef5-432a856bd0bd
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 693859b0-a0c3-43f1-95c0-be48a90d7d8d
role: Developer
exl-id: 1f5a2cf3-ef6b-45b4-8fa8-b300e492fee1
source-git-commit: c4cd9a61a226ace2a72d60b5b7b7432de12cb873
workflow-type: tm+mt
source-wordcount: '1525'
ht-degree: 0%

---

# DDX 문서 검증 {#validating-ddx-documents}

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms에 대해서만 적용됩니다.**

어셈블러 서비스에서 사용하는 DDX 문서의 유효성을 프로그래밍 방식으로 검사할 수 있습니다. 즉, 어셈블러 서비스 API를 사용하여 DDX 문서가 유효한지 여부를 결정할 수 있습니다. 예를 들어 이전 AEM Forms 버전에서 업그레이드한 경우 DDX 문서가 유효한지 확인하려면 어셈블러 서비스 API를 사용하여 유효성을 검사할 수 있습니다.

>[!NOTE]
>
>어셈블러 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDX 문서에 대한 자세한 내용은 [어셈블러 서비스 및 DDX 참조](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 단계 요약 {#summary-of-steps}

DDX 문서의 유효성을 검사하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. 어셈블러 클라이언트를 만듭니다.
1. 기존 DDX 문서를 참조합니다.
1. 런타임 옵션을 설정하여 DDX 문서의 유효성을 검사합니다.
1. 유효성 검사를 수행합니다.
1. 로그 파일에 유효성 검사 결과를 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필수)

AEM Forms이 JBoss 이외의 지원되는 J2EE 애플리케이션 서버에 배포된 경우 adobe-utilities.jar 및 jbossall-client.jar 파일을 AEM Forms이 배포된 J2EE 애플리케이션 서버에 관련된 JAR 파일로 교체해야 합니다.

**PDF 어셈블러 클라이언트 만들기**

어셈블러 작업을 프로그래밍 방식으로 수행하려면 먼저 어셈블러 서비스 클라이언트를 만들어야 합니다.

**기존 DDX 문서 참조**

DDX 문서의 유효성을 검사하려면 기존 DDX 문서를 참조해야 합니다.

**런타임 옵션을 설정하여 DDX 문서의 유효성 검사**

DDX 문서의 유효성을 검사할 때 어셈블러 서비스에서 DDX 문서를 실행할 때와 반대로 유효성 검사하도록 지시하는 특정 런타임 옵션을 설정해야 합니다. 또한 어셈블러 서비스에서 로그 파일에 쓰는 정보의 양을 늘릴 수 있습니다.

**유효성 검사 수행**

어셈블러 서비스 클라이언트를 만들고 DDX 문서를 참조하며 런타임 옵션을 설정한 후 `invokeDDX` ddx 문서의 유효성을 검사하는 작업입니다. DDX 문서의 유효성을 검사할 때 `null` 맵 매개 변수로 사용됩니다. 이 매개 변수는 일반적으로 어셈블러가 DDX 문서에 지정된 작업을 수행하는 데 필요한 PDF 문서를 저장합니다.

유효성 검사가 실패하면 예외가 발생하고 로그 파일에는 DDX 문서가 유효하지 않은 이유를 설명하는 세부 정보가 포함되어 있습니다. `OperationException` 인스턴스. 기본 XML 구문 분석 및 스키마 검사를 지난 후 DDX 사양에 대한 유효성 검사가 수행됩니다. DDX 문서에 있는 모든 오류는 로그에 지정됩니다.

**로그 파일에 유효성 검사 결과 저장**

어셈블러 서비스는 XML 로그 파일에 작성할 수 있는 유효성 검사 결과를 반환합니다. 어셈블러 서비스에서 로그 파일에 쓰는 세부 정보의 양은 사용자가 설정한 런타임 옵션에 따라 다릅니다.

**추가 참조**

[Java API를 사용하여 DDX 문서의 유효성 검사](#validate-a-ddx-document-using-the-java-api)

[웹 서비스 API를 사용하여 DDX 문서의 유효성 검사](#validate-a-ddx-document-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[프로그래밍 방식으로 PDF 문서 어셈블](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API를 사용하여 DDX 문서의 유효성 검사 {#validate-a-ddx-document-using-the-java-api}

어셈블러 서비스 API(Java)를 사용하여 DDX 문서의 유효성을 검사합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-assembler-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. PDF 어셈블러 클라이언트를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.
   * 만들기 `AssemblerServiceClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체.

1. 기존 DDX 문서를 참조합니다.

   * 만들기 `java.io.FileInputStream` 생성자를 사용하고 DDX 파일의 위치를 지정하는 문자열 값을 전달하여 DDX 문서를 나타내는 개체입니다.
   * 만들기 `com.adobe.idp.Document` 개체를 생성자를 사용하고 `java.io.FileInputStream` 개체.

1. 런타임 옵션을 설정하여 DDX 문서의 유효성을 검사합니다.

   * 만들기 `AssemblerOptionSpec` 생성자를 사용하여 런타임 옵션을 저장하는 개체입니다.
   * 어셈블러 서비스에서 를 호출하여 DDX 문서의 유효성을 검사하도록 지시하는 런타임 옵션을 설정합니다. `AssemblerOptionSpec` 개체의 setValidateOnly 메서드 및 전달 `true`.
   * 어셈블러 서비스에서 로그 파일에 쓰는 정보의 양을 설정합니다. `AssemblerOptionSpec` 개체 `getLogLevel` 메서드 및 문자열 값 전달은 요구 사항을 충족합니다. DDX 문서의 유효성을 검사할 때 유효성 검사 프로세스에 도움이 되도록 로그 파일에 자세한 정보를 작성해야 합니다. 따라서 값을 전달할 수 있습니다 `FINE` 또는 `FINER`.

1. 유효성 검사를 수행합니다.

   호출 `AssemblerServiceClient` 개체 `invokeDDX` 메서드를 실행하고 다음 값을 전달합니다.

   * A `com.adobe.idp.Document` DDX 문서를 나타내는 개체입니다.
   * 값 `null` 일반적으로 PDF 문서를 저장하는 java.io.Map 개체의 경우.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 런타임 옵션을 지정하는 개체입니다.

   다음 `invokeDDX` 메서드가 다음을 반환합니다. `AssemblerResult` DDX 문서가 유효한지 여부를 지정하는 정보가 포함된 개체입니다.

1. 로그 파일에 유효성 검사 결과를 저장합니다.

   * 만들기 `java.io.File` 개체를 클릭하고 파일 이름 확장명이 .xml인지 확인하십시오.
   * 호출 `AssemblerResult` 개체 `getJobLog` 메서드를 사용합니다. 이 메서드는 `com.adobe.idp.Document` 유효성 검사 정보가 포함된 인스턴스입니다.
   * 호출 `com.adobe.idp.Document` 개체 `copyToFile` 콘텐츠 복사 방법 `com.adobe.idp.Document` 파일에 대한 개체입니다.

   >[!NOTE]
   >
   >DDX 문서가 유효하지 않은 경우 `OperationException` 이 throw됩니다. catch 문 내에서 `OperationException` 개체 `getJobLog` 메서드를 사용합니다.

**추가 참조**

[DDX 문서 검증](#validating-ddx-documents)

[빠른 시작(SOAP 모드): Java API를 사용하여 DDX 문서 유효성 검사](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api) (SOAP 모드)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API를 사용하여 DDX 문서의 유효성 검사 {#validate-a-ddx-document-using-the-web-service-api}

어셈블러 서비스 API(웹 서비스)를 사용하여 DDX 문서의 유효성을 검사합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용하는지 확인합니다. `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >localhost를 Forms 서버의 IP 주소로 바꿉니다.

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
   * 만들기 `System.IO.FileStream` 개체를 호출하고 DDX 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여
   * 의 콘텐츠를 저장하는 바이트 배열 만들기 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채우기 `System.IO.FileStream` 개체 `Read` 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하는 방법.
   * 채우기 `BLOB` 개체 할당 `MTOM` 속성을 바이트 배열의 콘텐츠와 함께 사용합니다.

1. 런타임 옵션을 설정하여 DDX 문서의 유효성을 검사합니다.

   * 만들기 `AssemblerOptionSpec` 생성자를 사용하여 런타임 옵션을 저장하는 개체입니다.
   * true 값을 로 할당하여 어셈블러 서비스에서 DDX 문서의 유효성을 검사하도록 지시하는 런타임 옵션을 설정합니다. `AssemblerOptionSpec` 개체 `validateOnly` 데이터 구성원입니다.
   * 문자열 값을 로 할당하여 어셈블러 서비스에서 로그 파일에 쓰는 정보의 양을 설정합니다. `AssemblerOptionSpec` 개체 `logLevel` 데이터 구성원입니다. 메서드 DDX 문서의 유효성을 검사할 때 유효성 검사 프로세스에 도움이 되도록 로그 파일에 자세한 정보를 기록해야 합니다. 따라서 값을 지정할 수 있습니다 `FINE` 또는 `FINER`. 설정할 수 있는 런타임 옵션에 대한 자세한 내용은 `AssemblerOptionSpec` 의 클래스 참조 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. 유효성 검사를 수행합니다.

   호출 `AssemblerServiceClient` 개체 `invokeDDX` 메서드를 실행하고 다음 값을 전달합니다.

   * A `BLOB` DDX 문서를 나타내는 개체입니다.
   * 값 `null` 대상: `Map` 일반적으로 PDF 문서를 저장하는 객체입니다.
   * An `AssemblerOptionSpec` 런타임 옵션을 지정하는 개체입니다.

   다음 `invokeDDX` 메서드가 다음을 반환합니다. `AssemblerResult` DDX 문서가 유효한지 여부를 지정하는 정보가 포함된 개체입니다.

1. 로그 파일에 유효성 검사 결과를 저장합니다.

   * 만들기 `System.IO.FileStream` 개체를 호출하고 로그 파일의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다. 파일 이름 확장명이 .xml인지 확인합니다.
   * 만들기 `BLOB` 값을 가져와서 로그 정보를 저장하는 개체 `AssemblerResult` 개체 `jobLog` 데이터 구성원입니다.
   * 의 콘텐츠를 저장하는 바이트 배열 만들기 `BLOB` 개체. 의 값을 가져와서 바이트 배열 채우기 `BLOB` 개체 `MTOM` 필드.
   * 만들기 `System.IO.BinaryWriter` 개체를 호출하고 `System.IO.FileStream` 개체.
   * 를 호출하여 바이트 배열의 내용을 PDF 파일에 씁니다 `System.IO.BinaryWriter` 개체 `Write` 메서드 및 바이트 배열 전달.

   >[!NOTE]
   >
   >DDX 문서가 유효하지 않은 경우 `OperationException` 이 throw됩니다. catch 문 내에서 `OperationException` 개체 `jobLog` 멤버.

**추가 참조**

[DDX 문서 검증](#validating-ddx-documents)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
