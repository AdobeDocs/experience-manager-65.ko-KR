---
title: 문서 PDF/A 규격 확인
seo-title: 문서 PDF/A 규격 확인
description: 'null'
seo-description: 'null'
uuid: 4e9d8c8f-2153-411b-9c4b-2d14b3c8f4bb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c429d6e1-7847-43c8-bf75-cb0078dbb9d5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 문서 PDF/A 규격 확인 {#determining-whether-documents-are-pdf-a-compliant}

Assembler 서비스를 사용하여 PDF 문서가 PDF/A 규격인지 확인할 수 있습니다. PDF/A 문서는 문서 컨텐츠를 장기 보존하기 위한 보관 포맷으로 존재합니다. 글꼴은 문서 내에 포함되고 파일의 압축이 해제됩니다. 따라서 PDF/A 문서는 일반적으로 표준 PDF 문서보다 큽니다. 또한 PDF/A 문서에는 오디오 및 비디오 컨텐츠가 포함되어 있지 않습니다.

PDF/A-1 규격은 두 가지 적합성, 즉 A와 B로 구성됩니다.두 수준 간의 주요 차이는 논리적 구조(접근성) 지원이며, 적합성 수준 B에는 필요하지 않습니다.적합성 수준에 관계없이 PDF/A-1은 생성된 PDF/A 문서 내에 모든 글꼴이 임베드되어 있음을 나타냅니다. 현재 유효성 검사(및 변환)에서는 PDF/A-1b만 지원됩니다.

이 토론의 목적을 위해 다음 DCX 문서가 사용되었다고 가정합니다.

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
         <DocumentInformation source="Loan.pdf" result="Loan_result.xml">
         <PDFAValidation compliance="PDF/A-1b" resultLevel="Detailed"                       ignoreUnusedResources="true" allowCertificationSignatures="true" />
     </DocumentInformation>
 </DDX>
```

이 DDX 문서 내에서, `DocumentInformation` 요소는 어셈블러 서비스에 입력 PDF 문서에 대한 정보를 반환하도록 지시합니다. 요소 `DocumentInformation` 내에서, `PDFAValidation` 요소는 입력 PDF 문서가 PDF/A와 호환되는지 여부를 어셈블러 서비스에 지시합니다.

Assembler 서비스는 입력 PDF 문서가 `PDFAConformance` 요소가 포함된 XML 문서 내에서 PDF/A와 호환되는지 여부를 지정하는 정보를 반환합니다. 입력 PDF 문서가 PDF/A와 호환되는 경우 `PDFAConformance` 요소 `isCompliant` 속성의 값은 `true`입니다. PDF 문서가 PDF/A 규격이 아닌 경우 `PDFAConformance` 요소의 `isCompliant` 속성 값은 `false`입니다.

>[!NOTE]
>
>이 섹션에 지정된 DDX 문서에 `DocumentInformation` 요소가 포함되어 있으므로 어셈블러 서비스는 PDF 문서 대신 XML 데이터를 반환합니다. 즉, 어셈블러 서비스는 PDF 문서를 구성하거나 분해하지 않습니다.XML 문서 내의 입력 PDF 문서에 대한 정보를 반환합니다.

>[!NOTE]
>
>어셈블러 서비스에 대한 자세한 내용은 AEM Forms [에 대한 서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDX 문서에 대한 자세한 내용은 어셈블러 서비스 [및 DCX 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 단계 요약 {#summary-of-steps}

PDF 문서가 PDF/A 규격인지 확인하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일 포함
1. PDF Assembler 클라이언트 만들기
1. 기존 DCX 문서를 참조합니다.
1. PDF/A 규정 준수를 확인하는 데 사용되는 PDF 문서를 참조합니다.
1. 런타임 옵션을 설정합니다.
1. PDF 문서에 대한 정보를 검색합니다.
1. 반환된 XML 문서를 저장합니다.

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

어셈블러 서비스 작업을 수행하려면 DCX 문서를 참조해야 합니다. 입력 PDF 문서가 PDF/A와 호환되는지 확인하려면 DCX 문서에 `PDFAValidation` 요소 내의 `DocumentInformation` 요소가 포함되어 있는지 확인합니다. 이 `PDFAValidation` 요소는 입력 PDF 문서가 PDF/A 호환 문서인지 여부를 지정하는 XML 문서를 어셈블러 서비스에 반환하도록 합니다.

**PDF/A 규정 준수를 확인하는 데 사용되는 PDF 문서 참조**

PDF 문서가 PDF/A 규격인지 확인하려면 PDF 문서를 참조하고 어셈블러 서비스로 전달해야 합니다.

**런타임 옵션 설정**

작업을 수행하는 동안 어셈블러 서비스의 동작을 제어하는 런타임 옵션을 설정할 수 있습니다. 예를 들어 오류가 발생하면 어셈블리 서비스에서 작업을 계속 처리하도록 하는 옵션을 설정할 수 있습니다. 설정할 수 있는 런타임 옵션에 대한 자세한 내용은 AEM Forms API 참조에서 `AssemblerOptionSpec` 클래스 [참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**PDF 문서에 대한 정보 검색**

Assembler 서비스 클라이언트를 만들고, DCX 문서를 참조하고, 대화형 PDF 문서를 참조하고, 런타임 옵션을 설정한 후 `invokeDDX` 작업을 호출할 수 있습니다. DCX 문서에 `DocumentInformation` 요소가 포함되어 있으므로 어셈블러 서비스는 PDF 문서 대신 XML 데이터를 반환합니다.

**반환된 XML 문서 저장**

어셈블러 서비스에서 반환하는 XML 문서는 입력 PDF 문서가 PDF/A 규격인지 여부를 지정합니다. 예를 들어 입력 PDF 문서가 PDF/A 규격이 아닌 경우 어셈블러 서비스는 다음 요소를 포함하는 XML 문서를 반환합니다.

```as3
 <PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Detailed" ignoreUnusedResources="true" allowCertificationSignatures="true">
```

XML 문서를 XML 파일로 저장하여 파일을 열고 결과를 볼 수 있습니다.

**참고 항목**

[Java API를 사용하여 문서가 PDF/A 규격인지 확인](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api)

[웹 서비스 API를 사용하여 문서가 PDF/A 규격인지 확인](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[프로그래밍 방식으로 PDF 문서 취합](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API를 사용하여 문서가 PDF/A 규격인지 확인 {#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api}

Assembler Service API(Java)를 사용하여 PDF 문서가 PDF/A 규격인지 확인합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-assembler-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. PDF Assembler 클라이언트 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 객체를 전달하여 `AssemblerServiceClient` 객체를 만듭니다 `ServiceClientFactory` .

1. 기존 DCX 문서를 참조합니다.

   * 생성자를 사용하고 DCX 파일의 위치를 지정하는 문자열 값을 전달하여 DCX 문서를 나타내는 `java.io.FileInputStream` 객체를 만듭니다. PDF 문서가 PDF/A를 준수하는지 확인하려면 DCX 문서에 `PDFAValidation` `DocumentInformation` 요소 내에 포함된 요소가 포함되어 있는지 확인합니다.
   * 생성자를 사용하여 객체를 전달하여 `com.adobe.idp.Document` 객체를 만듭니다 `java.io.FileInputStream` .

1. PDF/A 규정 준수를 확인하는 데 사용되는 PDF 문서를 참조합니다.

   * 생성자를 사용하여 `java.io.FileInputStream` 개체를 만들고 PDF/A 규정 준수를 확인하는 데 사용되는 PDF 문서의 위치를 전달하여 만듭니다.
   * 생성자를 사용하여 `com.adobe.idp.Document` 개체를 만들고 PDF 문서가 들어 있는 `java.io.FileInputStream` 개체를 전달합니다.
   * 생성자를 사용하여 입력 PDF 문서를 저장하는 데 사용되는 `java.util.Map` 개체를 `HashMap` 만듭니다.
   * 해당 `java.util.Map` `put` 메서드를 호출하고 다음 인수를 전달하여 개체에 항목을 추가합니다.

      * 키 이름을 나타내는 문자열 값입니다. 이 값은 DCX 문서에 지정된 소스 요소의 값과 일치해야 합니다. 예를 들어, 이 섹션에서 소개된 DCX 문서에 있는 소스 요소의 값은 Loan.pdf입니다.
      * 입력 PDF 문서를 포함하는 `com.adobe.idp.Document` 개체입니다.

1. 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 런타임 옵션을 저장하는 `AssemblerOptionSpec` 객체를 만듭니다.
   * 객체에 속하는 메서드를 호출하여 비즈니스 요구 사항을 충족하도록 런타임 옵션을 `AssemblerOptionSpec` 설정합니다. 예를 들어 오류가 발생할 때 어셈블리 서비스에서 작업을 계속 처리하도록 하려면 `AssemblerOptionSpec` 개체의 `setFailOnError` 메서드를 호출하고 전달합니다 `false`.

1. PDF 문서에 대한 정보를 검색합니다.

   객체의 `AssemblerServiceClient` `invokeDDX` 메서드를 호출하고 다음 필수 값을 전달합니다.

   * 사용할 DCX 문서를 나타내는 `com.adobe.idp.Document` 개체
   * PDF/A 규정 준수를 확인하는 데 사용되는 입력 PDF 파일이 포함된 `java.util.Map` 개체
   * 런타임 옵션을 지정하는 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 개체
   이 `invokeDDX` 메서드는 입력 PDF 문서가 PDF/A 호환 문서인지 여부를 지정하는 XML 데이터가 포함된 `com.adobe.livecycle.assembler.client.AssemblerResult` 개체를 반환합니다.

1. 반환된 XML 문서를 저장합니다.

   입력 PDF 문서가 PDF/A 문서인지 여부를 지정하는 XML 데이터를 얻으려면 다음 작업을 수행하십시오.

   * 객체의 메서드를 `AssemblerResult` 호출합니다 `getDocuments` . 이렇게 하면 `java.util.Map` 개체가 반환됩니다.
   * 결과 개체를 찾을 때까지 `java.util.Map` `com.adobe.idp.Document` 개체를 반복합니다.
   * XML 문서를 추출하려면 `com.adobe.idp.Document` 개체의 `copyToFile` 메서드를 호출합니다. XML 데이터를 XML 파일로 저장해야 합니다.

**참고 항목**

[빠른 시작(SOAP 모드):Java API를 사용하여 문서가 PDF/A와 호환되는지](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-determining-whether-a-document-is-pdf-a-compliant-using-the-java-api) 확인(SOAP 모드)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API를 사용하여 문서가 PDF/A 규격인지 확인 {#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api}

Assembler Service API(웹 서비스)를 사용하여 PDF 문서가 PDF/A 규격인지 확인합니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`Adobe

   >[!NOTE]
   >
   >AEM `localhost` Forms를 호스팅하는 서버의 IP 주소로 대체합니다.

1. PDF Assembler 클라이언트 만들기

   * 기본 생성자를 사용하여 `AssemblerServiceClient` 객체를 만듭니다.
   * 생성자를 사용하여 `AssemblerServiceClient.Endpoint.Address` 객체를 만듭니다 `System.ServiceModel.EndpointAddress` . WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). 속성을 사용할 필요는 `lc_version` 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
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
   * 바이트 배열의 내용으로 해당 `BLOB` `MTOM` 필드를 할당하여 개체를 채웁니다.

1. PDF/A 규정 준수를 확인하는 데 사용되는 PDF 문서를 참조합니다.

   * 생성자를 사용하여 `BLOB` 객체를 만듭니다. 이 `BLOB` 개체는 입력 PDF 문서를 저장하는 데 사용됩니다.
   * 생성자를 호출하고 입력 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * 개체의 내용을 저장하는 바이트 배열을 `System.IO.FileStream` 만듭니다. 개체의 `System.IO.FileStream` `Length` 속성을 가져와 바이트 배열의 크기를 결정할 수 있습니다.
   * 객체의 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다. `System.IO.FileStream` `Read`
   * 바이트 배열의 컨텐츠로 해당 `BLOB` `MTOM` 속성을 할당하여 객체를 채웁니다.
   * 객체를 `MyMapOf_xsd_string_To_xsd_anyType` 만듭니다. 이 컬렉션 개체는 PDF 문서를 저장하는 데 사용됩니다.
   * 객체를 `MyMapOf_xsd_string_To_xsd_anyType_Item` 만듭니다.
   * 키 이름을 나타내는 문자열 값을 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체의 `key` 필드에 지정합니다. 이 값은 DCX 문서에 지정된 PDF 소스 요소의 값과 일치해야 합니다.
   * PDF 문서를 저장하는 `BLOB` 개체를 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체의 `value` 필드에 할당합니다.
   * 개체에 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체를 추가합니다 `MyMapOf_xsd_string_To_xsd_anyType` . 객체의 `MyMapOf_xsd_string_To_xsd_anyType` 메서드를 호출하고 `Add` `MyMapOf_xsd_string_To_xsd_anyType` 객체를 전달합니다.

1. 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 런타임 옵션을 저장하는 `AssemblerOptionSpec` 객체를 만듭니다.
   * 객체에 속하는 데이터 멤버에 값을 할당하여 비즈니스 요구 사항에 맞게 런타임 옵션을 설정할 수 `AssemblerOptionSpec` 있습니다. 예를 들어 오류가 발생할 때 어셈블리 서비스에서 작업을 계속 처리하도록 하려면 개체의 `false` `AssemblerOptionSpec` `failOnError` 데이터 멤버에 할당합니다.

1. PDF 문서에 대한 정보를 검색합니다.

   객체의 `AssemblerServiceService` `invoke` 메서드를 호출하고 다음 값을 전달합니다.

   * DCX 문서를 나타내는 `BLOB` 개체입니다.
   * 입력 PDF 문서를 포함하는 `MyMapOf_xsd_string_To_xsd_anyType` 개체입니다. 해당 키는 PDF 소스 파일의 이름과 일치해야 하며, 해당 값은 입력 PDF 파일에 해당하는 `BLOB` 개체여야 합니다.
   * 런타임 옵션을 지정하는 `AssemblerOptionSpec` 객체입니다.
   이 `invoke` 메서드는 입력 PDF 문서가 PDF/A 문서인지 여부를 지정하는 XML 데이터가 포함된 `AssemblerResult` 개체를 반환합니다.

1. 반환된 XML 문서를 저장합니다.

   입력 PDF 문서가 PDF/A 문서인지 여부를 지정하는 XML 데이터를 얻으려면 다음 작업을 수행하십시오.

   * 입력 PDF 문서가 PDF/A 문서인지 여부를 지정하는 XML 데이터가 들어 있는 `AssemblerResult` `documents` `Map` 개체인 개체의 필드에 액세스합니다.
   * 객체를 반복하여 각 결과 문서를 가져옵니다. `Map` 그런 다음 해당 스토리지 멤버의 값을 a로 `BLOB`캐스팅하십시오.
   * 객체의 필드에 액세스하여 XML 데이터를 나타내는 이진 데이터를 `BLOB` 추출합니다 `MTOM` . 이 필드에는 XML 파일로 작성할 수 있는 바이트 배열이 저장됩니다.

**참고 항목**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
