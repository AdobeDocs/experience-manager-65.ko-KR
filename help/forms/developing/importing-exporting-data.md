---
title: 데이터 가져오기 및 내보내기
seo-title: 데이터 가져오기 및 내보내기
description: 'null'
seo-description: 'null'
uuid: 94ccb6f2-6e5f-43ea-a954-9a4402871a17
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2e783745-c986-45ba-8e65-7437d114ca38
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2742'
ht-degree: 0%

---


# 데이터 가져오기 및 내보내기 {#importing-and-exporting-data}

## 양식 데이터 통합 서비스 {#about-the-form-data-integration-service} 정보

양식 데이터 통합 서비스는 데이터를 PDF 양식으로 가져와서 PDF 양식의 데이터를 내보낼 수 있습니다. 가져오기 및 내보내기 작업은 두 가지 유형의 PDF forms을 지원합니다.

* Acrobat 양식(Acrobat에서 작성)은 양식 필드가 포함된 PDF 문서입니다.
* Designer에서 만든 Adobe XML 양식은 XFA(XML Adobe XML Forms 아키텍처)를 준수하는 PDF 문서입니다.

양식 데이터는 PDF 양식 유형에 따라 다음 형식 중 하나로 존재할 수 있습니다.

* XFDF 파일로, Acrobat 양식 데이터 형식의 XML 버전입니다.
* 양식 필드 정의를 포함하는 XML 파일인 XDP 파일입니다. 또한 양식 필드 데이터와 포함된 PDF 파일을 포함할 수 있습니다. 디자이너가 생성한 XDP 파일은 기본 64로 인코딩된 PDF 문서가 포함된 경우에만 사용할 수 있습니다.

양식 데이터 통합 서비스를 사용하여 다음 작업을 수행할 수 있습니다.

* PDF forms으로 데이터 가져오기 자세한 내용은 [양식 데이터 가져오기](importing-exporting-data.md#importing-form-data)를 참조하십시오.
* PDF forms에서 데이터 내보내기 자세한 내용은 [양식 데이터 내보내기](importing-exporting-data.md#exporting-form-data)를 참조하십시오.

>[!NOTE]
>
>양식 데이터 통합 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

## 양식 데이터 가져오기 {#importing-form-data}

양식 데이터 통합 서비스를 사용하여 양식 데이터를 대화형 PDF forms으로 가져올 수 있습니다. 인터랙티브한 PDF 양식이란 사용자의 정보를 수집하거나 사용자 정의 정보를 표시하기 위한 필드가 하나 이상 포함되어 있는 PDF 문서입니다. 양식 데이터 통합 서비스는 양식 계산, 유효성 검사 또는 스크립팅을 지원하지 않습니다.

Designer에서 만든 양식으로 데이터를 가져오려면 유효한 XDP XML 데이터 소스를 참조해야 합니다. 다음 예제 모기지 신청서 양식을 고려하십시오.

![ie_ie_loanformodata](assets/ie_ie_loanformdata.png)

이 양식으로 데이터 값을 가져오려면 양식에 해당하는 유효한 XDP XML 데이터 소스가 있어야 합니다. 임의의 XML 데이터 소스를 사용하여 양식 데이터 통합 서비스를 사용하여 데이터를 양식으로 가져올 수 없습니다. 임의 XML 데이터 소스와 XDP XML 데이터 소스의 차이점은 XDP 데이터 소스가 XFA(XML Forms 아키텍처)를 준수한다는 점입니다. 다음 XML은 예제 모기지 애플리케이션 양식에 해당하는 XDP XML 데이터 소스를 나타냅니다.

```xml
 <?xml version="1.0" encoding="UTF-8" ?>
 - <xfa:datasets xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
 - <xfa:data>
 - <data>
     - <Layer>
         <closeDate>1/26/2007</closeDate>
         <lastName>Johnson</lastName>
         <firstName>Jerry</firstName>
         <mailingAddress>JJohnson@NoMailServer.com</mailingAddress>
         <city>New York</city>
         <zipCode>00501</zipCode>
         <state>NY</state>
         <dateBirth>26/08/1973</dateBirth>
         <middleInitials>D</middleInitials>
         <socialSecurityNumber>(555) 555-5555</socialSecurityNumber>
         <phoneNumber>5555550000</phoneNumber>
     </Layer>
     - <Mortgage>
         <mortgageAmount>295000.00</mortgageAmount>
         <monthlyMortgagePayment>1724.54</monthlyMortgagePayment>
         <purchasePrice>300000</purchasePrice>
         <downPayment>5000</downPayment>
         <term>25</term>
         <interestRate>5.00</interestRate>
     </Mortgage>
 </data>
 </xfa:data>
 </xfa:datasets>
```

>[!NOTE]
>
>양식 데이터 통합 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### {#summary-of-steps} 단계 요약

양식 데이터를 PDF 양식으로 가져오려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. 양식 데이터 통합 서비스 클라이언트를 만듭니다.
1. PDF 양식 참조
1. XML 데이터 소스를 참조합니다.
1. 데이터를 PDF 양식으로 가져올 수 있습니다.
1. PDF 양식을 PDF 파일로 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

다음 JAR 파일을 프로젝트의 클래스 경로에 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss에 배포된 경우 필요)
* jbossall-client.jar (AEM Forms이 JBoss에 배포된 경우 필수)

이러한 JAR 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)을 참조하십시오.

**양식 데이터 통합 서비스 클라이언트 만들기**

프로그래밍 방식으로 데이터를 PDF 양식 클라이언트 API로 가져오기 전에 데이터 통합 서비스 클라이언트를 만들어야 합니다. 서비스 클라이언트를 만들 때 서비스를 호출하는 데 필요한 연결 설정을 정의합니다. 자세한 내용은 [연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)을 참조하십시오.

**PDF 양식 참조**

데이터를 PDF 양식으로 가져오려면 Designer에서 만든 XML 양식이나 Acrobat에서 만든 Acrobat 양식을 참조해야 합니다.

**XML 데이터 소스 참조**

양식 데이터를 가져오려면 유효한 데이터 소스를 참조해야 합니다. Designer에서 만든 XFA XML 양식으로 데이터를 가져오려면 XDP XML 데이터 소스를 사용해야 합니다. Acrobat 양식을 참조하면 XFDF 데이터 소스를 사용해야 합니다. 데이터를 가져올 각 필드에 대해 값을 지정해야 합니다. XML 데이터 소스에 있는 요소가 양식의 필드에 해당되지 않는 경우 요소는 무시됩니다.

**PDF 양식으로 데이터 가져오기**

PDF 양식과 유효한 XML 데이터 소스를 참조한 후 데이터를 PDF 양식으로 가져올 수 있습니다.

**PDF 양식을 PDF 파일로 저장**

데이터를 양식으로 가져온 후 양식을 PDF 파일로 저장할 수 있습니다. PDF 파일로 저장한 후에는 Adobe Reader 또는 Acrobat에서 양식을 열고 가져온 데이터가 포함된 양식을 볼 수 있습니다.

**참고 항목**

[Java API를 사용하여 양식 데이터 가져오기](importing-exporting-data.md#import-form-data-using-the-java-api)

[웹 서비스 API를 사용하여 양식 데이터 가져오기](importing-exporting-data.md#import-form-data-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[양식 데이터 통합 서비스 API 빠른 시작](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[양식 데이터 내보내기](importing-exporting-data.md#exporting-form-data)

### Java API {#import-form-data-using-the-java-api}를 사용하여 양식 데이터 가져오기

양식 데이터 통합 API(Java)를 사용하여 양식 데이터를 가져옵니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-formdataintegration-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. 양식 데이터 통합 서비스 클라이언트를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 `FormDataIntegrationClient` 개체를 만들고 `ServiceClientFactory` 개체를 전달합니다.

1. PDF 양식 참조

   * 생성자를 사용하여 `java.io.FileInputStream` 개체를 만듭니다. PDF 양식의 위치를 지정하는 문자열 값을 전달합니다.
   * `com.adobe.idp.Document` 생성자를 사용하여 PDF 양식을 저장하는 `com.adobe.idp.Document` 개체를 만듭니다. PDF 양식이 포함된 `java.io.FileInputStream` 개체를 생성자에게 전달합니다.

1. XML 데이터 소스를 참조합니다.

   * 생성자를 사용하여 `java.io.FileInputStream` 개체를 만들고 폼으로 가져올 데이터가 포함된 XML 파일의 위치를 지정하는 문자열 값을 전달합니다.
   * `com.adobe.idp.Document` 생성자를 사용하여 양식 데이터를 저장하는 `com.adobe.idp.Document` 개체를 만듭니다. 양식 데이터가 포함된 `java.io.FileInputStream` 개체를 생성자에 전달합니다.

1. 데이터를 PDF 양식으로 가져올 수 있습니다.

   `FormDataIntegrationClient` 개체의 `importData` 메서드를 호출하고 다음 값을 전달하여 데이터를 PDF 양식으로 가져옵니다.

   * PDF 양식을 저장하는 `com.adobe.idp.Document` 개체
   * 양식 데이터를 저장하는 `com.adobe.idp.Document` 개체입니다.

   `importData` 메서드는 XML 데이터 소스에 있는 데이터를 포함하는 PDF 양식을 저장하는 `com.adobe.idp.Document` 개체를 반환합니다.

1. PDF 양식을 PDF 파일로 저장합니다.

   * `java.io.File` 개체를 만들고 파일 확장자가 &quot;.PDF&quot;인지 확인합니다.
   * `Document` 개체의 `copyToFile` 메서드를 호출하여 `Document` 개체의 내용을 파일에 복사합니다.(`importData` 메서드에서 반환된 `Document` 개체를 사용해야 합니다.)

**참고 항목**

[단계 요약](importing-exporting-data.md#summary-of-steps)

[빠른 시작(SOAP 모드):Java API를 사용하여 양식 데이터 가져오기](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-importing-form-data-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API {#import-form-data-using-the-web-service-api}를 사용하여 양식 데이터 가져오기

양식 데이터 통합 API(웹 서비스)를 사용하여 양식 데이터를 가져옵니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다.`http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 대체합니다.

1. 양식 데이터 통합 서비스 클라이언트를 만듭니다.

   * 기본 생성자를 사용하여 `FormDataIntegrationClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `FormDataIntegrationClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`). `lc_version` 특성을 사용할 필요는 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다. 그러나 MTOM을 사용하려면 `?blob=mtom`을 지정합니다.
   * `FormDataIntegrationClient.Endpoint.Binding` 필드의 값을 가져와 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`으로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`로 설정합니다. 이 값을 사용하면 MTOM이 사용됩니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * AEM 양식 사용자 이름을 `FormDataIntegrationClient.ClientCredentials.UserName.UserName` 필드에 지정합니다.
      * 해당 암호 값을 `FormDataIntegrationClient.ClientCredentials.UserName.Password` 필드에 지정합니다.
      * 상수 값 `HttpClientCredentialType.Basic`을 `BasicHttpBindingSecurity.Transport.ClientCredentialType` 필드에 할당합니다.
      * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을 `BasicHttpBindingSecurity.Security.Mode` 필드에 할당합니다.

1. PDF 양식 참조

   * 생성자를 사용하여 `BLOB` 개체를 만듭니다. 이 `BLOB` 개체는 PDF 양식을 저장하는 데 사용됩니다.
   * 생성자를 호출하여 `System.IO.FileStream` 개체를 만듭니다. PDF 양식의 위치와 파일을 열 모드를 지정하는 문자열 값을 전달합니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하여 바이트 배열을 스트림 데이터로 채웁니다. 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 바이트 배열의 내용으로 `MTOM` 필드를 할당하여 `BLOB` 개체를 채웁니다.

1. XML 데이터 소스를 참조합니다.

   * 생성자를 사용하여 `BLOB` 개체를 만듭니다. 이 `BLOB` 개체는 폼으로 가져온 데이터를 저장하는 데 사용됩니다.
   * 생성자를 호출하여 `System.IO.FileStream` 개체를 만듭니다. 가져올 데이터가 포함된 XML 파일의 위치와 파일을 열 모드를 지정하는 문자열 값을 전달합니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하여 바이트 배열을 스트림 데이터로 채웁니다. 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 바이트 배열의 내용으로 `MTOM` 필드를 할당하여 `BLOB` 개체를 채웁니다.

1. 데이터를 PDF 양식으로 가져올 수 있습니다.

   `FormDataIntegrationClient` 개체의 `importData` 메서드를 호출하고 다음 값을 전달하여 데이터를 PDF 양식으로 가져옵니다.

   * PDF 양식을 저장하는 `BLOB` 개체
   * 양식 데이터를 저장하는 `BLOB` 개체입니다.

   `importData` 메서드는 XML 데이터 소스에 있는 데이터를 포함하는 PDF 양식을 저장하는 `BLOB` 개체를 반환합니다.

1. PDF 양식을 PDF 파일로 저장합니다.

   * 생성자를 호출하고 PDF 파일의 파일 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `importData` 메서드에서 반환된 `BLOB` 개체의 데이터 내용을 저장하는 바이트 배열을 만듭니다. `BLOB` 개체의 `MTOM` 필드의 값을 가져와 바이트 배열을 채웁니다.
   * 생성자를 호출하고 `System.IO.FileStream` 개체를 전달하여 `System.IO.BinaryWriter` 개체를 만듭니다.
   * `System.IO.BinaryWriter` 개체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 PDF 파일에 기록합니다.

**참고 항목**

[단계 요약](importing-exporting-data.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 양식 데이터 내보내기 {#exporting-form-data}

양식 데이터 통합 서비스를 사용하여 대화형 PDF 양식에서 양식 데이터를 내보낼 수 있습니다. 내보낼 데이터의 형식은 양식 유형에 따라 다릅니다. 양식 유형이 Acrobat에서 만든 Acrobat 양식이면 내보낸 데이터는 XFDF입니다. 양식 유형이 Designer에서 만든 XML 양식이면 내보낸 데이터는 XDP입니다.

>[!NOTE]
>
>양식 데이터 통합 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### {#summary_of_steps-1} 단계 요약

PDF 양식에서 양식 데이터를 내보내려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. 양식 데이터 통합 서비스 클라이언트를 만듭니다.
1. PDF 양식 참조
1. PDF 양식에서 데이터 내보내기
1. 내보낸 데이터를 XML 파일로 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

다음 JAR 파일을 프로젝트의 클래스 경로에 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss에 배포된 경우 필요)
* jbossall-client.jar (AEM Forms이 JBoss에 배포된 경우 필수)

**양식 데이터 통합 서비스 클라이언트 만들기**

프로그래밍 방식으로 데이터를 PDF formClient API로 가져오기 전에 데이터 통합 서비스 클라이언트를 만들어야 합니다. 서비스 클라이언트를 만들 때 서비스를 호출하는 데 필요한 연결 설정을 정의합니다. 자세한 내용은 [연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**PDF 양식 참조**

PDF 양식의 데이터를 내보내려면 Designer 또는 Facebook에서 만든 PDF 양식이며 양식 데이터가 들어 있는 PDF 양식을 참조해야 합니다. 빈 PDF 양식에서 데이터를 내보내려고 하면 빈 XML 스키마가 표시됩니다.

**PDF 양식에서 데이터 내보내기**

양식 데이터가 포함된 PDF 양식을 참조하면 양식에서 데이터를 내보낼 수 있습니다. 데이터는 양식을 기반으로 하는 XML 스키마 내에서 내보내집니다.

**양식 데이터를 XML 파일로 저장**

양식 데이터를 내보낸 후 데이터를 XML 파일로 저장할 수 있습니다. XML 파일로 저장한 후에는 XML 뷰어 내에서 XML 파일을 열어 양식 데이터를 볼 수 있습니다.

**참고 항목**

[Java API를 사용하여 양식 데이터 내보내기](importing-exporting-data.md#export-form-data-using-the-java-api)

[웹 서비스 API를 사용하여 양식 데이터 내보내기](importing-exporting-data.md#export-form-data-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[양식 데이터 통합 서비스 API 빠른 시작](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[양식 데이터 가져오기](importing-exporting-data.md#importing-form-data)

### Java API {#export-form-data-using-the-java-api}를 사용하여 양식 데이터 내보내기

양식 데이터 통합 API(Java)를 사용하여 양식 데이터를 내보냅니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-formdataintegration-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. 양식 데이터 통합 서비스 클라이언트를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 `FormDataIntegrationClient` 개체를 만들고 `ServiceClientFactory` 개체를 전달합니다.

1. PDF 양식 참조

   * 생성자를 사용하여 `java.io.FileInputStream` 개체를 만들고 내보낼 데이터가 포함된 PDF 양식의 위치를 지정하는 문자열 값을 전달합니다.
   * `com.adobe.idp.Document` 생성자를 사용하여 PDF 양식을 저장하는 `com.adobe.idp.Document` 개체를 만듭니다. PDF 양식이 포함된 `java.io.FileInputStream` 개체를 생성자에게 전달합니다.

1. PDF 양식에서 데이터 내보내기

   `FormDataIntegrationClient` 개체의 `exportData` 메서드를 호출하여 양식 데이터를 내보내고 PDF 양식을 저장하는 `com.adobe.idp.Document` 개체를 전달합니다. 이 메서드는 양식 데이터를 XML 스키마로 저장하는 `com.adobe.idp.Document` 개체를 반환합니다.

1. PDF 양식을 PDF 파일로 저장합니다.

   * `java.io.File` 개체를 만들고 파일 확장자가 XML인지 확인합니다.
   * `Document` 개체의 `copyToFile` 메서드를 호출하여 `Document` 개체의 내용을 파일에 복사합니다.(`exportData` 메서드에서 반환된 `Document` 개체를 사용해야 합니다.)

**참고 항목**

[단계 요약](importing-exporting-data.md#summary-of-steps)

[빠른 시작(SOAP 모드):Java API를 사용하여 양식 데이터 내보내기](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-exporting-form-data-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API {#export-form-data-using-the-web-service-api}를 사용하여 양식 데이터 내보내기

양식 데이터 통합 API(웹 서비스)를 사용하여 양식 데이터를 내보냅니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다.`http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   * `localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 대체합니다.

1. 양식 데이터 통합 서비스 클라이언트를 만듭니다.

   * 기본 생성자를 사용하여 `FormDataIntegrationClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `FormDataIntegrationClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`). `lc_version` 특성을 사용할 필요는 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다. 그러나 MTOM을 사용하려면 `?blob=mtom`을 지정합니다.
   * `FormDataIntegrationClient.Endpoint.Binding` 필드의 값을 가져와 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`으로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`로 설정합니다. 이 값을 사용하면 MTOM이 사용됩니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * AEM 양식 사용자 이름을 `FormDataIntegrationClient.ClientCredentials.UserName.UserName` 필드에 지정합니다.
      * 해당 암호 값을 `FormDataIntegrationClient.ClientCredentials.UserName.Password` 필드에 지정합니다.
      * 상수 값 `HttpClientCredentialType.Basic`을 `BasicHttpBindingSecurity.Transport.ClientCredentialType` 필드에 할당합니다.
      * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을 `BasicHttpBindingSecurity.Security.Mode` 필드에 할당합니다.

1. PDF 양식 참조

   * 생성자를 사용하여 `BLOB` 개체를 만듭니다. 이 `BLOB` 개체는 데이터를 내보낼 PDF 양식을 저장하는 데 사용됩니다.
   * 생성자를 호출하여 `System.IO.FileStream` 개체를 만듭니다. PDF 양식의 위치와 파일을 열 모드를 지정하는 문자열 값을 전달합니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * 바이트 배열의 내용으로 `MTOM` 필드를 할당하여 `BLOB` 개체를 채웁니다.

1. PDF 양식에서 데이터 내보내기

   `FormDataIntegrationClient` 개체의 `exportData` 메서드를 호출하여 데이터를 PDF 양식으로 가져오고 PDF 양식을 저장하는 `BLOB` 개체를 전달합니다. 이 메서드는 양식 데이터를 XML 스키마로 저장하는 `BLOB` 개체를 반환합니다.

1. PDF 양식을 PDF 파일로 저장합니다.

   * 생성자를 호출하고 XML 파일의 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `exportData` 메서드에서 반환된 `BLOB` 개체의 데이터 내용을 저장하는 바이트 배열을 만듭니다. `BLOB` 개체의 `MTOM` 필드의 값을 가져와 바이트 배열을 채웁니다.
   * 생성자를 호출하고 `System.IO.FileStream` 개체를 전달하여 `System.IO.BinaryWriter` 개체를 만듭니다.
   * `System.IO.BinaryWriter` 개체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 XML 파일에 씁니다.

**참고 항목**

[단계 요약](importing-exporting-data.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
