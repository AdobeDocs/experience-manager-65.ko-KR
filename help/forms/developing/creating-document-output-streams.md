---
title: 문서 출력 스트림 만들기
seo-title: 문서 출력 스트림 만들기
description: 출력 서비스를 사용하여 문서를 PDF(PDF/A 문서 포함), PostScript, PCL(Printer Control Language) 및 Zebra - ZPL, Intermec - IPL, Datamax - DPL 및 TecToshiba - TPCL 레이블 형식으로 변환합니다.
seo-description: 출력 서비스를 사용하여 문서를 PDF(PDF/A 문서 포함), PostScript, PCL(Printer Control Language) 및 Zebra - ZPL, Intermec - IPL, Datamax - DPL 및 TecToshiba - TPCL 레이블 형식으로 변환합니다.
uuid: 80c28efa-35ce-4073-9ca6-2d93bcd67fdd
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: de527d50-991b-4ca3-a8ac-44d5cab988e9
role: Developer
exl-id: a521bfac-f417-4002-9c5c-8d7794d3eec7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '19044'
ht-degree: 0%

---

# 문서 출력 스트림 만들기 {#creating-document-output-streams}

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms용입니다.**

**출력 서비스 정보**

출력 서비스를 사용하여 문서를 PDF(PDF/A 문서 포함), PostScript, Printer Control Language(PCL) 및 다음 레이블 형식으로 출력할 수 있습니다.

* 제브라 - ZPL
* 인터페이스 - IPL
* Datamax - DPL
* TecToshiba - TPCL

출력 서비스를 사용하여 XML 양식 데이터를 양식 디자인과 병합하고 문서를 네트워크 프린터 또는 파일로 출력할 수 있습니다.

양식 디자인(XDP 파일)을 출력 서비스에 전달할 수 있는 방법에는 두 가지가 있습니다. 양식 디자인이 포함된 `com.adobe.idp.Document` 인스턴스를 출력 서비스에 전달할 수 있습니다. 또는 양식 디자인의 위치를 지정하는 URI 값을 전달할 수 있습니다. 이 두 방법 모두 *AEM Forms*&#x200B;로 프로그래밍에 설명되어 있습니다.

>[!NOTE]
>
>출력 서비스는 응용 프로그램 개체 특정 스크립트가 포함된 Acrobat PDF 문서를 지원하지 않습니다. 응용 프로그램 개체 특정 스크립트가 포함된 양식 PDF 문서는 렌더링되지 않습니다.

다음 섹션에서는 URI 값을 사용하여 양식 디자인을 출력 서비스에 전달하는 방법을 보여 줍니다.

* [PDF 문서 만들기](creating-document-output-streams.md#creating-pdf-documents)
* [PDF/A 문서 만들기](creating-document-output-streams.md#creating-pdf-a-documents)

다음 섹션에서는 `com.adobe.idp.Document` 인스턴스 내에서 양식 디자인을 전달하는 방법을 보여 줍니다.

* [컨텐츠 서비스에 있는 문서(더 이상 사용되지 않음)를 출력 서비스에 전달](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [조각을 사용하여 PDF 문서 만들기](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

사용할 기술을 결정할 때 고려해야 할 사항은 다른 AEM Forms 서비스에서 양식 디자인을 가져온 다음 `com.adobe.idp.Document` 인스턴스 내에 전달하는 것입니다. *출력 서비스에 문서 전달* 및 *조각을 사용하여 PDF 문서 작성* 섹션에서는 모두 다른 AEM Forms 서비스에서 양식 디자인을 가져오는 방법을 보여줍니다. 첫 번째 섹션은 Content Services에서 양식 디자인을 검색합니다(더 이상 사용되지 않음). 두 번째 섹션은 어셈블러 서비스에서 양식 디자인을 검색합니다.

파일 시스템과 같은 고정된 위치에서 양식 디자인을 가져오는 경우 두 방법 중 하나를 사용할 수 있습니다. 즉, XDP 파일에 URI 값을 지정하거나 `com.adobe.idp.Document` 인스턴스를 사용할 수 있습니다.

PDF 문서를 만들 때 양식 디자인 위치를 지정하는 URI 값을 전달하려면 `generatePDFOutput` 메서드를 사용합니다. 마찬가지로 PDF 문서를 만들 때 `com.adobe.idp.Document` 인스턴스를 출력 서비스에 전달하려면 `generatePDFOutput2` 메서드를 사용합니다.

출력 스트림을 네트워크 프린터로 보낼 때 두 방법 중 하나를 사용할 수도 있습니다. 양식 디자인이 포함된 `com.adobe.idp.Document` 인스턴스를 전달하여 출력 스트림을 프린터로 보내려면 `sendToPrinter2` 메서드를 사용합니다. URI 값을 전달하여 출력 스트림을 프린터로 보내려면 `sendToPrinter`메서드를 사용합니다. *프린터로 인쇄 스트림 보내기* 섹션에서는 `sendToPrinter` 메서드를 사용합니다.

출력 서비스를 사용하여 다음 작업을 수행할 수 있습니다.

* [PDF 문서 만들기](creating-document-output-streams.md#creating-pdf-documents)
* [PDF/A 문서 만들기](creating-document-output-streams.md#creating-pdf-a-documents)
* [컨텐츠 서비스에 있는 문서(더 이상 사용되지 않음)를 출력 서비스에 전달](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [조각을 사용하여 PDF 문서 만들기](creating-document-output-streams.md#creating-pdf-documents-using-fragments)
* [파일로 인쇄](creating-document-output-streams.md#printing-to-files)
* [프린터로 인쇄 스트림 보내기](creating-document-output-streams.md#sending-print-streams-to-printers)
* [여러 출력 파일 만들기](creating-document-output-streams.md#creating-multiple-output-files)
* [검색 규칙 만들기](creating-document-output-streams.md#creating-search-rules)
* [PDF 문서 병합](creating-document-output-streams.md#flattening-pdf-documents)

>[!NOTE]
>
>출력 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

## PDF 문서 만들기 {#creating-pdf-documents}

출력 서비스를 사용하여 제공된 양식 디자인 및 XML 양식 데이터를 기반으로 하는 PDF 문서를 만들 수 있습니다. 출력 서비스에서 만든 PDF 문서는 대화형 PDF 문서가 아닙니다.사용자는 양식 데이터를 입력하거나 수정할 수 없습니다.

장기 보관을 위한 PDF 문서를 만들려면 PDF/A 문서를 만드는 것이 좋습니다. ([PDF/A 문서 작성](creating-document-output-streams.md#creating-pdf-a-documents)을 참조하십시오.)

사용자가 데이터를 입력할 수 있는 대화형 PDF 양식을 만들려면 Forms 서비스를 사용하십시오. ( [대화형 PDF forms 렌더링](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms) 참조).

>[!NOTE]
>
>출력 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary-of-steps}

PDF 문서를 만들려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. 출력 클라이언트 개체를 만듭니다.
1. XML 데이터 소스를 참조합니다.
1. PDF 런타임 옵션을 설정합니다.
1. 렌더링 런타임 옵션을 설정합니다.
1. PDF 문서를 생성합니다.
1. 작업의 결과를 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함하십시오. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

다음 JAR 파일을 프로젝트의 클래스 경로에 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms이 JBoss에 배포되는 경우 필수)

AEM Forms이 JBoss가 아닌 지원되는 J2EE 애플리케이션 서버에 배포되는 경우 adobe-utilities.jar 및 jbossall-client.jar 파일을 AEM Forms이 배포된 J2EE 애플리케이션 서버와 관련된 JAR 파일로 대체해야 합니다.

**출력 클라이언트 개체 만들기**

출력 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 출력 서비스 클라이언트 개체를 만들어야 합니다. Java API를 사용하는 경우 `OutputClient` 개체를 만듭니다. 출력 웹 서비스 API를 사용하는 경우 `OutputServiceService` 개체를 만듭니다.

**XML 데이터 소스 참조**

데이터를 양식 디자인과 병합하려면 데이터가 포함된 XML 데이터 소스를 참조해야 합니다. 데이터로 채우려는 모든 양식 필드에 대해 XML 요소가 있어야 합니다. XML 요소 이름은 필드 이름과 일치해야 합니다. XML 요소는 양식 필드에 해당하지 않거나 XML 요소 이름이 필드 이름과 일치하지 않는 경우에는 무시됩니다. 모든 XML 요소가 지정된 경우 XML 요소가 표시되는 순서와 일치하지 않아도 됩니다.

다음 예제 대출 신청 양식을 고려하십시오.

![cp_cp_loanformdata](assets/cp_cp_loanformdata.png)

데이터를 이 양식 디자인에 병합하려면 양식에 해당하는 XML 데이터 소스를 만들어야 합니다. 다음 XML은 예제 모기지 응용 프로그램 양식에 해당하는 XDP XML 데이터 소스를 나타냅니다.

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

PDF 문서를 만들 때 파일 URI 옵션을 설정합니다. 이 옵션은 출력 서비스에서 생성하는 PDF 파일의 이름과 위치를 지정합니다.

>[!NOTE]
>
>파일 URI 런타임 옵션을 설정하는 대신 출력 서비스에서 반환하는 복잡한 데이터 유형에서 프로그래밍 방식으로 PDF 문서를 검색할 수 있습니다. 그러나 파일 URI 런타임 옵션을 설정하면 프로그래밍 방식으로 PDF 문서를 검색하는 응용 프로그램 논리를 만들 필요가 없습니다.

**렌더링 런타임 옵션 설정**

PDF 문서를 만들 때 렌더링 런타임 옵션을 설정할 수 있습니다. 이러한 옵션이 필요하지 않지만(필요한 PDF 런타임 옵션과 달리) 출력 서비스의 성능 향상과 같은 작업을 수행할 수 있습니다. 예를 들어 출력 서비스에서 성능을 개선하기 위해 사용하는 양식 디자인을 캐시할 수 있습니다.

태그가 지정된 Acrobat 양식을 입력으로 사용하는 경우 출력 서비스 Java 또는 웹 서비스 API를 사용하여 태그가 지정된 설정을 해제할 수 없습니다. 이 옵션을 `false`로 프로그래밍 방식으로 설정하려고 하면 결과 PDF 문서에 여전히 태그가 지정됩니다.

>[!NOTE]
>
>렌더링 런타임 옵션을 지정하지 않으면 기본값이 사용됩니다. 런타임 옵션 렌더링에 대한 자세한 내용은 `RenderOptionsSpec` 클래스 참조를 참조하십시오. ( [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en) 참조).

**PDF 문서 생성**

양식 데이터가 포함된 유효한 XML 데이터 소스를 참조하고 런타임 옵션을 설정한 후에는 출력 서비스를 호출하여 PDF 문서를 생성할 수 있습니다.

PDF 문서를 생성할 때 출력 서비스에서 PDF 문서를 만드는 데 필요한 URI 값을 지정합니다. 양식 디자인은 서버 파일 시스템과 같은 위치 또는 AEM Forms 애플리케이션의 일부로 저장할 수 있습니다. 컨텐츠 루트 URI 값 `repository:///`을 사용하여 Forms 애플리케이션의 일부로 존재하는 양식 디자인(또는 이미지 파일 등의 기타 리소스)을 참조할 수 있습니다. 예를 들어, *Applications/FormsApplication*&#x200B;라는 Forms 애플리케이션 내에 있는 *Loan.xdp*&#x200B;라는 양식 디자인을 생각해 보십시오.

![cp_cp_formrepository](assets/cp_cp_formrepository.png)

이전 그림에서 표시된 Loan.xdp 파일에 액세스하려면 `repository:///Applications/FormsApplication/1.0/FormsFolder/`을 `OutputClient` 개체의 `generatePDFOutput` 메서드에 전달된 세 번째 매개 변수로 지정합니다. 양식 이름(*Loan.xdp*)을 `OutputClient` 개체의 `generatePDFOutput` 메서드에 전달된 두 번째 매개 변수로 지정합니다.

XDP 파일에 이미지(또는 조각과 같은 기타 리소스)가 포함된 경우 리소스를 XDP 파일과 동일한 애플리케이션 폴더에 넣습니다. AEM Forms에서는 컨텐츠 루트 URI를 기본 경로로 사용하여 이미지에 대한 참조를 확인합니다. 예를 들어 Loan.xdp 파일에 이미지가 포함되어 있는 경우 이미지를 `Applications/FormsApplication/1.0/FormsFolder/`에 배치해야 합니다.

>[!NOTE]
>
>`OutputClient` 개체의 `generatePDFOutput` 또는 `generatePrintedOutput` 메서드를 호출할 때 Forms 애플리케이션 URI를 참조할 수 있습니다.

>[!NOTE]
>
>Forms 응용 프로그램에 있는 XDP를 참조하여 PDF 문서를 생성하는 전체 빠른 시작을 보려면 [빠른 시작(EJB 모드)을 참조하십시오.Java API](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api)를 사용하여 애플리케이션 XDP 파일을 기반으로 PDF 문서 만들기

**작업 결과 검색**

출력 서비스에서 작업을 수행하면 작업이 성공했는지 여부를 지정하는 상태 XML 데이터와 같은 다양한 데이터 항목이 반환됩니다.

**참고 항목**

[Java API를 사용하여 PDF 문서 만들기](creating-document-output-streams.md#create-a-pdf-document-using-the-java-api)

[웹 서비스 API를 사용하여 PDF 문서 만들기](creating-document-output-streams.md#create-a-pdf-document-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[출력 서비스 API 빠른 시작](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java API {#create-a-pdf-document-using-the-java-api}를 사용하여 PDF 문서 만들기

출력 API(Java)를 사용하여 PDF 문서를 만듭니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-output-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. 출력 클라이언트 개체를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 `OutputClient` 개체를 만들고 `ServiceClientFactory` 개체를 전달합니다.

1. XML 데이터 소스를 참조합니다.

   * 생성자를 사용하여 PDF 문서를 채우고 XML 파일의 위치를 지정하는 문자열 값을 전달하여 PDF 문서를 채우는 데 사용되는 XML 데이터 소스를 나타내는 `java.io.FileInputStream` 개체를 만듭니다.
   * 생성자를 사용하여 `com.adobe.idp.Document` 개체를 만듭니다. `java.io.FileInputStream` 개체를 전달합니다.

1. PDF 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 `PDFOutputOptionsSpec` 개체를 만듭니다.
   * `PDFOutputOptionsSpec` 개체의 `setFileURI` 메서드를 호출하여 파일 URI 옵션을 설정합니다. 출력 서비스에서 생성하는 PDF 파일의 위치를 지정하는 문자열 값을 전달합니다. 파일 URI 옵션은 클라이언트 컴퓨터가 아닌 AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버에 상대적입니다.

1. 렌더링 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 `RenderOptionsSpec` 개체를 만듭니다.
   * 양식 디자인을 캐시하여 `RenderOptionsSpec` 개체의 `setCacheEnabled`을 호출하고 `true`를 전달하여 출력 서비스의 성능을 개선합니다.

   >[!NOTE]
   >
   >입력 문서가 Acrobat 양식(Acrobat에서 만든 양식) 또는 서명 또는 인증된 XFA 문서인 경우 `RenderOptionsSpec` 개체의 `setPdfVersion` 메서드를 사용하여 PDF 문서 버전을 설정할 수 없습니다. 출력 PDF 문서는 원본 PDF 버전을 유지합니다. 마찬가지로, 입력 문서가 Acrobat 양식이거나 서명된 XFA 문서이거나 인증된 XFA 문서인 경우 `RenderOptionsSpec` 개체의 `setTaggedPDF` 메서드를 호출하여 태그가 지정된 Adobe PDF 옵션을 설정할 수 없습니다.

   >[!NOTE]
   >
   >입력 PDF 문서가 인증되거나 디지털 서명된 경우 `RenderOptionsSpec` 개체의 `setLinearizedPDF` 메서드를 사용하여 선형화된 PDF 옵션을 설정할 수 없습니다. ([PDF 문서에 디지털 서명&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*참조)*

1. PDF 문서를 생성합니다.

   `OutputClient` 개체의 `generatePDFOutput` 메서드를 호출하고 다음 값을 전달하여 PDF 문서를 만듭니다.

   * `TransformationFormat` 열거형 값입니다. PDF 문서를 생성하려면 `TransformationFormat.PDF`을 지정합니다.
   * 양식 디자인의 이름을 지정하는 문자열 값입니다.
   * 양식 디자인이 있는 컨텐츠 루트를 지정하는 문자열 값입니다.
   * PDF 런타임 옵션이 포함된 `PDFOutputOptionsSpec` 개체입니다.
   * 렌더링 런타임 옵션이 포함된 `RenderOptionsSpec` 개체입니다.
   * 양식 디자인과 병합할 데이터가 포함된 XML 데이터 소스가 포함된 `com.adobe.idp.Document` 개체입니다.

   `generatePDFOutput` 메서드는 작업 결과를 포함하는 `OutputResult` 개체를 반환합니다.

   >[!NOTE]
   >
   >`generatePDFOutput` 메서드를 호출하여 PDF 문서를 생성하는 경우 서명되거나 인증된 XFA PDF 양식과 데이터를 병합할 수 없습니다. ([디지털 서명 및 인증 문서&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*참조)*

   >[!NOTE]
   >
   >`OutputResult` 개체의 `getRecordLevelMetaDataList` 메서드는 `null`*를 반환합니다.*

   >[!NOTE]
   >
   >`OutputClient` 개체의 `generatePDFOutput2` 메서드를 호출하여 PDF 문서를 만들 수도 있습니다. ([컨텐츠 서비스에 있는 문서 전달(더 이상 사용되지 않음)을 출력 서비스&#x200B;](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*에 참조하십시오.)*

1. 작업의 결과를 검색합니다.

   * `OutputResult` 개체의 `getStatusDoc` 메서드를 호출하여 `generatePDFOutput` 작업의 상태를 나타내는 `com.adobe.idp.Document` 개체를 검색합니다. 이 메서드는 작업의 성공 여부를 지정하는 상태 XML 데이터를 반환합니다.
   * 작업 결과가 포함된 `java.io.File` 개체를 만듭니다. 파일 이름 확장명이 .xml인지 확인합니다.
   * `com.adobe.idp.Document` 개체의 `copyToFile` 메서드를 호출하여 `com.adobe.idp.Document` 개체의 내용을 파일에 복사합니다. `getStatusDoc` 메서드에서 반환된 `com.adobe.idp.Document` 개체를 사용해야 합니다.

   출력 서비스는 `PDFOutputOptionsSpec` 개체의 `setFileURI` 메서드에 전달된 인수에 의해 지정된 위치에 PDF 문서를 쓰지만, `OutputResult` 개체의 `getGeneratedDoc` 메서드를 호출하여 프로그래밍 방식으로 PDF/A 문서를 검색할 수 있습니다.

**참고 항목**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[빠른 시작(EJB 모드):Java API를 사용하여 PDF 문서 만들기](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 PDF 문서 만들기](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API {#create-a-pdf-document-using-the-web-service-api}를 사용하여 PDF 문서 만들기

출력 API(웹 서비스)를 사용하여 PDF 문서를 만듭니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다.`http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`

   >[!NOTE]
   >
   >`localhost` 을 AEM Forms을 호스팅하는 서버의 IP 주소로 바꿉니다.

1. 출력 클라이언트 개체를 만듭니다.

   * 기본 생성자를 사용하여 `OutputServiceClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `OutputServiceClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/OutputService?blob=mtom`). `lc_version` 특성을 사용할 필요는 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다. 그러나 MTOM을 사용하려면 `?blob=mtom`을 지정하십시오.
   * `OutputServiceClient.Endpoint.Binding` 필드의 값을 가져와서 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * AEM Forms 사용자 이름을 `OutputServiceClient.ClientCredentials.UserName.UserName` 필드에 지정합니다.
      * 해당 암호 값을 `OutputServiceClient.ClientCredentials.UserName.Password` 필드에 할당합니다.
      * 상수 값 `HttpClientCredentialType.Basic`을 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.
      * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. XML 데이터 소스를 참조합니다.

   * 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 PDF 문서와 병합될 XML 데이터를 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하고 양식 데이터가 포함된 XML 파일의 파일 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하고 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * `MTOM` 필드를 바이트 배열의 콘텐츠로 할당하여 `BLOB` 개체를 채웁니다.

1. PDF 런타임 옵션 설정

   * 생성자를 사용하여 `PDFOutputOptionsSpec` 개체를 만듭니다.
   * 출력 서비스에서 생성하는 PDF 파일의 위치를 `PDFOutputOptionsSpec` 개체의 `fileURI` 데이터 멤버에 지정하는 문자열 값을 할당하여 파일 URI 옵션을 설정합니다. 파일 URI 옵션은 클라이언트 컴퓨터가 아닌 AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버에 상대적입니다.

1. 렌더링 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 `RenderOptionsSpec` 개체를 만듭니다.
   * 양식 디자인을 캐시하여 `true` 값을 `RenderOptionsSpec` 개체의 `cacheEnabled` 데이터 멤버에 할당하여 출력 서비스의 성능을 향상시킵니다.

   >[!NOTE]
   >
   >입력 문서가 Acrobat 양식(Acrobat에서 만든 양식) 또는 서명 또는 인증된 XFA 문서인 경우 `RenderOptionsSpec` 개체의 `setPdfVersion` 메서드를 사용하여 PDF 문서 버전을 설정할 수 없습니다. 출력 PDF 문서는 원본 PDF 버전을 유지합니다. 마찬가지로, 입력 문서가 Acrobat 양식이거나 서명된 XFA 문서이거나 인증된 XFA 문서인 경우 `RenderOptionsSpec` 개체의 `setTaggedPDF`* 메서드를 호출하여 태그가 지정된 Adobe PDF 옵션을 설정할 수 없습니다.*

   >[!NOTE]
   >
   >입력 PDF 문서가 인증되거나 디지털 서명된 경우 `RenderOptionsSpec` 개체의 `linearizedPDF` 멤버를 사용하여 선형화된 PDF 옵션을 설정할 수 없습니다. ([PDF 문서에 디지털 서명&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*참조)*

1. PDF 문서를 생성합니다.

   `OutputServiceService` 개체의 `generatePDFOutput` 메서드를 호출하고 다음 값을 전달하여 PDF 문서를 만듭니다.

   * `TransformationFormat` 열거형 값입니다. PDF 문서를 생성하려면 `TransformationFormat.PDF`을 지정합니다.
   * 양식 디자인의 이름을 지정하는 문자열 값입니다.
   * 양식 디자인이 있는 컨텐츠 루트를 지정하는 문자열 값입니다.
   * PDF 런타임 옵션이 포함된 `PDFOutputOptionsSpec` 개체입니다.
   * 렌더링 런타임 옵션이 포함된 `RenderOptionsSpec` 개체입니다.
   * 양식 디자인과 병합할 데이터가 포함된 XML 데이터 소스가 포함된 `BLOB` 개체입니다.
   * `generatePDFOutput` 메서드로 채워지는 `BLOB` 개체입니다. `generatePDFOutput` 메서드는 이 개체를 문서를 설명하는 생성된 메타데이터로 채웁니다. (이 매개 변수 값은 웹 서비스 호출에만 필요합니다.)
   * `generatePDFOutput` 메서드로 채워지는 `BLOB` 개체입니다. `generatePDFOutput` 메서드는 이 개체를 결과 데이터로 채웁니다. (이 매개 변수 값은 웹 서비스 호출에만 필요합니다.)
   * 작업 결과를 포함하는 `OutputResult` 개체입니다. (이 매개 변수 값은 웹 서비스 호출에만 필요합니다.)

   >[!NOTE]
   >
   >`generatePDFOutput` 메서드를 호출하여 PDF 문서를 생성하는 경우 서명되거나 인증된 XFA PDF 양식과 데이터를 병합할 수 없습니다. ([디지털 서명 및 인증 문서&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*참조)*

   >[!NOTE]
   >
   >`OutputClient` 개체의 `generatePDFOutput2` 메서드를 호출하여 PDF 문서를 만들 수도 있습니다. ([컨텐츠 서비스에 있는 문서 전달(더 이상 사용되지 않음)을 출력 서비스&#x200B;](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*에 참조하십시오.)*

1. 작업의 결과를 검색합니다.

   * 해당 생성자를 호출하고 결과 데이터가 포함된 XML 파일 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다. 파일 이름 확장명이 .xml인지 확인합니다.
   * `OutputServiceService` 개체의 `generatePDFOutput` 메서드(8번째 매개 변수)로 결과 데이터로 채워지는 `BLOB` 개체의 데이터 콘텐츠를 저장하는 바이트 배열을 만듭니다. `BLOB` 개체의 `MTOM` `field` 값을 가져와서 바이트 배열을 채웁니다.
   * 해당 생성자를 호출하고 `System.IO.FileStream` 개체를 전달하여 `System.IO.BinaryWriter` 개체를 만듭니다.
   * `System.IO.BinaryWriter` 개체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 XML 파일에 씁니다.

   참고 항목

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

   >[!NOTE]
   >
   >`OutputServiceService` 개체의 `generateOutput` 메서드는 더 이상 사용되지 않습니다.

## PDF/A 문서 만들기 {#creating-pdf-a-documents}

출력 서비스를 사용하여 PDF/A 문서를 만들 수 있습니다. PDF/A는 문서의 컨텐츠를 장기간 보존하기 위한 보관 형식이므로 모든 글꼴이 포함되고 파일의 압축이 해제됩니다. 따라서 PDF/A 문서는 일반적으로 표준 PDF 문서보다 큽니다. 또한 PDF/A 문서에는 오디오 및 비디오 컨텐츠가 포함되어 있지 않습니다. 다른 출력 서비스 작업과 마찬가지로 양식 디자인과 데이터를 모두 제공하여 PDF/A 문서를 만들 수 있습니다.

PDF/A-1 사양은 a와 b라는 두 가지 적합성 수준으로 구성됩니다.두 가지 간의 주요 차이점은 적합성 수준 b에 필요하지 않은 논리 구조(액세서빌러티) 지원과 관련되어 있습니다.적합성 수준에 관계없이 PDF/A-1은 생성된 PDF/A 문서에 모든 글꼴이 포함되도록 지시합니다.

PDF/A는 PDF 문서 보관의 표준이지만 표준 PDF 문서가 회사의 요구 사항에 맞는 경우 보관에 PDF/A를 사용해야 하는 것은 아닙니다. PDF/A 표준은 문서 보존 요구 사항을 충족하면서 장기간 저장할 수 있는 PDF 파일을 설정하는 데 목적이 있습니다. 예를 들어, 시간이 지남에 따라 URL이 유효하지 않을 수 있으므로 URL을 PDF/A에 포함할 수 없습니다.

조직은 자체 요구 사항, 문서 보존 기간, 파일 크기 고려 사항을 평가하고 자체 아카이빙 전략을 결정해야 합니다. DocConverter 서비스를 사용하여 PDF 문서가 PDF/A 호환인지 프로그래밍 방식으로 확인할 수 있습니다. ([프로그래밍 방식으로 PDF/A 규정 준수 결정](/help/forms/developing/pdf-a-documents.md#programmatically-determining-pdf-a-compliancy) 참조)

PDF/A 문서는 양식 디자인에 지정된 글꼴을 사용해야 하며 글꼴은 대체할 수 없습니다. 따라서 OS(호스트 운영 체제)에서 PDF 문서 내에 있는 글꼴을 사용할 수 없으면 예외가 발생합니다.

Acrobat에서 PDF/A 문서를 열면 다음 그림과 같이 문서가 PDF/A 문서임을 확인하는 메시지가 표시됩니다.

![cp_cp_pdfamessage](assets/cp_cp_pdfamessage.png)

>[!NOTE]
>
>AIIM 웹 사이트에는 [https://www.aiim.org/documents/standards/19005-1_FAQ.pdf](https://www.aiim.org/documents/standards/19005-1_FAQ.pdf)에서 액세스할 수 있는 PDF/A FAQ 섹션이 있습니다.

>[!NOTE]
>
>출력 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary_of_steps-1}

PDF/A 문서를 만들려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. 출력 클라이언트 개체를 만듭니다.
1. XML 데이터 소스를 참조합니다.
1. PDF/A 런타임 옵션을 설정합니다.
1. 렌더링 런타임 옵션을 설정합니다.
1. PDF/A 문서를 생성합니다.
1. 작업의 결과를 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 사용자 지정 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함하십시오. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms이 JBoss에 배포되는 경우 필수)

AEM Forms이 JBoss가 아닌 지원되는 J2EE 애플리케이션 서버에 배포되는 경우 adobe-utilities.jar 및 jbossall-client.jar 파일을 AEM Forms이 배포된 J2EE 애플리케이션 서버와 관련된 JAR 파일로 대체해야 합니다.

**출력 클라이언트 개체 만들기**

출력 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 출력 서비스 클라이언트 개체를 만들어야 합니다. Java API를 사용하는 경우 `OutputClient` 개체를 만듭니다. 출력 웹 서비스 API를 사용하는 경우 `OutputServiceService` 개체를 만듭니다.

**XML 데이터 소스 참조**

데이터를 양식 디자인과 병합하려면 데이터가 포함된 XML 데이터 소스를 참조해야 합니다. 데이터로 채울 모든 양식 필드에 대해 XML 요소가 있어야 합니다. XML 요소 이름은 필드 이름과 일치해야 합니다. XML 요소는 양식 필드에 해당하지 않거나 XML 요소 이름이 필드 이름과 일치하지 않는 경우에는 무시됩니다. 모든 XML 요소가 지정된 경우 XML 요소가 표시되는 순서와 일치하지 않아도 됩니다.

**PDF/A 런타임 옵션 설정**

PDF/A 문서를 만들 때 파일 URI 옵션을 설정할 수 있습니다. URI는 AEM Forms을 호스팅하는 J2EE 애플리케이션 서버를 기준으로 합니다. 즉, C:\Adobe을 설정하면 클라이언트 컴퓨터가 아닌 서버의 폴더에 파일이 기록됩니다. URI는 출력 서비스에서 생성하는 PDF/A 파일의 이름과 위치를 지정합니다.

**렌더링 런타임 옵션 설정**

PDF/A 문서를 만들 때 렌더링 런타임 옵션을 설정할 수 있습니다. 설정할 수 있는 두 개의 PDF/A 관련 옵션은 `PDFAConformance` 및 `PDFARevisionNumber` 값입니다. `PDFAConformance` 값은 PDF 문서가 장기간 전자 문서가 보존되는 요구 사항을 준수하는 방법을 나타냅니다. 이 옵션의 유효한 값은 `A` 및 `B`입니다. 레벨 a 및 b 적합성에 대한 자세한 내용은 *ISO 19005-1 문서 관리*&#x200B;라는 이름의 PDF/A-1 ISO 사양을 참조하십시오.

`PDFARevisionNumber` 값은 PDF/A 문서의 개정 번호를 나타냅니다. PDF/A 문서의 개정 번호에 대한 자세한 내용은 *ISO 19005-1 문서 관리*&#x200B;라는 이름의 PDF/A-1 ISO 사양을 참조하십시오.

>[!NOTE]
>
>PDF/A 1A 문서를 만들 때 태그가 지정된 Adobe PDF 옵션을 `false`(으)로 설정할 수 없습니다. PDF/A 1A는 항상 태그가 지정된 PDF 문서입니다. 또한 PDF/A 1B 문서를 만들 때 태그가 지정된 Adobe PDF 옵션을 `true`(으)로 설정할 수도 없습니다. PDF/A 1B는 항상 태그가 지정되지 않은 PDF 문서입니다.

**PDF/A 문서 생성**

양식 데이터가 포함된 유효한 XML 데이터 소스를 참조하고 런타임 옵션을 설정한 후에는 출력 서비스를 호출하여 PDF/A 문서를 생성할 수 있습니다.

**작업 결과 검색**

출력 서비스에서 작업을 수행하면 작업이 성공했는지 여부를 지정하는 XML 데이터와 같은 다양한 데이터 항목이 반환됩니다.

**참고 항목**

[Java API를 사용하여 PDF/A 문서 만들기](creating-document-output-streams.md#create-a-pdf-a-document-using-the-java-api)

[웹 서비스 API를 사용하여 PDF/A 문서 만들기](creating-document-output-streams.md#create-a-pdf-a-document-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[출력 서비스 API 빠른 시작](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java API {#create-a-pdf-a-document-using-the-java-api}를 사용하여 PDF/A 문서를 만듭니다

출력 API(Java)를 사용하여 PDF/A 문서를 만듭니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-output-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. 출력 클라이언트 개체를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 `OutputClient` 개체를 만들고 `ServiceClientFactory` 개체를 전달합니다.

1. XML 데이터 소스를 참조합니다.

   * 해당 생성자를 사용하여 PDF/A 문서를 채우고 XML 파일의 위치를 지정하는 문자열 값을 전달하여 PDF/A 문서를 채우는 데 사용되는 XML 데이터 소스를 나타내는 `java.io.FileInputStream` 개체를 만듭니다.
   * 생성자를 사용하여 `com.adobe.idp.Document` 개체를 만들고 `java.io.FileInputStream` 개체를 전달합니다.

1. PDF/A 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 `PDFOutputOptionsSpec` 개체를 만듭니다.
   * `PDFOutputOptionsSpec` 개체의 `setFileURI` 메서드를 호출하여 파일 URI 옵션을 설정합니다. 출력 서비스에서 생성하는 PDF 파일의 위치를 지정하는 문자열 값을 전달합니다. 파일 URI 옵션은 클라이언트 컴퓨터가 아닌 AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버에 상대적입니다.

1. 렌더링 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 `RenderOptionsSpec` 개체를 만듭니다.
   * `RenderOptionsSpec` 개체의 `setPDFAConformance` 메서드를 호출하고 적합성 수준을 지정하는 `PDFAConformance` 열거형 값을 전달하여 `PDFAConformance` 값을 설정합니다. 예를 들어 적합성 수준 A를 지정하려면 `PDFAConformance.A`를 전달합니다.
   * `RenderOptionsSpec` 개체의 `setPDFARevisionNumber` 메서드를 호출하고 `PDFARevisionNumber.Revision_1` 메서드를 전달하여 `PDFARevisionNumber` 값을 설정합니다.

   >[!NOTE]
   >
   >PDF/A 문서의 PDF 버전은 `RenderOptionsSpec` 개체의 `setPdfVersion`*메서드에 대해 지정한 값에 관계없이 1.4입니다.*

1. PDF/A 문서를 생성합니다.

   `OutputClient` 개체의 `generatePDFOutput` 메서드를 호출하고 다음 값을 전달하여 PDF/A 문서를 만듭니다.

   * `TransformationFormat` 열거형 값입니다. PDF/A 문서를 생성하려면 `TransformationFormat.PDFA`을 지정합니다.
   * 양식 디자인의 이름을 지정하는 문자열 값입니다.
   * 양식 디자인이 있는 컨텐츠 루트를 지정하는 문자열 값입니다.
   * PDF 런타임 옵션이 포함된 `PDFOutputOptionsSpec` 개체입니다.
   * 렌더링 런타임 옵션이 포함된 `RenderOptionsSpec` 개체입니다.
   * 양식 디자인과 병합할 데이터가 포함된 XML 데이터 소스가 포함된 `com.adobe.idp.Document` 개체입니다.

   `generatePDFOutput` 메서드는 작업 결과를 포함하는 `OutputResult` 개체를 반환합니다.

   >[!NOTE]
   >
   >`OutputResult` 개체의 `getRecordLevelMetaDataList` 메서드는 `null`를 반환합니다.

   >[!NOTE]
   >
   >`OutputClient` 개체의 `generatePDFOutput`2 메서드를 호출하여 PDF/A 문서를 만들 수도 있습니다. ([컨텐츠 서비스에 있는 문서 전달(더 이상 사용되지 않음)을 출력 서비스](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)에 참조하십시오.)

1. 작업의 결과를 검색합니다.

   * `OutputResult` 개체의 `getStatusDoc` 메서드를 호출하여 `generatePDFOutput` 메서드의 상태를 나타내는 `com.adobe.idp.Document` 개체를 만듭니다.
   * 작업 결과를 포함할 `java.io.File` 개체를 만듭니다. 파일 이름 확장명이 .xml인지 확인합니다.
   * `com.adobe.idp.Document` 개체의 `copyToFile` 메서드를 호출하여 `com.adobe.idp.Document` 개체의 내용을 파일에 복사합니다. `getStatusDoc` 메서드에서 반환된 `com.adobe.idp.Document` 개체를 사용해야 합니다.

   >[!NOTE]
   >
   >출력 서비스는 PDF/A 문서를 `PDFOutputOptionsSpec` 개체의 `setFileURI` 메서드에 전달된 인수에 의해 지정된 위치에 기록하지만, `OutputResult` 개체의 `getGeneratedDoc` 메서드를 호출하여 프로그래밍 방식으로 PDF/A 문서를 검색할 수 있습니다.

**참고 항목**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[빠른 시작(SOAP 모드):Java API를 사용하여 PDF/A 문서 만들기](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-a-document-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성을 설정합니다](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### 웹 서비스 API {#create-a-pdf-a-document-using-the-web-service-api}를 사용하여 PDF/A 문서를 만듭니다

출력 API(웹 서비스)를 사용하여 PDF/A 문서를 만듭니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다.`http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`

   >[!NOTE]
   >
   >`localhost` 을 AEM Forms을 호스팅하는 서버의 IP 주소로 바꿉니다.

1. 출력 클라이언트 개체를 만듭니다.

   * 기본 생성자를 사용하여 `OutputServiceClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `OutputServiceClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/OutputService?blob=mtom`). `lc_version` 특성을 사용할 필요는 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다. 그러나 MTOM을 사용하려면 `?blob=mtom`을 지정하십시오.
   * `OutputServiceClient.Endpoint.Binding` 필드의 값을 가져와서 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * AEM Forms 사용자 이름을 `OutputServiceClient.ClientCredentials.UserName.UserName` 필드에 지정합니다.
      * 해당 암호 값을 `OutputServiceClient.ClientCredentials.UserName.Password` 필드에 할당합니다.
      * 상수 값 `HttpClientCredentialType.Basic`을 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.
      * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. XML 데이터 소스를 참조합니다.

   * 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 PDF/A 문서에 병합될 데이터를 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하고 암호화할 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하고 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * `MTOM` 필드를 바이트 배열 콘텐츠로 할당하여 `BLOB` 개체를 채웁니다.

1. PDF/A 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 `PDFOutputOptionsSpec` 개체를 만듭니다.
   * 출력 서비스에서 생성하는 PDF 파일의 위치를 `PDFOutputOptionsSpec` 개체의 `fileURI` 데이터 멤버에 지정하는 문자열 값을 할당하여 파일 URI 옵션을 설정합니다. 파일 URI 옵션은 클라이언트 컴퓨터가 아니라 AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버에 상대적입니다

1. 렌더링 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 `RenderOptionsSpec` 개체를 만듭니다.
   * `PDFAConformance` 열거형 값을 `RenderOptionsSpec` 개체의 `PDFAConformance` 데이터 멤버에 할당하여 `PDFAConformance` 값을 설정합니다. 예를 들어 적합성 수준 A를 지정하려면 이 데이터 멤버에 `PDFAConformance.A`을 할당합니다.
   * `PDFARevisionNumber` 열거형 값을 `RenderOptionsSpec` 개체의 `PDFARevisionNumber` 데이터 멤버에 할당하여 `PDFARevisionNumber` 값을 설정합니다. 이 데이터 멤버에 `PDFARevisionNumber.Revision_1`을(를) 할당합니다.

   >[!NOTE]
   >
   >PDF/A 문서의 PDF 버전은 지정한 값에 관계없이 1.4입니다.

1. PDF/A 문서를 생성합니다.

   `OutputServiceService` 개체의 `generatePDFOutput` 메서드를 호출하고 다음 값을 전달하여 PDF 문서를 만듭니다.

   * TransformationFormat 열거형 값입니다. PDF 문서를 생성하려면 `TransformationFormat.PDFA`을 지정합니다.
   * 양식 디자인의 이름을 지정하는 문자열 값입니다.
   * 양식 디자인이 있는 컨텐츠 루트를 지정하는 문자열 값입니다.
   * PDF 런타임 옵션이 포함된 `PDFOutputOptionsSpec` 개체입니다.
   * 렌더링 런타임 옵션이 포함된 `RenderOptionsSpec` 개체입니다.
   * 양식 디자인과 병합할 데이터가 포함된 XML 데이터 소스가 포함된 `BLOB` 개체입니다.
   * `generatePDFOutput` 메서드로 채워지는 `BLOB` 개체입니다. `generatePDFOutput` 메서드는 이 개체를 문서를 설명하는 생성된 메타데이터로 채웁니다. (이 매개 변수 값은 웹 서비스 호출에만 필요합니다.)
   * `generatePDFOutput` 메서드로 채워지는 `BLOB` 개체입니다. `generatePDFOutput` 메서드는 이 개체를 결과 데이터로 채웁니다. (이 매개 변수 값은 웹 서비스 호출에만 필요합니다.)
   * 작업 결과를 포함하는 `OutputResult` 개체입니다. (이 매개 변수 값은 웹 서비스 호출에만 필요합니다.)

   >[!NOTE]
   >
   >`OutputClient` 개체의 `generatePDFOutput`2 메서드를 호출하여 PDF/A 문서를 만들 수도 있습니다. ([컨텐츠 서비스에 있는 문서 전달(더 이상 사용되지 않음)을 출력 서비스](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)에 참조하십시오.)

1. 작업의 결과를 검색합니다.

   * 해당 생성자를 호출하고 결과 데이터가 포함된 XML 파일 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다. 파일 이름 확장명이 .xml인지 확인합니다.
   * `OutputServiceService` 개체의 `generatePDFOutput` 메서드(8번째 매개 변수)로 결과 데이터로 채워지는 `BLOB` 개체의 데이터 콘텐츠를 저장하는 바이트 배열을 만듭니다. `BLOB` 개체의 `MTOM` 필드 값을 가져와서 바이트 배열을 채웁니다.
   * 해당 생성자를 호출하고 `System.IO.FileStream` 개체를 전달하여 `System.IO.BinaryWriter` 개체를 만듭니다.
   * `System.IO.BinaryWriter` 개체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 XML 파일에 씁니다.

**참고 항목**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 컨텐츠 서비스에 있는 문서(더 이상 사용되지 않음)를 출력 서비스 {#passing-documents-located-in-content-services-deprecated-to-the-output-service}에 전달

출력 서비스는 일반적으로 XDP 파일로 저장되고 디자이너에서 만들어지는 양식 디자인을 기반으로 하는 비대화형 PDF 양식을 렌더링합니다. 양식 디자인이 포함된 `com.adobe.idp.Document` 개체를 출력 서비스에 전달할 수 있습니다. 그런 다음 출력 서비스는 `com.adobe.idp.Document` 개체에 있는 양식 디자인을 렌더링합니다.

`com.adobe.idp.Document` 개체를 출력 서비스에 전달하면 다른 AEM Forms 서비스 작업에서 `com.adobe.idp.Document` 인스턴스를 반환하는 이점이 있습니다. 즉, 다른 서비스 작업에서 `com.adobe.idp.Document` 인스턴스를 가져와 렌더링할 수 있습니다. 예를 들어, 다음 그림과 같이 XDP 파일이 `/Company Home/Form Designs`(더 이상 사용되지 않음) 노드인 컨텐츠 서비스 노드에 저장된다고 가정합니다.

컨텐츠 서비스(더 이상 사용되지 않음)에서 Loan.xdp를 프로그래밍 방식으로 검색하고 XDP 파일을 `com.adobe.idp.Document` 개체 내의 출력 서비스에 전달할 수 있습니다.

>[!NOTE]
>
>Forms 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary_of_steps-2}

컨텐츠 서비스(더 이상 사용되지 않음)에서 가져온 문서를 출력 서비스로 전달하려면 다음 작업을 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. 출력 및 Document Management 클라이언트 API 개체를 만듭니다.
1. Content Services에서 양식 디자인을 검색합니다(더 이상 사용되지 않음).
1. 비대화형 PDF 양식을 렌더링합니다.
1. 데이터 스트림으로 작업을 수행합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함하십시오. 웹 서비스를 사용하는 경우 프록시 파일을 포함하십시오.

**출력 및 Document Management 클라이언트 API 개체 만들기**

출력 서비스 API 작업을 프로그래밍 방식으로 수행하려면 먼저 출력 클라이언트 API 개체를 만듭니다. 또한 이 워크플로우는 컨텐츠 서비스에서 XDP 파일을 검색하므로(더 이상 사용되지 않음) 문서 관리 API 개체를 만듭니다.

**컨텐츠 서비스에서 양식 디자인을 검색합니다(더 이상 사용되지 않음).**

Java 또는 웹 서비스 API를 사용하여 콘텐츠 서비스에서 XDP 파일을 검색합니다(더 이상 사용되지 않음). XDP 파일은 `com.adobe.idp.Document` 인스턴스(또는 웹 서비스를 사용하는 경우 `BLOB` 인스턴스) 내에서 반환됩니다. 그런 다음 `com.adobe.idp.Document` 인스턴스를 출력 서비스에 전달할 수 있습니다.

**비대화형 PDF 양식 렌더링**

비대화형 양식을 렌더링하려면 Content Services(사용 중지)에서 반환된 `com.adobe.idp.Document` 인스턴스를 출력 서비스로 전달합니다.

>[!NOTE]
>
>`generatePDFOutput2`과 g `eneratePrintedOutput2`라는 두 개의 새 메서드는 양식 디자인이 포함된 `com.adobe.idp.Document` 개체를 허용합니다. 네트워크 프린터로 인쇄 스트림을 보낼 때 양식 디자인이 포함된 `com.adobe.idp.Document`을 출력 서비스에 전달할 수도 있습니다.

**양식 데이터 스트림으로 작업 수행**

비대화형 양식을 PDF 파일로 저장할 수 있습니다. 양식은 Adobe Reader 또는 Acrobat에서 볼 수 있습니다.

**참고 항목**

[Java API를 사용하여 출력 서비스에 문서를 전달합니다](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-java-api)

[웹 서비스 API를 사용하여 출력 서비스에 문서를 전달합니다](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[출력 서비스 API 빠른 시작](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[조각을 사용하여 PDF 문서 만들기](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

### Java API {#pass-documents-to-the-output-service-using-the-java-api}를 사용하여 출력 서비스에 문서를 전달합니다

출력 서비스 및 컨텐츠 서비스(더 이상 사용되지 않음) API(Java)를 사용하여 컨텐츠 서비스에서 검색한 문서를 전달합니다.

1. 프로젝트 파일을 포함합니다.

   adobe-output-client.jar 및 adobe-contentservices-client.jar와 같은 클라이언트 JAR 파일을 Java 프로젝트의 클래스 경로에 포함합니다.

1. 출력 및 Document Management 클라이언트 API 개체를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다. ([연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties) 참조)
   * 생성자를 사용하여 `OutputClient` 개체를 만들고 `ServiceClientFactory` 개체를 전달합니다.
   * 생성자를 사용하여 `DocumentManagementServiceClientImpl` 개체를 만들고 `ServiceClientFactory` 개체를 전달합니다.

1. Content Services에서 양식 디자인을 검색합니다(더 이상 사용되지 않음).

   `DocumentManagementServiceClientImpl` 개체의 `retrieveContent` 메서드를 호출하고 다음 값을 전달합니다.

   * 컨텐츠가 추가되는 저장소를 지정하는 문자열 값입니다. 기본 저장소는 `SpacesStore`입니다. 이 값은 필수 매개 변수입니다.
   * 검색할 컨텐츠의 정규화된 경로를 지정하는 문자열 값입니다(예: `/Company Home/Form Designs/Loan.xdp`). 이 값은 필수 매개 변수입니다.
   * 버전을 지정하는 문자열 값입니다. 이 값은 선택적 매개 변수이며 빈 문자열을 전달할 수 있습니다. 이 경우 최신 버전이 검색됩니다.

   `retrieveContent` 메서드는 XDP 파일이 포함된 `CRCResult` 개체를 반환합니다. `CRCResult` 개체의 `getDocument` 메서드를 호출하여 `com.adobe.idp.Document` 인스턴스를 검색합니다.

1. 비대화형 PDF 양식을 렌더링합니다.

   `OutputClient` 개체의 `generatePDFOutput2` 메서드를 호출하고 다음 값을 전달합니다.

   * `TransformationFormat` 열거형 값입니다. PDF 문서를 생성하려면 `TransformationFormat.PDF`을 지정합니다.
   * 이미지와 같은 추가 리소스가 있는 컨텐츠 루트를 지정하는 문자열 값입니다.
   * 양식 디자인을 나타내는 `com.adobe.idp.Document` 개체입니다( `CRCResult` 개체의 `getDocument` 메서드에서 반환된 인스턴스 사용).
   * PDF 런타임 옵션이 포함된 `PDFOutputOptionsSpec` 개체입니다.
   * 렌더링 런타임 옵션이 포함된 `RenderOptionsSpec` 개체입니다.
   * 양식 디자인과 병합할 데이터가 포함된 XML 데이터 소스가 포함된 `com.adobe.idp.Document` 개체입니다.

   `generatePDFOutput2` 메서드는 작업 결과를 포함하는 `OutputResult` 개체를 반환합니다.

1. 양식 데이터 스트림으로 작업을 수행합니다.

   * `OutputResult` 개체의 `getGeneratedDoc` 메서드를 호출하여 비대화형 양식을 나타내는 `com.adobe.idp.Document` 개체를 검색합니다.
   * 작업 결과가 포함된 `java.io.File` 개체를 만듭니다. 파일 이름 확장명이 .pdf인지 확인합니다.
   * `com.adobe.idp.Document` 개체의 `copyToFile` 메서드를 호출하여 `com.adobe.idp.Document` 개체의 내용을 파일에 복사합니다. `getGeneratedDoc` 메서드에서 반환된 `com.adobe.idp.Document` 개체를 사용해야 합니다.

**참고 항목**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[빠른 시작(EJB 모드):Java API를 사용하여 출력 서비스에 문서 전달](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 출력 서비스에 문서 전달](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API {#pass-documents-to-the-output-service-using-the-web-service-api}를 사용하여 출력 서비스에 문서를 전달합니다

출력 서비스 및 컨텐츠 서비스(더 이상 사용되지 않음) API(웹 서비스)를 사용하여 컨텐츠 서비스에서 검색한 문서를 전달합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 이 클라이언트 응용 프로그램은 두 개의 AEM Forms 서비스를 호출하므로 두 개의 서비스 참조를 만듭니다. 출력 서비스와 연결된 서비스 참조에 대해 다음 WSDL 정의를 사용하십시오.`http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`

   문서 관리 서비스와 연결된 서비스 참조에 대해 다음 WSDL 정의를 사용하십시오.`http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`

   `BLOB` 데이터 유형은 두 서비스 참조에 공통이므로 사용할 때 `BLOB` 데이터 형식을 완전히 정규화합니다. 해당 웹 서비스 빠른 시작에서 모든 `BLOB` 인스턴스는 완전히 검증됩니다.

   >[!NOTE]
   >
   >`localhost` 을 AEM Forms을 호스팅하는 서버의 IP 주소로 바꿉니다.

1. 출력 및 Document Management 클라이언트 API 개체를 만듭니다.

   * 기본 생성자를 사용하여 `OutputServiceClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `OutputServiceClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/OutputService?blob=mtom`). `lc_version` 특성을 사용할 필요는 없습니다. 이 속성은 서비스 참조를 생성할 때 사용됩니다.)
   * `OutputServiceClient.Endpoint.Binding` 필드의 값을 가져와서 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * AEM Forms 사용자 이름을 `OutputServiceClient.ClientCredentials.UserName.UserName` 필드에 지정합니다.
      * 해당 암호 값을 `OutputServiceClient.ClientCredentials.UserName.Password` 필드에 할당합니다.
      * 상수 값 `HttpClientCredentialType.Basic`을 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.
   * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

   >[!NOTE]
   >
   >`DocumentManagementServiceClient`서비스 클라이언트에 대해 이러한 단계를 반복합니다.

1. Content Services에서 양식 디자인을 검색합니다(더 이상 사용되지 않음).

   `DocumentManagementServiceClient` 개체의 `retrieveContent` 메서드를 호출하고 다음 값을 전달하여 콘텐츠를 검색합니다.

   * 컨텐츠가 추가되는 저장소를 지정하는 문자열 값입니다. 기본 저장소는 `SpacesStore`입니다. 이 값은 필수 매개 변수입니다.
   * 검색할 컨텐츠의 정규화된 경로를 지정하는 문자열 값입니다(예: `/Company Home/Form Designs/Loan.xdp`). 이 값은 필수 매개 변수입니다.
   * 버전을 지정하는 문자열 값입니다. 이 값은 선택적 매개 변수이며 빈 문자열을 전달할 수 있습니다. 이 경우 최신 버전이 검색됩니다.
   * 찾아보기 링크 값을 저장하는 문자열 출력 매개 변수입니다.
   * 컨텐츠를 저장하는 `BLOB` 출력 매개 변수입니다. 이 출력 매개 변수를 사용하여 컨텐츠를 검색할 수 있습니다.
   * 컨텐츠 속성을 저장하는 `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` 출력 매개 변수입니다.
   * `CRCResult` 출력 매개 변수입니다. 이 개체를 사용하는 대신 `BLOB` 출력 매개 변수를 사용하여 콘텐츠를 검색할 수 있습니다.

1. 비대화형 PDF 양식을 렌더링합니다.

   `OutputServiceClient` 개체의 `generatePDFOutput2` 메서드를 호출하고 다음 값을 전달합니다.

   * `TransformationFormat` 열거형 값입니다. PDF 문서를 생성하려면 `TransformationFormat.PDF`을 지정합니다.
   * 이미지와 같은 추가 리소스가 있는 컨텐츠 루트를 지정하는 문자열 값입니다.
   * 양식 디자인을 나타내는 `BLOB` 개체(Content Services에서 반환된 `BLOB` 인스턴스 사용(사용 중지)).
   * PDF 런타임 옵션이 포함된 `PDFOutputOptionsSpec` 개체입니다.
   * 렌더링 런타임 옵션이 포함된 `RenderOptionsSpec` 개체입니다.
   * 양식 디자인과 병합할 데이터가 포함된 XML 데이터 소스가 포함된 `BLOB` 개체입니다.
   * `generatePDFOutput2` 메서드로 채워지는 출력 `BLOB` 개체입니다. `generatePDFOutput2` 메서드는 이 개체를 문서를 설명하는 생성된 메타데이터로 채웁니다. (이 매개 변수 값은 웹 서비스 호출에만 필요합니다.)
   * 작업 결과를 포함하는 출력 `OutputResult` 개체입니다. (이 매개 변수 값은 웹 서비스 호출에만 필요합니다.)

   `generatePDFOutput2` 메서드는 비대화형 PDF 양식을 포함하는 `BLOB` 개체를 반환합니다.

1. 양식 데이터 스트림으로 작업을 수행합니다.

   * 해당 생성자를 호출하여 `System.IO.FileStream` 개체를 만듭니다. 대화형 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * `generatePDFOutput2` 메서드에서 검색한 `BLOB` 개체의 콘텐츠를 저장하는 바이트 배열을 만듭니다. `BLOB` 개체의 `MTOM` 데이터 멤버의 값을 가져와서 바이트 배열을 채웁니다.
   * 해당 생성자를 호출하고 `System.IO.FileStream` 개체를 전달하여 `System.IO.BinaryWriter` 개체를 만듭니다.
   * `System.IO.BinaryWriter` 개체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열 내용을 PDF 파일에 씁니다.

**참고 항목**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 저장소에 있는 문서를 출력 서비스 {#passing-documents-located-in-the-repository-to-the-output-service}에 전달

출력 서비스는 일반적으로 XDP 파일로 저장되고 디자이너에서 만들어지는 양식 디자인을 기반으로 하는 비대화형 PDF 양식을 렌더링합니다. 양식 디자인이 포함된 `com.adobe.idp.Document` 개체를 출력 서비스에 전달할 수 있습니다. 그런 다음 출력 서비스는 `com.adobe.idp.Document` 개체에 있는 양식 디자인을 렌더링합니다.

`com.adobe.idp.Document` 개체를 출력 서비스에 전달하면 다른 AEM Forms 서비스 작업에서 `com.adobe.idp.Document` 인스턴스를 반환하는 이점이 있습니다. 즉, 다른 서비스 작업에서 `com.adobe.idp.Document` 인스턴스를 가져와 렌더링할 수 있습니다. 예를 들어 다음 그림과 같이 XDP 파일이 AEM Forms 저장소에 저장된다고 가정합니다.

![pd_pd_formrepository](assets/pd_pd_formrepository.png)

*FormsFolder* 폴더는 AEM Forms 리포지토리에서 사용자가 정의한 위치입니다(이 위치는 예이며, 기본적으로 존재하지 않습니다.). 이 예제에서 Loan.xdp라는 양식 디자인은 이 폴더에 있습니다. 양식 디자인 외에도 이미지와 같은 다른 양식 자료를 이 위치에 저장할 수 있습니다. AEM Forms 저장소에 있는 리소스의 경로는 다음과 같습니다.

`Applications/Application-name/Application-version/Folder.../Filename`

AEM Forms 저장소에서 Loan.xdp를 프로그래밍 방식으로 검색하고 `com.adobe.idp.Document` 개체 내의 출력 서비스에 전달할 수 있습니다.

다음 두 가지 방법 중 하나를 사용하여 리포지토리에 있는 XDP 파일을 기반으로 PDF를 만들 수 있습니다. 참조용으로 XDP 위치를 전달하거나 리포지토리에서 XDP를 프로그래밍 방식으로 검색하여 XDP 파일 내의 출력 서비스에 전달할 수 있습니다.

[빠른 시작(EJB 모드):Java API ](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api) 를 사용하여 애플리케이션 XDP 파일을 기반으로 PDF 문서 만들기(참조를 통해 XDP 파일의 위치를 전달하는 방법 표시).

[빠른 시작(EJB 모드):Java API ](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) 를 사용하여 AEM Forms 저장소에 있는 문서를 출력 서비스에 전달합니다(AEM Forms 저장소에서 XDP 파일을 프로그래밍 방식으로 검색하고 인스턴스 내에서 출력 서비스에 전달하는 방법을  `com.adobe.idp.Document` 표시). (이 섹션에서는 이 작업을 수행하는 방법을 설명합니다.)

>[!NOTE]
>
>Forms 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary_of_steps-3}

AEM Forms 리포지토리에서 가져온 문서를 출력 서비스로 전달하려면 다음 작업을 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. 출력 및 Document Management 클라이언트 API 개체를 만듭니다.
1. AEM Forms 저장소에서 양식 디자인을 검색합니다.
1. 비대화형 PDF 양식을 렌더링합니다.
1. 데이터 스트림으로 작업을 수행합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함하십시오. 웹 서비스를 사용하는 경우 프록시 파일을 포함하십시오.

**출력 및 Document Management 클라이언트 API 개체 만들기**

출력 서비스 API 작업을 프로그래밍 방식으로 수행하려면 먼저 출력 클라이언트 API 개체를 만듭니다. 또한 이 워크플로우는 컨텐츠 서비스에서 XDP 파일을 검색하므로(더 이상 사용되지 않음) 문서 관리 API 개체를 만듭니다.

**AEM Forms 리포지토리에서 양식 디자인 검색**

저장소 API를 사용하여 AEM Forms 저장소에서 XDP 파일을 검색합니다. ([리소스 읽기](/help/forms/developing/aem-forms-repository.md#reading-resources) 참조)

XDP 파일은 `com.adobe.idp.Document` 인스턴스(또는 웹 서비스를 사용하는 경우 `BLOB` 인스턴스) 내에서 반환됩니다. 그런 다음 `com.adobe.idp.Document` 인스턴스를 출력 서비스에 전달할 수 있습니다.

**비대화형 PDF 양식 렌더링**

비대화형 양식을 렌더링하려면 AEM Forms 저장소 API를 사용하여 반환된 `com.adobe.idp.Document` 인스턴스를 전달합니다.

>[!NOTE]
>
>`generatePDFOutput2`과 `generatePrintedOutput2`이라는 두 개의 새 메서드는 양식 디자인이 포함된 `com.adobe.idp.Document`개체를 허용합니다. 네트워크 프린터로 인쇄 스트림을 보낼 때 양식 디자인이 포함된 `com.adobe.idp.Document` 을 출력 서비스에 전달할 수도 있습니다.

**양식 데이터 스트림으로 작업 수행**

비대화형 양식을 PDF 파일로 저장할 수 있습니다. 양식은 Adobe Reader 또는 Acrobat에서 볼 수 있습니다.

**참고 항목**

[Java API를 사용하여 저장소에 있는 문서를 출력 서비스에 전달합니다](creating-document-output-streams.md#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[출력 서비스 API 빠른 시작](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

리소스 저장소 클라이언트

### Java API {#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api}를 사용하여 저장소에 있는 문서를 출력 서비스에 전달합니다

출력 서비스 및 저장소 API(Java)를 사용하여 저장소에서 검색한 문서를 전달합니다.

1. 프로젝트 파일을 포함합니다.

   adobe-output-client.jar 및 adobe-repository-client.jar와 같은 클라이언트 JAR 파일을 Java 프로젝트의 클래스 경로에 포함합니다.

1. 출력 및 Document Management 클라이언트 API 개체를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다. ([연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties) 참조)
   * 생성자를 사용하여 `OutputClient` 개체를 만들고 `ServiceClientFactory` 개체를 전달합니다.
   * 생성자를 사용하여 `DocumentManagementServiceClientImpl` 개체를 만들고 `ServiceClientFactory` 개체를 전달합니다.

1. AEM Forms 리포지토리에서 양식 디자인을 검색합니다.

   `ResourceRepositoryClient` 개체의 `readResourceContent` 메서드를 호출하고 URI 위치를 지정하는 문자열 값을 XDP 파일에 전달합니다. 예, `/Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`. 이 값은 필수입니다. 이 메서드는 XDP 파일을 나타내는 `com.adobe.idp.Document` 인스턴스를 반환합니다.

1. 비대화형 PDF 양식을 렌더링합니다.

   `OutputClient` 개체의 `generatePDFOutput2` 메서드를 호출하고 다음 값을 전달합니다.

   * `TransformationFormat` 열거형 값입니다. PDF 문서를 생성하려면 `TransformationFormat.PDF`을 지정합니다.
   * 이미지와 같은 추가 리소스가 있는 컨텐츠 루트를 지정하는 문자열 값입니다. 예, `repository:///Applications/FormsApplication/1.0/FormsFolder/`.
   * 양식 디자인을 나타내는 `com.adobe.idp.Document` 개체입니다( `ResourceRepositoryClient` 개체의 `readResourceContent` 메서드에서 반환된 인스턴스 사용).
   * PDF 런타임 옵션이 포함된 `PDFOutputOptionsSpec` 개체입니다.
   * 렌더링 런타임 옵션이 포함된 `RenderOptionsSpec` 개체입니다.
   * 양식 디자인과 병합할 데이터가 포함된 XML 데이터 소스가 포함된 `com.adobe.idp.Document` 개체입니다.

   `generatePDFOutput2` 메서드는 작업 결과를 포함하는 `OutputResult` 개체를 반환합니다.

1. 양식 데이터 스트림으로 작업을 수행합니다.

   * `OutputResult` 개체의 `getGeneratedDoc` 메서드를 호출하여 비대화형 양식을 나타내는 `com.adobe.idp.Document` 개체를 검색합니다.
   * 작업 결과가 포함된 `java.io.File` 개체를 만듭니다. 파일 이름 확장명이 .pdf인지 확인합니다.
   * `com.adobe.idp.Document` 개체의 `copyToFile` 메서드를 호출하여 `com.adobe.idp.Document` 개체의 내용을 파일에 복사합니다. `getGeneratedDoc` 메서드에서 반환된 `com.adobe.idp.Document` 개체를 사용해야 합니다.

**참고 항목**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[빠른 시작(EJB 모드):Java API를 사용하여 AEM Forms 리포지토리에 있는 문서를 출력 서비스로 전달](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 조각을 사용하여 PDF 문서 만들기 {#creating-pdf-documents-using-fragments}

[출력] 및 [어셈블러] 서비스를 사용하여 조각을 기반으로 하는 PDF 문서와 같은 출력 스트림을 생성할 수 있습니다. 어셈블러 서비스는 여러 XDP 파일에 있는 조각을 기반으로 하는 XDP 문서를 어셈블합니다. 어셈블된 XDP 문서가 출력 서비스로 전달되어 PDF 문서가 만들어집니다. 이 워크플로우에는 생성 중인 PDF 문서가 표시되지만 출력 서비스는 이 워크플로우에 대해 ZPL과 같은 다른 출력 유형을 생성할 수 있습니다. PDF 문서는 토론용으로만 사용됩니다.

다음 그림은 이 워크플로우를 보여줍니다.

![cp_cp_outputassemlefragments](assets/cp_cp_outputassemblefragments.png)

*조각을 사용하여 PDF 문서 만들기*&#x200B;를 읽기 전에 어셈블러 서비스를 사용하여 여러 XDP 문서를 어셈블하는 것을 잘 알고 있어야 합니다. ([여러 XDP 구성요소 조합](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments)을 참조하십시오.)

>[!NOTE]
>
>또한 어셈블러 서비스에 의해 어셈블된 양식 디자인을 출력 서비스 대신 Forms 서비스에 전달할 수 있습니다. 출력 서비스와 Forms 서비스의 주요 차이점은 Forms 서비스가 대화형 PDF 문서를 생성하고 출력 서비스에서 비대화형 PDF 문서를 생성한다는 것입니다. 또한 Forms 서비스는 ZPL과 같은 프린터 기반 출력 스트림을 생성할 수 없습니다.

>[!NOTE]
>
>출력 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary_of_steps-4}

조각을 기반으로 PDF 문서를 만들려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. 출력 및 어셈블러 클라이언트 개체를 만듭니다.
1. 어셈블러 서비스를 사용하여 양식 디자인을 생성합니다.
1. 출력 서비스를 사용하여 PDF 문서를 생성합니다.
1. PDF 문서를 PDF 파일로 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함하십시오. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**출력 및 어셈블러 클라이언트 개체 만들기**

출력 서비스 API 작업을 프로그래밍 방식으로 수행하려면 먼저 출력 클라이언트 API 개체를 만듭니다. 또한 이 워크플로우는 어셈블러 서비스를 호출하여 양식 디자인을 만들기 때문에 어셈블러 클라이언트 API 개체를 만듭니다.

**어셈블러 서비스를 사용하여 양식 디자인을 생성합니다**

어셈블러 서비스를 사용하여 조각을 사용하여 양식 디자인을 생성합니다. 어셈블러 서비스는 양식 디자인을 포함하는 `com.adobe.idp.Document` 인스턴스를 반환합니다.

**출력 서비스를 사용하여 PDF 문서를 생성합니다**

출력 서비스를 사용하여 어셈블러 서비스에서 만든 양식 디자인을 사용하여 PDF 문서를 생성할 수 있습니다. 어셈블러 서비스가 출력 서비스로 반환한 `com.adobe.idp.Document` 인스턴스를 전달합니다.

**PDF 문서를 PDF 파일로 저장**

출력 서비스에서 PDF 문서를 생성한 후 PDF 파일로 저장할 수 있습니다.

**참고 항목**

[Java API를 사용하여 조각을 기반으로 PDF 문서 만들기](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-java-api)

[웹 서비스 API를 사용하여 조각을 기반으로 PDF 문서 만들기](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[출력 서비스 API 빠른 시작](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[여러 XDP 조각 어셈블링](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments)

[PDF 문서 만들기](creating-document-output-streams.md#creating-pdf-documents)

### Java API {#create-a-pdf-document-based-on-fragments-using-the-java-api}를 사용하여 조각을 기반으로 PDF 문서 만들기

출력 서비스 API 및 어셈블러 서비스 API(Java)를 사용하여 조각을 기반으로 PDF 문서를 만듭니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-output-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. 출력 및 어셈블러 클라이언트 개체를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 `OutputClient` 개체를 만들고 `ServiceClientFactory` 개체를 전달합니다.
   * 생성자를 사용하여 `AssemblerServiceClient` 개체를 만들고 `ServiceClientFactory` 개체를 전달합니다.

1. 어셈블러 서비스를 사용하여 양식 디자인을 생성합니다.

   `AssemblerServiceClient` 개체의 `invokeDDX` 메서드를 호출하고 다음 필수 값을 전달합니다.

   * 사용할 DDX 문서를 나타내는 `com.adobe.idp.Document` 개체입니다.
   * 입력 XDP 파일이 포함된 `java.util.Map` 개체입니다.
   * 기본 글꼴 및 작업 로그 수준을 포함하여 런타임 옵션을 지정하는 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 개체입니다.

   `invokeDDX` 메서드는 어셈블된 XDP 문서가 포함된 `com.adobe.livecycle.assembler.client.AssemblerResult` 개체를 반환합니다. 어셈블된 XDP 문서를 검색하려면 다음 작업을 수행하십시오.

   * `AssemblerResult` 개체의 `getDocuments` 메서드를 호출합니다. 이 메서드는 `java.util.Map` 개체를 반환합니다.
   * 결과 `com.adobe.idp.Document` 개체를 찾을 때까지 `java.util.Map` 개체를 반복합니다.
   * `com.adobe.idp.Document` 개체의 `copyToFile` 메서드를 호출하여 어셈블된 XDP 문서를 추출합니다.


1. 출력 서비스를 사용하여 PDF 문서를 생성합니다.

   `OutputClient` 개체의 `generatePDFOutput2` 메서드를 호출하고 다음 값을 전달합니다.

   * `TransformationFormat` 열거형 값입니다. PDF 문서를 생성하려면 `TransformationFormat.PDF` 을 지정합니다
   * 이미지와 같은 추가 리소스가 있는 컨텐츠 루트를 지정하는 문자열 값입니다
   * 양식 디자인을 나타내는 `com.adobe.idp.Document` 개체(어셈블러 서비스에서 반환한 인스턴스 사용)
   * PDF 런타임 옵션이 포함된 `PDFOutputOptionsSpec` 개체
   * 렌더링 런타임 옵션이 포함된 `RenderOptionsSpec` 개체
   * 양식 디자인과 병합할 데이터가 포함된 XML 데이터 소스가 포함된 `com.adobe.idp.Document` 개체입니다

   `generatePDFOutput2` 메서드는 작업 결과를 포함하는 `OutputResult` 개체를 반환합니다

1. PDF 문서를 PDF 파일로 저장합니다.

   * `OutputResult` 개체의 `getGeneratedDoc` 메서드를 호출하여 PDF 문서를 나타내는 `com.adobe.idp.Document` 개체를 검색합니다.
   * 작업 결과가 포함된 `java.io.File` 개체를 만듭니다. 파일 이름 확장명이 .pdf인지 확인합니다.
   * `com.adobe.idp.Document` 개체의 `copyToFile` 메서드를 호출하여 `com.adobe.idp.Document` 개체의 내용을 파일에 복사합니다. ( `getGeneratedDoc` 메서드가 반환한 `com.adobe.idp.Document` 개체를 사용해야 합니다.)

**참고 항목**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[빠른 시작(EJB 모드):Java API를 사용하여 조각을 기반으로 PDF 문서 만들기](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 조각을 기반으로 PDF 문서 만들기](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성을 설정합니다](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### 웹 서비스 API {#create-a-pdf-document-based-on-fragments-using-the-web-service-api}를 사용하여 조각을 기반으로 PDF 문서 만들기

출력 서비스 API 및 어셈블러 서비스 API(웹 서비스)를 사용하여 조각을 기반으로 PDF 문서를 만듭니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 출력 서비스와 연결된 서비스 참조에 대해 다음 WSDL 정의를 사용하십시오.

   ```java
    http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1.
   ```

   어셈블러 서비스와 연결된 서비스 참조에 대해 다음 WSDL 정의를 사용하십시오.

   ```java
    http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   `BLOB` 데이터 유형은 두 서비스 참조에 공통이므로 사용할 때 `BLOB` 데이터 형식을 완전히 정규화합니다. 해당 웹 서비스 빠른 시작에서 모든 `BLOB` 인스턴스는 완전히 검증됩니다.

   >[!NOTE]
   >
   >`localhost` 을 AEM Forms을 호스팅하는 서버의 IP 주소로 바꿉니다.

1. 출력 및 어셈블러 클라이언트 개체를 만듭니다.

   * 기본 생성자를 사용하여 `OutputServiceClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `OutputServiceClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/OutputService?blob=mtom`). `lc_version` 특성을 사용할 필요는 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다. 그러나 MTOM을 사용하려면 `?blob=mtom`을 지정하십시오.
   * `OutputServiceClient.Endpoint.Binding` 필드의 값을 가져와서 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * AEM Forms 사용자 이름을 `OutputServiceClient.ClientCredentials.UserName.UserName`필드에 지정합니다.
      * 해당 암호 값을 `OutputServiceClient.ClientCredentials.UserName.Password`필드에 할당합니다.
      * `BasicHttpBindingSecurity.Transport.ClientCredentialType`필드에 상수 값 `HttpClientCredentialType.Basic`을 할당합니다.
   * `BasicHttpSecurityMode.TransportCredentialOnly` 상수 값을 `BasicHttpBindingSecurity.Security.Mode`필드에 할당합니다.

   >[!NOTE]
   >
   >`AssemblerServiceClient`개체에 대해 다음 단계를 반복합니다.

1. 어셈블러 서비스를 사용하여 양식 디자인을 생성합니다.

   `AssemblerServiceClient` 개체의 `invokeDDX` 메서드를 호출하고 다음 값을 전달합니다.

   * DDX 문서를 나타내는 `BLOB` 개체
   * 필요한 파일이 포함된 `MyMapOf_xsd_string_To_xsd_anyType` 개체
   * 런타임 옵션을 지정하는 `AssemblerOptionSpec` 개체

   `invokeDDX` 메서드는 작업 결과와 발생한 예외가 포함된 `AssemblerResult` 개체를 반환합니다. 새로 만든 XDP 문서를 가져오려면 다음 작업을 수행하십시오.

   * 결과 PDF 문서가 포함된 `Map` 개체인 `AssemblerResult` 개체의 `documents` 필드에 액세스합니다.
   * `Map` 개체를 반복하여 어셈블된 양식 디자인을 검색합니다. 해당 배열 멤버의 `value`을(를) `BLOB`에 캐스팅합니다. 이 `BLOB` 인스턴스를 출력 서비스에 전달합니다.


1. 출력 서비스를 사용하여 PDF 문서를 생성합니다.

   `OutputServiceClient` 개체의 `generatePDFOutput2` 메서드를 호출하고 다음 값을 전달합니다.

   * `TransformationFormat` 열거형 값입니다. PDF 문서를 생성하려면 `TransformationFormat.PDF`을 지정합니다.
   * 이미지와 같은 추가 리소스가 있는 컨텐츠 루트를 지정하는 문자열 값입니다.
   * 양식 디자인을 나타내는 `BLOB` 개체(어셈블러 서비스에서 반환한 `BLOB` 인스턴스 사용)입니다.
   * PDF 런타임 옵션이 포함된 `PDFOutputOptionsSpec` 개체입니다.
   * 렌더링 런타임 옵션이 포함된 `RenderOptionsSpec` 개체입니다.
   * 양식 디자인과 병합할 데이터가 포함된 XML 데이터 소스가 포함된 `BLOB` 개체입니다.
   * `generatePDFOutput2` 메서드가 채우는 출력 `BLOB` 개체입니다. `generatePDFOutput2` 메서드는 이 개체를 문서를 설명하는 생성된 메타데이터로 채웁니다. (이 매개 변수 값은 웹 서비스 호출에만 필요합니다.)
   * 작업 결과를 포함하는 출력 `OutputResult` 개체입니다. (이 매개 변수 값은 웹 서비스 호출에만 필요합니다.)

   `generatePDFOutput2` 메서드는 비대화형 PDF 양식을 포함하는 `BLOB` 개체를 반환합니다.

1. PDF 문서를 PDF 파일로 저장합니다.

   * 해당 생성자를 호출하여 `System.IO.FileStream` 개체를 만듭니다. 대화형 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * `generatePDFOutput2` 메서드에서 검색한 `BLOB` 개체의 콘텐츠를 저장하는 바이트 배열을 만듭니다. `BLOB` 개체의 `MTOM` 데이터 멤버의 값을 가져와서 바이트 배열을 채웁니다.
   * 해당 생성자를 호출하고 `System.IO.FileStream` 개체를 전달하여 `System.IO.BinaryWriter` 개체를 만듭니다.
   * `System.IO.BinaryWriter` 개체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열 내용을 PDF 파일에 씁니다.

**참고 항목**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 파일 {#printing-to-files}에 인쇄

출력 서비스를 사용하여 PostScript, PCL(Printer Control Language) 또는 다음 레이블 형식과 같은 스트림을 파일에 인쇄할 수 있습니다.

* 제브라 - ZPL
* 인터페이스 - IPL
* Datamax - DPL
* TecToshiba - TPCL

출력 서비스를 사용하면 XML 데이터를 양식 디자인과 병합하고 양식을 파일에 인쇄할 수 있습니다. 다음 그림은 레이저 및 레이블 파일을 생성하는 출력 서비스를 보여줍니다.

>[!NOTE]
>
>프린터로 인쇄 스트림을 전송하는 방법은 [프린터로 인쇄 스트림 보내기](creating-document-output-streams.md#sending-print-streams-to-printers)를 참조하십시오.

>[!NOTE]
>
>출력 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary_of_steps-5}

파일로 인쇄하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. 출력 클라이언트 개체를 만듭니다.
1. XML 데이터 소스를 참조합니다.
1. 파일로 인쇄하는 데 필요한 인쇄 런타임 옵션을 설정합니다.
1. 인쇄 스트림을 파일로 인쇄합니다.
1. 작업의 결과를 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함하십시오. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms이 JBoss에 배포되는 경우 필요)

AEM Forms이 JBoss가 아닌 지원되는 J2EE 애플리케이션 서버에 배포되는 경우 adobe-utilities.jar 및 jbossall-client.jar 파일을 AEM Forms이 배포된 J2EE 애플리케이션 서버와 관련된 JAR 파일로 대체해야 합니다. ([AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files) 참조)

**출력 클라이언트 개체 만들기**

출력 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 출력 서비스 클라이언트 개체를 만들어야 합니다. Java API를 사용하는 경우 `OutputClient` 개체를 만듭니다. 출력 웹 서비스 API를 사용하는 경우 `OutputServiceService` 개체를 만듭니다.

**XML 데이터 소스 참조**

데이터가 포함된 문서를 인쇄하려면 데이터를 채울 모든 양식 필드에 대해 XML 요소가 포함된 XML 데이터 소스를 참조해야 합니다. XML 요소 이름은 필드 이름과 일치해야 합니다. XML 요소는 양식 필드에 해당하지 않거나 XML 요소 이름이 필드 이름과 일치하지 않는 경우에는 무시됩니다. 모든 XML 요소가 지정된 경우 XML 요소가 표시되는 순서와 일치하지 않아도 됩니다.

**파일에 인쇄하는 데 필요한 인쇄 실행 시간 옵션을 설정합니다.**

파일로 인쇄하려면 출력 서비스가 인쇄하는 파일의 위치와 이름을 지정하여 파일 URI 런타임 옵션을 설정해야 합니다. 예를 들어 출력 서비스에서 *ModerationForm.ps*&#x200B;라는 PostScript 파일을 C:\Adobe으로 인쇄하도록 지시하려면 C:\Adobe\MortgageForm.ps을 지정합니다.

>[!NOTE]
>
>정의할 수 있는 선택적 런타임 옵션이 있습니다. 설정할 수 있는 모든 옵션에 대한 자세한 내용은 [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)에서 `PrintedOutputOptionsSpec` 클래스 참조를 참조하십시오.

**인쇄 스트림을 파일로 인쇄**

양식 데이터가 포함된 유효한 XML 데이터 원본을 참조하고 인쇄 런타임 옵션을 설정한 후에는 출력 서비스를 호출하여 파일을 인쇄할 수 있습니다.

**작업 결과 검색**

출력 서비스에서 작업을 수행하면 작업이 성공했는지 여부를 지정하는 XML 데이터와 같은 다양한 데이터 항목이 반환됩니다.

**참고 항목**

[Java API를 사용하여 파일에 인쇄](creating-document-output-streams.md#print-to-files-using-the-java-api)

[웹 서비스 API를 사용하여 파일에 인쇄](creating-document-output-streams.md#print-to-files-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[출력 서비스 API 빠른 시작](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java API {#print-to-files-using-the-java-api}를 사용하여 파일로 인쇄

출력 API(Java)를 사용하여 파일로 인쇄:

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-output-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. 출력 클라이언트 개체를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 `OutputClient` 개체를 만들고 `ServiceClientFactory` 개체를 전달합니다.

1. XML 데이터 소스를 참조합니다.

   * 생성자를 사용하여 문서를 채우고 XML 파일의 위치를 지정하는 문자열 값을 전달하여 문서를 채우는 데 사용되는 XML 데이터 소스를 나타내는 `java.io.FileInputStream` 개체를 만듭니다.
   * 생성자를 사용하여 `com.adobe.idp.Document` 개체를 만들고 `java.io.FileInputStream` 개체를 전달합니다.

1. 파일로 인쇄하는 데 필요한 인쇄 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 `PrintedOutputOptionsSpec` 개체를 만듭니다.
   * PrintedOutputOptionsSpec 개체의 `setFileURI` 메서드를 호출하고 파일의 이름과 위치를 나타내는 문자열 값을 전달하여 파일을 지정합니다. 예를 들어, 출력 서비스가 C:\Adobe에 있는 ModerationForm.ps라는 PostScript 파일에 인쇄되도록 하려면 C:\\Adobe\MortgageForm.ps을 지정합니다.
   * `PrintedOutputOptionsSpec` 개체의 `setCopies` 메서드를 호출하고 복사본 수를 나타내는 정수 값을 전달하여 인쇄할 복사본 수를 지정합니다.

1. 인쇄 스트림을 파일로 인쇄합니다.

   `OutputClient` 개체의 `generatePrintedOutput` 메서드를 호출하고 다음 값을 전달하여 파일에 인쇄합니다.

   * 만들 인쇄 스트림 형식을 지정하는 `PrintFormat` 열거형 값입니다. 예를 들어 PostScript 인쇄 스트림을 만들려면 `PrintFormat.PostScript`을 전달합니다.
   * 양식 디자인의 이름을 지정하는 문자열 값입니다.
   * 이미지 파일과 같은 관련 자료 파일의 위치를 지정하는 문자열 값입니다.
   * 사용할 XDC 파일의 위치를 지정하는 문자열 값입니다(`PrintedOutputOptionsSpec` 개체를 사용하여 사용할 XDC 파일을 지정한 경우 `null`을 전달할 수 있음).
   * 파일에 인쇄하는 데 필요한 런타임 옵션이 포함된 `PrintedOutputOptionsSpec` 개체입니다.
   * 양식 데이터가 포함된 XML 데이터 소스를 포함하는 `com.adobe.idp.Document` 개체입니다.

   `generatePrintedOutput` 메서드는 작업 결과를 포함하는 `OutputResult` 개체를 반환합니다.

   >[!NOTE]
   >
   >`OutputResult` 개체의 `getRecordLevelMetaDataList` 메서드는 `null`를 반환합니다.

1. 작업의 결과를 검색합니다.

   * `OutputResult` 개체의 `getStatusDoc` 메서드를 호출하여 `generatePrintedOutput` 메서드의 상태를 나타내는 `com.adobe.idp.Document` 개체를 만듭니다(`generatePrintedOutput` 메서드에서 `OutputResult` 개체가 반환됨).
   * 작업 결과를 포함할 `java.io.File` 개체를 만듭니다. 파일 확장명이 XML인지 확인합니다.
   * `com.adobe.idp.Document` 개체의 `copyToFile` 메서드를 호출하여 `com.adobe.idp.Document` 개체의 내용을 파일에 복사합니다. `getStatusDoc` 메서드에서 반환된 `com.adobe.idp.Document` 개체를 사용해야 합니다.

**참고 항목**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[빠른 시작(SOAP 모드):Java API를 사용하여 파일에 인쇄](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-printing-to-a-file-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성을 설정합니다](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### 웹 서비스 API {#print-to-files-using-the-web-service-api}를 사용하여 파일로 인쇄

출력 API(웹 서비스)를 사용하여 파일로 인쇄:

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다.`http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`

   >[!NOTE]
   >
   >`localhost` 을 AEM Forms을 호스팅하는 서버의 IP 주소로 바꿉니다.

1. 출력 클라이언트 개체를 만듭니다.

   * 기본 생성자를 사용하여 `OutputServiceClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `OutputServiceClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/OutputService?blob=mtom`). `lc_version` 특성을 사용할 필요는 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다. 그러나 MTOM을 사용하려면 `?blob=mtom`을 지정하십시오.
   * `OutputServiceClient.Endpoint.Binding` 필드의 값을 가져와서 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * AEM Forms 사용자 이름을 `OutputServiceClient.ClientCredentials.UserName.UserName` 필드에 지정합니다.
      * 해당 암호 값을 `OutputServiceClient.ClientCredentials.UserName.Password` 필드에 할당합니다.
      * 상수 값 `HttpClientCredentialType.Basic`을 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.
      * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. XML 데이터 소스를 참조합니다.

   * 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 양식 데이터를 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하고 양식 데이터가 포함된 XML 파일의 위치를 지정하는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하고 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * `binaryData` 속성을 바이트 배열의 콘텐츠로 할당하여 `BLOB` 개체를 채웁니다.

1. 파일로 인쇄하는 데 필요한 인쇄 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 `PrintedOutputOptionsSpec` 개체를 만듭니다.
   * 파일의 위치와 이름을 나타내는 문자열 값을 `PrintedOutputOptionsSpec` 개체의 `fileURI` 데이터 멤버에 할당하여 파일을 지정합니다. 예를 들어, 출력 서비스가 C:\Adobe에 있는 *ModerationForm.ps*&#x200B;라는 PostScript 파일에 인쇄하도록 하려면 C:\\Adobe\MortgageForm.ps을 지정합니다.
   * `PrintedOutputOptionsSpec` 개체의 `copies` 데이터 멤버에 복사본 수를 나타내는 정수 값을 할당하여 인쇄할 복사본 수를 지정합니다.

1. 인쇄 스트림을 파일로 인쇄합니다.

   `OutputServiceService` 개체의 `generatePrintedOutput` 메서드를 호출하고 다음 값을 전달하여 파일에 인쇄합니다.

   * 만들 인쇄 스트림 형식을 지정하는 `PrintFormat` 열거형 값입니다. 예를 들어 PostScript 인쇄 스트림을 만들려면 `PrintFormat.PostScript`을 전달합니다.
   * 양식 디자인의 이름을 지정하는 문자열 값입니다.
   * 이미지 파일과 같은 관련 자료 파일의 위치를 지정하는 문자열 값입니다.
   * 사용할 XDC 파일의 위치를 지정하는 문자열 값입니다(`PrintedOutputOptionsSpec` 개체를 사용하여 사용할 XDC 파일을 지정한 경우 `null`을 전달할 수 있음).
   * 파일에 인쇄하는 데 필요한 인쇄 런타임 옵션이 포함된 `PrintedOutputOptionsSpec` 개체입니다.
   * 양식 데이터가 포함된 XML 데이터 소스를 포함하는 `BLOB` 개체입니다.
   * `generatePDFOutput` 메서드로 채워지는 `BLOB` 개체입니다. `generatePDFOutput` 메서드는 이 개체를 문서를 설명하는 생성된 메타데이터로 채웁니다. (이 매개 변수 값은 웹 서비스 호출에만 필요합니다.)
   * `generatePDFOutput` 메서드로 채워지는 `BLOB` 개체입니다. `generatePDFOutput` 메서드는 이 개체를 결과 데이터로 채웁니다. (이 매개 변수 값은 웹 서비스 호출에만 필요합니다.)
   * 작업 결과를 포함하는 `OutputResult` 개체입니다. (이 매개 변수 값은 웹 서비스 호출에만 필요합니다.)

1. 작업의 결과를 검색합니다.

   * 해당 생성자를 호출하고 결과 데이터가 포함된 XML 파일 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다. 파일 확장명이 XML인지 확인합니다.
   * `OutputServiceService` 개체의 `generatePDFOutput` 메서드(8번째 매개 변수)로 결과 데이터로 채워지는 `BLOB` 개체의 데이터 콘텐츠를 저장하는 바이트 배열을 만듭니다. `BLOB` 개체의 `MTOM` 데이터 멤버의 값을 가져와서 바이트 배열을 채웁니다.
   * 해당 생성자를 호출하고 `System.IO.FileStream` 개체를 전달하여 `System.IO.BinaryWriter` 개체를 만듭니다.
   * `System.IO.BinaryWriter` 개체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 XML 파일에 씁니다.

**참고 항목**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 인쇄 스트림을 프린터로 보내는 중 {#sending-print-streams-to-printers}

출력 서비스를 사용하여 PostScript, PCL(Printer Control Language) 또는 다음 레이블 형식과 같은 인쇄 스트림을 네트워크 프린터로 보낼 수 있습니다.

* 제브라 - ZPL
* 인터페이스 - IPL
* Datamax - DPL
* TecToshiba - TPCL

출력 서비스를 사용하여 XML 데이터를 양식 디자인과 병합하고 양식을 인쇄 스트림으로 출력할 수 있습니다. 예를 들어 PostScript 인쇄 스트림을 만들어 네트워크 프린터로 보낼 수 있습니다. 다음 그림은 인쇄 스트림을 네트워크 프린터로 보내는 출력 서비스를 보여줍니다.

>[!NOTE]
>
>네트워크 프린터로 인쇄 스트림을 보내는 방법을 보여주기 위해 이 섹션에서는 SharedPrinter 프린터 프로토콜을 사용하여 PostScript 인쇄 스트림을 네트워크 프린터로 보냅니다.

>[!NOTE]
>
>출력 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary_of_steps-6}

인쇄 스트림을 네트워크 프린터로 보내려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. 출력 클라이언트 개체를 만듭니다.
1. XML 데이터 소스를 참조합니다.
1. 인쇄 런타임 옵션 설정
1. 인쇄할 문서를 검색합니다.
1. 문서를 네트워크 프린터로 보냅니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함하십시오. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms이 JBoss에 배포되는 경우 필수)

AEM Forms이 JBoss가 아닌 지원되는 J2EE 애플리케이션 서버에 배포되는 경우 adobe-utilities.jar 및 jbossall-client.jar 파일을 AEM Forms이 배포된 J2EE 애플리케이션 서버와 관련된 JAR 파일로 대체해야 합니다.

**출력 클라이언트 개체 만들기**

출력 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 출력 서비스 클라이언트 개체를 만듭니다. Java API를 사용하는 경우 `OutputClient` 개체를 만듭니다. 출력 웹 서비스 API를 사용하는 경우 `OutputServiceClient` 개체를 만듭니다.

**XML 데이터 소스 참조**

데이터가 포함된 문서를 인쇄하려면 데이터를 채울 모든 양식 필드에 대해 XML 요소가 포함된 XML 데이터 소스를 참조해야 합니다. XML 요소 이름은 필드 이름과 일치해야 합니다. XML 요소는 양식 필드에 해당하지 않거나 XML 요소 이름이 필드 이름과 일치하지 않는 경우에는 무시됩니다. 모든 XML 요소가 지정된 경우 XML 요소가 표시되는 순서와 일치하지 않아도 됩니다.

**인쇄 런타임 옵션 설정**

다음 옵션을 포함하여 인쇄 스트림을 프린터로 전송할 때 런타임 옵션을 설정할 수 있습니다.

* **복사**:프린터에 보낼 복사본 수를 지정합니다. 기본값은 1입니다.
* **스테이플**:스테이플러를 사용할 때 XCI 옵션이 설정됩니다. 이 옵션은 스테이플 요소에 의해 구성 모델에서 지정할 수 있으며 PS 및 PCL 프린터에만 사용됩니다.
* **OutputJog**:출력 페이지를 조인해야 할 때(출력 트레이에서 물리적으로 이동) XCI 옵션이 설정됩니다. 이 옵션은 PS 및 PCL 프린터에만 사용됩니다.
* **OutputBin**:인쇄 드라이버가 적절한 출력 저장소를 선택할 수 있도록 하는 데 사용되는 XCI 값입니다.

>[!NOTE]
>
>설정할 수 있는 모든 런타임 옵션에 대한 자세한 내용은 `PrintedOutputOptionsSpec` 클래스 참조를 참조하십시오.

**인쇄할 문서 검색**

프린터로 전송할 인쇄 스트림을 검색합니다. 예를 들어 PostScript 파일을 검색하고 프린터로 보낼 수 있습니다.

프린터가 PDF를 지원하는 경우 PDF 파일을 보내도록 선택할 수 있습니다. 그러나 PDF 문서를 프린터로 보낼 때 문제가 되는 것은 각 프린터 제조업체마다 PDF 인터프리터를 다르게 구현한다는 것입니다. 즉, 일부 인쇄업체는 Adobe PDF 해석을 사용하지만 프린터에 따라 다릅니다. 다른 프린터에는 자체 PDF 인터프리터가 있습니다. 따라서 인쇄 결과는 달라질 수 있습니다.

PDF 문서를 프린터에 보내는 또 다른 제한 사항은 프린트라는 것입니다.프린터의 설정을 제외하고 듀플렉스, 용지 트레이 선택 및 스테이플에 액세스할 수 없습니다.

인쇄할 문서를 검색하려면 `generatePrintedOutput` 메서드를 사용합니다. 다음 표는 `generatePrintedOutput` 메서드를 사용할 때 지정된 인쇄 스트림에 대해 설정된 컨텐츠 유형을 지정합니다.

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
   <td><p>기본적으로 또는 사용자 지정 xdc 출력 스트림으로 dpl203.xdc를 만듭니다.</p></td>
  </tr>
  <tr>
   <td><p>DPL 300 DPI </p></td>
   <td><p>DPL 300DPI 출력 스트림을 생성합니다.</p></td>
  </tr>
  <tr>
   <td><p>DPL 406 DPI </p></td>
   <td><p>DPL 400DPI 출력 스트림을 생성합니다.</p></td>
  </tr>
  <tr>
   <td><p>DPL 600 DPI </p></td>
   <td><p>DPL 600DPI 출력 스트림을 생성합니다.</p></td>
  </tr>
  <tr>
   <td><p>GenericColorPCL </p></td>
   <td><p>일반 색상 PCL(5c) 출력 스트림을 만듭니다.</p></td>
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
   <td><p>일반 모노크롬 PCL(5e) 출력 스트림을 만듭니다.</p></td>
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
   <td><p>TPCL 600DPI 출력 스트림을 만듭니다.</p></td>
  </tr>
  <tr>
   <td><p>ZPL </p></td>
   <td><p>ZPL 203DPI 출력 스트림을 만듭니다.</p></td>
  </tr>
  <tr>
   <td><p>ZPL 300 DPI </p></td>
   <td><p>ZPL 300DPI 출력 스트림을 만듭니다.</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>`generatePrintedOutput2` 메서드를 사용하여 인쇄 스트림을 프린터로 보낼 수도 있습니다. 그러나 프린터로 인쇄 스트림 전송 섹션과 관련된 빠른 시작은 `generatePrintedOutput` 메서드를 사용합니다.

**네트워크 프린터로 인쇄 스트림을 보냅니다.**

인쇄할 문서를 검색한 후 출력 서비스를 호출하여 인쇄 스트림을 네트워크 프린터로 보냅니다. 출력 서비스에서 프린터를 성공적으로 찾으려면 인쇄 서버와 프린터 이름을 모두 지정해야 합니다. 또한 인쇄 프로토콜을 지정해야 합니다.

>[!NOTE]
>
>PDFG가 Forms 서버에 설치되어 있고 서버가 Windows Server 2008에서 실행되는 경우에는 SharedPrinter 속성을 사용할 수 없습니다. 이 경우 다른 프린터 프로토콜을 사용합니다.

>[!NOTE]
>
>네트워크 프린터를 사용하고 액세스 메커니즘이 SharedPrinter인 경우 프린터의 전체 네트워크 경로를 지정해야 합니다.Java API를 사용하여 네트워크 프린터로 인쇄 스트림을 전송하십시오

출력 API(Java)를 사용하여 네트워크 프린터로 인쇄 스트림을 보냅니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-output-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. 출력 클라이언트 개체 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 `OutputClient` 개체를 만들고 `ServiceClientFactory` 개체를 전달합니다.

1. XML 데이터 소스 참조

   * 생성자를 사용하여 문서를 채우고 XML 파일의 위치를 지정하는 문자열 값을 전달하여 문서를 채우는 데 사용되는 XML 데이터 소스를 나타내는 `java.io.FileInputStream` 개체를 만듭니다.
   * 생성자를 사용하여 `com.adobe.idp.Document` 개체를 만들고 `java.io.FileInputStream` 개체를 전달합니다.

1. 인쇄 런타임 옵션 설정

   인쇄 런타임 옵션을 나타내는 `PrintedOutputOptionsSpec` 개체를 만듭니다. 예를 들어 `PrintedOutputOptionsSpec` 개체의 `setCopies` 메서드를 호출하여 인쇄할 복사본 수를 지정할 수 있습니다.

   >[!NOTE]
   >
   >ZPL 인쇄 스트림을 생성하는 경우 `PrintedOutputOptionsSpec` 개체의 `setPagination` 메서드를 사용하여 페이지 매김 값을 설정할 수 없습니다. 마찬가지로 ZPL 인쇄 스트림에 대해 다음 옵션을 설정할 수 없습니다.OutputJog, PageOffset 및 Staple입니다. `setPagination` 메서드는 PostScript 생성에 적합하지 않습니다. PCL 생성에만 유효합니다.

1. 인쇄할 문서 검색

   * `OutputClient` 개체의 `generatePrintedOutput` 메서드를 호출하고 다음 값을 전달하여 인쇄할 문서를 검색합니다.

      * 인쇄 스트림을 지정하는 `PrintFormat` 열거형 값입니다. 예를 들어 PostScript 인쇄 스트림을 만들려면 `PrintFormat.PostScript`을 전달합니다.
      * 양식 디자인의 이름을 지정하는 문자열 값입니다.
      * 이미지 파일과 같은 관련 자료 파일의 위치를 지정하는 문자열 값입니다.
      * 사용할 XDC 파일의 위치를 지정하는 문자열 값입니다.
      * 파일에 인쇄하는 데 필요한 런타임 옵션이 포함된 `PrintedOutputOptionsSpec` 개체입니다.
      * 양식 디자인과 병합할 양식 데이터가 포함된 XML 데이터 소스를 나타내는 `com.adobe.idp.Document` 개체입니다.

      이 메서드는 작업 결과를 포함하는 `OutputResult` 개체를 반환합니다.

   * `OutputResult` 개체 &#39;s `getGeneratedDoc` 메서드를 호출하여 프린터에 보낼 `com.adobe.idp.Document` 개체를 만듭니다. 이 메서드는 `com.adobe.idp.Document` 개체를 반환합니다.


1. 네트워크 프린터로 인쇄 스트림을 보냅니다.

   `OutputClient` 개체의 `sendToPrinter` 메서드를 호출하고 다음 값을 전달하여 인쇄 스트림을 네트워크 프린터로 보냅니다.

   * 프린터로 전송할 인쇄 스트림을 나타내는 `com.adobe.idp.Document` 개체입니다.
   * 사용할 프린터 프로토콜을 지정하는 `PrinterProtocol` 열거형 값입니다. 예를 들어 SharedPrinter 프로토콜을 지정하려면 `PrinterProtocol.SharedPrinter`을 전달합니다.
   * 인쇄 서버의 이름을 지정하는 문자열 값입니다. 예를 들어 인쇄 서버의 이름이 PrintServer1이라고 가정할 경우 `\\\PrintSever1`을 전달합니다.
   * 프린터의 이름을 지정하는 문자열 값입니다. 예를 들어 프린터 이름이 Printer1이라고 가정할 경우 `\\\PrintSever1\Printer1`을 전달합니다.

   >[!NOTE]
   >
   >`sendToPrinter` 메서드가 버전 8.2.1에서 AEM Forms API에 추가되었습니다.

### 웹 서비스 API {#send-a-print-stream-to-a-printer-using-the-web-service-api}를 사용하여 인쇄 스트림을 프린터로 보냅니다.

출력 API(웹 서비스)를 사용하여 네트워크 프린터로 인쇄 스트림을 보냅니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다.`http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`

   >[!NOTE]
   >
   >`localhost` 을 AEM Forms을 호스팅하는 서버의 IP 주소로 바꿉니다.

1. 출력 클라이언트 개체를 만듭니다.

   * 기본 생성자를 사용하여 `OutputServiceClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `OutputServiceClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/OutputService?blob=mtom`). `lc_version` 특성을 사용할 필요는 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다. 그러나 MTOM을 사용하려면 `?blob=mtom`을 지정하십시오.
   * `OutputServiceClient.Endpoint.Binding` 필드의 값을 가져와서 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * AEM Forms 사용자 이름을 `OutputServiceClient.ClientCredentials.UserName.UserName` 필드에 지정합니다.
      * 해당 암호 값을 `OutputServiceClient.ClientCredentials.UserName.Password` 필드에 할당합니다.
      * 상수 값 `HttpClientCredentialType.Basic`을 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.
      * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. XML 데이터 소스를 참조합니다.

   * 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 양식 데이터를 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하여 `System.IO.FileStream` 개체를 만듭니다. 양식 데이터가 포함된 XML 파일의 위치를 지정하는 문자열 값을 전달합니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열 길이를 결정합니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하고 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * `MTOM` 필드를 바이트 배열의 콘텐츠로 할당하여 `BLOB` 개체를 채웁니다.

1. 인쇄 런타임 옵션을 설정합니다.

   생성자를 사용하여 `PrintedOutputOptionsSpec` 개체를 만듭니다. 예를 들어 `PrintedOutputOptionsSpec` 개체의 `copies` 데이터 멤버에 복사본 수를 나타내는 정수 값을 할당하여 인쇄할 복사본 수를 지정할 수 있습니다.

   >[!NOTE]
   >
   >ZPL 인쇄 스트림을 생성하는 경우 `PrintedOutputOptionsSpec` 개체의 `pagination` 데이터 멤버를 사용하여 페이지 매김 값을 설정할 수 없습니다. 마찬가지로 ZPL 인쇄 스트림에 대해 다음 옵션을 설정할 수 없습니다.OutputJog, PageOffset 및 Staple입니다. `pagination` 데이터 멤버는 PostScript 생성에 적합하지 않습니다. PCL 생성에만 유효합니다.

1. 인쇄할 문서를 검색합니다.

   * `OutputServiceService` 개체의 `generatePrintedOutput` 메서드를 호출하고 다음 값을 전달하여 인쇄할 문서를 검색합니다.

      * 인쇄 스트림을 지정하는 `PrintFormat` 열거형 값입니다. 예를 들어 PostScript 인쇄 스트림을 만들려면 `PrintFormat.PostScript`을 전달합니다.
      * 양식 디자인의 이름을 지정하는 문자열 값입니다.
      * 이미지 파일과 같은 관련 자료 파일의 위치를 지정하는 문자열 값입니다.
      * 사용할 XDC 파일의 위치를 지정하는 문자열 값입니다.
      * 인쇄 스트림을 네트워크 프린터로 보낼 때 사용되는 인쇄 런타임 옵션이 포함된 `PrintedOutputOptionsSpec` 개체입니다.
      * 양식 데이터가 포함된 XML 데이터 소스를 포함하는 `BLOB` 개체입니다.
      * `generatePrintedOutput` 메서드로 채워지는 `BLOB` 개체입니다. `generatePrintedOutput` 메서드는 이 개체를 문서를 설명하는 생성된 메타데이터로 채웁니다. (이 매개 변수 값은 웹 서비스 호출에만 필요합니다.)
      * `generatePrintedOutput` 메서드로 채워지는 `BLOB` 개체입니다. `generatePrintedOutput` 메서드는 이 개체를 결과 데이터로 채웁니다. (이 매개 변수 값은 웹 서비스 호출에만 필요합니다.)
      * 작업 결과를 포함하는 `OutputResult` 개체입니다. (이 매개 변수 값은 웹 서비스 호출에만 필요합니다.)
   * `OutputResult` 개체 &#39;s `generatedDoc` 메서드 값을 가져와서 프린터에 보낼 `BLOB` 개체를 만듭니다. 이 메서드는 `generatePrintedOutput` 메서드에서 반환된 PostScript 데이터가 포함된 `BLOB` 개체를 반환합니다.


1. 인쇄 스트림을 네트워크 프린터로 보냅니다.

   `OutputClient` 개체의 `sendToPrinter` 메서드를 호출하고 다음 값을 전달하여 인쇄 스트림을 네트워크 프린터로 보냅니다.

   * 프린터로 전송할 인쇄 스트림을 나타내는 `BLOB` 개체입니다.
   * 사용할 프린터 프로토콜을 지정하는 `PrinterProtocol` 열거형 값입니다. 예를 들어 SharedPrinter 프로토콜을 지정하려면 `PrinterProtocol.SharedPrinter`을 전달합니다.
   * 이전 매개 변수 값을 사용할지 여부를 지정하는 `bool` 값입니다. 값 `true`을 전달합니다. (이 매개 변수 값은 웹 서비스 호출에만 필요합니다.)
   * 인쇄 서버의 이름을 지정하는 문자열 값입니다. 예를 들어 인쇄 서버의 이름이 PrintServer1이라고 가정할 경우 `\\\PrintSever1`을 전달합니다.
   * 프린터의 이름을 지정하는 문자열 값입니다. 예를 들어 프린터 이름이 Printer1이라고 가정할 경우 `\\\PrintSever1\Printer1`을 전달합니다.

   >[!NOTE]
   >
   >`sendToPrinter` 메서드가 버전 8.2.1에서 AEM Forms API에 추가되었습니다.

## 여러 출력 파일 만들기 {#creating-multiple-output-files}

출력 서비스는 XML 데이터 원본 내의 각 레코드나 모든 레코드가 포함된 단일 파일에 대해 별도의 문서를 만들 수 있습니다(이 기능은 기본값). 예를 들어, 10개의 레코드가 XML 데이터 소스 내에 있고 출력 서비스에서 출력 서비스 API를 사용하여 각 레코드에 대해 별도의 PDF 문서(또는 다른 유형의 출력)를 작성하도록 지시한다고 가정합니다. 그 결과 출력 서비스는 10개의 PDF 문서를 생성합니다. (문서를 만드는 대신 여러 인쇄 스트림을 프린터로 보낼 수 있습니다.)

다음 그림은 여러 개의 레코드가 포함된 XML 데이터 파일을 처리하는 출력 서비스도 보여 줍니다. 그러나 출력 서비스에 모든 데이터 레코드가 포함된 단일 PDF 문서를 작성하도록 지시한다고 가정합니다. 이 경우 출력 서비스는 모든 레코드가 포함된 하나의 문서를 생성합니다.

다음 그림은 여러 레코드가 포함된 XML 데이터 파일을 처리하는 출력 서비스를 보여 줍니다. 출력 서비스에 각 데이터 레코드에 대해 별도의 PDF 문서를 작성하도록 지시한다고 가정합니다. 이 경우 출력 서비스는 각 데이터 레코드에 대해 별도의 PDF 문서를 생성합니다.

![cm_outputbatchmany](assets/cm_outputbatchmany.png)

다음 XML 데이터는 세 개의 데이터 레코드가 포함된 데이터 파일의 예를 보여 줍니다.

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

각 데이터 레코드를 시작하고 끝나는 XML 요소는 `LoanRecord`입니다. 이 XML 요소는 여러 파일을 생성하는 응용 프로그램 논리에 의해 참조됩니다.

>[!NOTE]
>
>출력 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary_of_steps-7}

XML 데이터 소스를 기반으로 여러 PDF 파일을 만들려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. 출력 클라이언트 개체를 만듭니다.
1. XML 데이터 소스를 참조합니다.
1. PDF 런타임 옵션을 설정합니다.
1. 렌더링 런타임 옵션을 설정합니다.
1. 여러 PDF 파일을 생성합니다.
1. 작업의 결과를 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함하십시오. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms이 JBoss에 배포되는 경우 필요)

AEM Forms이 JBoss가 아닌 지원되는 J2EE 애플리케이션 서버에 배포되는 경우 adobe-utilities.jar 및 jbossall-client.jar 파일을 AEM Forms이 배포된 J2EE 애플리케이션 서버와 관련된 JAR 파일로 대체해야 합니다.

**출력 클라이언트 개체 만들기**

출력 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 출력 서비스 클라이언트 개체를 만들어야 합니다. Java API를 사용하는 경우 `OutputClient` 개체를 만듭니다. 출력 웹 서비스 API를 사용하는 경우 `OutputServiceService` 개체를 만듭니다.

**XML 데이터 소스 참조**

여러 레코드가 포함된 XML 데이터 소스를 참조합니다. 데이터 레코드를 구분하려면 XML 요소를 사용해야 합니다. 예를 들어 이 섹션 앞에 표시된 XML 데이터 소스 예제에서 데이터 레코드를 구분하는 XML 요소의 이름은 `LoanRecord`입니다.

데이터로 채울 모든 양식 필드에 대해 XML 요소가 있어야 합니다. XML 요소 이름은 필드 이름과 일치해야 합니다. XML 요소는 양식 필드에 해당하지 않거나 XML 요소 이름이 필드 이름과 일치하지 않는 경우에는 무시됩니다. 모든 XML 요소가 지정된 경우 XML 요소가 표시되는 순서와 일치하지 않아도 됩니다.

**PDF 런타임 옵션 설정**

XML 데이터 소스를 기반으로 여러 파일을 성공적으로 만들려면 출력 서비스에 대해 다음 런타임 옵션을 설정해야 합니다.

* **많은 파일**:출력 서비스에서 단일 문서를 만들지 여러 문서를 만들지 여부를 지정합니다. true 또는 false를 지정할 수 있습니다. XML 데이터 소스의 각 데이터 레코드에 대해 별도의 문서를 만들려면 true를 지정합니다.
* **파일 URI**:출력 서비스에서 생성하는 파일의 위치를 지정합니다. 예를 들어 C:\\Adobe\forms\Loan.pdf 을 지정한다고 가정해 보겠습니다. 이 경우 출력 서비스는 Loan.pdf 파일을 만들고 C:\\Adobe\forms folder폴더에 파일을 넣습니다. 여러 파일이 있는 경우 파일 이름은 Loan0001.pdf, Loan0002.pdf, Loan003.pdf 등입니다. 파일 위치를 지정하면 클라이언트 컴퓨터가 아닌 서버에 파일이 배치됩니다.
* **레코드 이름**:데이터 레코드를 구분하는 데이터 소스의 XML 요소 이름을 지정합니다. 예를 들어 이 섹션 앞에 표시된 XML 데이터 소스 예제에서 데이터 레코드를 구분하는 XML 요소를 `LoanRecord` 이라고 합니다. 레코드 이름 런타임 옵션을 설정하는 대신 데이터 레코드가 포함된 요소 레벨을 나타내는 숫자 값을 지정하여 레코드 수준을 설정할 수 있습니다. 그러나 레코드 이름 또는 레코드 수준만 설정할 수 있습니다. 두 값을 모두 설정할 수 없습니다.)

**렌더링 런타임 옵션 설정**

여러 파일을 만드는 동안 렌더링 런타임 옵션을 설정할 수 있습니다. 이러한 옵션이 필요하지 않지만(필요한 출력 런타임 옵션과 달리) 출력 서비스의 성능 향상과 같은 작업을 수행할 수 있습니다. 예를 들어 출력 서비스에서 성능을 개선하기 위해 사용하는 양식 디자인을 캐시할 수 있습니다.

출력 서비스에서 일괄 레코드를 처리하면 여러 레코드가 포함된 데이터를 증분 방식으로 읽습니다. 즉, 출력 서비스는 데이터를 메모리로 읽고 레코드 일괄 처리가 처리되면 데이터를 해제합니다. 두 개의 런타임 옵션 중 하나가 설정되면 출력 서비스는 데이터를 증분 방식으로 로드합니다. 레코드 이름 런타임 옵션을 설정하면 출력 서비스가 데이터를 증분 방식으로 읽습니다. 마찬가지로, 레코드 수준 런타임 옵션을 2 이상으로 설정하면 출력 서비스는 증분 방식으로 데이터를 읽습니다.

출력 서비스에서 `PDFOutputOptionsSpec` 또는 `PrintedOutputOptionSpec` 개체의 `setLazyLoading` 메서드를 사용하여 증분 로드를 수행하는지 여부를 제어할 수 있습니다. 이 메서드에 `false` 값을 전달하여 증분 로드를 해제할 수 있습니다.

**여러 PDF 파일 생성**

여러 데이터 레코드가 포함된 유효한 XML 데이터 소스를 참조하고 런타임 옵션을 설정한 후에는 출력 서비스를 호출하여 여러 파일을 생성할 수 있습니다. 여러 레코드를 생성할 때 `OutputResult` 개체의 `getGeneratedDoc` 메서드는 `null`를 반환합니다.

**작업 결과 검색**

출력 서비스에서 작업을 수행하면 작업이 성공했는지 여부를 지정하는 XML 데이터가 반환됩니다. 출력 서비스에서 다음 XML을 반환합니다. 이 경우 출력 서비스에서 42개의 문서를 생성했습니다.

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

### Java API {#create-multiple-pdf-files-using-the-java-api}를 사용하여 여러 PDF 파일 만들기

출력 API(Java)를 사용하여 여러 PDF 파일을 만듭니다.

1. 프로젝트 파일 포함&quot;

   Java 프로젝트의 클래스 경로에 adobe-output-client.jar와 같은 클라이언트 JAR 파일을 포함합니다..

1. 출력 클라이언트 개체 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 `OutputClient` 개체를 만들고 `ServiceClientFactory` 개체를 전달합니다.

1. XML 데이터 소스 참조

   * 생성자를 사용하여 여러 레코드를 포함하는 XML 데이터 소스를 나타내는 `java.io.FileInputStream` 개체를 만들고 XML 파일의 위치를 지정하는 문자열 값을 전달합니다.
   * 생성자를 사용하여 `com.adobe.idp.Document` 개체를 만들고 `java.io.FileInputStream` 개체를 전달합니다.

1. PDF 런타임 옵션 설정

   * 생성자를 사용하여 `PDFOutputOptionsSpec` 개체를 만듭니다.
   * `PDFOutputOptionsSpec` 개체의 `setGenerateManyFiles` 메서드를 호출하여 여러 파일 옵션을 설정합니다. 예를 들어 값 `true`을 전달하여 출력 서비스에서 XML 데이터 소스의 각 레코드에 대해 별도의 PDF 파일을 만들도록 지시합니다. ( `false`을 전달하면 출력 서비스에서 모든 레코드가 포함된 단일 PDF 문서를 생성합니다.)
   * `PDFOutputOptionsSpec` 개체의 `setFileUri` 메서드를 호출하고 출력 서비스에서 생성하는 파일의 위치를 지정하는 문자열 값을 전달하여 파일 URI 옵션을 설정합니다. 파일 URI 옵션은 클라이언트 컴퓨터가 아닌 AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버에 상대적입니다.
   * `OutputOptionsSpec` 개체의 `setRecordName` 메서드를 호출하고 데이터 레코드를 구분하는 데이터 소스에서 XML 요소 이름을 지정하는 문자열 값을 전달하여 레코드 이름 옵션을 설정합니다. 예를 들어 이 섹션 앞에 표시된 XML 데이터 소스를 고려해 보십시오. 데이터 레코드를 구분하는 XML 요소의 이름은 LoanRecord)입니다.

1. 렌더링 런타임 옵션 설정

   * 생성자를 사용하여 `RenderOptionsSpec` 개체를 만듭니다.
   * 양식 디자인을 캐시하여 `RenderOptionsSpec` 개체의 `setCacheEnabled`을 호출하고 `true`의 `Boolean` 값을 전달하여 출력 서비스의 성능을 개선합니다.

1. 여러 PDF 파일 생성

   `OutputClient` 개체의 `generatePDFOutput` 메서드를 호출하고 다음 값을 전달하여 여러 PDF 파일을 생성합니다.

   * `TransformationFormat` 열거형 값. PDF 문서를 생성하려면 `TransformationFormat.PDF`을 지정합니다.
   * 양식 디자인의 이름을 지정하는 문자열 값입니다.
   * 양식 디자인이 있는 컨텐츠 루트를 지정하는 문자열 값입니다.
   * PDF 런타임 옵션이 포함된 `PDFOutputOptionsSpec` 개체입니다.
   * 렌더링 런타임 옵션이 포함된 `RenderOptionsSpec` 개체입니다.
   * 양식 디자인과 병합할 데이터가 포함된 XML 데이터 소스가 포함된 `com.adobe.idp.Document` 개체입니다.

   `generatePDFOutput` 메서드는 작업 결과를 포함하는 `OutputResult` 개체를 반환합니다.

1. 작업 결과 검색

   * `generatePDFOutput` 메서드의 결과를 포함할 XML 파일을 나타내는 `java.io.File` 개체를 만듭니다. 파일 이름 확장명이 .xml인지 확인합니다.
   * `com.adobe.idp.Document` 개체의 `copyToFile` 메서드를 호출하여 `com.adobe.idp.Document` 개체의 내용을 파일에 복사합니다. `applyUsageRights` 메서드에서 반환된 `com.adobe.idp.Document` 개체를 사용해야 합니다.

**참고 항목**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[빠른 시작(EJB 모드):Java API를 사용하여 여러 PDF 파일 만들기](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-multiple-pdf-files-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API {#create-multiple-pdf-files-using-the-web-service-api}를 사용하여 여러 PDF 파일 만들기

출력 API(웹 서비스)를 사용하여 여러 PDF 파일을 만들 수 있습니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다.`http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`

   >[!NOTE]
   >
   >`localhost` 을 AEM Forms을 호스팅하는 서버의 IP 주소로 바꿉니다.

1. 출력 클라이언트 개체를 만듭니다.

   * 기본 생성자를 사용하여 `OutputServiceClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `OutputServiceClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/OutputService?blob=mtom`). `lc_version` 특성을 사용할 필요는 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다. 그러나 MTOM을 사용하려면 `?blob=mtom`을 지정하십시오.
   * `OutputServiceClient.Endpoint.Binding` 필드의 값을 가져와서 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * AEM Forms 사용자 이름을 `OutputServiceClient.ClientCredentials.UserName.UserName` 필드에 지정합니다.
      * 해당 암호 값을 `OutputServiceClient.ClientCredentials.UserName.Password` 필드에 할당합니다.
      * 상수 값 `HttpClientCredentialType.Basic`을 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.
      * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. XML 데이터 소스를 참조합니다.

   * 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 여러 레코드가 포함된 양식 데이터를 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하여 `System.IO.FileStream` 개체를 만듭니다. 여러 레코드가 포함된 XML 파일의 파일 위치를 나타내는 문자열 값을 전달합니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하고 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * `MTOM` 필드를 바이트 배열의 콘텐츠로 할당하여 `BLOB` 개체를 채웁니다.

1. PDF 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 `PDFOutputOptionsSpec` 개체를 만듭니다.
   * `OutputOptionsSpec` 개체의 `generateManyFiles` 데이터 멤버에 부울 값을 할당하여 [많은 파일] 옵션을 설정합니다. 예를 들어, 이 데이터 멤버에 `true` 값을 할당하여 출력 서비스에서 XML 데이터 소스의 각 레코드에 대해 별도의 PDF 파일을 만들도록 지시합니다. (`false`을 이 데이터 구성원에게 지정하는 경우 출력 서비스는 모든 레코드가 포함된 단일 PDF를 생성합니다.)
   * 출력 서비스에서 생성하는 파일의 위치를 `OutputOptionsSpec` 개체의 `fileURI` 데이터 멤버에 지정하는 문자열 값을 할당하여 파일 URI 옵션을 설정합니다. 파일 URI 옵션은 클라이언트 컴퓨터가 아닌 AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버에 상대적입니다.
   * 데이터 레코드를 `OutputOptionsSpec` 개체의 `recordName` 데이터 멤버로 구분하는 데이터 원본에서 XML 요소 이름을 지정하는 문자열 값을 할당하여 레코드 이름 옵션을 설정합니다.
   * 출력 서비스에서 생성하는 복사본 수를 `OutputOptionsSpec` 개체의 `copies` 데이터 멤버에 지정하는 정수 값을 할당하여 복사 옵션을 설정합니다.

1. 렌더링 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 `RenderOptionsSpec` 개체를 만듭니다.
   * 양식 디자인을 캐시하여 `true` 값을 `RenderOptionsSpec` 개체의 `cacheEnabled` 데이터 멤버에 할당하여 출력 서비스의 성능을 향상시킵니다.

1. 여러 PDF 파일을 생성합니다.

   `OutputServiceService` 개체의 `generatePDFOutput` 메서드를 호출하고 다음 값을 전달하여 여러 PDF 파일을 만듭니다.

   * TransformationFormat 열거형 값입니다. PDF 문서를 생성하려면 `TransformationFormat.PDF`을 지정합니다.
   * 양식 디자인의 이름을 지정하는 문자열 값입니다.
   * 양식 디자인이 있는 컨텐츠 루트를 지정하는 문자열 값입니다.
   * PDF 런타임 옵션이 포함된 `PDFOutputOptionsSpec` 개체입니다.
   * 렌더링 런타임 옵션이 포함된 `RenderOptionsSpec` 개체입니다.
   * 양식 디자인과 병합할 데이터가 포함된 XML 데이터 소스가 포함된 `BLOB` 개체입니다.
   * `generatePDFOutput` 메서드로 채워지는 `BLOB` 개체입니다. `generatePDFOutput` 메서드는 이 개체를 문서를 설명하는 생성된 메타데이터로 채웁니다.
   * `generatePDFOutput` 메서드로 채워지는 `BLOB` 개체입니다. `generatePDFOutput` 메서드는 이 개체를 결과 데이터로 채웁니다.
   * 작업 결과를 포함하는 `OutputResult` 개체입니다.

1. 작업 결과 검색

   * 해당 생성자를 호출하고 결과 데이터가 포함된 XML 파일 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다. 파일 이름 확장명이 .xml인지 확인합니다.
   * `OutputServiceService` 개체의 `generatePDFOutput` 메서드(8번째 매개 변수)로 결과 데이터로 채워지는 `BLOB` 개체의 데이터 콘텐츠를 저장하는 바이트 배열을 만듭니다. `BLOB` 개체의 `binaryData` 데이터 멤버의 값을 가져와서 바이트 배열을 채웁니다.
   * 해당 생성자를 호출하고 `System.IO.FileStream` 개체를 전달하여 `System.IO.BinaryWriter` 개체를 만듭니다.
   * `System.IO.BinaryWriter` 개체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 XML 파일에 씁니다.

**참고 항목**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 검색 규칙 만들기 {#creating-search-rules}

출력 서비스에서 입력 데이터를 검사하고 데이터 컨텐츠를 기반으로 다른 양식 디자인을 사용하여 출력을 생성하는 검색 규칙을 만들 수 있습니다. 예를 들어 텍스트 *모기지*&#x200B;가 입력 데이터 내에 있는 경우 출력 서비스에서 Moderation.xdp라는 양식 디자인을 사용할 수 있습니다. 마찬가지로, *자동차* 텍스트가 입력 데이터에 있으면 출력 서비스는 CarLoan.xdp로 저장된 양식 디자인을 사용할 수 있습니다. 출력 서비스에서 다른 출력 유형을 생성할 수 있지만 이 섹션에서는 출력 서비스에서 PDF 파일을 생성한다고 가정합니다. 다음 다이어그램은 XML 데이터 파일을 처리하고 많은 양식 디자인 중 하나를 사용하여 PDF 파일을 생성하는 출력 서비스를 보여 줍니다.

또한, 출력 서비스는 문서 패키지를 생성할 수 있으며, 이 경우 데이터 세트에 여러 개의 레코드가 제공되고 각 레코드는 양식 디자인에 대응되며 하나의 문서는 여러 양식 디자인으로 생성됩니다.

![cs_outputbatchmanyformdesigns2](assets/cs_outputbatchmanyformdesigns2.png)

>[!NOTE]
>
>출력 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary_of_steps-8}

문서를 생성하는 동안 검색 규칙을 사용하도록 출력 서비스에 지시하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. 출력 클라이언트 개체를 만듭니다.
1. XML 데이터 소스를 참조합니다.
1. 검색 규칙을 정의합니다.
1. PDF 런타임 옵션을 설정합니다.
1. 렌더링 런타임 옵션을 설정합니다.
1. PDF 문서를 생성합니다.
1. 작업의 결과를 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

다음 JAR 파일을 프로젝트의 클래스 경로에 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms이 JBoss에 배포되는 경우 필수)

AEM Forms이 JBoss가 아닌 지원되는 J2EE 애플리케이션 서버에 배포된 경우, adobe-utilities.jar 및 jbossall-client.jar를 AEM Forms이 배포된 J2EE 애플리케이션 서버와 관련된 JAR 파일로 대체해야 합니다.

**출력 클라이언트 개체 만들기**

출력 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 출력 서비스 클라이언트 개체를 만들어야 합니다.

**XML 데이터 소스 참조**

데이터로 채울 모든 양식 필드에 대해 XML 요소가 있어야 합니다. XML 요소 이름은 필드 이름과 일치해야 합니다. XML 요소는 양식 필드에 해당하지 않거나 XML 요소 이름이 필드 이름과 일치하지 않는 경우에는 무시됩니다. 모든 XML 요소를 지정하는 한 XML 요소가 표시되는 순서와 일치하지 않아도 됩니다.

**검색 규칙 정의**

검색 규칙을 정의하려면 출력 서비스에서 입력 데이터에서 검색하는 하나 이상의 텍스트 패턴을 정의합니다. 정의한 각 텍스트 패턴에 대해 텍스트 패턴이 있는 경우 사용되는 해당 양식 디자인을 지정합니다. 텍스트 패턴이 있으면 출력 서비스에서 해당 양식 디자인을 사용하여 출력을 생성합니다. 텍스트 패턴의 예는 *moderation*&#x200B;입니다.

>[!NOTE]
>
>텍스트 패턴을 찾을 수 없으면 기본 양식이 사용됩니다. 사용하는 모든 양식 디자인이 콘텐츠 루트에 있는지 확인하십시오.

**PDF 런타임 옵션 설정**

출력 서비스에서 여러 양식 디자인을 기반으로 PDF 문서를 성공적으로 만들려면 다음 PDF 런타임 옵션을 설정합니다.

* **파일 URI**:출력 서비스에서 생성하는 PDF 파일의 이름과 위치를 지정합니다.
* **규칙**:정의한 규칙을 지정합니다.
* **LookAhead**:정의된 텍스트 패턴을 검색할 입력 데이터 파일의 시작 부분에서 사용할 바이트 수를 지정합니다. 기본값은 500바이트입니다.

**렌더링 런타임 옵션 설정**

PDF 파일을 만드는 동안 렌더링 런타임 옵션을 설정할 수 있습니다. 이러한 옵션이 필요하지 않지만(PDF 런타임 옵션과 달리) 출력 서비스의 성능 향상과 같은 작업을 수행할 수 있습니다. 예를 들어 출력 서비스에서 성능을 개선하기 위해 사용하는 양식 디자인을 캐시할 수 있습니다.

**PDF 문서 생성**

유효한 XML 데이터 소스를 참조하고 런타임 옵션을 설정한 후에는 출력 서비스를 호출하여 PDF 문서를 생성할 수 있습니다. 출력 서비스에서 입력 데이터에 지정된 텍스트 패턴을 찾으면 해당 양식 디자인을 사용합니다. 텍스트 패턴을 사용하지 않으면 출력 서비스에서 기본 양식 디자인을 사용합니다.

**작업 결과 검색**

출력 서비스에서 작업을 수행하면 작업이 성공했는지 여부를 지정하는 XML 데이터가 반환됩니다.

**참고 항목**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[출력 서비스 API 빠른 시작](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java API {#create-search-rules-using-the-java-api}를 사용하여 검색 규칙 만들기

출력 API(Java)를 사용하여 검색 규칙을 만듭니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-output-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. 출력 클라이언트 개체를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 `OutputClient` 개체를 만들고 `ServiceClientFactory` 개체를 전달합니다.

1. XML 데이터 소스를 참조합니다.

   * 생성자를 사용하여 PDF 문서를 채우고 XML 파일의 위치를 지정하는 문자열 값을 전달하여 PDF 문서를 채우는 데 사용되는 XML 데이터 소스를 나타내는 `java.io.FileInputStream` 개체를 만듭니다.
   * 생성자를 사용하여 `com.adobe.idp.Document` 개체를 만들고 `java.io.FileInputStream` 개체를 전달합니다.

1. 검색 규칙을 정의합니다.

   * 생성자를 사용하여 `Rule` 개체를 만듭니다.
   * `Rule` 개체의 `setPattern` 메서드를 호출하고 텍스트 패턴을 지정하는 문자열 값을 전달하여 텍스트 패턴을 정의합니다.
   * `Rule` 개체의 `setForm` 메서드를 호출하여 해당 양식 디자인을 정의합니다. 양식 디자인의 이름을 지정하는 문자열 값을 전달합니다.

   >[!NOTE]
   >
   >정의할 각 텍스트 패턴에 대해 이전 세 가지 하위 단계를 반복합니다.

   * `java.util.ArrayList` 생성자를 사용하여 `java.util.List` 개체를 만듭니다.
   * 생성한 각 `Rule` 개체에 대해 `java.util.List` 개체의 `add` 메서드를 호출하고 `Rule` 개체를 전달합니다.


1. PDF 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 `PDFOutputOptionsSpec` 개체를 만듭니다.
   * `PDFOutputOptionsSpec` 개체의 `setFileURI` 메서드를 호출하여 출력 서비스에서 생성하는 PDF 파일의 이름과 위치를 지정합니다. PDF 파일의 위치를 지정하는 문자열 값을 전달합니다. 파일 URI 옵션은 클라이언트 컴퓨터가 아닌 AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버에 상대적입니다.
   * `PDFOutputOptionsSpec` 개체의 `setRules` 메서드를 호출하여 정의한 규칙을 설정합니다. `Rule` 개체가 포함된 `java.util.List` 개체를 전달합니다.
   * `PDFOutputOptionsSpec` 개체의 `setLookAhead` 메서드를 호출하여 정의된 텍스트 패턴을 검색할 바이트 수를 설정합니다. 바이트 수를 나타내는 정수 값을 전달합니다.

1. 렌더링 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 `RenderOptionsSpec` 개체를 만듭니다.
   * 양식 디자인을 캐시하여 `RenderOptionsSpec` 개체의 `setCacheEnabled`을 호출하고 `true`를 전달하여 출력 서비스의 성능을 향상시킵니다.

1. PDF 문서를 생성합니다.

   `OutputClient` 개체의 `generatePDFOutput` 메서드를 호출하고 다음 값을 전달하여 여러 양식 디자인을 기반으로 하는 PDF 문서를 생성합니다.

   * `TransformationFormat` 열거형 값입니다. PDF 문서를 생성하려면 `TransformationFormat.PDF`을 지정합니다.
   * 기본 양식 디자인의 이름을 지정하는 문자열 값입니다. 즉, 텍스트 패턴이 없는 경우 사용되는 양식 디자인입니다.
   * 양식 디자인이 있는 컨텐츠 루트를 지정하는 문자열 값입니다.
   * PDF 런타임 옵션이 포함된 `PDFOutputOptionsSpec` 개체입니다.
   * 렌더링 런타임 옵션이 포함된 `RenderOptionsSpec` 개체입니다.
   * 정의된 텍스트 패턴에 대해 출력 서비스에서 검색하는 양식 데이터가 포함된 `com.adobe.idp.Document` 개체입니다.

   `generatePDFOutput` 메서드는 작업 결과를 포함하는 `OutputResult` 개체를 반환합니다.

1. 작업의 결과를 검색합니다.

   * `OutputResult` 개체의 `getStatusDoc` 메서드를 호출하여 `generatePDFOutput` 메서드의 상태를 나타내는 `com.adobe.idp.Document` 개체를 만듭니다.
   * 작업 결과를 포함할 `java.io.File` 개체를 만듭니다. 파일 확장명이 .xml인지 확인합니다.
   * `com.adobe.idp.Document` 개체의 `copyToFile` 메서드를 호출하여 `com.adobe.idp.Document` 개체의 내용을 파일에 복사합니다. `getStatusDoc` 메서드에서 반환된 `com.adobe.idp.Document` 개체를 사용해야 합니다.

**참고 항목**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[빠른 시작(EJB 모드):Java API를 사용하여 검색 규칙 만들기](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 검색 규칙 만들기](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API {#create-search-rules-using-the-web-service-api}를 사용하여 검색 규칙 만들기

출력 API(웹 서비스)를 사용하여 검색 규칙을 만듭니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다.`http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`

   >[!NOTE]
   >
   >`localhost` 을 AEM Forms을 호스팅하는 서버의 IP 주소로 바꿉니다.

1. 출력 클라이언트 개체를 만듭니다.

   * 기본 생성자를 사용하여 `OutputServiceClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `OutputServiceClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/OutputService?blob=mtom`). `lc_version` 특성을 사용할 필요는 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다. 그러나 MTOM을 사용하려면 `?blob=mtom`을 지정하십시오.
   * `OutputServiceClient.Endpoint.Binding` 필드의 값을 가져와서 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * AEM Forms 사용자 이름을 `OutputServiceClient.ClientCredentials.UserName.UserName` 필드에 지정합니다.
      * 해당 암호 값을 `OutputServiceClient.ClientCredentials.UserName.Password` 필드에 할당합니다.
      * 상수 값 `HttpClientCredentialType.Basic`을 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.
      * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. XML 데이터 소스를 참조합니다.

   * 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 PDF 문서와 병합될 데이터를 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하고 암호화할 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하고 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * `MTOM` 필드를 바이트 배열의 콘텐츠로 할당하여 `BLOB` 개체를 채웁니다.

1. 검색 규칙을 정의합니다.

   * 생성자를 사용하여 `Rule` 개체를 만듭니다.
   * `Rule` 개체의 `pattern` 데이터 멤버에 텍스트 패턴을 지정하는 문자열 값을 할당하여 텍스트 패턴을 정의합니다.
   * 양식 디자인을 지정하는 문자열 값을 `Rule` 개체의 `form` 데이터 멤버에 할당하여 해당 양식 디자인을 정의합니다.

   >[!NOTE]
   >
   >정의할 각 텍스트 패턴에 대해 이전 세 가지 하위 단계를 반복합니다.

   * 규칙을 저장하는 `MyArrayOf_xsd_anyType` 개체를 만듭니다.
   * 각 `Rule` 개체를 `MyArrayOf_xsd_anyType` 배열의 요소에 할당합니다. 각 `Rule` 개체에 대해 `MyArrayOf_xsd_anyType` 개체의 `Add` 메서드를 호출합니다.


1. PDF 런타임 옵션 설정

   * 생성자를 사용하여 `PDFOutputOptionsSpec` 개체를 만듭니다.
   * 출력 서비스에서 생성하는 PDF 파일의 위치를 `PDFOutputOptionsSpec` 개체의 `fileURI` 데이터 멤버에 지정하는 문자열 값을 할당하여 파일 URI 옵션을 설정합니다. 파일 URI 옵션은 클라이언트 컴퓨터가 아닌 AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버에 상대적입니다.
   * 출력 서비스에서 생성하는 복사본 수를 `PDFOutputOptionsSpec` 개체의 `copies` 데이터 멤버에 지정하는 정수 값을 할당하여 복사 옵션을 설정합니다.
   * 규칙을 저장하는 `MyArrayOf_xsd_anyType` 개체를 `PDFOutputOptionsSpec` 개체의 `rules` 데이터 멤버에 할당하여 정의한 규칙을 설정합니다.
   * `PDFOutputOptionsSpec` 개체의 `lookAhead` 데이터 메서드에 검사할 바이트 수를 나타내는 정수 값을 할당하여 정의된 텍스트 패턴을 검색할 바이트 수를 설정합니다.

1. 렌더링 런타임 옵션 설정

   * 생성자를 사용하여 `RenderOptionsSpec` 개체를 만듭니다.
   * `RenderOptionsSpec` 개체의 `cacheEnabled` 데이터 멤버에 `true` 값을 할당하여 출력 서비스의 성능을 향상시키기 위해 양식 디자인을 캐시합니다.

   >[!NOTE]
   >
   >입력 문서가 Acrobat 양식인 경우 `RenderOptionsSpec` 개체의 `pdfVersion` 멤버를 사용하여 PDF 문서 버전을 설정할 수 없습니다. 출력 PDF 문서는 Acrobat 양식의 PDF 버전을 유지합니다. 마찬가지로 입력 문서가 Acrobat 양식인 경우 `RenderOptionsSpec` 개체의 `taggedPDF` 메서드를 사용하여 태그가 지정된 PDF 옵션을 설정할 수 없습니다.

   >[!NOTE]
   >
   >입력 PDF 문서가 인증되거나 디지털 서명된 경우 `RenderOptionsSpec` 개체의 `linearizedPDF` 멤버를 사용하여 선형화된 PDF 옵션을 설정할 수 없습니다. 자세한 내용은 [PDF 문서에 디지털 서명](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)을 참조하십시오.

1. PDF 문서 생성

   `OutputServiceService` 개체의 `generatePDFOutput` 메서드를 호출하고 다음 값을 전달하여 PDF 문서를 만듭니다.

   * `TransformationFormat` 열거형 값입니다. PDF 문서를 생성하려면 `TransformationFormat.PDF`을 지정합니다.
   * 양식 디자인의 이름을 지정하는 문자열 값입니다.
   * 양식 디자인이 있는 컨텐츠 루트를 지정하는 문자열 값입니다.
   * PDF 런타임 옵션이 포함된 `PDFOutputOptionsSpec` 개체입니다.
   * 렌더링 런타임 옵션이 포함된 `RenderOptionsSpec` 개체입니다.
   * 양식 디자인과 병합할 데이터가 포함된 XML 데이터 소스가 포함된 `BLOB` 개체입니다.
   * `generatePDFOutput` 메서드로 채워지는 `BLOB` 개체입니다. `generatePDFOutput` 메서드는 이 개체를 문서를 설명하는 생성된 메타데이터로 채웁니다. (이 매개 변수 값은 웹 서비스 호출에만 필요합니다.)
   * `generatePDFOutput` 메서드로 채워지는 `BLOB` 개체입니다. `generatePDFOutput` 메서드는 이 개체를 결과 데이터로 채웁니다. (이 매개 변수 값은 웹 서비스 호출에만 필요합니다.)
   * 작업 결과를 포함하는 `OutputResult` 개체입니다. (이 매개 변수 값은 웹 서비스 호출에만 필요합니다.)

   >[!NOTE]
   >
   >`generatePDFOutput` 메서드를 호출하여 PDF 문서를 생성하는 경우 서명, 인증 또는 사용 권한이 있는 XFA PDF 양식과 데이터를 병합할 수 없습니다. 사용 권한에 대한 자세한 내용은 [PDF 문서에 사용 권한 적용](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)을 참조하십시오.

1. 작업 결과 검색

   * 해당 생성자를 호출하고 결과 데이터가 포함된 XML 파일 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다. 파일 확장명이 XML인지 확인합니다.
   * `OutputServiceService` 개체의 `generatePDFOutput` 메서드(8번째 매개 변수)로 결과 데이터로 채워지는 `BLOB` 개체의 데이터 콘텐츠를 저장하는 바이트 배열을 만듭니다. `BLOB` 개체의 `MTOM` 데이터 멤버의 값을 가져와서 바이트 배열을 채웁니다.
   * 해당 생성자를 호출하고 `System.IO.FileStream` 개체를 전달하여 `System.IO.BinaryWriter` 개체를 만듭니다.
   * `System.IO.BinaryWriter` 개체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 XML 파일에 씁니다.

**참고 항목**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## PDF 문서 병합 {#flattening-pdf-documents}

출력 서비스를 사용하여 대화형 PDF 문서를 비대화형 PDF로 변환할 수 있습니다. 대화형 PDF 문서를 사용하면 PDF 문서 필드에 있는 데이터를 입력하거나 수정할 수 있습니다. 대화형 PDF 문서를 비대화형 PDF 문서로 변환하는 프로세스를 *flating*&#x200B;이라고 합니다. PDF 문서를 병합하면 사용자가 문서 필드의 데이터를 수정할 수 없습니다. PDF 문서를 평면화하는 한 가지 이유는 데이터를 수정할 수 없도록 하기 위한 것입니다.

다음과 같은 유형의 PDF 문서를 병합할 수 있습니다.

* 대화형 XFA PDF 문서
* Acrobat Forms

비대화형 PDF 문서인 PDF를 병합하려고 하면 예외가 발생합니다.

>[!NOTE]
>
>출력 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary_of_steps-9}

대화형 PDF 문서를 비대화형 PDF 문서로 병합하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. 출력 클라이언트 개체를 만듭니다.
1. 대화형 PDF 문서를 검색합니다.
1. PDF 문서를 변형합니다.
1. 비대화형 PDF 문서를 PDF 파일로 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함하십시오. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms이 JBoss에 배포되는 경우 필요)

AEM Forms이 JBoss가 아닌 지원되는 J2EE 애플리케이션 서버에 배포되는 경우 adobe-utilities.jar 및 jbossall-client.jar 파일을 AEM Forms이 배포된 J2EE 애플리케이션 서버와 관련된 JAR 파일로 대체해야 합니다. 모든 AEM Forms JAR 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)을 참조하십시오.

**출력 클라이언트 개체 만들기**

출력 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 출력 서비스 클라이언트 개체를 만들어야 합니다. Java API를 사용하는 경우 `OutputClient` 개체를 만듭니다. 출력 웹 서비스 API를 사용하는 경우 `OutputServiceService` 개체를 만듭니다.

**대화형 PDF 문서 검색**

비대화형 PDF 문서로 변환할 대화형 PDF 문서를 검색합니다. 비대화형 PDF 문서를 변환하려고 하면 예외가 발생합니다.

**PDF 문서 변환**

대화형 PDF 문서를 검색한 후 비대화형 PDF 문서로 변환할 수 있습니다. 출력 서비스는 비대화형 PDF 문서를 반환합니다.

**비대화형 PDF 문서를 PDF 파일로 저장**

비대화형 PDF 문서를 PDF 파일로 저장할 수 있습니다.

**참고 항목**

[Java API를 사용하여 PDF 문서 평면화](creating-document-output-streams.md#flatten-a-pdf-document-using-the-java-api)

[웹 서비스 API를 사용하여 PDF 문서 평면화](creating-document-output-streams.md#flatten-a-pdf-document-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[출력 서비스 API 빠른 시작](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java API {#flatten-a-pdf-document-using-the-java-api}를 사용하여 PDF 문서 평면화

출력 API(Java)를 사용하여 대화형 PDF 문서를 비대화형 PDF 문서로 병합합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-output-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. 출력 클라이언트 개체를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 `OutputClient` 개체를 만들고 `ServiceClientFactory` 개체를 전달합니다.

1. 대화형 PDF 문서를 검색합니다.

   * 생성자를 사용하여 변환할 대화형 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만들고 대화형 PDF 파일의 위치를 지정하는 문자열 값을 전달합니다.
   * 생성자를 사용하여 `com.adobe.idp.Document` 개체를 만들고 `java.io.FileInputStream` 개체를 전달합니다.

1. PDF 문서를 변형합니다.

   `OutputServiceService` 개체의 `transformPDF` 메서드를 호출하고 다음 값을 전달하여 대화형 PDF 문서를 비대화형 PDF 문서로 변환합니다.

   * 대화형 PDF 문서가 포함된 `com.adobe.idp.Document` 개체입니다.
   * `TransformationFormat` 열거형 값. 비대화형 PDF 문서를 생성하려면 `TransformationFormat.PDF`을 지정합니다.
   * 개정 번호를 지정하는 `PDFARevisionNumber` 열거형 값. 이 매개 변수는 PDF/A 문서를 위한 것이므로 `null`을 지정할 수 있습니다.
   * 콜론으로 구분되는 수정 번호 및 연도를 나타내는 문자열 값입니다. 이 매개 변수는 PDF/A 문서를 위한 것이므로 `null`을 지정할 수 있습니다.
   * PDF/A 적합성 수준을 나타내는 `PDFAConformance` 열거형 값. 이 매개 변수는 PDF/A 문서를 위한 것이므로 `null`을 지정할 수 있습니다.

   `transformPDF` 메서드는 비대화형 PDF 문서가 포함된 `com.adobe.idp.Document` 개체를 반환합니다.

1. 비대화형 PDF 문서를 PDF 파일로 저장합니다.

   * `java.io.File` 개체를 만들고 파일 이름 확장명이 .pdf인지 확인합니다.
   * `Document` 개체의 `copyToFile` 메서드를 호출하여 `Document` 개체의 내용을 파일에 복사합니다. `transformPDF` 메서드에서 반환된 `Document` 개체를 사용해야 합니다.

**참고 항목**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[빠른 시작(EJB 모드):Java API를 사용하여 PDF 문서 변환](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 PDF 문서 변환](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API {#flatten-a-pdf-document-using-the-web-service-api}를 사용하여 PDF 문서 평면화

출력 API(웹 서비스)를 사용하여 대화형 PDF 문서를 비대화형 PDF 문서로 병합합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다.`http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`

   >[!NOTE]
   >
   >`localhost` 을 AEM Forms을 호스팅하는 서버의 IP 주소로 바꿉니다.

1. 출력 클라이언트 개체를 만듭니다.

   * 기본 생성자를 사용하여 `OutputServiceClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `OutputServiceClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/OutputService?blob=mtom`). `lc_version` 특성을 사용할 필요는 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다. 그러나 MTOM을 사용하려면 `?blob=mtom`을 지정하십시오.
   * `OutputServiceClient.Endpoint.Binding` 필드의 값을 가져와서 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * AEM Forms 사용자 이름을 `OutputServiceClient.ClientCredentials.UserName.UserName` 필드에 지정합니다.
      * 해당 암호 값을 `OutputServiceClient.ClientCredentials.UserName.Password` 필드에 할당합니다.
      * 상수 값 `HttpClientCredentialType.Basic`을 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.
      * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. 대화형 PDF 문서를 검색합니다.

   * 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 대화형 PDF 문서를 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하고 대화형 PDF 문서의 파일 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하고 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * `MTOM` 속성을 바이트 배열의 콘텐츠로 할당하여 `BLOB` 개체를 채웁니다.

1. PDF 문서를 변형합니다.

   `OutputClient` 개체의 `transformPDF` 메서드를 호출하고 다음 값을 전달하여 대화형 PDF 문서를 비대화형 PDF 문서로 변환합니다.

   * 대화형 PDF 문서가 포함된 `BLOB` 개체입니다.
   * `TransformationFormat` 열거형 값입니다. 비대화형 PDF 문서를 생성하려면 `TransformationFormat.PDF`을 지정합니다.
   * 개정 번호를 지정하는 `PDFARevisionNumber` 열거형 값.
   * `PDFARevisionNumber` 열거형 값이 사용되는지 여부를 지정하는 부울 값입니다. 이 매개 변수는 PDF/A 문서를 위한 것이므로 `false`을 지정할 수 있습니다.
   * 콜론으로 구분되는 수정 번호 및 연도를 나타내는 문자열 값입니다. 이 매개 변수는 PDF/A 문서를 위한 것이므로 `null`을 지정할 수 있습니다.
   * PDF/A 적합성 수준을 나타내는 `PDFAConformance` 열거형 값.
   * `PDFAConformance` 열거형 값이 사용되는지 여부를 지정하는 부울 값입니다. 이 매개 변수는 PDF/A 문서를 위한 것이므로 `false`을 지정할 수 있습니다.

   `transformPDF` 메서드는 비대화형 PDF 문서가 포함된 `BLOB` 개체를 반환합니다.

1. 비대화형 PDF 문서를 PDF 파일로 저장합니다.

   * 해당 생성자를 호출하고 비대화형 PDF 문서의 파일 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `transformPDF` 메서드에서 반환된 `BLOB` 개체의 데이터 콘텐츠를 저장하는 바이트 배열을 만듭니다. `BLOB` 개체의 `MTOM` 데이터 멤버의 값을 가져와서 바이트 배열을 채웁니다.
   * 해당 생성자를 호출하고 `System.IO.FileStream` 개체를 전달하여 `System.IO.BinaryWriter` 개체를 만듭니다.
   * `System.IO.BinaryWriter` 개체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열 내용을 PDF 파일에 씁니다.

**참고 항목**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
