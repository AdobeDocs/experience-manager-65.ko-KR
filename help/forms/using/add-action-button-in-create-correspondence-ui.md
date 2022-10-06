---
title: 서신 UI에서 사용자 지정 작업/단추 추가
seo-title: Add custom action/button in Create Correspondence UI
description: 서신 UI에서 사용자 지정 작업/단추를 추가하는 방법을 알아봅니다
seo-description: Learn how to add custom action/button in Create Correspondence UI
uuid: 1b2b00bb-93ef-4bfe-9fc5-25c45e4cb4b1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 046e3314-b436-47ed-98be-43d85f576789
docset: aem65
feature: Correspondence Management
exl-id: a582ba41-83cb-46f2-9de9-3752f6a7820a
source-git-commit: ba2c753cfd041ccfcd6ba7a45648234290b99d25
workflow-type: tm+mt
source-wordcount: '1881'
ht-degree: 1%

---

# 서신 UI에서 사용자 지정 작업 단추 추가 {#add-custom-action-button-in-create-correspondence-ui}

## 개요 {#overview}

서신 관리 솔루션을 사용하여 서신 만들기 사용자 인터페이스에 사용자 지정 작업을 추가할 수 있습니다.

이 문서의 시나리오에서는 서신 사용자 만들기 인터페이스에서 단추를 만들어 편지를 이메일에 첨부된 검토 PDF으로 공유하는 방법을 설명합니다.

### 사전 요구 사항 {#prerequisites}

이 시나리오를 완료하려면 다음이 필요합니다.

* CRX 및 JavaScript 지식
* LiveCycle 서버

## 시나리오: 서신 사용자 만들기 인터페이스에서 버튼을 만들어 검토할 편지를 보냅니다 {#scenario-create-the-button-in-the-create-correspondence-user-interface-to-send-a-letter-for-review}

작업(검토를 위해 편지 보내기)이 있는 단추를 서신 사용자 만들기 인터페이스에 추가합니다.

1. 서신 사용자 인터페이스에 단추 추가
1. 단추에 작업 처리 추가
1. 작업 처리를 활성화하기 위해 LiveCycle 프로세스 추가

### 서신 사용자 인터페이스에 단추 추가 {#add-the-button-to-the-create-correspondence-user-interface}

1. 이동 `https://'[server]:[port]'/[ContextPath]/crx/de` 관리자로 로그인합니다.
1. apps 폴더에서 `defaultApp` (구성 폴더에 있음)와 유사한 경로/구조. 폴더를 만들려면 다음 단계를 수행하십시오.

   1. 마우스 오른쪽 단추를 클릭합니다. **defaultApp** 다음 경로에 있는 폴더를 선택하고 을 선택합니다. **오버레이 노드**:

      /libs/fd/cm/config/defaultApp/

      ![오버레이 노드](assets/1_defaultapp.png)

   1. 오버레이 노드 대화 상자에 다음 값이 있는지 확인합니다.

      **경로:** /libs/fd/cm/config/defaultApp/

      **오버레이 위치:** /apps/

      **일치 노드 유형:** 선택됨

      ![오버레이 노드](assets/2_defaultappoverlaynode.png)

   1. **확인**&#x200B;을 클릭합니다.
   1. 클릭 **모두 저장**.

1. /apps 분기 아래의 acmExtensionsConfig.xml 파일( /libs 분기 아래에 있음)을 복사합니다.

   1. &quot;/libs/fd/cm/config/defaultApp/acmExtensionsConfig.xml&quot;으로 이동합니다.

   1. acmExtensionsConfig.xml 파일을 마우스 오른쪽 단추로 클릭하고 를 선택합니다 **복사**.

      ![acmExtensionsConfig.xml 복사](assets/3_acmextensionsconfig_xml_copy.png)

   1. 마우스 오른쪽 단추를 클릭합니다. **defaultApp** &quot;/apps/fd/cm/config/defaultApp/&quot;의 폴더를 선택하고 **붙여넣기**.
   1. 클릭 **모두 저장**.

1. apps 폴더에서 새로 만든 acmExtentionsConfig.xml 사본을 두 번 클릭합니다. 편집할 파일이 열립니다.
1. 다음 코드를 찾습니다.

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <extensionsConfig>
       <modelExtensions>
           <modelExtension type="LetterInstance">
     <customAction name="Preview" label="loc.letterInstance.preview.label" tooltip="loc.letterInstance.preview.tooltip" styleName="previewButton"/>
               <customAction name="Submit" label="loc.letterInstance.submit.label" tooltip="loc.letterInstance.submit.tooltip" styleName="submitButton" permissionName="forms-users"/>
               <customAction name="SaveAsDraft" label="loc.letterInstance.saveAsDraft.label" tooltip="loc.letterInstance.saveAsDraft.tooltip" styleName="submitButton" permissionName="forms-users"/>
               <customAction name="Close" label="loc.letterInstance.close.label" tooltip="loc.letterInstance.close.tooltip" styleName="closeButton"/>
           </modelExtension>
       </modelExtensions>
   </extensionsConfig>
   ```

1. 편지를 전자 메일로 보내려면 LiveCycle Forms Workflow을 사용할 수 있습니다. acmExtensionsConfig.xml의 modelExtension 태그 아래에 다음과 같이 customAction 태그를 추가합니다.

   ```xml
    <customAction name="Letter Review" label="Letter Review" tooltip="Letter Review" styleName="" permissionName="forms-users" actionHandler="CM.domain.CCRCustomActionHandler">
         <serviceName>Forms Workflow -> SendLetterForReview/SendLetterForReviewProcess</serviceName>
       </customAction>
   ```

   ![customAction 태그](assets/5_acmextensionsconfig_xml.png)

   modelExtension 태그에는 작업 단추의 작업, 권한 및 모양을 구성하는 customAction 하위 태그 세트가 있습니다. 다음은 customAction 구성 태그 목록입니다.

   | **이름** | **설명** |
   |---|---|
   | 이름 | 수행할 작업의 영숫자 이름입니다. 이 태그의 값은 필수 값이며 modelExtension 태그 내에서 고유해야 하며 알파벳으로 시작해야 합니다. |
   | 레이블 | 작업 단추에 표시할 레이블입니다 |
   | 도구 설명 | 사용자가 단추를 마우스로 가리키면 표시되는 단추의 도구 설명 텍스트입니다. |
   | styleName | 작업 단추에 적용되는 사용자 지정 스타일의 이름입니다. |
   | permissionName | 사용자에게 permissionName으로 지정된 권한이 있는 경우에만 해당 작업이 표시됩니다. permissionName을 `forms-users`로 설정되면 모든 사용자가 이 옵션에 액세스할 수 있습니다. |
   | actionHandler | 사용자가 단추를 클릭할 때 호출되는 ActionHandler 클래스의 정규화된 이름입니다. |

   위의 매개 변수 외에도 customAction과 연결된 추가 구성이 있을 수 있습니다. 이러한 추가 구성은 CustomAction 개체를 통해 처리기에서 사용할 수 있습니다.

   | **이름** | **설명** |
   |---|---|
   | serviceName | customAction에 name serviceName의 하위 태그가 포함된 경우 관련 단추/링크를 클릭하면 serviceName 태그로 표시된 이름으로 프로세스가 호출됩니다. 이 프로세스의 서명이 Letter PostProcess와 동일한지 확인합니다. 서비스 이름에 &quot;Forms Workflow ->&quot; 접두사를 추가합니다. |
   | 태그 이름에 cm_ 접두어가 포함된 매개 변수 | customAction에 name cm_로 시작하는 하위 태그가 포함되어 있는 경우 이후 프로세스(Letter Post 프로세스 또는 serviceName 태그로 표시된 특수 프로세스)에서 이러한 매개 변수는 cm_ 접두어가 제거된 관련 태그 아래의 입력 XML 코드에서 사용할 수 있습니다. |
   | actionName | 클릭으로 인해 사후 프로세스가 수행될 때마다 제출된 XML에 사용자 작업의 이름이 있는 태그 아래에 이름이 지정된 특수 태그가 포함되어 있습니다. |

1. 클릭 **모두 저장**.

#### /apps 분기에 속성 파일을 사용하여 로케일 폴더를 만듭니다 {#create-a-locale-folder-with-properties-file-in-the-apps-branch}

ACMExtensionMessages.properties 파일에는 서신 작성 사용자 인터페이스의 다양한 필드의 레이블 및 도구 설명 메시지가 포함되어 있습니다. 사용자 지정된 작업/단추가 작동하려면 /apps 분기에서 이 파일의 복사본을 만듭니다.

1. 마우스 오른쪽 단추를 클릭합니다. **로케일** 다음 경로에 있는 폴더를 선택하고 을 선택합니다. **오버레이 노드**:

   /libs/fd/cm/config/defaultApp/locale

1. 오버레이 노드 대화 상자에 다음 값이 있는지 확인합니다.

   **경로:** /libs/fd/cm/config/defaultApp/locale

   **오버레이 위치:** /apps/

   **일치 노드 유형:** 선택됨

1. **확인**&#x200B;을 클릭합니다.
1. 클릭 **모두 저장**.
1. 다음 파일을 마우스 오른쪽 단추로 클릭하고 **복사**:

   `/libs/fd/cm/config/defaultApp/locale/ACMExtensionsMessages.properties`

1. 마우스 오른쪽 단추를 클릭합니다. **로케일** 다음 경로에 있는 폴더를 선택하고 을 선택합니다. **붙여넣기**:

   `/apps/fd/cm/config/defaultApp/locale/`

   ACMExtensionMessages.properties 파일이 로케일 폴더에 복사됩니다.

1. 새로 추가한 사용자 지정 작업/단추의 레이블을 현지화하려면 의 해당 로케일에 대해 ACMExtensionMessages.properties 파일을 만듭니다 `/apps/fd/cm/config/defaultApp/locale/`.

   예를 들어 이 문서에서 만든 사용자 지정 작업/단추를 현지화하기 위해 다음 항목으로 ACMExtensionMessages_fr.properties 파일을 만듭니다.

   `loc.letterInstance.letterreview.label=Revue De Lettre`

   마찬가지로 이 파일에 도구 설명 및 스타일과 같은 속성을 더 추가할 수 있습니다.

1. 클릭 **모두 저장**.

#### Adobe 자산 작성기 빌딩 블록 번들을 다시 시작합니다 {#restart-the-adobe-asset-composer-building-block-bundle}

서버측 변경을 모두 수행한 후 Adobe 자산 작성기 빌딩 블록 번들을 다시 시작합니다. 이 시나리오에서는 서버 측에 있는 acmExtensionsConfig.xml 및 ACMExtensionMessages.properties 파일이 편집되므로 Adobe Asset Composer 빌딩 블록 번들을 다시 시작해야 합니다.

>[!NOTE]
>
>브라우저 캐시를 지워야 할 수 있습니다.

1. 이동 `https://[host]:'port'/system/console/bundles`. 필요한 경우 관리자로 로그인합니다.

1. Adobe 자산 작성기 빌딩 블록 번들을 찾습니다. 번들을 다시 시작합니다. 중지 를 클릭한 다음 시작 을 클릭합니다.

   ![Adobe 자산 작성기 빌딩 블록](assets/6_assetcomposerbuildingblockbundle.png)

Adobe 자산 작성기 빌딩 블록 번들을 다시 시작하면 사용자 지정 단추가 서신 사용자 만들기 인터페이스에 표시됩니다. 서신 사용자 인터페이스에서 문자를 열어 사용자 지정 단추를 미리 볼 수 있습니다.

### 버튼에 작업 처리 추가 {#add-action-handling-to-the-button}

Create Correspondence 사용자 인터페이스는 기본적으로 다음 위치의 cm.domain.js 파일에서 ActionHandler가 구현되어 있습니다.

/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccr/js/cm.domain.js

사용자 지정 작업 처리를 위해 CRX의 /apps 분기에서 cm.domain.js 파일의 오버레이를 만듭니다.

작업/버튼을 클릭할 때 작업/버튼을 처리하면 다음과 같은 논리가 포함됩니다.

* 새로 추가된 작업을 시각적/보이지 않음으로 만들기: actionVisible() 함수를 재정의하여 수행합니다.
* 새로 추가된 작업 활성화/비활성화: actionEnabled() 함수를 재정의하여 수행합니다.
* 사용자가 버튼을 클릭할 때의 실제 작업 처리: handleAction() 함수의 구현을 재정의하여 수행됩니다.

1. 이동 `https://'[server]:[port]'/[ContextPath]/crx/de`. 필요한 경우 관리자로 로그인합니다.

1. apps 폴더에서 `js` 다음 폴더와 유사한 구조를 사용하는 CRX의 /apps 분기에서 다음을 수행합니다.

   `/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/js`

   폴더를 만들려면 다음 단계를 수행하십시오.

   1. 마우스 오른쪽 단추를 클릭합니다. **js** 다음 경로에 있는 폴더를 선택하고 을 선택합니다. **오버레이 노드**:

      `/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/js`

   1. 오버레이 노드 대화 상자에 다음 값이 있는지 확인합니다.

      **경로:** /libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/js

      **오버레이 위치:** /apps/

      **일치 노드 유형:** 선택됨

   1. **확인**&#x200B;을 클릭합니다.
   1. 클릭 **모두 저장**.

1. js 폴더에서 다음 단계를 사용하여 버튼을 처리할 수 있는 코드로 ccrcustomization.js라는 파일을 만듭니다.

   1. 마우스 오른쪽 단추를 클릭합니다. **js** 다음 경로에 있는 폴더를 선택하고 을 선택합니다. **만들기 > 파일 만들기**:

      `/apps/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/js`

      파일의 이름을 ccrcustomization.js로 지정합니다.

   1. ccrcustomization.js 파일을 두 번 클릭하여 CRX에서 엽니다.
   1. 파일에서 다음 코드를 붙여 넣고 **모두 저장**:

      ```javascript
      /* for adding and handling custom actions in Extensible Toolbar.
        * One instance of handler will be created for each action.
        * CM.domain.CCRCustomActionHandler is actionHandler class.
        */
      var CCRCustomActionHandler;
          CCRCustomActionHandler = CM.domain.CCRCustomActionHandler = new Class({
              className: 'CCRCustomActionHandler',
              extend: CCRDefaultActionHandler,
              construct : function(action,model){
              }
          });
          /**
           * Called when user user click an action
           * @param extraParams additional arguments that may be passed to handler (For future use)
           */
          CCRCustomActionHandler.prototype.handleAction = function(extraParams){
              if (this.action.name == CCRCustomActionHandler.SEND_FOR_REVIEW) {
                  var sendForReview = function(){
                      var serviceName = this.action.actionConfig["serviceName"];
                      var inputParams = {};
                      inputParams["dataXML"] = this.model.iccData.data;
                      inputParams["letterId"] = this.letterVO.id;
                      inputParams["letterName"] = this.letterVO.name;
                      inputParams["mailId"] = $('#email').val();
                      /*function to invoke the LivecyleService */
                      ServiceDelegate.callJSONService(this,"lc.icc.renderlib.serviceInvoker.json","invokeProcess",[serviceName,inputParams],this.onProcessInvokeComplete,this.onProcessInvokeFail);
                      $('#ccraction').modal("hide");
                  }
                  if($('#ccraction').length == 0){
                      /*For first click adding popup & setting letterName.*/
                      $("body").append(popUp);
                      $("input[id*='letterName']").val(this.letterVO.name);
                      $(document).on('click',"#submitLetter",$.proxy( sendForReview, this ));
                  }
                  $('#ccraction').modal("show");
              }
          };
          /**
           * Should the action be enabled in toolbar
           * @param extraParams additional arguements that may be passed to handler (For future use)
           * @return flag indicating whether the action should be enabled
           */
         CCRCustomActionHandler.prototype.actionEnabled = function(extraParams){
                  /*can be customized as per user requirement*/
                  return true;
          };
          /**
           * Should the action be visible in toolbar
           * @param extraParams additional arguments that may be passed to handler (For future use)
           * @return flag indicating whether the action should be enabled
           */
          CCRCustomActionHandler.prototype.actionVisible = function(extraParams){
              /*Check can be enabled for Non-Preview Mode.*/
              return true;
          };
          /*SuccessHandler*/
          CCRCustomActionHandler.prototype.onProcessInvokeComplete = function(response) {
              ErrorHandler.showSuccess("Letter Sent for Review");
          };
          /*FaultHandler*/
          CCRCustomActionHandler.prototype.onProcessInvokeFail = function(event) {
              ErrorHandler.showError(event.message);
          };
          CCRCustomActionHandler.SEND_FOR_REVIEW  = "Letter Review";
      /*For PopUp*/
          var popUp = '<div class="modal fade" id="ccraction" tabindex="-1" role="dialog" aria-hidden="true">'+
          '<div class="modal-dialog modal-sm">'+
              '<div class="modal-content">' +
                  '<div class="modal-header">'+
                      '<button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</code></button>'+
                      '<h4 class="modal-title"> Send Review </h4>'+
                  '</div>'+
                  '<div class="modal-body">'+
                      '<form>'+
                          '<div class="form-group">'+
                              '<label class="control-label">Email Id</label>'+
                              '<input type="text" class="form-control" id="email">'+
                          '</div>'+
                          '<div class="form-group">'+
                              '<label  class="control-label">Letter Name</label>'+
                              '<input id="letterName" type="text" class="form-control" readonly>'+
                          '</div>'+
                          '<div class="form-group">'+
                              '<input id="letterData" type="text" class="form-control hide" readonly>'+
                          '</div>'+
                      '</form>'+
                  '</div>'+
                  '<div class="modal-footer">'+
                     '<button type="button" class="btn btn-default" data-dismiss="modal"> Cancel </button>'+
                     '<button type="button" class="btn btn-primary" id="submitLetter"> Submit </button>'+
                  '</div>'+
              '</div>'+
          '</div>'+
      '</div>';
      ```

### LiveCycle 프로세스를 추가하여 작업을 활성화합니다 <span class="acrolinxCursorMarker"></code>처리 {#add-the-livecycle-process-to-enable-action-span-class-acrolinxcursormarker-span-handling}

이 시나리오에서는 첨부된 components.zip 파일의 일부인 다음 구성 요소를 활성화합니다.

* DSC 구성 요소 jar(DSCSample.jar)
* 검토 프로세스 LCA(SendLetterForReview.lca)를 위한 편지 보내기

components.zip 파일을 다운로드하고 압축 해제하여 DSCSample.jar 및 SendLetterForReview.lca 파일을 가져옵니다. 다음 절차에 지정된 대로 이 파일을 사용하십시오.
[파일 가져오기](assets/components.zip)

#### LCA 프로세스를 실행하도록 LiveCycle 서버 구성 {#configure-the-livecycle-server-to-run-the-lca-process}

>[!NOTE]
>
>이 단계는 OSGI 설정을 사용하고 있으며 구현하려는 사용자 지정 유형에 LC 통합이 필요한 경우에만 필요합니다.

LCA 프로세스는 LiveCycle 서버에서 실행되며 서버 주소와 로그인 자격 증명이 필요합니다.

1. 이동 `https://'[server]:[port]'/system/console/configMgr` 관리자로 로그인합니다.
1. Adobe LiveCycle 클라이언트 SDK 구성을 찾은 다음 **편집** (편집 아이콘) 구성 패널이 열립니다.

1. 다음 세부 정보를 입력하고 **저장**:

   * **서버 Url**: 작업 처리기 코드가 사용하는 검토 보내기 서비스의 LC 서버의 URL입니다.
   * **사용자 이름**: LC 서버의 관리자 사용자 이름
   * **암호**: 관리자 사용자 이름의 암호

   ![Adobe LiveCycle 클라이언트 SDK 구성](assets/3_clientsdkconfiguration.png)

#### LCA(LiveCycle 아카이브) 설치 {#install-livecycle-archive-lca}

이메일 서비스 프로세스를 활성화하는 필수 LiveCycle 프로세스입니다.

>[!NOTE]
>
>이 프로세스가 수행하는 작업을 보거나 유사한 프로세스를 만들려면 Workbench가 필요합니다.

1. 관리자로 로그인하여 LiveCycle® 서버 관리자 로 `https:/[lc server]/:[lc port]/adminui`.

1. 다음으로 이동 **홈 > 서비스 > 애플리케이션 및 서비스 > 애플리케이션 관리**.

1. SendLetterForReview 응용 프로그램이 이미 있는 경우 이 절차의 나머지 단계를 건너뛰고 다음 단계를 계속 진행합니다.

   ![UI의 SendLetterForReview 애플리케이션](assets/12_applicationmanagementlc.png)

1. **가져오기**&#x200B;를 클릭합니다. 

1. 클릭 **파일 선택** SendLetterForReview.lca를 선택합니다.

   ![SendLetterForReview.lca 파일을 선택합니다.](assets/14_sendletterforreview_lca.png)

1. 클릭 **미리 보기**.

1. 선택 **가져오기가 완료되면 런타임에 자산 배포**.

1. **가져오기**&#x200B;를 클릭합니다. 

#### 서비스 목록에 허용 목록에 추가하다 ServiceName 추가 {#adding-servicename-to-the-allowlist-service-list}

Experience Manager 서버에 액세스할 LiveCycle 서비스가 Experience Manager 서버에 설명되어 있습니다.

1. 관리자로 로그인하여 `https:/[host]:'port'/system/console/configMgr`.

1. 을(를) 찾아 클릭합니다 **Adobe LiveCycle 클라이언트 SDK 구성**. Adobe LiveCycle 클라이언트 SDK 구성 패널이 나타납니다.
1. 서비스 이름 목록에서 + 아이콘을 클릭하고 serviceName을 추가합니다 **SendLetterForReview/SendLetterForReviewProcess**.

1. **저장**&#x200B;을 클릭합니다.

#### 이메일 서비스 구성 {#configure-the-email-service}

이 시나리오에서 서신 관리가 이메일을 보낼 수 있도록 하려면 LiveCycle 서버에서 이메일 서비스를 구성하십시오.

1. 관리 자격 증명으로 로그인하여 LiveCycle 서버 관리자 `https:/[lc server]:[lc port]/adminui`.

1. 다음으로 이동 **홈 > 서비스 > 애플리케이션 및 서비스 > 서비스 관리**.

1. 을(를) 찾아 클릭합니다 **EmailService**.

1. in **SMTP 호스트**, 이메일 서비스를 구성합니다.

1. **저장**&#x200B;을 클릭합니다.

#### DSC 서비스 구성 {#configure-the-dsc-service}

서신 관리 API를 사용하려면 DSCSample.jar(이 문서에 components.zip의 일부로 첨부됨)를 다운로드하고 LiveCycle 서버에 업로드합니다. DSCSample.jar 파일이 LiveCycle 서버에 업로드되면 Experience Manager 서버는 DSCSample.jar 파일을 사용하여 renderLetter API에 액세스합니다.

자세한 내용은 [AEM Forms과 Adobe LiveCycle 연결](/help/forms/using/aem-livecycle-connector.md).

1. 다음 위치에 있는 DSCSample.jar의 cmsa.properties에서 Experience Manager 서버 URL을 업데이트합니다.

   DSCSample.jar\com\adobe\livecycle\cmsa.properties

1. 구성 파일에 다음 매개 변수를 제공합니다.

   * **crx.serverUrl**= https:/host:port/[컨텍스트 경로]/[AEM URL]
   * **crx.username**= Experience Manager 사용자 이름
   * **crx.password**= Experience Manager 암호
   * **crx.appRoot**=/content/apps/cm

   >[!NOTE]
   >
   >서버 측에서 변경할 때마다 LiveCycle 서버를 다시 시작합니다.

   DSCSample.jar 파일은 renderLetter API를 사용합니다. renderLetter API에 대한 자세한 내용은 [인터페이스 LetterRenderService](https://www.adobe.io/experience-manager/reference-materials/6-5/forms/javadocs/index.html?com/adobe/icc/ddg/api/LetterRenderService.html).

#### LiveCyle로 DSC 가져오기 {#import-dsc-to-livecyle}

DSCSample.jar 파일은 renderLetter API를 사용하여 DSC가 입력으로 제공하는 XML 데이터의 PDF 바이트로 편지를 렌더링합니다. renderLetter 및 기타 API에 대한 자세한 내용은 [편지 렌더링 서비스](https://www.adobe.io/experience-manager/reference-materials/6-5/forms/javadocs/index.html?com/adobe/icc/ddg/api/LetterRenderService.html).

1. Workbench를 시작하고 로그인합니다.
1. 선택 **창 > 보기 표시 > 구성 요소**. 구성 요소 보기가 Workbench ES2에 추가됩니다.

1. 마우스 오른쪽 단추 클릭 **구성 요소** 을(를) 선택합니다. **구성 요소 설치**.

1. 을(를) 선택합니다 **DSCSample.jar** 파일 브라우저를 통해 파일을 작성하고 **열기**.
1. 마우스 오른쪽 단추 클릭 **RenderWrapper** 을(를) 선택합니다. **구성 요소 시작**. 구성 요소가 시작되면 구성 요소 이름 옆에 녹색 화살표가 나타납니다.

## 검토를 위해 편지 보내기 {#send-letter-for-review}

검토를 위해 편지를 보내기 위한 작업 및 버튼을 구성한 후:

1. 브라우저 캐시를 지웁니다.

1. Create Correspondence UI에서 **편지 검토** 검토자의 이메일 ID를 지정합니다.

1. 클릭 **제출**.

![sendreview](assets/sendreview.png)

검토자는 시스템에서 편지를 PDF 첨부 파일로 받은 이메일을 수신합니다.
