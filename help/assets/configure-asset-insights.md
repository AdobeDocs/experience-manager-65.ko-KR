---
title: 분석을 가져오도록 자산 통찰력을 구성합니다.
description: 에서 자산 통찰력 구성 [!DNL Adobe Experience Manager Assets].
contentOwner: AG
role: Architect, Admin
feature: Asset Insights,Asset Reports
exl-id: 67be0ae6-5939-40fe-bf8a-b8a2c2f68f15
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 7%

---

# 자산 통찰력 구성 {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] 에서는 타사 웹 사이트에서 사용하는 디지털 자산에 대한 사용 데이터를 [!DNL Adobe Analytics]. 자산 인사이트에서 이 데이터를 검색하고 인사이트를 생성하려면 먼저 와 통합하도록 기능을 구성합니다 [!DNL Adobe Analytics]. 온-프레미스 설치에서 이 기능을 사용하려면 를 구입하십시오 [!DNL Adobe Analytics] 라이센스를 별도로 지정합니다. 고객이 [!DNL Managed Services] 수신 [!DNL Analytics] 번들로 제공되는 라이선스 [!DNL Experience Manager]. 자세한 내용은 [Managed Services 제품 설명](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html).

>[!NOTE]
>
>인사이트는 이미지에서만 지원되고 제공됩니다.

1. in [!DNL Experience Manager]를 클릭합니다. **[!UICONTROL 도구]** > **[!UICONTROL 자산]**.

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. Click the **[!UICONTROL Insights Configuration]** card.
1. 마법사에서 데이터 센터를 선택하고 조직 이름, 사용자 이름 및 공유 암호가 포함된 자격 증명을 제공합니다.

   ![Experience Manager에서 자산 통찰력에 대한 Adobe Analytics 구성](assets/insights_config2.png)

   *그림: 구성 [!DNL Adobe Analytics] 의 자산 통찰력에 대해 [!DNL Experience Manager].*

1. 클릭 **[!UICONTROL 인증]**.
1. 후 [!DNL Experience Manager] 에서 자격 증명을 인증합니다. **[!UICONTROL 보고서 세트]** 목록, 선택 [!DNL Adobe Analytics] 자산 통찰력 이 데이터를 가져오려는 위치의 보고서 세트입니다. **[!UICONTROL 추가]**&#x200B;를 클릭합니다.
1. 후 [!DNL Experience Manager] 보고서 세트를 설정하고 **[!UICONTROL 완료]**.

## 페이지 추적기 {#page-tracker}

구성 후 [!DNL Adobe Analytics] 계정이 만들어지면 페이지 추적기 코드가 생성됩니다. Assets Insights가 추적하도록 하려면 다음을 수행하십시오 [!DNL Experience Manager] 타사 웹 사이트에서 사용되는 자산은 웹 사이트 코드에 페이지 추적기 코드를 포함합니다. 를 사용하십시오 [!UICONTROL 페이지 추적기] 의 유틸리티 [!DNL Experience Manager Assets] 를 입력하여 페이지 추적기 코드를 생성합니다. 타사 웹 페이지에 페이지 추적기 코드를 포함하는 방법에 대한 자세한 내용은 다음을 참조하십시오 [웹 페이지에 페이지 추적기 및 포함 코드 사용](/help/assets/use-page-tracker.md).

1. in [!DNL Experience Manager]를 클릭합니다. **[!UICONTROL 도구]** > **[!UICONTROL 자산]**.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. From the **[!UICONTROL Navigation]** page, click the **[!UICONTROL Insights Page Tracker]** card.
1. 클릭 **[!UICONTROL 다운로드]** 를 클릭하여 페이지 추적기 코드를 다운로드합니다.
