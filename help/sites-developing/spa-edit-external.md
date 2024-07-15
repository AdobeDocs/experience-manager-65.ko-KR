---
title: Adobe Experience Manager 내에서 외부 SPA 편집
description: 이 문서에서는 독립 실행형 SPA을 Adobe Experience Manager 인스턴스에 업로드하고, 편집 가능한 콘텐츠 섹션을 추가하고, 저작을 활성화하는 권장 단계에 대해 설명합니다.
exl-id: 25236af4-405a-4152-8308-34d983977e9a
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '2391'
ht-degree: 0%

---

# Adobe Experience Manager 내에서 외부 SPA 편집 {#editing-external-spa-within-aem}

외부 SPA과 Adobe Experience Manager(AEM) 간에 원하는 통합 수준을 결정할 때 AEM 내에서 SPA을 편집하고 볼 수 있어야 하는 경우가 많습니다.

## 개요 {#overview}

이 문서에서는 독립 실행형 SPA을 AEM 인스턴스에 업로드하고, 편집 가능한 콘텐츠 섹션을 추가하고, 저작을 활성화하는 권장 단계에 대해 설명합니다.

## 사전 요구 사항 {#prerequisites}

사전 요구 사항은 간단합니다.

* AEM 인스턴스가 로컬에서 실행 중인지 확인합니다.
* [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?#available-properties)을(를) 사용하여 기본 AEM SPA 프로젝트를 만듭니다.
   * 이는 외부 SPA을 포함하도록 업데이트되는 AEM 프로젝트의 기초가 됩니다.
   * 이 문서의 샘플은 [WKND SPA 프로젝트](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html#spa-editor)의 시작점을 사용합니다.
* 즉시 통합하고자 하는 작동 중인 외부 React SPA이 있습니다.

## AEM 프로젝트에 SPA 업로드 {#upload-spa-to-aem-project}

먼저 외부 SPA을 AEM 프로젝트에 업로드해야 합니다.

1. `/ui.frontend` 프로젝트 폴더의 `src`을(를) React 응용 프로그램의 `src` 폴더로 바꾸십시오.
1. `/ui.frontend/package.json` 파일에 있는 앱의 `package.json`에 추가 종속성을 포함하십시오.
   * SPA SDK 종속성이 [권장 버전](spa-getting-started-react.md#dependencies)인지 확인하십시오.
1. `/public` 폴더에 모든 사용자 지정을 포함합니다.
1. `/public/index.html` 파일에 추가된 모든 인라인 스크립트나 스타일을 포함합니다.

## 원격 SPA 구성 {#configure-remote-spa}

이제 외부 SPA은 AEM 프로젝트의 일부이므로 AEM 내에서 구성해야 합니다.

### Adobe SPA SDK 패키지 포함 {#include-spa-sdk-packages}

AEM SPA 기능을 활용하기 위해 다음 세 가지 패키지에 종속성이 있습니다.

* [`@adobe/aem-react-editable-components`](https://github.com/adobe/aem-react-editable-components)
* [`@adobe/aem-spa-component-mapping`](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)
* [`@adobe/aem-spa-page-model-manager`](https://www.npmjs.com/package/@adobe/aem-spa-model-manager)

`@adobe/aem-spa-page-model-manager`은(는) 모델 관리자를 초기화하고 AEM 인스턴스에서 모델을 검색하기 위한 API를 제공합니다. 그런 다음 `@adobe/aem-react-editable-components` 및 `@adobe/aem-spa-component-mapping`의 API를 사용하여 AEM 구성 요소를 렌더링하는 데 이 모델을 사용할 수 있습니다.

#### 설치 {#installation}

다음 npm 명령을 실행하여 필요한 패키지를 설치합니다.

```shell
npm install --save @adobe/aem-spa-component-mapping @adobe/aem-spa-page-model-manager @adobe/aem-react-editable-components
```

### ModelManager 초기화 {#model-manager-initialization}

앱이 렌더링되기 전에 AEM `ModelStore`의 생성을 처리하려면 [`ModelManager`](spa-blueprint.md#pagemodelmanager)을(를) 초기화해야 합니다.

이 작업은 응용 프로그램의 `src/index.js` 파일 내에서 또는 응용 프로그램의 루트가 렌더링되는 모든 위치에서 수행해야 합니다.

이를 위해 `ModelManager`에서 제공한 `initializationAsync` API를 사용하십시오.

다음 스크린샷은 간단한 React 애플리케이션에서 `ModelManager`의 초기화를 활성화하는 방법을 보여 줍니다. 유일한 제약 조건은 `ReactDOM.render()` 전에 `initializationAsync`을(를) 호출해야 한다는 것입니다.

![ModelManager 초기화](assets/external-spa-initialize-modelmanager.png)

이 예제에서는 `ModelManager`이(가) 초기화되고 빈 `ModelStore`이(가) 만들어집니다.

`initializationAsync`은(는) 필요에 따라 `options` 개체를 매개 변수로 허용할 수 있습니다.

* `path` - 초기화 시 정의된 경로의 모델을 가져와서 `ModelStore`에 저장합니다. 필요한 경우 초기화 시 `rootModel`을(를) 가져오는 데 사용할 수 있습니다.
* `modelClient` - 모델 가져오기를 담당하는 사용자 지정 클라이언트를 제공할 수 있습니다.
* `model` - [SSR을 사용할 때 ](spa-ssr.md) 매개 변수로 전달된 `model` 개체

### AEM Authorable Leaf 구성 요소 {#authorable-leaf-components}

1. 작성 가능한 React 구성 요소가 생성될 AEM 구성 요소를 생성/식별합니다. 이 예에서 WKND 프로젝트는 텍스트 구성 요소를 사용하고 있습니다.

   ![WKND 텍스트 구성 요소](assets/external-spa-text-component.png)

1. SPA에서 간단한 React 텍스트 구성 요소를 만듭니다. 이 예제에서는 다음 콘텐츠로 새 파일 `Text.js`을(를) 만들었습니다.

   ![Text.js](assets/external-spa-textjs.png)

1. 구성 객체를 생성하여 AEM 편집을 활성화하는 데 필요한 속성을 지정합니다.

   ![구성 개체 만들기](assets/external-spa-config-object.png)

   * `resourceType`은(는) React 구성 요소를 AEM 구성 요소에 매핑하고 AEM 편집기에서 열 때 편집을 활성화하려면 필수입니다.

1. 래퍼 함수 `withMappable`을(를) 사용합니다.

   ![Mappable과 함께 사용](assets/external-spa-withmappable.png)

   이 래퍼 함수는 React 구성 요소를 구성에 지정된 AEM `resourceType`에 매핑하고 AEM 편집기에서 열면 편집 기능을 사용하도록 설정합니다. 독립형 구성 요소의 경우 특정 노드에 대한 모델 콘텐츠도 가져옵니다.

   >[!NOTE]
   >
   >이 예에는 구성 요소의 개별 버전인 AEM 래핑된 구성 요소와 래핑되지 않은 React 구성 요소가 있습니다. 구성 요소를 명시적으로 사용할 때는 래핑된 버전을 사용해야 합니다. 구성 요소가 페이지의 일부인 경우 SPA 편집기에서 현재 작업을 수행한 대로 기본 구성 요소를 계속 사용할 수 있습니다.

1. 구성 요소에서 콘텐츠를 렌더링합니다.

   텍스트 구성 요소의 JCR 속성은 AEM에서 다음과 같이 표시됩니다.

   ![텍스트 구성 요소 속성](assets/external-spa-text-properties.png)

   이러한 값은 새로 만든 `AEMText` React 구성 요소에 속성으로 전달되며 콘텐츠를 렌더링하는 데 사용할 수 있습니다.

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

   AEM 구성이 완료되면 구성 요소가 표시됩니다.

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
   >이 예제에서는 렌더링된 구성 요소를 기존 텍스트 구성 요소와 일치하도록 추가로 사용자 지정했습니다. 그러나 이는 AEM의 작성과 관련이 없습니다.

#### 페이지에 작성 가능한 구성 요소 추가 {#add-authorable-component-to-page}

작성 가능한 React 구성 요소가 생성되면 애플리케이션 전체에서 사용할 수 있습니다.

WKND SPA 프로젝트의 텍스트를 추가해야 하는 예제 페이지를 예로 들어 보겠습니다. 이 예제에서는 &quot;Hello World!&quot; 텍스트를 표시합니다. `/content/wknd-spa-react/us/en/home.html`에.

1. 표시할 노드의 경로를 결정합니다.

   * `pagePath`: `/content/wknd-spa-react/us/en/home` 예제에서 노드가 포함된 페이지
   * `itemPath`: 페이지 내의 노드 경로(예: `root/responsivegrid/text`)
      * 이 이름은 페이지에 있는 포함 항목의 이름으로 구성됩니다.

   ![노드의 경로](assets/external-spa-path.png)

1. 페이지에서 필요한 위치에 구성 요소를 추가합니다.

   ![페이지에 구성 요소 추가](assets/external-spa-add-component.png)

   `pagePath` 및 `itemPath` 값이 속성으로 설정된 페이지 내에서 필요한 위치에 `AEMText` 구성 요소를 추가할 수 있습니다. `pagePath`은(는) 필수 속성입니다.

#### AEM에서 텍스트 컨텐츠 편집 확인 {#verify-text-edit}

이제 실행 중인 AEM 인스턴스에서 구성 요소를 테스트합니다.

1. `aem-guides-wknd-spa` 디렉터리에서 다음 Maven 명령을 실행하여 프로젝트를 빌드하고 AEM에 배포합니다.

```shell
mvn clean install -PautoInstallSinglePackage
```

1. AEM 인스턴스에서 `http://<host>:<port>/editor.html/content/wknd-spa-react/us/en/home.html`(으)로 이동합니다.

![AEM에서 SPA 편집](assets/external-spa-edit-aem.png)

이제 AEM에서 `AEMText` 구성 요소를 작성할 수 있습니다.

### AEM 승인 가능 페이지 {#aem-authorable-pages}

1. SPA에서 작성하기 위해 추가할 페이지를 식별합니다. 이 예제에서는 `/content/wknd-spa-react/us/en/home.html`을(를) 사용합니다.
1. 작성 가능한 페이지 구성 요소에 대한 파일(예: `Page.js`)을 만듭니다. 여기에서 `@adobe/cq-react-editable-components`에서 제공된 페이지 구성 요소를 다시 사용할 수 있습니다.
1. [AEM 승인 가능한 리프 구성 요소](#authorable-leaf-components) 섹션에서 4단계를 반복합니다. 구성 요소에서 래퍼 함수 `withMappable`을(를) 사용합니다.
1. 이전에 수행한 대로 페이지 내의 모든 하위 구성 요소에 대한 AEM 리소스 유형에 `MapTo`을(를) 적용합니다.

   ```javascript
   import { Page, MapTo, withMappable } from '@adobe/aem-react-editable-components';
   import Text, { TextEditConfig } from './Text';
   
   export default withMappable(Page);
   
   MapTo('wknd-spa-react/components/text')(Text, TextEditConfig);
   ```

   >[!NOTE]
   >
   >이 예제에서는 이전에 만든 래핑된 `AEMText` 대신 래핑되지 않은 React 텍스트 구성 요소를 사용하고 있습니다. 구성 요소가 페이지/컨테이너의 일부이며 독립 실행형이 아닌 경우 컨테이너는 구성 요소를 재귀적으로 매핑하고 작성 기능을 활성화하므로 각 하위 항목에 대해 추가 래퍼가 필요하지 않습니다.

1. SPA에서 작성 가능한 페이지를 추가하려면 [페이지에 작성 가능한 구성 요소 추가](#add-authorable-component-to-page) 섹션에서 동일한 단계를 수행합니다. 그러나 여기서는 `itemPath` 속성을 건너뛸 수 있습니다.

#### AEM에서 페이지 컨텐츠 확인 {#verify-page-content}

페이지를 편집할 수 있는지 확인하려면 [AEM에서 텍스트 콘텐츠 편집 확인](#verify-text-edit) 섹션에서 동일한 단계를 수행합니다.

![AEM에서 페이지 편집](assets/external-spa-edit-page.png)

이제 레이아웃 컨테이너 및 하위 텍스트 구성 요소를 사용하여 AEM에서 페이지를 편집할 수 있습니다.

### 가상 리프 구성 요소 {#virtual-leaf-components}

앞의 예제에서는 기존 AEM 컨텐츠가 있는 SPA에 구성 요소를 추가했습니다. 그러나 AEM에서 아직 콘텐츠를 만들지 않았지만 콘텐츠 작성자가 나중에 추가해야 하는 경우가 있습니다. 이를 수용하기 위해 프론트엔드 개발자는 SPA 내의 적절한 위치에 구성 요소를 추가할 수 있습니다. 이러한 구성 요소는 AEM의 편집기에서 열리면 자리 표시자를 표시합니다. 콘텐츠 작성자가 이러한 자리 표시자 내에 콘텐츠를 추가하면 노드가 JCR 구조로 만들어지고 콘텐츠가 유지됩니다. 생성된 구성 요소는 독립 실행형 리프 구성 요소와 동일한 작업 세트를 허용합니다.

이 예제에서는 이전에 만든 `AEMText` 구성 요소를 다시 사용합니다. WKND 홈 페이지의 기존 텍스트 구성 요소 아래에 새 텍스트를 추가하려고 합니다. 컴포넌트 추가는 일반 리프 컴포넌트와 동일합니다. 그러나 새 구성 요소를 추가해야 하는 경로로 `itemPath`을(를) 업데이트할 수 있습니다.

새 구성 요소를 `root/responsivegrid/text`의 기존 텍스트 아래에 추가해야 하므로 새 경로는 `root/responsivegrid/{itemName}`이(가) 됩니다.

```html
<AEMText
 pagePath='/content/wknd-spa-react/us/en/home'
 itemPath='root/responsivegrid/text_20' />
```

가상 구성 요소를 추가한 후 `TestPage` 구성 요소는 다음과 같습니다.

![가상 구성 요소 테스트](assets/external-spa-virtual-component.png)

>[!NOTE]
>
>이 기능을 사용하려면 구성에 `AEMText` 구성 요소의 `resourceType`이(가) 설정되어 있는지 확인하십시오.

이제 [AEM에서 텍스트 콘텐츠 편집 확인](#verify-text-edit) 섹션의 단계에 따라 변경 사항을 AEM에 배포할 수 있습니다. 현재 존재하지 않는 `text_20` 노드에 대한 자리 표시자가 표시됩니다.

![aem의 text_20 노드](assets/external-spa-text20-aem.png)

콘텐츠 작성자가 이 구성 요소를 업데이트하면 `/content/wknd-spa-react/us/en/home`의 `root/responsivegrid/text_20`에 새 `text_20` 노드가 만들어집니다.

![text20 노드](assets/external-spa-text20-node.png)

#### 요구 사항 및 제한 사항 {#limitations}

가상 리프 구성 요소를 추가하기 위한 몇 가지 요구 사항과 몇 가지 제한 사항이 있습니다.

* 가상 구성 요소를 만들려면 `pagePath` 속성이 필수입니다.
* `pagePath`의 경로에 제공된 페이지 노드가 AEM 프로젝트에 있어야 합니다.
* 만들 노드의 이름을 `itemPath`에 입력해야 합니다.
* 구성 요소는 모든 수준에서 만들 수 있습니다.
   * 앞의 예제에서 `itemPath='text_20'`을(를) 제공하면 새 노드가 페이지 바로 아래에 만들어집니다. 즉, `/content/wknd-spa-react/us/en/home/jcr:content/text_20`
* 새 노드가 만들어지는 노드의 경로는 `itemPath`을(를) 통해 제공된 경우 유효해야 합니다.
   * 이 예제에서는 새 노드 `text_20`을(를) 만들려면 `root/responsivegrid`이(가) 있어야 합니다.
* 리프 구성 요소 생성만 지원됩니다. 가상 컨테이너 및 페이지는 이후 버전에서 지원됩니다.

### 가상 컨테이너 {#virtual-containers}

해당 컨테이너가 AEM에서 아직 만들어지지 않은 경우에도 컨테이너를 추가하는 기능이 지원됩니다. 개념 및 접근 방식은 [가상 리프 구성 요소](#virtual-leaf-components)와(과) 유사합니다.

프론트엔드 개발자는 SPA 내의 적절한 위치에 컨테이너 구성 요소를 추가할 수 있으며, AEM의 편집기에서 열면 이러한 구성 요소에 자리 표시자가 표시됩니다. 그런 다음 작성자는 구성 요소와 해당 콘텐츠를 컨테이너에 추가하여 JCR 구조에 필요한 노드를 만들 수 있습니다.

예를 들어, 컨테이너가 `/root/responsivegrid`에 이미 있고 개발자가 새 하위 컨테이너를 추가하려는 경우:

![컨테이너 위치](assets/container-location.png)

`newContainer`이(가) 아직 AEM에 없습니다.

AEM에서 이 구성 요소가 포함된 페이지를 편집할 때 작성자가 컨텐츠를 추가할 수 있는 컨테이너에 대한 빈 자리 표시자가 표시됩니다.

![컨테이너 자리 표시자](assets/container-placeholder.png)

![JCR의 컨테이너 위치](assets/container-jcr-structure.png)

작성자가 하위 구성 요소를 컨테이너에 추가하면 새 컨테이너 노드가 JCR 구조에서 해당 이름으로 만들어집니다.

![콘텐츠가 있는 컨테이너](assets/container-with-content.png)

![JCR의 콘텐츠가 있는 컨테이너](assets/container-with-content-jcr.png)

작성자가 필요로 하므로 이제 더 많은 구성 요소와 콘텐츠를 컨테이너에 추가할 수 있으며 변경 사항은 지속됩니다.

#### 요구 사항 및 제한 사항 {#container-limitations}

가상 컨테이너를 추가하기 위한 몇 가지 요구 사항과 몇 가지 제한 사항이 있습니다.

* 추가할 수 있는 구성 요소를 결정하는 정책은 상위 컨테이너에서 상속됩니다.
* 만들 컨테이너의 바로 상위 항목이 AEM에 이미 있어야 합니다.
   * `root/responsivegrid` 컨테이너가 이미 AEM 컨테이너에 있는 경우 `root/responsivegrid/newContainer` 경로를 제공하여 새 컨테이너를 만들 수 있습니다.
   * 그러나 `root/responsivegrid/newContainer/secondNewContainer`은(는) 가능하지 않습니다.
* 한 번에 하나의 새로운 수준의 구성 요소만 가상으로 만들 수 있습니다.

## 추가 사용자 정의 {#additional-customizations}

이전 예제를 따랐다면 이제 AEM 내에서 외부 SPA을 편집할 수 있습니다. 그러나 추가로 사용자 정의할 수 있는 외부 SPA의 추가 측면이 있습니다.

### 루트 노드 ID {#root-node-id}

기본적으로 React 응용 프로그램이 요소 ID `spa-root`의 `div` 내에서 렌더링된다고 가정합니다. 필요한 경우 이를 사용자 정의할 수 있습니다.

예를 들어 요소 ID `root`의 `div` 내에서 응용 프로그램이 렌더링되는 SPA이 있다고 가정해 보겠습니다. 이는 세 가지 파일에 반영되어야 합니다.

1. React 응용 프로그램의 `index.js`(또는 `ReactDOM.render()`이(가) 호출된 경우)에서

   index.js 파일의 ![ReactDOM.render()](assets/external-spa-root-index.png)

1. React 응용 프로그램의 `index.html`에서

   ![응용 프로그램의 index.html](assets/external-spa-index.png)

1. 다음 두 단계를 통해 AEM 앱의 페이지 구성 요소 본문에서 확인할 수 있습니다.

   1. 페이지 구성 요소에 대한 `body.html`을(를) 만듭니다.

   ![body.html 파일 만들기](assets/external-spa-update-body.gif)

   1. 새 `body.html` 파일에 새 루트 요소를 추가합니다.

   ![body.html에 루트 요소 추가](assets/external-spa-add-root.png)

### 라우팅으로 React SPA 편집 {#editing-react-spa-with-routing}

외부 React SPA 응용 프로그램에 여러 페이지가 있는 경우 [라우팅을 사용하여 렌더링할 페이지/구성 요소를 결정할 수 있습니다](spa-routing.md). 기본 사용 사례는 경로에 대해 제공된 경로에 대해 현재 활성화된 URL을 일치시키는 것입니다. 이러한 라우팅 지원 응용 프로그램에서 편집할 수 있도록 하려면 AEM 관련 정보를 수용하도록 일치시킬 경로를 변환해야 합니다.

다음 예에는 두 개의 페이지가 있는 간단한 React 애플리케이션이 있습니다. 렌더링할 페이지는 라우터에 제공된 경로를 활성 URL과 일치시켜 결정됩니다. 예를 들어 `mydomain.com/test`에 있으면 `TestPage`이(가) 렌더링됩니다.

외부 SPA에서 ![라우팅](assets/external-spa-routing.png)

이 예제 SPA에 대해 AEM 내에서 편집을 활성화하려면 다음 단계를 수행해야 합니다.

1. AEM에서 루트로 사용할 레벨을 식별합니다.

   * 샘플의 경우 `wknd-spa-react/us/en`을(를) SPA의 루트로 간주합니다. 즉, 해당 경로 이전의 모든 항목은 AEM 전용 페이지/컨텐츠입니다.

1. 필요한 수준에서 페이지를 만듭니다.

   * 이 예제에서 편집할 페이지는 `mydomain.com/test`입니다. `test`이(가) 앱의 루트 경로에 있습니다. AEM에서 페이지를 만들 때도 이 상태를 유지해야 합니다. 따라서 이전 단계에서 정의된 루트 수준에서 페이지를 만들 수 있습니다.
   * 작성된 새 페이지는 편집할 페이지와 이름이 같아야 합니다. `mydomain.com/test`에 대한 이 예제에서 새 페이지는 `/path/to/aem/root/test`이어야 합니다.

1. SPA 라우팅 내에 도우미를 추가합니다.

   * 새로 만든 페이지는 아직 AEM의 예상 콘텐츠를 렌더링하지 않습니다. 이는 라우터에는 `/test` 경로가 필요한데 AEM 활성 경로는 `/wknd-spa-react/us/en/test`이기 때문입니다. URL의 AEM 관련 부분을 수용하려면 SPA 측에 몇 가지 도우미를 추가해야 합니다.

   ![라우팅 도우미](assets/external-spa-router-helper.png)

   * 이 작업에는 `@adobe/cq-spa-page-model-manager`에서 제공한 `toAEMPath` 도우미를 사용할 수 있습니다. AEM 인스턴스에서 애플리케이션이 열려 있을 때 AEM 관련 부분을 포함하도록 라우팅에 제공된 경로를 변환합니다. 세 가지 매개 변수를 사용할 수 있습니다.
      * 라우팅에 필요한 경로
      * SPA이 편집되는 AEM 인스턴스의 원본 URL
      * 첫 번째 단계에서 결정된 대로 AEM의 프로젝트 루트

   * 이러한 값은 보다 유연하게 사용할 수 있도록 환경 변수로 설정할 수 있습니다.

1. AEM에서 페이지 편집을 확인합니다.

   * AEM에 프로젝트를 배포하고 새로 만든 `test` 페이지로 이동합니다. 이제 페이지 콘텐츠가 렌더링되고 AEM 구성 요소를 편집할 수 있습니다.

## 프레임워크 제한 사항 {#framework-limitations}

RemotePage 구성 요소에서는 구현이 [여기에 있는 ](https://github.com/shellscape/webpack-manifest-plugin)과(와) 같은 자산 매니페스트를 제공할 것으로 예상합니다. 그러나 RemotePage 구성 요소는 React 프레임워크(및 remote-page-next 구성 요소를 통한 Next.js)에서만 작동하도록 테스트되었으므로 Angular과 같은 다른 프레임워크에서 원격으로 응용 프로그램을 로드할 수 없습니다.

## 추가 리소스 {#additional-resources}

다음 참조 자료가 AEM의 컨텍스트에서 SPA을 이해하는 데 도움이 될 수 있습니다.

* [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)
* [WKND SPA 프로젝트](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html?lang=ko-KR)
* [React를 사용하여 AEM에서 SPA 시작하기](spa-getting-started-react.md)
* [SPA 참조 자료(API 참조)](spa-reference-materials.md)
* [SPA 블루프린트 및 PageModelManager](spa-blueprint.md#pagemodelmanager)
* [SPA 모델 라우팅](spa-routing.md)
* [SPA 및 서버측 렌더링](spa-ssr.md)
