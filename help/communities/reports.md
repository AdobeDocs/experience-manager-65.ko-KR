---
title: 보고서 콘솔
description: Adobe Experience Manager 작성 환경에서 여러 가지 방법으로 액세스할 수 있는 다양한 보고서를 사용하는 방법을 알아봅니다.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 2aff2ffe-ba6f-4cc9-a126-40fc2a1161e2
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 6%

---

# 보고서 콘솔 {#reports-console}

## 개요 {#overview}

AEM Communities의 경우 작성 환경에서 여러 가지 방법으로 액세스할 수 있는 다양한 보고서가 있습니다.

일반적으로 다양한 보고서는 다음과 같습니다.

* [보고서 보기](#views-report)

  모든 커뮤니티 사이트에 대해 커뮤니티 구성원과 사이트 방문자별로 컨텐츠 보기 차트를 제공합니다.

* [게시물 보고서](#posts-report)

  모든 커뮤니티 사이트에 커뮤니티 구성원의 다양한 게시물 유형 차트를 제공합니다.

테이블 형식 보고서는 후속 처리를 위해 .csv 형식으로 내보낼 수 있습니다.

## 보고 콘솔 {#reporting-consoles}

### 커뮤니티 사이트에 대한 보고서 {#reports-for-community-sites}

* 전역 탐색에서: **[!UICONTROL 탐색]** > **[!UICONTROL 커뮤니티]** > **[!UICONTROL 보고서]**

* 다음 중에서 선택:

   * **[!UICONTROL 할당 보고서]**

      * 선택한 커뮤니티 사이트, 사용자 또는 그룹 및 할당에 대한 보고서를 생성합니다.

   * **[!UICONTROL 게시물 보고서]**

      * 선택한 커뮤니티 사이트, 콘텐츠 유형 및 기간에 대한 보고서를 생성합니다.

   * **[!UICONTROL 보고서 보기]**

      * 선택한 커뮤니티 사이트, 콘텐츠 유형 및 기간에 대한 보고서를 생성합니다.

![보고서](assets/reports1.png)

## 보기 보고서 {#views-report}

보기 콘솔을 사용하면 지정된 기간 동안 커뮤니티 기능을 통해 페이지 보기에서 보고서를 생성할 수 있습니다.

![보기-보고서](assets/view-report.png)

보고서 기준을 선택합니다.

* **[!UICONTROL 사이트]**

  커뮤니티 사이트를 선택합니다.

* **[!UICONTROL 콘텐츠 형식]**

  모든 콘텐츠를 선택하거나 사이트에 있는 기능 중 하나를 선택할 수 있습니다.

* **[!UICONTROL 일정]**

  다음 중 하나를 선택합니다.

   * 지난 7일
   * 지난 30일
   * 최근 90일
   * 지난 해

보고서를 만들려면 **[!UICONTROL 생성]**&#x200B;을 선택하십시오.

![생성 보기](assets/generate-views.png)

## 게시물 보고서 {#posts-report}

게시물 콘솔을 사용하면 지정된 기간 동안 커뮤니티 기능에 대한 게시물 수에 대해 보고서를 생성할 수 있습니다.

![게시물-보고서](assets/posts-report.png)

보고서 기준을 선택합니다.

* **[!UICONTROL 사이트]**

  커뮤니티 사이트를 선택합니다.

* **[!UICONTROL 콘텐츠 형식]**

  모든 콘텐츠를 선택하거나 사이트에 있는 기능 중 하나를 선택할 수 있습니다.

* **[!UICONTROL 일정]**

  다음 중 하나를 선택합니다.

   * 지난 7일
   * 지난 30일
   * 최근 90일
   * 지난 해

보고서를 만들려면 **[!UICONTROL 생성]**&#x200B;을 선택하십시오.

![생성-보고서](assets/generate-posts-report.png)

## 문제 해결 {#troubleshooting}

### 나열된 커뮤니티 사이트 없음 {#no-community-sites-listed}

나열된 커뮤니티 사이트가 없는 경우 사이트에 대해 Adobe Analytics이 활성화되어 있는지 확인합니다. 할당에 대한 보고서를 선택하는 경우 할당 기능이 커뮤니티 사이트의 구조에 있는지 확인합니다.

### 보고서가 AEM 작성자 인스턴스에 표시되지 않음 {#reports-do-not-show-in-aem-author-instance}

AEM 작성자 인스턴스에 보고서가 표시되지 않는 경우 Publish 인스턴스의 URL 매핑과 같은 사용자 지정에 대해 확인하십시오. URL 매핑이 커뮤니티 사이트의 AEM Publish 인스턴스에서만 수행되는 경우 **사이트 트렌드 보고서 소셜 구성 요소 팩터리** 구성의 AEM 작성자 인스턴스에서도 구성되었는지 확인하십시오.

![AEM 작성자의 URL 매핑](assets/sitetrend.png)
