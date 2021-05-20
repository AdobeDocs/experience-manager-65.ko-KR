---
title: Dynamic Media 자산 게시
description: Dynamic Media 자산을 게시하는 방법
uuid: b1bee905-86cf-4284-8d4e-067e11557899
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 99d7025f-d022-4213-83c0-815a4712c573
role: Business Practitioner, Administrator
exl-id: 750627fc-2a29-43ff-867e-55cb2e371043
feature: 게시
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 1%

---

# Dynamic Media 자산 게시 {#publishing-dynamic-media-assets}

이미 업로드한 자산을 선택하고 **[!UICONTROL 게시]** 또는 **[!UICONTROL 빠른 게시를 탭하여 Dynamic Media 자산을 게시합니다.]** Dynamic Media 자산이 게시되면 URL을 통해 또는 페이지에 해당 코드를 포함하여 웹 페이지에 포함할 수 있습니다.

사용자가 개입하지 않고 업로드한 자산을 즉시 게시할 수도 있습니다. [Dynamic Media 구성 - Scene7 모드 을 참조하십시오.](config-dms7.md)
또는 폴더 수준에서  **[!UICONTROL 선택적 게시]** 를 사용하여 서로 배타적으로 Dynamic Media 또는 AEM에 자산을 선택적으로 게시할 수 있습니다. [Dynamic Media의 선택적 게시 작업](/help/assets/selective-publishing.md)을 참조하십시오.

**[!UICONTROL 카드 보기]**&#x200B;에서 작은 지구본 아이콘이 자산의 이름 바로 아래에 있고 날짜 및 시간 왼쪽에 표시되어 게시된 것임을 나타냅니다. **[!UICONTROL 목록 보기]**&#x200B;에서 **[!UICONTROL 게시된]** 열은 게시되었거나 게시되지 않은 자산을 나타냅니다.

>[!NOTE]
>
>자산이 이미 게시되어 있다면, AEM을 사용하여 자산을 다른 폴더로 이동하고 새 위치에서 다시 게시하는 경우, 새로 다시 게시된 자산과 함께 원래 게시된 자산 위치를 계속 사용할 수 있습니다. 그러나 게시된 원래 자산은 AEM에 &quot;손실&quot;이며 게시 취소할 수 없습니다. 따라서 다른 폴더로 이동하기 전에 먼저 자산을 게시 취소하는 것이 좋습니다.

비디오 자산을 인코딩한 후 바로 게시하려면 인코딩이 완전히 수행되었는지 확인하십시오. 비디오를 인코딩하고 있으면 시스템에서 비디오 처리 워크플로우가 진행 중임을 알 수 있습니다. 비디오 인코딩이 완료되면 비디오 렌디션을 미리 볼 수 있습니다. 이때 게시 오류가 발생하지 않고 비디오를 게시하면 됩니다.

또한 [URL을 웹 응용 프로그램에 연결](linking-urls-to-yourwebapplication.md)을 참조하십시오.

웹 페이지에 [Dynamic Media 비디오 또는 이미지 뷰어 포함](embed-code.md)을 참조하십시오

>[!NOTE]
>
>* URL을 사용하려면 자산을 게시해야 합니다. 자산이 게시되지 않은 경우 URL을 웹 브라우저에 복사하여 붙여넣을 수 없습니다.
>* 라이브 전달을 위해 이미지 사전 설정 및 뷰어 사전 설정을 활성화하고 게시해야 합니다.

>



집합 또는 자산 게시에 대한 자세한 내용은 [자산 게시](manage-assets.md)를 참조하십시오.

## Dynamic Media 자산 {#http-delivery-of-dynamic-media-assets} 의 HTTP/2 전달

이제 AEM에서는 HTTP/2를 통해 모든 Dynamic Media 컨텐츠(이미지 및 비디오)의 전달을 지원합니다. 즉, 이미지나 비디오에 대해 게시된 URL 또는 포함 코드는 호스팅된 자산을 허용하는 모든 애플리케이션과 통합할 수 있습니다. 게시된 자산은 HTTP/2 프로토콜을 통해 전달됩니다. 이 전달 방법은 브라우저 및 서버의 통신 방식을 개선하여 모든 Dynamic Media 자산의 응답 및 로드 시간을 향상시킬 수 있습니다.

자세한 내용은 FAQ](/help/sites-administering/scene7-http2faq.md) 컨텐츠의 [HTTP/2 전달 을 참조하십시오.
