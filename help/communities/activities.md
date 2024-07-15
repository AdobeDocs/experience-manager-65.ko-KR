---
title: 활동 스트림 기능
description: 로그인한 커뮤니티 구성원의 활동을 활동 스트림 구성 요소를 통해 필터링하고 표시할 수 있는 스트림으로 수집하는 방법에 대해 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 2b2a5de0-e7c7-4417-a217-4b929bc7dcfb
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# 활동 스트림 기능 {#activity-streams-feature}

## 소개 {#introduction}

포럼 또는 블로그에 게시하는 것과 같이 로그인한 커뮤니티 구성원의 활동은 스트림으로 수집되며 `Activity Streams` 구성 요소의 구성을 통해 다양한 방식으로 필터링되고 표시될 수 있습니다.

팔로우 능력은 커뮤니티 회원들이 관심 있는 게시물을 팔로우하거나 다른 커뮤니티 회원들의 활동을 팔로우할 때 활동에 대한 또 다른 관점을 추가한다.

이 문서에서는 다음 사항을 설명합니다.

* AEM 사이트에 활동 스트림 구성 요소 추가
* 활동 스트림 구성 요소에 대한 구성 설정

### 페이지에 활동 스트림 추가 {#adding-activity-streams-to-a-page}

작성자 모드에서 페이지에 `Activity Streams` 구성 요소를 추가하려면 구성 요소 브라우저를 사용하여 찾습니다

* `Communities / Activity Streams`

활동 스트림이 표시되어야 하는 페이지에 드래그합니다.

필요한 정보는 [커뮤니티 구성 요소 기본 사항](/help/communities/basics.md)을 참조하세요.

[필수 클라이언트측 라이브러리](/help/communities/essentials-activities.md#essentials-for-client-side)가 포함된 경우 `Activity Streams` 구성 요소는 다음과 같이 표시됩니다.

![activity-streams](assets/activity-component.png)

### 활동 스트림 구성 {#configuring-activity-streams}

배치된 `Activity Streams` 구성 요소를 선택하여 편집 대화 상자를 여는 `Configure` 아이콘에 액세스하고 선택합니다.

![구성](assets/configure-new.png)

**사용자 활동** 탭에서 표시할 활동을 지정합니다.

![사용자 활동](assets/user-activities.png)

* **최대 활동 수**

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

다음을 활성화하도록 구성 요소를 구성해야 합니다. 다음을 허용하는 기능은 [블로그](/help/communities/blog-feature.md), [포럼](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [달력](/help/communities/calendar.md), [파일 라이브러리](/help/communities/file-library.md) 및 [댓글](/help/communities/comments.md)입니다.

![다음 보기](assets/following-activities.png)

**팔로우** 단추는 항목을 활동, [알림](/help/communities/notifications.md) 또는 [구독](/help/communities/subscriptions.md)(으)로 팔로우하는 수단을 제공합니다. **팔로우** 단추를 선택할 때마다 선택 항목을 켜거나 끌 수 있습니다. `Email Subscriptions` 선택은 구성된 경우에만 존재합니다.

다음 방법을 선택하면 단추의 텍스트가 **Following**(으)로 변경됩니다. 편의를 위해 `Unfollow All`을(를) 선택하여 모든 메서드를 해제할 수 있습니다.

**팔로우** 단추가 나타납니다.

* 다른 구성원의 프로필을 볼 때
* 포럼, QnA 및 블로그 등 주요 기능 페이지

   * 해당 일반 기능에 대한 모든 활동을 따릅니다.

* 포럼 주제, QnA 질문 또는 블로그 문서와 같은 특정 항목의 경우

   * 해당 특정 항목에 대한 모든 활동을 따릅니다.

### 추가 정보 {#additional-information}

자세한 내용은 개발자를 위한 [Activity Streams Essentials](/help/communities/essentials-activities.md) 페이지에서 확인할 수 있습니다.
