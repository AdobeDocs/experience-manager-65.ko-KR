---
title: 데코레이션 태그
seo-title: 데코레이션 태그
description: 웹 페이지의 구성 요소가 렌더링되면 렌더링된 구성 요소를 자체 내에 래핑하여 HTML 요소를 생성할 수 있습니다. 개발자를 위해 AEM은 포함된 구성 요소를 래핑하는 데코레이션 태그를 제어하는 명확하고 간단한 로직을 제공합니다.
seo-description: 웹 페이지의 구성 요소가 렌더링되면 렌더링된 구성 요소를 자체 내에 래핑하여 HTML 요소를 생성할 수 있습니다. 개발자를 위해 AEM은 포함된 구성 요소를 래핑하는 데코레이션 태그를 제어하는 명확하고 간단한 로직을 제공합니다.
uuid: db796a22-b053-48dd-a50c-354dead7e8ec
contentOwner: user
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 8cb9fd6e-5e1f-43cd-8121-b490dee8c2be
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835

---


# 데코레이션 태그{#decoration-tag}

>[!NOTE]
>
>이 문서에 설명된 데코레이션 태그 동작 및 옵션은 AEM 6. [3 CFP1을](https://helpx.adobe.com/experience-manager/release-notes--aem-6-3-cumulative-fix-pack.html)기반으로 합니다.
>
>CFP1 이전 6.3의 데코레이션 태그의 동작은 AEM 6.2의 동작과 유사합니다.

웹 페이지의 구성 요소가 렌더링되면 렌더링된 구성 요소를 자체 내에 래핑하여 HTML 요소를 생성할 수 있습니다. 이 기능은 주로 두 가지 목적으로 사용됩니다.

* 구성 요소는 HTML 요소로 래핑된 경우에만 편집할 수 있습니다.
* 래핑 요소는 다음을 제공하는 HTML 클래스를 적용하는 데 사용됩니다.

   * 레이아웃 정보
   * 스타일 정보

개발자를 위해 AEM은 포함된 구성 요소를 래핑하는 데코레이션 태그를 제어하는 명확하고 간단한 로직을 제공합니다. 데코레이션 태그가 렌더링되는지 여부와 어떻게 렌더링되는지는 이 페이지에서 설명하는 두 가지 요소의 조합으로 정의됩니다.

* 구성 요소 자체는 속성 집합을 사용하여 데코레이션 태그를 구성할 수 있습니다.
* 구성 요소(HTL, JSP, 디스패처 등)가 포함된 스크립트는 포함 매개 변수를 사용하여 데코레이션 태그의 측면을 정의할 수 있습니다.

## 추천 {#recommendations}

다음은 예기치 않은 문제로 인한 실행을 방지하는 데 도움이 되는 래퍼 요소를 포함할 시기에 대한 일반적인 권장 사항입니다.

* 래퍼 요소의 존재 여부는 WCMMods(편집 또는 미리 보기 모드), 인스턴스(작성자 또는 게시) 또는 환경(스테이징 또는 프로덕션)과 달라야 하므로 페이지의 CSS와 JavaScript가 모든 경우에 동일하게 작동합니다.
* 페이지 편집기가 래퍼 요소를 제대로 초기화하고 업데이트할 수 있도록 래퍼 요소를 편집 가능한 모든 구성 요소에 추가해야 합니다.
* 편집할 수 없는 구성 요소의 경우 래퍼 요소가 특정 기능을 제공하지 않는 경우 이를 방지하여 결과 마크업이 불필요하게 부풀려지지 않습니다.

## 구성 요소 컨트롤 {#component-controls}

다음 속성 및 노드를 구성 요소에 적용하여 데코레이션 태그의 동작을 제어할 수 있습니다.

* **`cq:noDecoration {boolean}`**:이 속성을 구성 요소에 추가할 수 있으며 true 값을 사용하면 AEM이 구성 요소 위에 래퍼 요소를 생성하지 않습니다.

* **`cq:htmlTag`**node :이 노드는 구성 요소 아래에 추가할 수 있으며 다음 속성을 가질 수 있습니다.

   * **`cq:tagName {String}`**:기본 DIV 요소 대신 구성 요소를 래핑하는 데 사용할 사용자 지정 HTML 태그를 지정하는 데 사용할 수 있습니다.
   * **`class {String}`**:래퍼에 추가할 css 클래스 이름을 지정하는 데 사용할 수 있습니다.
   * 다른 속성 이름은 제공된 것과 동일한 문자열 값을 갖는 HTML 속성으로 추가됩니다.

## 스크립트 컨트롤 {#script-controls}

래퍼 동작은 다르지만 HTL 또는 JSP [를](/help/sites-developing/decoration-tag.md#htl) 사용하여 [요소를](/help/sites-developing/decoration-tag.md#jsp) 포함하는지 여부에 따라 달라집니다.

### HTL {#htl}

일반적으로 HTL의 래퍼 동작은 다음과 같이 요약할 수 있습니다.

* No wrapper DIV is rendered by default (when just doing). `data-sly-resource="foo"`
* 모든 wcm-modes(비활성화, 미리 보기, 작성자 및 게시 모두에서 편집) 동일하게 렌더링됩니다.

또한 래퍼의 동작을 완벽하게 제어할 수 있습니다.

* HTL 스크립트는 래퍼 태그의 결과 동작을 완전히 제어합니다.
* 구성 요소 속성(예: `cq:noDecoration` 및 `cq:tagName`)은 래퍼 태그를 정의할 수도 있습니다.

HTL 스크립트에서 래퍼 태그의 비헤이비어와 관련 로직을 완벽하게 제어할 수 있습니다.

HTL에서의 개발에 대한 자세한 내용은 HTL [설명서를](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html)참조하십시오.

#### 의사 결정 트리 {#decision-tree}

이 결정 트리는 래퍼 태그의 동작을 결정하는 논리를 요약합니다.

![chlimage_1-75](assets/chlimage_1-75a.png)

#### Use Cases {#use-cases}

다음 세 가지 사용 사례에서는 래퍼 태그가 처리되는 방식에 대한 예와 래퍼 태그의 원하는 동작을 간단하게 제어하는 방법을 보여 줍니다.

다음에 나오는 모든 예는 다음과 같은 컨텐츠 구조 및 구성 요소를 가정합니다.

```
/content/test/
  @resourceType = "test/components/one"
  child/
    @resourceType = "test/components/two"
```

```
/apps/test/components/
  one/
    one.html
  two/
    two.html
    cq:htmlTag/
      @cq:tagName = "article"
      @class = "component-two"
```

#### 사용 사례 1:코드 재사용을 위한 구성 요소 포함 {#use-case-include-a-component-for-code-reuse}

가장 일반적인 사용 사례는 구성 요소에 코드 재사용을 위해 다른 구성 요소가 포함되는 경우입니다. 이 경우 포함된 구성 요소는 자체 도구 모음과 대화 상자를 사용하여 편집할 수 없도록 해야 하므로 래퍼가 필요하지 않으므로 구성 요소의 구성 요소는 `cq:htmlTag` 무시됩니다. 기본 동작으로 간주할 수 있습니다.

`one.html: <sly data-sly-resource="child"></sly>`

`two.html: Hello World!`

결과 출력 기준 `/content/test.html`:

**`Hello World!`**

예를 들어, 이미지를 표시하는 핵심 이미지 구성 요소를 포함하는 구성 요소로서, 일반적으로 합성 리소스를 사용하여 구성 요소를 포함하는 구성 요소로서, 가상 하위 구성 요소는 구성 요소의 모든 속성을 나타내는 Map 개체에 데이터-ly 리소스로 전달하여 포함됩니다.

#### 사용 사례 2:편집 가능한 구성 요소 포함 {#use-case-include-an-editable-component}

또 다른 일반적인 사용 사례는 컨테이너 구성 요소에 레이아웃 컨테이너와 같은 편집 가능한 하위 구성 요소가 포함되는 경우입니다. 이 경우, 포함된 각 하위 항목은 편집기가 제대로 작동하기 위해 래퍼가 필요합니다( `cq:noDecoration` 속성을 사용하여 명시적으로 비활성화하지 않은 경우).

포함된 구성 요소는 이 경우에 독립적인 구성 요소이므로 편집기가 작동하기 위해 래퍼 요소가 필요하며, 적용할 레이아웃과 스타일을 정의해야 합니다. 이 동작을 트리거하기 위한 `decoration=true` 옵션이 있습니다.

`one.html: <sly data-sly-resource="${'child' @ decoration=true}"></sly>`

`two.html: Hello World!`

결과 출력 기준 `/content/test.html`:

**`<article class="component-two">Hello World!</article>`**

#### 사용 사례 3:사용자 지정 동작 {#use-case-custom-behavior}

HTL이 명시적으로 제공할 수 있는 가능성이 있는 복잡한 사례는 얼마든지 있을 수 있습니다.

* **`decorationTagName='ELEMENT_NAME'`** 래퍼의 요소 이름을 정의하려면
* **`cssClassName='CLASS_NAME'`** 설정할 CSS 클래스 이름을 정의하려면

`one.html: <sly data-sly-resource="${'child' @ decorationTagName='aside', cssClassName='child'}"></sly>`

`two.html: Hello World!`

결과 출력 `/content/test.html`:

**`<aside class="child">Hello World!</aside>`**

## JSP {#jsp}

e 또는 `cq:includ`를 사용하여 구성 요소를 포함할 `sling:include`경우 AEM의 기본 동작은 DIV를 사용하여 요소를 래핑하는 것입니다. 그러나 다음 두 가지 방법으로 이 래핑을 사용자 지정할 수 있습니다.

* AEM에 구성 요소를 래핑하지 않도록 명시적으로 `cq:noDecoration`지정합니다.
* 사용자 지정 HTML 태그를 사용하여 `cq:htmlTag`/ `cq:tagName` 또는 `decorationTagName`를 사용하여 구성 요소를 래핑합니다.

### 의사 결정 트리 {#decision-tree-1}

다음 의사 결정 트리는 래퍼 동작에 `cq:noDecoration`대한 방법, `cq:htmlTag``cq:tagName`및 `decorationTagName` 영향을 보여 줍니다.

![chlimage_1-3](assets/chlimage_1-3a.jpeg)

