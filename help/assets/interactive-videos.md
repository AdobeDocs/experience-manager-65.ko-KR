---
title: 대화형 비디오
description: Dynamic Media에서 대화형 비디오 및 쇼퍼블 비디오를 사용하여 작업하는 방법을 알아봅니다
uuid: c3ff6839-fff5-4709-8163-5c4245b80e6d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 04be55f2-c7d8-45ef-89e5-58856b971de5
docset: aem65
feature: 대화형 비디오
role: Business Practitioner, Administrator
exl-id: d118879d-c17b-43f3-9cc8-0405531b4d9f
source-git-commit: 1cef6f87fa66fd78d439c23e6ac907f9531b8fd6
workflow-type: tm+mt
source-wordcount: '6058'
ht-degree: 0%

---

# 대화형 비디오{#interactive-videos}

비디오에서 직접 전환을 유도하는 쇼퍼블 비디오라고도 하는 대화형 비디오를 쉽게 만들 수 있습니다. 비디오에 대한 고객 참여는 비디오 플레이어와 함께 패널에서 발생합니다. 비디오 플레이어에서 관련 서비스, 정보 또는 제품 축소판 그림이 포함된 내용을 기준으로 스크롤하여 보기로 표시됩니다. 고객은 축소판을 탭하여 서비스에 직접 연결하거나, 항목을 장바구니에 추가하여 즉시 구매하거나, 웹 페이지에 연결하여 자세한 내용을 확인할 수 있습니다.

비디오가 종료되면 클릭유도하기 위해 모든 오퍼링의 시각적 요약이 표시됩니다. 고객은 원하는 항목을 탭할 수 있는 다른 기회를 갖게 됩니다. 실행 가능하고 특별한 환경(예: )이 있어야 고객 참여 및 전환이 증가합니다.

[대화형 이미지](/help/assets/interactive-images.md)도 참조하십시오.

## 대화형 비디오 실행 {#interactive-video-in-action}

상호 작용하며 쇼퍼블 비디오 기능을 보려면 [라이브 데모](https://landing.adobe.com/en/na/dynamic-media/ctir-2755/live-demos.html)를 클릭하고 페이지에서 **[!UICONTROL 쇼퍼블 미디어]** 헤딩으로 스크롤한 다음 쇼퍼블 비디오를 클릭합니다.

* 재생 중에 제품이 비디오에 사용되므로 동일한 제품이 축소판 이미지로 오른쪽에 나타납니다.

* 축소판을 클릭하여 비디오를 일시 중지하고 제품의 빠른 보기를 엽니다. 예를 들어, 비디오에서 KitchenAid 축소판 이미지를 클릭하여 믹서의 360도 스핀 보기를 경험하거나 확대하면서 혼합 세부 정보를 볼 수 있습니다.

<!-- There was a link here that showed the video frame of an interactive video and when the reader clicked the frame the video would play https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/AXIS/index.html. This now needs to call a new interactive video-->

![대화형 쇼퍼블 비디오에서 만든 ](assets/chlimage_1-126.png) *프레임대화형 쇼퍼블 비디오에서 비디오 프레임을 캡처합니다.*

>[!NOTE]
>
>사용자가 축소판 이미지를 클릭할 때 웹 페이지를 실행하는 대화형 비디오를 만들 경우, 일부 장치는 팝업 웹 페이지가 열리지 않도록 차단합니다. 이러한 경우 장치에서 팝업 차단 설정을 변경해야 합니다. 예를 들어 Apple iPhone 6에서는 **[!UICONTROL 설정]** > **Safari** > **팝업 차단**&#x200B;을 탭한 다음, 컨트롤을 **[!UICONTROL 해제]**&#x200B;로 슬라이드합니다. 이제 대화형 비디오를 재생하고 축소판을 클릭하면 팝업을 열겠는지 묻는 메시지가 표시됩니다. 수락하면 웹 페이지가 열립니다.

### 대화형 비디오를 만드는 방법 보기 {#watch-how-interactive-videos-are-created}

[대화형 비디오를 만드는 방법에 대한 7분 30초 연습을 시청하십시오](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveVideo) [](https://outv.omniture.com?v=s4NHQ2dzqd7hIqWjeG2sIdyNWsTWyupA).
(비디오 연습은 Assets on Demand로 브랜딩되지만, 원칙 및 단계는 AEM Assets의 대화형 비디오에 계속 적용됩니다.)

### Adobe 고객 성공 웨비나 {#adobe-customer-success-webinar}

&quot;AEM Assets에서 대화형 비디오, 링크 공유 및 YouTube 공유 사용&quot; 웨비나에서는 대화형 비디오 및 기타 기능을 사용하여 전환 기반 이벤트를 비디오 마케팅 컨텐츠에 연결하는 방법을 설명합니다.

>[!NOTE]
[AEM Assets에서 대화형 비디오, 링크 공유 및 YouTube 공유 사용](https://adobecustomersuccess.adobeconnect.com/p1yxzdo4aec/).

## 빠른 시작:대화형 비디오 {#quick-start-interactive-videos}

다음 단계별 워크플로우 설명은 Dynamic Media에서 대화형 비디오를 빠르게 시작하고 실행할 수 있도록 설계되었습니다.

일부 빠른 시작 작업 내에서 **예제** 제목을 찾습니다. 여기에는 *이 아직 여기에 추가된 인터랙션이 없는 이 시작 데모 웹 페이지를 기반으로 한 간단한 자습서가 포함되어 있습니다.*

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html)

**예제** 도움말은 웹 사이트에서 대화형 비디오를 통합하는 단계를 보여줍니다.

마지막 예제 섹션에서 자습서를 완료하면 완전히 통합된 대화형 비디오가 있는 최종 데모 웹 페이지의 모습은 다음과 같습니다.

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-3.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-3.html)

대화형 비디오 단계:

1. **(선택 사항) Quickview 변수 식별**  - 기존 Quickview 구현에서 사용하는 동적 변수를 식별하여 시작합니다. 대화형 비디오를 만들 때 변수를 사용하여 제품 축소판 그림을 해당 제품 빠른 보기에 매핑합니다. [(선택 사항) Quickview 변수 식별](#optional-identifying-quickview-variables)을 참조하십시오.
   *이 단계는 다음 사항이 모두 참인 경우에만 필요합니다*.・ 빠른 보기를 트리거하여 비디오에 상호 작용을 추가하려고 합니다.
・ AEM 구현에서는 IBM Websphere Commerce, Elastic Path, hybris 또는 Intershop과 같은 eCommerce 솔루션에서 제품 데이터를 AEM으로 가져오는 데 eCommerce 통합 프레임워크를 사용하지 *않습니다.* AEM Assets](/help/commerce/cif-classic/administering/concepts.md)에서 [eCommerce 개념을 참조하십시오.

1. **(선택 사항) 대화형 비디오 뷰어 사전 설정 만들기**  - 비디오 스크러버 및 대화형 축소판과 같은 플레이어를 구성하는 다양한 구성 요소의 모양과 동작을 사용자 정의합니다.
기본 제공 대화형 비디오 뷰어 사전 설정 `Shoppable_Video_Light` 또는 `Shoppable_Video_Dark` 을 대신 사용하려는 경우에는 대화형 비디오 뷰어 사전 설정을 직접 만들 필요가 없습니다.
[새 뷰어 사전 설정 만들기](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset)(선택 사항) 및 [대화형 뷰어 사전 설정을 만들기 위한 특수 고려 사항](/help/assets/managing-viewer-presets.md#special-considerations-for-creating-an-interactive-viewer-preset)을 참조하십시오.

1. **비디오 및 관련 이미지 자산 업로드**  - 대화형으로 만들려는 비디오 및 관련 이미지를 업로드합니다.
[비디오 및 관련 축소판 자산 업로드](#uploading-a-video-and-its-associated-thumbnail-assets)를 참조하십시오.

1. **비디오에 대화형 활동 추가**  - 비디오에 하나 이상의 시간 세그먼트를 추가합니다. 그런 다음 해당 시간 세그먼트 내에서 이미지 축소판을 연결합니다. 하이퍼링크, 빠른 보기 또는 경험 조각과 같은 작업에 각 이미지 축소판을 할당합니다.
(대화형 컨텐츠에 상대 URL이 있는 링크, 특히 AEM Sites 페이지에 대한 링크가 있는 경우 URL 기반 연결 방법이 지원되지 않습니다.)
대화형 비디오 자산을 게시하여 완료합니다. 게시하면 나중에 복사하여 웹 사이트 랜딩 페이지에 적용할 포함 코드 또는 URL이 만들어집니다.자세한 내용은 [비디오에 대화형 활동 추가](#adding-interactivity-to-your-video)를 참조하십시오.
[자산 게시](/help/assets/publishing-dynamicmedia-assets.md)를 참조하십시오.

1. **AEM Sites, AEM eCommerce 또는**
두 가지 모두를 사용하는 경우 AEMI에서 웹 사이트 또는 웹 사이트에 대화형 비디오를 추가하십시오. 대화형 미디어 구성 요소를 페이지에 드래그하여 AEM의 웹 페이지에 직접 대화형 비디오를 추가할 수 있습니다. [페이지에 Dynamic Media 자산 추가 를 참조하십시오.](/help/assets/adding-dynamic-media-assets-to-pages.md)
포함 코드 또는 URL을 사용하여 대화형 비디오를 웹 사이트 환경과 통합합니다. [웹 사이트와 대화형 비디오 통합](#integrating-an-interactive-video-with-your-website)을 참조하십시오.
타사 WCM(Web Content Manager)을 사용하는 경우, 새 대화형 비디오를 웹 사이트에서 사용되는 기존 Quickview 구현과 통합해야 합니다. [기존 Quickview](#integrating-an-interactive-video-with-an-existing-quickview)와 대화형 비디오 통합 을 참조하십시오.
   [페이지에 Dynamic Media 자산 추가](/help/assets/adding-dynamic-media-assets-to-pages.md)

## (선택 사항) Quickview 변수 식별 {#optional-identifying-quickview-variables}

>[!NOTE]
이 작업은 다음 내용이 true인 경우에만 필요합니다.
* 빠른 보기를 트리거하여 비디오에 상호 작용을 추가하려고 합니다.
* AEM 구현에서는 IBM Websphere Commerce, Elastic Path, hybris 또는 Intershop과 같은 eCommerce 솔루션에서 제품 데이터를 AEM으로 가져오는 데 eCommerce 통합 프레임워크를 사용하지 *않습니다.* AEM Assets](/help/commerce/cif-classic/administering/concepts.md)에서 [eCommerce 개념을 참조하십시오.

AEM 구현에서 eCommerce를 사용하는 경우 이 작업을 건너뛰고 다음 작업으로 진행할 수 있습니다.

먼저 기존 Quickview 구현에서 사용하는 동적 변수를 식별하여 대화형 비디오 작성 프로세스 동안 제품 축소판을 해당 제품 Quickview에 매핑할 수 있습니다.

비디오에 시간 세그먼트를 추가하면 세그먼트에 추가하는 각 섬네일에 SKU와 추가 변수를 할당합니다. 이러한 변수는 나중에 적절한 빠른 보기 제품을 표시하는 데 사용됩니다.

제품 빠른 보기를 고유하게 트리거하는 데 필요한 변수를 올바르게 식별하는 것이 중요합니다.

기존 Quickview 구현을 담당하는 IT 전문가에게 문의하는 것도 충분할 수 있습니다. 따라서 시스템에서 빠른 보기를 식별하는 데 필요한 최소 데이터 세트를 알 수 있을 것입니다. 그러나 대부분의 경우 프런트 엔드 코드의 기존 동작을 간단히 분석할 수도 있습니다.

대부분의 Quickview 구현은 다음 패러다임을 사용합니다.

* 사용자가 웹 사이트에서 사용자 인터페이스 요소를 활성화합니다. 예를 들어 &quot;빠른 보기&quot; 단추를 클릭합니다.
* 필요한 경우 웹 사이트에서 Quickview 데이터 또는 콘텐츠를 로드하기 위해 백엔드에 Ajax 요청을 보냅니다.
* 빠른 보기 데이터는 웹 페이지에서 렌더링을 준비하기 위해 컨텐츠로 변환됩니다.
* 마지막으로 프런트 엔드 코드는 그러한 콘텐츠를 화면에서 시각적으로 렌더링합니다.

따라서 이 방법은 Quickview가 구현된 기존 웹 사이트의 다양한 영역을 방문하고, Quickview를 트리거하며, Quickview 데이터 또는 컨텐츠를 로드하기 위해 웹 페이지에서 보낸 Ajax URL을 캡처하는 것입니다.

일반적으로 전문 디버깅 도구를 사용할 필요가 없습니다. 최신 웹 브라우저에는 적절한 작업을 수행하는 웹 검사자가 포함되어 있습니다. 다음은 웹 관리자를 포함하는 웹 브라우저의 몇 가지 예입니다.

* Google Chrome에서 나가는 HTTP 요청을 모두 보려면 **F12**(Windows) 또는 **Command+Options+I**(Mac)를 눌러 개발자 도구 패널을 열고 **네트워크** 탭을 클릭하십시오.

* Firefox에서는 **F12**(Windows) 또는 **Command+Option+I**(Mac)를 눌러 Firebug 플러그인을 활성화하고 해당 **`[Net]`** 탭을 사용하거나 내장된 Inspector 도구 및 해당 네트워크 탭을 사용할 수 있습니다.

* Internet Explorer에서 **F12**&#x200B;를 눌러 디버거 도구를 활성화합니다.

브라우저에서 네트워크 모니터링이 켜져 있으면 페이지에서 빠른 보기를 트리거합니다.

이제 네트워크 로그에서 Quickview Ajax URL을 찾아 기록된 URL을 복사하여 향후 분석할 수 있습니다. 대부분의 경우 빠른 보기를 트리거할 때 서버로 전송되는 요청이 많습니다. 일반적으로 Quickview Ajax URL은 목록에서 첫 번째 중 하나입니다. 여기에는 복잡한 쿼리 문자열 부분 또는 경로가 있으며 해당 응답 MIME 유형은 `text/html`, `text/xml` 또는 `text/javascript`입니다.

이 프로세스 중에는 다양한 제품 카테고리와 유형을 사용하여 웹 사이트의 다양한 영역을 방문하는 것이 중요합니다. 그 이유는 Quickview URL에 주어진 웹 사이트 카테고리에 공통되는 부분이 있을 수 있지만 웹 사이트의 다른 영역을 방문하는 경우에만 변경되기 때문입니다.

가장 간단한 경우 Quickview URL에 있는 유일한 변수 부분은 제품 SKU입니다. 이 경우 제품 SKU 값은 AEM의 대화형 비디오에서 시간 세그먼트에 축소판을 추가하는 데 필요한 유일한 데이터 조각입니다.

그러나 복잡한 경우, Quickview URL은 카테고리 ID, 색상 코드 등과 같은 제품 SKU 외에도 다양한 요소를 갖습니다. 이러한 경우 이러한 모든 요소는 AEM의 축소판 데이터 정의에서 별도의 변수가 됩니다.

Quickview URL 및 그 결과 축소판 변수의 다음 예를 생각해 보십시오.

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
    </ul> <p>URL의 유일한 변수 부분은 <code>productId=</code> 쿼리 문자열 매개 변수의 값이며 이는 명확하게 SKU 값입니다. 따라서 미리 보기에서는 <strong><code>866558</code></strong>, <strong><code>1196184</code></strong>, <strong><code>1081492</code></strong>, <strong><code>1898294</code></strong> 등의 값으로 채워진 SKU 필드만 필요합니다.</p> </td>
  </tr>
  <tr>
    <td><p>URL 경로에 있는 단일 SKU입니다.</p> </td>
    <td><p>기록된 Quickview URL은 다음과 같습니다.</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>변수 부품은 경로의 마지막 부분에 있으며 AEM 축소판 그림의 SKU 값이 됩니다.<strong><code>6422350843</code></strong>, <strong><code>1607745002</code></strong>, <strong><code>0086724882</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>쿼리 문자열의 SKU 및 카테고리 ID.</p> </td>
    <td><p>기록된 Quickview URL은 다음과 같습니다.</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>이 경우 URL에는 두 가지 다양한 부분이 있습니다. SKU는 <code>prodId</code> 매개 변수에 저장되고 카테고리 ID는 <code>category=</code> 매개 변수에 저장됩니다.</p> <p>이와 같이 축소판 정의는 쌍입니다. 즉, SKU 값과 <code>categoryId</code>이라는 추가 변수입니다. 결과 쌍은 다음과 같습니다.</p>
    <ul>
      <li>SKU는 <code>305466</code>이고 <code>categoryId</code>은 <code>1100004</code></li>
      <li>SKU는 <code>310181</code>이고 <code>categoryId</code>은 <code>1100004</code></li>
      <li>SKU는 <code>308706</code>이고 <code>categoryId</code>은 <code>1740148</code></li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**예**

위의 접근 방식이 예제 웹 사이트에 적용되면 각각 &quot;자세히 보기&quot; 단추가 있는 여러 제품 축소판이 포함된 웹 페이지가 표시됩니다.

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html)

페이지에서 사용할 수 있는 모든 제품 빠른 보기를 활성화하면 백엔드에 대한 다음 Quickview 요청 목록을 가져올 수 있습니다.

* datafeed/candles-233396346.json
* datafeed/candles-233978050.json
* datafeed/candles-234024346.json
* datafeed/candles-234024356.json
* datafeed/candles-234024359.json
* datafeed/cushions-233939848.json
* datafeed/cushions-234019477.json
* datafeed/cushions-234019483.json
* datafeed/furniture-231747479.json
* datafeed/furniture-232625621.json
* datafeed/furniture-232625626.json
* datafeed/furniture-233939810.json
* datafeed/furniture-233939825.json
* datafeed/furniture-233939828.json
* datafeed/furniture-233939853.json
* datafeed/furniture-233940334.json
* datafeed/glassware-000064007.json
* datafeed/glassware-230722193.json
* datafeed/glassware-233916550.json
* datafeed/glassware-233916597.json

이러한 서버 호출을 보면 제품별 정보가 요청 경로에만 있음을 알 수 있습니다. 또한 쿼리 문자열이 전혀 사용되지 않으며 두 가지 데이터 유형이 관련되어 있습니다.

* 첫 번째 유형은 초, 쿠션, 가구, 그리고 유리용기이다. 이를 &quot;제품 카테고리&quot;라고 할 수 있습니다.
* 두 번째 유형은 233916597과 같은 제품 코드입니다. 제품 SKU라고 가정할 수 있습니다.

이 정보가 주어지면 전체 Quickview URL은 다음 패턴을 가집니다.

`/datafeed/$categoryId$-$SKU$.json`

이러한 분석을 기반으로 축소판에 다음 두 변수를 사용할 수 있다고 결론 짓습니다.`categoryId` 및 `SKU`

이제 비디오 및 관련 축소판 자산을 업로드할 준비가 되었습니다.

## (선택 사항) 대화형 비디오 뷰어 사전 설정 만들기 {#optional-creating-an-interactive-video-viewer-preset}

기본 대화형 비디오 뷰어 사전 설정 유형 `Shoppable_Video_dark` 또는 `Shoppable_Video_light` 중 하나를 사용하려는 경우 이 작업을 건너뛰고 다음 작업을 계속 진행할 수 있습니다.

작성 환경에서 축소판을 클릭하면 빠른 보기 대화 상자의 미리 보기가 나타납니다.

![chlimage_1-21](assets/chlimage_1-127.png)

사용자 정의 대화형 비디오 뷰어 사전 설정을 선택적으로 만들 수 있습니다. 특히 비디오 플레이어의 스타일링, 대화형 축소판, 비디오 끝에 표시되는 축소판 그림 그리드 보기를 결정할 수 있습니다.

대화형 비디오 뷰어 사전 설정이 추가한 비디오 및 모든 타임라인 세그먼트를 올바르게 렌더링합니다. 또한 미리 보기 모드에서 제품 축소판을 클릭할 때 기본 Quickview 예시를 사용하므로 게시하기 전에 해당 상호 작용을 테스트할 수 있습니다.

뷰어 사전 설정을 저장하면 [뷰어 사전 설정] 페이지에서 해당 상태가 **On**으로 자동으로 설정됩니다. 이 상태는 Dynamic Media 구성 요소에 표시되고 이 구성 요소로 비디오를 미리 볼 때마다 표시됩니다. 새 뷰어 사전 설정을 수동으로 게시해야 합니다.

고유한 대화형 비디오 뷰어 사전 설정을 만들려면 [새 뷰어 사전 설정 만들기](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset) 를 참조하십시오.

## 비디오와 관련 썸네일 자산 업그레이드 {#uploading-a-video-and-its-associated-thumbnail-assets}

비디오 및 축소판 자산을 이미 업로드한 경우 [비디오에 상호 작용 추가](#adding-interactivity-to-your-video)로 진행합니다.

잘못된 비디오나 이미지를 업로드했거나 더 이상 필요하지 않은 업로드된 비디오나 이미지를 삭제하려면 [자산 삭제](/help/assets/manage-assets.md#deleting-assets)를 참조하십시오.

비디오 및 관련 축소판 자산을 업로드하려면 다음을 수행하십시오.

1. 비디오 및 연결된 축소판 자산을 원하는 폴더나 폴더에 업로드합니다.

   [자산 업로드](/help/assets/manage-assets.md)를 참조하십시오.
[FTP 작업 예약을 사용하여 자산 업로드](/help/assets/manage-assets.md)를 참조하십시오.

   이제 비디오에 대화형 기능을 추가합니다.

## 비디오에 대화형 기능 추가 {#adding-interactivity-to-your-video}

대화형 비디오 만들기 페이지에서 즉석 시각적 편집기를 사용하여 비디오에 타임라인 세그먼트를 추가합니다.

타임라인 세그먼트를 추가한 후 각 세그먼트 내에 축소판 이미지를 추가합니다. 추가한 각 축소판에 대해 작업을 적용합니다. 예를 들어, 섬네일에 빠른 보기를 적용하거나, 하이퍼링크를 지정하거나 경험 조각을 지정할 수 있습니다.

[경험 구성요소](/help/sites-authoring/experience-fragments.md)를 참조하십시오.

>[!NOTE]
경험 조각에 뷰어를 포함할 때 대화형 비디오의 소셜 미디어 공유 도구는 지원되지 않습니다. 이 문제를 해결하려면 소셜 미디어 공유 도구가 없는 뷰어 사전 설정을 사용하거나 만들 수 있습니다. 이러한 뷰어 사전 설정을 사용하면 경험 조각에 성공적으로 포함할 수 있습니다.

>[!NOTE]
대화형 컨텐츠에 상대 URL이 있는 링크, 특히 AEM Sites 페이지에 대한 링크가 있는 경우 URL 기반 연결 방법이 없습니다.

현재 작성/편집 세션 중에 페이지의 오른쪽 위 모서리 근처에 있는 실행 취소 및 재실행 옵션이 지원됩니다.

대화형 비디오를 저장하면 비디오가 즉시 미리 보기에 열립니다. 여기에서 대화형 비디오 뷰어 사전 설정을 선택하고 비디오를 재생하여 고객에게 표시되는 모양을 대략적으로 볼 수 있습니다.

비디오에 대화형 기능을 추가하려면:

1. 자산 보기에서 업로드한 비디오로 이동하고 대화형 항목으로 만들 비디오로 이동합니다.
1. 다음 중 하나를 수행하십시오.

   * 이미지를 마우스로 가리킨 다음 **[!UICONTROL 선택]**(확인 표시 아이콘)을 탭합니다. 도구 모음에서 **[!UICONTROL 편집.]**

   * 이미지를 마우스로 가리킨 다음 **[!UICONTROL 추가 작업]**(세 점 아이콘) **[!UICONTROL 편집.]**

   * 이미지를 탭하여 세부 사항 보기 페이지에서 엽니다. 도구 모음에서 **[!UICONTROL 편집.]**

1. 대화형 비디오 만들기 페이지에서 다음 중 하나를 수행합니다.

   * 비디오 재생을 시작하려면 **[!UICONTROL 재생]** 단추를 탭합니다. 강조 표시할 특정 제품, 서비스 또는 세부 사항이 표시되면 도구 모음에서 **[!UICONTROL 세그먼트 추가]**&#x200B;를 누릅니다. 비디오 끝에 도달할 때까지 이 작업을 반복합니다.

      추가할 때마다 축소판 이미지를 하나 이상 지정한 다음 해당 축소판 이미지를 Quickview 제품 페이지에 연결하여 고객이 구매할 수 있도록 하거나 웹 페이지에 자세한 정보를 추가할 수 있습니다.

   * 비디오 재생을 시작하려면 **[!UICONTROL 재생]** 단추를 탭합니다. 강조 표시할 특정 제품, 서비스 또는 세부 사항이 표시되면 **[!UICONTROL 일시 정지를 누릅니다.]** 세그먼트  **[!UICONTROL 추가 를 누릅니다.]**

      비디오 끝에 도달할 때까지 세그먼트를 추가할 타임라인의 지점에서 비디오를 계속 재생하고 일시 중지합니다.

1. (선택 사항) **[!UICONTROL 타임라인 배율 슬라이더]**&#x200B;의 막대를 왼쪽으로 끌어 확대 또는 축소하여 추가한 세그먼트에 대한 세부 사항의 양을 제어합니다.

   ![chlimage_1-22](assets/chlimage_1-128.png)

   비디오 길이에 따라 세그먼트 지속 기간의 기본값은 다음 값으로 설정됩니다.

   <table>
      <tbody>
        <tr>
        <td><strong>비디오 길이가..</strong></td>
        <td><strong>세그먼트 기간 설정은 기본적으로..</strong></td>
        </tr>
        <tr>
        <td>3분 이상</td>
        <td>60초</td>
        </tr>
        <tr>
        <td>2-3분</td>
        <td>30초</td>
        </tr>
        <tr>
        <td>1 ~ 2분</td>
        <td>20초<br /> </td>
        </tr>
        <tr>
        <td>30-60초</td>
        <td>10초</td>
        </tr>
        <tr>
        <td>30초 이하</td>
        <td>5초</td>
        </tr>
      </tbody>
    </table>

   비디오 타임라인은 사용 가능한 만큼의 화면 공간을 사용합니다. 따라서 브라우저 크기를 조정할 때 추가한 세그먼트의 너비가 올바르게 유지됩니다.

   예시 하기 위해 다음 세 스크린샷에서는 동일한 비디오를 사용합니다. 각 세그먼트의 너비는 타임라인 비율 설정에 따라 달라집니다.

   ![chlimage_1-23](assets/chlimage_1-129.png)

   스크린샷 A

   위의 스크린샷 A는 29초 제품 비디오의 기본 보기를 보여 줍니다. [타임라인 비율]은 기본적으로 5초로 설정되어 있습니다.

   ![chlimage_1-130](assets/chlimage_1-130.png)

   스크린샷 B

   위의 스크린샷 B에서는 타임라인 비율 슬라이더가 기본값인 5초에서 3초로 드래그되었습니다. 개별 타임라인 크기 조정 타임스탬프가 이제 3초 간격으로 모두 설정됩니다.

   ![chlimage_1-25](assets/chlimage_1-131.png)

   스크린샷 C

   위의 스크린샷 C에서 타임라인 비율 설정이 8초로 이동되었습니다. 제품 축소판이 포함된 세그먼트가 어떻게 축소되었는지 확인합니다. 이러한 확대/축소는 긴 비디오가 있고 일반적으로 페이지 너비에 맞는 추가 세그먼트에 대한 개요를 보려는 경우 유용합니다.

1. (선택 사항) 다음 중 하나를 수행합니다.

   * 세그먼트의 시작 시간 및 종료 시간을 조정하려면

      세그먼트를 선택한 다음 선행 또는 후행 파란색 타원을 드래그하여 각각 시작 또는 종료 시간을 조정합니다. 표시되는 비디오 프레임은 조정에 따라 비디오의 적절한 시간으로 이동합니다. 타임라인 세그먼트의 이동은 타임라인에 인접한 모든 세그먼트를 기반으로 제한됩니다. 허용되는 최소 세그먼트 시간은 1초입니다.

      다음 탐색 단축키를 사용하여 비디오 세그먼트를 빠르게 확인하고 세밀하게 조정할 수 있습니다.

      * 앞쪽의 파란색 타원을 탭하여 해당 세그먼트의 시작 부분으로 직접 비디오를 찾습니다.
      * 후행 파란색 타원을 탭하여 해당 세그먼트의 끝까지 비디오를 직접 찾습니다.
      * 전체 세그먼트를 탭하여 비디오 재생을 해당 세그먼트의 시작으로 돌아갑니다

   ![chlimage_1-26](assets/chlimage_1-132.png)

   타임라인 세그먼트의 끝 위치 변경

   * 세그먼트를 삭제하려면

      타임라인에 있는 마지막 세그먼트를 선택한 다음 도구 모음에서 **[!UICONTROL 세그먼트 삭제 를 누릅니다.]** 두 개 이상의 세그먼트를 선택한 경우 세그먼트 삭제 기능이 비활성화됩니다.

      마지막 세그먼트만 삭제할 수 있습니다. 예를 들어 타임라인에서 모든 세그먼트를 삭제하려면 항상 마지막 세그먼트를 선택한 다음 **[!UICONTROL 세그먼트 삭제]**&#x200B;를 탭해야 합니다.


1. 하나 이상의 축소판 이미지를 연결할 시간 세그먼트를 선택합니다.
1. 비디오 오른쪽의 **[!UICONTROL 컨텐츠]** 탭을 탭합니다.
1. 컨텐츠 탭에서 **[!UICONTROL 자산 선택]** 을 누른 다음 비디오에 사용할 이미지 자산을 모두 찾아 선택합니다. 선택한 자산이 콘텐츠 탭의 자산 선택기 패널에 추가됩니다.

1. 컨텐츠 탭 아래의 자산 선택기에서 다음 중 하나를 수행합니다.

   <table>
      <tbody>
        <tr>
        <td>축소판을 선택한 타임라인 세그먼트에 연결하려면</td>
        <td><p>오른쪽의 자산 선택기 패널에서 이미지를 탭합니다.</p> <p>타임라인 세그먼트에 원하는 만큼 축소판을 추가할 수 있습니다. 선택하는 각 이미지에 대해 자산 선택기의 이미지 위에 확인 표시가 나타납니다.</p> </td>
        </tr>
        <tr>
        <td>선택한 타임라인 세그먼트에서 축소판을 제거하려면</td>
        <td><p>다음 중 하나를 수행합니다.</p>
          <ul>
          <li>자산 선택기 패널에서 확인 표시가 있는 이미지를 탭하여 이미지를 선택 해제합니다. 이미지 자산이 타임라인 세그먼트에서 제거됩니다.<br /> </li>
          <li>선택한 타임라인 세그먼트에서 이미지를 탭한 다음, 도구 모음에서 <strong>제품 삭제</strong>를 탭합니다.</li>
          </ul> </td>
        </tr>
      </tbody>
    </table>

   ![자산 선택기](assets/chlimage_1-133.png)

   자산 선택기 패널에서 이미지를 탭하면 선택한 타임라인 세그먼트에 추가됩니다.

1. 타임라인 세그먼트 중 하나에서 단일 축소판 이미지를 선택한 다음 **[!UICONTROL 작업]** 탭을 탭합니다.
1. 다음 중 하나를 수행합니다.
   <table> 
    <tbody> 
      <tr> 
      <td>선택한 축소판 이미지를 빠른 보기에 연결하려면</td> 
      <td><p>작업 유형에서 <strong>Quickview</strong>를 누릅니다.</p> <p>AEM Sites 및 Ecommerce 고객인 경우:</p> 
       <ul> 
       <li>SKU 값 텍스트 필드는 사용자가 제공하는 각 개별 제품 또는 서비스의 고유 식별자인 선택한 제품의 SKU(Stock Keeping Unit)로 미리 채워집니다. 이미지가 AEM Commerce의 제품과 연결되면 자동으로 채워집니다.</li> 
       <li>미리 채워진 SKU가 올바르지 않은 경우 제품 선택기 아이콘(확대경)을 탭하거나 클릭하여 제품 선택 페이지를 엽니다. 사용할 제품을 탭하거나 클릭한 다음, 페이지의 오른쪽 위 모서리에 있는 확인 표시를 탭하여 대화형 비디오 편집기로 돌아갑니다.</li> 
       </ul> <p> AEM Sites 또는 Ecommerce 고객이 아닌 <em>입니다.</em></p> 
       <ul> 
       <li><a href="/help/assets/carousel-banners.md#identifying-hotspot-and-image-map-variables">핫스팟 변수 식별</a>을 참조하십시오. 이러한 변수를 정의해야 합니다. </li> 
       <li>기본적으로 이 SKU 필드는 확장자 없이 이미지 자산의 파일 이름을 사용합니다. SKU를 기반으로 파일에 대한 표준 명명 규칙을 따르는 경우 일반적으로 추가적인 편집이 필요하지 않습니다. </li> 
       <li>그렇지 않으면 기본값을 편집하고 올바른 SKU 값을 입력합니다. SKU 값 텍스트 필드에 제공하는 각 개별 제품 또는 서비스의 고유 식별자인 제품의 SKU(Stock Keeping Unit)를 입력합니다. 입력한 SKU 값은 시스템이 탭한 이미지를 특정 SKU의 빠른 보기와 연결하도록 빠른 보기 템플릿의 변수 부분을 자동으로 채웁니다.</li> 
       </ul> <p>(선택 사항) Quickview 내에 제품을 추가로 식별하는 데 사용해야 하는 다른 변수가 있는 경우 <strong>일반 변수 추가</strong>를 누릅니다. 텍스트 필드에서 추가 변수를 지정합니다. 예를 들어 <code>category=Womens</code>은 추가된 변수입니다.</p> <p> </p> </td> 
      </tr> 
      <tr> 
      <td>선택한 축소판 이미지를 하이퍼링크와 연결하려면</td> 
      <td><p>작업 유형에서 <strong>하이퍼링크</strong>를 탭한 후 다음 중 하나를 수행합니다.</p> 
       <ul> 
       <li>AEM Sites 고객인 경우 사이트 선택기 아이콘(폴더)을 탭하여 웹 페이지로 이동합니다. 대화형 컨텐츠에 상대 URL이 있는 링크, 특히 AEM Sites 페이지에 대한 링크가 있는 경우 URL 기반 연결 방법이 지원되지 않습니다.</li> 
       <li>독립형 Dynamic Media 고객인 경우, HREF 텍스트 필드에서 연결된 웹 페이지에 대한 전체 URL 경로를 지정합니다.</li> 
       </ul> <p>링크를 새 브라우저 탭에서 열지 또는 현재 탭에서 열지를 지정합니다.</p> </td> 
      </tr> 
      <tr> 
      <td>선택한 축소판 이미지를 경험 조각과 연결하려면</td> 
      <td><p>작업 유형에서 <strong>경험 조각</strong>을 탭한 후 다음을 수행합니다.<p> 
       <ul> 
       <li>AEM Sites 고객인 경우 검색 아이콘(확대경)을 탭하거나 클릭하여 경험 조각 페이지를 엽니다. 사용할 경험 조각을 탭하거나 클릭한 다음, 페이지의 오른쪽 위 모서리에서 <strong>선택 </strong>을 탭하여 이전 페이지의 작업 패널로 돌아갑니다.<br /> 경험  <a href="/help/sites-authoring/experience-fragments.md">구성요소 를 참조하십시오</a>.</li> 
      </ul> 
       <ul> 
       <li>경험 조각의 폭과 높이를 비디오에 나타낼 지정합니다.</li>
       </ul><strong>참고</strong>:경험 조각에 뷰어를 포함할 때 대화형 비디오의 소셜 미디어 공유 도구는 지원되지 않습니다. 이 문제를 해결하려면 소셜 미디어 공유 도구가 없는 뷰어 사전 설정을 사용하거나 만들 수 있습니다. 이러한 뷰어 사전 설정을 사용하면 경험 조각에 성공적으로 포함할 수 있습니다.</p></tr>&lt;&gt; 
      <tr> 
      <td>축소판 이미지에 이미 할당된 작업을 편집하려면</td> 
      <td>타임라인 세그먼트 내에서 텍스트 레이블 오른쪽에 체인 링크가 있는 축소판 이미지를 누릅니다. 체인 링크는 작업이 할당되었음을 나타냅니다. <strong>작업</strong> 탭을 탭하여 변경합니다.</td> 
      </tr> 
      <tr> 
      <td>축소판 이미지의 텍스트 레이블을 변경하려면</td> 
      <td><p>기본적으로 텍스트 레이블은 축소판 이미지의 <code>Title</code> 메타데이터 필드를 사용합니다. <code>Title</code> 이 없으면 축소판 이미지의 파일 이름이 대신 사용되지만 확장명이 없습니다.</p> <p>축소판 이미지의 텍스트 레이블을 변경하려면 표시되는 이미지 자산 바로 아래에 있는 <strong>작업 </strong>탭에서 원하는 텍스트를 입력합니다. 아래 그림을 참조하십시오.</p> <p>새 텍스트 레이블은 비디오 플레이어 자체와 타임라인 세그먼트에 표시되는 축소판 텍스트에서만 사용됩니다. 레이블 변경은 축소판 이미지의 제목 메타데이터 필드나 파일 이름에 영향을 주지 않습니다.</p> </td> 
      </tr> 
      <tr> 
      <td>변경한 내용을 되돌리기</td> 
      <td>페이지의 오른쪽 위 모서리 근처에 있는 <strong>실행 취소</strong> 또는 <strong>재실행</strong>을 누릅니다.</td> 
      </tr> 
    </tbody> 
   </table>

   ![experiencefragment_interactivevideos](assets/experiencefragment_interactivevideos.png)

   축소판 이미지에 새 텍스트 레이블이 추가됩니다.

1. 다음 중 하나를 수행하십시오.

   * 6-11단계를 반복하여 비디오의 타임라인 세그먼트에 축소판 이미지를 더 추가합니다.
   * 옵션 단계 13으로 계속 진행합니다.

1. (선택 사항) 다음 중 하나를 수행합니다.

   * **[!UICONTROL 세그먼트 병합]**  - 인접한 두 세그먼트(지정된 제품 축소판이 있거나 없는)를 하나의 세그먼트로 결합할 수 있습니다.

      타임라인에서 1에 병합할 두 개 이상의 연속 세그먼트를 누릅니다. 아래 그림에서 선택한 두 세그먼트에 파란색 타원 드래그 핸들이 없습니다.

      도구 모음에서 **[!UICONTROL 세그먼트 병합]**&#x200B;을 누릅니다.
   ![chlimage_1-134](assets/chlimage_1-134.png)

   선택한 두 개의 5초 세그먼트를 10초 세그먼트로 병합합니다.

   * **[!UICONTROL 세그먼트 분할]**  - 단일 세그먼트를 두 개의 동일한 시간 세그먼트로 나눌 수 있습니다. 세그먼트에 이미 지정된 제품 축소판이 있는 경우 축소판이 왼쪽 세그먼트에 결합됩니다.

      타임라인에서 반으로 나눌 세그먼트를 탭한 다음, 도구 모음에서 **[!UICONTROL 세그먼트 분할]** 을 탭합니다.

      두 개 이상의 세그먼트를 선택하면 **[!UICONTROL 세그먼트 분할]** 기능이 비활성화됩니다.
   ![chlimage_1-135](assets/chlimage_1-135.png)

   선택한 10초 세그먼트를 각각 5초의 두 세그먼트로 분할합니다.

1. **[!UICONTROL 대화형 비디오 만들기]** 페이지의 오른쪽 위 모서리 근처에 비디오에 사용된 현재 선택한 뷰어 사전 설정의 이름이 표시됩니다. 다른 뷰어 사전 설정을 선택하려면 이름을 누릅니다.

   예를 들어 `Shoppable_Video_light` 뷰어 사전 설정을 사용하면 비디오와 인접한 흰색 표시 영역과 함께 비디오를 재생할 수 있습니다. 표시 영역은 재생 중에 클릭 가능한 축소판 이미지가 표시되는 영역입니다. `Shoppable_Video_dark` 뷰어 사전 설정을 사용하면 비디오와 인접한 검정색 표시 영역과 함께 비디오를 재생할 수 있습니다.

   자신만의 대화형 비디오 뷰어 사전 설정을 만든 경우, 선택할 수 있는 사전 설정 목록에도 이 사전 설정이 표시됩니다.

   완료되면 **[!UICONTROL 저장.]**

   >[!NOTE]
   대화형 비디오를 저장하면 연결된 `.vtt` 파일이 자동으로 저장됩니다. `.vtt` 파일은 **[!UICONTROL Assets의 루트에 있는 `_VTT` 폴더에 저장됩니다.]** 대화형 비디오가 웹 사이트에서 올바르게 재생되려면 파일 및 폴더가 필요합니다. 따라서 `_VTT` 폴더 또는 해당 컨텐츠를 이동, 편집 또는 삭제하지 마십시오.

1. 대화형 비디오를 게시합니다. 게시하면 웹 사이트 경험에 최종적으로 복사하여 붙여넣을 포함 코드 또는 URL이 만들어집니다.

   빠른 보기를 사용하여 상호 작용을 추가한 경우 포함 코드만 사용하십시오.하이퍼연결된 웹 페이지가 포함된 상호 작용을 추가한 경우 게시된 URL을 사용할 수도 있습니다. 그러나 대화형 컨텐츠에 상대 URL이 있는 링크, 특히 AEM Sites 페이지에 대한 링크가 있는 경우에는 URL 기반 연결 방법이 가능하지 않습니다.

   [자산 게시](publishing-dynamicmedia-assets.md)를 참조하십시오.

   >[!NOTE]
   Quickviews를 사용하여 쇼퍼블 비디오를 게시하려면 상거래 영역에서 각 비디오의 관련 이미지 자산을 별도로 게시해야 합니다.

   타임라인 세그먼트를 추가하고 대화형 비디오를 게시하면 기존 웹 사이트 랜딩 페이지에 추가할 수 있습니다. [웹 사이트와 대화형 비디오 통합](#integrating-an-interactive-video-with-your-website) 을 참조하십시오.

## 대화형 비디오 자산 게시 {#publishing-interactive-video-assets}

대화형 비디오 자산을 게시하는 방법에 대한 자세한 내용은 [자산 게시](/help/assets/publishing-dynamicmedia-assets.md) 를 참조하십시오.

## 웹 사이트 {#integrating-an-interactive-video-with-your-website}와 대화형 비디오 통합

이제 비디오를 업로드하고, 여기에 타임라인 세그먼트를 추가하고, 대화형 비디오를 게시하면 기존 웹 사이트에 추가할 수 있습니다.

AEM Sites 고객의 경우 대화형 미디어 구성 요소를 페이지로 드래그하여 대화형 비디오를 추가할 수 있습니다. [페이지에 Dynamic Media 자산 추가](/help/assets/adding-dynamic-media-assets-to-pages.md)를 참조하십시오.

독립형 AEM Assets 고객의 경우 이 섹션에 설명된 대로 웹 사이트에 대화형 비디오를 수동으로 추가할 수 있습니다.

1. 게시된 대화형 비디오의 포함 코드 또는 URL을 복사합니다.
웹 페이지에 비디오 또는 이미지 뷰어 포함](/help/assets/embed-code.md)을 참조하십시오.
[
빠른 보기를 사용하여 상호 작용을 추가한 경우 포함 코드만 사용하십시오.하이퍼연결된 웹 페이지가 포함된 상호 작용을 추가한 경우 게시된 URL을 사용할 수도 있습니다. 그러나 대화형 컨텐츠에 상대 URL이 있는 링크, 특히 AEM Sites 페이지에 대한 링크가 있는 경우에는 URL 기반 연결 방법이 가능하지 않습니다.

1. 대상의 웹 페이지 코드에서 정적 비디오가 있는 위치를 식별합니다.
1. 정적 비디오를 제거하고 코드를 그대로 AEM Assets에서 복사한 포함 코드 또는 URL로 바꿉니다.
복사된 포함 코드는 응답형 환경에 대해 설정되므로 정적 비디오가 이전에 채운 영역에 자동으로 맞게 됩니다.

>[!NOTE]
따라서 하이퍼링크된 웹 페이지로만 상호 작용을 추가한 경우 됩니다.
그러나 빠른 보기를 트리거하기 위해 상호 작용을 추가한 경우 대화형 비디오에 인접한 축소판은 표시 목적으로만 사용됩니다.아직 기존 빠른 보기와 통합되지 않았습니다. 이러한 경우 이제 웹 사이트의 기존 빠른 보기와 대화형 비디오를 통합해야 합니다.

**예**

데모 웹 사이트 사용 예:

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html)

표준 비디오 포함 코드임을 알 수 있습니다.

```xml
<style type="text/css">
 #s7video_div.s7videoviewer{
   width:100%;
   height:auto;
 }
</style>

<script type="text/javascript" src="https://demos-pub.assetsadobe.com/etc/dam/viewers/s7viewers/html5/js/VideoViewer.js"></script>
<div id="s7video_div"></div>
<script type="text/javascript">
 var s7videoviewer = new s7viewers.VideoViewer({
  "containerId" : "s7video_div",
  "params" : {
   "serverurl" : "https://adobedemo62-h.assetsadobe.com/is/image",
   "contenturl" : "https://demos-pub.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Video",
   "config2": "/etc/dam/presets/analytics",
   "videoserverurl": "https://gateway-na.assetsadobe.com/DMGateway/public/demoCo",
   "posterimage": "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4",
   "asset" : "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4" }
 }).init();
</script>
```

통합은 비디오 포함 코드를 제거하고 AEM에서 대화형 비디오 포함 코드로 바꾸는 것만큼 간단합니다. 다음 URL에서 결과를 볼 수 있습니다. 페이지에 있는 대화형 비디오에 대한 표시이지만 아직 기존 빠른 보기에 통합되지 않았습니다.

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-1.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-1.html)

## 대화형 비디오와 기존 Quickview {#integrating-an-interactive-video-with-an-existing-quickview} 통합

>[!NOTE]
이 작업은 독립 실행형 AEM Assets 고객인 경우에만 적용됩니다.

이 프로세스의 마지막 단계는 대화형 비디오를 웹 사이트에서 사용되는 기존 Quickview 구현과 통합하는 것입니다. 모든 경우에 작동하는 통합에 대한 해결 방법이 없습니다. 모든 Quickview 구현은 고유합니다. 따라서 프런트 엔드 IT 담당자의 지원을 필요로 하는 구체적인 접근 방식이 필요합니다.

기존 Quickview 구현은 일반적으로 다음 순서로 웹 페이지에서 발생하는 관련 간 작업 체인을 나타냅니다.

1. 사용자가 웹 사이트의 사용자 인터페이스에서 요소를 트리거합니다.
1. 프런트 엔드 코드는 1단계에서 트리거된 사용자 인터페이스 요소를 기반으로 Quickview URL을 가져옵니다.
1. 프런트 엔드 코드는 2단계에서 얻은 URL을 사용하여 AJAX 요청을 보냅니다.
1. 백엔드 로직은 해당 Quickview 데이터 또는 컨텐츠를 다시 프런트 엔드 코드로 반환합니다.
1. 프런트 엔드 코드는 Quickview 데이터 또는 콘텐츠를 로드합니다.
1. 선택적으로, 프런트 엔드 코드는 로드된 Quickview 데이터를 HTML 표현으로 변환합니다.
1. 프런트 엔드 코드는 모달 대화 상자나 패널을 표시하고 최종 사용자를 위해 화면에 HTML 콘텐츠를 렌더링합니다.

이러한 호출은 임의의 단계에서 웹 페이지 로직에서 호출할 수 있는 독립 공용 API 호출을 나타내지 않을 수 있습니다. 대신, 이전 단계의 마지막 단계(콜백)에서 모든 다음 단계가 숨겨지는 체인 호출입니다.

동시에 대화형 비디오가 1단계와 2단계를 대체하며, 사용자가 대화형 비디오 내의 축소판을 클릭하면 이러한 사용자 상호 작용은 뷰어에 의해 처리됩니다. 뷰어는 이전에 AEM에 추가된 모든 축소판 데이터를 포함하는 웹 페이지에 이벤트를 반환합니다.

이러한 이벤트 처리기에서 프런트 엔드 코드는 다음을 수행합니다.

* 대화형 비디오에서 내보낸 이벤트를 수신합니다.
* 축소판 데이터를 기반으로 Quickview URL을 구성합니다.
* 백엔드에서 Quickview를 로드하고 표시하기 위해 화면에서 렌더링하는 프로세스를 트리거합니다.

또한 대화형 비디오 뷰어는 전체 화면 작업 모드를 지원합니다. 최종 사용자는 전체 화면을 종료하지 않고 축소판을 클릭하여 빠른 보기를 트리거합니다. 이 기능을 사용하려면 빠른 보기 모달 대화 상자가 뷰어의 컨테이너에 연결되도록 프런트 엔드 코드를 변경합니다. 뷰어가 전체 화면 모드에 있을 때 사용할 수 없는 문서 BODY 또는 기타 웹 페이지 요소를 추가하지 마십시오. 이 작업을 수행하는 코드는 뷰어가 페이지에 로드된 후 전송되는 하나 이상의 뷰어 콜백을 수신해야 합니다.

AEM에서 반환한 포함 코드에 이미 사용 가능한 이벤트 처리기가 있습니다. 강조 표시된 다음 코드 조각에 표시된 대로 주석 처리됩니다.

```xml
<style type="text/css">
 #s7interactivevideo_div.s7interactivevideoviewer{
   width:100%;
   height:auto;
 }
</style>
<script type="text/javascript" src="https://demos-pub.assetsadobe.com/etc/dam/viewers/s7viewers/html5/js/InteractiveVideoViewer.js"></script>

<div id="s7interactivevideo_div"></div>
<script type="text/javascript">
 var s7interactivevideoviewer = new s7viewers.InteractiveVideoViewer({
  "containerId" : "s7interactivevideo_div",
  "params" : {
   "serverurl" : "https://adobedemo62-h.assetsadobe.com/is/image",
   "contenturl" : "https://demos-pub.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Shoppable_Video_light",
   "config2": "/etc/dam/presets/analytics",
   "videoserverurl": "https://gateway-na.assetsadobe.com/DMGateway/public/demoCo",
   "interactivedata": "content/dam/_VTT/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4.svideo.vtt",
   "VideoPlayer.contenturl": "https://adobedemo62-h.assetsadobe.com/is/content",
   "asset" : "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4" }
 })
 /* // Example of interactive video event for quickview.
   s7interactivevideoviewer.setHandlers({
   "quickViewActivate": function(inData) {
     var sku=inData.sku; //SKU for product ID
    //To pass other parameter from the hotspot, you need to add custom parameter during the hotspot setup as parameterName=value
    loadQuickView(sku); //Replace this call with your quickview plugin
    //Please refer to your quickviewer plugin for the quickview call
    },
"initComplete":function() {
    //--- Attach quickview popup to viewer container so popup will work in fullscreen mode ---
    var popup = document.getElementById('quickview_div'); // get custom quickview container
    popup.parentNode.removeChild(popup); // remove it from current DOM
    var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
    var inner_container = document.getElementById(sdkContainerId);
    inner_container.appendChild(popup); //Attach custom quickview container to viewer
    }
   });
 */
 s7interactivevideoviewer.init();
</script>
```

따라서 위에 강조 표시된 코드 조각의 주석을 해제하고 더미 처리기 본문을 특정 웹 페이지에 해당하는 코드로 대체하기만 하면 됩니다.

표준 포함 코드에 있는 두 개의 기본 콜백 핸들러가 있습니다.`quickViewActivate` 및 `initComplete` `quickViewActivate` 처리기는 뷰어에서 축소판을 클릭하면 트리거됩니다. 이 플러그인을 사용하여 뷰어를 Quickview 활성화 논리와 통합합니다. `initComplete` 처리기는 뷰어가 페이지에 로드될 때 한 번만 트리거됩니다. 이 처리기는 웹 페이지 DOM에서 빠른 보기 대화 상자 위치를 조정하는 데 사용됩니다.

Quickview URL을 구성하는 프로세스는 이 항목의 앞부분에서 설명한 축소판 변수를 식별하는 프로세스와 반대됩니다. 이전에 식별한 Quickview URL 예를 사용하면 각 사례에 Quickview URL이 구성되는 방식을 확인할 수 있습니다.

<table>
  <tbody>
  <tr>
    <td><p>쿼리 문자열에 있는 단일 SKU</p> </td>
    <td><code class="code">s7interactivevideoviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/json?productId=" + inData.sku + "&amp;source=100";
      },
      });</code></td>
  </tr>
  <tr>
    <td>URL 경로에 있는 단일 SKU</td>
    <td><code class="code">s7interactivevideoviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/product/" + inData.sku;
      },
      });</code></td>
  </tr>
  <tr>
    <td><p>쿼리 문자열의 SKU 및 카테고리 ID</p> </td>
    <td><code class="code">s7interactivevideoviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/quickView/product/?category=" + inData.categoryId + "&amp;prodId=" + inData.sku;
      },
      });</code></td>
  </tr>
  </tbody>
</table>

Quickview URL을 트리거하고 Quickview 패널을 활성화하는 마지막 단계는 IT 부서의 프런트 엔드 IT 담당자의 지원이 필요할 수 있습니다. 이들은 사용 준비 중인 Quickview URL을 사용하여 적절한 단계에서 Quickview 구현을 정확하게 트리거하는 방법을 잘 알고 있습니다.

대화형 비디오를 Quickview 코드와 완전히 통합하기 위해 이러한 단계가 데모 웹 사이트에 적용되는 방법을 확인할 수 있습니다. 이 주제의 앞부분에서 Quickview URL의 구조는 다음과 같이 식별되었습니다.

```xml
/datafeed/$CategoryId$-$SKU$.json
```

다음과 같이 뷰어의 코드를 통해 처리기에 전달된 `inData` 개체에서 사용할 수 있는 `categoryId` 및 `sku` 필드를 사용하여 `quickViewActivate` 처리기 내에서 이 URL을 쉽게 재구성할 수 있습니다.

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

데모 웹 사이트에서 간단한 `loadQuickView()` 함수 호출을 사용하여 Quickview 대화 상자를 트리거합니다. 이 함수는 Quickview 데이터 URL인 인수를 하나만 사용합니다. 따라서 대화형 비디오를 통합하는 데 필요한 마지막 단계는 다음 코드 행을 `quickViewActivate` 처리기에 추가하는 것입니다.

```xml
loadQuickView(quickViewUrl);
```

마지막으로 Quickview 대화 상자가 뷰어의 컨테이너 요소에 연결되어 있는지 확인합니다. 기본 포함 코드는 이 기능을 수행하는 샘플 단계를 제공합니다. 뷰어의 컨테이너 요소에 대한 참조를 가져오려면 다음 코드 행을 사용할 수 있습니다.

```xml
var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
var inner_container = document.getElementById(sdkContainerId);
```

여기서 `inner_container`은 뷰어가 관리하는 `DIV` 요소에 대한 참조입니다. 대화 상자를 `DIV`의 자식으로 지정할 수 있습니다.

모달 대화 상자 요소를 실제로 찾아 위의 컨테이너에 연결하는 단계는 경우에 따라 다릅니다. 필요한 Quickview 구현에 익숙한 프런트 엔드 개발자의 도움을 받을 수 있습니다.

샘플 웹 사이트의 경우, Quickview 모달 대화 상자는 문서 `BODY`에 바로 연결된 `DIV`으로 구현됩니다. 따라서 이 대화 상자를 뷰어의 컨테이너로 이동할 코드는 다음과 같이 간단합니다.

```xml
var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
var inner_container = document.getElementById(sdkContainerId);
inner_container.appendChild(document.getElementById("quickview-modal"));
```

전체 소스 코드는 다음과 같습니다.

```xml
<style type="text/css">
 #s7interactivevideo_div.s7interactivevideoviewer{
   width:100%;
   height:auto;
 }
</style>
<script type="text/javascript" src="https://demos-pub.assetsadobe.com/etc/dam/viewers/s7viewers/html5/js/InteractiveVideoViewer.js"></script>

<div id="s7interactivevideo_div"></div>
<script type="text/javascript">
 var s7interactivevideoviewer = new s7viewers.InteractiveVideoViewer({
  "containerId" : "s7interactivevideo_div",
  "params" : {
   "serverurl" : "https://adobedemo62-h.assetsadobe.com/is/image",
   "contenturl" : "https://demos-pub.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Shoppable_Video_light",
   "videoserverurl": "https://gateway-na.assetsadobe.com/DMGateway/public/demoCo",
   "interactivedata": "content/dam/_VTT/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4.svideo.vtt",
   "VideoPlayer.contenturl": "https://adobedemo62-h.assetsadobe.com/is/content",
   "asset" : "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4" }
 })
 // Example of interactive video event for quickview.
   s7interactivevideoviewer.setHandlers({
   "quickViewActivate": function(inData) {
     var sku=inData.sku; //SKU for product ID
     var categoryId=inData.categoryId; //categoryId
    var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
    loadQuickView(quickViewUrl);
    },
   "initComplete":function() {
    //--- Attach quickview popup to viewer container so popup will work in fullscreen mode ---
    var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
    var inner_container = document.getElementById(sdkContainerId);
    inner_container.appendChild(document.getElementById("quickview-modal"));
    }
   });
 s7interactivevideoviewer.init();
</script>
```

완전히 통합된 대화형 비디오를 사용하는 최종 데모 웹 사이트는 다음과 같습니다.

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-3.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-3.html)

## 빠른 보기를 사용하여 사용자 지정 팝업 만들기 {#using-quickviews-to-create-custom-pop-ups}

[빠른 보기를 사용하여 사용자 지정 팝업 만들기](/help/assets/custom-pop-ups.md)를 참조하십시오.
