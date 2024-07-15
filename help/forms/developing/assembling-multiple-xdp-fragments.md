---
title: 여러 XDP 조각 어셈블
description: Java API 및 웹 서비스 API를 사용하여 여러 XDP 조각을 단일 XDP 문서로 조합합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
docset: aem65
role: Developer
exl-id: 54d98c69-2b2e-46cb-9f6a-7e9bdbe5c378
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1859'
ht-degree: 0%

---

# 여러 XDP 조각 어셈블{#assembling-multiple-xdp-fragments}

여러 XDP 조각을 단일 XDP 문서로 조합할 수 있습니다. 예를 들어 각 XDP 파일에 상태 양식을 만드는 데 사용되는 하나 이상의 하위 양식이 포함된 XDP 조각을 고려해 보십시오. 다음 그림은 개요 보기를 보여 줍니다(*여러 XDP 조각 조합* 빠른 시작에 사용된 tuc018_template_flow.xdp 파일을 나타냄).

![am_am_forma](assets/am_am_forma.png)

다음 그림은 환자 섹션을 보여 줍니다(*여러 XDP 조각 어셈블* 빠른 시작에 사용된 tuc018_contact.xdp 파일을 나타냄).

![am_am_formb](assets/am_am_formb.png)

다음 그림은 환자 상태 섹션을 보여 줍니다(*여러 XDP 조각 어셈블* 빠른 시작에 사용된 tuc018_patient.xdp 파일을 나타냄).

![am_am_formc](assets/am_am_formc.png)

이 조각에는 *subPatientPhysical* 및 *subPatientHealth*&#x200B;이라는 두 개의 하위 양식이 포함되어 있습니다. 이러한 두 하위 양식은 어셈블러 서비스에 전달되는 DDX 문서에서 참조됩니다. 어셈블러 서비스를 사용하면 다음 그림과 같이 이러한 XDP 조각을 모두 단일 XDP 문서로 결합할 수 있습니다.

![am_am_formd](assets/am_am_formd.png)

다음 DDX 문서는 여러 XDP 조각을 XDP 문서로 어셈블합니다.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
         <XDP result="tuc018result.xdp">
            <XDP source="tuc018_template_flowed.xdp">
             <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
               <XDPContent insertionPoint="ddx_fragment" source="tuc018_patient.xdp" fragment="subPatientPhysical" required="false"/>
               <XDPContent insertionPoint="ddx_fragment" source="tuc018_patient.xdp" fragment="subPatientHealth" required="false"/>
            </XDP>
         </XDP>
 </DDX>
```

DDX 문서에 결과의 이름을 지정하는 XDP `result` 태그가 있습니다. 이 경우 값은 `tuc018result.xdp`입니다. 이 값은 어셈블러 서비스가 결과를 반환한 후 XDP 문서를 검색하는 데 사용되는 응용 프로그램 논리에서 참조됩니다. 예를 들어 어셈블된 XDP 문서를 검색하는 데 사용되는 다음 Java 애플리케이션 논리를 고려하십시오(값이 굵게 표시됨).

```java
 //Iterate through the map object to retrieve the result XDP document
 for (Iterator i = allDocs.entrySet().iterator(); i.hasNext();) {
     // Retrieve the Map object’s value
     Map.Entry e = (Map.Entry)i.next();
     //Get the key name as specified in the
     //DDX document
     String keyName = (String)e.getKey();
     if (keyName.equalsIgnoreCase("tuc018result.xdp"))
                 {
         Object o = e.getValue();
         outDoc = (Document)o;
         //Save the result PDF file
         File myOutFile = new File("C:\\AssemblerResultXDP.xdp");
         outDoc.copyToFile(myOutFile);
     }
 }
```

`XDP source` 태그는 XDP 조각을 추가하기 위한 컨테이너나 순서대로 첨부된 여러 문서 중 하나로 사용할 수 있는 전체 XDP 문서를 나타내는 XDP 파일을 지정합니다. 이 경우 XDP 문서는 컨테이너로만 사용됩니다(*여러 XDP 조각 어셈블*&#x200B;에 표시된 첫 번째 그림). 즉, 다른 XDP 파일은 XDP 컨테이너 내에 배치됩니다.

각 하위 양식에 `XDPContent` 요소를 추가할 수 있습니다(이 요소는 선택 사항입니다). 위의 예제에는 세 개의 하위 양식(`subPatientContact`, `subPatientPhysical` 및 `subPatientHealth`)이 있습니다. `subPatientPhysical` 하위 폼과 `subPatientHealth` 하위 폼이 모두 동일한 XDP 파일인 tuc018_patient.xdp에 있습니다. 조각 요소는 Designer에 정의된 대로 하위 양식의 이름을 지정합니다.

>[!NOTE]
>
>어셈블러 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

>[!NOTE]
>
>DDX 문서에 대한 자세한 내용은 [어셈블러 서비스 및 DDX 참조](https://www.adobe.com/go/learn_aemforms_ddx_63)를 참조하십시오.

## 단계 요약 {#summary-of-steps}

여러 XDP 조각을 취합하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. PDF 어셈블러 클라이언트를 만듭니다.
1. 기존 DDX 문서를 참조합니다.
1. XDP 문서를 참조하십시오.
1. 런타임 옵션을 설정합니다.
1. 여러 XDP 문서를 어셈블합니다.
1. 어셈블된 XDP 문서를 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필수)

**PDF 어셈블러 클라이언트 만들기**

어셈블러 작업을 프로그래밍 방식으로 수행하려면 먼저 어셈블러 서비스 클라이언트를 만듭니다.

**기존 DDX 문서 참조**

여러 XDP 문서를 어셈블하려면 DDX 문서를 참조해야 합니다. 이 DDX 문서에는 `XDP result`, `XDP source` 및 `XDPContent` 요소가 있어야 합니다.

**XDP 문서 참조**

여러 XDP 문서를 어셈블하려면 결과 XDP 문서를 어셈블하는 데 사용되는 모든 XDP 파일을 참조하십시오. `source` 특성에 의해 참조되는 XDP 문서에 포함된 하위 양식의 이름이 `fragment` 특성에 지정되어 있는지 확인합니다. Designer에서 하위 양식을 정의합니다. 예를 들어 다음 XML을 고려해 보십시오.

```xml
 <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
```

*subPatientContact* 하위 양식은 *tuc018_contact.xdp* XDP 파일에 있어야 합니다.

**런타임 옵션 설정**

작업을 수행하는 동안 어셈블러 서비스의 동작을 제어하는 런타임 옵션을 설정할 수 있습니다. 예를 들어 오류가 발생하는 경우 어셈블러 서비스에서 작업 처리를 계속하도록 지시하는 옵션을 설정할 수 있습니다.

**여러 XDP 문서를 어셈블합니다**

여러 XDP 파일을 취합하려면 `invokeDDX` 작업을 호출하십시오. 어셈블러 서비스는 컬렉션 개체 내에서 어셈블된 XDP 문서를 반환합니다.

**어셈블된 XDP 문서 검색**

어셈블된 XDP 문서가 컬렉션 개체 내에서 반환됩니다. 컬렉션 개체를 반복하고 XDP 문서를 XDP 파일로 저장합니다. XDP 문서를 Output과 같은 다른 AEM Forms 서비스에 전달할 수도 있습니다.

**추가 참조**

[Java API를 사용하여 여러 XDP 조각 조합](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-java-api)

[웹 서비스 API를 사용하여 여러 XDP 조각 조합](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[프로그래밍 방식으로 PDF 문서 어셈블](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)

[조각을 사용하여 PDF 문서 생성](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)

## Java API를 사용하여 여러 XDP 조각 조합 {#assemble-multiple-xdp-fragments-using-the-java-api}

어셈블러 서비스 API(Java)를 사용하여 여러 XDP 조각을 어셈블합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-assembler-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. PDF 어셈블러 클라이언트를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하고 `ServiceClientFactory` 개체를 전달하여 `AssemblerServiceClient` 개체를 만듭니다.

1. 기존 DDX 문서를 참조합니다.

   * 생성자를 사용하고 DDX 파일의 위치를 지정하는 문자열 값을 전달하여 DDX 문서를 나타내는 `java.io.FileInputStream` 개체를 만듭니다.
   * 생성자를 사용하고 `java.io.FileInputStream` 개체를 전달하여 `com.adobe.idp.Document` 개체를 만듭니다.

1. XDP 문서를 참조하십시오.

   * `HashMap` 생성자를 사용하여 입력 XDP 문서를 저장하는 데 사용되는 `java.util.Map` 개체를 만듭니다.
   * `com.adobe.idp.Document` 개체를 만들고 입력 XDP 파일이 포함된 `java.io.FileInputStream` 개체를 전달합니다(각 XDP 파일에 대해 이 작업을 반복합니다).
   * `put` 메서드를 호출하고 다음 인수를 전달하여 `java.util.Map` 개체에 항목을 추가합니다.

      * 키 이름을 나타내는 문자열 값입니다. 이 값은 DDX 문서에 지정된 `source` 요소 값과 일치해야 합니다(각 XDP 파일에 대해 이 작업을 반복합니다).
      * `source` 요소에 해당하는 XDP 문서가 포함된 `com.adobe.idp.Document` 개체입니다(각 XDP 파일에 대해 이 작업을 반복합니다).

1. 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 런타임 옵션을 저장하는 `AssemblerOptionSpec` 개체를 만듭니다.
   * `AssemblerOptionSpec` 개체에 속하는 메서드를 호출하여 비즈니스 요구 사항을 충족하도록 런타임 옵션을 설정하십시오. 예를 들어 오류가 발생할 때 어셈블러 서비스에서 작업 처리를 계속하도록 하려면 `AssemblerOptionSpec` 개체의 `setFailOnError` 메서드를 호출하고 `false`을(를) 전달합니다.

1. 여러 XDP 문서를 어셈블합니다.

   `AssemblerServiceClient` 개체의 `invokeDDX` 메서드를 호출하고 다음 필수 값을 전달하십시오.

   * 사용할 DDX 문서를 나타내는 `com.adobe.idp.Document` 개체
   * 입력 XDP 파일이 포함된 `java.util.Map` 개체
   * 기본 글꼴 및 작업 로그 수준을 포함하여 런타임 옵션을 지정하는 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 개체입니다.

   `invokeDDX` 메서드가 어셈블된 XDP 문서가 포함된 `com.adobe.livecycle.assembler.client.AssemblerResult` 개체를 반환합니다.

1. 어셈블된 XDP 문서를 검색합니다.

   어셈블된 XDP 문서를 가져오려면 다음 작업을 수행합니다.

   * `AssemblerResult` 개체의 `getDocuments` 메서드를 호출합니다. 이 메서드는 `java.util.Map` 개체를 반환합니다.
   * 결과 `com.adobe.idp.Document` 개체가 발견될 때까지 `java.util.Map` 개체를 반복합니다.
   * `com.adobe.idp.Document` 개체의 `copyToFile` 메서드를 호출하여 어셈블된 XDP 문서를 추출하십시오.

**추가 참조**

[여러 XDP 조각 어셈블](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[빠른 시작(SOAP 모드): Java API를 사용하여 여러 XDP 조각 어셈블](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-multiple-xdp-fragments-using-the-java-api)
[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API를 사용하여 여러 XDP 조각 조합 {#assemble-multiple-xdp-fragments-using-the-web-service-api}

어셈블러 서비스 API(웹 서비스)를 사용하여 여러 XDP 조각을 어셈블합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 서비스 참조를 설정할 때 다음 WSDL 정의를 사용하는지 확인합니다.

   ```java
    https://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꾸십시오.

1. PDF 어셈블러 클라이언트를 만듭니다.

   * 기본 생성자를 사용하여 `AssemblerServiceClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `AssemblerServiceClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값(예: `https://localhost:8080/soap/services/AssemblerService?blob=mtom`)을 AEM Forms 서비스에 전달합니다. `lc_version` 특성은 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.
   * `AssemblerServiceClient.Endpoint.Binding` 필드의 값을 가져와 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`(으)로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * `AssemblerServiceClient.ClientCredentials.UserName.UserName` 필드에 AEM Forms 사용자 이름을 지정하십시오.
      * 해당 암호 값을 `AssemblerServiceClient.ClientCredentials.UserName.Password` 필드에 지정하십시오.
      * `BasicHttpBindingSecurity.Transport.ClientCredentialType` 필드에 `HttpClientCredentialType.Basic` 상수 값을 할당합니다.
      * `BasicHttpBindingSecurity.Security.Mode` 필드에 `BasicHttpSecurityMode.TransportCredentialOnly` 상수 값을 할당합니다.

1. 기존 DDX 문서를 참조합니다.

   * 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 DDX 문서를 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하고 DDX 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하여 바이트 배열을 스트림 데이터로 채웁니다. 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 해당 `MTOM` 속성을 바이트 배열의 내용으로 할당하여 `BLOB` 개체를 채웁니다.

1. XDP 문서를 참조하십시오.

   * 각 입력 XDP 파일에 대해 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 입력 파일을 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하고 입력 파일의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하여 바이트 배열을 스트림 데이터로 채웁니다. 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 해당 `MTOM` 필드를 바이트 배열의 내용으로 할당하여 `BLOB` 개체를 채웁니다.
   * `MyMapOf_xsd_string_To_xsd_anyType` 개체를 만듭니다. 이 컬렉션 개체는 어셈블된 XDP 문서를 만드는 데 필요한 입력 파일을 저장하는 데 사용됩니다.
   * 각 입력 파일에 대해 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체를 만듭니다.
   * `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체의 `key` 필드에 키 이름을 나타내는 문자열 값을 지정하십시오. 이 값은 DDX 문서에 지정된 요소의 값과 일치해야 합니다. (각 입력 XDP 파일에 대해 이 작업을 수행합니다.)
   * 입력 파일을 저장하는 `BLOB` 개체를 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체의 `value` 필드에 할당합니다. (각 입력 XDP 파일에 대해 이 작업을 수행합니다.)
   * `MyMapOf_xsd_string_To_xsd_anyType` 개체에 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체를 추가합니다. `MyMapOf_xsd_string_To_xsd_anyType` 개체의 `Add` 메서드를 호출하고 `MyMapOf_xsd_string_To_xsd_anyType` 개체를 전달하십시오. (각 입력 XDP 문서에 대해 이 작업을 수행합니다.)

1. 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 런타임 옵션을 저장하는 `AssemblerOptionSpec` 개체를 만듭니다.
   * `AssemblerOptionSpec` 개체에 속하는 데이터 멤버에 값을 할당하여 비즈니스 요구 사항에 맞게 런타임 옵션을 설정하십시오. 예를 들어 오류가 발생할 때 어셈블러 서비스에서 작업 처리를 계속하도록 하려면 `AssemblerOptionSpec` 개체의 `failOnError` 데이터 멤버에 `false`을(를) 할당합니다.

1. 여러 XDP 문서를 어셈블합니다.

   `AssemblerServiceClient` 개체의 `invokeDDX` 메서드를 호출하고 다음 값을 전달하십시오.

   * DDX 문서를 나타내는 `BLOB` 개체
   * 필요한 파일이 포함된 `MyMapOf_xsd_string_To_xsd_anyType` 개체
   * 런타임 옵션을 지정하는 `AssemblerOptionSpec` 개체

   `invokeDDX` 메서드가 작업 결과와 발생한 모든 예외를 포함하는 `AssemblerResult` 개체를 반환합니다.

1. 어셈블된 XDP 문서를 검색합니다.

   새로 만든 XDP 문서를 가져오려면 다음 작업을 수행합니다.

   * 결과 PDF 문서를 포함하는 `Map` 개체인 `AssemblerResult` 개체의 `documents` 필드에 액세스합니다.
   * `Map` 개체를 반복하여 각 결과 문서를 가져옵니다. 그런 다음 해당 배열 멤버의 `value`을(를) `BLOB`(으)로 캐스팅합니다.
   * `BLOB` 개체의 `MTOM` 속성에 액세스하여 PDF 문서를 나타내는 이진 데이터를 추출합니다. XDP 파일에 쓸 수 있는 바이트 배열이 반환됩니다.

**추가 참조**

[여러 XDP 조각 어셈블](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
