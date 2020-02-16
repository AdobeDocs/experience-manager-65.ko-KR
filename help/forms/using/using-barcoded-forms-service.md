---
title: Barcoded Forms Service
seo-title: AEM Forms Barcoded Forms Service 사용
description: 'AEM Forms Barcoded Forms 서비스를 사용하여 바코드의 전자 이미지에서 데이터를 추출합니다. '
seo-description: 'AEM Forms Barcoded Forms 서비스를 사용하여 바코드의 전자 이미지에서 데이터를 추출합니다. '
uuid: b044a788-0e4a-4718-b71a-bd846933d51b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: d431c4cb-e4be-41a5-8085-42393d4d468c
docset: aem65
translation-type: tm+mt
source-git-commit: 94472fad34fe97740e4711d2cb35beb884db52ce

---


# Barcoded Forms Service{#barcoded-forms-service}

## 개요 {#overview}

Barcoded Forms 서비스는 바코드의 전자 이미지에서 데이터를 추출합니다. 이 서비스는 하나 이상의 바코드를 입력으로 포함하는 TIFF 및 PDF 파일을 수용하고 바코드 데이터를 추출합니다. 바코드 데이터는 XML, 구분된 문자열 또는 JavaScript로 만든 사용자 정의 형식을 포함하여 다양한 방법으로 형식을 지정할 수 있습니다.

Barcoded Forms 서비스는 스캔한 TIFF 또는 PDF 문서로 제공된 다음 **2D(2D)** 기호를 지원합니다.

* PDF417
* 데이터 매트릭스
* QR 코드

또한 이 서비스는 스캔한 TIFF 또는 PDF 문서로 제공되는 다음 **1차원** 기호를 지원합니다.

* 코다바
* Code128
* 코드 3/9
* EAN13
* EAN8

Barcoded Forms 서비스를 사용하여 다음 작업을 수행할 수 있습니다.

* 바코드 이미지(TIFF 또는 PDF)에서 바코드 데이터를 추출할 수 있습니다. 데이터는 구분된 텍스트로 저장됩니다.
* 구분된 텍스트 데이터를 XML(XDP 또는 XFDF)로 변환할 수 있습니다. XML 데이터는 구분 기호로 구분된 텍스트보다 구문 분석하기가 쉽습니다. 또한 XDP 또는 XFDF 형식의 데이터는 AEM Forms의 다른 서비스에 대한 입력으로 사용할 수 있습니다.

Barcoded Forms 서비스는 이미지의 각 바코드를 찾아서 디코딩하고 데이터를 추출합니다. 서비스는 XML 문서의 컨텐츠 요소에서 필요한 경우 엔티티 인코딩을 사용하여 바코드 데이터를 반환합니다. 예를 들어, 다음 스캔한 양식의 TIFF 이미지에는 두 개의 바코드가 포함되어 있습니다.

![example](assets/example.png)

Barcoded Forms 서비스는 바코드를 디코딩한 후 다음 XML 문서를 반환합니다.

```xml
<?xml version="1.0" encoding="UTF-8" ?>  
<xb:scanned_image xmlns:xb="https://decoder.barcodedforms.adobe.com/xmlbeans"     path="tiff" version="1.0"> 
    <xb:decode> 
        <xb:date>2007-05-11T15:07:49.965-04:00</xb:date>  
        <xb:host_name>myhost.adobe.com</xb:host_name>  
        <xb:status type="success"> 
            <xb:message />  
        </xb:status> 
    </xb:decode> 
    <xb:barcode id="1"> 
        <xb:header symbology="pdf417"> 
            <xb:location page_no="1"> 
                <xb:coordinates> 
                    <xb:point x="0.119526625" y="0.60945123" />  
                    <xb:point x="0.44457594" y="0.60945123" />  
                    <xb:point x="0.44457594" y="0.78445125" />  
                    <xb:point x="0.119526625" y="0.78445125" />  
                </xb:coordinates> 
            </xb:location> 
        </xb:header> 
        <xb:body> 
            <xb:content encoding="utf-8">t_SID t_FirstName t_MiddleName t_LastName t_nFirstName t_nMiddleName t_nLastName 90210 Patti Y Penne Patti P Prosciutto</xb:content>  
        </xb:body> 
    </xb:barcode> 
    <xb:barcode id="2"> 
        <xb:header symbology="pdf417"> 
            <xb:location page_no="1"> 
                <xb:coordinates> 
                    <xb:point x="0.119526625" y="0.825" />  
                    <xb:point x="0.44457594" y="0.825" />  
                    <xb:point x="0.44457594" y="0.9167683" />  
                    <xb:point x="0.119526625" y="0.9167683" />  
                </xb:coordinates> 
            </xb:location> 
         </xb:header> 
        <xb:body> 
            <xb:content encoding="utf-8">t_FormType t_FormVersion ChangeName 20061128</xb:content>  
         </xb:body> 
    </xb:barcode> 
</xb:scanned_image>
```

## 서비스 고려 사항 {#considerations}

### 바코드 양식을 사용하는 워크플로우 {#workflows-that-use-barcoded-forms}

양식 작성자는 Designer를 사용하여 인터랙티브한 바코드 양식을 만듭니다. (디자이너 [도움말을](https://www.adobe.com/go/learn_aemforms_designer_63)참조하십시오.) 사용자가 Adobe Reader 또는 Acrobat을 사용하여 바코드를 입력하면 바코드가 자동으로 업데이트되어 양식 데이터를 인코딩합니다.

Barcoded Forms 서비스는 종이에 존재하는 데이터를 전자 형식으로 변환하는 데 유용합니다. 예를 들어 바코드 양식을 작성하여 인쇄하면 인쇄된 사본을 스캔하여 Barcoded Forms 서비스에 입력으로 사용할 수 있습니다.

감시 폴더 끝점은 일반적으로 바코딩된 양식 서비스를 사용하는 응용 프로그램을 시작하는 데 사용됩니다. 예를 들어 문서 스캐너는 바코드 양식의 TIFF 또는 PDF 이미지를 감시 폴더에 저장할 수 있습니다. 감시 폴더 끝점이 디코딩을 위해 이미지를 서비스로 전달합니다.

### 인코딩 및 디코딩 형식 권장 {#recommended-encoding-and-decoding-formats}

바코드 양식 작성자는 바코드에서 데이터를 인코딩할 때 간단하고 구분된 형식(예: 탭으로 구분)을 사용하는 것이 좋습니다. 또한 캐리지 리턴을 필드 구분 기호로 사용하지 마십시오. 디자이너는 바코드를 인코딩하기 위해 JavaScript 스크립트를 자동으로 생성하는 구분된 인코딩을 제공합니다. 디코딩된 데이터에는 첫 번째 줄에 필드 이름이 있고 두 번째 줄에 값이 있으며 각 필드 사이에 탭이 있습니다.

바코드를 디코딩할 때 필드를 구분하는 데 사용되는 문자를 지정합니다. 디코딩에 지정된 문자는 바코드를 인코딩하는 데 사용한 문자와 동일해야 합니다. 예를 들어, 권장 탭 구분 형식을 사용하는 경우 XML로 추출 작업은 필드 구분 기호에 Tab의 기본값을 사용해야 합니다.

### 사용자 지정 문자 집합 {#user-specified-character-sets}

양식 작성자가 Designer를 사용하여 양식에 바코드 개체를 추가하면 문자 인코딩을 지정할 수 있습니다. 인식된 인코딩은 UTF-8, ISO-8859-1, ISO-8859-2, ISO-8859-7, Shift-JIS, KSC-5601, Big-Five, GB-2312, UTF-16입니다. 기본적으로 모든 데이터는 바코드로 UTF-8로 인코딩됩니다.

바코드를 디코딩할 때 사용할 문자 집합 인코딩을 지정할 수 있습니다. 모든 데이터가 올바르게 디코딩되도록 하려면 양식을 디자인할 때 양식 작성자가 지정한 것과 동일한 문자 집합을 지정하십시오.

### API 제한 사항 {#api-limitations}

BCF API를 사용하는 경우 다음 제한 사항을 고려하십시오.

* 동적 양식은 지원되지 않습니다.
* 인터랙티브한 양식은 병합되지 않는 한 제대로 디코딩되지 않습니다.
* 1-D 바코드는 영숫자 값만 포함해야 합니다(지원되는 경우). 특수 기호를 포함하는 1차원 바코드는 디코딩되지 않습니다.

### 기타 제한 사항 {#other-limitations}

또한 Barcoded Forms 서비스를 사용할 때는 다음 제한 사항을 고려하십시오.

* 이 서비스는 AcroForms와 Adobe Reader 또는 Acrobat을 사용하여 저장된 2D 바코드가 포함된 정적 양식을 완벽하게 지원합니다. 그러나 1D 바코드의 경우 양식을 병합하거나 스캔한 PDF 또는 TIFF 문서로 제공합니다.
* 동적 XFA 양식은 완전히 지원되지 않습니다. 1D 및 2D 바코드를 동적 양식으로 적절하게 디코딩하려면 양식을 병합하거나 스캔한 PDF 또는 TIFF 문서로 제공하십시오.

또한 서비스는 위의 제한 사항이 관찰된 경우 지원되는 기호를 사용하는 모든 바코드를 디코딩할 수 있습니다. 인터랙티브한 바코드 양식을 만드는 방법에 대한 자세한 내용은 디자이너 [도움말을 참조하십시오](https://www.adobe.com/go/learn_aemforms_designer_63).

## 서비스의 속성 구성 {#configureproperties}

AEM 콘솔의 **AEMFD Barcoded Forms** Service를 사용하여 이 서비스에 대한 속성을 구성할 수 있습니다. AEM 콘솔의 기본 URL은 `https://[host]:[port]/system/console/configMgr`입니다.

## 서비스 사용 {#using}

Barcoded Forms Service는 다음과 같은 두 가지 API를 제공합니다.

* **[디코드](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode)**:입력 PDF 문서 또는 tiff 이미지에서 사용할 수 있는 모든 바코드를 디코딩합니다. 입력 문서 또는 이미지에서 사용할 수 있는 모든 바코드에서 검색한 데이터가 들어 있는 다른 XML 문서를 반환합니다.

* **[extractToXML](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode)**:디코딩 API를 사용하여 디코딩된 데이터를 XML 데이터로 변환합니다. 이 XML 데이터는 XFA 양식과 병합할 수 있습니다. XML 문서 목록을 반환합니다. 바코드마다 하나씩 표시됩니다.

### JSP 또는 서블릿과 BCF 서비스 사용 {#using-bcf-service-with-a-jsp-or-servlets}

다음 샘플 코드는 문서의 바코드를 디코딩하고 출력 XML을 디스크에 저장합니다.

```java
<%@ page import="java.util.List,
                com.adobe.fd.bcf.api.BarcodedFormsService,
                com.adobe.fd.bcf.api.CharSet,
                com.adobe.fd.bcf.api.Delimiter,
                com.adobe.fd.bcf.api.XMLFormat,
                com.adobe.aemfd.docmanager.Document,
                javax.xml.transform.Transformer,
                javax.xml.transform.TransformerFactory,
                java.io.StringWriter,
                javax.xml.transform.stream.StreamResult,
                javax.xml.transform.dom.DOMSource,
                javax.servlet.jsp.JspWriter,
                org.apache.commons.lang.StringEscapeUtils" %><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/><%

 // Get reference to BarcodedForms OSGi service.
 // Within an OSGi bundle @Reference annotation 
 // can be used to retrieve service reference

 BarcodedFormsService bcfService = sling.getService(BarcodedFormsService.class);

 // Path to image containing barcodes in AEM repository. 
 // Replace this with path to image in your repository
 String documentPath = "/content/dam/TestImage-010.tif";

 // Create a Docmanager Document object for 
 // the tiff file containing barcode
 // Please see Docmanager Document javadoc for
 // more details
 Document inputDoc = new Document(documentPath);

 // Invoke decode operation of barcoded forms service 
 // Second parameter is set to true to decode PDF417 barcode symbology
 // Please see javadoc for details of parameters

 org.w3c.dom.Document result = bcfService.decode(inputDoc, // Input Document Object
                                                    true, 
                                                    false,  
                                                    false,
                                                    false,
                                                    false,
                                                    false,
                                                    false,
                                                    false,
                                                    CharSet.UTF_8);// use UTF-8 character encoding 

 out.println("<h2> Output Returned from decode operation </h2>");
 printDoc(result,out);

 // Invoke extractToXML to convert Carriage 
 // return / Tab delimited data to XML 

 List<org.w3c.dom.Document> listResult = bcfService.extractToXML(result, // w3c document from the output of decode operation
                                                                    Delimiter.Carriage_Return, // Lines are separated using "\r"
                                                                    Delimiter.Tab, // Fields are separated using "\t" 
                                                                    XMLFormat.XDP); // wraps generated XML in <xdp:xdp> packet

 out.println("<h2> Output returned from extractToXML </h2>");
 printDoc(listResult.get(0),out);

%><%!

 // helper function to convert w3c document to string

 String convertToString(org.w3c.dom.Document inputDoc) throws Exception {
   TransformerFactory tf = TransformerFactory.newInstance();
   Transformer tr = tf.newTransformer();
   StringWriter sw = new StringWriter();
   StreamResult sr = new StreamResult(sw);
   tr.transform(new DOMSource(inputDoc), sr);
   return sw.toString();
 }

 // helper function to render XML to response

 void printDoc(org.w3c.dom.Document inputDoc,JspWriter out) throws Exception {
   String escapedString = StringEscapeUtils.escapeHtml(convertToString(inputDoc));
   out.println(escapedString);
 }

%>
```

### AEM 워크플로우에서 BCF 서비스 사용 {#using-the-bcf-service-with-aem-workflows}

워크플로우에서 Barcoded Forms 서비스를 실행하는 것은 JSP/Servlet에서 서비스를 실행하는 것과 비슷합니다. 유일한 차이점은 JSP/Servlet에서 서비스를 실행하는 것뿐입니다. 문서 객체는 ResourceResolverHelper 객체에서 ResourceResolver 객체의 인스턴스를 자동으로 검색합니다. 이 자동 메커니즘은 워크플로우에서 코드를 호출할 때 작동하지 않습니다.

워크플로의 경우 ResourceResolver 개체의 인스턴스를 명시적으로 Document 클래스 생성자에 전달합니다. 그런 다음 Document 개체는 제공된 ResourceResolver 개체를 사용하여 보관소의 컨텐츠를 읽습니다.

다음 샘플 워크플로우 프로세스에서는 문서의 바코드를 디코딩하여 결과를 디스크에 저장합니다. 코드는 ECMAScript로 작성되며 문서는 워크플로우 페이로드로 전달됩니다.

```
/*
 * Imports 
 */
var BarcodedFormsService = Packages.com.adobe.fd.bcf.api.BarcodedFormsService;
var CharSet = Packages.com.adobe.fd.bcf.api.CharSet;

var Document = Packages.com.adobe.aemfd.docmanager.Document;
var File = Packages.java.io.File;
var FileOutputStream = Packages.java.io.FileOutputStream;
var TransformerFactory = Packages.javax.xml.transform.TransformerFactory;
var Transformer = Packages.javax.xml.transform.Transformer;
var StreamResult = Packages.javax.xml.transform.stream.StreamResult;
var DOMSource = Packages.javax.xml.transform.dom.DOMSource;

var ResourceResolverFactory = Packages.org.apache.sling.api.resource.ResourceResolverFactory;

// get reference to BarcodedFormsService
var bcfService = sling.getService(BarcodedFormsService);

/*
 * workflow payload and path to it
 */
var payload = graniteWorkItem.getWorkflowData().getPayload();
var payload_path = payload.toString();

/* Create resource resolver using current session 
 * this resource resolver needs to be passed to Document
 * object constructor when file is to be read from 
 * crx repository. 
 */

/* get ResourceResolverFactory service reference , used 
 * to construct resource resolver
 */
var resourceResolverFactory = sling.getService(ResourceResolverFactory);

var authInfo = {
    "user.jcr.session":graniteWorkflowSession.getSession()
};

var resourceResolver = resourceResolverFactory.getResourceResolver(authInfo);

// Create Document object from payload_path 
var inputDocument = new Document(payload_path, resourceResolver);

// invoke decode operation to decode barcodes in inputDocument
var decodedBarcode = bcfService.decode(inputDocument, true, false, false, false, false, false, false, false, CharSet.UTF_8);

// save decoded barcode data to disk
saveW3CDocument(decodedBarcode, "C:/temp/decoded.xml");

/*
 * Helper function to save W3C Document
 * to a file on disk
 */
function saveW3CDocument(inputDoc, filePath) {
   var tf = TransformerFactory.newInstance();
   var tr = tf.newTransformer();
   var os = new FileOutputStream(filePath);
   var sr = new StreamResult(os);
   tr.transform(new DOMSource(inputDoc), sr);
   os.close();
}
```

