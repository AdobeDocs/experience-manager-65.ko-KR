---
title: 랜딩 페이지용 디자인 Importer 확장 및 구성
description: 랜딩 페이지용 디자인 가져오기 도구를 구성하는 방법을 알아봅니다.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: 1b8c6075-13c6-4277-b726-8dea7991efec
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '3442'
ht-degree: 0%

---

# 랜딩 페이지용 디자인 Importer 확장 및 구성{#extending-and-configuring-the-design-importer-for-landing-pages}

이 섹션에서는 랜딩 페이지의 디자인 임포터를 구성하고 원하는 경우 확장하는 방법을 설명합니다. 가져오기 후 랜딩 페이지 작업은 [랜딩 페이지](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)에서 다룹니다.

**디자인 가져오기에서 사용자 지정 구성 요소를 추출하도록 설정**

다음은 디자인 임포터에서 사용자 지정 구성 요소를 인식하도록 하는 논리적 단계입니다

1. TagHandler 만들기

   * 태그 처리기는 특정 종류의 HTML 태그를 처리하는 POJO입니다. TagHandler가 처리할 수 있는 HTML 태그의 &quot;종류&quot;는 TagHandlerFactory의 OSGi 속성 &quot;tagpattern.name&quot;을 통해 정의됩니다. 이 OSGi 속성은 기본적으로 처리하려는 입력 html 태그와 일치해야 하는 정규 표현식입니다. 중첩된 모든 태그는 처리를 위해 태그 처리기에 throw됩니다. 예를 들어 중첩된 &lt;p> 태그가 포함된 div에 등록하는 경우 &lt;p> 태그도 TagHandler에 throw되며 처리 방법은 사용자가 결정합니다.
   * 태그 처리기 인터페이스는 SAX 콘텐츠 처리기 인터페이스와 유사합니다. 각 html 태그에 대한 SAX 이벤트를 수신합니다. 태그 처리기 공급자는 디자인 가져오기 프레임워크에서 자동으로 호출되는 특정 라이프사이클 메서드를 구현해야 합니다.

1. 해당 TagHandlerFactory를 만듭니다.

   * 태그 처리기 팩토리는 태그 처리기의 인스턴스 생성을 담당하는 OSGi 구성 요소(단일 항목)입니다.
   * 태그 처리기 팩터리에서는 이 값이 입력 html 태그에 대해 일치하는 &quot;tagpattern.name&quot;이라는 OSGi 속성을 노출해야 합니다.
   * 입력 html 태그와 일치하는 태그 처리기가 여러 개 있는 경우 순위가 더 높은 태그 처리기가 선택됩니다. 순위 자체가 OSGi 속성 **service.ranking**(으)로 노출됩니다.
   * TagHandlerFactory는 OSGi 구성 요소입니다. TagHandler에 제공하려는 모든 참조는 이 팩터리를 통해서만 가능합니다.

1. 기본값을 재정의하려면 TagHandlerFactory의 순위가 더 높아야 합니다.

>[!CAUTION]
>
>랜딩 페이지 [을(를) 가져오는 데 사용되는 디자인 가져오기는 AEM 6.5](/help/release-notes/deprecated-removed-features.md#deprecated-features)에서 더 이상 사용되지 않습니다.

## 가져오기 HTML 준비 {#preparing-the-html-for-import}

Importer 페이지를 만든 후 전체 HTML 랜딩 페이지를 가져올 수 있습니다. HTML 랜딩 페이지를 가져오려면 먼저 해당 콘텐츠를 디자인 패키지에 압축해야 합니다. 디자인 패키지에는 참조된 에셋(이미지, css, 아이콘, 스크립트 등)과 함께 HTML 랜딩 페이지가 포함되어 있습니다.

다음 치트 시트는 가져올 HTML을 준비하는 방법에 대한 샘플을 제공합니다.

랜딩 페이지 치트 시트

[파일 가져오기](assets/cheatsheet.zip)

### Zip 파일 레이아웃 및 요구 사항 {#zip-file-layout-and-requirements}

>[!NOTE]
>
>이 시점에서 ZIP 파일은 하나의 HTML 페이지 또는 페이지의 일부만 포함할 수 있습니다.

zip의 샘플 레이아웃은 다음과 같습니다.

* /index.html > 랜딩 페이지 HTML 파일
* /css > CSS clientlib에 추가합니다.
* /img > 모든 이미지 및 에셋
* /js > JS clientlib에 추가

레이아웃은 HTML5 Boilerplate 모범 사례 레이아웃을 기반으로 합니다. 자세한 내용은 [https://html5boilerplate.com/](https://html5boilerplate.com/)을 참조하세요.

>[!NOTE]
>
>최소한 디자인 패키지 **must**&#x200B;에는 루트 수준에서 **index.html** 파일이 포함되어 있습니다. 가져올 랜딩 페이지에 모바일 버전도 있는 경우, zip에는 루트 수준에서 **mobile.index.html**&#x200B;과 **index.html**&#x200B;이(가) 포함되어야 합니다.

### 랜딩 페이지 HTML 준비 {#preparing-the-landing-page-html}

HTML을 가져오려면 캔버스 div를 랜딩 페이지 HTML에 추가해야 합니다.

캔버스 div는 `id="cqcanvas"`이(가) 있는 html **div**&#x200B;이며, HTML `<body>` 태그 내에 삽입해야 하며 변환을 위한 콘텐츠를 둘러싸야 합니다.

캔버스 div 추가 후 랜딩 페이지 HTML의 샘플 조각은 다음과 같습니다.

```xml
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title></title>
  <meta name="description" content="">
</head>
<body>
 <div id="cqcanvas">
  <!-- HTML content intended for conversion -->
 </div>
</body>
</html>
```

### 편집 가능한 AEM 구성 요소를 포함하도록 HTML 준비 {#preparing-the-html-to-include-editable-aem-components}

랜딩 페이지를 가져올 때 페이지를 있는 그대로 가져올 수 있습니다. 즉, 랜딩 페이지를 가져온 후에는 AEM에서 가져온 항목을 편집할 수 없습니다(페이지에 AEM 구성 요소를 추가할 수 있음).

랜딩 페이지를 가져오기 전에 랜딩 페이지의 일부 부분을 편집 가능한 AEM 구성 요소로 변환할 수 있습니다. 이를 통해 랜딩 페이지 디자인을 가져온 후에도 랜딩 페이지의 일부를 빠르게 편집할 수 있습니다.

가져온 HTML 파일의 적절한 구성 요소에 `data-cq-component`을(를) 추가하면 됩니다.

다음 섹션에서는 랜딩 페이지의 특정 부분을 다른 편집 가능한 AEM 구성 요소로 변환할 수 있도록 HTML 파일을 편집하는 방법을 설명합니다. 구성 요소는 [랜딩 페이지 구성 요소](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)에 자세히 설명되어 있습니다.

>[!NOTE]
>
>랜딩 페이지의 일부를 AEM 구성 요소로 변환하는 HTML 마크업에는 긴 양식과 축약된 태그 선언이 모두 있습니다. 두 가지 모두 각 구성 요소에 대해 설명되어 있습니다.

### 제한 사항 {#limitations}

가져오기 전에 다음 제한 사항에 유의하십시오.

### &amp;lt;body> 태그에 적용된 클래스 또는 ID와 같은 모든 속성은 유지되지 않습니다 {#any-attribute-like-class-or-id-applied-on-the-amp-lt-body-tag-is-not-preserved}

ID 또는 클래스와 같은 특성이 본문 태그에 적용되면(예: `<body id="container">`) 가져오기 후에는 유지되지 않습니다. 따라서 가져올 디자인에는 `<body>` 태그에 적용된 특성에 대한 종속성이 없어야 합니다.

### zip 드래그 앤 드롭 {#drag-and-drop-zip}

Internet Explorer 및 Firefox 버전 3.6 이하에서는 드래그/드롭 zip 업로드가 지원되지 않습니다. 이러한 브라우저를 사용할 때 디자인을 업로드하려면 파일 놓기 영역을 클릭하여 파일 업로드 대화 상자를 열고 해당 대화 상자를 사용하여 디자인을 업로드합니다.

디자인 zip의 &quot;드래그 앤 드롭&quot;을 지원하는 브라우저는 Chrome, Safari5.x, Firefox 4 이상입니다.

### 현대화는 지원되지 않습니다. {#modernizr-is-not-supported}

`Modernizr.js`은(는) 브라우저의 기본 기능을 감지하고 html5 요소에 적합한지 여부를 감지하는 JavaScript 기반 도구입니다. 다른 브라우저의 이전 버전에서 지원을 강화하기 위해 Modernizr를 사용하는 디자인은 랜딩 페이지 솔루션에서 가져오기 문제를 일으킬 수 있습니다. `Modernizr.js` 스크립트는 디자인 임포터에서 지원되지 않습니다.

### 디자인 패키지를 가져올 때 페이지 속성이 유지되지 않습니다 {#page-properties-are-not-preserved-at-the-time-of-importing-design-package}

디자인 패키지를 가져오기 전에 페이지(빈 랜딩 페이지 템플릿을 사용)에 대해 설정된 모든 페이지 속성(예: 사용자 지정 도메인, HTTPS 적용 등)은 디자인을 가져온 후에 손실됩니다. 따라서 디자인 패키지를 가져온 후 페이지 속성을 설정하는 것이 좋습니다.

### HTML 전용 마크업 가정 {#html-only-markup-assumed}

가져올 때 보안상의 이유로 잘못된 마크업을 가져와서 게시하지 않도록 마크업이 정리됩니다. 이는 HTML 전용 마크업과 인라인 SVG 또는 웹 구성 요소와 같은 다른 모든 형식의 요소가 필터링된다고 가정합니다.

### 텍스트 {#text}

디자인 패키지 내의 HTML에 텍스트 구성 요소(`foundation/components/text`)를 삽입하는 HTML 마크업:

```xml
<div data-cq-component="text"> <p>This is some editable text</p> </div>
```

위의 마크업을 HTML에 포함하면에서 다음을 수행합니다.

* 디자인 패키지를 가져온 후 만든 랜딩 페이지에서 편집 가능한 AEM 텍스트 구성 요소(`sling:resourceType=foundation/components/text`)를 만듭니다.
* 만든 텍스트 구성 요소의 `text` 속성을 `div` 내에 포함된 HTML으로 설정합니다.

**축약 구성 요소 태그 선언**:

```xml
<p data-cq-component="text">Text component shorthand</p>
```

**목록이 있는 텍스트**

목록이 있는 텍스트를 추가하려면:

* 1st
* 2nd

RTE 편집기에서 편집할 수 있습니다.

```xml
<div data-cq-component="text"><p>This is text with a list:</p><ul><li>1st</li><li>2nd</li></ul><p>It can be edited with the RTE editor</p></div>
```

**색상 텍스트**

RTE 편집기에서 편집할 수 있는 색상(분홍색)의 텍스트를 추가하려면 다음을 수행합니다.

```xml
<div class="pink" data-cq-component="text"><p>This is pink text.</p><p>It can be edited with the RTE editor</p></div>
```

### 제목 {#title}

디자인 패키지 내의 HTML에 제목 구성 요소(`wcm/landingpage/components/title`)를 삽입하는 HTML 마크업:

```xml
<div data-cq-component="title"> <h1>This is some editable title text</h1> </div>
```

위의 마크업을 HTML에 포함하면에서 다음을 수행합니다.

* 디자인 패키지를 가져온 후 만든 랜딩 페이지에서 편집 가능한 AEM 제목 구성 요소(`sling:resourceType=wcm/landingpage/components/title`)를 만듭니다.
* 만들어진 제목 구성 요소의 `jcr:title` 속성을 div에 래핑된 제목 태그 내의 텍스트로 설정합니다.
* `type` 속성을 제목 태그(이 경우 `h1`)로 설정합니다.

제목 구성 요소는 `h1, h2, h3, h4, h5, h6` 및 `default` 형식을 지원합니다.

**축약 구성 요소 태그 선언**:

```xml
<h1 data-cq-component="title">Title component shorthand</h1>
```

### 이미지 {#image}

디자인 패키지 내의 HTML에 이미지 구성 요소(foundation/components/image)를 삽입하는 HTML 마크업:

```xml
<div data-cq-component="image">
<img src="img/video1.png" alt="Video about Polar Brake Goggles in action" title="Polar Brake Goggles" width="300" height="200" />
</div>
```

위의 마크업을 HTML에 포함하면에서 다음을 수행합니다.

* 디자인 패키지를 가져온 후 만든 랜딩 페이지에서 편집 가능한 AEM 이미지 구성 요소(`sling:resourceType=foundation/components/image`)를 만듭니다.
* 생성된 이미지 구성 요소의 `fileReference` 속성을 src 특성에 지정된 이미지를 가져오는 경로로 설정합니다.
* `alt` 속성을 img 태그의 alt 특성 값으로 설정합니다.
* `title` 속성을 img 태그의 title 특성 값으로 설정합니다.
* `width` 속성을 img 태그의 width 특성 값으로 설정합니다.
* `height` 속성을 img 태그의 height 특성 값으로 설정합니다.

**축약 구성 요소 태그 선언:**

```xml
<img data-cq-component="image" src="test.png" alt="Image component shorthand"/>
```

#### 절대 URL img src는 이미지 구성 요소 Div 내에서 지원되지 않습니다. {#absolute-url-img-src-not-supported-within-image-component-div}

절대 URL src가 있는 `<img>` 태그가 구성 요소 변환에 시도되면 적절한 **UnsupportedTagContentException**&#x200B;이(가) 발생합니다. 예를 들어, 다음은 지원되지 않습니다.

`<div data-cq-component="image">`

`<img src="https://cdn.printfriendly.com/pf-button.gif" alt="Print Friendly and PDF"/>`

`</div>`

그렇지 않으면 이미지 구성 요소 div의 일부가 아닌 img 태그에 대해 절대 URL 이미지가 지원됩니다.

### 클릭 유도 문안 구성 요소 {#call-to-action-components}

가져오기할 랜딩 페이지의 일부를 &quot;편집 가능한 콜 투 액션 구성 요소&quot;로 표시할 수 있습니다. 가져온 콜 투 액션 구성 요소는 랜딩 페이지를 가져온 후 편집할 수 있습니다. AEM에는 다음 CTA 구성 요소가 포함되어 있습니다.

* 클릭스루 링크 - 클릭할 때 방문자를 대상 URL로 안내하는 텍스트 링크를 추가할 수 있습니다.
* 그래픽 링크 - 클릭하면 방문자를 대상 URL로 안내하는 이미지를 추가할 수 있습니다.

#### 클릭스루 링크 {#click-through-link}

이 CTA 구성 요소를 사용하여 랜딩 페이지에 텍스트 링크를 추가할 수 있습니다.

지원되는 속성

* 굵게, 기울임체 및 밑줄 옵션이 있는 레이블
* 대상 URL, 타사 및 AEM URL 지원
* 페이지 렌더링 옵션(같은 창, 새 창 등)

가져온 zip에 클릭스루 구성 요소를 포함하는 HTML 태그입니다. 여기서 href는 대상 URL에 매핑되고 &quot;제품 세부 정보 보기&quot;는 레이블에 매핑되는 방식입니다.

```xml
<div id="cqcanvas">
.
.
                <div data-cq-component="clickThroughLink">
        <a href="/content/we-retail/us/en/products/equipment/snow-sports/flying-snowboard.html">View Product Details  ></a>
  </div>
.
.
</div>
```

이 구성 요소는 독립 실행형 애플리케이션에서 사용하거나 zip에서 가져올 수 있습니다.

**축약 구성 요소 태그 선언**:

```xml
<a href="/somelink.html" data-cq-component="clickThroughLink">Click Through Link shorthand</a>
```

#### 그래픽 링크 {#graphical-link}

이 CTA 구성 요소를 사용하여 랜딩 페이지에 링크가 있는 모든 그래픽 이미지를 추가할 수 있습니다. 이미지는 간단한 버튼일 수 있거나 배경으로서의 모든 그래픽 이미지일 수 있습니다. 이미지를 클릭하면 구성 요소 속성에 지정된 대상 URL로 이동합니다. &quot;콜 투 액션&quot; 그룹의 일부입니다.

지원되는 속성

* 이미지 자르기, 회전
* 가리킨 텍스트, 설명, 크기(픽셀)
* 대상 URL, 타사 및 AEM URL 지원
* 페이지 렌더링 옵션(같은 창, 새 창 등)

가져온 zip에 그래픽 링크 구성 요소를 포함하는 HTML 태그입니다. 여기서 href는 타겟 URL에 매핑되고, img src는 렌더링 이미지이며, &quot;title&quot;은 마우스로 가리키면 표시되는 텍스트 등입니다.

```xml
<div id="cqcanvas">
  <div data-cq-component="clickThroughGraphicalLink"><a href="https://www.adobe.com/go/wem"><img src="img/call-to-action-button.png" title="Click Here to Learn More" /></a></div>
</div>
```

**축약 구성 요소 태그 선언**:

```xml
<a href="/somelink.html" data-cq-component="clickThroughGraphicalLink"><img src="linkimage.png" alt="Click Through Graphical Link shorthand"/></a>
```

>[!NOTE]
>
>클릭스루 그래픽 링크를 만들려면 div 내의 앵커 태그와 이미지 태그를 `data-cq-component="clickthroughgraphicallink"` 특성으로 둘러싸야 합니다.
>
>예, `<div data-cq-component="clickthroughlink"> <a href="https://myURLhere/"><img src="image source here"></a> </div>`
>
>CSS를 사용하여 이미지를 앵커 태그와 연결하는 다른 방법은 지원되지 않습니다. 예를 들어 다음 마크업은 작동하지 않습니다.
>
>`<div data-cq-component="clickthroughgraphicallink">`
>
>`<a class="hasBackground" href="https://myURLhere/"></a>`
>
>`</div>`
>
>연결된 `css .hasbackground { background-image: pathtoimage }` 포함
>

### 리드 양식 {#lead-form}

잠재 고객 양식은 방문자/잠재 고객의 프로필 정보를 수집하는 데 사용되는 양식입니다. 이 정보는 나중에 저장해 두었다가 그 정보를 바탕으로 효과적인 마케팅을 하는 데 사용할 수 있다. 이 정보에는 일반적으로 제목, 이름, 이메일, 생년월일, 주소, 관심 등이 포함됩니다. &quot;CTA 리드 양식&quot; 그룹의 일부입니다.

**지원되는 기능**

* 사전 정의된 리드 필드 - 이름, 성, 주소, dob, 성별, 정보, userId, emailId, 제출 버튼 은 사이드 킥에서 사용할 수 있습니다. 리드 양식에서 필요한 구성 요소를 드래그/드롭하기만 하면 됩니다.
* 이러한 구성 요소를 통해 작성자는 독립형 리드 양식을 디자인할 수 있으며 이러한 필드는 리드 양식 필드에 해당합니다. 독립형 또는 가져온 zip 애플리케이션에서 사용자는 cq:form 또는 cta 리드 양식 필드를 사용하여 필드를 추가하고 요구 사항에 따라 이름을 지정하고 디자인할 수 있습니다.
* CTA 리드 양식의 미리 정의된 특정 이름(예: 리드 양식의 이름에 대한 - firstName 등)을 사용하여 리드 양식 필드를 매핑합니다.
* 리드 양식에 매핑되지 않은 필드는 cq:form 구성 요소(텍스트, 라디오, 확인란, 드롭다운, 숨김, 암호)에 매핑됩니다.
* 사용자는 &quot;label&quot; 태그를 사용하여 제목을 제공하고 스타일 속성 &quot;class&quot;(CTA 리드 양식 구성 요소에만 사용 가능)를 사용하여 스타일을 제공할 수 있습니다.
* 감사 페이지 및 구독 목록은 양식의 숨겨진 매개 변수(index.htm에 있음)로 제공되거나 &quot;리드 양식 시작&quot;의 편집 막대에서 추가/편집할 수 있습니다.

  &lt;input type=&quot;hidden&quot; name=&quot;redirectUrl&quot; value=&quot;/content/we-retail/en/user/register/thank_you&quot;/>

  &lt;input type=&quot;hidden&quot; name=&quot;groupName&quot; value=&quot;leadForm&quot;/>

* 각 구성 요소의 편집 구성에서 - 필수 와 같은 제한을 제공할 수 있습니다.

가져온 zip에 그래픽 링크 구성 요소를 포함하는 HTML 태그입니다. 여기서 &quot;firstName&quot;은 잠재 고객 양식 firstName에 매핑됩니다. 확인란 외에는 이 두 개의 확인란이 cq:form 드롭다운 구성 요소에 매핑됩니다.

```xml
<div id="cqcanvas">
   <div id="form_wrapper">
    <h2>NEWSLETTER SIGN UP</h2>
       <div data-cq-component="leadFormGeneration">
       <form method="post" action="#" onsubmit="return popupBox()">
       <label for="firstName" class="checkText">
        FIRST NAME
       </label><br />
       <input name="firstName" class="text pink" type="text" /><br />
       <label for="lastName" class="checkText">
        LAST NAME
       </label><br />
       <input name="lastName" class="text pink" type="text" /><br />
       <label for="emailId" class="checkText">
        EMAIL ADDRESS
       </label><br />
       <input name="emailId" class="text pink" type="text" /><br />

       <div class="checkboxes">
       <input type="checkbox" class="check" name="send_news" /> <label for="send_news" class="checkText">Send me the latest We.Retail news and announcements.</label><br />
       <input type="checkbox" class="check" name="send_offers" /> <label for="send_offers" class="checkText">Send me We.Retail deals and special offers.</label><br />
       </div>
       <input type="submit" name="submit" class="submit pink" value="Sign Up >" />
       </form>
     </div>
   </div>
```

### Parsys {#parsys}

AEM Parsys 구성 요소는 다른 AEM 구성 요소를 포함할 수 있는 컨테이너 구성 요소입니다. 가져온 HTML에 Parsys 구성 요소를 추가할 수 있습니다. 이를 통해 사용자는 편집 가능한 AEM 구성 요소를 가져온 후에도 랜딩 페이지에 추가/삭제할 수 있습니다.

단락 시스템은 사용자에게 사이드 킥을 사용하여 구성 요소를 추가할 수 있는 기능을 제공합니다.

디자인 패키지 내의 HTML에 Parsys 구성 요소(`foundation/components/parsys`)를 삽입하는 HTML 마크업:

```xml
<div data-cq-component="parsys">
   <div data-cq-component="title"><h2>ULTIMATE PROTECTION</h2></div>
        <div data-cq-component="title"><h3>ON SALE</h3></div>
</div>
```

위의 마크업을 HTML에 포함하면 다음 작업이 수행됩니다.

* 디자인 패키지를 가져온 후 생성된 랜딩 페이지에 AEM Parsys 구성 요소(foundation/components/parsys)를 삽입합니다.
* 기본 구성 요소로 사이드 킥을 초기화합니다. 사이드 킥에서 Parsys 구성 요소로 구성 요소를 드래그하여 새 구성 요소를 랜딩 페이지에 추가할 수 있습니다.
* 두 개의 제목 구성 요소도 Parsys의 일부입니다.

### 대상 {#target}

타겟 구성 요소는 페이지에 경험 콘텐츠를 표시합니다. 하나는 캠페인에서 생성된 많은 경험을 가질 수 있으며 타겟 구성 요소는 페이지를 방문하는 다양한 사용자에게 다양한 경험의 콘텐츠를 동적으로 표시할 수 있습니다.

타겟 구성 요소를 삽입하고 캠페인에서 다른 경험을 만드는 html 마크업입니다.

```xml
<div data-cq-component="target">
 <section data-cq-component="experience" data-cq-experience="default">
  <p data-cq-component="text">Default content. Select this campaign in client context to view other experiences</p>
 </section>

 <section data-cq-component="experience" data-cq-segment="over-30">
  <p data-cq-component="text">Content for Over 30</p>
 </section>

 <section data-cq-component="experience" data-cq-segment="under-30">
  <p data-cq-component="text">Content for Under 30</p>
 </section>
</div>
```

## 추가 가져오기 옵션 {#additional-importing-options}

가져온 구성 요소가 편집 가능한 AEM 구성 요소인지 여부를 지정하는 것 외에 디자인 패키지를 가져오기 전에 다음을 구성할 수도 있습니다.

* 가져온 페이지에 정의된 메타데이터를 추출하여 HTML 속성을 설정합니다.
* HTML에서 charset 인코딩을 지정합니다.
* Importer 페이지 템플릿을 오버레이합니다.

### HTML 가져온 페이지에 정의된 메타데이터를 추출하여 페이지 속성 설정 {#setting-page-properties-by-extracting-metadata-defined-in-imported-html}

가져온 HTML의 헤드에 선언된 다음 메타데이터는 디자인 임포터에 의해 속성 &quot;jcr:description&quot;으로 추출 및 보존됩니다.

* &lt;meta name=&quot;description&quot; content=&quot;&quot;>

HTML 태그에 설정된 Lang 속성은 디자인 임포터에서 &quot;jcr:language&quot; 속성으로 추출 및 보존됩니다.

* &lt;html lang=&quot;en&quot;>

### html에서 charset 인코딩 지정 {#specifying-the-charset-encoding-in-the-html}

디자인 가져오기는 가져온 HTML에 지정된 인코딩을 읽습니다. 인코딩을 다음과 같이 지정할 수 있습니다.

`<meta charset="UTF-8">`

*또는*

`<meta http-equiv="content-type" content="text/html;charset=utf-8">`

가져온 HTML에 인코딩이 지정되지 않은 경우 디자인 임포터에 의해 설정된 기본 인코딩 세트는 UTF-8입니다.

### 템플릿 오버레이 {#overlaying-template}

빈 랜딩 페이지 템플릿은 `/apps/<appName>/designimporter/templates/<templateName>`에 만들어 겹칠 수 있습니다.

AEM에서 템플릿을 만드는 단계는 [템플릿](/help/sites-developing/templates.md)에 설명되어 있습니다.

### 랜딩 페이지에서 구성 요소 참조 {#referring-a-component-from-landing-page}

data-cq-component 속성을 사용하여 HTML에서 참조할 구성 요소가 있어서 디자인 임포터가 여기에 포함된 구성 요소를 렌더링한다고 가정해 보십시오. 예를들어, 테이블 구성 요소(`resourceType = /libs/foundation/components/table`)를 참조합니다. HTML에 다음을 추가해야 합니다.

`<div data-cq-component="/libs/foundation/components/table">foundation table</div>`

data-cq-component의 경로는 구성 요소의 resourceType이어야 합니다.

### 모범 사례 {#best-practices}

가져오기 시 구성 요소 변환으로 표시된 요소에는 다음 선택기와 유사한 CSS 선택기를 사용하지 않는 것이 좋습니다.

| E > F | E 요소의 F 요소 자식 | [자식 조합기](https://www.w3.org/TR/css3-selectors/#child-combinators) |
|---|---|---|
| E + F | E 요소 바로 앞에 있는 F 요소 | [인접 형제 결합자](https://www.w3.org/TR/css3-selectors/#adjacent-sibling-combinators) |
| E ~ F | 앞에 E 요소가 오는 F 요소 | [일반 형제 조합자](https://www.w3.org/TR/css3-selectors/#general-sibling-combinators) |
| E:root | 문서의 루트인 E 요소 | [구조적 의사 클래스](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-child(n) | 상위 요소의 n번째 하위 요소인 E 요소 | [구조적 의사 클래스](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-last-child(n) | 마지막 요소부터 계산하여 상위의 n번째 하위가 되는 E 요소 | [구조적 의사 클래스](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-of-type(n) | 해당 유형의 n 번째 형제 요소인 E 요소 | [구조적 의사 클래스](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-last-of-type(n) | E 원소, 즉 해당 유형의 n번째 형제, 마지막 원소로부터 계산 | [구조적 의사 클래스](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |

가져오기 후 생성된 HTML에 &lt;div> 태그와 같은 추가 html 요소가 추가되기 때문입니다.

* 위와 유사한 구조에 의존하는 스크립트도 AEM 구성 요소로 전환되도록 표시된 요소와 함께 사용하지 않는 것이 좋습니다.
* &lt;div data-cq-component=&quot;&amp;ast;&quot;>와 같은 구성 요소 전환을 위해 마크업 태그에 스타일을 사용하는 것은 권장되지 않습니다.
* 디자인 레이아웃은 HTML5 Boilerplate의 모범 사례를 따라야 합니다. 자세한 내용: [https://html5boilerplate.com/](https://html5boilerplate.com/).

## OSGI 모듈 구성 {#configuring-osgi-modules}

OSGI 콘솔을 통해 구성 가능한 속성을 표시하는 구성 요소는 다음과 같습니다.

* 랜딩 페이지 디자인 가져오기
* 랜딩 페이지 빌더
* 모바일 랜딩 페이지 빌더
* 랜딩 페이지 항목 전처리기

아래 표는 속성에 대해 간략하게 설명합니다.

<table>
 <tbody>
  <tr>
   <td><strong>구성 요소</strong></td>
   <td><strong>속성 이름</strong></td>
   <td><strong>속성 설명 </strong></td>
  </tr>
  <tr>
   <td>랜딩 페이지 디자인 가져오기</td>
   <td>필터 추출</td>
   <td>추출 시 파일을 필터링하는 데 사용할 정규 표현식 목록입니다. 지정된 패턴과 일치하는 <br />개의 Zip 항목이 추출에서 제외됨</td>
  </tr>
  <tr>
   <td>랜딩 페이지 빌더</td>
   <td>파일 패턴</td>
   <td>파일 패턴으로 정의된 정규 표현식과 일치하는 HTML 파일을 처리하도록 랜딩 페이지 빌더를 구성할 수 있습니다.</td>
  </tr>
  <tr>
   <td>모바일 랜딩 페이지 빌더</td>
   <td>파일 패턴</td>
   <td>파일 패턴으로 정의된 정규 표현식과 일치하는 HTML 파일을 처리하도록 랜딩 페이지 빌더를 구성할 수 있습니다.</td>
  </tr>
  <tr>
   <td> </td>
   <td>장치 그룹</td>
   <td>지원할 장치 그룹 목록입니다.</td>
  </tr>
  <tr>
   <td>랜딩 페이지 항목 전처리기</td>
   <td>검색 패턴 </td>
   <td>아카이브 항목 컨텐츠에서 검색할 패턴입니다. 이 정규 표현식은 입력 내용 라인과 행별로 일치합니다. 일치하는 텍스트가 있으면 지정된 대체 패턴으로 바뀝니다.<br /> <br /> 랜딩 페이지 항목 전처리기의 현재 제한 사항에 대해서는 아래 참고 사항을 참조하십시오.</td>
  </tr>
  <tr>
   <td> </td>
   <td>패턴 바꾸기</td>
   <td>찾은 일치 항목을 대체하는 패턴입니다. $1, $2와 같은 정규 표현식 그룹 참조를 사용할 수 있습니다. 또한 이 패턴은 가져오는 동안 실제 값으로 확인되는 {designPath}과(와) 같은 키워드를 지원합니다.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>**랜딩 페이지 항목 전처리기의 현재 제한:**
>검색 패턴을 변경해야 하는 경우 felix 속성 편집기를 열 때 regex 메타문자를 이스케이프하려면 백슬래시 문자를 수동으로 추가해야 합니다. 백슬래시 문자를 수동으로 추가하지 않으면 정규 표현식은 유효하지 않은 것으로 간주되며 이전 문자를 대체하지 않습니다.
>
>예를 들어 기본 구성이
>
>>`/\* *CQ_DESIGN_PATH *\*/ *(['"])`
>
>검색 패턴에서 `CQ_DESIGN_PATH`을(를) `VIPURL`(으)로 바꾸어야 검색 패턴이 다음과 같습니다.
>
>`/\* *VIPURL *\*/ *(['"])`

## 문제 해결 {#troubleshooting}

디자인 패키지를 가져올 때 이 섹션에 설명된 몇 가지 오류가 발생할 수 있습니다.

### 랜딩 페이지 관련 구성 요소로 사이드 킥 초기화 {#initialization-of-sidekick-with-landing-page-relevant-components}

디자인 패키지에 Parsys 구성 요소 마크업이 포함된 경우 가져온 후 사이드 킥에서 랜딩 페이지 관련 구성 요소를 표시하기 시작합니다. 새 구성 요소를 랜딩 페이지 내의 Parsys 구성 요소로 끌어다 놓을 수 있습니다. 디자인 모드로 이동하여 사이드 킥에 새 구성 요소를 추가할 수도 있습니다.

### 가져오는 동안 오류 메시지가 표시됨 {#error-messages-displayed-during-import}

오류가 있는 경우(예: 가져온 패키지가 유효한 zip이 아님) 디자인 가져오기에서 패키지를 가져오지 않습니다. 대신, 드래그 앤 드롭 상자 바로 위의 페이지 맨 위에 오류 메시지가 표시됩니다. 오류 시나리오의 예는 여기에 설명되어 있습니다. 오류를 수정한 후 업데이트된 zip 파일을 동일한 빈 랜딩 페이지로 다시 가져올 수 있습니다. 오류가 발생하는 다양한 시나리오는 다음과 같습니다.

* 가져온 디자인 패키지는 유효한 zip 아카이브가 아닙니다.
* 가져온 디자인 패키지에 최상위 수준의 index.html이 포함되어 있지 않습니다.

### 가져오기 후 표시되는 경고 {#warnings-displayed-after-import}

경고(예: HTML은 패키지 내에 존재하지 않는 이미지를 참조)가 있는 경우 디자인 임포터는 zip을 가져오지만 동시에 결과 창에 문제/경고 목록이 표시됩니다. 문제 링크를 클릭하면 디자인 패키지 내에 문제가 있음을 나타내는 경고 목록이 표시됩니다. 디자인 임포터에 의해 경고가 포착되고 표시되는 다양한 시나리오는 다음과 같습니다.

* HTML은 패키지 내에 존재하지 않는 이미지를 나타냅니다.
* HTML은 패키지 내에 존재하지 않는 스크립트를 나타냅니다.
* HTML은 패키지 내에 존재하지 않는 스타일을 나타냅니다.

### AEM에서 ZIP 파일의 파일은 어디에 저장되어 있습니까? {#where-are-the-files-of-the-zip-file-being-stored-in-aem}

랜딩 페이지를 가져오면 디자인 패키지 내의 파일(이미지, css, js 등)이 AEM의 다음 위치에 저장됩니다.

`/etc/designs/default/canvas/content/campaigns/<name of brand>/<name of campaign>/<name of landing page>`

랜딩 페이지가 캠페인 `We.Retail` 아래에 생성되고 랜딩 페이지의 이름이 **myBlankLandingPage**&#x200B;라고 가정하고 Zip 파일이 저장된 위치는 다음과 같습니다.

`/etc/designs/default/canvas/content/campaigns/geometrixx/myBlankLandingPage`

### 서식이 유지되지 않음 {#formatting-not-preserved}

CSS를 만들 때는 다음 제한 사항에 유의하십시오.

텍스트 및 (편집 가능한) 이미지가 다음과 같은 경우:

```xml
<div class="box">
<p><div data-cq-component="image"><img src="assets/image.jpg" width="115"
height="116" /></div>Some Text </p>
</div>
```

`box` 클래스에 다음과 같이 CSS를 적용합니다.

```xml
.box

{ width: 450px; padding:10px; border: 1px #C5DBE7 solid; margin: 0px auto 0 auto; background-image:url(assets/box.gif); background-repeat:repeat-x,y; font-family:Verdana, Arial, Helvetica, sans-serif; font-size:12px; color:#6D6D6D; }
```

`box img`이(가) 디자인 Importer에서 사용되면 결과 랜딩 페이지의 형식이 유지되지 않은 것으로 보입니다. 이 문제를 해결하기 위해 AEM은 CSS에 div 태그를 추가하고 그에 따라 코드를 다시 작성합니다. 그렇지 않으면 일부 CSS 규칙이 올바르지 않습니다.

```xml
.box img

{ float:right; margin: 0 0 5px 5px; border: 1px #343434 solid; }
```

>[!NOTE]
>
>디자이너는 **id=cqcanvas** 태그 내의 코드만 가져오기에서 인식해야 합니다. 그렇지 않으면 디자인이 유지되지 않습니다.
