---
title: ' [!DNL Experience Manager Assets]의 액세스 가능한 기능 및 인터페이스'
description: ' [!DNL Adobe Experience Manager] 6.5 [!DNL Assets] 의 접근성 기능이 장애가 있는 사용자에게 어떤 도움이 되는지 알아보십시오.'
contentOwner: AG
feature: 자산 관리
role: Business Practitioner, Architect, Leader
exl-id: 15555941-99a2-4586-8d7b-b22f3ec17805
source-git-commit: a7a9a31364497ab67d805e45ba4fa03c927828ed
workflow-type: tm+mt
source-wordcount: '1924'
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

# [!DNL Adobe Experience Manager Assets] {#accessibility-in-aem-assets}의 접근성 기능

[!DNL Adobe Experience Manager] 콘텐츠 작성자 및 게시자가 웹에서 놀라운 경험을 제공할 수 있도록 해줍니다. Adobe은 [!DNL Experience Manager]의 액세스 가능성을 개선하여 장애가 있는 작성자를 포함하도록 노력하고 있습니다. 소프트웨어는 모든 유형의 사용자의 요구 사항을 충족하도록 지속적으로 향상되며 시각, 청각, 이동성 또는 기타 장애가 있는 개인을 포함하는 전 세계 표준을 준수합니다.

[!DNL Experience Manager] 는 이 표준을 준수하며 제품의 액세서빌러티 기능에 대해 간략하게 설명하고 규정 준수 수준을 설명하는 적합성 정보를 게시합니다. 액세서빌러티 적합성 보고서는 [!DNL Experience Manager] 사용자가 다양한 표준에 대한 준수 수준을 이해하는 데 도움이 됩니다. [!DNL Assets]에서 향상된 기능을 통해 모든 사용자는 키보드, 화면 판독기, 돋보기 및 기타 보조 기술을 통해 인터페이스를 쉽게 사용할 수 있습니다.

[!DNL Experience Manager] 에서는 다음 표준에 대해 다양한 수준의 지원을 제공합니다.

* [웹 컨텐츠 액세스 가능성 지침(WCAG) 2.1](https://www.w3.org/TR/WCAG/).
* [제508조 개정](https://www.access-board.gov/guidelines-and-standards/communications-and-it/about-the-ict-refresh/final-rule/text-of-the-standards-and-guidelines).
* [Accessibility Initiative - W3C의 WAI-ARIA(Accessible Rich Internet Applications)](https://www.w3.org/WAI/standards-guidelines/aria/).
* [EN 301 549](https://en.wikipedia.org/wiki/EN_301_549).

준수 수준의 세부 정보가 있는 보고서를 읽으려면 [액세서빌러티 준수 보고서](https://www.adobe.com/accessibility/compliance.html) (ACR) 페이지를 참조하십시오.

[!DNL Dynamic Media]에 액세스할 수 있는 방법을 알려면 [!DNL Dynamic Media]](/help/assets/accessibility-dm.md)에서 [액세스 가능성 을 참조하십시오.

## 보조 기술 {#at-support}

장애가 있는 사용자는 웹 컨텐츠에 액세스하고 소프트웨어 제품을 사용하기 위해 하드웨어와 소프트웨어를 자주 사용합니다. 이러한 도구를 보조 기술이라고 합니다. [!DNL Experience Manager Assets] 는 소프트웨어의 핵심 기능을 사용할 때 다음과 같은 유형의 AT(보조 기술)와 작업할 수 있습니다.

* 화면 판독기 및 화면 돋보기.
* 음성 인식 소프트웨어
* 키보드 사용 - 탐색 및 바로 가기.
* 스위치 컨트롤, 새로 고칠 수 있는 점자 디스플레이 및 기타 컴퓨터 입력 장치를 포함한 보조 하드웨어
* UI 확대 도구.

## [!DNL Experience Manager Assets] 액세스 가능한 사용 사례  {#accessible-assets-use-cases}

[!DNL Experience Manager]에서 액세스 가능성 기능은 [!DNL Experience Manager] 사용자 및 해당 고객의 두 가지 주요 요구 사항을 해결합니다.

* 컨텐츠 디자이너와 작성자를 위해 고객 및 웹 사이트 방문자가 차례로 사용하는 액세스 가능한 컨텐츠를 만들고 게시하는 기능이 있습니다. 장애가 있는 사용자는 보조 기술의 도움을 받아 컨텐츠를 사용합니다. 자세한 내용은 [웹 액세스 가능성 지침](/help/managing/web-accessibility.md)을 참조하십시오.
* [!DNL Experience Manager] 또한 사용자와 장애가 있는 관리자가 사용자 인터페이스와 컨트롤에 액세스하여 컨텐츠를 만들고 관리할 수 있습니다. 장애가 있는 사용자는 보조 기술을 사용하여 [!DNL Assets] 기능을 탐색, 사용 및 관리할 수 있습니다.

[!DNL Assets]의 핵심 기능은 이전보다 더 쉽게 액세스할 수 있으며 글로벌 표준에 대한 호환성을 향상하도록 정기적으로 업데이트됩니다. [!DNL Assets]의 CRUD 작업에는 그러한 작업에 적용되는 액세스 가능성이 약간 있습니다. 키보드 단축키, 화면 판독기 텍스트, 색상 대비 등의 도움을 받아 자산 추가, 관리, 검색 및 배포와 같은 DAM 워크플로우에 액세스할 수 있습니다.

## 키보드 사용 지원 {#keyboard-use}

포인터를 사용하여 클릭하거나 실행할 수 있는 많은 사용자 인터페이스 요소도 키보드를 사용하여 참여할 수 있습니다. 키보드를 사용하여 사용자는 UI 요소에 초점을 맞추고 적절한 작업을 수행할 수 있습니다. 사용자는 키보드 단축키를 사용하여 UI 요소에 포커스를 설정하고 키보드를 사용하여 명령 또는 작업을 트리거할 필요가 없습니다. 예를 들어, 사용자는 키보드를 사용하여 사용자 인터페이스 컨트롤로 이동하여 `Return` 을 선택하고 `Alt + 2` 키보드 단축키를 선택하여 사용자 인터페이스 왼쪽에 있는 자산의 타임라인을 열 수 있습니다.

<!-- TBD items:

* The option to toggle between list view and card view exposes relevant info to the screen readers. What about column view option? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* How to open and browse through the profile popup dialog in [!DNL Experience Manager] UI using a keyboard? The navigation does not match the order of visual display of options on the UI. This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’. What about setting preferences and impersonating a user?
* Using the [!DNL Experience Manager] tag browser and operating the options like delete tag? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* Read-only form fields can be focused with the keyboard. Can users tab to these fields to understand the contents and are they able to copy text from the fields?
-->

### [!DNL Assets] {#keyboard-shortcuts}의 키보드 단축키

[!DNL Assets]의 다음 작업은 나열된 키보드 단축키로 작동합니다. [!DNL Experience Manager] 콘솔에 적용되는 대부분의 키보드 단축키는 [!DNL Assets]에도 적용됩니다. 콘솔용 [키보드 단축키](/help/sites-authoring/keyboard-shortcuts.md#keyboard-shortcuts)를 참조하십시오. [키보드 단축키를 활성화 또는 비활성화하는 방법을 참조하십시오](/help/sites-authoring/keyboard-shortcuts.md#deactivating-keyboard-shortcuts).

| 사용자 인터페이스 또는 시나리오 | 키보드 단축키 | 작업 |
|---|---|---|
| [!DNL Assets] 사용자 인터페이스의 열 보기 | 위쪽 및 아래쪽 화살표 키 | 동일한 계층 내에서 파일 및 폴더로 이동합니다. |
| [!DNL Assets] 사용자 인터페이스의 열 보기 | 왼쪽 및 오른쪽 화살표 키 | 현재 폴더 위 또는 아래로 파일 및 폴더로 이동합니다. |
| [!DNL Assets]에서 폴더 찾아보기 | `/` | Omnisearch 상자를 열어 검색을 호출합니다. |
| [!DNL Assets] 콘솔 | ` | 사이드 레일 전환 |
| [!DNL Assets] 콘솔 | `Alt + 1` | 컨텐츠 트리를 엽니다. |
| [!DNL Assets] 콘솔 | `Alt + 2` | [!UICONTROL 탐색] 왼쪽 레일을 엽니다. |
| [!DNL Assets] 콘솔 | `Alt + 3` | 선택한 자산의 [!UICONTROL 타임라인]을 표시합니다. |
| [!DNL Assets] 콘솔 | `Alt + 4` | 선택한 자산의 Live Copy 참조를 엽니다. |
| [!DNL Assets] 콘솔 | `Alt + 5` | 선택한 폴더 내에서 검색 및 검색을 시작합니다. |
| 자산 또는 폴더를 선택함 | 백스페이스 | 선택한 자산 또는 폴더를 삭제합니다. |
| 자산 또는 폴더를 선택함 | `p` | 선택한 자산의 속성 페이지를 엽니다. |
| 자산 또는 폴더를 선택함 | `e` | 선택한 자산을 편집합니다. |
| 자산 또는 폴더를 선택함 | `m` | 선택한 자산을 이동합니다. |
| 자산 또는 폴더를 선택함 | `Ctrl + c` | 선택한 자산을 복사합니다. |
| 자산 또는 폴더를 선택함 | `Esc` | 선택 항목을 취소합니다. |
| 대화 상자가 열리고 포커스가 있습니다 | `Esc` | 닫기 대화 상자. |
| DAM의 폴더 내부 | `Ctrl + v` | 복사한 자산을 붙여넣습니다. |
| [!DNL Assets] 콘솔 | `Ctrl + A` | 모든 자산을 선택합니다. |
| 자산 속성 페이지 | `Ctrl + S` | 변경 사항을 저장합니다. |
| [!DNL Assets] 콘솔 | `?` | 키보드 단축키 목록을 참조하십시오. |

## 로그인 및 [!DNL Assets] 사용자 인터페이스 탐색 {#login}

사용자는 키보드를 사용하여 로그인 필드로 이동하고 필드를 입력하여 로그인할 수 있습니다. 로그인 페이지의 잘못된 사용자 이름 및 암호 조합으로 인한 오류 메시지는 오류가 발생할 때마다 화면 판독기에 표시됩니다.

로그인한 후 DAM 사용자는 키보드를 사용하여 [!DNL Assets] 사용자 인터페이스 내에서 탐색할 수 있습니다. 왼쪽 레일, 메뉴, 사용자 프로필, 검색 막대, 파일 및 폴더, 관리 및 구성 설정과 같은 사용자 인터페이스 요소는 키보드를 사용하여 탐색할 수 있습니다. 키보드 탐색 순서는 왼쪽에서 오른쪽 및 위에서 아래로 이동합니다. 키보드를 사용하여 탐색할 때 포커스가 있으면 강조 표시된 작업 가능한 옵션이 더 나은 색상 대비로 강조 표시되고 화면 판독기에 의해 내레이션이 적용됩니다. 적절한 경우 메뉴의 포커스가 있는 옵션(예: 확장, 축소 및 혼합 상태)의 상태가 화면 판독기에 표시됩니다. 또한 화면 판독기는 모양이나 인터페이스 배치 대신 실행 가능한 옵션의 목적을 알려줍니다.

사용자가 메뉴에서 도움말 또는 사용자 프로필 옵션을 확장하면 화면 판독기에서 해당 옵션 또는 상태를 알려줍니다. 사용자가 사용자 프로필 옵션을 확장하는 경우 키보드를 사용하여 사용 가능한 옵션을 선택할 수 있습니다. 예를 들어 관리자는 다른 사용자를 가장할 수 있습니다. 사용자가 [!UICONTROL 도움말] 옵션에서 문자열을 검색하는 경우 내레이터는 &quot;검색 도움말&quot;을 발표하여 검색이 진행 중임을 나타냅니다.

<!-- TBD: Removing for now. Add a more informative video later. Host it on tv.adobe

![Keyboard navigation of top options in [!DNL Experience Manager] user interface](assets/keyboard-navigation-in-aem.gif)

*Figure: Navigating through the options at the top of [!DNL Experience Manager] user interface using `Tab` key.*
-->

## 자산 찾아보기 및 관련 정보 보기 {#browse}

[!DNL Assets] 사용자 인터페이스에서 사용자는 키보드를 사용하여 DAM 리포지토리의 기존 디지털 자산 목록을 탐색하거나, 자산을 미리 보거나, 다운로드하고, 생성된 표현물, 보기 전환, 생성된 표현물 보기, 타임라인 및 버전 기록 보기, 주석 및 참조 보기, 메타데이터 보기 및 관리 등을 수행할 수 있습니다.

<!-- TBD: Not sure about the following list items mean:

In [!DNL Experience Manager] header section, when navigating in browse mode, screen reader now announces,
  
  * Suggestions to search in Omnisearch.
  * The state as expanded or collapsed for Solutions, Help, Inbox and User options.
  * The Searching Help status message that is displayed when user enters a search string in Search for Help field under Help option
  * The error message if incorrect value is entered in Impersonate as field under User option and focus correctly moves to the text field (NPR-33804).

Review CQ-4282133 before adding - Close option in a coral-dialog wasn't accessible through keyboard, due to which user cannot trigger close option through keyboard press in version preview dialog. After fix, user can close dialog through close option using keyboard.

* CQ-4273122 - Assets of video/audio type will have aria-label in format "Multimedia player: <Title>" so users relying on screen-reader will get to know that they are video/audio assets.
-->

자산 저장소를 검색할 때 다음 기능이 액세스 가능성을 개선합니다.

* 화면 판독기는 이름 대신 아이콘의 목적이나 기능을 설명하는 텍스트 대체 요소를 알려줍니다.
* 사용자는 키보드 키를 사용하여 자산 참조 목록에서 대화형 사용자 인터페이스 옵션에 액세스하고 포커스를 둘 수 있습니다.
* 목록 보기의 각 행에 있는 요소는 화면 판독기에서 동일한 행의 요소로 표시됩니다.
* `Tab` 키를 사용하여 탐색할 때 포커스가 버전 미리 보기에서 닫기 옵션으로 이동할 수 있습니다.
* 키보드를 사용하여 검색할 때 강조 표시된 실행 가능한 사용자 인터페이스 옵션에는 향상된 대비 기능이 있는 더 눈에 띄는 시각적 포커스가 있습니다. 따라서 사용자가 초점을 맞춘 영역을 보다 쉽게 식별할 수 있습니다.
* 축소판 보기에서 빠른 작업 아이콘을 제거하려면 `Esc` 키를 사용해도 마지막 포커스가 있는 항목에서 키보드 포커스가 제거되지 않습니다.
* 자산을 선택한 상태에서 `Alt + 4` 키보드 단축키를 선택하면 왼쪽 레일에서 [!UICONTROL 참조] 목록이 열립니다. `Tab` 키를 사용하면 사용자가 0이 아닌 참조 항목을 탐색할 수 있습니다. 0이 아닌 참조 항목만 탐색하면 노력과 키 입력도 절약됩니다.
* 자산에 대한 설명은 자산 타임라인에서 사용할 수 있습니다. 키보드 또는 키보드 단축키를 사용하여 왼쪽 레일에 액세스하면 액세스할 수 있습니다.
* [!UICONTROL 보기 ] 설정 [!DNL Experience Manager] 은 키보드를 사용하여 액세스할 수 있습니다. 사용자는 화살표 키를 사용하여 사용 가능한 카드 크기를 탐색하고 를 선택하고 탭하여 기존 보기 설정 보기에서 다른 요소를 탐색하고 설정할 수 있습니다.

<!-- TBD: Gradually, as more enhancements are done in these categories, add more content.

## Add and upload digital assets {#upload}

## Configure and administer [!DNL Assets] {#config-admin}

* List the a11y fixes in workflows to configure and administer [!DNL Experience Manager Assets]?
* Some enhancements in Processing profiles creation or application to a folder?
* Some enhancements to metadata properties UI?
-->

## 디지털 자산을 관리합니다 {#manage-assets}

CRUD 작업, 자산 다운로드, 메타데이터 추가와 같은 많은 자산 관리 작업은 다양한 수준에서 액세스할 수 있습니다. [!DNL Assets] 화면 판독기 및 키보드 등 다양한 보조 기술을 사용하여 작업을 수행할 수 있습니다.

키보드를 사용하여 [저장소를 탐색하고 자산](https://youtu.be/K3dgqMRQJys)을 다운로드하는 방법에 대한 비디오 데모를 참조하십시오.

일반적으로 마케터 및 관리자와 같은 역할이 수행하는 메타데이터 작업의 경우 다음 기능은 액세스 가능성을 개선합니다.

* [!UICONTROL 이제 ] 키보드를 사용하여 자산 속성   페이지의 저장 및 닫기 옵션에 액세스할 수 있습니다.
* 화면 판독기는 자산 [!UICONTROL 속성]의 [!UICONTROL 기본] 탭에서 선택한 태그를 삭제하는 옵션을 알려줍니다.
* 사용자는 키보드에서 Datepicker 팝업 대화 상자를 사용할 수 있습니다. Datepicker 사용자 인터페이스 요소는 설정 및 해제 시간을 설정하고 날짜를 선택하는 데 사용됩니다.
* 키보드를 사용하는 드래그 기능은 화면 판독기의 검색 모드에서 [!UICONTROL 메타데이터 스키마 편집기]에서 올바르게 작동합니다.
* 사용자는 키보드를 사용하여 [!UICONTROL 속성] 폴더의 [!UICONTROL 권한] 탭에서 [!UICONTROL 닫힌 사용자 그룹] 아래의 사용자 또는 그룹 추가 필드로 포커스를 이동할 수 있습니다.

## 디지털 자산 검색 {#search-assets}

빠르고 원활한 자산 검색 환경을 통해 컨텐츠 속도를 높일 수 있습니다. 컨텐츠 속도 사용 사례는 코어 [!DNL Assets] 기능의 일부입니다. Omnisearch 막대에서 검색을 시작하려면 키보드 단축키 `/` 를 사용하거나 화면 판독기와 함께 `Tab` 를 사용하여 검색 옵션을 빠르게 찾을 수 있습니다. 화면 판독기는 검색 옵션 ![검색 옵션](assets/do-not-localize/search_icon.png)에 포커스가 있을 때 옵션 이름을 &quot;검색 단추&quot;로 내레이션합니다. 사용자는 `Return` 을 선택하여 Omnisearch 상자를 열 수 있습니다. 화면 판독기는 검색 상자에 입력한 키워드에 내레이션뿐만 아니라 [!DNL Experience Manager Assets]에서 제공하는 제안에 대해서도 내레이션합니다. 사용자는 화살표 키, `Return` 및 `Tab` 조합을 사용하여 검색을 트리거하는 다양한 옵션에 액세스할 수 있습니다.

검색 기능은 다음 기능으로 액세스할 수 있습니다.

* 화면 판독기에서 사용할 수 있는 페이지 제목은 페이지를 자산의 검색 페이지로 식별하는 데 도움이 됩니다.
* 사용자는 Omnisearch 필드 내에서 자산을 검색합니다. 키보드 탐색 또는 키보드 단축키 `/` 를 사용하여 열 수 있습니다.
* 사용자는 검색 키워드 입력을 시작한 다음 화살표 키를 사용하여 자동 제안 을 선택할 수 있습니다. `Return` 키를 사용하여 강조 표시된 제안을 선택할 수 있으며 선택한 제안에 대해 자산이 검색됩니다.
* 화면 판독기는 검색 결과를 필터링할 때 필터 패널에서 혼합 상태 확인란(중첩된 모든 확인란을 선택하지 않은 경우 첫 번째 수준의 확인란을 선택하지 않고 나머지도 선택되지 않음)을 식별하고 알릴 수 있습니다.
* Omnisearch 상자가 닫히면 사용자 포커스가 검색 옵션으로 이동합니다.

검색 결과를 필터링할 때:

* 검색 결과 페이지에는 화면 판독기 사용자를 더 잘 이해할 수 있는 유용한 제목이 있습니다.
* 화면 판독기는 검색 필터의 옵션을 확장 가능한 아코디언으로 알려줍니다.
* 혼합 상태 옵션이 있는 설명은 화면 판독기에 표시됩니다.

## 자산 공유 {#share-assets}

<!-- TBD: Anything about accessibility in DA, BP? AAL team confirmed that there's no content for AAL a11y on helpx.
-->

자산을 공유할 때 다음 기능을 사용하면 액세스 가능성이 개선됩니다.

* 사용자는 링크 공유 대화 상자의 검색 및 이메일 주소 추가 필드 내에서 키보드를 사용하여 포커스를 이동할 수 있습니다.

* 링크 공유 대화 상자의 검색 모드에서 탐색할 때 화면 판독기에서

   * 대화 상자가 로드될 때 테이블 정보에 내레이션이 적용되지 않습니다.
   * 나열된 모든 제안 항목으로 이동할 수 있습니다.
   * 이메일 주소 추가 및 검색 필드에 대해 표시된 제안에 내레이션이 적용됩니다.

## 액세스 가능한 설명서 {#accessible-docs}

[!DNL Experience Manager] 장애가 있는 사용자가 사용할 수 있는 액세스 가능한 설명서를 제공합니다. Adobe은 템플릿 및 컨텐츠를 계속 개선하는 동안 다음을 통해 컨텐츠 서비스에 액세스할 수 있도록 합니다.

* 화면 판독기에서 텍스트를 읽을 수 있습니다.
* 이미지 및 그림에는 대체 텍스트를 사용할 수 있습니다.
* 키보드 탐색을 할 수 있습니다.
* 대비율은 설명서 웹 사이트의 일부 부분을 강조 표시하는 데 도움이 됩니다.

## 피드백 제공 {#a11y-feedback}

피드백을 제공하고, 질문을 하고, 접근성과 관련된 제품 개선 사항을 요청하려면 다음 방법을 사용하십시오.

* [www.adobe.com/accessibility/feedback.html](https://www.adobe.com/accessibility/feedback.html)에서 양식을 채웁니다.
* access@adobe.com으로 이메일을 보내주십시오.

>[!MORELIKETHIS]
>
>* [ [!DNL Dynamic Media]](/help/assets/accessibility-dm.md)의 접근성 기능.
>* [각 서비스 팩 릴리스에서 수행된 개선 사항에 대한 릴리스 노트입니다](/help/release-notes/new-features-latest-service-pack.md).
>* [[!DNL Adobe Experience Manager] 액세스 가능성 지침](/help/managing/web-accessibility.md).
>* [Adobe 솔루션에 대한 적합성 보고서(ACR) 및 VPAT 목록](https://www.adobe.com/accessibility/compliance.html).

