---
title: 이벤트 추적 확장
seo-title: 이벤트 추적 확장
description: AEM Analytics를 사용하면 웹 사이트에서 사용자 상호 작용을 추적할 수 있습니다
seo-description: AEM Analytics를 사용하면 웹 사이트에서 사용자 상호 작용을 추적할 수 있습니다
uuid: 722798ac-4043-4918-a6df-9eda2c85020b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e0372f4a-fe7b-4526-8391-5bb345b51d70
exl-id: a71d20e6-0321-4afb-95fe-6de8b7b37245
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 1%

---

# 이벤트 추적 확장{#extending-event-tracking}

AEM Analytics를 사용하면 웹 사이트에서 사용자 상호 작용을 추적할 수 있습니다. 개발자로서 다음을 수행해야 할 수 있습니다.

* 방문자가 구성 요소와 상호 작용하는 방법을 추적합니다. 이 작업은 [사용자 지정 이벤트로 수행할 수 있습니다.](#custom-events)
* [ContextHub에서 값에 액세스합니다](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub).
* [레코드 콜백을 추가합니다](#adding-record-callbacks).

>[!NOTE]
>
>이 정보는 기본적으로 일반적이지만 특정 예제에 [Adobe Analytics](/help/sites-administering/adobeanalytics.md)을 사용합니다.
>
>구성 요소 및 대화 상자 개발에 대한 일반적인 정보는 [구성 요소 개발](/help/sites-developing/components.md)을 참조하십시오.

## 사용자 지정 이벤트 {#custom-events}

사용자 지정 이벤트는 페이지에서 특정 구성 요소의 가용성에 따라 달라지는 모든 것을 추적합니다. 페이지 구성 요소가 다른 구성 요소로 처리되므로 여기에 템플릿별 이벤트가 포함됩니다.

### 페이지 로드 시 사용자 지정 이벤트 추적 {#tracking-custom-events-on-page-load}

이 작업은 의사 특성 `data-tracking` 을 사용하여 수행할 수 있습니다(이전 레코드 속성은 이전 버전과의 호환성을 위해 계속 지원됨). HTML 태그에 추가할 수 있습니다.

`data-tracking`의 구문은 다음과 같습니다

* `data-tracking="{'event': ['eventName'], 'values': {'key': 'value', 'nextKey': 'nextValue'}, componentPath: 'myapp/component/mycomponent'}"`

임의의 수의 키-값 쌍을 페이로드라고 하는 두 번째 매개 변수로 전달할 수 있습니다.

예는 다음과 같습니다.

```xml
<span data-tracking="{event:'blogEntryView',
                                values:{
                                   'blogEntryContentType': 'blog',
                                   'blogEntryUniqueID': '<%= xssAPI.encodeForJSString(entry.getId()) %>',
                                   'blogEntryTitle': '<%= xssAPI.encodeForJSString(entry.getTitle()) %>',
                                   'blogEntryAuthor':'<%= xssAPI.encodeForJSString(entry.getAuthor()) %>',
                                   'blogEntryPageLanguage':'<%= currentPage.getLanguage(true) %>'
                                },
                                componentPath:'myapp/component/mycomponent'}">
</span>
```

페이지 로드 시 모든 `data-tracking` 속성이 수집되어 ContextHub의 이벤트 저장소에 추가됩니다. 이 위치에서 Adobe Analytics 이벤트에 매핑할 수 있습니다. 매핑되지 않은 이벤트는 Adobe Analytics에서 추적하지 않습니다. 매핑 이벤트에 대한 자세한 내용은 [Adobe Analytics에 연결](/help/sites-administering/adobeanalytics.md)을 참조하십시오.

### 페이지 로드 후 사용자 지정 이벤트 추적 {#tracking-custom-events-after-page-load}

페이지가 로드된 후 발생하는 이벤트(예: 사용자 상호 작용)를 추적하려면 `CQ_Analytics.record` JavaScript 함수를 사용합니다.

* `CQ_Analytics.record({event: 'eventName', values: { valueName: 'VALUE' }, collect: false, options: { obj: this, defaultLinkType: 'X' }, componentPath: '<%=resource.getResourceType()%>'})`

위치

* `events` 는 문자열 또는 문자열 배열(여러 이벤트의 경우)입니다.

* `values` 추적할 모든 값을 포함합니다
* `collect` 는 선택 사항이며 이벤트 및 데이터 개체가 포함된 배열이 반환됩니다.
* `options` 는 선택 사항이며 HTML 요소  `obj` 및  ` [defaultLinkType](https://microsite.omniture.com/t2/help/en_US/sc/implement/index.html#linkType)`와 같은 링크 추적 옵션을 포함합니다.

* `componentPath` 는 필수 속성이므로 로 설정하는 것이 좋습니다.  `<%=resource.getResourceType()%>`

예를 들어, 다음 정의를 사용하여 **맨 위로 이동** 링크를 클릭하면 두 이벤트 `jumptop` 및 `headlineclick`이 실행됩니다.

```xml
<h1 data-tracking="{event: 'headline', values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'}">
  My Headline <a href="#" onclick="CQ_Analytics.record({event: ['jumptop','headlineclick'],  values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'})">Jump to top</a>
</h1>
```

## ContextHub {#accessing-values-in-the-contexthub}의 값에 액세스

ContextHub JavaScript API에는 지정된 스토어를 반환하는 `getStore(name)` 함수가 있습니다(가능한 경우). 가능한 경우 지정된 키의 값을 반환하는 `getItem(key)` 함수가 저장소에 있습니다. `getKeys()` 함수를 사용하면 특정 저장소에 대해 정의된 키 배열을 검색할 수 있습니다.

`ContextHub.getStore(name).eventing.on(ContextHub.Constants.EVENT_STORE_UPDATED, handler, selector, triggerForPastEvents)` 함수를 사용하여 함수를 바인딩하여 저장소에서 값 변경 사항에 대한 알림을 받을 수 있습니다.

ContextHub의 초기 가용성에 대한 알림을 받는 가장 좋은 방법은 `ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);` 함수를 사용하는 것입니다.

**ContextHub에 대한 추가 이벤트:**

모든 스토어가 준비되었습니다.

`ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`

저장 특정:

`ContextHub.getStore(store).eventing.on(ContextHub.Constants.EVENT_STORE_READY, handler, selector, triggerForPastEvents)`

>[!NOTE]
>
>전체 [ContextHub API 참조](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/contexthub-api.html#ContextHubJavascriptAPIReference)도 참조하십시오

## 레코드 콜백 추가 {#adding-record-callbacks}

콜백 전후에 `CQ_Analytics.registerBeforeCallback(callback,rank)` 및 `CQ_Analytics.registerAfterCallback(callback,rank)` 함수를 사용하여 등록됩니다.

두 함수 모두 첫 번째 인수로 함수를 가져오고 두 번째 인수로서 등급을 가져와서 콜백이 실행되는 순서를 나타냅니다.

콜백이 false를 반환하는 경우 실행 체인에서 다음에 오는 콜백이 실행되지 않습니다.
