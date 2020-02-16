---
title: SPA Blueprint
seo-title: SPA Blueprint
description: 이 문서에서는 AEM 내에서 편집 가능한 SPA 구성 요소를 구현하기 위해 모든 SPA 프레임워크가 수행해야 하는 일반적인 프레임워크 독립적인 계약에 대해 설명합니다.
seo-description: 이 문서에서는 AEM 내에서 편집 가능한 SPA 구성 요소를 구현하기 위해 모든 SPA 프레임워크가 수행해야 하는 일반적인 프레임워크 독립적인 계약에 대해 설명합니다.
uuid: 48f2d415-ec34-49dc-a8e1-6feb5a8a5bbe
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 04ac8203-320b-4671-aaad-6e1397b12b6f
docset: aem65
translation-type: tm+mt
source-git-commit: 2dad220d6593ed542816f8a97b0d4b44f0d57876

---


# SPA Blueprint{#spa-blueprint}

작성자가 AEM SPA 편집기를 사용하여 SPA의 컨텐츠를 편집할 수 있도록 하려면 SPA가 반드시 준수해야 하는 요구 사항이 있으며, 이 문서에는 설명되어 있습니다.

>[!NOTE]
>
>SPA 편집기는 SPA 프레임워크 기반의 클라이언트측 렌더링(예: 반응 또는 각도)이 필요한 프로젝트에 권장되는 솔루션입니다.

## 소개 {#introduction}

이 문서에서는 AEM 내에서 편집 가능한 SPA 구성 요소를 구현하기 위해 모든 SPA 프레임워크가 수행해야 하는 일반적인 계약(예: AEM 지원 레이어)에 대해 설명합니다.

>[!NOTE]
>
>다음 요구 사항은 프레임워크에 독립적입니다. 이러한 요구 사항이 충족되면 모듈, 구성 요소 및 서비스로 구성된 프레임워크별 레이어를 제공할 수 있습니다.
>
>**이러한 요구 사항은 AEM의 반응 및 각 프레임워크에 대해 이미 충족되었습니다.** 이 블루프린트의 요구 사항은 AEM과 함께 사용할 다른 프레임워크를 구현하려는 경우에만 관련이 있습니다.

>[!CAUTION]
>
>AEM의 SPA 기능은 프레임워크에 독립적이지만 현재 React 및 Angular 프레임워크만 지원됩니다.

작성자가 AEM 페이지 편집기를 사용하여 단일 페이지 애플리케이션 프레임워크에 의해 노출된 데이터를 편집할 수 있도록 하려면, 프로젝트는 AEM 리포지토리 내의 응용 프로그램에 대해 저장된 데이터의 의미성을 나타내는 모델의 구조를 해석할 수 있어야 합니다. 이러한 목표를 달성하기 위해 프레임워크에 관계없이 다음 두 개의 라이브러리가 제공됩니다.Adobe `PageModelManager` Sign을 `ComponentMapping`사용하면

### PageModelManager {#pagemodelmanager}

라이브러리는 SPA 프로젝트에서 사용할 NPM 패키지로 제공됩니다. `PageModelManager` SPA와 함께 제공되며 데이터 모델 관리자 역할을 합니다.

SPA를 대신하여 실제 컨텐츠 구조를 나타내는 JSON 구조의 검색 및 관리를 추상화합니다. 또한 구성 요소를 다시 렌더링해야 하는 시기를 알려주기 위해 SPA와 동기화하는 작업도 담당합니다.

NPM 패키지 [@adobe/cq-spa-page-model-manager 참조](https://www.npmjs.com/package/@adobe/cq-spa-page-model-manager)

라이브러리를 초기화할 `PageModelManager`때 라이브러리는 먼저 제공된 앱 루트 모델(매개 변수, 메타 속성 또는 현재 URL을 통해)을 로드합니다. 라이브러리가 현재 페이지의 모델이 루트 모델의 일부가 아님을 식별하는 경우 이 모델을 하위 페이지의 모델로 포함합니다.

![page_model_consolidation](assets/page_model_consolidation.png)

### ComponentMapping {#componentmapping}

이 `ComponentMapping` 모듈은 프런트 엔드 프로젝트에 NPM 패키지로 제공됩니다. 프런트 엔드 구성 요소를 저장하고 SPA에서 프런트 엔드 구성 요소를 AEM 리소스 유형에 매핑할 수 있는 방법을 제공합니다. 이렇게 하면 애플리케이션의 JSON 모델을 구문 분석할 때 구성 요소의 동적 해상도를 사용할 수 있습니다.

모델에 있는 각 항목에는 AEM 리소스 유형을 표시하는 `:type` 필드가 포함되어 있습니다. 마운트되면 프런트 엔드 구성 요소는 기본 라이브러리에서 받은 모델 조각을 사용하여 자체 렌더링할 수 있습니다.

#### 동적 모델을 구성 요소 매핑으로 {#dynamic-model-to-component-mapping}

AEM용 Javascript SPA SDK에서 구성 요소에 대한 동적 모델 매핑이 발생하는 방법에 대한 자세한 내용은 SPA에 [대한 구성 요소 매핑에 대한 아티클을 참조하십시오](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

### 프레임워크별 레이어 {#framework-specific-layer}

각 프런트 엔드 프레임워크에 대해 세 번째 레이어를 구현해야 합니다. 이 세 번째 라이브러리는 기본 라이브러리와 상호 작용하는 작업을 담당하고 있으며 데이터 모델과 상호 작용할 수 있도록 잘 통합되어 있고 사용하기 쉬운 일련의 진입점을 제공합니다.

이 문서의 나머지 부분에서는 이 중간 프레임워크 특정 레이어의 요구 사항을 설명하고 프레임워크에 독립적이어야 합니다. 다음 요구 사항을 준수하여 프로젝트 구성 요소가 데이터 모델을 관리하는 기본 라이브러리와 상호 작용할 수 있도록 프레임워크별 레이어를 제공할 수 있습니다.

## 일반 개념 {#general-concepts}

### 페이지 모델 {#page-model}

페이지의 콘텐츠 구조는 AEM에 저장됩니다. 페이지 모델은 SPA 구성 요소를 매핑하고 인스턴스화하는 데 사용됩니다. SPA 개발자는 AEM 구성 요소에 매핑되는 SPA 구성 요소를 만듭니다. 이렇게 하려면 리소스 유형(또는 AEM 구성 요소의 경로)을 고유 키로 사용합니다.

SPA 구성 요소는 페이지 모델과 동기화되어야 하며 그에 따라 컨텐츠의 변경 사항과 함께 업데이트해야 합니다. 동적 구성 요소를 활용하는 패턴을 사용하여 제공된 페이지 모델 구조 다음의 구성 요소를 즉시 인스턴스화해야 합니다.

### 메타 필드 {#meta-fields}

페이지 모델은 Sling Model API를 기반으로 하는 JSON 모델 [익스포터를](https://sling.apache.org/documentation/bundles/models.html) 활용합니다. 내보낼 수 있는 슬링 모델은 기본 라이브러리가 데이터 모델을 해석할 수 있도록 다음 필드 목록을 표시합니다.

* `:type`:AEM 리소스 유형(기본값 = 리소스 유형)
* `:children`:현재 리소스의 계층 하위 항목입니다. 하위는 현재 리소스의 내부 컨텐츠에 속하지 않습니다(페이지를 나타내는 항목에서 찾을 수 있음).
* `:hierarchyType`:리소스의 계층적 유형입니다. 현재 페이지 유형을 `PageModelManager` 지원합니다.

* `:items`:현재 리소스의 하위 컨텐츠 리소스(중첩된 구조, 컨테이너에만 있음)
* `:itemsOrder`:순차 하위 구성요소 목록. JSON 지도 개체는 해당 필드의 순서를 보장하지 않습니다. 맵과 현재 배열을 모두 보유함으로써 API의 소비자는 두 구조의 이점을 얻을 수 있습니다
* `:path`:항목의 컨텐츠 경로(페이지를 나타내는 항목에 있음)

AEM [Content Services 시작하기를 참조하십시오.](https://helpx.adobe.com/experience-manager/kt/sites/using/content-services-tutorial-use.html)

### 프레임워크별 모듈 {#framework-specific-module}

문제를 분리하면 프로젝트 구현을 용이하게 하는 데 도움이 됩니다. 따라서 npm별 패키지를 제공해야 합니다. 이 패키지는 기본 모듈, 서비스 및 구성 요소를 집계하고 노출하는 책임을 집니다. 이러한 구성 요소는 데이터 모델 관리 로직을 캡슐화하고 프로젝트의 구성 요소에서 기대하는 데이터에 대한 액세스를 제공해야 합니다. 또한 모듈은 기본 라이브러리의 유용한 시작 지점을 전이적으로 노출할 책임이 있습니다.

Adobe는 라이브러리의 상호 운용성을 돕기 위해 프레임워크별 모듈에 다음 라이브러리를 번들로 묶을 것을 권장합니다. 필요한 경우 레이어는 기본 API를 캡슐화하고 프로젝트에 적용하기 전에 적용할 수 있습니다.

* [@adobe/cq-spa-page-model-manager](https://www.npmjs.com/package/@adobe/cq-spa-page-model-manager)
* [@adobe/cq-spa-component-mapping](https://www.npmjs.com/package/@adobe/cq-spa-component-mapping)

#### 구현 {#implementations}

#### 반응 {#react}

npm 모듈: [@adobe/cq-response-editable-components](https://www.npmjs.com/package/@adobe/cq-react-editable-components)

#### 각진 {#angular}

npm 모듈:곧 제공

## 기본 서비스 및 구성 요소 {#main-services-and-components}

다음 개체는 각 프레임워크에 적용되는 지침에 따라 구현해야 합니다. 프레임워크 아키텍처를 기반으로 구현은 다양하지만 설명된 기능을 제공해야 합니다.

### 모델 공급자 {#the-model-provider}

프로젝트 구성 요소는 모델의 조각에 대한 액세스를 모델 공급자에 위임해야 합니다. 그러면 모델 공급자가 모델의 지정된 조각에 대한 변경 사항을 수신하고 업데이트된 모델을 위임 구성 요소로 되돌립니다.

이렇게 하려면 모델 공급자가 에 등록해야 합니다 ` [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager)`. 그런 다음 변경 사항이 발생하면 업데이트된 데이터를 수신하여 위임 구성 요소에 전달합니다. 규칙에 따라 모델 조각을 운반할 위임 구성 요소에 사용할 수 있는 속성의 이름이 `cqModel`지정됩니다. 구현은 구성 요소에 이 속성을 제공하는 데 무료이지만 프레임워크 아키텍처와의 통합, 발견 가능성 및 사용 용이성과 같은 측면을 고려해야 합니다.

### 구성 요소 HTML Decorator {#the-component-html-decorator}

구성 요소 데코레이터는 페이지 편집기에서 필요한 일련의 데이터 속성 및 클래스 이름으로 각 구성 요소 인스턴스의 외부 HTML을 장식할 책임이 있습니다.

#### 구성 요소 선언 {#component-declaration}

다음 메타 데이터를 프로젝트의 구성 요소에서 만든 외부 HTML 요소에 추가해야 합니다. 페이지 편집기에서 해당 편집 구성을 검색할 수 있습니다.

* `data-cq-data-path`:Path to the resource relative to the `jcr:content`

#### 기능 선언 및 자리 표시자 편집 {#editing-capability-declaration-and-placeholder}

다음 메타데이터 및 클래스 이름은 프로젝트의 구성 요소에서 만든 외부 HTML 요소에 추가해야 합니다. 페이지 편집기에서 관련 기능을 제공할 수 있습니다.

* `cq-placeholder`:빈 구성 요소의 자리 표시자를 식별하는 클래스 이름
* `data-emptytext`:구성 요소 인스턴스가 비어 있을 때 오버레이에서 표시할 레이블

**빈 구성 요소에 대한 자리 표시자**

각 구성 요소가 비어 있는 것으로 식별될 때 외부 HTML 요소를 자리 표시자 및 관련 오버레이와 관련된 데이터 특성 및 클래스 이름으로 장식 기능을 사용하여 확장해야 합니다.

**구성 요소의 비어 있음**

* 구성 요소가 논리적으로 비어 있습니까?
* 구성 요소가 비어 있을 때 오버레이에서 표시되는 레이블은 무엇입니까?

### 컨테이너 {#container}

컨테이너는 하위 구성 요소를 포함하고 렌더링하기 위한 구성 요소입니다. 이렇게 하려면 컨테이너가 모델의 `:itemsOrder`및 `:items` 속성을 반복합니다 `:children` .

컨테이너는 라이브러리의 저장소에서 자식 구성 요소를 동적으로 가져옵니다. ` [ComponentMapping](/help/sites-developing/spa-blueprint.md#componentmapping)` 그런 다음 컨테이너는 모델 공급자 기능으로 하위 구성 요소를 확장하고 마지막으로 인스턴스화합니다.

### 페이지 {#page}

구성 `Page` 요소는 구성 요소를 확장합니다 `Container` . 컨테이너는 하위 페이지를 포함한 하위 구성 요소를 포함하고 렌더링하기 위한 구성 요소입니다. 이렇게 하려면 컨테이너가 모델의 `:itemsOrder`속성, `:items`속성을 반복합니다 `:children` . 구성 `Page` 요소는 ComponentMapping 라이브러리의 저장소에서 자식 구성 요소를 동적으로 [가져옵니다](/help/sites-developing/spa-blueprint.md#componentmapping) . 하위 구성 요소를 인스턴스화하는 `Page` 작업은 에서 담당합니다.

### 응답형 격자 {#responsive-grid}

응답형 격자 구성 요소는 컨테이너입니다. 여기에는 열을 나타내는 모델 공급자의 특정 변형이 포함되어 있습니다. 응답형 격자 및 해당 열은 프로젝트 구성 요소의 외부 HTML 요소를 모델에 포함된 특정 클래스 이름으로 꾸밀 책임이 있습니다.

응답형 격자 구성 요소는 복잡하고 거의 사용자 지정되지 않았으므로 AEM 상대방과 미리 매핑되어야 합니다.

#### 특정 모델 필드 {#specific-model-fields}

* `gridClassNames:` 응답형 격자에 대해 클래스 이름을 제공했습니다.
* `columnClassNames:` 응답형 열에 대한 클래스 이름을 제공했습니다.

참고 항목: npm resource [@adobe/cq-response-editable-components#srccomponentsResponsiveGridjsx](https://www.npmjs.com/package/@adobe/cq-react-editable-components#srccomponentsresponsivegridjsx)

#### 응답형 격자의 자리 표시자 {#placeholder-of-the-reponsive-grid}

SPA 구성 요소는 응답형 격자와 같은 그래픽 컨테이너에 매핑되며 컨텐츠를 작성할 때 가상 하위 자리 표시자를 추가해야 합니다. 페이지 편집기에서 SPA의 컨텐츠를 작성하고 있는 경우 해당 컨텐츠는 iframe을 사용하여 편집기에 삽입되고 `data-cq-editor` 속성이 해당 컨텐츠의 문서 노드에 추가됩니다. 속성이 `data-cq-editor` 있는 경우, 컨테이너에는 새 구성 요소를 페이지에 삽입할 때 작성자가 상호 작용하는 영역을 나타내는 HTMLElement가 포함되어야 합니다.

예:

```
<div data-cq-data-path={"path/to/the/responsivegrid/*"} className="new section aem-Grid-newComponent"/>
```

>[!NOTE]
>
>이 예제에서 사용되는 클래스 이름은 현재 페이지 편집기에서 필요합니다.
>
>* `"new section"`:현재 요소가 컨테이너의 자리 표시자임을 나타냅니다.
>* `"aem-Grid-newComponent"`:레이아웃 작성을 위한 구성 요소 정규화
>



#### Component Mapping {#component-mapping}

기본 [구성 요소 매핑](/help/sites-developing/spa-blueprint.md#componentmapping) 라이브러리와 해당 `MapTo` 함수를 캡슐화하고 확장하여 현재 구성 요소 클래스와 함께 제공된 편집 구성에 관련된 기능을 제공할 수 있습니다.

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

위의 구현에서 프로젝트 구성 요소는 구성 요소 매핑 저장소에 실제로 등록되기 전에 비어 있는 [기능으로 확장됩니다](/help/sites-developing/spa-blueprint.md#componentmapping) . 이렇게 하려면 라이브러리를 캡슐화하고 확장하여 구성 개체에 대한 지원을 도입합니다. ` [ComponentMapping](/content.md#main-pars_header_906602219)` `EditConfig`

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

## 페이지 편집기를 사용한 계약 {#contract-wtih-the-page-editor}

프로젝트 구성 요소는 편집자가 이러한 구성 요소와 상호 작용할 수 있도록 다음과 같은 데이터 속성을 최소한 생성해야 합니다.

* `data-cq-data-path`:구성 요소의 상대 경로( `PageModel` (예: `"root/responsivegrid/image"`). 이 속성은 페이지에 추가할 수 없습니다.

요약하면, 페이지 편집기로 해석하려면 프로젝트 구성 요소는 다음 계약을 존중해야 합니다.

* 프런트 엔드 구성 요소 인스턴스를 AEM 리소스에 연결하는 데 필요한 특성을 제공합니다.
* 빈 자리 표시자를 만들 수 있도록 필요한 일련의 특성과 클래스 이름을 제공합니다.
* 에셋을 드래그하여 놓을 수 있도록 필요한 클래스 이름을 제공합니다.

### 일반적인 HTML 요소 구조 {#typical-html-element-structure}

다음 조각은 페이지 컨텐츠 구조의 일반적인 HTML 표현을 보여줍니다. 다음은 몇 가지 중요한 사항입니다.

* 응답형 격자 요소에는 `aem-Grid--`
* 응답형 열 요소에는 `aem-GridColumn--`
* 상위 격자의 열이기도 한 응답형 격자는 이전 두 개의 접두사가 동일한 요소에 나타나지 않는 것과 같이 래핑됩니다
* 편집 가능한 리소스에 해당하는 요소에는 `data-cq-data-path` 속성이 포함됩니다. 이 [문서의 페이지 편집기로](#contract-wtih-the-page-editor) 계약 섹션을 참조하십시오.

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

앱이 라우팅을 소유합니다. 프런트 엔드 개발자는 먼저 내비게이션 구성 요소(AEM 탐색 구성 요소에 매핑됨)를 구현해야 합니다. 이 구성 요소는 컨텐츠 조각을 표시하거나 숨길 일련의 경로와 함께 사용할 URL 링크를 렌더링합니다.

기본 [ `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) ` [ModelRouter](/help/sites-developing/spa-routing.md)` 라이브러리와 해당 모듈(기본적으로 활성화됨)은 사전 페치 및 지정된 리소스 경로와 연결된 모델에 대한 액세스 권한을 제공합니다.

두 개체는 라우팅 개념과 관련이 있지만 ` [ModelRouter](/help/sites-developing/spa-routing.md)` 는 현재 응용 프로그램 상태와 동기화되어 있는 데이터 모델을 ` [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager)` 불러와야 합니다.

자세한 내용은 SPA [모델](/help/sites-developing/spa-routing.md) 라우팅 문서를 참조하십시오.

## SPA in Action {#spa-in-action}

AEM에서 SPA 시작하기 문서를 계속 진행하여 간단한 SPA가 어떻게 작동하는지 직접 [확인하고 SPA를 사용해 보십시오](/help/sites-developing/spa-getting-started-react.md).

## 추가 읽기 {#further-reading}

AEM의 SPA에 대한 자세한 내용은 다음 문서를 참조하십시오.

* [AEM](/help/sites-developing/spa-overview.md) 및 통신 모델의 SPA에 대한 개요에 대한 SPA 작성 개요
* [AEM에서 SPA](/help/sites-developing/spa-getting-started-react.md) 시작하기를 참조하십시오.
