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

구성 요소 `Rating` 는 독립형 또는 다른 커뮤니티 기능과 함께 사용됩니다. 이 구성 요소를 사용하면 로그인한 커뮤니티 구성원이 컨텐츠에 대한 등급을 매기면서 자신의 의견을 표현할 수 있습니다.

## Adding a Rating to a Page {#adding-a-rating-to-a-page}

작성 모드에서 페이지에 구성 `Rating` 요소를 추가하려면 구성 요소를 찾아 `Communities / Rating` 페이지에 배치합니다. 예를 들어 등급을 매길 멤버에 대한 기능에 상대적인 위치입니다.

필요한 정보를 보려면 커뮤니티 구성 요소 [기본 사항을 방문하십시오](basics.md).

[필요한 클라이언트측 라이브러리가](rating-basics.md#essentials-for-client-side) 포함되어 있으면 구성 요소가 표시되는 `Rating` 방식입니다.

![등급](assets/rating.png)

## 등급 구성 {#configuring-rating}

액세스할 배치된 `Rating` 구성 요소를 선택하고 편집 대화 상자를 여는 `Configure` 아이콘을 선택합니다.

![configure-new](assets/configure-new.png)

텍스트 및 **[!UICONTROL 레이블]** 탭 아래에서 등급에 대한 내부 식별자를 지정합니다.

![tallyname](assets/tallyname.png)

**[!UICONTROL Tally Name]**(*필수*) `Rating` 이 인스턴스를 고유하게 식별하는 간단한 이름입니다. 저장소에 대한 유효한 노드 이름이어야 합니다.

## 사이트 방문자 경험 {#site-visitor-experience}

### 구성원 {#members}

멤버당 1개의 등급만 허용됩니다. 회원은 언제든지 등급을 변경할 수 있습니다.

### 익명 {#anonymous}

등급의 익명 게시는 지원되지 않습니다. 사이트 방문자는 등록(회원이 되기)하고 로그인해야 참여합니다.

## 추가 정보 {#additional-information}

개발자를 위한 필수 [등급](rating-basics.md) 페이지에 대한 자세한 내용이 나와 있습니다.
