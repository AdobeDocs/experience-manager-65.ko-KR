---
title: Dynamic Media 이미지 사전 설정 적용
description: Dynamic Media에서 이미지 사전 설정을 적용하는 방법 알아보기
uuid: 8bafcbd0-6df0-4d5b-b2f7-116ddb4ec060
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 5c1f60ac-3741-4002-9c5d-c128f118342b
feature: 이미지 사전 설정
role: User,Admin
exl-id: 98d88b59-eb8f-42db-abb8-04506a5b8c30
source-git-commit: 4b8369de9e6a10b73115d53358ce98729d92ed44
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 11%

---

# Dynamic Media 이미지 사전 설정 적용 {#applying-image-presets}

이미지 사전 설정을 사용하면 자산에서 서로 다른 크기, 다른 형식 또는 동적으로 생성된 다른 이미지 속성이 있는 이미지를 동적으로 전달할 수 있습니다. 이미지를 내보낼 때 사전 설정을 선택할 수 있습니다. 이 사전 설정은 관리자가 지정한 사양에 맞게 이미지를 다시 포맷합니다.

또한 응답형(**[!UICONTROL RESS]** 버튼을 선택한 후 지정)인 이미지 사전 설정을 선택할 수 있습니다.

이 섹션에서는 이미지 사전 설정을 사용하는 방법을 설명합니다. [관리자는 이미지 사전 설정을 만들고 구성할 수 있습니다](managing-image-presets.md).

>[!NOTE]
>
>스마트 이미징은 기존 이미지 사전 설정에서 작동하며 마지막 전달 순간에 인텔리전스를 사용하여 브라우저 또는 네트워크 연결 속도에 따라 이미지 파일 크기를 더 줄입니다. 자세한 내용은 [스마트 이미징](imaging-faq.md) 을 참조하십시오.

미리 볼 때 언제든지 이미지에 이미지 사전 설정을 적용할 수 있습니다.

>[!NOTE]
>
>Dynamic Media - Scene7 모드에서 이미지 사전 설정은 이미지 자산에 대해서만 지원됩니다.

**Dynamic Media 이미지 사전 설정을 적용하려면:**

1. 자산을 열고 왼쪽 레일에서 드롭다운 메뉴를 선택한 다음 **[!UICONTROL 표현물]**&#x200B;을 선택합니다.

   >[!NOTE]
   >
   >* 정적 표현물은 창의 위쪽 절반에 나타납니다. 동적 표현물은 하단에 나타납니다. 동적 변환만 사용하면 URL을 사용하여 이미지를 표시할 수 있습니다. **[!UICONTROL URL]** 단추는 동적 변환을 선택하는 경우에만 나타납니다. **[!UICONTROL RESS]** 단추는 응답형 이미지 사전 설정을 선택하는 경우에만 나타납니다.
      >
      >
   * 자산의 세부 사항 보기에서 **[!UICONTROL 표현물]**&#x200B;을 선택하면 시스템은 다양한 표현물을 보여줍니다. 표시되는 사전 설정 수를 늘릴 수 있습니다. [표시되는 이미지 사전 설정 수를 늘립니다](managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display).


   ![chlimage_1-208](assets/chlimage_1-208.png)

1. 다음 중 하나를 수행합니다.

   * 이미지 사전 설정을 미리 볼 수 있도록 다이내믹 렌디션을 선택합니다.
   * 팝업을 표시하려면 **[!UICONTROL URL]**, **[!UICONTROL 포함]** 또는 **[!UICONTROL RESS]**&#x200B;를 선택합니다.

   >[!NOTE]
   >
   >자산 *및* 이미지 사전 설정이 아직 게시되지 않은 경우 **[!UICONTROL URL]** 단추(또는 **[!UICONTROL URL]** 및 **[!UICONTROL RESS]** 단추(해당하는 경우)를 사용할 수 없습니다.
   >
   >또한 이미지 사전 설정은 Dynamic Media 서버에 자동으로 게시됩니다.
