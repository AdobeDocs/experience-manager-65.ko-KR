---
title: 웹 페이지에 Dynamic Media 비디오 또는 이미지 뷰어 포함
description: 웹 페이지에 Dynamic Media 비디오 또는 이미지를 포함하는 방법을 알아봅니다
uuid: 6f786521-eb6c-4c80-8c15-9bf97b56818f
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 4ae76d8a-208f-4099-9f17-a94df424685e
feature: 뷰어
role: Business Practitioner, Administrator
exl-id: 203ea349-ef4c-421c-b4b6-76ee9d46ec34
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---

# 웹 페이지에 Dynamic Media 비디오, Image viewer 또는 Dimensional viewer 포함 {#embedding-the-video-or-image-viewer-on-a-web-page}

비디오를 재생하거나 웹 페이지에 포함된 자산을 보려면 **[!UICONTROL 포함 코드]** 기능을 사용하십시오. 포함 코드를 클립보드에 복사하여 웹 페이지에 붙여넣을 수 있습니다. **[!UICONTROL 포함 코드]** 대화 상자에서는 코드 편집이 허용되지 않습니다.

AEM을 WCM으로 사용하지 _않고_&#x200B;인 경우에만 URL을 포함합니다. AEM을 WCM으로 사용하는 경우 [자산을 페이지에 직접 추가합니다.](adding-dynamic-media-assets-to-pages.md)

[URL을 웹 응용 프로그램에 연결 을 참조하십시오.](linking-urls-to-yourwebapplication.md)

[응답형 사이트용으로 최적화된 이미지 제공](responsive-site.md) 을 참조하십시오.

>[!NOTE]
>
>선택한 자산을 게시하기 전까지는 포함 코드를 복사할 수 없습니다. 또한 뷰어 사전 설정 또는 이미지 사전 설정도 게시해야 합니다.
>
>[자산 게시](publishing-dynamicmedia-assets.md)를 참조하십시오.
>
>[뷰어 사전 설정 게시](managing-viewer-presets.md#publishing-viewer-presets)를 참조하십시오.
>
>[이미지 사전 설정 게시](managing-image-presets.md#publishing-image-presets)를 참조하십시오.

**웹 페이지에 Dynamic Media 비디오 또는 이미지 뷰어를 포함하려면**

1. 복사할 포함 코드가 있는 *게시된* 비디오 또는 이미지 자산으로 이동합니다.

   포함 코드는 먼저 *게시된*&#x200B;후에 *를 복사하는 데에만 사용할 수 있습니다.* 또한 뷰어 사전 설정 또는 이미지 사전 설정도 게시해야 합니다.

   [자산 게시를 참조하십시오.](publishing-dynamicmedia-assets.md)

   [뷰어 사전 설정 게시](managing-viewer-presets.md#publishing-viewer-presets)를 참조하십시오.

   [이미지 사전 설정 게시](managing-image-presets.md#publishing-image-presets)를 참조하십시오.

1. 왼쪽 레일에서 드롭다운 메뉴를 선택하고 **[!UICONTROL Viewers.]**
1. 왼쪽 레일에서 뷰어 사전 설정 이름을 탭합니다. 뷰어 사전 설정이 자산에 적용됩니다.
1. **[!UICONTROL 포함 을 누릅니다.]**
1. **[!UICONTROL 포함 코드]** 대화 상자에서 전체 코드를 클립보드에 복사한 다음 **[!UICONTROL 닫기.]**
1. 포함 코드를 웹 페이지에 붙여넣습니다.

## HTTP/2를 사용하여 Dynamic Media 자산 {#using-http-to-deliver-your-dynamic-media-assets} 제공

HTTP/2는 브라우저 및 서버의 통신 방식을 향상시키는 업데이트된 새로운 웹 프로토콜입니다. 보다 신속하게 정보를 전송할 수 있고 필요한 처리 능력을 줄일 수 있습니다. 이제 Dynamic Media 자산의 배달이 HTTP/2를 통해 수행될 수 있으므로 로드 시간이 향상됩니다.

Dynamic Media 계정에서 HTTP/2를 사용하는 시작에 대한 자세한 내용은 [HTTP2 컨텐츠 전달](http2.md)을 참조하십시오.
