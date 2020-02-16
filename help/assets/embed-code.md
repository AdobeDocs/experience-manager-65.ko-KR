---
title: 웹 페이지에 Dynamic Media 비디오 또는 이미지 뷰어 포함
description: 웹 페이지에 Dynamic Media 비디오 또는 이미지를 임베드하는 방법 학습
uuid: 6f786521-eb6c-4c80-8c15-9bf97b56818f
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 4ae76d8a-208f-4099-9f17-a94df424685e
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# 웹 페이지에 Dynamic Media 비디오 또는 이미지 뷰어 포함 {#embedding-the-video-or-image-viewer-on-a-web-page}

비디오를 **[!UICONTROL 재생하거나 웹]** 페이지에 포함된 자산을 보려는 경우 포함 코드 기능을 사용합니다. 내장 코드를 클립보드에 복사하여 웹 페이지에 붙여넣을 수 있습니다. 포함 코드 대화 상자에서는 코드를 편집할 **[!UICONTROL 수]** 없습니다.

AEM을 WCM으로 사용하지 _않는_ 경우에만 URL을 포함합니다. AEM을 WCM으로 사용하는 경우 자산을 페이지에 직접 [추가합니다.](adding-dynamic-media-assets-to-pages.md)

See [Linking URLs to your Web Application.](linking-urls-to-yourwebapplication.md)

반응형 [사이트에 최적화된 이미지 제공을 참조하십시오.](responsive-site.md)

>[!NOTE]
>
>선택한 자산을 게시하기 전까지 포함 코드를 복사할 수 없습니다. 또한 뷰어 사전 설정 또는 이미지 사전 설정도 게시해야 합니다.
>
>자산 [게시를 참조하십시오](publishing-dynamicmedia-assets.md).
>
>See [Publishing Viewer Presets](managing-viewer-presets.md#publishing-viewer-presets).
>
>See [Publishing Image Presets](managing-image-presets.md#publishing-image-presets).

**웹 페이지에 Dynamic Media 비디오 또는 이미지 뷰어를 포함하려면**

1. 임베드 코드를 복사할 *게시된* 비디오 또는 이미지 자산으로 이동합니다.

   임베드 코드는 자산을 처음 *게시한* 후에만 *복사할* 수 있습니다. 또한 뷰어 사전 설정 또는 이미지 사전 설정도 게시해야 합니다.

   자산 [게시를 참조하십시오.](publishing-dynamicmedia-assets.md)

   See [Publishing Viewer Presets](managing-viewer-presets.md#publishing-viewer-presets).

   See [Publishing Image Presets](managing-image-presets.md#publishing-image-presets).

1. 왼쪽 레일에서 드롭다운 메뉴를 선택하고 뷰어를 **[!UICONTROL 누릅니다]**.
1. 왼쪽 레일에서 뷰어 사전 설정 이름을 누릅니다. 뷰어 사전 설정이 자산에 적용됩니다.
1. 포함을 **[!UICONTROL 누릅니다]**.
1. 포함 **[!UICONTROL 코드]** 대화 상자에서 전체 코드를 클립보드에 복사한 다음 닫기를 **[!UICONTROL 누릅니다]**.
1. 포함 코드를 웹 페이지에 붙여넣습니다.

## HTTP/2를 사용하여 다이내믹 미디어 에셋 전달 {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2는 브라우저와 서버의 통신 방식을 향상시키는 업데이트된 새로운 웹 프로토콜입니다. 보다 신속하게 정보를 전송할 수 있고 필요한 처리 능력을 줄일 수 있습니다. 이제 Dynamic Media 에셋 배달을 HTTP/2를 통해 보다 나은 응답 및 로드 시간을 제공할 수 있습니다.

Dynamic [Media 계정으로](http2.md) HTTP/2 사용을 시작하는 방법에 대한 자세한 내용은 HTTP2 컨텐츠 제공을 참조하십시오.
