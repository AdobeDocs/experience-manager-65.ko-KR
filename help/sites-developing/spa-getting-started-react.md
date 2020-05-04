---
title: AEM에서 SPA 시작하기 - 반응
seo-title: AEM에서 SPA 시작하기 - 반응
description: 본 문서는 샘플 SPA 응용 프로그램을 소개하고 SPA가 어떻게 구성되어 있는지를 설명하며 Repact 프레임워크를 사용하여 신속하게 자체 SPA를 바로 시작할 수 있도록 합니다.
seo-description: 본 문서는 샘플 SPA 응용 프로그램을 소개하고 SPA가 어떻게 구성되어 있는지를 설명하며 Repact 프레임워크를 사용하여 신속하게 자체 SPA를 바로 시작할 수 있도록 합니다.
uuid: 2beca277-a381-4482-99f6-85005d826d06
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: cc1e5c20-cc9c-4222-8a11-ec5a963d4466
docset: aem65
translation-type: tm+mt
source-git-commit: 590dc4464182d4baf8293e7bb0774ce92971c0af

---


# AEM에서 SPA 시작하기 - 반응{#getting-started-with-spas-in-aem-react}

단일 페이지 애플리케이션(SPA)을 통해 웹 사이트 사용자에게 매력적인 경험을 제공할 수 있습니다. 개발자는 SPA 프레임워크를 사용하여 사이트를 구축하고, 작성자는 AEM 내에서 SPA 프레임워크를 사용하여 구축한 사이트에 맞는 컨텐츠를 완벽하게 편집하고자 합니다.

SPA 작성 기능은 AEM 내의 SPA를 지원하는 포괄적인 솔루션을 제공합니다. 이 문서는 Reperimate 프레임워크에 간소화된 SPA 애플리케이션을 제시하며, 이를 어떻게 취합하여 SPA를 신속하게 바로 사용할 수 있도록 합니다.

>[!NOTE]
>
>이 문서는 Responsive 프레임워크를 기반으로 합니다. Angular 프레임워크에 해당하는 문서는 AEM에서 [SPA 시작하기 - 각형을 참조하십시오](/help/sites-developing/spa-getting-started-angular.md).

>[!NOTE]
>
>SPA 편집기는 SPA 프레임워크 기반의 클라이언트측 렌더링(예: 반응 또는 각도)이 필요한 프로젝트에 권장되는 솔루션입니다.

## 소개 {#introduction}

이 문서는 간단한 SPA의 기본적인 기능과 필요한 최소 기능을 요약해 놓은 것입니다.

AEM에서 SPA가 작동하는 방식에 대한 자세한 내용은 다음 문서를 참조하십시오.

* [SPA 소개 및 연습](/help/sites-developing/spa-walkthrough.md)
* [SPA 저작 소개](/help/sites-developing/spa-overview.md)
* [SPA 블루프린트](/help/sites-developing/spa-blueprint.md)

>[!NOTE]
>
>SPA 내에서 컨텐츠를 저작할 수 있으려면 컨텐츠를 AEM에 저장하고 컨텐츠 모델에 의해 노출되어야 합니다.
>
>AEM 외부에서 개발된 SPA는 컨텐츠 모델 계약을 준수하지 않는 경우 인증할 수 없습니다.

본 문서는 React 프레임워크를 사용하여 만든 간소화된 SPA의 구조를 자세히 설명하고 사용 방법을 설명함으로써 SPA에 이러한 이해를 적용할 수 있습니다.

## 종속성, 구성 및 작성 {#dependencies-configuration-and-building}

예상 Responsive 종속성 외에도 샘플 SPA는 추가 라이브러리를 활용하여 SPA를 보다 효율적으로 만들 수 있습니다.

### 종속성 {#dependencies}

이 `package.json` 파일은 전체 SPA 패키지의 요구 사항을 정의합니다. 작업 SPA에 대한 최소 AEM 종속성이 여기에 나열되어 있습니다.

```
  "dependencies": {
    "@adobe/cq-react-editable-components": "~1.0.3",
    "@adobe/cq-spa-component-mapping": "~1.0.3",
    "@adobe/cq-spa-page-model-manager": "~1.0.4"
  }
```

이 예는 Response 프레임워크를 기반으로 하므로 `package.json` 파일에 의무적인 두 개의 Response 관련 종속성이 있습니다.

```
react
 react-dom
```

빌드 프로세스 `aem-clientlib-generator` 의 일부로 클라이언트 라이브러리를 자동으로 만드는 데 사용됩니다.

`"aem-clientlib-generator": "^1.4.1",`

자세한 내용은 GitHub [에서 확인할 수 있습니다](https://github.com/wcm-io-frontend/aem-clientlib-generator).

>[!CAUTION]
>
>필요한 최소 버전은 `aem-clientlib-generator` 1.4.1입니다.

파일 `aem-clientlib-generator` 에 다음과 같이 `clientlib.config.js` 구성됩니다.

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

### Building {#building}

실제로 앱을 빌드하면 자동 클라이언트 라이브러리 [를](https://webpack.js.org/) 만들기 위한 aem-clientlib-generator 외에도 전달을 위한 Webpack이 활용됩니다. 따라서 빌드 명령은 다음과 같습니다.

`"build": "webpack && clientlib --verbose"`

일단 빌드하면 패키지를 AEM 인스턴스에 업로드할 수 있습니다.

### AEM 프로젝트 전형 {#aem-project-archetype}

모든 AEM 프로젝트는 React 또는 Angular를 사용하여 SPA 프로젝트를 [지원하고 SPA SDK를 활용하는 AEM Project 원형형을 활용해야](https://docs.adobe.com/content/help/ko-KR/experience-manager-core-components/using/developing/archetype/overview.html)합니다.

## 애플리케이션 구조 {#application-structure}

이전에 설명한 대로 종속성 및 앱 빌드를 포함시키면 AEM 인스턴스에 업로드할 수 있는 작업 SPA 패키지가 남습니다.

이 문서의 다음 섹션에서는 AEM의 SPA가 구조화된 방식, 애플리케이션을 구동하는 중요한 파일 및 이러한 SPA가 어떻게 연동되는지 살펴볼 수 있습니다.

간소화된 이미지 구성 요소를 예로 사용하지만 애플리케이션의 모든 구성 요소는 동일한 개념을 기반으로 합니다.

### index.js {#index-js}

SPA의 진입점은 중요한 컨텐츠에 초점을 맞추기 위해 여기에 나와 있는 `index.js` 파일을 말합니다.

```
import ReactDOM from 'react-dom';
import App from './App';
import { ModelManager, Constants } from "@adobe/cq-spa-page-model-manager";

...

ModelManager.initialize().then((pageModel) => {
ReactDOM.render(
    <App cqChildren={pageModel[Constants.CHILDREN_PROP]} cqItems={pageModel[Constants.ITEMS_PROP]} cqItemsOrder={pageModel[Constants.ITEMS_ORDER_PROP]} cqPath={ModelManager.rootPath} locationPathname={ window.location.pathname }/>
, document.getElementById('page'));

});
```

DOM `index.js` 에서 애플리케이션을 주입할 위치를 결정하는 기능은 `ReactDOM.render` 함수를 활용하는 것입니다.

이 예제 앱에서만 사용되는 것이 아니라 이 함수의 표준 사용입니다.

#### 정적 인스턴스화 {#static-instantiation}

구성 요소 템플릿(예: JSX)을 사용하여 구성 요소가 정적으로 인스턴스화될 경우, 값은 모델에서 구성 요소의 속성으로 전달되어야 합니다.

### App.js {#app-js}

이 앱을 렌더링하면 `index.js` 호출이 `App.js`중요한 컨텐츠에 초점을 맞춰 간소화된 버전으로 표시됩니다.

```
import {Page, withModel } from '@adobe/cq-react-editable-components';

...

class App extends Page {
...
}

export default withModel(App);
```

`App.js` 기본적으로 앱을 구성하는 루트 구성 요소를 둘러싸는 데 사용됩니다. 앱의 시작 지점이 페이지입니다.

### Page.js {#page-js}

페이지를 렌더링하면 `App.js` 여기에 나열된 간단한 버전 `Page.js` 으로 호출이 수행됩니다.

```
import {Page, MapTo, withComponentMappingContext } from "@adobe/cq-react-editable-components";

...

class AppPage extends Page {
...
}

MapTo('my-react-app/components/structure/page')(withComponentMappingContext(AppPage));
```

이 예제에서 `AppPage` 클래스는 확장되어 사용할 수 `Page`있는 내부 컨텐츠 메서드를 포함합니다.

페이지 모델의 JSON 표현을 `Page` 인제스트하고 페이지의 각 요소를 둘러싸거나 장식하기 위해 컨텐츠를 처리합니다. 자세한 내용은 `Page` SPA Blueprint [](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501)문서를 참조하십시오.

### Image.js {#image-js}

페이지를 렌더링하면 여기에 표시된 것과 같은 구성 요소 `Image.js` 가 렌더링될 수 있습니다.

```
import React, {Component} from 'react';
import {MapTo} from '@adobe/cq-react-editable-components';

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

AEM의 SPA에 대한 중앙 아이디어는 SPA 구성 요소를 AEM 구성 요소에 매핑하고 컨텐츠가 수정될 때(또는 그 반대로) 구성 요소를 업데이트하는 것입니다. 이 통신 모델에 대한 요약 내용은 [SPA Editor](/help/sites-developing/spa-overview.md) Overview 문서를 참조하십시오.

`MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);`

이 `MapTo` 방법은 SPA 구성 요소를 AEM 구성 요소에 매핑합니다. 단일 문자열 또는 문자열 배열을 사용할 수 있습니다.

`ImageEditConfig` 는 편집기가 자리 표시자를 생성하는 데 필요한 메타데이터를 제공하여 구성 요소의 작성 기능을 활성화하는 데 도움이 되는 구성 개체입니다.

콘텐트가 없으면 빈 콘텐트를 나타내는 자리 표시자로 레이블이 제공됩니다.

#### 동적으로 전달된 속성 {#dynamically-passed-properties}

모델에서 나오는 데이터는 구성 요소의 속성으로 동적으로 전달됩니다.

## 편집 가능한 컨텐츠 내보내기 {#exporting-editable-content}

구성 요소를 내보내고 편집 가능한 상태로 유지할 수 있습니다.

```
import React, { Component } from 'react';
import { MapTo } from '@cq/cq-react-editable-components';

...

const EditConfig = {...}

class PageClass extends Component {...};

...

export default MapTo('my-react-app/react/components/structure/page')(PageClass, EditConfig);
```

이 `MapTo` 함수는 작성을 가능하게 해주는 클래스 이름 및 특성과 함께 제공된 `Component` `PageClass` 을 확장하는 컴포지션의 결과인 a를 반환합니다. 이 구성 요소를 내보내 나중에 응용 프로그램의 마크업에서 인스턴스화할 수 있습니다.

구성 요소 `MapTo` 나 `withModel` 함수를 사용하여 내보내면 `Page` 구성 요소는 최신 페이지 모델 버전 또는 해당 페이지 모델의 정확한 위치에 대한 표준 구성 요소에 액세스할 수 있는 `ModelProvider` 구성 요소로 래핑됩니다.

자세한 내용은 [SPA Blueprint 문서를 참조하십시오](/help/sites-developing/spa-blueprint.md#main-pars-header-329251743).

>[!NOTE]
>
>기본적으로 함수를 사용할 때 구성 요소의 전체 모델을 `withModel` 받습니다.

## SPA 구성 요소 간 정보 공유 {#sharing-information-between-spa-components}

단일 페이지 애플리케이션 내의 구성 요소가 정보를 공유하려면 정기적으로 필요합니다. 다음과 같이 복잡성이 증가하는 여러 가지 권장 방법으로 이 작업을 수행할 수 있습니다.

* **옵션 1:** 상황에 따라 컨텍스트를 사용하여 로직과 브로드캐스트를 필요한 구성 요소로 중앙에서 제어할 수 있습니다.
* **옵션 2:** Redux와 같은 상태 라이브러리를 사용하여 구성 요소 상태를 공유합니다.
* **옵션 3:** 컨테이너 구성 요소를 사용자 지정하고 확장하여 객체 계층 구조를 활용할 수 있습니다.

## 다음 단계 {#next-steps}

자체 SPA를 만드는 단계별 가이드는 AEM SPA 편집기 [시작하기 - WKND 이벤트 자습서를 참조하십시오](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html).

AEM용 SPA를 개발하기 위해 자신을 구성하는 방법에 대한 자세한 내용은 AEM용 SPA [개발 문서를 참조하십시오](/help/sites-developing/spa-architecture.md).

동적 모델-구성 요소 매핑 및 AEM의 SPA 내에서 작동하는 방식에 대한 자세한 내용은 SPA에 대한 구성 요소 매핑 [에 대한 아티클을 참조하십시오](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

AEM에서 React 또는 Angular 이외의 프레임워크에 대해 SPA를 구현하거나 AEM용 SPA SDK 작동 방식을 자세히 살펴보려면 [SPA Blueprint](/help/sites-developing/spa-blueprint.md) 문서를 참조하십시오.
