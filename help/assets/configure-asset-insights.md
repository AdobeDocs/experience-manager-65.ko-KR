---
title: Analytics를 가져오도록 Assets Insights 를 구성합니다.
description: '[!DNL Adobe Experience Manager Assets]에서 Assets Insights를 구성합니다.'
contentOwner: AG
role: Developer, Admin
feature: Asset Insights,Asset Reports
exl-id: 67be0ae6-5939-40fe-bf8a-b8a2c2f68f15
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: a4e1c1f5-18fc-592e-bfc7-453ce6ae0030
    internal-label: Asset Insights
  - id: ac365bec-0634-4744-9473-c42f47320593
    internal-label: Asset management and governance
subfeature_v2:
  - id: c29e3a96-cd2b-4e21-b382-a8279aa04553
    internal-label: Asset reports
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 7%
---
# Assets 통찰력 구성 {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets]은(는) [!DNL Adobe Analytics]에서 서드파티 웹 사이트에서 사용하는 디지털 자산에 대한 사용 데이터를 가져옵니다. Assets Insights를 사용하여 이 데이터를 검색하고 인사이트를 생성하려면 먼저 [!DNL Adobe Analytics]과(와) 통합되도록 기능을 구성하십시오. 온-프레미스 설치에서 이 기능을 사용하려면 별도로 [!DNL Adobe Analytics] 라이선스를 구입하세요. [!DNL Managed Services]의 고객은 [!DNL Experience Manager]과(와) 번들로 제공되는 [!DNL Analytics] 라이선스를 받습니다. [Managed Services 제품 설명](https://helpx.adobe.com/kr/legal/product-descriptions/adobe-experience-manager-managed-services.html)을 참조하세요.

>[!NOTE]
>
>인사이트는 이미지만 지원되고 제공됩니다.

1. [!DNL Experience Manager]에서 **[!UICONTROL 도구]** > **[!UICONTROL Assets]**&#x200B;을(를) 클릭합니다.

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. Click the **[!UICONTROL Insights Configuration]** card.
1. 마법사에서 데이터 센터를 선택하고 조직 이름, 사용자 이름 및 공유 암호를 포함한 자격 증명을 제공합니다.

   ![Experience Manager에서 Assets Insights용 Adobe Analytics 구성](assets/insights_config2.png)

   *그림: [!DNL Experience Manager]에서 Assets Insights에 대해 [!DNL Adobe Analytics] 구성.*

1. **[!UICONTROL 인증]**&#x200B;을 클릭합니다.
1. [!DNL Experience Manager]에서 자격 증명을 인증한 후 **[!UICONTROL 보고서 세트]** 목록에서 Assets Insights에서 데이터를 가져올 [!DNL Adobe Analytics] 보고서 세트를 선택하십시오. **[!UICONTROL 추가]**&#x200B;를 클릭합니다.
1. [!DNL Experience Manager]이(가) 보고서 세트를 설정한 후 **[!UICONTROL 완료]**&#x200B;를 클릭합니다.

## 페이지 추적기 {#page-tracker}

[!DNL Adobe Analytics] 계정을 구성하면 페이지 추적기 코드가 생성됩니다. Assets Insights를 사용하여 서드파티 웹 사이트에서 사용되는 [!DNL Experience Manager]개의 자산을 추적할 수 있도록 하려면 웹 사이트 코드에 페이지 추적기 코드를 포함하십시오. [!DNL Experience Manager Assets]에서 [!UICONTROL 페이지 추적기] 유틸리티를 사용하여 페이지 추적기 코드를 생성합니다. 타사 웹 페이지에 페이지 추적기 코드를 포함하는 방법에 대한 자세한 내용은 [웹 페이지에 페이지 추적기 및 포함 코드 사용](/help/assets/use-page-tracker.md)을 참조하십시오.

1. [!DNL Experience Manager]에서 **[!UICONTROL 도구]** > **[!UICONTROL Assets]**&#x200B;을(를) 클릭합니다.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. From the **[!UICONTROL Navigation]** page, click the **[!UICONTROL Insights Page Tracker]** card.
1. **[!UICONTROL 다운로드]**&#x200B;를 클릭하여 페이지 추적기 코드를 다운로드합니다.
