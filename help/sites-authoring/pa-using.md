---
title: 페이지 분석 데이터를 보고 페이지 콘텐츠의 효과를 측정합니다
description: 페이지 분석 데이터를 사용하여 페이지 콘텐츠의 효과를 측정합니다
uuid: 8dda89be-13e3-4a13-9a44-0213ca66ed9c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 42d2195a-1327-45c0-a14c-1cf5ca196cfc
exl-id: 554b10c2-6157-4821-a6a7-f2fb6666cdff
source-git-commit: 75c6bb87bb06c5ac9378ccebf193b5416c080bb1
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 4%

---

# 페이지 분석 데이터 보기{#seeing-page-analytics-data}

페이지 분석 데이터를 사용하여 페이지 콘텐츠의 효과를 측정합니다.

## 콘솔에서 볼 수 있는 분석 {#analytics-visible-from-the-console}

![aa-10](assets/aa-10.png)

페이지 분석 데이터가에 표시됩니다. [목록 보기](/help/sites-authoring/basic-handling.md#list-view) 사이트 콘솔의 페이지가 목록 형식으로 표시되면 기본적으로 다음 열을 사용할 수 있습니다.

* 페이지 조회수
* 고유 방문자
* 페이지 시간

각 열에는 현재 보고 기간에 대한 값이 표시되며, 이전 보고 기간 이후 값이 증가했는지 또는 감소했는지도 표시됩니다. 표시되는 데이터는 12시간마다 업데이트됩니다.

>[!NOTE]
>
>업데이트 기간을 변경하려면 [가져오기 간격 구성](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval).

1. 를 엽니다. **사이트** 콘솔 - 예 [http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content)
1. 도구 모음의 맨 오른쪽(오른쪽 상단)에서 아이콘을 클릭하거나 탭하여 선택합니다 **목록 보기** (표시된 아이콘은 다음에 따라 다릅니다. [현재 보기](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)).

1. 다시, 도구 모음의 맨 오른쪽 (오른쪽 상단)에서 아이콘을 클릭하거나 탭한 다음 을 선택합니다 **설정 보기**. 다음 **열 구성** 대화 상자가 열립니다. 필요한 사항을 변경하고 다음을 사용하여 확인합니다. **업데이트**.

   ![aa-4](assets/aa-04.png)

### 보고 기간 선택 {#selecting-the-reporting-period}

Analytics 데이터가 사이트 콘솔에 표시되는 보고 기간을 선택하십시오.

* 최근 30일 데이터
* 최근 90일 데이터
* 올해의 데이터

현재 보고 기간은 사이트 콘솔의 도구 모음(상단 도구 모음 오른쪽)에 표시됩니다. 드롭다운을 사용하여 필요한 보고 기간을 선택합니다.
![aa-5](assets/aa-05.png)

### 사용 가능한 데이터 열 구성 {#configuring-available-data-columns}

Analytics-Administrators 사용자 그룹의 구성원은 작성자가 추가 Analytics 열을 볼 수 있도록 Sites 콘솔을 구성할 수 있습니다.

>[!NOTE]
>
>페이지 트리에 다른 Adobe Analytics 클라우드 구성과 연결된 하위 항목이 포함되어 있는 경우 페이지에 사용할 수 있는 데이터 열을 구성할 수 없습니다.

1. 목록 보기에서 보기 선택기(도구 모음의 오른쪽)를 사용하여 **설정 보기** 그런 다음 **사용자 지정 Analytics 데이터 추가**.

   ![aa-](assets/aa-15.png)

1. 사이트 콘솔에서 작성자에게 노출하려는 지표를 선택한 다음 을 클릭합니다 **추가**.

   표시되는 열은 Adobe Analytics에서 검색됩니다.

   ![aa-](assets/aa-16.png)

### 사이트에서 컨텐츠 인사이트 열기 {#opening-content-insights-from-sites}

열기 [컨텐츠 인사이트](/help/sites-authoring/content-insights.md) 를 클릭하여 페이지 효과를 추가로 조사하십시오.

1. 사이트 콘솔에서 컨텐츠 인사이트를 보려는 페이지를 선택합니다.
1. 도구 모음에서 Analytics 및 Recommendations 아이콘을 클릭합니다.

   ![Analytics 및 Recommendations 아이콘](do-not-localize/chlimage_1-16a.png)

## 페이지 편집기(Activity Map)에 표시되는 분석 {#analytics-visible-from-the-page-editor-activity-map}

>[!NOTE]
>
>다음과 같은 경우 표시됩니다. [Activity Map이 구성되었습니다.](/help/sites-administering/adobeanalytics-connect.md#configuring-for-the-activity-map) 웹 사이트용.

>[!NOTE]
>
>Activity Map에 대한 데이터는 Adobe Analytics에서 가져옵니다.

웹 사이트가 다음과 같은 경우 [Adobe Analytics에 대해 구성됨](/help/sites-administering/adobeanalytics-connect.md), 다음을 사용할 수 있습니다. [모드 Activity Map](/help/sites-authoring/author-environment-tools.md#page-modes) 관련 데이터를 봅니다. 예:

![aa-7](assets/aa-07.png)

### Activity Map 액세스 {#accessing-the-activity-map}

을(를) 선택한 후 [Activity Map](/help/sites-authoring/author-environment-tools.md#page-modes) 모드에서는 Adobe Analytics 자격 증명을 입력하라는 메시지가 표시됩니다.

![aa-3](assets/aa-03.png)

다음 **분석** 부동 도구 모음이 표시됩니다. 여기에서 다음 작업을 수행할 수 있습니다.

* 이중 화살표를 사용하여 도구 모음 형식 변경(**>>**)
* 페이지 세부 정보 전환(눈 모양 아이콘)
* Activity Map 설정 구성( cog 아이콘)
* 표시할 분석을 선택합니다(다양한 드롭다운 선택기).
* Activity Map을 종료하고 도구 모음(x)을 닫습니다.

![aa-09](assets/aa-09.png)

### 표시할 분석 선택 {#selecting-the-analytics-to-show}

다양한 기준을 사용하여 표시할 분석 데이터와 표시 방법을 선택할 수 있습니다.

* **표준**/**라이브**

* 이벤트 유형
* 사용자 그룹
* **거품**/**그레이디언트**/**승자 및 패자**/**끔**

* 표시할 기간

![aa-](assets/aa-13.png)

### Activity Map 구성 {#configuring-the-activity-map}

사용 **설정 표시** 아이콘을 클릭하여 엽니다. **Activity Map 설정** 대화 상자.

![aa-04-1](assets/aa-04-1.png)

다음 **Activity Map 설정** 대화 상자는 다음 세 가지 탭에 다양한 옵션을 제공합니다.

![aa-06](assets/aa-06.png)

* 일반

   * 보고서 세트
   * 페이지 이름
   * 언어
   * 레이블 오버레이 방법
   * 레이블 글꼴 크기
   * 그라데이션 색상
   * 거품 색상
   * 색상 그라데이션 기준
   * 그라데이션 투명도

* 표준

   * 표시(링크 유형 및 수)
   * 조회 수가 없는 링크에 대한 오버레이 숨기기

* 라이브 버전

   * 상위 표시(승자 또는 패자)
   * 하위 % 제외
   * 자동 업데이트(데이터 및 기간)
