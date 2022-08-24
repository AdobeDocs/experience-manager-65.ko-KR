---
title: 데이터 가져오기 및 내보내기
seo-title: Importing and Exporting Data
description: 양식 데이터 통합 서비스를 사용하여 데이터를 PDF 양식으로 가져오고 Java API 및 웹 서비스 API를 사용하여 PDF 양식에서 데이터를 내보냅니다.
seo-description: Use the Form Data Integration service to import data into a PDF form and export data from a PDF form using the Java API and Web Service API.
uuid: 94ccb6f2-6e5f-43ea-a954-9a4402871a17
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2e783745-c986-45ba-8e65-7437d114ca38
role: Developer
exl-id: 96310e0a-8e95-4a55-9508-5298b8d67f83
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '2778'
ht-degree: 0%

---

# 데이터 가져오기 및 내보내기 {#importing-and-exporting-data}

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms용입니다.**

## 양식 데이터 통합 서비스 정보 {#about-the-form-data-integration-service}

양식 데이터 통합 서비스는 데이터를 PDF 양식으로 가져오고 PDF 양식에서 데이터를 내보낼 수 있습니다. 가져오기 및 내보내기 작업은 두 가지 유형의 PDF forms을 지원합니다.

* Acrobat 양식(Acrobat에서 작성)은 양식 필드를 포함하는 PDF 문서입니다.
* 디자이너에서 만든 Adobe XML 양식은 XFA(XML Adobe XML Forms Architecture)를 준수하는 PDF 문서입니다.

양식 데이터는 PDF 양식 유형에 따라 다음 형식 중 하나에 있을 수 있습니다.

* Acrobat 양식 데이터 형식의 XML 버전인 XFDF 파일입니다.
* 양식 필드 정의를 포함하는 XML 파일인 XDP 파일입니다. 양식 필드 데이터와 포함된 PDF 파일도 포함할 수 있습니다. 디자이너에서 생성한 XDP 파일은 포함된 기본-64로 인코딩된 PDF 문서를 포함하는 경우에만 사용할 수 있습니다.

양식 데이터 통합 서비스를 사용하여 다음 작업을 수행할 수 있습니다.

* 데이터를 PDF forms으로 가져옵니다. 자세한 내용은 [양식 데이터 가져오기](importing-exporting-data.md#importing-form-data).
* PDF forms에서 데이터를 내보냅니다. 자세한 내용은 [양식 데이터 내보내기](importing-exporting-data.md#exporting-form-data).

>[!NOTE]
>
>양식 데이터 통합 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

## 양식 데이터 가져오기 {#importing-form-data}

양식 데이터 통합 서비스를 사용하여 양식 데이터를 대화형 PDF forms으로 가져올 수 있습니다. 대화형 PDF 양식은 사용자의 정보를 수집하거나 사용자 지정 정보를 표시하기 위한 필드를 하나 이상 포함하는 PDF 문서입니다. 양식 데이터 통합 서비스는 양식 계산, 유효성 검사 또는 스크립팅을 지원하지 않습니다.

Designer에서 만든 양식으로 데이터를 가져오려면 유효한 XDP XML 데이터 소스를 참조해야 합니다. 다음 예제 모기지 신청 양식을 고려하십시오.

![ie_ie_loanformdata](assets/ie_ie_loanformdata.png)

데이터 값을 이 양식으로 가져오려면 양식에 해당하는 유효한 XDP XML 데이터 소스가 있어야 합니다. 임의의 XML 데이터 소스를 사용하여 양식 데이터 통합 서비스를 사용하여 데이터를 양식으로 가져올 수 없습니다. 임의 XML 데이터 소스와 XDP XML 데이터 소스의 차이점은 XDP 데이터 소스가 XFA(XML Forms Architecture)를 준수하다는 것입니다. 다음 XML은 예제 모기지 응용 프로그램 양식에 해당하는 XDP XML 데이터 소스를 나타냅니다.

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
>양식 데이터 통합 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary-of-steps}

양식 데이터를 PDF 양식으로 가져오려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. 양식 데이터 통합 서비스 클라이언트를 만듭니다.
1. PDF 양식을 참조합니다.
1. XML 데이터 소스를 참조합니다.
1. 데이터를 PDF 양식으로 가져옵니다.
1. PDF 양식을 PDF 파일로 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

다음 JAR 파일을 프로젝트의 클래스 경로에 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar(AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms이 JBoss에 배포되는 경우 필수)

이러한 JAR 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**양식 데이터 통합 서비스 클라이언트 만들기**

데이터를 프로그래밍 방식으로 클라이언트 API의 PDF으로 가져오려면 먼저 데이터 통합 서비스 클라이언트를 만들어야 합니다. 서비스 클라이언트를 만들 때 서비스를 호출하는 데 필요한 연결 설정을 정의합니다. 자세한 내용은 [연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**PDF 양식 참조**

데이터를 PDF 양식으로 가져오려면 디자이너에서 만든 XML 양식이나 Acrobat에서 만든 Acrobat 양식을 참조해야 합니다.

**XML 데이터 소스 참조**

양식 데이터를 가져오려면 유효한 데이터 소스를 참조해야 합니다. Designer에서 만든 XFA XML 양식으로 데이터를 가져오려면 XDP XML 데이터 소스를 사용해야 합니다. Acrobat 양식을 참조하는 경우 XFDF 데이터 소스를 사용해야 합니다. 데이터를 로 가져올 각 필드에 대해 값을 지정해야 합니다. XML 데이터 소스에 있는 요소가 양식의 필드에 해당하지 않으면 요소가 무시됩니다.

**PDF 양식으로 데이터 가져오기**

PDF 양식 및 유효한 XML 데이터 소스를 참조한 후 데이터를 PDF 양식으로 가져올 수 있습니다.

**PDF 양식을 PDF 파일로 저장**

데이터를 양식으로 가져온 후에는 양식을 PDF 파일로 저장할 수 있습니다. PDF 파일로 저장되면 Adobe Reader 또는 Acrobat에서 양식을 열고 가져온 데이터가 있는 양식을 볼 수 있습니다.

**추가 참조**

[Java API를 사용하여 양식 데이터 가져오기](importing-exporting-data.md#import-form-data-using-the-java-api)

[웹 서비스 API를 사용하여 양식 데이터 가져오기](importing-exporting-data.md#import-form-data-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[양식 데이터 통합 서비스 API 빠른 시작](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[양식 데이터 내보내기](importing-exporting-data.md#exporting-form-data)

### Java API를 사용하여 양식 데이터 가져오기 {#import-form-data-using-the-java-api}

양식 데이터 통합 API(Java)를 사용하여 양식 데이터를 가져옵니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-formdataintegration-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. 양식 데이터 통합 서비스 클라이언트를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 객체입니다.
   * 만들기 `FormDataIntegrationClient` 생성자를 사용하여 객체를 전달하고 `ServiceClientFactory` 개체.

1. PDF 양식을 참조합니다.

   * 만들기 `java.io.FileInputStream` 생성자를 사용하여 개체를 작성합니다. PDF 양식의 위치를 지정하는 문자열 값을 전달합니다.
   * 만들기 `com.adobe.idp.Document` 를 사용하여 PDF 양식을 저장하는 개체 `com.adobe.idp.Document` 생성자입니다. 전달 `java.io.FileInputStream` 생성자에 PDF 양식을 포함하는 객체입니다.

1. XML 데이터 소스를 참조합니다.

   * 만들기 `java.io.FileInputStream` 개체를 생성자로 사용하고 양식에 가져올 데이터가 포함된 XML 파일의 위치를 지정하는 문자열 값을 전달합니다.
   * 만들기 `com.adobe.idp.Document` 양식 데이터를 저장하는 개체 `com.adobe.idp.Document` 생성자입니다. 전달 `java.io.FileInputStream` 생성자에 양식 데이터가 포함된 객체입니다.

1. 데이터를 PDF 양식으로 가져옵니다.

   를 호출하여 PDF 양식으로 데이터 가져오기 `FormDataIntegrationClient` 개체 `importData` 메서드 및 다음 값 전달:

   * 다음 `com.adobe.idp.Document` PDF 양식을 저장하는 개체입니다.
   * 다음 `com.adobe.idp.Document` 양식 데이터를 저장하는 개체.

   다음 `importData` 메서드 반환 `com.adobe.idp.Document` XML 데이터 소스에 있는 데이터가 포함된 PDF 양식을 저장하는 개체입니다.

1. PDF 양식을 PDF 파일로 저장합니다.

   * 만들기 `java.io.File` 개체 및 파일 확장자가 &quot;.PDF&quot;인지 확인합니다.
   * 를 호출합니다 `Document` 개체 `copyToFile` 컨텐츠의 내용 복사 방법 `Document` 개체를 파일에 추가합니다. `Document` 반환되는 개체 `importData` 메서드).

**추가 참조**

[단계 요약](importing-exporting-data.md#summary-of-steps)

[빠른 시작(SOAP 모드): Java API를 사용하여 양식 데이터 가져오기](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-importing-form-data-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 양식 데이터 가져오기 {#import-form-data-using-the-web-service-api}

양식 데이터 통합 API(웹 서비스)를 사용하여 양식 데이터를 가져옵니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` (AEM Forms을 호스팅하는 서버의 IP 주소 사용)

1. 양식 데이터 통합 서비스 클라이언트를 만듭니다.

   * 만들기 `FormDataIntegrationClient` 기본 생성자를 사용하여 개체를 만듭니다.
   * 만들기 `FormDataIntegrationClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`) 를 사용할 필요가 없습니다 `lc_version` 속성을 사용합니다. 이 속성은 서비스 참조를 만들 때 사용됩니다. 하지만, `?blob=mtom` MTOM을 사용하려면 다음을 수행하십시오.
   * 만들기 `System.ServiceModel.BasicHttpBinding` 개체의 값을 가져와서 `FormDataIntegrationClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스팅합니다. `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름을 지정합니다 `FormDataIntegrationClient.ClientCredentials.UserName.UserName`.
      * 필드에 해당 암호 값을 지정합니다 `FormDataIntegrationClient.ClientCredentials.UserName.Password`.
      * 상수 값 할당 `HttpClientCredentialType.Basic` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 상수 값 할당 `BasicHttpSecurityMode.TransportCredentialOnly` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Security.Mode`.

1. PDF 양식을 참조합니다.

   * 만들기 `BLOB` 생성자를 사용하여 개체를 작성합니다. 이 `BLOB` 개체는 PDF 양식을 저장하는 데 사용됩니다.
   * 만들기 `System.IO.FileStream` 개체를 생성자로 호출하여 개체를 가져옵니다. PDF 양식의 위치와 파일을 열 모드를 지정하는 문자열 값을 전달합니다.
   * 의 내용을 저장하는 바이트 배열을 만듭니다 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성을 사용합니다.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채웁니다 `System.IO.FileStream` 개체 `Read` 메서드를 사용합니다. 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 을(를) 채우기 `BLOB` 개체를 할당하여 개체를 개체 개체 `MTOM` 바이트 배열의 내용을 포함하는 필드입니다.

1. XML 데이터 소스를 참조합니다.

   * 만들기 `BLOB` 생성자를 사용하여 개체를 작성합니다. 이 `BLOB` 개체는 양식으로 가져오는 데이터를 저장하는 데 사용됩니다.
   * 만들기 `System.IO.FileStream` 개체를 생성자로 호출하여 개체를 가져옵니다. 가져올 데이터가 포함된 XML 파일의 위치와 파일을 열 모드를 지정하는 문자열 값을 전달합니다.
   * 의 내용을 저장하는 바이트 배열을 만듭니다 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성을 사용합니다.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채웁니다 `System.IO.FileStream` 개체 `Read` 메서드를 사용합니다. 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 을(를) 채우기 `BLOB` 개체를 할당하여 개체를 개체 개체 `MTOM` 바이트 배열의 내용을 포함하는 필드입니다.

1. 데이터를 PDF 양식으로 가져옵니다.

   를 호출하여 PDF 양식으로 데이터 가져오기 `FormDataIntegrationClient` 개체 `importData` 메서드 및 다음 값 전달:

   * 다음 `BLOB` PDF 양식을 저장하는 개체입니다.
   * 다음 `BLOB` 양식 데이터를 저장하는 개체.

   다음 `importData` 메서드 반환 `BLOB` XML 데이터 소스에 있는 데이터가 포함된 PDF 양식을 저장하는 개체입니다.

1. PDF 양식을 PDF 파일로 저장합니다.

   * 만들기 `System.IO.FileStream` 객체를 사용하여 해당 생성자를 호출하고 PDF 파일의 파일 위치를 나타내는 문자열 값을 전달합니다.
   * 의 데이터 내용을 저장하는 바이트 배열을 만듭니다 `BLOB` 반환되는 개체 `importData` 메서드를 사용합니다. 의 값을 가져와서 바이트 배열을 채웁니다 `BLOB` 개체 `MTOM` 필드.
   * 만들기 `System.IO.BinaryWriter` 생성자를 호출하고 전달하여 개체를 `System.IO.FileStream` 개체.
   * 를 호출하여 PDF 파일에 바이트 배열의 내용을 씁니다. `System.IO.BinaryWriter` 개체 `Write` 메서드를 사용하여 바이트 배열을 전달합니다.

**추가 참조**

[단계 요약](importing-exporting-data.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 양식 데이터 내보내기 {#exporting-form-data}

양식 데이터 통합 서비스를 사용하여 대화형 PDF 양식에서 양식 데이터를 내보낼 수 있습니다. 내보내는 데이터의 형식은 양식 유형에 따라 다릅니다. 양식 유형이 Acrobat에서 만든 Acrobat 양식인 경우 내보낸 데이터는 XFDF입니다. 양식 형식이 디자이너에서 만든 XML 양식인 경우 내보낸 데이터는 XDP입니다.

>[!NOTE]
>
>양식 데이터 통합 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-1}

PDF 양식에서 양식 데이터를 내보내려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. 양식 데이터 통합 서비스 클라이언트를 만듭니다.
1. PDF 양식을 참조합니다.
1. PDF 양식에서 데이터를 내보냅니다.
1. 내보낸 데이터를 XML 파일로 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

다음 JAR 파일을 프로젝트의 클래스 경로에 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar(AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms이 JBoss에 배포되는 경우 필수)

**양식 데이터 통합 서비스 클라이언트 만들기**

데이터를 프로그래밍 방식으로 PDF formClient API로 가져오려면 먼저 데이터 통합 서비스 클라이언트를 만들어야 합니다. 서비스 클라이언트를 만들 때 서비스를 호출하는 데 필요한 연결 설정을 정의합니다. 자세한 내용은 [연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**PDF 양식 참조**

PDF 양식에서 데이터를 내보내려면 디자이너 또는 Acrobat에서 만든 양식 및 양식 데이터가 포함된 PDF 양식을 참조해야 합니다. 빈 PDF 양식에서 데이터를 내보내려고 하면 빈 XML 스키마가 제공됩니다.

**PDF 양식에서 데이터 내보내기**

양식 데이터가 포함된 PDF 양식을 참조하면 양식에서 데이터를 내보낼 수 있습니다. 데이터는 양식을 기반으로 하는 XML 스키마 내에 내보내집니다.

**양식 데이터를 XML 파일로 저장**

양식 데이터를 내보낸 후 데이터를 XML 파일로 저장할 수 있습니다. XML 파일로 저장되면 XML 뷰어 내에서 XML 파일을 열어 양식 데이터를 볼 수 있습니다.

**추가 참조**

[Java API를 사용하여 양식 데이터 내보내기](importing-exporting-data.md#export-form-data-using-the-java-api)

[웹 서비스 API를 사용하여 양식 데이터 내보내기](importing-exporting-data.md#export-form-data-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[양식 데이터 통합 서비스 API 빠른 시작](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[양식 데이터 가져오기](importing-exporting-data.md#importing-form-data)

### Java API를 사용하여 양식 데이터 내보내기 {#export-form-data-using-the-java-api}

양식 데이터 통합 API(Java)를 사용하여 양식 데이터를 내보냅니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-formdataintegration-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. 양식 데이터 통합 서비스 클라이언트를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 객체입니다.
   * 만들기 `FormDataIntegrationClient` 생성자를 사용하여 객체를 전달하고 `ServiceClientFactory` 개체.

1. PDF 양식을 참조합니다.

   * 만들기 `java.io.FileInputStream` 개체를 생성자로 사용하고 내보낼 데이터가 포함된 PDF 양식의 위치를 지정하는 문자열 값을 전달합니다.
   * 만들기 `com.adobe.idp.Document` 를 사용하여 PDF 양식을 저장하는 개체 `com.adobe.idp.Document` 생성자입니다. 전달 `java.io.FileInputStream` 생성자에 PDF 양식을 포함하는 객체입니다.

1. PDF 양식에서 데이터를 내보냅니다.

   를 호출하여 양식 데이터를 내보냅니다 `FormDataIntegrationClient` 개체 `exportData` 메서드 및 전달 `com.adobe.idp.Document` PDF 양식을 저장하는 개체입니다. 이 메서드는 `com.adobe.idp.Document` 양식 데이터를 XML 스키마로 저장하는 개체입니다.

1. PDF 양식을 PDF 파일로 저장합니다.

   * 만들기 `java.io.File` 개체 및 파일 확장자가 XML인지 확인합니다.
   * 를 호출합니다 `Document` 개체 `copyToFile` 컨텐츠의 내용 복사 방법 `Document` 개체를 파일에 추가합니다. `Document` 반환되는 개체 `exportData` 메서드).

**추가 참조**

[단계 요약](importing-exporting-data.md#summary-of-steps)

[빠른 시작(SOAP 모드): Java API를 사용하여 양식 데이터 내보내기](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-exporting-form-data-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 양식 데이터 내보내기 {#export-form-data-using-the-web-service-api}

양식 데이터 통합 API(웹 서비스)를 사용하여 양식 데이터를 내보냅니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   * 바꾸기 `localhost` (AEM Forms을 호스팅하는 서버의 IP 주소 사용)

1. 양식 데이터 통합 서비스 클라이언트를 만듭니다.

   * 만들기 `FormDataIntegrationClient` 기본 생성자를 사용하여 개체를 만듭니다.
   * 만들기 `FormDataIntegrationClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`) 를 사용할 필요가 없습니다 `lc_version` 속성을 사용합니다. 이 속성은 서비스 참조를 만들 때 사용됩니다. 하지만, `?blob=mtom` MTOM을 사용하려면 다음을 수행하십시오.
   * 만들기 `System.ServiceModel.BasicHttpBinding` 개체의 값을 가져와서 `FormDataIntegrationClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스팅합니다. `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름을 지정합니다 `FormDataIntegrationClient.ClientCredentials.UserName.UserName`.
      * 필드에 해당 암호 값을 지정합니다 `FormDataIntegrationClient.ClientCredentials.UserName.Password`.
      * 상수 값 할당 `HttpClientCredentialType.Basic` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 상수 값 할당 `BasicHttpSecurityMode.TransportCredentialOnly` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Security.Mode`.

1. PDF 양식을 참조합니다.

   * 만들기 `BLOB` 생성자를 사용하여 개체를 작성합니다. 이 `BLOB` 개체는 데이터를 내보내는 PDF 양식을 저장하는 데 사용됩니다.
   * 만들기 `System.IO.FileStream` 개체를 생성자로 호출하여 개체를 가져옵니다. PDF 양식의 위치와 파일을 열 모드를 지정하는 문자열 값을 전달합니다.
   * 의 내용을 저장하는 바이트 배열을 만듭니다 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성을 사용합니다.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채웁니다 `System.IO.FileStream` 개체 `Read` 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하는 메서드와 전달
   * 을(를) 채우기 `BLOB` 개체를 할당하여 개체를 개체 개체 `MTOM` 바이트 배열의 내용을 포함하는 필드입니다.

1. PDF 양식에서 데이터를 내보냅니다.

   를 호출하여 PDF 양식으로 데이터 가져오기 `FormDataIntegrationClient` 개체 `exportData` 메서드 및 전달 `BLOB` PDF 양식을 저장하는 개체입니다. 이 메서드는 `BLOB` 양식 데이터를 XML 스키마로 저장하는 개체입니다.

1. PDF 양식을 PDF 파일로 저장합니다.

   * 만들기 `System.IO.FileStream` 개체를 사용하여 해당 생성자를 호출하고 XML 파일의 위치를 나타내는 문자열 값을 전달합니다.
   * 의 데이터 내용을 저장하는 바이트 배열을 만듭니다 `BLOB` 반환되는 개체 `exportData` 메서드를 사용합니다. 의 값을 가져와서 바이트 배열을 채웁니다 `BLOB` 개체 `MTOM` 필드.
   * 만들기 `System.IO.BinaryWriter` 생성자를 호출하고 전달하여 개체를 `System.IO.FileStream` 개체.
   * 를 호출하여 바이트 배열의 내용을 XML 파일에 씁니다 `System.IO.BinaryWriter` 개체 `Write` 메서드를 사용하여 바이트 배열을 전달합니다.

**추가 참조**

[단계 요약](importing-exporting-data.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
