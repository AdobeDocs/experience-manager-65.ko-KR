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
source-git-commit: e4456e80059479ca874681e20f8546f29ac92597

---


# 좋아요 사용 {#using-liking}

구성 `Liking` 요소는 사용자가 포럼 내의 주석과 같은 특정 컨텐츠에 대한 의견을 표현할 수 있도록 하는 유용한 도구입니다. 구성 요소를 사용하여 멤버는 `Liking` 하트 아이콘을 선택하여 긍정적인 의견을 표시합니다.

## 페이지에 좋아요 추가 {#adding-liking-to-a-page}

작성 모드에서 페이지에 `Liking` 구성 요소를 추가하려면 구성 요소 브라우저를 사용하여 다음을 찾습니다.

* `Communities / Liking`

사용자가 좋아하는 기능과 관련된 위치와 같이 페이지에 드래그합니다.

필요한 정보를 보려면 커뮤니티 구성 [요소 기본 사항을 참조하십시오](basics.md).

필요한 [클라이언트측 라이브러리가](essentials-liking.md#essentials-for-client-side) `Liking` 포함되어 있으면 구성 요소가 표시되는 방식입니다.

![chlimage_1-93](assets/chlimage_1-93.png)

## 좋아요 구성 {#configuring-liking}

액세스할 배치된 `Liking` 구성 요소를 선택하고 편집 대화 상자를 여는 `Configure` 아이콘을 선택합니다.

![chlimage_1-94](assets/chlimage_1-94.png)

텍스트 **[!UICONTROL 및 레이블]** 탭에서 좋아요를 기록하는 데 사용되는 속성을 지정합니다.

![chlimage_1-95](assets/chlimage_1-95.png)

* **[!UICONTROL 긍정적인 응답 레이블]**

   (*필수*) 긍정적인 응답의 속성 이름입니다.

* **[!UICONTROL 부정적인 응답 레이블]**

   (*필수*) 음수 응답의 속성 이름입니다.

* **[!UICONTROL Tally 이름]**

   (*필수*) 투표 구성 요소의 이 인스턴스에 대한 내부 식별 가능 속성 이름입니다.

## 사이트 방문자 경험 {#site-visitor-experience}

### 구성원 {#members}

멤버는 언제든지 자신의 모습을 바꿀 수 있습니다.

### 익명 {#anonymous}

익명 좋아요 기능은 지원되지 않습니다. 사이트 방문자는 등록(회원이 되기)하고 로그인하여 좋아요를 표시해야 합니다.

## 추가 정보 {#additional-information}

개발자를 위한 기본 사항 좋아하기 [페이지에서 자세한](essentials-liking.md) 내용을 참조할 수 있습니다.
