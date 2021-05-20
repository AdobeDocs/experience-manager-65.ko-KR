---
title: ' [!DNL Assets]에서 파일 체크인 및 체크아웃'
description: 편집할 자산을 확인하고 변경 사항이 완료되면 다시 체크 인하는 방법을 알아봅니다.
contentOwner: AG
role: Business Practitioner
feature: 자산 관리
exl-id: 544ef73c-4e4b-433f-a173-fdf1c8f45d8e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 1%

---

# [!DNL Experience Manager] DAM {#check-in-and-check-out-files-in-assets}의 체크인 및 체크아웃 파일

[!DNL Adobe Experience Manager Assets] 편집할 자산을 확인하고 변경을 완료한 후 다시 체크 인할 수 있습니다. 자산을 체크 아웃한 후에는 자산을 편집, 주석 달기, 게시, 이동 또는 삭제할 수만 있습니다. 자산을 체크 아웃하면 자산이 잠깁니다. 다른 사용자는 자산을 다시 [!DNL Assets]에 체크 인할 때까지 자산에서 이러한 작업을 수행할 수 없습니다. 그러나 잠긴 자산에 대한 메타데이터를 변경할 수 있습니다.

자산을 체크 아웃/체크 인하려면 자산에 대한 쓰기 액세스 권한이 필요합니다.

이 기능은 여러 사용자가 여러 팀 간의 워크플로우 편집에서 공동 작업하는 작성자가 변경한 내용을 다른 사용자가 덮어쓰지 않도록 하는 데 도움이 됩니다.

## 자산 확인 {#checking-out-assets}

1. [!DNL Assets] 사용자 인터페이스에서 체크 아웃할 자산을 선택합니다. 여러 자산을 선택하여 체크아웃할 수도 있습니다.
1. 도구 모음에서 **[!UICONTROL 체크아웃]**&#x200B;을 클릭합니다. **[!UICONTROL Checkout]** 옵션은 **[!UICONTROL Checkin]**으로 전환합니다.
다른 사용자가 체크 아웃한 자산을 편집할 수 있는지 확인하려면 다른 사용자로 로그인합니다. 체크 아웃한 자산의 축소판에 잠금 기호가 표시됩니다.

   ![chlimage_1-471](assets/chlimage_1-471.png)

   자산을 선택합니다. 도구 모음에는 자산을 편집, 주석 달기, 게시 또는 삭제할 수 있는 옵션이 표시되지 않습니다.

   ![chlimage_1-472](assets/chlimage_1-472.png)

   잠긴 자산의 메타데이터를 편집하려면 **[!UICONTROL 속성 보기]**&#x200B;를 클릭합니다.

1. **[!UICONTROL 편집]**&#x200B;을 클릭하여 자산을 편집 모드로 엽니다.

   ![chlimage_1-473](assets/chlimage_1-473.png)

1. 자산을 편집하고 변경 사항을 저장합니다. 예를 들어, 이미지를 자르거나 저장합니다.

   ![chlimage_1-474](assets/chlimage_1-474.png)

   자산에 주석을 달거나 게시하도록 선택할 수도 있습니다.

1. [!DNL Assets] 인터페이스에서 편집된 자산을 선택하고 도구 모음에서 **[!UICONTROL 체크 인]**&#x200B;을 클릭합니다. 수정된 자산은 [!DNL Assets]에 체크 인되며, 다른 사용자가 편집할 수 있습니다.

## {#forced-check-in} 강제 체크 인

관리자는 다른 사용자가 체크 아웃한 자산을 체크 인할 수 있습니다.

1. 관리자로 [!DNL Assets]에 로그인합니다.
1. [!DNL Assets] 사용자 인터페이스에서 다른 사용자가 체크 아웃한 자산을 한 개 이상 선택합니다.

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. 도구 모음에서 **[!UICONTROL 잠금 해제]**&#x200B;를 클릭합니다. 자산이 다시 체크 인되고 다른 사용자가 편집할 수 있습니다.

## 우수 사례 및 제한 사항 {#tips-limitations}

* 체크 아웃된 자산 파일이 포함된 *폴더*&#x200B;를 삭제할 수 있습니다. 폴더를 삭제하기 전에 사용자가 디지털 자산을 체크 아웃하지 않았는지 확인합니다.

>[!MORELIKETHIS]
>
>* [데스크탑 앱의 체크인 및  [!DNL Experience Manager] 체크아웃 이해](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=en#how-app-works2)
>* [체크인 및 체크아웃 이해 비디오 튜토리얼 [!DNL Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/collaboration/check-in-and-check-out.html)

