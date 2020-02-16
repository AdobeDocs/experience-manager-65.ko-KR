---
title: 클래식 UI 태깅 콘솔
seo-title: 클래식 UI 태깅 콘솔
description: 클래식 UI 태깅 콘솔에 대해 알아보십시오.
seo-description: 클래식 UI 태깅 콘솔에 대해 알아보십시오.
uuid: 51e29422-f967-424b-a7fd-4ca2ddc6b8a3
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: b279c033-bc93-4e62-81ad-123c40b9fdd2
docset: aem65
translation-type: tm+mt
source-git-commit: 684d2d5f73d571a15c8155e7870134c28dc892b7

---


# 클래식 UI 태깅 콘솔{#classic-ui-tagging-console}

이 섹션은 클래식 UI 태깅 콘솔에 사용됩니다.

터치에 적합한 UI 태그 지정 콘솔이 [여기에 있습니다](/help/sites-administering/tags.md#tagging-console).

클래식 UI 태깅 콘솔에 액세스하려면:

* 작성자
* 관리자 권한으로 로그인
* 콘솔로 이동합니다(예: [https://localhost:4502/tagging).](https://localhost:4502/tagging)

![](assets/managing_tags_usingthetagasministrationconsole.png)

## 태그 및 네임스페이스 만들기 {#creating-tags-and-namespaces}

1. 작업을 시작하는 수준에 따라 **새로 만들기**&#x200B;를 사용하여 태그 또는 네임스페이스를 만들 수 있습니다.

   **태그**&#x200B;를 선택하는 경우 네임스페이스를 만들 수 있습니다.

   ![](assets/creating_tags_andnamespaces.png)

   네임스페이스(예: **데모**)를 선택하는 경우 해당 네임스페이스 안에 태그를 만들 수 있습니다.

   ![](assets/creating_tags_andnamespacesinnewnamespace.png)

1. 두 경우 모두

   * **제목**(*필수*)태그의 표시 제목입니다. 문자를 입력할 수 있지만 다음 특수 문자는 사용하지 않는 것이 좋습니다.

      * `colon (:)` - 네임스페이스 구분 기호
      * `forward slash (/)` - 하위 태그 구분 기호
      이러한 문자를 입력하면 표시되지 않습니다.

   * **이름**(*필수*)태그의 노드 이름입니다.

   * **설명**(*선택*&#x200B;사항) 태그에 대한 설명입니다.

   * select **Create**


## 태그 편집 {#editing-tags}

1. 오른쪽 창에서 편집할 태그를 선택합니다.
1. **편집**&#x200B;을 클릭합니다. 
1. **제목** 및 **설명**&#x200B;을 수정할 수 있습니다.
1. **저장**&#x200B;을 클릭하여 대화 상자를 닫습니다.

## 태그 삭제 {#deleting-tags}

1. 오른쪽 창에서 삭제할 태그를 선택합니다.
1. **삭제**&#x200B;를 클릭합니다. 
1. Click **Yes** to close the dialog.

   더 이상 태그를 나열하지 않아야 합니다.

## 태그 활성화 및 비활성화 {#activating-and-deactivating-tags}

1. 오른쪽 창에서 활성화(게시) 또는 비활성화(게시 취소)할 네임스페이스 또는 태그를 선택합니다.
1. 필요에 따라 **활성화** 또는 **비활성화**&#x200B;를 클릭합니다.

## 목록 - 태그 참조 위치 표시 {#list-showing-where-tags-are-referenced}

**목록**&#x200B;을 클릭하면 강조된 태그를 사용하는 모든 페이지의 경로를 보여 주는 새 창이 열립니다.

![](assets/list_showing_wheretagsarereferenced.png)

## 태그 이동 {#moving-tags}

태그 관리자 및 개발자가 택소노미를 정리하거나 태그 ID의 이름을 변경할 수 있도록 태그를 새 위치로 이동할 수 있습니다.

1. **Tagging** 콘솔을 엽니다.
1. 태그를 선택하고 상단 도구 모음이나 컨텍스트 메뉴에서 **이동...**&#x200B;을 클릭합니다.
1. **태그 이동** 대화 상자에서 다음을 정의합니다.

   * **끝**: 대상 노드
   * **이름 바꾸기**: 새 노드 이름

1. **이동**&#x200B;을 클릭합니다.

**태그 이동** 대화 상자의 모양은 다음과 같습니다.

![](assets/move_tag.png)

>[!NOTE]
>
>작성자는 태그를 이동하거나 태그 ID의 이름을 변경할 수 없습니다. 필요한 경우 작성자는 태그 제목만 [변경해야 합니다](#editing-tags).

## 태그 병합 {#merging-tags}

분류 체계에 중복이 있을 경우 태그 병합을 사용할 수 있습니다. 태그 A를 태그 B로 병합하면 태그 A가 적용된 모든 페이지에 태그 B가 적용되고 작성자는 태그 A를 더 이상 사용할 수 없습니다.

태그를 다른 태그로 병합하는 방법은 다음과 같습니다.

1. **Tagging** 콘솔을 엽니다.
1. 태그를 선택하고 상단 도구 모음이나 컨텍스트 메뉴에서 **병합...**&#x200B;을 클릭합니다.
1. **태그 병합** 대화 상자에서 다음을 정의합니다.

   * **대상**: 대상 노드

1. **병합**&#x200B;을 클릭합니다.

The **Merge Tag** dialog looks as follows:

![](assets/mergetag.png)

## 태그 사용 횟수 {#counting-usage-of-tags}

태그가 사용된 횟수를 확인하는 방법은 다음과 같습니다.

1. **Tagging** 콘솔을 엽니다.
1. 상단 도구 모음에서 **사용 횟수**&#x200B;를 클릭하면 개수 열에 결과가 표시됩니다.

## 여러 언어로 태그 관리 {#managing-tags-in-different-languages}

태그의 선택적 `title`속성은 여러 언어로 번역될 수 있습니다. Tag `titles` can then be displayed according to the user language or to the page language.

### 여러 언어로 태그 제목 정의 {#defining-tag-titles-in-multiple-languages}

The following procedure shows how to translate the `title`of the tag **Animals** into English, German and French:

1. Go to the **Tagging** console.
1. Edit the tag **Animals** below **Tags** > **Stock Photography**.
1. 다음 언어로 번역을 추가합니다.

   * **영어**: Animals
   * **독일어**: Tiere
   * **프랑스어**: Animaux

1. 변경 사항을 저장합니다.

대화 상자의 모양은 다음과 같습니다.

![](assets/edit_tag.png)

Tagging 콘솔은 사용자 언어 설정을 사용하므로 사용자 속성에서 언어를 프랑스어로 설정하는 사용자에 대해 Animal 태그의 경우 &#39;Animaux&#39;가 표시됩니다.

To add a new language to the dialog, please refer to the section [Adding a New Language to the Edit Tag Dialog](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog) in the **Tagging for Developers** section.

### 페이지 속성에 지정된 언어로 태그 제목 표시 {#displaying-tag-titles-in-page-properties-in-a-specified-language}

By default the tag `titles`in the page properties are displayed in the page language. The tag dialog in the page properties has a language field that enables the display of tag `titles`in a different language. The following procedure describes how to display the tag `titles`in French:

1. Refer to the previous section to add the French translation to the **Animals** below **Tags** > **Stock Photography**.
1. **Geometrixx** 사이트의 English 분기에서 **Products** 페이지의 페이지 속성을 엽니다.
1. 태그/ **키워드** 표시 영역의 오른쪽에 있는 풀다운 메뉴를 선택하여 태그/키워드 대화 상자를 열고 오른쪽 하단에 **있는 풀다운 메뉴에서** 프랑스어 언어를 선택합니다.
1. Stock Photography 탭을 선택할 때까지 왼쪽 오른쪽 화살표를 사용하여 **스크롤합니다** .

   Animals **** (Animaux ****) 태그를 선택하고 대화 상자 외부를 선택하여 닫고 태그를 페이지 속성에 추가합니다.

   ![](assets/french_tag.png)

By default, the Page Properties dialog displays the tag `titles`according to the page language.

일반적으로 페이지 언어를 사용할 수 있는 경우 페이지 언어에서 태그 언어를 가져옵니다. When the [ `tag` widget](/help/sites-developing/building.md#tagging-on-the-client-side) is used in other cases (for example in forms or in dialogs), the tag language depends on the context.

>[!NOTE]
>
>The tag cloud and the meta keywords in the standard page component use the localized tag `titles`based on the page language, if available.