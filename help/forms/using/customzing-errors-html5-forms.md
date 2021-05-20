---
title: HTML5 양식에 대한 오류 메시지 사용자 지정
seo-title: HTML5 양식에 대한 오류 메시지 사용자 지정
description: 위치 및 모양을 변경하는 방법을 비롯하여 HTML5 양식의 오류 메시지 표시를 사용자 지정하는 방법을 알아봅니다.
seo-description: 위치 및 모양을 변경하는 방법을 비롯하여 HTML5 양식의 오류 메시지 표시를 사용자 지정하는 방법을 알아봅니다.
uuid: 6f48b64e-858f-4323-ad50-88e25f3c2e3d
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 44e49789-9075-41b3-bce8-03e8efce2d5a
feature: Mobile Forms
exl-id: c4ae53a3-8de1-4985-a73e-829749de9814
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 0%

---

# HTML5 양식에 대한 오류 메시지 사용자 지정 {#customizing-error-messages-for-html-forms}

HTML5 양식에서 즉시 오류 메시지와 경고에는 고정된 위치와 모양(글꼴과 색상)이 있고, 선택한 필드에 대해서만 오류가 표시되고 하나의 오류만 표시됩니다.

이 문서에서는 HTML5 양식 오류 메시지를

* 오류 메시지의 모양과 위치를 변경합니다. 필드의 위쪽, 아래쪽 및 오른쪽에 표시되는 오류를 만들 수 있습니다.
* 지정된 시간에 여러 필드에 대한 오류 메시지를 표시합니다.
* 선택한 필드에 관계없이 오류를 표시합니다.

## 오류 메시지 사용자 지정  {#customizing-error-messages-nbsp}

오류 메시지를 사용자 지정하기 전에 첨부된 패키지(CustomErrorManager-1.0-SNAPSHOT.zip)를 다운로드하여 추출합니다.

패키지를 추출한 후 CustomErrorManager-1.0-SNAPSHOT 폴더를 엽니다. jcr_root 및 META-INF 폴더가 포함되어 있습니다. 이러한 폴더에는 오류 메시지를 사용자 지정하는 데 필요한 CSS 및 .JS 파일이 포함되어 있습니다.

[파일 가져오기](assets/customerrormanager-1.0-snapshot.zip)

### 오류 메시지 위치 사용자 지정  {#customizing-the-position-of-error-messages-nbsp}

오류 메시지의 위치를 사용자 지정하려면 각 오류 및 경고 필드에 &lt;div> 태그를 추가하고, 왼쪽 또는 오른쪽에 &lt;div> 태그를 지정한 다음, &lt;div> 태그에 css 스타일을 적용합니다. 자세한 단계는 아래 나열된 절차를 참조하십시오.

1. `CustomErrorManager-1.0-SNAPSHOT`폴더로 이동하고 `etc\clientlibs\mf-custom-error-manager\CustomErrorManager\javascript` 폴더를 엽니다.
1. 편집할 `customErrorManager.js` 파일을 엽니다. 파일의 `markError` 함수는 다음 매개 변수를 허용합니다.

   |  |  |
   |---|---|
   | jqWidget | jqWidget 은 위젯의 핸들입니다. |
   | msg | 오류 메시지 포함 |
   | 유형 | 오류 또는 경고 표시 |

1. 즉시 구현하면 필드 오른쪽에 오류 메시지가 표시됩니다. 오류 메시지가 맨 위에 표시되도록 하려면 다음 코드를 사용하십시오.

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
1. `CustomErrorManager-1.0-SNAPSHOT` 폴더로 이동하고 jcr_root 및 META-INF 폴더의 아카이브를 만듭니다. 아카이브 이름을 CustomErrorManager-1.0-SNAPSHOT.zip으로 변경합니다.
1. 패키지 관리자를 사용하여 패키지를 업로드하고 설치합니다.

## 여러 필드에 대한 오류 메시지 표시  {#display-error-messages-for-multiple-fields-nbsp}

첨부된 패키지를 사용하여 모든 필드에 대한 오류 메시지를 동시에 표시합니다. 단일 오류 메시지를 표시하려면 기본 프로필을 사용하십시오.

### 오류 메시지 모양을 사용자 지정합니다.  {#customizing-the-appearance-of-error-messages-nbsp}

1. etc\clientlibs\mf-custom-error-manager\CustomErrorManager\css folder 로 이동합니다.

1. 편집할 sample.css 파일을 엽니다.css 파일에는 #customError, #customWarning라는 2개의 id가 포함되어 있습니다. 이러한 ID를 사용하여 색상, 글꼴 크기 등의 다양한 속성을 변경할 수 있습니다.

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
1. CustomErrorManager-1.0-SNAPSHOT 폴더로 이동하고 jcr_root 및 META-INF 폴더의 아카이브를 만듭니다. 아카이브 이름을 CustomErrorManager-1.0-SNAPSHOT.zip으로 변경합니다.
1. 패키지 관리자를 사용하여 패키지를 업로드하고 설치합니다.

## 새 프로필로 양식을 렌더링합니다.  {#render-the-form-with-the-new-profile-nbsp}

곧바로 사용할 수 있는 html5 양식에서는 기본 프로필을 사용합니다.https://&lt;server>/content/xfaforms/profiles/default.html?contentRoot=&lt;xdp 위치>&amp;template=&lt;xdp 이름>

사용자 지정 오류 메시지가 있는 양식을 보려면 오류 프로필로 양식을 렌더링하십시오.https://&lt;server>/content/xfaforms/profiles/error.html?contentRoot=&lt;xdp 위치>&amp;template=&lt;xdp 이름>

>[!NOTE]
>
>첨부된 패키지는 오류 프로필을 설치합니다.
