---
title: 활동 트렌드
description: 페이지에 커뮤니티 활동 목록 구성 요소 추가
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 2a4297e4-2d88-4fa6-8fea-3fea06753605
source-git-commit: 518207a0d8a95ef17b0972855a58f124fb215c85
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 1%

---

# 활동 트렌드 {#activity-trends}

## 소개 {#introduction}

다음 `Community Activity List` 구성 요소를 사용하여 구성원의 게시물 및 보기, 콘텐츠의 게시물 및 보기에 대한 트렌드 정보를 추가할 수 있습니다.

이 문서에서는 다음 사항을 설명합니다.

* 추가 `Community Activity List` 구성 요소를 a로 [커뮤니티 사이트](/help/communities/overview.md#community-sites).

* 에 대한 구성 설정 `Community Activity List` 구성 요소.

### 요구 사항 {#requirement}

다음에 대한 데이터 `Community Activity List` Adobe Analytics에 라이선스가 부여되고 커뮤니티 사이트에 대해 구성된 경우에만 사용할 수 있습니다.

다음을 참조하십시오 [커뮤니티 기능에 대한 Analytics 구성](/help/communities/analytics.md).

### 페이지에 커뮤니티 활동 목록 추가 {#adding-a-community-activity-list-to-a-page}

을(를) 추가하려면 `Community Activity List` 구성 요소를 페이지에 추가하려면 작성자 모드에서 구성 요소를 찾습니다. `Communities / Community Activity List` 을 페이지에 끌어서 놓습니다.

필요한 정보는 다음을 참조하십시오. [커뮤니티 구성 요소 기본 사항](/help/communities/basics.md).

커뮤니티 사이트의 페이지에 처음 배치하면 구성 요소가 다음과 같이 표시됩니다.

![community-activity](assets/community-activity.png)

### 커뮤니티 활동 목록 구성  {#configuring-community-activity-list}

배치된 을(를) 선택합니다 `Community Activity List` 구성 요소를 선택한 다음, `Configure` 아이콘을 클릭하여 편집 대화 상자를 열 수 있습니다.

![구성](assets/configure-new.png)

아래 **댓글** 탭에서 업로드한 파일에 대한 댓글이 표시되는지 여부 및 방법을 지정합니다.

![속성](assets/activity-list-properties.png)

* **유형**

  커뮤니티 구성원에 대한 데이터를 표시할지 또는 UGC(사용자 생성 컨텐츠)를 표시할지를 지정합니다.

  다음 중에서 선택:

   * `Members`
   * `Content`

  기본값은 입니다 `Members`.

* **제목 표시**

  데이터 위에 표시할 설명적인 제목입니다. 예: `Trending Content`.
기본값은 제목이 없습니다.

* **개수 표시**

  나열할 항목의 수입니다.
기본값은 10입니다.

* **활동 유형**

  다음 중 하나를 선택합니다.

   * `Views`(페이지 방문 횟수)
   * `Posts`(UGC 만들기)
   * `Follows`
   * `Likes`

  기본값은 보기 입니다.

* **기간**

  다음 중 하나를 선택합니다.

   * `Last 24 hours`
   * `Last 7 days`
   * `Last 30 days`
   * `Last 90 days`
   * `This year (since Jan 1)`
   * `Total`

  기본값은 입니다 `Total`.

* **컨텍스트 경로**

  이를 통해 특정 블로그와 같은 사이트의 하위 집합으로 활동의 범위를 지정할 수 있습니다.
기본값은 전체 커뮤니티 사이트입니다.

* **구성원 수 집계**

  선택을 취소(해제)하면 최상위 수준의 게시물만 카운트됩니다. 예를 들어 컨텍스트가 루트 페이지(기본값)이면 `Activity Type` / `Posts` 루트 페이지에 콘텐츠를 게시할 수 없으므로 활동을 표시하지 않습니다. 선택하면 모든 하위 페이지의 카운트가 포함됩니다.
기본값은 선택되어 있습니다.

### 4개의 구성 요소가 있는 예제 페이지 {#example-page-with-components}

**상위 방문자 수** config: 유형 = 멤버, 활동 유형 = 보기

**상위 기여자** config: Type = Members, Activity type = Posts

**상위 콘텐츠** 구성: 유형 = 컨텐츠, 활동 유형 = 보기,

**트렌드 콘텐츠** 구성: 유형 = 컨텐츠, 활동 유형 = 게시물

![구성 요소](assets/activity-list-components.png)
