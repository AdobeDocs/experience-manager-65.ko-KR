---
title: AEM에서 SPA 시작하기 - 반응
seo-title: AEM에서 SPA 시작하기 - 반응
description: 이 문서에서는 샘플 SPA 애플리케이션을 소개하고 이를 통합하는 방법을 설명하며 React 프레임워크를 사용하여 신속하게 자체 SPA를 사용할 수 있도록 합니다.
seo-description: 이 문서에서는 샘플 SPA 애플리케이션을 소개하고 이를 통합하는 방법을 설명하며 React 프레임워크를 사용하여 신속하게 자체 SPA를 사용할 수 있도록 합니다.
uuid: 2beca277-a381-4482-99f6-85005d826d06
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: cc1e5c20-cc9c-4222-8a11-ec5a963d4466
docset: aem65
translation-type: tm+mt
source-git-commit: 2dad220d6593ed542816f8a97b0d4b44f0d57876

---


# AEM에서 SPA 시작하기 - 반응{#getting-started-with-spas-in-aem-react}

단일 페이지 애플리케이션(SPA)을 통해 웹 사이트 사용자에게 매력적인 경험을 제공할 수 있습니다. 개발자는 SPA 프레임워크를 사용하여 사이트를 구축하고자 하며 작성자는 AEM 내에서 SPA 프레임워크를 사용하여 구축한 사이트에 대한 컨텐츠를 완벽하게 편집하고자 합니다.

SPA 제작 기능은 AEM 내의 SPA를 지원하는 포괄적인 솔루션을 제공합니다. 이 문서에서는 React 프레임워크에 간소화된 SPA 애플리케이션을 소개하며, 이를 통합하는 방법을 설명합니다. 이를 통해 SPA를 신속하게 바로 사용할 수 있습니다.

>[!NOTE]
>
>이 문서는 Response 프레임워크를 기반으로 합니다. Angular 프레임워크에 해당하는 문서는 AEM에서 [SPA 시작하기 - Angular를 참조하십시오](/help/sites-developing/spa-getting-started-angular.md).

>[!NOTE]
>
>SPA 편집기는 SPA 프레임워크 기반의 클라이언트측 렌더링(예: 반응 또는 각도)이 필요한 프로젝트에 권장되는 솔루션입니다.

## 소개 {#introduction}

이 문서에서는 간단한 SPA의 기본 기능과 필요한 최소 기능을 간략하게 설명합니다.

AEM에서 SPA가 작동하는 방식에 대한 자세한 내용은 다음 문서를 참조하십시오.

* [SPA 소개 및 연습](/help/sites-developing/spa-walkthrough.md)
* [SPA 저작 소개](/help/sites-developing/spa-overview.md)
* [SPA Blueprint](/help/sites-developing/spa-blueprint.md)

>[!NOTE]
>
>SPA 내에서 컨텐츠를 저작할 수 있으려면 컨텐츠를 AEM에 저장하고 컨텐츠 모델에 의해 노출되어야 합니다.
>
>AEM 외부에서 개발된 SPA는 컨텐츠 모델 계약을 준수하지 않는 경우 인증할 수 없습니다.

본 문서는 React 프레임워크를 사용하여 만든 간소화된 SPA의 구조를 자세히 설명하여 SPA에 이러한 이해를 적용할 수 있는 방법을 설명합니다.

## 종속성, 구성 및 빌드 {#dependencies-configuration-and-building}

예상되는 반응 종속성 외에도 샘플 SPA는 추가 라이브러리를 활용하여 SPA를 보다 효율적으로 만들 수 있습니다.

### 종속성 {#dependencies}

이 `package.json` 파일은 전체 SPA 패키지의 요구 사항을 정의합니다. 작업 SPA에 대한 최소 AEM 종속성이 여기에 나열되어 있습니다.

```
  "dependencies": {
    "@adobe/cq-react-editable-components": "~1.0.3",
    "@adobe/cq-spa-component-mapping": "~1.0.3",
    "@adobe/cq-spa-page-model-manager": "~1.0.4"
  }
```

이 예는 Response 프레임워크를 기반으로 하므로 `package.json` 파일에 의무적인 두 개의 React-specific 종속성이 있습니다.

```
react
 react-dom
```

를 `aem-clientlib-generator` 사용하여 클라이언트 라이브러리를 작성 프로세스의 일부로 자동으로 만들 수 있습니다.

`"aem-clientlib-generator": "^1.4.1",`

자세한 내용은 GitHub [에서 확인할 수 있습니다](https://github.com/wcm-io-frontend/aem-clientlib-generator).

>[!CAUTION]
>
>필요한 최소 버전은 1.4.1 `aem-clientlib-generator` 입니다.

는 `aem-clientlib-generator` 다음과 같이 `clientlib.config.js` 파일에 구성됩니다.

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

실제로 앱을 빌드하면 자동 클라이언트 라이브러리 [생성을](https://webpack.js.org/) 위해 aem-clientlib-generator뿐만 아니라 전달을 위해 Webpack이 활용됩니다. 따라서 빌드 명령은 다음과 같습니다.

`"build": "webpack && clientlib --verbose"`

일단 빌드하면 패키지를 AEM 인스턴스에 업로드할 수 있습니다.

### SPA Starter Kit를 위한 Maven Tranype {#maven-archetype-for-spa-starter-kit}

Adobe에서는 AEM용 SPA [프로젝트를 시작하는 데 도움이 되도록 SPA](https://github.com/adobe/aem-spa-project-archetype) Starter Kit용 Maven Tranype을 활용하는 것이 좋습니다.

## 애플리케이션 구조 {#application-structure}

앞에서 설명한 바와 같이 종속성을 포함하고 앱을 빌드하면 AEM 인스턴스에 업로드할 수 있는 작업 중인 SPA 패키지가 표시됩니다.

이 문서의 다음 섹션에서는 AEM의 SPA가 구조화된 방식, 애플리케이션을 구동하는 중요한 파일 및 이러한 SPA의 작동 방식을 살펴봅니다.

간소화된 이미지 구성 요소가 예로 사용되지만 애플리케이션의 모든 구성 요소는 동일한 개념을 기반으로 합니다.

### index.js {#index-js}

SPA의 엔트리 포인트는 중요한 컨텐츠에 초점을 맞추기 위해 여기에 간단히 표시된 `index.js` 파일입니다.

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

의 주요 `index.js` 기능은 `ReactDOM.render` 함수를 활용하여 DOM에서 애플리케이션을 주입할 위치를 결정하는 것입니다.

이 예제 앱은 이 함수의 표준 용도가 아닙니다.

#### 정적 인스턴스화 {#static-instantiation}

구성 요소 템플릿(예: JSX)을 사용하여 구성 요소가 정적으로 인스턴스화되는 경우, 이 값은 모델에서 구성 요소의 속성으로 전달되어야 합니다.

### App.js {#app-js}

앱을 렌더링하면 `index.js` 호출이 `App.js`간소화되며 중요한 컨텐츠에 집중할 수 있습니다.

```
import {Page, withModel } from '@adobe/cq-react-editable-components';

...

class App extends Page {
...
}

export default withModel(App);
```

`App.js` 기본적으로 앱을 구성하는 루트 구성 요소를 래핑하는 데 사용됩니다. 앱의 시작 지점은 페이지입니다.

### Page.js {#page-js}

페이지를 렌더링하면 `App.js` 여기에 나열된 간단한 버전으로 통화가 `Page.js` 이루어집니다.

```
import {Page, MapTo, withComponentMappingContext } from "@adobe/cq-react-editable-components";

...

class AppPage extends Page {
...
}

MapTo('my-react-app/components/structure/page')(withComponentMappingContext(AppPage));
```

이 예제에서 `AppPage` 클래스는 확장되어 사용할 수 `Page`있는 내부 컨텐츠 메서드가 포함됩니다.

인제스트는 페이지 모델의 JSON 표현을 `Page` 설정하고 컨텐츠가 페이지의 각 요소를 래핑/장식하도록 처리합니다. 자세한 내용은 `Page` SPA Blueprint 문서를 [참조하십시오](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501).

### Image.js {#image-js}

페이지를 렌더링하면 여기에 `Image.js` 표시된 것과 같은 구성 요소를 렌더링할 수 있습니다.

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

AEM에서 SPA의 주된 아이디어는 SPA 구성 요소를 AEM 구성 요소에 매핑하고 컨텐츠가 수정될 때(또는 그 반대로) 구성 요소를 업데이트하는 것입니다. 이 커뮤니케이션 모델에 [대한](/help/sites-developing/spa-overview.md) 요약은 SPA 편집기 개요를 참조하십시오.

`MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);`

이 `MapTo` 메서드는 SPA 구성 요소를 AEM 구성 요소에 매핑합니다. 단일 문자열 또는 문자열 배열을 사용할 수 있습니다.

`ImageEditConfig` 는 편집기에서 자리 표시자를 생성하는 데 필요한 메타데이터를 제공하여 구성 요소의 작성 기능을 활성화하는 데 기여하는 구성 개체입니다.

컨텐츠가 없으면 빈 컨텐츠를 나타내는 자리 표시자로 레이블이 제공됩니다.

#### 동적으로 전달된 속성 {#dynamically-passed-properties}

모델에서 오는 데이터는 구성 요소의 속성으로 동적으로 전달됩니다.

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

이 `MapTo` 함수는 작성이 가능한 클래스 이름 및 속성과 함께 제공된 속성을 `Component` `PageClass` 확장하는 컴포지션의 결과인 를 반환합니다. 이 구성 요소는 나중에 애플리케이션 마크업에서 인스턴스화하도록 내보낼 수 있습니다.

When exported using the `MapTo` or `withModel` functions, the `Page` `ModelProvider` component is wrap with a standard components access to the latest version of the page model or a precise location in the page model.

자세한 내용은 SPA Blueprint [문서를](/help/sites-developing/spa-blueprint.md#main-pars-header-329251743)참조하십시오.

>[!NOTE]
>
>기본적으로 `withModel` 함수를 사용할 때 구성 요소의 전체 모델을 받습니다.

## SPA 구성 요소 간 정보 공유 {#sharing-information-between-spa-components}

단일 페이지 애플리케이션 내의 구성 요소가 정보를 공유하려면 정기적으로 필요합니다. 다음과 같이 복잡성이 증가하면서 여러 가지 권장 방법으로 이 작업을 수행할 수 있습니다.

* **** 옵션 1:React Context를 사용하여 로직과 브로드캐스트를 필요한 구성 요소로 중앙에서 처리합니다.
* **** 옵션 2:리덕스와 같은 상태 라이브러리를 사용하여 구성 요소 상태를 공유합니다.
* **** 옵션 3:컨테이너 구성 요소를 사용자 지정하고 확장하여 객체 계층 구조를 활용할 수 있습니다.

## 다음 단계 {#next-steps}

자체 SPA를 만드는 단계별 가이드는 AEM SPA 편집기 [- WKND 이벤트 자습서를 참조하십시오](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html).

AEM용 SPA를 개발하기 위해 자신을 구성하는 방법에 대한 자세한 내용은 AEM용 SPA [개발 문서를 참조하십시오](/help/sites-developing/spa-architecture.md).

동적 모델-구성 요소 매핑 및 AEM의 SPA 내에서 작동하는 방식에 대한 자세한 내용은 SPA에 대한 [구성 요소 매핑에 대한 동적 모델을 참조하십시오](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

AEM에서 React 또는 Angular 이외의 프레임워크에 대해 SPA를 구현하거나 AEM용 SPA SDK의 작동 방식을 심층적으로 살펴보려면 SPA Blueprint [문서를 참조하십시오](/help/sites-developing/spa-blueprint.md) .
