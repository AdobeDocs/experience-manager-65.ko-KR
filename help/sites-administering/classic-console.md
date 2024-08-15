---
title: 클래식 UI 태깅 콘솔
description: Adobe Experience Manager Classic UI 태깅 콘솔에 대해 알아봅니다.
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
docset: aem65
exl-id: 8c6ba22f-5555-4e3c-998a-9353bd44715b
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 2%

---


# 클래식 UI 태깅 콘솔{#classic-ui-tagging-console}

이 섹션은 클래식 UI 태그 지정 콘솔용입니다.

>[!NOTE]
>
>터치에 적합한 UI 태그 지정 콘솔에 대한 자세한 내용은 [태그 관리](/help/sites-administering/tags.md#tagging-console)를 참조하십시오.

클래식 UI 태깅 콘솔에 액세스하려면:

* 작성자
* 관리자 권한으로 로그인
* 콘솔로 이동
예: [https://localhost:4502/tagging](https://localhost:4502/tagging)

![클래식 콘솔 창](assets/managing_tags_usingthetagasministrationconsole.png)

## 태그 및 네임스페이스 만들기 {#creating-tags-and-namespaces}

1. 시작 수준에 따라 **New**&#x200B;을(를) 사용하여 태그나 네임스페이스를 만들 수 있습니다.

   **태그**&#x200B;을(를) 선택하면 네임스페이스를 만들 수 있습니다.

   ![이름 공간 대화 상자 만들기](assets/creating_tags_andnamespaces.png)

   네임스페이스(예: **Demo**)를 선택하는 경우 해당 네임스페이스 내에 태그를 만들 수 있습니다.

   ![태그 대화 상자 만들기](assets/creating_tags_andnamespacesinnewnamespace.png)

1. 두 경우 모두 다음을 입력합니다.

   * **제목**
(*필수*) 태그의 표시 제목입니다. 모든 문자를 입력할 수 있지만,
다음과 같은 특수 문자는 사용하지 않는 것이 좋습니다.

      * `colon (:)` - 네임스페이스 구분 기호
      * `forward slash (/)` - 하위 태그 구분 기호

     입력한 경우 이 문자가 표시되지 않습니다.

   * **이름**
(*필수*) 태그의 노드 이름입니다.

   * **설명**
(*선택 사항*) 태그에 대한 설명입니다.

   * **만들기** 선택

## 태그 편집 {#editing-tags}

1. 오른쪽 창에서 편집할 태그를 선택합니다.
1. **편집**&#x200B;을 클릭합니다.
1. **제목** 및 **설명**&#x200B;을 수정할 수 있습니다.
1. 대화 상자를 닫으려면 **저장**&#x200B;을 클릭합니다.

## 태그 삭제 {#deleting-tags}

1. 오른쪽 창에서 삭제할 태그를 선택합니다.
1. **삭제**&#x200B;를 클릭합니다.
1. 대화 상자를 닫으려면 **예**&#x200B;를 클릭하세요.

   더 이상 태그를 나열하면 안 됩니다.

## 태그 활성화 및 비활성화 {#activating-and-deactivating-tags}

1. 오른쪽 창에서 활성화(게시)하거나 비활성화(게시 취소)할 네임스페이스 또는 태그를 선택합니다.
1. 필요에 따라 **활성화** 또는 **비활성화**&#x200B;를 클릭합니다.

## 목록 - 태그가 참조되는 위치 표시 {#list-showing-where-tags-are-referenced}

**목록**&#x200B;에서 강조 표시된 태그를 사용하여 모든 페이지의 경로를 표시하는 새 창을 엽니다.

![태그가 참조되는 위치 찾기](assets/list_showing_wheretagsarereferenced.png)

## 태그로 이동 {#moving-tags}

태그 관리자 및 개발자가 분류를 정리하거나 태그 ID의 이름을 변경할 수 있도록 태그를 새 위치로 이동할 수 있습니다.

1. **태그 지정** 콘솔을 엽니다.
1. 태그를 선택하고 위쪽 도구 모음(또는 상황에 맞는 메뉴)에서 **이동...**&#x200B;을 클릭합니다.
1. **태그 이동** 대화 상자에서 다음을 정의합니다.

   * 대상 노드인 **to**&#x200B;입니다.
   * **새 노드 이름인**(으)로 이름을 바꿉니다.

1. **이동**&#x200B;을 클릭합니다.

**태그 이동** 대화 상자는 다음과 같습니다.

![태그 이동](assets/move_tag.png)

>[!NOTE]
>
>작성자는 태그를 이동하거나 태그 ID의 이름을 변경하면 안 됩니다. 필요한 경우 작성자는 [태그 제목을 변경](#editing-tags)해야 합니다.

## 태그 병합 {#merging-tags}

분류법에 중복 태그가 있는 경우 병합 태그를 사용할 수 있습니다. 태그 A가 태그 B에 병합되면 태그 A로 태그가 지정된 모든 페이지에 태그 B로 태그가 지정되며 태그 A는 작성자가 더 이상 사용할 수 없습니다.

태그를 다른 태그로 병합하려면 다음과 같이 하십시오.

1. **태그 지정** 콘솔을 엽니다.
1. 태그를 선택하고 위쪽 도구 모음(또는 상황에 맞는 메뉴)에서 **병합...**&#x200B;을 클릭합니다.
1. **태그 병합** 대화 상자에서 다음을 정의합니다.

   * 대상 노드인 **into**.

1. **병합**&#x200B;을 클릭합니다.

**태그 병합** 대화 상자는 다음과 같습니다.

![태그 병합](assets/mergetag.png)

## 태그 사용 계산 {#counting-usage-of-tags}

태그가 몇 번 사용되고 있는지 확인하려면 다음을 수행하십시오.

1. **태그 지정** 콘솔을 엽니다.
1. 상단 도구 모음에서 **사용 개수**&#x200B;를 클릭합니다. 열 개수에는 결과가 표시됩니다.

## 다양한 언어로 태그 관리 {#managing-tags-in-different-languages}

태그의 선택적 `title` 속성은 여러 언어로 번역될 수 있습니다. 사용자 언어 또는 페이지 언어에 따라 태그 `titles`을(를) 표시할 수 있습니다.

### 여러 언어로 태그 제목 정의 {#defining-tag-titles-in-multiple-languages}

다음 절차에서는 **동물** 태그의 `title`을(를) 영어, 독일어 및 프랑스어로 번역하는 방법을 보여 줍니다.

1. **태그 지정** 콘솔로 이동합니다.
1. **동물** 태그를 **태그** > **스톡 사진** 아래에서 편집합니다.
1. 다음 언어로 번역을 추가합니다.

   * **영어**: 동물
   * **독일어**: 제목
   * **프랑스어**: 애니메이션

1. 변경 사항을 저장합니다.

대화 상자는 다음과 같습니다.

![태그 편집](assets/edit_tag.png)

태깅 콘솔은 사용자 언어 설정을 사용하므로, 사용자 속성에서 언어를 프랑스어로 설정하는 사용자에게 동물 태그의 경우 &#39;Animux&#39;가 표시됩니다.

대화 상자에 새 언어를 추가하려면 **개발자를 위한 태그 지정** 섹션에서 [태그 편집 대화 상자에 새 언어 추가](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog) 섹션을 참조하십시오.

### 지정된 언어로 페이지 속성에 태그 제목 표시 {#displaying-tag-titles-in-page-properties-in-a-specified-language}

기본적으로 페이지 속성의 `titles` 태그는 페이지 언어로 표시됩니다. 페이지 속성의 태그 대화 상자에 다른 언어로 태그 `titles`을(를) 표시할 수 있는 언어 필드가 있습니다. 다음 절차에서는 태그 `titles`을(를) 프랑스어로 표시하는 방법을 설명합니다.

1. **태그** > **스톡 사진** 아래의 **동물**&#x200B;에 프랑스어 번역을 추가하려면 이전 섹션을 참조하세요.
1. **Geometrixx** 사이트의 영어 분기에서 **Products** 페이지의 페이지 속성을 엽니다.
1. 태그/키워드 표시 영역의 오른쪽에 있는 풀다운 메뉴를 선택하여 **태그/키워드** 대화 상자를 열고 오른쪽 아래 모서리에 있는 풀다운 메뉴에서 **프랑스어** 언어를 선택합니다.
1. **스톡 사진** 탭을 선택할 수 있을 때까지 왼쪽/오른쪽 화살표로 스크롤합니다.

   **Animals**(**Animux**) 태그를 선택하고 대화 상자 바깥쪽을 선택하여 태그를 닫고 페이지 속성에 태그를 추가합니다.

   ![다른 태그 편집](assets/french_tag.png)

기본적으로 [페이지 속성] 대화 상자는 페이지 언어에 따라 `titles` 태그를 표시합니다.

일반적으로 태그의 언어는 페이지 언어를 사용할 수 있는 경우 페이지 언어에서 가져옵니다. [`tag` 위젯](/help/sites-developing/building.md#tagging-on-the-client-side)을(를) 다른 경우(예: 폼이나 대화 상자)에 사용하는 경우 태그 언어는 컨텍스트에 따라 다릅니다.

>[!NOTE]
>
>표준 페이지 구성 요소의 태그 클라우드 및 메타 키워드는 페이지 언어를 기반으로 현지화된 태그 `titles`을(를) 사용합니다(사용 가능한 경우).
