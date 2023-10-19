---
title: 활동 스트림 기능
description: 로그인한 커뮤니티 구성원의 활동을 활동 스트림 구성 요소를 통해 필터링하고 표시할 수 있는 스트림으로 수집하는 방법에 대해 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 2b2a5de0-e7c7-4417-a217-4b929bc7dcfb
source-git-commit: b8887b4a6f757352e9dbfdf074c10e9ccd6dbd4f
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 4%

---

# 활동 스트림 기능 {#activity-streams-feature}

## 소개 {#introduction}

포럼 또는 블로그에 게시하는 것과 같이, 로그인한 커뮤니티 구성원의 활동은 스트림으로 수집되며, 스트림의 구성을 통해 다양한 방식으로 필터링되고 표시될 수 있습니다. `Activity Streams` 구성 요소.

팔로우 능력은 커뮤니티 회원들이 관심 있는 게시물을 팔로우하거나 다른 커뮤니티 회원들의 활동을 팔로우할 때 활동에 대한 또 다른 관점을 추가한다.

이 문서에서는 다음 사항을 설명합니다.

* AEM 사이트에 활동 스트림 구성 요소 추가
* 활동 스트림 구성 요소에 대한 구성 설정

### 페이지에 활동 스트림 추가 {#adding-activity-streams-to-a-page}

를 추가하려는 경우 `Activity Streams` 구성 요소를 페이지에 추가하려면 작성자 모드에서 구성 요소 브라우저를 사용하여

* `Communities / Activity Streams`

활동 스트림이 표시되어야 하는 페이지에 드래그합니다.

필요한 정보는 다음을 참조하십시오. [커뮤니티 구성 요소 기본 사항](/help/communities/basics.md).

다음의 경우 [필수 클라이언트측 라이브러리](/help/communities/essentials-activities.md#essentials-for-client-side) 포함됩니다. 이렇게 하면 `Activity Streams` 구성 요소가 표시됩니다.

![활동 스트림](assets/activity-component.png)

### 활동 스트림 구성 {#configuring-activity-streams}

배치된 을(를) 선택합니다 `Activity Streams` 에 액세스하고 선택할 수 있는 구성 요소 `Configure` 편집 대화 상자를 여는 아이콘.

![구성](assets/configure-new.png)

아래 **사용자 활동** 탭에서 표시할 활동 을 지정합니다.

![사용자 활동](assets/user-activities.png)

* **최대 활동 개수**

  표시할 활동 수

* **스트림 리소스 경로**

  커뮤니티 사이트 또는 커뮤니티 그룹의 기본값을 사용하려면 비워 둡니다. 스트림 리소스 경로는 활동의 소스를 식별합니다. 기본값은 비어 있습니다.

* **사용자 활동 보기 표시**

  선택하면 활동 페이지에 현재 구성원이 커뮤니티 내에서 생성한 활동을 기반으로 활동을 필터링하는 탭이 포함됩니다. 기본값은 선택되어 있습니다.

* **모든 활동 보기 표시**

  선택하면 활동 페이지에 현재 구성원이 액세스할 수 있는 커뮤니티 내에서 생성된 모든 활동이 포함된 탭이 포함됩니다. 기본값은 선택되어 있습니다.

* **다음 보기 표시**

  선택하면 활동 페이지에 현재 멤버가 따르는 활동을 기반으로 활동을 필터링하는 탭이 포함됩니다. 기본값은 선택되어 있습니다.

### 다음 보기 {#following-view}

다음을 활성화하도록 구성 요소를 구성해야 합니다. 다음을 허용하는 기능은 [블로그](/help/communities/blog-feature.md), [포럼](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [달력](/help/communities/calendar.md), [파일 라이브러리](/help/communities/file-library.md), 및 [댓글](/help/communities/comments.md).

![팔로잉 뷰](assets/following-activities.png)

다음 **팔로우** 단추는 항목을 활동으로 팔로우하는 수단을 제공합니다. [알림](/help/communities/notifications.md), 또는 [구독](/help/communities/subscriptions.md). 매번 **팔로우** 버튼을 선택한 경우 선택 항목을 켜거나 끌 수 있습니다. 다음 `Email Subscriptions` 선택한 항목은 구성된 경우에만 표시됩니다.

다음 방법을 선택하면 단추 텍스트가 다음으로 변경됩니다. **팔로잉**. 편의를 위해 다음을 선택할 수 있습니다. `Unfollow All` 모든 메서드를 해제합니다.

다음 **팔로우** 버튼이 표시됩니다.

* 다른 구성원의 프로필을 볼 때
* 포럼, QnA 및 블로그 등 주요 기능 페이지

   * 해당 일반 기능에 대한 모든 활동을 따릅니다.

* 포럼 주제, QnA 질문 또는 블로그 문서와 같은 특정 항목의 경우

   * 해당 특정 항목에 대한 모든 활동을 따릅니다.

### 추가 정보 {#additional-information}

자세한 내용은 [Activity Streams Essentials](/help/communities/essentials-activities.md) 개발자용 페이지입니다.
