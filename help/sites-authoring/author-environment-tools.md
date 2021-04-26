---
title: 작성 - 환경 및 도구
seo-title: 작성 - 환경 및 도구
description: AEM의 작성 환경에서는 컨텐츠를 구성하고 편집하기 위한 다양한 메커니즘을 제공합니다
seo-description: AEM의 작성 환경에서는 컨텐츠를 구성하고 편집하기 위한 다양한 메커니즘을 제공합니다
uuid: 23a8aa93-b3d2-423b-b402-9e5f3f273d9a
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: f488ba79-5bda-46e9-9c15-9a8c3dbfa2ce
docset: aem65
exl-id: 3b3c118b-ca35-484b-a62e-7bec98953123
translation-type: tm+mt
source-git-commit: 1cef6f87fa66fd78d439c23e6ac907f9531b8fd6
workflow-type: tm+mt
source-wordcount: '2239'
ht-degree: 97%

---

# 작성 - 환경 및 도구{#authoring-the-environment-and-tools}

AEM의 작성 환경에서는 컨텐츠를 구성하고 편집하기 위한 다양한 메커니즘을 제공합니다. 제공된 도구는 다양한 콘솔 및 페이지 편집기에서 액세스됩니다.

## 사이트 관리 {#managing-your-site}

**사이트** 콘솔에서는 헤더 막대, 도구 모음, 작업 아이콘(선택한 리소스에 대해 적용 가능), 탐색 표시 및 (선택 시) 보조 레일(예: 타임라인 및 참조)을 사용하여 웹 사이트를 탐색 및 관리할 수 있습니다.

예를 들면 열 보기에서 다음을 수행합니다.

![ateat-01](assets/ateat-01.png)

## 페이지 컨텐츠 편집 {#editing-page-content}

페이지 편집기로 페이지를 편집할 수 있습니다. 예:

`https://localhost:4502/editor.html/content/we-retail/us/en/equipment.html`

![ateat-02](assets/ateat-02.png)

>[!NOTE]
>
>편집하기 위해 페이지를 처음 열면, 일련의 슬라이드를 통해 기능을 둘러볼 수 있습니다.
>
>원할 경우 둘러보기를 건너뛰고 언제든지 **페이지 정보** 메뉴에서 선택하여 반복할 수도 있습니다.

## 도움말 액세스 {#accessing-help}

페이지를 편집할 때 다음 위치에서 **도움말**&#x200B;에 액세스할 수 있습니다.

* [**페이지 정보**](/help/sites-authoring/editing-page-properties.md#page-properties) 선택기: 소개 슬라이드(편집기에 처음 액세스할 때 표시됨)가 표시됩니다.
* 특정 구성 요소의 [구성](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) 대화 상자(대화 상자 도구 모음의 ? 아이콘 사용): 상황에 맞는 도움말이 표시됩니다.

추가 [도움말 관련 리소스는 콘솔에서 사용할 수 있습니다](/help/sites-authoring/basic-handling.md#accessing-help).

## 구성 요소 브라우저 {#components-browser}

구성 요소 브라우저에는 현재 페이지에서 사용할 수 있는 모든 구성 요소가 표시됩니다. 이 구성 요소들은 적절한 위치로 드래그한 다음 편집하여 컨텐츠를 추가할 수 있습니다.

구성 요소 브라우저는 사이드 패널 내의 탭입니다([자산 브라우저](/help/sites-authoring/author-environment-tools.md#assets-browser) 및 [컨텐츠 트리](/help/sites-authoring/author-environment-tools.md#content-tree)와 함께 있음). 사이드 패널을 열려면(또는 닫으려면) 도구 모음의 왼쪽 상단에 있는 아이콘을 사용합니다.

![ateat-03](assets/ateat-03.png)

사이드 패널을 열 때는(왼쪽에서) 밀어서 열게 됩니다. 필요한 경우 **구성 요소** 탭을 선택하고 연 후에는 페이지에 대해 사용 가능한 모든 구성 요소를 찾아볼 수 있습니다.

실제 모양 및 처리는 사용하는 장치 유형에 따라 달라집니다.

>[!NOTE]
>
>너비가 1024px 미만이면 모바일 장치가 검색됩니다. 소형 데스크톱 창에 해당할 수도 있습니다.

* **모바일 장치(예: iPad)**

   구성 요소 브라우저는 편집되는 페이지를 완전히 포함합니다.

   구성 요소를 페이지에 추가하려면 필요한 구성 요소를 길게 터치하고 오른쪽으로 이동합니다. 구성 요소 브라우저가 닫히고 페이지가 다시 표시되어 구성 요소를 배치할 수 있습니다.

   ![ateat-04](assets/ateat-04.png)

* **데스크탑 장치**

   창의 왼쪽에 구성 요소 브라우저가 열립니다.

   구성 요소를 페이지에 추가하려면 필요한 구성 요소를 클릭하고 필요한 위치로 끕니다.

   ![ateat-05](assets/ateat-05.png)

   구성 요소는 다음으로 표시됩니다.

   * 구성 요소 이름
   * 구성 요소 그룹(회색)
   * 아이콘 또는 약어

      * 표준 구성 요소의 아이콘은 단색입니다.
      * 약어는 항상 구성 요소 이름의 첫 번째 두 문자입니다.

   **구성 요소** 브라우저의 맨 위 도구 모음에서 다음 작업을 수행할 수 있습니다.

   * 구성 요소를 이름별로 필터링합니다.
   * 드롭다운 선택을 사용하여 표시를 특정 그룹으로 제한합니다.

   구성 요소에 대한 자세한 설명을 보려면 **구성 요소** 브라우저의 구성 요소 옆에 있는 정보 아이콘(있는 경우)을 클릭하거나 탭할 수 있습니다. 예: **레이아웃 컨테이너**

   ![ateat-06](assets/ateat-06.png)

   사용 가능한 구성 요소에 대한 자세한 내용은 [구성 요소 콘솔](/help/sites-authoring/default-components-console.md)을 참조하십시오.

## 자산 브라우저 {#assets-browser}

자산 브라우저에는 현재 페이지에서 직접 사용할 수 있는 모든 [자산](/help/assets/home.md)이 표시됩니다.

자산 브라우저는 사이드 패널 내의 탭이며 [구성 요소 브라우저](/help/sites-authoring/author-environment-tools.md#components-browser) 및 [컨텐츠 트리](/help/sites-authoring/author-environment-tools.md#content-tree)와 함께 있습니다. 사이드 패널을 열려면(또는 닫으려면) 도구 모음의 왼쪽 상단에 있는 아이콘을 사용합니다.

![ateat-03-1](assets/ateat-03-1.png)

사이드 패널을 열 때는 왼쪽에서 밀어서 열게 됩니다. 필요한 경우 **자산** 탭을 선택합니다.

![ateat-07](assets/ateat-07.png)

자산 브라우저가 열려 있으면 페이지에 사용 가능한 모든 자산을 검색할 수 있습니다. 필요하면 목록을 확장하는 데 스크롤을 무제한으로 사용합니다.

![ateat-08](assets/ateat-08.png)

자산을 페이지에 추가하려면 선택한 후 필요한 위치로 끕니다. 다음과 같은 경우일 수 있습니다.

* 해당 유형의 기존 구성 요소


   * 예를 들어 유형 이미지의 자산을 이미지 구성 요소로 끌 수 있습니다.

* 해당 유형의 새 구성 요소를 만들기 위한 단락 시스템의 [자리 표시자](/help/sites-authoring/editing-content.md#component-placeholder) 


   * 예를 들어 유형 이미지의 자산을 단락 시스템으로 드래그하여 이미지 구성 요소를 만들 수 있습니다.

>[!NOTE]
>
>특정 자산 및 구성 요소 유형에 사용할 수 있습니다. 자세한 내용은 [자산 브라우저를 사용하여 구성 요소 삽입](/help/sites-authoring/editing-content.md#inserting-a-component-using-the-assets-browser)을 참조하십시오.

자산 브라우저의 상단 도구 모음에서 다음 기준에 따라 자산을 필터링할 수 있습니다.

* 이름
* 경로
* 자산 유형(예: 이미지, 원고, 문서, 비디오, 페이지, 단락, 제품)
* 방향(세로, 가로, 정사각형) 및 스타일(색상, 단색, 회색)과 같은 자산 특성

   * 특정 자산 유형에만 사용할 수 있음

실제 모양 및 처리는 사용하는 장치 유형에 따라 달라집니다.

>[!NOTE]
>
>모바일 장치는 폭이 1024픽셀 미만인 경우 감지됩니다(즉, 작은 데스크톱 창에서도 감지됨).

* **iPad와 같은 모바일 장치**

   자산 브라우저는 편집되는 페이지를 완전히 포함합니다.

   자산을 페이지에 추가하려면 필요한 자산을 길게 터치하고 오른쪽으로 이동합니다. 자산 브라우저가 닫히고 페이지가 다시 표시되어 필요한 구성 요소에 자산을 추가할 수 있습니다.

   ![ateat-09](assets/ateat-09.png)

* **데스크탑 장치**

   창의 왼쪽에 자산 브라우저가 열립니다.

   자산을 페이지에 추가하려면 필요한 자산을 클릭하고 필요한 구성 요소 또는 위치로 드래그합니다.

   ![ateat-10](assets/ateat-10.png)

자산을 빠르게 변경해야 하는 경우, 자산의 이름 옆에 있는 편집 아이콘을 클릭하여 [자산 편집기](/help/assets/manage-assets.md)를 자산 브라우저에서 직접 시작할 수 있습니다.

![](do-not-localize/screen_shot_2018-03-22at142448.png)

## 컨텐츠 트리 {#content-tree}

**컨텐츠 트리**&#x200B;는 계층 구조의 페이지에 있는 모든 구성 요소에 대한 개요를 제공하여 페이지 작성 방법을 한눈에 볼 수 있습니다.

컨텐츠 트리는 구성 요소 및 자산 브라우저와 함께 있는 측면 패널 내의 탭입니다. 사이드 패널을 열려면(또는 닫으려면) 도구 모음의 왼쪽 상단에 있는 아이콘을 사용합니다.

![](do-not-localize/screen_shot_2018-03-22at142042.png)

사이드 패널을 열 때는(왼쪽에서) 밀어서 열게 됩니다. 필요한 경우 **컨텐츠 트리** 탭을 선택하십시오. 열리면 페이지나 템플릿의 트리 보기 표시를 확인하여 컨텐츠가 계층 구조로 구성되는 방식을 쉽게 이해할 수 있습니다. 또한 복잡한 페이지에서는 페이지의 구성 요소 간에 쉽게 이동할 수 있습니다.

![ateat-11](assets/ateat-11.png)

페이지는 동일한 유형의 여러 구성 요소로 쉽게 구성할 수 있으므로 컨텐츠(구성 요소) 트리에는 구성 요소 유형의 이름(검은색) 뒤에 설명 텍스트(회색)가 표시됩니다. 설명 텍스트는 제목 또는 텍스트와 같은 구성 요소의 공통된 특성에서 가져옵니다.

구성 요소 유형은 사용자 언어로 표시되는 반면 구성 요소 설명 텍스트는 페이지 언어로 제공됩니다.

구성 요소 옆에 있는 V자형 화살표를 클릭하면 해당 수준을 축소하거나 확장합니다.

![screen_shot_2018-03-22at142559](assets/screen_shot_2018-03-22at142559.png)

>[!NOTE]
>
>모바일 장치(브라우저 너비가 1024px 미만인 경우)에서 페이지를 편집하는 경우, 컨텐츠 트리를 사용할 수 없습니다.

[구성 요소]를 클릭하면 페이지 편집기에서 구성 요소가 강조 표시됩니다. 사용 가능한 작업은 페이지 상태에 따라 다릅니다.

* 예: 기본 페이지

   `https://localhost:4502/editor.html/content/we-retail/language-masters/en/equipment.html`

   ![ateat-12](assets/ateat-12.png)

   트리에서 클릭한 구성 요소가 편집 가능한 경우 이름의 오른쪽에 공구 모양 아이콘이 표시됩니다. 이 아이콘을 클릭하면 구성 요소의 편집 대화 상자가 바로 시작됩니다.

   ![](do-not-localize/screen_shot_2018-03-22at142725.png)

* 또는 구성 요소가 다른 페이지에서 상속되는 [Live Copy](/help/sites-administering/msm.md)의 일부인 페이지: 예:

   `https://localhost:4502/editor.html/content/we-retail/us/en/equipment.html`

   ![ateat-13](assets/ateat-13.png)

## 조각 - 관련 컨텐츠 브라우저 {#fragments-associated-content-browser}

페이지에 컨텐츠 조각이 포함되어 있으면 [관련 컨텐츠 브라우저](/help/sites-authoring/content-fragments.md#using-associated-content)에 액세스할 수도 있습니다.

## 참조 {#references}

**참조**&#x200B;에는 선택한 페이지에 대한 연결 내용이 표시됩니다.

* 블루프린트
* 론치
* Live copy
* 언어 복사
* 수신 링크
* 참조 구성 요소 사용: 빌린 컨텐츠 및 빌려준 컨텐츠
* 제품 페이지에 대한 참조(커머스 - 제품 콘솔)

필수 콘솔을 연 다음 필수 리소스로 이동하고 다음을 사용하여 **참조**&#x200B;를 엽니다.

![screen_shot_2018-03-22at153653](assets/screen_shot_2018-03-22at153653.png)

필수 리소스와 관련이 있는 참조 유형 목록을 표시하려면 [관련 리소스를 선택](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)합니다.

![ateat-22](assets/ateat-22.png)

자세한 내용을 보려면 적절한 참조 유형을 선택합니다. 특정 상황에서 다음을 비롯한 특정 참조를 선택하면 추가 작업을 사용할 수 있습니다.

* **수신 링크**: 페이지를 참조하는 페이지 목록과 함께, 특정 링크를 선택할 때 그러한 페이지 중 하나를 **편집**&#x200B;하기 위해 직접 액세스할 수 있는 권한 제공

* **참조** 구성 요소를 사용하여 빌린 컨텐츠와 빌려준 컨텐츠의 인스턴스: 여기서 참조하는/참조한 페이지로 이동할 수 있음

* [제품 페이지에 대한 참조](/help/commerce/cif-classic/administering/generic.md#showing-product-references)(커머스 - 제품 콘솔에서 사용 가능)
* [론치](/help/sites-authoring/launches.md): 관련 론치에 대한 액세스 권한 제공
* [](/help/sites-administering/msm.md)LiveCopy: 선택한 리소스를 기반으로 하는 모든 LiveCopy 경로 표시 
* [세부](/help/sites-administering/msm-best-practices.md) 사항과 다양한 작업을 제공하는 블루프린트
* [언어 사본](/help/sites-administering/tc-manage.md#creating-translation-projects-using-the-references-panel): 세부 사항 및 여러 작업 제공

예를 들어 참조 구성 요소 내에서 끊어진 참조를 수정할 수 있습니다.

![ateat-14](assets/ateat-14.png)

## 이벤트 - 타임라인 {#events-timeline}

해당 리소스(예: **사이트** 콘솔의 페이지 또는 **자산**&#x200B;콘솔의 자산)에 대해 타임라인을 사용하여 [선택한 항목에 대한 최근 활동을 표시할 수 있습니다](/help/sites-authoring/basic-handling.md#timeline).

필수 콘솔을 연 다음 필수 리소스로 이동하고 다음을 사용하여 **타임라인**&#x200B;을 엽니다.

![ateat-15](assets/ateat-15.png)

[필수 리소스를 선택](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)한 다음 **모두 표시**&#x200B;나 **활동**&#x200B;을 선택하여 선택한 리소스에 대한 모든 최근 작업을 나열합니다.

![ateat-16](assets/ateat-16.png)

## 페이지 정보 {#page-information}

페이지 정보(이퀄라이저 아이콘)에서는 마지막 편집과 마지막 게시에 대한 세부 사항을 보여 주는 메뉴가 열립니다. 페이지, 사이트 및 인스턴스의 특성에 따라 다음 옵션을 사용할 수 있습니다.

![ateat-17](assets/ateat-17.png)

* [속성 열기](/help/sites-authoring/editing-page-properties.md)
* [페이지 롤아웃](/help/sites-administering/msm.md#msm-from-the-ui)
* [워크플로우 시작](/help/sites-authoring/workflows-applying.md#starting-a-workflow-from-the-page-editor)
* [페이지 잠금](/help/sites-authoring/editing-content.md#locking-a-page)
* [페이지 게시](/help/sites-authoring/publishing-pages.md#main-pars-title-10)
* [페이지 게시 취소](/help/sites-authoring/publishing-pages.md#main-pars-title-5)
* [템플릿 편집](/help/sites-authoring/templates.md): 페이지가 [편집 가능한 템플릿](/help/sites-authoring/templates.md#editable-and-static-templates)을 기반으로 하는 경우

* [게시됨으로 보기](/help/sites-authoring/editing-content.md#view-as-published)
* [관리자로 보기](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)
* [도움말](/help/sites-authoring/basic-handling.md#accessing-help)

예를 들어 해당하는 경우 **페이지 정보** 옵션도 표시됩니다.

* [출시 홍보](/help/sites-authoring/launches-promoting.md): 페이지가 출시되었을 경우
* [클래식 ](/help/sites-authoring/select-ui.md#switching-to-classic-ui-when-editing-a-page) UI에서 열기관리자가 이  [옵션을 활성화한 경우](/help/sites-administering/enable-classic-ui-editor.md)

또한 **페이지 정보**&#x200B;는 해당하는 경우 분석 및 권장 사항에 대한 액세스 권한을 제공할 수 있습니다.

## 페이지 모드 {#page-modes}

여러 작업을 허용하는 페이지를 편집할 때는 다음과 같은 다양한 모드가 있습니다.

* [편집](/help/sites-authoring/editing-content.md) - 페이지 컨텐츠를 편집할 때 사용할 모드
* [레이아웃](/help/sites-authoring/responsive-layout.md) - 장치에 따라 응답형 레이아웃을 만들고 편집할 수 있도록 허용(페이지가 레이아웃 컨테이너를 기반으로 하는 경우)

* [스캐폴딩](/help/sites-authoring/scaffolding.md) - 구조는 동일하면서 내용이 다른 페이지를 여러 개 만드는 데 도움이 됩니다.
* [개발자](/help/sites-developing/developer-mode.md) - 다양한 작업을 수행할 수 있습니다(권한 필요). 이러한 작업에는 페이지 및 해당 구성 요소의 기술적인 세부 정보 검사가 포함됩니다.

* [디자인](/help/sites-authoring/default-components-designmode.md) - 페이지에서 사용할 구성 요소를 활성화/비활성화하고 구성 요소의 디자인을 구성할 수 있습니다(페이지가 [정적 템플릿](/help/sites-authoring/templates.md#editable-and-static-templates)을 기반으로 하는 경우).

* [타깃팅](/help/sites-authoring/content-targeting-touch.md) - 모든 채널에서 타깃팅과 측정을 통해 컨텐츠 관련성을 높입니다.
* [활동 맵](/help/sites-authoring/page-analytics-using.md#analyticsvisiblefromthepageeditor) - 페이지에 대한 분석 데이터를 표시합니다.

* [타임워프](/help/sites-authoring/working-with-page-versions.md#timewarp) - 특정 시점에 페이지 상태를 볼 수 있습니다.
* [Live Copy 상태](/help/sites-authoring/editing-content.md#live-copy-status) - live copy 상태와 상속되었거나 상속되지 않은 구성 요소에 대한 간단한 개요를 알 수 있습니다.
* [미리 보기](/help/sites-authoring/editing-content.md#previewing-pages) - 페이지가 게시 환경에 표시될 상태로 해당 페이지를 보거나 컨텐츠의 링크를 사용하여 탐색하는 데 사용됩니다.

* [주석](/help/sites-authoring/annotations.md) - 페이지에서 주석을 추가하거나 보는 데 사용됩니다.

오른쪽 상단 모서리의 아이콘을 사용하여 다음 화면에 액세스할 수 있습니다. 실제 아이콘은 현재 사용 중인 모드를 반영하도록 변경됩니다.

![ateat-18](assets/ateat-18.png)

>[!NOTE]
>
>* 페이지의 특성에 따라 사용 가능한 일부 모드를 사용할 수 없습니다.
>* 일부 모드에 액세스하려면 적절한 권한이 필요합니다.
>* 공간 제약으로 인해 [개발자 모드]는 모바일 장치에서 사용할 수 없습니다.
>* [키보드 단축키](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)(`Ctrl-Shift-M`)를 사용하여 **미리 보기**&#x200B;와 현재 선택한 모드(예: **편집**, **레이아웃** 등) 간에 전환합니다.

>



## 경로 선택 {#path-selection}

작성할 때, 다른 페이지나 리소스에 대한 링크를 정의하거나 이미지를 선택할 때와 같이 다른 리소스를 선택해야 하는 경우가 있습니다. 경로를 쉽게 선택할 수 있도록 [경로 필드](/help/sites-authoring/author-environment-tools.md#path-fields)가 자동 완성 기능을 제공하고 [경로 브라우저](/help/sites-authoring/author-environment-tools.md#path-browser)가 보다 강력하게 선택할 수 있도록 지원합니다.

### 경로 필드  {#path-fields}

여기에 사용되는 예제는 이미지 구성 요소입니다. 구성 요소 사용 및 편집에 대한 자세한 내용은 [페이지 작성 구성 요소](/help/sites-authoring/default-components.md)를 참조하십시오.

경로 필드에는 자동 완성 및 예측 기능이 있어 리소스를 쉽게 찾을 수 있습니다.

경로 필드에서 **선택 대화 상자 열기** 단추를 클릭하면 [경로 브라우저](/help/sites-authoring/author-environment-tools.md#path-browser) 대화 상자가 열려 좀 더 상세한 선택 옵션을 사용할 수 있습니다.

![](do-not-localize/screen_shot_2018-03-22at154427.png)

또는 경로 필드에 입력을 시작하면 AEM에서 사용자가 입력하는 것과 일치하는 경로를 제공합니다.

![ateat-19](assets/ateat-19.png)

### 경로 브라우저 {#path-browser}

경로 브라우저는 [사이트 콘솔]의 [열 보기](/help/sites-authoring/basic-handling.md#column-view)와 같이 구성되어 리소스에 대한 상세한 선택 항목을 확인할 수 있습니다.

![screen_shot_2018-03-22at154521](assets/screen_shot_2018-03-22at154521.png)

* 리소스를 선택하면 대화 상자의 오른쪽 상단에 **선택** 단추가 활성화됩니다. 클릭하거나 탭하여 선택 사항을 확인하거나 **취소**&#x200B;를 선택하여 중단할 수 있습니다.
* 컨텍스트가 여러 리소스를 선택할 수 있도록 허용하는 경우 리소스를 선택해도 **선택** 단추가 활성화되지만 창 오른쪽 상단에 선택한 리소스 수가 추가됩니다. 숫자 옆에 있는 **X**&#x200B;를 클릭하면 모두 선택 취소됩니다.
* 트리를 탐색할 때 위치는 대화 상자 상단의 탐색 표시에 반영됩니다. 이러한 탐색 표시를 사용하여 리소스 계층 구조 내에서 빠르게 이동할 수도 있습니다.
* 언제든지 대화 상자 상단의 검색 필드를 사용할 수 있습니다. 검색을 지우려면 검색 필드에서 **X**&#x200B;를 클릭합니다.
* 검색 범위를 좁히려면 필터 옵션을 표시하고 특정 경로에 따라 결과를 필터링할 수 있습니다.

   ![ateat-21](assets/ateat-21.png)

## 키보드 단축키 {#keyboard-shortcuts}

다양한 [키보드 단축키](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)도 사용할 수 있습니다.
