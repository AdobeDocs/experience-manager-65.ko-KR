---
title: 사용자 정의 도구 모음 작업 만들기
seo-title: 사용자 정의 도구 모음 작업 만들기
description: 양식 개발자는 AEM Forms에서 적응형 양식에 대한 사용자 정의 도구 모음 동작을 만들 수 있습니다. 작성자는 사용자 정의 작업을 사용하여 최종 사용자에게 더 많은 워크플로우와 옵션을 제공할 수 있습니다.
seo-description: 양식 개발자는 AEM Forms에서 적응형 양식에 대한 사용자 정의 도구 모음 동작을 만들 수 있습니다. 작성자는 사용자 정의 작업을 사용하여 최종 사용자에게 더 많은 워크플로우와 옵션을 제공할 수 있습니다.
uuid: cd785cfb-e1bb-4158-be9b-d99e04eccc02
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 4beca23f-dbb0-4e56-8047-93e4f1775418
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---


# 사용자 정의 도구 모음 작업 만들기{#creating-a-custom-toolbar-action}

## 전제 조건 {#prerequisite}

사용자 정의 도구 모음 액션을 만들기 전에 클라이언트 측 라이브러리 [사용](/help/sites-developing/clientlibs.md) 및 CRXDE Lite를 사용한 [개발에 익숙해지십시오](/help/sites-developing/developing-with-crxde-lite.md).

## 액션이란? {#what-is-an-action-br}

적응형 양식에서는 양식 작성자가 옵션 집합을 구성할 수 있는 도구 모음을 제공합니다. 이러한 옵션은 적응형 양식의 작업으로 정의됩니다. [패널의 도구 모음]에서 [편집] 단추를 클릭하여 응용 양식에서 지원하는 작업을 설정합니다.

![기본 도구 모음 작업](assets/default_toolbar_actions.png)

기본적으로 제공되는 작업 세트 외에도, 도구 모음에서 사용자 정의 작업을 만들 수 있습니다. 예를 들어 양식을 제출하기 전에 사용자가 모든 적응형 양식 필드를 검토할 수 있도록 동작을 추가할 수 있습니다.

## 적응형 양식에서 사용자 정의 동작을 만드는 절차 {#steps}

사용자 지정 도구 모음 작업 생성을 설명하기 위해 다음 단계를 통해 최종 사용자가 채워진 양식을 제출하기 전에 모든 응용 양식 필드를 검토할 수 있는 단추를 만들 수 있습니다.

1. 적응형 양식에서 지원하는 모든 기본 작업이 `/libs/fd/af/components/actions` 폴더에 있습니다. CRXDE에서 노드를 `fileattachmentlisting` 다음으로 `/libs/fd/af/components/actions/fileattachmentlisting` 복사합니다 `/apps/customaction`.

1. 노드를 폴더에 복사한 후 노드 이름 `apps/customaction` 을 다음으로 변경하십시오 `reviewbeforesubmit`. 또한 노드의 `jcr:title` 및 `jcr:description` 속성을 변경합니다.

   이 `jcr:title` 속성에는 도구 모음 대화 상자에 표시되는 작업의 이름이 포함되어 있습니다. 이 `jcr:description` 속성에는 사용자가 포인터를 동작 위로 가져가면 표시되는 추가 정보가 포함됩니다.

   ![도구 모음 사용자 지정을 위한 노드 계층](assets/action3.png)

1. 노드에서 `cq:template` 노드를 `reviewbeforesubmit` 선택합니다. 속성 값이 `guideNodeClass` 있는지 확인하고 그에 따라 `guideButton` 속성을 `jcr:title` 변경합니다.
1. 노드에서 유형 속성을 `cq:Template` 변경합니다. 현재 예제의 경우 type 속성을 단추로 변경합니다.

   유형 값은 구성 요소의 생성된 HTML에서 CSS 클래스로 추가됩니다. 사용자는 해당 CSS 클래스를 사용하여 작업 스타일을 지정할 수 있습니다. 모바일 및 데스크톱 장치 모두에 대한 기본 스타일이 단추, 전송, 재설정 및 저장 유형 값에 대해 제공됩니다.

1. 적응형 양식 편집 도구 모음 대화 상자에서 사용자 지정 작업을 선택합니다. 패널의 도구 모음에 [검토] 단추가 표시됩니다.

   ![사용자 지정 작업은 도구 모음에서](assets/custom_action_available_in_toolbar.png) 사용할 수 ![있습니다](assets/action7.png)

1. [검토] 단추에 기능을 제공하려면 노드 내에 있는 init.jsp 파일에 일부 JavaScript 및 CSS 코드와 서버측 코드를 `reviewbeforesubmit` 추가합니다.

   다음 코드를 에 추가합니다 `init.jsp`.

   ```jsp
   <%@include file="/libs/fd/af/components/guidesglobal.jsp" %>
   <guide:initializeBean name="guideField" className="com.adobe.aemds.guide.common.GuideButton"/>
   
   <c:if test="${not isEditMode}">
           <cq:includeClientLib categories="reviewsubmitclientlibruntime" />
   </c:if>
   
   <%--- BootStrap Modal Dialog  --------------%>
   <div class="modal fade" id="reviewSubmit" tabindex="-1">
       <div class="modal-dialog">
           <div class="modal-content">
               <div class="modal-header">
                   <h3>Review the Form Fields</h3>
               </div>
               <div class="modal-body">
                   <div class="modal-list">
                       <table class="table table-bordered">
                           <tr class="name">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Name is: </label>
                               </td>
                           </tr>
                           <tr class="pan">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Pan Number is: </label>
                               </td>
                           </tr>
                           <tr class="dob">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Date Of Birth is: </label>
                               </td>
                           </tr>
                           <tr class="80cdeclaration">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Total 80C Declaration Amount is: </label>
                               </td>
                           </tr>
                           <tr class="rentpaid">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Total HRA Amount is: </label>
                               </td>
                           </tr>
                       </table>
                   </div>
               </div><!-- /.modal-body -->
               <div class="modal-footer">
                   <div class="fileAttachmentListingCloseButton col-md-2 col-xs-2 col-sm-2">
                       <button data-dismiss="modal">Close</button>
                   </div>
               </div>
           </div><!-- /.modal-content -->
       </div><!-- /.modal-dialog -->
   </div><!-- /.modal -->
   ```

   파일에 다음 코드를 `ReviewBeforeSubmit.js` 추가합니다.

   ```javascript
   /*anonymous function to handle show of review before submit view */
   $(function () {
       if($("div.reviewbeforesubmit button[id*=reviewbeforesubmit]").length > 0) {
           $("div.reviewbeforesubmit button[id*=reviewbeforesubmit]").click(function(){
               // Create the options object to be passed to the getElementProperty API
               var options = {},
                   result = [];
               options.somExpressions = [];
               options.propertyName = "value";
               guideBridge.visit(function(model){
                   if(model.name === "name" || model.name === "pan" || model.name === "dateofbirth" || model.name === "total" || model.name === "totalmonthlyrent"){
                           options.somExpressions.push(model.somExpression);
                   }
               }, this);
               result = guideBridge.getElementProperty(options);
   
               $('#reviewSubmit .reviewlabel').each(function(index, item){
                   var data = ((result.data[index] == null) ? "No Data Filled" : result.data[index]);
                   if($(this).next().hasClass("reviewlabelvalue")){
                       $(this).next().html(data);
                   } else {
                       $(this).after($("<td></td>").addClass("reviewlabelvalue col-md-6 active").html(data));
                   }
               });
               // added because in mobile devices it was causing problem of backdrop
               $("#reviewSubmit").appendTo('body');
               $("#reviewSubmit").modal("show");
           });
       }
   });
   ```

   파일에 다음 코드를 `ReviewBeforeSubmit.css` 추가합니다.

   ```css
   .modal-list .reviewlabel {
       white-space: normal;
       text-align: right;
       padding:2px;
   }
   
   .modal-list .reviewlabelvalue {
       border: #cde0ec 1px solid;
       padding:2px;
   }
   
   /* Adding icon for this action in mobile devices */
   /* This is the glyphicon provided by bootstrap eye-open */
   /* .<type> .iconButton-icon */
   .reviewbeforesubmit .iconButton-icon {
       position: relative;
       top: -8px;
       font-family: 'Glyphicons Halflings';
       font-style: normal;
   }
   
   .reviewbeforesubmit .iconButton-icon:before {
       content: "\e105"
   }
   ```

1. 사용자 지정 작업의 기능을 확인하려면 미리 보기 모드에서 응용 양식을 열고 도구 모음에서 검토를 클릭합니다.

   >[!NOTE]
   >
   >라이브러리가 `GuideBridge` 작성 모드로 로드되지 않았습니다. 따라서 이 사용자 지정 작업은 작성 모드에서 작동하지 않습니다.

   ![사용자 정의 검토 단추의 동작 데모](assets/action9.png)

## 샘플 {#samples}

다음 아카이브는 컨텐츠 패키지를 포함합니다. 이 패키지에는 사용자 지정 도구 모음 동작의 위 데모와 관련된 응용 양식이 포함됩니다.

[파일 가져오기](assets/customtoolbaractiondemo.zip)
