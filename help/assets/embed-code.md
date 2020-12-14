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
source-git-commit: e916f70549197ac9f95443e972401a78735b0560
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---


# 웹 페이지에 Dynamic Media 비디오, 이미지 뷰어 또는 차원 뷰어 포함 {#embedding-the-video-or-image-viewer-on-a-web-page}

비디오를 재생하거나 웹 페이지에 포함된 자산을 보려면 **[!UICONTROL 포함 코드]** 기능을 사용합니다. 포함 코드를 클립보드에 복사하여 웹 페이지에 붙여넣을 수 있습니다. **[!UICONTROL 포함 코드]** 대화 상자에서 코드 편집이 허용되지 않습니다.

AEM을 WCM으로 사용하는 _이 아닌_&#x200B;인 경우에만 URL을 포함합니다. AEM을 WCM으로 사용하는 경우 [페이지에서 직접 자산을 추가합니다.](adding-dynamic-media-assets-to-pages.md)

[웹 응용 프로그램에 URL 연결을 참조하십시오.](linking-urls-to-yourwebapplication.md)

[응답형 사이트에 대해 최적화된 이미지 제공을 참조하십시오.](responsive-site.md)

>[!NOTE]
>
>선택한 자산을 게시하기 전에는 포함 코드를 복사할 수 없습니다. 또한 뷰어 사전 설정 또는 이미지 사전 설정도 게시해야 합니다.
>
>[자산 게시](publishing-dynamicmedia-assets.md)를 참조하십시오.
>
>[게시 뷰어 사전 설정](managing-viewer-presets.md#publishing-viewer-presets)을 참조하십시오.
>
>[이미지 사전 설정 게시](managing-image-presets.md#publishing-image-presets)를 참조하십시오.

**웹 페이지에 Dynamic Media 비디오 또는 이미지 뷰어를 포함하려면**

1. 포함 코드를 복사하려는 *게시된* 비디오 또는 이미지 자산으로 이동합니다.

   *게시된*&#x200B;에셋을 *이후*&#x200B;만 복사할 수 있습니다. 또한 뷰어 사전 설정 또는 이미지 사전 설정도 게시해야 합니다.

   [자산 게시를 참조하십시오.](publishing-dynamicmedia-assets.md)

   [게시 뷰어 사전 설정](managing-viewer-presets.md#publishing-viewer-presets)을 참조하십시오.

   [이미지 사전 설정 게시](managing-image-presets.md#publishing-image-presets)를 참조하십시오.

1. 왼쪽 레일에서 드롭다운 메뉴를 선택하고 **[!UICONTROL 뷰어를 누릅니다.]**
1. 왼쪽 레일에서 뷰어 사전 설정 이름을 누릅니다. 뷰어 사전 설정이 자산에 적용됩니다.
1. **[!UICONTROL 포함을 누릅니다.]**
1. **[!UICONTROL 포함 코드]** 대화 상자에서 전체 코드를 클립보드로 복사한 다음 **[!UICONTROL 닫기.]**
1. 포함 코드를 웹 페이지에 붙여넣습니다.

## HTTP/2를 사용하여 Dynamic Media 에셋 {#using-http-to-deliver-your-dynamic-media-assets} 제공

HTTP/2는 브라우저와 서버의 통신 방식을 향상시키는 업데이트된 새로운 웹 프로토콜입니다. 정보를 빠르게 전송할 수 있고 필요한 처리 능력을 줄일 수 있습니다. 이제 Dynamic Media 에셋 배달을 HTTP/2를 통해 더 나은 응답 및 로드 시간을 제공할 수 있습니다.

Dynamic Media 계정으로 HTTP/2를 사용하는 시작에 대한 자세한 내용은 [HTTP2 콘텐츠 제공](http2.md)을 참조하십시오.
