---
title: AEM Forms 작업 공간 사용자 인터페이스의 로케일 변경
description: 텍스트, 축소된 카테고리, 큐 및 프로세스, 인터페이스의 날짜 선택기를 현지화하기 위해 AEM Forms 작업 영역을 수정하는 방법입니다.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 9a069486-02a8-4058-adfb-4e0e49d8c0cf
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 0%

---

# AEM Forms 작업 공간 사용자 인터페이스의 로케일 변경{#changing-the-locale-of-aem-forms-workspace-user-interface}

AEM Forms workspace는 영어, 프랑스어, 독일어 및 일본어 언어를 즉시 지원합니다. 또한 AEM Forms 작업 공간 사용자 인터페이스를 다른 언어로 현지화하는 기능도 제공합니다.

AEM Forms 작업 공간 사용자 인터페이스를 선택한 언어로 현지화하려면 다음 작업을 수행하십시오.

* AEM Forms 작업 영역의 텍스트를 현지화합니다.
* 축소된 범주, 큐 및 프로세스를 현지화합니다.
* 현지화 날짜 선택기

위의 단계를 수행하기 전에 다음 단계를 따르는지 확인하십시오. [AEM Forms 작업 공간 사용자 정의에 대한 일반 단계](../../forms/using/generic-steps-html-workspace-customization.md).

>[!NOTE]
>
>AEM Forms 작업 영역의 로그인 화면의 언어를 변경하려면 다음을 참조하십시오. [로그인 화면 만들기](../../forms/using/creating-new-login-screen.md).

## 텍스트 현지화 {#localizing-text}

언어에 대한 지원을 추가할 수 있도록 다음 단계를 수행하십시오 *신규* 및 브라우저 로케일 코드 *nw*.

1. CRXDE Lite에 로그인합니다.
CRXDE Lite의 기본 URL은 `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. 위치로 이동 `apps/ws/locales` 및 폴더 만들기 `nw.`
1. 파일 복사 `translation.json`(위치: 부터) `/apps/ws/locales/en-US` 대상 위치 `/apps/ws/locales/nw` .
1. 다음으로 이동 `/apps/ws/locales/nw` 및 열기 `translation.json` 편집할 수 있습니다. translation.json 파일을 로케일별로 변경합니다.

   다음 예에는 AEM Forms 작업 영역의 영어 및 프랑스어 로케일에 대한 translation.json 파일이 포함되어 있습니다.

   ![translation_json_in_en](assets/translation_json_in_en.png) ![translation_json_in_fr](assets/translation_json_in_fr.png)

## 축소된 범주, 큐 및 프로세스 현지화 {#localizing-collapsed-categories-queues-and-processes}

AEM Forms workspace는 이미지를 사용하여 카테고리, 큐 및 프로세스의 헤더를 표시합니다. 이러한 헤더를 현지화하려면 개발 패키지가 필요합니다. 개발 패키지 만들기에 대한 자세한 내용은 [AEM Forms 작업 공간 코드를 빌드하고 있습니다.](introduction-customizing-html-workspace.md#building-html-workspace-code)

다음 단계에서는 현지화된 새 이미지 파일이 *Categories_nw.png*, *Queue_nw.png*, 및 *Processes_nw.png*. 이미지의 권장 너비는 19픽셀로 설정해야 합니다.

>[!NOTE]
>
>브라우저의 브라우저 언어 로케일 코드를 찾으려면 다음을 수행하십시오. `https://'[server]:[port]'/lc/libs/ws/Locale.html`를 엽니다.

![collapsing_panels_image](assets/collapsing_panels_image.png)

이미지를 현지화하려면 다음 단계를 수행하십시오.

1. WebDAV 클라이언트를 사용하여 이미지 파일을 */apps/ws/images* 폴더를 삭제합니다.
1. 다음으로 이동 */apps/ws/css*. 열기 *newStyle.css* 을(를) 편집하고 다음 항목을 추가합니다.

   ```css
   #categoryListBar .content.nw {
        background: #3e3e3e url(../images/Categories_nw.png) no-repeat 10px 10px;
    }
   
   #filterListBar .content.nw {
       background: #3e3e3e url(../images/Queues_nw.png) no-repeat 10px 10px;
   }
   
   #processNameListBar .content.nw {
       background: #3e3e3e url(../images/Processes_nw.png) no-repeat 10px 10px;
   }
   ```

1. 에 나열된 모든 의미 체계 변경 수행 [작업 영역 사용자 지정](../../forms/using/introduction-customizing-html-workspace.md) 기사.
1. 다음 위치로 이동 *js/runtime/utility* 폴더를 만들고 *usersession.js* 편집할 파일입니다.
1. 원래 코드 블록에 나열된 코드를 찾아 조건을 추가합니다 *lang!==nw&#39; 사용* if 문:

   ```javascript
   // Orignal code
   setLocale = function () {
           var lang = $.trim(i18n.lng());
           if (lang === null || lang === '' || (lang !== 'fr-FR' && lang !== 'de-DE' && lang !== 'ja-JP')) {
               window.lcWorkspace.locale = 'en-US';
           } else {
               window.lcWorkspace.locale = lang;
           }
       }
   ```

   ```javascript
   //new code
    setLocale = function () {
           var lang = $.trim(i18n.lng());
           if (lang === null || lang === '' || (lang !== 'fr-FR' && lang !== 'de-DE' && lang !== 'ja-JP' && lang !== 'nw')) {
               window.lcWorkspace.locale = 'en-US';
           } else {
               window.lcWorkspace.locale = lang;
           }
       }
   ```

## 날짜 선택기 현지화 {#localizing-date-picker}

를 현지화하려면 개발 패키지가 필요합니다. *datepicker* API. 개발 패키지 만들기에 대한 자세한 내용은 [AEM Forms 작업 공간 코드 작성](introduction-customizing-html-workspace.md#building-html-workspace-code).

1. 다운로드 및 추출 [jQuery UI 패키지](https://jqueryui.com/download/all/), 다음으로 이동 *&lt;extracted jquery=&quot;&quot; ui=&quot;&quot; package=&quot;&quot;>*\jquery-ui-1.10.2.zip\jquery-ui-1.10.2\ui\i18n.
1. 로케일 코드 nw에 대한 jquery.ui.datepicker-nw.js 파일을 apps/ws/js/libs/jqueryui에 복사하고 로케일별로 파일을 변경합니다.
1. 다음으로 이동 `apps/ws/js` 및 열기 `jquery.ui.datepicker-nw.js` 편집할 파일입니다.
1. main.js 파일에서 `jquery.ui.datepicker-nw.js.` 에 대한 별칭을 만드는 코드 `jquery.ui.datepicker-nw.js` 파일:

   ```javascript
   jqueryuidatepickernw : pathprefix + 'libs/jqueryui/jquery.ui.datepicker-nw'
   ```

1. 별칭 사용 `jqueryuidatepickernw` 다음을 포함 `jquery.ui.datepicker-nw.js` datepicker를 사용하는 모든 파일의 파일입니다. 날짜 선택기는 다음 파일에 사용됩니다.

   * `js/runtime/views/outofoffice.js`
   * `js/runtime/views/searchtemplatedetails.js`

   아래 샘플 코드는 jquery.ui.datepicker-nw.js의 항목을 추가하는 방법을 보여 줍니다.

   ```json
   //Original Code
   define([
       'jquery',
       'underscore',
       'backbone',
       'jqueryui',
       'jqueryuidatepickerja',
       'jqueryuidatepickerde',
       'jqueryuidatepickerfr',
       'slimscroll',
       'usersearchview',
       'logmanagerutil',
       'loggerutil'
   ], function ($, _, Backbone, jQueryUI, jQueryUIDatePickerJA, jQueryUIDatePickerDE, jQueryUIDatePickerFR, slimScroll, UserSearch, LogManager, Logger) {
   ```

   ```json
   // Code with Date Picker alias for new language
   define([
       'jquery',
       'underscore',
       'backbone',
       'jqueryui',
       'jqueryuidatepickerja',
       'jqueryuidatepickerde',
       'jqueryuidatepickerfr',
       'jqueryuidatepickernw', // Date Picker alias
       'slimscroll',
       'usersearchview',
       'logmanagerutil',
       'loggerutil'
   ], function ($, _, Backbone, jQueryUI, jQueryUIDatePickerJA, jQueryUIDatePickerDE, jQueryUIDatePickerFR, jQueryUIDatePickerNW, slimScroll, UserSearch, LogManager, Logger) {
   ```

1. datepicker API를 사용하는 모든 파일에서 기본 datepicker API 설정을 변경합니다. datepicker API는 다음 파일에서 사용됩니다.

   * apps\ws\js\runtime\views\searchtemplatedetails.js
   * apps\ws\js\runtime\views\outofoffice.js

   다음 코드를 변경하여 새 로케일을 추가합니다.

   ```javascript
   if (locale === 'ja-JP') {
      $.datepicker.setDefaults($.datepicker.regional.ja);
   } else if (locale === 'de-DE') {
      $.datepicker.setDefaults($.datepicker.regional.de);
   } else if (locale === 'fr-FR') {
      $.datepicker.setDefaults($.datepicker.regional.fr);
   } else {
      $.datepicker.setDefaults($.datepicker.regional['']);
   }
   ```

   ```javascript
   if (locale === 'ja-JP') {
       $.datepicker.setDefaults($.datepicker.regional.ja);
   } else if (locale === 'de-DE') {
       $.datepicker.setDefaults($.datepicker.regional.de);
   } else if (locale === 'fr-FR') {
       $.datepicker.setDefaults($.datepicker.regional.fr);
   } else if (locale === 'nw') {
       $.datepicker.setDefaults($.datepicker.regional.nw);
   } else {
       $.datepicker.setDefaults($.datepicker.regional['']);
   }
   ```
