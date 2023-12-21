---
title: HTML5 양식에 대한 오류 메시지 사용자 지정
description: 위치 및 모양을 변경하는 방법을 포함하여 HTML 5 양식에 대한 오류 메시지 표시를 사용자 지정하는 방법에 대해 알아봅니다.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
feature: HTML5 Forms
exl-id: c4ae53a3-8de1-4985-a73e-829749de9814
source-git-commit: 524475c8f9dbd02bae30ecd558a376505fbe0aed
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 3%

---

# HTML5 양식에 대한 오류 메시지 사용자 지정 {#customizing-error-messages-for-html-forms}

HTML5 양식에서는 기본적으로 오류 메시지 및 경고의 위치와 모양(글꼴과 색상)이 고정되어 있으며 선택한 필드에 대해서만 오류가 표시되고 하나의 오류만 표시됩니다.

이 문서에서는 다음을 수행할 수 있도록 HTML 5 양식 오류 메시지를 사용자 지정하는 단계를 제공합니다.

* 오류 메시지의 모양과 위치를 변경합니다. 필드의 위쪽, 아래쪽 및 오른쪽에 표시되는 오류를 만들 수 있습니다.
* 특정 시점에 여러 필드에 대한 오류 메시지를 표시합니다.
* 필드 선택 여부와 관계없이 오류를 표시합니다.

## 오류 메시지 사용자 지정  {#customizing-error-messages-nbsp}

오류 메시지를 사용자 지정하기 전에 첨부된 패키지(CustomErrorManager-1.0-SNAPSHOT.zip)를 다운로드하여 추출하십시오.

패키지를 추출한 후 CustomErrorManager-1.0-SNAPSHOT 폴더를 엽니다. 여기에는 jcr_root 및 META-INF 폴더가 포함되어 있습니다. 이러한 폴더에는 오류 메시지를 사용자 지정하는 데 필요한 CSS 및 .JS 파일이 포함되어 있습니다.

[파일 가져오기](assets/customerrormanager-1.0-snapshot.zip)

### 오류 메시지 위치 사용자 정의  {#customizing-the-position-of-error-messages-nbsp}

오류 메시지의 위치를 사용자 지정하려면 &lt;div> 각 오류 및 경고 필드에 태그를 지정하고 &lt;div> 왼쪽 또는 오른쪽에 태그를 지정하고 &lt;div> 태그에 가깝게 배치하십시오. 자세한 단계는 아래 절차를 참조하십시오.

1. 다음 위치로 이동 `CustomErrorManager-1.0-SNAPSHOT`폴더를 만들고 `etc\clientlibs\mf-custom-error-manager\CustomErrorManager\javascript` 폴더를 삭제합니다.
1. 편집할 `customErrorManager.js` 페이지를 엽니다. 다음 `markError` 파일의 함수는 다음 매개 변수를 허용합니다.

   |   |  |
   |---|---|
   | jqWidget | jqWidget은 위젯에 대한 핸들입니다. |
   | msg | 오류 메시지 포함 |
   | 유형 | 오류인지 또는 경고인지를 나타냅니다. |

1. 기본 제공 구현 시 오류 메시지가 필드의 오른쪽에 나타납니다. 오류 메시지가 맨 위에 표시되도록 하려면 다음 코드를 사용하십시오.

   ```javascript
   markError: function (jqWidget, msg, type) {
               var element = jqWidget.element,                                //Gives the div containing widget
                   pos = $(element).offset(),                          //Calculates the position of the div in the view port
                                                                   msgHeight = xfalib.view.util.TextMetrics.measureExtent(msg).height + 5;  //Calculating the height of the Error Message
                   styles = {};
                   styles.left = pos.left + "px";         // Assign the desired left position using pos.left. Here it is calculated for exact left of the field
                   styles.top = pos.top - msgHeight + "px";  // Assign the desired top position using pos.top. Here it is calculated for top of the field
               if (type != "warning") {
                   if(!jqWidget.errorDiv){
                                                                                   //Adding the warning div if it is not present already
                       jqWidget.errorDiv=$("<div id='customError'></div>").appendTo('body');
                   }
                   jqWidget.$css(jqWidget.errorDiv.get(0), styles); // Applying the styles to the warning div
                   jqWidget.errorDiv.text(msg).show();                     //Showing the warning message
               } else {
                   if(!jqWidget.errorDiv){
                                                                                   //Adding the error div if it is not present already
                       jqWidget.errorDiv=$("<div id='customWarning'></div>").appendTo('body');
                   }
                   jqWidget.$css(jqWidget.errorDiv.get(0), styles); // Applying the styles to the error div
                   jqWidget.errorDiv.text(msg).show();                     //Showing the warning message
               }
   
           },
   ```

1. 파일을 저장하고 닫습니다.
1. 다음 위치로 이동 `CustomErrorManager-1.0-SNAPSHOT` 폴더를 만들고 jcr_root 및 META-INF 폴더의 아카이브를 만듭니다. 아카이브 이름을 CustomErrorManager-1.0-SNAPSHOT.zip으로 바꿉니다.
1. 패키지 관리자를 사용하여 패키지를 업로드하고 설치합니다.

## 여러 필드에 대한 오류 메시지 표시  {#display-error-messages-for-multiple-fields-nbsp}

첨부된 패키지를 사용하여 모든 필드에 대한 오류 메시지를 동시에 표시합니다. 단일 오류 메시지를 표시하려면 기본 프로파일을 사용합니다.

### 오류 메시지의 모양 사용자 지정.  {#customizing-the-appearance-of-error-messages-nbsp}

1. etc\clientlibs\mf-custom-error-manager\CustomErrorManager\css 폴더로 이동합니다.

1. 편집할 sample.css 파일을 엽니다. css 파일에는 2개의 ID(#customError, #customWarning)가 포함되어 있습니다. 이러한 ID를 사용하여 색상 및 글꼴 크기와 같은 다양한 속성을 변경할 수 있습니다.

   다음 코드를 사용하여 오류/경고 메시지의 글꼴 크기와 색상을 변경합니다.

   ```css
   #customError {
   color: #0000FF; // it changes the color of Error Message
   display:none;
   position:absolute;
   opacity:0.85;
   font-size: 24px;  // it changes the font size of Error Message
   z-index:5;
   }
   
   #customWarning {
   color: #00FF00;  // it changes the color of Warning Message
   display:none;
   position:absolute;
   opacity:0.85;
   font-size: 18px;   // it changes the font size of Warning Message
   z-index:5;
   }
   
   Save the changes.
   ```

1. 파일을 저장하고 닫습니다.
1. CustomErrorManager-1.0-SNAPSHOT 폴더로 이동하고 jcr_root 및 META-INF 폴더의 아카이브를 만듭니다. 아카이브 이름을 CustomErrorManager-1.0-SNAPSHOT.zip으로 바꿉니다.
1. 패키지 관리자를 사용하여 패키지를 업로드하고 설치합니다.

## 새 프로필로 양식을 렌더링합니다.  {#render-the-form-with-the-new-profile-nbsp}

기본적으로 html5 양식은 기본 프로필을 사용합니다. `https://&lt;server&gt;/content/xfaforms/profiles/default.html?contentRoot=&lt;xdp location&gt;&template=&lt;name of the xdp&gt;`

사용자 지정 오류 메시지가 있는 양식을 보려면 오류 프로필이 있는 양식을 렌더링합니다. `https://&lt;server&gt;/content/xfaforms/profiles/error.html?contentRoot=&lt;xdp location&gt;&template=&lt;name of the xdp&gt;`

>[!NOTE]
>
>첨부된 패키지는 오류 프로필을 설치합니다.
