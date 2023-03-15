---
title: 페이지 분석 데이터 보기
seo-title: Seeing Page Analytics Data
description: 페이지 컨텐츠의 효율성을 측정하려면 페이지 분석 데이터를 사용하십시오.
seo-description: Use page analytics data to gauge the effectiveness of their page content
uuid: 8dda89be-13e3-4a13-9a44-0213ca66ed9c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 42d2195a-1327-45c0-a14c-1cf5ca196cfc
exl-id: 554b10c2-6157-4821-a6a7-f2fb6666cdff
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 93%

---

# 페이지 분석 데이터 보기{#seeing-page-analytics-data}

페이지 컨텐츠의 효율성을 측정하려면 페이지 분석 데이터를 사용하십시오.

## 콘솔에서 볼 수 있는 Analytics {#analytics-visible-from-the-console}

![aa-10](assets/aa-10.png)

페이지 분석 데이터는 사이트 콘솔의 [목록 보기](/help/sites-authoring/basic-handling.md#list-view)에 표시됩니다. 페이지가 목록 형식으로 표시되면 기본적으로 다음 열을 사용할 수 있습니다.

* 페이지 조회수
* 고유 방문자 수
* 페이지 시간

각 열에는 현재 보고 기간에 대한 값이 표시되며, 이전 보고 기간 이후에 값이 증가했는지 또는 감소했는지 여부도 표시됩니다. 표시되는 데이터는 12시간마다 업데이트됩니다.

>[!NOTE]
>
>업데이트 기간을 변경하려면 [가져오기 간격을 구성](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval)하십시오.

1. **사이트** 콘솔을 엽니다(예: [http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content)).
1. 도구 모음의 맨 오른쪽에 있는(오른쪽 위 모서리) 아이콘을 클릭하거나 탭하여 **목록 보기**&#x200B;를 선택합니다(표시되는 아이콘은 [현재 보기](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)에 따라 달라집니다.).

1. 다시 도구 모음의 맨 오른쪽에 있는(오른쪽 위 모서리) 아이콘을 클릭하거나 탭한 다음, **설정 보기**&#x200B;를 선택합니다. **열 구성** 대화 상자가 열립니다. 필요한 변경 작업을 수행하고 **업데이트**&#x200B;를 확인하십시오.

   ![aa-4](assets/aa-04.png)

### 보고 기간 선택 {#selecting-the-reporting-period}

사이트 콘솔에 분석 데이터가 나타나는 보고 기간을 선택하십시오.

* 최근 30일 데이터
* 최근 90일 데이터
* 올해의 데이터

현재 보고 기간은 사이트 콘솔의 도구 모음에 표시됩니다(맨 위 도구 모음의 오른쪽). 드롭다운을 사용하여 필요한 보고 기간을 선택하십시오.
![aa-5](assets/aa-05.png)

### 사용 가능한 데이터 열 구성 {#configuring-available-data-columns}

analytics-administrators 사용자 그룹의 구성원은 작성자가 추가 Analytics 열을 볼 수 있도록 사이트 콘솔을 구성할 수 있습니다.

>[!NOTE]
>
>페이지 트리에 다른 Adobe Analytics 클라우드 구성과 연관된 하위가 있는 경우 페이지에 사용 가능한 데이터 열을 구성할 수 없습니다.

1. 목록 보기에서 보기 선택기(도구 모음의 오른쪽)를 사용하여 **설정 보기** 그런 다음 **사용자 지정 Analytics 데이터 추가**.

   ![aa-](assets/aa-15.png)

1. 사이트 콘솔의 작성자에게 노출할 지표를 선택한 후 **추가**&#x200B;를 클릭합니다.

   표시되는 열은 Adobe Analytics에서 검색됩니다.

   ![aa-](assets/aa-16.png)

### 사이트에서 컨텐츠 인사이트 열기 {#opening-content-insights-from-sites}

열기 [컨텐츠 인사이트](/help/sites-authoring/content-insights.md) 를 클릭하여 페이지 효과를 추가로 조사하십시오.

1. 사이트 콘솔에서 컨텐츠 인사이트를 보려는 페이지를 선택합니다.
1. 도구 모음에서 [분석 및 권장 사항] 아이콘을 클릭합니다.

   ![](do-not-localize/chlimage_1-16a.png)

## 페이지 편집기에서 볼 수 있는 Analytics(활동 맵) {#analytics-visible-from-the-page-editor-activity-map}

>[!NOTE]
>
>웹 사이트에 대해 [활동 맵이 구성된 경우](/help/sites-administering/adobeanalytics-connect.md#configuring-for-the-activity-map) 표시됩니다.

>[!NOTE]
>
>활동 맵에 대한 데이터를 Adobe Analytics에서 가져옵니다.

웹 사이트가 [Adobe Analytics에 대해 구성](/help/sites-administering/adobeanalytics-connect.md)된 경우 [활동 맵 모드](/help/sites-authoring/author-environment-tools.md#page-modes)를 사용하여 관련 데이터를 볼 수 있습니다. 예:

![aa-7](assets/aa-07.png)

### 활동 맵에 액세스 {#accessing-the-activity-map}

[활동 맵](/help/sites-authoring/author-environment-tools.md#page-modes) 모드를 선택하면 Adobe Analytics 자격 증명을 입력하라는 메시지가 표시됩니다.

![aa-3](assets/aa-03.png)

**Analytics** 부동 도구 모음이 표시됩니다. 여기서 다음을 수행할 수 있습니다.

* 양방향 화살표(**>>**)를 사용하여 도구 모음 형식 변경
* 페이지 세부 사항(눈 모양 아이콘) 토글
* 활동 맵 설정(cog 아이콘) 구성
* 표시할 분석 선택(여러 드롭다운 선택기)
* 활동 맵 종료 및 도구 막대 닫기(x)

![aa-09](assets/aa-09.png)

### 표시할 Analytics 선택 {#selecting-the-analytics-to-show}

다음과 같은 여러 기준을 사용하여 표시할 분석 데이터 및 표시 방법을 선택할 수 있습니다.

* **표준**/**라이브**

* 이벤트 유형
* 사용자 그룹
* **버블**/**그라데이션**/**승자 및 패자**/**해제**

* 표시할 기간

![aa-](assets/aa-13.png)

### 활동 맵 구성 {#configuring-the-activity-map}

**설정 표시** 아이콘을 사용하여 **활동 맵 설정** 대화 상자를 엽니다.

![aa-04-1](assets/aa-04-1.png)

**활동 맵 설정** 대화 상자는 다음 세 개의 탭에 다양한 옵션을 제공합니다.

![aa-06](assets/aa-06.png)

* 일반

   * 보고서 세트
   * 페이지 이름
   * 언어
   * 레이블 오버레이 방법
   * 레이블 글꼴 크기
   * 그라데이션 색상
   * 버블 색상
   * 색상 그라데이션 기준
   * 그라데이션 투명도

* 표준

   * 표시(링크 유형 및 수)
   * 조회 수가 없는 링크에 대한 오버레이는 숨깁니다

* 라이브 버전

   * 상위 표시(승자 또는 패자)
   * 하위(%) 제외
   * 자동 업데이트(데이터 및 기간)
