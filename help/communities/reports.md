---
title: 보고서 콘솔
seo-title: 보고서 콘솔
description: 보고서에 액세스하는 방법 학습
seo-description: 보고서에 액세스하는 방법 학습
uuid: 7bb15a15-077b-4bfb-aaf4-50fddc67f237
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: fde053ff-b671-456b-869c-81f16ea1f1be
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 보고서 콘솔{#reports-console}

## 개요 {#overview}

AEM Communities에는 작성 환경에서 여러 가지 방법으로 액세스할 수 있는 다양한 보고서가 있습니다.

일반적으로 다양한 보고서는 다음과 같습니다.

* [할당 보고서](#assignments-report) - [역량 강화 커뮤니티의](/help/communities/overview.md#enablement-community)경우, SCORM 표준을 구현할 때 관련 점수를 포함하여 학습자의 과제 진행 상황을 대략적으로 설명합니다
* [보기 보고서](#views-report) - 커뮤니티 구성원 및 모든 커뮤니티 사이트에 대한 사이트 방문자별 컨텐츠 보기 차트를 제공합니다.
* [게시물 보고서](#posts-report) - 커뮤니티 구성원이 모든 커뮤니티 사이트에 게시하는 다양한 유형의 게시물 차트를 제공합니다.

Adobe [Analytics가 활성화되면](/help/communities/sites-console.md#analytics)보고서에는 시간에 따른 각 활성 리소스에 대한 보기, 재생, 댓글 및 등급 수가 포함됩니다

테이블 형식 보고서를 후속 처리를 위해 .csv 형식으로 내보낼 수 있습니다.

## 보고 콘솔 {#reporting-consoles}

### 커뮤니티 사이트에 대한 보고서 {#reports-for-community-sites}

* 전역 탐색:탐색 **,****커뮤니티, 보고서**

* 선택 항목

   * **할당 보고서**

      * 선택한 커뮤니티 사이트, 사용자 또는 그룹 및 할당에 대한 보고서 생성

      * **게시물 보고서**

         * 선택한 커뮤니티 사이트, 컨텐츠 유형 및 기간에 대한 보고서 생성
      * **보기 보고서**

         * 선택한 커뮤니티 사이트, 컨텐츠 유형 및 기간에 대한 보고서 생성


![chlimage_1-236](assets/chlimage_1-236.png)

### 지원 리소스 및 학습 경로에 대한 보고서 {#reports-for-enablement-resources-and-learning-paths}

* 전역 탐색에서 다음을 수행합니다.탐색 **,****커뮤니티, 리소스**

* 기존 활성 커뮤니티 사이트 선택

   * **보고서 **아이콘을 선택하여 모든 활성 리소스를 포함하는 보고서를 생성합니다.
   * 역량 강화 학습 경로 선택
   * **보고서 **아이콘을 선택하여

      * 포함된 역량 강화 리소스
      * 학습 경로에 할당된 수강생

* 이 보고서에서는 다음을 제공합니다.

   * 표 데이터, CSV로 다운로드 가능

      * 수강생 식별
      * 그들의 상태
      * 카탈로그를 통해 할당 또는 액세스
      * 댓글 수
      * 별 등급

자세한 내용은 리소스 [콘솔의 보고서 섹션을](/help/communities/resources.md#report) 참조하십시오.

## 할당 보고서 {#assignments-report}

[할당] 콘솔에서는 활성 커뮤니티 사이트, 사용자 또는 그룹, 할당으로 보고서를 필터링할 수 있습니다.

보고서는 제공된 의견 또는 등급뿐만 아니라 진행 상황에 대한 정보를 제공합니다.

![chlimage_1-237](assets/chlimage_1-237.png)

보고서 기준을 선택합니다.

* **사이트**

   활성 커뮤니티 사이트 선택

* **사용자 및 그룹**
   * 수강생 한 명에 대한 보고서를 생성하려면 사용자를 선택합니다.
   * 그룹을 선택하여 수강생 그룹에 대한 보고서를 생성합니다.
   터널 서비스는 게시 환경에서 구성원 및 구성원 그룹에 액세스합니다.

* **할당**

   선택한 수강생에게 할당된 지원 리소스 중에서 선택

생성을 **선택하여** 보고서를 만듭니다.

![chlimage_1-238](assets/chlimage_1-238.png)

## 보기 보고서 {#views-report}

보기 콘솔을 사용하면 지정된 기간 동안 커뮤니티 기능별로 페이지 보기에서 보고서를 생성할 수 있습니다.

![chlimage_1-239](assets/chlimage_1-239.png)

보고서 기준을 선택합니다.

* **사이트**

   커뮤니티 사이트 선택

* **컨텐트 유형**

   모든 컨텐츠를 선택하거나 사이트에 있는 기능 중 하나를 선택할 수 있습니다.

* 시간 프레임

   다음 중 하나 선택

   * 최근 7일
   * 최근 30일
   * 최근 90일
   * 지난 해

생성을 **선택하여** 보고서를 만듭니다.

![chlimage_1-240](assets/chlimage_1-240.png)

## 게시물 보고서 {#posts-report}

게시물 콘솔에서는 지정된 기간 동안 커뮤니티 기능에 대한 게시물 수에 대한 보고서를 생성할 수 있습니다.

![chlimage_1-241](assets/chlimage_1-241.png)

보고서 기준을 선택합니다.

* **사이트**

   커뮤니티 사이트 선택

* **컨텐트 유형**

   모든 컨텐츠를 선택하거나 사이트에 있는 기능 중 하나를 선택할 수 있습니다.

* 시간 프레임

   다음 중 하나 선택

   * 최근 7일
   * 최근 30일
   * 최근 90일
   * 지난 해

생성을 **선택하여** 보고서를 만듭니다.

![chlimage_1-242](assets/chlimage_1-242.png)

## 문제 해결 {#troubleshooting}

### 나열된 커뮤니티 사이트 없음 {#no-community-sites-listed}

목록에 커뮤니티 사이트가 없으면 Adobe Analytics가 사이트에 대해 활성화되어 있는지 확인합니다. 할당에서 보고서를 선택하는 경우 할당 기능이 커뮤니티 사이트의 구조에 있는지 확인합니다.

### 보고서는 AEM 작성자 인스턴스에 표시되지 않습니다. {#reports-do-not-show-in-aem-author-instance}

보고서가 AEM 작성자 인스턴스 확인에서 게시 인스턴스의 URL 매핑과 같은 사용자 지정을 확인하지 않는 경우 URL 매핑이 커뮤니티 사이트의 AEM 게시 인스턴스에서만 수행되는 경우 **Site Trend Report Social Component Factory **구성의 AEM 작성자 인스턴스에서 동일한지 확인합니다.

![AEM 작성자의 URL 매핑](assets/sitetrend.png)