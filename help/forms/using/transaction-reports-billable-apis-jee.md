---
title: JEE의 AEM Forms에 대한 거래 보고서 청구 가능 API.
description: JEE의 AEM Forms에 대한 트랜잭션으로 계산되는 모든 API의 목록입니다.
topic-tags: forms-manager
feature: Transaction Reports
exl-id: dbb22369-c0a2-4cf6-b01b-096b4de13a14
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 3%

---

# JEE의 AEM Forms에 대한 거래 보고 청구 가능 API {#transaction-reports-billable-apis}

AEM Forms on JEE는 문서를 제출, 처리 및 렌더링하기 위한 여러 API를 제공합니다. 일부 API는 트랜잭션으로 계산되며 다른 API는 무료로 사용할 수 있습니다. 이 문서에서는 트랜잭션으로 분류된 모든 API 목록을 제공합니다. 다음은 청구 가능한 API가 사용되는 몇 가지 일반적인 시나리오입니다.

* 한 형식에서 다른 형식으로 문서 변환
* 동적 PDF 문서 펼치기
* 대화형 PDF 문서를 다른 PDF 문서와 병합

과금 API는 페이지 수, 문서 또는 양식의 길이 또는 렌더링된 문서의 최종 포맷을 고려하지 않습니다.
<!--

* **Forms Submitted:** When data is submitted from any type of form created with AEM Forms and the data is submitted to any data storage repository or database is considered form submission. For example, submitting an HTML5 Form, PDF Forms are accounted as forms submitted. Each form in a form set is considered a submission. For example, if a form set has 5 forms, when the form set is submitted, transaction reporting service counts it as 5 submissions.

* **Documents Rendered:** Generating a document by combining a template and data, digitally signing or certifying a document, using a billable document services API for document services, or converting a document from one format to another are accounted as documents rendered.

-->

다음은 JEE 청구 가능 API 목록입니다. 목록 찾기 [OSGi의 AEM Forms에 대한 청구 가능 API](/help/forms/using/transaction-reports-billable-apis.md).

## 청구 가능 문서 서비스 API {#billable-document-services-apis}

### PDF 서비스 생성 {#generate-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>설명</td>
   <td>거래 보고서 범주</td>
  </tr>
   <tr>
   <td><a>CreatePDF</a></td>
   <td>지원되는 파일 형식에 대한 Adobe PDF을 만듭니다.</td>
   <td>전환<br /> </td>
  </tr>
  <tr>
   <td><a>CreatePDF3</a></td>
   <td>지원되는 파일 형식에 대한 Adobe PDF을 만듭니다. </td>
   <td>전환<br /> </td>
  </tr>
  <tr>
   <td><a> HtmlToPDF</a></td>
   <td>HTML 파일을 Adobe PDF으로 변환합니다. </td>
   <td>전환<br /> </td>
  </tr>
  <tr>
   <td><a>PDF 내보내기</a></td>
   <td>PDF을 지원되는 파일 형식으로 내보냅니다. </td>
   <td>전환<br /> </td>
  </tr>
  <tr>
   <td><a>ExportPDF2</a></td>
   <td><p>PDF을 지원되는 파일 형식으로 내보냅니다.</p> </td>
   <td>전환<br /> </td>
  </tr>
  <tr>
   <td><a>ExportPDF3</a></td>
   <td>PDF을 지원되는 파일 형식으로 내보냅니다.</td>
   <td>전환<br /> </td>
  </tr>
  <tr>
   <td><a>HtmlFileToPDF</a></td>
   <td>HTML 파일을 PDF으로 변환합니다.</td>
   <td>전환<br /> </td>
  </tr>
  <tr>
   <td><a>HtmlToPDF2</a></td>
   <td>HTML 파일을 PDF으로 변환합니다.</td>
   <td>전환<br /> </td>
  </tr>
  <tr>
   <td><a>PDF 최적화</a></td>
   <td>품질에 영향을 주지 않고 불필요한 메타데이터를 제거하여 파일 크기를 줄이도록 PDF을 최적화합니다.</td>
   <td>전환<br /> </td>
  </tr>
 </tbody>
</table>

### DocAssurance 서비스 {#DocAssurance-Service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>설명</td>
   <td>거래 보고서 범주</td>
  </tr>
  <tr>
   <td><a>서명/인증</a><br /> </td>
   <td>이 API를 사용하면 문서의 보안을 유지할 수 있습니다. API를 사용하여 PDF 문서에 서명하고 인증할 수 있습니다.</td>
   <td>전환</td>
  </tr>
 </tbody>
</table>


### Distiller 서비스 {#distiller-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>설명</td>
   <td>거래 보고서 범주</td>
  </tr>
  <tr>
  <tr>
   <td><a>CreatePDF</a></td>
   <td>지원되는 파일 형식에서 Adobe PDF을 만듭니다.</td>
   <td>전환</td>
  </tr>
  <tr>
   <td><a>CreatePDF2</a></td>
   <td>지원되는 파일 형식에서 Adobe PDF을 만듭니다.</td>
   <td>전환</td>
  </tr>
 </tbody>
</table>

<!--

### Document of Record Service (DoR Service) {#document-of-record-service-dor-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aemds/guide/addon/dor/DoRService.html#render-com.adobe.aemds.guide.addon.dor.DoROptions-" target="_blank">render</a></td>
   <td>Invokes the specified render method to generate a document of record using provided parameters.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->

### 출력 서비스 {#output-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>설명</td>
   <td>거래 보고서 범주</td>
  </tr>
  <tr>
   <td><a>generateOutput</a></td>
   <td>데이터와 템플릿을 병합하여 PDF 문서를 만듭니다.</td>
   <td>렌더링된 문서</td>
  </tr>
  <tr>
   <td><a>generatePDFOutput</a></td>
   <td>데이터와 템플릿을 병합하여 PDF 문서를 만듭니다.</td>
   <td>렌더링된 문서</td>
  </tr>
  <tr>
   <td><a>generatePDFOutput2</a></td>
   <td>데이터와 템플릿을 병합하여 PDF 문서를 만듭니다.</td>
   <td>렌더링된 문서</td>
  </tr>
  <tr>
   <td><a>generatePrintedOutput</a></td>
   <td>XDP 및 PDF 문서를 PS(PostScript), PCL(Printer Command Language) 및 ZPL 파일 형식으로 변환합니다. </td>
   <td>렌더링된 문서</td>
  </tr>
  <tr>
   <td><a>generatePrintedOutput2</a></td>
   <td>XDP 및 PDF 문서를 PS(PostScript), PCL(Printer Command Language) 및 ZPL 파일 형식으로 변환합니다. </td>
   <td>렌더링된 문서</td>
  </tr>
  <tr>
   <td><a>pdf 변환</a></td>
   <td>XDP 및 PDF 문서 집합을 PostScript(PS), 프린터 명령 언어(PCL) 및 ZPL 파일 형식 집합으로 변환합니다. </td>
   <td>문서 변환</td>
  </tr>
 </tbody>
</table>

<!-- ### Forms Service {#forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#renderPDFForm-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.PDFFormRenderOptions-" target="_blank">renderPDFForm</a></td>
   <td>Renders PDF Form from XDP templates. The XDP templates are created in Forms Designer.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#exportData-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.DataFormat-" target="_blank">exportData</a></td>
   <td>Extracts data from a PDF Form or XDP templates</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->

### PDF 서비스 변환 {#convert-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>설명</td>
   <td>거래 보고서 범주</td>
  </tr>
  <tr>
   <td><a>toImage2</a></td>
   <td>PDF 문서를 이미지 문서 목록으로 변환합니다. 지원되는 이미지 형식은 JPEG, JPEG 2K, PNG 및 TIFF입니다.</td>
   <td>문서 변환</td>
  </tr>
  <tr>
   <td><a>toPS2</a></td>
   <td>옵션 사양에 지정된 옵션을 사용하여 플랫 PDF 파일을 PostScript 형식으로 변환합니다.</td>
   <td>문서 변환</td>
  </tr>
  <tr>
   <td><a>toSWF</a></td>
   <td>옵션 사양에 지정된 옵션을 사용하여 플랫 PDF 파일을 SWF 형식으로 변환합니다.</td>
   <td>문서 변환</td>
  </tr>
 </tbody>
</table>

### 바코드 Forms 서비스 {#barcoded-forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>설명</td>
   <td>거래 보고서 범주</td>
  </tr>
  <tr>
   <td><a>decode</a></td>
   <td>Document 객체의 모든 바코드를 디코딩하고 바코드에서 검색된 데이터가 포함된 org.w3c.dom.Document 객체를 반환합니다.</td>
   <td>문서 변환</td>
  </tr>
 </tbody>
</table>

### 어셈블러 서비스 {#assembler-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>설명</td>
   <td>거래 보고서 범주</td>
  </tr>
  <tr>
   <td><a>호출</a></td>
   <td>지정된 DDX 문서를 실행하고 결과 문서가 포함된 AssemblerResult 개체를 반환합니다. </td>
   <td>문서 변환</td>
  </tr>
  <tr>
   <td><a>invokeDDX</a></td>
   <td>지정된 DDX 문서를 실행하고 결과 문서가 포함된 AssemblerResult 개체를 반환합니다. </td>
   <td>문서 변환</td>
  </tr>
  <tr>
   <td><a>invokeOneDocument</a></td>
   <td>지정된 옵션을 사용하여 지정된 문서를 PDF/A로 변환합니다.</td>
   <td>문서 변환</td>
  </tr>
  <tr>
   <td><a>invokeDDXOneDocument</a></td>
   <td>지정된 옵션을 사용하여 지정된 문서를 PDF/A로 변환합니다.</td>
   <td>문서 변환</td>
  </tr>
  <tr>
   <td><a>toPDFA</a></td>
   <td>지정된 옵션을 사용하여 지정된 문서를 PDF/A로 변환합니다.</td>
   <td>문서 변환</td>
  </tr>
 </tbody>
</table>

다음 작업 중 하나 이상을 수행하면 호출 API 사용이 트랜잭션으로 계산됩니다.
1. PDF 형식이 아닌 형식에서 PDF 형식으로 변환. 예를 들어 XDP 형식에서 PDF 형식으로 변환됩니다.<!-- catering to both interactive and non-interactive forms of communication, and the conversion from Word to PDF.-->
1. PDF 형식에서 PDF/A 형식으로 변환.
1. PDF 형식에서 PDF 형식이 아닌 형식으로 변환. 예제에서는 PDF 형식에서 이미지 형식으로 변환하거나 PDF 형식에서 텍스트 형식으로 변환할 수 있습니다.

>[!NOTE]
>
>* 어셈블러 서비스의 호출 API는 입력에 따라 다른 서비스의 과금 가능한 API를 내부적으로 호출할 수 있습니다. 그래서, `invoke API` 없음, 단일 또는 다중 트랜잭션으로 계상할 수 있습니다. 계산되는 트랜잭션 수는 입력 및 호출된 내부 API에 따라 다릅니다.
>* 다음과 같은 어셈블러 서비스를 사용하여 생성된 단일 PDF 문서 `invoke` 및 `invokeDDX`는 없음, 단일 또는 다중 트랜잭션으로 처리할 수 있습니다. 계산되는 거래 수는 제공된 항목에 따라 다릅니다 <!--DDX--> 코드.

<!--
### PDF Utility Service  {#pdf-utility-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a>convertPDFtoXDP</a></td>
   <td>Converts a PDF document into an XDP file. For a PDF document to be successfully converted to an XDP file, the PDF document must contain an XFA stream in the AcroForm dictionary.</td>
   <td>Documents Conversion</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->

## 청구 가능 데이터 캡처 API {#billable-data-capture-apis}

<!--All the submission events of Forms, HTML5 Forms, and form set are accounted as transactions. By default, submission of a PDF Form is not accounted as a transaction. Use the provided [transaction recorder API](record-transaction-custom-implementation.md) to record a PDF Forms submission as a transaction.-->

<!--
### Adaptive Forms {#adaptive-forms}

<table>
 <tbody>
  <tr>
   <td><p>Use Case</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Submitting an adaptive form</td>
   <td>Submits an adaptive form to configured submit action. </td>
   <td>Forms Submitted</td>
   <td>
    <ul>
     <li>Successful submissions account for single or two transactions. The number of transactions counted depends upon the type of submit action used for submission. For example, sending PDF through email submit action accounts for two counts of transactions. One transaction for form submission and another for PDF generated using the Document of Record (DOR) service. </li>
     <li>Using the adaptive form within an adaptive form (Adaptive form formset) accounts only single transaction. You can have any number of adaptive forms within an adaptive form.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

-->

<!--### HTML5 Forms {#html-forms}

<table>
 <tbody>
  <tr>
   <td><p>Use Case</p> </td>
   <td>Description </td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Submitting an HTML5 Form</td>
   <td>Submits an HTML5 Form to submit URL configured in the form.</td>
   <td>Forms Submitted</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->

### Forms {#form-set}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>설명</td>
   <td>거래 보고서 범주</td>
  </tr>
  <tr>
   <td>exportData</td>
   <td>양식을 제출합니다.</td>
   <td>제출된 양식</td>
  </tr>
  <tr>
   <td>exportData2</td>
   <td>양식을 제출합니다.</td>
   <td>제출된 양식</td>
  </tr>
  <tr>
   <td>renderForm</td>
   <td>양식을 제출합니다.</td>
   <td>Forms 렌더링됨</td>
  </tr>
  <tr>
   <td>renderHTMLForm</td>
   <td>양식을 제출합니다.</td>
   <td>Forms 렌더링됨</td>
  </tr>
  <tr>
   <td>renderHTMLForm2</td>
   <td>양식을 제출합니다.</td>
   <td>Forms 렌더링됨</td>
  </tr>
  <tr>
   <td>renderPDFForm</td>
   <td>양식을 제출합니다.</td>
   <td>Forms 렌더링됨</td>
  </tr>
  <tr>
   <td>renderPDFForm2</td>
   <td>양식을 제출합니다.</td>
   <td>Forms 렌더링됨</td>
  </tr>
  <tr>
   <td>renderPDFFormWithUsageRights</td>
   <td>양식을 제출합니다.</td>
   <td>Forms 렌더링됨</td>
  </tr>
 </tbody>
</table>

<!-- ## Billable Interactive Communication and Form-centric AEM Workflows on OSGi APIs {#billable-interactive-communication-and-form-centric-aem-workflows-on-osgi-apis}

Assign task and document services steps of Form-centric AEM Workflows on OSGi and all the renditions of interactive communication and are accounted as transactions. Previewing an interactive communication on the author instance and previewing on the publish instance using Agent UI are not accounted as transactions. If a workflow step accounts a transaction and the workflow fails to complete, the transaction count is not reversed.

<!--

### Interactive Communication - Web Channel {#interactive-communication-web-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Rendering a web channel</td>
   <td>Opens the web version of an interactive communication.</td>
   <td>Documents Rendered</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### Interactive Communication - Print Channel {#interactive-communication-print-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/channels/print/api/model/PrintChannel.html" target="_blank">render</a> (convert to PDF)</td>
   <td>Generates the PDF version of an interactive communication.</td>
   <td>Documents Rendered</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

-->


<!--
### Form-centric AEM Workflows on OSGi  {#form-centric-aem-workflows-on-osgi}

<table>
 <tbody>
  <tr>
   <td><p>Use case</p> </td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Submitting an Assign Task step</td>
   <td>Forms Submitted</td>
   <td>
    <div>
    </div> </td>
  </tr>
  <tr>
   <td>Submitting a workflow application startpoint </td>
   <td>Forms Submitted</td>
   <td> </td>
  </tr>
  <tr>
   <td>Submitting an interactive communication (Print Channel) from the Agent UI to a workflow</td>
   <td>Documents Rendered</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->


<!--

WILL ADD THIS ONE - 

## Recording billable APIs as transactions for custom code {#recording-billable-apis-as-transactions-for-custom-code}

Actions like submitting a PDF Form, using Agent UI to preview an interactive communication, using non-standard form submission, and custom implementations are not accounted as transactions. AEM Forms provides an API to record such actions as transactions. You can call the API from your custom implementations to [record a transaction](/help/forms/using/record-transaction-custom-implementation.md).

## Related Articles {#related-articles}

* [Transaction Reports Overview](../../forms/using/transaction-reports-overview.md)
* [Viewing and Understanding a Transaction Reports](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [Record a transaction for custom implementations](/help/forms/using/record-transaction-custom-implementation.md)

-->

## 관련 문서

* [JEE의 AEM Forms에 대한 트랜잭션 보고서 활성화 및 보기](/help/forms/using/transaction-report-overview-jee.md)
* [JEE의 AEM Forms에 대한 사용자 지정 구성 요소 API에 대한 트랜잭션을 기록합니다](/help/forms/using/record-transaction-custom-component-jee.md)
