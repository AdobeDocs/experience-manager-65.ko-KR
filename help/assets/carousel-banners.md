---
title: 회전 배너
description: Dynamic Media에서 회전 배너를 사용하여 작업하는 방법을 알아봅니다
uuid: 73684a08-d84d-4665-ab89-3a1bf88ac5dd
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: e26c7f7f-bdd7-421a-8614-ba48abf381d2
docset: aem65
feature: 회전 배너
role: User, Admin
exl-id: 53d34d3a-ecb6-4fa0-9665-60d21f48021e
source-git-commit: 5192a284c38eb10c214c67a8727de0f7dd4d1ee2
workflow-type: tm+mt
source-wordcount: '4732'
ht-degree: 0%

---

# 회전 배너{#carousel-banners}

회전 배너를 통해 마케터는 대화형 회전 프로모션 컨텐츠를 쉽게 만들어 모든 화면에 전달하여 전환을 촉진할 수 있습니다.

홍보 배너에 포함된 콘텐츠를 만들고 수정하는 데에는 시간이 오래 걸릴 수 있으므로 새 콘텐츠를 빠르게 게시하거나 더 타겟팅할 수 있는 기능을 제한할 수 있습니다. 회전 배너를 사용하여 회전 배너를 빠르게 만들거나 수정할 수 있습니다. 제품 세부 사항 또는 관련 리소스에 연결하는 핫스팟과 같은 인터랙티브한 요소를 추가하고 모든 화면에 제공할 수 있으므로 새로운 홍보 컨텐츠를 보다 빠르게 출시할 수 있습니다.

캐러셀 배너는 **[!UICONTROL CAROUSELSET]**&#x200B;이라는 단어가 포함된 배너에 의해 지정됩니다

![chlimage_1-438](assets/chlimage_1-438.png)

웹 사이트에서 회전 배너는 다음과 같이 표시될 수 있습니다.

![chlimage_1-439](assets/chlimage_1-439.png)

여기에서 이미지를 탐색할 수 있습니다(숫자를 클릭). 또한 슬라이드는 사용자 정의할 수 있는 시간 간격에 따라 자동으로 회전합니다. 회전 배너에 추가하는 이미지는 핫스팟과 이미지 맵을 모두 지원합니다. 이 맵에서는 사용자가 하이퍼링크를 선택하거나 이동하여 하이퍼링크 또는 빠른 보기 창에 액세스할 수 있습니다.

이 예에서는 사용자가 이미지 맵을 탭하거나 클릭하고 장갑을 찾기 위해 빠른 보기 창에 액세스합니다.

![chlimage_1-440](assets/chlimage_1-440.png)

## 회전 배너가 만들어지는 방식을 확인하십시오 {#watch-how-carousel-banners-are-created}

[캐러셀 배너를 만드는 방법에 대한 연습을 재생합니다](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner)(10분 33초). 또한 회전 배너를 미리 보고 편집하고 전달하는 방법을 알아봅니다.

>[!NOTE]
>
>회전 배너를 만들거나 편집하려면 관리자가 아닌 사용자를 **[!UICONTROL dam-users]** 그룹에 추가해야 합니다. 만들거나 편집하는 데 문제가 있는 경우 **[!UICONTROL dam-users]** 그룹에 사용자를 추가할 수 있는 시스템 관리자에게 문의하십시오.

## 빠른 시작: 회전 배너 {#quick-start-carousel-banners}

회전 배너를 사용하여 빠르게 시작하고 실행하려면:

1. [핫스팟 및 이미지 맵 변수](#identifying-hotspot-and-image-map-variables)  식별(Experience Manager 자산 + Dynamic Media을 사용하는 고객에게만 해당됨)

   먼저 Adobe Experience Manager Assets의 캐러셀 배너 작성 프로세스 중에 핫스팟과 이미지 맵 데이터를 제대로 입력할 수 있도록 기존 Quickview 구현에서 사용하는 동적 변수를 식별합니다.

   >[!NOTE]
   >
   >Experience Manager 사이트 또는 Ecommerce 고객인 경우 기본 기능을 사용하여 제품 페이지로 이동하고 제품 카탈로그에서 기존 SKU(Stock Keeping Unit)를 조회할 수 있습니다. 핫스팟이나 이미지 맵 변수를 수동으로 입력할 필요가 없습니다. [eCommerce](/help/commerce/cif-classic/administering/generic.md) 설정에 대한 정보를 참조하십시오.
   >
   >
   >Experience Manager 자산 및 Dynamic Media 고객의 경우, 핫스팟과 이미지 맵에 대한 데이터를 수동으로 입력한 다음 게시된 URL 또는 포함 코드를 타사 컨텐츠 관리 시스템과 통합합니다.

1. 선택 사항: [필요에 따라 회전 메뉴 집합 뷰어 사전 설정을 만듭니다](/help/assets/managing-viewer-presets.md).

   관리자의 경우 자체 캐러셀 뷰어 사전 설정을 만들어 회전판의 동작과 모양을 사용자 지정할 수 있습니다. 주요 이점은 여러 회전 메뉴에 대해 이 사용자 지정 뷰어 사전 설정을 재사용할 수 있다는 것입니다. 그러나 사용자는 회전판을 작성하는 동안 회전판의 동작 및 모양을 직접 사용자 지정할 수도 있습니다. 이 방법은 지정된 회전판에 대해 특정 디자인을 원하는 경우 선호하는 방법입니다.

1. [이미지 배너를 업로드합니다](#uploading-image-banners).

   대화형 이미지를 만들 이미지 배너를 업로드합니다.

1. [회전 메뉴 세트를 만듭니다](#creating-carousel-sets).

   회전 메뉴 세트에서 사용자는 배너 이미지를 탐색하고 핫스팟이나 이미지 맵을 선택하여 관련 컨텐츠에 액세스합니다.

   자산에 회전 메뉴 세트를 만들려면 **[!UICONTROL 만들기]**&#x200B;를 선택한 다음 **[!UICONTROL 회전 메뉴 세트]**&#x200B;를 선택합니다. 슬라이드에 자산을 추가하고 **[!UICONTROL 저장]**&#x200B;을 선택합니다. 편집기 내에서 직접 회전판의 모양과 동작을 편집할 수도 있습니다.

1. [이미지 배너에 핫스팟이나 이미지 맵을 추가합니다](#adding-hotspots-or-image-maps-to-an-image-banner).

   이미지 배너에 핫스팟이나 이미지 맵을 한 개 이상 추가하고 각 핫스팟을 링크, 빠른 보기 또는 경험 조각과 같은 작업에 연결합니다. 핫스팟이나 이미지 맵을 추가한 후에는 회전 메뉴 세트를 게시하여 이 작업을 완료합니다. 게시하면 웹 사이트 랜딩 페이지를 복사하여 적용하는 데 사용할 수 있는 포함 코드가 만들어집니다.

   [(선택 사항) 미리 보기 회전 배너](#optional-previewing-carousel-banners) - 선택 사항 을 참조하십시오. 원하는 경우 회전 메뉴 세트의 표시를 보고 상호 작용을 테스트할 수 있습니다.

1. [회전 배너를 게시합니다](#publishing-carousel-banners).

   모든 자산과 마찬가지로 회전 메뉴 세트를 게시합니다. 자산에서 회전 메뉴 집합으로 이동하여 선택한 다음 **[!UICONTROL 게시]**&#x200B;를 선택합니다. 회전 메뉴 세트를 게시하면 URL 및 포함 문자열이 활성화됩니다.

1. 다음 중 하나를 수행하십시오.

   * [웹 사이트 페이지에 회전 배너 추가](#adding-a-carousel-banner-to-your-website-page) 웹 사이트 페이지에 복사한 회전 배너 URL 또는 포함 코드를 추가할 수 있습니다.

      * [캐러셀 배너를 기존 빠른 보기와 통합합니다](#integrating-the-carousel-banner-with-an-existing-quickview). 타사 웹 컨텐츠 관리 시스템을 사용하는 경우 새 회전 배너를 웹 사이트의 기존 Quickview 구현과 통합해야 합니다.
   * [Experience ](/help/assets/adding-dynamic-media-assets-to-pages.md) Manager에서 웹 사이트에 회전 배너를 추가합니다. Experience Manager 사이트 고객인 경우 대화형 미디어 구성 요소를 사용하여 Experience Manager의 페이지에 직접 회전 메뉴 세트를 추가할 수 있습니다.


회전판 세트를 편집하려면 [회전판 세트 편집](#editing-carousel-sets)을 참조하십시오. 또한 [회전 메뉴 설정 속성](manage-assets.md#editing-properties)을 보고 편집할 수 있습니다.

## 핫스팟 및 이미지 맵 변수 식별 {#identifying-hotspot-and-image-map-variables}

먼저 Experience Manager Assets에서 회전판 세트 생성 프로세스 중에 핫스팟이나 이미지 맵 데이터를 제대로 입력할 수 있도록 기존 Quickview 구현에서 사용하는 동적 변수를 식별합니다.

Experience Manager Assets의 배너 이미지에 핫스팟이나 이미지 맵을 추가할 때 각 핫스팟이나 이미지 맵에 SKU 및 선택적 추가 변수를 할당합니다. 이러한 변수는 나중에 핫스팟이나 이미지 맵을 Quickview 컨텐츠와 일치시키는 데 사용됩니다.

>[!NOTE]
>
>Experience Manager 사이트 및/또는 Experience Manager Ecommerce 고객인 경우 이 단계를 건너뜁니다. 핫스팟이나 이미지 맵 변수를 수동으로 식별할 필요는 없습니다. 제품 통합을 위해 Ecommerce와의 통합을 사용할 수 있습니다. [eCommerce](/help/commerce/cif-classic/administering/generic.md) 설정에 대한 정보를 참조하십시오. 또한 대화형 구성 요소를 사용하여 웹 페이지에 추가할 수 있습니다.
>
>Assets 또는 Media Experience Manager 고객의 경우 URL 또는 포함 코드를 게시한 다음 타사 컨텐츠 관리 시스템과 통합하여 핫스팟과 이미지 맵을 수동으로 식별합니다.

핫스팟이나 이미지 맵 데이터와 연결할 변수의 수 및 유형을 올바르게 식별하는 것이 중요합니다. 배너 이미지에 추가된 각 핫스팟이나 이미지 맵은 기존 백엔드 시스템에서 제품을 명확하게 식별할 수 있도록 충분한 정보를 전달해야 합니다. 동시에 각 핫스팟이나 이미지 맵에 필요한 것보다 더 많은 데이터가 포함되지 않아야 합니다. 이유는 이렇게 하면 데이터 입력 프로세스가 지나치게 복잡해지고 진행 중인 핫스팟이나 이미지 맵 관리에 오류가 발생하기 쉽습니다.

핫스팟이나 이미지 맵 데이터에 사용할 변수 세트를 식별하는 방법은 서로 다릅니다.

기존 Quickview 구현을 담당하는 IT 전문가에게 문의하는 것도 충분합니다. 따라서 시스템에서 빠른 보기를 식별하는 데 필요한 최소 데이터 세트가 무엇인지 알 수 있을 것입니다. 그러나 일반적으로 프런트 엔드 코드의 기존 동작을 간단히 분석할 수도 있습니다.

대부분의 빠른 보기 구현에서는 다음 패러다임을 사용합니다.

* 사용자가 웹 사이트에서 사용자 인터페이스 요소를 활성화합니다. 예를 들어 **[!UICONTROL Quickview]** 단추를 탭합니다.
* 필요한 경우 웹 사이트에서 Quickview 데이터 또는 콘텐츠를 로드하기 위해 백엔드에 Ajax 요청을 보냅니다.
* 빠른 보기 데이터는 웹 페이지에서 렌더링을 준비하기 위해 컨텐츠로 변환됩니다.
* 마지막으로 프런트 엔드 코드는 그러한 콘텐츠를 화면에서 시각적으로 렌더링합니다.

그런 다음 빠른 보기 기능이 구현된 기존 웹 사이트의 다른 영역을 방문하는 것이 좋습니다. Quickview를 트리거하고 Quickview 데이터 또는 컨텐츠를 로드하기 위해 웹 페이지에서 보낸 Ajax URL을 캡처합니다.

일반적으로 전문 디버깅 도구를 사용할 필요가 없습니다. 최신 웹 브라우저에는 적절한 작업을 수행하는 웹 검사자가 포함되어 있습니다. 다음은 웹 관리자를 포함하는 웹 브라우저의 몇 가지 예입니다.

* Google Chrome에서 나가는 HTTP 요청을 모두 보려면 F12(Windows) 또는 Command-Option-I(Mac)를 눌러 개발자 도구 패널을 열고 네트워크 탭을 선택하십시오.
* Firefox에서는 F12(Windows) 또는 Command-Option-I(Mac)를 눌러 Firebug 플러그인을 활성화하고 Net 탭을 사용하거나 내장 Inspector 도구 및 Network 탭을 사용할 수 있습니다.

브라우저에서 네트워크 모니터링이 켜져 있으면 페이지에서 빠른 보기를 트리거합니다.

이제 네트워크 로그에서 Quickview Ajax URL을 찾아 기록된 URL을 복사하여 향후 분석할 수 있습니다. 일반적으로 빠른 보기를 트리거할 때, 서버로 전송되는 요청이 많습니다. 일반적으로 Quickview Ajax URL은 목록에서 첫 번째 중 하나입니다. 여기에는 복잡한 쿼리 문자열 부분 또는 경로가 있으며 해당 응답 MIME 유형은 `text/html`, `text/xml` 또는 `text/javascript`입니다.

이 프로세스 중에 제품 카테고리와 유형이 다른 웹 사이트의 다양한 영역을 방문하는 것이 중요합니다. 이유는 Quickview URL에 주어진 웹 사이트 카테고리에 대해 공통인 부분이 있지만 웹 사이트의 다른 영역을 방문하는 경우에만 변경되기 때문입니다.

가장 간단한 경우 Quickview URL에 있는 유일한 변수 부분은 제품 SKU입니다. 이 경우 SKU 값은 배너 이미지에 핫스팟이나 이미지 맵을 추가하는 데 필요한 유일한 데이터 조각입니다.

그러나 복잡한 경우, Quickview URL은 카테고리 ID, 색상 코드 및 크기 코드 등 SKU 외에도 다양한 요소를 제공합니다. 이러한 경우 모든 요소는 캐러셀 배너 기능의 핫스팟이나 이미지 맵 데이터 정의에 있는 별도의 변수입니다.

Quickview URL 및 그 결과 핫스팟이나 이미지 맵 변수의 다음 예를 생각해 보십시오.

<table>
 <tbody>
  <tr>
   <td>쿼리 문자열에 있는 단일 SKU입니다.</td>
   <td><p>기록된 Quickview URL은 다음과 같습니다.</p>
    <ul>
     <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>URL의 유일한 변수 부분은 <code>productId=</code> 쿼리 문자열 매개 변수의 값이며 이는 명확하게 SKU 값입니다. 따라서 핫스팟이나 이미지 맵에는 다음과 같은 값으로 채워진 SKU 필드만 필요합니다 <code>866558,</code> <code>1196184,</code> <code>1081492,</code> <code>1898294.</code></p> </td>
  </tr>
  <tr>
   <td>URL 경로에 있는 단일 SKU입니다.</td>
   <td><p>기록된 Quickview URL은 다음과 같습니다.</p>
    <ul>
     <li><p><code>https://server/product/6422350843</code></p> </li>
     <li><p><code>https://server/product/1607745002</code></p> </li>
     <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>변수 부분은 경로의 마지막 부분에 있으며 핫스팟/이미지 맵의 SKU 값이 됩니다.<strong><code>6422350843</code>, <code>1607745002,</code> </strong><code>0086724882.</code></p> </td>
  </tr>
  <tr>
   <td>쿼리 문자열의 SKU 및 카테고리 ID.</td>
   <td><p>기록된 Quickview URL은 다음과 같습니다.</p>
    <ul>
     <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>이 경우 URL에는 두 가지 다양한 부분이 있습니다. SKU는 <code>prodId</code> 매개 변수에 저장되고 카테고리 ID는 <code>category=</code> 매개 변수에 저장됩니다.</p> <p>따라서 핫스팟/이미지 맵 정의는 쌍입니다. 즉, SKU 값과 <code>categoryId</code>이라는 추가 변수가 있습니다. 결과 쌍은 다음과 같습니다.</p>
    <ul>
     <li><p>SKU는 <strong><code>305466</code></strong>이고 <code>categoryId</code>는 <code>1100004</code>입니다.</p> </li>
     <li><p>SKU는 <strong><code>310181</code></strong>이고 <code>categoryId</code>는 <strong><code>1100004</code></strong>입니다.</p> </li>
     <li><p>SKU는 <strong><code>308706</code></strong>이고 <code>categoryId</code>는 <strong><code>1740148</code></strong>입니다.</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 이미지 배너 업로드 {#uploading-image-banners}

사용하려는 이미지를 이미 업로드한 경우 다음 단계인 [회전 메뉴 세트 만들기](#creating-carousel-sets)로 이동하십시오. 회전판에 사용되는 이미지는 Dynamic Media이 활성화된 후에 업로드해야 합니다.

이미지 배너를 업로드하려면 [자산 업로드](/help/assets/manage-assets.md)를 참조하십시오.

## 회전판 세트 만들기 {#creating-carousel-sets}

>[!NOTE]
>
>회전 배너를 만들거나 편집하려면 관리자가 아닌 사용자를 **[!UICONTROL dam-users]** 그룹에 추가해야 합니다. 만들거나 편집하는 데 문제가 있는 경우 **[!UICONTROL dam-users]** 그룹에 사용자를 추가할 수 있는 시스템 관리자에게 문의하십시오.

**회전판 세트를 만들려면 다음을 수행하십시오.**

1. 자산에서 회전판 세트를 만들 폴더로 이동하여 **[!UICONTROL 만들기]** > **[!UICONTROL 회전판 세트]**&#x200B;로 이동합니다.
1. 캐러셀 배너 편집기 페이지에서 **[!UICONTROL 탭하여 자산 선택기]**&#x200B;를 열어 첫 번째 슬라이드에 대한 이미지를 선택합니다.

   캐러셀 배너 편집기 페이지에서 다음 중 하나를 수행합니다.

   * 페이지의 왼쪽 위 모서리 근처에 있는 **[!UICONTROL 슬라이드 추가]** 아이콘을 선택합니다.

   * 페이지 가운데 근처에 있는 **[!UICONTROL 탭하여 자산 선택기]**&#x200B;를 엽니다.
   회전판 세트에 포함할 자산을 선택하려면 선택합니다. 선택한 자산에는 확인 표시 아이콘이 표시됩니다. 완료되면 페이지의 오른쪽 위 모서리 근처에 있는 **[!UICONTROL 선택]**&#x200B;을 선택합니다.

   자산 선택기를 사용하여 키워드를 입력하고 **[!UICONTROL Return]**&#x200B;을 탭하거나 클릭하여 자산을 검색할 수 있습니다. 필터를 적용하여 검색 결과를 세분화할 수도 있습니다. 경로, 컬렉션, 파일 유형 및 태그별로 필터링할 수 있습니다. 필터를 선택한 다음 도구 모음에서 **[!UICONTROL 필터]** 아이콘을 선택합니다. 보기 아이콘을 탭하고 **[!UICONTROL 열 보기]**, **[!UICONTROL 카드 보기]** 또는 **[!UICONTROL 목록 보기]**&#x200B;를 선택하여 보기를 변경합니다.

   자세한 내용은 [선택기를 사용한 작업](/help/assets/working-with-selectors.md)을 참조하십시오.

1. 회전판 세트에서 회전할 모든 이미지를 추가할 때까지 슬라이드를 계속 추가합니다.
1. (선택 사항) 다음 중 하나를 수행합니다.

   * 필요한 경우 슬라이드를 드래그하여 이 목록에서 이미지를 재정렬합니다.
   * 이미지를 삭제하려면 이미지를 선택한 다음 도구 모음에서 **[!UICONTROL 슬라이드 삭제]**&#x200B;를 선택합니다.

   * 페이지의 오른쪽 위 모서리 근처에 있는 사전 설정을 적용하려면 사전 설정 드롭다운 목록을 선택한 다음, 세트에 한 번에 적용할 사전 설정을 선택합니다.
   슬라이드를 삭제하려면 슬라이드를 선택한 다음 도구 모음에서 **[!UICONTROL 슬라이드 삭제]**&#x200B;를 선택합니다. 슬라이드를 이동하려면 순서 조정 아이콘을 선택하고 누른 채로 원하는 위치로 이동합니다.

1. 슬라이드에 이미지를 추가한 후 이미지에 핫스팟이나 이미지 맵 또는 둘 다 추가할 수 있습니다. [이미지 배너에 핫스팟 또는 이미지 맵 추가](#adding-hotspots-or-image-maps-to-an-image-banner)를 참조하십시오.
1. 회전판 세트의 시각적 디자인과 동작을 변경할 수 있습니다. **[!UICONTROL 동작]** 및 **[!UICONTROL 모양]** 탭을 선택하고 회전 배너가 표시되는 방식 또는 특정 구성 요소가 동작하는 방식을 조정합니다. 뷰어 편집기 사용 방법에 대한 자세한 내용은 [뷰어 사전 설정 관리](/help/assets/viewer-presets.md) 를 참조하십시오.

   >[!NOTE]
   >
   >회전 배너의 경우 다음과 같이 조정할 수 있습니다.
   >
   >    * 이미지가 표시되는 기간입니다. 기본적으로 각 이미지는 9초 동안 표시됩니다.
   >    * 애니메이션. 기본적으로 각 슬라이드 전환은 페이드입니다. 슬라이드 전환으로 변경할 수 있습니다.
   >    * 단추의 스타일입니다. 각 점 또는 숫자를 탭하여 배너를 통해 회전할 수 있습니다. 세트 표시기 단추가 표시되는 위치와 숫자 또는 점선 스타일인 경우 그 크기를 변경할 수 있습니다.
   >    * 이미지 맵의 밝은 영역 스타일 또는 핫스팟에 사용되는 아이콘을 변경합니다.
   >    * 뷰어 사전 설정을 편집하기 전에 사전 설정을 기반으로 할 스타일을 선택합니다. 스타일을 선택하지 않으면 뷰어 사전 설정을 편집하기 시작하면 다른 사전 설정으로 변경하기로 하면 모든 변경 사항이 손실됩니다.

   >
   >뷰어 편집기에 대한 자세한 설명과 자세한 내용은 [회전 배너에 대한 특수 고려 사항](/help/assets/managing-viewer-presets.md#special-considerations-for-creating-a-carousel-banner-viewer-preset)을 참조하십시오.

   캐러셀 배너가 표시되는 방식을 미리 볼 수도 있습니다. [(선택 사항) 미리 보기 회전 배너](#optional-previewing-carousel-banners)를 참조하십시오.

1. 완료되면 **[!UICONTROL 저장]**&#x200B;을 선택합니다.

## 이미지 배너에 핫스팟 또는 이미지 맵 추가 {#adding-hotspots-or-image-maps-to-an-image-banner}

회전판 세트 편집기를 사용하여 배너에 핫스팟이나 이미지 맵을 추가할 수 있습니다.

핫스팟이나 이미지 맵을 추가할 때 핫스팟이나 이미지 맵을 하이퍼링크 또는 경험 조각으로 빠른 보기 팝업 디스플레이로 정의할 수 있습니다.

[경험 조각](/help/sites-authoring/experience-fragments.md)을 참조하십시오.

>[!NOTE]
>
>캐러셀 배너의 소셜 미디어 공유 도구는 경험 조각에 뷰어를 포함할 때 지원되지 않습니다.
>
>이 문제를 해결하려면 소셜 미디어 공유 도구가 없는 뷰어 사전 설정을 사용하거나 만들 수 있습니다. 이러한 뷰어 사전 설정을 사용하면 경험 조각에 성공적으로 포함할 수 있습니다.

이미지에 핫스팟이나 이미지 맵을 추가할 때 작업을 저장해야 합니다. 현재 작성/편집 세션 중에 페이지의 오른쪽 위 모서리 근처에 있는 실행 취소 및 재실행 옵션이 지원됩니다.

캐러셀 배너 만들기를 완료하면 선택적으로 미리 보기 를 사용하여 캐러셀 배너가 고객에게 표시되는 방식을 확인할 수 있습니다.

[(선택 사항) 미리 보기 회전 배너](#optional-previewing-carousel-banners)를 참조하십시오.

>[!NOTE]
>
>[대화형 이미지](/help/assets/interactive-images.md) 또는 회전 배너의 이미지에 핫스팟을 추가하면 핫스팟이 동일한 메타데이터 위치에 저장됩니다. 해당 위치는 대화형 이미지나 회전 배너 여부에 관계없이 이미지의 위치를 기준으로 합니다. 이 기능은 두 뷰어에서 동일한 이미지를 정의된 핫스팟 데이터와 함께 쉽게 다시 사용할 수 있음을 의미합니다.
그러나 회전 배너는 핫스팟도 포함될 수 있는 이미지에서 이미지 맵을 지원합니다. 대화형 이미지는 표시되지 않습니다. 동일한 이미지를 사용하는 대화형 이미지나 회전 배너를 만들려는 경우에는 이 규칙을 염두에 두십시오. 대신 동일한 이미지의 별도 사본을 사용하여 대화형 이미지와 회전 배너를 만드는 것이 좋습니다.

>[!NOTE]
핫스팟으로 대화형 이미지를 편집하고 이미지를 자르면 핫스팟이 제거됩니다.

[이미지 맵 추가](/help/assets/image-maps.md)도 참조하십시오.

**이미지 배너에 핫스팟이나 이미지 맵을 추가하려면 다음을 수행합니다.**

1. Assets에서 인터랙티브하게 만들 회전 메뉴 세트로 이동합니다.
1. 회전판 세트를 선택하고 **[!UICONTROL 편집]**&#x200B;을 선택합니다. 회전판 뷰어 편집기가 열립니다.
1. 대화형으로 만들 슬라이드를 선택합니다.
1. 페이지의 왼쪽 위 모서리 근처에 있는 **[!UICONTROL Hotspot]** 또는 **[!UICONTROL 이미지 맵]**&#x200B;을 선택합니다.
1. 다음 중 하나를 수행합니다.

   * 핫스팟: 이미지에서 핫스팟을 표시할 위치를 선택합니다.
   * 이미지 맵의 경우: 이미지에서 를 선택한 다음 왼쪽 상단에서 오른쪽 하단으로 드래그하여 이미지 맵 영역을 만듭니다. 모퉁이를 끌어서 이미지 맵의 크기를 조정할 수 있습니다.

   필요한 경우 핫스팟이나 이미지 맵을 새 위치로 드래그합니다. 필요에 따라 핫스팟이나 이미지 맵을 추가합니다.

   핫스팟이나 이미지 맵을 삭제하려면 **[!UICONTROL 작업]** 탭을 선택합니다. **[!UICONTROL 맵 및 핫스팟]** 제목의 **[!UICONTROL 선택한 유형]** 드롭다운 메뉴에서 제거할 핫스팟이나 이미지 맵의 이름을 선택합니다. 메뉴 옆에 있는 **[!UICONTROL 휴지통]** 아이콘을 선택한 다음 **[!UICONTROL 삭제]**&#x200B;를 선택합니다.

1. 이름 텍스트 필드에 핫스팟이나 이미지 맵의 이름을 입력합니다. 이 이름은 **[!UICONTROL 맵 및 핫스팟]** 드롭다운 목록에도 나타납니다. 이름을 제공하면 나중에 핫스팟이나 이미지 맵을 변경하기로 결정하는 경우 핫스팟이나 이미지 맵을 쉽게 식별할 수 있습니다.
1. **[!UICONTROL 작업]** 탭에서 다음 중 하나를 수행합니다.

   * **[!UICONTROL Quickview]**&#x200B;를 선택합니다.

      * Experience Manager 사이트 및 Ecommerce 고객인 경우 제품 선택기 아이콘(확대경)을 선택하여 제품 선택 페이지를 엽니다. 사용할 제품을 선택한 다음 회전판 배너 편집기로 돌아갈 수 있도록 페이지의 오른쪽 위 모서리에서 확인 표시를 선택합니다.
      * Experience Manager 사이트 또는 Ecommerce 고객이 아닌 경우

         * 이러한 변수를 정의하려면 [핫스팟 변수 식별](#identifying-hotspot-and-image-map-variables) 을 참조하십시오.
         * 그런 다음 SKU 값을 수동으로 입력합니다. SKU 값 텍스트 필드에 제공하는 각 개별 제품 또는 서비스의 고유 식별자인 제품의 SKU(Stock Keeping Unit)를 입력합니다. 입력한 SKU 값은 Quickview 템플릿의 변수 부분을 자동으로 채우므로 시스템이 탭된 핫스팟을 특정 SKU의 Quickview와 연결하려는 것을 알게 됩니다.
         * (선택 사항) Quickview 내에 제품을 추가로 식별하는 데 사용해야 하는 다른 변수가 있는 경우 **[!UICONTROL 일반 변수 추가]**&#x200B;를 선택합니다. 텍스트 필드에 추가 변수를 지정합니다. 예를 들어 category=Mens는 추가된 변수입니다.

         * 자세한 내용은 [선택기를 사용한 작업](/help/assets/working-with-selectors.md)을 참조하십시오.
   * **[!UICONTROL 하이퍼링크]**&#x200B;를 선택합니다.

      * Experience Manager 사이트 고객인 경우 사이트 선택기 아이콘(폴더)을 선택하여 URL로 이동합니다.
         >[!NOTE]
         대화형 컨텐츠에 상대 URL이 있는 링크, 특히 Experience Manager 사이트 페이지에 대한 링크가 있는 경우 URL 기반 연결 방법이 없습니다.

      * 독립형 고객인 경우, HREF 텍스트 필드에서 연결된 웹 페이지에 대한 전체 URL 경로를 지정합니다.

   링크를 새 브라우저 탭(권장 기본값)에서 열지 또는 동일한 탭에서 열지를 지정해야 합니다.

   자세한 내용은 [선택기 작업](/help/assets/working-with-selectors.md)을 참조하십시오.

   * **[!UICONTROL 경험 조각]**&#x200B;을 선택합니다.

      * Experience Manager 사이트 고객인 경우 검색 아이콘(확대경)을 선택하여 경험 조각 페이지를 엽니다. 사용할 경험 조각을 선택한 다음 핫스팟 관리 페이지로 돌아갈 수 있도록 페이지의 오른쪽 위 모서리에서 **[!UICONTROL 선택]**을 선택합니다.
[경험 구성요소](/help/sites-authoring/experience-fragments.md)를 참조하십시오.

      * 배너에 표시되는 경험 조각의 폭과 높이를 지정합니다.

         >[!NOTE]
         캐러셀 배너의 소셜 미디어 공유 도구는 경험 조각에 뷰어를 포함할 때 지원되지 않습니다.
         이 문제를 해결하려면 소셜 미디어 공유 도구가 없는 뷰어 사전 설정을 만드십시오. 이러한 뷰어 사전 설정을 사용하면 경험 조각에 성공적으로 포함할 수 있습니다.
   ![experience_fragment-carouselbanner](assets/experience_fragment-carouselbanner.png)

   캐러셀 배너가 표시되는 방식을 미리 볼 수도 있습니다. [(선택 사항) 회전 배너 미리 보기](#optional-previewing-carousel-banners)를 참조하십시오.

1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.
1. 회전판 세트를 게시합니다. 게시하면 웹 사이트 페이지에서 사용할 수 있는 포함 코드 또는 URL이 만들어집니다. Experience Manager 사이트 고객의 경우 웹 페이지에 직접 회전 메뉴 세트를 추가할 수 있습니다.

   [자산 게시](/help/assets/publishing-dynamicmedia-assets.md)를 참조하십시오.

   웹 사이트 랜딩 페이지에 설정된 회전 메뉴 추가](#adding-a-carousel-banner-to-your-website-page)를 참조하십시오[

## 회전 메뉴 집합 편집 {#editing-carousel-sets}

>[!NOTE]
회전 배너를 만들거나 편집하려면 관리자가 아닌 사용자를 **[!UICONTROL dam-users]** 그룹에 추가해야 합니다. 만들거나 편집하는 데 문제가 있는 경우 **[!UICONTROL dam-users]** 그룹에 사용자를 추가할 수 있는 시스템 관리자에게 문의하십시오.

다음과 같은 회전 메뉴 세트에서 다양한 편집 작업을 수행할 수 있습니다.

* 회전 메뉴에 슬라이드를 추가합니다. [선택기를 사용한 작업](/help/assets/working-with-selectors.md)도 참조하십시오.
* 회전판 세트에서 슬라이드 순서를 변경합니다.
* 회전판 세트에서 자산을 삭제합니다.
* 뷰어 사전 설정을 적용합니다.
* 회전판 세트를 삭제합니다.
* 핫스팟과 이미지 맵을 추가하거나 편집합니다. [선택기를 사용한 작업](/help/assets/working-with-selectors.md)도 참조하십시오.

**회전판 세트를 편집하려면**

1. 다음 중 하나를 수행합니다.

   * 회전판 세트 자산 위로 마우스를 가져간 다음 **[!UICONTROL 편집]**(연필 아이콘)을 선택합니다.
   * 회전판 세트 자산 위로 마우스를 가져간 후 **[!UICONTROL 선택]**(확인 표시 아이콘)을 선택한 다음, 도구 모음에서 **[!UICONTROL 편집]**&#x200B;을 선택합니다.

   * 회전판 세트 자산을 선택한 다음 페이지의 왼쪽 위 모서리에서 **[!UICONTROL 편집]** (연필 아이콘)을 선택합니다.

1. 회전판 세트를 편집하려면 다음 중 하나를 수행합니다.

   * 슬라이드를 추가하려면 **[!UICONTROL 슬라이드 추가]** 아이콘을 선택한 다음 해당 슬라이드에 추가할 자산으로 이동하여 확인 표시를 선택합니다.
   * 슬라이드를 다시 정렬하려면 슬라이드를 새 위치로 드래그합니다(항목을 이동하려면 다시 정렬 아이콘 선택).
   * 핫스팟이나 이미지 맵을 추가하려면 핫스팟이나 이미지 맵 아이콘을 선택하고 [핫스팟 및 이미지 맵 추가](#adding-hotspots-or-image-maps-to-an-image-banner)를 참조하십시오.
   * 회전판 집합의 모양이나 동작을 편집하려면 **[!UICONTROL 모양]** 탭 또는 **[!UICONTROL 동작]** 탭을 선택한 다음 원하는 옵션을 설정합니다.
   * 핫스팟이나 이미지 맵을 편집하려면 적절한 슬라이드에서 핫스팟이나 이미지 맵을 선택하고 **[!UICONTROL 작업]** 탭에서 필요에 따라 변경합니다.
   * 슬라이드를 삭제하려면 슬라이드를 선택한 다음 도구 모음에서 **[!UICONTROL 슬라이드 삭제]**&#x200B;를 선택합니다.
   * 페이지의 오른쪽 위 모서리 근처에 있는 사전 설정을 적용하려면 **[!UICONTROL 사전 설정]** 드롭다운 목록을 선택한 다음 뷰어 사전 설정을 선택합니다.
   * 전체 캐러셀 세트를 삭제하려면 캐러셀 세트로 이동하여 **[!UICONTROL 삭제]**&#x200B;를 선택합니다.

   >[!NOTE]
   핫스팟으로 대화형 이미지를 편집하고 이미지를 자르면 핫스팟이 제거됩니다.

## (선택 사항) 회전 배너 미리 보기 {#optional-previewing-carousel-banners}

[미리 보기]를 사용하여 회전 배너가 고객에게 표시되는 방식을 확인하고 회전 배너 핫스팟과 이미지 맵을 테스트하여 예상대로 작동하는지 확인할 수 있습니다.

캐러셀 배너에 만족하면 게시할 수 있습니다.
웹 페이지에 비디오 또는 이미지 뷰어 포함](/help/assets/embed-code.md)을 참조하십시오.
[
[URL을 웹 애플리케이션에 연결](/help/assets/linking-urls-to-yourwebapplication.md)을 참조하십시오. 대화형 컨텐츠에 상대 URL이 있는 링크, 특히 Experience Manager 사이트 페이지에 대한 링크가 있는 경우 URL 기반 연결 방법이 없습니다.
[페이지에 Dynamic Media 자산 추가](/help/assets/adding-dynamic-media-assets-to-pages.md)를 참조하십시오.

회전판 편집기(기본 설정 메서드) 또는 **[!UICONTROL Viewers]** 목록에서 회전판 배너를 미리 볼 수 있습니다.

**회전 배너를 미리 보려면:**

1. **[!UICONTROL Assets]**&#x200B;에서 생성한 기존 회전 배너로 이동하여 엽니다.
1. **[!UICONTROL 편집]**&#x200B;을 선택하십시오.
1. 도구 모음의 오른쪽 모서리에 있는 뷰어 사전 설정 목록에서 회전 배너를 미리 볼 뷰어를 선택합니다.

   ![experience_fragment-carousselbanner-viewerdropdown](assets/experience_fragment-carouselbanner-viewerdropdown.png)

1. **[!UICONTROL 미리 보기]**&#x200B;를 선택합니다.
1. 이미지에서 핫스팟이나 이미지 맵을 선택하여 연결된 작업을 테스트할 수 있습니다.

**뷰어 목록에서 회전 배너를 미리 보려면:**

1. **[!UICONTROL Assets]**&#x200B;에서 생성한 기존 회전 배너로 이동하여 엽니다.
1. 미리 보기 페이지의 왼쪽 위 모서리 근처에 있는 컨텐츠 아이콘을 선택합니다.
1. 페이지 왼쪽에 있는 패널의 **[!UICONTROL 뷰어]** 목록에서 사용할 캐러셀 배너 뷰어 사전 설정의 이름을 선택합니다.
1. 이미지에서 핫스팟이나 이미지 맵을 선택하여 연결된 작업을 테스트할 수 있습니다.

## 회전 배너 게시 {#publishing-carousel-banners}

사용할 수 있도록 회전판을 게시합니다. 회전 메뉴 세트를 게시하면 URL 및 포함 코드가 활성화됩니다. 또한 확장성과 성능을 제공하기 위해 CDN과 통합된 Dynamic Media 클라우드에 회전판을 게시합니다.

>[!NOTE]
캐러셀 배너의 핫스팟이 있는 기존 대화형 이미지를 사용하는 경우 캐러셀 배너를 게시한 후 개별적으로 대화형 이미지를 게시해야 합니다.
또한 회전 배너에서 사용하는 이전에 게시된 대화형 이미지를 수정한 경우 해당 변경 사항이 회전 배너에 반영되기 전에 대화형 이미지를 게시해야 합니다.

회전 배너를 게시하는 방법에 대한 자세한 내용은 [Dynamic Media 자산 게시](/help/assets/publishing-dynamicmedia-assets.md) 를 참조하십시오.

## 웹 사이트 페이지에 회전 배너를 추가합니다 {#adding-a-carousel-banner-to-your-website-page}

배너 이미지를 업로드하여 캐러셀, 핫스팟 및/또는 이미지 맵을 배너에 추가하고 캐러셀 세트를 게시하면 기존 웹 사이트 페이지에 추가할 수 있습니다.

>[!NOTE]
Experience Manager 사이트 고객의 경우 대화형 미디어 구성 요소를 페이지로 드래그하여 회전 배너를 페이지에 직접 추가할 수 있습니다. [페이지에 Dynamic Media 자산 추가](/help/assets/adding-dynamic-media-assets-to-pages.md)를 참조하십시오.

그러나 독립형 Experience Manager 자산 고객인 경우, 이 섹션에 설명된 대로 웹 사이트 랜딩 페이지에 회전 배너를 수동으로 추가할 수 있습니다.

1. 게시된 회전 메뉴 세트의 포함 코드를 복사합니다.
[웹 페이지에 비디오 또는 이미지 뷰어 포함](/help/assets/embed-code.md)을 참조하십시오.

1. Experience Manager 자산에서 복사한 포함 코드를 웹 페이지에 추가합니다.
복사된 포함 코드는 응답형이므로 페이지의 포함 영역에 자동으로 맞게 조정되어야 합니다.

## 캐러셀 배너를 기존 Quickview와 통합합니다 {#integrating-the-carousel-banner-with-an-existing-quickview}

>[!NOTE]
이 단계는 독립 실행형 Experience Manager Assets 고객인 경우에만 적용됩니다.

이 프로세스의 마지막 단계는 캐러셀 배너를 웹 사이트의 기존 Quickview 구현과 통합하는 것입니다. 모든 Quickview 구현은 고유하며 프런트 엔드 IT 담당자의 지원을 필요로 하는 특정 접근 방식이 필요합니다.

기존 Quickview 구현은 일반적으로 다음 순서로 웹 페이지에서 발생하는 관련 간 작업 체인을 나타냅니다.

1. 사용자가 웹 사이트의 사용자 인터페이스에서 요소를 트리거합니다.
1. 프런트 엔드 코드는 1단계에서 트리거된 사용자 인터페이스 요소를 기반으로 Quickview URL을 가져옵니다.
1. 프런트 엔드 코드는 2단계에서 얻은 URL을 사용하여 Ajax 요청을 보냅니다.
1. 백엔드 로직은 해당 Quickview 데이터 또는 컨텐츠를 다시 프런트 엔드 코드로 반환합니다.
1. 프런트 엔드 코드는 Quickview 데이터 또는 콘텐츠를 로드합니다.
1. 선택적으로, 프런트 엔드 코드는 로드된 Quickview 데이터를 HTML 표현으로 변환합니다.
1. 프런트 엔드 코드는 모달 대화 상자나 패널을 표시하고 최종 사용자를 위해 화면에 HTML 콘텐츠를 렌더링합니다.

이러한 호출은 임의의 단계에서 웹 페이지 로직에서 호출할 수 있는 독립 공용 API 호출을 나타내지 않습니다. 대신, 이전 단계의 마지막 단계(콜백)에서 모든 다음 단계가 숨겨지는 체인 호출입니다.

동시에 회전판 배너가 1단계와 2단계의 일부를 대체하면서 사용자가 회전판 배너의 내부에 핫스팟이나 이미지 맵을 탭하면 이러한 상호 작용은 뷰어에 의해 처리됩니다. 뷰어는 이전에 추가된 모든 핫스팟이나 이미지 맵 데이터를 포함하는 웹 페이지에 이벤트를 반환합니다.

이러한 이벤트 처리기에서 프런트 엔드 코드는 다음을 수행합니다.

* 캐러셀 배너에서 나오는 이벤트를 수신합니다.
* 핫스팟이나 이미지 맵 데이터를 기반으로 Quickview URL을 구성합니다.
* 백엔드에서 Quickview를 로드하고 표시하기 위해 화면에서 렌더링하는 프로세스를 트리거합니다.

Experience Manager 자산에서 반환한 포함 코드에는 이미 주석 처리된 사용 가능한 이벤트 처리기가 있습니다.

따라서 코드의 주석을 해제하고 더미 처리기 본문을 특정 웹 페이지에 해당하는 코드로 대체하기만 하면 됩니다.

Quickview URL을 구성하는 프로세스는 이전에 설명한 핫스팟과 이미지 맵 변수를 식별하는 데 사용되는 프로세스와 반대입니다.

[핫스팟 및 이미지 맵 변수 식별](#identifying-hotspot-and-image-map-variables)을 참조하십시오.

Quickview URL을 트리거하고 Quickview 패널을 활성화하는 마지막 단계는 IT 부서의 프런트 엔드 IT 담당자의 지원이 필요할 수 있습니다. 이들은 사용 준비 중인 Quickview URL을 사용하여 적절한 단계에서 Quickview 구현을 정확하게 트리거하는 방법을 잘 알고 있습니다.

## 빠른 보기를 사용하여 사용자 지정 팝업 만들기 {#using-quickviews-to-create-custom-pop-ups}

[Quickview](/help/assets/custom-pop-ups.md)를 사용하여 사용자 지정 팝업 만들기를 참조하십시오.
