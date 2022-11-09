---
title: 장식 태그
description: 웹 페이지의 구성 요소를 렌더링할 때 HTML 요소를 생성하여 자체에 렌더링된 구성 요소를 둘러쌀 수 있습니다. 개발자를 위해 AEM에서는 포함된 구성 요소를 감싸는 데코레이션 태그를 제어하는 분명하고 단순한 로직을 제공합니다.
exl-id: d049ebf1-7fa6-4d2c-86f9-b18e107092ea
source-git-commit: 43a30b5ba76ea470cc50a962d4f04b4a1508964d
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 장식 태그{#decoration-tag}

웹 페이지의 구성 요소를 렌더링할 때 HTML 요소를 생성하여 자체에 렌더링된 구성 요소를 둘러쌀 수 있습니다. 이 기능은 주로 다음 두 가지 용도로 사용됩니다.

* 구성 요소는 HTML 요소로 래핑될 때만 편집할 수 있습니다.
* 래핑 요소는 다음을 제공하는 HTML 클래스를 적용하는 데 사용됩니다.

   * 레이아웃 정보
   * 스타일 정보

개발자를 위해 AEM에서는 포함된 구성 요소를 감싸는 데코레이션 태그를 제어하는 분명하고 단순한 로직을 제공합니다. 데코레이션 태그가 렌더링되는지 여부와 방법은 두 가지 요소의 조합으로 정의되며, 이 페이지는 다음과 같이 분류합니다.

* 구성 요소 자체는 속성 세트로 장식 태그를 구성할 수 있습니다.
* 구성 요소(HTL, JSP, 디스패처 등)를 포함하는 스크립트는 포함 매개 변수로 장식 태그의 측면을 정의할 수 있습니다.

## 권장 사항 {#recommendations}

다음은 예기치 않은 문제가 발생하지 않도록 하는 데 도움이 되는 래퍼 요소를 포함할 시기에 대한 일반적인 권장 사항입니다.

* 페이지의 CSS와 JavaScript가 모든 경우에 동일하게 작동하도록 래퍼 요소의 존재 여부가 WCMMods(편집 또는 미리 보기 모드), 인스턴스(작성자 또는 게시) 또는 환경(스테이징 또는 프로덕션)과 다를 수 없습니다.
* 페이지 편집기가 래퍼 요소를 제대로 초기화하고 업데이트할 수 있도록 래퍼 요소를 편집 가능한 모든 구성 요소에 추가해야 합니다.
* 편집할 수 없는 구성 요소의 경우 특정 함수를 제공하지 않는 경우 래퍼 요소를 피할 수 있으므로 결과 마크업이 불필요하게 팽창되지 않습니다.

## 구성 요소 컨트롤 {#component-controls}

다음 속성 및 노드를 구성 요소에 적용하여 장식 태그의 동작을 제어할 수 있습니다.

* **`cq:noDecoration {boolean}`:** 이 속성을 구성 요소에 추가할 수 있고, true 값을 사용하면 AEM이 구성 요소 위에 래퍼 요소를 생성하지 않습니다.

* **`cq:htmlTag`노드 :** 이 노드는 구성 요소 아래에 추가할 수 있으며 다음 속성을 가질 수 있습니다.

   * **`cq:tagName {String}`:** 이 태그는 기본 DIV 요소 대신 구성 요소를 래핑하는 데 사용할 사용자 지정 HTML 태그를 지정하는 데 사용할 수 있습니다.
   * **`class {String}`:** 래퍼에 추가할 css 클래스 이름을 지정하는 데 사용할 수 있습니다.
   * 다른 속성 이름은 제공된 것과 동일한 문자열 값을 갖는 HTML 속성으로 추가됩니다.

## 스크립트 컨트롤 {#script-controls}

그러나 래퍼 동작은 [HTL](/help/sites-developing/decoration-tag.md#htl) 또는 [JSP](/help/sites-developing/decoration-tag.md#jsp) 요소를 포함하는 데 사용됩니다.

### HTL {#htl}

일반적으로 HTL의 래퍼 동작은 다음과 같이 요약할 수 있습니다.

* 기본적으로 래퍼 DIV가 렌더링되지 않습니다(를 수행할 때). `data-sly-resource="foo"`).
* 모든 wcm 모드(비활성화됨, 미리 보기, 작성자와 게시 모두에서 편집)는 동일하게 렌더링됩니다.

래퍼의 동작은 완전히 제어할 수도 있습니다.

* HTL 스크립트는 래퍼 태그의 결과 동작을 완벽하게 제어할 수 있습니다.
* 구성 요소 속성(예: `cq:noDecoration` 및 `cq:tagName`)에서 래퍼 태그를 정의할 수도 있습니다.

HTL 스크립트에서 래퍼 태그의 동작 및 관련 로직을 완전히 제어할 수 있습니다.

HTL에서의 개발에 대한 자세한 내용은 [HTL 설명서](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html).

#### 의사 결정 트리 {#decision-tree}

이 의사 결정 트리에는 래퍼 태그의 동작을 결정하는 로직이 요약됩니다.

![chlimage_1-75](assets/chlimage_1-75a.png)

#### 사용 사례 {#use-cases}

다음 세 가지 사용 사례에서는 래퍼 태그가 처리되는 방식에 대한 예와 래퍼 태그의 원하는 동작을 제어하는 것이 간단한 방법을 보여줍니다.

다음의 모든 예제는 다음의 컨텐츠 구조 및 구성 요소를 가정합니다.

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

가장 일반적인 사용 사례는 코드 재사용을 위해 구성 요소에 다른 구성 요소가 포함된 경우입니다. 이 경우 포함된 구성 요소는 자체 도구 모음 및 대화 상자에서 편집할 수 없으므로 래퍼가 필요하지 않고 구성 요소의 `cq:htmlTag` 이 무시됩니다. 기본 동작으로 간주할 수 있습니다.

`one.html: <sly data-sly-resource="child"></sly>`

`two.html: Hello World!`

결과 출력 `/content/test.html`:

**`Hello World!`**

예로는 이미지를 표시하는 코어 이미지 구성 요소를 포함하는 구성 요소가 있습니다. 이 경우 일반적으로 합성 리소스를 사용하여 가상 하위 구성 요소를 포함하는 구성 요소는 구성 요소가 가질 모든 속성을 나타내는 Map 개체에 data-sly-resource로 전달하여 구성합니다.

#### 사용 사례 2: 편집 가능한 구성 요소 포함 {#use-case-include-an-editable-component}

또 다른 일반적인 사용 사례는 컨테이너 구성 요소에 레이아웃 컨테이너와 같은 편집 가능한 하위 구성 요소가 포함되는 경우입니다. 이 경우, 포함된 각 자식은 명시적으로 를 사용하여 비활성화하지 않는 한 편집기가 작동하려면 래퍼가 필요하지 않습니다 `cq:noDecoration` Analytics JavaScript용 URL 섹션을 참조하십시오.

포함된 구성 요소는 이 경우 독립 구성 요소이므로 편집기가 작동하고 적용할 레이아웃 및 스타일을 정의해야 합니다. 이 동작을 트리거하기 위해 다음과 같은 항목이 있습니다 `decoration=true` 선택 사항입니다.

`one.html: <sly data-sly-resource="${'child' @ decoration=true}"></sly>`

`two.html: Hello World!`

결과 출력 `/content/test.html`:

**`<article class="component-two">Hello World!</article>`**

#### 사용 사례 3: 사용자 지정 동작 {#use-case-custom-behavior}

HTL을 통해 명시적으로 제공할 수 있으므로 다양한 복잡한 사례가 있을 수 있습니다.

* **`decorationTagName='ELEMENT_NAME'`** 래퍼의 요소 이름을 정의하려면
* **`cssClassName='CLASS_NAME'`** 설정할 CSS 클래스 이름을 정의하려면

`one.html: <sly data-sly-resource="${'child' @ decorationTagName='aside', cssClassName='child'}"></sly>`

`two.html: Hello World!`

결과 출력 `/content/test.html`:

**`<aside class="child">Hello World!</aside>`**

## JSP {#jsp}

구성 요소를 포함할 때 `cq:includ`e 또는 `sling:include`: AEM의 기본 동작은 DIV를 사용하여 요소를 래핑하는 것입니다. 그러나 이 포장은 다음 두 가지 방법으로 사용자 지정할 수 있습니다.

* AEM에서 `cq:noDecoration`.
* 사용자 지정 HTML 태그를 사용하여 `cq:htmlTag`/ `cq:tagName` 또는 `decorationTagName`.

### 의사 결정 트리 {#decision-tree-1}

다음 의사 결정 트리는 `cq:noDecoration`, `cq:htmlTag`, `cq:tagName`, 및 `decorationTagName` 래퍼 동작에 영향을 줍니다.

![chlimage_1-3](assets/chlimage_1-3a.jpeg)
