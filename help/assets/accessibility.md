---
title: ' [!DNL Experience Manager Assets]의 액세스 가능한 기능 및 인터페이스'
description: ' [!DNL Adobe Experience Manager] 6.5 [!DNL Assets] 장애가 있는 사용자를 돕는 접근성 기능에 대해 알아봅니다.'
contentOwner: AG
feature: Asset Management
role: User, Developer, Leader
exl-id: 15555941-99a2-4586-8d7b-b22f3ec17805
solution: Experience Manager, Experience Manager Assets
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '1898'
ht-degree: 1%

---

<!--
Possible topics to cover in this article are below.

* Compile a list of enhancements done in the last ~1 year.
* Showcase a few prominent use cases (search?) in a screencast.
* Top-level actions supported, such as clickable UI elements, keyboard shortcuts, popup dialogs, and so on.
* List all UIs that are keyboard navigable.
* Unified list of the product tasks supported, such as, search assets, download assets, add or editing metadata, use DM Viewers, and so on.
* Do we need to add support matrix of user tasks with browser and screen reader combinations. Everything may not work in all browsers and/or using all screen readers.
* Any exceptions that users should be aware of. It may help to call out (it may be done in ACR) what tasks are NOT supported.
* CTAs – what's next and more info from AEM team:
  * Link to ACRs on a.com.
  * Generic a11y info by Adobe to begin with.
  * Link to a11y-specific online methods to report issues, seek support, or request enhancements, if any. Asked the a11y team on Slack.
-->

# [!DNL Adobe Experience Manager Assets]의 접근성 기능 {#accessibility-in-aem-assets}

[!DNL Adobe Experience Manager]을(를) 사용하면 콘텐츠 작성자 및 게시자가 웹에서 놀라운 경험을 제공할 수 있습니다. Adobe은 [!DNL Experience Manager]의 접근성을 개선하여 장애가 있는 작성자를 포함하도록 노력하고 있습니다. 이 소프트웨어는 모든 유형의 사용자의 요구 사항을 충족하도록 지속적으로 향상되며 시각적, 청각적, 이동성 또는 기타 장애가 있는 개인을 포함한 전 세계 표준을 준수합니다.

[!DNL Experience Manager]은(는) 준수하는 표준을 설명하고 제품의 접근성 기능에 대해 간략히 설명하며 준수 수준을 설명하는 적합성 정보를 게시합니다. 접근성 적합성 보고서는 [!DNL Experience Manager] 사용자가 다양한 표준 준수 수준을 이해하는 데 도움이 됩니다. [!DNL Assets]에서 향상된 기능을 통해 모든 사용자는 키보드, 화면 판독기, 돋보기 및 기타 보조 기술을 통해 인터페이스를 쉽게 사용할 수 있습니다.

[!DNL Experience Manager]은(는) 다음 표준에 대한 다양한 수준의 지원을 제공합니다.

* [WCAG(웹 콘텐츠 접근성 지침) 2.1](https://www.w3.org/TR/WCAG/).
* [회생법 제508조를 개정함](https://www.access-board.gov/guidelines-and-standards/communications-and-it/about-the-ict-refresh/final-rule/text-of-the-standards-and-guidelines).
* [접근성 이니셔티브 - W3C에서 WAI-ARIA(Accessible Rich Internet Applications)](https://www.w3.org/WAI/standards-guidelines/aria/).
* [EN 301 549](https://en.wikipedia.org/wiki/EN_301_549).

준수 수준에 대한 세부 정보가 포함된 보고서를 읽으려면 [접근성 적합성 보고서](https://www.adobe.com/kr/accessibility/compliance.html)&#x200B;(ACR) 페이지를 참조하십시오.

[!DNL Dynamic Media]에 액세스하는 방법을 알아보려면 [다음 위치의 액세스 가능성 [!DNL Dynamic Media]](/help/assets/accessibility-dm.md)을 참조하세요.

## 보조 기술 {#at-support}

장애가 있는 사용자는 웹 콘텐츠에 액세스하고 소프트웨어 제품을 사용하기 위해 하드웨어와 소프트웨어에 의존하는 경우가 많습니다. 이러한 도구를 보조 기술이라고 합니다. [!DNL Experience Manager Assets]은(는) 소프트웨어의 핵심 기능을 사용할 때 다음 유형의 AT(보조 기술)에서 작업할 수 있습니다.

* 화면 판독기 및 화면 돋보기.
* 음성 인식 소프트웨어.
* 키보드 사용 - 탐색 및 단축키.
* 스위치 컨트롤, 재생 가능한 점자 디스플레이 및 기타 컴퓨터 입력 장치를 포함한 보조 하드웨어.
* UI 확대 도구.

## 액세스 가능한 사용 사례 [!DNL Experience Manager Assets]개 {#accessible-assets-use-cases}

[!DNL Experience Manager]에서 접근성 기능은 [!DNL Experience Manager] 사용자와 해당 고객의 두 가지 주요 요구 사항을 해결합니다.

* 콘텐츠 디자이너 및 제작자를 위해 고객 및 웹 사이트 방문자가 차례로 사용하는 액세스 가능한 콘텐츠를 만들고 게시할 수 있는 기능이 있습니다. 장애인 개인은 보조 기술의 도움을 받아 콘텐츠를 이용한다. 자세한 내용은 [웹 액세스 가능성 지침](/help/managing/web-accessibility.md)을 참조하세요.
* [!DNL Experience Manager]을(를) 사용하면 장애가 있는 사용자와 관리자가 사용자 인터페이스와 컨트롤에 액세스하여 콘텐츠를 만들고 관리할 수 있습니다. 장애가 있는 사용자는 보조 기술을 사용하여 [!DNL Assets] 기능을 탐색, 사용 및 관리할 수 있습니다.

[!DNL Assets]의 핵심 기능은 이전보다 더 쉽게 액세스할 수 있으며 글로벌 표준 준수를 개선하기 위해 정기적으로 업데이트됩니다. [!DNL Assets]의 CRUD 작업에는 어느 정도의 액세스 가능성이 내장되어 있습니다. 키보드 단축키, 화면 판독기 텍스트, 색상 대비 등을 사용하여 자산 추가, 관리, 검색 및 배포와 같은 DAM 워크플로우에 액세스할 수 있습니다.

## 키보드 사용 지원 {#keyboard-use}

포인터로 클릭 가능하거나 실행 가능한 많은 사용자 인터페이스 요소도 키보드를 사용하여 와 결합할 수 있습니다. 키보드를 사용하여 UI 요소에 집중하고 적절한 작업을 수행할 수 있습니다. 사용자는 키보드 단축키를 사용하여 UI 요소에 집중하지 않고 키보드를 사용하여 명령 또는 작업을 트리거할 수 있습니다. 예를 들어, 사용자는 키보드를 사용하여 사용자 인터페이스 컨트롤을 탐색하고 `Return`을(를) 선택한 다음 `Alt + 2` 키보드 단축키를 선택하여 사용자 인터페이스 왼쪽에 있는 에셋의 타임라인을 열 수 있습니다.

<!-- TBD items:

* The option to toggle between list view and card view exposes relevant info to the screen readers. What about column view option? This info can go into 'basic handling' info aka article to 'understand and use the workspace'.
* How to open and browse through the profile popup dialog in [!DNL Experience Manager] UI using a keyboard? The navigation does not match the order of visual display of options on the UI. This info can go into 'basic handling' info aka article to 'understand and use the workspace'. What about setting preferences and impersonating a user?
* Using the [!DNL Experience Manager] tag browser and operating the options like delete tag? This info can go into 'basic handling' info aka article to 'understand and use the workspace'.
* Read-only form fields can be focused with the keyboard. Can users tab to these fields to understand the contents and are they able to copy text from the fields?
-->

### [!DNL Assets]의 키보드 단축키 {#keyboard-shortcuts}

[!DNL Assets]의 다음 작업은 나열된 키보드 바로 가기를 사용합니다. [!DNL Experience Manager] 콘솔에 적용되는 대부분의 키보드 단축키는 [!DNL Assets]에도 적용됩니다. [콘솔용 키보드 단축키](/help/sites-authoring/keyboard-shortcuts.md#keyboard-shortcuts)를 참조하십시오. 키보드 단축키를 [사용 또는 사용 안 함으로 설정하는 방법](/help/sites-authoring/keyboard-shortcuts.md#deactivating-keyboard-shortcuts)을 참조하세요.

| 사용자 인터페이스 또는 시나리오 | 키보드 단축키 | 작업 |
|---|---|---|
| [!DNL Assets] 사용자 인터페이스의 열 보기 | 위쪽 및 아래쪽 화살표 키 | 동일한 계층 내에서 파일 및 폴더로 이동합니다. |
| [!DNL Assets] 사용자 인터페이스의 열 보기 | 왼쪽 및 오른쪽 화살표 키 | 현재 폴더의 위나 아래에 있는 파일 및 폴더로 이동합니다. |
| [!DNL Assets]에서 폴더 검색 중 | `/` | Omnisearch 상자를 열어 검색을 호출합니다. |
| [!DNL Assets] 콘솔 | &grave; | 사이드 레일 전환 |
| [!DNL Assets] 콘솔 | `Alt + 1` | 콘텐츠 트리를 엽니다. |
| [!DNL Assets] 콘솔 | `Alt + 2` | [!UICONTROL 탐색] 왼쪽 레일을 엽니다. |
| [!DNL Assets] 콘솔 | `Alt + 3` | 선택한 자산의 [!UICONTROL 타임라인]을 표시합니다. |
| [!DNL Assets] 콘솔 | `Alt + 4` | 선택한 자산의 라이브 카피 참조를 엽니다. |
| [!DNL Assets] 콘솔 | `Alt + 5` | 선택한 폴더에서 검색 및 검색을 시작합니다. |
| 에셋 또는 폴더가 선택되었습니다. | 백스페이스키 | 선택한 에셋 또는 폴더를 삭제합니다. |
| 에셋 또는 폴더가 선택되었습니다. | `p` | 선택한 자산의 속성 페이지를 엽니다. |
| 에셋 또는 폴더가 선택되었습니다. | `e` | 선택한 자산을 편집합니다. |
| 에셋 또는 폴더가 선택되었습니다. | `m` | 선택한 자산을 이동합니다. |
| 에셋 또는 폴더가 선택되었습니다. | `Ctrl + c` | 선택한 자산을 복사합니다. |
| 에셋 또는 폴더가 선택되었습니다. | `Esc` | 선택 항목을 취소합니다. |
| 대화 상자가 열리고 초점이 맞춰집니다 | `Esc` | 대화 상자를 닫습니다. |
| DAM의 폴더 내부 | `Ctrl + v` | 복사한 자산을 붙여넣습니다. |
| [!DNL Assets] 콘솔 | `Ctrl + A` | 모든 자산을 선택합니다. |
| 자산 속성 페이지 | `Ctrl + S` | 변경 사항을 저장합니다. |
| [!DNL Assets] 콘솔 | `?` | 키보드 단축키 목록을 참조하십시오. |

## 로그인 및 [!DNL Assets] 사용자 인터페이스 탐색 {#login}

사용자는 키보드를 사용하여 로 이동하고 로그인 필드를 입력하여 로그인할 수 있습니다. 로그인 페이지의 잘못된 사용자 이름 및 암호 조합으로 인한 오류 메시지는 오류가 발생할 때마다 화면 판독기에서 알려줍니다.

로그인 후 DAM 사용자는 키보드를 사용하여 [!DNL Assets] 사용자 인터페이스 내에서 탐색할 수 있습니다. 왼쪽 레일, 메뉴, 사용자 프로필, 검색 창, 파일 및 폴더, 관리 및 구성 설정과 같은 사용자 인터페이스 요소는 키보드를 사용하여 탐색할 수 있습니다. 키보드 탐색 순서는 왼쪽에서 오른쪽, 위에서 아래입니다. 키보드를 사용하여 탐색할 때 포커스를 둘 때 실행 가능한 옵션이 더 나은 색상 대비로 강조 표시되고 화면 판독기에서 내레이션을 수행합니다. 필요한 경우 메뉴에서 포커스가 있는 옵션의 상태(예: 확장, 축소 및 혼합 상태)가 화면 판독기에 의해 표시됩니다. 또한 화면 판독기는 모양이나 인터페이스 배치 대신 실행 가능한 옵션의 용도를 알려줍니다.

사용자가 메뉴에서 도움말 또는 사용자 프로필 옵션을 확장하면 화면 판독기에서 적절한 옵션이나 상태를 알립니다. 사용자가 사용자 프로필 옵션을 확장하면 키보드를 사용하여 사용 가능한 옵션을 선택할 수 있습니다. 예를 들어 관리자가 다른 사용자를 가장할 수 있습니다. 사용자가 [!UICONTROL 도움말] 옵션에서 문자열을 검색하는 경우 내레이터는 검색이 진행 중임을 나타내기 위해 &quot;도움말 검색&quot;을 알립니다.

<!-- TBD: Removing for now. Add a more informative video later. Host it on tv.adobe

![Keyboard navigation of top options in [!DNL Experience Manager] user interface](assets/keyboard-navigation-in-aem.gif)

*Figure: Navigating through the options at the top of [!DNL Experience Manager] user interface using `Tab` key.*
-->

## 에셋 검색 및 관련 정보 보기 {#browse}

[!DNL Assets] 사용자 인터페이스에서 사용자는 키보드를 사용하여 DAM 저장소의 기존 디지털 에셋 목록을 찾아보고, 에셋을 미리 보거나 다운로드하고, 생성된 렌디션을 보고, 보기를 전환하고, 생성된 렌디션을 보고, 타임라인 및 버전 기록을 보고, 설명 및 참조를 보고, 메타데이터를 보고 관리할 수 있습니다.

<!-- TBD: Not sure about the following list items mean:

In [!DNL Experience Manager] header section, when navigating in browse mode, screen reader now announces,
  
  * Suggestions to search in Omnisearch.
  * The state as expanded or collapsed for Solutions, Help, Inbox and User options.
  * The Searching Help status message that is displayed when user enters a search string in Search for Help field under Help option
  * The error message if incorrect value is entered in Impersonate as field under User option and focus correctly moves to the text field (NPR-33804).

Review CQ-4282133 before adding - Close option in a coral-dialog was not accessible through keyboard, due to which user cannot trigger close option through keyboard press in version preview dialog. After fix, user can close dialog through close option using keyboard.

* CQ-4273122 - Assets of video/audio type will have aria-label in format "Multimedia player: <Title>" so users relying on screen-reader will get to know that they are video/audio assets.
-->

에셋 저장소를 탐색할 때 다음 기능을 사용하여 액세스 가능성을 높일 수 있습니다.

* 화면 판독기는 아이콘 이름 대신 아이콘의 용도나 기능을 설명하는 텍스트 대체 요소를 알려줍니다.
* 사용자는 키보드 키를 사용하여 자산 참조 목록의 대화형 사용자 인터페이스 옵션에 액세스하고 포커스를 맞출 수 있습니다.
* 목록 보기의 각 행에 있는 요소는 화면 판독기에서 동일한 행의 요소로 표시됩니다.
* `Tab` 키를 사용하여 탐색할 때 포커스가 버전 미리 보기에서 닫기 옵션으로 이동할 수 있습니다.
* 키보드를 사용하여 검색할 때 강조 표시된 실행 가능한 사용자 인터페이스 옵션은 시각적 포커스가 더 높고 대비가 향상됩니다. 집중 영역이 사용자에게 더 잘 식별될 수 있도록 합니다.
* `Esc` 키를 사용하여 썸네일 보기에서 빠른 작업 아이콘을 제거해도 마지막 포커스 항목에서 키보드 포커스가 제거되지 않습니다.
* 자산을 선택한 상태에서 `Alt + 4` 바로 가기 키를 선택하면 왼쪽 레일에서 [!UICONTROL 참조] 목록이 열립니다. `Tab` 키를 사용하면 0이 아닌 참조 항목을 탐색할 수 있습니다. 0이 아닌 참조 항목만 탐색하면 작업량과 키 입력도 절약됩니다.
* 에셋에 대한 댓글은 에셋 타임라인에서 사용할 수 있습니다. 키보드 또는 키보드 단축키를 사용하여 왼쪽 레일에 액세스하는 경우 액세스할 수 있습니다.
* 키보드를 사용하여 [!UICONTROL 의 &#x200B;]보기 설정[!DNL Experience Manager]에 액세스할 수 있습니다. 사용자는 화살표 키를 사용하여 사용 가능한 카드 크기를 탐색하고 탭 스루를 선택하여 기존 보기 설정 보기에서 다른 요소를 탐색하고 설정할 수 있습니다.

<!-- TBD: Gradually, as more enhancements are done in these categories, add more content.

## Add and upload digital assets {#upload}

## Configure and administer [!DNL Assets] {#config-admin}

* List the a11y fixes in workflows to configure and administer [!DNL Experience Manager Assets]?
* Some enhancements in Processing profiles creation or application to a folder?
* Some enhancements to metadata properties UI?
-->

## 디지털 자산 관리 {#manage-assets}

CRUD 작업, 에셋 다운로드, 메타데이터 추가 등 다양한 에셋 관리 작업에 액세스할 수 있습니다. [!DNL Assets]을(를) 사용하면 화면 판독기, 키보드 등의 다양한 보조 기술을 사용하여 작업을 수행할 수 있습니다.

키보드를 사용하여 [저장소를 탐색하고 자산을 다운로드하는 방법](https://youtu.be/K3dgqMRQJys)에 대한 비디오 데모를 참조하십시오.

마케터 및 관리자와 같은 역할로 일반적으로 수행되는 메타데이터 작업의 경우 다음 기능은 접근성을 향상시킵니다.

* 이제 키보드를 사용하여 자산 [!UICONTROL 속성] 페이지의 [!UICONTROL 저장 및 닫기] 옵션에 액세스할 수 있습니다.
* 화면 판독기에는 자산 [!UICONTROL 속성]의 [!UICONTROL 기본] 탭에서 선택한 태그를 삭제하는 옵션이 표시됩니다.
* 사용자는 키보드와 함께 Datepicker 팝업 대화 상자를 사용할 수 있습니다. Datepicker 사용자 인터페이스 요소를 사용하여 설정 시간 및 해제 시간을 설정하고 날짜를 선택합니다.
* 키보드를 사용하는 드래그 기능은 화면 판독기의 찾아보기 모드에서 [!UICONTROL 메타데이터 스키마 편집기]에서 올바르게 작동합니다.
* 사용자는 키보드를 사용하여 [!UICONTROL 속성] 폴더의 [!UICONTROL 권한] 탭에 있는 [!UICONTROL 폐쇄된 사용자 그룹] 아래의 사용자 또는 그룹 추가 필드로 포커스를 이동할 수 있습니다.

## 디지털 자산 검색 {#search-assets}

빠르고 원활한 에셋 검색 경험을 통해 콘텐츠 속도가 향상됩니다. 콘텐츠 속도 사용 사례는 핵심 [!DNL Assets] 기능의 일부입니다. Omnisearch 막대에서 검색을 시작하려면 키보드 단축키 `/`을(를) 사용하거나 화면 판독기와 함께 `Tab`을(를) 사용하여 검색 옵션을 빠르게 찾을 수 있습니다. 검색 옵션 ![검색 옵션](assets/do-not-localize/search_icon.png)에 포커스가 있을 때 화면 판독기에서 옵션 이름을 &quot;검색 단추&quot;로 내레이션이 지정됩니다. `Return`을(를) 선택하여 Omnisearch 상자를 열 수 있습니다. 화면 판독기에서 검색 상자에 입력한 키워드에 내레이션이 지정될 뿐만 아니라 [!DNL Experience Manager Assets]이(가) 제공하는 제안 사항에도 내레이션이 지정됩니다. 사용자는 화살표 키, `Return` 및 `Tab`의 조합을 사용하여 검색을 트리거하는 다양한 옵션에 액세스할 수 있습니다.

다음 기능을 사용하여 검색 기능에 액세스할 수 있습니다.

* 화면 판독기에서 사용할 수 있는 페이지 제목은 페이지를 자산의 검색 페이지로 식별하는 데 도움이 됩니다.
* 사용자는 Omnisearch 필드 내에서 에셋을 검색합니다. 키보드 탐색 또는 키보드 단축키 `/`을(를) 사용하여 열 수 있습니다.
* 사용자는 검색 키워드를 입력한 다음 화살표 키를 사용하여 자동 제안을 선택할 수 있습니다. `Return` 키를 사용하여 강조 표시된 제안을 선택할 수 있으며 선택한 제안에 대한 자산을 검색합니다.
* 화면 판독기는 검색 결과를 필터링할 때 필터 패널에서 혼합 상태 확인란(중첩된 모든 확인란을 선택하지 않으면 첫 번째 수준 확인란이 선택되지 않고 클릭스루됨)을 식별하고 알릴 수 있습니다.
* Omnisearch 상자를 닫으면 사용자 포커스가 검색 옵션으로 이동합니다.

검색 결과를 필터링할 때:

* 검색 결과 페이지에는 화면 판독기 사용자를 더 잘 이해할 수 있는 유용한 제목이 있습니다.
* 화면 판독기는 검색 필터의 옵션을 확장 가능한 아코디언으로 알려줍니다.
* 혼합 상태 옵션이 있는 술어는 화면 판독기에서 알려줍니다.

## 자산 공유 {#share-assets}

<!-- TBD: Anything about accessibility in DA, BP? AAL team confirmed that there's no content for AAL a11y on helpx.
-->

에셋을 공유할 때 다음 기능은 접근성을 개선합니다.

* 사용자는 링크 공유 대화 상자의 이메일 주소 검색 및 추가 필드 내에서 키보드를 사용하여 포커스를 이동할 수 있습니다.

* 링크 공유 대화 상자에서 검색 모드로 탐색할 때 화면 판독기에서

   * 대화 상자가 로드될 때 테이블 정보에 내레이션을 사용하지 마십시오.
   * 나열된 모든 제안으로 이동할 수 있습니다.
   * 이메일 주소 추가 및 검색 필드에 표시된 제안 사항에 내레이션을 적용합니다.

## 액세스 가능한 설명서 {#accessible-docs}

[!DNL Experience Manager]은(는) 장애가 있는 사용자가 사용할 수 있도록 액세스 가능한 설명서를 제공합니다. 다음은 Adobe이 템플릿과 컨텐츠를 지속적으로 개선하는 동안 컨텐츠 제공을 지금 사용할 수 있도록 하는 데 도움이 됩니다.

* 화면 판독기는 텍스트를 읽을 수 있습니다.
* 이미지와 일러스트레이션에 대체 텍스트를 사용할 수 있습니다.
* 키보드 탐색이 가능합니다.
* 대비 비율은 설명서 웹 사이트의 일부 부분을 강조 표시하는 데 도움이 됩니다.

## 피드백 제공 {#a11y-feedback}

접근성과 관련하여 피드백을 제공하고, 질문하고, 제품 개선을 요청하려면 다음 방법을 사용하십시오.

* [www.adobe.com/accessibility/feedback.html](https://www.adobe.com/accessibility/feedback.html)에서 양식을 작성하십시오.
* access@adobe.com으로 이메일을 보내주십시오.

>[!MORELIKETHIS]
>
>* [의  [!DNL Dynamic Media]](/help/assets/accessibility-dm.md)접근성 기능.
>* [각 서비스 팩 릴리스에서 수행된 개선 사항의 릴리스 노트](/help/release-notes/release-notes.md).
>* [[!DNL Adobe Experience Manager] 접근성 지침](/help/managing/web-accessibility.md).
>* [Adobe 솔루션에 대한 적합성 보고서(ACR) 및 VPAT 목록](https://www.adobe.com/kr/accessibility/compliance.html).
