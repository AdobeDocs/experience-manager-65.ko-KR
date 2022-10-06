---
title: Bates 번호 지정을 사용하여 문서 조립
seo-title: Assembling Documents Using Bates Numbering
description: Java 및 웹 서비스 API를 사용하여 PDF 문서를 어셈블하려면 Bates 번호 지정을 사용합니다.
seo-description: Use Bates numbering to assemble PDF documents using the Java and Web Service API.
uuid: 28d5faeb-6915-41a2-b6a0-78d255df024f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 77e9b895-1313-4a5b-a2d5-cdb65bdc1966
role: Developer
exl-id: 2a4e21c4-f2f5-44cd-b8ed-7b572782a2f1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1922'
ht-degree: 0%

---

# Bates 번호 지정을 사용하여 문서 조립 {#assembling-documents-using-bates-numbering}

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms용입니다.**

Bates 번호 매기기를 사용하여 고유한 페이지 식별자를 포함하는 PDF 문서를 어셈블할 수 있습니다. *베이츠 번호 매기기* 는 관련 문서 일괄 처리에 고유 식별자를 적용하는 방법입니다. 문서(또는 문서 세트)의 각 페이지에는 페이지를 고유하게 식별하는 Bates 번호가 지정됩니다. 예를 들어, BOM 정보를 포함하고 어셈블리 생성과 연관된 제조 문서에는 식별자가 포함될 수 있습니다. Bates 번호에는 순차적으로 증가하는 숫자 값과 선택적 접두사 및 접미사가 포함됩니다. 접두사 + 숫자 + 접미사를 *베이츠 패턴*.

다음 그림은 문서 머리글에 있는 고유 식별자를 포함하는 PDF 문서를 보여줍니다.

![au_au_batesnumber](assets/au_au_batesnumber.png)

이 토론을 위해 고유한 페이지 ID가 문서의 머리글에 배치됩니다. 다음 DDX 문서가 사용된다고 가정하십시오.

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

이 DDX 문서는 *map.pdf* 및 *directions.pdf* 단일 PDF 문서로 이동합니다. 결과 PDF 문서에는 고유한 페이지 식별자로 구성된 헤더가 포함되어 있습니다. 예를 들어 위의 그림에서 문서는 000016.

>[!NOTE]
>
>이 섹션을 읽기 전에 어셈블러 서비스를 사용하여 PDF 문서 조립에 익숙해지는 것이 좋습니다. 이 단원에서는 입력 문서가 포함된 컬렉션 개체 만들기 또는 반환된 수집 개체에서 결과 추출과 같은 개념을 다루지 않습니다. (자세한 내용은 [프로그래밍 방식으로 PDF 문서 조립](/help/forms/developing/programmatically-assembling-pdf-documents.md))

>[!NOTE]
>
>어셈블러 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDX 문서에 대한 자세한 내용은 [어셈블러 서비스 및 DDX 참조](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 단계 요약 {#summary-of-steps}

고유한 페이지 식별자(Bates 번호 지정)가 포함된 PDF 문서를 어셈블하려면 다음 작업을 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. PDF 어셈블러 클라이언트를 만듭니다.
1. 기존 DDX 문서를 참조합니다.
1. 참조 입력 PDF 문서
1. 초기 Bates 번호 값을 설정합니다.
1. 입력 PDF 문서를 어셈블합니다.
1. 결과를 추출합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함하십시오. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms이 JBoss에 배포되는 경우 필요)

AEM Forms이 JBoss 이외의 지원되는 J2EE 애플리케이션 서버에 배포된 경우, adobe-utilities.jar 및 jbossall-client.jar 파일을 AEM Forms이 배포된 J2EE 애플리케이션 서버에 고유한 JAR 파일로 대체해야 합니다. 모든 AEM Forms JAR 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**PDF 어셈블러 클라이언트 만들기**

어셈블러 작업을 프로그래밍 방식으로 수행하려면 먼저 어셈블러 서비스 클라이언트를 만들어야 합니다.

**기존 DDX 문서 참조**

PDF 문서를 어셈블하려면 DDX 문서를 참조해야 합니다. 예를 들어 이 섹션에서 도입된 DDX 문서를 생각해 보십시오. 고유한 페이지 식별자를 포함하는 PDF 문서를 어셈블하려면 DDX 문서에 `BatesNumber` 요소를 생성하지 않습니다.

**참조 입력 PDF 문서**

PDF 문서를 어셈블하려면 입력 PDF 문서를 참조해야 합니다. 예를 들어, 맵.pdf 및 directions.pdf 문서를 참조하여 이러한 PDF 문서를 단일 PDF 문서로 어셈블해야 합니다.

**초기 Bates 번호 값을 설정합니다.**

비즈니스 요구 사항에 맞게 초기 Bates 번호 값을 설정할 수 있습니다. 예를 들어 초기 값을 000100으로 설정해야 한다고 가정합니다. 초기 값을 설정하지 않으면 첫 번째 페이지의 값은 000000.

**입력 PDF 문서 조합**

어셈블러 서비스 클라이언트를 만든 후 다음을 포함하는 DDX 문서를 참조합니다 `BatesNumber` 요소 정보, 입력 PDF 문서 참조 및 런타임 옵션을 설정하면 `invokeDDX` 고유한 페이지 식별자를 포함하는 PDF 문서를 어셈블러 서비스에서 어셈블하는 작업입니다.

**결과 추출**

어셈블러 서비스는 작업 결과가 포함된 컬렉션 개체를 반환합니다. 결과 PDF 문서와 throw되는 예외를 추출할 수 있습니다. 이 경우 암호화된 PDF 문서는 수집 객체 내에 있습니다.

>[!NOTE]
>
>컬렉션 개체는 `invokeDDX` 작업. 이 작업은 두 개 이상의 입력 PDF 문서를 어셈블러 서비스에 전달할 때 사용됩니다. 그러나 입력 PDF 문서를 어셈블러 서비스에 하나만 전달하면 `invokeOneDocument` 작업. 이 작업 사용에 대한 자세한 내용은 [암호화된 PDF 문서 정리](/help/forms/developing/assembling-encrypted-pdf-documents.md).

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[프로그래밍 방식으로 PDF 문서 조립](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API를 사용하여 Bates 번호 매기기를 사용하여 문서 조합 {#assemble-documents-with-bates-numbering-using-the-java-api}

어셈블러 서비스 API(Java)를 사용하여 고유한 페이지 식별자(Bates 번호 지정)를 사용하는 PDF 문서를 어셈블합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-assembler-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. PDF 어셈블러 클라이언트를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 객체입니다.
   * 만들기 `AssemblerServiceClient` 생성자를 사용하여 객체를 전달하고 `ServiceClientFactory` 개체.

1. 기존 DDX 문서를 참조합니다.

   * 만들기 `java.io.FileInputStream` 생성자를 사용하고 DDX 파일의 위치를 지정하는 문자열 값을 전달하여 DDX 문서를 나타내는 개체입니다.
   * 만들기 `com.adobe.idp.Document` 생성자를 사용하여 객체를 전달하고 `java.io.FileInputStream` 개체.

1. 참조 입력 PDF 문서

   * 만들기 `java.util.Map` 입력 PDF 문서를 저장하는 데 사용되는 객체 `HashMap` 생성자입니다.
   * 각 입력 PDF 문서에 대해 `java.io.FileInputStream` 생성자를 사용하여 입력 PDF 문서의 위치를 전달하여 개체를 가져옵니다. 이 경우 비보안 PDF 문서의 위치를 전달합니다.
   * 각 입력 PDF 문서에 대해 `com.adobe.idp.Document` 개체 및 전달 `java.io.FileInputStream` PDF 문서를 포함하는 객체입니다.
   * 에 항목 추가 `java.util.Map` 객체를 호출하여 `put` 메서드와 다음 인수를 전달합니다.

      * 키 이름을 나타내는 문자열 값입니다. 이 값은 DDX 문서에 지정된 PDF 소스 요소의 값과 일치해야 합니다. 예를 들어 이 섹션에서 도입된 DDX 문서에 지정된 PDF 소스 파일의 이름은 Loan.pdf입니다.
      * A `com.adobe.idp.Document` 비보안 PDF 문서를 포함하는 객체입니다.

1. 초기 Bates 번호 값을 설정합니다.

   * 만들기 `AssemblerOptionSpec` 생성자를 사용하여 런타임 옵션을 저장하는 개체입니다.
   * 를 호출하여 초기 Bates 번호를 설정합니다. `AssemblerOptionSpec` 개체 `setFirstBatesNumber` 초기 값을 지정하는 숫자 값을 전달합니다.

1. 입력 PDF 문서를 어셈블합니다.

   를 호출합니다 `AssemblerServiceClient` 개체 `invokeDDX` 메서드를 사용하여 다음 필수 값을 전달합니다.

   * A `com.adobe.idp.Document` DDX 문서를 나타내는 객체입니다.
   * A `java.util.Map` 입력 비보안 PDF 파일을 포함하는 개체입니다.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 기본 글꼴 및 작업 로그 수준을 포함하여 런타임 옵션을 지정하는 개체입니다.

   다음 `invokeDDX` 메서드 반환 `com.adobe.livecycle.assembler.client.AssemblerResult` 암호로 암호화된 PDF 문서를 포함하는 객체입니다.

1. 결과를 추출합니다.

   새로 만든 PDF 문서를 가져오려면 다음 작업을 수행하십시오.

   * 를 호출합니다 `AssemblerResult` 개체 `getDocuments` 메서드를 사용합니다. 이 작업은 `java.util.Map` 개체.
   * 를 통해 반복 `java.util.Map` 개체를 찾을 때까지 `com.adobe.idp.Document` 개체.
   * 를 호출합니다 `com.adobe.idp.Document` 개체 `copyToFile` PDF 문서를 추출하는 방법입니다.

**추가 참조**

[빠른 시작(SOAP 모드): Java API를 사용하여 Bates 번호를 사용하여 PDF 문서 어셈블링](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API를 사용하여 Bates 번호를 매기는 문서를 어셈블합니다 {#assemble-documents-with-bates-numbering-using-the-web-service-api}

어셈블러 서비스 API(웹 서비스)를 사용하여 고유한 페이지 식별자(Bates 번호 지정)를 사용하는 PDF 문서를 어셈블합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` (AEM Forms을 호스팅하는 서버의 IP 주소 사용)

1. PDF 어셈블러 클라이언트를 만듭니다.

   * 만들기 `AssemblerServiceClient` 기본 생성자를 사용하여 개체를 만듭니다.
   * 만들기 `AssemblerServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). 를 사용할 필요가 없습니다 `lc_version` 속성을 사용합니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.
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
   * 를 호출하여 바이트 배열을 스트림 데이터로 채웁니다 `System.IO.FileStream` 개체 `Read` 메서드를 사용합니다. 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 을(를) 채우기 `BLOB` 개체를 할당하여 개체를 개체 개체 `MTOM` 바이트 배열의 내용을 포함하는 필드입니다.

1. 참조 입력 PDF 문서

   * 각 입력 PDF 문서에 대해 `BLOB` 생성자를 사용하여 개체를 작성합니다. 다음 `BLOB` 개체는 입력 PDF 문서를 저장하는 데 사용됩니다.
   * 만들기 `System.IO.FileStream` 개체를 생성자로 호출하여 개체를 가져옵니다. 입력 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 내용을 저장하는 바이트 배열을 만듭니다 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성을 사용합니다.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채웁니다 `System.IO.FileStream` 개체 `Read` 메서드를 사용합니다. 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 을(를) 채우기 `BLOB` 개체를 할당하여 개체를 개체 개체 `MTOM` 바이트 배열의 내용을 포함하는 속성입니다.
   * 만들기 `MyMapOf_xsd_string_To_xsd_anyType` 개체. 이 컬렉션 개체는 입력 PDF 문서를 저장하는 데 사용됩니다.
   * 각 입력 PDF 문서에 대해 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체. 예를 들어 두 개의 입력 PDF 문서를 사용하는 경우 두 개의 입력 문서를 만듭니다 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체.
   * 키 이름을 나타내는 문자열 값을 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체 `key` 필드. 이 값은 DDX 문서에 지정된 PDF 소스 요소의 값과 일치해야 합니다. 각 입력 PDF 문서에 대해 이 작업을 수행합니다.
   * 을(를) 지정합니다. `BLOB` PDF 문서를 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체 `value` 필드. 각 입력 PDF 문서에 대해 이 작업을 수행합니다.
   * 추가 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체 `MyMapOf_xsd_string_To_xsd_anyType` 개체. 를 호출합니다 `MyMapOf_xsd_string_To_xsd_anyType` 개체 `Add` 메서드 및 전달 `MyMapOf_xsd_string_To_xsd_anyType` 개체. 각 입력 PDF 문서에 대해 이 작업을 수행합니다.

1. 초기 Bates 번호 값을 설정합니다.

   * 만들기 `AssemblerOptionSpec` 생성자를 사용하여 런타임 옵션을 저장하는 개체입니다.
   * 숫자 값을 로 할당하여 초기 Bates 번호를 설정합니다. `firstBatesNumber` 에 속하는 데이터 멤버 `AssemblerOptionSpec` 개체.

1. 입력 PDF 문서를 어셈블합니다.

   를 호출합니다 `AssemblerServiceClient` 개체 `invoke` 메서드를 사용하여 다음 값을 전달합니다.

   * A `BLOB` DDX 문서를 나타내는 객체입니다.
   * 다음 `MyMapOf_xsd_string_To_xsd_anyType` 입력 PDF 문서를 포함하는 객체입니다. 해당 키는 PDF 소스 파일의 이름과 일치해야 하며 해당 값은 `BLOB` 해당 파일에 해당하는 개체입니다.
   * An `AssemblerOptionSpec` 런타임 옵션을 지정하는 개체입니다.

   다음 `invoke` 메서드 반환 `AssemblerResult` 작업의 결과와 발생한 예외를 포함하는 객체입니다.

1. 결과를 추출합니다.

   새로 만든 PDF 문서를 가져오려면 다음 작업을 수행하십시오.

   * 액세스 권한 `AssemblerResult` 개체 `documents` 필드, 즉 `Map` 결과 PDF 문서를 포함하는 객체입니다.
   * 를 통해 반복 `Map` 결과 문서의 이름과 일치하는 키를 찾을 때까지 객체를 선택합니다. 그런 다음 해당 어레이 멤버의 `value` 변환 후 `BLOB`.
   * PDF 문서에 액세스하여 이진 데이터를 추출합니다 `BLOB` 개체 `MTOM` 속성을 사용합니다. PDF 파일에 쓸 수 있는 바이트 배열을 반환합니다.

**추가 참조**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
