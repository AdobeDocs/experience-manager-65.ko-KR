---
title: 커뮤니티 구독
seo-title: 커뮤니티 구독
description: 커뮤니티 구성원은 이메일을 통해 다른 구성원과 상호 작용합니다
seo-description: 커뮤니티 구성원은 이메일을 통해 다른 구성원과 상호 작용합니다
uuid: a4b98769-c219-4e18-8e80-9a806ab979ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 33c85af4-4c56-487a-ba60-55211cb9f72c
role: Administrator
exl-id: 338be220-659a-459c-8e90-55e3a11ddeb0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 2%

---

# 커뮤니티 구독 {#communities-subscriptions}

## 개요 {#overview}

커뮤니티 [FP1](deploy-communities.md#latestfeaturepack)부터는 커뮤니티 멤버가 구독이라고 하는 기능을 사용하여 이메일을 통해 커뮤니티와 상호 작용할 수 있습니다.

구독은 구성원이 다음 블로그 문서, 포럼 주제 또는 QnA 질문을 할 때 구독할 수 있으므로 [notifications](notifications.md)와 유사합니다.

알림과 구독을 구분하는 것은 다음과 같습니다.

* 다른 구성원을 따르는 경우 구성원이 가입할 수 없습니다.
* 구성원이 수행할 수 있는 유일한 작업은 다음과 같은 경우 `Email Subscriptions`을 선택하는 것입니다.
* 이메일 응답이 구성되면 구성원은 받은 이메일에 단순히 답글을 달아서 컨텐츠를 효과적으로 게시할 수 있습니다.

### 요구 사항 {#requirements}

**이메일 구성**

구독이 작동하고 구성원이 이메일로 응답하도록 이메일을 구성해야 합니다.

이메일 설정에 대한 지침은 [이메일 구성](email.md)을 참조하십시오.

**구독 활성화 및 팔로우**

다음 구독 *및*&#x200B;을 사용하도록 구성 요소를 구성해야 합니다. 구독을 허용하는 기능은 [블로그](blog-feature.md), [포럼](forum.md) 및 [QnA](working-with-qna.md)입니다.

## 다음 {#subscriptions-from-following}의 구독

![구독 후](assets/subscription-following.png)

**팔로우** 버튼은 항목을 활동, 구독 및/또는 알림으로 따르는 수단을 제공합니다. **팔로우** 단추를 선택할 때마다 선택 항목을 켜거나 끌 수 있습니다.

다음 방법을 선택하면 단추의 텍스트가 **Following**&#x200B;으로 변경됩니다. 편의를 위해 `Unfollow All` 을 선택하여 모든 메서드를 해제할 수 있습니다.

**팔로우** 단추에는 포럼, QnA 또는 블로그가 이메일 구독을 사용하도록 구성된 경우에만 `Email Subscriptions` 옵션이 포함됩니다. 이 단추가 나타납니다.

* 활성화된 포럼, QnA 또는 블로그 의 기본 기능 페이지에서 해당 기능 아래에 있는 모든 활동에 대한 이메일을 전송합니다.

* 포럼 주제, 질문 또는 블로그 문서와 같은 특정 항목의 경우 해당 특정 항목에 대한 활동이 있으면 이메일을 전송합니다.

## 전자 메일로 회신 {#reply-by-email}

이메일이 [전자 메일](email.md#configure-polling-importer)에 응답하도록 구성되어 있는 경우, 가입한 구성원은 게시된 컨텐츠와 온라인 컨텐츠에 대한 링크를 포함한 이메일을 받게 됩니다.

응답자가 전자 메일에 회신하면 응답에 입력한 컨텐츠가 온라인으로 표시됩니다.

![이메일 회신](assets/email-reply.png)

응답을 게시하는 데 걸리는 시간은 [폴링 임포터의 업데이트 간격](email.md#configure-polling-importer)에 의해 제어됩니다.

![QA](assets/qa.png)
