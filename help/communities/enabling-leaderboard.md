---
title: 리더보드 기능
seo-title: Leaderboard Feature
description: 페이지에 리더보드 구성 요소 추가
seo-description: Adding a Leaderboard component to a page
uuid: c4633919-75d3-4bc7-830c-ef9c28cc1cba
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 9045ce2e-a06d-4da5-9b83-56dd823007bb
docset: aem65
exl-id: 8b4d56d9-ba73-4eda-9773-3daaa9237abe
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 10%

---

# 리더보드 기능 {#leaderboard-feature}

## 소개 {#introduction}

다음 `Leaderboard` 구성 요소는 획득한 점수(기본 점수) 또는 전문 지식(고급 점수)에 따라 구성원의 등급을 매겨 커뮤니티 내에서 구성원이 어떻게 상호 작용하고 있는지에 대한 감을 얻을 수 있는 기능을 제공합니다.

페이지에 리더보드 구성 요소를 포함하기 전에 을 구성해야 합니다. [커뮤니티 점수 및 배지](/help/communities/implementing-scoring.md).

설명서의 이 섹션에서는 다음 사항에 대해 설명합니다.

* 추가 `Leaderboard` 구성 요소를 a로 [커뮤니티 사이트](/help/communities/overview.md#community-sites).
* 에 대한 구성 설정 `Leaderboard` 구성 요소.

### 페이지에 순위표 추가 {#adding-a-leaderboard-to-a-page}

을(를) 추가하려면 `Leaderboard` 구성 요소를 페이지에 추가하려면 작성자 모드에서 구성 요소를 찾습니다.

* `Communities / Leaderboard`

을 페이지에 끌어서 놓습니다.

필요한 정보는 다음을 참조하십시오. [커뮤니티 구성 요소 기본 사항](/help/communities/basics.md).

커뮤니티 사이트의 페이지에 처음 배치하면 구성 요소가 다음과 같이 표시됩니다.

![리더보드](assets/leaderboard.png)

### 리더보드 구성 {#configuring-leaderboard}

배치된 을(를) 선택합니다 `Leaderboard` 에 액세스하고 선택할 구성 요소 `Configure` 편집 대화 상자를 여는 아이콘.

![새로 구성](assets/configure-new.png)

![순위표 구성](assets/configure-leaderboard.png)

#### 설정 탭 {#settings-tab}

아래 **[!UICONTROL 설정]** 탭에서는 멤버와 관련된 정보가 표시될 내용을 지정합니다.

* **표시 이름**

   배지 및 점수를 표시하기 위해 선택한 규칙을 반영하며 보드에 대해 표시할 수사적 이름입니다.
기본값은 입니다 `Leaderboard`: 아무 것도 입력하지 않은 경우

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

아래 **규칙** 탭, 커뮤니티 사이트, 점수 및 배지 규칙

* **규칙 위치**

   (필수) 채점/배지 규칙이 구성되는 위치입니다.

* **점수 지정 규칙**

   (필수) 표시할 점수를 생성하는 특정 규칙입니다.

* **배지 규칙**

   (필수) 표시할 배지를 생성하는 특정 규칙입니다.

* **표시 제한**

   페이지당 표시할 멤버 수입니다. 기본값은 10입니다.

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
   * 점수 지정 규칙 = `/libs/settings/community/scoring/rules/forums-scoring`
   * 배지 규칙 = `/libs/settings/community/badging/rules//reference-badging`
   * 표시 제한 = `10`

![참가자-리더보드](assets/participants-leaderboard.png)

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
   * 점수 지정 규칙 = `/libs/settings/community/scoring/rules/adv-forums-scoring`
   * 배지 규칙 = `/libs/settings/community/badging/rules/adv-forums-badging`
   * 표시 제한 = `10`

![전문가 리더보드](assets/experts-leaderboard.png)

### 추가 정보 {#additional-information}

자세한 내용은 [리더보드 기본 사항](/help/communities/leaderboard.md) 개발자용 페이지입니다.

규칙 만들기에 대한 지침은 [커뮤니티 점수 및 배지](/help/communities/implementing-scoring.md) 관리자용 페이지입니다.
