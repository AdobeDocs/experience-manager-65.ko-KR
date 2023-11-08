---
title: SPA 블루프린트
description: 이 문서에서는 모든 SPA 프레임워크가 AEM 내에서 편집 가능한 SPA 구성 요소를 구현하기 위해 이행해야 하는 일반적인 프레임워크 독립적인 계약에 대해 설명합니다.
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
exl-id: 383f84fd-455c-49a4-9e2b-1c4757cc188b
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '2075'
ht-degree: 1%

---

# SPA 블루프린트{#spa-blueprint}

작성자가 AEM SPA Editor를 사용하여 SPA의 콘텐츠를 편집할 수 있도록 SPA에서 이행해야 하는 요구 사항이 있으며, 이는 이 문서에 설명되어 있습니다.

>[!NOTE]
>
>SPA 편집기는 SPA 프레임워크 기반의 클라이언트측 렌더링(예: React 또는 Angular)이 필요한 프로젝트에 권장되는 솔루션입니다.

## 소개 {#introduction}

이 문서에서는 모든 SPA 프레임워크가 AEM 내에서 편집 가능한 SPA 구성 요소를 구현하기 위해 이행해야 하는 일반 계약(즉, AEM 지원 계층의 종류)에 대해 설명합니다.

>[!NOTE]
>
>다음 요구 사항은 프레임워크에 독립적입니다. 이러한 요구 사항이 충족되면 모듈, 컴포넌트, 서비스로 구성된 프레임워크별 계층을 제공할 수 있다.
>
>**AEM의 React 및 Angular 프레임워크는 이러한 요구 사항을 이미 충족합니다.** 이 블루프린트의 요구 사항은 AEM에서 사용할 다른 프레임워크를 구현하려는 경우에만 관련이 있습니다.

>[!CAUTION]
>
>AEM의 SPA 기능은 프레임워크에 독립적이지만 현재는 React 및 Angular 프레임워크만 지원됩니다.

작성자가 AEM 페이지 편집기를 사용하여 단일 페이지 애플리케이션 프레임워크에 의해 노출된 데이터를 편집할 수 있도록 하려면 프로젝트가 AEM 저장소 내의 애플리케이션에 대해 저장된 데이터의 의미론적 의미를 나타내는 모델 구조를 해석할 수 있어야 합니다. 이 목표를 달성하기 위해 두 개의 프레임워크 독립적인 라이브러리가 제공됩니다. `PageModelManager` 및 `ComponentMapping`.

### PageModelManager {#pagemodelmanager}

다음 `PageModelManager` 라이브러리는 SPA 프로젝트에서 사용할 NPM 패키지로 제공됩니다. SPA과 함께 제공되며 데이터 모델 관리자 역할을 합니다.

SPA을 대신하여 실제 콘텐츠 구조를 나타내는 JSON 구조의 검색 및 관리를 추상화합니다. 또한 SPA과 동기화하여 구성 요소를 다시 렌더링해야 하는 시기를 알려주어야 합니다.

NPM 패키지 보기 [@adobe/aem-spa-page-model-manager](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager)

초기화 시 `PageModelManager`, 라이브러리는 먼저 앱의 제공된 루트 모델(매개 변수, 메타 속성 또는 현재 URL을 통해)을 로드합니다. 라이브러리가 현재 페이지의 모델이 루트 모델의 일부가 아님을 식별하면 가져온 후 하위 페이지의 모델로 포함합니다.

![page_model_integration](assets/page_model_consolidation.png)

### 구성 요소 매핑 {#componentmapping}

다음 `ComponentMapping` 모듈은 프론트엔드 프로젝트에 NPM 패키지로 제공됩니다. 프론트엔드 구성 요소를 저장하고 SPA에서 프론트엔드 구성 요소를 AEM 리소스 유형에 매핑하는 방법을 제공합니다. 이렇게 하면 애플리케이션의 JSON 모델을 구문 분석할 때 구성 요소를 동적으로 확인할 수 있습니다.

모델에 있는 각 항목에는 `:type` AEM 리소스 유형을 표시하는 필드입니다. 마운트되면 프론트엔드 구성 요소는 기본 라이브러리에서 받은 모델 조각을 사용하여 자신을 렌더링할 수 있습니다.

#### 구성 요소 매핑을 위한 동적 모델 {#dynamic-model-to-component-mapping}

AEM용 JavaScript SPA SDK에서 동적 모델과 구성 요소 간 매핑이 발생하는 방법에 대한 자세한 내용은 문서 를 참조하십시오 [SPA용 동적 모델과 구성 요소 간 매핑](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

### 프레임워크별 계층 {#framework-specific-layer}

각 프론트엔드 프레임워크에 대해 세 번째 레이어를 구현해야 합니다. 이 세 번째 라이브러리는 기본 라이브러리와의 상호 작용을 담당하며, 데이터 모델과 상호 작용하기 위해 잘 통합되고 사용하기 쉬운 일련의 진입점을 제공합니다.

본 문서의 나머지 부분은 이러한 중간 프레임워크 특정 계층과 프레임워크에 독립적이어야 하는 요구 사항을 기술한다. 다음 요구 사항을 고려하여 프로젝트 구성 요소가 데이터 모델 관리를 담당하는 기본 라이브러리와 상호 작용하는 프레임워크별 계층을 제공할 수 있습니다.

## 일반 개념 {#general-concepts}

### 페이지 모델 {#page-model}

페이지의 콘텐츠 구조는 AEM에 저장됩니다. 페이지 모델은 SPA 구성 요소를 매핑하고 인스턴스화하는 데 사용됩니다. SPA 개발자는 AEM 구성 요소에 매핑되는 SPA 구성 요소를 만듭니다. 이를 위해 리소스 유형(또는 AEM 구성 요소에 대한 경로)을 고유 키로 사용합니다.

SPA 구성 요소는 페이지 모델과 동기화되어야 하며 그에 따라 콘텐츠에 대한 변경 사항을 업데이트해야 합니다. 동적 구성 요소를 사용하는 패턴은 제공된 페이지 모델 구조에 따라 구성 요소를 즉시 인스턴스화하는 데 사용해야 합니다.

### 메타 필드 {#meta-fields}

페이지 모델은 를 기반으로 하는 JSON 모델 내보내기를 사용합니다. [Sling 모델](https://sling.apache.org/documentation/bundles/models.html) API. 내보내기 가능한 슬링 모델은 기본 라이브러리가 데이터 모델을 해석할 수 있도록 다음 필드 목록을 표시합니다.

* `:type`: AEM 리소스 유형(기본값 = 리소스 유형)
* `:children`: 현재 리소스의 계층 구조 하위 항목입니다. 하위 항목은 현재 리소스의 내부 콘텐츠에 속하지 않습니다(페이지를 나타내는 항목에서 찾을 수 있음)
* `:hierarchyType`: 리소스의 계층 구조 유형입니다. 다음 `PageModelManager` 는 현재 페이지 유형을 지원합니다

* `:items`: 현재 리소스의 하위 콘텐츠 리소스(중첩된 구조, 컨테이너에만 있음)
* `:itemsOrder`: 순서가 지정된 하위 목록입니다. JSON 맵 개체는 필드의 순서를 보장하지 않습니다. 맵과 현재 배열을 모두 가짐으로써 API 소비자는 두 구조의 이점을 얻을 수 있습니다
* `:path`: 항목의 콘텐츠 경로(페이지를 나타내는 항목에 있음)

참조: [AEM Content Services 시작](https://helpx.adobe.com/kr/experience-manager/kt/sites/using/content-services-tutorial-use.html)

### 프레임워크별 모듈 {#framework-specific-module}

문제를 분리하는 것은 프로젝트 구현을 용이하게 하는 데 도움이 됩니다. 따라서 npm 전용 패키지가 제공되어야 합니다. 이 패키지는 기본 모듈, 서비스 및 구성 요소를 집계 및 노출합니다. 이러한 구성 요소는 데이터 모델 관리 논리를 캡슐화하고 프로젝트의 구성 요소가 기대하는 데이터에 대한 액세스 권한을 제공해야 합니다. 모듈은 또한 기본 라이브러리의 유용한 진입점을 과도적으로 노출시킵니다.

라이브러리의 상호 운용성을 용이하게 하기 위해 Adobe은 프레임워크별 모듈에 다음 라이브러리를 번들로 제공할 것을 권장합니다. 필요한 경우 레이어는 기본 API를 프로젝트에 노출하기 전에 캡슐화하고 조정할 수 있습니다.

* [@adobe/aem-spa-page-model-manager](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager)
* [@adobe/aem-spa-component-매핑](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

#### 구현 {#implementations}

#### 반응 {#react}

npm 모듈: [@adobe/aem-react-edit-components](https://www.npmjs.com/package/@adobe/aem-react-editable-components)

#### Angular {#angular}

npm 모듈: [angular @adobe/aem-editable-components](https://www.npmjs.com/package/@adobe/aem-angular-editable-components)

## 주요 서비스 및 구성 요소 {#main-services-and-components}

다음 엔티티는 각 프레임워크에 명시된 지침에 따라 구현되어야 합니다. 프레임워크 아키텍처를 기반으로 구현은 폭넓게 다양할 수 있지만, 기술된 기능이 제공되어야 한다.

### 모델 공급자 {#the-model-provider}

프로젝트 구성 요소는 모델 공급자에게 모델 조각에 대한 액세스를 위임해야 합니다. 그러면 모델 공급자는 모델의 지정된 조각에 대한 변경 사항을 수신하고 업데이트된 모델을 위임 구성 요소에 반환해야 합니다.

이렇게 하려면 모델 공급자가에 등록해야 합니다 ` [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager)`. 그런 다음 변경이 발생하면 업데이트된 데이터를 받아 위임 구성 요소에 전달합니다. 규칙에 따라 모델 조각을 전달할 위임 구성 요소에 사용할 수 있는 속성은 다음과 같이 이름이 지정됩니다 `cqModel`. 구현은 이 속성을 구성 요소에 자유롭게 제공할 수 있지만, 프레임워크 아키텍처와의 통합, 검색 기능 및 사용 편의성과 같은 측면을 고려해야 합니다.

### 구성 요소 HTML 데코레이터 {#the-component-html-decorator}

Component Decorator는 페이지 편집기에서 예상하는 일련의 데이터 속성 및 클래스 이름으로 각 구성 요소 인스턴스의 요소 외부 HTML을 장식하는 역할을 합니다.

#### 구성 요소 선언 {#component-declaration}

프로젝트의 구성 요소에서 생성한 외부 HTML 요소에 다음 메타데이터를 추가해야 합니다. 이를 통해 페이지 편집기는 해당 편집 구성을 검색할 수 있습니다.

* `data-cq-data-path`: 와 관련된 리소스의 경로 `jcr:content`

#### 기능 선언 및 자리 표시자 편집 {#editing-capability-declaration-and-placeholder}

프로젝트의 구성 요소에서 생성한 외부 HTML 요소에 다음 메타데이터 및 클래스 이름을 추가해야 합니다. 이를 통해 페이지 편집기는 관련 기능을 제공할 수 있습니다.

* `cq-placeholder`: 빈 구성 요소의 자리 표시자를 식별하는 클래스 이름
* `data-emptytext`: 구성 요소 인스턴스가 비어 있을 때 오버레이에 표시되는 레이블입니다

**빈 구성 요소에 대한 자리 표시자**

각 구성 요소는 구성 요소가 비어 있는 것으로 식별될 때 자리 표시자 및 관련 오버레이와 관련된 데이터 특성 및 클래스 이름으로 외부 HTML 요소를 장식하는 기능으로 확장되어야 합니다.

**구성 요소 비움 정보**

* 구성 요소가 논리적으로 비어 있습니까?
* 구성 요소가 비어 있을 때 오버레이에 표시되는 레이블은 무엇입니까?

### 컨테이너 {#container}

컨테이너는 하위 구성 요소를 포함하고 렌더링하기 위한 구성 요소입니다. 이를 위해 컨테이너는 다음을 반복합니다. `:itemsOrder`, `:items` 및 `:children` 모델의 속성입니다.

컨테이너는 의 저장소에서 하위 구성 요소를 동적으로 가져옵니다. [`ComponentMapping`](/help/sites-developing/spa-blueprint.md#componentmapping) 라이브러리입니다. 그런 다음 컨테이너는 모델 공급자 기능으로 하위 구성 요소를 확장하고 마지막으로 인스턴스화합니다.

### 페이지 {#page}

다음 `Page` 구성 요소가 `Container` 구성 요소. 컨테이너는 하위 페이지를 포함한 하위 구성 요소를 포함하고 렌더링하기 위한 구성 요소입니다. 이를 위해 컨테이너는 다음을 반복합니다. `:itemsOrder`, `:items`, 및 `:children` 모델의 속성입니다. 다음 `Page` 구성 요소는 의 저장소에서 하위 구성 요소를 동적으로 가져옵니다. [구성 요소 매핑](/help/sites-developing/spa-blueprint.md#componentmapping) 라이브러리입니다. 다음 `Page` 은 하위 구성 요소를 인스턴스화합니다.

### 응답형 격자 {#responsive-grid}

응답형 격자 구성 요소는 컨테이너입니다. 여기에는 해당 열을 나타내는 모델 공급자의 특정 변형이 포함되어 있습니다. 반응형 그리드 및 해당 열은 프로젝트 구성 요소의 외부 HTML 요소를 모델에 포함된 특정 클래스 이름으로 장식하는 역할을 합니다.

응답형 격자 구성 요소는 복잡하고 사용자 지정된 경우가 거의 없기 때문에 AEM 구성 요소에 미리 매핑되어야 합니다.

#### 특정 모델 필드 {#specific-model-fields}

* `gridClassNames:` 응답형 격자에 대해 제공된 클래스 이름
* `columnClassNames:` 응답형 열에 대해 제공된 클래스 이름

#### 반응형 격자의 자리 표시자 {#placeholder-of-the-reponsive-grid}

SPA 구성 요소는 반응형 그리드 등의 그래픽 컨테이너에 매핑되며 콘텐츠를 작성할 때 가상 하위 자리 표시자를 추가해야 합니다. SPA의 콘텐츠를 페이지 편집기에서 작성할 때 해당 콘텐츠는 iframe 및 를 사용하여 편집기에 삽입됩니다. `data-cq-editor` 속성이 해당 컨텐츠의 문서 노드에 추가됩니다. 다음의 경우 `data-cq-editor` 속성이 있으면 컨테이너는 새 구성 요소를 페이지에 삽입할 때 작성자가 상호 작용하는 영역을 나타내는 HTMLElement를 포함해야 합니다.

예:

```
<div data-cq-data-path={"path/to/the/responsivegrid/*"} className="new section aem-Grid-newComponent"/>
```

>[!NOTE]
>
>예제에 사용된 클래스 이름은 현재 페이지 편집기에 필요합니다.
>
>* `"new section"`: 현재 요소가 컨테이너의 자리 표시자임을 나타냅니다
>* `"aem-Grid-newComponent"`: 레이아웃 작성을 위한 구성 요소를 표준화합니다.
>

#### 구성 요소 매핑 {#component-mapping}

기본 [`Component Mapping`](/help/sites-developing/spa-blueprint.md#componentmapping) 라이브러리 및 해당 `MapTo` 현재 구성 요소 클래스와 함께 제공되는 편집 구성과 관련된 기능을 제공하도록 기능을 캡슐화하고 확장할 수 있습니다.

```
const EditConfig = {

    emptyLabel: 'My Component',

    isEmpty: function() {
        return !this.props || !this.props.cqModel || this.props.cqModel.isEmpty;
    }
};

class MyComponent extends Component {

    render() {
        return <div className={'my-component'}></div>;
    }
}

MapTo('component/resource/path')(MyComponent, EditConfig);
```

위의 구현에서 프로젝트 구성 요소는에 실제로 등록되기 전에 빈 기능으로 확장됩니다. [구성 요소 매핑](/help/sites-developing/spa-blueprint.md#componentmapping) 저장. 이 작업은 를 캡슐화하고 확장하여 수행합니다. [`ComponentMapping`](/help/sites-developing/spa-blueprint.md#componentmapping) 라이브러리에서 의 지원을 소개합니다. `EditConfig` 구성 개체:

```
/**
 * Configuration object in charge of providing the necessary data expected by the page editor to initiate the authoring. The provided data will be decorating the associated component
 *
 * @typedef {{}} EditConfig
 * @property {String} [dragDropName]       If defined, adds a specific class name enabling the drag and drop functionality
 * @property {String} emptyLabel           Label to be displayed by the placeholder when the component is empty. Optionally returns an empty text value
 * @property {function} isEmpty            Should the component be considered empty. The function is called using the context of the wrapper component giving you access to the component model
 */

/**
 * Map a React component with the given resource types. If an {@link EditConfig} is provided the <i>clazz</i> is wrapped to provide edition capabilities on the AEM Page Editor
 *
 * @param {string[]} resourceTypes                      - List of resource types for which to use the given <i>clazz</i>
 * @param {class} clazz                                 - Class to be instantiated for the given resource types
 * @param {EditConfig} [editConfig]                     - Configuration object for enabling the edition capabilities
 * @returns {class}                                     - The resulting decorated Class
 */
ComponentMapping.map = function map (resourceTypes, clazz, editConfig) {};
```

## 페이지 편집기와의 계약 {#contract-with-the-page-editor}

편집기가 상호 작용할 수 있도록 프로젝트 구성 요소는 최소한 다음 데이터 속성을 생성해야 합니다.

* `data-cq-data-path`: 다음에서 제공하는 구성 요소의 상대 경로 `PageModel` (예: `"root/responsivegrid/image"`). 이 속성은 페이지에 추가해서는 안 됩니다.

요약하면, 페이지 편집기가 편집 가능한 것으로 해석하려면 프로젝트 구성 요소는 다음 계약을 준수해야 합니다.

* 프론트엔드 구성 요소 인스턴스를 AEM 리소스에 연결하는 데 필요한 속성을 제공합니다.
* 빈 자리 표시자를 만들 수 있도록 예상된 일련의 속성과 클래스 이름을 제공합니다.
* 에셋 드래그 앤 드롭을 활성화하는 예상 클래스 이름을 제공합니다.

### 일반적인 HTML 요소 구조 {#typical-html-element-structure}

다음 조각은 페이지 컨텐츠 구조의 일반적인 HTML 표현을 보여 줍니다. 다음은 몇 가지 중요한 점입니다.

* 응답형 격자 요소에는 접두사가 있는 클래스 이름이 있습니다. `aem-Grid--`
* 응답형 열 요소에는 접두사가 있는 클래스 이름이 있습니다. `aem-GridColumn--`
* 두 개의 이전 접두사가 동일한 요소에 표시되지 않는 것처럼 부모 그리드의 열이기도 한 응답형 그리드는 래핑됩니다
* 편집 가능한 리소스에 해당하는 요소에는 `data-cq-data-path` 속성. 다음을 참조하십시오. [페이지 편집기와 계약](#contract-wtih-the-page-editor) 섹션에 있는 마지막 항목이 될 필요가 없습니다.

```
<div data-cq-data-path="/content/page">
    <div class="aem-Grid aem-Grid--12 aem-Grid--default--12">
        <div class="aem-container aem-GridColumn aem-GridColumn--default--12" data-cq-data-path="/content/page/jcr:content/root/responsivegrid">
            <div class="aem-Grid aem-Grid--12 aem-Grid--default--12">
                <div class="cmp-image cq-dd-image aem-GridColumn aem-GridColumn--default--12" data-cq-data-path="/root/responsivegrid/image">
                    <img src="/content/we-retail-spa-sample/react/jcr%3acontent/root/responsivegrid/image.img.jpeg/1512113734019.jpeg">
                </div>
            </div>
        </div>
    </div>
</div>
```

## 탐색 및 라우팅 {#navigation-and-routing}

앱은 라우팅을 소유합니다. 프론트엔드 개발자는 먼저 탐색 구성 요소(AEM 탐색 구성 요소에 매핑됨)를 구현해야 합니다. 이 구성 요소는 콘텐츠 조각을 표시하거나 숨기는 일련의 경로와 함께 사용할 URL 링크를 렌더링합니다.

기본 [`PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) 라이브러리 및 해당 ` [ModelRouter](/help/sites-developing/spa-routing.md)` 모듈(기본적으로 활성화됨)은 주어진 리소스 경로와 연관된 모델을 미리 가져오고 액세스 권한을 제공합니다.

두 엔티티는 경로설정 개념과 관련이 있지만 ` [ModelRouter](/help/sites-developing/spa-routing.md)` 은(는) 다음을 보유하는 것에 대해서만 책임이 있습니다. ` [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager)` 현재 애플리케이션 상태와 동기화되는 구조화된 데이터 모델이 로드됩니다.

문서 보기 [SPA 모델 라우팅](/help/sites-developing/spa-routing.md) 추가 정보.

## SPA 작동 중 {#spa-in-action}

문서로 계속 진행하여 간단한 SPA의 작동 방식을 확인하고 SPA을 직접 실험해 보십시오 [AEM에서 SPA 시작하기](/help/sites-developing/spa-getting-started-react.md).

## 추가 참조 {#further-reading}

AEM의 SPA에 대한 자세한 내용은 다음 문서를 참조하십시오.

* [SPA 작성 개요](/help/sites-developing/spa-overview.md) AEM 및 커뮤니케이션 모델의 SPA 개요
* [AEM에서 SPA 시작하기](/help/sites-developing/spa-getting-started-react.md) 간단한 SPA 및 작동 방식에 대한 안내서
