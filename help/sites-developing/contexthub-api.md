---
title: ContextHub Javascript API 참조
seo-title: ContextHub Javascript API 참조
description: ContextHub 구성 요소를 페이지에 추가하면 스크립트에서 ContextHub Javascript API를 사용할 수 있습니다
seo-description: ContextHub 구성 요소를 페이지에 추가하면 스크립트에서 ContextHub Javascript API를 사용할 수 있습니다
uuid: 296d6c8e-517f-4837-9e86-ae571ea8aa17
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 90605f41-1861-4891-a7c8-b8b5918cd5c6
feature: Context Hub
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '5031'
ht-degree: 1%

---


# ContextHub Javascript API 참조{#contexthub-javascript-api-reference}

ContextHub Javascript API는 [ContextHub 구성 요소가 페이지](/help/sites-developing/ch-adding.md#adding-contexthub-to-a-page-component)에 추가된 경우 스크립트에서 사용할 수 있습니다.

## ContextHub 상수 {#contexthub-constants}

ContextHub Javascript API가 정의하는 상수 값입니다.

### 이벤트 상수 {#event-constants}

다음 표는 ContextHub 저장소에 대해 발생하는 이벤트 이름을 나열합니다. [ContextHub.Utils.Events](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing)도 참조하십시오.

| 상수 | 설명 | 값 |
|---|---|---|
| ContextHub.Constants.EVENT_NAMESPACE | ContextHub의 이벤트 네임스페이스 | ch |
| ContextHub.Constants.EVENT_ALL_STORES_READY | 모든 필수 스토어가 등록, 초기화 및 사용될 준비가 되었음을 나타냅니다. | 모든 상점들 준비 |
| ContextHub.Constants.EVENT_STORES_PARTIALLY_READY | 지정된 시간 제한 내에 일부 스토어가 초기화되지 않았음을 나타냅니다. | 상점들 부분적으로 준비 |
| ContextHub.Constants.EVENT_STORE_REGISTERED | 스토어가 등록될 때 실행됩니다. | 스토어 등록 |
| ContextHub.Constants.EVENT_STORE_READY | 스토어가 작업 준비가 되었음을 나타냅니다. 데이터를 가져올 때 실행되는 JSONP 스토어를 제외하고 등록 후 바로 트리거됩니다. | 저장 가능 |
| ContextHub.Constants.EVENT_STORE_UPDATED | 스토어에서 지속성을 업데이트할 때 실행됩니다. | store-updated |
| ContextHub.Constants.PERSISTENCE_CONTAINER_NAME | 지속성 컨테이너 이름 | ContextHubPersistence |
| ContextHub.Constants.SERVICE_RAW_RESPONSE_KEY | 원시 JSON 결과가 저장되는 특정 지속성 키 이름을 저장합니다. | /_/원시 응답 |
| ContextHub.Constants.SERVICE_RESPONSE_TIME_KEY | JSON 데이터를 가져올 시점을 나타내는 특정 타임스탬프를 저장합니다. | /_/response-time |
| ContextHub.Constants.SERVICE_LAST_URL_KEY | 마지막 호출 동안 사용된 JSON 서비스의 특정 url을 저장합니다. | /_/url |
| ContextHub.Constants.IS_CONTAINER_EXPANDED | ContextHub의 UI가 확장되었는지 여부를 나타냅니다. | /_/container-expanded |

### UI 이벤트 상수 {#ui-event-constants}

다음 표는 ContextHub UI에 대해 발생하는 이벤트 이름을 나열합니다.

| **상수** | **설명** | **값** |
|---|---|---|
| ContextHub.Constants.EVENT_UI_MODE_REGISTERED | 모드가 등록되면 실행됩니다. | ui-mode-registered |
| ContextHub.Constants.EVENT_UI_MODE_UNREGISTERED | 모드가 등록되지 않은 경우 실행됩니다. | ui-mode-unregisted |
| ContextHub.Constants.EVENT_UI_MODE_RENDERER_REGISTERED | 모드 렌더러가 등록될 때 실행됩니다. | ui-mode-renderer-registered |
| ContextHub.Constants.EVENT_UI_MODE_RENDERER_UNREGISTERED | 모드 렌더러가 등록되지 않은 경우 실행됩니다. | ui-mode-renderer-unregisted |
| ContextHub.Constants.EVENT_UI_MODE_ADDED | 새 모드가 추가되면 실행됩니다. | ui-mode-added |
| ContextHub.Constants.EVENT_UI_MODE_REMOVED | 모드가 제거될 때 실행됩니다. | ui-mode-removed |
| ContextHub.Constants.EVENT_UI_MODE_SELECTED | 사용자가 모드를 선택할 때 실행됩니다. | ui-mode-selected |
| ContextHub.Constants.EVENT_UI_MODULE_REGISTERED | 새 모듈이 등록되면 실행됩니다. | ui-module-registered |
| ContextHub.Constants.EVENT_UI_MODULE_UNREGISTERED | 모듈이 등록되지 않은 경우 실행됩니다. | ui-module-unregistered |
| ContextHub.Constants.EVENT_UI_MODULE_RENDERER_REGISTERED | 모듈 렌더러가 등록될 때 실행됩니다. | ui-module-renderer-registered |
| ContextHub.Constants.EVENT_UI_MODULE_RENDERER_UNREGISTERED | 모듈 렌더러가 등록되지 않은 경우 실행됩니다. | ui-module-renderer-unregisted |
| ContextHub.Constants.EVENT_UI_MODULE_ADDED | 새 모듈이 추가되면 실행됩니다. | ui-module-added |
| ContextHub.Constants.EVENT_UI_MODULE_REMOVED | 모듈이 제거되면 실행됩니다. | ui-module-removed |
| ContextHub.Constants.EVENT_UI_CONTAINER_ADDED | UI 컨테이너가 페이지에 추가되면 실행됩니다 | ui-container-added |
| ContextHub.Constants.EVENT_UI_CONTAINER_OPENED | ContextHub UI를 열 때 실행됩니다. | ui-container-opened |
| ContextHub.Constants.EVENT_UI_CONTAINER_CLOSED | ContextHub UI가 축소될 때 실행됩니다. | ui-container-closed |
| ContextHub.Constants.EVENT_UI_PROPERTY_MODIFIED | 속성이 수정될 때 실행됩니다. | ui-property-modified |
| ContextHub.Constants.EVENT_UI_RENDERED | ContextHub UI가 렌더링될 때마다(예: 속성 변경 후) 실행됩니다. | ui가 렌더링됨 |
| ContextHub.Constants.EVENT_UI_INITIALIZED | UI 컨테이너가 초기화될 때 실행됩니다. | ui 초기화 |
| ContextHub.Constants.ACTIVE_UI_MODE | 활성 UI 모드를 나타냅니다. | /_/active-ui-mode |

## ContextHub Javascript API 참조 {#contexthub-javascript-api-reference-2}

ContextHub 개체는 모든 스토어에 대한 액세스를 제공합니다.

### 함수(ContextHub) {#functions-contexthub}

#### getAllStores() {#getallstores}

등록된 모든 ContextHub 저장소를 반환합니다.

이 함수에는 매개 변수가 없습니다.

**반환**

모든 ContextHub 스토어를 포함하는 객체입니다. 각 스토어는 스토어와 동일한 이름을 사용하는 객체입니다.

**예**

다음 예제에서는 모든 스토어를 검색한 다음 위치 정보 스토어를 검색합니다.

```
var allStores = ContextHub.getAllStores();
var geoloc = allStores.geolocation
```

#### getStore(name) {#getstore-name}

스토어를 Javascript 객체로 검색합니다.

**매개 변수**

* **name:** 스토어가 등록된 이름입니다.

**반환**

스토어를 나타내는 객체입니다.

**예**

다음 예제에서는 지리적 위치 저장소를 검색합니다.

```
var geoloc = ContextHub.getStore("geolocation");
```

## ContextHub.SegmentEngine.Segment {#contexthub-segmentengine-segment}

ContextHub 세그먼트를 나타냅니다. ContextHub.SegmentEngine.SegmentManager를 사용하여 세그먼트를 가져옵니다.

### 함수(ContextHub.ContextEngine.Segment) {#functions-contexthub-contextengine-segment}

#### getName() {#getname}

세그먼트의 이름을 문자열 값으로 반환합니다.

#### getPath() {#getpath}

세그먼트 정의의 저장소 경로를 문자열 값으로 반환합니다.

## ContextHub.SegmentEngine.SegmentManager {#contexthub-segmentengine-segmentmanager}

ContextHub 세그먼트에 대한 액세스 권한을 제공합니다.

### 함수(ContextHub.SegmentEngine.SegmentManager) {#functions-contexthub-segmentengine-segmentmanager}

#### getResolvedSegments() {#getresolvedsegments}

현재 컨텍스트에서 해결된 세그먼트를 반환합니다. 이 함수에는 매개 변수가 없습니다.

**반환**

ContextHub.SegmentEngine.Segment 객체의 배열입니다.

## ContextHub.Store.Core {#contexthub-store-core}

ContextHub 저장소의 기본 클래스입니다.

### 속성(ContextHub.Store.Core) {#properties-contexthub-store-core}

#### 이벤트 {#eventing}

[ContextHub.Utils.Events](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) 개체. 이벤트를 저장하기 위해 바인딩 함수에 이 개체를 사용합니다. 기본값 및 초기화에 대한 자세한 내용은 [init(name,config)](/help/sites-developing/contexthub-api.md#init-name-config)을 참조하십시오.

#### 이름 {#name}

스토어의 이름입니다.

#### 지속성 {#persistence}

ContextHub.Utils.Persistence 객체입니다. 기본값 및 초기화에 대한 자세한 내용은 `[init(name,config)](/help/sites-developing/contexthub-api.md#init-name-config).`

### 함수(ContextHub.Store.Core) {#functions-contexthub-store-core}

#### addAllItems(tree, options) {#addallitems-tree-options}

데이터 객체 또는 배열을 저장소 데이터와 병합합니다. 개체나 배열의 각 키/값 쌍이 스토어에 추가됩니다(A0/> 함수를 통해).`setItem`

* **개체:** 키는 속성 이름입니다.
* **배열:** 키는 배열 인덱스입니다.

값은 객체일 수 있습니다.

**매개 변수**

* **tree:** (Object 또는 array) 스토어에 추가할 데이터입니다.
* **options:** (Object) setItem 함수에 전달되는 옵션 객체입니다. 자세한 내용은 [setItem(key,value,options)](/help/sites-developing/contexthub-api.md#setitem-key-value-options)의 `options` 매개 변수를 참조하십시오.

**반환**

`boolean` 값:

* `true` 값은 데이터 객체가 저장되었음을 나타냅니다.
* `false` 값은 데이터 저장소가 변경되지 않음을 나타냅니다.

#### addReference(key, anotherKey) {#addreference-key-anotherkey}

한 키에서 다른 키로 참조를 만듭니다. 키는 자신을 참조할 수 없습니다.

**매개 변수**

* **키:** 참조하는 키 `anotherKey`.

* **다른 키:** 이 참조하는 키 `key`입니다.

**반환**

`boolean` 값:

* `true` 값은 참조가 추가되었음을 나타냅니다.
* `false` 값은 추가된 참조가 없음을 나타냅니다.

#### announceReady() {#announcereadiness}

이 스토어에 대해 `ready` 이벤트를 트리거합니다. 이 함수에는 매개 변수가 없고 값이 없습니다.

#### clean() {#clean}

저장소에서 모든 데이터를 제거합니다. 함수에 매개 변수가 없고 반환 값이 없습니다.

#### getItem(key) {#getitem-key}

키와 연관된 값을 반환합니다.

**매개 변수**

* **key:** (String) 값을 반환할 키

**반환**

키의 값을 나타내는 객체입니다.

#### getKeys(includeInternals) {#getkeys-includeinternals}

스토어에서 키를 검색합니다. 선택적으로 ContextHub 프레임워크에서 내부적으로 사용되는 키를 검색할 수 있습니다.

**매개 변수**

* **includeInternals:** 내부적으로  `true` 사용하는 키를 결과에 포함하는 값입니다. 이러한 키는 밑줄(&quot;_&quot;) 문자로 시작합니다. 기본값은 `false`입니다.

**반환**

키 이름의 배열( `string` 값).

#### getReferences() {#getreferences}

스토어에서 참조를 검색합니다.

**반환**

참조하는 키를 참조된 키에 대한 인덱스로 사용하는 배열입니다.

* 참조하는 키는 `addReference` 함수의 `key` 매개 변수와 일치합니다.

* 참조된 키는 `addReference` 함수의 `anotherKey` 매개 변수에 해당합니다.

#### getTree(includeInternals) {#gettree-includeinternals}

저장소에서 데이터 트리를 검색합니다. 선택적으로 ContextHub 프레임워크에서 내부적으로 사용하는 키/값 쌍을 포함할 수 있습니다.

**매개 변수**

* `includeInternals:` 값은 내부적으로  `true` 사용한 키/값 쌍을 결과에 포함합니다. 이 데이터의 키는 밑줄(&quot;_&quot;) 문자로 시작합니다. 기본값은 `false`입니다.

**반환**

데이터 트리를 나타내는 객체입니다. 키는 객체의 속성 이름입니다.

#### init(name, config) {#init-name-config}

스토어를 초기화합니다.

* 저장소 데이터를 빈 개체로 설정합니다.
* 저장소 참조를 빈 개체에 설정합니다.
* eventChannel은 data:*name*&#x200B;이고 여기서 *name*&#x200B;은 스토어 이름입니다.

* storeDataKey는 /store/*name*&#x200B;이며 여기서 *name*&#x200B;은 스토어 이름입니다.

**매개 변수**

* **이름:** 스토어의 이름입니다.
* **config:** 구성 속성을 포함하는 객체입니다.

   * eventDeferring:기본값은 32입니다.
   * 이벤트:이 스토어에 대한 [ContextHub.Utils.Events](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) 개체. 기본값은 ContextHub.events 객체가 사용하는 ContextHub.events 객체입니다.
   * 지속성:이 저장소의 ContextHub.Utils.Persistence 객체입니다. 기본값은 ContextHub.persistence 객체입니다.

#### isEventsPaused() {#iseventingpaused}

이 스토어에 대해 이벤트가 일시 중지되었는지 여부를 결정합니다.

**반환**

부울 값:

* `true`:이 스토어에 대한 이벤트가 트리거되지 않도록 이벤트가 일시 중지됩니다.
* `false`:이벤트가 일시 중지되지 않아 이 스토어에 대해 이벤트가 트리거됩니다.

#### pauseEvents() {#pauseeventing}

이벤트가 트리거되지 않도록 스토어에 대한 이벤트를 일시 중지합니다. 이 함수에는 매개 변수가 필요하지 않으며 값이 없습니다.

#### removeItem(key, options) {#removeitem-key-options}

저장소에서 키/값 쌍을 제거합니다.

키가 제거되면 이 함수는 `data` 이벤트를 트리거합니다. 이벤트 데이터에는 스토어 이름, 제거된 키 이름, 제거된 값, 키의 새 값(null) 및 &quot;제거&quot;의 작업 유형이 포함됩니다.

원할 경우, `data` 이벤트의 트리거를 방지할 수 있습니다.

**매개 변수**

* **key:** (문자열) 제거할 키의 이름입니다.
* **options:** (개체) 옵션 객체입니다. 다음 개체 속성이 유효합니다.

   * silent:`true`의 값은 `data` 이벤트의 트리거를 방지합니다. 기본값은 `false`입니다.

**반환**

`boolean` 값:

* `true` 값은 키/값 쌍이 제거되었음을 나타냅니다.
* `false` 값은 키가 저장소에서 없으므로 데이터 저장소가 변경되지 않음을 나타냅니다.

#### removeReference(key) {#removereference-key}

스토어에서 참조를 제거합니다.

**매개 변수**

* **키:** 제거할 키 참조입니다. 이 매개 변수는 `addReference` 함수의 `key` 매개 변수와 일치합니다.

**반환**

`boolean` 값:

* `true` 값은 참조가 제거되었음을 나타냅니다.
* `false` 값은 키가 유효하지 않으며 스토어가 변경되지 않음을 나타냅니다.

#### reset(keepRemainingData) {#reset-keepremainingdata}

스토어의 지속적인 데이터의 초기 값을 재설정합니다. 선택적으로 저장소에서 다른 모든 데이터를 제거할 수 있습니다. 스토어를 재설정하는 동안 이 스토어에 대한 이벤트가 일시 중지되었습니다. 이 함수는 값을 반환하지 않습니다.

초기 값은 저장소 개체를 인스턴스화하는 데 사용되는 구성 개체의 initialValues 속성에 제공됩니다.

**매개 변수**

* **keepRemainingData:** (Boolean) true 값을 설정하면 초기 데이터가 아닌 데이터가 지속됩니다. false 값을 지정하면 초기 값을 제외한 모든 데이터가 제거됩니다.

스토어의 지속적인 데이터의 초기 값을 재설정합니다. 선택적으로 저장소에서 다른 모든 데이터를 제거할 수 있습니다. 스토어를 재설정하는 동안 이 스토어에 대한 이벤트가 일시 중지되었습니다. 이 함수는 값을 반환하지 않습니다.

초기 값은 저장소 개체를 인스턴스화하는 데 사용되는 구성 개체의 initialValues 속성에 제공됩니다.

**매개 변수**

* keepRemainingData:(부울) true 값을 설정하면 초기 데이터가 아닌 데이터가 지속됩니다. false 값을 지정하면 초기 값을 제외한 모든 데이터가 제거됩니다.

#### resolveReference(key, retry) {#resolvereference-key-retry}

참조된 키를 검색합니다. 최상의 일치 항목을 확인하는 데 사용할 반복 수를 지정할 수도 있습니다(선택 사항).

**매개 변수**

* **key:** (문자열) 참조를 확인할 키입니다. 이 `key` 매개 변수는 `addReference` 함수의 `key` 매개 변수와 일치합니다.

* **retry:** (Number) 사용할 반복 수입니다.

**반환**

참조된 키를 나타내는 `string` 값. 참조가 확인되지 않으면 `key` 매개 변수의 값이 반환됩니다.

#### resumeEventing() {#resumeeventing}

이벤트가 트리거되도록 이 스토어에 대한 이벤트를 다시 시작합니다. 이 함수는 매개 변수를 정의하지 않으며 값을 반환하지 않습니다.

#### setItem(key, value, options) {#setitem-key-value-options}

키/값 쌍을 스토어에 추가합니다.

키의 값이 현재 키에 저장된 값과 다른 경우에만 `data` 이벤트를 트리거합니다. 선택적으로 `data` 이벤트의 트리거를 방지할 수 있습니다.

이벤트 데이터에는 스토어 이름, 키, 이전 값, 새 값 및 `set` 작업 유형이 포함됩니다.

**매개 변수**

* **key:** (문자열) 키의 이름입니다.
* **options:** (개체) 옵션 객체입니다. 다음 개체 속성이 유효합니다.

   * silent:`true`의 값은 `data` 이벤트의 트리거를 방지합니다. 기본값은 `false`입니다.

* **value:** (Object) 키와 연결할 값입니다.

**반환**

`boolean` 값:

* `true` 값은 데이터 객체가 저장되었음을 나타냅니다.
* `false` 값은 데이터 저장소가 변경되지 않음을 나타냅니다.

## ContextHub.Store.JSONPStore {#contexthub-store-jsonpstore}

JSON 데이터가 포함된 스토어. 데이터는 외부 JSONP 서비스에서 또는 JSON 데이터를 반환하는 서비스에서 선택적으로 검색됩니다. 이 클래스의 인스턴스를 만들 때 [ `init`](/help/sites-developing/contexthub-api.md#init-name-config) 함수를 사용하여 서비스 세부 사항을 지정합니다.

저장소는 메모리 내 지속(Javascript 변수)을 사용합니다. 저장소 데이터는 페이지의 라이프타임 동안에만 사용할 수 있습니다.

ContextHub.Store.JSONPStore는 [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core)을(를) 확장하고 해당 클래스의 함수를 상속합니다.

### 함수(ContextHub.Store.JSONPStore) {#functions-contexthub-store-jsonpstore}

#### configureService(serviceConfig, override) {#configureservice-serviceconfig-override}

이 개체가 사용하는 JSONP 서비스에 연결하기 위한 세부 사항을 구성합니다. 기존 구성을 업데이트하거나 바꿀 수 있습니다. 이 함수는 값을 반환하지 않습니다.

**매개 변수**

* **serviceConfig:** 다음 속성을 포함하는 객체입니다.

   * 호스트:(문자열) 서버 이름 또는 IP 주소입니다.
   * jsonp:(부울) true 값은 서비스가 JSONP 서비스임을 나타내고, 그렇지 않으면 false를 반환합니다. true이면 {callback:&quot;ContextHub.Callback.*Object.name*} 개체는 service.params 개체에 추가됩니다.
   * params:(개체) 개체 속성으로 표시되는 URL 매개 변수입니다. 매개 변수 이름은 속성 이름이고 매개 변수 값은 속성 값입니다.
   * 경로:(문자열) 서비스의 경로입니다.
   * 포트:(번호) 서비스의 포트 번호입니다.
   * 보안:(문자열 또는 부울) 서비스 URL에 사용할 프로토콜을 결정합니다.

      * auto: //
      * true:https://
      * false:https://

* **override:** (Boolean). 값이 `true`이면 기존 서비스 구성이 `serviceConfig`의 속성으로 대체됩니다. 값이 `false`이면 기존 서비스 구성 속성이 `serviceConfig`의 속성과 병합됩니다.

#### getRawResponse() {#getrawresponse}

JSONP 서비스에 대한 마지막 호출 이후에 캐시되는 원시 응답을 반환합니다. 함수에 매개 변수가 필요하지 않습니다.

**반환**

원시 응답을 나타내는 객체입니다.

#### getServiceDetails() {#getservicedetails}

이 ContextHub.Store.JSONPStore 개체의 서비스 개체를 검색합니다. 서비스 객체에는 서비스 URL을 만드는 데 필요한 모든 정보가 포함됩니다.

**반환**

다음 속성을 갖는 개체:

* **host:** (문자열) 서버 이름 또는 IP 주소입니다.
* **jsonp:** (Boolean) true 값은 서비스가 JSONP 서비스임을 나타내고, 그렇지 않으면 false를 반환합니다. true이면 {callback:&quot;ContextHub.Callback.*Object.name*} 개체는 service.params 개체에 추가됩니다.

* **params:** (Object) 개체 속성으로 표시되는 URL 매개 변수입니다. 매개 변수 이름은 속성 이름이고 매개 변수 값은 속성 값입니다.
* **path:** (문자열) 서비스의 경로입니다.
* **port:** (번호) 서비스의 포트 번호입니다.
* **secure:** (문자열 또는 부울) 서비스 URL에 사용할 프로토콜을 결정합니다.

   * 자동://
   * true:https://
   * false:https://

#### getServiceURL(resolve) {#getserviceurl-resolve}

JSONP 서비스의 URL을 검색합니다.

**매개 변수**

* **resolve:** (부울) URL에 해결된 매개 변수를 포함할지 여부를 결정합니다. `true`의 값은 매개 변수를 확인하며 `false`은(는) 그렇지 않습니다.

**반환**

서비스 URL을 나타내는 `string` 값.

#### init(name, config) {#init-name-config-1}

ContextHub.Store.JSONPStore 개체를 초기화합니다.

**매개 변수**

* **name:** (문자열) 스토어의 이름입니다.
* **config:** (Object) 서비스 속성을 포함하는 객체입니다. JSONPStore 객체는 `service` 객체의 속성을 사용하여 JSONP 서비스의 URL을 구성합니다.

   * eventDeferring:32.
   * 이벤트:이 스토어에 대한 ContextHub.Utils.Eventing 객체입니다. 기본값은 `ContextHub.eventing` 객체입니다.
   * 지속성:이 저장소의 ContextHub.Utils.Persistence 객체입니다. 기본적으로 메모리 지속성(Javascript 객체)이 사용됩니다.
   * 서비스:(개체)

      * 호스트:(문자열) 서버 이름 또는 IP 주소입니다.
      * jsonp:(부울) true 값은 서비스가 JSONP 서비스임을 나타내고, 그렇지 않으면 false를 반환합니다. true이면 `{callback: "ContextHub.Callbacks.*Object.name*}`개체가 `service.params`에 추가됩니다.
      * params:(개체) 개체 속성으로 표시되는 URL 매개 변수입니다. 매개 변수 이름과 값은 각각 객체 속성 이름과 값입니다.
      * 경로:(문자열) 서비스의 경로입니다.
      * 포트:(번호) 서비스의 포트 번호입니다.
      * 보안:(문자열 또는 부울) 서비스 URL에 사용할 프로토콜을 결정합니다.

         * 자동://
         * true:https://
         * false:https://
      * timeout:(Number) 시간 초과 전에 JSONP 서비스가 응답할 때까지 기다리는 시간(밀리초)입니다.
      * ttl:JSONP 서비스에 대한 호출 사이에 전달되는 최소 시간(밀리초)입니다. ([queryService](/help/sites-developing/contexthub-api.md#queryservice-reload) 함수 참조).


#### queryService(다시 로드) {#queryservice-reload}

원격 JSONP 서비스를 쿼리하고 응답을 캐시합니다. 이 함수에 대한 이전 호출 이후의 시간이 `config.service.ttl` 값보다 작으면 서비스가 호출되지 않고 캐시된 응답이 변경되지 않습니다. 선택적으로 서비스를 강제로 호출할 수 있습니다. `config.service.ttl`속성은 [init](/help/sites-developing/contexthub-api.md#init-name-config) 함수를 호출하여 저장소를 초기화할 때 설정됩니다.

쿼리가 끝나면 준비 이벤트를 트리거합니다. JSONP 서비스 URL이 설정되지 않은 경우 이 함수는 아무 작업도 수행하지 않습니다.

**매개 변수**

* **reload:** (Boolean) true 값을 사용하면 캐시된 응답이 제거되고 JSONP 서비스가 호출되도록 합니다.

#### 재설정 {#reset}

스토어의 지속적인 데이터의 초기 값을 재설정한 다음 JSONP 서비스를 호출합니다. 선택적으로 저장소에서 다른 모든 데이터를 제거할 수 있습니다. 초기 값이 재설정되는 동안 이 스토어에 대한 이벤트가 일시 중지됩니다. 이 함수는 값을 반환하지 않습니다.

초기 값은 저장소 개체를 인스턴스화하는 데 사용되는 구성 개체의 initialValues 속성에 제공됩니다.

**매개 변수**

* **keepRemainingData:** (Boolean) true 값을 설정하면 초기 데이터가 아닌 데이터가 지속됩니다. false 값을 지정하면 초기 값을 제외한 모든 데이터가 제거됩니다.

#### resolveParameter(f) {#resolveparameter-f}

지정된 매개 변수를 확인합니다.

## ContextHub.Store.PersistentJSONPStore {#contexthub-store-persistedjsonpstore}

ContextHub.Store.PersistentJSONPStore는 [ContextHub.Store.JSONPStore](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore)을 확장하여 해당 클래스의 모든 함수를 상속합니다. 그러나 JSONP 서비스에서 검색된 데이터는 ContextHub 지속성 구성에 따라 유지됩니다. ([지속성 모드](/help/sites-developing/ch-adding.md#persistence-modes)를 참조하십시오.)

## ContextHub.Store.PersistentStore {#contexthub-store-persistedstore}

ContextHub.Store.PersistentStore는 [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core)을(를) 확장하여 해당 클래스의 모든 함수를 상속합니다. 이 저장소의 데이터는 ContextHub 지속성 구성에 따라 유지됩니다.

## ContextHub.Store.SessionStore {#contexthub-store-sessionstore}

ContextHub.Store.SessionStore는 [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core)을(를) 확장하여 해당 클래스의 모든 함수를 상속합니다. 이 저장소의 데이터는 메모리 내 지속(Javascript 개체)을 사용하여 지속됩니다.

## ContextHub.UI {#contexthub-ui}

UI 모듈 및 UI 모듈 렌더러를 관리합니다.

### 함수(ContextHub.UI) {#functions-contexthub-ui}

#### registerRenderer(moduleType, renderer, dontRender) {#registerrenderer-moduletype-renderer-dontrender}

ContextHub에 UI 모듈 렌더러를 등록합니다. 렌더러가 등록되면 [UI 모듈 만들기](ch-configuring.md#adding-a-ui-module)에 사용할 수 있습니다. 사용자 정의 UI 모듈 렌더러를 만들려면 [ContextHub.UI.BaseModuleRenderer](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types)를 확장할 때 이 함수를 사용합니다.

**매개 변수**

* **moduleType:** (String) UI 모듈 렌더러의 식별자입니다. 렌더러가 지정된 값을 사용하여 이미 등록된 경우 이 렌더러가 등록되기 전에 기존 렌더러가 등록되지 않습니다.
* **renderer:** (String) UI 모듈을 렌더링하는 클래스의 이름입니다.
* **dontRender:** (부울) 렌더러가  `true` 등록된 후 ContextHub UI가 렌더링되지 않도록 설정합니다. 기본값은 `false`입니다.

**예**

다음 예제에서는 렌더러를 contexthub.browserinfo 모듈 유형으로 등록합니다.

```
ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());
```

## ContextHub.Utils.Cookie {#contexthub-utils-cookie}

쿠키와 상호 작용하기 위한 유틸리티 클래스입니다.

### 함수(ContextHub.Utils.Cookie) {#functions-contexthub-utils-cookie}

#### exists(key) {#exists-key}

쿠키가 있는지 여부를 결정합니다.

**매개 변수**

* **키:** 테스트  `String` 중인 쿠키의 키가 포함된 키

**반환**

true의 `boolean` 값은 쿠키가 있음을 나타냅니다.

**예**

```
if (ContextHub.Utils.Cookie.exists("name")) {
   // conditionally-executed code
}
```

#### getAllItems(filter) {#getallitems-filter}

필터와 일치하는 키가 있는 모든 쿠키를 반환합니다.

**매개 변수**

* (선택 사항) **필터:** 쿠키 키 일치 기준. 모든 쿠키를 반환하려면 값을 지정하지 마십시오. 지원되는 유형은 다음과 같습니다.

   * 문자열:문자열은 쿠키 키와 비교됩니다.
   * 배열:배열의 각 항목은 필터입니다.
   * RegExp 객체:개체의 테스트 함수는 쿠키 키와 일치시키는 데 사용됩니다.
   * 함수:일치에 대한 쿠키 키를 테스트하는 함수입니다. 이 함수는 쿠키 키를 매개 변수로 가져와서 테스트가 일치를 확인하면 true를 반환해야 합니다.

**반환**

쿠키의 객체입니다. 개체 속성은 쿠키 키이고 키 값은 쿠키 값입니다.

**예**

```
ContextHub.Utils.Cookie.getAllItems([/^cq-authoring/, /^cq-editor/])
```

#### getItem(key) {#getitem-key-1}

쿠키 값을 반환합니다.

**매개 변수**

* **키:** 값이 필요한 쿠키의 키입니다.

**반환**

쿠키 값 또는 키에 대한 쿠키를 찾을 수 없는 경우 `null`.

**예**

```
ContextHub.Utils.Cookie.getItem("name");
```

#### getKeys(filter) {#getkeys-filter}

필터와 일치하는 기존 쿠키의 배열을 반환합니다.

**매개 변수**

* **필터:** 쿠키 키 일치를 위한 기준. 지원되는 유형은 다음과 같습니다.

   * 문자열:문자열은 쿠키 키와 비교됩니다.
   * 배열:배열의 각 항목은 필터입니다.
   * RegExp 객체:개체의 테스트 함수는 쿠키 키와 일치시키는 데 사용됩니다.
   * 함수:일치에 대한 쿠키 키를 테스트하는 함수입니다. 이 함수는 쿠키 키를 매개 변수로 가져와서 테스트가 일치를 확인하면 `true`을 반환해야 합니다.

**반환**

각 문자열이 필터와 일치하는 쿠키의 키인 문자열 배열입니다.

**예**

```
ContextHub.Utils.Cookie.getKeys([/^cq-authoring/, /^cq-editor/])
```

#### removeItem(key, options) {#removeitem-key-options-1}

쿠키를 제거합니다. 쿠키를 제거하려면 값이 포함 문자열로 설정되고 만료 날짜는 현재 날짜 전일로 설정됩니다.

**매개 변수**

* **키:** 제거할  `String` 쿠키의 키를 나타내는 값입니다.

* **옵션:** 쿠키 속성을 구성하기 위한 속성 값을 포함하는 객체입니다. 자세한 내용은 ` [setItem](/help/sites-developing/contexthub-api.md#setitem-key-value-options)` 함수를 참조하십시오. `expires` 속성은 효과가 없습니다.

**반환**

이 함수는 값을 반환하지 않습니다.

**예**

```
ContextHub.Utils.Cookie.vanish([/^cq-authoring/, 'cq-scrollpos']);
```

#### setItem(key, value, options) {#setitem-key-value-options-1}

주어진 키와 값의 쿠키를 만들고 현재 문서에 쿠키를 추가합니다. 선택적으로 쿠키의 속성을 구성하는 옵션을 지정할 수 있습니다.

**매개 변수**

* **키:** 쿠키의 키를 포함하는 문자열입니다.
* **값:** 쿠키 값을 포함하는 문자열입니다.
* **options:** (선택 사항) 쿠키 속성을 구성하는 다음 속성을 포함하는 객체입니다.

   * 만료:쿠키가 만료되는 시기를 지정하는 `date` 또는 `number` 값. 날짜 값은 절대 만료 시간을 지정합니다. 숫자(일 단위)는 만료 시간을 현재 시간 및 숫자로 설정합니다. 기본값은 `undefined`입니다.
   * 보안:쿠키의 `Secure` 특성을 지정하는 `boolean` 값. 기본값은 `false`입니다.
   * 경로:쿠키의 `Path` 특성으로 사용할 `String` 값입니다. 기본값은 `undefined`입니다.

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

#### disappear(filter, options) {#vanish-filter-options}

주어진 필터와 일치하는 모든 쿠키를 제거합니다. 쿠키는 getKeys 함수를 사용하여 일치하고 removeItem 함수를 사용하여 제거됩니다.

**매개 변수**

* **filter:** 함수  `filter` 호출에 사용할  `[getKeys](/help/sites-developing/contexthub-api.md#getkeys-filter)` 인수입니다.

* **options:** 함수  `options` 호출에 사용할  `[removeItem](/help/sites-developing/contexthub-api.md#removeitem-key-options)` 인수입니다.

**반환**

이 함수는 값을 반환하지 않습니다.

## ContextHub.Utils.Events {#contexthub-utils-eventing}

함수를 ContextHub 저장소 이벤트에 바인딩하고 바인딩 해제할 수 있습니다. 스토어의 [events](/help/sites-developing/contexthub-api.md#eventing) 속성을 사용하여 스토어에 대한 ContextHub.Utils.Events 개체에 액세스합니다.

### 함수(ContextHub.Utils.Events) {#functions-contexthub-utils-eventing}

#### off(name, selector) {#off-name-selector}

이벤트에서 함수를 바인딩하지 않습니다.

**매개 변수**

* **name:** 함수 [의 바인딩을 ](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) 해제할 이벤트의 이름입니다.

* **선택기:** 바인딩을 식별하는 선택기입니다. ([on](/help/sites-developing/contexthub-api.md#on-name-handler-selector-triggerforpastevents) 및 [once](/help/sites-developing/contexthub-api.md#once-name-handler-selector-triggerforpastevents) 함수의 `selector` 매개 변수를 참조하십시오.)

**반환**

이 함수는 값을 반환하지 않습니다.

#### on(name, handler, selector, triggerForPastEvents) {#on-name-handler-selector-triggerforpastevents}

함수를 이벤트에 바인딩합니다. 이 함수는 이벤트가 발생할 때마다 호출됩니다. 선택적으로, 바인딩이 설정되기 전에 이전에 발생한 이벤트에 대해 함수를 호출할 수 있습니다.

**매개 변수**

* **name:** (문자열) 함수를  [바인딩하](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) 는 이벤트의 이름입니다.

* **handler:** (함수) 이벤트에 바인딩할 함수입니다.
* **selector:** (문자열) 바인딩의 고유 식별자입니다. 바인딩을 제거하기 위해 `off` 함수를 사용하려면 선택기가 바인드를 식별해야 합니다.

* **triggerForPastEvents:** (Boolean) 과거에 발생한 이벤트에 대해 핸들러를 실행할지 여부를 나타냅니다. `true` 값은 이전 이벤트에 대한 핸들러를 호출합니다. `false` 값은 이후 이벤트에 대한 핸더를 호출합니다. 기본값은 `true`입니다.

**반환**

`triggerForPastEvents` 인수가 `true`이면 이 함수는 이벤트가 과거에 발생했는지 여부를 나타내는 `boolean` 값을 반환합니다.

* `true`:이전에 발생한 이벤트로 핸들러가 호출됩니다.
* `false`:이 이벤트는 과거에 발생하지 않았습니다.

`triggerForPastEvents`이 `false`이면 이 함수는 값을 반환하지 않습니다.

**예**

다음 예제에서는 함수를 지리적 위치 저장소의 데이터 이벤트에 바인딩합니다. 이 함수는 스토어의 위도 데이터 항목에 대한 값으로 페이지의 요소를 채웁니다.

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

함수를 이벤트에 바인딩합니다. 이 함수는 이벤트가 처음 발생할 때 한 번만 호출됩니다. 선택적으로, 바인딩이 설정되기 전에 과거에 발생한 이벤트에 대해 함수를 호출할 수 있습니다.

**매개 변수**

* **name:** (문자열) 함수를  [바인딩하](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) 는 이벤트의 이름입니다.

* **handler:** (함수) 이벤트에 바인딩할 함수입니다.
* **selector:** (문자열) 바인딩의 고유 식별자입니다. 바인딩을 제거하기 위해 `off` 함수를 사용하려면 선택기가 바인드를 식별해야 합니다.

* **triggerForPastEvents:** (Boolean) 과거에 발생한 이벤트에 대해 핸들러를 실행할지 여부를 나타냅니다. `true` 값은 이전 이벤트에 대한 핸들러를 호출합니다. `false` 값은 이후 이벤트에 대한 핸더를 호출합니다. 기본값은 `true`입니다.

**반환**

`triggerForPastEvents` 인수가 `true`이면 이 함수는 이벤트가 과거에 발생했는지 여부를 나타내는 `boolean` 값을 반환합니다.

* `true`:이전에 발생한 이벤트로 핸들러가 호출됩니다.
* `false`:이 이벤트는 과거에 발생하지 않았습니다.

`triggerForPastEvents`이 `false`이면 이 함수는 값을 반환하지 않습니다.

## ContextHub.Utils.inheritance {#contexthub-utils-inheritance}

객체가 다른 객체의 속성과 메서드를 상속할 수 있는 유틸리티 클래스입니다.

### 함수(ContextHub.Utils.inheritance) {#functions-contexthub-utils-inheritance}

#### inherit(child, parent) {#inherit-child-parent}

객체가 다른 객체의 속성과 메서드를 상속하도록 합니다.

**매개 변수**

* **child:** (Object) 상속하는 객체입니다.
* **parent:** (Object) 상속되는 속성과 메서드를 정의하는 객체입니다.

## ContextHub.Utils.JSON {#contexthub-utils-json}

개체를 JSON 형식으로 직렬화하고 JSON 문자열을 객체로 역직렬화하는 함수를 제공합니다.

### 함수(ContextHub.Utils.JSON) {#functions-contexthub-utils-json}

#### parse(data) {#parse-data}

문자열 값을 JSON으로 구문 분석하여 javascript 객체로 변환합니다.

**매개 변수**

* **data:** JSON 형식의 문자열 값입니다.

**반환**

Javascript 객체입니다.

**예**

`ContextHub.Utils.JSON.parse("{'city':'Basel','country':'Switzerland','population':'173330'}");` 코드는 다음 객체를 반환합니다.

```
Object {
   city: "Basel",
   country: "Switzerland",
   population: 173330
}
```

#### stringify(data) {#stringify-data}

Javascript 값과 개체를 JSON 형식의 문자열 값으로 정리합니다.

**매개 변수**

* **data:** serialize할 값 또는 객체입니다. 이 함수는 부울, 배열, 숫자, 문자열 및 날짜 값을 지원합니다.

**반환**

직렬화된 문자열 값입니다. `data`이 R `egExp` 값이면 이 함수는 빈 객체를 반환합니다. `data`이(가) 함수이면 `undefined`을 반환합니다.

**예**

다음 코드는 `"{'city':'Basel','country':'Switzerland','population':'173330'}":`을(를) 반환합니다.

```
ContextHub.Utils.JSON.stringify({
   city: "Basel",
   country: "Switzerland",
   population: 173330
});
```

## ContextHub.Utils.JSON.tree {#contexthub-utils-json-tree}

이 클래스는 저장되거나 ContextHub 저장소에서 검색되는 데이터 개체를 쉽게 조작합니다.

### 함수(ContextHub.Utils.JSON.tree) {#functions-contexthub-utils-json-tree}

#### addAllItems() {#addallitems}

데이터 개체의 복사본을 만들고 두 번째 개체의 데이터 트리에 추가합니다. 이 함수는 복사본을 반환하고 원본 객체 중 하나를 수정하지 않습니다. 두 개체의 데이터 트리에 동일한 키가 들어 있으면 두 번째 개체의 값이 첫 번째 개체의 값을 덮어씁니다.

**매개 변수**

* **트리:** 복사할 객체입니다.
* **secondTree:** 객체의 복사본과 병합되는  `tree` 객체입니다.

**반환**

병합된 데이터가 포함된 객체입니다.

#### cleanup() {#cleanup}

개체의 복사본을 만들고, 값, null 값 또는 정의되지 않은 값이 들어 있지 않은 데이터 트리의 항목을 찾거나 제거하고 복사본을 반환합니다.

**매개 변수**

* **트리:** 정리할 객체입니다.

**반환**

청소되는 나무 한 부입니다.

#### getItem() {#getitem}

키에 대한 개체에서 값을 검색합니다.

**매개 변수**

* **tree:** data 객체입니다.
* **키:** 검색할 값의 키입니다.

**반환**

키와 일치하는 값입니다. 키에 자식 키가 있으면 이 함수는 복잡한 객체를 반환합니다. 키의 값 유형이 `undefined`이면 `null`이 반환됩니다.

**예**

다음 Javascript 개체를 생각해 보십시오.

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

다음 예제 코드는 값 `260`을 반환합니다.

```
ContextHub.Utils.JSON.tree.getItem(myObject, "/user/location/details/elevation");
```

다음 예제 코드는 하위 키가 있는 키의 값을 검색합니다.

```
ContextHub.Utils.JSON.tree.getItem(myObject, "/user");
```

이 함수는 다음 객체를 반환합니다.

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

개체의 데이터 트리에서 모든 키를 검색합니다. 선택적으로 특정 키의 하위 키만 검색할 수 있습니다. 검색된 키의 정렬 순서를 선택적으로 지정할 수도 있습니다.

**매개 변수**

* **트리:** 데이터 트리의 키를 가져올 객체입니다.
* **parent:** (선택 사항) 자식 항목의 키를 검색할 데이터 트리의 항목 키
* **order:** (선택 사항) 반환된 키의 정렬 순서를 결정하는 함수입니다. (Mozilla Developer Network의 [Array.prototype.sort](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) 참조)

**반환**

키 배열입니다.

**예**

다음 개체를 생각해 보십시오.

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

`ContextHub.Utils.JSON.tree.getKeys(myObject);` 스크립트는 다음 배열을 반환합니다.

```
["/location", "/location/city", "/location/country", "/location/latitude", "/location/longitude", "/location/weather", "/location/weather/humidity", "/location/weather/precipitation", "/location/weather/temperature", "/location/weather/wind"]
```

#### removeItem() {#removeitem}

지정된 객체의 복사본을 만들고 데이터 트리에서 지정된 분기를 제거하고 수정된 복사본을 반환합니다.

**매개 변수**

* 트리:데이터 객체입니다.
* 키:제거할 키입니다.

**반환**

키가 제거된 원본 데이터 개체의 복사본입니다.

**예**

다음 개체를 생각해 보십시오.

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

다음 예제 스크립트는 데이터 트리에서 /one/2/3/4 분기를 제거합니다.

```
myObject = ContextHub.Utils.JSON.tree.removeItem(myObject, "/one/two/three/four");
```

이 함수는 다음 객체를 반환합니다.

```
myObject {
  one: {
    foo: "bar"
  }
}
```

#### 문서의 기밀 정보 가리기(key) {#sanitizekey-key}

문자열 값을 정리하여 키로 사용할 수 있도록 합니다. 문자열을 정리하기 위해 이 함수는 다음 작업을 수행합니다.

* 연속해서 여러 슬래시를 한 슬래시로 줄입니다.
* 문자열의 시작 및 끝 부분에서 공백을 제거합니다.
* 결과를 슬래시로 구분된 문자열 배열로 분할합니다.

결과 배열을 사용하여 사용 가능한 키를 만듭니다.  **매개 변수**

* **키:** 문서의  `string` 기밀 정보 가리기

**반환**

각 문자열이 슬래시로 구분된 `key`의 부분인 `string` 값의 배열입니다. 정리된 키를 나타냅니다. 정리된 배열의 길이가 0이면 이 함수는 `null`을 반환합니다.

**예**

다음 코드에서는 문자열을 정리하여 `["this", "is", "a", "path"]` 배열을 만든 다음 배열에서 `"/this/is/a/path"` 키를 생성합니다.

```
var key = " / this////is/a/path ";
ContextHub.Utils.JSON.tree.sanitizeKey(key)
"/" + ContextHub.Utils.JSON.tree.sanitizeKey(key).join("/");
```

#### setItem(tree, key, value) {#setitem-tree-key-value}

개체 사본의 데이터 트리에 키/값 쌍을 추가합니다. 데이터 트리에 대한 자세한 내용은 [지속성](/help/sites-developing/contexthub.md#persistence)을 참조하십시오.

**매개 변수**

* 트리:데이터 객체입니다.
* 키:추가하려는 값과 연결할 키. 키는 데이터 트리의 항목 경로입니다. 이 함수는 키를 추가하기 전에 `ContextHub.Utils.JSON.tree.sanitize`을 호출하여 키를 정리합니다.
* 값:데이터 트리에 추가할 값입니다.

**반환**

`key`/ `value` 쌍을 포함하는 `tree` 개체의 복사본.

**예**

다음 Javascript 코드를 고려하십시오.

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

myObject 객체에는 다음 값이 있습니다.

## ContextHub.Utils.store후보자 {#contexthub-utils-storecandidates}

스토어 지원자를 등록하고 등록된 스토어 지원자를 확보할 수 있습니다.

### 함수(ContextHub.Utils.store후보자) {#functions-contexthub-utils-storecandidates}

#### getRegisteredComputers(storeType) {#getregisteredcandidates-storetype}

스토어 후보로 등록된 스토어 유형을 반환합니다. 특정 스토어 유형의 등록된 캔들 또는 모든 스토어 유형의 캔버스를 검색합니다.

**매개 변수**

* **storeType:** (String) 저장소 유형의 이름입니다. [ `ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#contexthub-utils-storecandidates) 함수의 `storeType` 매개 변수를 참조하십시오.

**반환**

저장소 유형의 객체입니다. 객체 속성은 스토어 유형 이름이고 속성 값은 등록된 스토어 후보 배열입니다.

#### getStoreFromAcquisials(storeType) {#getstorefromcandidates-storetype}

등록된 지원자의 스토어 유형을 반환합니다. 동일한 이름의 스토어 유형이 두 개 이상 등록되면 이 함수는 우선 순위가 가장 높은 스토어 유형을 반환합니다.

**매개 변수**

* storeType:(문자열) 스토어 후보자의 이름입니다. [ `ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) 함수의 `storeType` 매개 변수를 참조하십시오.

**반환**

등록된 저장소 후보를 나타내는 객체입니다. 요청한 저장소 유형이 등록되어 있지 않으면 오류가 발생합니다.

#### getSupportedStoreTypes() {#getsupportedstoretypes}

스토어 후보로 등록된 스토어 유형의 이름을 반환합니다. 이 함수에는 매개 변수가 필요하지 않습니다.

**반환**

각 문자열이 저장소 후보가 등록된 스토어 유형인 문자열 값의 배열입니다. [ `ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#contexthub-utils-storecandidates) 함수의 `storeType` 매개 변수를 참조하십시오.

#### registerStoreCandier(store, storeType, priority, apply) {#registerstorecandidate-store-storetype-priority-applies}

이름과 우선 순위를 사용하여 스토어 개체를 스토어 후보로 등록합니다.

우선 순위는 같은 이름의 점포의 중요성을 나타내는 숫자입니다. 이미 등록한 스토어 후보자와 같은 이름을 사용하여 등록한 경우 우선 순위가 높은 후보가 사용됩니다. 매장 후보등록을 할 때 같은 이름 있는 스토어 후보보다 우선순위가 높은 경우에만 해당 스토어가 등록된다.

**매개 변수**

* **store:** (개체) 저장소 후보로 등록할 스토어 객체입니다.
* **storeType:** (String) 스토어 후보자의 이름입니다. 이 값은 스토어 대상의 인스턴스를 만들 때 필요합니다.
* **priority:** (Number) 스토어 후보자의 우선 순위입니다.
* **apples:** (함수) 현재 환경에서 스토어의 응용 프로그램을 평가하는 함수 스토어를 적용할 수 있으면 `true`을 반환하고 그렇지 않으면 `false`을 반환해야 합니다. 기본값은 true를 반환하는 함수입니다.`function() {return true;}`

**예**

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandiate', 0);
```

