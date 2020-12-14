---
title: Bates 번호 매기기를 사용하여 문서 정리
seo-title: Bates 번호 매기기를 사용하여 문서 정리
description: 'null'
seo-description: 'null'
uuid: 28d5faeb-6915-41a2-b6a0-78d255df024f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 77e9b895-1313-4a5b-a2d5-cdb65bdc1966
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1901'
ht-degree: 0%

---


# Bates 번호 매기기를 사용하여 문서 정리 {#assembling-documents-using-bates-numbering}

Bates 번호 매기기를 사용하여 고유한 페이지 식별자가 포함된 PDF 문서를 구성할 수 있습니다. *Bates* numbering은 여러 관련 문서에 고유한 식별자를 적용하는 방법입니다. 문서(또는 문서 집합)의 각 페이지에는 페이지를 고유하게 식별하는 Bates 번호가 할당됩니다. 예를 들어 BOM 정보가 들어 있고 어셈블리 생산과 연관된 제조 문서에는 식별자가 포함될 수 있습니다. Bates 번호에는 순차적으로 증가하는 숫자 값과 선택적 접두어와 접미어가 포함됩니다. 접두사 + 숫자 + 접미사는 *bates 패턴*&#x200B;이라고 합니다.

다음 그림은 문서 헤더에 있는 고유 식별자를 포함하고 있는 PDF 문서를 보여줍니다.

![au_au_batesnumber](assets/au_au_batesnumber.png)

이 토론을 위해 고유 페이지 ID는 문서의 헤더에 배치됩니다. 다음 DDX 문서가 사용되었다고 가정합니다.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
        <PDF result="out.pdf">
        <Header>
         <Center>
             <StyledText>
                 <p font-size="20pt"><BatesNumber/></p>
             </StyledText>
         </Center>
     </Header>
           <PDF source="map.pdf" />
          <PDF source="directions.pdf" />
          </PDF>
 </DDX>
```

이 DCX 문서는 *map.pdf* 및 *directions.pdf*&#x200B;라는 두 개의 PDF 문서를 하나의 PDF 문서로 병합합니다. 결과 PDF 문서에는 고유한 페이지 식별자로 구성된 헤더가 포함되어 있습니다. 예를 들어 위의 그림에서 문서는 000016을 보여 줍니다.

>[!NOTE]
>
>이 섹션을 읽기 전에 Assembler 서비스를 사용하여 PDF 문서를 취합하는 방법을 숙지하는 것이 좋습니다. 이 섹션에서는 입력 문서를 포함하는 컬렉션 개체를 만들거나 반환된 컬렉션 개체에서 결과를 추출하는 등의 개념에 대해 다루지 않습니다. 자세한 내용은 [프로그래밍 방식으로 PDF 문서 조합](/help/forms/developing/programmatically-assembling-pdf-documents.md)을 참조하십시오.

>[!NOTE]
>
>어셈블러 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

>[!NOTE]
>
>DCX 문서에 대한 자세한 내용은 [어셈블러 서비스 및 DCX 참조](https://www.adobe.com/go/learn_aemforms_ddx_63)를 참조하십시오.

## {#summary-of-steps} 단계 요약

고유한 페이지 식별자(Bates 번호 매기기)가 포함된 PDF 문서를 조합하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일 포함
1. PDF Assembler 클라이언트를 만듭니다.
1. 기존 DCX 문서를 참조합니다.
1. 입력 PDF 문서를 참조합니다.
1. 초기 Bates 번호 값을 설정합니다.
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

AEM Forms이 JBoss가 아닌 지원되는 J2EE 응용 프로그램 서버에 배포되는 경우 adobe-utilities.jar 및 jbossall-client.jar 파일을 AEM Forms이 배포된 J2EE 응용 프로그램 서버에 해당하는 JAR 파일로 대체해야 합니다. 모든 AEM Forms JAR 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)을 참조하십시오.

**PDF Assembler 클라이언트 만들기**

어셈블리 작업을 프로그래밍 방식으로 수행하려면 먼저 어셈블러 서비스 클라이언트를 만들어야 합니다.

**기존 DCX 문서 참조**

PDF 문서를 조합하려면 DCX 문서를 참조해야 합니다. 예를 들어 이 섹션에 도입된 DDX 문서를 생각해 보십시오. 고유한 페이지 식별자가 포함된 PDF 문서를 취합하려면 DCX 문서에 `BatesNumber` 요소가 포함되어야 합니다.

**입력 PDF 문서 참조**

입력 PDF 문서를 참조하여 PDF 문서를 조합해야 합니다. 예를 들어 map.pdf 및 directions.pdf 문서를 참조하여 이러한 PDF 문서를 단일 PDF 문서로 결합해야 합니다.

**초기 Bates 번호 값 설정**

비즈니스 요구 사항에 맞게 초기 Bates 번호 값을 설정할 수 있습니다. 예를 들어 초기 값을 000100으로 설정해야 한다고 가정합니다. 초기 값을 설정하지 않으면 첫 번째 페이지의 값은 000000입니다.

**입력 PDF 문서 조합**

Assembler 서비스 클라이언트를 만든 후 `BatesNumber` 요소 정보가 포함된 DDC 문서를 참조하고, 입력 PDF 문서를 참조하고, 런타임 옵션을 설정한 후 Assembler 서비스에서 고유한 페이지 식별자가 포함된 PDF 문서를 어셈블하는 `invokeDDX` 작업을 호출할 수 있습니다.

**결과 추출**

Assembler 서비스는 작업 결과를 포함하는 컬렉션 개체를 반환합니다. 결과 PDF 문서 및 throw되는 모든 예외를 추출할 수 있습니다. 이러한 경우 암호화된 PDF 문서는 컬렉션 개체 내에 있습니다.

>[!NOTE]
>
>`invokeDDX` 작업을 호출하면 컬렉션 객체가 반환됩니다. 이 작업은 두 개 이상의 입력 PDF 문서를 어셈블러 서비스로 전달할 때 사용됩니다. 그러나 입력 PDF 문서를 Assembler 서비스에 하나만 전달하는 경우 `invokeOneDocument` 작업을 호출해야 합니다. 이 작업 사용에 대한 자세한 내용은 [암호화된 PDF 문서 정리](/help/forms/developing/assembling-encrypted-pdf-documents.md)를 참조하십시오.

**참고 항목**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[프로그래밍 방식으로 PDF 문서 취합](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API {#assemble-documents-with-bates-numbering-using-the-java-api}를 사용하여 Bates 번호 매기기를 사용하여 문서 조합

Assembler Service API(Java)를 사용하여 고유한 페이지 식별자(Bates 번호 매기기)를 사용하는 PDF 문서를 조합합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-assembler-client.jar 등의 클라이언트 JAR 파일을 포함합니다.

1. PDF Assembler 클라이언트를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 `AssemblerServiceClient` 개체를 만들고 `ServiceClientFactory` 개체를 전달합니다.

1. 기존 DCX 문서를 참조합니다.

   * 생성자를 사용하여 DCX 문서를 나타내는 `java.io.FileInputStream` 객체를 만들고 DCX 파일의 위치를 지정하는 문자열 값을 전달합니다.
   * 생성자를 사용하여 `com.adobe.idp.Document` 개체를 만들고 `java.io.FileInputStream` 개체를 전달합니다.

1. 입력 PDF 문서를 참조합니다.

   * `HashMap` 생성자를 사용하여 입력 PDF 문서를 저장하는 데 사용되는 `java.util.Map` 개체를 만듭니다.
   * 각 입력 PDF 문서에 대해 생성자를 사용하여 입력 PDF 문서의 위치를 전달하여 `java.io.FileInputStream` 개체를 만듭니다. 이 경우 비보안 PDF 문서의 위치를 전달합니다.
   * 각 입력 PDF 문서에 대해 `com.adobe.idp.Document` 개체를 만들고 PDF 문서가 포함된 `java.io.FileInputStream` 개체를 전달합니다.
   * `put` 메서드를 호출하고 다음 인수를 전달하여 `java.util.Map` 객체에 항목을 추가합니다.

      * 키 이름을 나타내는 문자열 값입니다. 이 값은 DCX 문서에 지정된 PDF 소스 요소의 값과 일치해야 합니다. 예를 들어 이 섹션에서 소개된 DCX 문서에 지정된 PDF 소스 파일의 이름은 Loan.pdf입니다.
      * 보안되지 않은 PDF 문서를 포함하는 `com.adobe.idp.Document` 객체입니다.

1. 초기 Bates 번호 값을 설정합니다.

   * 생성자를 사용하여 런타임 옵션을 저장하는 `AssemblerOptionSpec` 객체를 만듭니다.
   * `AssemblerOptionSpec` 개체의 `setFirstBatesNumber`을 호출하고 초기 값을 지정하는 숫자 값을 전달하여 초기 Bates 번호를 설정합니다.

1. 입력 PDF 문서를 조합합니다.

   `AssemblerServiceClient` 객체의 `invokeDDX` 메서드를 호출하고 다음 필수 값을 전달합니다.

   * DCX 문서를 나타내는 `com.adobe.idp.Document` 객체입니다.
   * 입력 보안되지 않은 PDF 파일을 포함하는 `java.util.Map` 개체입니다.
   * 기본 글꼴 및 작업 로그 수준을 포함하여 런타임 옵션을 지정하는 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 객체입니다.

   `invokeDDX` 메서드는 암호로 암호화된 PDF 문서를 포함하는 `com.adobe.livecycle.assembler.client.AssemblerResult` 개체를 반환합니다.

1. 결과를 추출합니다.

   새로 만든 PDF 문서를 얻으려면 다음 작업을 수행합니다.

   * `AssemblerResult` 객체의 `getDocuments` 메서드를 호출합니다. 이 작업은 `java.util.Map` 개체를 반환합니다.
   * `com.adobe.idp.Document` 개체를 찾을 때까지 `java.util.Map` 개체를 반복합니다.
   * `com.adobe.idp.Document` 개체의 `copyToFile` 메서드를 호출하여 PDF 문서를 추출합니다.

**참고 항목**

[빠른 시작(SOAP 모드):Java API를 사용하여 Bates 번호 매기기를 사용하여 PDF 문서 취합](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API {#assemble-documents-with-bates-numbering-using-the-web-service-api}를 사용하여 Bates 번호 매기기를 사용하여 문서 조합

Assembler Service API(웹 서비스)를 사용하여 고유한 페이지 식별자(Bates 번호 매기기)를 사용하는 PDF 문서를 조합합니다.

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
   * 생성자를 호출하고 DCX 문서의 파일 위치 및 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 객체를 만듭니다.
   * `System.IO.FileStream` 객체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 객체의 `Length` 속성을 가져와 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 객체의 `Read` 메서드를 호출하여 바이트 배열을 스트림 데이터로 채웁니다. 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달합니다.
   * 바이트 배열의 내용으로 `MTOM` 필드를 할당하여 `BLOB` 개체를 채웁니다.

1. 입력 PDF 문서를 참조합니다.

   * 각 입력 PDF 문서에 대해 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 입력 PDF 문서를 저장하는 데 사용됩니다.
   * 생성자를 호출하여 `System.IO.FileStream` 객체를 만듭니다. 입력 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * `System.IO.FileStream` 객체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 객체의 `Length` 속성을 가져와 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 객체의 `Read` 메서드를 호출하여 바이트 배열을 스트림 데이터로 채웁니다. 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달합니다.
   * 바이트 배열의 내용으로 `MTOM` 속성을 할당하여 `BLOB` 객체를 채웁니다.
   * `MyMapOf_xsd_string_To_xsd_anyType` 개체를 만듭니다. 이 컬렉션 개체는 입력 PDF 문서를 저장하는 데 사용됩니다.
   * 각 입력 PDF 문서에 대해 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체를 만듭니다. 예를 들어 2개의 입력 PDF 문서를 사용하는 경우 2개의 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체를 만듭니다.
   * 키 이름을 나타내는 문자열 값을 `MyMapOf_xsd_string_To_xsd_anyType_Item` 객체의 `key` 필드에 지정합니다. 이 값은 DCX 문서에 지정된 PDF 소스 요소의 값과 일치해야 합니다. 각 입력 PDF 문서에 대해 이 작업을 수행합니다.
   * PDF 문서를 저장하는 `BLOB` 개체를 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체의 `value` 필드에 할당합니다. 각 입력 PDF 문서에 대해 이 작업을 수행합니다.
   * `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체를 `MyMapOf_xsd_string_To_xsd_anyType` 개체에 추가합니다. `MyMapOf_xsd_string_To_xsd_anyType` 객체의 `Add` 메서드를 호출하고 `MyMapOf_xsd_string_To_xsd_anyType` 객체를 전달합니다. 각 입력 PDF 문서에 대해 이 작업을 수행합니다.

1. 초기 Bates 번호 값을 설정합니다.

   * 생성자를 사용하여 런타임 옵션을 저장하는 `AssemblerOptionSpec` 객체를 만듭니다.
   * `AssemblerOptionSpec` 개체에 속하는 `firstBatesNumber` 데이터 멤버에 숫자 값을 할당하여 초기 Bates 번호를 설정합니다.

1. 입력 PDF 문서를 조합합니다.

   `AssemblerServiceClient` 객체의 `invoke` 메서드를 호출하고 다음 값을 전달합니다.

   * DCX 문서를 나타내는 `BLOB` 객체입니다.
   * 입력 PDF 문서를 포함하는 `MyMapOf_xsd_string_To_xsd_anyType` 객체입니다. 해당 키는 PDF 소스 파일의 이름과 일치해야 하며 해당 값은 해당 파일에 해당하는 `BLOB` 객체여야 합니다.
   * 런타임 옵션을 지정하는 `AssemblerOptionSpec` 객체입니다.

   `invoke` 메서드는 작업 결과와 발생한 예외가 포함된 `AssemblerResult` 개체를 반환합니다.

1. 결과를 추출합니다.

   새로 만든 PDF 문서를 얻으려면 다음 작업을 수행합니다.

   * 결과 PDF 문서를 포함하는 `Map` 개체인 `AssemblerResult` 개체의 `documents` 필드에 액세스합니다.
   * 결과 문서의 이름과 일치하는 키를 찾을 때까지 `Map` 개체를 반복합니다. 그런 다음 해당 배열 멤버의 `value`을(를) `BLOB`로 캐스팅합니다.
   * PDF 문서의 `BLOB` 개체의 `MTOM` 속성에 액세스하여 이진 데이터를 추출합니다. PDF 파일에 기록할 수 있는 바이트 배열을 반환합니다.

**참고 항목**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
