---
title: 여러 XDP 조각 정리
seo-title: 여러 XDP 조각 정리
description: 'null'
seo-description: 'null'
uuid: 0e35ff85-ff40-4878-ae31-aa8da75bd3ec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c4706632-02e5-4510-ad9c-4f732d5fbdad
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1876'
ht-degree: 0%

---


# 여러 XDP 조각 정리{#assembling-multiple-xdp-fragments}

여러 XDP 조각을 하나의 XDP 문서로 결합할 수 있습니다. 예를 들어 각 XDP 파일에 상태 양식을 만드는 데 사용되는 하위 양식이 하나 이상 포함되어 있는 XDP 조각을 고려해 보십시오. 다음 그림은 아웃라인 보기(여러 XDP 조각 ** 빠른 시작 집합에서 사용되는 tac018_template_flrode.xdp 파일 표시)를 보여줍니다.

![am_am_forma](assets/am_am_forma.png)

다음 그림에서는 환자 섹션(여러 XDP 조각 *정리 빠른 시작* 시 사용되는 tac018_contact.xdp 파일 표시)을 보여 줍니다.

![am_am_formb](assets/am_am_formb.png)

다음 그림은 환자 상태 섹션(여러 XDP 조각 ** 빠른 시작 집합에서 사용되는 tc018_patient.xdp 파일을 나타냅니다.)

![am_am_formc](assets/am_am_formc.png)

이 조각에는 *subPatientPhysical* 및 *subPatientHealth라는 두 개의 하위 양식이 포함되어 있습니다*. 이 두 하위 양식은 모두 어셈블러 서비스로 전달되는 DDC 문서에서 참조됩니다. 다음 그림과 같이 어셈블러 서비스를 사용하여 이러한 모든 XDP 조각을 단일 XDP 문서로 결합할 수 있습니다.

![am_am_formd](assets/am_am_formd.png)

다음 DDX 문서는 여러 XDP 조각을 XDP 문서로 취합합니다.

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

DDX 문서에는 결과 이름을 지정하는 XDP `result` 태그가 포함되어 있습니다. 이 경우 값이 `tuc018result.xdp`됩니다. 이 값은 Assembler 서비스가 결과를 반환하는 후에 XDP 문서를 검색하는 데 사용되는 응용 프로그램 논리에서 참조됩니다. 예를 들어, 조합된 XDP 문서를 검색하는 데 사용되는 다음 Java 애플리케이션 로직을 생각해 보십시오(값이 굵게 표시됨).

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

태그는 전체 XDP 문서를 나타내는 XDP 파일을 `XDP source` 지정합니다. 이 파일은 XDP 조각을 추가하기 위한 컨테이너나 함께 추가되는 여러 문서 중 하나로 사용할 수 있습니다. 이러한 경우 XDP 문서는 컨테이너로만 사용됩니다(여러 XDP 조각 *집합에서 처음 표시된 그림*). 즉, 다른 XDP 파일은 XDP 컨테이너 내에 배치됩니다.

각 하위 양식에 대해 요소를 추가할 수 있습니다(이 요소는 선택 사항). `XDPContent` 위의 예에서 세 가지 하위 양식이 있습니다. `subPatientContact`, `subPatientPhysical`and `subPatientHealth`. 하위 `subPatientPhysical` 폼과 하위 `subPatientHealth` 폼 모두 동일한 XDP 파일인 tc018_patient.xdp에 있습니다. 조각 요소는 디자이너에 정의된 대로 하위 양식의 이름을 지정합니다.

>[!NOTE]
>
>어셈블러 서비스에 대한 자세한 내용은 AEM Forms에 대한 [서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDX 문서에 대한 자세한 내용은 어셈블러 서비스 [및 DDX 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 단계 요약 {#summary-of-steps}

여러 XDP 조각을 취합하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일 포함
1. PDF 어셈블러 클라이언트 만들기
1. 기존 DDX 문서를 참조합니다.
1. XDP 문서를 참조하십시오.
1. 런타임 옵션을 설정합니다.
1. 여러 XDP 문서를 취합합니다.
1. 결합된 XDP 문서를 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(AEM Forms이 JBoss에 배포된 경우 필요)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필요)

**PDF 어셈블러 클라이언트 만들기**

어셈블리 작업을 프로그래밍 방식으로 수행하려면 먼저 어셈블러 서비스 클라이언트를 만듭니다.

**기존 DCX 문서 참조**

여러 XDP 문서를 취합하려면 DDX 문서를 참조해야 합니다. 이 DDX 문서에는 `XDP result`요소, `XDP source`및 `XDPContent` 요소가 포함되어야 합니다.

**XDP 문서 참조**

여러 XDP 문서를 취합하려면 결과 XDP 문서를 구성하는 데 사용되는 모든 XDP 파일을 참조하십시오. XDP 문서에 포함된 하위 양식의 이름( `source` 속성으로 참조되는 하위 양식)이 속성에 `fragment` 지정되어 있는지 확인합니다. 하위 양식은 Designer에서 정의됩니다. 예를 들어 다음 XML을 고려합니다.

```xml
 <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
```

subPatientContact라는 하위 양식 *은* tac018_contact.xdp라는 XDP 파일에 있어야 합니다 **.

**런타임 옵션 설정**

작업을 수행하는 동안 어셈블러 서비스의 동작을 제어하는 런타임 옵션을 설정할 수 있습니다. 예를 들어 오류가 발생한 경우 어셈블리 서비스에서 작업을 계속 처리하도록 하는 옵션을 설정할 수 있습니다.

**여러 XDP 문서 조합**

여러 XDP 파일을 취합하려면 `invokeDDX` 작업을 호출합니다. 어셈블러 서비스는 컬렉션 개체 내에서 어셈블된 XDP 문서를 반환합니다.

**결합된 XDP 문서 검색**

조합 XDP 문서는 컬렉션 개체 내에서 반환됩니다. 컬렉션 개체를 반복하여 XDP 문서를 XDP 파일로 저장합니다. 또한 XDP 문서를 출력과 같은 다른 AEM Forms 서비스로 전달할 수 있습니다.

**참고 항목**

[Java API를 사용하여 여러 XDP 조각 조합](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-java-api)

[웹 서비스 API를 사용하여 여러 XDP 조각 조합](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[프로그래밍 방식으로 PDF 문서 취합](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)

[조각을 사용하여 PDF 문서 만들기](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)

## Java API를 사용하여 여러 XDP 조각 조합 {#assemble-multiple-xdp-fragments-using-the-java-api}

Assembler Service API(Java)를 사용하여 여러 XDP 조각을 어셈블합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-assembler-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. PDF 어셈블러 클라이언트 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 개체를 `AssemblerServiceClient` 만들고 개체를 `ServiceClientFactory` 전달합니다.

1. 기존 DDX 문서를 참조합니다.

   * 생성자를 사용하여 DCX 문서를 나타내는 `java.io.FileInputStream` 개체를 만들고 DDX 파일의 위치를 지정하는 문자열 값을 전달합니다.
   * 생성자를 사용하여 개체를 `com.adobe.idp.Document` 만들고 개체를 `java.io.FileInputStream` 전달합니다.

1. XDP 문서를 참조하십시오.

   * 생성자를 사용하여 입력 XDP 문서를 저장하는 데 사용되는 `java.util.Map` 개체를 `HashMap` 만듭니다.
   * 개체를 만들고 입력 XDP 파일이 포함된 `com.adobe.idp.Document` `java.io.FileInputStream` 개체를 전달합니다(각 XDP 파일에 대해 이 작업 반복).
   * 해당 메서드를 호출하고 다음 인수를 전달하여 `java.util.Map` 개체에 `put` 항목을 추가합니다.

      * 키 이름을 나타내는 문자열 값입니다. 이 값은 DDX 문서에 지정된 `source` 요소 값과 일치해야 합니다(각 XDP 파일에 대해 이 작업 반복).
      * 요소에 해당하는 XDP 문서를 포함하는 `com.adobe.idp.Document` 개체(각 XDP 파일에 대해 이 `source` 작업을 반복합니다.)

1. 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 런타임 옵션을 저장하는 `AssemblerOptionSpec` 객체를 만듭니다.
   * 개체에 속하는 메서드를 호출하여 비즈니스 요구 사항에 맞게 런타임 옵션을 `AssemblerOptionSpec` 설정합니다. 예를 들어 오류가 발생할 때 어셈블리 서비스에서 작업을 계속 처리하도록 지정하려면 `AssemblerOptionSpec` 개체의 `setFailOnError` 메서드를 호출하고 전달합니다 `false`.

1. 여러 XDP 문서를 취합합니다.

   개체의 `AssemblerServiceClient` `invokeDDX` 메서드를 호출하고 다음 필수 값을 전달합니다.

   * 사용할 DCX 문서를 나타내는 `com.adobe.idp.Document` 개체
   * 입력 XDP 파일을 포함하는 `java.util.Map` 개체
   * 기본 글꼴 및 작업 로그 수준을 포함하여 런타임 옵션을 지정하는 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 개체

   이 `invokeDDX` 메서드는 조합된 XDP 문서를 포함하는 `com.adobe.livecycle.assembler.client.AssemblerResult` 개체를 반환합니다.

1. 결합된 XDP 문서를 검색합니다.

   결합된 XDP 문서를 얻으려면 다음 작업을 수행하십시오.

   * 개체의 `AssemblerResult` 메서드를 `getDocuments` 호출합니다. 이 메서드는 `java.util.Map` 개체를 반환합니다.
   * 결과 개체를 찾을 때까지 개체 `java.util.Map` 를 반복하십시오 `com.adobe.idp.Document` .
   * 오브젝트의 `com.adobe.idp.Document` `copyToFile` 방법을 불러와서 결합된 XDP 문서를 추출합니다.

**참고 항목**

[여러 XDP 조각 정리](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)[빠른 시작(SOAP 모드): Java API를 사용하여 여러 XDP 조각 조합](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-multiple-xdp-fragments-using-the-java-api)AEM Forms[를 포함하는 Java 라이브러리 파일](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)연결 속성[설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API를 사용하여 여러 XDP 조각 조합 {#assemble-multiple-xdp-fragments-using-the-web-service-api}

Assembler Service API(웹 서비스)를 사용하여 여러 XDP 조각을 조합합니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 서비스 참조를 설정할 때 다음 WSDL 정의를 사용해야 합니다.

   ```java
    https://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   >[!NOTE]
   >
   >AEM Forms `localhost` 를 호스팅하는 서버의 IP 주소로 대체합니다.

1. PDF 어셈블러 클라이언트 만들기

   * 기본 생성자를 사용하여 `AssemblerServiceClient` 개체를 만듭니다.
   * 생성자를 사용하여 `AssemblerServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스(예: `https://localhost:8080/soap/services/AssemblerService?blob=mtom`)로 전달합니다. 속성을 사용할 필요는 `lc_version` 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.
   * 필드의 값을 `System.ServiceModel.BasicHttpBinding` 가져와 개체를 `AssemblerServiceClient.Endpoint.Binding` 만듭니다. 반환 값을 다음으로 캐스팅합니다 `BasicHttpBinding`.
   * 개체 `System.ServiceModel.BasicHttpBinding` 필드를 (으)로 `MessageEncoding` 설정합니다 `WSMessageEncoding.Mtom`. 이 값을 사용하면 MTOM이 사용됩니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * AEM Forms 사용자 이름을 `AssemblerServiceClient.ClientCredentials.UserName.UserName` 필드에 지정합니다.
      * 해당 암호 값을 `AssemblerServiceClient.ClientCredentials.UserName.Password`필드에 지정합니다.
      * `HttpClientCredentialType.Basic` 필드에 `BasicHttpBindingSecurity.Transport.ClientCredentialType`상수 값을 지정합니다.
      * `BasicHttpSecurityMode.TransportCredentialOnly` 필드에 `BasicHttpBindingSecurity.Security.Mode`상수 값을 지정합니다.

1. 기존 DDX 문서를 참조합니다.

   * 생성자를 사용하여 `BLOB` 개체를 만듭니다. 이 `BLOB` 개체는 DDX 문서를 저장하는 데 사용됩니다.
   * 생성자를 호출하고 DDX 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * 개체의 내용을 저장하는 바이트 배열을 `System.IO.FileStream` 만듭니다. 개체의 속성을 가져와 바이트 배열의 크기를 결정할 수 `System.IO.FileStream` `Length` 있습니다.
   * 개체의 메서드를 호출하여 바이트 배열을 스트림 데이터로 `System.IO.FileStream` 채웁니다 `Read` . 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 바이트 배열의 컨텐츠로 해당 `BLOB` `MTOM` 속성을 지정하여 개체를 채웁니다.

1. XDP 문서를 참조하십시오.

   * 각 입력 XDP 파일에 대해 생성자를 사용하여 `BLOB` 개체를 만듭니다. 이 `BLOB` 개체는 입력 파일을 저장하는 데 사용됩니다.
   * 생성자를 호출하고 입력 파일의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * 개체의 내용을 저장하는 바이트 배열을 `System.IO.FileStream` 만듭니다. 개체의 속성을 가져와 바이트 배열의 크기를 결정할 수 `System.IO.FileStream` `Length` 있습니다.
   * 개체의 메서드를 호출하여 바이트 배열을 스트림 데이터로 `System.IO.FileStream` 채웁니다 `Read` . 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 바이트 배열의 내용으로 해당 `BLOB` `MTOM` 필드를 할당하여 개체를 채웁니다.
   * 개체를 `MyMapOf_xsd_string_To_xsd_anyType` 만듭니다. 이 컬렉션 개체는 어셈블된 XDP 문서를 만드는 데 필요한 입력 파일을 저장하는 데 사용됩니다.
   * 각 입력 파일에 대해 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체를 만듭니다.
   * 키 이름을 나타내는 문자열 값을 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체의 `key` 필드에 할당합니다. 이 값은 DDX 문서에 지정된 요소의 값과 일치해야 합니다. 각 입력 XDP 파일에 대해 이 작업을 수행합니다.
   * 입력 파일을 저장하는 `BLOB` 객체를 `MyMapOf_xsd_string_To_xsd_anyType_Item` 객체 `value` 필드에 지정합니다. 각 입력 XDP 파일에 대해 이 작업을 수행합니다.
   * 개체에 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체를 `MyMapOf_xsd_string_To_xsd_anyType` 추가합니다. 개체의 `MyMapOf_xsd_string_To_xsd_anyType` 메서드를 호출하고 개체를 `Add` `MyMapOf_xsd_string_To_xsd_anyType` 전달합니다. 각 입력 XDP 문서에 대해 이 작업을 수행합니다.

1. 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 런타임 옵션을 저장하는 `AssemblerOptionSpec` 객체를 만듭니다.
   * 객체에 속하는 데이터 멤버에 값을 할당하여 비즈니스 요구 사항에 맞게 런타임 옵션을 `AssemblerOptionSpec` 설정합니다. 예를 들어 오류가 발생할 때 어셈블리 서비스에서 작업을 계속 처리하도록 지정하려면 개체 `false` 의 `AssemblerOptionSpec` 데이터 `failOnError` 멤버에 할당합니다.

1. 여러 XDP 문서를 취합합니다.

   개체의 `AssemblerServiceClient` 메서드를 `invokeDDX` 호출하고 다음 값을 전달합니다.

   * DCX 문서를 나타내는 `BLOB` 개체
   * 필수 파일이 포함된 `MyMapOf_xsd_string_To_xsd_anyType` 개체
   * 런타임 옵션을 지정하는 `AssemblerOptionSpec` 개체

   이 `invokeDDX` `AssemblerResult` 메서드는 작업 결과와 발생한 예외를 포함하는 개체를 반환합니다.

1. 결합된 XDP 문서를 검색합니다.

   새로 만든 XDP 문서를 얻으려면 다음 작업을 수행하십시오.

   * 결과 PDF 문서 `AssemblerResult` 가 포함된 개체인 개체의 `documents` 필드에 `Map` 액세스합니다.
   * 객체를 반복하여 결과 문서를 `Map` 가져옵니다. 그런 다음 해당 어레이 멤버 `value` 를 a로 캐스팅합니다 `BLOB`.
   * 개체의 속성에 액세스하여 PDF 문서를 나타내는 이진 데이터 `BLOB` 를 `MTOM` 추출합니다. XDP 파일에 쓸 수 있는 바이트 배열을 반환합니다.

**참고 항목**

[MTOM을 사용하여 여러 XDP 조각](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)[을 호출하는 AEM Forms 조합](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)