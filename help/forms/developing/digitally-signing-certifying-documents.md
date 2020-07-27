---
title: 문서 디지털 서명 및 인증
seo-title: 문서 디지털 서명 및 인증
description: 'null'
seo-description: 'null'
uuid: 6331de8a-2a9c-45bf-89d2-29f1ad5cc856
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 42de04bf-25e4-4478-a411-38671ed871ae
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '16977'
ht-degree: 0%

---


# 문서 디지털 서명 및 인증 {#digitally-signing-and-certifying-documents}

**서명 서비스 정보**

서명 서비스를 사용하면 조직이 배포 및 수신하는 Adobe PDF 문서의 보안 및 개인 정보를 보호할 수 있습니다. 이 서비스는 수신자만 문서를 변경할 수 있도록 디지털 서명 및 인증을 사용합니다. 문서 자체에 보안 기능이 적용되므로 문서의 전체 수명 주기 동안 안전하게 관리됩니다. 문서가 오프라인으로 다운로드될 때 조직에 다시 제출될 때 방화벽 외부의 보안이 유지됩니다.

>[!NOTE]
>
>PDF 문서 서명과 같은 특정 작업을 호출할 때 호출되는 서명 서비스에 대한 사용자 정의 서명 핸들러를 만들 수 있습니다.

**서명 필드 이름**

일부 서명 서비스 작업에서는 작업이 수행되는 서명 필드의 이름을 지정해야 합니다. 예를 들어 PDF 문서에 서명할 때 서명할 서명 필드의 이름을 지정합니다. 서명 필드의 전체 이름이 있다고 가정합니다 `form1[0].Form1[0].SignatureField1[0]`. 대신 `SignatureField1[0]` 지정할 수 있습니다 `form1[0].Form1[0].SignatureField1[0]`.

때로 충돌이 발생하면 서명 서비스가 잘못된 필드에 서명하거나 서명 필드 이름이 필요한 다른 작업을 수행합니다. 이러한 충돌은 동일한 PDF 문서의 두 곳 `SignatureField1[0]` 이상에 나타나는 이름이 원인입니다. 예를 들어, 이름을 지정하고 지정하는 두 개의 서명 필드 `form1[0].Form1[0].SignatureField1[0]` 가 들어 있는 PDF 문서 `form1[0].Form1[0].SubForm1[0].SignatureField1[0]` 를 고려해 보십시오 `SignatureField1[0]`. 이러한 경우 서명 서비스는 문서의 모든 서명 필드를 반복하면서 발견한 첫 번째 서명 필드에 서명합니다.

PDF 문서 내에 여러 개의 서명 필드가 있는 경우 서명 필드의 전체 이름을 지정하는 것이 좋습니다. 즉, 대신 `form1[0].Form1[0].SignatureField1[0]`지정합니다 `SignatureField1[0]`.

서명 서비스를 사용하여 이러한 작업을 수행할 수 있습니다.

* PDF 문서에 디지털 서명 필드 추가 및 삭제 (서명 필드 [추가를 참조하십시오](digitally-signing-certifying-documents.md#adding-signature-fields).)
* PDF 문서에 있는 서명 필드의 이름을 검색합니다. (서명 [필드 이름 검색을 참조하십시오](digitally-signing-certifying-documents.md#retrieving-signature-field-names).)
* 서명 필드를 수정합니다. (서명 필드 [수정을 참조하십시오](digitally-signing-certifying-documents.md#modifying-signature-fields).)
* PDF 문서에 디지털 서명 (PDF 문서 [디지털 서명 참조](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents))
* PDF 문서 인증 (PDF [문서 인증을 참조하십시오](digitally-signing-certifying-documents.md#certifying-pdf-documents).)
* PDF 문서에 있는 디지털 서명의 유효성을 확인합니다. (디지털 서명 [확인을 참조하십시오](digitally-signing-certifying-documents.md#verifying-digital-signatures).)
* PDF 문서에 있는 모든 디지털 서명의 유효성을 확인합니다. (여러 [디지털 서명 확인을 참조하십시오](digitally-signing-certifying-documents.md#verifying-digital-signatures).)
* 서명 필드에서 디지털 서명을 제거합니다. (디지털 서명 [제거를 참조하십시오](digitally-signing-certifying-documents.md#removing-digital-signatures).)

>[!NOTE]
>
>서명 서비스에 대한 자세한 내용은 AEM Forms에 대한 [서비스 참조 자료를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

## 서명 필드 추가 {#adding-signature-fields}

디지털 서명은 서명의 그래픽 표현이 포함된 양식 필드인 서명 필드에 나타납니다. 서명 필드는 표시하거나 숨길 수 있습니다. 서명자는 기존 서명 필드를 사용하거나 서명 필드를 프로그래밍 방식으로 추가할 수 있습니다. 두 경우 모두 PDF 문서에 서명하기 전에 서명 필드가 있어야 합니다.

서명 서비스 Java API 또는 서명 웹 서비스 API를 사용하여 프로그래밍 방식으로 서명 필드를 추가할 수 있습니다. PDF 문서에 두 개 이상의 서명 필드를 추가할 수 있습니다. 그러나 각 서명 필드 이름은 고유해야 합니다.

>[!NOTE]
>
>일부 PDF 문서 유형에서는 프로그래밍 방식으로 서명 필드를 추가할 수 없습니다. 서명 서비스 및 서명 필드 추가에 대한 자세한 내용은 AEM Forms에 대한 [서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary-of-steps}

PDF 문서에 서명 필드를 추가하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일 포함
1. 서명 클라이언트 만들기를 참조하십시오.
1. 서명 필드가 추가된 PDF 문서를 가져옵니다.
1. 서명 필드 추가
1. PDF 문서를 PDF 파일로 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

다음 JAR 파일을 프로젝트의 클래스 경로에 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(AEM Forms이 JBoss에 배포된 경우 필요)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필요)

**서명 클라이언트 만들기**

서명 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 서명 서비스 클라이언트를 만들어야 합니다.

**서명 필드가 추가된 PDF 문서 가져오기**

서명 필드가 추가된 PDF 문서를 얻어야 합니다.

**서명 필드 추가**

PDF 문서에 서명 필드를 성공적으로 추가하려면 서명 필드의 위치를 식별하는 좌표 값을 지정합니다. 보이지 않는 서명 필드를 추가하는 경우 이러한 값은 필요하지 않습니다. 또한 서명을 서명 필드에 적용한 후 PDF 문서에서 잠길 필드를 지정할 수 있습니다.

**PDF 문서를 PDF 파일로 저장**

서명 서비스가 PDF 문서에 서명 필드를 추가한 후 사용자가 Acrobat 또는 Adobe Reader에서 문서를 열 수 있도록 문서를 PDF 파일로 저장할 수 있습니다.

**참고 항목**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF 문서에 디지털 서명](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Java API를 사용하여 서명 필드 추가 {#add-signature-fields-using-the-java-api}

서명 API(Java)를 사용하여 서명 필드를 추가합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-signatures-client.jar 등의 클라이언트 JAR 파일을 포함합니다.

1. 서명 클라이언트 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 개체를 `SignatureServiceClient` 만들고 개체를 `ServiceClientFactory` 전달합니다.

1. 서명 필드가 추가된 PDF 문서 가져오기

   * 생성자를 사용하여 서명 필드가 추가되는 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만들고 PDF 문서의 위치를 지정하는 문자열 값을 전달합니다.
   * 생성자를 사용하여 개체를 `com.adobe.idp.Document` 만들고 개체를 `java.io.FileInputStream` 전달합니다.

1. 서명 필드 추가

   * 생성자를 사용하여 서명 필드 위치를 지정하는 `PositionRectangle` 개체를 만듭니다. 생성자 내에서 좌표 값을 지정합니다.
   * 원하는 경우 디지털 서명이 서명 필드에 적용될 때 잠긴 필드를 지정하는 `FieldMDPOptions` 개체를 만듭니다.
   * 개체의 메서드를 호출하고 다음 값을 전달하여 PDF 문서에 서명 필드 `SignatureServiceClient` `addSignatureField` 를 추가합니다.

      * A `com.adobe.idp`. `Document` 서명 필드가 추가된 PDF 문서를 나타내는 개체
      * 서명 필드의 이름을 지정하는 문자열 값.
      * 서명 필드가 추가된 페이지 번호를 나타내는 `java.lang.Integer` 값입니다.
      * 서명 필드의 위치를 지정하는 `PositionRectangle` 개체입니다.
      * 디지털 서명이 서명 필드에 적용된 후 잠긴 PDF 문서의 필드를 지정하는 `FieldMDPOptions` 개체 이 매개 변수 값은 선택 사항이며 전달할 수 있습니다 `null`.
   * 다양한 런타임 값을 지정하는 `PDFSeedValueOptions` 개체입니다. 이 매개 변수 값은 선택 사항이며 전달할 수 있습니다 `null`.

      이 `addSignatureField` 메서드는 a를 반환합니다 `com.adobe.idp`. `Document` 서명 필드가 포함된 PDF 문서를 나타내는 개체
   >[!NOTE]
   >
   >객체의 메서드를 호출하여 보이지 않는 서명 필드를 추가할 수 `SignatureServiceClient` `addInvisibleSignatureField` 있습니다.

1. PDF 문서를 PDF 파일로 저장

   * 개체를 만들고 파일 확장자가 .pdf인지 확인합니다. `java.io.File`
   * 를 `com.adobe.idp`불러옵니다. `Document` 개체의 내용을 파일에 복사하는 개체의 `copyToFile` `Document` 메서드입니다. 를 사용해야 합니다 `com.adobe.idp`. `Document` 메서드에서 반환된 `addSignatureField` 개체입니다.

**참고 항목**

[서명 서비스 API 빠른 시작](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

### 웹 서비스 API를 사용하여 서명 필드 추가 {#add-signature-fields-using-the-web-service-api}

서명 API(웹 서비스)를 사용하여 서명 필드를 추가하려면:

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Forms `localhost` 를 호스팅하는 서버의 IP 주소로 대체합니다.

1. 서명 클라이언트 만들기

   * 기본 생성자를 사용하여 `SignatureServiceClient` 개체를 만듭니다.
   * 생성자를 사용하여 `SignatureServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/SignatureService?WSDL`). 속성을 사용할 필요는 `lc_version` 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * 필드의 값을 `System.ServiceModel.BasicHttpBinding` 가져와 개체를 `SignatureServiceClient.Endpoint.Binding` 만듭니다. 반환 값을 다음으로 캐스팅합니다 `BasicHttpBinding`.
   * 개체 `System.ServiceModel.BasicHttpBinding` 필드를 (으)로 `MessageEncoding` 설정합니다 `WSMessageEncoding.Mtom`. 이 값을 사용하면 MTOM이 사용됩니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM 양식 사용자 이름을 지정합니다 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 해당 암호 값을 필드에 지정합니다 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 필드에 상수 값 `HttpClientCredentialType.Basic` 을 지정합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 필드에 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly` 을 지정합니다 `BasicHttpBindingSecurity.Security.Mode`.

1. 서명 필드가 추가된 PDF 문서 가져오기

   * 생성자를 사용하여 `BLOB` 개체를 만듭니다. 이 `BLOB` 개체는 서명 필드가 포함될 PDF 문서를 저장하는 데 사용됩니다.
   * 생성자를 호출하고 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * 개체의 내용을 저장하는 바이트 배열을 `System.IO.FileStream` 만듭니다. 개체의 속성을 가져와 바이트 배열의 크기를 결정할 수 `System.IO.FileStream` `Length` 있습니다.
   * 개체의 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열 `System.IO.FileStream` `Read` 을 스트림 데이터로 채웁니다.
   * 바이트 배열의 컨텐츠로 해당 `BLOB` `MTOM` 속성을 지정하여 개체를 채웁니다.

1. 서명 필드 추가

   개체의 메서드를 호출하고 다음 값을 전달하여 PDF 문서에 서명 필드를 `SignatureServiceClient` `addSignatureField` 추가합니다.

   * 서명 필드가 추가된 PDF 문서를 나타내는 `BLOB` 개체입니다.
   * 서명 필드 이름을 지정하는 문자열 값.
   * 서명 필드가 추가되는 페이지 번호를 나타내는 정수 값.
   * 서명 필드의 위치를 지정하는 `PositionRect` 개체입니다.
   * 디지털 서명이 서명 필드에 적용된 후 잠긴 PDF 문서의 필드를 지정하는 `FieldMDPOptions` 개체 이 매개 변수 값은 선택 사항이며 전달할 수 있습니다 `null`.
   * 다양한 런타임 값을 지정하는 `PDFSeedValueOptions` 개체입니다. 이 매개 변수 값은 선택 사항이며 전달할 수 있습니다 `null`.

   이 `addSignatureField` 메서드는 서명 필드가 포함된 PDF 문서를 나타내는 `BLOB` 개체를 반환합니다.

1. PDF 문서를 PDF 파일로 저장

   * 생성자를 호출하고 서명 필드와 파일을 열 모드가 포함되어 있는 PDF 문서의 파일 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * 메서드에서 반환된 개체의 내용을 저장하는 바이트 배열을 `BLOB` `addSignatureField` 만듭니다. 개체 데이터 멤버의 값을 가져와 바이트 배열 `BLOB` 을 `binaryData` 채웁니다.
   * 생성자를 호출하고 개체를 전달하여 `System.IO.BinaryWriter` 개체를 `System.IO.FileStream` 만듭니다.
   * 개체의 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 PDF 파일 `System.IO.BinaryWriter` `Write` 에 씁니다.

**참고 항목**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 서명 필드 이름 검색 {#retrieving-signature-field-names}

서명하거나 인증할 PDF 문서에 있는 모든 서명 필드의 이름을 검색할 수 있습니다. PDF 문서에 있는 서명 필드 이름을 잘 모르거나 이름을 확인하려는 경우 프로그래밍 방식으로 검색할 수 있습니다. 서명 서비스는 서명 필드의 정규화된 이름(예: `form1[0].grantApplication[0].page1[0].SignatureField1[0]`

>[!NOTE]
>
>서명 서비스에 대한 자세한 내용은 AEM Forms에 대한 [서비스 참조를 참조하십시오.](https://www.adobe.com/go/learn_aemforms_services_63)

### 단계 요약 {#summary_of_steps-1}

서명 필드 이름을 검색하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일 포함
1. 서명 클라이언트 만들기를 참조하십시오.
1. 서명 필드가 포함된 PDF 문서를 가져올 수 있습니다.
1. 서명 필드 이름을 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

다음 JAR 파일을 프로젝트의 클래스 경로에 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(AEM Forms이 JBoss에 배포된 경우 필요)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필요)

이러한 JAR 파일의 위치에 대한 자세한 내용은 AEM Forms Java 라이브러리 파일 [포함을 참조하십시오](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**서명 클라이언트 만들기**

서명 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 서명 서비스 클라이언트를 만들어야 합니다.

**서명 필드가 포함된 PDF 문서 가져오기**

서명 필드가 포함된 PDF 문서 검색

**서명 필드 이름 검색**

하나 이상의 서명 필드가 포함된 PDF 문서를 검색한 후 서명 필드 이름을 검색할 수 있습니다.

**참고 항목**

[Java API를 사용하여 서명 필드 이름 검색](digitally-signing-certifying-documents.md#retrieve-signature-field-names-using-the-java-api)

[웹 서비스 API를 사용하여 서명 필드 검색](digitally-signing-certifying-documents.md#retrieve-signature-field-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[서명 필드 추가](digitally-signing-certifying-documents.md#adding-signature-fields)

### Java API를 사용하여 서명 필드 이름 검색 {#retrieve-signature-field-names-using-the-java-api}

서명 API(Java)를 사용하여 서명 필드 이름 검색:

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-signatures-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. 서명 클라이언트 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 개체를 `SignatureServiceClient` 만들고 개체를 `ServiceClientFactory` 전달합니다.

1. 서명 필드가 포함된 PDF 문서 가져오기

   * 생성자를 사용하여 PDF 문서의 위치를 지정하는 문자열 값을 전달하여 서명 필드가 포함된 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만듭니다.
   * 생성자를 사용하여 개체를 `com.adobe.idp.Document` 만들고 개체를 `java.io.FileInputStream` 전달합니다.

1. 서명 필드 이름 검색

   * 서명 필드 이름은 `SignatureServiceClient` 개체의 `getSignatureFieldList` 메서드를 호출하고 서명 필드가 포함된 PDF 문서가 들어 있는 `com.adobe.idp.Document` 개체를 전달하여 검색합니다. 이 메서드는 각 요소에 개체가 들어 있는 개체를 `java.util.List` `PDFSignatureField` 반환합니다. 이 개체를 사용하면 서명 필드의 표시 여부 등 추가 정보를 얻을 수 있습니다.
   * 서명 필드 이름이 `java.util.List` 있는지 확인하려면 개체를 반복합니다. PDF 문서의 각 서명 필드에 대해 별도의 `PDFSignatureField` 개체를 가져올 수 있습니다. 서명 필드의 이름을 얻으려면 `PDFSignatureField` 개체의 `getName` 메서드를 호출합니다. 이 메서드는 서명 필드 이름을 지정하는 문자열 값을 반환합니다.

**참고 항목**

[서명 필드 이름 검색](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[빠른 시작(SOAP 모드): Java API를 사용하여 서명 필드 이름 검색](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-retrieving-signature-field-names-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 서명 필드 검색 {#retrieve-signature-field-using-the-web-service-api}

서명 API(웹 서비스)를 사용하여 서명 필드 이름 검색:

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Forms `localhost` 를 호스팅하는 서버의 IP 주소로 대체합니다.

1. 서명 클라이언트 만들기

   * 기본 생성자를 사용하여 `SignatureServiceClient` 개체를 만듭니다.
   * 생성자를 사용하여 `SignatureServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/SignatureService?WSDL`). 속성을 사용할 필요는 `lc_version` 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * 필드의 값을 `System.ServiceModel.BasicHttpBinding` 가져와 개체를 `SignatureServiceClient.Endpoint.Binding` 만듭니다. 반환 값을 다음으로 캐스팅합니다 `BasicHttpBinding`.
   * 개체 `System.ServiceModel.BasicHttpBinding` 필드를 (으)로 `MessageEncoding` 설정합니다 `WSMessageEncoding.Mtom`. 이 값을 사용하면 MTOM이 사용됩니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM 양식 사용자 이름을 지정합니다 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 해당 암호 값을 필드에 지정합니다 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 필드에 상수 값 `HttpClientCredentialType.Basic` 을 지정합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 필드에 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly` 을 지정합니다 `BasicHttpBindingSecurity.Security.Mode`.

1. 서명 필드가 포함된 PDF 문서 가져오기

   * 생성자를 사용하여 `BLOB` 개체를 만듭니다. 이 `BLOB` 개체는 서명 필드가 포함된 PDF 문서를 저장하는 데 사용됩니다.
   * 생성자를 호출하고 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * 개체의 내용을 저장하는 바이트 배열을 `System.IO.FileStream` 만듭니다. 개체의 속성을 가져와 바이트 배열의 크기를 결정할 수 `System.IO.FileStream` `Length` 있습니다.
   * 개체의 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열 `System.IO.FileStream` `Read` 을 스트림 데이터로 채웁니다.
   * 바이트 배열 컨텐츠에 해당 `BLOB` `MTOM` 필드를 할당하여 객체를 채웁니다.

1. 서명 필드 이름 검색

   * 서명 필드 이름은 `SignatureServiceClient` 개체의 `getSignatureFieldList` 메서드를 호출하고 서명 필드가 포함된 PDF 문서가 포함된 `BLOB` 개체를 전달하여 검색합니다. 이 메서드는 각 요소에 개체가 포함되어 있는 `MyArrayOfPDFSignatureField` 컬렉션 개체를 `PDFSignatureField` 반환합니다.
   * 서명 필드 이름이 있는지 여부를 `MyArrayOfPDFSignatureField` 확인하려면 개체를 반복합니다. PDF 문서의 각 서명 필드에 대해 `PDFSignatureField` 개체를 가져올 수 있습니다. 서명 필드의 이름을 얻으려면 `PDFSignatureField` 개체의 `getName` 메서드를 호출합니다. 이 메서드는 서명 필드 이름을 지정하는 문자열 값을 반환합니다.

**참고 항목**

[서명 필드 이름 검색](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 서명 필드 수정 {#modifying-signature-fields}

Java API 및 웹 서비스 API를 사용하여 PDF 문서에 있는 서명 필드를 수정할 수 있습니다. 서명 필드를 수정하면 서명 필드 잠금 사전 값 또는 시드 값 사전 값을 조작하는 작업이 포함됩니다.

필드 *잠금 사전은* 서명 필드가 서명될 때 잠긴 필드 목록을 지정합니다. 필드가 잠기면 사용자가 필드를 변경할 수 없습니다. 시드 값 사전 ** 은 서명이 적용될 때 사용되는 제한 정보를 포함합니다. 예를 들어 서명을 무효화하지 않고 발생할 수 있는 작업을 제어하는 권한을 변경할 수 있습니다.

기존 서명 필드를 수정하여 변경된 비즈니스 요구 사항을 반영하도록 PDF 문서를 변경할 수 있습니다. 예를 들어, 새로운 비즈니스 요구 사항은 문서에 서명한 후 모든 문서 필드를 잠가야 할 수 있습니다.

이 섹션에서는 필드 잠금 사전 및 시드 값 사전 값을 모두 수정하여 서명 필드를 수정하는 방법에 대해 설명합니다. 서명 필드 잠금 사전이 변경되면 PDF 문서의 모든 필드가 서명 필드에 서명할 때 잠깁니다. 시드 값 사전의 변경 사항으로 인해 문서의 특정 유형이 변경되지 않습니다.

>[!NOTE]
>
>서명 서비스 및 서명 필드 수정에 대한 자세한 내용은 AEM Forms에 대한 [서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-2}

PDF 문서에 있는 서명 필드를 수정하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일 포함
1. 서명 클라이언트 만들기를 참조하십시오.
1. 수정할 서명 필드가 포함된 PDF 문서를 가져옵니다.
1. 사전 값을 설정합니다.
1. 서명 필드를 수정합니다.
1. PDF 문서를 PDF 파일로 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

다음 JAR 파일을 프로젝트의 클래스 경로에 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(AEM Forms이 JBoss에 배포된 경우 필요)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필요)

이러한 JAR 파일의 위치에 대한 자세한 내용은 LiveCycle [Java 라이브러리 파일 포함을 참조하십시오](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**서명 클라이언트 만들기**

서명 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 서명 서비스 클라이언트를 만들어야 합니다.

**수정할 서명 필드가 포함된 PDF 문서 가져오기**

수정할 서명 필드가 포함된 PDF 문서를 검색합니다.

**사전 값 설정**

서명 필드를 수정하려면 필드 잠금 사전 또는 시드 값 사전에 값을 할당합니다. 서명 필드 잠금 사전 값 지정에는 서명 필드가 서명될 때 잠긴 PDF 문서 필드를 지정하는 작업이 포함됩니다. (이 섹션에서는 모든 필드를 잠그는 방법에 대해 설명합니다.)

다음 시드 값 사전 값을 설정할 수 있습니다.

* **개정 확인**: 서명이 서명 필드에 적용될 때 해지 검사가 수행되는지 여부를 지정합니다.
* **인증서 옵션**: 인증서 시드 값 사전에 값을 할당합니다. 인증서 옵션을 지정하기 전에 인증서 시드 값 사전에 익숙해지는 것이 좋습니다. ( [PDF 참조](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf)참조)
* **다이제스트 옵션**: 서명에 사용되는 다이제스트 알고리즘을 할당합니다. 유효한 값은 SHA1, SHA256, SHA384, SHA512 및 RIPEMD160입니다.
* **필터**: 서명 필드에 사용할 필터를 지정합니다. 예를 들어 Adobe.PPKLite 필터를 사용할 수 있습니다. ( [PDF 참조](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf)참조)
* **플래그 옵션**: 이 서명 필드와 관련된 플래그 값을 지정합니다. 값이 1이면 서명자는 항목에 대해 지정된 값만 사용해야 합니다. 값이 0이면 다른 값이 허용됩니다. 비트 위치는 다음과 같습니다.

   * **1(필터):** 서명 필드에 서명하는 데 사용할 서명 처리기
   * **2(하위 필터):** 서명 시 사용할 수 있는 인코딩을 나타내는 이름 배열
   * **3 (V)**: 서명 필드에 서명하는 데 사용할 서명 처리기의 최소 버전 번호
   * **4(사유):** 문서 서명의 가능한 이유를 지정하는 문자열 배열
   * **5(PDFLegalWarnings):** 가능한 법적 입증인을 지정하는 문자열 배열

* **법적 증거 자료**: 문서가 인증되면 문서의 내용을 모호하게 만들거나 오해할 수 있도록 특정 유형의 컨텐츠를 자동으로 스캔합니다. 예를 들어 주석을 사용하면 인증되는 텍스트를 이해하는 데 중요한 텍스트를 가릴 수 있습니다. 스캔 프로세스는 이 유형의 컨텐츠가 있음을 나타내는 경고를 생성합니다. 또한 경고를 생성했을 수 있는 컨텐츠에 대한 추가 설명을 제공합니다.
* **권한**: 서명을 무효화하지 않고 PDF 문서에서 사용할 수 있는 권한을 지정합니다.
* **이유**: 이 문서에 서명해야 하는 이유를 지정합니다.
* **타임스탬프**: 타임스탬프 옵션을 지정합니다. 예를 들어 사용되는 타임스탬프 서버의 URL을 설정할 수 있습니다.
* **버전**: 서명 필드에 서명하는 데 사용할 서명 처리기의 최소 버전 번호를 지정합니다.

**서명 필드 수정**

서명 서비스 클라이언트를 만들고, 수정할 서명 필드가 포함된 PDF 문서를 검색하고, 사전 값을 설정한 후 서명 서비스에 서명 필드를 수정하도록 지시할 수 있습니다. 그런 다음 서명 서비스는 수정된 서명 필드가 포함된 PDF 문서를 반환합니다. 원본 PDF 문서는 영향을 받지 않습니다.

**PDF 문서를 PDF 파일로 저장**

수정된 서명 필드가 포함된 PDF 문서를 PDF 파일로 저장하여 사용자가 Acrobat 또는 Adobe Reader에서 열 수 있습니다.

**참고 항목**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[서명 서비스 API 빠른 시작](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

[PDF 문서에 디지털 서명](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Java API를 사용하여 서명 필드 수정 {#modify-signature-fields-using-the-java-api}

서명 API(Java)를 사용하여 서명 필드를 수정합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-signatures-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. 서명 클라이언트 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 개체를 `SignatureServiceClient` 만들고 개체를 `ServiceClientFactory` 전달합니다.

1. 수정할 서명 필드가 포함된 PDF 문서 가져오기

   * 생성자를 사용하여 수정할 서명 필드가 포함된 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만들고 PDF 문서의 위치를 지정하는 문자열 값을 전달합니다.
   * 생성자를 사용하여 개체를 `com.adobe.idp.Document` 만들고 개체를 `java.io.FileInputStream` 전달합니다.

1. 사전 값 설정

   * 생성자를 사용하여 `PDFSignatureFieldProperties` 개체를 만듭니다. 개체가 서명 필드 잠금 사전 및 시드 값 사전 정보를 저장합니다. `PDFSignatureFieldProperties`
   * 생성자를 사용하여 `PDFSeedValueOptionSpec` 개체를 만듭니다. 이 개체를 사용하면 시드 값 사전 값을 설정할 수 있습니다.
   * 개체의 메서드를 호출하고 열거형 값을 전달하여 PDF 문서 `PDFSeedValueOptionSpec` 에 대한 변경 `setMdpValue` 을 `MDPPermissions.NoChanges` 허용하지 않습니다.
   * 생성자를 사용하여 `FieldMDPOptionSpec` 개체를 만듭니다. 이 개체를 사용하면 서명 필드 잠금 사전 값을 설정할 수 있습니다.
   * 개체의 메서드를 호출하고 열거형 값을 전달하여 PDF 문서의 모든 필드 `FieldMDPOptionSpec` 를 `setMdpValue` `FieldMDPAction.ALL` 잠급니다.
   * 개체의 메서드를 호출하고 개체를 전달하여 시드 값 사전 정보 `PDFSignatureFieldProperties` 를 `setSeedValue` `PDFSeedValueOptionSpec` 설정합니다.
   * 개체의 메서드를 호출하고 개체를 전달하여 서명 필드 잠금 사전 정보 `PDFSignatureFieldProperties`를 `setFieldMDP` `FieldMDPOptionSpec` 설정합니다.

   >[!NOTE]
   >
   >설정할 수 있는 모든 시드 값 사전 값을 보려면 `PDFSeedValueOptionSpec` 클래스 참조를 참조하십시오. (AEM Forms [API 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

1. 서명 필드 수정

   객체의 메서드를 호출하고 다음 값을 전달하여 `SignatureServiceClient` 서명 `modifySignatureField` 필드를 수정합니다.

   * 수정할 서명 필드가 포함된 PDF 문서를 저장하는 `com.adobe.idp.Document` 개체
   * 서명 필드의 이름을 지정하는 문자열 값
   * 서명 필드 잠금 사전 및 시드 값 사전 정보를 저장하는 `PDFSignatureFieldProperties` 개체

   이 `modifySignatureField` 메서드는 수정된 서명 필드가 포함된 PDF 문서를 저장하는 `com.adobe.idp.Document` 개체를 반환합니다.

1. PDF 문서를 PDF 파일로 저장

   * 객체를 만들고 파일 이름 확장자가 .pdf인지 확인합니다. `java.io.File`
   * 개체의 `com.adobe.idp.Document` 메서드를 `copyToFile` 호출하여 `com.adobe.idp.Document` 개체의 내용을 파일에 복사합니다. 메서드가 반환한 `com.adobe.idp.Document` 개체를 `modifySignatureField` 사용해야 합니다.

### 웹 서비스 API를 사용하여 서명 필드 수정 {#modify-signature-fields-using-the-web-service-api}

서명 API(웹 서비스)를 사용하여 서명 필드를 수정합니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Forms `localhost` 를 호스팅하는 서버의 IP 주소로 대체합니다.

1. 서명 클라이언트 만들기

   * 기본 생성자를 사용하여 `SignatureServiceClient` 개체를 만듭니다.
   * 생성자를 사용하여 `SignatureServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/SignatureService?WSDL`). 속성을 사용할 필요는 `lc_version` 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * 필드의 값을 `System.ServiceModel.BasicHttpBinding` 가져와 개체를 `SignatureServiceClient.Endpoint.Binding` 만듭니다. 반환 값을 다음으로 캐스팅합니다 `BasicHttpBinding`.
   * 개체 `System.ServiceModel.BasicHttpBinding` 필드를 (으)로 `MessageEncoding` 설정합니다 `WSMessageEncoding.Mtom`. 이 값을 사용하면 MTOM이 사용됩니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM 양식 사용자 이름을 지정합니다 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 해당 암호 값을 필드에 지정합니다 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 필드에 상수 값 `HttpClientCredentialType.Basic` 을 지정합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 필드에 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly` 을 지정합니다 `BasicHttpBindingSecurity.Security.Mode`.

1. 수정할 서명 필드가 포함된 PDF 문서 가져오기

   * 생성자를 사용하여 `BLOB` 개체를 만듭니다. 이 `BLOB` 개체는 수정할 서명 필드가 포함된 PDF 문서를 저장하는 데 사용됩니다.
   * 생성자를 호출하고 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * 개체의 내용을 저장하는 바이트 배열을 `System.IO.FileStream` 만듭니다. 개체의 속성을 가져와 바이트 배열의 크기를 결정할 수 `System.IO.FileStream` `Length` 있습니다.
   * 개체의 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열 `System.IO.FileStream` `Read` 을 스트림 데이터로 채웁니다.
   * 바이트 배열의 컨텐츠에 해당 `BLOB``MTOM` 속성을 할당하여 개체를 채웁니다.

1. 사전 값 설정

   * 생성자를 사용하여 `PDFSignatureFieldProperties` 개체를 만듭니다. 이 개체는 서명 필드 잠금 사전 및 시드 값 사전 정보를 저장합니다.
   * 생성자를 사용하여 `PDFSeedValueOptionSpec` 개체를 만듭니다. 이 개체를 사용하면 시드 값 사전 값을 설정할 수 있습니다.
   * 개체의 데이터 멤버에 열거형 값을 할당하여 PDF 문서 `MDPPermissions.NoChanges` 를 변경할 수 `PDFSeedValueOptionSpec` 없습니다 `mdpValue` .
   * 생성자를 사용하여 `FieldMDPOptionSpec` 개체를 만듭니다. 이 개체를 사용하면 서명 필드 잠금 사전 값을 설정할 수 있습니다.
   * 개체의 데이터 멤버에 열거형 값을 할당하여 PDF 문서의 모든 필드 `FieldMDPAction.ALL` 를 `FieldMDPOptionSpec` `mdpValue` 잠급니다.
   * 개체의 데이터 멤버에 개체를 할당하여 시드 값 사전 정보 `PDFSeedValueOptionSpec` 를 `PDFSignatureFieldProperties` `seedValue` 설정합니다.
   * 개체의 데이터 멤버에 개체를 할당하여 서명 필드 잠금 사전 정보 `FieldMDPOptionSpec` 를 `PDFSignatureFieldProperties` `fieldMDP` 설정합니다.

   >[!NOTE]
   >
   >설정할 수 있는 모든 시드 값 사전 값을 보려면 `PDFSeedValueOptionSpec` 클래스 참조를 참조하십시오. (AEM Forms [API 참조 참조 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)).

1. 서명 필드 수정

   객체의 메서드를 호출하고 다음 값을 전달하여 `SignatureServiceClient` 서명 `modifySignatureField` 필드를 수정합니다.

   * 수정할 서명 필드가 포함된 PDF 문서를 저장하는 `BLOB` 개체
   * 서명 필드의 이름을 지정하는 문자열 값
   * 서명 필드 잠금 사전 및 시드 값 사전 정보를 저장하는 `PDFSignatureFieldProperties` 개체

   이 `modifySignatureField` 메서드는 수정된 서명 필드가 포함된 PDF 문서를 저장하는 `BLOB` 개체를 반환합니다.

1. PDF 문서를 PDF 파일로 저장

   * 생성자를 호출하고 서명 필드가 포함될 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * 메서드가 반환하는 개체의 내용을 저장하는 바이트 배열 `BLOB` 을 `addSignatureField` 만듭니다. 개체 데이터 멤버의 값을 가져와 바이트 배열 `BLOB` 을 `MTOM` 채웁니다.
   * 생성자를 호출하고 개체를 전달하여 `System.IO.BinaryWriter` 개체를 `System.IO.FileStream` 만듭니다.
   * 개체의 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 PDF 파일 `System.IO.BinaryWriter` `Write` 에 씁니다.

**참고 항목**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## PDF 문서에 디지털 서명 {#digitally-signing-pdf-documents}

디지털 서명을 PDF 문서에 적용하여 높은 수준의 보안을 제공할 수 있습니다. 자필 서명과 같은 디지털 서명은 서명자가 자신을 식별하고 문서에 대해 진술하는 수단을 제공합니다. 문서에 디지털 서명을 하는 데 사용되는 기술은 서명자와 수신자 모두 서명된 문서를 명확하게 파악하고 서명된 이후 문서가 변경되지 않았음을 보증하는 데 도움이 됩니다.

PDF 문서는 공개 키 기술을 통해 서명됩니다. 서명자에게는 두 가지 키가 있습니다. 공개 키와 개인 키. 개인 키는 서명 시 사용할 수 있어야 하는 사용자의 자격 증명에 저장됩니다. 공개 키는 서명을 검증하기 위해 수신자가 사용할 수 있어야 하는 사용자의 인증서에 저장됩니다. 해지된 인증서에 대한 정보는 CA(인증 기관)가 배포한 CRL(인증서 해지 목록) 및 OCSP(온라인 인증서 상태 프로토콜) 응답에서 찾을 수 있습니다. 서명 시간은 타임스탬프 기관이라고 하는 신뢰할 수 있는 소스에서 얻을 수 있습니다.

>[!NOTE]
>
>PDF 문서에 디지털 서명을 하려면 AEM Forms에 인증서를 추가해야 합니다. 관리 콘솔을 사용하거나 Trust Manager API를 사용하여 프로그래밍 방식으로 인증서를 추가합니다. (Trust [Manager API를 사용하여 자격 증명 가져오기를 참조하십시오](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

PDF 문서에 디지털 서명을 할 수 있습니다. PDF 문서에 디지털 서명을 하는 경우 AEM Forms에 있는 보안 자격 증명을 참조해야 합니다. 자격 증명은 서명하는 데 사용되는 개인 키입니다.

서명 서비스는 PDF 문서에 서명할 때 다음 단계를 수행합니다.

1. 서명 서비스는 요청에 지정된 별칭을 전달하여 Truststore에서 자격 증명을 검색합니다.
1. Truststore가 지정된 자격 증명을 검색합니다.
1. 이 자격 증명은 서명 서비스로 반환되며 문서에 서명하는 데 사용됩니다. 또한 자격 증명은 향후 요청에 대해 별칭에 캐시됩니다.

보안 자격 증명 처리에 대한 자세한 내용은 응용 프로그램 서버에 대한 *AEM Forms* 설치 및 배포 안내서를 참조하십시오.

>[!NOTE]
>
>문서 서명과 인증에는 차이가 있습니다. (PDF [문서 인증을 참조하십시오](digitally-signing-certifying-documents.md#certifying-pdf-documents).)

>[!NOTE]
>
>일부 PDF 문서에서 서명을 지원하는 것은 아닙니다. 서명 서비스 및 디지털 서명 문서에 대한 자세한 내용은 AEM Forms에 대한 [서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>서명 서비스는 문서 인증과 같은 작업에 대한 입력으로 포함된 PDF 데이터가 포함된 XDP 파일을 지원하지 않습니다. 이 작업을 수행하면 서명 서비스가 게시됩니다 `PDFOperationException`. 이 문제를 해결하려면 PDF 유틸리티 서비스를 사용하여 XDP 파일을 PDF 파일로 변환한 다음 변환된 PDF 파일을 서명 서비스 작업으로 전달합니다. (PDF 유틸리티 [작업을 참조하십시오](/help/forms/developing/pdf-utilities.md#working-with-pdf-utilities).)

**nCipher nShield HSM 자격 증명**

Cipher NShield HSM 자격 증명을 사용하여 PDF 문서에 서명하거나 인증할 때 AEM Forms이 배포된 J2EE 응용 프로그램 서버를 다시 시작할 때까지 새 자격 증명을 사용할 수 없습니다. 그러나 구성 값을 설정하면 J2EE 응용 프로그램 서버를 다시 시작하지 않고 서명 또는 인증 작업이 작동합니다.

cknfastrc 파일에 /opt/nfast/cknfastrc(또는 c:\nfast\cknfastrc)에 있는 다음 구성 값을 추가할 수 있습니다.

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

이 구성 값을 cknfastrc 파일에 추가하면 J2EE 응용 프로그램 서버를 다시 시작하지 않고 새 자격 증명을 사용할 수 있습니다.

**서명을 신뢰할 수 없음**

동일한 PDF 문서를 인증하고 서명할 때 인증 서명을 신뢰할 수 없으면 Acrobat 또는 Adobe Reader에서 PDF 문서를 열 때 첫 번째 서명에 노란색 삼각형이 나타납니다. 이러한 상황을 방지하려면 인증 서명을 신뢰할 수 있어야 합니다.

**XFA 기반 양식인 문서 서명**

Signature service API를 사용하여 XFA 기반 양식에 서명하려고 하면 Acrobat에 `View` `Signed` `Version` 있는 데이터에서 데이터가 누락될 수 있습니다. 예를 들어 다음 워크플로우를 고려해 보십시오.

* Designer를 사용하여 만든 XDP 파일을 사용하면 서명 필드와 양식 데이터가 포함된 XML 데이터가 포함된 양식 디자인을 병합합니다. Forms 서비스를 사용하여 대화형 PDF 문서를 생성합니다.
* Signature service API를 사용하여 PDF 문서에 서명합니다.

### 단계 요약 {#summary_of_steps-3}

PDF 문서에 디지털 서명을 하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일 포함
1. 서명 서비스 클라이언트를 만듭니다.
1. PDF 문서에 서명
1. PDF 문서에 서명
1. 서명된 PDF 문서를 PDF 파일로 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

다음 JAR 파일을 프로젝트의 클래스 경로에 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(AEM Forms이 JBoss에 배포된 경우 필요)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필요)

**서명 클라이언트 만들기**

서명 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 서명 서비스 클라이언트를 만들어야 합니다.

**PDF 문서에 서명 받기**

PDF 문서에 서명하려면 서명 필드가 포함된 PDF 문서를 받아야 합니다. PDF 문서에 서명 필드가 없으면 서명할 수 없습니다. 서명 필드는 디자이너를 사용하거나 프로그래밍 방식으로 추가할 수 있습니다.

**PDF 문서 서명**

PDF 문서에 서명할 때 서명 서비스에서 사용하는 런타임 옵션을 설정할 수 있습니다. 다음 옵션을 설정할 수 있습니다.

* 모양 옵션
* 취소 확인
* 타임스탬프 값

객체를 사용하여 모양 옵션을 `PDFSignatureAppearanceOptionSpec` 설정합니다. 예를 들어, 객체의 메서드를 호출하고 전달하여 서명 내에 `PDFSignatureAppearanceOptionSpec` 날짜를 표시할 수 `setShowDate` 있습니다 `true`.

PDF 문서에 디지털 서명하는 데 사용되는 인증서가 해지되었는지 여부를 결정하는 취소 검사를 수행할지 여부를 지정할 수도 있습니다. 해지 검사를 수행하려면 다음 값 중 하나를 지정할 수 있습니다.

* **확인 안 함**: 취소 확인을 수행하지 마십시오.
* **최상의 노력**: 항상 체인에 있는 모든 인증서의 취소를 확인하십시오. 확인 시 문제가 발생하면 해제가 유효하다고 가정합니다. 오류가 발생하면 인증서가 해지되지 않는다고 가정합니다.
* **CheckIfAvailable:** 해지 정보를 사용할 수 있는 경우 체인에 있는 모든 인증서의 취소를 확인하십시오. 확인 시 문제가 발생하면 해제가 잘못된 것으로 간주됩니다. 오류가 발생하면 인증서가 취소되고 유효하지 않다고 가정합니다. 기본값은 기본값입니다.
* **AlwaysCheck**: 체인에 있는 모든 인증서의 취소를 확인하십시오. 인증서에 해지 정보가 없는 경우 취소는 잘못된 것으로 간주됩니다.

인증서에 대한 해지 검사를 수행하려면 개체를 사용하여 CRL(인증서 해지 목록) 서버의 URL을 지정할 수 `CRLOptionSpec` 있습니다. 그러나 취소 확인을 수행하고 CRL 서버에 대한 URL을 지정하지 않을 경우 서명 서비스는 인증서에서 URL을 얻습니다.

CRL 서버를 사용하는 대신 해지 확인을 수행할 때 OCSP(온라인 인증서 상태 프로토콜) 서버를 사용할 수 있습니다. 일반적으로 CRL 서버가 아닌 OCSP 서버를 사용하는 경우 해지 검사가 더 빨리 수행됩니다. (https://tools.ietf.org/html/rfc2560에서 &quot;온라인 인증서 상태 프로토콜&quot;을 [참조하십시오](https://tools.ietf.org/html/rfc2560).)

서명 서비스가 Adobe 응용 프로그램 및 서비스를 사용하여 사용하는 CRL 및 OCSP 서버 순서를 설정할 수 있습니다. 예를 들어, Adobe 응용 프로그램 및 서비스에서 OCSP 서버가 먼저 설정된 경우 OCSP 서버가 선택된 후 CRL 서버가 선택됩니다. (AAC 도움말의 &quot;Trust Store를 사용하여 인증서 및 자격 증명 관리&quot;를 참조하십시오.)

취소 확인을 수행하지 않도록 지정한 경우 서명 서비스는 문서에 서명하거나 인증하는 데 사용된 인증서가 해지되었는지 확인하지 않습니다. 즉, CRL 및 OCSP 서버 정보는 무시됩니다.

>[!NOTE]
>
>인증서에 CRL 또는 OCSP 서버가 지정되어 있지만, `CRLOptionSpec` 및 개체를 사용하여 인증서에 지정된 URL을 재정의할 수 `OCSPOptionSpec` 있습니다. 예를 들어, CRL 서버를 재정의하려면 `CRLOptionSpec` 객체의 메서드를 호출할 수 `setLocalURI` 있습니다.

타임스탬프는 서명된 문서 또는 인증된 문서가 수정된 시간을 추적하는 프로세스를 의미합니다. 문서에 서명이 완료되면 문서 소유자가 문서를 수정할 수 없습니다. 타임스탬프를 통해 서명된 문서 또는 인증된 문서의 유효성을 강화할 수 있습니다. 개체를 사용하여 타임스탬프 옵션을 설정할 수 `TSPOptionSpec` 있습니다. 예를 들어 TSP(타임스탬프 공급자) 서버의 URL을 지정할 수 있습니다.

>[!NOTE]
>
>Java 및 웹 서비스에서 섹션 및 해당 빠른 시작을 안내하면 취소 검사가 사용됩니다. CRL 또는 OCSP 서버 정보가 지정되지 않았으므로 PDF 문서에 디지털 서명하는 데 사용되는 인증서에서 서버 정보를 얻습니다.

PDF 문서에 성공적으로 서명하려면 디지털 서명이 포함되어 있는 서명 필드의 정규화된 이름을 지정할 수 있습니다(예: `form1[0].#subform[1].SignatureField3[3]`). XFA 양식 필드를 사용할 때 서명 필드의 부분 이름도 사용할 수 있습니다. `SignatureField3[3]`.

또한 PDF 문서에 디지털 서명을 하려면 보안 자격 증명을 참조해야 합니다. 보안 자격 증명을 참조하려면 별칭을 지정합니다. 별칭은 PKCS#12 파일(확장명이 .pfx) 또는 HSM(하드웨어 보안 모듈)에 있을 수 있는 실제 자격 증명을 참조합니다. 보안 자격 증명에 대한 자세한 내용은 응용 프로그램 서버에 대한 *AEM Forms* 설치 및 배포 안내서를 참조하십시오.

**서명된 PDF 문서 저장**

서명 서비스가 PDF 문서에 디지털 서명을 하면 PDF 파일로 저장하여 사용자가 Acrobat 또는 Adobe Reader에서 열 수 있습니다.

**참고 항목**

[Java API를 사용하여 PDF 문서에 디지털 서명](digitally-signing-certifying-documents.md#digitally-sign-pdf-documents-using-the-java-api)

[웹 서비스 API를 사용하여 PDF 문서에 디지털 서명](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[서명 필드 추가](digitally-signing-certifying-documents.md#adding-signature-fields)

[서명 필드 이름 검색](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

### Java API를 사용하여 PDF 문서에 디지털 서명 {#digitally-sign-pdf-documents-using-the-java-api}

서명 API(Java)를 사용하여 PDF 문서에 디지털 서명:

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-signatures-client.jar 등의 클라이언트 JAR 파일을 포함합니다.

1. 서명 클라이언트 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 개체를 `SignatureServiceClient` 만들고 개체를 `ServiceClientFactory` 전달합니다.

1. PDF 문서에 서명 받기

   * 생성자를 사용하여 디지털 서명할 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만들고 PDF 문서의 위치를 지정하는 문자열 값을 전달합니다.
   * 생성자를 사용하여 개체를 `com.adobe.idp.Document` 만들고 개체를 `java.io.FileInputStream` 전달합니다.

1. PDF 문서 서명

   개체의 방법을 호출하고 다음 값을 전달하여 `SignatureServiceClient` PDF 문서에 `sign` 서명합니다.

   * 서명할 PDF 문서를 나타내는 `com.adobe.idp.Document` 개체입니다.
   * 디지털 서명이 포함될 서명 필드의 이름을 나타내는 문자열 값입니다.
   * PDF 문서에 디지털 서명하는 데 사용되는 자격 증명을 나타내는 `Credential` 개체입니다. 개체의 정적 `Credential` `Credential` `getInstance` 메서드를 호출하고 보안 자격 증명에 해당하는 별칭 값을 지정하는 문자열 값을 전달하여 개체를 만듭니다.
   * PDF 문서를 소화하는 데 사용할 해시 알고리즘을 나타내는 정적 데이터 멤버를 지정하는 `HashAlgorithm` 객체입니다. 예를 들어 SHA1 알고리즘 `HashAlgorithm.SHA1` 을 사용하도록 지정할 수 있습니다.
   * PDF 문서가 디지털 서명된 이유를 나타내는 문자열 값입니다.
   * 서명자의 연락처 정보를 나타내는 문자열 값입니다.
   * 디지털 서명의 모양을 제어하는 `PDFSignatureAppearanceOptions` 개체입니다. 예를 들어 이 개체를 사용하여 디지털 서명에 사용자 정의 로고를 추가할 수 있습니다.
   * 서명자의 인증서에 대한 취소 확인을 수행할지 여부를 지정하는 `java.lang.Boolean` 개체
   * OCSP(Online Certificate Status Protocol) 지원에 대한 환경 설정을 저장하는 `OCSPOptionSpec` 개체입니다. 해지 검사가 수행되지 않으면 이 매개 변수가 사용되지 않으며 지정할 수 있습니다 `null`.
   * CRL(인증서 해지 목록) 기본 설정을 저장하는 `CRLPreferences` 객체입니다. 해지 검사가 수행되지 않으면 이 매개 변수가 사용되지 않으며 지정할 수 있습니다 `null`.
   * TSP(타임스탬프 공급자) 지원에 대한 환경 설정을 저장하는 `TSPPreferences` 개체입니다. 이 매개 변수는 선택 사항이며 사용할 수 있습니다 `null`. 자세한 내용은 [AEM Forms API 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

   이 `sign` 메서드는 서명된 PDF 문서를 나타내는 `com.adobe.idp.Document` 개체를 반환합니다.

1. 서명된 PDF 문서 저장

   * 개체를 만들고 파일 확장자가 .pdf인지 확인합니다. `java.io.File`
   * 개체의 `com.adobe.idp.Document` 메서드를 `copyToFile` 호출하고 전달하여 개체 내용 `java.io.File`을 파일에 `Document` 복사합니다. 메서드에서 반환된 `com.adobe.idp.Document` 개체를 사용해야 `sign` 합니다.

**참고 항목**

[PDF 문서에 디지털 서명](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[빠른 시작(SOAP 모드): Java API를 사용하여 PDF 문서에 디지털 서명](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 PDF 문서에 디지털 서명 {#digitally-signing-pdf-documents-using-the-web-service-api}

서명 API(웹 서비스)를 사용하여 PDF 문서에 디지털 서명을 하려면

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Forms `localhost` 를 호스팅하는 서버의 IP 주소로 대체합니다.

1. 서명 클라이언트 만들기

   * 기본 생성자를 사용하여 `SignatureServiceClient` 개체를 만듭니다.
   * 생성자를 사용하여 `SignatureServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/SignatureService?WSDL`). 속성을 사용할 필요는 `lc_version` 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * 필드의 값을 `System.ServiceModel.BasicHttpBinding` 가져와 개체를 `SignatureServiceClient.Endpoint.Binding` 만듭니다. 반환 값을 다음으로 캐스팅합니다 `BasicHttpBinding`.
   * 개체 `System.ServiceModel.BasicHttpBinding` 필드를 (으)로 `MessageEncoding` 설정합니다 `WSMessageEncoding.Mtom`. 이 값을 사용하면 MTOM이 사용됩니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM 양식 사용자 이름을 지정합니다 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 해당 암호 값을 필드에 지정합니다 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 필드에 상수 값 `HttpClientCredentialType.Basic` 을 지정합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 필드에 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly` 을 지정합니다 `BasicHttpBindingSecurity.Security.Mode`.

1. PDF 문서에 서명 받기

   * 생성자를 사용하여 `BLOB` 개체를 만듭니다. 이 `BLOB` 개체는 서명된 PDF 문서를 저장하는 데 사용됩니다.
   * 생성자를 호출하고 서명할 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * 개체의 내용을 저장하는 바이트 배열을 `System.IO.FileStream` 만듭니다. 개체의 속성을 가져와 바이트 배열의 크기를 결정할 수 `System.IO.FileStream` `Length` 있습니다.
   * 개체의 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열 `System.IO.FileStream` `Read` 을 스트림 데이터로 채웁니다.
   * 바이트 배열의 컨텐츠에 해당 `BLOB``MTOM` 속성을 할당하여 개체를 채웁니다.

1. PDF 문서 서명

   개체의 방법을 호출하고 다음 값을 전달하여 `SignatureServiceClient` PDF 문서에 `sign` 서명합니다.

   * 서명할 PDF 문서를 나타내는 `BLOB` 개체입니다.
   * 디지털 서명이 포함될 서명 필드의 이름을 나타내는 문자열 값입니다.
   * PDF 문서에 디지털 서명하는 데 사용되는 자격 증명을 나타내는 `Credential` 개체입니다. 생성자를 사용하여 `Credential` 개체를 만들고 개체의 속성에 값을 할당하여 `Credential` 별칭을 `alias` 지정합니다.
   * PDF 문서를 소화하는 데 사용할 해시 알고리즘을 나타내는 정적 데이터 멤버를 지정하는 `HashAlgorithm` 객체입니다. 예를 들어 SHA1 알고리즘 `HashAlgorithm.SHA1` 을 사용하도록 지정할 수 있습니다.
   * 해시 알고리즘의 사용 여부를 지정하는 부울 값.
   * PDF 문서가 디지털 서명된 이유를 나타내는 문자열 값입니다.
   * 서명자의 위치를 나타내는 문자열 값.
   * 서명자의 연락처 정보를 나타내는 문자열 값입니다.
   * 디지털 서명의 모양을 제어하는 `PDFSignatureAppearanceOptions` 개체입니다. 예를 들어 이 개체를 사용하여 디지털 서명에 사용자 정의 로고를 추가할 수 있습니다.
   * 서명자의 인증서에 대한 취소 확인을 수행할지 여부를 지정하는 `System.Boolean` 개체 이 해지 검사가 완료되면 서명에 포함됩니다. The default is `false`.
   * OCSP(Online Certificate Status Protocol) 지원에 대한 환경 설정을 저장하는 `OCSPOptionSpec` 개체입니다. 해지 검사가 수행되지 않으면 이 매개 변수가 사용되지 않으며 지정할 수 있습니다 `null`. 이 개체에 대한 자세한 내용은 [AEM Forms API 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * CRL(인증서 해지 목록) 기본 설정을 저장하는 `CRLPreferences` 객체입니다. 해지 검사가 수행되지 않으면 이 매개 변수가 사용되지 않으며 지정할 수 있습니다 `null`.
   * TSP(타임스탬프 공급자) 지원에 대한 환경 설정을 저장하는 `TSPPreferences` 개체입니다. 이 매개 변수는 선택 사항이며 사용할 수 있습니다 `null`.

   이 `sign` 메서드는 서명된 PDF 문서를 나타내는 `BLOB` 개체를 반환합니다.

1. 서명된 PDF 문서 저장

   * 생성자를 호출하여 `System.IO.FileStream` 개체를 만듭니다. 서명된 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 메서드에서 반환된 개체의 내용을 저장하는 바이트 배열을 `BLOB` `sign` 만듭니다. 개체 데이터 멤버의 값을 가져와 바이트 배열 `BLOB` 을 `MTOM` 채웁니다.
   * 생성자를 호출하고 개체를 전달하여 `System.IO.BinaryWriter` 개체를 `System.IO.FileStream` 만듭니다.
   * 개체의 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 PDF 파일 `System.IO.BinaryWriter` `Write` 에 씁니다.

**참고 항목**

[PDF 문서에 디지털 서명](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 인터랙티브한 양식에 디지털 서명 {#digitally-signing-interactive-forms}

Forms 서비스가 만드는 대화형 양식에 서명할 수 있습니다. 예를 들어 다음 워크플로우를 고려해 보십시오.

* Designer를 사용하여 만든 XFA 기반 PDF 양식과 Forms 서비스를 사용하여 XML 문서에 있는 양식 데이터를 병합합니다. Forms 서버가 대화형 양식을 렌더링합니다.
* Signature service API를 사용하여 대화형 양식에 서명합니다.

디지털 방식으로 서명된 인터랙티브한 PDF 양식을 통해 XFA 양식을 기반으로 하는 PDF 양식에 서명할 때는 PDF 파일을 Adobe 정적 PDF 양식으로 저장해야 합니다. Adobe Dynamic PDF 양식으로 저장된 PDF 양식에 서명하려고 하면 예외가 발생합니다. 양식 서비스에서 반환되는 양식에 서명하고 있으므로 양식에 서명 필드가 포함되어 있는지 확인하십시오.

>[!NOTE]
>
>대화형 양식에 디지털 서명을 하려면 먼저 AEM Forms에 인증서를 추가해야 합니다. 관리 콘솔을 사용하거나 Trust Manager API를 사용하여 프로그래밍 방식으로 인증서를 추가합니다. (Trust [Manager API를 사용하여 자격 증명 가져오기를 참조하십시오](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

Forms Service API를 사용할 때는 `GenerateServerAppearance` 런타임 옵션을 로 설정합니다 `true`. 이 런타임 옵션을 사용하면 Acrobat 또는 Adobe Reader에서 파일을 열 때 서버에서 생성된 양식의 모양이 유효하게 유지됩니다. Forms API를 사용하여 서명할 대화형 양식을 생성할 때는 이 런타임 옵션을 설정하는 것이 좋습니다.

>[!NOTE]
>
>대화형 양식에 디지털 서명을 하기 전에 PDF 문서 서명에 익숙한 것이 좋습니다. (PDF 문서 [디지털 서명 참조](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents))

### 단계 요약 {#summary_of_steps-4}

Forms 서비스가 반환하는 대화형 양식에 디지털 서명을 하려면 다음 작업을 수행합니다.

1. 프로젝트 파일 포함
1. 양식 및 서명 클라이언트 만들기
1. Forms 서비스를 사용하여 대화형 양식을 얻습니다.
1. 인터랙티브한 양식에 서명
1. 서명된 PDF 문서를 PDF 파일로 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

다음 JAR 파일을 프로젝트의 클래스 경로에 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-forms-client.jar
* adobe-utilities.jar(AEM Forms이 JBoss에 배포된 경우 필요)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필요)

이러한 JAR 파일의 위치에 대한 자세한 내용은 AEM Forms Java 라이브러리 파일 [포함을 참조하십시오](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**양식 및 서명 클라이언트 만들기**

이 워크플로우는 양식 및 서명 서비스를 모두 불러오므로 양식 서비스 클라이언트와 서명 서비스 클라이언트를 모두 만듭니다.

**Forms 서비스를 사용하여 대화형 양식 얻기**

양식 서비스를 사용하여 서명할 인터랙티브한 PDF 양식을 얻을 수 있습니다. AEM Forms의 경우 렌더링할 양식이 포함된 Forms 서비스에 `com.adobe.idp.Document` 개체를 전달할 수 있습니다. 이 메서드의 이름은 입니다 `renderPDFForm2`. 이 메서드는 서명할 양식이 포함된 `com.adobe.idp.Document` 개체를 반환합니다. 이 `com.adobe.idp.Document` 인스턴스를 서명 서비스에 전달할 수 있습니다.

마찬가지로, 웹 서비스를 사용하는 경우 Forms 서비스가 Signature 서비스로 반환되는 `BLOB` 인스턴스를 전달할 수 있습니다.

>[!NOTE]
>
>[대화형 양식 디지털 서명] 섹션과 연관된 빠른 시작을 통해 이 방법을 `renderPDFForm2` 호출합니다.

**인터랙티브한 양식 서명**

PDF 문서에 서명할 때 서명 서비스가 사용하는 런타임 옵션을 설정할 수 있습니다. 다음 옵션을 설정할 수 있습니다.

* 모양 옵션
* 취소 확인
* 타임스탬프 값

객체를 사용하여 모양 옵션을 `PDFSignatureAppearanceOptionSpec` 설정합니다. 예를 들어, 객체의 메서드를 호출하고 전달하여 서명 내에 `PDFSignatureAppearanceOptionSpec` 날짜를 표시할 수 `setShowDate` 있습니다 `true`.

**서명된 PDF 문서 저장**

서명 서비스가 PDF 문서에 디지털 서명을 하면 PDF 파일로 저장할 수 있습니다. PDF 파일은 Acrobat 또는 Adobe Reader에서 열 수 있습니다.

**참고 항목**

[Java API를 사용하여 대화형 양식에 디지털 서명](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-java-api)

[웹 서비스 API를 사용하여 대화형 양식에 디지털 서명](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF 문서에 디지털 서명](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[대화형 PDF forms 렌더링](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)

### Java API를 사용하여 대화형 양식에 디지털 서명 {#digitally-sign-an-interactive-form-using-the-java-api}

양식 및 서명 API(Java)를 사용하여 대화형 양식에 디지털 서명을 합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-signatures-client.jar 및 adobe-forms-client.jar 등의 클라이언트 JAR 파일을 포함합니다.

1. 양식 및 서명 클라이언트 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 개체를 `SignatureServiceClient` 만들고 개체를 `ServiceClientFactory` 전달합니다.
   * 생성자를 사용하여 개체를 `FormsServiceClient` 만들고 개체를 `ServiceClientFactory` 전달합니다.

1. Forms 서비스를 사용하여 대화형 양식 얻기

   * 생성자를 사용하여 Forms 서비스에 전달할 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만듭니다. PDF 문서의 위치를 지정하는 문자열 값을 전달합니다.
   * 생성자를 사용하여 개체를 `com.adobe.idp.Document` 만들고 개체를 `java.io.FileInputStream` 전달합니다.
   * 양식 데이터가 포함된 XML 문서를 나타내는 `java.io.FileInputStream` 객체를 만든 후 해당 생성자를 사용하여 Forms 서비스에 전달합니다. XML 파일의 위치를 지정하는 문자열 값을 전달합니다.
   * 생성자를 사용하여 개체를 `com.adobe.idp.Document` 만들고 개체를 `java.io.FileInputStream` 전달합니다.
   * 런타임 옵션을 설정하는 데 사용되는 `PDFFormRenderSpec` 개체를 만듭니다. 개체의 `PDFFormRenderSpec` 메서드를 호출하고 `setGenerateServerAppearance` 전달합니다 `true`.
   * 개체의 `FormsServiceClient` 메서드를 `renderPDFForm2` 호출하고 다음 값을 전달합니다.

      * 렌더링할 PDF 양식이 포함된 `com.adobe.idp.Document` 개체
      * 양식과 병합할 데이터가 포함된 `com.adobe.idp.Document` 개체
      * 런타임 옵션을 저장하는 `PDFFormRenderSpec` 개체입니다.
      * Forms 서비스에 필요한 URI 값이 포함된 `URLSpec` 개체입니다. 이 매개 변수 값 `null` 에 대해 지정할 수 있습니다.
      * 첨부 파일을 저장하는 `java.util.HashMap` 개체입니다. 선택 매개 변수이며 양식에 파일을 첨부하지 않으려는 `null` 경우 지정할 수 있습니다.

      이 `renderPDFForm2` 메서드는 양식 데이터 스트림을 포함하는 `FormsResult` 개체를 반환합니다

   * 개체의 방법을 호출하여 PDF 양식 `FormsResult` 을 `getOutputContent` 검색합니다. 이 메서드는 대화형 양식을 나타내는 `com.adobe.idp.Document` 개체를 반환합니다.


1. 인터랙티브한 양식 서명

   개체의 방법을 호출하고 다음 값을 전달하여 `SignatureServiceClient` PDF 문서에 `sign` 서명합니다.

   * 서명할 PDF 문서를 나타내는 `com.adobe.idp.Document` 개체입니다. 이 개체가 Forms 서비스에서 가져온 `com.adobe.idp.Document` 개체인지 확인합니다.
   * 서명된 서명 필드의 이름을 나타내는 문자열 값입니다.
   * PDF 문서에 디지털 서명하는 데 사용되는 자격 증명을 나타내는 `Credential` 개체입니다. 개체의 정적 `Credential` 메서드를 호출하여 개체를 `Credential` 만듭니다 `getInstance` . 보안 자격 증명에 해당하는 별칭 값을 지정하는 문자열 값을 전달합니다.
   * PDF 문서를 소화하는 데 사용할 해시 알고리즘을 나타내는 정적 데이터 멤버를 지정하는 `HashAlgorithm` 객체입니다. 예를 들어 SHA1 알고리즘 `HashAlgorithm.SHA1` 을 사용하도록 지정할 수 있습니다.
   * PDF 문서가 디지털 서명된 이유를 나타내는 문자열 값입니다.
   * 서명자의 연락처 정보를 나타내는 문자열 값입니다.
   * 디지털 서명의 모양을 제어하는 `PDFSignatureAppearanceOptions` 개체입니다. 예를 들어 이 개체를 사용하여 디지털 서명에 사용자 정의 로고를 추가할 수 있습니다.
   * 서명자의 인증서에 대한 취소 확인을 수행할지 여부를 지정하는 `java.lang.Boolean` 개체
   * OCSP(Online Certificate Status Protocol) 지원에 대한 환경 설정을 저장하는 `OCSPPreferences` 개체입니다. 해지 검사가 수행되지 않으면 이 매개 변수가 사용되지 않으며 지정할 수 있습니다 `null`.
   * CRL(인증서 해지 목록) 기본 설정을 저장하는 `CRLPreferences` 객체입니다. 해지 검사가 수행되지 않으면 이 매개 변수가 사용되지 않으며 지정할 수 있습니다 `null`.
   * TSP(타임스탬프 공급자) 지원에 대한 환경 설정을 저장하는 `TSPPreferences` 개체입니다. 이 매개 변수는 선택 사항이며 사용할 수 있습니다 `null`.

   이 `sign` 메서드는 서명된 PDF 문서를 나타내는 `com.adobe.idp.Document` 개체를 반환합니다.

1. 서명된 PDF 문서 저장

   * 객체를 만들고 파일 이름 확장자가 .pdf인지 확인합니다. `java.io.File`
   * 개체의 `com.adobe.idp.Document` 메서드를 `copyToFile` 호출하고 전달하여 개체 내용 `java.io.File`을 파일에 `Document` 복사합니다. 메서드가 반환한 `com.adobe.idp.Document` 개체를 `sign` 사용해야 합니다.

**참고 항목**

[인터랙티브한 양식에 디지털 서명](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[빠른 시작(SOAP 모드): Java API를 사용하여 PDF 문서에 디지털 서명](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 대화형 양식에 디지털 서명 {#digitally-sign-an-interactive-form-using-the-web-service-api}

양식 및 서명 API(웹 서비스)를 사용하여 대화형 양식에 디지털 서명을 합니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 이 클라이언트 응용 프로그램은 두 개의 AEM Forms 서비스를 호출하므로 두 개의 서비스 참조를 만듭니다. 서명 서비스와 연결된 서비스 참조에 다음 WSDL 정의를 사용하십시오. `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   Forms 서비스와 관련된 서비스 참조에 대해 다음 WSDL 정의를 사용하십시오. `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   데이터 `BLOB` 유형은 두 서비스 참조 모두에서 일반적이므로 데이터 유형을 사용할 때 `BLOB` 데이터 유형을 완전히 분류합니다. 해당 웹 서비스 빠른 시작에서 모든 `BLOB` 인스턴스는 정규화된 인스턴스입니다.

   >[!NOTE]
   >
   >AEM Forms `localhost` 를 호스팅하는 서버의 IP 주소로 대체합니다.

1. 양식 및 서명 클라이언트 만들기

   * 기본 생성자를 사용하여 `SignatureServiceClient` 개체를 만듭니다.
   * 생성자를 사용하여 `SignatureServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/SignatureService?WSDL`). 속성을 사용할 필요는 `lc_version` 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * 필드의 값을 `System.ServiceModel.BasicHttpBinding` 가져와 개체를 `SignatureServiceClient.Endpoint.Binding` 만듭니다. 반환 값을 다음으로 캐스팅합니다 `BasicHttpBinding`.
   * 개체 `System.ServiceModel.BasicHttpBinding` 필드를 (으)로 `MessageEncoding` 설정합니다 `WSMessageEncoding.Mtom`. 이 값을 사용하면 MTOM이 사용됩니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM 양식 사용자 이름을 지정합니다 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 해당 암호 값을 필드에 지정합니다 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 필드에 상수 값 `HttpClientCredentialType.Basic` 을 지정합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 필드에 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly` 을 지정합니다 `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Forms 서비스 클라이언트에 대해 다음 단계를 반복합니다.

1. Forms 서비스를 사용하여 대화형 양식 얻기

   * 생성자를 사용하여 `BLOB` 개체를 만듭니다. 이 `BLOB` 개체는 서명된 PDF 문서를 저장하는 데 사용됩니다.
   * 생성자를 호출하고 서명할 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * 개체의 내용을 저장하는 바이트 배열을 `System.IO.FileStream` 만듭니다. 개체의 속성을 가져와 바이트 배열의 크기를 결정할 수 `System.IO.FileStream` `Length` 있습니다.
   * 개체의 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열 `System.IO.FileStream` `Read` 을 스트림 데이터로 채웁니다.
   * 바이트 배열의 컨텐츠에 해당 `BLOB``MTOM` 속성을 할당하여 개체를 채웁니다.
   * 생성자를 사용하여 `BLOB` 개체를 만듭니다. 이 `BLOB` 개체는 양식 데이터를 저장하는 데 사용됩니다.
   * 생성자를 호출하고 양식 데이터가 포함된 XML 파일의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * 개체의 내용을 저장하는 바이트 배열을 `System.IO.FileStream` 만듭니다. 개체의 속성을 가져와 바이트 배열의 크기를 결정할 수 `System.IO.FileStream` `Length` 있습니다.
   * 개체의 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열 `System.IO.FileStream` `Read` 을 스트림 데이터로 채웁니다.
   * 바이트 배열의 컨텐츠에 해당 `BLOB``MTOM` 속성을 할당하여 개체를 채웁니다.
   * 런타임 옵션을 설정하는 데 사용되는 `PDFFormRenderSpec` 개체를 만듭니다. 객체 `true` 의 `PDFFormRenderSpec` 필드에 값을 `generateServerAppearance` 지정합니다.
   * 개체의 `FormsServiceClient` 메서드를 `renderPDFForm2` 호출하고 다음 값을 전달합니다.

      * 렌더링할 PDF 양식이 포함된 `BLOB` 개체
      * 양식과 병합할 데이터가 포함된 `BLOB` 개체
      * 런타임 옵션을 저장하는 `PDFFormRenderSpec` 개체입니다.
      * Forms 서비스에 필요한 URI 값이 포함된 `URLSpec` 개체입니다. 이 매개 변수 값 `null` 에 대해 지정할 수 있습니다.
      * 첨부 파일을 저장하는 `java.util.HashMap` 개체입니다. 선택 매개 변수이며 양식에 파일을 첨부하지 않으려는 `null` 경우 지정할 수 있습니다.
      * 양식의 페이지 수를 저장하는 데 사용되는 긴 출력 매개 변수입니다.
      * 로케일 값에 사용되는 문자열 출력 매개 변수입니다.
      * 대화형 양식을 저장하는 데 사용되는 출력 매개 변수인 `FormResult` 값입니다.
   * 개체 필드를 호출하여 PDF 양식 `FormsResult` 을 `outputContent` 지웁니다. 이 필드는 대화형 양식을 나타내는 `BLOB` 개체를 저장합니다.


1. 인터랙티브한 양식 서명

   개체의 방법을 호출하고 다음 값을 전달하여 `SignatureServiceClient` PDF 문서에 `sign` 서명합니다.

   * 서명할 PDF 문서를 나타내는 `BLOB` 개체입니다. Forms 서비스에서 반환된 `BLOB` 인스턴스를 사용합니다.
   * 서명된 서명 필드의 이름을 나타내는 문자열 값입니다.
   * PDF 문서에 디지털 서명하는 데 사용되는 자격 증명을 나타내는 `Credential` 개체입니다. 생성자를 사용하여 `Credential` 개체를 만들고 개체의 속성에 값을 할당하여 `Credential` 별칭을 `alias` 지정합니다.
   * PDF 문서를 소화하는 데 사용할 해시 알고리즘을 나타내는 정적 데이터 멤버를 지정하는 `HashAlgorithm` 객체입니다. 예를 들어 SHA1 알고리즘 `HashAlgorithm.SHA1` 을 사용하도록 지정할 수 있습니다.
   * 해시 알고리즘의 사용 여부를 지정하는 부울 값.
   * PDF 문서가 디지털 서명된 이유를 나타내는 문자열 값입니다.
   * 서명자의 위치를 나타내는 문자열 값.
   * 서명자의 연락처 정보를 나타내는 문자열 값입니다.
   * 디지털 서명의 모양을 제어하는 `PDFSignatureAppearanceOptions` 개체입니다. 예를 들어 이 개체를 사용하여 디지털 서명에 사용자 정의 로고를 추가할 수 있습니다.
   * 서명자의 인증서에 대한 취소 확인을 수행할지 여부를 지정하는 `System.Boolean` 개체 이 해지 검사가 완료되면 서명에 포함됩니다. The default is `false`.
   * OCSP(Online Certificate Status Protocol) 지원에 대한 환경 설정을 저장하는 `OCSPPreferences` 개체입니다. 해지 검사가 수행되지 않으면 이 매개 변수가 사용되지 않으며 지정할 수 있습니다 `null`. 이 개체에 대한 자세한 내용은 [AEM Forms API 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * CRL(인증서 해지 목록) 기본 설정을 저장하는 `CRLPreferences` 객체입니다. 해지 검사가 수행되지 않으면 이 매개 변수가 사용되지 않으며 지정할 수 있습니다 `null`.
   * TSP(타임스탬프 공급자) 지원에 대한 환경 설정을 저장하는 `TSPPreferences` 개체입니다. 이 매개 변수는 선택 사항이며 사용할 수 있습니다 `null`.

   이 `sign` 메서드는 서명된 PDF 문서를 나타내는 `BLOB` 개체를 반환합니다.

1. 서명된 PDF 문서 저장

   * 생성자를 호출하여 `System.IO.FileStream` 개체를 만듭니다. 서명된 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 메서드에서 반환된 개체의 내용을 저장하는 바이트 배열을 `BLOB` `sign` 만듭니다. 개체 데이터 멤버의 값을 가져와 바이트 배열 `BLOB` 을 `MTOM` 채웁니다.
   * 생성자를 호출하고 개체를 전달하여 `System.IO.BinaryWriter` 개체를 `System.IO.FileStream` 만듭니다.
   * 개체의 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 PDF 파일 `System.IO.BinaryWriter` `Write` 에 씁니다.

**참고 항목**

[인터랙티브한 양식에 디지털 서명](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## PDF 문서 인증 {#certifying-pdf-documents}

PDF 문서를 인증된 서명이라고 하는 특정 유형의 서명을 사용하여 인증하여 보호할 수 있습니다. 인증된 서명은 다음과 같은 방식으로 디지털 서명과 구별됩니다.

* PDF 문서에 적용되는 첫 번째 서명이어야 합니다. 즉, 인증된 서명이 적용될 때 문서의 다른 모든 서명 필드는 서명되지 않아야 합니다. PDF 문서에는 하나의 인증된 서명만 허용됩니다. PDF 문서에 서명하여 인증하려는 경우 서명하기 전에 이를 인증해야 합니다. PDF 문서를 인증한 후 추가 서명 필드에 디지털 방식으로 서명할 수 있습니다.
* 문서의 작성자 또는 작성자는 인증된 서명을 무효화하지 않고 특정 방식으로 문서를 수정할 수 있음을 지정할 수 있습니다. 예를 들어, 문서에 양식 입력 또는 주석 달기가 허용될 수 있습니다. 작성자가 특정 수정 사항이 허용되지 않도록 지정하는 경우 Acrobat에서는 사용자가 해당 방식으로 문서를 수정할 수 없도록 제한합니다. 다른 응용 프로그램을 사용하는 등 이러한 수정이 이루어지면 인증된 서명이 유효하지 않으며 사용자가 문서를 열 때 Acrobat에서 경고 메시지가 표시됩니다. (인증되지 않은 서명을 사용하는 경우 수정 작업이 수행되지 않으며 일반적인 편집 작업으로 인해 원본 서명이 무효화되지는 않습니다.)
* 서명 시 문서의 내용이 모호하거나 오해를 불러일으킬 수 있는 특정 유형의 컨텐츠에 대해 문서가 스캔됩니다. 예를 들어, 주석에서는 인증되는 내용을 이해하는 데 중요한 페이지의 일부 텍스트를 모호하게 할 수 있습니다. 이러한 컨텐츠에 대한 설명(법적 증명)을 제공할 수 있습니다.

서명 서비스 Java API 또는 서명 웹 서비스 API를 사용하여 프로그래밍 방식으로 PDF 문서를 인증할 수 있습니다. PDF 문서를 인증할 때는 자격 증명 서비스에 있는 보안 자격 증명을 참조해야 합니다. 보안 자격 증명에 대한 자세한 내용은 응용 프로그램 서버에 대한 *AEM Forms* 설치 및 배포 안내서를 참조하십시오.

>[!NOTE]
>
>동일한 PDF 문서를 인증하고 서명할 때 인증 서명을 신뢰할 수 없는 경우 Acrobat 또는 Adobe Reader에서 PDF 문서를 열 때 첫 번째 서명 옆에 노란색 삼각형이 나타납니다. 이러한 상황을 방지하려면 인증 서명을 신뢰할 수 있어야 합니다.

>[!NOTE]
>
>Cipher NShield HSM 자격 증명을 사용하여 PDF 문서에 서명하거나 인증할 때 AEM Forms이 배포된 J2EE 응용 프로그램 서버를 다시 시작할 때까지 새 자격 증명을 사용할 수 없습니다. 그러나 구성 값을 설정하면 J2EE 응용 프로그램 서버를 다시 시작하지 않고 서명 또는 인증 작업이 작동합니다.

cknfastrc 파일에 /opt/nfast/cknfastrc(또는 c:\nfast\cknfastrc)에 있는 다음 구성 값을 추가할 수 있습니다.

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

이 구성 값을 cknfastrc 파일에 추가하면 J2EE 응용 프로그램 서버를 다시 시작하지 않고 새 자격 증명을 사용할 수 있습니다.

>[!NOTE]
>
>서명 서비스 및 문서 인증에 대한 자세한 내용은 AEM Forms에 대한 [서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-5}

PDF 문서를 인증하려면 다음 작업을 수행합니다.

1. 프로젝트 파일 포함
1. 서명 클라이언트 만들기를 참조하십시오.
1. PDF 문서를 인증하여
1. PDF 문서 인증
1. 인증된 PDF 문서를 PDF 파일로 저장할 수 있습니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

다음 JAR 파일을 프로젝트의 클래스 경로에 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(AEM Forms이 JBoss에 배포된 경우 필요)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필요)

이러한 JAR 파일의 위치에 대한 자세한 내용은 AEM Forms Java 라이브러리 파일 [포함을 참조하십시오](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**서명 클라이언트 만들기**

프로그래밍 방식으로 서명 작업을 수행하려면 먼저 서명 클라이언트를 만들어야 합니다.

**PDF 문서를 통해 인증 받기**

PDF 문서를 인증하려면 서명 필드가 포함된 PDF 문서를 받아야 합니다. PDF 문서에 서명 필드가 없으면 인증할 수 없습니다. 서명 필드는 디자이너를 사용하거나 프로그래밍 방식으로 추가할 수 있습니다. 서명 필드를 프로그래밍 방식으로 추가하는 방법에 대한 자세한 내용은 서명 필드 [추가를 참조하십시오](digitally-signing-certifying-documents.md#adding-signature-fields).

**PDF 문서 인증**

PDF 문서를 성공적으로 인증하려면 서명 서비스에서 PDF 문서를 인증하는 데 사용하는 다음 입력 값이 필요합니다.

* **PDF 문서**: 서명 필드가 포함된 PDF 문서로서, 인증된 서명의 그래픽 표현이 포함된 양식 필드입니다. PDF 문서에 서명 필드가 포함되어야 인증을 받을 수 있습니다. 서명 필드는 디자이너를 사용하거나 프로그래밍 방식으로 추가할 수 있습니다. (서명 필드 [추가를 참조하십시오](digitally-signing-certifying-documents.md#adding-signature-fields).)
* **서명 필드 이름**: 인증된 서명 필드의 정규화된 이름입니다. 다음 값이 예입니다. `form1[0].#subform[1].SignatureField3[3]`. XFA 양식 필드를 사용할 때 서명 필드의 부분 이름도 사용할 수 있습니다. `SignatureField3[3]`. 필드 이름에 대해 null 값이 전달되면 보이지 않는 서명 필드가 동적으로 만들어지고 인증됩니다.
* **보안 자격 증명**: PDF 문서를 인증하는 데 사용되는 자격 증명 이 보안 자격 증명에는 암호 및 별칭이 포함되어 있습니다. 이 별칭은 자격 증명 서비스 내에 있는 자격 증명에 나타나는 별칭과 일치해야 합니다. 별칭은 PKCS#12 파일(확장명이 .pfx) 또는 HSM(하드웨어 보안 모듈)에 있을 수 있는 실제 자격 증명을 참조합니다.
* **해시 알고리즘**: PDF 문서를 다이제스트하는 데 사용할 해시 알고리즘입니다.
* **서명 이유**: Acrobat 또는 Adobe Reader에 표시되므로 다른 사용자가 PDF 문서를 인증한 이유를 알 수 있습니다.
* **서명자의 위치**: 자격 증명에 의해 지정된 서명자의 위치입니다.
* **연락처 정보**: 서명자의 주소 및 전화 번호 등 연락처 정보
* **권한 정보**: 인증된 서명이 유효하지 않게 만들지 않고도 최종 사용자가 문서에서 수행할 수 있는 작업을 제어하는 권한 예를 들어 PDF 문서를 변경하면 인증된 서명이 유효하지 않게 되도록 권한을 설정할 수 있습니다.
* **법적 설명**: 문서가 인증되면 문서의 내용이 모호하거나 오해를 불러일으킬 수 있는 특정 유형의 컨텐츠를 자동으로 스캔합니다. 예를 들어, 주석에서는 인증되는 내용을 이해하는 데 중요한 페이지의 일부 텍스트를 모호하게 할 수 있습니다. 스캔 프로세스는 이러한 유형의 컨텐츠에 대한 경고를 생성합니다. 이 값은 경고를 생성할 수 있는 컨텐츠에 대한 추가 설명을 제공합니다.
* **모양 옵션**: 인증된 서명의 모양을 제어하는 옵션 예를 들어 인증된 서명에는 날짜 정보가 표시될 수 있습니다.
* **취소 확인**: 이 값은 서명자의 인증서에 대해 해지 검사가 수행되는지 여부를 지정합니다. 의 기본 설정은 해지 검사가 수행되지 않음을 `false` 의미합니다.
* **OCSP 설정**: PDF 문서를 인증하는 데 사용되는 자격 증명 상태에 대한 정보를 제공하는 OCSP(온라인 인증서 상태 프로토콜) 지원 설정 예를 들어 PDF 문서에 로그인하는 데 사용하는 자격 증명에 대한 정보를 제공하는 서버의 URL을 지정할 수 있습니다.
* **CRL 설정**: 해지 검사가 완료된 경우 CRL(인증서 해지 목록) 기본 설정에 대한 설정입니다. 예를 들어 자격 증명이 해지되었는지 항상 확인하도록 지정할 수 있습니다.
* **타임스탬프**: 인증된 서명에 적용되는 타임스탬프 정보를 정의하는 설정입니다. 타임스탬프는 특정 시간 이전에 특정 데이터가 설정되었음을 나타냅니다. 이러한 지식은 서명자와 확인자 간의 신뢰관계를 구축하는 데 도움이 됩니다.

**인증된 PDF 문서를 PDF 파일로 저장**

서명 서비스가 PDF 문서를 인증한 후 사용자가 Acrobat 또는 Adobe Reader에서 문서를 열 수 있도록 PDF 파일로 저장할 수 있습니다.

**참고 항목**

[Java API를 사용하여 PDF 문서 인증](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-java-api)

[웹 서비스 API를 사용하여 PDF 문서 인증](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[서명 필드 추가](digitally-signing-certifying-documents.md#adding-signature-fields)

### Java API를 사용하여 PDF 문서 인증 {#certify-pdf-documents-using-the-java-api}

서명 API(Java)를 사용하여 PDF 문서를 인증합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-signatures-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. 서명 클라이언트 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 개체를 `SignatureServiceClient` 만들고 개체를 `ServiceClientFactory` 전달합니다.

1. PDF 문서를 통해 인증 받기

   * 생성자를 사용하여 인증할 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만들고 PDF 문서의 위치를 지정하는 문자열 값을 전달합니다.
   * 생성자를 사용하여 개체를 `com.adobe.idp.Document` 만들고 개체를 `java.io.FileInputStream` 전달합니다.

1. PDF 문서 인증

   개체의 방법을 호출하고 다음 값을 전달하여 `SignatureServiceClient` PDF 문서를 `certify` 인증합니다.

   * 인증할 PDF 문서를 나타내는 `com.adobe.idp.Document` 개체
   * 서명이 포함될 서명 필드의 이름을 나타내는 문자열 값입니다.
   * PDF 문서를 인증하는 데 사용되는 자격 증명을 나타내는 `Credential` 개체입니다. 개체의 정적 `Credential` `Credential` `getInstance` 메서드를 호출하고 보안 자격 증명에 해당하는 별칭 값을 지정하는 문자열 값을 전달하여 개체를 만듭니다.
   * PDF 문서를 소화하는 데 사용되는 해시 알고리즘을 나타내는 정적 데이터 멤버를 지정하는 `HashAlgorithm` 객체입니다. 예를 들어 SHA1 알고리즘 `HashAlgorithm.SHA1` 을 사용하도록 지정할 수 있습니다.
   * PDF 문서가 인증된 이유를 나타내는 문자열 값입니다.
   * 서명자의 연락처 정보를 나타내는 문자열 값입니다.
   * 서명을 무효화하는 PDF 문서에서 수행할 수 있는 작업을 지정하는 `MDPPermissions` 개체
   * 인증된 서명의 모양을 제어하는 `PDFSignatureAppearanceOptions` 오브젝트입니다. 원하는 경우 메서드를 호출하여 서명의 모양을 수정합니다 `setShowDate`.
   * 서명을 무효화하는 작업에 대한 설명을 제공하는 문자열 값.
   * 서명자의 인증서에 대한 취소 확인을 수행할지 여부를 지정하는 `java.lang.Boolean` 개체 이 해지 검사가 완료되면 서명에 포함됩니다. The default is `false`.
   * 인증되는 서명 필드가 잠겨 있는지 여부를 지정하는 `java.lang.Boolean` 개체입니다. 필드가 잠겨 있으면 서명 필드는 읽기 전용으로 표시되고, 해당 속성은 수정할 수 없으며, 필요한 권한이 없는 사람은 지울 수 없습니다. The default is `false`.
   * OCSP(Online Certificate Status Protocol) 지원에 대한 환경 설정을 저장하는 `OCSPPreferences` 개체입니다. 해지 검사가 수행되지 않으면 이 매개 변수가 사용되지 않으며 지정할 수 있습니다 `null`. 이 개체에 대한 자세한 내용은 [AEM Forms API 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * CRL(인증서 해지 목록) 기본 설정을 저장하는 `CRLPreferences` 객체입니다. 해지 검사가 수행되지 않으면 이 매개 변수가 사용되지 않으며 지정할 수 있습니다 `null`.
   * TSP(타임스탬프 공급자) 지원에 대한 환경 설정을 저장하는 `TSPPreferences` 개체입니다. 예를 들어 `TSPPreferences` 개체를 만든 후 개체의 메서드를 호출하여 TSP 서버의 URL을 설정할 수 `TSPPreferences` `setTspServerURL` 있습니다. 이 매개 변수는 선택 사항이며 사용할 수 있습니다 `null`. 자세한 내용은 AEM Forms에 대한 [서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

   이 `certify` 메서드는 인증된 PDF 문서를 나타내는 `com.adobe.idp.Document` 개체를 반환합니다.

1. 인증된 PDF 문서를 PDF 파일로 저장

   * 개체를 만들고 파일 확장자가 .pdf인지 확인합니다. `java.io.File`
   * 개체의 `com.adobe.idp.Document` 메서드를 `copyToFile` 호출하여 `com.adobe.idp.Document` 개체의 내용을 파일에 복사합니다.

**참고 항목**

[PDF 문서 인증](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[빠른 시작(SOAP 모드): Java API를 사용하여 PDF 문서 인증](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-certifying-a-pdf-document-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 PDF 문서 인증 {#certify-pdf-documents-using-the-web-service-api}

서명 API(웹 서비스)를 사용하여 PDF 문서를 인증합니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Forms `localhost` 를 호스팅하는 서버의 IP 주소로 대체합니다.

1. 서명 클라이언트 만들기

   * 기본 생성자를 사용하여 `SignatureServiceClient` 개체를 만듭니다.
   * 생성자를 사용하여 `SignatureServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/SignatureService?WSDL`). 속성을 사용할 필요는 `lc_version` 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * 필드의 값을 `System.ServiceModel.BasicHttpBinding` 가져와 개체를 `SignatureServiceClient.Endpoint.Binding` 만듭니다. 반환 값을 다음으로 캐스팅합니다 `BasicHttpBinding`.
   * 개체 `System.ServiceModel.BasicHttpBinding` 필드를 (으)로 `MessageEncoding` 설정합니다 `WSMessageEncoding.Mtom`. 이 값을 사용하면 MTOM이 사용됩니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM 양식 사용자 이름을 지정합니다 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 해당 암호 값을 필드에 지정합니다 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 필드에 상수 값 `HttpClientCredentialType.Basic` 을 지정합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 필드에 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly` 을 지정합니다 `BasicHttpBindingSecurity.Security.Mode`.

1. PDF 문서를 통해 인증 받기

   * 생성자를 사용하여 `BLOB` 개체를 만듭니다. 이 `BLOB` 개체는 인증된 PDF 문서를 저장하는 데 사용됩니다.
   * 생성자를 호출하고 인증할 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * 개체의 내용을 저장하는 바이트 배열을 `System.IO.FileStream` 만듭니다. 개체의 속성을 가져와 바이트 배열의 크기를 결정할 수 `System.IO.FileStream` `Length` 있습니다.
   * 개체의 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열 `System.IO.FileStream` `Read` 을 스트림 데이터로 채웁니다.
   * 바이트 배열의 컨텐츠에 데이터 `BLOB` `MTOM` 멤버를 할당하여 객체를 채웁니다.

1. PDF 문서 인증

   개체의 방법을 호출하고 다음 값을 전달하여 `SignatureServiceClient` PDF 문서를 `certify` 인증합니다.

   * 인증할 PDF 문서를 나타내는 `BLOB` 개체
   * 서명이 포함될 서명 필드의 이름을 나타내는 문자열 값입니다.
   * PDF 문서를 인증하는 데 사용되는 자격 증명을 나타내는 `Credential` 개체입니다. 생성자를 사용하여 `Credential` 개체를 만들고 개체의 속성에 값을 할당하여 `Credential` 별칭을 `alias` 지정합니다.
   * PDF 문서를 소화하는 데 사용되는 해시 알고리즘을 나타내는 정적 데이터 멤버를 지정하는 `HashAlgorithm` 객체입니다. 예를 들어 SHA1 알고리즘 `HashAlgorithm.SHA1` 을 사용하도록 지정할 수 있습니다.
   * 해시 알고리즘의 사용 여부를 지정하는 부울 값.
   * PDF 문서가 인증된 이유를 나타내는 문자열 값입니다.
   * 서명자의 위치를 나타내는 문자열 값.
   * 서명자의 연락처 정보를 나타내는 문자열 값입니다.
   * 서명을 무효화하는 PDF 문서에서 수행할 수 있는 작업을 지정하는 `MDPPermissions` 개체의 정적 데이터 멤버
   * 이전 매개 변수 값으로 전달된 `MDPPermissions` 개체를 사용할지 여부를 지정하는 부울 값입니다.
   * 서명이 무효화되는 동작을 설명하는 문자열 값.
   * 인증된 서명의 모양을 제어하는 `PDFSignatureAppearanceOptions` 오브젝트입니다. 생성자를 사용하여 `PDFSignatureAppearanceOptions` 개체를 만듭니다. 데이터 멤버 중 하나를 설정하여 서명의 모양을 수정할 수 있습니다.
   * 서명자의 인증서에 대한 취소 확인을 수행할지 여부를 지정하는 `System.Boolean` 개체 이 해지 검사가 완료되면 서명에 포함됩니다. The default is `false`.
   * 인증되는 서명 필드가 잠겨 있는지 여부를 지정하는 `System.Boolean` 개체입니다. 필드가 잠겨 있으면 서명 필드는 읽기 전용으로 표시되고, 해당 속성은 수정할 수 없으며, 필요한 권한이 없는 사람은 지울 수 없습니다. The default is `false`.
   * 서명 필드가 잠겨 있는지 여부를 지정하는 `System.Boolean` 개체입니다. 즉, 이전 매개 변수 `true` 로 전달하면 이 매개 변수 `true` 로 전달됩니다.
   * OCSP(Online Certificate Status Protocol) 지원에 대한 기본 설정을 저장하는 `OCSPPreferences` 개체로, PDF 문서를 인증하는 데 사용되는 자격 증명의 상태에 대한 정보를 제공합니다. 해지 검사가 수행되지 않으면 이 매개 변수가 사용되지 않으며 지정할 수 있습니다 `null`.
   * CRL(인증서 해지 목록) 기본 설정을 저장하는 `CRLPreferences` 객체입니다. 해지 검사가 수행되지 않으면 이 매개 변수가 사용되지 않으며 지정할 수 있습니다 `null`.
   * TSP(타임스탬프 공급자) 지원에 대한 환경 설정을 저장하는 `TSPPreferences` 개체입니다. 예를 들어 `TSPPreferences` 개체를 만든 후 개체의 데이터 멤버를 설정하여 TSP의 URL을 `TSPPreferences` 설정할 수 `tspServerURL` 있습니다. 이 매개 변수는 선택 사항이며 사용할 수 있습니다 `null`.

   이 `certify` 메서드는 인증된 PDF 문서를 나타내는 `BLOB` 개체를 반환합니다.

1. 인증된 PDF 문서를 PDF 파일로 저장

   * 생성자를 호출하고 인증된 PDF 문서와 파일을 열 모드를 포함하는 PDF 문서의 파일 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * 메서드에서 반환된 개체의 내용을 저장하는 바이트 배열을 `BLOB` `certify` 만듭니다. 개체 데이터 멤버의 값을 가져와 바이트 배열 `BLOB` 을 `binaryData` 채웁니다.
   * 생성자를 호출하고 개체를 전달하여 `System.IO.BinaryWriter` 개체를 `System.IO.FileStream` 만듭니다.
   * 개체의 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 PDF 파일 `System.IO.BinaryWriter` `Write` 에 씁니다.

**참고 항목**

[PDF 문서 인증](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 디지털 서명 확인 {#verifying-digital-signatures}

서명된 PDF 문서가 수정되지 않았고 디지털 서명이 유효한지 디지털 서명을 확인할 수 있습니다. 디지털 서명을 확인할 때 서명의 상태 및 서명자의 ID와 같은 서명의 속성을 확인할 수 있습니다. 디지털 서명을 신뢰하기 전에 확인하는 것이 좋습니다. 디지털 서명을 확인할 때는 디지털 서명이 포함된 PDF 문서를 참조하십시오.

서명자의 신원을 알 수 없다고 가정합니다. Acrobat에서 PDF 문서를 열면 다음 그림과 같이 서명자의 ID를 알 수 없다는 경고 메시지가 나타납니다.

![vd_verifysig](assets/vd_vd_verifysig.png)

마찬가지로, 디지털 서명을 프로그램 방식으로 확인할 때 서명자의 ID 상태를 확인할 수 있습니다. 예를 들어 이전 그림에 표시된 문서의 디지털 서명을 확인하는 경우 서명자의 ID를 알 수 없다는 결과가 나타납니다.

>[!NOTE]
>
>서명 서비스 및 디지털 서명 확인에 대한 자세한 내용은 AEM Forms에 대한 [서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-6}

디지털 서명을 확인하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일 포함
1. 서명 클라이언트 만들기를 참조하십시오.
1. 확인할 서명이 포함된 PDF 문서를 가져옵니다.
1. PKI 런타임 옵션을 설정합니다.
1. 디지털 서명 확인
1. 서명의 상태를 확인합니다.
1. 서명자의 ID 확인

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함하십시오.

다음 JAR 파일을 프로젝트의 클래스 경로에 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(AEM Forms이 JBoss에 배포된 경우 필요)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필요)

이러한 JAR 파일의 위치에 대한 자세한 내용은 AEM Forms Java 라이브러리 파일 [포함을 참조하십시오](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**서명 클라이언트 만들기**

서명 서비스 작업을 프로그래밍 방식으로 수행하기 전에 서명 서비스 클라이언트를 만듭니다.

**확인할 서명이 포함된 PDF 문서 가져오기**

PDF 문서에 디지털 서명 또는 인증하는 데 사용되는 서명을 확인하려면 서명이 포함된 PDF 문서를 가져옵니다.

**PKI 런타임 옵션 설정**

서명 서비스가 PDF 문서에서 서명을 확인할 때 사용하는 다음과 같은 PKI 런타임 옵션을 설정합니다.

* 확인 시간
* 취소 확인
* 타임스탬프 값

이러한 옵션 설정의 일부로 확인 시간을 지정할 수 있습니다. 예를 들어 현재 시간(유효성 검사기 컴퓨터의 시간)을 선택하여 현재 시간을 사용할 수 있습니다. 다른 시간 값에 대한 자세한 내용은 AEM Forms API 참조 `VerificationTime` 의 [열거형 값을 참조하십시오](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

확인 프로세스의 일부로 취소 확인을 수행할지 여부를 지정할 수도 있습니다. 예를 들어 해지 검사를 수행하여 인증서가 해지되었는지 확인할 수 있습니다. 해지 확인 옵션에 대한 자세한 내용은 AEM Forms API 참조 `RevocationCheckStyle` 의 [열거형 값을 참조하십시오](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

인증서에 대한 해지 검사를 수행하려면 개체를 사용하여 CRL(인증서 해지 목록) 서버의 URL을 `CRLOptionSpec` 지정합니다. 그러나 CRL 서버에 대한 URL을 지정하지 않으면 서명 서비스는 인증서에서 URL을 가져옵니다.

CRL 서버를 사용하는 대신 해지 확인을 수행할 때 OCSP(온라인 인증서 상태 프로토콜) 서버를 사용할 수 있습니다. 일반적으로 CRL 서버와 반대로 OCSP 서버를 사용하는 경우 해지 검사가 더 빨리 수행됩니다. (온라인 [인증서 상태 프로토콜](https://tools.ietf.org/html/rfc2560)참조)

서명 서비스가 Adobe 응용 프로그램 및 서비스를 사용하여 사용하는 CRL 및 OSP 서버 순서를 설정할 수 있습니다. 예를 들어, Adobe 응용 프로그램 및 서비스에서 OCSP 서버가 먼저 설정된 경우 OCSP 서버가 선택된 후 CRL 서버가 선택됩니다.

해지 확인을 수행하지 않으면 서명 서비스는 인증서가 해지되었는지 확인하지 않습니다. 즉, CRL 및 OCSP 서버 정보는 무시됩니다.

>[!NOTE]
>
>및 개체를 사용하여 인증서에 지정된 URL을 재정의할 수 `CRLOptionSpec` `OCSPOptionSpec` 있습니다. 예를 들어, CRL 서버를 재정의하려면 `CRLOptionSpec` 객체의 메서드를 호출할 수 `setLocalURI` 있습니다.

타임스탬프는 서명된 문서 또는 인증된 문서가 수정된 시간을 추적하는 프로세스입니다. 문서에 서명이 완료되면 아무도 문서를 수정할 수 없습니다. 타임스탬프를 통해 서명된 문서 또는 인증된 문서의 유효성을 강화할 수 있습니다. 개체를 사용하여 타임스탬프 옵션을 설정할 수 `TSPOptionSpec` 있습니다. 예를 들어 TSP(타임스탬프 공급자) 서버의 URL을 지정할 수 있습니다.

>[!NOTE]
>
>Java 및 웹 서비스 빠른 시작에서 확인 시간은 로 설정되고 취소 확인 `VerificationTime.CURRENT_TIME` 은 로 설정됩니다 `RevocationCheckStyle.BestEffort`. CRL 또는 OCSP 서버 정보가 지정되지 않았으므로 서버 정보를 인증서에서 가져옵니다.

**디지털 서명 확인**

서명을 성공적으로 확인하려면 서명을 포함하는 서명 필드의 정규화된 이름(예: `form1[0].#subform[1].SignatureField3[3]` XFA 양식 필드를 사용하는 경우 서명 필드의 부분 이름을 사용할 수도 있습니다. `SignatureField3`.

기본적으로 서명 서비스는 확인 시간 후 문서에 서명할 수 있는 시간을 65분으로 제한합니다. 사용자가 현재 시간에 서명을 확인하고 서명 시간이 현재 시간보다 늦고 65분 이내인 경우 서명 서비스는 확인 오류를 생성하지 않습니다.

>[!NOTE]
>
>서명을 확인할 때 필요한 기타 값은 [AEM Forms API 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**서명 상태 확인**

디지털 서명 확인의 일부로 서명 상태를 확인할 수 있습니다.

**서명자의 ID 확인**

다음 값 중 하나일 수 있는 서명자의 ID를 확인할 수 있습니다.

* **알 수 없음**: 서명자 확인을 수행할 수 없기 때문에 이 서명자를 알 수 없습니다.
* **신뢰할 수 있는**&#x200B;제품: 이 서명자는 신뢰할 수 있습니다.
* **신뢰할 수 없음**: 이 서명자는 신뢰할 수 없습니다.

**참고 항목**

[Java API를 사용하여 디지털 서명 확인](#verify-digital-signatures-using-the-java-api)

[웹 서비스 API를 사용하여 디지털 서명 확인](#verify-digital-signatures-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API를 사용하여 디지털 서명 확인 {#verify-digital-signatures-using-the-java-api}

서명 서비스 API(Java)를 사용하여 디지털 서명을 확인합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-signatures-client.jar 등의 클라이언트 JAR 파일을 포함합니다.

1. 서명 클라이언트 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 개체를 `SignatureServiceClient` 만들고 개체를 `ServiceClientFactory` 전달합니다.

1. 확인할 서명이 포함된 PDF 문서 가져오기

   * 생성자를 사용하여 확인할 서명이 포함된 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만듭니다. PDF 문서의 위치를 지정하는 문자열 값을 전달합니다.
   * 생성자를 사용하여 개체를 `com.adobe.idp.Document` 만들고 개체를 `java.io.FileInputStream` 전달합니다.

1. PKI 런타임 옵션 설정

   * 생성자를 사용하여 `PKIOptions` 개체를 만듭니다.
   * 개체의 메서드를 호출하고 확인 시간을 지정하는 `PKIOptions` `setVerificationTime` `VerificationTime` 열거형 값을 전달하여 확인 시간을 설정합니다.
   * 개체의 메서드를 호출하고 해지 확인 수행 여부를 지정하는 `PKIOptions` `setRevocationCheckStyle` `RevocationCheckStyle` 열거형 값을 전달하여 해지 확인 옵션을 설정합니다.

1. 디지털 서명 확인

   개체의 메서드를 호출하고 다음 값을 전달하여 서명을 확인합니다. `SignatureServiceClient` `verify2`

   * 디지털 서명 또는 인증된 PDF 문서가 포함된 `com.adobe.idp.Document` 개체입니다.
   * 확인할 서명이 포함된 서명 필드 이름을 나타내는 문자열 값입니다.
   * PKI 런타임 옵션이 포함된 `PKIOptions` 개체입니다.
   * SPI 정보가 포함된 `VerifySPIOptions` 인스턴스입니다. 이 매개 변수 `null` 에 대해 지정할 수 있습니다.

   이 `verify2` 메서드는 디지털 서명을 확인하는 데 사용할 수 있는 정보가 포함된 `PDFSignatureVerificationInfo` 개체를 반환합니다.

1. 서명 상태 확인

   * 개체의 메서드를 호출하여 서명 상태를 `PDFSignatureVerificationInfo` 확인합니다 `getStatus` . 이 메서드는 서명 상태를 지정하는 `SignatureStatus` 개체를 반환합니다. 예를 들어 서명된 PDF 문서가 수정되지 않은 경우 이 방법이 반환됩니다 `SignatureStatus.DocumentSigNoChanges`.

1. 서명자의 ID 확인

   * 개체의 방법을 호출하여 서명자의 ID를 `PDFSignatureVerificationInfo` `getSigner` 확인합니다. 이 메서드는 `IdentityInformation` 개체를 반환합니다.
   * 서명자의 ID를 확인하려면 `IdentityInformation` 개체의 `getStatus` 방법을 불러옵니다. 이 메서드는 ID를 지정하는 `IdentityStatus` 열거형 값을 반환합니다. 예를 들어, 서명자를 신뢰할 수 있는 경우 이 방법을 반환합니다 `IdentityStatus.TRUSTED`.

**참고 항목**

[디지털 서명 확인](#verify-digital-signatures-using-the-java-api)

[빠른 시작(SOAP 모드): Java API를 사용하여 디지털 서명 확인](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-a-digital-signature-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 디지털 서명 확인 {#verify-digital-signatures-using-the-web-service-api}

Signature Service API(웹 서비스)를 사용하여 디지털 서명을 확인합니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Forms `localhost` 를 호스팅하는 서버의 IP 주소로 대체합니다.

1. 서명 클라이언트 만들기

   * 기본 생성자를 사용하여 `SignatureServiceClient` 개체를 만듭니다.
   * 생성자를 사용하여 `SignatureServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/SignatureService?WSDL`). 속성을 사용할 필요는 `lc_version` 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * 필드의 값을 `System.ServiceModel.BasicHttpBinding` 가져와 개체를 `SignatureServiceClient.Endpoint.Binding` 만듭니다. 반환 값을 다음으로 캐스팅합니다 `BasicHttpBinding`.
   * 개체 `System.ServiceModel.BasicHttpBinding` 필드를 (으)로 `MessageEncoding` 설정합니다 `WSMessageEncoding.Mtom`. 이 값을 사용하면 MTOM이 사용됩니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM 양식 사용자 이름을 지정합니다 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 해당 암호 값을 필드에 지정합니다 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 필드에 상수 값 `HttpClientCredentialType.Basic` 을 지정합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 필드에 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly` 을 지정합니다 `BasicHttpBindingSecurity.Security.Mode`.

1. 확인할 서명이 포함된 PDF 문서 가져오기

   * 생성자를 사용하여 `BLOB` 개체를 만듭니다. 이 `BLOB` 개체는 확인할 디지털 또는 인증된 서명이 포함된 PDF 문서를 저장하는 데 사용됩니다.
   * 생성자를 호출하여 `System.IO.FileStream` 개체를 만듭니다. 서명된 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 개체의 내용을 저장하는 바이트 배열을 `System.IO.FileStream` 만듭니다. 개체의 속성을 가져와 바이트 배열의 크기를 결정할 수 `System.IO.FileStream` `Length` 있습니다.
   * 개체의 메서드를 호출하여 바이트 배열을 스트림 데이터로 `System.IO.FileStream` 채웁니다 `Read` . 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 바이트 배열의 컨텐츠에 해당 `BLOB``MTOM` 속성을 할당하여 개체를 채웁니다.

1. PKI 런타임 옵션 설정

   * 생성자를 사용하여 `PKIOptions` 개체를 만듭니다.
   * 확인 시간을 지정하는 열거형 값을 `PKIOptions` 개체의 `verificationTime` 데이터 멤버에 할당하여 확인 시간을 `VerificationTime` 설정합니다.
   * 해지 확인 수행 여부를 지정하는 열거형 값을 `PKIOptions` 개체의 `revocationCheckStyle` 데이터 멤버에 할당하여 해지 확인 옵션을 `RevocationCheckStyle` 설정합니다.

1. 디지털 서명 확인

   개체의 메서드를 호출하고 다음 값을 전달하여 서명을 확인합니다. `SignatureServiceClient` `verify2`

   * 디지털 서명 또는 인증된 PDF 문서가 포함된 `BLOB` 개체입니다.
   * 확인할 서명이 포함된 서명 필드 이름을 나타내는 문자열 값입니다.
   * PKI 런타임 옵션이 포함된 `PKIOptions` 개체입니다.
   * SPI 정보가 포함된 `VerifySPIOptions` 인스턴스입니다. 이 매개 변수 `null` 에 대해 지정할 수 있습니다.

   이 `verify2` 메서드는 디지털 서명을 확인하는 데 사용할 수 있는 정보가 포함된 `PDFSignatureVerificationInfo` 개체를 반환합니다.

1. 서명 상태 확인

   개체 데이터 멤버의 값을 가져와 서명 상태를 `PDFSignatureVerificationInfo` 확인합니다 `status` . 이 데이터 멤버는 서명의 상태를 지정하는 `SignatureStatus` 개체를 저장합니다. 예를 들어 서명된 PDF 문서가 수정된 경우 `status` 데이터 멤버는 값을 저장합니다 `SignatureStatus.DocumentSigNoChanges`.

1. 서명자의 ID 확인

   * 개체 데이터 멤버의 값을 검색하여 서명자의 ID를 `PDFSignatureVerificationInfo` 결정합니다 `signer` . 이 멤버는 `IdentityInformation` 개체를 반환합니다.
   * 개체의 `IdentityInformation` 데이터 `status` 멤버를 검색하여 서명자의 ID를 확인합니다. 이 데이터 멤버는 ID를 지정하는 `IdentityStatus` 열거형 값을 반환합니다. 예를 들어, 서명자를 신뢰하는 경우 이 멤버는 다시 `IdentityStatus.TRUSTED`반환합니다.

**참고 항목**

[디지털 서명 확인](#verify-digital-signatures-using-the-java-api)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 여러 디지털 서명 확인 {#verifying-multiple-digital-signatures}

AEM Forms은 PDF 문서에 있는 모든 디지털 서명을 확인하는 방법을 제공합니다. 여러 서명자의 서명이 필요한 업무 처리 과정의 결과로 PDF 문서에 여러 개의 디지털 서명이 포함되어 있다고 가정합니다. 예를 들어 대출 담당자와 관리자의 서명이 모두 필요한 금융 거래를 고려합니다. 서명 서비스 Java API 또는 웹 서비스 API를 사용하여 PDF 문서 내의 모든 서명을 확인할 수 있습니다. 여러 디지털 서명을 확인하는 경우 각 서명의 상태 및 속성을 확인할 수 있습니다. 디지털 서명을 신뢰하기 전에 이를 확인하는 것이 좋습니다. 단일 디지털 서명 확인에 익숙한 것이 좋습니다.

>[!NOTE]
>
>서명 서비스 및 디지털 서명 확인에 대한 자세한 내용은 AEM Forms에 대한 [서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-7}

여러 디지털 서명을 확인하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일 포함
1. 서명 클라이언트 만들기를 참조하십시오.
1. 확인할 서명이 포함된 PDF 문서를 가져올 수 있습니다.
1. PKI 런타임 옵션을 설정합니다.
1. 모든 디지털 서명 검색
1. 모든 서명을 통해 공유

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함하십시오.

다음 JAR 파일을 프로젝트의 클래스 경로에 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(AEM Forms이 JBoss에 배포된 경우 필요)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필요)

이러한 JAR 파일의 위치에 대한 자세한 내용은 AEM Forms Java 라이브러리 파일 [포함을 참조하십시오](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**서명 클라이언트 만들기**

서명 서비스 작업을 프로그래밍 방식으로 수행하기 전에 서명 서비스 클라이언트를 만듭니다.

**서명을 포함하는 PDF 문서를 가져와 확인**

PDF 문서에 디지털 서명 또는 인증하는 데 사용되는 서명을 확인하려면 서명이 포함된 PDF 문서를 가져옵니다.

**PKI 런타임 옵션 설정**

PDF 문서에서 모든 서명을 확인할 때 서명 서비스가 사용하는 다음과 같은 PKI 런타임 옵션을 설정합니다.

* 확인 시간
* 취소 확인
* 타임스탬프 값

이러한 옵션 설정의 일부로 확인 시간을 지정할 수 있습니다. 예를 들어 현재 시간(유효성 검사기 컴퓨터의 시간)을 선택하여 현재 시간을 사용할 수 있습니다. 다른 시간 값에 대한 자세한 내용은 AEM Forms API 참조 `VerificationTime` 의 [열거형 값을 참조하십시오](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

확인 프로세스의 일부로 취소 확인을 수행할지 여부를 지정할 수도 있습니다. 예를 들어 해지 검사를 수행하여 인증서가 해지되었는지 확인할 수 있습니다. 해지 확인 옵션에 대한 자세한 내용은 AEM Forms API 참조 `RevocationCheckStyle` 의 [열거형 값을 참조하십시오](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

인증서에 대한 해지 검사를 수행하려면 개체를 사용하여 CRL(인증서 해지 목록) 서버의 URL을 `CRLOptionSpec` 지정합니다. 그러나 CRL 서버에 대한 URL을 지정하지 않으면 서명 서비스는 인증서에서 URL을 가져옵니다.

CRL 서버를 사용하는 대신 해지 확인을 수행할 때 OCSP(온라인 인증서 상태 프로토콜) 서버를 사용할 수 있습니다. 일반적으로 CRL 서버 대신 OCSP 서버를 사용하는 경우 해지 검사가 더 빨리 수행됩니다. (온라인 [인증서 상태 프로토콜](https://tools.ietf.org/html/rfc2560)참조)

서명 서비스가 Adobe 응용 프로그램 및 서비스를 사용하여 사용하는 CRL 및 OSP 서버 순서를 설정할 수 있습니다. 예를 들어 Adobe 응용 프로그램 및 서비스에서 OCSP 서버가 먼저 설정된 경우 OCSP 서버가 선택된 후 CRL 서버가 선택됩니다.

해지 확인을 수행하지 않으면 서명 서비스는 인증서가 해지되었는지 확인하지 않습니다. 즉, CRL 및 OCSP 서버 정보는 무시됩니다.

>[!NOTE]
>
>및 개체를 사용하여 인증서에 지정된 URL을 재정의할 수 `CRLOptionSpec` `OCSPOptionSpec` 있습니다. 예를 들어, CRL 서버를 재정의하려면 `CRLOptionSpec` 객체의 메서드를 호출할 수 `setLocalURI` 있습니다.

타임스탬프는 서명된 문서 또는 인증된 문서가 수정된 시간을 추적하는 프로세스입니다. 문서에 서명이 완료되면 아무도 문서를 수정할 수 없습니다. 타임스탬프를 통해 서명된 문서 또는 인증된 문서의 유효성을 강화할 수 있습니다. 개체를 사용하여 타임스탬프 옵션을 설정할 수 `TSPOptionSpec` 있습니다. 예를 들어 TSP(타임스탬프 공급자) 서버의 URL을 지정할 수 있습니다.

>[!NOTE]
>
>Java 및 웹 서비스 빠른 시작에서 확인 시간은 로 설정되고 취소 확인 `VerificationTime.CURRENT_TIME` 은 로 설정됩니다 `RevocationCheckStyle.BestEffort`. CRL 또는 OCSP 서버 정보가 지정되지 않았으므로 서버 정보를 인증서에서 가져옵니다.

**모든 디지털 서명 검색**

PDF 문서에 있는 모든 디지털 서명을 확인하려면 PDF 문서에서 디지털 서명을 검색합니다. 모든 서명은 목록에 반환됩니다. 디지털 서명 확인의 일부로 서명 상태를 확인합니다.

>[!NOTE]
>
>단일 디지털 서명을 확인하는 경우와 달리 여러 서명을 확인하는 경우 서명 필드 이름을 지정할 필요가 없습니다.

**모든 서명을 통해 공유**

각 서명을 통해 반복 즉, 각 서명에 대해 디지털 서명을 확인하고 서명자의 ID와 각 서명의 상태를 확인합니다. (디지털 서명 [확인을 참조하십시오](#verify-digital-signatures-using-the-java-api).)

>[!NOTE]
>
>요구 사항이 전체 문서인 경우 모든 서명을 통해 반복할 필요는 없습니다.

**참고 항목**

[Java API를 사용하여 여러 디지털 서명 확인](#verify-digital-signatures-using-the-java-api)

[웹 서비스 API를 사용하여 여러 디지털 서명 확인](#verify-digital-signatures-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API를 사용하여 여러 디지털 서명 확인 {#verify-multiple-digital-signatures-using-the-java-api}

Signature Service API(Java)를 사용하여 여러 디지털 서명을 확인합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-signatures-client.jar 등의 클라이언트 JAR 파일을 포함합니다.

1. 서명 클라이언트 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 개체를 `SignatureServiceClient` 만들고 개체를 `ServiceClientFactory` 전달합니다.

1. 서명을 포함하는 PDF 문서를 가져와 확인

   * 생성자를 사용하여 확인할 여러 디지털 서명이 포함된 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만듭니다. PDF 문서의 위치를 지정하는 문자열 값을 전달합니다.
   * 생성자를 사용하여 개체를 `com.adobe.idp.Document` 만들고 개체를 `java.io.FileInputStream` 전달합니다.

1. PKI 런타임 옵션 설정

   * 생성자를 사용하여 `PKIOptions` 개체를 만듭니다.
   * 개체의 메서드를 호출하고 확인 시간을 지정하는 `PKIOptions` `setVerificationTime` `VerificationTime` 열거형 값을 전달하여 확인 시간을 설정합니다.
   * 해지 확인 옵션을 설정하려면 `PKIOptions` 개체의 `setRevocationCheckStyle` 메서드를 호출하고 해지 확인 수행 여부를 지정하는 열거형 값을 `RevocationCheckStyle` 전달합니다.

1. 모든 디지털 서명 검색

   개체의 `SignatureServiceClient` 메서드를 `verifyPDFDocument` 호출하고 다음 값을 전달합니다.

   * 여러 디지털 서명이 포함된 PDF 문서를 포함하는 `com.adobe.idp.Document` 개체입니다.
   * PKI 런타임 옵션이 포함된 `PKIOptions` 개체입니다.
   * SPI 정보가 포함된 `VerifySPIOptions` 인스턴스입니다. 이 매개 변수 `null` 에 대해 지정할 수 있습니다.

   이 방법 `verifyPDFDocument` 은 PDF 문서에 있는 모든 디지털 서명에 대한 정보가 포함된 `PDFDocumentVerificationInfo` 개체를 반환합니다.

1. 모든 서명을 통해 공유

   * 개체의 메서드를 호출하여 모든 서명을 `PDFDocumentVerificationInfo` `getVerificationInfos` 반복합니다. 이 메서드는 각 요소가 개체인 `java.util.List` 개체를 `PDFSignatureVerificationInfo` 반환합니다. 서명 목록을 `java.util.Iterator` 반복하려면 개체를 사용하십시오.
   * 개체를 사용하여 `PDFSignatureVerificationInfo` 개체의 메서드를 호출하여 서명 상태를 확인하는 등의 작업을 수행할 수 `PDFSignatureVerificationInfo` `getStatus` 있습니다. 이 메서드는 정적 데이터 구성원이 서명 상태를 알려주는 `SignatureStatus` 개체를 반환합니다. 예를 들어 서명을 알 수 없으면 이 메서드는 반환합니다 `SignatureStatus.DocumentSignatureUnknown`.

**참고 항목**

[여러 디지털 서명 확인](#verifying-multiple-digital-signatures)

[빠른 시작(SOAP 모드): Java API를 사용하여 여러 디지털 서명 확인](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[디지털 서명 확인](#verify-digital-signatures-using-the-java-api)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 여러 디지털 서명 확인 {#verifying-multiple-digital-signatures-using-the-web-service-api}

Signature Service API(웹 서비스)를 사용하여 여러 디지털 서명을 확인합니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Forms `localhost` 를 호스팅하는 서버의 IP 주소로 대체합니다.

1. 서명 클라이언트 만들기

   * 기본 생성자를 사용하여 `SignatureServiceClient` 개체를 만듭니다.
   * 생성자를 사용하여 `SignatureServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/SignatureService?WSDL`). 속성을 사용할 필요는 `lc_version` 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * 필드의 값을 `System.ServiceModel.BasicHttpBinding` 가져와 개체를 `SignatureServiceClient.Endpoint.Binding` 만듭니다. 반환 값을 다음으로 캐스팅합니다 `BasicHttpBinding`.
   * 개체 `System.ServiceModel.BasicHttpBinding` 필드를 (으)로 `MessageEncoding` 설정합니다 `WSMessageEncoding.Mtom`. 이 값을 사용하면 MTOM이 사용됩니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM 양식 사용자 이름을 지정합니다 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 해당 암호 값을 필드에 지정합니다 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 필드에 상수 값 `HttpClientCredentialType.Basic` 을 지정합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 필드에 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly` 을 지정합니다 `BasicHttpBindingSecurity.Security.Mode`.

1. 서명을 포함하는 PDF 문서를 가져와 확인

   * 생성자를 사용하여 `BLOB` 개체를 만듭니다. 이 `BLOB` 개체는 확인할 여러 개의 디지털 서명이 포함된 PDF 문서를 저장합니다.
   * 생성자를 호출하여 `System.IO.FileStream` 개체를 만듭니다. PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 개체의 내용을 저장하는 바이트 배열을 `System.IO.FileStream` 만듭니다. 개체의 속성을 가져와 바이트 배열의 크기를 결정할 수 `System.IO.FileStream` `Length` 있습니다.
   * 개체의 메서드를 호출하여 바이트 배열을 스트림 데이터로 `System.IO.FileStream` 채웁니다 `Read` . 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 바이트 배열의 컨텐츠에 해당 `BLOB``MTOM` 속성을 할당하여 개체를 채웁니다.

1. PKI 런타임 옵션 설정

   * 생성자를 사용하여 `PKIOptions` 개체를 만듭니다.
   * 확인 시간을 지정하는 열거형 값을 `PKIOptions` 개체의 `verificationTime` 데이터 멤버에 할당하여 확인 시간을 `VerificationTime` 설정합니다.
   * 해지 확인 수행 여부를 지정하는 열거형 값을 `PKIOptions` 개체의 `revocationCheckStyle` 데이터 멤버에 할당하여 해지 확인 옵션을 `RevocationCheckStyle` 설정합니다.

1. 모든 디지털 서명 검색

   개체의 `SignatureServiceClient` 메서드를 `verifyPDFDocument` 호출하고 다음 값을 전달합니다.

   * 여러 디지털 서명이 포함된 PDF 문서를 포함하는 `BLOB` 개체입니다.
   * PKI 런타임 옵션이 포함된 `PKIOptions` 개체입니다.
   * SPI 정보가 포함된 `VerifySPIOptions` 인스턴스입니다. 이 매개 변수에 null을 지정할 수 있습니다.

   이 방법 `verifyPDFDocument` 은 PDF 문서에 있는 모든 디지털 서명에 대한 정보가 포함된 `PDFDocumentVerificationInfo` 개체를 반환합니다.

1. 모든 서명을 통해 공유

   * 개체의 데이터 멤버를 가져와 모든 서명을 `PDFDocumentVerificationInfo` 반복할 수 `verificationInfos` 있습니다. 이 데이터 멤버는 각 요소가 개체인 `Object` 배열을 `PDFSignatureVerificationInfo` 반환합니다.
   * 개체를 사용하여 `PDFSignatureVerificationInfo` 개체의 데이터 멤버를 가져와 서명 상태를 확인하는 등의 작업을 수행할 `PDFSignatureVerificationInfo` 수 `status` 있습니다. 이 데이터 멤버는 정적 데이터 구성원이 서명 상태를 알려주는 `SignatureStatus` 개체를 반환합니다. 예를 들어 서명을 알 수 없으면 이 메서드는 반환합니다 `SignatureStatus.DocumentSignatureUnknown`.

**참고 항목**

[여러 디지털 서명 확인](#verifying-multiple-digital-signatures)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 디지털 서명 제거 {#removing-digital-signatures}

새로운 디지털 서명을 적용하려면 서명 필드에서 디지털 서명을 제거해야 합니다. 디지털 서명을 덮어쓸 수 없습니다. 서명이 포함된 서명 필드에 디지털 서명을 적용하려고 하면 예외가 발생합니다.

>[!NOTE]
>
>서명 서비스에 대한 자세한 내용은 AEM Forms에 대한 [서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-8}

서명 필드에서 디지털 서명을 제거하려면 다음 작업을 수행합니다.

1. 프로젝트 파일 포함
1. 서명 클라이언트 만들기를 참조하십시오.
1. 제거할 서명이 포함된 PDF 문서를 가져올 수 있습니다.
1. 서명 필드에서 디지털 서명을 제거합니다.
1. PDF 문서를 PDF 파일로 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

다음 JAR 파일을 프로젝트의 클래스 경로에 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(AEM Forms이 JBoss에 배포된 경우 필요)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필요)

이러한 JAR 파일의 위치에 대한 자세한 내용은 AEM Forms Java 라이브러리 파일 [포함을 참조하십시오](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**서명 클라이언트 만들기**

서명 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 서명 서비스 클라이언트를 만들어야 합니다.

**제거할 서명이 포함된 PDF 문서 가져오기**

PDF 문서에서 서명을 제거하려면 서명이 포함된 PDF 문서를 받아야 합니다.

**서명 필드에서 디지털 서명 제거**

PDF 문서에서 디지털 서명을 성공적으로 제거하려면 디지털 서명이 포함된 서명 필드의 이름을 지정해야 합니다. 또한 디지털 서명을 제거할 수 있는 권한이 있어야 합니다. 그렇지 않으면 예외가 발생합니다.

**PDF 문서를 PDF 파일로 저장**

서명 서비스가 서명 필드에서 디지털 서명을 제거한 후 PDF 문서를 PDF 파일로 저장하여 사용자가 Acrobat 또는 Adobe Reader에서 열 수 있습니다.

**참고 항목**

[Java API를 사용하여 디지털 서명 제거](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-java-api)

[웹 서비스 API를 사용하여 디지털 서명 제거](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[서명 필드 추가](digitally-signing-certifying-documents.md#adding-signature-fields)

### Java API를 사용하여 디지털 서명 제거 {#remove-digital-signatures-using-the-java-api}

서명 API(Java)를 사용하여 디지털 서명을 제거합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-signatures-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. 서명 클라이언트 만들기를 참조하십시오.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 개체를 `SignatureServiceClient` 만들고 개체를 `ServiceClientFactory` 전달합니다.

1. 제거할 서명이 포함된 PDF 문서 가져오기

   * 생성자를 사용하고 PDF 문서의 위치를 지정하는 문자열 값을 전달하여 제거할 서명이 포함된 PDF 문서를 나타내는 `java.io.FileInputStream` 객체를 만듭니다.
   * 생성자를 사용하여 개체를 `com.adobe.idp.Document` 만들고 개체를 `java.io.FileInputStream` 전달합니다.

1. 서명 필드에서 디지털 서명 제거

   객체의 메서드를 호출하고 다음 값을 전달하여 서명 필드에서 `SignatureServiceClient` 디지털 `clearSignatureField` 서명을 제거합니다.

   * 제거할 서명이 포함된 PDF 문서를 나타내는 `com.adobe.idp.Document` 개체입니다.
   * 디지털 서명이 포함된 서명 필드의 이름을 지정하는 문자열 값.

   이 방법 `clearSignatureField` 은 디지털 서명이 제거된 PDF 문서를 나타내는 `com.adobe.idp.Document` 개체를 반환합니다.

1. PDF 문서를 PDF 파일로 저장

   * 개체를 만들고 파일 확장자가 .pdf인지 확인합니다. `java.io.File`
   * 개체의 `com.adobe.idp.Document` 메서드를 `copyToFile` 호출합니다. 객체를 전달하여 객체 `java.io.File` 내용을 파일에 `com.adobe.idp.Document` 복사합니다. 메서드에서 반환된 `Document` 개체를 사용해야 `clearSignatureField` 합니다.

**참고 항목**

[디지털 서명 제거](digitally-signing-certifying-documents.md#removing-digital-signatures)

[빠른 시작(SOAP 모드): Java API를 사용하여 디지털 서명 제거](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-removing-a-digital-signature-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 디지털 서명 제거 {#remove-digital-signatures-using-the-web-service-api}

서명 API(웹 서비스)를 사용하여 디지털 서명을 제거합니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Forms `localhost` 를 호스팅하는 서버의 IP 주소로 대체합니다.

1. 서명 클라이언트 만들기

   * 기본 생성자를 사용하여 `SignatureServiceClient` 개체를 만듭니다.
   * 생성자를 사용하여 `SignatureServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/SignatureService?WSDL`). 속성을 사용할 필요는 `lc_version` 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * 필드의 값을 `System.ServiceModel.BasicHttpBinding` 가져와 개체를 `SignatureServiceClient.Endpoint.Binding` 만듭니다. 반환 값을 다음으로 캐스팅합니다 `BasicHttpBinding`.
   * 개체 `System.ServiceModel.BasicHttpBinding` 필드를 (으)로 `MessageEncoding` 설정합니다 `WSMessageEncoding.Mtom`. 이 값을 사용하면 MTOM이 사용됩니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM 양식 사용자 이름을 지정합니다 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 해당 암호 값을 필드에 지정합니다 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 필드에 상수 값 `HttpClientCredentialType.Basic` 을 지정합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 필드에 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly` 을 지정합니다 `BasicHttpBindingSecurity.Security.Mode`.

1. 제거할 서명이 포함된 PDF 문서 가져오기

   * 생성자를 사용하여 `BLOB` 개체를 만듭니다. 이 `BLOB` 개체는 제거할 디지털 서명이 포함된 PDF 문서를 저장하는 데 사용됩니다.
   * 생성자를 호출하고 서명된 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * 개체의 내용을 저장하는 바이트 배열을 `System.IO.FileStream` 만듭니다. 개체의 속성을 가져와 바이트 배열의 크기를 결정할 수 `System.IO.FileStream` `Length` 있습니다.
   * 개체의 메서드를 호출하여 바이트 배열을 스트림 데이터로 `System.IO.FileStream` 채웁니다 `Read` . 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 바이트 배열의 컨텐츠로 해당 `BLOB` `MTOM` 속성을 지정하여 개체를 채웁니다.

1. 서명 필드에서 디지털 서명 제거

   개체의 메서드를 호출하고 다음 값을 전달하여 `SignatureServiceClient` 디지털 서명을 `clearSignatureField` 제거합니다.

   * 서명된 PDF 문서를 포함하는 `BLOB` 개체입니다.
   * 제거할 디지털 서명이 포함된 서명 필드의 이름을 나타내는 문자열 값입니다.

   이 방법 `clearSignatureField` 은 디지털 서명이 제거된 PDF 문서를 나타내는 `BLOB` 개체를 반환합니다.

1. PDF 문서를 PDF 파일로 저장

   * 생성자를 호출하고 빈 서명 필드가 포함된 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * 메서드에서 반환된 개체의 내용을 저장하는 바이트 배열을 `BLOB` `sign` 만듭니다. 개체 데이터 멤버의 값을 가져와 바이트 배열 `BLOB` 을 `MTOM` 채웁니다.
   * 생성자를 호출하고 개체를 전달하여 `System.IO.BinaryWriter` 개체를 `System.IO.FileStream` 만듭니다.
   * 개체의 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열 내용을 PDF 파일에 `System.IO.BinaryWriter``Write` 씁니다.

**참고 항목**

[디지털 서명 제거](digitally-signing-certifying-documents.md#removing-digital-signatures)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
