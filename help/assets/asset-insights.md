---
title: Assets Insights
description: Assets Insights 기능을 사용하여 타사 웹 사이트, 마케팅 캠페인 및 Adobe의 광고 솔루션에서 사용되는 이미지의 사용자 등급 및 사용 통계를 추적하는 방법에 대해 알아봅니다.
contentOwner: AG
role: User, Admin
feature: Asset Insights,Asset Reports
exl-id: 0130ac40-a72b-4caf-a10f-3c7d76eaa1e6
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 9%

---

# Assets Insights {#asset-insights}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/assets-insights.html?lang=en) |
| AEM 6.5 | 이 문서 |

Assets Insights 기능을 사용하면 타사 웹 사이트, 마케팅 캠페인 및 Adobe의 광고 솔루션에서 사용되는 이미지의 사용자 등급 및 사용 통계를 추적할 수 있습니다. 이는 성능 및 인기에 대한 통찰력을 도출하는 데 도움이 됩니다.

[!DNL Assets] Insights는 이미지에 대한 등급, 클릭 횟수 및 노출 횟수(이미지가 웹 사이트에 로드되는 횟수) 등 사용자 활동 세부 정보를 캡처합니다. 이러한 통계를 기반으로 이미지에 점수를 할당합니다. 점수 및 성과 통계를 사용하여 카탈로그, 마케팅 캠페인 등에 포함할 인기 있는 이미지를 선택할 수 있습니다. 이러한 통계를 기반으로 아카이브 및 라이선스 갱신 정책을 수립할 수도 있습니다.

대상 [!DNL Assets] 웹 사이트의 이미지에 대한 사용 통계를 캡처하려면 웹 사이트 코드에 이미지에 대한 포함 코드를 포함해야 합니다.

Assets Insights에서 에셋에 대한 사용 통계를 표시하도록 하려면 먼저 Adobe Analytics에서 보고 데이터를 가져오도록 기능을 구성합니다. 자세한 내용은 [자산 통찰력 구성](/help/assets/configure-asset-insights.md). 온-프레미스 설치에서 이 기능을 사용하려면 [!DNL Adobe Analytics] 별도로 라이센스 부여 의 고객 [!DNL Managed Services] 수신 [!DNL Analytics] 와 번들로 제공되는 라이선스 [!DNL Experience Manager]. 다음을 참조하십시오 [Managed Services 제품 설명](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html).

>[!NOTE]
>
>인사이트는 이미지만 지원되고 제공됩니다.

## 이미지에 대한 통계 보기 {#viewing-statistics-for-an-image}

메타데이터 페이지에서 Assets Insights 점수를 볼 수 있습니다.

1. 다음에서 [!DNL Assets] UI(사용자 인터페이스)에서 이미지를 선택한 다음 **[!UICONTROL 속성]** 을 클릭합니다.
1. Properties 페이지에서 **[!UICONTROL Insights]** 탭.
1. 에서 에셋에 대한 사용 세부 사항을 검토합니다. **[!UICONTROL Insights]** 탭. 다음 **[!UICONTROL 점수]** 섹션은 에셋의 총 에셋 사용 및 성능 저장에 대해 설명합니다.

   사용 점수는 다양한 솔루션에서 에셋이 사용된 횟수를 설명합니다.

   다음 **[!UICONTROL 노출 횟수]** score는 웹 사이트에 자산이 로드된 횟수입니다. 아래에 표시된 번호 **[!UICONTROL 클릭수]** 는 에셋을 클릭한 횟수입니다.

1. 리뷰 **[!UICONTROL 사용 통계]** 섹션이 에셋이 속한 엔티티와 최근에 사용한 크리에이티브 솔루션에 대해 알아봅니다. 사용량이 많을수록 해당 자산이 사용자들 사이에서 인기를 끌 가능성도 커진다. 사용 데이터는 다음 헤드 아래에 표시됩니다.

   * **자산**: 에셋이 컬렉션 또는 복합 에셋에 포함된 횟수
   * **웹 및 모바일**: 자산이 웹 사이트 및 앱에 포함된 횟수
   * **소셜**: Adobe Social 및 Adobe Campaign과 같은 솔루션에서 에셋이 사용된 횟수
   * **이메일**: 이메일 캠페인에서 에셋이 사용된 횟수

   ![usage_statistics](assets/usage_statistics.png)

   >[!NOTE]
   >
   >Assets Insights 기능은 일반적으로 Adobe Analytics에서 솔루션 데이터를 정기적으로 가져오기 때문에 솔루션 섹션에는 최신 데이터가 표시되지 않을 수 있습니다. 데이터가 표시되는 기간은 Assets Insights에서 Analytics 데이터를 검색하기 위해 실행하는 가져오기 작업의 일정에 따라 다릅니다.

1. To view performance statistics for the asset graphically over a period of time, select period in the **[!UICONTROL Performance Statistics]** section. Details, including clicks and impressions are displayed as trend lines of a graph.

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >솔루션 섹션의 데이터와 달리 성능 통계 섹션에는 가장 최근 데이터가 표시됩니다.

1. 웹 사이트에 포함하여 성능 데이터를 가져오는 에셋에 대한 포함 코드를 얻으려면 다음을 클릭합니다. **[!UICONTROL 포함 코드 가져오기]** 자산 썸네일 아래에 있습니다. 타사 웹 페이지에 포함 코드를 포함하는 방법에 대한 자세한 내용은 [웹 페이지에서 페이지 추적기 및 포함 코드 사용](/help/assets/use-page-tracker.md).

   ![chlimage_1-98](assets/chlimage_1-303.png)

## 이미지에 대한 집계 통계 보기 {#viewing-aggregate-statistics-for-images}

You can view scores of all assets within a folder simultaneously using **[!UICONTROL Insights View]**.

1. 다음에서 [!DNL Assets] 사용자 인터페이스에서 인사이트를 보려는 자산이 포함된 폴더로 이동합니다.
1. 도구 모음에서 레이아웃 을 클릭한 다음 **[!UICONTROL 인사이트 보기]**.
1. 페이지에 에셋에 대한 사용 점수가 표시됩니다. 다양한 에셋의 등급을 비교하고 통찰력을 도출합니다.

## 백그라운드 작업 예약 {#scheduling-background-job}

Assets Insights는 정기적으로 Adobe Analytics 보고서 세트의 자산에 대한 사용 데이터를 가져옵니다. 기본적으로 Assets Insights는 오전 2시에 24시간마다 백그라운드 작업을 실행하여 데이터를 가져옵니다. 그러나 를 구성하여 빈도와 시간을 모두 수정할 수 있습니다. **[!UICONTROL Adobe CQ DAM 자산 성능 보고서 동기화 작업]** 웹 콘솔의 서비스입니다.

1. 다음을 클릭합니다. [!DNL Experience Manager] 로고 및 다음으로 이동 **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 웹 콘솔]**.
1. 를 엽니다. **[!UICONTROL Adobe CQ DAM 자산 성능 보고서 동기화 작업]** 서비스 구성.

   ![chlimage_1-99](assets/chlimage_1-304.png)

1. 속성 스케줄러 표현식에서 원하는 스케줄러 빈도와 작업 시작 시간을 지정합니다. 변경 사항을 저장합니다.
