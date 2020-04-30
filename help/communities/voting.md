---
title: 투표 사용
seo-title: 투표 사용
description: 페이지에 투표 구성 요소 추가
seo-description: 페이지에 투표 구성 요소 추가
uuid: 56e6cced-2f2d-434a-8fde-92a6c2478a04
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 071cac6d-05c5-47ab-85bc-ead6693ca1f4
translation-type: tm+mt
source-git-commit: 2bcd098ae901070d5e50cd89d06c854884b4e461

---


# 투표 사용 {#using-voting}

구성 `Voting` 요소는 커뮤니티 구성원이 QnA 구성 요소 내의 응답과 같은 특정 컨텐츠의 등급을 매길 수 있도록 하는 유용한 도구입니다. 구성 요소를 사용하여 `Voting` 멤버는 위쪽 또는 아래쪽 화살표를 선택하여 의견을 표시합니다.

## 페이지에 투표 추가 {#adding-voting-to-a-page}

작성 모드에서 페이지에 구성 `Voting` `Communities / Voting` 요소를 추가하려면 구성 요소 브라우저를 사용하여 구성 요소를 찾아 페이지에 드래그합니다. 예를 들어 사용자가 투표할 수 있는 기능과 관련된 위치입니다.

필요한 정보를 보려면 커뮤니티 구성 [요소 기본 사항을 참조하십시오](basics.md).

필요한 [클라이언트측 라이브러리가](essentials-voting.md#essentials-for-client-side) `Voting` 포함되어 있으면 구성 요소가 표시되는 방식입니다.

![chlimage_1-307](assets/chlimage_1-307.png)

## 투표 구성 {#configuring-voting}

액세스할 배치된 `Voting` 구성 요소를 선택하고 편집 대화 상자를 여는 `Configure` 아이콘을 선택합니다.

![chlimage_1-308](assets/chlimage_1-308.png)

텍스트 **[!UICONTROL 및 레이블]** 탭에서 투표를 기록하는 데 사용되는 속성을 지정합니다.

![chlimage_1-309](assets/chlimage_1-309.png)

* **[!UICONTROL 긍정적인 응답 레이블]**

   (*필수*) 긍정적인 응답을 위한 내부 속성 이름입니다.

* **[!UICONTROL 부정적인 응답 레이블]**

   (*필수*) 네거티브 응답의 내부 속성 이름입니다.

* **[!UICONTROL Tally 이름]**

   (*필수*) 투표 구성 요소의 이 인스턴스에 대한 내부 식별 가능 속성 이름입니다.

## 사이트 방문자 경험 {#site-visitor-experience}

### 구성원 {#members}

회원은 한 번만 투표할 수 있지만, 언제든지 표를 변경할 수 있습니다.

### 익명 {#anonymous}

익명의 투표는 지원되지 않습니다. 사이트 방문자는 등록(회원이 되기)하고 로그인하여 한 번 투표에 참여해야 합니다.

## 추가 정보 {#additional-information}

개발자를 위한 투표 필수 [사항](essentials-voting.md) 페이지에서 자세한 내용을 확인할 수 있습니다.
