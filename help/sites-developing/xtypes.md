---
title: xtype 사용(클래식 UI)
description: Adobe Experience Manager에서 사용할 수 있는 모든 xtype에 대해 알아봅니다
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
exl-id: 06ca4e6d-9ab7-4c5b-905c-07c448632f2b
source-git-commit: 1ef5593495b4bf22d2635492a360168bccc1725d
workflow-type: tm+mt
source-wordcount: '6384'
ht-degree: 0%

---

# xtype 사용(클래식 UI){#using-xtypes-classic-ui}

이 페이지에서는 AEM(Adobe Experience Manager)에서 사용할 수 있는 모든 xtype에 대해 설명합니다.

ExtJS 언어에서 xtype은 클래스에 제공되는 기호 이름입니다. 의 &quot;구성 요소 XTypes&quot; 단락을 읽을 수 있습니다. [ExtJS 2 개요](https://www.sencha.com/learn/overview-of-extjs-2) xtype의 정의와 사용 방법에 대한 자세한 설명.

AEM에서 사용 가능한 모든 위젯에 대한 전체 정보는 을 참조하십시오. [위젯 API 설명서](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html).

특정 xtype이 AEM에서 사용되는 구성 요소를 확인하려면 &#39;checkbox&#39;를 원하는 xtype으로 바꾸어 CRXDE에서 다음 Xpath 쿼리를 사용할 수 있습니다.

`//element(*, cq:Widget)[@xtype='checkbox']`

>[!NOTE]
>
>이 페이지에서는 클래식 UI 내에서 ExtJS xtype 사용에 대해 설명합니다.
>
>Adobe은 표준, 최신, [터치 지원 UI](/help/sites-developing/touch-ui-concepts.md) 기준 [Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui) 및 [Granite UI](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components).

## xtypes {#xtypes}

다음은 Adobe Experience Manager에서 사용할 수 있는 xtype입니다.

* 주석

  [CQ.wcm.Annotation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Annotation)

  대화 상자는 본문에 양식이 있고 바닥글에 단추 그룹이 있는 특수한 종류의 창입니다. 일반적으로 콘텐츠를 편집하는 데 사용되지만, 정보만 표시할 수도 있습니다.

* arraystore

  [CQ.Ext.data.ArrayStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.ArrayStore)

  이전에 &quot;SimpleStore&quot;라고 했습니다.

  만들기 위한 작은 도우미 클래스 [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)스토리지 데이터를 보다 쉽게 가져올 수 있습니다. ArrayStore 는 [CQ.Ext.data.ArrayReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.ArrayReader).

* asseteditor

  [CQ.dam.AssetEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.dam.AssetEditor)

  DAM 관리에 사용되는 자산 편집기입니다.

* assetreferencesearchdialog

  [CQ.wcm.AssetReferenceSearchDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.AssetReferenceSearchDialog)

  AssetReferenceSearchDialog는 페이지가 에셋 또는 태그를 참조하는 경우 표시되는 대화 상자입니다.

* blueprintconfig

  [CQ.wcm.msm.BlueprintConfig](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintConfig)

  BlueprintConfig는 블루프린트의 라이브 카피를 보고 이 블루프린트 속성을 편집할 수 있는 패널을 제공합니다( 동기화 트리거 및 동기화 작업 ).

* blueprintstatus

  [CQ.wcm.msm.BlueprintStatus](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintStatus)

  BlueprintStatus는 블루프린트 및 해당 라이브 카피 관계를 보고 편집할 수 있는 패널을 제공합니다. 탐색은 다음을 통해 수행됩니다. [CQ.wcm.msm.BlueprintStatus.Tree](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintStatus.Tree), 를 통한 에디션 [CQ.wcm.msm.BlueprintConfig](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintConfig) 및 a [CQ.wcm.msm.LiveCopyProperties](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.LiveCopyProperties).

* 상자

  [CQ.Ext.BoxComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.BoxComponent)

  임의의 기본 클래스 [구성 요소](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component) 너비와 높이를 사용하여 상자 크기를 지정합니다.

  BoxComponent는 크기 조정 및 위치 지정을 위한 자동 상자 모델 조정을 제공하며 구성 요소 렌더링 모델 내에서 올바르게 작동합니다.

* 브라우저 대화 상자

  [CQ.BrowseDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.BrowseDialog)

  찾아보기 대화 상자를 통해 사용자는 저장소를 탐색하여 경로를 선택할 수 있습니다. 일반적으로 다음을 통해 사용됩니다 [찾아보기 필드](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.BrowseField).

* 브라우저 필드

  [CQ.form.BrowseField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.BrowseField)

  **더 이상 사용되지 않는 기능: [CQ.form.PathField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField) 대신**

* 벌키터

  [CQ.wcm.Bulk편집기](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor)

  BulkEditor는 검색 결과를 편집할 수 있는 검색 엔진 및 그리드를 제공합니다.

  BulkEditor는 HTML 양식에 삽입해야 합니다(가져오기 기능에 필요). 이 기능은 와 완벽하게 호환됩니다. [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog).

* 벌케디토르폼

  [CQ.wcm.BulkEditorForm](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditorForm)

  BulkEditorForm은 [CQ.wcm.Bulk편집기](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor) HTML 양식으로 둘러싸여 있습니다. 독립 실행형 버전의 입니다. [CQ.wcm.Bulk편집기](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor), 가져오기 단추에 HTML 양식이 필요합니다.

* 추가할 수도 있습니다

  [CQ.Ext.Button](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button)

  단순 Button 클래스

* 단추 그룹

  [CQ.Ext.ButtonGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ButtonGroup)

  단추 그룹에 대한 컨테이너입니다.

* 차트

  [CQ.Ext.chart.Chart](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart)

  CQ.Ext.chart 패키지는 Flash 기반 차트를 사용하여 데이터를 시각화하는 기능을 제공합니다. 각 차트는 차트의 자동 업데이트를 활성화하는 CQ.Ext.data.Store에 직접 바인딩됩니다. 차트의 모양과 느낌을 변경하려면 [차트 스타일](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart) 및 [extraStyle](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart) 구성 옵션을 참조하십시오.

* 확인란

  [CQ.Ext.form.Checkbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Checkbox)

  단일 확인란 필드. 기존 확인란 필드를 직접 대체할 수 있습니다.

* checkbox 그룹

  [CQ.Ext.form.CheckboxGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.CheckboxGroup)

  다음에 대한 그룹화 컨테이너 [CQ.Ext.form.Checkbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Checkbox) 컨트롤.

* clearcombo

  [CQ.form.ClearableComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ClearableComboBox)

  ClearableComboBox는 값을 지우기 위한 트리거가 있는 편집할 수 없는 콤보 상자입니다.

* colorfield

  [CQ.form.ColorField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ColorField)

  ColorField를 사용하여 직접 또는 을 사용하여 색상 16진수 값을 입력할 수 있습니다. [CQ.Ext.ColorMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorMenu).

* 색상 목록

  [CQ.form.ColorList](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ColorList)

  ColorList를 사용하면 편집 가능한 목록에서 색상을 선택할 수 있습니다.

* 색상 메뉴

  [CQ.Ext.menu.ColorMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.ColorMenu)

  다음 항목이 포함된 메뉴: [CQ.Ext.ColorPalette](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorPalette) 구성 요소.

* 색상 팔레트

  [CQ.Ext.ColorPalette](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorPalette)

  색상을 선택할 수 있는 간단한 색상 팔레트 클래스입니다. 팔레트를 모든 컨테이너에 렌더링할 수 있습니다.

* 콤보

  [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)

  자동 완성, 원격 로드, 페이징 및 기타 다양한 기능을 지원하는 combobox 컨트롤입니다.

  ComboBox는 기존 HTML과 유사한 방식으로 작동합니다 &lt;select> 필드. 차이점은 을 제출한다는 것입니다. [valueField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox), 다음을 지정해야 합니다. [hiddenName](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox) 을 클릭하여 숨겨진 입력을 만듭니다.

* 구성 요소

  [CQ.Ext.Component](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component)

  모든 외부 구성 요소에 대한 기본 클래스입니다. Component의 모든 하위 클래스는 에서 제공하는 작성, 렌더링 및 삭제의 자동 외부 구성 요소 라이프사이클에 참여할 수 있습니다. [컨테이너](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) 클래스. 구성 요소는 를 통해 컨테이너에 추가될 수 있습니다. [개 항목](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) 컨테이너를 만들 때 옵션을 구성합니다.

* componentextractor

  [CQ.wcm.ComponentExtractor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ComponentExtractor)

  ComponentExtractor를 사용하면 사용자가 웹 사이트/페이지에서 구성 요소를 추출할 수 있습니다.

* componentselector

  [CQ.form.ComponentSelector](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ComponentSelector)

  사용 가능한 구성 요소를 그룹화하고 순서대로 선택한 항목.

* componentstyles

  [CQ.form.ComponentStyles](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ComponentStyles)

* 컴포지트 필드

  [CQ.form.CompositeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.CompositeField)

  한 개의 양식 필드 또는 양식 필드 그룹이 포함된 복잡한 양식 필드를 패널 기반으로 하는 기본 클래스입니다.

* 컨테이너

  [CQ.Ext.Container](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container)

  임의의 기본 클래스 [CQ.Ext.BoxComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.BoxComponent) 다른 구성 요소를 포함할 수 있습니다. 컨테이너는 포함 항목의 기본 동작, 즉 항목 추가, 삽입 및 제거를 처리합니다.

  가장 일반적으로 사용되는 컨테이너 클래스는 다음과 같습니다 [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel), [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window), 및 [CQ.Ext.TabPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.TabPanel).

* 컨텐츠 파인더

  [CQ.wcm.ContentFinder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder)

  ContentFinder는 전문화된 2열 구조입니다 [뷰포트](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Viewport) 왼쪽에는 실제 콘텐츠 파인더, 오른쪽에는 콘텐츠 프레임이 들어 있습니다.

* contentfindertab

  [CQ.wcm.ContentFinderTab](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinderTab)

  ContentFinderTab은 의 탭 패널에 사용되는 기능을 제공하는 특수 패널입니다 [CQ.wcm.ContentFinder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder). 일반적으로 검색 폼(쿼리 상자)과 검색을 표시하는 데이터 보기를 포함합니다.

* cq.workflow.model.combo

  [CQ.wcm.WorkflowModelCombo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.WorkflowModelCombo)

  WorkflowModelCombo는 사용자 지정입니다. [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox) 사용 가능한 워크플로우 모델 목록을 표시합니다.

* cq.workflow.model.selector

  [CQ.wcm.WorkflowModelSelector](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.WorkflowModelSelector)

  WorkflowModelSelector는 WorkflowModelCombo와 워크플로의 축소판 이미지, 워크플로 모델을 만들고 편집하기 위한 단추를 결합합니다.

* createsitewizard

  [CQ.wcm.CreateSiteWizard](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.CreateSiteWizard)

  CreateSiteWizard는 (MSM) 사이트를 만드는 단계별 마법사입니다.

* createversiondialog

  [CQ.wcm.CreateVersionDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.CreateVersionDialog)

  CreateVersionDialog는 페이지의 새 버전을 만들 수 있는 대화 상자입니다.

* customcontentpanel

  [CQ.CustomContentPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.CustomContentPanel)

  CustomContentPanel은에서 사용할 수 있는 특별한 종류의 패널입니다 [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog): 콘텐츠를 읽어들여 대화 상자의 다른 필드와 다른 URL에 제출합니다.

* 주기

  [CQ.Ext.CycleButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton)

  메뉴가 포함된 특수화된 SplitButton [CQ.Ext.menu.CheckItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.CheckItem) 요소. 이 단추는 클릭 시 각 메뉴 항목을 자동으로 순환하며 [변경](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton) 이벤트(또는 버튼 호출) [changeHandler](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton) 함수(제공된 경우).

* 데이터 보기

  [CQ.Ext.DataView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DataView)

  사용자 지정 레이아웃 템플릿과 서식을 사용하여 데이터를 표시하는 메커니즘입니다. 데이터 보기에서 다음을 사용 [CQ.Ext.XTemplate](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.XTemplate) 를 내부 템플릿 메커니즘으로 사용하고 [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store) 따라서 저장소의 데이터가 변경될 때 변경 사항을 반영하도록 보기가 자동으로 업데이트됩니다.

* 일자 필드

  [CQ.Ext.form.DateField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField)

  날짜 입력 필드에 [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker) 드롭다운 및 자동 날짜 유효성 검사.

* 다테메누

  [CQ.Ext.menu.DateMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.DateMenu)

  다음 항목이 포함된 메뉴: [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker) 구성 요소.

* datepicker

  [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker)

  팝업 날짜 선택기. 이 클래스는 [DateField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField) 클래스를 사용하여 유효한 날짜를 검색하고 선택할 수 있습니다.

* datetime

  [CQ.form.DateTime](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.DateTime)

  DateTime을 사용하면 날짜 및 시간을 조합하여 입력할 수 있습니다 [CQ.Ext.form.DateField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField) 및 [CQ.Ext.form.TimeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TimeField).

* 사용할 수 없게 됩니다

  [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog)

  대화 상자는 본문에 양식이 있고 바닥글에 단추 그룹이 있는 특수한 종류의 창입니다. 일반적으로 콘텐츠를 편집하는 데 사용되지만, 정보만 표시할 수도 있습니다.

* 대화 상자 세트

  [CQ.form.DialogFieldSet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.DialogFieldSet)

  대화 상자 필드 집합은 [필드 집합](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FieldSet) 에서 사용 [대화 상자](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog).

* directstore

  [CQ.Ext.data.DirectStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.DirectStore)

  을(를) 만드는 작은 도우미 클래스 [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store) (으)로 구성됨 [CQ.Ext.data.DirectProxy](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.DirectProxy) 및 [CQ.Ext.data.JsonReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader) 와 상호 작용하려면 [CQ.Ext.Direct](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Direct) 서버측 [공급자](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.direct.Provider) 더 쉬워

* displayfield

  [CQ.Ext.form.DisplayField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DisplayField)

  검증되지 않고 제출되지 않은 표시 전용 텍스트 필드.

* 편집 막대

  [CQ.wcm.EditBar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditBar)

  EditBar를 사용하면 막대의 버튼을 사용하여 컨텐츠를 편집할 수 있습니다.

  EditBar에는 나열되어 있지 않지만 [CQ.wcm.EditBase](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditBase).

* 편집기

  [CQ.Ext.Editor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Editor)

  요청 시 표시/숨김을 처리하며 일부 내장된 크기 조정 및 이벤트 처리 논리를 갖는 기본 편집기 필드입니다.

* 편집기 격자

  [CQ.Ext.grid.EditorGridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.EditorGridPanel)

  이 클래스는 [GridPanel 클래스](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) 선택한 항목에 셀 편집을 제공하려면 [열](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.Column). 편집 가능한 열은 다음을 제공하여 지정합니다. [편집자](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.ColumnModel) 다음에서 [열 구성](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.Column).

* editrollover

  [CQ.wcm.EditRollover](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditRollover)

  EditRollover를 사용하면 두 번 클릭하여 콘텐츠를 편집할 수 있으며 컨텍스트 메뉴를 통해 추가 편집 작업을 제공할 수 있습니다. 편집 가능 영역은 마우스가 컨텐츠 위로 롤오버될 때 프레임으로 표시됩니다.

* 사료용 어구

  [CQ.wcm.Feedimporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.FeedImporter)

  FeedImporter를 사용하면 사용자가 RSS 또는 Atom 피드를 가져오고 각 피드 항목에 대한 페이지를 만들 수 있습니다.

* 필드

  [CQ.Ext.form.Field](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Field)

  기본 이벤트 처리, 크기 조정, 값 처리 및 기타 기능을 제공하는 양식 필드의 기본 클래스입니다.

* 필드 세트

  [CQ.Ext.form.FieldSet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FieldSet)

  내에서 항목을 그룹화하는 데 사용되는 표준 컨테이너 [양식](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FormPanel). ...

* fileuploaddialogbutton

  [CQ.form.FileUploadDialogButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.FileUploadDialogButton)

  FileUploadDialogButton은 FileUploadField를 통해 파일을 업로드하기 위한 새 대화 상자를 여는 단추를 만듭니다. 별도의 양식으로 업로드해야 하는 편집 대화 상자 내에서 사용할 수 있습니다.

* fileuploadfield

  [CQ.form.FileUploadField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.FileUploadField)

  FileUploadField를 사용하여 업로드할 단일 파일을 선택할 수 있습니다.

* findreplacedialog

  [CQ.wcm.FindReplaceDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.FindReplaceDialog)

  FindReplaceDialog는 페이지 및 하위 페이지에서 토큰을 찾고 바꾸는 대화 상자입니다.

* flash

  [CQ.Ext.FlashComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.FlashComponent)

* 격자

  [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)

  이 클래스는 데이터를 행과 열의 테이블 형식으로 나타내는 구성 요소 기반 그리드 컨트롤의 기본 인터페이스를 나타냅니다.

* groupingstore

  [CQ.Ext.data.GroupingStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.GroupingStore)

  사용 가능한 필드 중 하나별로 레코드를 그룹화하는 기능을 제공하는 전문 스토어 구현입니다. 다음과함께 사용됩니다. [CQ.Ext.grid.GroupingView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GroupingView) 그룹화된 GridPanel에 대한 데이터 모델을 증명합니다.

* heavymovedialog

  [CQ.wcm.HeavyMoveDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.HeavyMoveDialog)

  HeavyMoveDialog는 페이지 및 하위 페이지를 이동하는 대화 상자로, 이전에 활성화된 페이지(&#39;heavy&#39; 이동)의 재활성화도 고려합니다.

* 숨김

  [CQ.Ext.form.Hidden](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Hidden)

  양식 제출에서 전달해야 하는 양식의 숨겨진 값을 저장하기 위한 기본 숨김 필드입니다.

* historybutton

  [CQ.HistoryButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.HistoryButton)

  HistoryButton은 뒤로 및 앞으로 단추를 쉽게 제공할 수 있는 작은 도우미 클래스입니다. 일반적으로 두 개의 관련 인스턴스가 필요합니다. 앞으로 단추 인스턴스는 기록을 처리하는 뒤로 단추 인스턴스에 연결된 간단한 단추입니다.

* htmleditor

  [CQ.Ext.form.HtmlEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.HtmlEditor)

  간단한 HTML 편집기 구성 요소를 제공합니다. 일부 도구 모음 기능은 Safari에서 지원되지 않으며 필요한 경우 자동으로 숨겨집니다. 이러한 사항은 해당되는 경우 구성 옵션에 명시되어 있습니다.

  편집기의 도구 모음 단추는에 정의된 도구 설명이 있습니다. [단추 설명](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.HtmlEditor) 속성.

* iframedialog

  [CQ.IframeDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.IframeDialog)

  iframe의 콘텐츠를 표시하고 iframe의 양식을 허용하는 일반 대화 상자입니다.

* iframepanel

  [CQ.IframePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.IframePanel)

  iframe이 포함된 패널입니다. iframe을 쉽게 만들고, iframe 로드 이벤트를 만들고, iframe 컨텐츠에 쉽게 액세스할 수 있습니다.

* inlinetextfield

  [CQ.form.InlineTextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.InlineTextField)

  InlineField는 포커스가 없을 때 레이블로 표시되는 텍스트 필드입니다.

* jsonstore

  [CQ.Ext.data.JsonStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonStore)

  만들기 위한 작은 도우미 클래스 [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)JSON 데이터에서 보다 쉽게 가져온 . JsonStore는 [CQ.Ext.data.JsonReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader).

* 레이블

  [CQ.Ext.form.Label](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Label)

  기본 레이블 필드.

* languagecopydialog

  [CQ.wcm.LanguageCopyDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.LanguageCopyDialog)

  LanguageCopyDialog는 언어 트리를 복사하기 위한 대화 상자입니다.

* 링크 확인

  [CQ.wcm.LinkChecker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.LinkChecker)

  LinkChecker는 사이트에서 외부 링크를 확인하는 도구입니다.

* listview

  [CQ.Ext.list.ListView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.ListView)

  CQ.Ext.list.ListView는 [격자](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) 보기 좋아요.

* livecopyproperties

  [CQ.wcm.msm.LiveCopyProperties](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.LiveCopyProperties)

  라이브 카피 속성은 라이브 카피 속성( 관계 상속, 동기화 트리거 및 동기화 작업 )을 보고 편집할 수 있는 패널을 제공합니다.

* lvbooleancolumn

  [CQ.Ext.list.BooleanColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.BooleanColumn)

  부울 데이터 필드를 렌더링하는 열 정의 클래스입니다. 다음을 참조하십시오. [xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) 구성 옵션 / [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) 을 참조하십시오.

* lvcolumn

  [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column)

  이 클래스는 의 초기화에서 사용할 열 구성 데이터를 캡슐화합니다. [목록 보기](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.ListView).

* lvdatecolumn

  [CQ.Ext.list.DateColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.DateColumn)

  전달된 날짜를 기본 로케일에 따라 렌더링하거나 구성된 열 정의 클래스 [형식](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.DateColumn). 다음을 참조하십시오. [xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) 구성 옵션 / [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) 을 참조하십시오.

* lvnumbercolumn

  [CQ.Ext.list.NumberColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.NumberColumn)

  에 따라 숫자 데이터 필드를 렌더링하는 열 정의 클래스 [형식](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.NumberColumn) 문자열. 다음을 참조하십시오. [xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) 구성 옵션 / [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) 을 참조하십시오.

* mediabrowsedialog

  [CQ.MediaBrowseDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.MediaBrowseDialog)

  **더 이상 사용되지 않는 기능: [콘텐츠 파인더](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder) 미디어를 찾아봅니다.**

  MediaBrowseDialog는 미디어 라이브러리를 탐색하기 위한 대화 상자입니다.

* 메뉴

  [CQ.Ext.menu.Menu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Menu)

  메뉴 개체. 메뉴 항목을 추가할 수 있는 컨테이너입니다. 다른 구성 요소를 기반으로 특수 메뉴를 원하는 경우 Menu를 기본 클래스로 사용할 수도 있습니다 [CQ.Ext.menu.DateMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.DateMenu) 예).

  메뉴에는 다음 중 하나가 포함될 수 있습니다. [메뉴 항목](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Item)또는 일반 [구성 요소](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component)s.

* 메누바세템

  [CQ.Ext.menu.BaseItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.BaseItem)

  메뉴에 렌더링되는 모든 항목의 기본 클래스입니다. BaseItem은 모든 메뉴 구성 요소에서 공유하는 기본 렌더링, 활성화된 상태 관리 및 기본 구성 옵션을 제공합니다.

* menucheckitem

  [CQ.Ext.menu.CheckItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.CheckItem)

  기본적으로 확인란이 포함되어 있지만 라디오 그룹의 일부일 수도 있는 메뉴 항목을 추가합니다.

* menuitem

  [CQ.Ext.menu.Item](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Item)

  메뉴 관련 기능(예: 하위 메뉴)이 필요하며 정적 표시 항목이 아닌 모든 메뉴 항목에 대한 기본 클래스입니다. 항목이 의 기본 기능을 확장합니다. [CQ.Ext.menu.BaseItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.BaseItem) 메뉴별 활성화 추가 및 처리 클릭.

* 메뉴 분리자

  [CQ.Ext.menu.Separator](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Separator)

  메뉴 항목의 논리적 그룹을 나누는 데 사용되는 메뉴에 구분 기호를 추가합니다. 일반적으로 를 직접 만들지 않고 add()에 대한 호출이나 항목 구성에서 &quot;-&quot;를 사용하여 이 중 하나를 추가합니다.

* menutextitem

  [CQ.Ext.menu.TextItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.TextItem)

  머리글 또는 그룹 구분 기호로 사용되는 메뉴에 정적 텍스트 문자열을 추가합니다.

* 메타데이터

  [CQ.dam.form.Metadata](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.dam.form.Metadata)

  메타데이터는 에셋 편집기 페이지와 같이 사용되는 메타데이터 필드에 필요한 정보를 결정하기 위한 필드 집합을 제공합니다.

  이 변수는 다음 필드를 제공합니다.

* 다중 필드

  [CQ.form.MultiField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MultiField)

  MultiField는 다중 값 속성을 편집하기 위한 편집 가능한 양식 필드 목록입니다.

* mvt

  [CQ.form.MVT](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MVT)

  Multivariate Testing 구성 요소를 사용하여 배너 교대용으로 표시되는 이미지 세트를 정의하고 편집할 수 있습니다. 클릭스루 비율 통계는 배너별로 수집됩니다.

* notificationinbox

  [CQ.wcm.NotificationInbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.NotificationInbox)

  사용자는 NotificationInbox를 사용하여 WCM 작업에 가입하고 알림을 관리할 수 있습니다.

* numberfield

  [CQ.Ext.form.NumberField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.NumberField)

  자동 키 입력 필터링 및 숫자 유효성 검사를 제공하는 숫자 텍스트 필드입니다.

* offlineimporter

  [CQ.wcm.OfflineImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.OfflineImporter)

  OfflineImporter는 Microsoft® Word 문서를 가져와 AEM 페이지로 변환하는 도구입니다. 이 기능을 사용하면 워드 프로세서를 사용하여 콘텐츠를 오프라인으로 편집할 수 있습니다.

* ownerdraw

  [CQ.form.OwnerDraw](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.OwnerDraw)

  OwnerDraw에는 사용자 지정 HTML 코드(직접 입력되거나 URL에서 검색됨)가 포함될 수 있습니다.

* 페이징

  [CQ.Ext.PagingToolbar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.PagingToolbar)

  레코드 수가 증가하면 브라우저에서 레코드를 렌더링하는 데 필요한 시간이 증가합니다. 페이징은 클라이언트와 교환되는 데이터의 양을 줄이기 위해 사용됩니다.

* 패널

  [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel)

  패널은 애플리케이션 중심의 사용자 인터페이스를 위한 완벽한 구성 요소로 만들어주는 특정 기능과 구조적 구성 요소를 갖춘 컨테이너입니다.

  패널은 의 상속을 통해 다음과 같은 특성을 갖습니다. [CQ.Ext.Container](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container).

* 단락 참조

  [CQ.form.ParagraphReference](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ParagraphReference)

  단락 참조 필드를 사용하면 페이지를 탐색하고 해당 단락 중 하나를 선택할 수 있습니다. 트리거 필드와 연결된 단락 찾아보기 대화 상자로 구성됩니다.

* 암호

  [CQ.form.Password](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Password)

  암호는 다음과 같습니다. [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField) 그러나 값을 비공개로 유지하므로 사용자가 중요한 데이터를 입력할 수 있습니다.

* 경로 완성

  [CQ.form.PathCompletion](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathCompletion)

  **더 이상 사용되지 않는 기능: [CQ.form.PathField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField) 대신**

* pathfield

  [CQ.form.PathField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField)

  PathField는 경로 완료가 있는 경로에 대해 설계된 입력 필드이며 [CQ.BrowseDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.BrowseDialog) 서버 저장소 검색. 고급 링크 생성을 위해 페이지 단락을 탐색할 수도 있습니다.

* 진행 상황

  [CQ.Ext.ProgressBar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ProgressBar)

  업데이트할 수 있는 진행률 표시줄 구성 요소입니다. 진행률 표시줄은 수동 모드와 자동 모드, 이렇게 두 가지 모드를 지원합니다.

  수동 모드에서는 표시, 업데이트(를 통해) 책임이 있습니다. [update진행률](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ProgressBar))를 추가하고 자체 코드에서 필요에 따라 진행률 표시줄을 지웁니다. 이 메서드는 진행률을 표시하려는 경우에 가장 적합합니다.

* propertygrid

  [CQ.Ext.grid.PropertyGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.PropertyGrid)

  개발 IDE에서 일반적으로 표시되는 기존 속성 격자를 모방하도록 설계된 특수 격자 구현입니다. 그리드의 각 행은 일부 객체의 속성을 나타내며, 데이터는에서 이름/값 쌍 세트로 저장됩니다. [CQ.Ext.grid.PropertyRecord](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.PropertyRecord)s.

* Propgrid

  [CQ.PropertyGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.PropertyGrid)

  PropertyGrid는 개체의 속성을 표시하고 편집하는 데 사용되는 일반 그리드입니다.

* 빠른 팁

  [CQ.Ext.QuickTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTip)

  @xtype 빠른 팁 마크업에 지정할 수 있고 자동으로 글로벌에서 관리할 수 있는 툴팁에 대한 특수 툴팁 클래스입니다 [CQ.Ext.QuickTips](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTips) 인스턴스. 자세한 사용 방법 및 예제는 QuickTips 클래스 헤더를 참조하십시오.

* 라디오

  [CQ.Ext.form.Radio](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Radio)

  단일 라디오 필드. 확인란과 동일하지만 입력 유형을 자동으로 설정하는 데 편리하도록 제공됩니다. 라디오 그룹화는 그룹의 각 라디오에 동일한 이름을 지정하는 경우 브라우저에서 자동으로 처리됩니다.

* 방사선군

  [CQ.Ext.form.RadioGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.RadioGroup)

  다음에 대한 그룹화 컨테이너 [CQ.Ext.form.Radio](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Radio) 컨트롤.

* 참조 대화 상자

  [CQ.wcm.ReferencesDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ReferencesDialog)

  참조 대화 상자는 페이지에 참조를 표시하는 대화 상자입니다.

* 복원트리대화 상자

  [CQ.wcm.RestoreTreeDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.RestoreTreeDialog)

  RestoreTreeDialog는 이전 버전의 트리를 복원하기 위한 대화 상자입니다.

* restoreversiondialog

  [CQ.wcm.RestoreVersionDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.RestoreVersionDialog)

  RestoreVersionDialog는 페이지의 이전 버전을 복원하는 대화 상자입니다.

* richtext

  [CQ.form.RichText](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.RichText)

  RichText는 스타일이 지정된 텍스트 정보(서식 있는 텍스트)를 편집하기 위한 양식 필드를 제공합니다.

  RichText 구성 요소는 현재 다음 기능을 제공합니다.

* 롤아웃 계획

  [CQ.wcm.msm.RolloutPlan](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutPlan)

  롤아웃 계획은 페이지 롤아웃 진행 상황을 확인하는 대화 상자를 제공합니다. 롤아웃 계획은 다음에 의해 시작됩니다. [CQ.wcm.msm.롤아웃 마법사](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutWizard).

* rolloutwizard

  [CQ.wcm.msm.롤아웃 마법사](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutWizard)

  롤아웃 마법사는 페이지를 롤아웃하는 마법사를 제공합니다. 롤아웃 마법사가 다음을 시작합니다. [CQ.wcm.msm.RolloutPlan](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutPlan).

* searchfield

  [CQ.form.SearchField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SearchField)

  SearchField는 저장소 검색에 사용할 수 있는 드롭다운 목록에 결과를 제공하는 검색 필드를 제공합니다.

* 선택

  [CQ.form.Selection](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Selection)

  선택 항목을 사용하면 사용자가 여러 옵션 중에서 선택할 수 있습니다. 옵션은 구성의 일부이거나 JSON 응답에서 로드될 수 있습니다. 선택 영역을 드롭다운(선택)으로 렌더링하거나 콤보 상자(선택 및 자유 텍스트 항목)로 렌더링할 수 있습니다.

* 사이드 킥

  [CQ.wcm.Sidekick](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Sidekick)

  Sidekick은 사용자에게 페이지 편집을 위한 일반적인 도구를 제공하는 부동 도우미입니다.

* siteadmin

  [CQ.wcm.SiteAdmin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.SiteAdmin)

  SiteAdmin은 WCM 관리 기능을 제공하는 콘솔입니다.

* siteimporter

  [CQ.wcm.SiteImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.SiteImporter)

  SiteImporter를 사용하여 사용자가 전체 웹 사이트를 가져오고 초기 프로젝트를 만들 수 있습니다.

* sizefield

  [CQ.form.SizeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SizeField)

  SizeField를 사용하여 폭과 높이를 입력할 수 있습니다(예: 이미지의 경우).

* 슬라이더

  [CQ.Ext.Slider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Slider)

  수직 또는 수평 방향, 키보드 조정, 구성 가능한 스냅, 축 클릭 및 애니메이션을 지원하는 슬라이더입니다. 컨테이너에 항목으로 추가할 수 있습니다. 사용 예: ...

* 슬라이드 쇼

  [CQ.form.Slideshow](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Slideshow)

  Slideshow는 슬라이드쇼로 볼 수 있는 이미지 및 이미지 제목 집합을 정의하고 편집하는 데 사용할 수 있는 구성 요소를 제공합니다.

  Slideshow 구성 요소는 [CQ.form.SmartImage](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartImage) 구성 요소.

* smartfile

  [CQ.form.SmartFile](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartFile)

  SmartFile은 지능형 파일 업로더입니다.

  Flash 플러그인(버전 >= 9)이 설치되어 있으면 업로드를 편리하게 처리할 수 있는 SWFupload 라이브러리를 사용하여 업로드가 실행됩니다.

* 스마티마게

  [CQ.form.SmartImage](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartImage)

  SmartImage는 지능형 이미지 업로더입니다. 이 도구는 업로드된 이미지를 처리하는 도구, 예를 들어 이미지 맵과 이미지 크롭을 정의하는 도구를 제공합니다.

  구성 요소는 별도의 대화 상자 탭에서 사용하도록 설계되었습니다.

* 스페이서

  [CQ.Ext.Spacer](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Spacer)

  레이아웃에 큰 공간을 제공하는 데 사용됩니다.

* 회전기

  [CQ.form.Spinner](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Spinner)

  회전자는 숫자, 날짜 또는 시간 값에 대한 트리거 필드입니다. 제공된 위 및 아래 트리거, 스크롤 휠 또는 키를 사용하여 값을 증가 및 감소시킬 수 있습니다.

* 분할 단추

  [CQ.Ext.SplitButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.SplitButton)

  단추의 기본 클릭 이벤트와 별도로 이벤트를 실행할 수 있는 기본 제공 드롭다운 화살표를 제공하는 분할 단추입니다. 일반적으로 기본 버튼 작업에 추가 옵션을 제공하는 드롭다운 메뉴를 표시하는 데 사용되지만, 모든 사용자 지정 처리기에서 arrowclick 구현을 제공할 수 있습니다.

* 정적

  [CQ.Static](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Static)

  정적 을 사용하여 임의의 텍스트나 HTML을 표시할 수 있습니다.

* 통계

  [CQ.wcm.Statistics](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Statistics)

  통계는 페이지 노출 횟수를 차트로 표시합니다. 위젯을 사용하여 기간을 선택할 수 있으며 통계가 표시되어야 합니다.

* 스토어

  [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)

  Store 클래스는 클라이언트 측 캐시를 캡슐화합니다. [기록](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Record) 구성 요소에 대한 입력 데이터를 제공하는 개체 [격자 패널](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel), [콤보 상자](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)또는 [데이터 보기](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DataView).

* 제안 필드

  [CQ.form.SuggestField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SuggestField)

  SuggestField는 해당 항목에 따라 제안 사항을 사용자에게 제공합니다.

* 전환기

  [CQ.Switcher](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Switcher)

  전환기는 콘솔에 웹 사이트, 디지털 자산, 도구, 워크플로우 및 보안 간을 전환하는 헤더 막대의 단추 그룹을 제공합니다.

* tableedit

  [CQ.form.TableEdit](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit)

  **더 이상 사용되지 않는 기능: [CQ.form.TableEdit2](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit2) 대신,**

* tableedit2

  [CQ.form.TableEdit2](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit2)

  TableEdit2는 테이블을 만들기 위한 위젯을 제공합니다.

* 탭패널

  [CQ.Ext.TabPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.TabPanel)

  기본 탭 컨테이너입니다. TabPanels는 표준과 동일하게 사용할 수 있습니다 [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel) 레이아웃 목적으로(하위 구성 요소 포함에 대한 특별 지원 포함)[`items`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container)).

* 태그

  [CQ.tagging.TagInputField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.tagging.TagInputField)

  ```
  CQ.tagging.TagInputField
  ```

  는 태그를 입력하기 위한 양식 위젯입니다. 기존 태그에서 선택할 수 있는 팝업 메뉴가 있으며, 자동 완성 및 기타 다양한 기능을 포함합니다.

* 텍스트 영역

  [CQ.Ext.form.TextArea](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextArea)

  여러 줄 텍스트 필드. 기존 텍스트 영역 필드를 직접 대체하고 자동 크기 조정을 지원할 수 있습니다.

* 텍스트 단추

  [CQ.TextButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.TextButton)

  TextButton은 [CQ.Ext.Button](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button).

* 텍스트 필드

  [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField)

  기본 텍스트 필드. 기존 텍스트 입력을 직접 대체하거나 보다 정교한 입력 컨트롤의 기본 클래스로 사용할 수 있습니다 [CQ.Ext.form.TextArea](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextArea) 및 [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)).

* 축소판

  [CQ.form.Thumbnail](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Thumbnail)

* timefield

  [CQ.Ext.form.TimeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TimeField)

  시간 드롭다운과 자동 시간 유효성 검사가 포함된 시간 입력 필드를 제공합니다. 사용 예: ...

* 팁

  [CQ.Ext.Tip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Tip)

  @xtype 팁 이것은 의 기본 클래스입니다. [CQ.Ext.QuickTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTip) 및 [CQ.Ext.Tooltip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Tooltip) 모든 팁 기반 클래스에 필요한 기본 레이아웃과 위치를 제공합니다. 이 클래스는 간단하고 정적으로 배치된 팁에 직접 사용할 수 있습니다.

* titleseparator

  [CQ.menu.TitleSeparator](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.menu.TitleSeparator)

  메뉴 항목의 논리적 그룹을 나누는 데 사용되는 메뉴에 구분 기호를 추가합니다. 구분 기호는 제목을 포함할 수도 있습니다.

* 도구 모음

  [CQ.Ext.Toolbar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Toolbar)

  기본 도구 모음 클래스입니다. 하지만 [`defaultType`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) 도구 모음 의 경우: [`button`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button), 도구 모음 요소(도구 모음 컨테이너의 하위 항목)는 사실상 모든 유형의 구성 요소일 수 있습니다. 도구 모음 요소는 생성자를 통해 명시적으로 만들 수 있습니다.

* 툴팁

  [CQ.Ext.ToolTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ToolTip)

  대상 요소 위로 마우스를 가져갈 때 추가 정보를 제공하기 위한 표준 도구 설명 구현입니다. @xtype을 선택합니다.

* 나무그늘막

  [CQ.tree.TreeGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.tree.TreeGrid)

  @xtype 트리그리드

* 트리패널

  [CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)

  TreePanel은 트리 구조 데이터의 트리 구조 UI 표현을 제공합니다.

  [트리 노드](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreeNode)TreePanel에 추가된 에는 애플리케이션에서 사용하는 메타데이터가 각각 포함될 수 있습니다. [속성](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreeNode) 속성.

* 트리거

  [CQ.Ext.form.TriggerField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField)

  클릭 가능한 트리거 단추를 추가하는 TextFields용 편리한 래퍼를 제공합니다(기본적으로 콤보 상자와 유사). 트리거에는 기본 작업이 없으므로 재정의하여 트리거 클릭 처리기를 구현할 함수를 할당해야 합니다 [onTriggerClick](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField). 콤보 상자와 동일하게 렌더링되므로 TriggerField를 직접 만들 수 있습니다.

* uploadadalog

  [CQ.UploadDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.UploadDialog)

  UploadDialog를 사용하면 사용자가 저장소에 파일을 업로드할 수 있습니다. 새 UploadDialog를 만듭니다.

* 사용자 정보

  [CQ.UserInfo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.UserInfo)

  현재 사용자 이름을 표시하고 사용자 속성 편집 및 가장과 같은 사용자 작업을 허용하는 도구 모음 항목입니다.

* 뷰포트

  [CQ.Ext.Viewport](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Viewport)

  볼 수 있는 애플리케이션 영역(브라우저 뷰포트)을 나타내는 전문 컨테이너입니다.

  뷰포트는 문서 본문으로 렌더링되고 브라우저 뷰포트의 크기에 맞게 자동으로 크기가 조정되며 창 크기 조정을 관리합니다. 뷰포트가 하나만 생성될 수 있습니다.

* 창

  [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)

  응용 프로그램 창으로 사용하기 위한 특수 패널입니다. 창문은 떠있고 [크기 변경 가능](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window), 및 [드래그 가능해](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) 기본적으로. Windows는 [최대화](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) 뷰포트를 채우고 이전 크기로 복원하며 다음 작업을 수행할 수 있습니다. [최소화](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)d.

* xmlstore

  [CQ.Ext.data.XmlStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.XmlStore)

  만들기 위한 작은 도우미 클래스 [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)XML 데이터에서 보다 쉽게 가져옵니다. XmlStore는 [CQ.Ext.data.XmlReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.XmlReader).

  **cqinclude** 저장소에 있는 다른 경로의 위젯 정의를 포함하는 의사 xtype. 이 변수는 페이지 대화 상자에서 가장 일반적으로 사용됩니다. 이 xtype에 대한 실제 JavaScript 위젯 클래스가 없습니다. CQ.Util 클래스의 formatData() 함수에 의해 처리됩니다. 자세한 내용은 이 기술 자료 문서를 참조하십시오.
