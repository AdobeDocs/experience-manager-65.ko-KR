---
title: 자산 목록 보기에 사용자 지정 작업 추가
seo-title: 자산 목록 보기에 사용자 지정 작업 추가
description: 이 문서에서는 자산 목록 보기에 사용자 지정 작업을 추가하는 방법을 설명합니다
seo-description: 이 문서에서는 자산 목록 보기에 사용자 지정 작업을 추가하는 방법을 설명합니다
uuid: 45f25cfb-f08f-42c6-99c5-01900dd8cdee
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 6378ae30-a351-49f7-8e9a-f0bd4287b9d3
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1381'
ht-degree: 2%

---


# 자산 목록 보기에 사용자 지정 작업 추가{#add-custom-action-to-the-asset-listing-view}

## 개요 {#overview}

통신 관리 솔루션을 사용하면 사용자 지정 작업을 자산 관리 사용자 인터페이스에 추가할 수 있습니다.

다음에 대한 자산 목록 보기에 사용자 지정 작업을 추가할 수 있습니다.

* 하나 이상의 자산 유형 또는 문자
* 단일, 여러 자산/문자 선택 시 또는 선택 없이 실행(작업/명령이 활성)

이 사용자 지정은 &quot;Download Flat PDF&quot; 명령을 Assets Listing for Letters 보기에 추가하는 시나리오로 증명됩니다. 이 사용자 정의 시나리오를 사용하면 사용자가 선택한 단일 서신의 일반 PDF를 다운로드할 수 있습니다.

### 전제 조건 {#prerequisites}

다음 시나리오 또는 유사한 시나리오를 완료하려면 다음 사항에 대한 지식이 필요합니다.

* CRX
* JavaScript
* Java

## 시나리오: 편지 목록 사용자 인터페이스에 명령을 추가하여 일반 PDF 버전의 문자를 다운로드합니다 {#addcommandtoletters}

아래 단계에서는 &quot;편지지 자산 목록 보기&quot;에 &quot;일반 PDF 다운로드&quot; 명령을 추가하고 사용자가 선택한 편지의 일반 PDF를 다운로드할 수 있도록 합니다. 이러한 단계를 적절한 코드 및 매개 변수와 함께 사용하여 데이터 사전이나 텍스트 등 다른 자산에 대해 다른 기능을 추가할 수 있습니다.

사용자가 일반 PDF를 다운로드할 수 있도록 통신 관리를 사용자 정의하려면 다음 단계를 완료하십시오.

1. 관리자로 `https://'[server]:[port]'/[ContextPath]/crx/de` 이동합니다.

1. 앱 폴더에서 다음 단계를 사용하여 선택 폴더에 있는 항목 폴더와 유사한 경로/구조가 있는 항목이라는 폴더를 만듭니다.

   1. 다음 경로에서 **항목** 폴더를 마우스 오른쪽 단추로 클릭하고 **Overlay Node를 선택합니다**.

      `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/body/content/header/items/selection/items`

      >[!NOTE]
      >
      >이 경로는 하나 이상의 자산/문자 중 하나를 선택하여 작동하는 동작을 만드는 특정 경로입니다. 선택 없이 작동하는 작업을 만들려면 다음 경로에 대해 오버레이 노드를 만들고 이에 따라 나머지 단계를 완료해야 합니다.
      >
      >
      >`/libs/fd/cm/ma/gui/content/cmassets/jcr:content/body/content/header/items/default/items`

      ![노드 만들기](assets/1_itemscreatenode.png)

   1. [오버레이 노드] 대화 상자에 다음 값이 있는지 확인합니다.

      **경로:** /libs/fd/cm/ma/gui/content/cmasets/jcr:content/body/content/header/items/selection/items

      **위치:** /apps/

      **일치 노드 유형:** 선택됨

      ![오버레이 노드](assets/2_createnodedownloadflatpdf.png)

   1. **확인**&#x200B;을 클릭합니다. 앱 폴더에 폴더 구조가 만들어집니다.

      모두 **저장을 클릭합니다**.

1. 새로 만든 항목 폴더 아래에서 특정 자산의 사용자 지정 단추/작업에 대한 노드를 추가합니다(예: downloadFlatPDF):

   1. 항목 **폴더를 마우스 오른쪽 단추로 클릭하고** 만들기 **> 노드** 만들기 **를**&#x200B;선택합니다.

   1. 노드 만들기 대화 상자에 다음 값이 있는지 확인하고 **확인을 클릭합니다**.

      **이름:** downloadFlatPDF(또는 이 속성에 지정할 이름)

      **유형:** nt:unstructured

   1. 새로 만든 노드를 클릭합니다(여기에서 downloadFlatPDF). CRX에 노드의 속성이 표시됩니다.

   1. 노드에 다음 속성을 추가하고(여기에서 downloadFlatPDF) [모두 **저장]을 클릭합니다**.

      <table>
        <tbody>
        <tr>
        <td><strong>이름</strong></td>
        <td><strong>유형</strong></td>
        <td><strong>값 및 설명</strong></td>
        </tr>
        <tr>
        <td>클래스</td>
        <td>문자열</td>
        <td>foundation-collection-action</td>
        </tr>
        <tr>
        <td>foundation-collection-action</td>
        <td>문자열</td>
        <td><p>{"target": ".cq-management-set-admin-childpages", "activeSelectionCount": "single","type": "LETTER"}<br /><br /> activeSelectionCount는 <br /> 하나 또는 여러 개의 <strong>자산을 선택하여 사용자 지정 작업을 수행할 수 있습니다</strong> .</p> <p><strong>type</strong> can be one or more (comma separate multiple entries) of following: LETTER,TEXT,LIST,CONDITION,DATADICTIONARY</p> </td>
        </tr>
        <tr>
        <td>아이콘</td>
        <td>문자열</td>
        <td>icon-download<br /> <br /> Correspondence Management가 명령/메뉴의 왼쪽에 표시하는 아이콘 사용 가능한 다양한 아이콘 및 설정에 대해서는 CoralUI <a href="https://docs.adobe.com/docs/en/aem/6-3/develop/ref/coral-ui/coralui3/Coral.Icon.html" target="_blank">아이콘 설명서를 참조하십시오</a>.<br /> </td>
        </tr>
        <tr>
        <td>jcr:primaryType</td>
        <td>이름</td>
        <td>nt:unstructured</td>
        </tr>
        <tr>
        <td>rel</td>
        <td>문자열</td>
        <td>download-flat-pdf-button</td>
        </tr>
        <tr>
        <td>sling:resourceType</td>
        <td>문자열</td>
        <td>granite/ui/components/endor/actionbar/button</td>
        </tr>
        <tr>
        <td>text</td>
        <td>문자열</td>
        <td>플랫 PDF 다운로드(또는 기타 레이블)<br /> 에셋 목록 <br /> 인터페이스에 나타나는 명령</td>
        </tr>
        <tr>
        <td>제목</td>
        <td>문자열</td>
        <td>선택한 문자(또는 다른 레이블/대체 텍스트)의<br /> 일반 PDF <br /> 다운로드 제목은 사용자가 사용자 지정 명령을 마우스로 가리키면 통신 관리에서 표시하는 대체 텍스트입니다.</td>
        </tr>
        </tbody>
       </table>

1. 앱 폴더에서 다음 단계를 사용하여 관리자 폴더에 있는 항목 폴더와 유사한 경로/구조가 있는 js라는 폴더를 만듭니다.

   1. 다음 경로에서 **js** 폴더를 마우스 오른쪽 버튼으로 클릭하고 **Overlay Node를 선택합니다**.

      `/libs/fd/cm/ma/gui/components/admin/clientlibs/admin/js`

   1. [오버레이 노드] 대화 상자에 다음 값이 있는지 확인합니다.

      **경로:** /libs/fd/cm/ma/gui/components/admin/clientlibs/admin/js

      **위치:** /apps/

      **일치 노드 유형:** 선택됨

   1. **확인**&#x200B;을 클릭합니다. 앱 폴더에 폴더 구조가 만들어집니다. 모두 **저장을 클릭합니다**.

1. js 폴더에서 다음 단계를 사용하여 단추의 작업 처리를 위한 코드와 함께 formaction.js라는 파일을 만듭니다.

   1. 다음 경로에서 **js** 폴더를 마우스 오른쪽 단추로 클릭하고 **만들기 > 파일 만들기를 선택합니다**.

      `/apps/fd/cm/ma/gui/components/admin/clientlibs/admin/js`

      파일 이름을 formaction.js로 지정합니다.

   1. 파일을 두 번 클릭하여 CRX에서 엽니다.
   1. formaction.js 파일(/apps 분기 아래)에서 다음 위치의 formaction.js 파일에서 코드를 복사합니다.

      `/libs/fd/cm/ma/gui/components/admin/clientlibs/admin/js/formaction.js`

      그런 다음 formaction.js 파일(/apps 분기 아래)의 끝에 다음 코드를 추가하고 모두 **저장을 클릭합니다**.

      ```javascript
      /* Action url for xml file to be added.*/
      var ACTION_URL = "/apps/fd/cm/ma/gui/content/commons/actionhandlers/items/letterpdfdownloader.html";
      
      /* File upload handling*/
      var fileSelectedHandler = function(e){
          if(e && e.target && e.target.value)
              $(".downloadLetterPDFBtn").removeAttr('disabled');
          else
              $(".downloadLetterPDFBtn").attr('disabled','disabled');
      }
      
      /*Handing of Download button in pop up.*/
      var downloadClickHandler = function(){
          $('#downloadLetterPDFDilaog').modal("hide");
          var element = $('.foundation-selections-item');
          var path = $(element).data("path");
          $("#fileUploadForm").attr('action', ACTION_URL + "?letterId="+path).submit();
      }
      
      /*Click handling on action button.*/
      $(document).on("click",'.download-flat-pdf-button',function(e){
          $("#uploadSamepledata").val("");
           if($('#downloadLetterPDFDilaog').length == 0){
              $(document).on("click",".downloadLetterPDFBtn",downloadClickHandler);
              $(document).on("change","#uploadSamepledata",fileSelectedHandler);
              $("body").append(downloadLetterPDFDilaog);
          }
            $('#downloadLetterPDFDilaog').modal("show");
      });
      
      /*Download popup.*/
      var downloadLetterPDFDilaog = '<div id="downloadLetterPDFDilaog" class="coral-Modal notice " role="dialog"  aria-hidden="true">'+
          '<form id="fileUploadForm" method="POST" enctype="multipart/form-data">'+
              '<div class="coral-Modal-header">'+
                  '<h2 class="coral-Modal-title coral-Heading coral-Heading--2" id="modal-header1443020790107-label" tabindex="0">Download Letter as PDF.</h2>'+
                  '<button type="button" class="coral-MinimalButton coral-Modal-closeButton" data-dismiss="modal">×</button>'+
              '</div>'+
              '<div class="coral-Modal-body" id="modal-header1443020790107-message" role="document" tabindex="0">'+
                  '<div class="coral-Modal-message">'+
                      '<p></p>'+
                  '</div>'+
                  '<div class="coral-Modal-uploader">'+
                      '<p>Select sample data for letter.</p>'+
                      '<input type="file" id="uploadSamepledata" name="file" accept=".xml" size="70px">'+
                  '</div>'+
              '</div>'+
           '</form>'+
              '<div class="coral-Modal-footer">'+
                  '<button type="button" class="coral-Button" data-dismiss="modal">Cancel</button>'+
                  '<button type="button" class="coral-Button coral-Button--primary downloadLetterPDFBtn" disabled="disabled">Download</button>'+
              '</div>'+
      '</div>';
      ```

      이 단계에서 추가하는 코드는 libs 폴더 아래의 코드를 무시하므로 이전 코드를 /apps 분기의 formaction.js 파일에 복사합니다. /libs 분기에서 /apps 분기로 코드를 복사하면 이전 기능도 작동합니다.

      위 코드는 이 절차에서 작성된 명령의 문자별 작업 처리를 위한 것입니다. 다른 자산에 대한 작업 처리를 위해 JavaScript 코드를 수정합니다.

1. 앱 폴더에서 다음 단계를 사용하여 actionhandlers 폴더에 있는 항목 폴더와 유사한 경로/구조가 있는 항목이라는 폴더를 만듭니다.

   1. 다음 경로에서 **항목** 폴더를 마우스 오른쪽 단추로 클릭하고 **Overlay Node를 선택합니다**.

      `/libs/fd/cm/ma/gui/content/commons/actionhandlers/items/`

   1. [오버레이 노드] 대화 상자에 다음 값이 있는지 확인합니다.

      **경로:** /libs/fd/cm/ma/gui/content/commons/actionhandlers/items/

      **위치:** /apps/

      **일치 노드 유형:** 선택됨

   1. **확인**&#x200B;을 클릭합니다. 앱 폴더에 폴더 구조가 만들어집니다.

   1. 모두 **저장을 클릭합니다**.

1. 새로 만든 항목 노드 아래에서 특정 자산에 사용자 지정 단추/작업에 대한 노드를 추가합니다(예: letterpddddownloader)를 사용하십시오.

   1. 항목 폴더를 마우스 오른쪽 단추로 클릭하고 **만들기 > 노드 만들기를 선택합니다**.

   1. 노드 만들기 대화 상자에 다음 값이 있는지 확인하고 **확인을 클릭합니다**.

      **이름:** letterpdfdownloader(또는 이 속성에 지정할 이름)는 고유해야 합니다. 여기에서 다른 이름을 사용하는 경우 formaction.js 파일의 ACTION_URL 변수에서 동일한 이름을 지정하십시오.)

      **유형:** nt:unstructured

   1. 새로 만든 노드를 클릭합니다(여기에서 downloadFlatPDF). CRX에 노드의 속성이 표시됩니다.

   1. 노드에 다음 속성을 추가하고(여기에서 레터프다운로더) [모두 **저장]을 클릭합니다**.

      | **이름** | **유형** | **값** |
      |---|---|---|
      | sling:resourceType | 문자열 | fd/cm/ma/gui/components/admin/clientlibs/admin |

1. 다음 위치에서 명령의 작업 처리를 위한 코드를 사용하여 POST.jsp라는 파일을 만듭니다.

   /apps/fd/cm/ma/gui/components/admin/clientlibs/admin

   1. 다음 경로에서 **관리자** 폴더를 마우스 오른쪽 단추로 클릭하고 **만들기 > 파일 만들기를 선택합니다**.

      /apps/fd/cm/ma/gui/components/admin/clientlibs/admin

      파일의 이름을 POST.jsp로 지정합니다. 파일 이름은 POST.jsp여야 합니다.

   1. POST.jsp **** 파일을 두 번 클릭하여 CRX에서 엽니다.
   1. POST.jsp 파일에 다음 코드를 추가하고 모두 **저장을 클릭합니다**.

      이 코드는 문자 렌더링 서비스에만 적용됩니다. 다른 에셋의 경우 해당 에셋의 Java 라이브러리를 이 코드에 추가합니다. AEM Forms API에 대한 자세한 내용은 [AEM Forms API를 참조하십시오](https://adobe.com/go/learn_aemforms_javadocs_63_en).

      AEM 라이브러리에 대한 자세한 내용은 AEM 구성 [요소를 참조하십시오](/help/sites-developing/components.md).

      ```xml
      /*Import libraries. Here we are downloading letter flat pdf with input xml data so we require letterRender Api. For any other Module functionality we need to first import that library. */
      <%@include file="/libs/foundation/global.jsp"%>
      <!DOCTYPE html lang="en" PUBLIC "-//W3C//DTD XHTML 1.1//EN" "https://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">
      <%@page import="com.adobe.icc.ddg.api.*"%>
      <%@page import="com.adobe.icc.dbforms.obj.*"%>
      <%@page import="com.adobe.icc.render.obj.*" %>
      <%@page import="com.adobe.icc.services.api.*" %>
      <%@page import="org.apache.sling.api.resource.*" %>
      <%@page import="java.io.File" %>
      <%@page import="java.util.*" %>
      <%@page import="com.adobe.livecycle.content.appcontext.AppContextManager"%>
      <%@page import=" com.adobe.icc.dbforms.exceptions.ICCException"%>
      <%@page import="java.io.InputStream" %>
      <%@page import="java.io.FileInputStream" %>
      <%@page import="org.apache.commons.io.IOUtils" %>
      <%@page session="false" contentType="text/html; charset=utf-8"%>
      <%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0"%>
      <%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %>
       <%@page session="false" contentType="text/html; charset=utf-8"%>
      <%
         AppContextManager.setCurrentAppContext("/content/apps/cm");
         /*Get letter id sent in js file.*/
          String letterId = request.getParameter("letterId");
          if(letterId.lastIndexOf("?") != -1)
              letterId = letterId.substring(0, letterId.indexOf("?"));
          String fileName = null;
          String letterName = null;
          InputStream inputStream = null;
          /*Get xml file data*/
          if (slingRequest.getRequestParameter("file") != null)
              inputStream = slingRequest.getRequestParameter("file").getInputStream();
          if(letterId != null){
              String xmlData = null;
              try{
                  xmlData = IOUtils.toString(inputStream, "UTF-8");
              }
              catch (Exception e) {
                  log.error("Xml data does not exists.");
              }
              /*letter Name from letter letter id.*/
              letterName = letterId.substring(letterId.lastIndexOf("/")+1);
              /*Invoking letter render services API.*/
              LetterRenderService letterRenderService = sling.getService(LetterRenderService.class);
              /*using CM renderLetter api to get pdfbytes.*/
              PDFResponseType  pdfResponseType= letterRenderService.renderLetter(letterId,xmlData,true,false,false,false);
              byte[] bytes = null;
              /*Downloading pdf bytes as pdf.*/
              if(pdfResponseType != null && pdfResponseType.getFile() != null){
                  bytes = pdfResponseType.getFile().getDocument();
                  /*set the response header to enable download*/
                  response.setContentType("application/OCTET-STREAM");
                  response.setHeader("Content-Disposition", "attachment;filename=\"" + letterName + ".pdf\"");
                  response.setHeader("Pragma", "cache");
                  response.setHeader("Cache-Control", "private");
                  out.clear();
                  response.getOutputStream().write(bytes);
              }
          }
          else{
              log.error("Letter id does not exists.");
          }
      %>
      ```

## 사용자 정의 기능을 사용하여 편지의 일반 PDF 다운로드 {#download-flat-pdf-of-a-letter-using-the-custom-functionality}

편지의 일반 PDF를 다운로드하는 사용자 정의 기능을 추가한 후 다음 단계에 따라 선택한 편지의 일반 PDF 버전을 다운로드할 수 있습니다.

1. 이동 `https://'[server]:[port]'/[ContextPath]/projects.html` 후 로그인합니다.

1. 양식 **> 문자를 선택합니다**. 통신 관리에서는 시스템에서 사용 가능한 문자를 나열합니다.
1. 선택 **을** 클릭한 다음 문자를 클릭하여 선택합니다.
1. 자세히 **** > **&lt;일반 PDF 다운로드>** (이 문서의 지침에 따라 만든 사용자 정의 기능)를 선택합니다. PDF로 문자 다운로드 대화 상자가 나타납니다.

   메뉴 항목 이름, 기능 및 대체 텍스트는 [시나리오에서 만든 사용자 정의에 따라 달라집니다. 편지 목록 사용자 인터페이스에 명령을 추가하여 일반 PDF 버전의 문자를 다운로드합니다.](#addcommandtoletters)

   ![사용자 지정 기능: 플랫 PDF 다운로드](assets/5_downloadflatpdf.png)

1. PDF로 편지 다운로드 대화 상자에서 PDF의 데이터를 채울 관련 XML을 선택합니다.

   >[!NOTE]
   >
   >편지를 평평한 PDF로 다운로드하기 전에 [보고서 작성] 옵션을 사용하여 편지의 데이터가 포함된 XML 파일을 만들 수 **있습니다** .

   ![PDF로 문자 다운로드](assets/6_downloadflatpdf.png)

   편지는 컴퓨터에 일반 PDF로 다운로드됩니다.

