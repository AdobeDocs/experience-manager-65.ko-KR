---
title: 프로그래밍 방식으로 PDF 문서 취합
seo-title: 프로그래밍 방식으로 PDF 문서 취합
description: 'null'
seo-description: 'null'
uuid: aa3f8f39-1fbc-48d0-82ff-6caaadf125fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ebe8136b-2a79-4035-b9d5-aa70a5bbd4af
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2092'
ht-degree: 0%

---


# 프로그래밍 방식으로 PDF 문서 취합 {#programmatically-assembling-pdf-documents}

Assembler Service API를 사용하여 여러 PDF 문서를 하나의 PDF 문서로 결합할 수 있습니다. 다음 그림은 세 개의 PDF 문서를 하나의 PDF 문서로 병합하는 것을 보여줍니다.

![pa_pa_document_assembly](assets/pa_pa_document_assembly.png)

두 개 이상의 PDF 문서를 하나의 PDF 문서로 취합하려면 DDX 문서가 필요합니다. DDX 문서에서는 어셈블러 서비스에서 만드는 PDF 문서를 설명합니다. 즉, DCX 문서는 어셈블러 서비스에 수행할 작업을 지시합니다.

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

이 DDX 문서는 *map.pdf* 및 *directions.pdf* 라는 두 개의 PDF 문서를 하나의 PDF 문서로 병합합니다.

>[!NOTE]
>
>PDF 문서를 분해하는 DCX 문서를 보려면 프로그램 [으로 PDF 문서 조합 해제를 참조하십시오](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents).

>[!NOTE]
>
>어셈블러 서비스에 대한 자세한 내용은 AEM Forms에 대한 [서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDX 문서에 대한 자세한 내용은 어셈블러 서비스 [및 DDX 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 웹 서비스를 사용하여 어셈블러 서비스를 호출할 때의 고려 사항 {#considerations-when-invoking-assembler-service-using-web-services}

큰 문서를 조합하는 동안 머리말과 꼬리말을 추가할 때 오류가 발생할 수 있으며 파일이 어셈블되지 않습니다. `OutOfMemory` 이 문제가 발생할 가능성을 줄이려면 다음 예와 같이 DDX 문서에 `DDXProcessorSetting` 요소를 추가하십시오.

`<DDXProcessorSetting name="checkpoint" value="2000" />`

이 요소를 요소의 하위 또는 요소의 하위 `DDX` 로 추가할 수 `PDF result` 있습니다. 이 설정의 기본값은 0(영)으로, 체크포인트를 비활성화하고 DDC가 요소가 없는 것처럼 동작합니다 `DDXProcessorSetting` . 오류가 발생한 경우 값을 정수로 설정해야 할 수 있습니다(일반적으로 500에서 5000 사이). `OutOfMemory` 체크포인트 값이 작으면 체크포인트가 더 자주 발생합니다.

## 단계 요약 {#summary-of-steps}

여러 PDF 문서에서 단일 PDF 문서를 취합하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일 포함
1. PDF 어셈블러 클라이언트 만들기
1. 기존 DDX 문서를 참조합니다.
1. 입력 PDF 문서를 참조합니다.
1. 런타임 옵션을 설정합니다.
1. 입력 PDF 문서 조합
1. 결과를 추출합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(AEM Forms이 JBoss에 배포된 경우 필요)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필요)

AEM Forms이 JBoss 이외의 지원되는 J2EE 응용 프로그램 서버에 배포된 경우 adobe-utilities.jar 및 jbossall-client.jar 파일을 AEM Forms이 배포된 J2EE 응용 프로그램 서버에 고유한 JAR 파일로 교체해야 합니다.

**PDF 어셈블러 클라이언트 만들기**

어셈블리 작업을 프로그래밍 방식으로 수행하려면 먼저 어셈블러 클라이언트를 만들어야 합니다.

**기존 DCX 문서 참조**

PDF 문서를 조합하려면 DDX 문서를 참조해야 합니다. 예를 들어 이 섹션에 도입된 DDX 문서를 생각해 보십시오. 이 DDX 문서는 두 개의 PDF 문서를 하나의 PDF 문서로 병합하도록 어셈블리 서비스에 지시합니다.

**참조 입력 PDF 문서**

어셈블러 서비스로 전달할 입력 PDF 문서를 참조합니다. 예를 들어 Map and Directions라는 두 개의 입력 PDF 문서를 전달하려면 해당 PDF 파일을 전달해야 합니다.

map.pdf 파일과 directions.pdf 파일을 모두 컬렉션 개체에 배치해야 합니다. 키 이름은 DDX 문서의 PDF 소스 속성 값과 일치해야 합니다. DDX 문서의 키와 소스 특성이 일치하는 경우 PDF 파일의 이름이 무엇인지는 중요하지 않습니다.

>[!NOTE]
>
>컬렉션 개체를 포함하는 `AssemblerResult` 개체는 작업을 호출하는 경우 `invokeDDX` 반환됩니다. 이 작업은 두 개 이상의 입력 PDF 문서를 어셈블러 서비스에 전달할 때 사용됩니다. 그러나 입력 PDF를 어셈블러 서비스에 하나만 전달하면 하나의 반환 문서만 예상할 경우 `invokeOneDocument` 작업을 호출합니다. 이 작업을 호출하면 단일 문서가 반환됩니다. 이 작업 사용에 대한 자세한 내용은 암호화된 PDF 문서 [합성을 참조하십시오](/help/forms/developing/assembling-encrypted-pdf-documents.md#assembling-encrypted-pdf-documents).

**런타임 옵션 설정**

작업을 수행하는 동안 어셈블러 서비스의 동작을 제어하는 런타임 옵션을 설정할 수 있습니다. 예를 들어 오류가 발생한 경우 어셈블리 서비스에서 작업을 계속 처리하도록 하는 옵션을 설정할 수 있습니다. 설정할 수 있는 런타임 옵션에 대한 자세한 내용은 `AssemblerOptionSpec` AEM Forms API 참조에서 [클래스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**입력 PDF 문서 조합**

서비스 클라이언트를 만들고 DDX 파일을 참조하고, 입력 PDF 문서를 저장하는 컬렉션 개체를 만들고, 런타임 옵션을 설정한 후 DDX 작업을 호출할 수 있습니다. 이 섹션에 지정된 DDX 문서를 사용하는 경우 map.pdf 및 direction.pdf 파일이 하나의 PDF 문서로 병합됩니다.

**결과 추출**

어셈블리 서비스는 개체에서 가져올 수 있고 작업 결과를 포함하는 개체를 `java.util.Map` `AssemblerResult` 반환합니다. 반환된 `java.util.Map` 객체에는 결과 문서와 예외가 포함됩니다.

다음 표에는 반환된 개체에 위치할 수 있는 몇 가지 키 값과 개체 유형이 요약되어 `java.util.Map` 있습니다.

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
   <td><p>DDX 결과 요소에 지정된 결과 문서를 포함합니다.</p></td>
  </tr>
  <tr>
   <td><p><code><i>documentName</i></code></p></td>
   <td><p><code>Exception</code></p></td>
   <td><p>문서에 대한 예외 포함</p></td>
  </tr>
  <tr>
   <td><p><code>OutputMapConstants.LOG_NAME</code></p></td>
   <td><p><code>com.adobe.idp.Documen</code></p></td>
   <td><p>작업 로그 포함</p></td>
  </tr>
 </tbody>
</table>

**참고 항목**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[프로그래밍 방식으로 PDF 문서 분리](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Java API를 사용하여 PDF 문서 조합 {#assemble-pdf-documents-using-the-java-api}

Assembler Service API(Java)를 사용하여 PDF 문서를 어셈블합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-assembler-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. PDF 어셈블러 클라이언트 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 개체를 `AssemblerServiceClient` 만들고 개체를 `ServiceClientFactory` 전달합니다.

1. 기존 DDX 문서를 참조합니다.

   * 생성자를 사용하여 DCX 문서를 나타내는 `java.io.FileInputStream` 개체를 만들고 DDX 파일의 위치를 지정하는 문자열 값을 전달합니다.
   * 생성자를 사용하여 개체를 `com.adobe.idp.Document` 만들고 개체를 `java.io.FileInputStream` 전달합니다.

1. 입력 PDF 문서를 참조합니다.

   * 생성자를 사용하여 입력 PDF 문서를 저장하는 데 사용되는 `java.util.Map` 개체를 `HashMap` 만듭니다.
   * 각 입력 PDF 문서에 대해 생성자를 사용하여 입력 PDF 문서의 위치를 전달하여 `java.io.FileInputStream` 개체를 만듭니다.
   * 입력된 각 PDF 문서에 대해 개체를 만들어 PDF 문서가 포함된 `com.adobe.idp.Document` `java.io.FileInputStream` 개체를 전달합니다.
   * 각 입력 문서에 대해 해당 메서드를 호출하고 다음 인수를 전달하여 `java.util.Map` 개체에 `put` 항목을 추가합니다.

      * 키 이름을 나타내는 문자열 값입니다. 이 값은 DCX 문서에 지정된 PDF 소스 요소의 값과 일치해야 합니다.
      * 소스 PDF 문서를 포함하는 `com.adobe.idp.Document` 개체(또는 여러 문서를 지정하는 `java.util.List` 개체)입니다.

1. 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 런타임 옵션을 저장하는 `AssemblerOptionSpec` 객체를 만듭니다.
   * 개체에 속하는 메서드를 호출하여 비즈니스 요구 사항에 맞게 런타임 옵션을 `AssemblerOptionSpec` 설정합니다. 예를 들어 오류가 발생할 때 어셈블리 서비스에서 작업을 계속 처리하도록 지정하려면 `AssemblerOptionSpec` 개체의 `setFailOnError` 메서드를 호출하고 전달합니다 `false`.

1. 입력 PDF 문서 조합

   개체의 `AssemblerServiceClient` `invokeDDX` 메서드를 호출하고 다음 필수 값을 전달합니다.

   * 사용할 DCX 문서를 나타내는 `com.adobe.idp.Document` 개체
   * 어셈블할 입력 PDF 파일이 포함된 `java.util.Map` 개체
   * 기본 글꼴 및 작업 로그 수준을 포함하여 런타임 옵션을 지정하는 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 개체

   이 `invokeDDX` `com.adobe.livecycle.assembler.client.AssemblerResult` 메서드는 작업 결과와 발생한 예외를 포함하는 개체를 반환합니다.

1. 결과를 추출합니다.

   새로 만든 PDF 문서를 얻으려면 다음 작업을 수행하십시오.

   * 개체의 `AssemblerResult` 메서드를 `getDocuments` 호출합니다. 그러면 `java.util.Map` 개체가 반환됩니다.
   * 결과 개체를 찾을 때까지 개체 `java.util.Map` 를 반복하십시오 `com.adobe.idp.Document` . DDX 문서에 지정된 PDF 결과 요소를 사용하여 문서를 가져올 수 있습니다.
   * PDF 문서 `com.adobe.idp.Document` 를 추출하려면 개체의 `copyToFile` 방법을 불러옵니다.

   >[!NOTE]
   >
   >로그를 생성하도록 `LOG_LEVEL` 설정된 경우 `AssemblerResult` 객체의 `getJobLog` 방법을 사용하여 로그를 추출할 수 있습니다.

**참고 항목**

[빠른 시작(SOAP 모드): Java API를 사용하여 PDF 문서 취합](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API를 사용하여 PDF 문서 조합 {#assemble-pdf-documents-using-the-web-service-api}

Assembler Service API(웹 서비스)를 사용하여 PDF 문서 조합:

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Forms `localhost` 를 호스팅하는 서버의 IP 주소로 대체합니다.

1. PDF 어셈블러 클라이언트 만들기

   * 기본 생성자를 사용하여 `AssemblerServiceClient` 개체를 만듭니다.
   * 생성자를 사용하여 `AssemblerServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). 속성을 사용할 필요는 `lc_version` 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.
   * 필드의 값을 `System.ServiceModel.BasicHttpBinding` 가져와 개체를 `AssemblerServiceClient.Endpoint.Binding` 만듭니다. 반환 값을 다음으로 캐스팅합니다 `BasicHttpBinding`.
   * 개체 `System.ServiceModel.BasicHttpBinding` 필드를 (으)로 `MessageEncoding` 설정합니다 `WSMessageEncoding.Mtom`. 이 값을 사용하면 MTOM이 사용됩니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM 양식 사용자 이름을 지정합니다 `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * 해당 암호 값을 필드에 지정합니다 `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * 필드에 상수 값 `HttpClientCredentialType.Basic` 을 지정합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 필드에 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly` 을 지정합니다 `BasicHttpBindingSecurity.Security.Mode`.

1. 기존 DDX 문서를 참조합니다.

   * 생성자를 사용하여 `BLOB` 개체를 만듭니다. 이 `BLOB` 개체는 DDX 문서를 저장하는 데 사용됩니다.
   * 생성자를 호출하고 DDX 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * 개체의 내용을 저장하는 바이트 배열을 `System.IO.FileStream` 만듭니다. 개체의 속성을 가져와 바이트 배열의 크기를 결정할 수 `System.IO.FileStream` `Length` 있습니다.
   * 개체의 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열 `System.IO.FileStream` `Read` 을 스트림 데이터로 채웁니다.
   * 바이트 배열의 컨텐츠로 해당 `BLOB` `MTOM` 속성을 지정하여 개체를 채웁니다.

1. 입력 PDF 문서를 참조합니다.

   * 각 입력 PDF 문서에 대해 생성자를 사용하여 `BLOB` 개체를 만듭니다. 이 `BLOB` 개체는 입력 PDF 문서를 저장하는 데 사용됩니다.
   * 생성자를 호출하고 입력 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * 개체의 내용을 저장하는 바이트 배열을 `System.IO.FileStream` 만듭니다. 개체의 속성을 가져와 바이트 배열의 크기를 결정할 수 `System.IO.FileStream` `Length` 있습니다.
   * 개체의 메서드를 호출하여 바이트 배열을 스트림 데이터로 `System.IO.FileStream` 채웁니다 `Read` . 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 바이트 배열의 내용으로 해당 `BLOB` `MTOM` 필드를 할당하여 개체를 채웁니다.
   * 개체를 `MyMapOf_xsd_string_To_xsd_anyType` 만듭니다. 이 컬렉션 개체는 입력 PDF 문서를 저장하는 데 사용됩니다.
   * 각 입력 PDF 문서에 대해 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체를 만듭니다. 예를 들어 두 개의 입력 PDF 문서를 사용하는 경우 두 개의 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체를 만듭니다.
   * 키 이름을 나타내는 문자열 값을 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체의 `key` 필드에 할당합니다. 이 값은 DCX 문서에 지정된 PDF 소스 요소의 값과 일치해야 합니다. 각 입력 PDF 문서에 대해 이 작업을 수행합니다.
   * PDF 문서를 저장하는 `BLOB` 개체를 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체 `value` 필드에 할당합니다. 각 입력 PDF 문서에 대해 이 작업을 수행합니다.
   * 개체에 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체를 `MyMapOf_xsd_string_To_xsd_anyType` 추가합니다. 개체의 `MyMapOf_xsd_string_To_xsd_anyType` 메서드를 호출하고 개체를 `Add` `MyMapOf_xsd_string_To_xsd_anyType` 전달합니다. 각 입력 PDF 문서에 대해 이 작업을 수행합니다.

1. 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 런타임 옵션을 저장하는 `AssemblerOptionSpec` 객체를 만듭니다.
   * 객체에 속하는 데이터 멤버에 값을 할당하여 비즈니스 요구 사항에 맞게 런타임 옵션을 `AssemblerOptionSpec` 설정합니다. 예를 들어 오류가 발생할 때 어셈블리 서비스에서 작업을 계속 처리하도록 지정하려면 개체 `false` 의 `AssemblerOptionSpec` 데이터 `failOnError` 멤버에 할당합니다.

1. 입력 PDF 문서 조합

   개체의 `AssemblerServiceClient` 메서드를 `invoke` 호출하고 다음 값을 전달합니다.

   * DDX 문서를 나타내는 `BLOB` 개체입니다.
   * 입력 PDF 문서를 포함하는 `mapItem` 배열입니다. 해당 키는 PDF 소스 파일의 이름과 일치해야 하며 해당 값은 해당 파일에 해당하는 `BLOB` 객체여야 합니다.
   * 런타임 옵션을 지정하는 `AssemblerOptionSpec` 개체입니다.

   이 `invoke` `AssemblerResult` 메서드는 작업 결과와 발생했을 수 있는 예외를 포함하는 개체를 반환합니다.

1. 결과를 추출합니다.

   새로 만든 PDF 문서를 얻으려면 다음 작업을 수행하십시오.

   * 결과 PDF 문서를 포함하는 `AssemblerResult` 개체인 개체의 `documents` `Map` 필드에 액세스합니다.
   * 결과 문서의 이름과 일치하는 키를 찾을 때까지 `Map` 개체를 반복합니다. 그런 다음 해당 어레이 멤버 `value` 를 a로 캐스팅합니다 `BLOB`.
   * 개체의 속성에 액세스하여 PDF 문서를 나타내는 이진 데이터 `BLOB` 를 `MTOM` 추출합니다. PDF 파일에 기록할 수 있는 바이트 배열을 반환합니다.

   >[!NOTE]
   >
   >로그를 생성하도록 `LOG_LEVEL` 설정된 경우 `AssemblerResult` 개체 `jobLog` 데이터 멤버의 값을 가져와 로그를 추출할 수 있습니다.

**참고 항목**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
