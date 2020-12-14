---
title: 대화형 비디오
description: Dynamic Media에서 인터랙티브한 비디오 및 쇼퍼블 비디오를 사용하여 작업하는 방법 살펴보기
uuid: c3ff6839-fff5-4709-8163-5c4245b80e6d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 04be55f2-c7d8-45ef-89e5-58856b971de5
docset: aem65
translation-type: tm+mt
source-git-commit: ce43c49f8f7d4509e414554b8f4eba368ff66e95
workflow-type: tm+mt
source-wordcount: '6056'
ht-degree: 0%

---


# 대화형 비디오{#interactive-videos}

비디오에서 바로 전환율을 높일 수 있는 쇼퍼블 비디오로 인식되는 인터랙티브한 비디오를 손쉽게 제작할 수 있습니다. 비디오에 포함된 요소를 기반으로 관련 서비스, 정보 또는 제품 축소판을 나란히 열어 볼 수 있는 비디오 플레이어와 함께 패널에서 고객의 참여를 유도할 수 있습니다. 고객은 축소판을 눌러 서비스에 바로 연결하거나 장바구니에 항목을 추가하여 즉시 구매하거나 웹 페이지에 연결하여 자세한 내용을 확인할 수 있습니다.

비디오가 끝나면 클릭유도하기 위해 모든 오퍼에 대한 시각적 요약이 표시됩니다. 고객은 원하는 항목을 이용할 수 있는 다른 기회를 얻을 수 있습니다. 고객의 참여도와 전환율을 높이는 실행 가능하고 특정 경험을 제공합니다.

[대화형 이미지](/help/assets/interactive-images.md)도 참조하십시오.

## 대화형 비디오 실행 중 {#interactive-video-in-action}

인터랙티브한 쇼퍼블 비디오를 직접 보려면 [라이브 데모](https://landing.adobe.com/en/na/dynamic-media/ctir-2755/live-demos.html)를 클릭하고 페이지에서 **[!UICONTROL 쇼퍼블 미디어]** 제목으로 스크롤한 다음 쇼퍼블 비디오를 클릭합니다.

* 재생하는 동안 제품이 비디오에 사용되므로 동일한 제품이 축소판 이미지로 오른쪽에 나타납니다.

* 축소판을 클릭하여 비디오를 일시 중지하고 제품의 빠른 보기를 엽니다. 예를 들어 비디오에서 KitchenAid 축소판 이미지를 클릭하여 믹서의 360도 회전 보기를 경험하거나 확대하면서 믹서의 세부 사항을 확인할 수 있습니다.

<!-- There was a link here that showed the video frame of an interactive video and when the reader clicked the frame the video would play https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/AXIS/index.html. This now needs to call a new interactive video-->

![인터랙티브한 쇼퍼블 비디오에서 얻은 프레임](assets/chlimage_1-126.png) *인터랙티브한 쇼퍼블 비디오에서 촬영한 비디오 프레임.*

>[!NOTE]
>
>사용자가 축소판 이미지를 클릭할 때 웹 페이지를 시작할 대화형 비디오를 만드는 경우 일부 장치에서는 팝업 웹 페이지가 열리지 않습니다. 이러한 경우 장치에서 팝업 차단기 설정을 변경해야 합니다. 예를 들어 Apple iPhone 6의 경우 **[!UICONTROL 설정]** > **Safari** > **팝업 차단**&#x200B;을 누른 다음 해당 컨트롤을 **[!UICONTROL 오프]**&#x200B;로 밀십시오. 이제 대화형 비디오를 재생하고 축소판을 클릭하면 팝업을 열 것인지 묻는 메시지가 표시됩니다. 승인하면 웹 페이지가 열립니다.

### 대화형 비디오를 만드는 방법 보기 {#watch-how-interactive-videos-are-created}

[대화형 비디오를 만드는 방법에 대한 7분 30초 연습](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveVideo) [](https://outv.omniture.com?v=s4NHQ2dzqd7hIqWjeG2sIdyNWsTWyupA)을 보십시오.
(비디오 연습은 Assets on Demand로 브랜딩되지만 원칙과 단계는 AEM Assets의 대화형 비디오에 계속 적용됩니다.)

### Adobe 고객 성공 웨비나 {#adobe-customer-success-webinar}

&quot;AEM Assets에서 대화형 비디오 사용, 링크 공유 및 YouTube 공유&quot; 웨비나에서는 대화형 비디오 및 기타 기능을 사용하여 전환 기반 이벤트를 비디오 마케팅 컨텐츠에 연결하는 방법을 설명합니다.

>[!NOTE]
[AEM Assets에서 대화형 비디오, 링크 공유 및 YouTube 공유 사용](https://adobecustomersuccess.adobeconnect.com/p1yxzdo4aec/).

## 빠른 시작:대화형 비디오 {#quick-start-interactive-videos}

다음 단계별 워크플로우 설명은 Dynamic Media에서 인터랙티브한 비디오를 빠르게 시작하고 실행하는 데 도움이 되도록 설계되었습니다.

빠른 시작 작업 중 일부 내에서 **Example** 머리글을 찾습니다. 여기에는 *이(가) 아직 여기에 인터랙티브한 요소를 추가하지 않은 이 시작 데모 웹 페이지를 기반으로 하는 간단한 자습서가 포함되어 있습니다.*

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html)

자신의 웹 사이트에서 대화형 비디오를 통합하는 단계를 보여주는 **Examples** 도움말입니다.

마지막 예제 섹션에서 튜토리얼을 완료하면 완전히 통합된 대화형 비디오가 포함된 최종 데모 웹 페이지는 다음과 같이 표시됩니다.

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-3.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-3.html)

인터랙티브한 비디오 단계:

1. **(선택 사항) Quickview 변수**  식별 - 기존 Quickview 구현에서 사용하는 동적 변수를 식별하여 시작합니다. 대화형 비디오를 만들 때 변수를 사용하여 제품 축소판을 해당 제품 Quickview에 매핑합니다. [(선택 사항) Quickview 변수 확인](#optional-identifying-quickview-variables)을 참조하십시오.
   *이 단계는 다음 내용이 모두 참인 경우에만 필요합니다*.・ 빠른 보기를 트리거하여 비디오에 인터랙티브한 요소를 추가하려고 합니다.
・ AEM 구현은 IBM Websphere Commerce, Elastic Path, hybris 또는 Intershop과 같은 모든 eCommerce 솔루션에서 제품 데이터를 AEM으로 가져오는 데 eCommerce 통합 프레임워크를 사용하지 *않습니다.* AEM Assets](/help/sites-administering/concepts.md)의 [eCommerce 개념을 참조하십시오.

1. **(선택 사항) 대화형 비디오 뷰어 사전**  설정 만들기 - 비디오 스크러버 및 대화형 축소판과 같은 플레이어를 구성하는 다양한 구성 요소의 모양과 동작을 사용자 정의합니다.
바로 사용 가능한 대화형 비디오 뷰어 사전 설정 `Shoppable_Video_Light` 또는 `Shoppable_Video_Dark`을 대신 사용하려는 경우에는 자신의 대화형 비디오 뷰어 사전 설정을 만들 필요가 없습니다.
[새 뷰어 사전 설정 만들기](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset)(선택 사항) 및 [대화형 뷰어 사전 설정 만들기 위한 특수 고려 사항](/help/assets/managing-viewer-presets.md#special-considerations-for-creating-an-interactive-viewer-preset)을 참조하십시오.

1. **비디오 및 관련 이미지 자산**  업로드 - 대화형으로 만들 비디오 및 관련 이미지를 업로드합니다.
[비디오 및 관련 축소판 에셋 업로드](#uploading-a-video-and-its-associated-thumbnail-assets)를 참조하십시오.

1. **비디오에**  인터랙티브한 요소 추가 - 비디오에 하나 이상의 시간 세그먼트를 추가합니다. 그런 다음 해당 시간 세그먼트 내에 이미지 축소판을 연결합니다. 하이퍼링크, 빠른 보기 또는 경험 조각과 같은 작업에 각 이미지 축소판을 할당합니다.
(인터랙티브 컨텐츠에 상대 URL, 특히 AEM Sites 페이지로 연결되는 링크가 있는 경우에는 URL 기반 연결 방법을 사용할 수 없습니다.)
대화형 비디오 에셋을 게시하여 마칩니다. 게시를 사용하면 나중에 복사하고 웹 사이트 랜딩 페이지에 적용할 포함 코드나 URL이 만들어집니다. 비디오[대화형 작업 추가를 참조하십시오.
](#adding-interactivity-to-your-video)
[자산 게시](/help/assets/publishing-dynamicmedia-assets.md)를 참조하십시오.

1. **AEM Sites, AEM eCommerce 또는**
두 가지 모두를 사용하는 경우, AEMI의 웹 사이트 또는 웹 사이트에 대화형 비디오를 추가하거나, 대화형 미디어 구성 요소를 페이지로 드래그하여 AEM의 웹 페이지에 직접 대화형 비디오를 추가할 수 있습니다. [페이지에 Dynamic Media 자산 추가를 참조하십시오.](/help/assets/adding-dynamic-media-assets-to-pages.md)
임베드 코드 또는 URL을 사용하여 인터랙티브한 비디오를 웹 사이트 경험과 통합할 수 있습니다. [웹 사이트](#integrating-an-interactive-video-with-your-website)와 대화형 비디오 통합을 참조하십시오.
제3자 WCM(Web Content Manager)을 사용하는 경우 새 대화형 비디오를 웹 사이트에서 사용되는 기존 Quickview 구현과 통합해야 합니다. [기존 Quickview](#integrating-an-interactive-video-with-an-existing-quickview)와 대화형 비디오 통합을 참조하십시오.
   [페이지에 Dynamic Media 자산 추가](/help/assets/adding-dynamic-media-assets-to-pages.md)

## (선택 사항) Quickview 변수 {#optional-identifying-quickview-variables} 확인

>[!NOTE]
이 작업은 다음 내용이 참인 경우에만 필요합니다.
* Quickviews에 트리거하여 비디오에 인터랙티브한 요소를 추가하려고 합니다.
* AEM 구현은 IBM Websphere Commerce, Elastic Path, hybris 또는 Intershop과 같은 모든 eCommerce 솔루션에서 제품 데이터를 AEM으로 가져오는 데 eCommerce 통합 프레임워크를 사용하지 *않습니다.* AEM Assets](/help/sites-administering/concepts.md)의 [eCommerce 개념을 참조하십시오.

AEM 구현에서 eCommerce를 사용하는 경우 이 작업을 건너뛰고 다음 작업으로 진행할 수 있습니다.

인터랙티브한 비디오 작성 프로세스 동안 제품 축소판을 해당 제품 Quickview에 매핑할 수 있도록 기존 Quickview 구현에서 사용하는 동적 변수를 식별함으로써 시작합니다.

시간 세그먼트를 비디오에 추가하면 SKU와 세그먼트에 추가하는 각 축소판에 추가 변수를 할당합니다. 이러한 변수는 나중에 적절한 Quickview 제품을 표시하는 데 사용됩니다.

제품 Quickview를 고유하게 트리거하는 데 필요한 변수를 올바르게 식별해야 합니다.

기존 Quickview 구현을 담당하는 IT 전문가와 상담하는 데 충분할 수 있습니다. 시스템에서 빠른 보기를 식별하는 데 필요한 최소 데이터 세트를 알 수 있습니다. 그러나 대부분의 경우 프런트 엔드 코드의 기존 동작을 간단하게 분석할 수도 있습니다.

대부분의 Quickview 구현은 다음 패러다임을 사용합니다.

* 사용자는 웹 사이트에서 사용자 인터페이스 요소를 활성화합니다. 예를 들어 &quot;빠른 보기&quot; 단추를 클릭합니다.
* 필요한 경우 이 웹 사이트에서 Quickview 데이터 또는 컨텐츠를 로드하기 위해 Ajax 요청을 백엔드로 보냅니다.
* Quickview 데이터는 웹 페이지에서 렌더링할 준비를 위해 컨텐츠로 변환됩니다.
* 마지막으로 프런트 엔드 코드는 이러한 컨텐츠를 화면에 시각적으로 렌더링합니다.

따라서 이 방법은 Quickview가 구현된 기존 웹 사이트의 여러 영역을 방문하고, Quickview를 트리거하고, Quickview 데이터 또는 컨텐츠를 로드하기 위해 웹 페이지에서 보낸 Ajax URL을 캡처하는 것입니다.

일반적으로 전문적인 디버깅 도구를 사용할 필요가 없습니다. 최신 웹 브라우저는 적절한 작업을 수행하는 웹 관리자를 제공합니다. 다음은 웹 관리자를 포함하는 웹 브라우저의 몇 가지 예입니다.

* Google Chrome에서 나가는 HTTP 요청을 모두 보려면 **F12**(Windows) 또는 **Command+Options+I**(Mac)을 눌러 개발자 도구 패널을 연 다음 **네트워크** 탭을 클릭합니다.

* Firefox에서는 **F12**(Windows) 또는 **Command+Option+I**(Mac)를 눌러 Firebug 플러그인을 활성화하고 **`[Net]`** 탭을 사용하거나 내장된 검사기 도구 및 해당 네트워크 탭을 사용할 수 있습니다.

* Internet Explorer에서 **F12**&#x200B;를 눌러 디버거 도구를 활성화합니다.

브라우저에서 네트워크 모니터링이 켜져 있으면 페이지의 빠른 보기를 트리거합니다.

이제 네트워크 로그에서 Quickview Ajax URL을 찾아 기록된 URL을 복사하여 향후 분석을 수행할 수 있습니다. Quickview를 트리거하는 대부분의 경우 서버로 전송되는 요청이 많습니다. 일반적으로 Quickview Ajax URL은 목록에서 첫 번째 URL 중 하나입니다. 복잡한 쿼리 문자열 부분이나 경로가 있으며 응답 MIME 유형은 `text/html`, `text/xml` 또는 `text/javascript`입니다.

이 프로세스 중에 제품 카테고리 및 유형이 다른 웹 사이트의 여러 영역을 방문하는 것이 중요합니다. 이유는 Quickview URL에 특정 웹 사이트 카테고리에 공통인 부분이 있을 수 있지만 웹 사이트의 다른 영역을 방문하는 경우에만 변경될 수 있기 때문입니다.

가장 간단한 경우 Quickview URL에서 변수 부분만 제품 SKU입니다. 이 경우 제품 SKU 값은 AEM의 대화형 비디오에서 시간 세그먼트에 축소판을 추가하는 데 필요한 유일한 데이터 조각입니다.

그러나 복잡한 경우 Quickview URL에는 카테고리 ID, 색상 코드 등 제품 SKU 외에도 다양한 요소가 있습니다. 이 경우 이러한 모든 요소는 AEM의 축소판 데이터 정의에 별도의 변수가 됩니다.

Quickview URL 및 결과 축소판 변수의 다음 예를 생각해 보십시오.

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
    </ul> <p>URL에 있는 유일한 변수 부분은 <code>productId=</code> 쿼리 문자열 매개 변수의 값이며 SKU 값입니다. 따라서 축소판에서는 <strong><code>866558</code></strong>, <strong><code>1196184</code></strong>, <strong><code>1081492</code></strong>, <strong><code>1898294</code></strong> 등의 값으로 채워진 SKU 필드만 필요합니다.</p> </td>
  </tr>
  <tr>
    <td><p>URL 경로에 있는 단일 SKU입니다.</p> </td>
    <td><p>기록된 Quickview URL에는 다음이 포함됩니다.</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>변수 부분은 경로의 마지막 부분에 있으며 AEM 축소판의 SKU 값이 됩니다.<strong><code>6422350843</code></strong>, <strong><code>1607745002</code></strong>, <strong><code>0086724882</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>쿼리 문자열에서 SKU 및 카테고리 ID.</p> </td>
    <td><p>기록된 Quickview URL에는 다음이 포함됩니다.</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>이 경우 URL에는 2개의 다양한 부분이 있습니다. SKU는 <code>prodId</code> 매개 변수에 저장되고 카테고리 ID는 <code>category=</code> 매개 변수에 저장됩니다.</p> <p>이와 같이 축소판 정의는 쌍입니다. 즉, SKU 값과 <code>categoryId</code>이라는 추가 변수입니다. 결과 쌍은 다음과 같습니다.</p>
    <ul>
      <li>SKU는 <code>305466</code>이고 <code>categoryId</code>는 <code>1100004</code></li>
      <li>SKU는 <code>310181</code>이고 <code>categoryId</code>는 <code>1100004</code></li>
      <li>SKU는 <code>308706</code>이고 <code>categoryId</code>는 <code>1740148</code></li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**예**

위의 접근 방식이 Example 웹 사이트에 적용되면 각각 &quot;SEE MORE&quot; 버튼이 있는 여러 개의 제품 축소판이 포함된 웹 페이지가 나타납니다.

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html)

페이지에서 사용 가능한 모든 제품 빠른 보기를 활성화하면 백 엔드에 대한 다음 빠른 보기 요청 목록을 볼 수 있습니다.

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

이러한 서버 호출을 보면 제품 특정 정보가 요청 경로에만 있음을 알 수 있습니다. 또한 쿼리 문자열이 전혀 사용되지 않으며 두 가지 유형의 데이터 요소가 관련되어 있습니다.

* 첫 번째 유형은 초, 쿠션, 가구 그리고 유리 제품이다. 이를 &quot;제품 카테고리&quot;라고 할 수 있습니다.
* 두 번째 유형은 제품 코드(예: 233916597)입니다. &quot;제품 SKU&quot;라고 가정할 수 있습니다.

이 정보가 주어지면 전체 Quickview URL에는 다음 패턴이 있습니다.

`/datafeed/$categoryId$-$SKU$.json`

이러한 분석을 바탕으로 축소판에 대해 다음 두 가지 변수를 사용할 수 있다고 결론을 내리게 됩니다.`categoryId` 및 `SKU`.

이제 비디오 및 관련 축소판 에셋을 업로드할 준비가 되었습니다.

## (선택 사항) 대화형 비디오 뷰어 사전 설정 만들기 {#optional-creating-an-interactive-video-viewer-preset}

기본 즉시 사용 가능한 대화형 비디오 뷰어 사전 설정 유형 `Shoppable_Video_dark` 또는 `Shoppable_Video_light` 중 하나를 사용하려는 경우 이 작업을 건너뛰고 다음 작업을 계속할 수 있습니다.

작성 환경에서 축소판을 클릭하면 [빠른 보기] 대화 상자의 미리 보기가 나타납니다.

![chlimage_1-21](assets/chlimage_1-127.png)

선택적으로 나만의 사용자 정의 대화형 비디오 뷰어 사전 설정을 만들 수 있습니다. 비디오 플레이어의 스타일, 인터랙티브한 축소판 및 비디오 끝에 표시되는 축소판 격자 보기를 결정할 수 있습니다.

대화형 비디오 뷰어 사전 설정은 추가한 비디오 및 모든 타임라인 세그먼트를 올바르게 렌더링합니다. 미리 보기 모드에서 제품 축소판을 클릭할 때 기본 Quickview 예도 사용하므로 게시하기 전에 인터랙티브한 요소를 테스트할 수 있습니다.

뷰어 사전 설정을 저장하면 [뷰어 사전 설정] 페이지에서 상태**On **이 자동으로 설정됩니다. 이 상태는 Dynamic Media 구성 요소에서 볼 수 있고 이 구성 요소와 함께 비디오를 미리 볼 때마다 표시됩니다. 새 뷰어 사전 설정을 수동으로 게시해야 합니다.

자신의 대화형 비디오 뷰어 사전 설정을 만들려면 [새 뷰어 사전 설정 만들기](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset)를 참조하십시오.

## 비디오 및 관련 축소판 에셋 {#uploading-a-video-and-its-associated-thumbnail-assets} 업로드

비디오 및 축소판 에셋을 이미 업로드한 경우 [비디오에 상호 작용 추가](#adding-interactivity-to-your-video)로 진행합니다.

잘못된 비디오 또는 이미지를 업로드하거나 업로드된 비디오나 더 이상 필요하지 않은 이미지를 삭제하려는 경우 [자산 삭제](/help/assets/manage-assets.md#deleting-assets)를 참조하십시오.

비디오 및 관련 축소판 에셋을 업로드하려면:

1. 비디오 및 관련 축소판 에셋을 원하는 폴더 또는 폴더에 업로드합니다.

   [자산 업로드](/help/assets/manage-assets.md)를 참조하십시오.
[FTP 작업 예약을 사용하여 자산 업로드](/help/assets/manage-assets.md)를 참조하십시오.

   이제 비디오에 인터랙티브한 요소를 추가할 수 있습니다.

## 비디오 {#adding-interactivity-to-your-video}에 인터랙티브한 요소 추가

[대화형 비디오 만들기] 페이지의 즉석 시각 편집기를 사용하여 타임라인 세그먼트를 비디오에 추가합니다.

타임라인 세그먼트를 추가하면 각 세그먼트 내에 축소판 이미지를 추가할 수 있습니다. 추가하는 각 축소판에 대해 작업을 적용합니다. 예를 들어 축소판에 빠른 보기를 적용하거나, 해당 축소판에 하이퍼링크를 지정하거나 경험 조각을 지정할 수 있습니다.

[경험 조각](/help/sites-authoring/experience-fragments.md)을 참조하십시오.

>[!NOTE]
경험 조각에 뷰어를 포함할 때는 대화형 비디오의 소셜 미디어 공유 도구가 지원되지 않습니다. 이 문제를 해결하려면 소셜 미디어 공유 도구가 없는 뷰어 사전 설정을 사용하거나 만들 수 있습니다. 이러한 뷰어 사전 설정을 사용하여 경험 조각에 성공적으로 포함할 수 있습니다.

>[!NOTE]
인터랙티브한 컨텐츠에 상대 URL, 특히 AEM Sites 페이지로 연결되는 링크가 있는 경우에는 URL 기반 연결 방법을 사용할 수 없습니다.

현재 작성/편집 세션 동안 페이지의 오른쪽 위 모서리 근처에 있는 실행 취소 및 재실행 옵션이 지원됩니다.

대화형 비디오를 저장하면 비디오가 미리 보기로 즉시 열립니다. 이 비디오에서는 대화형 비디오 뷰어 사전 설정을 선택하고 재생할 수 있어 고객에게 표시되는 모양을 대략적으로 확인할 수 있습니다.

비디오에 인터랙티브한 기능을 추가하려면:

1. 자산 보기에서 업로드한 비디오로 이동하여 대화형으로 만들 비디오로 이동합니다.
1. 다음 중 하나를 수행하십시오.

   * 이미지를 마우스로 가리킨 다음 **[!UICONTROL Select]** (확인 표시 아이콘)을 누릅니다. 도구 모음에서 **[!UICONTROL 편집을 누릅니다.]**

   * 이미지를 가리킨 다음 **[!UICONTROL 추가 작업]**(세 개의 점 아이콘) **[!UICONTROL 편집을 누릅니다.]**

   * 이미지를 눌러 [세부 사항 보기] 페이지에서 엽니다. 도구 모음에서 **[!UICONTROL 편집을 누릅니다.]**

1. [대화형 비디오 만들기] 페이지에서 다음 중 하나를 수행합니다.

   * **[!UICONTROL 재생]** 단추를 눌러 비디오 재생을 시작합니다. 강조 표시할 특정 제품, 서비스 또는 세부 사항이 표시되면 도구 모음에서 **[!UICONTROL 세그먼트 추가]**&#x200B;를 누릅니다. 비디오 끝까지 반복합니다.

      추가하는 각 세그먼트에 대해 하나 이상의 축소판 이미지를 해당 축소판 이미지에 지정한 다음 해당 축소판을 Quickview 제품 페이지에 연결하여 고객이 구매하거나 웹 페이지에 자세한 내용을 볼 수 있습니다.

   * **[!UICONTROL 재생]** 단추를 눌러 비디오 재생을 시작합니다. 강조 표시할 특정 제품, 서비스 또는 세부 사항이 표시되면 **[!UICONTROL 일시 중지를 누릅니다.]** 세그먼트  **[!UICONTROL 추가를 누릅니다.]**

      비디오 끝에 도달할 때까지 세그먼트를 추가하려는 타임라인의 지점에서 비디오를 계속 재생하고 일시 정지합니다.

1. (선택 사항) **[!UICONTROL 타임라인 비율 슬라이더]** 왼쪽에 있는 막대를 드래그하여 확대 또는 축소하여 추가한 세그먼트의 세부 사항 정도를 제어할 수 있습니다.

   ![chlimage_1-22](assets/chlimage_1-128.png)

   비디오 길이에 따라 세그먼트 지속 시간은 기본적으로 다음 값으로 설정됩니다.

   <table>
      <tbody>
        <tr>
        <td><strong>비디오 길이가</strong></td>
        <td><strong>세그먼트 지속 시간 설정은 기본적으로..</strong></td>
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

   비디오 타임라인에서는 사용 가능한 화면만큼 많은 화면 공간을 사용합니다. 이와 같이 브라우저 크기를 조정할 때 추가한 세그먼트는 정확한 폭을 유지합니다.

   예감 하기 위해 다음 3개의 스크린샷이 동일한 비디오를 사용하고 있습니다. 각 세그먼트의 너비는 [타임라인 비율] 설정에 따라 달라집니다.

   ![chlimage_1-23](assets/chlimage_1-129.png)

   스크린샷 A

   위의 스크린샷 A는 29번째 제품 비디오의 기본 보기를 보여줍니다. 타임라인 비율은 기본적으로 5초로 설정됩니다.

   ![chlimage_1-130](assets/chlimage_1-130.png)

   스크린샷 B

   위의 스크린샷 B에서 타임라인 비율 슬라이더는 기본값인 5초에서 3초로 끌렸습니다. 개별 타임라인 크기 조절 타임스탬프가 이제 3초 간격으로 모두 설정됩니다.

   ![chlimage_1-25](assets/chlimage_1-131.png)

   스크린샷 C

   위의 스크린샷 C에서 타임라인 비율 설정이 8초로 이동되었습니다. 제품 축소판이 포함된 세그먼트가 어떻게 축소되었는지 확인합니다. 이 방식으로 축소하는 것은 긴 비디오가 있고 페이지의 너비에 일반적으로 맞는 더 많은 세그먼트의 개요를 보려는 경우에 유용합니다.

1. (선택 사항) 다음 중 하나를 수행합니다.

   * 세그먼트의 시작 시간과 종료 시간을 조정하려면

      세그먼트를 선택한 다음 앞쪽 또는 뒤쪽 파란색 타원을 드래그하여 각각 시작 또는 종료 시간을 조정합니다. 표시된 비디오 프레임은 조정을 기반으로 비디오의 해당 시간으로 이동합니다. 타임라인 세그먼트의 이동은 타임라인에서 인접한 세그먼트를 기준으로 제한됩니다. 허용되는 최소 세그먼트 시간은 1초입니다.

      다음 탐색 단축키를 사용하여 비디오 세그먼트를 신속하게 확인하고 세밀하게 조정할 수 있습니다.

      * 맨 앞에 있는 파란색 타원을 눌러 해당 세그먼트의 시작 부분으로 바로 비디오를 이동합니다.
      * 후행 파란색 타원을 눌러 해당 세그먼트 끝으로 바로 비디오를 찾습니다.
      * 세그먼트 전체를 탭하여 비디오 재생을 해당 세그먼트의 시작으로 되돌립니다.

   ![chlimage_1-26](assets/chlimage_1-132.png)

   타임라인 세그먼트의 끝 위치 변경

   * 세그먼트를 삭제하려면

      타임라인에 있는 마지막 세그먼트를 선택한 다음 도구 모음에서 **[!UICONTROL 세그먼트 삭제를 누릅니다.]** 두 개 이상의 세그먼트를 선택하면 세그먼트 삭제 기능이 비활성화됩니다.

      마지막 세그먼트만 삭제할 수 있습니다. 예를 들어 타임라인의 모든 세그먼트를 삭제하려면 항상 마지막 세그먼트를 선택한 다음 **[!UICONTROL 세그먼트 삭제를 탭해야 합니다.]**


1. 하나 이상의 축소판 이미지를 연결할 시간 세그먼트를 선택합니다.
1. 비디오 오른쪽의 **[!UICONTROL 컨텐트]** 탭을 누릅니다.
1. 콘텐츠 탭에서 **[!UICONTROL 자산 선택]**&#x200B;을 누른 다음 비디오에 사용할 이미지 자산을 모두 찾아 선택합니다. 선택한 에셋이 콘텐츠 탭의 자산 선택기 패널에 추가됩니다.

1. 콘텐츠 탭 아래의 자산 선택기에서 다음 중 하나를 수행합니다.

   <table>
      <tbody>
        <tr>
        <td>축소판을 선택한 타임라인 세그먼트에 연결하려면</td>
        <td><p>오른쪽의 자산 선택기 패널에서 이미지를 누릅니다.</p> <p>타임라인 세그먼트에 원하는 만큼 축소판을 추가할 수 있습니다. 선택하는 각 이미지에 대해 자산 선택기의 이미지 위에 확인 표시가 나타납니다.</p> </td>
        </tr>
        <tr>
        <td>선택한 타임라인 세그먼트에서 축소판을 제거하려면</td>
        <td><p>다음 중 하나를 수행합니다.</p>
          <ul>
          <li>자산 선택기 패널에서 확인 표시가 있는 이미지를 눌러 선택 해제합니다. 이미지 자산이 타임라인 세그먼트에서 제거됩니다.<br /> </li>
          <li>선택한 타임라인 세그먼트에서 이미지를 누른 다음 도구 모음에서 <strong>제품 삭제</strong>를 누릅니다.</li>
          </ul> </td>
        </tr>
      </tbody>
    </table>

   ![자산 선택기](assets/chlimage_1-133.png)

   자산 선택기 패널에서 이미지를 누르면 선택한 타임라인 세그먼트에 이미지가 추가됩니다.

1. 타임라인 세그먼트 중 하나에서 단일 축소판 이미지를 선택한 다음 **[!UICONTROL 작업]** 탭을 누릅니다.
1. 다음 중 하나를 수행합니다.
   <table> 
    <tbody> 
      <tr> 
      <td>선택한 축소판 이미지를 빠른 보기에 연결하려면</td> 
      <td><p>작업 유형 아래에서 <strong>빠른 보기</strong>를 탭합니다.</p> <p>AEM Sites 및 Ecommerce 고객인 경우:</p> 
       <ul> 
       <li>SKU 값 텍스트 필드는 제공하는 각 고유 제품 또는 서비스에 대한 고유 식별자인 선택한 제품의 SKU(Stock Keeping Unit)로 미리 채워집니다. 이미지가 AEM Commerce의 제품과 연결되면 자동으로 채워집니다.</li> 
       <li>미리 채워진 SKU가 잘못된 경우 제품 선택기 아이콘(확대경)을 탭하거나 클릭하여 제품 선택 페이지를 엽니다. 사용할 제품을 탭하거나 클릭한 다음, 페이지의 오른쪽 상단에 있는 확인 표시를 눌러 대화형 비디오 편집기로 돌아갑니다.</li> 
       </ul> <p> AEM Sites 또는 Ecommerce 고객이 아닌 <em>인 경우</em></p> 
       <ul> 
       <li><a href="/help/assets/carousel-banners.md#identifying-hotspot-and-image-map-variables">핫스팟 변수 확인</a>을 참조하십시오. 이러한 변수를 정의해야 합니다. </li> 
       <li>기본적으로 이 SKU 필드는 확장자 없이 이미지 자산의 파일 이름을 사용합니다. SKU를 기반으로 파일에 대한 표준 이름 지정 규칙을 따르는 경우 일반적으로 추가적인 편집 작업이 필요하지 않습니다. </li> 
       <li>그렇지 않은 경우 기본값을 편집하고 올바른 SKU 값을 입력합니다. SKU 값 텍스트 필드에 제공하는 각 고유 제품 또는 서비스에 대한 고유 식별자인 제품의 SKU(Stock Keeping Unit)를 입력합니다. 입력한 SKU 값은 시스템이 탭한 이미지를 특정 SKU의 Quickview와 연결하도록 Quickview 템플릿의 변수 부분을 자동으로 채웁니다.</li> 
       </ul> <p>(선택 사항) 제품을 추가로 식별하기 위해 사용해야 하는 다른 변수가 Quickview 내에 있으면 <strong>범용 변수 추가</strong>를 탭합니다. 텍스트 필드에서 추가 변수를 지정합니다. 예를 들어 <code>category=Womens</code>은(는) 추가된 변수입니다.</p> <p> </p> </td> 
      </tr> 
      <tr> 
      <td>선택한 축소판 이미지를 하이퍼링크와 연결하려면</td> 
      <td><p>작업 유형에서 <strong>하이퍼링크</strong>를 누른 다음 다음 중 하나를 수행합니다.</p> 
       <ul> 
       <li>AEM Sites 고객인 경우 사이트 선택기 아이콘(폴더)을 탭하여 웹 페이지로 이동합니다. 인터랙티브한 컨텐츠에 상대 URL, 특히 AEM Sites 페이지로 연결되는 링크가 있는 경우에는 URL 기반 링크 연결 방법을 사용할 수 없습니다.</li> 
       <li>독립형 Dynamic Media 고객인 경우, HREF 텍스트 필드에 연결된 웹 페이지의 전체 URL 경로를 지정합니다.</li> 
       </ul> <p>링크를 새 브라우저 탭에서 열지 또는 현재 탭에서 열지를 지정해야 합니다.</p> </td> 
      </tr> 
      <tr> 
      <td>선택한 축소판 이미지를 경험 조각과 연결하려면</td> 
      <td><p>작업 유형에서 <strong>경험 조각</strong>을 탭한 다음 다음을 수행합니다.<p> 
       <ul> 
       <li>AEM Sites 고객인 경우 검색 아이콘(확대경)을 탭하거나 클릭하여 경험 조각 페이지를 엽니다. 사용할 경험 조각을 탭하거나 클릭한 다음, 페이지의 오른쪽 위 모서리에 있는 <strong>선택 </strong>을 탭하여 이전 페이지의 [액션] 패널로 돌아갑니다.<br /> 경험  <a href="/help/sites-authoring/experience-fragments.md">조각을 참조하십시오</a>.</li> 
      </ul> 
       <ul> 
       <li>비디오에 나타나는 경험 조각의 폭과 높이를 지정합니다.</li>
       </ul><strong>참고</strong>:경험 조각에 뷰어를 포함할 때는 대화형 비디오의 소셜 미디어 공유 도구가 지원되지 않습니다. 이 문제를 해결하려면 소셜 미디어 공유 도구가 없는 뷰어 사전 설정을 사용하거나 만들 수 있습니다. 이러한 뷰어 사전 설정을 사용하여 경험 조각에 성공적으로 포함할 수 있습니다.</p></tr>&lt;&gt; 
      <tr> 
      <td>축소판 이미지에 이미 할당된 작업을 편집하려면</td> 
      <td>타임라인 세그먼트 내에서 텍스트 레이블 오른쪽에 체인 링크가 있는 축소판 이미지를 누릅니다. 체인 링크는 작업이 할당되었음을 나타냅니다. <strong>작업</strong> 탭을 눌러 변경합니다.</td> 
      </tr> 
      <tr> 
      <td>축소판 이미지의 텍스트 레이블을 변경하려면</td> 
      <td><p>기본적으로 텍스트 레이블은 축소판 이미지의 <code>Title</code> 메타데이터 필드를 사용합니다. <code>Title</code>이(가) 없는 경우 축소판 이미지의 파일 이름이 대신 사용되지만 확장명은 없습니다.</p> <p>축소판 이미지의 텍스트 레이블을 변경하려면 <strong>작업 </strong> 탭의 표시되는 이미지 자산 바로 아래에 원하는 텍스트를 입력합니다. 아래 그림을 참조하십시오.</p> <p>새 텍스트 레이블은 비디오 플레이어 자체와 타임라인 세그먼트에 표시되는 축소판 텍스트에서만 사용됩니다. 레이블 변경은 축소판 이미지의 [제목] 메타데이터 필드나 해당 파일 이름에 영향을 주지 않습니다.</p> </td> 
      </tr> 
      <tr> 
      <td>변경한 내용을 되돌리려면</td> 
      <td>페이지의 오른쪽 위 모서리 근처에 있는 <strong>실행 취소</strong> 또는 <strong>재실행</strong>을 탭합니다.</td> 
      </tr> 
    </tbody> 
   </table>

   ![experience_interactivevideos](assets/experiencefragment_interactivevideos.png)

   축소판 이미지에 새 텍스트 레이블이 추가됩니다.

1. 다음 중 하나를 수행하십시오.

   * 6-11단계를 반복하여 비디오의 타임라인 세그먼트에 축소판 이미지를 더 추가합니다.
   * 선택 단계 13으로 이동합니다.

1. (선택 사항) 다음 중 하나를 수행합니다.

   * **[!UICONTROL 세그먼트]**  병합 - 인접한 두 세그먼트(제품 축소판이 지정되거나 지정되지 않은 경우)를 하나의 세그먼트로 결합할 수 있습니다.

      타임라인에서 하나로 병합할 두 개 이상의 인접한 세그먼트를 누릅니다. 아래 그림에서 선택한 두 세그먼트에 파란색 타원 드래그 핸들이 없습니다.

      도구 모음에서 **[!UICONTROL 세그먼트 병합]**&#x200B;을 탭합니다.
   ![chlimage_1-134](assets/chlimage_1-134.png)

   선택한 5초 세그먼트를 10초 세그먼트로 2개 병합

   * **[!UICONTROL 세그먼트 분할]**  - 단일 세그먼트를 동일한 시간 지정 두 개의 세그먼트로 나눌 수 있습니다. 세그먼트에 이미 지정된 제품 축소판이 있는 경우 축소판이 왼쪽 세그먼트로 결합됩니다.

      타임라인에서 반으로 나눌 세그먼트를 탭한 다음 도구 모음에서 **[!UICONTROL 세그먼트 분할]**&#x200B;을 탭합니다.

      두 개 이상의 세그먼트를 선택하면 **[!UICONTROL 세그먼트 분할]** 기능이 비활성화됩니다.
   ![chlimage_1-135](assets/chlimage_1-135.png)

   선택한 10번째 세그먼트를 각각 5초의 2개의 세그먼트로 분할합니다.

1. **[!UICONTROL 대화형 비디오 만들기]** 페이지의 오른쪽 위 모서리 근처에 비디오에 사용된 현재 선택한 뷰어 사전 설정의 이름이 표시됩니다. 이름을 눌러 다른 뷰어 사전 설정을 선택합니다.

   예를 들어 `Shoppable_Video_light` 뷰어 사전 설정을 사용하면 비디오와 인접한 흰색 표시 영역이 있는 비디오를 재생할 수 있습니다. 표시 영역은 재생 중에 클릭 가능한 축소판 이미지가 표시되는 영역입니다. `Shoppable_Video_dark` 뷰어 사전 설정을 사용하면 비디오에 인접한 검은색 표시 영역을 사용하여 비디오를 재생할 수 있습니다.

   직접 대화형 비디오 뷰어 사전 설정을 만든 경우 선택할 수 있는 사전 설정 목록에서도 이 사전 설정이 표시됩니다.

   완료되면 **[!UICONTROL 저장을 탭합니다.]**

   >[!NOTE]
   대화형 비디오를 저장할 때 연결된 `.vtt` 파일이 해당 비디오와 함께 자동으로 저장됩니다. `.vtt` 파일은 **[!UICONTROL 에셋 루트에 있는 `_VTT` 폴더에 저장됩니다.]** 웹 사이트에서 대화형 비디오를 올바르게 재생하려면 파일과 폴더가 필요합니다. 따라서 `_VTT` 폴더 또는 해당 컨텐츠를 이동, 편집 또는 삭제하지 마십시오.

1. 대화형 비디오를 게시합니다. 게시를 사용하면 웹 사이트 경험에 최종적으로 복사하고 붙여넣을 포함 코드나 URL이 만들어집니다.

   Quickviews를 사용하여 인터랙티브한 요소를 추가한 경우 포함 코드만 사용하십시오.하이퍼링크된 웹 페이지에 인터랙티브한 요소를 추가한 경우 게시된 URL을 사용할 수도 있습니다. 그러나 인터랙티브한 컨텐츠에 상대 URL, 특히 AEM Sites 페이지에 대한 링크가 있는 경우에는 URL 기반 링크 연결 방법을 사용할 수 없습니다.

   [자산 게시](publishing-dynamicmedia-assets.md)를 참조하십시오.

   >[!NOTE]
   Quickviews를 사용하여 쇼퍼블 비디오를 게시하려면 상거래 영역에서 각 비디오의 관련 이미지 에셋을 별도로 게시해야 합니다.

   타임라인 세그먼트를 추가하고 대화형 비디오를 게시한 후 기존 웹 사이트 랜딩 페이지에 추가할 수 있습니다. [웹 사이트와 대화형 비디오 통합을 참조하십시오.](#integrating-an-interactive-video-with-your-website)

## 대화형 비디오 자산 게시 중 {#publishing-interactive-video-assets}

대화형 비디오 자산을 게시하는 방법에 대한 자세한 내용은 [자산 게시](/help/assets/publishing-dynamicmedia-assets.md)을 참조하십시오.

## 대화형 비디오를 웹 사이트 {#integrating-an-interactive-video-with-your-website}와 통합

비디오를 업로드하고 타임라인 세그먼트를 추가하고 대화형 비디오를 게시한 후 이제 기존 웹 사이트에 추가할 준비가 되었습니다.

AEM Sites 고객인 경우 대화형 미디어 구성 요소를 페이지로 드래그하여 대화형 비디오를 추가할 수 있습니다. [페이지에 Dynamic Media 자산 추가를 참조하십시오.](/help/assets/adding-dynamic-media-assets-to-pages.md)

독립 실행형 AEM Assets 고객인 경우 이 섹션에 설명된 대로 웹 사이트에 대화형 비디오를 수동으로 추가할 수 있습니다.

1. 게시된 대화형 비디오의 포함 코드 또는 URL을 복사합니다.
[웹 페이지에 비디오 또는 이미지 뷰어 포함](/help/assets/embed-code.md)을 참조하십시오.
Quickviews를 사용하여 인터랙티브한 요소를 추가한 경우 포함 코드만 사용하십시오.하이퍼링크된 웹 페이지에 인터랙티브한 요소를 추가한 경우 게시된 URL을 사용할 수도 있습니다. 그러나 인터랙티브한 컨텐츠에 상대 URL, 특히 AEM Sites 페이지에 대한 링크가 있는 경우에는 URL 기반 링크 연결 방법을 사용할 수 없습니다.

1. 대상의 웹 페이지 코드에서 정적 비디오가 있는 위치를 식별합니다.
1. 정적 비디오를 제거하고 코드를 그대로 AEM Assets에서 복사한 포함 코드 또는 URL로 바꿉니다.
복사된 포함 코드는 응답형 환경에 맞게 설정되므로 정적 비디오에 이전에 사용된 영역에 자동으로 맞게 지정됩니다.

>[!NOTE]
따라서 하이퍼링크된 웹 페이지로만 대화형 작업을 추가하면 됩니다.
그러나 Quickview를 트리거하는 대화형 기능을 추가한 경우 대화형 비디오에 인접한 축소판은 표시 목적으로만 사용됩니다.아직 기존 Quickviews와 통합되지 않았습니다. 이러한 경우 이제 대화형 비디오를 웹 사이트의 기존 Quickviews와 통합해야 합니다.

**예**

데모 웹 사이트를 예로 사용:

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html)

표준 비디오 포함 코드입니다.

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

통합은 비디오 포함 코드를 제거하고 AEM에서 인터랙티브한 비디오 포함 코드로 바꾸는 것만큼 간단합니다. 다음 URL에서 결과를 볼 수 있습니다. 페이지에 있는 대화형 비디오를 표시하지만, 이 비디오는 아직 기존 빠른 보기와 통합되지 않습니다.

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-1.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-1.html)

## 대화형 비디오를 기존 Quickview {#integrating-an-interactive-video-with-an-existing-quickview}과 통합

>[!NOTE]
이 작업은 독립 실행형 AEM Assets 고객인 경우에만 적용됩니다.

이 프로세스의 마지막 단계는 웹 사이트에서 사용되는 기존 Quickview 구현과 대화형 비디오를 통합하는 것입니다. 모든 경우에 적용되는 통합에 대한 해결 방법이 없습니다. 모든 Quickview 구현은 고유합니다. 따라서 프런트 엔드 IT 담당자의 지원을 필요로 하는 특정 접근 방식이 필요합니다.

일반적으로 기존 Quickview 구현은 웹 페이지에서 다음 순서로 발생하는 관련 간 작업 체인을 나타냅니다.

1. 사용자는 웹 사이트의 사용자 인터페이스에서 요소를 트리거합니다.
1. 프런트 엔드 코드는 1단계에서 트리거된 사용자 인터페이스 요소를 기반으로 Quickview URL을 가져옵니다.
1. 프런트 엔드 코드는 2단계에서 얻은 URL을 사용하여 AJAX 요청을 전송합니다.
1. 백엔드 로직은 해당 Quickview 데이터 또는 컨텐츠를 프런트 엔드 코드로 다시 반환합니다.
1. 프런트 엔드 코드는 Quickview 데이터 또는 컨텐츠를 로드합니다.
1. 선택적으로, 프런트 엔드 코드는 로드된 Quickview 데이터를 HTML 표현으로 변환합니다.
1. 프런트 엔드 코드는 모달 대화 상자나 패널을 표시하고 최종 사용자를 위해 화면에 HTML 컨텐츠를 렌더링합니다.

이러한 호출은 임의의 단계에서 웹 페이지 로직에서 호출할 수 있는 독립 공개 API 호출을 나타내지 않을 수 있습니다. 대신, 이전 단계의 마지막 단계(콜백)에서 모든 다음 단계가 숨겨지는 연쇄 호출입니다.

대화형 비디오가 1단계와 2단계를 부분적으로 대체하는 동시에 사용자가 대화형 비디오 내에서 축소판을 클릭하면 이러한 사용자 상호 작용은 뷰어에서 처리됩니다. 뷰어는 AEM에 이전에 추가한 모든 축소판 데이터를 포함하는 웹 페이지에 이벤트를 반환합니다.

이러한 이벤트 핸들러에서 프런트 엔드 코드는 다음을 수행합니다.

* 대화형 비디오에서 전송된 이벤트를 수신합니다.
* 축소판 데이터를 기반으로 빠른 보기 URL을 생성합니다.
* 백엔드에서 Quickview를 로드하고 표시하기 위해 화면에 렌더링하는 프로세스를 트리거합니다.

또한 대화형 비디오 뷰어는 전체 화면 작업 모드를 지원합니다. 최종 사용자는 전체 화면을 종료하지 않고 축소판을 클릭하여 빠른 보기를 트리거합니다. 이 기능을 수행하려면 [빠른 보기 양식] 대화 상자가 뷰어의 컨테이너에 연결되도록 프런트 엔드 코드를 변경합니다. 뷰어가 전체 화면 모드일 때 사용할 수 없는 문서 BODY 또는 다른 웹 페이지 요소를 추가하지 마십시오. 이 작업을 수행하는 코드는 뷰어가 페이지에 로드된 후 전송되는 하나 이상의 뷰어 콜백을 수신해야 합니다.

AEM에서 반환된 포함 코드에는 이미 사용 가능한 이벤트 핸들러가 있습니다. 강조 표시된 다음 코드 조각에서 볼 수 있는 것처럼 주석으로 처리됩니다.

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

따라서 위의 강조 표시된 코드 조각에 대한 주석을 해제하고 더미 핸들러 본문을 특정 웹 페이지에 맞는 코드로 교체해야 합니다.

표준 포함 코드에 2개의 기본 콜백 핸들러가 있습니다.`quickViewActivate` 및 `initComplete`. 뷰어에서 축소판을 클릭하면 `quickViewActivate` 핸들러가 트리거됩니다. 뷰어를 Quickview 활성화 로직과 통합하는 데 사용합니다. `initComplete` 핸들러는 뷰어가 페이지로 로드될 때 한 번만 트리거합니다. 이 핸들러는 웹 페이지 DOM의 빠른 보기 대화 상자 위치를 조정하는 데 사용됩니다.

Quickview URL을 구성하는 프로세스는 이 주제의 앞부분에서 다루는 축소판 변수를 식별하는 프로세스와 반대됩니다. 이전에 식별한 Quickview URL 예를 사용하면 각 케이스에서 Quickview URL이 구성되는 방식을 확인할 수 있습니다.

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

Quickview URL을 트리거하고 Quickview 패널을 활성화하는 마지막 단계는 IT 부서의 프런트 엔드 IT 담당자의 지원이 필요합니다. 바로 사용할 수 있는 Quickview URL을 사용하여 적절한 단계에서 Quickview 구현을 정확하게 트리거하는 방법을 잘 알고 있습니다.

이러한 단계를 데모 웹 사이트에 적용하여 인터랙티브한 비디오를 Quickview 코드와 완벽하게 통합하는 방법을 확인할 수 있습니다. 이 항목의 앞부분에서 Quickview URL의 구조는 다음과 같이 확인되었습니다.

```xml
/datafeed/$CategoryId$-$SKU$.json
```

다음과 같이 뷰어의 코드를 통해 핸들러에 전달되는 `inData` 객체에 있는 `categoryId` 및 `sku` 필드를 사용하여 `quickViewActivate` 핸들러 내에서 이 URL을 재구성하는 것은 쉽습니다.

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

데모 웹 사이트에서 간단한 `loadQuickView()` 함수 호출을 사용하여 빠른 보기 대화 상자를 트리거합니다. 이 함수는 Quickview 데이터 URL인 하나의 인수만 사용합니다. 따라서 대화형 비디오를 통합하는 데 필요한 마지막 단계는 다음 코드 행을 `quickViewActivate` 핸들러에 추가하는 것입니다.

```xml
loadQuickView(quickViewUrl);
```

마지막으로 [빠른 보기] 대화 상자가 뷰어의 컨테이너 요소에 연결되어 있는지 확인합니다. 기본 포함 코드는 이 기능을 수행하는 샘플 단계를 제공합니다. 뷰어의 컨테이너 요소에 대한 참조를 얻으려면 다음 코드 줄을 사용할 수 있습니다.

```xml
var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
var inner_container = document.getElementById(sdkContainerId);
```

여기서 `inner_container`은 뷰어가 관리하는 `DIV` 요소에 대한 참조입니다. 대화 상자를 `DIV`의 자식으로 지정합니다.

모달 대화 상자 요소를 실제로 찾아 위 컨테이너에 첨부하는 단계는 대/소문자를 구분합니다. 필요한 Quickview 구현에 익숙한 프런트 엔드 개발자의 도움을 받을 수 있습니다.

샘플 웹 사이트의 경우 빠른 보기 모달 대화 상자가 문서 `BODY`에 직접 연결된 quickview-modal ID와 함께 `DIV`으로 구현됩니다. 따라서 대화 상자를 뷰어의 컨테이너로 이동하는 코드는 다음과 같이 간단합니다.

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

완전히 통합된 대화형 비디오가 포함된 최종 데모 웹 사이트는 다음과 같습니다.

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-3.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-3.html)

## 빠른 보기를 사용하여 사용자 지정 팝업 만들기 {#using-quickviews-to-create-custom-pop-ups}

[빠른 보기를 사용하여 사용자 정의 팝업 만들기](/help/assets/custom-pop-ups.md)를 참조하십시오.
