---
title: Bates 번호 매기기를 사용하여 문서 어셈블
description: Java 및 웹 서비스 API를 사용하여 PDF 문서를 어셈블하려면 Bates 번호 매기기를 사용하십시오.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 2a4e21c4-f2f5-44cd-b8ed-7b572782a2f1
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1910'
ht-degree: 0%

---

# Bates 번호 매기기를 사용하여 문서 어셈블 {#assembling-documents-using-bates-numbering}

**이 문서의 샘플과 예제는 JEE 환경의 AEM Forms에 대해서만 적용됩니다.**

Bates 번호 매기기를 사용하여 고유한 페이지 식별자가 포함된 PDF 문서를 어셈블할 수 있습니다. *Bates 번호 매기기*&#x200B;는 관련 문서 배치에 고유 식별자를 적용하는 방법입니다. 문서(또는 문서 세트)의 각 페이지에는 페이지를 고유하게 식별하는 베이츠 번호가 지정됩니다. 예를 들어, BOM 정보가 포함되어 있고 어셈블리 생산과 연관된 제조 문서에는 식별자가 포함될 수 있습니다. Bates 번호에는 순차적으로 증가하는 숫자 값과 선택적 접두어 및 접미어가 포함됩니다. 접두사 + 숫자 + 접미사를 *베이츠 패턴*&#x200B;이라고 합니다.

다음 그림은 문서 헤더에 고유 식별자가 포함된 PDF 문서를 보여 줍니다.

![au_au_batesnumber](assets/au_au_batesnumber.png)

이를 위해 문서 헤더에 고유한 페이지 식별자가 배치됩니다. 다음 DDX 문서가 사용된다고 가정해 보십시오.

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

이 DDX 문서는 *map.pdf* 및 *directions.pdf*&#x200B;라는 두 개의 PDF 문서를 하나의 PDF 문서로 병합합니다. 결과 PDF 문서에는 고유한 페이지 식별자로 구성된 헤더가 포함됩니다. 예를 들어, 위 그림의 문서에는 000016 사항이 표시됩니다.

>[!NOTE]
>
>이 섹션을 읽기 전에 어셈블러 서비스를 사용하는 PDF 문서 어셈블링에 익숙해지는 것이 좋습니다. 이 섹션에서는 입력 문서가 포함된 컬렉션 객체 작성이나 반환된 컬렉션 객체에서 결과 추출과 같은 개념에 대해서는 다루지 않습니다. ([프로그래밍 방식으로 PDF 문서 어셈블](/help/forms/developing/programmatically-assembling-pdf-documents.md)을 참조하세요.)

>[!NOTE]
>
>어셈블러 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

>[!NOTE]
>
>DDX 문서에 대한 자세한 내용은 [어셈블러 서비스 및 DDX 참조](https://www.adobe.com/go/learn_aemforms_ddx_63)를 참조하십시오.

## 단계 요약 {#summary-of-steps}

고유한 페이지 식별자(Bates 번호 매기기)가 포함된 PDF 문서를 어셈블하려면 다음 작업을 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. PDF 어셈블러 클라이언트를 만듭니다.
1. 기존 DDX 문서를 참조합니다.
1. 입력 PDF 문서 참조.
1. 초기 Bates 번호 값을 설정합니다.
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

AEM Forms이 JBoss 이외의 지원되는 J2EE 애플리케이션 서버에 배포된 경우 adobe-utilities.jar 및 jbossall-client.jar 파일을 AEM Forms이 배포된 J2EE 애플리케이션 서버에 관련된 JAR 파일로 교체해야 합니다. 모든 AEM Forms JAR 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)을 참조하십시오.

**PDF 어셈블러 클라이언트 만들기**

어셈블러 작업을 프로그래밍 방식으로 수행하려면 먼저 어셈블러 서비스 클라이언트를 만들어야 합니다.

**기존 DDX 문서 참조**

PDF 문서를 어셈블하려면 DDX 문서를 참조해야 합니다. 예를 들어 이 섹션에 소개된 DDX 문서를 생각해 보십시오. 고유한 페이지 식별자가 포함된 PDF 문서를 어셈블하려면 DDX 문서에 `BatesNumber` 요소가 있어야 합니다.

**입력 PDF 문서 참조**

PDF 문서를 어셈블하려면 입력 PDF 문서를 참조해야 합니다. 예를 들어 이러한 PDF 문서를 단일 PDF 문서로 어셈블하려면 map.pdf 및 directions.pdf 문서를 참조해야 합니다.

**초기 베이츠 수 값 설정**

비즈니스 요구 사항에 맞게 초기 베이츠 번호 값을 설정할 수 있습니다. 예를 들어 초기 값을 000100으로 설정하는 것이 요구 사항이라고 가정해 보겠습니다. 초기 값을 설정하지 않으면 첫 번째 페이지의 값이 000000.

**입력 PDF 문서를 어셈블합니다**

어셈블러 서비스 클라이언트를 만들고 `BatesNumber` 요소 정보가 포함된 DDX 문서를 참조하며 입력 PDF 문서를 참조하고 런타임 옵션을 설정한 후 어셈블러 서비스에서 고유한 페이지 식별자가 포함된 PDF 문서를 어셈블하는 `invokeDDX` 작업을 호출할 수 있습니다.

**결과 추출**

어셈블러 서비스는 작업 결과가 포함된 컬렉션 개체를 반환합니다. 결과 PDF 문서와 throw되는 모든 예외를 추출할 수 있습니다. 이 경우 암호화된 PDF 문서는 컬렉션 개체 내에 있습니다.

>[!NOTE]
>
>`invokeDDX` 작업을 호출하면 컬렉션 개체가 반환됩니다. 이 작업은 두 개 이상의 입력 PDF 문서를 어셈블러 서비스에 전달할 때 사용됩니다. 그러나 한 개의 입력 PDF 문서만 어셈블러 서비스에 전달하는 경우에는 `invokeOneDocument` 작업을 호출해야 합니다. 이 작업 사용에 대한 자세한 내용은 [암호화된 PDF 문서 어셈블](/help/forms/developing/assembling-encrypted-pdf-documents.md)을 참조하십시오.

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[프로그래밍 방식으로 PDF 문서 어셈블](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API를 사용하여 Bates 번호 매기기를 사용하여 문서를 어셈블합니다. {#assemble-documents-with-bates-numbering-using-the-java-api}

어셈블러 서비스 API(Java)를 사용하여 고유한 PDF 식별자(Bates 번호 매기기)를 사용하는 페이지 문서를 어셈블합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-assembler-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. PDF 어셈블러 클라이언트를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하고 `ServiceClientFactory` 개체를 전달하여 `AssemblerServiceClient` 개체를 만듭니다.

1. 기존 DDX 문서를 참조합니다.

   * 생성자를 사용하고 DDX 파일의 위치를 지정하는 문자열 값을 전달하여 DDX 문서를 나타내는 `java.io.FileInputStream` 개체를 만듭니다.
   * 생성자를 사용하고 `java.io.FileInputStream` 개체를 전달하여 `com.adobe.idp.Document` 개체를 만듭니다.

1. 입력 PDF 문서 참조.

   * `HashMap` 생성자를 사용하여 입력 PDF 문서를 저장하는 데 사용되는 `java.util.Map` 개체를 만듭니다.
   * 각 입력 PDF 문서에 대해 해당 생성자를 사용하고 입력 PDF 문서의 위치를 전달하여 `java.io.FileInputStream` 개체를 만듭니다. 이 경우 보안되지 않은 PDF 문서의 위치를 전달합니다.
   * 각 입력 PDF 문서에 대해 `com.adobe.idp.Document` 개체를 만들고 PDF 문서가 포함된 `java.io.FileInputStream` 개체를 전달합니다.
   * `put` 메서드를 호출하고 다음 인수를 전달하여 `java.util.Map` 개체에 항목을 추가합니다.

      * 키 이름을 나타내는 문자열 값입니다. 이 값은 DDX 문서에 지정된 PDF 원본 요소의 값과 일치해야 합니다. 예를 들어, 이 섹션에 소개된 DDX 문서에 지정된 PDF 소스 파일의 이름은 Loan.pdf입니다.
      * 보안되지 않은 PDF 문서가 포함된 `com.adobe.idp.Document` 개체입니다.

1. 초기 Bates 번호 값을 설정합니다.

   * 생성자를 사용하여 런타임 옵션을 저장하는 `AssemblerOptionSpec` 개체를 만듭니다.
   * `AssemblerOptionSpec` 개체의 `setFirstBatesNumber`을(를) 호출하고 초기 값을 지정하는 숫자 값을 전달하여 초기 Bates 번호를 설정하십시오.

1. 입력 PDF 문서를 어셈블합니다.

   `AssemblerServiceClient` 개체의 `invokeDDX` 메서드를 호출하고 다음 필수 값을 전달하십시오.

   * DDX 문서를 나타내는 `com.adobe.idp.Document` 개체입니다.
   * 입력 비보안 PDF 파일이 포함된 `java.util.Map` 개체입니다.
   * 기본 글꼴 및 작업 로그 수준을 포함하여 런타임 옵션을 지정하는 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 개체입니다.

   `invokeDDX` 메서드가 암호로 암호화된 PDF 문서를 포함하는 `com.adobe.livecycle.assembler.client.AssemblerResult` 개체를 반환합니다.

1. 결과 추출

   새로 만든 PDF 문서를 가져오려면 다음 작업을 수행합니다.

   * `AssemblerResult` 개체의 `getDocuments` 메서드를 호출합니다. 이 작업은 `java.util.Map` 개체를 반환합니다.
   * `com.adobe.idp.Document` 개체를 찾을 때까지 `java.util.Map` 개체를 반복합니다.
   * `com.adobe.idp.Document` 개체의 `copyToFile` 메서드를 호출하여 PDF 문서를 추출하십시오.

**추가 참조**

[빠른 시작(SOAP 모드): Java API를 사용하여 PDF 번호 매기기를 사용하여 페이지 문서 어셈블](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API를 사용하여 Bates 번호 매기기를 사용하여 문서를 어셈블합니다. {#assemble-documents-with-bates-numbering-using-the-web-service-api}

어셈블러 서비스 API(웹 서비스)를 사용하여 고유한 PDF 식별자(Bates 번호 매기기)를 사용하는 페이지 문서를 어셈블합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. WSDL 정의 `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`을(를) 사용하는지 확인하십시오.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꾸십시오.

1. PDF 어셈블러 클라이언트를 만듭니다.

   * 기본 생성자를 사용하여 `AssemblerServiceClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `AssemblerServiceClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). `lc_version` 특성은 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.
   * `AssemblerServiceClient.Endpoint.Binding` 필드의 값을 가져와 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`(으)로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * `AssemblerServiceClient.ClientCredentials.UserName.UserName` 필드에 AEM Forms 사용자 이름을 지정하십시오.
      * 필드 `AssemblerServiceClient.ClientCredentials.UserName.Password`에 해당 암호 값을 지정하십시오.
      * 상수 값 `HttpClientCredentialType.Basic`을(를) 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.
      * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을(를) 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. 기존 DDX 문서를 참조합니다.

   * 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 DDX 문서를 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하고 DDX 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하여 바이트 배열을 스트림 데이터로 채웁니다. 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 해당 `MTOM` 필드를 바이트 배열의 내용으로 할당하여 `BLOB` 개체를 채웁니다.

1. 입력 PDF 문서 참조.

   * 각 입력 PDF 문서에 대해 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 입력 PDF 문서를 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하여 `System.IO.FileStream` 개체를 만듭니다. 입력 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하여 바이트 배열을 스트림 데이터로 채웁니다. 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 해당 `MTOM` 속성을 바이트 배열의 내용으로 할당하여 `BLOB` 개체를 채웁니다.
   * `MyMapOf_xsd_string_To_xsd_anyType` 개체를 만듭니다. 이 컬렉션 개체는 입력 PDF 문서를 저장하는 데 사용됩니다.
   * 각 입력 PDF 문서에 대해 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체를 만듭니다. 예를 들어 두 개의 입력 PDF 문서를 사용하는 경우 두 개의 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체를 만듭니다.
   * `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체의 `key` 필드에 키 이름을 나타내는 문자열 값을 지정하십시오. 이 값은 DDX 문서에 지정된 PDF 원본 요소의 값과 일치해야 합니다. (각 입력 PDF 문서에 대해 이 작업을 수행합니다.)
   * PDF 문서를 저장하는 `BLOB` 개체를 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체의 `value` 필드에 할당합니다. (각 입력 PDF 문서에 대해 이 작업을 수행합니다.)
   * `MyMapOf_xsd_string_To_xsd_anyType` 개체에 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체를 추가합니다. `MyMapOf_xsd_string_To_xsd_anyType` 개체의 `Add` 메서드를 호출하고 `MyMapOf_xsd_string_To_xsd_anyType` 개체를 전달하십시오. (각 입력 PDF 문서에 대해 이 작업을 수행합니다.)

1. 초기 Bates 번호 값을 설정합니다.

   * 생성자를 사용하여 런타임 옵션을 저장하는 `AssemblerOptionSpec` 개체를 만듭니다.
   * `AssemblerOptionSpec` 개체에 속하는 `firstBatesNumber` 데이터 멤버에 숫자 값을 할당하여 초기 Bates 번호를 설정합니다.

1. 입력 PDF 문서를 어셈블합니다.

   `AssemblerServiceClient` 개체의 `invoke` 메서드를 호출하고 다음 값을 전달하십시오.

   * DDX 문서를 나타내는 `BLOB` 개체입니다.
   * 입력 PDF 문서를 포함하는 `MyMapOf_xsd_string_To_xsd_anyType` 개체입니다. 해당 키는 PDF 원본 파일의 이름과 일치해야 하며 해당 값은 해당 파일에 해당하는 `BLOB` 개체여야 합니다.
   * 런타임 옵션을 지정하는 `AssemblerOptionSpec` 개체입니다.

   `invoke` 메서드가 작업 결과와 발생한 모든 예외를 포함하는 `AssemblerResult` 개체를 반환합니다.

1. 결과 추출

   새로 만든 PDF 문서를 가져오려면 다음 작업을 수행합니다.

   * 결과 PDF 문서를 포함하는 `Map` 개체인 `AssemblerResult` 개체의 `documents` 필드에 액세스합니다.
   * 결과 문서 이름과 일치하는 키를 찾을 때까지 `Map` 개체를 반복합니다. 그런 다음 배열 구성원의 `value`을(를) `BLOB`(으)로 캐스팅합니다.
   * `BLOB` 개체의 `MTOM` 속성에 액세스하여 PDF 문서를 나타내는 이진 데이터를 추출합니다. PDF 파일에 쓸 수 있는 바이트 배열이 반환됩니다.

**추가 참조**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
