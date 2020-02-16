---
title: 자격 증명 작업
seo-title: 자격 증명 작업
description: 'null'
seo-description: 'null'
uuid: b794428f-49bf-4a91-bc5f-d855881f4f38
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: bc06d9bd-af6c-47b1-b46f-aab990ef5816
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 자격 증명 작업 {#working-with-credentials}

**자격 증명 서비스 정보**

자격 증명에는 문서 서명 또는 식별에 필요한 개인 키 정보가 포함되어 있습니다. 인증서는 신뢰하도록 구성하는 공개 키 정보입니다. AEM Forms에서는 다음과 같은 여러 용도로 인증서 및 자격 증명을 사용합니다.

* Acrobat Reader DC 익스텐션은 자격 증명을 사용하여 PDF 문서에서 Adobe Reader 사용 권한을 활성화합니다. (PDF [문서에 사용 권한 적용을 참조하십시오](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).)
* 서명 서비스는 PDF 문서에 디지털 서명을 하는 등의 작업을 수행하는 동안 인증서와 자격 증명에 액세스합니다. (PDF [문서에 디지털 서명을 참조하십시오](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)

Trust Manager Java API를 사용하여 자격 증명 서비스와 프로그래밍 방식으로 상호 작용할 수 있습니다. 다음 작업을 수행할 수 있습니다.

* [Trust Manager API를 사용하여 자격 증명 가져오기](credentials.md#importing-credentials-by-using-the-trust-manager-api)
* [Trust Manager API를 사용하여 자격 증명 삭제](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

>[!NOTE]
>
>관리 콘솔을 사용하여 인증서를 가져오고 삭제할 수도 있습니다. ( [관리 도움말을 참조하십시오.](https://www.adobe.com/go/learn_aemforms_admin_63))

## Trust Manager API를 사용하여 자격 증명 가져오기 {#importing-credentials-by-using-the-trust-manager-api}

Trust Manager API 파섹 예를 들어 PDF 문서에 서명하는 데 사용되는 자격 증명을 가져올 수 있습니다. (PDF [문서에 디지털 서명 참조](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)).

자격 증명을 가져올 때 자격 증명의 별칭을 지정합니다. 별칭은 자격 증명이 필요한 양식 작업을 수행하는 데 사용됩니다. 자격 증명을 가져온 후에는 다음 그림과 같이 관리 콘솔에서 볼 수 있습니다. 자격 증명의 별칭은 안전합니다 **.

![ww_ww_truststore](assets/ww_ww_truststore.png)

>[!NOTE]
>
>웹 서비스를 사용하여 자격 증명을 AEM Forms로 가져올 수 없습니다.

### 단계 요약 {#summary-of-steps}

자격 증명을 AEM Forms로 가져오려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. 자격 증명 서비스 클라이언트를 만듭니다.
1. 자격 증명을 참조하십시오.
1. 가져오기 작업을 수행합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

다음 JAR 파일을 프로젝트의 클래스 경로에 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar (AEM Forms가 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms가 JBoss에 배포된 경우 필수)

이러한 JAR 파일의 위치에 대한 자세한 내용은 AEM [Forms Java 라이브러리 파일](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)포함을 참조하십시오.

**자격 증명 서비스 클라이언트 만들기**

프로그램 방식으로 자격 증명을 AEM Forms로 가져오기 전에 자격 증명 서비스 클라이언트를 만드십시오. 자세한 내용은 연결 [속성](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)설정을 참조하십시오.

**자격 증명 참조**

AEM Forms로 가져올 자격 증명을 참조합니다. 이 섹션과 연관된 빠른 시작은 파일 시스템에 있는 P12 파일을 참조합니다.

**가져오기 작업 수행**

자격 증명을 참조한 후 자격 증명을 AEM Forms로 가져옵니다. 자격 증명을 가져오지 못하면 예외가 발생합니다. 자격 증명을 가져올 때 자격 증명의 별칭을 지정합니다.

**참고 항목**

[Java API를 사용하여 자격 증명 가져오기](credentials.md#import-credentials-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[자격 증명 서비스 API 빠른 시작](/help/forms/developing/credential-service-java-api-quick.md#credential-service-java-api-quick-start-soap)

[Trust Manager API를 사용하여 자격 증명 삭제](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

### Java API를 사용하여 자격 증명 가져오기 {#import-credentials-using-the-java-api}

Trust Manager API(Java)를 사용하여 자격 증명을 AEM Forms로 가져옵니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-truststore-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. 자격 증명 서비스 클라이언트 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 객체를 전달하여 `CredentialServiceClient` 객체를 만듭니다 `ServiceClientFactory` .

1. 자격 증명 참조

   * 생성자를 사용하여 `java.io.FileInputStream` 객체를 만듭니다. 자격 증명의 위치를 지정하는 문자열 값을 전달합니다.
   * 생성자를 사용하여 자격 증명을 저장하는 `com.adobe.idp.Document` 개체를 `com.adobe.idp.Document` 만듭니다. 자격 증명이 포함된 `java.io.FileInputStream` 개체를 생성자에게 전달합니다.

1. 가져오기 작업 수행

   * 하나의 요소를 포함하는 문자열 배열을 만듭니다. 요소에 값을 `truststore.usage.type.sign` 지정합니다.
   * 객체의 `CredentialServiceClient` `importCredential` 메서드를 호출하고 다음 값을 전달합니다.

      * 자격 증명의 별칭 값을 지정하는 문자열 값입니다.
      * 자격 증명을 저장하는 `com.adobe.idp.Document` 인스턴스입니다.
      * 자격 증명과 관련된 암호를 지정하는 문자열 값입니다.
      * 사용 값을 포함하는 문자열 배열입니다. 예를 들어 이 값을 지정할 수 `truststore.usage.type.sign`있습니다. Reader 확장 자격 증명을 가져오려면 `truststore.usage.type.lcre`지정합니다.

**참고 항목**

[Trust Manager API를 사용하여 자격 증명 가져오기](credentials.md#importing-credentials-by-using-the-trust-manager-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 자격 증명 가져오기](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-importing-credentials-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Trust Manager API를 사용하여 자격 증명 삭제 {#deleting-credentials-by-using-the-trust-manager-api}

Trust Manager API를 사용하여 자격 증명을 프로그래밍 방식으로 삭제할 수 있습니다. 자격 증명을 삭제할 때 자격 증명에 해당하는 별칭을 지정합니다. 삭제하면 자격 증명을 사용하여 작업을 수행할 수 없습니다.

>[!NOTE]
>
>웹 서비스를 사용하여 AEM Forms로 자격 증명을 삭제할 수 없습니다.

### 단계 요약 {#summary_of_steps-1}

자격 증명을 삭제하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. 자격 증명 서비스 클라이언트를 만듭니다.
1. 삭제 작업을 수행합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 다음 JAR 파일을 프로젝트의 클래스 경로에 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar (AEM Forms가 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms가 JBoss에 배포된 경우 필수)

이러한 JAR 파일의 위치에 대한 자세한 내용은 AEM [Forms Java 라이브러리 파일](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)포함을 참조하십시오.

**자격 증명 서비스 클라이언트 만들기**

자격 증명을 프로그래밍 방식으로 삭제하려면 먼저 데이터 통합 서비스 클라이언트를 만드십시오. 서비스 클라이언트를 만들 때 서비스를 호출하는 데 필요한 연결 설정을 정의합니다. 자세한 내용은 연결 [속성](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)설정을 참조하십시오.

**삭제 작업 수행**

자격 증명을 삭제하려면 자격 증명에 해당하는 별칭을 지정합니다. 존재하지 않는 별칭을 지정하면 예외가 발생합니다.

**참고 항목**

[Java API를 사용하여 자격 증명 가져오기](credentials.md#import-credentials-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Java API를 사용하여 자격 증명 가져오기](credentials.md#import-credentials-using-the-java-api)

### Java API를 사용하여 자격 증명 삭제 {#deleting-credentials-using-the-java-api}

Trust Manager API(Java)를 사용하여 AEM Forms에서 자격 증명을 삭제합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-truststore-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. 자격 증명 서비스 클라이언트 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 객체를 전달하여 `CredentialServiceClient` 객체를 만듭니다 `ServiceClientFactory` .

1. 삭제 작업 수행

   객체의 `CredentialServiceClient` `deleteCredential` 메서드를 호출하고 별칭 값을 지정하는 문자열 값을 전달합니다.

**참고 항목**

[Trust Manager API를 사용하여 자격 증명 삭제](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 자격 증명 삭제](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-deleting-credentials-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
