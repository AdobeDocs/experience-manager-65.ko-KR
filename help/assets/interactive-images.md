---
title: 대화형 이미지
description: Dynamic Media에서 대화형 이미지로 작업하는 방법에 대해 알아봅니다
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
feature: Interactive Images
role: User, Admin
exl-id: 8a609024-e9e6-4805-8306-48d095110eb6
solution: Experience Manager, Experience Manager Assets
source-git-commit: a28883778c5e8fb90cbbd0291ded17059ab2ba7e
workflow-type: tm+mt
source-wordcount: '4132'
ht-degree: 1%

---

# 대화형 이미지{#interactive-images}

&quot;구매 가능한&quot; 핫스팟을 이미지에 끌어다 놓아 정적 이미지를 고객에게 풍부하고 매력적인 경험을 쉽게 만들 수 있습니다. 구매 가능한 핫스팟은 제품 또는 서비스에 대한 추가 정보를 판매 시점(&quot;장바구니에 추가&quot; 또는 &quot;구매&quot;) 기능과 결합합니다. 고객은 이러한 핫스팟을 선택하고 제품 또는 서비스에 직접 연결하거나 장바구니에 추가하거나 웹 페이지에 연결할 수 있습니다. 이와 같은 직접 경험은 웹 사이트에서 고객 참여 및 전환을 증가시킵니다.

다음은 빠른 보기 팝업이 포함된 구매 가능한 배너입니다. 사용자가 모델에서 원 또는 &quot;핫스팟&quot;을 선택하여 빠른 보기를 활성화합니다.

![chlimage_1-152](assets/chlimage_1-368.png)

다음으로 이동하여 위의 웹 페이지에서 작동 중인 대화형 이미지를 참조하십시오.

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html)

## 대화형 이미지 배너가 생성되는 방식 보기 {#watch-how-interactive-image-banners-are-created}

연습: [대화형 이미지 배너를 만드는 방법](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner) (10분 33초). 또한 대화형 이미지 배너를 미리 보고, 편집하고, 전달하는 방법도 알아봅니다.

## 빠른 시작: 대화형 이미지 {#quick-start-interactive-images}

다음 단계별 워크플로 설명은 Adobe Experience Manager Assets에서 대화형 이미지를 빠르게 시작하고 실행하는 데 도움이 되도록 설계되었습니다.

다음 항목을 찾습니다. **예** 일부 빠른 시작 작업 내 제목 여기에는 아직 대화형 이미지가 추가되지 않은 다음 웹 페이지 예를 기반으로 하는 간단한 자습서가 포함되어 있습니다.

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html)

이 자습서는 웹 사이트에서 대화형 이미지를 통합하는 단계를 설명하는 데 도움이 됩니다.

대화형 이미지 단계:

1. **(선택 사항) 핫스팟 변수를 식별합니다** - Experience Manager Assets 및 Dynamic Media 독립 실행형을 사용하는 경우 기존 빠른 보기 구현에 사용된 동적 변수를 식별하여 시작합니다. 그런 다음 대화형 이미지를 만들 때 핫스팟 데이터를 입력할 수 있습니다. 다음을 참조하십시오 [(선택 사항) 핫스팟 변수를 식별합니다](#optional-identifying-hotspot-variables).
그러나 Adobe Experience Manager Sites, Adobe Experience Manager eCommerce 또는 둘 다를 사용하는 경우 이 단계는 필요하지 않습니다.
다음을 참조하십시오 [Experience Manager Assets의 eCommerce 개념](/help/commerce/cif-classic/administering/concepts.md).

1. **(선택 사항) 대화형 이미지 뷰어 사전 설정 만들기** - 핫스팟을 표시하는 데 사용되는 그래픽 이미지를 사용자 지정합니다. 기본 제공 대화형 이미지 뷰어 사전 설정을 로 사용하려면 고유한 대화형 이미지 뷰어 사전 설정을 만들 필요가 없습니다 `Shoppable_Banner` 대신,
다음을 참조하십시오 [(선택 사항) 대화형 이미지 뷰어 사전 설정 만들기](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset).

1. **이미지 배너 업로드** - 대화형으로 만들 이미지 배너를 업로드합니다.
다음을 참조하십시오 [이미지 배너 업로드](#uploading-an-image-banner).

1. **이미지 배너에 핫스팟 추가** - 이미지 배너에 핫스팟을 하나 이상 추가하고 각 핫스팟을 하이퍼링크, 빠른 보기 또는 경험 조각과 같은 작업에 연결합니다. 핫스팟을 추가한 후 대화형 이미지를 게시하여 이 작업을 완료합니다.

   * 다음을 참조하십시오 [이미지 배너에 핫스팟 추가](#adding-hotspots-to-an-image-banner).
   * 다음을 참조하십시오 [대화형 이미지 미리 보기](#optional-previewing-interactive-images) - 선택 사항입니다. 원하는 경우 구매 가능한 배너의 표현을 보고 상호 작용을 테스트할 수 있습니다.
   * 다음을 참조하십시오 [자산 게시](/help/assets/publishing-dynamicmedia-assets.md) 인터랙티브 이미지 에셋을 게시하는 방법에 대한 자세한 정보.

1. **웹 사이트에 대화형 이미지 추가** - Experience Manager Sites나 eCommerce 또는 둘 다 사용하는 경우 Experience Manager의 웹 페이지에 대화형 이미지를 추가할 수 있습니다. 대화형 미디어 구성 요소를 페이지로 드래그합니다. 다음을 참조하십시오 [페이지에 Dynamic Media 에셋 추가](/help/assets/adding-dynamic-media-assets-to-pages.md).

   Experience Manager Assets 및 Dynamic Media 독립 실행형을 사용하는 경우 웹 사이트에서 포함 코드를 복사한 다음 기존 Quickview와 통합해야 합니다. 다음을 참조하십시오 [대화형 이미지를 웹 사이트에 통합](#integrating-an-interactive-image-with-your-website).

   타사 WCM(Web Content Manager)을 사용하는 경우, 새 대화형 비디오를 웹 사이트에서 사용되는 기존 빠른 보기 구현과 통합해야 합니다. 다음을 참조하십시오 [기존 빠른 보기와 대화형 이미지 통합](#integrating-an-interactive-image-with-an-existing-quickview).

## (선택 사항) 핫스팟 변수를 식별합니다 {#optional-identifying-hotspot-variables}

>[!NOTE]
>
>이 작업은 다음이 참인 경우에만 필요합니다.
>
>* 빠른 보기로 트리거하여 이미지에 대화형 기능을 추가하려는 경우.
>* Experience Manager 구현은 다음을 수행합니다 *아님* IBM® WebSphere® Commerce, Elastic Path, hybris 또는 Intershop과 같은 모든 eCommerce 솔루션에서 제품 데이터를 Experience Manager으로 가져오려면 eCommerce 통합 프레임워크를 사용합니다. 다음을 참조하십시오 [Experience Manager Assets의 eCommerce 개념](/help/commerce/cif-classic/administering/concepts.md).
>
>Experience Manager 구현에서 eCommerce를 사용하는 경우 이 작업을 건너뛰고 다음 작업으로 진행할 수 있습니다.

핫스팟 데이터를 입력하여 대화형 이미지를 만들 수 있도록 기존 Quickview 구현에서 사용하는 동적 변수를 식별하여 시작합니다.

Experience Manager Assets의 배너 이미지에 핫스팟을 추가하는 경우 SKU(Stock Keeping Unit) 및 선택적 추가 변수를 각 핫스팟에 할당해야 합니다. 이러한 핫스팟 변수는 나중에 핫스팟을 빠른 보기 콘텐츠와 일치시키는 데 사용됩니다.

핫스팟 데이터와 연결할 변수의 수와 유형을 올바르게 식별하는 것이 중요합니다. 배너 이미지에 추가된 각 핫스팟에는 기존 백엔드 시스템의 제품을 명확하게 식별할 수 있는 충분한 정보가 있어야 합니다.

핫스팟 데이터에 사용할 변수 세트를 식별하는 방법은 여러 가지가 있습니다.

때로는 기존 Quickview 구현을 담당하는 IT 전문가와 상담하는 것으로 충분합니다. IT 전문가는 시스템에서 Quickview를 식별하는 데 필요한 최소 데이터 세트가 무엇인지 알 수 있습니다. 그러나 프론트엔드 코드의 기존 동작을 간단하게 분석할 수도 있습니다.

대부분의 빠른 보기 구현은 다음 패러다임을 사용합니다.

* User activates a user interface element on the website. 예를 들어 &quot;빠른 보기&quot; 버튼을 선택합니다.
* 필요한 경우 웹 사이트에서 백엔드에 Ajax 요청을 전송하여 Quickview 데이터 또는 컨텐츠를 로드합니다.
* 빠른 보기 데이터는 웹 페이지에서의 렌더링을 준비하기 위해 콘텐츠로 변환됩니다.
* 마지막으로 프론트엔드 코드는 이러한 콘텐츠를 화면에서 시각적으로 렌더링합니다.

그러면 빠른 보기 기능이 구현된 기존 웹 사이트의 다른 영역을 방문하는 방법이 제공됩니다. 그런 다음 빠른 보기를 트리거하고 웹 페이지에서 보낸 Ajax URL을 캡처하여 빠른 보기 데이터 또는 콘텐츠를 로드합니다.

일반적으로 특수 디버깅 도구를 사용할 필요가 없습니다. 최신 웹 브라우저에는 적절한 작업을 수행하는 웹 검사기가 있습니다. 다음은 웹 검사기를 포함하는 웹 브라우저의 몇 가지 예입니다.

* Google Chrome에서 나가는 모든 HTTP 요청을 보려면 F12 키를 눌러 [개발자 도구] 패널을 연 다음 [네트워크] 탭을 선택합니다.
Mac에서 Command+Option+I를 눌러 [개발자 도구] 패널을 연 다음 [네트워크] 탭을 선택합니다.

* Firefox에서는 F12를 눌러 Firebug 플러그인을 활성화하고 Net 탭을 사용하거나 내장된 Inspector 도구와 Network 탭을 사용할 수 있습니다.
Mac에서 Command+Option+I를 눌러 [개발자 도구] 패널을 연 다음 [검사기] 탭을 선택합니다.

브라우저에서 네트워크 모니터링이 켜지면 페이지에서 빠른 보기를 트리거합니다.

이제 네트워크 로그에서 Quickview Ajax URL을 찾아 기록된 URL을 복사하여 향후 분석할 수 있습니다. 일반적으로 빠른 보기를 트리거하면 서버로 전송되는 요청이 많이 있습니다. 일반적으로 Quickview Ajax URL은 목록의 첫 번째 URL 중 하나입니다. 복잡한 쿼리 문자열 부분 또는 경로가 있으며 응답 MIME 유형은 다음 중 하나입니다. `text/html`, `text/xml`, 또는 `text/javascript`.

이 프로세스 중에 다양한 제품 카테고리와 유형을 사용하여 웹 사이트의 다양한 영역을 방문하는 것이 중요합니다. 그 이유는 Quickview URL이 특정 웹 사이트 카테고리에 대해 공통적인 부분을 가질 수 있지만, 웹 사이트의 다른 영역을 방문하는 경우에만 변경되기 때문입니다.

가장 간단한 경우, 빠른 보기 URL에 있는 유일한 변수 부분은 제품 SKU입니다. 이 경우 SKU 값은 배너 이미지에 핫스팟을 추가하는 데 필요한 유일한 데이터 부분입니다.

그러나 복잡한 경우 빠른 보기 URL에는 카테고리 ID, 색상 코드 및 크기 코드와 같이 SKU와는 다른 다양한 요소가 있습니다. 이러한 경우 모든 요소는 Experience Manager Assets의 구매 가능한 대화형 이미지 기능에서 핫스팟 데이터 정의에 있는 별도의 변수입니다.

다음 Quickview URL 및 결과 핫스팟 변수 예를 생각해 보십시오.

<table>
  <tbody>
  <tr>
    <td><p>쿼리 문자열에 있는 단일 SKU.</p> </td>
    <td><p>기록된 빠른 보기 URL에는 다음이 포함됩니다.</p>
    <ul>
      <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>URL에서 유일한 변수 부분은 productId= 쿼리 문자열 매개 변수의 값이며 이는 명백히 SKU 값입니다. 따라서 핫스팟에는 다음과 같은 값으로 채워진 SKU 필드만 필요합니다. <strong><code>866558</code></strong>, <strong><code>1196184</code></strong>, <strong><code>1081492</code></strong>, <strong><code>1898294</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>URL 경로에 있는 단일 SKU.</p> </td>
    <td><p>기록된 빠른 보기 URL에는 다음이 포함됩니다.</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>변수 부분은 경로의 마지막 부분에 있으며, 핫스팟의 SKU 값이 됩니다. <strong><code>6422350843</code></strong>, <strong><code>1607745002</code></strong>, <strong><code>0086724882</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>쿼리 문자열의 SKU 및 카테고리 ID.</p> </td>
    <td><p>기록된 빠른 보기 URL에는 다음이 포함됩니다.</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>이 경우 URL에는 두 가지 다양한 부분이 있습니다. SKU는에 저장됩니다. <code>prodId</code> 매개 변수 및 범주 ID<code></code> 에 저장됩니다. <code>category=</code> 매개 변수.</p> <p>따라서 핫스팟 정의는 쌍입니다. 즉, SKU 값과 라는 추가 변수입니다. <code>categoryId</code>. 결과 쌍은 다음과 같습니다.</p>
    <ul>
      <li><p>SKU: <strong><code>305466</code></strong> 및 <code>categoryId</code> 은(는) <code>1100004</code>.</p> </li>
      <li><p>SKU: <strong><code>310181</code></strong> 및 <code>categoryId</code> 은(는) <strong><code>1100004</code></strong>.</p> </li>
      <li><p>SKU: <strong><code>308706</code></strong> 및 <code>categoryId</code> 은(는) <strong><code>1740148</code></strong>.</p> </li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**예**

위의 세 가지 예에서 사용한 것과 동일한 접근 방식을 데모 웹 페이지에 적용할 수 있습니다.

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html)

데모 웹 페이지에는 여러 제품 썸네일이 있으며, 각 페이지에는 &quot;자세히 보기&quot;라는 빠른 보기 버튼이 있습니다. 웹 브라우저의 디버깅 도구가 여전히 활성화된 상태에서 각 버튼을 선택하고 기록된 빠른 보기 URL을 확인합니다. 페이지에서 사용할 수 있는 네 개의 제품 빠른 보기를 모두 활성화하면 다음과 같은 백엔드에 대한 빠른 보기 요청 목록이 제공됩니다.

* `/datafeed/Male-Windbreaker.json`
* `/datafeed/Male-SimpleHenley.json`
* `/datafeed/Male-CamoPullover.json`
* `/datafeed/Female-QuiltedDownJacket.json`

서버 호출을 살펴보면 제품별 정보가 요청 경로에만 표시됩니다. 또한 쿼리 문자열은 전혀 사용되지 않으며 두 가지 유형의 데이터가 관련되어 있습니다.

* 첫 번째 유형은 남성 또는 여성입니다. 이를 &quot;제품 범주&quot;라고 할 수 있습니다.
* 두 번째 유형은 CamoPullover와 같은 제품 이름입니다. 이 정보는 제품 SKU라고 가정할 수 있습니다.

이 정보가 주어지면 전체 Quickview URL의 패턴은 다음과 같습니다.

`/datafeed/$categoryId$-$SKU$.json`

이러한 분석을 기반으로 다음을 사용할 수 있습니다 `categoryId` 및 `SKU` 핫스팟용

이제 Experience Manager Assets에서 구매 가능한 대화형 이미지 기능을 사용하여 이미지 배너를 업로드하고 핫스팟을 추가할 준비가 되었습니다.

## (선택 사항) 대화형 이미지 뷰어 사전 설정 만들기 {#optional-creating-an-interactive-image-viewer-preset}

라는 기본 제공 대화형 이미지 뷰어 사전 설정을 사용하도록 선택할 수 있습니다. `Shoppable_Banner` Experience Manager Assets과 함께 제공됩니다. 또는 대화형 이미지에 사용할 사용자 지정 뷰어 사전 설정을 만들 수 있습니다.

사용자 지정 대화형 이미지 뷰어 사전 설정을 만들 때 이미지 배너에 핫스팟의 모양을 결정할 수 있습니다. 뷰어 사전 설정을 만들 때 미리 정의된 이미지 갤러리에서 핫스팟 그래픽을 사용하도록 선택할 수 있습니다.

뷰어 사전 설정을 저장하면 Experience Manager Assets의 뷰어 사전 설정 목록 페이지에서 자동으로 활성화(켜짐)됩니다. 이 기능은 자산을 볼 때마다 대화형 미디어 구성 요소에서 볼 수 있음을 의미합니다. 단, 종료 *게재* 이 뷰어 사전 설정을 사용하는 대화형 배너, 다음 작업을 수행해야 합니다. *게시* 뷰어 사전 설정도 참조하십시오. 이 규칙은 사용자 지정 또는 기본 뷰어 사전 설정에 대해 적용됩니다.

**대화형 이미지 뷰어 사전 설정을 만들려면 다음을 수행하십시오.**

1. 왼쪽 레일에서 다음 위치에 대한 네비게이터 **[!UICONTROL 도구]** > **[!UICONTROL 에셋]** > **[!UICONTROL 뷰어 사전 설정]**.
1. 페이지의 오른쪽 상단 모서리 근처에서 을 선택합니다. **[!UICONTROL 만들기]**.
1. 새 뷰어 사전 설정 대화 상자에서 대화형 배너 뷰어 사전 설정을 설명하는 이름을 입력합니다.

   제목을 저장하면 뷰어 사전 설정 목록 페이지에 나타납니다.

1. In the Rich Media Type pull-down menu, select **[!UICONTROL Interactive Image]**.
1. **[!UICONTROL 만들기]**&#x200B;를 선택합니다.
1. 뷰어 사전 설정 편집 페이지에서 **[!UICONTROL 모양]** 탭.
1. 다음 중 하나를 수행하십시오.

   * 이미지에 사용할 자신만의 핫스팟 이미지를 업로드하려면 에셋 선택기 아이콘을 선택합니다. [컨텐츠 선택] 페이지에서 사용할 핫스팟 이미지로 이동하여 선택한 다음 오른쪽 상단의 확인 표시 아이콘을 선택합니다.
   * 미리 정의된 핫스팟 이미지를 선택하려면 [핫스팟 갤러리] 아이콘을 선택합니다. 핫스팟 갤러리 팔레트에서 사용할 핫스팟 이미지를 선택합니다.

1. 페이지의 오른쪽 상단 모서리 근처에서 을 선택합니다. **[!UICONTROL 저장]**.

   새 뷰어 사전 설정을 게시해야 합니다.

   다음을 참조하십시오 [추가한 뷰어 사전 설정 게시](/help/assets/managing-viewer-presets.md#publishing-viewer-presets).

   이제 이미지 배너를 업로드할 준비가 되었습니다.

## 이미지 배너 업로드 {#uploading-an-image-banner}

사용할 이미지를 이미 업로드한 경우 다음 단계로 이동하십시오. [이미지 배너에 핫스팟 추가](#adding-hotspots-to-an-image-banner).

**이미지 배너를 업로드하려면:**

1. 대화형으로 만들 이미지 배너를 업로드합니다.

   다음을 참조하십시오 [에셋 업로드](/help/assets/manage-assets.md#uploading-assets).

   이제 이미지 배너에 핫스팟을 추가할 준비가 되었습니다. 아래 다음 작업을 참조하십시오.

## 이미지 배너에 핫스팟 추가 {#adding-hotspots-to-an-image-banner}

핫스팟 관리 페이지의 편집기를 사용하여 이미지 배너에 핫스팟을 추가할 수 있습니다.

핫스팟을 추가할 때 빠른 보기 팝업 표시, 하이퍼링크 또는 경험 조각으로 정의할 수 있습니다.

다음을 참조하십시오 [경험 조각](/help/sites-authoring/experience-fragments.md).

>[!NOTE]
>
>뷰어를 경험 조각에 포함할 때에는 대화형 이미지의 소셜 미디어 공유 도구가 지원되지 않습니다. 이 문제를 해결하려면 소셜 미디어 공유 도구가 없는 뷰어 사전 설정을 사용하거나 만들 수 있습니다. 이러한 뷰어 사전 설정을 사용하면 경험 조각에 성공적으로 포함할 수 있습니다.

페이지의 오른쪽 상단 모서리 근처에 있는 실행 취소 및 재실행 옵션은 현재 생성/편집 세션 중에 지원됩니다.

대화형 이미지 만들기가 완료되면 미리보기 를 사용하여 대화형 이미지가 고객에게 표시되는 방식을 확인할 수 있습니다.

다음을 참조하십시오 [(선택 사항) 대화형 이미지 미리 보기](#optional-previewing-interactive-images).

>[!NOTE]
>
>대화형 이미지 또는 회전식 배너의 이미지에 핫스팟을 추가하면 핫스팟 정보가 동일한 메타데이터 위치에 저장됩니다. 이 위치는 대화형 이미지인지 회전식 배너인지에 관계없이 이미지의 위치를 기준으로 합니다. 이 기능은 정의된 핫스팟 데이터와 함께 동일한 이미지를 두 뷰어에서 쉽게 재사용할 수 있음을 의미합니다.
>
>회전 배너는 핫스팟을 포함할 수도 있는 이미지에 대한 이미지 맵을 지원합니다. 대화형 이미지는 지원하지 않습니다. 동일한 이미지를 사용하는 대화형 이미지 또는 회전 배너를 만들려면 이 규칙을 염두에 두십시오. 동일한 이미지의 별도의 복사본을 대신 사용하여 대화형 이미지 및 회전식 배너를 만들 수 있습니다.
>
>참조: [회전 배너](/help/assets/carousel-banners.md).

>[!NOTE]
>
>핫스팟이 있는 대화형 이미지를 편집하고 이미지를 자르는 경우 핫스팟이 제거됩니다.

**이미지 배너에 핫스팟을 추가하려면:**

1. 자산 보기에서 대화형으로 만들 이미지 배너로 이동합니다.
1. 다음 중 하나를 수행하십시오.

   * 이미지를 마우스로 가리킨 다음, **[!UICONTROL 선택]** (확인 표시 아이콘) 도구 모음에서 를 선택합니다. **[!UICONTROL 편집]**.

   * 이미지를 마우스로 가리킨 다음, **[!UICONTROL 추가 작업]** (세 점 아이콘) **[!UICONTROL 편집]**.

   * 세부 사항 보기 페이지에서 이미지를 열 수 있도록 이미지를 선택합니다. 도구 모음에서 를 선택합니다. **[!UICONTROL 편집]**.

1. 페이지의 왼쪽 상단 모서리 근처에서 을 선택합니다. **[!UICONTROL 핫스팟 추가]** (손가락 선택 아이콘) - 핫스팟 관리 페이지를 엽니다.
1. 페이지의 왼쪽 상단 모서리 근처에서 을 선택합니다. **[!UICONTROL 핫스팟]**.

   1. 핫스팟 관리 페이지의 왼쪽 상단 모서리 근처에서 을 선택합니다. **[!UICONTROL 핫스팟]**.
   1. 이미지에서 핫스팟을 표시할 위치를 선택합니다. If necessary, drag the hotspot to adjust its location.
   1. 필요에 따라 a단계와 b단계를 반복하여 추가 핫스팟을 추가합니다.
   1. (선택 사항) 핫스팟을 삭제하려면 이미지에서 핫스팟을 선택한 다음 를 선택합니다 **[!UICONTROL 삭제]** (휴지통 아이콘) **[!UICONTROL 핫스팟]** 제목.

1. 이름 텍스트 필드에 핫스팟의 이름을 입력합니다. 이 이름은 선택한 핫스팟 드롭다운 목록에도 나타납니다.
1. 다음 중 하나를 수행하십시오.

   * 선택 **[!UICONTROL 빠른 보기]**.

      * Experience Manager Sites 또는 eCommerce 고객의 경우 제품 선택기 아이콘(돋보기)을 선택하여 제품 선택 페이지를 엽니다. 사용할 제품을 선택한 다음 를 선택합니다 **[!UICONTROL 선택]** 핫스팟 관리 페이지로 돌아갈 수 있도록 페이지의 오른쪽 상단 모서리에서 를 클릭합니다.
      * 다음과 같은 경우 *아님* Experience Manager Sites 또는 eCommerce 고객

         * 다음을 참조하십시오 [핫스팟 변수 식별](#optional-identifying-hotspot-variables); 이러한 변수를 정의해야 합니다.
         * 그런 다음 수동으로 SKU 값을 입력합니다. SKU 값 텍스트 필드에 제품의 SKU(Stock Keeping Unit)를 입력합니다. 이 SKU는 제공하는 각 고유 제품이나 서비스에 대한 고유 식별자입니다. 입력한 SKU 값은 빠른 보기 템플릿의 변수 부분을 자동으로 입력하므로 선택한 핫스팟을 특정 SKU의 빠른 보기와 연결해야 한다는 것을 시스템에서 알 수 있습니다.
         * (선택 사항) Quickview 내에 제품을 추가로 식별하는 데 사용해야 하는 다른 변수가 있는 경우 다음을 선택합니다. **[!UICONTROL 일반 변수 추가]**. 텍스트 필드에 추가 변수를 지정합니다. 예를 들어, `category=Males` 는 추가된 변수입니다.

   * 선택 **[!UICONTROL 하이퍼링크]**.

      * Experience Manager Sites 고객의 경우 사이트 선택기 아이콘(폴더)을 선택하여 URL로 이동합니다. 대화형 콘텐츠에 상대 URL이 있는 링크, 특히 Experience Manager Sites 페이지에 대한 링크가 있는 경우에는 URL 기반 연결 방법이 불가능합니다.
      * 독립형 고객인 경우 HREF 텍스트 필드에 연결된 웹 페이지에 대한 전체 URL 경로를 지정합니다.

   링크를 새 브라우저 탭(권장 기본값)에서 열지 또는 동일한 탭에서 열지를 지정해야 합니다.

   다음을 참조하십시오 [선택기를 사용한 작업](/help/assets/working-with-selectors.md) 추가 정보.

   * 선택 **[!UICONTROL 경험 조각]**.

      * Experience Manager Sites 고객인 경우 검색 아이콘(돋보기)을 선택하여 경험 조각 페이지를 엽니다. 사용할 경험 조각을 선택한 다음 를 선택합니다 **[!UICONTROL 선택]** 핫스팟 관리 페이지로 돌아갈 수 있도록 페이지의 오른쪽 상단 모서리에서 를 클릭합니다.
다음을 참조하십시오 [경험 조각](/help/sites-authoring/experience-fragments.md).

      * 배너에 표시할 경험 조각의 너비와 높이를 지정합니다.

        >[!NOTE]
        >
        >뷰어를 경험 조각에 포함할 때에는 대화형 이미지의 소셜 미디어 공유 도구가 지원되지 않습니다. 이 문제를 해결하려면 소셜 미디어 공유 도구가 없는 뷰어 사전 설정을 사용하거나 만들 수 있습니다. 이러한 뷰어 사전 설정을 사용하면 경험 조각에 성공적으로 포함할 수 있습니다.

1. 선택 **[!UICONTROL 저장]** 작업을 저장하고 찾아보기 페이지로 돌아갑니다.
1. 대화형 이미지를 게시합니다. 게시를 사용하면 배너를 클라우드를 통해 게재할 수 있으며 서드파티 웹 사이트와 통합해야 하는 경우 포함 코드를 생성할 수도 있습니다.

   다음을 참조하십시오 [자산 게시](/help/assets/manage-assets.md#publishing-assets).

   핫스팟을 추가하고 대화형 이미지를 게시하면 이제 기존 웹 사이트에 추가할 준비가 된 것입니다.

   다음을 참조하십시오 [대화형 이미지를 웹 사이트에 통합](#integrating-an-interactive-image-with-your-website).

   >[!NOTE]
   >
   >핫스팟이 있는 대화형 이미지를 편집하고 이미지를 자르는 경우 핫스팟이 삭제됩니다.

### (선택 사항) 대화형 이미지 미리 보기 {#optional-previewing-interactive-images}

미리보기 를 사용하여 대화형 이미지가 고객에게 어떻게 표시되는지 재현하고 이미지의 핫스팟을 테스트하여 예상대로 작동하는지 확인할 수 있습니다.

대화형 이미지가 만족스러우면 게시할 수 있습니다.
다음을 참조하십시오 [웹 페이지에 비디오 또는 이미지 뷰어 포함](/help/assets/embed-code.md).
다음을 참조하십시오 [웹 애플리케이션에 URL 연결](/help/assets/linking-urls-to-yourwebapplication.md). 대화형 콘텐츠에 상대 URL이 있는 링크, 특히 Experience Manager Sites 페이지에 대한 링크가 있는 경우에는 URL 기반 연결 방법이 불가능합니다.
다음을 참조하십시오 [페이지에 Dynamic Media 에셋 추가](/help/assets/adding-dynamic-media-assets-to-pages.md).

**대화형 이미지를 미리 보려면 다음을 수행하십시오.**

1. 에셋 보기에서 생성한 기존 대화형 이미지로 이동한 다음 선택하여 미리보기에서 엽니다.
1. 미리보기 페이지의 왼쪽 상단 모서리 근처에 있는 콘텐츠 드롭다운 목록에서 을(를) 선택합니다. **[!UICONTROL 뷰어]**.
1. 뷰어 목록에서 다음을 선택합니다. **[!UICONTROL Shopable_Banner]** 또는 만든 대화형 이미지 뷰어 사전 설정의 이름입니다.
1. 연결된 작업을 테스트하려면 이미지에서 핫스팟을 선택합니다.

## 대화형 이미지 자산 게시 {#publishing-interactive-image-assets}

다음을 참조하십시오 [자산 게시](/help/assets/publishing-dynamicmedia-assets.md) 인터랙티브 이미지 에셋을 게시하는 방법에 대한 자세한 정보.

## 대화형 이미지를 웹 사이트에 통합 {#integrating-an-interactive-image-with-your-website}

배너 이미지를 업로드하고, 이미지에 핫스팟을 추가하고, 대화형 이미지를 게시하면 이제 웹 사이트 페이지에 추가할 준비가 된 것입니다.

Experience Manager Sites 고객의 경우 대화형 미디어 구성 요소를 페이지에 드래그하여 대화형 이미지를 추가할 수 있습니다. 다음을 참조하십시오 [페이지에 Dynamic Media 에셋 추가](/help/assets/adding-dynamic-media-assets-to-pages.md).

독립형 Experience Manager Assets 고객인 경우 이 섹션에 설명된 대로 대화형 이미지를 웹 사이트에 수동으로 추가할 수 있습니다.

1. 게시된 대화형 이미지의 포함 코드를 복사합니다.
다음을 참조하십시오 [웹 페이지에 비디오 또는 이미지 뷰어 포함](/help/assets/embed-code.md).

1. 복사한 포함 코드를 웹 페이지 내의 원하는 위치에 추가합니다.
복사된 포함 코드는 지정된 영역에 자동으로 맞도록 응답형 환경에 대해 설정됩니다.

**예**

데모 웹 사이트 사용 예:

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html)

세 수컷의 그림은 정적이다 `IMG` 태그:

```xml
<img class="img-responsive" width="100%" title="Hero Image 2" alt="Hero Image 2" src="images/shoppable-banner.jpg">
```

통합은 를 제거하는 것만큼 간단합니다. `IMG` 태그를 지정하고 Experience Manager Assets에서 복사한 포함 코드로 대체합니다. 3개의 원형 핫스팟이 있는 페이지에서 구매 가능한 대화형 이미지를 표시하는 다음 URL에서 결과를 볼 수 있습니다.

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-1.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-1.html)

>[!NOTE]
>
>이 시점에서 데모 웹 사이트의 구매 가능한 대화형 이미지에 있는 핫스팟은 표시용으로만 사용되며 기존 Quickview와 아직 통합되지 않았습니다.

응답형 환경에 대해 구매 가능한 대화형 이미지에 &quot;자르기&quot;를 적용하려면 대화형 이미지 구성 속성을 포함할 수 있습니다 `ZoomView.iscommand` 경로를 표시합니다. 구성 요소 `ZoomView` 이(가) 및 (이)라고 함 `iscommand` 는 사용자가 적용하는 &quot;자르기&quot; 이미지 제공 명령입니다.

다음을 참조하십시오 [ZoomView.iscommand](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/command-reference-configuration-attributes-interactive-images/r-html5-aem-interactive-image-config-attrib-zoomview-iscommand) 구성 속성입니다.

다음을 참조하십시오 [자르기](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-crop) 이미지 제공 명령.

이제 대화형 이미지를 웹 사이트의 기존 빠른 보기와 통합할 준비가 되었습니다.

## 기존 빠른 보기와 대화형 이미지 통합 {#integrating-an-interactive-image-with-an-existing-quickview}

>[!NOTE]
>
>이 작업은 독립형 Experience Manager Assets 고객인 경우에만 적용됩니다.

이 프로세스의 마지막 단계는 웹 사이트에서 대화형 이미지를 기존 Quickview 구현과 통합하는 것입니다. 모든 경우에 작동하는 통합 솔루션은 없습니다. 모든 Quickview 구현은 고유하며 특정 접근 방식이 필요합니다. 프론트엔드 IT 담당자의 도움이 필요할 수 있습니다.

기존 빠른 보기 구현은 일반적으로 웹 페이지에서 다음 순서로 발생하는 상호 관련된 작업 체인을 나타냅니다.

1. 사용자가 웹 사이트의 사용자 인터페이스에서 요소를 트리거합니다.
1. 프론트엔드 코드는 1단계에서 트리거된 사용자 인터페이스 요소를 기반으로 Quickview URL을 가져옵니다.
1. 프론트엔드 코드는 2단계에서 얻은 URL을 사용하여 Ajax 요청을 보냅니다.
1. 백엔드 로직은 해당 Quickview 데이터 또는 컨텐츠를 프론트엔드 코드로 다시 반환합니다.
1. 프론트엔드 코드는 Quickview 데이터 또는 콘텐츠를 로드합니다.
1. 선택적으로, 프론트엔드 코드는 로드된 Quickview 데이터를 HTML 표시로 변환합니다.
1. 프론트엔드 코드는 모달 대화 상자 또는 패널을 표시하고 최종 사용자를 위해 화면에 HTML 콘텐츠를 렌더링합니다.

이러한 호출은 임의의 단계에서 웹 페이지 논리에 의해 호출될 수 있는 독립적인 공개 API 호출을 나타내지 않습니다. 대신 모든 다음 단계가 이전 단계의 마지막 단계(콜백)에서 숨겨지는 체인 호출입니다.

쇼퍼블 대화형 이미지가 1단계, 부분적으로 2단계를 대체하는 것과 동시에, 사용자가 쇼퍼블 이미지 내에서 핫스팟을 선택할 때, 그러한 사용자 상호작용은 뷰어에 의해 처리된다. 뷰어가 이전에 Experience Manager Assets에 추가한 모든 핫스팟 데이터를 포함하는 웹 페이지에 이벤트를 반환합니다.

이러한 이벤트 처리기에서 프론트엔드 코드는 다음을 수행합니다.

* 쇼퍼블 대화형 이미지에서 방출되는 이벤트를 수신합니다.
* 핫스팟 데이터를 기반으로 빠른 보기 URL을 구성합니다.
* 백엔드에서 Quickview를 로드하고 화면에 렌더링하여 표시하는 프로세스를 트리거합니다.

Experience Manager Assets에서 반환한 포함 코드에는 이미 다음 강조 표시된 코드 조각에 표시된 대로 주석 처리된 바로 사용 가능한 이벤트 핸들러가 있습니다.

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
                    //To pass other parameter from the hotspot, you must add custom parameter during the hotspot setup as parameterName=value
                    loadQuickView(sku); //Replace this call with your Quickview plugin
                    //See your Quickviewer plugin for the Quickview call
                 },
             });
        */
        s7interactiveimageviewer.init();
```

따라서 코드의 주석 처리를 제거하고 더미 처리기 본문을 특정 웹 페이지에만 해당하는 코드로 바꾸기만 하면 됩니다.

Quickview URL을 구성하는 프로세스는 이전에 설명한 핫스팟 변수를 식별하는 데 사용되는 프로세스와 반대입니다.

다음을 참조하십시오 [핫스팟 변수 식별](#optional-identifying-hotspot-variables).

앞의 Quickview URL 예제를 사용하면 다음 예에서 각 경우에 Quickview URL이 구성되는 방식을 확인할 수 있습니다.

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

빠른 보기 URL을 트리거하고 빠른 보기 패널을 활성화하는 마지막 단계는 IT 부서의 프론트엔드 IT 직원의 지원이 필요할 수 있습니다. 바로 사용 가능한 빠른 보기 URL을 가지고 적절한 단계에서 빠른 보기 구현을 정확하게 트리거하는 방법을 가장 잘 알고 있는 지식을 보유하고 있습니다.

이러한 단계를 데모 웹 사이트에 적용하여 구매 가능한 대화형 이미지를 Quickview 코드와 완전히 통합하는 방법을 확인할 수 있습니다. 이전에는 빠른 보기 URL의 구조가 다음과 같이 식별되었습니다.

```xml
/datafeed/$categoryId$-$SKU$.json
```

내에서 이 URL을 재구성하려면 `quickViewActivate` 핸들러에서 `categoryId` 및 `SKU` 에서 사용할 수 있는 필드 `inData` 뷰어의 코드에서 처리기에 전달되는 개체:

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

데모 웹 사이트에서 간단한 을 사용하여 빠른 보기 대화 상자를 트리거하고 있습니다. `loadQuickView()` 함수 호출. 이 함수는 Quickview 데이터 URL인 인수를 하나만 사용합니다. 따라서 구매 가능한 대화형 이미지를 통합하는 마지막 단계는 다음에 다음 코드 행을 추가하는 것입니다 `quickViewActivate` 핸들러:

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

완전히 통합된 대화형 이미지가 포함된 최종 데모 웹 사이트는 다음과 같습니다.

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-3.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-3.html)

## 빠른 보기를 사용하여 사용자 지정 팝업 만들기 {#using-quickviews-to-create-custom-pop-ups}

다음을 참조하십시오 [빠른 보기를 사용하여 사용자 지정 팝업 만들기](/help/assets/custom-pop-ups.md).
