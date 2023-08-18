---
title: 거래 보고서 청구 가능 API
seo-title: Transaction Reports Billable APIs
description: 트랜잭션으로 계산되는 모든 API 목록
seo-description: List of all the APIs that are accounted as transactions
uuid: d2f38ae4-75df-426f-af34-52ae6fb324f3
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 929a298d-7f22-487f-bf7d-8ab2556d0d81
docset: aem65
exl-id: 1bc99f3b-3f28-4e74-b259-6ebddc11ffc5
source-git-commit: d636d987f5d62c9169bc4015d7ac50090e362faa
workflow-type: tm+mt
source-wordcount: '2089'
ht-degree: 6%

---

# 거래 보고서 청구 가능 API{#transaction-reports-billable-apis}

AEM Forms은 양식 제출, 문서 처리 및 문서 렌더링에 필요한 여러 API를 제공합니다. 일부 API는 트랜잭션으로 계산되며 다른 API는 무료로 사용할 수 있습니다. 이 문서에서는 거래 보고서에서 거래로 간주되는 모든 API 목록을 제공합니다. 다음은 청구 가능한 API가 사용되는 몇 가지 일반적인 시나리오입니다.

* 적응형 양식, HTML5 양식 및 양식 세트 제출
* 대화형 통신의 인쇄 또는 웹 버전 렌더링
* 한 형식에서 다른 형식으로 문서 변환
* 동적 PDF 문서 펼치기
* 기록 문서 생성
* 대화형 PDF 문서를 다른 PDF 문서와 병합
* AEM Workflow의 작업 할당 단계 및 문서 서비스 단계 사용
* 적응형 양식 내에서 적응형 양식 사용

과금 API는 페이지 수, 문서 또는 양식의 길이 또는 렌더링된 문서의 최종 포맷을 고려하지 않습니다. 트랜잭션 보고서는 트랜잭션을 렌더링된 문서 및 Forms 제출의 두 가지 범주로 나눕니다.

* **Forms 제출됨:** AEM Forms으로 만든 모든 유형의 양식에서 데이터를 제출하고 데이터를 데이터 저장소 또는 데이터베이스로 제출한 경우 양식 제출로 간주됩니다. 예를 들어 적응형 양식, HTML5 양식, PDF forms 및 양식 세트 제출은 제출된 양식으로 계산됩니다. 양식 세트의 각 양식은 제출로 간주됩니다. 예를 들어 양식 세트에 5개의 양식이 있는 경우 양식 세트가 제출되면 거래 보고 서비스는 5개의 제출로 계산합니다.

* **렌더링된 문서:** 템플릿과 데이터를 결합하여 문서를 생성하거나, 문서에 디지털 서명 또는 인증을 하거나, 문서 서비스를 위한 과금 가능한 문서 서비스 API를 사용하거나, 문서를 한 형식에서 다른 형식으로 변환하여 문서를 생성한 문서라고 간주합니다.

>[!NOTE]
>
>트랜잭션 보고서 UI에는 Forms 제출됨, 렌더링된 문서 및 처리된 문서의 세 가지 범주가 표시됩니다. 렌더링된 문서와 처리된 문서는 모두 렌더링된 문서로 계산됩니다.

## 청구 가능 문서 서비스 API {#billable-document-services-apis}

### PDF 서비스 생성 {#generate-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>설명</td>
   <td>거래 보고서 범주</td>
   <td>추가 정보</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a></td>
   <td>지원되는 파일 형식에서 Adobe PDF을 만듭니다.</td>
   <td>처리된 문서</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>지원되는 파일 형식에서 Adobe PDF을 만듭니다.</td>
   <td>처리된 문서</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF</a></td>
   <td>Adobe PDF을 지원되는 파일 유형으로 변환합니다. </td>
   <td>처리된 문서<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF2</a></td>
   <td>Adobe PDF을 지원되는 파일 유형으로 변환합니다. </td>
   <td>처리된 문서<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF3</a></td>
   <td>Adobe PDF을 지원되는 파일 유형으로 변환합니다. </td>
   <td>처리된 문서<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlFileToPdf-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-">htmlFileToPdf</a></td>
   <td><p>HTML 페이지에서 PDF을 만듭니다.</p> </td>
   <td>처리된 문서<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf</a></td>
   <td>HTML 페이지를 가리키는 URL에서 PDF을 만듭니다.</td>
   <td>처리된 문서<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf2-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf2</a></td>
   <td>HTML 페이지를 가리키는 URL에서 PDF을 만듭니다.</td>
   <td>처리된 문서<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#optimizePDF-com.adobe.aemfd.docmanager.Document-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">optimizePDF</a></td>
   <td>품질에 영향을 주지 않고 불필요한 메타데이터를 제거하여 파일 크기를 줄이도록 PDF을 최적화합니다.</td>
   <td>처리된 문서<br /> </td>
   <td> </td>
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
   <td>추가 정보</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/fd/docassurance/client/api/DocAssuranceService.html#secureDocument-com.adobe.aemfd.docmanager.Document-com.adobe.fd.docassurance.client.api.EncryptionOptions-com.adobe.fd.docassurance.client.api.SignatureOptions-com.adobe.fd.docassurance.client.api.ReaderExtensionOptions-com.adobe.fd.signatures.pdf.inputs.UnlockOptions-" target="_blank">secureDocument</a><br /> </td>
   <td>이 API를 사용하면 문서의 보안을 유지할 수 있습니다. API를 사용하여 PDF 문서에 서명, 인증, 리더 확장 또는 암호화할 수 있습니다.</td>
   <td>처리된 문서</td>
   <td>secureDocument의 서명 및 인증 작업만 청구됩니다.</td>
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
   <td>추가 정보</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a><br /> </td>
   <td>지원되는 파일 형식에서 Adobe PDF을 만듭니다.</td>
   <td>처리된 문서</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>지원되는 파일 형식에서 Adobe PDF을 만듭니다.</td>
   <td>처리된 문서</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 기록 문서 서비스(DoR 서비스) {#document-of-record-service-dor-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>설명</td>
   <td>거래 보고서 범주</td>
   <td>추가 정보</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aemds/guide/addon/dor/DoRService.html#render-com.adobe.aemds.guide.addon.dor.DoROptions-" target="_blank">렌더링</a></td>
   <td>지정된 렌더링 메서드를 호출하여 제공된 매개 변수를 사용하여 기록 문서를 생성합니다.</td>
   <td>처리된 문서</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 출력 서비스 {#output-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>설명</td>
   <td>거래 보고서 범주</td>
   <td>추가 정보</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutput-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PDFOutputOptions-" target="_blank">generatePDFOutput</a></td>
   <td>데이터와 템플릿을 병합하여 PDF 문서를 만듭니다.</td>
   <td>처리된 문서</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutput-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PDFOutputOptions-" target="_blank">generatePDFOutput</a></td>
   <td>데이터와 템플릿을 병합하여 PDF 문서를 만듭니다.</td>
   <td>처리된 문서</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutputBatch-java.util.Map-java.util.Map-com.adobe.fd.output.api.PDFOutputOptions-com.adobe.fd.output.api.BatchOptions-" target="_blank">generatePDFOutputBatch</a></td>
   <td>데이터와 템플릿을 병합하여 PDF 문서 세트를 만듭니다.</td>
   <td>처리된 문서</td>
   <td> generatePDFOutputBatch API는 양식 템플릿을 레코드와 결합하고 PDF을 생성합니다. 레코드 일괄 처리를 처리할 때 Transaction Reporting Service에서는 각 레코드를 별도의 PDF 렌디션으로 계산합니다. <br> 다음을 사용할 수 있습니다. <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles</a> 여러 표현물을 단일 PDF 파일로 결합하는 플래그입니다. 플래그의 상태에 관계없이 이 서비스는 각 레코드를 별도의 PDF 렌디션으로 계산합니다. </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutput-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PrintedOutputOptions-" target="_blank">generatePrintedOutput</a></td>
   <td>XDP 및 PDF 문서를 PS(PostScript), PCL(Printer Command Language) 및 ZPL 파일 형식으로 변환합니다. </td>
   <td>처리된 문서</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutput-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PrintedOutputOptions-" target="_blank">generatePrintedOutput</a></td>
   <td>XDP 및 PDF 문서를 PS(PostScript), PCL(Printer Command Language) 및 ZPL 파일 형식으로 변환합니다. </td>
   <td>처리된 문서</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutputBatch-java.util.Map-java.util.Map-com.adobe.fd.output.api.PrintedOutputOptions-com.adobe.fd.output.api.BatchOptions-" target="_blank">generatePrintedOutputBatch</a></td>
   <td>XDP 및 PDF 문서 집합을 PostScript(PS), 프린터 명령 언어(PCL) 및 ZPL 파일 형식 집합으로 변환합니다. </td>
   <td>처리된 문서</td>
   <td> generatePDFOutputBatch API는 양식 템플릿을 레코드와 결합하고 PDF을 생성합니다. 레코드 일괄 처리를 처리할 때 Transaction Reporting Service에서는 각 레코드를 별도의 PDF 렌디션으로 계산합니다. <br> 다음을 사용할 수 있습니다. <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles</a> 여러 표현물을 단일 PDF 파일로 결합하는 플래그입니다. 플래그의 상태에 관계없이 이 서비스는 각 레코드를 별도의 PDF 렌디션으로 계산합니다. </td>
  </tr>
 </tbody>
</table>

### Forms 서비스 {#forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>설명</td>
   <td>거래 보고서 범주</td>
   <td>추가 정보</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#renderPDFForm-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.PDFFormRenderOptions-" target="_blank">renderPDFForm</a></td>
   <td>XDP 템플릿에서 PDF 양식을 렌더링합니다. XP 템플릿은 Forms Designer에서 만듭니다.</td>
   <td>처리된 문서</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#exportData-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.DataFormat-" target="_blank">exportData</a></td>
   <td>PDF 양식 또는 XDP 템플릿에서 데이터 추출</td>
   <td>처리된 문서</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### PDF 서비스 변환 {#convert-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>설명</td>
   <td>거래 보고서 범주</td>
   <td>추가 정보</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toImage</a></td>
   <td>PDF 문서를 이미지 문서 목록으로 변환합니다. 지원되는 이미지 형식은 JPEG, JPEG 2K, PNG 및 TIFF입니다.</td>
   <td>처리된 문서</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toPS</a></td>
   <td>옵션 사양에 지정된 옵션을 사용하여 플랫 PDF 파일을 PostScript 형식으로 변환합니다.</td>
   <td>처리된 문서</td>
   <td> </td>
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
   <td>추가 정보</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode-com.adobe.aemfd.docmanager.Document-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-com.adobe.fd.bcf.api.CharSet-" target="_blank">decode</a></td>
   <td>Document 객체의 모든 바코드를 디코딩하고 바코드에서 검색된 데이터가 포함된 org.w3c.dom.Document 객체를 반환합니다.</td>
   <td>처리된 문서</td>
   <td> </td>
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
   <td>추가 정보</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#invoke-com.adobe.aemfd.docmanager.Document-java.util.Map-com.adobe.fd.assembler.client.AssemblerOptionSpec-">호출</a></td>
   <td>지정된 DDX 문서를 실행하고 <a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">어셈블러 결과</a> 결과 문서가 포함된 객체입니다. </td>
   <td>처리된 문서</td>
   <td>다음 작업은 트랜잭션으로 계상되지 않습니다.
    <ul>
     <li>패키지 또는 포트폴리오 만들기</li>
     <li>여러 XDP 결합 </li>
    </ul> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#invoke-com.adobe.aemfd.docmanager.Document-java.util.Map-com.adobe.fd.assembler.client.AssemblerOptionSpec-" target="_blank">호출</a></td>
   <td>지정된 DDX 문서를 실행하고 <a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">어셈블러 결과</a> 결과 문서가 포함된 객체입니다. </td>
   <td>처리된 문서</td>
   <td>PDF Generator, Forms 및 출력 서비스에서 지원하는 모든 입력 파일 형식이며 어셈블러 서비스에서는 이러한 모든 형식을 출력 파일 형식으로 지원합니다. </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#toPDFA-com.adobe.aemfd.docmanager.Document-com.adobe.fd.assembler.client.PDFAConversionOptionSpec-">toPDFA</a></td>
   <td>지정된 옵션을 사용하여 지정된 문서를 PDF/A로 변환합니다.</td>
   <td>처리된 문서</td>
   <td> </td>
  </tr>
 </tbody>
</table>

다음 작업 중 하나 이상을 수행하면 호출 API 사용이 트랜잭션으로 계산됩니다.
1. PDF 형식이 아닌 형식에서 PDF 형식으로 변환. 예를 들어 대화형 및 비대화형 통신 형식을 모두 제공하는 XDP 형식에서 PDF 형식으로 변환 및 Word에서 PDF으로 변환.
1. PDF 형식에서 PDF/A 형식으로 변환.
1. PDF 형식에서 PDF 형식이 아닌 형식으로 변환. 예제에서는 PDF 형식에서 이미지 형식으로 변환하거나 PDF 형식에서 텍스트 형식으로 변환할 수 있습니다.

>[!NOTE]
>
>* 어셈블러 서비스의 호출 API는 입력에 따라 다른 서비스의 과금 가능한 API를 내부적으로 호출할 수 있습니다. 따라서 호출 API는 없음, 단일 또는 여러 트랜잭션으로 간주할 수 있습니다. 계산되는 트랜잭션 수는 입력 및 호출된 내부 API에 따라 다릅니다.
>* 어셈블러 서비스를 사용하여 생성된 단일 PDF 문서는 없음, 단일 또는 다중 트랜잭션으로 계상될 수 있습니다. 계산되는 거래 수는 제공된 DDX 코드에 따라 다릅니다.

### PDF 유틸리티 서비스  {#pdf-utility-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>설명</td>
   <td>거래 보고서 범주</td>
   <td>추가 정보</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/pdfutility/services/PDFUtilityService.html#convertPDFtoXDP-com.adobe.aemfd.docmanager.Document-" target="_blank">convertPDFtoXDP</a></td>
   <td>PDF 문서를 XDP 파일로 변환합니다. PDF 문서를 XDP 파일로 성공적으로 변환하려면 PDF 문서에 AcroForm 사전에 XFA 스트림이 있어야 합니다.</td>
   <td>처리된 문서</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 청구 가능 데이터 캡처 API {#billable-data-capture-apis}

적응형 양식, HTML 5 Forms 및 양식 세트의 모든 제출 이벤트는 트랜잭션으로 처리됩니다. 기본적으로 PDF 양식 제출은 거래로 간주되지 않습니다. 제공된 를 사용하십시오 [트랜잭션 레코더 API](record-transaction-custom-implementation.md) PDF forms 제출을 거래로 기록하려면 다음과 같이 하십시오.

### 적응형 양식 {#adaptive-forms}

<table>
 <tbody>
  <tr>
   <td><p>사용 사례</p> </td>
   <td>설명</td>
   <td>거래 보고서 범주</td>
   <td>추가 정보</td>
  </tr>
  <tr>
   <td>적응형 양식 제출</td>
   <td>구성된 제출 액션에 적응형 양식을 제출합니다. </td>
   <td>제출된 양식</td>
   <td>
    <ul>
     <li>성공한 제출은 단일 또는 두 개의 트랜잭션을 처리합니다. 계산되는 거래 수는 실행에 사용되는 실행 작업 유형에 따라 달라집니다. 예를 들어 이메일 제출 액션을 통해 PDF을 전송하는 것은 두 가지 트랜잭션 수에 해당합니다. 양식 제출을 위한 트랜잭션과 DOR(기록 문서) 서비스를 사용하여 생성된 PDF을 위한 트랜잭션. </li>
     <li>적응형 양식(적응형 양식 세트) 내에서 적응형 양식을 사용하면 단일 트랜잭션만 계산됩니다. 적응형 양식 내에 여러 적응형 양식을 보유할 수 있습니다.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### HTML5 양식 {#html-forms}

<table>
 <tbody>
  <tr>
   <td><p>사용 사례</p> </td>
   <td>설명 </td>
   <td>거래 보고서 범주</td>
   <td>추가 정보</td>
  </tr>
  <tr>
   <td>HTML5 양식 제출</td>
   <td>HTML5 양식을 제출하여 양식에 구성된 URL을 제출합니다.</td>
   <td>제출된 양식</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 양식 집합 {#form-set}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>설명</td>
   <td>거래 보고서 범주</td>
   <td>추가 정보</td>
  </tr>
  <tr>
   <td>양식 세트 제출</td>
   <td>양식 세트를 양식 세트에 구성된 제출 URL로 제출합니다.</td>
   <td>제출된 양식</td>
   <td>
    <ul>
     <li>적응형 양식(적응형 양식 세트) 내에서 적응형 양식을 사용하면 단일 트랜잭션만 계산됩니다. 적응형 양식 내에 여러 적응형 양식을 보유할 수 있습니다.</li>
     <li>HTML5 Forms 양식의 모든 양식은 별도의 트랜잭션으로 계정을 설정합니다. </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## OSGi API에서 청구 가능한 대화형 통신 및 양식 중심의 AEM 워크플로 {#billable-interactive-communication-and-form-centric-aem-workflows-on-osgi-apis}

OSGi의 양식 중심 AEM 워크플로의 작업 및 문서 서비스 단계와 대화형 통신의 모든 렌디션을 할당하며 트랜잭션으로 계산됩니다. 작성자 인스턴스에서 대화형 통신 미리 보기 및 에이전트 UI를 사용하여 게시 인스턴스에서 미리 보기는 트랜잭션으로 간주되지 않습니다. 워크플로우 단계에서 트랜잭션을 처리하지만 워크플로우가 완료되지 않으면 트랜잭션 수가 취소되지 않습니다.

### 대화형 통신 - 웹 채널 {#interactive-communication-web-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>설명</td>
   <td>거래 보고서 범주</td>
   <td>추가 정보</td>
  </tr>
  <tr>
   <td>웹 채널 렌더링</td>
   <td>대화형 통신의 웹 버전을 엽니다.</td>
   <td>렌더링된 문서</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### 대화형 통신 - 인쇄 채널 {#interactive-communication-print-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>설명</td>
   <td>거래 보고서 범주</td>
   <td>추가 정보</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/channels/print/api/model/PrintChannel.html" target="_blank">렌더링</a> (PDF으로 변환)</td>
   <td>대화형 통신의 PDF 버전을 생성합니다.</td>
   <td>렌더링된 문서</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### OSGi의 양식 중심의 AEM 워크플로  {#form-centric-aem-workflows-on-osgi}

<table>
 <tbody>
  <tr>
   <td><p>사용 사례</p> </td>
   <td>거래 보고서 범주</td>
   <td>추가 정보</td>
  </tr>
  <tr>
   <td>작업 할당 단계 제출</td>
   <td>제출된 양식</td>
   <td>
    <div>
    </div> </td>
  </tr>
  <tr>
   <td>워크플로우 응용 프로그램 시작 지점 제출 </td>
   <td>제출된 양식</td>
   <td> </td>
  </tr>
  <tr>
   <td>에이전트 UI에서 워크플로우로 대화형 통신(인쇄 채널) 제출</td>
   <td>렌더링된 문서</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 사용자 지정 코드에 대한 트랜잭션으로 청구 가능 API 기록 {#recording-billable-apis-as-transactions-for-custom-code}

PDF 양식 제출, 에이전트 UI를 사용하여 대화형 통신 미리 보기, 비표준 양식 제출 및 사용자 지정 구현과 같은 작업은 트랜잭션으로 계산되지 않습니다. AEM Forms은 트랜잭션과 같은 작업을 기록하는 API를 제공합니다. 사용자 지정 구현에서 API를 호출하여 [거래 기록](/help/forms/using/record-transaction-custom-implementation.md).

## 관련 문서 {#related-articles}

* [거래 보고서 개요](../../forms/using/transaction-reports-overview.md)
* [거래 보고서 보기 및 이해](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [사용자 지정 구현에 대한 트랜잭션 기록](/help/forms/using/record-transaction-custom-implementation.md)
