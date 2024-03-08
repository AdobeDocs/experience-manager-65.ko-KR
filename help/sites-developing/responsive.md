---
title: 웹 페이지를 위한 응답형 디자인
description: 응답형 디자인을 사용하면 동일한 페이지를 여러 방향에서 여러 디바이스에 효과적으로 표시할 수 있습니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
legacypath: /content/docs/en/aem/6-0/develop/mobile/responsive
exl-id: c705710b-a94a-4f4f-affa-ddd4fc6cb0ec
source-git-commit: db0e9d6105484b37e2e21e49bf0f95cef9da2a62
workflow-type: tm+mt
source-wordcount: '5293'
ht-degree: 0%

---

# 웹 페이지를 위한 응답형 디자인{#responsive-design-for-web-pages}

>[!NOTE]
>
>Adobe은 단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: )이 필요한 프로젝트에 SPA Editor 를 사용하는 것을 권장합니다 _반응_). [자세히 알아보기](/help/sites-developing/spa-overview.md).
>

>[!NOTE]
>
>다양한 예는 더 이상 AEM(Adobe Experience Manager)와 함께 제공되지 않으며 We.Retail로 대체된 Geometrixx 샘플 콘텐츠를 기반으로 합니다. 문서 보기 [We.Retail 참조 구현](/help/sites-developing/we-retail.md#we-retail-geometrixx) Geometrixx 다운로드 및 설치 방법에 대해 알아보십시오.

웹 페이지가 표시되는 클라이언트 뷰포트에 맞게 조정되도록 웹 페이지를 디자인합니다. 응답형 디자인을 사용하면 동일한 페이지를 두 방향에서 여러 디바이스에 효과적으로 표시할 수 있습니다. 다음 이미지는 페이지가 뷰포트 크기의 변화에 응답할 수 있는 몇 가지 방법을 보여 줍니다.

* 레이아웃: 작은 뷰포트에는 단일 열 레이아웃을 사용하고 큰 뷰포트에는 다중 열 레이아웃을 사용합니다.
* 텍스트 크기: 큰 뷰포트에서는 텍스트 크기(예: 제목)를 크게 사용합니다.
* 컨텐츠: 작은 장치에 표시할 때 가장 중요한 컨텐츠만 포함합니다.
* 탐색: 다른 페이지에 액세스하기 위해 장치별 도구가 제공됩니다.
* 이미지: 클라이언트 뷰포트에 적합한 이미지 렌디션 제공. 창 크기에 따라 다릅니다.

![chlimage_1-4](assets/chlimage_1-4a.png)

다양한 창 크기 및 방향에 맞는 HTML5 페이지를 생성하는 Adobe Experience Manager(AEM) 애플리케이션을 개발합니다. 예를 들어, 다음 뷰포트 너비 범위는 다양한 디바이스 유형 및 방향에 해당합니다

* 최대 너비 480픽셀(전화, 세로)
* 최대 너비 767픽셀(휴대폰, 가로)
* 768픽셀에서 979픽셀 사이의 폭(태블릿, 세로)
* 980픽셀에서 1199픽셀 사이의 폭(태블릿, 가로)
* 너비 1200픽셀 이상(데스크탑)

반응형 디자인 동작 구현에 대한 자세한 내용은 다음 항목을 참조하십시오.

* [미디어 쿼리](/help/sites-developing/responsive.md#using-media-queries)
* [유체 격자](/help/sites-developing/responsive.md#developing-a-fluid-grid)
* [응용 이미지](/help/sites-developing/responsive.md#using-adaptive-images)

디자인할 때 **[!UICONTROL Sidekick]** 를 클릭하여 다양한 화면 크기로 페이지를 미리 봅니다.

## 개발하기 전에 {#before-you-develop}

웹 페이지를 지원하는 AEM 애플리케이션을 개발하기 전에 몇 가지 디자인 결정을 내려야 합니다. 예를 들어 다음 정보가 있어야 합니다.

* 타깃팅하는 장치입니다.
* 대상 뷰포트 크기.
* 타겟팅된 각 뷰포트 크기에 대한 페이지 레이아웃.

### 애플리케이션 구조 {#application-structure}

일반적인 AEM 애플리케이션 구조는 모든 응답형 디자인 구현을 지원합니다.

* 페이지 구성 요소는 /apps/ 아래에 있습니다.*application_name*/components
* 템플릿은 /apps/ 아래에 있습니다.*application_name*/templates
* 디자인은 /etc/designs 아래에 있습니다.

## 미디어 쿼리 사용 {#using-media-queries}

미디어 쿼리를 사용하면 페이지 렌더링에 CSS 스타일을 선택적으로 사용할 수 있습니다. AEM 개발 도구 및 기능을 사용하면 애플리케이션에서 미디어 쿼리를 효과적이고 효율적으로 구현할 수 있습니다.

W3C 그룹은 [미디어 쿼리](https://www.w3.org/TR/mediaqueries-3/) 이 CSS3 기능 및 구문을 설명하는 권장 사항입니다.

### CSS 파일 만들기 {#creating-the-css-file}

CSS 파일에서 타겟팅하는 장치의 속성을 기반으로 미디어 쿼리를 정의합니다. 다음 구현 전략은 각 미디어 쿼리의 스타일을 관리하는 데 효과적입니다.

* ClientLibraryFolder를 사용하여 페이지가 렌더링될 때 어셈블되는 CSS를 정의합니다.
* 별도의 CSS 파일에서 각 미디어 쿼리와 관련 스타일을 정의합니다. 미디어 쿼리의 장치 기능을 나타내는 파일 이름을 사용하는 것이 유용합니다.
* 별도의 CSS 파일에서 모든 장치에 공통되는 스타일을 정의합니다.
* ClientLibraryFolder의 css.txt 파일에서 어셈블된 CSS 파일에 필요한 CSS 파일 목록을 정렬합니다.

다음 `We.Retail` 미디어 샘플은 이 전략을 사용하여 사이트 디자인의 스타일을 정의합니다. 에서 사용하는 CSS 파일 `We.Retail` 다음 위치에 있음 `*/apps/weretail/clientlibs/clientlib-site/less/grid.less`.

다음 표에는 css 하위 폴더의 파일이 나열되어 있습니다.

<table>
 <tbody>
  <tr>
   <th>파일 이름</th>
   <th>설명</th>
   <th>미디어 쿼리</th>
  </tr>
  <tr>
   <td>style.css</td>
   <td>일반적인 스타일.</td>
   <td>해당 사항 없음</td>
  </tr>
  <tr>
   <td>bootstrap.css</td>
   <td>twitter Bootstrap으로 정의된 일반적인 스타일.</td>
   <td>해당 사항 없음</td>
  </tr>
  <tr>
   <td>responsive-1200px.css</td>
   <td>너비가 1200픽셀 이상인 모든 미디어의 스타일입니다.</td>
   <td><p>@media(최소 너비: 1200픽셀) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-980px-1199px.css</td>
   <td>980픽셀에서 1199픽셀 사이의 미디어 스타일입니다.</td>
   <td><p>@media(최소 너비: 980px) 및 (최대 너비: 1199px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-768px-979px.css</td>
   <td>768픽셀에서 979픽셀 사이의 미디어 스타일입니다. </td>
   <td><p>@media(최소 너비: 768px) 및 (최대 너비: 979px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-767px-max.css</td>
   <td>너비가 768픽셀 미만인 모든 미디어의 스타일입니다.</td>
   <td><p>@media(최대 너비: 767px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-480px.css</td>
   <td>너비가 481픽셀 미만인 모든 미디어의 스타일입니다.</td>
   <td>@media(최대 너비: 480px) {<br /> ...<br /> }</td>
  </tr>
 </tbody>
</table>

의 css.txt 파일 `/etc/designs/weretail/clientlibs` 폴더는 클라이언트 라이브러리 폴더에 포함된 CSS 파일을 나열합니다. 파일의 순서는 스타일 우선 순위를 구현합니다. 장치 크기가 줄어들면 스타일이 더 구체화됩니다.

`#base=css`

```
style.css
 bootstrap.css
```

```
responsive-1200px.css
 responsive-980px-1199px.css
 responsive-768px-979px.css
 responsive-767px-max.css
 responsive-480px.css
```

**팁**: 수사적 파일 이름을 사용하면 타겟팅된 뷰포트 크기를 쉽게 식별할 수 있습니다.

### AEM 페이지에서 미디어 쿼리 사용 {#using-media-queries-with-aem-pages}

페이지 구성 요소의 JSP 스크립트에 클라이언트 라이브러리 폴더를 포함합니다. 이렇게 하면 미디어 쿼리를 포함하고 파일을 참조하는 CSS 파일을 생성하는 데 도움이 됩니다.

```xml
<ui:includeClientLib categories="apps.weretail.all"/>
```

>[!NOTE]
>
>다음 `apps.weretail.all` client library 폴더는 clientlibs 라이브러리를 임베드합니다.

JSP 스크립트는 스타일 시트를 참조하는 다음 HTML 코드를 생성합니다.

```xml
<link rel="stylesheet" href="/etc/designs/weretail/clientlibs-all.css" type="text/css">
<link href="/etc/designs/weretail.css" rel="stylesheet" type="text/css">
```

## 특정 장치에 대한 미리 보기 {#previewing-for-specific-devices}

반응형 디자인의 동작을 테스트할 수 있도록 다양한 뷰포트 크기로 페이지 미리보기 를 참조하십시오. 위치 **[!UICONTROL 미리 보기]** 모드, **[!UICONTROL Sidekick]** 다음 포함: **[!UICONTROL 장치]** 장치를 선택하는 데 사용하는 드롭다운 메뉴. 장치를 선택하면 페이지가 뷰포트 크기에 맞게 변경됩니다.

![chlimage_1-5](assets/chlimage_1-5a.png)

에서 장치 미리 보기를 활성화하려면 **[!UICONTROL Sidekick]**, 페이지 및 를 구성해야 합니다. **[!UICONTROL MobileEmulatorProvider]** 서비스. 다른 페이지 구성은 다음에 나타나는 장치 목록을 제어합니다. **[!UICONTROL 장치]** 목록을 표시합니다.

### 장치 목록 추가 {#adding-the-devices-list}

다음 **[!UICONTROL 장치]** 목록이 다음 위치에 표시됨: **[!UICONTROL Sidekick]** 페이지에 를 렌더링하는 JSP 스크립트가 포함된 경우 **[!UICONTROL 장치]** 목록을 표시합니다. 을(를) 추가하려면 **[!UICONTROL 장치]** 나열 대상 **[!UICONTROL Sidekick]**, 다음을 포함 `/libs/wcm/mobile/components/simulator/simulator.jsp` 스크립트 `head` 섹션에 있는 마지막 항목이 될 필요가 없습니다.

다음을 정의하는 다음 코드를 JSP에 포함 `head` 섹션:

`<cq:include script="/libs/wcm/mobile/components/simulator/simulator.jsp"/>`

예제를 보려면 `/apps/weretail/components/page/head.jsp` CRXDE Lite에 있는 파일입니다.

### 시뮬레이션을 위한 페이지 구성 요소 등록 {#registering-page-components-for-simulation}

Device Simulator가 페이지를 지원하도록 하려면 페이지 구성 요소를 MobileEmulatorProvider 팩토리 서비스에 등록하고 다음을 정의합니다. `mobile.resourceTypes` 속성.

AEM을 사용하여 작업할 때 이러한 서비스에 대한 구성 설정을 관리하는 방법에는 몇 가지가 있습니다. 다음을 참조하십시오. [OSGi 구성](/help/sites-deploying/configuring-osgi.md) 전체 세부 정보.

예를 들어 ` [sling:OsgiConfig](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)` 애플리케이션의 노드:

* 상위 폴더: `/apps/application_name/config`
* 이름: `com.day.cq.wcm.mobile.core.impl.MobileEmulatorProvider-*alias*`

  다음 - `*alias*` mobileEmulatorProvider 서비스가 공장 서비스이므로 접미사가 필요합니다. 이 팩토리에 대해 고유한 별칭을 사용합니다.

* `jcr:primaryType`: `sling:OsgiConfig`

다음 노드 속성을 추가합니다.

* 이름: `mobile.resourceTypes`
* 유형: `String[]`
* 값: 웹 페이지를 렌더링하는 페이지 구성 요소에 대한 경로입니다. 예를 들어 geometrixx-media 앱은 다음 값을 사용합니다.

  ```
  geometrixx-media/components/page
   geometrixx-unlimited/components/pages/page
   geometrixx-unlimited/components/pages/coverpage
   geometrixx-unlimited/components/pages/issue
  ```

### 장치 그룹 지정 {#specifying-the-device-groups}

장치 목록에 나타나는 장치 그룹을 지정하려면 `cq:deviceGroups` 에 대한 속성 `jcr:content` 사이트의 루트 페이지에 있는 노드 속성 값은 장치 그룹 노드에 대한 경로 배열입니다.

장치 그룹 노드는 `/etc/mobile/groups` 폴더를 삭제합니다.

예를 들어 Geometrixx Media 사이트의 루트 페이지는 입니다. `/content/geometrixx-media`. 다음 `/content/geometrixx-media/jcr:content` 노드에는 다음 속성이 포함됩니다.

* 이름: `cq:deviceGroups`
* 유형: `String[]`
* 값: `/etc/mobile/groups/responsive`

도구 콘솔을 사용하여 [장치 그룹 만들기 및 편집](/help/sites-developing/groupfilters.md).

>[!NOTE]
>
>응답형 디자인에 사용하는 장치 그룹의 경우 장치 그룹을 편집하고 일반 탭에서 에뮬레이터 사용 안 함 을 선택합니다. 이 옵션은 응답형 디자인과 관련이 없는 에뮬레이터 회전 메뉴가 표시되지 않도록 합니다.
>

## 적응형 이미지 사용 {#using-adaptive-images}

미디어 쿼리를 사용하여 페이지에 표시할 이미지 리소스를 선택할 수 있습니다. 단, 미디어 쿼리를 사용하여 사용을 조건화하는 모든 리소스는 클라이언트에 다운로드됩니다. 미디어 쿼리는 다운로드한 리소스가 표시되는지 여부만 결정합니다.

이미지와 같은 대규모 리소스의 경우 모든 리소스를 다운로드하는 것은 클라이언트의 데이터 파이프라인을 효율적으로 사용하는 것이 아닙니다. 리소스를 선택적으로 다운로드하려면 미디어 쿼리가 선택을 수행한 후 JavaScript를 사용하여 리소스 요청을 시작합니다.

다음 전략은 미디어 쿼리를 사용하여 선택된 단일 리소스를 로드합니다.

1. 리소스의 각 버전에 대한 DIV 요소를 추가합니다. 리소스의 URI를 속성 값의 값으로 포함합니다. 브라우저가 속성을 리소스로 해석하지 않습니다.
1. 리소스에 적합한 각 DIV 요소에 미디어 쿼리를 추가합니다.
1. 문서가 로드되거나 창 크기가 조정되면 JavaScript 코드는 각 DIV 요소의 미디어 쿼리를 테스트합니다.
1. 쿼리 결과에 따라 포함할 리소스를 결정합니다.
1. 리소스를 참조하는 HTML 요소를 DOM에 삽입합니다.

### JavaScript를 사용하여 미디어 쿼리 평가 {#evaluating-media-queries-using-javascript}

구현 [MediaQueryList 인터페이스](https://drafts.csswg.org/cssom-view/#the-mediaquerylist-interface) W3C가 정의하면 JavaScript를 사용하여 미디어 쿼리를 평가할 수 있습니다. 미디어 쿼리 결과에 논리를 적용하고 현재 창에 대해 타겟팅된 스크립트를 실행할 수 있습니다.

* MediaQueryList 인터페이스를 구현하는 브라우저는 `window.matchMedia()` 함수. 이 함수는 특정 문자열에 대해 미디어 쿼리를 테스트합니다. 이 함수는 `MediaQueryList` 쿼리 결과에 대한 액세스를 제공하는 개체입니다.

* 인터페이스를 구현하지 않는 브라우저의 경우 `matchMedia()` 다중 채우기(예: ) [matchMedia.js](https://github.com/paulirish/matchMedia.js): 자유롭게 사용할 수 있는 JavaScript 라이브러리.

#### 미디어별 리소스 선택 {#selecting-media-specific-resources}

더 W3C [그림 요소](https://html.spec.whatwg.org/multipage/embedded-content.html#the-picture-element) 미디어 쿼리를 사용하여 이미지 요소에 사용할 소스를 결정합니다. 그림 요소는 요소 특성을 사용하여 미디어 쿼리를 이미지 경로와 연결합니다.

자유롭게 이용할 수 있는 [picturefee.js 라이브러리](https://github.com/scottjehl/picturefill) 는 제안된 것과 유사한 기능을 제공합니다. `picture` 요소를 만들고 유사한 전략을 사용합니다. picturefeel.js 라이브러리가 `window.matchMedia` 세트에 대해 정의된 미디어 쿼리를 평가하려면 `div` 요소. 각 `div` 요소는 이미지 소스도 지정합니다. 소스는 의 미디어 쿼리가 `div` 요소 반환 `true`.

다음 `picturefill.js` 라이브러리를 사용하려면 다음 예제와 유사한 HTML 코드가 필요합니다.

```xml
<div data-picture>
    <div data-src='path to default image'></div>
    <div data-src='path to small image'    data-media="(media query for phone)"></div>
    <div data-src='path to medium image'   data-media="(media query for tablet)"></div>
    <div data-src='path to large image'     data-media="(media query for monitor)"></div>
</div>
```

페이지가 렌더링되면 picturebloll.js에서 `img` 요소를 의 마지막 하위 항목으로 사용 `<div data-picture>` 요소:

```xml
<div data-picture>
    <div data-src='path to default image'></div>
    <div data-src='path to small image'    data-media="(media query for phone)"></div>
    <div data-src='path to medium image'   data-media="(media query for tablet)"></div>
    <div data-src='path to large image'     data-media="(media query for monitor)"></div>
    <img src="path to medium image">
</div>
```

AEM 페이지에서 `data-src` 속성은 저장소의 리소스 경로입니다.

### AEM에서 적응형 이미지 구현 {#implementing-adaptive-images-in-aem}

AEM 애플리케이션에서 적응형 이미지를 구현하려면 필요한 JavaScript 라이브러리를 추가하고 페이지에 필요한 HTML 마크업을 포함해야 합니다.

**라이브러리**

다음 JavaScript 라이브러리를 가져와 클라이언트 라이브러리 폴더에 포함합니다.

* [matchMedia.js](https://github.com/paulirish/matchMedia.js) (MediaQueryList 인터페이스를 구현하지 않는 브라우저의 경우)
* [picturefee.js](https://github.com/scottjehl/picturefill)
* jquery.js(다음을 통해 사용 가능 `/etc/clientlibs/granite/jquery` 클라이언트 라이브러리 폴더(범주 = jquery)
* [jquery.debouncedresize.js](https://github.com/louisremi/jquery-smartresize) (창 크기가 조정된 후 한 번 발생하는 jquery 이벤트)

**팁:** 다음을 수행하여 여러 클라이언트 라이브러리 폴더를 자동으로 연결할 수 있습니다 [포함](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries).

**HTML**

picturefill.js 코드에 필요한 div 요소를 생성하는 구성 요소를 만듭니다. AEM 페이지에서 data-src 속성의 값은 저장소의 리소스에 대한 경로입니다. 예를 들어 페이지 구성 요소는 DAM에서 이미지 표현물에 대한 미디어 쿼리와 관련 경로를 하드 코딩할 수 있습니다. 또는 작성자가 이미지 표현물을 선택하거나 런타임 렌더링 옵션을 지정할 수 있는 사용자 지정 이미지 구성 요소를 만듭니다.

다음 예제 HTML은 동일한 이미지의 두 DAM 표현물을 선택합니다.

```xml
<div data-picture>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png'></div>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png/jcr:content/renditions/cq5dam.thumbnail.319.319.png'    data-media="(min-width: 769px)"></div>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png/jcr:content/renditions/cq5dam.thumbnail.140.100.png'   data-media="(min-width: 481px)"></div>
</div>
```

>[!NOTE]
>
>응용 이미지 기초 구성 요소는 응용 이미지를 구현합니다.
>
>* 클라이언트 라이브러리 폴더: `/libs/foundation/components/adaptiveimage/clientlibs`
>* HTML을 생성하는 스크립트: `/libs/foundation/components/adaptiveimage/adaptiveimage.jsp`
>
>다음 섹션에서는 이 구성 요소에 대해 자세히 설명합니다.
>

### AEM의 이미지 렌더링 이해 {#understanding-image-rendering-in-aem}

이미지 렌더링을 사용자 지정하려면 기본 AEM 정적 이미지 렌더링 구현을 이해해야 합니다. AEM은 웹 페이지에 대한 이미지를 렌더링하기 위해 함께 작동하는 이미지 구성 요소와 이미지 렌더링 서블릿을 제공합니다. 이미지 구성 요소가 페이지의 단락 시스템에 포함되면 다음 이벤트 시퀀스가 발생합니다.

1. 작성: 작성자가 이미지 구성 요소를 편집하여 HTML 페이지에 포함할 이미지 파일을 지정합니다. 파일 경로는 이미지 구성 요소 노드의 속성 값으로 저장됩니다.
1. 페이지 요청: 페이지 구성 요소의 JSP가 HTML 코드를 생성합니다. 이미지 구성 요소의 JSP는 img 요소를 생성하여 페이지에 추가합니다.
1. 이미지 요청: 웹 브라우저는 페이지를 로드하고 img 요소의 src 속성에 따라 이미지를 요청합니다.
1. 이미지 렌더링: 이미지 렌더링 서블릿은 웹 브라우저에 이미지를 반환합니다.

![chlimage_1-6](assets/chlimage_1-6a.png)

예를 들어 이미지 구성 요소의 JSP는 다음 HTML 요소를 생성합니다.

`<img title="My Image" alt="My Image" class="cq-dd-image" src="/content/mywebsite/en/_jcr_content/par/image_0.img.jpg/1358372073597.jpg">`

브라우저가 페이지를 로드하면 src 속성의 값을 URL로 사용하여 이미지를 요청합니다. Sling은 URL을 분해합니다.

* 리소스: `/content/mywebsite/en/_jcr_content/par/image_0`
* 파일 이름 확장명: `.jpg`
* 선택기: `img`
* 접미어: `1358372073597.jpg`

다음 `image_0` 노드에 `jcr:resourceType` 값 `foundation/components/image`, 다음에 대한 `sling:resourceSuperType` 값 `foundation/components/parbase`. parbase 구성 요소에는 선택기와 요청 URL의 파일 이름 확장자가 일치하는 img.GET.java 스크립트가 포함됩니다. CQ는 이 스크립트(서블릿)를 사용하여 이미지를 렌더링합니다.

스크립트의 소스 코드를 보려면 CRXDE Lite을 사용하여 `/libs/foundation/components/parbase/img.GET.java`
파일.

## 현재 뷰포트 크기에 대한 이미지 크기 조절 {#scaling-images-for-the-current-viewport-size}

클라이언트 뷰포트의 특성에 따라 런타임에 이미지의 비율을 조정하여 반응형 디자인의 원칙에 부합하는 이미지를 제공합니다. 서블릿 및 작성 구성 요소를 사용하여 정적 이미지 렌더링과 동일한 디자인 패턴을 사용합니다.

구성 요소는 다음 작업을 수행해야 합니다.

* 이미지 리소스의 경로 및 원하는 크기를 속성 값으로 저장합니다.
* 생성 `div` 이미지 렌더링에 대한 미디어 선택기 및 서비스 호출이 포함된 요소입니다.

>[!NOTE]
>
>웹 클라이언트는 matchMedia 및 Picturepe JavaScript 라이브러리(또는 이와 유사한 라이브러리)를 사용하여 미디어 선택기를 평가합니다.
>

이미지 요청을 처리하는 서블릿은 다음 작업을 수행해야 합니다.

* 구성 요소 속성에서 이미지의 경로와 치수를 검색합니다.
* 속성에 따라 이미지 크기를 조정하고 이미지를 반환합니다.

**사용 가능한 솔루션**

AEM은 사용하거나 확장할 수 있는 다음 구현을 설치합니다.

* 미디어 쿼리를 생성하는 적응형 이미지 기초 구성 요소 및 이미지 크기를 조정하는 적응형 이미지 구성 요소 서블릿에 대한 HTTP 요청.
* Geometrixx Commons 패키지는 이미지 해상도를 변경하는 이미지 참조 수정 서블릿 샘플 서블릿을 설치합니다.

### 응용 이미지 구성 요소 이해 {#understanding-the-adaptive-image-component}

적응형 이미지 구성 요소는 디바이스 화면에 따라 크기가 조정된 이미지를 렌더링하기 위해 적응형 이미지 구성 요소 서블릿에 대한 호출을 생성합니다. 구성 요소에는 다음 리소스가 포함됩니다.

* JSP: 미디어 쿼리와 호출을 연결하는 div 요소를 적응형 이미지 구성 요소 서블릿에 추가합니다.
* 클라이언트 라이브러리: clientlibs 폴더는 `cq:ClientLibraryFolder` matchMedia polyfill JavaScript 라이브러리와 수정된 Pictureip JavaScript 라이브러리를 어셈블합니다.
* 편집 대화 상자: `cq:editConfig` 노드는 CQ 기본 이미지 구성 요소를 무시하므로 드롭 대상은 기본 이미지 구성 요소가 아닌 응용 이미지 구성 요소를 만듭니다.

#### DIV 요소 추가 {#adding-the-div-elements}

adaptive-image.jsp 스크립트에는 div 요소 및 미디어 쿼리를 생성하는 다음 코드가 포함됩니다.

```
<div data-picture data-alt='<%= alt %>'>
    <div data-src='<%= path + ".img.320.low." + extension + suffix %>'       data-media="(min-width: 1px)"></div>                                        <%-- Small mobile --%>
    <div data-src='<%= path + ".img.320.medium." + extension + suffix %>'    data-media="(min-width: 320px)"></div>  <%-- Portrait mobile --%>
    <div data-src='<%= path + ".img.480.medium." + extension + suffix %>'    data-media="(min-width: 321px)"></div>  <%-- Landscape mobile --%>
    <div data-src='<%= path + ".img.476.high." + extension + suffix %>'      data-media="(min-width: 481px)"></div>   <%-- Portrait iPad --%>
    <div data-src='<%= path + ".img.620.high." + extension + suffix %>'      data-media="(min-width: 769px)"></div>  <%-- Landscape iPad --%>
    <div data-src='<%= path + ".img.full.high." + extension + suffix %>'     data-media="(min-width: 1025px)"></div> <%-- Desktop --%>

    <%-- Fallback content for non-JS browsers. Same img src as the initial, unqualified source element. --%>
    <noscript>
        <img src='<%= path + ".img.320.low." + extension + suffix %>' alt='<%= alt %>'>
    </noscript>
</div>
```

다음 `path` 변수에는 현재 리소스(응용 이미지 구성 요소 노드)의 경로가 포함됩니다. 이 코드는 일련의 `div` 요소는 다음과 같은 구조를 갖습니다.

`<div data-scr = "*path-to-parent-node*.adaptive-image.adapt.*width*.*quality*.jpg" data-media="*media query*"></div>`

값 `data-scr` 속성은 Sling이 이미지를 렌더링하는 적응형 이미지 구성 요소 서블릿으로 확인되는 URL입니다. data-media 속성에는 클라이언트 속성에 대해 평가되는 미디어 쿼리가 포함됩니다.

다음 HTML 코드는 의 예입니다. `div` jsp가 생성하는 요소:

```xml
<div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.320.low.jpg'></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.320.medium.jpg'    data-media="(min-width: 320px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.480.medium.jpg'    data-media="(min-width: 321px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.476.high.jpg'     data-media="(min-width: 481px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.620.high.jpg'     data-media="(min-width: 769px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.full.high.jpg'     data-media="(min-width: 1025px)"></div>
```

#### 이미지 크기 선택기 변경 {#changing-the-image-size-selectors}

적응형 이미지 구성 요소를 사용자 정의하고 너비 선택기를 변경하는 경우 너비를 지원하도록 적응형 이미지 구성 요소 서블릿 을 구성해야 합니다.

### 적응형 이미지 구성 요소 서블릿 이해 {#understanding-the-adaptive-image-component-servlet}

적응형 이미지 구성 요소 서블릿은 지정된 너비에 따라 JPEG 이미지 크기를 조정하고 JPEG 품질을 설정합니다.

#### 적응형 이미지 구성 요소 서블릿의 인터페이스 {#the-interface-of-the-adaptive-image-component-servlet}

적응형 이미지 구성 요소 서블릿은 기본 Sling 서블릿에 바인딩되며 .jpg, .jpeg, .gif 및 .png 파일 확장명을 지원합니다. 서블릿 선택기가 img입니다.

>[!CAUTION]
>
>애니메이션 .gif 파일은 적응형 변환용 AEM에서 지원되지 않습니다.

따라서 Sling은 다음 형식의 HTTP 요청 URL을 이 서블릿으로 확인합니다.

`*path-to-node*.img.*extension*`

예를 들어 Sling은 URL을 사용하여 HTTP 요청을 전달합니다 `http://localhost:4502/content/geometrixx/adaptiveImage.img.jpg` 적응형 이미지 구성 요소 서블릿을 참조하십시오.

두 개의 추가 선택기는 요청된 이미지 폭과 JPEG 품질을 지정합니다. 다음 예제에서는 너비가 480픽셀이고 중간 품질인 이미지를 요청합니다.

`http://localhost:4502/content/geometrixx/adaptiveImage.adapt.480.MEDIUM.jpg`

**지원되는 이미지 속성**

서블릿은 유한한 수의 이미지 폭과 품질을 허용합니다. 다음 너비는 기본적으로 지원됩니다(픽셀 단위).

* 전체
* 320
* 480
* 476
* 620

전체 값은 배율이 없음을 나타냅니다.

JPEG 품질에 대한 다음 값이 지원됩니다.

* 낮음
* 중간
* 높음

숫자 값은 각각 0.4, 0.82 및 1.0입니다.

**지원되는 기본 폭 변경**

웹 콘솔 사용([http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)) 또는 sling:OsgiConfig 노드를 사용하여 Adobe CQ 적응형 이미지 구성 요소 서블릿의 지원되는 폭을 구성합니다.

AEM 서비스를 구성하는 방법에 대한 자세한 내용은 [OSGi 구성](/help/sites-deploying/configuring-osgi.md).

<table>
 <tbody>
  <tr>
   <th> </th>
   <th>웹 콘솔</th>
   <th>sling:OsgiConfig</th>
  </tr>
  <tr>
   <th>서비스 또는 노드 이름</th>
   <td>구성 탭의 서비스 이름은 Adobe CQ 적응형 이미지 구성 요소 서블릿입니다</td>
   <td>com.day.cq.wcm.foundation.impl. AdaptiveImageComponentServlet</td>
  </tr>
  <tr>
   <th>속성</th>
   <td><p>지원되는 너비</p>
    <ul>
     <li>지원되는 너비를 추가하려면 + 단추를 클릭하고 양의 정수를 입력합니다.</li>
     <li>지원되는 너비를 제거하려면 관련 - 버튼을 클릭합니다.</li>
     <li>지원되는 너비를 수정하려면 필드 값을 편집합니다.</li>
    </ul> </td>
   <td><p>adapt.supported.widths</p>
    <ul>
     <li>속성은 다중 값 문자열 값입니다.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

#### 구현 세부 사항 {#implementation-details}

다음 `com.day.cq.wcm.foundation.impl.AdaptiveImageComponentServlet` 클래스가 다음을 확장합니다. [AbstractImageServlet](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.html) 클래스. AdaptiveImageComponentServlet 소스 코드는 `/libs/foundation/src/impl/src/com/day/cq/wcm/foundation/impl` 폴더를 삭제합니다.

이 클래스는 Felix SCR 주석을 사용하여 서블릿이 연결되는 리소스 유형 및 파일 확장자와 첫 번째 선택기의 이름을 구성합니다.

```java
@Component(metatype = true, label = "Adobe CQ Adaptive Image Component Servlet",
        description = "Render adaptive images in a variety of qualities")
@Service
@Properties(value = {
    @Property(name = "sling.servlet.resourceTypes", value = "foundation/components/adaptiveimage", propertyPrivate = true),
    @Property(name = "sling.servlet.selectors", value = "img", propertyPrivate = true),
    @Property(name = "sling.servlet.extensions", value ={
            "jpg",
            "jpeg",
            "png",
            "gif"
    }, propertyPrivate = true)
})
```

서블릿은 속성 SCR 주석을 사용하여 지원되는 기본 이미지 품질 및 차원을 설정합니다.

```java
@Property(value = {
            "320", // iPhone portrait
            "480", // iPhone landscape
            "476", // iPad portrait
            "620" // iPad landscape
    },
            label = "Supported Widths",
            description = "List of widths this component is permitted to generate.")
```

다음 `AbstractImageServlet` 클래스에서 제공하는 `doGet` http 요청을 처리하는 메서드입니다. 이 메서드는 요청과 연결된 리소스를 결정하고 저장소에서 리소스 속성을 검색하여 [ImageContext](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.ImageContext.html) 개체.

>[!NOTE]
>
>다음 [com.day.cq.commons.DownloadResource](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/DownloadResource.html) 클래스에서 제공하는 `getFileReference method`: 리소스 값을 검색합니다. `fileReference` 속성.

다음 `AdaptiveImageComponentServlet` 클래스는 를 재정의합니다. `createLayer` 메서드를 사용합니다. 이 방법은 이미지 리소스의 경로 및 요청된 이미지 폭을 `ImageContext` 개체. 그런 다음 의 메서드를 호출합니다. `info.geometrixx.commons.impl.AdaptiveImageHelper` 실제 이미지 크기 조절을 수행하는 클래스입니다.

AdaptiveImageComponentServlet 클래스도 writeLayer 메서드를 재정의합니다. 이 메서드는 이미지에 JPEG 품질을 적용합니다.

### 이미지 참조 수정 서블릿(Geometrixx 공통) {#image-reference-modification-servlet-geometrixx-common}

샘플 이미지 참조 수정 서블릿은 웹 페이지에서 이미지 크기를 조정할 img 요소에 대한 크기 속성을 생성합니다.

#### 서블릿 호출 {#calling-the-servlet}

서블릿은에 바인딩되어 있습니다. `cq:page` .jpg 파일 확장명을 지원하는 리소스입니다. 서블릿 선택기는 입니다. `image`. 따라서 Sling은 다음 형식의 HTTP 요청 URL을 이 서블릿으로 확인합니다.

`path-to-page-node.image.jpg`

예를 들어 Sling은 URL을 사용하여 HTTP 요청을 전달합니다 `http://localhost:4502/content/geometrixx/en.image.jpg` 이미지 참조 수정 서블릿을 참조하십시오.

세 개의 추가 선택기는 요청된 이미지 너비, 높이 및 (선택적으로) 품질을 지정합니다. 다음 예제에서는 폭 770픽셀, 높이 360픽셀, 중간 품질의 이미지를 요청합니다.

`http://localhost:4502/content/geometrixx/en.image.770.360.MEDIUM.jpg`

**지원되는 이미지 속성**

서블릿은 한정된 수의 이미지 차원과 품질 값을 허용합니다.

기본적으로 다음 값이 지원됩니다(widthxheight).

* 256x192
* 370x150
* 480x200
* 127x127
* 770x360
* 620x290
* 480x225
* 320x150
* 375x175
* 303x142
* 1170x400
* 940x340
* 770x300
* 480x190

이미지 품질에 대해 다음 값이 지원됩니다.

* 낮음
* 중간
* 높음

AEM을 사용하여 작업할 때 이러한 서비스에 대한 구성 설정을 관리하는 방법에는 몇 가지가 있습니다. 다음을 참조하십시오. [OSGi 구성](/help/sites-deploying/configuring-osgi.md) 전체 세부 정보.

#### 이미지 리소스 지정 {#specifying-the-image-resource}

이미지 경로, 치수 및 품질 값은 저장소의 노드 속성으로 저장해야 합니다.

* 노드 이름은 입니다. `image`.
* 상위 노드는 `jcr:content` 노드의 노드 `cq:page` 리소스.

* 이미지 경로는 라는 속성의 값으로 저장됩니다. `fileReference`.

페이지를 작성할 때 다음을 사용합니다. **Sidekick** 이미지를 지정하고 `image` 페이지 속성에 대한 노드:

1. 위치 **Sidekick**&#x200B;를 클릭하고 **페이지** 탭을 클릭한 다음 **페이지 속성**.
1. 다음을 클릭합니다. **이미지** 을 탭하고 이미지를 지정합니다.
1. **확인**&#x200B;을 클릭합니다.

#### 구현 세부 사항 {#implementation-details-1}

info.geometrixx.commons.impl.servlets.ImageReferenceModificationServlet 클래스는 [AbstractImageServlet](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.html) 클래스. cq-geometrixx-commons-pkg 패키지가 설치되어 있는 경우 ImageReferenceModificationServlet 소스 코드는 `/apps/geometrixx-commons/src/core/src/main/java/info/geometrixx/commons/impl/servlets` 폴더를 삭제합니다.

이 클래스는 Felix SCR 주석을 사용하여 서블릿이 연결되는 리소스 유형 및 파일 확장자와 첫 번째 선택기의 이름을 구성합니다.

```java
@Component(metatype = true, label = "Adobe CQ Image Reference Modification Servlet",
        description = "Render the image associated with a page in a variety of dimensions and qualities")
@Service
@Properties(value = {
    @Property(name = "sling.servlet.resourceTypes", value = NameConstants.NT_PAGE, propertyPrivate = true),
    @Property(name = "sling.servlet.selectors", value = "image", propertyPrivate = true),
    @Property(name = "sling.servlet.extensions", value = "jpg", propertyPrivate = true)
})
```

서블릿은 속성 SCR 주석을 사용하여 지원되는 기본 이미지 품질 및 차원을 설정합니다.

```java
@Property(label = "Image Quality",
            description = "Quality must be a double between 0.0 and 1.0", value = "0.82")
@Property(value = {
                "256x192", // Category page article list images
                "370x150", // "Most popular" desktop & iPad & carousel min-width: 1px
                "480x200", // "Most popular" phone
                "127x127", // article summary phone square images
                "770x360", // article summary, desktop
                "620x290", // article summary, tablet
                "480x225", // article summary, phone (landscape)
                "320x150", // article summary, phone (portrait) and fallback
                "375x175", // 2-column article summary, desktop
                "303x142", // 2-column article summary, tablet
                "1170x400", // carousel, full
                "940x340",  // carousel min-width: 980px
                "770x300",  // carousel min-width: 768px
                "480x190"   // carousel min-width: 480px
            },
            label = "Supported Resolutions",
            description = "List of resolutions this component is permitted to generate.")
```

다음 `AbstractImageServlet` 클래스에서 제공하는 `doGet` http 요청을 처리하는 메서드입니다. 이 메서드는 호출과 연결된 리소스를 결정하고 저장소에서 리소스 속성을 검색하여 [ImageContext](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.ImageContext.html) 개체.

다음 `ImageReferenceModificationServlet` 클래스는 를 재정의합니다. `createLayer` 렌더링할 이미지 리소스를 결정하는 논리를 메서드 및 구현합니다. 메서드는 페이지의 하위 노드를 검색합니다. `jcr:content` 노드 이름: `image`. An [이미지](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/foundation/Image.html) 개체가 다음에서 만들어집니다. `image` 노드 및 `getFileReference` 메서드는 이미지 파일의 경로를 `fileReference` 이미지 노드의 속성입니다.

>[!NOTE]
>다음 [com.day.cq.commons.DownloadResource](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/DownloadResource.html) 클래스는 getFileReferencemethod를 제공합니다.
>

## 유체 그리드 개발 {#developing-a-fluid-grid}

AEM을 사용하면 유체 그리드를 효율적이고 효과적으로 구현할 수 있습니다. 이 페이지에서는 유체 그리드나 기존 그리드 구현(예: [Bootstrap](https://github.com/topics/twitter-bootstrap?l=css))을 클릭하여 AEM 애플리케이션에 로그인합니다.

유동 격자에 익숙하지 않은 경우 다음을 참조하십시오. [Fluid Grid 소개](/help/sites-developing/responsive.md#developing-a-fluid-grid) 섹션에 있는 마지막 항목이 될 필요가 없습니다. 이 소개에서는 유체 격자의 개요와 유체 격자를 설계하기 위한 지침을 제공합니다.

### 페이지 구성 요소를 사용하여 그리드 정의 {#defining-the-grid-using-a-page-component}

페이지 구성 요소를 사용하여 페이지의 콘텐츠 블록을 정의하는 HTML 요소를 생성합니다. 페이지가 참조하는 ClientLibraryFolder는 콘텐츠 블록의 레이아웃을 제어하는 CSS를 제공합니다.

* 페이지 구성 요소: 콘텐츠 블록의 행을 나타내는 div 요소를 추가합니다. 콘텐츠 블록을 나타내는 div 요소에는 작성자가 콘텐츠를 추가하는 parsys 구성 요소가 포함됩니다.
* 클라이언트 라이브러리 폴더: div 요소의 미디어 쿼리 및 스타일이 포함된 CSS 파일을 제공합니다.

예를 들어 샘플 geometrixx-media 애플리케이션에는 media-home 구성 요소가 포함되어 있습니다. 이 페이지 구성 요소는 두 개의 스크립트를 삽입하여 두 개의 스크립트를 생성합니다 `div` 클래스의 요소 `row-fluid`:

* 첫 번째 행에는 `div` 클래스의 요소 `span12` (컨텐츠는 12개 열에 걸쳐 있습니다.) 다음 `div` 요소에 parsys 구성 요소가 포함되어 있습니다.

* 두 번째 행에는 두 개의 행이 포함됩니다 `div` 요소, 클래스 중 하나 `span8` 그리고 계층의 다른 사람 `span4`. 각 `div` 요소는 parsys 구성 요소를 포함합니다.

```xml
<div class="page-content">
    <div class="row-fluid">
        <div class="span12">
            <cq:include path="grid-12-par" resourceType="foundation/components/parsys" />
        </div>
    </div>
    <div class="row-fluid">
        <div class="span8">
            <cq:include path="grid-8-par" resourceType="foundation/components/parsys" />
        </div>
        <div class="span4">
            <cq:include path="grid-4-par" resourceType="foundation/components/parsys" />
        </div>
    </div>
</div>
```

>[!NOTE]
>
>구성 요소에 여러 개가 포함된 경우 `cq:include` parsys 구성 요소를 참조하는 요소, 각각 `path` 속성에는 다른 값이 있어야 합니다.
>

#### 페이지 구성 요소 격자 크기 조절 {#scaling-the-page-component-grid}

geometrixx-media 페이지 구성 요소와 연결된 디자인(`/etc/designs/geometrixx-media`)에는 `clientlibs` ClientLibraryFolder. 이 ClientLibraryFolder는 `row-fluid` 클래스, `span*` 클래스 및 `span*` 하위 클래스 `row-fluid` 클래스입니다. 미디어 쿼리를 사용하면 다양한 뷰포트 크기에 대해 스타일을 다시 정의할 수 있습니다.

다음 예제 CSS는 이러한 스타일의 하위 집합입니다. 이 하위 세트는 다음에 중점을 둡니다. `span12`, `span8`, 및 `span4` 클래스 및 두 뷰포트 크기에 대한 미디어 쿼리입니다. CSS의 다음 특성에 주목하십시오.

* 다음 `.span` 스타일은 절대 숫자를 사용하여 요소 폭을 정의합니다.
* 다음 `.row-fluid .span*` 스타일은 요소 폭을 상위의 백분율로 정의합니다. 백분율은 절대 너비로 계산됩니다.
* 더 큰 뷰포트에 대한 미디어 쿼리는 더 큰 절대 폭을 할당합니다.

>[!NOTE]
>
>Geometrixx Media 샘플은 [Bootstrap](https://getbootstrap.com/2.0.2/) JavaScript 프레임워크를 Fluid Grid 구현에 포함합니다. Bootstrap 프레임워크는 bootstrap.css 파일을 제공합니다.

```xml
/* default styles (no media queries) */
 .span12 { width: 940px }
 .span8 { width: 620px }
 .span4 { width: 300px }
 .row-fluid .span12 { width: 100% }
 .row-fluid .span8 { width: 65.95744680851064% }
 .row-fluid .span4 { width: 31.914893617021278% }

@media (min-width: 768px) and (max-width: 979px) {
 .span12 { width: 724px; }
 .span8 {     width: 476px; }
 .span4 {     width: 228px; }
 .row-fluid .span12 {     width: 100%;}
 .row-fluid .span8 {     width: 65.74585635359117%; }
 .row-fluid .span4 {     width: 31.491712707182323%; }
}

@media (min-width: 1200px) {
 .span12 { width: 1170px }
 .span8 { width: 770px }
 .span4 { width: 370px }
 .row-fluid .span12 { width: 100% }
 .row-fluid .span8 { width: 65.81196581196582% }
 .row-fluid .span4 { width: 31.623931623931625% }
}
```

#### 페이지 구성 요소 그리드에서 컨텐츠 위치 변경 {#repositioning-content-in-the-page-component-grid}

샘플 Geometrixx Media 애플리케이션의 페이지는 콘텐츠 블록의 행을 넓은 뷰포트에 수평으로 분배합니다. 더 작은 뷰포트에서는 동일한 블록이 수직으로 분산됩니다. 다음 예제 CSS는 미디어 홈 페이지 구성 요소가 생성하는 HTML 코드에 대해 이 동작을 구현하는 스타일을 보여 줍니다.

* media-welcome 페이지의 기본 CSS는 `float:left` 스타일 `span*` 내에 있는 클래스 `row-fluid` 클래스입니다.

* 작은 뷰포트에 대한 미디어 쿼리는 `float:none` 동일한 클래스에 대해 스타일을 지정합니다.

```xml
/* default styles (no media queries) */
    .row-fluid [class*="span"] {
        width: 100%;
        float: left;
}

@media (max-width: 767px) {
    [class*="span"], .row-fluid [class*="span"] {
        float: none;
        width: 100%;
    }
}
```

#### 페이지 구성 요소 모듈화 {#tip-modularize-your-page-components}

코드를 효율적으로 사용할 수 있도록 구성 요소를 모듈화합니다. 사이트에서는 시작 페이지, 문서 페이지 또는 제품 페이지와 같은 몇 가지 유형의 페이지를 사용할 수 있습니다. 각 페이지 유형에는 서로 다른 유형의 콘텐츠가 포함되어 있으며 서로 다른 레이아웃을 사용할 수 있습니다. 그러나 각 레이아웃의 특정 요소가 여러 페이지에서 공통되는 경우 레이아웃의 해당 부분을 구현하는 코드를 다시 사용할 수 있습니다.

**페이지 구성 요소 오버레이 사용**

다음과 같이 페이지의 다양한 부분을 생성하는 스크립트를 제공하는 기본 페이지 구성 요소를 만듭니다. `head` 및 `body` 섹션 및 `header`, `content`, 및 `footer` 본문 내의 섹션입니다.

기본 페이지 구성 요소를 로 사용하는 다른 페이지 구성 요소를 만듭니다. `cq:resourceSuperType`. 이러한 구성 요소에는 필요에 따라 기본 페이지의 스크립트를 재정의하는 스크립트가 포함됩니다.

예를 들어, goemetrixx-media 애플리케이션에는 페이지 구성 요소 ( `sling:resourceSuperType` 는 기본 페이지 구성 요소입니다. 여러 하위 구성 요소(예: 문서, 카테고리 및 media-home)는 이 페이지 구성 요소를 로 사용합니다. `sling:resourceSuperType`. 각 하위 구성 요소에는 페이지 구성 요소의 content.jsp 파일을 무시하는 content.jsp 파일이 포함됩니다.

**스크립트 재사용**

여러 페이지 구성 요소에 대해 공통적인 행 및 열 조합을 생성하는 여러 JSP 스크립트를 생성합니다. 예를 들어 `content.jsp` 문서 스크립트 및 media-home 구성 요소는 모두 `8x4col.jsp` 스크립트.

**타깃팅된 뷰포트 크기별로 CSS 스타일 구성**

서로 다른 뷰포트 크기에 대한 CSS 스타일과 미디어 쿼리를 별도의 파일에 포함합니다. 클라이언트 라이브러리 폴더를 사용하여 연결합니다.

### 페이지 그리드에 구성 요소 삽입 {#inserting-components-into-the-page-grid}

구성 요소가 단일 콘텐츠 블록을 생성할 때 일반적으로 페이지 구성 요소가 설정하는 그리드는 콘텐츠의 배치를 제어합니다.

작성자는 콘텐츠 블록을 다양한 크기 및 상대적 위치로 렌더링할 수 있습니다. 컨텐츠 텍스트는 다른 컨텐츠 블록을 참조하는 데 상대 방향을 사용하지 않아야 합니다.

필요한 경우 구성 요소는 생성하는 HTML 코드에 필요한 CSS 또는 JavaScript 라이브러리를 제공해야 합니다. CSS 및 JS 파일이 생성되도록 구성 요소 내에 클라이언트 라이브러리 폴더를 사용하십시오. 파일을 노출하려면 [종속성 만들기 또는 라이브러리 포함](/help/sites-developing/clientlibs.md#creating-client-library-folders) /etc 폴더 아래의 다른 클라이언트 라이브러리 폴더에서

**하위 그리드**

구성 요소에 여러 개의 콘텐츠 블록이 포함된 경우 행 내에 콘텐츠 블록을 추가하여 페이지의 하위 그리드를 설정합니다.

* div 요소를 행 및 콘텐츠 블록으로 표현할 수 있도록 포함 페이지 구성 요소와 동일한 클래스 이름을 사용합니다.
* 페이지 디자인의 CSS가 구현하는 동작을 무시하려면 행 div 요소에 두 번째 클래스 이름을 사용하고 클라이언트 라이브러리 폴더에 관련 CSS를 제공합니다.

예를 들어 `/apps/geometrixx-media/components/2-col-article-summary` 구성 요소는 두 개의 콘텐츠 열을 생성합니다. 이 HTML이 생성하는 구조는 다음과 같습니다.

```xml
<div class="row-fluid mutli-col-article-summary">
    <div class="span6">
        <article>
            <div class="article-summary-image">...</div>
            <div class="social-header">...</div>
            <div class="article-summary-description">...</div>
            <div class="social">...</div>
        </article>
    </div>
</div>
```

다음 `.row-fluid .span6` 페이지 CSS의 선택기는 `div` 이 HTML에서 동일한 클래스 및 구조의 요소입니다. 그러나 구성 요소에는 /apps/geometrixx-media/components/2-col-article-summary/clientlibs 클라이언트 라이브러리 폴더도 포함됩니다.

* CSS는 페이지 구성 요소와 동일한 미디어 쿼리를 사용하여 동일한 개별 페이지 너비로 레이아웃에 변경 사항을 설정합니다.
* 선택기는 `multi-col-article-summary` 행의 클래스 `div` 페이지의 동작을 재정의하는 요소 `row-fluid` 클래스.

예를 들어, 다음 스타일은 `/apps/geometrixx-media/components/2-col-article-summary/clientlibs/css/responsive-480px.css` 파일:

```xml
@media (max-width: 480px) {
    .mutli-col-article-summary .article-summary-image {
        float: left;
        width: 127px;
    }
    .mutli-col-article-summary .article-summary-description {
        width: auto;
        margin-left: 127px;
    }
    .mutli-col-article-summary .article-summary-description h4 {
        padding-left: 10px;
    }
    .mutli-col-article-summary .article-summary-text {
        margin-left: 127px;
        min-height: 122px;
        top: 0;
    }
}
```

## 유동 격자 소개 {#introduction-to-fluid-grids}

유동 격자를 사용하면 페이지 레이아웃을 클라이언트 뷰포트의 크기에 맞게 조정할 수 있습니다. 그리드는 페이지에 콘텐츠 블록을 배치하는 논리적 열과 행으로 구성됩니다.

* 열은 콘텐츠 블록의 가로 위치 및 너비를 결정합니다.
* 행은 콘텐츠 블록의 상대적인 세로 위치를 결정합니다.

HTML5 기술을 사용하여 그리드를 구현하고 이를 조작하여 페이지 레이아웃을 다양한 뷰포트 크기로 조정할 수 있습니다.

* HTML `div` 요소에는 일부 열에 걸쳐 있는 콘텐츠 블록이 포함되어 있습니다.
* 이러한 div 요소 중 하나 이상은 공통 상위 div 요소를 공유할 때 행을 구성합니다.

### 개별 폭 사용 {#using-discrete-widths}

타겟팅하는 각 뷰포트 폭 범위에 대해 정적 페이지 폭과 일정한 폭의 콘텐츠 블록을 사용합니다. 브라우저 창의 크기를 수동으로 조정할 때, 컨텐츠 크기 변경은 개별 창 너비(중단점이라고도 함)에서 발생합니다. 따라서, 페이지 디자인은 더욱 밀착되어, 사용자 경험을 최대화한다.

#### 격자 크기 조절 {#scaling-the-grid}

그리드를 사용하여 콘텐츠 블록의 크기를 다른 뷰포트 크기에 맞게 조정합니다. 콘텐츠 블록은 특정 수의 열에 걸쳐 있습니다. 서로 다른 뷰포트 크기에 맞게 열 너비가 증가 또는 감소하면 콘텐츠 블록의 너비도 그에 따라 증가 또는 감소합니다. 크기를 조정하면 콘텐츠 블록의 병렬 배치를 수용할 수 있을 만큼 넓은 대형 및 중간 크기의 뷰포트를 모두 지원할 수 있습니다.

![크기가 다른 두 격자보다 작은 두 격자선의 이미지입니다.](do-not-localize/chlimage_1-1a.png)

#### 그리드에서 컨텐츠 위치 변경 {#repositioning-content-in-the-grid}

콘텐츠 블록의 크기는 최소 너비에 의해 제한될 수 있으며, 이를 초과하는 스케일링은 더 이상 효과적이지 않다. 작은 뷰포트의 경우 격자를 사용하여 콘텐츠 블록을 가로가 아닌 세로로 배포할 수 있습니다.

![위치가 다른 격자보다 작은 두 격자선 이미지](do-not-localize/chlimage_1-2a.png)

### 격자 디자인 {#designing-the-grid}

페이지에 콘텐츠 블록을 배치해야 하는 열과 행을 결정합니다. 페이지 레이아웃은 격자에 걸쳐 있는 열과 행의 수를 결정합니다.

**열 수**

모든 뷰포트 크기에 대해 모든 레이아웃에서 컨텐츠 블록을 수평으로 배치하기에 충분한 열을 포함합니다. 향후 페이지 디자인을 수용할 수 있도록 현재 필요한 것보다 더 많은 열을 사용하십시오.

**행 컨텐츠**

행을 사용하여 콘텐츠 블록의 세로 위치를 제어합니다. 동일한 행을 공유하는 콘텐츠 블록을 결정합니다.

* 레이아웃에서 가로 방향으로 서로 옆에 있는 콘텐츠 블록은 같은 행에 있습니다.
* 가로(더 넓은 뷰포트)와 세로(더 작은 뷰포트)로 서로 옆에 있는 콘텐츠 블록은 같은 행에 있습니다.

### 그리드 구현 {#grid-implementations}

페이지에서 콘텐츠 블록의 레이아웃을 제어할 수 있도록 CSS 클래스와 스타일을 만듭니다. 페이지 디자인은 종종 뷰포트 내의 콘텐츠 블록의 상대적 크기와 위치를 기반으로 합니다. 뷰포트는 콘텐츠 블록의 실제 크기를 결정합니다. CSS는 상대 크기와 절대 크기를 고려해야 합니다. 다음 세 가지 유형의 CSS 클래스를 사용하여 유동 격자를 구현할 수 있습니다.

* a에 대한 클래스 `div` 모든 행의 컨테이너인 요소입니다. 이 클래스는 격자의 절대 너비를 설정합니다.
* 클래스 `div` 행을 나타내는 요소입니다. 이 클래스는 포함된 콘텐츠 블록의 가로 또는 세로 위치를 제어합니다.
* 클래스 `div` 서로 다른 너비의 콘텐츠 블록을 나타내는 요소입니다. 너비는 상위(행)의 백분율로 표시됩니다.

타깃팅된 뷰포트 폭(및 관련 미디어 쿼리)은 페이지 레이아웃에 사용되는 개별 폭을 분리합니다.

#### 콘텐츠 블록의 너비 {#widths-of-content-blocks}

일반적으로 `width` 콘텐츠 블록 클래스의 스타일은 페이지 및 그리드의 다음 특성을 기반으로 합니다.

* 타겟팅된 각 뷰포트 크기에 사용할 절대 페이지 너비입니다. 알려진 값.
* 각 페이지 너비에 대한 그리드 열의 절대 너비입니다. 이 값을 결정합니다.
* 각 열의 상대적 너비(총 페이지 너비의 백분율)입니다. 이러한 값을 계산합니다.

CSS에는 다음 구조를 사용하는 일련의 미디어 쿼리가 포함되어 있습니다.

```xml
@media(query_for_targeted_viewport){

  .class_for_container{ width:absolute_page_width }
  .class_for_row { width:100%}

  /* several selectors for content blocks   */
  .class_for_content_block1 { width:absolute_block_width1 }
  .class_for_content_block2 { width:absolute_block_width2 }
  ...

  /* several selectors for content blocks inside rows */
  .class_for_row .class_for_content_block1 { width:relative_block_width1 }
  .class_for_row .class_for_content_block2 { width:relative_block_width2 }
  ...
}
```

페이지의 요소 클래스 및 CSS 스타일을 개발하기 위한 시작점으로 다음 알고리즘을 사용하십시오.

1. 모든 행을 포함하는 div 요소에 대한 클래스 이름을 정의합니다(예: ). `content.`
1. 다음과 같이 행을 나타내는 div 요소에 대한 CSS 클래스를 정의합니다. `row-fluid`.
1. 콘텐츠 블록 요소에 대한 클래스 이름을 정의합니다. 열 범위 측면에서 가능한 모든 너비에 클래스가 필요합니다. 예를 들어 `span3` 클래스 `div` 3개 열에 걸쳐 있는 요소 `span4` 4개 열 범위 클래스. 격자에 열이 있는 수만큼 클래스를 정의합니다.

1. 타겟팅하는 각 뷰포트 크기에 대해 해당 미디어 쿼리를 CSS 파일에 추가합니다. 각 미디어 쿼리에 다음 항목을 추가합니다.

   * 에 대한 선택기 `content` 클래스(예: ) `.content{}`.
   * 각 span 클래스에 대한 선택기(예: ) `.span3{ }`.
   * 에 대한 선택기 `row-fluid` 클래스(예: ) `.row-fluid{ }`
   * 행-유동 클래스 내부에 있는 span 클래스의 선택기 `.row-fluid span3 { }`.

1. 각 선택기의 폭 스타일 추가:

   1. 너비 설정 `content` 페이지의 절대 크기로 선택기(예: ) `width:480px`.
   1. 모든 행 유체 선택기의 너비를 100%로 설정합니다.
   1. 모든 스팬 선택기의 너비를 콘텐츠 블록의 절대 너비로 설정합니다. 작은 격자는 동일한 너비의 균일하게 분포된 열을 사용합니다. `(absolute width of page)/(number of columns)`.
   1. 너비 설정 `.row-fluid .span` 선택기를 총 너비에 대한 백분율로 표시합니다. 다음을 사용하여 이 너비 계산 `(absolute span width)/(absolute page width)*100` 공식.

#### 행에서 콘텐츠 블록 위치 지정 {#positioning-content-blocks-in-rows}

의 부동 스타일 사용 `.row-fluid` 클래스를 사용하여 한 행에 있는 콘텐츠 블록을 가로로 배열할지 세로로 배열할지 여부를 제어할 수 있습니다.

* 다음 `float:left` 또는 `float:right` 스타일은 하위 요소(콘텐츠 블록)의 수평 배포를 유발합니다.

* 다음 `float:none` 스타일은 하위 요소의 세로 분포를 발생시킵니다.

에 스타일 추가 `.row-fluid` 각 미디어 쿼리 내의 선택기입니다. 해당 미디어 쿼리에 사용하는 페이지 레이아웃에 따라 값을 설정합니다. 예를 들어 다음 다이어그램은 넓은 뷰포트의 경우 가로, 좁은 뷰포트의 경우 세로 방향으로 컨텐츠를 배포하는 행을 보여 줍니다.

![행에 있는 콘텐츠 블록의 두 이미지이며, 행을 나타내는 두 번째 이미지입니다.](do-not-localize/chlimage_1-3a.png)

다음 CSS는 이 동작을 구현할 수 있습니다.

```xml
@media (min-width: 768px) and (max-width: 979px) {
   .row-fluid {
       width:100%;
       float:left
   }
}

@media (max-width:480px){
    .row-fluid {
       width:100%;
       float:none
   }
}
```

#### 콘텐츠 블록에 클래스 할당 {#assigning-classes-to-content-blocks}

타깃팅하는 각 뷰포트 크기의 페이지 레이아웃에 대해 각 콘텐츠 블록이 걸쳐 있는 열의 수를 결정합니다. 그런 다음 해당 콘텐츠 블록의 div 요소에 사용할 클래스를 결정합니다.

div 클래스를 설정한 경우 AEM 애플리케이션을 사용하여 그리드를 구현할 수 있습니다.
