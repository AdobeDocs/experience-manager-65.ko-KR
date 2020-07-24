---
title: 좋아요 사용
seo-title: 좋아요 사용
description: 좋아요 구성 요소 추가 및 구성
seo-description: 좋아요 구성 요소 추가 및 구성
uuid: 12103ab7-1a1c-49cd-8dad-6c7508b4550e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: dcde4e03-78ab-4779-96a1-05ac41f14701
translation-type: tm+mt
source-git-commit: e7268e43620860b7a1f7aa0a1f1a54199dadcf17
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 6%

---


# 좋아요 사용 {#using-liking}

구성 요소 `Liking` 는 포럼 내의 주석과 같은 특정 컨텐트에 대한 의견을 표시할 수 있는 유용한 도구입니다. 구성 요소 `Liking` 를 사용하여 구성원은 긍정 의견을 나타내기 위해 심장 아이콘을 선택합니다.

## 페이지에 좋아요 추가 {#adding-liking-to-a-page}

작성 모드에서 페이지에 `Liking` 구성 요소를 추가하려면 구성 요소 브라우저를 사용하여

* `Communities / Liking`

사용자가 좋아할만한 기능을 기준으로 하는 위치와 같이 페이지에 드래그합니다.

필요한 정보를 보려면 커뮤니티 구성 요소 [기본 사항을 방문하십시오](basics.md).

[필요한 클라이언트측 라이브러리가](essentials-liking.md#essentials-for-client-side) 포함되어 있으면 구성 요소가 표시되는 `Liking` 방식입니다.

![chlimage_1-93](assets/chlimage_1-93.png)

## 좋아요 구성 {#configuring-liking}

액세스할 배치된 `Liking` 구성 요소를 선택하고 편집 대화 상자를 여는 `Configure` 아이콘을 선택합니다.

![chlimage_1-94](assets/chlimage_1-94.png)

텍스트 및 **[!UICONTROL 레이블]** 탭 아래에서 좋아요를 기록하는 데 사용되는 속성을 지정합니다.

![chlimage_1-95](assets/chlimage_1-95.png)

* **[!UICONTROL 긍정적인 응답 레이블]**

   (*필수*) 긍정적인 응답을 위한 속성 이름입니다.

* **[!UICONTROL 부정적인 응답 레이블]**

   (*필수*) 네거티브 응답의 속성 이름입니다.

* **[!UICONTROL Tally 이름]**

   (*필수*) 투표 구성 요소의 이 인스턴스에 대한 내부 식별 가능한 속성 이름입니다.

## 사이트 방문자 경험 {#site-visitor-experience}

### 구성원 {#members}

회원은 언제든지 자신의 모습을 바꿀 수 있습니다.

### 익명 {#anonymous}

익명 좋아요 기능은 지원되지 않습니다. 사이트 방문자는 등록(회원이 되기)하고 로그인해야 좋아지는 상황에 참여할 수 있습니다.

## 추가 정보 {#additional-information}

개발자를 위한 필수 [제품](essentials-liking.md) 좋아요 페이지에 대한 자세한 내용이 나와 있습니다.
