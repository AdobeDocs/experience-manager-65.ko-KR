---
title: ContextHub 확장
description: 제공된 ContextHub 저장소 및 모듈이 솔루션 요구 사항을 충족하지 못할 경우 새로운 유형의 ContextHub 저장소 및 모듈을 정의합니다
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: 41898fa7-a369-4c63-8ccb-69eb3fa146a1
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---

# ContextHub 확장{#extending-contexthub}

제공된 ContextHub 저장소 및 모듈이 솔루션 요구 사항을 충족하지 않는 경우 새로운 유형의 ContextHub 저장소 및 모듈을 정의합니다.

## 사용자 지정 스토어 후보 생성 {#creating-custom-store-candidates}

ContextHub 저장소는 등록된 저장소 후보에서 만들어집니다. 사용자 지정 저장소를 만들려면 저장소 후보를 만들고 등록합니다.

저장소 후보를 만들고 등록하는 코드가 포함된 JavaScript 파일은에 포함되어야 합니다. [클라이언트 라이브러리 폴더](/help/sites-developing/clientlibs.md#creating-client-library-folders). 폴더의 범주는 다음 패턴과 일치해야 합니다.

```xml
contexthub.store.[storeType]
```

다음 `[storeType]` 이 범주의 일부는 `storeType` 상점 후보가 등록된 상대. (참조: [ContextHub 저장소 후보 등록](/help/sites-developing/ch-extend.md#registering-a-contexthub-store-candidate)). 예: storeType of `contexthub.mystore`: 클라이언트 라이브러리 폴더의 범주는 다음과 같아야 합니다. `contexthub.store.contexthub.mystore`.

### ContextHub 저장소 후보 만들기 {#creating-a-contexthub-store-candidate}

스토어 후보를 생성하려면 다음을 사용합니다. [`ContextHub.Utils.inheritance.inherit`](/help/sites-developing/contexthub-api.md#inherit-child-parent) 기본 저장소 중 하나를 확장하는 기능:

* [&#39;ContextHub.Store.PersistedStore&#39;](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore)
* [&#39;ContextHub.Store.SessionStore&#39;](/help/sites-developing/contexthub-api.md#contexthub-store-sessionstore)
* [&#39;ContextHub.Store.JSONPtore&#39;](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore)
* [&#39;ContextHub.Store.PersistedJSONPtore&#39;](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)

각 기본 저장소는 [`ContextHub.Store.Core`](/help/sites-developing/contexthub-api.md#contexthub-store-core) 저장.

다음 예제에서는 `ContextHub.Store.PersistedStore` 저장소 후보:

```
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

현실적으로 사용자 정의 저장소 후보는 추가 기능을 정의하거나 저장소의 초기 구성을 재정의합니다. 여러 개 [샘플 저장소 후보](/help/sites-developing/ch-samplestores.md) 아래 저장소에 설치됨 `/libs/granite/contexthub/components/stores`. 이러한 샘플에서 배우려면 CRXDE Lite 를 사용하여 JavaScript 파일을 엽니다.

### ContextHub 저장소 후보 등록 {#registering-a-contexthub-store-candidate}

ContextHub 프레임워크와 통합할 저장소 후보를 등록하고 이를 통해 저장소를 만들 수 있습니다. 스토어 후보를 등록하려면 다음을 사용합니다. [`registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) 의 함수 `ContextHub.Utils.storeCandidates` 클래스.

스토어 후보를 등록할 때 스토어 유형의 이름을 입력합니다. 후보에서 스토어를 생성할 때 스토어 유형을 사용하여 기준이 되는 후보를 식별합니다.

스토어 후보를 등록할 때 우선 순위를 나타냅니다. 이미 등록된 매장 후보자와 동일한 매장 타입을 이용하여 매장 후보자를 등록한 경우, 우선 순위가 높은 후보를 이용한다. 따라서 기존 저장소 후보를 새 구현으로 재정의할 수 있습니다.

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

일반적으로 한 명의 후보자만 필요하며 우선 순위를 다음으로 설정할 수 있습니다. `0`. 그러나 관심이 있다면 다음을 배울 수 있습니다. [추가 고급 등록,](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) JavaScript 조건()을 기반으로 몇 가지 스토어 구현 중 하나를 선택할 수 있습니다.`applies`) 및 후보 우선 순위.

## ContextHub UI 모듈 유형 작성 {#creating-contexthub-ui-module-types}

다음과 같은 경우 사용자 정의 UI 모듈 유형을 만듭니다. [contextHub와 함께 설치됨](/help/sites-developing/ch-samplemodules.md) 요구 사항을 충족하지 않습니다. UI 모듈 유형을 만들려면 를 확장하여 UI 모듈 렌더러를 만듭니다. `ContextHub.UI.BaseModuleRenderer` 클래스를 지정한 다음 `ContextHub.UI`.

UI 모듈 렌더러를 만들려면 `Class` ui 모듈을 렌더링하는 논리를 포함하는 개체입니다. 최소한 클래스는 다음 작업을 수행해야 합니다.

* 확장 `ContextHub.UI.BaseModuleRenderer` 클래스. 이 클래스는 모든 UI 모듈 렌더러에 대한 기본 구현입니다. 다음 `Class` 객체는 이름이 인 속성을 정의합니다. `extend` 이 클래스의 이름을 확장 중인 클래스로 지정하는 데 사용합니다.

* 기본 구성을 제공합니다. 만들기 `defaultConfig` 속성. 이 속성은 다음에 대해 정의된 속성을 포함하는 개체입니다. [`contexthub.base`](/help/sites-developing/ch-samplemodules.md#contexthub-base-ui-module-type) UI 모듈 및 필요한 기타 모든 속성.

다음에 대한 소스 `ContextHub.UI.BaseModuleRenderer` 는 /libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js에 있습니다. 렌더러를 등록하려면 [`registerRenderer`](/help/sites-developing/contexthub-api.md#registerrenderer-moduletype-renderer-dontrender) 방법 `ContextHub.UI` 클래스. 모듈 유형의 이름을 입력합니다. 관리자는 이 렌더러를 기반으로 UI 모듈을 만들 때 이 이름을 지정합니다.

자체 실행 익명 함수에서 렌더러 클래스를 만들고 등록합니다. 다음 예제는 contexthub.browserinfo UI 모듈의 소스 코드를 기반으로 합니다. 이 UI 모듈은 `ContextHub.UI.BaseModuleRenderer` 클래스.

```xml
;(function() {

    var SurferinfoRenderer = new Class({
        extend: ContextHub.UI.BaseModuleRenderer,

        defaultConfig: {
            icon: 'coral-Icon--globe',
            title: 'Browser/OS Information',

            storeMapping: {
                surferinfo: 'surferinfo'
            },

            template:
                '<p>{{surferinfo.browser.family}} {{surferinfo.browser.version}}</p>' +
                '<p>{{surferinfo.os.name}} {{surferinfo.os.version}}</p>'
        }
    });

    ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());

}());
```

렌더러를 만들고 등록하는 코드가 포함된 JavaScript 파일은에 포함되어야 합니다 [클라이언트 라이브러리 폴더](/help/sites-developing/clientlibs.md#creating-client-library-folders). 폴더의 범주는 다음 패턴과 일치해야 합니다.

```xml
contexthub.module.[moduleType]
```

다음 `[moduleType]` 이 범주의 일부는 `moduleType` 를 사용하여 모듈 렌더러가 등록됩니다. 예: `moduleType` / `contexthub.browserinfo`: 클라이언트 라이브러리 폴더의 범주는 다음과 같아야 합니다. `contexthub.module.contexthub.browserinfo`.
