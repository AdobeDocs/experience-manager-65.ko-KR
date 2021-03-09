---
title: ' [!DNL Experience Manager Assets]의 액세스 가능성'
description: ' [!DNL Adobe Experience Manager] 6.5 [!DNL Assets] 의 액세서빌러티 기능이 장애가 있는 사용자를 돕는 방법을 알아봅니다.'
contentOwner: AG
translation-type: tm+mt
source-git-commit: cf86d0c38e326766b35318e78a94a3f32e166e01
workflow-type: tm+mt
source-wordcount: '1919'
ht-degree: 2%

---


<!--
Possible topics to cover in this article are below.

* Compile a list of enhancements done in the last ~1 year.
* Showcase a few prominent use cases (search?) in a screencast.
* Top-level actions supported, such as clickable UI elements, keyboard shortcuts, popup dialogs, etc.
* List all UIs that are keyboard navigable.
* Unified list of the product tasks supported, such as, search assets, download assets, add or editing metadata, use DM Viewers, etc.
* Do we need to add support matrix of user tasks with browser and screen reader combinations. Everything may not work in all browsers and/or using all screen readers.
* Any exceptions that users should be aware of. It may help to call out (it may be done in ACR) what tasks are NOT supported.
* CTAs – what's next and more info from AEM team:
  * Link to ACRs on a.com.
  * Generic a11y info by Adobe to begin with.
  * Link to a11y-specific online methods to report issues, seek support, or request enhancements, if any. Asked the a11y team on Slack.
-->

# [!DNL Adobe Experience Manager Assets] {#accessibility-in-aem-assets}의 액세스 가능성 기능

[!DNL Adobe Experience Manager] 컨텐츠 제작자와 출판업체는 웹에서 탁월한 경험을 제공할 수 있습니다. Adobe은 [!DNL Experience Manager]의 액세서빌러티를 개선하여 장애가 있는 생성자를 포함시키기 위해 노력하고 있습니다. 소프트웨어는 모든 유형의 사용자의 요구 사항을 충족하도록 지속적으로 향상되고 시각, 청각, 이동 또는 기타 장애가 있는 개인을 포함하는 전세계 표준을 준수합니다.

[!DNL Experience Manager] 표준을 설명하고 제품의 액세스 가능성 기능에 대한 개요를 설명하고 규정 준수 수준을 설명하는 적합성 정보를 게시합니다. 액세스 가능성 준수 보고서는 [!DNL Experience Manager] 사용자가 다양한 표준을 준수하는 수준을 이해하는 데 도움이 됩니다. [!DNL Assets]의 향상된 기능을 통해 모든 사용자는 키보드, 화면 판독기, 확대기 및 기타 보조 기술을 통해 인터페이스를 쉽게 사용할 수 있습니다.

[!DNL Experience Manager] 에서는 다음 표준에 대한 다양한 수준의 지원을 제공합니다.

* [웹 컨텐츠 액세스 가능성 지침(WCAG) 2.1](https://www.w3.org/TR/WCAG/).
* [재활법](https://www.access-board.gov/guidelines-and-standards/communications-and-it/about-the-ict-refresh/final-rule/text-of-the-standards-and-guidelines) 508조 개정
* [접근성 이니셔티브 - W3C의 액세스 가능한 리치 인터넷 애플리케이션(WAI-ARIA)](https://www.w3.org/WAI/standards-guidelines/aria/).
* [EN 301 549](https://en.wikipedia.org/wiki/EN_301_549).

준수 수준에 대한 세부 정보가 있는 보고서를 읽으려면 [액세스 가능성 보고서](https://www.adobe.com/accessibility/compliance.html) (ACR) 페이지를 참조하십시오.

[!DNL Dynamic Media]에 액세스할 수 있는 방법을 알려면  [!DNL Dynamic Media]](/help/assets/accessibility-dm.md)의 [접근성을 참조하십시오.

## 보조 기술 {#at-support}

장애가 있는 사용자는 주로 하드웨어와 소프트웨어에 의존하여 웹 컨텐츠에 액세스하고 소프트웨어 제품을 사용합니다. 이러한 도구는 보조 기술로 알려져 있습니다. [!DNL Experience Manager Assets] 소프트웨어의 핵심 기능을 사용할 때 다음 유형의 보조 기술(AT)을 사용할 수 있습니다.

* 화면 판독기 및 화면 돋보기
* 음성 인식 소프트웨어
* 키보드 사용 - 내비게이션 및 바로 가기
* 스위치 컨트롤, 새로 고침 가능한 점자 디스플레이, 기타 컴퓨터 입력 디바이스 등 보조 하드웨어입니다.
* 확대경 툴

## [!DNL Experience Manager Assets] 액세스 가능한 사용 사례  {#accessible-assets-use-cases}

[!DNL Experience Manager]에서 액세스 가능성 기능은 [!DNL Experience Manager] 사용자 및 해당 고객의 두 가지 주요 요구 사항을 해결합니다.

* 컨텐츠 디자이너 및 크리에이터에게는 고객과 웹 사이트 방문자가 차례로 사용하는 액세스 가능한 컨텐츠를 만들고 게시하는 기능이 있습니다. 장애가 있는 사용자는 보조 기술의 도움을 받아 컨텐츠를 사용합니다. 자세한 내용은 [웹 액세스 가능성 지침](/help/managing/web-accessibility.md)을 참조하십시오.
* [!DNL Experience Manager] 또한 장애가 있는 사용자와 관리자가 사용자 인터페이스와 컨트롤에 액세스하여 컨텐츠를 만들고 관리할 수 있습니다. 장애가 있는 사용자는 보조 기술을 사용하여 [!DNL Assets] 기능을 탐색, 사용 및 관리할 수 있습니다.

[!DNL Assets]의 핵심 기능은 이전보다 더 쉽게 액세스할 수 있으며 글로벌 표준 준수를 개선하기 위해 정기적으로 업데이트됩니다. [!DNL Assets]의 CRUD 작업은 이러한 작업에 어느 정도의 액세서빌러티를 내장합니다. 키보드 단축키, 화면 판독기 텍스트, 색상 대비 등을 사용하면 에셋 추가, 관리, 검색 및 배포와 같은 DAM 워크플로우를 이용할 수 있습니다.

## 키보드 {#keyboard-use} 사용 지원

포인터를 클릭하거나 실행 가능한 많은 사용자 인터페이스 요소도 키보드를 사용하여 연결할 수 있습니다. 키보드를 사용하여 사용자는 UI 요소에 집중할 수 있으며 적절한 작업을 수행할 수 있습니다. 사용자는 키보드 단축키를 사용하여 UI 요소에 집중할 필요 없이 명령 또는 동작을 트리거할 수 있고 키보드를 사용하여 명령을 트리거할 수 있습니다. 예를 들어, 사용자는 키보드를 사용하여 사용자 인터페이스 컨트롤을 탐색하고 `Return`, `Alt + 2` 키보드 단축키를 선택하여 사용자 인터페이스 왼쪽에서 에셋의 타임라인을 열 수 있습니다.

<!-- TBD items:

* The option to toggle between list view and card view exposes relevant info to the screen readers. What about column view option? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* How to open and browse through the profile popup dialog in [!DNL Experience Manager] UI using a keyboard? The navigation does not match the order of visual display of options on the UI. This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’. What about setting preferences and impersonating a user?
* Using the [!DNL Experience Manager] tag browser and operating the options like delete tag? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* Read-only form fields can be focused with the keyboard. Can users tab to these fields to understand the contents and are they able to copy text from the fields?
-->

### [!DNL Assets] {#keyboard-shortcuts}의 키보드 단축키

[!DNL Assets]의 다음 작업은 나열된 키보드 단축키로 작동합니다. [!DNL Experience Manager] 콘솔에 적용되는 대부분의 키보드 단축키는 [!DNL Assets]에도 적용됩니다. 콘솔](/help/sites-authoring/keyboard-shortcuts.md#keyboard-shortcuts)에 대한 [키보드 단축키를 참조하십시오. [키보드 단축키](/help/sites-authoring/keyboard-shortcuts.md#deactivating-keyboard-shortcuts)를 활성화하거나 비활성화하는 방법을 참조하십시오.

| 사용자 인터페이스 또는 시나리오 | 키보드 단축키 | 작업 |
|---|---|---|
| [!DNL Assets] 사용자 인터페이스의 열 보기 | 위쪽 및 아래쪽 화살표 키 | 동일한 계층 구조 내의 파일 및 폴더로 이동합니다. |
| [!DNL Assets] 사용자 인터페이스의 열 보기 | 왼쪽 및 오른쪽 화살표 키 | 현재 폴더 위 또는 아래로 파일과 폴더로 이동합니다. |
| [!DNL Assets]에서 폴더 찾기 | `/` | Omnisearch 상자를 열어 검색을 호출합니다. |
| [!DNL Assets] 콘솔 | ` | 사이드 레일 전환 |
| [!DNL Assets] 콘솔 | `Alt + 1` | 컨텐츠 트리를 엽니다. |
| [!DNL Assets] 콘솔 | `Alt + 2` | [!UICONTROL 내비게이션] 왼쪽 레일을 엽니다. |
| [!DNL Assets] 콘솔 | `Alt + 3` | 선택한 자산의 [!UICONTROL 타임라인]을 표시합니다. |
| [!DNL Assets] 콘솔 | `Alt + 4` | 선택한 자산의 Live Copy 참조를 엽니다. |
| [!DNL Assets] 콘솔 | `Alt + 5` | 선택한 폴더 내에서 검색을 시작합니다. |
| 자산 또는 폴더가 선택됨 | 백스페이스 | 선택한 자산 또는 폴더를 삭제합니다. |
| 자산 또는 폴더가 선택됨 | `p` | 선택한 자산의 속성 페이지를 엽니다. |
| 자산 또는 폴더가 선택됨 | `e` | 선택한 자산을 편집합니다. |
| 자산 또는 폴더가 선택됨 | `m` | 선택한 자산을 이동합니다. |
| 자산 또는 폴더가 선택됨 | `Ctrl + c` | 선택한 자산을 복사합니다. |
| 자산 또는 폴더가 선택됨 | `Esc` | 선택을 취소합니다. |
| 대화 상자가 열리고 포커스에 있음 | `Esc` | 대화 상자를 닫습니다. |
| DAM의 폴더 내부 | `Ctrl + v` | 복사한 자산을 붙여넣습니다. |
| [!DNL Assets] 콘솔 | `Ctrl + A` | 모든 자산을 선택합니다. |
| 자산 속성 페이지 | `Ctrl + S` | 변경 내용을 저장합니다. |
| [!DNL Assets] 콘솔 | `?` | 키보드 단축키 목록을 참조하십시오. |

## 로그인 및 [!DNL Assets] 사용자 인터페이스 {#login} 탐색

사용자는 키보드를 사용하여 로그인 필드로 이동하여 입력하여 로그인할 수 있습니다. 로그인 페이지의 잘못된 사용자 이름 및 암호 조합으로 인한 오류 메시지는 오류가 발생할 때마다 화면 판독기에 의해 표시됩니다.

로그인하면 DAM 사용자는 키보드를 사용하여 [!DNL Assets] 사용자 인터페이스 내에서 탐색할 수 있습니다. 왼쪽 레일, 메뉴, 사용자 프로필, 검색 막대, 파일 및 폴더, 관리 및 구성 설정과 같은 사용자 인터페이스 요소는 키보드를 사용하여 탐색할 수 있습니다. 키보드 탐색 순서는 왼쪽에서 오른쪽 및 위에서 아래로 지정됩니다. 키보드를 사용하여 탐색할 때 포커스가 있으면 화면 판독기에 의해 내레이션이 더 나은 색상 대비로 강조 표시되고 실행 가능한 옵션이 표시됩니다. 해당하는 경우 메뉴에서 초점이 맞춰진 옵션의 상태(예: 확장, 축소 및 혼합 상태)가 화면 판독기에 의해 표시됩니다. 또한 화면 판독기는 모양 또는 인터페이스 배치 대신 실행 가능한 옵션의 목적을 알립니다.

사용자가 메뉴에서 도움말 또는 사용자 프로필 옵션을 확장하면 화면 판독기가 해당 옵션 또는 상태를 알려줍니다. 사용자가 사용자 프로필 옵션을 확장하면 키보드를 사용하여 사용 가능한 옵션을 선택할 수 있습니다. 예를 들어, 관리자는 다른 사용자로 가장할 수 있습니다. 사용자가 [!UICONTROL 도움말] 옵션에서 문자열을 검색하는 경우, 내레이터는 검색이 진행 중임을 나타내는 &quot;도움말 검색&quot;을 발표했습니다.

<!-- TBD: Removing for now. Add a more informative video later. Host it on tv.adobe

![Keyboard navigation of top options in [!DNL Experience Manager] user interface](assets/keyboard-navigation-in-aem.gif)

*Figure: Navigating through the options at the top of [!DNL Experience Manager] user interface using `Tab` key.*
-->

## 에셋을 찾아보고 관련 정보 {#browse} 보기

[!DNL Assets] 사용자 인터페이스에서 사용자는 키보드를 사용하여 DAM 저장소의 기존 디지털 자산 목록을 탐색하거나, 자산을 미리 보거나 다운로드할 수 있습니다. 생성된 표현물을 보고, 보기를 전환하고, 생성된 표현물을 보고, 타임라인과 버전 내역을 보고, 주석과 참조를 보고, 메타데이터를 보고 관리할 수 있습니다.

<!-- TBD: Not sure about the following list items mean:

In [!DNL Experience Manager] header section, when navigating in browse mode, screen reader now announces,
  
  * Suggestions to search in Omnisearch.
  * The state as expanded or collapsed for Solutions, Help, Inbox and User options.
  * The Searching Help status message that is displayed when user enters a search string in Search for Help field under Help option
  * The error message if incorrect value is entered in Impersonate as field under User option and focus correctly moves to the text field (NPR-33804).

Review CQ-4282133 before adding - Close option in a coral-dialog wasn't accessible through keyboard, due to which user cannot trigger close option through keyboard press in version preview dialog. After fix, user can close dialog through close option using keyboard.

* CQ-4273122 - Assets of video/audio type will have aria-label in format "Multimedia player: <Title>" so users relying on screen-reader will get to know that they are video/audio assets.
-->

자산 저장소를 검색할 때 다음 기능을 사용하면 액세서빌러티가 개선됩니다.

* 화면 판독기는 이름 대신 아이콘의 목적 또는 기능을 설명하는 텍스트 대체 요소를 발표했습니다.
* 사용자는 키보드 키를 사용하여 에셋 참조 목록에 있는 대화형 사용자 인터페이스 옵션에 액세스하고 집중할 수 있습니다.
* 목록 보기의 각 행에 있는 요소는 화면 판독기로 동일한 행의 요소로 선언됩니다.
* `Tab` 키를 사용하여 탐색할 때 포커스가 버전 미리 보기의 닫기 옵션으로 이동할 수 있습니다.
* 키보드를 사용하여 검색할 때 강조 표시된 실행 가능한 유저 인터페이스 옵션이 향상된 대비 효과를 통해 보다 눈에 잘 띄는 집중을 할 수 있습니다. 이렇게 하면 초점이 맞춰진 영역을 사용자가 더 쉽게 식별할 수 있게 됩니다.
* 축소판 보기에서 빠른 작업 아이콘을 제거하기 위해 `Esc` 키를 사용해도 마지막 초점이 맞춰진 항목에서 키보드 포커스가 제거되지 않습니다.
* 에셋을 선택하고 `Alt + 4` 키보드 단축키를 선택하면 왼쪽 레일에 있는 [!UICONTROL 참조] 목록이 열립니다. `Tab` 키를 사용하면 0이 아닌 참조 항목을 탐색할 수 있습니다. 0이 아닌 참조 항목만 검색하면 노력과 키 입력도 절약됩니다.
* 자산에 대한 주석은 자산 타임라인에서 사용할 수 있습니다. 키보드 또는 키보드 단축키를 사용하여 왼쪽 레일에 액세스하면 액세스할 수 있습니다.
* [!UICONTROL 키보드] 를  [!DNL Experience Manager] 사용하여 설정 보기를 액세스할 수 있습니다. 사용자는 화살표 키를 사용하여 사용 가능한 카드 크기를 탐색하고 선택 및 탭하여 기존 보기 설정 보기에서 다른 요소를 탐색하고 설정할 수 있습니다.

<!-- TBD: Gradually, as more enhancements are done in these categories, add more content.

## Add and upload digital assets {#upload}

## Configure and administer [!DNL Assets] {#config-admin}

* List the a11y fixes in workflows to configure and administer [!DNL Experience Manager Assets]?
* Some enhancements in Processing profiles creation or application to a folder?
* Some enhancements to metadata properties UI?
-->

## 디지털 자산을 관리합니다 {#manage-assets}

CRUD 작업, 에셋 다운로드, 메타데이터 추가 등과 같은 다양한 에셋 관리 작업에 액세스할 수 있습니다. [!DNL Assets] 화면 판독기 및 키보드와 같은 다양한 보조 기술을 사용하여 작업을 수행할 수 있습니다.

키보드를 사용하여 [저장소를 탐색하고 에셋](https://youtu.be/K3dgqMRQJys)을 다운로드하는 방법에 대한 비디오 데모를 참조하십시오.

마케터 및 관리자와 같은 역할에 의해 일반적으로 수행되는 메타데이터 작업의 경우 다음 기능이 액세서빌러티를 향상시킵니다.

* [!UICONTROL 자산 ] 속성 페이지의 저장 및   닫기 옵션은 키보드를 사용하여 액세스할 수 있습니다.
* 화면 판독기는 자산 [!UICONTROL 속성]의 [!UICONTROL 기본] 탭에서 선택한 태그를 삭제하는 옵션을 발표합니다.
* 사용자는 키보드에서 Datepicker 팝업 대화 상자를 사용할 수 있습니다. Datepicker 사용자 인터페이스 요소는 설정 및 해제 시간을 설정하고 날짜를 선택하는 데 사용됩니다.
* 키보드를 사용하는 드래그 기능은 화면 판독기의 검색 모드에서 [!UICONTROL 메타데이터 스키마 편집기]에서 올바르게 작동합니다.
* 키보드를 사용하여 포커스를 [!UICONTROL 속성] 폴더의 [!UICONTROL 권한] 탭에 있는 [!UICONTROL 폐쇄된 사용자 그룹] 아래의 사용자 또는 그룹 추가 필드로 이동할 수 있습니다.

## 디지털 자산 검색 {#search-assets}

신속하고 원활한 에셋 검색 경험을 통해 콘텐츠 제작 시간을 단축할 수 있습니다. 콘텐츠 속도 사용 사례는 핵심 [!DNL Assets] 기능의 일부입니다. Omnissearch 막대에서 검색을 시작하려면 키보드 단축키 `/`을 사용하거나 화면 판독기와 함께 `Tab`을 사용하여 검색 옵션을 빠르게 찾을 수 있습니다. 스크린 리더는 검색 옵션 ![검색 옵션](assets/do-not-localize/search_icon.png)에 포커스가 있을 때 옵션 이름을 &quot;검색 단추&quot;로 나레이션합니다. 사용자는 `Return`을 선택하여 Omnisearch 상자를 열 수 있습니다. 화면 판독기는 검색 상자에 입력한 키워드에 대해 내레이션할 뿐만 아니라 [!DNL Experience Manager Assets]에서 제공하는 제안에 대해서도 내레이션이 적용됩니다. 사용자는 화살표 키, `Return` 및 `Tab`의 조합을 사용하여 검색을 트리거하는 다양한 옵션에 액세스할 수 있습니다.

검색 기능은 다음 기능을 통해 액세스할 수 있습니다.

* 화면 판독기에서 사용할 수 있는 페이지 제목은 페이지를 자산의 검색 페이지로 식별하는 데 도움이 됩니다.
* 사용자는 Omnisearch 필드 내에서 자산을 검색합니다. 키보드 탐색 또는 키보드 단축키 `/`를 사용하여 열 수 있습니다.
* 사용자는 검색 키워드를 입력한 다음 화살표 키를 사용하여 자동 제안을 선택할 수 있습니다. 강조 표시된 제안은 `Return` 키를 사용하여 선택할 수 있으며 선택한 제안을 위해 자산이 검색됩니다.
* 검색 결과를 필터링할 때 화면 판독기는 [필터] 패널에서 중첩된 모든 표기를 선택하지 않고 첫 번째 수준의 확인란은 선택하지 않고 전체를 클릭한다는 혼합 상태 확인란을 식별하고 발표할 수 있습니다.
* Omnisearch 상자가 닫힌 후 사용자 포커스가 검색 옵션으로 이동합니다.

검색 결과를 필터링할 때:

* 검색 결과 페이지에는 화면 판독기 사용자를 더 잘 이해할 수 있는 정보 제목이 있습니다.
* 화면 판독기는 검색 필터의 옵션을 확장 가능한 아코디언으로 표시합니다.
* 혼합 상태 옵션이 있는 예측자는 화면 판독기에 의해 발표됩니다.

## 자산 공유 {#share-assets}

<!-- TBD: Anything about accessibility in DA, BP? AAL team confirmed that there's no content for AAL a11y on helpx.
-->

자산을 공유할 때 다음 기능을 통해 액세서빌러티를 향상시킬 수 있습니다.

* 사용자는 링크 공유 대화 상자의 검색 및 이메일 주소 추가 필드 내에서 키보드를 사용하여 포커스를 이동할 수 있습니다.

* 링크 공유 대화 상자에서 찾아보기 모드에서 탐색할 때 화면 판독기에서

   * 대화 상자가 로드될 때 표 정보를 분류하지 마십시오.
   * 나열된 모든 제안을 탐색할 수 있습니다.
   * 이메일 주소 및 검색 추가 필드에 대해 표시되는 제안을 나레이트합니다.

## 액세스 가능한 설명서 {#accessible-docs}

[!DNL Experience Manager] 장애가 있는 사용자가 사용할 수 있는 설명서를 제공합니다. Adobe은 템플릿 및 컨텐츠를 계속 개선하는 동안 다음을 통해 컨텐츠를 액세스할 수 있도록 합니다.

* 화면 판독기는 텍스트를 읽을 수 있습니다.
* 이미지와 일러스트레이션에는 대체 텍스트가 있습니다.
* 키보드 탐색을 할 수 있습니다.
* 대비율은 설명서 웹 사이트의 일부 부분을 강조하도록 도와줍니다.

## 피드백 {#a11y-feedback} 제공

피드백을 제공하고 질문하고 액세서빌러티와 관련된 제품 개선 사항을 요청하려면 다음 방법을 사용합니다.

* [www.adobe.com/accessibility/feedback.html](https://www.adobe.com/accessibility/feedback.html)에서 양식을 채웁니다.
* access@adobe.com으로 이메일을 보내주십시오.

>[!MORELIKETHIS]
>
>* [액세스 가능성 기능을 [!DNL Dynamic Media]](/help/assets/accessibility-dm.md) 참조하십시오.
>* [각 서비스 팩 릴리스에서 수행한 개선 사항의 릴리스 노트입니다](/help/release-notes/new-features-latest-service-pack.md).
>* [[!DNL Adobe Experience Manager] 접근성 안내](/help/managing/web-accessibility.md).
>* [Adobe 솔루션에 대한 적합성 보고서(ACR) 및 VPAT 목록](https://www.adobe.com/accessibility/compliance.html).

