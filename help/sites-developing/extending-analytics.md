---
title: 이벤트 추적 확장
seo-title: 이벤트 추적 확장
description: AEM Analytics를 사용하여 웹 사이트에서 사용자 상호 작용을 추적할 수 있습니다.
seo-description: AEM Analytics를 사용하여 웹 사이트에서 사용자 상호 작용을 추적할 수 있습니다.
uuid: 722798ac-4043-4918-a6df-9eda2c85020b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e0372f4a-fe7b-4526-8391-5bb345b51d70
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# 이벤트 추적 확장{#extending-event-tracking}

AEM Analytics를 사용하면 웹 사이트에서 사용자 상호 작용을 추적할 수 있습니다. 개발자는 다음을 수행해야 합니다.

* 방문자가 구성 요소와 상호 작용하는 방식을 추적할 수 있습니다. 이 작업은 사용자 지정 이벤트로 수행할 수 [있습니다.](#custom-events)
* [ContextHub에서 값에 액세스합니다](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub).
* [레코드 콜백을](#adding-record-callbacks)추가합니다.

>[!NOTE]
>
>이 정보는 기본적으로 일반적이지만 특정 예제에 [Adobe](/help/sites-administering/adobeanalytics.md) Analytics를 사용합니다.
>
>구성 요소 및 대화 상자 개발에 대한 일반적인 내용은 구성 요소 [개발을 참조하십시오](/help/sites-developing/components.md).

## 사용자 지정 이벤트 {#custom-events}

사용자 지정 이벤트는 페이지에서 특정 구성 요소의 사용 가능성에 의존하는 모든 것을 추적합니다. 페이지 구성 요소가 다른 구성 요소로 처리되므로 템플릿별 이벤트도 포함합니다.

### 페이지 로드 시 사용자 지정 이벤트 추적 {#tracking-custom-events-on-page-load}

pseudo this can be done using the pseudo-attribute `data-tracking` (이전 레코드 속성은 이전 버전과의 호환성을 위해 여전히 지원됨). HTML 태그에 추가할 수 있습니다.

의 구문은 `data-tracking` 다음과 같습니다.

* `data-tracking="{'event': ['eventName'], 'values': {'key': 'value', 'nextKey': 'nextValue'}, componentPath: 'myapp/component/mycomponent'}"`

키-값 쌍의 수를 페이로드라고 하는 두 번째 매개 변수로 전달할 수 있습니다.

예를 들면 다음과 같습니다.

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

페이지 로드 시 모든 `data-tracking` 속성이 수집되어 ContextHub의 이벤트 저장소에 추가되며, 여기에서 Adobe Analytics 이벤트에 매핑할 수 있습니다. 매핑되지 않은 이벤트는 Adobe Analytics에서 추적하지 않습니다. 매핑 [이벤트에 대한 자세한 내용은 Adobe](/help/sites-administering/adobeanalytics.md) Analytics에 연결을 참조하십시오.

### 페이지 로드 후 사용자 지정 이벤트 추적 {#tracking-custom-events-after-page-load}

페이지가 로드된 후 발생하는 이벤트(예: 사용자 상호 작용)를 추적하려면 JavaScript `CQ_Analytics.record` 함수를 사용합니다.

* `CQ_Analytics.record({event: 'eventName', values: { valueName: 'VALUE' }, collect: false, options: { obj: this, defaultLinkType: 'X' }, componentPath: '<%=resource.getResourceType()%>'})`

위치

* `events` 은 문자열 또는 문자열 배열(여러 이벤트에 대해)입니다.

* `values` 추적할 모든 값을 포함합니다.
* `collect` 은 선택 사항이며 이벤트 및 데이터 객체가 포함된 배열을 반환합니다.
* `options` 은 선택 사항이며 HTML 요소 `obj` 및 ` [defaultLinkType](https://microsite.omniture.com/t2/help/en_US/sc/implement/index.html#linkType)`같은 링크 추적 옵션을 포함합니다.

* `componentPath` 은 필수 특성이며 `<%=resource.getResourceType()%>`

예를 들어, 다음 정의에서 맨 위로 **이동** 링크를 클릭하면 두 개의 이벤트가 `jumptop` 실행되고 `headlineclick`실행됩니다.

```xml
<h1 data-tracking="{event: 'headline', values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'}">
  My Headline <a href="#" onclick="CQ_Analytics.record({event: ['jumptop','headlineclick'],  values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'})">Jump to top</a>
</h1>
```

## ContextHub에서 값 액세스 {#accessing-values-in-the-contexthub}

ContextHub JavaScript API에는 가능한 경우 지정된 스토어를 반환하는 함수가 `getStore(name)` 있습니다. 저장소에 지정된 키(있는 경우)의 값을 반환하는 `getItem(key)` 함수가 있습니다. 이 `getKeys()` 함수를 사용하면 특정 저장소에 대해 정의된 키 배열을 검색할 수 있습니다.

함수를 사용하여 함수를 바인딩하여 저장소에서 값 변경 내용을 알릴 수 `ContextHub.getStore(name).eventing.on(ContextHub.Constants.EVENT_STORE_UPDATED, handler, selector, triggerForPastEvents)` 있습니다.

ContextHub의 초기 가용성을 알리는 가장 좋은 방법은 `ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);` 함수를 사용하는 것입니다.

**ContextHub에 대한 추가 이벤트:**

모든 스토어 준비:

`ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`

저장별:

`ContextHub.getStore(store).eventing.on(ContextHub.Constants.EVENT_STORE_READY, handler, selector, triggerForPastEvents)`

>[!NOTE]
>
>전체 ContextHub [API 참조](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/contexthub-api.html#ContextHubJavascriptAPIReference)

## 레코드 콜백 추가 {#adding-record-callbacks}

호출 전과 후 는 함수 `CQ_Analytics.registerBeforeCallback(callback,rank)` 및 `CQ_Analytics.registerAfterCallback(callback,rank)`을 사용하여 등록됩니다.

두 함수는 첫 번째 인수로 함수를 사용하고 두 번째 인수로 등급을 가져와서 콜백이 실행되는 순서를 나타냅니다.

콜백이 false를 반환하면 실행 체인에 따라 콜백이 실행되지 않습니다.
