---
title: 페이지 컨텐츠 편집
description: 콘텐츠는 페이지로 끌 수 있는 구성 요소를 사용하여 추가됩니다. 그런 다음 그 자리에서 편집하거나, 이동하거나 삭제할 수 있습니다.
uuid: e7b65ceb-263c-46f2-91e3-11dec3a016fa
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: de321869-ebf9-41a1-8203-e12bdb088678
docset: aem65
exl-id: e1b5aea0-983c-4e7b-9d35-d7beeee45dc7
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '1755'
ht-degree: 18%

---

# 페이지 콘텐츠 편집{#editing-page-content}

페이지가 만들어지면(launch 또는 live copy의 일부 또는 신규) 콘텐츠를 편집하여 필요한 업데이트 작업을 수행할 수 있습니다.

콘텐츠는 페이지로 끌 수 있는 [구성 요소](/help/sites-classic-ui-authoring/classic-page-author-default-components.md)(콘텐츠 유형에 맞는)를 사용하여 추가됩니다. 그런 다음 그 자리에서 편집하거나, 이동하거나 삭제할 수 있습니다.

>[!NOTE]
>
>계정에 다음이 필요합니다. [적절한 액세스 권한](/help/sites-administering/security.md) 및 [권한](/help/sites-administering/security.md#permissions) 구성 요소 추가, 편집 또는 삭제, 주석 달기, 잠금 해제 등과 같은 페이지 편집
>
>문제가 발생하면 시스템 관리자에게 문의하십시오.

## 사이드 킥 {#sidekick}

사이드 킥은 페이지를 작성할 때의 주요 도구입니다. 페이지를 작성할 때 부동 되므로 항상 표시됩니다.

다음을 포함한 몇 가지 탭과 아이콘을 사용할 수 있습니다.

* 구성 요소
* 페이지
* 정보
* 버전 관리
* 워크플로
* 모드
* 스캐폴딩
* Client Context
* 웹 사이트

![chlimage_1-71](assets/chlimage_1-71.png)

이를 통해 다음을 포함한 다양한 기능에 액세스할 수 있습니다.

* [구성 요소 선택](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#sidekick)
* [참조 표시](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#showing-references)
* [감사 로그 액세스](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#audit-log)
* [모드 전환](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#page-modes)
* [생성 중](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#creating-a-new-version), [복원 중](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#restoring-a-page-version-from-sidekick) 및 [비교](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#comparing-with-a-previous-version) 버전

* [게시](/help/sites-classic-ui-authoring/classic-page-author-publish-pages.md#publishing-a-page), [게시 취소](/help/sites-classic-ui-authoring/classic-page-author-publish-pages.md#unpublishing-a-page) 페이지

* [페이지 속성 편집](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md)

* [스캐폴딩](/help/sites-authoring/scaffolding.md)

* [client context](/help/sites-administering/client-context.md)

## 구성 요소 삽입 {#inserting-a-component}

### 구성 요소 삽입 {#inserting-a-component-1}

페이지를 열면 콘텐츠를 추가할 수 있습니다. 구성 요소(단락이라고도 함)를 추가하여 이 작업을 수행합니다.

새 구성 요소를 삽입하려면 다음 작업을 수행하십시오.

1. 삽입할 단락 유형을 선택하는 방법에는 여러 가지가 있습니다.

   * 레이블이 지정된 영역을 두 번 클릭합니다 **여기에 구성 요소 또는 자산을 드래그합니다...** - **새 구성 요소 삽입** 도구 모음이 열립니다. 구성 요소를 선택하고 **확인**.

   * 부동 도구 모음(사이드 킥이라고 함)에서 구성 요소를 드래그하여 새 단락을 삽입합니다.
   * 기존 단락을 마우스 오른쪽 단추로 클릭하고 **새로 만들기...** - 새 구성 요소 삽입 도구 모음이 열립니다. 구성 요소를 선택하고 **확인**.

   ![screen_shot_2012-02-15at115605am](assets/screen_shot_2012-02-15at115605am.png)

1. 사이드 킥과 **새 구성 요소 삽입** 도구 모음에 사용 가능한 구성 요소(단락 유형) 목록이 표시됩니다. 이들은 다양한 섹션들(예를 들어, 일반, 열 등)로 분할될 수 있고, 이는 필요에 따라 확장될 수 있다.

   프로덕션 환경에 따라 이러한 선택 사항이 다를 수 있습니다. 구성 요소에 대한 자세한 내용은 [기본 구성 요소](/help/sites-classic-ui-authoring/classic-page-author-default-components.md).

1. 페이지에 원하는 구성 요소를 삽입합니다. 단락을 두 번 클릭하면 단락을 구성하고 콘텐츠를 추가할 수 있는 창이 열립니다.

### 콘텐츠 파인더를 사용하여 구성 요소 삽입 {#inserting-a-component-using-the-content-finder}

에서 에셋을 끌어 페이지에 새 구성 요소를 추가할 수도 있습니다. [콘텐츠 파인더](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#the-content-finder). 이렇게 하면 자산이 포함된 적절한 유형의 새 구성 요소가 자동으로 만들어집니다.

다음은 다음 자산 유형에 대해 유효합니다(일부는 페이지/단락 시스템에 따라 다름).

| 자산 유형 | 결과 구성 요소 유형 |
|---|---|
| 이미지 | 이미지 |
| 문서 | 다운로드 |
| 제품 | 제품 |
| 비디오 | Flash |

>[!NOTE]
>
>이 동작은 설치에 대해 구성할 수 있습니다. 다음을 참조하십시오 [자산을 드래그하여 구성 요소 인스턴스를 만들도록 단락 시스템 구성](/help/sites-developing/developing-components.md#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance) 을 참조하십시오.

위의 에셋 유형 중 하나를 끌어 구성 요소를 만들려면

1. 페이지가 [**편집** 모드](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#page-modes)인지 확인합니다.
1. 를 엽니다. [콘텐츠 파인더](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#the-content-finder).
1. 필요한 에셋을 필요한 위치로 끕니다. [구성 요소 플레이스홀더](#componentplaceholder)는 구성 요소가 위치할 곳을 보여 줍니다.

   에셋 유형에 적절한 구성 요소가 필요한 위치에 만들어지게 됩니다. 여기에 선택한 에셋이 포함됩니다.

1. [편집](#editmovecopypastedelete) 필요한 경우 구성 요소입니다.

## 구성 요소 편집(컨텐츠 및 속성) {#editing-a-component-content-and-properties}

기존 단락을 편집하려면 다음 중 하나를 수행하십시오.

* **두 번 클릭** 단락을 열어 보십시오. 기존 내용으로 단락을 만들 때와 동일한 창이 표시됩니다. 변경 작업을 수행한 다음 **확인**.

* **마우스 오른쪽 버튼 클릭** 단락 및 클릭 **편집**.

* **클릭** 즉석 편집 모드로 전환하려면 단락을 두 번 클릭합니다(느리게 두 번 클릭). 대화 상자 창 내부가 아닌 페이지에서 텍스트를 직접 편집할 수 있습니다. 이 모드에서는 페이지 상단에 도구 모음이 제공됩니다. 변경하기만 하면 자동으로 저장됩니다.

## 구성 요소 이동 {#moving-a-component}

단락을 이동하려면 다음을 수행합니다.

>[!NOTE]
>
>[잘라내기 및 붙여넣기](#cut-copy-paste-a-component)를 사용하여 구성 요소를 이동할 수도 있습니다.

1. 이동할 단락을 선택합니다.

   ![screen_shot_2012-02-15at115855am](assets/screen_shot_2012-02-15at115855am.png)

1. 단락을 새 위치로 드래그합니다. AEM에서 녹색 확인 표시로 단락을 이동할 수 있는 위치를 보여 줍니다. 원하는 위치에 드롭합니다.
1. 단락이 이동됩니다:

   ![screen_shot_2012-02-15at120030pm](assets/screen_shot_2012-02-15at120030pm.png)

## 구성 요소 삭제 {#deleting-a-component}

단락을 삭제하려면:

1. 단락 선택 및 **마우스 오른쪽 버튼 클릭**:

   ![screen_shot_2012-02-15at120220pm](assets/screen_shot_2012-02-15at120220pm.png)

1. 선택 **삭제** 메뉴에서 삭제할 수 있습니다. AEM WCM은 이 작업을 실행 취소할 수 없으므로 단락을 삭제하라는 확인을 요청합니다.
1. **확인**&#x200B;을 클릭합니다.

>[!NOTE]
>
>다음을 설정한 경우 [전역 편집 도구 모음을 표시하는 사용자 속성](/help/sites-classic-ui-authoring/author-env-user-props.md) 를 사용하여 단락에 대해 특정 작업을 수행할 수도 있습니다. **복사**, **잘라내기**, **붙여넣기**, **삭제** 단추를 사용할 수 있습니다.
>
>다양 [키보드 단축키](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md) 사용할 수도 있습니다.

## 구성 요소 잘라내기/복사/붙여넣기 {#cut-copy-paste-a-component}

다음과 같은 경우 [구성 요소 삭제](#deleting-a-component) 컨텍스트 메뉴를 사용하여 구성 요소를 복사, 잘라내기 및/또는 붙여넣을 수 있습니다

>[!NOTE]
>
>다음을 설정한 경우 [전역 편집 도구 모음을 표시하는 사용자 속성](/help/sites-classic-ui-authoring/author-env-user-props.md) 를 사용하여 단락에 대해 특정 작업을 수행할 수도 있습니다. **복사**, **잘라내기**, **붙여넣기**, **삭제** 단추를 사용할 수 있습니다.
>
>다양 [키보드 단축키](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md) 사용할 수도 있습니다.

>[!NOTE]
>
>콘텐츠 잘라내기, 복사 및 붙여넣기는 동일한 페이지 내에서만 지원됩니다.

## 상속된 구성 요소 {#inherited-components}

상속된 구성 요소는 다음을 포함하여 다양한 시나리오의 제품일 수 있습니다.

* [다중 사이트 관리](/help/sites-administering/msm.md)와 결합하여 [스캐폴딩](/help/sites-classic-ui-authoring/classic-feature-scaffolding.md#scaffolding-with-msm-inheritance).

* [론치](/help/sites-classic-ui-authoring/classic-launches.md) (livecopy를 기반으로 할 때).
* 특정 구성 요소(예: Geometrixx 내의 상속된 단락 시스템)

상속을 취소(그런 다음 다시 활성화)할 수 있습니다. 구성 요소에 따라 다음 위치에서 사용할 수 있습니다.

1. **Live Copy**

   구성 요소가 라이브 카피 또는 론치의 일부인 경우 자물쇠 아이콘으로 표시됩니다. 자물쇠를 클릭하여 상속을 취소할 수 있습니다.

   * 구성 요소를 선택하면 자물쇠 아이콘이 표시됩니다. 예:

   ![chlimage_1-72](assets/chlimage_1-72.png)

   * 자물쇠는 구성 요소 대화 상자에도 표시됩니다. 예:

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. **상속된 단락 시스템**

   구성 대화 상자 예를 들어 Geometrixx 내의 상속된 단락 시스템과 마찬가지로

   ![chlimage_1-74](assets/chlimage_1-74.png)

## 주석 추가 {#adding-annotations}

[주석](/help/sites-classic-ui-authoring/classic-page-author-annotations.md) 다른 작성자가 콘텐츠에 대한 피드백을 제공할 수 있도록 허용합니다. 이는 종종 검토 및 유효성 검사 목적으로 사용됩니다.

## 페이지 미리보기 {#previewing-pages}

사이드 킥의 하단 테두리에 페이지를 미리 보는 데 중요한 두 가지 아이콘이 있습니다.

![](do-not-localize/chlimage_1-5.png)

* 연필 아이콘은 콘텐츠를 추가, 수정, 이동 또는 삭제할 수 있는 편집 모드에 있음을 보여 줍니다.

   ![](do-not-localize/chlimage_1-6.png)

* 돋보기 아이콘을 사용하면 페이지가 게시 환경에 표시될 상태로 표시되는 미리보기 모드를 선택할 수 있습니다(경우에 따라 페이지 새로 고침이 필요함).

   ![](do-not-localize/chlimage_1-7.png)

   미리보기 모드에서 사이드 킥이 줄어들게 됩니다. 아래 화살표 아이콘을 클릭하여 편집 모드로 돌아갑니다.

   ![](do-not-localize/chlimage_1-8.png)

## 찾기 및 바꾸기 {#find-replace}

동일한 구문에 대한 대규모 크기 조정 편집의 경우 **[찾기 및 바꾸기](/help/sites-classic-ui-authoring/author-env-search.md#find-and-replace)** 메뉴 옵션을 사용하면 웹 사이트의 섹션 내에서 문자열의 여러 인스턴스를 검색하고 바꿀 수 있습니다.

## 페이지 잠금 {#locking-a-page}

AEM에서는 다른 사람이 콘텐츠를 수정할 수 없도록 페이지를 잠글 수 있습니다. 이 기능은 하나의 특정 페이지를 많이 편집하거나 잠시 동안 페이지를 동결해야 할 때 유용합니다.

>[!CAUTION]
>
>페이지 잠금은 페이지를 잠근 사용자(또는 관리자 권한이 있는 계정)만이 페이지 잠금을 해제할 수 있으므로 주의하여 사용해야 합니다.

페이지를 잠그려면 다음을 수행하십시오.

1. 다음에서 **웹 사이트** 탭에서 잠글 페이지를 선택합니다.
1. 편집할 페이지를 두 번 클릭하여 엽니다.
1. 다음에서 **페이지** 사이드 킥 탭, 선택 **페이지 잠금**:

   ![screen_shot_2012-02-08at15750pm](assets/screen_shot_2012-02-08at15750pm.png)

   페이지가 다른 사용자에게 잠겨 있다는 메시지가 표시됩니다. 또한 의 오른쪽 창에서 **웹 사이트** 콘솔, AEM WCM은 페이지를 잠김으로 표시하고 어느 사용자가 페이지를 잠갔는지를 나타냅니다.

   ![screen_shot_2012-02-08at20657pm](assets/screen_shot_2012-02-08at20657pm.png)

## 페이지 잠금 해제 {#unlocking-a-page}

페이지 잠금을 해제하려면:

1. 다음에서 **웹 사이트** 탭에서 잠금 해제할 페이지를 선택합니다.
1. 페이지를 두 번 클릭하여 엽니다.
1. 다음에서 **페이지** 사이드 킥 탭, 선택 **페이지 잠금 해제**.

## 페이지 편집 실행 취소 및 재실행 {#undoing-and-redoing-page-edits}

페이지의 콘텐츠 프레임에 포커스가 있는 동안 다음 키보드 단축키를 사용하십시오.

* 실행 취소: Ctrl+Z (Windows) 또는 Cmd+Z (Mac)
* 다시 실행: Ctrl+Y(Windows) 또는 Cmd+Y(Mac)

하나 이상의 단락의 제거, 추가 또는 재배치를 실행 취소하거나 재실행하면 깜박임(기본 비헤이비어) 강조 표시가 영향을 받는 단락을 나타냅니다.

>[!NOTE]
>
>페이지 편집 내용을 실행 취소하거나 재실행할 때 가능한 사항에 대한 모든 세부 사항은 [페이지 편집 실행 취소 및 재실행 - 이론](#undoing-and-redoing-page-edits-the-theory)을 참조하십시오.

## 페이지 편집 내용 실행 취소 및 재실행 - 이론 {#undoing-and-redoing-page-edits-the-theory}

>[!NOTE]
>
>시스템 관리자가 다음을 수행할 수 있습니다. [실행 취소/다시 실행 기능의 다양한 측면 구성](/help/sites-administering/config-undo.md) 인스턴스의 요구 사항에 따라 을 선택합니다.

AEM은 사용자가 수행한 작업 내역과 해당 작업을 수행한 순서를 저장합니다. 따라서 수행한 순서대로 여러 작업을 실행 취소합니다. 그런 다음 다시 실행을 사용하여 하나 이상의 작업을 다시 적용할 수 있습니다.

컨텐트 페이지의 요소를 선택하면 실행 취소 및 다시 실행 명령이 텍스트 구성 요소와 같이 선택한 항목에 적용됩니다.

실행 취소 및 재실행 명령의 동작은 다른 소프트웨어 프로그램의 동작과 유사합니다. 명령을 사용하여 콘텐츠에 대한 결정을 내릴 때 웹 페이지의 최근 상태를 복원합니다. 예를 들어 텍스트 단락을 페이지의 다른 위치로 이동한 후 실행 취소 명령을 사용하여 단락을 원래 위치로 되돌릴 수 있습니다. 그런 다음 단락을 다시 이동하려면 다시 실행 명령을 사용합니다.

>[!NOTE]
>
>다음과 같은 작업을 수행할 수 있습니다.
>
>* 실행 취소를 사용한 이후 페이지 편집을 하지 않는 한 작업을 재실행합니다.
>* 최대 20개의 편집 작업을 실행 취소합니다(기본 설정).
>* 또한 [키보드 단축키](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md) 실행 취소 및 다시 실행의 경우.
>


다음 유형의 페이지 변경 사항에 대해 실행 취소 및 재실행을 사용할 수 있습니다.

* 단락 추가, 편집, 제거 및 이동
* 단락 콘텐츠 즉석 편집
* 페이지 내에서 항목 복사, 잘라내기 및 붙여넣기
* 페이지 간에 항목 복사, 잘라내기 및 붙여넣기
* 파일 및 이미지 추가, 제거 및 변경
* 주석 및 스케치 추가, 제거 및 변경
* 스캐폴드 변경 사항
* 참조 추가 및 제거
* 구성 요소 대화 상자에서 속성 값 변경.

양식 구성 요소가 렌더링되는 양식 필드는 페이지를 작성하는 동안 지정된 값을 갖지 않습니다. 따라서 실행 취소 및 재실행 명령은 이러한 유형의 구성 요소 값에 대한 변경 내용에 영향을 주지 않습니다. 예를 들어 드롭다운 목록에서 값 선택을 실행 취소할 수 없습니다.

>[!NOTE]
>
>파일 및 이미지 변경을 취소하거나 재실행하려면 특수 권한이 필요합니다. 또한 파일 및 이미지에 대한 변경 내용 실행 취소 기록은 최소 시간 동안 지속됩니다. 그러나 이 시간 이후에는 변경 사항의 실행 취소가 보장되지 않습니다. 관리자가 권한을 제공하고 기본 시간인 10시간을 변경할 수 있습니다.
