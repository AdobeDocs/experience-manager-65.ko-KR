---
title: 페이지 성능 분석
seo-title: Analyzing Page Performance
description: 작성하는 페이지의 성능을 컨텐츠 인사이트 페이지를 사용하여 분석해 보십시오.
seo-description: Use the Content Insight page to analyze the performance of the page that you are authoring
uuid: 563d3e98-20d9-4cca-a174-bafd6e65c1bb
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 57cd61d5-78f2-4f8c-99ee-75e100c052ef
docset: aem65
exl-id: 14484a90-4e44-4c85-9411-b78ed11dc70d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 98%

---

# 페이지 성능 분석{#analyzing-page-performance}

작성하는 페이지의 성능을 [컨텐츠 인사이트](/help/sites-authoring/content-insights.md) 페이지를 열어 분석할 수 있습니다. 분석에 집중할 보고 기간을 구성하십시오.

## 페이지에 대한 분석 및 권장 사항 열기 {#opening-analytics-and-recommendations-for-a-page}

페이지에 대한 [분석 및 권장 사항]을 확인하려면 다음 절차를 사용하십시오.

1. 분석할 페이지로 이동합니다.
1. 도구 모음에서 **분석 및 권장 사항**&#x200B;을 클릭하거나 탭합니다.

   >[!NOTE]
   >
   >페이지에 대한 [분석 및 권장 사항]은 ](/help/sites-administering/adobeanalytics-connect.md)Adobe Analytics와 통합[하도록 AEM을 구성한 경우에만 나타납니다.

   ![screen-shot_2019-03-05at115319](assets/screen-shot_2019-03-05at115319.png)

### 보고 기간 변경 {#changing-the-reporting-period}

Analytics 보고서에 대한 다음 시간 관련 특성을 변경하십시오.

* 보고할 기간
* 데이터 세부기간

보고서의 시간 관련 특성을 변경하는 도구는 컨텐츠 인사이트 페이지의 맨 위에 표시됩니다. ![chlimage_1-126](assets/chlimage_1-126.png)

#### 보고 기간 변경 {#changing-the-reporting-period-1}

컨텐츠 인사이트 페이지의 보고 기간을 페이지 활동 분석을 집중하도록 특정 기간으로 변경하십시오. 보고 기간을 변경하면 보고서가 자동으로 새로 고쳐집니다. 일정에서 음영 영역은 보고 기간을 나타냅니다. 일정의 날짜는 왼쪽에서 오른쪽으로 증가합니다.

![chlimage_1-127](assets/chlimage_1-127.png)

컨텐츠 인사이트 페이지의 보고 기간을 변경하려면 다음을 수행하십시오.

1. 페이지의 맨 위에 일정이 표시되지 않으면 [일정 전환] 아이콘을 클릭하거나 탭합니다.

   ![](do-not-localize/chlimage_1-22.png)

1. 보고 기간의 시작 날짜를 변경하려면 음영 영역의 왼쪽에 나타나는 원을 원하는 시작 날짜로 드래그합니다.

   음영 영역의 왼쪽을 볼 수 없다면 화면 스크롤 막대를 사용하여 보이게 하십시오.

1. 보고 기간의 종료 날짜를 변경하려면 음영 영역의 오른쪽에 나타나는 원을 원하는 종료 날짜로 드래그합니다.

#### 보고 기간의 세부기간 변경 {#changing-the-granularity-of-the-reporting-period}

보고서에서 각 데이터 요소가 걸쳐 있는 시간을 변경하십시오. 예를 들어 주 세부기간을 선택하면 보기 보고서의 각 데이터 요소는 1주일 동안의 보기 횟수를 나타냅니다.

![screen_shot_2017-11-29at141001](assets/screen_shot_2017-11-29at141001.png)

세부기간은 보기 및 페이지 평균 참여 시간(분) 보고서와 같이 시간을 기준으로 데이터를 표시하는 보고서에 영향을 줍니다. 세부기간은 일정의 눈금에도 영향을 줍니다.

1. 세부기간 컨트롤이 나타나지 않으면 세부기간 전환 아이콘을 클릭하거나 탭합니다.

   ![chlimage_1-128](assets/chlimage_1-128.png)

1. 원하는 세부기간을 클릭하거나 탭합니다. 세부기간이 선택되면 이 세부기간을 반영하도록 보고서가 자동으로 업데이트됩니다.

### SEO 추천용 작업 지정 {#assigning-tasks-for-seo-recommendations}

SEO 추천 보고서를 사용하여 검색 엔진에 대한 페이지 표시 향상을 위한 작업을 생성할 수 있습니다. 확인 표시가 없는 보고서의 각 추천에 대해 필요한 일을 수행하도록 사용자에게 지정할 작업을 생성할 수 있습니다.

![chlimage_1-129](assets/chlimage_1-129.png)

SEO 추천의 상태는 작업이 생성되었지만 아직 완료되지 않았음을 나타냅니다.

![chlimage_1-130](assets/chlimage_1-130.png)

생성된 작업은 사용자의 작업 목록에 나타납니다. 작업에 대한 자세한 내용은 [작업](/help/sites-authoring/task-content.md).

SEO 추천을 위한 작업을 생성하려면 다음 절차를 수행하십시오.

1. 정보 아이콘을 클릭하거나 탭하여 SEO 추천 내용을 표시합니다.

   ![](do-not-localize/chlimage_1-23.png)

1. 정보 아이콘 옆에 나타나는 원으로 둘러싸인 삼각형 아이콘을 클릭합니다.

   ![chlimage_1-131](assets/chlimage_1-131.png)

1. 양식 필드가 나타나면 채우고 [만들기]를 탭합니다.

   * 프로젝트: 작업을 생성할 프로젝트를 선택하십시오.
   * 이름: 작업을 식별하는 이름입니다. 기본 이름은 SEO 추천의 제목입니다.
   * 할당 대상: 작업을 지정받을 사용자를 선택하십시오. 목록을 필터링하려면 사용자의 이름을 입력합니다.
   * 설명: 작업을 완료하는 데 필요한 활동에 대한 설명입니다. 기본 설명은 SEO 추천을 동반하는 정보입니다.
   * 작업 우선 순위: 작업의 우선 순위입니다.
   * 기한: 작업을 완료해야 하는 날짜입니다.

   **참고:**&#x200B;생성된 작업은 SEO 추천이 적용되는 페이지의 경로를 포함합니다.

1. [완료]를 클릭하거나 탭하여 [작업 생성됨] 메시지를 닫습니다.
