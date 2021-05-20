---
title: 사용 권한 할당
seo-title: 사용 권한 할당
description: Acrobat Reader DC 확장 Java Client API 및 Web Service API를 사용하여 PDF 문서에서 사용 권한을 적용하고 제거합니다.
seo-description: Acrobat Reader DC 확장 Java Client API 및 Web Service API를 사용하여 PDF 문서에서 사용 권한을 적용하고 제거합니다.
uuid: 8c2020df-ea3c-49fa-916f-38a458f40d2b
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9e8db506-9ace-4e1f-8a7b-c4e9b15dde7e
role: Developer
exl-id: 6af148eb-427a-4b54-9c5f-8750736882d8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3951'
ht-degree: 0%

---

# 사용 권한 할당 {#assigning-usage-rights}

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms용입니다.**

## Acrobat Reader DC 확장 서비스 {#about-the-acrobat-reader-dc-extensions-service} 정보

Acrobat Reader DC 확장 서비스를 통해 조직은 Adobe Reader의 기능을 확장하여 대화형 PDF 문서를 쉽게 공유할 수 있습니다. Acrobat Reader DC 확장 서비스는 PDF 1.7까지 포함된 모든 PDF 문서를 완벽하게 지원합니다. Adobe Reader 7.0 이상에서 작동합니다. 이 서비스는 PDF 문서에 사용 권한을 추가하여 Adobe Reader을 사용하여 PDF 문서를 열 때 일반적으로 사용할 수 없는 기능을 활성화합니다. 타사 사용자는 권한이 활성화된 문서에서 작업할 추가 소프트웨어 또는 플러그인이 필요하지 않습니다.

Acrobat Reader DC 확장 서비스를 사용하여 다음 작업을 수행할 수 있습니다.

* PDF 문서에 사용 권한을 적용합니다. 자세한 내용은 [PDF 문서에 사용 권한 적용](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)을 참조하십시오.
* PDF 문서에서 사용 권한을 제거합니다. 자세한 내용은 [PDF 문서에서 사용 권한 제거](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)를 참조하십시오.
* 자격 증명 세부 정보를 검색합니다. 자세한 내용은 [자격 증명 정보 검색](assigning-usage-rights.md#retrieving-credential-information)을 참조하십시오.

>[!NOTE]
>
>Acrobat Reader DC 확장 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

## PDF 문서에 사용 권한 적용 {#applying-usage-rights-to-pdf-documents}

Acrobat Reader DC 확장 Java Client API 및 웹 서비스를 사용하여 PDF 문서에 사용 권한을 적용할 수 있습니다. 사용 권한은 Acrobat에서 기본적으로 사용할 수 있지만, 양식에 주석을 추가하거나, 양식 필드를 작성하고, 양식을 저장하는 기능과 같이 Adobe Reader에서는 사용할 수 없는 기능과 관련이 있습니다. 사용 권한이 적용된 PDF 문서를 권한 사용 문서라고 합니다. Adobe Reader에서 권한 사용 문서를 여는 사용자는 해당 특정 문서에 대해 사용 가능한 작업을 수행할 수 있습니다.

>[!NOTE]
>
>Java API의 일부인 `applyUsageRights` 메서드를 사용하여 PDF 문서에 사용 권한을 적용할 때 `ReaderExtensionsOptionSpec` 개체의 `isModeFinal` 매개 변수를 `false`로 설정할 수 있습니다. 따라서 양식 처리 카운터가 업데이트되지 않고 성능이 향상됩니다. 처리된 양식 카운터를 업데이트할 필요가 없는 경우에는 `isModeFinal` 매개 변수를 `false`(으)로 설정하는 것이 좋습니다.

>[!NOTE]
>
>Acrobat Reader DC 확장 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary-of-steps}

사용 권한을 PDF 문서에 적용하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. Acrobat Reader DC 확장 클라이언트 개체를 만듭니다.
1. PDF 문서를 검색합니다.
1. 적용할 사용 권한을 지정합니다.
1. PDF 문서에 사용 권한을 적용합니다.
1. 권한이 활성화된 PDF 문서를 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Acrobat Reader DC 확장 클라이언트 개체 만들기**

Acrobat Reader DC 확장 프로그램 서비스 작업을 프로그래밍 방식으로 수행하려면 Acrobat Reader DC 확장 서비스 클라이언트 개체를 만들어야 합니다. Acrobat Reader DC 확장 Java API를 사용하는 경우 `ReaderExtensionsServiceClient` 개체를 만듭니다. Acrobat Reader DC 확장 웹 서비스 API를 사용하는 경우 `ReaderExtensionsServiceService` 개체를 만듭니다.

**PDF 문서 검색**

사용 권한을 적용하려면 PDF 문서를 검색해야 합니다. 권한 사용 PDF 문서에는 사용 권한 사전이 포함되어 있습니다. Adobe Reader에서 이러한 사전이 포함된 문서를 열면 해당 문서의 사전에서 지정한 사용 권한만 활성화됩니다. 문서에 사용 권한 사전이 없으면 Acrobat Reader DC 확장 서비스에서 사용 권한 사전이 만들어집니다. 이미 사전이 포함되어 있는 경우 Acrobat Reader DC 확장 서비스는 사용자가 지정하는 사전으로 기존 사용 권한을 덮어씁니다. 사전은 사용 권한을 지정합니다. 사용자가 Adobe Reader에서 문서를 열면 사전에서 지정한 사용 권한만 허용됩니다.

**적용할 사용 권한 지정**

설정할 수 있는 사용 권한은 Adobe Systems Incorporated에서 구매하는 자격 증명에 의해 결정됩니다. 자격 증명은 일반적으로 대화형 양식과 관련된 사용 권한 그룹과 같은 관련 사용 권한 그룹을 설정할 수 있는 권한을 제공합니다. 각 자격 증명은 특정 수의 권한이 활성화된 PDF 문서를 만들 수 있는 권한을 제공합니다. 평가 자격 증명은 무제한 초안 문서를 만들 수 있는 권한을 제공합니다.

>[!NOTE]
>
>자격 증명에서 허용되지 않는 사용 권한을 할당하려고 하면 예외가 발생합니다.

**PDF 문서에 사용 권한 적용**

사용 권한을 PDF 문서에 적용하려면 사용 권한을 적용하는 데 사용하는 자격 증명의 별칭을 참조합니다(자격 증명은 AEM Forms 설치 중에 설치됨). 또한 사용 권한이 적용되는 PDF 문서를 지정해야 합니다. 자격 증명 구성에 대한 자세한 내용은 애플리케이션 서버에 대한 설치 및 배포 안내서를 참조하십시오.

**권한이 활성화된 PDF 문서를 저장합니다**

Acrobat Reader DC 확장 서비스가 PDF 문서에 사용 권한을 적용하면 권한이 활성화된 PDF 문서를 PDF 파일로 저장할 수 있습니다.

**참고 항목**

[Java API를 사용하여 사용 권한 적용](assigning-usage-rights.md#apply-usage-rights-using-the-java-api)

[웹 서비스 API를 사용하여 사용 권한 적용](assigning-usage-rights.md#apply-usage-rights-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC 확장 서비스 API 빠른 시작](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Java API {#apply-usage-rights-using-the-java-api}를 사용하여 사용 권한 적용

Acrobat Reader DC 확장 API(Java)를 사용하여 PDF 문서에 사용 권한을 적용합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-reader-extensions-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. Acrobat Reader DC 확장 클라이언트 개체를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 `ReaderExtensionsServiceClient` 개체를 만들고 `ServiceClientFactory` 개체를 전달합니다.

1. PDF 문서를 검색합니다.

   * 해당 생성자를 사용하여 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만들고 PDF 문서의 위치를 지정하는 문자열 값을 전달합니다.
   * 생성자를 사용하여 `com.adobe.idp.Document` 개체를 만들고 `java.io.FileInputStream` 개체를 전달합니다.

1. 적용할 사용 권한을 지정합니다.

   * 해당 생성자를 사용하여 사용 권한을 나타내는 `UsageRights` 개체를 만듭니다.
   * 적용할 각 사용 권한에 대해 `UsageRights` 개체에 속한 해당 메서드를 호출합니다. 예를 들어 `enableFormFillIn` 사용 권한을 추가하려면 `UsageRights` 개체의 `enableFormFillIn` 메서드를 호출하고 `true`를 전달합니다. (적용할 각 사용 권한에 대해 이 단계를 반복합니다.)

1. PDF 문서에 사용 권한을 적용합니다.

   * 생성자를 사용하여 `ReaderExtensionsOptionSpec` 개체를 만듭니다. 이 개체에는 Acrobat Reader DC 확장 서비스에 필요한 런타임 옵션이 포함되어 있습니다. 이 생성자를 호출할 때는 다음 값을 지정해야 합니다.

      * 문서에 적용할 사용 권한이 포함된 `UsageRights` 개체입니다.
      * Adobe Reader 7.x에서 권한이 활성화된 PDF 문서를 열 때 사용자에게 표시되는 메시지를 지정하는 문자열 값입니다.이 메시지는 Adobe Reader 8.0에 표시되지 않습니다.
   * `ReaderExtensionsServiceClient` 개체의 `applyUsageRights` 메서드를 호출하고 다음 값을 전달하여 PDF 문서에 사용 권한을 적용합니다.

      * 사용 권한이 적용되는 PDF 문서가 포함된 `com.adobe.idp.Document` 개체입니다.
      * 사용 권한을 적용할 수 있는 자격 증명의 별칭을 지정하는 문자열 값입니다.
      * 해당 암호 값을 지정하는 문자열 값입니다. 현재 이 매개 변수는 무시됩니다. `null`을 전달할 수 있습니다.)
   * 런타임 옵션이 포함된 `ReaderExtensionsOptionSpec` 개체입니다.

   `applyUsageRights` 메서드는 권한이 활성화된 PDF 문서가 포함된 `com.adobe.idp.Document` 개체를 반환합니다.

1. 권한이 활성화된 PDF 문서를 저장합니다.

   * `java.io.File` 개체를 만들고 파일 확장명이 .pdf인지 확인합니다.
   * `com.adobe.idp.Document` 개체의 `copyToFile` 메서드를 호출하여 `com.adobe.idp.Document` 개체의 내용을 파일에 복사합니다. `applyUsageRights` 메서드에서 반환된 `com.adobe.idp.Document` 개체를 사용해야 합니다.

**참고 항목**

[PDF 문서에 사용 권한 적용](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[빠른 시작(SOAP 모드):Java API를 사용하여 사용 권한 적용](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-applying-usage-rights-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API {#apply-usage-rights-using-the-web-service-api}를 사용하여 사용 권한 적용

Acrobat Reader DC 확장 API(웹 서비스)를 사용하여 PDF 문서에 사용 권한을 적용합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다.`http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`

   >[!NOTE]
   >
   >`localhost` 을 AEM Forms을 호스팅하는 서버의 IP 주소로 바꿉니다.

1. Acrobat Reader DC 확장 클라이언트 개체를 만듭니다.

   * 기본 생성자를 사용하여 `ReaderExtensionsServiceClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `ReaderExtensionsServiceClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`). `?blob=mtom` 을 지정했는지 확인합니다.
   * `ReaderExtensionsServiceClient.Endpoint.Binding` 필드의 값을 가져와서 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * AEM Forms 사용자 이름을 `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName` 필드에 지정합니다.
      * 해당 암호 값을 `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password` 필드에 할당합니다.
      * 상수 값 `HttpClientCredentialType.Basic`을 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.
      * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. PDF 문서를 검색합니다.

   * 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 사용 권한이 적용되는 PDF 문서를 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하고 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하여 바이트 배열을 스트림 데이터로 채웁니다. 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * `MTOM` 속성을 바이트 배열의 콘텐츠로 할당하여 `BLOB` 개체를 채웁니다.

1. 적용할 사용 권한을 지정합니다.

   * 해당 생성자를 사용하여 사용 권한을 나타내는 `UsageRights` 개체를 만듭니다.
   * 적용할 각 사용 권한에 대해 `true` 값을 `UsageRights` 객체에 속하는 해당 데이터 멤버에 할당합니다. 예를 들어 `enableFormFillIn` 사용 권한을 추가하려면 `true` 개체의 `enableFormFillIn` 데이터 멤버에 `UsageRights`을 할당합니다. (적용할 각 사용 권한에 대해 이 단계를 반복합니다.)

1. PDF 문서에 사용 권한을 적용합니다.

   * 생성자를 사용하여 `ReaderExtensionsOptionSpec` 개체를 만듭니다. 이 개체에는 Acrobat Reader DC 확장 서비스에 필요한 런타임 옵션이 포함되어 있습니다.
   * `UsageRights` 개체를 `ReaderExtensionsOptionSpec` 개체의 `usageRights` 데이터 멤버에 할당합니다.
   * Adobe Reader에서 권한 사용 PDF 문서를 `ReaderExtensionsOptionSpec` 개체의 `message` 데이터 멤버에 열 때 사용자에게 표시되는 메시지를 지정하는 문자열 값을 지정합니다.
   * `ReaderExtensionsServiceClient` 개체의 `applyUsageRights` 메서드를 호출하고 다음 값을 전달하여 PDF 문서에 사용 권한을 적용합니다.

      * 사용 권한이 적용되는 PDF 문서가 포함된 `BLOB` 개체입니다.
      * 사용 권한을 적용할 수 있는 자격 증명의 별칭을 지정하는 문자열 값입니다.
      * 해당 암호 값을 지정하는 문자열 값입니다. 현재 이 매개 변수는 무시됩니다. `null`을 전달할 수 있습니다.)
   * 런타임 옵션이 포함된 `ReaderExtensionsOptionSpec` 개체입니다.

   `applyUsageRights` 메서드는 권한이 활성화된 PDF 문서가 포함된 `BLOB` 개체를 반환합니다.

1. 권한이 활성화된 PDF 문서를 저장합니다.

   * 해당 생성자를 호출하여 `System.IO.FileStream` 개체를 만듭니다. 권한이 활성화된 PDF 문서의 파일 위치를 나타내는 문자열 값을 전달합니다.
   * `applyUsageRights` 메서드에서 반환된 `BLOB` 개체의 데이터 콘텐츠를 저장하는 바이트 배열을 만듭니다. `BLOB` 개체의 `MTOM` 데이터 멤버의 값을 가져와서 바이트 배열을 채웁니다.
   * 해당 생성자를 호출하고 `System.IO.FileStream` 개체를 전달하여 `System.IO.BinaryWriter` 개체를 만듭니다.
   * `System.IO.BinaryWriter` 개체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열 내용을 PDF 파일에 씁니다.

**참고 항목**

[PDF 문서에 사용 권한 적용](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## PDF 문서에서 사용 권한 제거 {#removing-usage-rights-from-pdf-documents}

권한 사용 문서에서 사용 권한을 제거할 수 있습니다. 권한이 활성화된 PDF 문서에서 사용 권한을 제거해야 해당 문서에 대한 다른 AEM Forms 작업을 수행할 수도 있습니다. 예를 들어 사용 권한을 설정하기 전에 PDF 문서에 디지털 서명(또는 인증)해야 합니다. 따라서 권한이 활성화된 문서에서 작업을 수행하려면 PDF 문서에서 사용 권한을 제거하고 문서에 디지털 서명을 하는 등의 기타 작업을 수행한 다음 문서에 사용 권한을 다시 적용해야 합니다.

>[!NOTE]
>
>Acrobat Reader DC 확장 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary_of_steps-1}

권한이 활성화된 PDF 문서에서 사용 권한을 제거하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. Acrobat Reader DC 확장 클라이언트 개체를 만듭니다.
1. 권한이 활성화된 PDF 문서를 검색합니다.
1. PDF 문서에서 사용 권한을 제거합니다.
1. PDF 문서를 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Acrobat Reader DC 확장 클라이언트 개체 만들기**

Acrobat Reader DC 확장 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 Acrobat Reader DC 확장 서비스 클라이언트 개체를 만들어야 합니다. Java API를 사용하는 경우 `ReaderExtensionsServiceClient` 개체를 만듭니다. Acrobat Reader DC 확장 웹 서비스 API를 사용하는 경우 `ReaderExtensionsServiceService` 개체를 만듭니다.

**권한이 활성화된 PDF 문서 검색**

사용 권한을 제거하려면 권한이 활성화된 PDF 문서를 검색합니다.

**PDF 문서에서 사용 권한 제거**

권한이 활성화된 PDF 문서를 검색한 후 사용 권한을 제거할 수 있습니다. 사용 권한을 제거하면 Adobe Reader 내에서 보는 동안 PDF 문서에 추가 기능이 없습니다.

**PDF 문서를 저장합니다**

사용 권한이 더 이상 포함되지 않은 PDF 문서를 PDF 파일로 저장할 수 있습니다. PDF 파일로 저장되면 PDF 문서를 Adobe Reader 또는 Acrobat에서 볼 수 있습니다.

**참고 항목**

[Java API를 사용하여 사용 권한 제거](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[웹 서비스 API를 사용하여 사용 권한 제거](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC 확장 서비스 API 빠른 시작](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

[PDF 문서에 사용 권한 적용](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

### Java API {#remove-usage-rights-using-the-java-api}를 사용하여 사용 권한 제거

Acrobat Reader DC 확장 API(Java)를 사용하여 권한이 활성화된 PDF 문서에서 사용 권한을 제거합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-reader-extensions-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. Acrobat Reader DC 확장 클라이언트 개체를 만듭니다.

   해당 생성자를 사용하여 `ReaderExtensionsServiceClient` 개체를 만들고 연결 속성이 포함된 `ServiceClientFactory` 개체를 전달합니다.

1. PDF 문서를 검색합니다.

   * 해당 생성자를 사용하여 권한 사용 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만들고 PDF 문서의 위치를 지정하는 문자열 값을 전달합니다.
   * 생성자를 사용하여 `com.adobe.idp.Document` 개체를 만들고 `java.io.FileInputStream` 개체를 전달합니다.

1. PDF 문서에서 사용 권한을 제거합니다.

   `ReaderExtensionsServiceClient` 개체의 `removeUsageRights` 메서드를 호출하고 권한이 활성화된 PDF 문서가 포함된 `com.adobe.idp.Document` 개체를 전달하여 PDF 문서에서 사용 권한을 제거합니다. 이 메서드는 사용 권한이 없는 PDF 문서를 포함하는 `com.adobe.idp.Document` 개체를 반환합니다.

1. PDF 문서에 사용 권한을 적용합니다.

   * `java.io.File` 개체를 만들고 파일 확장명이 .PDF인지 확인합니다.
   * `Document` 개체의 `copyToFile` 메서드를 호출하여 `Document` 개체의 내용을 파일에 복사합니다. `removeUsageRights` 메서드에서 반환된 `Document` 개체를 사용해야 합니다.

**참고 항목**

[PDF 문서에서 사용 권한 제거](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[빠른 시작(SOAP 모드):Java API를 사용하여 PDF 문서에서 사용 권한 제거](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API {#remove-usage-rights-using-the-web-service-api}를 사용하여 사용 권한 제거

Acrobat Reader DC 확장 API(웹 서비스)를 사용하여 권한이 활성화된 PDF 문서에서 사용 권한을 제거합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다.`http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`

   >[!NOTE]
   >
   >`localhost` 을 AEM Forms을 호스팅하는 서버의 IP 주소로 바꿉니다.

1. Acrobat Reader DC 확장 클라이언트 개체를 만듭니다.

   * 기본 생성자를 사용하여 `ReaderExtensionsServiceClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `ReaderExtensionsServiceClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`). `?blob=mtom` 을 지정했는지 확인합니다.
   * `ReaderExtensionsServiceClient.Endpoint.Binding` 필드의 값을 가져와서 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * AEM Forms 사용자 이름을 `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName` 필드에 지정합니다.
      * 해당 암호 값을 `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password` 필드에 할당합니다.
      * 상수 값 `HttpClientCredentialType.Basic`을 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.
      * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. PDF 문서를 검색합니다.

   * 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 사용 권한이 제거된 권한 사용 PDF 문서를 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하고 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하고 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * `MTOM` 속성을 바이트 배열의 콘텐츠로 할당하여 `BLOB` 개체를 채웁니다.

1. PDF 문서에서 사용 권한을 제거합니다.

   `ReaderExtensionsServiceClient` 개체의 `removeUsageRights` 메서드를 호출하고 권한이 활성화된 PDF 문서가 포함된 `BLOB` 개체를 전달하여 PDF 문서에서 사용 권한을 제거합니다. 이 메서드는 사용 권한이 없는 PDF 문서를 포함하는 `BLOB` 개체를 반환합니다.

1. PDF 문서에 사용 권한을 적용합니다.

   * 해당 생성자를 호출하고 PDF 파일 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `removeUsageRights` 메서드에서 반환된 `BLOB` 개체의 데이터 콘텐츠를 저장하는 바이트 배열을 만듭니다. `BLOB` 개체의 `MTOM` 데이터 멤버의 값을 가져와서 바이트 배열을 채웁니다.
   * 해당 생성자를 호출하고 `System.IO.FileStream` 개체를 전달하여 `System.IO.BinaryWriter` 개체를 만듭니다.

**참고 항목**

[PDF 문서에서 사용 권한 제거](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 자격 증명 정보 검색 중 {#retrieving-credential-information}

사용 권한을 사용 가능한 PDF 문서에 적용하는 데 사용된 자격 증명에 대한 정보를 검색할 수 있습니다. 자격 증명에 대한 정보를 검색하면 인증서가 더 이상 유효하지 않은 날짜와 같은 정보를 얻을 수 있습니다.

>[!NOTE]
>
>Acrobat Reader DC 확장 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary_of_steps-2}

사용 권한을 PDF 문서에 적용하는 데 사용된 자격 증명에 대한 정보를 검색하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. Acrobat Reader DC 확장 클라이언트 개체를 만듭니다.
1. 권한이 활성화된 PDF 문서를 검색합니다.
1. 자격 증명에 대한 정보를 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Acrobat Reader DC 확장 클라이언트 개체 만들기**

Acrobat Reader DC 확장 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 Acrobat Reader DC 확장 서비스 클라이언트 개체를 만들어야 합니다. Java API를 사용하는 경우 `ReaderExtensionsServiceClient` 개체를 만듭니다. Acrobat Reader DC 확장 웹 서비스 API를 사용하는 경우 `ReaderExtensionsServiceService` 개체를 만듭니다.

**권한이 활성화된 PDF 문서 검색**

자격 증명에 대한 정보를 검색하려면 권한이 활성화된 PDF 문서를 검색해야 합니다. 별칭을 지정하여 자격 증명에 대한 정보를 검색할 수도 있습니다.그러나 사용 권한을 특정 권한 사용 PDF 문서에 적용하는 데 사용된 자격 증명에 대한 정보를 검색하려면 문서를 검색해야 합니다.

**자격 증명에 대한 정보 검색**

권한 사용 PDF 문서를 검색한 후 사용 권한을 적용하는 데 사용된 자격 증명에 대한 정보를 얻을 수 있습니다. 자격 증명에 대한 다음 정보를 얻을 수 있습니다.

* 권한이 활성화된 PDF 문서를 열 때 Adobe Reader 내에 표시되는 메시지입니다.
* 자격 증명이 더 이상 유효하지 않은 이후의 날짜입니다.
* 자격 증명이 유효하지 않은 이전 날짜입니다.
* 이 권한이 활성화된 PDF 문서에 설정된 사용 권한.
* 자격 증명을 사용한 횟수입니다.

**참고 항목**

[Java API를 사용하여 사용 권한 제거](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[웹 서비스 API를 사용하여 사용 권한 제거](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC 확장 서비스 API 빠른 시작](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Java API {#retrieve-credential-information-using-the-java-api}를 사용하여 자격 증명 정보 검색

Acrobat Reader DC 확장 API(Java)를 사용하여 자격 증명 정보를 검색합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-reader-extensions-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. Acrobat Reader DC 확장 클라이언트 개체를 만듭니다.

   해당 생성자를 사용하여 `ReaderExtensionsServiceClient` 개체를 만들고 연결 속성이 포함된 `ServiceClientFactory` 개체를 전달합니다.

1. PDF 문서를 검색합니다.

   * 해당 생성자를 사용하여 권한 사용 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만들고 권한 사용 PDF 문서의 위치를 지정하는 문자열 값을 전달합니다.
   * 생성자를 사용하여 `com.adobe.idp.Document` 개체를 만들고 `java.io.FileInputStream` 개체를 전달합니다.

1. PDF 문서에서 사용 권한을 제거합니다.

   * `ReaderExtensionsServiceClient` 개체의 `getDocumentUsageRights` 메서드를 호출하고 권한이 활성화된 PDF 문서가 포함된 `com.adobe.idp.Document` 개체를 전달하여 PDF 문서에 사용 권한을 적용하는 데 사용되는 자격 증명에 대한 정보를 검색합니다. 이 메서드는 자격 증명 정보를 포함하는 `GetUsageRightsResult` 개체를 반환합니다.
   * `GetUsageRightsResult` 개체의 `getNotAfter` 메서드를 호출하여 자격 증명이 더 이상 유효하지 않은 날짜를 검색합니다. 이 메서드는 자격 증명이 더 이상 유효하지 않은 이후의 날짜를 나타내는 `java.util.Date` 개체를 반환합니다.
   * `GetUsageRightsResult` 개체의 `getMessage` 메서드를 호출하여 권한이 활성화된 PDF 문서를 열 때 Adobe Reader에 표시되는 메시지를 검색합니다. 이 메서드는 메시지를 나타내는 문자열 값을 반환합니다.

**참고 항목**

[자격 증명 정보 검색](assigning-usage-rights.md#retrieving-credential-information)

[빠른 시작(SOAP 모드):Java API를 사용하여 자격 증명 정보 검색](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-retrieving-credential-information-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API {#retrieve-credential-information-using-the-web-service-api}를 사용하여 자격 증명 정보 검색

Acrobat Reader DC 확장 API(웹 서비스)를 사용하여 자격 증명 정보를 검색합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다.`http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`

   >[!NOTE]
   >
   >`localhost` 을 AEM Forms을 호스팅하는 서버의 IP 주소로 바꿉니다.

1. Acrobat Reader DC 확장 클라이언트 개체를 만듭니다.

   * 기본 생성자를 사용하여 `ReaderExtensionsServiceClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `ReaderExtensionsServiceClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`). `?blob=mtom` 을 지정했는지 확인합니다.
   * `ReaderExtensionsServiceClient.Endpoint.Binding` 필드의 값을 가져와서 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * AEM Forms 사용자 이름을 `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName` 필드에 지정합니다.
      * 해당 암호 값을 `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password` 필드에 할당합니다.
      * 상수 값 `HttpClientCredentialType.Basic`을 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.
      * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. PDF 문서를 검색합니다.

   * 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 권한이 활성화된 PDF 문서를 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하고 권한 사용 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하고 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * `MTOM` 속성을 바이트 배열의 콘텐츠로 할당하여 `BLOB` 개체를 채웁니다.

1. PDF 문서에서 사용 권한을 제거합니다.

   * `ReaderExtensionsServiceClient` 개체의 `getDocumentUsageRights` 메서드를 호출하고 권한이 활성화된 PDF 문서가 포함된 `com.adobe.idp.Document` 개체를 전달하여 PDF 문서에 사용 권한을 적용하는 데 사용되는 자격 증명에 대한 정보를 검색합니다. 이 메서드는 자격 증명 정보를 포함하는 `GetUsageRightsResult` 개체를 반환합니다.
   * `GetUsageRightsResult` 개체의 `notAfter` 데이터 멤버의 값을 가져와서 자격 증명이 더 이상 유효하지 않은 날짜를 검색합니다. 이 데이터 멤버의 데이터 유형은 `System.DateTime`입니다.
   * 권한 사용 PDF 문서가 Adobe Reader에서 열릴 때 표시되는 메시지를 검색하려면 `GetUsageRightsResult` 개체의 `message` 데이터 구성원의 값을 가져옵니다. 이 데이터 멤버의 데이터 유형은 문자열입니다.
   * `GetUsageRightsResult` 개체의 `useCount` 데이터 멤버의 값을 가져와서 자격 증명이 사용되는 횟수를 검색합니다. 이 데이터 멤버의 데이터 형식은 정수입니다.

**참고 항목**

[자격 증명 정보 검색](assigning-usage-rights.md#retrieving-credential-information)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
