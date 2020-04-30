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
source-git-commit: 77d00c1d6e94b257aa0533ca88b5f9a12dba0054

---


# 소셜 태그 클라우드 사용 {#using-social-tag-cloud}

## 소개 {#introduction}

이 `Social Tag Cloud` 구성 요소는 컨텐츠를 게시할 때 커뮤니티 구성원이 적용한 태그를 강조 표시합니다. 이것은 트렌드 토픽을 식별하고 사이트 방문자가 태그 있는 컨텐츠를 신속하게 찾을 수 있도록 하는 수단입니다.

현재 트렌드를 식별하는 또 다른 방법을 보려면 활동 트렌드를 [참조하십시오](trends.md).

이 페이지에서는 구성 요소 대화 상자 설정을 문서화하고 사용자 경험에 대해 설명합니다. `Social Tag Cloud`

개발자를 위한 자세한 내용은 Tag Essentials [를 참조하십시오](tag.md).

See [Administering Tags](../../help/sites-administering/tags.md) for information about creating and managing tags, as well as to which content tags have been applied.

## 소셜 태그 클라우드 추가 {#adding-a-social-tag-cloud}

작성 모드에서 구성 요소를 페이지에 추가하려면 구성 요소 브라우저를 사용하여 태그 클라우드가 표시되어야 하는 페이지에서 구성 요소를 찾아 `Social Tag Cloud` `Communities / Social Tag Cloud` 제자리에 드래그합니다.

필요한 정보를 보려면 커뮤니티 구성 [요소 기본 사항을 참조하십시오](basics.md).

필요한 [클라이언트측 라이브러리가](tag.md#essentials-for-client-side) `Social Tag Cloud` 포함되어 있으면 구성 요소가 표시되는 방식입니다.

![chlimage_1-303](assets/chlimage_1-303.png)

## 소셜 태그 클라우드 구성 {#configuring-social-tag-cloud}

액세스할 배치된 `Social Tag Cloud` 구성 요소를 선택하고 편집 대화 상자를 여는 `Configure` 아이콘을 선택합니다.

![chlimage_1-304](assets/chlimage_1-304.png)

소셜 **[!UICONTROL 태그 클라우드]** 탭에서 표시할 태그를 지정하고, 태그가 활성 링크인 경우 검색 결과를 위한 페이지 위치를 지정합니다.

![chlimage_1-305](assets/chlimage_1-305.png)

* **[!UICONTROL 표시할 소셜]**&#x200B;태그표시할 UGC 태그를 식별합니다. 풀다운 옵션은 다음과 같습니다.

   * `From page and child pages`
   * `All tags`
   기본값은 `From page and child pages`입니다. 여기서 &quot;page&quot;는 **아래의 페이지** 설정을 나타냅니다.

* **[!UICONTROL 페이지]**

   (그렇지 않은 경우 `All tags)` 필수) 페이지에 대한 UGC 경로입니다. 기본값은 현재 페이지를 비워 두면 됩니다.

* **[!UICONTROL 태그에 링크 없음]**

   이 확인란을 선택하면 태그가 일반 텍스트로 태그 클라우드에 표시됩니다. 이 옵션을 선택하지 않으면 태그가 적용되는 모든 컨텐츠를 검색하는 활성 링크로 태그가 표시됩니다. 기본값은 선택 취소되어 있으며 검색 **[!UICONTROL 결과 경로를]** 설정해야 합니다.

* **[!UICONTROL 검색 결과 경로]**

   페이지 설정에서 지정한 UGC 경로를 포함하는 UGC를 참조하도록 구성된 `Search Result` 구성 요소가 배치된 페이지의 **경로입니다** .

## 소셜 태그 클라우드 표시 변경 {#change-display-of-social-tag-cloud}

소셜 태그 클라우드의 표시를 편집하려면 **디자인**&#x200B;모드를 [입력하고](../../help/sites-authoring/default-components-designmode.md) 가져온 `Social Tag Cloud` 구성 요소를 두 번 클릭하여 추가 탭이 있는 대화 상자를 엽니다.

소셜 **[!UICONTROL 태그 클라우드(디자인)]** 탭을 사용하여 태그를 표시하는 방법을 지정합니다. 태그는 단순 태그, 기본 네임스페이스의 단일 단어 또는 계층적 분류법일 수 있습니다.

![chlimage_1-306](assets/chlimage_1-306.png)

* **[!UICONTROL 전체 제목 경로 표시]**

   이 확인란을 선택하면 상위 태그의 제목과 적용된 각 태그의 네임스페이스가 표시됩니다.

   예:

   * 선택됨: `Geometrixx Media: Gadgets / Cars`
   * 선택되지 않음: `Cars`
   단순 태그에는 차이가 없습니다.

   기본값은 선택 취소입니다.

* **[!UICONTROL 리프 태그만 표시]**

   이 확인란을 선택하면 다른 태그가 없는 적용된 태그만 표시됩니다.

   예를 들어 다음과 같은 TagID가 주어집니다.

   `Geometrixx Media: Gadgets / Cars`

   적용할 수 있는 태그는 다음과 같습니다.

   `Geometrixx Media (the namespace)`, `Gadgets`및 `Cars`

   * 선택:적용된 경우에만 `Cars` 표시됩니다.
   * 선택 취소:적용되는 경우 `Geometrixx Media``Gadgets`및 `Cars` 표시됩니다.
   단순 태그는 리프 태그입니다.

   기본값은 선택 취소입니다.

* **[!UICONTROL 링크 템플릿]**

   구성 요소 편집 대화 상자를 통해 링크가 활성화될 때 태그 클라우드에 링크를 표시하는 데 사용되는 기본 템플릿이 아닌 템플릿입니다.

* **[!UICONTROL 모든 태그에 동일한 크기 사용]**

   이 확인란을 선택하면 태그 클라우드의 모든 단어가 동일하게 스타일이 지정됩니다. 이 확인란을 선택하지 않으면 단어의 용도에 따라 다르게 스타일이 지정됩니다. 기본값은 선택 취소입니다.

## 추가 정보 {#additional-information}

개발자를 위한 태그 필수 [사항](tag.md) 페이지에서 자세한 내용을 확인할 수 있습니다.

태그 [생성 및 관리에 대한 자세한 내용은 UGC](tag-ugc.md) (사용자 생성 컨텐츠 태깅)를 참조하십시오.
