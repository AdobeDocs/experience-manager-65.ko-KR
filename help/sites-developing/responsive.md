---
title: 웹 페이지를 위한 반응형 디자인
seo-title: 웹 페이지를 위한 반응형 디자인
description: 반응형 디자인을 사용하면 여러 장치에서 여러 방향으로 동일한 페이지를 효과적으로 표시할 수 있습니다
seo-description: 반응형 디자인을 사용하면 여러 장치에서 여러 방향으로 동일한 페이지를 효과적으로 표시할 수 있습니다
uuid: 3d324557-e7ff-4c82-920f-9b5a906925e8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: 532544b0-1932-419a-b6bd-ecf57a926fef
legacypath: /content/docs/en/aem/6-0/develop/mobile/responsive
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '5339'
ht-degree: 1%

---


# 웹 페이지를 위한 응답형 디자인{#responsive-design-for-web-pages}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: _Responsive_)이 필요한 프로젝트에는 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).


웹 페이지가 표시되는 클라이언트 뷰포트에 맞게 디자인할 수 있습니다. 반응형 디자인을 사용하면 두 방향 모두에서 여러 장치에서 동일한 페이지를 효과적으로 표시할 수 있습니다. 다음 이미지는 페이지가 뷰포트 크기 변화에 응답하는 몇 가지 방법을 보여 줍니다.

* 레이아웃:단일 열 레이아웃을 사용하여 작은 뷰포트를 표시하고 여러 열로 구성된 레이아웃을 사용하여 큰 뷰포트를 볼 수 있습니다.
* 텍스트 크기:더 큰 뷰포트에서 더 큰 텍스트 크기(해당하는 경우 제목 등)를 사용합니다.
* 컨텐츠:작은 장치에 표시할 때 가장 중요한 컨텐츠만 포함합니다.
* 탐색:장치별 도구는 다른 페이지에 액세스하기 위해 제공됩니다.
* 이미지:클라이언트 뷰포트에 적합한 이미지 변환 제공 를 참조하십시오.

![chlimage_1-4](assets/chlimage_1-4a.png)

다양한 창 크기 및 방향에 맞게 HTML5 페이지를 생성하는 Adobe Experience Manager(AEM) 애플리케이션을 개발할 수 있습니다. 예를 들어, 다음 범위의 뷰포트 너비는 다양한 장치 유형 및 방향에 해당합니다

* 최대 너비 480픽셀(전화, 세로)
* 최대 너비: 767픽셀(휴대폰, 가로)
* 너비(768픽셀과 979픽셀)(태블릿, 세로)
* 너비: 980픽셀 ~ 1199픽셀(태블릿, 가로)
* 너비: 1200px 이상(데스크탑)

반응형 디자인 비헤이비어의 구현에 대한 자세한 내용은 다음 항목을 참조하십시오.

* [미디어 쿼리](/help/sites-developing/responsive.md#using-media-queries)
* [유동 격자](/help/sites-developing/responsive.md#developing-a-fluid-grid)
* [적응형 이미지](/help/sites-developing/responsive.md#using-adaptive-images)

디자인할 때 **[!UICONTROL 사이드킥을 사용하여 다양한 화면 크기에 맞게 페이지를 미리 봅니다.]**

## {#before-you-develop} 개발 전

웹 페이지를 지원하는 AEM 애플리케이션을 개발하기 전에 몇 가지 디자인 결정을 내려야 합니다. 예를 들어 다음 정보가 필요합니다.

* 타깃팅하는 장치.
* 대상 뷰포트 크기입니다.
* 타깃팅된 각 뷰포트 크기에 대한 페이지 레이아웃입니다.

### 응용 프로그램 구조 {#application-structure}

일반적인 AEM 애플리케이션 구조는 모든 반응형 디자인 구현을 지원합니다.

* 페이지 구성 요소는 /apps/*application_name*/components 아래에 있습니다.
* 템플릿은 /apps/*application_name*/templates 아래에 상주합니다.
* 디자인은 /etc/designs 아래에 상주합니다.

## 미디어 쿼리 사용 {#using-media-queries}

미디어 쿼리를 사용하면 페이지 렌더링을 위해 CSS 스타일을 선택적으로 사용할 수 있습니다. AEM 개발 툴과 기능을 사용하면 애플리케이션에서 미디어 쿼리를 효과적이고 효율적으로 구현할 수 있습니다.

W3C 그룹은 이 CSS3 기능 및 구문을 설명하는 [미디어 쿼리](https://www.w3.org/TR/css3-mediaqueries/) 권장 사항을 제공합니다.

### CSS 파일 {#creating-the-css-file} 만들기

CSS 파일에서 타깃팅하는 장치의 속성을 기반으로 미디어 쿼리를 정의합니다. 다음 구현 전략은 각 미디어 쿼리에 대한 스타일을 관리하는 데 효과적입니다.

* ClientLibraryFolder를 사용하여 페이지가 렌더링될 때 어셈블되는 CSS를 정의합니다.
* 각 미디어 쿼리 및 관련 스타일을 별도의 CSS 파일로 정의할 수 있습니다. 미디어 쿼리의 장치 기능을 나타내는 파일 이름을 사용하는 것이 유용합니다.
* 별도의 CSS 파일에서 모든 디바이스에서 공통으로 사용되는 스타일을 정의할 수 있습니다.
* ClientLibraryFolder의 css.txt 파일에서 어셈블된 CSS 파일에 필요한 CSS 파일 목록을 정렬합니다.

We.Retail 미디어 샘플에서는 이 전략을 사용하여 사이트 디자인에서 스타일을 정의합니다. We.Retail에서 사용하는 CSS 파일은 `*/apps/weretail/clientlibs/clientlib-site/less/grid.less`에 있습니다.

다음 표에는 css 하위 폴더의 파일이 나열됩니다.

<table>
 <tbody>
  <tr>
   <th>파일 이름</th>
   <th>설명</th>
   <th>미디어 쿼리</th>
  </tr>
  <tr>
   <td>style.css</td>
   <td>공통 스타일.</td>
   <td>N/A</td>
  </tr>
  <tr>
   <td>bootstrap.css</td>
   <td>Twitter Bootstrap에 의해 정의된 일반 스타일.</td>
   <td>해당 없음</td>
  </tr>
  <tr>
   <td>responsive-1200px.css</td>
   <td>가로 1200픽셀 이상의 모든 미디어에 대한 스타일</td>
   <td><p>@media(최소 너비:1200px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-980px-1199px.css</td>
   <td>980픽셀과 1199픽셀 사이의 미디어용 스타일입니다.</td>
   <td><p>@media(최소 너비:980px) 및 (최대 너비:1199px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-768px-979px.css</td>
   <td>768픽셀과 979픽셀 사이의 미디어용 스타일입니다. </td>
   <td><p>@media(최소 너비:768px) 및 (최대 너비:979px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-767px-max.css</td>
   <td>가로 768픽셀 미만인 모든 미디어에 대한 스타일</td>
   <td><p>@media(최대 너비:767px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-480px.css</td>
   <td>폭이 481픽셀 미만인 모든 미디어에 대한 스타일</td>
   <td>@media(최대 너비:480) {<br /> ...<br /> }</td>
  </tr>
 </tbody>
</table>

`/etc/designs/weretail/clientlibs` 폴더의 css.txt 파일에는 클라이언트 라이브러리 폴더에 포함된 CSS 파일이 나열됩니다. 파일의 순서는 스타일 우선 순위를 구현합니다. 장치 크기가 줄어들면 스타일이 더 구체적입니다.

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

**팁**:설명 파일 이름을 사용하면 대상 뷰포트 크기를 쉽게 식별할 수 있습니다.

### AEM 페이지에 미디어 쿼리 사용 {#using-media-queries-with-aem-pages}

페이지 구성 요소의 JSP 스크립트에 클라이언트 라이브러리 폴더를 포함시켜 미디어 쿼리를 포함하는 CSS 파일을 생성하고 파일을 참조합니다.

```xml
<ui:includeClientLib categories="apps.weretail.all"/>
```

>[!NOTE]
>
>`apps.weretail.all` 클라이언트 라이브러리 폴더는 clientlibs 라이브러리를 포함합니다.

JSP 스크립트는 스타일 시트를 참조하는 다음 HTML 코드를 생성합니다.

```xml
<link rel="stylesheet" href="/etc/designs/weretail/clientlibs-all.css" type="text/css">
<link href="/etc/designs/weretail.css" rel="stylesheet" type="text/css">
```

## 특정 장치에 대한 미리 보기{#previewing-for-specific-devices}

반응형 디자인의 동작을 테스트하려면 다양한 뷰포트 크기로 페이지 미리 보기를 참조하십시오. **[!UICONTROL 미리 보기]** 모드에서 **[!UICONTROL 사이드킥은 장치를 선택하는 데 사용하는**[!UICONTROL &#x200B;장치&#x200B;]**드롭다운 메뉴를 포함합니다.]** 장치를 선택하면 페이지가 뷰포트 크기에 맞게 변경됩니다.

![chlimage_1-5](assets/chlimage_1-5a.png)

**[!UICONTROL Sidekick]**&#x200B;에서 장치 미리 보기를 활성화하려면 페이지와 **[!UICONTROL MobileEmulatorProvider]** 서비스를 구성해야 합니다. 다른 페이지 구성은 **[!UICONTROL 장치]** 목록에 나타나는 장치 목록을 제어합니다.

### 장치 목록 추가 {#adding-the-devices-list}

페이지에 **[!UICONTROL 장치]** 목록을 렌더링하는 JSP 스크립트가 포함된 경우 **[!UICONTROL 장치]** 목록이 **[!UICONTROL 사이드 킥이]**&#x200B;에 나타납니다. **[!UICONTROL 장치]** 목록을 **[!UICONTROL 사이드 킥이나]**&#x200B;에 추가하려면 페이지의 `head` 섹션에 `/libs/wcm/mobile/components/simulator/simulator.jsp` 스크립트를 포함시키십시오.

`head` 섹션을 정의하는 JSP에 다음 코드를 포함합니다.

`<cq:include script="/libs/wcm/mobile/components/simulator/simulator.jsp"/>`

예를 보려면 CRXDE Lite에서 `/apps/weretail/components/page/head.jsp` 파일을 엽니다.

### 시뮬레이션에 대한 페이지 구성 요소 등록 {#registering-page-components-for-simulation}

장치 시뮬레이터가 페이지를 지원할 수 있도록 하려면 MobileEmulatorProvider 팩토리 서비스로 페이지 구성 요소를 등록하고 `mobile.resourceTypes` 속성을 정의하십시오.

AEM을 사용하는 경우 이러한 서비스에 대한 구성 설정을 관리하는 방법에는 여러 가지가 있습니다.자세한 내용은 [OSGi](/help/sites-deploying/configuring-osgi.md) 구성을 참조하십시오.

예를 들어 애플리케이션에서 ` [sling:OsgiConfig](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)` 노드를 만들려면 다음을 수행하십시오.

* 상위 폴더:`/apps/application_name/config`
* 이름: `com.day.cq.wcm.mobile.core.impl.MobileEmulatorProvider-*alias*`

   MobileEmulatorProvider 서비스는 팩터리 서비스이므로 - `*alias*` 접미사가 필요합니다. 이 팩터리에 대해 고유한 별칭을 사용하십시오.

* jcr:primaryType: `sling:OsgiConfig`

다음 노드 속성을 추가합니다.

* 이름: `mobile.resourceTypes`
* 유형: `String[]`
* 값:웹 페이지를 렌더링하는 페이지 구성 요소의 경로입니다. 예를 들어 geometrixx-media 앱은 다음 값을 사용합니다.

   ```
   geometrixx-media/components/page
    geometrixx-unlimited/components/pages/page
    geometrixx-unlimited/components/pages/coverpage
    geometrixx-unlimited/components/pages/issue
   ```

### 장치 그룹 지정 {#specifying-the-device-groups}

장치 목록에 나타나는 장치 그룹을 지정하려면 사이트의 루트 페이지 `jcr:content` 노드에 `cq:deviceGroups` 속성을 추가합니다. 속성 값은 장치 그룹 노드에 대한 경로 배열입니다.

장치 그룹 노드는 `/etc/mobile/groups` 폴더에 있습니다.

예를 들어 Geometrixx Media 사이트의 루트 페이지는 `/content/geometrixx-media`입니다. `/content/geometrixx-media/jcr:content` 노드에는 다음 속성이 포함됩니다.

* 이름: `cq:deviceGroups`
* 유형: `String[]`
* 값: `/etc/mobile/groups/responsive`

[장치 그룹 만들기 및 편집](/help/sites-developing/groupfilters.md)에 도구 콘솔을 사용하십시오.

>[!NOTE]
>
>응답형 디자인에 사용하는 장치 그룹의 경우 장치 그룹을 편집하고 일반 탭에서 에뮬레이터 사용 안 함을 선택합니다. 이 옵션은 에뮬레이터 회전판이 반응형 디자인과는 관련이 없는 것을 방지합니다.


## 응용 이미지 사용 {#using-adaptive-images}

미디어 쿼리를 사용하여 페이지에 표시할 이미지 리소스를 선택할 수 있습니다. 그러나 미디어 쿼리를 사용하여 사용을 조건화하는 모든 리소스는 클라이언트에 다운로드됩니다. 미디어 쿼리는 다운로드한 리소스가 표시되는지 여부를 판별할 뿐입니다.

이미지와 같은 대형 리소스의 경우 모든 리소스를 다운로드하는 것은 클라이언트의 데이터 파이프라인을 효율적으로 사용하는 것이 아닙니다. 리소스를 선택적으로 다운로드하려면, 미디어 쿼리가 선택을 수행한 후 javascript를 사용하여 리소스 요청을 시작합니다.

다음 전략은 미디어 쿼리를 사용하여 선택한 단일 리소스를 로드합니다.

1. 각 리소스 버전에 대한 DIV 요소를 추가합니다. 리소스의 URI를 속성 값의 값으로 포함합니다. 브라우저가 속성을 리소스로 해석하지 않습니다.
1. 리소스에 적합한 각 DIV 요소에 미디어 쿼리를 추가합니다.
1. 문서가 로드되거나 창 크기가 변경되면 javascript 코드는 각 DIV 요소의 미디어 쿼리를 테스트합니다.
1. 쿼리 결과에 따라 포함할 리소스를 결정합니다.
1. 리소스를 참조하는 DOM에 HTML 요소를 삽입합니다.

### Javascript {#evaluating-media-queries-using-javascript}을(를) 사용하여 미디어 쿼리 평가

W3C가 정의하는 [MediaQueryList 인터페이스](https://dev.w3.org/csswg/cssom-view/#the-mediaquerylist-interface)의 구현을 통해 javascript를 사용하여 미디어 쿼리를 평가할 수 있습니다. 미디어 쿼리 결과에 로직을 적용하고 현재 창에 대해 타깃팅된 스크립트를 실행할 수 있습니다.

* MediaQueryList 인터페이스를 구현하는 브라우저는 `window.matchMedia()` 함수를 지원합니다. 이 함수는 지정된 문자열에 대해 미디어 쿼리를 테스트합니다. 이 함수는 쿼리 결과에 대한 액세스를 제공하는 `MediaQueryList` 개체를 반환합니다.

* 인터페이스를 구현하지 않는 브라우저의 경우 무료로 사용할 수 있는 javascript 라이브러리인 [matchMedia.js](https://github.com/paulirish/matchMedia.js)와 같은 `matchMedia()` polyfill을 사용할 수 있습니다.

#### 미디어별 리소스 선택 {#selecting-media-specific-resources}

W3C 제안 [그림 요소](https://picture.responsiveimages.org/)는 미디어 쿼리를 사용하여 이미지 요소에 사용할 소스를 결정합니다. 그림 요소는 요소 속성을 사용하여 미디어 쿼리를 이미지 경로와 연결합니다.

자유롭게 사용할 수 있는 [picturefill.js 라이브러리](https://github.com/scottjehl/picturefill)는 제안된 `picture` 요소와 유사한 기능을 제공하며 유사한 전략을 사용합니다. picturefill.js 라이브러리는 `window.matchMedia`을 호출하여 `div` 요소 집합에 대해 정의된 미디어 쿼리를 평가합니다. 각 `div` 요소는 이미지 소스도 지정합니다. 소스는 `div` 요소의 미디어 쿼리가 `true`을 반환하는 경우에 사용됩니다.

`picturefill.js` 라이브러리에는 다음 예와 유사한 HTML 코드가 필요합니다.

```xml
<div data-picture>
    <div data-src='path to default image'></div>
    <div data-src='path to small image'    data-media="(media query for phone)"></div>
    <div data-src='path to medium image'   data-media="(media query for tablet)"></div>
    <div data-src='path to large image'     data-media="(media query for monitor)"></div>
</div>
```

페이지가 렌더링되면 pictureflow.js는 `<div data-picture>` 요소의 마지막 자식으로 `img` 요소를 삽입합니다.

```xml
<div data-picture>
    <div data-src='path to default image'></div>
    <div data-src='path to small image'    data-media="(media query for phone)"></div>
    <div data-src='path to medium image'   data-media="(media query for tablet)"></div>
    <div data-src='path to large image'     data-media="(media query for monitor)"></div>
    <img src="path to medium image">
</div>
```

AEM 페이지에서 `data-src` 속성의 값은 저장소의 리소스에 대한 경로입니다.

### AEM {#implementing-adaptive-images-in-aem}에서 응용 이미지 구현

AEM 애플리케이션에서 응용 이미지를 구현하려면 필요한 javascript 라이브러리를 추가하고 페이지에 필요한 HTML 마크업을 포함해야 합니다.

**라이브러리**

다음 javascript 라이브러리를 입수하고 클라이언트 라이브러리 폴더에 포함합니다.

* [matchMedia.js](https://github.com/paulirish/matchMedia.js) (MediaQueryList 인터페이스를 구현하지 않는 브라우저의 경우)
* [picturefill.js](https://github.com/scottjehl/picturefill)
* jquery.js(`/etc/clientlibs/granite/jquery` 클라이언트 라이브러리 폴더(category = jquery)를 통해 사용 가능
* [jquery.devounceedsize.js](https://github.com/louisremi/jquery-smartresize) (창 크기를 조정한 후 한 번 발생하는 jquery 이벤트)

**팁:** 임베드하여 여러 클라이언트 라이브러리 폴더를 자동으로 연결할  [수 있습니다](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries).

**HTML**

picturefill.js 코드에서 필요로 하는 div 요소를 생성하는 구성 요소를 만듭니다. AEM 페이지에서 data-src 속성의 값은 저장소의 리소스 경로입니다. 예를 들어 페이지 구성 요소는 미디어 쿼리 및 DAM의 이미지 표현물에 대한 관련 경로를 하드 코딩할 수 있습니다. 또는 작성자가 이미지 변환을 선택하거나 런타임 렌더링 옵션을 지정할 수 있는 사용자 정의 이미지 구성 요소를 만듭니다.

다음 예제 HTML은 동일한 이미지의 2개의 DAM 표현물 중에서 선택합니다.

```xml
<div data-picture>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png'></div>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png/jcr:content/renditions/cq5dam.thumbnail.319.319.png'    data-media="(min-width: 769px)"></div>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png/jcr:content/renditions/cq5dam.thumbnail.140.100.png'   data-media="(min-width: 481px)"></div>
</div>
```

>[!NOTE]
>
>응용 이미지 기반 구성 요소는 응용 이미지를 구현합니다.
>
>* 클라이언트 라이브러리 폴더:`/libs/foundation/components/adaptiveimage/clientlibs`
>* HTML을 생성하는 스크립트:`/libs/foundation/components/adaptiveimage/adaptiveimage.jsp`

>
>
다음 섹션에서는 이 구성 요소에 대한 세부 사항을 제공합니다.


### AEM {#understanding-image-rendering-in-aem}의 이미지 렌더링 이해

이미지 렌더링을 사용자 정의하려면 기본 AEM 정적 이미지 렌더링 구현을 이해해야 합니다. AEM은 웹 페이지용 이미지를 렌더링하기 위해 함께 작동하는 이미지 구성 요소와 이미지 렌더링 서블릿을 제공합니다. 다음 이벤트 시퀀스는 이미지 구성 요소가 페이지의 단락 시스템에 포함될 때 발생합니다.

1. 작성:작성자는 이미지 구성 요소를 편집하여 HTML 페이지에 포함할 이미지 파일을 지정합니다. 파일 경로는 이미지 구성 요소 노드의 속성 값으로 저장됩니다.
1. 페이지 요청:페이지 구성 요소의 JSP는 HTML 코드를 생성합니다. 이미지 구성 요소의 JSP는 페이지에 img 요소를 생성하고 추가합니다.
1. 이미지 요청:웹 브라우저는 페이지를 로드하고 img 요소의 src 속성에 따라 이미지를 요청합니다.
1. 이미지 렌더링:이미지 렌더링 서블릿은 웹 브라우저에 이미지를 반환합니다.

![chlimage_1-6](assets/chlimage_1-6a.png)

예를 들어 이미지 구성 요소의 JSP는 다음 HTML 요소를 생성합니다.

`<img title="My Image" alt="My Image" class="cq-dd-image" src="/content/mywebsite/en/_jcr_content/par/image_0.img.jpg/1358372073597.jpg">`

브라우저가 페이지를 로드할 때 src 속성의 값을 URL로 사용하여 이미지를 요청합니다. Sling은 URL을 디컴파일합니다.

* 리소스: `/content/mywebsite/en/_jcr_content/par/image_0`
* 파일 이름 확장자:`.jpg`
* 선택기: `img`
* 접미어: `1358372073597.jpg`

`image_0` 노드에는 `jcr:resourceType` 값이 `foundation/components/image`이고 `sling:resourceSuperType` 값이 `foundation/components/parbase`입니다. parbase 구성 요소에는 선택기와 일치하는 img.GET.java 스크립트와 요청 URL의 파일 이름 확장자가 포함됩니다. CQ는 이 스크립트(servlet)를 사용하여 이미지를 렌더링합니다.

스크립트의 소스 코드를 보려면 CRXDE Lite을 사용하여 `/libs/foundation/components/parbase/img.GET.java`
file.

## 현재 뷰포트 크기 {#scaling-images-for-the-current-viewport-size}에 대한 이미지 크기 조절

클라이언트 뷰포트의 특성에 따라 런타임 시 이미지 크기를 조절하여 반응형 디자인의 원칙을 준수하는 이미지를 제공합니다. 서블릿 및 제작 구성 요소를 사용하여 정적 이미지 렌더링과 동일한 디자인 패턴을 사용합니다.

구성 요소는 다음 작업을 수행해야 합니다.

* 이미지 리소스의 경로와 원하는 크기를 속성 값으로 저장합니다.
* 이미지 렌더링에 대한 미디어 선택기 및 서비스 호출이 포함된 `div` 요소를 생성합니다.

>[!NOTE]
>
>웹 클라이언트는 matchMedia 및 Picturefill javascript 라이브러리(또는 유사한 라이브러리)를 사용하여 미디어 선택기를 평가합니다.


이미지 요청을 처리하는 서블릿은 다음 작업을 수행해야 합니다.

* 구성 요소 속성에서 이미지의 경로 및 크기를 검색합니다.
* 속성에 따라 이미지의 크기를 조절하고 이미지를 반환합니다.

**사용 가능한 솔루션**

AEM은 사용하거나 확장할 수 있는 다음 구현을 설치합니다.

* 미디어 쿼리를 생성하는 응용 이미지 기반 구성 요소로서, 이미지를 확장하는 응용 이미지 구성 요소 서블릿에 대한 HTTP 요청을 제공합니다.
* Geometrixx Commons 패키지는 이미지 해상도를 변경하는 이미지 참조 수정 서블릿 샘플 서버를 설치합니다.

### 응용 이미지 구성 요소 {#understanding-the-adaptive-image-component} 이해

응용 이미지 구성 요소는 응용 이미지 구성 요소 서블릿에 대한 호출을 생성하여 장치 화면에 따라 크기가 조정된 이미지를 렌더링합니다. 구성 요소에는 다음 리소스가 포함되어 있습니다.

* JSP:미디어 쿼리를 응용 이미지 구성 요소 서블릿에 대한 호출과 연결하는 div 요소를 추가합니다.
* 클라이언트 라이브러리:clientlibs 폴더는 matchMedia polyfill javascript 라이브러리와 수정된 Picturefill javascript 라이브러리를 어셈블하는 `cq:ClientLibraryFolder`입니다.
* 편집 대화 상자:`cq:editConfig` 노드는 CQ foundation 이미지 구성 요소를 무시하므로 드롭 대상이 기본 이미지 구성 요소가 아닌 응용 이미지 구성 요소를 만듭니다.

#### DIV 요소 {#adding-the-div-elements} 추가

adaptive-image.jsp 스크립트에는 div 요소 및 미디어 쿼리를 생성하는 다음 코드가 포함되어 있습니다.

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

`path` 변수에는 현재 리소스(응용 이미지 구성 요소 노드)의 경로가 포함됩니다. 코드는 다음 구조를 가진 일련의 `div` 요소를 생성합니다.

`<div data-scr = "*path-to-parent-node*.adaptive-image.adapt.*width*.*quality*.jpg" data-media="*media query*"></div>`

`data-scr` 속성의 값은 Sling이 이미지를 렌더링하는 응용 이미지 구성 요소 서블릿으로 확인되는 URL입니다. data-media 속성에는 클라이언트 속성에 대해 평가되는 미디어 쿼리가 포함됩니다.

다음 HTML 코드는 JSP가 생성하는 `div` 요소의 예입니다.

```xml
<div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.320.low.jpg'></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.320.medium.jpg'    data-media="(min-width: 320px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.480.medium.jpg'    data-media="(min-width: 321px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.476.high.jpg'     data-media="(min-width: 481px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.620.high.jpg'     data-media="(min-width: 769px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.full.high.jpg'     data-media="(min-width: 1025px)"></div>
```

#### 이미지 크기 선택기 변경 {#changing-the-image-size-selectors}

응용 이미지 구성 요소를 사용자 정의하고 너비 선택기를 변경하는 경우 너비를 지원하도록 응용 이미지 구성 요소 서블릿을 구성해야 합니다.

### 응용 이미지 구성 요소 서블릿 이해 {#understanding-the-adaptive-image-component-servlet}

응용 이미지 구성 요소 서블릿은 지정된 너비에 따라 JPEG 이미지의 크기를 조절하고 JPEG 품질을 설정합니다.

#### 응용 이미지 구성 요소 서블릿의 인터페이스 {#the-interface-of-the-adaptive-image-component-servlet}

응용 이미지 구성 요소 서블릿은 기본 Sling 서블릿에 바인딩되며 .jpg, .jpeg, .gif 및 .png 파일 확장명을 지원합니다. 서블릿 선택기는 img입니다.

>[!CAUTION]
>
>애니메이션된 .gif 파일은 적응형 표현물에 대해 AEM에서 지원되지 않습니다.

따라서 Sling은 다음 형식의 HTTP 요청 URL을 이 서블릿으로 확인합니다.

`*path-to-node*.img.*extension*`

예를 들어 Sling은 URL `http://localhost:4502/content/geometrixx/adaptiveImage.img.jpg`이 있는 HTTP 요청을 응용 이미지 구성 요소 서블릿으로 전달합니다.

두 개의 추가 선택기는 요청된 이미지 너비와 JPEG 품질을 지정합니다. 다음 예에서는 너비 480픽셀과 중간 품질의 이미지를 요청합니다.

`http://localhost:4502/content/geometrixx/adaptiveImage.adapt.480.MEDIUM.jpg`

**지원되는 이미지 속성**

서블릿은 제한된 수의 이미지 폭과 품질을 허용합니다. 기본적으로 지원되는 너비(픽셀 단위):

* 전체
* 320
* 480
* 476
* 620

전체 값은 크기 조정이 없음을 나타냅니다.

JPEG 품질에 대한 다음 값이 지원됩니다.

* LOW
* 중간
* 높음

숫자 값은 각각 0.4, 0.82 및 1.0입니다.

**지원되는 기본 너비 변경**

웹 콘솔([http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)) 또는 sling:OsgiConfig 노드를 사용하여 Adobe CQ 응용 이미지 구성 요소 서블릿의 지원되는 너비를 구성합니다.

AEM 서비스 구성 방법에 대한 자세한 내용은 [OSGi 구성](/help/sites-deploying/configuring-osgi.md)을 참조하십시오.

<table>
 <tbody>
  <tr>
   <th> </th>
   <th>웹 콘솔</th>
   <th>sling:OsgiConfig</th>
  </tr>
  <tr>
   <th>서비스 또는 노드 이름</th>
   <td>구성 탭의 서비스 이름은 Adobe CQ 응용 이미지 구성 요소 서블릿입니다.</td>
   <td>com.day.cq.wcm.foundation.impl. AdaptiveImageComponentServlet</td>
  </tr>
  <tr>
   <th>속성</th>
   <td><p>지원되는 너비</p>
    <ul>
     <li>지원되는 너비를 추가하려면 + 단추를 클릭하고 양의 정수를 입력합니다.</li>
     <li>지원되는 너비를 제거하려면 연결된 - 단추를 클릭합니다.</li>
     <li>지원되는 너비를 수정하려면 필드 값을 편집합니다.</li>
    </ul> </td>
   <td><p>adapt.supported.widths</p>
    <ul>
     <li>이 속성은 다중값 문자열 값입니다.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

#### 구현 세부 정보 {#implementation-details}

`com.day.cq.wcm.foundation.impl.AdaptiveImageComponentServlet` 클래스는 [AbstractImageServlet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.html) 클래스를 확장합니다. AdaptiveImageComponentServlet 소스 코드는 `/libs/foundation/src/impl/src/com/day/cq/wcm/foundation/impl` 폴더에 있습니다.

이 클래스는 Felix SCR 주석을 사용하여 서블릿과 연관된 리소스 유형 및 파일 확장자와 첫 번째 선택기의 이름을 구성합니다.

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

서블릿은 속성 SCR 주석을 사용하여 지원되는 기본 이미지 품질과 치수를 설정합니다.

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

`AbstractImageServlet` 클래스는 HTTP 요청을 처리하는 `doGet` 메서드를 제공합니다. 이 메서드는 요청과 연결된 리소스를 결정하고 저장소에서 리소스 속성을 검색하고 [ImageContext](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.ImageContext.html) 개체에서 반환합니다.

>[!NOTE]
>
>[com.day.cq.commons.DownloadResource](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/DownloadResource.html) 클래스는 리소스의 `fileReference` 속성 값을 검색하는 `getFileReference method`를 제공합니다.

`AdaptiveImageComponentServlet` 클래스는 `createLayer` 메서드를 재정의합니다. 이 메서드는 `ImageContext` 개체에서 이미지 리소스의 경로와 요청된 이미지 너비를 가져옵니다. 그런 다음 실제 이미지 크기 조정을 수행하는 `info.geometrixx.commons.impl.AdaptiveImageHelper` 클래스의 메서드를 호출합니다.

AdaptiveImageComponentServlet 클래스는 writeLayer 메서드도 무시합니다. 이 방법은 이미지에 JPEG 품질을 적용합니다.

### 이미지 참조 수정 서블릿(Geometrixx 공통) {#image-reference-modification-servlet-geometrixx-common}

샘플 이미지 참조 수정 서블릿은 웹 페이지에서 이미지의 크기를 조절하기 위해 img 요소에 대한 크기 속성을 생성합니다.

#### servlet {#calling-the-servlet} 호출

서블릿은 `cq:page` 리소스에 바인딩되며 .jpg 파일 확장명을 지원합니다. 서블릿 선택기는 `image`입니다. 따라서 Sling은 다음 형식의 HTTP 요청 URL을 이 서블릿으로 확인합니다.

`path-to-page-node.image.jpg`

예를 들어 Sling은 URL이 `http://localhost:4502/content/geometrixx/en.image.jpg`인 HTTP 요청을 이미지 참조 수정 서블릿으로 전달합니다.

세 개의 추가 선택기는 요청된 이미지 너비, 높이 및 (선택 사항) 품질을 지정합니다. 다음 예에서는 너비 770픽셀, 높이 360픽셀 및 중간 품질의 이미지를 요청합니다.

`http://localhost:4502/content/geometrixx/en.image.770.360.MEDIUM.jpg`

**지원되는 이미지 속성**

서블릿은 한정된 이미지 크기와 품질 값을 허용합니다.

기본적으로 다음 값이 지원됩니다(위젯 높이).

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

이미지 품질에 대한 다음 값이 지원됩니다.

* 낮음
* 중간
* 높음

AEM을 사용하는 경우 이러한 서비스에 대한 구성 설정을 관리하는 방법에는 여러 가지가 있습니다.자세한 내용은 [OSGi](/help/sites-deploying/configuring-osgi.md) 구성을 참조하십시오.

#### 이미지 리소스 {#specifying-the-image-resource} 지정

이미지 경로, 차원 및 품질 값은 저장소에 있는 노드의 속성으로 저장해야 합니다.

* 노드 이름은 `image`입니다.
* 상위 노드는 `cq:page` 리소스의 `jcr:content` 노드입니다.

* 이미지 경로는 `fileReference`이라는 속성의 값으로 저장됩니다.

페이지를 작성할 때 **Sidekick**&#x200B;을 사용하여 이미지를 지정하고 페이지 속성에 `image` 노드를 추가합니다.

1. **사이드 킥이**&#x200B;에서 **페이지** 탭을 클릭한 다음 **페이지 속성**&#x200B;을 클릭합니다.
1. **이미지** 탭을 클릭하고 이미지를 지정합니다.
1. **확인**&#x200B;을 클릭합니다.

#### 구현 세부 정보 {#implementation-details-1}

info.geometrixx.commons.impl.servlets.ImageReferenceModificationServlet 클래스는 [AbstractImageServlet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.html) 클래스를 확장합니다. cq-geometrixx-commons-pkg 패키지가 설치되어 있는 경우 ImageReferenceModificationServlet 소스 코드는 `/apps/geometrixx-commons/src/core/src/main/java/info/geometrixx/commons/impl/servlets` 폴더에 있습니다.

이 클래스는 Felix SCR 주석을 사용하여 서블릿과 연관된 리소스 유형 및 파일 확장자와 첫 번째 선택기의 이름을 구성합니다.

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

서블릿은 속성 SCR 주석을 사용하여 지원되는 기본 이미지 품질과 치수를 설정합니다.

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

`AbstractImageServlet` 클래스는 HTTP 요청을 처리하는 `doGet` 메서드를 제공합니다. 이 메서드는 호출과 연결된 리소스를 결정하고 저장소에서 리소스 속성을 검색하고 이를 [ImageContext](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.ImageContext.html) 개체에 저장합니다.

`ImageReferenceModificationServlet` 클래스는 `createLayer` 메서드를 재정의하고 렌더링할 이미지 리소스를 결정하는 논리를 구현합니다. 이 메서드는 페이지의 `jcr:content` 노드에서 `image`이라는 하위 노드를 검색합니다. [Image](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/foundation/Image.html) 개체가 이 `image` 노드에서 만들어지고 `getFileReference` 메서드는 이미지 노드의 `fileReference` 속성에서 이미지 파일에 대한 경로를 반환합니다.

>[!NOTE]
>[com.day.cq.commons.DownloadResource](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/DownloadResource.html) 클래스는 getFileReference 메서드를 제공합니다.


## 유동 격자 개발 {#developing-a-fluid-grid}

AEM을 사용하면 유동 격자를 효율적이고 효과적으로 구현할 수 있습니다. 이 페이지에서는 유동 격자 또는 기존 그리드 구현(예: [Bootstrap](https://twitter.github.com/bootstrap/))을 AEM 애플리케이션에 통합하는 방법을 설명합니다.

유동 격자에 익숙하지 않은 경우 이 페이지 하단의 [유동 격자 소개](/help/sites-developing/responsive.md#developing-a-fluid-grid) 섹션을 참조하십시오. 이 소개에서는 유동 격자에 대한 개요와 이러한 격자 디자인을 위한 지침을 제공합니다.

### 페이지 구성 요소 {#defining-the-grid-using-a-page-component}을(를) 사용하여 그리드 정의

페이지 구성 요소를 사용하여 페이지의 컨텐츠 블록을 정의하는 HTML 요소를 생성합니다. 페이지가 참조하는 ClientLibraryFolder는 콘텐츠 블록의 레이아웃을 제어하는 CSS를 제공합니다.

* 페이지 구성 요소:컨텐츠 블록 행을 나타내는 div 요소를 추가합니다. 컨텐츠 블록을 나타내는 div 요소에는 작성자가 컨텐츠를 추가하는 parsys 구성 요소가 포함됩니다.
* 클라이언트 라이브러리 폴더:div 요소에 대한 미디어 쿼리 및 스타일을 포함하는 CSS 파일을 제공합니다.

예를 들어 샘플 geometrixx-media 응용 프로그램에는 media-home 구성 요소가 포함되어 있습니다. 이 페이지 구성 요소는 두 개의 스크립트를 삽입합니다. 이 스크립트를 통해 `row-fluid` 클래스의 두 개의 `div` 요소가 생성됩니다.

* 첫 번째 행은 `span12` 클래스의 `div` 요소를 포함합니다(컨텐츠는 12열). `div` 요소에는 parsys 구성 요소가 포함되어 있습니다.

* 두 번째 행에는 `div` 요소, 클래스 `span8` 중 하나와 클래스 `span4`의 다른 요소가 있습니다. 각 `div` 요소에는 parsys 구성 요소가 포함됩니다.

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
>구성 요소에 parsys 구성 요소를 참조하는 여러 개의 `cq:include` 요소가 포함된 경우 각 `path` 속성에는 다른 값이 있어야 합니다.


#### 페이지 구성 요소 그리드 크기 조정 {#scaling-the-page-component-grid}

geometrixx-media 페이지 구성 요소(`/etc/designs/geometrixx-media`)와 연결된 디자인에는 `clientlibs` ClientLibraryFolder가 포함되어 있습니다. 이 ClientLibraryFolder는 `row-fluid` 클래스의 자식인 `row-fluid` 클래스, `span*` 클래스 및 `span*` 클래스에 대한 CSS 스타일을 정의합니다. 미디어 쿼리를 사용하면 다양한 뷰포트 크기에 맞게 스타일을 재정의할 수 있습니다.

다음 예제 CSS는 이러한 스타일의 하위 집합입니다. 이 하위 세트는 `span12`, `span8` 및 `span4` 클래스에 중점을 두고 두 개의 뷰포트 크기에 대한 미디어 쿼리에 중점을 둡니다. CSS의 다음 특성을 확인합니다.

* `.span` 스타일은 절대 숫자를 사용하여 요소 너비를 정의합니다.
* `.row-fluid .span*` 스타일은 요소 너비를 상위의 백분율로 정의합니다. 비율은 절대 너비에서 계산됩니다.
* 더 큰 뷰포트를 위한 미디어 쿼리는 더 큰 절대 너비를 할당합니다.

>[!NOTE]
>
>Geometrixx Media 샘플은 [Bootstrap](https://twitter.github.com/bootstrap/javascript.html) javascript 프레임워크를 유동 격자 구현에 통합합니다. Bootstrap 프레임워크은 bootstrap.css 파일을 제공합니다.

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

#### 페이지 구성 요소 그리드 {#repositioning-content-in-the-page-component-grid}에서 컨텐츠 위치 변경

샘플 Geometrixx Media 애플리케이션의 페이지는 컨텐츠 블록 행을 광범위한 뷰포트에 가로로 배포합니다. 작은 뷰포트에서는 동일한 블록이 세로로 배포됩니다. 다음 예제 CSS는 media-home 페이지 구성 요소가 생성하는 HTML 코드에 대해 이 동작을 구현하는 스타일을 보여줍니다.

* 미디어 시작 페이지의 기본 CSS는 `row-fluid` 클래스 내에 있는 `span*` 클래스에 대해 `float:left` 스타일을 지정합니다.

* 작은 뷰포트에 대한 미디어 쿼리는 동일한 클래스에 대해 `float:none` 스타일을 지정합니다.

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

#### 페이지 구성 요소 수정{#tip-modularize-your-page-components}

구성 요소를 수정하여 코드를 효율적으로 사용합니다. 사이트에서 시작 페이지, 아티클 페이지 또는 제품 페이지와 같은 여러 가지 유형의 페이지를 사용할 수 있습니다. 각 유형의 페이지에는 서로 다른 유형의 컨텐츠가 포함되어 있으며 서로 다른 레이아웃을 사용할 수 있습니다. 그러나 각 레이아웃의 특정 요소가 여러 페이지에서 공통인 경우 레이아웃의 해당 부분을 구현하는 코드를 다시 사용할 수 있습니다.

**페이지 구성 요소 오버레이 사용**

본문 내의 `head` 및 `body` 섹션과 같은 페이지의 다양한 부분을 생성하기 위한 스크립트와 `header`, `content` 및 `footer` 섹션 등을 제공하는 기본 페이지 구성 요소를 만듭니다.

기본 페이지 구성 요소를 `cq:resourceSuperType`으로 사용하는 다른 페이지 구성 요소를 만듭니다. 이러한 구성 요소에는 필요에 따라 기본 페이지의 스크립트를 무시하는 스크립트가 포함되어 있습니다.

예를 들어, Geometrixx-media 응용 프로그램에는 페이지 구성 요소가 포함됩니다(`sling:resourceSuperType`은 기본 페이지 구성 요소임). 아티클, 카테고리 및 media-home과 같은 여러 하위 구성 요소는 이 페이지 구성 요소를 `sling:resourceSuperType`으로 사용합니다. 각 하위 구성 요소에는 페이지 구성 요소의 content.jsp 파일을 무시하는 content.jsp 파일이 포함되어 있습니다.

**스크립트 재사용**

여러 페이지 구성 요소에 공통인 행 및 열 조합을 생성하는 여러 JSP 스크립트를 만듭니다. 예를 들어, 아티클 및 media-home 구성 요소의 `content.jsp` 스크립트는 모두 `8x4col.jsp` 스크립트를 참조합니다.

**대상 뷰포트 크기별로 CSS 스타일 구성**

별도의 파일에 서로 다른 뷰포트 크기에 대한 CSS 스타일과 미디어 쿼리를 포함할 수 있습니다. 클라이언트 라이브러리 폴더를 사용하여 연결합니다.

### 구성 요소를 페이지 격자에 삽입 {#inserting-components-into-the-page-grid}

구성 요소가 단일 컨텐츠 블록을 생성하는 경우 일반적으로 페이지 구성 요소가 설정하는 격자가 컨텐츠 배치를 제어합니다.

컨텐츠 블록은 다양한 크기와 상대적 위치로 렌더링될 수 있습니다. 컨텐츠 텍스트는 다른 컨텐츠 블록을 참조하기 위해 상대 방향을 사용하지 않아야 합니다.

필요한 경우 구성 요소는 생성하는 HTML 코드에 필요한 CSS 또는 javascript 라이브러리를 제공해야 합니다. 구성 요소 내의 클라이언트 라이브러리 폴더를 사용하여 CSS 및 JS 파일을 생성합니다. 파일을 노출하려면 [종속성을 만들거나 /etc 폴더 아래의 다른 클라이언트 라이브러리 폴더에 라이브러리](/help/sites-developing/clientlibs.md#creating-client-library-folders)을 포함합니다.

**하위 격자**

구성 요소에 여러 개의 컨텐츠 블록이 포함되어 있는 경우 행 내에 컨텐츠 블록을 추가하여 페이지에서 하위 그리드를 설정합니다.

* 포함된 페이지 구성 요소와 동일한 클래스 이름을 사용하여 div 요소를 행과 컨텐츠 블록으로 표현합니다.
* 페이지 디자인의 CSS가 구현하는 동작을 무시하려면 행 div 요소에 두 번째 클래스 이름을 사용하고 클라이언트 라이브러리 폴더에 연결된 CSS를 제공하십시오.

예를 들어 `/apps/geometrixx-media/components/2-col-article-summary` 구성 요소는 두 개의 컨텐츠 열을 생성합니다. 생성되는 HTML에는 다음 구조가 있습니다.

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

페이지 CSS의 `.row-fluid .span6` 선택기는 이 HTML에서 동일한 클래스 및 구조의 `div` 요소에 적용됩니다. 그러나 구성 요소에는 /apps/geometrixx-media/components/2-col-article-summary/clientlibs 클라이언트 라이브러리 폴더도 포함되어 있습니다.

* CSS는 페이지 구성 요소와 동일한 미디어 쿼리를 사용하여 동일한 개별 페이지 너비로 레이아웃 변경을 설정합니다.
* 선택기는 `div` 행 요소의 `multi-col-article-summary` 클래스를 사용하여 페이지의 `row-fluid` 클래스의 동작을 덮어씁니다.

예를 들어 다음 스타일이 `/apps/geometrixx-media/components/2-col-article-summary/clientlibs/css/responsive-480px.css` 파일에 포함됩니다.

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

유동 격자 기능을 사용하면 페이지 레이아웃이 클라이언트 뷰포트의 크기에 맞게 조정됩니다. 격자는 페이지에 컨텐츠 블록을 배치하는 논리 열과 행으로 구성됩니다.

* 열은 컨텐츠 블록의 가로 위치와 너비를 결정합니다.
* 행은 컨텐츠 블록의 상대적 세로 위치를 결정합니다.

HTML5 기술을 사용하면 격자를 구현하고 조작하여 페이지 레이아웃을 다양한 뷰포트 크기에 맞게 조정할 수 있습니다.

* HTML `div` 요소에는 특정 개수의 열을 확장하는 컨텐츠 블록이 포함됩니다.
* 이러한 div 요소 중 하나 이상이 공통 상위 요소를 공유할 때 행을 구성합니다.

### 추가 폭 사용 {#using-discrete-widths}

타깃팅하는 각 뷰포트 폭 범위에 대해 고정 페이지 너비와 일정한 너비의 컨텐츠 블록을 사용하십시오. 브라우저 창의 크기를 수동으로 변경하면 컨텐츠 크기가 개별 창 너비(중단점이라고도 함)에서 변경됩니다. 따라서 페이지 디자인이 사용자 경험을 최대화하면서 더 긴밀하게 부착됩니다.

#### 격자 크기 조정 {#scaling-the-grid}

격자를 사용하여 다양한 뷰포트 크기에 맞게 컨텐츠 블록의 크기를 조절할 수 있습니다. 컨텐츠 블록은 특정 개수의 열에 걸쳐 있습니다. 열 너비가 다른 보기 포트 크기에 맞게 늘어나거나 줄면 컨텐츠 블록의 너비가 그에 따라 늘어나거나 줄어듭니다. 크기 조절은 컨텐츠 블록의 나란히 배치할 수 있을 만큼 충분히 넓은 대형 및 중간 크기의 뷰포트를 모두 지원할 수 있습니다.

![](do-not-localize/chlimage_1-1a.png)

#### 격자 {#repositioning-content-in-the-grid}에서 컨텐츠 위치 변경

컨텐츠 블록의 크기는 더 이상 크기 조정이 적용되지 않는 최소 폭으로 제한할 수 있습니다. 더 작은 뷰포트의 경우 격자를 사용하여 컨텐츠 블록을 가로가 아니라 세로로 배포할 수 있습니다.

![](do-not-localize/chlimage_1-2a.png)

### 격자 디자인 {#designing-the-grid}

페이지에 컨텐츠 블록을 배치해야 하는 열과 행을 결정합니다. 페이지 레이아웃에서는 그리드에 걸쳐 있는 열과 행의 수를 결정합니다.

**열 수**

모든 뷰포트 크기에 대해 모든 레이아웃에 컨텐츠 블록을 가로로 배치할 수 있는 충분한 열을 포함합니다. 향후 페이지 디자인을 수용하기 위해 현재 필요한 것보다 많은 열을 사용해야 합니다.

**행 내용**

행을 사용하여 내용 블록의 세로 위치를 제어할 수 있습니다. 동일한 행을 공유하는 콘텐츠 블록을 결정합니다.

* 레이아웃 중 하나에서 서로 가로 옆에 있는 콘텐츠 블록은 동일한 행에 있습니다.
* 서로 가로(더 넓은 보기 포트) 및 세로(더 작은 보기 포트)에 있는 컨텐츠 블록은 동일한 행에 있습니다.

### 격자 구현 {#grid-implementations}

CSS 클래스와 스타일을 만들어 페이지에 있는 컨텐츠 블록의 레이아웃을 제어합니다. 페이지 디자인은 일반적으로 뷰포트 내의 컨텐츠 블록의 상대적 크기와 위치를 기반으로 합니다. 뷰포트는 컨텐츠 블록의 실제 크기를 결정합니다. CSS는 상대 및 절대 크기를 고려해야 합니다. 다음 세 가지 유형의 CSS 클래스를 사용하여 유동 격자를 구현할 수 있습니다.

* 모든 행의 컨테이너인 `div` 요소의 클래스입니다. 이 클래스는 격자의 절대 너비를 설정합니다.
* 행을 나타내는 `div` 요소의 클래스입니다. 이 클래스는 포함된 내용 블록의 가로 또는 세로 위치를 제어합니다.
* 다른 너비의 컨텐츠 블록을 나타내는 `div` 요소에 대한 클래스입니다. 폭은 상위(행)의 백분율로 표시됩니다.

타깃팅된 뷰포트 너비(및 관련 미디어 쿼리)가 페이지 레이아웃에 사용되는 개별 너비를 구분하는 것입니다.

#### 콘텐츠 블록 너비 {#widths-of-content-blocks}

일반적으로 컨텐츠 블록 클래스의 `width` 스타일은 페이지 및 격자의 다음 특성을 기반으로 합니다.

* 타깃팅된 각 뷰포트 크기에 사용 중인 절대 페이지 너비입니다. 알려진 값입니다.
* 각 페이지 너비에 대한 격자 열의 절대 폭입니다. 이러한 값을 결정합니다.
* 각 열의 상대적 너비를 전체 페이지 너비의 백분율로 나타낸 것입니다. 이러한 값을 계산합니다.

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

다음 알고리즘을 사용하여 페이지에 대한 요소 클래스와 CSS 스타일을 개발할 수 있습니다.

1. 모든 행을 포함하는 div 요소의 클래스 이름을 정의합니다(예: `content.`).
1. `row-fluid`과 같은 행을 나타내는 div 요소에 대한 CSS 클래스를 정의합니다.
1. 콘텐츠 블록 요소의 클래스 이름을 정의합니다. 열 범위에서 가능한 모든 너비에 대해 클래스가 필요합니다. 예를 들어 3개의 열에 걸쳐 있는 `div` 요소에 대해 `span3` 클래스를 사용하고 4개의 열에 대해 `span4` 클래스를 사용하십시오. 그리드에 열 수만큼 클래스를 정의합니다.

1. 타깃팅하는 각 뷰포트 크기에 대해 해당 미디어 쿼리를 CSS 파일에 추가합니다. 각 미디어 쿼리에 다음 항목을 추가합니다.

   * `content` 클래스에 대한 선택기(예: `.content{}`).
   * 각 span 클래스에 대한 선택기(예: `.span3{ }`).
   * `row-fluid` 클래스에 대한 선택기(예: `.row-fluid{ }`
   * 행-유동 클래스 내에 있는 범위 클래스에 대한 선택기(예: `.row-fluid span3 { }`).

1. 각 선택기에 너비 스타일 추가:

   1. `content` 선택기 너비를 페이지의 절대 크기로 설정합니다(예: `width:480px`).
   1. 모든 행 유동 선택기 너비를 100%로 설정합니다.
   1. 모든 범위 선택기의 너비를 컨텐츠 블록의 절대 너비로 설정합니다. 작은 격자는 동일한 너비의 균등하게 배포된 열을 사용합니다.`(absolute width of page)/(number of columns)`.
   1. `.row-fluid .span` 선택기 너비를 전체 너비의 백분율로 설정합니다. `(absolute span width)/(absolute page width)*100` 공식을 사용하여 이 너비를 계산합니다.

#### {#positioning-content-blocks-in-rows} 행에 컨텐츠 블록 배치

`.row-fluid` 클래스의 부동 스타일을 사용하여 행의 콘텐츠 블록이 가로로 정렬되는지 또는 세로로 배열되는지를 제어합니다.

* `float:left` 또는 `float:right` 스타일로 인해 하위 요소(콘텐츠 블록)가 가로 분포됩니다.

* `float:none` 스타일로 인해 하위 요소가 세로로 분포됩니다.

각 미디어 쿼리 내의 `.row-fluid` 선택기에 스타일을 추가합니다. 해당 미디어 쿼리에 사용하는 페이지 레이아웃에 따라 값을 설정합니다. 예를 들어, 다음 다이어그램은 컨텐츠를 넓은 뷰포트에 대해 가로로 배포하고, 좁은 뷰포트를 위해 세로로 배포하는 행을 보여줍니다.

![](do-not-localize/chlimage_1-3a.png)

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

#### 클래스 할당{#assigning-classes-to-content-blocks}

타깃팅하는 각 뷰포트 크기의 페이지 레이아웃에 대해 각 컨텐츠 블록에 걸쳐 있는 열 수를 결정합니다. 그런 다음 해당 컨텐츠 블록의 div 요소에 사용할 클래스를 결정합니다.

div 클래스를 설정하면 AEM 응용 프로그램을 사용하여 그리드를 구현할 수 있습니다.
