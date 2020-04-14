---
title: AEM Forms 작업 영역 사용자 인터페이스의 로케일 변경
seo-title: AEM Forms 작업 영역 사용자 인터페이스의 로케일 변경
description: AEM Forms 작업 영역을 수정하여 텍스트, 축소된 카테고리, 큐 및 프로세스를 현지화하는 방법, 인터페이스의 날짜 선택기
seo-description: AEM Forms 작업 영역을 수정하여 텍스트, 축소된 카테고리, 큐 및 프로세스를 현지화하는 방법, 인터페이스의 날짜 선택기
uuid: c89ff150-a36e-45cc-99a6-8768dbe58eab
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 89f9d666-28e2-4201-8467-ae90693ca5d2
docset: aem65
translation-type: tm+mt
source-git-commit: 49da3dbe590f70b98185a6bc330db6077dc864c0

---


# AEM Forms 작업 영역 사용자 인터페이스의 로케일 변경{#changing-the-locale-of-aem-forms-workspace-user-interface}

AEM Forms 작업 공간에서는 영어, 프랑스어, 독일어 및 일본어를 기본적으로 지원합니다. 또한 AEM Forms 작업 영역 사용자 인터페이스를 다른 언어로 현지화할 수 있는 기능도 제공합니다.

AEM Forms 작업 영역 사용자 인터페이스를 원하는 언어로 현지화하려면:

* AEM Forms 작업 영역의 텍스트를 현지화합니다.
* 축소된 카테고리, 큐 및 프로세스를 현지화할 수 있습니다.
* 날짜 선택기 현지화

위의 단계를 수행하기 전에 AEM Forms 작업 영역 사용자 [지정에](../../forms/using/generic-steps-html-workspace-customization.md)대한 일반 단계에 나열된 단계를 따르십시오.

>[!NOTE]
>
>AEM Forms 작업 영역의 로그인 화면 언어를 변경하려면 [새 로그인 화면](../../forms/using/creating-new-login-screen.md)만들기를 참조하십시오.

## 텍스트 현지화 {#localizing-text}

다음 단계를 수행하여 언어 새로 만들기 및 브라우저 *로케일* 코드에 대한 지원을 *지금*&#x200B;추가합니다.

1. CRXDE Lite에 로그인합니다.
CRXDE Lite의 기본 URL은 `https://'[server]:[port]'/lc/crx/de/index.jsp`입니다.
1. 위치로 이동하여 새 폴더를 `apps/ws/locales` 만듭니다. `nw.`
1. 파일을 `translation.json`위치에서 `/apps/ws/locales/en-US` 위치로 복사합니다 `/apps/ws/locales/nw` .
1. 편집을 위해 탐색하고 `/apps/ws/locales/nw` 엽니다 `translation.json` . translation.json 파일을 로케일별로 변경합니다.

   다음 예에는 AEM Forms 작업 영역의 영어 및 프랑스어 로캘에 대한 translation.json 파일이 포함되어 있습니다.

   ![translation_json_in_en](assets/translation_json_in_en.png) ![translation_json_in_fr](assets/translation_json_in_fr.png)

## 축소된 카테고리, 대기열 및 프로세스 현지화 {#localizing-collapsed-categories-queues-and-processes}

AEM Forms 작업 영역에서는 이미지를 사용하여 카테고리, 큐 및 프로세스의 헤더를 표시합니다. 이러한 헤더를 현지화하려면 개발 패키지가 필요합니다. 개발 패키지 만들기에 대한 자세한 내용은 AEM Forms 작업 [영역 코드 작성을 참조하십시오.](introduction-customizing-html-workspace.md#building-html-workspace-code)

다음 단계에서는 새로운 현지화된 이미지 파일이 Categories_nw.png, Queue_ *nw.png*&#x200B;및 *Processes_nw.png**라고 가정합니다*. 권장 이미지 너비는 19px입니다.

>[!NOTE]
>
>브라우저의 브라우저 언어 로케일 코드를 찾으려면 열기 `https://'[server]:[port]'/lc/libs/ws/Locale.html`.

![collections_panels_image](assets/collapsing_panels_image.png)

이미지를 현지화하려면 다음 단계를 수행하십시오.

1. WebDAV 클라이언트를 사용하여 이미지 파일을 */apps/ws/images* 폴더에 배치합니다.
1. /apps/ws/css *로*&#x200B;이동합니다. 편집할 *newStyle.css* 를 열고 다음 항목을 추가합니다.

   ```
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

1. 작업 공간 사용자 정의 문서에 나열된 모든 의미 [변경 사항을](../../forms/using/introduction-customizing-html-workspace.md) 수행합니다.
1. js/runtime/utility *폴더로 이동하여* usersession.js ** 파일을 열어 편집합니다.
1. 원래 코드 블록에 나열된 코드를 찾고 조건 *lang!== &#39;nw&#39;* to if 문:

   ```
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

   ```
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

Datepicker API를 현지화하려면 개발 패키지가 *필요합니다* . 개발 패키지 만들기에 대한 자세한 내용은 AEM [Forms 작업 영역 코드](introduction-customizing-html-workspace.md#building-html-workspace-code)작성을 참조하십시오.

1. jQuery UI [패키지를](https://jqueryui.com/download/all/)다운로드하고 추출하면 *&lt;extraced jquery UI package>*\jquery-ui-1.10.2.zip\jquery-ui-1.10.2\ui\i18n으로 이동합니다.
1. 이제 로케일 코드의 jquery.ui.datepicker-nw.js 파일을 apps/ws/js/libs/jqueryi에 복사하고 로케일별 파일 변경을 수행합니다.
1. 편집할 파일을 `apps/ws/js` 찾아 엽니다 `jquery.ui.datepicker-nw.js` .
1. main.js 파일에서 파일에 대한 별칭을 `jquery.ui.datepicker-nw.js.` 만드는 코드는 `jquery.ui.datepicker-nw.js` 다음과 같습니다.

   ```
   jqueryuidatepickernw : pathprefix + 'libs/jqueryui/jquery.ui.datepicker-nw'
   ```

1. 별칭을 `jqueryuidatepickernw` 사용하여 `jquery.ui.datepicker-nw.js` 파일을 datepicker를 사용하는 모든 파일에 포함합니다. 날짜 입력기는 다음 파일에 사용됩니다.

   * `js/runtime/views/outofoffice.js`
   * `js/runtime/views/searchtemplatedetails.js`
   아래 샘플 코드는 jquery.ui.datepicker-nw.js의 항목을 추가하는 방법을 보여줍니다.

   ```
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

   ```
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

1. Datepicker API를 사용하는 모든 파일에서 기본 Datepicker API 설정을 변경합니다. 날짜 입력기 API는 다음 파일에 사용됩니다.

   * apps\ws\js\runtime\views\searchtemplatedetails.js
   * apps\ws\js\runtime\views\outofoffice.js
   다음 코드를 변경하여 새 로케일을 추가합니다.

   ```
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

   ```
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
