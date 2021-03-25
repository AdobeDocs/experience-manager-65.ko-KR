---
title: AEM 내에서 외부 SPA 편집
description: 이 문서에서는 AEM 인스턴스에 독립 실행형 SPA을 업로드하고, 편집 가능한 컨텐츠 섹션을 추가하고, 저작을 활성화하는 데 권장되는 단계에 대해 설명합니다.
translation-type: tm+mt
source-git-commit: 431bed450ed5b0239d9191dcf061f01e64b8981a
workflow-type: tm+mt
source-wordcount: '2118'
ht-degree: 0%

---

# AEM {#editing-external-spa-within-aem} 내에서 외부 SPA 편집

외부 SPA과 AEM 간에 어떤 통합 수준을 원하는지 결정할 때 AEM 내에서 SPA을 볼 뿐만 아니라 편집할 수 있어야 하는 경우도 있습니다.

## 개요 {#overview}

이 문서에서는 AEM 인스턴스에 독립 실행형 SPA을 업로드하고, 편집 가능한 컨텐츠 섹션을 추가하고, 저작을 활성화하는 데 권장되는 단계에 대해 설명합니다.

## 전제 조건 {#prerequisites}

전제 조건은 간단합니다.

* AEM 인스턴스가 로컬로 실행되고 있는지 확인합니다.
* AEM 프로젝트 원형을 사용하여 [기본 AEM SPA 프로젝트를 만듭니다.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?#available-properties)
   * 외부 SPA을 포함하도록 업데이트되는 AEM 프로젝트의 기반이 됩니다.
   * 이 문서의 샘플에 대해 [WKND SPA 프로젝트의 시작점을 사용합니다.](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html#spa-editor)
* 통합하려는 외부 반응형 SPA을 사용할 수 있습니다.

## AEM 프로젝트에 SPA 업로드 {#upload-spa-to-aem-project}

먼저 외부 SPA을 AEM 프로젝트에 업로드해야 합니다.

1. `/ui.frontend` 프로젝트 폴더의 `src`을 React 응용 프로그램의 `src` 폴더로 바꿉니다.
1. `/ui.frontend/package.json` 파일의 앱 `package.json`에 추가 종속성을 포함시킵니다.
   * SPA SDK 종속성이 [권장 버전인지 확인합니다.](spa-getting-started-react.md#dependencies)
1. `/public` 폴더에 모든 사용자 지정을 포함합니다.
1. `/public/index.html` 파일에 추가된 인라인 스크립트 또는 스타일을 포함합니다.

## 원격 SPA {#configure-remote-spa} 구성

외부 SPA은 AEM 프로젝트에 포함되어 있으므로 AEM 내에서 구성해야 합니다.

### Adobe SPA SDK 패키지 포함 {#include-spa-sdk-packages}

AEM SPA 기능을 활용하려면 다음 3개의 패키지에 종속됩니다.

* [`@adobe/aem-react-editable-components`](https://github.com/adobe/aem-react-editable-components)
* [`@adobe/aem-spa-component-mapping`](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)
* [`@adobe/aem-spa-page-model-manager`](https://www.npmjs.com/package/@adobe/aem-spa-model-manager)

`@adobe/aem-spa-page-model-manager` 는 모델 관리자를 초기화하고 AEM 인스턴스에서 모델을 검색하는 데 사용할 API를 제공합니다. 그런 다음 이 모델을 사용하여 `@adobe/aem-react-editable-components` 및 `@adobe/aem-spa-component-mapping`의 API를 사용하여 AEM 구성 요소를 렌더링할 수 있습니다.

#### 설치 {#installation}

다음 npm 명령을 실행하여 필요한 패키지를 설치합니다.

```shell
npm install --save @adobe/aem-spa-component-mapping @adobe/aem-spa-page-model-manager @adobe/aem-react-editable-components
```

### ModelManager 초기화 {#model-manager-initialization}

앱이 렌더링되기 전에 AEM `ModelStore` 생성을 처리하도록 [`ModelManager`](spa-blueprint.md#pagemodelmanager)을(를) 초기화해야 합니다.

이 작업은 응용 프로그램의 `src/index.js` 파일 내에서 또는 응용 프로그램의 루트가 렌더링될 때마다 수행해야 합니다.

이를 위해 `ModelManager`에서 제공하는 `initializationAsync` API를 사용할 수 있습니다.

다음 스크린샷은 단순 응답 응용 프로그램에서 `ModelManager`의 초기화를 활성화하는 방법을 보여줍니다. 유일한 제약 조건은 `initializationAsync`을(를) `ReactDOM.render()` 이전에 호출해야 한다는 것입니다.

![ModelManager 초기화](assets/external-spa-initialize-modelmanager.png)

이 예에서 `ModelManager`은 초기화되고 빈 `ModelStore`이 만들어집니다.

`initializationAsync` 선택적으로 객체를 매개  `options` 변수로 허용할 수 있습니다.

* `path` - 초기화 시 정의된 경로의 모델을 가져와 에 저장합니다 `ModelStore`. 필요한 경우 초기화 시 `rootModel`을 가져오는 데 사용할 수 있습니다.
* `modelClient` - 모델을 가져오는 책임을 지는 사용자 지정 클라이언트를 제공할 수 있습니다.
* `model` -  `model` SSR을  [사용할 때 일반적으로 채워진 매개 변수로 전달되는 객체입니다.](spa-ssr.md)

### AEM 작성 가능한 리프 구성 요소 {#authorable-leaf-components}

1. authorable React 구성 요소가 생성될 AEM 구성 요소를 만들거나 식별합니다. 이 예에서는 WKND 프로젝트의 텍스트 구성 요소를 사용합니다.

   ![WKND 텍스트 구성 요소](assets/external-spa-text-component.png)

1. SPA에서 간단한 반응형 텍스트 구성 요소를 만듭니다. 이 예에서는 다음 콘텐트로 새 파일 `Text.js`이(가) 만들어졌습니다.

   ![Text.js](assets/external-spa-textjs.png)

1. AEM 편집을 활성화하는 데 필요한 특성을 지정하는 구성 객체를 만듭니다.

   ![구성 개체 만들기](assets/external-spa-config-object.png)

   * `resourceType` 은 AEM 구성 요소에 반응형 구성 요소를 매핑하고 AEM 편집기에서 열 때 편집을 활성화해야 합니다.

1. 래퍼 함수 `withMappable`을 사용합니다.

   ![매핑 가능한 사용](assets/external-spa-withmappable.png)

   이 래퍼 함수는 Responsive 구성 요소를 구성에 지정된 AEM `resourceType`에 매핑하고 AEM 편집기에서 열 때 편집 기능을 활성화합니다. 독립 실행형 구성 요소의 경우 특정 노드의 모델 컨텐츠도 가져옵니다.

   >[!NOTE]
   >
   >이 예에서는 구성 요소의 개별 버전이 있습니다.AEM 래핑 및 래핑되지 않은 반응형 구성 요소. 구성 요소를 명시적으로 사용할 때는 래핑된 버전을 사용해야 합니다. 구성 요소가 페이지의 일부인 경우 SPA 편집기에서 현재 수행한 대로 기본 구성 요소를 계속 사용할 수 있습니다.

1. 구성 요소의 컨텐츠를 렌더링합니다.

   텍스트 구성 요소의 JCR 속성은 AEM에서 다음과 같이 표시됩니다.

   ![텍스트 구성 요소 속성](assets/external-spa-text-properties.png)

   이러한 값은 새로 만든 `AEMText` 반응 구성 요소에 속성으로 전달되며 컨텐츠를 렌더링하는 데 사용할 수 있습니다.

   ```javascript
   import React from 'react';
   import { withMappable } from '@adobe/aem-react-editable-components';
   
   export const TextEditConfig = {
       // Empty component placeholder label
       emptyLabel:'Text', 
       isEmpty:function(props) {
          return !props || !props.text || props.text.trim().length < 1;
       },
       // resourcetype of the AEM counterpart component
       resourceType:'wknd-spa-react/components/text'
   };
   
   const Text = ({ text }) => (<div>{text}</div>);
   
   export default Text;
   
   export const AEMText = withMappable(Text, TextEditConfig);
   ```

   AEM 구성이 완료되면 구성 요소가 표시되는 방식입니다.

   ```javascript
   const Text = ({ cqPath, richText, text }) => {
      const richTextContent = () => (
         <div className="aem_text" id={cqPath.substr(cqPath.lastIndexOf('/') + 1)} data-rte-editelement dangerouslySetInnerHTML={{__html: text}}/>
      );
      return richText ? richTextContent() : (<div className="aem_text">{text}</div>);
   };
   ```

   >[!NOTE]
   >
   >이 예에서는 기존 텍스트 구성 요소에 맞게 렌더링된 구성 요소를 추가로 사용자 정의했습니다. 그러나 AEM에서의 작성과는 관련이 없습니다.

#### 작성 가능한 구성 요소를 페이지 {#add-authorable-component-to-page}에 추가

작성 가능한 반응 구성 요소가 만들어지면 애플리케이션 전체에서 사용할 수 있습니다.

WKND SPA 프로젝트에서 텍스트를 추가해야 하는 예제 페이지를 예로 들어보겠습니다. 이 예에서는 &quot;Hello World!&quot; 텍스트를 표시하려고 합니다. on `/content/wknd-spa-react/us/en/home.html`.

1. 표시할 노드의 경로를 결정합니다.

   * `pagePath`:노드를 포함하는 페이지(예:  `/content/wknd-spa-react/us/en/home`
   * `itemPath`:페이지 내의 노드에 대한 경로(예:  `root/responsivegrid/text`
      * 이것은 페이지에 있는 포함 항목의 이름으로 구성됩니다.

   ![노드의 경로](assets/external-spa-path.png)

1. 페이지에서 필요한 위치에 구성 요소를 추가합니다.

   ![페이지에 구성 요소 추가](assets/external-spa-add-component.png)

   `AEMText` 구성 요소는 `pagePath` 및 `itemPath` 값이 속성으로 설정된 페이지 내의 필요한 위치에 추가할 수 있습니다. `pagePath` 은 필수 속성입니다.

#### AEM {#verify-text-edit}에서 텍스트 내용 편집 확인

이제 실행 중인 AEM 인스턴스에서 구성 요소를 테스트할 수 있습니다.

1. `aem-guides-wknd-spa` 디렉토리에서 다음 Maven 명령을 실행하여 프로젝트를 빌드하고 AEM에 배포합니다.

```shell
mvn clean install -PautoInstallSinglePackage
```

1. AEM 인스턴스에서 `http://<host>:<port>/editor.html/content/wknd-spa-react/us/en/home.html`으로 이동합니다.

![AEM에서 SPA 편집](assets/external-spa-edit-aem.png)

이제 AEM에서 `AEMText` 구성 요소를 인증할 수 있습니다.

### AEM 작성 가능한 페이지 {#aem-authorable-pages}

1. SPA에서 작성을 위해 추가할 페이지를 식별합니다. 이 예에서는 `/content/wknd-spa-react/us/en/home.html`을 사용합니다.
1. 새 파일(예:작성 가능한 페이지 구성 요소에 대한 `Page.js`). 여기서는 `@adobe/cq-react-editable-components`에 제공된 페이지 구성 요소를 재사용할 수 있습니다.
1. [AEM 인증 가능한 리프 구성 요소 섹션에서 4단계를 반복합니다.](#authorable-leaf-components) 구성 요소 `withMappable` 에서 래퍼 함수를 사용합니다.
1. 이전에 수행한 대로 페이지 내의 모든 하위 구성 요소에 대해 AEM 리소스 유형에 `MapTo`을 적용합니다.

   ```javascript
   import { Page, MapTo, withMappable } from '@adobe/aem-react-editable-components';
   import Text, { TextEditConfig } from './Text';
   
   export default withMappable(Page);
   
   MapTo('wknd-spa-react/components/text')(Text, TextEditConfig);
   ```

   >[!NOTE]
   >
   >이 예에서는 이전에 만든 래핑 `AEMText` 대신 래핑되지 않은 반응형 텍스트 구성 요소를 사용합니다. 구성 요소가 페이지/컨테이너의 일부이며 단독으로 설 수 없는 경우 컨테이너는 구성 요소를 반복적으로 매핑하고 작성 기능을 활성화하며 각 하위 요소에 대해 추가 래퍼가 필요하지 않기 때문입니다.

1. SPA에서 작성 가능한 페이지를 추가하려면 페이지에 작성 가능한 구성 요소 추가 섹션의 동일한 단계를 수행합니다.[](#add-authorable-component-to-page) 여기에서 이 속성은 건너뛸 수  `itemPath` 있습니다.

#### AEM {#verify-page-content}에서 페이지 컨텐츠 확인

페이지를 편집할 수 있는지 확인하려면 AEM에서 텍스트 컨텐츠 편집 확인 섹션 [과 동일한 단계를 수행합니다.](#verify-text-edit)

![AEM에서 페이지 편집](assets/external-spa-edit-page.png)

이제 레이아웃 컨테이너와 하위 텍스트 구성 요소가 있는 AEM에서 페이지를 편집할 수 있습니다.

### 가상 리프 구성 요소 {#virtual-leaf-components}

이전 예에서 기존 AEM 컨텐츠가 있는 SPA에 구성 요소를 추가했습니다. 그러나 AEM에서 아직 컨텐츠를 만들지 않았지만 컨텐츠 작성자가 나중에 컨텐츠를 추가해야 하는 경우가 있습니다. 이를 수용하기 위해 프런트 엔드 개발자는 SPA 내의 적절한 위치에 구성 요소를 추가할 수 있습니다. 이러한 구성 요소는 AEM의 편집기에서 열 때 자리 표시자를 표시합니다. 컨텐츠 작성자가 이러한 자리 표시자 내에 컨텐츠를 추가하면 JCR 구조에서 노드가 만들어지고 컨텐츠가 유지됩니다. 생성된 구성 요소는 독립형 리프 구성 요소와 동일한 작업 세트를 허용합니다.

이 예에서는 이전에 만든 `AEMText` 구성 요소를 다시 사용합니다. WKND 홈 페이지의 기존 텍스트 구성 요소 아래에 새 텍스트를 추가할 수 있습니다. 구성 요소의 추가는 일반적인 리프 구성 요소와 동일합니다. 그러나 `itemPath`은(는) 새 구성 요소를 추가해야 하는 경로로 업데이트할 수 있습니다.

새 구성 요소를 `root/responsivegrid/text`의 기존 텍스트 아래에 추가해야 하므로 새 경로는 `root/responsivegrid/{itemName}`입니다.

```html
<AEMText
 pagePath='/content/wknd-spa-react/us/en/home'
 itemPath='root/responsivegrid/text_20' />
```

`TestPage` 구성 요소는 가상 구성 요소를 추가한 후 다음과 같습니다.

![가상 구성 요소 테스트](assets/external-spa-virtual-component.png)

>[!NOTE]
>
>이 기능을 사용하도록 설정하려면 `AEMText` 구성 요소에 해당 `resourceType` 설정이 있는지 확인합니다.

이제 AEM에서 텍스트 컨텐츠 편집 확인 섹션의 단계를 따라 AEM에 변경 사항을 배포할 수 있습니다.[](#verify-text-edit) 현재 존재하지 않는 노드에 대한 자리 표시자가  `text_20` 표시됩니다.

![aem의 text_20 노드](assets/external-spa-text20-aem.png)

내용 작성자가 이 구성 요소를 업데이트하면 `/content/wknd-spa-react/us/en/home`의 `root/responsivegrid/text_20`에 새 `text_20` 노드가 만들어집니다.

![text20 노드](assets/external-spa-text20-node.png)

#### 요구 사항 및 제한 사항 {#limitations}

가상 리프 구성 요소를 추가하기 위한 요구 사항뿐만 아니라 몇 가지 제한 사항이 있습니다.

* 가상 구성 요소를 만들려면 `pagePath` 속성이 필요합니다.
* `pagePath`의 경로에 제공된 페이지 노드가 AEM 프로젝트에 있어야 합니다.
* 만들 노드의 이름은 `itemPath`에 제공해야 합니다.
* 구성 요소는 모든 수준에서 만들 수 있습니다.
   * 이전 예제에서 `itemPath='text_20'`을 제공하는 경우 새 노드가 페이지(예:`/content/wknd-spa-react/us/en/home/jcr:content/text_20`
* 새 노드를 만드는 노드의 경로는 `itemPath`을 통해 제공할 때 유효해야 합니다.
   * 이 예에서 새 노드 `text_20`을(를) 거기에 만들 수 있도록 `root/responsivegrid`이(가) 있어야 합니다.
* 리프 구성 요소 생성만 지원됩니다. 가상 컨테이너 및 페이지는 향후 버전에서 지원됩니다.

## 추가 사용자 지정 {#additional-customizations}

이전 예제를 따라 외부 SPA을 이제 AEM 내에서 편집할 수 있습니다. 그러나 사용자 정의할 수 있는 외부 SPA의 다른 측면도 있습니다.

### 루트 노드 ID {#root-node-id}

기본적으로 React 응용 프로그램이 요소 ID `spa-root`의 `div` 내에 렌더링된다고 가정합니다. 필요한 경우 사용자 정의할 수 있습니다.

예를 들어 요소 ID `root`의 `div` 내에 응용 프로그램이 렌더링되는 SPA이 있다고 가정합니다. 3개의 파일에 반영해야 합니다.

1. React 응용 프로그램의 `index.js`에서(또는 `ReactDOM.render()`이 호출된 경우)

   ![index.js 파일의 ReactDOM.render()](assets/external-spa-root-index.png)

1. 반응형 응용 프로그램의 `index.html`에서

   ![응용 프로그램의 index.html](assets/external-spa-index.png)

1. 2단계를 통해 AEM 앱의 페이지 구성 요소 본문에서

   1. 페이지 구성 요소에 대해 새 `body.html`을 만듭니다.

   ![새 body.html 파일 만들기](assets/external-spa-update-body.gif)

   1. 새 `body.html` 파일에 새 루트 요소를 추가합니다.

   ![body.html에 루트 요소 추가](assets/external-spa-add-root.png)

### 라우팅 {#editing-react-spa-with-routing}이(가) 있는 반응형 SPA 편집

외부 React SPA 응용 프로그램에 여러 페이지가 있는 경우, 렌더링할 페이지/구성 요소를 결정하는 데 라우팅을 사용할 수 있습니다.[](spa-routing.md) 기본 사용 사례는 현재 활성화된 URL을 경로용으로 제공된 경로와 일치시키는 것입니다. 이러한 라우팅이 활성화된 응용 프로그램에서 편집을 활성화하려면 AEM 관련 정보를 수용하도록 경로를 변형해야 합니다.

다음 예에서는 두 페이지에 간단한 반응형 애플리케이션이 있습니다. 렌더링할 페이지는 활성 URL에 대해 라우터에 제공된 경로를 일치시켜 결정됩니다. 예를 들어 `mydomain.com/test`에 있는 경우 `TestPage`이 렌더링됩니다.

![외부 SPA에서 라우팅](assets/external-spa-routing.png)

이 예시 SPA에서 편집을 활성화하려면 다음 단계가 필요합니다.

1. AEM의 루트로 사용할 수준을 확인합니다.

   * 샘플의 경우 `wknd-spa-react/us/en`을 SPA의 루트로 간주합니다. 즉, 해당 경로 이전의 모든 것이 AEM 전용 페이지/컨텐츠입니다.

1. 필요한 수준에서 새 페이지를 만듭니다.

   * 이 예에서 편집할 페이지는 `mydomain.com/test`입니다. `test` 은 앱의 루트 경로에 있습니다. AEM에서 페이지를 만들 때도 보존해야 합니다. 따라서 이전 단계에서 정의된 루트 수준에서 새 페이지를 만들 수 있습니다.
   * 새로 만든 페이지의 이름은 편집할 페이지와 동일해야 합니다. 이 예에서 `mydomain.com/test`에 대해 새로 만든 페이지는 `/path/to/aem/root/test`이어야 합니다.

1. SPA 라우팅 내에서 도움말을 추가합니다.

   * 새로 만든 페이지는 아직 AEM에서 예상 컨텐츠를 렌더링하지 않습니다. 이는 라우터에 `/test` 경로가 필요한 반면 AEM 활성 경로는 `/wknd-spa-react/us/en/test`이기 때문입니다. URL의 AEM 특정 부분을 수용하기 위해 SPA 측에 일부 도우미를 추가해야 합니다.

   ![라우팅 도우미](assets/external-spa-router-helper.png)

   * 이 경우 `@adobe/cq-spa-page-model-manager`에서 제공하는 `toAEMPath` 도우미를 사용할 수 있습니다. AEM 인스턴스에서 응용 프로그램을 열 때 라우팅에 대해 제공된 경로를 AEM 특정 부분까지 포함하도록 변환하며, 3개의 매개 변수를 사용합니다.
      * 라우팅에 필요한 경로
      * SPA이 편집된 AEM 인스턴스의 원본 URL
      * 첫 번째 단계에서 결정된 대로 AEM에서 프로젝트가 루트됩니다.
   * 이러한 값은 보다 유연하게 사용하기 위해 환경 변수로 설정할 수 있습니다.



1. AEM에서 페이지 편집을 확인합니다.

   * 프로젝트를 AEM에 배포하고 새로 만든 `test` 페이지로 이동합니다. 이제 페이지 컨텐츠가 렌더링되고 AEM 구성 요소가 편집 가능합니다.

## 추가 리소스 {#additional-resources}

다음 참조 자료는 AEM 컨텍스트에서 SPA을 이해하는 데 도움이 될 수 있습니다.

* [AEM 프로젝트 원형](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)
* [WKND SPA 프로젝트](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html)
* [반응을 사용하여 AEM에서 SPA 시작하기](spa-getting-started-react.md)
* [SPA 참조 자료(API 참조)](spa-reference-materials.md)
* [SPA Blueprint 및 PageModelManager](spa-blueprint.md#pagemodelmanager)
* [SPA 모델 라우팅](spa-routing.md)
* [SPA 및 서버측 렌더링](spa-ssr.md)
