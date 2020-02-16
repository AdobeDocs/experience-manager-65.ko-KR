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
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# 다이내믹 미디어 자산 게시 {#publishing-dynamic-media-assets}

자산을 선택하고 게시를 탭하여 Dynamic Media 자산을 **[!UICONTROL 게시합니다]**. 다이내믹 미디어 에셋이 게시되면 URL을 통해 웹 페이지에 포함하거나 임베드할 수 있습니다.

또한 사용자가 개입하지 않고도 업로드한 자산을 즉시 게시할 수 있습니다. 동적 [미디어 구성 - Scene7 모드를](config-dms7.md)참조하십시오.

카드 **[!UICONTROL 보기에서]**, 자산 이름 바로 아래에 작은 글로벌 아이콘이 표시되어 게시되었음을 나타냅니다. 목록 **[!UICONTROL 보기에서]**&#x200B;게시된 **[!UICONTROL 열은]** 게시되었거나 게시되지 않은 자산을 나타냅니다.

>[!NOTE]
>
>자산이 이미 게시된 경우, AEM을 사용하여 자산을 다른 폴더로 이동하고 새 위치에서 다시 게시하면 새로 다시 게시된 자산과 함께 원래 게시된 자산 위치를 계속 사용할 수 있습니다. 그러나 원래 게시된 자산은 AEM에 &quot;손실&quot;이며 게시 취소할 수 없습니다. 따라서 다른 폴더로 이동하기 전에 먼저 에셋을 게시 취소하는 것이 좋습니다.

비디오 에셋을 인코딩한 후 즉시 게시하려면 인코딩이 완전히 완료되었는지 확인하십시오. 비디오를 인코딩하는 동안 시스템에서 비디오 처리 워크플로우가 진행 중임을 알 수 있습니다. 비디오 인코딩이 완료되면 비디오 변환을 미리 볼 수 있어야 합니다. 이때 게시 오류를 발생시키지 않고 비디오를 게시할 수 있습니다.

웹 [애플리케이션에 URL 연결을 참조하십시오](linking-urls-to-yourwebapplication.md).

웹 [페이지에 비디오 뷰어 포함을 참조하십시오.](embed-code.md)

>[!NOTE]
>
>* URL을 사용하려면 자산을 게시해야 합니다. 에셋이 게시되지 않으면 URL을 복사하여 웹 브라우저에 붙여넣을 수 없습니다.
>* 실시간 전달을 위해 이미지 사전 설정 및 뷰어 사전 설정을 활성화하고 게시해야 합니다.
>



세트 또는 자산 게시에 대한 자세한 내용은 자산 게시를 [참조하십시오.](managing-assets-touch-ui.md)

## 다이내믹 미디어 자산의 HTTP/2 전달 {#http-delivery-of-dynamic-media-assets}

이제 AEM은 HTTP/2를 통해 모든 다이내믹 미디어 컨텐츠(이미지 및 비디오)의 배달을 지원합니다. 즉, 이미지 또는 비디오에 대해 게시된 URL 또는 임베드 코드는 호스팅된 자산을 허용하는 모든 응용 프로그램과 통합할 수 있습니다. 그런 다음 HTTP/2 프로토콜을 통해 게시된 에셋을 전달합니다. 이 전달 방법은 브라우저와 서버의 통신 방식을 개선하여 모든 Dynamic Media 자산의 응답 및 로드 시간을 향상시킵니다.

자세한 [내용은 FAQ](/help/sites-administering/scene7-http2faq.md) HTTP/2 제공을 참조하십시오.
