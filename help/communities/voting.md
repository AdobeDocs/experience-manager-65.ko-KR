---
title: 투표 사용
description: 로그인한 커뮤니티 구성원이 답변과 같은 특정 콘텐츠를 평가할 수 있도록 페이지에 투표 구성 요소를 추가하는 방법을 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: aa90bf1b-6053-4949-b061-232d72b80682
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 1%

---

# 투표 사용 {#using-voting}

다음 `Voting` 구성 요소는 커뮤니티 구성원이 QnA 구성 요소 내의 답변과 같은 특정 콘텐츠에 대해 등급을 지정할 수 있는 유용한 도구입니다. 포함 `Voting` 구성 요소, 멤버는 위쪽 또는 아래쪽 화살표를 선택하여 의견을 나타냅니다.

## 페이지에 투표 추가 {#adding-voting-to-a-page}

을(를) 추가하려면 `Voting` 작성자 모드에서 페이지에 대한 구성 요소를 보려면 구성 요소 브라우저를 사용하십시오. 찾기 `Communities / Voting` 및 을 페이지에 드래그하여 사용자가 투표할 수 있는 기능에 상대적인 위치와 같은 작업을 수행합니다.

필요한 정보는 다음을 참조하십시오. [커뮤니티 구성 요소 기본 사항](basics.md).

다음의 경우 [필수 클라이언트측 라이브러리](essentials-voting.md#essentials-for-client-side) 포함됩니다. 이렇게 하면 `Voting` 구성 요소가 표시됩니다.

![투표 구성 요소](assets/voting-component.png)

## 투표 구성 {#configuring-voting}

배치된 을(를) 선택합니다 `Voting` 에 액세스하고 선택할 수 있는 구성 요소 `Configure` 편집 대화 상자를 여는 아이콘.

![구성](assets/configure-new.png)

아래 **[!UICONTROL 텍스트 및 레이블]** 탭에서 투표를 기록하는 데 사용되는 속성을 지정합니다.

![투표 표시](assets/voting-label.png)

* **[!UICONTROL 긍정적인 응답 레이블]**

  (*필수*) 긍정적인 응답을 위한 내부 속성 이름입니다.

* **[!UICONTROL 부정적 응답 레이블]**

  (*필수*) 부정적 응답에 대한 내부 속성 이름입니다.

* **[!UICONTROL Tally 이름]**

  (*필수*) 투표 구성 요소의 이 인스턴스에 대해 식별할 수 있는 내부 속성 이름입니다.

## 사이트 방문자 경험 {#site-visitor-experience}

### 구성원 {#members}

구성원은 한 번만 투표할 수 있지만, 언제든지 자신의 투표를 변경할 수 있습니다.

### 익명 {#anonymous}

익명 투표는 지원되지 않습니다. 사이트 방문자가 한 번 투표에 참여하려면 등록(회원 가입)하고 로그인해야 합니다.

## 추가 정보 {#additional-information}

자세한 내용은 [투표 기본 사항](essentials-voting.md) 개발자용 페이지입니다.
