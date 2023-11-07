---
title: 클래식 UI 태깅 콘솔
description: Adobe Experience Manager Classic UI 태깅 콘솔에 대해 알아봅니다.
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
docset: aem65
exl-id: 8c6ba22f-5555-4e3c-998a-9353bd44715b
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 2%

---


# 클래식 UI 태깅 콘솔{#classic-ui-tagging-console}

이 섹션은 클래식 UI 태그 지정 콘솔용입니다.

터치에 적합한 UI 태깅 콘솔은 [여기](/help/sites-administering/tags.md#tagging-console).

클래식 UI 태깅 콘솔에 액세스하려면:

* 작성자
* 관리자 권한으로 로그인
* 예를 들어 콘솔로 이동합니다. [https://localhost:4502/tagging](https://localhost:4502/tagging)

![클래식 콘솔 창](assets/managing_tags_usingthetagasministrationconsole.png)

## 태그 및 네임스페이스 만들기 {#creating-tags-and-namespaces}

1. 시작 레벨에 따라 다음을 사용하여 태그 또는 네임스페이스를 만들 수 있습니다. **신규**:

   다음을 선택하는 경우 **태그** 네임스페이스를 만들 수 있습니다.

   ![이름 공간 만들기 대화 상자](assets/creating_tags_andnamespaces.png)

   네임스페이스를 선택하는 경우(예: **데모**) 해당 네임스페이스 내에 태그를 만들 수 있습니다.

   ![태그 대화 상자 만들기](assets/creating_tags_andnamespacesinnewnamespace.png)

1. 두 경우 모두 다음을 입력합니다.

   * **제목**
(*필수*) 태그의 표시 제목입니다. 모든 문자를 입력할 수 있지만 다음과 같은 특수 문자는 사용하지 않는 것이 좋습니다.

      * `colon (:)` - 네임스페이스 구분 기호
      * `forward slash (/)` - 하위 태그 구분 기호

     입력한 경우 이 문자가 표시되지 않습니다.

   * **이름**
(*필수*) 태그의 노드 이름입니다.

   * **설명**
(*선택 사항*) 태그에 대한 설명입니다.

   * 선택 **만들기**

## 태그 편집 {#editing-tags}

1. 오른쪽 창에서 편집할 태그를 선택합니다.
1. 클릭 **편집**.
1. 다음을 수정할 수 있습니다. **제목** 및 **설명**.
1. 클릭 **저장** 대화 상자를 닫습니다.

## 태그 삭제 {#deleting-tags}

1. 오른쪽 창에서 삭제할 태그를 선택합니다.
1. **삭제**&#x200B;를 클릭합니다.
1. 클릭 **예** 대화 상자를 닫습니다.

   더 이상 태그를 나열하면 안 됩니다.

## 태그 활성화 및 비활성화 {#activating-and-deactivating-tags}

1. 오른쪽 창에서 활성화(게시)하거나 비활성화(게시 취소)할 네임스페이스 또는 태그를 선택합니다.
1. 클릭 **활성화** 또는 **비활성화** 필요에 따라.

## 목록 - 태그가 참조되는 위치 표시 {#list-showing-where-tags-are-referenced}

**목록** 강조 표시된 태그를 사용하여 모든 페이지의 경로를 보여 주는 새 창을 엽니다.

![태그가 참조되는 위치 찾기](assets/list_showing_wheretagsarereferenced.png)

## 태그로 이동 {#moving-tags}

태그 관리자 및 개발자가 분류를 정리하거나 태그 ID의 이름을 변경할 수 있도록 태그를 새 위치로 이동할 수 있습니다.

1. 를 엽니다. **태깅** 콘솔.
1. 태그를 선택하고 **이동...** 을 클릭합니다.
1. 다음에서 **태그 이동** 대화 상자에서 다음을 정의합니다.

   * **끝**: 대상 노드.
   * **이름 바꾸기**: 새 노드 이름입니다.

1. 클릭 **이동**.

다음 **태그 이동** 대화 상자는 다음과 같습니다.

![태그 이동](assets/move_tag.png)

>[!NOTE]
>
>작성자는 태그를 이동하거나 태그 ID의 이름을 변경하면 안 됩니다. 필요한 경우 작성자는 [태그 제목 변경](#editing-tags).

## 태그 병합 {#merging-tags}

분류법에 중복 태그가 있는 경우 병합 태그를 사용할 수 있습니다. 태그 A가 태그 B에 병합되면 태그 A로 태그가 지정된 모든 페이지에 태그 B로 태그가 지정되며 태그 A는 작성자가 더 이상 사용할 수 없습니다.

태그를 다른 태그로 병합하려면 다음과 같이 하십시오.

1. 를 엽니다. **태깅** 콘솔.
1. 태그를 선택하고 **병합...** 을 클릭합니다.
1. 다음에서 **태그 병합** 대화 상자에서 다음을 정의합니다.

   * **대상**: 대상 노드.

1. 클릭 **병합**.

다음 **태그 병합** 대화 상자는 다음과 같습니다.

![태그 병합](assets/mergetag.png)

## 태그 사용 계산 {#counting-usage-of-tags}

태그가 몇 번 사용되고 있는지 확인하려면 다음을 수행하십시오.

1. 를 엽니다. **태깅** 콘솔.
1. 클릭 **사용 횟수** 맨 위 도구 모음: 열 카운트 결과에 결과가 표시됩니다.

## 다양한 언어로 태그 관리 {#managing-tags-in-different-languages}

선택 사항 `title`태그의 속성은 여러 언어로 번역될 수 있습니다. 태그 `titles` 사용자 언어 또는 페이지 언어에 따라 표시할 수 있습니다.

### 여러 언어로 태그 제목 정의 {#defining-tag-titles-in-multiple-languages}

다음 절차에서는 `title`/ 태그 **동물** 영어, 독일어 및 프랑스어로:

1. 로 이동 **태깅** 콘솔.
1. 태그 편집 **동물** 아래 **태그** > **스톡 사진**.
1. 다음 언어로 번역을 추가합니다.

   * **영어**: 동물
   * **독일어**: Tiere
   * **프랑스어**: Animux

1. 변경 사항을 저장합니다.

대화 상자는 다음과 같습니다.

![태그 편집](assets/edit_tag.png)

태깅 콘솔은 사용자 언어 설정을 사용하므로, 사용자 속성에서 언어를 프랑스어로 설정하는 사용자에게 동물 태그의 경우 &#39;Animux&#39;가 표시됩니다.

대화 상자에 새 언어를 추가하려면 섹션을 참조하십시오 [태그 편집 대화 상자에 새 언어 추가](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog) 다음에서 **개발자를 위한 태깅** 섹션.

### 지정된 언어로 페이지 속성에 태그 제목 표시 {#displaying-tag-titles-in-page-properties-in-a-specified-language}

기본적으로 태그 `titles`페이지 속성에는 페이지 언어가 표시됩니다. 페이지 속성의 태그 대화 상자에는 태그를 표시할 수 있는 언어 필드가 있습니다 `titles`다른 언어로. 다음 절차에서는 태그를 표시하는 방법을 설명합니다 `titles`프랑스어로:

1. 이전 섹션을 참조하여 프랑스어 번역을에 추가합니다. **동물** 아래 **태그** > **스톡 사진**.
1. 의 페이지 속성을 엽니다. **제품** 페이지의 영어 분기 **Geometrixx** 사이트.
1. 를 엽니다. **태그/키워드** 대화 상자(태그/키워드 표시 영역 오른쪽에 있는 풀다운 메뉴 선택)에서 **프랑스어** 오른쪽 아래 모서리에 있는 풀다운 메뉴의 언어.
1. 을(를) 선택할 수 있을 때까지 왼쪽/오른쪽 화살표를 사용하여 스크롤 **스톡 사진** 탭

   다음 항목 선택 **동물** (**Animux**) 태그를 닫고 대화 상자 바깥쪽을 선택하여 페이지 속성에 태그를 추가합니다.

   ![다른 태그 편집](assets/french_tag.png)

기본적으로 페이지 속성 대화 상자에 태그가 표시됩니다 `titles`페이지 언어에 따라.

일반적으로 태그의 언어는 페이지 언어를 사용할 수 있는 경우 페이지 언어에서 가져옵니다. 다음의 경우 [`tag` 위젯](/help/sites-developing/building.md#tagging-on-the-client-side) 는 다른 경우(예: 양식이나 대화 상자)에 사용되며 태그 언어는 컨텍스트에 따라 다릅니다.

>[!NOTE]
>
>표준 페이지 구성 요소의 태그 클라우드 및 메타 키워드는 현지화된 태그를 사용합니다 `titles`페이지 언어를 기반으로 합니다(사용 가능한 경우).
