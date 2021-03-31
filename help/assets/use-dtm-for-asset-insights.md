---
title: DTM을 통해 자산 인사이트 활성화
description: Adobe DTM(다이내믹 태그 관리)을 사용하여 자산 통찰력을 활성화하는 방법을 알아봅니다.
contentOwner: AG
role: 비즈니스 전문가, 관리자
feature: 자산 통찰력,자산 보고서
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 1%

---


# DTM {#enable-asset-insights-through-dtm}을(를) 통해 자산 인사이트 활성화

Adobe 다이내믹 태그 관리는 디지털 마케팅 툴을 활성화하는 도구입니다. Adobe Analytics 고객에게 무료로 제공됩니다. 추적 코드를 사용자 지정하여 제3자 CMS 솔루션이 자산 인사이트를 사용할 수 있도록 하거나 DTM을 사용하여 자산 인사이트 태그를 삽입할 수 있습니다. 인사이트는 이미지만 지원되고 제공됩니다.

>[!CAUTION]
>
>Adobe DTM은 [!DNL Adobe Experience Platform Launch] 대신 사용되지 않으며, 곧 [수명 종료](https://medium.com/launch-by-adobe/dtm-plans-for-a-sunset-3c6aab003a6f)에 도달하게 됩니다. Adobe에서는 [자산 인사이트](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/asset-insights-launch-tutorial.html)에  [!DNL Launch] 을 사용하는 것이 좋습니다.

DTM을 통해 자산 인사이트를 활성화하려면 다음 단계를 수행합니다.

1. Experience Manager 로고를 클릭하고 **[!UICONTROL 도구]** > **[!UICONTROL 자산]** > **[!UICONTROL 인사이트 구성]**&#x200B;으로 이동합니다.
1. [DTM Cloud Service을 사용하여 Experience Manager 배포 구성](/help/sites-administering/dtm.md)

   API 토큰은 사용자 프로필에서 [https://dtm.adobe.com](https://dtm.adobe.com/)에 로그온하고 **[!UICONTROL 계정 설정]**&#x200B;을(를) 방문한 후 사용할 수 있어야 합니다. 자산 인사이트와 자산 인사이트의 통합이 아직 진행 중이기 때문에 자산 인사이트의 관점에서 이 단계는 필요하지 않습니다.

1. [https://dtm.adobe.com](https://dtm.adobe.com/)에 로그온하고 적절한 회사를 선택합니다.
1. 기존 웹 속성 만들기 또는 열기

   * **[!UICONTROL 웹 속성]** 탭을 선택한 다음 **[!UICONTROL 속성 추가]**&#x200B;를 클릭합니다.

   * 필드를 적절히 업데이트하고 **[!UICONTROL 속성 만들기]**&#x200B;를 클릭합니다. [설명서](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)를 참조하십시오.

   ![웹 속성 편집 만들기](assets/Create-edit-web-property.png)

1. **[!UICONTROL 규칙]** 탭의 탐색 창에서 **[!UICONTROL 페이지 로드 규칙]**&#x200B;을 선택하고 **[!UICONTROL 새 규칙 만들기]**&#x200B;를 클릭합니다.

   ![chlimage_1-58](assets/chlimage_1-194.png)

1. **[!UICONTROL JavaScript /타사 태그]**&#x200B;를 확장합니다. 그런 다음 **[!UICONTROL 순차적 HTML]** 탭에서 **[!UICONTROL 새 스크립트 추가]**&#x200B;를 클릭하여 스크립트 대화 상자를 엽니다.

   ![chlimage_1-59](assets/chlimage_1-195.png)

1. Experience Manager 로고를 클릭하고 **[!UICONTROL 도구]** > **[!UICONTROL 자산]**&#x200B;으로 이동합니다.
1. **[!UICONTROL 인사이트 페이지 추적기]**&#x200B;를 클릭하고 추적기 코드를 복사한 다음 6단계에서 연 스크립트 대화 상자에 붙여넣습니다. 변경 사항을 저장합니다.

   >[!NOTE]
   >
   >* `AppMeasurement.js` 가 제거됩니다. DTM의 Adobe Analytics 도구를 통해 사용할 수 있을 것으로 예상됩니다.
   >* `assetAnalytics.dispatcher.init()` 호출이 제거되었습니다. DTM의 Adobe Analytics 도구 로드가 완료되면 이 함수가 호출될 예정입니다.
   >* 자산 인사이트 페이지 추적기가 호스팅되는 위치(예: Experience Manager, CDN 등)에 따라 스크립트 소스의 출처를 변경해야 할 수 있습니다.
   >* Experience Manager에서 호스팅하는 페이지 추적기의 경우 소스는 발송자 인스턴스의 호스트 이름을 사용하여 게시 인스턴스를 가리켜야 합니다.


1. 액세스 `https://dtm.adobe.com`. 웹 속성에서 **[!UICONTROL 개요]**&#x200B;를 클릭하고 **[!UICONTROL 도구 추가]**&#x200B;를 클릭하거나 기존 Adobe Analytics 도구를 엽니다. 도구를 만드는 동안 **[!UICONTROL 구성 메서드]**&#x200B;를 **[!UICONTROL 자동]**&#x200B;으로 설정할 수 있습니다.

   ![Adobe Analytics 도구 추가](assets/Add-Adobe-Analytics-Tool.png)

   필요에 따라 스테이징/프로덕션 보고서 세트를 선택합니다.

1. **[!UICONTROL 라이브러리 관리]**&#x200B;를 확장하고 ]**에 있는**[!UICONTROL &#x200B;라이브러리 로드가 **[!UICONTROL 페이지 위쪽]**&#x200B;으로 설정되어 있는지 확인합니다.

   ![chlimage_1-61](assets/chlimage_1-197.png)

1. **[!UICONTROL 페이지 코드 사용자 지정]**&#x200B;을 확장하고 **[!UICONTROL 편집기 열기]**&#x200B;를 클릭합니다.

   ![chlimage_1-62](assets/chlimage_1-198.png)

1. 윈도우에 다음 코드를 붙여넣습니다.

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

   * DTM의 페이지 로드 규칙은 `pagetracker.js` 코드만 포함합니다. 모든 `assetAnalytics` 필드는 기본값으로 재정의됩니다. 기본적으로 필요하지 않습니다.
   * 이 코드는 `_satellite.getToolsByType('sc')[0].getS()`이(가) 초기화되었고 `assetAnalytics,dispatcher.init`을(를) 사용할 수 있는지 확인한 후 `assetAnalytics.dispatcher.init()`을 호출합니다. 따라서 11단계에서 추가 작업을 생략할 수 있습니다.
   * 인사이트 페이지 추적기 코드(**[!UICONTROL 도구 > 자산 > 인사이트 페이지 추적기]**) 내의 주석에 명시된 대로, 페이지 추적기에서 `AppMeasurement` 개체를 만들지 않으면 처음 세 개의 인수(RSID, 추적 서버 및 방문자 네임스페이스)는 관련이 없습니다. 대신 빈 문자열이 전달되어 이 내용이 강조 표시됩니다.\
      나머지 인수는 인사이트 구성 페이지(**[!UICONTROL 도구 > 자산 > 인사이트 구성]**)에 구성된 것과 일치합니다.
   * 사용 가능한 모든 SiteCatalyst 엔진에 대해 `satelliteLib`을 쿼리하여 AppMeasurement 개체를 검색합니다. 여러 태그가 구성된 경우 배열 선택기의 인덱스를 적절하게 변경합니다. 배열의 항목은 DTM 인터페이스에서 사용할 수 있는 SiteCatalyst 도구에 따라 정렬됩니다.

1. 코드 편집기 창을 저장하고 닫은 다음 도구 구성에 변경 사항을 저장합니다.
1. **[!UICONTROL 승인]** 탭에서 대기 중인 승인 모두를 승인합니다. DTM 태그가 웹 페이지에 삽입할 준비가 되었습니다. 웹 페이지에 DTM 태그를 삽입하는 방법에 대한 자세한 내용은 [사용자 지정 페이지 템플릿에 DTM 통합](https://blogs.adobe.com/experiencedelivers/experience-management/integrating-dtm-custom-aem6-page-template/)을 참조하십시오.
