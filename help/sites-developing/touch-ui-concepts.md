---
title: AEM 터치 지원 UI의 개념
seo-title: AEM 터치 지원 UI의 개념
description: AEM 5.6 Adobe을 통해 작성 환경을 위한 응답형 디자인을 갖춘 새로운 터치에 적합한 UI가 도입되었습니다
seo-description: AEM 5.6 Adobe을 통해 작성 환경을 위한 응답형 디자인을 갖춘 새로운 터치에 적합한 UI가 도입되었습니다
uuid: 401c5a65-6ddc-4942-ab8e-395016f9c629
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: df3aaed1-97b5-4a4a-af74-cb887462475b
docset: aem65
exl-id: f13ac6c2-16ab-422d-9005-ab0b49172271
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2197'
ht-degree: 2%

---

# AEM 터치 지원 UI의 개념{#concepts-of-the-aem-touch-enabled-ui}

AEM에서는 터치 및 데스크톱 장치에서 모두 작동하도록 설계된 작성자 환경을 위해 [응답형 디자인](/help/sites-authoring/responsive-layout.md)이 있는 터치 지원 UI를 제공합니다.

>[!NOTE]
>
>터치 지원 UI는 AEM의 표준 UI입니다. 클래식 UI는 AEM 6.4에서 더 이상 사용되지 않습니다.

터치 활성화 UI는 다음과 같습니다.

* 다음을 수행하는 세트 헤더.
   * 로고를 표시합니다
   * 전역 탐색에 대한 링크를 제공합니다.
   * 다른 일반 작업에 대한 링크를 제공합니다.검색, 도움말, Marketing Cloud 솔루션, 알림 및 사용자 설정과 같은 .
* 표시할 수 있는 왼쪽 레일(필요한 경우 및 힌지 가능)입니다.
   * 타임라인
   * 참조
   * 필터
* 탐색 헤더입니다. 이 헤더는 다시 컨텍스트에 따라 지정되며 다음을 표시할 수 있습니다.
   * 현재 사용 중인 콘솔 및/또는 해당 콘솔 내의 위치를 나타냅니다
   * 왼쪽 레일에 대한 선택
   * 탐색 표시
   * 적절한 **만들기** 작업에 액세스
   * 선택 항목 보기
* 다음과 같은 컨텐츠 영역:
   * 컨텐츠의 항목(페이지, 자산, 포럼 게시물 등)을 나열합니다
   * 요청 시 형식 지정(예: 열, 카드 또는 목록) 가능
   * 반응형 디자인을 사용합니다(디스플레이의 크기는 장치 및/또는 창 크기에 따라 자동으로 조정됨)
   * 무한 스크롤을 사용합니다(페이지 매김이 더 이상 없음, 모든 항목이 한 창에 나열됨).

![chlimage_1-79](assets/chlimage_1-79.png)

>[!NOTE]
>
>거의 모든 AEM 기능이 터치 지원 UI에 포팅되었습니다. 그러나 일부 제한된 경우에는 기능이 클래식 UI로 되돌립니다. 자세한 내용은 [Touch UI 기능 상태](/help/release-notes/touch-ui-features-status.md) 를 참조하십시오.

터치 활성화 UI는 여러 제품에서 사용자 경험의 일관성을 제공하도록 Adobe이 디자인했습니다. 이 API는 다음을 기반으로 합니다.

* **Coral UI** (CUI) 터치 지원 UI에 대한 Adobe의 시각적 스타일 구현. Coral UI는 제품/프로젝트/웹 애플리케이션에서 UI 시각적 스타일을 채택하는 데 필요한 모든 것을 제공합니다.
* **Granite** UI 구성 요소는 Coral UI를 사용하여 빌드됩니다.

터치 지원 UI의 기본 원칙은 다음과 같습니다.

* 모바일 우선(데스크탑을 염두에 두고)
* 반응형 디자인
* 컨텍스트 관련 디스플레이
* 재사용 가능
* 포함된 참조 설명서 포함
* 포함된 테스트 포함
* 이러한 원칙이 모든 요소 및 구성 요소에 적용되도록 하는 상향식 설계

터치 지원 UI 구조에 대한 자세한 개요는 AEM 터치 지원 UI의 [구조](/help/sites-developing/touch-ui-structure.md) 문서를 참조하십시오.

## AEM 기술 스택 {#aem-technology-stack}

AEM은 Granite 플랫폼을 기반으로 하고, Granite 플랫폼에는 Java Content Repository가 포함되어 있습니다.

![chlimage_1-80](assets/chlimage_1-80.png)

## Granite {#granite}

Granite는 Adobe의 개방형 웹 스택으로, 다음을 포함한 다양한 구성 요소를 제공합니다.

* 응용 프로그램 런처
* 모든 것이 배포되는 OSGi 프레임워크
* 다양한 OSGi 보상 서비스를 통해 애플리케이션 구축 지원
* 다양한 로깅 API를 제공하는 포괄적인 로깅 프레임워크
* JCR API 사양의 CRX 저장소 구현
* Apache Sling Web Framework
* 현재 CRX 제품의 추가 부분

>[!NOTE]
>
>Granite는 Adobe 내에서 개방형 개발 프로젝트로 실행됩니다.코드, 토론 및 문제에 대한 기여는 전체 회사에서 수행됩니다.
>
>그러나 Granite는 오픈 소스 프로젝트가 아닌 **입니다.** 이것은 몇 개의 공개 소스 프로젝트(특히 Apache Sling, Felix, Jackrabbit 및 Lucene)를 기반으로 크게 이루어지지만, Adobe은 공개되는 것과 내부적인 것 사이에 명확한 선을 그어 있다.

## Granite UI {#granite-ui}

Granite 엔지니어링 플랫폼도 기초 UI 프레임워크를 제공합니다. 이것의 주요 목적은 다음과 같습니다.

* 세분화된 UI 위젯 제공
* UI 개념을 구현하고 모범 사례(긴 목록 렌더링, 목록 필터링, 개체 CRUD, CUD 마법사...)를 보여 줍니다.
* 확장 및 플러그인 기반 관리 UI 제공

이러한 요구 사항은 다음과 같습니다.

* &quot;모바일 우선&quot;을 준수합니다.
* 확장 가능
* 쉽게 재정의하십시오

![chlimage_1-81](assets/chlimage_1-81.png)
GraniteUI.pdf

[파일 ](assets/graniteui.pdf)
가져오기Granite UI:

* Sling의 RESTful 아키텍처를 사용합니다
* 콘텐츠 중심의 웹 애플리케이션을 빌드하기 위한 구성 요소 라이브러리 구현
* 세분화된 UI 위젯 제공
* 기본적이고 표준화된 UI 제공
* 확장 가능
* 모바일 장치와 데스크톱 장치 모두를 위해 설계되었습니다(모바일 우선 고려 사항)
* Granite 기반 플랫폼/제품/프로젝트에서 사용할 수 있습니다.예 AEM

![chlimage_1-82](assets/chlimage_1-82.png)

* [Granite UI 기초 ](#granite-ui-foundation-components)
구성 요소이 기초 구성 요소 라이브러리는 다른 라이브러리에서 사용하거나 확장할 수 있습니다.
* [Granite UI 관리 구성 요소](#granite-ui-administration-components)

### 클라이언트 측과 서버 측 {#client-side-vs-server-side}

Granite UI의 클라이언트-서버 통신은 개체가 아닌 하이퍼텍스트로 구성되므로 클라이언트가 비즈니스 논리를 이해할 필요가 없습니다

* 서버는 의미 있는 데이터로 HTML을 향상시킵니다
* 클라이언트는 하이퍼미디어로 하이퍼텍스트를 강화합니다(상호 작용)

![chlimage_1-83](assets/chlimage_1-83.png)

#### 클라이언트측 {#client-side}

여기서는 작성자가 대화형 웹 앱을 빌드할 의도를 표현할 수 있도록 제공된 HTML 어휘의 확장을 사용합니다. 이는 [WAI-ARIA](https://www.w3.org/TR/wai-aria/) 및 [microformats](https://microformats.org/)와 유사한 접근 방식입니다.

주로 클라이언트측에서 실행되는 JS 및 CSS 코드로 해석되는 상호 작용 패턴 컬렉션(예: 비동기 양식 제출)으로 구성됩니다. 클라이언트측의 역할은 상호 작용을 위한 마크업(서버에서 제공하는 하이퍼미디어 제공)을 향상시키는 것입니다.

클라이언트측은 모든 서버 기술과 독립적입니다. 서버가 적절한 마크업을 제공하는 한 클라이언트측은 해당 역할을 수행할 수 있습니다.

현재 JS 및 CSS 코드는 범주 아래에 Granite [clientlibs](/help/sites-developing/clientlibs.md) 로 전달됩니다.

`granite.ui.foundation and granite.ui.foundation.admin`

이러한 구성 요소는 컨텐츠 패키지의 일부로 전달됩니다.

`granite.ui.content`

#### 서버측 {#server-side}

이는 작성자가 빠르게 웹 앱을 *compose*&#x200B;할 수 있도록 하는 sling 구성 요소 컬렉션으로 이루어집니다. 개발자는 구성 요소를 개발하고, 작성자는 구성 요소를 웹 앱으로 결합합니다. 서버측 역할은 하이퍼미디어 지원(마크업)을 클라이언트에 제공하는 것입니다.

현재 구성 요소는 Granite 리포지토리의 다음 위치에 있습니다.

`/libs/granite/ui/components/foundation`

컨텐츠 패키지의 일부로 전달됩니다.

`granite.ui.content`

### 클래식 UI {#differences-with-the-classic-ui} 의 차이점

Granite UI와 ExtJS(클래식 UI에 사용됨)의 차이점도 다음과 같습니다.

<table>
 <tbody>
  <tr>
   <td><strong>ExtJS</strong></td>
   <td><strong>Granite UI</strong></td>
  </tr>
  <tr>
   <td>원격 프로시저 호출<br /> </td>
   <td>상태 변환</td>
  </tr>
  <tr>
   <td>데이터 전송 개체</td>
   <td>Hypermedia</td>
  </tr>
  <tr>
   <td>클라이언트가 서버 내부 정보 파악</td>
   <td>클라이언트가 내부 정보를 모릅니다.</td>
  </tr>
  <tr>
   <td>"패트 클라이언트"</td>
   <td>"씬 클라이언트"</td>
  </tr>
  <tr>
   <td>전문 클라이언트 라이브러리</td>
   <td>범용 클라이언트 라이브러리</td>
  </tr>
 </tbody>
</table>

### Granite UI 기초 구성 요소 {#granite-ui-foundation-components}

[Granite UI 기초 구성 요소](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)는 UI를 작성하는 데 필요한 기본 구성 요소를 제공합니다. 여기에는 다음과 같은 것들이 포함됩니다.

* 단추
* 하이퍼링크
* 사용자 아바타

기초 구성 요소는 다음 위치에서 찾을 수 있습니다.

`/libs/granite/ui/components/foundation`

이 라이브러리에는 각 Coral 요소에 대한 Granite UI 구성 요소가 포함되어 있습니다. 구성 요소는 저장소에 구성이 있는 컨텐츠 제어 구성 요소입니다. 이렇게 하면 HTML 마크업을 직접 작성하지 않고도 Granite UI 애플리케이션을 작성할 수 있습니다.

목적:

* HTML 요소에 대한 구성 요소 모델
* 구성 요소 구성
* 자동 장치 및 기능 테스트

구현:

* 저장소 기반 구성 및 구성
* Granite 플랫폼에서 제공하는 테스트 시설 활용
* JSP 템플릿

이 기초 구성 요소 라이브러리는 다른 라이브러리에서 사용하거나 확장할 수 있습니다.

### ExtJS 및 해당 Granite UI 구성 요소 {#extjs-and-corresponding-granite-ui-components}

Granite UI를 사용하도록 ExtJS 코드를 업그레이드할 때, 다음 목록은 동일한 Granite UI 리소스 유형을 사용하는 ExtJS xtype 및 노드 유형에 대한 편리한 개요를 제공합니다.

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

[Granite UI 관리 구성 요소](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html) 빌드는 모든 관리 애플리케이션에서 구현할 수 있는 일반적인 빌딩 블록을 제공합니다. 여기에는 다음과 같은 것들이 포함됩니다.

* 전역 탐색 모음
* 레일(뼈대)
* 검색 패널

목적:

* 관리 애플리케이션을 위한 통합 모양 및 느낌
* 관리 응용 프로그램 Rad

구현:

* 기초 구성 요소를 사용하여 사전 정의된 구성 요소
* 구성 요소를 사용자 지정할 수 있습니다

## Coral UI {#coral-ui}

CoralUI.pdf

[Get ](assets/coralui.pdf)
FileCoral UI(CUI)는 터치 지원 UI에 대한 Adobe의 시각적 스타일 구현으로, 여러 제품에서 사용자 경험의 일관성을 제공하도록 설계되었습니다. Coral UI는 작성 환경에서 사용되는 시각적 스타일을 적용하는 데 필요한 모든 것을 제공합니다.

>[!CAUTION]
>
>Coral UI는 AEM 고객이 라이선스가 부여된 제품 사용 범위 내에 애플리케이션 및 웹 인터페이스를 구축할 수 있도록 제공되는 UI 라이브러리입니다.
>
>Coral UI는 다음 경우에만 사용할 수 있습니다.
>
>
>* AEM과 함께 배송되고 번들로 제공되는 경우입니다.
>* 작성 환경의 기존 UI를 확장할 때 사용할 수 있습니다.
>* 기업 자료, 광고 및 프레젠테이션 Adobe
>* Adobe 브랜드 애플리케이션의 UI(다른 사용자가 해당 글꼴을 쉽게 사용할 수 있게 해서는 안 됨).
>* 사소한 사용자 지정 사용.

>
>
Coral UI는 다음 위치에서 사용하지 않아야 합니다.
>
>* Adobe과 관련이 없는 문서 및 기타 항목입니다.
>* 컨텐츠 작성 환경(다른 사용자가 이전 항목을 생성할 수 있는 경우).
>* Adobe에 명확하게 연결되지 않은 응용 프로그램/구성 요소/웹 페이지입니다.

>



Coral UI는 웹 응용 프로그램을 개발하기 위한 기본 구성 요소의 컬렉션입니다.

![chlimage_1-84](assets/chlimage_1-84.png)

처음부터 모듈식으로 설계되었으므로 각 모듈은 기본 역할에 따라 고유한 계층을 형성합니다. 레이어는 서로 지원하도록 설계되었지만 필요한 경우 독립적으로 사용할 수도 있습니다. 따라서 HTML 가능 환경에서 Coral의 사용자 경험을 구현할 수 있습니다.

Coral UI에서는 특정 개발 모델 및/또는 플랫폼을 사용해야 하는 것이 아닙니다. Coral의 기본 목표는 이 마크업을 내보내는 데 사용되는 실제 방법과는 무관하게 통합 및 깨끗한 HTML5 마크업을 제공하는 것입니다. 몇 가지 예를 들면 클라이언트 또는 서버측 렌더링, 템플릿, JSP, PHP 또는 Adobe Flash RIA 응용 프로그램에 사용할 수 있습니다.

### HTML 요소 - 마크업 레이어 {#html-elements-the-markup-layer}

HTML 요소는 모든 기본 UI 요소(탐색 막대, 단추, 메뉴, 레일 등)에 대한 일반적인 모양과 느낌을 제공합니다.

가장 기본적인 수준에서 HTML 요소는 전용 클래스 이름을 사용하는 HTML 태그입니다. 보다 복잡한 요소는 서로 중첩된(특정 방식으로) 여러 태그로 구성될 수 있습니다.

CSS는 실제 모양과 느낌을 제공하는 데 사용됩니다. 모양과 느낌(예: 브랜딩의 경우)을 쉽게 사용자 지정할 수 있도록 하기 위해 실제 스타일 값은 런타임 동안 [LESS](https://lesscss.org/) 사전 프로세서에 의해 확장된 변수로 선언됩니다.

목적:

* 일반적인 모양 및 느낌을 갖는 기본 UI 요소 제공
* 기본 그리드 시스템을 제공합니다.

구현:

* [부트스트랩](https://twitter.github.com/bootstrap/)에서 영감을 받은 스타일을 사용하는 HTML 태그
* 클래스는 LESS 파일에서 정의됩니다
* 아이콘은 글꼴 스프라이트로 정의됩니다

예를 들어 다음과 같은 마크업이 있습니다.

```xml
<button class="btn btn-large btn-primary" type="button">Large button</button>
<button class="btn btn-large" type="button">Large button</button>
```

이 다음과 같이 표시됩니다.

![chlimage_1-85](assets/chlimage_1-85.png)

모양과 느낌은 전용 클래스 이름으로 요소에 연결된 LESS에서 정의됩니다(간결성을 위해 다음 추출이 단축됨).

```xml
.btn {
    font-size: @baseFontSize;
    line-height: @baseLineHeight;
    .buttonBackground(@btnBackground,
                                @btnBackgroundHighlight,
                                @grayDark, 0 1px 1px rgba(255,255,255,.75));
```

실제 값은 LESS 변수 파일에 정의됩니다. (간결성을 위해 다음 추출이 단축되었습니다.)

```xml
@btnBackgroundHighlight: darken(@white, 10%);
@btnPrimaryBackgroundHighlight: spin(@btnPrimaryBackground, 20%);
@baseFontSize: 17px;
@baseFontFamily: @sansFontFamily;
```

### 요소 플러그인 {#element-plugins}

많은 HTML 요소에서는 팝업 메뉴 열기 및 닫기와 같은 일부 종류의 동적 동작이 표시되어야 합니다. JavaScript를 사용하여 DOM을 조작하여 이러한 작업을 수행하는 요소 플러그인의 역할입니다.

플러그인은 다음 중 하나입니다.

* 특정 DOM 요소에서 작동하도록 디자인되었습니다. 예를 들어 대화 상자 플러그인은 `DIV class=dialog`을 찾아야 합니다.
* 일반적이죠 예를 들어 레이아웃 관리자는 `DIV` 또는 `LI` 요소 목록에 대한 레이아웃을 제공합니다

다음 중 한 방법으로 매개 변수로 플러그인 동작을 사용자 지정할 수 있습니다.

* javascript 호출을 통해 매개 변수 전달
* HTML 마크업에 연결된 전용 `data-*` 속성 사용

개발자는 모든 플러그인에 대해 가장 적합한 접근 방식을 선택할 수 있지만 경험상 다음과 같은 규칙을 사용합니다.

* `data-*` html 레이아웃과 관련된 옵션의 속성입니다. 예를 들어, 열 수를 지정하려면
* 데이터와 관련된 기능에 대한 API 옵션/클래스입니다. 예를 들어, 표시할 항목 목록을 구성합니다

양식 유효성 검사를 구현하는 데에도 동일한 개념이 사용됩니다. 유효성을 검사하려는 요소의 경우 필수 입력 양식을 사용자 지정 `data-*` 속성으로 지정해야 합니다. 그런 다음 이 속성을 유효성 검사 플러그인의 옵션으로 사용합니다.

>[!NOTE]
>
>HTML5 네이티브 양식 유효성 검사는 가능한 경우 사용하거나 확장할 때 사용해야 합니다.

목적:

* HTML 요소에 동적 동작 제공
* 순수 CSS로 불가능한 사용자 지정 레이아웃 제공
* 양식 유효성 검사 수행
* 고급 DOM 조작 수행

구현:

* jQuery 플러그인, 특정 DOM 요소에 연결되어 있습니다.
* `data-*` 속성을 사용하여 동작 사용자 지정

예제 마크업 추출(data-* 속성으로 지정된 옵션 참고):

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

`cardLayout` 플러그인은 각각의 높이를 기준으로 둘러싸인 `UL` 요소를 레이아웃하며 부모의 너비를 고려합니다.

### HTML 요소 위젯 {#html-elements-widgets}

위젯은 하나 이상의 기본 요소를 Javascript 플러그인과 결합하여 &quot;높은 수준&quot; UI 요소를 형성합니다. 이렇게 하면 단일 요소가 전달할 수 있는 것보다 더 복잡한 동작과 더 복잡한 모양과 느낌을 구현할 수 있습니다. 태그 선택기 또는 레일 위젯이 좋은 예입니다.

위젯은 트리거와 사용자 지정 이벤트를 모두 수신하여 페이지의 다른 위젯과 협력할 수 있습니다. 일부 위젯은 실제로 Coral HTML 요소를 사용하는 기본 jQuery 위젯입니다.

목적:

* 복잡한 동작을 나타내는 높은 수준의 UI 요소 구현
* 이벤트 트리거 및 처리

구현:

* jQuery 플러그인 + HTML 마크업
* 클라이언트/서버 측 템플릿을 활용할 수 있음

마크업 예는 다음과 같습니다.

```
<input type="text" name="tags" placeholder="Tags" class="tagManager"/>
```

jQuery 플러그인에 대한 호출(옵션 포함):

```
$(".tagManager").tagsManager({
        prefilled: ["Pisa", "Rome"] })
```

플러그인은 HTML 마크업을 내보냅니다(이 마크업에서는 기본 요소를 사용하므로 내부적으로 다른 플러그인을 사용할 수 있습니다.).

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
* 모든 기능을 갖춘 웹 애플리케이션을 구축하려면 매우 중요한

여기에는 XSS 처리 및 이벤트 버스가 포함됩니다.

HTML 요소 플러그인 및 위젯은 유틸리티 라이브러리에서 제공하는 기능에 의존할 수 있지만 유틸리티 라이브러리는 요소 또는 위젯 자체에 대한 하드 종속성을 가질 수 없습니다.

목적:

* 공통 기능 제공
* 이벤트 버스 구현
* 클라이언트측 템플릿
* XSS

구현:

* jQuery 플러그인 또는 AMD 호환 JavaScript 모듈
