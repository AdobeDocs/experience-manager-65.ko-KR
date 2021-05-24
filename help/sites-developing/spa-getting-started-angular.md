---
title: AEM에서 SPA 시작하기 - Angular
seo-title: AEM에서 SPA 시작하기 - Angular
description: 이 문서에서는 샘플 SPA 애플리케이션을 제공하며 이 응용 프로그램을 구성하는 방법을 설명하고 Angular 프레임워크을 사용하여 신속하게 자체 SPA을 사용하여 실행 및 실행할 수 있도록 해줍니다.
seo-description: 이 문서에서는 샘플 SPA 애플리케이션을 제공하며 이 응용 프로그램을 구성하는 방법을 설명하고 Angular 프레임워크을 사용하여 신속하게 자체 SPA을 사용하여 실행 및 실행할 수 있도록 해줍니다.
uuid: d3d2fa63-68c8-4a48-8c8d-045f4f8db937
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 9cdd7648-d67e-414d-aedf-a5687da39326
docset: aem65
exl-id: 9528d92b-0989-4e2d-83be-ba6c07c845e2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1053'
ht-degree: 5%

---

# AEM에서 SPA 시작하기 - Angular{#getting-started-with-spas-in-aem-angular}

SPA(단일 페이지 애플리케이션)는 웹 사이트 사용자에게 훌륭한 경험을 제공할 수 있습니다. 개발자는 SPA 프레임워크을 사용하여 사이트를 작성하려고 하며 작성자는 SPA 프레임워크을 사용하여 작성된 사이트의 AEM 내에서 컨텐츠를 원활하게 편집하려고 합니다.

SPA 작성 기능은 AEM 내에서 SPA을 지원하는 포괄적인 솔루션을 제공합니다. 이 문서에서는 Angular 프레임워크에 간소화된 SPA 애플리케이션을 제공하며 이 애플리케이션을 구성하는 방법을 설명하므로 SPA을 빠르게 시작하고 실행할 수 있습니다.

>[!NOTE]
>
>이 문서는 Angular 프레임워크을 기반으로 합니다. React 프레임워크에 대한 해당 문서는 [AEM에서 SPA 시작하기 - React](/help/sites-developing/spa-getting-started-react.md)를 참조하십시오.

>[!NOTE]
>
>SPA 편집기는 SPA 프레임워크 기반 클라이언트측 렌더링(예: React 또는 Angular)이 필요한 프로젝트에 권장되는 솔루션입니다.

## 소개 {#introduction}

이 문서에서는 간단한 SPA의 기본 기능과 최소 기능을 사용하여 실행할 수 있도록 합니다.

AEM에서 SPA이 작동하는 방법에 대한 자세한 내용은 다음 문서를 참조하십시오.

* [SPA 소개 및 연습](/help/sites-developing/spa-walkthrough.md)
* [SPA Authoring 소개](/help/sites-developing/spa-overview.md)
* [SPA 블루프린트](/help/sites-developing/spa-blueprint.md)

>[!NOTE]
>
>SPA 내에서 컨텐츠를 작성할 수 있으려면 컨텐츠를 AEM에 저장하고 컨텐츠 모델에 의해 노출되어야 합니다.
>
>AEM 외부에서 개발된 SPA은 컨텐츠 모델 계약을 준수하지 않으면 승인되지 않습니다.

이 문서는 간소화된 SPA의 구조를 살펴보고 이 이해를 SPA에 적용할 수 있도록 작동 방식을 설명하겠습니다.

## 종속성, 구성 및 빌드 {#dependencies-configuration-and-building}

예상되는 Angular 종속성 외에, 샘플 SPA은 추가 라이브러리를 활용하여 SPA을 보다 효율적으로 만들 수 있습니다.

### 종속성 {#dependencies}

`package.json` 파일은 전체 SPA 패키지의 요구 사항을 정의합니다. 필요한 최소 AEM 종속성은 여기에 나열됩니다.

```
"dependencies": {
  "@adobe/aem-angular-editable-components": "~1.0.3",
  "@adobe/aem-spa-component-mapping": "~1.0.5",
  "@adobe/aem-spa-page-model-manager": "~1.0.3"
}
```

`aem-clientlib-generator`은 빌드 프로세스의 일부로 클라이언트 라이브러리를 자동으로 만드는 데 사용됩니다.

`"aem-clientlib-generator": "^1.4.1",`

이에 대한 자세한 내용은 여기](https://github.com/wcm-io-frontend/aem-clientlib-generator)GitHub에서 [을 참조하십시오.

>[!CAUTION]
>
>필요한 `aem-clientlib-generator`의 최소 버전은 1.4.1입니다.

`aem-clientlib-generator`은 `clientlib.config.js` 파일에 다음과 같이 구성됩니다.

```
module.exports = {
    // default working directory (can be changed per 'cwd' in every asset option)
    context: __dirname,

    // path to the clientlib root folder (output)
    clientLibRoot: "./../content/jcr_root/apps/my-angular-app/clientlibs",

    libs: {
        name: "my-angular-app",
        allowProxy: true,
        categories: ["my-angular-app"],
        embed: ["my-angular-app.responsivegrid"],
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

### 빌딩 {#building}

실제로 앱을 빌드하면 자동 클라이언트 라이브러리 생성을 위한 aem-clientlib-generator 외에 전달을 위해 [Webpack](https://webpack.js.org/)이 활용됩니다. 따라서 build 명령은 다음과 같습니다.

`"build": "ng build --build-optimizer=false && clientlib",`

완료되면 패키지를 AEM 인스턴스에 업로드할 수 있습니다.

### AEM 프로젝트 전형 {#aem-project-archetype}

모든 AEM 프로젝트는 React 또는 Angular을 사용하여 SPA 프로젝트를 지원하고 SPA SDK를 활용하는 [AEM Project Archetype](https://docs.adobe.com/content/help/ko-KR/experience-manager-core-components/using/developing/archetype/overview.html)을 활용해야 합니다.

## 응용 프로그램 구조 {#application-structure}

앞에서 설명한 대로 종속성을 포함하고 앱을 빌드하면 AEM 인스턴스에 업로드할 수 있는 작업 SPA 패키지가 표시됩니다.

이 문서의 다음 섹션에서는 AEM에서 SPA을 구성하는 방법, 애플리케이션을 구동하는 중요한 파일 및 이러한 파일이 함께 작동하는 방식을 살펴봅니다.

간소화된 이미지 구성 요소가 예로 사용되지만 애플리케이션의 모든 구성 요소는 동일한 개념을 기반으로 합니다.

### app.module.ts {#app-module-ts}

SPA의 시작 지점은 중요한 컨텐츠에 집중할 수 있도록 여기에 간소화된 `app.module.ts` 파일입니다.

```
// app.module.ts
import { BrowserModule, BrowserTransferStateModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component';
import { SpaAngularEditableComponentsModule } from '@adobe/aem-angular-editable-components';
import { AppRoutingModule } from './app-routing.module';

@NgModule({
  imports: [ BrowserModule.withServerTransition({ appId: 'my-angular-app' }),
    SpaAngularEditableComponentsModule,
    AppRoutingModule,
    BrowserTransferStateModule ],
  providers: ...,
  declarations: [ ... ],
  entryComponents: [ ... ],
  bootstrap: [ AppComponent ]
})
export class AppModule {}
```

`app.module.ts` 파일은 앱의 시작점이며 초기 프로젝트 구성을 포함하고 `AppComponent` 을 사용하여 앱을 부트스트랩합니다.

#### 정적 인스턴스화 {#static-instantiation}

구성 요소 템플릿을 사용하여 구성 요소가 정적으로 인스턴스화될 때 이 값을 모델에서 구성 요소의 속성으로 전달해야 합니다. 모델의 값은 나중에 구성 요소 속성으로 사용할 수 있도록 속성으로 전달됩니다.

### app.component.ts {#app-component-ts}

`app.module.ts` 부트스트랩 `AppComponent`을(를) 시작하면 앱을 초기화할 수 있습니다. 이 앱은 중요한 컨텐츠에 집중할 수 있도록 간소화된 버전으로 여기에 표시됩니다.

```
// app.component.ts
import { Component } from '@angular/core';
import { ModelManager } from '@adobe/aem-spa-page-model-manager';
import { Constants } from "@adobe/aem-angular-editable-components";

@Component({
  selector: 'app-root',
  template: `
    <router-outlet></router-outlet>
  `
})

export class AppComponent {
  items;
  itemsOrder;
  path;

  constructor() {
    ModelManager.initialize().then(this.updateData.bind(this));
  }

  private updateData(model) {
    this.path = model[Constants.PATH_PROP];
    this.items = model[Constants.ITEMS_PROP];
    this.itemsOrder = model[Constants.ITEMS_ORDER_PROP];
  }
}
```

### main.content.component.ts {#main-content-component-ts}

페이지를 처리하면 `app.component.ts`이 여기에 나열된 `main-content.component.ts`을 단순 버전으로 호출합니다.

```
import { Component } from '@angular/core';
import { ModelManagerService }     from '../model-manager.service';
import { ActivatedRoute } from '@angular/router';
import { Constants } from "@adobe/aem-angular-editable-components";

@Component({
  selector: 'app-main',
  template: `
    <aem-page class="structure-page" [attr.data-cq-page-path]="path" [cqPath]="path" [cqItems]="items" [cqItemsOrder]="itemsOrder" ></aem-page>
  `
})

export class MainContentComponent {
  items;
  itemsOrder;
  path;

  constructor( private route: ActivatedRoute,
    private modelManagerService: ModelManagerService) {
    this.modelManagerService.getData({ path: this.route.snapshot.data.path }).then((data) => {
      this.path = data[Constants.PATH_PROP];
      this.items = data[Constants.ITEMS_PROP];
      this.itemsOrder = data[Constants.ITEMS_ORDER_PROP];
    });
  }
}
```

`MainComponent` 은 페이지 모델의 JSON 표현을 수집하고 컨텐츠를 처리하여 페이지의 각 요소를 래핑/장식합니다. `Page`에 대한 자세한 내용은 [SPA Blueprint](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501) 문서에서 확인할 수 있습니다.

### image.component.ts {#image-component-ts}

`Page`은 구성 요소로 구성됩니다. JSON을 통해 `Page`은 여기에 표시된 것처럼 `image.component.ts`과 같은 구성 요소를 처리할 수 있습니다.

```
/// image.component.ts
import { Component, Input } from '@angular/core';

const ImageEditConfig = {

    emptyLabel: 'Image',

    isEmpty: function(cqModel) {
        return !cqModel || !cqModel.src || cqModel.src.trim().length < 1;
    }
};

@Component({
  selector: 'app-image',
  templateUrl: './image.component.html',
})

export class ImageComponent {
  @Input() src: string;
  @Input() alt: string;
  @Input() title: string;
}

MapTo('my-angular-app/components/image')(ImageComponent, ImageEditConfig);
```

AEM에서 SPA의 핵심 개념은 SPA 구성 요소를 AEM 구성 요소에 매핑하고 컨텐츠가 수정될 때(또는 그 반대로) 구성 요소를 업데이트하는 것입니다. 이 통신 모델에 대한 요약은 [SPA 편집기 개요](/help/sites-developing/spa-overview.md) 문서를 참조하십시오.

`MapTo('my-angular-app/components/image')(Image, ImageEditConfig);`

`MapTo` 메서드는 SPA 구성 요소를 AEM 구성 요소에 매핑합니다. 단일 문자열 또는 문자열 배열을 사용할 수 있습니다.

`ImageEditConfig` 는 편집기에서 자리 표시자를 생성하는 데 필요한 메타데이터를 제공하여 구성 요소의 작성 기능을 활성화하는 데 기여하는 구성 개체입니다

콘텐츠가 없으면 빈 콘텐츠를 나타내는 자리 표시자로 레이블이 제공됩니다.

#### 동적으로 전달된 속성 {#dynamically-passed-properties}

모델에서 나오는 데이터는 구성 요소의 속성으로 동적으로 전달됩니다.

### image.component.html {#image-component-html}

마지막으로 이미지를 `image.component.html`에서 렌더링할 수 있습니다.

```
// image.component.html
<img [src]="src" [alt]="alt" [title]="title"/>
```

## SPA 구성 요소 간 정보 공유 {#sharing-information-between-spa-components}

단일 페이지 애플리케이션 내의 구성 요소가 정보를 공유하려면 정기적으로 필요합니다. 다음과 같이 복잡도 순서로 나열하는 몇 가지 권장 방법이 있습니다.

* **옵션 1:** 논리 및 브로드캐스트를 필수 구성 요소로 집중하려면 예를 들어, util 클래스를 순수한 개체 지향 솔루션으로 사용합니다.
* **옵션 2:** NgRx와 같은 상태 라이브러리를 사용하여 구성 요소 상태를 공유합니다.
* **옵션 3:** 컨테이너 구성 요소를 사용자 지정하고 확장하여 객체 계층 구조를 활용합니다.

## 다음 단계 {#next-steps}

자신만의 SPA을 만드는 단계별 안내서는 [AEM SPA Editor 시작하기 - WKND 이벤트 자습서](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html)를 참조하십시오.

SPA for AEM을 개발하도록 조직화하는 방법에 대한 자세한 내용은 [AEM용 SPA 개발](/help/sites-developing/spa-architecture.md) 문서를 참조하십시오.

동적 모델과 AEM에서 구성 요소 간 매핑 및 SPA 내에서 작동하는 방법에 대한 자세한 내용은 [동적 모델과 SPA](/help/sites-developing/spa-dynamic-model-to-component-mapping.md)의 구성 요소 간 매핑 문서를 참조하십시오.

React 또는 Angular 이외의 프레임워크에 대해 AEM에서 SPA을 구현하거나 AEM용 SPA SDK의 작동 방식을 자세히 살펴보려면 [SPA Blueprint](/help/sites-developing/spa-blueprint.md) 문서를 참조하십시오.
