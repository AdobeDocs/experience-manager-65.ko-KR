---
title: 활동 스트림 기능
seo-title: 활동 스트림 기능
description: 로그인한 커뮤니티 구성원의 활동
seo-description: 로그인한 커뮤니티 구성원의 활동
uuid: decd2d6c-4d4b-4698-a92c-2b5b441458cf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 89f3630f-c01a-4dc0-9ff5-169785f22c01
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 활동 스트림 기능{#activity-streams-feature}

## 소개 {#introduction}

포럼 또는 블로그에 게시하고 같이 로그인한 커뮤니티 멤버의 활동은 구성 요소의 구성을 통해 필터링되어 다양한 방법으로 표시될 수 있는 스트림으로 수집됩니다. `Activity Streams`

팔로우 기능은 커뮤니티 회원이 관심 있는 게시물을 팔로우하거나 다른 커뮤니티 구성원의 활동을 팔로우할 때 다른 활동 관점을 추가합니다.

이 문서에서는 다음 사항에 대해 설명합니다.

* aem 사이트에 활동 스트림 구성 요소 추가
* 활동 스트림 구성 요소에 대한 구성 설정

### 페이지에 활동 스트림 추가 {#adding-activity-streams-to-a-page}

작성 모드에서 페이지에 `Activity Streams` 구성 요소를 추가하려면 구성 요소 브라우저를 사용하여

* `Communities / Activity Streams`

활동 스트림이 표시되어야 하는 페이지에 드래그합니다.

필요한 정보를 보려면 커뮤니티 구성 [요소 기본 사항을 참조하십시오](/help/communities/basics.md).

필요한 [클라이언트측 라이브러리가](/help/communities/essentials-activities.md#essentials-for-client-side) `Activity Streams` 포함되어 있으면 구성 요소가 표시되는 방식입니다.

![chlimage_1-24](assets/chlimage_1-24.png)

### 활동 스트림 구성 {#configuring-activity-streams}

액세스할 배치된 `Activity Streams` 구성 요소를 선택하고 편집 대화 상자를 여는 `Configure` 아이콘을 선택합니다.

![chlimage_1-25](assets/chlimage_1-25.png)

사용자 **활동** 탭에서 표시할 활동을 지정합니다.

![chlimage_1-26](assets/chlimage_1-26.png)

* **표시할 활동**&#x200B;수의 최대 활동 수

* **스트림 리소스**&#x200B;경로 커뮤니티 사이트 또는 커뮤니티 그룹에 기본값으로 설정하려면 비워 둡니다. 스트림 리소스 경로는 활동의 소스를 식별합니다. 기본값은 비어 있습니다.

* **사용자 활동 보기**&#x200B;표시를 선택하면 활동 페이지에 현재 구성원이 커뮤니티 내에서 생성한 활동을 기준으로 하는 탭이 포함됩니다. 기본값은 선택되어 있습니다.

* **모든 활동 보기**&#x200B;표시를 선택하면 활동 페이지에 현재 구성원이 액세스할 수 있는 커뮤니티 내에서 생성된 모든 활동이 포함된 탭이 포함됩니다. 기본값은 선택되어 있습니다.

* **선택한**&#x200B;경우 다음 보기 표시를 선택하면 활동 페이지에 현재 구성원이 팔로우하는 활동을 필터링하는 탭이 포함됩니다. 기본값은 선택되어 있습니다.

### 다음 보기 {#following-view}

구성 요소는 다음을 사용하도록 구성해야 합니다. 다음을 수행할 수 있는 기능은 [블로그](/help/communities/blog-feature.md), [포럼](/help/communities/forum.md), [Qn](/help/communities/working-with-qna.md), 달력 [,](/help/communities/calendar.md)[](/help/communities/file-library.md)[](/help/communities/comments.md)filteraryFilterary, elibraryElibrary 및 Comments입니다.

![chlimage_1-27](assets/chlimage_1-27.png)

**팔로우 **버튼은 활동, [알림](/help/communities/notifications.md)또는 [구독으로](/help/communities/subscriptions.md)항목을 팔로우할 수 있는 방법을 제공합니다. **팔로우 **버튼을 선택할 때마다 선택한 항목을 켜거나 끌 수 있습니다. 선택은 `Email Subscriptions` 구성된 경우에만 표시됩니다.

다음 방법을 선택하면 단추 텍스트가 **다음과 같이 변경됩니다**. 편의를 위해 모든 방법을 전환하도록 선택할 `Unfollow All` 수 있습니다.

**팔로우 **버튼이 표시됩니다.

* 다른 구성원의 프로필을 볼 때
* 포럼, QnA 및 블로그와 같은 기본 기능 페이지에

   * 해당 일반 기능에 대한 모든 활동을 수행합니다.

* 포럼 주제, QnA 질문 또는 블로그 아티클과 같은 특정 항목에 대해

   * 해당 특정 항목에 대한 모든 활동

### 추가 정보 {#additional-information}

개발자를 위한 Activity Streams 필수 [사항](/help/communities/essentials-activities.md) 페이지에서는 자세한 내용을 확인할 수 있습니다.
