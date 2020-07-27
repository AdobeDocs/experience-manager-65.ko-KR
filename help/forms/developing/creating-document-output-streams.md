---
title: 문서 출력 스트림 만들기
seo-title: 문서 출력 스트림 만들기
description: 'null'
seo-description: 'null'
uuid: 80c28efa-35ce-4073-9ca6-2d93bcd67fdd
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: de527d50-991b-4ca3-a8ac-44d5cab988e9
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '18972'
ht-degree: 0%

---


# 문서 출력 스트림 만들기  {#creating-document-output-streams}

**출력 서비스 정보**

출력 서비스를 사용하면 문서를 PDF(PDF/A 문서 포함), PostScript, 프린터 제어 언어(PCL) 및 다음 레이블 포맷으로 출력할 수 있습니다.

* Zebra - ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

출력 서비스를 사용하면 XML 양식 데이터를 양식 디자인과 병합하고 문서를 네트워크 프린터 또는 파일로 출력할 수 있습니다.

두 가지 방법으로 양식 디자인(XDP 파일)을 출력 서비스에 전달할 수 있습니다. 양식 디자인이 포함된 `com.adobe.idp.Document` 인스턴스를 출력 서비스로 전달할 수 있습니다. 또는 양식 디자인의 위치를 지정하는 URI 값을 전달할 수 있습니다. 두 방법 모두 AEM *양식과 프로그래밍*&#x200B;에서 설명합니다.

>[!NOTE]
>
>출력 서비스는 응용 프로그램 개체별 스크립트가 포함된 Acrobat PDF 문서를 지원하지 않습니다. 응용 프로그램 개체별 스크립트가 포함된 PDF 문서 간에 렌더링되지 않습니다.

다음 섹션에서는 URI 값을 사용하여 양식 디자인을 출력 서비스로 전달하는 방법을 보여 줍니다.

* [PDF 문서 작성](creating-document-output-streams.md#creating-pdf-documents)
* [PDF/A 문서 작성](creating-document-output-streams.md#creating-pdf-a-documents)

다음 섹션에서는 인스턴스 내에서 양식 디자인을 전달하는 방법을 `com.adobe.idp.Document` 보여 줍니다.

* [Content Services에 있는 문서 전달(더 이상 사용되지 않음)](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [조각을 사용하여 PDF 문서 만들기](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

사용할 기술을 결정할 때 고려해야 할 사항은 다른 AEM Forms 서비스에서 양식 디자인을 받은 다음 인스턴스 내에 전달하면 `com.adobe.idp.Document` 됩니다. 문서를 출력 서비스에 *전달* 및 조각을 사용하여 PDF 문서 *만들기* 섹션은 모두 다른 AEM Forms 서비스에서 양식 디자인을 가져오는 방법을 보여줍니다. 첫 번째 섹션은 컨텐츠 서비스에서 양식 디자인을 검색합니다(더 이상 사용되지 않음). 두 번째 섹션은 어셈블러 서비스에서 양식 디자인을 검색합니다.

파일 시스템과 같은 고정된 위치에서 양식 디자인을 가져오는 경우 두 가지 방법을 사용할 수 있습니다. 즉, XDP 파일에 URI 값을 지정하거나 인스턴스를 사용할 수 `com.adobe.idp.Document` 있습니다.

PDF 문서를 만들 때 양식 디자인의 위치를 지정하는 URI 값을 전달하려면 이 방법을 `generatePDFOutput` 사용합니다. 마찬가지로 PDF 문서를 만들 때 `com.adobe.idp.Document` 인스턴스를 출력 서비스로 전달하려면 이 방법을 `generatePDFOutput2` 사용합니다.

출력 스트림을 네트워크 프린터로 전송할 때 두 가지 방법을 사용할 수도 있습니다. 양식 디자인이 포함된 인스턴스를 전달하여 출력 스트림을 프린터로 `com.adobe.idp.Document` 전송하려면 `sendToPrinter2`메서드를 사용합니다. URI 값을 전달하여 출력 스트림을 프린터로 보내려면 `sendToPrinter`메서드를 사용합니다. 프린터로 *인쇄 스트림* 전송 섹션에서는 `sendToPrinter` 방법을 사용합니다.

출력 서비스를 사용하여 이러한 작업을 수행할 수 있습니다.

* [PDF 문서 작성](creating-document-output-streams.md#creating-pdf-documents)
* [PDF/A 문서 작성](creating-document-output-streams.md#creating-pdf-a-documents)
* [Content Services에 있는 문서 전달(더 이상 사용되지 않음)](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [조각을 사용하여 PDF 문서 만들기](creating-document-output-streams.md#creating-pdf-documents-using-fragments)
* [파일로 인쇄](creating-document-output-streams.md#printing-to-files)
* [인쇄업체에 인쇄 스트림 전송](creating-document-output-streams.md#sending-print-streams-to-printers)
* [여러 출력 파일 만들기](creating-document-output-streams.md#creating-multiple-output-files)
* [검색 규칙 만들기](creating-document-output-streams.md#creating-search-rules)
* [PDF 문서 병합](creating-document-output-streams.md#flattening-pdf-documents)

>[!NOTE]
>
>출력 서비스에 대한 자세한 내용은 AEM Forms에 대한 [서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

## PDF 문서 작성 {#creating-pdf-documents}

출력 서비스를 사용하여 사용자가 제공하는 양식 디자인 및 XML 양식 데이터를 기반으로 하는 PDF 문서를 만들 수 있습니다. 출력 서비스에서 만든 PDF 문서는 대화형 PDF 문서가 아닙니다. 사용자는 양식 데이터를 입력하거나 수정할 수 없습니다.

장기 보관을 위한 PDF 문서를 만들려면 PDF/A 문서를 만드는 것이 좋습니다. (PDF/ [A 문서 만들기를 참조하십시오](creating-document-output-streams.md#creating-pdf-a-documents).)

사용자가 데이터를 입력할 수 있는 대화형 PDF 양식을 만들려면 Forms 서비스를 사용하십시오. (대화형 [PDF forms 렌더링을 참조하십시오](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms).)

>[!NOTE]
>
>출력 서비스에 대한 자세한 내용은 AEM Forms에 대한 [서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary-of-steps}

PDF 문서를 만들려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. 출력 클라이언트 개체를 만듭니다.
1. XML 데이터 소스를 참조합니다.
1. PDF 런타임 옵션을 설정합니다.
1. 렌더링 런타임 옵션을 설정합니다.
1. PDF 문서를 생성합니다.
1. 작업 결과를 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

다음 JAR 파일을 프로젝트의 클래스 경로에 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(AEM Forms이 JBoss에 배포된 경우 필요)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필수)

AEM Forms이 JBoss가 아닌 지원되는 J2EE 응용 프로그램 서버에 배포된 경우 adobe-utilities.jar 및 jbossall-client.jar 파일을 AEM Forms이 배포된 J2EE 응용 프로그램 서버에 고유한 JAR 파일로 대체해야 합니다.

**출력 클라이언트 개체 만들기**

출력 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 출력 서비스 클라이언트 개체를 만들어야 합니다. Java API를 사용하는 경우 `OutputClient` 개체를 만듭니다. 출력 웹 서비스 API를 사용하는 경우 `OutputServiceService` 개체를 만듭니다.

**XML 데이터 소스 참조**

데이터를 양식 디자인과 병합하려면 데이터가 포함된 XML 데이터 소스를 참조해야 합니다. 데이터로 채울 모든 양식 필드에 대해 XML 요소가 있어야 합니다. XML 요소 이름은 필드 이름과 일치해야 합니다. XML 요소는 양식 필드에 해당되지 않거나 XML 요소 이름이 필드 이름과 일치하지 않는 경우 무시됩니다. 모든 XML 요소가 지정된 경우 XML 요소가 표시되는 순서와 일치할 필요는 없습니다.

다음의 대출 신청 양식을 고려하십시오.

![cp_cp_loanformdata](assets/cp_cp_loanformdata.png)

이 양식 디자인에 데이터를 병합하려면 양식에 해당하는 XML 데이터 소스를 만들어야 합니다. 다음 XML은 예제 모기지 애플리케이션 양식에 해당하는 XDP XML 데이터 소스를 나타냅니다.

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

**PDF 런타임 옵션 설정**

PDF 문서를 만들 때 파일 URI 옵션을 설정합니다. 이 옵션은 출력 서비스가 생성하는 PDF 파일의 이름과 위치를 지정합니다.

>[!NOTE]
>
>파일 URI 런타임 옵션을 설정하는 대신 출력 서비스에서 반환된 복잡한 데이터 유형에서 프로그래밍 방식으로 PDF 문서를 검색할 수 있습니다. 그러나 파일 URI 런타임 옵션을 설정하면 프로그래밍 방식으로 PDF 문서를 검색하는 응용 프로그램 로직을 만들 필요가 없습니다.

**렌더링 런타임 옵션 설정**

PDF 문서를 만들 때 렌더링 런타임 옵션을 설정할 수 있습니다. 이러한 옵션은 필요하지 않지만(필요한 PDF 런타임 옵션과 달리) 출력 서비스의 성능을 향상시키는 등의 작업을 수행할 수 있습니다. 예를 들어 출력 서비스가 사용하는 양식 디자인을 캐시하여 성능을 향상시킬 수 있습니다.

태그가 지정된 Acrobat 양식을 입력으로 사용하는 경우 출력 서비스 Java 또는 웹 서비스 API를 사용하여 태그 지정된 설정을 끌 수 없습니다. 프로그래밍 방식으로 이 옵션을 로 설정하려고 하면 결과 PDF 문서 `false`에 태그가 지정됩니다.

>[!NOTE]
>
>렌더링 런타임 옵션을 지정하지 않으면 기본값이 사용됩니다. 런타임 옵션 렌더링에 대한 자세한 내용은 `RenderOptionsSpec` 클래스 참조를 참조하십시오. (AEM Forms [API 참조 참조 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)).

**PDF 문서 생성**

양식 데이터가 포함된 유효한 XML 데이터 소스를 참조하고 런타임 옵션을 설정한 후 출력 서비스를 호출하여 PDF 문서를 생성합니다.

PDF 문서를 생성할 때 출력 서비스에서 PDF 문서를 만드는 데 필요한 URI 값을 지정합니다. 양식 디자인은 서버 파일 시스템과 같은 위치 또는 AEM Forms 응용 프로그램의 일부로 저장할 수 있습니다. 양식 애플리케이션의 일부로 존재하는 양식 디자인(또는 이미지 파일과 같은 기타 리소스)은 컨텐츠 루트 URI 값을 사용하여 참조할 수 있습니다 `repository:///`. 예를 들어 Applications/FormsApplication이라는 Forms 응용 프로그램 내에 *있는 Loan.xdp* 라는 이름의 다음 양식 디자인을 *생각해 보십시오*.

![cp_formrepository](assets/cp_cp_formrepository.png)

이전 그림에서 표시된 Loan.xdp 파일에 액세스하려면 개체 `repository:///Applications/FormsApplication/1.0/FormsFolder/` 의 메서드에 전달된 세 번째 매개 변수로 `OutputClient` 지정합니다 `generatePDFOutput` . 양식 이름(*Loan.xdp*)을 `OutputClient` 개체의 `generatePDFOutput` 메서드에 전달된 두 번째 매개 변수로 지정합니다.

XDP 파일에 이미지(또는 조각 등 기타 리소스)가 포함되어 있는 경우 리소스를 XDP 파일과 동일한 애플리케이션 폴더에 넣습니다. AEM Forms은 컨텐츠 루트 URI를 기본 경로로 사용하여 이미지에 대한 참조를 확인합니다. 예를 들어 Loan.xdp 파일에 이미지가 포함되어 있는 경우 이미지를 원래 위치에 배치해야 합니다 `Applications/FormsApplication/1.0/FormsFolder/`.

>[!NOTE]
>
>개체의 `OutputClient` 또는 `generatePDFOutput` `generatePrintedOutput` 메서드를 호출할 때 Forms 응용 프로그램 URI를 참조할 수 있습니다.

>[!NOTE]
>
>양식 응용 프로그램에 있는 XDP를 참조하여 PDF 문서를 만드는 전체 빠른 시작을 보려면 [빠른 시작(EJB 모드)을 참조하십시오. Java API를 사용하여 응용 프로그램 XDP 파일을 기반으로 PDF 문서 만들기](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api)

**작업 결과 검색**

출력 서비스는 작업을 수행한 후 작업 성공 여부를 지정하는 상태 XML 데이터와 같은 다양한 데이터 항목을 반환합니다.

**참고 항목**

[Java API를 사용하여 PDF 문서 만들기](creating-document-output-streams.md#create-a-pdf-document-using-the-java-api)

[웹 서비스 API를 사용하여 PDF 문서 만들기](creating-document-output-streams.md#create-a-pdf-document-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[출력 서비스 API 빠른 시작](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java API를 사용하여 PDF 문서 만들기 {#create-a-pdf-document-using-the-java-api}

출력 API(Java)를 사용하여 PDF 문서를 만듭니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-output-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. 출력 클라이언트 개체를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 개체를 `OutputClient` 만들고 개체를 `ServiceClientFactory` 전달합니다.

1. XML 데이터 소스를 참조합니다.

   * 생성자를 사용하여 PDF 문서를 채우는 데 사용되는 XML 데이터 소스를 나타내는 `java.io.FileInputStream` 객체를 만들고 XML 파일의 위치를 지정하는 문자열 값을 전달합니다.
   * 생성자를 사용하여 `com.adobe.idp.Document` 개체를 만듭니다. 개체를 `java.io.FileInputStream` 전달합니다.

1. PDF 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 `PDFOutputOptionsSpec` 개체를 만듭니다.
   * 개체의 메서드를 호출하여 파일 URI 옵션 `PDFOutputOptionsSpec` 을 `setFileURI` 설정합니다. 출력 서비스가 생성하는 PDF 파일의 위치를 지정하는 문자열 값을 전달합니다. 파일 URI 옵션은 클라이언트 컴퓨터가 아닌 AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버를 기준으로 합니다.

1. 렌더링 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 `RenderOptionsSpec` 개체를 만듭니다.
   * 개체의 호출과 전달을 통해 출력 서비스의 성능을 개선하기 위해 양식 디자인 `RenderOptionsSpec` 을 캐시합니다 `setCacheEnabled` `true`.

   >[!NOTE]
   >
   >입력 문서가 Acrobat 양식(Acrobat에서 만든 양식) 또는 서명 또는 인증된 XFA 문서인 경우 `RenderOptionsSpec` 개체의 `setPdfVersion` 방법을 사용하여 PDF 문서 버전을 설정할 수 없습니다. 출력 PDF 문서는 원본 PDF 버전을 유지합니다. 마찬가지로, 입력 문서가 Acrobat 양식 또는 서명된 XFA 문서인 경우 `RenderOptionsSpec` 개체의 `setTaggedPDF` 방법을 호출하여 태그 지정된 Adobe PDF 옵션을 설정할 수 없습니다.

   >[!NOTE]
   >
   >입력 PDF 문서가 인증되거나 디지털 서명된 경우 `RenderOptionsSpec` 개체의 `setLinearizedPDF` 방법을 사용하여 선형화된 PDF 옵션을 설정할 수 없습니다. (PDF 문서 [디지털 서명 참조](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*)*

1. PDF 문서를 생성합니다.

   개체의 방법을 호출하고 다음 값을 전달하여 `OutputClient` PDF 문서를 `generatePDFOutput` 만듭니다.

   * 열거형 `TransformationFormat` 값입니다. PDF 문서를 생성하려면 을 지정합니다 `TransformationFormat.PDF`.
   * 양식 디자인의 이름을 지정하는 문자열 값입니다.
   * 양식 디자인이 있는 컨텐츠 루트를 지정하는 문자열 값입니다.
   * PDF 런타임 옵션이 포함된 `PDFOutputOptionsSpec` 개체
   * 렌더링 런타임 옵션이 포함된 `RenderOptionsSpec` 개체입니다.
   * 양식 디자인과 병합할 데이터가 들어 있는 XML 데이터 소스를 포함하는 `com.adobe.idp.Document` 개체입니다.

   이 `generatePDFOutput` 메서드는 작업 결과를 포함하는 `OutputResult` 개체를 반환합니다.

   >[!NOTE]
   >
   >방법을 호출하여 PDF 문서를 생성하는 경우 `generatePDFOutput` 서명되거나 인증된 XFA PDF 양식과 데이터를 병합할 수 없습니다. (문서 [디지털 서명 및 인증을 참조하십시오](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*.)*

   >[!NOTE]
   >
   >개체의 `OutputResult` 메서드가 `getRecordLevelMetaDataList` 반환됩니다 `null`*.*

   >[!NOTE]
   >
   >또한 개체의 방법을 호출하여 PDF 문서를 만들 수도 `OutputClient` `generatePDFOutput2` 있습니다. (컨텐츠 서비스 [에 있는 문서 전달(더 이상 사용되지 않음)을 출력 서비스로 참조하십시오](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*.)*

1. 작업 결과를 검색합니다.

   * 객체의 메서드를 호출하여 작업 상태를 나타내는 `com.adobe.idp.Document` 객체를 `generatePDFOutput` `OutputResult` `getStatusDoc` 검색합니다. 이 메서드는 작업이 성공했는지 여부를 지정하는 상태 XML 데이터를 반환합니다.
   * 작업 결과가 포함된 `java.io.File` 개체를 만듭니다. 파일 이름 확장자가 .xml인지 확인합니다.
   * 객체의 메서드를 호출하여 `com.adobe.idp.Document` 객체의 내용을 파일에 복사합니다(메서드에서 반환된 `copyToFile` 객체를 `com.adobe.idp.Document` `com.adobe.idp.Document` `getStatusDoc` 사용해야 함).

   출력 서비스는 PDF 문서를 객체의 메서드에 전달된 인수로 지정한 위치에 쓰지만, `PDFOutputOptionsSpec` 개체의 `setFileURI` `OutputResult` `getGeneratedDoc` 메서드를 호출하여 프로그래밍 방식으로 PDF/A 문서를 검색할 수 있습니다.

**참고 항목**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[빠른 시작(EJB 모드): Java API를 사용하여 PDF 문서 만들기](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[빠른 시작(SOAP 모드): Java API를 사용하여 PDF 문서 만들기](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 PDF 문서 만들기 {#create-a-pdf-document-using-the-web-service-api}

출력 API(웹 서비스)를 사용하여 PDF 문서를 만듭니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Forms `localhost` 를 호스팅하는 서버의 IP 주소로 대체합니다.

1. 출력 클라이언트 개체를 만듭니다.

   * 기본 생성자를 사용하여 `OutputServiceClient` 개체를 만듭니다.
   * 생성자를 사용하여 `OutputServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 속성을 사용할 필요는 `lc_version` 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다. 하지만 MTOM `?blob=mtom` 을 사용하도록 지정합니다.
   * 필드의 값을 `System.ServiceModel.BasicHttpBinding` 가져와 개체를 `OutputServiceClient.Endpoint.Binding` 만듭니다. 반환 값을 다음으로 캐스팅합니다 `BasicHttpBinding`.
   * 개체 `System.ServiceModel.BasicHttpBinding` 필드를 (으)로 `MessageEncoding` 설정합니다 `WSMessageEncoding.Mtom`. 이 값을 사용하면 MTOM이 사용됩니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM 양식 사용자 이름을 지정합니다 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 해당 암호 값을 필드에 지정합니다 `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 필드에 상수 값 `HttpClientCredentialType.Basic` 을 지정합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 필드에 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly` 을 지정합니다 `BasicHttpBindingSecurity.Security.Mode`.

1. XML 데이터 소스를 참조합니다.

   * 생성자를 사용하여 `BLOB` 개체를 만듭니다. 이 `BLOB` 개체는 PDF 문서와 병합할 XML 데이터를 저장하는 데 사용됩니다.
   * 생성자를 호출하고 양식 데이터가 포함된 XML 파일의 파일 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * 개체의 내용을 저장하는 바이트 배열을 `System.IO.FileStream` 만듭니다. 개체의 속성을 가져와 바이트 배열의 크기를 결정할 수 `System.IO.FileStream` `Length` 있습니다.
   * 개체의 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열 `System.IO.FileStream` `Read` 을 스트림 데이터로 채웁니다.
   * 바이트 배열의 내용으로 해당 `BLOB` `MTOM` 필드를 할당하여 개체를 채웁니다.

1. PDF 런타임 옵션 설정

   * 생성자를 사용하여 `PDFOutputOptionsSpec` 개체를 만듭니다.
   * 출력 서비스가 생성하는 PDF 파일의 위치를 개체의 데이터 멤버에 지정하는 문자열 값을 할당하여 파일 URI 옵션 `PDFOutputOptionsSpec` 을 `fileURI` 설정합니다. 파일 URI 옵션은 클라이언트 컴퓨터가 아닌 AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버를 기준으로 합니다.

1. 렌더링 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 `RenderOptionsSpec` 개체를 만듭니다.
   * 개체의 데이터 멤버에 값을 할당하여 출력 서비스의 성능 `true` 을 개선하기 위해 양식 디자인을 `RenderOptionsSpec` 캐시합니다 `cacheEnabled` .

   >[!NOTE]
   >
   >입력 문서가 Acrobat 양식(Acrobat에서 만든 양식) 또는 서명 또는 인증된 XFA 문서인 경우 `RenderOptionsSpec` 개체의 `setPdfVersion` 방법을 사용하여 PDF 문서 버전을 설정할 수 없습니다. 출력 PDF 문서는 원본 PDF 버전을 유지합니다. 마찬가지로 입력 문서가 Acrobat 양식 또는 서명된 XFA 문서 또는 인증된 XFA 문서인 경우 `RenderOptionsSpec` 개체의 `setTaggedPDF`* 방법을 호출하여 태그 지정된 Adobe PDF 옵션을 설정할 수 없습니다.*

   >[!NOTE]
   >
   >입력 PDF 문서가 인증되거나 디지털 서명된 경우 `RenderOptionsSpec` 개체의 `linearizedPDF` 구성원을 사용하여 선형화된 PDF 옵션을 설정할 수 없습니다. (PDF 문서 [디지털 서명 참조](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*)*

1. PDF 문서를 생성합니다.

   개체의 `OutputServiceService` `generatePDFOutput`메서드를 호출하고 다음 값을 전달하여 PDF 문서를 만듭니다.

   * 열거형 `TransformationFormat` 값입니다. PDF 문서를 생성하려면 을 지정합니다 `TransformationFormat.PDF`.
   * 양식 디자인의 이름을 지정하는 문자열 값입니다.
   * 양식 디자인이 있는 컨텐츠 루트를 지정하는 문자열 값입니다.
   * PDF 런타임 옵션이 포함된 `PDFOutputOptionsSpec` 개체
   * 렌더링 런타임 옵션이 포함된 `RenderOptionsSpec` 개체입니다.
   * 양식 디자인과 병합할 데이터가 들어 있는 XML 데이터 소스를 포함하는 `BLOB` 개체입니다.
   * 메서드로 채워지는 `BLOB` `generatePDFOutput` 개체입니다. 이 `generatePDFOutput` 메서드는 문서를 설명하는 생성된 메타데이터로 이 개체를 채웁니다. 이 매개 변수 값은 웹 서비스 호출에만 필요합니다.
   * 메서드로 채워지는 `BLOB` `generatePDFOutput` 개체입니다. 이 `generatePDFOutput` 개체는 결과 데이터로 채워집니다. 이 매개 변수 값은 웹 서비스 호출에만 필요합니다.
   * 작업 결과를 포함하는 `OutputResult` 개체입니다. 이 매개 변수 값은 웹 서비스 호출에만 필요합니다.

   >[!NOTE]
   >
   >방법을 호출하여 PDF 문서를 생성하는 경우 `generatePDFOutput` 서명되거나 인증된 XFA PDF 양식과 데이터를 병합할 수 없습니다. (문서 [디지털 서명 및 인증을 참조하십시오](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*.)*

   >[!NOTE]
   >
   >또한 개체의 방법을 호출하여 PDF 문서를 만들 수도 `OutputClient` `generatePDFOutput2` 있습니다. (컨텐츠 서비스 [에 있는 문서 전달(더 이상 사용되지 않음)을 출력 서비스로 참조하십시오](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*.)*

1. 작업 결과를 검색합니다.

   * 생성자를 호출하고 결과 데이터가 포함된 XML 파일 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다. 파일 이름 확장자가 .xml인지 확인합니다.
   * 개체의 메서드(8번째 매개 변수)로 결과 데이터로 채워진 `BLOB` 개체의 데이터 콘텐츠를 저장하는 `OutputServiceService` 바이트 `generatePDFOutput` 배열을 만듭니다. 개체 값을 가져와 바이트 배열을 `BLOB` 채웁니다 `MTOM` `field`.
   * 생성자를 호출하고 개체를 전달하여 `System.IO.BinaryWriter` 개체를 `System.IO.FileStream` 만듭니다.
   * 개체의 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열 내용을 XML 파일에 `System.IO.BinaryWriter``Write` 씁니다.

   참고 항목

   [단계 요약](creating-document-output-streams.md#summary-of-steps)

   [MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

   [SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

   >[!NOTE]
   >
   >개체 `OutputServiceService` 의 `generateOutput` 메서드는 더 이상 사용되지 않습니다.

## PDF/A 문서 작성 {#creating-pdf-a-documents}

출력 서비스를 사용하여 PDF/A 문서를 만들 수 있습니다. PDF/A는 문서 컨텐츠를 장기 보존하기 위한 보관 포맷이므로 모든 글꼴이 임베드되고 파일이 압축되지 않습니다. 따라서 PDF/A 문서는 표준 PDF 문서보다 일반적으로 더 큽니다. 또한 PDF/A 문서에는 오디오 및 비디오 컨텐츠가 포함되어 있지 않습니다. 다른 출력 서비스 작업과 마찬가지로 양식 디자인과 병합하는 양식 디자인 및 데이터를 제공하여 PDF/A 문서를 만듭니다.

PDF/A-1 규격은 a 및 b의 두 가지 적합성 수준으로 구성되어 있습니다. 두 가지 간의 주요 차이는 논리 구조(액세서빌러티) 지원에 관한 것으로, 적합성 수준 b에는 필요하지 않습니다. 적합성 수준에 관계없이 PDF/A-1은 생성된 PDF/A 문서에 모든 글꼴이 임베드되어 있음을 나타냅니다.

PDF/A는 PDF 문서 보관을 위한 표준이지만 표준 PDF 문서가 회사의 요구 사항에 부합되는 경우 보관을 위해 PDF/A를 반드시 사용해야 하는 것은 아닙니다. PDF/A 표준은 문서 보존 요구 사항을 충족하고 장기간 저장할 수 있는 PDF 파일을 작성하는 데 사용됩니다. 예를 들어 URL은 시간이 지남에 따라 URL이 잘못될 수 있으므로 PDF/A에 URL을 포함할 수 없습니다.

조직은 자신의 요구 사항, 문서 보관 기간, 파일 크기 고려 사항 등을 평가하고 자신의 아카이빙 전략을 결정해야 합니다. DocConverter 서비스를 사용하여 PDF 문서가 PDF/A 규격인지 프로그래밍 방식으로 확인할 수 있습니다. 자세한 내용은 [프로그래밍 방식으로 PDF/A 규정 준수 여부 결정을 참조하십시오](/help/forms/developing/pdf-a-documents.md#programmatically-determining-pdf-a-compliancy).

PDF/A 문서는 양식 디자인에 지정된 글꼴을 사용해야 하며 글꼴을 대체할 수 없습니다. 따라서 PDF 문서 내에 있는 글꼴을 호스트 운영 체제(OS)에서 사용할 수 없는 경우 예외가 발생합니다.

Acrobat에서 PDF/A 문서를 열면 다음 그림과 같이 문서가 PDF/A 문서임을 확인하는 메시지가 표시됩니다.

![cp_cp_pdfamessage](assets/cp_cp_pdfamessage.png)

>[!NOTE]
>
>AIIM 웹 사이트에는 https://www.aiim.org/documents/standards/19005-1_FAQ.pdf에서 액세스할 수 있는 PDF/A FAQ 섹션이 [있습니다](https://www.aiim.org/documents/standards/19005-1_FAQ.pdf).

>[!NOTE]
>
>출력 서비스에 대한 자세한 내용은 AEM Forms에 대한 [서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-1}

PDF/A 문서를 만들려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. 출력 클라이언트 개체를 만듭니다.
1. XML 데이터 소스를 참조합니다.
1. PDF/A 런타임 옵션을 설정합니다.
1. 렌더링 런타임 옵션을 설정합니다.
1. PDF/A 문서를 생성합니다.
1. 작업 결과를 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 사용자 정의 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(AEM Forms이 JBoss에 배포된 경우 필요)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필수)

AEM Forms이 JBoss가 아닌 지원되는 J2EE 응용 프로그램 서버에 배포된 경우 adobe-utilities.jar 및 jbossall-client.jar 파일을 AEM Forms이 배포된 J2EE 응용 프로그램 서버에 고유한 JAR 파일로 대체해야 합니다.

**출력 클라이언트 개체 만들기**

출력 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 출력 서비스 클라이언트 개체를 만들어야 합니다. Java API를 사용하는 경우 `OutputClient` 개체를 만듭니다. 출력 웹 서비스 API를 사용하는 경우 `OutputServiceService` 개체를 만듭니다.

**XML 데이터 소스 참조**

데이터를 양식 디자인과 병합하려면 데이터가 포함된 XML 데이터 소스를 참조해야 합니다. 데이터로 채울 모든 양식 필드에 대해 XML 요소가 있어야 합니다. XML 요소 이름은 필드 이름과 일치해야 합니다. XML 요소는 양식 필드에 해당되지 않거나 XML 요소 이름이 필드 이름과 일치하지 않는 경우 무시됩니다. 모든 XML 요소가 지정된 경우 XML 요소가 표시되는 순서와 일치할 필요는 없습니다.

**PDF/A 런타임 옵션 설정**

PDF/A 문서를 만들 때 파일 URI 옵션을 설정할 수 있습니다. URI는 AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버에 상대적입니다. 즉, C:\Adobe을 설정하면 파일이 클라이언트 컴퓨터가 아닌 서버의 폴더에 기록됩니다. URI는 출력 서비스가 생성하는 PDF/A 파일의 이름과 위치를 지정합니다.

**렌더링 런타임 옵션 설정**

PDF/A 문서를 만들 때 렌더링 런타임 옵션을 설정할 수 있습니다. 설정할 수 있는 두 가지 PDF/A 관련 옵션은 `PDFAConformance` 및 `PDFARevisionNumber` 값입니다. 이 `PDFAConformance` 값은 PDF 문서가 장기 전자 문서의 보존 기간을 지정하는 요구 사항을 준수하는 방식을 나타냅니다. 이 옵션에 유효한 값은 `A` 및 `B`입니다. 레벨 a 및 b 적합성 정보에 대한 자세한 내용은 *ISO 19005-1 문서 관리라는 PDF/A-1 ISO 사양을 참조하십시오*.

이 `PDFARevisionNumber` 값은 PDF/A 문서의 개정 번호를 나타냅니다. PDF/A 문서의 개정 번호에 대한 자세한 내용은 *ISO 19005-1 문서 관리라는 PDF/A-1 ISO 사양을 참조하십시오*.

>[!NOTE]
>
>PDF/A 1A 문서를 만들 때는 태그가 지정된 Adobe PDF 옵션 `false` 을 설정할 수 없습니다. PDF/A 1A는 항상 태그가 지정된 PDF 문서입니다. 또한 PDF/A 1B 문서를 만들 때는 태그가 지정된 Adobe PDF 옵션 `true` 을 설정할 수 없습니다. PDF/A 1B는 항상 태그가 없는 PDF 문서입니다.

**PDF/A 문서 생성**

양식 데이터가 포함된 유효한 XML 데이터 소스를 참조하고 런타임 옵션을 설정한 후 출력 서비스를 호출하여 PDF/A 문서를 생성할 수 있습니다.

**작업 결과 검색**

출력 서비스가 작업을 수행한 후 작업이 성공했는지 여부를 지정하는 XML 데이터와 같은 다양한 데이터 항목을 반환합니다.

**참고 항목**

[Java API를 사용하여 PDF/A 문서 만들기](creating-document-output-streams.md#create-a-pdf-a-document-using-the-java-api)

[웹 서비스 API를 사용하여 PDF/A 문서 만들기](creating-document-output-streams.md#create-a-pdf-a-document-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[출력 서비스 API 빠른 시작](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java API를 사용하여 PDF/A 문서 만들기 {#create-a-pdf-a-document-using-the-java-api}

출력 API(Java)를 사용하여 PDF/A 문서를 만듭니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-output-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. 출력 클라이언트 개체를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 개체를 `OutputClient` 만들고 개체를 `ServiceClientFactory` 전달합니다.

1. XML 데이터 소스를 참조합니다.

   * 생성자를 사용하여 PDF/A 문서를 채우는 데 사용되는 XML 데이터 소스를 나타내는 `java.io.FileInputStream` 객체를 만들고 XML 파일의 위치를 지정하는 문자열 값을 전달합니다.
   * 생성자를 사용하여 개체를 `com.adobe.idp.Document` 만들고 개체를 `java.io.FileInputStream` 전달합니다.

1. PDF/A 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 `PDFOutputOptionsSpec` 개체를 만듭니다.
   * 개체의 메서드를 호출하여 파일 URI 옵션 `PDFOutputOptionsSpec` 을 `setFileURI` 설정합니다. 출력 서비스가 생성하는 PDF 파일의 위치를 지정하는 문자열 값을 전달합니다. 파일 URI 옵션은 클라이언트 컴퓨터가 아닌 AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버를 기준으로 합니다.

1. 렌더링 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 `RenderOptionsSpec` 개체를 만듭니다.
   * 객체의 메서드를 호출하고 적합성 수준을 지정하는 `PDFAConformance` `RenderOptionsSpec` `setPDFAConformance` `PDFAConformance` 열거형 값을 전달하여 값을 설정합니다. 예를 들어 적합성 레벨 A를 지정하려면 pass `PDFAConformance.A`를 수행합니다.
   * 개체의 `PDFARevisionNumber` 메서드를 호출하고 전달하여 `RenderOptionsSpec` 값을 `setPDFARevisionNumber` 설정합니다 `PDFARevisionNumber.Revision_1`.

   >[!NOTE]
   >
   >PDF/A 문서의 PDF 버전은 `RenderOptionsSpec` 개체 `setPdfVersion`*방식에 대해 지정한 값과 관계없이 1.4입니다.*

1. PDF/A 문서를 생성합니다.

   개체의 메서드를 호출하고 다음 값을 전달하여 PDF/ `OutputClient` A 문서 `generatePDFOutput` 를 만듭니다.

   * 열거형 `TransformationFormat` 값입니다. PDF/A 문서를 생성하려면 을 지정합니다 `TransformationFormat.PDFA`.
   * 양식 디자인의 이름을 지정하는 문자열 값입니다.
   * 양식 디자인이 있는 컨텐츠 루트를 지정하는 문자열 값입니다.
   * PDF 런타임 옵션이 포함된 `PDFOutputOptionsSpec` 개체
   * 렌더링 런타임 옵션이 포함된 `RenderOptionsSpec` 개체입니다.
   * 양식 디자인과 병합할 데이터가 포함된 XML 데이터 소스가 포함된 `com.adobe.idp.Document` 객체입니다.

   이 `generatePDFOutput` 메서드는 작업 결과를 포함하는 `OutputResult` 개체를 반환합니다.

   >[!NOTE]
   >
   >개체의 `OutputResult` 메서드가 `getRecordLevelMetaDataList` 반환됩니다 `null`.

   >[!NOTE]
   >
   >또한 개체의 `OutputClient` `generatePDFOutput`2 메서드를 호출하여 PDF/A 문서를 만들 수도 있습니다. (컨텐츠 서비스 [에 있는 문서 전달(더 이상 사용되지 않음)을 출력 서비스로 참조하십시오](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service).)

1. 작업 결과를 검색합니다.

   * 개체의 메서드를 호출하여 메서드 `com.adobe.idp.Document` 의 상태를 나타내는 `generatePDFOutput` 개체를 `OutputResult` `getStatusDoc` 만듭니다.
   * 작업 결과를 포함할 `java.io.File` 개체를 만듭니다. 파일 이름 확장자가 .xml인지 확인합니다.
   * 객체의 메서드를 호출하여 `com.adobe.idp.Document` 객체의 내용을 파일에 복사합니다(메서드에서 반환된 `copyToFile` 객체를 `com.adobe.idp.Document` `com.adobe.idp.Document` `getStatusDoc` 사용해야 함).

   >[!NOTE]
   >
   >출력 서비스는 PDF/A 문서를 개체의 메서드에 전달된 인수로 지정한 위치에 쓰지만, `PDFOutputOptionsSpec` 개체의 `setFileURI` `OutputResult` `getGeneratedDoc` 메서드를 호출하여 프로그래밍 방식으로 PDF/A 문서를 검색할 수 있습니다.

**참고 항목**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[빠른 시작(SOAP 모드): Java API를 사용하여 PDF/A 문서 만들기](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-a-document-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성을 설정합니다](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### 웹 서비스 API를 사용하여 PDF/A 문서 만들기 {#create-a-pdf-a-document-using-the-web-service-api}

출력 API(웹 서비스)를 사용하여 PDF/A 문서를 만듭니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Forms `localhost` 를 호스팅하는 서버의 IP 주소로 대체합니다.

1. 출력 클라이언트 개체를 만듭니다.

   * 기본 생성자를 사용하여 `OutputServiceClient` 개체를 만듭니다.
   * 생성자를 사용하여 `OutputServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 속성을 사용할 필요는 `lc_version` 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다. 하지만 MTOM `?blob=mtom` 을 사용하도록 지정합니다.
   * 필드의 값을 `System.ServiceModel.BasicHttpBinding` 가져와 개체를 `OutputServiceClient.Endpoint.Binding` 만듭니다. 반환 값을 다음으로 캐스팅합니다 `BasicHttpBinding`.
   * 개체 `System.ServiceModel.BasicHttpBinding` 필드를 (으)로 `MessageEncoding` 설정합니다 `WSMessageEncoding.Mtom`. 이 값을 사용하면 MTOM이 사용됩니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM 양식 사용자 이름을 지정합니다 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 해당 암호 값을 필드에 지정합니다 `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 필드에 상수 값 `HttpClientCredentialType.Basic` 을 지정합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 필드에 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly` 을 지정합니다 `BasicHttpBindingSecurity.Security.Mode`.

1. XML 데이터 소스를 참조합니다.

   * 생성자를 사용하여 `BLOB` 개체를 만듭니다. 이 `BLOB` 개체는 PDF/A 문서와 병합할 데이터를 저장하는 데 사용됩니다.
   * 생성자를 호출하고 암호화할 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * 개체의 내용을 저장하는 바이트 배열을 `System.IO.FileStream` 만듭니다. 개체의 속성을 가져와 바이트 배열의 크기를 결정할 수 `System.IO.FileStream` `Length` 있습니다.
   * 개체의 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열 `System.IO.FileStream` `Read` 을 스트림 데이터로 채웁니다.
   * 바이트 배열 컨텐츠로 해당 `BLOB` `MTOM` 필드를 할당하여 개체를 채웁니다.

1. PDF/A 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 `PDFOutputOptionsSpec` 개체를 만듭니다.
   * 출력 서비스가 생성하는 PDF 파일의 위치를 개체의 데이터 멤버에 지정하는 문자열 값을 할당하여 파일 URI 옵션 `PDFOutputOptionsSpec` 을 `fileURI` 설정합니다. 파일 URI 옵션은 클라이언트 컴퓨터가 아닌 AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버를 기준으로 합니다

1. 렌더링 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 `RenderOptionsSpec` 개체를 만듭니다.
   * 개체 `PDFAConformance` 의 데이터 멤버에 `PDFAConformance` 열거형 값을 할당하여 `RenderOptionsSpec` 값을 `PDFAConformance` 설정합니다. 예를 들어 적합성 수준 A를 지정하려면 이 데이터 멤버 `PDFAConformance.A` 에 할당합니다.
   * 개체 `PDFARevisionNumber` 의 데이터 멤버에 `PDFARevisionNumber` 열거형 값을 할당하여 `RenderOptionsSpec` 값을 `PDFARevisionNumber` 설정합니다. 이 데이터 멤버 `PDFARevisionNumber.Revision_1` 에 할당합니다.

   >[!NOTE]
   >
   >PDF/A 문서의 PDF 버전은 지정한 값에 관계없이 1.4입니다.

1. PDF/A 문서를 생성합니다.

   개체의 `OutputServiceService` `generatePDFOutput`메서드를 호출하고 다음 값을 전달하여 PDF 문서를 만듭니다.

   * TransformationFormat 열거형 값. PDF 문서를 생성하려면 을 지정합니다 `TransformationFormat.PDFA`.
   * 양식 디자인의 이름을 지정하는 문자열 값입니다.
   * 양식 디자인이 있는 컨텐츠 루트를 지정하는 문자열 값입니다.
   * PDF 런타임 옵션이 포함된 `PDFOutputOptionsSpec` 개체
   * 렌더링 런타임 옵션이 포함된 `RenderOptionsSpec` 개체입니다.
   * 양식 디자인과 병합할 데이터가 들어 있는 XML 데이터 소스를 포함하는 `BLOB` 개체입니다.
   * 메서드로 채워지는 `BLOB` `generatePDFOutput` 개체입니다. 이 `generatePDFOutput` 메서드는 문서를 설명하는 생성된 메타데이터로 이 개체를 채웁니다. 이 매개 변수 값은 웹 서비스 호출에만 필요합니다.
   * 메서드로 채워지는 `BLOB` `generatePDFOutput` 개체입니다. 이 `generatePDFOutput` 개체는 결과 데이터로 채워집니다. 이 매개 변수 값은 웹 서비스 호출에만 필요합니다.
   * 작업 결과를 포함하는 `OutputResult` 개체입니다. 이 매개 변수 값은 웹 서비스 호출에만 필요합니다.

   >[!NOTE]
   >
   >또한 개체의 `OutputClient` `generatePDFOutput`2 메서드를 호출하여 PDF/A 문서를 만들 수도 있습니다. (컨텐츠 서비스 [에 있는 문서 전달(더 이상 사용되지 않음)을 출력 서비스로 참조하십시오](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service).)

1. 작업 결과를 검색합니다.

   * 생성자를 호출하고 결과 데이터가 포함된 XML 파일 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다. 파일 이름 확장자가 .xml인지 확인합니다.
   * 개체의 메서드(8번째 매개 변수)로 결과 데이터로 채워진 `BLOB` 개체의 데이터 콘텐츠를 저장하는 `OutputServiceService` 바이트 `generatePDFOutput` 배열을 만듭니다. 개체 필드의 값을 가져와 바이트 배열 `BLOB` 을 `MTOM` 채웁니다.
   * 생성자를 호출하고 개체를 전달하여 `System.IO.BinaryWriter` 개체를 `System.IO.FileStream` 만듭니다.
   * 개체의 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열 내용을 XML 파일에 `System.IO.BinaryWriter``Write` 씁니다.

**참고 항목**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Content Services에 있는 문서 전달(더 이상 사용되지 않음) {#passing-documents-located-in-content-services-deprecated-to-the-output-service}

출력 서비스는 일반적으로 XDP 파일로 저장되고 Designer에서 작성된 양식 디자인을 기반으로 하는 비대화형 PDF 양식을 렌더링합니다. 양식 디자인이 포함된 `com.adobe.idp.Document` 개체를 출력 서비스로 전달할 수 있습니다. 그런 다음 출력 서비스는 `com.adobe.idp.Document` 개체에 있는 양식 디자인을 렌더링합니다.

다른 AEM Forms 서비스 작업에서 인스턴스 `com.adobe.idp.Document` 를 반환하면 개체를 출력 서비스에 전달할 수 있는 이점이 `com.adobe.idp.Document` 있습니다. 즉, 다른 서비스 작업에서 `com.adobe.idp.Document` 인스턴스를 가져와 렌더링할 수 있습니다. 예를 들어, 다음 그림과 같이 XDP 파일이 이름이 지정된 컨텐츠 서비스(더 이상 사용되지 않음) 노드 `/Company Home/Form Designs`에 저장되어 있다고 가정합니다.

Content Services에서 Loan.xdp를 프로그래밍 방식으로 검색하고(더 이상 사용되지 않음) XDP 파일을 객체 내의 출력 서비스로 전달할 수 `com.adobe.idp.Document` 있습니다.

>[!NOTE]
>
>양식 서비스에 대한 자세한 내용은 AEM Forms에 대한 [서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-2}

콘텐츠 서비스에서 얻은 문서(더 이상 사용되지 않음)를 출력 서비스로 전달하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일 포함
1. 출력 및 문서 관리 클라이언트 API 객체를 만듭니다.
1. 콘텐츠 서비스에서 양식 디자인을 검색합니다(더 이상 사용되지 않음).
1. 비대화형 PDF 양식을 렌더링합니다.
1. 데이터 스트림으로 작업을 수행합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함하십시오.

**출력 및 문서 관리 클라이언트 API 객체 만들기**

출력 서비스 API 작업을 프로그래밍 방식으로 수행하려면 먼저 출력 클라이언트 API 개체를 만듭니다. 또한 이 워크플로우는 Content Services(더 이상 사용되지 않음)에서 XDP 파일을 검색하므로 Document Management API 개체를 만듭니다.

**콘텐츠 서비스에서 양식 디자인 검색(더 이상 사용되지 않음)**

Java 또는 웹 서비스 API를 사용하여 콘텐츠 서비스에서 XDP 파일을 검색합니다(더 이상 사용되지 않음). XDP 파일은 인스턴스(또는 웹 서비스를 사용하는 경우 `com.adobe.idp.Document` `BLOB` 인스턴스) 내에서 반환됩니다. 그런 다음 인스턴스를 출력 서비스에 `com.adobe.idp.Document` 전달할 수 있습니다.

**비대화형 PDF 양식 렌더링**

비대화형 양식을 렌더링하려면 Content Services(더 이상 사용되지 않음)에서 반환된 `com.adobe.idp.Document` 인스턴스를 출력 서비스로 전달합니다.

>[!NOTE]
>
>and g라는 두 가지 새로운 메서드 `generatePDFOutput2`는 양식 디자인이 포함된 개체를 `eneratePrintedOutput2`수락합니다 `com.adobe.idp.Document` . 또한 인쇄 스트림을 네트워크 프린터로 전송할 때 양식 디자인 `com.adobe.idp.Document`이 들어 있는 텍스트를 출력 서비스로 전달할 수 있습니다.

**양식 데이터 스트림으로 작업 수행**

비대화형 양식을 PDF 파일로 저장할 수 있습니다. 이 양식은 Adobe Reader 또는 Acrobat에서 볼 수 있습니다.

**참고 항목**

[Java API를 사용하여 문서를 출력 서비스로 전달](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-java-api)

[웹 서비스 API를 사용하여 문서를 출력 서비스로 전달](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[출력 서비스 API 빠른 시작](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[조각을 사용하여 PDF 문서 만들기](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

### Java API를 사용하여 문서를 출력 서비스로 전달 {#pass-documents-to-the-output-service-using-the-java-api}

출력 서비스 및 컨텐츠 서비스(더 이상 사용되지 않음) API(Java)를 사용하여 컨텐츠 서비스에서 검색된 문서를 전달합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-output-client.jar 및 adobe-contentservices-client.jar 등의 클라이언트 JAR 파일을 포함합니다.

1. 출력 및 문서 관리 클라이언트 API 객체를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다. 연결 [속성 설정을 참조하십시오](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).
   * 생성자를 사용하여 개체를 `OutputClient` 만들고 개체를 `ServiceClientFactory` 전달합니다.
   * 생성자를 사용하여 개체를 `DocumentManagementServiceClientImpl` 만들고 개체를 `ServiceClientFactory` 전달합니다.

1. 콘텐츠 서비스에서 양식 디자인을 검색합니다(더 이상 사용되지 않음).

   개체의 `DocumentManagementServiceClientImpl` 메서드를 `retrieveContent` 호출하고 다음 값을 전달합니다.

   * 컨텐츠가 추가되는 스토어를 지정하는 문자열 값. 기본 스토어는 입니다 `SpacesStore`. 이 값은 필수 매개 변수입니다.
   * 검색할 컨텐츠의 정규화된 경로를 지정하는 문자열 값(예: `/Company Home/Form Designs/Loan.xdp`). 이 값은 필수 매개 변수입니다.
   * 버전을 지정하는 문자열 값. 이 값은 선택적 매개 변수이며 빈 문자열을 전달할 수 있습니다. 이 경우 최신 버전이 검색됩니다.

   이 `retrieveContent` 메서드는 XDP 파일이 포함된 `CRCResult` 개체를 반환합니다. 객체의 메서드를 호출하여 인스턴스 `com.adobe.idp.Document` 를 `CRCResult` `getDocument` 검색합니다.

1. 비대화형 PDF 양식을 렌더링합니다.

   개체의 `OutputClient` 메서드를 `generatePDFOutput2` 호출하고 다음 값을 전달합니다.

   * 열거형 `TransformationFormat` 값입니다. PDF 문서를 생성하려면 을 지정합니다 `TransformationFormat.PDF`.
   * 이미지와 같은 추가 리소스가 있는 컨텐츠 루트를 지정하는 문자열 값입니다.
   * 양식 디자인을 나타내는 개체( `com.adobe.idp.Document` 개체의 `CRCResult` `getDocument` 메서드에서 반환된 인스턴스 사용)입니다.
   * PDF 런타임 옵션이 포함된 `PDFOutputOptionsSpec` 개체
   * 렌더링 런타임 옵션이 포함된 `RenderOptionsSpec` 개체입니다.
   * 양식 디자인과 병합할 데이터가 들어 있는 XML 데이터 소스를 포함하는 `com.adobe.idp.Document` 개체입니다.

   이 `generatePDFOutput2` 메서드는 작업 결과를 포함하는 `OutputResult` 개체를 반환합니다.

1. 양식 데이터 스트림으로 작업을 수행합니다.

   * 객체의 메서드를 호출하여 비대화형 양식을 나타내는 `com.adobe.idp.Document` 객체를 `OutputResult` `getGeneratedDoc` 검색합니다.
   * 작업 결과가 포함된 `java.io.File` 개체를 만듭니다. 파일 이름 확장자가 .pdf인지 확인합니다.
   * 객체의 메서드를 호출하여 `com.adobe.idp.Document` 객체의 내용을 파일에 복사합니다(메서드에서 반환된 `copyToFile` 객체를 `com.adobe.idp.Document` `com.adobe.idp.Document` `getGeneratedDoc` 사용해야 함).

**참고 항목**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[빠른 시작(EJB 모드): Java API를 사용하여 문서를 출력 서비스로 전달](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[빠른 시작(SOAP 모드): Java API를 사용하여 문서를 출력 서비스로 전달](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 문서를 출력 서비스로 전달 {#pass-documents-to-the-output-service-using-the-web-service-api}

출력 서비스 및 컨텐츠 서비스(더 이상 사용되지 않음) API(웹 서비스)를 사용하여 컨텐츠 서비스에서 검색된 문서를 전달합니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 이 클라이언트 응용 프로그램은 두 개의 AEM Forms 서비스를 호출하므로 두 개의 서비스 참조를 만듭니다. 출력 서비스와 연결된 서비스 참조에 대해 다음 WSDL 정의를 사용하십시오. `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   Document Management 서비스와 연결된 서비스 참조에 다음 WSDL 정의를 사용하십시오. `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   데이터 `BLOB` 유형은 두 서비스 참조 모두에서 일반적이므로 데이터 유형을 사용할 때 `BLOB` 데이터 유형을 완전히 분류합니다. 해당 웹 서비스 빠른 시작에서 모든 `BLOB` 인스턴스는 정규화된 인스턴스입니다.

   >[!NOTE]
   >
   >AEM Forms `localhost` 를 호스팅하는 서버의 IP 주소로 대체합니다.

1. 출력 및 문서 관리 클라이언트 API 객체를 만듭니다.

   * 기본 생성자를 사용하여 `OutputServiceClient` 개체를 만듭니다.
   * 생성자를 사용하여 `OutputServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 만듭니다. WSDL을 지정하는 문자열 값을 Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/OutputService?blob=mtom`). 속성을 사용할 필요는 `lc_version` 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * 필드의 값을 `System.ServiceModel.BasicHttpBinding` 가져와 개체를 `OutputServiceClient.Endpoint.Binding` 만듭니다. 반환 값을 다음으로 캐스팅합니다 `BasicHttpBinding`.
   * 개체 `System.ServiceModel.BasicHttpBinding` 필드를 (으)로 `MessageEncoding` 설정합니다 `WSMessageEncoding.Mtom`. 이 값을 사용하면 MTOM이 사용됩니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM 양식 사용자 이름을 지정합니다 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 해당 암호 값을 필드에 지정합니다 `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 필드에 상수 값 `HttpClientCredentialType.Basic` 을 지정합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 필드에 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly` 을 지정합니다 `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >서비스 클라이언트에 대해 다음 단계를 `DocumentManagementServiceClient`반복합니다.

1. 콘텐츠 서비스에서 양식 디자인을 검색합니다(더 이상 사용되지 않음).

   객체의 메서드를 호출하고 다음 값을 전달하여 `DocumentManagementServiceClient` 컨텐츠를 `retrieveContent` 검색합니다.

   * 컨텐츠가 추가되는 스토어를 지정하는 문자열 값. 기본 스토어는 입니다 `SpacesStore`. 이 값은 필수 매개 변수입니다.
   * 검색할 컨텐츠의 정규화된 경로를 지정하는 문자열 값(예: `/Company Home/Form Designs/Loan.xdp`). 이 값은 필수 매개 변수입니다.
   * 버전을 지정하는 문자열 값. 이 값은 선택적 매개 변수이며 빈 문자열을 전달할 수 있습니다. 이 경우 최신 버전이 검색됩니다.
   * 검색 링크 값을 저장하는 문자열 출력 매개 변수입니다.
   * 컨텐츠를 저장하는 `BLOB` 출력 매개 변수입니다. 이 출력 매개 변수를 사용하여 내용을 검색할 수 있습니다.
   * 컨텐츠 속성을 저장하는 `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` 출력 매개 변수입니다.
   * 출력 `CRCResult` 매개 변수입니다. 이 객체를 사용하는 대신 출력 매개 변수를 사용하여 컨텐츠를 검색할 수 있습니다. `BLOB`

1. 비대화형 PDF 양식을 렌더링합니다.

   개체의 `OutputServiceClient` 메서드를 `generatePDFOutput2` 호출하고 다음 값을 전달합니다.

   * 열거형 `TransformationFormat` 값입니다. PDF 문서를 생성하려면 을 지정합니다 `TransformationFormat.PDF`.
   * 이미지와 같은 추가 리소스가 있는 컨텐츠 루트를 지정하는 문자열 값입니다.
   * 양식 디자인을 나타내는 `BLOB` `BLOB` 개체(Content Services에서 반환되는 인스턴스 사용(더 이상 사용되지 않음).
   * PDF 런타임 옵션이 포함된 `PDFOutputOptionsSpec` 개체
   * 렌더링 런타임 옵션이 포함된 `RenderOptionsSpec` 개체입니다.
   * 양식 디자인과 병합할 데이터가 들어 있는 XML 데이터 소스를 포함하는 `BLOB` 개체입니다.
   * 메서드로 채워지는 출력 `BLOB` `generatePDFOutput2` 개체입니다. 이 `generatePDFOutput2` 메서드는 문서를 설명하는 생성된 메타데이터로 이 개체를 채웁니다. 이 매개 변수 값은 웹 서비스 호출에만 필요합니다.
   * 작업 결과를 포함하는 출력 `OutputResult` 개체입니다. 이 매개 변수 값은 웹 서비스 호출에만 필요합니다.

   이 `generatePDFOutput2` 메서드는 비대화형 PDF 양식이 포함된 `BLOB` 개체를 반환합니다.

1. 양식 데이터 스트림으로 작업을 수행합니다.

   * 생성자를 호출하여 `System.IO.FileStream` 개체를 만듭니다. 대화형 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 메서드에서 검색된 개체의 내용을 저장하는 바이트 `BLOB` 배열을 `generatePDFOutput2` 만듭니다. 개체 데이터 멤버의 값을 가져와 바이트 배열 `BLOB` 을 `MTOM` 채웁니다.
   * 생성자를 호출하고 개체를 전달하여 `System.IO.BinaryWriter` 개체를 `System.IO.FileStream` 만듭니다.
   * 개체의 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 PDF 파일 `System.IO.BinaryWriter` `Write` 에 씁니다.

**참고 항목**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 저장소에 있는 문서를 출력 서비스로 전달 {#passing-documents-located-in-the-repository-to-the-output-service}

출력 서비스는 일반적으로 XDP 파일로 저장되고 Designer에서 작성된 양식 디자인을 기반으로 하는 비대화형 PDF 양식을 렌더링합니다. 양식 디자인이 포함된 `com.adobe.idp.Document` 개체를 출력 서비스로 전달할 수 있습니다. 그런 다음 출력 서비스는 `com.adobe.idp.Document` 개체에 있는 양식 디자인을 렌더링합니다.

다른 AEM Forms 서비스 작업에서 인스턴스 `com.adobe.idp.Document` 를 반환하면 개체를 출력 서비스에 전달할 수 있는 이점이 `com.adobe.idp.Document` 있습니다. 즉, 다른 서비스 작업에서 `com.adobe.idp.Document` 인스턴스를 가져와 렌더링할 수 있습니다. 예를 들어 다음 그림과 같이 XDP 파일이 AEM Forms 저장소에 저장된다고 가정합니다.

![pd_pd_formrepository](assets/pd_pd_formrepository.png)

FormsFolder ** 폴더는 AEM Forms 저장소의 사용자 정의 위치입니다(이 위치는 예이며 기본적으로 존재하지 않음). 이 예에서는 Loan.xdp라는 양식 디자인이 이 폴더에 있습니다. 양식 디자인 외에도 이미지와 같은 기타 양식 자료를 이 위치에 저장할 수 있습니다. AEM Forms 저장소에 있는 리소스의 경로는 다음과 같습니다.

`Applications/Application-name/Application-version/Folder.../Filename`

프로그래밍 방식으로 AEM Forms 저장소에서 Loan.xdp를 검색하고 객체 내의 출력 서비스에 전달할 수 `com.adobe.idp.Document` 있습니다.

두 가지 방법 중 하나를 사용하여 저장소에 있는 XDP 파일을 기반으로 PDF를 만들 수 있습니다. XDP 위치를 참조로 전달하거나 저장소에서 XDP를 프로그래밍 방식으로 검색하여 XDP 파일 내의 출력 서비스로 전달할 수 있습니다.

[빠른 시작(EJB 모드): Java API를 사용하여 응용 프로그램 XDP 파일을 기반으로 PDF](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api) 문서 만들기(XDP 파일의 위치를 참조로 전달하는 방법 표시)

[빠른 시작(EJB 모드): Java API를 사용하여 AEM Forms 저장소에 있는 문서를 출력 서비스로](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) 전달합니다(AEM Forms 저장소에서 XDP 파일을 프로그래밍 방식으로 검색하고 인스턴스 내에서 출력 서비스에 전달하는 방법 `com.adobe.idp.Document` 표시). (이 섹션에서는 이 작업을 수행하는 방법에 대해 설명합니다.)

>[!NOTE]
>
>양식 서비스에 대한 자세한 내용은 AEM Forms에 대한 [서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-3}

AEM Forms 저장소에서 출력 서비스로 가져온 문서를 전달하려면 다음 작업을 수행합니다.

1. 프로젝트 파일 포함
1. 출력 및 문서 관리 클라이언트 API 객체를 만듭니다.
1. AEM Forms 저장소에서 양식 디자인을 검색합니다.
1. 비대화형 PDF 양식을 렌더링합니다.
1. 데이터 스트림으로 작업을 수행합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함하십시오.

**출력 및 문서 관리 클라이언트 API 객체 만들기**

출력 서비스 API 작업을 프로그래밍 방식으로 수행하려면 먼저 출력 클라이언트 API 개체를 만듭니다. 또한 이 워크플로우는 Content Services(더 이상 사용되지 않음)에서 XDP 파일을 검색하므로 Document Management API 개체를 만듭니다.

**AEM Forms 저장소에서 양식 디자인 검색**

저장소 API를 사용하여 AEM Forms 저장소에서 XDP 파일을 검색합니다. 자세한 내용은 리소스 [읽기를 참조하십시오](/help/forms/developing/aem-forms-repository.md#reading-resources).

XDP 파일은 인스턴스(또는 웹 서비스를 사용하는 경우 `com.adobe.idp.Document` `BLOB` 인스턴스) 내에서 반환됩니다. 그런 다음 출력 서비스의 `com.adobe.idp.Document` 인스턴스를 전달할 수 있습니다.

**비대화형 PDF 양식 렌더링**

비대화형 양식을 렌더링하려면 AEM Forms 저장소 API를 사용하여 반환된 `com.adobe.idp.Document` 인스턴스를 전달합니다.

>[!NOTE]
>
>양식 디자인 `generatePDFOutput2`이 포함된 개체 `generatePrintedOutput2`에 대해 이름을 지정하고 `com.adobe.idp.Document`수락하는 두 가지 새로운 메서드입니다. 또한 인쇄 스트림을 네트워크 프린터로 전송할 때 양식 디자인이 포함된 `com.adobe.idp.Document` 파일을 출력 서비스로 전달할 수 있습니다.

**양식 데이터 스트림으로 작업 수행**

비대화형 양식을 PDF 파일로 저장할 수 있습니다. 이 양식은 Adobe Reader 또는 Acrobat에서 볼 수 있습니다.

**참고 항목**

[Java API를 사용하여 저장소에 있는 문서를 출력 서비스로 전달](creating-document-output-streams.md#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[출력 서비스 API 빠른 시작](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

ResourceRepositoryClient

### Java API를 사용하여 저장소에 있는 문서를 출력 서비스로 전달 {#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api}

출력 서비스 및 저장소 API(Java)를 사용하여 저장소에서 검색한 문서를 전달합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-output-client.jar 및 adobe-repository-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. 출력 및 문서 관리 클라이언트 API 객체를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다. 연결 [속성 설정을 참조하십시오](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).
   * 생성자를 사용하여 개체를 `OutputClient` 만들고 개체를 `ServiceClientFactory` 전달합니다.
   * 생성자를 사용하여 개체를 `DocumentManagementServiceClientImpl` 만들고 개체를 `ServiceClientFactory` 전달합니다.

1. AEM Forms 저장소에서 양식 디자인을 검색합니다.

   개체의 `ResourceRepositoryClient` `readResourceContent` 메서드를 호출하고 URI 위치를 XDP 파일에 지정하는 문자열 값을 전달합니다. 예, `/Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`. 이 값은 필수입니다. 이 메서드는 XDP 파일을 나타내는 `com.adobe.idp.Document` 인스턴스를 반환합니다.

1. 비대화형 PDF 양식을 렌더링합니다.

   개체의 `OutputClient` 메서드를 `generatePDFOutput2` 호출하고 다음 값을 전달합니다.

   * 열거형 `TransformationFormat` 값입니다. PDF 문서를 생성하려면 을 지정합니다 `TransformationFormat.PDF`.
   * 이미지와 같은 추가 리소스가 있는 컨텐츠 루트를 지정하는 문자열 값입니다. 예, `repository:///Applications/FormsApplication/1.0/FormsFolder/`.
   * 양식 디자인을 나타내는 개체( `com.adobe.idp.Document` 개체의 `ResourceRepositoryClient` `readResourceContent` 메서드에서 반환된 인스턴스 사용)입니다.
   * PDF 런타임 옵션이 포함된 `PDFOutputOptionsSpec` 개체
   * 렌더링 런타임 옵션이 포함된 `RenderOptionsSpec` 개체입니다.
   * 양식 디자인과 병합할 데이터가 들어 있는 XML 데이터 소스를 포함하는 `com.adobe.idp.Document` 개체입니다.

   이 `generatePDFOutput2` 메서드는 작업 결과를 포함하는 `OutputResult` 개체를 반환합니다.

1. 양식 데이터 스트림으로 작업을 수행합니다.

   * 객체의 메서드를 호출하여 비대화형 양식을 나타내는 `com.adobe.idp.Document` 객체를 `OutputResult` `getGeneratedDoc` 검색합니다.
   * 작업 결과가 포함된 `java.io.File` 개체를 만듭니다. 파일 이름 확장자가 .pdf인지 확인합니다.
   * 객체의 메서드를 호출하여 `com.adobe.idp.Document` 객체의 내용을 파일에 복사합니다(메서드에서 반환된 `copyToFile` 객체를 `com.adobe.idp.Document` `com.adobe.idp.Document` `getGeneratedDoc` 사용해야 함).

**참고 항목**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[빠른 시작(EJB 모드): Java API를 사용하여 AEM Forms 저장소에 있는 문서를 출력 서비스로 전달](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 조각을 사용하여 PDF 문서 만들기 {#creating-pdf-documents-using-fragments}

출력 및 어셈블러 서비스를 사용하여 조각을 기반으로 하는 PDF 문서와 같은 출력 스트림을 만들 수 있습니다. Assembler 서비스는 여러 XDP 파일에 있는 조각을 기반으로 하는 XDP 문서를 어셈블합니다. 결합된 XDP 문서는 PDF 문서를 만드는 출력 서비스로 전달됩니다. 이 워크플로우에는 생성 중인 PDF 문서가 표시되지만 출력 서비스는 이 워크플로우에서 ZPL과 같은 다른 출력 유형을 생성할 수 있습니다. PDF 문서는 토론의 목적으로만 사용됩니다.

다음 그림은 이 워크플로우를 보여줍니다.

![cp_cp_outputassemblyfragments](assets/cp_cp_outputassemblefragments.png)

[조각 *을 사용하여 PDF 문서*&#x200B;만들기]를 읽기 전에 여러 XDP 문서를 조합하는 데 어셈블러 서비스를 사용하는 것에 익숙해지는 것이 좋습니다. (여러 [XDP 조각 조합을 참조하십시오](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments).)

>[!NOTE]
>
>또한 어셈블러 서비스에서 어셈블하는 양식 디자인을 출력 서비스 대신 양식 서비스로 전달할 수 있습니다. Output service와 Forms 서비스의 주요 차이점은 Forms 서비스가 대화형 PDF 문서를 생성하고 출력 서비스에서 비대화형 PDF 문서를 생성한다는 것입니다. 또한 양식 서비스는 ZPL과 같은 프린터 기반 출력 스트림을 생성할 수 없습니다.

>[!NOTE]
>
>출력 서비스에 대한 자세한 내용은 AEM Forms에 대한 [서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-4}

조각을 기반으로 PDF 문서를 만들려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. 출력 및 어셈블러 클라이언트 개체를 만듭니다.
1. 어셈블리 서비스를 사용하여 양식 디자인을 생성합니다.
1. 출력 서비스를 사용하여 PDF 문서를 생성합니다.
1. PDF 문서를 PDF 파일로 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**출력 및 어셈블러 클라이언트 개체 만들기**

출력 서비스 API 작업을 프로그래밍 방식으로 수행하려면 먼저 출력 클라이언트 API 개체를 만듭니다. 또한 이 워크플로우는 Assembler 서비스를 호출하여 양식 디자인을 만들기 때문에 Assembler Client API 개체를 만듭니다.

**Assembler 서비스를 사용하여 양식 디자인 생성**

어셈블리 서비스를 사용하여 조각을 사용하여 양식 디자인을 생성합니다. 어셈블러 서비스는 양식 디자인이 포함된 `com.adobe.idp.Document` 인스턴스를 반환합니다.

**출력 서비스를 사용하여 PDF 문서 생성**

출력 서비스를 사용하여 어셈블러 서비스가 만든 양식 디자인을 사용하여 PDF 문서를 생성할 수 있습니다. Assembler 서비스가 출력 서비스로 반환한 `com.adobe.idp.Document` 인스턴스를 전달합니다.

**PDF 문서를 PDF 파일로 저장**

출력 서비스에서 PDF 문서를 생성한 후 PDF 파일로 저장할 수 있습니다.

**참고 항목**

[Java API를 사용하여 조각을 기반으로 PDF 문서 만들기](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-java-api)

[웹 서비스 API를 사용하여 조각을 기반으로 PDF 문서 만들기](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[출력 서비스 API 빠른 시작](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[여러 XDP 조각 정리](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments)

[PDF 문서 작성](creating-document-output-streams.md#creating-pdf-documents)

### Java API를 사용하여 조각을 기반으로 PDF 문서 만들기 {#create-a-pdf-document-based-on-fragments-using-the-java-api}

출력 서비스 API 및 어셈블러 서비스 API(Java)를 사용하여 조각을 기반으로 PDF 문서를 만듭니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-output-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. 출력 및 어셈블러 클라이언트 개체를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 개체를 `OutputClient` 만들고 개체를 `ServiceClientFactory` 전달합니다.
   * 생성자를 사용하여 개체를 `AssemblerServiceClient` 만들고 개체를 `ServiceClientFactory` 전달합니다.

1. 어셈블리 서비스를 사용하여 양식 디자인을 생성합니다.

   개체의 `AssemblerServiceClient` `invokeDDX` 메서드를 호출하고 다음 필수 값을 전달합니다.

   * 사용할 DCX 문서를 나타내는 `com.adobe.idp.Document` 개체입니다.
   * 입력 XDP 파일을 포함하는 `java.util.Map` 개체입니다.
   * 기본 글꼴 및 작업 로그 수준을 포함하여 런타임 옵션을 지정하는 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 개체입니다.

   이 `invokeDDX` 메서드는 조합된 XDP 문서를 포함하는 `com.adobe.livecycle.assembler.client.AssemblerResult` 개체를 반환합니다. 어셈블된 XDP 문서를 검색하려면 다음 작업을 수행하십시오.

   * 개체의 `AssemblerResult` 메서드를 `getDocuments` 호출합니다. 이 메서드는 `java.util.Map` 개체를 반환합니다.
   * 결과 개체를 찾을 때까지 개체 `java.util.Map` 를 반복하십시오 `com.adobe.idp.Document` .
   * 오브젝트의 `com.adobe.idp.Document` `copyToFile` 방법을 불러와서 결합된 XDP 문서를 추출합니다.


1. 출력 서비스를 사용하여 PDF 문서를 생성합니다.

   개체의 `OutputClient` 메서드를 `generatePDFOutput2` 호출하고 다음 값을 전달합니다.

   * 열거형 `TransformationFormat` 값입니다. PDF 문서를 생성하려면 `TransformationFormat.PDF`
   * 이미지와 같은 추가 리소스가 있는 컨텐츠 루트를 지정하는 문자열 값
   * 양식 디자인을 나타내는 `com.adobe.idp.Document` 개체(어셈블러 서비스에서 반환된 인스턴스 사용)
   * PDF 런타임 옵션이 포함된 `PDFOutputOptionsSpec` 개체
   * 렌더링 런타임 옵션이 포함된 `RenderOptionsSpec` 개체
   * 양식 디자인과 병합할 데이터가 들어 있는 XML 데이터 소스를 포함하는 `com.adobe.idp.Document` 개체

   이 `generatePDFOutput2` `OutputResult` 메서드는 작업 결과를 포함하는 개체를 반환합니다.

1. PDF 문서를 PDF 파일로 저장합니다.

   * 개체의 메서드를 호출하여 PDF 문서를 나타내는 `com.adobe.idp.Document` 개체를 `OutputResult` `getGeneratedDoc` 검색합니다.
   * 작업 결과가 포함된 `java.io.File` 개체를 만듭니다. 파일 이름 확장자가 .pdf인지 확인합니다.
   * 개체의 `com.adobe.idp.Document` 메서드를 `copyToFile` 호출하여 `com.adobe.idp.Document` 개체의 내용을 파일에 복사합니다. 메서드가 반환되는 `com.adobe.idp.Document` 개체를 사용해야 `getGeneratedDoc` 합니다.

**참고 항목**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[빠른 시작(EJB 모드): Java API를 사용하여 조각을 기반으로 PDF 문서 만들기](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[빠른 시작(SOAP 모드): Java API를 사용하여 조각을 기반으로 PDF 문서 만들기](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성을 설정합니다](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### 웹 서비스 API를 사용하여 조각을 기반으로 PDF 문서 만들기 {#create-a-pdf-document-based-on-fragments-using-the-web-service-api}

출력 서비스 API 및 어셈블러 서비스 API(웹 서비스)를 사용하여 조각을 기반으로 PDF 문서를 만듭니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 출력 서비스와 연결된 서비스 참조에 대해 다음 WSDL 정의를 사용하십시오.

   ```java
    http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1.
   ```

   어셈블러 서비스와 연결된 서비스 참조에 다음 WSDL 정의를 사용하십시오.

   ```java
    http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   데이터 `BLOB` 유형은 두 서비스 참조 모두에서 일반적이므로 데이터 유형을 사용할 때 `BLOB` 데이터 유형을 완전히 분류합니다. 해당 웹 서비스 빠른 시작에서 모든 `BLOB` 인스턴스는 정규화된 인스턴스입니다.

   >[!NOTE]
   >
   >AEM Forms `localhost` 를 호스팅하는 서버의 IP 주소로 대체합니다.

1. 출력 및 어셈블러 클라이언트 개체를 만듭니다.

   * 기본 생성자를 사용하여 `OutputServiceClient` 개체를 만듭니다.
   * 생성자를 사용하여 `OutputServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 속성을 사용할 필요는 `lc_version` 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다. 하지만 MTOM `?blob=mtom` 을 사용하도록 지정합니다.
   * 필드의 값을 `System.ServiceModel.BasicHttpBinding` 가져와 개체를 `OutputServiceClient.Endpoint.Binding` 만듭니다. 반환 값을 다음으로 캐스팅합니다 `BasicHttpBinding`.
   * 개체 `System.ServiceModel.BasicHttpBinding` 필드를 (으)로 `MessageEncoding` 설정합니다 `WSMessageEncoding.Mtom`. 이 값을 사용하면 MTOM이 사용됩니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * AEM Forms 사용자 이름을 `OutputServiceClient.ClientCredentials.UserName.UserName`필드에 지정합니다.
      * 해당 암호 값을 `OutputServiceClient.ClientCredentials.UserName.Password`필드에 지정합니다.
      * 상수 값 `HttpClientCredentialType.Basic` 을 `BasicHttpBindingSecurity.Transport.ClientCredentialType`필드에 지정합니다.
   * `BasicHttpSecurityMode.TransportCredentialOnly` 필드에 `BasicHttpBindingSecurity.Security.Mode`상수 값을 지정합니다.

   >[!NOTE]
   >
   >객체에 대해 이 단계를 `AssemblerServiceClient`반복합니다.

1. 어셈블리 서비스를 사용하여 양식 디자인을 생성합니다.

   개체의 `AssemblerServiceClient` 메서드를 `invokeDDX` 호출하고 다음 값을 전달합니다.

   * DCX 문서를 나타내는 `BLOB` 개체
   * 필수 파일이 포함된 `MyMapOf_xsd_string_To_xsd_anyType` 개체
   * 런타임 옵션을 지정하는 `AssemblerOptionSpec` 개체

   이 `invokeDDX` `AssemblerResult` 메서드는 작업 결과와 발생한 예외를 포함하는 개체를 반환합니다. 새로 만든 XDP 문서를 얻으려면 다음 작업을 수행하십시오.

   * 결과 PDF 문서 `AssemblerResult` 가 포함된 개체인 개체의 `documents` 필드에 `Map` 액세스합니다.
   * 개체를 반복하여 `Map` 어셈블된 양식 디자인을 검색합니다. 해당 어레이 멤버 `value` 를 A로 `BLOB`캐스팅합니다. 이 `BLOB` 인스턴스를 출력 서비스로 전달합니다.


1. 출력 서비스를 사용하여 PDF 문서를 생성합니다.

   개체의 `OutputServiceClient` 메서드를 `generatePDFOutput2` 호출하고 다음 값을 전달합니다.

   * 열거형 `TransformationFormat` 값입니다. PDF 문서를 생성하려면 을 지정합니다 `TransformationFormat.PDF`.
   * 이미지와 같은 추가 리소스가 있는 컨텐츠 루트를 지정하는 문자열 값입니다.
   * 양식 디자인을 나타내는 `BLOB` 개체(Assembler 서비스에서 반환한 인스턴스 사용) `BLOB` .
   * PDF 런타임 옵션이 포함된 `PDFOutputOptionsSpec` 개체
   * 렌더링 런타임 옵션이 포함된 `RenderOptionsSpec` 개체입니다.
   * 양식 디자인과 병합할 데이터가 들어 있는 XML 데이터 소스를 포함하는 `BLOB` 개체입니다.
   * 메서드가 채우는 출력 `BLOB``generatePDFOutput2` 개체입니다. 이 `generatePDFOutput2` 메서드는 문서를 설명하는 생성된 메타데이터로 이 개체를 채웁니다. 이 매개 변수 값은 웹 서비스 호출에만 필요합니다.
   * 작업 결과를 포함하는 출력 `OutputResult` 개체입니다. 이 매개 변수 값은 웹 서비스 호출에만 필요합니다.

   이 `generatePDFOutput2` 메서드는 비대화형 PDF 양식이 포함된 `BLOB` 개체를 반환합니다.

1. PDF 문서를 PDF 파일로 저장합니다.

   * 생성자를 호출하여 `System.IO.FileStream` 개체를 만듭니다. 대화형 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 메서드에서 검색된 개체의 내용을 저장하는 바이트 `BLOB` 배열을 `generatePDFOutput2` 만듭니다. 개체 데이터 멤버의 값을 가져와 바이트 배열 `BLOB` 을 `MTOM` 채웁니다.
   * 생성자를 호출하고 개체를 전달하여 `System.IO.BinaryWriter` 개체를 `System.IO.FileStream` 만듭니다.
   * 개체의 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 PDF 파일 `System.IO.BinaryWriter` `Write` 에 씁니다.

**참고 항목**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 파일로 인쇄 {#printing-to-files}

출력 서비스를 사용하여 PostScript, PCL(프린터 제어 언어) 또는 다음 레이블 포맷과 같은 스트림을 파일로 인쇄할 수 있습니다.

* Zebra - ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

출력 서비스를 사용하면 XML 데이터를 양식 디자인과 병합하고 양식을 파일로 인쇄할 수 있습니다. 다음 그림은 레이저 및 레이블 파일을 만드는 출력 서비스입니다.

>[!NOTE]
>
>인쇄업체에 인쇄 스트림을 전송하는 방법에 대한 자세한 내용은 인쇄소에 [인쇄 스트림 전송을 참조하십시오](creating-document-output-streams.md#sending-print-streams-to-printers).

>[!NOTE]
>
>출력 서비스에 대한 자세한 내용은 AEM Forms에 대한 [서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-5}

파일로 인쇄하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. 출력 클라이언트 개체를 만듭니다.
1. XML 데이터 소스를 참조합니다.
1. 파일로 인쇄하는 데 필요한 인쇄 런타임 옵션을 설정합니다.
1. 인쇄 스트림을 파일로 인쇄합니다.
1. 작업 결과를 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(AEM Forms이 JBoss에 배포된 경우 필요)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필요)

AEM Forms이 JBoss가 아닌 지원되는 J2EE 응용 프로그램 서버에 배포된 경우 adobe-utilities.jar 및 jbossall-client.jar 파일을 AEM Forms이 배포된 J2EE 응용 프로그램 서버에 고유한 JAR 파일로 대체해야 합니다. AEM Forms Java 라이브러리 파일 [포함을 참조하십시오](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**출력 클라이언트 개체 만들기**

출력 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 출력 서비스 클라이언트 개체를 만들어야 합니다. Java API를 사용하는 경우 `OutputClient` 개체를 만듭니다. 출력 웹 서비스 API를 사용하는 경우 `OutputServiceService` 개체를 만듭니다.

**XML 데이터 소스 참조**

데이터가 포함된 문서를 인쇄하려면 데이터를 채울 모든 양식 필드에 대한 XML 요소가 포함된 XML 데이터 소스를 참조해야 합니다. XML 요소 이름은 필드 이름과 일치해야 합니다. XML 요소는 양식 필드에 해당되지 않거나 XML 요소 이름이 필드 이름과 일치하지 않는 경우 무시됩니다. 모든 XML 요소가 지정된 경우 XML 요소가 표시되는 순서와 일치할 필요는 없습니다.

**파일로 인쇄하는 데 필요한 인쇄 런타임 옵션 설정**

파일로 인쇄하려면 출력 서비스가 인쇄하는 파일의 위치와 이름을 지정하여 파일 URI 런타임 옵션을 설정해야 합니다. 예를 들어 출력 서비스가 MortgageForm.ps라는 PostScript 파일을 C:\Adobe으로 *인쇄하도록 지정하려면 C:\Adobe\MortgageForm.ps을* 지정합니다.

>[!NOTE]
>
>정의할 수 있는 선택적 런타임 옵션이 있습니다. 설정할 수 있는 모든 옵션에 대한 자세한 내용은 `PrintedOutputOptionsSpec` AEM Forms API 참조 [](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)의 클래스 참조를 참조하십시오.

**인쇄 스트림을 파일로 인쇄**

양식 데이터가 포함된 유효한 XML 데이터 소스를 참조하고 인쇄 런타임 옵션을 설정한 후 출력 서비스를 호출하여 파일을 인쇄할 수 있습니다.

**작업 결과 검색**

출력 서비스는 작업을 수행한 후 XML 데이터와 같은 다양한 데이터 항목을 반환하여 작업이 성공했는지 여부를 지정합니다.

**참고 항목**

[Java API를 사용하여 파일로 인쇄](creating-document-output-streams.md#print-to-files-using-the-java-api)

[웹 서비스 API를 사용하여 파일로 인쇄](creating-document-output-streams.md#print-to-files-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[출력 서비스 API 빠른 시작](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java API를 사용하여 파일로 인쇄 {#print-to-files-using-the-java-api}

출력 API(Java)를 사용하여 파일로 인쇄:

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-output-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. 출력 클라이언트 개체를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 개체를 `OutputClient` 만들고 개체를 `ServiceClientFactory` 전달합니다.

1. XML 데이터 소스를 참조합니다.

   * 생성자를 사용하여 문서를 채우는 데 사용되는 XML 데이터 소스를 나타내는 `java.io.FileInputStream` 객체를 만들고 XML 파일의 위치를 지정하는 문자열 값을 전달합니다.
   * 생성자를 사용하여 개체를 `com.adobe.idp.Document` 만들고 개체를 `java.io.FileInputStream` 전달합니다.

1. 파일로 인쇄하는 데 필요한 인쇄 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 `PrintedOutputOptionsSpec` 개체를 만듭니다.
   * PrintedOutputOptionsSpec 개체의 메서드를 호출하고 파일의 이름과 위치를 나타내는 문자열 값을 전달하여 파일을 지정합니다. `setFileURI` 예를 들어 출력 서비스가 C:\Adobe에 있는 ModitionForm.ps라는 PostScript 파일로 인쇄되도록 하려면 C:\\Adobe\MortgageForm.ps을 지정합니다.
   * 개체의 메서드를 호출하고 복사본 수를 나타내는 정수 값을 전달하여 인쇄할 복사본 수를 `PrintedOutputOptionsSpec` 지정합니다 `setCopies` .

1. 인쇄 스트림을 파일로 인쇄합니다.

   개체의 메서드를 호출하고 다음 값을 전달하여 `OutputClient` 파일로 `generatePrintedOutput` 인쇄합니다.

   * 만들 인쇄 스트림 형식을 지정하는 열거형 `PrintFormat` 값입니다. 예를 들어 PostScript 인쇄 스트림을 만들려면 전달하십시오 `PrintFormat.PostScript`.
   * 양식 디자인의 이름을 지정하는 문자열 값입니다.
   * 이미지 파일과 같은 관련 자료 파일의 위치를 지정하는 문자열 값.
   * 사용할 XDC 파일의 위치를 지정하는 문자열 값(개체를 사용하여 사용할 XDC 파일을 지정한 `null` 경우 전달할 수 `PrintedOutputOptionsSpec` 있습니다).
   * 파일로 인쇄하는 데 필요한 런타임 옵션이 포함된 `PrintedOutputOptionsSpec` 개체입니다.
   * 양식 데이터를 포함하는 XML 데이터 소스를 포함하는 `com.adobe.idp.Document` 개체입니다.

   이 `generatePrintedOutput` 메서드는 작업 결과를 포함하는 `OutputResult` 개체를 반환합니다.

   >[!NOTE]
   >
   >개체의 `OutputResult` 메서드가 `getRecordLevelMetaDataList` 반환됩니다 `null`.

1. 작업 결과를 검색합니다.

   * 개체의 메서드를 호출하여 메서드 `com.adobe.idp.Document` 의 상태를 나타내는 `generatePrintedOutput` 개체 `OutputResult` 를 만듭니다( `getStatusDoc` 개체가 메서드에 의해 `OutputResult` `generatePrintedOutput` 반환됨).
   * 작업 결과를 포함할 `java.io.File` 개체를 만듭니다. 파일 확장자가 XML인지 확인합니다.
   * 객체의 메서드를 호출하여 `com.adobe.idp.Document` 객체의 내용을 파일에 복사합니다(메서드에서 반환된 `copyToFile` 객체를 `com.adobe.idp.Document` `com.adobe.idp.Document` `getStatusDoc` 사용해야 함).

**참고 항목**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[빠른 시작(SOAP 모드): Java API를 사용하여 파일로 인쇄](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-printing-to-a-file-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성을 설정합니다](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### 웹 서비스 API를 사용하여 파일로 인쇄 {#print-to-files-using-the-web-service-api}

출력 API(웹 서비스)를 사용하여 파일로 인쇄:

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Forms `localhost` 를 호스팅하는 서버의 IP 주소로 대체합니다.

1. 출력 클라이언트 개체를 만듭니다.

   * 기본 생성자를 사용하여 `OutputServiceClient` 개체를 만듭니다.
   * 생성자를 사용하여 `OutputServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 속성을 사용할 필요는 `lc_version` 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다. 하지만 MTOM `?blob=mtom` 을 사용하도록 지정합니다.
   * 필드의 값을 `System.ServiceModel.BasicHttpBinding` 가져와 개체를 `OutputServiceClient.Endpoint.Binding` 만듭니다. 반환 값을 다음으로 캐스팅합니다 `BasicHttpBinding`.
   * 개체 `System.ServiceModel.BasicHttpBinding` 필드를 (으)로 `MessageEncoding` 설정합니다 `WSMessageEncoding.Mtom`. 이 값을 사용하면 MTOM이 사용됩니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM 양식 사용자 이름을 지정합니다 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 해당 암호 값을 필드에 지정합니다 `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 필드에 상수 값 `HttpClientCredentialType.Basic` 을 지정합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 필드에 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly` 을 지정합니다 `BasicHttpBindingSecurity.Security.Mode`.

1. XML 데이터 소스를 참조합니다.

   * 생성자를 사용하여 `BLOB` 개체를 만듭니다. 이 `BLOB` 개체는 양식 데이터를 저장하는 데 사용됩니다.
   * 생성자를 호출하고 양식 데이터를 포함하는 XML 파일의 위치를 지정하는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * 개체의 내용을 저장하는 바이트 배열을 `System.IO.FileStream` 만듭니다. 개체의 속성을 가져와 바이트 배열의 크기를 결정할 수 `System.IO.FileStream` `Length` 있습니다.
   * 개체의 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열 `System.IO.FileStream` `Read` 을 스트림 데이터로 채웁니다.
   * 바이트 배열의 컨텐츠로 해당 `BLOB` `binaryData` 속성을 지정하여 개체를 채웁니다.

1. 파일로 인쇄하는 데 필요한 인쇄 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 `PrintedOutputOptionsSpec` 개체를 만듭니다.
   * 파일의 위치와 이름을 나타내는 문자열 값을 `PrintedOutputOptionsSpec` 개체의 `fileURI` 데이터 멤버에 할당하여 파일을 지정합니다. 예를 들어 출력 서비스가 C:\Adobe에 있는 MortgageForm.ps라는 PostScript 파일로 인쇄되도록 하려면 C:\\Adobe\MortgageForm.ps *을* 지정합니다.
   * 개체의 데이터 멤버에 대한 복사본 수를 나타내는 정수 값을 할당하여 인쇄할 복사본 수를 `PrintedOutputOptionsSpec` 지정합니다 `copies` .

1. 인쇄 스트림을 파일로 인쇄합니다.

   개체의 메서드를 호출하고 다음 값을 전달하여 `OutputServiceService` 파일로 `generatePrintedOutput` 인쇄합니다.

   * 만들 인쇄 스트림 형식을 지정하는 열거형 `PrintFormat` 값입니다. 예를 들어 PostScript 인쇄 스트림을 만들려면 전달하십시오 `PrintFormat.PostScript`.
   * 양식 디자인의 이름을 지정하는 문자열 값입니다.
   * 이미지 파일과 같은 관련 자료 파일의 위치를 지정하는 문자열 값.
   * 사용할 XDC 파일의 위치를 지정하는 문자열 값(개체를 사용하여 사용할 XDC 파일을 지정한 `null` 경우 전달할 수 `PrintedOutputOptionsSpec` 있습니다).
   * 파일로 인쇄하는 데 필요한 인쇄 런타임 옵션이 포함된 `PrintedOutputOptionsSpec` 개체입니다.
   * 양식 데이터를 포함하는 XML 데이터 소스를 포함하는 `BLOB` 개체입니다.
   * 메서드로 채워지는 `BLOB` `generatePDFOutput` 개체입니다. 이 `generatePDFOutput` 메서드는 문서를 설명하는 생성된 메타데이터로 이 개체를 채웁니다. 이 매개 변수 값은 웹 서비스 호출에만 필요합니다.
   * 메서드로 채워지는 `BLOB` `generatePDFOutput` 개체입니다. 이 `generatePDFOutput` 개체는 결과 데이터로 채워집니다. 이 매개 변수 값은 웹 서비스 호출에만 필요합니다.
   * 작업 결과를 포함하는 `OutputResult` 개체입니다. 이 매개 변수 값은 웹 서비스 호출에만 필요합니다.

1. 작업 결과를 검색합니다.

   * 생성자를 호출하고 결과 데이터가 포함된 XML 파일 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다. 파일 확장자가 XML인지 확인합니다.
   * 개체의 메서드(8번째 매개 변수)로 결과 데이터로 채워진 `BLOB` 개체의 데이터 콘텐츠를 저장하는 `OutputServiceService` 바이트 `generatePDFOutput` 배열을 만듭니다. 개체 데이터 멤버의 값을 가져와 바이트 배열 `BLOB` 을 `MTOM` 채웁니다.
   * 생성자를 호출하고 개체를 전달하여 `System.IO.BinaryWriter` 개체를 `System.IO.FileStream` 만듭니다.
   * 개체의 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열 내용을 XML 파일에 `System.IO.BinaryWriter``Write` 씁니다.

**참고 항목**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 인쇄업체에 인쇄 스트림 전송 {#sending-print-streams-to-printers}

출력 서비스를 사용하여 PostScript, PCL(프린터 제어 언어) 또는 다음 레이블 포맷과 같은 인쇄 스트림을 네트워크 프린터에 전송할 수 있습니다.

* Zebra - ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

출력 서비스를 사용하면 XML 데이터를 양식 디자인과 병합하고 양식을 인쇄 스트림으로 출력할 수 있습니다. 예를 들어 PostScript 인쇄 스트림을 만들어 네트워크 프린터로 전송할 수 있습니다. 다음 그림은 네트워크 프린터로 인쇄 스트림을 전송하는 출력 서비스입니다.

>[!NOTE]
>
>인쇄 스트림을 네트워크 프린터로 보내는 방법을 보여주기 위해 이 섹션에서는 SharedPrinter 프로토콜을 사용하여 PostScript 인쇄 스트림을 네트워크 프린터로 보냅니다.

>[!NOTE]
>
>출력 서비스에 대한 자세한 내용은 AEM Forms에 대한 [서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-6}

인쇄 스트림을 네트워크 프린터로 전송하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. 출력 클라이언트 개체를 만듭니다.
1. XML 데이터 소스를 참조합니다.
1. 인쇄 런타임 옵션 설정
1. 인쇄할 문서를 검색합니다.
1. 문서를 네트워크 프린터로 보냅니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(AEM Forms이 JBoss에 배포된 경우 필요)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필수)

AEM Forms이 JBoss가 아닌 지원되는 J2EE 응용 프로그램 서버에 배포된 경우 adobe-utilities.jar 및 jbossall-client.jar 파일을 AEM Forms이 배포된 J2EE 응용 프로그램 서버에 고유한 JAR 파일로 대체해야 합니다.

**출력 클라이언트 개체 만들기**

출력 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 출력 서비스 클라이언트 개체를 만듭니다. Java API를 사용하는 경우 `OutputClient` 개체를 만듭니다. 출력 웹 서비스 API를 사용하는 경우 `OutputServiceClient` 개체를 만듭니다.

**XML 데이터 소스 참조**

데이터가 포함된 문서를 인쇄하려면 데이터를 채울 모든 양식 필드에 대한 XML 요소가 포함된 XML 데이터 소스를 참조해야 합니다. XML 요소 이름은 필드 이름과 일치해야 합니다. XML 요소는 양식 필드에 해당되지 않거나 XML 요소 이름이 필드 이름과 일치하지 않는 경우 무시됩니다. 모든 XML 요소가 지정된 경우 XML 요소가 표시되는 순서와 일치할 필요는 없습니다.

**인쇄 런타임 옵션 설정**

인쇄 스트림을 프린터로 전송할 때 다음 옵션을 비롯한 런타임 옵션을 설정할 수 있습니다.

* **사본**: 프린터로 전송할 복사본 수를 지정합니다. 기본값은 1입니다.
* **스테이플**: 스테이플러를 사용할 때 XCI 옵션이 설정됩니다. 이 옵션은 구성 모델에서 스테이플 요소로 지정할 수 있으며 PS 및 PCL 프린터에만 사용됩니다.
* **출력 조그**: 출력 페이지에 주석을 달 때(출력 트레이에서 물리적으로 이동) XCI 옵션이 설정됩니다. 이 옵션은 PS 및 PCL 프린터 전용입니다.
* **출력 저장소**: 인쇄 드라이버가 해당 출력 저장소를 선택할 수 있도록 하는 데 사용되는 XCI 값.

>[!NOTE]
>
>설정할 수 있는 모든 런타임 옵션에 대한 자세한 내용은 `PrintedOutputOptionsSpec` 클래스 참조를 참조하십시오.

**인쇄할 문서 검색**

인쇄 스트림을 검색하여 프린터로 보냅니다. 예를 들어 PostScript 파일을 검색하여 프린터로 전송할 수 있습니다.

프린터가 PDF를 지원하는 경우 PDF 파일을 보내도록 선택할 수 있습니다. 그러나 PDF 문서를 프린터로 보내는 데 문제가 있는 경우 각 프린터 제조업체는 PDF 인터프리터를 다르게 구현했습니다. 즉, 일부 인쇄 제조업체는 Adobe PDF 해석을 사용하지만 프린터에 따라 다릅니다. 다른 프린터에는 자체 PDF 인터프리터가 있습니다. 따라서 인쇄 결과는 다를 수 있습니다.

PDF 문서를 프린터로 전송할 때의 또 다른 제한 사항은 인쇄용이라는 것입니다. 프린터의 설정을 제외한 이중, 용지 트레이 선택 및 스테이플에 액세스할 수 없습니다.

인쇄할 문서를 검색하려면 해당 방법을 `generatePrintedOutput` 사용합니다. 다음 표는 메서드를 사용할 때 지정된 인쇄 스트림에 대해 설정된 내용 유형을 `generatePrintedOutput` 지정합니다.

<table>
 <thead>
  <tr>
   <th><p>인쇄 형식 </p></th>
   <th><p>설명</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>DPL </p></td>
   <td><p>기본 또는 사용자 정의 xdc 출력 스트림으로 dpl203.xdc를 만듭니다.</p></td>
  </tr>
  <tr>
   <td><p>DPL 300 DPI </p></td>
   <td><p>DPL 300 DPI 출력 스트림을 만듭니다.</p></td>
  </tr>
  <tr>
   <td><p>DPL 406 DPI </p></td>
   <td><p>DPL 400 DPI 출력 스트림을 만듭니다.</p></td>
  </tr>
  <tr>
   <td><p>DPL 600 DPI </p></td>
   <td><p>DPL 600 DPI 출력 스트림을 만듭니다.</p></td>
  </tr>
  <tr>
   <td><p>범용 색상 PCL </p></td>
   <td><p>범용 색상 PCL(5c) 출력 스트림을 만듭니다.</p></td>
  </tr>
  <tr>
   <td><p>GenericPSLevel3 </p></td>
   <td><p>일반 PostScript 레벨 3 출력 스트림을 만듭니다.</p></td>
  </tr>
  <tr>
   <td><p>IPL </p></td>
   <td><p>사용자 지정 IPL 출력 스트림을 만듭니다.</p></td>
  </tr>
  <tr>
   <td><p>IPL 300 DPI </p></td>
   <td><p>IPL 300DPI 출력 스트림을 만듭니다.</p></td>
  </tr>
  <tr>
   <td><p>IPL 400 DPI </p></td>
   <td><p>IPL 400DPI 출력 스트림을 만듭니다.</p></td>
  </tr>
  <tr>
   <td><p>PCL </p></td>
   <td><p>범용 단색 PCL(5e) 출력 스트림을 만듭니다.</p></td>
  </tr>
  <tr>
   <td><p>PostScript </p></td>
   <td><p>일반 PostScript 레벨 2 출력 스트림을 만듭니다.</p></td>
  </tr>
  <tr>
   <td><p>TPCL </p></td>
   <td><p>사용자 지정 TPCL 출력 스트림을 만듭니다.</p></td>
  </tr>
  <tr>
   <td><p>TPCL 305 DPI </p></td>
   <td><p>TPCL 305 DPI 출력 스트림을 만듭니다.</p></td>
  </tr>
  <tr>
   <td><p>TPCL 600 DPI </p></td>
   <td><p>TPCL 600 DPI 출력 스트림을 만듭니다.</p></td>
  </tr>
  <tr>
   <td><p>ZPL </p></td>
   <td><p>ZPL 203 DPI 출력 스트림을 만듭니다.</p></td>
  </tr>
  <tr>
   <td><p>ZPL 300 DPI </p></td>
   <td><p>ZPL 300 DPI 출력 스트림을 만듭니다.</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>이 방법을 사용하여 인쇄 스트림을 프린터로 보낼 수도 `generatePrintedOutput2` 있습니다. 그러나 프린터로 인쇄 스트림 전송 섹션과 연관된 빠른 시작은 `generatePrintedOutput` 방법을 사용합니다.

**인쇄 스트림을 네트워크 프린터로 보내기**

인쇄할 문서를 검색한 후 출력 서비스를 호출하여 인쇄 스트림을 네트워크 프린터로 전송할 수 있습니다. 출력 서비스가 프린터를 성공적으로 찾으려면 인쇄 서버와 프린터 이름을 모두 지정해야 합니다. 또한 인쇄 프로토콜도 지정해야 합니다.

>[!NOTE]
>
>PDFG가 양식 서버에 설치되어 있고 서버가 Windows Server 2008에서 실행되는 경우 SharedPrinter 속성을 사용할 수 없습니다. 이 경우 다른 프린터 프로토콜을 사용하십시오.

>[!NOTE]
>
>네트워크 프린터를 사용하고 있고 액세스 메커니즘이 SharedPrinter인 경우 프린터의 전체 네트워크 경로를 지정해야 합니다.Java API를 사용하여 인쇄 스트림을 네트워크 프린터로 보냅니다

출력 API(Java)를 사용하여 인쇄 스트림을 네트워크 프린터로 보냅니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-output-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. 출력 클라이언트 개체 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 개체를 `OutputClient` 만들고 개체를 `ServiceClientFactory` 전달합니다.

1. XML 데이터 소스 참조

   * 생성자를 사용하여 문서를 채우는 데 사용되는 XML 데이터 소스를 나타내는 `java.io.FileInputStream` 객체를 만들고 XML 파일의 위치를 지정하는 문자열 값을 전달합니다.
   * 생성자를 사용하여 개체를 `com.adobe.idp.Document` 만들고 개체를 `java.io.FileInputStream` 전달합니다.

1. 인쇄 런타임 옵션 설정

   인쇄 런타임 옵션을 나타내는 `PrintedOutputOptionsSpec` 개체를 만듭니다. 예를 들어 개체의 방법을 호출하여 인쇄할 복사본 수를 지정할 수 `PrintedOutputOptionsSpec` `setCopies` 있습니다.

   >[!NOTE]
   >
   >ZPL 인쇄 스트림을 생성하는 경우 `PrintedOutputOptionsSpec` 개체의 `setPagination` 방법을 사용하여 페이지 매김 값을 설정할 수 없습니다. 마찬가지로 ZPL 인쇄 스트림에 대해 다음 옵션을 설정할 수 없습니다. 출력 조그, 페이지 오프셋 및 스테이플. 이 `setPagination` 메서드는 PostScript 생성에서 유효하지 않습니다. PCL 생성 전용입니다.

1. 인쇄할 문서 검색

   * 개체의 메서드를 호출하고 다음 값을 전달하여 인쇄할 문서를 `OutputClient` `generatePrintedOutput` 검색합니다.

      * 인쇄 스트림을 지정하는 열거형 `PrintFormat` 값입니다. 예를 들어 PostScript 인쇄 스트림을 만들려면 전달하십시오 `PrintFormat.PostScript`.
      * 양식 디자인의 이름을 지정하는 문자열 값입니다.
      * 이미지 파일과 같은 관련 자료 파일의 위치를 지정하는 문자열 값.
      * 사용할 XDC 파일의 위치를 지정하는 문자열 값입니다.
      * 파일로 인쇄하는 데 필요한 런타임 옵션이 포함된 `PrintedOutputOptionsSpec` 개체입니다.
      * 양식 `com.adobe.idp.Document` 디자인과 병합할 양식 데이터가 들어 있는 XML 데이터 소스를 나타내는 개체입니다.

      이 메서드는 작업 결과를 포함하는 `OutputResult` 개체를 반환합니다.

   * 개체 &#39;s 메서드 `com.adobe.idp.Document` 를 호출하여 프린터로 전송할 개체를 `OutputResult` 만듭니다 `getGeneratedDoc` . 이 메서드는 `com.adobe.idp.Document` 개체를 반환합니다.


1. 인쇄 스트림을 네트워크 프린터로 보내기

   개체의 메서드를 호출하고 다음 값을 전달하여 인쇄 스트림 `OutputClient` 을 네트워크 프린터로 `sendToPrinter` 보냅니다.

   * 프린터로 전송할 인쇄 스트림을 나타내는 `com.adobe.idp.Document` 개체입니다.
   * 사용할 프린터 프로토콜을 지정하는 열거형 `PrinterProtocol` 값입니다. 예를 들어, SharedPrinter 프로토콜을 지정하려면 pass `PrinterProtocol.SharedPrinter`.
   * 인쇄 서버의 이름을 지정하는 문자열 값입니다. 예를 들어 인쇄 서버의 이름이 PrintServer1이라고 가정할 경우 전달됩니다 `\\\PrintSever1`.
   * 프린터 이름을 지정하는 문자열 값입니다. 예를 들어 프린터 이름이 Printer1이라고 가정할 경우 통과합니다 `\\\PrintSever1\Printer1`.

   >[!NOTE]
   >
   >버전 8.2.1에서 AEM Forms API에 이 `sendToPrinter` 메서드가 추가되었습니다.

### 웹 서비스 API를 사용하여 인쇄 스트림을 프린터로 보내기 {#send-a-print-stream-to-a-printer-using-the-web-service-api}

출력 API(웹 서비스)를 사용하여 인쇄 스트림을 네트워크 프린터로 보냅니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Forms `localhost` 를 호스팅하는 서버의 IP 주소로 대체합니다.

1. 출력 클라이언트 개체를 만듭니다.

   * 기본 생성자를 사용하여 `OutputServiceClient` 개체를 만듭니다.
   * 생성자를 사용하여 `OutputServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 속성을 사용할 필요는 `lc_version` 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다. 하지만 MTOM `?blob=mtom` 을 사용하도록 지정합니다.
   * 필드의 값을 `System.ServiceModel.BasicHttpBinding` 가져와 개체를 `OutputServiceClient.Endpoint.Binding` 만듭니다. 반환 값을 다음으로 캐스팅합니다 `BasicHttpBinding`.
   * 개체 `System.ServiceModel.BasicHttpBinding` 필드를 (으)로 `MessageEncoding` 설정합니다 `WSMessageEncoding.Mtom`. 이 값을 사용하면 MTOM이 사용됩니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM 양식 사용자 이름을 지정합니다 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 해당 암호 값을 필드에 지정합니다 `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 필드에 상수 값 `HttpClientCredentialType.Basic` 을 지정합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 필드에 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly` 을 지정합니다 `BasicHttpBindingSecurity.Security.Mode`.

1. XML 데이터 소스를 참조합니다.

   * 생성자를 사용하여 `BLOB` 개체를 만듭니다. 이 `BLOB` 개체는 양식 데이터를 저장하는 데 사용됩니다.
   * 생성자를 호출하여 `System.IO.FileStream` 개체를 만듭니다. 양식 데이터를 포함하는 XML 파일의 위치를 지정하는 문자열 값을 전달합니다.
   * 개체의 내용을 저장하는 바이트 배열을 `System.IO.FileStream` 만듭니다. 개체의 속성을 가져와 바이트 배열 길이를 `System.IO.FileStream` 결정합니다 `Length` .
   * 개체의 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열 `System.IO.FileStream` `Read` 을 스트림 데이터로 채웁니다.
   * 바이트 배열의 내용으로 해당 `BLOB` `MTOM` 필드를 할당하여 개체를 채웁니다.

1. 인쇄 런타임 옵션을 설정합니다.

   생성자를 사용하여 `PrintedOutputOptionsSpec` 개체를 만듭니다. 예를 들어 개체의 데이터 멤버에 대한 복사본 수를 나타내는 정수 값을 할당하여 인쇄할 복사본 수를 지정할 수 `PrintedOutputOptionsSpec` `copies` 있습니다.

   >[!NOTE]
   >
   >ZPL 인쇄 스트림을 생성하는 경우 `PrintedOutputOptionsSpec` 개체의 `pagination` 데이터 멤버를 사용하여 페이지 매김 값을 설정할 수 없습니다. 마찬가지로 ZPL 인쇄 스트림에 대해 다음 옵션을 설정할 수 없습니다. 출력 조그, 페이지 오프셋 및 스테이플. 데이터 `pagination` 멤버는 PostScript 생성에서 유효하지 않습니다. PCL 생성 전용입니다.

1. 인쇄할 문서를 검색합니다.

   * 개체의 메서드를 호출하고 다음 값을 전달하여 인쇄할 문서를 `OutputServiceService` `generatePrintedOutput` 검색합니다.

      * 인쇄 스트림을 지정하는 열거형 `PrintFormat` 값입니다. 예를 들어 PostScript 인쇄 스트림을 만들려면 전달하십시오 `PrintFormat.PostScript`.
      * 양식 디자인의 이름을 지정하는 문자열 값입니다.
      * 이미지 파일과 같은 관련 자료 파일의 위치를 지정하는 문자열 값.
      * 사용할 XDC 파일의 위치를 지정하는 문자열 값입니다.
      * 인쇄 스트림을 네트워크 프린터로 전송할 때 사용되는 인쇄 런타임 옵션이 포함된 `PrintedOutputOptionsSpec` 개체입니다.
      * 양식 데이터를 포함하는 XML 데이터 소스를 포함하는 `BLOB` 개체입니다.
      * 메서드로 채워지는 `BLOB` `generatePrintedOutput` 개체입니다. 이 `generatePrintedOutput` 메서드는 문서를 설명하는 생성된 메타데이터로 이 개체를 채웁니다. 이 매개 변수 값은 웹 서비스 호출에만 필요합니다.
      * 메서드로 채워지는 `BLOB` `generatePrintedOutput` 개체입니다. 이 `generatePrintedOutput` 개체는 결과 데이터로 채워집니다. 이 매개 변수 값은 웹 서비스 호출에만 필요합니다.
      * 작업 결과를 포함하는 `OutputResult` 개체입니다. 이 매개 변수 값은 웹 서비스 호출에만 필요합니다.
   * 개체 &#39;s 메서드 `BLOB` 의 값을 가져와 프린터로 전송할 개체를 `OutputResult` 만듭니다 `generatedDoc` . 이 메서드는 메서드에서 반환한 PostScript 데이터가 포함된 `BLOB` 개체를 `generatePrintedOutput` 반환합니다.


1. 인쇄 스트림을 네트워크 프린터로 보냅니다.

   개체의 메서드를 호출하고 다음 값을 전달하여 인쇄 스트림 `OutputClient` 을 네트워크 프린터로 `sendToPrinter` 보냅니다.

   * 프린터로 전송할 인쇄 스트림을 나타내는 `BLOB` 개체입니다.
   * 사용할 프린터 프로토콜을 지정하는 열거형 `PrinterProtocol` 값입니다. 예를 들어, SharedPrinter 프로토콜을 지정하려면 pass `PrinterProtocol.SharedPrinter`.
   * 이전 매개 변수 값을 사용할지 여부를 지정하는 `bool` 값입니다. 값을 전달합니다 `true`. 이 매개 변수 값은 웹 서비스 호출에만 필요합니다.
   * 인쇄 서버의 이름을 지정하는 문자열 값입니다. 예를 들어 인쇄 서버의 이름이 PrintServer1이라고 가정할 경우 전달됩니다 `\\\PrintSever1`.
   * 프린터 이름을 지정하는 문자열 값입니다. 예를 들어 프린터 이름이 Printer1이라고 가정할 경우 전달됩니다 `\\\PrintSever1\Printer1`.

   >[!NOTE]
   >
   >버전 8.2.1에서 AEM Forms API에 이 `sendToPrinter` 메서드가 추가되었습니다.

## 여러 출력 파일 만들기 {#creating-multiple-output-files}

출력 서비스는 XML 데이터 소스 또는 모든 레코드가 들어 있는 단일 파일에 대해 별도의 문서를 만들 수 있습니다(이 기능이 기본값입니다). 예를 들어, 10개의 레코드가 XML 데이터 소스 내에 있으며 출력 서비스가 출력 서비스 API를 사용하여 각 레코드에 대해 별도의 PDF 문서(또는 다른 출력 유형)를 생성하도록 했다고 가정합니다. 그 결과 출력 서비스는 10개의 PDF 문서를 생성합니다. 문서를 만드는 대신 여러 인쇄 스트림을 프린터로 보낼 수 있습니다.

다음 그림에서는 여러 개의 레코드가 포함된 XML 데이터 파일을 처리하는 Output service도 보여 줍니다. 그러나 출력 서비스가 모든 데이터 레코드가 포함된 단일 PDF 문서를 생성하도록 지시한다고 가정합니다. 이러한 경우 출력 서비스는 모든 레코드가 포함된 하나의 문서를 생성합니다.

다음 그림은 여러 레코드가 포함된 XML 데이터 파일을 처리하는 출력 서비스입니다. 출력 서비스가 각 데이터 레코드에 대해 별도의 PDF 문서를 생성하도록 했다고 가정해 보십시오. 이러한 경우 출력 서비스는 각 데이터 레코드에 대해 별도의 PDF 문서를 생성합니다.

![cm_outputbatchmany](assets/cm_outputbatchmany.png)

다음 XML 데이터는 3개의 데이터 레코드가 포함된 데이터 파일의 예를 보여줍니다.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <batch>
 <LoanRecord>
     <mortgageAmount>500000</mortgageAmount>
     <lastName>Blue</lastName>
     <firstName>Tony</firstName>
     <SSN>555666777</SSN>
     <PositionTitle>Product Manager</PositionTitle>
     <Address>555 No Where Dr</Address>
     <City>New York</City>
     <StateProv>New York</StateProv>
     <ZipCode>51256</ZipCode>
     <Email>TBlue@NoMailServer.com</Email>
     <PhoneNum>555-7418</PhoneNum>
     <FaxNum>555-9981</FaxNum>
     <Description>Buy a home</Description>
 </LoanRecord>
 <LoanRecord>
     <mortgageAmount>300000</mortgageAmount>
     <lastName>White</lastName>
     <firstName>Sam</firstName>
     <SSN>555666222</SSN>
     <PositionTitle>Program Manager</PositionTitle>
     <Address>557 No Where Dr</Address>
     <City>New York</City>
     <StateProv>New York</StateProv>
     <ZipCode>51256</ZipCode>
     <Email>SWhite@NoMailServer.com</Email>
     <PhoneNum>555-7445</PhoneNum>
     <FaxNum>555-9986</FaxNum>
     <Description>Buy a home</Description>
 </LoanRecord>
 <LoanRecord>
     <mortgageAmount>700000</mortgageAmount>
     <lastName>Green</lastName>
     <firstName>Steve</firstName>
     <SSN>55566688</SSN>
     <PositionTitle>Project Manager</PositionTitle>
     <Address>445 No Where Dr</Address>
     <City>New York</City>
     <StateProv>New York</StateProv>
     <ZipCode>51256</ZipCode>
     <Email>SGreeb@NoMailServer.com</Email>
     <PhoneNum>555-2211</PhoneNum>
     <FaxNum>555-2221</FaxNum>
     <Description>Buy a home</Description>
 </LoanRecord>
 </batch>
```

각 데이터 레코드를 시작하고 끝나는 XML 요소가 있습니다 `LoanRecord`. 이 XML 요소는 여러 파일을 생성하는 응용 프로그램 로직에서 참조합니다.

>[!NOTE]
>
>출력 서비스에 대한 자세한 내용은 AEM Forms에 대한 [서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-7}

XML 데이터 소스를 기반으로 여러 PDF 파일을 만들려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. 출력 클라이언트 개체를 만듭니다.
1. XML 데이터 소스를 참조합니다.
1. PDF 런타임 옵션을 설정합니다.
1. 렌더링 런타임 옵션을 설정합니다.
1. 여러 개의 PDF 파일을 생성할 수 있습니다.
1. 작업 결과를 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(AEM Forms이 JBoss에 배포된 경우 필요)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필요)

AEM Forms이 JBoss가 아닌 지원되는 J2EE 응용 프로그램 서버에 배포된 경우 adobe-utilities.jar 및 jbossall-client.jar 파일을 AEM Forms이 배포된 J2EE 응용 프로그램 서버에 고유한 JAR 파일로 대체해야 합니다.

**출력 클라이언트 개체 만들기**

출력 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 출력 서비스 클라이언트 개체를 만들어야 합니다. Java API를 사용하는 경우 `OutputClient` 개체를 만듭니다. 출력 웹 서비스 API를 사용하는 경우 `OutputServiceService` 개체를 만듭니다.

**XML 데이터 소스 참조**

여러 레코드가 포함된 XML 데이터 소스를 참조합니다. 데이터 레코드를 구분하는 데 XML 요소를 사용해야 합니다. 예를 들어 이 섹션 앞에 표시된 예제 XML 데이터 소스에서 데이터 레코드를 구분하는 XML 요소의 이름이 지정됩니다 `LoanRecord`.

데이터로 채울 모든 양식 필드에 대해 XML 요소가 있어야 합니다. XML 요소 이름은 필드 이름과 일치해야 합니다. XML 요소는 양식 필드에 해당되지 않거나 XML 요소 이름이 필드 이름과 일치하지 않는 경우 무시됩니다. 모든 XML 요소가 지정된 경우 XML 요소가 표시되는 순서와 일치할 필요는 없습니다.

**PDF 런타임 옵션 설정**

XML 데이터 소스를 기반으로 여러 파일을 성공적으로 만들려면 출력 서비스에 대해 다음 런타임 옵션을 설정해야 합니다.

* **많은 파일**: 출력 서비스에서 단일 문서를 만들지 또는 여러 문서를 만들지를 지정합니다. true 또는 false를 지정할 수 있습니다. XML 데이터 소스의 각 데이터 레코드에 대해 별도의 문서를 만들려면 true를 지정합니다.
* **파일 URI**: 출력 서비스가 생성하는 파일의 위치를 지정합니다. 예를 들어 C:\\Adobe\forms\Loan.pdf을 지정한다고 가정합니다. 이러한 경우 출력 서비스는 Loan.pdf라는 파일을 만들고 이 파일을 C:\\Adobe\forms folder폴더에 넣습니다. 여러 파일이 있는 경우 파일 이름은 Loan001.pdf, Loan0002.pdf, Loan003.pdf 등으로 구성됩니다. 파일 위치를 지정하면 클라이언트 컴퓨터가 아닌 서버에 파일이 배치됩니다.
* **레코드 이름**: 데이터 레코드를 구분하는 데이터 소스의 XML 요소 이름을 지정합니다. 예를 들어 이 섹션 앞에 표시된 예제 XML 데이터 소스에서 데이터 레코드를 구분하는 XML 요소를 호출합니다 `LoanRecord`. 레코드 이름 런타임 옵션을 설정하는 대신 데이터 레코드가 포함된 요소 수준을 나타내는 숫자 값을 지정하여 레코드 수준을 설정할 수 있습니다. 하지만 레코드 이름 또는 레코드 수준만 설정할 수 있습니다. 두 값을 모두 설정할 수는 없습니다.)

**렌더링 런타임 옵션 설정**

여러 파일을 만드는 동안 렌더링 런타임 옵션을 설정할 수 있습니다. 이러한 옵션은 필요하지 않지만(필요한 출력 런타임 옵션과 달리) 출력 서비스의 성능을 향상시키는 등의 작업을 수행할 수 있습니다. 예를 들어, 출력 서비스에서 사용하는 양식 디자인을 캐시하여 성능을 향상시킬 수 있습니다.

출력 서비스가 일괄 레코드를 처리할 때 여러 레코드가 포함된 데이터를 증분 방식으로 읽습니다. 즉, 출력 서비스는 데이터를 메모리로 읽어 레코드 일괄 처리가 진행될 때 데이터를 전송합니다. 두 개의 런타임 옵션 중 하나가 설정되면 출력 서비스는 데이터를 증분 방식으로 로드합니다. 레코드 이름 런타임 옵션을 설정하면 출력 서비스는 증분 방식으로 데이터를 읽습니다. 마찬가지로 [레코드 수준 런타임] 옵션을 2 이상으로 설정하면 출력 서비스는 증분 방식으로 데이터를 읽습니다.

출력 서비스가 객체의 메서드를 사용하여 증분 로드를 수행하는지 `PDFOutputOptionsSpec` 또는 `PrintedOutputOptionSpec` 객체의 `setLazyLoading` 방식을 사용하여 제어할 수 있습니다. 이 방법 `false` 으로 값을 전달하여 증분 로드를 끌 수 있습니다.

**여러 PDF 파일 생성**

여러 데이터 레코드가 포함된 유효한 XML 데이터 소스를 참조하고 런타임 옵션을 설정한 후 출력 서비스를 호출하여 여러 파일을 생성할 수 있습니다. 여러 레코드를 생성할 때 `OutputResult` 개체의 `getGeneratedDoc` 메서드가 반환됩니다 `null`.

**작업 결과 검색**

출력 서비스가 작업을 수행하면 작업이 성공했는지 여부를 지정하는 XML 데이터가 반환됩니다. 출력 서비스에서 다음 XML을 반환합니다. 이러한 경우 출력 서비스에서 42개의 문서를 생성했습니다.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <printResult>
 <status>0</status>
 <requestId>4ad85f9e2</requestId>
 <context/>
 <messages>
 <message>Printed all 42 records successfully.</message>
 </messages>
 <printSpec>
 <input>
 <validated>true</validated>
 <dataFile recordIdField="" recordLevel="0" recordName="LoanRecord"/>
 <sniffRules lookAhead="300"/>
 <formDesign>Loan.xdp</formDesign>
 <contentRoot>C:\Adobe</contentRoot>
 <metadata-spec record="false"/>
 </input>
 <output>
 <format>PDF</format>
 <fileURI>C:\Adobe\forms\Loan.pdf</fileURI>
 <optionString>cacheenabled=true&padebug=false&linearpdf=false&pdfarevisionnumber=1&pdfaconformance=A&taggedpdf=false&TransactionTimeOut=180</optionString>
 <waitForResponse>true</waitForResponse>
 <outputStream>multiple</outputStream>
 </output>
 </printSpec>
 </printResult>
```

**참고 항목**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[출력 서비스 API 빠른 시작](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java API를 사용하여 여러 PDF 파일 만들기 {#create-multiple-pdf-files-using-the-java-api}

출력 API(Java)를 사용하여 여러 개의 PDF 파일을 작성합니다.

1. 프로젝트 파일 포함&quot;

   Java 프로젝트의 클래스 경로에 adobe-output-client.jar와 같은 클라이언트 JAR 파일을 포함합니다. .

1. 출력 클라이언트 개체 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 개체를 `OutputClient` 만들고 개체를 `ServiceClientFactory` 전달합니다.

1. XML 데이터 소스 참조

   * 생성자를 사용하고 XML 파일의 위치를 지정하는 문자열 값을 전달하여 여러 레코드가 포함된 XML 데이터 소스를 나타내는 `java.io.FileInputStream` 객체를 만듭니다.
   * 생성자를 사용하여 개체를 `com.adobe.idp.Document` 만들고 개체를 `java.io.FileInputStream` 전달합니다.

1. PDF 런타임 옵션 설정

   * 생성자를 사용하여 `PDFOutputOptionsSpec` 개체를 만듭니다.
   * 개체의 메서드를 호출하여 [여러 파일] 옵션 `PDFOutputOptionsSpec` 을 `setGenerateManyFiles` 설정합니다. 예를 들어 값을 전달하여 출력 서비스 `true` 에서 XML 데이터 소스의 각 레코드에 대해 별도의 PDF 파일을 생성하도록 합니다. (전달하면 출력 서비스 `false`에서 모든 레코드가 포함된 단일 PDF 문서를 생성합니다.)
   * 개체의 메서드를 호출하고 출력 서비스가 생성하는 파일의 위치를 지정하는 문자열 값을 전달하여 파일 URI 옵션 `PDFOutputOptionsSpec` `setFileUri` 을 설정합니다. 파일 URI 옵션은 클라이언트 컴퓨터가 아닌 AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버를 기준으로 합니다.
   * 개체의 메서드를 호출하고 데이터 레코드를 구분하는 데이터 소스에서 XML 요소 이름을 지정하는 문자열 값을 전달하여 [ `OutputOptionsSpec` `setRecordName` 레코드 이름] 옵션을 설정합니다. 예를 들어 이 섹션 앞에 나와 있는 XML 데이터 소스를 고려해 보십시오. 데이터 레코드를 구분하는 XML 요소의 이름은 LoanRecord)입니다.

1. 렌더링 런타임 옵션 설정

   * 생성자를 사용하여 `RenderOptionsSpec` 개체를 만듭니다.
   * 개체의 값을 호출하고 전달하여 출력 서비스의 성능을 개선하기 위해 양식 디자인 `RenderOptionsSpec` 을 `setCacheEnabled` 캐시합니다 `Boolean` `true`.

1. 여러 PDF 파일 생성

   개체의 메서드를 호출하고 다음 값을 전달하여 여러 PDF 파일 `OutputClient` 을 `generatePDFOutput` 생성합니다.

   * 열거형 `TransformationFormat` 값입니다. PDF 문서를 생성하려면 을 지정합니다 `TransformationFormat.PDF`.
   * 양식 디자인의 이름을 지정하는 문자열 값입니다.
   * 양식 디자인이 있는 컨텐츠 루트를 지정하는 문자열 값입니다.
   * PDF 런타임 옵션이 포함된 `PDFOutputOptionsSpec` 개체
   * 렌더링 런타임 옵션이 포함된 `RenderOptionsSpec` 개체입니다.
   * 양식 디자인과 병합할 데이터가 들어 있는 XML 데이터 소스를 포함하는 `com.adobe.idp.Document` 개체입니다.

   이 `generatePDFOutput` 메서드는 작업 결과를 포함하는 `OutputResult` 개체를 반환합니다.

1. 작업 결과 검색

   * 메서드 결과를 포함할 XML 파일을 나타내는 `java.io.File` 객체를 `generatePDFOutput` 만듭니다. 파일 이름 확장자가 .xml인지 확인합니다.
   * 객체의 메서드를 호출하여 `com.adobe.idp.Document` 객체의 내용을 파일에 복사합니다(메서드에서 반환된 `copyToFile` 객체를 `com.adobe.idp.Document` `com.adobe.idp.Document` `applyUsageRights` 사용해야 함).

**참고 항목**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[빠른 시작(EJB 모드): Java API를 사용하여 여러 PDF 파일 만들기](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-multiple-pdf-files-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 여러 PDF 파일 작성 {#create-multiple-pdf-files-using-the-web-service-api}

출력 API(웹 서비스)를 사용하여 여러 개의 PDF 파일을 작성합니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Forms `localhost` 를 호스팅하는 서버의 IP 주소로 대체합니다.

1. 출력 클라이언트 개체를 만듭니다.

   * 기본 생성자를 사용하여 `OutputServiceClient` 개체를 만듭니다.
   * 생성자를 사용하여 `OutputServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 속성을 사용할 필요는 `lc_version` 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다. 하지만 MTOM `?blob=mtom` 을 사용하도록 지정합니다.
   * 필드의 값을 `System.ServiceModel.BasicHttpBinding` 가져와 개체를 `OutputServiceClient.Endpoint.Binding` 만듭니다. 반환 값을 다음으로 캐스팅합니다 `BasicHttpBinding`.
   * 개체 `System.ServiceModel.BasicHttpBinding` 필드를 (으)로 `MessageEncoding` 설정합니다 `WSMessageEncoding.Mtom`. 이 값을 사용하면 MTOM이 사용됩니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM 양식 사용자 이름을 지정합니다 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 해당 암호 값을 필드에 지정합니다 `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 필드에 상수 값 `HttpClientCredentialType.Basic` 을 지정합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 필드에 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly` 을 지정합니다 `BasicHttpBindingSecurity.Security.Mode`.

1. XML 데이터 소스를 참조합니다.

   * 생성자를 사용하여 `BLOB` 개체를 만듭니다. 이 `BLOB` 개체는 여러 레코드가 포함된 양식 데이터를 저장하는 데 사용됩니다.
   * 생성자를 호출하여 `System.IO.FileStream` 개체를 만듭니다. 여러 레코드가 포함된 XML 파일의 파일 위치를 나타내는 문자열 값을 전달합니다.
   * 개체의 내용을 저장하는 바이트 배열을 `System.IO.FileStream` 만듭니다. 개체의 속성을 가져와 바이트 배열의 크기를 결정할 수 `System.IO.FileStream` `Length` 있습니다.
   * 개체의 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열 `System.IO.FileStream` `Read` 을 스트림 데이터로 채웁니다.
   * 바이트 배열의 내용으로 해당 `BLOB` `MTOM` 필드를 할당하여 개체를 채웁니다.

1. PDF 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 `PDFOutputOptionsSpec` 개체를 만듭니다.
   * 개체의 데이터 멤버에 부울 값을 할당하여 [여러 파일] 옵션 `OutputOptionsSpec` 을 `generateManyFiles` 설정합니다. 예를 들어, 이 데이터 멤버 `true` 에 값을 할당하여 출력 서비스가 XML 데이터 소스의 각 레코드에 대해 별도의 PDF 파일을 만들도록 지시합니다. 이 데이터 멤버 `false` 에 할당하는 경우 출력 서비스는 모든 레코드가 포함된 단일 PDF를 생성합니다.
   * 출력 서비스가 생성하는 파일의 위치를 `OutputOptionsSpec` 개체의 데이터 멤버에 지정하는 문자열 값을 할당하여 파일 URI 옵션을 `fileURI` 설정합니다. 파일 URI 옵션은 클라이언트 컴퓨터가 아닌 AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버를 기준으로 합니다.
   * 데이터 레코드를 `OutputOptionsSpec` 개체의 데이터 `recordName` 멤버에 분리하는 데이터 소스에서 XML 요소 이름을 지정하는 문자열 값을 지정하여 레코드 이름 옵션을 설정합니다.
   * 출력 서비스가 객체의 데이터 멤버에 생성하는 복사본 수를 지정하는 정수 값을 할당하여 `OutputOptionsSpec` 복사 옵션을 `copies` 설정합니다.

1. 렌더링 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 `RenderOptionsSpec` 개체를 만듭니다.
   * 개체의 데이터 멤버에 값을 할당하여 출력 서비스의 성능 `true` 을 개선하기 위해 양식 디자인을 `RenderOptionsSpec` 캐시합니다 `cacheEnabled` .

1. 여러 개의 PDF 파일을 생성할 수 있습니다.

   개체의 `OutputServiceService` `generatePDFOutput`메서드를 호출하고 다음 값을 전달하여 여러 개의 PDF 파일을 만듭니다.

   * TransformationFormat 열거형 값. PDF 문서를 생성하려면 을 지정합니다 `TransformationFormat.PDF`.
   * 양식 디자인의 이름을 지정하는 문자열 값입니다.
   * 양식 디자인이 있는 컨텐츠 루트를 지정하는 문자열 값입니다.
   * PDF 런타임 옵션이 포함된 `PDFOutputOptionsSpec` 개체
   * 렌더링 런타임 옵션이 포함된 `RenderOptionsSpec` 개체입니다.
   * 양식 디자인과 병합할 데이터가 들어 있는 XML 데이터 소스를 포함하는 `BLOB` 개체입니다.
   * 메서드로 채워지는 `BLOB` `generatePDFOutput` 개체입니다. 이 `generatePDFOutput` 메서드는 문서를 설명하는 생성된 메타데이터로 이 개체를 채웁니다.
   * 메서드로 채워지는 `BLOB` `generatePDFOutput` 개체입니다. 이 `generatePDFOutput` 개체는 결과 데이터로 채워집니다.
   * 작업 결과를 포함하는 `OutputResult` 개체입니다.

1. 작업 결과 검색

   * 생성자를 호출하고 결과 데이터가 포함된 XML 파일 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다. 파일 이름 확장자가 .xml인지 확인합니다.
   * 개체의 메서드(8번째 매개 변수)로 결과 데이터로 채워진 `BLOB` 개체의 데이터 콘텐츠를 저장하는 `OutputServiceService` 바이트 `generatePDFOutput` 배열을 만듭니다. 개체 데이터 멤버의 값을 가져와 바이트 배열 `BLOB` 을 `binaryData` 채웁니다.
   * 생성자를 호출하고 개체를 전달하여 `System.IO.BinaryWriter` 개체를 `System.IO.FileStream` 만듭니다.
   * 개체의 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열 내용을 XML 파일에 `System.IO.BinaryWriter``Write` 씁니다.

**참고 항목**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 검색 규칙 만들기 {#creating-search-rules}

출력 서비스에서 입력 데이터를 검사하고 데이터 컨텐트를 기준으로 다른 양식 디자인을 사용하여 출력을 생성하는 검색 규칙을 만들 수 있습니다. 예를 들어 텍스트 *저당권이* 입력 데이터 내에 있는 경우 출력 서비스는 Modition.xdp라는 양식 디자인을 사용할 수 있습니다. 마찬가지로 텍스트 *자동차가* 입력 데이터에 있으면 출력 서비스는 AutomobileLoan.xdp로 저장된 양식 디자인을 사용할 수 있습니다. 출력 서비스는 다른 출력 유형을 생성할 수 있지만 이 섹션에서는 출력 서비스가 PDF 파일을 생성한다고 가정합니다. 다음 다이어그램은 XML 데이터 파일을 처리하고 많은 양식 디자인 중 하나를 사용하여 PDF 파일을 생성하는 출력 서비스입니다.

또한 출력 서비스는 문서 패키지를 생성할 수 있습니다. 이 경우 데이터 세트에서 여러 개의 레코드가 제공되고 각 레코드가 양식 디자인과 일치하며 하나의 문서가 여러 양식 디자인으로 구성됩니다.

![cs_outputbatchmanyformdesigns2](assets/cs_outputbatchmanyformdesigns2.png)

>[!NOTE]
>
>출력 서비스에 대한 자세한 내용은 AEM Forms에 대한 [서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-8}

문서를 생성하는 동안 출력 서비스가 검색 규칙을 사용하도록 지정하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. 출력 클라이언트 개체를 만듭니다.
1. XML 데이터 소스를 참조합니다.
1. 검색 규칙을 정의합니다.
1. PDF 런타임 옵션을 설정합니다.
1. 렌더링 런타임 옵션을 설정합니다.
1. PDF 문서를 생성합니다.
1. 작업 결과를 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

다음 JAR 파일을 프로젝트의 클래스 경로에 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(AEM Forms이 JBoss에 배포된 경우 필요)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필수)

AEM Forms이 JBoss가 아닌 지원되는 J2EE 응용 프로그램 서버에 배포된 경우 adobe-utilities.jar 및 jbossall-client.jar를 AEM Forms이 배포된 J2EE 응용 프로그램 서버에 고유한 JAR 파일로 교체해야 합니다.

**출력 클라이언트 개체 만들기**

출력 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 출력 서비스 클라이언트 개체를 만들어야 합니다.

**XML 데이터 소스 참조**

데이터로 채울 모든 양식 필드에 대해 XML 요소가 있어야 합니다. XML 요소 이름은 필드 이름과 일치해야 합니다. XML 요소는 양식 필드에 해당되지 않거나 XML 요소 이름이 필드 이름과 일치하지 않는 경우 무시됩니다. 모든 XML 요소가 지정된 한 XML 요소가 표시되는 순서와 일치할 필요는 없습니다.

**검색 규칙 정의**

검색 규칙을 정의하려면, 출력 서비스가 입력 데이터에서 검색하는 하나 이상의 텍스트 패턴을 정의합니다. 정의한 각 텍스트 패턴에 대해 텍스트 패턴이 있는 경우 사용되는 해당 양식 디자인을 지정합니다. 텍스트 패턴이 있는 경우 출력 서비스는 해당 양식 디자인을 사용하여 출력을 생성합니다. 텍스트 패턴의 예는 *저당이다*.

>[!NOTE]
>
>텍스트 패턴이 없으면 기본 양식이 사용됩니다. 사용하는 모든 양식 디자인이 컨텐츠 루트에 있는지 확인합니다.

**PDF 런타임 옵션 설정**

출력 서비스가 여러 양식 디자인을 기반으로 PDF 문서를 성공적으로 만들려면 다음 PDF 런타임 옵션을 설정합니다.

* **파일 URI**: 출력 서비스가 생성하는 PDF 파일의 이름과 위치를 지정합니다.
* **규칙**: 정의한 규칙을 지정합니다.
* **LookAHead**: 입력 데이터 파일의 시작부터 정의된 텍스트 패턴을 검색할 바이트 수를 지정합니다. 기본값은 500바이트입니다.

**렌더링 런타임 옵션 설정**

PDF 파일을 만드는 동안 렌더링 런타임 옵션을 설정할 수 있습니다. 이러한 옵션은 필요하지 않지만(PDF 런타임 옵션과 달리) 출력 서비스의 성능을 향상시키는 등의 작업을 수행할 수 있습니다. 예를 들어, 출력 서비스에서 사용하는 양식 디자인을 캐시하여 성능을 향상시킬 수 있습니다.

**PDF 문서 생성**

유효한 XML 데이터 소스를 참조하고 런타임 옵션을 설정한 후 출력 서비스를 호출하여 PDF 문서를 생성할 수 있습니다. 출력 서비스가 입력 데이터에서 지정된 텍스트 패턴을 찾으면 해당 양식 디자인을 사용합니다. 텍스트 패턴을 사용하지 않는 경우 출력 서비스는 기본 양식 디자인을 사용합니다.

**작업 결과 검색**

출력 서비스가 작업을 수행하면 작업이 성공했는지 여부를 지정하는 XML 데이터가 반환됩니다.

**참고 항목**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[출력 서비스 API 빠른 시작](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java API를 사용하여 검색 규칙 만들기 {#create-search-rules-using-the-java-api}

출력 API(Java)를 사용하여 검색 규칙을 만듭니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-output-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. 출력 클라이언트 개체를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 개체를 `OutputClient` 만들고 개체를 `ServiceClientFactory` 전달합니다.

1. XML 데이터 소스를 참조합니다.

   * 생성자를 사용하여 PDF 문서를 채우는 데 사용되는 XML 데이터 소스를 나타내는 `java.io.FileInputStream` 객체를 만들고 XML 파일의 위치를 지정하는 문자열 값을 전달합니다.
   * 생성자를 사용하여 개체를 `com.adobe.idp.Document` 만들고 개체를 `java.io.FileInputStream` 전달합니다.

1. 검색 규칙을 정의합니다.

   * 생성자를 사용하여 `Rule` 개체를 만듭니다.
   * 객체의 메서드를 호출하고 텍스트 패턴을 지정하는 문자열 값을 전달하여 `Rule` 텍스트 패턴을 `setPattern` 정의합니다.
   * 개체의 메서드를 호출하여 해당 양식 디자인을 `Rule` `setForm` 정의합니다. 양식 디자인의 이름을 지정하는 문자열 값을 전달합니다.

   >[!NOTE]
   >
   >정의할 각 텍스트 패턴에 대해 이전 세 개의 하위 단계를 반복합니다.

   * 생성자를 사용하여 `java.util.List` 개체를 `java.util.ArrayList` 만듭니다.
   * 만든 각 `Rule` 개체에 대해 `java.util.List` 개체의 `add` 메서드를 호출하고 `Rule` 개체를 전달합니다.


1. PDF 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 `PDFOutputOptionsSpec` 개체를 만듭니다.
   * 출력 서비스가 객체의 메서드를 호출하여 생성하는 PDF 파일의 이름과 위치를 `PDFOutputOptionsSpec` `setFileURI` 지정합니다. PDF 파일의 위치를 지정하는 문자열 값을 전달합니다. 파일 URI 옵션은 클라이언트 컴퓨터가 아닌 AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버를 기준으로 합니다.
   * 개체의 메서드를 호출하여 정의한 규칙을 `PDFOutputOptionsSpec` `setRules` 설정합니다. 개체가 `java.util.List` 포함된 개체를 `Rule` 전달합니다.
   * 개체의 메서드를 호출하여 정의된 텍스트 패턴을 검색할 바이트 수를 `PDFOutputOptionsSpec` `setLookAhead` 설정합니다. 바이트 수를 나타내는 정수 값을 전달합니다.

1. 렌더링 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 `RenderOptionsSpec` 개체를 만듭니다.
   * 개체의 호출과 전달을 통해 출력 서비스의 성능을 개선하기 위해 양식 디자인 `RenderOptionsSpec` 을 캐시합니다 `setCacheEnabled` `true`.

1. PDF 문서를 생성합니다.

   개체의 메서드를 호출하고 다음 값을 전달하여 여러 양식 디자인을 기반으로 하는 PDF 문서 `OutputClient` `generatePDFOutput` 를 생성합니다.

   * 열거형 `TransformationFormat` 값입니다. PDF 문서를 생성하려면 을 지정합니다 `TransformationFormat.PDF`.
   * 기본 양식 디자인의 이름을 지정하는 문자열 값. 즉, 텍스트 패턴이 없을 때 사용되는 양식 디자인입니다.
   * 양식 디자인이 있는 컨텐츠 루트를 지정하는 문자열 값입니다.
   * PDF 런타임 옵션이 포함된 `PDFOutputOptionsSpec` 개체
   * 렌더링 런타임 옵션이 포함된 `RenderOptionsSpec` 개체입니다.
   * 출력 서비스에서 정의된 텍스트 패턴에 대해 검색하는 양식 데이터가 포함된 `com.adobe.idp.Document` 객체입니다.

   이 `generatePDFOutput` 메서드는 작업 결과를 포함하는 `OutputResult` 개체를 반환합니다.

1. 작업 결과를 검색합니다.

   * 개체의 메서드를 호출하여 메서드 `com.adobe.idp.Document` 의 상태를 나타내는 `generatePDFOutput` 개체를 `OutputResult` `getStatusDoc` 만듭니다.
   * 작업 결과를 포함할 `java.io.File` 개체를 만듭니다. 파일 확장자가 .xml인지 확인합니다.
   * 객체의 메서드를 호출하여 `com.adobe.idp.Document` 객체의 내용을 파일에 복사합니다(메서드에서 반환된 `copyToFile` 객체를 `com.adobe.idp.Document` `com.adobe.idp.Document` `getStatusDoc` 사용해야 함).

**참고 항목**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[빠른 시작(EJB 모드): Java API를 사용하여 검색 규칙 만들기](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[빠른 시작(SOAP 모드): Java API를 사용하여 검색 규칙 만들기](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 검색 규칙 만들기 {#create-search-rules-using-the-web-service-api}

출력 API(웹 서비스)를 사용하여 검색 규칙을 만듭니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Forms `localhost` 를 호스팅하는 서버의 IP 주소로 대체합니다.

1. 출력 클라이언트 개체를 만듭니다.

   * 기본 생성자를 사용하여 `OutputServiceClient` 개체를 만듭니다.
   * 생성자를 사용하여 `OutputServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 속성을 사용할 필요는 `lc_version` 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다. 하지만 MTOM `?blob=mtom` 을 사용하도록 지정합니다.
   * 필드의 값을 `System.ServiceModel.BasicHttpBinding` 가져와 개체를 `OutputServiceClient.Endpoint.Binding` 만듭니다. 반환 값을 다음으로 캐스팅합니다 `BasicHttpBinding`.
   * 개체 `System.ServiceModel.BasicHttpBinding` 필드를 (으)로 `MessageEncoding` 설정합니다 `WSMessageEncoding.Mtom`. 이 값을 사용하면 MTOM이 사용됩니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM 양식 사용자 이름을 지정합니다 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 해당 암호 값을 필드에 지정합니다 `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 필드에 상수 값 `HttpClientCredentialType.Basic` 을 지정합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 필드에 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly` 을 지정합니다 `BasicHttpBindingSecurity.Security.Mode`.

1. XML 데이터 소스를 참조합니다.

   * 생성자를 사용하여 `BLOB` 개체를 만듭니다. 이 `BLOB` 개체는 PDF 문서와 병합할 데이터를 저장하는 데 사용됩니다.
   * 생성자를 호출하고 암호화할 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * 개체의 내용을 저장하는 바이트 배열을 `System.IO.FileStream` 만듭니다. 개체의 속성을 가져와 바이트 배열의 크기를 결정할 수 `System.IO.FileStream` `Length` 있습니다.
   * 개체의 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열 `System.IO.FileStream` `Read` 을 스트림 데이터로 채웁니다.
   * 바이트 배열의 내용으로 해당 `BLOB` `MTOM` 필드를 할당하여 개체를 채웁니다.

1. 검색 규칙을 정의합니다.

   * 생성자를 사용하여 `Rule` 개체를 만듭니다.
   * 개체의 데이터 멤버에 텍스트 패턴을 지정하는 문자열 값을 할당하여 `Rule` 텍스트 패턴을 `pattern` 정의합니다.
   * 개체의 데이터 멤버에 양식 디자인을 지정하는 문자열 값을 지정하여 해당 양식 디자인을 `Rule` 정의합니다 `form` .

   >[!NOTE]
   >
   >정의할 각 텍스트 패턴에 대해 이전 세 개의 하위 단계를 반복합니다.

   * 규칙을 저장하는 `MyArrayOf_xsd_anyType` 개체를 만듭니다.
   * 각 `Rule` 개체를 `MyArrayOf_xsd_anyType` 배열의 요소에 할당합니다. 각 개체에 대해 `MyArrayOf_xsd_anyType` 개체의 `Add` 메서드를 `Rule` 호출합니다.


1. PDF 런타임 옵션 설정

   * 생성자를 사용하여 `PDFOutputOptionsSpec` 개체를 만듭니다.
   * 출력 서비스가 생성하는 PDF 파일의 위치를 개체의 데이터 멤버에 지정하는 문자열 값을 지정하여 파일 URI 옵션을 `PDFOutputOptionsSpec` 설정합니다 `fileURI` . 파일 URI 옵션은 클라이언트 컴퓨터가 아닌 AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버를 기준으로 합니다.
   * 출력 서비스가 객체의 데이터 멤버에 생성하는 복사본 수를 지정하는 정수 값을 할당하여 `PDFOutputOptionsSpec` 복사 옵션을 `copies` 설정합니다.
   * 규칙을 저장하는 `MyArrayOf_xsd_anyType` 객체를 `PDFOutputOptionsSpec` 객체의 데이터 멤버에 할당하여 정의한 규칙을 `rules` 설정합니다.
   * 개체의 데이터 메서드에 검색할 바이트 수를 나타내는 정수 값을 할당하여 정의된 텍스트 패턴을 검색할 바이트 수를 `PDFOutputOptionsSpec` 설정합니다 `lookAhead` .

1. 렌더링 런타임 옵션 설정

   * 생성자를 사용하여 `RenderOptionsSpec` 개체를 만듭니다.
   * 개체의 데이터 멤버에 값을 할당하여 출력 서비스의 성능을 개선하기 위해 양식 디자인 `true` 을 `RenderOptionsSpec` 캐시합니다 `cacheEnabled` .

   >[!NOTE]
   >
   >입력 문서가 Acrobat 양식인 경우 `RenderOptionsSpec` 개체의 `pdfVersion` 구성원을 사용하여 PDF 문서 버전을 설정할 수 없습니다. 출력 PDF 문서는 Acrobat 양식의 PDF 버전을 유지합니다. 마찬가지로 입력 문서가 Acrobat 양식인 경우 `RenderOptionsSpec` 개체의 `taggedPDF` 방법을 사용하여 태그 지정된 PDF 옵션을 설정할 수 없습니다.

   >[!NOTE]
   >
   >입력 PDF 문서가 인증되거나 디지털 서명된 경우 `RenderOptionsSpec` 개체의 `linearizedPDF` 구성원을 사용하여 선형화된 PDF 옵션을 설정할 수 없습니다. 자세한 내용은 PDF 문서 [디지털 서명을 참조하십시오](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).

1. PDF 문서 생성

   개체의 `OutputServiceService` `generatePDFOutput`메서드를 호출하고 다음 값을 전달하여 PDF 문서를 만듭니다.

   * 열거형 `TransformationFormat` 값입니다. PDF 문서를 생성하려면 을 지정합니다 `TransformationFormat.PDF`.
   * 양식 디자인의 이름을 지정하는 문자열 값입니다.
   * 양식 디자인이 있는 컨텐츠 루트를 지정하는 문자열 값입니다.
   * PDF 런타임 옵션이 포함된 `PDFOutputOptionsSpec` 개체
   * 렌더링 런타임 옵션이 포함된 `RenderOptionsSpec` 개체입니다.
   * 양식 디자인과 병합할 데이터가 들어 있는 XML 데이터 소스를 포함하는 `BLOB` 개체입니다.
   * 메서드로 채워지는 `BLOB` `generatePDFOutput` 개체입니다. 이 `generatePDFOutput` 메서드는 문서를 설명하는 생성된 메타데이터로 이 개체를 채웁니다. 이 매개 변수 값은 웹 서비스 호출에만 필요합니다.
   * 메서드로 채워지는 `BLOB` `generatePDFOutput` 개체입니다. 이 `generatePDFOutput` 개체는 결과 데이터로 채워집니다. 이 매개 변수 값은 웹 서비스 호출에만 필요합니다.
   * 작업 결과를 포함하는 `OutputResult` 개체입니다. 이 매개 변수 값은 웹 서비스 호출에만 필요합니다.

   >[!NOTE]
   >
   >방법을 호출하여 PDF 문서를 생성하는 경우 서명, 인증 또는 사용 권한이 있는 XFA PDF 양식과 데이터를 병합할 수 없다는 점을 `generatePDFOutput` 알아야 합니다. 사용 권한에 대한 자세한 내용은 PDF 문서에 [사용 권한 적용을 참조하십시오](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).

1. 작업 결과 검색

   * 생성자를 호출하고 결과 데이터가 포함된 XML 파일 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다. 파일 확장자가 XML인지 확인합니다.
   * 개체의 메서드(8번째 매개 변수)로 결과 데이터로 채워진 `BLOB` 개체의 데이터 콘텐츠를 저장하는 `OutputServiceService` 바이트 `generatePDFOutput` 배열을 만듭니다. 개체 데이터 멤버의 값을 가져와 바이트 배열 `BLOB` 을 `MTOM` 채웁니다.
   * 생성자를 호출하고 개체를 전달하여 `System.IO.BinaryWriter` 개체를 `System.IO.FileStream` 만듭니다.
   * 개체의 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열 내용을 XML 파일에 `System.IO.BinaryWriter``Write` 씁니다.

**참고 항목**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## PDF 문서 병합 {#flattening-pdf-documents}

출력 서비스를 사용하여 대화형 PDF 문서를 비대화형 PDF로 변환할 수 있습니다. 인터랙티브한 PDF 문서를 사용하면 PDF 문서 필드에 있는 데이터를 입력하거나 수정할 수 있습니다. 대화형 PDF 문서를 비대화형 PDF 문서로 변환하는 과정을 *병합이라고 합니다*. PDF 문서를 병합할 때 사용자는 문서 필드의 데이터를 수정할 수 없습니다. PDF 문서를 병합하는 한 가지 이유는 데이터를 수정할 수 없기 때문입니다.

다음과 같은 유형의 PDF 문서를 병합할 수 있습니다.

* 인터랙티브한 XFA PDF 문서
* Acrobat Forms

비대화형 PDF 문서인 PDF를 병합하려고 하면 예외가 발생합니다.

>[!NOTE]
>
>출력 서비스에 대한 자세한 내용은 AEM Forms에 대한 [서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-9}

대화형 PDF 문서를 비대화형 PDF 문서로 병합하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. 출력 클라이언트 개체를 만듭니다.
1. 인터랙티브한 PDF 문서 검색
1. PDF 문서 변환
1. 비대화형 PDF 문서를 PDF 파일로 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(AEM Forms이 JBoss에 배포된 경우 필요)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필요)

AEM Forms이 JBoss가 아닌 지원되는 J2EE 응용 프로그램 서버에 배포된 경우 adobe-utilities.jar 및 jbossall-client.jar 파일을 AEM Forms이 배포된 J2EE 응용 프로그램 서버에 고유한 JAR 파일로 대체해야 합니다. 모든 AEM Forms JAR 파일의 위치에 대한 자세한 내용은 AEM Forms Java 라이브러리 파일 [포함을 참조하십시오](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**출력 클라이언트 개체 만들기**

출력 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 출력 서비스 클라이언트 개체를 만들어야 합니다. Java API를 사용하는 경우 `OutputClient` 개체를 만듭니다. 출력 웹 서비스 API를 사용하는 경우 `OutputServiceService` 개체를 만듭니다.

**인터랙티브한 PDF 문서 검색**

비대화형 PDF 문서로 변환할 인터랙티브한 PDF 문서를 검색할 수 있습니다. 비대화형 PDF 문서를 변환하려고 하면 예외가 발생합니다.

**PDF 문서 변환**

인터랙티브한 PDF 문서를 검색한 후 인터랙티브한 PDF 문서가 아닌 문서로 변환할 수 있습니다. 출력 서비스는 비대화형 PDF 문서를 반환합니다.

**비대화형 PDF 문서를 PDF 파일로 저장**

비대화형 PDF 문서를 PDF 파일로 저장할 수 있습니다.

**참고 항목**

[Java API를 사용하여 PDF 문서 분리](creating-document-output-streams.md#flatten-a-pdf-document-using-the-java-api)

[웹 서비스 API를 사용하여 PDF 문서 분리](creating-document-output-streams.md#flatten-a-pdf-document-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[출력 서비스 API 빠른 시작](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java API를 사용하여 PDF 문서 분리 {#flatten-a-pdf-document-using-the-java-api}

Output API(Java)를 사용하여 대화형 PDF 문서를 비대화형 PDF 문서로 병합합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-output-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. 출력 클라이언트 개체를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 개체를 `OutputClient` 만들고 개체를 `ServiceClientFactory` 전달합니다.

1. 인터랙티브한 PDF 문서 검색

   * 생성자를 사용하고 인터랙티브한 PDF 파일의 위치를 지정하는 문자열 값을 전달하여 변형할 대화형 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만듭니다.
   * 생성자를 사용하여 개체를 `com.adobe.idp.Document` 만들고 개체를 `java.io.FileInputStream` 전달합니다.

1. PDF 문서 변환

   개체의 방법을 호출하고 다음 값을 전달하여 대화형 PDF 문서를 비대화형 PDF 문서로 `OutputServiceService` `transformPDF` 변환합니다.

   * 인터랙티브한 PDF 문서를 포함하는 `com.adobe.idp.Document` 개체입니다.
   * 열거형 `TransformationFormat` 값입니다. 비대화형 PDF 문서를 생성하려면 을 지정합니다 `TransformationFormat.PDF`.
   * 개정 번호를 지정하는 `PDFARevisionNumber` 열거형 값. 이 매개 변수는 PDF/A 문서를 위한 것이기 때문에 지정할 수 있습니다 `null`.
   * 개정 번호와 연도를 나타내는 문자열 값으로서 콜론으로 구분됩니다. 이 매개 변수는 PDF/A 문서를 위한 것이기 때문에 지정할 수 있습니다 `null`.
   * PDF/A 적합성 수준을 나타내는 열거형 값. `PDFAConformance` 이 매개 변수는 PDF/A 문서를 위한 것이기 때문에 지정할 수 있습니다 `null`.

   이 방법 `transformPDF` 은 비대화형 PDF 문서를 포함하는 `com.adobe.idp.Document` 개체를 반환합니다.

1. 비대화형 PDF 문서를 PDF 파일로 저장합니다.

   * 객체를 만들고 파일 이름 확장자가 .pdf인지 확인합니다. `java.io.File`
   * 객체의 메서드를 호출하여 `Document` 객체의 내용을 파일에 복사합니다(메서드에서 반환된 `copyToFile` 객체를 `Document` `Document` `transformPDF` 사용해야 함).

**참고 항목**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[빠른 시작(EJB 모드): Java API를 사용하여 PDF 문서 변환](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[빠른 시작(SOAP 모드): Java API를 사용하여 PDF 문서 변환](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 PDF 문서 분리 {#flatten-a-pdf-document-using-the-web-service-api}

Output API(웹 서비스)를 사용하여 대화형 PDF 문서를 비대화형 PDF 문서로 병합합니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Forms `localhost` 를 호스팅하는 서버의 IP 주소로 대체합니다.

1. 출력 클라이언트 개체를 만듭니다.

   * 기본 생성자를 사용하여 `OutputServiceClient` 개체를 만듭니다.
   * 생성자를 사용하여 `OutputServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 속성을 사용할 필요는 `lc_version` 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다. 하지만 MTOM `?blob=mtom` 을 사용하도록 지정합니다.
   * 필드의 값을 `System.ServiceModel.BasicHttpBinding` 가져와 개체를 `OutputServiceClient.Endpoint.Binding` 만듭니다. 반환 값을 다음으로 캐스팅합니다 `BasicHttpBinding`.
   * 개체 `System.ServiceModel.BasicHttpBinding` 필드를 (으)로 `MessageEncoding` 설정합니다 `WSMessageEncoding.Mtom`. 이 값을 사용하면 MTOM이 사용됩니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM 양식 사용자 이름을 지정합니다 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 해당 암호 값을 필드에 지정합니다 `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 필드에 상수 값 `HttpClientCredentialType.Basic` 을 지정합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 필드에 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly` 을 지정합니다 `BasicHttpBindingSecurity.Security.Mode`.

1. 인터랙티브한 PDF 문서 검색

   * 생성자를 사용하여 `BLOB` 개체를 만듭니다. 이 `BLOB` 개체는 대화형 PDF 문서를 저장하는 데 사용됩니다.
   * 생성자를 호출하고 대화형 PDF 문서의 파일 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * 개체의 내용을 저장하는 바이트 배열을 `System.IO.FileStream` 만듭니다. 개체의 속성을 가져와 바이트 배열의 크기를 결정할 수 `System.IO.FileStream` `Length` 있습니다.
   * 개체의 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열 `System.IO.FileStream` `Read` 을 스트림 데이터로 채웁니다.
   * 바이트 배열의 컨텐츠로 해당 `BLOB` `MTOM` 속성을 지정하여 개체를 채웁니다.

1. PDF 문서 변환

   개체의 방법을 호출하고 다음 값을 전달하여 대화형 PDF 문서를 비대화형 PDF 문서로 `OutputClient` `transformPDF` 변환합니다.

   * 인터랙티브한 PDF 문서를 포함하는 `BLOB` 오브젝트입니다.
   * 열거형 `TransformationFormat` 값입니다. 비대화형 PDF 문서를 생성하려면 을 지정합니다 `TransformationFormat.PDF`.
   * 개정 번호를 지정하는 `PDFARevisionNumber` 열거형 값.
   * 열거형 값의 사용 여부를 지정하는 `PDFARevisionNumber` 부울 값. 이 매개 변수는 PDF/A 문서를 위한 것이기 때문에 지정할 수 있습니다 `false`.
   * 개정 번호와 연도를 나타내는 문자열 값으로서 콜론으로 구분됩니다. 이 매개 변수는 PDF/A 문서를 위한 것이기 때문에 지정할 수 있습니다 `null`.
   * PDF/A 적합성 수준을 나타내는 열거형 값. `PDFAConformance`
   * 열거형 값의 사용 여부를 지정하는 `PDFAConformance` 부울 값. 이 매개 변수는 PDF/A 문서를 위한 것이기 때문에 지정할 수 있습니다 `false`.

   이 방법 `transformPDF` 은 비대화형 PDF 문서를 포함하는 `BLOB` 개체를 반환합니다.

1. 비대화형 PDF 문서를 PDF 파일로 저장합니다.

   * 생성자를 호출하고 비대화형 PDF 문서의 파일 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * 메서드에서 반환된 개체의 데이터 내용을 저장하는 바이트 배열을 `BLOB` `transformPDF` 만듭니다. 개체 데이터 멤버의 값을 가져와 바이트 배열 `BLOB` 을 `MTOM` 채웁니다.
   * 생성자를 호출하고 개체를 전달하여 `System.IO.BinaryWriter` 개체를 `System.IO.FileStream` 만듭니다.
   * 개체의 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 PDF 파일 `System.IO.BinaryWriter` `Write` 에 씁니다.

**참고 항목**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
