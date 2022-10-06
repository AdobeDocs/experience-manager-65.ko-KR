---
title: DTM을 통해 자산 통찰력 활성화
description: Dynamic Tag Management(DTM) Adobe을 사용하여 자산 통찰력을 활성화하는 방법을 알아봅니다.
contentOwner: AG
role: User, Admin
feature: Asset Insights,Asset Reports
exl-id: 80e8f84e-3235-4212-9dcd-6acdb9067893
source-git-commit: afc72fb6b324cf2e0ad8168f783d9c1a6f96c614
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 2%

---

# DTM을 통해 자산 통찰력 활성화 {#enable-asset-insights-through-dtm}

Adobe Dynamic Tag Management 는 디지털 마케팅 도구를 활성화하는 도구입니다. Adobe Analytics 고객에게 무료로 제공됩니다. 추적 코드를 사용자 지정하여 타사 CMS 솔루션에서 자산 통찰력을 사용할 수 있도록 하거나 DTM을 사용하여 자산 통찰력 태그를 삽입할 수 있습니다. 인사이트는 이미지에서만 지원되고 제공됩니다.

>[!CAUTION]
>
>Adobe DTM은 더 이상 사용되지 않으며, [!DNL Adobe Experience Platform] 곧 [인생의 끝](https://medium.com/launch-by-adobe/dtm-plans-for-a-sunset-3c6aab003a6f). Adobe은 다음을 수행하는 것을 권장합니다. [사용 [!DNL Adobe Experience Platform] assets insights](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/asset-insights-launch-tutorial.html).

다음 단계를 수행하여 DTM을 통해 자산 통찰력을 활성화합니다.

1. Experience Manager 로고를 클릭하고 **[!UICONTROL 도구]** > **[!UICONTROL 자산]** > **[!UICONTROL 통찰력 구성]**.
1. [DTM Cloud Service을 사용하여 Experience Manager 배포 구성](/help/sites-administering/dtm.md)

   API 토큰은 다음에 로그인하면 사용할 수 있습니다 [https://dtm.adobe.com](https://dtm.adobe.com/) 및 방문 **[!UICONTROL 계정 설정]** ( 사용자 프로필) 아래에 그룹화됩니다. Assets Insights와 Experience Manager Sites의 통합이 아직 작동 중이기 때문에 이 단계는 자산 통찰력 측면에서 필요하지 않습니다.

1. 에 로그온 [https://dtm.adobe.com](https://dtm.adobe.com/), 그리고 회사를 적절하게 선택합니다.
1. 기존 웹 속성 만들기 또는 열기

   * 을(를) 선택합니다 **[!UICONTROL 웹 속성]** 탭을 클릭한 다음 **[!UICONTROL 속성 추가]**.

   * 필드를 적절하게 업데이트한 다음 **[!UICONTROL 속성 만들기]**. 자세한 내용은 [설명서](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html).

   ![웹 속성 편집 만들기](assets/Create-edit-web-property.png)

1. 에서 **[!UICONTROL 규칙]** 탭, 선택 **[!UICONTROL 페이지 로드 규칙]** 탐색 창에서 **[!UICONTROL 새 규칙 만들기]**.

   ![chlimage_1-58](assets/chlimage_1-194.png)

1. 확장 **[!UICONTROL JavaScript/타사 태그]**. 그런 다음 **[!UICONTROL 새 스크립트 추가]** 에서 **[!UICONTROL 순차적 HTML]** 탭을 클릭하여 스크립트 대화 상자를 엽니다.

   ![chlimage_1-59](assets/chlimage_1-195.png)

1. Experience Manager 로고를 클릭하고 **[!UICONTROL 도구]** > **[!UICONTROL 자산]**.
1. 클릭 **[!UICONTROL 통찰력 페이지 추적기]**&#x200B;를 사용하여 추적기 코드를 복사한 다음 6단계에서 연 스크립트 대화 상자에 붙여넣습니다. 변경 사항을 저장합니다.

   >[!NOTE]
   >
   >* `AppMeasurement.js` 가 제거되었습니다. DTM의 Adobe Analytics 도구를 통해 사용할 수 있습니다.
   >* 호출 `assetAnalytics.dispatcher.init()` 가 제거되었습니다. 함수는 DTM의 Adobe Analytics 도구 로드가 완료되면 호출됩니다.
   >* Assets Insights 페이지 추적기가 호스팅되는 위치(예: Experience Manager, CDN 등)에 따라 스크립트 소스의 출처를 변경해야 할 수 있습니다.
   >* Experience Manager이 호스팅하는 페이지 추적기의 경우 소스는 디스패처 인스턴스의 호스트 이름을 사용하여 게시 인스턴스를 가리켜야 합니다.


1. 액세스 `https://dtm.adobe.com`. 클릭 **[!UICONTROL 개요]** 웹 속성에서 **[!UICONTROL 도구 추가]** 기존 Adobe Analytics 도구를 엽니다. 도구를 만드는 동안 **[!UICONTROL 구성 방법]** to **[!UICONTROL 자동]**.

   ![Adobe Analytics 도구 추가](assets/Add-Adobe-Analytics-Tool.png)

   필요에 따라 스테이징/프로덕션 보고서 세트를 선택합니다.

1. 확장 **[!UICONTROL 라이브러리 관리]**, 및 **[!UICONTROL 라이브러리 로드 위치]** 가 로 설정되어 있습니다. **[!UICONTROL 페이지 상단]**.

   ![chlimage_1-61](assets/chlimage_1-197.png)

1. 확장 **[!UICONTROL 페이지 코드 사용자 지정]**&#x200B;를 클릭하고 **[!UICONTROL 편집기 열기]**.

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
             "",  /** listVar to put comma-separated-list of Asset IDs for Asset Impression Events in tracking-call, e.g. 'listVar1' */
             "",  /** eVar to put Asset ID for Asset Click Events in, e.g. 'eVar3' */
             "",  /** event to include in tracking-calls for Asset Impression Events, e.g. 'event8' */
             "",  /** event to include in tracking-calls for Asset Click Events, e.g. 'event7' */
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

   * DTM의 페이지 로드 규칙은 `pagetracker.js` 코드가 있어야 합니다. 임의 `assetAnalytics` 필드는 기본값 재정의로 간주됩니다. 기본적으로 필요하지 않습니다.
   * 코드 호출 `assetAnalytics.dispatcher.init()` 그 후에 `_satellite.getToolsByType('sc')[0].getS()` 초기화된 후 `assetAnalytics,dispatcher.init` 사용할 수 있습니다. 따라서 11단계에서 추가하지 않아도 됩니다.
   * 인사이트 페이지 추적기 코드(**[!UICONTROL 도구 > 자산 > 통찰력 페이지 추적기]**)가 있어야 합니다. `AppMeasurement` 개체의 첫 번째 세 개 인수(RSID, 추적 서버 및 방문자 네임스페이스)는 관련이 없습니다. 대신 빈 문자열이 전달되어 이 강조 표시됩니다.\
      나머지 인수는 인사이트 구성 페이지에 구성된 것에 해당합니다(**[!UICONTROL 도구 > 자산 > 통찰력 구성]**).
   * AppMeasurement 개체는 쿼리를 통해 검색됩니다 `satelliteLib` 사용 가능한 모든 SiteCatalyst 엔진에 대해 을 참조하십시오. 여러 태그가 구성된 경우 배열 선택기의 인덱스를 적절하게 변경합니다. 배열의 항목은 DTM 인터페이스에서 사용할 수 있는 SiteCatalyst 도구에 따라 순서가 지정됩니다.

1. 코드 편집기 창을 저장하고 닫은 다음 도구 구성에 변경 사항을 저장합니다.
1. 에서 **[!UICONTROL 승인]** 탭에서 보류 중인 승인을 모두 승인합니다. DTM 태그가 웹 페이지에 삽입할 준비가 되었습니다.
