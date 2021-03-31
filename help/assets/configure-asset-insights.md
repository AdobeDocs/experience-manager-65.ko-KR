---
title: 분석을 얻기 위해 자산 통찰력을 구성합니다.
description: ' [!DNL Adobe Experience Manager Assets]에서 자산 인사이트를 구성합니다.'
contentOwner: AG
role: 건축가, 관리자
feature: 자산 통찰력,자산 보고서
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 1%

---


# 자산 인사이트 구성 {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] 제3자 웹 사이트에서 사용하는 디지털 자산에 대한 사용 데이터를  [!DNL Adobe Analytics] 자산 인사이트에서 이 데이터를 검색하고 인사이트를 생성하려면 먼저 Adobe Analytics과 통합할 기능을 구성합니다.

>[!NOTE]
>
>인사이트는 이미지만 지원되고 제공됩니다.

1. [!DNL Experience Manager]에서 **[!UICONTROL 도구]** > **[!UICONTROL 자산]**&#x200B;을 클릭합니다.

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. **[!UICONTROL 인사이트 구성]** 카드를 클릭합니다.
1. 마법사에서 데이터 센터를 선택하고 조직의 이름, 사용자 이름 및 공유 암호를 포함한 자격 증명을 제공합니다.

   ![Experience Manager에서 자산 인사이트에 대한 Adobe Analytics 구성](assets/insights_config2.png)

   *그림:자산  [!DNL Adobe Analytics] 인사이트에 대한 구성을 참조하십시오 [!DNL Experience Manager].*

1. **[!UICONTROL 인증]**&#x200B;을 클릭합니다.
1. [!DNL Experience Manager]이(가) 자격 증명을 인증한 후 **[!UICONTROL 보고서 세트]** 목록에서 자산 통찰력을 가져올 [!DNL Adobe Analytics] 보고서 세트를 선택합니다. **[!UICONTROL 추가]**&#x200B;를 클릭합니다.
1. [!DNL Experience Manager] 보고서 세트를 설정한 후 **[!UICONTROL 완료]**&#x200B;를 클릭합니다.

## 페이지 추적기 {#page-tracker}

[!DNL Adobe Analytics] 계정을 구성하면 페이지 추적기 코드가 자동으로 생성됩니다. 자산 인사이트를 사용하여 타사 웹 사이트에 사용된 [!DNL Experience Manager] 자산을 추적하려면 웹 사이트 코드에 페이지 추적기 코드를 포함하십시오. [!DNL Experience Manager Assets]에서 [!UICONTROL 페이지 추적기] 유틸리티를 사용하여 페이지 추적기 코드를 생성합니다. 타사 웹 페이지에 페이지 추적기 코드를 포함하는 방법에 대한 자세한 내용은 [페이지 추적기 사용 및 웹 페이지에 포함 코드](/help/assets/use-page-tracker.md)를 참조하십시오.

1. [!DNL Experience Manager]에서 **[!UICONTROL 도구]** > **[!UICONTROL 자산]**&#x200B;을 클릭합니다.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. **[!UICONTROL 탐색]** 페이지에서 **[!UICONTROL 인사이트 페이지 추적기]** 카드를 클릭합니다.
1. 페이지 추적기 코드를 다운로드하려면 **[!UICONTROL 다운로드]**&#x200B;를 클릭합니다.
