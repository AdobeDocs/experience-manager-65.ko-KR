---
title: 커뮤니티 가입
seo-title: 커뮤니티 가입
description: 커뮤니티 멤버는 이메일을 통해 다른 구성원과 상호 작용할 수 있습니다.
seo-description: 커뮤니티 멤버는 이메일을 통해 다른 구성원과 상호 작용할 수 있습니다.
uuid: a4b98769-c219-4e18-8e80-9a806ab979ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 33c85af4-4c56-487a-ba60-55211cb9f72c
translation-type: tm+mt
source-git-commit: 2fcd87cd1def7fc265ba40c83b50db86618f3b70
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---


# 커뮤니티 구독 {#communities-subscriptions}

## 개요 {#overview}

커뮤니티 [FP1](deploy-communities.md#latestfeaturepack)의 경우 커뮤니티 구성원은 가입이라고 하는 기능을 사용하여 이메일을 통해 커뮤니티와 상호 작용할 수 있습니다.

구독은 회원이 블로그 기사, 포럼 주제 또는 QnA 질문 다음에 가입할 때 가입할 수 있으므로 [알림](notifications.md)과 유사합니다.

알림과 가입을 구분하는 것은 다음과 같습니다.

* 다른 구성원을 팔로우하는 경우 회원은 가입할 수 없습니다.
* 멤버가 다음을 수행할 때 `Email Subscriptions`을(를) 선택하면 됩니다.
* 이메일 회신이 구성되면, 회원은 받은 이메일에 단순히 답글을 달아서 컨텐츠를 효과적으로 게시할 수 있습니다.

### 요구 사항 {#requirements}

**이메일 구성**

구독이 제대로 작동하고 회원이 이메일을 통해 회신하려면 이메일을 구성해야 합니다.

이메일 설정에 대한 지침은 [이메일 구성](email.md)을 참조하십시오.

**구독 활성화 및 팔로우**

*및* 다음에 대한 구독을 사용하도록 구성 요소를 구성해야 합니다. 구독을 허용하는 기능은 [블로그](blog-feature.md), [포럼](forum.md) 및 [QnA](working-with-qna.md)입니다.

## 다음 {#subscriptions-from-following}의 구독

![가입 후](assets/subscription-following.png)

**Follow** 단추는 항목 다음에 활동, 구독 및/또는 알림을 제공합니다. **팔로우** 단추를 선택할 때마다 선택 항목을 켜거나 끌 수 있습니다.

다음 방법을 선택하면 단추의 텍스트가 **Following**&#x200B;으로 변경됩니다. 편의를 위해 `Unfollow All`을 선택하여 모든 메서드를 전환할 수 있습니다.

**팔로우** 버튼에는 포럼, QnA 또는 블로그가 이메일 구독을 사용하도록 구성된 경우에만 `Email Subscriptions` 옵션이 포함됩니다. 이 단추가 표시됩니다.

* 활성화된 포럼, QnA 또는 블로그의 기본 기능 페이지에서 해당 기능 아래의 모든 활동에 대한 이메일을 전송합니다.

* 포럼 주제, QnA 질문, 블로그 기사 등 특정 항목에 대한 활동이 있는 경우 이메일을 보냅니다.

## 전자 메일 {#reply-by-email}(으)로 회신

이메일이 [이메일](email.md#configure-polling-importer)에 답글을 남길 수 있도록 구성되면 가입한 회원은 게시된 컨텐트와 온라인 컨텐트에 대한 링크가 포함된 이메일을 수신하게 됩니다.

응답자가 이메일에 회신을 하면 응답에 입력한 컨텐츠가 온라인으로 콘텐트로 표시됩니다.

![이메일 회신](assets/email-reply.png)

응답을 게시하는 데 걸리는 시간은 [폴링 가져오기의 업데이트 간격](email.md#configure-polling-importer)에 의해 제어됩니다.

![QA](assets/qa.png)

