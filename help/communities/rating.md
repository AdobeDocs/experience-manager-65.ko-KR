---
title: 등급 사용
seo-title: 등급 사용
description: 페이지에 등급 구성 요소 추가
seo-description: 페이지에 등급 구성 요소 추가
uuid: a986970b-1221-4648-9a69-410f4480e0ae
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: a0e5491e-66bc-47b0-94a5-45a02bc558da
translation-type: tm+mt
source-git-commit: 0051791da06d15a48b82cf93164a89b4ea42ce98
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 2%

---


# 등급 사용 {#using-ratings}

`Rating` 구성 요소는 독립형이거나 다른 커뮤니티 기능과 함께 사용됩니다. 이 구성 요소를 사용하면 로그인한 커뮤니티 구성원이 컨텐츠에 대한 등급을 매겨 자신의 의견을 표현할 수 있습니다.

## 페이지 {#adding-a-rating-to-a-page}에 등급 추가

작성 모드에서 페이지에 `Rating` 구성 요소를 추가하려면 구성 요소 `Communities / Rating`을 찾아 등급을 매길 멤버에 대한 기능과 관련된 위치와 같이 페이지에 배치합니다.

필요한 정보를 보려면 [커뮤니티 구성 요소 기본 사항](basics.md)을 방문하십시오.

[필수 클라이언트측 라이브러리](rating-basics.md#essentials-for-client-side)가 포함될 때 `Rating` 구성 요소가 표시되는 방법입니다.

![등급](assets/rating.png)

## 등급 {#configuring-rating} 구성

액세스할 배치된 `Rating` 구성 요소를 선택하고 편집 대화 상자를 여는 `Configure` 아이콘을 선택합니다.

![configure-new](assets/configure-new.png)

**[!UICONTROL 텍스트 및 레이블]** 탭에서 등급에 대한 내부 식별자를 지정합니다.

![tallyname](assets/tallyname.png)

**[!UICONTROL 총계 이름]**
(*필수*)이  `Rating` 이 인스턴스를 고유하게 식별하는 간단한 이름입니다. 저장소에 대한 유효한 노드 이름이어야 합니다.

## 사이트 방문자 경험 {#site-visitor-experience}

### 구성원 {#members}

멤버당 한 개의 등급만 허용됩니다. 회원은 언제든지 등급을 변경할 수 있습니다.

### 익명 {#anonymous}

평점의 익명 게시는 지원되지 않습니다. 사이트 방문자는 등록을 하고(회원이 됨) 로그인해야 참여합니다.

## 추가 정보 {#additional-information}

개발자를 위한 [Rating Essentials](rating-basics.md) 페이지에 자세한 내용이 있을 수 있습니다.
