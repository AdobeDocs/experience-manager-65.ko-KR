---
title: AEM 터치 지원 UI의 개념
seo-title: AEM 터치 지원 UI의 개념
description: AEM 5.6 Adobe에서 작성 환경에 대한 반응형 디자인을 갖는 새로운 터치에 적합한 UI를 도입했습니다.
seo-description: AEM 5.6 Adobe에서 작성 환경에 대한 반응형 디자인을 갖는 새로운 터치에 적합한 UI를 도입했습니다.
uuid: 401c5a65-6ddc-4942-ab8e-395016f9c629
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: df3aaed1-97b5-4a4a-af74-cb887462475b
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5
workflow-type: tm+mt
source-wordcount: '2197'
ht-degree: 2%

---


# AEM 터치 지원 UI의 개념{#concepts-of-the-aem-touch-enabled-ui}

AEM은 터치 및 데스크톱 장치에서 모두 작동하도록 설계된 작성 환경을 위해 [반응형 디자인](/help/sites-authoring/responsive-layout.md)이(가) 있는 터치 지원 UI를 제공합니다.

>[!NOTE]
>
>터치를 지원하는 UI는 AEM의 표준 UI입니다. 클래식 UI는 AEM 6.4에서 더 이상 사용되지 않습니다.

터치 지원 UI에는 다음이 포함됩니다.

* 다음과 같은 패키지 헤더입니다.
   * 로고를 표시합니다.
   * 전역 탐색에 대한 링크를 제공합니다.
   * 다른 일반 작업에 대한 링크를 제공합니다.검색, 도움말, Marketing Cloud 솔루션, 알림 및 사용자 설정과 같은 기능을 사용할 수 있습니다.
* 필요한 경우 표시되고 가이드할 수 있는 왼쪽 레일(표시):
   * 타임라인
   * 참조
   * 필터
* 상황에 따라 달라지며 표시할 수 있는 탐색 헤더입니다.
   * 현재 사용 중인 콘솔 및/또는 해당 콘솔 내의 위치를 나타냅니다.
   * 왼쪽 레일 선택
   * 탐색 표시
   * 적절한 **만들기** 작업에 액세스
   * 선택 영역 보기
* 다음과 같은 컨텐츠 영역
   * 컨텐츠 항목(페이지, 자산, 포럼 게시물 등)을 나열합니다.
   * 요청대로 서식 지정(예: 열, 카드 또는 목록) 가능
   * 반응형 디자인을 사용합니다(장치 및/또는 창 크기에 따라 디스플레이의 크기가 자동으로 조정됨).
   * 무한 스크롤을 사용합니다(더 이상 페이지 매김이 없고 모든 항목이 한 창에 나열됨).

![chlimage_1-79](assets/chlimage_1-79.png)

>[!NOTE]
>
>거의 모든 AEM 기능을 터치 지원 UI로 이식했습니다. 그러나 일부 제한된 경우에는 기능이 클래식 UI로 되돌려집니다. 자세한 내용은 [터치 UI 기능 상태](/help/release-notes/touch-ui-features-status.md)를 참조하십시오.

터치 지원 UI는 여러 제품에서 사용자 경험을 일관되게 제공하기 위해 Adobe에 의해 설계되었습니다. 이것은 다음을 기반으로 합니다.

* **CUI** (Coral UI)가 터치 지원 UI에 대한 Adobe 시각적 스타일 구현 Coral UI는 UI 시각적 스타일을 채택하는 데 필요한 모든 제품/프로젝트/웹 애플리케이션을 제공합니다.
* **Granite** UI구성 요소는 Coral UI로 빌드됩니다.

터치 지원 UI의 기본 원칙은 다음과 같습니다.

* 모바일 퍼스트(데스크탑을 고려한 솔루션)
* 반응형 디자인
* 컨텍스트 관련 디스플레이
* 재사용 가능
* 포함된 참조 설명서 포함
* 포함된 테스트 포함
* 이러한 원칙이 모든 요소 및 구성 요소에 적용되도록 하는 상향식 설계

터치 지원 UI 구조에 대한 자세한 개요는 AEM 터치 지원 UI의 [구조](/help/sites-developing/touch-ui-structure.md) 문서를 참조하십시오.

## AEM 기술 스택 {#aem-technology-stack}

AEM은 Granite platform을 기본으로 사용하고 Granite 플랫폼에는 Java Content Repository가 포함됩니다.

![chlimage_1-80](assets/chlimage_1-80.png)

## Granite {#granite}

Granite는 Adobe의 Open Web 스택으로, 다음을 비롯한 다양한 구성 요소를 제공합니다.

* 응용 프로그램 실행 프로그램
* 모든 것이 배포되는 OSGi 프레임워크
* 빌드 응용 프로그램을 지원하기 위한 다양한 OSGi 무료 서비스
* 다양한 로깅 API를 제공하는 포괄적인 로깅 프레임워크
* JCR API 사양의 CRX 저장소 구현
* Apache Sling Web Framework
* 현재 CRX 제품의 추가 부분

>[!NOTE]
>
>Granite는 Adobe 내에서 개방형 개발 프로젝트로 실행됩니다.코드, 토론 및 문제에 대한 기여도는 전체 회사에서 이루어집니다.
>
>그러나 Granite는 오픈 소스 프로젝트가 아닌 **입니다.** 이것은 몇몇 오픈 소스 프로젝트(특히 아파치 슬링, 펠릭스, 잭래빗, 루센)를 기반으로 하고 있지만, Adobe은 대중이 무엇이고 내부에 무엇이 있는지 사이의 명확한 선을 그립니다.

## Granite UI {#granite-ui}

Granite 엔지니어링 플랫폼도 기본적인 UI 프레임워크를 제공합니다. 이것의 주요 목표는 다음과 같습니다.

* 세부적인 UI 위젯 제공
* UI 개념을 구현하고 모범 사례(긴 목록 렌더링, 목록 필터링, 개체 CRUD, CUD 마법사...)를 보여 줍니다.
* 확장 가능한 플러그인 기반의 관리 UI 제공

다음은 요구 사항을 준수합니다.

* &quot;모바일 퍼스트&quot; 존중
* 확장 가능
* 간편한 재정의

![chlimage_1-81](assets/chlimage_1-81.png)
GraniteUI.pdf

[파일 ](assets/graniteui.pdf)
가져오기Granite UI:

* Sling의 RESTful 아키텍처 사용
* 컨텐츠 중심의 웹 애플리케이션 구축을 위한 구성 요소 라이브러리 구현
* 세부 UI 위젯 제공
* 기본 표준 UI 제공
* 확장 가능 여부
* 모바일 디바이스와 데스크탑 디바이스 모두를 위해 설계되었습니다(모바일 우선 고려).
* 모든 Granite 기반 플랫폼/제품/프로젝트에서 사용할 수 있습니다.eg AEM

![chlimage_1-82](assets/chlimage_1-82.png)

* [Granite UI Foundation ](#granite-ui-foundation-components)
Components다른 라이브러리에서 이 기초 구성 요소 라이브러리를 사용하거나 확장할 수 있습니다.
* [Granite UI 관리 구성 요소](#granite-ui-administration-components)

### 클라이언트측과 서버측 {#client-side-vs-server-side} 비교

Granite UI의 클라이언트-서버 통신은 개체가 아니라 하이퍼텍스트로 이루어지므로 클라이언트가 비즈니스 로직을 이해할 필요가 없습니다

* 서버는 의미 데이터를 사용하여 HTML을 풍부하게 합니다.
* 클라이언트는 하이퍼미디어로 하이퍼텍스트를 풍부하게 합니다(상호 작용).

![chlimage_1-83](assets/chlimage_1-83.png)

#### 클라이언트측 {#client-side}

이는 작성자가 인터랙티브한 웹 앱을 빌드할 의도를 표현할 수 있도록 제공된 HTML 단어 확장을 사용합니다. 이 방법은 [WAI-ARIA](https://www.w3.org/TR/wai-aria/) 및 [microformats](https://microformats.org/)와 비슷한 접근 방식입니다.

주로 JS 및 CSS 코드로 해석되고 클라이언트 쪽에서 실행되는 인터랙션 패턴(예: 비동기 방식의 양식 제출) 컬렉션으로 구성됩니다. 클라이언트측의 역할은 인터랙티브한 기능을 위해 마크업(서버에서 제공하는 하이퍼미디어로 제공)을 향상시키는 것입니다.

클라이언트측은 모든 서버 기술과 독립적입니다. 서버가 적절한 마크업을 제공하는 한 클라이언트측은 해당 역할을 수행할 수 있습니다.

현재 JS 및 CSS 코드는 카테고리 아래의 Granite [clientlibs](/help/sites-developing/clientlibs.md)로 제공됩니다.

`granite.ui.foundation and granite.ui.foundation.admin`

이러한 내용은 컨텐츠 패키지의 일부로 제공됩니다.

`granite.ui.content`

#### 서버측 {#server-side}

이는 작성자가 웹 앱을 빨리 *compose*&#x200B;할 수 있도록 하는 sling 구성 요소 모음을 통해 이루어집니다. 개발자는 구성 요소를 개발하고, 작성자는 구성 요소를 웹 앱으로 취합합니다. 서버측의 역할은 하이퍼미디어(markup)를 클라이언트에 제공하는 것입니다.

현재 구성 요소는 Granite repository at:

`/libs/granite/ui/components/foundation`

이것은 컨텐츠 패키지의 일부로 제공됩니다.

`granite.ui.content`

### 클래식 UI {#differences-with-the-classic-ui} 차이

Granite UI와 ExtJS(클래식 UI에 사용됨)의 차이도 다음과 같습니다.

<table>
 <tbody>
  <tr>
   <td><strong>ExtJS</strong></td>
   <td><strong>Granite UI</strong></td>
  </tr>
  <tr>
   <td>원격 프로시저 호출<br /> </td>
   <td>상태 전환</td>
  </tr>
  <tr>
   <td>데이터 전송 개체</td>
   <td>Hypermedia</td>
  </tr>
  <tr>
   <td>클라이언트, 서버 내부 파악</td>
   <td>클라이언트가 내부 정보를 모릅니다.</td>
  </tr>
  <tr>
   <td>"Fat client"</td>
   <td>"씬 클라이언트"</td>
  </tr>
  <tr>
   <td>전문 클라이언트 라이브러리</td>
   <td>범용 클라이언트 라이브러리</td>
  </tr>
 </tbody>
</table>

### Granite UI Foundation 구성 요소 {#granite-ui-foundation-components}

[Granite UI 기본 구성 요소](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)는 모든 UI를 작성하는 데 필요한 기본 구성 요소를 제공합니다. 여기에는 다음이 포함됩니다.

* 단추
* 하이퍼링크
* 사용자 아바타

기본 구성 요소는 다음과 같습니다.

`/libs/granite/ui/components/foundation`

이 라이브러리에는 각 Coral 요소에 대한 Granite UI 구성 요소가 포함되어 있습니다. 구성 요소는 저장소에 구성이 있는 컨텐츠 기반입니다. 따라서 HTML 마크업을 수동으로 작성하지 않고도 Granite UI 애플리케이션을 구성할 수 있습니다.

목적:

* HTML 요소에 대한 구성 요소 모델
* 구성 요소 구성
* 자동 유닛 및 기능 테스트

구현:

* 저장소 기반 구성 및 구성
* Granite platform에서 제공하는 테스트 시설 활용
* JSP 템플릿 설정

이 기본 구성 요소 라이브러리는 다른 라이브러리에서 사용하거나 확장할 수 있습니다.

### ExtJS 및 해당 Granite UI 구성 요소 {#extjs-and-corresponding-granite-ui-components}

Granite UI를 사용하도록 ExtJS 코드를 업그레이드할 때 다음 목록은 동일한 Granite UI 리소스 유형을 갖는 ExtJS xtype 및 노드 유형에 대한 간편한 개요를 제공합니다.

| **ExtJS xtype** | **Granite UI 리소스 유형** |
|---|---|
| `button` | `granite/ui/components/foundation/form/button` |
| `checkbox` | `granite/ui/components/foundation/form/checkbox` |
| `componentstyles` | `cq/gui/components/authoring/dialog/componentstyles` |
| `cqinclude` | `granite/ui/components/foundation/include` |
| `datetime` | `granite/ui/components/foundation/form/datepicker` |
| `dialogfieldset` | `granite/ui/components/foundation/form/fieldset` |
| `hidden` | `granite/ui/components/foundation/form/hidden` |
| `html5smartfile, html5smartimage` | `granite/ui/components/foundation/form/fileupload` |
| `multifield` | `granite/ui/components/foundation/form/multifield` |
| `numberfield` | `granite/ui/components/foundation/form/numberfield` |
| `pathfield, paragraphreference` | `granite/ui/components/foundation/form/pathbrowser` |
| `selection` | `granite/ui/components/foundation/form/select` |
| `sizefield` | `cq/gui/components/authoring/dialog/sizefield` |
| `tags` | `granite/ui/components/foundation/form/autocomplete``cq/gui/components/common/datasources/tags` |
| `textarea` | `granite/ui/components/foundation/form/textarea` |
| `textfield` | `granite/ui/components/foundation/form/textfield` |

| **노드 유형** | **Granite UI 리소스 유형** |
|---|---|
| `cq:WidgetCollection` | `granite/ui/components/foundation/container` |
| `cq:TabPanel` | `granite/ui/components/foundation/container``granite/ui/components/foundation/layouts/tabs` |
| `cq:panel` | `granite/ui/components/foundation/container` |

### Granite UI 관리 구성 요소 {#granite-ui-administration-components}

모든 관리 응용 프로그램이 구현할 수 있는 일반적인 빌드 블록을 제공하기 위해 기본 구성 요소에 대한 [Granite UI 관리 구성 요소](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html) 빌드가 빌드됩니다. 여기에는 다음이 포함됩니다.

* 전역 탐색 막대
* 레일(뼈대)
* 검색 패널

목적:

* 관리 애플리케이션을 위한 일관된 모양 및 느낌
* 관리 애플리케이션을 위한 Rad

구현:

* 기본 구성 요소를 사용하여 사전 정의된 구성 요소
* 구성 요소를 사용자 정의할 수 있습니다.

## Coral UI {#coral-ui}

CoralUI.pdf

[Get ](assets/coralui.pdf)
FileCoral UI(CUI)는 터치 지원 UI에 대한 Adobe의 시각적 스타일 구현으로, 여러 제품에서 사용자 경험을 일관되게 제공하도록 설계되었습니다. Coral UI는 작성 환경에서 사용되는 시각적 스타일을 적용하는 데 필요한 모든 것을 제공합니다.

>[!CAUTION]
>
>Coral UI는 AEM 고객이 라이선스가 부여된 제품 사용 범위 내에서 애플리케이션 및 웹 인터페이스를 구축할 수 있도록 제공되는 UI 라이브러리입니다.
>
>Coral UI는 다음과 같은 경우에만 사용할 수 있습니다.
>
>
>* AEM과 함께 배송되고 번들로 제공되는 경우
>* 작성 환경의 기존 UI를 확장할 때 사용합니다.
>* Adobe 기업 자료, 광고 및 프레젠테이션.
>* Adobe 브랜드 애플리케이션의 UI(다른 사용자가 해당 글꼴을 즉시 사용할 수 없도록 해야 함).
>* 간단한 사용자 정의

>
>
Coral UI는 다음 위치에 사용하지 않아야 합니다.
>
>* Adobe과 관련이 없는 문서 및 기타 항목.
>* 컨텐츠 작성 환경(이전 항목이 다른 사람이 생성할 수 있는 경우).
>* Adobe에 명확하게 연결되어 있지 않은 애플리케이션/구성 요소/웹 페이지

>



Coral UI는 웹 애플리케이션을 개발하기 위한 구성 요소 모음입니다.

![chlimage_1-84](assets/chlimage_1-84.png)

처음부터 모듈식으로 설계된 각 모듈은 기본 역할에 따라 별개의 레이어를 형성합니다. 레이어는 서로 지원하도록 설계되었지만 필요할 경우 독립적으로 사용할 수도 있습니다. 따라서 HTML 지원 환경에서 Coral의 사용자 경험을 구현할 수 있습니다.

Coral UI에서는 특정 개발 모델 및/또는 플랫폼을 사용해야 하는 것은 아닙니다. Coral의 주요 목표는 이 마크업을 전송하는 데 사용되는 실제 방법과 관계없이 통합 및 깔끔한 HTML5 마크업을 제공하는 것입니다. 클라이언트 또는 서버측 렌더링, 템플릿, JSP, PHP 또는 Adobe Flash RIA 애플리케이션의 이름을 몇 개만 지정할 때 사용할 수 있습니다.

### HTML 요소 - 마크업 레이어 {#html-elements-the-markup-layer}

HTML 요소는 모든 기본 UI 요소(탐색 막대, 단추, 메뉴, 레일 등)에 대한 일반적인 모양과 느낌을 제공합니다.

가장 기본적인 수준에서 HTML 요소는 전용 클래스 이름을 가진 HTML 태그입니다. 보다 복잡한 요소는 서로 중첩된 여러 태그로 구성될 수 있습니다(특정 방식으로).

CSS는 실제 모양과 느낌을 제공하는 데 사용됩니다. 모양 및 느낌(예: 브랜딩의 경우) 실제 스타일 값을 쉽게 사용자 지정할 수 있도록 하기 위해 런타임 동안 [LESS](https://lesscss.org/) 프리 프로세서에 의해 확장되는 변수로 선언됩니다.

목적:

* 기본적인 UI 요소에 일반적인 모양 및 느낌 제공
* 기본 그리드 시스템 제공

구현:

* [bootstrap](https://twitter.github.com/bootstrap/)에서 영감을 받은 스타일이 있는 HTML 태그
* 클래스는 LESS 파일에 정의됩니다.
* 아이콘은 글꼴 스프라이트로 정의됩니다

예를 들어 마크업은 다음과 같습니다.

```xml
<button class="btn btn-large btn-primary" type="button">Large button</button>
<button class="btn btn-large" type="button">Large button</button>
```

다음으로 표시됩니다.

![chlimage_1-85](assets/chlimage_1-85.png)

모양과 느낌은 전용 클래스 이름으로 요소에 연결된 LESS에 정의됩니다(간결성을 위해 다음 추출이 단축됨).

```xml
.btn {
    font-size: @baseFontSize;
    line-height: @baseLineHeight;
    .buttonBackground(@btnBackground,
                                @btnBackgroundHighlight,
                                @grayDark, 0 1px 1px rgba(255,255,255,.75));
```

실제 값은 LESS 변수 파일에 정의됩니다(간결성을 위해 다음 추출이 단축됨).

```xml
@btnBackgroundHighlight: darken(@white, 10%);
@btnPrimaryBackgroundHighlight: spin(@btnPrimaryBackground, 20%);
@baseFontSize: 17px;
@baseFontFamily: @sansFontFamily;
```

### 요소 플러그인 {#element-plugins}

대부분의 HTML 요소에는 팝업 메뉴를 열고 닫는 등 동적 비헤이비어가 표시되어야 합니다. JavaScript를 사용하여 DOM을 조작함으로써 이러한 작업을 수행하는 요소 플러그인의 역할입니다.

플러그인은 다음 중 하나입니다.

* 특정 DOM 요소에서 작동하도록 설계되었습니다. 예를 들어 대화 상자 플러그인은 `DIV class=dialog`을(를) 찾습니다.
* 본성은 일반적이다. 예를 들어 레이아웃 관리자는 `DIV` 또는 `LI` 요소 목록에 대한 레이아웃을 제공합니다.

다음 중 한 방법으로 매개 변수를 사용하여 플러그인 비헤이비어를 사용자 정의할 수 있습니다.

* javascript 호출을 통해 매개 변수 전달
* HTML 마크업에 연결된 전용 `data-*` 특성 사용

개발자는 모든 플러그인에 대해 최상의 접근 방법을 선택할 수 있지만 thumb 규칙은 다음과 같습니다.

* `data-*` 속성을 참조하십시오. 예를 들어 열 수를 지정하려면
* 데이터와 관련된 기능에 대한 API 옵션/클래스입니다. 예를 들어 표시할 항목 목록을 구성합니다.

양식 유효성 검사를 구현하는 데 동일한 개념을 사용합니다. 유효성을 검사하려는 요소의 경우 필요한 입력 양식을 사용자 지정 `data-*` 속성으로 지정해야 합니다. 그런 다음 이 속성은 유효성 검사 플러그인에 대한 옵션으로 사용됩니다.

>[!NOTE]
>
>가능한 경우 HTML5 기본 양식 유효성 검사를 사용하고/또는 확장할 때는 항상 사용해야 합니다.

목적:

* HTML 요소에 동적 동작 제공
* 순수 CSS로 사용할 수 없는 사용자 정의 레이아웃 제공
* 양식 유효성 검사 수행
* 고급 DOM 조작 수행

구현:

* jQuery 플러그인, 특정 DOM 요소에 연결되어 있습니다.
* `data-*` 특성을 사용하여 비헤이비어 사용자 정의

예제 태그의 추출(data-* 속성으로 지정된 옵션 참고):

```xml
<ul data-column-width="220" data-layout="card" class="cards">
  <li class="item">
    <div class="thumbnail">
      <img href="/a.html" src="/a.thumb.319.319..png">
      <div class="caption">
        <h4>Toolbar</h4>
          <p><small>toolbar</small><br></p>
      </div>
    </div>
  </li>
  <li class="item">
    <div class="thumbnail">
      <img href="/a.html" src="/a.thumb.319.319..png">
      <div class="caption">
        <h4>Toolbar</h4>
        <p><small>toolbar</small><br></p>
      </div>
    </div>
  </li>
```

jQuery 플러그인에 대한 호출:

```
$(‘.cards’).cardlayout ();
```

다음과 같이 표시됩니다.

![chlimage_1-86](assets/chlimage_1-86.png)

`cardLayout` 플러그인은 각 높이를 기준으로 둘러싸인 `UL` 요소를 레이아웃하며 부모의 너비를 고려합니다.

### HTML 요소 위젯 {#html-elements-widgets}

위젯은 하나 이상의 기본 요소를 Javascript 플러그인과 결합하여 &quot;상위 수준&quot; UI 요소를 형성합니다. 이러한 요소는 단일 요소가 제공할 수 있는 것보다 더 복잡한 비헤이비어와 보다 복잡한 모양과 느낌을 구현할 수 있습니다. 태그 선택기 또는 레일 위젯이 좋은 예입니다.

위젯은 페이지의 다른 위젯과 협력하기 위해 사용자 정의 이벤트를 트리거하고 들을 수 있습니다. 일부 위젯은 실제로 Coral HTML 요소를 사용하는 기본 jQuery 위젯입니다.

목적:

* 복잡한 비헤이비어를 표시하는 높은 수준의 UI 요소 구현
* 이벤트 트리거 및 처리

구현:

* jQuery plugin + HTML 마크업
* 클라이언트/서버측 템플릿을 활용할 수 있음

마크업 예:

```
<input type="text" name="tags" placeholder="Tags" class="tagManager"/>
```

jQuery 플러그인 호출(옵션 포함):

```
$(".tagManager").tagsManager({
        prefilled: ["Pisa", "Rome"] })
```

플러그인은 HTML 마크업을 전송합니다(이 마크업에서는 다른 플러그인을 내부적으로 사용할 수 있는 기본 요소를 사용합니다).

```
<span>Pisa</code>
<a title="Removing tag" tagidtoremove="0"
   id="myRemover_0" class="myTagRemover" href="#">x</a></code>

<span id="myTag_1" class="myTag"><span>Rome</code>
<a title="Removing tag" tagidtoremove="1"
   id="myRemover_1" class="myTagRemover" href="#">x</a></code>

<input type="text" data-original-title="" class="input-medium tagManager"
       placeholder="Tags" name="tags" data-provide="typeahead" data-items="6"
       autocomplete="off">
```

다음과 같이 표시됩니다.

![chlimage_1-87](assets/chlimage_1-87.png)

### 유틸리티 라이브러리 {#utility-library}

이 라이브러리는 다음과 같은 javascript 도우미 플러그인 및/또는 함수의 컬렉션입니다.

* UI 독립적
* 모든 기능을 갖춘 웹 애플리케이션을 구축하는 데 있어 매우 중요합니다

여기에는 XSS 처리 및 이벤트 버스가 포함됩니다.

HTML 요소 플러그인 및 위젯은 유틸리티 라이브러리에서 제공하는 기능에 의존할 수 있지만 유틸리티 라이브러리는 요소 또는 위젯 자체에 대한 강력한 종속성을 가질 수 없습니다.

목적:

* 일반적인 기능 제공
* 이벤트 버스 구현
* 클라이언트측 템플릿
* XSS

구현:

* jQuery 플러그인 또는 AMD 호환 JavaScript 모듈
