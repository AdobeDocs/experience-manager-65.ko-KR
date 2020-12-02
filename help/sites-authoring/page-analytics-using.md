---
title: 페이지 분석 데이터 보기
seo-title: 페이지 분석 데이터 보기
description: 페이지 컨텐츠의 효율성을 측정하려면 페이지 분석 데이터를 사용하십시오.
seo-description: 페이지 컨텐츠의 효율성을 측정하려면 페이지 분석 데이터를 사용하십시오.
uuid: 5398a5d5-0239-4194-a403-77f5e6fcd741
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 5d192a48-c86f-4803-bb0d-0411ac7470f5
docset: aem65
legacypath: /content/help/en/experience-manager/6-4/help/sites-authoring/pa-using.html
translation-type: tm+mt
source-git-commit: e3683f6254295e606e9d85e88979feaaea76c42e
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 87%

---


# 페이지 분석 데이터 보기{#seeing-page-analytics-data}

페이지 컨텐츠의 효율성을 측정하려면 페이지 분석 데이터를 사용하십시오.

## 콘솔에서 볼 수 있는 Analytics {#analytics-visible-from-the-console}

![spad-01](assets/spad-01.png)

페이지 분석 데이터는 사이트 콘솔의 [목록 보기](/help/sites-authoring/basic-handling.md#list-view)에 표시됩니다. 페이지가 목록 형식으로 표시되면 기본적으로 다음 열을 사용할 수 있습니다.

* 페이지 보기 수
* 고유 방문자 수
* 페이지 시간

각 열에는 현재 보고 기간에 대한 값이 표시되며, 이전 보고 기간 이후에 값이 증가했는지 또는 감소했는지 여부도 표시됩니다. 표시되는 데이터는 12시간마다 업데이트됩니다.

>[!NOTE]
>
>업데이트 기간을 변경하려면 [가져오기 간격을 구성](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval)하십시오.

1. **사이트** 콘솔을 엽니다.예: [https://localhost:4502/sites.html/content](https://localhost:4502/sites.html/content)
1. 도구 모음의 맨 오른쪽에 있는(오른쪽 위 모서리) 아이콘을 클릭하거나 탭하여 **목록 보기**&#x200B;를 선택합니다(표시되는 아이콘은 [현재 보기](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)에 따라 달라집니다.).

1. 다시 도구 모음의 맨 오른쪽에 있는(오른쪽 위 모서리) 아이콘을 클릭하거나 탭한 다음, **설정 보기**&#x200B;를 선택합니다. **열 구성** 대화 상자가 열립니다. 필요한 변경 작업을 수행하고 **업데이트**&#x200B;를 확인하십시오.

   ![spad-02](assets/spad-02.png)

### 보고 기간 선택 {#selecting-the-reporting-period}

사이트 콘솔에 분석 데이터가 나타나는 보고 기간을 선택하십시오.

* 최근 30일 데이터
* 최근 90일 데이터
* 올해의 데이터

현재 보고 기간은 사이트 콘솔의 도구 모음에 표시됩니다(맨 위 도구 모음의 오른쪽). 드롭다운을 사용하여 필요한 보고 기간을 선택하십시오.

![aa-05](assets/aa-05.png)

### 사용 가능한 데이터 열 구성 {#configuring-available-data-columns}

analytics-administrators 사용자 그룹의 구성원은 작성자가 추가 Analytics 열을 볼 수 있도록 사이트 콘솔을 구성할 수 있습니다.

>[!NOTE]
>
>페이지 트리에 다른 Adobe Analytics 클라우드 구성과 연관된 하위가 있는 경우 페이지에 사용 가능한 데이터 열을 구성할 수 없습니다.

1. 목록 보기에서 보기 선택기(도구 모음의 오른쪽)를 사용하고 **설정 보기**&#x200B;를 선택한 다음 **사용자 지정 분석 데이터 추가**&#x200B;를 선택합니다.

   ![spad-03](assets/spad-03.png)

1. 사이트 콘솔의 작성자에게 노출할 지표를 선택한 후 **추가**&#x200B;를 클릭합니다.

   표시되는 열은 Adobe Analytics에서 검색됩니다.

   ![aa-16](assets/aa-16.png)

### 사이트에서 컨텐츠 인사이트 열기 {#opening-content-insights-from-sites}

사이트 콘솔에서 [컨텐츠 인사이트](/help/sites-authoring/content-insights.md)를 열어 페이지 효과를 자세히 조사합니다.

1. 사이트 콘솔에서 컨텐츠 인사이트를 보려는 페이지를 선택합니다.
1. 도구 모음에서 [분석 및 권장 사항] 아이콘을 클릭합니다.

   ![](do-not-localize/chlimage_1-14.png)

## 페이지 편집기에서 볼 수 있는 Analytics(활동 맵)  {#analytics-visible-from-the-page-editor-activity-map}

>[!CAUTION]
>
>Adobe Analytics API의 보안 변경 사항으로 인해, AEM 내에 포함된 Activity Map 버전을 더는 사용할 수 없습니다.
>
>이제 Adobe Analytics](https://docs.adobe.com/content/help/ko-KR/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html)에서 제공하는 [ActivityMap 플러그인을 사용해야 합니다.
