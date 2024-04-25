---
title: 소셜 태그 클라우드 사용
description: 로그인한 커뮤니티 구성원이 트렌드 주제를 빠르게 식별하고 태그가 지정된 콘텐츠를 찾을 수 있도록 페이지에 Social Tag Cloud 구성 요소를 추가하는 방법을 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 56af5362-78de-4308-8958-63a45e8573cc
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 5%

---

# 소셜 태그 클라우드 사용 {#using-social-tag-cloud}

## 소개 {#introduction}

다음 `Social Tag Cloud` 구성 요소는 콘텐츠를 게시할 때 커뮤니티 구성원이 적용한 태그를 강조 표시합니다. 트렌드 주제를 식별하고 사이트 방문자가 태그가 지정된 콘텐츠를 빠르게 찾을 수 있도록 하는 수단입니다.

현재 트렌드를 식별하는 다른 방법은 다음을 참조하십시오. [활동 트렌드](trends.md).

이 페이지에는 다음 문서가 있습니다. `Social Tag Cloud` 구성 요소 대화 상자 설정 및 사용자 경험에 대해 설명합니다.

개발자를 위한 자세한 내용은 [태그 기본 사항](tag.md).

태그 작성 및 관리 방법과 콘텐츠 태그가 적용되는 항목에 대한 내용은 [태그 관리](../../help/sites-administering/tags.md)를 참조하십시오.

## 소셜 태그 클라우드 추가 {#adding-a-social-tag-cloud}

을(를) 추가하려면 `Social Tag Cloud` 구성 요소를 페이지에 추가하려면 작성자 모드에서 구성 요소 브라우저를 사용하여 `Communities / Social Tag Cloud` 및 를 태그 클라우드가 표시되어야 하는 페이지에 있는 위치로 드래그합니다.

필요한 정보는 다음을 참조하십시오. [커뮤니티 구성 요소 기본 사항](basics.md).

다음의 경우 [필수 클라이언트측 라이브러리](tag.md#essentials-for-client-side) 포함됩니다. 이렇게 하면 `Social Tag Cloud` 구성 요소가 표시됩니다.

![소셜 태그](assets/social-tag.png)

## 소셜 태그 클라우드 구성 {#configuring-social-tag-cloud}

배치된 을(를) 선택합니다 `Social Tag Cloud` 에 액세스하고 선택할 수 있는 구성 요소 `Configure` 편집 대화 상자를 여는 아이콘.

![구성](assets/configure-new.png)

아래 **[!UICONTROL 소셜 태그 클라우드]** 탭에서 표시할 태그를 지정하고, 태그가 활성 링크인 경우 검색 결과를 위한 페이지 위치를 지정합니다.

![social-tag-cloud](assets/social-tag-cloud.png)

* **[!UICONTROL 표시할 소셜 태그]**
표시할 UGC 태그를 식별합니다. 풀다운 옵션은 다음과 같습니다.

   * `From page and child pages`
   * `All tags`

  기본값은 입니다 `From page and child pages`, 여기서 &quot;페이지&quot;는 **페이지** 을(를) 아래에 설정합니다.

* **[!UICONTROL 페이지]**

  (그렇지 않은 경우 필수) `All tags)` 페이지의 UGC 경로. 기본값은 비워 두면 현재 페이지입니다.

* **[!UICONTROL 태그에 링크 없음]**

  선택하면 태그가 태그 클라우드에 일반 텍스트로 표시됩니다. 선택하지 않으면 태그는 해당 태그가 적용되는 모든 콘텐츠를 검색하는 활성 링크로 표시됩니다. 기본값은 선택 취소되어 있으며 **[!UICONTROL 검색 결과 경로]** 설정할 수 있습니다.

* **[!UICONTROL 검색 결과 경로]**

  가 있는 페이지의 경로 `Search Result` 구성 요소가 배치되었으며, 이 구성 요소는 **페이지** 설정.

## 소셜 태그 클라우드의 표시 변경 {#change-display-of-social-tag-cloud}

디스플레이 편집하기 **소셜 태그 클라우드**, 입력 [디자인 모드](../../help/sites-authoring/default-components-designmode.md) 배치된 을 두 번 클릭합니다. `Social Tag Cloud` 추가 탭이 있는 대화 상자를 여는 구성 요소.

사용 **[!UICONTROL 소셜 태그 클라우드(디자인)]** 탭에서 태그 표시 방법을 지정합니다. 태그는 단순 태그, 기본 네임스페이스의 단일 단어 또는 계층 분류법일 수 있습니다.

![social-tag-cloud-design](assets/social-tag-cloud-design.png)

* **[!UICONTROL 전체 제목 경로 표시]**

  선택하면 상위 태그의 제목과 적용된 각 태그의 네임스페이스가 표시됩니다.

  예:

   * 선택함: `Geometrixx Media: Gadgets / Cars`
   * 선택 취소됨: `Cars`

  단순 태그는 차이가 없습니다.

  기본값은 선택 취소되어 있습니다.

* **[!UICONTROL 리프 태그만 표시]**

  선택하면 다른 태그가 포함되지 않은 적용된 태그만 표시됩니다.

  예를 들어 의 TagID가 지정된 경우:

  `Geometrixx Media: Gadgets / Cars`

  세 가지 태그를 적용할 수 있습니다.

  `Geometrixx Media (the namespace)`, `Gadgets` 및 `Cars`

   * 선택됨: 만 `Cars` 적용되는 경우 표시됩니다.
   * 선택 취소됨: `Geometrixx Media`, `Gadgets`, 및 `Cars` 적용되는 경우 표시됩니다.

  단순 태그는 리프 태그입니다.

  기본값은 선택 취소되어 있습니다.

* **[!UICONTROL 링크 템플릿]**

  구성 요소 편집 대화 상자를 통해 링크를 활성화하면 태그 클라우드에서 링크를 표시하는 데 사용되는 템플릿(기본값 제외)입니다.

* **[!UICONTROL 모든 태그에 동일한 크기 사용]**

  선택하면 태그 클라우드의 모든 단어 스타일이 동일합니다. 선택하지 않으면 단어 용법에 따라 다른 스타일이 지정됩니다. 기본값은 선택 취소되어 있습니다.

## 추가 정보 {#additional-information}

자세한 내용은 [태그 기본 사항](tag.md) 개발자용 페이지입니다.

다음을 참조하십시오 [사용자 생성 컨텐츠 태깅](tag-ugc.md) (UGC) 를 참조하십시오.
