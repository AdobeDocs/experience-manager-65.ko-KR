---
title: 샘플 ContextHub UI 모듈 유형
seo-title: 샘플 ContextHub UI 모듈 유형
description: ContextHub에서는 솔루션에서 사용할 수 있는 몇 가지 샘플 UI 모듈을 제공합니다
seo-description: ContextHub에서는 솔루션에서 사용할 수 있는 몇 가지 샘플 UI 모듈을 제공합니다
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
translation-type: tm+mt
source-git-commit: a8ba56849f6bb9f0cf6571fc51f4b5cae71620e0
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 2%

---


# 샘플 ContextHub UI 모듈 유형 {#sample-contexthub-ui-module-types}

ContextHub에서는 솔루션에서 사용할 수 있는 몇 가지 샘플 UI 모듈을 제공합니다. 다음 정보가 제공됩니다.

* UI 모듈의 기본 기능
* 학습 목적으로 소스 코드를 열 수 있는 위치.
* UI 모듈을 구성하는 방법입니다.

ContextHub에 UI 모듈 추가에 대한 자세한 내용은 [UI 모듈 추가](ch-configuring.md#adding-a-ui-module)를 참조하십시오. UI 모듈 개발에 대한 자세한 내용은 [ContextHub UI 모듈 유형 만들기](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types)를 참조하십시오.

## contexthub.base UI 모듈 유형 {#contexthub-base-ui-module-type}

contexthub.base UI 모듈 유형은 다른 모든 UI 모듈 유형에 대한 기본 유형입니다. 따라서 저장소 데이터를 렌더링하기 위한 일반 기능을 제공합니다.

다음 기능을 사용할 수 있습니다.

* **제목 및 아이콘:** UI 모듈의 제목과 아이콘을 지정합니다. 이 아이콘은 URL을 사용하거나 Coral UI 아이콘 라이브러리에서 참조할 수 있습니다.
* **데이터 저장:** 데이터를 검색할 하나 이상의 저장소를 식별합니다.
* **컨텐츠:** UI 모듈에 나타나는 컨텐츠가 ContextHub 도구 모음에 나타날 때 나타나도록 지정합니다.
* **팝오버 컨텐츠:** UI 모듈을 클릭하거나 탭할 때 팝업에 표시되는 컨텐츠를 지정합니다.
* **전체 화면 모드:** 전체 화면 모드를 허용할지 여부를 제어합니다.

소스 코드는 /libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js에 있습니다.

### 구성 {#configuration}

JSON 형식의 Javascript 개체를 사용하여 contexthub.base UI 모듈을 구성합니다. 다음 속성을 포함하여 UI 모듈 기능을 구성합니다.

* **이미지:** 아이콘으로 표시할 이미지의 URL입니다.
* **아이콘:** Coral  [UI ](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html) iconclass의 이름입니다. 아이콘과 이미지 속성 모두에 대한 값을 지정하면 이미지가 사용됩니다.

* **title:** UI 모듈의 제목입니다. UI 모듈 아이콘 위에서 포인터가 일시 중지되면 제목이 나타납니다.
* **fullscreen:** UI 모듈이 전체 화면 모드를 지원하는지 여부를 나타내는 부울 값입니다. 전체 화면 모드를 방지하려면 `true`을 사용하고, 전체 화면 모드를 방지하려면 `false`을 사용합니다.

* **템플릿:** ContextHub  [](https://handlebarsjs.com/) 도구 모음에서 렌더링할 컨텐츠를 지정하는 Handlebarstemplate 최대 두 개의 `<p>` 태그를 사용합니다.

* **storeMapping:** 키/스토어 매핑입니다. 핸들바 템플릿의 키를 사용하여 관련 ContextHub 저장소 데이터에 액세스합니다.
* **list:** UI 모듈을 클릭할 때 팝업에서 목록으로 표시할 항목의 배열. 이 항목을 포함하는 경우 popuverTemplate을 포함하지 마십시오. 값은 다음 키가 있는 개체 배열입니다.

   * title:이 항목에 표시할 텍스트
   * image:(선택 사항) 왼쪽에 표시되어야 하는 이미지의 URL
   * 아이콘:(선택 사항) 왼쪽에 표시되어야 하는 CUI 아이콘 클래스이미지가 지정된 경우 무시됨
   * 선택:(선택 사항) 이 항목을 선택된 상태로 표시할지를 지정하는 부울 값(true=selected)입니다. 기본적으로 선택한 항목이 굵은 글꼴을 사용하여 표시됩니다. `listType` 속성을 사용하여 다른 모양을 구성합니다(아래 참조).

* **listType:** 팝업 목록 항목에 사용할 스타일입니다. 다음 값 중 하나를 사용하십시오.

   * 체크 표시
   * 확인란
   * 라디오

* **popoverTemplate:** UI 모듈을 클릭할 때 팝업에서 렌더링할 내용을 지정하는 Handlebars 템플릿입니다. 이 항목을 포함하는 경우 `list` 항목을 포함하지 마십시오.

### 예 {#example}

다음 예에서는 [contexthub.에뮬레이터](/help/sites-developing/ch-samplestores.md#granite-emulators-sample-store-candidate) 저장소의 정보를 표시하도록 contexthub.base UI 모듈을 구성합니다. `template` 항목은 `storeMapping` 항목이 설정하는 키를 사용하여 저장소에서 데이터를 가져오는 방법을 보여 줍니다.

```xml
{
   "icon": "coral-Icon--move",
    "title": "Screen Resolution",
    "storeMapping": {
      "emulator": "emulators"
    },
    "template": "<p>{{{ i18n \"Resolution\"}}}</p><p>{{{emulator.currentDevice.width}}} x {{{emulator.currentDevice.height}}}</p>"
}
```

![chlimage_1-76](assets/chlimage_1-76a.png)

## contexthub.browserinfo UI 모듈 유형 {#contexthub-browserinfo-ui-module-type}

contexthub.browserinfo UI 모듈에는 클라이언트 웹 브라우저 및 운영 체제에 대한 정보가 표시됩니다. 정보는 [contexthub.surferinfo](/help/sites-developing/ch-samplestores.md#contexthub-surferinfo-sample-store-candidate) 스토어 후보를 기준으로 surferinfo 스토어에서 얻습니다.

![chlimage_1-77](assets/chlimage_1-77a.png)

UI 모듈의 소스 코드는 /libs/granite/contexthub/components/modules/browserinfo에 있습니다. contexthub.browserinfo는 contexthub.base UI 모듈을 확장하지만 추가 함수를 재정의하거나 제공하지 않습니다. 구현은 브라우저 정보를 렌더링하기 위한 기본 구성을 제공합니다.

### 구성 {#configuration-1}

contexthub.browserinfo UI 모듈 인스턴스에는 세부 구성 값이 필요하지 않습니다. 다음 JSON 텍스트는 모듈의 기본 구성을 나타냅니다.

```xml
{
   "icon":"coral-Icon--globe",
   "title":"Browser/OS Information",
   "storeMapping":{"surferinfo":"surferinfo"},
   "template":"<p>{{surferinfo.browser.family}} {{surferinfo.browser.version}}</p><p>{{surferinfo.os.name}} {{surferinfo.os.version}}</p>"
}
```

## contexthub.datetime UI 모듈 유형 {#contexthub-datetime-ui-module-type}

contexthub.datetime UI 모듈은 [contexthub.datetime](/help/sites-developing/ch-samplestores.md#contexthub-datetime-sample-store-candidate) 저장소 후보를 기반으로 하는 datetime이라는 저장소에 저장된 날짜 및 시간을 표시합니다.

![chlimage_1-78](assets/chlimage_1-78a.png)

이 모듈에서는 스토어의 날짜와 시간을 변경할 수 있는 팝업 양식을 제공합니다.

contexthub.datetime UI 모듈의 소스는 /libs/granite/contexthub/components/modules/datetime에 있습니다.

### 구성 {#configuration-2}

contexthub.datetime UI 모듈의 인스턴스에는 세부 사항 구성에 대한 값이 필요하지 않습니다. 다음 JSON 텍스트는 모듈의 기본 구성을 나타냅니다.

```xml
{
   "icon":"coral-Icon--clock",
   "title":"DATE&TIME",
   "clickable":true,
   "storeMapping":{"d":"datetime"},
   "template":"<p class=\"contexthub-module-line1\">{{i18n \"Date&Time\"}}</p><p class=\"contexthub-module-line2\">{{d.formatted.locale.date}} {{d.formatted.locale.time}}</p>",
   "popoverTemplate":"<div class=\"datetime center\"><div class=\"coral-DatePicker-calendar\" data-init=\"datepicker\"><input class=\"coral-Textfield\" type=\"datetime\" value=\"{{d.formatted.iso}}\"><button class=\"coral-Button coral-Button--secondary coral-Button--square\" title=\"{{i18n \"Datetime picker\"}}\"><i class=\"coral-Icon coral-Icon--calendar coral-Icon--sizeS\"></i></button></div></div>"
}
```

## contexthub.location UI 모듈 유형 {#contexthub-location-ui-module-type}

contexthub.location UI 모듈은 클라이언트의 경도와 위도를 표시합니다. 이 모듈에서는 현재 위치를 변경하기 위해 클릭할 수 있는 Google 지도를 표시하는 팝오버를 제공합니다. 모듈은 [contexthub.geolocation](/help/sites-developing/ch-samplestores.md#contexthub-geolocation-sample-store-candidate) 저장소 후보를 기반으로 하는 지리적 위치라는 ContextHub 저장소에서 정보를 가져옵니다.

![chlimage_1-80](assets/chlimage_1-80a.png)

UI 모듈의 소스는 /etc/cloudsettings/default/contexthub/geolocation에 있습니다.

### 구성 {#configuration-4}

contexthub.location UI 모듈의 인스턴스에는 세부 사항 구성에 대한 값이 필요하지 않습니다. 다음 JSON 텍스트는 모듈의 기본 구성을 나타냅니다.

```xml
{
 "icon":"coral-Icon--compass",
 "title":"Location",
 "clickable":true,
 "editable":{"key":"/geolocation","disabled":[],"hidden":["/geolocation/generatedThumbnail","/geolocation/city","/geolocation/country"]},
 "fullscreen":true,
 "storeMapping":{"g":"geolocation"},
 "template":"<p>{{i18n \"Location\"}}</p><p>{{g.address.postalCode}} {{g.address.city}}{{#if g.address.city}}{{#if g.address.region}},{{/if}}{{/if}} {{g.address.region}}</p>",
 "list":[
  {"title":"Basel, Switzerland",
  "data":{"longitude":7.58929,"latitude":47.554746,"city":"Basel","country":"Switzerland"}},
  {"title":"Melbourne, Australia",
  "data":{"longitude":144.96328,"latitude":-37.814107,"city":"Melbourne","country":"Australia"}},
  {"title":"Beijing, China",
  "data":{"longitude":116.407526,"latitude":39.90403,"city":"Beijing","country":"China"}},
  {"title":"New York, NY, USA",
  "data":{"longitude":-74.005973,"latitude":40.714353,"city":"New York","country":"United States"}},
  {"title":"Paris, France",
  "data":{"longitude":2.352222,"latitude":48.856614,"city":"Paris","country":"France"}},
  {"title":"Rio de Janeiro, Brazil",
  "data":{"longitude":-43.20071,"latitude":-22.913395,"city":"Rio","country":"Brazil"}},
  {"title":"San Jose, CA, USA",
  "data":{"longitude":-121.894955,"latitude":37.339386,"city":"San Jose","country":"United States"}},
  {"title":"Tokyo, Japan",
  "data":{"longitude":139.691706,"latitude":35.689487,"city":"Shinjuku","country":"Japan"}}
 ],
 "listType":"checkmark"
}
```

## contexthub.screen-orientation UI 모듈 유형 {#contexthub-screen-orientation-ui-module-type}

contexthub.screen-orientation UI 모듈은 클라이언트의 현재 화면 방향을 표시합니다. 기본적으로 비활성화되어 있지만 이 모듈에서는 방향을 선택할 수 있는 팝업 창을 제공합니다. 이 모듈은 [granite.에뮬레이터](/help/sites-developing/ch-samplestores.md#granite-emulators-sample-store-candidate) 저장소 후보를 기반으로 하는 에뮬레이터라는 ContextHub 저장소에서 정보를 가져옵니다.

![chlimage_1-81](assets/chlimage_1-81a.png)

UI 모듈의 소스는 /libs/granite/contexthub/components/modules/screen-orientation에 있습니다.

### 구성 {#configuration-5}

contexthub.screen-orientation UI 모듈의 인스턴스에는 세부 구성 값이 필요하지 않습니다. 다음 JSON 텍스트는 모듈의 기본 구성을 나타냅니다. 기본적으로 `clickable` 속성은 `false`입니다. `clickable`을(를) `true`로 설정하도록 기본 구성을 재정의하면 모듈을 클릭하면 방향을 선택할 수 있는 팝업이 표시됩니다.

```xml
{
   "icon":"coral-Icon--rotateRight",
   "title":"Screen Orientation",
   "clickable":false,
   "storeMapping":{"emulator":"emulators"},
   "template":"<p>{{{ i18n \"Screen Orientation\" }}}</p><p>{{{ emulator.currentDevice.orientation }}}",
   "listReference":"/emulators/orientations",
   "listType":"checkmark"
}
```

## contexthub.tagcloud UI 모듈 유형 {#contexthub-tagcloud-ui-module-type}

contexthub.tagcloud UI 모듈에는 태그에 대한 정보가 표시됩니다. 도구 모음에서 UI 모듈에는 태그 수가 표시됩니다. 팝업에 새 태그를 추가하기 위한 태그 클라우드 및 텍스트 상자가 표시됩니다. UI 모듈은 [contexthub.tagcloud](/help/sites-developing/ch-samplestores.md#contexthub-tagcloud-sample-data-store) 저장소 후보를 기반으로 하는 tagcloud라는 ContextHub 저장소에서 정보를 가져옵니다.

![chlimage_1-82](assets/chlimage_1-82a.png)

UI 모듈의 소스는 /libs/granite/contexthub/components/modules/tagcloud에 있습니다.

### 구성 {#configuration-6}

contexthub.tagcloud UI 모듈 인스턴스에는 세부 사항 구성에 대한 값이 필요하지 않습니다. 다음 JSON 텍스트는 모듈의 기본 구성을 나타냅니다.

```xml
{
   "icon":"coral-Icon--tag",
   "title":"TagCloud",
   "clickable":true,
   "storeMapping":{"t":"tagcloud"},
   "maxTags":20,
   "template":"<p class=\"contexthub-module-line1\">{{i18n \"TagCloud\"}}</p><p class=\"contexthub-module-line2\">{{stats.total}} {{i18n \"Tags\"}}</p>",
   "popoverTemplate":"<div class=\"contexthub-popover-content center\"><p class=\"stats\">{{stats.total}} {{i18n \"Tags\"}} | {{stats.hits}} {{i18n \"Hits\"}} | {{i18n \"Last tag\"}}: {{#if stats.recent}}{{stats.recent}}{{else}}{{i18n \"Unknown\"}}{{/if}}</p><p class=\"tagcloud\">{{#each tags}}<span class=\"tag{{this.weight}}\">{{this.name}}</span> {{/each}}</p><div class=\"coral-InputGroup\"><input type=\"text\" class=\"coral-InputGroup-input coral-Textfield tag-name\" placeholder=\"{{i18n \"Add a namespace:my/tag\"}}\" pattern=\"^[A-Za-z0-9_\\-]+(:[A-Za-z0-9_\\-\\/]+)?$\" title=\"{{i18n \"namespace:my/tag\"}}\"><span class=\"coral-InputGroup-button\"><button class=\"coral-Button coral-Button--secondary coral-Button--square contexthub-new-tag\" type=\"button\" title=\"{{i18n \"increment\"}}\"><i class=\"coral-Icon coral-Icon--sizeS coral-Icon--add\"></i></button></span></div></div>"
}
```

## granite.profile UI 모듈 유형 {#granite-profile-ui-module-type}

granite.profile ContextHub UI 모듈은 현재 사용자의 표시 이름을 표시합니다. 팝업에 사용자의 로그인 이름이 표시되며 표시 이름의 값을 변경할 수 있습니다. UI 모듈은 [granite.profile](/help/sites-developing/ch-samplestores.md#granite-profile-sample-store-candidate) 저장소 후보를 기반으로 하는 프로필이라는 ContextHub 저장소에서 정보를 가져옵니다.

![chlimage_1-83](assets/chlimage_1-83a.png)

UI 모듈의 소스는 /libs/granite/contexthub/components/modules/profile에 있습니다.

### 구성 {#configuration-7}

grant.profile UI 모듈의 인스턴스에는 세부 구성 값이 필요하지 않습니다. 다음 JSON 텍스트는 모듈의 기본 구성을 나타냅니다.

```xml
{
   "icon":"coral-Icon--user",
   "title":"Profile",
   "clickable":true,
   "editable":{
      "key":"/profile",
      "disabled":["/profile/authorizableId"],
      "hidden":["/profile/avatar","/profile/path"]},
   "storeMapping":{"p":"profile"},
   "template":"<p class=\"contexthub-module-line1\">{{i18n \"Persona\"}}</p><p class=\"contexthub-module-line2\">{{p.displayName}}</p>",
   "listType":"checkmark"
}
```
