---
title: 등급 사용
description: 로그인한 커뮤니티 구성원이 등급 콘텐츠별로 자신의 의견을 표현할 수 있도록 페이지에 등급 구성 요소를 추가하는 방법을 알아봅니다.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 7534ad5d-b408-4b09-bd3d-da7ab009d55b
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 1%

---

# 등급 사용 {#using-ratings}

`Rating` 구성 요소는 독립 실행형이거나 다른 Communities 기능과 함께 사용됩니다. 이 구성 요소를 사용하면 로그인한 커뮤니티 구성원이 콘텐츠를 등급별로 자신의 의견을 표현할 수 있습니다.

## 페이지에 등급 추가 {#adding-a-rating-to-a-page}

작성자 모드에서 페이지에 `Rating` 구성 요소를 추가하려면 구성 요소 `Communities / Rating`을(를) 찾아 페이지에서 원하는 위치로 드래그합니다(예: 구성원이 평가할 기능을 기준으로 한 위치).

필요한 정보는 [커뮤니티 구성 요소 기본 사항](basics.md)을 참조하세요.

[필수 클라이언트측 라이브러리](rating-basics.md#essentials-for-client-side)가 포함된 경우 `Rating` 구성 요소가 표시되는 방식입니다.

![등급](assets/rating.png)

## 등급 구성 {#configuring-rating}

배치된 `Rating` 구성 요소를 선택하여 편집 대화 상자를 여는 `Configure` 아이콘에 액세스하고 선택합니다.

![새로 구성](assets/configure-new.png)

**[!UICONTROL 텍스트 및 레이블]** 탭에서 등급에 대한 내부 식별자를 지정합니다.

![tallyname](assets/tallyname.png)

**[!UICONTROL 집계 이름]**
(*필수*) 이 인스턴스를 고유하게 식별하는 `Rating`의 간단한 이름입니다. 저장소에 대한 유효한 노드 이름이어야 합니다.

## 사이트 방문자 경험 {#site-visitor-experience}

### 구성원 {#members}

구성원당 하나의 등급만 허용됩니다. 회원은 언제든지 등급을 변경할 수 있습니다.

### 익명 {#anonymous}

등급의 익명 게시는 지원되지 않습니다. 사이트 방문자가 참여하려면 등록(회원 가입)하고 로그인해야 합니다.

## 추가 정보 {#additional-information}

자세한 내용은 개발자를 위한 [Rating Essentials](rating-basics.md) 페이지에서 확인할 수 있습니다.
