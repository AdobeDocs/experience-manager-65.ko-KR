---
title: 문서 출력 스트림 만들기
description: 출력 서비스를 사용하여 문서를 PDF(PDF/A 문서 포함), PostScript, PCL(프린터 제어 언어) 및 Zebra - ZPL, Intermec - IPL, Datamax - DPL 및 TecToshiba - TPCL 레이블 형식으로 변환합니다.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: a521bfac-f417-4002-9c5c-8d7794d3eec7
source-git-commit: 5e56441d2dc9b280547c91def8d971e7b1dfcfe3
workflow-type: tm+mt
source-wordcount: '18956'
ht-degree: 0%

---

# 문서 출력 스트림 만들기  {#creating-document-output-streams}

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms에 대해서만 적용됩니다.**

**출력 서비스 정보**

출력 서비스를 사용하면 문서를 PDF(PDF/A 문서 포함), PostScript, PCL(프린터 제어 언어) 및 다음 레이블 형식으로 출력할 수 있습니다.

* 얼룩말 - ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

출력 서비스를 사용하면 XML 양식 데이터를 양식 디자인과 병합하고 문서를 네트워크 프린터 또는 파일로 출력할 수 있습니다.

양식 디자인(XDP 파일)을 출력 서비스에 전달하는 방법에는 두 가지가 있습니다. 다음을 전달할 수 있습니다. `com.adobe.idp.Document` 출력 서비스에 대한 양식 디자인을 포함하는 인스턴스입니다. 또는 양식 디자인의 위치를 지정하는 URI 값을 전달할 수 있습니다. 이 두 가지 방법은 모두에서 설명합니다. *AEM Forms를 사용한 프로그래밍*.

>[!NOTE]
>
>Output 서비스는 응용 프로그램 개체별 스크립트가 포함된 Acroform PDF 문서를 지원하지 않습니다. 애플리케이션 개체별 스크립트가 포함된 Acroform PDF 문서는 렌더링되지 않습니다.

다음 섹션에서는 URI 값을 사용하여 양식 디자인을 출력 서비스로 전달하는 방법을 보여줍니다.

* [PDF 문서 만들기](creating-document-output-streams.md#creating-pdf-documents)
* [PDF/A 문서 생성](creating-document-output-streams.md#creating-pdf-a-documents)

다음 단원에서는 `com.adobe.idp.Document` 인스턴스:

* [컨텐츠 서비스(사용 중단됨)의 문서를 출력 서비스로 전달](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [조각을 사용하여 PDF 문서 생성](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

사용할 기술을 결정할 때 고려해야 할 사항 중 하나는 다른 AEM Forms 서비스에서 양식 디자인을 가져오는 경우 `com.adobe.idp.Document` 인스턴스. 두 가지 모두 *출력 서비스에 문서 전달* 및 *조각을 사용하여 PDF 문서 생성* 섹션은 다른 AEM Forms 서비스에서 양식 디자인을 가져오는 방법을 보여 줍니다. 첫 번째 섹션은 Content Services에서 양식 디자인을 검색합니다(더 이상 사용되지 않음). 두 번째 섹션은 어셈블러 서비스에서 양식 디자인을 검색합니다.

파일 시스템과 같은 고정된 위치에서 양식 디자인을 가져오는 경우 두 기법 중 하나를 사용할 수 있습니다. 즉, XDP 파일에 URI 값을 지정하거나 `com.adobe.idp.Document` 인스턴스.

PDF 문서를 만들 때 양식 디자인의 위치를 지정하는 URI 값을 전달하려면 `generatePDFOutput` 메서드를 사용합니다. 마찬가지로 을(를) 전달합니다. `com.adobe.idp.Document` 인스턴스 - 출력 서비스 PDF 문서를 만들 때 `generatePDFOutput2` 메서드를 사용합니다.

출력 스트림을 네트워크 프린터로 보낼 때 다음 중 하나를 사용할 수도 있습니다. 를 전달하여 출력 스트림을 프린터로 보내려면 `com.adobe.idp.Document` 양식 디자인이 포함된 인스턴스에서는 `sendToPrinter2`메서드를 사용합니다. URI 값을 전달하여 출력 스트림을 프린터로 보내려면 `sendToPrinter`메서드를 사용합니다. 다음 *프린터로 인쇄 스트림 보내기* 섹션에서 다음을 사용합니다. `sendToPrinter` 메서드를 사용합니다.

출력 서비스를 사용하여 다음 작업을 수행할 수 있습니다.

* [PDF 문서 만들기](creating-document-output-streams.md#creating-pdf-documents)
* [PDF/A 문서 생성](creating-document-output-streams.md#creating-pdf-a-documents)
* [컨텐츠 서비스(사용 중단됨)의 문서를 출력 서비스로 전달](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [조각을 사용하여 PDF 문서 생성](creating-document-output-streams.md#creating-pdf-documents-using-fragments)
* [파일로 인쇄](creating-document-output-streams.md#printing-to-files)
* [프린터로 인쇄 스트림 보내기](creating-document-output-streams.md#sending-print-streams-to-printers)
* [여러 출력 파일 만들기](creating-document-output-streams.md#creating-multiple-output-files)
* [검색 규칙 만들기](creating-document-output-streams.md#creating-search-rules)
* [PDF 문서 병합](creating-document-output-streams.md#flattening-pdf-documents)

>[!NOTE]
>
>출력 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

## PDF 문서 만들기 {#creating-pdf-documents}

출력 서비스를 사용하여 사용자가 제공하는 양식 디자인과 XML 양식 데이터를 기반으로 하는 PDF 문서를 만들 수 있습니다. 출력 서비스에서 만든 PDF 문서는 대화형 PDF 문서가 아닙니다. 사용자는 양식 데이터를 입력하거나 수정할 수 없습니다.

장기 저장을 위한 PDF 문서를 만들려면 PDF/A 문서를 만드는 것이 좋습니다. (참조: [PDF/A 문서 생성](creating-document-output-streams.md#creating-pdf-a-documents).)

사용자가 데이터를 입력할 수 있는 대화형 PDF 양식을 만들려면 Forms 서비스를 사용하십시오. (참조: [대화형 PDF forms 렌더링](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms).)

>[!NOTE]
>
>출력 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary-of-steps}

PDF 문서를 만들려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. 출력 클라이언트 개체를 만듭니다.
1. XML 데이터 소스를 참조합니다.
1. PDF 런타임 옵션을 설정합니다.
1. 렌더링 런타임 옵션을 설정합니다.
1. PDF 문서를 생성합니다.
1. 작업 결과를 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar (AEM Forms이 JBoss에 배포된 경우 필수)

AEM Forms이 JBoss가 아닌 지원되는 J2EE 애플리케이션 서버에 배포된 경우 adobe-utilities.jar 및 jbossall-client.jar 파일을 AEM Forms이 배포된 J2EE 애플리케이션 서버에 관련된 JAR 파일로 교체해야 합니다.

**출력 클라이언트 개체 만들기**

출력 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 출력 서비스 클라이언트 개체를 만들어야 합니다. Java API를 사용하는 경우 `OutputClient` 개체. Output 웹 서비스 API를 사용하는 경우 `OutputServiceService` 개체.

**XML 데이터 소스 참조**

데이터를 양식 디자인과 병합하려면 데이터가 포함된 XML 데이터 원본을 참조해야 합니다. 데이터로 채울 모든 양식 필드에 XML 요소가 있어야 합니다. XML 요소 이름은 필드 이름과 일치해야 합니다. XML 요소가 양식 필드에 해당하지 않거나 XML 요소 이름이 필드 이름과 일치하지 않으면 XML 요소가 무시됩니다. 모든 XML 요소를 지정한 경우 XML 요소가 표시되는 순서를 일치시킬 필요는 없습니다.

다음 예시 대출 신청서 양식을 고려하십시오.

![cp_cp_loanformdata](assets/cp_cp_loanformdata.png)

이 양식 디자인에 데이터를 병합하려면 양식에 해당하는 XML 데이터 소스를 만들어야 합니다. 다음 XML은 예제 담보 대출 신청 양식에 해당하는 XDP XML 데이터 소스를 나타냅니다.

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
>파일 URI 런타임 옵션을 설정하는 대신 출력 서비스에서 반환되는 복잡한 데이터 형식에서 프로그래밍 방식으로 PDF 문서를 검색할 수 있습니다. 그러나 파일 URI 런타임 옵션을 설정하면 프로그래밍 방식으로 PDF 문서를 검색하는 응용 프로그램 논리를 만들 필요가 없습니다.

**렌더링 런타임 옵션 설정**

PDF 문서를 만들 때 렌더링 런타임 옵션을 설정할 수 있습니다. 이러한 옵션이 필요하지 않지만(필요한 PDF 런타임 옵션과 달리) 출력 서비스의 성능 향상과 같은 작업을 수행할 수 있습니다. 예를 들어 출력 서비스에서 사용하는 양식 디자인을 캐시하여 성능을 향상시킬 수 있습니다.

태그된 Acrobat 양식을 입력으로 사용하는 경우 출력 서비스 Java 또는 웹 서비스 API를 사용하여 태그된 설정을 끌 수 없습니다. 프로그래밍 방식으로 이 옵션을 로 설정하려고 하는 경우 `false`로 설정되어 있어도 결과 PDF 문서에 태그가 지정되어 있습니다.

>[!NOTE]
>
>렌더링 런타임 옵션을 지정하지 않으면 기본값이 사용됩니다. 렌더링 런타임 옵션에 대한 자세한 내용은 `RenderOptionsSpec` 클래스 참조. (참조: [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)).

**PDF 문서 생성**

양식 데이터가 포함된 유효한 XML 데이터 소스를 참조하고 런타임 옵션을 설정한 후 출력 서비스를 호출할 수 있으므로 PDF 문서가 생성됩니다.

PDF 문서를 생성할 때 출력 서비스에서 PDF 문서를 만드는 데 필요한 URI 값을 지정합니다. 양식 디자인은 서버 파일 시스템과 같은 위치나 AEM Forms 애플리케이션의 일부로 저장할 수 있습니다. 컨텐츠 루트 URI 값을 사용하여 Forms 애플리케이션의 일부로 존재하는 양식 디자인(또는 이미지 파일과 같은 기타 리소스)을 참조할 수 있습니다 `repository:///`. 예를 들어, 다음 양식 디자인을 고려해 보십시오. *Loan.xdp* 다음 Forms 애플리케이션 내에 위치: *Applications/FormsApplication*:

![cp_cp_formrepository](assets/cp_cp_formrepository.png)

이전 그림에 표시된 Loan.xdp 파일에 액세스하려면 다음을 지정합니다 `repository:///Applications/FormsApplication/1.0/FormsFolder/` 에 전달된 세 번째 매개 변수로 `OutputClient` 개체 `generatePDFOutput` 메서드를 사용합니다. 양식 이름(*Loan.xdp*&#x200B;에 전달된 두 번째 매개 변수로서의 `OutputClient` 개체 `generatePDFOutput` 메서드를 사용합니다.

XDP 파일에 이미지(또는 조각과 같은 기타 리소스)가 포함된 경우 리소스를 XDP 파일과 동일한 애플리케이션 폴더에 배치합니다. AEM Forms은 컨텐츠 루트 URI를 기본 경로로 사용하여 이미지에 대한 참조를 확인합니다. 예를 들어 Loan.xdp 파일에 이미지가 포함되어 있는 경우 이미지를에 배치해야 합니다 `Applications/FormsApplication/1.0/FormsFolder/`.

>[!NOTE]
>
>다음을 호출할 때 Forms 응용 프로그램 URI를 참조할 수 있습니다. `OutputClient` 개체 `generatePDFOutput` 또는 `generatePrintedOutput` 메서드를 사용합니다.

>[!NOTE]
>
>Forms 애플리케이션에서 XDP를 참조하여 PDF 문서를 만드는 전체 빠른 시작을 보려면 다음을 참조하십시오. [빠른 시작(EJB 모드): Java API를 사용하여 애플리케이션 XDP 파일 기반 PDF 문서 생성](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api).

**작업 결과 검색**

출력 서비스는 작업을 수행한 후 작업 성공 여부를 지정하는 상태 XML 데이터와 같은 다양한 데이터 항목을 반환합니다.

**추가 참조**

[Java API를 사용하여 PDF 문서 만들기](creating-document-output-streams.md#create-a-pdf-document-using-the-java-api)

[웹 서비스 API를 사용하여 PDF 문서 만들기](creating-document-output-streams.md#create-a-pdf-document-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[출력 서비스 API 빠른 시작](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java API를 사용하여 PDF 문서 만들기 {#create-a-pdf-document-using-the-java-api}

출력 API(Java)를 사용하여 PDF 문서를 만듭니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-output-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. 출력 클라이언트 개체를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.
   * 만들기 `OutputClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체.

1. XML 데이터 소스를 참조합니다.

   * 만들기 `java.io.FileInputStream` PDF 문서의 생성자를 사용하고 XML 파일의 위치를 지정하는 문자열 값을 전달하여 XML 데이터 소스를 채우는 데 사용되는 개체를 나타냅니다.
   * 만들기 `com.adobe.idp.Document` 개체를 만들 때 사용됩니다. 전달 `java.io.FileInputStream` 개체.

1. PDF 런타임 옵션을 설정합니다.

   * 만들기 `PDFOutputOptionsSpec` 개체를 만들 때 사용됩니다.
   * 다음을 호출하여 파일 URI 옵션 설정 `PDFOutputOptionsSpec` 개체 `setFileURI` 메서드를 사용합니다. 출력 서비스에서 생성하는 PDF 파일의 위치를 지정하는 문자열 값을 전달합니다. 파일 URI 옵션은 클라이언트 컴퓨터가 아니라 AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버에 상대적입니다.

1. 렌더링 런타임 옵션을 설정합니다.

   * 만들기 `RenderOptionsSpec` 개체를 만들 때 사용됩니다.
   * 양식 디자인을 캐시하여 를 호출하여 출력 서비스의 성능을 개선합니다. `RenderOptionsSpec` 개체 `setCacheEnabled` 및 통과 `true`.

   >[!NOTE]
   >
   >를 사용하여 PDF 문서의 버전을 설정할 수 없습니다 `RenderOptionsSpec` 개체 `setPdfVersion` 메서드, 입력 문서가 Acrobat 양식(Acrobat에서 만든 양식) 또는 서명 또는 인증된 XFA 문서인 경우 출력 PDF 문서는 원래 PDF 버전을 유지합니다. 마찬가지로, 를 호출하여 태그가 지정된 Adobe PDF 옵션을 설정할 수 없습니다. `RenderOptionsSpec` 개체 `setTaggedPDF` 입력 문서가 Acrobat 양식 또는 서명 또는 인증된 XFA 문서인 경우 메서드입니다.

   >[!NOTE]
   >
   >를 사용하여 선형화된 PDF 옵션을 설정할 수 없습니다. `RenderOptionsSpec` 개체 `setLinearizedPDF` 입력 PDF 문서가 인증 또는 디지털 서명된 경우 메서드입니다. (참조: [PDF 문서에 디지털 서명&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*.)*

1. PDF 문서를 생성합니다.

   를 호출하여 PDF 문서 만들기 `OutputClient` 개체 `generatePDFOutput` 메서드 및 다음 값 전달:

   * A `TransformationFormat` 열거형 값입니다. PDF 문서를 생성하려면 다음을 지정합니다 `TransformationFormat.PDF`.
   * 양식 디자인의 이름을 지정하는 문자열 값입니다.
   * 양식 디자인이 있는 콘텐츠 루트를 지정하는 문자열 값입니다.
   * A `PDFOutputOptionsSpec` PDF 런타임 옵션이 포함된 객체입니다.
   * A `RenderOptionsSpec` 렌더링 런타임 옵션이 포함된 객체입니다.
   * 다음 `com.adobe.idp.Document` 폼 디자인과 병합할 데이터가 들어 있는 XML 데이터 원본을 포함하는 개체입니다.

   다음 `generatePDFOutput` 메서드가 다음을 반환합니다. `OutputResult` 작업의 결과를 포함하는 개체입니다.

   >[!NOTE]
   >
   >를 호출하여 PDF 문서를 생성하는 경우 `generatePDFOutput` 메서드에서 서명되거나 인증된 XFA PDF 양식과 데이터를 병합할 수 없습니다. (참조: [디지털 서명 및 인증 문서&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*.)*

   >[!NOTE]
   >
   >다음 `OutputResult` 개체 `getRecordLevelMetaDataList` 메서드 반환 `null`*.*

   >[!NOTE]
   >
   >PDF 문서를 만들 때는 `OutputClient` 개체 `generatePDFOutput2` 메서드를 사용합니다. (참조: [컨텐츠 서비스(사용 중단됨)의 문서를 출력 서비스로 전달&#x200B;](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*.)*

1. 작업 결과를 검색합니다.

   * 검색 `com.adobe.idp.Document` 의 상태를 나타내는 개체 `generatePDFOutput` 를 호출하여 `OutputResult` 개체 `getStatusDoc` 메서드를 사용합니다. 이 메서드는 작업이 성공했는지 여부를 지정하는 상태 XML 데이터를 반환합니다.
   * 만들기 `java.io.File` 작업의 결과를 포함하는 개체입니다. 파일 이름 확장명이 .xml인지 확인합니다.
   * 호출 `com.adobe.idp.Document` 개체 `copyToFile` 콘텐츠 복사 방법 `com.adobe.idp.Document` 파일에 대한 개체(를 사용해야 함) `com.adobe.idp.Document` 에서 반환한 개체 `getStatusDoc` 메서드).

   출력 서비스는 인수에 의해 지정된 위치에 PDF 문서를 작성하지만 `PDFOutputOptionsSpec` 개체 `setFileURI` 메서드에서 PDF/A 문서를 프로그래밍 방식으로 검색하려면 `OutputResult` 개체 `getGeneratedDoc` 메서드를 사용합니다.

**추가 참조**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[빠른 시작(EJB 모드): Java API를 사용하여 PDF 문서 생성](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[빠른 시작(SOAP 모드): Java API를 사용하여 PDF 문서 생성](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 PDF 문서 만들기 {#create-a-pdf-document-using-the-web-service-api}

출력 API(웹 서비스)를 사용하여 PDF 문서를 만듭니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용하는지 확인합니다. `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` AEM Forms을 호스팅하는 서버의 IP 주소입니다.

1. 출력 클라이언트 개체를 만듭니다.

   * 만들기 `OutputServiceClient` 기본 생성자를 사용하여 개체를 작성합니다.
   * 만들기 `OutputServiceClient.Endpoint.Address` 을 사용하여 개체 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 를 사용할 필요가 없습니다. `lc_version` 특성. 이 속성은 서비스 참조를 만들 때 사용됩니다. 단, 을 지정합니다. `?blob=mtom` MTOM을 사용합니다.
   * 만들기 `System.ServiceModel.BasicHttpBinding` 의 값을 가져와서 개체 `OutputServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스트 `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름 할당 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 해당 암호 값을 필드에 할당합니다. `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 지정 `HttpClientCredentialType.Basic` 필드에 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 상수 값 지정 `BasicHttpSecurityMode.TransportCredentialOnly` 필드에 `BasicHttpBindingSecurity.Security.Mode`.

1. XML 데이터 소스를 참조합니다.

   * 만들기 `BLOB` 개체를 만들 때 사용됩니다. 다음 `BLOB` 객체는 PDF 문서와 병합될 XML 데이터를 저장하는 데 사용됩니다.
   * 만들기 `System.IO.FileStream` 개체를 호출하고 양식 데이터가 포함된 XML 파일의 파일 위치를 나타내는 문자열 값을 전달합니다.
   * 의 콘텐츠를 저장하는 바이트 배열 만들기 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채우기 `System.IO.FileStream` 개체 `Read` 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하는 방법.
   * 채우기 `BLOB` 개체 할당 `MTOM` 바이트 배열의 내용이 있는 필드입니다.

1. PDF 런타임 옵션 설정

   * 만들기 `PDFOutputOptionsSpec` 개체를 만들 때 사용됩니다.
   * 출력 서비스에서 생성하는 PDF 파일의 위치를 지정하는 문자열 값을 로 할당하여 파일 URI 옵션을 설정합니다. `PDFOutputOptionsSpec` 개체 `fileURI` 데이터 구성원입니다. 파일 URI 옵션은 클라이언트 컴퓨터가 아니라 AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버에 상대적입니다.

1. 렌더링 런타임 옵션을 설정합니다.

   * 만들기 `RenderOptionsSpec` 개체를 만들 때 사용됩니다.
   * 양식 디자인을 캐시하여 값을 할당하여 출력 서비스의 성능을 개선합니다. `true` (으)로 `RenderOptionsSpec` 개체 `cacheEnabled` 데이터 구성원입니다.

   >[!NOTE]
   >
   >를 사용하여 PDF 문서의 버전을 설정할 수 없습니다 `RenderOptionsSpec` 개체 `setPdfVersion` 메서드, 입력 문서가 Acrobat 양식(Acrobat에서 만든 양식) 또는 서명 또는 인증된 XFA 문서인 경우 출력 PDF 문서는 원래 PDF 버전을 유지합니다. 마찬가지로, 를 호출하여 태그가 지정된 Adobe PDF 옵션을 설정할 수 없습니다. `RenderOptionsSpec` 개체 `setTaggedPDF`* 입력 문서가 Acrobat 양식 또는 서명 또는 인증된 XFA 문서인 경우 방법입니다.*

   >[!NOTE]
   >
   >를 사용하여 선형화된 PDF 옵션을 설정할 수 없습니다. `RenderOptionsSpec` 개체 `linearizedPDF` 구성원(입력 PDF 문서가 인증 또는 디지털 서명된 경우) (참조: [PDF 문서에 디지털 서명&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*.)*

1. PDF 문서를 생성합니다.

   를 호출하여 PDF 문서 만들기 `OutputServiceService` 개체 `generatePDFOutput`메서드 및 다음 값 전달:

   * A `TransformationFormat` 열거형 값입니다. PDF 문서를 생성하려면 다음을 지정합니다 `TransformationFormat.PDF`.
   * 양식 디자인의 이름을 지정하는 문자열 값입니다.
   * 양식 디자인이 있는 콘텐츠 루트를 지정하는 문자열 값입니다.
   * A `PDFOutputOptionsSpec` PDF 런타임 옵션이 포함된 객체입니다.
   * A `RenderOptionsSpec` 렌더링 런타임 옵션이 포함된 객체입니다.
   * 다음 `BLOB` 폼 디자인과 병합할 데이터가 들어 있는 XML 데이터 원본을 포함하는 개체입니다.
   * A `BLOB` 로 채워지는 개체 `generatePDFOutput` 메서드를 사용합니다. 다음 `generatePDFOutput` 메서드는 문서를 설명하는 생성된 메타데이터로 이 개체를 채웁니다. (이 매개 변수 값은 웹 서비스 호출에만 필요합니다.)
   * A `BLOB` 로 채워지는 개체 `generatePDFOutput` 메서드를 사용합니다. 다음 `generatePDFOutput` 메서드는 이 개체를 결과 데이터로 채웁니다. (이 매개 변수 값은 웹 서비스 호출에만 필요합니다.)
   * An `OutputResult` 작업의 결과를 포함하는 개체입니다. (이 매개 변수 값은 웹 서비스 호출에만 필요합니다.)

   >[!NOTE]
   >
   >를 호출하여 PDF 문서를 생성하는 경우 `generatePDFOutput` 메서드에서 서명되거나 인증된 XFA PDF 양식과 데이터를 병합할 수 없습니다. (참조: [디지털 서명 및 인증 문서&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*.)*

   >[!NOTE]
   >
   >PDF 문서를 만들 때는 `OutputClient` 개체 `generatePDFOutput2` 메서드를 사용합니다. (참조: [컨텐츠 서비스(사용 중단됨)의 문서를 출력 서비스로 전달&#x200B;](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*.)*

1. 작업 결과를 검색합니다.

   * 만들기 `System.IO.FileStream` 개체를 호출하고 결과 데이터가 포함된 XML 파일 위치를 나타내는 문자열 값을 전달합니다. 파일 이름 확장명이 .xml인지 확인합니다.
   * 의 데이터 콘텐츠를 저장하는 바이트 배열 만들기 `BLOB` 에서 결과 데이터로 채운 개체 `OutputServiceService` 개체 `generatePDFOutput` 메서드(여덟 번째 매개 변수). 의 값을 가져와서 바이트 배열 채우기 `BLOB` 개체 `MTOM` `field`.
   * 만들기 `System.IO.BinaryWriter` 개체를 호출하고 `System.IO.FileStream` 개체.
   * 바이트 배열의 내용을 XML 파일에 씁니다. `System.IO.BinaryWriter` 개체 `Write` 메서드 및 바이트 배열 전달.

   참고 항목

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

   >[!NOTE]
   >
   >다음 `OutputServiceService` 개체 `generateOutput` 메서드가 더 이상 사용되지 않습니다.

## PDF/A 문서 생성 {#creating-pdf-a-documents}

출력 서비스를 사용하여 PDF/A 문서를 만들 수 있습니다. PDF/A는 문서 내용을 장기간 보존하기 위한 보관 형식이므로 모든 글꼴이 임베드되고 파일이 압축 해제됩니다. 따라서 PDF/A 문서는 일반적으로 표준 PDF 문서보다 큽니다. 또한 PDF/A 문서에는 오디오 및 비디오 컨텐츠가 포함되어 있지 않습니다. 다른 출력 서비스 작업과 마찬가지로 양식 디자인과 데이터를 모두 제공하여 양식 디자인과 병합하여 PDF/A 문서를 만듭니다.

PDF/A-1 사양은 두 가지 적합성 수준, 즉 a와 b로 구성됩니다. 두 요소의 주요 차이점은 적합성 수준 b에 필요하지 않은 논리적 구조(접근성) 지원에 관한 것입니다. 적합성 수준에 관계없이 PDF/A-1은 모든 글꼴이 생성된 PDF/A 문서에 포함됨을 지시합니다.

PDF/A가 PDF 문서를 보관하는 표준이지만 표준 PDF 문서가 회사의 요구 사항에 부합하는 경우 PDF/A를 보관에 사용해야 하는 것은 아닙니다. PDF/A 표준은 장기간 보관이 가능하고 문서 보존 요건을 충족하는 PDF 파일을 구축하는 것이 목적이다. 예를 들어 시간이 지남에 따라 URL이 유효하지 않게 될 수 있으므로 URL을 PDF/A에 포함할 수 없습니다.

조직은 자체 요구 사항, 문서를 보관하려는 기간, 파일 크기 고려 사항을 평가하고 자체 보관 전략을 결정해야 합니다. DocConverter 서비스를 사용하여 PDF 문서가 PDF/A를 준수하는지 여부를 프로그래밍 방식으로 확인할 수 있습니다. (참조: [프로그래밍 방식으로 PDF/A 준수 여부 확인](/help/forms/developing/pdf-a-documents.md#programmatically-determining-pdf-a-compliancy).)

PDF/A 문서는 양식 디자인에 지정된 글꼴을 사용해야 하며 글꼴은 대체할 수 없습니다. 따라서 PDF 문서 내에 있는 글꼴을 호스트 OS에서 사용할 수 없는 경우에는 예외가 발생합니다.

Acrobat에서 PDF/A 문서를 열면 다음 그림과 같이 해당 문서가 PDF/A 문서임을 확인하는 메시지가 표시됩니다.

![cp_cp_pdfamessage](assets/cp_cp_pdfamessage.png)

>[!NOTE]
>
>AIIM 웹 사이트에는 액세스할 수 있는 PDF/A FAQ 섹션이 있습니다. [https://www.loc.gov/preservation/digital/formats/fdd/fdd000125.shtml](https://www.loc.gov/preservation/digital/formats/fdd/fdd000125.shtml).

>[!NOTE]
>
>출력 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_65).

### 단계 요약 {#summary_of_steps-1}

PDF/A 문서를 만들려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. 출력 클라이언트 개체를 만듭니다.
1. XML 데이터 소스를 참조합니다.
1. PDF/A 런타임 옵션을 설정합니다.
1. 렌더링 런타임 옵션을 설정합니다.
1. PDF/문서 생성.
1. 작업 결과를 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 사용자 정의 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar (AEM Forms이 JBoss에 배포된 경우 필수)

AEM Forms이 JBoss가 아닌 지원되는 J2EE 애플리케이션 서버에 배포된 경우 adobe-utilities.jar 및 jbossall-client.jar 파일을 AEM Forms이 배포된 J2EE 애플리케이션 서버에 관련된 JAR 파일로 교체해야 합니다.

**출력 클라이언트 개체 만들기**

출력 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 출력 서비스 클라이언트 개체를 만들어야 합니다. Java API를 사용하는 경우 `OutputClient` 개체. Output 웹 서비스 API를 사용하는 경우 `OutputServiceService` 개체.

**XML 데이터 소스 참조**

데이터를 양식 디자인과 병합하려면 데이터가 포함된 XML 데이터 원본을 참조해야 합니다. 데이터로 채울 모든 양식 필드에 XML 요소가 있어야 합니다. XML 요소 이름은 필드 이름과 일치해야 합니다. XML 요소가 양식 필드에 해당하지 않거나 XML 요소 이름이 필드 이름과 일치하지 않으면 XML 요소가 무시됩니다. 모든 XML 요소를 지정한 경우 XML 요소가 표시되는 순서를 일치시킬 필요는 없습니다.

**PDF/A 런타임 옵션 설정**

PDF/A 문서를 만들 때 파일 URI 옵션을 설정할 수 있습니다. URI는 AEM Forms을 호스팅하는 J2EE 애플리케이션 서버에 상대적입니다. 즉, C:\Adobe을 설정하면 파일이 클라이언트 컴퓨터가 아닌 서버의 폴더에 기록됩니다. URI는 출력 서비스가 생성하는 PDF/A 파일의 이름과 위치를 지정합니다.

**렌더링 런타임 옵션 설정**

PDF/A 문서를 만들 때 렌더링 런타임 옵션을 설정할 수 있습니다. 설정할 수 있는 두 가지 PDF/A 관련 옵션은 `PDFAConformance` 및 `PDFARevisionNumber` 값. 다음 `PDFAConformance` 값은 PDF 문서가 장기 전자 문서를 보존하는 방법을 지정하는 요구 사항을 준수하는 방법을 나타냅니다. 이 옵션의 유효한 값은 다음과 같습니다. `A` 및 `B`. 레벨 a 및 b 적합성에 대한 자세한 내용은 이라는 제목의 PDF/A-1 ISO 사양을 참조하십시오 *ISO 19005-1 문서 관리*.

다음 `PDFARevisionNumber` 값은 PDF/A 문서의 개정 번호를 나타냅니다. PDF/A 문서의 개정 번호에 대한 자세한 내용은 제목이 인 PDF/A-1 ISO 사양을 참조하십시오 *ISO 19005-1 문서 관리*.

>[!NOTE]
>
>태그가 지정된 Adobe PDF 옵션을 로 설정할 수 없습니다. `false` PDF/A 1A 문서를 만들 때. PDF/A 1A는 항상 태그가 지정된 PDF 문서입니다. 또한 태그가 지정된 Adobe PDF 옵션을 로 설정할 수 없습니다 `true` PDF/A 1B 문서를 만들 때. PDF/A 1B는 항상 태그가 지정되지 않은 PDF 문서입니다.

**PDF/A 문서 생성**

양식 데이터가 포함된 유효한 XML 데이터 소스를 참조하고 런타임 옵션을 설정한 후 출력 서비스를 호출하여 PDF/A 문서를 생성할 수 있습니다.

**작업 결과 검색**

출력 서비스는 작업을 수행한 후 작업이 성공했는지 여부를 지정하는 XML 데이터와 같은 다양한 데이터 항목을 반환합니다.

**추가 참조**

[Java API를 사용하여 PDF/A 문서 만들기](creating-document-output-streams.md#create-a-pdf-a-document-using-the-java-api)

[웹 서비스 API를 사용하여 PDF/A 문서 만들기](creating-document-output-streams.md#create-a-pdf-a-document-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[출력 서비스 API 빠른 시작](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java API를 사용하여 PDF/A 문서 만들기 {#create-a-pdf-a-document-using-the-java-api}

Output API(Java)를 사용하여 PDF/A 문서를 만듭니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-output-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. 출력 클라이언트 개체를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.
   * 만들기 `OutputClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체.

1. XML 데이터 소스를 참조합니다.

   * 만들기 `java.io.FileInputStream` 해당 생성자를 사용하고 XML 파일의 위치를 지정하는 문자열 값을 전달하여 PDF/A 문서를 채우는 데 사용되는 XML 데이터 소스를 나타내는 개체입니다.
   * 만들기 `com.adobe.idp.Document` 개체를 생성자를 사용하고 `java.io.FileInputStream` 개체.

1. PDF/A 런타임 옵션을 설정합니다.

   * 만들기 `PDFOutputOptionsSpec` 개체를 만들 때 사용됩니다.
   * 다음을 호출하여 파일 URI 옵션 설정 `PDFOutputOptionsSpec` 개체 `setFileURI` 메서드를 사용합니다. 출력 서비스에서 생성하는 PDF 파일의 위치를 지정하는 문자열 값을 전달합니다. 파일 URI 옵션은 클라이언트 컴퓨터가 아니라 AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버에 상대적입니다.

1. 렌더링 런타임 옵션을 설정합니다.

   * 만들기 `RenderOptionsSpec` 개체를 만들 때 사용됩니다.
   * 설정 `PDFAConformance` 를 호출하여 값을 `RenderOptionsSpec` 개체 `setPDFAConformance` 방법 및 전달 `PDFAConformance` 적합성 수준을 지정하는 열거형 값입니다. 예를 들어 적합성 수준 A를 지정하려면 를 전달합니다 `PDFAConformance.A`.
   * 설정 `PDFARevisionNumber` 를 호출하여 값을 `RenderOptionsSpec` 개체 `setPDFARevisionNumber` 방법 및 전달 `PDFARevisionNumber.Revision_1`.

   >[!NOTE]
   >
   >PDF/A 문서의 PDF 버전은 다음에 대해 지정하는 값에 관계없이 1.4입니다. `RenderOptionsSpec` 개체 `setPdfVersion`*메서드를 사용합니다.*

1. PDF/문서 생성.

   다음을 호출하여 PDF/A 문서 만들기 `OutputClient` 개체 `generatePDFOutput` 메서드 및 다음 값 전달:

   * A `TransformationFormat` 열거형 값입니다. PDF/A 문서를 생성하려면 `TransformationFormat.PDFA`.
   * 양식 디자인의 이름을 지정하는 문자열 값입니다.
   * 양식 디자인이 있는 콘텐츠 루트를 지정하는 문자열 값입니다.
   * A `PDFOutputOptionsSpec` PDF 런타임 옵션이 포함된 객체입니다.
   * A `RenderOptionsSpec` 렌더링 런타임 옵션이 포함된 객체입니다.
   * 다음 `com.adobe.idp.Document` 폼 디자인과 병합할 데이터가 들어 있는 XML 데이터 원본을 포함하는 개체입니다.

   다음 `generatePDFOutput` 메서드가 다음을 반환합니다. `OutputResult` 작업의 결과를 포함하는 개체입니다.

   >[!NOTE]
   >
   >다음 `OutputResult` 개체 `getRecordLevelMetaDataList` 메서드 반환 `null`.

   >[!NOTE]
   >
   >다음을 호출하여 PDF/A 문서를 만들 수도 있습니다. `OutputClient` 개체 `generatePDFOutput`2 방법. (참조: [컨텐츠 서비스(사용 중단됨)의 문서를 출력 서비스로 전달](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service).)

1. 작업 결과를 검색합니다.

   * 만들기 `com.adobe.idp.Document` 의 상태를 나타내는 개체 `generatePDFOutput` 메서드를 호출하여 `OutputResult` 개체 `getStatusDoc` 메서드를 사용합니다.
   * 만들기 `java.io.File` 작업의 결과를 포함할 개체입니다. 파일 이름 확장명이 .xml인지 확인합니다.
   * 호출 `com.adobe.idp.Document` 개체 `copyToFile` 콘텐츠 복사 방법 `com.adobe.idp.Document` 파일에 대한 개체(를 사용해야 함) `com.adobe.idp.Document` 에서 반환한 개체 `getStatusDoc` 메서드).

   >[!NOTE]
   >
   >출력 서비스는 PDF/A 문서를 인수에 의해 지정된 위치에 쓰고 `PDFOutputOptionsSpec` 개체 `setFileURI` 메서드에서 PDF/A 문서를 프로그래밍 방식으로 검색하려면 `OutputResult` 개체 `getGeneratedDoc` 메서드를 사용합니다.

**추가 참조**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[빠른 시작(SOAP 모드): Java API를 사용하여 PDF/문서 생성](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-a-document-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### 웹 서비스 API를 사용하여 PDF/A 문서 만들기 {#create-a-pdf-a-document-using-the-web-service-api}

Output API(웹 서비스)를 사용하여 PDF/A 문서를 만듭니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용하는지 확인합니다. `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` AEM Forms을 호스팅하는 서버의 IP 주소입니다.

1. 출력 클라이언트 개체를 만듭니다.

   * 만들기 `OutputServiceClient` 기본 생성자를 사용하여 개체를 작성합니다.
   * 만들기 `OutputServiceClient.Endpoint.Address` 을 사용하여 개체 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 를 사용할 필요가 없습니다. `lc_version` 특성. 이 속성은 서비스 참조를 만들 때 사용됩니다. 단, 을 지정합니다. `?blob=mtom` MTOM을 사용합니다.
   * 만들기 `System.ServiceModel.BasicHttpBinding` 의 값을 가져와서 개체 `OutputServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스트 `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름 할당 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 해당 암호 값을 필드에 할당합니다. `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 지정 `HttpClientCredentialType.Basic` 필드에 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 상수 값 지정 `BasicHttpSecurityMode.TransportCredentialOnly` 필드에 `BasicHttpBindingSecurity.Security.Mode`.

1. XML 데이터 소스를 참조합니다.

   * 만들기 `BLOB` 개체를 만들 때 사용됩니다. 다음 `BLOB` 객체는 PDF/A 문서와 병합될 데이터를 저장하는 데 사용됩니다.
   * 만들기 `System.IO.FileStream` 객체를 생성합니다. 생성자를 호출하고 암호화할 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 콘텐츠를 저장하는 바이트 배열 만들기 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채우기 `System.IO.FileStream` 개체 `Read` 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하는 방법.
   * 채우기 `BLOB` 개체 할당 `MTOM` 바이트 배열 내용이 있는 필드입니다.

1. PDF/A 런타임 옵션을 설정합니다.

   * 만들기 `PDFOutputOptionsSpec` 개체를 만들 때 사용됩니다.
   * 출력 서비스에서 생성하는 PDF 파일의 위치를 지정하는 문자열 값을 로 할당하여 파일 URI 옵션을 설정합니다. `PDFOutputOptionsSpec` 개체 `fileURI` 데이터 구성원입니다. 파일 URI 옵션은 클라이언트 컴퓨터가 아니라 AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버에 상대적입니다

1. 렌더링 런타임 옵션을 설정합니다.

   * 만들기 `RenderOptionsSpec` 개체를 만들 때 사용됩니다.
   * 설정 `PDFAConformance` 을(를) 할당한 값 `PDFAConformance` 열거형 값을 `RenderOptionsSpec` 개체 `PDFAConformance` 데이터 구성원입니다. 예를 들어 적합성 수준 A를 지정하려면 을 지정합니다 `PDFAConformance.A` 이 데이터 구성원에 연결합니다.
   * 설정 `PDFARevisionNumber` 을(를) 할당한 값 `PDFARevisionNumber` 열거형 값을 `RenderOptionsSpec` 개체 `PDFARevisionNumber` 데이터 구성원입니다. 할당 `PDFARevisionNumber.Revision_1` 이 데이터 구성원에 연결합니다.

   >[!NOTE]
   >
   >PDF/A 문서의 PDF 버전은 지정한 값에 관계없이 1.4입니다.

1. PDF/문서 생성.

   를 호출하여 PDF 문서 만들기 `OutputServiceService` 개체 `generatePDFOutput`메서드 및 다음 값 전달:

   * TransformationFormat 열거형 값입니다. PDF 문서를 생성하려면 다음을 지정합니다 `TransformationFormat.PDFA`.
   * 양식 디자인의 이름을 지정하는 문자열 값입니다.
   * 양식 디자인이 있는 콘텐츠 루트를 지정하는 문자열 값입니다.
   * A `PDFOutputOptionsSpec` PDF 런타임 옵션이 포함된 객체입니다.
   * A `RenderOptionsSpec` 렌더링 런타임 옵션이 포함된 객체입니다.
   * 다음 `BLOB` 폼 디자인과 병합할 데이터가 들어 있는 XML 데이터 원본을 포함하는 개체입니다.
   * A `BLOB` 로 채워지는 개체 `generatePDFOutput` 메서드를 사용합니다. 다음 `generatePDFOutput` 메서드는 문서를 설명하는 생성된 메타데이터로 이 개체를 채웁니다. 이 매개 변수 값은 웹 서비스 호출에만 필요합니다.
   * A `BLOB` 로 채워지는 개체 `generatePDFOutput` 메서드를 사용합니다. 다음 `generatePDFOutput` 메서드는 이 개체를 결과 데이터로 채웁니다. 이 매개 변수 값은 웹 서비스 호출에만 필요합니다.
   * An `OutputResult` 작업의 결과를 포함하는 개체입니다. 이 매개 변수 값은 웹 서비스 호출에만 필요합니다.

   >[!NOTE]
   >
   >다음을 호출하여 PDF/A 문서를 만들 수도 있습니다. `OutputClient` 개체 `generatePDFOutput`2 방법. (참조: [컨텐츠 서비스(사용 중단됨)의 문서를 출력 서비스로 전달](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service).)

1. 작업 결과를 검색합니다.

   * 만들기 `System.IO.FileStream` 개체를 호출하고 결과 데이터가 포함된 XML 파일 위치를 나타내는 문자열 값을 전달합니다. 파일 이름 확장명이 .xml인지 확인합니다.
   * 의 데이터 콘텐츠를 저장하는 바이트 배열 만들기 `BLOB` 에서 결과 데이터로 채운 개체 `OutputServiceService` 개체 `generatePDFOutput` 메서드(여덟 번째 매개 변수). 의 값을 가져와서 바이트 배열 채우기 `BLOB` 개체 `MTOM` 필드.
   * 만들기 `System.IO.BinaryWriter` 개체를 호출하고 `System.IO.FileStream` 개체.
   * 바이트 배열의 내용을 XML 파일에 씁니다. `System.IO.BinaryWriter` 개체 `Write` 메서드 및 바이트 배열 전달.

**추가 참조**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 컨텐츠 서비스(사용 중단됨)의 문서를 출력 서비스로 전달 {#passing-documents-located-in-content-services-deprecated-to-the-output-service}

출력 서비스는 일반적으로 XDP 파일로 저장되고 디자이너에서 만들어지는 양식 디자인을 기반으로 하는 비대화형 PDF 양식을 렌더링합니다. 다음을 전달할 수 있습니다. `com.adobe.idp.Document` 출력 서비스에 대한 양식 디자인을 포함하는 개체입니다. 그런 다음 Output 서비스는 `com.adobe.idp.Document` 개체.

를 전달할 때의 이점 `com.adobe.idp.Document` 출력 서비스의 개체는 다른 AEM Forms 서비스 작업에서 `com.adobe.idp.Document` 인스턴스. 즉, 다음을 얻을 수 있습니다. `com.adobe.idp.Document` 다른 서비스 작업의 인스턴스를 렌더링합니다. 예를 들어 XDP 파일이 Content Services(더 이상 사용되지 않음) 노드에 저장되어 있다고 가정해 보겠습니다 `/Company Home/Form Designs`다음 그림과 같이 을 참조하십시오.

Content Services(더 이상 사용되지 않음)에서 Loan.xdp를 프로그래밍 방식으로 검색하고 XDP 파일을 `com.adobe.idp.Document` 개체.

>[!NOTE]
>
>Forms 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-2}

Content Services(더 이상 사용되지 않음)에서 가져온 문서를 출력 서비스로 전달하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. 출력 및 Document Management 클라이언트 API 객체를 작성합니다.
1. 콘텐츠 서비스에서 양식 디자인을 검색합니다(더 이상 사용되지 않음).
1. 비대화형 PDF 양식 렌더링.
1. 데이터 스트림으로 작업을 수행합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함합니다.

**출력 및 Document Management 클라이언트 API 개체 만들기**

출력 서비스 API 작업을 프로그래밍 방식으로 수행하려면 먼저 출력 클라이언트 API 개체를 만듭니다. 또한 이 워크플로우는 콘텐츠 서비스에서 XDP 파일을 검색하므로(더 이상 사용되지 않음) 문서 관리 API 개체를 만듭니다.

**컨텐츠 서비스에서 양식 디자인 검색(더 이상 사용되지 않음)**

Java 또는 웹 서비스 API를 사용하여 콘텐츠 서비스에서 XDP 파일을 검색합니다(더 이상 사용되지 않음). XDP 파일이 `com.adobe.idp.Document` 인스턴스(또는 a `BLOB` 웹 서비스를 사용하는 경우의 인스턴스). 그런 다음 를 전달할 수 있습니다. `com.adobe.idp.Document` 인스턴스를 출력 서비스로 보냅니다.

**비대화형 PDF 양식 렌더링**

비대화형 양식을 렌더링하려면 `com.adobe.idp.Document` 콘텐츠 서비스(더 이상 사용되지 않음)에서 출력 서비스로 반환된 인스턴스.

>[!NOTE]
>
>이름이 인 두 개의 새 메서드 `generatePDFOutput2`및 g `eneratePrintedOutput2`수락 `com.adobe.idp.Document` 폼 디자인이 포함된 개체입니다. 를 전달할 수도 있습니다. `com.adobe.idp.Document`네트워크 프린터로 인쇄 스트림을 보낼 때 출력 서비스에 대한 양식 디자인을 포함합니다.

**양식 데이터 스트림으로 작업 수행**

비대화형 양식을 PDF 파일로 저장할 수 있습니다. 양식은 Adobe Reader 또는 Acrobat에서 볼 수 있습니다.

**추가 참조**

[Java API를 사용하여 출력 서비스에 문서 전달](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-java-api)

[웹 서비스 API를 사용하여 출력 서비스에 문서 전달](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[출력 서비스 API 빠른 시작](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[조각을 사용하여 PDF 문서 생성](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

### Java API를 사용하여 출력 서비스에 문서 전달 {#pass-documents-to-the-output-service-using-the-java-api}

출력 서비스 및 콘텐츠 서비스(더 이상 사용되지 않음) API(Java)를 사용하여 콘텐츠 서비스(더 이상 사용되지 않음)에서 검색한 문서를 전달합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-output-client.jar 및 adobe-contentservices-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. 출력 및 Document Management 클라이언트 API 객체를 작성합니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다. (참조: [연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * 만들기 `OutputClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체.
   * 만들기 `DocumentManagementServiceClientImpl` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체.

1. 콘텐츠 서비스에서 양식 디자인을 검색합니다(더 이상 사용되지 않음).

   호출 `DocumentManagementServiceClientImpl` 개체 `retrieveContent` 메서드를 실행하고 다음 값을 전달합니다.

   * 콘텐츠가 추가되는 저장소를 지정하는 문자열 값입니다. 기본 저장소는 입니다. `SpacesStore`. 이 값은 필수 매개 변수입니다.
   * 검색할 콘텐츠의 정규화된 경로를 지정하는 문자열 값(예: `/Company Home/Form Designs/Loan.xdp`). 이 값은 필수 매개 변수입니다.
   * 버전을 지정하는 문자열 값입니다. 이 값은 선택적 매개 변수이며 빈 문자열을 전달할 수 있습니다. 이 경우 최신 버전이 검색됩니다.

   다음 `retrieveContent` 메서드가 을 반환합니다. `CRCResult` xdp 파일이 포함된 개체입니다. 검색 `com.adobe.idp.Document` 를 호출하여 인스턴스 `CRCResult` 개체 `getDocument` 메서드를 사용합니다.

1. 비대화형 PDF 양식 렌더링.

   호출 `OutputClient` 개체 `generatePDFOutput2` 메서드를 실행하고 다음 값을 전달합니다.

   * A `TransformationFormat` 열거형 값입니다. PDF 문서를 생성하려면 다음을 지정합니다 `TransformationFormat.PDF`.
   * 이미지와 같은 추가 리소스가 있는 콘텐츠 루트를 지정하는 문자열 값입니다.
   * A `com.adobe.idp.Document` 양식 디자인을 나타내는 개체(에서 반환된 인스턴스 사용) `CRCResult` 개체 `getDocument` 메서드).
   * A `PDFOutputOptionsSpec` PDF 런타임 옵션이 포함된 객체입니다.
   * A `RenderOptionsSpec` 렌더링 런타임 옵션이 포함된 객체입니다.
   * 다음 `com.adobe.idp.Document` 폼 디자인과 병합할 데이터가 들어 있는 XML 데이터 원본을 포함하는 개체입니다.

   다음 `generatePDFOutput2` 메서드가 다음을 반환합니다. `OutputResult` 작업의 결과를 포함하는 개체입니다.

1. 양식 데이터 스트림으로 작업을 수행합니다.

   * 검색 `com.adobe.idp.Document` 를 호출하여 비대화형 양식을 나타내는 개체 `OutputResult` 개체 `getGeneratedDoc` 메서드를 사용합니다.
   * 만들기 `java.io.File` 작업의 결과를 포함하는 개체입니다. 파일 이름 확장명이 .pdf인지 확인합니다.
   * 호출 `com.adobe.idp.Document` 개체 `copyToFile` 콘텐츠 복사 방법 `com.adobe.idp.Document` 파일에 대한 개체(를 사용해야 함) `com.adobe.idp.Document` 에서 반환한 개체 `getGeneratedDoc` 메서드).

**추가 참조**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[빠른 시작(EJB 모드): Java API를 사용하여 문서를 출력 서비스에 전달](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[빠른 시작(SOAP 모드): Java API를 사용하여 문서를 출력 서비스에 전달](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 출력 서비스에 문서 전달 {#pass-documents-to-the-output-service-using-the-web-service-api}

출력 서비스 및 콘텐츠 서비스(더 이상 사용되지 않음) API(웹 서비스)를 사용하여 콘텐츠 서비스(더 이상 사용되지 않음)에서 검색한 문서를 전달합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 이 클라이언트 애플리케이션은 두 개의 AEM Forms 서비스를 호출하므로 두 개의 서비스 참조를 생성합니다. 출력 서비스와 연관된 서비스 참조에 대해 다음 WSDL 정의를 사용합니다. `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   문서 관리 서비스와 연관된 서비스 참조에 대해 다음 WSDL 정의를 사용합니다. `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   이유: `BLOB` 데이터 유형은 두 서비스 참조에 모두 공통적이므로 `BLOB` 데이터 유형(사용 시) 해당 웹 서비스 빠른 시작에서 모두 `BLOB` 인스턴스가 정규화된 상태입니다.

   >[!NOTE]
   >
   >바꾸기 `localhost` AEM Forms을 호스팅하는 서버의 IP 주소입니다.

1. 출력 및 Document Management 클라이언트 API 객체를 작성합니다.

   * 만들기 `OutputServiceClient` 기본 생성자를 사용하여 개체를 작성합니다.
   * 만들기 `OutputServiceClient.Endpoint.Address` 을 사용하여 개체 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/OutputService?blob=mtom`). 를 사용할 필요가 없습니다. `lc_version` 특성. 이 속성은 서비스 참조를 만들 때 사용됩니다.)
   * 만들기 `System.ServiceModel.BasicHttpBinding` 의 값을 가져와서 개체 `OutputServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스트 `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름 할당 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 해당 암호 값을 필드에 할당합니다. `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 지정 `HttpClientCredentialType.Basic` 필드에 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * 상수 값 지정 `BasicHttpSecurityMode.TransportCredentialOnly` 필드에 `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >다음 단계를 반복합니다. `DocumentManagementServiceClient`서비스 클라이언트.

1. 콘텐츠 서비스에서 양식 디자인을 검색합니다(더 이상 사용되지 않음).

   를 호출하여 콘텐츠 검색 `DocumentManagementServiceClient` 개체 `retrieveContent` 메서드 및 다음 값 전달:

   * 콘텐츠가 추가되는 저장소를 지정하는 문자열 값입니다. 기본 저장소는 입니다. `SpacesStore`. 이 값은 필수 매개 변수입니다.
   * 검색할 콘텐츠의 정규화된 경로를 지정하는 문자열 값(예: `/Company Home/Form Designs/Loan.xdp`). 이 값은 필수 매개 변수입니다.
   * 버전을 지정하는 문자열 값입니다. 이 값은 선택적 매개 변수이며 빈 문자열을 전달할 수 있습니다. 이 경우 최신 버전이 검색됩니다.
   * 찾아보기 링크 값을 저장하는 문자열 출력 매개 변수입니다.
   * A `BLOB` 컨텐츠를 저장하는 출력 매개 변수입니다. 이 출력 매개 변수를 사용하여 콘텐츠를 검색할 수 있습니다.
   * A `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` 컨텐츠 속성을 저장하는 출력 매개 변수.
   * A `CRCResult` 출력 매개 변수. 이 개체를 사용하는 대신 `BLOB` 출력 매개 변수를 사용하여 컨텐츠를 검색합니다.

1. 비대화형 PDF 양식 렌더링.

   호출 `OutputServiceClient` 개체 `generatePDFOutput2` 메서드를 실행하고 다음 값을 전달합니다.

   * A `TransformationFormat` 열거형 값입니다. PDF 문서를 생성하려면 다음을 지정합니다 `TransformationFormat.PDF`.
   * 이미지와 같은 추가 리소스가 있는 콘텐츠 루트를 지정하는 문자열 값입니다.
   * A `BLOB` 양식 디자인을 나타내는 개체(사용) `BLOB` 콘텐츠 서비스에서 반환한 인스턴스(더 이상 사용되지 않음).
   * A `PDFOutputOptionsSpec` PDF 런타임 옵션이 포함된 객체입니다.
   * A `RenderOptionsSpec` 렌더링 런타임 옵션이 포함된 객체입니다.
   * 다음 `BLOB` 폼 디자인과 병합할 데이터가 들어 있는 XML 데이터 원본을 포함하는 개체입니다.
   * 출력 `BLOB` 로 채워지는 개체 `generatePDFOutput2` 메서드를 사용합니다. 다음 `generatePDFOutput2` 메서드는 문서를 설명하는 생성된 메타데이터로 이 개체를 채웁니다. (이 매개 변수 값은 웹 서비스 호출에만 필요합니다.)
   * 출력 `OutputResult` 작업의 결과를 포함하는 개체입니다. (이 매개 변수 값은 웹 서비스 호출에만 필요합니다.)

   다음 `generatePDFOutput2` 메서드가 을 반환합니다. `BLOB` 비대화형 PDF 양식이 포함된 개체입니다.

1. 양식 데이터 스트림으로 작업을 수행합니다.

   * 만들기 `System.IO.FileStream` 해당 생성자를 호출하여 개체를 작성합니다. 대화형 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 콘텐츠를 저장하는 바이트 배열 만들기 `BLOB` 개체에서 검색됨 `generatePDFOutput2` 메서드를 사용합니다. 의 값을 가져와서 바이트 배열 채우기 `BLOB` 개체 `MTOM` 데이터 구성원입니다.
   * 만들기 `System.IO.BinaryWriter` 개체를 호출하고 `System.IO.FileStream` 개체.
   * 를 호출하여 바이트 배열의 내용을 PDF 파일에 씁니다 `System.IO.BinaryWriter` 개체 `Write` 메서드 및 바이트 배열 전달.

**추가 참조**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 저장소의 문서를 출력 서비스로 전달 {#passing-documents-located-in-the-repository-to-the-output-service}

출력 서비스는 일반적으로 XDP 파일로 저장되고 디자이너에서 만들어지는 양식 디자인을 기반으로 하는 비대화형 PDF 양식을 렌더링합니다. 다음을 전달할 수 있습니다. `com.adobe.idp.Document` 출력 서비스에 대한 양식 디자인을 포함하는 개체입니다. 그런 다음 Output 서비스는 `com.adobe.idp.Document` 개체.

를 전달할 때의 이점 `com.adobe.idp.Document` 출력 서비스의 개체는 다른 AEM Forms 서비스 작업에서 `com.adobe.idp.Document` 인스턴스. 즉, 다음을 얻을 수 있습니다. `com.adobe.idp.Document` 다른 서비스 작업의 인스턴스를 렌더링합니다. 예를 들어 다음 그림과 같이 XDP 파일이 AEM Forms 저장소에 저장되어 있다고 가정해 보겠습니다.

![pd_pd_formrepository](assets/pd_pd_formrepository.png)

다음 *양식 폴더* 폴더는 AEM Forms 저장소의 사용자 정의 위치입니다(이 위치는 예제 위치이며 기본적으로 존재하지 않음). 이 예에서는 Loan.xdp라는 양식 디자인이 이 폴더에 있습니다. 양식 디자인 외에도 이미지와 같은 다른 양식 자료가 이 위치에 저장될 수 있습니다. AEM Forms 저장소의 리소스 경로는 다음과 같습니다.

`Applications/Application-name/Application-version/Folder.../Filename`

AEM Forms 저장소에서 프로그래밍 방식으로 Loan.xdp를 검색하여 내의 출력 서비스로 전달할 수 있습니다. `com.adobe.idp.Document` 개체.

다음 두 가지 방법 중 하나를 사용하여 저장소의 XDP 파일을 기반으로 PDF을 만들 수 있습니다. XDP 위치를 참조로 전달하거나 저장소에서 프로그래밍 방식으로 XDP를 검색하여 XDP 파일 내의 출력 서비스로 전달할 수 있습니다.

[빠른 시작(EJB 모드): Java API를 사용하여 애플리케이션 XDP 파일 기반 PDF 문서 생성](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api) (참조에 의해 XDP 파일의 위치를 전달하는 방법을 보여 줍니다.)

[빠른 시작(EJB 모드): Java API를 사용하여 AEM Forms 저장소의 문서를 출력 서비스로 전달](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) ( AEM Forms 저장소에서 XDP 파일을 프로그래밍 방식으로 검색하고 내의 출력 서비스로 전달하는 방법을 보여 줍니다. `com.adobe.idp.Document` 인스턴스). (이 섹션에서는 이 작업을 수행하는 방법에 대해 설명합니다.)

>[!NOTE]
>
>Forms 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-3}

AEM Forms 저장소에서 가져온 문서를 출력 서비스로 전달하려면 다음 작업을 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. 출력 및 Document Management 클라이언트 API 객체를 작성합니다.
1. AEM Forms 저장소에서 양식 디자인을 검색합니다.
1. 비대화형 PDF 양식 렌더링.
1. 데이터 스트림으로 작업을 수행합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함합니다.

**출력 및 Document Management 클라이언트 API 개체 만들기**

출력 서비스 API 작업을 프로그래밍 방식으로 수행하려면 먼저 출력 클라이언트 API 개체를 만듭니다. 또한 이 워크플로우는 콘텐츠 서비스에서 XDP 파일을 검색하므로(더 이상 사용되지 않음) 문서 관리 API 개체를 만듭니다.

**AEM Forms 저장소에서 양식 디자인 가져오기**

저장소 API를 사용하여 AEM Forms 저장소에서 XDP 파일을 검색합니다. (참조: [리소스 읽기](/help/forms/developing/aem-forms-repository.md#reading-resources).)

XDP 파일이 `com.adobe.idp.Document` 인스턴스(또는 a `BLOB` 웹 서비스를 사용하는 경우의 인스턴스). 그런 다음 를 전달할 수 있습니다. `com.adobe.idp.Document` 출력 서비스의 인스턴스입니다.

**비대화형 PDF 양식 렌더링**

비대화형 양식을 렌더링하려면 `com.adobe.idp.Document` AEM Forms 저장소 API를 사용하여 반환된 인스턴스입니다.

>[!NOTE]
>
>이름이 인 두 개의 새 메서드 `generatePDFOutput2`및 `generatePrintedOutput2`수락 `com.adobe.idp.Document`폼 디자인이 포함된 개체입니다. 를 전달할 수도 있습니다. `com.adobe.idp.Document` 네트워크 프린터로 인쇄 스트림을 보낼 때 출력 서비스에 대한 양식 디자인을 포함합니다.

**양식 데이터 스트림으로 작업 수행**

비대화형 양식을 PDF 파일로 저장할 수 있습니다. 양식은 Adobe Reader 또는 Acrobat에서 볼 수 있습니다.

**추가 참조**

[Java API를 사용하여 저장소의 문서를 출력 서비스에 전달](creating-document-output-streams.md#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[출력 서비스 API 빠른 시작](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

ResourceRepositoryClient

### Java API를 사용하여 저장소의 문서를 출력 서비스에 전달 {#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api}

출력 서비스 및 저장소 API(Java)를 사용하여 저장소에서 가져온 문서를 전달합니다.

1. 프로젝트 파일을 포함합니다.

   adobe-output-client.jar 및 adobe-repository-client.jar와 같은 클라이언트 JAR 파일을 Java 프로젝트의 클래스 경로에 포함합니다.

1. 출력 및 Document Management 클라이언트 API 객체를 작성합니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다. (참조: [연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * 만들기 `OutputClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체.
   * 만들기 `DocumentManagementServiceClientImpl` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체.

1. AEM Forms 저장소에서 양식 디자인을 검색합니다.

   호출 `ResourceRepositoryClient` 개체 `readResourceContent` URI 위치를 지정하는 문자열 값을 XDP 파일에 전달합니다. 예, `/Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`. 이 값은 필수입니다. 이 메서드는 `com.adobe.idp.Document` xdp 파일을 나타내는 인스턴스입니다.

1. 비대화형 PDF 양식 렌더링.

   호출 `OutputClient` 개체 `generatePDFOutput2` 메서드를 실행하고 다음 값을 전달합니다.

   * A `TransformationFormat` 열거형 값입니다. PDF 문서를 생성하려면 다음을 지정합니다 `TransformationFormat.PDF`.
   * 이미지와 같은 추가 리소스가 있는 콘텐츠 루트를 지정하는 문자열 값입니다. 예: `repository:///Applications/FormsApplication/1.0/FormsFolder/`
   * A `com.adobe.idp.Document` 양식 디자인을 나타내는 개체(에서 반환된 인스턴스 사용) `ResourceRepositoryClient` 개체 `readResourceContent` 메서드).
   * A `PDFOutputOptionsSpec` PDF 런타임 옵션이 포함된 객체입니다.
   * A `RenderOptionsSpec` 렌더링 런타임 옵션이 포함된 객체입니다.
   * 다음 `com.adobe.idp.Document` 폼 디자인과 병합할 데이터가 들어 있는 XML 데이터 원본을 포함하는 개체입니다.

   다음 `generatePDFOutput2` 메서드가 다음을 반환합니다. `OutputResult` 작업의 결과를 포함하는 개체입니다.

1. 양식 데이터 스트림으로 작업을 수행합니다.

   * 검색 `com.adobe.idp.Document` 를 호출하여 비대화형 양식을 나타내는 개체 `OutputResult` 개체 `getGeneratedDoc` 메서드를 사용합니다.
   * 만들기 `java.io.File` 작업의 결과를 포함하는 개체입니다. 파일 이름 확장명이 .pdf인지 확인합니다.
   * 호출 `com.adobe.idp.Document` 개체 `copyToFile` 콘텐츠 복사 방법 `com.adobe.idp.Document` 파일에 대한 개체(를 사용해야 함) `com.adobe.idp.Document` 에서 반환한 개체 `getGeneratedDoc` 메서드).

**추가 참조**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[빠른 시작(EJB 모드): Java API를 사용하여 AEM Forms 저장소의 문서를 출력 서비스로 전달](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 조각을 사용하여 PDF 문서 생성 {#creating-pdf-documents-using-fragments}

출력 및 어셈블러 서비스를 사용하여 조각을 기반으로 하는 PDF 문서와 같은 출력 스트림을 만들 수 있습니다. 어셈블러 서비스는 여러 XDP 파일의 조각을 기반으로 하는 XDP 문서를 어셈블합니다. 어셈블된 XDP 문서가 출력 서비스로 전달되고 PDF 문서가 만들어집니다. 이 워크플로에서는 생성되는 PDF 문서를 표시하지만 출력 서비스는 이 워크플로에 대한 ZPL과 같은 다른 출력 유형을 생성할 수 있습니다. PDF 문서는 토론 목적으로만 사용됩니다.

다음 그림은 이 워크플로를 보여 줍니다.

![cp_cp_outputassemblefragments](assets/cp_cp_outputassemblefragments.png)

읽기 전 *조각을 사용하여 PDF 문서 생성*, 어셈블러 서비스를 사용하여 여러 XDP 문서를 어셈블하는 방법에 익숙해지는 것이 좋습니다. (참조: [여러 XDP 조각 어셈블](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments).)

>[!NOTE]
>
>어셈블러 서비스에서 어셈블한 양식 디자인을 출력 서비스 대신 Forms 서비스로 전달할 수도 있습니다. Output 서비스와 Forms 서비스의 주요 차이점은 Forms 서비스가 대화형 PDF 문서를 생성하고 Output 서비스가 비대화형 PDF 문서를 생성한다는 것입니다. 또한 Forms 서비스는 ZPL과 같은 프린터 기반 출력 스트림을 생성할 수 없습니다.

>[!NOTE]
>
>출력 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-4}

조각을 기반으로 PDF 문서를 만들려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. 출력 및 어셈블러 클라이언트 개체를 만듭니다.
1. 어셈블러 서비스를 사용하여 양식 디자인을 생성합니다.
1. 출력 서비스를 사용하여 PDF 문서를 생성합니다.
1. PDF 문서를 PDF 파일로 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**출력 및 어셈블러 클라이언트 개체 만들기**

출력 서비스 API 작업을 프로그래밍 방식으로 수행하려면 먼저 출력 클라이언트 API 개체를 만듭니다. 또한 이 워크플로는 어셈블러 서비스를 호출하여 양식 디자인을 만들기 때문에 어셈블러 클라이언트 API 개체를 만듭니다.

**어셈블러 서비스를 사용하여 양식 디자인 생성**

어셈블러 서비스를 사용하여 조각을 사용하여 양식 디자인을 생성합니다. 어셈블러 서비스가 `com.adobe.idp.Document` 양식 디자인을 포함하는 인스턴스입니다.

**출력 서비스를 사용하여 PDF 문서 생성**

출력 서비스를 사용하여 어셈블러 서비스에서 만든 양식 디자인을 사용하여 PDF 문서를 생성할 수 있습니다. 전달 `com.adobe.idp.Document` 어셈블러 서비스가 출력 서비스로 반환한 인스턴스입니다.

**PDF 문서를 PDF 파일로 저장**

출력 서비스에서 PDF 문서를 생성한 후 PDF 파일로 저장할 수 있습니다.

**추가 참조**

[Java API를 사용하여 조각을 기반으로 PDF 문서 만들기](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-java-api)

[웹 서비스 API를 사용하여 조각을 기반으로 PDF 문서 만들기](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[출력 서비스 API 빠른 시작](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[여러 XDP 조각 어셈블](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments)

[PDF 문서 만들기](creating-document-output-streams.md#creating-pdf-documents)

### Java API를 사용하여 조각을 기반으로 PDF 문서 만들기 {#create-a-pdf-document-based-on-fragments-using-the-java-api}

출력 서비스 API 및 어셈블러 서비스 API(Java)를 사용하여 조각을 기반으로 PDF 문서를 만듭니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-output-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. 출력 및 어셈블러 클라이언트 개체를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.
   * 만들기 `OutputClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체.
   * 만들기 `AssemblerServiceClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체.

1. 어셈블러 서비스를 사용하여 양식 디자인을 생성합니다.

   호출 `AssemblerServiceClient` 개체 `invokeDDX` 메서드를 실행하고 다음 필수 값을 전달합니다.

   * A `com.adobe.idp.Document` 사용할 DDX 문서를 나타내는 개체입니다.
   * A `java.util.Map` 입력 XDP 파일이 포함된 개체입니다.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 기본 글꼴과 작업 로그 수준을 포함하여 런타임 옵션을 지정하는 개체입니다.

   다음 `invokeDDX` 메서드가 을 반환합니다. `com.adobe.livecycle.assembler.client.AssemblerResult` 어셈블된 XDP 문서가 포함된 개체입니다. 어셈블된 XDP 문서를 검색하려면 다음 작업을 수행합니다.

   * 호출 `AssemblerResult` 개체 `getDocuments` 메서드를 사용합니다. 이 메서드는 `java.util.Map` 개체.
   * 다음을 반복합니다. `java.util.Map` 결과를 찾을 때까지 오브젝트 `com.adobe.idp.Document` 개체.
   * 호출 `com.adobe.idp.Document` 개체 `copyToFile` 어셈블된 XDP 문서를 추출하는 방법입니다.

1. 출력 서비스를 사용하여 PDF 문서를 생성합니다.

   호출 `OutputClient` 개체 `generatePDFOutput2` 메서드를 실행하고 다음 값을 전달합니다.

   * A `TransformationFormat` 열거형 값입니다. PDF 문서를 생성하려면 다음을 지정합니다 `TransformationFormat.PDF`
   * 이미지와 같은 추가 리소스가 있는 콘텐츠 루트를 지정하는 문자열 값입니다
   * A `com.adobe.idp.Document` 양식 디자인을 나타내는 개체(어셈블러 서비스에서 반환된 인스턴스 사용)
   * A `PDFOutputOptionsSpec` PDF 런타임 옵션이 포함된 개체
   * A `RenderOptionsSpec` 렌더링 런타임 옵션이 포함된 개체
   * 다음 `com.adobe.idp.Document` 폼 디자인과 병합할 데이터가 들어 있는 XML 데이터 원본이 포함된 개체

   다음 `generatePDFOutput2` 메서드가 다음을 반환합니다. `OutputResult` 작업의 결과가 포함된 개체

1. PDF 문서를 PDF 파일로 저장합니다.

   * 검색 `com.adobe.idp.Document` 를 호출하여 PDF 문서를 나타내는 개체 `OutputResult` 개체 `getGeneratedDoc` 메서드를 사용합니다.
   * 만들기 `java.io.File` 작업의 결과를 포함하는 개체입니다. 파일 이름 확장명이 .pdf인지 확인합니다.
   * 호출 `com.adobe.idp.Document` 개체 `copyToFile` 콘텐츠 복사 방법 `com.adobe.idp.Document` 파일에 대한 개체입니다. (다음을 사용해야 합니다. `com.adobe.idp.Document` 이 속한 개체 `getGeneratedDoc` 메서드가 반환되었습니다.).

**추가 참조**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[빠른 시작(EJB 모드): Java API를 사용하여 조각을 기반으로 PDF 문서 만들기](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[빠른 시작(SOAP 모드): Java API를 사용하여 조각을 기반으로 PDF 문서 생성](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### 웹 서비스 API를 사용하여 조각을 기반으로 PDF 문서 만들기 {#create-a-pdf-document-based-on-fragments-using-the-web-service-api}

출력 서비스 API 및 어셈블러 서비스 API(웹 서비스)를 사용하여 조각을 기반으로 PDF 문서를 만듭니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 출력 서비스와 연관된 서비스 참조에 대해 다음 WSDL 정의를 사용합니다.

   ```java
    http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1.
   ```

   어셈블러 서비스와 연결된 서비스 참조에 대해 다음 WSDL 정의를 사용합니다.

   ```java
    http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   이유: `BLOB` 데이터 유형은 두 서비스 참조에 모두 공통적이므로 `BLOB` 데이터 유형(사용 시) 해당 웹 서비스 빠른 시작에서 모두 `BLOB` 인스턴스가 정규화된 상태입니다.

   >[!NOTE]
   >
   >바꾸기 `localhost` AEM Forms을 호스팅하는 서버의 IP 주소입니다.

1. 출력 및 어셈블러 클라이언트 개체를 만듭니다.

   * 만들기 `OutputServiceClient` 기본 생성자를 사용하여 개체를 작성합니다.
   * 만들기 `OutputServiceClient.Endpoint.Address` 을 사용하여 개체 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 를 사용할 필요가 없습니다. `lc_version` 특성. 이 속성은 서비스 참조를 만들 때 사용됩니다. 단, 을 지정합니다. `?blob=mtom` MTOM을 사용합니다.
   * 만들기 `System.ServiceModel.BasicHttpBinding` 의 값을 가져와서 개체 `OutputServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스트 `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * AEM Forms 사용자 이름을 `OutputServiceClient.ClientCredentials.UserName.UserName`필드.
      * 에 해당 암호 값을 할당합니다. `OutputServiceClient.ClientCredentials.UserName.Password`필드.
      * 상수 값 지정 `HttpClientCredentialType.Basic` (으)로 `BasicHttpBindingSecurity.Transport.ClientCredentialType`필드.

   * 할당 `BasicHttpSecurityMode.TransportCredentialOnly` 상수 값 `BasicHttpBindingSecurity.Security.Mode`필드.

   >[!NOTE]
   >
   >다음 단계를 반복합니다. `AssemblerServiceClient`개체.

1. 어셈블러 서비스를 사용하여 양식 디자인을 생성합니다.

   호출 `AssemblerServiceClient` 개체 `invokeDDX` 메서드를 실행하고 다음 값을 전달합니다.

   * A `BLOB` DDX 문서를 나타내는 개체입니다
   * 다음 `MyMapOf_xsd_string_To_xsd_anyType` 필수 파일이 포함된 개체
   * An `AssemblerOptionSpec` 런타임 옵션을 지정하는 개체입니다

   다음 `invokeDDX` 메서드가 다음을 반환합니다. `AssemblerResult` 작업의 결과와 발생한 예외를 포함하는 객체입니다. 새로 만든 XDP 문서를 가져오려면 다음 작업을 수행합니다.

   * 액세스 `AssemblerResult` 개체 `documents` 필드: `Map` 결과 PDF 문서가 포함된 객체입니다.
   * 다음을 반복합니다. `Map` 어셈블된 양식 디자인을 검색하는 개체입니다. 배열 멤버를 캐스팅합니다 `value` (으)로 `BLOB`. 전달 `BLOB` 인스턴스를 출력 서비스로 보냅니다.

1. 출력 서비스를 사용하여 PDF 문서를 생성합니다.

   호출 `OutputServiceClient` 개체 `generatePDFOutput2` 메서드를 실행하고 다음 값을 전달합니다.

   * A `TransformationFormat` 열거형 값입니다. PDF 문서를 생성하려면 다음을 지정합니다 `TransformationFormat.PDF`.
   * 이미지와 같은 추가 리소스가 있는 콘텐츠 루트를 지정하는 문자열 값입니다.
   * A `BLOB` 양식 디자인을 나타내는 개체(사용) `BLOB` 어셈블러 서비스에서 반환된 인스턴스입니다.
   * A `PDFOutputOptionsSpec` PDF 런타임 옵션이 포함된 객체입니다.
   * A `RenderOptionsSpec` 렌더링 런타임 옵션이 포함된 객체입니다.
   * 다음 `BLOB` 폼 디자인과 병합할 데이터가 들어 있는 XML 데이터 원본을 포함하는 개체입니다.
   * 출력 `BLOB` 이 속한 개체 `generatePDFOutput2` 메서드가 채워집니다. 다음 `generatePDFOutput2` 메서드는 문서를 설명하는 생성된 메타데이터로 이 개체를 채웁니다. (이 매개 변수 값은 웹 서비스 호출에만 필요합니다.)
   * 출력 `OutputResult` 작업의 결과를 포함하는 개체입니다. (이 매개 변수 값은 웹 서비스 호출에만 필요합니다.)

   다음 `generatePDFOutput2` 메서드가 을 반환합니다. `BLOB` 비대화형 PDF 양식이 포함된 개체입니다.

1. PDF 문서를 PDF 파일로 저장합니다.

   * 만들기 `System.IO.FileStream` 해당 생성자를 호출하여 개체를 작성합니다. 대화형 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 콘텐츠를 저장하는 바이트 배열 만들기 `BLOB` 개체에서 검색됨 `generatePDFOutput2` 메서드를 사용합니다. 의 값을 가져와서 바이트 배열 채우기 `BLOB` 개체 `MTOM` 데이터 구성원입니다.
   * 만들기 `System.IO.BinaryWriter` 개체를 호출하고 `System.IO.FileStream` 개체.
   * 를 호출하여 바이트 배열의 내용을 PDF 파일에 씁니다 `System.IO.BinaryWriter` 개체 `Write` 메서드 및 바이트 배열 전달.

**추가 참조**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 파일로 인쇄 {#printing-to-files}

출력 서비스를 사용하여 PostScript, PCL(프린터 제어 언어) 또는 다음 레이블 형식과 같은 스트림을 파일로 인쇄할 수 있습니다.

* 얼룩말 - ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

출력 서비스를 사용하면 XML 데이터를 양식 디자인과 병합하고 양식을 파일로 인쇄할 수 있습니다. 다음 그림은 출력 서비스에서 레이저 및 레이블 파일을 생성하는 방법을 보여 줍니다.

>[!NOTE]
>
>인쇄 스트림을 프린터로 보내는 방법에 대한 자세한 내용은 [프린터로 인쇄 스트림 보내기](creating-document-output-streams.md#sending-print-streams-to-printers).

>[!NOTE]
>
>출력 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-5}

파일로 인쇄하려면 다음 단계를 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. 출력 클라이언트 개체를 만듭니다.
1. XML 데이터 소스를 참조합니다.
1. 파일로 인쇄하는 데 필요한 인쇄 런타임 옵션을 설정합니다.
1. 인쇄 스트림을 파일로 인쇄합니다.
1. 작업 결과를 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필수)

AEM Forms이 JBoss가 아닌 지원되는 J2EE 애플리케이션 서버에 배포된 경우 adobe-utilities.jar 및 jbossall-client.jar 파일을 AEM Forms이 배포된 J2EE 애플리케이션 서버에 관련된 JAR 파일로 교체해야 합니다. (참조: [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).)

**출력 클라이언트 개체 만들기**

출력 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 출력 서비스 클라이언트 개체를 만들어야 합니다. Java API를 사용하는 경우 `OutputClient` 개체. Output 웹 서비스 API를 사용하는 경우 `OutputServiceService` 개체.

**XML 데이터 소스 참조**

데이터가 들어 있는 문서를 인쇄하려면 데이터로 채울 모든 양식 필드에 대해 XML 요소가 들어 있는 XML 데이터 원본을 참조해야 합니다. XML 요소 이름은 필드 이름과 일치해야 합니다. XML 요소가 양식 필드에 해당하지 않거나 XML 요소 이름이 필드 이름과 일치하지 않으면 XML 요소가 무시됩니다. 모든 XML 요소를 지정한 경우 XML 요소가 표시되는 순서를 일치시킬 필요는 없습니다.

**파일로 인쇄하는 데 필요한 인쇄 런타임 옵션 설정**

파일로 인쇄하려면 출력 서비스가 인쇄할 파일의 위치와 이름을 지정하여 파일 URI 런타임 옵션을 설정해야 합니다. 예를 들어 Output 서비스가 이름이 인 PostScript 파일을 인쇄하도록 지시하려면 다음을 수행합니다 *MortgageForm.ps* C:\Adobe에 C:\Adobe\MortgageForm.ps을 지정합니다.

>[!NOTE]
>
>정의할 수 있는 선택적 런타임 옵션이 있습니다. 설정할 수 있는 모든 옵션에 대한 자세한 내용은 `PrintedOutputOptionsSpec` 의 클래스 참조 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**파일에 인쇄 스트림 인쇄**

양식 데이터가 포함된 유효한 XML 데이터 원본을 참조하고 인쇄 런타임 옵션을 설정한 후 출력 서비스를 호출하여 파일을 인쇄할 수 있습니다.

**작업 결과 검색**

Output 서비스는 작업을 수행한 후 작업이 성공했는지 여부를 지정하는 XML 데이터와 같은 다양한 데이터 항목을 반환합니다.

**추가 참조**

[Java API를 사용하여 파일에 인쇄](creating-document-output-streams.md#print-to-files-using-the-java-api)

[웹 서비스 API를 사용하여 파일로 인쇄](creating-document-output-streams.md#print-to-files-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[출력 서비스 API 빠른 시작](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java API를 사용하여 파일에 인쇄 {#print-to-files-using-the-java-api}

출력 API(Java)를 사용하여 파일로 인쇄:

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-output-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. 출력 클라이언트 개체를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.
   * 만들기 `OutputClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체.

1. XML 데이터 소스를 참조합니다.

   * 만들기 `java.io.FileInputStream` 해당 생성자를 사용하고 XML 파일의 위치를 지정하는 문자열 값을 전달하여 문서를 채우는 데 사용되는 XML 데이터 소스를 나타내는 개체입니다.
   * 만들기 `com.adobe.idp.Document` 개체를 생성자를 사용하고 `java.io.FileInputStream` 개체.

1. 파일로 인쇄하는 데 필요한 인쇄 런타임 옵션을 설정합니다.

   * 만들기 `PrintedOutputOptionsSpec` 개체를 만들 때 사용됩니다.
   * PrintedOutputOptionsSpec 개체의 `setFileURI` 메서드 및 파일의 이름과 위치를 나타내는 문자열 값 전달 예를 들어 출력 서비스가 C:\Adobe에서 MortgageForm.ps라는 PostScript 파일로 인쇄되도록 하려면 C:\\Adobe\MortgageForm.ps을 지정합니다.
   * 인쇄 매수를 지정하려면 `PrintedOutputOptionsSpec` 개체 `setCopies` 매수를 나타내는 정수 값을 전달하는 메서드입니다.

1. 인쇄 스트림을 파일로 인쇄합니다.

   를 호출하여 파일에 인쇄 `OutputClient` 개체 `generatePrintedOutput` 메서드 및 다음 값 전달:

   * A `PrintFormat` 만들 인쇄 스트림 형식을 지정하는 열거형 값입니다. 예를 들어 PostScript 인쇄 스트림을 만들려면 를 전달합니다 `PrintFormat.PostScript`.
   * 양식 디자인의 이름을 지정하는 문자열 값입니다.
   * 이미지 파일과 같은 관련 자료 파일의 위치를 지정하는 문자열 값입니다.
   * 사용할 XDC 파일의 위치를 지정하는 문자열 값(전달할 수 있음) `null` 를 사용하여 사용할 XDC 파일을 지정한 경우 `PrintedOutputOptionsSpec` 개체)를 참조하십시오.
   * 다음 `PrintedOutputOptionsSpec` 파일로 인쇄하는 데 필요한 런타임 옵션이 들어 있는 개체입니다.
   * 다음 `com.adobe.idp.Document` 양식 데이터가 포함된 XML 데이터 소스가 포함된 객체입니다.

   다음 `generatePrintedOutput` 메서드가 다음을 반환합니다. `OutputResult` 작업의 결과를 포함하는 개체입니다.

   >[!NOTE]
   >
   >다음 `OutputResult` 개체 `getRecordLevelMetaDataList` 메서드 반환 `null`.

1. 작업 결과를 검색합니다.

   * 만들기 `com.adobe.idp.Document` 의 상태를 나타내는 개체 `generatePrintedOutput` 메서드를 호출하여 `OutputResult` 개체 `getStatusDoc` 메서드 (the `OutputResult` 개체가 다음에 의해 반환되었습니다. `generatePrintedOutput` 메서드).
   * 만들기 `java.io.File` 작업의 결과를 포함할 개체입니다. 파일 확장명이 XML인지 확인합니다.
   * 호출 `com.adobe.idp.Document` 개체 `copyToFile` 콘텐츠 복사 방법 `com.adobe.idp.Document` 파일에 대한 개체(를 사용해야 함) `com.adobe.idp.Document` 에서 반환한 개체 `getStatusDoc` 메서드).

**추가 참조**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[빠른 시작(SOAP 모드): Java API를 사용하여 파일에 인쇄](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-printing-to-a-file-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### 웹 서비스 API를 사용하여 파일로 인쇄 {#print-to-files-using-the-web-service-api}

출력 API(웹 서비스)를 사용하여 파일로 인쇄:

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용하는지 확인합니다. `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` AEM Forms을 호스팅하는 서버의 IP 주소입니다.

1. 출력 클라이언트 개체를 만듭니다.

   * 만들기 `OutputServiceClient` 기본 생성자를 사용하여 개체를 작성합니다.
   * 만들기 `OutputServiceClient.Endpoint.Address` 을 사용하여 개체 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 를 사용할 필요가 없습니다. `lc_version` 특성. 이 속성은 서비스 참조를 만들 때 사용됩니다. 단, 을 지정합니다. `?blob=mtom` MTOM을 사용합니다.
   * 만들기 `System.ServiceModel.BasicHttpBinding` 의 값을 가져와서 개체 `OutputServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스트 `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름 할당 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 해당 암호 값을 필드에 할당합니다. `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 지정 `HttpClientCredentialType.Basic` 필드에 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 상수 값 지정 `BasicHttpSecurityMode.TransportCredentialOnly` 필드에 `BasicHttpBindingSecurity.Security.Mode`.

1. XML 데이터 소스를 참조합니다.

   * 만들기 `BLOB` 개체를 만들 때 사용됩니다. 다음 `BLOB` 개체를 사용하여 양식 데이터를 저장합니다.
   * 만들기 `System.IO.FileStream` 개체를 호출하고 양식 데이터가 포함된 XML 파일의 위치를 지정하는 문자열 값을 전달합니다.
   * 의 콘텐츠를 저장하는 바이트 배열 만들기 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채우기 `System.IO.FileStream` 개체 `Read` 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하는 방법.
   * 채우기 `BLOB` 개체 할당 `binaryData` 속성을 바이트 배열의 콘텐츠와 함께 사용합니다.

1. 파일로 인쇄하는 데 필요한 인쇄 런타임 옵션을 설정합니다.

   * 만들기 `PrintedOutputOptionsSpec` 개체를 만들 때 사용됩니다.
   * 파일의 위치 및 이름을 나타내는 문자열 값을 `PrintedOutputOptionsSpec` 개체 `fileURI` 데이터 구성원입니다. 예를 들어 출력 서비스가 라는 PostScript 파일로 인쇄되게 하려면 *MortgageForm.ps* C:\Adobe에서 C:\\Adobe\MortgageForm.ps을 지정합니다.
   * 인쇄 매수를 나타내는 정수 값을 `PrintedOutputOptionsSpec` 개체 `copies` 데이터 멤버.

1. 인쇄 스트림을 파일로 인쇄합니다.

   를 호출하여 파일에 인쇄 `OutputServiceService` 개체 `generatePrintedOutput` 메서드 및 다음 값 전달:

   * A `PrintFormat` 만들 인쇄 스트림 형식을 지정하는 열거형 값입니다. 예를 들어 PostScript 인쇄 스트림을 만들려면 를 전달합니다 `PrintFormat.PostScript`.
   * 양식 디자인의 이름을 지정하는 문자열 값입니다.
   * 이미지 파일과 같은 관련 자료 파일의 위치를 지정하는 문자열 값입니다.
   * 사용할 XDC 파일의 위치를 지정하는 문자열 값(전달할 수 있음) `null` 를 사용하여 사용할 XDC 파일을 지정한 경우 `PrintedOutputOptionsSpec` 개체)를 참조하십시오.
   * 다음 `PrintedOutputOptionsSpec` 파일로 인쇄하는 데 필요한 인쇄 런타임 옵션이 포함된 객체입니다.
   * 다음 `BLOB` 양식 데이터가 포함된 XML 데이터 소스가 포함된 객체입니다.
   * A `BLOB` 로 채워지는 개체 `generatePDFOutput` 메서드를 사용합니다. 다음 `generatePDFOutput` 메서드는 문서를 설명하는 생성된 메타데이터로 이 개체를 채웁니다. 이 매개 변수 값은 웹 서비스 호출에만 필요합니다.
   * A `BLOB` 로 채워지는 개체 `generatePDFOutput` 메서드를 사용합니다. 다음 `generatePDFOutput` 메서드는 이 개체를 결과 데이터로 채웁니다. 이 매개 변수 값은 웹 서비스 호출에만 필요합니다.
   * An `OutputResult` 작업의 결과를 포함하는 개체입니다. 이 매개 변수 값은 웹 서비스 호출에만 필요합니다.

1. 작업 결과를 검색합니다.

   * 만들기 `System.IO.FileStream` 개체를 호출하고 결과 데이터가 포함된 XML 파일 위치를 나타내는 문자열 값을 전달합니다. 파일 확장명이 XML인지 확인합니다.
   * 의 데이터 콘텐츠를 저장하는 바이트 배열 만들기 `BLOB` 에서 결과 데이터로 채운 개체 `OutputServiceService` 개체 `generatePDFOutput` 메서드(여덟 번째 매개 변수). 의 값을 가져와서 바이트 배열 채우기 `BLOB` 개체 `MTOM` 데이터 구성원입니다.
   * 만들기 `System.IO.BinaryWriter` 개체를 호출하고 `System.IO.FileStream` 개체.
   * 바이트 배열의 내용을 XML 파일에 씁니다. `System.IO.BinaryWriter` 개체 `Write` 메서드 및 바이트 배열 전달.

**추가 참조**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 프린터로 인쇄 스트림 보내기 {#sending-print-streams-to-printers}

[출력] 서비스를 사용하여 PostScript, PCL(프린터 제어 언어) 또는 다음 레이블 형식과 같은 인쇄 스트림을 네트워크 프린터로 보낼 수 있습니다.

* 얼룩말 - ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

출력 서비스를 사용하면 XML 데이터를 양식 디자인과 병합하고 양식을 인쇄 스트림으로 출력할 수 있습니다. 예를 들어 PostScript 인쇄 스트림을 만들어 네트워크 프린터로 보낼 수 있습니다. 다음 그림은 인쇄 스트림을 네트워크 프린터로 전송하는 출력 서비스를 보여줍니다.

>[!NOTE]
>
>인쇄 스트림을 네트워크 프린터로 보내는 방법을 보여 주기 위해 이 섹션에서는 SharedPrinter 프로토콜을 사용하여 네트워크 프린터로 PostScript 인쇄 스트림을 보냅니다.

>[!NOTE]
>
>출력 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-6}

인쇄 스트림을 네트워크 프린터로 보내려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. 출력 클라이언트 개체를 만듭니다.
1. XML 데이터 소스를 참조합니다.
1. 인쇄 런타임 옵션 설정
1. 인쇄할 문서를 검색합니다.
1. 문서를 네트워크 프린터로 보냅니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar (AEM Forms이 JBoss에 배포된 경우 필수)

AEM Forms이 JBoss가 아닌 지원되는 J2EE 애플리케이션 서버에 배포된 경우 adobe-utilities.jar 및 jbossall-client.jar 파일을 AEM Forms이 배포된 J2EE 애플리케이션 서버에 관련된 JAR 파일로 교체해야 합니다.

**출력 클라이언트 개체 만들기**

출력 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 출력 서비스 클라이언트 개체를 만듭니다. Java API를 사용하는 경우 `OutputClient` 개체. Output 웹 서비스 API를 사용하는 경우 `OutputServiceClient` 개체.

**XML 데이터 소스 참조**

데이터가 들어 있는 문서를 인쇄하려면 데이터로 채울 모든 양식 필드에 대해 XML 요소가 들어 있는 XML 데이터 원본을 참조해야 합니다. XML 요소 이름은 필드 이름과 일치해야 합니다. XML 요소가 양식 필드에 해당하지 않거나 XML 요소 이름이 필드 이름과 일치하지 않으면 XML 요소가 무시됩니다. 모든 XML 요소를 지정한 경우 XML 요소가 표시되는 순서를 일치시킬 필요는 없습니다.

**인쇄 런타임 옵션 설정**

인쇄 스트림을 프린터로 보낼 때 다음 옵션을 포함하여 런타임 옵션을 설정할 수 있습니다.

* **사본**: 프린터로 보낼 복사본 수를 지정합니다. 기본값은 1입니다.
* **스테이플**: 스테이플러를 사용할 때 XCI 옵션이 설정됩니다. 이 옵션은 스테이플 요소로 구성 모델에 지정할 수 있으며 PS 및 PCL 프린터에만 사용됩니다.
* **출력 조그**: XCI 옵션은 출력 페이지를 조깅해야 할 때(출력 트레이에서 물리적으로 전환됨) 설정됩니다. 이 옵션은 PS 및 PCL 프린터에만 해당됩니다.
* **OutputBin**: 인쇄 드라이버가 적절한 출력 저장소를 선택할 수 있도록 하는 데 사용되는 XCI 값입니다.

>[!NOTE]
>
>설정할 수 있는 모든 런타임 옵션에 대한 자세한 내용은 `PrintedOutputOptionsSpec` 클래스 참조.

**인쇄할 문서 검색**

인쇄 스트림을 검색하여 프린터로 보냅니다. 예를 들어 PostScript 파일을 검색하여 프린터로 보낼 수 있습니다.

프린터가 PDF을 지원하는 경우 PDF 파일을 보내도록 선택할 수 있습니다. 그러나 프린터에 PDF 문서를 보낼 때 발생하는 문제는 각 프린터 제조업체가 PDF 인터프리터의 다른 구현을 가지고 있다는 것입니다. 즉, 일부 인쇄 제조업체는 Adobe PDF 해석을 사용하지만 프린터에 따라 다릅니다. 다른 프린터에는 자체 PDF 인터프리터가 있습니다. 따라서 인쇄 결과가 달라질 수 있습니다.

프린터로 PDF 문서를 보내는 또 다른 제한 사항은 프린터에서 설정을 통하지 않는 한 인쇄만 한다는 것입니다.

인쇄할 문서를 검색하려면 `generatePrintedOutput` 메서드를 사용합니다. 다음 표에서는 를 사용할 때 지정된 인쇄 스트림에 대해 설정되는 콘텐츠 형식을 지정합니다. `generatePrintedOutput` 메서드를 사용합니다.

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
   <td><p>기본 또는 사용자 지정 xdc 출력 스트림으로 dpl203.xdc를 만듭니다.</p></td>
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
   <td><p>일반 색상 PCL </p></td>
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
   <td><p>IPL 300 DPI 출력 스트림을 만듭니다.</p></td>
  </tr>
  <tr>
   <td><p>IPL 400 DPI </p></td>
   <td><p>IPL 400 DPI 출력 스트림을 만듭니다.</p></td>
  </tr>
  <tr>
   <td><p>PCL </p></td>
   <td><p>일반 단색 PCL(5e) 출력 스트림을 만듭니다.</p></td>
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
>를 사용하여 인쇄 스트림을 프린터로 보낼 수도 있습니다. `generatePrintedOutput2` 메서드를 사용합니다. 하지만 프린터로 인쇄 스트림 보내기 섹션과 연관된 빠른 시작은 `generatePrintedOutput` 메서드를 사용합니다.

**네트워크 프린터로 인쇄 스트림 보내기**

인쇄할 문서를 검색한 후 Output 서비스를 호출하면 인쇄 스트림을 네트워크 프린터로 보낼 수 있습니다. 출력 서비스에서 프린터를 성공적으로 찾으려면 인쇄 서버와 프린터 이름을 모두 지정해야 합니다. 또한 인쇄 프로토콜도 지정해야 합니다.

>[!NOTE]
>
>Forms 서버에 PDFG가 설치되어 있고 서버가 Windows Server 2008에서 실행되는 경우 SharedPrinter 속성을 사용할 수 없습니다. 이 경우 다른 프린터 프로토콜을 사용합니다.

>[!NOTE]
>
>네트워크 프린터를 사용하고 있고 액세스 메커니즘이 SharedPrinter인 경우 프린터의 전체 네트워크 경로를 지정해야 합니다.Java API를 사용하여 네트워크 프린터로 인쇄 스트림을 보냅니다

출력 API(Java)를 사용하여 네트워크 프린터로 인쇄 스트림 보내기:

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-output-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. 출력 클라이언트 개체 만들기

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.
   * 만들기 `OutputClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체.

1. XML 데이터 소스 참조

   * 만들기 `java.io.FileInputStream` 해당 생성자를 사용하고 XML 파일의 위치를 지정하는 문자열 값을 전달하여 문서를 채우는 데 사용되는 XML 데이터 소스를 나타내는 개체입니다.
   * 만들기 `com.adobe.idp.Document` 개체를 생성자를 사용하고 `java.io.FileInputStream` 개체.

1. 인쇄 런타임 옵션 설정

   만들기 `PrintedOutputOptionsSpec` 인쇄 런타임 옵션을 나타내는 개체입니다. 예를들어, `PrintedOutputOptionsSpec` 개체 `setCopies` 메서드를 사용합니다.

   >[!NOTE]
   >
   >를 사용하여 페이지 매김 값을 설정할 수 없습니다. `PrintedOutputOptionsSpec` 개체 `setPagination` 메서드는 ZPL 인쇄 스트림을 생성하는 경우에 사용합니다. 마찬가지로 ZPL 인쇄 스트림에 대해 OutputJog, PageOffset 및 Staple 옵션을 설정할 수 없습니다. 다음 `setPagination` 메서드는 PostScript 생성에 유효하지 않습니다. 이 변수는 PCL 생성에만 유효합니다.

1. 인쇄할 문서 검색

   * 다음을 호출하여 인쇄할 문서 검색 `OutputClient` 개체 `generatePrintedOutput` 메서드 및 다음 값 전달:

      * A `PrintFormat` 인쇄 스트림을 지정하는 열거형 값입니다. 예를 들어 PostScript 인쇄 스트림을 만들려면 를 전달합니다 `PrintFormat.PostScript`.
      * 양식 디자인의 이름을 지정하는 문자열 값입니다.
      * 이미지 파일과 같은 관련 자료 파일의 위치를 지정하는 문자열 값입니다.
      * 사용할 XDC 파일의 위치를 지정하는 문자열 값입니다.
      * 다음 `PrintedOutputOptionsSpec` 파일로 인쇄하는 데 필요한 런타임 옵션이 포함된 객체입니다.
      * 다음 `com.adobe.idp.Document` 양식 디자인과 병합할 양식 데이터가 포함된 XML 데이터 소스를 나타내는 개체입니다.

     이 메서드는 `OutputResult` 작업의 결과를 포함하는 개체입니다.

   * 만들기 `com.adobe.idp.Document` 를 호출하여 프린터로 보낼 개체 `OutputResult` 의 오브젝트 `getGeneratedDoc` 메서드를 사용합니다. 이 메서드는 `com.adobe.idp.Document` 개체.

1. 네트워크 프린터로 인쇄 스트림 보내기

   다음을 호출하여 인쇄 스트림을 네트워크 프린터로 보냅니다. `OutputClient` 개체 `sendToPrinter` 메서드 및 다음 값 전달:

   * A `com.adobe.idp.Document` 프린터로 보낼 인쇄 스트림을 나타내는 개체입니다.
   * A `PrinterProtocol` 사용할 프린터 프로토콜을 지정하는 열거형 값입니다. 예를 들어 SharedPrinter 프로토콜을 지정하려면 를 전달합니다 `PrinterProtocol.SharedPrinter`.
   * 인쇄 서버의 이름을 지정하는 문자열 값입니다. 예를 들어 인쇄 서버의 이름이 PrintSever1이라고 가정할 경우 `\\\PrintSever1`.
   * 프린터의 이름을 지정하는 문자열 값입니다. 예를 들어 프린터의 이름이 Printer1이라고 가정하면 `\\\PrintSever1\Printer1`.

   >[!NOTE]
   >
   >다음 `sendToPrinter` 메서드가 버전 8.2.1의 AEM Forms API에 추가되었습니다.

### 웹 서비스 API를 사용하여 프린터로 인쇄 스트림 보내기 {#send-a-print-stream-to-a-printer-using-the-web-service-api}

출력 API(웹 서비스)를 사용하여 네트워크 프린터로 인쇄 스트림 보내기:

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용하는지 확인합니다. `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` AEM Forms을 호스팅하는 서버의 IP 주소입니다.

1. 출력 클라이언트 개체를 만듭니다.

   * 만들기 `OutputServiceClient` 기본 생성자를 사용하여 개체를 작성합니다.
   * 만들기 `OutputServiceClient.Endpoint.Address` 을 사용하여 개체 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 를 사용할 필요가 없습니다. `lc_version` 특성. 이 속성은 서비스 참조를 만들 때 사용됩니다. 단, 을 지정합니다. `?blob=mtom` MTOM을 사용합니다.
   * 만들기 `System.ServiceModel.BasicHttpBinding` 의 값을 가져와서 개체 `OutputServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스트 `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름 할당 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 해당 암호 값을 필드에 할당합니다. `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 지정 `HttpClientCredentialType.Basic` 필드에 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 상수 값 지정 `BasicHttpSecurityMode.TransportCredentialOnly` 필드에 `BasicHttpBindingSecurity.Security.Mode`.

1. XML 데이터 소스를 참조합니다.

   * 만들기 `BLOB` 개체를 만들 때 사용됩니다. 다음 `BLOB` 개체를 사용하여 양식 데이터를 저장합니다.
   * 만들기 `System.IO.FileStream` 해당 생성자를 호출하여 개체를 작성합니다. 양식 데이터가 포함된 XML 파일의 위치를 지정하는 문자열 값을 전달합니다.
   * 의 콘텐츠를 저장하는 바이트 배열 만들기 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열 길이를 결정합니다. `System.IO.FileStream` 개체 `Length` 속성.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채우기 `System.IO.FileStream` 개체 `Read` 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하는 방법.
   * 채우기 `BLOB` 개체 할당 `MTOM` 바이트 배열의 내용이 있는 필드입니다.

1. 인쇄 런타임 옵션을 설정합니다.

   만들기 `PrintedOutputOptionsSpec` 개체를 만들 때 사용됩니다. 예를 들어 인쇄 매수를 나타내는 정수 값을 `PrintedOutputOptionsSpec` 개체 `copies` 데이터 구성원입니다.

   >[!NOTE]
   >
   >를 사용하여 페이지 매김 값을 설정할 수 없습니다. `PrintedOutputOptionsSpec` 개체 `pagination` ZPL 인쇄 스트림을 생성하는 경우 데이터 멤버입니다. 마찬가지로 ZPL 인쇄 스트림에 대해 OutputJog, PageOffset 및 Staple 옵션을 설정할 수 없습니다. 다음 `pagination` 데이터 멤버가 PostScript 생성에 유효하지 않습니다. 이 변수는 PCL 생성에만 유효합니다.

1. 인쇄할 문서를 검색합니다.

   * 다음을 호출하여 인쇄할 문서 검색 `OutputServiceService` 개체 `generatePrintedOutput` 메서드 및 다음 값 전달:

      * A `PrintFormat` 인쇄 스트림을 지정하는 열거형 값입니다. 예를 들어 PostScript 인쇄 스트림을 만들려면 를 전달합니다 `PrintFormat.PostScript`.
      * 양식 디자인의 이름을 지정하는 문자열 값입니다.
      * 이미지 파일과 같은 관련 자료 파일의 위치를 지정하는 문자열 값입니다.
      * 사용할 XDC 파일의 위치를 지정하는 문자열 값입니다.
      * 다음 `PrintedOutputOptionsSpec` 네트워크 프린터로 인쇄 스트림을 보낼 때 사용되는 인쇄 런타임 옵션이 포함된 개체입니다.
      * 다음 `BLOB` 양식 데이터가 포함된 XML 데이터 소스가 포함된 객체입니다.
      * A `BLOB` 로 채워지는 개체 `generatePrintedOutput` 메서드를 사용합니다. 다음 `generatePrintedOutput` 메서드는 문서를 설명하는 생성된 메타데이터로 이 개체를 채웁니다. 이 매개 변수 값은 웹 서비스 호출에만 필요합니다.
      * A `BLOB` 로 채워지는 개체 `generatePrintedOutput` 메서드를 사용합니다. 다음 `generatePrintedOutput` 메서드는 이 개체를 결과 데이터로 채웁니다. 이 매개 변수 값은 웹 서비스 호출에만 필요합니다.
      * An `OutputResult` 작업의 결과를 포함하는 개체입니다. 이 매개 변수 값은 웹 서비스 호출에만 필요합니다.

   * 만들기 `BLOB` 값을 가져와서 프린터로 보낼 개체 `OutputResult` 의 오브젝트 `generatedDoc` 메서드를 사용합니다. 이 메서드는 `BLOB` 개체에서 반환된 PostScript 데이터가 포함된 개체 `generatePrintedOutput` 메서드를 사용합니다.

1. 네트워크 프린터로 인쇄 스트림을 보냅니다.

   다음을 호출하여 인쇄 스트림을 네트워크 프린터로 보냅니다. `OutputClient` 개체 `sendToPrinter` 메서드 및 다음 값 전달:

   * A `BLOB` 프린터로 보낼 인쇄 스트림을 나타내는 개체입니다.
   * A `PrinterProtocol` 사용할 프린터 프로토콜을 지정하는 열거형 값입니다. 예를 들어 SharedPrinter 프로토콜을 지정하려면 를 전달합니다 `PrinterProtocol.SharedPrinter`.
   * A `bool` 이전 매개 변수 값을 사용할지 여부를 지정하는 값입니다. 값 전달 `true`. 이 매개 변수 값은 웹 서비스 호출에만 필요합니다.
   * 인쇄 서버의 이름을 지정하는 문자열 값입니다. 예를 들어 인쇄 서버의 이름이 PrintSever1이라고 가정하면 를 전달합니다 `\\\PrintSever1`.
   * 프린터의 이름을 지정하는 문자열 값입니다. 예를 들어 프린터 이름이 Printer1이라고 가정하면 `\\\PrintSever1\Printer1`.

   >[!NOTE]
   >
   >다음 `sendToPrinter` 메서드가 버전 8.2.1의 AEM Forms API에 추가되었습니다.

## 여러 출력 파일 만들기 {#creating-multiple-output-files}

출력 서비스는 XML 데이터 소스 또는 모든 레코드가 포함된 단일 파일 내의 각 레코드에 대해 별도의 문서를 만들 수 있습니다(이 기능은 기본값). 예를 들어 XML 데이터 소스 내에 10개의 레코드가 있고 출력 서비스 API를 사용하여 각 레코드에 대해 별도의 PDF 문서(또는 다른 유형의 출력)를 만들도록 출력 서비스에 지시한다고 가정해 보겠습니다. 결과적으로 출력 서비스는 10개의 PDF 문서를 생성합니다. 문서를 만드는 대신 여러 인쇄 스트림을 프린터로 보낼 수 있습니다.

다음 그림에서는 출력 서비스가 여러 레코드가 포함된 XML 데이터 파일을 처리하는 모습도 보여 줍니다. 그러나 모든 데이터 레코드가 포함된 단일 PDF 문서를 만들도록 출력 서비스에 지시한다고 가정합니다. 이 경우 출력 서비스는 모든 레코드가 포함된 하나의 문서를 생성합니다.

다음 그림은 출력 서비스에서 여러 레코드가 포함된 XML 데이터 파일을 처리하는 방법을 보여 줍니다. 각 데이터 레코드에 대해 별도의 PDF 문서를 생성하도록 출력 서비스에 지시한다고 가정합니다. 이 경우 출력 서비스는 각 데이터 레코드에 대해 별도의 PDF 문서를 생성합니다.

![cm_outputbatchmany](assets/cm_outputbatchmany.png)

다음 XML 데이터는 세 개의 데이터 레코드를 포함하는 데이터 파일의 예를 보여 줍니다.

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

각 데이터 레코드를 시작하고 끝내는 XML 요소는 다음과 같습니다. `LoanRecord`. 이 XML 요소는 여러 파일을 생성하는 응용 프로그램 논리에 의해 참조됩니다.

>[!NOTE]
>
>출력 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-7}

XML 데이터 소스를 기반으로 여러 PDF 파일을 만들려면 다음 단계를 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. 출력 클라이언트 개체를 만듭니다.
1. XML 데이터 소스를 참조합니다.
1. PDF 런타임 옵션을 설정합니다.
1. 렌더링 런타임 옵션을 설정합니다.
1. 여러 PDF 파일을 생성합니다.
1. 작업 결과를 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필수)

AEM Forms이 JBoss가 아닌 지원되는 J2EE 애플리케이션 서버에 배포된 경우 adobe-utilities.jar 및 jbossall-client.jar 파일을 AEM Forms이 배포된 J2EE 애플리케이션 서버에 관련된 JAR 파일로 교체해야 합니다.

**출력 클라이언트 개체 만들기**

출력 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 출력 서비스 클라이언트 개체를 만들어야 합니다. Java API를 사용하는 경우 `OutputClient` 개체. Output 웹 서비스 API를 사용하는 경우 `OutputServiceService` 개체.

**XML 데이터 소스 참조**

여러 레코드가 포함된 XML 데이터 소스를 참조합니다. 데이터 레코드를 구분하려면 XML 요소를 사용해야 합니다. 예를들어, 이 단원의 앞부분에 표시된 예제 XML 데이터 원본에서는 데이터 레코드를 구분하는 XML 요소의 이름이 로 지정됩니다 `LoanRecord`.

데이터로 채울 모든 양식 필드에 XML 요소가 있어야 합니다. XML 요소 이름은 필드 이름과 일치해야 합니다. XML 요소가 양식 필드에 해당하지 않거나 XML 요소 이름이 필드 이름과 일치하지 않으면 XML 요소가 무시됩니다. 모든 XML 요소를 지정한 경우 XML 요소가 표시되는 순서를 일치시킬 필요는 없습니다.

**PDF 런타임 옵션 설정**

Output 서비스가 XML 데이터 원본을 기반으로 여러 파일을 성공적으로 만들 수 있도록 다음과 같은 런타임 옵션을 설정합니다.

* **많은 파일**: 출력 서비스에서 단일 문서를 만들지 아니면 여러 문서를 만들지 지정합니다. 참 또는 거짓을 지정할 수 있습니다. XML 데이터 원본의 각 데이터 레코드에 대해 별도의 문서를 만들려면 true를 지정합니다.
* **파일 URI**: 출력 서비스에서 생성하는 파일의 위치를 지정합니다. 예를 들어 C:\\Adobe\forms\Loan.pdf 을 지정한다고 가정해 보겠습니다. 이 경우 출력 서비스는 Loan.pdf라는 파일을 만들어 C:\\Adobe\forms 폴더에 저장합니다. 여러 파일이 있는 경우 파일 이름은 Loan0001.pdf, Loan0002.pdf, Loan0003.pdf 등입니다. 파일 위치를 지정하면 파일이 클라이언트 컴퓨터가 아닌 서버에 배치됩니다.
* **레코드 이름**: 데이터 레코드를 구분하는 데이터 소스의 XML 요소 이름을 지정합니다. 예를들어, 이 단원의 앞부분에 표시된 예제 XML 데이터 원본에서는 데이터 레코드를 구분하는 XML 요소를 호출합니다 `LoanRecord`. (레코드 이름 런타임 옵션을 설정하는 대신 데이터 레코드를 포함하는 요소 레벨을 나타내는 숫자 값을 지정하여 레코드 레벨을 설정할 수 있습니다. 그러나 레코드 이름 또는 레코드 수준만 설정할 수 있습니다. 두 값을 모두 설정할 수는 없습니다.)

**렌더링 런타임 옵션 설정**

여러 파일을 만드는 동안 렌더링 런타임 옵션을 설정할 수 있습니다. 이러한 옵션이 필요하지 않지만(필요한 출력 런타임 옵션과 달리) 출력 서비스의 성능 향상과 같은 작업을 수행할 수 있습니다. 예를 들어 출력 서비스에서 사용하는 양식 디자인을 캐시하여 성능을 향상시킬 수 있습니다.

출력 서비스는 배치 레코드를 처리할 때 여러 레코드가 포함된 데이터를 증분 방식으로 읽습니다. 즉, 출력 서비스는 데이터를 메모리로 읽어 들이고, 레코드들의 배치가 처리됨에 따라 데이터를 해제한다. 두 런타임 옵션 중 하나가 설정되면 출력 서비스가 증분 방식으로 데이터를 로드합니다. 레코드 이름 런타임 옵션을 설정하면 출력 서비스가 증분 방식으로 데이터를 읽습니다. 마찬가지로, 레코드 수준 런타임 옵션을 2 이상으로 설정하면 출력 서비스가 증분 방식으로 데이터를 읽습니다.

출력 서비스에서 증분 로드를 수행할지 여부를 제어할 수 있습니다. `PDFOutputOptionsSpec` 또는 `PrintedOutputOptionSpec` 개체 `setLazyLoading` 메서드를 사용합니다. 값을 전달할 수 있습니다. `false` 증분 로드를 해제하는 이 메서드로.

**여러 PDF 파일 생성**

여러 데이터 레코드를 포함하는 올바른 XML 데이터 원본을 참조하고 런타임 옵션을 설정한 후 출력 서비스를 호출하여 여러 파일을 생성할 수 있습니다. 여러 레코드를 생성할 때 `OutputResult` 개체 `getGeneratedDoc` 메서드 반환 `null`.

**작업 결과 검색**

출력 서비스는 작업을 수행한 후 작업이 성공했는지 여부를 지정하는 XML 데이터를 반환합니다. 출력 서비스에서 다음 XML을 반환합니다. 이 경우 출력 서비스에서 42개의 문서를 생성했습니다.

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

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[출력 서비스 API 빠른 시작](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java API를 사용하여 여러 PDF 파일 만들기 {#create-multiple-pdf-files-using-the-java-api}

출력 API(Java)를 사용하여 여러 PDF 파일을 만듭니다.

1. 프로젝트 파일 포함&quot;

   Java 프로젝트의 클래스 경로에 adobe-output-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. 출력 클라이언트 개체 만들기

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.
   * 만들기 `OutputClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체.

1. XML 데이터 소스 참조

   * 만들기 `java.io.FileInputStream` 생성자를 사용하고 XML 파일의 위치를 지정하는 문자열 값을 전달하여 여러 레코드가 포함된 XML 데이터 소스를 나타내는 개체입니다.
   * 만들기 `com.adobe.idp.Document` 개체를 생성자를 사용하고 `java.io.FileInputStream` 개체.

1. PDF 런타임 옵션 설정

   * 만들기 `PDFOutputOptionsSpec` 개체를 만들 때 사용됩니다.
   * 다음을 호출하여 많은 파일 옵션을 설정합니다. `PDFOutputOptionsSpec` 개체 `setGenerateManyFiles` 메서드를 사용합니다. 예를 들어 값을 전달합니다 `true` 출력 서비스에서 XML 데이터 원본의 각 레코드에 대해 별도의 PDF 파일을 만들도록 지시합니다. (통과 시 `false`: 출력 서비스는 모든 레코드가 포함된 단일 PDF 문서를 생성합니다.
   * 다음을 호출하여 파일 URI 옵션 설정 `PDFOutputOptionsSpec` 개체 `setFileUri` 출력 서비스에서 생성하는 파일의 위치를 지정하는 문자열 값을 전달합니다. 파일 URI 옵션은 클라이언트 컴퓨터가 아니라 AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버에 상대적입니다.
   * 다음을 호출하여 레코드 이름 옵션을 설정합니다. `OutputOptionsSpec` 개체 `setRecordName` 데이터 레코드를 구분하는 데이터 소스의 XML 요소 이름을 지정하는 문자열 값을 전달하는 메서드입니다. (예를 들어 이 섹션의 앞에 표시된 XML 데이터 소스를 고려하십시오. 데이터 레코드를 구분하는 XML 요소의 이름은 LoanRecord입니다.

1. 렌더링 런타임 옵션 설정

   * 만들기 `RenderOptionsSpec` 개체를 만들 때 사용됩니다.
   * 양식 디자인을 캐시하여 를 호출하여 출력 서비스의 성능을 개선합니다. `RenderOptionsSpec` 개체 `setCacheEnabled` 및 전달 `Boolean` 값 `true`.

1. 여러 PDF 파일 생성

   를 호출하여 여러 PDF 파일 생성 `OutputClient` 개체 `generatePDFOutput` 메서드 및 다음 값 전달:

   * A `TransformationFormat` 열거형 값입니다. PDF 문서를 생성하려면 다음을 지정합니다 `TransformationFormat.PDF`.
   * 양식 디자인의 이름을 지정하는 문자열 값입니다.
   * 양식 디자인이 있는 콘텐츠 루트를 지정하는 문자열 값입니다.
   * A `PDFOutputOptionsSpec` PDF 런타임 옵션이 포함된 객체입니다.
   * A `RenderOptionsSpec` 렌더링 런타임 옵션이 포함된 객체입니다.
   * 다음 `com.adobe.idp.Document` 폼 디자인과 병합할 데이터가 들어 있는 XML 데이터 원본을 포함하는 개체입니다.

   다음 `generatePDFOutput` 메서드가 다음을 반환합니다. `OutputResult` 작업의 결과를 포함하는 개체입니다.

1. 작업 결과 검색

   * 만들기 `java.io.File` 의 결과를 포함할 XML 파일을 나타내는 개체입니다. `generatePDFOutput` 메서드를 사용합니다. 파일 이름 확장명이 .xml인지 확인합니다.
   * 호출 `com.adobe.idp.Document` 개체 `copyToFile` 콘텐츠 복사 방법 `com.adobe.idp.Document` 파일에 대한 개체(를 사용해야 함) `com.adobe.idp.Document` 에서 반환한 개체 `applyUsageRights` 메서드).

**추가 참조**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[빠른 시작(EJB 모드): Java API를 사용하여 여러 PDF 파일 만들기](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-multiple-pdf-files-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 여러 PDF 파일 만들기 {#create-multiple-pdf-files-using-the-web-service-api}

출력 API(웹 서비스)를 사용하여 여러 PDF 파일을 만듭니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용하는지 확인합니다. `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` AEM Forms을 호스팅하는 서버의 IP 주소입니다.

1. 출력 클라이언트 개체를 만듭니다.

   * 만들기 `OutputServiceClient` 기본 생성자를 사용하여 개체를 작성합니다.
   * 만들기 `OutputServiceClient.Endpoint.Address` 을 사용하여 개체 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 를 사용할 필요가 없습니다. `lc_version` 특성. 이 속성은 서비스 참조를 만들 때 사용됩니다. 단, 을 지정합니다. `?blob=mtom` MTOM을 사용합니다.
   * 만들기 `System.ServiceModel.BasicHttpBinding` 의 값을 가져와서 개체 `OutputServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스트 `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름 할당 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 해당 암호 값을 필드에 할당합니다. `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 지정 `HttpClientCredentialType.Basic` 필드에 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 상수 값 지정 `BasicHttpSecurityMode.TransportCredentialOnly` 필드에 `BasicHttpBindingSecurity.Security.Mode`.

1. XML 데이터 소스를 참조합니다.

   * 만들기 `BLOB` 개체를 만들 때 사용됩니다. 다음 `BLOB` 개체는 여러 레코드가 포함된 양식 데이터를 저장하는 데 사용됩니다.
   * 만들기 `System.IO.FileStream` 해당 생성자를 호출하여 개체를 작성합니다. 여러 레코드가 포함된 XML 파일의 파일 위치를 나타내는 문자열 값을 전달합니다.
   * 의 콘텐츠를 저장하는 바이트 배열 만들기 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채우기 `System.IO.FileStream` 개체 `Read` 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하는 방법.
   * 채우기 `BLOB` 개체 할당 `MTOM` 바이트 배열의 내용이 있는 필드입니다.

1. PDF 런타임 옵션을 설정합니다.

   * 만들기 `PDFOutputOptionsSpec` 개체를 만들 때 사용됩니다.
   * 부울 값을 로 할당하여 많은 파일 옵션을 설정합니다. `OutputOptionsSpec` 개체 `generateManyFiles` 데이터 구성원입니다. 예를 들어 값을 할당합니다 `true` 출력 서비스에서 XML 데이터 원본의 각 레코드에 대해 별도의 PDF 파일을 만들도록 이 데이터 멤버에 지시합니다. (할당하는 경우 `false` 이 데이터 멤버에 대해 출력 서비스는 모든 레코드를 포함하는 단일 PDF을 생성합니다.
   * 출력 서비스에서 생성하는 파일의 위치를 지정하는 문자열 값을 로 할당하여 파일 URI 옵션을 설정합니다. `OutputOptionsSpec` 개체 `fileURI` 데이터 구성원입니다. 파일 URI 옵션은 클라이언트 컴퓨터가 아니라 AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버에 상대적입니다.
   * 데이터 레코드를 구분하는 데이터 소스의 XML 요소 이름을 지정하는 문자열 값을 지정하여 레코드 이름 옵션을 설정합니다. `OutputOptionsSpec` 개체 `recordName` 데이터 구성원입니다.
   * 출력 서비스에서 생성하는 사본 수를 지정하는 정수 값을 할당하여 사본 옵션을 설정합니다. `OutputOptionsSpec` 개체 `copies` 데이터 구성원입니다.

1. 렌더링 런타임 옵션을 설정합니다.

   * 만들기 `RenderOptionsSpec` 개체를 만들 때 사용됩니다.
   * 양식 디자인을 캐시하여 값을 할당하여 출력 서비스의 성능을 개선합니다. `true` (으)로 `RenderOptionsSpec` 개체 `cacheEnabled` 데이터 구성원입니다.

1. 여러 PDF 파일을 생성합니다.

   다음을 호출하여 여러 PDF 파일 만들기 `OutputServiceService` 개체 `generatePDFOutput`메서드 및 다음 값 전달:

   * TransformationFormat 열거형 값입니다. PDF 문서를 생성하려면 다음을 지정합니다 `TransformationFormat.PDF`.
   * 양식 디자인의 이름을 지정하는 문자열 값입니다.
   * 양식 디자인이 있는 콘텐츠 루트를 지정하는 문자열 값입니다.
   * A `PDFOutputOptionsSpec` PDF 런타임 옵션이 포함된 객체입니다.
   * A `RenderOptionsSpec` 렌더링 런타임 옵션이 포함된 객체입니다.
   * 다음 `BLOB` 폼 디자인과 병합할 데이터가 들어 있는 XML 데이터 원본을 포함하는 개체입니다.
   * A `BLOB` 로 채워지는 개체 `generatePDFOutput` 메서드를 사용합니다. 다음 `generatePDFOutput` 메서드는 문서를 설명하는 생성된 메타데이터로 이 개체를 채웁니다.
   * A `BLOB` 로 채워지는 개체 `generatePDFOutput` 메서드를 사용합니다. 다음 `generatePDFOutput` 메서드는 이 개체를 결과 데이터로 채웁니다.
   * An `OutputResult` 작업의 결과를 포함하는 개체입니다.

1. 작업 결과 검색

   * 만들기 `System.IO.FileStream` 개체를 호출하고 결과 데이터가 포함된 XML 파일 위치를 나타내는 문자열 값을 전달합니다. 파일 이름 확장명이 .xml인지 확인합니다.
   * 의 데이터 콘텐츠를 저장하는 바이트 배열 만들기 `BLOB` 에서 결과 데이터로 채운 개체 `OutputServiceService` 개체 `generatePDFOutput` 메서드(여덟 번째 매개 변수). 의 값을 가져와서 바이트 배열 채우기 `BLOB` 개체 `binaryData` 데이터 구성원입니다.
   * 만들기 `System.IO.BinaryWriter` 개체를 호출하고 `System.IO.FileStream` 개체.
   * 바이트 배열의 내용을 XML 파일에 씁니다. `System.IO.BinaryWriter` 개체 `Write` 메서드 및 바이트 배열 전달.

**추가 참조**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 검색 규칙 만들기 {#creating-search-rules}

출력 서비스에서 입력 데이터를 검사하고 데이터 콘텐츠를 기반으로 다양한 양식 디자인을 사용하여 출력을 생성하는 검색 규칙을 만들 수 있습니다. 예를 들어 *저당* 입력 데이터 내에 있는 경우 출력 서비스는 Mortgage.xdp라는 양식 디자인을 사용할 수 있습니다. 마찬가지로 텍스트가 *자동차* 입력 데이터에 있는 경우 출력 서비스는 AutomobileLoan.xdp로 저장된 양식 디자인을 사용할 수 있습니다. 출력 서비스는 다른 출력 유형을 생성할 수 있지만 이 섹션에서는 출력 서비스가 PDF 파일을 생성한다고 가정합니다. 다음 다이어그램은 XML 데이터 파일을 처리하고 여러 양식 디자인 중 하나를 사용하여 PDF 파일을 생성하는 출력 서비스를 보여 줍니다.

또한 출력 서비스는 문서 패키지를 생성할 수 있습니다. 데이터 세트에 여러 개의 레코드가 제공되고 각 레코드가 양식 디자인과 일치하며 단일 문서가 여러 개의 양식 디자인으로 구성됩니다.

![cs_outputbatchmanyformdesigns2](assets/cs_outputbatchmanyformdesigns2.png)

>[!NOTE]
>
>출력 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-8}

문서를 생성하는 동안 검색 규칙을 사용하도록 출력 서비스에 지시하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. 출력 클라이언트 개체를 만듭니다.
1. XML 데이터 소스를 참조합니다.
1. 검색 규칙을 정의합니다.
1. PDF 런타임 옵션을 설정합니다.
1. 렌더링 런타임 옵션을 설정합니다.
1. PDF 문서를 생성합니다.
1. 작업 결과를 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 생성하는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar (AEM Forms이 JBoss에 배포된 경우 필수)

AEM Forms이 JBoss가 아닌 지원되는 J2EE 애플리케이션 서버에 배포된 경우 adobe-utilities.jar 및 jbossall-client.jar을 AEM Forms이 배포된 J2EE 애플리케이션 서버에 관련된 JAR 파일로 교체해야 합니다.

**출력 클라이언트 개체 만들기**

출력 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 출력 서비스 클라이언트 개체를 만들어야 합니다.

**XML 데이터 소스 참조**

데이터로 채울 모든 양식 필드에 XML 요소가 있어야 합니다. XML 요소 이름은 필드 이름과 일치해야 합니다. XML 요소가 양식 필드에 해당하지 않거나 XML 요소 이름이 필드 이름과 일치하지 않으면 XML 요소가 무시됩니다. 모든 XML 요소를 지정하는 한 XML 요소가 표시되는 순서를 일치시킬 필요는 없습니다.

**검색 규칙 정의**

검색 규칙을 정의하려면 출력 서비스에서 입력 데이터에서 검색하는 하나 이상의 텍스트 패턴을 정의합니다. 정의하는 각 텍스트 패턴에 대해 텍스트 패턴이 있는 경우 사용되는 해당 양식 디자인을 지정합니다. 텍스트 패턴이 있으면 출력 서비스는 해당 양식 디자인을 사용하여 출력을 생성합니다. 텍스트 패턴의 예는 다음과 같습니다. *저당*.

>[!NOTE]
>
>텍스트 패턴이 없으면 기본 양식이 사용됩니다. 사용하는 모든 양식 디자인이 컨텐츠 루트에 있는지 확인합니다.

**PDF 런타임 옵션 설정**

출력 서비스에서 여러 양식 디자인을 기반으로 PDF 문서를 성공적으로 만들려면 다음 PDF 런타임 옵션을 설정하십시오.

* **파일 URI**: 출력 서비스에서 생성하는 PDF 파일의 이름과 위치를 지정합니다.
* **규칙**: 정의한 규칙을 지정합니다.
* **LookAhead**: 정의된 텍스트 패턴을 스캔하기 위해 입력 데이터 파일의 시작 부분부터 사용할 바이트 수를 지정합니다. 기본값은 500바이트입니다.

**렌더링 런타임 옵션 설정**

PDF 파일을 만드는 동안 렌더링 런타임 옵션을 설정할 수 있습니다. PDF 런타임 옵션과 달리 이러한 옵션이 필요하지 않지만 출력 서비스의 성능 향상과 같은 작업을 수행할 수 있습니다. 예를 들어 출력 서비스에서 사용하는 양식 디자인을 캐시하여 성능을 향상시킬 수 있습니다.

**PDF 문서 생성**

유효한 XML 데이터 소스를 참조하고 런타임 옵션을 설정한 후 출력 서비스를 호출하여 PDF 문서를 생성할 수 있습니다. 출력 서비스가 입력 데이터에서 지정된 텍스트 패턴을 찾으면 해당 양식 디자인을 사용합니다. 텍스트 패턴이 사용되지 않으면 출력 서비스에서 기본 양식 디자인을 사용합니다.

**작업 결과 검색**

출력 서비스는 작업을 수행한 후 작업이 성공했는지 여부를 지정하는 XML 데이터를 반환합니다.

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[출력 서비스 API 빠른 시작](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java API를 사용하여 검색 규칙 만들기 {#create-search-rules-using-the-java-api}

출력 API(Java)를 사용하여 검색 규칙을 만듭니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-output-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. 출력 클라이언트 개체를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.
   * 만들기 `OutputClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체.

1. XML 데이터 소스를 참조합니다.

   * 만들기 `java.io.FileInputStream` PDF 문서의 생성자를 사용하고 XML 파일의 위치를 지정하는 문자열 값을 전달하여 XML 데이터 소스를 채우는 데 사용되는 개체를 나타냅니다.
   * 만들기 `com.adobe.idp.Document` 개체를 생성자를 사용하고 `java.io.FileInputStream` 개체.

1. 검색 규칙을 정의합니다.

   * 만들기 `Rule` 개체를 만들 때 사용됩니다.
   * 다음을 호출하여 텍스트 패턴 정의 `Rule` 개체 `setPattern` 메서드 및 텍스트 패턴을 지정하는 문자열 값 전달
   * 를 호출하여 해당 양식 디자인을 정의합니다. `Rule` 개체 `setForm` 메서드 . 양식 디자인의 이름을 지정하는 문자열 값을 전달합니다.

   >[!NOTE]
   >
   >정의하려는 각 텍스트 패턴에 대해 앞의 세 단계를 반복합니다.

   * 만들기 `java.util.List` 을 사용하여 개체 `java.util.ArrayList` 생성자입니다.
   * 각 `Rule` 작성한 개체를 호출합니다. `java.util.List` 개체 `add` 메서드 및 전달 `Rule` 개체.

1. PDF 런타임 옵션을 설정합니다.

   * 만들기 `PDFOutputOptionsSpec` 개체를 만들 때 사용됩니다.
   * Output 서비스가 를 호출하여 생성하는 PDF 파일의 이름과 위치를 지정합니다. `PDFOutputOptionsSpec` 개체 `setFileURI` 메서드를 사용합니다. PDF 파일의 위치를 지정하는 문자열 값을 전달합니다. 파일 URI 옵션은 클라이언트 컴퓨터가 아니라 AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버에 상대적입니다.
   * 를 호출하여 정의한 규칙을 설정합니다. `PDFOutputOptionsSpec` 개체 `setRules` 메서드를 사용합니다. 전달 `java.util.List` 이 포함된 개체 `Rule` 개체.
   * 를 호출하여 정의된 텍스트 패턴을 검색할 바이트 수를 설정합니다. `PDFOutputOptionsSpec` 개체 `setLookAhead` 메서드를 사용합니다. 바이트 수를 나타내는 정수 값을 전달합니다.

1. 렌더링 런타임 옵션을 설정합니다.

   * 만들기 `RenderOptionsSpec` 개체를 만들 때 사용됩니다.
   * 양식 디자인을 캐시하여 를 호출하여 출력 서비스의 성능을 개선합니다. `RenderOptionsSpec` 개체 `setCacheEnabled` 및 통과 `true`.

1. PDF 문서를 생성합니다.

   를 호출하여 여러 양식 디자인을 기반으로 하는 PDF 문서 생성 `OutputClient` 개체 `generatePDFOutput` 메서드 및 다음 값 전달:

   * A `TransformationFormat` 열거형 값입니다. PDF 문서를 생성하려면 다음을 지정합니다 `TransformationFormat.PDF`.
   * 기본 양식 디자인의 이름을 지정하는 문자열 값입니다. 즉, 텍스트 패턴이 없는 경우에 사용되는 양식 디자인입니다.
   * 양식 디자인이 있는 콘텐츠 루트를 지정하는 문자열 값입니다.
   * A `PDFOutputOptionsSpec` PDF 런타임 옵션이 포함된 객체입니다.
   * A `RenderOptionsSpec` 렌더링 런타임 옵션이 포함된 객체입니다.
   * 다음 `com.adobe.idp.Document` 출력 서비스에서 정의된 텍스트 패턴을 검색하는 양식 데이터가 포함된 개체입니다.

   다음 `generatePDFOutput` 메서드가 다음을 반환합니다. `OutputResult` 작업의 결과를 포함하는 개체입니다.

1. 작업 결과를 검색합니다.

   * 만들기 `com.adobe.idp.Document` 의 상태를 나타내는 개체 `generatePDFOutput` 메서드를 호출하여 `OutputResult` 개체 `getStatusDoc` 메서드를 사용합니다.
   * 만들기 `java.io.File` 작업의 결과를 포함할 개체입니다. 파일 확장명이 .xml인지 확인합니다.
   * 호출 `com.adobe.idp.Document` 개체 `copyToFile` 콘텐츠 복사 방법 `com.adobe.idp.Document` 파일에 대한 개체(를 사용해야 함) `com.adobe.idp.Document` 에서 반환한 개체 `getStatusDoc` 메서드).

**추가 참조**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[빠른 시작(EJB 모드): Java API를 사용하여 검색 규칙 만들기](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[빠른 시작(SOAP 모드): Java API를 사용하여 검색 규칙 만들기](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 검색 규칙 만들기 {#create-search-rules-using-the-web-service-api}

출력 API(웹 서비스)를 사용하여 검색 규칙을 만듭니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용하는지 확인합니다. `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` AEM Forms을 호스팅하는 서버의 IP 주소입니다.

1. 출력 클라이언트 개체를 만듭니다.

   * 만들기 `OutputServiceClient` 기본 생성자를 사용하여 개체를 작성합니다.
   * 만들기 `OutputServiceClient.Endpoint.Address` 을 사용하여 개체 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 를 사용할 필요가 없습니다. `lc_version` 특성. 이 속성은 서비스 참조를 만들 때 사용됩니다. 단, 을 지정합니다. `?blob=mtom` MTOM을 사용합니다.
   * 만들기 `System.ServiceModel.BasicHttpBinding` 의 값을 가져와서 개체 `OutputServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스트 `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름 할당 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 해당 암호 값을 필드에 할당합니다. `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 지정 `HttpClientCredentialType.Basic` 필드에 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 상수 값 지정 `BasicHttpSecurityMode.TransportCredentialOnly` 필드에 `BasicHttpBindingSecurity.Security.Mode`.

1. XML 데이터 소스를 참조합니다.

   * 만들기 `BLOB` 개체를 만들 때 사용됩니다. 다음 `BLOB` 객체는 PDF 문서와 병합될 데이터를 저장하는 데 사용됩니다.
   * 만들기 `System.IO.FileStream` 객체를 생성합니다. 생성자를 호출하고 암호화할 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 콘텐츠를 저장하는 바이트 배열 만들기 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채우기 `System.IO.FileStream` 개체 `Read` 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하는 방법.
   * 채우기 `BLOB` 개체 할당 `MTOM` 바이트 배열의 내용이 있는 필드입니다.

1. 검색 규칙을 정의합니다.

   * 만들기 `Rule` 개체를 만들 때 사용됩니다.
   * 텍스트 패턴을 지정하는 문자열 값을 `Rule` 개체 `pattern` 데이터 구성원입니다.
   * 양식 디자인을 지정하는 문자열 값을 `Rule` 개체 `form` 데이터 구성원입니다.

   >[!NOTE]
   >
   >정의하려는 각 텍스트 패턴에 대해 앞의 세 단계를 반복합니다.

   * 만들기 `MyArrayOf_xsd_anyType` 규칙을 저장하는 개체입니다.
   * 각각 할당 `Rule` 의 요소에 대한 오브젝트 `MyArrayOf_xsd_anyType` 배열입니다. 호출 `MyArrayOf_xsd_anyType` 개체 `Add` 각각에 대한 방법 `Rule` 개체.

1. PDF 런타임 옵션 설정

   * 만들기 `PDFOutputOptionsSpec` 개체를 만들 때 사용됩니다.
   * 출력 서비스에서 생성하는 PDF 파일의 위치를 지정하는 문자열 값을 로 할당하여 파일 URI 옵션을 설정합니다. `PDFOutputOptionsSpec` 개체 `fileURI` 데이터 구성원입니다. 파일 URI 옵션은 클라이언트 컴퓨터가 아니라 AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버에 상대적입니다.
   * 출력 서비스에서 생성하는 사본 수를 지정하는 정수 값을 할당하여 사본 옵션을 설정합니다. `PDFOutputOptionsSpec` 개체 `copies` 데이터 구성원입니다.
   * 다음을 할당하여 정의한 규칙을 설정합니다. `MyArrayOf_xsd_anyType` 에 규칙을 저장하는 객체 `PDFOutputOptionsSpec` 개체 `rules` 데이터 구성원입니다.
   * 검색할 바이트 수를 나타내는 정수 값을 로 할당하여 정의된 텍스트 패턴을 검색할 바이트 수를 설정합니다. `PDFOutputOptionsSpec` 개체 `lookAhead` data 메서드.

1. 렌더링 런타임 옵션 설정

   * 만들기 `RenderOptionsSpec` 개체를 만들 때 사용됩니다.
   * 양식 디자인을 캐시하여 값을 할당하여 출력 서비스의 성능을 개선합니다. `true` (으)로 `RenderOptionsSpec` 개체 `cacheEnabled` 데이터 구성원입니다.

   >[!NOTE]
   >
   >를 사용하여 PDF 문서의 버전을 설정할 수 없습니다 `RenderOptionsSpec` 개체 `pdfVersion` 멤버(입력 문서가 Acrobat 양식인 경우). 출력 PDF 문서에는 Acrobat 양식의 PDF 버전이 유지됩니다. 마찬가지로 를 사용하여 태그가 지정된 PDF 옵션을 설정할 수 없습니다. `RenderOptionsSpec` 개체 `taggedPDF` 메서드, 입력 문서가 Acrobat 양식인 경우

   >[!NOTE]
   >
   >를 사용하여 선형화된 PDF 옵션을 설정할 수 없습니다. `RenderOptionsSpec` 개체 `linearizedPDF` 구성원(입력 PDF 문서가 인증 또는 디지털 서명된 경우) 자세한 내용은 [PDF 문서에 디지털 서명](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).

1. PDF 문서 생성

   를 호출하여 PDF 문서 만들기 `OutputServiceService` 개체 `generatePDFOutput`메서드 및 다음 값 전달:

   * A `TransformationFormat` 열거형 값입니다. PDF 문서를 생성하려면 다음을 지정합니다 `TransformationFormat.PDF`.
   * 양식 디자인의 이름을 지정하는 문자열 값입니다.
   * 양식 디자인이 있는 콘텐츠 루트를 지정하는 문자열 값입니다.
   * A `PDFOutputOptionsSpec` PDF 런타임 옵션이 포함된 객체입니다.
   * A `RenderOptionsSpec` 렌더링 런타임 옵션이 포함된 객체입니다.
   * 다음 `BLOB` 폼 디자인과 병합할 데이터가 들어 있는 XML 데이터 원본을 포함하는 개체입니다.
   * A `BLOB` 로 채워지는 개체 `generatePDFOutput` 메서드를 사용합니다. 다음 `generatePDFOutput` 메서드는 문서를 설명하는 생성된 메타데이터로 이 개체를 채웁니다. (이 매개 변수 값은 웹 서비스 호출에만 필요합니다.)
   * A `BLOB` 로 채워지는 개체 `generatePDFOutput` 메서드를 사용합니다. 다음 `generatePDFOutput` 메서드는 이 개체를 결과 데이터로 채웁니다. (이 매개 변수 값은 웹 서비스 호출에만 필요합니다.)
   * An `OutputResult` 작업의 결과를 포함하는 개체입니다. (이 매개 변수 값은 웹 서비스 호출에만 필요합니다.)

   >[!NOTE]
   >
   >를 호출하여 PDF 문서를 생성하는 경우 `generatePDFOutput` 메서드에서 서명, 인증 또는 사용 권한이 포함된 XFA PDF 양식과 데이터를 병합할 수 없습니다. 사용 권한에 대한 자세한 내용은 [PDF 문서에 사용 권한 적용](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).

1. 작업 결과 검색

   * 만들기 `System.IO.FileStream` 개체를 호출하고 결과 데이터가 포함된 XML 파일 위치를 나타내는 문자열 값을 전달합니다. 파일 확장명이 XML인지 확인합니다.
   * 의 데이터 콘텐츠를 저장하는 바이트 배열 만들기 `BLOB` 에서 결과 데이터로 채운 개체 `OutputServiceService` 개체 `generatePDFOutput` 메서드(여덟 번째 매개 변수). 의 값을 가져와서 바이트 배열 채우기 `BLOB` 개체 `MTOM` 데이터 구성원입니다.
   * 만들기 `System.IO.BinaryWriter` 개체를 호출하고 `System.IO.FileStream` 개체.
   * 바이트 배열의 내용을 XML 파일에 씁니다. `System.IO.BinaryWriter` 개체 `Write` 메서드 및 바이트 배열 전달.

**추가 참조**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## PDF 문서 병합 {#flattening-pdf-documents}

출력 서비스를 사용하여 대화형 PDF 문서를 비대화형 PDF으로 변환할 수 있습니다. 대화형 PDF 문서를 사용하면 PDF 문서 필드에 있는 데이터를 입력하거나 수정할 수 있습니다. 대화형 PDF 문서를 비대화형 PDF 문서로 변환하는 프로세스를 호출합니다 *병합*. PDF 문서가 병합되면 사용자는 문서 필드의 데이터를 수정할 수 없습니다. PDF 문서를 병합하는 한 가지 이유는 데이터를 수정할 수 없도록 하기 위해서입니다.

다음 유형의 PDF 문서를 병합할 수 있습니다.

* 대화형 XFA PDF 문서
* Acrobat Forms

비대화형 PDF 문서인 PDF을 병합하려고 하면 예외가 발생합니다.

>[!NOTE]
>
>출력 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-9}

대화형 PDF 문서를 비대화형 PDF 문서로 병합하려면 다음 단계를 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. 출력 클라이언트 개체를 만듭니다.
1. 대화형 PDF 문서를 검색합니다.
1. PDF 문서를 변환합니다.
1. 비대화형 PDF 문서를 PDF 파일로 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필수)

AEM Forms이 JBoss가 아닌 지원되는 J2EE 애플리케이션 서버에 배포된 경우 adobe-utilities.jar 및 jbossall-client.jar 파일을 AEM Forms이 배포된 J2EE 애플리케이션 서버에 관련된 JAR 파일로 교체해야 합니다. 모든 AEM Forms JAR 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**출력 클라이언트 개체 만들기**

출력 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 출력 서비스 클라이언트 개체를 만들어야 합니다. Java API를 사용하는 경우 `OutputClient` 개체. Output 웹 서비스 API를 사용하는 경우 `OutputServiceService` 개체.

**대화형 PDF 문서 검색**

비대화형 PDF 문서로 변형할 대화형 PDF 문서를 검색합니다. 비대화형 PDF 문서를 변형하려고 하면 예외가 발생합니다.

**PDF 문서 변형**

대화형 PDF 문서를 검색한 후 비대화형 PDF 문서로 변환할 수 있습니다. 출력 서비스는 비대화형 PDF 문서를 반환합니다.

**비대화형 PDF 문서를 PDF 파일로 저장**

비대화형 PDF 문서를 PDF 파일로 저장할 수 있습니다.

**추가 참조**

[Java API를 사용하여 PDF 문서 평면화](creating-document-output-streams.md#flatten-a-pdf-document-using-the-java-api)

[웹 서비스 API를 사용하여 PDF 문서 병합](creating-document-output-streams.md#flatten-a-pdf-document-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[출력 서비스 API 빠른 시작](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java API를 사용하여 PDF 문서 평면화 {#flatten-a-pdf-document-using-the-java-api}

출력 API(Java)를 사용하여 대화형 PDF 문서를 비대화형 PDF 문서로 병합합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-output-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. 출력 클라이언트 개체를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.
   * 만들기 `OutputClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체.

1. 대화형 PDF 문서를 검색합니다.

   * 만들기 `java.io.FileInputStream` 해당 생성자를 사용하고 대화형 PDF 파일의 위치를 지정하는 문자열 값을 전달하여 변환할 대화형 PDF 문서를 나타내는 개체입니다.
   * 만들기 `com.adobe.idp.Document` 개체를 생성자를 사용하고 `java.io.FileInputStream` 개체.

1. PDF 문서를 변환합니다.

   를 호출하여 대화형 PDF 문서를 비대화형 PDF 문서로 변환 `OutputServiceService` 개체 `transformPDF` 메서드 및 다음 값 전달:

   * 다음 `com.adobe.idp.Document` 대화형 PDF 문서를 포함하는 개체입니다.
   * A `TransformationFormat` 열거형 값입니다. 비대화형 PDF 문서를 생성하려면 다음을 지정합니다 `TransformationFormat.PDF`.
   * A `PDFARevisionNumber` 개정 번호를 지정하는 열거형 값입니다. 이 매개 변수는 PDF/A 문서를 위한 것이므로 다음을 지정할 수 있습니다 `null`.
   * 수정안 번호 및 연도를 콜론으로 구분하여 나타내는 문자열 값입니다. 이 매개 변수는 PDF/A 문서를 위한 것이므로 다음을 지정할 수 있습니다 `null`.
   * A `PDFAConformance` PDF/A 적합성 수준을 나타내는 열거형 값입니다. 이 매개 변수는 PDF/A 문서를 위한 것이므로 다음을 지정할 수 있습니다 `null`.

   다음 `transformPDF` 메서드가 을 반환합니다. `com.adobe.idp.Document` 비대화형 PDF 문서가 포함된 개체입니다.

1. 비대화형 PDF 문서를 PDF 파일로 저장합니다.

   * 만들기 `java.io.File` 개체를 클릭하고 파일 이름 확장명이 .pdf인지 확인합니다.
   * 호출 `Document` 개체 `copyToFile` 콘텐츠 복사 방법 `Document` 파일에 대한 개체(를 사용해야 함) `Document` 에서 반환한 개체 `transformPDF` 메서드).

**추가 참조**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[빠른 시작(EJB 모드): Java API를 사용하여 PDF 문서 변환](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[빠른 시작(SOAP 모드): Java API를 사용하여 PDF 문서 변형](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 PDF 문서 병합 {#flatten-a-pdf-document-using-the-web-service-api}

출력 API(웹 서비스)를 사용하여 대화형 PDF 문서를 비대화형 PDF 문서로 병합합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용하는지 확인합니다. `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` AEM Forms을 호스팅하는 서버의 IP 주소입니다.

1. 출력 클라이언트 개체를 만듭니다.

   * 만들기 `OutputServiceClient` 기본 생성자를 사용하여 개체를 작성합니다.
   * 만들기 `OutputServiceClient.Endpoint.Address` 을 사용하여 개체 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 를 사용할 필요가 없습니다. `lc_version` 특성. 이 속성은 서비스 참조를 만들 때 사용됩니다. 단, 을 지정합니다. `?blob=mtom` MTOM을 사용합니다.
   * 만들기 `System.ServiceModel.BasicHttpBinding` 의 값을 가져와서 개체 `OutputServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스트 `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름 할당 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 해당 암호 값을 필드에 할당합니다. `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 지정 `HttpClientCredentialType.Basic` 필드에 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 상수 값 지정 `BasicHttpSecurityMode.TransportCredentialOnly` 필드에 `BasicHttpBindingSecurity.Security.Mode`.

1. 대화형 PDF 문서를 검색합니다.

   * 만들기 `BLOB` 개체를 만들 때 사용됩니다. 다음 `BLOB` 객체는 대화형 PDF 문서를 저장하는 데 사용됩니다.
   * 만들기 `System.IO.FileStream` 개체를 호출하고 대화형 PDF 문서의 파일 위치를 나타내는 문자열 값을 전달합니다.
   * 의 콘텐츠를 저장하는 바이트 배열 만들기 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채우기 `System.IO.FileStream` 개체 `Read` 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하는 방법.
   * 채우기 `BLOB` 개체 할당 `MTOM` 속성을 바이트 배열의 콘텐츠와 함께 사용합니다.

1. PDF 문서를 변환합니다.

   를 호출하여 대화형 PDF 문서를 비대화형 PDF 문서로 변환 `OutputClient` 개체 `transformPDF` 메서드 및 다음 값 전달:

   * A `BLOB` 대화형 PDF 문서를 포함하는 개체입니다.
   * A `TransformationFormat` 열거형 값입니다. 비대화형 PDF 문서를 생성하려면 다음을 지정합니다 `TransformationFormat.PDF`.
   * A `PDFARevisionNumber` 개정 번호를 지정하는 열거형 값입니다.
   * 다음을 수행할지 여부를 지정하는 부울 값 `PDFARevisionNumber` 열거형 값이 사용됩니다. 이 매개 변수는 PDF/A 문서를 위한 것이므로 다음을 지정할 수 있습니다 `false`.
   * 수정안 번호 및 연도를 콜론으로 구분하여 나타내는 문자열 값입니다. 이 매개 변수는 PDF/A 문서를 위한 것이므로 다음을 지정할 수 있습니다 `null`.
   * A `PDFAConformance` PDF/A 적합성 수준을 나타내는 열거형 값입니다.
   * 다음을 수행할지 여부를 지정하는 부울 값 `PDFAConformance` 열거형 값이 사용됩니다. 이 매개 변수는 PDF/A 문서를 위한 것이므로 다음을 지정할 수 있습니다 `false`.

   다음 `transformPDF` 메서드가 을 반환합니다. `BLOB` 비대화형 PDF 문서가 포함된 개체입니다.

1. 비대화형 PDF 문서를 PDF 파일로 저장합니다.

   * 만들기 `System.IO.FileStream` 개체를 호출하고 비대화형 PDF 문서의 파일 위치를 나타내는 문자열 값을 전달합니다.
   * 의 데이터 콘텐츠를 저장하는 바이트 배열 만들기 `BLOB` 에서 반환한 개체 `transformPDF` 메서드를 사용합니다. 의 값을 가져와서 바이트 배열 채우기 `BLOB` 개체 `MTOM` 데이터 구성원입니다.
   * 만들기 `System.IO.BinaryWriter` 개체를 호출하고 `System.IO.FileStream` 개체.
   * 를 호출하여 바이트 배열의 내용을 PDF 파일에 씁니다 `System.IO.BinaryWriter` 개체 `Write` 메서드 및 바이트 배열 전달.

**추가 참조**

[단계 요약](creating-document-output-streams.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
