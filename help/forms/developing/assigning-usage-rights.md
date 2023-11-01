---
title: 사용 권한 할당
seo-title: Assigning Usage Rights
description: Acrobat Reader DC 확장 Java 클라이언트 API 및 웹 서비스 API를 사용하여 PDF 문서에 사용 권한을 적용 및 제거합니다.
seo-description: Use the Acrobat Reader DC extensions Java Client API and Web Service API to apply and remove usage rights from PDF documents.
uuid: 8c2020df-ea3c-49fa-916f-38a458f40d2b
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9e8db506-9ace-4e1f-8a7b-c4e9b15dde7e
role: Developer
exl-id: 6af148eb-427a-4b54-9c5f-8750736882d8
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '3918'
ht-degree: 0%

---

# 사용 권한 할당 {#assigning-usage-rights}

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms에 대해서만 적용됩니다.**

## Acrobat Reader DC 확장 서비스 정보 {#about-the-acrobat-reader-dc-extensions-service}

Acrobat Reader DC 확장 서비스를 사용하면 Adobe Reader의 기능을 확장하여 조직에서 대화형 PDF 문서를 쉽게 공유할 수 있습니다. Acrobat Reader DC 확장 서비스는 최대 PDF 1.7을 포함한 모든 PDF 문서를 완벽하게 지원합니다. Adobe Reader 7.0 이상에서 작동합니다. 이 서비스는 PDF 문서에 사용 권한을 추가하여 Adobe Reader을 사용하여 PDF 문서를 열 때 일반적으로 사용할 수 없는 기능을 활성화합니다. 서드파티 사용자는 권한이 활성화된 문서에서 작동하는 데 추가 소프트웨어나 플러그인이 필요하지 않습니다.

Acrobat Reader DC 확장 서비스를 사용하여 다음 작업을 수행할 수 있습니다.

* PDF 문서에 사용 권한을 적용합니다. 자세한 내용은 [PDF 문서에 사용 권한 적용](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).
* PDF 문서에서 사용 권한을 제거합니다. 자세한 내용은 [PDF 문서에서 사용 권한 제거](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents).
* 자격 증명 세부 정보를 검색합니다. 자세한 내용은 [자격 증명 정보 검색](assigning-usage-rights.md#retrieving-credential-information).

>[!NOTE]
>
>Acrobat Reader DC 확장 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

## PDF 문서에 사용 권한 적용 {#applying-usage-rights-to-pdf-documents}

Acrobat Reader DC 확장 Java 클라이언트 API 및 웹 서비스를 사용하여 PDF 문서에 사용 권한을 적용할 수 있습니다. 사용 권한은 양식에 주석을 추가하거나 양식 필드를 채우고 양식을 저장하는 기능과 같이 Acrobat에서 기본적으로 사용할 수 있지만 Adobe Reader에서는 사용할 수 없는 기능과 관련이 있습니다. 사용 권한이 적용된 PDF 문서를 권한 사용 문서라고 합니다. Adobe Reader에서 권한이 활성화된 문서를 여는 사용자는 특정 문서에 대해 활성화된 작업을 수행할 수 있습니다.

>[!NOTE]
>
>를 사용하여 PDF 문서에 사용 권한을 적용할 때 `applyUsageRights` 메서드, Java API의 일부 `isModeFinal` 매개 변수 `ReaderExtensionsOptionSpec` 대상 오브젝트 `false`. 이로 인해 양식 처리 카운터가 업데이트되지 않고 성능이 향상됩니다. Forms 처리된 카운터를 업데이트할 필요가 없다면 를 설정하는 것이 좋습니다. `isModeFinal` 매개 변수 `false`.

>[!NOTE]
>
>Acrobat Reader DC 확장 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary-of-steps}

PDF 문서에 사용 권한을 적용하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. Acrobat Reader DC 확장 클라이언트 개체를 만듭니다.
1. PDF 문서를 검색합니다.
1. 적용할 사용 권한을 지정합니다.
1. PDF 문서에 사용 권한을 적용합니다.
1. 권한이 활성화된 PDF 문서를 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 생성하는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Acrobat Reader DC 확장 클라이언트 개체 만들기**

Acrobat Reader DC 확장 서비스 작업을 프로그래밍 방식으로 수행하려면 Acrobat Reader DC 확장 서비스 클라이언트 개체를 만들어야 합니다. Acrobat Reader DC 확장 Java API를 사용하는 경우 `ReaderExtensionsServiceClient` 개체. Acrobat Reader DC 확장 웹 서비스 API를 사용하는 경우 `ReaderExtensionsServiceService` 개체.

**PDF 문서 검색**

사용 권한을 적용하려면 PDF 문서를 검색해야 합니다. 권한이 활성화된 PDF 문서에는 사용 권한 사전이 포함되어 있습니다. Adobe Reader에서 이러한 사전이 포함된 문서를 열면 해당 문서에 대해서만 사전에 지정된 사용 권한을 활성화합니다. 문서에 사용 권한 사전이 없으면 Acrobat Reader DC 확장 서비스에서 이를 만듭니다. 사전에 이미 포함되어 있는 경우 Acrobat Reader DC 확장 서비스는 사용자가 지정한 사용 권한으로 기존 사용 권한을 덮어씁니다. 사전은 사용할 수 있는 사용 권한을 지정합니다. 사용자가 Adobe Reader에서 문서를 열면 사전에 지정된 사용 권한만 허용됩니다.

**적용할 사용 권한 지정**

설정할 수 있는 사용 권한은 Adobe Systems Incorporated에서 구입한 자격 증명에 의해 결정됩니다. 자격 증명은 일반적으로 대화형 양식과 관련된 사용 권한 등의 관련 사용 권한 그룹을 설정할 수 있는 권한을 제공합니다. 각 자격 증명은 특정 수의 권한이 활성화된 PDF 문서를 만들 수 있는 권한을 제공합니다. 평가 자격 증명은 초안 문서를 무제한으로 만들 수 있는 권한을 부여합니다.

>[!NOTE]
>
>자격 증명에서 허용되지 않는 사용 권한을 할당하려고 하면 예외가 발생합니다.

**PDF 문서에 사용 권한 적용**

PDF 문서에 사용 권한을 적용하려면 사용 권한을 적용하는 데 사용 중인 자격 증명의 별칭을 참조합니다(자격 증명은 일반적으로 AEM Forms 설치 중에 설치됩니다). 또한 사용 권한이 적용되는 PDF 문서를 지정해야 합니다. 자격 증명 구성에 대한 자세한 내용은 애플리케이션 서버용 설치 및 배포 안내서를 참조하십시오.

**권한이 활성화된 PDF 문서 저장**

Acrobat Reader DC 확장 서비스가 사용 권한을 PDF 문서에 적용한 후 권한이 활성화된 PDF 문서를 PDF 파일로 저장할 수 있습니다.

**추가 참조**

[Java API를 사용하여 사용 권한 적용](assigning-usage-rights.md#apply-usage-rights-using-the-java-api)

[웹 서비스 API를 사용하여 사용 권한 적용](assigning-usage-rights.md#apply-usage-rights-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC 확장 서비스 API 빠른 시작](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Java API를 사용하여 사용 권한 적용 {#apply-usage-rights-using-the-java-api}

Acrobat Reader DC 확장 API(Java)를 사용하여 PDF 문서에 사용 권한 적용:

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-reader-extensions-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. Acrobat Reader DC 확장 클라이언트 개체를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.
   * 만들기 `ReaderExtensionsServiceClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체.

1. PDF 문서를 검색합니다.

   * 만들기 `java.io.FileInputStream` PDF 문서의 위치를 지정하는 문자열 값을 전달하고 생성자를 사용하여 PDF 문서를 나타내는 개체입니다.
   * 만들기 `com.adobe.idp.Document` 개체를 생성자를 사용하고 `java.io.FileInputStream` 개체.

1. 적용할 사용 권한을 지정합니다.

   * 만들기 `UsageRights` 생성자를 사용하여 사용 권한을 나타내는 개체입니다.
   * 적용할 각 사용 권한에 대해 `UsageRights` 개체. 예를 들어 `enableFormFillIn` 사용 권한, 호출 `UsageRights` 개체 `enableFormFillIn` 방법 및 통과 `true`. 각 사용 권한에 대해 이 단계를 반복하여 적용합니다.

1. PDF 문서에 사용 권한을 적용합니다.

   * 만들기 `ReaderExtensionsOptionSpec` 개체를 만들 때 사용됩니다. 이 개체에는 Acrobat Reader DC 확장 서비스에 필요한 런타임 옵션이 포함되어 있습니다. 이 생성자를 호출할 때는 다음 값을 지정해야 합니다.

      * 다음 `UsageRights` 문서에 적용할 사용 권한이 포함된 개체입니다.
      * Adobe Reader 7.x에서 권한이 활성화된 PDF 문서를 열 때 사용자에게 표시되는 메시지를 지정하는 문자열 값입니다. 이 메시지는 Adobe Reader 8.0에 표시되지 않습니다.

   * 를 호출하여 PDF 문서에 사용 권한 적용 `ReaderExtensionsServiceClient` 개체 `applyUsageRights` 메서드 및 다음 값 전달:

      * 다음 `com.adobe.idp.Document` 사용 권한이 적용되는 PDF 문서가 포함된 객체입니다.
      * 사용 권한을 적용할 수 있는 자격 증명의 별칭을 지정하는 문자열 값입니다.
      * 해당 암호 값을 지정하는 문자열 값입니다. (현재 이 매개 변수는 무시됩니다. 다음을 전달할 수 있습니다. `null`.)

   * 다음 `ReaderExtensionsOptionSpec` 런타임 옵션이 포함된 객체입니다.

   다음 `applyUsageRights` 메서드가 을 반환합니다. `com.adobe.idp.Document` 권한이 활성화된 PDF 문서가 포함된 객체입니다.

1. 권한이 활성화된 PDF 문서를 저장합니다.

   * 만들기 `java.io.File` 개체로 식별되고 파일 확장명이 .pdf인지 확인합니다.
   * 호출 `com.adobe.idp.Document` 개체 `copyToFile` 콘텐츠 복사 방법 `com.adobe.idp.Document` 파일에 대한 개체(를 사용해야 함) `com.adobe.idp.Document` 에서 반환한 개체 `applyUsageRights` 메서드).

**추가 참조**

[PDF 문서에 사용 권한 적용](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[빠른 시작(SOAP 모드):Java API를 사용하여 사용 권한 적용](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-applying-usage-rights-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 사용 권한 적용 {#apply-usage-rights-using-the-web-service-api}

Acrobat Reader DC 확장 API(웹 서비스)를 사용하여 PDF 문서에 사용 권한을 적용합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용하는지 확인합니다. `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` AEM Forms을 호스팅하는 서버의 IP 주소입니다.

1. Acrobat Reader DC 확장 클라이언트 개체를 만듭니다.

   * 만들기 `ReaderExtensionsServiceClient` 기본 생성자를 사용하여 개체를 작성합니다.
   * 만들기 `ReaderExtensionsServiceClient.Endpoint.Address` 을 사용하여 개체 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. 다음을 지정하십시오. `?blob=mtom`.)
   * 만들기 `System.ServiceModel.BasicHttpBinding` 의 값을 가져와서 개체 `ReaderExtensionsServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스트 `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름 할당 `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * 해당 암호 값을 필드에 할당합니다. `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 지정 `HttpClientCredentialType.Basic` 필드에 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 상수 값 지정 `BasicHttpSecurityMode.TransportCredentialOnly` 필드에 `BasicHttpBindingSecurity.Security.Mode`.

1. PDF 문서를 검색합니다.

   * 만들기 `BLOB` 개체를 만들 때 사용됩니다. 다음 `BLOB` 객체는 사용 권한이 적용되는 PDF 문서를 저장하는 데 사용됩니다.
   * 만들기 `System.IO.FileStream` PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 콘텐츠를 저장하는 바이트 배열 만들기 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채우기 `System.IO.FileStream` 개체 `Read` 메서드를 사용합니다. 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 채우기 `BLOB` 개체 할당 `MTOM` 속성을 바이트 배열의 콘텐츠와 함께 사용합니다.

1. 적용할 사용 권한을 지정합니다.

   * 만들기 `UsageRights` 생성자를 사용하여 사용 권한을 나타내는 개체입니다.
   * 적용할 각 사용 권한에 대해 값을 할당합니다. `true` 에 속한 해당 데이터 멤버에게 `UsageRights` 개체. 예를 들어 `enableFormFillIn` 사용 권한, 할당 `true` (으)로 `UsageRights` 개체 `enableFormFillIn` 데이터 구성원입니다. 각 사용 권한에 대해 이 단계를 반복하여 적용합니다.

1. PDF 문서에 사용 권한을 적용합니다.

   * 만들기 `ReaderExtensionsOptionSpec` 개체를 만들 때 사용됩니다. 이 개체에는 Acrobat Reader DC 확장 서비스에 필요한 런타임 옵션이 포함되어 있습니다.
   * 할당 `UsageRights` 에 대한 오브젝트 `ReaderExtensionsOptionSpec` 개체 `usageRights` 데이터 구성원입니다.
   * Adobe Reader에서 권한이 활성화된 PDF 문서를 열 때 사용자에게 표시되는 메시지를 지정하는 문자열 값을 `ReaderExtensionsOptionSpec` 개체 `message` 데이터 구성원입니다.
   * 를 호출하여 PDF 문서에 사용 권한 적용 `ReaderExtensionsServiceClient` 개체 `applyUsageRights` 메서드 및 다음 값 전달:

      * 다음 `BLOB` 사용 권한이 적용되는 PDF 문서가 포함된 객체입니다.
      * 사용 권한을 적용할 수 있는 자격 증명의 별칭을 지정하는 문자열 값입니다.
      * 해당 암호 값을 지정하는 문자열 값입니다. (현재 이 매개 변수는 무시됩니다. 다음을 전달할 수 있습니다. `null`.)

   * 다음 `ReaderExtensionsOptionSpec` 런타임 옵션이 포함된 객체입니다.

   다음 `applyUsageRights` 메서드가 을 반환합니다. `BLOB` 권한이 활성화된 PDF 문서가 포함된 객체입니다.

1. 권한이 활성화된 PDF 문서를 저장합니다.

   * 만들기 `System.IO.FileStream` 해당 생성자를 호출하여 개체를 작성합니다. 권한이 활성화된 PDF 문서의 파일 위치를 나타내는 문자열 값을 전달합니다.
   * 의 데이터 콘텐츠를 저장하는 바이트 배열 만들기 `BLOB` 에서 반환한 개체 `applyUsageRights` 메서드를 사용합니다. 의 값을 가져와서 바이트 배열 채우기 `BLOB` 개체 `MTOM` 데이터 구성원입니다.
   * 만들기 `System.IO.BinaryWriter` 개체를 호출하고 `System.IO.FileStream` 개체.
   * 를 호출하여 바이트 배열의 내용을 PDF 파일에 씁니다 `System.IO.BinaryWriter` 개체 `Write` 메서드 및 바이트 배열 전달.

**추가 참조**

[PDF 문서에 사용 권한 적용](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## PDF 문서에서 사용 권한 제거 {#removing-usage-rights-from-pdf-documents}

권한이 활성화된 문서에서 사용 권한을 제거할 수 있습니다. 권한이 활성화된 PDF 문서에서 사용 권한을 제거하면 해당 문서에 대한 다른 AEM Forms 작업을 수행할 수도 있습니다. 예를 들어 사용 권한을 설정하기 전에 PDF 문서에 디지털 서명(또는 인증)을 해야 합니다. 따라서 권한이 활성화된 문서에 대해 작업을 수행하려면 PDF 문서에서 사용 권한을 제거하고 문서에 디지털 서명하는 등의 다른 작업을 수행한 다음 문서에 사용 권한을 다시 적용해야 합니다.

>[!NOTE]
>
>Acrobat Reader DC 확장 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-1}

권한이 활성화된 PDF 문서에서 사용 권한을 제거하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. Acrobat Reader DC 확장 클라이언트 개체를 만듭니다.
1. 권한이 활성화된 PDF 문서를 검색합니다.
1. PDF 문서에서 사용 권한을 제거합니다.
1. PDF 문서를 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 생성하는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Acrobat Reader DC 확장 클라이언트 개체 만들기**

Acrobat Reader DC 확장 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 Acrobat Reader DC 확장 서비스 클라이언트 개체를 만들어야 합니다. Java API를 사용하는 경우 `ReaderExtensionsServiceClient` 개체. Acrobat Reader DC 확장 웹 서비스 API를 사용하는 경우 `ReaderExtensionsServiceService` 개체.

**권한이 활성화된 PDF 문서 검색**

사용 권한을 제거하기 위해 권한이 활성화된 PDF 문서를 검색합니다.

**PDF 문서에서 사용 권한 제거**

권한이 활성화된 PDF 문서를 검색한 후 사용 권한을 제거할 수 있습니다. 사용 권한을 제거하면 Adobe Reader 내에서 볼 때 PDF 문서에 추가 기능이 없습니다.

**PDF 문서 저장**

더 이상 사용 권한이 포함되지 않은 PDF 문서를 PDF 파일로 저장할 수 있습니다. PDF 파일로 저장하면 PDF 문서를 Adobe Reader 또는 Acrobat에서 볼 수 있습니다.

**추가 참조**

[Java API를 사용하여 사용 권한 제거](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[웹 서비스 API를 사용하여 사용 권한 제거](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC 확장 서비스 API 빠른 시작](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

[PDF 문서에 사용 권한 적용](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

### Java API를 사용하여 사용 권한 제거 {#remove-usage-rights-using-the-java-api}

Acrobat Reader DC 확장 API(Java)를 사용하여 권한이 활성화된 PDF 문서에서 사용 권한을 제거합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-reader-extensions-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. Acrobat Reader DC 확장 클라이언트 개체를 만듭니다.

   만들기 `ReaderExtensionsServiceClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.

1. PDF 문서를 검색합니다.

   * 만들기 `java.io.FileInputStream` 해당 생성자를 사용하고 PDF 문서의 위치를 지정하는 문자열 값을 전달하여 권한이 활성화된 PDF 문서를 나타내는 개체입니다.
   * 만들기 `com.adobe.idp.Document` 개체를 생성자를 사용하고 `java.io.FileInputStream` 개체.

1. PDF 문서에서 사용 권한을 제거합니다.

   를 호출하여 PDF 문서에서 사용 권한 제거 `ReaderExtensionsServiceClient` 개체 `removeUsageRights` 메서드 및 전달 `com.adobe.idp.Document` 권한이 활성화된 PDF 문서가 포함된 객체입니다. 이 메서드는 `com.adobe.idp.Document` 사용 권한이 없는 PDF 문서가 포함된 개체입니다.

1. PDF 문서에 사용 권한을 적용합니다.

   * 만들기 `java.io.File` 개체로 변환하고 파일 확장명이 .PDF인지 확인합니다.
   * 호출 `Document` 개체 `copyToFile` 콘텐츠 복사 방법 `Document` 파일에 대한 개체(를 사용해야 함) `Document` 에서 반환한 개체 `removeUsageRights` 메서드).

**추가 참조**

[PDF 문서에서 사용 권한 제거](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[빠른 시작(SOAP 모드): Java API를 사용하여 PDF 문서에서 사용 권한 제거](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 사용 권한 제거 {#remove-usage-rights-using-the-web-service-api}

Acrobat Reader DC 확장 API(웹 서비스)를 사용하여 권한이 활성화된 PDF 문서에서 사용 권한을 제거합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용하는지 확인합니다. `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` AEM Forms을 호스팅하는 서버의 IP 주소입니다.

1. Acrobat Reader DC 확장 클라이언트 개체를 만듭니다.

   * 만들기 `ReaderExtensionsServiceClient` 기본 생성자를 사용하여 개체를 작성합니다.
   * 만들기 `ReaderExtensionsServiceClient.Endpoint.Address` 을 사용하여 개체 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. 다음을 지정하십시오. `?blob=mtom`.)
   * 만들기 `System.ServiceModel.BasicHttpBinding` 의 값을 가져와서 개체 `ReaderExtensionsServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스트 `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름 할당 `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * 해당 암호 값을 필드에 할당합니다. `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 지정 `HttpClientCredentialType.Basic` 필드에 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 상수 값 지정 `BasicHttpSecurityMode.TransportCredentialOnly` 필드에 `BasicHttpBindingSecurity.Security.Mode`.

1. PDF 문서를 검색합니다.

   * 만들기 `BLOB` 개체를 만들 때 사용됩니다. 다음 `BLOB` 객체는 사용 권한이 제거된 권한이 활성화된 PDF 문서를 저장하는 데 사용됩니다.
   * 만들기 `System.IO.FileStream` PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 콘텐츠를 저장하는 바이트 배열 만들기 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채우기 `System.IO.FileStream` 개체 `Read` 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하는 방법.
   * 채우기 `BLOB` 개체 할당 `MTOM` 속성을 바이트 배열의 콘텐츠와 함께 사용합니다.

1. PDF 문서에서 사용 권한을 제거합니다.

   를 호출하여 PDF 문서에서 사용 권한 제거 `ReaderExtensionsServiceClient` 개체 `removeUsageRights` 메서드 및 전달 `BLOB` 권한이 활성화된 PDF 문서가 포함된 객체입니다. 이 메서드는 `BLOB` 사용 권한이 없는 PDF 문서가 포함된 개체입니다.

1. PDF 문서에 사용 권한을 적용합니다.

   * 만들기 `System.IO.FileStream` 개체를 호출하고 PDF 파일 위치를 나타내는 문자열 값을 전달합니다.
   * 의 데이터 콘텐츠를 저장하는 바이트 배열 만들기 `BLOB` 에서 반환한 개체 `removeUsageRights` 메서드를 사용합니다. 의 값을 가져와서 바이트 배열 채우기 `BLOB` 개체 `MTOM` 데이터 구성원입니다.
   * 만들기 `System.IO.BinaryWriter` 개체를 호출하고 `System.IO.FileStream` 개체.

**추가 참조**

[PDF 문서에서 사용 권한 제거](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 자격 증명 정보 검색 {#retrieving-credential-information}

권한이 활성화된 PDF 문서에 사용 권한을 적용하는 데 사용된 자격 증명에 대한 정보를 검색할 수 있습니다. 자격 증명에 대한 정보를 검색하면 인증서가 더 이상 유효하지 않은 날짜 등의 정보를 얻을 수 있습니다.

>[!NOTE]
>
>Acrobat Reader DC 확장 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-2}

PDF 문서에 사용 권한을 적용하는 데 사용된 자격 증명에 대한 정보를 검색하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. Acrobat Reader DC 확장 클라이언트 개체를 만듭니다.
1. 권한이 활성화된 PDF 문서를 검색합니다.
1. 자격 증명에 대한 정보를 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 생성하는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Acrobat Reader DC 확장 클라이언트 개체 만들기**

Acrobat Reader DC 확장 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 Acrobat Reader DC 확장 서비스 클라이언트 개체를 만들어야 합니다. Java API를 사용하는 경우 `ReaderExtensionsServiceClient` 개체. Acrobat Reader DC 확장 웹 서비스 API를 사용하는 경우 `ReaderExtensionsServiceService` 개체.

**권한이 활성화된 PDF 문서 검색**

자격 증명에 대한 정보를 검색하려면 권한이 활성화된 PDF 문서를 검색해야 합니다. 별칭을 지정하여 자격 증명에 대한 정보를 검색할 수도 있습니다. 그러나 권한이 활성화된 특정 PDF 문서에 사용 권한을 적용하는 데 사용된 자격 증명에 대한 정보를 검색하려면 문서를 검색해야 합니다.

**자격 증명에 대한 정보 검색**

권한이 활성화된 PDF 문서를 검색한 후 사용 권한을 적용하는 데 사용된 자격 증명에 대한 정보를 가져올 수 있습니다. 자격 증명에 대한 다음 정보를 가져올 수 있습니다.

* 권한이 활성화된 PDF 문서를 열 때 Adobe Reader 내에 표시되는 메시지입니다.
* 자격 증명이 더 이상 유효하지 않은 날짜입니다.
* 자격 증명이 유효하지 않은 이전 날짜입니다.
* 이 권한이 활성화된 PDF 문서에 대해 설정된 사용 권한입니다.
* 자격 증명이 사용된 횟수입니다.

**추가 참조**

[Java API를 사용하여 사용 권한 제거](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[웹 서비스 API를 사용하여 사용 권한 제거](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC 확장 서비스 API 빠른 시작](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Java API를 사용하여 자격 증명 정보 검색 {#retrieve-credential-information-using-the-java-api}

Acrobat Reader DC 확장 API(Java)를 사용하여 자격 증명 정보를 검색합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-reader-extensions-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. Acrobat Reader DC 확장 클라이언트 개체를 만듭니다.

   만들기 `ReaderExtensionsServiceClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.

1. PDF 문서를 검색합니다.

   * 만들기 `java.io.FileInputStream` 해당 생성자를 사용하고 권한이 활성화된 PDF 문서의 위치를 지정하는 문자열 값을 전달하여 권한이 활성화된 PDF 문서를 나타내는 개체입니다.
   * 만들기 `com.adobe.idp.Document` 개체를 생성자를 사용하고 `java.io.FileInputStream` 개체.

1. PDF 문서에서 사용 권한을 제거합니다.

   * 를 호출하여 PDF 문서에 사용 권한을 적용하는 데 사용되는 자격 증명에 대한 정보를 검색합니다. `ReaderExtensionsServiceClient` 개체 `getDocumentUsageRights` 메서드 및 전달 `com.adobe.idp.Document` 권한이 활성화된 PDF 문서가 포함된 객체입니다. 이 메서드는 `GetUsageRightsResult` 자격 증명 정보가 포함된 개체입니다.
   * 를 호출하여 자격 증명이 더 이상 유효하지 않은 날짜를 검색합니다. `GetUsageRightsResult` 개체 `getNotAfter` 메서드를 사용합니다. 이 메서드는 `java.util.Date` 자격 증명이 더 이상 유효하지 않은 날짜를 나타내는 개체입니다.
   * 권한이 활성화된 PDF 문서를 열 때 Adobe Reader에 표시되는 메시지를 `GetUsageRightsResult` 개체 `getMessage` 메서드를 사용합니다. 이 메서드는 메시지를 나타내는 문자열 값을 반환합니다.

**추가 참조**

[자격 증명 정보 검색](assigning-usage-rights.md#retrieving-credential-information)

[빠른 시작(SOAP 모드): Java API를 사용하여 자격 증명 정보 검색](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-retrieving-credential-information-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 자격 증명 정보 검색 {#retrieve-credential-information-using-the-web-service-api}

Acrobat Reader DC 확장 API(웹 서비스)를 사용하여 자격 증명 정보를 검색합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용하는지 확인합니다. `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` AEM Forms을 호스팅하는 서버의 IP 주소입니다.

1. Acrobat Reader DC 확장 클라이언트 개체를 만듭니다.

   * 만들기 `ReaderExtensionsServiceClient` 기본 생성자를 사용하여 개체를 작성합니다.
   * 만들기 `ReaderExtensionsServiceClient.Endpoint.Address` 을 사용하여 개체 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. 다음을 지정하십시오. `?blob=mtom`.)
   * 만들기 `System.ServiceModel.BasicHttpBinding` 의 값을 가져와서 개체 `ReaderExtensionsServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스트 `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름 할당 `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * 해당 암호 값을 필드에 할당합니다. `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 지정 `HttpClientCredentialType.Basic` 필드에 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 상수 값 지정 `BasicHttpSecurityMode.TransportCredentialOnly` 필드에 `BasicHttpBindingSecurity.Security.Mode`.

1. PDF 문서를 검색합니다.

   * 만들기 `BLOB` 개체를 만들 때 사용됩니다. 다음 `BLOB` 권한이 활성화된 PDF 문서를 저장하는 데 개체를 사용합니다.
   * 만들기 `System.IO.FileStream` 개체를 호출하고 권한이 활성화된 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여
   * 의 콘텐츠를 저장하는 바이트 배열 만들기 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채우기 `System.IO.FileStream` 개체 `Read` 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하는 방법.
   * 채우기 `BLOB` 개체 할당 `MTOM` 속성을 바이트 배열의 콘텐츠와 함께 사용합니다.

1. PDF 문서에서 사용 권한을 제거합니다.

   * 를 호출하여 PDF 문서에 사용 권한을 적용하는 데 사용되는 자격 증명에 대한 정보를 검색합니다. `ReaderExtensionsServiceClient` 개체 `getDocumentUsageRights` 메서드 및 전달 `com.adobe.idp.Document` 권한이 활성화된 PDF 문서가 포함된 객체입니다. 이 메서드는 `GetUsageRightsResult` 자격 증명 정보가 포함된 개체입니다.
   * 값을 가져와 자격 증명이 더 이상 유효하지 않은 날짜를 검색합니다. `GetUsageRightsResult` 개체 `notAfter` 데이터 구성원입니다. 이 데이터 멤버의 데이터 형식은 입니다. `System.DateTime`.
   * 다음 값을 가져와 권한이 활성화된 PDF 문서를 Adobe Reader에서 열 때 표시되는 메시지를 검색합니다. `GetUsageRightsResult` 개체 `message` 데이터 구성원입니다. 이 데이터 멤버의 데이터 형식이 문자열입니다.
   * 의 값을 가져와 자격 증명이 사용되는 횟수를 검색합니다. `GetUsageRightsResult` 개체 `useCount` 데이터 구성원입니다. 이 데이터 멤버의 데이터 형식이 정수입니다.

**추가 참조**

[자격 증명 정보 검색](assigning-usage-rights.md#retrieving-credential-information)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
