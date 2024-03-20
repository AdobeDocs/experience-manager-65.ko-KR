---
title: Dynamic Media 이미지 사전 설정 적용
description: 에셋이 다른 크기, 다른 형식 또는 동적으로 생성된 다른 이미지 속성으로 이미지를 동적으로 게재할 수 있도록 하는 방법에 대해 알아봅니다.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: Image Presets
role: User,Admin
exl-id: 98d88b59-eb8f-42db-abb8-04506a5b8c30
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 13%

---

# Dynamic Media 이미지 사전 설정 적용 {#applying-image-presets}

이미지 사전 설정을 사용하면 에셋이 다른 크기, 다른 형식 또는 동적으로 생성되는 다른 이미지 속성으로 이미지를 동적으로 전달할 수 있습니다. 이미지를 내보낼 때 사전 설정을 선택할 수 있습니다. 사전 설정은 관리자가 지정한 사양에 맞게 이미지 형식을 다시 지정합니다.

또한 응답형 이미지 사전 설정을 선택할 수 있습니다( 로 지정됨). **[!UICONTROL RESS]** 을(를) 선택한 후 버튼을 클릭합니다.

이 섹션에서는 이미지 사전 설정을 사용하는 방법에 대해 설명합니다. [관리자는 이미지 사전 설정을 만들고 구성할 수 있습니다](managing-image-presets.md).

>[!NOTE]
>
>스마트 이미징은 기존 이미지 사전 설정에서 작동하며 마지막 전달 순간에 인텔리전스를 사용하여 브라우저 또는 네트워크 연결 속도에 따라 이미지 파일 크기를 더 줄입니다. 다음을 참조하십시오 [스마트 이미징](imaging-faq.md) 추가 정보.

미리 볼 때마다 이미지 사전 설정을 이미지에 적용할 수 있습니다.

>[!NOTE]
>
>Dynamic Media - Scene7 모드에서는 이미지 에셋에 대해서만 이미지 사전 설정이 지원됩니다.

**Dynamic Media 이미지 사전 설정을 적용하려면 다음을 수행합니다.**

1. 에셋을 열고 왼쪽 레일에서 드롭다운 메뉴를 선택한 다음 를 선택합니다. **[!UICONTROL 표현물]**.

   >[!NOTE]
   >
   >* 정적 렌디션은 창의 맨 위에 나타납니다. 동적 렌디션은 하반기에 나타납니다. 동적 변환에만 해당 URL을 사용하여 이미지를 표시할 수 있습니다. 다음 **[!UICONTROL URL]** 동적 렌디션을 선택한 경우에만 버튼이 나타납니다. 다음 **[!UICONTROL RESS]** [버튼]은 응답형 이미지 사전 설정을 선택하는 경우에만 나타납니다.
   >
   >* 를 선택하면 시스템에 다양한 렌디션이 표시됩니다 **[!UICONTROL 표현물]** 를 클릭합니다. You can increase the number of presets seen. 다음을 참조하십시오 [표시되는 이미지 사전 설정 수 늘리기](managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display).

   ![chlimage_1-208](assets/chlimage_1-208.png)

1. 다음 중 하나를 수행합니다.

   * 이미지 사전 설정을 미리 볼 수 있도록 동적 렌디션을 선택합니다.
   * 팝업을 표시하려면 을 선택합니다. **[!UICONTROL URL]**, **[!UICONTROL 포함]**, 또는 **[!UICONTROL RESS]**.

   >[!NOTE]
   >
   >자산이 *및* 이미지 사전 설정이 아직 게시되지 않았습니다. **[!UICONTROL URL]** 단추(또는 **[!UICONTROL URL]** 및 **[!UICONTROL RESS]** 단추(해당하는 경우)를 사용할 수 없습니다.
   >
   >또한 이미지 사전 설정은 Dynamic Media 서버에 자동으로 게시됩니다.
