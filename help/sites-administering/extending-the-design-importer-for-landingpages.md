---
title: 랜딩 페이지용 디자인 가져오기 확장 및 구성
seo-title: 랜딩 페이지용 디자인 가져오기 확장 및 구성
description: 랜딩 페이지에 대한 디자인 가져오기를 구성하는 방법에 대해 알아봅니다.
seo-description: 랜딩 페이지에 대한 디자인 가져오기를 구성하는 방법에 대해 알아봅니다.
uuid: a2dd0c30-03e4-4e52-ba01-6b0b306c90fc
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: e02f5484-fbc2-40dc-8d06-ddb53fd9afc2
docset: aem65
translation-type: tm+mt
source-git-commit: 0a94bf49a7136c5831c42eb274d07517c12014ec
workflow-type: tm+mt
source-wordcount: '3522'
ht-degree: 62%

---


# 랜딩 페이지용 디자인 가져오기 확장 및 구성{#extending-and-configuring-the-design-importer-for-landing-pages}

이 섹션에서는 랜딩 페이지를 위해 디자인 가져오기를 구성하는 방법과 원하는 경우, 확장하는 방법도 설명합니다. 가져오기 후 랜딩 페이지 작업이 [랜딩 페이지에서 다룹니다.](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)

**디자인 가져오기로 사용자 지정 구성 요소 추출**

디자인 가져오기로 사용자 지정 구성 요소를 인식하는 논리 단계는 다음과 같습니다.

1. TagHandler 만들기

   * 태그 처리기는 특정 종류의 HTML 태그를 처리하는 POJO입니다. TagHandler가 처리할 수 있는 HTML 태그의 “종류”는 TagHandlerFactory의 OSGi 속성 “tagpattern.name”을 통해 정의됩니다. 이 OSGi 속성은 근본적으로 처리할 입력 html 태그와 일치해야 하는 regex입니다. 중첩된 모든 태그가 처리를 위해 태그 처리기에 반환됩니다. 예를 들어 중첩된 &lt;p> 태그가 포함된 div에 등록하는 경우, &lt;p> 태그도 TagHandler에 반환되고 이 태그를 처리하는 방법은 사용자에게 달려 있습니다.
   * 태그 처리기 인터페이스는 SAX 컨텐트 처리기 인터페이스와 유사합니다. 이 인터페이스는 각 html 태그에 대해 SAX 이벤트를 받습니다. 태그 처리기 공급자의 경우, 디자인 가져오기 프레임워크에 의해 자동으로 호출되는 특정 라이프사이클 방식을 구현해야 합니다.

1. 해당 TagHandlerFactory를 만듭니다.

   * 태그 처리기 팩터리는 태그 처리기의 인스턴스를 발생시킬 책임이 있는 OSGi 구성 요소(단독 개체)입니다.
   * 태그 처리기 팩터리는 입력 html 태그와 대해 일치하는 값인 “tagpattern.name”이라는 OSGi 속성을 노출해야 합니다.
   * 입력 html 태그와 일치하는 태그 처리기가 여러 개 있을 경우 등급이 높은 처리기가 선택됩니다. 등급 자체는 OSGi 속성 **service.ranking**&#x200B;으로 노출됩니다.
   * TagHandlerFactory는 OSGi 구성 요소입니다. TagHandler에 제공할 모든 참조는 이 팩터리를 통해야 합니다.

1. 기본값을 무시하려면 TagHandlerFactory의 등급이 더 높은지 확인하십시오.

>[!CAUTION]
>
>랜딩 페이지를 가져오는 데 사용되는 디자인 가져오기 프로그램은 [AEM 6.5에서 더 이상 사용되지 않습니다](/help/release-notes/deprecated-removed-features.md#deprecated-features).

## 가져오기용 HTML 준비 {#preparing-the-html-for-import}

Importer 페이지를 만든 후 전체 HTML 랜딩 페이지를 가져올 수 있습니다. HTML 랜딩 페이지를 가져오려면, 먼저 컨텐트를 디자인 패키지에 zip으로 압축해야 합니다.. 디자인 패키지에는 참조된 자산(이미지, css, 아이콘, 스크립트 등)과 함께 HTML 랜딩 페이지가 들어 있습니다.

다음 치트 시트에서는 가져올 HTML을 준비하는 방법에 대한 샘플을 볼 수 있습니다.

랜딩 페이지 요약서

[파일 가져오기](assets/cheatsheet.zip)

### Zip 파일 레이아웃 및 요구 사항 {#zip-file-layout-and-requirements}

>[!NOTE]
>
>이때, ZIP 파일에는 하나의 HTML 페이지나 페이지의 한 부분만 포함할 수 있습니다.

zip의 샘플 레이아웃은 다음과 같습니다.

* /index.html -> 랜딩 페이지 HTML 파일
* /css -> CSS clientlib에 추가
* /img -> 모든 이미지 및 자산
* /js -> JS clientlib에 추가

레이아웃은 HTML5 표준 문안 우수 사례 레이아웃을 기반으로 합니다. 자세한 내용은 [https://html5boilerplate.com/](https://html5boilerplate.com/)에서 확인하십시오.

>[!NOTE]
>
>최소한 디자인 패키지 **은(는) 루트 수준에서** index.html **파일을 포함해야 합니다.** 가져올 랜딩 페이지에 모바일 버전도 있는 경우, zip에는 루트 수준에서 **index.html**&#x200B;과 함께 **mobile.index.html**&#x200B;이 포함되어야 합니다.

### 랜딩 페이지 HTML 준비 {#preparing-the-landing-page-html}

HTML을 가져올 수 있으려면, canvas div를 랜딩 페이지 HTML에 추가해야 합니다.

canvas div는 HTML `<body>` 태그 내에 삽입해야 하는 html **div**&#x200B;이고 변환할 컨텐츠를 둘러싸야 합니다.`id="cqcanvas"`

canvas div의 추가 후 랜딩 페이지 HTML의 샘플 스니펫은 다음과 같습니다.

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

### 편집 가능한 AEM 구성 요소를 포함하는 HTML 준비 {#preparing-the-html-to-include-editable-aem-components}

랜딩 페이지를 가져오면, 페이지를 있는 그대로 가져올 수 있으며, 이것은 랜딩 페이지를 가져온 후에는 AEM에 있는 가져온 항목을 편집할 수 없다는 것을 의미합니다(페이지에서 AEM 구성 요소를 더 추가할 수는 있습니다).

랜딩 페이지를 가져오기 전에 AEM 구성 요소를 편집할 수 있도록 랜딩 페이지의 일부분을 전환할 수도 있습니다. 이렇게 하면 랜딩 페이지 디자인을 가져온 후에도 랜딩 페이지의 일부분을 신속히 편집할 수 있습니다.

가져오는 HTML 파일의 해당 구성 요소에 `data-cq-component`를 추가하여 이렇게 할 수 있습니다.

다음 섹션에서는 랜딩 페이지의 특정 부분들을 편집 가능한 다양한 AEM 구성 요소로 전환할 수 있도록 HTML 파일을 편집하는 방법에 대해 설명합니다. 구성 요소는 [랜딩 페이지 구성 요소](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)에서 자세히 설명합니다.

>[!NOTE]
>
>랜딩 페이지의 일부를 AEM 구성 요소로 전환하는 HTML 마크업에는 긴 양식과 축약형 태그 선언이 모두 있습니다. 두 선언 모두 각 구성 요소에 대해 설명합니다.

### 제한 사항 {#limitations}

가져오기 전에 다음 제한 사항을 주의하십시오.

### 태그에 적용된 class나 id와 같은 모든 특성은 &amp;lt;body> 태그는 {#any-attribute-like-class-or-id-applied-on-the-amp-lt-body-tag-is-not-preserved} 보존되지 않습니다.

id 또는 class와 같은 속성이 본문 태그에 적용되는 경우(예: `<body id="container">`) 가져오기 후 유지되지 않습니다. 따라서 가져오는 디자인에는 `<body>` 태그에 적용되는 특성에 대한 종속성이 없어야 합니다.

### zip 드래그 앤 드롭 {#drag-and-drop-zip}

zip 드래그/드롭 업로드는 Internet Explorer 및 Firefox 버전 3.6 이하에서는 지원되지 않습니다. 이 브라우저 사용 시 디자인을 업로드하려면, 드롭 파일 영역을 클릭하여 파일 업로드 대화 상자를 열고 이 대화 상자를 사용하여 디자인을 업로드합니다.

디자인 zip의 &quot;드래그 앤 드롭&quot;을 지원하는 브라우저는 Chrome, Safari5.x, Firefox 4 이상입니다.

### Modernizr는 지원되지 않습니다.{#modernizr-is-not-supported}

`Modernizr.js`는 브라우저의 기본 기능을 탐지하고 이 기능이 html5 요소에 적합한지를 탐지하는 javascript 기반 도구입니다. 다양한 브라우저의 이전 버전 지원을 개선하기 위해 Modernizr를 사용하는 디자인은 랜딩 페이지 솔루션에서 가져오기 문제를 일으킬 수 있습니다. `Modernizr.js` 스크립트는 디자인 가져오기에서 지원되지 않습니다.

### 디자인 패키지를 가져올 때 페이지 속성은 유지되지 않습니다.{#page-properties-are-not-preserved-at-the-time-of-importing-design-package}

디자인 패키지를 가져오기 전에 페이지(빈 랜딩 페이지 템플릿을 사용하는 페이지)에 설정된 페이지 속성(예: 사용자 지정 도메인, HTTPS 시행, 등)은디자인을 가져온 후 잃게 됩니다. 따라서 권장 방법은 디자인 패키지를 가져온 후 페이지 속성을 설정하는 것입니다.

### HTML 전용 마크업에는 {#html-only-markup-assumed}

가져오기를 수행할 경우 올바르지 않은 마크업 가져오기 및 게시를 방지하기 위해 보안상의 이유로 마크업이 삭제됩니다. 이 경우 HTML 전용 마크업 및 기타 모든 양식의 요소(예: 인라인 SVG 또는 웹 구성 요소)가 필터링되는 것으로 가정합니다.

### 텍스트 {#text}

디자인 패키지 내의 HTML에 있는 텍스트 구성 요소를 삽입하는 HTML 마크업(`foundation/components/text`):

```xml
<div data-cq-component="text"> <p>This is some editable text</p> </div>
```

HTML에 위의 마크업을 포함하면 다음과 같이 됩니다.

* 디자인 패키지를 가져온 후 만든 랜딩 페이지에서 편집 가능한 AEM 텍스트 구성 요소( `sling:resourceType=foundation/components/text`)를 만듭니다.
* 만들어진 텍스트 구성 요소의 `text` 속성을 `div` 내에 들어 있는 HTML로 설정합니다.

**축약형 구성 요소 태그 선언**:

```xml
<p data-cq-component="text">Text component shorthand</p>
```

**목록이 있는 텍스트**

목록이 있는 텍스트를 추가하려면:

* 1차
* 2차

RTE 편집기에서 편집할 수 있습니다.

```xml
<div data-cq-component="text"><p>This is text with a list:</p><ul><li>1st</li><li>2nd</li></ul><p>It can be edited with the RTE editor</p></div>
```

**색상이 있는 텍스트**

RTE 편집기에서 편집할 수 있는 색상(분홍)이 있는 텍스트를 추가하려면:

```xml
<div class="pink" data-cq-component="text"><p>This is pink text.</p><p>It can be edited with the RTE editor</p></div>
```

### 제목 {#title}

디자인 패키지 내의 HTML에 제목 구성 요소를 삽입하는 HTML 마크업( `wcm/landingpage/components/title`):

```xml
<div data-cq-component="title"> <h1>This is some editable title text</h1> </div>
```

HTML에 위의 마크업을 포함하면 다음과 같이 됩니다.

* 디자인 패키지를 가져온 후 만든 랜딩 페이지에서 편집 가능한 AEM 제목 구성 요소( `sling:resourceType=wcm/landingpage/components/title`)를 만듭니다.
* 만들어진 제목 구성 요소의 `jcr:title`   속성을 div 내에 둘러싸여 있는 제목 태그 내의 텍스트로 설정합니다.
* `type` 속성을 제목 태그로 설정합니다(이 경우, `h1`).

제목 구성 요소는 7가지 유형( `h1, h2, h3, h4, h5, h6` 및 `default`)을 지원합니다.

**축약형 구성 요소 태그 선언**:

```xml
<h1 data-cq-component="title">Title component shorthand</h1>
```

### 이미지 {#image}

디자인 패키지 내의 HTML에 있는 이미지 구성 요소를 삽입하는 HTML 마크업(foundation/components/text):

```xml
<div data-cq-component="image">
<img src="img/video1.png" alt="Video about Polar Brake Goggles in action" title="Polar Brake Goggles" width="300" height="200" />
</div>
```

HTML에 위의 마크업을 포함하면 다음과 같이 됩니다.

* 디자인 패키지를 가져온 후 만든 랜딩 페이지에서 편집 가능한 AEM 이미지 구성 요소( `sling:resourceType=foundation/components/image`)를 만듭니다.
* 만들어진 이미지 구성 요소의 `fileReference` 속성을 src 특성에 지정된 이미지를 가져오는 경로로 설정합니다.
* `alt` 속성을 img 태그에 있는 alt 특성의 값으로 설정합니다.
* `title` 속성을 img 태그에 있는 title 특성의 값으로 설정합니다.
* `width` 속성을 img 태그에 있는 width 특성의 값으로 설정합니다.
* `height` 속성을 img 태그에 있는 height 특성의 값으로 설정합니다.

**축약형 구성 요소 태그 선언**:

```xml
<img data-cq-component="image" src="test.png" alt="Image component shorthand"/>
```

#### 절대 URL img src는 이미지 구성 요소 Div에서 지원되지 않음 {#absolute-url-img-src-not-supported-within-image-component-div}

절대 url src가 있는 `<img>` 태그를 구성 요소 변환에 시도하면 적절한 **UnsupportedTagContentException**&#x200B;이 발생합니다. 예를 들어, 다음은 지원되지 않습니다.

`<div data-cq-component="image">`

`<img src="https://cdn.printfriendly.com/pf-button.gif" alt="Print Friendly and PDF"/>`

`</div>`

하지만, 그렇지 않으면, 절대 URL 이미지는 이미지 구성 요소 div의 일부가 아닌 img 태그에 대해 지원됩니다.

### 클릭유도문안 구성 요소  {#call-to-action-components}

&quot;편집 가능한 클릭유도문안 구성 요소&quot;로 가져올 랜딩 페이지의 일부를 표시할 수 있습니다. 이렇게 가져온 클릭유도문안 구성 요소는 랜딩 페이지를 가져온 후 편집할 수 있습니다. AEM에는 다음의 CTA 구성 요소가 포함되어 있습니다.

* 클릭스루 링크 - 클릭 시 방문자를 타겟 URL로 이동시키는 텍스트 링크를 추가할 수 있습니다.
* 그래픽 링크 - 클릭 시 방문자를 타겟 URL로 이동시키는 이미지를 추가할 수 있습니다.

#### 클릭스루 링크  {#click-through-link}

이 CTA 구성 요소는 랜딩 페이지에서 텍스트 링크를 추가하는 데 사용할 수 있습니다.

지원되는 속성

* 굵은체, 이탤릭체 및 밑줄 옵션이 있는 레이블
* 타사 및 AEM URL을 지원하는 타겟 URL
* 페이지 렌더링 옵션(동일한 창, 새 창, 등)

가져온 zip에 클릭스루 구성 요소를 포함하는 HTML 태그입니다. 여기 href는 타겟 url로 매핑하고, &quot;제품 세부 사항 보기&quot;는 레이블 등으로 매핑합니다.

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

이 구성 요소는 독립형 애플리케이션에 사용하거나, zip에서 가져올 수 있습니다.

**축약형 구성 요소 태그 선언**:

```xml
<a href="/somelink.html" data-cq-component="clickThroughLink">Click Through Link shorthand</a>
```

#### 그래픽 링크 {#graphical-link}

이 CTA 구성 요소는 랜딩 페이지에서 링크가 있는 그래픽 이미지를 추가하는 데 사용할 수 있습니다. 이미지는 간단한 단추나 배경용 그래픽 이미지일 수 있습니다. 이미지를 클릭하면, 구성 요소 속성에 지정된 타겟 URL로 이동합니다. &quot;클릭유도문안&quot; 그룹의 일부입니다.

지원되는 속성

* 이미지 자르기, 회전
* 텍스트, 설명, px 단위 크기를 마우스로 가리키기
* 타사 및 AEM URL을 지원하는 타겟 URL
* 페이지 렌더링 옵션(동일한 창, 새 창, 등)

가져온 zip에 그래픽 링크 구성 요소를 포함하는 HTML 태그입니다. 여기 href는 타겟 url에 매핑되고, img src는 렌더링 이미지이고, &quot;title&quot;은 텍스트 등을 마우스로 가리키면 이동됩니다.

```xml
<div id="cqcanvas">
  <div data-cq-component="clickThroughGraphicalLink"><a href="https://www.adobe.com/go/wem"><img src="img/call-to-action-button.png" title="Click Here to Learn More" /></a></div>
</div>
```

**축약형 구성 요소 태그 선언**:

```xml
<a href="/somelink.html" data-cq-component="clickThroughGraphicalLink"><img src="linkimage.png" alt="Click Through Graphical Link shorthand"/></a>
```

>[!NOTE]
>
>clickthroughgraphical 링크를 만들려면 `data-cq-component="clickthroughgraphicallink"` 특성이 있는 div 내에서 앵커 태그와 이미지 태그를 둘러싸야 합니다.
>
>예: `<div data-cq-component="clickthroughlink"> <a href="https://myURLhere/"><img src="image source here"></a> </div>`
>
>CSS를 사용하여 이미지를 anchor 태그와 연결하는 다른 방법은 지원되지 않습니다. 예를 들어 다음 마크업은 작동하지 않습니다.
>
>`<div data-cq-component="clickthroughgraphicallink">`
>
>`<a class="hasBackground" href="https://myURLhere/"></a>`
>
>`</div>`
>
>연결된 `css .hasbackground { background-image: pathtoimage }`에


### 리드 양식 {#lead-form}

리드 양식은 방문자/리드의 프로필 정보를 수집하는 데 사용되는 양식입니다. 이 정보는 저장했다가 나중에 이 정보를 기반으로 효과적인 마케팅을 수행하는 데 사용할 수 있습니다. 이 정보에는 일반적으로 직책, 이름, 이메일, 출생일, 주소, 관심사 등이 포함됩니다. &quot;CTA 리드 양식&quot; 그룹의 일부입니다.

**지원되는 기능**

* 사전 정의된 리드 필드(이름, 성, 주소, dob, 성별, 정보, 사용자 ID, 이메일 ID, 제출 단추)는 사이드 킥에서 사용할 수 있습니다. 리드 양식에 필요한 구성 요소를 드래그/드롭하면 됩니다.
* 이 구성 요소 작성자의 도움으로 독립형 리드 양식을 디자인할 수 있고, 이렇게 디자인된 필드는 리드 양식 필드에 해당합니다. 독립형 또는 가져온 zip 애플리케이션에서 사용자는 요구 사항에 따라 cq:form이나 cta 리드 양식 필드를 사용하여 필드를 더 만들고, 여기에 이름을 지정하고 디자인할 수 있습니다.
* CTA 리드 양식의 사전 정의된 특정 이름을 사용하여 리드 양식 필드를 매핑할 수 있습니다. 예를 들어 리드 양식의 첫 번째 이름에 firstName을 매핑할 수 있습니다.
* 리드 양식에 매핑되지 않는 필드는 cq:form 구성 요소(텍스트, 라디오 단추, 확인란, 드롭다운, 숨김, 암호)에 매핑됩니다.
* 사용자는 “label” 태그를 사용하여 제목을 제공하고, 스타일 특성 “class”(CTA 리드 양식 구성 요소에만 사용 가능)를 사용하여 스타일을 지정할 수 있습니다.
* 감사 페이지 및 가입 목록은 양식의 숨겨진 매개 변수(index.htm에 있음)로 제공하거나 &quot;리드 양식 시작&quot;의 편집 막대에서 추가/편집할 수 있습니다.

   &lt;input type=&quot;hidden&quot; name=&quot;redirectUrl&quot; value=&quot;/content/we-retail/en/user/register/thank_you&quot; />

   &lt;input type=&quot;hidden&quot; name=&quot;groupName&quot; value=&quot;leadForm&quot; />

* 필수 제한 사항은 각 구성 요소의 편집 구성에서 제공할 수 있습니다.

가져온 zip에 그래픽 링크 구성 요소를 포함하는 HTML 태그입니다. 여기서 &quot;firstName&quot;은 확인란을 제외한 리드 양식 firstName 등에 매핑됩니다. 이 두 확인란은 cq:form 드롭다운 구성 요소에 매핑됩니다.

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

AEM parsys 구성 요소는 다른 AEM 구성 요소를 포함할 수 있는 컨테이너 구성 요소입니다. 가져온 HTML에 parsys 구성 요소를 추가할 수 있습니다. 이렇게 하면 랜딩 페이지를 가져온 후에라도 랜딩 페이지에 편집 가능한 AEM 구성 요소를 추가/삭제할 수 있습니다.

단락 시스템을 사용하면 사이드킥을 사용하여 구성 요소를 추가할 수 있습니다.

디자인 패키지 내의 HTML에 있는 parsys 구성 요소를 삽입하는 HTML 마크업(`foundation/components/parsys`):

```xml
<div data-cq-component="parsys">
   <div data-cq-component="title"><h2>ULTIMATE PROTECTION</h2></div>
        <div data-cq-component="title"><h3>ON SALE</h3></div>
</div>
```

HTML에 위의 마크업을 포함하면 다음과 같이 됩니다.

* 디자인 패키지를 가져온 후 만든 랜딩 페이지에서 AEM parsys 구성 요소(foundation/components/parsys)를 삽입합니다.
* 사이드킥을 기본 구성 요소로 초기화합니다. 사이드킥의 구성 요소를 parsys 구성 요소로 드래그하여 랜딩 페이지에 새 구성 요소를 추가할 수 있습니다.
* 두 제목 구성 요소도 parsys의 일부분입니다.

### 타겟  {#target}

타겟 구성 요소는 페이지에서 경험하는 컨텐트를 보여줍니다. 캠페인에서 만들어진 많은 경험이 있을 수 있고 타겟 구성 요소는 동적으로 다른 경험의 컨텐트를 페이지를 방문하는 다양한 사용자에게 보여줄 수 있습니다.

타겟 구성 요소를 삽입하고 캠페인에서 다양한 경험을 만드는 html 마크업:

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

## 추가적인 가져오기 옵션 {#additional-importing-options}

가져온 구성 요소가 편집 가능한 AEM 구성 요소인지 지정하는 것 외에도, 디자인 패키지를 가져오기 전에 다음 사항도 구성할 수 있습니다.

* 가져온 HTML에 정의된 메타데이터를 추출하여 페이지 속성 설정
* HTML에서 charset 인코딩 지정
* Importer 페이지 템플릿 오버레이입니다.

### 가져온 HTML에 정의된 메타데이터를 추출하여 페이지 속성 설정 {#setting-page-properties-by-extracting-metadata-defined-in-imported-html}

가져온 HTML의 헤드에 선언된 다음 메타데이터는 디자인 가져오기가 추출하여 속성 &quot;jcr:description&quot;으로 보존합니다.

* &lt;meta name=&quot;description&quot; content=&quot;&quot;>

HTML 태그에 설정된 Lang 속성은 디자인 가져오기가 추출하여 속성 &quot;jcr:language&quot;로 보존합니다.

* &lt;html lang=&quot;en&quot;>

### html에서 charset 인코딩 지정 {#specifying-the-charset-encoding-in-the-html}

디자인 가져오기는 가져온 HTML에 지정된 인코딩을 읽습니다. 인코딩은 다음과 같이 지정할 수 있습니다.

`<meta charset="UTF-8">`

*또는*

`<meta http-equiv="content-type" content="text/html;charset=utf-8">`

가져온 HTML에 지정된 인코딩이 없을 경우 디자인 가져오기가 설정하는 기본 인코딩은 UTF-8입니다.

### 템플릿 오버레이  {#overlaying-template}

빈 랜딩 페이지 템플릿은`/apps/<appName>/designimporter/templates/<templateName>`

AEM에서 새 템플릿을 만드는 단계는 [여기](/help/sites-developing/templates.md)에 설명되어 있습니다.

### 랜딩 페이지의 구성 요소 참조 {#referring-a-component-from-landing-page}

디자인 가져오기가 이곳에서 구성 요소 포함을 렌더링하도록 data-cq-component 특성을 사용하여 HTML에서 참조할 구성 요소가 있다고 가정합니다. 예를 들어 표 구성 요소( `resourceType = /libs/foundation/components/table`)를 참조하려고 합니다. HTML에서 다음을 추가해야 합니다.

`<div data-cq-component="/libs/foundation/components/table">foundation table</div>`

data-cq-component에 있는 경로는 구성 요소의 resourceType이어야 합니다.

### 우수 사례 {#best-practices}

가져오기 시 구성 요소 전환을 위해 표시된 요소 사용의 경우 다음과 유사한 CSS 선택기를 사용하는 것은 권장되지 않습니다.

| E > F | E 요소의 F 요소 하위 | [하위 조합기](https://www.w3.org/TR/css3-selectors/#child-combinators) |
|---|---|---|
| E + F | F 요소가 E 요소 바로 뒤에 있습니다. | [인접 동기 콤비네이터](https://www.w3.org/TR/css3-selectors/#adjacent-sibling-combinators) |
| E ~ F | F 요소가 E 요소 뒤에 있습니다. | [일반 동기 콤비네이터](https://www.w3.org/TR/css3-selectors/#general-sibling-combinators) |
| E:root | E 요소, 문서의 루트 | [구조적 유사 계층](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-child(n) | E 요소, 해당 상위의 n번째 하위 | [구조적 유사 계층](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-last-child(n) | E 요소, 그 상위의 n번째 하위, 마지막 항목부터 셈 | [구조적 유사 계층](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-of-type(n) | E 요소, 이 유형의 n번째 동기 | [구조적 유사 계층](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-last-of-type(n) | E 요소, 해당 유형의 n번째 동기, 마지막 항목부터 셈 | [구조적 유사 계층](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |

이것은 가져오기 후 생성된 Html에 &lt;div> 태그와 같은 추가 html 요소가 추가되었기 때문입니다.

* 위와 유사한 구조에 의존하는 스크립트도 AEM 구성 요소로의 전환을 위해 표시된 요소를 사용할 경우에는 권장되지 않습니다.
* &lt;div data-cq-component=&quot;&amp;ast;&quot;>와 같은 구성 요소 전환을 위해 마크업 태그에 스타일을 사용하는 것은 권장되지 않습니다.
* 디자인 레이아웃은 HTML5 표준 문안의 우수 사례를 따라야 합니다. 자세한 내용:[https://html5boilerplate.com/](https://html5boilerplate.com/).

## OSGI 모듈 구성 {#configuring-osgi-modules}

OSGI 콘솔을 통해 구성할 수 있는 속성을 보여주는 구성 요소는 다음과 같습니다.

* 랜딩 페이지 디자인 가져오기
* 랜딩 페이지 빌더
* 모바일 랜딩 페이지 빌더
* 랜딩 페이지 입력 사전 처리기

아래 표에서는 속성에 대해 간략히 설명합니다.

<table>
 <tbody>
  <tr>
   <td><strong>구성 요소</strong></td>
   <td><strong>속성 이름</strong></td>
   <td><strong>속성 설명 </strong></td>
  </tr>
  <tr>
   <td>랜딩 페이지 디자인 가져오기</td>
   <td>추출 필터</td>
   <td>추출에서 파일을 필터링하는 데 사용되는 일반 표현식 목록입니다. <br />지정된 패턴 중 하나라도 일치하는 Zip 항목은 추출에서 제외됩니다.</td>
  </tr>
  <tr>
   <td>랜딩 페이지 빌더</td>
   <td>파일 패턴</td>
   <td>랜딩 페이지 빌더를 구성하여 파일 패턴에 정의된 대로 일반 표현식과 일치하는 HTML 파일을 처리할 수 있습니다.</td>
  </tr>
  <tr>
   <td>모바일 랜딩 페이지 빌더</td>
   <td>파일 패턴</td>
   <td>랜딩 페이지 빌더를 구성하여 파일 패턴에 정의된 대로 일반 표현식과 일치하는 HTML 파일을 처리할 수 있습니다.</td>
  </tr>
  <tr>
   <td> </td>
   <td>장치 그룹</td>
   <td>지원되는 장치 그룹 목록입니다.</td>
  </tr>
  <tr>
   <td>랜딩 페이지 입력 사전 처리기</td>
   <td>검색 패턴 </td>
   <td>아카이브 항목 컨텐트에서 검색할 패턴입니다. 이 일반 표현식은 라인별로 항목 컨텐츠 라인과 일치합니다. 일치하는 텍스트는 지정된 대체 패턴으로 대체됩니다.<br /> <br /> 랜딩 페이지 항목 사전 처리기의 현재 제한 사항에 관해서는 아래 주를 참조하십시오.</td>
  </tr>
  <tr>
   <td> </td>
   <td>대체 패턴</td>
   <td>찾은 일치 항목을 대체하는 패턴입니다. $1, $2 등의 regex 그룹 참조를 사용할 수 있습니다. 또한 이 패턴은 가져오는 동안 실제 값으로 확인되는 {designPath} 같은 키워드를 지원합니다.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>**랜딩 페이지 입력 사전 처리기의 현재 제한 사항:**
>검색 패턴을 변경해야 할 경우에는, felix 속성 편집기를 열고 수동으로 백슬래시 문자를 추가하여 regex metacharacter를 escape해야 합니다. 수동으로 백슬래시 문자를 추가하지 않는 경우, regex는 잘못된 것으로 간주되며 이전 것을 대체하지 않습니다.
>
>예를 들어 기본 구성이
>`/\* *CQ_DESIGN_PATH *\*/ *(['"])`
>
>그리고 당신은 >`CQ_DESIGN_PATH` 검색 패턴에 `VIPURL`이 있는 경우 검색 패턴은 다음과 같아야 합니다.
`/\* *VIPURL *\*/ *(['"])`

## 문제 해결 {#troubleshooting}

디자인 패키지를 가져올 때 이 섹션에 설명된 몇 가지 오류가 발생할 수 있습니다.

### 랜딩 페이지 관련 구성 요소를 사용한 사이드킥 초기화  {#initialization-of-sidekick-with-landing-page-relevant-components}

디자인 패키지에 parsys 구성 요소 마크업이 있을 경우, 가져오기 후 사이드킥은 랜딩 페이지 관련 구성 요소를 보여주기 시작합니다. 랜딩 페이지 내에서 새 구성 요소를 parsys 구성 요소로 드래그 드롭할 수 있습니다. 디자인 모드로 들어가서 새 구성 요소를 사이드킥에 추가할 수도 있습니다.

### 가져오기 중 표시된 오류 메시지 {#error-messages-displayed-during-import}

오류가 발생하면(예: 가져온 패키지가 올바른 zip이 아님) 디자인 가져오기가 패키지를 가져오지 않고 드래그 앤 드롭 상자 바로 위의 페이지 맨 위에 오류 메시지를 표시합니다. 다음은 오류 시나리오의 예입니다. 오류를 수정하면, 업데이트된 zip을 동일한 빈 랜딩 페이지에 다시 가져올 수 있습니다. 오류가 발생하는 다양한 시나리오는 다음과 같습니다.

* 가져온 디자인 패키지는 올바른 zip 아카이브가 아닙니다.
* 가져온 디자인 패키지에는 최상위 수준에 index.html이 없습니다.

### 가져오기 후 표시되는 경고 {#warnings-displayed-after-import}

경고가 표시되는 경우(예: HTML이 패키지 내에 없는 이미지를 참조) 디자인 가져오기는 zip을 가져오지만, 동시에 결과 창에 문제/경고 목록을 표시합니다. 문제 링크를 클릭하면 디자인 패키지 내의 문제를 가리키는 경고 목록이 표시됩니다. 디자인 가져오기에서 포착하고 표시하는 경고가 표시되는 다양한 시나리오는 다음과 같습니다.

* HTML이 패키지 내에 없는 이미지를 참조합니다.
* HTML이 패키지 내에 없는 스크립트를 참조합니다.
* HTML이 패키지 내에 없는 스타일을 참조합니다.

### ZIP 파일의 파일은 AEM에서 어디에 저장됩니까? {#where-are-the-files-of-the-zip-file-being-stored-in-aem}

랜딩 페이지를 가져온 후 디자인 패키지 내의 파일(이미지, css, js, 등)은 디자인 패키지 내에서 는 AEM의 다음 위치에 저장됩니다.

`/etc/designs/default/canvas/content/campaigns/<name of brand>/<name of campaign>/<name of landing page>`

랜딩 페이지가 캠페인 We.Retail 아래에 만들어지고 랜딩 페이지의 이름이 **myBlankLandingPage**&#x200B;이면 Zip 파일이 저장되는 위치는 다음과 같습니다.

`/etc/designs/default/canvas/content/campaigns/geometrixx/myBlankLandingPage`

### 형식이 유지되지 않음 {#formatting-not-preserved}

CSS를 만들 때에는 다음 제한 사항을 알고 있어야 합니다.

텍스트 및(편집 가능) 이미지가 다음과 같은 경우:

```xml
<div class="box">
<p><div data-cq-component="image"><img src="assets/image.jpg" width="115"
height="116" /></div>Some Text </p>
</div>
```

를 사용하여 `box` 클래스에 다음과 같이 CSS를 적용할 수 있습니다.

```xml
.box

{ width: 450px; padding:10px; border: 1px #C5DBE7 solid; margin: 0px auto 0 auto; background-image:url(assets/box.gif); background-repeat:repeat-x,y; font-family:Verdana, Arial, Helvetica, sans-serif; font-size:12px; color:#6D6D6D; }
```

그런 다음 디자인 가져오기에서 `box img`이(가) 사용되면 결과 랜딩 페이지에 형식이 유지되지 않은 것으로 나타납니다. 이 문제를 해결하려면, AEM이 CSS에서 div 태그를 추가하고 그에 따라 코드를 다시 쓴다는 것을 알고 있어야 합니다. 그렇지 않을 경우, 일부 CSS 규칙이 올바르지 않게 됩니다.

```xml
.box img

{ float:right; margin: 0 0 5px 5px; border: 1px #343434 solid; }
```

>[!NOTE]
또한 디자이너는 가져오기 도구에서 **id=cqcanvas** 태그 내의 코드만 인식하며, 그렇지 않으면 디자인이 유지되지 않습니다.

