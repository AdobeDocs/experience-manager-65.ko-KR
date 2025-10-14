---
title: 페이지 작성에 대한 빠른 안내서
description: 페이지 콘텐츠 작성의 주요 작업에 대한 빠른 개요 안내서
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
exl-id: a7e16555-9bbe-4da2-817c-4495a0193f3f
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '1540'
ht-degree: 62%

---

# 페이지 작성에 대한 빠른 안내서{#quick-guide-to-authoring-pages}

이러한 절차는 AEM에서 페이지 콘텐츠를 작성하는 주요 작업에 대한 빠른 안내(고급)입니다.

절차는 다음과 같습니다.

* 포괄적인 내용을 담고 있지는 않습니다.
* 자세한 설명서에 대한 링크를 제공합니다.

AEM을 사용한 작성 작업에 대한 자세한 내용은 다음을 참조하십시오.

* [작성자를 위한 첫 번째 단계](/help/sites-authoring/first-steps.md)
* [페이지 작성](/help/sites-authoring/page-authoring.md)

## 몇 가지 빠른 힌트 {#a-few-quick-hints}

세부 사항의 개요를 제공하기 전에 기억해야 할 가치가 있는 일반적인 팁과 힌트에 대한 간단한 컬렉션을 살펴보십시오.

### Sites 콘솔 {#sites-console}

* **만들기**

   * 이 버튼은 여러 콘솔에서 사용할 수 있습니다. 제공된 옵션은 상황에 맞는 옵션이므로 시나리오에 따라 달라질 수 있습니다.

* 폴더의 페이지 재정렬

   * 이 작업은 [목록 보기](/help/sites-authoring/basic-handling.md#list-view)에서 수행할 수 있습니다. 변경 사항이 적용되고 다른 보기에 표시됩니다.

#### 페이지 작성 {#page-authoring}

* 링크 탐색

   * **편집** 모드에 있는 경우 ***링크를 탐색에 사용할 수 없습니다***. 링크를 사용하여 탐색하려면 다음 방법 중 하나를 사용하여 [페이지를 미리 보기](/help/sites-authoring/editing-content.md#previewing-pages)해야 합니다.

      * [미리보기 모드](/help/sites-authoring/editing-content.md#preview-mode)
      * [게시됨으로 보기](/help/sites-authoring/editing-content.md#view-as-published)

* 버전이 페이지 편집기에서 시작/만들어지지 않습니다. 이제 선택한 리소스에 대해 **만들기** 또는 [타임라인](/help/sites-authoring/basic-handling.md#timeline)을 통해 사이트 콘솔에서 수행됩니다.

>[!NOTE]
>
>작성 작업을 보다 쉽게 할 수 있는 몇 가지 키보드 단축키가 있습니다.
>
>* [페이지 편집 시 키보드 단축키](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)
>* [콘솔용 키보드 단축키](/help/sites-authoring/keyboard-shortcuts.md)
>

### 페이지 찾기 {#finding-your-page}

페이지 찾기에 대한 여러 측면이 있습니다. 탐색 및/또는 검색할 수 있습니다.

1. **사이트** 콘솔을 엽니다([전역 탐색](/help/sites-authoring/basic-handling.md#global-navigation)에서 **사이트** 옵션 사용) - Adobe Experience Manager 링크(왼쪽 상단)를 선택하면 트리거됩니다(드롭다운).

1. 해당 페이지를 탭/클릭하여 트리 아래로 탐색합니다. 페이지 리소스가 표시되는 방식은 사용 중인 보기([카드, 목록 또는 열](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources))에 따라 다릅니다.

   ![screen_shot_2018-03-21at160214](assets/screen_shot_2018-03-21at160214.png)

1. [헤더에서 이동 경로](/help/sites-authoring/basic-handling.md#theheaderwithbreadcrumbs)를 사용하여 트리 위로 탐색합니다. 그러면 선택한 위치로 돌아갈 수 있습니다.

   ![qgtap-01](assets/qgtap-01.png)

1. 페이지를 [검색](/help/sites-authoring/search.md)할 수도 있습니다. 표시된 결과에서 페이지를 선택할 수 있습니다.

   ![qgtap-03](assets/qgtap-03.png)

### 새 페이지 만들기 {#creating-a-new-page}

[페이지를 만들려면](/help/sites-authoring/managing-pages.md#creating-a-new-page):

1. [페이지를 만들 위치로 이동](#finding-your-page)합니다.
1. **만들기** 아이콘을 사용한 다음 목록에서 **페이지**&#x200B;를 선택합니다.

   ![qgtap-02](assets/qgtap-02.png)

1. 이렇게 하면 [새 페이지를 만들 때 &#x200B;](/help/sites-authoring/managing-pages.md#creating-a-new-page)필요한 정보를 수집하는 과정을 안내하는 마법사가 열립니다. 화면에 표시되는 안내를 따릅니다.

### 추가 작업을 수행할 페이지 선택 {#selecting-your-page-for-further-action}

작업을 수행할 수 있도록 페이지를 선택할 수 있습니다. 페이지를 선택하면 도구 모음이 자동으로 업데이트되면서 해당 리소스와 관련된 작업이 표시됩니다.

페이지를 선택하는 방법은 콘솔에서 사용 중인 보기에 따라 다음과 같이 달라집니다.

1. 열 보기:

   * 필요한 리소스에 대한 썸네일을 클릭합니다. 썸네일 위에 확인 표시가 나타나 썸네일이 선택되었음을 나타냅니다.

1. 목록 보기:

   * 필요한 리소스에 대한 썸네일을 클릭합니다. 썸네일 위에 확인 표시가 나타나 썸네일이 선택되었음을 나타냅니다.

1. 카드 보기:

   * 다음을 사용하여 [필요한 리소스를 선택](/help/sites-authoring/basic-handling.md#viewingandselectingyourresources)하여 선택 모드에 들어갑니다.

      * 모바일 장치: 길게 선택
      * 데스크톱: [빠른 작업](/help/sites-authoring/basic-handling.md#quick-actions) - 확인 표시 아이콘:

   ![screen_shot_2018-03-21at160503](assets/screen_shot_2018-03-21at160503.png)

   * 카드 위에 확인 표시가 나타나 페이지가 선택되었음을 나타냅니다.

   >[!NOTE]
   >
   >선택 모드에 있으면 **Select** 아이콘(확인 표시)이 **Deselect** 아이콘(교차)으로 변경됩니다.

### 빠른 작업(카드 보기/데스크탑 전용) {#quick-actions-card-view-desktop-only}

[빠른 작업](/help/sites-authoring/basic-handling.md#quick-actions)을 사용할 수 있습니다.

1. 작업을 수행할 [페이지로 이동](#finding-your-page)합니다.
1. 필요한 리소스를 나타내는 카드 위에 마우스 포인터를 두면 빠른 작업이 표시됩니다.

   ![screen_shot_2018-03-21at160503-1](assets/screen_shot_2018-03-21at160503-1.png)

### 페이지 콘텐츠 편집 {#editing-your-page-content}

1. 편집할 [페이지로 이동](#finding-your-page)합니다.
1. [편집(연필) 아이콘을 사용하여](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing) 편집할 페이지를 엽니다.

   ![screen_shot_2018-03-21at160607](assets/screen_shot_2018-03-21at160607.png)

   다음 방법 중 하나로 해당 아이콘에 액세스할 수 있습니다.

   * 적절한 리소스에 대한 [빠른 작업(카드 보기/데스크탑 전용)](#quick-actions-card-view-desktop-only)
   * [페이지를 선택했을 때](#selectiingyourpageforfurtheraction)의 도구 모음

1. 편집기가 열리면 다음과 같은 작업을 수행할 수 있습니다.

   * 다음 작업을 수행하여 [페이지에 새 구성 요소 추가](/help/sites-authoring/editing-content.md#inserting-a-component):

      * 사이드 패널 열기
      * 구성 요소 탭([구성 요소 브라우저](/help/sites-authoring/author-environment-tools.md#components-browser)) 선택
      * 필요한 구성 요소를 페이지로 드래그

     다음 아이콘을 사용하여 사이드 패널을 열고 닫을 수 있습니다.

     ![사이드 패널 열기](do-not-localize/screen_shot_2018-03-21at160738.png)

   * [페이지의](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) 기존 구성 요소 콘텐츠를 편집합니다.

      * 를 클릭하여 구성 요소 도구 모음을 엽니다. **편집**(연필) 아이콘을 사용하여 대화 상자를 엽니다.
      * 선택하고 길게 누르거나 느리게 더블 클릭하여 구성 요소에 대한 즉석 편집기를 엽니다. 사용 가능한 작업이 표시됩니다(일부 구성 요소의 경우, 선택이 제한됨).
      * 사용 가능한 모든 작업을 보려면 다음 아이콘을 사용하여 전체 화면 모드로 들어갑니다.

     ![전체 화면 모드](do-not-localize/screen_shot_2018-03-21at160706.png)

   * [기존 구성 요소의 속성 구성](/help/sites-authoring/editing-content.md#component-edit-dialog)

      * 를 클릭하여 구성 요소 도구 모음을 엽니다. **구성**(렌치) 아이콘을 사용하여 대화 상자를 엽니다.

   * 다음 방법 중 하나로 [구성 요소를 이동](/help/sites-authoring/editing-content.md#moving-a-component)합니다.

      * 필요한 구성 요소를 새 위치로 끕니다.
      * 를 클릭하여 구성 요소 도구 모음을 엽니다. 필요한 경우 **잘라내기**&#x200B;를 사용한 다음 **붙여넣기** 아이콘을 사용합니다.

   * 구성 요소 [복사(및 붙여넣기):](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste)

      * 를 클릭하여 구성 요소 도구 모음을 엽니다. 필요에 따라 **복사**&#x200B;를 사용한 다음 **붙여넣기** 아이콘을 사용합니다.

   >[!NOTE]
   >
   >같은 페이지나 다른 페이지에 구성 요소를 **붙여넣을** 수 있습니다. 잘라내기/복사 작업 전에 이미 열려 있었던 다른 페이지에 붙여넣은 경우 해당 페이지를 새로 고쳐야 합니다.

   * 구성 요소 [삭제:](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste)

      * 클릭하여 구성 요소 도구 모음을 열고 **삭제** 아이콘을 사용합니다.

   * 페이지에 [주석 추가](/help/sites-authoring/annotations.md#annotations):

      * **주석** 모드(말풍선 아이콘)를 선택합니다. **주석 추가**(더하기) 아이콘을 사용하여 주석을 추가합니다. 오른쪽 상단의 X를 사용하여 주석 모드를 끝냅니다.

     ![주석](do-not-localize/screen_shot_2018-03-21at160813.png)

   * [페이지 미리보기](/help/sites-authoring/editing-content.md#preview-mode)(게시 환경에 표시될 모양 보기)

      * 도구 모음에서 **미리보기**&#x200B;를 선택합니다.

   * **편집** 드롭다운 선택기를 사용하여 편집 모드로 돌아가거나 다른 모드를 선택합니다.

   >[!NOTE]
   >
   >콘텐츠에서 링크를 사용하여 탐색하려면 [미리 보기 모드](/help/sites-authoring/editing-content.md#preview-mode)를 사용해야 합니다.

### 페이지 속성 편집 {#editing-the-page-properties}

[페이지 속성을 편집](/help/sites-authoring/editing-page-properties.md)하는 방법에는 두 가지(기본) 방법이 있습니다.

* **Sites** 콘솔에서:

   1. 게시할 [페이지로 이동](#finding-your-page)합니다.
   1. 다음 중 하나를 사용하여 **속성** 아이콘을 선택합니다.

      * 적절한 리소스에 대한 [빠른 작업(카드 보기/데스크탑 전용)](#quick-actions-card-view-desktop-only)
      * [페이지를 선택했을 때](#selectiingyourpageforfurtheraction)의 도구 모음

  ![screen_shot_2018-03-21at160850](assets/screen_shot_2018-03-21at160850.png)

   1. 페이지 속성이 표시됩니다. 필요에 따라 업데이트한 다음 [저장]을 사용하여 이러한 내용을 유지할 수 있습니다.

* [페이지를 편집할 때](#editing-your-page-content):

   1. **페이지 정보** 메뉴를 엽니다.
   1. **속성 열기**&#x200B;를 선택하여 속성을 편집할 수 있는 대화 상자를 엽니다.

  ![screen_shot_2018-03-21at160920](assets/screen_shot_2018-03-21at160920.png)

### 페이지 게시(또는 게시 취소) {#publishing-your-page-or-unpublishing}

페이지를 게시 및 게시 취소하는 [방법에는](/help/sites-authoring/publishing-pages.md) 두 가지 기본 방법이 있습니다.

* **Sites** 콘솔에서:

   1. 게시할 [페이지로 이동](#finding-your-page)합니다.
   1. 다음 중 하나에서 **빠른 게시** 아이콘을 선택합니다.

      * 적절한 리소스에 대한 [빠른 작업(카드 보기/데스크탑 전용)](#quick-actions-card-view-desktop-only)
      * [페이지를 선택했을 때](#selectiingyourpageforfurtheraction)(또는 [나중에 게시](/help/sites-authoring/publishing-pages.md#main-pars-title-12)에 액세스할 때)의 도구 모음

  ![screen_shot_2018-03-21at160957](assets/screen_shot_2018-03-21at160957.png)

* [페이지를 편집할 때](#editing-your-page-content):

   1. **페이지 정보** 메뉴를 엽니다.
   1. **페이지 게시**&#x200B;를 선택합니다.

  ![screen_shot_2018-03-21at161026](assets/screen_shot_2018-03-21at161026.png)

* **게시 관리** 옵션을 통해서만 콘솔에서 페이지의 게시를 취소할 수 있으며, 이 옵션은 빠른 작업이 아닌 도구 모음에서만 사용할 수 있습니다.

  **페이지 게시 취소** 옵션은 편집기의 **페이지 정보** 메뉴를 통해서도 사용할 수 있습니다.

  ![screen_shot_2018-03-21at161059](assets/screen_shot_2018-03-21at161059.png)

  자세한 내용은 [페이지 게시](/help/sites-authoring/publishing-pages.md#unpublishing-pages)를 참조하십시오.

### 페이지 이동, 복사 및 붙여넣기 또는 삭제 {#move-copy-and-paste-or-delete-your-page}

이러한 작업은 모두 다음 작업을 수행하여 트리거할 수 있습니다.

1. 이동, 복사 및 붙여넣기 또는 삭제할 [페이지로 이동](#finding-your-page)하십시오.
1. 복사(및 붙여넣기)를 선택하고 필요한 경우 다음 중 하나를 사용하여 아이콘을 이동하거나 삭제합니다.

   * 필요한 리소스에 대한 [빠른 작업(카드 보기/데스크탑 전용)](#quick-actions-card-view-desktop-only)
   * [페이지를 선택했을 때](#selecting-your-page-for-further-action)의 도구 모음

   그런 다음 작업에 따라 수행합니다.

   * 복사:

      * 새 위치로 이동하여 붙여넣습니다.

   * 이동:

      * 마법사가 열리고 페이지 이동에 필요한 정보를 수집합니다. 화면에 표시되는 안내를 따릅니다.

   * 삭제:

      * 작업을 확인하는 메시지가 표시됩니다.

   >[!NOTE]
   >
   >삭제는 빠른 작업으로 사용할 수 없습니다.

### 페이지 잠금(및 잠금 해제) {#locking-your-page-then-unlocking}

[페이지 잠금](/help/sites-authoring/editing-content.md#locking-a-page)을 사용하면 사용자가 작업하는 동안 다른 작성자가 작업할 수 없습니다. 잠금(및 잠금 해제) 아이콘/버튼은 다음에 있습니다.

* [페이지를 선택했을 때](#selecting-your-page-for-further-action)의 도구 모음
* 페이지를 편집할 때 [[페이지 정보] 드롭다운 메뉴](#editing-the-page-properties)
* 페이지를 편집할 때 페이지 도구 모음(페이지가 잠겨 있을 때)

예를 들어 잠금 아이콘은 다음과 같습니다.

![screen_shot_2018-03-21at161124](assets/screen_shot_2018-03-21at161124.png)

### 페이지 참조에 액세스 {#accessing-page-references}

참조 레일에서 페이지 또는 페이지에 대한 [참조](/help/sites-authoring/author-environment-tools.md#references)에 빠르게 액세스할 수 있습니다.

1. **페이지를 선택**&#x200B;하기 전이나 후에 도구 모음 아이콘을 사용하여 [참조](#selecting-your-page-for-further-action)를 선택합니다.

   ![screen_shot_2018-03-21at161210](assets/screen_shot_2018-03-21at161210.png)

   참조 유형 목록이 표시됩니다.

   ![screen-shot_2019-03-05at114412](assets/screen-shot_2019-03-05at114412.png)

1. 필요한 참조 유형을 클릭하여 자세한 내용을 표시하고(해당되는 경우) 추가 작업을 수행합니다.

### 페이지 버전 생성 {#creating-a-version-of-your-page}

페이지의 [버전](/help/sites-authoring/working-with-page-versions.md)을 생성하려면:

1. 타임라인 레인을 열려면 **[페이지를 선택](/help/sites-authoring/basic-handling.md#timeline)**&#x200B;하기 전이나 후에 도구 모음 아이콘을 사용하여 [타임라인](#selecting-your-page-for-further-action)을 선택합니다.

   ![screen_shot_2018-03-21at161355](assets/screen_shot_2018-03-21at161355.png)

1. 타임라인 열 오른쪽 하단에 있는 위쪽 화살표를 클릭하여 **다른 버전으로 저장**&#x200B;을 비롯한 추가 단추를 표시합니다.

   ![screen-shot_2019-03-05at114600](assets/screen-shot_2019-03-05at114600.png)

1. **다른 버전으로 저장**&#x200B;을 선택한 후 **만들기**&#x200B;를 선택합니다.

### 페이지 버전 복원/비교 {#restoring-comparing-a-version-of-your-page}

페이지 버전을 복원 및/또는 비교할 때 동일한 기본 메커니즘이 사용됩니다.

1. **[페이지를 선택](/help/sites-authoring/basic-handling.md#timeline)**&#x200B;하기 전이나 후에 도구 모음 아이콘을 사용하여 [타임라인](#selecting-your-page-for-further-action)을 선택합니다.

   ![screen_shot_2018-03-21at161355-1](assets/screen_shot_2018-03-21at161355-1.png)

   페이지 버전이 이미 저장된 경우, 타임라인에 나열됩니다.

1. 복원할 버전을 클릭합니다. 그러면 다음과 같은 추가 작업 버튼이 표시됩니다.

   * **이 버전으로 되돌리기**

      * 버전이 복원됩니다.

   * **차이 표시**

      * 두 버전 간의 차이가 강조 표시된 채로 페이지가 열립니다.
