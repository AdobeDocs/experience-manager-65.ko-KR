---
title: SPA의 합성 구성 요소
description: AEM SPA(Single-Page Application) Editor에서 작동하는 다른 구성 요소로 구성된 고유한 합성 구성 요소를 만드는 방법을 알아봅니다.
translation-type: tm+mt
source-git-commit: 431bed450ed5b0239d9191dcf061f01e64b8981a
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 0%

---


# SPA {#composite-components-in-spas}의 합성 구성 요소

합성 구성 요소는 여러 기본 구성 요소를 단일 구성 요소로 결합하여 AEM 구성 요소의 모듈식 특성을 활용합니다. 일반적인 합성 구성 요소 사용 사례는 이미지와 텍스트 구성 요소의 조합으로 만들어진 카드 구성 요소입니다.

복합 구성 요소가 AEM Single Page Application (SPA) Editor 프레임워크 내에서 올바르게 구현되면 컨텐츠 작성자는 다른 구성 요소처럼 해당 구성 요소를 드래그하여 놓을 수 있지만 합성 구성 요소를 구성하는 각 구성 요소를 개별적으로 편집할 수는 있습니다.

이 문서에서는 AEM SPA 편집기와 원활하게 연동되도록 단일 페이지 애플리케이션에 합성 구성 요소를 추가하는 방법을 설명합니다.

## 사용 사례 {#use-case}

이 아티클은 일반적인 카드 구성 요소를 사용 사례로 사용합니다. 카드는 많은 디지털 경험을 위한 일반적인 UI 요소로서 일반적으로 이미지와 연관된 텍스트 또는 캡션으로 구성됩니다. 작성자는 전체 카드를 드래그 앤 드롭할 수 있지만 카드의 이미지를 개별적으로 편집하고 관련 텍스트를 사용자 정의할 수 있습니다.

## 전제 조건 {#prerequisites}

복합 구성 요소 사용 사례를 지원하기 위한 다음 모델에는 다음 전제 조건이 필요합니다.

* AEM 개발 인스턴스가 샘플 프로젝트를 사용하여 포트 4502에서 로컬로 실행되고 있습니다.
* AEM에서 편집할 수 있는 작업 중인 외부 응답 앱 [이(가) 활성화되어 있습니다.](spa-edit-external.md)
* React 앱은 RemotePage 구성 요소를 사용하여 AEM 편집기 [에 로드됩니다.](spa-remote-page.md)

## SPA {#adding-composite-components}에 합성 구성 요소 추가

AEM 내 SPA 구현에 따라 합성 구성 요소를 구현하는 데 사용할 수 있는 세 가지 모델이 있습니다.

* [구성 요소가 AEM 프로젝트에 없습니다.](#component-does-not-exist)
* [구성 요소는 AEM 프로젝트에 있지만 필요한 컨텐츠는 없습니다.](#content-does-not-exist)
* [구성 요소와 필요한 컨텐츠는 모두 AEM 프로젝트에 있습니다.](#both-exist)

다음 섹션에서는 카드 구성 요소를 예로 사용하여 각 사례를 구현하는 예를 제공합니다.

### 구성 요소가 AEM 프로젝트에 없습니다.{#component-does-not-exist}

먼저 합성 구성 요소(예: 이미지와 해당 텍스트의 구성 요소)를 구성하는 구성 요소를 만듭니다.

1. AEM 프로젝트에서 텍스트 구성 요소를 만듭니다.
1. 구성 요소의 `editConfig` 노드에 있는 프로젝트에서 해당 `resourceType`을 추가합니다.

   ```text
    resourceType: 'wknd-spa/components/text' 
   ```

1. 구성 요소에 대한 편집을 활성화하려면 `withMappable` 도우미를 사용합니다.

   ```text
   export const AEMText = withMappable(Text, TextEditConfig); 
   ```

텍스트 구성 요소는 다음과 유사합니다.

```javascript
import React from 'react';
import { withMappable } from '@adobe/aem-react-editable-components';

export const TextEditConfig = {
  emptyLabel: 'Text',
  isEmpty: function(props) {
    return !props || !props.text || props.text.trim().length < 1;
  },
  resourceType: 'wknd-spa/components/text'
};

export const Text = ({ cqPath, richText, text }) => {
  const richTextContent = () => (
    <div className="aem_text"
      id={cqPath.substr(cqPath.lastIndexOf('/') + 1)}
      data-rte-editelement
      dangerouslySetInnerHTML={{__html: text}} />
  );
  return richText ? richTextContent() : (
     <div className="aem_text">{text}</div>
  );
};

export const AEMText = withMappable(Text, TextEditConfig);
```

비슷한 방식으로 이미지 구성 요소를 만드는 경우 이미지 및 텍스트 구성 요소를 자식으로 사용하여 이미지 구성 요소를 `AEMText` 구성 요소와 결합하여 새 카드 구성 요소에 통합할 수 있습니다.

```javascript
import React from 'react';
import { AEMText } from './AEMText';
import { AEMImage } from './AEMImage';

export const AEMCard = ({ pagePath, itemPath}) => (
  <div>
    <AEMText
       pagePath={pagePath}
       itemPath={`text`} />
    <AEMImage
       pagePath={pagePath}
       itemPath={`image`} />
   </div>
);
```

이렇게 만들어진 합성 구성 요소는 이제 앱의 모든 위치에 배치할 수 있으며, 이 구성 요소는 SPA Editor에서 텍스트 및 이미지 구성 요소의 자리 표시자를 추가합니다. 아래 샘플에서는 카드 구성 요소가 제목 아래의 홈 구성 요소에 추가됩니다.

```javascript
function Home() {
  return (
    <div className="Home">
      <h2>Current Adventures</h2>
      <AEMCard
        pagePath='/content/wknd-spa/home' />
    </div>
  );
}
```

그러면 편집기에 텍스트와 이미지의 빈 자리 표시자가 표시됩니다. 편집기를 사용하여 이러한 값에 값을 입력하면 지정된 페이지 경로(예: `itemPath`에 지정된 이름의 루트 수준에 `/content/wknd-spa/home`)에 저장됩니다.

![편집기의 합성 카드 구성 요소](assets/composite-card.png)

### 구성 요소는 AEM 프로젝트에 있지만 필요한 컨텐츠는 없습니다.{#content-does-not-exist}

이 경우 카드 구성 요소는 제목 및 이미지 노드를 포함하는 AEM 프로젝트에 이미 만들어져 있습니다. 하위 노드(텍스트 및 이미지)에는 해당 리소스 유형이 있습니다.

![카드 구성 요소의 노드 구조](assets/composite-node-structure.png)

그런 다음 SPA에 추가하고 해당 콘텐츠를 검색할 수 있습니다.

1. 이를 위해 SPA에서 해당 구성 요소를 만듭니다. 하위 구성 요소가 SPA 프로젝트 내의 해당 AEM 리소스 유형에 매핑되는지 확인합니다. 이 예제에서는 이전 예제에서 세부 [과 동일한 `AEMText` 및 `AEMImage` 구성 요소를 사용합니다.](#component-does-not-exist)

   ```javascript
   import React from 'react';
   import { Container, withMappable, MapTo } from '@adobe/aem-react-editable-components';
   import { Text, TextEditConfig } from './AEMText';
   import Image, { ImageEditConfig } from './AEMImage';
   
   export const AEMCard = withMappable(Container, {
     resourceType: 'wknd-spa/components/imagecard'
   });
   
   MapTo('wknd-spa/components/text')(Text, TextEditConfig);
   MapTo('wknd-spa/components/image')(Image, ImageEditConfig);
   ```

1. `imagecard` 구성 요소에 대한 내용이 없으므로 페이지에 카드를 추가하십시오. SPA에 AEM의 기존 컨테이너를 포함합니다.
   * AEM 프로젝트에 이미 컨테이너가 있는 경우 대신 SPA에 이 컨테이너를 포함하고 대신 AEM에서 컨테이너에 구성 요소를 추가할 수 있습니다.
   * 카드 구성 요소가 SPA의 해당 리소스 유형에 매핑되는지 확인합니다.

   ```javascript
   <ResponsiveGrid
    pagePath='/content/wknd-spa/home'
    itemPath='root/responsivegrid' />
   ```

1. 만들어진 `wknd-spa/components/imagecard` 구성 요소를 페이지 템플릿에서 컨테이너 구성 요소 [의 허용된 구성 요소에 추가합니다.](/help/sites-authoring/templates.md)

이제 `imagecard` 구성 요소를 AEM 편집기의 컨테이너에 직접 추가할 수 있습니다.

![편집기의 합성 카드](assets/composite-card.gif)

### 구성 요소와 필요한 컨텐츠는 모두 AEM 프로젝트에 있습니다.{#both-exist}

컨텐츠가 AEM에 있는 경우 컨텐츠의 경로를 제공하여 SPA에 직접 포함할 수 있습니다.

```javascript
<AEMCard
    pagePath='/content/wknd-spa/home'
    itemPath='root/responsivegrid/imagecard' />
```

![노드 구조의 합성 경로](assets/composite-path.png)

`AEMCard` 구성 요소는 이전 사용 사례에서 정의된 [과 동일합니다.](#content-does-not-exist) 여기서는 AEM 프로젝트의 위 위치에 정의된 컨텐츠가 SPA에 포함됩니다.
