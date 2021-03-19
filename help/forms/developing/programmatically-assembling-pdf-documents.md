---
title: 프로그래밍 방식으로 PDF 문서 취합
seo-title: 프로그래밍 방식으로 PDF 문서 취합
description: Assembler 서비스 API를 사용하여 Java API 및 웹 서비스 API를 사용하여 여러 PDF 문서를 하나의 PDF 문서로 결합합니다.
seo-description: Assembler 서비스 API를 사용하여 Java API 및 웹 서비스 API를 사용하여 여러 PDF 문서를 하나의 PDF 문서로 결합합니다.
uuid: aa3f8f39-1fbc-48d0-82ff-6caaadf125fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ebe8136b-2a79-4035-b9d5-aa70a5bbd4af
role: 개발자
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2153'
ht-degree: 0%

---


# 프로그래밍 방식으로 PDF 문서 정리 {#programmatically-assembling-pdf-documents}

**이 문서의 샘플과 예는 JEE 환경의 AEM Forms에만 해당됩니다.**

Assembler Service API를 사용하여 여러 PDF 문서를 하나의 PDF 문서로 결합할 수 있습니다. 다음 그림은 세 개의 PDF 문서를 하나의 PDF 문서로 병합하는 것을 보여줍니다.

![pa_pa_document_assembly](assets/pa_pa_document_assembly.png)

두 개 이상의 PDF 문서를 하나의 PDF 문서로 취합하려면 DCX 문서가 필요합니다. DDX 문서에서는 Assembler 서비스에서 만드는 PDF 문서를 설명합니다. 즉, DDX 문서는 어셈블러 서비스에 수행할 작업을 지시합니다.

이 토론의 목적으로 다음 DDX 문서를 사용한다고 가정합니다.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     <PDF result="out.pdf">
         <PDF source="map.pdf" />
         <PDF source="directions.pdf" />
     </PDF>
 </DDX>
```

이 DCX 문서는 *map.pdf* 및 *directions.pdf*&#x200B;라는 두 개의 PDF 문서를 하나의 PDF 문서로 병합합니다.

>[!NOTE]
>
>PDF 문서를 분해하는 DCX 문서를 보려면 [프로그래밍 방식으로 PDF 문서 정리](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)를 참조하십시오.

>[!NOTE]
>
>어셈블러 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

>[!NOTE]
>
>DCX 문서에 대한 자세한 내용은 [어셈블러 서비스 및 DCX 참조](https://www.adobe.com/go/learn_aemforms_ddx_63)를 참조하십시오.

## 웹 서비스 {#considerations-when-invoking-assembler-service-using-web-services}를 사용하여 어셈블러 서비스를 호출할 때의 고려 사항

큰 문서를 조합하는 동안 머리말과 꼬리말을 추가할 때 `OutOfMemory` 오류가 발생할 수 있으며 파일이 어셈블되지 않습니다. 이 문제가 발생할 가능성을 줄이려면 다음 예와 같이 `DDXProcessorSetting` 요소를 DCX 문서에 추가하십시오.

`<DDXProcessorSetting name="checkpoint" value="2000" />`

이 요소를 `DDX` 요소의 자식으로 추가하거나 `PDF result` 요소의 자식으로 추가할 수 있습니다. 이 설정의 기본값은 0(영)입니다. 이 값은 체크 포인팅을 해제하며 DCX는 `DDXProcessorSetting` 요소가 없는 것처럼 동작합니다. `OutOfMemory` 오류가 발생한 경우 값을 정수로 설정해야 할 수 있습니다(일반적으로 500~5000). 체크포인트 값이 작으면 체크포인트가 더 자주 발생합니다.

## {#summary-of-steps} 단계 요약

여러 PDF 문서에서 단일 PDF 문서를 취합하려면 다음 작업을 수행합니다.

1. 프로젝트 파일 포함
1. PDF Assembler 클라이언트를 만듭니다.
1. 기존 DCX 문서를 참조합니다.
1. 입력 PDF 문서를 참조합니다.
1. 런타임 옵션을 설정합니다.
1. 입력 PDF 문서를 조합합니다.
1. 결과를 추출합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

다음 JAR 파일을 프로젝트의 클래스 경로에 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar (AEM Forms이 JBoss에 배포된 경우 필수)

AEM Forms이 JBoss가 아닌 지원되는 J2EE 응용 프로그램 서버에 배포되는 경우 adobe-utilities.jar 및 jbossall-client.jar 파일을 AEM Forms이 배포된 J2EE 응용 프로그램 서버에 해당하는 JAR 파일로 대체해야 합니다.

**PDF Assembler 클라이언트 만들기**

어셈블리 작업을 프로그래밍 방식으로 수행하려면 먼저 어셈블러 클라이언트를 만들어야 합니다.

**기존 DCX 문서 참조**

PDF 문서를 조합하려면 DCX 문서를 참조해야 합니다. 예를 들어 이 섹션에 도입된 DDX 문서를 생각해 보십시오. 이 DDC 문서는 두 개의 PDF 문서를 하나의 PDF 문서로 병합하도록 어셈블러 서비스에 지시합니다.

**입력 PDF 문서 참조**

어셈블러 서비스로 전달할 입력 PDF 문서를 참조합니다. 예를 들어 Map and Directions라는 두 개의 입력 PDF 문서를 전달하려면 해당 PDF 파일을 전달해야 합니다.

map.pdf 파일과 directions.pdf 파일을 모두 컬렉션 개체에 배치해야 합니다. 키 이름은 DCX 문서의 PDF 소스 속성 값과 일치해야 합니다. DCX 문서의 키와 소스 특성이 일치할 경우 PDF 파일의 이름이 무엇인지에 상관 없습니다.

>[!NOTE]
>
>`invokeDDX` 작업을 호출하면 컬렉션 객체가 포함된 `AssemblerResult` 객체가 반환됩니다. 이 작업은 두 개 이상의 입력 PDF 문서를 어셈블러 서비스로 전달할 때 사용됩니다. 그러나 입력 PDF를 어셈블러 서비스로 한 개만 전달하고 하나의 반환 문서만 예상하는 경우에는 `invokeOneDocument` 작업을 호출합니다. 이 작업을 호출하면 단일 문서가 반환됩니다. 이 작업 사용에 대한 자세한 내용은 [암호화된 PDF 문서 정리](/help/forms/developing/assembling-encrypted-pdf-documents.md#assembling-encrypted-pdf-documents)를 참조하십시오.

**런타임 옵션 설정**

작업을 수행하는 동안 어셈블리 서비스의 동작을 제어하는 런타임 옵션을 설정할 수 있습니다. 예를 들어 오류가 발생하면 어셈블리 서비스에 작업을 계속 처리하도록 하는 옵션을 설정할 수 있습니다. 설정할 수 있는 런타임 옵션에 대한 자세한 내용은 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)의 `AssemblerOptionSpec` 클래스 참조를 참조하십시오.

**입력 PDF 문서 조합**

서비스 클라이언트를 만들고 DDX 파일을 참조하고, 입력 PDF 문서를 저장하는 컬렉션 개체를 만들고, 런타임 옵션을 설정한 후 DDC 작업을 호출할 수 있습니다. 이 섹션에 지정된 DDC 문서를 사용할 때 map.pdf 및 direction.pdf 파일은 하나의 PDF 문서로 병합됩니다.

**결과 추출**

Assembler 서비스는 `AssemblerResult` 개체에서 가져올 수 있고 작업 결과를 포함하는 `java.util.Map` 개체를 반환합니다. 반환된 `java.util.Map` 개체에는 결과 문서와 예외가 포함되어 있습니다.

다음 표는 반환된 `java.util.Map` 개체에 위치할 수 있는 일부 키 값과 개체 유형을 요약해 놓은 것입니다.

<table>
 <thead>
  <tr>
   <th><p>키 값</p></th>
   <th><p>개체 유형</p></th>
   <th><p>설명</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code><i>documentName</i></code></p></td>
   <td><p><code>com.adobe.idp.Document</code></p></td>
   <td><p>DCX 결과 요소에 지정된 결과 문서를 포함합니다.</p></td>
  </tr>
  <tr>
   <td><p><code><i>documentName</i></code></p></td>
   <td><p><code>Exception</code></p></td>
   <td><p>문서에 대한 예외 포함</p></td>
  </tr>
  <tr>
   <td><p><code>OutputMapConstants.LOG_NAME</code></p></td>
   <td><p><code>com.adobe.idp.Documen</code></p></td>
   <td><p>작업 로그를 포함합니다.</p></td>
  </tr>
 </tbody>
</table>

**참고 항목**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[프로그래밍 방식으로 PDF 문서 분리](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Java API {#assemble-pdf-documents-using-the-java-api}를 사용하여 PDF 문서 조합

Assembler Service API(Java)를 사용하여 PDF 문서를 조합합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-assembler-client.jar 등의 클라이언트 JAR 파일을 포함합니다.

1. PDF Assembler 클라이언트를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 `AssemblerServiceClient` 개체를 만들고 `ServiceClientFactory` 개체를 전달합니다.

1. 기존 DCX 문서를 참조합니다.

   * 생성자를 사용하여 DCX 문서를 나타내는 `java.io.FileInputStream` 객체를 만들고 DCX 파일의 위치를 지정하는 문자열 값을 전달합니다.
   * 생성자를 사용하여 `com.adobe.idp.Document` 개체를 만들고 `java.io.FileInputStream` 개체를 전달합니다.

1. 입력 PDF 문서를 참조합니다.

   * `HashMap` 생성자를 사용하여 입력 PDF 문서를 저장하는 데 사용되는 `java.util.Map` 객체를 만듭니다.
   * 각 입력 PDF 문서에 대해 생성자를 사용하여 입력 PDF 문서의 위치를 전달하여 `java.io.FileInputStream` 개체를 만듭니다.
   * 각 입력 PDF 문서에 대해 `com.adobe.idp.Document` 개체를 만들고 PDF 문서가 포함된 `java.io.FileInputStream` 개체를 전달합니다.
   * 각 입력 문서에 대해 `put` 메서드를 호출하고 다음 인수를 전달하여 `java.util.Map` 객체에 항목을 추가합니다.

      * 키 이름을 나타내는 문자열 값입니다. 이 값은 DCX 문서에 지정된 PDF 소스 요소의 값과 일치해야 합니다.
      * 소스 PDF 문서를 포함하는 `com.adobe.idp.Document` 개체(또는 여러 문서를 지정하는 `java.util.List` 개체).

1. 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 런타임 옵션을 저장하는 `AssemblerOptionSpec` 객체를 만듭니다.
   * `AssemblerOptionSpec` 개체에 속하는 메서드를 호출하여 비즈니스 요구 사항을 충족하도록 런타임 옵션을 설정합니다. 예를 들어 오류가 발생할 때 어셈블리 서비스에서 작업을 계속 처리하도록 하려면 `AssemblerOptionSpec` 개체의 `setFailOnError` 메서드를 호출하고 `false`를 전달합니다.

1. 입력 PDF 문서를 조합합니다.

   `AssemblerServiceClient` 객체의 `invokeDDX` 메서드를 호출하고 다음 필수 값을 전달합니다.

   * 사용할 DCX 문서를 나타내는 `com.adobe.idp.Document` 개체
   * 어셈블할 입력 PDF 파일을 포함하는 `java.util.Map` 개체
   * 기본 글꼴 및 작업 로그 수준을 포함하여 런타임 옵션을 지정하는 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 개체

   `invokeDDX` 메서드는 작업 결과와 발생한 예외가 포함된 `com.adobe.livecycle.assembler.client.AssemblerResult` 개체를 반환합니다.

1. 결과를 추출합니다.

   새로 만든 PDF 문서를 얻으려면 다음 작업을 수행합니다.

   * `AssemblerResult` 객체의 `getDocuments` 메서드를 호출합니다. `java.util.Map` 객체를 반환합니다.
   * 결과 `com.adobe.idp.Document` 개체를 찾을 때까지 `java.util.Map` 개체를 반복합니다. DCX 문서에 지정된 PDF 결과 요소를 사용하여 문서를 가져올 수 있습니다.
   * `com.adobe.idp.Document` 개체의 `copyToFile` 메서드를 호출하여 PDF 문서를 추출합니다.

   >[!NOTE]
   >
   >`LOG_LEVEL`이(가) 로그를 생성하도록 설정된 경우 `AssemblerResult` 객체의 `getJobLog` 메서드를 사용하여 로그를 추출할 수 있습니다.

**참고 항목**

[빠른 시작(SOAP 모드):Java API를 사용하여 PDF 문서 취합](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API {#assemble-pdf-documents-using-the-web-service-api}를 사용하여 PDF 문서 조합

Assembler Service API(웹 서비스)를 사용하여 PDF 문서를 조합합니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다.`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꿉니다.

1. PDF Assembler 클라이언트를 만듭니다.

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
   * 생성자를 호출하고 DCX 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 객체를 만듭니다.
   * `System.IO.FileStream` 객체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 객체의 `Length` 속성을 가져와 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 객체의 `Read` 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * 바이트 배열의 내용으로 `MTOM` 속성을 할당하여 `BLOB` 객체를 채웁니다.

1. 입력 PDF 문서를 참조합니다.

   * 각 입력 PDF 문서에 대해 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 입력 PDF 문서를 저장하는 데 사용됩니다.
   * 생성자를 호출하고 입력 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 객체를 만듭니다.
   * `System.IO.FileStream` 객체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 객체의 `Length` 속성을 가져와 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 객체의 `Read` 메서드를 호출하여 바이트 배열을 스트림 데이터로 채웁니다. 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달합니다.
   * 바이트 배열의 내용으로 `MTOM` 필드를 할당하여 `BLOB` 개체를 채웁니다.
   * `MyMapOf_xsd_string_To_xsd_anyType` 개체를 만듭니다. 이 컬렉션 개체는 입력 PDF 문서를 저장하는 데 사용됩니다.
   * 각 입력 PDF 문서에 대해 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체를 만듭니다. 예를 들어 2개의 입력 PDF 문서를 사용하는 경우 2개의 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체를 만듭니다.
   * 키 이름을 나타내는 문자열 값을 `MyMapOf_xsd_string_To_xsd_anyType_Item` 객체의 `key` 필드에 지정합니다. 이 값은 DCX 문서에 지정된 PDF 소스 요소의 값과 일치해야 합니다. 각 입력 PDF 문서에 대해 이 작업을 수행합니다.
   * PDF 문서를 저장하는 `BLOB` 개체를 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체의 `value` 필드에 할당합니다. 각 입력 PDF 문서에 대해 이 작업을 수행합니다.
   * `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체를 `MyMapOf_xsd_string_To_xsd_anyType` 개체에 추가합니다. `MyMapOf_xsd_string_To_xsd_anyType` 객체의 `Add` 메서드를 호출하고 `MyMapOf_xsd_string_To_xsd_anyType` 객체를 전달합니다. 각 입력 PDF 문서에 대해 이 작업을 수행합니다.

1. 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 런타임 옵션을 저장하는 `AssemblerOptionSpec` 객체를 만듭니다.
   * `AssemblerOptionSpec` 개체에 속하는 데이터 멤버에 값을 할당하여 비즈니스 요구 사항에 맞게 런타임 옵션을 설정합니다. 예를 들어 오류가 발생할 때 어셈블리 서비스에서 작업을 계속 처리하도록 하려면 `false`을(를) `AssemblerOptionSpec` 개체의 `failOnError` 데이터 멤버에 할당합니다.

1. 입력 PDF 문서를 조합합니다.

   `AssemblerServiceClient` 객체의 `invoke` 메서드를 호출하고 다음 값을 전달합니다.

   * DCX 문서를 나타내는 `BLOB` 객체입니다.
   * 입력 PDF 문서를 포함하는 `mapItem` 배열입니다. 해당 키는 PDF 소스 파일의 이름과 일치해야 하며 해당 값은 해당 파일에 해당하는 `BLOB` 객체여야 합니다.
   * 런타임 옵션을 지정하는 `AssemblerOptionSpec` 객체입니다.

   `invoke` 메서드는 작업 결과와 발생한 예외가 포함된 `AssemblerResult` 개체를 반환합니다.

1. 결과를 추출합니다.

   새로 만든 PDF 문서를 얻으려면 다음 작업을 수행합니다.

   * 결과 PDF 문서를 포함하는 `Map` 개체인 `AssemblerResult` 개체의 `documents` 필드에 액세스합니다.
   * 결과 문서의 이름과 일치하는 키를 찾을 때까지 `Map` 개체를 반복합니다. 그런 다음 해당 배열 멤버의 `value`을(를) `BLOB`로 캐스팅합니다.
   * PDF 문서의 `BLOB` 개체의 `MTOM` 속성에 액세스하여 이진 데이터를 추출합니다. PDF 파일에 기록할 수 있는 바이트 배열을 반환합니다.

   >[!NOTE]
   >
   >`LOG_LEVEL`이(가) 로그를 생성하도록 설정된 경우 `AssemblerResult` 객체의 `jobLog` 데이터 멤버 값을 가져와 로그를 추출할 수 있습니다.

**참고 항목**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
