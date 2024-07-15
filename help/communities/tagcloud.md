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

`Social Tag Cloud` 구성 요소는 콘텐츠를 게시할 때 커뮤니티 구성원이 적용한 태그를 강조 표시합니다. 트렌드 주제를 식별하고 사이트 방문자가 태그가 지정된 콘텐츠를 빠르게 찾을 수 있도록 하는 수단입니다.

현재 트렌드를 식별하는 다른 방법을 보려면 [활동 트렌드](trends.md)를 방문하세요.

이 페이지에서는 `Social Tag Cloud` 구성 요소 대화 상자 설정을 설명하고 사용자 환경에 대해 설명합니다.

개발자에 대한 자세한 내용은 [Tag Essentials](tag.md)을(를) 참조하십시오.

태그 작성 및 관리 방법과 콘텐츠 태그가 적용되는 항목에 대한 내용은 [태그 관리](../../help/sites-administering/tags.md)를 참조하십시오.

## 소셜 태그 클라우드 추가 {#adding-a-social-tag-cloud}

작성자 모드에서 페이지에 `Social Tag Cloud` 구성 요소를 추가하려면 구성 요소 브라우저를 사용하여 `Communities / Social Tag Cloud`을(를) 찾아 태그 클라우드가 표시되어야 하는 페이지로 끌어옵니다.

필요한 정보는 [커뮤니티 구성 요소 기본 사항](basics.md)을 참조하세요.

[필수 클라이언트측 라이브러리](tag.md#essentials-for-client-side)가 포함된 경우 `Social Tag Cloud` 구성 요소는 다음과 같이 표시됩니다.

![소셜 태그](assets/social-tag.png)

## 소셜 태그 클라우드 구성 {#configuring-social-tag-cloud}

배치된 `Social Tag Cloud` 구성 요소를 선택하여 편집 대화 상자를 여는 `Configure` 아이콘에 액세스하고 선택합니다.

![구성](assets/configure-new.png)

**[!UICONTROL 소셜 태그 클라우드]** 탭에서 표시할 태그를 지정하고, 태그가 활성 링크인 경우 검색 결과를 위한 페이지 위치를 지정합니다.

![social-tag-cloud](assets/social-tag-cloud.png)

* 표시할 **[!UICONTROL 소셜 태그]**
표시할 UGC 태그를 식별합니다. 풀다운 옵션은 다음과 같습니다.

   * `From page and child pages`
   * `All tags`

  기본값은 `From page and child pages`입니다. 여기서 &quot;page&quot;는 아래의 **Page** 설정을 참조합니다.

* **[!UICONTROL 페이지]**

  `All tags)`이(가) 아닌 경우 필수 사항입니다. 페이지의 UGC 경로입니다. 기본값은 비워 두면 현재 페이지입니다.

* **[!UICONTROL 태그에 링크 없음]**

  선택하면 태그가 태그 클라우드에 일반 텍스트로 표시됩니다. 선택하지 않으면 태그는 해당 태그가 적용되는 모든 콘텐츠를 검색하는 활성 링크로 표시됩니다. 기본값은 선택 취소이며 **[!UICONTROL 검색 결과 경로]**&#x200B;을(를) 설정해야 합니다.

* **[!UICONTROL 검색 결과 경로]**

  **Page** 설정에 지정된 UGC 경로를 포함하는 UGC를 참조하도록 구성된 `Search Result` 구성 요소가 배치된 페이지의 경로입니다.

## 소셜 태그 클라우드의 표시 변경 {#change-display-of-social-tag-cloud}

**소셜 태그 클라우드**&#x200B;의 표시를 편집하려면 [디자인 모드](../../help/sites-authoring/default-components-designmode.md)를 입력하고 배치된 `Social Tag Cloud` 구성 요소를 두 번 클릭하여 추가 탭이 있는 대화 상자를 엽니다.

**[!UICONTROL 소셜 태그 클라우드(디자인)]** 탭을 사용하여 태그가 표시되는 방식을 지정하십시오. 태그는 단순 태그, 기본 네임스페이스의 단일 단어 또는 계층 분류법일 수 있습니다.

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

   * 선택함: 적용된 경우 `Cars`만 표시됩니다.
   * 선택 취소됨: `Geometrixx Media`, `Gadgets` 및 `Cars`이(가) 표시됩니다(적용된 경우).

  단순 태그는 리프 태그입니다.

  기본값은 선택 취소되어 있습니다.

* **[!UICONTROL 템플릿 연결]**

  구성 요소 편집 대화 상자를 통해 링크를 활성화하면 태그 클라우드에서 링크를 표시하는 데 사용되는 템플릿(기본값 제외)입니다.

* **[!UICONTROL 모든 태그에 동일한 크기]**

  선택하면 태그 클라우드의 모든 단어 스타일이 동일합니다. 선택하지 않으면 단어 용법에 따라 다른 스타일이 지정됩니다. 기본값은 선택 취소되어 있습니다.

## 추가 정보 {#additional-information}

자세한 내용은 개발자를 위한 [Tag Essentials](tag.md) 페이지에서 확인할 수 있습니다.

태그 만들기 및 관리에 대한 자세한 내용은 [UGC(사용자 생성 콘텐츠 태그 지정](tag-ugc.md))를 참조하십시오.
