---
title: 사용 권한 할당
seo-title: 사용 권한 할당
description: 'null'
seo-description: 'null'
uuid: 8c2020df-ea3c-49fa-916f-38a458f40d2b
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9e8db506-9ace-4e1f-8a7b-c4e9b15dde7e
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7

---


# 사용 권한 할당 {#assigning-usage-rights}

## Acrobat Reader DC 확장 서비스 정보 {#about-the-acrobat-reader-dc-extensions-service}

Acrobat Reader DC 확장 서비스를 사용하면 조직은 Adobe Reader의 기능을 확장하여 인터랙티브한 PDF 문서를 손쉽게 공유할 수 있습니다. Acrobat Reader DC 확장 서비스는 PDF 1.7까지 포함한 모든 PDF 문서를 완벽하게 지원합니다.Adobe Reader 7.0 이상에서 사용할 수 있습니다. 이 서비스는 PDF 문서에 사용 권한을 추가함으로써 Adobe Reader를 사용하여 PDF 문서를 열 때 일반적으로 사용할 수 없는 기능을 활성화합니다. 서드 파티 사용자는 권한이 있는 문서를 사용하여 작업할 추가 소프트웨어 또는 플러그인을 요구하지 않습니다.

Acrobat Reader DC 확장 서비스를 사용하여 다음 작업을 수행할 수 있습니다.

* PDF 문서에 사용 권한 적용 자세한 내용은 PDF [문서에 사용 권한 적용을 참조하십시오](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).
* PDF 문서에서 사용 권한 제거 자세한 내용은 PDF [문서에서 사용 권한 제거를 참조하십시오](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents).
* 자격 증명 세부 정보 검색 자세한 내용은 자격 증명 정보 [검색을 참조하십시오](assigning-usage-rights.md#retrieving-credential-information).

>[!NOTE]
>
>Acrobat Reader DC 확장 서비스에 대한 자세한 내용은 AEM Forms [에 대한 서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

## PDF 문서에 사용 권한 적용 {#applying-usage-rights-to-pdf-documents}

Acrobat Reader DC 확장 Java Client API 및 웹 서비스를 사용하여 PDF 문서에 사용 권한을 적용할 수 있습니다. 사용 권한은 Acrobat에서는 기본적으로 사용할 수 있지만 Adobe Reader에서는 사용할 수 없는 기능(예: 양식에 주석을 추가하거나 양식 필드를 채우고 양식을 저장하는 기능)과 관련이 있습니다. 사용 권한이 적용된 PDF 문서를 권한 사용 문서라고 합니다. Adobe Reader에서 권한이 활성화된 문서를 여는 사용자는 해당 특정 문서에 대해 활성화된 작업을 수행할 수 있습니다.

>[!NOTE]
>
>Java API의 일부인 `applyUsageRights` 방법을 사용하여 PDF 문서에 사용 권한을 적용할 때 `isModeFinal` 개체의 `ReaderExtensionsOptionSpec` 매개 변수를 로 설정할 수 있습니다 `false`. 이로 인해 양식 처리 카운터가 업데이트되지 않고 성능이 개선됩니다. 처리된 양식 카운터의 업데이트에 관심이 없다면 `isModeFinal` 매개 변수를 로 설정하는 것이 좋습니다 `false`.

>[!NOTE]
>
>Acrobat Reader DC 확장 서비스에 대한 자세한 내용은 AEM Forms [에 대한 서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary-of-steps}

PDF 문서에 사용 권한을 적용하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. Acrobat Reader DC 확장 클라이언트 개체를 만듭니다.
1. PDF 문서 검색
1. 적용할 사용 권한을 지정합니다.
1. PDF 문서에 사용 권한 적용
1. 권한이 활성화된 PDF 문서를 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Acrobat Reader DC 확장 클라이언트 개체 만들기**

프로그래밍 방식으로 Acrobat Reader DC 확장 기능 서비스 작업을 수행하려면 Acrobat Reader DC 확장 서비스 클라이언트 개체를 만들어야 합니다. Acrobat Reader DC 확장 Java API를 사용하는 경우 `ReaderExtensionsServiceClient` 개체를 만듭니다. Acrobat Reader DC 확장 웹 서비스 API를 사용하는 경우 `ReaderExtensionsServiceService` 개체를 만듭니다.

**PDF 문서 검색**

사용 권한을 적용하려면 PDF 문서를 검색해야 합니다. 권한이 활성화된 PDF 문서에는 사용 권한 사전이 포함되어 있습니다. Adobe Reader에서 이러한 사전이 포함된 문서를 열면 해당 문서의 사전에서 지정한 사용 권한만 활성화됩니다. 문서에 사용 권한 사전이 없는 경우 Acrobat Reader DC 확장 서비스가 이를 만듭니다. 사전에 있는 경우 Acrobat Reader DC 확장 서비스는 기존 사용 권한을 지정한 사용 권한으로 덮어씁니다. 사전은 어떤 사용 권한을 활성화할지 지정합니다. 사용자가 Adobe Reader에서 문서를 열면 사전에서 지정한 사용 권한만 허용됩니다.

**적용할 사용 권한 지정**

설정할 수 있는 사용 권한은 Adobe Systems Incorporated에서 구입한 자격 증명에 의해 결정됩니다. 자격 증명은 일반적으로 대화형 양식과 관련된 사용 권한 그룹과 같은 관련 사용 권한 그룹을 설정할 수 있는 권한을 제공합니다. 각 자격 증명은 권한이 부여된 특정 수의 PDF 문서를 작성할 수 있는 권한을 제공합니다. 평가 자격 증명은 무제한 초안 문서를 만들 수 있는 권한을 제공합니다.

>[!NOTE]
>
>자격 증명에서 허용되지 않는 사용 권한을 할당하려고 하면 예외가 발생합니다.

**PDF 문서에 사용 권한 적용**

PDF 문서에 사용 권한을 적용하려면 사용 권한을 적용하는 데 사용하는 자격 증명의 별칭을 참조하십시오(자격 증명은 일반적으로 AEM Forms 설치 중에 설치됨). 또한 사용 권한이 적용되는 PDF 문서를 지정해야 합니다. 자격 증명 구성에 대한 자세한 내용은 응용 프로그램 서버에 대한 설치 및 배포 안내서를 참조하십시오.

**권한이 활성화된 PDF 문서 저장**

Acrobat Reader DC 확장 서비스가 PDF 문서에 사용 권한을 적용하면 권한이 활성화된 PDF 문서를 PDF 파일로 저장할 수 있습니다.

**참고 항목**

[Java API를 사용하여 사용 권한 적용](assigning-usage-rights.md#apply-usage-rights-using-the-java-api)

[웹 서비스 API를 사용하여 사용 권한 적용](assigning-usage-rights.md#apply-usage-rights-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC Extensions Service API 빠른 시작](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Java API를 사용하여 사용 권한 적용 {#apply-usage-rights-using-the-java-api}

Acrobat Reader DC Extensions API(Java)를 사용하여 PDF 문서에 사용 권한 적용:

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-reader-extensions-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. Acrobat Reader DC 확장 클라이언트 개체를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 객체를 전달하여 `ReaderExtensionsServiceClient` 객체를 만듭니다 `ServiceClientFactory` .

1. PDF 문서 검색

   * 생성자를 사용하여 PDF 문서의 위치를 지정하는 문자열 값을 전달하여 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만듭니다.
   * 생성자를 사용하여 객체를 전달하여 `com.adobe.idp.Document` 객체를 만듭니다 `java.io.FileInputStream` .

1. 적용할 사용 권한을 지정합니다.

   * 생성자를 사용하여 사용 권한을 나타내는 `UsageRights` 개체를 만듭니다.
   * 적용할 각 사용 권한에 대해 `UsageRights` 개체에 속하는 해당 메서드를 호출합니다. 예를 들어 `enableFormFillIn` 사용 권한을 추가하려면 `UsageRights` 개체의 `enableFormFillIn` 메서드를 호출하고 전달하십시오 `true`. 적용할 각 사용 권한에 대해 이 단계를 반복합니다.

1. PDF 문서에 사용 권한 적용

   * 생성자를 사용하여 `ReaderExtensionsOptionSpec` 객체를 만듭니다. 이 개체에는 Acrobat Reader DC 확장 서비스에 필요한 런타임 옵션이 포함되어 있습니다. 이 생성자를 호출할 때는 다음 값을 지정해야 합니다.

      * 문서에 적용할 사용 권한이 포함된 `UsageRights` 개체입니다.
      * Adobe Reader 7.x에서 권한이 활성화된 PDF 문서를 열 때 사용자에게 표시되는 메시지를 지정하는 문자열 값입니다.이 메시지는 Adobe Reader 8.0에 표시되지 않습니다.
   * 개체의 `ReaderExtensionsServiceClient` `applyUsageRights` 메서드를 호출하고 다음 값을 전달하여 PDF 문서에 사용 권한을 적용합니다.

      * 사용 권한이 적용되는 PDF 문서를 포함하는 `com.adobe.idp.Document` 개체입니다.
      * 사용 권한을 적용할 수 있는 자격 증명의 별칭을 지정하는 문자열 값.
      * 해당 암호 값을 지정하는 문자열 값입니다. (현재 이 매개 변수는 무시됩니다. 통과하셔도 `null`됩니다.)
   * 런타임 옵션이 포함된 `ReaderExtensionsOptionSpec` 객체입니다.
   이 `applyUsageRights` `com.adobe.idp.Document` 메서드는 권한이 활성화된 PDF 문서를 포함하는 개체를 반환합니다.

1. 권한이 활성화된 PDF 문서를 저장합니다.

   * 개체를 만들고 파일 확장자가 .pdf인지 확인합니다. `java.io.File`
   * 객체의 메서드를 호출하여 `com.adobe.idp.Document` 객체의 내용을 파일에 복사합니다( `copyToFile` 메서드에서 반환된 `com.adobe.idp.Document` `com.adobe.idp.Document` `applyUsageRights` 객체를 사용하는지 확인).

**참고 항목**

[PDF 문서에 사용 권한 적용](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[빠른 시작(SOAP 모드):Java API를 사용하여 사용 권한 적용](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-applying-usage-rights-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 사용 권한 적용 {#apply-usage-rights-using-the-web-service-api}

Acrobat Reader DC Extensions API(웹 서비스)를 사용하여 PDF 문서에 사용 권한 적용:

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`Adobe

   >[!NOTE]
   >
   >AEM `localhost` Forms를 호스팅하는 서버의 IP 주소로 대체합니다.

1. Acrobat Reader DC 확장 클라이언트 개체를 만듭니다.

   * 기본 생성자를 사용하여 `ReaderExtensionsServiceClient` 객체를 만듭니다.
   * 생성자를 사용하여 `ReaderExtensionsServiceClient.Endpoint.Address` 객체를 만듭니다 `System.ServiceModel.EndpointAddress` . WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`). 지정해야 `?blob=mtom`합니다.)
   * 필드의 값을 가져와 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다 `ReaderExtensionsServiceClient.Endpoint.Binding` . 반환 값을 로 `BasicHttpBinding`캐스팅합니다.
   * 개체 `System.ServiceModel.BasicHttpBinding` 필드를 로 설정합니다 `MessageEncoding` . `WSMessageEncoding.Mtom` 이 값을 사용하면 MTOM이 사용됩니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * AEM 양식 사용자 이름을 필드에 `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`지정합니다.
      * 필드에 해당 암호 값을 지정합니다 `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * 필드에 상수 값을 `HttpClientCredentialType.Basic` 지정합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 필드에 상수 값을 `BasicHttpSecurityMode.TransportCredentialOnly` 지정합니다 `BasicHttpBindingSecurity.Security.Mode`.

1. PDF 문서 검색

   * 생성자를 사용하여 `BLOB` 객체를 만듭니다. 이 `BLOB` 개체는 사용 권한이 적용되는 PDF 문서를 저장하는 데 사용됩니다.
   * 생성자를 호출하고 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * 개체의 내용을 저장하는 바이트 배열을 `System.IO.FileStream` 만듭니다. 개체의 `System.IO.FileStream` `Length` 속성을 가져와 바이트 배열의 크기를 결정할 수 있습니다.
   * 개체의 `System.IO.FileStream` `Read` 메서드를 호출하여 바이트 배열을 스트림 데이터로 채웁니다. 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달합니다.
   * 바이트 배열의 컨텐츠로 해당 `BLOB` `MTOM` 속성을 할당하여 객체를 채웁니다.

1. 적용할 사용 권한을 지정합니다.

   * 생성자를 사용하여 사용 권한을 나타내는 `UsageRights` 개체를 만듭니다.
   * 적용할 각 사용 권한에 대해, 객체에 `true` 속하는 해당 데이터 멤버에 값을 할당합니다 `UsageRights` . 예를 들어 `enableFormFillIn` 사용 권한을 추가하려면 개체의 `true` `UsageRights` `enableFormFillIn` 데이터 멤버에 할당합니다. 적용할 각 사용 권한에 대해 이 단계를 반복합니다.

1. PDF 문서에 사용 권한 적용

   * 생성자를 사용하여 `ReaderExtensionsOptionSpec` 객체를 만듭니다. 이 개체에는 Acrobat Reader DC 확장 서비스에 필요한 런타임 옵션이 포함되어 있습니다.
   * 개체의 `UsageRights` `ReaderExtensionsOptionSpec` `usageRights` 데이터 멤버에 개체를 할당합니다.
   * Adobe Reader에서 권한이 활성화된 PDF 문서를 열면 사용자에게 표시되는 메시지를 `ReaderExtensionsOptionSpec` 개체의 `message` 데이터 구성원에게 지정하는 문자열 값을 지정합니다.
   * 개체의 `ReaderExtensionsServiceClient` `applyUsageRights` 메서드를 호출하고 다음 값을 전달하여 PDF 문서에 사용 권한을 적용합니다.

      * 사용 권한이 적용되는 PDF 문서를 포함하는 `BLOB` 개체입니다.
      * 사용 권한을 적용할 수 있는 자격 증명의 별칭을 지정하는 문자열 값.
      * 해당 암호 값을 지정하는 문자열 값입니다. (현재 이 매개 변수는 무시됩니다. 통과하셔도 `null`됩니다.)
   * 런타임 옵션이 포함된 `ReaderExtensionsOptionSpec` 객체입니다.
   이 `applyUsageRights` `BLOB` 메서드는 권한이 활성화된 PDF 문서를 포함하는 개체를 반환합니다.

1. 권한이 활성화된 PDF 문서를 저장합니다.

   * 생성자를 호출하여 `System.IO.FileStream` 객체를 만듭니다. 권한이 활성화된 PDF 문서의 파일 위치를 나타내는 문자열 값을 전달합니다.
   * 메서드에서 반환된 `BLOB` 개체의 데이터 내용을 저장하는 바이트 배열을 `applyUsageRights` 만듭니다. 개체 데이터 멤버의 값을 가져와 바이트 배열을 `BLOB` 채웁니다 `MTOM` .
   * 생성자를 호출하고 객체를 전달하여 `System.IO.BinaryWriter` `System.IO.FileStream` 객체를 만듭니다.
   * 개체의 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 PDF 파일에 씁니다. `System.IO.BinaryWriter` `Write`

**참고 항목**

[PDF 문서에 사용 권한 적용](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## PDF 문서에서 사용 권한 제거 {#removing-usage-rights-from-pdf-documents}

권한이 활성화된 문서에서 사용 권한을 제거할 수 있습니다. 권한이 활성화된 PDF 문서에서 사용 권한을 제거하는 것도 다른 AEM Forms 작업을 수행하기 위해 필요합니다. 예를 들어 사용 권한을 설정하기 전에 PDF 문서에 디지털 서명(또는 인증)해야 합니다. 따라서 권한이 부여된 문서에서 작업을 수행하려면 PDF 문서에서 사용 권한을 제거하고 문서에 디지털 서명을 하는 등 다른 작업을 수행한 다음 사용 권한을 다시 적용해야 합니다.

>[!NOTE]
>
>Acrobat Reader DC 확장 서비스에 대한 자세한 내용은 AEM Forms [에 대한 서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-1}

권한이 활성화된 PDF 문서에서 사용 권한을 제거하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. Acrobat Reader DC 확장 클라이언트 개체를 만듭니다.
1. 권한이 부여된 PDF 문서 검색
1. PDF 문서에서 사용 권한을 제거합니다.
1. PDF 문서를 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Acrobat Reader DC 확장 클라이언트 개체 만들기**

프로그래밍 방식으로 Acrobat Reader DC 확장 서비스 작업을 수행하려면 먼저 Acrobat Reader DC 확장 서비스 클라이언트 개체를 만들어야 합니다. Java API를 사용하는 경우 `ReaderExtensionsServiceClient` 개체를 만듭니다. Acrobat Reader DC 확장 웹 서비스 API를 사용하는 경우 `ReaderExtensionsServiceService` 개체를 만듭니다.

**권한이 부여된 PDF 문서 검색**

사용 권한을 제거하기 위해 권한이 활성화된 PDF 문서를 검색할 수 있습니다.

**PDF 문서에서 사용 권한 제거**

권한이 활성화된 PDF 문서를 검색한 후 사용 권한을 제거할 수 있습니다. 사용 권한을 제거하면 Adobe Reader 내에서 보는 동안 PDF 문서에 추가 기능이 없습니다.

**PDF 문서 저장**

사용 권한이 더 이상 포함되지 않은 PDF 문서를 PDF 파일로 저장할 수 있습니다. PDF 파일로 저장하면 Adobe Reader 또는 Acrobat에서 PDF 문서를 볼 수 있습니다.

**참고 항목**

[Java API를 사용하여 사용 권한 제거](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[웹 서비스 API를 사용하여 사용 권한 제거](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC Extensions Service API 빠른 시작](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

[PDF 문서에 사용 권한 적용](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

### Java API를 사용하여 사용 권한 제거 {#remove-usage-rights-using-the-java-api}

Acrobat Reader DC 확장 API(Java)를 사용하여 권한이 활성화된 PDF 문서에서 사용 권한을 제거합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-reader-extensions-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. Acrobat Reader DC 확장 클라이언트 개체를 만듭니다.

   생성자를 사용하여 `ReaderExtensionsServiceClient` 객체를 만들고 연결 속성이 포함된 `ServiceClientFactory` 객체를 전달합니다.

1. PDF 문서 검색

   * 생성자를 사용하여 PDF 문서의 위치를 지정하는 문자열 값을 전달하여 권한이 활성화된 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만듭니다.
   * 생성자를 사용하여 객체를 전달하여 `com.adobe.idp.Document` 객체를 만듭니다 `java.io.FileInputStream` .

1. PDF 문서에서 사용 권한을 제거합니다.

   개체의 `ReaderExtensionsServiceClient` 방법을 호출하고 권한이 활성화된 PDF 문서가 포함된 `removeUsageRights` `com.adobe.idp.Document` 개체를 전달하여 PDF 문서에서 사용 권한을 제거합니다. 이 메서드는 사용 권한이 없는 PDF 문서를 포함하는 `com.adobe.idp.Document` 개체를 반환합니다.

1. PDF 문서에 사용 권한 적용

   * 개체를 만들고 파일 확장자가 .PDF인지 확인합니다. `java.io.File`
   * 객체의 메서드를 호출하여 `Document` 객체의 내용을 파일에 복사합니다( `copyToFile` 메서드에서 반환된 `Document` `Document` `removeUsageRights` 객체를 사용하는지 확인).

**참고 항목**

[PDF 문서에서 사용 권한 제거](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[빠른 시작(SOAP 모드):Java API를 사용하여 PDF 문서에서 사용 권한 제거](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 사용 권한 제거 {#remove-usage-rights-using-the-web-service-api}

Acrobat Reader DC 확장 API(웹 서비스)를 사용하여 권한이 활성화된 PDF 문서에서 사용 권한을 제거합니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`Adobe

   >[!NOTE]
   >
   >AEM `localhost` Forms를 호스팅하는 서버의 IP 주소로 대체합니다.

1. Acrobat Reader DC 확장 클라이언트 개체를 만듭니다.

   * 기본 생성자를 사용하여 `ReaderExtensionsServiceClient` 객체를 만듭니다.
   * 생성자를 사용하여 `ReaderExtensionsServiceClient.Endpoint.Address` 객체를 만듭니다 `System.ServiceModel.EndpointAddress` . WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`). 지정해야 `?blob=mtom`합니다.)
   * 필드의 값을 가져와 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다 `ReaderExtensionsServiceClient.Endpoint.Binding` . 반환 값을 로 `BasicHttpBinding`캐스팅합니다.
   * 개체 `System.ServiceModel.BasicHttpBinding` 필드를 로 설정합니다 `MessageEncoding` . `WSMessageEncoding.Mtom` 이 값을 사용하면 MTOM이 사용됩니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * AEM 양식 사용자 이름을 필드에 `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`지정합니다.
      * 필드에 해당 암호 값을 지정합니다 `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * 필드에 상수 값을 `HttpClientCredentialType.Basic` 지정합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 필드에 상수 값을 `BasicHttpSecurityMode.TransportCredentialOnly` 지정합니다 `BasicHttpBindingSecurity.Security.Mode`.

1. PDF 문서 검색

   * 생성자를 사용하여 `BLOB` 객체를 만듭니다. 이 `BLOB` 개체는 사용 권한이 제거되는 PDF 문서를 저장하는 데 사용됩니다.
   * 생성자를 호출하고 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * 개체의 내용을 저장하는 바이트 배열을 `System.IO.FileStream` 만듭니다. 개체의 `System.IO.FileStream` `Length` 속성을 가져와 바이트 배열의 크기를 결정할 수 있습니다.
   * 객체의 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다. `System.IO.FileStream` `Read`
   * 바이트 배열의 컨텐츠로 해당 `BLOB` `MTOM` 속성을 할당하여 객체를 채웁니다.

1. PDF 문서에서 사용 권한을 제거합니다.

   개체의 `ReaderExtensionsServiceClient` 방법을 호출하고 권한이 활성화된 PDF 문서가 포함된 `removeUsageRights` `BLOB` 개체를 전달하여 PDF 문서에서 사용 권한을 제거합니다. 이 메서드는 사용 권한이 없는 PDF 문서를 포함하는 `BLOB` 개체를 반환합니다.

1. PDF 문서에 사용 권한 적용

   * 생성자를 호출하고 PDF 파일 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * 메서드에서 반환된 `BLOB` 개체의 데이터 내용을 저장하는 바이트 배열을 `removeUsageRights` 만듭니다. 개체 데이터 멤버의 값을 가져와 바이트 배열을 `BLOB` 채웁니다 `MTOM` .
   * 생성자를 호출하고 객체를 전달하여 `System.IO.BinaryWriter` `System.IO.FileStream` 객체를 만듭니다.

**참고 항목**

[PDF 문서에서 사용 권한 제거](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 자격 증명 정보 검색 {#retrieving-credential-information}

사용 권한을 사용 가능한 PDF 문서에 적용하는 데 사용된 자격 증명에 대한 정보를 검색할 수 있습니다. 자격 증명에 대한 정보를 검색하여 인증서가 더 이상 유효하지 않은 날짜 등의 정보를 얻을 수 있습니다.

>[!NOTE]
>
>Acrobat Reader DC 확장 서비스에 대한 자세한 내용은 AEM Forms [에 대한 서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-2}

PDF 문서에 사용 권한을 적용하는 데 사용된 자격 증명에 대한 정보를 검색하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. Acrobat Reader DC 확장 클라이언트 개체를 만듭니다.
1. 권한이 부여된 PDF 문서 검색
1. 자격 증명에 대한 정보를 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Acrobat Reader DC 확장 클라이언트 개체 만들기**

프로그래밍 방식으로 Acrobat Reader DC 확장 서비스 작업을 수행하려면 먼저 Acrobat Reader DC 확장 서비스 클라이언트 개체를 만들어야 합니다. Java API를 사용하는 경우 `ReaderExtensionsServiceClient` 개체를 만듭니다. Acrobat Reader DC 확장 웹 서비스 API를 사용하는 경우 `ReaderExtensionsServiceService` 개체를 만듭니다.

**권한이 부여된 PDF 문서 검색**

자격 증명에 대한 정보를 검색하려면 권한이 있는 PDF 문서를 검색해야 합니다. 별칭을 지정하여 자격 증명에 대한 정보를 검색할 수도 있습니다.그러나 사용 권한을 사용 가능한 특정 PDF 문서에 적용하는 데 사용된 자격 증명에 대한 정보를 검색하려면 해당 문서를 검색해야 합니다.

**자격 증명에 대한 정보 검색**

권한이 활성화된 PDF 문서를 검색한 후 사용 권한을 적용하는 데 사용한 자격 증명에 대한 정보를 얻을 수 있습니다. 자격 증명에 대한 다음 정보를 얻을 수 있습니다.

* 권한이 활성화된 PDF 문서를 열 때 Adobe Reader 내에 표시되는 메시지입니다.
* 자격 증명이 더 이상 유효하지 않은 날짜입니다.
* 자격 증명이 유효하지 않은 이전 날짜입니다.
* 이 권한이 활성화된 PDF 문서에 설정된 사용 권한
* 자격 증명을 사용한 횟수입니다.

**참고 항목**

[Java API를 사용하여 사용 권한 제거](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[웹 서비스 API를 사용하여 사용 권한 제거](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC Extensions Service API 빠른 시작](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Java API를 사용하여 자격 증명 정보 검색 {#retrieve-credential-information-using-the-java-api}

Acrobat Reader DC 확장 API(Java)를 사용하여 자격 증명 정보를 검색합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-reader-extensions-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. Acrobat Reader DC 확장 클라이언트 개체를 만듭니다.

   생성자를 사용하여 `ReaderExtensionsServiceClient` 객체를 만들고 연결 속성이 포함된 `ServiceClientFactory` 객체를 전달합니다.

1. PDF 문서 검색

   * 해당 생성자를 사용하여 권한이 활성화된 PDF 문서의 위치를 지정하는 문자열 값을 전달하여 권한이 활성화된 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만듭니다.
   * 생성자를 사용하여 객체를 전달하여 `com.adobe.idp.Document` 객체를 만듭니다 `java.io.FileInputStream` .

1. PDF 문서에서 사용 권한을 제거합니다.

   * 개체의 `ReaderExtensionsServiceClient` 방법을 호출하고 권한이 활성화된 PDF 문서가 포함된 `getDocumentUsageRights` `com.adobe.idp.Document` 개체를 전달하여 PDF 문서에 사용 권한을 적용하는 데 사용된 자격 증명에 대한 정보를 검색합니다. 이 메서드는 자격 증명 정보를 포함하는 `GetUsageRightsResult` 개체를 반환합니다.
   * 개체의 `GetUsageRightsResult` `getNotAfter` 메서드를 호출하여 자격 증명이 더 이상 유효하지 않은 날짜를 검색합니다. 이 메서드는 자격 증명이 더 이상 유효하지 않은 이후의 날짜를 나타내는 `java.util.Date` 개체를 반환합니다.
   * 개체의 `GetUsageRightsResult` `getMessage` 방법을 호출하여 권한이 활성화된 PDF 문서를 열 때 Adobe Reader에 표시되는 메시지를 검색합니다. 이 메서드는 메시지를 나타내는 문자열 값을 반환합니다.

**참고 항목**

[자격 증명 정보 검색](assigning-usage-rights.md#retrieving-credential-information)

[빠른 시작(SOAP 모드):Java API를 사용하여 자격 증명 정보 검색](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-retrieving-credential-information-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 자격 증명 정보 검색 {#retrieve-credential-information-using-the-web-service-api}

Acrobat Reader DC 확장 API(웹 서비스)를 사용하여 자격 증명 정보 검색:

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`Adobe

   >[!NOTE]
   >
   >AEM `localhost` Forms를 호스팅하는 서버의 IP 주소로 대체합니다.

1. Acrobat Reader DC 확장 클라이언트 개체를 만듭니다.

   * 기본 생성자를 사용하여 `ReaderExtensionsServiceClient` 객체를 만듭니다.
   * 생성자를 사용하여 `ReaderExtensionsServiceClient.Endpoint.Address` 객체를 만듭니다 `System.ServiceModel.EndpointAddress` . WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`). 지정해야 `?blob=mtom`합니다.)
   * 필드의 값을 가져와 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다 `ReaderExtensionsServiceClient.Endpoint.Binding` . 반환 값을 로 `BasicHttpBinding`캐스팅합니다.
   * 개체 `System.ServiceModel.BasicHttpBinding` 필드를 로 설정합니다 `MessageEncoding` . `WSMessageEncoding.Mtom` 이 값을 사용하면 MTOM이 사용됩니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * AEM 양식 사용자 이름을 필드에 `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`지정합니다.
      * 필드에 해당 암호 값을 지정합니다 `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * 필드에 상수 값을 `HttpClientCredentialType.Basic` 지정합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 필드에 상수 값을 `BasicHttpSecurityMode.TransportCredentialOnly` 지정합니다 `BasicHttpBindingSecurity.Security.Mode`.

1. PDF 문서 검색

   * 생성자를 사용하여 `BLOB` 객체를 만듭니다. 이 `BLOB` 개체는 권한이 활성화된 PDF 문서를 저장하는 데 사용됩니다.
   * 생성자를 호출하고 권한이 활성화된 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * 개체의 내용을 저장하는 바이트 배열을 `System.IO.FileStream` 만듭니다. 개체의 `System.IO.FileStream` `Length` 속성을 가져와 바이트 배열의 크기를 결정할 수 있습니다.
   * 객체의 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다. `System.IO.FileStream` `Read`
   * 바이트 배열의 컨텐츠로 해당 `BLOB` `MTOM` 속성을 할당하여 객체를 채웁니다.

1. PDF 문서에서 사용 권한을 제거합니다.

   * 개체의 `ReaderExtensionsServiceClient` 방법을 호출하고 권한이 활성화된 PDF 문서가 포함된 `getDocumentUsageRights` `com.adobe.idp.Document` 개체를 전달하여 PDF 문서에 사용 권한을 적용하는 데 사용된 자격 증명에 대한 정보를 검색합니다. 이 메서드는 자격 증명 정보를 포함하는 `GetUsageRightsResult` 개체를 반환합니다.
   * 개체의 데이터 멤버 값을 가져와서 자격 증명이 더 이상 유효하지 않은 날짜를 `GetUsageRightsResult` 검색합니다 `notAfter` . 이 데이터 멤버의 데이터 유형은 입니다 `System.DateTime`.
   * Adobe Reader에서 권한이 활성화된 PDF 문서를 열 때 `GetUsageRightsResult` 개체의 `message` 데이터 멤버의 값을 가져와 표시되는 메시지를 검색합니다. 이 데이터 멤버의 데이터 유형은 문자열입니다.
   * 개체의 데이터 멤버 값을 가져와서 자격 증명을 사용하는 횟수를 `GetUsageRightsResult` 검색합니다 `useCount` . 이 데이터 멤버의 데이터 유형은 정수입니다.

**참고 항목**

[자격 증명 정보 검색](assigning-usage-rights.md#retrieving-credential-information)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
