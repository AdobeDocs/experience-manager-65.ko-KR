---
title: 배지 콘솔
seo-title: Badges Console
description: Communities Badge 콘솔을 사용하면 수익을 낼 때(수상) 또는 커뮤니티에서 특정 역할을 수행할 때(지정된) 회원에게 표시될 수 있는 사용자 지정 배지를 추가할 수 있습니다
seo-description: The Communities Badges console lets you add custom badges that can be displayed for members when earned (awarded) or when they take on a specific role in the community (assigned)
uuid: 7103b133-ef3f-47d6-a2dc-4e6ff92e8fed
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 135b3077-5343-4888-858d-de5e9b1d4b04
docset: aem65
role: Admin
exl-id: 50ed9ec4-ff04-4f9d-aefb-0837542a9455
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 4%

---

# 배지 콘솔 {#badges-console}

## 배지 정보 {#about-badges}

Communities Badge 콘솔에서는 수익을 내거나 커뮤니티에서 특정 역할을 수행할 때(지정된) 회원에게 표시될 수 있는 사용자 지정 배지를 추가하는 기능을 제공합니다.

### 배지 가시성 {#badge-visibility}

현재, 한 커뮤니티 구성원이 번거나 배정되는 배지는 다음 위치에 그들의 이름과 아바타와 함께 나타납니다.

* 프로필
* [포럼](/help/communities/forum.md)
* [QnA](/help/communities/working-with-qna.md)
* [리드보드](/help/communities/enabling-leaderboard.md)
* [관념화](/help/communities/ideation-feature.md)

작성 환경에서 Badge 콘솔로 이동합니다.

* 전역 탐색에서: **[!UICONTROL 도구]** > **[!UICONTROL 커뮤니티]** > **[!UICONTROL 배지]**

이 콘솔에는 현재 사용 가능한 배지와 새 배지를 추가할 수 있는 배지가 표시됩니다.

![배지 홈페이지](assets/badges-homepage.png)

## 배지 만들기 {#create-badge}

배지는 26~32픽셀 범위의 높이로 적절하게 작은 이미지(72dpi)를 업로드하고 이름을 제공하여 만들어집니다. 배지 이미지는 다음 저장소에 저장됩니다. `/libs/settings/community/badging/images` 및 은 게시 환경에 자동으로 복제됩니다.

게시 환경이 게시자의 팜인 경우 구성해야 합니다 [사용자 동기화](/help/communities/sync.md).

![create-badge](assets/create-badge.png)

* **이미지 업로드**

   (*필수 여부*) JPEG 또는 PNG 포맷의 권장 크기가 32 x 32픽셀인 배지 이미지입니다.

* **이름**

   (*필수 여부*) 배지 이름입니다. 기본값입니다 `Display Name` 또한 저장소 노드 이름이기도 합니다. 만약 `Name` 이 올바른 저장소 노드 이름이 아니므로 수정됩니다.

* **표시 이름**

   (*선택 사항입니다*) UI에서 배지에 대해 표시할 이름입니다. 기본값은 `Name`.

* **설명**

   (*선택 사항입니다*) 배지에 대한 설명입니다.

## 추가 정보 {#additional-information}

점수 및 배지 규칙 설정에 대한 자세한 내용은 [점수 및 배지](/help/communities/implementing-scoring.md).

구성원에 대한 배지를 관리하는 방법은 [구성원 콘솔](/help/communities/members.md).
