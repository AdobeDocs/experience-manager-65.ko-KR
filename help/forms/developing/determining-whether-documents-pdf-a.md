---
title: 문서가 PDF/A 호환 여부 확인
seo-title: Determining Whether Documents Are PDF/A-Compliant
description: 어셈블러 서비스를 사용하여 PDF 문서가 Java API 및 웹 서비스 API를 사용하여 PDF/A 호환인지 확인합니다.
seo-description: Use the Assembler service to determine if a PDF document is PDF/A-compliant using the Java API and Web Service API.
uuid: 4e9d8c8f-2153-411b-9c4b-2d14b3c8f4bb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c429d6e1-7847-43c8-bf75-cb0078dbb9d5
role: Developer
exl-id: 096fd2ac-616f-484a-b093-9d98b2f87093
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2082'
ht-degree: 0%

---

# 문서가 PDF/A 호환 여부 확인 {#determining-whether-documents-are-pdf-a-compliant}

어셈블러 서비스를 사용하여 PDF 문서가 PDF/A를 준수하는지 여부를 확인할 수 있습니다. PDF/문서는 문서 컨텐츠의 장기 보존을 위한 보관 형식으로 존재합니다. 글꼴은 문서 내에 포함되고 파일의 압축이 해제됩니다. 따라서 PDF/A 문서는 일반적으로 표준 PDF 문서보다 큽니다. 또한 PDF/문서에 오디오 및 비디오 컨텐츠가 포함되어 있지 않습니다.

PDF/A-1 사양은 두 가지 적합성 수준으로 구성됩니다. 즉, A와 B로 구성됩니다. 두 레벨 간의 주요 차이점은 적합성 레벨 B에 필요하지 않은 논리 구조(액세서빌러티) 지원입니다. 적합성 수준에 관계없이 PDF/A-1은 생성된 PDF/A 문서 내에 모든 글꼴이 포함된다는 것을 나타냅니다. 현재 유효성 검사(및 전환)에서는 PDF/A-1b만 지원됩니다.

이 토론을 위해 다음 DDX 문서가 사용된다고 가정하십시오.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
         <DocumentInformation source="Loan.pdf" result="Loan_result.xml">
         <PDFAValidation compliance="PDF/A-1b" resultLevel="Detailed"                       ignoreUnusedResources="true" allowCertificationSignatures="true" />
     </DocumentInformation>
 </DDX>
```

이 DDX 문서 내에서 `DocumentInformation` 요소는 어셈블러 서비스에서 입력 PDF 문서에 대한 정보를 반환하도록 지시합니다. 내 `DocumentInformation` 요소, `PDFAValidation` 요소는 입력 PDF 문서가 PDF/A를 준수하는지 여부를 어셈블러 서비스에 지시합니다.

어셈블러 서비스는 입력 PDF 문서가 포함된 XML 문서 내의 PDF/A 규격 문서인지 여부를 지정하는 정보를 반환합니다 `PDFAConformance` 요소를 생성하지 않습니다. 입력 PDF 문서가 PDF/A 규격 문서인 경우 `PDFAConformance` 요소 `isCompliant` attribute `true`. PDF 문서가 PDF/A 규격이 아닌 경우 `PDFAConformance` 요소 `isCompliant` attribute `false`.

>[!NOTE]
>
>이 섹션에 지정된 DDX 문서에는 `DocumentInformation` 요소를 사용하면 어셈블러 서비스가 PDF 문서 대신 XML 데이터를 반환합니다. 즉, 어셈블러 서비스는 PDF 문서를 어셈블하거나 분해하지 않습니다. XML 문서 내의 입력 PDF 문서에 대한 정보를 반환합니다.

>[!NOTE]
>
>어셈블러 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDX 문서에 대한 자세한 내용은 [어셈블러 서비스 및 DDX 참조](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 단계 요약 {#summary-of-steps}

PDF 문서가 PDF/A 규격 문서인지 확인하려면 다음 작업을 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. PDF 어셈블러 클라이언트를 만듭니다.
1. 기존 DDX 문서를 참조합니다.
1. PDF/A 규정을 결정하는 데 사용되는 PDF 문서를 참조합니다.
1. 런타임 옵션을 설정합니다.
1. PDF 문서에 대한 정보를 검색합니다.
1. 반환된 XML 문서를 저장합니다.

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

어셈블러 서비스 작업을 수행하려면 DDX 문서를 참조해야 합니다. 입력 PDF 문서가 PDF/A 규격 문서인지 확인하려면 DDX 문서에 `PDFAValidation` 내의 요소 `DocumentInformation` 요소를 생성하지 않습니다. 다음 `PDFAValidation` 요소는 입력 PDF 문서가 PDF/A를 준수하는지 여부를 지정하는 XML 문서를 어셈블러 서비스에 반환하도록 지시합니다.

**PDF/A 규정을 결정하는 데 사용되는 PDF 문서를 참조합니다.**

PDF 문서를 참조하고 어셈블러 서비스로 전달하여 PDF 문서가 PDF/A 규격 문서인지 확인해야 합니다.

**런타임 옵션 설정**

작업을 수행하는 동안 어셈블러 서비스의 동작을 제어하는 런타임 옵션을 설정할 수 있습니다. 예를 들어 오류가 발생하면 어셈블러 서비스에 작업을 계속 처리하도록 지시하는 옵션을 설정할 수 있습니다. 설정할 수 있는 런타임 옵션에 대한 자세한 내용은 `AssemblerOptionSpec` 클래스 참조 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**PDF 문서에 대한 정보 검색**

어셈블러 서비스 클라이언트를 만들고 DDX 문서를 참조하고 대화형 PDF 문서를 참조하며 런타임 옵션을 설정한 후에는 `invokeDDX` 작업. DDX 문서에 `DocumentInformation` 요소를 사용하면 어셈블러 서비스가 PDF 문서 대신 XML 데이터를 반환합니다.

**반환된 XML 문서를 저장합니다**

어셈블러 서비스가 반환하는 XML 문서는 입력 PDF 문서가 PDF/A 규격 문서인지 여부를 지정합니다. 예를 들어, 입력 PDF 문서가 PDF/A를 준수하지 않으면 어셈블러 서비스는 다음 요소가 포함된 XML 문서를 반환합니다.

```xml
 <PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Detailed" ignoreUnusedResources="true" allowCertificationSignatures="true">
```

XML 문서를 XML 파일로 저장하여 파일을 열고 결과를 볼 수 있습니다.

**추가 참조**

[Java API를 사용하여 문서가 PDF/A 호환되는지 확인](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api)

[웹 서비스 API를 사용하여 문서가 PDF/A 호환되는지 확인](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[프로그래밍 방식으로 PDF 문서 조립](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API를 사용하여 문서가 PDF/A 호환되는지 확인 {#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api}

Assembler Service API(Java)를 사용하여 PDF 문서가 PDF/A 호환되는지 확인합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-assembler-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. PDF 어셈블러 클라이언트를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 객체입니다.
   * 만들기 `AssemblerServiceClient` 생성자를 사용하여 객체를 전달하고 `ServiceClientFactory` 개체.

1. 기존 DDX 문서를 참조합니다.

   * 만들기 `java.io.FileInputStream` 생성자를 사용하고 DDX 파일의 위치를 지정하는 문자열 값을 전달하여 DDX 문서를 나타내는 개체입니다. PDF 문서가 PDF/A 규격 문서인지 확인하려면 DDX 문서에 `PDFAValidation` 내에 들어 있는 요소 `DocumentInformation` 요소를 생성하지 않습니다.
   * 만들기 `com.adobe.idp.Document` 생성자를 사용하여 객체를 전달하고 `java.io.FileInputStream` 개체.

1. PDF/A 규정을 결정하는 데 사용되는 PDF 문서를 참조합니다.

   * 만들기 `java.io.FileInputStream` 생성자를 사용하여 PDF/A 규정 준수를 결정하는 데 사용되는 PDF 문서의 위치를 전달하여 객체를 만듭니다.
   * 만들기 `com.adobe.idp.Document` 생성자를 사용하여 객체를 전달하고 `java.io.FileInputStream` PDF 문서를 포함하는 객체입니다.
   * 만들기 `java.util.Map` 입력 PDF 문서를 저장하는 데 사용되는 객체 `HashMap` 생성자입니다.
   * 에 항목 추가 `java.util.Map` 객체를 호출하여 `put` 메서드와 다음 인수를 전달합니다.

      * 키 이름을 나타내는 문자열 값입니다. 이 값은 DDX 문서에 지정된 소스 요소의 값과 일치해야 합니다. 예를 들어 이 섹션에서 도입된 DDX 문서에 있는 소스 요소의 값은 Loan.pdf입니다.
      * A `com.adobe.idp.Document` 입력 PDF 문서를 포함하는 객체입니다.

1. 런타임 옵션을 설정합니다.

   * 만들기 `AssemblerOptionSpec` 생성자를 사용하여 런타임 옵션을 저장하는 개체입니다.
   * 에 속한 메서드를 호출하여 비즈니스 요구 사항을 충족하도록 런타임 옵션을 설정합니다. `AssemblerOptionSpec` 개체. 예를 들어 오류가 발생할 때 어셈블러 서비스에서 작업을 계속 처리하도록 하려면 `AssemblerOptionSpec` 개체 `setFailOnError` 메서드 및 전달 `false`.

1. PDF 문서에 대한 정보를 검색합니다.

   를 호출합니다 `AssemblerServiceClient` 개체 `invokeDDX` 메서드를 사용하여 다음 필수 값을 전달합니다.

   * A `com.adobe.idp.Document` 사용할 DDX 문서를 나타내는 객체입니다
   * A `java.util.Map` PDF/A 규정을 결정하는 데 사용되는 입력 PDF 파일이 포함된 객체
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 런타임 옵션을 지정하는 객체

   다음 `invokeDDX` 메서드 반환 `com.adobe.livecycle.assembler.client.AssemblerResult` 입력 PDF 문서가 PDF/A 규격 문서인지 여부를 지정하는 XML 데이터가 포함된 객체입니다.

1. 반환된 XML 문서를 저장합니다.

   입력 PDF 문서가 PDF/A 문서인지 여부를 지정하는 XML 데이터를 가져오려면 다음 작업을 수행하십시오.

   * 를 호출합니다 `AssemblerResult` 개체 `getDocuments` 메서드를 사용합니다. 이는 를 반환합니다 `java.util.Map` 개체.
   * 를 통해 반복 `java.util.Map` 결과를 찾을 때까지 객체 `com.adobe.idp.Document` 개체.
   * 를 호출합니다 `com.adobe.idp.Document` 개체 `copyToFile` XML 문서를 추출하는 방법입니다. XML 데이터를 XML 파일로 저장해야 합니다.

**추가 참조**

[빠른 시작(SOAP 모드): Java API를 사용하여 문서가 PDF/A 호환인지 확인](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-determining-whether-a-document-is-pdf-a-compliant-using-the-java-api) (SOAP 모드)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API를 사용하여 문서가 PDF/A 호환되는지 확인 {#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api}

어셈블러 서비스 API(웹 서비스)를 사용하여 PDF 문서가 PDF/A 규격 문서인지 확인합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` (AEM Forms을 호스팅하는 서버의 IP 주소 사용)

1. PDF 어셈블러 클라이언트를 만듭니다.

   * 만들기 `AssemblerServiceClient` 기본 생성자를 사용하여 개체를 만듭니다.
   * 만들기 `AssemblerServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). 를 사용할 필요가 없습니다 `lc_version` 속성을 사용합니다. 이 속성은 서비스 참조를 생성할 때 사용됩니다.)
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
   * 를 호출하여 바이트 배열을 스트림 데이터로 채웁니다 `System.IO.FileStream` 개체 `Read` 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하는 메서드와 전달
   * 을(를) 채우기 `BLOB` 개체를 할당하여 개체를 개체 개체 `MTOM` 바이트 배열의 내용을 포함하는 필드입니다.

1. PDF/A 규정을 결정하는 데 사용되는 PDF 문서를 참조합니다.

   * 만들기 `BLOB` 생성자를 사용하여 개체를 작성합니다. 다음 `BLOB` 개체는 입력 PDF 문서를 저장하는 데 사용됩니다.
   * 만들기 `System.IO.FileStream` 객체를 사용하여 생성자를 호출하고 입력 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 내용을 저장하는 바이트 배열을 만듭니다 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성을 사용합니다.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채웁니다 `System.IO.FileStream` 개체 `Read` 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하는 메서드와 전달
   * 을(를) 채우기 `BLOB` 개체를 할당하여 개체를 개체 개체 `MTOM` 바이트 배열의 내용을 포함하는 속성입니다.
   * 만들기 `MyMapOf_xsd_string_To_xsd_anyType` 개체. 이 컬렉션 개체는 PDF 문서를 저장하는 데 사용됩니다.
   * 만들기 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체.
   * 키 이름을 나타내는 문자열 값을 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체 `key` 필드. 이 값은 DDX 문서에 지정된 PDF 소스 요소의 값과 일치해야 합니다.
   * 을(를) 지정합니다. `BLOB` PDF 문서를 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체 `value` 필드.
   * 추가 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체 `MyMapOf_xsd_string_To_xsd_anyType` 개체. 를 호출합니다 `MyMapOf_xsd_string_To_xsd_anyType` object&#39; `Add` 메서드 및 전달 `MyMapOf_xsd_string_To_xsd_anyType` 개체.

1. 런타임 옵션을 설정합니다.

   * 만들기 `AssemblerOptionSpec` 생성자를 사용하여 런타임 옵션을 저장하는 개체입니다.
   * 비즈니스 요구 사항에 맞게 런타임 옵션을 설정하려면 `AssemblerOptionSpec` 개체. 예를 들어 오류가 발생할 때 어셈블러 서비스에서 작업을 계속 처리하도록 지시하려면 을 할당합니다. `false` 변환 후 `AssemblerOptionSpec` 개체 `failOnError` 데이터 멤버.

1. PDF 문서에 대한 정보를 검색합니다.

   를 호출합니다 `AssemblerServiceService` 개체 `invoke` 메서드를 사용하여 다음 값을 전달합니다.

   * A `BLOB` DDX 문서를 나타내는 객체입니다.
   * 다음 `MyMapOf_xsd_string_To_xsd_anyType` 입력 PDF 문서를 포함하는 객체입니다. 해당 키는 PDF 소스 파일의 이름과 일치해야 하며 해당 값은 `BLOB` 입력 PDF 파일에 해당하는 개체입니다.
   * An `AssemblerOptionSpec` 런타임 옵션을 지정하는 개체입니다.

   다음 `invoke` 메서드 반환 `AssemblerResult` 입력 PDF 문서가 PDF/A 문서인지 여부를 지정하는 XML 데이터가 포함된 객체입니다.

1. 반환된 XML 문서를 저장합니다.

   입력 PDF 문서가 PDF/A 문서인지 여부를 지정하는 XML 데이터를 가져오려면 다음 작업을 수행하십시오.

   * 액세스 권한 `AssemblerResult` 개체 `documents` 필드, 즉 `Map` 입력 PDF 문서가 PDF/A 문서인지 여부를 지정하는 XML 데이터가 포함된 객체입니다.
   * 를 통해 반복 `Map` 각 결과 문서를 가져올 객체입니다. 그런 다음 해당 배열 멤버의 값을 `BLOB`.
   * XML 데이터에 액세스하여 XML 데이터를 나타내는 이진 데이터를 추출합니다 `BLOB` 개체 `MTOM` 필드. 이 필드에는 XML 파일로 쓸 수 있는 바이트 배열이 저장됩니다.

**추가 참조**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
