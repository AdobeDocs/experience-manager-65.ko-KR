---
title: 프로그래밍 방식으로 PDF 문서 어셈블
description: 어셈블러 서비스 API를 사용하여 Java API 및 웹 서비스 API를 사용하여 여러 PDF 문서를 단일 PDF 문서로 어셈블합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 7d6fd230-e477-4286-9fb3-18a3474e3e48
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2105'
ht-degree: 0%

---

# 프로그래밍 방식으로 PDF 문서 어셈블 {#programmatically-assembling-pdf-documents}

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms에 대해서만 적용됩니다.**

어셈블러 서비스 API를 사용하여 여러 PDF 문서를 단일 PDF 문서로 어셈블할 수 있습니다. 다음 그림은 세 개의 PDF 문서가 하나의 PDF 문서로 병합되는 모습을 보여 줍니다.

![pa_pa_document_assembly](assets/pa_pa_document_assembly.png)

두 개 이상의 PDF 문서를 단일 PDF 문서로 어셈블하려면 DDX 문서가 필요합니다. DDX 문서에서는 어셈블러 서비스가 생성하는 PDF 문서에 대해 설명합니다. 즉, DDX 문서는 어셈블러 서비스에 수행할 작업을 지시합니다.

이러한 논의를 위해 다음과 같은 DDX 문서가 사용된다고 가정하자.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     <PDF result="out.pdf">
         <PDF source="map.pdf" />
         <PDF source="directions.pdf" />
     </PDF>
 </DDX>
```

이 DDX 문서는 이름이 인 두 개의 PDF 문서를 병합합니다. *map.pdf* 및 *directions.pdf* 단일 PDF 문서로 전환합니다.

>[!NOTE]
>
>PDF 문서를 디스어셈블하는 DDX 문서를 보려면 [프로그래밍 방식으로 PDF 문서 디스어셈블](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents).

>[!NOTE]
>
>어셈블러 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDX 문서에 대한 자세한 내용은 [어셈블러 서비스 및 DDX 참조](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 웹 서비스를 사용하여 어셈블러 서비스를 호출할 때 고려 사항 {#considerations-when-invoking-assembler-service-using-web-services}

큰 문서를 어셈블하는 동안 머리글과 바닥글을 추가하면 `OutOfMemory` 오류가 발생하여 파일이 어셈블되지 않습니다. 이 문제가 발생할 가능성을 줄이려면 `DDXProcessorSetting` 다음 예와 같이 요소를 DDX 문서에 추가합니다.

`<DDXProcessorSetting name="checkpoint" value="2000" />`

이 요소를 의 하위 요소로 추가할 수 있습니다 `DDX` 요소 또는 의 하위 항목 `PDF result` 요소를 생성하지 않습니다. 이 설정의 기본값은 0(영)으로, 체크포인트를 해제하고 DDX가 `DDXProcessorSetting` 요소가 없습니다. 다음 오류가 발생한 경우: `OutOfMemory` 오류가 발생했습니다. 값을 일반적으로 500에서 5000 사이의 정수로 설정해야 할 수 있습니다. 체크포인트 값이 작을수록 체크포인트가 더 자주 발생합니다.

## 단계 요약 {#summary-of-steps}

여러 PDF 문서에서 단일 PDF 문서를 어셈블하려면 다음 작업을 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. PDF 어셈블러 클라이언트를 만듭니다.
1. 기존 DDX 문서를 참조합니다.
1. 입력 PDF 문서 참조.
1. 런타임 옵션을 설정합니다.
1. 입력 PDF 문서를 어셈블합니다.
1. 결과 추출

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

어셈블러 작업을 프로그래밍 방식으로 수행하려면 먼저 어셈블러 클라이언트를 만들어야 합니다.

**기존 DDX 문서 참조**

PDF 문서를 어셈블하려면 DDX 문서를 참조해야 합니다. 예를 들어 이 섹션에 소개된 DDX 문서를 생각해 보십시오. 이 DDX 문서는 어셈블러 서비스에 두 개의 PDF 문서를 하나의 PDF 문서로 병합하도록 지시합니다.

**참조 입력 PDF 문서**

어셈블러 서비스에 전달할 입력 PDF 문서를 참조합니다. 예를 들어 맵 및 방향이라는 두 개의 입력 PDF 문서를 전달하려면 해당 PDF 파일을 전달해야 합니다.

map.pdf 파일과 directions.pdf 파일은 모두 컬렉션 개체에 배치해야 합니다. 키 이름은 DDX 문서에 있는 PDF 소스 속성 값과 일치해야 합니다. DDX 문서의 키와 소스 속성이 일치하는 경우 PDF 파일의 이름이 무엇이든 상관없습니다.

>[!NOTE]
>
>An `AssemblerResult` 를 호출하면 컬렉션 개체가 포함된 개체가 반환됩니다. `invokeDDX` 작업. 이 작업은 두 개 이상의 입력 PDF 문서를 어셈블러 서비스에 전달할 때 사용됩니다. 그러나 어셈블러 서비스에 입력 PDF을 하나만 전달하고 반환 문서가 하나만 필요한 경우에는 `invokeOneDocument` 작업. 이 작업을 호출하면 단일 문서가 반환됩니다. 이 작업 사용에 대한 자세한 내용은 [암호화된 PDF 문서 어셈블](/help/forms/developing/assembling-encrypted-pdf-documents.md#assembling-encrypted-pdf-documents).

**런타임 옵션 설정**

작업을 수행하는 동안 어셈블러 서비스의 동작을 제어하는 런타임 옵션을 설정할 수 있습니다. 예를 들어 오류가 발생하는 경우 어셈블러 서비스에서 작업 처리를 계속하도록 지시하는 옵션을 설정할 수 있습니다. 설정할 수 있는 런타임 옵션에 대한 자세한 내용은 `AssemblerOptionSpec` 의 클래스 참조 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**입력 PDF 문서 어셈블**

서비스 클라이언트를 만들고, DDX 파일을 참조하고, 입력 PDF 문서를 저장하는 컬렉션 개체를 만들고, 런타임 옵션을 설정한 후 DDX 작업을 호출할 수 있습니다. 이 섹션에 지정된 DDX 문서를 사용하는 경우 map.pdf 및 direction.pdf 파일이 하나의 PDF 문서로 병합됩니다.

**결과 추출**

어셈블러 서비스가 `java.util.Map` 개체에서 가져올 수 있는 개체 `AssemblerResult` 개체와 작업 결과를 포함하는 입니다. 반환된 `java.util.Map` 객체에는 결과 문서 및 모든 예외가 포함됩니다.

다음 표에는 반환될 수 있는 키 값과 객체 유형이 요약되어 있습니다 `java.util.Map` 개체.

<table>
 <thead>
  <tr>
   <th><p>키 값</p></th>
   <th><p>오브젝트 유형</p></th>
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
   <td><p>문서에 대한 예외를 포함합니다.</p></td>
  </tr>
  <tr>
   <td><p><code>OutputMapConstants.LOG_NAME</code></p></td>
   <td><p><code>com.adobe.idp.Documen</code></p></td>
   <td><p>작업 로그를 포함합니다.</p></td>
  </tr>
 </tbody>
</table>

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[프로그래밍 방식으로 PDF 문서 디스어셈블](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Java API를 사용하여 PDF 문서 어셈블 {#assemble-pdf-documents-using-the-java-api}

어셈블러 서비스 API(Java)를 사용하여 PDF 문서를 어셈블합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-assembler-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. PDF 어셈블러 클라이언트를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.
   * 만들기 `AssemblerServiceClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체.

1. 기존 DDX 문서를 참조합니다.

   * 만들기 `java.io.FileInputStream` 생성자를 사용하고 DDX 파일의 위치를 지정하는 문자열 값을 전달하여 DDX 문서를 나타내는 개체입니다.
   * 만들기 `com.adobe.idp.Document` 개체를 생성자를 사용하고 `java.io.FileInputStream` 개체.

1. 입력 PDF 문서 참조.

   * 만들기 `java.util.Map` 개체를 사용하여 입력 PDF 문서를 저장하는 데 사용됩니다 `HashMap` 생성자입니다.
   * 각 입력 PDF 문서에 대해 `java.io.FileInputStream` 개체를 작성자에 사용하고 입력 PDF 문서의 위치를 전달합니다.
   * 각 입력 PDF 문서에 대해 `com.adobe.idp.Document` 개체 및 전달 `java.io.FileInputStream` PDF 문서가 포함된 객체입니다.
   * 각 입력 문서에 대한 항목을 `java.util.Map` 개체 `put` 메서드 및 다음 인수 전달:

      * 키 이름을 나타내는 문자열 값입니다. 이 값은 DDX 문서에 지정된 PDF 원본 요소의 값과 일치해야 합니다.
      * A `com.adobe.idp.Document` 오브젝트(또는 `java.util.List` 원본 PDF 문서를 포함하는 여러 문서를 지정하는 개체입니다.

1. 런타임 옵션을 설정합니다.

   * 만들기 `AssemblerOptionSpec` 생성자를 사용하여 런타임 옵션을 저장하는 개체입니다.
   * 에 속한 메서드를 호출하여 비즈니스 요구 사항을 충족하도록 런타임 옵션을 설정합니다. `AssemblerOptionSpec` 개체. 예를 들어 오류가 발생할 때 어셈블러 서비스에서 작업 처리를 계속하도록 하려면 `AssemblerOptionSpec` 개체 `setFailOnError` 방법 및 통과 `false`.

1. 입력 PDF 문서를 어셈블합니다.

   호출 `AssemblerServiceClient` 개체 `invokeDDX` 메서드를 실행하고 다음 필수 값을 전달합니다.

   * A `com.adobe.idp.Document` 사용할 DDX 문서를 나타내는 개체입니다
   * A `java.util.Map` 어셈블할 입력 PDF 파일이 포함된 개체
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 기본 글꼴 및 작업 로그 수준을 포함하여 런타임 옵션을 지정하는 개체

   다음 `invokeDDX` 메서드가 을 반환합니다. `com.adobe.livecycle.assembler.client.AssemblerResult` 작업의 결과와 발생한 예외를 포함하는 객체입니다.

1. 결과 추출

   새로 만든 PDF 문서를 가져오려면 다음 작업을 수행합니다.

   * 호출 `AssemblerResult` 개체 `getDocuments` 메서드를 사용합니다. 이 값은 `java.util.Map` 개체.
   * 다음을 반복합니다. `java.util.Map` 결과를 찾을 때까지 오브젝트 `com.adobe.idp.Document` 개체. (DDX 문서에 지정된 PDF 결과 요소를 사용하여 문서를 가져올 수 있습니다.)
   * 호출 `com.adobe.idp.Document` 개체 `copyToFile` PDF 문서를 추출하는 방법입니다.

   >[!NOTE]
   >
   >If `LOG_LEVEL` 로그를 생성하도록 설정된 경우 `AssemblerResult` 개체 `getJobLog` 메서드를 사용합니다.

**추가 참조**

[빠른 시작(SOAP 모드): Java API를 사용하여 PDF 문서 어셈블](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API를 사용하여 PDF 문서 어셈블 {#assemble-pdf-documents-using-the-web-service-api}

어셈블러 서비스 API(웹 서비스)를 사용하여 PDF 문서를 어셈블합니다.

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
   * 채우기 `BLOB` 개체 할당 `MTOM` 속성을 바이트 배열의 콘텐츠와 함께 사용합니다.

1. 입력 PDF 문서 참조.

   * 각 입력 PDF 문서에 대해 `BLOB` 개체를 만들 때 사용됩니다. 다음 `BLOB` 객체는 입력 PDF 문서를 저장하는 데 사용됩니다.
   * 만들기 `System.IO.FileStream` 개체를 호출하고 입력 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 콘텐츠를 저장하는 바이트 배열 만들기 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채우기 `System.IO.FileStream` 개체 `Read` 메서드를 사용합니다. 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 채우기 `BLOB` 개체 할당 `MTOM` 바이트 배열의 내용이 있는 필드입니다.
   * 만들기 `MyMapOf_xsd_string_To_xsd_anyType` 개체. 이 컬렉션 개체는 입력 PDF 문서를 저장하는 데 사용됩니다.
   * 각 입력 PDF 문서에 대해 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체. 예를 들어 두 개의 입력 PDF 문서를 사용하는 경우 두 개를 만듭니다 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체.
   * 키 이름을 나타내는 문자열 값을 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체 `key` 필드. 이 값은 DDX 문서에 지정된 PDF 원본 요소의 값과 일치해야 합니다. (각 입력 PDF 문서에 대해 이 작업을 수행합니다.)
   * 할당 `BLOB` 에 PDF 문서를 저장하는 개체 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체 `value` 필드. (각 입력 PDF 문서에 대해 이 작업을 수행합니다.)
   * 추가 `MyMapOf_xsd_string_To_xsd_anyType_Item` 에 대한 오브젝트 `MyMapOf_xsd_string_To_xsd_anyType` 개체. 호출 `MyMapOf_xsd_string_To_xsd_anyType` 개체 `Add` 메서드 및 전달 `MyMapOf_xsd_string_To_xsd_anyType` 개체. (각 입력 PDF 문서에 대해 이 작업을 수행합니다.)

1. 런타임 옵션을 설정합니다.

   * 만들기 `AssemblerOptionSpec` 생성자를 사용하여 런타임 옵션을 저장하는 개체입니다.
   * 에 속한 데이터 멤버에 값을 할당하여 비즈니스 요구 사항을 충족하는 런타임 옵션을 설정합니다. `AssemblerOptionSpec` 개체. 예를 들어 오류가 발생할 때 어셈블러 서비스에서 작업 처리를 계속하도록 하려면 다음을 할당합니다 `false` (으)로 `AssemblerOptionSpec` 개체 `failOnError` 데이터 구성원입니다.

1. 입력 PDF 문서를 어셈블합니다.

   호출 `AssemblerServiceClient` 개체 `invoke` 메서드를 실행하고 다음 값을 전달합니다.

   * A `BLOB` DDX 문서를 나타내는 개체입니다.
   * 다음 `mapItem` 입력 PDF 문서를 포함하는 배열입니다. 키는 PDF 소스 파일의 이름과 일치해야 하며 값은 다음과 같아야 합니다. `BLOB` 해당 파일에 해당하는 개체입니다.
   * An `AssemblerOptionSpec` 런타임 옵션을 지정하는 개체입니다.

   다음 `invoke` 메서드가 다음을 반환합니다. `AssemblerResult` 작업의 결과와 발생했을 수 있는 예외를 포함하는 객체입니다.

1. 결과 추출

   새로 만든 PDF 문서를 가져오려면 다음 작업을 수행합니다.

   * 액세스 `AssemblerResult` 개체 `documents` 필드: `Map` 결과 PDF 문서가 포함된 객체입니다.
   * 다음을 반복합니다. `Map` 결과 문서의 이름과 일치하는 키를 찾을 때까지 객체를 검색합니다. 그런 다음 해당 배열 멤버의 `value` (으)로 `BLOB`.
   * 에 액세스하여 PDF 문서를 나타내는 이진 데이터 추출 `BLOB` 개체 `MTOM` 속성. PDF 파일에 쓸 수 있는 바이트 배열이 반환됩니다.

   >[!NOTE]
   >
   >If `LOG_LEVEL` 이(가) 로그를 생성하도록 설정되어 있으면 의 값을 가져와 로그를 추출할 수 있습니다. `AssemblerResult` 개체 `jobLog` 데이터 구성원입니다.

**추가 참조**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
