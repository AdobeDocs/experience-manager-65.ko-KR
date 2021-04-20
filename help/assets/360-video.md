---
title: 360/VR 비디오
description: Dynamic Media에서 360 및 VR(Virtual Reality) 비디오로 작업하는 방법을 알아봅니다.
uuid: c21bf2c0-7acc-401f-857e-0186de86e7a1
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: aac3c850-ae84-4bff-80de-d370e150f675
docset: aem65
feature: 360 VR Video
role: Business Practitioner, Administrator
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '1100'
ht-degree: 0%

---


# 360/VR 비디오 {#vr-video}

360도 비디오는 모든 방향에서 동시에 보기를 기록합니다. 그것들은 전방향 카메라나 카메라 모음을 사용하여 촬영한다. 평면 디스플레이에서 재생하는 동안 사용자가 보기 각도를 제어할 수 있습니다.모바일 디바이스에서 재생하는 경우 일반적으로 내장된 자이로스코프 컨트롤을 활용할 수 있습니다.

Dynamic Media - Scene7 모드는 360개의 비디오 에셋 전달을 기본적으로 지원합니다. 기본적으로 보거나 재생하는 데 추가 구성이 필요하지 않습니다. .mp4, .mkv 및 .mov와 같은 표준 비디오 확장을 사용하여 360개의 비디오를 제공할 수 있습니다. 가장 일반적인 코덱은 H.264입니다.

이 섹션에서는 360/VR 비디오 뷰어를 사용하여 공간, 속성, 위치, 가로, 의료 절차 등의 몰입형 보기 환경을 위해 필요한 사각형 비디오를 렌더링하는 작업에 대해 설명합니다.

공간 오디오는 현재 지원되지 않습니다.오디오가 스테레오로 혼합되어 있는 경우 고객이 카메라 보기 각도를 변경해도 균형(L/R)이 변경되지 않습니다.

[뷰어 사전 설정 관리](/help/assets/managing-viewer-presets.md)도 참조하십시오.

## 360 비디오 실행 중 {#video-in-action}

[Space Station 360](http://mobiletest.scene7.com/s7viewers/html5/Video360Viewer.html?asset=Viewers/space_station_360-AVS)을 눌러 브라우저 창을 열고 360도 비디오를 보십시오. 비디오를 재생하는 동안 마우스 포인터를 새 위치로 드래그하여 보기 각도를 변경합니다.

![360 비디오 ](assets/6_5_360videoiss_simplified.png)
*샘플스페이스 스테이션 360의 비디오 프레임*

## 360/VR 비디오 및 Adobe Premiere Pro {#vr-video-and-adobe-premiere-pro}

Adobe Premiere Pro를 사용하여 360/VR 푸티지를 보고 편집할 수 있습니다. 예를 들어 장면에 로고와 텍스트를 제대로 배치하고 등장방형 미디어용으로 특별히 디자인된 효과 및 전환을 적용할 수 있습니다.

[360/VR 비디오 편집](https://helpx.adobe.com/premiere-pro/how-to/edit-360-vr-video.html)을 참조하십시오.

## 360 비디오 뷰어에 사용할 에셋 업로드 {#uploading-assets-for-use-with-the-video-viewer}

AEM에 업로드된 360개의 비디오 에셋은 일반적인 비디오 에셋과 유사하게 에셋 페이지에서 **멀티미디어**&#x200B;로 레이블이 지정됩니다.

![6_5_360video-](assets/6_5_360video-selecttopreview.png)
*selecttopreview카드 보기에 표시된 업로드된 360개의 비디오 에셋입니다. 에셋은 멀티미디어로 레이블이 지정됩니다.*

**360 비디오 뷰어와 함께 사용할 에셋을 업로드하려면:**

1. 360 비디오 자산 전용 폴더를 만들었습니다.
1. [응용 비디오 프로필을 폴더에 적용합니다.](/help/assets/video-profiles.md#applying-a-video-profile-to-folders)

   360개의 비디오 컨텐츠를 렌더링하면 소스 비디오 해상도와 인코딩된 변환 해상도에 대한 요구 사항이 360개가 아닌 표준 비디오 컨텐츠보다 더 높습니다.

   이미 Dynamic Media과 함께 제공되는 즉시 사용 가능한 비디오 프로필을 사용할 수 있습니다. 그러나 360이 아닌 비디오 뷰어로 렌더링된 것과 동일한 설정으로 인코딩된 비 360 비디오에 대해 가져오는 것보다 비디오 품질이 상당히 낮습니다. 따라서 고품질 360 비디오가 필요한 경우 다음을 수행합니다.

   * 가장 좋은 방법은 원본 360 비디오 컨텐츠에 다음 해상도 중 하나를 사용하는 것입니다.

      * 풀 HD 또는 FHD 해상도로 알려진 1080p - 1920 x 1080 또는
      * 4K, UHD 또는 Ultra HD 해상도로 알려진 2160p - 3840 x 2160 이 대형 디스플레이 해상도는 프리미엄 TV 세트와 컴퓨터 모니터에서 가장 자주 볼 수 있습니다. 2160p 해상도는 너비가 4000픽셀과 가깝기 때문에 &quot;4K&quot;라고도 합니다. 즉, 1080p의 4배 픽셀을 제공합니다.
   * [고품질의 표현물을 사용하여 사용자 ](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) 정의 응용 비디오 프로필을 만듭니다. 예를 들어 다음 3가지 설정을 포함하는 응용 비디오 프로필을 만들 수 있습니다.

      * width=auto;height=720;bitrate=2500kbps
      * width=auto;height=1080;bitrate=5000kbps
      * width=auto;height=1440;bitrate=6600kbps
   * 360개의 비디오 에셋에만 사용되는 폴더에서 360개의 비디오 컨텐츠를 처리합니다.

   이러한 접근 방식은 최종 사용자의 네트워크 및 CPU에 더 많은 요구도 발생한다는 점에 유의하십시오.

1. [비디오를 폴더에 업로드합니다](/help/assets/managing-video-assets.md#upload-and-preview-video-assets).

## 360 비디오의 기본 종횡비 재정의 {#overriding-the-default-aspect-ratio-of-videos}

업로드된 자산이 360 비디오 뷰어와 함께 사용하려는 360 비디오로 자격을 얻으려면 자산의 종횡비가 2이어야 합니다.

기본적으로 AEM에서는 비디오가 종횡비(너비/높이)가 2.0이면 &quot;360&quot;으로 인식합니다. 관리자인 경우, CRXDE Lite의 옵션 `s7video360AR` 속성을 다음 위치에 설정하여 기본 종횡비 설정을 2로 재정의할 수 있습니다.

* `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

   * **속성 유형**:Double
   * **값**:부동 소수점 종횡비, 기본 2.0

이 속성을 설정하면 기존 비디오와 새로 업로드된 비디오 모두에 즉시 적용됩니다.

종횡비는 자산 세부 사항 페이지와 [Video 360 Media WCM 구성 요소](/help/assets/adding-dynamic-media-assets-to-pages.md#dynamic-media-components)에 대해 360개의 비디오 자산에 적용됩니다.

먼저 360 비디오를 업로드합니다.

## 360 비디오 미리 보기 {#previewing-video}

미리 보기를 사용하여 360 비디오가 고객에게 어떤 모습인지 보고 예상대로 작동하는지 확인할 수 있습니다.

[뷰어 사전 설정 편집](/help/assets/managing-viewer-presets.md#editing-viewer-presets)을 참조하십시오.

360 비디오가 마음에 들면 게시할 수 있습니다.

웹 페이지에 비디오 또는 이미지 뷰어 포함을 참조하십시오.[](https://helpx.adobe.com/experience-manager/6-5/help/assets/embed-code.html)
웹  [응용 프로그램에 URL 연결을 참조하십시오](https://helpx.adobe.com/experience-manager/6-5/help/assets/linking-urls-to-yourwebapplication.html). 인터랙티브한 컨텐츠에 상대 URL, 특히 AEM Sites 페이지로 연결되는 링크가 있는 경우에는 URL 기반 링크 연결 방법을 사용할 수 없습니다.
[페이지에 Dynamic Media 자산 추가를 참조하십시오.](https://helpx.adobe.com/experience-manager/6-5/help/assets/adding-dynamic-media-assets-to-pages.html)

**360 비디오를 미리 보려면**

1. **[!UICONTROL 자산]**&#x200B;에서 만든 기존 360 비디오로 이동합니다. 360 비디오 에셋을 눌러 미리 보기 모드에서 엽니다.

   ![6_5_360video-selecttopreview-1](assets/6_5_360video-selecttopreview-1.png)

   360 비디오 에셋을 눌러 비디오를 미리 봅니다.

1. 미리 보기 페이지의 왼쪽 위 모서리 근처에 있는 드롭다운 목록을 탭한 다음 **[!UICONTROL 뷰어를 선택합니다.]**

   ![6_5_360video-preview-viewers](assets/6_5_360video-preview-viewers.png)

   뷰어 목록에서 **[!UICONTROL Video360_social]**&#x200B;을 누른 다음 중 하나를 수행합니다.

   * 마우스 포인터를 비디오 위로 드래그하여 정적 장면의 보기 각도를 변경합니다.
   * 비디오의 **[!UICONTROL 재생]** 단추를 눌러 재생을 시작합니다.비디오가 재생되면 마우스 포인터를 비디오 위로 드래그하여 보기 각도를 변경합니다.

   ![6_5_360video-preview-video360-](assets/6_5_360video-preview-video360-social.png)*socialA 360 비디오 스크린샷*

   * 뷰어 목록에서 **[!UICONTROL Video360VR.]**

      VR(Virtual Reality) 비디오는 가상 현실(VR) 헤드셋을 사용하여 액세스하는 몰입형 비디오 콘텐츠입니다. 일반 비디오와 마찬가지로 비디오를 360도 비디오 카메라를 사용하여 녹화하거나 캡처할 때 초기에 VR 비디오를 만들 수 있습니다.
   ![6_5_360video-preview-video360vr](assets/6_5_360video-preview-video360vr.png)
   *360 VR 비디오 스크린샷*

1. 미리 보기 페이지의 오른쪽 위 근처에 있는 **[!UICONTROL 닫기.]**

## 360 비디오 게시 {#publishing-video}

360 비디오를 사용하려면 게시해야 합니다. 360 비디오를 게시하면 URL 및 포함 코드가 활성화됩니다. 또한 확장 가능한 성능 전달을 위해 CDN과 통합된 Dynamic Media 클라우드에 360 비디오를 게시합니다.

360 비디오를 게시하는 방법에 대한 자세한 내용은 [Dynamic Media Assets](/help/assets/publishing-dynamicmedia-assets.md) 게시를 참조하십시오.
웹 페이지에 비디오 또는 이미지 뷰어 포함](https://helpx.adobe.com/experience-manager/6-5/help/assets/embed-code.html)을 참조하십시오.
[
웹 응용 프로그램](https://helpx.adobe.com/experience-manager/6-5/help/assets/linking-urls-to-yourwebapplication.html)에 URL 연결을 참조하십시오. [ 인터랙티브한 컨텐츠에 상대 URL, 특히 AEM Sites 페이지로 연결되는 링크가 있는 경우에는 URL 기반 링크 연결 방법을 사용할 수 없습니다.
[페이지에 Dynamic Media 자산 추가를 참조하십시오.](https://helpx.adobe.com/experience-manager/6-5/help/assets/adding-dynamic-media-assets-to-pages.html)
