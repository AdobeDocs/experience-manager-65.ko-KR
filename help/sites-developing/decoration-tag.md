---
title: 장식 태그
description: 웹 페이지의 구성 요소를 렌더링할 때 HTML 요소를 생성하여 자체에 렌더링된 구성 요소를 둘러쌀 수 있습니다. 개발자를 위해 AEM에서는 포함된 구성 요소를 감싸는 데코레이션 태그를 제어하는 분명하고 단순한 로직을 제공합니다.
exl-id: d049ebf1-7fa6-4d2c-86f9-b18e107092ea
source-git-commit: 43a30b5ba76ea470cc50a962d4f04b4a1508964d
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 9%

---

# 장식 태그{#decoration-tag}

웹 페이지의 구성 요소를 렌더링할 때 HTML 요소를 생성하여 자체에 렌더링된 구성 요소를 둘러쌀 수 있습니다. 이는 주로 다음 두 가지 용도로 사용됩니다.

* 구성 요소는 HTML 요소로 래핑될 때만 편집할 수 있습니다.
* 래핑 요소는 다음을 제공하는 HTML 클래스를 적용하는 데 사용됩니다.

   * 레이아웃 정보
   * 스타일 정보

개발자를 위해 AEM에서는 포함된 구성 요소를 감싸는 데코레이션 태그를 제어하는 분명하고 단순한 로직을 제공합니다. 장식 태그의 렌더링 여부와 방법은 이 페이지에서 다룰 두 요소의 조합으로 정의됩니다.

* 구성 요소 자체는 속성 세트로 장식 태그를 구성할 수 있습니다.
* 구성 요소(HTL, JSP, Dispatcher 등)를 포함하는 스크립트는 포함 매개 변수를 사용하여 장식 태그의 측면을 정의할 수 있습니다.

## 권장 사항 {#recommendations}

예기치 않은 문제가 발생하지 않도록 하는 데 도움이 되는 래퍼 요소를 언제 포함할지를 지정하는 일반적인 권장 사항은 다음과 같습니다.

* 래퍼 요소의 존재는 페이지의 CSS와 JavaScripts가 모든 경우에 동일하게 작동하도록 WCMModes(편집 또는 미리보기 모드), 인스턴스(작성자 또는 게시) 또는 환경(스테이징 또는 프로덕션) 간에 달라서는 안 됩니다.
* 페이지 편집기에서 제대로 초기화하고 업데이트할 수 있도록 편집 가능한 모든 구성 요소에 래퍼 요소를 추가해야 합니다.
* 편집할 수 없는 구성 요소의 경우 래퍼 요소가 특정 기능을 수행하지 않으면 결과 마크업이 불필요하게 늘어나지 않도록 방지할 수 있습니다.

## 구성 요소 컨트롤 {#component-controls}

다음 속성 및 노드를 구성 요소에 적용하여 데코레이션 태그의 동작을 제어할 수 있습니다.

* **`cq:noDecoration {boolean}`:** 이 속성을 구성 요소에 추가할 수 있으며, true 값을 지정하면 AEM에서 구성 요소에 래퍼 요소를 생성하지 않습니다.

* **`cq:htmlTag`노드 :** 이 노드는 구성 요소 아래에 추가할 수 있으며 다음과 같은 속성을 가질 수 있습니다.

   * **`cq:tagName {String}`:** 기본 DIV 요소 대신 구성 요소를 래핑하는 데 사용할 사용자 지정 HTML 태그를 지정하는 데 사용할 수 있습니다.
   * **`class {String}`:** 래퍼에 추가할 css 클래스 이름을 지정하는 데 사용할 수 있습니다.
   * 다른 속성 이름은 제공된 것과 동일한 문자열 값을 가진 HTML 속성으로 추가됩니다.

## 스크립트 컨트롤 {#script-controls}

그러나 래퍼 동작은 경우에 따라 다릅니다 [HTL](/help/sites-developing/decoration-tag.md#htl) 또는 [JSP](/help/sites-developing/decoration-tag.md#jsp) 요소를 포함하는 데 사용됩니다.

### HTL {#htl}

일반적으로 HTL의 래퍼 동작은 다음과 같이 요약할 수 있습니다.

* 기본적으로 래퍼 DIV가 렌더링되지 않습니다(다음을 수행하는 경우). `data-sly-resource="foo"`).
* 모든 wcm 모드(비활성화, 작성자 및 게시 모두에서 미리보기, 편집)가 동일하게 렌더링됩니다.

래퍼의 비헤이비어도 완전히 제어할 수 있습니다.

* HTL 스크립트는 래퍼 태그의 최종 동작에 대한 모든 권한을 갖습니다.
* 구성 요소 속성(예: `cq:noDecoration` 및 `cq:tagName`)에서 래퍼 태그를 정의할 수도 있습니다.

HTL 스크립트 및 관련 로직의 래퍼 태그 동작을 완전히 제어할 수 있습니다.

HTL에서의 개발에 대한 자세한 내용은 [HTL 설명서](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html).

#### 의사 결정 트리 {#decision-tree}

이 의사 결정 트리는 래퍼 태그의 동작을 결정하는 논리를 요약합니다.

![chlimage_1-75](assets/chlimage_1-75a.png)

#### 사용 사례 {#use-cases}

다음 세 가지 사용 사례에서는 래퍼 태그가 처리되는 방법의 예를 제공하며, 원하는 래퍼 태그의 동작을 제어하는 것이 얼마나 간단한지도 보여 줍니다.

다음의 모든 예제는 다음 콘텐츠 구조 및 구성 요소를 가정합니다.

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

#### 사용 사례 1: 코드 재사용을 위한 구성 요소 포함 {#use-case-include-a-component-for-code-reuse}

가장 일반적인 사용 사례는 코드 재사용을 위해 구성 요소에 다른 구성 요소가 포함된 경우입니다. 이 경우 포함된 구성 요소는 자체 도구 모음 및 대화 상자로 편집할 수 없으므로 래퍼가 필요하지 않으며 구성 요소의 `cq:htmlTag` 은(는) 무시됩니다. 이는 기본 동작으로 간주할 수 있습니다.

`one.html: <sly data-sly-resource="child"></sly>`

`two.html: Hello World!`

결과 출력 `/content/test.html`:

**`Hello World!`**

예를 들어 이미지를 표시할 핵심 이미지 구성 요소를 포함하는 구성 요소가 있습니다. 이 경우 일반적으로 합성 리소스를 사용하며, 구성 요소는 구성 요소가 가질 모든 속성을 나타내는 맵 개체를 data-sly-resource에 전달하여 가상 하위 구성 요소를 포함하도록 구성됩니다.

#### 사용 사례 2: 편집 가능한 구성 요소 포함 {#use-case-include-an-editable-component}

또 다른 일반적인 사용 사례는 컨테이너 구성 요소에 레이아웃 컨테이너처럼 편집 가능한 하위 구성 요소가 포함된 경우입니다. 이 경우 포함된 각 하위 항목은 편집기가 작동할 래퍼가 필요합니다( 를 사용하여 명시적으로 비활성화하지 않은 경우). `cq:noDecoration` 속성)을 참조하십시오.

포함된 구성 요소는 이 경우 독립적인 구성 요소이므로 편집기가 작동하고 적용할 레이아웃과 스타일을 정의하려면 래퍼 요소가 필요합니다. 이 비헤이비어를 트리거하려면 `decoration=true` 옵션을 선택합니다.

`one.html: <sly data-sly-resource="${'child' @ decoration=true}"></sly>`

`two.html: Hello World!`

결과 출력 `/content/test.html`:

**`<article class="component-two">Hello World!</article>`**

#### 사용 사례 3: 사용자 지정 동작 {#use-case-custom-behavior}

HTL이 다음을 명시적으로 제공할 수 있으므로 쉽게 달성할 수 있는 복잡한 사례는 얼마든지 있을 수 있습니다.

* **`decorationTagName='ELEMENT_NAME'`** 래퍼의 요소 이름을 정의합니다.
* **`cssClassName='CLASS_NAME'`** 설정할 CSS 클래스 이름을 정의합니다.

`one.html: <sly data-sly-resource="${'child' @ decorationTagName='aside', cssClassName='child'}"></sly>`

`two.html: Hello World!`

결과 출력 `/content/test.html`:

**`<aside class="child">Hello World!</aside>`**

## JSP {#jsp}

다음을 사용하여 구성 요소를 포함하는 경우 `cq:includ`e 또는 `sling:include`AEM의 기본 비헤이비어는 DIV를 사용하여 요소를 래핑하는 것입니다. 그러나 이 래핑은 다음 두 가지 방법으로 사용자 정의할 수 있습니다.

* 를 사용하여 구성 요소를 래핑하지 않도록 AEM에 명시적으로 지시합니다. `cq:noDecoration`.
* 사용자 지정 HTML 태그를 사용하여 다음을 사용하여 구성 요소 래핑 `cq:htmlTag`/ `cq:tagName` 또는 `decorationTagName`.

### 의사 결정 트리 {#decision-tree-1}

다음 의사 결정 트리는 방법을 보여 줍니다 `cq:noDecoration`, `cq:htmlTag`, `cq:tagName`, 및 `decorationTagName` 은 래퍼 동작에 영향을 줍니다.

![chlimage_1-3](assets/chlimage_1-3a.jpeg)
