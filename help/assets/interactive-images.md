---
title: 대화형 이미지
description: Dynamic Media에서 대화형 이미지로 작업하는 방법 알아보기
uuid: 0bdb73f7-6ce9-4cdf-b6b5-a4d3d4e19a23
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: a6f58f6a-015a-4ced-941c-ef1b6d3e1d6f
docset: aem65
feature: 대화형 이미지
role: Business Practitioner, Administrator
exl-id: 8a609024-e9e6-4805-8306-48d095110eb6
source-git-commit: 1cef6f87fa66fd78d439c23e6ac907f9531b8fd6
workflow-type: tm+mt
source-wordcount: '4332'
ht-degree: 0%

---

# 대화형 이미지{#interactive-images}

이미지에 &quot;쇼퍼블&quot; 핫스팟을 끌어다 놓아 고객을 위한 정적 이미지가 풍부하고 매력적인 경험으로 쉽게 만들 수 있습니다. 쇼퍼블 핫스팟은 제품 또는 서비스에 대한 추가 정보를 직접 판매 지점 &quot;장바구니에 추가&quot; 또는 &quot;구매&quot; 기능과 결합합니다. 고객은 이러한 핫스팟을 탭하거나 클릭하고 제품이나 서비스에 직접 연결되거나, 장바구니에 추가하거나, 웹 페이지에 연결할 수 있습니다. 이러한 직접 경험은 웹 사이트에서 고객 참여 및 전환을 증가시킵니다.

다음은 Quickview 팝업이 있는 쇼퍼블 배너입니다. 사용자가 모델에서 원 또는 &quot;핫스팟&quot;을 탭하여 빠른 보기를 활성화합니다.

![chlimage_1-152](assets/chlimage_1-368.png)

다음 위치로 이동하여 위의 웹 페이지에서 대화형 이미지를 참조하십시오.

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html)

## 대화형 이미지 배너가 만들어지는 방법을 확인하십시오 {#watch-how-interactive-image-banners-are-created}

[대화형 이미지 배너를 만드는 방법에 대한 10분 및 33초 연습을 시청하십시오](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner). 또한 대화형 이미지 배너를 미리 보고 편집하고 전달하는 방법을 알아봅니다.

## 빠른 시작:대화형 이미지 {#quick-start-interactive-images}

다음 단계별 워크플로우 설명은 AEM Assets에서 대화형 이미지를 빠르게 시작하고 실행할 수 있도록 설계되었습니다.

일부 빠른 시작 작업 내에서 **예제** 제목을 찾습니다. 여기에 대화형 이미지가 아직 추가되지 않은 다음 웹 페이지 예제를 기반으로 하는 간단한 자습서가 포함되어 있습니다.

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html)

자습서는 자신의 웹 사이트에서 대화형 이미지를 통합하는 단계를 설명하는 데 도움이 됩니다.

대화형 이미지 단계:

1. **(선택 사항) 핫스팟 변수 식별**  - AEM Assets 및 Dynamic Media 독립 실행형을 사용하는 경우 대화형 이미지를 만들 때 핫스팟 데이터를 입력할 수 있도록 기존 Quickview 구현에서 사용되는 동적 변수를 식별하여 시작하십시오. [(선택 사항) 핫스팟 변수 식별](#optional-identifying-hotspot-variables)을 참조하십시오.
그러나 AEM Sites, AEM eCommerce 또는 두 가지 모두를 사용하는 경우 이 단계가 필요하지 않습니다.
AEM Assets](/help/commerce/cif-classic/administering/concepts.md)에서 [eCommerce 개념을 참조하십시오.

1. **(선택 사항) 대화형 이미지 뷰어 사전 설정 만들기**  - 핫스팟을 표시하는 데 사용되는 그래픽 이미지를 사용자 지정합니다. `Shoppable_Banner` 이라는 기본 대화형 이미지 뷰어 사전 설정을 대신 사용하려는 경우에는 대화형 이미지 뷰어 사전 설정을 만들 필요가 없습니다.
[(선택 사항) 대화형 이미지 뷰어 사전 설정 만들기](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset)를 참조하십시오.

1. **이미지 배너 업로드**  - 대화형 이미지를 만들 이미지 배너를 업로드합니다.
[이미지 배너 업로드](#uploading-an-image-banner)를 참조하십시오.

1. **이미지 배너에 핫스팟 추가**  - 이미지 배너에 하나 이상의 핫스팟을 추가하고 각각 하이퍼링크, 빠른 보기 또는 경험 조각과 같은 작업에 연결합니다. 핫스팟을 추가한 후에는 대화형 이미지를 게시하여 이 작업을 완료합니다.

   * [이미지 배너에 핫스팟 추가](#adding-hotspots-to-an-image-banner)를 참조하십시오.
   * [대화형 이미지 미리 보기](#optional-previewing-interactive-images) - 선택 사항 를 참조하십시오. 원할 경우 쇼퍼블 배너의 표현을 보고 상호 작용을 테스트할 수 있습니다.
   * 대화형 이미지 자산을 게시하는 방법에 대한 자세한 내용은 [자산 게시](/help/assets/publishing-dynamicmedia-assets.md) 를 참조하십시오.

1. **AEM Sites, AEM eCommerce 또는**
둘 다 사용하는 경우 AEMI에서 웹 사이트 또는 웹 사이트에 대화형 이미지를 추가하거나, AEM의 웹 페이지에 대화형 이미지를 대화형 미디어 구성 요소를 페이지로 드래그하여 직접 추가할 수 있습니다. [페이지에 Dynamic Media 자산 추가 를 참조하십시오.](/help/assets/adding-dynamic-media-assets-to-pages.md)
AEM Assets 및 Dynamic Media 독립 실행형 을 사용하는 경우 웹 사이트에서 포함 코드를 복사한 다음 기존 Quickview와 통합해야 합니다. [웹 사이트와 대화형 이미지 통합](#integrating-an-interactive-image-with-your-website)을 참조하십시오.
타사 WCM(Web Content Manager)을 사용하는 경우, 새 대화형 비디오를 웹 사이트에서 사용되는 기존 Quickview 구현과 통합해야 합니다. [기존 Quickview](#integrating-an-interactive-image-with-an-existing-quickview)와 대화형 이미지 통합을 참조하십시오.

## (선택 사항) 핫스팟 변수 식별 {#optional-identifying-hotspot-variables}

>[!NOTE]
>
>이 작업은 다음 내용이 true인 경우에만 필요합니다.
>
>* 빠른 보기에 트리거하여 이미지에 상호 작용을 추가하려고 합니다.
>* AEM 구현에서는 IBM Websphere Commerce, Elastic Path, hybris 또는 Intershop과 같은 eCommerce 솔루션에서 제품 데이터를 AEM으로 가져오는 데 eCommerce 통합 프레임워크를 사용하지 *않습니다.* AEM Assets](/help/commerce/cif-classic/administering/concepts.md)에서 [eCommerce 개념을 참조하십시오.

>
>
AEM 구현에서 eCommerce를 사용하는 경우 이 작업을 건너뛰고 다음 작업으로 진행할 수 있습니다.

먼저 핫스팟 데이터를 입력하여 대화형 이미지를 만들 수 있도록 기존 Quickview 구현에서 사용하는 동적 변수를 식별합니다.

AEM Assets에서 배너 이미지에 핫스팟을 추가할 때 SKU(Stock Keeping Unit)를 할당해야 합니다.각 핫스팟에 대한 선택적 추가 변수 및 개별 제품 또는 서비스의 고유 식별자입니다. 이러한 핫스팟 변수는 나중에 Quickview 컨텐츠와 핫스팟을 일치시키기 위해 사용됩니다.

핫스팟 데이터와 연결할 변수의 수와 유형을 올바르게 식별해야 합니다. 배너 이미지에 추가된 각 핫스팟은 기존 백엔드 시스템에서 제품을 명확하게 식별할 수 있도록 충분한 정보를 전달해야 합니다.

핫스팟 데이터에 사용할 변수 집합을 식별하는 다른 방법이 있습니다.

시스템에서 Quickview를 식별하는 데 필요한 최소 데이터 세트를 알 수 있으므로 경우에 따라 기존 Quickview 구현을 담당하는 IT 전문가와 상의하는 것이 충분할 수 있습니다. 그러나 대부분의 경우 프런트 엔드 코드의 기존 동작을 간단히 분석할 수도 있습니다.

대부분의 Quickview 구현은 다음 패러다임을 사용합니다.

* 사용자가 웹 사이트에서 사용자 인터페이스 요소를 활성화합니다. 예를 들어 &quot;빠른 보기&quot; 단추를 클릭합니다.
* 필요한 경우 웹 사이트에서 Quickview 데이터 또는 콘텐츠를 로드하기 위해 백엔드에 Ajax 요청을 보냅니다.
* 빠른 보기 데이터는 웹 페이지에서 렌더링을 준비하기 위해 컨텐츠로 변환됩니다.
* 마지막으로 프런트 엔드 코드는 그러한 콘텐츠를 화면에서 시각적으로 렌더링합니다.

그런 다음 빠른 보기 기능이 구현된 기존 웹 사이트의 다른 영역을 방문하여 빠른 보기를 트리거하고 Quickview 데이터 또는 컨텐츠를 로드하기 위해 웹 페이지에서 보낸 Ajax URL을 캡처하는 것이 좋습니다.

일반적으로 전문 디버깅 도구를 사용할 필요가 없습니다. 최신 웹 브라우저에는 적절한 작업을 수행하는 웹 검사자가 포함되어 있습니다. 다음은 웹 관리자를 포함하는 웹 브라우저의 몇 가지 예입니다.

* Google Chrome에서 나가는 모든 HTTP 요청을 보려면 F12 키를 눌러 개발자 도구 패널을 열고 네트워크 탭을 클릭합니다.
Mac에서 Command+Option+I를 눌러 개발자 도구 패널을 연 다음 네트워크 탭을 클릭합니다.

* Firefox에서는 F12를 눌러 Firebug 플러그인을 활성화하고 Net 탭을 사용하거나 내장 Inspector 도구 및 Network 탭을 사용할 수 있습니다.
Mac에서 Command+Option+I를 눌러 [개발자 도구] 패널을 열고 [검사자] 탭을 클릭합니다.

브라우저에서 네트워크 모니터링이 켜져 있으면 페이지에서 빠른 보기를 트리거합니다.

이제 네트워크 로그에서 Quickview Ajax URL을 찾아 기록된 URL을 복사하여 향후 분석할 수 있습니다. 대부분의 경우 빠른 보기를 트리거할 때 서버로 전송되는 요청이 많습니다. 일반적으로 Quickview Ajax URL은 목록에서 첫 번째 중 하나입니다. 여기에는 복잡한 쿼리 문자열 부분 또는 경로가 있으며 해당 응답 MIME 유형은 `text/html`, `text/xml` 또는 `text/javascript`입니다.

이 프로세스 중에는 다양한 제품 카테고리와 유형을 사용하여 웹 사이트의 다양한 영역을 방문하는 것이 중요합니다. 그 이유는 Quickview URL에 주어진 웹 사이트 카테고리에 공통되는 부분이 있을 수 있지만 웹 사이트의 다른 영역을 방문하는 경우에만 변경되기 때문입니다.

가장 간단한 경우 Quickview URL에 있는 유일한 변수 부분은 제품 SKU입니다. 이 경우 SKU 값은 배너 이미지에 핫스팟을 추가하는 데 필요한 유일한 데이터 조각입니다.

하지만 복잡한 경우, Quickview URL은 카테고리 ID, 색상 코드, 크기 코드 등과 같은 SKU 외에도 다양한 요소를 가지고 있습니다. 이러한 경우 AEM Assets에서 쇼퍼블 대화형 이미지 기능에서 모든 요소는 핫스팟 데이터 정의에서 별도의 변수입니다.

Quickview URL 및 그 결과 핫스팟 변수의 다음 예를 생각해 보십시오.

<table>
  <tbody>
  <tr>
    <td><p>쿼리 문자열에 있는 단일 SKU입니다.</p> </td>
    <td><p>기록된 Quickview URL은 다음과 같습니다.</p>
    <ul>
      <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>URL에서 유일한 변수 부분은 productId= 쿼리 문자열 매개 변수의 값이며 이는 명확하게 SKU 값입니다. 따라서 핫스팟에는 <strong><code>866558</code></strong>, <strong><code>1196184</code></strong>, <strong><code>1081492</code></strong>, <strong><code>1898294</code></strong> 등의 값으로 채워진 SKU 필드만 필요합니다.</p> </td>
  </tr>
  <tr>
    <td><p>URL 경로에 있는 단일 SKU입니다.</p> </td>
    <td><p>기록된 Quickview URL은 다음과 같습니다.</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>변수 부분은 경로의 마지막 부분에 있으며 핫스팟의 SKU 값이 됩니다.<strong><code>6422350843</code></strong>, <strong><code>1607745002</code></strong>, <strong><code>0086724882</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>쿼리 문자열의 SKU 및 카테고리 ID.</p> </td>
    <td><p>기록된 Quickview URL은 다음과 같습니다.</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>이 경우 URL에는 두 가지 다양한 부분이 있습니다. SKU는 <code>prodId</code> 매개 변수에 저장되고 카테고리 ID<code></code>는 <code>category=</code> 매개 변수에 저장됩니다.</p> <p>따라서 핫스팟 정의는 쌍입니다. 즉, SKU 값과 <code>categoryId</code>이라는 추가 변수입니다. 결과 쌍은 다음과 같습니다.</p>
    <ul>
      <li><p>SKU는 <strong><code>305466</code></strong>이고 <code>categoryId</code>는 <code>1100004</code>입니다.</p> </li>
      <li><p>SKU는 <strong><code>310181</code></strong>이고 <code>categoryId</code>는 <strong><code>1100004</code></strong>입니다.</p> </li>
      <li><p>SKU는 <strong><code>308706</code></strong>이고 <code>categoryId</code>는 <strong><code>1740148</code></strong>입니다.</p> </li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**예**

위의 세 예에서 사용된 동일한 접근 방식을 데모 웹 페이지에 적용할 수 있습니다.

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html)

데모 웹 페이지에는 &quot;자세히 보기&quot;라는 빠른 보기 단추가 있는 여러 제품 축소판이 있습니다. 웹 브라우저의 디버깅 도구가 계속 활성화되면 각 단추를 클릭하고 기록된 Quickview URL을 기록해 둡니다. 페이지에서 사용할 수 있는 4개의 제품 빠른 보기를 모두 활성화하면 백엔드에 대해 수행된 Quickview 요청 목록이 있습니다.

* `/datafeed/Men-Windbreaker.json`
* `/datafeed/Men-SimpleHenley.json`
* `/datafeed/Men-CamoPullover.json`
* `/datafeed/Women-QuiltedDownJacket.json`

이러한 서버 호출을 보면 제품별 정보가 요청 경로에만 있음을 알 수 있습니다. 또한 쿼리 문자열이 전혀 사용되지 않으며 두 가지 데이터 유형이 관련되어 있습니다.

* 첫 번째 유형은 남성 혹은 여성입니다. 이를 &quot;제품 카테고리&quot;라고 할 수 있습니다.
* 두 번째 유형은 CamoPullover와 같은 제품 이름입니다. 제품 SKU라고 가정할 수 있습니다.

이 정보가 주어지면 전체 Quickview URL은 다음 패턴을 가집니다.

`/datafeed/$categoryId$-$SKU$.json`

이러한 분석을 기반으로 핫스팟에는 `categoryId` 및 `SKU`을 사용합니다.

이제 AEM Assets에서 쇼퍼블 대화형 이미지 기능을 사용하여 이미지 배너를 업로드하고 핫스팟을 추가할 준비가 되었습니다.

## (선택 사항) 대화형 이미지 뷰어 사전 설정 만들기 {#optional-creating-an-interactive-image-viewer-preset}

AEM Assets과 함께 제공되는 `Shoppable_Banner`이라는 기본 기본 기본 대화형 이미지 뷰어 사전 설정을 사용하도록 선택할 수 있습니다. 또는 대화형 이미지에 사용할 사용자 지정 뷰어 사전 설정을 직접 만들 수도 있습니다.

사용자 정의 대화형 이미지 뷰어 사전 설정을 만들 때 이미지 배너의 핫스팟의 모양을 결정할 수 있습니다. 뷰어 사전 설정 작성 과정의 일부로, 사전 정의된 이미지의 갤러리에서 핫스팟 그래픽을 사용하도록 선택할 수 있습니다.

뷰어 사전 설정을 저장하면 AEM Assets의 뷰어 사전 설정 목록 페이지에서 자동으로 활성화(켜짐)됩니다. 이 기능은 Interactive Media 구성 요소에 표시되고 자산을 볼 때마다 표시됩니다. 그러나 이 뷰어 사전 설정을 사용하는 대화형 배너를 *게재하려면 *뷰어 사전 설정도 게시 *해야 합니다. 이는 사용자 지정 또는 기본 제공 뷰어 사전 설정의 경우 true입니다.

**대화형 이미지 뷰어 사전 설정을 만들려면**

1. 왼쪽 레일에서 **[!UICONTROL 도구 > 자산 > 뷰어 사전 설정 을 누릅니다.]**
1. 페이지의 오른쪽 위 모서리 근처에 있는 **[!UICONTROL 만들기]**&#x200B;를 탭합니다.
1. 새 뷰어 사전 설정 대화 상자에서 대화형 배너 뷰어 사전 설정을 설명하는 이름을 입력합니다.

   저장한 후 뷰어 사전 설정 목록 페이지에 나타나는 제목입니다.

1. 리치 미디어 유형 풀다운 메뉴에서 **[!UICONTROL 대화형 이미지를 선택합니다.]**
1. **[!UICONTROL 만들기]**&#x200B;를 누릅니다.
1. [뷰어 사전 설정 편집] 페이지에서 **[!UICONTROL 모양]** 탭을 탭합니다.
1. 다음 중 하나를 수행하십시오.

   * 이미지에 사용할 자체 핫스팟 이미지를 업로드하려면 자산 선택기 아이콘을 누릅니다. 컨텐츠 선택 페이지에서 사용할 핫스팟 이미지로 이동하여 선택한 다음 오른쪽 상단 모서리에서 확인 표시 아이콘을 누릅니다.
   * 사전 정의된 핫스팟 이미지를 선택하려면 핫스팟 갤러리 아이콘을 누릅니다. 핫스팟 갤러리 팔레트에서 사용할 핫스팟 이미지를 탭합니다.

1. 페이지의 오른쪽 위 모서리 근처에 있는 **[!UICONTROL 저장.]**

   새 뷰어 사전 설정을 게시해야 합니다.

   &lt;A0/>추가한 뷰어 사전 설정 게시를 참조하십시오&lt;A1/>.[](/help/assets/managing-viewer-presets.md#publishing-viewer-presets)

   이제 이미지 배너를 업로드할 준비가 되었습니다.

## 이미지 배너 업로드 중 {#uploading-an-image-banner}

사용하려는 이미지를 이미 업로드한 경우 다음 단계인 [이미지 배너에 핫스팟 추가](#adding-hotspots-to-an-image-banner)로 이동하십시오.

**이미지 배너를 업로드하려면**

1. 대화형 이미지를 만들 이미지 배너를 업로드합니다.

   [자산 업로드](/help/assets/manage-assets.md#uploading-assets)를 참조하십시오.

   이제 이미지 배너에 핫스팟을 추가할 준비가 되었습니다.아래의 다음 작업을 참조하십시오.

## 이미지 배너에 핫스팟 추가 {#adding-hotspots-to-an-image-banner}

핫스팟 관리 페이지의 편집기를 사용하여 이미지 배너에 핫스팟을 추가할 수 있습니다.

핫스팟을 추가할 때 핫스팟을 Quickview 팝업 표시, 하이퍼링크 또는 경험 조각으로 정의할 수 있습니다.

[경험 구성요소](/help/sites-authoring/experience-fragments.md)를 참조하십시오.

>[!NOTE]
>
>경험 조각에 뷰어를 포함할 때에는 대화형 이미지의 소셜 미디어 공유 도구가 지원되지 않습니다. 이 문제를 해결하려면 소셜 미디어 공유 도구가 없는 뷰어 사전 설정을 사용하거나 만들 수 있습니다. 이러한 뷰어 사전 설정을 사용하면 경험 조각에 성공적으로 포함할 수 있습니다.

현재 작성/편집 세션 중에 페이지의 오른쪽 위 모서리 근처에 있는 실행 취소 및 재실행 옵션이 지원됩니다.

대화형 이미지 만들기를 마치면 미리 보기 를 사용하여 대화형 이미지가 고객에게 표시되는 방식을 보여 줍니다.

[(선택 사항) 대화형 이미지 미리 보기](#optional-previewing-interactive-images)를 참조하십시오.

>[!NOTE]
>
>대화형 이미지나 회전 배너의 이미지에 핫스팟을 추가하면 핫스팟이 이미지의 위치에 대해 동일하게 메타데이터 위치에 저장됩니다. 이는 대화형 이미지나 회전 배너인지에 관계없이 이미지 위치에 대한 상대적 메시지입니다. 이 기능은 두 뷰어에서 동일한 이미지를 정의된 핫스팟 데이터와 함께 쉽게 다시 사용할 수 있음을 의미합니다.
>
>그러나 회전 배너는 핫스팟도 포함될 수 있는 이미지에서 이미지 맵을 지원합니다.대화형 이미지는 표시되지 않습니다. 동일한 이미지를 사용하는 대화형 이미지나 회전 배너를 만들려면 이 점을 염두에 두십시오. 대신 동일한 이미지의 별도의 복사본을 사용하여 대화형 이미지와 회전 배너를 만들 수 있습니다.
>
>또한 [회전 배너](/help/assets/carousel-banners.md)도 참조하십시오.

>[!NOTE]
>
>핫스팟으로 대화형 이미지를 편집하고 이미지를 자르면 핫스팟이 제거됩니다.

**이미지 배너에 핫스팟을 추가하려면**

1. 자산 보기에서 대화형 양식으로 만들 이미지 배너로 이동합니다.
1. 다음 중 하나를 수행하십시오.

   * 이미지를 마우스로 가리킨 다음 **[!UICONTROL 선택]**(확인 표시 아이콘)을 탭합니다. 도구 모음에서 **[!UICONTROL 편집.]**

   * 이미지를 마우스로 가리킨 다음 **[!UICONTROL 추가 작업]**(세 점 아이콘) **[!UICONTROL 편집.]**

   * 이미지를 탭하여 세부 사항 보기 페이지에서 엽니다. 도구 모음에서 **[!UICONTROL 편집.]**

1. 페이지의 왼쪽 위 모서리 근처에 있는 **[!UICONTROL Hotspot]** 추가(손가락 탭 아이콘)를 탭하여 Hotspot 관리 페이지를 엽니다.
1. 페이지의 왼쪽 위 모서리 근처에 있는 **[!UICONTROL Hotspot.]**

1. 핫스팟 관리 페이지의 왼쪽 위 모서리 근처에 있는 **[!UICONTROL Hotspot.]**
1. 이미지에서 핫스팟을 표시할 위치를 누릅니다. 필요한 경우 핫스팟을 끌어 위치를 조정합니다.
1. a 및 b 단계를 반복하여 필요에 따라 핫스팟을 추가합니다.
1. (선택 사항) 핫스팟을 삭제하려면 이미지에서 핫스팟을 선택한 다음 **[!UICONTROL 핫스팟]** 제목 아래에 있는 **[!UICONTROL 삭제]**(쓰레기통 아이콘)를 누릅니다.

1. 이름 텍스트 필드에 핫스팟의 이름을 입력합니다. 이 이름은 선택한 핫스팟 드롭다운 목록에도 나타납니다.
1. 다음 중 하나를 수행하십시오.

   * **[!UICONTROL 빠른 보기를 누릅니다.]**

      * AEM Sites 또는 eCommerce 고객인 경우 제품 선택기 아이콘(돋보기)을 탭하거나 클릭하여 제품 선택 페이지를 엽니다. 사용할 제품을 탭하거나 클릭한 다음, 페이지의 오른쪽 위 모서리에서 **선택 **을 탭하여 핫스팟 관리 페이지로 돌아갑니다.
      * AEM Sites 또는 eCommerce 고객이 아닌 *입니다.*

         * [핫스팟 변수 식별](#optional-identifying-hotspot-variables);을 참조하십시오.이러한 변수를 정의해야 합니다.
         * 그런 다음 SKU 값을 수동으로 입력합니다. SKU 값 텍스트 필드에 제공하는 각 개별 제품 또는 서비스의 고유 식별자인 제품의 SKU(Stock Keeping Unit)를 입력합니다. 입력한 SKU 값은 Quickview 템플릿의 변수 부분을 자동으로 채우므로 시스템이 탭된 핫스팟을 특정 SKU의 Quickview와 연결하려는 것을 알게 됩니다.
         * (선택 사항) Quickview 내에 제품을 추가로 식별하는 데 사용해야 하는 다른 변수가 있는 경우 **[!UICONTROL 일반 변수 추가 를 탭합니다.]** 텍스트 필드에서 추가 변수를 지정합니다. 예를 들어 `category=Mens`은 추가된 변수입니다.
   * **[!UICONTROL 하이퍼링크를 누릅니다.]**

      * AEM Sites 고객인 경우 사이트 선택기 아이콘(폴더)을 탭하거나 클릭하여 URL로 이동합니다. 대화형 컨텐츠에 상대 URL이 있는 링크, 특히 AEM Sites 페이지에 대한 링크가 있는 경우 URL 기반 연결 방법이 지원되지 않습니다.
      * 독립형 고객인 경우, HREF 텍스트 필드에서 연결된 웹 페이지에 대한 전체 URL 경로를 지정합니다.

   링크를 새 브라우저 탭(권장 기본값)에서 열지 또는 동일한 탭에서 열지를 지정해야 합니다.

   자세한 내용은 [선택기 작업](/help/assets/working-with-selectors.md)을 참조하십시오.

   * **[!UICONTROL 경험 조각을 누릅니다.]**

      * AEM Sites 고객인 경우 검색 아이콘(확대경)을 탭하거나 클릭하여 경험 조각 페이지를 엽니다. 사용할 경험 조각을 탭하거나 클릭한 다음, 페이지의 오른쪽 위 모서리에서 선택 을 탭하여 핫스팟 관리 페이지로 돌아갑니다.
[경험 구성요소](/help/sites-authoring/experience-fragments.md)를 참조하십시오.

      * 배너에 표시될 경험 조각의 폭과 높이를 지정합니다.

         >[!NOTE]
         >
         >경험 조각에 뷰어를 포함할 때에는 대화형 이미지의 소셜 미디어 공유 도구가 지원되지 않습니다. 이 문제를 해결하려면 소셜 미디어 공유 도구가 없는 뷰어 사전 설정을 사용하거나 만들 수 있습니다. 이러한 뷰어 사전 설정을 사용하면 경험 조각에 성공적으로 포함할 수 있습니다.



1. **[!UICONTROL 저장]**&#x200B;을 눌러 작업을 저장하고 찾아보기 페이지로 돌아갑니다.
1. 대화형 이미지를 게시합니다. 게시를 사용하면 배너를 클라우드를 통해 제공할 수 있고 타사 웹 사이트와 통합해야 하는 경우 포함 코드도 생성됩니다.

   [자산 게시](/help/assets/manage-assets.md#publishing-assets)를 참조하십시오.

   이제 핫스팟을 추가하고 대화형 이미지를 게시하면 기존 웹 사이트에 추가할 수 있습니다.

   [웹 사이트와 대화형 이미지 통합](#integrating-an-interactive-image-with-your-website)을 참조하십시오.

   >[!NOTE]
   >
   >핫스팟이 있는 대화형 이미지를 편집하고 이미지를 자르면 핫스팟이 삭제됩니다.

### (선택 사항) 대화형 이미지 미리 보기 {#optional-previewing-interactive-images}

[미리 보기]를 사용하여 고객에게 표시되는 대화형 이미지의 표현을 보고 이미지의 핫스팟을 테스트하여 예상대로 작동하는지 확인할 수 있습니다.

대화형 이미지에 만족하면 게시할 수 있습니다.
웹 페이지에 비디오 또는 이미지 뷰어 포함](/help/assets/embed-code.md)을 참조하십시오.
[
[URL을 웹 애플리케이션에 연결](/help/assets/linking-urls-to-yourwebapplication.md)을 참조하십시오. 대화형 컨텐츠에 상대 URL이 있는 링크, 특히 AEM Sites 페이지에 대한 링크가 있는 경우 URL 기반 연결 방법이 지원되지 않습니다.
[페이지에 Dynamic Media 자산 추가](/help/assets/adding-dynamic-media-assets-to-pages.md)를 참조하십시오.

**대화형 이미지를 미리 보려면**

1. 자산 보기에서 만든 기존 대화형 이미지로 이동하고 탭하여 미리 보기에서 엽니다.
1. 미리 보기 페이지의 왼쪽 위 모서리 근처에 있는 컨텐츠 드롭다운 목록에서 **[!UICONTROL Viewers.]**
1. 뷰어 목록에서 **[!UICONTROL Shoppable_Banner]** 를 탭하거나 생성한 대화형 이미지 뷰어 사전 설정의 이름을 탭합니다.
1. 이미지의 핫스팟을 탭하여 연결된 작업을 테스트합니다.

## 대화형 이미지 자산 게시 {#publishing-interactive-image-assets}

대화형 이미지 자산을 게시하는 방법에 대한 자세한 내용은 [자산 게시](/help/assets/publishing-dynamicmedia-assets.md) 를 참조하십시오.

## 웹 사이트 {#integrating-an-interactive-image-with-your-website}와 대화형 이미지 통합

이제 배너 이미지를 업로드하고, 이미지에 핫스팟을 추가하고, 대화형 이미지를 게시하면 웹 사이트 페이지에 추가할 수 있습니다.

AEM Sites 고객의 경우 대화형 미디어 구성 요소를 페이지로 드래그하여 대화형 이미지를 추가할 수 있습니다. [페이지에 Dynamic Media 자산 추가](/help/assets/adding-dynamic-media-assets-to-pages.md)를 참조하십시오.

독립형 AEM Assets 고객의 경우 이 섹션에 설명된 대로 웹 사이트에 대화형 이미지를 수동으로 추가할 수 있습니다.

1. 게시된 대화형 이미지의 포함 코드를 복사합니다.
웹 페이지에 비디오 또는 이미지 뷰어 포함](/help/assets/embed-code.md)을 참조하십시오.[

1. 복사한 포함 코드를 웹 페이지 내에서 원하는 위치에 추가합니다.
복사된 포함 코드는 응답형 환경에 대해 설정되므로 지정된 영역에 자동으로 맞게 조정됩니다.

**예**

데모 웹 사이트 사용 예:

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html)

세 사람의 그림은 정적 `IMG` 태그입니다.

```xml
<img class="img-responsive" width="100%" title="Hero Image 2" alt="Hero Image 2" src="images/shoppable-banner.jpg">
```

통합은 `IMG` 태그를 제거하고 AEM Assets에서 복사된 포함 코드로 바꾸는 것만큼 간단합니다. 다음 URL에서 세 개의 원 핫스팟이 있는 페이지에서 쇼퍼블 인터랙티브 이미지를 보여 줍니다.

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-1.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-1.html)

>[!NOTE]
>
>따라서 데모 웹 사이트의 쇼퍼블 대화형 이미지에 있는 핫스팟은 표시 목적으로만 사용됩니다.아직 기존 빠른 보기와 통합되지 않았습니다.

응답형 환경을 위한 쇼퍼블 대화형 이미지에 &quot;자르기&quot;를 적용하려면 경로에 대화형 이미지 구성 속성 `ZoomView.iscommand`을 포함할 수 있습니다. 여기서 `ZoomView`은 호출할 구성 요소이고 `iscommand`는 사용자가 적용하는 &quot;자르기&quot; 이미지 제공 명령입니다.

[ZoomView.iscommand](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/command-reference-configuration-attributes-interactive-images/r-html5-aem-interactive-image-config-attrib-zoomview-iscommand.html) 구성 속성을 참조하십시오.

[자르기](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-crop.html) 이미지 제공 명령을 참조하십시오.

이제 대화형 이미지를 웹 사이트의 기존 Quickview와 통합할 준비가 되었습니다.

## 대화형 이미지를 기존 Quickview {#integrating-an-interactive-image-with-an-existing-quickview}과 통합

>[!NOTE]
>
>이 작업은 독립 실행형 AEM Assets 고객인 경우에만 적용됩니다.

이 프로세스의 마지막 단계는 대화형 이미지를 웹 사이트의 기존 Quickview 구현과 통합하는 것입니다. 모든 경우에 작동하는 통합에 대한 해결 방법이 없습니다. 모든 Quickview 구현은 고유하며 프런트 엔드 IT 담당자의 지원이 필요한 특정 접근 방식이 필요합니다.

기존 Quickview 구현은 일반적으로 다음 순서로 웹 페이지에서 발생하는 관련 간 작업 체인을 나타냅니다.

1. 사용자가 웹 사이트의 사용자 인터페이스에서 요소를 트리거합니다.
1. 프런트 엔드 코드는 1단계에서 트리거된 사용자 인터페이스 요소를 기반으로 Quickview URL을 가져옵니다.
1. 프런트 엔드 코드는 2단계에서 얻은 URL을 사용하여 Ajax 요청을 보냅니다.
1. 백엔드 로직은 해당 Quickview 데이터 또는 컨텐츠를 다시 프런트 엔드 코드로 반환합니다.
1. 프런트 엔드 코드는 Quickview 데이터 또는 콘텐츠를 로드합니다.
1. 선택적으로, 프런트 엔드 코드는 로드된 Quickview 데이터를 HTML 표현으로 변환합니다.
1. 프런트 엔드 코드는 모달 대화 상자나 패널을 표시하고 최종 사용자를 위해 화면에 HTML 콘텐츠를 렌더링합니다.

이러한 호출은 임의의 단계에서 웹 페이지 로직에서 호출할 수 있는 독립 공용 API 호출을 나타내지 않을 수 있습니다. 대신, 이전 단계의 마지막 단계(콜백)에서 모든 다음 단계가 숨겨지는 체인 호출입니다.

동시에 쇼퍼블 대화형 이미지에는 1단계와 2단계를 대체하고, 사용자가 쇼퍼블 이미지 내의 핫스팟을 클릭할 때 이러한 사용자 상호 작용은 뷰어에 의해 처리됩니다. 뷰어는 이전에 AEM Assets에 추가된 모든 핫스팟 데이터를 포함하는 웹 페이지에 이벤트를 반환합니다.

이러한 이벤트 처리기에서 프런트 엔드 코드는 다음을 수행합니다.

* 쇼퍼블 대화형 이미지에서 발생된 이벤트를 수신합니다.
* 핫스팟 데이터를 기반으로 Quickview URL을 구성합니다.
* 백엔드에서 Quickview를 로드하고 표시하기 위해 화면에서 렌더링하는 프로세스를 트리거합니다.

AEM Assets에서 반환된 포함 코드에는 강조 표시된 다음 코드 조각에 표시된 대로 주석 처리된 사용 가능한 이벤트 처리기가 이미 있습니다.

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

따라서 코드의 주석을 해제하고 더미 처리기 본문을 특정 웹 페이지에 해당하는 코드로 대체하기만 하면 됩니다.

Quickview URL을 구성하는 프로세스는 기본적으로 이전에 설명한 핫스팟 변수를 식별하는 데 사용되는 프로세스와 반대입니다.

[핫스팟 변수 식별](#optional-identifying-hotspot-variables)을 참조하십시오.

이전 Quickview URL 예를 사용하면 다음 예에서 각 사례에 Quickview URL이 구성되는 방식을 확인할 수 있습니다.

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

Quickview URL을 트리거하고 Quickview 패널을 활성화하는 마지막 단계는 IT 부서의 프런트 엔드 IT 담당자의 지원이 필요할 수 있습니다. 이들은 사용 준비 중인 Quickview URL을 사용하여 적절한 단계에서 Quickview 구현을 정확하게 트리거하는 방법을 잘 알고 있습니다.

이러한 단계를 데모 웹 사이트에 적용하여 쇼퍼블 인터랙티브 이미지를 Quickview 코드와 완전히 통합하는 방법을 확인할 수 있습니다. 이전에는 Quickview URL의 구조가 다음과 같이 식별되었습니다.

```xml
/datafeed/$categoryId$-$SKU$.json
```

`quickViewActivate` 처리기 내에서 이 URL을 재구성하려면 뷰어 코드에서 처리기에 전달되는 `inData` 개체에서 사용할 수 있는 `categoryId` 및 `SKU` 필드를 사용할 수 있습니다.

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

데모 웹 사이트에서 간단한 `loadQuickView()` 함수 호출을 사용하여 Quickview 대화 상자를 트리거합니다. 이 함수는 Quickview 데이터 URL인 인수를 하나만 사용합니다. 따라서 쇼퍼블 대화형 이미지를 통합하는 데 필요한 마지막 단계는 다음 코드 행을 `quickViewActivate` 처리기에 추가하는 것입니다.

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

완전히 통합된 대화형 이미지를 사용하는 최종 데모 웹 사이트는 다음과 같습니다.

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-3.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-3.html)

## 빠른 보기를 사용하여 사용자 지정 팝업 만들기 {#using-quickviews-to-create-custom-pop-ups}

[빠른 보기를 사용하여 사용자 지정 팝업 만들기](/help/assets/custom-pop-ups.md)를 참조하십시오.
