---
title: 소셜 태그 클라우드 사용
seo-title: 소셜 태그 클라우드 사용
description: 페이지에 소셜 태그 클라우드 구성 요소 추가
seo-description: 페이지에 소셜 태그 클라우드 구성 요소 추가
uuid: 8c400030-976c-457a-bb5f-e473909647a9
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 23a5a65e-774d-4789-9659-09e8be0c2bcd
translation-type: tm+mt
source-git-commit: 2fcd87cd1def7fc265ba40c83b50db86618f3b70
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 8%

---


# 소셜 태그 클라우드 사용 {#using-social-tag-cloud}

## 소개 {#introduction}

`Social Tag Cloud` 구성 요소는 컨텐츠를 게시할 때 커뮤니티 구성원이 적용한 태그를 강조 표시합니다. 트렌드 토픽을 식별하고 사이트 방문자가 태그 있는 컨텐츠를 빠르게 찾을 수 있도록 하는 방법입니다.

현재 트렌드를 식별하는 다른 방법은 [활동 트렌드](trends.md)를 참조하십시오.

이 페이지에서는 `Social Tag Cloud` 구성 요소 대화 상자 설정을 문서화하고 사용자 경험에 대해 설명합니다.

개발자를 위한 자세한 내용은 [Tag Essentials](tag.md)를 참조하십시오.

태그 작성 및 관리 방법과 컨텐츠 태그가 적용되는 항목에 대한 내용은 [태그 관리](../../help/sites-administering/tags.md)를 참조하십시오.

## 소셜 태그 클라우드 추가 {#adding-a-social-tag-cloud}

작성 모드에서 페이지에 `Social Tag Cloud` 구성 요소를 추가하려면 구성 요소 브라우저를 사용하여 `Communities / Social Tag Cloud`을 찾아 태그 클라우드가 표시되어야 하는 페이지에 드래그합니다.

필요한 정보를 보려면 [커뮤니티 구성 요소 기본 사항](basics.md)을 방문하십시오.

[필수 클라이언트측 라이브러리](tag.md#essentials-for-client-side)가 포함될 때 `Social Tag Cloud` 구성 요소가 표시되는 방식입니다.

![social-tag](assets/social-tag.png)

## 소셜 태그 클라우드 구성 {#configuring-social-tag-cloud}

액세스할 배치된 `Social Tag Cloud` 구성 요소를 선택하고 편집 대화 상자를 여는 `Configure` 아이콘을 선택합니다.

![configure](assets/configure-new.png)

**[!UICONTROL 소셜 태그 클라우드]** 탭에서 표시할 태그를 지정하고, 태그가 활성 링크인 경우 검색 결과를 위한 페이지의 위치를 지정합니다.

![social-tag-cloud](assets/social-tag-cloud.png)

* **[!UICONTROL 표시할 소셜]**
태그표시할 UGC 태그를 식별합니다. 풀다운 옵션은 다음과 같습니다.

   * `From page and child pages`
   * `All tags`

   기본값은 `From page and child pages`입니다. 여기서 &quot;page&quot;는 아래의 **페이지** 설정을 참조합니다.

* **[!UICONTROL 페이지]**

   (필수 사항: `All tags)`) 페이지에 대한 UGC 경로입니다. 기본값은 현재 페이지(비워 둔 경우)입니다.

* **[!UICONTROL 태그에 링크 없음]**

   선택하는 경우 태그가 태그 클라우드에 일반 텍스트로 표시됩니다. 이 옵션을 선택하지 않으면 태그가 적용되는 모든 컨텐츠를 검색하는 활성 링크로 태그가 표시됩니다. 기본값은 선택 취소되어 있으므로 **[!UICONTROL 검색 결과 경로]**&#x200B;를 설정해야 합니다.

* **[!UICONTROL 검색 결과 경로]**

   **페이지** 설정에서 지정한 UGC 경로를 포함하는 UGC를 참조하도록 구성된 `Search Result` 구성 요소가 배치된 페이지의 경로입니다.

## 소셜 태그 클라우드 표시 변경 {#change-display-of-social-tag-cloud}

**소셜 태그 클라우드**&#x200B;의 표시를 편집하려면 [디자인 모드](../../help/sites-authoring/default-components-designmode.md)를 입력하고 배치된 `Social Tag Cloud` 구성 요소를 두 번 클릭하여 추가 탭이 있는 대화 상자를 엽니다.

**[!UICONTROL 소셜 태그 클라우드(디자인)]** 탭을 사용하여 태그가 표시되는 방식을 지정합니다. 태그는 단순한 태그, 기본 네임스페이스의 단일 단어 또는 계층적 분류법일 수 있습니다.

![social-tag-cloud-design](assets/social-tag-cloud-design.png)

* **[!UICONTROL 전체 제목 경로 표시]**

   이 확인란을 선택하면 적용된 각 태그에 대한 상위 태그 및 네임스페이스의 제목이 표시됩니다.

   예:

   * 선택됨: `Geometrixx Media: Gadgets / Cars`
   * 선택되지 않음: `Cars`

   단순 태그에는 아무런 차이가 없습니다.

   기본값은 선택되어 있지 않습니다.

* **[!UICONTROL 리프 태그만 표시]**

   이 확인란을 선택하면 다른 태그가 없는 적용된 태그만 표시됩니다.

   예를 들어 다음 TagID가 주어집니다.

   `Geometrixx Media: Gadgets / Cars`

   적용할 수 있는 태그는 다음과 같습니다.

   `Geometrixx Media (the namespace)`, `Gadgets`, 및 `Cars`

   * 확인:적용된 경우 `Cars`만 표시됩니다.
   * 선택 취소:적용된 경우 `Geometrixx Media` 및 `Gadgets`과 `Cars`가 표시됩니다.

   단순 태그는 리프 태그입니다.

   기본값은 선택되어 있지 않습니다.

* **[!UICONTROL 링크 템플릿]**

   링크를 구성 요소 편집 대화 상자를 통해 활성화할 때 태그 클라우드에 링크를 표시하는 데 사용되는 기본 템플릿이 아닌 템플릿입니다.

* **[!UICONTROL 모든 태그에 동일한 크기 사용]**

   이 확인란을 선택하면 태그 클라우드의 모든 단어가 동일하게 스타일이 지정됩니다. 이 확인란을 선택하지 않으면 단어들의 용법에 따라 다르게 스타일이 지정됩니다. 기본값은 선택되어 있지 않습니다.

## 추가 정보 {#additional-information}

개발자를 위한 [Tag Essentials](tag.md) 페이지에 자세한 내용이 있을 수 있습니다.

태그 만들기 및 관리에 대한 자세한 내용은 [사용자 생성 컨텐트 태그 지정](tag-ugc.md)(UGC)을 참조하십시오.
