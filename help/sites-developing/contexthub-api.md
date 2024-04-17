---
title: ContextHub JavaScript API 참조
description: ContextHub JavaScript API는 ContextHub 구성 요소가 페이지에 추가되면 스크립트에 사용할 수 있습니다
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
feature: Context Hub,Developing,Personalization
exl-id: b472d96f-b1a5-40b7-be2a-52f3396f6884
solution: Experience Manager, Experience Manager Sites
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '4913'
ht-degree: 2%

---

# ContextHub JavaScript API 참조{#contexthub-javascript-api-reference}

ContextHub JavaScript API는 다음과 같은 경우에 스크립트에서 사용할 수 있습니다. [ContextHub 구성 요소가 페이지에 추가되었습니다](/help/sites-developing/ch-adding.md#adding-contexthub-to-a-page-component).

## ContextHub 상수 {#contexthub-constants}

ContextHub JavaScript API에서 정의하는 상수 값입니다.

### 이벤트 상수 {#event-constants}

다음 표에는 ContextHub 저장소에서 발생하는 이벤트의 이름이 나열되어 있습니다. 참조: [ContextHub.Utils.Eventing](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing).

| 상수 | 설명 | 값 |
|---|---|---|
| ContextHub.Constants.EVENT_NAMESPACE | ContextHub의 이벤트 네임스페이스 | ch |
| ContextHub.Constants.EVENT_ALL_STORES_READY | 필요한 모든 저장소가 등록되고 초기화되어 사용할 준비가 되었음을 나타냅니다. | 모든 상점 준비되어 |
| ContextHub.Constants.EVENT_STORES_PARTIALLY_READY | 지정된 시간 제한 내에 모든 저장소가 초기화되지 않았음을 나타냅니다. | 부분적으로 준비되 |
| ContextHub.Constants.EVENT_STORE_REGISTERED | 스토어가 등록되면 실행됨 | 저장소 등록됨 |
| ContextHub.Constants.EVENT_STORE_READY | 스토어가 작동할 준비가 되었음을 나타냅니다. JSONP 스토어를 제외하고 등록 직후 트리거되며 데이터를 가져올 때 실행됩니다. | 저장소 기반 |
| ContextHub.Constants.EVENT_STORE_UPDATED | 스토어가 지속성을 업데이트할 때 실행됨 | 스토어 업데이트됨 |
| ContextHub.Constants.PERSISTENCE_CONTAINER_NAME | 지속성 컨테이너 이름 | Context허브 지속성 |
| ContextHub.Constants.SERVICE_RAW_RESPONSE_KEY | 원시 JSON 결과가 저장되는 특정 지속성 키 이름을 저장합니다. | /_/raw 응답 |
| ContextHub.Constants.SERVICE_RESPONSE_TIME_KEY | JSON 데이터를 가져온 시기를 나타내는 특정 타임스탬프를 저장합니다. | /_/응답 시간 |
| ContextHub.Constants.SERVICE_LAST_URL_KEY | 마지막 호출 동안 사용된 JSON 서비스의 특정 URL 저장 | /_/url |
| ContextHub.Constants.IS_CONTAINER_EXPANDED | ContextHub의 UI가 확장되었는지 여부를 나타냅니다. | /_/container-extended |

### UI 이벤트 상수 {#ui-event-constants}

다음 표에는 ContextHub UI에 대해 발생하는 이벤트의 이름이 나열되어 있습니다.

| **상수** | **설명** | **값** |
|---|---|---|
| ContextHub.Constants.EVENT_UI_MODE_REGISTERED | 모드가 등록되면 실행됩니다. | ui 모드 등록됨 |
| ContextHub.Constants.EVENT_UI_MODE_UNREGISTERED | 모드가 등록 취소되면 실행됩니다. | ui 모드 등록 취소됨 |
| ContextHub.Constants.EVENT_UI_MODE_RENDERER_REGISTERED | 모드 렌더러가 등록되면 실행됩니다. | ui-mode-renderer-registered |
| ContextHub.Constants.EVENT_UI_MODE_RENDERER_UNREGISTERED | 모드 렌더러가 등록 취소되면 실행됩니다. | ui-mode-renderer-unregistered |
| ContextHub.Constants.EVENT_UI_MODE_ADDED | 새 모드가 추가되면 실행됩니다. | ui 모드 추가됨 |
| ContextHub.Constants.EVENT_UI_MODE_REMOVED | 모드가 제거되면 실행됩니다. | ui 모드 제거됨 |
| ContextHub.Constants.EVENT_UI_MODE_SELECTED | 사용자가 모드를 선택하면 실행됩니다. | ui 모드 선택됨 |
| ContextHub.Constants.EVENT_UI_MODULE_REGISTERED | 새 모듈이 등록되면 실행됩니다. | ui-module-registered |
| ContextHub.Constants.EVENT_UI_MODULE_UNREGISTERED | 모듈이 등록 취소되면 실행됩니다. | ui-module이 등록되지 않음 |
| ContextHub.Constants.EVENT_UI_MODULE_RENDERER_REGISTERED | 모듈 렌더러가 등록되면 실행됩니다. | ui-module-renderer-registered |
| ContextHub.Constants.EVENT_UI_MODULE_RENDERER_UNREGISTERED | 모듈 렌더러가 등록 취소될 때 실행됨 | ui-module-renderer-unregistered |
| ContextHub.Constants.EVENT_UI_MODULE_ADDED | 새 모듈이 추가되면 실행됩니다. | ui-module-added |
| ContextHub.Constants.EVENT_UI_MODULE_REMOVED | 모듈이 제거되면 실행됩니다. | ui-module이 제거됨 |
| ContextHub.Constants.EVENT_UI_CONTAINER_ADDED | UI 컨테이너가 페이지에 추가되면 실행됩니다 | ui-container-added |
| ContextHub.Constants.EVENT_UI_CONTAINER_OPENED | ContextHub UI가 열리면 실행됩니다. | ui-container-opened |
| ContextHub.Constants.EVENT_UI_CONTAINER_CLOSED | ContextHub UI가 축소되면 실행됩니다 | ui-container-closed |
| ContextHub.Constants.EVENT_UI_PROPERTY_MODIFIED | 속성이 수정되면 실행됩니다. | ui-property-modified |
| ContextHub.Constants.EVENT_UI_RENDERED | ContextHub UI가 렌더링될 때마다(예: 속성 변경 후) 실행됩니다 | ui 렌더링됨 |
| ContextHub.Constants.EVENT_UI_INITIALIZED | UI 컨테이너가 초기화되면 실행됩니다. | ui 초기화됨 |
| ContextHub.Constants.ACTIVE_UI_MODE | 활성 UI 모드를 나타냅니다. | /_/active-ui-mode |

## ContextHub JavaScript API 참조 {#contexthub-javascript-api-reference-2}

ContextHub 개체는 모든 저장소에 대한 액세스를 제공합니다.

### 함수(ContextHub) {#functions-contexthub}

#### getAllStores() {#getallstores}

등록된 모든 ContextHub 저장소를 반환합니다.

이 함수에는 매개 변수가 없습니다.

**반환**

모든 ContextHub 저장소를 포함하는 개체입니다. 각 저장소는 저장소와 동일한 이름을 사용하는 객체입니다.

**예**

다음 예제에서는 모든 스토어를 검색한 다음 지리적 위치 스토어를 검색합니다.

```
var allStores = ContextHub.getAllStores();
var geoloc = allStores.geolocation
```

#### getStore(name) {#getstore-name}

저장소를 JavaScript 개체로 검색합니다.

**매개변수**

* **이름:** 스토어가 등록된 이름입니다.

**반환**

저장소를 나타내는 개체입니다.

**예**

다음 예제에서는 geolocation 스토어를 검색합니다.

```
var geoloc = ContextHub.getStore("geolocation");
```

## ContextHub.SegmentEngine.Segment {#contexthub-segmentengine-segment}

ContextHub 세그먼트를 나타냅니다. 세그먼트를 가져오려면 ContextHub.SegmentEngine.SegmentManager를 사용합니다.

### 함수(ContextHub.ContextEngine.Segment) {#functions-contexthub-contextengine-segment}

#### getName() {#getname}

세그먼트 이름을 문자열 값으로 반환합니다.

#### getPath() {#getpath}

세그먼트 정의의 저장소 경로를 문자열 값으로 반환합니다.

## ContextHub.SegmentEngine.SegmentManager {#contexthub-segmentengine-segmentmanager}

ContextHub 세그먼트에 대한 액세스를 제공합니다.

### 함수(ContextHub.SegmentEngine.SegmentManager) {#functions-contexthub-segmentengine-segmentmanager}

#### getResolvedSegments() {#getresolvedsegments}

현재 컨텍스트에서 확인된 세그먼트를 반환합니다. 이 함수에는 매개 변수가 없습니다.

**반환**

ContextHub.SegmentEngine.Segment 객체의 배열입니다.

## ContextHub.Store.Core {#contexthub-store-core}

ContextHub 저장소의 기본 클래스입니다.

### 속성(ContextHub.Store.Core) {#properties-contexthub-store-core}

#### 이벤트 {#eventing}

A [ContextHub.Utils.Eventing](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) 개체. 이벤트를 저장하는 바인딩 함수에 이 개체를 사용합니다. 기본값 및 초기화에 대한 자세한 내용은 [init(name,config)](/help/sites-developing/contexthub-api.md#init-name-config).

#### 이름 {#name}

스토어의 이름입니다.

#### 지속성 {#persistence}

ContextHub.Utils.Persistence 개체입니다. 기본값 및 초기화에 대한 자세한 내용은 `[init(name,config)](/help/sites-developing/contexthub-api.md#init-name-config).`

### 함수(ContextHub.Store.Core) {#functions-contexthub-store-core}

#### addAllItems(tree, options) {#addallitems-tree-options}

데이터 개체 또는 배열을 저장소 데이터와 병합합니다. 개체 또는 배열의 각 키/값 쌍은 저장소를 통해 `setItem` 함수):

* **개체:** 키는 속성 이름입니다.
* **배열:** 키는 배열 인덱스입니다.

값은 개체가 될 수 있습니다.

**매개변수**

* **트리:** (개체 또는 배열) 저장소에 추가할 데이터입니다.
* **옵션:** (객체) setItem 함수에 전달되는 옵션의 선택적 객체입니다. 자세한 내용은 `options` 매개 변수 [setItem(key,value,options)](/help/sites-developing/contexthub-api.md#setitem-key-value-options).

**반환**

A `boolean` 값:

* 값 `true` 데이터 개체가 저장되었음을 나타냅니다.
* 값 `false` 는 데이터 저장소가 변경되지 않았음을 나타냅니다.

#### addReference(key, anotherKey) {#addreference-key-anotherkey}

한 키에서 다른 키로의 참조를 만듭니다. 키는 자신을 참조할 수 없습니다.

**매개변수**

* **키:** 참조하는 키 `anotherKey`.

* **다른 키:** 참조되는 키 `key`.

**반환**

A `boolean` 값:

* 값 `true` 참조가 추가되었음을 나타냅니다.
* 값 `false` 참조가 추가되지 않았음을 나타냅니다.

#### announceReadiness() {#announcereadiness}

트리거 `ready` 이 스토어에 대한 이벤트입니다. 이 함수에는 매개 변수가 없으며 값을 반환하지 않습니다.

#### clean() {#clean}

저장소에서 모든 데이터를 제거합니다. 함수에는 매개 변수와 반환 값이 없습니다.

#### getItem(key) {#getitem-key}

키와 연결된 값을 반환합니다.

**매개변수**

* **키:** (문자열) 값을 반환할 키입니다.

**반환**

키의 값을 나타내는 개체입니다.

#### getKeys(includeInternals) {#getkeys-includeinternals}

스토어에서 키를 검색합니다. 필요한 경우 ContextHub 프레임워크에서 내부적으로 사용되는 키를 검색할 수 있습니다.

**매개변수**

* **includeInternals:** 값 `true` 결과에 내부적으로 사용된 키를 포함합니다. 이 키는 밑줄(&quot;_&quot;) 문자로 시작합니다. 기본값은 `false`입니다.

**반환**

키 이름의 배열( `string` 값).

#### getReferences() {#getreferences}

저장소에서 참조를 검색합니다.

**반환**

참조 키를 참조된 키의 인덱스로 사용하는 배열입니다.

* 참조 키는 `key` 매개 변수 `addReference` 함수.

* 참조된 키는 `anotherKey` 매개 변수 `addReference` 함수.

#### getTree(includeInternal) {#gettree-includeinternals}

스토어에서 데이터 트리를 검색합니다. 필요한 경우 ContextHub 프레임워크에서 내부적으로 사용하는 키/값 쌍을 포함할 수 있습니다.

**매개변수**

* `includeInternals:` 값 `true` 내부적으로 사용된 키/값 쌍을 결과에 포함합니다. 이 데이터의 키는 밑줄(&quot;_&quot;) 문자로 시작합니다. 기본값은 `false`입니다.

**반환**

데이터 트리를 나타내는 개체입니다. 키는 개체의 속성 이름입니다.

#### init(name, config) {#init-name-config}

저장소를 초기화합니다.

* 저장소 데이터를 빈 개체로 설정합니다.
* 저장소 참조를 빈 개체로 설정합니다.
* eventChannel 은 다음과 같은 데이터입니다.*이름*, 여기서 *이름* 는 스토어 이름입니다.

* storeDataKey 는 /store/ 입니다.*이름*, 여기서 *이름* 는 스토어 이름입니다.

**매개변수**

* **이름:** 스토어의 이름입니다.
* **구성:** 구성 속성이 포함된 개체:

   * eventDefering: 기본값은 32입니다.
   * 이벤트: [ContextHub.Utils.Eventing](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) 이 저장소에 대한 개체입니다. 기본값은 ContextHub.eventing 개체에서 사용하는 ContextHub.eventing입니다.
   * 지속성: 이 저장소의 ContextHub.Utils.Persistence 개체입니다. 기본값은 ContextHub.persistence 개체입니다.

#### isEventingPaused() {#iseventingpaused}

이 저장소에 대한 이벤트가 일시 중지되었는지 여부를 결정합니다.

**반환**

부울 값:

* `true`: 이 저장소에 대해 트리거된 이벤트가 없도록 이벤트가 일시 중지되었습니다.
* `false`: 이 저장소에 대해 이벤트가 트리거되도록 이벤트가 일시 중지되지 않았습니다.

#### pauseEventing() {#pauseeventing}

이벤트가 트리거되지 않도록 스토어에 대한 이벤트를 일시 중지합니다. 이 함수는 매개 변수가 필요하지 않으며 값을 반환하지 않습니다.

#### removeItem(key, options) {#removeitem-key-options}

저장소에서 키/값 쌍을 제거합니다.

키가 제거되면 함수는 `data` 이벤트. 이벤트 데이터에는 저장소 이름, 제거된 키의 이름, 제거된 값, 키의 새 값(null) 및 &quot;remove&quot;라는 작업 유형이 포함됩니다.

필요한 경우 의 트리거를 방지할 수 있습니다. `data` 이벤트.

**매개변수**

* **키:** (문자열) 제거할 키의 이름입니다.
* **옵션:** (객체) 옵션의 객체입니다. 다음 개체 속성이 유효합니다.

   * silent: 값 `true` 의 트리거를 방지합니다. `data` 이벤트. 기본값은 `false`입니다.

**반환**

A `boolean` 값:

* 값 `true` 키/값 쌍이 제거되었음을 나타냅니다.
* 값 `false` 저장소에서 키를 찾을 수 없기 때문에 데이터 저장소가 변경되지 않았음을 나타냅니다.

#### removeReference(key) {#removereference-key}

저장소에서 참조를 제거합니다.

**매개변수**

* **키:** 제거할 키 참조입니다. 이 매개 변수는 `key` 매개 변수 `addReference` 함수.

**반환**

A `boolean` 값:

* 값 `true` 참조가 제거되었음을 나타냅니다.
* 값 `false` 키가 유효하지 않고 저장소가 변경되지 않았음을 나타냅니다.

#### reset(keepRemainingData) {#reset-keepremainingdata}

저장소 지속 데이터의 초기 값을 재설정합니다. 선택적으로 저장소에서 다른 모든 데이터를 제거할 수 있습니다. 저장소가 다시 설정되는 동안 이 저장소에 대한 이벤트가 일시 중지되었습니다. 이 함수는 값을 반환하지 않습니다.

초기 값은 저장소 개체를 인스턴스화하는 데 사용되는 구성 개체의 initialValues 속성에 제공됩니다.

**매개변수**

* **keepRemainingData:** (부울) 값이 true 로 설정되면 초기 데이터가 아닌 데이터가 지속됩니다. false 값을 지정하면 초기 값을 제외한 모든 데이터가 제거됩니다.

저장소 지속 데이터의 초기 값을 재설정합니다. 선택적으로 저장소에서 다른 모든 데이터를 제거할 수 있습니다. 저장소가 다시 설정되는 동안 이 저장소에 대한 이벤트가 일시 중지되었습니다. 이 함수는 값을 반환하지 않습니다.

초기 값은 저장소 개체를 인스턴스화하는 데 사용되는 구성 개체의 initialValues 속성에 제공됩니다.

**매개변수**

* keepRemainingData: (부울) 값이 true이면 초기 데이터가 아닌 데이터가 지속됩니다. false 값을 지정하면 초기 값을 제외한 모든 데이터가 제거됩니다.

#### resolveReference(key, retry) {#resolvereference-key-retry}

참조된 키를 검색합니다. 선택적으로 최상의 일치 문제를 해결하는 데 사용할 반복 횟수를 지정할 수 있습니다.

**매개변수**

* **키:** (문자열) 참조를 확인할 키입니다. 이 `key` 매개 변수는 `key` 매개 변수 `addReference` 함수.

* **다시 시도:** (숫자) 사용할 반복 횟수입니다.

**반환**

A `string` 참조된 키를 나타내는 값입니다. 참조가 확인되지 않으면 `key` 매개 변수가 반환됩니다.

#### resumeEventing() {#resumeeventing}

이벤트가 트리거되도록 이 스토어에 대한 이벤트를 다시 시작합니다. 이 함수는 매개 변수를 정의하지 않으며 값을 반환하지 않습니다.

#### setItem(키, 값, 옵션) {#setitem-key-value-options}

저장소에 키/값 쌍을 추가합니다.

트리거 `data` 이벤트 는 키에 대한 값이 현재 키에 저장된 값과 다른 경우에만 발생합니다. 필요한 경우 의 트리거를 방지할 수 있습니다. `data` 이벤트.

이벤트 데이터에는 저장소 이름, 키, 이전 값, 새 값 및 의 작업 유형이 포함됩니다. `set`.

**매개변수**

* **키:** (문자열) 키의 이름입니다.
* **옵션:** (객체) 옵션의 객체입니다. 다음 개체 속성이 유효합니다.

   * silent: 값 `true` 의 트리거를 방지합니다. `data` 이벤트. 기본값은 `false`입니다.

* **값:** (객체) 키와 연결할 값입니다.

**반환**

A `boolean` 값:

* 값 `true` 데이터 개체가 저장되었음을 나타냅니다.
* 값 `false` 는 데이터 저장소가 변경되지 않았음을 나타냅니다.

## ContextHub.Store.JSONPStore {#contexthub-store-jsonpstore}

JSON 데이터가 포함된 저장소입니다. 데이터는 외부 JSONP 서비스 또는 JSON 데이터를 반환하는 서비스에서 검색됩니다. 다음을 사용하여 서비스 세부 정보 지정 [`init`](/help/sites-developing/contexthub-api.md#init-name-config) 이 클래스의 인스턴스를 만들 때 작동합니다.

저장소는 인메모리 지속성(JavaScript 변수)을 사용합니다. 저장 데이터는 페이지 수명 동안에만 사용할 수 있습니다.

ContextHub.Store.JSONPtore 확장 [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) 및 는 해당 클래스의 함수를 상속합니다.

### 함수(ContextHub.Store.JSONPtore) {#functions-contexthub-store-jsonpstore}

#### configureService(serviceConfig, override) {#configureservice-serviceconfig-override}

이 개체가 사용하는 JSONP 서비스에 연결하기 위한 세부 정보를 구성합니다. 기존 구성을 업데이트하거나 바꿀 수 있습니다. 이 함수는 값을 반환하지 않습니다.

**매개변수**

* **serviceConfig:** 다음 속성을 포함하는 객체입니다.

   * host: (문자열) 서버 이름 또는 IP 주소입니다.
   * jsonp: (부울) 값이 true 이면 서비스가 JSONP 서비스이고 그렇지 않으면 false 입니다. true인 경우 {callback: &quot;ContextHub.Callbacks.*Object.name*} 개체가 service.params 개체에 추가됩니다.
   * params: (오브젝트) 오브젝트 속성으로 표시되는 URL 매개 변수입니다. 매개 변수 이름은 속성 이름이고 매개 변수 값은 속성 값입니다.
   * path: (문자열) 서비스 경로입니다.
   * port: (숫자) 서비스의 포트 번호입니다.
   * secure: (문자열 또는 부울) 서비스 URL에 사용할 프로토콜을 결정합니다.

      * 자동: //
      * true: https://
      * false: https://

* **재정의:** (부울) 값 `true` 기존 서비스 구성이 의 속성으로 대체됩니다. `serviceConfig`. 값 `false` 기존 서비스 구성 속성을 의 속성과 병합합니다. `serviceConfig`.

#### getRawResponse() {#getrawresponse}

JSONP 서비스에 대한 마지막 호출 이후 캐시된 원시 응답을 반환합니다. 함수에는 매개 변수가 필요하지 않습니다.

**반환**

원시 응답을 나타내는 개체입니다.

#### getServiceDetails() {#getservicedetails}

이 ContextHub.Store.JSONPtore 개체에 대한 서비스 개체를 검색합니다. 서비스 개체에는 서비스 URL을 만드는 데 필요한 모든 정보가 들어 있습니다.

**반환**

다음 속성을 갖는 객체:

* **호스트:** (문자열) 서버 이름 또는 IP 주소입니다.
* **jsonp:** (부울) 값이 true 이면 서비스가 JSONP 서비스이고 그렇지 않으면 false 입니다. true인 경우 {callback: &quot;ContextHub.Callbacks.*Object.name*} 개체가 service.params 개체에 추가됩니다.

* **매개 변수:** (객체) 객체 속성으로 표시되는 URL 매개 변수. 매개 변수 이름은 속성 이름이고 매개 변수 값은 속성 값입니다.
* **경로:** (문자열) 서비스 경로입니다.
* **포트:** (번호) 서비스의 포트 번호입니다.
* **보안:** (문자열 또는 부울) 서비스 URL에 사용할 프로토콜을 결정합니다.

   * 자동: //
   * true: https://
   * false: https://

#### getServiceURL(resolve) {#getserviceurl-resolve}

JSONP 서비스의 URL을 검색합니다.

**매개변수**

* **해결:** (부울) URL에 해결된 매개 변수를 포함할지 여부를 결정합니다. 값 `true` 매개 변수 확인 및 `false` 그렇지 않습니다.

**반환**

A `string` 서비스 URL을 나타내는 값입니다.

#### init(name, config) {#init-name-config-1}

는 ContextHub.Store.JSONPtore 개체를 초기화합니다.

**매개변수**

* **이름:** (문자열) 저장소의 이름입니다.
* **구성:** (객체) 서비스 속성을 포함하는 객체입니다. JSONPtore 개체는 `service` jsonp 서비스의 URL을 구성하는 개체:

   * eventDefering: 32.
   * 이벤트: 이 저장소의 ContextHub.Utils.Eventing 개체입니다. 기본값은 입니다 `ContextHub.eventing` 개체.
   * 지속성: 이 저장소의 ContextHub.Utils.Persistence 개체입니다. 기본적으로 메모리 지속성이 사용됩니다(JavaScript 개체).
   * service: (객체)

      * host: (문자열) 서버 이름 또는 IP 주소입니다.
      * jsonp: (부울) 값이 true 이면 서비스가 JSONP 서비스이고 그렇지 않으면 false 입니다. true인 경우 `{callback: "ContextHub.Callbacks.*Object.name*}`개체가 추가됨 `service.params`.
      * params: (오브젝트) 오브젝트 속성으로 표시되는 URL 매개 변수입니다. 매개 변수 이름과 값은 각각 개체 속성 이름과 값입니다.
      * path: (문자열) 서비스 경로입니다.
      * port: (숫자) 서비스의 포트 번호입니다.
      * secure: (문자열 또는 부울) 서비스 URL에 사용할 프로토콜을 결정합니다.

         * 자동: //
         * true: https://
         * false: https://

      * timeout: (숫자) 시간 초과 전에 JSONP 서비스가 응답할 때까지 대기하는 시간(밀리초)입니다.
      * ttl: JSONP 서비스 호출 사이에 경과되는 최소 시간(밀리초)입니다. (다음을 참조하십시오. [queryService](/help/sites-developing/contexthub-api.md#queryservice-reload) 함수).

#### queryService(다시 로드) {#queryservice-reload}

원격 JSONP 서비스를 쿼리하고 응답을 캐시합니다. 이 함수에 대한 이전 호출 이후의 시간이 값보다 작은 경우 `config.service.ttl`, 서비스가 호출되지 않으며 캐시된 응답이 변경되지 않습니다. 선택적으로 서비스를 강제로 호출할 수 있습니다. 다음 `config.service.ttl`속성은 를 호출할 때 설정됩니다. [init](/help/sites-developing/contexthub-api.md#init-name-config) 저장소를 초기화하는 함수입니다.

쿼리가 완료되면 준비 이벤트를 트리거합니다. JSONP 서비스 URL이 설정되지 않은 경우 함수는 아무 작업도 하지 않습니다.

**매개변수**

* **다시 로드:** (부울) 값이 true 이면 캐시된 응답이 제거되고 JSONP 서비스가 호출됩니다.

#### 재설정 {#reset}

저장소의 지속 데이터의 초기 값을 재설정한 다음 JSONP 서비스를 호출합니다. 선택적으로 저장소에서 다른 모든 데이터를 제거할 수 있습니다. 초기값이 재설정되는 동안 이 저장소에 대한 이벤트가 일시 중지되었습니다. 이 함수는 값을 반환하지 않습니다.

초기 값은 저장소 개체를 인스턴스화하는 데 사용되는 구성 개체의 initialValues 속성에 제공됩니다.

**매개변수**

* **keepRemainingData:** (부울) 값이 true 로 설정되면 초기 데이터가 아닌 데이터가 지속됩니다. false 값을 지정하면 초기 값을 제외한 모든 데이터가 제거됩니다.

#### resolveParameter(f) {#resolveparameter-f}

지정된 매개 변수를 확인합니다.

## ContextHub.Store.PersistedJSONPStore {#contexthub-store-persistedjsonpstore}

ContextHub.Store.PersistedJSONPtore 확장 [ContextHub.Store.JSONPtore](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore) 그래서 그것은 그 클래스의 모든 기능을 상속합니다. 그러나 JSONP 서비스에서 검색하는 데이터는 ContextHub 지속성 구성에 따라 지속됩니다. (참조: [지속성 모드](/help/sites-developing/ch-adding.md#persistence-modes).)

## ContextHub.Store.PersistedStore {#contexthub-store-persistedstore}

ContextHub.Store.PersistedStore 확장 [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) 그래서 그것은 그 클래스의 모든 기능을 상속합니다. 이 저장소의 데이터는 ContextHub 지속성 구성에 따라 유지됩니다.

## ContextHub.Store.SessionStore {#contexthub-store-sessionstore}

ContextHub.Store.SessionStore 확장 [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) 그래서 그것은 그 클래스의 모든 기능을 상속합니다. 이 저장소의 데이터는 메모리 내 지속성(JavaScript 개체)을 사용하여 유지됩니다.

## ContextHub.UI {#contexthub-ui}

UI 모듈 및 UI 모듈 렌더러를 관리합니다.

### 함수(ContextHub.UI) {#functions-contexthub-ui}

#### registerRenderer(moduleType, renderer, dontRender) {#registerrenderer-moduletype-renderer-dontrender}

UI 모듈 렌더러를 ContextHub에 등록합니다. 렌더러가 등록된 후에는 다음 작업을 수행할 수 있습니다. [ui 모듈 만들기](ch-configuring.md#adding-a-ui-module). 다음과 같은 경우 이 함수 사용 [ContextHub.UI.BaseModuleRenderer 확장](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types) 사용자 지정 UI 모듈 렌더러를 만듭니다.

**매개변수**

* **모듈 유형:** (문자열) UI 모듈 렌더러의 식별자입니다. 렌더러가 이미 지정된 값을 사용하여 등록된 경우, 이 렌더러가 등록되기 전에 기존 렌더러가 등록 취소되었습니다.
* **렌더러:** (문자열) UI 모듈을 렌더링하는 클래스의 이름입니다.
* **dontRender:** (부울) 로 설정 `true` 렌더러가 등록된 후 ContextHub UI가 렌더링되지 않도록 합니다. 기본값은 `false`입니다.

**예**

다음 예제에서는 렌더러를 contexthub.browserinfo 모듈 유형으로 등록합니다.

```
ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());
```

## ContextHub.Utils.Cookie {#contexthub-utils-cookie}

쿠키와 상호 작용하기 위한 유틸리티 클래스.

### 함수 (ContextHub.Utils.Cookie) {#functions-contexthub-utils-cookie}

#### 존재함(키) {#exists-key}

쿠키가 존재하는지 여부를 결정합니다.

**매개변수**

* **키:** A `String` 에는 테스트 중인 쿠키의 키가 포함되어 있습니다.

**반환**

A `boolean` 값이 true이면 쿠키가 있음을 나타냅니다.

**예**

```
if (ContextHub.Utils.Cookie.exists("name")) {
   // conditionally-executed code
}
```

#### getAllItems(filter) {#getallitems-filter}

필터와 일치하는 키가 있는 모든 쿠키를 반환합니다.

**매개변수**

* (선택 사항) **필터:** 일치하는 쿠키 키에 대한 기준. 모든 쿠키를 반환하려면 값을 지정하지 마십시오. 지원되는 유형은 다음과 같습니다.

   * 문자열: 문자열은 쿠키 키와 비교됩니다.
   * 배열: 배열의 각 항목은 필터입니다.
   * RegExp 개체: 개체의 테스트 함수는 쿠키 키를 일치시키는 데 사용됩니다.
   * 함수: 일치 항목에 대한 쿠키 키를 테스트하는 함수입니다. 함수는 쿠키 키를 매개 변수로 사용하고, 테스트에서 일치하는 것이 확인되면 true를 반환해야 합니다.

**반환**

쿠키의 개체입니다. 개체 속성은 쿠키 키이고 키 값은 쿠키 값입니다.

**예**

```
ContextHub.Utils.Cookie.getAllItems([/^cq-authoring/, /^cq-editor/])
```

#### getItem(key) {#getitem-key-1}

쿠키 값을 반환합니다.

**매개변수**

* **키:** 값을 원하는 쿠키의 키입니다.

**반환**

쿠키 값 또는 `null` 키에 대한 쿠키가 없는 경우.

**예**

```
ContextHub.Utils.Cookie.getItem("name");
```

#### getKeys(filter) {#getkeys-filter}

필터와 일치하는 기존 쿠키의 배열을 반환합니다.

**매개변수**

* **필터:** 일치하는 쿠키 키에 대한 기준. 지원되는 유형은 다음과 같습니다.

   * 문자열: 문자열은 쿠키 키와 비교됩니다.
   * 배열: 배열의 각 항목은 필터입니다.
   * RegExp 개체: 개체의 테스트 함수는 쿠키 키를 일치시키는 데 사용됩니다.
   * 함수: 일치 항목에 대한 쿠키 키를 테스트하는 함수입니다. 함수는 쿠키 키를 매개 변수로 가져와서 반환해야 합니다. `true` 일치가 테스트에서 확인된 경우.

**반환**

각 문자열이 필터와 일치하는 쿠키의 키인 문자열의 배열입니다.

**예**

```
ContextHub.Utils.Cookie.getKeys([/^cq-authoring/, /^cq-editor/])
```

#### removeItem(key, options) {#removeitem-key-options-1}

쿠키를 제거합니다. 쿠키를 제거하려면 값이 빈 문자열로 설정되고 만료 날짜는 현재 날짜의 전일로 설정됩니다.

**매개변수**

* **키:** A `String` 제거할 쿠키의 키를 나타내는 값입니다.

* **옵션:** 쿠키 속성을 구성하기 위한 속성 값을 포함하는 객체입니다. 다음을 참조하십시오. ` [setItem](/help/sites-developing/contexthub-api.md#setitem-key-value-options)` 함수 를 참조하십시오. 다음 `expires` 속성은 영향을 주지 않습니다.

**반환**

이 함수는 값을 반환하지 않습니다.

**예**

```
ContextHub.Utils.Cookie.vanish([/^cq-authoring/, 'cq-scrollpos']);
```

#### setItem(키, 값, 옵션) {#setitem-key-value-options-1}

지정된 키 및 값의 쿠키를 만들고 현재 문서에 쿠키를 추가합니다. 선택적으로 쿠키의 속성을 구성하는 옵션을 지정할 수 있습니다.

**매개변수**

* **키:** 쿠키의 키를 포함하는 문자열입니다.
* **값:** 쿠키 값을 포함하는 문자열입니다.
* **옵션:** (선택 사항) 쿠키 속성을 구성하는 다음 속성 중 하나가 포함된 객체입니다.

   * 만료: A `date` 또는 `number` 쿠키가 만료되는 시기를 지정하는 값입니다. 날짜 값은 절대 만료 시간을 지정합니다. 숫자(일)는 만료 시간을 현재 시간과 숫자를 더한 값으로 설정합니다. 기본값은 `undefined`입니다.
   * 보안: A `boolean` 을 지정하는 값 `Secure` 쿠키의 특성입니다. 기본값은 `false`입니다.
   * 경로: A `String` 로 사용할 값 `Path` 쿠키의 특성입니다. 기본값은 `undefined`입니다.

**반환**

설정된 값이 있는 쿠키입니다.

**예**

```
ContextHub.Utils.Cookie.setItem("name", "mycookie", {
    expires: 3,
    domain: 'localhost',
    path: '/some/directory',
    secure: true
});
```

#### 단축(필터, 옵션) {#vanish-filter-options}

지정된 필터와 일치하는 모든 쿠키를 제거합니다. 쿠키는 getKeys 함수를 사용하여 일치되고 removeItem 함수를 사용하여 제거됩니다.

**매개변수**

* **필터:** 다음 `filter` 호출에 사용할 인수 `[getKeys](/help/sites-developing/contexthub-api.md#getkeys-filter)` 함수.

* **옵션:** 다음 `options` 호출에 사용할 인수 `[removeItem](/help/sites-developing/contexthub-api.md#removeitem-key-options)` 함수.

**반환**

이 함수는 값을 반환하지 않습니다.

## ContextHub.Utils.Eventing {#contexthub-utils-eventing}

ContextHub 저장소 이벤트에 함수를 바인딩 및 바인딩 해제할 수 있습니다. 를 사용하여 저장소의 ContextHub.Utils.Eventing 개체에 액세스 [이벤트](/help/sites-developing/contexthub-api.md#eventing) 스토어의 속성입니다.

### 함수(ContextHub.Utils.Eventing) {#functions-contexthub-utils-eventing}

#### off(name, selector) {#off-name-selector}

이벤트에서 함수의 바인딩을 해제합니다.

**매개변수**

* **이름:** 다음 [이벤트 이름](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) 에 대해 함수를 바인딩 해제합니다.

* **선택기:** 바인딩을 식별하는 선택기입니다. (다음을 참조하십시오. `selector` 매개 변수 [날짜](/help/sites-developing/contexthub-api.md#on-name-handler-selector-triggerforpastevents) 및 [한 번](/help/sites-developing/contexthub-api.md#once-name-handler-selector-triggerforpastevents) 함수)를 참조하십시오.

**반환**

이 함수는 값을 반환하지 않습니다.

#### on(name, handler, selector, triggerForPastEvents) {#on-name-handler-selector-triggerforpastevents}

함수를 이벤트에 바인딩합니다. 이 함수는 이벤트가 발생할 때마다 호출됩니다. 선택적으로, 바인딩이 설정되기 전에 과거에 발생한 이벤트에 대해 함수를 호출할 수 있습니다.

**매개변수**

* **이름:** (문자열) [이벤트 이름](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) 함수를 바인딩할 대상.

* **핸들러:** (함수) 이벤트에 바인딩할 함수입니다.
* **선택기:** (문자열) 바인딩에 대한 고유 식별자입니다. 를 사용하려면 선택기가 바인딩을 식별해야 합니다. `off` 바인딩을 제거하는 함수입니다.

* **triggerForPastEvents:** (부울) 과거에 발생한 이벤트에 대해 핸들러를 실행해야 하는지 여부를 나타냅니다. 값 `true` 이전 이벤트에 대한 핸들러를 호출합니다. 값 `false` 은(는) 다음 이벤트에 대해 핸들러를 호출합니다. 기본값은 `true`입니다.

**반환**

다음의 경우 `triggerForPastEvents` 인수: `true`, 이 함수는 `boolean` 이벤트가 과거에 발생했는지 여부를 나타내는 값:

* `true`: 이벤트가 과거에 발생했으며 핸들러가 호출됩니다.
* `false`: 이벤트가 과거 발생하지 않았습니다.

If `triggerForPastEvents` 은(는) `false`, 이 함수는 값을 반환하지 않습니다.

**예**

다음 예제에서는 함수를 geolocation 저장소의 데이터 이벤트에 바인딩합니다. 함수는 페이지의 요소를 저장소의 위도 데이터 항목에 대한 값으로 채웁니다.

```
<div class="location">
    <p>latitude: <span id="lat"></span></p>
</div>

<script>
    var geostore = ContextHub.getStore("geolocation");
    geostore.eventing.on(ContextHub.Constants.EVENT_DATA_UPDATE,getlat,"getlat");

    function getlat(){
       latitude = geostore.getItem("latitude");
       $("#lat").html(latitude);
    }
</script>
```

#### once(name, handler, selector, triggerForPastEvents) {#once-name-handler-selector-triggerforpastevents}

함수를 이벤트에 바인딩합니다. 함수는 이벤트의 첫 번째 발생에 대해 한 번만 호출됩니다. 선택적으로, 바인딩이 설정되기 전에 과거에 발생한 이벤트에 대해 함수를 호출할 수 있습니다.

**매개변수**

* **이름:** (문자열) [이벤트 이름](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) 함수를 바인딩할 대상.

* **핸들러:** (함수) 이벤트에 바인딩할 함수입니다.
* **선택기:** (문자열) 바인딩에 대한 고유 식별자입니다. 를 사용하려면 선택기가 바인딩을 식별해야 합니다. `off` 바인딩을 제거하는 함수입니다.

* **triggerForPastEvents:** (부울) 과거에 발생한 이벤트에 대해 핸들러를 실행해야 하는지 여부를 나타냅니다. 값 `true` 이전 이벤트에 대한 핸들러를 호출합니다. 값 `false` 은(는) 다음 이벤트에 대해 핸들러를 호출합니다. 기본값은 `true`입니다.

**반환**

다음의 경우 `triggerForPastEvents` 인수: `true`, 이 함수는 `boolean` 이벤트가 과거에 발생했는지 여부를 나타내는 값:

* `true`: 이벤트가 과거에 발생했으며 핸들러가 호출됩니다.
* `false`: 이벤트가 과거 발생하지 않았습니다.

If `triggerForPastEvents` 은(는) `false`, 이 함수는 값을 반환하지 않습니다.

## ContextHub.Utils.inheritance {#contexthub-utils-inheritance}

개체가 다른 개체의 속성과 메서드를 상속하도록 하는 유틸리티 클래스입니다.

### 함수(ContextHub.Utils.inheritance) {#functions-contexthub-utils-inheritance}

#### inherit(하위, 상위) {#inherit-child-parent}

개체가 다른 개체의 속성과 메서드를 상속하도록 합니다.

**매개변수**

* **하위:** (객체) 상속되는 객체입니다.
* **상위:** (객체) 상속된 속성 및 메서드를 정의하는 객체입니다.

## ContextHub.Utils.JSON {#contexthub-utils-json}

개체를 JSON 형식으로 serialize하고 JSON 문자열을 개체로 deserialize하는 함수를 제공합니다.

### 함수 (ContextHub.Utils.JSON) {#functions-contexthub-utils-json}

#### parse(data) {#parse-data}

문자열 값을 JSON으로 구문 분석하고 Javascript 개체로 변환합니다.

**매개변수**

* **데이터:** JSON 형식의 문자열 값입니다.

**반환**

JavaScript 개체.

**예**

코드 `ContextHub.Utils.JSON.parse("{'city':'Basel','country':'Switzerland','population':'173330'}");` 는 다음 개체를 반환합니다.

```
Object {
   city: "Basel",
   country: "Switzerland",
   population: 173330
}
```

#### stringify(data) {#stringify-data}

JavaScript 값 및 개체를 JSON 형식의 문자열 값으로 serialize합니다.

**매개변수**

* **데이터:** 직렬화할 값 또는 개체입니다. 이 함수는 부울, 배열, 숫자, 문자열 및 날짜 값을 지원합니다.

**반환**

직렬화된 문자열 값입니다. 날짜 `data` R임 `egExp` 값이 반환되면 이 함수는 빈 개체를 반환합니다. 날짜 `data` 는 함수이고, 를 반환합니다. `undefined`.

**예**

다음 코드는 를 반환합니다. `"{'city':'Basel','country':'Switzerland','population':'173330'}":`

```
ContextHub.Utils.JSON.stringify({
   city: "Basel",
   country: "Switzerland",
   population: 173330
});
```

## ContextHub.Utils.JSON.tree {#contexthub-utils-json-tree}

이 클래스를 사용하면 ContextHub 저장소에서 저장하거나 검색할 데이터 개체를 쉽게 조작할 수 있습니다.

### 함수 (ContextHub.Utils.JSON.tree) {#functions-contexthub-utils-json-tree}

#### addAllItems() {#addallitems}

데이터 개체의 복사본을 만들고 두 번째 개체의 데이터 트리에 추가합니다. 이 함수는 복사본을 반환하고 원본 개체 중 하나를 수정하지 않습니다. 두 개체의 데이터 트리가 동일한 키를 포함하면 두 번째 개체의 값이 첫 번째 개체의 값을 덮어씁니다.

**매개변수**

* **트리:** 복사되는 객체입니다.
* **두 번째 트리:** 의 복사본과 병합되는 개체 `tree` 개체.

**반환**

병합된 데이터가 포함된 객체입니다.

#### cleanup() {#cleanup}

개체의 복사본을 만들고 데이터 트리에서 값, null 값 또는 정의되지 않은 값이 없는 항목을 찾아서 제거한 다음 복사본을 반환합니다.

**매개변수**

* **트리:** 정리할 개체입니다.

**반환**

정리된 트리 사본.

#### getItem() {#getitem}

키에 대한 개체에서 값을 검색합니다.

**매개변수**

* **트리:** 데이터 개체입니다.
* **키:** 검색할 값에 대한 키입니다.

**반환**

키와 일치하는 값입니다. 키에 자식 키가 있으면 이 함수는 복잡한 개체를 반환합니다. 키 값의 유형이 다음과 같은 경우 `undefined`, `null` 가 반환됩니다.

**예**

다음 JavaScript 개체를 고려해 보십시오.

```
myObject {
  user: {
    location: {
      city: "Basel",
        details: {
          population: 173330,
          elevation: 260
        }
      }
    }
  }
```

다음 예제 코드는 값을 반환합니다 `260`:

```
ContextHub.Utils.JSON.tree.getItem(myObject, "/user/location/details/elevation");
```

다음 예제 코드는 하위 키가 있는 키의 값을 검색합니다.

```
ContextHub.Utils.JSON.tree.getItem(myObject, "/user");
```

이 함수는 다음 개체를 반환합니다.

```
Object {
  location: {
    city: "Basel",
    details: {
      population: 173330,
      elevation: 260
    }
  }
}
```

#### getKeys() {#getkeys}

개체의 데이터 트리에서 모든 키를 검색합니다. 선택적으로 특정 키의 하위 키만 검색할 수 있습니다. 선택적으로 검색된 키의 정렬 순서를 지정할 수도 있습니다.

**매개변수**

* **트리:** 데이터 트리의 키를 검색할 객체입니다.
* **상위:** (선택 사항) 데이터 트리에서 하위 항목의 키를 검색할 항목의 키입니다.
* **순서:** (선택 사항) 반환된 키의 정렬 순서를 결정하는 함수입니다. (참조: [Array.prototype.sort](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) Mozilla Developer Network에서)

**반환**

키 배열.

**예**

다음 객체를 고려하십시오.

```
myObject {
  location: {
    weather: {
      temperature: "28C",
      humidity: "77%",
      precipitation: "10%",
      wind: "8km/h"
    },
    city: "Basel",
    country: "Switzerland",
    longitude: 7.5925727,
    latitude: 47.557421
  }
}
```

다음 `ContextHub.Utils.JSON.tree.getKeys(myObject);` script는 다음 배열을 반환합니다.

```
["/location", "/location/city", "/location/country", "/location/latitude", "/location/longitude", "/location/weather", "/location/weather/humidity", "/location/weather/precipitation", "/location/weather/temperature", "/location/weather/wind"]
```

#### removeItem() {#removeitem}

지정된 객체의 복사본을 만들고 데이터 트리에서 지정된 분기를 제거한 다음 수정된 복사본을 반환합니다.

**매개변수**

* 트리: 데이터 개체.
* 키: 제거할 키입니다.

**반환**

키가 제거된 원본 데이터 개체의 사본입니다.

**예**

다음 객체를 고려하십시오.

```
myObject {
  one: {
    foo: "bar",
    two: {
      three: {
        four: {
          five: 5,
          six: 6
        }
      }
    }
  }
}
```

다음 예제 스크립트는 데이터 트리에서 /one/two/three/four 분기를 제거합니다.

```
myObject = ContextHub.Utils.JSON.tree.removeItem(myObject, "/one/two/three/four");
```

이 함수는 다음 개체를 반환합니다.

```
myObject {
  one: {
    foo: "bar"
  }
}
```

#### sanitizeKey(키) {#sanitizekey-key}

문자열 값을 정리하여 키로 사용할 수 있도록 합니다. 문자열을 정리하기 위해 이 함수는 다음 작업을 수행합니다.

* 여러 연속 슬래시를 하나의 슬래시로 줄입니다.
* 문자열의 시작과 끝에서 공백을 제거합니다.
* 결과를 슬래시로 구분된 문자열 배열로 분할합니다.

결과 배열을 사용하여 사용 가능한 키를 만듭니다.  **매개변수**

* **키:** 다음 `string` 소독을 위해.

**반환**

배열 `string` 각 문자열이 `key` 그것은 슬래시로 구분되었다. 정리된 키를 나타냅니다. 정리된 배열의 길이가 0이면 이 함수는 `null`.

**예**

다음 코드는 문자열을 삭제하여 배열을 생성합니다. `["this", "is", "a", "path"]`를 클릭한 다음 키를 생성합니다 `"/this/is/a/path"` 스토리지에서:

```
var key = " / this////is/a/path ";
ContextHub.Utils.JSON.tree.sanitizeKey(key)
"/" + ContextHub.Utils.JSON.tree.sanitizeKey(key).join("/");
```

#### setItem(트리, 키, 값) {#setitem-tree-key-value}

개체 사본의 데이터 트리에 키/값 쌍을 추가합니다. 데이터 트리에 대한 자세한 내용은 [지속성](/help/sites-developing/contexthub.md#persistence).

**매개변수**

* 트리: 데이터 개체.
* 키: 추가하려는 값과 연결할 키입니다. 키는 데이터 트리에 있는 항목에 대한 경로입니다. 이 함수 호출 `ContextHub.Utils.JSON.tree.sanitize` 키를 삭제하여 추가합니다.
* 값: 데이터 트리에 추가할 값입니다.

**반환**

사본 `tree` 을 포함하는 개체 `key`/ `value` 짝을 지어

**예**

다음 JavaScript 코드를 생각해 보십시오.

```
var myObject = {
     user: {
        location: {
           city: "Basel"
           }
        }
     };

var myKey = "/user/location/details";

var myValue = {
      population: 173330,
      elevation: 260
     };

myObject = ContextHub.Utils.JSON.tree.setItem(myObject, myKey, myValue);
```

myObject 개체에는 다음 값이 있습니다.

## ContextHub.Utils.storeCandidates {#contexthub-utils-storecandidates}

스토어 후보를 등록하고 등록된 스토어 후보를 가져올 수 있습니다.

### 함수(ContextHub.Utils.storeCandidates) {#functions-contexthub-utils-storecandidates}

#### getRegisteredCandidates(storeType) {#getregisteredcandidates-storetype}

저장소 후보로 등록된 저장소 유형을 반환합니다. 특정 저장소 유형 또는 모든 저장소 유형의 등록된 인증서를 검색합니다.

**매개변수**

* **스토어 유형:** (문자열) 저장소 유형의 이름입니다. 다음을 참조하십시오. `storeType` 매개 변수 [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#contexthub-utils-storecandidates) 함수.

**반환**

저장소 유형의 객체입니다. 객체 등록 정보는 저장소 유형 이름이고 등록 정보 값은 등록된 저장소 후보의 배열입니다.

#### getStoreFromCandidates(storeType) {#getstorefromcandidates-storetype}

등록된 후보에서 스토어 유형을 반환합니다. 같은 이름의 저장소 유형이 두 개 이상 등록되면 이 함수는 우선 순위가 가장 높은 저장소 유형을 반환합니다.

**매개변수**

* storeType: (문자열) 저장소 후보의 이름입니다. 다음을 참조하십시오. `storeType` 매개 변수 [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) 함수.

**반환**

등록된 저장소 후보를 나타내는 개체입니다. 요청한 스토어 유형이 등록되지 않으면 오류가 발생합니다.

#### getSupportedStoreTypes() {#getsupportedstoretypes}

저장소 후보로 등록된 저장소 유형의 이름을 반환합니다. 이 함수에는 매개 변수가 필요하지 않습니다.

**반환**

각 문자열이 저장소 후보가 등록된 storetype인 문자열 값의 배열입니다. 다음을 참조하십시오. `storeType` 매개 변수 [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#contexthub-utils-storecandidates) 함수.

#### registerStoreCandidate(store, storeType, priority, applies) {#registerstorecandidate-store-storetype-priority-applies}

저장소 개체를 이름 및 우선 순위를 사용하여 저장소 후보로 등록합니다.

우선 순위는 같은 이름의 매장의 중요성을 나타내는 숫자이다. 이미 등록된 점포 후보자와 동일한 명칭을 사용하여 점포 후보자를 등록한 경우, 우선순위가 더 높은 후보를 이용한다. 점포 후보 등록 시 동명이등록 점포 후보보다 우선순위가 높은 경우에만 점포를 등록한다.

**매개변수**

* **스토어:** (객체) 저장소 후보로 등록할 저장소 객체입니다.
* **스토어 유형:** (문자열) 저장소 후보의 이름입니다. 저장소 후보의 인스턴스를 만들 때 이 값이 필요합니다.
* **우선 순위:** (숫자) 저장소 후보의 우선 순위입니다.
* **적용:** (함수) 현재 환경에서 저장소의 적용 가능성을 평가하는 호출할 함수입니다. 함수는 를 반환해야 합니다. `true` 매장이 해당되면, `false` 그렇지 않으면. 기본값은 true를 반환하는 함수입니다. `function() {return true;}`

**예**

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandiate', 0);
```
