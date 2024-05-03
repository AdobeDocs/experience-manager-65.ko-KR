---
title: ConvertPDF 서비스
description: Adobe Experience Manager Forms ConvertPDF 서비스를 사용하여 PDF 문서를 PostScript 또는 이미지 파일로 변환합니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
feature: Document Services
exl-id: 50c7a385-b56d-4573-932f-1f44eec948f8
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# ConvertPDF 서비스 {#convertpdf-service}

## 개요 {#overview}

PDF 변환 서비스는 PDF 문서를 PostScript 또는 이미지 파일(JPEG, JPEG 2000, PNG 및 TIFF)로 변환합니다. PDF 문서를 PostScript로 변환하면 모든 PostScript 프린터에서 무인 서버 기반 인쇄에 유용합니다. PDF 문서를 다중 페이지 TIFF 파일로 변환하는 것은 PDF 문서를 지원하지 않는 컨텐츠 관리 시스템에 문서를 보관할 때 실용적입니다.

PDF 변환 서비스를 사용하여 다음을 수행할 수 있습니다.

* PDF 문서를 PostScript로 변환합니다. PostScript로 변환할 때 변환 작업을 사용하여 소스 문서를 지정하고 PostScript 레벨 2로 변환할지 또는 3으로 변환할지 여부를 지정할 수 있습니다. PostScript 파일로 변환하는 PDF 문서는 비대화형이어야 합니다.
* PDF 문서를 JPEG, JPEG 2000, PNG 및 TIFF 이미지 형식으로 변환합니다. 이러한 이미지 형식으로 변환할 때 변환 작업을 사용하여 소스 문서와 이미지 옵션 사양을 지정할 수 있습니다. 명세서에는 영상 변환 포맷, 영상 해상도, 색 변환 등과 같은 다양한 선호도가 포함된다.

## 서비스의 속성 구성   {#properties}

다음을 사용할 수 있습니다. **AEMFD ConvertPDF 서비스** AEM 콘솔에서 이 서비스에 대한 속성을 구성합니다. AEM 콘솔의 기본 URL은 입니다. `https://[host]:'port'/system/console/configMgr`.

## 서비스 사용 {#using-the-service}

ConvertPDF 서비스는 다음 두 가지 API를 제공합니다.

* **[toPS](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toPS)**: PDF 문서를 PostScript 파일로 변환합니다.

* **[toImage](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage)**: PDF 문서를 이미지 파일로 변환합니다. 지원되는 이미지 형식은 JPEG, JPEG 2000, PNG 및 TIFF 입니다.

### JSP 또는 서블릿에서 toPS API 사용 {#using-tops-api-with-a-jsp-or-servlets}

```jsp
<%@ page import="java.util.List, java.io.File,

                com.adobe.fd.cpdf.api.ConvertPdfService,
                com.adobe.fd.cpdf.api.ToPSOptionsSpec,
                com.adobe.fd.cpdf.api.enumeration.PSLevel,

                com.adobe.aemfd.docmanager.Document" %><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/><%

 // Get reference to ConvertPdfService OSGi service.
 // Within an OSGi bundle @Reference annotation
 // can be used to retrieve service reference

 ConvertPdfService cpdfService = sling.getService(ConvertPdfService.class);

 // path to input document in AEM repository
 // replace this with path to your document
String documentPath = "/content/dam/formsanddocuments/ExpenseClaimFlat.pdf";

 // Create a Docmanager Document object for
 // the flat PDF file which needs to be converted
 // to PostScript

 Document inputPDF = new Document(documentPath);

 // options object to pass to toPS API
 ToPSOptionsSpec toPSOptions = new ToPSOptionsSpec();

 // mandatory option to pass, sets PostScript language
 toPSOptions.setPsLevel(PSLevel.LEVEL_3);

 // invoke toPS method to convert inputPDF to PostScript
 Document convertedPS = cpdfService.toPS(inputPDF, toPSOptions);

 // save converted PostScript file to disk
 convertedPS.copyToFile(new File("C:/temp/out.ps"));

%>
```

### JSP 또는 서블릿에서 toImage API 사용 {#using-toimage-api-with-a-jsp-or-servlets}

```jsp
<%@ page import="java.util.List, java.io.File,

                com.adobe.fd.cpdf.api.ConvertPdfService,
                com.adobe.fd.cpdf.api.ToImageOptionsSpec,
                com.adobe.fd.cpdf.api.enumeration.ImageConvertFormat,

                com.adobe.aemfd.docmanager.Document" %><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/><%

 // Get reference to ConvertPdfService OSGi service.
 // Within an OSGi bundle @Reference annotation
 // can be used to retrieve service reference

 ConvertPdfService cpdfService = sling.getService(ConvertPdfService.class);

 // path to input document in AEM repository
 // replace this with path to your document
 String documentPath = "/content/dam/formsanddocuments/ExpenseClaimFlat.pdf";

 // Create a Docmanager Document object for
 // the flat PDF file which needs to be converted
 // to image

 Document inputPDF = new Document(documentPath);

 // options object to pass to toImage API
 ToImageOptionsSpec toImageOptions = new ToImageOptionsSpec();

 // mandatory option to pass, image format
 toImageOptions.setImageConvertFormat(ImageConvertFormat.JPEG);

 // invoke toImage method to convert inputPDF to Image
 List<Document> convertedImages = cpdfService.toImage(inputPDF, toImageOptions);

 // save converted image files to disk
 for(int i=0;i<convertedImages.size();i++){
     Document pageImage = convertedImages.get(i);
     pageImage.copyToFile(new File("C:/temp/out_"+(i+1)+".jpeg"));
 }

%>
```

### AEM 워크플로에서 ConvertPDF 서비스 사용 {#using-convertpdf-service-with-aem-workflows}

워크플로우에서 ConvertPDF 서비스를 실행하는 것은 JSP/Servlet에서 실행하는 것과 비슷합니다.

유일한 차이점은 JSP/Servlet에서 서비스를 실행한다는 것입니다. 문서 개체는 ResourceResolverHelper 개체에서 ResourceResolver 개체의 인스턴스를 자동으로 검색합니다. 워크플로우에서 코드가 호출될 때 이 자동 메커니즘이 작동하지 않습니다. 워크플로의 경우 ResourceResolver 개체의 인스턴스를 Document 클래스 생성자에 명시적으로 전달합니다. 그런 다음 Document 개체는 제공된 ResourceResolver 개체를 사용하여 저장소의 콘텐츠를 읽습니다.

다음 샘플 워크플로 프로세스는 입력 문서를 PostScript 문서로 변환합니다. 코드는 ECMAScript에 기록되며 문서는 워크플로 페이로드로 전달됩니다.

```javascript
/*
 * Imports
 */
var ConvertPdfService = Packages.com.adobe.fd.cpdf.api.ConvertPdfService;
var ToPSOptionsSpec = Packages.com.adobe.fd.cpdf.api.ToPSOptionsSpec;
var PSLevel = Packages.com.adobe.fd.cpdf.api.enumeration.PSLevel;
var Document = Packages.com.adobe.aemfd.docmanager.Document;
var File = Packages.java.io.File;
var ResourceResolverFactory = Packages.org.apache.sling.api.resource.ResourceResolverFactory;

// get reference to ConvertPdfService
var cpdfService = sling.getService(ConvertPdfService);

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

// options object to be passed to toPS operation
var toPSOptions = new ToPSOptionsSpec();

// Set PostScript Language Three
toPSOptions.setPsLevel(PSLevel.LEVEL_3);

// invoke toPS operation to convert inputDocument to PS
var convertedPS = cpdfService.toPS(inputDocument, toPSOptions);

// save converted PostScript file to disk
convertedPS.copyToFile(new File("C:/temp/out.ps"));
```
