---
title: 문서 디지털 서명 및 인증
description: 서명 서비스를 사용하여 PDF 문서에 디지털 서명 필드를 추가 및 삭제하고, PDF 문서의 서명 필드 이름을 검색하고, 서명 필드를 수정하고, PDF 문서에 디지털 서명하고, PDF 문서를 인증하고, PDF 문서에서 디지털 서명을 확인하고, PDF 문서의 모든 디지털 서명을 확인하고, 서명 필드에서 디지털 서명을 제거합니다.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: c200f345-40ab-46fd-b6ed-f3af0a23796b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '16916'
ht-degree: 0%

---

# 문서 디지털 서명 및 인증 {#digitally-signing-and-certifying-documents}

**이 문서의 샘플과 예제는 JEE 환경의 AEM Forms에 대해서만 적용됩니다.**

**서명 서비스 정보**

서명 서비스를 사용하면 조직에서 배포하고 받는 Adobe PDF 문서의 보안 및 개인 정보를 보호할 수 있습니다. 이 서비스는 디지털 서명 및 인증을 사용하여 의도한 수신자만 문서를 변경할 수 있도록 합니다. 보안 기능은 문서 자체에 적용되므로, 문서는 전체 라이프 사이클에 대해 안전하게 제어됩니다. 문서는 오프라인으로 다운로드할 때와 조직에 다시 제출될 때 방화벽 이후에도 안전하게 보호됩니다.

>[!NOTE]
>
>PDF 문서 서명과 같은 특정 작업이 호출될 때 호출되는 서명 서비스에 대한 사용자 지정 서명 처리기를 만들 수 있습니다.

**서명 필드 이름**

일부 서명 서비스 작업에서는 작업을 수행할 서명 필드의 이름을 지정해야 합니다. 예를 들어 PDF 문서에 서명할 때 서명할 서명 필드의 이름을 지정합니다. 서명 필드의 전체 이름이 `form1[0].Form1[0].SignatureField1[0]`이라고 가정합니다. `SignatureField1[0]` 대신 `form1[0].Form1[0].SignatureField1[0]`을(를) 지정할 수 있습니다.

경우에 따라 충돌로 인해 서명 서비스가 잘못된 필드에 서명(또는 서명 필드 이름이 필요한 다른 작업을 수행)하게 됩니다. 이 충돌은 이름 `SignatureField1[0]`이(가) 같은 PDF 문서에서 둘 이상의 위치에 있기 때문입니다. 예를 들어, 이름이 `form1[0].Form1[0].SignatureField1[0]`과(와) `form1[0].Form1[0].SubForm1[0].SignatureField1[0]`인 두 개의 서명 필드가 포함된 PDF 문서에 `SignatureField1[0]`을(를) 지정한다고 가정해 보겠습니다. 이 경우 서명 서비스는 문서의 모든 서명 필드를 반복하는 동안 찾은 첫 번째 서명 필드에 서명합니다.

PDF 문서 내에 여러 서명 필드가 있는 경우 서명 필드의 전체 이름을 지정하는 것이 좋습니다. 즉, `form1[0].Form1[0].SignatureField1[0]` 대신 `SignatureField1[0]`을(를) 지정하십시오.

서명 서비스를 사용하여 다음 작업을 수행할 수 있습니다.

* PDF 문서에 디지털 서명 필드를 추가하고 삭제합니다. ([서명 필드 추가](digitally-signing-certifying-documents.md#adding-signature-fields)를 참조하십시오.)
* PDF 문서에서 서명 필드의 이름을 검색합니다. ([서명 필드 이름 검색](digitally-signing-certifying-documents.md#retrieving-signature-field-names)을 참조하십시오.)
* 서명 필드를 수정합니다. ([서명 필드 수정](digitally-signing-certifying-documents.md#modifying-signature-fields)을 참조하십시오.)
* PDF 문서에 디지털 서명합니다. ([PDF 문서에 디지털 서명하기](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)를 참조하십시오.)
* PDF 문서를 인증합니다. ([PDF 문서 인증](digitally-signing-certifying-documents.md#certifying-pdf-documents)을 참조하십시오.)
* PDF 문서에서 디지털 서명의 유효성을 검사합니다. ([디지털 서명 확인](digitally-signing-certifying-documents.md#verifying-digital-signatures)을 참조하십시오.)
* PDF 문서에서 모든 디지털 서명의 유효성을 검사합니다. ([여러 디지털 서명 확인](digitally-signing-certifying-documents.md#verifying-digital-signatures)을 참조하십시오.)
* 서명 필드에서 디지털 서명을 제거합니다. ([디지털 서명 제거](digitally-signing-certifying-documents.md#removing-digital-signatures)를 참조하십시오.)

>[!NOTE]
>
>서명 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

## 서명 필드 추가 {#adding-signature-fields}

디지털 서명은 서명의 그래픽 표현이 포함된 양식 필드인 서명 필드에 나타납니다. 서명 필드는 표시되거나 표시되지 않을 수 있습니다. 서명자는 기존 서명 필드를 사용하거나 서명 필드를 프로그래밍 방식으로 추가할 수 있습니다. 두 경우 모두 PDF 문서에 서명하려면 서명 필드가 있어야 합니다.

서명 서비스 Java API 또는 서명 웹 서비스 API를 사용하여 서명 필드를 프로그래밍 방식으로 추가할 수 있습니다. PDF 문서에 두 개 이상의 서명 필드를 추가할 수 있지만 각 서명 필드 이름은 고유해야 합니다.

>[!NOTE]
>
>일부 PDF 문서 유형에서는 서명 필드를 프로그래밍 방식으로 추가할 수 없습니다. 서명 서비스 및 서명 필드 추가에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary-of-steps}

PDF 문서에 서명 필드를 추가하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. 서명 클라이언트를 만듭니다.
1. 서명 필드가 추가된 PDF 문서를 가져옵니다.
1. 서명 필드를 추가합니다.
1. PDF 문서를 PDF 파일로 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필수)

**서명 클라이언트 만들기**

서명 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 서명 서비스 클라이언트를 만들어야 합니다.

**서명 필드가 추가된 PDF 문서 가져오기**

서명 필드가 추가된 PDF 문서를 가져옵니다.

**서명 필드 추가**

서명 필드를 PDF 문서에 성공적으로 추가하려면 서명 필드의 위치를 식별하는 좌표 값을 지정합니다. (보이지 않는 서명 필드를 추가하는 경우 이러한 값은 필요하지 않습니다.) 또한 서명이 서명 필드에 적용된 후 PDF 문서에서 잠길 필드를 지정할 수 있습니다.

**PDF 문서를 PDF 파일로 저장**

서명 서비스에서 PDF 문서에 서명 필드를 추가한 후 사용자가 Acrobat 또는 Adobe Reader에서 열 수 있도록 문서를 PDF 파일로 저장할 수 있습니다.

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF 문서에 디지털 서명](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Java API를 사용하여 서명 필드 추가 {#add-signature-fields-using-the-java-api}

서명 API(Java)를 사용하여 서명 필드를 추가합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-signatures-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. 서명 클라이언트 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하고 `SignatureServiceClient` 개체를 전달하여 `ServiceClientFactory` 개체를 만듭니다.

1. 서명 필드가 추가된 PDF 문서 가져오기

   * 해당 생성자를 사용하고 PDF 문서의 위치를 지정하는 문자열 값을 전달하여 서명 필드가 추가된 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만듭니다.
   * 생성자를 사용하고 `com.adobe.idp.Document` 개체를 전달하여 `java.io.FileInputStream` 개체를 만듭니다.

1. 서명 필드 추가

   * 해당 생성자를 사용하여 서명 필드 위치를 지정하는 `PositionRectangle` 개체를 만듭니다. 생성자 내에서 좌표 값을 지정합니다.
   * 필요한 경우 서명 필드에 디지털 서명을 적용할 때 잠기는 필드를 지정하는 `FieldMDPOptions` 개체를 만듭니다.
   * `SignatureServiceClient` 개체의 `addSignatureField` 메서드를 호출하고 다음 값을 전달하여 PDF 문서에 서명 필드를 추가합니다.

      * `com.adobe.idp`. 서명 필드가 추가된 PDF 문서를 나타내는 `Document` 개체입니다.
      * 서명 필드의 이름을 지정하는 문자열 값입니다.
      * 서명 필드가 추가되는 페이지 번호를 나타내는 `java.lang.Integer` 값입니다.
      * 서명 필드의 위치를 지정하는 `PositionRectangle` 개체입니다.
      * 디지털 서명이 서명 필드에 적용된 후 잠기는 PDF 문서의 필드를 지정하는 `FieldMDPOptions` 개체입니다. 이 매개 변수 값은 선택 사항이며 `null`을(를) 전달할 수 있습니다.

   * 다양한 런타임 값을 지정하는 `PDFSeedValueOptions` 개체입니다. 이 매개 변수 값은 선택 사항이며 `null`을(를) 전달할 수 있습니다.

     `addSignatureField` 메서드가 `com.adobe.idp`을(를) 반환합니다. 서명 필드가 포함된 PDF 문서를 나타내는 `Document` 개체입니다.

   >[!NOTE]
   >
   >`SignatureServiceClient` 개체의 `addInvisibleSignatureField` 메서드를 호출하여 보이지 않는 서명 필드를 추가할 수 있습니다.

1. PDF 문서를 PDF 파일로 저장

   * `java.io.File` 개체를 만들고 파일 확장명이 .pdf인지 확인하십시오.
   * `com.adobe.idp` 호출. `Document` 개체의 `copyToFile` 메서드를 사용하여 `Document` 개체의 내용을 파일에 복사합니다. `com.adobe.idp`을(를) 사용하는지 확인하십시오. `Document` 메서드에서 반환된 `addSignatureField` 개체입니다.

**추가 참조**

[서명 서비스 API 빠른 시작](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

### 웹 서비스 API를 사용하여 서명 필드 추가 {#add-signature-fields-using-the-web-service-api}

서명 API(웹 서비스)를 사용하여 서명 필드를 추가하려면:

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. WSDL 정의 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`을(를) 사용하는지 확인하십시오.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꾸십시오.

1. 서명 클라이언트 만들기

   * 기본 생성자를 사용하여 `SignatureServiceClient` 개체를 만듭니다.
   * `SignatureServiceClient.Endpoint.Address` 생성자를 사용하여 `System.ServiceModel.EndpointAddress` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/SignatureService?WSDL`). `lc_version` 특성은 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * `System.ServiceModel.BasicHttpBinding` 필드의 값을 가져와 `SignatureServiceClient.Endpoint.Binding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`(으)로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * `SignatureServiceClient.ClientCredentials.UserName.UserName` 필드에 AEM Forms 사용자 이름을 지정하십시오.
      * 필드 `SignatureServiceClient.ClientCredentials.UserName.Password`에 해당 암호 값을 지정하십시오.
      * 상수 값 `HttpClientCredentialType.Basic`을(를) 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.
      * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을(를) 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. 서명 필드가 추가된 PDF 문서 가져오기

   * 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 서명 필드를 포함할 PDF 문서를 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하고 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * 해당 `BLOB` 속성을 바이트 배열의 내용으로 할당하여 `MTOM` 개체를 채웁니다.

1. 서명 필드 추가

   `SignatureServiceClient` 개체의 `addSignatureField` 메서드를 호출하고 다음 값을 전달하여 PDF 문서에 서명 필드를 추가합니다.

   * 서명 필드가 추가된 PDF 문서를 나타내는 `BLOB` 개체입니다.
   * 서명 필드 이름을 지정하는 문자열 값입니다.
   * 서명 필드가 추가되는 페이지 번호를 나타내는 정수 값입니다.
   * 서명 필드의 위치를 지정하는 `PositionRect` 개체입니다.
   * 디지털 서명이 서명 필드에 적용된 후 잠기는 PDF 문서의 필드를 지정하는 `FieldMDPOptions` 개체입니다. 이 매개 변수 값은 선택 사항이며 `null`을(를) 전달할 수 있습니다.
   * 다양한 런타임 값을 지정하는 `PDFSeedValueOptions` 개체입니다. 이 매개 변수 값은 선택 사항이며 `null`을(를) 전달할 수 있습니다.

   `addSignatureField` 메서드는 서명 필드가 포함된 PDF 문서를 나타내는 `BLOB` 개체를 반환합니다.

1. PDF 문서를 PDF 파일로 저장

   * 해당 생성자를 호출하고 서명 필드와 파일을 열 모드를 포함할 PDF 문서의 파일 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `BLOB` 메서드에서 반환된 `addSignatureField` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `BLOB` 개체의 `binaryData` 데이터 멤버의 값을 가져와서 바이트 배열을 채웁니다.
   * 해당 생성자를 호출하고 `System.IO.BinaryWriter` 개체를 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.BinaryWriter` 개체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 PDF 파일에 씁니다.

**추가 참조**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 서명 필드 이름 검색 중 {#retrieving-signature-field-names}

서명 또는 인증하려는 PDF 문서에 있는 모든 서명 필드의 이름을 검색할 수 있습니다. PDF 문서에 있는 서명 필드 이름을 잘 모르거나 이름을 확인하려는 경우 프로그래밍 방식으로 검색할 수 있습니다. Signature 서비스에서 서명 필드의 정규화된 이름(예: `form1[0].grantApplication[0].page1[0].SignatureField1[0]`)을 반환합니다.

>[!NOTE]
>
>서명 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary_of_steps-1}

서명 필드 이름을 검색하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. 서명 클라이언트를 만듭니다.
1. 서명 필드가 포함된 PDF 문서를 가져옵니다.
1. 서명 필드 이름을 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필수)

이러한 JAR 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)을 참조하십시오.

**서명 클라이언트 만들기**

서명 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 서명 서비스 클라이언트를 만들어야 합니다.

**서명 필드가 포함된 PDF 문서를 가져옵니다**

서명 필드가 포함된 PDF 문서를 검색합니다.

**서명 필드 이름 검색**

하나 이상의 서명 필드가 포함된 PDF 문서를 검색한 후 서명 필드 이름을 검색할 수 있습니다.

**추가 참조**

[Java API를 사용하여 서명 필드 이름 검색](digitally-signing-certifying-documents.md#retrieve-signature-field-names-using-the-java-api)

[웹 서비스 API를 사용하여 서명 필드 검색](digitally-signing-certifying-documents.md#retrieve-signature-field-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[서명 필드 추가](digitally-signing-certifying-documents.md#adding-signature-fields)

### Java API를 사용하여 서명 필드 이름 검색 {#retrieve-signature-field-names-using-the-java-api}

서명 API(Java)를 사용하여 서명 필드 이름을 검색합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-signatures-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. 서명 클라이언트 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하고 `SignatureServiceClient` 개체를 전달하여 `ServiceClientFactory` 개체를 만듭니다.

1. 서명 필드가 포함된 PDF 문서 가져오기

   * 해당 생성자를 사용하고 PDF 문서의 위치를 지정하는 문자열 값을 전달하여 서명 필드가 포함된 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만듭니다.
   * 생성자를 사용하고 `com.adobe.idp.Document` 개체를 전달하여 `java.io.FileInputStream` 개체를 만듭니다.

1. 서명 필드 이름 검색

   * `SignatureServiceClient` 개체의 `getSignatureFieldList` 메서드를 호출하고 서명 필드가 포함된 PDF 문서가 포함된 `com.adobe.idp.Document` 개체를 전달하여 서명 필드 이름을 검색합니다. 이 메서드는 각 요소에 `java.util.List` 개체가 포함된 `PDFSignatureField` 개체를 반환합니다. 이 개체를 사용하면 표시 여부와 같은 서명 필드에 대한 추가 정보를 얻을 수 있습니다.
   * `java.util.List` 개체를 반복하여 서명 필드 이름이 있는지 확인합니다. PDF 문서의 각 서명 필드에 대해 별도의 `PDFSignatureField` 개체를 가져올 수 있습니다. 서명 필드의 이름을 가져오려면 `PDFSignatureField` 개체의 `getName` 메서드를 호출하십시오. 이 메서드는 서명 필드 이름을 지정하는 문자열 값을 반환합니다.

**추가 참조**

[서명 필드 이름 검색 중](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[빠른 시작(SOAP 모드): Java API를 사용하여 서명 필드 이름 검색](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-retrieving-signature-field-names-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 서명 필드 검색 {#retrieve-signature-field-using-the-web-service-api}

서명 API(웹 서비스)를 사용하여 서명 필드 이름 검색:

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. WSDL 정의 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`을(를) 사용하는지 확인하십시오.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꾸십시오.

1. 서명 클라이언트 만들기

   * 기본 생성자를 사용하여 `SignatureServiceClient` 개체를 만듭니다.
   * `SignatureServiceClient.Endpoint.Address` 생성자를 사용하여 `System.ServiceModel.EndpointAddress` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/SignatureService?WSDL`). `lc_version` 특성은 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * `System.ServiceModel.BasicHttpBinding` 필드의 값을 가져와 `SignatureServiceClient.Endpoint.Binding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`(으)로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * `SignatureServiceClient.ClientCredentials.UserName.UserName` 필드에 AEM Forms 사용자 이름을 지정하십시오.
      * 필드 `SignatureServiceClient.ClientCredentials.UserName.Password`에 해당 암호 값을 지정하십시오.
      * 상수 값 `HttpClientCredentialType.Basic`을(를) 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.
      * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을(를) 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. 서명 필드가 포함된 PDF 문서 가져오기

   * 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 서명 필드가 포함된 PDF 문서를 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하고 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * `BLOB` 필드에 바이트 배열 내용을 할당하여 `MTOM` 개체를 채웁니다.

1. 서명 필드 이름 검색

   * `SignatureServiceClient` 개체의 `getSignatureFieldList` 메서드를 호출하고 서명 필드가 포함된 PDF 문서가 포함된 `BLOB` 개체를 전달하여 서명 필드 이름을 검색합니다. 이 메서드는 각 요소에 `MyArrayOfPDFSignatureField` 개체가 포함된 `PDFSignatureField` 컬렉션 개체를 반환합니다.
   * `MyArrayOfPDFSignatureField` 개체를 반복하여 서명 필드 이름이 있는지 확인합니다. PDF 문서의 각 서명 필드에 대해 `PDFSignatureField` 개체를 가져올 수 있습니다. 서명 필드의 이름을 가져오려면 `PDFSignatureField` 개체의 `getName` 메서드를 호출하십시오. 이 메서드는 서명 필드 이름을 지정하는 문자열 값을 반환합니다.

**추가 참조**

[서명 필드 이름 검색 중](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 서명 필드 수정 {#modifying-signature-fields}

Java API 및 웹 서비스 API를 사용하여 PDF 문서에 있는 서명 필드를 수정할 수 있습니다. 서명 필드를 수정하려면 해당 서명 필드 잠금 사전 값 또는 시드 값 사전 값을 조작해야 합니다.

*필드 잠금 사전*&#x200B;은(는) 서명 필드에 서명할 때 잠기는 필드 목록을 지정합니다. 잠긴 필드는 사용자가 필드를 변경할 수 없도록 합니다. *시드 값 사전*&#x200B;에 서명이 적용될 때 사용되는 제한 정보가 포함되어 있습니다. 예를 들어 서명을 무효화하지 않고 발생할 수 있는 작업을 제어하는 권한을 변경할 수 있습니다.

기존 서명 필드를 수정하여 변화하는 비즈니스 요구 사항을 반영하도록 PDF 문서를 변경할 수 있습니다. 예를 들어, 새 비즈니스 요구 사항을 충족하려면 문서에 서명한 후 모든 문서 필드를 잠가야 할 수 있습니다.

이 섹션에서는 필드 잠금 사전과 시드 값 사전 값을 모두 수정하여 서명 필드를 수정하는 방법을 설명합니다. 서명 필드 잠금 사전을 변경하면 서명 필드에 서명할 때 PDF 문서의 모든 필드가 잠깁니다. 시드 값 사전을 변경하면 문서에 대한 특정 유형의 변경이 금지됩니다.

>[!NOTE]
>
>서명 서비스 및 서명 필드 수정에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary_of_steps-2}

PDF 문서의 서명 필드를 수정하려면 다음 작업을 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. 서명 클라이언트를 만듭니다.
1. 수정할 서명 필드가 포함된 PDF 문서를 가져옵니다.
1. 사전 값을 설정합니다.
1. 서명 필드를 수정합니다.
1. PDF 문서를 PDF 파일로 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필수)

이러한 JAR 파일의 위치에 대한 자세한 내용은 [LiveCycle Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)을 참조하십시오.

**서명 클라이언트 만들기**

서명 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 서명 서비스 클라이언트를 만들어야 합니다.

**수정할 서명 필드가 포함된 PDF 문서를 가져옵니다**

수정할 서명 필드가 포함된 PDF 문서를 검색합니다.

**사전 값 설정**

서명 필드를 수정하려면 해당 필드 잠금 사전 또는 시드 값 사전에 값을 할당합니다. 서명 필드 잠금 사전 값 지정에는 서명 필드에 서명할 때 잠기는 PDF 문서 필드 지정이 포함됩니다. (이 섹션에서는 모든 필드를 잠그는 방법에 대해 설명합니다.)

다음 시드 값 사전 값을 설정할 수 있습니다.

* **수정 검사**: 서명이 서명 필드에 적용될 때 해지 검사를 수행할지 여부를 지정합니다.
* **인증서 옵션**: 인증서 시드 값 사전에 값을 할당합니다. 인증서 옵션을 지정하기 전에 인증서 시드 값 사전에 익숙해지는 것이 좋습니다. ([PDF 참조](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf)를 참조하세요.)
* **다이제스트 옵션**: 서명에 사용되는 다이제스트 알고리즘을 지정합니다. 유효한 값은 SHA1, SHA256, SHA384, SHA512 및 RIPEMD160입니다.
* **필터**: 서명 필드에 사용되는 필터를 지정합니다. 예를 들어 Adobe.PPKLite 필터를 사용할 수 있습니다. ([PDF 참조](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf)를 참조하세요.)
* **플래그 옵션**: 이 서명 필드와 연결된 플래그 값을 지정합니다. 값이 1이면 서명자는 항목에 대해 지정된 값만 사용해야 합니다. 값이 0이면 다른 값이 허용됨을 의미합니다. 다음은 비트 위치입니다.

   * **1(필터):** 서명 필드에 서명하는 데 사용할 서명 처리기입니다.
   * **2(SubFilter):** 서명할 때 사용할 수 있는 인코딩을 나타내는 이름의 배열입니다.
   * **3(V)**: 서명 필드에 서명하는 데 사용할 서명 처리기의 최소 필요 버전 번호입니다
   * **4(이유):** 문서에 서명하는 가능한 이유를 지정하는 문자열 배열입니다.
   * **5(PDFLegalWarnings):** 가능한 법적 증명을 지정하는 문자열 배열

* **법적 증명**: 문서가 인증되면 문서의 내용을 모호하게 하거나 오해의 소지가 있는 특정 유형의 내용을 자동으로 검사합니다. 예를 들어 주석은 인증된 내용을 이해하는 데 중요한 텍스트를 모호하게 할 수 있습니다. 검색 프로세스는 이러한 유형의 콘텐츠가 있음을 나타내는 경고를 생성합니다. 또한 경고를 생성했을 수 있는 콘텐츠에 대한 추가 설명도 제공합니다.
* **권한**: 서명을 무효화하지 않고 PDF 문서에 사용할 수 있는 권한을 지정합니다.
* **이유**: 이 문서에 서명해야 하는 이유를 지정합니다.
* **타임스탬프**: 타임스탬프 옵션을 지정합니다. 예를 들어 사용되는 타임스탬프 서버의 URL을 설정할 수 있습니다.
* **버전**: 서명 필드에 서명하는 데 사용할 서명 처리기의 최소 버전 번호를 지정합니다.

**서명 필드 수정**

서명 서비스 클라이언트를 만들고 수정할 서명 필드가 포함된 PDF 문서를 검색하고 사전 값을 설정한 후 서명 서비스에 서명 필드를 수정하도록 지시할 수 있습니다. 그런 다음 서명 서비스는 수정된 서명 필드가 포함된 PDF 문서를 반환합니다. 원본 PDF 문서는 영향을 받지 않습니다.

**PDF 문서를 PDF 파일로 저장**

사용자가 PDF 또는 Adobe Reader에서 열 수 있도록 수정된 서명 필드가 포함된 Acrobat 문서를 PDF 파일로 저장합니다.

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[서명 서비스 API 빠른 시작](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

[PDF 문서에 디지털 서명](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Java API를 사용하여 서명 필드 수정 {#modify-signature-fields-using-the-java-api}

서명 API(Java)를 사용하여 서명 필드를 수정합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-signatures-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. 서명 클라이언트 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하고 `SignatureServiceClient` 개체를 전달하여 `ServiceClientFactory` 개체를 만듭니다.

1. 수정할 서명 필드가 포함된 PDF 문서 가져오기

   * 생성자를 사용하고 PDF 문서의 위치를 지정하는 문자열 값을 전달하여 수정할 서명 필드가 포함된 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만듭니다.
   * 생성자를 사용하고 `com.adobe.idp.Document` 개체를 전달하여 `java.io.FileInputStream` 개체를 만듭니다.

1. 사전 값 설정

   * 해당 생성자를 사용하여 `PDFSignatureFieldProperties` 개체를 만듭니다. `PDFSignatureFieldProperties` 개체는 서명 필드 잠금 사전 및 시드 값 사전 정보를 저장합니다.
   * 해당 생성자를 사용하여 `PDFSeedValueOptionSpec` 개체를 만듭니다. 이 개체를 사용하면 시드 값 사전 값을 설정할 수 있습니다.
   * `PDFSeedValueOptionSpec` 개체의 `setMdpValue` 메서드를 호출하고 `MDPPermissions.NoChanges` 열거형 값을 전달하여 PDF 문서를 변경할 수 없습니다.
   * 해당 생성자를 사용하여 `FieldMDPOptionSpec` 개체를 만듭니다. 이 개체를 사용하면 서명 필드 잠금 사전 값을 설정할 수 있습니다.
   * `FieldMDPOptionSpec` 개체의 `setMdpValue` 메서드를 호출하고 `FieldMDPAction.ALL` 열거형 값을 전달하여 PDF 문서의 모든 필드를 잠급니다.
   * `PDFSignatureFieldProperties` 개체의 `setSeedValue` 메서드를 호출하고 `PDFSeedValueOptionSpec` 개체를 전달하여 시드 값 사전 정보를 설정하십시오.
   * `PDFSignatureFieldProperties`개체의 `setFieldMDP` 메서드를 호출하고 `FieldMDPOptionSpec` 개체를 전달하여 서명 필드 잠금 사전 정보를 설정합니다.

   >[!NOTE]
   >
   >설정할 수 있는 모든 시드 값 사전 값을 보려면 `PDFSeedValueOptionSpec` 클래스 참조를 참조하십시오. ([AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)를 참조하십시오.)

1. 서명 필드 수정

   `SignatureServiceClient` 개체의 `modifySignatureField` 메서드를 호출하고 다음 값을 전달하여 서명 필드를 수정합니다.

   * 수정할 서명 필드가 포함된 PDF 문서를 저장하는 `com.adobe.idp.Document` 개체
   * 서명 필드의 이름을 지정하는 문자열 값
   * 서명 필드 잠금 사전 및 시드 값 사전 정보를 저장하는 `PDFSignatureFieldProperties` 개체

   `modifySignatureField` 메서드는 수정된 서명 필드가 포함된 PDF 문서를 저장하는 `com.adobe.idp.Document` 개체를 반환합니다.

1. PDF 문서를 PDF 파일로 저장

   * `java.io.File` 개체를 만들고 파일 이름 확장명이 .pdf인지 확인하십시오.
   * `com.adobe.idp.Document` 개체의 `copyToFile` 메서드를 호출하여 `com.adobe.idp.Document` 개체의 내용을 파일에 복사합니다. `com.adobe.idp.Document` 메서드가 반환한 `modifySignatureField` 개체를 사용하는지 확인하십시오.

### 웹 서비스 API를 사용하여 서명 필드 수정 {#modify-signature-fields-using-the-web-service-api}

서명 API(웹 서비스)를 사용하여 서명 필드를 수정합니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. WSDL 정의 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`을(를) 사용하는지 확인하십시오.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꾸십시오.

1. 서명 클라이언트 만들기

   * 기본 생성자를 사용하여 `SignatureServiceClient` 개체를 만듭니다.
   * `SignatureServiceClient.Endpoint.Address` 생성자를 사용하여 `System.ServiceModel.EndpointAddress` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/SignatureService?WSDL`). `lc_version` 특성은 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * `System.ServiceModel.BasicHttpBinding` 필드의 값을 가져와 `SignatureServiceClient.Endpoint.Binding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`(으)로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * `SignatureServiceClient.ClientCredentials.UserName.UserName` 필드에 AEM Forms 사용자 이름을 지정하십시오.
      * 필드 `SignatureServiceClient.ClientCredentials.UserName.Password`에 해당 암호 값을 지정하십시오.
      * 상수 값 `HttpClientCredentialType.Basic`을(를) 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.
      * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을(를) 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. 수정할 서명 필드가 포함된 PDF 문서 가져오기

   * 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 수정할 서명 필드가 포함된 PDF 문서를 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하고 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * 해당 `BLOB` 속성을 바이트 배열의 내용으로 할당하여 `MTOM` 개체를 채웁니다.

1. 사전 값 설정

   * 해당 생성자를 사용하여 `PDFSignatureFieldProperties` 개체를 만듭니다. 이 개체는 서명 필드 잠금 사전 및 시드 값 사전 정보를 저장합니다.
   * 해당 생성자를 사용하여 `PDFSeedValueOptionSpec` 개체를 만듭니다. 이 개체를 사용하면 시드 값 사전 값을 설정할 수 있습니다.
   * `MDPPermissions.NoChanges` 열거형 값을 `PDFSeedValueOptionSpec` 개체의 `mdpValue` 데이터 멤버에 할당하여 PDF 문서를 변경할 수 없습니다.
   * 해당 생성자를 사용하여 `FieldMDPOptionSpec` 개체를 만듭니다. 이 개체를 사용하면 서명 필드 잠금 사전 값을 설정할 수 있습니다.
   * `FieldMDPAction.ALL` 열거형 값을 `FieldMDPOptionSpec` 개체의 `mdpValue` 데이터 멤버에 할당하여 PDF 문서의 모든 필드를 잠급니다.
   * `PDFSeedValueOptionSpec` 개체를 `PDFSignatureFieldProperties` 개체의 `seedValue` 데이터 멤버에 할당하여 시드 값 사전 정보를 설정합니다.
   * `FieldMDPOptionSpec` 개체를 `PDFSignatureFieldProperties` 개체의 `fieldMDP` 데이터 멤버에 할당하여 서명 필드 잠금 사전 정보를 설정합니다.

   >[!NOTE]
   >
   >설정할 수 있는 모든 시드 값 사전 값을 보려면 `PDFSeedValueOptionSpec` 클래스 참조를 참조하십시오. ([AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en) 참조).

1. 서명 필드 수정

   `SignatureServiceClient` 개체의 `modifySignatureField` 메서드를 호출하고 다음 값을 전달하여 서명 필드를 수정합니다.

   * 수정할 서명 필드가 포함된 PDF 문서를 저장하는 `BLOB` 개체
   * 서명 필드의 이름을 지정하는 문자열 값
   * 서명 필드 잠금 사전 및 시드 값 사전 정보를 저장하는 `PDFSignatureFieldProperties` 개체

   `modifySignatureField` 메서드는 수정된 서명 필드가 포함된 PDF 문서를 저장하는 `BLOB` 개체를 반환합니다.

1. PDF 문서를 PDF 파일로 저장

   * 해당 생성자를 호출하고 서명 필드를 포함할 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `BLOB` 메서드가 반환하는 `addSignatureField` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `BLOB` 개체의 `MTOM` 데이터 멤버의 값을 가져와서 바이트 배열을 채웁니다.
   * 해당 생성자를 호출하고 `System.IO.BinaryWriter` 개체를 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.BinaryWriter` 개체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 PDF 파일에 씁니다.

**추가 참조**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## PDF 문서에 디지털 서명 {#digitally-signing-pdf-documents}

디지털 서명을 PDF 문서에 적용하여 보안 수준을 제공할 수 있습니다. 디지털 서명은 자필 서명과 마찬가지로 서명자가 자신을 확인하고 문서에 대해 진술할 수 있는 수단을 제공합니다. 문서에 디지털 서명을 할 때 사용하는 기술은 서명자와 수신자 모두가 서명된 내용에 대해 명확하게 이해하고 서명된 이후 문서가 변경되지 않았음을 확신할 수 있도록 도와줍니다.

PDF 문서는 공개 키 기술을 통해 서명됩니다. 서명자는 공개 키와 개인 키의 두 가지 키를 갖습니다. 개인 키는 서명 시 사용할 수 있어야 하는 사용자의 자격 증명에 저장됩니다. 공개 키는 서명을 확인하기 위해 수신자가 사용할 수 있어야 하는 사용자의 인증서에 저장됩니다. 해지된 인증서에 대한 정보는 CA(인증 기관)에서 배포한 CRL(인증서 해지 목록) 및 OCSP(온라인 인증서 상태 프로토콜) 응답에서 찾을 수 있습니다. 서명 시간은 타임스탬핑 인증 기관이라고 하는 신뢰할 수 있는 소스에서 가져올 수 있습니다.

>[!NOTE]
>
>PDF 문서에 디지털 서명을 하려면 먼저 인증서를 AEM Forms에 추가해야 합니다. 인증서는 관리 콘솔을 사용하거나 Trust Manager API를 프로그래밍 방식으로 사용하여 추가됩니다. [Trust Manager API를 사용하여 자격 증명 가져오기](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)를 참조하십시오.

PDF 문서에 프로그래밍 방식으로 디지털 서명할 수 있습니다. PDF 문서에 디지털 서명을 할 때는 AEM Forms에 있는 보안 자격 증명을 참조해야 합니다. 자격 증명은 서명에 사용되는 개인 키입니다.

PDF 문서에 서명할 때 서명 서비스는 다음 단계를 수행합니다.

1. Signature 서비스는 요청에 지정된 별칭을 전달하여 Truststore에서 자격 증명을 검색합니다.
1. Truststore는 지정된 자격 증명을 검색합니다.
1. 자격 증명은 서명 서비스로 반환되며 문서에 서명하는 데 사용됩니다. 또한 자격 증명은 향후 요청을 위해 별칭에 캐시됩니다.

보안 자격 증명 처리에 대한 자세한 내용은 응용 프로그램 서버에 대한 *AEM Forms 설치 및 배포* 안내서를 참조하십시오.

>[!NOTE]
>
>문서에 서명하는 것과 문서에 서명하는 것 사이에는 차이가 있다. ([PDF 문서 인증](digitally-signing-certifying-documents.md#certifying-pdf-documents)을 참조하십시오.)

>[!NOTE]
>
>일부 PDF 문서에서는 서명을 지원하지 않습니다. 서명 서비스 및 디지털 서명 문서에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

>[!NOTE]
>
>서명 서비스는 문서 인증과 같은 작업에 대한 입력으로 포함된 PDF 데이터가 있는 XDP 파일을 지원하지 않습니다. 이 작업으로 인해 서명 서비스에서 `PDFOperationException`이(가) 발생합니다. 이 문제를 해결하려면 PDF 유틸리티 서비스를 사용하여 XDP 파일을 PDF 파일로 변환한 다음 변환된 PDF 파일을 서명 서비스 작업에 전달합니다. [PDF 유틸리티 작업](/help/forms/developing/pdf-utilities.md#working-with-pdf-utilities)을(를) 참조하십시오.

**nShield HSM 자격 증명 암호화**

nShield nShield HSM 자격 증명을 사용하여 PDF 문서에 서명하거나 인증할 때 AEM Forms이 배포된 J2EE 애플리케이션 서버를 다시 시작할 때까지 새 자격 증명을 사용할 수 없습니다. 그러나 구성 값을 설정하면 J2EE 응용 프로그램 서버를 다시 시작하지 않고도 서명 또는 인증 작업이 작동합니다.

/opt/nfast/cknfastrc(또는 c:\nfast\cknfastrc)에 있는 cknfastrc 파일에 다음 구성 값을 추가할 수 있습니다.

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

이 구성 값을 cknfastrc 파일에 추가한 후에는 J2EE 애플리케이션 서버를 다시 시작하지 않고도 새 자격 증명을 사용할 수 있습니다.

>[!NOTE]
>
> SDK를 다시 시작하려면 &#39;Ctrl+C&#39; 명령을 사용하는 것이 좋습니다. 예를 들어 Java 프로세스를 중지하는 것과 같은 대체 방법을 사용하여 AEM SDK를 다시 시작하면 AEM 개발 환경에서 불일치가 발생할 수 있습니다.

**서명을 신뢰할 수 없습니다**

동일한 PDF 문서를 인증하고 서명할 때 인증 서명을 신뢰할 수 없는 경우 Acrobat 또는 Adobe Reader에서 PDF 문서를 열 때 첫 번째 서명에 대해 노란색 삼각형이 나타납니다. 이러한 상황을 방지하려면 인증 서명을 신뢰해야 합니다.

**XFA 기반 양식인 문서에 서명하는 중**

서명 서비스 API를 사용하여 XFA 기반 양식에 서명하려고 하면 Acrobat의 `View` `Signed` `Version`에서 데이터가 누락될 수 있습니다. 예를 들어 다음 워크플로를 고려하십시오.

* Designer을 사용하여 만든 XDP 파일을 사용하여 서명 필드가 포함된 양식 디자인과 양식 데이터가 포함된 XML 데이터를 병합합니다. Forms 서비스를 사용하여 대화형 PDF 문서를 생성합니다.
* 서명 서비스 API를 사용하여 PDF 문서에 서명합니다.

### 단계 요약 {#summary_of_steps-3}

PDF 문서에 디지털 서명하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. 서명 서비스 클라이언트를 만듭니다.
1. 서명할 PDF 문서를 가져옵니다.
1. PDF 문서에 서명합니다.
1. 서명된 PDF 문서를 PDF 파일로 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필수)

**서명 클라이언트 만들기**

서명 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 서명 서비스 클라이언트를 만들어야 합니다.

**서명할 PDF 문서 가져오기**

PDF 문서에 서명하려면 서명 필드가 포함된 PDF 문서를 가져와야 합니다. PDF 문서에 서명 필드가 없으면 서명할 수 없습니다. 서명 필드는 Designer을 사용하거나 프로그래밍 방식으로 추가할 수 있습니다.

**PDF 문서에 서명**

PDF 문서에 서명할 때 서명 서비스에서 사용하는 런타임 옵션을 설정할 수 있습니다. 다음 옵션을 설정할 수 있습니다.

* 모양 옵션
* 해지 확인
* 타임스탬프 값

`PDFSignatureAppearanceOptionSpec` 개체를 사용하여 모양 옵션을 설정합니다. 예를들어, `PDFSignatureAppearanceOptionSpec` 개체의 `setShowDate` 메서드를 호출하고 `true`을(를) 전달하여 서명 내에 날짜를 표시할 수 있습니다.

PDF 문서에 디지털 서명하는 데 사용되는 인증서가 해지되었는지 여부를 확인하는 해지 검사를 수행할지 여부도 지정할 수 있습니다. 해지 확인을 수행하기 위해 다음 값 중 하나를 지정할 수 있습니다.

* **NoCheck**: 해지 검사를 수행하지 않습니다.
* **BestEffort**: 항상 체인에 있는 모든 인증서의 해지 확인을 시도합니다. 확인하는 데 문제가 발생하면 취소가 유효한 것으로 간주됩니다. 오류가 발생하면 인증서가 해지되지 않았다고 가정하십시오.
* **CheckIfAvailable:** 해지 정보를 사용할 수 있는 경우 체인에 있는 모든 인증서의 해지 여부를 확인합니다. 확인하는 데 문제가 발생하면 취소가 유효하지 않은 것으로 간주됩니다. 오류가 발생하면 인증서가 해지되고 유효하지 않다고 가정하십시오. (기본값)
* **AlwaysCheck**: 체인에 있는 모든 인증서의 취소를 확인하십시오. 인증서에 해지 정보가 없으면 해지가 유효하지 않은 것으로 간주됩니다.

인증서에 대한 해지 검사를 수행하려면 `CRLOptionSpec` 개체를 사용하여 CRL(인증서 해지 목록) 서버에 대한 URL을 지정할 수 있습니다. 그러나 해지 확인을 수행하려 하고 CRL 서버에 대한 URL을 지정하지 않는 경우 서명 서비스는 인증서에서 URL을 가져옵니다.

해지 검사를 수행할 때 CRL 서버를 사용하는 대신 OCSP(온라인 인증서 상태 프로토콜) 서버를 사용할 수 있습니다. 일반적으로 CRL 서버가 아닌 OCSP 서버를 사용하는 경우 해지 확인이 더 빨리 수행됩니다. ([https://tools.ietf.org/html/rfc2560](https://tools.ietf.org/html/rfc2560)에서 &quot;온라인 인증서 상태 프로토콜&quot;을 참조하십시오.)

Signature 서비스에서 Adobe 애플리케이션 및 서비스를 사용하여 사용하는 CRL 및 OCSP 서버 순서를 설정할 수 있습니다. 예를 들어 OCSP 서버가 Adobe Applications and Services에서 먼저 설정된 경우 OCSP 서버를 확인하고 CRL 서버를 선택합니다. (AAC 도움말의 &quot;Trust Store를 사용하여 인증서 및 자격 증명 관리&quot;를 참조하십시오.)

해지 확인을 수행하지 않도록 지정하면 서명 서비스에서 문서 서명 또는 인증에 사용된 인증서가 해지되었는지 확인하지 않습니다. 즉, CRL 및 OCSP 서버 정보는 무시됩니다.

>[!NOTE]
>
>인증서에 CRL 또는 OCSP 서버를 지정할 수 있지만 `CRLOptionSpec` 및 `OCSPOptionSpec` 개체를 사용하여 인증서에 지정된 URL을 무시할 수 있습니다. 예를 들어 CRL 서버를 재정의하려면 `CRLOptionSpec` 개체의 `setLocalURI` 메서드를 호출할 수 있습니다.

타임스탬핑은 서명 또는 인증된 문서가 수정된 시간을 추적하는 과정을 의미한다. 문서에 서명한 후에는 문서 소유자가 수정해도 안 됩니다. 타임스탬프는 서명 또는 인증된 문서의 유효성을 검사하는 데 도움이 됩니다. `TSPOptionSpec` 개체를 사용하여 타임스탬프 옵션을 설정할 수 있습니다. 예를 들어 TSP(타임스탬프 제공자) 서버의 URL을 지정할 수 있습니다.

>[!NOTE]
>
>Java 및 웹 서비스에서는 섹션과 해당 빠른 시작을 단계별로 살펴보면서 해지 확인이 사용됩니다. CRL 또는 OCSP 서버 정보가 지정되지 않았으므로 서버 정보는 PDF 문서에 디지털 서명하는 데 사용된 인증서에서 가져옵니다.

PDF 문서에 성공적으로 서명하려면 `form1[0].#subform[1].SignatureField3[3]`과 같이 디지털 서명이 포함될 서명 필드의 정규화된 이름을 지정할 수 있습니다. XFA 양식 필드를 사용하는 경우 서명 필드의 일부 이름을 사용할 수도 있습니다. `SignatureField3[3]`.

PDF 문서에 디지털 서명하려면 보안 자격 증명도 참조해야 합니다. 보안 자격 증명을 참조하려면 별칭을 지정합니다. 별칭은 PKCS#12 파일(.pfx 확장명 포함) 또는 HSM(하드웨어 보안 모듈)에 있을 수 있는 실제 자격 증명에 대한 참조입니다. 보안 자격 증명에 대한 자세한 내용은 응용 프로그램 서버에 대한 *AEM Forms 설치 및 배포* 안내서를 참조하십시오.

**서명된 PDF 문서 저장**

서명 서비스에서 PDF 문서에 디지털 서명을 한 후 사용자가 Acrobat 또는 Adobe Reader에서 열 수 있도록 PDF 파일로 저장할 수 있습니다.

**추가 참조**

[Java API를 사용하여 PDF 문서에 디지털 서명](digitally-signing-certifying-documents.md#digitally-sign-pdf-documents-using-the-java-api)

[웹 서비스 API를 사용하여 PDF 문서에 디지털 서명](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[서명 필드 추가](digitally-signing-certifying-documents.md#adding-signature-fields)

[서명 필드 이름 검색 중](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

### Java API를 사용하여 PDF 문서에 디지털 서명 {#digitally-sign-pdf-documents-using-the-java-api}

서명 API(Java)를 사용하여 PDF 문서에 디지털 서명합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-signatures-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. 서명 클라이언트 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하고 `SignatureServiceClient` 개체를 전달하여 `ServiceClientFactory` 개체를 만듭니다.

1. 서명할 PDF 문서 가져오기

   * 생성자를 사용하고 PDF 문서의 위치를 지정하는 문자열 값을 전달하여 디지털 서명할 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만듭니다.
   * 생성자를 사용하고 `com.adobe.idp.Document` 개체를 전달하여 `java.io.FileInputStream` 개체를 만듭니다.

1. PDF 문서에 서명

   `SignatureServiceClient` 개체의 `sign` 메서드를 호출하고 다음 값을 전달하여 PDF 문서에 서명합니다.

   * 서명할 PDF 문서를 나타내는 `com.adobe.idp.Document` 개체입니다.
   * 디지털 서명을 포함할 서명 필드의 이름을 나타내는 문자열 값입니다.
   * PDF 문서에 디지털 서명하는 데 사용되는 자격 증명을 나타내는 `Credential` 개체입니다. `Credential` 개체의 정적 `Credential` 메서드를 호출하고 보안 자격 증명에 해당하는 별칭 값을 지정하는 문자열 값을 전달하여 `getInstance` 개체를 만듭니다.
   * PDF 문서를 요약하는 데 사용할 해시 알고리즘을 나타내는 정적 데이터 멤버를 지정하는 `HashAlgorithm` 개체입니다. 예를 들어 SHA1 알고리즘을 사용하도록 `HashAlgorithm.SHA1`을(를) 지정할 수 있습니다.
   * PDF 문서가 디지털 서명된 이유를 나타내는 문자열 값입니다.
   * 서명자의 연락처 정보를 나타내는 문자열 값입니다.
   * 디지털 서명의 모양을 제어하는 `PDFSignatureAppearanceOptions` 개체입니다. 예를 들어 이 개체를 사용하여 디지털 서명에 사용자 지정 로고를 추가할 수 있습니다.
   * 서명자의 인증서에 대해 해지 검사를 수행할지 여부를 지정하는 `java.lang.Boolean` 개체입니다.
   * OCSP(온라인 인증서 상태 프로토콜) 지원에 대한 기본 설정을 저장하는 `OCSPOptionSpec` 개체입니다. 해지 검사가 수행되지 않으면 이 매개 변수가 사용되지 않으므로 `null`을(를) 지정할 수 있습니다.
   * CRL(인증서 해지 목록) 기본 설정을 저장하는 `CRLPreferences` 개체입니다. 해지 검사가 수행되지 않으면 이 매개 변수가 사용되지 않으므로 `null`을(를) 지정할 수 있습니다.
   * TSP(타임스탬프 공급자) 지원에 대한 환경 설정을 저장하는 `TSPPreferences` 개체입니다. 이 매개 변수는 선택 사항이며 `null`일 수 있습니다. 자세한 내용은 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)를 참조하십시오.

   `sign` 메서드는 서명된 PDF 문서를 나타내는 `com.adobe.idp.Document` 개체를 반환합니다.

1. 서명된 PDF 문서 저장

   * `java.io.File` 개체를 만들고 파일 확장명이 .pdf인지 확인하십시오.
   * `com.adobe.idp.Document` 개체의 `copyToFile` 메서드를 호출하고 `java.io.File`을(를) 전달하여 `Document` 개체의 내용을 파일에 복사합니다. `com.adobe.idp.Document` 메서드에서 반환된 `sign` 개체를 사용하는지 확인하십시오.

**추가 참조**

[PDF 문서에 디지털 서명](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[빠른 시작(SOAP 모드): Java API를 사용하여 PDF 문서에 디지털 서명](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 PDF 문서에 디지털 서명 {#digitally-signing-pdf-documents-using-the-web-service-api}

서명 API(웹 서비스)를 사용하여 PDF 문서에 디지털 서명하려면 다음을 수행하십시오.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. WSDL 정의 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`을(를) 사용하는지 확인하십시오.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꾸십시오.

1. 서명 클라이언트 만들기

   * 기본 생성자를 사용하여 `SignatureServiceClient` 개체를 만듭니다.
   * `SignatureServiceClient.Endpoint.Address` 생성자를 사용하여 `System.ServiceModel.EndpointAddress` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/SignatureService?WSDL`). `lc_version` 특성은 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * `System.ServiceModel.BasicHttpBinding` 필드의 값을 가져와 `SignatureServiceClient.Endpoint.Binding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`(으)로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * `SignatureServiceClient.ClientCredentials.UserName.UserName` 필드에 AEM Forms 사용자 이름을 지정하십시오.
      * 필드 `SignatureServiceClient.ClientCredentials.UserName.Password`에 해당 암호 값을 지정하십시오.
      * 상수 값 `HttpClientCredentialType.Basic`을(를) 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.
      * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을(를) 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. 서명할 PDF 문서 가져오기

   * 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 서명된 PDF 문서를 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하고 서명할 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * 해당 `BLOB` 속성을 바이트 배열의 내용으로 할당하여 `MTOM` 개체를 채웁니다.

1. PDF 문서에 서명

   `SignatureServiceClient` 개체의 `sign` 메서드를 호출하고 다음 값을 전달하여 PDF 문서에 서명합니다.

   * 서명할 PDF 문서를 나타내는 `BLOB` 개체입니다.
   * 디지털 서명을 포함할 서명 필드의 이름을 나타내는 문자열 값입니다.
   * PDF 문서에 디지털 서명하는 데 사용되는 자격 증명을 나타내는 `Credential` 개체입니다. 생성자를 사용하여 `Credential` 개체를 만들고 `Credential` 개체의 `alias` 속성에 값을 할당하여 별칭을 지정합니다.
   * PDF 문서를 요약하는 데 사용할 해시 알고리즘을 나타내는 정적 데이터 멤버를 지정하는 `HashAlgorithm` 개체입니다. 예를 들어 SHA1 알고리즘을 사용하도록 `HashAlgorithm.SHA1`을(를) 지정할 수 있습니다.
   * 해시 알고리즘의 사용 여부를 지정하는 부울 값입니다.
   * PDF 문서가 디지털 서명된 이유를 나타내는 문자열 값입니다.
   * 서명자의 위치를 나타내는 문자열 값입니다.
   * 서명자의 연락처 정보를 나타내는 문자열 값입니다.
   * 디지털 서명의 모양을 제어하는 `PDFSignatureAppearanceOptions` 개체입니다. 예를 들어 이 개체를 사용하여 디지털 서명에 사용자 지정 로고를 추가할 수 있습니다.
   * 서명자의 인증서에 대해 해지 검사를 수행할지 여부를 지정하는 `System.Boolean` 개체입니다. 이 해지 확인이 완료되면 서명에 포함됩니다. 기본값은 `false`입니다.
   * OCSP(온라인 인증서 상태 프로토콜) 지원에 대한 기본 설정을 저장하는 `OCSPOptionSpec` 개체입니다. 해지 검사가 수행되지 않으면 이 매개 변수가 사용되지 않으므로 `null`을(를) 지정할 수 있습니다. 이 개체에 대한 자세한 내용은 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)를 참조하십시오.
   * CRL(인증서 해지 목록) 기본 설정을 저장하는 `CRLPreferences` 개체입니다. 해지 검사가 수행되지 않으면 이 매개 변수가 사용되지 않으므로 `null`을(를) 지정할 수 있습니다.
   * TSP(타임스탬프 공급자) 지원에 대한 환경 설정을 저장하는 `TSPPreferences` 개체입니다. 이 매개 변수는 선택 사항이며 `null`일 수 있습니다.

   `sign` 메서드는 서명된 PDF 문서를 나타내는 `BLOB` 개체를 반환합니다.

1. 서명된 PDF 문서 저장

   * 해당 생성자를 호출하여 `System.IO.FileStream` 개체를 만듭니다. 서명된 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * `BLOB` 메서드에서 반환된 `sign` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `BLOB` 개체의 `MTOM` 데이터 멤버의 값을 가져와서 바이트 배열을 채웁니다.
   * 해당 생성자를 호출하고 `System.IO.BinaryWriter` 개체를 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.BinaryWriter` 개체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 PDF 파일에 씁니다.

**추가 참조**

[PDF 문서에 디지털 서명](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 대화형 Forms 디지털 서명 {#digitally-signing-interactive-forms}

Forms 서비스에서 만드는 대화형 양식에 서명할 수 있습니다. 예를 들어 다음 워크플로를 고려하십시오.

* Designer을 사용하여 만든 XFA 기반 PDF 양식과 Forms 서비스를 사용하여 양식 데이터를 XML 문서에 병합합니다. Forms 서버는 대화형 양식을 렌더링합니다.
* 서명 서비스 API를 사용하여 대화형 양식에 서명합니다.

그 결과 디지털 서명된 대화형 PDF 양식이 만들어집니다. XFA 양식을 기반으로 하는 PDF 양식에 서명할 때 PDF 파일을 Adobe 정적 PDF 양식으로 저장해야 합니다. Adobe Dynamic PDF 양식으로 저장된 PDF 양식에 서명하려고 하면 예외가 발생합니다. Forms 서비스에서 반환된 양식에 서명하고 있으므로 양식에 서명 필드가 포함되어 있는지 확인하십시오.

>[!NOTE]
>
>대화형 양식에 디지털 서명하려면 먼저 인증서를 AEM Forms에 추가해야 합니다. 인증서는 관리 콘솔을 사용하거나 Trust Manager API를 프로그래밍 방식으로 사용하여 추가됩니다. [Trust Manager API를 사용하여 자격 증명 가져오기](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)를 참조하십시오.

Forms 서비스 API를 사용하는 경우 `GenerateServerAppearance` 런타임 옵션을 `true`(으)로 설정합니다. 이 런타임 옵션을 사용하면 Acrobat 또는 Adobe Reader에서 열 때 서버에서 생성된 양식의 모양이 그대로 유지됩니다. Forms API를 사용하여 서명할 대화형 양식을 생성할 때 이 런타임 옵션을 설정하는 것이 좋습니다.

>[!NOTE]
>
>디지털 서명 대화형 Forms을 읽기 전에 PDF 문서 서명에 익숙해지는 것이 좋습니다. ([PDF 문서에 디지털 서명하기](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)를 참조하십시오.)

### 단계 요약 {#summary_of_steps-4}

Forms 서비스가 반환하는 대화형 양식에 디지털 서명하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. Forms 및 서명 클라이언트를 만듭니다.
1. Forms 서비스를 사용하여 대화형 양식을 가져옵니다.
1. 대화형 양식에 서명합니다.
1. 서명된 PDF 문서를 PDF 파일로 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-forms-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필수)

이러한 JAR 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)을 참조하십시오.

**Forms 및 서명 클라이언트 만들기**

이 워크플로우는 Forms 및 서명 서비스를 모두 호출하므로 Forms 서비스 클라이언트와 서명 서비스 클라이언트를 모두 만듭니다.

**Forms 서비스를 사용하여 대화형 양식을 가져옵니다**

Forms 서비스를 사용하여 서명할 대화형 PDF 양식을 가져올 수 있습니다. AEM Forms부터는 렌더링할 양식이 포함된 Forms 서비스에 `com.adobe.idp.Document` 개체를 전달할 수 있습니다. 이 메서드의 이름은 `renderPDFForm2`입니다. 이 메서드는 서명할 양식을 포함하는 `com.adobe.idp.Document` 개체를 반환합니다. 이 `com.adobe.idp.Document` 인스턴스를 서명 서비스에 전달할 수 있습니다.

마찬가지로 웹 서비스를 사용하는 경우 Forms 서비스가 반환하는 `BLOB` 인스턴스를 서명 서비스로 전달할 수 있습니다.

>[!NOTE]
>
>디지털 서명 대화형 Forms 섹션과 연결된 빠른 시작은 `renderPDFForm2` 메서드를 호출합니다.

**대화형 양식에 서명**

PDF 문서에 서명할 때 서명 서비스에서 사용하는 런타임 옵션을 설정할 수 있습니다. 다음 옵션을 설정할 수 있습니다.

* 모양 옵션
* 해지 확인
* 타임스탬프 값

`PDFSignatureAppearanceOptionSpec` 개체를 사용하여 모양 옵션을 설정합니다. 예를들어, `PDFSignatureAppearanceOptionSpec` 개체의 `setShowDate` 메서드를 호출하고 `true`을(를) 전달하여 서명 내에 날짜를 표시할 수 있습니다.

**서명된 PDF 문서 저장**

서명 서비스에서 PDF 문서에 디지털 서명을 한 후 이 문서를 PDF 파일로 저장할 수 있습니다. PDF 파일은 Acrobat 또는 Adobe Reader에서 열 수 있습니다.

**추가 참조**

[Java API를 사용하여 대화형 양식에 디지털 서명](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-java-api)

[웹 서비스 API를 사용하여 대화형 양식에 디지털 서명](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF 문서에 디지털 서명](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[대화형 PDF 양식 렌더링](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)

### Java API를 사용하여 대화형 양식에 디지털 서명 {#digitally-sign-an-interactive-form-using-the-java-api}

Forms 및 서명 API(Java)를 사용하여 대화형 양식에 디지털 서명합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-signatures-client.jar 및 adobe-forms-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. Forms 및 Signatures 클라이언트 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하고 `SignatureServiceClient` 개체를 전달하여 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하고 `FormsServiceClient` 개체를 전달하여 `ServiceClientFactory` 개체를 만듭니다.

1. Forms 서비스를 사용하여 대화형 양식 얻기

   * 생성자를 사용하여 Forms 서비스에 전달할 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만듭니다. PDF 문서의 위치를 지정하는 문자열 값을 전달합니다.
   * 생성자를 사용하고 `com.adobe.idp.Document` 개체를 전달하여 `java.io.FileInputStream` 개체를 만듭니다.
   * 생성자를 사용하여 Forms 서비스에 전달할 양식 데이터가 포함된 XML 문서를 나타내는 `java.io.FileInputStream` 개체를 만듭니다. XML 파일의 위치를 지정하는 문자열 값을 전달합니다.
   * 생성자를 사용하고 `com.adobe.idp.Document` 개체를 전달하여 `java.io.FileInputStream` 개체를 만듭니다.
   * 런타임 옵션을 설정하는 데 사용되는 `PDFFormRenderSpec` 개체를 만듭니다. `PDFFormRenderSpec` 개체의 `setGenerateServerAppearance` 메서드를 호출하고 `true`을(를) 전달합니다.
   * `FormsServiceClient` 개체의 `renderPDFForm2` 메서드를 호출하고 다음 값을 전달하십시오.

      * 렌더링할 PDF 양식을 포함하는 `com.adobe.idp.Document` 개체입니다.
      * 양식과 병합할 데이터가 포함된 `com.adobe.idp.Document` 개체입니다.
      * 런타임 옵션을 저장하는 `PDFFormRenderSpec` 개체입니다.
      * Forms 서비스에 필요한 URI 값을 포함하는 `URLSpec` 개체입니다. 이 매개 변수 값에 `null`을(를) 지정할 수 있습니다.
      * 첨부 파일을 저장하는 `java.util.HashMap` 개체입니다. 선택적 매개 변수이며, 양식에 파일을 첨부하지 않으려면 `null`을(를) 지정할 수 있습니다.

     `renderPDFForm2` 메서드가 양식 데이터 스트림을 포함하는 `FormsResult` 개체를 반환합니다

   * `FormsResult` 개체의 `getOutputContent` 메서드를 호출하여 PDF 양식을 검색하십시오. 이 메서드는 대화형 양식을 나타내는 `com.adobe.idp.Document` 개체를 반환합니다.

1. 대화형 양식에 서명

   `SignatureServiceClient` 개체의 `sign` 메서드를 호출하고 다음 값을 전달하여 PDF 문서에 서명합니다.

   * 서명할 PDF 문서를 나타내는 `com.adobe.idp.Document` 개체입니다. 이 개체가 Forms 서비스에서 가져온 `com.adobe.idp.Document` 개체인지 확인하십시오.
   * 서명된 서명 필드의 이름을 나타내는 문자열 값입니다.
   * PDF 문서에 디지털 서명하는 데 사용되는 자격 증명을 나타내는 `Credential` 개체입니다. `Credential` 개체의 정적 `Credential` 메서드를 호출하여 `getInstance` 개체를 만듭니다. 보안 자격 증명에 해당하는 별칭 값을 지정하는 문자열 값을 전달합니다.
   * PDF 문서를 요약하는 데 사용할 해시 알고리즘을 나타내는 정적 데이터 멤버를 지정하는 `HashAlgorithm` 개체입니다. 예를 들어 SHA1 알고리즘을 사용하도록 `HashAlgorithm.SHA1`을(를) 지정할 수 있습니다.
   * PDF 문서가 디지털 서명된 이유를 나타내는 문자열 값입니다.
   * 서명자의 연락처 정보를 나타내는 문자열 값입니다.
   * 디지털 서명의 모양을 제어하는 `PDFSignatureAppearanceOptions` 개체입니다. 예를 들어 이 개체를 사용하여 디지털 서명에 사용자 지정 로고를 추가할 수 있습니다.
   * 서명자의 인증서에 대해 해지 검사를 수행할지 여부를 지정하는 `java.lang.Boolean` 개체입니다.
   * OCSP(온라인 인증서 상태 프로토콜) 지원에 대한 기본 설정을 저장하는 `OCSPPreferences` 개체입니다. 해지 검사가 수행되지 않으면 이 매개 변수가 사용되지 않으므로 `null`을(를) 지정할 수 있습니다.
   * CRL(인증서 해지 목록) 기본 설정을 저장하는 `CRLPreferences` 개체입니다. 해지 검사가 수행되지 않으면 이 매개 변수가 사용되지 않으므로 `null`을(를) 지정할 수 있습니다.
   * TSP(타임스탬프 공급자) 지원에 대한 환경 설정을 저장하는 `TSPPreferences` 개체입니다. 이 매개 변수는 선택 사항이며 `null`일 수 있습니다.

   `sign` 메서드는 서명된 PDF 문서를 나타내는 `com.adobe.idp.Document` 개체를 반환합니다.

1. 서명된 PDF 문서 저장

   * `java.io.File` 개체를 만들고 파일 이름 확장명이 .pdf인지 확인하십시오.
   * `com.adobe.idp.Document` 개체의 `copyToFile` 메서드를 호출하고 `java.io.File`을(를) 전달하여 `Document` 개체의 내용을 파일에 복사합니다. `com.adobe.idp.Document` 메서드가 반환한 `sign` 개체를 사용하는지 확인하십시오.

**추가 참조**

[대화형 Forms 디지털 서명](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[빠른 시작(SOAP 모드): Java API를 사용하여 PDF 문서에 디지털 서명](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 대화형 양식에 디지털 서명 {#digitally-sign-an-interactive-form-using-the-web-service-api}

Forms 및 서명 API(웹 서비스)를 사용하여 대화형 양식에 디지털 서명합니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 이 클라이언트 애플리케이션은 두 개의 AEM Forms 서비스를 호출하므로 두 개의 서비스 참조를 생성합니다. 서명 서비스와 연결된 서비스 참조에 대해 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1` WSDL 정의를 사용합니다.

   Forms 서비스와 연결된 서비스 참조에 대해 `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1` WSDL 정의를 사용합니다.

   `BLOB` 데이터 형식은 두 서비스 참조에 모두 공통적이므로 사용할 때 `BLOB` 데이터 형식을 완전히 정규화합니다. 해당 웹 서비스 빠른 시작에서 모든 `BLOB` 인스턴스가 정규화되었습니다.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꾸십시오.

1. Forms 및 Signatures 클라이언트 만들기

   * 기본 생성자를 사용하여 `SignatureServiceClient` 개체를 만듭니다.
   * `SignatureServiceClient.Endpoint.Address` 생성자를 사용하여 `System.ServiceModel.EndpointAddress` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/SignatureService?WSDL`). `lc_version` 특성은 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * `System.ServiceModel.BasicHttpBinding` 필드의 값을 가져와 `SignatureServiceClient.Endpoint.Binding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`(으)로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * `SignatureServiceClient.ClientCredentials.UserName.UserName` 필드에 AEM Forms 사용자 이름을 지정하십시오.
      * 필드 `SignatureServiceClient.ClientCredentials.UserName.Password`에 해당 암호 값을 지정하십시오.
      * 상수 값 `HttpClientCredentialType.Basic`을(를) 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.

   * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을(를) 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

   >[!NOTE]
   >
   >Forms 서비스 클라이언트에 대해 이 단계를 반복합니다.

1. Forms 서비스를 사용하여 대화형 양식 얻기

   * 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 서명된 PDF 문서를 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하고 서명할 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * 해당 `BLOB` 속성을 바이트 배열의 내용으로 할당하여 `MTOM` 개체를 채웁니다.
   * 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 양식 데이터를 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하고 양식 데이터가 포함된 XML 파일의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * 해당 `BLOB` 속성을 바이트 배열의 내용으로 할당하여 `MTOM` 개체를 채웁니다.
   * 런타임 옵션을 설정하는 데 사용되는 `PDFFormRenderSpec` 개체를 만듭니다. `true` 개체의 `PDFFormRenderSpec` 필드에 값 `generateServerAppearance`을(를) 할당합니다.
   * `FormsServiceClient` 개체의 `renderPDFForm2` 메서드를 호출하고 다음 값을 전달하십시오.

      * 렌더링할 PDF 양식을 포함하는 `BLOB` 개체입니다.
      * 양식과 병합할 데이터가 포함된 `BLOB` 개체입니다.
      * 런타임 옵션을 저장하는 `PDFFormRenderSpec` 개체입니다.
      * Forms 서비스에 필요한 URI 값을 포함하는 `URLSpec` 개체입니다. 이 매개 변수 값에 `null`을(를) 지정할 수 있습니다.
      * 첨부 파일을 저장하는 `java.util.HashMap` 개체입니다. 선택적 매개 변수이며, 양식에 파일을 첨부하지 않으려면 `null`을(를) 지정할 수 있습니다.
      * 양식의 페이지 수를 저장하는 데 사용되는 긴 출력 매개 변수입니다.
      * 로케일 값에 사용되는 문자열 출력 매개 변수입니다.
      * 대화형 양식을 저장하는 데 사용되는 출력 매개 변수인 `FormResult` 값입니다.

   * `FormsResult` 개체의 `outputContent` 필드를 호출하여 PDF 양식을 검색합니다. 이 필드에는 대화형 양식을 나타내는 `BLOB` 개체가 저장됩니다.

1. 대화형 양식에 서명

   `SignatureServiceClient` 개체의 `sign` 메서드를 호출하고 다음 값을 전달하여 PDF 문서에 서명합니다.

   * 서명할 PDF 문서를 나타내는 `BLOB` 개체입니다. Forms 서비스에서 반환된 `BLOB` 인스턴스를 사용합니다.
   * 서명된 서명 필드의 이름을 나타내는 문자열 값입니다.
   * PDF 문서에 디지털 서명하는 데 사용되는 자격 증명을 나타내는 `Credential` 개체입니다. 생성자를 사용하여 `Credential` 개체를 만들고 `Credential` 개체의 `alias` 속성에 값을 할당하여 별칭을 지정합니다.
   * PDF 문서를 요약하는 데 사용할 해시 알고리즘을 나타내는 정적 데이터 멤버를 지정하는 `HashAlgorithm` 개체입니다. 예를 들어 SHA1 알고리즘을 사용하도록 `HashAlgorithm.SHA1`을(를) 지정할 수 있습니다.
   * 해시 알고리즘의 사용 여부를 지정하는 부울 값입니다.
   * PDF 문서가 디지털 서명된 이유를 나타내는 문자열 값입니다.
   * 서명자의 위치를 나타내는 문자열 값입니다.
   * 서명자의 연락처 정보를 나타내는 문자열 값입니다.
   * 디지털 서명의 모양을 제어하는 `PDFSignatureAppearanceOptions` 개체입니다. 예를 들어 이 개체를 사용하여 디지털 서명에 사용자 지정 로고를 추가할 수 있습니다.
   * 서명자의 인증서에 대해 해지 검사를 수행할지 여부를 지정하는 `System.Boolean` 개체입니다. 이 해지 확인이 완료되면 서명에 포함됩니다. 기본값은 `false`입니다.
   * OCSP(온라인 인증서 상태 프로토콜) 지원에 대한 기본 설정을 저장하는 `OCSPPreferences` 개체입니다. 해지 검사가 수행되지 않으면 이 매개 변수가 사용되지 않으므로 `null`을(를) 지정할 수 있습니다. 이 개체에 대한 자세한 내용은 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)를 참조하십시오.
   * CRL(인증서 해지 목록) 기본 설정을 저장하는 `CRLPreferences` 개체입니다. 해지 검사가 수행되지 않으면 이 매개 변수가 사용되지 않으므로 `null`을(를) 지정할 수 있습니다.
   * TSP(타임스탬프 공급자) 지원에 대한 환경 설정을 저장하는 `TSPPreferences` 개체입니다. 이 매개 변수는 선택 사항이며 `null`일 수 있습니다.

   `sign` 메서드는 서명된 PDF 문서를 나타내는 `BLOB` 개체를 반환합니다.

1. 서명된 PDF 문서 저장

   * 해당 생성자를 호출하여 `System.IO.FileStream` 개체를 만듭니다. 서명된 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * `BLOB` 메서드에서 반환된 `sign` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `BLOB` 개체의 `MTOM` 데이터 멤버의 값을 가져와서 바이트 배열을 채웁니다.
   * 해당 생성자를 호출하고 `System.IO.BinaryWriter` 개체를 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.BinaryWriter` 개체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 PDF 파일에 씁니다.

**추가 참조**

[대화형 Forms 디지털 서명](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## PDF 문서 인증 {#certifying-pdf-documents}

인증된 서명이라는 특정 유형의 서명으로 PDF 문서를 인증하면 문서를 보호할 수 있습니다. 인증된 서명은 다음과 같은 방법으로 디지털 서명과 구별됩니다.

* 이 서명은 PDF 문서에 적용된 첫 번째 서명이어야 합니다. 즉, 인증 서명이 적용될 때에는 문서의 다른 서명 필드에 서명이 없어야 합니다. PDF 문서에는 하나의 인증된 서명만 허용됩니다. PDF 문서에 서명하고 인증하려면 서명하기 전에 해당 문서를 인증해야 합니다. PDF 문서를 인증하면 추가 서명 필드에 디지털 서명할 수 있습니다.
* 문서의 작성자 또는 작성자는 인증된 서명을 무효화하지 않고 문서를 특정 방식으로 수정할 수 있음을 지정할 수 있다. 예를 들어, 문서에서는 양식 작성 또는 댓글 달기를 허용할 수 있습니다. 작성자가 특정 수정이 허용되지 않는다고 지정하면 Acrobat에서 사용자가 이러한 방식으로 문서를 수정할 수 없도록 제한합니다. 다른 애플리케이션 사용과 같이 이러한 수정이 이루어진 경우, 인증된 서명이 유효하지 않으며 사용자가 문서를 열 때 Acrobat에서 경고가 표시됩니다. 인증되지 않은 서명을 사용하면 수정할 수 없으며 일반 편집 작업으로 인해 원래 서명이 무효화되지 않습니다.
* 서명 시 문서의 내용을 모호하게 하거나 오해의 소지가 있는 특정 유형의 내용이 있는지 문서를 스캔합니다. 예를 들어 주석은 인증된 내용을 이해하는 데 중요한 페이지의 일부 텍스트를 가릴 수 있습니다. 이러한 내용에 대한 설명(법적 증명)을 제공할 수 있다.

서명 서비스 Java API 또는 서명 웹 서비스 API를 사용하여 PDF 문서를 프로그래밍 방식으로 인증할 수 있습니다. PDF 문서를 인증할 때 자격 증명 서비스에 있는 보안 자격 증명을 참조해야 합니다. 보안 자격 증명에 대한 자세한 내용은 응용 프로그램 서버에 대한 *AEM Forms 설치 및 배포* 안내서를 참조하십시오.

>[!NOTE]
>
>동일한 PDF 문서를 인증하고 서명할 때 인증 서명을 신뢰할 수 없는 경우 Acrobat 또는 Adobe Reader에서 PDF 문서를 열면 첫 번째 서명 서명 옆에 노란색 삼각형이 나타납니다. 이러한 상황을 방지하려면 인증 서명을 신뢰해야 합니다.

>[!NOTE]
>
>nShield nShield HSM 자격 증명을 사용하여 PDF 문서에 서명하거나 인증하는 경우 AEM Forms이 배포된 J2EE 애플리케이션 서버를 다시 시작할 때까지 새 자격 증명을 사용할 수 없습니다. 그러나 구성 값을 설정하면 J2EE 응용 프로그램 서버를 다시 시작하지 않고도 서명 또는 인증 작업이 작동합니다.

/opt/nfast/cknfastrc(또는 c:\nfast\cknfastrc)에 있는 cknfastrc 파일에 다음 구성 값을 추가할 수 있습니다.

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

이 구성 값을 cknfastrc 파일에 추가한 후에는 J2EE 애플리케이션 서버를 다시 시작하지 않고도 새 자격 증명을 사용할 수 있습니다.

>[!NOTE]
>
>서명 서비스 및 문서 인증에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary_of_steps-5}

PDF 문서를 인증하려면 다음 작업을 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. 서명 클라이언트를 만듭니다.
1. PDF 문서를 인증합니다.
1. PDF 문서를 인증합니다.
1. 인증된 PDF 문서를 PDF 파일로 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필수)

이러한 JAR 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)을 참조하십시오.

**서명 클라이언트 만들기**

서명 작업을 프로그래밍 방식으로 수행하려면 먼저 서명 클라이언트를 만들어야 합니다.

**인증할 PDF 문서 가져오기**

PDF 문서를 인증하려면 서명 필드가 포함된 PDF 문서를 받아야 합니다. PDF 문서에 서명 필드가 없으면 인증을 받을 수 없습니다. 서명 필드는 Designer을 사용하거나 프로그래밍 방식으로 추가할 수 있습니다. 프로그래밍 방식으로 서명 필드를 추가하는 방법에 대한 자세한 내용은 [서명 필드 추가](digitally-signing-certifying-documents.md#adding-signature-fields)를 참조하십시오.

**PDF 문서 인증**

PDF 문서를 성공적으로 인증하려면 서명 서비스에서 PDF 문서를 인증하는 데 사용하는 다음 입력 값이 필요합니다.

* **PDF 문서**: 서명 필드가 포함된 PDF 문서입니다. 이 필드는 인증된 서명의 그래픽 표현이 포함된 양식 필드입니다. PDF 문서를 인증하려면 먼저 서명 필드가 포함되어야 합니다. 서명 필드는 Designer을 사용하거나 프로그래밍 방식으로 추가할 수 있습니다. ([서명 필드 추가](digitally-signing-certifying-documents.md#adding-signature-fields)를 참조하십시오.)
* **서명 필드 이름**: 인증된 서명 필드의 정규화된 이름입니다. 다음 값은 예제입니다. `form1[0].#subform[1].SignatureField3[3]` XFA 양식 필드를 사용하는 경우 서명 필드의 일부 이름을 사용할 수도 있습니다. `SignatureField3[3]`. 필드 이름에 대해 null 값이 전달되면 보이지 않는 서명 필드가 동적으로 생성되고 인증됩니다.
* **보안 자격 증명**: PDF 문서를 인증하는 데 사용되는 자격 증명입니다. 이 보안 자격 증명에는 암호 및 별칭이 포함되어 있으며, 이 별칭은 자격 증명 서비스 내에 있는 자격 증명에 나타나는 별칭과 일치해야 합니다. 별칭은 PKCS#12 파일(.pfx 확장명 포함) 또는 HSM(하드웨어 보안 모듈)에 있을 수 있는 실제 자격 증명에 대한 참조입니다.
* **해시 알고리즘**: PDF 문서를 요약하는 데 사용할 해시 알고리즘입니다.
* **서명 이유**: 다른 사용자가 PDF 문서가 인증된 이유를 알 수 있도록 Acrobat 또는 Adobe Reader에 표시되는 값입니다.
* **서명자의 위치**: 자격 증명으로 지정된 서명자의 위치입니다.
* **연락처 정보**: 서명자의 주소 및 전화 번호와 같은 연락처 정보.
* **권한 정보**: 인증 서명이 올바르지 않게 되지 않고 최종 사용자가 문서에서 수행할 수 있는 작업을 제어하는 권한입니다. 예를 들어 PDF 문서를 변경하면 인증된 서명이 무효화되도록 권한을 설정할 수 있습니다.
* **법적 설명**: 문서가 인증되면 문서의 내용을 모호하게 하거나 오해의 소지가 있는 특정 유형의 내용을 자동으로 검사합니다. 예를 들어 주석은 인증된 내용을 이해하는 데 중요한 페이지의 일부 텍스트를 가릴 수 있습니다. 검색 프로세스는 이러한 유형의 콘텐츠에 대한 경고를 생성합니다. 이 값은 생성된 경고일 수 있는 콘텐츠에 대한 추가 설명을 제공합니다.
* **모양 옵션**: 인증된 서명의 모양을 제어하는 옵션입니다. 예를 들어 인증된 서명은 날짜 정보를 표시할 수 있습니다.
* **해지 확인**: 이 값은 서명자의 인증서에 대해 해지 확인이 수행되는지 여부를 지정합니다. `false`의 기본 설정은 해지 검사가 수행되지 않았음을 의미합니다.
* **OCSP 설정**: OCSP(온라인 인증서 상태 프로토콜) 지원에 대한 설정으로, PDF 문서를 인증하는 데 사용되는 자격 증명의 상태에 대한 정보를 제공합니다. 예를 들어 PDF 문서에 로그온하는 데 사용 중인 자격 증명에 대한 정보를 제공하는 서버의 URL을 지정할 수 있습니다.
* **CRL 설정**: 해지 검사가 완료된 경우 CRL(인증서 해지 목록) 기본 설정. 예를 들어 자격 증명이 취소되었는지 여부를 항상 확인하도록 지정할 수 있습니다.
* **타임스탬프**: 인증된 서명에 적용되는 타임스탬프 정보를 정의하는 설정입니다. 타임스탬프는 특정 시간 전에 특정 데이터가 설정되었음을 나타냅니다. 이러한 지식은 서명자와 검증자 사이에 신뢰 관계를 구축하는 데 도움이 된다.

**인증된 PDF 문서를 PDF 파일로 저장**

서명 서비스에서 PDF 문서를 인증하면 사용자가 Acrobat 또는 Adobe Reader에서 열 수 있도록 문서를 PDF 파일로 저장할 수 있습니다.

**추가 참조**

[Java API를 사용하여 PDF 문서 인증](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-java-api)

[웹 서비스 API를 사용하여 PDF 문서 인증](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[서명 필드 추가](digitally-signing-certifying-documents.md#adding-signature-fields)

### Java API를 사용하여 PDF 문서 인증 {#certify-pdf-documents-using-the-java-api}

서명 API(Java)를 사용하여 PDF 문서 인증:

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-signatures-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. 서명 클라이언트 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하고 `SignatureServiceClient` 개체를 전달하여 `ServiceClientFactory` 개체를 만듭니다.

1. 인증할 PDF 문서 가져오기

   * 생성자를 사용하고 PDF 문서의 위치를 지정하는 문자열 값을 전달하여 인증할 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만듭니다.
   * 생성자를 사용하고 `com.adobe.idp.Document` 개체를 전달하여 `java.io.FileInputStream` 개체를 만듭니다.

1. PDF 문서 인증

   `SignatureServiceClient` 개체의 `certify` 메서드를 호출하고 다음 값을 전달하여 PDF 문서를 인증합니다.

   * 인증할 PDF 문서를 나타내는 `com.adobe.idp.Document` 개체입니다.
   * 서명을 포함할 서명 필드의 이름을 나타내는 문자열 값입니다.
   * PDF 문서를 인증하는 데 사용되는 자격 증명을 나타내는 `Credential` 개체입니다. `Credential` 개체의 정적 `Credential` 메서드를 호출하고 보안 자격 증명에 해당하는 별칭 값을 지정하는 문자열 값을 전달하여 `getInstance` 개체를 만듭니다.
   * PDF 문서를 요약하는 데 사용되는 해시 알고리즘을 나타내는 정적 데이터 멤버를 지정하는 `HashAlgorithm` 개체입니다. 예를 들어 SHA1 알고리즘을 사용하도록 `HashAlgorithm.SHA1`을(를) 지정할 수 있습니다.
   * PDF 문서가 인증된 이유를 나타내는 문자열 값입니다.
   * 서명자의 연락처 정보를 나타내는 문자열 값입니다.
   * 서명을 무효화하는 PDF 문서에서 수행할 수 있는 작업을 지정하는 `MDPPermissions` 개체입니다.
   * 인증된 서명의 모양을 제어하는 `PDFSignatureAppearanceOptions` 개체입니다. 필요한 경우 `setShowDate`과(와) 같은 메서드를 호출하여 시그니처의 모양을 수정합니다.
   * 서명을 무효화하는 작업에 대한 설명을 제공하는 문자열 값입니다.
   * 서명자의 인증서에 대해 해지 검사를 수행할지 여부를 지정하는 `java.lang.Boolean` 개체입니다. 이 해지 확인이 완료되면 서명에 포함됩니다. 기본값은 `false`입니다.
   * 인증 중인 서명 필드의 잠금 여부를 지정하는 `java.lang.Boolean` 개체입니다. 필드가 잠겨 있으면 서명 필드가 읽기 전용으로 표시되어 해당 속성을 수정할 수 없으며 필요한 권한이 없는 사람은 지울 수 없습니다. 기본값은 `false`입니다.
   * OCSP(온라인 인증서 상태 프로토콜) 지원에 대한 기본 설정을 저장하는 `OCSPPreferences` 개체입니다. 해지 검사가 수행되지 않으면 이 매개 변수가 사용되지 않으므로 `null`을(를) 지정할 수 있습니다. 이 개체에 대한 자세한 내용은 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)를 참조하십시오.
   * CRL(인증서 해지 목록) 기본 설정을 저장하는 `CRLPreferences` 개체입니다. 해지 검사가 수행되지 않으면 이 매개 변수가 사용되지 않으므로 `null`을(를) 지정할 수 있습니다.
   * TSP(타임스탬프 공급자) 지원에 대한 환경 설정을 저장하는 `TSPPreferences` 개체입니다. 예를 들어 `TSPPreferences` 개체를 만든 후 `TSPPreferences` 개체의 `setTspServerURL` 메서드를 호출하여 TSP 서버의 URL을 설정할 수 있습니다. 이 매개 변수는 선택 사항이며 `null`일 수 있습니다. 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

   `certify` 메서드가 인증된 PDF 문서를 나타내는 `com.adobe.idp.Document` 개체를 반환합니다.

1. 인증된 PDF 문서를 PDF 파일로 저장

   * `java.io.File` 개체를 만들고 파일 확장명이 .pdf인지 확인하십시오.
   * `com.adobe.idp.Document` 개체의 `copyToFile` 메서드를 호출하여 `com.adobe.idp.Document` 개체의 내용을 파일에 복사합니다.

**추가 참조**

[PDF 문서 인증](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[빠른 시작(SOAP 모드): Java API를 사용하여 PDF 문서 인증](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-certifying-a-pdf-document-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 PDF 문서 인증 {#certify-pdf-documents-using-the-web-service-api}

서명 API(웹 서비스)를 사용하여 PDF 문서 인증:

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. WSDL 정의 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`을(를) 사용하는지 확인하십시오.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꾸십시오.

1. 서명 클라이언트 만들기

   * 기본 생성자를 사용하여 `SignatureServiceClient` 개체를 만듭니다.
   * `SignatureServiceClient.Endpoint.Address` 생성자를 사용하여 `System.ServiceModel.EndpointAddress` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/SignatureService?WSDL`). `lc_version` 특성은 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * `System.ServiceModel.BasicHttpBinding` 필드의 값을 가져와 `SignatureServiceClient.Endpoint.Binding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`(으)로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * `SignatureServiceClient.ClientCredentials.UserName.UserName` 필드에 AEM Forms 사용자 이름을 지정하십시오.
      * 필드 `SignatureServiceClient.ClientCredentials.UserName.Password`에 해당 암호 값을 지정하십시오.
      * 상수 값 `HttpClientCredentialType.Basic`을(를) 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.
      * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을(를) 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. 인증할 PDF 문서 가져오기

   * 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 인증된 PDF 문서를 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하고 인증할 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * `BLOB` 데이터 멤버에 바이트 배열의 내용을 할당하여 `MTOM` 개체를 채웁니다.

1. PDF 문서 인증

   `SignatureServiceClient` 개체의 `certify` 메서드를 호출하고 다음 값을 전달하여 PDF 문서를 인증합니다.

   * 인증할 PDF 문서를 나타내는 `BLOB` 개체입니다.
   * 서명을 포함할 서명 필드의 이름을 나타내는 문자열 값입니다.
   * PDF 문서를 인증하는 데 사용되는 자격 증명을 나타내는 `Credential` 개체입니다. 생성자를 사용하여 `Credential` 개체를 만들고, `Credential` 개체의 `alias` 속성에 값을 할당하여 별칭을 지정합니다.
   * PDF 문서를 요약하는 데 사용되는 해시 알고리즘을 나타내는 정적 데이터 멤버를 지정하는 `HashAlgorithm` 개체입니다. 예를 들어 SHA1 알고리즘을 사용하도록 `HashAlgorithm.SHA1`을(를) 지정할 수 있습니다.
   * 해시 알고리즘의 사용 여부를 지정하는 부울 값입니다.
   * PDF 문서가 인증된 이유를 나타내는 문자열 값입니다.
   * 서명자의 위치를 나타내는 문자열 값입니다.
   * 서명자의 연락처 정보를 나타내는 문자열 값입니다.
   * 서명을 무효화하는 PDF 문서에서 수행할 수 있는 작업을 지정하는 `MDPPermissions` 개체의 정적 데이터 멤버입니다.
   * 이전 매개 변수 값으로 전달된 `MDPPermissions` 개체를 사용할지 여부를 지정하는 부울 값입니다.
   * 서명을 무효화하는 작업을 설명하는 문자열 값입니다.
   * 인증된 서명의 모양을 제어하는 `PDFSignatureAppearanceOptions` 개체입니다. 해당 생성자를 사용하여 `PDFSignatureAppearanceOptions` 개체를 만듭니다. 해당 데이터 멤버 중 하나를 설정하여 서명의 모양을 수정할 수 있습니다.
   * 서명자의 인증서에 대해 해지 검사를 수행할지 여부를 지정하는 `System.Boolean` 개체입니다. 이 해지 확인이 완료되면 서명에 포함됩니다. 기본값은 `false`입니다.
   * 인증 중인 서명 필드의 잠금 여부를 지정하는 `System.Boolean` 개체입니다. 필드가 잠겨 있으면 서명 필드가 읽기 전용으로 표시되어 해당 속성을 수정할 수 없으며 필요한 권한이 없는 사람은 지울 수 없습니다. 기본값은 `false`입니다.
   * 서명 필드가 잠겨 있는지 여부를 지정하는 `System.Boolean` 개체입니다. 즉, 이전 매개 변수에 `true`을(를) 전달한 다음 이 매개 변수에 `true`을(를) 전달합니다.
   * OCSP(온라인 인증서 상태 프로토콜) 지원에 대한 기본 설정을 저장하는 `OCSPPreferences` 개체로, PDF 문서를 인증하는 데 사용되는 자격 증명의 상태에 대한 정보를 제공합니다. 해지 검사가 수행되지 않으면 이 매개 변수가 사용되지 않으므로 `null`을(를) 지정할 수 있습니다.
   * CRL(인증서 해지 목록) 기본 설정을 저장하는 `CRLPreferences` 개체입니다. 해지 검사가 수행되지 않으면 이 매개 변수가 사용되지 않으므로 `null`을(를) 지정할 수 있습니다.
   * TSP(타임스탬프 공급자) 지원에 대한 환경 설정을 저장하는 `TSPPreferences` 개체입니다. 예를 들어 `TSPPreferences` 개체를 만든 후 `TSPPreferences` 개체의 `tspServerURL` 데이터 멤버를 설정하여 TSP의 URL을 설정할 수 있습니다. 이 매개 변수는 선택 사항이며 `null`일 수 있습니다.

   `certify` 메서드가 인증된 PDF 문서를 나타내는 `BLOB` 개체를 반환합니다.

1. 인증된 PDF 문서를 PDF 파일로 저장

   * 해당 생성자를 호출하고 인증된 PDF 문서를 포함할 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `BLOB` 메서드에서 반환된 `certify` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `BLOB` 개체의 `binaryData` 데이터 멤버의 값을 가져와서 바이트 배열을 채웁니다.
   * 해당 생성자를 호출하고 `System.IO.BinaryWriter` 개체를 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.BinaryWriter` 개체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 PDF 파일에 씁니다.

**추가 참조**

[PDF 문서 인증](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 디지털 서명 확인 {#verifying-digital-signatures}

서명된 PDF 문서가 수정되지 않았고 디지털 서명이 유효한지 확인하기 위해 디지털 서명을 확인할 수 있습니다. 디지털 서명을 확인할 때 서명의 상태와 서명자의 신원과 같은 서명의 속성을 확인할 수 있습니다. 디지털 서명을 신뢰하기 전에 확인하는 것이 좋습니다. 디지털 서명을 확인할 때 디지털 서명이 포함된 PDF 문서를 참조하십시오.

서명자의 ID를 알 수 없다고 가정합니다. Acrobat에서 PDF 문서를 열면 다음 그림과 같이 서명자의 ID를 알 수 없다는 경고 메시지가 표시됩니다.

![vd_vd_verifysig](assets/vd_vd_verifysig.png)

마찬가지로, 디지털 서명을 프로그래밍 방식으로 확인할 때 서명자의 ID 상태를 확인할 수 있습니다. 예를 들어 이전 그림에 표시된 문서에서 디지털 서명을 확인하는 경우 서명자의 ID를 알 수 없게 됩니다.

>[!NOTE]
>
>서명 서비스 및 디지털 서명 확인에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary_of_steps-6}

디지털 서명을 확인하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. 서명 클라이언트를 만듭니다.
1. 확인할 서명이 포함된 PDF 문서를 가져옵니다.
1. PKI 런타임 옵션을 설정합니다.
1. 디지털 서명을 확인합니다.
1. 서명의 상태를 확인합니다.
1. 서명자의 ID를 확인합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필수)

이러한 JAR 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)을 참조하십시오.

**서명 클라이언트 만들기**

서명 서비스 작업을 프로그래밍 방식으로 수행하기 전에 서명 서비스 클라이언트를 만듭니다.

**확인할 서명이 포함된 PDF 문서를 가져옵니다**

PDF 문서에 디지털 서명하거나 인증하는 데 사용되는 서명을 확인하려면 서명이 포함된 PDF 문서를 가져옵니다.

**PKI 런타임 옵션 설정**

PDF 문서에서 서명을 확인할 때 서명 서비스에서 사용하는 다음 PKI 런타임 옵션을 설정합니다.

* 확인 시간
* 해지 확인
* 시간 스탬핑 값

이러한 옵션을 설정하는 과정의 일부로 확인 시간을 지정할 수 있습니다. 예를 들어 현재 시간(유효성 검사기의 컴퓨터에 있는 시간)을 선택하여 현재 시간을 사용할 수 있습니다. 다른 시간 값에 대한 자세한 내용은 `VerificationTime`AEM Forms API 참조[에서 ](https://www.adobe.com/go/learn_aemforms_javadocs_63_en) 열거 값을 참조하십시오.

유효성 검사 프로세스의 일부로 해지 검사를 수행할지 여부도 지정할 수 있습니다. 예를 들어 해지 확인을 수행하여 인증서가 해지되었는지 확인할 수 있습니다. 해지 확인 옵션에 대한 자세한 내용은 `RevocationCheckStyle`AEM Forms API 참조[의 ](https://www.adobe.com/go/learn_aemforms_javadocs_63_en) 열거 값을 참조하십시오.

인증서에 대한 해지 검사를 수행하려면 `CRLOptionSpec` 개체를 사용하여 CRL(인증서 해지 목록) 서버에 대한 URL을 지정하십시오. 그러나 CRL 서버에 대한 URL을 지정하지 않으면 서명 서비스가 인증서에서 URL을 가져옵니다.

해지 검사를 수행할 때 CRL 서버를 사용하는 대신 OCSP(온라인 인증서 상태 프로토콜) 서버를 사용할 수 있습니다. 일반적으로 CRL 서버가 아닌 OCSP 서버를 사용하는 경우 해지 확인이 더 빨리 수행됩니다. ([온라인 인증서 상태 프로토콜](https://tools.ietf.org/html/rfc2560)을 참조하세요.)

Adobe 응용 프로그램 및 서비스를 사용하여 서명 서비스에서 사용하는 CRL 및 OCSP 서버 순서를 설정할 수 있습니다. 예를 들어 OCSP 서버가 Adobe Applications and Services에서 먼저 설정된 경우 OCSP 서버를 확인하고 CRL 서버를 선택합니다.

해지 확인을 수행하지 않으면 서명 서비스에서 인증서가 해지되었는지 여부를 확인하지 않습니다. 즉, CRL 및 OCSP 서버 정보는 무시됩니다.

>[!NOTE]
>
>`CRLOptionSpec` 및 `OCSPOptionSpec` 개체를 사용하여 인증서에 지정된 URL을 재정의할 수 있습니다. 예를 들어 CRL 서버를 재정의하려면 `CRLOptionSpec` 개체의 `setLocalURI` 메서드를 호출할 수 있습니다.

타임스탬프는 서명 또는 인증된 문서가 수정된 시간을 추적하는 프로세스입니다. 문서에 서명한 후에는 아무도 수정할 수 없습니다. 타임스탬프는 서명 또는 인증된 문서의 유효성을 검사하는 데 도움이 됩니다. `TSPOptionSpec` 개체를 사용하여 타임스탬프 옵션을 설정할 수 있습니다. 예를 들어 TSP(타임스탬프 제공자) 서버의 URL을 지정할 수 있습니다.

>[!NOTE]
>
>Java 및 웹 서비스 빠른 시작에서 확인 시간은 `VerificationTime.CURRENT_TIME`(으)로 설정되고 해지 검사는 `RevocationCheckStyle.BestEffort`(으)로 설정됩니다. CRL 또는 OCSP 서버 정보를 지정하지 않았으므로 인증서에서 서버 정보를 가져옵니다.

**디지털 서명 확인**

서명을 확인하려면 서명을 포함하는 서명 필드의 정규화된 이름을 지정하십시오(예: `form1[0].#subform[1].SignatureField3[3]`). XFA 양식 필드를 사용할 때 서명 필드의 일부 이름(`SignatureField3`)을 사용할 수도 있습니다.

기본적으로 서명 서비스는 유효성 검사 시간 후 문서에 서명할 수 있는 시간을 65분으로 제한합니다. 사용자가 현재 시간에 서명을 확인하려고 할 때 서명 시간이 현재 시간보다 늦고 65분 이내인 경우 서명 서비스에서 확인 오류가 발생하지 않습니다.

>[!NOTE]
>
>서명을 확인할 때 필요한 다른 값은 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)를 참조하십시오.

**서명 상태 확인**

디지털 서명을 확인하는 과정의 일부로 서명 상태를 확인할 수 있습니다.

**서명자의 ID 확인**

다음 값 중 하나가 될 수 있는 서명자의 ID를 확인할 수 있습니다.

* **알 수 없음**: 서명자 확인을 수행할 수 없으므로 이 서명자를 알 수 없습니다.
* **신뢰할 수 있음**: 이 서명자는 신뢰할 수 있습니다.
* **신뢰할 수 없음**: 이 서명자는 신뢰할 수 없습니다.

**추가 참조**

[Java API를 사용하여 디지털 서명 확인](#verify-digital-signatures-using-the-java-api)

[웹 서비스 API를 사용하여 디지털 서명 확인](#verify-digital-signatures-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API를 사용하여 디지털 서명 확인 {#verify-digital-signatures-using-the-java-api}

Java(서명 서비스 API)를 사용하여 디지털 서명을 확인합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-signatures-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. 서명 클라이언트 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하고 `SignatureServiceClient` 개체를 전달하여 `ServiceClientFactory` 개체를 만듭니다.

1. 확인할 서명이 포함된 PDF 문서 가져오기

   * 생성자를 사용하여 확인할 서명이 포함된 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만듭니다. PDF 문서의 위치를 지정하는 문자열 값을 전달합니다.
   * 생성자를 사용하고 `com.adobe.idp.Document` 개체를 전달하여 `java.io.FileInputStream` 개체를 만듭니다.

1. PKI 런타임 옵션 설정

   * 해당 생성자를 사용하여 `PKIOptions` 개체를 만듭니다.
   * `PKIOptions` 개체의 `setVerificationTime` 메서드를 호출하고 확인 시간을 지정하는 `VerificationTime` 열거형 값을 전달하여 확인 시간을 설정합니다.
   * `PKIOptions` 개체의 `setRevocationCheckStyle` 메서드를 호출하고 해지 검사를 수행할지 여부를 지정하는 `RevocationCheckStyle` 열거형 값을 전달하여 해지 검사 옵션을 설정합니다.

1. 디지털 서명 확인

   `SignatureServiceClient` 개체의 `verify2` 메서드를 호출하고 다음 값을 전달하여 서명을 확인합니다.

   * 디지털 서명 또는 인증된 PDF 문서가 포함된 `com.adobe.idp.Document` 개체입니다.
   * 확인할 서명이 포함된 서명 필드 이름을 나타내는 문자열 값입니다.
   * PKI 런타임 옵션이 포함된 `PKIOptions` 개체입니다.
   * SPI 정보가 포함된 `VerifySPIOptions` 인스턴스입니다. 이 매개 변수에 대해 `null`을(를) 지정할 수 있습니다.

   `verify2` 메서드가 디지털 서명을 확인하는 데 사용할 수 있는 정보가 포함된 `PDFSignatureVerificationInfo` 개체를 반환합니다.

1. 서명 상태 확인

   * `PDFSignatureVerificationInfo` 개체의 `getStatus` 메서드를 호출하여 서명의 상태를 확인합니다. 이 메서드는 서명 상태를 지정하는 `SignatureStatus` 개체를 반환합니다. 예를 들어 서명된 PDF 문서가 수정되지 않으면 이 메서드는 `SignatureStatus.DocumentSigNoChanges`을(를) 반환합니다.

1. 서명자의 ID 확인

   * `PDFSignatureVerificationInfo` 개체의 `getSigner` 메서드를 호출하여 서명자의 ID를 확인합니다. 이 메서드는 `IdentityInformation` 개체를 반환합니다.
   * 서명자의 ID를 확인하려면 `IdentityInformation` 개체의 `getStatus` 메서드를 호출하십시오. 이 메서드는 ID를 지정하는 `IdentityStatus` 열거 값을 반환합니다. 예를 들어 서명자를 신뢰할 수 있는 경우 이 메서드는 `IdentityStatus.TRUSTED`을(를) 반환합니다.

**추가 참조**

[디지털 서명 확인](#verify-digital-signatures-using-the-java-api)

[빠른 시작(SOAP 모드): Java API를 사용하여 디지털 서명 확인](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-a-digital-signature-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 디지털 서명 확인 {#verify-digital-signatures-using-the-web-service-api}

서명 서비스 API(웹 서비스)를 사용하여 디지털 서명을 확인합니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. WSDL 정의 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`을(를) 사용하는지 확인하십시오.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꾸십시오.

1. 서명 클라이언트 만들기

   * 기본 생성자를 사용하여 `SignatureServiceClient` 개체를 만듭니다.
   * `SignatureServiceClient.Endpoint.Address` 생성자를 사용하여 `System.ServiceModel.EndpointAddress` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/SignatureService?WSDL`). `lc_version` 특성은 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * `System.ServiceModel.BasicHttpBinding` 필드의 값을 가져와 `SignatureServiceClient.Endpoint.Binding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`(으)로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * `SignatureServiceClient.ClientCredentials.UserName.UserName` 필드에 AEM Forms 사용자 이름을 지정하십시오.
      * 필드 `SignatureServiceClient.ClientCredentials.UserName.Password`에 해당 암호 값을 지정하십시오.
      * 상수 값 `HttpClientCredentialType.Basic`을(를) 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.
      * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을(를) 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. 확인할 서명이 포함된 PDF 문서 가져오기

   * 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 확인할 디지털 서명 또는 인증된 서명이 포함된 PDF 문서를 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하여 `System.IO.FileStream` 개체를 만듭니다. 서명된 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하여 바이트 배열을 스트림 데이터로 채웁니다. 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 해당 `BLOB` 속성을 바이트 배열의 내용으로 할당하여 `MTOM` 개체를 채웁니다.

1. PKI 런타임 옵션 설정

   * 해당 생성자를 사용하여 `PKIOptions` 개체를 만듭니다.
   * `PKIOptions` 개체의 `verificationTime` 데이터 멤버에 확인 시간을 지정하는 `VerificationTime` 열거형 값을 할당하여 확인 시간을 설정합니다.
   * 해지 검사를 수행할지 여부를 지정하는 `PKIOptions` 열거형 값을 `revocationCheckStyle` 개체의 `RevocationCheckStyle` 데이터 멤버에 할당하여 해지 검사 옵션을 설정합니다.

1. 디지털 서명 확인

   `SignatureServiceClient` 개체의 `verify2` 메서드를 호출하고 다음 값을 전달하여 서명을 확인합니다.

   * 디지털 서명 또는 인증된 PDF 문서가 포함된 `BLOB` 개체입니다.
   * 확인할 서명이 포함된 서명 필드 이름을 나타내는 문자열 값입니다.
   * PKI 런타임 옵션이 포함된 `PKIOptions` 개체입니다.
   * SPI 정보가 포함된 `VerifySPIOptions` 인스턴스입니다. 이 매개 변수에 대해 `null`을(를) 지정할 수 있습니다.

   `verify2` 메서드가 디지털 서명을 확인하는 데 사용할 수 있는 정보가 포함된 `PDFSignatureVerificationInfo` 개체를 반환합니다.

1. 서명 상태 확인

   `PDFSignatureVerificationInfo` 개체의 `status` 데이터 멤버의 값을 가져와서 서명의 상태를 확인합니다. 이 데이터 멤버는 서명의 상태를 지정하는 `SignatureStatus` 개체를 저장합니다. 예를 들어 서명된 PDF 문서가 수정되면 `status` 데이터 멤버가 값 `SignatureStatus.DocumentSigNoChanges`을(를) 저장합니다.

1. 서명자의 ID 확인

   * `PDFSignatureVerificationInfo` 개체의 `signer` 데이터 멤버의 값을 검색하여 서명자의 ID를 확인합니다. 이 멤버는 `IdentityInformation` 개체를 반환합니다.
   * `IdentityInformation` 개체의 `status` 데이터 구성원을 검색하여 서명자의 ID를 확인합니다. 이 데이터 멤버는 ID를 지정하는 `IdentityStatus` 열거형 값을 반환합니다. 예를 들어 서명자를 신뢰할 수 있는 경우 이 멤버는 `IdentityStatus.TRUSTED`을(를) 반환합니다.

**추가 참조**

[디지털 서명 확인](#verify-digital-signatures-using-the-java-api)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 여러 디지털 서명 확인 {#verifying-multiple-digital-signatures}

AEM Forms은 PDF 문서에 있는 모든 디지털 서명을 확인하는 수단을 제공합니다. 여러 서명자의 서명이 필요한 비즈니스 프로세스의 결과로 PDF 문서에 여러 디지털 서명이 포함되어 있다고 가정합니다. 예를 들어 대출담당자와 관리자의 서명이 모두 필요한 금융거래를 고려한다. 서명 서비스 Java API 또는 웹 서비스 API를 사용하여 PDF 문서 내의 모든 서명을 확인할 수 있습니다. 여러 디지털 서명을 검증할 때 각 서명의 상태와 속성을 확인할 수 있습니다. 디지털 서명을 신뢰하기 전에 확인하는 것이 좋습니다. 단일 디지털 서명 확인에 익숙한 것이 좋습니다.

>[!NOTE]
>
>서명 서비스 및 디지털 서명 확인에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary_of_steps-7}

여러 디지털 서명을 확인하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. 서명 클라이언트를 만듭니다.
1. 확인할 서명이 포함된 PDF 문서를 가져옵니다.
1. PKI 런타임 옵션을 설정합니다.
1. 모든 디지털 서명을 검색합니다.
1. 모든 서명을 반복합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필수)

이러한 JAR 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)을 참조하십시오.

**서명 클라이언트 만들기**

서명 서비스 작업을 프로그래밍 방식으로 수행하기 전에 서명 서비스 클라이언트를 만듭니다.

**확인할 서명이 포함된 PDF 문서를 가져옵니다**

PDF 문서에 디지털 서명하거나 인증하는 데 사용되는 서명을 확인하려면 서명이 포함된 PDF 문서를 가져옵니다.

**PKI 런타임 옵션 설정**

PDF 문서에서 모든 서명을 확인할 때 서명 서비스에서 사용하는 다음 PKI 런타임 옵션을 설정합니다.

* 확인 시간
* 해지 확인
* 시간 스탬핑 값

이러한 옵션을 설정하는 과정의 일부로 확인 시간을 지정할 수 있습니다. 예를 들어 현재 시간(유효성 검사기의 컴퓨터에 있는 시간)을 선택하여 현재 시간을 사용할 수 있습니다. 다른 시간 값에 대한 자세한 내용은 `VerificationTime`AEM Forms API 참조[에서 ](https://www.adobe.com/go/learn_aemforms_javadocs_63_en) 열거 값을 참조하십시오.

유효성 검사 프로세스의 일부로 해지 검사를 수행할지 여부도 지정할 수 있습니다. 예를 들어 해지 확인을 수행하여 인증서가 해지되었는지 확인할 수 있습니다. 해지 확인 옵션에 대한 자세한 내용은 `RevocationCheckStyle`AEM Forms API 참조[의 ](https://www.adobe.com/go/learn_aemforms_javadocs_63_en) 열거 값을 참조하십시오.

인증서에 대한 해지 검사를 수행하려면 `CRLOptionSpec` 개체를 사용하여 CRL(인증서 해지 목록) 서버에 대한 URL을 지정하십시오. 그러나 CRL 서버에 대한 URL을 지정하지 않으면 서명 서비스가 인증서에서 URL을 가져옵니다.

해지 검사를 수행할 때 CRL 서버를 사용하는 대신 OCSP(온라인 인증서 상태 프로토콜) 서버를 사용할 수 있습니다. 일반적으로 CRL 서버 대신 OCSP 서버를 사용하는 경우 해지 확인이 더 빨리 수행됩니다. ([온라인 인증서 상태 프로토콜](https://tools.ietf.org/html/rfc2560)을 참조하세요.)

Adobe 응용 프로그램 및 서비스를 사용하여 서명 서비스에서 사용하는 CRL 및 OCSP 서버 순서를 설정할 수 있습니다. 예를 들어 OCSP 서버가 Adobe Applications and Services에서 먼저 설정된 경우 OCSP 서버를 확인하고 CRL 서버를 선택합니다.

해지 확인을 수행하지 않으면 서명 서비스에서 인증서가 해지되었는지 여부를 확인하지 않습니다. 즉, CRL 및 OCSP 서버 정보는 무시됩니다.

>[!NOTE]
>
>`CRLOptionSpec` 및 `OCSPOptionSpec` 개체를 사용하여 인증서에 지정된 URL을 재정의할 수 있습니다. 예를 들어 CRL 서버를 재정의하려면 `CRLOptionSpec` 개체의 `setLocalURI` 메서드를 호출할 수 있습니다.

타임스탬프는 서명 또는 인증된 문서가 수정된 시간을 추적하는 프로세스입니다. 문서에 서명한 후에는 아무도 수정할 수 없습니다. 타임스탬프는 서명 또는 인증된 문서의 유효성을 검사하는 데 도움이 됩니다. `TSPOptionSpec` 개체를 사용하여 타임스탬프 옵션을 설정할 수 있습니다. 예를 들어 TSP(타임스탬프 제공자) 서버의 URL을 지정할 수 있습니다.

>[!NOTE]
>
>Java 및 웹 서비스 빠른 시작에서 확인 시간은 `VerificationTime.CURRENT_TIME`(으)로 설정되고 해지 검사는 `RevocationCheckStyle.BestEffort`(으)로 설정됩니다. CRL 또는 OCSP 서버 정보를 지정하지 않았으므로 인증서에서 서버 정보를 가져옵니다.

**모든 디지털 서명 검색**

PDF 문서에서 모든 디지털 서명을 확인하려면 PDF 문서에서 디지털 서명을 검색하십시오. 모든 서명은 목록에 반환됩니다. 디지털 서명을 확인하는 과정의 일부로 서명 상태를 확인하십시오.

>[!NOTE]
>
>단일 디지털 서명을 확인하는 경우와 달리 여러 서명을 확인하는 경우에는 서명 필드 이름을 지정할 필요가 없습니다.

**모든 서명을 반복합니다**

각 서명을 반복합니다. 즉, 각 서명에 대하여 전자서명을 검증하고 서명자의 신원과 각 서명의 상태를 확인한다. ([디지털 서명 확인](#verify-digital-signatures-using-the-java-api)을 참조하십시오.)

>[!NOTE]
>
>전체 문서가 필수인 경우에는 모든 서명을 반복할 필요가 없습니다.

**추가 참조**

[Java API를 사용하여 여러 디지털 서명 확인](#verify-digital-signatures-using-the-java-api)

[웹 서비스 API를 사용하여 여러 디지털 서명 확인](#verify-digital-signatures-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API를 사용하여 여러 디지털 서명 확인 {#verify-multiple-digital-signatures-using-the-java-api}

Java(서명 서비스 API)를 사용하여 여러 디지털 서명을 확인합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-signatures-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. 서명 클라이언트 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하고 `SignatureServiceClient` 개체를 전달하여 `ServiceClientFactory` 개체를 만듭니다.

1. 확인할 서명이 포함된 PDF 문서 가져오기

   * 생성자를 사용하여 확인할 여러 디지털 서명이 포함된 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만듭니다. PDF 문서의 위치를 지정하는 문자열 값을 전달합니다.
   * 생성자를 사용하고 `com.adobe.idp.Document` 개체를 전달하여 `java.io.FileInputStream` 개체를 만듭니다.

1. PKI 런타임 옵션 설정

   * 해당 생성자를 사용하여 `PKIOptions` 개체를 만듭니다.
   * `PKIOptions` 개체의 `setVerificationTime` 메서드를 호출하고 확인 시간을 지정하는 `VerificationTime` 열거형 값을 전달하여 확인 시간을 설정합니다.
   * `PKIOptions` 개체의 `setRevocationCheckStyle` 메서드를 호출하고 해지 검사를 수행할지 여부를 지정하는 `RevocationCheckStyle` 열거형 값을 전달하여 해지 검사 옵션을 설정하십시오.

1. 모든 디지털 서명 검색

   `SignatureServiceClient` 개체의 `verifyPDFDocument` 메서드를 호출하고 다음 값을 전달하십시오.

   * 여러 디지털 서명이 포함된 PDF 문서가 포함된 `com.adobe.idp.Document` 개체입니다.
   * PKI 런타임 옵션이 포함된 `PKIOptions` 개체입니다.
   * SPI 정보가 포함된 `VerifySPIOptions` 인스턴스입니다. 이 매개 변수에 대해 `null`을(를) 지정할 수 있습니다.

   `verifyPDFDocument` 메서드는 PDF 문서의 모든 디지털 서명에 대한 정보가 포함된 `PDFDocumentVerificationInfo` 개체를 반환합니다.

1. 모든 서명 반복

   * `PDFDocumentVerificationInfo` 개체의 `getVerificationInfos` 메서드를 호출하여 모든 서명을 반복합니다. 이 메서드는 각 요소가 `java.util.List` 개체인 `PDFSignatureVerificationInfo` 개체를 반환합니다. `java.util.Iterator` 개체를 사용하여 서명 목록을 반복합니다.
   * `PDFSignatureVerificationInfo` 개체를 사용하면 `PDFSignatureVerificationInfo` 개체의 `getStatus` 메서드를 호출하여 서명 상태를 확인하는 등의 작업을 수행할 수 있습니다. 이 메서드는 정적 데이터 멤버가 서명의 상태에 대해 알리는 `SignatureStatus` 개체를 반환합니다. 예를 들어 서명을 알 수 없는 경우 이 메서드는 `SignatureStatus.DocumentSignatureUnknown`을(를) 반환합니다.

**추가 참조**

[여러 디지털 서명 확인](#verifying-multiple-digital-signatures)

[빠른 시작(SOAP 모드): Java API를 사용하여 여러 디지털 서명 확인](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[디지털 서명 확인](#verify-digital-signatures-using-the-java-api)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 여러 디지털 서명 확인 {#verifying-multiple-digital-signatures-using-the-web-service-api}

서명 서비스 API(웹 서비스)를 사용하여 여러 디지털 서명을 확인합니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. WSDL 정의 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`을(를) 사용하는지 확인하십시오.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꾸십시오.

1. 서명 클라이언트 만들기

   * 기본 생성자를 사용하여 `SignatureServiceClient` 개체를 만듭니다.
   * `SignatureServiceClient.Endpoint.Address` 생성자를 사용하여 `System.ServiceModel.EndpointAddress` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/SignatureService?WSDL`). `lc_version` 특성은 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * `System.ServiceModel.BasicHttpBinding` 필드의 값을 가져와 `SignatureServiceClient.Endpoint.Binding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`(으)로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * `SignatureServiceClient.ClientCredentials.UserName.UserName` 필드에 AEM Forms 사용자 이름을 지정하십시오.
      * 필드 `SignatureServiceClient.ClientCredentials.UserName.Password`에 해당 암호 값을 지정하십시오.
      * 상수 값 `HttpClientCredentialType.Basic`을(를) 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.
      * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을(를) 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. 확인할 서명이 포함된 PDF 문서 가져오기

   * 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 확인할 여러 디지털 서명이 포함된 PDF 문서를 저장합니다.
   * 해당 생성자를 호출하여 `System.IO.FileStream` 개체를 만듭니다. PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하여 바이트 배열을 스트림 데이터로 채웁니다. 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 해당 `BLOB` 속성을 바이트 배열의 내용으로 할당하여 `MTOM` 개체를 채웁니다.

1. PKI 런타임 옵션 설정

   * 해당 생성자를 사용하여 `PKIOptions` 개체를 만듭니다.
   * `PKIOptions` 개체의 `verificationTime` 데이터 멤버에 확인 시간을 지정하는 `VerificationTime` 열거형 값을 할당하여 확인 시간을 설정합니다.
   * 해지 검사를 수행할지 여부를 지정하는 `PKIOptions` 열거형 값을 `revocationCheckStyle` 개체의 `RevocationCheckStyle` 데이터 멤버에 할당하여 해지 검사 옵션을 설정합니다.

1. 모든 디지털 서명 검색

   `SignatureServiceClient` 개체의 `verifyPDFDocument` 메서드를 호출하고 다음 값을 전달하십시오.

   * 여러 디지털 서명이 포함된 PDF 문서가 포함된 `BLOB` 개체입니다.
   * PKI 런타임 옵션이 포함된 `PKIOptions` 개체입니다.
   * SPI 정보가 포함된 `VerifySPIOptions` 인스턴스입니다. 이 매개 변수에 대해 null을 지정할 수 있습니다.

   `verifyPDFDocument` 메서드는 PDF 문서의 모든 디지털 서명에 대한 정보가 포함된 `PDFDocumentVerificationInfo` 개체를 반환합니다.

1. 모든 서명 반복

   * `PDFDocumentVerificationInfo` 개체의 `verificationInfos` 데이터 멤버를 가져와서 모든 서명을 반복합니다. 이 데이터 멤버는 각 요소가 `Object` 개체인 `PDFSignatureVerificationInfo` 배열을 반환합니다.
   * `PDFSignatureVerificationInfo` 개체를 사용하면 `PDFSignatureVerificationInfo` 개체의 `status` 데이터 멤버를 가져와서 서명 상태를 확인하는 등의 작업을 수행할 수 있습니다. 이 데이터 멤버는 정적 데이터 멤버가 서명 상태에 대해 알리는 `SignatureStatus` 개체를 반환합니다. 예를 들어 서명을 알 수 없는 경우 이 메서드는 `SignatureStatus.DocumentSignatureUnknown`을(를) 반환합니다.

**추가 참조**

[여러 디지털 서명 확인](#verifying-multiple-digital-signatures)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 디지털 서명 제거 {#removing-digital-signatures}

최신 디지털 서명을 적용하려면 먼저 서명 필드에서 디지털 서명을 제거해야 합니다. 디지털 서명은 덮어쓸 수 없습니다. 서명이 포함된 서명 필드에 디지털 서명을 적용하려고 하면 예외가 발생합니다.

>[!NOTE]
>
>서명 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary_of_steps-8}

서명 필드에서 디지털 서명을 제거하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. 서명 클라이언트를 만듭니다.
1. 제거할 서명이 포함된 PDF 문서를 가져옵니다.
1. 서명 필드에서 디지털 서명을 제거합니다.
1. PDF 문서를 PDF 파일로 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 생성하는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필수)

이러한 JAR 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)을 참조하십시오.

**서명 클라이언트 만들기**

서명 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 서명 서비스 클라이언트를 만들어야 합니다.

**제거할 서명이 포함된 PDF 문서를 가져옵니다**

PDF 문서에서 서명을 제거하려면 서명이 포함된 PDF 문서를 받아야 합니다.

**서명 필드에서 디지털 서명 제거**

PDF 문서에서 디지털 서명을 성공적으로 제거하려면 디지털 서명이 포함된 서명 필드의 이름을 지정해야 합니다. 또한 디지털 서명을 제거할 수 있는 권한이 있어야 합니다. 그렇지 않으면 예외가 발생합니다.

**PDF 문서를 PDF 파일로 저장**

서명 서비스에서 서명 필드에서 디지털 서명을 제거한 후 사용자가 PDF 또는 Adobe Reader에서 열 수 있도록 PDF 문서를 Acrobat 파일로 저장할 수 있습니다.

**추가 참조**

[Java API를 사용하여 디지털 서명 제거](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-java-api)

[웹 서비스 API를 사용하여 디지털 서명 제거](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[서명 필드 추가](digitally-signing-certifying-documents.md#adding-signature-fields)

### Java API를 사용하여 디지털 서명 제거 {#remove-digital-signatures-using-the-java-api}

서명 API(Java)를 사용하여 디지털 서명을 제거합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-signatures-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. 서명 클라이언트를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하고 `SignatureServiceClient` 개체를 전달하여 `ServiceClientFactory` 개체를 만듭니다.

1. 제거할 서명이 포함된 PDF 문서 가져오기

   * 생성자를 사용하고 PDF 문서의 위치를 지정하는 문자열 값을 전달하여 제거할 서명이 포함된 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만듭니다.
   * 생성자를 사용하고 `com.adobe.idp.Document` 개체를 전달하여 `java.io.FileInputStream` 개체를 만듭니다.

1. 서명 필드에서 디지털 서명 제거

   `SignatureServiceClient` 개체의 `clearSignatureField` 메서드를 호출하고 다음 값을 전달하여 서명 필드에서 디지털 서명을 제거합니다.

   * 제거할 서명이 포함된 PDF 문서를 나타내는 `com.adobe.idp.Document` 개체입니다.
   * 디지털 서명이 포함된 서명 필드의 이름을 지정하는 문자열 값입니다.

   `clearSignatureField` 메서드는 디지털 서명이 제거된 PDF 문서를 나타내는 `com.adobe.idp.Document` 개체를 반환합니다.

1. PDF 문서를 PDF 파일로 저장

   * `java.io.File` 개체를 만들고 파일 확장명이 .pdf인지 확인하십시오.
   * `com.adobe.idp.Document` 개체의 `copyToFile` 메서드를 호출합니다. `java.io.File` 개체를 전달하여 `com.adobe.idp.Document` 개체의 내용을 파일에 복사합니다. `Document` 메서드에서 반환된 `clearSignatureField` 개체를 사용하는지 확인하십시오.

**추가 참조**

[디지털 서명 제거](digitally-signing-certifying-documents.md#removing-digital-signatures)

[빠른 시작(SOAP 모드): Java API를 사용하여 디지털 서명 제거](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-removing-a-digital-signature-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 디지털 서명 제거 {#remove-digital-signatures-using-the-web-service-api}

서명 API(웹 서비스)를 사용하여 디지털 서명을 제거합니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. WSDL 정의 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`을(를) 사용하는지 확인하십시오.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꾸십시오.

1. 서명 클라이언트 만들기

   * 기본 생성자를 사용하여 `SignatureServiceClient` 개체를 만듭니다.
   * `SignatureServiceClient.Endpoint.Address` 생성자를 사용하여 `System.ServiceModel.EndpointAddress` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/SignatureService?WSDL`). `lc_version` 특성은 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * `System.ServiceModel.BasicHttpBinding` 필드의 값을 가져와 `SignatureServiceClient.Endpoint.Binding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`(으)로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * `SignatureServiceClient.ClientCredentials.UserName.UserName` 필드에 AEM Forms 사용자 이름을 지정하십시오.
      * 필드 `SignatureServiceClient.ClientCredentials.UserName.Password`에 해당 암호 값을 지정하십시오.
      * 상수 값 `HttpClientCredentialType.Basic`을(를) 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.
      * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을(를) 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. 제거할 서명이 포함된 PDF 문서 가져오기

   * 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 제거할 디지털 서명이 포함된 PDF 문서를 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하고 서명된 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하여 바이트 배열을 스트림 데이터로 채웁니다. 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 해당 `BLOB` 속성을 바이트 배열의 내용으로 할당하여 `MTOM` 개체를 채웁니다.

1. 서명 필드에서 디지털 서명 제거

   `SignatureServiceClient` 개체의 `clearSignatureField` 메서드를 호출하고 다음 값을 전달하여 디지털 서명을 제거하십시오.

   * 서명된 PDF 문서가 포함된 `BLOB` 개체입니다.
   * 제거할 디지털 서명이 포함된 서명 필드의 이름을 나타내는 문자열 값입니다.

   `clearSignatureField` 메서드는 디지털 서명이 제거된 PDF 문서를 나타내는 `BLOB` 개체를 반환합니다.

1. PDF 문서를 PDF 파일로 저장

   * 해당 생성자를 호출하고 빈 서명 필드가 포함된 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `BLOB` 메서드에서 반환된 `sign` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `BLOB` 개체의 `MTOM` 데이터 멤버의 값을 가져와서 바이트 배열을 채웁니다.
   * 해당 생성자를 호출하고 `System.IO.BinaryWriter` 개체를 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.BinaryWriter` 개체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 PDF 파일에 씁니다.

**추가 참조**

[디지털 서명 제거](digitally-signing-certifying-documents.md#removing-digital-signatures)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
