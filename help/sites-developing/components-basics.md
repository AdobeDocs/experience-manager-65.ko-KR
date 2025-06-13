---
title: Adobe Experience Manager 구성 요소 - 기본 사항
description: 새 구성 요소를 개발하기 시작하려면 해당 구성 요소의 구조 및 구성에 대한 기본 사항을 이해해야 합니다.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
legacypath: /content/docs/en/aem/6-0/develop/components/components-develop
exl-id: 7ff92872-697c-4e66-b654-15314a8cb429
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: f96b178ae84b4b930b59e36d4994970682c53dbd
workflow-type: tm+mt
source-wordcount: '4828'
ht-degree: 1%

---

# Adobe Experience Manager(AEM) 구성 요소 - 기본 사항{#aem-components-the-basics}

새 구성 요소를 개발하기 시작하려면 해당 구성 요소의 구조 및 구성에 대한 기본 사항을 이해해야 합니다.

이 프로세스에는 이론을 읽고 표준 AEM 인스턴스에서 광범위한 구성 요소 구현을 살펴보는 작업이 포함됩니다. 이 후자의 접근 방식은 AEM이 새로운 표준, 최신, 터치 지원 UI로 전환되었지만 클래식 UI를 계속 지원한다는 점에서 약간 복잡합니다.

## 개요 {#overview}

이 섹션에서는 구성 요소를 개발할 때 필요한 세부 사항을 소개하는 주요 개념과 문제를 다룹니다.

### 계획 수립 {#planning}

구성 요소를 실제로 구성하거나 코딩하기 전에 다음 사항을 문의해야 합니다.

* 새 구성 요소를 사용하려면 정확히 어떤 작업이 필요합니까?
   * 명확한 사양은 개발, 테스트 및 인수의 모든 단계에 도움이 됩니다. 세부 사항은 시간이 지남에 따라 변경될 수 있지만 세부 사항은 업데이트할 수 있습니다(변경 사항도 문서화되어야 함).
* 구성 요소를 처음부터 만들어야 합니까? 또는 기존 구성 요소에서 기본 사항을 상속할 수 있습니까?
   * 시간을 낭비할 필요가 없다.
   * AEM에서 제공하는 메커니즘에는 재정의, 오버레이 및 [Sling 리소스 병합](/help/sites-developing/sling-resource-merger.md)을(를) 포함하여 다른 구성 요소 정의에서 세부 정보를 상속하고 확장할 수 있는 몇 가지 메커니즘이 있습니다.
* 콘텐츠를 선택하거나 조작하기 위해 구성 요소에 논리가 필요합니까?
   * 논리는 사용자 인터페이스 레이어와 별도로 유지되어야 합니다. HTL은 이러한 일이 발생하는지 확인할 수 있도록 설계되었습니다.
* 구성 요소에 CSS 서식이 필요합니까?
   * CSS 서식은 구성 요소 정의와 별도로 유지해야 합니다. 외부 CSS 파일을 통해 수정할 수 있도록 HTML 요소의 이름을 지정하는 규칙을 정의합니다.
* 어떤 보안 측면을 고려해야 합니까?
   * 자세한 내용은 [보안 검사 목록 - 개발 모범 사례](/help/sites-administering/security-checklist.md#development-best-practices)를 참조하세요.

### 터치 지원 및 클래식 UI {#touch-enabled-vs-classic-ui}

구성 요소 개발에 대한 진지한 논의를 시작하기 전에 작성자가 사용 중인 UI를 알고 있어야 합니다.

* **터치 사용 UI**
  [표준 사용자 인터페이스](/help/sites-developing/touch-ui-concepts.md)는 [Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui) 및 [Granite UI](/help/sites-developing/touch-ui-concepts.md#granite-ui)의 기본 기술을 사용하여 Adobe Experience Cloud에 대한 통합 사용자 경험을 기반으로 합니다.
* **클래식 UI**
AEM 6.4에서 더 이상 사용되지 않는 ExtJS 기술을 기반으로 한 사용자 인터페이스입니다.

자세한 내용은 [고객을 위한 UI 인터페이스 권장 사항](/help/sites-deploying/ui-recommendations.md)을 참조하십시오.

터치 지원 UI, 클래식 UI 또는 둘 다를 지원하도록 구성 요소를 구현할 수 있습니다. 표준 인스턴스를 보면 원래 클래식 UI나 터치 지원 UI 또는 둘 다에 맞게 디자인된 즉시 사용 가능한 구성 요소도 표시됩니다.

두 페이지의 기본 사항과 이를 인식하는 방법에 대해 설명합니다.

>[!NOTE]
>
>Adobe에서는 터치 지원 UI를 사용하여 최신 기술을 활용할 것을 권장합니다. [AEM 현대화 도구](modernization-tools.md)를 통해 마이그레이션을 더 쉽게 수행할 수 있습니다.

### 컨텐츠 논리 및 렌더링 마크업  {#content-logic-and-rendering-markup}

Adobe에서는 마크업 및 렌더링을 담당하는 코드를 구성 요소의 콘텐츠를 선택하는 데 사용되는 논리를 제어하는 코드와 별도로 유지하는 것이 좋습니다.

이 철학은 기본 비즈니스 논리를 정의하는 데 실제 프로그래밍 언어를 사용하도록 의도적으로 제한된 템플릿 언어인 [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html)에서 지원됩니다. 이 (선택 사항) 논리는 특정 명령을 사용하여 HTL에서 호출됩니다. 이 메커니즘은 주어진 뷰에 대해 호출되는 코드를 강조 표시하고, 필요한 경우 동일한 구성 요소의 다른 뷰에 대해 특정 논리를 허용합니다.

### HTL과 JSP {#htl-vs-jsp}

HTL은 AEM 6.0과 함께 도입된 HTML 템플릿 언어입니다.

이제 AEM에서 HTL이 권장 스크립팅 언어이므로 자체 구성 요소를 개발할 때 [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html)을 사용할지 JSP(Java™ Server Pages)를 사용할지 여부는 간단해야 합니다.

HTL과 JSP는 모두 클래식 및 터치 지원 UI 모두에 대한 구성 요소 개발에 사용할 수 있습니다. HTL은 터치 지원 UI용이고 JSP는 클래식 UI용이라고 가정하는 경향이 있을 수 있지만, 이는 잘못된 인식이며 타이밍으로 인한 더 많은 것입니다. 터치 지원 UI 및 HTL은 거의 동일한 기간에 AEM에 통합되었습니다. 이제 HTL이 권장 언어이므로 터치 지원 UI용 경향이 있는 새 구성 요소에 사용되고 있습니다.

>[!NOTE]
>
>대화 상자에 사용되는 Granite UI Foundation 양식 필드는 예외입니다. 이러한 경우에도 JSP를 사용해야 합니다.

### 자체 구성 요소 개발 {#developing-your-own-components}

적절한 UI에 대한 자체 구성 요소를 만들려면 (이 페이지를 읽은 후)를 참조하십시오.

* [터치 지원 UI용 AEM 구성 요소](/help/sites-developing/developing-components.md)
* [클래식 UI용 AEM 구성 요소](/help/sites-developing/developing-components-classic.md)

기존 구성 요소를 복사한 다음 원하는 대로 변경하는 것이 가장 빠른 시작 방법입니다. 자체 구성 요소를 만들고 단락 시스템에 추가하는 방법은 다음을 참조하십시오.

* [구성 요소 개발](/help/sites-developing/developing-components-samples.md)(터치 사용 UI에 중점)

### 구성 요소를 게시 인스턴스로 이동 {#moving-components-to-the-publish-instance}

콘텐츠를 렌더링하는 구성 요소는 콘텐츠와 동일한 AEM 인스턴스에 배포해야 합니다. 따라서 작성 인스턴스에서 페이지를 작성 및 렌더링하는 데 사용되는 모든 구성 요소를 게시 인스턴스에 배포해야 합니다. 배포되면 구성 요소를 활성화된 페이지를 렌더링하는 데 사용할 수 있습니다.

다음 도구를 사용하여 구성 요소를 게시 인스턴스로 이동합니다.

* [패키지 관리자를 사용하여](/help/sites-administering/package-manager.md) 구성 요소를 패키지에 추가하고 다른 AEM 인스턴스로 이동합니다.
* [트리 복제 활성화 도구를 사용하여](/help/sites-authoring/publishing-pages.md#manage-publication) 구성 요소를 복제하십시오.

>[!NOTE]
>
>이러한 메커니즘은 예를 들어 개발에서 테스트 인스턴스로 구성 요소를 다른 인스턴스 간에 전송하는 데에도 사용할 수 있습니다.

### 처음부터 알아야 할 구성 요소 {#components-to-be-aware-of-from-the-start}

* 페이지:

   * AEM에 *페이지* 구성 요소(`cq:Page`)가 있습니다.
   * 이는 콘텐츠 관리에 중요한 특정 유형의 리소스입니다.
      * 페이지는 웹 사이트의 콘텐츠가 들어 있는 웹 페이지에 해당합니다.

* 단락 시스템:

   * 단락 시스템은 단락 목록을 관리하기 때문에 웹 사이트의 주요 부분입니다. 실제 콘텐츠를 보관하는 개별 구성 요소를 보관하고 구성하는 데 사용됩니다.
   * 단락 시스템에서 단락을 작성, 이동, 복사 및 삭제할 수 있습니다.
   * 특정 단락 시스템 내에서 사용할 수 있는 구성 요소를 선택할 수도 있습니다.
   * 표준 인스턴스(예: `parsys`, ` [responsivegrid](/help/sites-authoring/responsive-layout.md)`) 내에서 다양한 단락 시스템을 사용할 수 있습니다.

## 구조 {#structure}

AEM 구성 요소의 구조는 강력하고 유연하며 주요 고려 사항은 다음과 같습니다.

* 리소스 유형
* 구성 요소 정의
* 구성 요소의 속성 및 하위 노드
* 대화 상자
* 디자인 대화 상자
* 구성 요소 가용성
* 구성 요소 및 구성 요소가 만드는 콘텐츠

### 리소스 유형 {#resource-type}

구조의 주요 요소는 리소스 유형입니다.

* 콘텐츠 구조가 의도를 선언합니다.
* 리소스 유형은 이를 구현합니다.

이는 시간이 지남에 따라 외모와 느낌이 변하는 경우에도 의도가 시간에 머물게 하는 것을 돕는 추상화이다.

### 구성 요소 정의 {#component-definition}

#### 구성 요소 기본 사항 {#component-basics}

컴포넌트의 정의는 다음과 같이 나눌 수 있습니다.

* AEM 구성 요소는 [Sling](https://sling.apache.org/documentation.html)을(를) 기반으로 합니다.
* AEM 구성 요소는 (일반적으로) 다음 아래에 있습니다.

   * HTL: `/libs/wcm/foundation/components`
   * JSP: `/libs/foundation/components`

* 프로젝트/사이트별 구성 요소는 (일반적으로) 아래에 있습니다.

   * `/apps/<myApp>/components`

* AEM 표준 구성 요소는 `cq:Component`(으)로 정의되어 있으며 다음과 같은 주요 요소를 가지고 있습니다.

   * jcr 속성:

     jcr 속성 목록입니다. 이러한 속성은 변수이며, 구성 요소 노드의 기본 구조, 해당 속성 및 하위 노드가 `cq:Component` 정의에 의해 정의되어 있지만 일부는 선택 사항입니다

   * 리소스:

     구성 요소에서 사용하는 정적 요소를 정의합니다.

   * 스크립트:

  구성 요소의 결과 인스턴스 동작을 구현하는 데 사용됩니다.

* **루트 노드**:

   * `<mycomponent> (cq:Component)` - 구성 요소의 계층 노드.

* **중요 속성**:

   * `jcr:title` - 구성 요소 제목. 예를 들어 구성 요소가 구성 요소 브라우저 또는 사이드 킥에 나열될 때 레이블로 사용됩니다.
   * `jcr:description` - 구성 요소에 대한 설명. 구성 요소 브라우저 또는 사이드 킥에서 마우스 오버 힌트로 사용할 수 있습니다.
   * 클래식 UI:

      * `icon.png` - 이 구성 요소의 아이콘입니다.
      * `thumbnail.png` - 이 구성 요소가 단락 시스템 내에 나열되면 표시되는 이미지

   * Touch UI

      * 자세한 내용은 [Touch UI의 구성 요소 아이콘](/help/sites-developing/components-basics.md#component-icon-in-touch-ui) 섹션을 참조하십시오.

* **중요한 하위 노드**:

   * `cq:editConfig (cq:EditConfig)` - 구성 요소의 편집 속성을 정의하고 구성 요소를 구성 요소 브라우저 또는 Sidekick에 표시할 수 있습니다.

     참고: 구성 요소에 대화 상자가 있으면 cq:editConfig가 없어도 구성 요소 브라우저 또는 Sidekick에 자동으로 표시됩니다.

   * `cq:childEditConfig (cq:EditConfig)` - 자체 `cq:editConfig`을(를) 정의하지 않는 하위 구성 요소에 대한 작성자 UI 측면을 제어합니다.
   * 터치 지원 UI:

      * `cq:dialog`( `nt:unstructured`) - 이 구성 요소에 대한 대화 상자. 사용자가 구성 요소를 구성 및/또는 콘텐츠를 편집할 수 있는 인터페이스를 정의합니다.
      * `cq:design_dialog`( `nt:unstructured`) - 이 구성 요소의 디자인 편집 중

   * 클래식 UI:

      * `dialog`( `cq:Dialog`) - 이 구성 요소에 대한 대화 상자. 사용자가 구성 요소를 구성하거나, 콘텐츠를 편집하거나, 둘 다 편집할 수 있는 인터페이스를 정의합니다.
      * `design_dialog`( `cq:Dialog`) - 이 구성 요소에 대한 디자인 편집 중

#### Touch UI의 구성 요소 아이콘 {#component-icon-in-touch-ui}

구성 요소의 아이콘 또는 약어는 개발자가 구성 요소를 만들 때 구성 요소의 JCR 속성을 통해 정의됩니다. 이러한 속성은 다음 순서로 평가되며 발견된 첫 번째 유효한 속성이 사용됩니다.

1. `cq:icon` - 구성 요소 브라우저에 표시할 [Coral UI 라이브러리](https://developer.adobe.com/experience-manager/reference-materials/6-5/coral-ui/coralui3/Coral.Icon.html)의 표준 아이콘을 가리키는 문자열 속성
   * Coral 아이콘의 HTML 속성 값을 사용합니다.
1. `abbreviation` - 구성 요소 브라우저에서 구성 요소 이름의 약어를 사용자 지정하는 문자열 속성
   * 약어는 두 문자로 제한해야 합니다.
   * 빈 문자열을 제공하면 `jcr:title` 속성의 처음 두 문자에서 약어가 만들어집니다.
      * 예: &quot;Image&quot;의 &quot;Im&quot;
      * 지역화된 제목은 약어를 작성하는 데 사용됩니다.
   * 구성 요소에 `abbreviation_commentI18n` 속성이 있는 경우에만 약어가 번역되며, 이 속성은 번역 힌트로 사용됩니다.
1. `cq:icon.png` 또는 `cq:icon.svg` - 구성 요소 브라우저에 표시되는 이 구성 요소의 아이콘
   * 20 x 20 픽셀은 표준 구성 요소의 아이콘 크기입니다.
      * 더 큰 아이콘은 크기가 줄어듭니다(클라이언트측).
   * 권장 색상은 rgb(112, 112, 112) > #707070입니다.
   * 표준 구성 요소 아이콘의 배경은 투명합니다.
   * `.png` 및 `.svg` 파일만 지원됩니다.
   * Eclipse 플러그인을 통해 파일 시스템에서 가져오는 경우 파일 이름을 `_cq_icon.png` 또는 `_cq_icon.svg`(으)로 이스케이프 처리해야 합니다.
   * `.png`이(가) 둘 다 있는 경우 `.svg`보다 우선합니다.

구성 요소에 위의 속성( `cq:icon`, `abbreviation`, `cq:icon.png` 또는 `cq:icon.svg`)이 없는 경우:

* 시스템은 `sling:resourceSuperType` 속성 다음에 있는 Super 구성 요소에서 동일한 속성을 검색합니다.
* 수퍼 구성 요소 수준에서 검색되지 않거나 빈 약어가 발견되면 현재 구성 요소의 `jcr:title` 속성 첫 글자로 약어를 작성합니다.

상위 구성 요소에서 아이콘 상속을 취소하려면 구성 요소에서 빈 `abbreviation` 속성을 설정하면 기본 동작으로 되돌아갑니다.

[구성 요소 콘솔](/help/sites-authoring/default-components-console.md#component-details)에 특정 구성 요소의 아이콘이 정의된 방법이 표시됩니다.

#### SVG 아이콘 예 {#svg-icon-example}

```xml
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "https://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
<svg version="1.1" id="Layer_1" xmlns="https://www.w3.org/2000/svg" xmlns:xlink="https://www.w3.org/1999/xlink" x="0px" y="0px"
     width="20px" height="20px" viewBox="0 0 20 20" enable-background="new 0 0 20 20" xml:space="preserve">
    <ellipse cx="5" cy="5" rx="3" ry="3" fill="#707070"/>
    <ellipse cx="15" cy="5" rx="4" ry="4" fill="#707070"/>
    <ellipse cx="5" cy="15" rx="5" ry="5" fill="#707070"/>
    <ellipse cx="15" cy="15" rx="4" ry="4" fill="#707070"/>
</svg>
```

### 구성 요소의 속성 및 하위 노드 {#properties-and-child-nodes-of-a-component}

구성 요소를 정의하는 데 필요한 노드/속성 중 다수는 두 UI에 공통되지만, 구성 요소가 두 환경에서 모두 작동할 수 있도록 차이는 독립적으로 유지됩니다.

구성 요소가 `cq:Component` 유형의 노드이며 다음 속성과 자식 노드가 있습니다.

<table>
 <tbody>
  <tr>
   <td><strong>이름 <br /> </strong></td>
   <td><strong>유형 <br /> </strong></td>
   <td><strong>설명 <br /> </strong></td>
  </tr>
  <tr>
   <td>.<br /> </td>
   <td><code>cq:Component</code></td>
   <td>현재 구성 요소입니다. 구성 요소가 <code>cq:Component</code>.<br /> 노드 유형입니다. </td>
  </tr>
  <tr>
   <td><code>componentGroup</code></td>
   <td><code>String</code></td>
   <td>구성 요소 브라우저(터치 지원 UI) 또는 Sidekick(클래식 UI)에서 구성 요소를 선택할 수 있는 그룹입니다.<br /> <code>.hidden</code> 값은 실제 단락 시스템과 같이 UI에서 선택할 수 없는 구성 요소에 사용됩니다.</td>
  </tr>
  <tr>
   <td><code>cq:isContainer</code></td>
   <td><code>Boolean</code></td>
   <td>구성 요소가 컨테이너 구성 요소이므로 단락 시스템과 같은 다른 구성 요소를 포함할 수 있는지 여부를 나타냅니다.</td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><code>cq:dialog</code></td>
   <td><code>nt:unstructured</code><br /> </td>
   <td>터치 사용 UI에 대한 편집 대화 상자 정의.</td>
  </tr>
  <tr>
   <td><code>dialog</code></td>
   <td><code>cq:Dialog</code></td>
   <td>클래식 UI에 대한 편집 대화 상자 정의.</td>
  </tr>
  <tr>
   <td><code>cq:design_dialog</code></td>
   <td><code>nt:unstructured</code></td>
   <td>터치 지원 UI에 대한 디자인 대화 상자의 정의.</td>
  </tr>
  <tr>
   <td><code>design_dialog</code></td>
   <td><code>cq:Dialog </code></td>
   <td>클래식 UI에 대한 디자인 대화 상자의 정의.<br /> </td>
  </tr>
  <tr>
   <td><code>dialogPath</code></td>
   <td><code>String</code></td>
   <td>구성 요소에 대화 노드가 없는 경우 대소문자를 다루는 대화 상자 경로입니다.<br /> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><code>cq:cellName</code></td>
   <td><code>String</code></td>
   <td>설정하면 이 속성은 셀 ID로 간주됩니다.<br /> </td>
  </tr>
  <tr>
   <td><code>cq:childEditConfig</code></td>
   <td><code>cq:EditConfig</code></td>
   <td>구성 요소가 컨테이너(예: 단락 시스템)인 경우 하위 노드의 편집 구성을 구동합니다.<br /> </td>
  </tr>
  <tr>
   <td><code>cq:editConfig</code></td>
   <td><code>cq:EditConfig</code></td>
   <td><a href="#edit-behavior">구성 요소의 구성 편집</a>.<br /> </td>
  </tr>
  <tr>
   <td><code>cq:htmlTag</code></td>
   <td><code>nt:unstructured </code></td>
   <td>주변 html 태그에 추가된 추가 태그 속성을 반환합니다. 자동으로 생성된 div에 속성을 추가할 수 있습니다.</td>
  </tr>
  <tr>
   <td><code>cq:noDecoration</code></td>
   <td><code>Boolean</code></td>
   <td>true인 경우 구성 요소는 자동으로 생성된 div 및 css 클래스로 렌더링되지 않습니다.<br /> </td>
  </tr>
  <tr>
   <td><code>cq:template</code></td>
   <td><code>nt:unstructured</code></td>
   <td>이 노드가 검색되면 구성 요소 브라우저 또는 Sidekick에서 구성 요소를 추가할 때 컨텐츠 템플릿으로 사용됩니다.</td>
  </tr>
  <tr>
   <td><code>cq:templatePath</code></td>
   <td><code>String</code></td>
   <td>구성 요소 브라우저 또는 Sidekick에서 구성 요소를 추가할 때 컨텐츠 템플릿으로 사용할 노드에 대한 경로입니다. 구성 요소 노드에 대한 상대 경로가 아닌 절대 경로여야 합니다.<br /> 다른 곳에서 이미 사용 가능한 콘텐츠를 다시 사용하지 않으려면 이 작업이 필요하지 않으며 <code>cq:template</code>이면 충분합니다(아래 참조).</td>
  </tr>
  <tr>
   <td><code>jcr:created</code></td>
   <td><code>Date</code></td>
   <td>구성 요소를 만든 날짜입니다.<br /> </td>
  </tr>
  <tr>
   <td><code>jcr:description</code></td>
   <td><code>String</code></td>
   <td>구성 요소에 대한 설명입니다.<br /> </td>
  </tr>
  <tr>
   <td><code>jcr:title</code></td>
   <td><code>String</code></td>
   <td>구성 요소의 제목입니다.<br /> </td>
  </tr>
  <tr>
   <td><code>sling:resourceSuperType</code></td>
   <td><code>String</code></td>
   <td>설정하면 구성 요소가 이 구성 요소에서 상속됩니다.<br /> </td>
  </tr>
  <tr>
   <td><code>virtual</code></td>
   <td><code>sling:Folder</code></td>
   <td>가상 구성 요소를 만들 수 있습니다. 예를 보려면 다음 위치에서 연락처 구성 요소를 확인하십시오.<br /> <code>/libs/foundation/components/profile/form/contact</code></td>
  </tr>
  <tr>
   <td><code>&lt;breadcrumb.jsp&gt;</code></td>
   <td><code>nt:file</code><br /> </td>
   <td>스크립트 파일.<br /> </td>
  </tr>
  <tr>
   <td><code>icon.png</code></td>
   <td><code>nt:file</code></td>
   <td>구성 요소의 아이콘이 Sidekick의 제목 옆에 나타납니다.<br /> </td>
  </tr>
  <tr>
   <td><code>thumbnail.png</code></td>
   <td><code>nt:file</code></td>
   <td>구성 요소를 Sidekick에서 제자리로 드래그하는 동안 표시되는 선택적 축소판입니다.<br /> </td>
  </tr>
 </tbody>
</table>

**Text** 구성 요소(두 버전 중 하나)를 보면 다음 요소가 표시됩니다.

* HTL( `/libs/wcm/foundation/components/text`)

  ![chlimage_1-241](assets/chlimage_1-241.png)

* JSP( `/libs/foundation/components/text`)

  ![screen_shot_2012-02-13at60457pm](assets/screen_shot_2012-02-13at60457pm.png)

관심 있는 속성은 다음과 같습니다.

* `jcr:title` - 구성 요소의 제목입니다. 구성 요소를 식별하는 데 사용할 수 있습니다. 예를 들어 구성 요소 브라우저 또는 사이드 킥의 구성 요소 목록에 표시됩니다.
* `jcr:description` - 구성 요소에 대한 설명. sidekick 내의 구성 요소 목록에서 마우스 오버 힌트로 사용할 수 있습니다.
* `sling:resourceSuperType`: 정의를 재정의하여 구성 요소를 확장할 때 상속 경로를 나타냅니다.

특히 관심 있는 하위 노드는 다음과 같습니다.

* `cq:editConfig`( `cq:EditConfig`) - 시각적 측면을 제어합니다. 예를 들어 막대 또는 위젯의 모양을 정의하거나 사용자 지정된 컨트롤을 추가할 수 있습니다
* `cq:childEditConfig`( `cq:EditConfig`) - 자체 정의가 없는 자식 구성 요소의 시각적 측면을 제어합니다.
* 터치 지원 UI:
   * `cq:dialog`( `nt:unstructured`) - 이 구성 요소의 콘텐츠를 편집하기 위한 대화 상자를 정의합니다.
   * `cq:design_dialog`( `nt:unstructured`) - 이 구성 요소의 디자인 편집 옵션을 지정합니다.
* 클래식 UI:
   * `dialog`( `cq:Dialog`) - 이 구성 요소의 콘텐츠를 편집하기 위한 대화 상자를 정의합니다(클래식 UI에만 해당).
   * `design_dialog`( `cq:Dialog`) - 이 구성 요소의 디자인 편집 옵션을 지정합니다.
   * `icon.png` - Sidekick에서 구성 요소의 아이콘으로 사용할 그래픽 파일
   * `thumbnail.png` - Sidekick에서 구성 요소를 드래그하는 동안 구성 요소의 썸네일로 사용할 그래픽 파일

### 대화 상자 {#dialogs}

대화 상자는 작성자가 구성 및 해당 구성 요소에 대한 입력 기능을 제공할 수 있는 인터페이스를 제공하므로 구성 요소의 핵심 요소입니다.

구성 요소의 복잡성에 따라 대화 상자를 짧게 하고 입력 필드를 정렬하려면 대화 상자에 하나 이상의 탭이 필요할 수 있습니다.

대화 상자 정의는 UI에만 해당됩니다.

>[!NOTE]
>
>* 호환성을 위해 터치 지원 UI에 대한 대화 상자가 정의되지 않은 경우 터치 지원 UI는 클래식 UI 대화 상자 정의를 사용할 수 있습니다.
>* 클래식 UI에 대해 정의된 대화 상자만 있는 구성 요소를 확장/변환하는 데 도움이 되는 [AEM 현대화 도구](/help/sites-developing/modernization-tools.md)도 제공됩니다.
>

* 터치 지원 UI
   * `cq:dialog`( `nt:unstructured`) 노드:
      * 이 구성 요소의 콘텐츠를 편집하기 위한 대화 상자 정의
      * 터치 지원 UI별
      * granite UI 구성 요소를 사용하여 정의됩니다
      * 표준 Sling 콘텐츠 구조로서 `sling:resourceType` 속성이 있습니다.
      * 속성 `helpPath`을(를) 사용하여 도움말 아이콘(`?` 아이콘)을 선택할 때 액세스하는 상황에 맞는 도움말 리소스(절대 또는 상대 경로)를 정의할 수 있습니다.
         * 기본 구성 요소의 경우 이 기능은 종종 설명서의 페이지를 참조합니다.
         * `helpPath`을(를) 지정하지 않으면 기본 URL(설명서 개요 페이지)이 표시됩니다.

  ![chlimage_1-242](assets/chlimage_1-242.png)

  대화 상자 내에서 개별 필드가 정의됩니다.

  ![screen_shot_2012-02-13at60937pm](assets/screen_shot_2012-02-13at60937pm.png)

* 클래식 UI
   * `dialog`( `cq:Dialog`) 노드
      * 이 구성 요소의 콘텐츠를 편집하기 위한 대화 상자 정의
      * 클래식 UI용
      * ExtJS 위젯을 사용하여 정의됩니다
      * ExtJS를 참조하는 `xtype` 속성이 있습니다.
      * **도움말** 단추를 선택할 때 액세스하는 상황에 맞는 도움말 리소스(절대 또는 상대 경로)를 정의하는 속성 `helpPath`이(가) 있을 수 있습니다.
         * 기본 구성 요소의 경우 이 기능은 종종 설명서의 페이지를 참조합니다.
         * `helpPath`을(를) 지정하지 않으면 기본 URL(설명서 개요 페이지)이 표시됩니다.

  ![chlimage_1-243](assets/chlimage_1-243.png)

  대화 상자 내에서 개별 필드가 정의됩니다.

  ![chlimage_1-244](assets/chlimage_1-244.png)

  클래식 대화 상자 내에서:

   * 텍스트 구성 요소에서와 같이 단일 탭을 제공하는 대화 상자를 `cq:Dialog`(으)로 만들거나, textimage 구성 요소에서와 같이 여러 탭이 필요한 경우 대화 상자를 `cq:TabPanel`(으)로 정의할 수 있습니다.
   * `cq:WidgetCollection`( `items`)은(는) 입력 필드( `cq:Widget`) 또는 추가 탭( `cq:Widget`)의 기준을 제공하는 데 사용됩니다. 이 계층은 확장할 수 있습니다.

### 디자인 대화 상자 {#design-dialogs}

디자인 대화 상자는 콘텐츠를 편집하고 구성하는 데 사용되는 대화 상자와 유사하지만, 작성자가 해당 구성 요소에 대한 디자인 세부 정보를 구성하고 제공할 수 있는 인터페이스를 제공합니다.

[디자인 대화 상자를 디자인 모드에서 사용할 수 있습니다](/help/sites-authoring/default-components-designmode.md). 모든 구성 요소에는 사용할 필요가 없지만 **제목** 및 **이미지**&#x200B;에는 모두 디자인 대화 상자가 있지만 **텍스트**&#x200B;에는 사용할 수 없습니다.

단락 시스템(예: parsys)의 디자인 대화 상자는 사용자가 페이지에서 다른 특정 구성 요소를 선택(구성 요소 브라우저 또는 사이드 킥)할 수 있도록 하는 특별한 경우입니다.

### 단락 시스템에 구성 요소 추가 {#adding-your-component-to-the-paragraph-system}

구성 요소를 정의한 후 사용할 수 있도록 해야 합니다. 구성 요소를 단락 시스템에서 사용할 수 있도록 하려면 다음 중 하나를 수행할 수 있습니다.

1. 페이지의 [디자인 모드](/help/sites-authoring/default-components-designmode.md)를 열고 필요한 구성 요소를 사용하도록 설정합니다.
1. 다음 아래에 있는 템플릿 정의의 `components` 속성에 필요한 구성 요소를 추가합니다.

   `/etc/designs/<*yourProject*>/jcr:content/<*yourTemplate*>/par`

   예를 들어 다음을 참조하십시오.

   `/etc/designs/geometrixx/jcr:content/contentpage/par`

   ![chlimage_1-245](assets/chlimage_1-245.png)

### 구성 요소 및 구성 요소가 만드는 콘텐츠 {#components-and-the-content-they-create}

페이지에서 **Title** 구성 요소의 인스턴스를 만들고 구성하는 경우: `<content-path>/Prototype.html`

* 터치 지원 UI

  ![chlimage_1-246](assets/chlimage_1-246.png)

* 클래식 UI

  ![screen_shot_2012-02-01at34257pm](assets/screen_shot_2012-02-01at34257pm.png)

그러면 저장소 내에 만들어진 컨텐츠의 구조를 볼 수 있습니다.

![screen_shot_2012-02-13at61405pm](assets/screen_shot_2012-02-13at61405pm.png)

특히 **제목**&#x200B;의 실제 텍스트를 보면 다음과 같습니다.

* 두 UI에 대한 정의에 `name`= `./jcr:title` 속성이 있습니다.

   * `/libs/foundation/components/title/cq:dialog/content/items/column/items/title`
   * `/libs/foundation/components/title/dialog/items/title`

* 콘텐츠 내에서 작성자의 콘텐츠를 포함하는 속성 `jcr:title`이(가) 생성됩니다.

정의된 속성은 개별 정의에 따라 다릅니다. 비록 그것들이 위보다 더 복잡할 수 있지만, 여전히 같은 기본 원칙을 따르고 있다.

## 구성 요소 계층 및 상속 {#component-hierarchy-and-inheritance}

AEM 내의 구성 요소는 세 가지 계층을 따릅니다.

* **리소스 유형 계층 구조**

  속성 `sling:resourceSuperType`을(를) 사용하여 구성 요소를 확장하는 데 사용됩니다. 이렇게 하면 구성 요소가 상속될 수 있습니다. 예를 들어 텍스트 구성 요소는 표준 구성 요소에서 다양한 속성을 상속합니다.

   * 스크립트(Sling으로 해결됨)
   * 대화 상자
   * 설명(썸네일 이미지 및 아이콘 포함)

* **컨테이너 계층**

  이 메서드는 하위 구성 요소에 대한 구성 설정을 채우는 데 사용되며 parsys 시나리오에서 가장 일반적으로 사용됩니다.

  예를 들어 편집 막대 단추, 컨트롤 세트 레이아웃(편집 막대, 롤오버), 대화 상자 레이아웃(인라인, 부동)에 대한 구성 설정을 상위 구성 요소에서 정의하고 하위 구성 요소로 전파할 수 있습니다.

  `cq:editConfig` 및 `cq:childEditConfig`의 구성 설정(편집 기능 관련)이 전파되었습니다.

* **계층 포함**

  이는 다음을 포함하는 순서에 따라 런타임에 적용됩니다.

  이 계층은 Designer에서 사용되며, 레이아웃 정보, css 정보 및 parsys의 사용 가능한 구성 요소를 포함하여 렌더링의 다양한 디자인 측면에 대한 기반 역할을 합니다.

## 비헤이비어 편집 {#edit-behavior}

이 섹션에서는 구성 요소의 편집 동작을 구성하는 방법을 설명합니다. 여기에는 구성 요소에 사용할 수 있는 작업, 즉석 편집기의 특성 및 구성 요소의 이벤트와 관련된 리스너와 같은 속성이 포함됩니다.

이 구성은 터치 지원 UI와 클래식 UI에 공통되지만, 특정 차이점이 있습니다.

구성 요소의 편집 동작은 구성 요소 노드(유형 `cq:Component`) 아래에 유형 `cq:EditConfig`의 `cq:editConfig` 노드를 추가하고 특정 속성 및 하위 노드를 추가하여 구성되었습니다. 다음 속성 및 하위 노드를 사용할 수 있습니다.

* [`cq:editConfig` 노드 속성](#configuring-with-cq-editconfig-properties):

   * `cq:actions`( `String array`): 구성 요소에서 수행할 수 있는 작업을 정의합니다.
   * `cq:layout`( `String`): 클래식 UI에서 구성 요소를 편집하는 방법을 정의합니다.
   * `cq:dialogMode`( `String`): 구성 요소 대화 상자를 클래식 UI에서 여는 방법을 정의합니다

      * 터치 지원 UI에서 대화 상자는 항상 데스크탑 모드에서 부동이며 모바일에서 전체 화면으로 자동으로 열립니다.

   * `cq:emptyText`( `String`): 시각적 컨텐츠가 없을 때 표시되는 텍스트를 정의합니다.
   * `cq:inherit`( `Boolean`): 누락된 값이 상속되는 구성 요소에서 상속되는지 여부를 정의합니다.
   * `dialogLayout`(문자열): 대화 상자를 여는 방법을 정의합니다.

* [`cq:editConfig`개의 하위 노드](#configuring-with-cq-editconfig-child-nodes):

   * `cq:dropTargets`(노드 유형 `nt:unstructured`): 콘텐츠 파인더의 에셋에서 삭제를 수락할 수 있는 삭제 대상 목록을 정의합니다.

      * 여러 놓기 대상은 클래식 UI에서만 사용할 수 있습니다.
      * 터치 활성화 UI에서는 단일 드롭 대상이 허용됩니다.

   * `cq:actionConfigs`(노드 유형 `nt:unstructured`): cq:actions 목록에 추가되는 새 작업 목록을 정의합니다.
   * `cq:formParameters`(노드 유형 `nt:unstructured`): 대화 상자 양식에 추가되는 추가 매개 변수를 정의합니다.
   * `cq:inplaceEditing`(노드 유형 `cq:InplaceEditingConfig`): 구성 요소에 대한 즉석 편집 구성을 정의합니다.
   * `cq:listeners`(노드 유형 `cq:EditListenersConfig`): 구성 요소에서 작업이 발생하기 전이나 후에 수행되는 작업을 정의합니다.

>[!NOTE]
>
>이 페이지에서 노드(속성 및 하위 노드)는 다음 예와 같이 XML로 표시됩니다.

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:actions="[edit]"
    cq:dialogMode="floating"
    cq:layout="editbar"
    jcr:primaryType="cq:EditConfig">
    <cq:listeners
        jcr:primaryType="cq:EditListenersConfig"
        afteredit="REFRESH_PAGE"/>
</jcr:root>
```

저장소에는 많은 기존 구성이 있습니다. 특정 속성이나 하위 노드를 쉽게 검색할 수 있습니다.

* `cq:editConfig` 노드의 속성(예: `cq:actions`)을 찾으려면 **CRXDE Lite**&#x200B;에서 쿼리 도구를 사용하고 다음 XPath 쿼리 문자열로 검색할 수 있습니다.

  `//element(cq:editConfig, cq:EditConfig)[@cq:actions]`

* 예를 들어 `cq:editConfig`의 자식 노드를 찾으려면 `cq:DropTargetConfig` 유형의 `cq:dropTargets`을(를) 검색하고** CRXDE Lite**에서 쿼리 도구를 사용하여 다음 XPath 쿼리 문자열로 검색할 수 있습니다.

  `//element(cq:dropTargets, cq:DropTargetConfig)`

### 구성 요소 자리 표시자 {#component-placeholders}

구성 요소는 구성 요소에 콘텐츠가 없는 경우에도 항상 작성자가 볼 수 있는 일부 HTML을 렌더링해야 합니다. 그렇지 않으면 편집기의 인터페이스에서 시각적으로 사라져 페이지와 편집기에서 기술적으로 표시되지만 보이지 않을 수 있습니다. 이러한 경우 작성자는 빈 구성 요소를 선택하고 상호 작용할 수 없습니다.

따라서 구성 요소는 페이지가 페이지 편집기에서 렌더링될 때(WCM 모드가 `edit` 또는 `preview`일 때) 표시되는 출력을 렌더링하지 않는 한 자리 표시자를 렌더링해야 합니다.
자리 표시자에 대한 일반적인 HTML 마크업은 다음과 같습니다.

```HTML
<div class="cq-placeholder" data-emptytext="Component Name"></div>
```

위의 자리 표시자 HTML을 렌더링하는 일반적인 HTL 스크립트는 다음과 같습니다.

```HTML
<div class="cq-placeholder" data-emptytext="${component.properties.jcr:title}"
     data-sly-test="${(wcmmode.edit || wcmmode.preview) && isEmpty}"></div>
```

앞의 예에서 `isEmpty`은(는) 구성 요소에 콘텐츠가 없고 작성자에게 보이지 않는 경우에만 true인 변수입니다.

Adobe에서는 반복을 방지하기 위해 구성 요소 구현자가 핵심 구성 요소에서 제공하는 것과 같은 [자리 표시자에 HTL 템플릿을 사용하는 것이 좋습니다.](https://github.com/adobe/aem-core-wcm-components/blob/master/content/src/content/jcr_root/apps/core/wcm/components/commons/v1/templates.html)

그런 다음 이전 링크에서 템플릿 사용은 다음 HTL 행을 통해 수행됩니다.

```HTML
<sly data-sly-use.template="core/wcm/components/commons/v1/templates.html"
     data-sly-call="${template.placeholder @ isEmpty=!model.text}"></sly>
```

앞의 예에서 `model.text`은(는) 콘텐츠에 콘텐츠가 있고 표시되는 경우에만 true인 변수입니다.

이 템플릿의 사용 예는 제목 구성 요소와 같은 핵심 구성 요소 [에서 볼 수 있습니다.](https://github.com/adobe/aem-core-wcm-components/blob/master/content/src/content/jcr_root/apps/core/wcm/components/title/v2/title/title.html#L27)

### cq:EditConfig 속성으로 구성 {#configuring-with-cq-editconfig-properties}

### cq:actions {#cq-actions}

`cq:actions` 속성(`String array`)은 구성 요소에서 수행할 수 있는 하나 이상의 작업을 정의합니다. 구성에 사용할 수 있는 값은 다음과 같습니다.

<table>
 <tbody>
  <tr>
   <td><strong>속성 값</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td><code>text:&lt;some text&gt;</code></td>
   <td>정적 텍스트 값 &lt;일부 텍스트&gt;<br />을(를) 표시합니다. 클래식 UI에만 표시됩니다. 터치 지원 UI는 상황에 맞는 메뉴에 작업을 표시하지 않으므로 적용할 수 없습니다.</td>
  </tr>
  <tr>
   <td>-</td>
   <td>스페이서를 추가합니다.<br />은(는) 클래식 UI에만 표시됩니다. 터치 지원 UI는 상황에 맞는 메뉴에 작업을 표시하지 않으므로 적용할 수 없습니다.</td>
  </tr>
  <tr>
   <td><code>edit</code></td>
   <td>구성 요소 편집을 위한 단추를 추가합니다.</td>
  </tr>
      <tr>
    <td><code>editannotate</code></td>
    <td>구성 요소를 편집하고 <a href="/help/sites-authoring/annotations.md">주석</a>을 허용하는 단추를 추가합니다.</td>
   </tr>
  <tr>
   <td><code>delete</code></td>
   <td>구성 요소를 삭제하는 단추를 추가합니다.</td>
  </tr>
  <tr>
   <td><code>insert</code></td>
   <td>현재 구성 요소 앞에 새 구성 요소를 삽입하는 단추를 추가합니다.</td>
  </tr>
  <tr>
   <td><code>copymove</code></td>
   <td>구성 요소를 복사하고 잘라내기 위한 단추를 추가합니다.</td>
  </tr>
 </tbody>
</table>

다음 구성은 구성 요소 편집 막대에 편집 버튼, 스페이서, 삭제 및 삽입 버튼을 추가합니다.

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:actions="[edit,-,delete,insert]"
    cq:layout="editbar"
    jcr:primaryType="cq:EditConfig"/>
```

다음 구성은 구성 요소 편집 막대에 &quot;기본 프레임워크에서 상속된 구성&quot; 텍스트를 추가합니다.

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:actions="[text:Inherited Configurations from Base Framework]"
    cq:layout="editbar"
    jcr:primaryType="cq:EditConfig"/>
```

### cq:layout (클래식 UI만 해당) {#cq-layout-classic-ui-only}

`cq:layout` 속성(`String`)은 클래식 UI에서 구성 요소를 편집할 수 있는 방법을 정의합니다. 다음 값을 사용할 수 있습니다.

<table>
 <tbody>
  <tr>
   <td><strong>속성 값</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td><code>rollover</code></td>
   <td>기본값. 구성 요소 에디션은 클릭 및/또는 상황에 맞는 메뉴를 통해 "마우스 오버"로 액세스할 수 있습니다.<br /> 고급 사용 시 해당 클라이언트측 개체는 <code>CQ.wcm.EditRollover</code>입니다.</td>
  </tr>
  <tr>
   <td><code>editbar</code></td>
   <td>구성 요소 버전은 도구 모음을 통해 액세스할 수 있습니다.<br /> 고급 사용 시 해당 클라이언트측 개체는 <code>CQ.wcm.EditBar</code>입니다.</td>
  </tr>
  <tr>
   <td><code>auto</code></td>
   <td>선택은 클라이언트측 코드에 맡깁니다.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>터치 사용 UI에는 롤오버 및 편집 막대의 개념을 적용할 수 없습니다.

다음 구성은 구성 요소 편집 막대에 편집 단추를 추가합니다.

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:actions="[edit]"
    cq:layout="editbar"
    jcr:primaryType="cq:EditConfig">
</jcr:root>
```

### cq:dialogMode(클래식 UI만 해당) {#cq-dialogmode-classic-ui-only}

구성 요소를 편집 대화 상자에 연결할 수 있습니다. `cq:dialogMode` 속성(`String`)은 구성 요소 대화 상자를 클래식 UI에서 여는 방법을 정의합니다. 다음 값을 사용할 수 있습니다.

<table>
 <tbody>
  <tr>
   <td><strong>속성 값</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td><code>floating</code></td>
   <td>대화 상자가 부동입니다.<br /> </td>
  </tr>
  <tr>
   <td><code>inline</code></td>
   <td>(기본값). 대화 상자가 구성 요소 위에 고정되었습니다.<br /> </td>
  </tr>
  <tr>
   <td><code>auto</code></td>
   <td>구성 요소 너비가 클라이언트측 <code>CQ.themes.wcm.EditBase.INLINE_MINIMUM_WIDTH</code> 값보다 작으면 대화 상자가 부동이고, 그렇지 않으면 인라인입니다.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>터치 지원 UI에서 대화 상자는 항상 데스크탑 모드에서 부동이며 모바일에서 전체 화면으로 자동으로 열립니다.

다음 구성은 편집 단추가 있는 편집 막대 및 부동 대화 상자를 정의합니다.

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:actions="[edit]"
    cq:dialogMode="floating"
    cq:layout="editbar"
    jcr:primaryType="cq:EditConfig">
</jcr:root>
```

### cq:emptyText {#cq-emptytext}

`cq:emptyText` 속성(`String`)은 시각적 컨텐츠가 없을 때 표시되는 텍스트를 정의합니다. 기본값은 `Drag components or assets here`입니다.

### cq:inherit {#cq-inherit}

`cq:inherit` 속성(`boolean`)은 누락된 값이 상속되는 구성 요소에서 상속되는지 여부를 정의합니다. 기본값은 `false`입니다.

### 대화 상자 레이아웃 {#dialoglayout}

`dialogLayout` 속성은 기본적으로 대화 상자가 열리는 방법을 정의합니다.

* 값이 `fullscreen`이면 대화 상자가 전체 화면으로 열립니다.
* 속성이 비어 있거나 비어 있으면 대화 상자가 정상적으로 열립니다.
* 사용자는 대화 상자 내에서 항상 전체 화면 모드를 전환할 수 있습니다.
* 클래식 UI에는 적용되지 않습니다.

### cq:EditConfig 하위 노드로 구성 {#configuring-with-cq-editconfig-child-nodes}

### cq:dropTargets {#cq-droptargets}

`cq:dropTargets` 노드(노드 유형 `nt:unstructured`)는 콘텐츠 파인더에서 드래그한 에셋에서 드롭할 수 있는 드롭 대상 목록을 정의합니다. `cq:DropTargetConfig` 유형의 노드 컬렉션 역할을 합니다.

>[!NOTE]
>
>여러 놓기 대상은 클래식 UI에서만 사용할 수 있습니다.
>
>터치 지원 UI에서는 첫 번째 타겟만 사용됩니다.

`cq:DropTargetConfig` 형식의 각 자식 노드는 구성 요소에서 드롭 대상을 정의합니다. 노드 이름은 다음과 같이 JSP에서 유효 드롭 대상인 DOM 요소에 지정된 CSS 클래스 이름을 생성하기 위해 사용해야 하므로 중요합니다.

```
<drop target css class> = <drag and drop prefix> +
 <node name of the drop target in the edit configuration>
```

`<drag and drop prefix>`은(는) Java™ 속성으로 정의됩니다.

`com.day.cq.wcm.api.components.DropTarget.CSS_CLASS_PREFIX`

예를 들어 클래스 이름은 다운로드 구성 요소의 JSP에서 다음과 같이 정의됩니다
( `/libs/foundation/components/download/download.jsp`). 여기서 `file`은(는) 다운로드 구성 요소의 편집 구성에 있는 드롭 대상의 노드 이름입니다.

`String ddClassName = DropTarget.CSS_CLASS_PREFIX + "file";`

`cq:DropTargetConfig` 형식의 노드에는 다음 속성이 있어야 합니다.

<table>
 <tbody>
  <tr>
   <td><strong>속성 이름</strong></td>
   <td><strong>속성 값<br /> </strong></td>
  </tr>
  <tr>
   <td><code>accept</code></td>
   <td>드롭이 허용되는지 확인하기 위해 자산 MIME 유형에 적용되는 Regex입니다.</td>
  </tr>
  <tr>
   <td><code>groups</code></td>
   <td>드롭 대상 그룹의 배열입니다. 각 그룹은 콘텐츠 파인더 확장에 정의되어 있고 에셋에 첨부된 그룹 유형과 일치해야 합니다.</td>
  </tr>
  <tr>
   <td><code>propertyName</code></td>
   <td>유효한 삭제 후 업데이트될 속성의 이름입니다.</td>
  </tr>
 </tbody>
</table>

다음 구성은 다운로드 구성 요소에서 가져온 것입니다. `media` 그룹의 모든 에셋(mime 유형은 임의의 문자열일 수 있음)을 콘텐츠 파인더에서 구성 요소로 끌어 놓을 수 있습니다. 삭제 후 구성 요소 속성 `fileReference`이(가) 업데이트되고 있습니다.

```
    <cq:dropTargets jcr:primaryType="nt:unstructured">
        <file
            jcr:primaryType="cq:DropTargetConfig"
            accept="[.*]"
            groups="[media]"
            propertyName="./fileReference"/>
    </cq:dropTargets>
```

### cq:actionConfigs(클래식 UI만 해당) {#cq-actionconfigs-classic-ui-only}

`cq:actionConfigs` 노드(노드 유형 `nt:unstructured`)는 `cq:actions` 속성으로 정의된 목록에 추가되는 새 작업의 목록을 정의합니다. `cq:actionConfigs`의 각 자식 노드는 위젯을 정의하여 새 작업을 정의합니다.

다음 샘플 구성은 새 버튼(클래식 UI에 대해 구분 기호 사용)을 정의합니다.

* xtype `tbseparator`(으)로 정의된 구분 기호

   * 클래식 UI에서만 사용됩니다.
   * xtype이 무시되므로 터치 사용 UI에서 이 정의는 무시됩니다. (작업 도구 모음이 터치 사용 UI에서 다르게 구성되므로 구분 기호는 필요하지 않음).

* 처리기 함수 `CQ_collab_forum_openCollabAdmin()`을(를) 실행하는 **댓글 관리** 단추.

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    cq:actions="[EDIT,COPYMOVE,DELETE,INSERT]"
    jcr:primaryType="cq:EditConfig">
    <cq:actionConfigs jcr:primaryType="nt:unstructured">
        <separator0
            jcr:primaryType="nt:unstructured"
            xtype="tbseparator"/>
        <manage
            jcr:primaryType="nt:unstructured"
            handler="function(){CQ_collab_forum_openCollabAdmin();}"
            text="Manage comments"/>
    </cq:actionConfigs>
</jcr:root>
```

>[!NOTE]
>
>터치 사용 UI의 예로 [구성 요소 도구 모음에 새 작업 추가](/help/sites-developing/customizing-page-authoring-touch.md#add-new-action-to-a-component-toolbar)를 참조하십시오.

### cq:formParameters {#cq-formparameters}

`cq:formParameters` 노드(노드 유형 `nt:unstructured`)는 대화 상자 양식에 추가되는 추가 매개 변수를 정의합니다. 각 속성은 양식 매개 변수에 매핑됩니다.

다음 구성은 값이 `photos/primary`인 `name` 매개 변수를 대화 상자 양식에 추가합니다.

```
    <cq:formParameters
        jcr:primaryType="nt:unstructured"
        name="photos/primary"/>
```

### cq:inplaceEditing {#cq-inplaceediting}

`cq:inplaceEditing` 노드(노드 유형 `cq:InplaceEditingConfig`)가 구성 요소에 대한 즉석 편집 구성을 정의합니다. 다음과 같은 속성을 가질 수 있습니다.

<table>
 <tbody>
  <tr>
   <td><strong>속성 이름</strong></td>
   <td><strong>속성 값<br /> </strong></td>
  </tr>
  <tr>
   <td><code>active</code></td>
   <td>(<code>boolean</code>) True로 설정하면 구성 요소를 즉석에서 편집할 수 있습니다.</td>
  </tr>
  <tr>
   <td><code>configPath</code></td>
   <td>(<code>String</code>) 편집기 구성의 경로입니다. 구성은 구성 노드에서 지정할 수 있습니다.</td>
  </tr>
  <tr>
   <td><code>editorType</code></td>
   <td><p>(<code>String</code>) 편집기 유형. 사용 가능한 유형은 다음과 같습니다.</p>
    <ul>
     <li>일반 텍스트: HTML 이외의 콘텐츠에 사용됩니다.<br /> </li>
     <li>title: 는 편집을 시작하기 전에 그래픽 제목을 일반 텍스트로 변환하는 향상된 일반 텍스트 편집기입니다. Geometrixx 제목 구성 요소에서 사용됩니다.<br /> </li>
     <li>텍스트: HTML 콘텐츠에 사용할 텍스트(리치 텍스트 편집기 사용).<br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

다음 구성은 구성 요소를 즉석에서 편집할 수 있도록 하고 `plaintext`을(를) 편집기 유형으로 정의합니다.

```
    <cq:inplaceEditing
        jcr:primaryType="cq:InplaceEditingConfig"
        active="{Boolean}true"
        editorType="plaintext"/>
```

### cq:listeners {#cq-listeners}

`cq:listeners` 노드(노드 유형 `cq:EditListenersConfig`)는 구성 요소에서 작업 전이나 후에 수행되는 작업을 정의합니다. 다음 표는 가능한 속성을 정의합니다.

<table>
 <tbody>
  <tr>
   <td><strong>속성 이름</strong></td>
   <td><strong>속성 값<br /> </strong></td>
   <td><p><strong>기본 값</strong></p> <p>(클래식 UI만 해당)</p> </td>
  </tr>
  <tr>
   <td><code>beforedelete</code></td>
   <td>구성 요소를 제거하기 전에 처리기가 트리거됩니다.<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforeedit</code></td>
   <td>구성 요소를 편집하기 전에 처리기가 트리거됩니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforecopy</code></td>
   <td>구성 요소가 복사되기 전에 처리기가 트리거됩니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforemove</code></td>
   <td>구성 요소를 이동하기 전에 처리기가 트리거됩니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforeinsert</code></td>
   <td>구성 요소를 삽입하기 전에 처리기가 트리거됩니다.<br /> 터치 사용 UI에 대해서만 작동합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforechildinsert</code></td>
   <td>처리기는 구성 요소가 다른 구성 요소 내부에 삽입되기 전에 트리거됩니다(컨테이너만 해당).</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>afterdelete</code></td>
   <td>구성 요소가 제거되면 핸들러가 트리거됩니다.</td>
   <td><code>REFRESH_SELF</code></td>
  </tr>
  <tr>
   <td><code>afteredit</code></td>
   <td>처리기는 구성 요소를 편집한 후 트리거됩니다.</td>
   <td><code>REFRESH_SELF</code></td>
  </tr>
  <tr>
   <td><code>aftercopy</code></td>
   <td>처리기는 구성 요소가 복사된 후 트리거됩니다.</td>
   <td><code>REFRESH_SELF</code></td>
  </tr>
  <tr>
   <td><code>afterinsert</code></td>
   <td>처리기는 구성 요소가 삽입된 후 트리거됩니다.</td>
   <td><code>REFRESH_INSERTED</code></td>
  </tr>
  <tr>
   <td><code>aftermove</code></td>
   <td>처리기는 구성 요소를 이동한 후 트리거됩니다.</td>
   <td><code>REFRESH_SELFMOVED</code></td>
  </tr>
  <tr>
   <td><code>afterchildinsert</code></td>
   <td>처리기는 구성 요소가 다른 구성 요소 내부에 삽입되면 트리거됩니다(컨테이너만 해당).</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>`REFRESH_INSERTED` 및 `REFRESH_SELFMOVED` 처리기는 클래식 UI에서만 사용할 수 있습니다.

>[!NOTE]
>
>리스너에 대한 기본값은 클래식 UI에서만 설정됩니다.

>[!NOTE]
>
>중첩된 구성 요소가 있는 경우 `cq:listeners` 노드에서 속성으로 정의된 작업에 특정 제한 사항이 있습니다.
>
>* 중첩된 구성 요소의 경우 *must* 속성의 값은 `REFRESH_PAGE`입니다. >
>  * `aftermove`
>  * `aftercopy`

이벤트 처리기는 사용자 지정 구현으로 구현할 수 있습니다. 예를 들어, `project.customerAction`은(는) 정적 메서드입니다.

`afteredit = "project.customerAction"`

다음 예제는 `REFRESH_INSERTED` 구성과 같습니다.

`afterinsert="function(path, definition) { this.refreshCreated(path, definition); }"`

>[!NOTE]
>
>클래식 UI의 경우, 처리기에서 사용할 수 있는 매개 변수를 보려면 [`CQ.wcm.EditBar`](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.EditBar) 및 [`CQ.wcm.EditRollover`](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.EditRollover) 위젯 설명서의 `before<action>` 및 `after<action>` 이벤트 섹션을 참조하십시오.

다음 구성을 사용하면 구성 요소가 삭제, 편집, 삽입 또는 이동된 후 페이지가 새로 고쳐집니다.

```
    <cq:listeners
        jcr:primaryType="cq:EditListenersConfig"
        afterdelete="REFRESH_PAGE"
        afteredit="REFRESH_PAGE"
        afterinsert="REFRESH_PAGE"
        afterMove="REFRESH_PAGE"/>
```
