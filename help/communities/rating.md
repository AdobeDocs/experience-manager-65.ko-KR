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

다음 `Rating` 구성 요소는 독립 실행형이나 다른 Communities 기능과 함께 사용됩니다. 이 구성 요소를 사용하면 로그인한 커뮤니티 구성원이 콘텐츠를 등급별로 자신의 의견을 표현할 수 있습니다.

## 페이지에 등급 추가 {#adding-a-rating-to-a-page}

을(를) 추가하려면 `Rating` 구성 요소를 페이지에 추가하려면 작성자 모드에서 구성 요소를 찾습니다. `Communities / Rating` 을 페이지의 위치로 드래그합니다(예: 멤버가 등급을 매길 기능을 기준으로 한 위치).

필요한 정보는 다음을 참조하십시오. [커뮤니티 구성 요소 기본 사항](basics.md).

다음의 경우 [필수 클라이언트측 라이브러리](rating-basics.md#essentials-for-client-side) 포함됩니다. 이렇게 하면 `Rating` 구성 요소가 표시됩니다.

![등급](assets/rating.png)

## 등급 구성 {#configuring-rating}

배치된 을(를) 선택합니다 `Rating` 에 액세스하고 선택할 구성 요소 `Configure` 편집 대화 상자를 여는 아이콘.

![새로 구성](assets/configure-new.png)

아래 **[!UICONTROL 텍스트 및 레이블]** 탭에서는 등급에 대한 내부 식별자를 지정합니다.

![tallyname](assets/tallyname.png)

**[!UICONTROL Tally 이름]**
(*필수*) 간단한 이름 `Rating` 이 인스턴스를 고유하게 식별합니다. 저장소에 대한 유효한 노드 이름이어야 합니다.

## 사이트 방문자 경험 {#site-visitor-experience}

### 구성원 {#members}

구성원당 하나의 등급만 허용됩니다. 회원은 언제든지 등급을 변경할 수 있습니다.

### 익명 {#anonymous}

등급의 익명 게시는 지원되지 않습니다. 사이트 방문자가 참여하려면 등록(회원 가입)하고 로그인해야 합니다.

## 추가 정보 {#additional-information}

자세한 내용은 [등급 기본 사항](rating-basics.md) 개발자용 페이지입니다.
