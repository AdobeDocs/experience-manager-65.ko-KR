---
title: AEM에서 SPA 시작하기 - React
seo-title: AEM에서 SPA 시작하기 - React
description: 이 문서에서는 샘플 SPA 응용 프로그램을 소개하고 이를 통합하는 방법을 설명하며 React 프레임워크를 사용하여 직접 SPA을 빠르게 익힐 수 있도록 합니다.
seo-description: 이 문서에서는 샘플 SPA 응용 프로그램을 소개하고 이를 통합하는 방법을 설명하며 React 프레임워크를 사용하여 직접 SPA을 빠르게 익힐 수 있도록 합니다.
uuid: 2beca277-a381-4482-99f6-85005d826d06
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: cc1e5c20-cc9c-4222-8a11-ec5a963d4466
docset: aem65
translation-type: tm+mt
source-git-commit: 4c9a0bd73e8d87d3869c6a133f5d1049f8430cd1
workflow-type: tm+mt
source-wordcount: '1203'
ht-degree: 3%

---


# AEM에서 SPA 시작하기 - React{#getting-started-with-spas-in-aem-react}

단일 페이지 애플리케이션(SPA)을 통해 웹 사이트 사용자에게 매력적인 경험을 제공할 수 있습니다. 개발자는 SPA 프레임워크을 사용하여 사이트를 구축하고자 하며, 작성자는 SPA 프레임워크을 사용하여 구축된 사이트에서 AEM의 컨텐츠를 매끄럽게 편집하고자 합니다.

SPA 저작 기능은 AEM 내에서 SPA을 지원하는 포괄적인 솔루션을 제공합니다. 이 문서에서는 Responsive 프레임워크에 대한 간소화된 SPA 애플리케이션을 소개하고, 이를 통합하는 방법을 설명하며, SPA을 빠르게 시작할 수 있도록 해줍니다.

>[!NOTE]
>
>이 문서는 Response 프레임워크를 기반으로 합니다. 각도 프레임워크에 해당하는 문서는 AEM에서 SPA 시작하기 - 각도[를 참조하십시오.](/help/sites-developing/spa-getting-started-angular.md)

>[!NOTE]
>
>SPA 편집기는 SPA 프레임워크 기반의 클라이언트측 렌더링(예: 반응형 또는 각도)이 필요한 프로젝트에 권장되는 솔루션입니다.

## 소개 {#introduction}

이 문서는 간단한 SPA의 기본적인 기능과 최소 기능을 사용하여 실행할 수 있도록 알아야 하는 사항을 요약합니다.

AEM에서 SPA을 사용하는 방법에 대한 자세한 내용은 다음 문서를 참조하십시오.

* [SPA 소개 및 연습](/help/sites-developing/spa-walkthrough.md)
* [SPA 제작 소개](/help/sites-developing/spa-overview.md)
* [SPA 블루프린트](/help/sites-developing/spa-blueprint.md)

>[!NOTE]
>
>SPA 내에서 컨텐츠를 저작할 수 있으려면 컨텐츠가 AEM에 저장되어 컨텐츠 모델에 의해 노출되어야 합니다.
>
>AEM 외부에서 개발된 SPA은 컨텐트 모델 계약을 준수하지 않으면 저작권을 상실할 것이다.

이 문서는 React 프레임워크를 사용하여 만든 간소화된 SPA의 구조를 설명하고 작동 방식을 설명하여 SPA에 이러한 이해를 적용할 수 있습니다.

## 종속성, 구성 및 빌드 {#dependencies-configuration-and-building}

예상 응답 종속성 외에도 샘플 SPA은 추가 라이브러리를 활용하여 SPA을 보다 효율적으로 만들 수 있습니다.

### 종속성 {#dependencies}

`package.json` 파일은 전체 SPA 패키지의 요구 사항을 정의합니다. 작업 중인 SPA에 대한 최소 AEM 종속성은 여기에 나와 있습니다.

```
  "dependencies": {
    "@adobe/aem-react-editable-components": "~1.0.4",
    "@adobe/aem-spa-component-mapping": "~1.0.5",
    "@adobe/aem-spa-page-model-manager": "~1.0.3"
  }
```

이 예제는 React 프레임워크를 기반으로 하므로 `package.json` 파일에 의무적인 2개의 React 특정 종속성이 있습니다.

```
react
 react-dom
```

`aem-clientlib-generator`은(는) 빌드 프로세스의 일부로 클라이언트 라이브러리를 자동으로 만드는 데 사용됩니다.

`"aem-clientlib-generator": "^1.4.1",`

자세한 내용은 GitHub](https://github.com/wcm-io-frontend/aem-clientlib-generator)에서 [을 참조하십시오.

>[!CAUTION]
>
>필요한 `aem-clientlib-generator`의 최소 버전은 1.4.1.

`aem-clientlib-generator`은 다음과 같이 `clientlib.config.js` 파일에 구성됩니다.

```
module.exports = {
    // default working directory (can be changed per 'cwd' in every asset option)
    context: __dirname,

    // path to the clientlib root folder (output)
    clientLibRoot: "./../content/jcr_root/apps/my-react-app/clientlibs",

    libs: {
        name: "my-react-app",
        allowProxy: true,
        categories: ["my-react-app"],
        embed: ["my-react-app.responsivegrid"],
        jsProcessor: ["min:gcc"],
        serializationFormat: "xml",
        assets: {
            js: [
                "dist/**/*.js"
            ],
            css: [
                "dist/**/*.css"
            ]
        }
    }
};
```

### {#building} 빌드

실제로 앱을 빌드하면 자동 클라이언트 라이브러리 생성을 위한 aem-clientlib-generator 외에도 전달을 위해 [Webpack](https://webpack.js.org/)이 활용됩니다. 따라서 빌드 명령은 다음과 같습니다.

`"build": "webpack && clientlib --verbose"`

패키지가 빌드되면 AEM 인스턴스에 패키지를 업로드할 수 있습니다.

### AEM 프로젝트 전형 {#aem-project-archetype}

모든 AEM 프로젝트는 React 또는 Angular를 사용하여 SPA 프로젝트를 지원하고 SPA SDK를 활용하는 [AEM Project Tranype](https://docs.adobe.com/content/help/ko-KR/experience-manager-core-components/using/developing/archetype/overview.html)을 활용해야 합니다.

## 응용 프로그램 구조 {#application-structure}

앞에서 설명한 바와 같이 종속성 및 앱 빌드를 포함하면 AEM 인스턴스에 업로드할 수 있는 작업 중인 SPA 패키지가 표시됩니다.

이 문서의 다음 섹션에서는 AEM의 구조, 애플리케이션을 유도하는 중요한 파일 및 이러한 파일을 함께 사용하는 방법을 살펴봅니다.

간소화된 이미지 구성 요소가 예로 사용되지만 응용 프로그램의 모든 구성 요소는 동일한 개념을 기반으로 합니다.

### index.js {#index-js}

SPA의 시작 지점은 중요한 컨텐츠에 초점을 맞추기 위해 여기에 간소화된 `index.js` 파일입니다.

```
import ReactDOM from 'react-dom';
import App from './App';
import { ModelManager, Constants } from "@adobe/aem-spa-page-model-manager";

...

ModelManager.initialize().then((pageModel) => {
ReactDOM.render(
    <App cqChildren={pageModel[Constants.CHILDREN_PROP]} cqItems={pageModel[Constants.ITEMS_PROP]} cqItemsOrder={pageModel[Constants.ITEMS_ORDER_PROP]} cqPath={ModelManager.rootPath} locationPathname={ window.location.pathname }/>
, document.getElementById('page'));

});
```

`index.js`의 기본 함수는 `ReactDOM.render` 함수를 활용하여 DOM에서 애플리케이션을 주입할 위치를 결정하는 것입니다.

이것은 이 예제 앱에만 국한되지 않고 이 함수의 표준 사용입니다.

#### 정적 인스턴스화 {#static-instantiation}

구성 요소 템플릿(예: JSX)을 사용하여 구성 요소가 정적으로 인스턴스화되는 경우 이 값은 모델에서 구성 요소의 속성으로 전달되어야 합니다.

### App.js {#app-js}

앱을 렌더링하면 `index.js`은(는) 중요한 콘텐츠에 집중할 수 있도록 여기에 간소화된 버전으로 표시되는 `App.js`을 호출합니다.

```
import {Page, withModel } from '@adobe/aem-react-editable-components';

...

class App extends Page {
...
}

export default withModel(App);
```

`App.js` 기본적으로 에서는 앱을 구성하는 루트 구성 요소를 래핑합니다. 앱의 시작 지점은 페이지입니다.

### Page.js {#page-js}

페이지를 렌더링하면, `App.js`은 여기에 나열된 `Page.js`을(를) 단순화된 버전으로 호출합니다.

```
import {Page, MapTo, withComponentMappingContext } from "@adobe/aem-react-editable-components";

...

class AppPage extends Page {
...
}

MapTo('my-react-app/components/structure/page')(withComponentMappingContext(AppPage));
```

이 예제에서 `AppPage` 클래스는 `Page`을(를) 확장합니다. 여기에는 여기에 사용할 수 있는 내부 내용 메서드가 포함되어 있습니다.

`Page`은 페이지 모델의 JSON 표현을 인제스트하고 페이지의 각 요소를 래핑/장식하기 위한 컨텐츠를 처리합니다. `Page`에 대한 자세한 내용은 [SPA Blueprint](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501) 문서에 있습니다.

### Image.js {#image-js}

페이지를 렌더링하면 여기에 표시된 대로 `Image.js`과 같은 구성 요소를 렌더링할 수 있습니다.

```
import React, {Component} from 'react';
import {MapTo} from '@adobe/aem-react-editable-components';

require('./Image.css');

const ImageEditConfig = {

    emptyLabel: 'Image',

    isEmpty: function() {
        return !this.props || !this.props.src || this.props.src.trim().length < 1;
    }
};

class Image extends Component {

    render() {
        return (<img src={this.props.src}>);
    }
}

MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);
```

AEM의 기본 아이디어는 SPA 구성 요소를 AEM 구성 요소에 매핑하고 컨텐츠가 수정될 때(또는 그 반대로) 구성 요소를 업데이트하는 것입니다. 이 통신 모델에 대한 요약은 [SPA 편집기 개요](/help/sites-developing/spa-overview.md) 문서를 참조하십시오.

`MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);`

`MapTo` 메서드는 SPA 구성 요소를 AEM 구성 요소에 매핑합니다. 단일 문자열 또는 문자열 배열을 사용할 수 있습니다.

`ImageEditConfig` 편집기가 자리 표시자를 생성하는 데 필요한 메타데이터를 제공하여 구성 요소의 작성 기능을 활성화하는 데 기여하는 구성 개체입니다.

내용이 없으면 빈 컨텐츠를 나타내는 자리 표시자로 레이블이 제공됩니다.

#### 동적으로 전달된 속성 {#dynamically-passed-properties}

모델에서 나오는 데이터는 구성 요소의 속성으로 동적으로 전달됩니다.

## 편집 가능한 내용 내보내기 {#exporting-editable-content}

구성 요소를 내보내고 편집 가능한 상태로 유지할 수 있습니다.

```
import React, { Component } from 'react';
import { MapTo } from '@adobe/aem-react-editable-components';

...

const EditConfig = {...}

class PageClass extends Component {...};

...

export default MapTo('my-react-app/react/components/structure/page')(PageClass, EditConfig);
```

`MapTo` 함수는 `Component`을 반환합니다. 이 결과는 작성을 가능하게 하는 클래스 이름과 특성을 사용하여 제공된 `PageClass`을 확장하는 컴포지션의 결과입니다. 이 구성 요소를 내보내 나중에 응용 프로그램의 마크업에서 인스턴스화할 수 있습니다.

`MapTo` 또는 `withModel` 함수를 사용하여 내보낼 때 `Page` 구성 요소는 최신 페이지 모델 버전이나 해당 페이지 모델의 정확한 위치에 대한 표준 구성 요소에 액세스할 수 있는 `ModelProvider` 구성 요소로 래핑됩니다.

자세한 내용은 [SPA Blueprint 문서](/help/sites-developing/spa-blueprint.md#main-pars-header-329251743)를 참조하십시오.

>[!NOTE]
>
>기본적으로 `withModel` 함수를 사용할 때 구성 요소의 전체 모델을 받게 됩니다.

## SPA 구성 요소 간 정보 공유 {#sharing-information-between-spa-components}

단일 페이지 애플리케이션 내의 구성 요소가 정보를 공유하려면 정기적으로 필요합니다. 다음과 같이 복잡성이 증가하는 데 권장되는 여러 방법이 있습니다.

* **옵션 1:** 반응 컨텍스트를 사용하여 로직과 브로드캐스트를 필요한 구성 요소로 중앙에서 처리합니다.
* **옵션 2:** 리덕스와 같은 상태 라이브러리를 사용하여 구성 요소 상태를 공유합니다.
* **옵션 3:** 컨테이너 구성 요소를 사용자 지정하고 확장하여 객체 계층 구조를 활용합니다.

## 다음 단계 {#next-steps}

직접 SPA을 만드는 단계별 안내는 [AEM SPA Editor 시작하기 - WKND 이벤트 자습서](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html)를 참조하십시오.

AEM용 SPA을 개발하기 위해 자신을 구성하는 방법에 대한 자세한 내용은 [AEM용 SPA 개발](/help/sites-developing/spa-architecture.md) 문서를 참조하십시오.

동적 모델을 구성 요소로 매핑하는 방법 및 AEM에서 작동하는 방식에 대한 자세한 내용은 SPA[의 구성 요소 매핑에 대한 동적 모델 집필을 참조하십시오.](/help/sites-developing/spa-dynamic-model-to-component-mapping.md)

React 또는 Angular 이외의 프레임워크를 위해 AEM에서 SPA을 구현하거나 AEM용 SPA SDK의 작동 방식을 자세히 살펴보려면 [SPA Blueprint](/help/sites-developing/spa-blueprint.md) 문서를 참조하십시오.
