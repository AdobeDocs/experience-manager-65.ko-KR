---
title: 커뮤니티 구독
seo-title: 커뮤니티 구독
description: 커뮤니티 구성원은 이메일을 통해 다른 구성원과 상호 작용합니다.
seo-description: 커뮤니티 구성원은 이메일을 통해 다른 구성원과 상호 작용합니다.
uuid: a4b98769-c219-4e18-8e80-9a806ab979ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 33c85af4-4c56-487a-ba60-55211cb9f72c
translation-type: tm+mt
source-git-commit: 3296db289b2e2f4ca0d1981597ada6ca1310bd46

---


# 커뮤니티 구독 {#communities-subscriptions}

## 개요 {#overview}

Communities FP [1의](deploy-communities.md#latestfeaturepack)경우 커뮤니티 구성원은 가입이라고 하는 기능을 사용하여 이메일을 통해 커뮤니티와 교류할 수 있습니다.

구독은 블로그 기사, 포럼 주제 또는 QnA 질문을 팔로우할 때 회원이 가입할 수 있는 [알림과](notifications.md) 유사합니다.

가입과 알림의 차이점은 다음과 같습니다.

* 다른 구성원을 팔로우하는 경우 회원은 가입할 수 없습니다.
* 멤버가 수행할 수 있는 유일한 작업은 `Email Subscriptions` 다음을 선택할 때 선택합니다.
* 이메일 회신이 구성되면 회원은 수신한 이메일에 간단하게 답글을 달아서 컨텐츠를 효과적으로 게시할 수 있습니다.

### 요구 사항 {#requirements}

**이메일 구성**

구독이 제대로 작동하고 회원이 이메일로 회신하려면 이메일을 구성해야 합니다.

이메일 설정에 대한 지침은 이메일 구성을 [참조하십시오](email.md).

**구독 활성화 및 팔로우**

가입 *및* 팔로잉을 사용하도록 구성 요소를 구성해야 합니다. 구독을 허용하는 기능은 [블로그](blog-feature.md), [포럼](forum.md) 및 QnA [입니다](working-with-qna.md).

## 다음의 구독 {#subscriptions-from-following}

![chlimage_1-5](assets/chlimage_1-5.png)

[ **따라하기** ] 단추는 활동, 구독 및/또는 알림으로 항목을 팔로우하는 방법을 제공합니다. [ **따라하기** ] 단추를 선택할 때마다 선택 항목을 켜거나 끌 수 있습니다.

다음 방법을 선택하면 단추 텍스트가 **다음과 같이 변경됩니다**. 편의를 위해 모든 방법을 전환하도록 선택할 `Unfollow All` 수 있습니다.

[ **팔로우** ] 단추에는 포럼, QnA 또는 블로그가 이메일 구독을 사용하도록 구성된 경우에만 `Email Subscriptions` 옵션이 포함됩니다. 이 단추가 표시됩니다.

* 활성화된 포럼, QnA 또는 블로그의 기본 기능 페이지에서 해당 기능 아래의 모든 활동에 대한 이메일을 보냅니다.

* 포럼 주제, QnA 질문 또는 블로그 아티클과 같은 특정 항목의 경우 해당 특정 항목에 대한 활동이 있을 때 이메일을 보냅니다.

## 이메일로 회신 {#reply-by-email}

이메일을 통해 [회신하도록](email.md#configure-polling-importer)구성한 경우 구독을 한 회원은 게시된 컨텐츠와 온라인 컨텐츠의 링크가 포함된 이메일을 받게 됩니다.

응답자가 이메일에 회신하면 응답에 입력한 컨텐츠가 온라인으로 표시됩니다.

![chlimage_1-6](assets/chlimage_1-6.png)

답글을 게시하는 데 걸리는 시간은 [폴링 가져오기의 업데이트 간격에](email.md#configure-polling-importer)의해 제어됩니다.

![chlimage_1-7](assets/chlimage_1-7.png)

