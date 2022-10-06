---
title: 활동 트렌드
seo-title: Activity Trends
description: 페이지에 커뮤니티 활동 목록 구성 요소 추가
seo-description: Adding a Community Activity List component to a page
uuid: 316aabf7-01a5-46da-be59-70c206eb6a3d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 4a0debdd-acb9-4646-80bb-fec66fae4088
docset: aem65
exl-id: 2a4297e4-2d88-4fa6-8fea-3fea06753605
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 4%

---

# 활동 트렌드 {#activity-trends}

## 소개 {#introduction}

다음 `Community Activity List` 구성 요소는 컨텐츠 게시물 및 보기를 비롯하여 구성원의 게시물 및 보기에 대한 트렌드 정보를 추가할 수 있는 기능을 제공합니다.

이 문서에서는 다음 내용을 설명합니다.

* 추가 `Community Activity List` 구성 요소를 [커뮤니티 사이트](/help/communities/overview.md#community-sites).

* 에 대한 구성 설정 `Community Activity List` 구성 요소.

### 요구 사항 {#requirement}

에 대한 데이터 `Community Activity List` 는 커뮤니티 사이트에 대해 Adobe Analytics 라이센스가 부여되고 구성된 경우에만 사용할 수 있습니다.

자세한 내용은 [커뮤니티 기능에 대한 Analytics 구성](/help/communities/analytics.md).

### 페이지에 커뮤니티 활동 목록 추가 {#adding-a-community-activity-list-to-a-page}

을(를) 추가하려면 `Community Activity List` 구성 요소를 페이지에 작성자 모드에서 찾아 구성 요소를 찾습니다

* `Communities / Community Activity List`

페이지로 끌어서 놓습니다.

필요한 정보를 보려면 [커뮤니티 구성 요소 기본 사항](/help/communities/basics.md).

커뮤니티 사이트의 페이지에 처음 배치되면 구성 요소가 다음과 같이 나타납니다.

![community-activity](assets/community-activity.png)

### 커뮤니티 활동 목록 구성  {#configuring-community-activity-list}

배치된 항목을 선택합니다 `Community Activity List` 액세스하여 선택할 구성 요소 `Configure` 아이콘 편집 대화 상자를 엽니다.

![구성](assets/configure-new.png)

아래에 **댓글** 탭에서 업로드된 파일에 대한 주석이 표시되는 여부와 방법을 지정합니다.

![속성](assets/activity-list-properties.png)

* **유형**

   커뮤니티 구성원과 관련된 데이터를 표시할지 또는 UGC(사용자 생성 콘텐츠)에 데이터를 표시할지를 지정합니다.

   다음 중에서 선택합니다.

   * `Members`
   * `Content`

   기본값은 입니다. `Members`.

* **표시 제목**

   데이터 위에 표시할 설명 제목(예: ) `Trending Content`.
기본값은 제목이 아닙니다.

* **표시 개수**

   나열할 항목의 수입니다.
기본값은 10입니다.

* **활동 유형**

   다음 중 하나를 선택합니다.

   * `Views`(페이지 방문 횟수)
   * `Posts`(UGC 만들기)
   * `Follows`
   * `Likes`

   기본값은 보기입니다.

* **기간**

   다음 중 하나를 선택합니다.

   * `Last 24 hours`
   * `Last 7 days`
   * `Last 30 days`
   * `Last 90 days`
   * `This year (since Jan 1st)`
   * `Total`

   기본값은 입니다. `Total`.

* **컨텍스트 경로**

   특정 블로그와 같이 활동의 범위를 사이트의 하위 집합으로 지정하는 기능을 제공합니다.
기본값은 전체 커뮤니티 사이트입니다.

* **구성원 수 집계**

   선택을 취소하면(꺼져 있음) 최상위 게시물만 카운트됩니다. 예를 들어 컨텍스트가 루트 페이지(기본값)인 경우 `Activity Type` 의 `Posts` 루트 페이지에 컨텐츠를 게시할 수 없으므로 활동은 표시되지 않습니다. 이 옵션을 선택하면 모든 하위 페이지의 카운트가 포함됩니다.
기본값이 선택되어 있습니다.

### 4개의 구성 요소가 있는 예제 페이지 {#example-page-with-components}

**상위 방문자** 구성: 유형 = 구성원, 활동 유형 = 보기

**상위 기여자** 구성: 유형 = 구성원, 활동 유형 = 게시물

**상위 컨텐츠** 구성: 유형 = 컨텐츠, 활동 유형 = 보기,

**트렌드 콘텐츠** 구성: 유형 = 컨텐츠, 활동 유형 = 게시물

![구성 요소](assets/activity-list-components.png)
