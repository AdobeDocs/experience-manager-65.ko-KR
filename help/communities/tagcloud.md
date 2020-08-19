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

구성 요소는 컨텐츠를 게시할 때 커뮤니티 구성원이 적용한 태그를 강조 표시합니다. `Social Tag Cloud` 트렌드 토픽을 식별하고 사이트 방문자가 태그 있는 컨텐츠를 신속하게 찾을 수 있도록 하는 방법입니다.

현재 트렌드를 식별하는 또 다른 방법은 [활동 트렌드를 참조하십시오](trends.md).

이 페이지에서는 구성 요소 대화 상자 `Social Tag Cloud` 설정을 문서화하고 사용자 경험에 대해 설명합니다.

개발자를 위한 자세한 내용은 [Tag Essentials를 참조하십시오](tag.md).

태그 작성 및 관리 방법과 컨텐츠 태그가 적용되는 항목에 대한 내용은 [태그 관리](../../help/sites-administering/tags.md)를 참조하십시오.

## 소셜 태그 클라우드 추가 {#adding-a-social-tag-cloud}

작성 모드에서 페이지에 `Social Tag Cloud` `Communities / Social Tag Cloud` 구성 요소를 추가하려면 구성 요소 브라우저를 사용하여 구성 요소를 찾아 태그 클라우드가 표시되어야 하는 페이지에 드래그합니다.

필요한 정보를 보려면 커뮤니티 구성 요소 [기본 사항을 방문하십시오](basics.md).

필요한 [클라이언트측 라이브러리가](tag.md#essentials-for-client-side) 포함되어 있으면 구성 요소가 표시되는 `Social Tag Cloud` 방식입니다.

![social-tag](assets/social-tag.png)

## 소셜 태그 클라우드 구성 {#configuring-social-tag-cloud}

액세스할 배치된 `Social Tag Cloud` 구성 요소를 선택하고 편집 대화 상자를 여는 `Configure` 아이콘을 선택합니다.

![configure](assets/configure-new.png)

소셜 **[!UICONTROL 태그 클라우드]** 탭 아래에서 표시할 태그를 지정하고, 태그가 활성 링크인 경우 검색 결과를 위한 페이지의 위치를 지정합니다.

![social-tag-cloud](assets/social-tag-cloud.png)

* **[!UICONTROL 표시할 소셜 태그]**&#x200B;표시할 UGC 태그를 식별합니다. 풀다운 옵션은 다음과 같습니다.

   * `From page and child pages`
   * `All tags`

   기본값은 `From page and child pages`입니다. 여기서 &quot;page&quot;는 아래의 **페이지** 설정을 나타냅니다.

* **[!UICONTROL 페이지]**

   (그렇지 않은 경우 `All tags)` 필수) 페이지에 대한 UGC 경로입니다. 기본값은 현재 페이지(비워 둔 경우)입니다.

* **[!UICONTROL 태그에 링크 없음]**

   이 확인란을 선택하면 태그가 일반 텍스트로 태그 클라우드에 표시됩니다. 이 확인란을 선택하지 않으면 태그가 적용되는 모든 컨텐츠를 검색하는 활성 링크로 태그가 표시됩니다. 기본값은 선택 취소되어 있으며 **[!UICONTROL 검색 결과 경로를]** 설정해야 합니다.

* **[!UICONTROL 검색 결과 경로]**

   페이지 `Search Result` 설정에서 지정한 UGC 경로를 포함하는 UGC를 참조하도록 구성된 구성 요소 **가 배치된 페이지의 경로입니다** .

## 소셜 태그 클라우드 표시 변경 {#change-display-of-social-tag-cloud}

소셜 **태그 클라우드**&#x200B;표시를 편집하려면 [디자인 모드를](../../help/sites-authoring/default-components-designmode.md) 입력하고 배치된 구성 요소를 두 번 클릭하여 추가 탭이 있는 대화 `Social Tag Cloud` 상자를 엽니다.

소셜 **[!UICONTROL 태그 클라우드(디자인)]** 탭을 사용하여 태그를 표시하는 방법을 지정합니다. 태그는 단순한 태그, 기본 네임스페이스의 단일 단어 또는 계층 분류법일 수 있습니다.

![social-tag-cloud-design](assets/social-tag-cloud-design.png)

* **[!UICONTROL 전체 제목 경로 표시]**

   이 확인란을 선택하면 적용된 각 태그에 대한 상위 태그 및 네임스페이스의 제목이 표시됩니다.

   예:

   * 선택됨: `Geometrixx Media: Gadgets / Cars`
   * 선택되지 않음: `Cars`

   단순 태그에는 아무런 차이가 없습니다.

   기본값은 선택 취소입니다.

* **[!UICONTROL 리프 태그만 표시]**

   이 확인란을 선택하면 다른 태그가 없는 적용된 태그만 표시됩니다.

   예를 들어 다음 TagID가 주어집니다.

   `Geometrixx Media: Gadgets / Cars`

   적용할 수 있는 태그는 다음과 같습니다.

   `Geometrixx Media (the namespace)`, `Gadgets`, 및 `Cars`

   * 선택:적용된 경우에만 `Cars` 표시됩니다.
   * 선택 취소: `Geometrixx Media` 및 `Gadgets`는 `Cars` 적용된 경우 표시됩니다.

   단순 태그는 리프 태그입니다.

   기본값은 선택 취소입니다.

* **[!UICONTROL 링크 템플릿]**

   링크를 구성 요소 편집 대화 상자를 통해 활성화하면 기본 템플릿이 아닌 템플릿이 태그 클라우드에 링크를 표시하는 데 사용됩니다.

* **[!UICONTROL 모든 태그에 동일한 크기 사용]**

   이 확인란을 선택하면 태그 클라우드의 모든 단어가 동일하게 스타일이 지정됩니다. 이 확인란을 선택하지 않으면 단어는 용어에 따라 다르게 스타일이 지정됩니다. 기본값은 선택 취소입니다.

## 추가 정보 {#additional-information}

개발자를 위한 [Tag Essentials](tag.md) 페이지에 자세한 내용이 나와 있습니다.

태그 [만들기 및 관리에 대한 자세한 내용은 UGC(사용자 생성 컨텐츠](tag-ugc.md) 태그 지정)를 참조하십시오.
