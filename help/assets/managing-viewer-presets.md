---
title: 뷰어 사전 설정 관리
description: Dynamic Media에서 뷰어 사전 설정을 생성, 편집 및 관리하는 방법.
uuid: 64fcf16a-7c4a-435b-bf1a-f27b8b39a715
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: cf7823f4-82c2-4e36-9b65-3c58359b8104
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/dynamic-media/viewer-presets
feature: 뷰어 사전 설정
role: User, Admin
exl-id: 0899e497-88e9-4fc3-a6be-b3a149fb5b32
source-git-commit: 363e5159d290ecfbf4338f6b9793e11b613389a5
workflow-type: tm+mt
source-wordcount: '4334'
ht-degree: 1%

---

# 뷰어 사전 설정 관리{#managing-viewer-presets}

뷰어 사전 설정은 사용자가 컴퓨터 화면과 모바일 장치에서 리치 미디어 자산을 보는 방법을 결정하는 설정 모음입니다. 관리자는 뷰어 사전 설정을 만들 수 있습니다. 설정은 뷰어 구성 옵션 배열에 사용할 수 있습니다. 예를 들어 뷰어 표시 크기 또는 확대/축소 동작을 변경할 수 있습니다.

고유한 HTML5 뷰어 사전 설정을 만들고 사용자 지정하는 방법에 대한 지침은 Dynamic Media Adobe *HTML5 Viewer SDK API 설명서*&#x200B;를 참조하십시오. SDK는 SDK 자체에 포함된 IS 게시 서버에서 사용할 수 있습니다. 각 라이브러리 버전에는 자체 SDK 설명서가 포함되어 있습니다.

경로: `<scene7_domain>/s7sdk/<library_version>/docs/jsdocs/index.html`.\
예: 3.10 SDK: [https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html](https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html)

또한 [Adobe Dynamic Media 뷰어 참조 안내서](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html)를 참조하십시오.

이 섹션에서는 뷰어 사전 설정을 만들고, 편집하고, 관리하는 방법을 설명합니다. 미리 볼 때 언제든지 자산에 뷰어 사전 설정을 적용할 수 있습니다. [뷰어 사전 설정 적용](#applying-a-viewer-preset-to-an-asset)을 참조하십시오.

>[!NOTE]
>
>사전 정의된 기본 제공 뷰어 사전 설정&#x200B;*을 편집하는 것은 지원되는 시나리오가 아닙니다.* 기본 뷰어 사전 설정을 편집하려고 하면 새 이름을 사용하여 뷰어 사전 설정을 저장하라는 메시지가 표시됩니다.

## 뷰어의 키보드 액세스 가능성 {#keyboard-accessibility-for-viewers}

모든 기본 뷰어는 키보드 액세스 가능성을 지원합니다.

[키보드 액세스 가능성 및 탐색](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html)도 참조하십시오.

## 뷰어 사전 설정 관리 {#managing-viewer-presets-1}

**[!UICONTROL 도구]** (망치 아이콘) > **[!UICONTROL 자산]** > **[!UICONTROL 뷰어 사전 설정]**&#x200B;을 탭하여 Adobe Experience Manager에서 뷰어 사전 설정을 추가, 편집, 삭제, 게시, 게시 취소 및 미리 볼 수 있습니다.

![6_5_tools-assets-viewerpresets](assets/6_5_tools-assets-viewerpresets.png)

>[!NOTE]
>
>기본적으로 자산의 세부 사항 보기에서 뷰어 를 선택하면 시스템에 15개의 뷰어 사전 설정이 표시됩니다. 이 제한을 늘릴 수 있습니다. [표시되는 뷰어 사전 설정 수를 늘립니다](#increasing-the-number-of-viewer-presets-that-display).

### 반응형 디자인 웹 페이지에 대한 뷰어 지원 {#viewer-support-for-responsive-designed-web-pages}

웹 페이지마다 요구 사항이 다릅니다. 예를 들어, 별도의 브라우저 창에서 HTML5 뷰어를 여는 링크를 제공하는 웹 페이지를 원하는 경우가 있습니다. 다른 경우 HTML5 뷰어를 호스팅 페이지에 직접 포함해야 할 수도 있습니다. 후자의 경우 웹 페이지에 정적 레이아웃이 있을 수 있습니다. 또는 &quot;응답형&quot;일 수 있으며 다른 장치 또는 다른 브라우저 창 크기에 대해 다르게 표시될 수 있습니다. 이러한 요구 사항을 수용하기 위해 Dynamic Media과 함께 제공되는 사전 정의된 모든 기본 제공 HTML5 뷰어는 정적 웹 페이지와 응답형 디자인 웹 페이지를 모두 지원합니다.

웹 페이지에 응답형 뷰어를 포함하는 방법에 대한 자세한 내용은 [응답형 이미지 라이브러리](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/responsive-static-image-library/c-about-responsive-static-image-library.html) 를 참조하십시오.

>[!NOTE]
>
>처음 사용하기 전에 모든 기본 제공 뷰어를 게시해야 합니다.
>[뷰어 사전 설정 게시]를 참조하십시오.(#publishing-viewer-presets)

### 뷰어 사전 설정 시스템 호환성 {#viewer-preset-system-compatibility}

Dynamic Media과 함께 제공되는 모든 기본 뷰어 사전 설정은 다음 시스템과 완전히 호환됩니다.

* 데스크톱
* Apple iPhone
* Apple iPad
* Android™ Smartphone
* Android™ 태블릿
* 비디오의 경우 [BlackBerry®](https://developer.blackberry.com/devzone/develop/supported_media/bb_media_support_at_a_glance.html#kba1328730952678) 및 [Windows Phone](https://docs.microsoft.com/en-us/windows/uwp/audio-video-camera/supported-codecs)에 대해 MP4 재생에 대한 추가 지원이 제공됩니다.

### 뷰어 사전 설정에 대한 리치 미디어 유형 {#rich-media-types-for-viewer-presets}

관리자는 뷰어 사전 설정을 만들 때 다음의 리치 미디어 유형을 추가하고 사용자 지정할 수 있습니다.

<table>
 <tbody>
  <tr>
   <td><strong>회전 메뉴 세트</strong><br /> </td>
   <td><p>핫스팟이나 이미지 맵 또는 둘 다 둘 이상의 이미지에 추가됩니다. 고객은 이미지를 왼쪽 또는 오른쪽으로 팬한 다음 이미지에 있는 핫스팟을 선택하여 추가 세부 사항을 확인하거나 웹 사이트의 카테고리, 홈 또는 랜딩 페이지에서 직접 구매할 수 있습니다.</p> </td>
  </tr>
  <tr>
   <td><strong>차원</strong><br /> </td>
   <td><p>카메라를 회전, 이동, 확대/축소 또는 재입력할 수 있는 3D 장면을 표시합니다.</p> </td>
  </tr>
  <tr>
   <td><strong>플라이아웃 확대/축소</strong></td>
   <td><p>원본 이미지 옆에 확대/축소된 영역의 두 번째 이미지를 표시합니다. 사용할 컨트롤이 없습니다. 사용자가 원하는 영역으로 선택 영역을 이동합니다.</p> <p>이 뷰어에 대한 전체 대역폭 사용을 결정할 때 기본 이미지와 플라이아웃 이미지가 모두 뷰어에서 제공되는지 고려하십시오. 기본 이미지 크기(스테이지 너비 및 높이)와 확대/축소 인수가 플라이아웃 이미지 크기를 결정합니다. 플라이아웃 파일 크기가 너무 크지 않도록 하려면 다음 두 값의 균형을 맞춥니다. 주 이미지 크기가 큰 경우 확대/축소 계수 값을 낮춥니다. (플라이아웃 폭 및 플라이아웃 높이 는 플라이아웃 창의 크기를 결정하지만 뷰어에 제공되는 플라이아웃 이미지의 크기는 결정합니다.)</p> <p>예를 들어 기본 이미지 크기가 350 x 350 픽셀이고 확대/축소 인수가 3인 경우 결과 플라이아웃 이미지는 1050 x 1050 픽셀입니다. 기본 이미지 크기가 300 x 300 픽셀이고 확대/축소 인수가 4인 경우 플라이아웃 이미지는 1200 x 1200 픽셀입니다. JPEG 품질 설정(권장 설정은 80~90 사이)에 따라 파일 크기를 크게 줄일 수 있습니다. 권장되는 확대/축소 요소는 기본 이미지의 크기에 따라 2.5~4입니다.</p> </td>
  </tr>
  <tr>
   <td><strong>인라인 확대/축소</strong></td>
   <td>원래 뷰어 내에서 확대/축소된 영역의 이미지를 표시합니다. 사용할 컨트롤이 없습니다. 즉, 사용자가 보려는 영역으로 선택 영역을 이동합니다.</td>
  </tr>
  <tr>
   <td><strong>이미지 집합</strong></td>
   <td>이미지 세트 뷰어에서는 축소판 이미지를 선택하여 항목의 다른 보기 또는 색상 변형을 볼 수 있습니다. 또한 이 뷰어는 이미지를 자세히 검사할 수 있는 확대/축소 도구를 제공합니다.</td>
  </tr>
  <tr>
   <td><strong>대화형 이미지</strong></td>
   <td>핫스팟은 고객이 추가 세부 사항을 위해 선택하거나 웹 사이트의 카테고리, 홈 또는 랜딩 페이지에서 직접 구매할 수 있는 이미지의 일부에 추가됩니다.</td>
  </tr>
  <tr>
   <td><strong>대화형 비디오</strong></td>
   <td>미리 보기는 고객이 추가 세부 사항을 위해 선택하거나 웹 사이트의 카테고리, 홈 또는 랜딩 페이지에서 직접 구매할 수 있는 비디오의 타임라인 세그먼트에 추가됩니다.</td>
  </tr>
  <tr>
   <td><strong>혼합 미디어</strong></td>
   <td>한 뷰어에 다른 유형의 미디어를 표시합니다. 스핀 세트, 이미지 세트, 이미지 및 비디오를 포함할 수 있습니다.</td>
  </tr>
  <tr>
   <td><strong>파노라마 이미지</strong></td>
   <td><p>파노라마 이미지 및 PanoramicVR 뷰어는 공간, 속성, 위치 또는 조경에 대한 360° 보기 환경에서 사용자를 몰입하도록 구형 파노라마 이미지를 렌더링합니다.</p> <p>업로드된 이미지가 구형 파노라마를 사용할 수 있도록 하려면 다음 중 하나 또는 둘 다 있어야 합니다.</p>
    <ul>
     <li>2:1 종횡비입니다.</li>
     <li><code>equirectangular</code>, <code>spherical</code> 및 <code>panorama</code>, 또는 <code>spherical </code>와 <code>panoramic</code> 키워드가 태그되었습니다. <a href="/help/sites-authoring/tags.md">태그 사용</a>을 참조하십시오.</li>
    </ul> <p>종횡비와 키워드 기준은 모두 자산 세부 사항 페이지와 "파노라마 미디어" WCM 구성 요소의 파노라마 자산에 적용됩니다.</p> <p><strong>중요</strong>: 이 뷰어는 Dynamic Media - Scene7 모드에서만 사용할 수 있습니다.</p> </td>
  </tr>
  <tr>
   <td><strong>스마트 크롭 비디오</strong><br /> </td>
   <td><p>이 뷰어를 사용하여 비디오의 초점을 자동으로 감지하고 자릅니다.</p> </td>
  </tr>
  <tr>
   <td><strong>회전 집합</strong></td>
   <td>여러 이미지 뷰를 제공하여 개체를 돌려 다른 면과 각도를 검사할 수 있습니다.</td>
  </tr>
  <tr>
   <td><strong>360 비디오</strong></td>
   <td><p>360/VR Video 뷰어를 사용하여 방, 속성, 위치, 가로 또는 의료 과정에서 몰입형 시청 환경을 위해 필요한 사각형 비디오를 렌더링합니다.</p> <p>평면 디스플레이에서 재생 중에 사용자는 보기 각도를 제어할 수 있습니다. 모바일 장치에서 재생은 일반적으로 내장된 회전 제어 기능을 적용합니다.</p> <p>뷰어에는 360개의 비디오 자산 전달에 대한 기본 지원이 포함되어 있습니다. 기본적으로 보거나 재생하는 데 추가 구성이 필요하지 않습니다. .mp4, .mkv 및 .mov와 같은 표준 비디오 확장 기능을 사용하여 360 비디오를 제공합니다. 가장 일반적인 코덱은 H.264입니다.</p> <p><strong>중요</strong>: 이 뷰어는 Dynamic Media - Scene7 모드에서만 사용할 수 있습니다.</p> </td>
  </tr>
  <tr>
   <td><strong>비디오</strong></td>
   <td><p>점진적 또는 적응형 비트율 스트리밍을 사용하여 비디오를 재생합니다. 적응형 비트율 스트리밍은 장치 및 대역폭 검색을 자동으로 수행하여 적합한 품질의 비디오를 적합한 형식으로 제공합니다.</p> </td>
  </tr>
  <tr>
   <td><strong>세로 확대/축소</strong></td>
   <td><p>세로 확대/축소 뷰어를 사용하면 제품 이미지 보기 경험을 최대화하여 사용자에게 제품에 대한 최상의 표현을 제공할 수 있습니다. 색상 견본의 수직 위치는 다음과 같습니다.</p>
    <ul>
     <li>견본이 "접힌 부분 위"에 있는지 확인합니다.<br/> 가로 색상 견본을 사용하면 사용자의 데스크탑 화면 크기에 따라 사용자가 페이지를 스크롤할 때까지 표시되지 않습니다. 뷰어에 색상 견본을 세로로 배치하면 사용자의 화면 크기에 상관없이 표시될 수 있습니다.</li>
     <li>기본 이미지 크기를 극대화합니다.<br /> 가로 색상 견본을 사용하면 페이지가 표시되도록 페이지의 공간을 예약해야 합니다. 이 위치 지정은 주 이미지의 크기를 줄였습니다. 그러나 세로 견본 레이아웃이 있으면 이 공간을 할당할 필요가 없습니다. 따라서 주 이미지 크기를 최대화할 수 있습니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>확대/축소</strong></td>
   <td>사용자가 영역을 선택하여 확대할 수 있습니다. 사용자는 컨트롤을 선택하여 이미지를 확대, 축소 및 기본 크기로 재설정할 수 있습니다.</td>
  </tr>
 </tbody>
</table>

### 즉시 사용 가능한 뷰어 사전 설정 목록 {#list-of-out-of-the-box-viewer-presets}

다음 표는 Dynamic Media과 함께 제공되는 사전 정의된 모든 즉시 사용 가능한 뷰어 사전 설정을 식별합니다.

[라이브 데모](https://landing.adobe.com/en/na/dynamic-media/ctir-2755/live-demos.html)도 참조하십시오.

뷰어를 위해 지원되는 웹 브라우저 및 운영 체제 버전에 대한 자세한 내용은 뷰어 릴리스 노트를 검토할 수 있습니다.

[뷰어 참조 안내서](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html)의 목차&quot;뷰어 릴리스 노트&quot;를 참조하십시오.

>[!NOTE]
>
>Dynamic Media의 모든 기본 뷰어 사전 설정이 이미 활성화(켜짐)되었지만 게시해야 합니다.
>[뷰어 사전 설정 게시](#publishing-viewer-presets)를 참조하십시오.
>
>만들고 추가하는 모든 새 뷰어 사전 설정은 활성화 *와 *게시되어야 합니다.
>[뷰어 사전 설정 활성화 또는 비활성화](#activating-or-deactivating-viewer-presets) 및 [뷰어 사전 설정 게시](#publishing-viewer-presets)를 참조하십시오.

<table>
 <tbody>
  <tr>
   <td><strong>뷰어 사전 설정 제목</strong></td>
   <td><strong>유형</strong></td>
   <td><strong>CSS 파일 이름</strong><br /> </td>
  </tr>
  <tr>
   <td>회전판_점선_어둡게</td>
   <td>회전판_설정</td>
   <td><code>html5_carouselviewer_dotted_dark.css</code></td>
  </tr>
  <tr>
   <td>회전판_점선_조명</td>
   <td>회전판_설정</td>
   <td><code>html5_carouselviewer_dotted_light.css</code></td>
  </tr>
  <tr>
   <td>회전판_Numeric_dark</td>
   <td>회전판_설정</td>
   <td><code>html5_carouselviewer_numeric_dark.css</code></td>
  </tr>
  <tr>
   <td>회전판_숫자_라이트</td>
   <td>회전판_설정</td>
   <td><code>html5_carouselviewer_numeric_light.css</code></td>
  </tr>
  <tr>
   <td>차원</td>
   <td>차원</td>
   <td><code>html5_dimensionalviewer.css</code></td>
  </tr>
  <tr>
   <td>플라이아웃</td>
   <td>Flyout_Zoom</td>
   <td><code>html5_flyoutviewer.css</code></td>
  </tr>
  <tr>
   <td>ImageSet_dark</td>
   <td>이미지 집합</td>
   <td><code>html5_zoomviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>ImageSet_light</td>
   <td>이미지 집합</td>
   <td><code>html5_zoomviewer_light.css</code></td>
  </tr>
  <tr>
   <td>InlineMixedMedia_dark</td>
   <td>Mixed_Media</td>
   <td><code>html5_inlinemixedmediaviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>InlineMixedMedia_light</td>
   <td>Mixed_Media</td>
   <td><code>html5_inlinemixedmediaviewer_light.css</code></td>
  </tr>
  <tr>
   <td>인라인 확대/축소</td>
   <td>Flyout_Zoom</td>
   <td><code>html5_inlinezoomviewer.css</code></td>
  </tr>
  <tr>
   <td>MixedMedia_dark</td>
   <td>Mixed_Media</td>
   <td><code>html5_mixedmediaviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>MixedMedia_light</td>
   <td>Mixed_Media</td>
   <td><code>html5_mixedmediaviewer_light.css</code></td>
  </tr>
  <tr>
   <td>파노라마 이미지</td>
   <td>Panoric_Image</td>
   <td><code>html5_panoramicimage.css</code></td>
  </tr>
  <tr>
   <td>PanoricImageVR</td>
   <td>Panoric_Image</td>
   <td><code>html5_panoramicimage.css</code></td>
  </tr>
  <tr>
   <td>Shopperable_Banner</td>
   <td>Interactive_Image</td>
   <td><code>html5_interactiveimage.css</code></td>
  </tr>
  <tr>
   <td>Shopperable_Video_dark</td>
   <td>Interactive_Video</td>
   <td><code>html5_interactivevideoviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>Shoppable_Video_light</td>
   <td>Interactive_Video</td>
   <td><code>html5_interactivevideovewer_light.css</code></td>
  </tr>
  <tr>
   <td>SmartCropVideo</td>
   <td>Smart_Crop_Video</td>
   <td><code>html5_smartcropvideoviewer.css</code></td>
  </tr>
  <tr>
   <td>SmartCropVideo_social</td>
   <td>Smart_Crop_Video</td>
   <td><code>html5_smartcropvideoviewersocial.css</code></td>
  </tr>
  <tr>
   <td>SpinSet_dark</td>
   <td>Spin_Set</td>
   <td><code>html5_spinviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>SpinSet_light</td>
   <td>Spin_Set</td>
   <td><code>html5_spinviewer_light.css</code></td>
  </tr>
  <tr>
   <td><p>비디오</p> <p>(자막 지원 포함)</p> </td>
   <td>비디오</td>
   <td><code>html5_videoviewer.css</code></td>
  </tr>
  <tr>
   <td><p>비디오360_social</p> <p>( 기본 비디오 재생 제어, 비디오 렌더링은 스테레오 모드로 수행되고, 수동 POV 제어는 꺼져 있지만 회전 제어 기능이 켜져 있고 소셜 미디어 기능이 없음)</p> </td>
   <td>Video_360</td>
   <td><code>html5_video360viewersocial.css</code></td>
  </tr>
  <tr>
   <td><p>Video360VR</p> <p>(가상 현실 안경을 사용하는 최종 사용자를 위해 설계되었습니다. 기본 비디오 재생 제어 및 소셜 미디어 기능 포함)</p> </td>
   <td>Video_360</td>
   <td><code>html5_video360viewer.css</code></td>
  </tr>
  <tr>
   <td><p>Video_social</p> <p>(자막 및 소셜 미디어 지원 포함)</p> </td>
   <td>비디오</td>
   <td><code>html5_videoviewersocial.css</code></td>
  </tr>
  <tr>
   <td>Zoom_dark<br /> </td>
   <td>확대/축소<br /> </td>
   <td><code>html5_basiczoomviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>Zoom_light<br /> </td>
   <td>확대/축소</td>
   <td><code>html5_basiczoomviewer_light.css</code></td>
  </tr>
  <tr>
   <td>ZoomVertical_dark<br /> </td>
   <td>Vertical_Zoom</td>
   <td><code>html5_zoomverticalviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>ZoomVertical_light</td>
   <td>Vertical_Zoom</td>
   <td><code>html5_zoomverticalviewer_light.css</code></td>
  </tr>
 </tbody>
</table>

### 지원되는 모바일 뷰어 제스처 매트릭스 {#supported-mobile-viewers-gestures-matrix}

다음 표는 iOS, Android™ 2.x 및 Android™ 3.x 장치에서 지원되는 모바일 뷰어 제스처를 식별합니다.

<table>
 <tbody>
  <tr>
   <td><strong>제스처</strong></td>
   <td><strong>플라이아웃 확대/축소</strong></td>
   <td><strong>확대/축소</strong></td>
   <td><strong>회전</strong></td>
  </tr>
  <tr>
   <td><p><strong>드래그</strong></p> </td>
   <td><p>팬</p> </td>
   <td><p>팬</p> </td>
   <td><p>팬</p> </td>
  </tr>
  <tr>
   <td><p><strong>선택</strong></p> </td>
   <td><p>플라이아웃 창을 표시합니다.</p> </td>
   <td><p>사용자 인터페이스를 표시하거나 숨깁니다.</p> </td>
   <td><p>사용자 인터페이스를 표시하거나 숨깁니다.</p> </td>
  </tr>
  <tr>
   <td><p><strong>두 번 탭</strong></p> </td>
   <td><p>적용되지 않음</p> </td>
   <td><p>확대 또는 재설정</p> </td>
   <td><p>확대 또는 재설정</p> </td>
  </tr>
  <tr>
   <td><p><strong>핀치 열기</strong></p> </td>
   <td><p>적용되지 않음</p> </td>
   <td><p>확대(iOS 및 Android™ 3x만 해당)</p> </td>
   <td><p>확대(iOS 및 Android™ 3x만 해당)</p> </td>
  </tr>
  <tr>
   <td><p><strong>핀치 닫기</strong></p> </td>
   <td><p>적용되지 않음</p> </td>
   <td><p>축소(iOS 및 Android™ 3x만 해당)</p> </td>
   <td><p>축소(iOS 및 Android™ 3x만 해당)</p> </td>
  </tr>
  <tr>
   <td><p><strong>밀기</strong></p> </td>
   <td><p>견본 막대 스크롤</p> </td>
   <td><p>이미지 스크롤</p> </td>
   <td><p>회전</p> </td>
  </tr>
  <tr>
   <td><p><strong>플릭</strong></p> </td>
   <td><p>견본 막대 스크롤</p> </td>
   <td><p>이미지 스크롤</p> </td>
   <td><p>회전</p> </td>
  </tr>
 </tbody>
</table>

## 표시되는 뷰어 사전 설정 수를 늘립니다 {#increasing-the-number-of-viewer-presets-that-display}

Experience Manager은 **[!UICONTROL 세부 사항 보기]** > **[!UICONTROL 뷰어]**&#x200B;에서 자산을 볼 때 광범위한 뷰어 사전 설정을 표시합니다. 표시되는 뷰어 수를 늘리거나 줄일 수 있습니다.

**표시되는 뷰어 사전 설정 수를 늘립니다.**

1. CRXDE Lite([https://localhost:4502/crx/de](https://localhost:4502/crx/de))로 이동합니다.
1. 다음 위치에서 뷰어 사전 설정 목록 노드로 이동합니다.

   `/libs/dam/gui/coral/content/commons/sidepanels/viewerpresets/viewerpresetslist`

   ![chlimage_1-221](assets/chlimage_1-221.png)

1. **[!UICONTROL limit]** 속성에서 기본적으로 15로 설정된 **[!UICONTROL 값]**&#x200B;을 원하는 숫자로 변경합니다.
1. `/libs/dam/gui/coral/content/commons/sidepanels/viewerpresets/viewerpresetslist/datasource`의 뷰어 사전 설정 데이터 소스로 이동합니다.

   ![chlimage_1-222](assets/chlimage_1-222.png)

1. limit 속성에서 숫자를 원하는 숫자(예: `{empty requestPathInfo.selectors[1] ? "20" : requestPathInfo.selectors[1]}`)로 변경합니다.
1. **[!UICONTROL 모두 저장]**&#x200B;을 선택합니다.

## 뷰어 사전 설정 만들기 {#creating-a-new-viewer-preset}

뷰어 사전 설정을 만들면 자산을 보고 상호 작용하는 다양한 설정을 적용할 수 있습니다. 그러나 뷰어 사전 설정을 만들 필요는 없습니다. 원할 경우 AEM Assets에 이미 제공되는 기본 기본 기본 기본 기본 기본 제공 뷰어 사전 설정을 사용할 수 있습니다.

뷰어 사전 설정을 만들도록 선택하는 경우, 저장한 후 뷰어 사전 설정 페이지에서 뷰어 상태가 자동으로 활성화(**[!UICONTROL On]**&#x200B;로 설정)됩니다. 이 상태는 Dynamic Media 구성 요소 및 대화형 미디어 구성 요소에 표시되고 이미지나 비디오를 미리 볼 때마다 표시됩니다.

일부 뷰어 사전 설정에는 뷰어의 사용 및 전체 동작에 영향을 줄 수 있는 전용 설정이 있습니다. 만드는 뷰어 사전 설정에 따라 이러한 특별한 고려 사항을 알고 싶을 수 있습니다.

[대화형 뷰어 사전 설정을 만들기 위한 특수 고려 사항](#special-considerations-for-creating-an-interactive-viewer-preset)을 참조하십시오.

[캐러셀 배너 뷰어 사전 설정을 만들기 위한 특별한 고려 사항](#special-considerations-for-creating-a-carousel-banner-viewer-preset)을 참조하십시오.

**뷰어 사전 설정을 만들려면:**

1. Experience Manager의 왼쪽 위 모서리에서 Experience Manager 로고를 선택한 다음 왼쪽 레일에서 **[!UICONTROL 도구]**(망치 아이콘) > **[!UICONTROL 자산] > [!UICONTROL 뷰어 사전 설정]**&#x200B;을 선택합니다.

   ![6_5_viewerpresets](assets/6_5_viewerpresets.png)

1. 뷰어 사전 설정 페이지의 도구 모음에서 **[!UICONTROL 만들기]**&#x200B;를 선택합니다.
1. **[!UICONTROL 새 뷰어 사전 설정]** 대화 상자의 **[!UICONTROL 사전 설정 이름]** 필드에 새 사전 설정의 이름을 입력합니다. 이름을 신중하게 선택합니다. **[!UICONTROL 만들기]**&#x200B;를 선택한 후에는 편집할 수 없습니다.

   이 단계의 나중에 사전 설정을 저장하면 해당 이름이 사전 설정 제목 열 헤더 아래의 뷰어 사전 설정 페이지에 표시됩니다.

1. 리치 미디어 유형 드롭다운 메뉴에서 만들려는 뷰어 사전 설정 유형을 선택한 다음 페이지의 오른쪽 상단 모서리에서 **[!UICONTROL 만들기]**&#x200B;를 선택합니다.

   뷰어 사전 설정에 대한 [리치 미디어 유형](#rich-media-types-for-viewer-presets)을 참조하십시오.

1. 뷰어 사전 설정 편집기 페이지에서 **[!UICONTROL 모양]** 탭을 선택합니다.
1. 다음 중 하나를 수행하십시오.

   * **[!UICONTROL 선택한 유형]** 풀다운 메뉴에서 시각적 디자인을 사용자 지정할 구성 요소를 선택합니다. 또는 뷰어에서 시각적 요소를 선택하여 구성에 대해 선택할 수 있습니다.

      시각적 편집기를 사용하면 특정 속성이 스타일에 어떤 영향을 주는지 확인할 수 있습니다. 속성을 설정하거나 조정하여 편집기의 왼쪽에 있는 샘플을 사용하여 뷰어에 미치는 영향을 즉시 확인할 수 있습니다.

      각 뷰어 사전 설정 유형에 대한 CSS 스타일 속성은 [뷰어 참조 안내서](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html)의 &quot;Customizing *`<viewer name>`* Viewer&quot; 도움말 항목에 설명되어 있습니다. 예를 들어 `Mixed_Media` 유형의 뷰어 사전 설정을 만드는 경우 각 속성의 목록 및 설명은 [혼합 미디어 뷰어 사용자 정의](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/mixed-media/customing-mixed-media/c-html5-mixedmedia-viewer-customizingviewer.html) 를 참조하십시오.

   * 별도의 CSS 파일에서 스타일 설정을 정의한 경우 CSS 파일을 AEM Assets에 업로드할 수 있습니다. 업로드된 CSS 파일을 찾아 뷰어 사전 설정과 연결할 수 있도록 **[!UICONTROL 선택한 유형]** 풀다운 메뉴 아래에서 **[!UICONTROL CSS 가져오기]**&#x200B;를 선택합니다(필요한 경우 시각적 편집기를 위로 스크롤하여 표시).

      CSS 파일을 가져올 때 시각적 편집기는 CSS가 올바른 뷰어 마커를 사용하는지 확인합니다. 예를 들어, 확대/축소 뷰어를 만드는 경우 가져오는 모든 CSS 규칙은 상위 뷰어 요소에 정의된 해당 뷰어 클래스 이름 `.s7mixedmediaviewer` 을 사용하여 정의해야 합니다.

      지정된 뷰어에 대한 CSS 마커를 적절히 정의하는 한 임의의 수제 CSS를 가져올 수 있습니다. (CSS 마커는 [뷰어 참조 안내서](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html)의 &quot;사용자 지정 *&lt;뷰어 이름>* 뷰어&quot; 도움말 항목에 설명되어 있습니다. 예를 들어 확대/축소 뷰어의 CSS 마커에 대해 읽으려면 [확대/축소 뷰어 사용자 지정](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/zoom/customizing-zoom/c-html5-20-zoom-viewer-customizingviewer.html) 을 참조하십시오. 그러나 시각적 편집기가 일부 CSS 값을 이해하지 못할 수 있습니다. 이러한 경우 시각적 편집기는 CSS가 계속 작동할 수 있도록 오류를 무시하려고 합니다.
   >[!NOTE]
   >
   >원시 양식에서 CSS를 직접 편집하려면 선택한 유형 풀다운 메뉴 아래에서 **[!UICONTROL CSS 표시/숨기기]**를 선택합니다(필요한 경우 시각적 편집기를 위로 스크롤하여 표시).
   >시각적 편집기와 마찬가지로 CSS에서 직접 속성을 변경하면 뷰어 샘플에 어떤 영향을 주는지 즉시 볼 수 있습니다. 또한 동일한 속성이 시각적 편집기에서 동시에 자동으로 업데이트됩니다. 따라서 원시 CSS 편집기 또는 시각적 편집기를 사용하거나 두 가지 모두를 서로 교환하여 사용할 수 있습니다.

   >[!NOTE]
   >
   >단추 아트웍의 경우 2x 이미지를 선택하고 고해상도 아트 작업을 업로드합니다. 대화형 이미지 및 쇼퍼블 배너를 사용하여 작업할 경우 바로 사용 가능한 다양한 핫스팟 단추에서 선택할 수도 있습니다.

1. (선택 사항) [뷰어 사전 설정 편집] 페이지의 상단 근처에 있는 **[!UICONTROL Desktop]**, **[!UICONTROL Tablet]** 또는 **[!UICONTROL Phone]**&#x200B;을 선택하여 다른 장치 및 화면 유형에 대한 시각적 스타일을 고유하게 정의합니다.
1. 뷰어 사전 설정 편집기 페이지에서 **[!UICONTROL 동작]** 탭을 선택합니다. 또는 뷰어에서 시각적 요소를 선택하여 구성에 대해 선택할 수 있습니다.
1. **[!UICONTROL 선택한 유형]** 풀다운 메뉴에서 동작을 변경할 구성 요소를 선택합니다.

   시각적 편집기의 많은 구성 요소에는 관련된 자세한 설명이 있습니다. 이러한 설명은 구성 요소를 확장하여 연결된 매개 변수를 표시할 때 파란색 상자 내에 표시됩니다.

   일부 뷰어 유형에는 **[!UICONTROL IS 명령]** 텍스트 필드에 이미지 제공 명령을 지정할 수 있는 구성 요소가 있습니다. 사용할 수 있는 명령 목록은 [이미지 제공 API 참조](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-is-home.html)를 참조하십시오.

   >[!NOTE]
   >
   >**휴대폰이나 태블릿과 같은 터치 장치를 사용하는 경우...**
   >
   >
   >텍스트 필드에 값을 입력한 후 사용자 인터페이스의 다른 곳을 선택하여 변경 사항을 제출하고 가상 키보드를 닫습니다. Enter 키를 선택하면 작업이 발생하지 않습니다.

1. 페이지의 오른쪽 위 모서리 근처에 있는 **[!UICONTROL 저장]**&#x200B;을 선택합니다.
1. 웹 사이트에서 사용할 수 있도록 새 뷰어 사전 설정을 게시합니다.

   [뷰어 사전 설정 게시](#publishing-viewer-presets)를 참조하십시오.

### 대화형 뷰어 사전 설정을 만들기 위한 특수 고려 사항 {#special-considerations-for-creating-an-interactive-viewer-preset}

**패널의 이미지 축소판 표시 모드 정보**

대화형 비디오 뷰어 사전 설정을 만들거나 편집할 때 **[!UICONTROL 동작]** 탭 아래의 **[!UICONTROL 선택한 구성 요소]** 메뉴에서 `InteractiveSwatches`을 선택할 때 사용할 표시 모드 설정을 선택할 수 있습니다. 선택한 표시 모드는 비디오가 재생되는 동안 축소판이 표시되는 방법과 시기에 영향을 줍니다. `segment`표시 모드(기본값) 또는 `continuous` 표시 모드를 선택할 수 있습니다.

<table>
 <tbody>
  <tr>
   <td><strong>표시 모드</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td>세그먼트</td>
   <td><p><code>Segment </code>는 직접 만드는 기본 대화형 비디오 뷰어 사전 설정 <code>Shoppable_Video_light</code> 및 <code>Shoppable_Video_dark</code> 과 대화형 비디오 뷰어 사전 설정에 대한 기본 표시 모드입니다.</p> <p>이 모드에서는 비디오 세그먼트에 지정된 축소판이 디스플레이 패널의 표시된 지점 수보다 적으면 됩니다. 또한 다음 또는 이전 하위 세그먼트의 축소판은 <i>이(가) 아니라 </i>이(가) 패널의 빈 점을 채우는 데 사용됩니다. 즉, 특정 비디오 세그먼트에 지정된 색상 견본의 표시를 유지합니다.</p> </td>
  </tr>
  <tr>
   <td>연속</td>
   <td><p><code>continuous </code>표시 모드에서 세그먼트의 축소판 수가 패널에 표시되는 수보다 작으면 뷰어에 다음 세그먼트의 축소판 표시가 자동으로 포함됩니다. 또는 마지막 축소판이 표시되는 경우 뷰어는 이전 세그먼트의 축소판 표시를 자동으로 포함합니다.</p> <p>이 항목</a>의 <a href="/help/assets/interactive-videos.md">비디오는 <code>continuous </code>표시 모드의 예입니다.</a></p> </td>
  </tr>
 </tbody>
</table>

**대화형 비디오 뷰어의 자동 스크롤 동작 정보**

대화형 비디오 뷰어의 축소판 자동 스크롤 동작은 선택한 표시 모드와 독립적으로 작동합니다.

대화형 비디오 뷰어 사전 설정을 만들거나 편집할 때 동작 탭에서 자동 스크롤에 액세스합니다. 동작 탭의 **[!UICONTROL 선택한 구성 요소]** 드롭다운 메뉴에서 **[!UICONTROL 대화형 색상 견본]**&#x200B;을 선택합니다. IS 명령 텍스트 필드 아래에 자동 스크롤 확인란이 나열됩니다.

사용자가 비디오를 재생하는 동안 뷰어 사전 설정에서 **[!UICONTROL 자동 스크롤]**(확인란 지우기)을 비활성화하면 패널의 전체 비디오 길이에 대한 첫 번째 축소판 이미지만 표시됩니다. 그러나 원하는 경우 위쪽 및 아래쪽 화살표 아이콘을 사용하여 축소판을 수동으로 스크롤할 수 있습니다.

뷰어 사전 설정에서 **[!UICONTROL 자동 스크롤]**&#x200B;을 활성화(선택)하면 비디오 재생 중에 비디오 세그먼트에 할당된 축소판 이미지가 세그먼트 시작 시 보기로 스크롤됩니다. 하지만 세그먼트 내의 특정 축소판이 이전 또는 이후에 다른 축소판보다 두 배 이상 표시되는 인스턴스가 있습니다. 이 동작은 세그먼트의 축소판 그림 수가 패널에 표시되는 수보다 크고 균일하게 분할되지 않으므로 발생합니다.

예시하기 위해 30초 비디오 세그먼트가 한 개 있다고 가정합니다. 30초 동안 표시할 총 9개의 축소판이 있습니다. 브라우저 크기가 표시 패널에 표시되는 축소판 위치가 4개 있는 방식으로 조정됩니다. 30초 비디오 시간 세그먼트는 세 개의 하위 세그먼트로 나누어집니다. 다음 표는 지정된 시간 하위 세그먼트에 대해 축소판이 표시되는 분류를 보여줍니다.

| **비디오 하위 세그먼트** | **하위 세그먼트 시간(초)** | **패널에 표시되는 축소판 그림** |
|---|---|---|
| 1 | 0-10 | 1, 2, 3, 4 |
| 2 | 10-20 | 4, 5, 6, 7 |
| 3 | 20-30 | 6, 7, 8, 9 |

비디오 하위 세그먼트 3은 지정된 축소판 그림 이상으로 확장되지 않습니다. 또한 다른 축소판보다 두 배 긴 축소판 그림 4, 6 및 7이 패널에 표시됩니다.

뷰어가 사용 가능한 위치의 수에 따라 패널에 표시되는 축소판 그림 수에 사용하는 논리는 다음과 같습니다.

* 하위 세그먼트 수 = 다음 하위 세그먼트로 반올림됩니다(브라우저 창 크기에 따라 축소판 그림 패널에 표시되는 슬롯 수/축소판 그림 수).
위의 표에서 예제 사용, 9개의 축소판 / 4개의 슬롯 = 2.25; 뷰어 로직은 최대 3개의 하위 세그먼트를 라운드합니다.

* 축소판 그림 수 = 다음 축소판 그림(축소판 그림 수/비디오 하위 세그먼트 수)로 반올림합니다.
위의 표에 나오는 예를 사용하면 9개의 축소판 그림 / 3개의 비디오 하위 세그먼트 = 3개의 축소판 그림이 표시됩니다.

* 하위 세그먼트 기간 = 총 비디오 지속 시간 / 비디오 하위 세그먼트 수.
위의 표에 나오는 예를 사용하여, 30초 / 3개의 비디오 하위 세그먼트 = 각 비디오 하위 세그먼트의 10초 표시.

#### 캐러셀 배너 뷰어 사전 설정 만들기에 대한 특수 고려 사항 {#special-considerations-for-creating-a-carousel-banner-viewer-preset}

회전 배너 뷰어 사전 설정을 만들 때 다음과 같이 핫스팟 스타일을 변경할 수 있습니다.

|  | **설명** | **작업** |
|---|---|---|
| **[!UICONTROL 핫스팟 아이콘]** | 핫스팟에 사용되는 아이콘 변경 | 핫스팟 아이콘 이미지를 변경하려면 **[!UICONTROL 모양]** 탭의 **[!UICONTROL 선택한 구성 요소]**&#x200B;에서 **[!UICONTROL ImageMapEffect]**&#x200B;를 선택합니다. **[!UICONTROL 아이콘]**&#x200B;에서 **[!UICONTROL 배경]**&#x200B;을 선택하고 **[!UICONTROL 이미지]** 필드에서 원하는 배경 이미지를 탐색합니다. |

## 뷰어 사전 설정 활성화 또는 비활성화 {#activating-or-deactivating-viewer-presets}

사용자 인터페이스에서 사용할 수 있는 뷰어 사전 설정은 작성자 모드에서 활성 상태인 뷰어 사전 설정에 따라 다릅니다. 기본적으로 뷰어 사전 설정은 만든 후 &quot;설정&quot;입니다. 사전 설정을 끄면 작성자 모드에서 표시되지 않습니다. 사전 설정이 게시되면 설정되었는지 여부에 관계없이 항상 게시됩니다. 목록이 너무 까다로워지거나 뷰어 사전 설정을 사용할 수 없게 하려는 경우 뷰어 사전 설정을 비활성화할 수 있습니다.

**뷰어 사전 설정을 활성화하거나 비활성화하려면:**

1. Experience Manager의 왼쪽 위 모서리에서 Experience Manager 로고를 선택한 다음 왼쪽 레일에서 **[!UICONTROL 도구]**(망치 아이콘) > **[!UICONTROL 자산]** > **[!UICONTROL 뷰어 사전 설정]**&#x200B;을 선택합니다.
1. 뷰어 사전 설정 페이지의 **[!UICONTROL 상태]** 열 헤더 아래에서 토글을 선택하여 뷰어 사전 설정을 활성화하거나 비활성화합니다.

   활성화되는 뷰어 사전 설정은 파란색 상자 내에 토글이 오른쪽에 나타납니다. 비활성화된 뷰어 사전 설정은 회색 상자 내에서 토글이 왼쪽에 표시됩니다.

## 뷰어 사전 설정 게시 {#publishing-viewer-presets}

뷰어 사전 설정의 상태를 활성화(또는 &quot;켜기&quot;)하면 Dynamic Media 구성 요소, 대화형 미디어 구성 요소에 표시되고 자산을 볼 때마다 표시됩니다.

그러나 뷰어 사전 설정이 있는 자산을 *전달*&#x200B;하려면 뷰어 사전 설정도 게시해야 합니다. 자산에 대한 URL 또는 포함 코드를 얻으려면 모든 뷰어 사전 설정을 *및*&#x200B;로 게시해야 합니다. Dynamic Media과 함께 제공되는 모든 기본 뷰어 사전 설정을 활성화하고 게시해야 합니다. 만들고 추가하는 사용자 지정 뷰어 사전 설정은 자동으로 활성화되지만 게시해야 합니다.

[뷰어 사전 설정 활성화 또는 비활성화](#activating-or-deactivating-viewer-presets)를 참조하십시오.

[자산 미리 보기](/help/assets/previewing-assets.md)도 참조하십시오.

**뷰어 사전 설정을 게시하려면:**

1. Experience Manager의 왼쪽 위 모서리에서 Experience Manager 로고를 선택한 다음 왼쪽 레일에서 **[!UICONTROL 도구]**(망치 아이콘) > **[!UICONTROL 자산]** > **[!UICONTROL 뷰어 사전 설정]**&#x200B;을 선택합니다.
1. 게시할 뷰어 사전 설정을 하나 이상 선택합니다.
1. 도구 모음에서 **[!UICONTROL 게시]** 아이콘을 선택합니다.

## 뷰어 사전 설정 정렬 {#sorting-viewer-presets}

1. Experience Manager의 왼쪽 위 모서리에서 Experience Manager 로고를 선택한 다음 왼쪽 레일에서 **[!UICONTROL 도구]**(망치 아이콘) > **[!UICONTROL 자산]** > **[!UICONTROL 뷰어 사전 설정]**&#x200B;을 선택합니다.
1. **[!UICONTROL 사전 설정 제목]**, **[!UICONTROL 유형]**, **[!UICONTROL 게시됨]** 또는 **[!UICONTROL 상태]**&#x200B;를 선택하여 해당 열 머리글을 기준으로 정렬합니다. 예를 들어, **[!UICONTROL 유형]**&#x200B;을 선택하여 뷰어 사전 설정 유형을 알파벳 또는 역방향 알파벳 순서로 정렬합니다.

## 뷰어 사전 설정 편집 {#editing-viewer-presets}

사전 정의된 기본 제공 뷰어 사전 설정&#x200B;*을 편집하는 것은 지원되는 시나리오가 아닙니다.* 즉시 사용 가능한 뷰어 사전 설정을 편집하는 경우 새 이름으로 저장하라는 메시지가 표시됩니다.

**뷰어 사전 설정을 편집하려면:**

1. Experience Manager의 왼쪽 위 모서리에서 Experience Manager 로고를 선택한 다음 왼쪽 레일에서 **[!UICONTROL 도구]**(망치 아이콘) > **[!UICONTROL 자산]** > **[!UICONTROL 뷰어 사전 설정]**&#x200B;을 선택합니다.
1. 뷰어 사전 설정 제목 왼쪽에 있는 상자를 선택하여 사전 설정을 선택합니다.
1. 도구 모음에서 **[!UICONTROL 편집]**&#x200B;을 선택합니다.
1. **[!UICONTROL 뷰어 사전 설정 편집기]** 페이지에서 **[!UICONTROL 모양]** 및 **[!UICONTROL 동작]** 탭에 있는 옵션을 사용하여 뷰어 사전 설정을 변경할 수 있습니다.

   뷰어 사전 설정 편집기 페이지의 왼쪽 위 모서리 근처에 있는 **[!UICONTROL 모양]** 탭에서 **[!UICONTROL 데스크탑]**, **[!UICONTROL 태블릿]** 또는 **[!UICONTROL Phone]**&#x200B;을 선택하여 자산의 프레젠테이션 모드를 변경합니다.

1. 페이지의 오른쪽 위 모서리 근처에 있는 다음 중 하나를 수행합니다.

   * **[!UICONTROL 저장]**&#x200B;을 선택하여 변경 사항을 저장하고 뷰어 사전 설정 페이지로 돌아갑니다.
   * **[!UICONTROL 취소]**&#x200B;를 선택하여 변경 내용을 적용하고 뷰어 사전 설정 페이지로 돌아갑니다.

## 사용자 지정 뷰어 사전 설정 삭제 {#deleting-custom-viewer-presets}

Dynamic Media에 만들어 추가한 뷰어 사전 설정을 삭제할 수 있습니다.

**사용자 지정 뷰어 사전 설정을 삭제하려면**

1. Experience Manager의 왼쪽 위 모서리에서 Experience Manager 로고를 선택한 다음 왼쪽 레일에서 **[!UICONTROL 도구]** (망치 아이콘) **[!UICONTROL 자산]** > **[!UICONTROL 뷰어 사전 설정]**&#x200B;을 선택합니다.
1. 뷰어 사전 설정 페이지에서 사전 설정 제목을 선택한 다음 **[!UICONTROL 휴지통]** 아이콘을 선택합니다.
1. **[!UICONTROL 삭제]**&#x200B;를 선택합니다.

## 자산에 뷰어 사전 설정 적용 {#applying-a-viewer-preset-to-an-asset}

자산과 선택한 뷰어를 모두 이미 게시한 경우 뷰어 사전 설정을 선택하면 **[!UICONTROL URL]** 및 **[!UICONTROL 포함]** 단추가 표시됩니다.

**자산에 뷰어 사전 설정을 적용하려면:**

1. 자산을 열고 페이지의 왼쪽 위 모서리 근처에 있는 드롭다운 메뉴를 선택한 다음 **[!UICONTROL Viewers]**&#x200B;를 선택합니다.

   >[!NOTE]
   >
   >자산과 선택한 뷰어를 모두 이미 게시한 경우 뷰어 사전 설정을 선택하면 **[!UICONTROL URL]** 및 **[!UICONTROL 포함]** 단추가 표시됩니다.

1. 자산에 적용할 수 있도록 왼쪽 창에서 뷰어 사전 설정을 선택합니다.

   [URL을 복사하여](/help/assets/linking-urls-to-yourwebapplication.md)을 다른 사용자와 공유할 수 있습니다.

## 뷰어 사전 설정을 사용하여 자산 제공 {#delivering-assets-with-viewer-presets}

뷰어 사전 설정에 대한 URL을 가져오려면 [웹 애플리케이션에 URL 연결](/help/assets/linking-urls-to-yourwebapplication.md)을 참조하십시오. 또한 [웹 페이지에 비디오 뷰어 포함](/help/assets/embed-code.md)을 참조하십시오.

Experience Manager을 WCM으로 사용하는 경우 페이지에서 바로 뷰어 사전 설정을 사용하여 자산을 추가할 수 있습니다. [페이지에 Dynamic Media 자산 추가](/help/assets/adding-dynamic-media-assets-to-pages.md)를 참조하십시오.
