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

Bates 번호 매기기를 사용하여 고유한 페이지 식별자가 포함된 PDF 문서를 취합할 수 있습니다. *Bates 번호* 매기기를 사용하면 여러 관련 문서에 고유한 식별자를 적용할 수 있습니다. 문서의 각 페이지(또는 문서 집합)에는 페이지를 고유하게 식별하는 Bates 번호가 할당됩니다. 예를 들어 BOM 정보가 들어 있고 어셈블리 생산과 연관된 제조 문서에는 식별자가 포함될 수 있습니다. Bates 번호에는 순차적으로 증가하는 숫자 값과 선택적 접두사와 접미어가 포함됩니다. 접두사 + 숫자 + 접미사는 *베이츠 패턴이라고 합니다*.

다음 그림은 문서 헤더에 있는 고유 식별자를 포함한 PDF 문서를 보여줍니다.

![au_au_batesnumber](assets/au_au_batesnumber.png)

이 토론의 목적으로 고유 페이지 식별자가 문서 헤더에 배치됩니다. 다음 DDX 문서가 사용되었다고 가정합니다.

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

이 DDX 문서는 *map.pdf* 및 *directions.pdf* 라는 두 개의 PDF 문서를 하나의 PDF 문서로 병합합니다. 결과 PDF 문서에는 고유한 페이지 식별자로 구성된 헤더가 포함되어 있습니다. 예를 들어 위의 그림에서 문서는 000016을 보여줍니다.

>[!NOTE]
>
>이 섹션을 읽기 전에 Assembler 서비스를 사용하여 PDF 문서를 조합하는 것에 익숙해지는 것이 좋습니다. 이 섹션에서는 입력 문서를 포함하는 컬렉션 개체를 만들거나 반환된 컬렉션 개체에서 결과를 추출하는 등의 개념을 논하지 않습니다. 자세한 내용은 [프로그래밍 방식으로 PDF 문서 조합을 참조하십시오](/help/forms/developing/programmatically-assembling-pdf-documents.md).

>[!NOTE]
>
>어셈블러 서비스에 대한 자세한 내용은 AEM Forms에 대한 [서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDX 문서에 대한 자세한 내용은 어셈블러 서비스 [및 DDX 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 단계 요약 {#summary-of-steps}

고유한 페이지 식별자(Bates 번호 매기기)가 포함된 PDF 문서를 조합하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일 포함
1. PDF 어셈블러 클라이언트 만들기
1. 기존 DDX 문서를 참조합니다.
1. 입력 PDF 문서를 참조합니다.
1. 초기 Bates 번호 값을 설정합니다.
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

AEM Forms이 JBoss 이외의 지원되는 J2EE 응용 프로그램 서버에 배포된 경우, adobe-utilities.jar 및 jbossall-client.jar 파일을 AEM Forms이 배포된 J2EE 응용 프로그램 서버에 고유한 JAR 파일로 대체해야 합니다. 모든 AEM Forms JAR 파일의 위치에 대한 자세한 내용은 AEM Forms Java 라이브러리 파일 [포함을 참조하십시오](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**PDF 어셈블러 클라이언트 만들기**

어셈블리 작업을 프로그래밍 방식으로 수행하려면 먼저 어셈블러 서비스 클라이언트를 만들어야 합니다.

**기존 DCX 문서 참조**

PDF 문서를 조합하려면 DDX 문서를 참조해야 합니다. 예를 들어 이 섹션에 도입된 DDX 문서를 생각해 보십시오. 고유한 페이지 식별자가 포함된 PDF 문서를 취합하려면 DDX 문서에 `BatesNumber` 요소가 포함되어야 합니다.

**참조 입력 PDF 문서**

PDF 문서를 취합하려면 입력 PDF 문서를 참조해야 합니다. 예를 들어 map.pdf 및 directions.pdf 문서를 참조하여 이러한 PDF 문서를 하나의 PDF 문서로 결합해야 합니다.

**초기 Bates 번호 값 설정**

비즈니스 요구 사항에 맞게 초기 Bates 번호 값을 설정할 수 있습니다. 예를 들어 초기 값을 000100으로 설정해야 한다고 가정합니다. 초기 값을 설정하지 않으면 첫 번째 페이지의 값은 00000입니다.

**입력 PDF 문서 조합**

어셈블러 서비스 클라이언트를 만든 후 `BatesNumber` `invokeDDX` 요소 정보가 포함된 DDDC 문서를 참조하고, 입력 PDF 문서를 참조하고, 런타임 옵션을 설정한 후, 어셈블러 서비스에서 고유한 페이지 식별자가 포함된 PDF 문서를 조합하는 작업을 호출할 수 있습니다.

**결과 추출**

어셈블러 서비스는 작업 결과를 포함하는 컬렉션 개체를 반환합니다. 결과 PDF 문서와 throw되는 모든 예외를 추출할 수 있습니다. 이러한 경우 암호화된 PDF 문서는 컬렉션 개체 내에 있습니다.

>[!NOTE]
>
>작업을 불러오면 컬렉션 개체가 `invokeDDX` 반환됩니다. 이 작업은 두 개 이상의 입력 PDF 문서를 어셈블러 서비스로 전달할 때 사용됩니다. 그러나 입력 PDF 문서를 한 개만 어셈블러 서비스로 전달하는 경우 작업을 `invokeOneDocument` 불러와야 합니다. 이 작업 사용에 대한 자세한 내용은 암호화된 PDF 문서 [합성을 참조하십시오](/help/forms/developing/assembling-encrypted-pdf-documents.md).

**참고 항목**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[프로그래밍 방식으로 PDF 문서 취합](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API를 사용하여 Bates 번호 매기기를 사용하여 문서 조합 {#assemble-documents-with-bates-numbering-using-the-java-api}

Assembler Service API(Java)를 사용하여 고유한 페이지 식별자(Bates 번호 매기기)를 사용하는 PDF 문서를 조합합니다.

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
   * 각 입력 PDF 문서에 대해 생성자를 사용하여 입력 PDF 문서의 위치를 전달하여 `java.io.FileInputStream` 개체를 만듭니다. 이 경우 비보안 PDF 문서의 위치를 전달합니다.
   * 입력된 각 PDF 문서에 대해 개체를 만들어 PDF 문서가 포함된 `com.adobe.idp.Document` `java.io.FileInputStream` 개체를 전달합니다.
   * 해당 메서드를 호출하고 다음 인수를 전달하여 `java.util.Map` 개체에 `put` 항목을 추가합니다.

      * 키 이름을 나타내는 문자열 값입니다. 이 값은 DCX 문서에 지정된 PDF 소스 요소의 값과 일치해야 합니다. 예를 들어, 이 섹션에서 소개된 DDX 문서에 지정된 PDF 소스 파일의 이름은 Loan.pdf입니다.
      * 보안되지 않은 PDF 문서를 포함하는 `com.adobe.idp.Document` 개체입니다.

1. 초기 Bates 번호 값을 설정합니다.

   * 생성자를 사용하여 런타임 옵션을 저장하는 `AssemblerOptionSpec` 객체를 만듭니다.
   * 개체의 이름을 호출하고 초기 값을 지정하는 숫자 값 `AssemblerOptionSpec` `setFirstBatesNumber` 을 전달하여 초기 Bates 번호를 설정합니다.

1. 입력 PDF 문서 조합

   개체의 `AssemblerServiceClient` `invokeDDX` 메서드를 호출하고 다음 필수 값을 전달합니다.

   * DDX 문서를 나타내는 `com.adobe.idp.Document` 개체입니다.
   * 입력 보안되지 않은 PDF 파일이 포함된 `java.util.Map` 개체입니다.
   * 기본 글꼴 및 작업 로그 수준을 포함하여 런타임 옵션을 지정하는 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 개체입니다.

   이 `invokeDDX` 메서드는 암호로 암호화된 PDF 문서를 포함하는 `com.adobe.livecycle.assembler.client.AssemblerResult` 개체를 반환합니다.

1. 결과를 추출합니다.

   새로 만든 PDF 문서를 얻으려면 다음 작업을 수행하십시오.

   * 개체의 `AssemblerResult` 메서드를 `getDocuments` 호출합니다. 이 작업은 `java.util.Map` 개체를 반환합니다.
   * 개체를 찾을 때까지 `java.util.Map` 개체를 `com.adobe.idp.Document` 반복합니다.
   * PDF 문서 `com.adobe.idp.Document` 를 추출하려면 개체의 `copyToFile` 방법을 불러옵니다.

**참고 항목**

[빠른 시작(SOAP 모드): Java API를 사용하여 Bates 번호 매기기를 사용하여 PDF 문서 취합](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API를 사용하여 Bates 번호를 사용하여 문서 조합 {#assemble-documents-with-bates-numbering-using-the-web-service-api}

Assembler Service API(웹 서비스)를 사용하여 고유한 페이지 식별자(Bates 번호 매기기)를 사용하는 PDF 문서를 조합합니다.

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
   * 생성자를 호출하고 DDX 문서의 파일 위치 및 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * 개체의 내용을 저장하는 바이트 배열을 `System.IO.FileStream` 만듭니다. 개체의 속성을 가져와 바이트 배열의 크기를 결정할 수 `System.IO.FileStream` `Length` 있습니다.
   * 개체의 메서드를 호출하여 바이트 배열을 스트림 데이터로 `System.IO.FileStream` 채웁니다 `Read` . 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 바이트 배열의 내용으로 해당 `BLOB` `MTOM` 필드를 할당하여 개체를 채웁니다.

1. 입력 PDF 문서를 참조합니다.

   * 각 입력 PDF 문서에 대해 생성자를 사용하여 `BLOB` 개체를 만듭니다. 이 `BLOB` 개체는 입력 PDF 문서를 저장하는 데 사용됩니다.
   * 생성자를 호출하여 `System.IO.FileStream` 개체를 만듭니다. 입력 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 개체의 내용을 저장하는 바이트 배열을 `System.IO.FileStream` 만듭니다. 개체의 속성을 가져와 바이트 배열의 크기를 결정할 수 `System.IO.FileStream` `Length` 있습니다.
   * 개체의 메서드를 호출하여 바이트 배열을 스트림 데이터로 `System.IO.FileStream` 채웁니다 `Read` . 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 바이트 배열의 컨텐츠로 해당 `BLOB` `MTOM` 속성을 지정하여 개체를 채웁니다.
   * 개체를 `MyMapOf_xsd_string_To_xsd_anyType` 만듭니다. 이 컬렉션 개체는 입력 PDF 문서를 저장하는 데 사용됩니다.
   * 각 입력 PDF 문서에 대해 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체를 만듭니다. 예를 들어 두 개의 입력 PDF 문서를 사용하는 경우 두 개의 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체를 만듭니다.
   * 키 이름을 나타내는 문자열 값을 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체의 `key` 필드에 할당합니다. 이 값은 DCX 문서에 지정된 PDF 소스 요소의 값과 일치해야 합니다. 각 입력 PDF 문서에 대해 이 작업을 수행합니다.
   * PDF 문서를 저장하는 `BLOB` 개체를 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체 `value` 필드에 할당합니다. 각 입력 PDF 문서에 대해 이 작업을 수행합니다.
   * 개체에 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체를 `MyMapOf_xsd_string_To_xsd_anyType` 추가합니다. 개체의 `MyMapOf_xsd_string_To_xsd_anyType` 메서드를 호출하고 개체를 `Add` `MyMapOf_xsd_string_To_xsd_anyType` 전달합니다. 각 입력 PDF 문서에 대해 이 작업을 수행합니다.

1. 초기 Bates 번호 값을 설정합니다.

   * 생성자를 사용하여 런타임 옵션을 저장하는 `AssemblerOptionSpec` 객체를 만듭니다.
   * 개체에 속하는 `firstBatesNumber` 데이터 멤버에 숫자 값을 할당하여 초기 Bates 번호를 `AssemblerOptionSpec` 설정합니다.

1. 입력 PDF 문서 조합

   개체의 `AssemblerServiceClient` 메서드를 `invoke` 호출하고 다음 값을 전달합니다.

   * DDX 문서를 나타내는 `BLOB` 개체입니다.
   * 입력 PDF 문서를 포함하는 `MyMapOf_xsd_string_To_xsd_anyType` 개체입니다. 해당 키는 PDF 소스 파일의 이름과 일치해야 하며 해당 값은 해당 파일에 해당하는 `BLOB` 객체여야 합니다.
   * 런타임 옵션을 지정하는 `AssemblerOptionSpec` 개체입니다.

   이 `invoke` `AssemblerResult` 메서드는 작업 결과와 발생한 예외를 포함하는 개체를 반환합니다.

1. 결과를 추출합니다.

   새로 만든 PDF 문서를 얻으려면 다음 작업을 수행하십시오.

   * 결과 PDF 문서를 포함하는 `AssemblerResult` 개체인 개체의 `documents` `Map` 필드에 액세스합니다.
   * 결과 문서의 이름과 일치하는 키를 찾을 때까지 `Map` 개체를 반복합니다. 그런 다음 해당 어레이 멤버 `value` 를 a로 캐스팅합니다 `BLOB`.
   * 개체의 속성에 액세스하여 PDF 문서를 나타내는 이진 데이터 `BLOB` 를 `MTOM` 추출합니다. PDF 파일에 기록할 수 있는 바이트 배열을 반환합니다.

**참고 항목**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
