---
title: Badges Console
seo-title: Badges Console
description: 커뮤니티 배지 콘솔에서는 회원이 획득(수상)할 때 또는 커뮤니티(할당됨)에서 특정 역할을 수행할 때 표시할 수 있는 사용자 지정 배지를 추가할 수 있습니다
seo-description: 커뮤니티 배지 콘솔에서는 회원이 획득(수상)할 때 또는 커뮤니티(할당됨)에서 특정 역할을 수행할 때 표시할 수 있는 사용자 지정 배지를 추가할 수 있습니다
uuid: 7103b133-ef3f-47d6-a2dc-4e6ff92e8fed
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 135b3077-5343-4888-858d-de5e9b1d4b04
docset: aem65
translation-type: tm+mt
source-git-commit: fb7d2a3cebda86fa4d91d2ea89ae459fa4b86fa0
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 4%

---


# Badges Console {#badges-console}

## 배지 정보 {#about-badges}

커뮤니티 배지 콘솔에서는 획득(수상) 시 또는 커뮤니티(지정)에서 특정 역할을 수행할 때 멤버에 대해 표시될 수 있는 사용자 지정 배지를 추가할 수 있습니다.

### 배지 가시성 {#badge-visibility}

현재, 회원이 번 또는 할당되는 커뮤니티 멤버가 다음 위치에 이름과 아바타와 함께 표시됩니다.

* 프로파일
* [포럼](/help/communities/forum.md)
* [QnA](/help/communities/working-with-qna.md)
* [리더보드](/help/communities/enabling-leaderboard.md)
* [관념화](/help/communities/ideation-feature.md)

작성 환경에서 Badges 콘솔에 도달하려면

* 글로벌 탐색에서 도구 > **[!UICONTROL 커뮤니티 > 배지로 이동합니다]**

이 콘솔에는 현재 사용할 수 있는 배지와 새 배지를 추가할 수 있는 배지가 표시됩니다.

![chlimage_1-123](assets/chlimage_1-123.png)

## 배지 만들기 {#create-badge}

배지는 26-32픽셀 크기의 적절하게 작은 이미지(72dpi)를 업로드하고 이름을 제공하여 만듭니다. 배지 이미지는 의 보관소에 저장되며 게시 환경 `/libs/settings/community/badging/images` 에 자동으로 복제됩니다.

게시 환경이 게시자의 팜인 경우 [사용자 동기화를 구성해야 합니다](/help/communities/sync.md).

![chlimage_1-124](assets/chlimage_1-124.png)

* **이미지 업로드**

   (*필수*) JPEG 또는 PNG 포맷의 32 x 32픽셀 권장 크기의 배지 이미지입니다.

* **이름**

   (*필수*) 배지 이름입니다. 저장소 노드 이름 `Display Name` 뿐만 아니라 기본값입니다. 저장소 노드 이름 `Name` 이 올바르지 않으면 수정됩니다.

* **표시 이름**

   (*선택*&#x200B;사항) UI에서 배지에 대해 표시할 이름입니다. 기본값은 에 대해 입력한 변경되지 않은 텍스트입니다 `Name`.

* **설명**

   (*선택*&#x200B;사항) 배지에 대한 설명입니다.

## 추가 정보 {#additional-information}

점수 지정 및 배지 규칙 설정에 대한 자세한 내용은 [점수 지정 및 배지를 참조하십시오](/help/communities/implementing-scoring.md).

구성원에 대한 배지를 관리하려면 [구성원 콘솔을 참조하십시오](/help/communities/members.md).
