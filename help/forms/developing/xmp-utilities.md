---
title: XMP 유틸리티 작업
seo-title: XMP 유틸리티 작업
description: XMP 유틸리티 Java 및 웹 서비스 API를 사용하여 프로그래밍 방식으로 XMP 메타데이터를 PDF 문서로 가져와 PDF 문서에서 XMP 메타데이터를 검색하고 저장할 수 있습니다.
seo-description: XMP 유틸리티 Java 및 웹 서비스 API를 사용하여 프로그래밍 방식으로 XMP 메타데이터를 PDF 문서로 가져와 PDF 문서에서 XMP 메타데이터를 검색하고 저장할 수 있습니다.
uuid: 90ce6cef-efe1-456a-8e0c-5ba90249dda0
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 01d5677f-5c87-4a6e-987b-8eda9acc0b27
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '1423'
ht-degree: 0%

---


# XMP 유틸리티 작업 {#working-with-xmp-utilities}

**XMP 유틸리티 서비스 정보**

PDF 문서에는 메타데이터가 포함되어 있는데, 메타데이터는 텍스트 및 그래픽과 같이 문서의 내용과 구분되는 정보에 대한 정보입니다. XMP(Adobe Extensible Metadata Platform)는 문서 메타데이터를 처리하기 위한 표준입니다.

XMP 유틸리티 서비스는 PDF 문서에서 XMP 메타데이터를 검색 및 저장하고 XMP 메타데이터를 PDF 문서로 가져올 수 있습니다.

XMP 유틸리티 서비스를 사용하여 다음 작업을 수행할 수 있습니다.

* 메타데이터를 PDF 문서로 가져올 수 있습니다. (PDF 문서로 메타데이터 가져오기[를 참조하십시오.)](xmp-utilities.md#importing-metadata-into-pdf-documents)
* PDF 문서에서 메타데이터 내보내기 (PDF 문서에서 메타데이터 내보내기[를 참조하십시오.)](xmp-utilities.md#exporting-metadata-from-pdf-documents)

>[!NOTE]
>
>XMP 유틸리티 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

## 메타데이터를 PDF 문서로 가져오기 {#importing-metadata-into-pdf-documents}

XMP 유틸리티 Java 및 웹 서비스 API를 사용하여 프로그래밍 방식으로 XMP 메타데이터를 PDF 문서로 가져올 수 있습니다. 메타데이터는 문서의 작성자 및 문서와 관련된 키워드와 같은 PDF 문서에 대한 정보를 제공합니다. 메타데이터는 다음 그림과 같이 문서의 문서 속성 대화 상자에서 찾을 수 있습니다.

![ww_metadatadialog](assets/ww_ww_metadatadialog.png)

메타데이터를 프로그래밍 방식으로 PDF 문서로 가져오려면 메타데이터 값을 지정하는 기존 XML 문서를 사용하거나 `XMPUtilityMetadata` 유형의 객체를 사용할 수 있습니다. ([AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en) 참조)

>[!NOTE]
>
>이 섹션에서는 XML 문서를 사용하여 메타데이터를 PDF 문서로 가져오는 방법에 대해 설명합니다.

다음 XML 코드에는 이전 그림에 해당하는 메타데이터 값이 포함되어 있습니다. 예를 들어 키워드를 지정하는 굵은체 항목이 있습니다.

```xml
 <?xpacket begin="?" id="W5M0MpCehiHzreSzNTczkc9d"?>
 <x:xmpmeta xmlns:x="adobe:ns:meta/" x:xmptk="Adobe XMP Core 4.2-jc015 52.349034, 2008 Jun 20 00:30:39-PDT (debug)">
       <rdf:RDF xmlns:rdf="https://www.w3.org/1999/02/22-rdf-syntax-ns#">
          <rdf:Description rdf:about=""
                xmlns:xmp="https://ns.adobe.com/xap/1.0/">
             <xmp:MetadataDate>2008-10-22T10:52:21-04:00</xmp:MetadataDate>
             <xmp:CreatorTool>AEM Forms</xmp:CreatorTool>
             <xmp:ModifyDate>2008-10-22T10:52:21-04:00</xmp:ModifyDate>
             <xmp:CreateDate>2008-02-13T11:00:18-05:00</xmp:CreateDate>
          </rdf:Description>
          <rdf:Description rdf:about=""
                xmlns:pdf="https://ns.adobe.com/pdf/1.3/">
             <pdf:Producer>AEM Forms</pdf:Producer>
             <pdf:Keywords>keyword1, keyword2, keyword3,keyword4</pdf:Keywords>
          </rdf:Description>
          <rdf:Description rdf:about=""
                xmlns:xmpMM="https://ns.adobe.com/xap/1.0/mm/">
             <xmpMM:DocumentID>uuid:1cce1f84-331e-4d8d-8538-15441c271dd7</xmpMM:DocumentID>
             <xmpMM:InstanceID>uuid:cdda0ca6-7c91-4771-9dc9-796c8fe59350</xmpMM:InstanceID>
          </rdf:Description>
          <rdf:Description rdf:about=""
                >
             <dc:format>application/pdf</dc:format>
             <dc:description>
                <rdf:Alt>
                   <rdf:li xml:lang="x-default">Adobe Designer Sample</rdf:li>
                </rdf:Alt>
             </dc:description>
             <dc:title>
                <rdf:Alt>
                   <rdf:li xml:lang="x-default">Grant Application</rdf:li>
                </rdf:Alt>
             </dc:title>
             <dc:creator>
                <rdf:Seq>
                   <rdf:li>Tony Blue</rdf:li>
                </rdf:Seq>
             </dc:creator>
             <dc:subject>
                <rdf:Bag>
                   <rdf:li>keyword1</rdf:li>
                   <rdf:li>keyword2</rdf:li>
                   <rdf:li>keyword3</rdf:li>
                   <rdf:li>keyword4</rdf:li>
                </rdf:Bag>
             </dc:subject>
          </rdf:Description>
          <rdf:Description rdf:about=""
                xmlns:desc="https://ns.adobe.com/xfa/promoted-desc/">
             <desc:version rdf:parseType="Resource">
                <rdf:value>1.0</rdf:value>
                <desc:ref>/template/subform[1]</desc:ref>
             </desc:version>
             <desc:contact rdf:parseType="Resource">
                <rdf:value>Adobe Systems Incorporated</rdf:value>
                <desc:ref>/template/subform[1]</desc:ref>
             </desc:contact>
          </rdf:Description>
       </rdf:RDF>
 </x:xmpmeta>
```

>[!NOTE]
>
>XMP 유틸리티 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### {#summary-of-steps} 단계 요약

XMP 메타데이터를 PDF 문서로 가져오려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. XMPUtenityService 클라이언트를 만듭니다.
1. XMP 메타데이터 가져오기 작업을 호출합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**XMPUtenityService 클라이언트 만들기**

XMP 유틸리티 작업을 프로그래밍 방식으로 수행하려면 먼저 XMPUtenityService 클라이언트를 만들어야 합니다. Java API를 사용하면 `XMPUtilityServiceClient` 개체를 만들어 이러한 작업을 수행할 수 있습니다. 웹 서비스 API를 사용하면 `XMPUtilityServiceService` 개체를 사용하여 이 작업을 수행할 수 있습니다.

**XMP 메타데이터 가져오기 작업 호출**

서비스 클라이언트를 만든 후 XMP 메타데이터 가져오기 작업 중 하나를 호출하여 XMP 메타데이터를 지정된 PDF 문서로 가져올 수 있습니다.

**참고 항목**

[Java API를 사용하여 XMP 메타데이터 가져오기](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[웹 서비스 API를 사용하여 XMP 메타데이터 가져오기](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API {#import-xmp-metadata-using-the-java-api}를 사용하여 XMP 메타데이터 가져오기

XMP 유틸리티 API(Java)를 사용하여 XMP 메타데이터를 가져옵니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-pdfility-client.jar 등의 클라이언트 JAR 파일을 포함합니다.

   >[!NOTE]
   >
   >adobe-pdfility-client.jar 파일에는 XMP 유틸리티 서비스를 프로그래밍 방식으로 호출할 수 있는 클래스가 포함되어 있습니다.

1. XMPUtenityService 클라이언트 만들기

   해당 생성자를 사용하고 연결 속성이 포함된 `ServiceClientFactory` 객체를 전달하여 `XMPUtilityServiceClient` 객체를 만듭니다.

1. XMP 메타데이터 가져오기 작업 호출

   XMP 메타데이터를 수정하려면 `XMPUtilityServiceClient` 객체의 `importMetadata` 메서드 또는 해당 `importXMP` 메서드를 호출합니다.

   `importMetadata` 메서드를 사용하는 경우 다음 값을 전달합니다.

   * PDF 파일을 나타내는 `com.adobe.idp.Document` 개체
   * 가져올 메타데이터를 포함하는 `XMPUtilityMetadata` 객체입니다.

   `importXMP` 메서드를 사용하는 경우 다음 값을 전달합니다.

   * PDF 파일을 나타내는 `com.adobe.idp.Document` 개체
   * 가져올 메타데이터가 포함된 XML 파일을 나타내는 `com.adobe.idp.Document` 객체입니다.

   두 경우 모두 반환된 값은 새로 가져온 메타데이터가 있는 PDF 파일을 나타내는 `com.adobe.idp.Document` 객체입니다. 그런 다음 이 개체를 디스크에 저장할 수 있습니다.

**참고 항목**

[메타데이터를 PDF 문서로 가져오기](xmp-utilities.md#importing-metadata-into-pdf-documents)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API {#importing-xmp-metadata-using-the-web-service-api}을(를) 사용하여 XMP 메타데이터 가져오기

XMP 유틸리티 웹 서비스 API를 사용하여 프로그래밍 방식으로 XMP 메타데이터를 가져오려면 다음 작업을 수행하십시오.

1. 프로젝트 파일 포함

   * XMP 유틸리티 서비스 WSDL 파일을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다. (Base64 인코딩[을 사용하여 AEM Forms 호출 참조)](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
   * Microsoft .NET 클라이언트 어셈블리를 참조하십시오. (Base64 인코딩[을 사용하는 .NET 클라이언트 어셈블리 만들기를 참조하십시오.)](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

1. XMPUtenityService 클라이언트 만들기

   프록시 클래스 생성자를 사용하여 `XMPUtilityServiceService` 개체를 만듭니다.

1. XMP 메타데이터 가져오기 작업 호출

   XMP 메타데이터를 수정하려면 `XMPUtilityServiceService` 객체의 `importMetadata` 메서드 또는 해당 `importXMP` 메서드를 호출합니다.

   `importMetadata` 메서드를 사용하는 경우 다음 값을 전달합니다.

   * PDF 파일을 나타내는 `BLOB` 개체
   * 가져올 메타데이터를 포함하는 `XMPUtilityMetadata` 객체입니다.

   `importXMP` 메서드를 사용하는 경우 다음 값을 전달합니다.

   * PDF 파일을 나타내는 `BLOB` 개체
   * 가져올 메타데이터가 포함된 XML 파일을 나타내는 `BLOB` 객체입니다.

   두 경우 모두 반환된 값은 새로 가져온 메타데이터가 있는 PDF 파일을 나타내는 `BLOB` 객체입니다. 그런 다음 이 개체를 디스크에 저장할 수 있습니다.

**참고 항목**

[메타데이터를 PDF 문서로 가져오기](xmp-utilities.md#importing-metadata-into-pdf-documents)

<!--REVIEW: [Quick Start (Base64): Importing XMP metadata using the web service API](unresolvedlink-lc-qs-xmp-utilities-xu.xml#ws624e3cba99b79e12e69a9941333732bac8-7be8.2)-->

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64 인코딩을 사용하는 .NET 클라이언트 어셈블리 만들기](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## PDF 문서에서 메타데이터 내보내기 {#exporting-metadata-from-pdf-documents}

XMP 유틸리티 Java 및 웹 서비스 API를 사용하여 프로그래밍 방식으로 PDF 문서에서 XMP 메타데이터를 검색하고 저장할 수 있습니다.

>[!NOTE]
>
>XMP 유틸리티 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### {#summary_of_steps-1} 단계 요약

PDF 문서에서 XMP 메타데이터를 내보내려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. XMPUtenityService 클라이언트를 만듭니다.
1. XMP 메타데이터 내보내기 작업을 호출합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**XMPUtenityService 클라이언트 만들기**

XMP 유틸리티 작업을 프로그래밍 방식으로 수행하려면 먼저 XMPUtenityService 클라이언트를 만들어야 합니다. Java AP를 사용하면 `XMPUtilityServiceClient` 개체를 만들어 이 작업을 수행할 수 있습니다. 웹 서비스 API를 사용하면 `XMPUtilityServiceService` 개체를 사용하여 완료됩니다.

**XMP 메타데이터 내보내기 작업 호출**

서비스 클라이언트를 만든 후 XMP 메타데이터 내보내기 작업 중 하나를 호출하여 XMP 메타데이터를 검사하거나 디스크에 저장할 수 있습니다.

**참고 항목**

[Java API를 사용하여 XMP 메타데이터 가져오기](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[웹 서비스 API를 사용하여 XMP 메타데이터 가져오기](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API {#export-xmp-metadata-using-the-java-api}를 사용하여 XMP 메타데이터 내보내기

XMP 유틸리티 API(Java)를 사용하여 XMP 메타데이터를 내보냅니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-pdfility-client.jar 등의 클라이언트 JAR 파일을 포함합니다.

   >[!NOTE]
   >
   >adobe-pdfility-client.jar 파일에는 XMP 유틸리티 서비스를 프로그래밍 방식으로 호출할 수 있는 클래스가 포함되어 있습니다.

1. XMPUtenityService 클라이언트 만들기

   해당 생성자를 사용하고 연결 속성이 포함된 `ServiceClientFactory` 객체를 전달하여 `XMPUtilityServiceClient` 객체를 만듭니다.

1. XMP 메타데이터 가져오기 작업 호출

   XMP 메타데이터를 검사하려면 `XMPUtilityServiceClient` 객체의 `exportMetadata` 메서드를 호출하고 PDF 파일을 나타내는 `com.adobe.idp.Document` 객체를 전달합니다. 이 메서드는 검색된 메타데이터가 포함된 `XMPUtilityMetadata` 객체를 반환합니다.

   XMP 메타데이터를 검색하고 저장하려면 `XMPUtilityServiceClient` 객체의 `exportXMP` 메서드를 호출하고 PDF 파일을 나타내는 `com.adobe.idp.Document` 객체를 전달합니다. 이 메서드는 검색된 메타데이터가 포함된 `com.adobe.idp.Document` 객체를 반환합니다. 이 객체는 나중에 디스크에 XML 파일로 저장할 수 있습니다.

**참고 항목**

[PDF 문서에서 메타데이터 내보내기](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API {#export-xmp-metadata-using-the-web-service-api}를 사용하여 XMP 메타데이터 내보내기

XMP 유틸리티 API(웹 서비스)를 사용하여 XMP 메타데이터를 내보냅니다.

1. 프로젝트 파일 포함

   * XMP 유틸리티 서비스 WSDL 파일을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다.
   * Microsoft .NET 클라이언트 어셈블리를 참조하십시오.

1. XMPUtenityService 클라이언트 만들기

   프록시 클래스 생성자를 사용하여 `XMPUtilityServiceService` 개체를 만듭니다.

1. XMP 메타데이터 가져오기 작업 호출

   XMP 메타데이터를 검사하려면 `XMPUtilityServiceClient` 객체의 `exportMetadata` 메서드를 호출하고 PDF 파일을 나타내는 `BLOB` 객체를 전달합니다. 이 메서드는 검색된 메타데이터가 포함된 `XMPUtilityMetadata` 객체를 반환합니다.

   XMP 메타데이터를 검색하고 저장하려면 `XMPUtilityServiceClient` 객체의 `exportXMP` 메서드를 호출하고 PDF 파일을 나타내는 `BLOB` 객체를 전달합니다. 이 메서드는 검색된 메타데이터가 포함된 `BLOB` 객체를 반환합니다. 이 객체는 나중에 디스크에 XML 파일로 저장할 수 있습니다.

**참고 항목**

[PDF 문서에서 메타데이터 내보내기](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64 인코딩을 사용하는 .NET 클라이언트 어셈블리 만들기](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
