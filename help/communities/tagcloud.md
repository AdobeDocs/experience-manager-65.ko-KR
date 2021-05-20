---
title: Social Tag Cloud 사용
seo-title: Social Tag Cloud 사용
description: 페이지에 소셜 태그 클라우드 구성 요소 추가
seo-description: 페이지에 소셜 태그 클라우드 구성 요소 추가
uuid: 8c400030-976c-457a-bb5f-e473909647a9
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 23a5a65e-774d-4789-9659-09e8be0c2bcd
exl-id: 56af5362-78de-4308-8958-63a45e8573cc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 8%

---

# 소셜 태그 클라우드 사용 {#using-social-tag-cloud}

## 소개 {#introduction}

`Social Tag Cloud` 구성 요소는 컨텐츠를 게시할 때 커뮤니티 구성원이 적용한 태그를 강조 표시합니다. 트렌드 항목을 식별하고 사이트 방문자가 태그가 지정된 컨텐츠를 빠르게 찾을 수 있도록 하는 방법입니다.

현재 트렌드를 식별하는 다른 방법은 [활동 트렌드](trends.md)를 방문하십시오.

이 페이지에서는 `Social Tag Cloud` 구성 요소 대화 상자 설정에 대해 설명하고 사용자 경험을 설명합니다.

개발자를 위한 자세한 내용은 [태그 필수 요소인](tag.md)을 참조하십시오.

태그 작성 및 관리 방법과 컨텐츠 태그가 적용되는 항목에 대한 내용은 [태그 관리](../../help/sites-administering/tags.md)를 참조하십시오.

## 소셜 태그 클라우드 추가 {#adding-a-social-tag-cloud}

작성자 모드의 페이지에 `Social Tag Cloud` 구성 요소를 추가하려면 구성 요소 브라우저를 사용하여 `Communities / Social Tag Cloud` 을(를) 찾아 태그 클라우드가 나타나는 페이지에 드래그합니다.

필요한 정보를 보려면 [커뮤니티 구성 요소 기본 사항](basics.md)을 방문하십시오.

필요한 [클라이언트 측 라이브러리](tag.md#essentials-for-client-side)가 포함된 경우 이 방법으로 `Social Tag Cloud` 구성 요소가 표시됩니다.

![소셜 태그](assets/social-tag.png)

## 소셜 태그 클라우드 구성 {#configuring-social-tag-cloud}

액세스할 배치된 `Social Tag Cloud` 구성 요소를 선택하고 편집 대화 상자를 여는 `Configure` 아이콘을 선택합니다.

![구성](assets/configure-new.png)

**[!UICONTROL 소셜 태그 클라우드]** 탭에서 표시할 태그를 지정하고, 태그가 활성 링크인 경우 검색 결과를 위한 페이지의 위치를 지정합니다.

![social-tag-cloud](assets/social-tag-cloud.png)

* **[!UICONTROL 표시할 소셜]**
태그표시할 UGC 태그를 식별합니다. 풀다운 옵션은 다음과 같습니다.

   * `From page and child pages`
   * `All tags`

   기본값은 `From page and child pages`입니다. 여기서 &quot;page&quot;는 아래의 **Page** 설정을 참조합니다.

* **[!UICONTROL 페이지]**

   ( `All tags)` 이 아닐 경우 필수) 페이지에 대한 UGC 경로입니다. 기본값은 비워 두면 현재 페이지입니다.

* **[!UICONTROL 태그에 링크 없음]**

   이 옵션을 선택하면 태그가 태그 클라우드에 일반 텍스트로 표시됩니다. 선택 취소하면 해당 태그가 적용되는 모든 컨텐츠를 검색하는 활성 링크로 태그가 표시됩니다. 기본값이 선택 취소되어 있으므로 **[!UICONTROL 검색 결과 경로]**&#x200B;를 설정해야 합니다.

* **[!UICONTROL 검색 결과 경로]**

   `Search Result` 구성 요소가 배치된 페이지의 경로이며, **Page** 설정에 지정된 UGC 경로를 포함하는 UGC를 참조하도록 구성되었습니다.

## 소셜 태그 클라우드 표시 변경 {#change-display-of-social-tag-cloud}

**Social Tag Cloud** 표시를 편집하려면 [디자인 모드](../../help/sites-authoring/default-components-designmode.md)를 입력하고 배치된 `Social Tag Cloud` 구성 요소를 두 번 클릭하여 추가 탭이 있는 대화 상자를 엽니다.

**[!UICONTROL 소셜 태그 클라우드(디자인)]** 탭을 사용하여 태그를 표시하는 방법을 지정합니다. 태그는 간단한 태그, 기본 네임스페이스의 단일 단어 또는 계층적 분류법일 수 있습니다.

![social-tag-cloud-design](assets/social-tag-cloud-design.png)

* **[!UICONTROL 전체 제목 경로 표시]**

   이 확인란을 선택하면 적용된 각 태그의 상위 태그 및 네임스페이스의 제목이 표시됩니다.

   예:

   * 선택됨: `Geometrixx Media: Gadgets / Cars`
   * 선택되지 않음: `Cars`

   단순 태그에는 차이가 없습니다.

   기본값은 선택 취소되어 있습니다.

* **[!UICONTROL 리프 태그만 표시]**

   이 확인란을 선택하면 다른 태그가 없는 적용된 태그만 표시됩니다.

   예를 들어, 다음과 같은 TagID가 주어집니다.

   `Geometrixx Media: Gadgets / Cars`

   적용할 수 있는 태그는 다음과 같습니다.

   `Geometrixx Media (the namespace)`, `Gadgets`, 및 `Cars`

   * 확인됨:적용되는 경우 `Cars`만 표시됩니다.
   * 선택 취소:적용되는 경우 `Geometrixx Media` 및 `Gadgets`과 `Cars`가 표시됩니다.

   간단한 태그는 리프 태그입니다.

   기본값은 선택 취소되어 있습니다.

* **[!UICONTROL 링크 템플릿]**

   구성 요소 편집 대화 상자를 통해 링크가 활성화될 때 태그 클라우드에 링크를 표시하는 데 사용되는 기본 이외의 템플릿입니다.

* **[!UICONTROL 모든 태그에 동일한 크기 사용]**

   이 확인란을 선택하면 태그 클라우드의 모든 단어가 동일하게 스타일이 지정됩니다. 선택 취소하면 단어들이 사용하는 방식에 따라 다르게 지정됩니다. 기본값은 선택 취소되어 있습니다.

## 추가 정보 {#additional-information}

개발자를 위한 [태그 필수 요소용](tag.md) 페이지에서 자세한 정보를 찾을 수 있습니다.

태그 만들기 및 관리에 대한 자세한 내용은 [사용자 생성 컨텐츠 태깅](tag-ugc.md) (UGC)을 참조하십시오.
