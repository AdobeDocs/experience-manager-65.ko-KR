---
title: 빠른 보기를 사용하여 사용자 지정 팝업 만들기
seo-title: 빠른 보기를 사용하여 사용자 지정 팝업 만들기
description: 기본 Quickview는 전자 상거래 경험에서 사용되어 제품 정보와 함께 팝업이 표시되어 구매를 유도합니다. 사용자 정의 컨텐츠를 트리거하여 팝업에 표시할 수 있습니다.
seo-description: 기본 Quickview는 전자 상거래 경험에서 사용되어 제품 정보와 함께 팝업이 표시되어 구매를 유도합니다. 사용자 정의 컨텐츠를 트리거하여 팝업에 표시할 수 있습니다.
uuid: b906cfff-ac44-4989-b6da-8a9bbf02af03
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 4bcab3f4-500f-432e-b16b-cdc26b9bab4d
feature: 뷰어
role: Business Practitioner, Administrator
exl-id: 4e7f17ea-6985-4644-b91c-2c1299d01321
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 2%

---

# 빠른 보기를 사용하여 사용자 지정 팝업 만들기 {#using-quickviews-to-create-custom-pop-ups}

기본 Quickview는 전자 상거래 경험에서 사용되어 제품 정보와 함께 팝업이 표시되어 구매를 유도합니다. 그러나 사용자 정의 컨텐츠를 트리거하여 팝업에 표시할 수 있습니다. 사용 중인 뷰어에 따라 이 기능을 사용하면 핫스팟이나 축소판 이미지를 클릭하거나 이미지 맵에서 정보나 관련 컨텐츠를 볼 수 있습니다.

빠른 보기는 Dynamic Media의 다음 뷰어에서 지원합니다.

* 대화형 이미지(클릭 가능한 핫스팟)
* 대화형 비디오(비디오 재생 중 클릭 가능한 축소판 이미지)
* 회전 배너(클릭 가능한 핫스팟이나 이미지 맵)

각 뷰어의 기능은 다르지만, 빠른 보기를 만드는 프로세스는 지원되는 세 뷰어 모두에서 동일합니다.

**빠른 보기를 사용하여 사용자 지정 팝업을 만들려면**

1. 업로드된 자산에 대한 빠른 보기를 만듭니다.

   일반적으로 사용 중인 뷰어와 함께 사용할 자산을 편집할 때 빠른 보기를 만듭니다.

   <table>
    <tbody>
    <tr>
    <td><strong>사용 중인 뷰어</strong></td>
    <td><strong>다음 단계를 완료하여 빠른 보기를 만듭니다</strong></td>
    </tr>
    <tr>
    <td>대화형 이미지</td>
    <td><a href="/help/assets/interactive-images.md#adding-hotspots-to-an-image-banner" target="_blank">이미지 배너에 핫스팟 추가</a>.</td>
    </tr>
    <tr>
    <td>대화형 비디오</td>
    <td><a href="/help/assets/interactive-videos.md#adding-interactivity-to-your-video" target="_blank">비디오에 인터랙티브한 추가</a>.</td>
    </tr>
    <tr>
    <td>회전 배너</td>
    <td><a href="/help/assets/carousel-banners.md#adding-hotspots-or-image-maps-to-an-image-banner" target="_blank">배너에 핫스팟 또는 이미지 맵 추가</a>.<br /> </td>
    </tr>
    </tbody>
   </table>

1. 웹 사이트 내에서 뷰어를 통합하기 위한 뷰어 포함 코드 가져오기.

   <table>
    <tbody>
    <tr>
    <td><strong>사용 중인 뷰어</strong><br /> </td>
    <td><strong>다음 단계를 완료하여 뷰어를 웹 사이트와 통합</strong></td>
    </tr>
    <tr>
    <td>대화형 이미지</td>
    <td><a href="/help/assets/interactive-images.md#integrating-an-interactive-image-with-your-website" target="_blank">웹 사이트와 대화형 이미지 통합</a>.<br /> </td>
    </tr>
    <tr>
    <td>대화형 비디오<br /> </td>
    <td><a href="/help/assets/interactive-videos.md#integrating-an-interactive-video-with-your-website" target="_blank">웹 사이트와 대화형 비디오 통합</a>.<br /> </td>
    </tr>
    <tr>
    <td>회전 배너</td>
    <td><a href="/help/assets/carousel-banners.md#adding-a-carousel-banner-to-your-website-page" target="_blank">웹 사이트 페이지에 회전 배너를 추가합니다</a>.<br /> </td>
    </tr>
    </tbody>
   </table>

1. 이제 사용 중인 뷰어는 빠른 보기를 사용하는 방법을 알아야 합니다.

   이렇게 하려면 뷰어가 `QuickViewActive` 이라는 핸들러를 사용합니다.

   ****
예: 대화형 이미지에 웹 페이지에서 다음 샘플 포함 코드를 사용했다고 가정해 봅시다.

   ![chlimage_1-291](assets/chlimage_1-291.png)

   처리기가 `setHandlers` 을 사용하여 뷰어에 로드됩니다.

   `*viewerInstance*.setHandlers({ *handler 1*, *handler 2*}, ...`

   **위의 샘플 포함 코드 예제를 사용하여 다음 코드가 있습니다.**

   ```xml
   s7interactiveimageviewer.setHandlers({
       quickViewActivate": function(inData) {
           var sku=inData.sku;
           var genericVariable1=inData.genericVariable1;
           var genericVariable2=inData.genericVariable2;
          loadQuickView(sku,genericVariable1,genericVariable2);
       }
   })
   ```

   다음 위치에서 `setHandlers()` 메서드에 대해 자세히 알아보십시오.

   * 대화형 이미지 뷰어:[https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-sethandlers.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-sethandlers.html)
   * 대화형 비디오 뷰어:[https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-sethandlers.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-sethandlers.html)

1. 이제 `quickViewActivate` 처리기를 구성해야 합니다.

   `quickViewActivate` 처리기는 뷰어의 빠른 보기를 제어합니다. 처리기에는 Quickview에 사용할 변수 목록과 함수 호출이 포함되어 있습니다. 포함 코드는 Quickview에 설정된 SKU 변수와 샘플 `loadQuickView` 함수 호출에 대한 매핑을 제공합니다.

   **웹**
페이지에서 사용할 변수 mappingMap 변수를 SKU 값 및 Quickview에 포함된 일반 변수에 매핑합니다.

   `var *variable1*= inData.*quickviewVariable*`

   제공된 포함 코드에는 SKU 변수에 대한 샘플 매핑이 있습니다.

   `var sku=inData.sku`

   다음과 같이 Quickview의 추가 변수도 매핑합니다.

   ```
   var <i>variable2</i>= inData.<i>quickviewVariable2</i>
    var <i>variable3</i>= inData.<i>quickviewVariable3</i>
   ```

   **함수**
호출Quickview가 작동하려면 처리기에 함수 호출이 필요합니다. 함수는 호스트 페이지에서 액세스할 수 있다고 가정합니다. 포함 코드는 샘플 함수 호출을 제공합니다.

   `loadQuickView(sku)`

   샘플 함수 호출에서는 함수 `loadQuickView()`이 존재하며 액세스할 수 있다고 가정합니다.

   다음 위치에서 `quickViewActivate` 메서드에 대해 자세히 알아보십시오.

   * 대화형 이미지 뷰어:[https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-event-callbacks.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-event-callbacks.html)
   * 대화형 비디오 뷰어:[https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-event-callbacks.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-event-callbacks.html)
   * 대화형 비디오 뷰어에서 대화형 데이터 지원:[https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-int-data-support.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-int-data-support.html)

1. 다음을 수행합니다.

   * 포함 코드의 setHandlers 섹션의 주석을 해제합니다.
   * Quickview에 포함된 모든 추가 변수를 매핑합니다.

      * 추가 변수를 추가할 경우 `loadQuickView(sku,*var1*,*var2*)` 호출을 업데이트합니다.
   * 뷰어 외부의 페이지에서 간단한 `loadQuickView` () 함수를 만듭니다.

      예를 들어, 다음은 sku 값을 브라우저 콘솔에 씁니다.

   ```xml
   function loadQuickView(sku){
       console.log ("quickview sku value is " + sku);
   }
   ```

   * 테스트 HTML 페이지를 웹 서버에 업로드하고 엽니다.

      Quickview의 변수가 매핑되고 함수 호출이 배치되면 브라우저 콘솔은 제공된 샘플 함수를 사용하여 브라우저 콘솔에 변수 값을 기록합니다.



1. 이제 함수를 사용하여 Quickview에서 간단한 팝업을 호출할 수 있습니다. 다음 예제에서는 팝업에 `DIV`을 사용합니다.
1. 팝업 `DIV` 스타일을 다음과 같은 방식으로 지정합니다. 원하는 대로 자신만의 스타일을 추가합니다.

   ```xml
   <style type="text/css">
       #quickview_div{
           position: absolute;
           z-index: 99999999;
           display: none;
       }
   </style>
   ```

1. 팝업 `DIV`을 HTML 페이지의 본문에 배치합니다.

   요소 중 하나는 사용자가 Quickview를 호출할 때 sku 값으로 업데이트된 ID로 설정됩니다. 또한 팝업이 표시된 후 팝업을 다시 숨기기 위한 간단한 단추도 포함되어 있습니다.

   ```xml
   <div id="quickview_div" >
       <table>
           <tr><td><input id="btnClosePopup" type="button" value="Close"        onclick='document.getElementById("quickview_div").style.display="none"' /><br /></td></tr>
           <tr><td>SKU</td><td><input type="text" id="txtSku" name="txtSku"></td></tr>
       </table>
   </div>
   ```

1. 팝업에서 sku 값을 업데이트하는 함수를 추가합니다.5단계에서 만든 단순 함수를 대체하여 팝업을 표시합니다. 사용:

   ```xml
   <script type="text/javascript">
       function loadQuickView(sku){
           document.getElementById("txtSku").setAttribute("value",sku); // write sku value
           document.getElementById("quickview_div").style.display="block"; // show popup
       }
   </script>
   ```

1. 테스트 HTML 페이지를 웹 서버에 업로드하고 엽니다. 사용자가 Quickview를 호출하면 뷰어에 팝업 `DIV`이 표시됩니다.
1. **전체 화면 모드로 사용자 지정 팝업을 표시하는 방법**

   대화형 비디오 뷰어와 같은 일부 뷰어는 전체 화면 모드로 표시를 지원합니다. 그러나 이전 단계에서 설명한 대로 팝업을 사용하면 전체 화면 모드에 있는 동안 뷰어 뒤에 표시됩니다.

   팝업을 표준 모드와 전체 화면 모드 모두에서 표시하려면 팝업을 뷰어 컨테이너에 첨부합니다. 이를 위해 두 번째 처리기 메서드인 `initComplete`를 사용할 수 있습니다.

   뷰어가 초기화되면 `initComplete` 핸더가 호출됩니다.

   ```xml
   "initComplete":function() { code block }
   ```

   다음 위치에서 `init()` 메서드에 대해 자세히 알아보십시오.

   * 대화형 이미지 뷰어:[https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-init.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-init.html)
   * 대화형 비디오 뷰어:[https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-init.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-init.html)

1. 이전 단계에서 설명한 팝업을 뷰어에 연결하려면 다음 코드를 사용하십시오.

   ```xml
   "initComplete":function() {
       var popup = document.getElementById('quickview_div');
       popup.parentNode.removeChild(popup);
       var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId();
       var inner_container = document.getElementById(sdkContainerId);
       inner_container.appendChild(popup);
   }
   ```

   위의 코드에서 다음을 수행했습니다.

   * 사용자 지정 팝업을 확인했습니다.
   * DOM에서 제거했습니다.
   * 뷰어 컨테이너를 식별했습니다.
   * 뷰어 컨테이너에 팝업을 첨부했습니다.

1. 이제 전체 setHandlers 코드는 다음과 유사해야 합니다(대화형 비디오 뷰어가 사용됨).

   ```xml
   s7interactivevideoviewer.setHandlers({
       "quickViewActivate": function(inData) {
           var sku=inData.sku;
           loadQuickView(sku);
   
       },
       "initComplete":function() {
           var popup = document.getElementById('quickview_div'); // get custom quick view container
           popup.parentNode.removeChild(popup); // remove it from current DOM
           var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId();
           var inner_container = document.getElementById(sdkContainerId);
           inner_container.appendChild(popup);
       }
   });
   ```

1. 핸들러가 로드되면 뷰어를 초기화합니다.

   `*viewerInstance.*init()`

   ****
예제 이 예제에서는 대화형 이미지 뷰어를 사용합니다.

   `s7interactiveimageviewer.init()`

   뷰어를 호스트 페이지에 포함시킨 후에는 뷰어 인스턴스가 생성되어 뷰어가 호출되기 전에 `init()` 처리기를 로드해야 합니다.
