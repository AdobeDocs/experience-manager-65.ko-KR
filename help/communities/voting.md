---
title: 투표 사용
seo-title: Using Voting
description: 페이지에 투표 구성 요소 추가
seo-description: Adding the Voting component to a page
uuid: 56e6cced-2f2d-434a-8fde-92a6c2478a04
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 071cac6d-05c5-47ab-85bc-ead6693ca1f4
exl-id: aa90bf1b-6053-4949-b061-232d72b80682
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 5%

---

# 투표 사용 {#using-voting}

다음 `Voting` 구성 요소는 커뮤니티 구성원이 QnA 구성 요소 내의 답변과 같은 특정 컨텐츠 부분을 평가할 수 있도록 해주는 유용한 도구입니다. 사용 `Voting` 구성 요소에서 구성원은 위쪽 또는 아래쪽 화살표를 선택하여 의견을 나타냅니다.

## 페이지에 투표 추가 {#adding-voting-to-a-page}

을(를) 추가하려면 `Voting` 구성 요소를 페이지에 작성자 모드에서 사용하려면 구성 요소 브라우저를 사용하여 를 찾습니다 `Communities / Voting` 사용자가 투표할 수 있는 기능을 기준으로 하는 위치와 같이 페이지에 드래그합니다.

필요한 정보를 보려면 [커뮤니티 구성 요소 기본 사항](basics.md).

이 [필수 클라이언트 측 라이브러리](essentials-voting.md#essentials-for-client-side) 포함된 경우, 다음과 같이 하십시오 `Voting` 구성 요소가 나타납니다.

![투표 요소](assets/voting-component.png)

## 투표 구성 {#configuring-voting}

배치된 항목을 선택합니다 `Voting` 액세스하여 선택할 구성 요소 `Configure` 아이콘 편집 대화 상자를 엽니다.

![구성](assets/configure-new.png)

아래에 **[!UICONTROL 텍스트 및 레이블]** 탭에서 투표를 기록하는 데 사용되는 속성을 지정합니다.

![투표 레이블](assets/voting-label.png)

* **[!UICONTROL 긍정적인 응답 레이블]**

   (*필수 여부*) 양수 응답에 대한 내부 속성 이름입니다.

* **[!UICONTROL 부정적인 응답 레이블]**

   (*필수 여부*) 음수 응답에 대한 내부 속성 이름입니다.

* **[!UICONTROL Tally 이름]**

   (*필수 여부*) 선호 구성 요소의 이 인스턴스에 대한 내부 식별 가능한 속성 이름입니다.

## 사이트 방문자 경험 {#site-visitor-experience}

### 구성원 {#members}

회원들은 한 번만 투표할 수 있지만 언제든지 그들의 투표를 변경할 수 있습니다.

### 익명 {#anonymous}

익명 투표는 지원되지 않습니다. 사이트 방문자는 한 번 투표에 참여하려면 등록(회원이 되기)하고 로그인해야 합니다.

## 추가 정보 {#additional-information}

자세한 내용은 [투표 핵심 사항](essentials-voting.md) 개발자를 위한 페이지입니다.
