---
title: 리더보드 기능
description: 리더보드 구성 요소를 통해 획득한 점수 및 전문 지식을 기반으로 구성원의 등급을 매겨 커뮤니티 내에서 구성원이 상호 작용하는 방법을 확인할 수 있습니다.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 8b4d56d9-ba73-4eda-9773-3daaa9237abe
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 2%

---

# 리더보드 기능 {#leaderboard-feature}

## 소개 {#introduction}

`Leaderboard` 구성 요소를 사용하면 획득한 점수(기본 점수) 또는 전문 지식(고급 점수)에 따라 구성원의 순위를 매겨 커뮤니티 내에서 구성원이 어떻게 상호 작용하는지 파악할 수 있습니다.

페이지에 순위표 구성 요소를 포함하기 전에 [커뮤니티 점수 및 배지](/help/communities/implementing-scoring.md)를 구성해야 합니다.

설명서의 이 섹션에서는 다음 사항에 대해 설명합니다.

* [커뮤니티 사이트](/help/communities/overview.md#community-sites)에 `Leaderboard` 구성 요소를 추가하는 중입니다.
* `Leaderboard` 구성 요소에 대한 구성 설정입니다.

### 페이지에 순위표 추가 {#adding-a-leaderboard-to-a-page}

작성자 모드에서 페이지에 `Leaderboard` 구성 요소를 추가하려면 구성 요소를 찾습니다

* `Communities / Leaderboard`

그리고 페이지에 있는 제자리에 드래그합니다.

필요한 정보는 [커뮤니티 구성 요소 기본 사항](/help/communities/basics.md)을 참조하세요.

커뮤니티 사이트의 페이지에 처음 배치하면 구성 요소가 다음과 같이 표시됩니다.

![순위표](assets/leaderboard.png)

### 리더보드 구성 {#configuring-leaderboard}

배치된 `Leaderboard` 구성 요소를 선택하여 편집 대화 상자를 여는 `Configure` 아이콘에 액세스하고 선택합니다.

![새로 구성](assets/configure-new.png)

![configure-leaderboard](assets/configure-leaderboard.png)

#### 설정 탭 {#settings-tab}

**[!UICONTROL 설정]** 탭에서 표시되는 구성원 관련 정보를 지정합니다.

* **표시 이름**

  배지 및 점수를 표시하기 위해 선택한 규칙을 반영하며 보드에 대해 표시할 수사적 이름입니다.
아무 것도 입력하지 않은 경우 기본값은 `Leaderboard`입니다.

* **배지**

  선택하면 배지 아이콘에 대한 열이 순위표에 포함됩니다.
기본값은 선택 취소되어 있습니다.

* **배지 이름**

  선택하면 배지 이름에 대한 열이 순위표에 포함됩니다.
기본값은 선택 취소되어 있습니다.

* **아바타 사용**

  선택하면, 멤버의 아바타 이미지가 리더보드에 포함되고, 리더보드는 멤버 프로필에 연결된 이름 링크 옆에 포함됩니다.
기본값은 선택 취소되어 있습니다.

#### 규칙 탭 {#rules-tab}

**규칙** 탭에서 커뮤니티 사이트와 점수 및 배지 규칙

* **규칙 위치**

  (필수) 채점/배지 규칙이 구성되는 위치입니다.

* **채점 규칙**

  (필수) 표시할 점수를 생성하는 특정 규칙입니다.

* **배지 규칙**

  (필수) 표시할 배지를 생성하는 특정 규칙입니다.

* **표시 제한**

  페이지당 표시할 멤버 수. 기본값은 10입니다.

### 예: 참가자 순위표 {#example-participants-leaderboard}

이 리더보드는 기본 채점 규칙을 적용한 결과를 보고합니다.

리더보드 구성 요소 구성:

* 설정 탭:

   * 표시 이름 = `Participation Board`
   * `checked`:

      * 배지
      * 배지 이름
      * 아바타 사용

* 규칙 탭:

   * 규칙 위치 = `/content/sites/<site name>/jcr:content`
   * 채점 규칙 = `/libs/settings/community/scoring/rules/forums-scoring`
   * 배지 규칙 = `/libs/settings/community/badging/rules//reference-badging`
   * 표시 제한 = `10`

![참가자-순위표](assets/participants-leaderboard.png)

### 예: Experts 순위표 {#example-experts-leaderboard}

이 리더보드는 고급 채점 규칙을 적용한 결과를 보고합니다.

리더보드 구성 요소 구성:

* 설정 탭:

   * 표시 이름 = `Expertise Board`
   * `checked`:

      * 배지
      * 아바타 사용

* 규칙 탭:

   * 규칙 위치 = `/content/sites/<site name>/jcr:content`
   * 채점 규칙 = `/libs/settings/community/scoring/rules/adv-forums-scoring`
   * 배지 규칙 = `/libs/settings/community/badging/rules/adv-forums-badging`
   * 표시 제한 = `10`

![experts-leaderboard](assets/experts-leaderboard.png)

### 추가 정보 {#additional-information}

자세한 내용은 개발자를 위한 [순위표 기본 사항](/help/communities/leaderboard.md) 페이지에서 확인할 수 있습니다.

규칙 만들기에 대한 지침은 관리자를 위한 [커뮤니티 점수 및 배지](/help/communities/implementing-scoring.md) 페이지에서 제공됩니다.
