---
title: PDF 문서 암호화 및 복호화
description: 암호화 서비스를 사용하여 문서를 암호화하고 해독합니다. 암호화 서비스 작업에는 암호로 PDF 문서 암호화, 인증서로 PDF 문서 암호화, PDF 문서에서 암호 기반 암호화 제거, PDF 문서에서 인증서 기반 암호화 제거, 다른 서비스 작업이 수행될 수 있도록 PDF 문서 잠금 해제, 보안 PDF 문서의 암호화 유형 결정 등이 포함된다.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: d3cbca7f-9277-4d61-b198-abf4bb008f15
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '8133'
ht-degree: 0%

---

# PDF 문서 암호화 및 복호화 {#encrypting-and-decrypting-pdf-documents}

**이 문서의 샘플과 예제는 JEE 환경의 AEM Forms에 대해서만 적용됩니다.**

**암호화 서비스 정보**

암호화 서비스를 사용하면 문서를 암호화하고 해독할 수 있습니다. 문서가 암호화되면 해당 내용을 읽을 수 없게 됩니다. 인가된 사용자는 문서의 암호를 해독하여 콘텐츠에 액세스할 수 있습니다. PDF 문서가 암호로 암호화된 경우 Adobe Reader 또는 Adobe Acrobat에서 문서를 보려면 열기 암호를 지정해야 합니다. 마찬가지로, PDF 문서가 인증서로 암호화되어 있는 경우, 사용자는 PDF 문서를 암호화하는 데 사용된 인증서(개인 키)에 해당하는 공개 키로 PDF 문서의 암호를 해독해야 합니다.

암호화 서비스를 사용하여 다음 작업을 수행할 수 있습니다.

* 암호로 PDF 문서를 암호화합니다. [암호를 사용하여 PDF 문서 암호화](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)를 참조하십시오.
* 인증서를 사용하여 PDF 문서를 암호화합니다. [인증서를 사용하여 PDF 문서 암호화](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)를 참조하십시오.
* PDF 문서에서 암호 기반 암호화를 제거합니다. ([암호 암호화 제거](encrypting-decrypting-pdf-documents.md#removing-password-encryption)를 참조하세요.)
* PDF 문서에서 인증서 기반 암호화를 제거합니다. [인증서 기반 암호화 제거](encrypting-decrypting-pdf-documents.md#removing-certificate-based-encryption)를 참조하십시오.
* 다른 서비스 작업을 수행할 수 있도록 PDF 문서의 잠금을 해제합니다. 예를 들어 암호로 암호화된 PDF 문서의 잠금이 해제된 후 디지털 서명을 적용할 수 있습니다. ([암호화된 PDF 문서 잠금 해제](encrypting-decrypting-pdf-documents.md#unlocking-encrypted-pdf-documents)를 참조하십시오.)
* 보안 PDF 문서의 암호화 유형을 확인합니다. [암호화 유형 확인](encrypting-decrypting-pdf-documents.md#determining-encryption-type)을 참조하세요.

>[!NOTE]
>
>암호화 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

## 암호로 PDF 문서 암호화 {#encrypting-pdf-documents-with-a-password}

암호를 사용하여 PDF 문서를 암호화할 때 사용자는 암호를 지정하여 Adobe Reader 또는 Acrobat에서 PDF 문서를 열어야 합니다. 또한 PDF 문서에 디지털 서명하는 것과 같은 다른 AEM Forms 작업을 문서에서 수행하려면 먼저 암호로 암호화된 PDF 문서의 잠금을 해제해야 합니다.

>[!NOTE]
>
>암호화된 PDF 문서를 AEM Forms 저장소에 업로드하면 PDF 문서의 암호를 해독하고 XDP 콘텐츠를 추출할 수 없습니다. AEM Forms 저장소에 문서를 업로드하기 전에 암호화하지 않는 것이 좋습니다. [리소스 쓰기](/help/forms/developing/aem-forms-repository.md#writing-resources)를 참조하세요.

>[!NOTE]
>
>암호화 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary-of-steps}

암호를 사용하여 PDF 문서를 암호화하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. 암호화 클라이언트 API 개체를 만듭니다.
1. 암호화할 PDF 문서를 가져옵니다.
1. 암호화 런타임 옵션을 설정합니다.
1. 암호를 추가합니다.
1. 암호화된 PDF 문서를 PDF 파일로 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필수)

**암호화 클라이언트 API 개체 만들기**

암호화 서비스 작업을 프로그래밍 방식으로 수행하려면 암호화 서비스 클라이언트를 만들어야 합니다.

**암호화할 PDF 문서 가져오기**

암호화되지 않은 PDF 문서를 가져와서 암호로 문서를 암호화합니다. 이미 암호화된 PDF 문서를 보호하려고 하면 예외가 발생합니다.

**암호화 실행 시간 옵션 설정**

암호로 PDF 문서를 암호화하려면 두 개의 암호 값을 포함하여 네 개의 값을 지정합니다. 첫 번째 암호 값은 PDF 문서를 암호화하는 데 사용되며 PDF 문서를 열 때 지정해야 합니다. 마스터 암호 값이라는 두 번째 암호 값은 PDF 문서에서 암호화를 제거하는 데 사용됩니다. 암호 값은 대/소문자를 구분하며 이 두 암호 값은 동일한 값일 수 없습니다.

암호화할 PDF 문서 리소스를 지정합니다. 전체 PDF 문서를 암호화할 수 있습니다. 문서의 메타데이터를 제외한 모든 항목이나 문서의 첨부 파일만 암호화할 수 있습니다. 문서의 첨부 파일만 암호화하면 사용자가 첨부 파일에 액세스하려고 할 때 암호를 입력하라는 메시지가 표시됩니다.

PDF 문서를 암호화할 때 보안 문서와 관련된 권한을 지정할 수 있습니다. 권한을 지정하면 암호로 암호화된 PDF 문서를 여는 사용자가 수행할 수 있는 작업을 제어할 수 있습니다. 예를 들어 양식 데이터를 성공적으로 추출하려면 다음 권한을 설정해야 합니다.

* PASSWORD_EDIT_ADD
* PASSWORD_EDIT_MODIFY

>[!NOTE]
>
>권한이 `PasswordEncryptionPermission` 열거형 값으로 지정되었습니다.

**암호 추가**

보안되지 않은 PDF 문서를 검색하고 암호화 런타임 값을 설정한 후 PDF 문서에 암호를 추가할 수 있습니다.

**암호화된 PDF 문서를 PDF 파일로 저장**

암호로 암호화된 PDF 문서를 PDF 파일로 저장할 수 있습니다.

**추가 참조**

[Java API를 사용하여 PDF 문서 암호화](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-using-the-java-api)

[웹 서비스 API를 사용하여 PDF 문서 암호화](encrypting-decrypting-pdf-documents.md#encrypting-a-pdf-document-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[암호화 서비스 API 빠른 시작](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[인증서를 사용하여 PDF 문서 암호화](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)

### Java API를 사용하여 PDF 문서 암호화 {#encrypt-a-pdf-document-using-the-java-api}

암호화 API(Java)를 사용하여 암호로 PDF 문서를 암호화합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-encryption-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. 암호화 클라이언트 API 만들기.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하고 `ServiceClientFactory` 개체를 전달하여 `EncryptionServiceClient` 개체를 만듭니다.

1. 암호화할 PDF 문서를 가져옵니다.

   * 생성자를 사용하고 PDF 문서의 위치를 지정하는 문자열 값을 전달하여 암호화할 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만듭니다.
   * 생성자를 사용하고 `java.io.FileInputStream` 개체를 전달하여 `com.adobe.idp.Document` 개체를 만듭니다.

1. 암호화 런타임 옵션을 설정합니다.

   * 해당 생성자를 호출하여 `PasswordEncryptionOptionSpec` 개체를 만듭니다.
   * `PasswordEncryptionOptionSpec` 개체의 `setEncryptOption` 메서드를 호출하고 암호화할 문서 리소스를 지정하는 `PasswordEncryptionOption` 열거형 값을 전달하여 암호화할 PDF 문서 리소스를 지정하십시오. 예를 들어 메타데이터와 첨부 파일을 포함하여 전체 PDF 문서를 암호화하려면 `PasswordEncryptionOption.ALL`을(를) 지정합니다.
   * `ArrayList` 생성자를 사용하여 암호화 권한을 저장하는 `java.util.List` 개체를 만듭니다.
   * `java.util.List` 개체의 `add` 메서드를 호출하고 설정할 권한에 해당하는 열거형 값을 전달하여 권한을 지정하십시오. 예를 들어 사용자가 PDF 문서의 데이터를 복사할 수 있도록 하는 권한을 설정하려면 `PasswordEncryptionPermission.PASSWORD_EDIT_COPY`을(를) 지정하십시오. 설정할 각 권한에 대해 이 단계를 반복합니다.
   * `PasswordEncryptionOptionSpec` 개체의 `setCompatability` 메서드를 호출하고 Acrobat 호환성 수준을 지정하는 열거형 값을 전달하여 Acrobat 호환성 옵션을 지정하십시오. 예를 들어 `PasswordEncryptionCompatability.ACRO_7`을(를) 지정할 수 있습니다.
   * `PasswordEncryptionOptionSpec` 개체의 `setDocumentOpenPassword` 메서드를 호출하고 열린 암호를 나타내는 문자열 값을 전달하여 사용자가 암호화된 PDF 문서를 열 수 있도록 해주는 암호 값을 지정하십시오.
   * 사용자가 `PasswordEncryptionOptionSpec` 개체의 `setPermissionPassword` 메서드를 호출하고 마스터 암호를 나타내는 문자열 값을 전달하여 PDF 문서에서 암호화를 제거할 수 있도록 하는 마스터 암호 값을 지정하십시오.

1. 암호를 추가합니다.

   `EncryptionServiceClient` 개체의 `encryptPDFUsingPassword` 메서드를 호출하고 다음 값을 전달하여 PDF 문서를 암호화합니다.

   * 암호로 암호화할 PDF 문서가 포함된 `com.adobe.idp.Document` 개체입니다.
   * 암호화 런타임 옵션이 포함된 `PasswordEncryptionOptionSpec` 개체입니다.

   `encryptPDFUsingPassword` 메서드가 암호로 암호화된 PDF 문서를 포함하는 `com.adobe.idp.Document` 개체를 반환합니다.

1. 암호화된 PDF 문서를 PDF 파일로 저장합니다.

   * `java.io.File` 개체를 만들고 파일 확장명이 .pdf인지 확인하십시오.
   * `com.adobe.idp.Document` 개체의 `copyToFile` 메서드를 호출하여 `com.adobe.idp.Document` 개체의 내용을 파일에 복사합니다. `encryptPDFUsingPassword` 메서드에서 반환된 `com.adobe.idp.Document` 개체를 사용하는지 확인하십시오.

**추가 참조**

[단계 요약](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[빠른 시작(SOAP 모드): Java API를 사용하여 PDF 문서 암호화](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)


[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 PDF 문서 암호화 {#encrypting-a-pdf-document-using-the-web-service-api}

암호화 API(웹 서비스)를 사용하여 암호로 PDF 문서를 암호화합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. WSDL 정의 `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`을(를) 사용하는지 확인하십시오.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꾸십시오.

1. 암호화 클라이언트 API 개체를 만듭니다.

   * 기본 생성자를 사용하여 `EncryptionServiceClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `EncryptionServiceClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/EncryptionService?WSDL`). `lc_version` 특성은 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * `EncryptionServiceClient.Endpoint.Binding` 필드의 값을 가져와 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`(으)로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * `EncryptionServiceClient.ClientCredentials.UserName.UserName` 필드에 AEM Forms 사용자 이름을 지정하십시오.
      * 필드 `EncryptionServiceClient.ClientCredentials.UserName.Password`에 해당 암호 값을 지정하십시오.
      * 상수 값 `HttpClientCredentialType.Basic`을(를) 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.
      * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을(를) 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. 암호화할 PDF 문서를 가져옵니다.

   * 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 암호로 암호화된 PDF 문서를 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하고 암호화할 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * 바이트 배열의 내용을 `BLOB` 개체의 `MTOM` 데이터 멤버에 할당하여 `BLOB` 개체를 채웁니다.

1. 암호화 런타임 옵션을 설정합니다.

   * 해당 생성자를 사용하여 `PasswordEncryptionOptionSpec` 개체를 만듭니다.
   * `PasswordEncryptionOption` 열거형 값을 `PasswordEncryptionOptionSpec` 개체의 `encryptOption` 데이터 멤버에 할당하여 암호화할 PDF 문서 리소스를 지정하십시오. 메타데이터 및 첨부 파일을 포함하여 전체 PDF을 암호화하려면 이 데이터 멤버에 `PasswordEncryptionOption.ALL`을(를) 지정하십시오.
   * `PasswordEncryptionCompatability` 열거형 값을 `PasswordEncryptionOptionSpec` 개체의 `compatability` 데이터 멤버에 할당하여 Acrobat 호환성 옵션을 지정하십시오. 예를 들어 이 데이터 멤버에 `PasswordEncryptionCompatability.ACRO_7`을(를) 할당합니다.
   * `PasswordEncryptionOptionSpec` 개체의 `documentOpenPassword` 데이터 멤버에 열린 암호를 나타내는 문자열 값을 할당하여 사용자가 암호화된 PDF 문서를 열 수 있도록 하는 암호 값을 지정하십시오.
   * 마스터 암호를 나타내는 문자열 값을 `PasswordEncryptionOptionSpec` 개체의 `permissionPassword` 데이터 멤버에 할당하여 사용자가 PDF 문서에서 암호화를 제거할 수 있는 암호 값을 지정하십시오.

1. 암호를 추가합니다.

   `EncryptionServiceClient` 개체의 `encryptPDFUsingPassword` 메서드를 호출하고 다음 값을 전달하여 PDF 문서를 암호화합니다.

   * 암호로 암호화할 PDF 문서가 포함된 `BLOB` 개체입니다.
   * 암호화 런타임 옵션이 포함된 `PasswordEncryptionOptionSpec` 개체입니다.

   `encryptPDFUsingPassword` 메서드가 암호로 암호화된 PDF 문서를 포함하는 `BLOB` 개체를 반환합니다.

1. 암호화된 PDF 문서를 PDF 파일로 저장합니다.

   * 해당 생성자를 호출하고 보안 PDF 문서의 파일 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `encryptPDFUsingPassword` 메서드에서 반환된 `BLOB` 개체의 데이터 내용을 저장하는 바이트 배열을 만듭니다. `BLOB` 개체의 `MTOM` 데이터 멤버의 값을 가져와서 바이트 배열을 채웁니다.
   * 해당 생성자를 호출하고 `System.IO.FileStream` 개체를 전달하여 `System.IO.BinaryWriter` 개체를 만듭니다.
   * `System.IO.BinaryWriter` 개체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 PDF 파일에 씁니다.

**추가 참조**

[단계 요약](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 인증서를 사용하여 PDF 문서 암호화 {#encrypting-pdf-documents-with-certificates}

인증서 기반 암호화를 사용하면 공개 키 기술을 사용하여 특정 수신자의 문서를 암호화할 수 있습니다. 다양한 수신자에게 문서에 대한 다양한 권한을 부여할 수 있습니다. 암호화의 많은 측면들은 공개 키 기술에 의해 가능해진다. 알고리즘은 다음 속성을 가진 두 개의 큰 숫자(*키*)를 생성하는 데 사용됩니다.

* 하나의 키는 데이터 집합을 암호화하는 데 사용됩니다. 그런 다음 다른 키만 사용하여 데이터를 해독할 수 있습니다.
* 하나의 키를 다른 키와 구별하는 것은 불가능하다.

키 중 하나가 사용자의 개인 키로 작동합니다. 사용자만 이 키에 액세스할 수 있습니다. 다른 키는 다른 사용자와 공유할 수 있는 사용자의 공개 키입니다.

공개 키 인증서에는 사용자의 공개 키와 식별 정보가 포함되어 있습니다. X.509 형식은 인증서를 저장하는 데 사용됩니다. 인증서는 일반적으로 인증서의 유효성에 대한 신뢰도를 측정하는 인증된 엔티티인 CA(인증 기관)에서 발급하고 디지털 서명합니다. 인증서에는 만료 날짜가 있으며, 그 이후에는 더 이상 유효하지 않습니다. 또한 CRL(인증서 해지 목록)은 만료일 이전에 해지된 인증서에 대한 정보를 제공합니다. CRL은 인증 기관에 의해 주기적으로 게시됩니다. 네트워크의 OCSP(온라인 인증서 상태 프로토콜)를 통해 인증서의 해지 상태를 검색할 수도 있습니다.

>[!NOTE]
>
>암호화된 PDF 문서를 AEM Forms 저장소에 업로드하면 PDF 문서의 암호를 해독하고 XDP 콘텐츠를 추출할 수 없습니다. AEM Forms 저장소에 문서를 업로드하기 전에 암호화하지 않는 것이 좋습니다. [리소스 쓰기](/help/forms/developing/aem-forms-repository.md#writing-resources)를 참조하세요.

>[!NOTE]
>
>인증서를 사용하여 PDF 문서를 암호화하려면 먼저 인증서를 AEM Forms에 추가해야 합니다. 인증서는 관리 콘솔을 사용하거나 Trust Manager API를 프로그래밍 방식으로 사용하여 추가됩니다. [Trust Manager API를 사용하여 자격 증명 가져오기](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)를 참조하십시오.

>[!NOTE]
>
>암호화 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary_of_steps-1}

인증서를 사용하여 PDF 문서를 암호화하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. 암호화 클라이언트 API 개체를 만듭니다.
1. 암호화할 PDF 문서를 가져옵니다.
1. 인증서를 참조합니다.
1. 암호화 런타임 옵션을 설정합니다.
1. 인증서로 암호화된 PDF 문서를 만듭니다.
1. 암호화된 PDF 문서를 PDF 파일로 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss 애플리케이션 서버에 배포된 경우 필요)
* jbossall-client.jar(AEM Forms이 JBoss 애플리케이션 서버에 배포된 경우 필수)

**암호화 클라이언트 API 개체 만들기**

암호화 서비스 작업을 프로그래밍 방식으로 수행하려면 암호화 서비스 클라이언트를 만들어야 합니다. Java 암호화 서비스 API를 사용하는 경우 `EncrytionServiceClient` 개체를 만드십시오. 웹 서비스 암호화 서비스 API를 사용하는 경우 `EncryptionServiceService` 개체를 만드십시오.

**암호화할 PDF 문서 가져오기**

암호화할 암호화되지 않은 PDF 문서를 가져옵니다. 이미 암호화된 PDF 문서를 보호하려고 하면 예외가 발생합니다.

**인증서 참조**

인증서를 사용하여 PDF 문서를 암호화하려면 PDF 문서를 암호화하는 데 사용되는 인증서를 참조하십시오. 인증서는 .cer 파일, .crt 파일 또는 .pem 파일입니다. PKCS#12 파일은 해당 인증서와 함께 개인 키를 저장하는 데 사용됩니다.

인증서를 사용하여 PDF 문서를 암호화할 때 보안 문서와 연결된 권한을 지정합니다. 권한을 지정하면 인증서로 암호화된 PDF 문서를 여는 사용자가 수행할 수 있는 작업을 제어할 수 있습니다.

**암호화 실행 시간 옵션 설정**

암호화할 PDF 문서 리소스를 지정합니다. 전체 PDF 문서, 문서의 메타데이터를 제외한 모든 문서 또는 문서의 첨부 파일만 암호화할 수 있습니다.

**인증서로 암호화된 PDF 문서 만들기**

보안되지 않은 PDF 문서를 검색하고 인증서를 참조한 다음 런타임 옵션을 설정하면 인증서로 암호화된 PDF 문서를 만들 수 있습니다. PDF 문서가 암호화되면 암호를 해독하기 위해 해당 공개 키가 필요합니다.

**암호화된 PDF 문서를 PDF 파일로 저장**

암호화된 PDF 문서를 PDF 파일로 저장할 수 있습니다.

**추가 참조**

[Java API를 사용하여 인증서로 PDF 문서 암호화](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-java-api)

[웹 서비스 API를 사용하여 인증서로 PDF 문서 암호화](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[암호화 서비스 API 빠른 시작](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[암호로 PDF 문서 암호화](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Java API를 사용하여 인증서로 PDF 문서 암호화 {#encrypt-a-pdf-document-with-a-certificate-using-the-java-api}

암호화 API(Java)를 사용하여 인증서로 PDF 문서를 암호화합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-encryption-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. 암호화 클라이언트 API 개체를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하고 `ServiceClientFactory` 개체를 전달하여 `EncryptionServiceClient` 개체를 만듭니다.

1. 암호화할 PDF 문서를 가져옵니다.

   * 생성자를 사용하고 PDF 문서의 위치를 지정하는 문자열 값을 전달하여 암호화할 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만듭니다.
   * 생성자를 사용하고 `java.io.FileInputStream` 개체를 전달하여 `com.adobe.idp.Document` 개체를 만듭니다.

1. 인증서를 참조합니다.

   * 해당 생성자를 사용하여 권한 정보를 저장하는 `java.util.List` 개체를 만듭니다.
   * `java.util.List` 개체의 `add` 메서드를 호출하고 보안 PDF 문서를 여는 사용자에게 부여된 권한을 나타내는 `CertificateEncryptionPermissions` 열거 값을 전달하여 암호화된 문서와 관련된 권한을 지정하십시오. 예를 들어 모든 권한을 지정하려면 `CertificateEncryptionPermissions.PKI_ALL_PERM`을(를) 전달하십시오.
   * 해당 생성자를 사용하여 `Recipient` 개체를 만듭니다.
   * 생성자를 사용하고 인증서의 위치를 지정하는 문자열 값을 전달하여 PDF 문서를 암호화하는 데 사용되는 인증서를 나타내는 `java.io.FileInputStream` 개체를 만듭니다.
   * 생성자를 사용하고 인증서를 나타내는 `java.io.FileInputStream` 개체를 전달하여 `com.adobe.idp.Document` 개체를 만듭니다.
   * `Recipient` 개체의 `setX509Cert` 메서드를 호출하고 인증서가 포함된 `com.adobe.idp.Document` 개체를 전달하십시오. 또한 `Recipient` 개체는 인증서 소스로 Truststore 인증서 별칭 또는 LDAP URL을 가질 수 있습니다.
   * 생성자를 사용하여 권한 및 인증서 정보를 저장하는 `CertificateEncryptionIdentity` 개체를 만듭니다.
   * `CertificateEncryptionIdentity` 개체의 `setPerms` 메서드를 호출하고 권한 정보를 저장하는 `java.util.List` 개체를 전달하십시오.
   * `CertificateEncryptionIdentity` 개체의 `setRecipient` 메서드를 호출하고 인증서 정보를 저장하는 `Recipient` 개체를 전달하십시오.
   * 생성자를 사용하여 인증서 정보를 저장하는 `java.util.List` 개체를 만듭니다.
   * `java.util.List` 개체의 추가 메서드를 호출하고 `CertificateEncryptionIdentity` 개체를 전달합니다. 이 `java.util.List` 개체는 `encryptPDFUsingCertificates` 메서드에 매개 변수로 전달됩니다.

1. 암호화 런타임 옵션을 설정합니다.

   * 해당 생성자를 호출하여 `CertificateEncryptionOptionSpec` 개체를 만듭니다.
   * `CertificateEncryptionOptionSpec` 개체의 `setOption` 메서드를 호출하고 암호화할 문서 리소스를 지정하는 `CertificateEncryptionOption` 열거형 값을 전달하여 암호화할 PDF 문서 리소스를 지정하십시오. 예를 들어 메타데이터와 첨부 파일을 포함하여 전체 PDF 문서를 암호화하려면 `CertificateEncryptionOption.ALL`을(를) 지정합니다.
   * `CertificateEncryptionOptionSpec` 개체의 `setCompat` 메서드를 호출하고 Acrobat 호환성 수준을 지정하는 `CertificateEncryptionCompatibility` 열거형 값을 전달하여 Acrobat 호환성 옵션을 지정하십시오. 예를 들어 `CertificateEncryptionCompatibility.ACRO_7`을(를) 지정할 수 있습니다.

1. 인증서로 암호화된 PDF 문서를 만듭니다.

   `EncryptionServiceClient` 개체의 `encryptPDFUsingCertificates` 메서드를 호출하고 다음 값을 전달하여 인증서로 PDF 문서를 암호화합니다.

   * 암호화할 PDF 문서가 포함된 `com.adobe.idp.Document` 개체입니다.
   * 인증서 정보를 저장하는 `java.util.List` 개체입니다.
   * 암호화 런타임 옵션이 포함된 `CertificateEncryptionOptionSpec` 개체입니다.

   `encryptPDFUsingCertificates` 메서드가 인증서로 암호화된 PDF 문서를 포함하는 `com.adobe.idp.Document` 개체를 반환합니다.

1. 암호화된 PDF 문서를 PDF 파일로 저장합니다.

   * `java.io.File` 개체를 만들고 파일 이름 확장명이 .pdf인지 확인하십시오.
   * `com.adobe.idp.Document` 개체의 `copyToFile` 메서드를 호출하여 `com.adobe.idp.Document` 개체의 내용을 파일에 복사합니다. `encryptPDFUsingCertificates` 메서드에서 반환된 `com.adobe.idp.Document` 개체를 사용하는지 확인하십시오.

**추가 참조**

[단계 요약](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[빠른 시작(SOAP 모드): Java API를 사용하여 인증서로 PDF 문서 암호화](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 인증서로 PDF 문서 암호화 {#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api}

암호화 API(웹 서비스)를 사용하여 인증서로 PDF 문서를 암호화합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. WSDL 정의 `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`을(를) 사용하는지 확인하십시오.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꾸십시오.

1. 암호화 클라이언트 API 개체를 만듭니다.

   * 기본 생성자를 사용하여 `EncryptionServiceClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `EncryptionServiceClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/EncryptionService?WSDL`). `lc_version` 특성은 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * `EncryptionServiceClient.Endpoint.Binding` 필드의 값을 가져와 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`(으)로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * `EncryptionServiceClient.ClientCredentials.UserName.UserName` 필드에 AEM Forms 사용자 이름을 지정하십시오.
      * 필드 `EncryptionServiceClient.ClientCredentials.UserName.Password`에 해당 암호 값을 지정하십시오.
      * 상수 값 `HttpClientCredentialType.Basic`을(를) 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.
      * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을(를) 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. 암호화할 PDF 문서를 가져옵니다.

   * 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 인증서로 암호화된 PDF 문서를 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하고 암호화할 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * 해당 `MTOM` 속성을 바이트 배열의 내용으로 할당하여 `BLOB` 개체를 채웁니다.

1. 인증서를 참조합니다.

   * 해당 생성자를 사용하여 `Recipient` 개체를 만듭니다. 이 개체는 인증서 정보를 저장합니다.
   * 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다. 이 `BLOB` 개체는 PDF 문서를 암호화하는 인증서를 저장합니다.
   * 해당 생성자를 호출하고 인증서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * 바이트 배열의 내용을 `BLOB` 개체의 `MTOM` 데이터 멤버에 할당하여 `BLOB` 개체를 채웁니다.
   * 인증서를 저장하는 `BLOB` 개체를 `Recipient` 개체의 `x509Cert` 데이터 멤버에 할당합니다.
   * 생성자를 사용하여 인증서 정보를 저장하는 `CertificateEncryptionIdentity` 개체를 만듭니다.
   * 인증서를 저장하는 `Recipient` 개체를 `CertificateEncryptionIdentity`개체의 받는 사람 데이터 멤버에 할당하십시오.
   * `Object` 배열을 만들고 `CertificateEncryptionIdentity` 개체를 `Object` 배열의 첫 번째 요소에 할당합니다. 이 `Object` 배열은 `encryptPDFUsingCertificates` 메서드에 매개 변수로 전달됩니다.

1. 암호화 런타임 옵션을 설정합니다.

   * 해당 생성자를 사용하여 `CertificateEncryptionOptionSpec` 개체를 만듭니다.
   * `CertificateEncryptionOption` 열거형 값을 `CertificateEncryptionOptionSpec` 개체의 `option` 데이터 멤버에 할당하여 암호화할 PDF 문서 리소스를 지정하십시오. 메타데이터 및 첨부 파일을 포함하여 전체 PDF 문서를 암호화하려면 이 데이터 멤버에 `CertificateEncryptionOption.ALL`을(를) 지정하십시오.
   * `CertificateEncryptionCompatibility` 열거형 값을 `CertificateEncryptionOptionSpec` 개체의 `compat` 데이터 멤버에 할당하여 Acrobat 호환성 옵션을 지정하십시오. 예를 들어 이 데이터 멤버에 `CertificateEncryptionCompatibility.ACRO_7`을(를) 할당합니다.

1. 인증서로 암호화된 PDF 문서를 만듭니다.

   `EncryptionServiceService` 개체의 `encryptPDFUsingCertificates` 메서드를 호출하고 다음 값을 전달하여 인증서로 PDF 문서를 암호화합니다.

   * 암호화할 PDF 문서가 포함된 `BLOB` 개체입니다.
   * 인증서 정보를 저장하는 `Object` 배열입니다.
   * 암호화 런타임 옵션이 포함된 `CertificateEncryptionOptionSpec` 개체입니다.

   `encryptPDFUsingCertificates` 메서드가 인증서로 암호화된 PDF 문서를 포함하는 `BLOB` 개체를 반환합니다.

1. 암호화된 PDF 문서를 PDF 파일로 저장합니다.

   * 해당 생성자를 호출하고 보안 PDF 문서의 파일 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `encryptPDFUsingCertificates` 메서드에서 반환된 `BLOB` 개체의 데이터 내용을 저장하는 바이트 배열을 만듭니다. `BLOB` 개체의 `binaryData` 데이터 멤버의 값을 가져와서 바이트 배열을 채웁니다.
   * 해당 생성자를 호출하고 `System.IO.FileStream` 개체를 전달하여 `System.IO.BinaryWriter` 개체를 만듭니다.
   * `System.IO.BinaryWriter` 개체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 PDF 파일에 씁니다.

**추가 참조**

[단계 요약](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 인증서 기반 암호화 제거 {#removing-certificate-based-encryption}

사용자가 Adobe Reader 또는 Acrobat에서 PDF 문서를 열 수 있도록 PDF 문서에서 인증서 기반 암호화를 제거할 수 있습니다. 인증서로 암호화된 PDF 문서에서 암호화를 제거하려면 공개 키를 참조해야 합니다. PDF 문서에서 암호화가 제거되면 더 이상 안전하지 않습니다.

>[!NOTE]
>
>암호화 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary_of_steps-2}

PDF 문서에서 인증서 기반 암호화를 제거하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. 암호화 서비스 클라이언트를 만듭니다.
1. 암호화된 PDF 문서를 가져옵니다.
1. 암호화를 제거합니다.
1. PDF 문서를 PDF 파일로 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss 애플리케이션 서버에 배포된 경우 필요)
* jbossall-client.jar(AEM Forms이 JBoss 애플리케이션 서버에 배포된 경우 필수)

**암호화 서비스 클라이언트 만들기**

암호화 서비스 작업을 프로그래밍 방식으로 수행하려면 암호화 서비스 클라이언트를 만들어야 합니다. Java 암호화 서비스 API를 사용하는 경우 `EncrytionServiceClient` 개체를 만드십시오. 웹 서비스 암호화 서비스 API를 사용하는 경우 `EncryptionServiceService` 개체를 만드십시오.

**암호화된 PDF 문서 가져오기**

인증서 기반 암호화를 제거하려면 암호화된 PDF 문서를 가져옵니다. 암호화되지 않은 PDF 문서에서 암호화를 제거하려고 하면 예외가 발생합니다. 마찬가지로 암호로 암호화된 문서에서 인증서 기반 암호화를 제거하려고 하면 예외가 발생합니다.

**암호화 제거**

암호화된 PDF 문서에서 인증서 기반 암호화를 제거하려면 암호화된 PDF 문서와 PDF 문서를 암호화하는 데 사용된 키에 해당하는 개인 키가 모두 필요합니다. 개인 키의 별칭 값은 암호화된 PDF 문서에서 인증서 기반 암호화를 제거할 때 지정됩니다. 공개 키에 대한 자세한 내용은 [인증서를 사용하여 PDF 문서 암호화](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)를 참조하십시오.

>[!NOTE]
>
>개인 키는 AEM Forms Trust Store에 저장됩니다. 인증서가 배치되면 별칭 값이 지정됩니다.

**PDF 문서 저장**

암호화된 PDF 문서에서 인증서 기반 암호화를 제거한 후 PDF 문서를 PDF 파일로 저장할 수 있습니다. 사용자는 Adobe Reader 또는 Acrobat에서 PDF 문서를 열 수 있습니다.

**추가 참조**

[Java API를 사용하여 인증서 기반 암호화 제거](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-java-api)

[웹 서비스 API를 사용하여 인증서 기반 암호화 제거](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[암호화 서비스 API 빠른 시작](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Java API를 사용하여 인증서 기반 암호화 제거 {#remove-certificate-based-encryption-using-the-java-api}

암호화 API(Java)를 사용하여 PDF 문서에서 인증서 기반 암호화를 제거합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-encryption-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. 암호화 서비스 클라이언트를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하고 `ServiceClientFactory` 개체를 전달하여 `EncryptionServiceClient` 개체를 만듭니다.

1. 암호화된 PDF 문서를 가져옵니다.

   * 생성자를 사용하고 암호화된 PDF 문서의 위치를 지정하는 문자열 값을 전달하여 암호화된 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만듭니다.
   * 생성자를 사용하고 `java.io.FileInputStream` 개체를 전달하여 `com.adobe.idp.Document` 개체를 만듭니다.

1. 암호화를 제거합니다.

   `EncryptionServiceClient` 개체의 `removePDFCertificateSecurity` 메서드를 호출하고 다음 값을 전달하여 PDF 문서에서 인증서 기반 암호화를 제거합니다.

   * 암호화된 PDF 문서를 포함하는 `com.adobe.idp.Document` 개체입니다.
   * PDf 문서 암호화에 사용된 키에 해당하는 개인 키의 별칭 이름을 지정하는 문자열 값입니다.

   `removePDFCertificateSecurity` 메서드가 보안되지 않은 PDF 문서를 포함하는 `com.adobe.idp.Document` 개체를 반환합니다.

1. PDF 문서를 저장합니다.

   * `java.io.File` 개체를 만들고 파일 확장명이 .pdf인지 확인하십시오.
   * `com.adobe.idp.Document` 개체의 `copyToFile` 메서드를 호출하여 `Document` 개체의 내용을 파일에 복사합니다. `removePDFCredentialSecurity` 메서드에서 반환된 `com.adobe.idp.Document` 개체를 사용하는지 확인하십시오.

**추가 참조**

[단계 요약](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[빠른 시작(SOAP 모드): Java API를 사용하여 인증서 기반 암호화 제거](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-certificate-based-encryption-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 인증서 기반 암호화 제거 {#remove-certificate-based-encryption-using-the-web-service-api}

암호화 API(웹 서비스)를 사용하여 인증서 기반 암호화를 제거합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. WSDL 정의 `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`을(를) 사용하는지 확인하십시오.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꾸십시오.

1. 암호화 서비스 클라이언트를 만듭니다.

   * 기본 생성자를 사용하여 `EncryptionServiceClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `EncryptionServiceClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/EncryptionService?WSDL`). `lc_version` 특성은 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * `EncryptionServiceClient.Endpoint.Binding` 필드의 값을 가져와 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`(으)로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * `EncryptionServiceClient.ClientCredentials.UserName.UserName` 필드에 AEM Forms 사용자 이름을 지정하십시오.
      * 필드 `EncryptionServiceClient.ClientCredentials.UserName.Password`에 해당 암호 값을 지정하십시오.
      * 상수 값 `HttpClientCredentialType.Basic`을(를) 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.
      * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을(를) 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. 암호화된 PDF 문서를 가져옵니다.

   * 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 암호화된 PDF 문서를 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하고 암호화된 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * 바이트 배열의 내용을 `BLOB` 개체의 `MTOM` 데이터 멤버에 할당하여 `BLOB` 개체를 채웁니다.

1. 암호화를 제거합니다.

   `EncryptionServiceClient` 개체의 `removePDFCertificateSecurity` 메서드를 호출하고 다음 값을 전달하십시오.

   * 암호화된 PDF 문서를 나타내는 파일 스트림 데이터를 포함하는 `BLOB` 개체입니다.
   * PDf 문서를 암호화하는 데 사용되는 개인 키에 해당하는 공개 키의 별칭 이름을 지정하는 문자열 값입니다.

   `removePDFCredentialSecurity` 메서드가 보안되지 않은 PDF 문서를 포함하는 `BLOB` 개체를 반환합니다.

1. PDF 문서를 저장합니다.

   * 해당 생성자를 호출하고 보안되지 않은 PDF 문서의 파일 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `removePDFPasswordSecurity` 메서드에서 반환된 `BLOB` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `BLOB` 개체의 `MTOM` 데이터 멤버의 값을 가져와서 바이트 배열을 채웁니다.
   * 해당 생성자를 호출하고 `System.IO.FileStream` 개체를 전달하여 `System.IO.BinaryWriter` 개체를 만듭니다.
   * `System.IO.BinaryWriter` 개체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 PDF 파일에 씁니다.

**추가 참조**

[단계 요약](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 암호 암호화 제거 {#removing-password-encryption}

사용자가 암호를 지정하지 않고도 Adobe Reader 또는 Acrobat에서 PDF 문서를 열 수 있도록 PDF 문서에서 암호 기반 암호화를 제거할 수 있습니다. PDF 문서에서 암호 기반 암호화를 제거하면 문서가 더 이상 안전하지 않습니다.

>[!NOTE]
>
>암호화 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary_of_steps-3}

PDF 문서에서 암호 기반 암호화를 제거하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. 암호화 서비스 클라이언트를 만듭니다.
1. 암호화된 PDF 문서를 가져옵니다.
1. 암호를 제거합니다.
1. PDF 문서를 PDF 파일로 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필수)

**암호화 서비스 클라이언트 만들기**

암호화 서비스 작업을 프로그래밍 방식으로 수행하려면 암호화 서비스 클라이언트를 만들어야 합니다. Java 암호화 서비스 API를 사용하는 경우 `EncrytionServiceClient` 개체를 만드십시오. 웹 서비스 암호화 서비스 API를 사용하는 경우 `EncryptionServiceService` 개체를 만드십시오.

**암호화된 PDF 문서 가져오기**

암호 기반 암호화를 제거하려면 암호화된 PDF 문서를 가져옵니다. 암호화되지 않은 PDF 문서에서 암호화를 제거하려고 하면 예외가 발생합니다.

**암호 제거**

암호화된 PDF 문서에서 암호 기반 암호화를 제거하려면 암호화된 PDF 문서와 PDF 문서에서 암호화를 제거하는 데 사용되는 마스터 암호 값이 모두 필요합니다. 암호로 암호화된 PDF 문서를 여는 데 사용되는 암호는 암호화를 제거하는 데 사용할 수 없습니다. 마스터 암호는 PDF 문서를 암호로 암호화할 때 지정됩니다. [암호를 사용하여 PDF 문서 암호화](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)를 참조하십시오.

**PDF 문서 저장**

암호화 서비스가 PDF 문서에서 암호 기반 암호화를 제거한 후 PDF 문서를 PDF 파일로 저장할 수 있습니다. 사용자는 암호를 지정하지 않고 Adobe Reader 또는 Acrobat에서 PDF 문서를 열 수 있습니다.

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[암호화 서비스 API 빠른 시작](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[암호로 PDF 문서 암호화](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Java API를 사용하여 암호 기반 암호화 제거 {#remove-password-based-encryption-using-the-java-api}

암호화 API(Java)를 사용하여 PDF 문서에서 암호 기반 암호화를 제거합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-encryption-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. 암호화 서비스 클라이언트를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하고 `ServiceClientFactory` 개체를 전달하여 `EncryptionServiceClient` 개체를 만듭니다.

1. 암호화된 PDF 문서를 가져옵니다.

   * 생성자를 사용하고 PDF 문서의 위치를 지정하는 문자열 값을 전달하여 암호화된 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만듭니다.
   * 생성자를 사용하고 `java.io.FileInputStream` 개체를 전달하여 `com.adobe.idp.Document` 개체를 만듭니다.

1. 암호를 제거합니다.

   `EncryptionServiceClient` 개체의 `removePDFPasswordSecurity` 메서드를 호출하고 다음 값을 전달하여 PDF 문서에서 암호 기반 암호화를 제거합니다.

   * 암호화된 PDF 문서를 포함하는 `com.adobe.idp.Document` 개체입니다.
   * PDF 문서에서 암호화를 제거하는 데 사용되는 마스터 암호 값을 지정하는 문자열 값입니다.

   `removePDFPasswordSecurity` 메서드가 보안되지 않은 PDF 문서를 포함하는 `com.adobe.idp.Document` 개체를 반환합니다.

1. PDF 문서를 저장합니다.

   * `java.io.File` 개체를 만들고 파일 이름 확장명이 .pdf인지 확인하십시오.
   * `com.adobe.idp.Document` 개체의 `copyToFile` 메서드를 호출하여 `Document` 개체의 내용을 파일에 복사합니다. `removePDFPasswordSecurity` 메서드에서 반환된 `Document` 개체를 사용하는지 확인하십시오.

**추가 참조**

[빠른 시작(SOAP 모드): Java API를 사용하여 암호 기반 암호화 제거](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api)

### 웹 서비스 API를 사용하여 암호 기반 암호화 제거 {#remove-password-based-encryption-using-the-web-service-api}

암호화 API(웹 서비스)를 사용하여 암호 기반 암호화를 제거합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. WSDL 정의 `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`을(를) 사용하는지 확인하십시오.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꾸십시오.

1. 암호화 서비스 클라이언트를 만듭니다.

   * 기본 생성자를 사용하여 `EncryptionServiceClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `EncryptionServiceClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/EncryptionService?WSDL`). `lc_version` 특성은 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * `EncryptionServiceClient.Endpoint.Binding` 필드의 값을 가져와 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`(으)로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * `EncryptionServiceClient.ClientCredentials.UserName.UserName` 필드에 AEM Forms 사용자 이름을 지정하십시오.
      * 필드 `EncryptionServiceClient.ClientCredentials.UserName.Password`에 해당 암호 값을 지정하십시오.
      * 상수 값 `HttpClientCredentialType.Basic`을(를) 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.
      * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을(를) 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. 암호화된 PDF 문서를 가져옵니다.

   * 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 암호로 암호화된 PDF 문서를 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하고 암호화된 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * 바이트 배열의 내용을 `BLOB` 개체의 `MTOM` 데이터 멤버에 할당하여 `BLOB` 개체를 채웁니다.

1. 암호를 제거합니다.

   `EncryptionServiceService` 개체의 `removePDFPasswordSecurity` 메서드를 호출하고 다음 값을 전달하십시오.

   * 암호화된 PDF 문서를 나타내는 파일 스트림 데이터를 포함하는 `BLOB` 개체입니다.
   * PDF 문서에서 암호화를 제거하는 데 사용되는 암호 값을 지정하는 문자열 값입니다. 이 값은 암호로 PDF 문서를 암호화할 때 지정됩니다.

   `removePDFPasswordSecurity` 메서드가 보안되지 않은 PDF 문서를 포함하는 `BLOB` 개체를 반환합니다.

1. PDF 문서를 저장합니다.

   * 해당 생성자를 호출하고 보안되지 않은 PDF 문서의 파일 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `removePDFPasswordSecurity` 메서드에서 반환된 `BLOB` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `BLOB` 개체의 `MTOM` 데이터 멤버의 값을 가져와서 바이트 배열을 채웁니다.
   * 해당 생성자를 호출하고 `System.IO.FileStream` 개체를 전달하여 `System.IO.BinaryWriter` 개체를 만듭니다.
   * `System.IO.BinaryWriter` 개체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 PDF 파일에 씁니다.

**추가 참조**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 암호화된 PDF 문서 잠금 해제 {#unlocking-encrypted-pdf-documents}

다른 AEM Forms 작업을 수행하려면 먼저 암호로 암호화되거나 인증서로 암호화된 PDF 문서의 잠금을 해제해야 합니다. 암호화된 PDF 문서에 대해 작업을 수행하려고 하면 예외가 발생합니다. 암호화된 PDF 문서의 잠금을 해제하면 해당 문서에 대해 하나 이상의 작업을 수행할 수 있습니다. 이러한 작업은 Acrobat Reader DC 확장 서비스와 같은 다른 서비스에 속할 수 있습니다.

>[!NOTE]
>
>암호화 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary_of_steps-4}

암호화된 PDF 문서의 잠금을 해제하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. 암호화 서비스 클라이언트를 만듭니다.
1. 암호화된 PDF 문서를 가져옵니다.
1. 문서 잠금을 해제합니다.
1. AEM Forms 작업을 수행합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss 애플리케이션 서버에 배포된 경우 필요)
* jbossall-client.jar(AEM Forms이 JBoss 애플리케이션 서버에 배포된 경우 필수)

**암호화 서비스 클라이언트 만들기**

암호화 서비스 작업을 프로그래밍 방식으로 수행하려면 암호화 서비스 클라이언트를 만들어야 합니다. Java 암호화 서비스 API를 사용하는 경우 `EncrytionServiceClient` 개체를 만드십시오. 웹 서비스 암호화 서비스 API를 사용하는 경우 `EncryptionServiceService` 개체를 만드십시오.

**암호화된 PDF 문서 가져오기**

잠금을 해제하려면 암호화된 PDF 문서를 가져옵니다. 암호화되지 않은 PDF 문서의 잠금을 해제하려고 하면 예외가 발생합니다.

**문서 잠금 해제**

암호로 암호화된 PDF 문서의 잠금을 해제하려면 암호화된 PDF 문서와 암호로 암호화된 PDF 문서를 여는 데 사용되는 암호 값이 모두 필요합니다. 이 값은 암호로 PDF 문서를 암호화할 때 지정됩니다. [암호를 사용하여 PDF 문서 암호화](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)를 참조하십시오.

인증서로 암호화된 PDF 문서의 잠금을 해제하려면 암호화된 PDF 문서와 PDF 문서를 암호화하는 데 사용된 개인 키에 해당하는 공개 키의 별칭 값이 모두 필요합니다.

**AEM Forms 작업 수행**

암호화된 PDF 문서의 잠금이 해제된 후에는 해당 문서에 사용 권한을 적용하는 등의 다른 서비스 작업을 수행할 수 있습니다. 이 작업은 Acrobat Reader DC 확장 서비스에 속합니다.

**추가 참조**

[Java API를 사용하여 암호화된 PDF 문서 잠금 해제](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-java-api)

[웹 서비스 API를 사용하여 암호화된 PDF 문서 잠금 해제](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[암호화 서비스 API 빠른 시작](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Java API를 사용하여 암호화된 PDF 문서 잠금 해제 {#unlock-an-encrypted-pdf-document-using-the-java-api}

암호화 API(Java)를 사용하여 암호화된 PDF 문서의 잠금을 해제합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-encryption-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. 암호화 서비스 클라이언트를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하고 `ServiceClientFactory` 개체를 전달하여 `EncryptionServiceClient` 개체를 만듭니다.

1. 암호화된 PDF 문서를 가져옵니다.

   * 생성자를 사용하고 암호화된 PDF 문서의 위치를 지정하는 문자열 값을 전달하여 암호화된 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만듭니다.
   * 생성자를 사용하고 `java.io.FileInputStream` 개체를 전달하여 `com.adobe.idp.Document` 개체를 만듭니다.

1. 문서 잠금을 해제합니다.

   `EncryptionServiceClient` 개체의 `unlockPDFUsingPassword` 또는 `unlockPDFUsingCredential` 메서드를 호출하여 암호화된 PDF 문서의 잠금을 해제합니다.

   암호로 암호화된 PDF 문서의 잠금을 해제하려면 `unlockPDFUsingPassword` 메서드를 호출하고 다음 값을 전달하십시오.

   * 암호로 암호화된 PDF 문서를 포함하는 `com.adobe.idp.Document` 개체입니다.
   * 암호로 암호화된 PDF 문서를 여는 데 사용되는 암호 값을 지정하는 문자열 값입니다. 이 값은 암호로 PDF 문서를 암호화할 때 지정됩니다.

   인증서로 암호화된 PDF 문서의 잠금을 해제하려면 `unlockPDFUsingCredential` 메서드를 호출하고 다음 값을 전달하십시오.

   * 인증서로 암호화된 PDF 문서를 포함하는 `com.adobe.idp.Document` 개체입니다.
   * PDF 문서를 암호화하는 데 사용되는 개인 키에 해당하는 공개 키의 별칭 이름을 지정하는 문자열 값입니다.

   `unlockPDFUsingPassword` 및 `unlockPDFUsingCredential` 메서드는 모두 작업을 수행하기 위해 다른 AEM Forms Java 메서드에 전달하는 `com.adobe.idp.Document` 개체를 반환합니다.

1. AEM Forms 작업을 수행합니다.

   비즈니스 요구 사항을 충족하기 위해 잠금 해제된 PDF 문서에서 AEM Forms 작업을 수행합니다. 예를 들어 잠금 해제된 PDF 문서에 사용 권한을 적용한다고 가정할 경우 `unlockPDFUsingPassword` 또는 `unlockPDFUsingCredential` 메서드에서 반환된 `com.adobe.idp.Document` 개체를 `ReaderExtensionsServiceClient` 개체의 `applyUsageRights` 메서드에 전달합니다.

**추가 참조**

[단계 요약](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[빠른 시작(SOAP 모드): Java API를 사용하여 암호화된 PDF 문서 잠금 해제](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api)(SOAP 모드)

[PDF 문서에 사용 권한 적용](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 암호화된 PDF 문서 잠금 해제 {#unlock-an-encrypted-pdf-document-using-the-web-service-api}

암호화 API(웹 서비스)를 사용하여 암호화된 PDF 문서의 잠금을 해제합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. WSDL 정의 `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`을(를) 사용하는지 확인하십시오.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꾸십시오.

1. 암호화 서비스 클라이언트를 만듭니다.

   * 기본 생성자를 사용하여 `EncryptionServiceClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `EncryptionServiceClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/EncryptionService?WSDL`). `lc_version` 특성은 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * `EncryptionServiceClient.Endpoint.Binding` 필드의 값을 가져와 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`(으)로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * `EncryptionServiceClient.ClientCredentials.UserName.UserName` 필드에 AEM Forms 사용자 이름을 지정하십시오.
      * 필드 `EncryptionServiceClient.ClientCredentials.UserName.Password`에 해당 암호 값을 지정하십시오.
      * 상수 값 `HttpClientCredentialType.Basic`을(를) 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.
      * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을(를) 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. 암호화된 PDF 문서를 가져옵니다.

   * 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다.
   * 해당 생성자를 호출하고 암호화된 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * 바이트 배열의 내용을 `BLOB` 개체의 `MTOM` 데이터 멤버에 할당하여 `BLOB` 개체를 채웁니다.

1. 문서 잠금을 해제합니다.

   `EncryptionServiceClient` 개체의 `unlockPDFUsingPassword` 또는 `unlockPDFUsingCredential` 메서드를 호출하여 암호화된 PDF 문서의 잠금을 해제합니다.

   암호로 암호화된 PDF 문서의 잠금을 해제하려면 `unlockPDFUsingPassword` 메서드를 호출하고 다음 값을 전달하십시오.

   * 암호로 암호화된 PDF 문서를 포함하는 `BLOB` 개체입니다.
   * 암호로 암호화된 PDF 문서를 여는 데 사용되는 암호 값을 지정하는 문자열 값입니다. 이 값은 암호로 PDF 문서를 암호화할 때 지정됩니다.

   인증서로 암호화된 PDF 문서의 잠금을 해제하려면 `unlockPDFUsingCredential` 메서드를 호출하고 다음 값을 전달하십시오.

   * 인증서로 암호화된 PDF 문서를 포함하는 `BLOB` 개체입니다.
   * PDf 문서를 암호화하는 데 사용되는 개인 키에 해당하는 공개 키의 별칭 이름을 지정하는 문자열 값입니다.

   `unlockPDFUsingPassword` 및 `unlockPDFUsingCredential` 메서드는 모두 작업을 수행하기 위해 다른 AEM Forms 메서드에 전달하는 `com.adobe.idp.Document` 개체를 반환합니다.

1. AEM Forms 작업을 수행합니다.

   비즈니스 요구 사항을 충족하기 위해 잠금 해제된 PDF 문서에서 AEM Forms 작업을 수행합니다. 예를 들어 잠금 해제된 PDF 문서에 사용 권한을 적용한다고 가정할 경우 `unlockPDFUsingPassword` 또는 `unlockPDFUsingCredential` 메서드에서 반환된 `BLOB` 개체를 `ReaderExtensionsServiceClient` 개체의 `applyUsageRights` 메서드에 전달합니다.

**추가 참조**

[단계 요약](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 암호화 유형 확인 {#determining-encryption-type}

Java 암호화 서비스 API 또는 웹 서비스 암호화 서비스 API를 사용하여 PDF 문서를 보호하는 암호화 유형을 프로그래밍 방식으로 결정할 수 있습니다. 경우에 따라 PDF 문서의 암호화 여부 및 암호화 유형을 동적으로 결정해야 합니다. 예를 들어 PDF 문서가 암호 기반 암호화로 보호되는지 또는 Rights Management 정책으로 보호되는지 여부를 확인할 수 있습니다.

PDF 문서는 다음 암호화 유형에 의해 보호될 수 있습니다.

* 암호 기반 암호화
* 인증서 기반 암호화
* Rights Management 서비스에서 만든 정책
* 다른 유형의 암호화

>[!NOTE]
>
>암호화 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary_of_steps-5}

PDF 문서를 보호하는 암호화 유형을 확인하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. 암호화 서비스 클라이언트를 만듭니다.
1. 암호화된 PDF 문서를 가져옵니다.
1. 암호화 유형을 확인합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss 애플리케이션 서버에 배포된 경우 필요)
* jbossall-client.jar(AEM Forms이 JBoss 애플리케이션 서버에 배포된 경우 필수)

**서비스 클라이언트 만들기**

암호화 서비스 작업을 프로그래밍 방식으로 수행하려면 암호화 서비스 클라이언트를 만들어야 합니다. Java 암호화 서비스 API를 사용하는 경우 `EncrytionServiceClient` 개체를 만드십시오. 웹 서비스 암호화 서비스 API를 사용하는 경우 `EncryptionServiceService` 개체를 만드십시오.

**암호화된 PDF 문서 가져오기**

PDF 문서를 가져와 보호하는 암호화 유형을 확인합니다.

**암호화 유형 확인**

PDF 문서를 보호하는 암호화 유형을 결정할 수 있습니다. PDF 문서가 보호되지 않으면 암호화 서비스는 PDF 문서가 보호되지 않았음을 알려 줍니다.

**추가 참조**

[Java API를 사용하여 암호화 유형 확인](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-java-api)

[웹 서비스 API를 사용하여 암호화 유형 확인](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[암호화 서비스 API 빠른 시작](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[정책으로 문서 보호](/help/forms/developing/protecting-documents-policies.md#protecting-documents-with-policies)

### Java API를 사용하여 암호화 유형 확인 {#determine-the-encryption-type-using-the-java-api}

암호화 API(Java)를 사용하여 PDF 문서를 보호하는 암호화 유형을 결정합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-encryption-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. 서비스 클라이언트를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하고 `ServiceClientFactory` 개체를 전달하여 `EncryptionServiceClient` 개체를 만듭니다.

1. 암호화된 PDF 문서를 가져옵니다.

   * 생성자를 사용하고 PDF 문서의 위치를 지정하는 문자열 값을 전달하여 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만듭니다.
   * 생성자를 사용하고 `java.io.FileInputStream` 개체를 전달하여 `com.adobe.idp.Document` 개체를 만듭니다.

1. 암호화 유형을 확인합니다.

   * `EncryptionServiceClient` 개체의 `getPDFEncryption` 메서드를 호출하고 PDF 문서가 포함된 `com.adobe.idp.Document` 개체를 전달하여 암호화 유형을 결정하십시오. 이 메서드는 `EncryptionTypeResult` 개체를 반환합니다.
   * `EncryptionTypeResult` 개체의 `getEncryptionType` 메서드를 호출합니다. 이 메서드는 암호화 형식을 지정하는 `EncryptionType` 열거형 값을 반환합니다. 예를 들어 PDF 문서가 암호 기반 암호화로 보호되어 있으면 이 메서드는 `EncryptionType.PASSWORD`을(를) 반환합니다.

**추가 참조**

[단계 요약](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[빠른 시작(SOAP 모드): Java API를 사용하여 암호화 유형 확인](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-determining-encryption-type-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 암호화 유형 확인 {#determine-the-encryption-type-using-the-web-service-api}

암호화 API(웹 서비스)를 사용하여 PDF 문서를 보호하는 암호화 유형을 결정합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. WSDL 정의 `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`을(를) 사용하는지 확인하십시오.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꾸십시오.

1. 서비스 클라이언트를 만듭니다.

   * 기본 생성자를 사용하여 `EncryptionServiceClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `EncryptionServiceClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/EncryptionService?WSDL`). `lc_version` 특성은 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * `EncryptionServiceClient.Endpoint.Binding` 필드의 값을 가져와 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`(으)로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * `EncryptionServiceClient.ClientCredentials.UserName.UserName` 필드에 AEM Forms 사용자 이름을 지정하십시오.
      * 필드 `EncryptionServiceClient.ClientCredentials.UserName.Password`에 해당 암호 값을 지정하십시오.
      * 상수 값 `HttpClientCredentialType.Basic`을(를) 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.
      * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을(를) 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. 암호화된 PDF 문서를 가져옵니다.

   * 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다.
   * 해당 생성자를 호출하고 암호화된 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * 바이트 배열의 내용을 `BLOB` 개체의 `MTOM` 데이터 멤버에 할당하여 `BLOB` 개체를 채웁니다.

1. 암호화 유형을 확인합니다.

   * `EncryptionServiceClient` 개체의 `getPDFEncryption` 메서드를 호출하고 PDF 문서가 포함된 `BLOB` 개체를 전달하십시오. 이 메서드는 `EncryptionTypeResult` 개체를 반환합니다.
   * `EncryptionTypeResult` 개체의 `encryptionType` 데이터 메서드의 값을 가져옵니다. 예를 들어 PDF 문서가 암호 기반 암호화로 보호되어 있으면 이 데이터 멤버의 값은 `EncryptionType.PASSWORD`입니다.

**추가 참조**

[단계 요약](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
