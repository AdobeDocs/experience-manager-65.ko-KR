---
title: DTM을 통해 자산 통찰력 활성화
description: Adobe DTM(Dynamic Tag Management)을 사용하여 Assets Insights를 활성화하는 방법을 알아봅니다.
contentOwner: AG
role: User, Admin
feature: Asset Insights,Asset Reports
exl-id: 80e8f84e-3235-4212-9dcd-6acdb9067893
source-git-commit: 5e56441d2dc9b280547c91def8d971e7b1dfcfe3
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 2%

---

# DTM을 통해 자산 통찰력 활성화 {#enable-asset-insights-through-dtm}

Adobe 다이내믹 Tag Management은 디지털 마케팅 도구를 활성화하는 도구입니다. Adobe Analytics 고객에게 무료로 제공됩니다. 추적 코드를 사용자 지정하여 서드파티 CMS 솔루션에서 Assets Insights를 사용할 수 있도록 하거나 DTM을 사용하여 Assets Insights 태그를 삽입할 수 있습니다. 인사이트는 이미지만 지원되고 제공됩니다.

>[!CAUTION]
>
>Adobe DTM은 더 이상 사용되지 않으며 [!DNL Adobe Experience Platform] 및 은 곧 다음 위치에 도달합니다. [수명 종료](https://medium.com/launch-by-adobe/dtm-plans-for-a-sunset-3c6aab003a6f). Adobe은 다음을 권장합니다. [사용 [!DNL Adobe Experience Platform] 자산 통찰력용](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/asset-insights-launch-tutorial.html).

다음 단계를 수행하여 DTM을 통해 Assets Insights를 활성화합니다.

1. Experience Manager 로고를 클릭하고 **[!UICONTROL 도구]** > **[!UICONTROL 에셋]** > **[!UICONTROL Insights 구성]**.
1. [DTM Cloud Service을 사용하여 Experience Manager 배포 구성](/help/sites-administering/dtm.md)

   API 토큰은에 로그온하면 사용할 수 있습니다. [https://dtm.adobe.com](https://dtm.adobe.com/) 및 방문 **[!UICONTROL 계정 설정]** 사용자 프로필에서. 이 단계는 Experience Manager Sites과 Assets Insights의 통합이 아직 진행 중이므로 Assets Insights 관점에서 필요하지 않습니다.

1. 에 로그온 [https://dtm.adobe.com](https://dtm.adobe.com/)을 클릭하고 회사를 적절하게 선택합니다.
1. 기존 웹 속성 만들기 또는 열기

   * 다음 항목 선택 **[!UICONTROL 웹 속성]** 탭을 클릭한 다음 **[!UICONTROL 속성 추가]**.

   * 필드를 적절하게 업데이트한 다음 **[!UICONTROL 속성 만들기]**. 다음을 참조하십시오 [설명서](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html).

   ![편집 웹 속성 만들기](assets/Create-edit-web-property.png)

1. 다음에서 **[!UICONTROL 규칙]** 탭, 선택 **[!UICONTROL 페이지 로드 규칙]** 탐색 창에서 **[!UICONTROL 새 규칙 만들기]**.

   ![chlimage_1-58](assets/chlimage_1-194.png)

1. 확장 **[!UICONTROL JavaScript/타사 태그]**. 그런 다음 **[!UICONTROL 새 스크립트 추가]** 다음에서 **[!UICONTROL 순차적 HTML]** 탭으로 이동하여 스크립트 대화 상자를 엽니다.

   ![chlimage_1-59](assets/chlimage_1-195.png)

1. Experience Manager 로고를 클릭하고 **[!UICONTROL 도구]** > **[!UICONTROL 에셋]**.
1. 클릭 **[!UICONTROL Insights 페이지 추적기]**&#x200B;를 클릭하고 추적기 코드를 복사한 다음 6단계에서 연 스크립트 대화 상자에 붙여넣습니다. 변경 사항을 저장합니다.

   >[!NOTE]
   >
   >* `AppMeasurement.js` 이(가) 제거되었습니다. DTM의 Adobe Analytics 도구를 통해 사용할 수 있을 것으로 예상됩니다.
   >* 에 대한 호출 `assetAnalytics.dispatcher.init()` 이(가) 제거되었습니다. 함수는 DTM의 Adobe Analytics 도구 로드가 완료되면 호출됩니다.
   >* Assets Insights 페이지 추적기가 호스팅되는 위치 (예: Experience Manager, CDN 등)에 따라 스크립트 소스의 원본을 변경해야 할 수 있습니다.
   >* Experience Manager이 호스팅된 페이지 추적기의 경우 소스는 Dispatcher 인스턴스의 호스트 이름을 사용하는 게시 인스턴스를 가리켜야 합니다.

1. 액세스 `https://dtm.adobe.com`. 클릭 **[!UICONTROL 개요]** 웹 속성에서 **[!UICONTROL 도구 추가]** 또는 기존 Adobe Analytics 도구를 엽니다. 도구를 만드는 동안 다음을 설정할 수 있습니다 **[!UICONTROL 구성 메서드]** 끝 **[!UICONTROL 자동]**.

   ![Adobe Analytics 도구 추가](assets/Add-Adobe-Analytics-Tool.png)

   필요에 따라 스테이징/프로덕션 보고서 세트를 선택합니다.

1. 확장 **[!UICONTROL 라이브러리 관리]**, 및 다음을 확인합니다 **[!UICONTROL 다음 위치에 라이브러리 로드]** 이(가) (으)로 설정됨 **[!UICONTROL 페이지 상단]**.

   ![chlimage_1-61](assets/chlimage_1-197.png)

1. 확장 **[!UICONTROL 페이지 코드 사용자 지정]**, 및 클릭 **[!UICONTROL 편집기 열기]**.

   ![chlimage_1-62](assets/chlimage_1-198.png)

1. 창에 다음 코드를 붙여넣습니다.

   ```Java
   var sObj;
   
   if (arguments.length > 0) {
     sObj = arguments[0];
   } else {
     sObj = _satellite.getToolsByType('sc')[0].getS();
   }
   _satellite.notify('in assetAnalytics customInit');
   (function initializeAssetAnalytics() {
     if ((!!window.assetAnalytics) && (!!assetAnalytics.dispatcher)) {
       _satellite.notify('assetAnalytics ready');
       /** NOTE:
           Copy over the call to 'assetAnalytics.dispatcher.init()' from Assets Pagetracker
           Be mindful about changing the AppMeasurement object as retrieved above.
       */
       assetAnalytics.dispatcher.init(
             "",  /** RSID to send tracking-call to */
             "",  /** Tracking Server to send tracking-call to */
             "",  /** Visitor Namespace to send tracking-call to */
             "",  /** listVar to put comma-separated-list of Asset IDs for Asset Impression Events in tracking-call, for example, 'listVar1' */
             "",  /** eVar to put Asset ID for Asset Click Events in, for example, 'eVar3' */
             "",  /** event to include in tracking-calls for Asset Impression Events, for example, 'event8' */
             "",  /** event to include in tracking-calls for Asset Click Events, for example, 'event7' */
             sObj  /** [OPTIONAL] if the webpage already has an AppMeasurement object, include the object here. If unspecified, Pagetracker Core shall create its own AppMeasurement object */
             );
       sObj.usePlugins = true;
       sObj.doPlugins = assetAnalytics.core.updateContextData;
       assetAnalytics.core.optimizedAssetInsights();
     }
     else {
       _satellite.notify('assetAnalytics not available. Consider updating the Custom Page Code', 4);
     }
   })();
   ```

   * DTM의 페이지 로드 규칙에는 `pagetracker.js` 코드. 임의 `assetAnalytics` 필드는 기본값에 대한 재정의로 간주됩니다. 기본적으로 필요하지 않습니다.
   * 코드 호출 `assetAnalytics.dispatcher.init()` 다음을 확인: `_satellite.getToolsByType('sc')[0].getS()` 초기화되고 `assetAnalytics,dispatcher.init` 을(를) 사용할 수 있습니다. 따라서 11단계에서 추가를 건너뛸 수 있습니다.
   * Insights 페이지 추적기 코드 내의 주석에 표시된 대로(**[!UICONTROL 도구 > 자산 > 통찰력 페이지 추적기]**), 페이지 추적기에서 `AppMeasurement` 개체, 처음 세 개의 인수(RSID, 추적 서버 및 방문자 네임스페이스)는 관련이 없습니다. 빈 문자열이 대신 전달되어 강조 표시됩니다.\
     나머지 인수는 Insights 구성 페이지에서 구성된 인수 (**[!UICONTROL 도구 > 에셋 > Insights 구성]**).
   * AppMeasurement 개체는 쿼리를 통해 검색됩니다. `satelliteLib` 사용 가능한 모든 SiteCatalyst 엔진에 사용됩니다. 여러 태그가 구성된 경우 배열 선택기의 인덱스를 적절하게 변경합니다. 배열의 항목은 DTM 인터페이스에서 사용할 수 있는 SiteCatalyst 도구에 따라 순서가 지정됩니다.

1. 코드 편집기 창을 저장하고 닫은 다음 도구 구성의 변경 사항을 저장합니다.
1. 다음에서 **[!UICONTROL 승인]** 탭에서 보류 중인 승인을 모두 승인합니다. DTM 태그를 웹 페이지에 삽입할 준비가 되었습니다.
