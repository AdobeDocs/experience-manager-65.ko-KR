---
title: 분석을 가져오도록 자산 통찰력을 구성합니다.
description: ' [!DNL Adobe Experience Manager Assets]에서 자산 통찰력을 구성합니다.'
contentOwner: AG
role: Architect, Administrator
feature: 자산 통찰력,자산 보고서
exl-id: 67be0ae6-5939-40fe-bf8a-b8a2c2f68f15
source-git-commit: c07467feb96c25a4bac1916f88f04fdb37979ee1
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 1%

---

# 자산 통찰력 구성 {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] 에서는 타사 웹 사이트에서 사용하는 디지털 자산에 대한 사용 데이터를  [!DNL Adobe Analytics]가져옵니다. 자산 통찰력 이 데이터를 검색하고 인사이트를 생성하려면 먼저 [!DNL Adobe Analytics]과 통합하도록 기능을 구성합니다. 이 기능을 사용하려면 [!DNL Adobe Analytics] 라이센스를 별도로 구입하십시오. [!DNL Managed Services] 의 고객은 [!DNL Experience Manager]와 번들로 제공되는 [!DNL Analytics] 라이센스를 받습니다. [Managed Services 제품 설명](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html)을 참조하십시오.

>[!NOTE]
>
>인사이트는 이미지에서만 지원되고 제공됩니다.

1. [!DNL Experience Manager]에서 **[!UICONTROL 도구]** > **[!UICONTROL 자산]**&#x200B;을 클릭합니다.

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. **[!UICONTROL 인사이트 구성]** 카드를 클릭합니다.
1. 마법사에서 데이터 센터를 선택하고 조직 이름, 사용자 이름 및 공유 암호가 포함된 자격 증명을 제공합니다.

   ![Experience Manager에서 자산 통찰력에 대한 Adobe Analytics 구성](assets/insights_config2.png)

   *그림:에서  [!DNL Adobe Analytics] 자산 통찰력에 대한 을  [!DNL Experience Manager]구성합니다.*

1. **[!UICONTROL 인증]**&#x200B;을 클릭합니다.
1. [!DNL Experience Manager]이 자격 증명을 인증하면 **[!UICONTROL 보고서 세트]** 목록에서 자산 통찰력이 데이터를 가져오려는 곳에서 [!DNL Adobe Analytics] 보고서 세트를 선택합니다. **[!UICONTROL 추가]**&#x200B;를 클릭합니다.
1. [!DNL Experience Manager] 보고서 세트를 설정한 후에 **[!UICONTROL 완료]**&#x200B;를 클릭합니다.

## 페이지 추적기 {#page-tracker}

[!DNL Adobe Analytics] 계정을 구성하면 페이지 추적기 코드가 생성됩니다. 자산 통찰력 이 타사 웹 사이트에서 사용되는 [!DNL Experience Manager] 자산을 추적하도록 하려면 웹 사이트 코드에 페이지 추적기 코드를 포함하십시오. [!DNL Experience Manager Assets]에서 [!UICONTROL 페이지 추적기] 유틸리티를 사용하여 페이지 추적기 코드를 생성합니다. 타사 웹 페이지에 페이지 추적기 코드를 포함하는 방법에 대한 자세한 내용은 [웹 페이지에 페이지 추적기 및 포함 코드 사용](/help/assets/use-page-tracker.md)을 참조하십시오.

1. [!DNL Experience Manager]에서 **[!UICONTROL 도구]** > **[!UICONTROL 자산]**&#x200B;을 클릭합니다.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. **[!UICONTROL 탐색]** 페이지에서 **[!UICONTROL 인사이트 페이지 추적기]** 카드를 클릭합니다.
1. **[!UICONTROL 다운로드]**&#x200B;를 클릭하여 페이지 추적기 코드를 다운로드합니다.
