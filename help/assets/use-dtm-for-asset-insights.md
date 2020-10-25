---
title: DTM을 통해 자산 통찰력 활성화
description: Adobe DTM(다이내믹 태그 관리)을 사용하여 자산 통찰력을 활성화하는 방법을 알아봅니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: d13381d961f7663366b041168da369c0b01c9336
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 2%

---


# Enable Asset Insights through DTM {#enable-asset-insights-through-dtm}

Adobe 다이내믹 태그 관리는 디지털 마케팅 툴을 활성화하는 도구입니다. Adobe Analytics 고객에게는 무료로 제공됩니다. 추적 코드를 사용자 지정하여 타사 CMS 솔루션을 사용하여 자산 통찰력을 사용하거나 DTM을 사용하여 자산 인사이트 태그를 삽입할 수 있습니다. 인사이트는 이미지만 지원되고 제공됩니다.

>[!CAUTION]
>
>Adobe DTM은 Adobe Experience Platform Launch에게 더 이상 사용되지 않으며 곧 [수명이 다될 것입니다](https://medium.com/launch-by-adobe/dtm-plans-for-a-sunset-3c6aab003a6f). Adobe에서는 자산 통찰력에 론치를 [사용하는 것이 좋습니다](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/advanced/asset-insights-launch-tutorial.html).

다음 단계를 수행하여 DTM을 통해 자산 통찰력을 활성화합니다.

1. Experience Manager 로고를 클릭하고 도구 > **[!UICONTROL 자산]** > **[!UICONTROL 인사이트 구성]** 으로 **[!UICONTROL 이동합니다]**.
1. [DTM Cloud Service을 사용하여 Experience Manager 배포 구성](/help/sites-administering/dtm.md)

   API 토큰은 https://dtm.adobe.com에 [로그인하고 사용자 프로필의](https://dtm.adobe.com/) 계정 설정을 **[!UICONTROL 방문한 후 사용할 수]** 있어야 합니다. 자산 인사이트와 Experience Manager 사이트의 통합이 아직 진행 중이기 때문에 자산 인사이트 관점에서 이 단계는 필요하지 않습니다.

1. https://dtm.adobe.com에 [로그인하여](https://dtm.adobe.com/)회사를 적절히 선택합니다.
1. 기존 웹 속성 만들기 또는 열기

   * 웹 **[!UICONTROL 속성]** 탭을 선택한 다음 속성 **[!UICONTROL 추가를 클릭합니다]**.

   * 필드를 적절히 업데이트하고 속성 **[!UICONTROL 만들기를 클릭합니다]**. 설명서를 [참조하십시오](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html).

   ![웹 속성 편집](assets/Create-edit-web-property.png)

1. 규칙 **** 탭 **[!UICONTROL 의 탐색 창에서]** 페이지 로드 규칙 **[!UICONTROL 을 선택하고 새 규칙]**&#x200B;만들기를 클릭합니다.

   ![chlimage_1-58](assets/chlimage_1-194.png)

1. JavaScript **[!UICONTROL /타사 태그를 확장합니다]**. 그런 다음 **[!UICONTROL 순차적 HTML]** 탭에서 새 스크립트 **** 추가를 클릭하여 스크립트 대화 상자를 엽니다.

   ![chlimage_1-59](assets/chlimage_1-195.png)

1. Experience Manager 로고를 클릭하고 **[!UICONTROL 도구]** > **[!UICONTROL 자산으로 이동합니다]**.
1. 인사이트 **[!UICONTROL 페이지 추적기를]**&#x200B;클릭하고 추적기 코드를 복사한 다음 6단계에서 연 스크립트 대화 상자에 붙여넣습니다. 변경 사항을 저장합니다.

   >[!NOTE]
   >
   >* `AppMeasurement.js` 가 제거됩니다. DTM의 Adobe Analytics 툴을 통해 제공될 예정입니다.
   >* 통화가 `assetAnalytics.dispatcher.init()` 제거됩니다. 이 함수는 DTM의 Adobe Analytics 도구 로드가 끝나면 호출될 예정입니다.
   >* 자산 통찰력 페이지 추적기가 호스팅되는 위치(예: Experience Manager, CDN 등)에 따라 스크립트 소스의 출처를 변경해야 할 수 있습니다.
   >* Experience Manager에서 호스팅하는 페이지 추적기의 경우 소스는 발송자 인스턴스의 호스트 이름을 사용하여 게시 인스턴스를 가리켜야 합니다.


1. 액세스 `https://dtm.adobe.com`. 웹 **[!UICONTROL 속성에서]** 개요를 클릭하고 도구 **[!UICONTROL 추가를]** 클릭하거나 기존 Adobe Analytics 도구를 엽니다. 도구를 만드는 동안 구성 방법 **[!UICONTROL 을]** 자동으로 설정할 수 **[!UICONTROL 있습니다]**.

   ![Adobe Analytics 도구 추가](assets/Add-Adobe-Analytics-Tool.png)

   필요에 따라 스테이징/프로덕션 보고서 세트를 선택합니다.

1. 라이브러리 관리 **[!UICONTROL 를]**&#x200B;확장하고 라이브러리 **[!UICONTROL 로드 위치]** 가 **[!UICONTROL 페이지 맨 위로]**&#x200B;설정되어 있는지확인합니다.

   ![chlimage_1-61](assets/chlimage_1-197.png)

1. 페이지 코드 **[!UICONTROL 사용자 지정을]**&#x200B;확장하고 편집기 **[!UICONTROL 열기를 클릭합니다]**.

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

   * DTM의 페이지 로드 규칙은 `pagetracker.js` 코드만 포함합니다. 모든 `assetAnalytics` 필드는 기본값으로 대체됩니다. 기본적으로 필요하지 않습니다.
   * 초기화된 후 사용할 수 있도록 `assetAnalytics.dispatcher.init()` 한 코드 `_satellite.getToolsByType('sc')[0].getS()` 가 `assetAnalytics,dispatcher.init` 호출됩니다. 따라서 11단계에서 추가하지 않아도 됩니다.
   * 인사이트 페이지 추적기 코드(**[!UICONTROL 도구 > 자산 > 인사이트 페이지 추적기]**) 내의 주석에 표시된 대로, 페이지 추적기에서 `AppMeasurement` 개체를 만들지 않으면 처음 세 개의 인수(RSID, 추적 서버 및 방문자 네임스페이스)는 관련이 없습니다. 대신 빈 문자열이 전달되어 강조 표시됩니다.\
      나머지 인수는 [인사이트 구성] 페이지(도구 >**[!UICONTROL 자산 > 인사이트 구성]**)에 구성된 것에 해당합니다.
   * 사용 가능한 모든 SiteCatalyst 엔진에 대해 쿼리하여 AppMeasurement 개체 `satelliteLib` 를 검색합니다. 여러 태그가 구성된 경우 배열 선택기의 인덱스를 적절하게 변경합니다. 배열의 항목은 DTM 인터페이스에서 사용할 수 있는 SiteCatalyst 도구에 따라 순서가 정해집니다.

1. 코드 편집기 창을 저장하고 닫은 다음 도구 구성에 변경 사항을 저장합니다.
1. 승인 **[!UICONTROL 탭에서]** 대기 중인 승인을 모두 승인합니다. DTM 태그가 웹 페이지에 삽입할 준비가 되었습니다. 웹 페이지에 DTM 태그를 삽입하는 방법에 대한 자세한 내용은 사용자 지정 페이지 템플릿에서 [DTM 통합을 참조하십시오](https://blogs.adobe.com/experiencedelivers/experience-management/integrating-dtm-custom-aem6-page-template/).
