---
title: 디지털 에셋을 체크 인하고 체크 아웃하여 편집할 수 있습니다.
description: 편집할 에셋을 체크 아웃하고 변경 사항이 완료된 후 다시 체크 인하는 방법을 살펴봅니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 1%

---


# DAM의 체크 인 및 체크 아웃 [!DNL Experience Manager] 파일 {#check-in-and-check-out-files-in-assets}

[!DNL Adobe Experience Manager Assets] 편집할 에셋을 확인하고 변경을 완료한 후 다시 체크 인할 수 있습니다. 자산을 체크 아웃한 후, 자신만 자산을 편집, 주석 달기, 게시, 이동 또는 삭제할 수 있습니다. 자산을 체크 아웃하면 자산이 잠깁니다. 자산을 다시 체크 인하기 전에는 다른 사용자가 자산에 대해 이러한 작업을 수행할 수 없습니다 [!DNL Assets]. 하지만 잠긴 자산에 대한 메타데이터를 변경할 수는 있습니다.

자산을 체크 아웃/체크 인하려면 자산에 대해 쓰기 액세스 권한이 필요합니다.

이 기능은 여러 사용자가 팀 간의 편집 워크플로우에 대해 공동으로 작업하는 작성자가 변경한 내용을 다른 사용자가 덮어쓰는 것을 방지할 수 있도록 도와줍니다.

## 자산 확인 {#checking-out-assets}

1. 사용자 [!DNL Assets] 인터페이스에서 체크 아웃할 자산을 선택합니다. 여러 자산을 선택하여 체크 아웃할 수도 있습니다.
1. 도구 모음에서 체크 **[!UICONTROL 아웃을 클릭합니다]**.
체크 **[!UICONTROL 아웃]** 옵션은 체크 인으로 **[!UICONTROL 전환합니다]**.
체크 아웃한 자산을 다른 사용자가 편집할 수 있는지 확인하려면 다른 사용자로 로그인합니다. 체크 아웃한 자산의 축소판에 잠금 기호가 표시됩니다.

   ![chlimage_1-471](assets/chlimage_1-471.png)

   자산을 선택합니다. 도구 모음에는 자산을 편집, 주석, 게시 또는 삭제할 수 있는 옵션이 표시되지 않습니다.

   ![chlimage_1-472](assets/chlimage_1-472.png)

   속성 **[!UICONTROL 보기를 클릭하여]** 잠긴 자산에 대한 메타데이터를 편집할 수 있습니다.

1. 편집 **[!UICONTROL 을]** 클릭하여 자산을 편집 모드로 엽니다.

   ![chlimage_1-473](assets/chlimage_1-473.png)

1. 자산을 편집하고 변경 내용을 저장합니다. 예를 들어 이미지를 자르고 저장합니다.

   ![chlimage_1-474](assets/chlimage_1-474.png)

   자산에 주석을 달거나 게시하도록 선택할 수도 있습니다.

1. 인터페이스에서 편집된 자산을 [!DNL Assets] 선택하고 도구 모음에서 **[!UICONTROL 체크 인]** 을 클릭합니다. 수정된 에셋이 체크 인되어 다른 사용자가 편집할 수 [!DNL Assets] 있습니다.

## 강제 체크 인 {#forced-check-in}

관리자는 다른 사용자가 체크 아웃한 자산을 체크 인할 수 있습니다.

1. 관리자로 [!DNL Assets] 로그인합니다.
1. 사용자 인터페이스에서 다른 사용자가 체크 아웃한 자산을 하나 이상 선택합니다. [!DNL Assets]

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. 도구 모음에서 잠금 **[!UICONTROL 해제를 클릭합니다]**. 자산이 다시 체크 인되고 다른 사용자가 편집할 수 있습니다.

>[!MORELIKETHIS]
>
>* [Experience Manager 데스크탑 앱에서 체크 인 및 체크 아웃 이해](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#how-app-works2)
>* [자산 체크 인 및 체크 아웃을 이해하는 비디오 자습서](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/collaboration/checkin-checkout-technical-video-understand.html)

