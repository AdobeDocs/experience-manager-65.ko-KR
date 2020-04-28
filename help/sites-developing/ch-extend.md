---
title: ContextHub 확장
seo-title: ContextHub 확장
description: 제공된 항목이 솔루션 요구 사항을 충족하지 않을 때 새로운 유형의 ContextHub 스토어 및 모듈 정의
seo-description: 제공된 항목이 솔루션 요구 사항을 충족하지 않을 때 새로운 유형의 ContextHub 스토어 및 모듈 정의
uuid: 1d80c01d-ec5d-4e76-849d-bec0e1c3941a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 13a908ae-6965-4438-96d0-93516b500884
translation-type: tm+mt
source-git-commit: ed34f2200f4ff4f407f7b92165685af390f5f7e3

---


# ContextHub 확장{#extending-contexthub}

제공된 항목이 솔루션 요구 사항을 충족하지 않을 때 새로운 유형의 ContextHub 스토어 및 모듈을 정의합니다.

## 사용자 지정 스토어 후보자 만들기 {#creating-custom-store-candidates}

ContextHub 스토어는 등록된 스토어 후보자로부터 만들어집니다. 사용자 정의 스토어를 만들려면 스토어 지원자를 만들고 등록해야 합니다.

저장소 후보를 만들고 등록하는 코드를 포함하는 javascript 파일은 [클라이언트 라이브러리 폴더에](/help/sites-developing/clientlibs.md#creating-client-library-folders)포함되어야 합니다. 폴더의 카테고리는 다음 패턴과 일치해야 합니다.

```xml
contexthub.store.[storeType]
```

카테고리의 `[storeType]` 부분은 매장 `storeType` 후보가 등록된 부분입니다. (ContextHub [저장소 후보 등록을 참조하십시오](/help/sites-developing/ch-extend.md#registering-a-contexthub-store-candidate)). 예를 들어 storeType의 `contexthub.mystore`경우 클라이언트 라이브러리 폴더의 카테고리가 있어야 합니다 `contexthub.store.contexthub.mystore`.

### ContextHub 저장소 후보 만들기 {#creating-a-contexthub-store-candidate}

저장소 후보를 만들려면 이 [`ContextHub.Utils.inheritance.inherit`](/help/sites-developing/contexthub-api.md#inherit-child-parent) 함수를 사용하여 기본 스토어 중 하나를 확장합니다.

* [`ContextHub.Store.PersistedStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore)
* [`ContextHub.Store.SessionStore`](/help/sites-developing/contexthub-api.md#contexthub-store-sessionstore)
* [`ContextHub.Store.JSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore)
* [`ContextHub.Store.PersistedJSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)

각 기본 스토어는 [`ContextHub.Store.Core`](/help/sites-developing/contexthub-api.md#contexthub-store-core) 스토어를 확장합니다.

다음 예제에서는 가장 간단한 `ContextHub.Store.PersistedStore` 스토어 후보 확장을 만듭니다.

```
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

현실적으로, 사용자 지정 스토어 지원자는 추가 기능을 정의하거나 스토어의 초기 구성을 무시합니다. 아래 보관소에 여러 [샘플 스토어 지원자가](/help/sites-developing/ch-samplestores.md) 설치되어 `/libs/granite/contexthub/components/stores`있습니다. 이러한 샘플에서 배우려면 CRXDE Lite를 사용하여 javascript 파일을 엽니다.

### ContextHub 저장소 후보 등록 {#registering-a-contexthub-store-candidate}

스토어 후보를 등록하여 ContextHub 프레임워크와 통합하고 스토어에서 만들 수 있습니다. 스토어 지원자를 등록하려면 [`registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) 클래스의 `ContextHub.Utils.storeCandidates` 기능을 사용합니다.

스토어 지원자를 등록할 때 스토어 유형의 이름을 제공합니다. 지원자로부터 스토어를 만들 때 스토어 유형을 사용하여 기반이 되는 후보를 식별합니다.

스토어 지원자를 등록할 때 우선 순위를 표시합니다. 이미 등록된 스토어 후보자와 같은 스토어 유형을 사용하여 등록한 경우 우선 순위가 높은 후보가 사용됩니다. 따라서 기존 스토어 후보자를 새로운 구현으로 재정의할 수 있습니다.

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

대부분의 경우 한 명의 지원자만 필요하고 우선 순위를 설정할 수 `0`있지만 관심 있는 경우 [더 많은 고급 등록에 대해 알 수 있습니다. 이 경우](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) JavaScript 조건(`applies`) 및 후보 우선 순위를 기준으로 몇 가지 스토어 구현 중 하나를 선택할 수 있습니다.

## ContextHub UI 모듈 유형 만들기 {#creating-contexthub-ui-module-types}

ContextHub에 [설치된 UI 모듈 유형이 요구 사항을 충족하지 않을](/help/sites-developing/ch-samplemodules.md) 때 사용자 정의 UI 모듈 유형을 만듭니다. UI 모듈 유형을 만들려면 `ContextHub.UI.BaseModuleRenderer` 클래스를 확장한 다음 여기에 등록하여 새 UI 모듈 렌더러를 만듭니다 `ContextHub.UI`.

UI 모듈 렌더러를 만들려면 UI 모듈을 렌더링하는 로직을 포함하는 `Class` 개체를 만듭니다. 최소한 클래스에서 다음 작업을 수행해야 합니다.

* 클래스를 `ContextHub.UI.BaseModuleRenderer` 확장합니다. 이 클래스는 모든 UI 모듈 렌더러에 대한 기본 구현입니다. 이 `Class` 개체는 이 클래스의 이름을 확장되는 것으로 지정하는 데 사용하는 `extend` 속성을 정의합니다.

* 기본 구성을 제공합니다. 속성을 `defaultConfig` 만듭니다. 이 속성은 UI 모듈에 대해 정의된 속성과 필요한 기타 [`contexthub.base`](/help/sites-developing/ch-samplemodules.md#contexthub-base-ui-module-type) 속성을 포함하는 오브젝트입니다.

The source for `ContextHub.UI.BaseModuleRenderer` is located at /libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js.  렌더러를 등록하려면 [`registerRenderer`](/help/sites-developing/contexthub-api.md#registerrenderer-moduletype-renderer-dontrender) 클래스의 `ContextHub.UI` 메서드를 사용합니다. 모듈 유형의 이름을 입력해야 합니다. 관리자는 이 렌더러를 기반으로 UI 모듈을 만들 때 이 이름을 지정합니다.

직접 실행되는 익명 함수에서 렌더러 클래스를 만들고 등록합니다. 다음 예는 contexthub.browserinfo UI 모듈의 소스 코드를 기반으로 합니다. 이 UI 모듈은 `ContextHub.UI.BaseModuleRenderer` 클래스의 간단한 확장입니다.

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

렌더러를 만들고 등록하는 코드를 포함하는 javascript 파일은 [클라이언트 라이브러리 폴더에](/help/sites-developing/clientlibs.md#creating-client-library-folders)포함되어야 합니다. 폴더의 카테고리는 다음 패턴과 일치해야 합니다.

```xml
contexthub.module.[moduleType]
```

범주의 `[moduleType]` 부분은 모듈 렌더러가 등록된 `moduleType` 부분입니다. 예를 들어, `moduleType` 의 `contexthub.browserinfo`경우 클라이언트 라이브러리 폴더의 카테고리가 있어야 합니다 `contexthub.module.contexthub.browserinfo`.
