---
title: 연결 사용
seo-title: Using Liking
description: 좋아요 구성 요소 추가 및 구성
seo-description: Adding and configuring the Liking component
uuid: 12103ab7-1a1c-49cd-8dad-6c7508b4550e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: dcde4e03-78ab-4779-96a1-05ac41f14701
exl-id: 226fa91c-4a12-4586-b694-1a52fa2ba358
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 5%

---

# 연결 사용 {#using-liking}

다음 `Liking` 구성 요소는 사용자가 포럼 내의 댓글과 같은 특정 콘텐츠에 대한 의견을 표현할 수 있는 유용한 도구입니다. 포함 `Liking` 구성 요소에서 구성원은 긍정적인 의견을 나타내는 하트 아이콘을 선택합니다.

## 페이지에 좋아요 추가 {#adding-liking-to-a-page}

을(를) 추가하려면 `Liking` 구성 요소를 페이지에 추가하려면 작성자 모드에서 구성 요소 브라우저를 사용하여

* `Communities / Liking`

및 를 페이지에 드래그하여 사용자가 좋아할 수 있는 기능에 상대적인 위치와 같은 위치에 배치합니다.

필요한 정보는 다음을 참조하십시오. [커뮤니티 구성 요소 기본 사항](basics.md).

다음의 경우 [필수 클라이언트측 라이브러리](essentials-liking.md#essentials-for-client-side) 포함됩니다. 이렇게 하면 `Liking` 구성 요소가 표시됩니다.

![호감 구성 요소](assets/liking-component.png)

## 연결 구성 {#configuring-liking}

배치된 을(를) 선택합니다 `Liking` 에 액세스하고 선택할 구성 요소 `Configure` 편집 대화 상자를 여는 아이콘.

![새로 구성](assets/configure-new.png)

아래 **[!UICONTROL 텍스트 및 레이블]** 탭에서 [좋아요]를 기록하는 데 사용되는 속성을 지정합니다.

![연결 구성](assets/configure-liking.png)

* **[!UICONTROL 긍정적인 응답 레이블]**

   (*필수*) 긍정적인 응답을 위한 속성 이름입니다.

* **[!UICONTROL 부정적인 응답 레이블]**

   (*필수*) 부정적 응답에 대한 속성 이름입니다.

* **[!UICONTROL Tally 이름]**

   (*필수*) 투표 구성 요소의 이 인스턴스에 대해 식별할 수 있는 내부 속성 이름입니다.

## 사이트 방문자 경험 {#site-visitor-experience}

### 구성원 {#members}

구성원은 언제든지 좋아요 를 변경할 수 있습니다.

### 익명 {#anonymous}

익명의 좋아요 지정은 지원되지 않습니다. 사이트 방문자가 좋아요 참여하려면 등록(회원 가입)하고 로그인해야 합니다.

## 추가 정보 {#additional-information}

자세한 내용은 [좋아요 기본 사항](essentials-liking.md) 개발자용 페이지입니다.
