---
title: 좋아요 사용
seo-title: 좋아요 사용
description: 연결 구성 요소 추가 및 구성
seo-description: 연결 구성 요소 추가 및 구성
uuid: 12103ab7-1a1c-49cd-8dad-6c7508b4550e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: dcde4e03-78ab-4779-96a1-05ac41f14701
exl-id: 226fa91c-4a12-4586-b694-1a52fa2ba358
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 5%

---

# {#using-liking} 좋아요 사용

`Liking` 구성 요소는 사용자가 포럼 내의 댓글과 같은 특정 컨텐츠에 대한 의견을 표현할 수 있도록 해주는 유용한 도구입니다. `Liking` 구성 요소를 사용하여 구성원은 하트아이콘을 선택하여 긍정적인 의견을 나타냅니다.

## 페이지에 연결 추가 {#adding-liking-to-a-page}

작성자 모드의 페이지에 `Liking` 구성 요소를 추가하려면 구성 요소 브라우저를 사용하여 을 찾습니다

* `Communities / Liking`

사용자가 원하는 기능을 기준으로 할 위치와 같이 페이지에 드래그합니다.

필요한 정보를 보려면 [커뮤니티 구성 요소 기본 사항](basics.md)을 방문하십시오.

필요한 [클라이언트 측 라이브러리](essentials-liking.md#essentials-for-client-side)가 포함되면 이 방법으로 `Liking` 구성 요소가 표시됩니다.

![연결 구성 요소](assets/liking-component.png)

## {#configuring-liking} 연결 구성

액세스할 배치된 `Liking` 구성 요소를 선택하고 편집 대화 상자를 여는 `Configure` 아이콘을 선택합니다.

![configure-new](assets/configure-new.png)

**[!UICONTROL 텍스트 및 레이블]** 탭에서 좋아하는 항목을 기록하는 데 사용되는 속성을 지정합니다.

![configure-linking](assets/configure-liking.png)

* **[!UICONTROL 긍정적인 응답 레이블]**

   (*필수*) 양의 응답에 대한 속성 이름입니다.

* **[!UICONTROL 부정적인 응답 레이블]**

   (*필수*) 음수 응답에 대한 속성 이름입니다.

* **[!UICONTROL Tally 이름]**

   (*필수*) 투표 구성 요소의 이 인스턴스에 대한 내부 식별 가능한 속성 이름입니다.

## 사이트 방문자 경험 {#site-visitor-experience}

### 구성원 {#members}

회원들은 언제든지 그들의 모습을 바꿀 수 있다.

### 익명 {#anonymous}

익명 연결은 지원되지 않습니다. 사이트 방문자가 등록을 하고(구성원이 되기) 로그인해야 해당 내용에 참여할 수 있습니다.

## 추가 정보 {#additional-information}

개발자를 위한 [Linking Essentials](essentials-liking.md) 페이지에서 자세한 내용을 확인할 수 있습니다.
