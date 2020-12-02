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
source-git-commit: c9fa5624a59f4b9a6f970628b03bbd8b7a277a73
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 5%

---


# {#using-liking} 좋아요 사용

`Liking` 구성 요소는 사용자가 포럼 내의 댓글과 같은 특정 컨텐트에 대한 의견을 표현할 수 있도록 하는 유용한 도구입니다. `Liking` 구성 요소를 사용하여 멤버는 하트 아이콘을 선택하여 긍정적인 의견을 표시합니다.

## 페이지에 좋아요 추가 {#adding-liking-to-a-page}

작성 모드에서 페이지에 `Liking` 구성 요소를 추가하려면 구성 요소 브라우저를 사용하여

* `Communities / Liking`

사용자가 좋아할만한 기능을 기준으로 하는 위치와 같이 페이지에 드래그합니다.

필요한 정보를 보려면 [커뮤니티 구성 요소 기본 사항](basics.md)을 방문하십시오.

[필수 클라이언트측 라이브러리](essentials-liking.md#essentials-for-client-side)가 포함될 때 이 방법으로 `Liking` 구성 요소가 표시됩니다.

![좋아요 구성 요소](assets/liking-component.png)

## {#configuring-liking} 좋아요 구성

액세스할 배치된 `Liking` 구성 요소를 선택하고 편집 대화 상자를 여는 `Configure` 아이콘을 선택합니다.

![configure-new](assets/configure-new.png)

**[!UICONTROL 텍스트 및 레이블]** 탭에서 좋아요를 기록하는 데 사용되는 속성을 지정합니다.

![configure-like](assets/configure-liking.png)

* **[!UICONTROL 긍정적인 응답 레이블]**

   (*필수*) 긍정적인 응답을 위한 속성 이름입니다.

* **[!UICONTROL 부정적인 응답 레이블]**

   (*필수*) 음수 응답의 속성 이름입니다.

* **[!UICONTROL Tally 이름]**

   (*필수*) 투표 구성 요소의 이 인스턴스에 대한 식별 가능한 내부 속성 이름입니다.

## 사이트 방문자 경험 {#site-visitor-experience}

### 구성원 {#members}

회원은 언제든지 자신의 모습을 바꿀 수 있습니다.

### 익명 {#anonymous}

익명 좋아요 기능은 지원되지 않습니다. 사이트 방문자는 등록(회원이 되기)하고 로그인해야 좋아지는 상황에 참여할 수 있습니다.

## 추가 정보 {#additional-information}

개발자를 위한 [필수 패키지](essentials-liking.md) 페이지에 더 많은 정보가 있을 수 있습니다.
