---
title: 반응형 사이트에 최적화된 이미지 제공
description: 반응형 코드 기능을 사용하여 최적화된 이미지를 제공하는 방법
uuid: 7c6baef5-7513-4644-94ed-2383e8724c17
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 5edcc765-c374-4368-a0d9-e02a713a24f2
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Delivering optimized images for a responsive site {#delivering-optimized-images-for-a-responsive-site}

반응형 코드 기능을 사용하면 웹 개발자와 반응형 서비스를 위해 코드를 공유할 수 있습니다. 반응형(**[!UICONTROL RESS]**) 코드를 클립보드에 복사하여 웹 개발자와 공유할 수 있습니다.

이 기능은 웹 사이트가 타사 WCM에 있는 경우에 사용하는 것이 적절합니다. 그러나 웹 사이트가 대신 AEM에 있는 경우 오프사이트 이미지 서버가 이미지를 렌더링하여 웹 페이지에 제공합니다.

웹 [페이지에 비디오 뷰어 포함을 참조하십시오.](embed-code.md)

웹 [애플리케이션에 URL 연결을 참조하십시오.](linking-urls-to-yourwebapplication.md)

**반응형 사이트에**&#x200B;최적화된 이미지를 제공하는 방법은 다음과 같습니다.

1. 응답형 코드를 제공하려는 이미지로 이동하고 드롭다운 메뉴에서 변환을 **[!UICONTROL 누릅니다]**.

   ![chlimage_1-408](assets/chlimage_1-408.png)

1. 반응형 이미지 사전 설정을 선택합니다. URL **[!UICONTROL 및]** RESS **[!UICONTROL 단추가]** 나타납니다.

   ![chlimage_1-409](assets/chlimage_1-208.png)

   >[!NOTE]
   >
   >URL *또는* RESS 단추를 사용할 수 있게 하려면 선택한 에셋 **[!UICONTROL 및]** 선택한 이미지 사전 설정 또는 뷰어 사전 설정을 게시해야 **** 합니다.
   >
   >다이내믹 미디어 - 하이브리드 모드에서는 이미지 사전 설정을 게시해야 합니다.Dynamic Media - Scene7 모드는 이미지 사전 설정을 자동으로 게시합니다.

1. RESS를 **[!UICONTROL 누릅니다]**.

   ![chlimage_1-410](assets/chlimage_1-410.png)

1. 반응형 **[!UICONTROL 이미지]** 포함 대화 상자에서 반응형 코드 텍스트를 선택하고 복사하여 웹 사이트에 붙여 넣어 반응형 자산에 액세스합니다.
1. 포함 코드의 기본 중단점을 코드에서 직접 응답형 웹 사이트의 중단점과 일치하도록 편집합니다. 또한 다양한 페이지 중단점에서 제공되는 다양한 이미지 해상도를 테스트합니다.

## HTTP/2를 사용하여 Dynamic Media 에셋 전달 {#using-http-to-delivery-your-dynamic-media-assets}

HTTP/2는 브라우저와 서버의 통신 방식을 향상시키는 업데이트된 새로운 웹 프로토콜입니다. 보다 신속하게 정보를 전송할 수 있고 필요한 처리 능력을 줄일 수 있습니다. Dynamic Media 에셋 전달은 보다 나은 응답 및 로드 시간을 제공하는 HTTP/2를 사용하여 지원됩니다.

Dynamic [Media 계정으로](http2.md) HTTP/2 사용을 시작하는 방법에 대한 자세한 내용은 HTTP2 컨텐츠 제공을 참조하십시오.
