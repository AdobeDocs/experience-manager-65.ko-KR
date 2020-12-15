---
title: 리드 보드 기능
seo-title: 리드 보드 기능
description: 페이지에 리드 보드 구성 요소 추가
seo-description: 페이지에 리드 보드 구성 요소 추가
uuid: c4633919-75d3-4bc7-830c-ef9c28cc1cba
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 9045ce2e-a06d-4da5-9b83-56dd823007bb
docset: aem65
translation-type: tm+mt
source-git-commit: a8b1ad0fcd2ca9c7fe3117dd8bd161da82d13e8a
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 9%

---


# 리드 보드 기능 {#leaderboard-feature}

## 소개 {#introduction}

`Leaderboard` 구성 요소는 획득한 점수(기본 점수) 또는 전문성(고급 점수)에 따라 회원이 커뮤니티 내에서 상호 작용하는 방식을 파악하는 기능을 제공합니다.

페이지에 리더보드 구성 요소를 포함하기 전에 [커뮤니티 점수 및 배지](/help/communities/implementing-scoring.md)를 구성해야 합니다.

설명서의 이 섹션에서는 다음 사항에 대해 설명합니다.

* `Leaderboard` 구성 요소를 [커뮤니티 사이트](/help/communities/overview.md#community-sites)에 추가합니다.
* `Leaderboard` 구성 요소에 대한 구성 설정입니다.

### {#adding-a-leaderboard-to-a-page} 페이지에 리드 보드 추가

작성 모드에서 페이지에 `Leaderboard` 구성 요소를 추가하려면 구성 요소를 찾습니다

* `Communities / Leaderboard`

페이지로 드래그하여 배치합니다.

필요한 정보를 보려면 [커뮤니티 구성 요소 기본 사항](/help/communities/basics.md)을 방문하십시오.

커뮤니티 사이트의 페이지에 처음 배치하면 구성 요소가 표시되는 방식입니다.

![리더보드](assets/leaderboard.png)

### 리드 보드 구성 {#configuring-leaderboard}

액세스할 배치된 `Leaderboard` 구성 요소를 선택하고 편집 대화 상자를 여는 `Configure` 아이콘을 선택합니다.

![configure-new](assets/configure-new.png)

![configure-leaderboard](assets/configure-leaderboard.png)

#### 설정 탭 {#settings-tab}

**[!UICONTROL 설정]** 탭에서 구성원과 관련된 정보가 표시되는 것을 지정합니다.

* **표시 이름**

   배지 및 점수를 표시하기 위해 선택한 규칙을 반영하여 보드에 대해 표시할 설명형 이름입니다.
입력하지 않은 경우 기본값은 `Leaderboard`입니다.

* **배지**

   이 확인란을 선택하면 배지 아이콘에 대한 열이 리더보드에 포함됩니다.
기본값은 선택되어 있지 않습니다.

* **배지 이름**

   이 확인란을 선택하면 배지 이름의 열이 리더보드에 포함됩니다.
기본값은 선택되어 있지 않습니다.

* **아바타 사용**

   이 확인란을 선택하면 회원의 아바타 이미지가 구성원 프로필에 대한 이름 링크 옆에 있는 리더보드에 포함됩니다.
기본값은 선택되어 있지 않습니다.

#### 규칙 탭 {#rules-tab}

**규칙** 탭 아래 커뮤니티 사이트, 점수 및 배지 규칙

* **규칙 위치**

   (필수) 점수 지정/배지 규칙이 구성된 위치.

* **점수 지정 규칙**

   (필수) 표시할 점수를 생성하는 특정 규칙.

* **배지 규칙**

   (필수) 표시할 배지를 생성하는 특정 규칙.

* **표시 제한**

   페이지당 표시할 구성원 수입니다.기본값은 10입니다.

### 예:참가자 리더보드 {#example-participants-leaderboard}

이 리더보드 보고서는 기본 점수 지정 규칙을 적용한 결과를 보고합니다.

리더보드 구성 요소 구성:

* 설정 탭:

   * 표시 이름 = `Participation Board`
   * `checked`:

      * 배지
      * 배지 이름
      * 아바타 사용

* 규칙 탭:

   * 규칙 위치 = `/content/sites/<site name>/jcr:content`
   * 점수 지정 규칙 = `/libs/settings/community/scoring/rules/forums-scoring`
   * 배지 규칙 = `/libs/settings/community/badging/rules//reference-badging`
   * 표시 제한 = `10`

![참가자 리더보드](assets/participants-leaderboard.png)

### 예:전문가 리더보드 {#example-experts-leaderboard}

이 리더보드는 고급 점수 지정 규칙을 적용하여 결과를 보고합니다.

리더보드 구성 요소 구성:

* 설정 탭:

   * 표시 이름 = `Expertise Board`
   * `checked`:

      * 배지
      * 아바타 사용

* 규칙 탭:

   * 규칙 위치 = `/content/sites/<site name>/jcr:content`
   * 점수 지정 규칙 = `/libs/settings/community/scoring/rules/adv-forums-scoring`
   * 배지 규칙 = `/libs/settings/community/badging/rules/adv-forums-badging`
   * 표시 제한 = `10`

![전문가 리더보드](assets/experts-leaderboard.png)

### 추가 정보 {#additional-information}

개발자를 위한 [Leaderboard Essentials](/help/communities/leaderboard.md) 페이지에 자세한 내용이 표시될 수 있습니다.

규칙 만들기에 대한 지침은 관리자를 위한 [커뮤니티 점수 지정 및 배지](/help/communities/implementing-scoring.md) 페이지에 제공됩니다.
