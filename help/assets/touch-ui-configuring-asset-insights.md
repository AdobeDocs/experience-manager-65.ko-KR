---
title: 디지털 자산 사용 분석을 얻으려면 자산 통찰력을 구성합니다.
description: 에서 자산 통찰력을 [!DNL Adobe Experience Manager Assets]구성합니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: b59f7471ab9f3c5e6eb3365122262b592c8e6244
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 1%

---


# Configure Asset Insights {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] 타사 웹 사이트에서 사용되는 디지털 자산에 대한 사용 데이터를 가져옵니다 [!DNL Adobe Analytics]. 자산 인사이트에서 이 데이터를 검색하고 인사이트를 생성하려면 먼저 Adobe Analytics과 통합되도록 기능을 구성합니다.

>[!NOTE]
>
>인사이트는 이미지만 지원되고 제공됩니다.

1. 에서 [!DNL Experience Manager]도구 **[!UICONTROL >]** 자산을 **[!UICONTROL 클릭합니다]**.

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. 인사이트 **[!UICONTROL 구성]** 카드를 클릭합니다.
1. 마법사에서 데이터 센터를 선택하고 조직의 이름, 사용자 이름 및 공유 암호를 비롯한 자격 증명을 제공합니다.

   ![Experience Manager에서 자산 인사이트를 위한 Adobe Analytics 구성](assets/insights_config2.png)

   *그림: 자산 인사이트 구성[!DNL Adobe Analytics]을 참조하십시오[!DNL Experience Manager].*

1. 인증을 **[!UICONTROL 클릭합니다]**.
1. 자격 증명을 [!DNL Experience Manager] 인증한 후 **[!UICONTROL 보고서 세트]** 목록에서 자산 인사이트를 데이터 [!DNL Adobe Analytics] 로 가져올 보고서 세트를 선택합니다. **[!UICONTROL 추가]**&#x200B;를 클릭합니다.
1. 보고서 [!DNL Experience Manager] 세트를 설정한 후 완료를 **[!UICONTROL 클릭합니다]**.

## 페이지 추적기 {#page-tracker}

계정을 구성하면 [!DNL Adobe Analytics] 페이지 추적기 코드가 자동으로 생성됩니다. 자산 통찰력이 타사 웹 사이트에서 사용되는 [!DNL Experience Manager] 자산을 추적하도록 하려면 웹 사이트 코드에 페이지 추적기 코드를 포함시키십시오. 에서 [!UICONTROL 페이지 추적기] 유틸리티 [!DNL Experience Manager Assets] 를 사용하여 페이지 추적기 코드를 생성합니다. 타사 웹 페이지에 페이지 추적기 코드를 포함하는 방법에 대한 자세한 내용은 페이지 추적기 [사용 및 웹 페이지에 코드 포함을 참조하십시오](/help/assets/touch-ui-using-page-tracker.md).

1. 에서 [!DNL Experience Manager]도구 **[!UICONTROL >]** 자산을 **[!UICONTROL 클릭합니다]**.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. [ **[!UICONTROL 탐색]** ] 페이지에서 **[!UICONTROL 인사이트 페이지 추적기]** 카드를 클릭합니다.
1. 페이지 **[!UICONTROL 추적기]** 코드를 다운로드하려면 다운로드를 클릭합니다.
