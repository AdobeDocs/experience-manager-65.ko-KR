---
title: Communities 알림
description: AEM Communities에는 로그인한 커뮤니티 구성원에게 관심도 이벤트를 표시하는 알림이 있습니다
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

# Communities 알림 {#communities-notifications}

## 개요 {#overview}

AEM Communities은 로그인한 커뮤니티 구성원의 관심 이벤트를 표시하는 알림 섹션을 제공합니다.

알림은 활동 및 구독과 [유사하며,](/help/communities/subscriptions.md) 그 결과는 다음과 같습니다.[](/help/communities/essentials-activities.md)

* 컨텐츠 게시 회원입니다.
* 다른 회원을 팔로우하기로 선택한 회원입니다.
* 특정 주제, 기사 및 기타 컨텐츠 스레드를 팔로우하기로 선택한 회원.
* 구성원이 사용자 생성 컨텐츠에서 다른 커뮤니티 구성원을 태그 지정(@mention)합니다.

알림을 활동 및 구독과 구분하는 것은 다음과 같습니다.

* 알림 섹션에 대한 링크는 항상 커뮤니티 사이트의 헤더에 있습니다.

   * 활동을 사용하려면 [활동 스트림 기능이](/help/communities/functions.md#activity-stream-function) 커뮤니티 사이트의 구조에 포함되어야 합니다.
   * 구독하려면 [전자 메일을](/help/communities/email.md) 구성해야 합니다.

* 알림의 구현 확장 가능하고 플러그 가능 채널을 통해 이루어집니다.

   * 활동은 웹에서만 사용할 수 있습니다.
   * 구독은 이메일을 통해서만 사용할 수 있습니다.

커뮤니티 기준 [FP1](/help/communities/deploy-communities.md#latestfeaturepack), 사용 가능한 알림 채널은 다음과 같습니다.

* 웹 채널, 을 사용하여 액세스 `Notifications` 링크를 클릭합니다.
* 이메일 채널, 이메일이 올바르게 구성된 경우 사용할 수 있습니다.

향후 채널은 모바일 및 데스크톱입니다.

### 요구 사항 {#requirements}

**이메일 구성**

알림에 대한 이메일 채널이 작동하려면 이메일을 구성해야 합니다.

이메일 설정에 대한 지침은 이메일](/help/communities/analytics.md) 구성을 참조하십시오[.

**팔로우 활성화**

다음을 활성화하도록 구성 요소를 구성해야 합니다. 다음을 [허용하는 기능은 블로그](/help/communities/blog-feature.md), 포럼](/help/communities/forum.md), [[QnA](/help/communities/working-with-qna.md), [일정](/help/communities/calendar.md), [파일 라이브러리](/help/communities/file-library.md) 및 [댓글](/help/communities/comments.md) 입니다.

**참고**:

* 커뮤니티 [사이트 서식 파일](/help/communities/sites.md) 및 [그룹 서식 파일](/help/communities/tools-groups.md) 내에서 사용되는 구성 요소는 이미 팔로우하도록 구성되어 있을 수 있습니다.

* 멤버 프로필은 이미 다른 밈이 팔로우 할 수 있도록 구성되어 있습니다.

## 다음의 알림 {#notifications-from-following}

![알림을](assets/notifications.png)

다음 **[!UICONTROL 팔로우]** 단추는 항목을 활동, 구독 및/또는 알림으로 따르는 수단을 제공합니다. [팔로우&#x200B;]**] 버튼 을 선택할 때마다**[!UICONTROL &#x200B;선택 항목을 켜거나 끌 수 있습니다. 다음 `Email Subscriptions` 선택한 항목은 구성된 경우에만 표시됩니다.

다음 방법을 선택하면 버튼 텍스트가 다음으로&#x200B;]**변경됩니다**[!UICONTROL . 편의상 모든 방법을 끄도록 선택할 `Unfollow All` 수 있습니다.

**[!UICONTROL 팔로우]** 버튼 이 나타납니다.

* 다른 회원의 프로필을 볼 때.
* 포럼, QnA 및 블로그 등 주요 기능 페이지에서:

   * 해당 일반 기능에 대한 모든 활동을 따릅니다.

* 포럼 주제, QnA 질문 또는 블로그 문서와 같은 특정 항목의 경우:

   * 해당 특정 항목에 대한 모든 활동을 따릅니다.

## 알림 설정 관리 {#managing-notification-settings}

알림 페이지에서 알림 설정 링크 선택하면 각 구성원이 알림 수신 방법을 관리 수 있습니다.

웹 채널은 항상 활성화되어 있습니다.

![알림14](assets/notifications1.png)

이메일](/help/communities/email.md)의 적절한 [구성에 의존하는 이메일 채널은 웹 채널과 동일한 설정을 제공합니다.

이메일 채널은 기본적으로 꺼져 있습니다.

![notifications2](assets/notifications2.png)

구성원에 의해 켜질 수 있지만 구성 중인 이메일에 따라 다릅니다.

![notifications3](assets/notifications3.png)

## 알림 보기 {#viewing-notifications}

### 웹 알림 {#web-notifications}

마법사가 만든 커뮤니티 사이트](/help/communities/sites-console.md)에는 [이제 배너 위의 사이트 헤더 표시줄에 기능에 대한 `Notifications` 링크가 포함됩니다. 메시지와 달리 알림은 모든 커뮤니티 사이트에 대해 만들어지지만 메시지는 사이트 생성 프로세스 중에 사용하도록 설정해야 합니다.

게시된 사이트를 방문할 때 `Notifications` 링크에 구성원에 대한 모든 알림이 표시됩니다.

![notifications4](assets/notifications4.png)

### 이메일 알림 {#email-notifications}

이메일 채널이 활성화되면 구성원은 웹의 콘텐츠에 대한 링크가 포함된 이메일을 받게 됩니다.

![notifications5](assets/notifications5.png)

## 이메일 알림 사용자 지정 {#customize-email-notifications}

조직은 /libs/settings/커뮤니티/templates/email/html **에서**&#x200B;템플릿을 오버레이](/help/communities/client-customize.md#overlays)하여 이메일 알림을 [사용자 지정할 수 있습니다.

예를 들어, 멘션 이메일 알림(커뮤니티 구성 요소의 경우)을 수정하려면 @mentions **지원을 활성화**&#x200B;한 구성 요소의 템플릿에서 동사 **멘션**&#x200B;에 대한 if **조건을 추가합니다**.

블로그 댓글에서 @mention에 대한 이메일 알림 템플릿 수정하려면 /libs/settings/커뮤니티/templates/email/html/social.journal.components.hbs.comment/en에 즉시 템플릿하십시오. ****

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```
