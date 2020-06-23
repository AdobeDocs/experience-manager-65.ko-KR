---
title: 대화형 이미지
description: Dynamic Media에서 인터랙티브한 이미지를 사용하여 작업하는 방법 살펴보기
uuid: 0bdb73f7-6ce9-4cdf-b6b5-a4d3d4e19a23
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: a6f58f6a-015a-4ced-941c-ef1b6d3e1d6f
docset: aem65
translation-type: tm+mt
source-git-commit: e916f70549197ac9f95443e972401a78735b0560
workflow-type: tm+mt
source-wordcount: '4345'
ht-degree: 0%

---


# 대화형 이미지{#interactive-images}

이미지에 &quot;쇼퍼블&quot; 핫스팟을 드래그 앤 드롭하여 정적인 이미지가 매력적이고 풍부한 경험을 제공할 수 있습니다. 쇼퍼블 핫스팟은 제품 또는 서비스에 대한 추가 정보와 판매 시점(POS: Add to cart) 또는 &quot;Buy&quot; 기능을 결합합니다. 고객은 이러한 핫스팟을 탭하거나 클릭하여 제품 또는 서비스에 직접 연결하거나 장바구니에 추가하거나 웹 페이지에 연결할 수 있습니다. 이러한 직접적인 경험은 웹 사이트의 고객 참여도와 전환율을 향상시킵니다.

다음은 Quickview 팝업이 있는 쇼퍼블 배너입니다. 사용자는 모델의 원 또는 &quot;핫스팟&quot;을 눌러 Quickview를 활성화합니다.

![chlimage_1-152](assets/chlimage_1-368.png)

다음 페이지로 이동하여 위의 웹 페이지에서 인터랙티브한 이미지를 확인할 수 있습니다.

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html)

## 인터랙티브한 이미지 배너를 만드는 방법 보기 {#watch-how-interactive-image-banners-are-created}

인터랙티브한 이미지 배너를 만드는 [방법에 대한 10분 33초의 연습을 시청하십시오](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner). 또한 인터랙티브한 이미지 배너를 미리 보고 편집 및 전달하는 방법을 살펴볼 수 있습니다.

## 빠른 시작: 인터랙티브한 이미지 {#quick-start-interactive-images}

다음 단계별 워크플로우 설명은 AEM Assets에서 인터랙티브한 이미지를 빠르게 시작하고 실행하는 데 도움이 되도록 설계되었습니다.

빠른 시작 작업 **의 일부** 내에서 예제 머리글을 찾습니다. 여기에는 아직 대화형 이미지가 추가되지 않은 다음 웹 페이지 예제를 기반으로 한 간단한 자습서가 포함되어 있습니다.

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html)

이 자습서는 자신의 웹 사이트에서 대화형 이미지를 통합하는 단계를 보여주는 데 도움이 됩니다.

대화형 이미지 단계:

1. **(선택 사항) 핫스팟 변수** 식별 - AEM Assets 및 Dynamic Media 독립 실행형 항목을 사용하는 경우, 대화형 이미지를 만들 때 핫스팟 데이터를 입력할 수 있도록 기존 Quickview 구현에서 사용되는 동적 변수를 식별하여 시작합니다. 핫스팟 [변수 식별을 참조하십시오(선택 사항)](#optional-identifying-hotspot-variables).
그러나 AEM Sites, AEM eCommerce 또는 두 가지 모두를 사용하는 경우에는 이 단계가 필요하지 않습니다.
AEM Assets [의 e커머스 개념을 참조하십시오](/help/sites-administering/concepts.md).

1. **(선택 사항) 대화형 이미지 뷰어 사전 설정** 만들기 - 핫스팟을 나타내는 데 사용되는 그래픽 이미지를 사용자 지정합니다. 기본 대화형 이미지 뷰어 사전 설정을 대신 사용하려면 직접 대화형 이미지 뷰어 사전 설정을 만들 필요가 `Shoppable_Banner` 없습니다.
대화형 [이미지 뷰어 사전 설정 만들기를 참조하십시오](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset).

1. **이미지 배너** 업로드 - 대화형으로 만들 이미지 배너를 업로드합니다.
이미지 배너 [업로드를 참조하십시오](#uploading-an-image-banner).

1. **이미지 배너에 핫스팟 추가** - 이미지 배너에 하나 이상의 핫스팟을 추가하고 각 핫스팟을 하이퍼링크, 빠른 보기 또는 경험 조각 등의 동작과 연결합니다. 핫스팟을 추가한 후 대화형 이미지를 게시하여 이 작업을 완료합니다.
이미지 [배너에 핫스팟 추가를 참조하십시오](#adding-hotspots-to-an-image-banner).
대화형 이미지 [미리 보기](#optional-previewing-interactive-images) - 선택 사항을 참조하십시오. 원하는 경우 쇼퍼블 배너의 표현을 보고 인터랙션을 테스트할 수 있습니다.
대화형 [이미지 자산을 게시하는 방법에 대한 자세한 내용은 자산](/help/assets/publishing-dynamicmedia-assets.md) 게시를 참조하십시오.

1. **AEM에서 웹 사이트 또는 웹 사이트에 대화형 이미지 추가** AEM Sites, AEM eCommerce 또는 둘 다를 사용하는 경우, 대화형 미디어 구성 요소를 페이지로 드래그하여 AEM의 웹 페이지에 직접 대화형 이미지를 추가할 수 있습니다. See [Adding Dynamic Media Assets to Pages.](/help/assets/adding-dynamic-media-assets-to-pages.md)
AEM Assets 및 Dynamic Media 독립 실행형 제품을 사용하는 경우 웹 사이트에 포함 코드를 복사한 다음 기존 Quickview와 통합해야 합니다. 웹 사이트 [와 대화형 이미지 통합을 참조하십시오](#integrating-an-interactive-image-with-your-website).
타사 WCM(Web Content Manager)을 사용하는 경우, 새 대화형 비디오를 웹 사이트에서 사용되는 기존 Quickview 구현과 통합해야 합니다. 기존 [Quickview와 대화형 이미지 통합을 참조하십시오](#integrating-an-interactive-image-with-an-existing-quickview).

## (선택 사항) 핫스팟 변수 식별 {#optional-identifying-hotspot-variables}

>[!NOTE]
>
>이 작업은 다음과 같은 경우에만 필요합니다.
>
>* Quickviews에 트리거하여 이미지에 인터랙티브한 요소를 추가하려고 합니다.
>* AEM을 구현해도 IBM Websphere Commerce, Elastic Path, hybris 또는 Intershop과 같은 전자 상거래 솔루션에서 제품 데이터를 AEM으로 가져오는 데 eCommerce 통합 프레임워크를 사용하지 *않습니다* . AEM Assets [의 e커머스 개념을 참조하십시오](/help/sites-administering/concepts.md).

>
>
AEM 구현에서 e커머스를 사용하는 경우 이 작업을 건너뛰고 다음 작업으로 진행할 수 있습니다.

먼저 핫스팟 데이터를 입력하여 대화형 이미지를 만들 수 있도록 기존 Quickview 구현에서 사용하는 동적 변수를 식별합니다.

AEM Assets의 배너 이미지에 핫스팟을 추가할 때 SKU(Stock Keeping Unit; 각 고유 제품 또는 서비스에 대한 고유 식별자) 및 각 핫스팟에 대한 선택적 추가 변수. 이러한 핫스팟 변수는 나중에 Quickview 컨텐츠와 핫스팟을 일치시키는 데 사용됩니다.

핫스팟 데이터와 연결할 변수의 수와 유형을 적절히 식별해야 합니다. 배너 이미지에 추가된 각 핫스팟은 기존 백엔드 시스템에서 제품을 명확하게 식별할 수 있도록 충분한 정보를 전달해야 합니다.

핫스팟 데이터에 사용할 변수 집합을 식별하는 다른 방법이 있습니다.

시스템에서 Quickview를 식별하는 데 필요한 최소 데이터 세트가 무엇인지 알 수 있으므로 기존 Quickview 구현을 담당하는 IT 전문가와 상담하는 데 충분할 수 있습니다. 그러나 대부분의 경우 프런트 엔드 코드의 기존 동작을 간단하게 분석할 수도 있습니다.

대부분의 Quickview 구현은 다음과 같은 패러다임을 사용합니다.

* 사용자는 웹 사이트에서 사용자 인터페이스 요소를 활성화합니다. 예를 들어 &quot;빠른 보기&quot; 단추를 클릭합니다.
* 필요한 경우 웹 사이트에서 Quickview 데이터 또는 컨텐츠를 로드하기 위해 Ajax 요청을 백엔드에 보냅니다.
* Quickview 데이터는 웹 페이지에서 렌더링하기 위해 컨텐츠로 변환됩니다.
* 마지막으로 프런트 엔드 코드는 이러한 컨텐츠를 화면에 시각적으로 렌더링합니다.

그런 다음 빠른 보기 기능이 구현된 기존 웹 사이트의 다양한 영역을 방문하고, 빠른 보기를 트리거하고, Quickview 데이터 또는 컨텐츠를 로드하기 위해 웹 페이지에서 보낸 Ajax URL을 캡처하는 방법을 살펴봅니다.

일반적으로 전문적인 디버깅 도구를 사용할 필요가 없습니다. 최신 웹 브라우저에는 적절한 작업을 수행하는 웹 관리자가 포함되어 있습니다. 다음은 웹 관리자를 포함하는 웹 브라우저의 몇 가지 예입니다.

* Google Chrome에서 나가는 HTTP 요청을 모두 보려면 F12를 눌러 개발자 도구 패널을 연 다음 네트워크 탭을 클릭합니다.
Mac에서 Command+Option+I를 눌러 개발자 도구 패널을 연 다음 네트워크 탭을 클릭합니다.

* Firefox에서는 F12를 눌러 Firebug 플러그인을 활성화하고 Net 탭을 사용하거나 내장 검사기 도구 및 네트워크 탭을 사용할 수 있습니다.
Mac에서 Command+Option+I를 눌러 개발자 도구 패널을 연 다음 검사기 탭을 클릭합니다.

브라우저에서 네트워크 모니터링이 켜지면 페이지의 빠른 보기를 트리거합니다.

이제 네트워크 로그에서 Quickview Ajax URL을 찾아 기록된 URL을 복사하여 이후 분석을 수행합니다. Quickview를 트리거하는 대부분의 경우 서버로 전송되는 요청이 많습니다. 일반적으로 빠른 보기 Ajax URL은 목록의 첫 번째 URL 중 하나입니다. 복잡한 쿼리 문자열 부분이나 경로가 있으며 응답 MIME 유형은 `text/html`, `text/xml`또는 `text/javascript`입니다.

이 과정 중에는 제품 카테고리 및 유형이 다른 웹 사이트의 여러 영역을 방문하는 것이 중요합니다. Quickview URL에는 지정된 웹 사이트 카테고리에 공통인 부분이 있을 수 있지만 웹 사이트의 다른 영역을 방문하는 경우에만 변경될 수 있습니다.

가장 간단한 경우 Quickview URL의 유일한 변수 부분은 제품 SKU입니다. 이 경우 SKU 값은 배너 이미지에 핫스팟을 추가하는 데 필요한 유일한 데이터 조각입니다.

하지만 복잡한 경우 Quickview URL에는 카테고리 ID, 색상 코드, 크기 코드 등과 같은 SKU 외에도 다양한 요소가 있습니다. 이러한 경우 모든 요소는 AEM Assets에서 쇼퍼블 인터랙티브 이미지 기능에 있는 핫스팟 데이터 정의에 있는 별도의 변수입니다.

Quickview URL 및 결과 핫스팟 변수의 다음 예를 생각해 보십시오.

<table>
  <tbody>
  <tr>
    <td><p>쿼리 문자열에 있는 단일 SKU입니다.</p> </td>
    <td><p>기록된 Quickview URL에는 다음이 포함됩니다.</p>
    <ul>
      <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>URL에 있는 유일한 변수 부분은 productId= 쿼리 문자열 매개 변수의 값이며 SKU 값입니다. 따라서, 핫스팟에는 값, <strong><code>866558</code></strong>, <strong><code>1196184</code></strong>등의 SKU 필드만 <strong><code>1081492</code></strong><strong><code>1898294</code></strong>필요합니다.</p> </td>
  </tr>
  <tr>
    <td><p>URL 경로에 있는 단일 SKU입니다.</p> </td>
    <td><p>기록된 Quickview URL에는 다음이 포함됩니다.</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>변수 부분은 경로의 마지막 부분에 있으며 핫스팟의 SKU 값이 됩니다. <strong><code>6422350843</code></strong>, <strong><code>1607745002</code></strong>, <strong><code>0086724882</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>쿼리 문자열에서 SKU 및 카테고리 ID.</p> </td>
    <td><p>기록된 Quickview URL에는 다음이 포함됩니다.</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>이 경우 URL에 서로 다른 두 부분이 있습니다. SKU는 매개 변수에 저장되고 카테고리 ID는 <code>prodId</code> 매개 변수에<code></code> <code>category=</code> 저장됩니다.</p> <p>이와 같이 핫스팟 정의는 쌍입니다. 즉, SKU 값과 <code>categoryId</code> 결과 쌍은 다음과 같습니다.</p>
    <ul>
      <li><p>SKU는 <strong><code>305466</code></strong> 및 <code>categoryId</code> 입니다 <code>1100004</code>.</p> </li>
      <li><p>SKU는 <strong><code>310181</code></strong> 및 <code>categoryId</code> 입니다 <strong><code>1100004</code></strong>.</p> </li>
      <li><p>SKU는 <strong><code>308706</code></strong> 및 <code>categoryId</code> 입니다 <strong><code>1740148</code></strong>.</p> </li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**예**

위의 세 가지 예에서 사용한 것과 동일한 접근 방법을 데모 웹 페이지에 적용할 수 있습니다.

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html)

데모 웹 페이지에는 각각 &quot;자세히 보기&quot;라는 빠른 보기 단추가 있는 여러 제품 축소판이 있습니다. 웹 브라우저의 디버깅 도구가 여전히 활성화된 상태에서 각 단추를 클릭하고 기록된 빠른 보기 URL을 기록합니다. 페이지에서 사용 가능한 4개의 제품 Quickviews를 모두 활성화한 후 백엔드에 대한 Quickview 요청 목록이 다음과 같습니다.

* `/datafeed/Men-Windbreaker.json`
* `/datafeed/Men-SimpleHenley.json`
* `/datafeed/Men-CamoPullover.json`
* `/datafeed/Women-QuiltedDownJacket.json`

이러한 서버 호출을 보면 제품 특정 정보가 요청 경로에만 있음을 알 수 있습니다. 쿼리 문자열은 전혀 사용되지 않으며 관련된 두 가지 유형의 데이터가 있습니다.

* 첫 번째 유형은 남성 또는 여성입니다. 이를 &quot;제품 카테고리&quot;라고 할 수 있습니다.
* 두 번째 유형은 CamoPullover와 같은 제품 이름입니다. 제품 SKU라고 가정할 수 있습니다.

이 정보가 주어지면 전체 Quickview URL에는 다음 패턴이 있습니다.

`/datafeed/$categoryId$-$SKU$.json`

이러한 분석을 기반으로 핫스팟을 사용하고 `categoryId``SKU` 는

이제 AEM Assets에서 쇼퍼블 인터랙티브한 이미지 기능을 사용하여 이미지 배너를 업로드하고 핫스팟을 추가할 준비가 되었습니다.

## (선택 사항) 대화형 이미지 뷰어 사전 설정 만들기 {#optional-creating-an-interactive-image-viewer-preset}

AEM Assets과 함께 제공되는 기본 대화형 이미지 뷰어 사전 설정 `Shoppable_Banner` 을 사용하도록 선택할 수 있습니다. 또는 대화형 이미지에 사용할 사용자 정의 뷰어 사전 설정을 만들 수 있습니다.

사용자 정의 대화형 이미지 뷰어 사전 설정을 만들 때 이미지 배너의 핫스팟 모양을 확인할 수 있습니다. 뷰어 사전 설정 만들기의 일부로 사전 정의된 이미지의 갤러리에서 핫스팟 그래픽을 사용하도록 선택할 수 있습니다.

뷰어 사전 설정을 저장하면 AEM Assets의 뷰어 사전 설정 목록 페이지에서 자동으로 활성화(켜짐)됩니다. 이 기능은 Interactive Media 구성 요소에서 그리고 자산을 볼 때마다 표시되도록 합니다. 그러나 *이 뷰어 사전 설정이 있는 대화형 배너를 *제공하려면 *사용자 정의 뷰어 사전 설정 또는 기본 뷰어 사전 설정의 경우 게시해야 합니다.

**대화형 이미지 뷰어 사전 설정을 만들려면**

1. 왼쪽 레일에서 **[!UICONTROL 도구 > 자산 > 뷰어 사전 설정을 누릅니다.]**
1. Near the upper-right corner of the page, tap **[!UICONTROL Create.]**
1. [새 뷰어 사전 설정] 대화 상자에서 대화형 배너 뷰어 사전 설정을 설명하는 이름을 입력합니다.

   저장 후 뷰어 사전 설정 목록 페이지에 표시되는 제목입니다.

1. 리치 미디어 유형 풀다운 메뉴에서 **[!UICONTROL 대화형 이미지를 선택합니다.]**
1. 만들기를 **[!UICONTROL 누릅니다.]**
1. 뷰어 사전 설정 편집 페이지에서 모양 **[!UICONTROL 탭을]** 누릅니다.
1. 다음 중 하나를 수행하십시오.

   * 이미지에 사용할 자체 핫스팟 이미지를 업로드하려면 자산 선택기 아이콘을 누릅니다. 컨텐츠 선택 페이지에서 사용할 핫스팟 이미지로 이동하고 선택한 다음 오른쪽 위 모서리에 있는 표시 확인 아이콘을 누릅니다.
   * 사전 정의된 핫스팟 이미지를 선택하려면 핫스팟 갤러리 아이콘을 누릅니다. 핫스팟 갤러리 팔레트에서 사용할 핫스팟 이미지를 누릅니다.

1. Near the upper-right corner of the page, tap **[!UICONTROL Save.]**

   새 뷰어 사전 설정을 게시해야 합니다.

   추가한 [Publishing Viewer 사전 설정을 참조하십시오](/help/assets/managing-viewer-presets.md#publishing-viewer-presets).

   이제 이미지 배너를 업로드할 준비가 되었습니다.

## 이미지 배너 업로드 {#uploading-an-image-banner}

사용할 이미지를 이미 업로드한 경우 다음 단계로 진행합니다. 이미지 배너에 [핫스팟 추가](#adding-hotspots-to-an-image-banner).

**이미지 배너를 업로드하려면**

1. 인터랙티브하게 만들 이미지 배너를 업로드합니다.

   See [Uploading assets](/help/assets/managing-assets-touch-ui.md#uploading-assets).

   이제 이미지 배너에 핫스팟을 추가할 준비가 되었습니다. 아래의 다음 작업을 참조하십시오.

## 이미지 배너에 핫스팟 추가 {#adding-hotspots-to-an-image-banner}

핫스팟 관리 페이지의 편집기를 사용하여 이미지 배너에 핫스팟을 추가할 수 있습니다.

핫스팟을 추가할 때 빠른 보기 팝업 표시, 하이퍼링크 또는 경험 조각으로 정의할 수 있습니다.

경험 [조각을 참조하십시오](/help/sites-authoring/experience-fragments.md).

>[!NOTE]
>
>경험 조각에 뷰어를 포함할 때는 대화형 이미지의 소셜 미디어 공유 도구가 지원되지 않는다는 점을 참고하십시오. 이 문제를 해결하려면 소셜 미디어 공유 도구가 없는 뷰어 사전 설정을 사용하거나 만들 수 있습니다. 이러한 뷰어 사전 설정을 사용하면 경험 조각에 성공적으로 포함할 수 있습니다.

페이지의 오른쪽 위 모서리 근처에 있는 실행 취소 및 재실행 옵션은 현재 생성/편집 세션 동안 지원됩니다.

인터랙티브한 이미지 작성을 마치면 [미리 보기]를 사용하여 대화형 이미지가 고객에게 어떻게 표시되는지 확인할 수 있습니다.

자세한 내용은 [(선택 사항) 대화형 이미지 미리 보기를 참조하십시오](#optional-previewing-interactive-images).

>[!NOTE]
>
>대화형 이미지 또는 회전 배너의 이미지에 핫스팟을 추가하면 핫스팟 정보는 대화형 이미지 또는 회전 메뉴 배너의 여부와 관계없이 동일한 메타데이터 위치(이미지의 위치를 기준으로)에 저장됩니다. 이 기능은 두 뷰어 모두에서 동일한 이미지를 정의된 핫스팟 데이터와 함께 쉽게 다시 사용할 수 있음을 의미합니다.

>그러나 회전판 배너는 핫스팟도 포함될 수 있는 이미지에서 이미지 맵을 지원합니다. 대화형 이미지는 그렇지 않습니다. 동일한 이미지를 사용하는 대화형 이미지 또는 회전 배너를 만들려는 경우 주의하십시오. 대신 동일한 이미지의 개별 사본을 사용하여 대화형 이미지 및 회전 배너를 만들 수 있습니다.
>
>회전판 [배너를 참조하십시오](/help/assets/carousel-banners.md).

>[!NOTE]
>
>핫스팟이 있는 대화형 이미지를 편집하고 이미지를 자르면 핫스팟이 제거됩니다.

**이미지 배너에 핫스팟을 추가하려면**

1. 자산 보기에서 대화형으로 만들 이미지 배너로 이동합니다.
1. 다음 중 하나를 수행하십시오.

   * 이미지를 마우스로 가리킨 다음 **[!UICONTROL 선택]** (확인 표시 아이콘)을 누릅니다. 도구 모음에서 **[!UICONTROL 편집을 누릅니다.]**

   * 이미지를 마우스로 가리킨 다음 **[!UICONTROL 추가 작업]** (세 점 아이콘) **[!UICONTROL > 편집을 누릅니다.]**

   * 이미지를 눌러 세부 사항 보기 페이지에서 엽니다. 도구 모음에서 **[!UICONTROL 편집을 누릅니다.]**

1. 페이지의 왼쪽 위 모서리 근처에 있는 핫스팟 **[!UICONTROL 추가]** (손가락 탭 아이콘)를 눌러 핫스팟 관리 페이지를 엽니다.
1. 페이지의 왼쪽 위 모서리 근처에 있는 핫스팟을 **[!UICONTROL 누릅니다.]**

1. [핫스팟 관리] 페이지의 왼쪽 위 모서리 근처에 있는 핫스팟을 **[!UICONTROL 탭합니다.]**
1. 이미지에서 핫스팟을 표시할 위치를 누릅니다. 필요한 경우 핫스팟을 드래그하여 위치를 조정합니다.
1. a 및 b 단계를 반복하여 필요에 따라 핫스팟을 추가합니다.
1. (선택 사항) 핫스팟을 삭제하려면 이미지에서 핫스팟을 선택한 다음 핫스팟 제목 **[!UICONTROL 아래의 삭제]** (가비지 can 아이콘)를 **[!UICONTROL 누릅니다]** .

1. 이름 텍스트 필드에 핫스팟 이름을 입력합니다. 이 이름은 선택한 핫스팟 드롭다운 목록에도 나타납니다.
1. 다음 중 하나를 수행하십시오.

   * 빠른 보기를 **[!UICONTROL 누릅니다.]**

      * AEM Sites 또는 전자 상거래 고객인 경우 제품 선택기 아이콘(확대경)을 탭하거나 클릭하여 제품 선택 페이지를 엽니다. 사용할 제품을 탭하거나 클릭한 다음 페이지의 오른쪽 위 모서리에 있는 **Select **를 탭하여 핫스팟 관리 페이지로 돌아갑니다.
      * AEM Sites 또는 전자 상거래 고객이 *아닌* 경우

         * 핫스팟 [변수 식별을 참조하십시오](#optional-identifying-hotspot-variables). 이러한 변수를 정의해야 합니다.
         * 그런 다음 SKU 값을 직접 입력합니다. SKU 값 텍스트 필드에 제공하는 각 개별 제품 또는 서비스에 대한 고유 식별자인 제품의 SKU(Stock Keeping Unit)를 입력합니다. 입력된 SKU 값은 시스템이 탭된 핫스팟을 특정 SKU의 Quickview와 연결할 수 있도록 빠른 보기 템플릿의 변수 부분을 자동으로 채웁니다.
         * (선택 사항) Quickview 내에 제품을 추가로 식별하기 위해 사용해야 하는 다른 변수가 있는 경우 일반 변수 **[!UICONTROL 추가를 누릅니다.]** 텍스트 필드에 추가 변수를 지정합니다. 예를 들어, 는 추가된 변수 `category=Mens` 입니다.
   * 하이퍼링크를 **[!UICONTROL 누릅니다.]**

      * AEM Sites 고객인 경우 사이트 선택기 아이콘(폴더)을 탭하거나 클릭하여 URL로 이동합니다. 인터랙티브 컨텐츠에 상대 URL이 있는 링크, 특히 AEM Sites 페이지에 대한 링크가 있는 경우에는 URL 기반 연결 방법이 지원되지 않습니다.
      * 독립 실행형 고객인 경우 HREF 텍스트 필드에 연결된 웹 페이지의 전체 URL 경로를 지정합니다.

   링크를 새 브라우저 탭(권장 기본값)에서 열지 또는 동일한 탭에서 열지를 지정해야 합니다.

   자세한 [내용은 선택기](/help/assets/working-with-selectors.md) 작업을 참조하십시오.

   * 경험 **[!UICONTROL 조각을 누릅니다.]**

      * AEM Sites 고객인 경우 검색 아이콘(확대경)을 탭하거나 클릭하여 경험 조각 페이지를 엽니다. 사용할 경험 조각을 탭하거나 클릭한 다음 페이지의 오른쪽 위 모서리에 있는 선택을 탭하여 핫스팟 관리 페이지로 돌아갑니다.
경험 [조각을 참조하십시오](/help/sites-authoring/experience-fragments.md).

      * 배너에 표시될 경험 조각의 폭과 높이를 지정합니다.

         >[!NOTE]
         >
         >경험 조각에 뷰어를 포함할 때는 대화형 이미지의 소셜 미디어 공유 도구가 지원되지 않는다는 점을 참고하십시오. 이 문제를 해결하려면 소셜 미디어 공유 도구가 없는 뷰어 사전 설정을 사용하거나 만들 수 있습니다. 이러한 뷰어 사전 설정을 사용하면 경험 조각에 성공적으로 포함할 수 있습니다.



1. 저장을 **[!UICONTROL 눌러]** 작업을 저장하고 검색 페이지로 돌아갑니다.
1. 대화형 이미지를 게시합니다. 게시를 사용하면 클라우드를 통해 배너를 전달할 수 있으며 타사 웹 사이트와 통합해야 하는 경우 포함 코드도 생성합니다.

   자산 [게시를 참조하십시오](/help/assets/managing-assets-touch-ui.md#publishing-assets).

   이제 핫스팟을 추가하고 대화형 이미지를 게시한 후 기존 웹 사이트에 추가할 수 있습니다.

   웹 사이트 [와 대화형 이미지 통합을 참조하십시오](#integrating-an-interactive-image-with-your-website).

   >[!NOTE]
   >
   >핫스팟이 있는 대화형 이미지를 편집하고 이미지를 자르면 핫스팟이 삭제됩니다.

### (선택 사항) 대화형 이미지 미리 보기 {#optional-previewing-interactive-images}

[미리 보기]를 사용하여 대화형 이미지가 고객에게 어떻게 보이는지 표시하고 이미지의 핫스팟을 테스트하여 예상대로 작동하는지 확인할 수 있습니다.

인터랙티브한 이미지가 마음에 들면 게시할 수 있습니다.
See [Embedding the Video or Image Viewer on a Web Page](/help/assets/embed-code.md).
See [Linking URLs to your web application](/help/assets/linking-urls-to-yourwebapplication.md). 인터랙티브 컨텐츠에 상대 URL이 있는 링크, 특히 AEM Sites 페이지에 대한 링크가 있는 경우에는 URL 기반 연결 방법이 지원되지 않습니다.
See [Adding Dynamic Media Assets to Pages.](/help/assets/adding-dynamic-media-assets-to-pages.md)

**대화형 이미지를 미리 보려면**

1. 자산 보기에서 만든 기존 대화형 이미지로 이동하고 을 눌러 미리 보기에서 엽니다.
1. 미리 보기 페이지의 왼쪽 위 모서리 근처에 있는 컨텐츠 드롭다운 목록에서 뷰어를 **[!UICONTROL 누릅니다.]**
1. [뷰어] 목록에서 **[!UICONTROL Shopperable_Banner]** 또는 만든 대화형 이미지 뷰어 사전 설정의 이름을 누릅니다.
1. 이미지의 핫스팟을 탭하여 연결된 동작을 테스트합니다.

## 인터랙티브한 이미지 에셋 게시 {#publishing-interactive-image-assets}

대화형 [이미지 자산을 게시하는 방법에 대한 자세한 내용은 자산](/help/assets/publishing-dynamicmedia-assets.md) 게시를 참조하십시오.

## 웹 사이트와 인터랙티브한 이미지 통합 {#integrating-an-interactive-image-with-your-website}

배너 이미지를 업로드하고, 이미지에 핫스팟을 추가하고, 대화형 이미지를 게시한 후 이제 웹 사이트 페이지에 추가할 준비가 되었습니다.

AEM Sites 고객인 경우 대화형 미디어 구성 요소를 페이지로 드래그하여 대화형 이미지를 추가할 수 있습니다. See [Adding Dynamic Media Assets to Pages.](/help/assets/adding-dynamic-media-assets-to-pages.md)

독립 실행형 AEM Assets 고객인 경우 이 섹션에 설명된 대로 웹 사이트에 대화형 이미지를 수동으로 추가할 수 있습니다.

1. 게시된 대화형 이미지의 포함 코드를 복사합니다.
See [Embedding the Video or Image Viewer on a Web Page](/help/assets/embed-code.md).

1. 복사한 포함 코드를 웹 페이지 내의 원하는 위치에 추가합니다.
복사된 포함 코드는 지정된 영역에 자동으로 맞게 반응형 환경을 위해 설정되어 있습니다.

**예**

데모 웹 사이트를 예로 사용:

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html)

세 사람의 사진은 정적인 `IMG` 태그이다.

```xml
<img class="img-responsive" width="100%" title="Hero Image 2" alt="Hero Image 2" src="images/shoppable-banner.jpg">
```

통합은 태그를 제거하고 AEM Assets에서 복사한 포함 코드로 바꾸는 것만큼 간단합니다. `IMG` 다음 URL에서 세 개의 서클 핫스팟이 있는 페이지에서 쇼퍼블 인터랙티브한 이미지를 보여 주는 결과를 볼 수 있습니다.

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-1.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-1.html)

>[!NOTE]
>
>이 시점에서 데모 웹 사이트의 쇼퍼블 인터랙티브 이미지에 있는 핫스팟은 표시 용도로만 사용됩니다. 이러한 지표는 아직 기존 빠른 보기와 통합되지 않았습니다.

응답형 환경을 위해 쇼퍼블 방식의 인터랙티브한 이미지에 &quot;자르기&quot;를 적용하려면 경로에 인터랙티브한 이미지 구성 속성 `ZoomView.iscommand` 을 포함시킬 수 있습니다. 여기서 호출해야 할 구성 요소이고 `ZoomView` `iscommand` 적용하는 &quot;자르기&quot; 이미지 제공 명령입니다.

ZoomView.iscommand [구성 속성을](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/r_html5_aem_interactive_image_config_attrib_zoomview_iscommand.html) 참조하십시오.

자르기 [이미지 제공 명령을](https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/http_ref/r_crop.html) 참조하십시오.

이제 인터랙티브한 이미지를 웹 사이트의 기존 Quickview와 통합할 수 있습니다.

## 기존 Quickview와 대화형 이미지 통합 {#integrating-an-interactive-image-with-an-existing-quickview}

>[!NOTE]
>
>이 작업은 사용자가 독립 실행형 AEM Assets 고객인 경우에만 적용됩니다.

이 프로세스의 마지막 단계는 대화형 이미지를 웹 사이트의 기존 Quickview 구현과 통합하는 것입니다. 모든 경우에 작동하는 통합에 대한 해결책은 없습니다. 모든 Quickview 구현은 고유하며 프런트 엔드 IT 담당자의 지원을 필요로 하는 특정 접근 방식이 필요합니다.

기존 Quickview 구현은 일반적으로 웹 페이지에서 다음 순서로 발생하는 관련 작업 체인을 나타냅니다.

1. 사용자는 웹 사이트의 사용자 인터페이스에 있는 요소를 트리거합니다.
1. 프런트 엔드 코드는 1단계에서 트리거된 사용자 인터페이스 요소를 기반으로 빠른 보기 URL을 가져옵니다.
1. 프런트 엔드 코드는 2단계에서 얻은 URL을 사용하여 Ajax 요청을 전송합니다.
1. 백엔드 로직은 해당 Quickview 데이터 또는 컨텐츠를 프런트 엔드 코드로 다시 반환합니다.
1. 프런트 엔드 코드는 Quickview 데이터 또는 컨텐츠를 로드합니다.
1. 필요한 경우, 프런트 엔드 코드는 로드된 Quickview 데이터를 HTML 표시로 변환합니다.
1. 프런트 엔드 코드는 모달 대화 상자나 패널을 표시하고 최종 사용자를 위해 화면에 HTML 컨텐츠를 렌더링합니다.

이러한 호출은 임의의 단계에서 웹 페이지 로직에서 호출할 수 있는 독립 공개 API 호출을 나타내지 않을 수 있습니다. 대신, 이 호출은 이전 단계의 마지막 단계(콜백)에서 모든 다음 단계가 숨겨지는 연쇄 호출입니다.

동시에 쇼퍼블 인터랙티브한 이미지가 1단계와 2단계를 부분적으로 대체하는 경우 사용자가 쇼퍼블 이미지 내에서 핫스팟을 클릭하면 해당 사용자 상호 작용이 뷰어에서 처리됩니다. 뷰어는 이전에 AEM Assets에 추가한 모든 핫스팟 데이터를 포함하는 웹 페이지에 이벤트를 반환합니다.

이러한 이벤트 핸들러에서 프런트 엔드 코드는 다음을 수행합니다.

* 쇼퍼블 인터랙티브 이미지가 방출하는 이벤트를 수신합니다.
* 핫스팟 데이터를 기반으로 빠른 보기 URL을 생성합니다.
* 백엔드에서 Quickview를 로드하고 표시하기 위해 화면에 렌더링하는 프로세스를 트리거합니다.

AEM Assets에서 반환되는 포함 코드에는 이미 다음 강조 표시된 코드 조각에서와 같이 주석으로 처리된 즉시 사용할 수 있는 이벤트 핸들러가 있습니다.

```xml
        var s7interactiveimageviewer = new s7viewers.InteractiveImage({
            "containerId" : "s7interactiveimage_div",
            "params" : {
                "serverurl" : "https://aodmarketingna.assetsadobe.com/is/image",
                "contenturl" : "https://aodmarketingna.assetsadobe.com/",
                "config" : "/etc/dam/presets/viewer/Shoppable_Media",
                "asset" : "/content/dam/mac/aodmarketingna/shoppable-banner/shoppable-banner.jpg" }
        })
        /* // Example of interactive image event for Quickview.
             s7interactiveimageviewer.setHandlers({
                "quickViewActivate": function(inData) {
                    var sku=inData.sku; //SKU for product ID
                    //To pass other parameter from the hotspot, you will need to add custom parameter during the hotspot setup as parameterName=value
                    loadQuickView(sku); //Replace this call with your Quickview plugin
                    //Please refer to your Quickviewer plugin for the Quickview call
                 },
             });
        */
        s7interactiveimageviewer.init();
```

따라서, 코드의 주석을 해제하고 더미 처리기 본문을 특정 웹 페이지에 맞는 코드로 바꾸는 것만 필요합니다.

Quickview URL을 구성하는 프로세스는 기본적으로 앞에서 설명한 핫스팟 변수를 식별하는 데 사용되는 프로세스와 반대됩니다.

핫스팟 [변수 식별을 참조하십시오](#optional-identifying-hotspot-variables).

이전 Quickview URL 예제를 사용하여 다음 예에서 각 케이스에서 Quickview URL이 구성되는 방식을 확인할 수 있습니다.

<table>
 <tbody>
  <tr>
   <td><p>쿼리 문자열에 있는 단일 SKU</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/json?productId=" + inData.sku + "&amp;amp;source=100";
      },
      });</code></td>
  </tr>
  <tr>
   <td><p>URL 경로에 있는 단일 SKU</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/product/" + inData.sku;
      },
      });</code></td>
  </tr>
  <tr>
   <td><p>쿼리 문자열의 SKU 및 카테고리 ID</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/quickView/product/?category=" + inData.categoryId + "&amp;amp;prodId=" + inData.sku;
      },
      });</code></td>
  </tr>
 </tbody>
</table>

Quickview URL을 트리거하고 Quickview 패널을 활성화하는 마지막 단계는 IT 부서의 프런트 엔드 IT 담당자의 지원이 필요합니다. 이들은 즉시 사용할 수 있는 Quickview URL을 사용하여 적절한 단계에서 Quickview 구현을 정확하게 트리거하는 방법을 가장 잘 알고 있습니다.

이러한 단계를 데모 웹 사이트에 적용하여 쇼퍼블 인터랙티브한 이미지를 Quickview 코드와 완벽하게 통합하는 방법을 확인할 수 있습니다. 이전에는 빠른 보기 URL의 구조가 다음과 같이 확인되었습니다.

```xml
/datafeed/$categoryId$-$SKU$.json
```

핸들러 내에서 이 URL을 재구성하려면 `quickViewActivate` 뷰어의 코드로 핸들러로 전달되는 `categoryId` 개체에서 사용할 수 있는 `SKU` 및 `inData` 필드를 사용할 수 있습니다.

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

데모 웹 사이트에서 간단한 함수 호출을 사용하여 빠른 보기 대화 상자를 `loadQuickView()` 트리거합니다. 이 함수는 Quickview 데이터 URL인 하나의 인수만 사용합니다. 따라서 쇼퍼블 인터랙티브 이미지를 통합하는 데 필요한 마지막 단계는 다음 코드 줄을 핸들러에 추가하는 것입니다. `quickViewActivate`

```xml
loadQuickView(quickViewUrl);
```

다음은 전체 소스 코드입니다.

```xml
 var s7interactiveimageviewer = new s7viewers.InteractiveImage({
  "containerId" : "s7interactiveimage_div",
  "params" : {
   "serverurl" : "https://aodmarketingna.assetsadobe.com/is/image",
   "contenturl" : "https://aodmarketingna.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Shoppable_Media",
   "asset" : "/content/dam/mac/aodmarketingna/shoppable-banner/shoppable-banner.jpg" }
 })
   s7interactiveimageviewer.setHandlers({
   "quickViewActivate": function(inData) {
     var sku=inData.sku;
     var categoryId=inData.categoryId;
    var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
    loadQuickView(quickViewUrl);
    },
   });
 s7interactiveimageviewer.init();
```

통합된 인터랙티브한 이미지가 포함된 최종 데모 웹 사이트는 다음과 같습니다.

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-3.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-3.html)

## 빠른 보기를 사용하여 사용자 지정 팝업 만들기 {#using-quickviews-to-create-custom-pop-ups}

See [Using Quickviews to create custom pop-ups](/help/assets/custom-pop-ups.md).
