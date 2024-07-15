---
title: 커뮤니티 알림
description: AEM Communities에는 로그인한 커뮤니티 구성원의 관심 이벤트를 표시하는 알림이 있습니다.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: cadb62c9-210d-4204-8abc-d0cf70960392
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 0%

---

# 커뮤니티 알림 {#communities-notifications}

## 개요 {#overview}

AEM Communities은 로그인한 커뮤니티 구성원의 관심 이벤트를 표시하는 알림 섹션을 제공합니다.

알림은 다음에서 발생할 수 있으므로 [활동](/help/communities/essentials-activities.md) 및 [구독](/help/communities/subscriptions.md)과 비슷합니다.

* 콘텐츠를 게시하는 멤버입니다.
* 멤버가 다른 멤버를 따르도록 선택합니다.
* 특정 주제, 문서 및 기타 콘텐츠 스레드를 따르도록 선택하는 멤버.
* 구성원이 사용자 생성 콘텐츠의 다른 커뮤니티 구성원에 태그 지정(@mention)합니다.

알림을 활동 및 구독과 구분하는 것은 다음과 같습니다.

* 알림 섹션에 대한 링크는 항상 커뮤니티 사이트의 헤더에 있습니다.

   * 활동을 사용하려면 [활동 스트림 함수](/help/communities/functions.md#activity-stream-function)가 커뮤니티 사이트의 구조에 포함되어야 합니다.
   * 구독을 사용하려면 [전자 메일 구성](/help/communities/email.md)이 필요합니다.

* 알림은 확장 가능하고 플러그할 수 있는 채널을 통해 구현됩니다.

   * 활동은 웹에서만 사용할 수 있습니다.
   * 구독은 이메일을 통해서만 사용할 수 있습니다.

커뮤니티 [FP1](/help/communities/deploy-communities.md#latestfeaturepack)부터 사용 가능한 알림 채널은 다음과 같습니다.

* `Notifications` 링크를 사용하여 액세스한 웹 채널입니다.
* 이메일 채널, 이메일이 올바르게 구성된 경우 사용할 수 있습니다.

향후 채널은 모바일 및 데스크톱입니다.

### 요구 사항 {#requirements}

**전자 메일 구성**

알림을 위한 이메일 채널이 작동하려면 이메일을 구성해야 합니다.

전자 메일 설정에 대한 지침은 [전자 메일 구성](/help/communities/analytics.md)을 참조하세요.

**팔로우 사용**

다음을 활성화하도록 구성 요소를 구성해야 합니다. 다음을 허용하는 기능은 [블로그](/help/communities/blog-feature.md), [포럼](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [달력](/help/communities/calendar.md), [파일 라이브러리](/help/communities/file-library.md) 및 [댓글](/help/communities/comments.md)입니다.

**참고**:

* 커뮤니티 [사이트 템플릿](/help/communities/sites.md) 및 [그룹 템플릿](/help/communities/tools-groups.md)에서 사용되는 구성 요소가 이미 팔로우하도록 구성되어 있을 수 있습니다.

* 다른 구성원이 따를 수 있도록 구성원 프로필이 이미 구성되어 있습니다.

## 다음 항목의 알림 {#notifications-from-following}

![알림](assets/notifications.png)

**[!UICONTROL 팔로우]** 단추는 항목을 활동, 구독 및/또는 알림으로 팔로우하는 수단을 제공합니다. **[!UICONTROL 팔로우]** 단추를 선택할 때마다 선택 항목을 켜거나 끌 수 있습니다. `Email Subscriptions` 선택은 구성된 경우에만 존재합니다.

다음 방법을 선택하면 단추의 텍스트가 **[!UICONTROL Following]**(으)로 변경됩니다. 편의를 위해 `Unfollow All`을(를) 선택하여 모든 메서드를 해제할 수 있습니다.

**[!UICONTROL 팔로우]** 단추가 나타납니다.

* 다른 구성원의 프로필을 볼 때
* 포럼, QnA 및 블로그 등 주요 기능 페이지에서:

   * 해당 일반 기능에 대한 모든 활동을 따릅니다.

* 포럼 주제, QnA 질문 또는 블로그 문서와 같은 특정 항목의 경우:

   * 해당 특정 항목에 대한 모든 활동을 따릅니다.

## 알림 설정 관리 {#managing-notification-settings}

알림 페이지에서 알림 설정 링크를 선택하면 각 구성원이 알림을 받는 방법을 관리할 수 있습니다.

웹 채널은 항상 활성화되어 있습니다.

![알림14](assets/notifications1.png)

전자 메일의 올바른 [구성](/help/communities/email.md)을 사용하는 전자 메일 채널은 웹 채널과 동일한 설정을 제공합니다.

이메일 채널은 기본적으로 꺼져 있습니다.

![알림2](assets/notifications2.png)

구성원에 의해 켜질 수 있지만 구성 중인 이메일에 따라 다릅니다.

![알림3](assets/notifications3.png)

## 알림 보기 {#viewing-notifications}

### 웹 알림 {#web-notifications}

[마법사에서 만든 커뮤니티 사이트](/help/communities/sites-console.md)에 배너 위에 있는 사이트의 헤더 막대에 `Notifications` 기능에 대한 링크가 포함되어 있습니다. 메시지와 달리 알림은 모든 커뮤니티 사이트에 대해 생성되지만 메시지는 사이트 생성 프로세스 중에 활성화되어야 합니다.

게시된 사이트를 방문할 때 `Notifications` 링크를 선택하면 구성원에 대한 모든 알림이 표시됩니다.

![알림4](assets/notifications4.png)

### 이메일 알림 {#email-notifications}

이메일 채널이 활성화되면 구성원은 웹의 콘텐츠에 대한 링크가 포함된 이메일을 받게 됩니다.

![알림5](assets/notifications5.png)

## 이메일 알림 사용자 지정 {#customize-email-notifications}

조직은 **/libs/settings/community/templates/email/html**&#x200B;에 있는 템플릿을 [오버레이](/help/communities/client-customize.md#overlays)하여 전자 메일 알림을 사용자 지정할 수 있습니다.

예를 들어, 언급 전자 메일 알림(커뮤니티 구성 요소)을 수정하려면 **@mentions** 지원을 사용하도록 설정한 구성 요소의 템플릿에 동사 **mention**&#x200B;에 대한 **if** 조건을 추가합니다.

블로그 댓글에 @mention 이메일 알림 템플릿을 수정하려면 기본 템플릿을 **/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en**&#x200B;에 배치합니다.

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```
