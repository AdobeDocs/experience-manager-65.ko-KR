---
title: xtype 사용(클래식 UI)
seo-title: Using xtypes (Classic UI)
description: AEM에서 사용할 수 있는 모든 xtype에 대해 알아봅니다
seo-description: Learn about all the xtypes that are available with AEM
uuid: 6497caa4-2f9b-4f21-9023-88d485fd1d78
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: adb70b43-1b0b-4302-905a-c7612675dabb
exl-id: 06ca4e6d-9ab7-4c5b-905c-07c448632f2b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '6400'
ht-degree: 0%

---

# xtype 사용(클래식 UI){#using-xtypes-classic-ui}

이 페이지에서는 Adobe Experience Manager(AEM)에서 사용할 수 있는 모든 xtype에 대해 설명합니다.

ExtJS 언어에서는 xtype이 클래스에 지정된 기호 이름입니다. 페이지의 &quot;구성 요소 유형&quot; 단락을 읽을 수 있습니다 [ExtJS 2 개요](https://www.sencha.com/learn/overview-of-extjs-2) xtype이 무엇이고 xtype을 사용할 수 있는 방법에 대한 자세한 설명입니다.

AEM에서 사용 가능한 모든 위젯에 대한 전체 정보는 [위젯 API 설명서](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html).

지정된 xtype이 AEM에서 사용되는 구성 요소를 확인하려면 &#39;checkbox&#39;를 관심 있는 xtype으로 대체하여 CRXDE의 다음 Xpath 쿼리를 사용할 수 있습니다.

`//element(*, cq:Widget)[@xtype='checkbox']`

>[!NOTE]
>
>이 페이지에서는 클래식 UI 내에서 ExtJS xtype의 사용에 대해 설명합니다.
>
>Adobe은 표준, 최신 버전 및 [터치 지원 UI](/help/sites-developing/touch-ui-concepts.md) 기준 [Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui) 및 [Granite UI](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components).

## xtype {#xtypes}

Adobe Experience Manager에서 사용할 수 있는 xtype 목록을 아래에 참조하십시오.

* 주석

   [CQ.wcm.Annotation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Annotation)

   대화 상자는 본문에 폼이 있고 바닥글에 단추 그룹이 있는 특별한 종류의 창입니다. 일반적으로 컨텐츠를 편집하는 데 사용되지만 정보만 표시할 수 있습니다.

* araystore

   [CQ.Ext.data.ArrayStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.ArrayStore)

   이전에 &quot;SimpleStore&quot;라고 했습니다.

   만들 작은 도우미 클래스 [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)Array의 데이터를 보다 쉽게 생성할 수 있습니다. ArrayStore는 [CQ.Ext.data.ArrayReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.ArrayReader).

* asseteditor

   [CQ.dam.AssetEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.dam.AssetEditor)

   DAM 관리에 사용되는 자산 편집기.

* assetreferencesearch 대화 상자

   [CQ.wcm.AssetReferenceSearchDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.AssetReferenceSearchDialog)

   AssetReferenceSearchDialog는 페이지가 자산이나 태그를 참조하는 경우 나타나는 대화 상자입니다.

* 블루프린팅

   [CQ.wcm.msm.BlueprintConfig](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintConfig)

   BlueprintConfig는 블루프린트의 Live Copy를 보고 이 블루프린트 속성( 동기화 트리거 및 동기화 작업 )을 편집하는 패널을 제공합니다.

* 블루프린트 상태

   [CQ.wcm.msm.BlueprintStatus](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintStatus)

   BlueprintStatus는 블루프린트 및 Live Copy 관계를 보고 편집할 수 있는 패널을 제공합니다. 브라우징은 [CQ.wcm.msm.BlueprintStatus.Tree](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintStatus.Tree)를 통해 편집 [CQ.wcm.msm.BlueprintConfig](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintConfig) 그리고 [CQ.wcm.msm.LiveCopyProperties](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.LiveCopyProperties).

* box

   [CQ.Ext.BoxComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.BoxComponent)

   임의의 기본 클래스 [구성 요소](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component) 너비 및 높이를 사용하여 상자로 크기를 지정합니다.

   BoxComponent는 크기 조정 및 위치를 위한 자동 상자 모델 조정을 제공하며 구성 요소 렌더링 모델 내에서 올바르게 작동합니다.

* browsedialog

   [CQ.BrowseDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.BrowseDialog)

   BrowseDialog를 사용하면 사용자가 경로를 선택하기 위해 저장소를 찾을 수 있습니다. 일반적으로 [BrowseField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.BrowseField).

* browsefield

   [CQ.form.BrowseField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.BrowseField)

   **사용되지 않음: 사용 [CQ.form.PathField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField) 대신**

* 벌커디터

   [CQ.wcm.BulkEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor)

   BulkEditor에서는 검색 결과를 편집할 검색 엔진 및 그리드를 제공합니다.

   BulkEditor는 HTML 양식에 삽입해야 합니다(가져오기 기능에 필요). 이 기능은 [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog).

* bulkeditorform

   [CQ.wcm.BulkEditorForm](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditorForm)

   BulkEditorForm에서는 [CQ.wcm.BulkEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor) HTML 양식으로 둘러싸입니다. 독립 실행형 버전 [CQ.wcm.BulkEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor), 가져오기 단추에는 HTML 양식이 필요합니다.

* 단추

   [CQ.Ext.Button](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button)

   단순 단추 클래스

* 단추 그룹

   [CQ.Ext.ButtonGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ButtonGroup)

   단추 그룹에 대한 컨테이너입니다.

* 차트

   [CQ.Ext.Chart.Chart](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart)

   CQ.Ext.Chart 패키지는 플래시 기반 차트로 데이터를 시각화하는 기능을 제공합니다. 각 차트는 CQ.Ext.data.Store에 직접 바인딩되므로 차트의 자동 업데이트를 수행할 수 있습니다. 차트의 모양과 느낌을 변경하려면 [chartStyle](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart) 및 [extraStyle](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart) 구성 옵션.

* 확인란

   [CQ.Ext.form.Checkbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Checkbox)

   단일 확인란 필드. 기존 확인란 필드를 직접 대체하여 사용할 수 있습니다.

* checkboxgroup

   [CQ.Ext.form.CheckboxGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.CheckboxGroup)

   그룹화 컨테이너 [CQ.Ext.form.Checkbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Checkbox) 컨트롤

* clearcombo

   [CQ.form.ClearableComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ClearableComboBox)

   ClearableComboBox는 값을 지울 트리거가 있는 편집할 수 없는 콤보 상자입니다.

* colorfield

   [CQ.form.ColorField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ColorField)

   ColorField를 사용하면 사용자가 직접 또는 [CQ.Ext.ColorMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorMenu).

* colorlist

   [CQ.form.ColorList](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ColorList)

   ColorList를 사용하면 사용자가 편집 가능한 목록에서 색상을 선택할 수 있습니다.

* colormenu

   [CQ.Ext.menu.ColorMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.ColorMenu)

   메뉴를 포함하는 메뉴 [CQ.Ext.ColorPalette](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorPalette) 구성 요소.

* 색상 팔레트

   [CQ.Ext.ColorPalette](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorPalette)

   색상을 선택하기 위한 간단한 색상 팔레트 클래스입니다. 팔레트는 모든 컨테이너에 렌더링할 수 있습니다.

* 콤보

   [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)

   자동 완료, 원격 로드, 페이징 및 기타 많은 기능을 지원하는 콤보 상자 컨트롤입니다.

   ComboBox는 기존 HTML과 유사한 방식으로 작동합니다 &lt;select> 필드. 차이점은 다음과 같습니다 [valueField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)를 지정하는 경우 [hiddenName](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox) 숨겨진 입력을 만들려면

* 구성 요소

   [CQ.Ext.Component](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component)

   모든 Ext 구성 요소의 기본 클래스입니다. 구성 요소의 모든 하위 클래스는 [컨테이너](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) 클래스 이름을 지정합니다. 구성 요소는 [항목](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) 컨테이너 생성 시 구성 옵션.

* compentextractor

   [CQ.wcm.ComponentExtractor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ComponentExtractor)

   ComponentExtractor를 사용하면 사용자가 웹 사이트/페이지에서 구성 요소를 추출할 수 있습니다.

* 구성 요소 선택기

   [CQ.form.ComponentSelector](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ComponentSelector)

   사용 가능한 구성 요소의 그룹화된 순차 선택.

* 구성 요소 스타일

   [CQ.form.ComponentStyles](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ComponentStyles)

* 복합 영역

   [CQ.form.CompositeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.CompositeField)

   한 개의 양식 필드 또는 양식 필드 그룹을 포함하는 복합 양식 필드에 대한 패널 기반 클래스입니다.

* 컨테이너

   [CQ.Ext.Container](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container)

   임의의 기본 클래스 [CQ.Ext.BoxComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.BoxComponent) 에는 다른 구성 요소가 포함될 수 있습니다. 컨테이너는 포함 항목의 기본 동작을 처리합니다. 즉, 항목을 추가, 삽입 및 제거합니다.

   가장 일반적으로 사용되는 Container 클래스는 [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel), [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) 및 [CQ.Ext.TabPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.TabPanel).

* contentfinder

   [CQ.wcm.ContentFinder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder)

   ContentFinder는 전문 두 개의 열입니다 [뷰포트](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Viewport) 여기에는 왼쪽의 실제 컨텐츠 파인더와 오른쪽의 컨텐츠 프레임이 포함됩니다.

* contentfindertab

   [CQ.wcm.ContentFinderTab](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinderTab)

   ContentFinderTab은 [CQ.wcm.ContentFinder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder). 일반적으로 검색 양식(쿼리 상자)과 검색을 표시하는 데이터 보기가 제공됩니다.

* cq.workflow.model.combo

   [CQ.wcm.WorkflowModelCombo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.WorkflowModelCombo)

   WorkflowModelCombo는 사용자 지정된 것입니다 [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox) 사용 가능한 워크플로우 모델 목록을 표시합니다.

* cq.workflow.model.selector

   [CQ.wcm.WorkflowModelSelector](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.WorkflowModelSelector)

   WorkflowModelSelector는 WorkflowModelCombo와 워크플로우의 축소판 이미지를 결합하고, Workflow 모델을 만들고 편집하는 단추를 결합합니다.

* createsitewizard

   [CQ.wcm.CreateSiteWizard](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.CreateSiteWizard)

   CreateSiteWizard는 MSM(SiteWizard) 사이트를 만드는 단계별 마법사입니다.

* createversiondialog

   [CQ.wcm.CreateVersionDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.CreateVersionDialog)

   CreateVersionDialog는 페이지의 새 버전을 만들 수 있는 대화 상자입니다.

* customcontentpanel

   [CQ.CustomContentPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.CustomContentPanel)

   CustomContentPanel은 에서 사용할 수 있는 특별한 종류의 패널입니다 [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog): 해당 콘텐츠는 대화 상자의 다른 필드와 다른 URL로 검색됩니다.

* 주기

   [CQ.Ext.CycleButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton)

   메뉴의 특수 SplitButton [CQ.Ext.menu.CheckItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.CheckItem) 요소를 생성하지 않습니다. 버튼을 클릭하면 각 메뉴 항목을 자동으로 순환하여 버튼을 [변경](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton) 이벤트(또는 단추의 호출) [changeHandler](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton) 함수(제공된 경우)를 채울 수 있습니다.

* dataview

   [CQ.Ext.DataView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DataView)

   사용자 지정 레이아웃 템플릿 및 서식을 사용하여 데이터를 표시하는 메커니즘입니다. DataView는 [CQ.Ext.XTemplate](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.XTemplate) 를 내부 템플릿 메커니즘으로 사용하여 [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store) 따라서 저장소의 데이터가 변경되면 변경 사항을 반영하도록 보기가 자동으로 업데이트됩니다.

* datefield

   [CQ.Ext.form.DateField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField)

   날짜 입력 필드에 [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker) 드롭다운 및 자동 날짜 유효성 검사.

* datemenu

   [CQ.Ext.menu.DateMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.DateMenu)

   메뉴를 포함하는 메뉴 [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker) 구성 요소.

* datepicker

   [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker)

   팝업 날짜 선택기. 이 클래스는 [DateField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField) 클래스를 사용하여 유효한 날짜를 검색하고 선택할 수 있습니다.

* datetime

   [CQ.form.DateTime](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.DateTime)

   DateTime을 사용하면 사용자가 조합하여 날짜와 시간을 입력할 수 있습니다 [CQ.Ext.form.DateField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField) 및 [CQ.Ext.form.TimeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TimeField).

* 사용할 수 없게 됩니다

   [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog)

   대화 상자는 본문에 폼이 있고 바닥글에 단추 그룹이 있는 특별한 종류의 창입니다. 일반적으로 컨텐츠를 편집하는 데 사용되지만 정보만 표시할 수 있습니다.

* dialgfieldset

   [CQ.form.DialogFieldSet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.DialogFieldSet)

   DialogFieldSet은 [FieldSet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FieldSet) 에서 사용 [대화 상자](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog).

* directstore

   [CQ.Ext.data.DirectStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.DirectStore)

   만들 작은 도우미 클래스 [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store) 다음으로 구성 [CQ.Ext.data.DirectProxy](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.DirectProxy) 및 [CQ.Ext.data.JsonReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader) 상호작용을 하다 [CQ.Ext.Direct](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Direct) 서버측 [공급자](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.direct.Provider) 더 쉬워

* displayfield

   [CQ.Ext.form.DisplayField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DisplayField)

   검증되지 않고 제출되지 않은 표시 전용 텍스트 필드입니다.

* 편집 막대

   [CQ.wcm.EditBar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditBar)

   EditBar를 사용하면 막대의 버튼을 사용하여 컨텐츠를 편집할 수 있습니다.

   여기에 나열되지는 않지만 EditBar에는 [CQ.wcm.EditBase](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditBase).

* 편집기

   [CQ.Ext.Editor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Editor)

   요청 시 표시/숨기기를 처리하고 기본 제공 크기 조정 및 이벤트 처리 논리를 사용하는 기본 편집기 필드입니다.

* editorgrid

   [CQ.Ext.grid.EditorGridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.EditorGridPanel)

   이 클래스는 [GridPanel 클래스](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) 선택 영역에 셀 편집을 제공하려면 [열](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.Column). 편집 가능한 열은 [편집기](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.ColumnModel) 에서 [열 구성](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.Column).

* 편집 롤오버

   [CQ.wcm.EditRollover](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditRollover)

   EditRollover를 사용하면 두 번 클릭으로 컨텐츠를 편집할 수 있고 컨텍스트 메뉴를 통해 더 많은 편집 작업을 수행할 수 있습니다. 편집 가능한 영역은 마우스가 컨텐츠를 스크롤할 때 프레임으로 표시됩니다.

* 미디어 포터

   [CQ.wcm.FeedImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.FeedImporter)

   FeedImporter를 사용하면 RSS 또는 Atom 피드를 가져와 각 피드 항목에 대한 페이지를 만들 수 있습니다.

* 필드

   [CQ.Ext.form.Field](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Field)

   기본 이벤트 처리, 크기 조정, 값 처리 및 기타 기능을 제공하는 양식 필드의 기본 클래스입니다.

* fieldset

   [CQ.Ext.form.FieldSet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FieldSet)

   내부 항목을 그룹화하는 데 사용되는 표준 컨테이너 [양식](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FormPanel). ...

* fileuploadalogbutton

   [CQ.form.FileUploadDialogButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.FileUploadDialogButton)

   FileUploadDialogButton은 FileUploadField를 통해 파일을 업로드하기 위한 새 대화 상자를 여는 단추를 만듭니다. 업로드가 별도의 양식으로 수행되어야 하는 편집 대화 상자에서 사용할 수 있습니다.

* fileuploadfield

   [CQ.form.FileUploadField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.FileUploadField)

   FileUploadField를 사용하면 사용자가 업로드할 단일 파일을 선택할 수 있습니다.

* finplacedialog

   [CQ.wcm.FindReplaceDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.FindReplaceDialog)

   FindReplaceDialog는 페이지와 해당 하위 페이지에서 토큰을 찾아서 바꾸는 대화 상자입니다.

* flash

   [CQ.Ext.FlashComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.FlashComponent)

* 그리드

   [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)

   이 클래스는 행과 열의 테이블 형식으로 데이터를 나타내는 구성 요소 기반 그리드 컨트롤의 기본 인터페이스를 나타냅니다.

* groupingstore

   [CQ.Ext.data.GroupingStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.GroupingStore)

   사용 가능한 필드 중 하나별로 레코드를 그룹화하는 기능을 제공하는 전문 저장소 구현입니다. 일반적으로 와 함께 사용됩니다 [CQ.Ext.grid.GroupingView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GroupingView) 그룹화된 GridPanel에 대한 데이터 모델을 입증하기 위해

* Heartmovedialog

   [CQ.wcm.HeavyMoveDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.HeavyMoveDialog)

   HeavyMoveDialog는 이전에 활성화한 페이지(&#39;무거운&#39; 이동)의 재활성화를 고려하여 페이지와 해당 하위 페이지를 이동하는 대화 상자입니다.

* 숨김

   [CQ.Ext.form.Hidden](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Hidden)

   양식 제출에서 전달해야 하는 양식에 숨겨진 값을 저장하기 위한 기본 숨김 필드.

* historybutton

   [CQ.HistoryButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.HistoryButton)

   HistoryButton은 뒤로 및 앞으로 단추를 쉽게 제공할 수 있는 작은 도우미 클래스입니다. 일반적으로 두 개의 관련 인스턴스가 필요합니다. 앞으로 단추 인스턴스는 기록을 처리하는 뒤로 단추 인스턴스에 연결된 간단한 단추입니다.

* htmleditor

   [CQ.Ext.form.HtmlEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.HtmlEditor)

   경량 HTML 편집기 구성 요소를 제공합니다. 일부 도구 모음 기능은 Safari에서 지원되지 않으며, 필요한 경우 자동으로 숨겨집니다. 이러한 구성 요소는 적절한 구성 옵션에 기록됩니다.

   편집기의 도구 모음 단추에는 [buttonTips](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.HtmlEditor) 속성을 사용합니다.

* iframedialog

   [CQ.IframeDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.IframeDialog)

   iframe의 내용을 보여 주고 iframe에서 양식을 허용하는 일반 대화 상자입니다.

* iframepanel

   [CQ.IframePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.IframePanel)

   iframe이 포함된 패널. iframe을 쉽게 만들고 iframe 로드 이벤트를 사용할 수 있으며 iframe의 컨텐츠에 쉽게 액세스할 수 있습니다.

* inlinetextfield

   [CQ.form.InlineTextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.InlineTextField)

   InlineField는 포커스에 없을 때 레이블로 표시되는 텍스트 필드입니다.

* jsonstore

   [CQ.Ext.data.JsonStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonStore)

   만들 작은 도우미 클래스 [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)JSON 데이터의 가 더 쉽습니다. Json 저장소는 [CQ.Ext.data.JsonReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader).

* 레이블

   [CQ.Ext.form.Label](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Label)

   기본 레이블 필드입니다.

* lanagecopydialog

   [CQ.wcm.LanguageCopyDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.LanguageCopyDialog)

   LanguageCopyDialog는 언어 트리를 복사하는 대화 상자입니다.

* linkchecker

   [CQ.wcm.LinkChecker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.LinkChecker)

   LinkChecker는 사이트에서 외부 링크를 확인하는 도구입니다.

* listview

   [CQ.Ext.list.ListView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.ListView)

   CQ.Ext.list.ListView는 [그리드](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) 보기.

* livecopyproperties

   [CQ.wcm.msm.LiveCopyProperties](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.LiveCopyProperties)

   LiveCopyProperties는 Live Copy 속성( 관계 상속, 동기화 트리거 및 동기화 작업 )을 보고 편집할 수 있는 패널을 제공합니다.

* lvboolean 열

   [CQ.Ext.list.BooleanColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.BooleanColumn)

   부울 데이터 필드를 렌더링하는 열 정의 클래스입니다. 자세한 내용은 [xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) 구성 옵션 [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) 자세한 내용

* lvcolumn

   [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column)

   이 클래스는 열 구성 데이터를 캡슐화하여 [ListView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.ListView).

* lvdatecolcolumn

   [CQ.Ext.list.DateColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.DateColumn)

   기본 로케일 또는 구성된 로케일에 따라 전달된 날짜를 렌더링하는 열 정의 클래스입니다 [포맷](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.DateColumn). 자세한 내용은 [xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) 구성 옵션 [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) 자세한 내용

* lvnumbercolumn

   [CQ.Ext.list.NumberColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.NumberColumn)

   숫자 데이터 필드를 [포맷](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.NumberColumn) 문자열. 자세한 내용은 [xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) 구성 옵션 [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) 자세한 내용

* mediabrowsedialog

   [CQ.MediaBrowseDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.MediaBrowseDialog)

   **사용되지 않음: 사용 [컨텐츠 파인더](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder) 미디어를 대신 탐색합니다.**

   MediaBrowseDialog는 미디어 라이브러리를 탐색하기 위한 대화 상자입니다.

* 메뉴

   [CQ.Ext.menu.Menu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Menu)

   메뉴 개체. 메뉴 항목을 추가할 수 있는 컨테이너입니다. 다른 구성 요소(예: [CQ.Ext.menu.DateMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.DateMenu) 예).

   메뉴에는 다음 중 하나가 포함될 수 있습니다 [메뉴 항목](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Item), 또는 일반 [구성 요소](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component)s.

* 메뉴 항목

   [CQ.Ext.menu.BaseItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.BaseItem)

   메뉴에 렌더링되는 모든 항목의 기본 클래스입니다. BaseItem은 기본 렌더링, 활성화된 상태 관리 및 모든 메뉴 구성 요소가 공유하는 기본 구성 옵션을 제공합니다.

* 메뉴 체크 항목

   [CQ.Ext.menu.CheckItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.CheckItem)

   기본적으로 확인란을 포함하지만 라디오 그룹의 일부일 수도 있는 메뉴 항목을 추가합니다.

* 메뉴 항목

   [CQ.Ext.menu.Item](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Item)

   메뉴 관련 기능(예: 하위 메뉴)이 필요하고 정적 표시 항목이 아닌 모든 메뉴 항목에 대한 기본 클래스입니다. 항목은 의 기본 기능을 확장합니다. [CQ.Ext.menu.BaseItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.BaseItem) 메뉴별 활성화를 추가하고 처리를 클릭합니다.

* 멘세이파레이터

   [CQ.Ext.menu.Separator](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Separator)

   메뉴 항목의 논리 그룹을 분할하는 데 사용되는 메뉴에 구분 기호 모음을 추가합니다. 일반적으로 add() 또는 항목 구성에 직접 만들지 않고 &quot;-&quot;를 사용하여 이러한 중 하나를 추가합니다.

* menutextem

   [CQ.Ext.menu.TextItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.TextItem)

   일반적으로 머리글이나 그룹 구분 기호로 사용되는 메뉴에 정적 텍스트 문자열을 추가합니다.

* 메타데이터

   [CQ.dam.form.Metadata](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.dam.form.Metadata)

   메타데이터는 메타데이터 필드에 필요한 정보를 결정하는 필드 세트를 제공합니다(예: 자산 편집기 페이지).

   여기에서는 다음 필드를 제공합니다.

* 멀티필드

   [CQ.form.MultiField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MultiField)

   MultiField는 다중 값 속성을 편집하기 위한 편집 가능한 양식 필드 목록입니다.

* mvt

   [CQ.form.MVT](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MVT)

   Multivariate Testing 구성 요소를 사용하여 배너로 표시되는 이미지 집합을 정의하고 편집할 수 있습니다. 클릭스루 비율 통계가 배너당 수집됩니다.

* notificationinbox

   [CQ.wcm.NotificationInbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.NotificationInbox)

   NotificationInbox를 사용하면 WCM 작업에 가입하고 알림을 관리할 수 있습니다.

* numberfield

   [CQ.Ext.form.NumberField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.NumberField)

   자동 키 필터링 및 숫자 유효성 검사를 제공하는 숫자 텍스트 필드입니다.

* offlineimporter

   [CQ.wcm.OfflineImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.OfflineImporter)

   OfflineImporter는 Microsoft Word 문서를 AEM 페이지로 가져와서 변환하는 도구입니다. 이 기능을 사용하면 워드 프로세서를 사용하여 컨텐츠를 오프라인으로 편집할 수 있습니다.

* 소유자 그리기

   [CQ.form.OwnerDraw](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.OwnerDraw)

   OwnerDraw에는 사용자 정의 HTML 코드(직접 입력되었거나 URL에서 검색됨)가 포함될 수 있습니다.

* 페이징

   [CQ.Ext.PagingToolbar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.PagingToolbar)

   레코드 수가 증가하면 브라우저가 이 레코드를 렌더링하는 데 필요한 시간이 증가합니다. 페이징은 클라이언트와 교환되는 데이터 양을 줄이는 데 사용됩니다.

* 패널

   [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel)

   패널은 특정 기능과 구조적 구성 요소를 갖춘 컨테이너로, 응용 프로그램 기반 사용자 인터페이스에 완벽한 빌딩 블록으로 만듭니다.

   패널은, 그들이 상속한 것에 의해 [CQ.Ext.Container](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container).

* paragraph 참조

   [CQ.form.ParagraphReference](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ParagraphReference)

   단락 참조 필드에서 페이지를 탐색하고 해당 단락 중 하나를 선택할 수 있습니다. 트리거 필드와 관련 단락 찾아보기 대화 상자로 구성됩니다.

* 암호

   [CQ.form.Password](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Password)

   암호는 [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField) 그러나 은 값을 비공개로 유지하므로 사용자가 중요한 데이터를 입력할 수 있습니다.

* 경로 완료

   [CQ.form.PathCompletion](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathCompletion)

   **사용되지 않음: 사용 [CQ.form.PathField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField) 대신**

* 경로 필드

   [CQ.form.PathField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField)

   PathField는 경로 완료가 가능한 경로용으로 설계된 입력 필드이며 [CQ.BrowseDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.BrowseDialog) 서버 저장소를 검색할 수 있습니다. 고급 링크 생성을 위해 페이지 단락을 검색할 수도 있습니다.

* 진행 상황

   [CQ.Ext.ProgressBar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ProgressBar)

   업데이트 가능한 진행률 표시줄 구성 요소입니다. 진행률 표시줄은 두 가지 다른 모드를 지원합니다. 수동 및 자동.

   수동 모드에서는 [updateProgress](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ProgressBar))을 클릭하여 코드에서 필요에 따라 진행률 표시줄을 지웁니다. 이 메서드는 진행률을 표시하려는 경우에 가장 적합합니다.

* pertygrid

   [CQ.Ext.grid.PropertyGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.PropertyGrid)

   개발 IDE에서 일반적으로 볼 수 있는 것과 같이 기존 속성 그리드를 모방하기 위한 전문 그리드 구현입니다. 그리드의 각 행은 일부 객체의 속성을 나타내며 데이터는에서 이름/값 쌍 집합으로 저장됩니다. [CQ.Ext.grid.PropertyRecord](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.PropertyRecord)s.

* prop격자

   [CQ.PropertyGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.PropertyGrid)

   PropertyGrid는 개체의 속성을 표시하고 편집하는 데 사용되는 일반 그리드입니다.

* 빠른 팁

   [CQ.Ext.QuickTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTip)

   @xtype quicktip 마크업에 지정할 수 있고 글로벌 플러그인에서 자동으로 관리할 수 있는 도구 설명에 대한 전문적인 도구 설명 클래스입니다 [CQ.Ext.QuickTips](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTips) 인스턴스. 추가 사용 세부 사항 및 예는 QuickTips 클래스 헤더를 참조하십시오.

* 라디오

   [CQ.Ext.form.Radio](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Radio)

   단일 라디오 필드. 확인란과 동일하지만 입력 유형을 자동으로 설정할 수 있도록 편의를 제공합니다. 라디오 그룹은 그룹의 각 라디오를 동일한 이름으로 지정하면 브라우저에 의해 자동으로 처리됩니다.

* 무선 그룹

   [CQ.Ext.form.RadioGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.RadioGroup)

   그룹화 컨테이너 [CQ.Ext.form.Radio](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Radio) 컨트롤

* 참조 대화 상자

   [CQ.wcm.ReferencesDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ReferencesDialog)

   참조 대화 상자는 페이지에 참조를 표시하는 대화 상자입니다.

* restoretreedialog

   [CQ.wcm.RestoreTreeDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.RestoreTreeDialog)

   RestoreTreeDialog는 이전 버전의 트리를 복원하는 대화 상자입니다.

* restoreversiondialog

   [CQ.wcm.RestoreVersionDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.RestoreVersionDialog)

   RestoreVersionDialog는 이전 버전의 페이지를 복원하는 대화 상자입니다.

* richtext

   [CQ.form.RichText](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.RichText)

   RichText는 스타일이 지정된 텍스트 정보(리치 텍스트)를 편집하는 양식 필드를 제공합니다.

   RichText 구성 요소는 현재 다음 기능을 제공합니다.

* rolloutplan

   [CQ.wcm.msm.RolloutPlan](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutPlan)

   RolloutPlan은 페이지 롤아웃 진행 상태를 보는 대화 상자를 제공합니다. RolloutPlan은 [CQ.wcm.msm.RolloutWizard](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutWizard).

* 롤아웃 마법사

   [CQ.wcm.msm.RolloutWizard](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutWizard)

   롤아웃 마법사는 페이지를 롤아웃하는 마법사를 제공합니다. RolloutWizard가 [CQ.wcm.msm.RolloutPlan](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutPlan).

* searchfield

   [CQ.form.SearchField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SearchField)

   SearchField는 리포지토리 검색에 사용할 수 있는 드롭다운 목록에 결과를 제공하는 검색 필드를 제공합니다.

* 선택

   [CQ.form.Selection](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Selection)

   선택 기능을 사용하면 여러 옵션 중에서 선택할 수 있습니다. 옵션은 구성의 일부이거나 JSON 응답에서 로드될 수 있습니다. 선택 항목을 드롭다운(선택) 또는 콤보 상자(더하기 자유 텍스트 항목 선택)로 렌더링할 수 있습니다.

* 사이드 킥의

   [CQ.wcm.Sidekick](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Sidekick)

   사이드킥은 사용자에게 페이지 편집을 위한 공통 도구를 제공하는 부동 도우미입니다.

* siteadmin

   [CQ.wcm.SiteAdmin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.SiteAdmin)

   SiteAdmin 은 WCM 관리 기능을 제공하는 콘솔입니다.

* siteimporter

   [CQ.wcm.SiteImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.SiteImporter)

   SiteImporter를 사용하면 사용자가 전체 웹 사이트를 가져오고 초기 프로젝트를 만들 수 있습니다.

* sizefield

   [CQ.form.SizeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SizeField)

   SizeField를 사용하면 너비와 높이를 입력할 수 있습니다(예: 이미지).

* 슬라이더

   [CQ.Ext.Slider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Slider)

   수직 또는 수평 방향, 키보드 조정, 구성 가능한 스냅, 축 클릭 및 애니메이션을 지원하는 슬라이더 어떤 컨테이너에나 항목으로 추가할 수 있습니다. 사용 예: ...

* 슬라이드 쇼

   [CQ.form.Slideshow](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Slideshow)

   Slideshow는 슬라이드쇼로 표시될 수 있는 이미지 및 이미지 제목 집합을 정의하고 편집하는 데 사용할 수 있는 구성 요소를 제공합니다.

   Slideshow 구성 요소는 [CQ.form.SmartImage](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartImage) 구성 요소.

* smartfile

   [CQ.form.SmartFile](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartFile)

   SmartFile은 지능형 파일 업로더입니다.

   Flash 플러그인(버전 >= 9)이 설치되어 있으면 업로드를 처리하는 편리한 방법을 제공하는 SWFupload 라이브러리를 사용하여 업로드를 실행합니다.

* 스마트 시대

   [CQ.form.SmartImage](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartImage)

   SmartImage는 지능형 이미지 업로더입니다. 이미지 맵과 이미지 크로퍼를 정의하는 도구 등 업로드된 이미지를 처리하는 도구를 제공합니다.

   구성 요소는 주로 별도의 대화 상자에서 사용하기 위해 설계되었습니다.

* 스페이서

   [CQ.Ext.Spacer](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Spacer)

   레이아웃에 큰 공간을 제공하는 데 사용됩니다.

* 스핀

   [CQ.form.Spinner](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Spinner)

   회전자는 숫자, 날짜 또는 시간 값에 대한 트리거 필드입니다. 제공된 위쪽 및 아래쪽 트리거, 스크롤 휠이나 키를 사용하여 값을 늘리고 줄일 수 있습니다.

* 분할 단추

   [CQ.Ext.SplitButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.SplitButton)

   버튼의 기본 클릭 이벤트와 별도로 이벤트를 실행할 수 있는 내장 드롭다운 화살표를 제공하는 분할 단추입니다. 일반적으로 기본 단추 작업에 대한 추가 옵션을 제공하는 드롭다운 메뉴를 표시하는 데 사용되지만 사용자 지정 처리기는 Rowclick 구현을 제공할 수 있습니다.

* 정적

   [CQ.Static](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Static)

   정적 을 사용하여 임의 텍스트 또는 HTML을 표시할 수 있습니다.

* 통계

   [CQ.wcm.Statistics](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Statistics)

   통계 에는 페이지 노출 수가 차트로 표시됩니다. 위젯에서는 기간을 선택할 수 있으며, 위젯에 대한 통계가 표시됩니다.

* 스토어

   [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)

   Store 클래스는 클라이언트 측 캐시를 캡슐화합니다. [레코드](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Record) 구성 요소에 대한 입력 데이터를 제공하는 객체(예: [그리드 패널](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel), [ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)또는 [DataView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DataView).

* 추천 필드

   [CQ.form.SuggestionField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SuggestField)

   Suggefield는 사용자에게 항목을 기반으로 제안을 제공합니다.

* 전환기

   [CQ.Switcher](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Switcher)

   전환기는 콘솔의 헤더 막대에서 웹 사이트, 디지털 자산, 도구, 워크플로우 및 보안 간을 전환할 수 있는 단추 그룹을 제공합니다.

* tableedit

   [CQ.form.TableEdit](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit)

   **사용되지 않음: 사용 [CQ.form.TableEdit2](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit2) 을 가리키도록 업데이트하는 것이 좋습니다.**

* tableedit2

   [CQ.form.TableEdit2](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit2)

   TableEdit2는 표를 만드는 위젯을 제공합니다.

* 표 패널

   [CQ.Ext.TabPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.TabPanel)

   기본 탭 컨테이너입니다. TabPanels는 표준 패널과 동일하게 사용할 수 있습니다 [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel) 레이아웃을 위해 하지만 하위 구성 요소([`items`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container)).

* 태그

   [CQ.tagging.TagInputField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.tagging.TagInputField)

   ```
   CQ.tagging.TagInputField
   ```

   는 태그를 입력하는 양식 위젯입니다. 기존 태그에서 선택할 수 있는 팝업 메뉴가 있고 자동 완성 및 기타 많은 기능이 포함되어 있습니다.

* 텍스트 영역

   [CQ.Ext.form.TextArea](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextArea)

   여러 줄 텍스트 필드. 기존 텍스트 영역 필드에 대한 직접 대체 요소로 사용할 수 있으며 자동 크기 조정을 지원합니다.

* 텍스트 단추

   [CQ.TextButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.TextButton)

   TextButton은 [CQ.Ext.Button](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button).

* 텍스트 필드

   [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField)

   기본 텍스트 필드. 기존 텍스트 입력을 직접 대체하거나 보다 정교한 입력 컨트롤(예: [CQ.Ext.form.TextArea](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextArea) 및 [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)).

* 축소판

   [CQ.form.Thumbnail](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Thumbnail)

* timefield

   [CQ.Ext.form.TimeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TimeField)

   시간 입력 필드에 시간 드롭다운 및 자동 시간 유효성 검사를 제공합니다. 사용 예: ...

* 팁

   [CQ.Ext.Tip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Tip)

   @xtype tip 이 클래스는 [CQ.Ext.QuickTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTip) 및 [CQ.Ext.Tooltip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Tooltip) 모든 팁 기반 클래스에 필요한 기본 레이아웃 및 위치를 제공합니다. 이 클래스는 간단하고 정적으로 위치한 팁에 직접 사용할 수 있습니다.

* 제목 구분 기호

   [CQ.menu.TitleSeparator](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.menu.TitleSeparator)

   메뉴 항목의 논리 그룹을 분할하는 데 사용되는 메뉴에 구분 기호 모음을 추가합니다. 구분 기호는 제목을 추가로 옮길 수 있습니다.

* 도구 모음

   [CQ.Ext.Toolbar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Toolbar)

   기본 도구 모음 클래스입니다. 하지만 [`defaultType`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) 도구 모음은 [`button`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button), 도구 모음 요소(도구 모음 컨테이너의 하위 항목)는 거의 모든 유형의 구성 요소일 수 있습니다. 도구 모음 요소는 생성자를 통해 명시적으로 만들 수 있습니다.

* 도구 설명

   [CQ.Ext.ToolTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ToolTip)

   대상 요소 위로 마우스를 가져가면 추가 정보를 제공하는 표준 도구 설명 구현입니다. @xtype 도구 설명.

* 트레그리드

   [CQ.tree.TreeGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.tree.TreeGrid)

   @xtype

* 트리파넬

   [CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)

   TreePanel은 트리 구조 데이터의 트리 구조 UI 표현을 제공합니다.

   [TreeNode](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreeNode)TreePanel에 추가된 각 메타데이터에는 애플리케이션이 사용하는 메타데이터가 포함될 수 있습니다 [속성](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreeNode) 속성을 사용합니다.

* 트리거

   [CQ.Ext.form.TriggerField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField)

   클릭 가능한 트리거 단추(기본적으로 콤보 상자처럼 표시됨)를 추가하는 TextFields에 대한 편리한 래퍼를 제공합니다. 트리거에 기본 작업이 없으므로 을 재정의하여 트리거 클릭 핸들러를 구현하는 함수를 할당해야 합니다 [onTriggerClick](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField). 콤보 상자처럼 렌더링되므로 TriggerField를 직접 만들 수 있습니다.

* 업로드 대화 상자

   [CQ.UploadDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.UploadDialog)

   UploadDialog를 사용하면 파일을 저장소에 업로드할 수 있습니다. 새 UploadDialog를 만들 수 있습니다.

* userinfo

   [CQ.UserInfo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.UserInfo)

   현재 사용자 이름을 표시하고 사용자 속성 편집 및 가장과 같은 사용자 작업을 허용하는 도구 모음 항목입니다.

* 뷰포트

   [CQ.Ext.Viewport](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Viewport)

   볼 수 있는 응용 프로그램 영역(브라우저 뷰포트)을 나타내는 전문 컨테이너입니다.

   뷰포트는 문서 본문으로 렌더링되며 브라우저 뷰포트의 크기에 맞게 자동으로 크기를 조정하고 창 크기를 관리합니다. 하나의 뷰포트만 만들 수 있습니다.

* 창

   [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)

   응용 프로그램 창으로 사용하기 위한 전문 패널입니다. 윈도우를 띄우고 [크기 조정 가능](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window), 및 [드래그 가능](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) 기본적으로 제공됩니다. Windows [최대화](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) 뷰포트를 채우려면 이전 크기로 복원한 다음 [최소화](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)d.

* xmlstore

   [CQ.Ext.data.XmlStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.XmlStore)

   만들 작은 도우미 클래스 [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)XML 데이터의 경우보다 쉽게 사용할 수 있습니다. XmlStore는 [CQ.Ext.data.XmlReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.XmlReader).

   **cqinclude** 리포지토리의 다른 경로에서 위젯 정의를 포함하는 의사 xtype입니다. 이 변수는 페이지 대화 상자에서 가장 일반적으로 사용됩니다. 이 xtype에 대한 실제 JavaScript 위젯 클래스가 없습니다. CQ.Util 클래스의 formatData() 함수에 의해 처리됩니다. 자세한 내용은 이 기술 자료 문서를 참조하십시오.
