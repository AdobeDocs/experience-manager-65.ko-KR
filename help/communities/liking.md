---
title: 연결 사용
description: 사용자가 댓글과 같은 특정 콘텐츠에 대한 의견을 표현할 수 있도록 좋아요 구성 요소를 추가하고 구성하는 방법에 대해 알아봅니다.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 226fa91c-4a12-4586-b694-1a52fa2ba358
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 1%

---

# 연결 사용 {#using-liking}

`Liking` 구성 요소는 사용자가 포럼 내의 댓글과 같은 특정 콘텐츠에 대한 의견을 표시할 수 있는 유용한 도구입니다. `Liking` 구성 요소를 사용하여 구성원은 긍정적인 의견을 나타내는 하트 아이콘을 선택합니다.

## 페이지에 좋아요 추가 {#adding-liking-to-a-page}

작성자 모드에서 페이지에 `Liking` 구성 요소를 추가하려면 구성 요소 브라우저를 사용하여 찾습니다

* `Communities / Liking`

사용자가 좋아할 기능을 기준으로 한 위치와 같이 페이지에 적절히 드래그합니다.

필요한 정보는 [커뮤니티 구성 요소 기본 사항](basics.md)을 참조하세요.

[필수 클라이언트측 라이브러리](essentials-liking.md#essentials-for-client-side)가 포함된 경우 `Liking` 구성 요소가 표시되는 방식입니다.

![좋아요 구성 요소](assets/liking-component.png)

## 연결 구성 {#configuring-liking}

배치된 `Liking` 구성 요소를 선택하여 편집 대화 상자를 여는 `Configure` 아이콘에 액세스하고 선택합니다.

![새로 구성](assets/configure-new.png)

**[!UICONTROL 텍스트 및 레이블]** 탭에서 좋아요 녹화에 사용되는 속성을 지정합니다.

![연결 구성](assets/configure-liking.png)

* **[!UICONTROL 긍정적인 응답 레이블]**

  (*필수*) 긍정적인 응답을 위한 속성 이름입니다.

* **[!UICONTROL 부정적 응답 레이블]**

  (*필수*) 부정적 응답에 대한 속성 이름입니다.

* **[!UICONTROL 집계 이름]**

  (*필수*) 이 투표 구성 요소 인스턴스에 대한 내부 식별 가능한 속성 이름입니다.

## 사이트 방문자 경험 {#site-visitor-experience}

### 구성원 {#members}

구성원은 언제든지 좋아요를 변경할 수 있습니다.

### 익명 {#anonymous}

익명의 좋아요 지정은 지원되지 않습니다. 사이트 방문자가 좋아요 참여하려면 등록(회원 가입)하고 로그인해야 합니다.

## 추가 정보 {#additional-information}

자세한 내용은 개발자를 위한 [Liking Essentials](essentials-liking.md) 페이지에서 확인할 수 있습니다.
