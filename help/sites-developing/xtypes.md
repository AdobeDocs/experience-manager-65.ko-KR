---
title: xtypes 사용(클래식 UI)
seo-title: xtypes 사용(클래식 UI)
description: AEM에서 사용할 수 있는 모든 xtype에 대해 알아보기
seo-description: AEM에서 사용할 수 있는 모든 xtype에 대해 알아보기
uuid: 6497caa4-2f9b-4f21-9023-88d485fd1d78
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: adb70b43-1b0b-4302-905a-c7612675dabb
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# xtypes 사용(클래식 UI){#using-xtypes-classic-ui}

이 페이지에서는 AEM(Adobe Experience Manager)에서 사용할 수 있는 모든 xtype에 대해 설명합니다.

ExtJS 언어에서 xtype은 클래스에 지정된 상징적 이름입니다. xtype의 정의와 사용 방법에 대한 자세한 설명을 보려면 ExtJS [2](https://www.sencha.com/learn/overview-of-extjs-2) 개요의 &quot;구성 요소 XTypes&quot; 단락을 참조하십시오.

AEM에서 사용 가능한 모든 위젯에 대한 자세한 내용은 [위젯 API 설명서를](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html)참조하십시오.

AEM에서 특정 xtype이 사용되는 구성 요소를 확인하려면 CRXDE에서 &#39;checkbox&#39;를 관심 있는 xtype으로 대체하여 다음 Xpath 쿼리를 사용할 수 있습니다.

`//element(*, cq:Widget)[@xtype='checkbox']`

>[!NOTE]
>
>이 페이지에서는 클래식 UI 내의 ExtJS xtype 사용에 대해 설명합니다.
>
>Adobe에서는 Coral UI 및 Granite UI를 기반으로 하는 표준 [터치 지원](/help/sites-developing/touch-ui-concepts.md) UI를 [활용할](/help/sites-developing/touch-ui-concepts.md#coral-ui) 것을 [권장합니다](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components).

## xtypes {#xtypes}

Adobe Experience Manager에서 사용 가능한 xtype 목록을 참조하십시오.

* 주석

   [CQ.wcm.Annotation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Annotation)

   대화 상자는 본문에 양식이 있고 바닥글에 단추 그룹이 있는 특별한 종류의 창입니다. 일반적으로 컨텐츠를 편집하는 데 사용되지만 정보만 표시할 수 있습니다.

* arraystore

   [CQ.Ext.data.ArrayStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.ArrayStore)

   이전에 &quot;SimpleStore&quot;라고 불렀습니다.

   Array 데이터에서 CQ. [Ext.data.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)Stores를 보다 쉽게 만들 수 있는 작은 도우미 클래스입니다. ArrayStore는 CQ.Ext.data. [ArrayReader로 자동으로 구성됩니다](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.ArrayReader).

* asseteditor

   [CQ.dam.AssetEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.dam.AssetEditor)

   DAM 관리에서 사용되는 자산 편집기.

* assetreferencesearch 대화 상자

   [CQ.wcm.AssetReferenceSearchDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.AssetReferenceSearchDialog)

   AssetReferenceSearchDialog는 페이지가 자산 또는 태그를 참조하는 경우 표시되는 대화 상자입니다.

* 블루프린팅

   [CQ.wcm.msm.BlueprintConfig](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintConfig)

   BlueprintConfig는 Blueprint의 Live Copy를 보고 이 Blueprint 속성(동기화 트리거 및 동기화 작업)을 편집할 수 있는 패널을 제공합니다.

* 블루프린트상태

   [CQ.wcm.msm.BlueprintStatus](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintStatus)

   BlueprintStatus는 블루프린트 및 Live Copy 관계를 보고 편집할 수 있는 패널을 제공합니다. 브라우징은 CQ.wcm. [msm.BlueprintStatus.Tree를](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintStatus.Tree)통해 수행되며 [CQ.wcm.msm.BlueprintConfig](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintConfig) 및 CQ.wcm. [msm.LiveCopyProperties를 통해 수행됩니다](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.LiveCopyProperties).

* box

   [CQ.Ext.BoxComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.BoxComponent)

   폭과 높이를 [사용하여](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component) 상자로 크기를 지정할 구성 요소에 대한 기본 클래스입니다.

   BoxComponent는 크기 조정 및 배치를 위한 자동 상자 모델 조정을 제공하며 구성 요소 렌더링 모델 내에서 올바르게 작동합니다.

* browsedialog

   [CQ.BrowseDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.BrowseDialog)

   찾아보기 대화 상자를 사용하면 경로를 선택하기 위해 저장소를 검색할 수 있습니다. 일반적으로 BrowseField를 통해 [사용됩니다](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.BrowseField).

* browsefield

   [CQ.form.BrowseField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.BrowseField)

   **가치 하락:CQ[.form.PathField를](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField)대신 사용하십시오**

* 벌커지터

   [CQ.wcm.BulkEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor)

   BulkEditor는 검색 엔진 및 그리드를 제공하여 검색 결과를 편집합니다.

   BulkEditor를 HTML 양식에 삽입해야 합니다(가져오기 기능에 필요). CQ.Dialog와 완벽하게 [호환됩니다](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog).

* 돌출 형태

   [CQ.wcm.BulkEditorForm](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditorForm)

   BulkEditorForm은 HTML [폼으로](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor) 둘러싸인 CQ.wcm.BulkEditor를 제공합니다. CQ.wcm.BulkEditor [의 독립 실행형 버전이며](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor)가져오기 단추에는 HTML 양식이 필요합니다.

* 단추

   [CQ.Ext.Button](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button)

   단순 단추 클래스

* 단추 그룹

   [CQ.Ext.ButtonGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ButtonGroup)

   단추 그룹의 컨테이너입니다.

* 차트

   [CQ.Ext.chart.Chart](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart)

   CQ.Ext.chart 패키지는 Flash 기반 차트로 데이터를 시각화하는 기능을 제공합니다. 각 차트는 CQ.Ext.data.Store에 직접 바인딩되므로 자동으로 차트를 업데이트할 수 있습니다. 차트의 모양과 느낌을 변경하려면 [chartStyle](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart) 및 [extraStyle](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart) 구성 옵션을 참조하십시오.

* 확인란

   [CQ.Ext.form.Checkbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Checkbox)

   단일 확인란 필드. 기존 확인란 필드를 직접 교체하여 사용할 수 있습니다.

* checkboxgroup

   [CQ.Ext.form.CheckboxGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.CheckboxGroup)

   CQ.Ext.form. [Checkbox 컨트롤의 그룹화](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Checkbox) 컨테이너입니다.

* clearcombo

   [CQ.form.ClearableComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ClearableComboBox)

   ClearableComboBox는 값을 지우는 트리거가 있는 편집할 수 없는 콤보 상자입니다.

* 색상 필드

   [CQ.form.ColorField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ColorField)

   ColorField를 사용하면 직접 또는 CQ.Ext.ColorMenu를 사용하여 색상 16진수 값을 입력할 [수 있습니다](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorMenu).

* 색상 목록

   [CQ.form.ColorList](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ColorList)

   ColorList를 사용하면 편집 가능한 목록에서 색상을 선택할 수 있습니다.

* 색상 메뉴

   [CQ.Ext.menu.ColorMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.ColorMenu)

   CQ.Ext. [ColorPalette 구성 요소를 포함하는](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorPalette) 메뉴입니다.

* 색상 팔레트

   [CQ.Ext.ColorPalette](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorPalette)

   색상을 선택하는 간단한 색상 팔레트 클래스입니다. 팔레트를 모든 컨테이너에 렌더링할 수 있습니다.

* 콤보

   [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)

   자동 완성, 원격 로딩, 페이징 및 기타 많은 기능을 지원하는 combobox 컨트롤입니다.

   ComboBox는 기존 HTML &lt;select> 필드와 유사한 방식으로 작동합니다. 차이점은 valueField를 제출하려면 [숨김](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)이름을 [지정하여 숨겨진](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox) 입력을 만들어야 한다는 것입니다.

* 구성 요소

   [CQ.Ext.Component](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component)

   모든 Ext 구성 요소에 대한 기본 클래스입니다. Component의 모든 하위 클래스는 Container 클래스에서 제공하는 생성, 렌더링 및 파괴의 자동화된 텍스트 구성 요소 라이프사이클에 참여할 [수](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) 있습니다. 구성 요소는 컨테이너를 만들 때 [항목](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) 구성 옵션을 통해 컨테이너에 추가될 수 있습니다.

* componentextractor

   [CQ.wcm.ComponentExtractor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ComponentExtractor)

   ComponentExtractor를 사용하면 웹 사이트/페이지에서 구성 요소를 추출할 수 있습니다.

* componentselector

   [CQ.form.ComponentSelector](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ComponentSelector)

   사용 가능한 구성 요소의 그룹화된 순차 선택

* componentstyles

   [CQ.form.ComponentStyles](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ComponentStyles)

* 합성 필드

   [CQ.form.CompositeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.CompositeField)

   하나의 양식 필드 또는 양식 필드 그룹을 포함하는 패널 기반 복잡한 양식 필드에 대한 기본 클래스입니다.

* 컨테이너

   [CQ.Ext.Container](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container)

   다른 구성 요소가 포함될 수 [있는 CQ.Ext.BoxComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.BoxComponent) 에 대한 기본 클래스입니다. 컨테이너는 포함 항목의 기본 동작(즉, 항목 추가, 삽입 및 제거)을 처리합니다.

   가장 일반적으로 사용되는 컨테이너 클래스는 CQ.Ext. [Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel), [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) 및 [CQ.Ext.TabPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.TabPanel)입니다.

* contentfinder

   [CQ.wcm.ContentFinder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder)

   ContentFinder는 [왼쪽에](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Viewport) 있는 실제 컨텐츠 파인더와 오른쪽에 컨텐츠 프레임이 포함된 두 개의 전문화된 뷰포트입니다.

* contentfindertab

   [CQ.wcm.ContentFinderTab](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinderTab)

   ContentFinderTab은 CQ.wcm.ContentFinder의 탭 패널에 사용되는 기능을 [제공하는 전문 패널입니다](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder). 일반적으로 검색 양식(쿼리 상자)과 검색을 표시하는 데이터 보기를 제공합니다.

* cq.workflow.model.combo

   [CQ.wcm.WorkflowModelCombo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.WorkflowModelCombo)

   WorkflowModelCombo는 사용 가능한 [워크플로우 모델 목록을 보여주는 사용자](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox) 지정된 CQ.Ext.form.ComboBox입니다.

* cq.workflow.model.selector

   [CQ.wcm.WorkflowModelSelector](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.WorkflowModelSelector)

   WorkflowModelSelector는 WorkflowModelCombo와 작업 과정의 축소판 이미지, 그리고 작업 흐름 모델을 만들고 편집하는 단추를 결합합니다.

* createtitewizard

   [CQ.wcm.CreateSiteWizard](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.CreateSiteWizard)

   CreateSiteWizard는 MSM(사이트 만들기)을 위한 단계별 마법사로

* createversiondialog

   [CQ.wcm.CreateVersionDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.CreateVersionDialog)

   CreateVersionDialog는 페이지의 새 버전을 만들 수 있는 대화 상자입니다.

* customcontentpanel

   [CQ.CustomContentPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.CustomContentPanel)

   CustomContentPanel은 CQ.Dialog에서 사용할 수 있는 특수 [종류의 패널입니다](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog).컨텐츠는 대화 상자의 다른 필드와 달리 검색되어 다른 URL로 제출됩니다.

* 주기

   [CQ.Ext.CycleButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton)

   CQ.Ext.menu.CheckItem [요소의 메뉴가 포함된 전문화된 SplitButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.CheckItem) . 단추는 클릭할 때마다 각 메뉴 항목을 자동으로 순환하여 단추의 [변경](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton) 이벤트를 발생시키거나(제공된 경우 단추의 [changeHandler](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton) 함수 호출)를 활성 메뉴 항목에 대해 발생시킵니다.

* dataview

   [CQ.Ext.DataView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DataView)

   사용자 지정 레이아웃 템플릿 및 서식을 사용하여 데이터를 표시하는 메커니즘입니다. DataView는 [CQ.Ext.XTemplate](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.XTemplate) 를 내부 템플릿 메커니즘으로 사용하며 [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store) CQ.Ext.data.Store에 바인딩되므로 스토어의 데이터가 변경되면 변경 내용이 반영되도록 보기가 자동으로 업데이트됩니다.

* 날짜 필드

   [CQ.Ext.form.DateField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField)

   CQ.Ext.DatePicker [드롭다운 및 자동](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker) 날짜 유효성 검사가 포함된 날짜 입력 필드를 제공합니다.

* 날짜 메뉴

   [CQ.Ext.menu.DateMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.DateMenu)

   CQ.Ext. [DatePicker 구성 요소를 포함하는](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker) 메뉴입니다.

* datepicker

   [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker)

   팝업 날짜 선택기입니다. 이 클래스는 DateField [클래스에서](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField) 유효한 날짜를 검색하고 선택할 수 있도록 합니다.

* datetime

   [CQ.form.DateTime](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.DateTime)

   DateTime을 사용하면 CQ.Ext.form.DateField와 CQ. [Ext.form.TimeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField) 를 결합하여 [날짜와 시간을 입력할 수 있습니다](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TimeField).

* 대화 상자

   [CQ 대화 상자](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog)

   대화 상자는 본문에 양식이 있고 바닥글에 단추 그룹이 있는 특별한 종류의 창입니다. 일반적으로 컨텐츠를 편집하는 데 사용되지만 정보만 표시할 수 있습니다.

* dialogfieldset

   [CQ.form.DialogFieldSet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.DialogFieldSet)

   DialogFieldSet은 [Dialog에](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FieldSet) 사용하기 위한 FieldSet [입니다](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog).

* directstore

   [CQ.Ext.data.DirectStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.DirectStore)

   CQ.Ext.data. [DirectProxy 및 CQ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store) 로 구성된 CQ.Ext.data.Store를 [만들 수 있는 소규모 헬퍼 클래스입니다.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.DirectProxy) ExtReader [를](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader) 사용하여 CQ.Cq Ext.DirectSide Server [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Direct) [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.direct.Provider) 와 보다 쉽게 상호 작용할 수 있는 CQ.Ext.data.StoreStore를 만듭니다.

* displayfield

   [CQ.Ext.form.DisplayField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DisplayField)

   유효성이 검증되지 않고 제출되지 않은 표시 전용 텍스트 필드입니다.

* 편집 막대

   [CQ.wcm.EditBar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditBar)

   EditBar를 사용하면 막대의 버튼을 사용하여 컨텐츠를 편집할 수 있습니다.

   여기에 나열되지는 않았지만 EditBar에는 CQ.wcm.EditBase의 모든 [멤버가 있습니다](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditBase).

* 편집기

   [CQ.Ext.Editor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Editor)

   요청 시 표시/숨기기를 처리하고 일부 내장 크기 및 이벤트 처리 논리를 제공하는 기본 편집기 필드입니다.

* editorrid

   [CQ.Ext.grid.EditorGridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.EditorGridPanel)

   이 클래스는 GridPanel [클래스를 확장하여](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) 선택한 [열에](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.Column)셀 편집을 제공합니다. 편집 가능한 열은 [열 구성에서](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.ColumnModel) 편집기를 [제공하여 지정합니다](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.Column).

* 편집 롤오버

   [CQ.wcm.EditRollover](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditRollover)

   EditRollover를 사용하면 두 번 클릭으로 컨텐츠를 편집할 수 있으며 컨텍스트 메뉴를 통해 더 많은 편집 작업을 할 수 있습니다. 편집 가능한 영역은 마우스가 내용 위로 롤오버할 때 프레임으로 표시됩니다.

* 편집자

   [CQ.wcm.FeedImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.FeedImporter)

   FeedImporter를 사용하면 RSS 또는 Atom 피드를 가져오고 각 피드 항목에 대한 페이지를 만들 수 있습니다.

* 필드

   [CQ.Ext.form.Field](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Field)

   기본 이벤트 처리, 크기 조정, 값 처리 및 기타 기능을 제공하는 양식 필드에 대한 기본 클래스입니다.

* fielset

   [CQ.Ext.form.FieldSet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FieldSet)

   [양식](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FormPanel)내에서 항목을 그룹화하는 데 사용되는 표준 컨테이너입니다....

* fileuploadalogbutton

   [CQ.form.FileUploadDialogButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.FileUploadDialogButton)

   FileUploadDialogButton은 FileUploadField를 통해 파일을 업로드하기 위한 새 대화 상자를 여는 단추를 만듭니다. 별도의 형식으로 업로드해야 하는 편집 대화 상자 내에서 사용할 수 있습니다.

* fileuploadfield

   [CQ.form.FileUploadField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.FileUploadField)

   FileUploadField를 사용하면 업로드할 단일 파일을 선택할 수 있습니다.

* findreplacement dialog

   [CQ.wcm.FindReplaceDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.FindReplaceDialog)

   FindReplaceDialog는 페이지와 해당 하위 페이지에서 토큰을 찾고 바꾸는 대화 상자입니다.

* flash

   [CQ.Ext.FlashComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.FlashComponent)

* 격자

   [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)

   이 클래스는 행과 열의 표 형식으로 데이터를 나타내는 구성 요소 기반 그리드 컨트롤의 기본 인터페이스를 나타냅니다.

* groupingstore

   [CQ.Ext.data.GroupingStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.GroupingStore)

   사용 가능한 필드 중 하나별로 레코드를 그룹화하는 기능을 제공하는 전문 저장소 구현입니다. 일반적으로 CQ.Ext.grid. [GroupingView와 함께](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GroupingView) 사용하여 그룹화된 GridPanel에 대한 데이터 모델을 증명합니다.

* 대화 상자

   [CQ.wcm.HeavyMoveDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.HeavyMoveDialog)

   HeavyMoveDialog는 이전에 활성화한 페이지(&#39;무거운&#39; 이동)의 재활성화를 고려하여 페이지와 하위 페이지를 이동하는 대화 상자입니다.

* 숨김

   [CQ.Ext.form.Hidden](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Hidden)

   양식 제출에서 전달해야 하는 양식에 숨겨진 값을 저장하기 위한 기본 숨김 필드.

* historybutton

   [CQ.HistoryButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.HistoryButton)

   HistoryButton은 뒤로 및 앞으로 단추를 쉽게 제공할 수 있는 작은 도우미 클래스입니다. 일반적으로 두 개의 관련 인스턴스가 필요합니다.앞으로 단추 인스턴스는 작업 내역을 처리하는 뒤로 단추 인스턴스에 연결된 간단한 단추입니다.

* htmlitor

   [CQ.Ext.form.HtmlEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.HtmlEditor)

   크기가 작은 HTML 편집기 구성 요소를 제공합니다. 일부 도구 모음 기능은 Safari에서 지원되지 않으며 필요한 경우 자동으로 숨겨집니다. 이러한 사항은 해당되는 구성 옵션에 설명되어 있습니다.

   편집기의 도구 모음 단추에는 buttonTips [속성에 정의된 도구 설명이](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.HtmlEditor) 있습니다.

* iframedialog

   [CQ.IframeDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.IframeDialog)

   iframe의 내용을 표시하고 iframe에서 양식을 허용하는 간단한 대화 상자입니다.

* iframepanel

   [CQ.IframePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.IframePanel)

   iframe이 들어 있는 패널입니다. iframe을 쉽게 만들고 iframe 로드 이벤트를 제공하며 iframe의 컨텐츠에 쉽게 액세스할 수 있습니다.

* inlinetextfield

   [CQ.form.InlineTextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.InlineTextField)

   InlineField는 포커스가 없을 때 레이블로 표시되는 텍스트 필드입니다.

* jsonstore

   [CQ.Ext.data.JsonStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonStore)

   JSON 데이터에서 CQ. [Ext.data.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)Stores를 보다 손쉽게 만들 수 있는 소규모 도우미 클래스입니다. JsonStore는 CQ.Ext.data. [JsonReader로 자동으로 구성됩니다](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader).

* label

   [CQ.Ext.form.Label](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Label)

   기본 레이블 필드.

* languagecopdialog

   [CQ.wcm.LanguageCopyDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.LanguageCopyDialog)

   LanguageCopyDialog는 언어 트리를 복사하는 대화 상자입니다.

* linkchecker

   [CQ.wcm.LinkChecker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.LinkChecker)

   LinkChecker는 사이트에서 외부 링크를 확인하는 도구입니다.

* 목록 보기

   [CQ.Ext.list.ListView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.ListView)

   CQ.Ext.list.ListView는 뷰와 같은 그리드의 빠르고 [가벼운](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) 구현입니다.

* livecopyproperties

   [CQ.wcm.msm.LiveCopyProperties](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.LiveCopyProperties)

   LiveCopyProperties는 Live Copy 속성(관계 상속, 동기화 트리거 및 동기화 작업)을 보고 편집할 수 있는 패널을 제공합니다.

* lvboolean

   [CQ.Ext.list.BooleanColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.BooleanColumn)

   부울 데이터 필드를 렌더링하는 열 정의 클래스입니다. 자세한 내용은 [CQ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) .Ext.list. [Column의 xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) 구성 옵션을참조하십시오.

* lvcolumn

   [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column)

   이 클래스는 ListView의 초기화에 사용할 열 구성 데이터를 캡슐화합니다 [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.ListView).

* lvdatecolumn

   [CQ.Ext.list.DateColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.DateColumn)

   기본 로케일 또는 구성된 [형식에](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.DateColumn)따라 전달된 날짜를 렌더링하는 열 정의 클래스입니다. 자세한 내용은 [CQ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) .Ext.list. [Column의 xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) 구성 옵션을참조하십시오.

* lvnumbercolumn

   [CQ.Ext.list.NumberColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.NumberColumn)

   [형식](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.NumberColumn) 문자열에 따라 숫자 데이터 필드를 렌더링하는 열 정의 클래스입니다. 자세한 내용은 [CQ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) .Ext.list. [Column의 xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) 구성 옵션을참조하십시오.

* mediabrowsedialog

   [CQ.MediaBrowseDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.MediaBrowseDialog)

   **가치 하락:Content[Finder를](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder)사용하여 미디어를 찾아봅니다.**

   MediaBrowseDialog는 미디어 라이브러리를 탐색하는 대화 상자입니다.

* 메뉴

   [CQ.Ext.menu.Menu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Menu)

   메뉴 개체입니다. 메뉴 항목을 추가할 수 있는 컨테이너입니다. 또한 CQ.Ext.menu.DateMenu와 같은 다른 구성 요소를 기반으로 하는 특수 메뉴를 원하는 경우 메뉴를 기본 [클래스로 사용할](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.DateMenu) 수 있습니다.

   메뉴에는 [메뉴 항목](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Item)또는 일반 구성 요소가 포함될 수 [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component)있습니다.

* menubaseitem

   [CQ.Ext.menu.BaseItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.BaseItem)

   메뉴로 렌더링되는 모든 항목의 기본 클래스입니다. BaseItem은 모든 메뉴 구성 요소에서 공유하는 기본 렌더링, 활성화된 상태 관리 및 기본 구성 옵션을 제공합니다.

* menucheckitem

   [CQ.Ext.menu.CheckItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.CheckItem)

   기본적으로 확인란이 포함된 메뉴 항목을 추가하지만 라디오 그룹의 일부일 수도 있습니다.

* menuitem

   [CQ.Ext.menu.Item](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Item)

   하위 메뉴와 같은 메뉴 관련 기능이 필요하고 정적 표시 항목이 아닌 모든 메뉴 항목에 대한 기본 클래스입니다. Item은 메뉴별 활성화를 추가하고 [클릭 처리를 통해](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.BaseItem) CQ.Ext.menu.BaseItem의 기본 기능을 확장합니다.

* 멘토레이터

   [CQ.Ext.menu.Separator](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Separator)

   메뉴 항목의 논리 그룹을 나누는 데 사용되는 구분 기호를 메뉴에 추가합니다. 일반적으로 add()를 호출하거나 항목 구성을 직접 만들지 않고 호출에서 &quot;-&quot;를 사용하여 이러한 구성 중 하나를 추가합니다.

* menutextitem

   [CQ.Ext.menu.TextItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.TextItem)

   정적 텍스트 문자열을 메뉴에 추가합니다. 이 문자열은 일반적으로 머리글이나 그룹 구분 문자로 사용됩니다.

* 메타데이터

   [CQ.dam.form.Metadata](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.dam.form.Metadata)

   메타데이터는 자산 편집기 페이지에서 사용되는 대로 메타데이터 필드에 필요한 정보를 결정하는 필드 세트를 제공합니다.

   다음과 같은 필드를 제공합니다.

* 멀티필드

   [CQ.form.MultiField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MultiField)

   MultiField는 다중 값 속성을 편집하기 위한 편집 가능한 양식 필드 목록입니다.

* mvt

   [CQ.form.MVT](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MVT)

   Multivariate Testing 구성 요소를 사용하여 대체 배너로 표시되는 이미지 세트를 정의하고 편집할 수 있습니다. 클릭스루 비율 통계가 배너당 수집됩니다.

* 알림 받은 편지함

   [CQ.wcm.NotificationInbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.NotificationInbox)

   NotificationInbox를 사용하면 WCM 작업에 구독하고 알림을 관리할 수 있습니다.

* 번호

   [CQ.Ext.form.NumberField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.NumberField)

   자동 키 입력 필터링 및 숫자 유효성 검사를 제공하는 숫자 텍스트 필드입니다.

* offlineimporter

   [CQ.wcm.OfflineImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.OfflineImporter)

   OfflineImporter는 Microsoft Word 문서를 가져와서 AEM 페이지로 변환하는 도구입니다. 이 기능을 사용하면 워드 프로세서를 사용하여 컨텐츠를 오프라인으로 편집할 수 있습니다.

* 소유자 그리기

   [CQ.form.OwnerDraw](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.OwnerDraw)

   OwnerDraw에는 사용자 정의 HTML 코드(직접 입력하거나 URL에서 검색)가 포함될 수 있습니다.

* 호출

   [CQ.Ext.PagingToolbar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.PagingToolbar)

   레코드 양이 증가하면 브라우저가 렌더링하는 데 필요한 시간이 증가합니다. 페이징은 클라이언트와 교환된 데이터의 양을 줄이는 데 사용됩니다.

* 패널

   [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel)

   패널은 애플리케이션 중심의 유저 인터페이스를 위한 완벽한 구성 요소를 제공하는 특정 기능과 구조적 구성 요소를 포함하는 컨테이너입니다.

   패널은 CQ.Ext.Container의 상속을 [통해 만들어집니다](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container).

* paragraph참조

   [CQ.form.ParagraphReference](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ParagraphReference)

   단락 참조 필드에서 페이지를 검색하고 해당 단락 중 하나를 선택할 수 있습니다. 트리거 필드와 연관된 단락 찾아보기 대화 상자로 구성됩니다.

* 암호

   [CQ.form.Password](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Password)

   암호는 CQ.Ext. [form.TextField와](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField) 비슷하지만 값을 비공개로 유지하여 사용자가 중요한 데이터를 입력할 수 있도록 합니다.

* 경로 완성

   [CQ.form.PathCompletion](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathCompletion)

   **가치 하락:CQ[.form.PathField를](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField)대신 사용하십시오**

* 경로 필드

   [CQ.form.PathField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField)

   PathField는 경로 수료로 구성된 경로와 서버 저장소를 검색할 수 있는 CQ.BrowseDialog [를 여는](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.BrowseDialog) 단추를 위해 디자인된 입력 필드입니다. 또한 고급 링크 생성을 위해 페이지 단락을 검색할 수도 있습니다.

* 진행 상황

   [CQ.Ext.ProgressBar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ProgressBar)

   업데이트 가능한 진행률 표시줄 구성 요소입니다. 진행률 표시줄은 두 가지 모드를 지원합니다.수동 및 자동

   수동 모드에서는 사용자 자신의 코드에서 필요에 따라 진행률 표시줄을 표시, 업데이트( [updateProgress](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ProgressBar))하고 삭제할 책임이 있습니다. 이 방법은 진행 상태를 표시하려는 경우에 가장 적합합니다.

* propertygrid

   [CQ.Ext.grid.PropertyGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.PropertyGrid)

   개발 IDE에서 일반적으로 볼 수 있는 기존의 속성 격자를 모방하기 위한 특수 격자 구현 그리드의 각 행은 일부 객체의 속성을 나타내며 데이터는 CQ.Ext.grid.PropertyRecords에서 이름/값 [쌍 세트로](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.PropertyRecord)저장됩니다.

* prop격자

   [CQ.PropertyGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.PropertyGrid)

   PropertyGrid는 개체의 속성을 표시하고 편집하는 데 사용되는 일반 격자입니다.

* 빠른 팁

   [CQ.Ext.QuickTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTip)

   @xtype quicktip 마크업에 지정할 수 있고 전역 CQ.Ext.QuickTips 인스턴스에서 자동으로 관리하는 툴팁에 [대한 전문적인 툴팁 클래스입니다](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTips) . 자세한 사용 정보와 예는 QuickTips 클래스 헤더를 참조하십시오.

* 라디오

   [CQ.Ext.form.Radio](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Radio)

   단일 라디오 필드. 확인란과 동일하지만 입력 유형을 자동으로 설정할 수 있는 편의를 위해 제공됩니다. 그룹의 각 라디오를 같은 이름으로 지정하면 브라우저에서 라디오 그룹화가 자동으로 처리됩니다.

* 무선 그룹

   [CQ.Ext.form.RadioGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.RadioGroup)

   CQ.Ext.form. [Radio 컨트롤의 그룹화](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Radio) 컨테이너입니다.

* 참조 대화 상자

   [CQ.wcm.ReferencesDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ReferencesDialog)

   ReferencesDialog는 페이지에 참조를 표시하기 위한 대화 상자입니다.

* restoretredialog

   [CQ.wcm.RestoreTreeDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.RestoreTreeDialog)

   RestoreTreeDialog는 이전 버전의 트리를 복원하는 대화 상자입니다.

* 복원버전대화 상자

   [CQ.wcm.RestoreVersionDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.RestoreVersionDialog)

   RestoreVersionDialog는 페이지의 이전 버전을 복원하는 대화 상자입니다.

* richtext

   [CQ.form.RichText](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.RichText)

   RichText는 스타일이 지정된 텍스트 정보(리치 텍스트)를 편집할 수 있는 양식 필드를 제공합니다.

   RichText 구성 요소는 현재 다음과 같은 기능을 제공합니다.

* 롤아웃플랜

   [CQ.wcm.msm.RolloutPlan](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutPlan)

   RolloutPlan에서는 페이지 롤아웃 진행률을 보는 대화 상자를 제공합니다. RolloutPlan은 CQ.wcm. [msm.RolloutWizard에 의해 시작됩니다](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutWizard).

* 롤아웃마법사

   [CQ.wcm.msm.RolloutWizard](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutWizard)

   RolloutWizard는 페이지를 롤아웃하는 마법사를 제공합니다. RolloutWizard가 [CQ.wcm.msm.RolloutPlan을 시작합니다](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutPlan).

* searchfield

   [CQ.form.SearchField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SearchField)

   SearchField는 검색 필드를 제공하여 저장소 검색에 사용할 수 있는 드롭다운 목록에 결과를 제공합니다.

* selection

   [CQ.form.Selection](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Selection)

   [선택]을 사용하면 여러 옵션 중에서 선택할 수 있습니다. 옵션은 구성의 일부이거나 JSON 응답에서 로드할 수 있습니다. 선택 항목을 드롭다운(선택) 또는 콤보 상자(더하기 무료 텍스트 입력 선택)로 렌더링할 수 있습니다.

* 사이드 킥이

   [CQ.wcm.Sidekick](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Sidekick)

   사이드 킥은 사용자에게 페이지 편집을 위한 일반적인 도구를 제공하는 부동 헬퍼입니다.

* siteadmin

   [CQ.wcm.SiteAdmin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.SiteAdmin)

   SiteAdmin은 WCM 관리 기능을 제공하는 콘솔입니다.

* siteimporter

   [CQ.wcm.SiteImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.SiteImporter)

   SiteImporter를 사용하면 사용자가 전체 웹 사이트를 가져오고 초기 프로젝트를 만들 수 있습니다.

* 시제필드

   [CQ.form.SizeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SizeField)

   SizeField를 사용하면 너비와 높이를 입력할 수 있습니다(예: 이미지).

* 슬라이더

   [CQ.Ext.Slider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Slider)

   수직 또는 수평 방향, 키보드 조정, 구성 가능한 물리기, 축 클릭 및 애니메이션을 지원하는 슬라이더 모든 컨테이너에 항목으로 추가할 수 있습니다. 사용 예:...

* 슬라이드쇼

   [CQ.form.Slideshow](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Slideshow)

   슬라이드 쇼는 슬라이드쇼로 볼 수 있는 이미지 및 이미지 제목 집합을 정의하고 편집하는 데 사용할 수 있는 구성 요소를 제공합니다.

   Slideshow 구성 요소는 CQ.form. [SmartImage 구성 요소를](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartImage) 기반으로 합니다.

* smartfile

   [CQ.form.SmartFile](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartFile)

   SmartFile은 지능형 파일 업로더입니다.

   Flash 플러그인(버전 >= 9)이 설치되어 있는 경우 업로드를 처리하는 편리한 방법을 제공하는 SWFupload 라이브러리를 사용하여 업로드가 실행됩니다.

* 스마트시대

   [CQ.form.SmartImage](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartImage)

   SmartImage는 지능적인 이미지 업로더입니다. 이미지 맵과 이미지 크로퍼를 정의하는 도구와 같이 업로드된 이미지를 처리하는 도구를 제공합니다.

   구성 요소는 주로 별도의 대화 상자 탭에서 사용하도록 디자인되었습니다.

* 스페이서

   [CQ.Ext.Spacer](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Spacer)

   레이아웃에 상당한 공간을 제공하는 데 사용됩니다.

* 스피너

   [CQ.form.Spinner](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Spinner)

   스피너는 숫자, 날짜 또는 시간 값에 대한 트리거 필드입니다. 제공된 위쪽/아래쪽 트리거, 스크롤 휠이나 키를 사용하여 값을 늘리거나 줄일 수 있습니다.

* 분할 단추

   [CQ.Ext.SplitButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.SplitButton)

   이벤트의 기본 클릭 이벤트와 별도로 이벤트를 실행할 수 있는 내장 드롭다운 화살표를 제공하는 분할 단추. 일반적으로 이 메서드는 기본 단추 동작에 대한 추가 옵션을 제공하는 드롭다운 메뉴를 표시하는 데 사용되지만, 모든 사용자 지정 핸들러는 브라우저 구현을 제공할 수 있습니다.

* 정적

   [CQ.Static](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Static)

   정적 요소를 사용하여 임의의 텍스트나 HTML을 표시할 수 있습니다.

* 통계

   [CQ.wcm.Statistics](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Statistics)

   통계에는 페이지 임프레션이 차트로 표시됩니다. 위젯을 사용하면 기간을 선택할 수 있고 통계를 표시할 수 있습니다.

* 스토어

   [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)

   Store 클래스는 GridPanel, [ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Record) 또는 DataViewStore와 같은 구성 요소에 대한 [입력 데이터를 제공하는 Record](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)개체의 [클라이언트](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)측면 [캐시를](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DataView)캡슐화합니다.

* 추천 필드

   [CQ.form.SuggestField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SuggestField)

   SuggestField는 사용자가 입력한 내용에 따라 제안을 제공합니다.

* 전환기

   [CQ.Switcher](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Switcher)

   전환기는 콘솔의 헤더 막대에 대한 단추 그룹을 제공하여 웹 사이트, 디지털 자산, 도구, 워크플로우 및 보안 간을 전환합니다.

* tableedit

   [CQ.form.TableEdit](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit)

   **가치 하락:CQ[.form.TableEdit2를](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit2)대신 사용하십시오.**

* tableedit2

   [CQ.form.TableEdit2](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit2)

   TableEdit2는 표를 만들기 위한 위젯을 제공합니다.

* 탭 패널

   [CQ.Ext.TabPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.TabPanel)

   기본 탭 컨테이너입니다. TabPanels는 레이아웃 작업을 위해 표준 [CQ.Ext.Panel과](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel) 정확히 유사하게 사용할 수 있지만 하위 구성 요소([`items`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container))를 포함하기 위한 특수 지원을 제공합니다.

* 태그

   [CQ.tagging.TagInputField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.tagging.TagInputField)

   ```
   CQ.tagging.TagInputField
   ```

    는 태그 입력을 위한 양식 위젯입니다. 기존 태그, 자동 완성 및 기타 많은 기능을 포함하는 팝업 메뉴가 있습니다.

* 텍스트 영역

   [CQ.Ext.form.TextArea](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextArea)

   여러 줄로 된 텍스트 필드. 기존 텍스트 영역 필드를 직접 대체하여 사용할 수 있을 뿐만 아니라 자동 크기 조정 지원이 추가되었습니다.

* textbutton

   [CQ.TextButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.TextButton)

   TextButton은 CQ.Ext.Button의 기능이 있는 텍스트 [링크를 제공합니다](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button).

* textfield

   [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField)

   기본 텍스트 필드. 기존 텍스트 입력을 직접 대체하거나 보다 정교한 입력 컨트롤을 위한 기본 클래스로 사용할 수 있습니다(예: CQ.Ext.form.TextArea 및 [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextArea) ) [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox).

* 축소판

   [CQ.form.Thumbnail](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Thumbnail)

* 시간 필드

   [CQ.Ext.form.TimeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TimeField)

   시간 드롭다운 및 자동 시간 유효성 검사가 포함된 시간 입력 필드를 제공합니다. 사용 예:...

* 팁

   [CQ.Ext.Tip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Tip)

   @xtype 팁 모든 팁 기반 클래스에 필요한 [기본 레이아웃과 위치를 제공하는 CQ.Ext](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTip) .QuickTip 및 [CQ.Ext.Tooltip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Tooltip) 의 기본 클래스입니다. 이 클래스는 간단하고 정적으로 배치된 팁에 직접 사용할 수 있습니다.

* titleasparator

   [CQ.menu.TitleSeparator](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.menu.TitleSeparator)

   메뉴 항목의 논리 그룹을 나누는 데 사용되는 구분 기호를 메뉴에 추가합니다. 구분 기호는 제목을 추가로 포함할 수 있습니다.

* 도구 모음

   [CQ.Ext.Toolbar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Toolbar)

   기본 도구 모음 클래스입니다. 도구 모음의 [`defaultType`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) 경우 [`button`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button)도구 모음 요소(도구 모음 컨테이너의 하위 항목)는 거의 모든 유형의 구성 요소일 수 있습니다. 도구 모음 요소는 생성자를 통해 명시적으로 만들 수 있습니다.

* 툴팁

   [CQ.Ext.ToolTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ToolTip)

   대상 요소 위로 마우스를 가져가면 추가 정보를 제공하기 위한 표준 도구 설명 구현입니다. @xtype 툴팁입니다.

* 트레그리드

   [CQ.tree.TreeGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.tree.TreeGrid)

   @xtype treegrid

* 트레파넬

   [CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)

   TreePanel은 트리 구조화된 데이터의 트리 구조 UI 표현을 제공합니다.

   [TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreeNode)에 추가된 TreeNodes는 각 응용 프로그램에서 사용하는 메타데이터를 [특성](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreeNode) 속성에 포함할 수 있습니다.

* 트리거

   [CQ.Ext.form.TriggerField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField)

   클릭 가능한 트리거 단추(기본적으로 combobox처럼 표시)를 추가하는 편리한 TextFields 래퍼를 제공합니다. 트리거에는 기본 작업이 없으므로 onTriggerClick을 무시하여 트리거 클릭 핸들러를 구현할 함수를 지정해야 [합니다](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField). TriggerField는 combobox와 동일하게 렌더링되므로 직접 만들 수 있습니다.

* uloadalog

   [CQ.UploadDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.UploadDialog)

   UploadDialog를 사용하면 사용자가 저장소에 파일을 업로드할 수 있습니다. 새 UploadDialog를 만듭니다.

* userinfo

   [CQ.UserInfo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.UserInfo)

   도구 모음 항목을 사용하여 현재 사용자 이름을 표시하고 사용자 속성 편집 및 가장과 같은 사용자 작업을 허용합니다.

* 뷰포트

   [CQ.Ext.Viewport](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Viewport)

   볼 수 있는 응용 프로그램 영역(브라우저 뷰포트)을 나타내는 특수 컨테이너입니다.

   뷰포트는 문서 본문에 렌더링하고 브라우저 뷰포트 크기에 맞게 자동으로 크기를 조정하고 창 크기를 관리합니다. 생성된 뷰포트는 하나만 있을 수 있습니다.

* 창

   [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)

   응용 프로그램 창으로 사용하기 위한 특수 패널. Windows는 기본적으로 [부동, 크기 조정](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)및 [드래그](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) 가능합니다. Windows를 [최대화하여](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) 뷰포트를 채우고 이전 크기로 복원하며 [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)최소화할 수 있습니다.

* xmlstore

   [CQ.Ext.data.XmlStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.XmlStore)

   XML 데이터에서 CQ. [Ext.data.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)Stores를 보다 쉽게 만들 수 있는 작은 도우미 클래스입니다. XmlStore는 CQ.Ext.data. [XmlReader로 자동으로 구성됩니다](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.XmlReader).

   **보관소의** 다른 경로에서 위젯 정의를 포함하는 유사 xtype을 포함합니다. 페이지 대화 상자에서 가장 일반적으로 사용됩니다. 이 xtype에 대한 실제 JavaScript 위젯 클래스가 없습니다. CQ.Util 클래스의 formatData() 함수에 의해 처리됩니다. 자세한 내용은 이 기술 자료 문서를 참조하십시오.
