---
title: 다이내믹 미디어 자산 게시
description: 다이내믹 미디어 자산을 게시하는 방법
uuid: b1bee905-86cf-4284-8d4e-067e11557899
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 99d7025f-d022-4213-83c0-815a4712c573
translation-type: tm+mt
source-git-commit: cec6c4f9a1a75eb049dd4b8461c36c8d58d46f79
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---


# Publishing Dynamic Media Assets {#publishing-dynamic-media-assets}

이미 업로드한 자산을 선택하고 게시 또는 **[!UICONTROL 빠른 게시를 탭하여 Dynamic Media]** 자산을 **[!UICONTROL 게시합니다.]** Dynamic Media 에셋이 게시된 후에는 URL을 통해 웹 페이지에 포함하거나 페이지에 코드를 포함시켜 사용할 수 있습니다.

또한 사용자가 개입하지 않고도 업로드한 자산을 즉시 게시할 수 있습니다. See [Configuring Dynamic Media - Scene7 mode.](config-dms7.md)
또는 폴더 수준에서 선택적 게시를 사용하여 서로 배타적인 Dynamic Media 또는 AEM에 선택적으로 **[!UICONTROL 에셋을 게시할]** 수 있습니다. 동적 [미디어에서 선택적 게시 작업을 참조하십시오.](/help/assets/selective-publishing.md)

[ **[!UICONTROL 카드 보기]**]에서 자산 이름 바로 아래에, 게시되었음을 나타내는 작은 둥근 모양 아이콘이 날짜와 시간 왼쪽에 표시됩니다. 목록 보기 **[!UICONTROL 에서]**&#x200B;게시된 **** 열은 게시되었거나 게시되지 않은 자산을 나타냅니다.

>[!NOTE]
>
>자산이 이미 게시된 경우, AEM을 사용하여 자산을 다른 폴더로 이동하고 새 위치에서 다시 게시할 경우에도 새로 게시된 자산과 함께 원래 게시된 자산 위치를 계속 사용할 수 있습니다. 그러나 원래 게시된 자산은 AEM에 &quot;손실&quot;이며 게시 취소할 수 없습니다. 따라서 다른 폴더로 이동하기 전에 먼저 자산을 게시 취소하는 것이 좋습니다.

비디오 에셋을 인코딩한 후 즉시 게시하려면 인코딩이 완전히 완료되었는지 확인하십시오. 비디오를 인코딩하는 동안 시스템에서 비디오 처리 워크플로가 진행 중임을 알 수 있습니다. 비디오 인코딩이 완료되면 비디오 변환을 미리 볼 수 있어야 합니다. 이때 게시 오류를 발생시키지 않고 비디오를 게시할 수 있습니다.

See also [Linking URLs to your Web Application](linking-urls-to-yourwebapplication.md).

See also [Embedding the Dynamic Media Video or Image viewer on a web page](embed-code.md)

>[!NOTE]
>
>* URL을 사용하려면 자산을 게시해야 합니다. 에셋이 게시되지 않으면 URL을 복사하여 웹 브라우저에 붙여넣는 기능이 작동하지 않습니다.
>* 실시간 전달을 위해 이미지 사전 설정과 뷰어 사전 설정을 활성화하고 게시해야 합니다.

>



세트 또는 자산 게시에 대한 자세한 내용은 자산 [게시를 참조하십시오.](manage-assets.md)

## 다이내믹 미디어 자산의 HTTP/2 전달 {#http-delivery-of-dynamic-media-assets}

AEM은 이제 HTTP/2를 통해 모든 다이내믹 미디어 컨텐츠(이미지 및 비디오)의 배달을 지원합니다. 즉, 이미지나 비디오에 대해 게시된 URL 또는 포함 코드는 호스팅된 자산을 허용하는 모든 응용 프로그램과 통합할 수 있습니다. 그런 다음 게시된 자산은 HTTP/2 프로토콜을 통해 전달됩니다. 이 전달 방법은 브라우저와 서버의 통신 방식을 개선하여 모든 Dynamic Media 자산의 응답 및 로드 시간을 향상시킵니다.

자세한 내용은 FAQ [의 HTTP/2 제공을](/help/sites-administering/scene7-http2faq.md) 참조하십시오.
