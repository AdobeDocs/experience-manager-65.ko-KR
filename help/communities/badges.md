---
title: 배지 콘솔
description: 커뮤니티 배지 콘솔을 사용하면 회원이 획득(수상)하거나 커뮤니티에서 특정 역할을 수행할 때(할당)에 표시할 수 있는 사용자 정의 배지를 추가할 수 있습니다
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 50ed9ec4-ff04-4f9d-aefb-0837542a9455
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 4%

---

# 배지 콘솔 {#badges-console}

## 배지 정보 {#about-badges}

커뮤니티 배지 콘솔을 사용하면 획득(수여) 또는 커뮤니티에서 특정 역할을 수행할(할당) 때 멤버에 대해 표시할 수 있는 사용자 정의 배지를 추가할 수 있습니다.

### 배지 가시성 {#badge-visibility}

현재 커뮤니티 회원이 획득하거나 할당된 배지가 이름 및 아바타와 함께 다음 위치에 나타납니다.

* 프로필
* [포럼](/help/communities/forum.md)
* [QnA](/help/communities/working-with-qna.md)
* [순위표](/help/communities/enabling-leaderboard.md)
* [관념화](/help/communities/ideation-feature.md)

작성 환경에서 배지 콘솔로 이동합니다.

* 전역 탐색에서: **[!UICONTROL 도구]** > **[!UICONTROL 커뮤니티]** > **[!UICONTROL 배지]**

이 콘솔에는 현재 사용 가능하고 새 배지를 추가할 수 있는 배지가 표시됩니다.

![배지-홈 페이지](assets/badges-homepage.png)

## 배지 만들기 {#create-badge}

배지는 적절한 작은 이미지(높이 72dpi, 26~32픽셀)를 업로드하고 이름을 제공하여 만들어집니다. 배지 이미지는 다음 위치의 저장소에 저장됩니다. `/libs/settings/community/badging/images` 및 이 게시 환경에 자동으로 복제됩니다.

게시 환경이 게시자의 팜인 경우 를 구성해야 합니다. [사용자 동기화](/help/communities/sync.md).

![배지 만들기](assets/create-badge.png)

* **이미지 업로드**

  (*필수*) JPEG 또는 PNG 포맷으로 권장 크기가 32 x 32 픽셀(72dpi)인 배지 이미지입니다.

* **이름**

  (*필수*) 배지 이름입니다. 기본값입니다 `Display Name` 및 저장소 노드 이름입니다. 다음과 같은 경우 `Name` 은(는) 유효한 저장소 노드 이름이 아닙니다. 수정되었습니다.

* **표시 이름**

  (*선택 사항*) 사용자 인터페이스에 배지에 대해 표시할 이름입니다. 기본값은 다음에 대해 입력된 변경되지 않은 텍스트입니다. `Name`.

* **설명**

  (*선택 사항*) 배지에 대한 설명입니다.

## 추가 정보 {#additional-information}

채점 및 배지 규칙 설정에 대한 자세한 내용은 을 참조하십시오. [채점 및 배지](/help/communities/implementing-scoring.md).

멤버의 배지 관리에 대해서는 다음을 참조하십시오. [구성원 콘솔](/help/communities/members.md).
