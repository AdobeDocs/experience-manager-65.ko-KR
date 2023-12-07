---
title: 커뮤니티 구독
description: 커뮤니티 구성원은 이메일을 통해 다른 구성원과 상호 작용합니다
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 338be220-659a-459c-8e90-55e3a11ddeb0
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 1%

---

# 커뮤니티 구독 {#communities-subscriptions}

## 개요 {#overview}

커뮤니티 기준 [FP1](deploy-communities.md#latestfeaturepack), 커뮤니티 구성원은 구독이라고 하는 기능을 사용하여 이메일을 통해 커뮤니티와 상호 작용할 수 있습니다.

구독은 와 유사합니다. [알림](notifications.md) 회원은 블로그 기사, 포럼 주제 또는 QnA 질문을 팔로우할 때 구독할 수 있습니다.

구독과 알림을 구분하는 것은 다음과 같습니다.

* 다른 회원을 팔로우하는 경우 회원이 가입할 수 없습니다.
* 구성원이 수행할 수 있는 유일한 작업은 선택하는 것입니다. `Email Subscriptions` 팔로우하는 경우.
* 이메일 회신을 구성하면, 회원은 수신된 이메일에 단순히 답장을 함으로써, 콘텐츠를 효과적으로 게시할 수 있다.

### 요구 사항 {#requirements}

**이메일 구성**

구독이 제대로 작동하고 회원이 이메일로 답장을 보내려면 이메일을 구성해야 합니다.

이메일 설정에 대한 지침은 [이메일 구성](email.md).

**구독 활성화 및 팔로우**

구독을 활성화하려면 구성 요소를 구성해야 합니다. *및* 팔로우하는 중입니다. 구독을 허용하는 기능은 다음과 같습니다 [블로그](blog-feature.md), [포럼](forum.md) 및 [QnA](working-with-qna.md).

## 다음에서 구독 {#subscriptions-from-following}

![가입-팔로우](assets/subscription-following.png)

다음 **팔로우** 단추는 항목을 활동, 구독 및/또는 알림으로 따르는 수단을 제공합니다. 매번 **팔로우** 버튼을 선택한 경우 선택 항목을 켜거나 끌 수 있습니다.

다음 방법을 선택하면 단추 텍스트가 다음으로 변경됩니다. **팔로잉**. 편의를 위해 다음을 선택할 수 있습니다. `Unfollow All` 모든 메서드를 해제합니다.

다음 **팔로우** 단추에 다음 항목이 포함됩니다. `Email Subscriptions` 옵션은 포럼, QnA 또는 블로그가 이메일 구독을 활성화하도록 구성된 경우에만 해당됩니다. 이 단추가 나타납니다.

* 활성화된 포럼의 기본 기능 페이지에서 QnA 또는 블로그는 해당 기능에 속한 모든 활동에 대한 이메일을 전송합니다.

* 포럼 주제, QnA 질문 또는 블로그 문서와 같은 특정 항목에 대한 활동이 있으면 이메일을 보냅니다.

## 이메일로 회신 {#reply-by-email}

이메일 [전자 메일로 답글을 보내도록 구성됨](email.md#configure-polling-importer)을(를) 구독한 회원은 게시된 내용과 온라인 콘텐츠에 대한 링크가 포함된 이메일을 받게 됩니다.

이메일에 회신하는 경우 회신에 입력하는 콘텐츠는 온라인으로 콘텐츠로 나타납니다.

![이메일 회신](assets/email-reply.png)

회신을 게시하는 데 걸리는 시간은 [폴링 가져오기의 업데이트 간격](email.md#configure-polling-importer).

![QA](assets/qa.png)
