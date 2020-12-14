---
title: 활동 트렌드
seo-title: 활동 트렌드
description: 페이지에 커뮤니티 활동 목록 구성 요소 추가
seo-description: 페이지에 커뮤니티 활동 목록 구성 요소 추가
uuid: 316aabf7-01a5-46da-be59-70c206eb6a3d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 4a0debdd-acb9-4646-80bb-fec66fae4088
docset: aem65
translation-type: tm+mt
source-git-commit: c190d5f223c85f6c49fea1391d8a3d2baff20192
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 4%

---


# 활동 트렌드 {#activity-trends}

## 소개 {#introduction}

`Community Activity List` 구성 요소는 컨텐츠의 게시물 및 보기뿐만 아니라 구성원의 게시물 및 보기에 대한 트렌드 정보를 추가하는 기능을 제공합니다.

이 문서에서는 다음 사항에 대해 설명합니다.

* `Community Activity List` 구성 요소를 [커뮤니티 사이트](/help/communities/overview.md#community-sites)에 추가합니다.

* `Community Activity List` 구성 요소에 대한 구성 설정입니다.

### 요구 사항 {#requirement}

`Community Activity List`에 대한 데이터는 Adobe Analytics에 대한 라이선스가 부여되고 커뮤니티 사이트에 대해 구성된 경우에만 사용할 수 있습니다.

[커뮤니티 기능에 대한 분석 구성](/help/communities/analytics.md)을 참조하십시오.

### {#adding-a-community-activity-list-to-a-page} 페이지에 커뮤니티 활동 목록 추가

작성 모드에서 페이지에 `Community Activity List` 구성 요소를 추가하려면 구성 요소를 찾습니다

* `Communities / Community Activity List`

페이지로 드래그하여 배치합니다.

필요한 정보를 보려면 [커뮤니티 구성 요소 기본 사항](/help/communities/basics.md)을 방문하십시오.

커뮤니티 사이트의 페이지에 처음 배치하면 구성 요소가 표시되는 방식입니다.

![커뮤니티 활동](assets/community-activity.png)

### 커뮤니티 활동 목록 구성 중 {#configuring-community-activity-list}

액세스할 배치된 `Community Activity List` 구성 요소를 선택하고 편집 대화 상자를 여는 `Configure` 아이콘을 선택합니다.

![configure](assets/configure-new.png)

**주석** 탭에서 업로드된 파일에 대한 주석이 어떻게 표시되는지 지정합니다.

![속성](assets/activity-list-properties.png)

* **유형**

   커뮤니티 구성원과 관련된 데이터를 표시할지 또는 사용자 생성 콘텐츠(UGC)를 표시할지를 지정합니다.

   다음 중에서 선택합니다.

   * `Members`
   * `Content`

   기본값은 `Members`입니다.

* **표시 제목**

   `Trending Content` 등의 데이터 위에 표시할 설명형 제목입니다.
기본값은 제목이 아닙니다.

* **표시 개수**

   나열할 항목 수입니다.
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

   기본값은 `Total`입니다.

* **컨텍스트 경로**

   특정 블로그와 같이 활동의 범위를 사이트의 하위 집합으로 지정하는 기능을 제공합니다.
기본값은 전체 커뮤니티 사이트입니다.

* **구성원 수 집계**

   선택 해제(해제)하면 최상위 게시물만 카운트됩니다. 예를 들어 컨텍스트가 루트 페이지(기본값)인 경우 루트 페이지에 컨텐츠를 게시할 수 없으므로 `Posts`의 `Activity Type`은 어떠한 활동도 표시하지 않습니다. 선택하면 모든 하위 페이지의 카운트가 포함됩니다.
기본값은 선택되었습니다.

### 4개의 구성 요소 {#example-page-with-components}이 있는 예제 페이지

**상위** 방문자 구성:유형 = 멤버, 활동 유형 = 보기

**상위** 기여도 구성:유형 = 멤버, 활동 유형 = 게시물

**상위** 컨텐트 구성:유형 = 컨텐트, 활동 유형 = 보기,

**트렌드** 콘텐츠 구성:유형 = 컨텐츠, 활동 유형 = 게시물

![components](assets/activity-list-components.png)

