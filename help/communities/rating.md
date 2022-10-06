---
title: 등급 사용
seo-title: Using Ratings
description: 페이지에 등급 구성 요소 추가
seo-description: Adding a Rating component to a page
uuid: a986970b-1221-4648-9a69-410f4480e0ae
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: a0e5491e-66bc-47b0-94a5-45a02bc558da
exl-id: 7534ad5d-b408-4b09-bd3d-da7ab009d55b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 2%

---

# 등급 사용 {#using-ratings}

다음 `Rating` 구성 요소는 독립형 또는 다른 커뮤니티 기능과 함께 사용됩니다. 이 구성 요소를 사용하면 로그인한 커뮤니티 구성원이 등급 컨텐츠로 자신의 의견을 표현할 수 있습니다.

## 페이지에 등급 추가 {#adding-a-rating-to-a-page}

을(를) 추가하려면 `Rating` 구성 요소를 페이지에 작성자 모드에서 찾아 구성 요소를 찾습니다 `Communities / Rating` 등급을 매길 기능을 기준으로 하는 위치와 같이 페이지에 배치합니다.

필요한 정보를 보려면 [커뮤니티 구성 요소 기본 사항](basics.md).

이 [필수 클라이언트 측 라이브러리](rating-basics.md#essentials-for-client-side) 포함된 경우, 다음과 같이 하십시오 `Rating` 구성 요소가 나타납니다.

![등급](assets/rating.png)

## 등급 구성 {#configuring-rating}

배치된 항목을 선택합니다 `Rating` 액세스하여 선택할 구성 요소 `Configure` 아이콘 편집 대화 상자를 엽니다.

![configure-new](assets/configure-new.png)

아래에 **[!UICONTROL 텍스트 및 레이블]** 탭에서는 등급에 대한 내부 식별자를 지정합니다.

![tallyname](assets/tallyname.png)

**[!UICONTROL 총명]**
(*필수 여부*) 간단한 `Rating` 은 이 인스턴스를 고유하게 식별합니다. 리포지토리에 유효한 노드 이름이어야 합니다.

## 사이트 방문자 경험 {#site-visitor-experience}

### 구성원 {#members}

멤버당 하나의 등급만 허용됩니다. 회원은 언제든지 등급을 변경할 수 있습니다.

### 익명 {#anonymous}

등급 익명의 게시는 지원되지 않습니다. 사이트 방문자는 등록(구성원 자격)하고 로그인해야 참여합니다.

## 추가 정보 {#additional-information}

자세한 내용은 [등급 핵심 사항](rating-basics.md) 개발자를 위한 페이지입니다.
