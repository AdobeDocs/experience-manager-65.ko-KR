---
title: 기본 처리
description: Adobe Experience Manager 작성 환경을 사용할 때의 기본 처리에 대한 개요입니다. 사이트 콘솔을 기본으로 사용합니다.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: 2981dc20-b2ba-4ea2-a53b-8b5fe526aa9c
source-git-commit: 3885cc51f7e821cdb352737336a29f9c4f0c2f41
workflow-type: tm+mt
source-wordcount: '1167'
ht-degree: 8%

---

# 기본 처리{#basic-handling}

>[!NOTE]
>
>* 이 페이지는 Adobe Experience Manager(AEM) 작성 환경을 사용할 때 기본 처리에 대한 개요를 알 수 있도록 설계되었습니다. **사이트** 콘솔을 기본으로 사용합니다.
>
>* 일부 기능은 일부 콘솔에서 사용할 수 없으며, 추가 기능은 일부 콘솔에서 사용할 수 있습니다. 개별 콘솔 및 관련 기능에 대한 특정 정보는 다른 페이지에서 더 자세히 다룹니다.
>* AEM 전체에서 키보드 단축키를 사용할 수 있습니다. 특히 [콘솔을 사용하고](/help/sites-classic-ui-authoring/author-env-keyboard-shortcuts.md) [페이지를 편집할 때 ](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md)이러한 키보드 단축키를 사용할 수 있습니다.
>

## 시작 화면 {#the-welcome-screen}

클래식 UI는 클릭, 두 번 클릭 및 과 같은 작업을 탐색하고 시작하는 데 잘 알려진 메커니즘을 사용하여 다양한 콘솔을 제공합니다 [컨텍스트 메뉴](#context-menus).

로그인 후 시작 화면이 표시됩니다. 콘솔 및 서비스에 대한 링크 목록을 제공합니다.

![screen_shot_2012-01-30at61745pm](assets/screen_shot_2012-01-30at61745pm.png)

## 콘솔 {#consoles}

기본 콘솔은 다음과 같습니다.

<table>
 <tbody>
  <tr>
   <td><strong>콘솔</strong></td>
   <td><strong>목적</strong></td>
  </tr>
  <tr>
   <td><strong>시작</strong></td>
   <td>AEM의 주요 기능에 대한 개요와 직접 액세스(링크를 통해)를 제공합니다.</td>
  </tr>
  <tr>
   <td><strong>디지털 자산</strong><br /> </td>
   <td>이러한 콘솔에서는 및 <a href="/help/sites-classic-ui-authoring/classicui-assets.md">디지털 자산 관리</a> 이미지, 비디오, 문서 및 오디오 파일 등. 그런 다음 동일한 AEM 인스턴스에서 실행되는 웹 사이트에서 이러한 자산을 사용할 수 있습니다.   </td>
  </tr>
  <tr>
   <td><strong>론치</strong></td>
   <td>이렇게 하면 을(를) 관리하는 데 도움이 됩니다. <a href="/help/sites-classic-ui-authoring/classic-launches.md">론치</a>: 하나 이상의 활성화된 웹 페이지의 향후 릴리스에 대한 콘텐츠를 개발할 수 있습니다.<br /> <i>참고: 터치 사용 UI에서는 참조 레일과 함께 사이트 콘솔에서 동일한 기능을 대부분 사용할 수 있습니다.</i> <i>필요한 경우 도구 콘솔에서 이 콘솔을 사용할 수 있습니다. 작업, 론치 순으로 선택합니다.</i></td>
  </tr>
  <tr>
   <td><strong>받은 편지함 </strong></td>
   <td>종종 다양한 사람들이 워크플로우의 하위 작업에 참여하며 각 사람은 작업을 다음 사람에게 넘기기 전에 단계를 완료해야 합니다. 받은 편지함에서 이러한 작업과 관련된 알림을 볼 수 있습니다. 다음을 참조하십시오 <a href="/help/sites-administering/workflows.md">워크플로우 작업</a>. <br /> </td>
  </tr>
  <tr>
   <td><strong>태그 지정</strong></td>
   <td>태깅 콘솔에서 태그를 관리할 수 있습니다. 태그는 짧은 이름 또는 구문으로, 콘텐츠를 분류하고 주석을 달아 콘텐츠를 쉽게 찾고 구성할 수 있습니다. 자세한 내용은 <a href="/help/sites-classic-ui-authoring/classic-feature-tags.md">태그 사용 및 관리</a>.</td>
  </tr>
  <tr>
   <td><strong>도구</strong></td>
   <td>다음 <a href="/help/sites-administering/tools-consoles.md">도구 콘솔</a> 웹 사이트, 디지털 에셋 및 콘텐츠 저장소의 다른 측면을 관리하는 데 도움이 되는 몇 가지 전문 도구 및 콘솔에 대한 액세스를 제공합니다.</td>
  </tr>
  <tr>
   <td><strong>사용자</strong></td>
   <td>이러한 콘솔에서는 사용자 및 그룹에 대한 액세스 권한을 관리할 수 있습니다. 자세한 내용은 <a href="/help/sites-administering/security.md">사용자 관리 및 보안</a>.<br /> </td>
  </tr>
  <tr>
   <td><strong>웹 사이트</strong></td>
   <td>Sites/Websites 콘솔에서는 <a href="/help/sites-classic-ui-authoring/classic-page-author.md">웹 사이트 생성, 보기 및 관리</a> AEM 인스턴스에서 실행 중입니다. 이러한 콘솔을 통해 웹 사이트 페이지를 만들고, 복사하고, 이동하고, 삭제하고, 워크플로우를 시작하고, 페이지를 활성화(게시)할 수 있습니다. 편집할 페이지를 열 수도 있습니다.<br /> </td>
  </tr>
  <tr>
   <td><strong>워크플로</strong></td>
   <td>워크플로우는 일부 작업을 완료하는 프로세스를 설명하는 일련의 단계를 정의한 것입니다. 종종 여러 사람이 작업에 참여하고 있으며 각 사람은 작업을 다음 사람에게 넘기기 전에 자신의 단계를 완료해야 합니다. 워크플로 콘솔에서는 워크플로 모델을 구축하고 실행 중인 워크플로 인스턴스를 관리할 수 있습니다. 다음을 참조하십시오 <a href="/help/sites-administering/workflows.md">워크플로우 작업</a>.<br /> </td>
  </tr>
 </tbody>
</table>

다음 **웹 사이트** console에는 페이지를 탐색 및 관리할 수 있는 두 개의 창이 있습니다.

* 왼쪽 창

  이는 웹 사이트 및 해당 웹 사이트 내 페이지의 트리 구조를 보여 줍니다.

  프로젝트, 블루프린트 및 자산을 포함한 다른 측면이나 AEM에 대한 정보도 표시합니다.

* 오른쪽 창

  왼쪽 창에서 선택한 위치에 페이지가 표시되며 작업을 수행하는 데 사용할 수 있습니다.

여기에서 다음을 수행할 수 있습니다. [페이지 관리](/help/sites-authoring/managing-pages.md) 도구 모음, 상황에 맞는 메뉴 사용 또는 추가 작업을 위해 페이지 열기

>[!NOTE]
>
>기본 처리는 모든 콘솔에서 동일합니다. 이 부에서는 다음의 물품을 중심으로 분류한다. **웹 사이트** 콘솔 : 작성 시 사용되는 기본 콘솔.

![chlimage_1-9](assets/chlimage_1-9a.png)

## 도움말 액세스 {#accessing-help}

다양한 콘솔(예: 웹 사이트)에서 **도움말** 버튼을 사용할 수 있습니다. 클릭 **도움말** 패키지 공유 또는 설명서 사이트를 엽니다.

![chlimage_1-10](assets/chlimage_1-10a.png)

페이지 편집 시 [sidekick에는 도움말에 액세스하기 위한 버튼도 있습니다](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#accessing-help).

## 웹 사이트 콘솔 탐색 {#navigating-with-the-websites-console}

다음 **웹 사이트** 콘솔에는 콘텐츠 페이지가 트리 구조로 나열됩니다(왼쪽 창). 탐색의 용이성을 위해 트리 구조의 섹션을 필요에 따라 확장(+)하거나 축소(-)할 수 있습니다.

* 왼쪽 창에서 페이지 이름을 클릭하면 다음 작업이 수행됩니다.

   * 오른쪽 창에 하위 페이지를 나열합니다.
   * 왼쪽 창에서 구조를 확장합니다.

     성능상의 이유로 이 작업은 하위 노드의 수에 따라 다릅니다. 표준 설치를 사용하면 다음과 같은 경우 확장 방법이 작동합니다. `30` 또는 더 적은 수의 하위 노드.

* 페이지 이름(왼쪽 창)을 두 번 클릭하면 트리가 확장되지만, 페이지가 열릴 때 이 효과는 명확하지 않습니다.

>[!NOTE]
>
>이 기본값( `30`)은 siteadmin 위젯의 애플리케이션별 구성에서 콘솔별로 변경할 수 있습니다.
>
>siteadmin 노드에서 다음을 수행합니다.
>
>속성 값을 설정합니다.
>`treeAutoExpandMax`
>켜짐:
>`/apps/wcm/core/content/siteadmin`
>
>또는 테마에서 전역적으로:
>값 설정:
>`TREE_AUTOEXPAND_MAX`
>위치:
>`/apps/cq/ui/widgets/themes/default/widgets/wcm/SiteAdmin.js`
>
>다음을 참조하십시오 [CQ 위젯 API의 SiteAdmin](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.SiteAdmin) 을 참조하십시오.

## 웹 사이트 콘솔의 페이지 정보 {#page-information-on-the-websites-console}

의 오른쪽 창 **웹 사이트** console은 페이지에 대한 정보가 포함된 목록 보기를 제공합니다.

![page-info](assets/page-info.png)

다음은 사용할 수 있습니다. 이러한 필드의 하위 집합이 기본값으로 표시됩니다.

<table>
 <tbody>
  <tr>
   <td><strong>열</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td>썸네일</td>
   <td>페이지의 썸네일을 표시합니다.</td>
  </tr>
  <tr>
   <td>제목</td>
   <td>페이지에 나타나는 제목</td>
  </tr>
  <tr>
   <td>이름</td>
   <td>AEM이라는 이름이 페이지를 참조합니다.</td>
  </tr>
  <tr>
   <td>게시됨</td>
   <td>페이지가 게시되었는지 여부를 나타내고 게시 날짜 및 시간을 제공합니다.</td>
  </tr>
  <tr>
   <td>수정됨</td>
   <td>페이지가 수정되었는지 여부를 나타내고 수정 날짜 및 시간을 제공합니다. 수정 사항을 저장하려면 페이지를 활성화해야 합니다.</td>
  </tr>
  <tr>
   <td>Scene7 게시</td>
   <td>페이지가 Scene7에 게시되었는지 여부를 나타냅니다.<br /> </td>
  </tr>
  <tr>
   <td>상태</td>
   <td>페이지가 워크플로의 일부인지 또는 라이브 카피의 일부인지 여부, 페이지가 잠겨 있는지 여부 등 페이지 상태를 나타냅니다.</td>
  </tr>
  <tr>
   <td>노출 횟수</td>
   <td>페이지의 활동을 히트 수로 표시합니다.</td>
  </tr>
  <tr>
   <td>템플릿</td>
   <td>페이지의 기반이 되는 템플릿을 나타냅니다.</td>
  </tr>
  <tr>
   <td>워크플로우</td>
   <td>페이지가 워크플로우에 있는 시기를 나타냅니다.</td>
  </tr>
  <tr>
   <td>잠근 사람</td>
   <td>페이지가 잠겼을 때와 잠근 사용자 계정을 표시합니다.</td>
  </tr>
  <tr>
   <td>Live Copy</td>
   <td>페이지가 라이브 카피의 일부인 시기를 나타냅니다.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>표시되는 열을 선택하려면 열 제목 위로 마우스를 가져갑니다. 드롭다운 메뉴가 표시되며 여기에서 **열** 옵션을 선택합니다.

에서 페이지 옆에 있는 색상 **게시됨** 및 **수정됨** 열은 게시 상태를 나타냅니다.

| **열** | **컬러** | **설명** |
|---|---|---|
| 게시됨 | 녹색 | 게시가 정상적으로 완료되었습니다. 콘텐츠가 게시되었습니다. |
| 게시됨 | 노란색 | 게시가 보류 중입니다. 게시 확인은 시스템에서 아직 받지 못했습니다. |
| 게시됨 | 빨간색 | 게시하지 못했습니다. 게시 인스턴스와 연결되어 있지 않습니다. 콘텐츠가 비활성화되었음을 의미할 수도 있습니다. |
| 게시됨 | *blank* | 이 페이지는 게시된 적이 없습니다. |
| 수정됨 | 파란색 | 마지막 게시 이후 페이지가 수정되었습니다. |
| 수정됨 | *blank* | 이 페이지는 수정되지 않았거나 마지막 게시 이후 수정되지 않았습니다. |

## 컨텍스트 메뉴 {#context-menus}

클래식 UI는 클릭 및 두 번 클릭을 포함하여 작업을 탐색하고 시작하는 데 잘 알려진 메커니즘을 사용합니다. 현재 상황에 따라 다양한 컨텍스트 메뉴(마우스 오른쪽 단추로 열림)도 사용할 수 있습니다.

![chlimage_1-11](assets/chlimage_1-11a.png)
