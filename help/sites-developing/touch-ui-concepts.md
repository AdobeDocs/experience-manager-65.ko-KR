---
title: Adobe Experience Manager 터치 지원 UI의 개념
description: Adobe Experience Manager 5.6에서 Adobe은 작성 환경을 위한 반응형 디자인이 포함된 터치에 최적화된 새 UI를 도입했습니다
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: f13ac6c2-16ab-422d-9005-ab0b49172271
source-git-commit: 69346a710708ee659ee97e9fdc193c8ea2658fe6
workflow-type: tm+mt
source-wordcount: '2167'
ht-degree: 1%

---

# Adobe Experience Manager 터치 지원 UI의 개념{#concepts-of-the-aem-touch-enabled-ui}

Adobe Experience Manager(AEM)에는 터치 지원 UI와 [반응형 디자인](/help/sites-authoring/responsive-layout.md) 터치 및 데스크탑 디바이스 모두에서 작동하도록 설계된 작성 환경용.

>[!NOTE]
>
>터치 활성화 UI는 AEM용 표준 UI입니다. 클래식 UI는 AEM 6.4에서 더 이상 사용되지 않습니다.

터치 지원 UI에는 다음이 포함됩니다.

* 다음과 같은 세트 헤더입니다.
   * 로고 표시
   * 전역 탐색에 대한 링크를 제공합니다.
   * 검색, 도움말, Experience Cloud 솔루션, 알림 및 사용자 설정과 같은 다른 일반 작업에 대한 링크를 제공합니다.
* 왼쪽 레일(필요할 때 표시되며 숨길 수 있음)은 다음과 같이 표시할 수 있습니다.
   * 타임라인
   * 참조
   * 필터
* 탐색 헤더입니다. 이 헤더는 다시 문맥을 구분하며 다음을 표시할 수 있습니다.
   * 현재 사용 중인 콘솔, 해당 콘솔 내 위치 또는 둘 다를 나타냅니다.
   * 왼쪽 레일 선택
   * 이동 경로
   * 적절한 액세스 권한 **만들기** 작업
   * 선택 항목 보기
* 다음과 같은 콘텐츠 영역:
   * 콘텐츠 항목(페이지, 에셋, 포럼 게시물 등)을 나열합니다.
   * 열, 카드 또는 목록과 같이 요청한 대로 형식을 지정할 수 있습니다.
   * 반응형 디자인 사용(디스플레이는 장치 및/또는 창 크기에 따라 자동으로 크기 조정)
   * 무한 스크롤링 사용(더 이상 페이지 매김을 하지 않음, 모든 항목이 하나의 창에 나열됨)

![chlimage_1-79](assets/chlimage_1-79.png)

>[!NOTE]
>
>거의 모든 AEM 기능이 터치 지원 UI로 포팅되었습니다. 그러나 일부 제한된 경우 기능은 클래식 UI로 되돌아갑니다. 다음을 참조하십시오 [Touch UI 기능 상태](/help/release-notes/touch-ui-features-status.md) 추가 정보.

터치 지원 UI는 여러 제품에서 Adobe 경험에 일관성을 제공하도록 사용자가 설계되었습니다. 이는 다음을 기반으로 합니다.

* **Coral UI** (CUI) 터치 지원 UI에 대한 Adobe의 시각적 스타일 구현. Coral UI는 제품/프로젝트/웹 애플리케이션이 UI 시각적 스타일을 채택하는 데 필요한 모든 것을 제공합니다.
* **Granite UI** 구성 요소는 Coral UI로 구축됩니다.

터치 지원 UI의 기본 원칙은 다음과 같습니다.

* 모바일 우선(데스크탑을 염두에 두고)
* 반응형 디자인
* 컨텍스트 관련 표시
* 재사용 가능
* 포함된 참조 설명서 포함
* 포함된 테스트 포함
* 이러한 원칙이 모든 요소 및 구성 요소에 적용되도록 하는 상향식 설계

터치 사용 UI 구조에 대한 자세한 개요는 를 참조하십시오. [AEM 터치 지원 UI의 구조](/help/sites-developing/touch-ui-structure.md).

## AEM 기술 스택 {#aem-technology-stack}

AEM은 Granite 플랫폼을 기반으로 하며, Granite 플랫폼에는 특히 Java™ Content Repository가 포함됩니다.

![chlimage_1-80](assets/chlimage_1-80.png)

## Granite {#granite}

Granite는 Adobe의 오픈 웹 스택으로, 다음을 포함한 다양한 구성 요소를 제공합니다.

* 애플리케이션 런처
* 모든 것이 배포되는 OSGi 프레임워크
* 애플리케이션 구축을 지원하는 여러 OSGi 표준 서비스
* 다양한 로깅 API를 제공하는 포괄적인 로깅 프레임워크
* JCR API 사양의 CRX 저장소 구현
* Apache Sling 웹 프레임워크
* 현재 CRX 제품의 추가 부분

>[!NOTE]
>
>Granite는 Adobe 내에서 개방형 개발 프로젝트로 운영됩니다. 코드, 토론 및 문제에 대한 기여는 회사 전체에서 이루어집니다.
>
>그러나 Granite는 **아님** 오픈 소스 프로젝트입니다. 여러 오픈 소스 프로젝트(특히 Apache Sling, Felix, Jackrabbit 및 Lucene)를 기반으로 하지만, Adobe은 공개 프로젝트와 내부 프로젝트 간에 명확한 선을 그립니다.

## Granite UI {#granite-ui}

Granite 엔지니어링 플랫폼은 기본 UI 프레임워크를 제공합니다. 주요 목표는 다음과 같습니다.

* 세분화된 UI 위젯 제공
* UI 개념 구현 및 모범 사례 설명(긴 목록 렌더링, 목록 필터링, 개체 CRUD, CUD 마법사...)
* 확장 가능한 플러그인 기반 관리 UI 제공

이는 다음 요구 사항을 준수합니다.

* &quot;모바일 우선&quot; 존중
* 확장 가능
* 재정의 용이성

![chlimage_1-81](assets/chlimage_1-81.png)
GraniteUI.pdf

[파일 가져오기](assets/graniteui.pdf)
Granite UI:

* Sling의 RESTful 아키텍처 사용
* 컨텐츠 중심 웹 애플리케이션 구축을 위한 구성 요소 라이브러리 구현
* 세분화된 UI 위젯 제공
* 표준화된 기본 UI 제공
* 확장 가능
* 모바일 장치와 데스크탑 장치 모두를 위해 설계되었습니다(먼저 모바일을 고려함).
* 모든 Granite 기반 플랫폼/제품/프로젝트에서 사용할 수 있습니다(예: AEM).

![chlimage_1-82](assets/chlimage_1-82.png)

* [Granite UI Foundation 구성 요소](#granite-ui-foundation-components)
이 기초 구성 요소 라이브러리는 다른 라이브러리에서 사용하거나 확장할 수 있습니다.
* [Granite UI 관리 구성 요소](#granite-ui-administration-components)

### 클라이언트측과 서버측 {#client-side-vs-server-side}

Granite UI의 클라이언트 서버 통신은 개체가 아닌 하이퍼텍스트로 구성되므로 클라이언트가 비즈니스 논리를 이해할 필요가 없습니다

* 서버는 의미 있는 데이터로 HTML을 강화합니다
* 클라이언트는 하이퍼미디어(상호 작용)로 하이퍼텍스트를 강화합니다

![chlimage_1-83](assets/chlimage_1-83.png)

#### 클라이언트측 {#client-side}

이는 작성자가 대화형 웹 앱을 빌드하려는 의도를 표현할 수 있도록 제공되는 HTML 어휘의 확장을 사용합니다. 이는 과 유사한 접근 방식입니다. [와이아리아](https://www.w3.org/TR/wai-aria/) 및 [마이크로포맷](https://microformats.org/).

주로 클라이언트측에서 실행되는 JS 및 CSS 코드로 해석되는 상호 작용 패턴(예: 양식을 비동기적으로 제출)의 컬렉션으로 구성됩니다. 클라이언트측의 역할은 상호 작용을 위한 마크업(서버에서 하이퍼미디어 어포던스로 제공됨)을 향상시키는 것입니다.

클라이언트측은 어떤 서버 기술과도 독립적입니다. 서버가 적절한 마크업을 제공하는 한 클라이언트측은 자신의 역할을 수행할 수 있습니다.

현재 JS 및 CSS 코드는 Granite로 제공됩니다 [clientlibs](/help/sites-developing/clientlibs.md) 카테고리 아래에 있는:

`granite.ui.foundation and granite.ui.foundation.admin`

이러한 구성 요소는 콘텐츠 패키지의 일부로 제공됩니다.

`granite.ui.content`

#### 서버측 {#server-side}

이는 작성자가 다음과 같은 작업을 수행할 수 있도록 하는 슬링 구성 요소 컬렉션으로 구성됩니다 *작성* 웹 앱 빠른. 개발자는 구성 요소를 개발하고 작성자는 구성 요소를 웹 앱으로 어셈블합니다. 서버측의 역할은 하이퍼미디어 어포던스(마크업)를 클라이언트에게 제공하는 것이다.

현재 구성 요소는 다음 위치의 Granite 저장소에 있습니다.

`/libs/granite/ui/components/foundation`

이는 콘텐츠 패키지의 일부로 제공됩니다.

`granite.ui.content`

### 클래식 UI와의 차이점 {#differences-with-the-classic-ui}

Granite UI와 ExtJS(클래식 UI에 사용됨) 간의 차이점도 관심 대상입니다.

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
   <td>하이퍼미디어</td>
  </tr>
  <tr>
   <td>클라이언트가 서버 내부 정보 파악</td>
   <td>클라이언트가 내부 정보를 알 수 없음</td>
  </tr>
  <tr>
   <td>"Fat 클라이언트"</td>
   <td>"씬 클라이언트"</td>
  </tr>
  <tr>
   <td>특수 클라이언트 라이브러리</td>
   <td>범용 클라이언트 라이브러리</td>
  </tr>
 </tbody>
</table>

### Granite UI Foundation 구성 요소 {#granite-ui-foundation-components}

다음 [Granite UI Foundation 구성 요소](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) 모든 UI 구축에 필요한 기본 구성 요소를 제공하십시오. 여기에는 다음과 같은 항목이 포함됩니다.

* 버튼
* 하이퍼링크
* 사용자 아바타

기초 구성 요소는 다음과 같습니다.

`/libs/granite/ui/components/foundation`

이 라이브러리에는 각 Coral 요소에 대한 Granite UI 구성 요소가 포함되어 있습니다. 구성 요소는 저장소에 상주하면서 컨텐츠를 기반으로 합니다. 이를 통해 손으로 HTML 마크업을 작성하지 않고도 Granite UI 애플리케이션을 구성할 수 있다.

용도:

* HTML 요소의 구성 요소 모델
* 구성 요소 구성
* 자동 장치 및 기능 테스트

구현:

* 저장소 기반 구성 및 구성
* Granite 플랫폼에서 제공하는 테스트 시설 사용
* JSP 템플릿

이 기초 구성 요소 라이브러리는 다른 라이브러리에서 사용하거나 확장할 수 있습니다.

### ExtJS 및 해당 Granite UI 구성 요소 {#extjs-and-corresponding-granite-ui-components}

Granite UI를 사용하도록 ExtJS 코드를 업그레이드할 때 다음 목록에서는 ExtJS xtype 및 노드 유형과 그에 해당하는 Granite UI 리소스 유형에 대한 편리한 개요를 제공합니다.

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

다음 [Granite UI 관리 구성 요소](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) 모든 관리 애플리케이션에서 구현할 수 있는 일반 구성 요소를 제공하기 위해 foundation 구성 요소를 기반으로 빌드합니다. 여기에는 다음과 같은 것들이 포함됩니다.

* 전역 탐색 막대
* 레일(스켈레톤)
* 검색 패널

용도:

* 관리 애플리케이션을 위한 통합 디자인
* 관리 애플리케이션용 Rad

구현:

* 기초 구성 요소를 사용하여 사전 정의된 구성 요소
* 구성 요소를 사용자 정의할 수 있습니다.

## Coral UI {#coral-ui}

CoralUI.pdf

[파일 가져오기](assets/coralui.pdf)
Coral UI(CUI)는 여러 제품에서 사용자 경험에 일관성을 제공하도록 설계된 터치 지원 UI에 대한 Adobe의 시각적 스타일 구현입니다. Coral UI는 작성 환경에서 사용되는 시각적 스타일을 채택하는 데 필요한 모든 기능을 제공합니다.

>[!CAUTION]
>
>Coral UI는 AEM 고객이 라이선스가 부여된 제품 사용 범위 내에서 애플리케이션 및 웹 인터페이스를 구축하기 위해 사용할 수 있는 UI 라이브러리입니다.
>
>Coral UI 사용은 다음 경우에만 허용됩니다.
>
>
>* AEM과 함께 배송되어 번들로 제공된 경우.
>* 작성 환경의 기존 UI를 확장할 때 사용합니다.
>* Adobe 회사 자료, 광고 및 프레젠테이션.
>* Adobe 브랜드 애플리케이션의 UI(글꼴을 다른 용도로 사용할 수 없음).
>* 약간의 맞춤화가 필요합니다.
>
>다음 환경에서는 Coral UI를 사용하지 않아야 합니다.
>
>* Adobe과 관련이 없는 문서 및 기타 항목.
>* 콘텐츠 만들기 환경(다른 사용자가 이전 항목을 생성할 수 있는 경우).
>* Adobe에 명확하게 연결되지 않은 응용 프로그램/구성 요소/웹 페이지.
>

Coral UI는 웹 애플리케이션 개발을 위한 빌딩 블록 모음입니다.

![chlimage_1-84](assets/chlimage_1-84.png)

처음부터 모듈식으로 설계되었으며, 각 모듈은 기본 역할을 기반으로 하여 별개의 레이어를 형성합니다. 비록 층들이 서로 지지하도록 설계되었지만, 필요하다면 독립적으로 사용될 수도 있다. 이를 통해 모든 HTML 가능 환경에서 Coral의 사용자 경험을 구현할 수 있습니다.

Coral UI를 사용하면 특정 개발 모델 및/또는 플랫폼을 사용해야 하는 것은 아닙니다. Coral의 기본 목표는 이 마크업을 내보내는 데 사용되는 실제 방법에 관계없이 통일되고 깔끔한 HTML5 마크업을 제공하는 것입니다. 이는 클라이언트 또는 서버측 렌더링, 템플릿, JSP, PHP 또는 Adobe Flash RIA 애플리케이션에 사용될 수 있습니다.

### HTML 요소 - 마크업 레이어 {#html-elements-the-markup-layer}

HTML 요소는 모든 기본 UI 요소(탐색 막대, 버튼, 메뉴, 레일 등 포함)에 대해 공통적인 모양과 느낌을 제공합니다.

가장 기본적인 수준에서 HTML 요소는 전용 클래스 이름이 있는 HTML 태그입니다. 보다 복잡한 요소는 여러 태그로 구성될 수 있으며, 특정 방식으로 서로 내부에 중첩될 수 있습니다.

CSS를 사용하여 실제 모양과 느낌을 제공합니다. 모양과 느낌을 쉽게 사용자 지정할 수 있도록 하기 위해(예: 브랜딩의 경우) 실제 스타일 값은 [간단히](https://lesscss.org/) 런타임 중 전처리기입니다.

용도:

* 일반적인 모양과 느낌의 기본 UI 요소 제공
* 기본 그리드 시스템 제공

구현:

* HTML에서 영감을 얻은 스타일 태그 [Bootstrap](https://twitter.github.com/bootstrap/)
* 클래스는 LESS 파일에 정의됩니다
* 아이콘은 글꼴 스프라이트로 정의됩니다

예를 들어 마크업은 다음과 같습니다.

```xml
<button class="btn btn-large btn-primary" type="button">Large button</button>
<button class="btn btn-large" type="button">Large button</button>
```

다음과 같이 표시됩니다.

![chlimage_1-85](assets/chlimage_1-85.png)

룩앤필은 전용 클래스 이름으로 요소에 연결된 LESS에서 정의됩니다(간결성을 위해 다음 추출이 단축됨).

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

대부분의 HTML 요소는 팝업 메뉴 열기 및 닫기와 같은 일종의 동적 동작을 표시해야 합니다. JavaScript를 사용하여 DOM을 조작하여 이러한 작업을 수행하는 요소 플러그인의 역할입니다.

플러그인은 다음 중 하나입니다.

* 특정 DOM 요소에서 작동하도록 디자인되었습니다. 예를 들어 대화 상자 플러그인은 다음을 찾을 것으로 예상합니다 `DIV class=dialog`
* 일반적인 기능. 예를 들어 레이아웃 관리자는 다음 목록에 대한 레이아웃을 제공합니다. `DIV` 또는 `LI` 요소

플러그인 동작은 다음 중 하나를 수행하여 매개 변수를 사용하여 사용자 정의할 수 있습니다.

* JavaScript 호출을 사용하여 매개 변수 전달
* 전용 사용 `data-*` HTML 마크업에 연결된 속성

개발자는 모든 플러그인에 대해 최상의 접근 방식을 선택할 수 있지만 경험상 규칙은 다음과 같습니다.

* `data-*` HTML 레이아웃과 관련된 옵션의 속성입니다. 예를 들어 열의 수를 지정하려면
* 데이터와 관련된 기능에 대한 API 옵션/클래스. 예를 들어 표시할 항목 목록 구성

양식 유효성 검사를 구현하는 데 동일한 개념을 사용합니다. 유효성을 검사하려는 요소의 경우 필수 입력 양식을 사용자 지정으로 지정해야 합니다 `data-*` 특성. 그런 다음 이 속성은 유효성 검사 플러그인에 대한 옵션으로 사용됩니다.

>[!NOTE]
>
>HTML5 기본 양식 유효성 검사는 가능한 한 항상 사용하거나 확장해야 합니다.

용도:

* HTML 요소에 동적 동작 제공
* 순수 CSS로는 불가능한 사용자 정의 레이아웃 제공
* 양식 유효성 검사 수행
* 고급 DOM 조작 수행

구현:

* 특정 DOM 요소에 연결된 jQuery 플러그인
* 사용 `data-*` 동작을 사용자 지정할 속성

예제 마크업의 추출(데이터로 지정된 옵션 참고)&#42; 속성):

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
$('.cards').cardlayout ();
```

이는 다음과 같이 표시됩니다.

![chlimage_1-86](assets/chlimage_1-86.png)

다음 `cardLayout` 플러그인은 동봉된 내용을 펼칩니다. `UL` 요소는 각 높이를 기반으로 하고 부모의 너비도 고려합니다.

### HTML 요소 위젯 {#html-elements-widgets}

위젯은 하나 이상의 기본 요소를 JavaScript 플러그인과 결합하여 &quot;더 높은 수준의&quot; UI 요소를 형성합니다. 이렇게 하면 단일 요소가 전달할 수 있는 것보다 더 복잡한 비헤이비어와 더 복잡한 모양과 느낌을 구현할 수 있습니다. 태그 선택기 또는 레일 위젯이 좋은 예입니다.

위젯은 사용자 정의 이벤트를 트리거하고 수신하여 페이지의 다른 위젯과 협력할 수 있습니다. 일부 위젯은 Coral HTML 요소를 사용하는 기본 jQuery 위젯입니다.

용도:

* 복잡한 동작을 나타내는 높은 수준의 UI 요소 구현
* 이벤트 트리거 및 처리

구현:

* jQuery 플러그인 + HTML 마크업
* 클라이언트/서버측 템플릿 사용 가능

마크업의 예는 다음과 같습니다.

```
<input type="text" name="tags" placeholder="Tags" class="tagManager"/>
```

jQuery 플러그인 호출(옵션 포함):

```
$(".tagManager").tagsManager({
        prefilled: ["Pisa", "Rome"] })
```

플러그인은 HTML 마크업을 내보냅니다(이 마크업은 내부적으로 다른 플러그인을 사용할 수 있는 기본 요소를 사용함).

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

이는 다음과 같이 표시됩니다.

![chlimage_1-87](assets/chlimage_1-87.png)

### 유틸리티 라이브러리 {#utility-library}

이 라이브러리는 다음과 같은 JavaScript 도우미 플러그인 및/또는 함수의 컬렉션입니다.

* UI 독립적
* 완벽한 기능을 갖춘 웹 애플리케이션을 구축하는 데 있어 매우 중요합니다.

여기에는 XSS 처리 및 이벤트 버스가 포함됩니다.

HTML 요소 플러그인 및 위젯은 유틸리티 라이브러리에서 제공하는 기능에 의존할 수 있지만 유틸리티 라이브러리는 요소 또는 위젯 자체에 대한 엄격한 종속성을 가질 수 없습니다.

용도:

* 공통 기능 제공
* 이벤트 버스 구현
* 클라이언트측 템플릿
* XSS

구현:

* jQuery 플러그인 또는 AMD 호환 JavaScript 모듈
