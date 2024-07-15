---
title: Dynamic Media Assets 게시
description: 이러한 에셋의 HTTP/2 전달을 비롯한 비디오 및 이미지와 같은 Dynamic Media 에셋을 게시하는 방법을 알아봅니다.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
role: User, Admin
exl-id: 750627fc-2a29-43ff-867e-55cb2e371043
feature: Publishing
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 4%

---

# Dynamic Media 자산 게시 {#publishing-dynamic-media-assets}

이미 업로드한 자산을 선택하고 **[!UICONTROL Dynamic Media]** 또는 **[!UICONTROL 빠른 Publish]**&#x200B;을(를) 탭하여 Publish 자산을 게시합니다. Dynamic Media 자산이 게시된 후 URL을 통해 또는 웹 페이지에 코드를 포함하여 웹 페이지에 포함할 수 있습니다.

또한 업로드한 에셋을 사용자의 개입 없이 즉시 게시할 수 있습니다. [Dynamic Media - Scene7 모드 구성](config-dms7.md)을 참조하십시오.
또는 폴더 수준에서 **[!UICONTROL 선택적 Publish]**&#x200B;을(를) 사용하여 자산을 Dynamic Media 또는 Adobe Experience Manager 중 서로 상호 배타적으로 게시할 수 있습니다. [Dynamic Media에서 선택적 Publish 작업](/help/assets/selective-publishing.md)을 참조하세요.

**[!UICONTROL 카드 보기]**&#x200B;에서 작은 지구 모양 아이콘이 자산 이름 바로 아래에 나타나며 날짜 및 시간 왼쪽에 게시되었음을 나타냅니다. In the **[!UICONTROL List View]**, a **[!UICONTROL Published]** column indicates which assets are published or which are not.

>[!NOTE]
>
>에셋이 이미 게시된 경우 Experience Manager 을 사용하여 에셋을 다른 폴더로 이동하고 새 위치에서 다시 게시합니다. 새로 다시 게시된 에셋과 함께 원래 게시된 에셋 위치는 계속 사용할 수 있습니다. 그러나 원래 게시된 에셋은 Experience Manager에게 &quot;유실&quot;되며 게시를 취소할 수 없습니다. 따라서 자산을 다른 폴더로 이동하기 전에 먼저 게시를 취소하는 것이 좋습니다.

비디오 에셋을 인코딩한 후 바로 게시하려면 인코딩이 수행되었는지 확인하십시오. 비디오가 인코딩되는 동안 시스템에서는 비디오 처리 워크플로우가 진행 중임을 알려줍니다. 비디오 인코딩이 완료되면 비디오 렌디션을 미리 볼 수 있습니다. 이때 게시 오류가 발생하지 않고 비디오를 게시해도 안전합니다.

[웹 응용 프로그램에 URL 연결](linking-urls-to-yourwebapplication.md)도 참조하세요.

[웹 페이지에 Dynamic Media 비디오 또는 이미지 뷰어 포함](embed-code.md)도 참조하세요.

>[!NOTE]
>
>* URL을 사용하려면 Assets을 게시해야 합니다. 에셋이 게시되지 않은 경우 URL을 복사하고 웹 브라우저에 붙여넣을 수 없습니다.
>* 라이브 게재를 위해서는 이미지 사전 설정 및 뷰어 사전 설정을 활성화하고 게시해야 합니다.
>

집합 또는 자산을 게시하는 방법에 대한 자세한 내용은 [Publish 자산](manage-assets.md)을 참조하세요.

## Dynamic Media 자산의 HTTP/2 전달 {#http-delivery-of-dynamic-media-assets}

이제 Experience Manager은 HTTP/2를 통해 모든 Dynamic Media 컨텐츠(이미지 및 비디오)의 전달을 지원합니다. 즉, 이미지 또는 비디오에 대한 게시된 URL 또는 포함 코드를 호스팅된 에셋을 허용하는 모든 애플리케이션과 통합할 수 있습니다. 그런 다음 게시된 에셋은 HTTP/2 프로토콜을 통해 전달됩니다. 이 전달 방법은 브라우저와 서버의 통신 방식을 개선하여 모든 Dynamic Media 에셋의 응답 및 로드 시간을 향상시킵니다.

자세한 내용은 [HTTP/2 콘텐츠 배달 FAQ](/help/sites-administering/scene7-http2faq.md)를 참조하세요.
