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
exl-id: 2b2a5de0-e7c7-4417-a217-4b929bc7dcfb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 4%

---

# 활동 스트림 기능 {#activity-streams-feature}

## 소개 {#introduction}

포럼 또는 블로그에 게시하는 등의 로그인한 커뮤니티 구성원의 활동은 `Activity Streams` 구성 요소의 구성을 통해 다양한 방법으로 필터링 및 표시할 수 있는 스트림에 수집됩니다.

팔로우하는 기능은 커뮤니티 구성원이 관심 있는 게시를 따르거나 다른 커뮤니티 구성원의 활동을 따를 때 다른 활동 보기를 추가합니다.

이 문서에서는 다음 내용을 설명합니다.

* AEM 사이트에 Activity Streams 구성 요소 추가
* 활동 스트림 구성 요소에 대한 구성 설정

### 페이지에 활동 스트림 추가 {#adding-activity-streams-to-a-page}

작성자 모드의 페이지에 `Activity Streams` 구성 요소를 추가하려면 구성 요소 브라우저를 사용하여 을 찾습니다

* `Communities / Activity Streams`

활동 스트림이 표시되어야 하는 페이지에 드래그합니다.

필요한 정보를 보려면 [커뮤니티 구성 요소 기본 사항](/help/communities/basics.md)을 방문하십시오.

필요한 [클라이언트 측 라이브러리](/help/communities/essentials-activities.md#essentials-for-client-side)가 포함되면 이 방법으로 `Activity Streams` 구성 요소가 표시됩니다.

![activity-streams](assets/activity-component.png)

### 활동 스트림 구성 {#configuring-activity-streams}

액세스할 배치된 `Activity Streams` 구성 요소를 선택하고 편집 대화 상자를 여는 `Configure` 아이콘을 선택합니다.

![구성](assets/configure-new.png)

**사용자 활동** 탭에서 표시할 활동을 지정합니다.

![사용자 활동](assets/user-activities.png)

* **최대 활동 개수**

   표시할 활동 수

* **스트림 리소스 경로**

   커뮤니티 사이트 또는 커뮤니티 그룹으로 기본적으로 비워 둡니다. 스트림 리소스 경로는 활동의 소스를 식별합니다. 기본값은 비어 있습니다.

* **사용자 활동 보기 표시**

   선택된 경우 활동 페이지에는 현재 구성원이 커뮤니티 내에서 생성한 활동을 기준으로 활동을 필터링하는 탭이 포함됩니다. 기본값이 선택되어 있습니다.

* **모든 활동 보기 표시**

   선택된 경우 활동 페이지에는 현재 구성원이 액세스할 수 있는 커뮤니티 내에서 생성된 모든 활동이 포함된 탭이 포함됩니다. 기본값이 선택되어 있습니다.

* **다음 보기 표시**

   이 옵션을 선택하면 활동 페이지에 현재 구성원이 따르는 활동을 필터링하는 탭이 포함됩니다. 기본값이 선택되어 있습니다.

### 다음 보기 {#following-view}

다음을 사용하도록 구성 요소를 구성해야 합니다. 다음을 허용하는 기능은 [블로그](/help/communities/blog-feature.md), [포럼](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [달력](/help/communities/calendar.md), [파일 라이브러리](/help/communities/file-library.md) 및 [주석](/help/communities/comments.md)입니다.

![다음 보기](assets/following-activities.png)

**팔로우** 단추는 항목을 활동, [알림](/help/communities/notifications.md) 또는 [구독](/help/communities/subscriptions.md)으로 따르는 수단을 제공합니다. **팔로우** 단추를 선택할 때마다 선택 항목을 켜거나 끌 수 있습니다. `Email Subscriptions` 선택 항목은 구성된 경우에만 나타납니다.

다음 방법을 선택하면 단추의 텍스트가 **Following**&#x200B;으로 변경됩니다. 편의를 위해 `Unfollow All` 을 선택하여 모든 메서드를 해제할 수 있습니다.

**팔로우** 단추가 나타납니다.

* 다른 구성원의 프로파일을 볼 때
* 포럼, QnA 및 블로그 등의 기본 기능 페이지에서 다음을 수행합니다.

   * 일반 기능에 대한 모든 활동을 따릅니다.

* 포럼 주제, 질문 또는 블로그 문서와 같은 특정 항목에 대해

   * 특정 항목에 대한 모든 활동을 따릅니다.

### 추가 정보 {#additional-information}

개발자를 위한 [Activity Streams Essentials](/help/communities/essentials-activities.md) 페이지에서 자세한 내용을 찾을 수 있습니다.
