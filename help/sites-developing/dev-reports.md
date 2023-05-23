---
title: 보고서 개발
seo-title: Developing Reports
description: AEM에서는 보고 프레임워크를 기반으로 표준 보고서 선택을 제공합니다
seo-description: AEM provides a selection of standard reports based on a reporting framework
uuid: 1b406d15-bd77-4531-84c0-377dbff5cab2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 50fafc64-d462-4386-93af-ce360588d294
exl-id: 3891150e-9972-4bbc-ad61-7f46a1f9bbb4
source-git-commit: 071bc0e36ed2d8eb4ce7bd0ba46823adc0e43095
workflow-type: tm+mt
source-wordcount: '5238'
ht-degree: 0%

---


# 보고서 개발 {#developing-reports}

AEM에서는 다음을 제공합니다. [표준 보고서](/help/sites-administering/reporting.md) 대부분은 보고 프레임워크를 기반으로 합니다.

프레임워크를 사용하여 이러한 표준 보고서를 확장하거나 완전히 새로운 보고서를 개발할 수 있습니다. 보고 프레임워크는 개발자가 CQ5에 대한 기존 지식을 보고서 개발의 발판으로 사용할 수 있도록 기존 CQ5 개념 및 원리와 긴밀하게 통합됩니다.

AEM과 함께 제공되는 표준 보고서의 경우:

* 이러한 보고서는 보고 프레임워크를 기반으로 구축됩니다.

   * [구성 요소 보고서](/help/sites-administering/reporting.md#component-report)
   * [페이지 활동 보고서](/help/sites-administering/reporting.md#page-activity-report)
   * [사용자 보고서](/help/sites-administering/reporting.md#user-report)
   * [워크플로우 상속 보고서](/help/sites-administering/reporting.md#workflow-instance-report)

* 다음 보고서는 개별 원칙을 기반으로 하므로 확장할 수 없습니다.

   * [디스크 사용량](/help/sites-administering/reporting.md#disk-usage)
   * [상태 검사](/help/sites-administering/reporting.md#health-check)
   * [워크플로우 보고서](/help/sites-administering/reporting.md#workflow-report)

>[!NOTE]
>
>튜토리얼 [자체 보고서 만들기 - 예제](#creating-your-own-report-an-example) 또한 아래 원칙 중 몇 가지를 사용할 수 있는지 보여 줍니다.
>
>표준 보고서 를 참조하여 구현의 다른 예를 볼 수도 있습니다.

>[!NOTE]
>
>아래 예와 정의에서는 다음 표기법 이 사용됩니다.
>
>* 각 행은 다음과 같은 노드 또는 속성을 정의합니다.
   >  `N:<name> [<nodeType>]` : 다음 이름의 노드를 설명합니다. `<*name*>` 및 노드 유형 `<*nodeType*>`*.*
   >  `P:<name> [<propertyType]` : 다음 이름의 속성을 설명합니다. `<*name*>` 및 속성 유형 `<*propertyType*>`.
   >  `P:<name> = <value>` : 속성을 설명합니다 `<name>` 을(를) 다음 값으로 설정해야 합니다. `<value>`.
>
>* 들여쓰기는 노드 간의 계층적 종속성을 보여 줍니다.
>* 다음으로 구분된 항목 |은(는) 가능한 항목의 목록을 나타냅니다(예: 유형 또는 이름). `String|String[]` 는 속성이 String 또는 String일 수 있음을 의미합니다.[].
>
>* `[]` 는 배열을 나타냅니다(예: String).[] 또는 와 같은 노드 배열 [쿼리 정의](#query-definition).
>
>달리 명시되지 않는 한 기본 유형은 다음과 같습니다.
>
>* 노드 - `nt:unstructured`
>* 속성 - `String`


## 보고 프레임워크 {#reporting-framework}

보고 프레임워크는 다음 원칙에 따라 작동합니다.

* 이는 전적으로 CQ5 QueryBuilder에서 실행한 쿼리에서 반환되는 결과 세트를 기반으로 합니다.
* 결과 세트는 보고서에 표시되는 데이터를 정의합니다. 결과 세트의 각 행은 보고서의 표 형식 뷰에 있는 행에 해당합니다.
* 결과 세트에서 실행할 수 있는 작업은 RDBMS 개념과 유사합니다. *그룹화* 및 *집계*.

* 대부분의 데이터 검색 및 처리는 서버측에서 수행됩니다.
* 사전 처리된 데이터를 표시할 책임은 전적으로 클라이언트에게 있습니다. 작은 처리 작업(예: 셀 콘텐츠에 링크 만들기)만 클라이언트측에서 실행됩니다.

보고 프레임워크(표준 보고서의 구조로 설명됨)는 처리 큐에서 제공하는 다음 기본 블록을 사용합니다.

![chlimage_1-248](assets/chlimage_1-248.png)

### 보고서 페이지 {#report-page}

보고서 페이지:

* 표준 CQ5 페이지입니다.
* 를 기반으로 함 [보고서에 대해 구성된 표준 CQ5 템플릿](#report-template).

### 보고서 기반 {#report-base}

다음 [ `reportbase` 구성 요소](#report-base-component) 는 다음과 같이 보고서의 기반을 구성합니다.

* 의 정의를 유지합니다. [쿼리](#the-query-and-data-retrieval) 는 기본 데이터 결과 세트를 제공합니다.

* 는 모든 열을 포함하는 조정된 단락 시스템입니다( `columnbase`)이 보고서에 추가되었습니다.
* 사용 가능한 차트 유형과 현재 활성화된 차트 유형을 정의합니다.
* 사용자가 보고서의 특정 측면을 구성할 수 있는 편집 대화 상자를 정의합니다.

### 열 기준 {#column-base}

각 열은 [ `columnbase` 구성 요소](#column-base-component) 그 결과는 다음과 같습니다.

* 는 parsys( )에서 사용하는 단락입니다. `reportbase`)을 클릭하여 제품에서 사용할 수 있습니다.
* 에 대한 링크를 정의합니다. [기본 결과 집합](#the-query-and-data-retrieval): 즉, 이 결과 세트 내에서 참조되는 특정 데이터와 처리 방법을 정의합니다.
* 사용 가능한 합계 및 필터와 같은 추가 정의를 기본값과 함께 저장합니다.

### 쿼리 및 데이터 검색 {#the-query-and-data-retrieval}

쿼리:

* 의 일부로 정의됩니다. [ `reportbase`](#report-base) 구성 요소.
* 을(를) 기반으로 함 [CQ QueryBuilder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html).
* 보고서의 기반으로 사용되는 데이터를 검색합니다. 결과 세트(테이블)의 각 행은 쿼리에서 반환된 대로 노드에 연결됩니다. 특정 정보 [개별 열](#column-base-component) 그런 다음 이 데이터 세트에서 추출됩니다.

* 일반적으로 다음으로 구성됩니다.

   * 루트 경로.

      검색할 저장소의 하위 트리를 지정합니다.

      성능에 미치는 영향을 최소화하려면 쿼리를 저장소의 특정 하위 트리로 제한(시도)하는 것이 좋습니다. 루트 경로는 다음 위치에 사전 정의될 수 있습니다. [보고서 템플릿](#report-template) 또는에서 사용자에 의해 설정됨 [구성(편집) 대화 상자](#configuration-dialog).

   * [하나 이상의 기준](#query-definition).

      이는 (초기) 결과 세트를 생성하기 위해 적용되며, 예를 들어 노드 유형에 대한 제한 또는 속성 제한을 포함합니다.

**여기서 핵심은 쿼리의 결과 집합에서 반환된 각 단일 노드가 보고서에서 단일 행(예: 1:1 관계)을 생성하는 데 사용된다는 것입니다.**

개발자는 보고서에 대해 정의된 쿼리가 해당 보고서에 적합한 노드 세트를 반환하도록 해야 합니다. 그러나 노드 자체가 모든 필수 정보를 보유할 필요는 없으며, 이는 상위 및/또는 하위 노드에서도 파생될 수 있습니다. (예: 다음에 사용되는 쿼리) [사용자 보고서](/help/sites-administering/reporting.md#user-report) 노드 유형을 기반으로 노드를 선택합니다(이 경우 `rep:user`). 그러나 이 보고서의 열 대부분은 이러한 노드에서 직접 데이터를 가져오지 않고 하위 노드에서 데이터를 가져옵니다 `profile`.

### 처리 큐 {#processing-queue}

다음 [쿼리](#the-query-and-data-retrieval) 보고서에서 행으로 표시될 데이터 결과 집합을 반환합니다. 결과 세트의 각 행은 다음 위치에서 처리됩니다(서버측) [여러 단계](#phases-of-the-processing-queue)를 보고서에 표시하기 위해 클라이언트에 전송되기 전에 호출됩니다.

이를 통해 다음과 같은 작업을 수행할 수 있습니다.

* 기본 결과 집합에서 값 추출 및 유도

   예를 들어 두 속성 간의 차이를 계산하여 두 속성 값을 단일 값으로 처리할 수 있습니다.

* 추출된 값 해결. 이 작업은 다양한 방법으로 수행할 수 있습니다.

   예를 들어, 경로는 (각각의 더 사람이 읽을 수 있는 콘텐츠에서처럼) 제목에 매핑될 수 있습니다 *jcr:title* 속성)을 참조하십시오.

* 다양한 지점에서 필터 적용.
* 필요한 경우 조합 값 생성.

   예를 들어, 사용자에게 표시되는 텍스트, 정렬에 사용할 값 및 링크를 만드는 데 사용되는 (클라이언트측에서) 추가 URL로 구성됩니다.

#### 처리 큐 워크플로 {#workflow-of-the-processing-queue}

다음 워크플로우는 처리 대기열을 나타냅니다.

![chlimage_1-249](assets/chlimage_1-249.png)

#### 처리 큐 단계 {#phases-of-the-processing-queue}

자세한 단계 및 요소는 다음과 같습니다.

1. 에서 반환된 결과를 변환합니다. [초기 쿼리(reportbase)](#query-definition) 값 추출기를 사용하여 기본 결과 세트에.

   값 추출기는 다음에 따라 자동으로 선택됩니다. [열 유형](#column-specific-definitions). 기본 JCR 쿼리에서 값을 읽고 결과 세트를 생성하는 데 사용됩니다. 그런 다음 추가 처리가 적용될 수 있습니다. 예: `diff` type을 입력하면 값 추출기가 두 개의 속성을 읽고 결과 세트에 추가되는 단일 값을 계산합니다. 값 추출기를 구성할 수 없습니다.

1. 원시 데이터를 포함하는 초기 결과 집합에 대해 [초기 필터링](#column-specific-definitions) (*raw* 단계)가 적용됩니다.

1. 값은 다음과 같습니다 [전처리됨](#processing-queue); 다음에 대해 정의된 대로 *적용* 단계.

1. [필터링](#column-specific-definitions) (에게 할당됨) *전처리됨* 단계)가 사전 처리된 값에 대해 실행됩니다.

1. 값에 따라 결정됩니다. [정의된 해결자](#processing-queue).
1. [필터링](#column-specific-definitions) (에게 할당됨) *해결됨* 단계)가 해결된 값에 대해 실행됩니다.

1. 데이터: [그룹화 및 집계](#column-specific-definitions).
1. 배열 데이터는 (문자열 기반) 목록으로 변환하여 확인됩니다.

   이는 다중 값 결과를 표시할 수 있는 목록으로 변환하는 암시적 단계입니다. 다중 값 JCR 속성을 기반으로 하는 (집계되지 않은) 셀 값에 필요합니다.

1. 값이 다시 표시됨 [전처리됨](#processing-queue); 다음에 대해 정의된 대로 *afterApplication* 단계.

1. 데이터가 정렬됩니다.
1. 처리된 데이터는 클라이언트로 전송됩니다.

>[!NOTE]
>
>기본 데이터 결과 세트를 반환하는 초기 쿼리는 `reportbase` 구성 요소.
>
>처리 큐의 다른 요소는 `columnbase` 구성 요소.

## 보고서 구성 및 구성 {#report-construction-and-configuration}

보고서를 구성하고 구성하는 데 필요한 사항은 다음과 같습니다.

* a [보고서 구성 요소 정의 위치](#location-of-report-components)
* a [ `reportbase` 구성 요소](#report-base-component)
* 하나 이상, [ `columnbase` 구성 요소](#column-base-component)
* a [페이지 구성 요소](#page-component)
* a [보고서 디자인](#report-design)
* a [보고서 템플릿](#report-template)

### 보고서 구성 요소 위치 {#location-of-report-components}

기본 보고 구성 요소는 아래에 유지됩니다. `/libs/cq/reporting/components`.

그러나 이러한 노드를 업데이트하지 말고 아래에 자체 구성 요소 노드를 만드는 것이 좋습니다 `/apps/cq/reporting/components` 또는 보다 적절한 경우 `/apps/<yourProject>/reports/components`.

여기서(예):

```
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:components [sling:Folder]
```

이 아래에는 보고서의 루트가 만들어지고, 이 아래에는 보고서 기반 구성 요소와 열 기반 구성 요소가 만들어집니다.

```
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:components [sling:Folder]
                N:<reportname> [sling:Folder]
                        N:<reportname> [cq:Component]  // report base component
                        N:<columnname> [cq:Component]  // column base component
```

### 페이지 구성 요소 {#page-component}

보고서 페이지는 `sling:resourceType` / `/libs/cq/reporting/components/reportpage`.

사용자 지정된 페이지 구성 요소는 필요하지 않습니다(대부분의 경우).

## 보고서 기본 구성 요소 {#report-base-component}

각 보고서 유형에는 다음에서 파생된 컨테이너 구성 요소가 필요합니다. `/libs/cq/reporting/components/reportbase`.

이 구성 요소는 보고서 전체의 컨테이너 역할을 하며 다음에 대한 정보를 제공합니다.

* 다음 [쿼리 정의](#query-definition).
* An [(선택 사항) 대화 상자](#configuration-dialog) 보고서를 구성합니다.
* 임의 [차트](#chart-definitions) 보고서에 통합되었습니다.

```
N:<reportname> [cq:Component]
    P:sling:resourceSuperType = "cq/reporting/components/reportbase"
    N:charting
    N:dialog [cq:Dialog]
    N:queryBuilder
```

### 쿼리 정의 {#query-definition}

```xml
N:queryBuilder
    N:propertyConstraints
    [
        N:<name> // array of nodes (name irrelevant), each with the following properties:
            P:name
            P:value
    ]
    P:nodeTypes [String|String[]]
    P:mandatoryProperties [String|String[]
  ]
```

* `propertyConstraints`

   를 사용하여 결과 세트를 특정 값이 있는 특정 속성이 있는 노드로 제한할 수 있습니다. 여러 개의 구속을 지정한 경우 노드는 모든 구속을 만족해야 합니다(AND 작업).

   예:

   ```
   N:propertyConstraints
    [
    N:0
    P:sling:resourceType
    P:foundation/components/textimage
    N:1
    P:jcr:modifiedBy
    P:admin
    ]
   ```

   모두 반환 `textimage` 에서 마지막으로 수정한 구성 요소 `admin` 사용자.

* `nodeTypes`

   결과 집합을 지정된 노드 유형으로 제한하는 데 사용됩니다. 여러 노드 유형을 지정할 수 있습니다.

* `mandatoryProperties`

   다음을 포함하는 노드로 결과 세트를 제한하는 데 사용할 수 있습니다. *모두* 을 참조하십시오. 속성 값은 고려되지 않습니다.

모두 선택 사항이며 필요에 따라 결합할 수 있지만 둘 중 하나 이상을 정의해야 합니다.

### 차트 정의 {#chart-definitions}

```xml
N:charting
    N:settings
        N:active [cq:WidgetCollection]
        [
            N:<name> // array of nodes, each with the following property
                P:id   // must match the id of a child node of definitions
        ]
    N:definitions [cq:WidgetCollection]
    [
        N:<name> // array of nodes, each with the following properties
            P:id
            P:type
            // additional, chart type specific configurations
    ]
```

* `settings`

   활성 차트에 대한 정의를 저장합니다.

   * `active`

      여러 설정을 정의할 수 있으므로 이 옵션을 사용하여 현재 활성화된 설정을 정의할 수 있습니다. 이러한 노드는 노드 배열로 정의됩니다. 이러한 노드에 대해 강제 명명 규칙이 없지만 표준 보고서는 종종 를 사용합니다 `0`, `1`.. `x`), 각 속성은 다음 속성을 갖습니다.

      * `id`

         활성 차트에 대한 식별. 차트 중 하나의 ID와 일치해야 합니다. `definitions`.

* `definitions`

   보고서에 사용할 수 있는 차트 유형을 정의합니다. 다음 `definitions` 사용할 대상을 (으)로 지정합니다. `active` 설정.

   노드 배열을 사용하여 정의를 지정합니다(다시 이라고도 함) `0`, `1`.. `x`), 각 속성은 다음과 같은 속성을 갖습니다.

   * `id`

      차트 식별.

   * `type`

      사용 가능한 차트 유형. 다음 중에서 선택:

      * `pie`
파이 차트 현재 데이터에서만 생성됩니다.

      * `lineseries`
일련의 선(실제 스냅샷을 나타내는 점을 연결함). 내역 데이터에서만 생성됩니다.
   * 차트 유형에 따라 추가 등록 정보를 사용할 수 있습니다.

      * 차트 유형에 대해 `pie`:

         * `maxRadius` ( `Double/Long`)

            파이 차트에 허용되는 최대 반경. 따라서 차트에 허용되는 최대 크기(범례 없음). 다음과 같은 경우 무시됨 `fixedRadius` 이(가) 정의되었습니다.

         * `minRadius` ( `Double/Long`)

            파이 차트에 허용되는 최소 반경입니다. 다음과 같은 경우 무시됨 `fixedRadius` 이(가) 정의되었습니다.

         * `fixedRadius` ( `Double/Long`) 원형 차트의 고정 반경을 정의합니다.
      * 차트 유형에 대해 [`lineseries`](/help/sites-administering/reporting.md#display-limits):

         * `totals` ( `Boolean`)

            True이면 추가 줄에 **합계** 표시되어야 합니다.
기본값: `false`

         * `series` ( `Long`)

            표시할 라인/시리즈의 수입니다.
기본값: `9` (또한 허용되는 최대값입니다.)

         * `hoverLimit` ( `Long`)

            팝업이 표시될 최대 집계된 스냅샷(각 수평선에 표시된 점, 고유한 값을 나타냄) 수(즉, 사용자가 차트 범례의 고유한 값 또는 해당 레이블에서 마우스를 가져가면).

            기본값: `35` (즉, 현재 차트 설정에 35개 이상의 고유 값을 적용할 수 있는 경우 팝업이 전혀 표시되지 않습니다.)

            병렬로 표시할 수 있는 추가 팝업은 10개로 제한됩니다(범례 텍스트를 마우스로 가리키면 여러 팝업을 표시할 수 있음).



### 구성 대화 상자 {#configuration-dialog}

모든 보고서에는 보고서에 대한 다양한 매개 변수를 지정할 수 있는 구성 대화 상자가 있습니다. 이 대화 상자는 **편집** 단추를 클릭합니다.

이 대화 상자는 표준 CQ입니다. [대화 상자](/help/sites-developing/components-basics.md#dialogs) 및 을 구성할 수 있습니다(참조) [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog) 을 참조하십시오.

예제 대화 상자는 다음과 같습니다.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    jcr:primaryType="cq:Dialog"
    height="{Long}424">
    <items jcr:primaryType="cq:WidgetCollection">
        <props jcr:primaryType="cq:Panel">
            <items jcr:primaryType="cq:WidgetCollection">
                <title
                    jcr:primaryType="cq:Widget"
                    path="/libs/cq/reporting/components/commons/title.infinity.json"
                    xtype="cqinclude"/>
                <description
                    jcr:primaryType="cq:Widget"
                    path="/libs/cq/reporting/components/commons/description.infinity.json"
                    xtype="cqinclude"/>
                <rootPath
                    jcr:primaryType="cq:Widget"
                    fieldLabel="Root path"
                    name="./report/rootPath"
                    rootPath=""
                    rootTitle="Repository root"
                    xtype="pathfield"/>
                <processing
                    jcr:primaryType="cq:Widget"
                    path="/libs/cq/reporting/components/commons/processing.infinity.json"
                    xtype="cqinclude"/>
                <scheduling
                    jcr:primaryType="cq:Widget"
                    path="/libs/cq/reporting/components/commons/scheduling.infinity.json"
                    xtype="cqinclude"/>
            </items>
        </props>
    </items>
</jcr:root>
```

사전 구성된 구성 요소 몇 가지가 제공됩니다. 이러한 구성 요소는 다음을 사용하여 대화 상자에서 참조할 수 있습니다. `xtype` 값이 인 속성 `cqinclude`:

* **`title`**

   `/libs/cq/reporting/components/commons/title`

   보고서 제목을 정의하는 텍스트 필드입니다.

* **`description`**

   `/libs/cq/reporting/components/commons/description`

   보고서 설명을 정의하는 텍스트 영역입니다.

* **`processing`**

   `/libs/cq/reporting/components/commons/processing`

   보고서의 처리 모드에 대한 선택기(수동으로/자동으로 데이터 로드).

* **`scheduling`**

   `/libs/cq/reporting/components/commons/scheduling`

   기록 차트의 스냅샷을 예약하기 위한 선택기입니다.

>[!NOTE]
>
>을 사용하여 참조된 구성 요소를 포함해야 합니다. `.infinity.json` 접미사(위의 예 참조)

### 루트 경로 {#root-path}

또한 보고서에 대한 루트 경로를 정의할 수 있습니다.

* **`rootPath`**

   이렇게 하면 보고서가 저장소의 특정 섹션(트리 또는 하위 트리)으로 제한되는데, 이것은 성능 최적화에 권장됩니다. 루트 경로는 `rootPath` 의 속성 `report` 각 보고서 페이지의 노드(페이지 생성 시 템플릿에서 가져옴).

   다음을 통해 지정할 수 있습니다.

   * 다음 [보고서 템플릿](#report-template) ( 구성 대화 상자의 고정 값 또는 기본값으로).
   * 사용자(이 매개 변수 사용)

## 열 기본 구성 요소 {#column-base-component}

각 열 유형에는 다음에서 파생된 구성 요소가 필요합니다. `/libs/cq/reporting/components/columnbase`.

열 구성 요소는 다음 항목의 조합을 정의합니다.

* 다음 [열별 쿼리](#column-specific-query) 구성.
* 다음 [해결자 및 사전 처리](#resolvers-and-preprocessing).
* 다음 [열별 정의](#column-specific-definitions) (필터, 골재 등) `definitions` 하위 노드).
* [열 기본값](#column-default-values).
* 다음 [클라이언트 필터](#client-filter) 서버에서 반환된 데이터에서 표시할 정보를 추출합니다.
* 또한 열 구성 요소는 다음과 같은 적절한 인스턴스를 제공해야 합니다. `cq:editConfig`. 을(를) 정의하려면 [이벤트 및 작업](#events-and-actions) 필수.
* 다음에 대한 구성 [일반 열](#generic-columns).

```
N:<columnname> [cq:Component]
    P:componentGroup
    P:jcr:title
    P:sling:resourceSuperType = "cq/reporting/components/columnbase"
    N:cq:editConfig [cq:EditConfig] // <a href="#events-and-actions">Events and Actions</a>
    N:defaults // <a href="#column-default-values">Column Default Values</a>
    N:definitions
      N:queryBuilder // <a href="#column-specific-query">Column Specific Query</a>
        P:property [String|String[]] // Column Specific Query
        P:subPath // Column Specific Query
        P:secondaryProperty [String|String[]] // Column Specific Query
        P:secondarySubPath // Column Specific Query
      N:data
        P:clientFilter [String] // <a href="#client-filter">Client Filter</a>
        P:resolver // <a href="#resolvers-and-preprocessing">Resolvers and Preprocessing</a>
        N:resolverConfig // Resolvers and Preprocessing
        N:preprocessing // Resolvers and Preprocessing
      P:type // <a href="#column-specific-definitions">Column Specific Definitions</a>
      P:groupable [Boolean] // Column Specific Definitions
      N:filters [cq:WidgetCollection] // Column Specific Definitions
      N:aggregates [cq:WidgetCollection] // Column Specific Definitions
```

참조: [새 보고서 정의](#defining-your-new-report).

### 열별 쿼리 {#column-specific-query}

이에 따라 특정 데이터 추출 정의(에서) [보고서 데이터 결과 집합](#the-query-and-data-retrieval))를 추가합니다.

```xml
N:definitions
    N:queryBuilder
        P:property [String|String[]]
        P:subPath
        P:secondaryProperty [String|String[]]
        P:secondarySubPath
```

* `property`

   실제 셀 값을 계산하는 데 사용할 속성을 정의합니다.

   속성이 문자열로 정의된 경우[] 실제 값을 찾기 위해 여러 속성을 차례로 스캔합니다.

   예를 들어 다음과 같은 경우:

   `property = [ "jcr:lastModified", "jcr:created" ]`

   해당 값 추출기(여기서 제어 중)는 다음을 수행합니다.

   * 사용 가능한 jcr:lastModified 속성이 있는지 확인하고 있는 경우 이 속성을 사용합니다.
   * 사용 가능한 jcr:lastModified 속성이 없으면 jcr:created의 콘텐츠가 대신 사용됩니다.

* `subPath`

   결과가 쿼리에서 반환된 노드에 없으면 `subPath` 는 속성이 실제로 있는 위치를 정의합니다.

* `secondaryProperty`

   실제 셀 값 계산에도 사용해야 하는 두 번째 속성을 정의합니다. 이 속성은 특정 열 유형(diff 및 정렬 가능)에만 사용됩니다.

   예를 들어 워크플로 인스턴스 보고서의 경우, 지정된 속성은 시작 시간과 종료 시간 사이의 시간 차이(밀리초)의 실제 값을 저장하는 데 사용됩니다.

* `secondarySubPath`

   다음과 같은 경우 subPath와 유사 `secondaryProperty` 를 사용합니다.

대부분의 경우 `property` 이 사용됩니다.

### 클라이언트 필터 {#client-filter}

클라이언트 필터는 서버에서 반환된 데이터에서 표시할 정보를 추출합니다.

>[!NOTE]
>
>이 필터는 전체 서버측 처리가 적용된 후 clientside에서 실행됩니다.

```xml
N:definitions
    N:data
        P:clientFilter [String]
```

`clientFilter` 는 다음과 같은 JavaScript 함수로 정의됩니다.

* 입력으로서 는 하나의 매개 변수, 즉 서버에서 반환된 데이터(완전히 전처리됨)를 수신합니다
* 출력 형식으로, 필터링된(처리된) 값, 즉 입력 정보에서 추출되거나 파생된 데이터를 반환합니다.

다음 예에서는 구성 요소 경로에서 해당 페이지 경로를 추출합니다.

```
function(v) {
    var sepPos = v.lastIndexOf('/jcr:content');
    if (sepPos < 0) {
        return v;
    }
    return v.substring(sepPos + '/jcr:content'.length, v.length);
}
```

### 해결자 및 사전 처리 {#resolvers-and-preprocessing}

다음 [처리 큐](#processing-queue) 다양한 해결자를 정의하고 전처리를 구성합니다.

```xml
N:definitions
    N:data
        P:resolver
        N:resolverConfig
        N:preprocessing
            N:apply
            N:applyAfter
```

* `resolver`

   사용할 확인자를 정의합니다. 다음 해결자를 사용할 수 있습니다.

   * `const`

      값을 다른 값에 매핑합니다. 예를 들어, 다음과 같은 상수를 확인하는 데 사용됩니다. `en` 해당 값으로 `English`.

   * `default`

      기본 해결자입니다. 이것은 실제로 아무것도 해결하지 않는 더미 해결자입니다.

   * `page`

      해당 페이지의 경로에 대한 경로 값을 확인합니다. 더 정확히 말하면 해당 페이지에 대한 경로 값 `jcr:content` 노드. 예를 들어, `/content/.../page/jcr:content/par/xyz` 이(가) (으)로 확인됨 `/content/.../page/jcr:content`.

   * `path`

      필요에 따라 하위 경로를 추가하고 노드의 속성에서 실제 값을 가져와 경로 값 확인(에 의해 정의됨) `resolverConfig`)을 클릭하여 제품에서 사용할 수 있습니다. 예: `path` / `/content/.../page/jcr:content` 을(를) 의 콘텐츠로 확인할 수 있습니다. `jcr:title` 즉, 페이지 경로가 페이지 제목으로 확인됩니다.

   * `pathextension`

      경로 앞에 추가하고 확인된 경로에 있는 노드의 속성에서 실제 값을 가져와 값을 확인합니다. (예: 값) `de` 다음과 같은 경로 앞에 붙을 수 있습니다. `/libs/wcm/core/resources/languages`, 속성에서 값 가져오기 `language`를 클릭하여 국가 코드를 확인합니다 `de` 언어 설명으로 `German`.

* `resolverConfig`

   해결 프로그램에 대한 정의를 제공합니다. 사용 가능한 옵션은 `resolver` 선택됨:

   * `const`

      속성을 사용하여 해결할 상수를 지정합니다. 속성의 이름은 확인할 상수를 정의하고, 속성의 값은 확인된 값을 정의합니다.

      예를 들어 가 있는 속성 **이름**= `1` 및 **값** `=One` 1에서 1로 해결됩니다.

   * `default`

      사용 가능한 구성이 없습니다.

   * `page`

      * `propertyName` (옵션)

         값 확인에 사용해야 하는 속성의 이름을 정의합니다. 지정하지 않으면 기본값은 *jcr:title* (페이지 제목)이 사용됩니다. `page` 확인자: 즉, 첫 번째 경로가 페이지 경로로 확인된 다음 페이지 제목으로도 확인됩니다.
   * `path`

      * `propertyName` (옵션)

         값 확인에 사용해야 하는 속성의 이름을 지정합니다. 지정하지 않으면 기본값은 `jcr:title` 를 사용합니다.

      * `subPath` (옵션)

         이 속성을 사용하여 값을 확인하기 전에 경로에 추가할 접미사를 지정할 수 있습니다.
   * `pathextension`

      * `path` (필수)

         앞에 추가할 경로를 정의합니다.

      * `propertyName` (필수)

         실제 값이 있는 해결된 경로의 속성을 정의합니다.

      * `i18n` (선택 사항, 부울 입력)

         해결된 값이 다음이 되어야 하는지 여부를 결정합니다. *다국어화됨* (예: 사용 [CQ5의 국제화 서비스](/help/sites-administering/tc-manage.md)).



* `preprocessing`

   전처리는 선택 사항이며 처리 단계에 (별도로) 바인딩할 수 있습니다 *적용* 또는 *applyAfter*:

   * `apply`

      초기 전처리 단계([처리 큐 표시 단계 3](#processing-queue)).

   * `applyAfter`

      사전 처리 후 적용([처리 큐 표시의 9단계](#processing-queue)).

#### 해결자 {#resolvers}

필요한 정보를 추출하는 데 확인자가 사용됩니다. 다양한 해결자의 예는 다음과 같습니다.

**Const**

다음은 의 상수 값을 해결합니다. `VersionCreated` 문자열로 변환 `New version created`.

자세한 내용은 `/libs/cq/reporting/components/auditreport/typecol/definitions/data`.

```xml
N:data
    P:resolver=const
    N:resolverConfig
        P:VersionCreated="New version created"
```

**페이지**

해당 페이지의 jcr:content (하위) 노드에서 jcr:description 속성에 대한 경로 값을 확인합니다.

자세한 내용은 `/libs/cq/reporting/components/compreport/pagecol/definitions/data`.

```xml
N:data
    P:resolver=page
    N:resolverConfig
        P:propertyName="jcr:description"
```

**경로**

다음은 의 경로를 확인합니다. `/content/.../page` 의 콘텐츠로 `jcr:title` 즉, 페이지 경로가 페이지 제목으로 확인됩니다.

자세한 내용은 `/libs/cq/reporting/components/auditreport/pagecol/definitions/data`.

```xml
N:data
    P:resolver=path
    N:resolverConfig
        P:propertyName="jcr:title"
        P:subPath="/jcr:content"
```

**경로 확장**

다음은 값 앞에 추가됩니다 `de` 경로 확장 사용 `/libs/wcm/core/resources/languages`를 클릭한 다음 속성에서 값을 가져옵니다. `language`를 클릭하여 국가 코드를 확인합니다 `de` 언어 설명으로 `German`.

자세한 내용은 `/libs/cq/reporting/components/userreport/languagecol/definitions/data`.

```xml
N:data
    P:resolver=pathextension
    N:resolverConfig
        P:path="/libs/wcm/core/resources/languages"
        P:propertyName="language"
```

#### 전처리 {#preprocessing}

다음 `preprocessing` 정의는 다음 중 하나에 적용할 수 있습니다.

* 원래 값:

   원래 값에 대한 사전 처리 정의가 다음에서 지정됩니다. `apply` 및/또는 `applyAfter` 직접.

* 집계된 상태의 값:

   필요한 경우, 각각의 응집에 대해 별개의 정의가 제공될 수 있다.

   집계된 값에 대한 명시적 사전 처리를 지정하려면 사전 처리 정의가 각각 상주해야 합니다 `aggregated` 하위 노드( `apply/aggregated`, `applyAfter/aggregated`). 개별 합계에 대한 명시적 사전 처리가 필요한 경우 사전 처리 정의는 각 합계의 이름이 있는 하위 노드에 있습니다(예: `apply/aggregated/min/max` 또는 기타 집계).

전처리 중에 사용할 다음 중 하나를 지정할 수 있습니다.

* [패턴 찾기 및 바꾸기](#preprocessing-find-and-replace-patterns)
찾으면 지정된 패턴(정규 표현식으로 정의됨)이 다른 패턴으로 바뀝니다. 예를 들어, 이 패턴을 사용하여 원본의 하위 문자열을 추출할 수 있습니다.

* [데이터 유형 포맷터](#preprocessing-data-type-formatters)

   숫자 값을 상대 문자열로 변환합니다. 예를 들어 &quot;1시간의 시간 차이를 나타내는 값은 다음과 같은 문자열로 확인됩니다. `1:24PM (1 hour ago)`.

예:

```xml
N:definitions
    N:data
        N:preprocessing
            N:apply|applyAfter
                P:pattern         // regex
                P:replace         // replacement for regex
                // and/or
                P:format          // data type formatter
```

#### 전처리 - 패턴 찾기 및 바꾸기 {#preprocessing-find-and-replace-patterns}

전처리의 경우 다음을 지정할 수 있습니다. `pattern` (로 정의됨) [정규 표현식](https://en.wikipedia.org/wiki/Regular_expression) 또는 정규 표현식)가 포함되며 다음 항목으로 대체됩니다. `replace` 패턴:

* `pattern`

   하위 문자열을 찾는 데 사용되는 정규 표현식입니다.

* `replace`

   원래 문자열의 대체 문자열로 사용될 문자열 또는 문자열 표현입니다. 종종 정규 표현식에 의해 위치한 문자열의 하위 문자열을 나타냅니다. `pattern`.

대체 예는 다음과 같이 분류할 수 있습니다.

* 노드의 경우 `definitions/data/preprocessing/apply` (다음 두 가지 속성 포함)

   * `pattern`: `(.*)(/jcr:content)(/|$)(.*)`
   * `replace`: `$1`

* 문자열은 다음과 같이 도착합니다.

   * `/content/geometrixx/en/services/jcr:content/par/text`

* 다음 네 개의 섹션으로 분류됩니다.

   * `$1` - `(.*)` - `/content/geometrixx/en/services`
   * `$2` - `(/jcr:content)` - `/jcr:content`
   * `$3` - `(/|$)` - `/`
   * `$4` - `(.*)` - `par/text`

* 및 가 로 표시된 문자열로 대체되었습니다. `$1`:

   * `/content/geometrixx/en/services`

#### 사전 처리 - 데이터 유형 포맷터 {#preprocessing-data-type-formatters}

이러한 포맷터는 숫자 값을 상대 문자열로 변환합니다.

예를 들어, 다음을 허용하는 시간 열에 사용할 수 있습니다. `min`, `avg` 및 `max` 집계. 다음으로: `min`/ `avg`/ `max` 합계는 다음으로 표시됨 *시간차* (예: `10 days ago`), 데이터 포맷터가 필요합니다. 이 경우 a `datedelta` 포맷터가 `min`/ `avg`/ `max` 집계된 값. 다음과 같은 경우 `count` 집계도 사용할 수 있으므로 포맷터가 필요하지 않으며 원래 값도 필요하지 않습니다.

현재 사용 가능한 데이터 유형 포맷터는 다음과 같습니다.

* `format`

   데이터 형식 포맷터:

   * `duration`

      기간은 정의된 두 날짜 사이의 시간 범위입니다. 예를 들어, 1시간이 소요된 워크플로 작업의 시작 및 종료는 2/13/11 11:23h에서 시작하여 1시간 후 2/13/11 12:23h에 끝납니다.

      숫자 값(밀리초로 해석됨)을 기간 문자열로 변환합니다. 예: `30000` 은(는) *로 포맷되었습니다. `30s`.*

   * `datedelta`

      Datadelta는 과거 날짜부터 &quot;지금&quot;까지의 시간 범위입니다(따라서 나중에 보고서를 볼 경우 다른 결과가 표시됨).

      숫자 값(일 단위 시간 차이로 해석됨)을 상대적 날짜 문자열로 변환합니다. 예를 들어 1의 형식은 1일 전으로 지정됩니다.

다음 예제는 `datedelta` 서식 `min` 및 `max` 집계:

```xml
N:definitions
    N:data
        N:preprocessing
            N:apply
                N:aggregated
                    N:min
                        P:format = "datedelta"
                    N:max
                        P:format = "datedelta"
```

### 열별 정의 {#column-specific-definitions}

열별 정의는 해당 열에 사용할 수 있는 필터 및 합계를 정의합니다.

```xml
N:definitions
    P:type
    P:groupable [Boolean]
    N:filters [cq:WidgetCollection]
    [
        N:<name> // array of nodes (names irrelevant) with the following properties:
            P:filterType
            P:id
            P:phase
    ]
    N:aggregates [cq:WidgetCollection]
    [
        N:<name> // array of nodes (names irrelevant) with the following properties:
            P:text
            P:type
    ]
```

* `type`

   다음은 표준 옵션으로 사용할 수 있습니다.

   * `string`
   * `number`
   * `int`
   * `date`
   * `diff`
   * `timeslot`

      합계에 필요한 날짜 중 일부를 추출하는 데 사용됩니다(예: 연도별 그룹화하여 각 연도의 데이터를 집계함).

   * `sortable`

      정렬 및 표시에 다른 값(다른 속성에서 가져옴)을 사용하는 값에 사용됩니다.
   또한 위의 모든 값은 다중 값으로 정의할 수 있습니다. 예: `string[]` 는 문자열의 배열을 정의합니다.

   값 추출기는 열 유형에 의해 선택됩니다. 열 유형에 값 추출기를 사용할 수 있는 경우 이 추출기가 사용됩니다. 그렇지 않으면 기본값 추출기가 사용됩니다.

   형식은 매개 변수를 사용할 수 있습니다(선택적). 예를 들어, `timeslot:year` 날짜 필드에서 연도를 추출합니다. 매개 변수가 있는 형식:

   * `timeslot` - 값은 의 해당 상수와 비교할 수 있습니다. `java.utils.Calendar`.

      * `timeslot:year` - `Calendar.YEAR`
      * `timeslot:month-of-year` - `Calendar.MONTH`
      * `timeslot:week-of-year` - `Calendar.WEEK_OF_YEAR`
      * `timeslot:day-of-month` - `Calendar.DAY_OF_MONTH`
      * `timeslot:day-of-week` - `Calendar.DAY_OF_WEEK`
      * `timeslot:day-of-year` - `Calendar.DAY_OF_YEAR`
      * `timeslot:hour-of-day` - `Calendar.HOUR_OF_DAY`
      * `timeslot:minute-of-hour` - `Calendar.MINUTE`


* `groupable`

   보고서를 이 열로 그룹화할 수 있는지 여부를 정의합니다.

* `filters`

   필터 정의.

   * `filterType`

      사용 가능한 필터는 다음과 같습니다.

      * `string`

         문자열 기반 필터입니다.
   * `id`

      필터 식별자.

   * `phase`

      사용 가능한 단계:

      * `raw`

         필터가 원시 데이터에 적용됩니다.

      * `preprocessed`

         필터가 사전 처리된 데이터에 적용됩니다.

      * `resolved`

         해결된 데이터에 필터가 적용됩니다.


* `aggregates`

   합계 정의.

   * `text`

      집계의 텍스트 이름입니다. If `text` 을 지정하지 않으면 집계의 기본 설명이 사용됩니다. 예: `minimum` 이(가) 다음에 사용됩니다. `min` 합계.

   * `type`

      집계 유형. 사용 가능한 합계는 다음과 같습니다.

      * `count`

         행 수를 계산합니다.

      * `count-nonempty`

         비어 있지 않은 행의 수를 계산합니다.

      * `min`

         최소값을 제공합니다.

      * `max`

         최대값을 제공합니다.

      * `average`

         평균 값을 제공합니다.

      * `sum`

         모든 값의 합계를 제공합니다.

      * `median`

         중간값을 제공합니다.

      * `percentile95`

         모든 값의 95번째 백분위수를 가져옵니다.

### 열 기본값 {#column-default-values}

열의 기본값을 정의하는 데 사용됩니다.

```xml
N:defaults
    P:aggregate
```

* `aggregate`

   유효 `aggregate` 값은 와 동일합니다. `type` 아래에 `aggregates` (참조 [열별 정의(정의 - 필터/합계)](#column-specific-definitions) ).

### 이벤트 및 작업 {#events-and-actions}

구성 편집 은 리스너가 감지하는 데 필요한 이벤트와 이러한 이벤트가 발생한 후 적용할 작업을 정의합니다. 다음을 참조하십시오. [구성 요소 개발 소개](/help/sites-developing/components.md) 배경 정보용입니다.

필요한 모든 작업이 충족되도록 하려면 다음 값을 정의해야 합니다.

```xml
N:cq:editConfig [cq:EditConfig]
    P:cq:actions [String[]] = "insert", "delete"
    P:cq:dialogMode = "floating"
    P:cq:layout = "auto"
    N:cq:listeners [cq:EditListenersConfig]
        P:aftercreate = "REFRESH_INSERTED"
        P:afterdelete = "REFRESH_SELF"
        P:afteredit = "REFRESH_SELF"
        P:afterinsert = "REFRESH_INSERTED"
        P:aftermove = "REFRESH_SELF"
        P:afterremove = "REFRESH_SELF"
```

### 일반 열 {#generic-columns}

일반 열은 (대부분의) 열 정의가 구성 요소 노드가 아닌 열 노드의 인스턴스에 저장되는 확장입니다.

개별 일반 컴포넌트에 대해 사용자정의하는 (표준) 대화상자를 사용합니다. 이 대화 상자를 통해 보고서 사용자는 메뉴 옵션을 사용하여 보고서 페이지에서 일반 열의 열 속성을 정의할 수 있습니다 **열 속성...**).

예: **일반** 열 **사용자 보고서**; 참조 `/libs/cq/reporting/components/userreport/genericcol`.

열을 제네릭으로 만들려면 다음을 수행합니다.

* 설정 `type` 열의 속성 `definition` 노드 대상 `generic`.

   자세한 내용은 `/libs/cq/reporting/components/userreport/genericcol/definitions`

* 열의 아래에 (표준) 대화 상자 정의를 지정합니다. `definition` 노드.

   자세한 내용은 `/libs/cq/reporting/components/userreport/genericcol/definitions/dialog`

   * 대화 상자의 필드는 해당 구성 요소 속성(경로 포함)과 동일한 이름을 참조해야 합니다.

      예를 들어, 대화 상자를 통해 일반 열의 유형을 구성할 수 있도록 하려면 `./definitions/type`.

   * UI/대화 상자를 사용하여 정의된 속성이 `columnbase` 구성 요소.

* 구성 편집을 정의합니다.

   자세한 내용은 `/libs/cq/reporting/components/userreport/genericcol/cq:editConfig`

* 표준 AEM 방법론을 사용하여 (추가적인) 열 속성을 정의합니다.

   구성 요소 인스턴스와 열 인스턴스 둘 다에 정의된 속성의 경우 열 인스턴스의 값이 우선합니다.

   일반 열에 사용할 수 있는 등록 정보는 다음과 같습니다.

   * `jcr:title` - 열 이름
   * `definitions/aggregates` - 집계
   * `definitions/filters` - 필터
   * `definitions/type`- 열 유형(선택기/콤보 상자 또는 숨겨진 필드를 사용하여 대화 상자에서 정의해야 함)
   * `definitions/data/resolver` 및 `definitions/data/resolverConfig` (그러나 아님) `definitions/data/preprocessing` 또는 `.../clientFilter`) - 해결 프로그램 및 구성
   * `definitions/queryBuilder` - 쿼리 빌더 구성
   * `defaults/aggregate` - 기본 집계

   에 있는 일반 열의 새 인스턴스인 경우 **사용자 보고서** 대화 상자로 정의된 속성은 아래에서 유지됩니다.

   `/etc/reports/userreport/jcr:content/report/columns/genericcol/settings/generic`

## 보고서 디자인 {#report-design}

디자인은 보고서를 만드는 데 사용할 수 있는 열 유형을 정의합니다. 또한 열이 추가되는 단락 시스템을 정의합니다.

각 보고서에 대해 개별 디자인을 만드는 것이 좋습니다. 이를 통해 완전한 유연성을 확보할 수 있습니다. 참조: [새 보고서 정의](#defining-your-new-report).

기본 보고 구성 요소는 아래에 유지됩니다. `/etc/designs/reports`.

보고서의 위치는 구성 요소가 있는 위치에 따라 달라질 수 있습니다.

* `/etc/designs/reports/<yourReport>` 보고서가 다음에 있는 경우에 적합합니다. `/apps/cq/reporting`

* `/etc/designs/<yourProject>/reports/<*yourReport*>` 를 사용하는 보고서용 `/apps/<yourProject>/reports` 패턴

필수 디자인 속성이에 등록됨 `jcr:content/reportpage/report/columns` (예: `/etc/designs/reports/<reportName>/jcr:content/reportpage/report/columns`):

* `components`

   보고서에서 허용되는 모든 구성 요소 및/또는 구성 요소 그룹.

* `sling:resourceType`

   값이 있는 속성 `cq/reporting/components/repparsys`.

예제 디자인 코드 조각(구성 요소 보고서의 디자인에서 가져옴)은 다음과 같습니다.

```xml
<!-- ... -->
    <jcr:content
        jcr:primaryType="nt:unstructured"
        jcr:title="Component Report"
        sling:resourceType="wcm/core/components/designer">
        <reportpage jcr:primaryType="nt:unstructured">
            <report jcr:primaryType="nt:unstructured">
                <columns
                    jcr:primaryType="nt:unstructured"
                    sling:resourceType="cq/reporting/components/repparsys"
                    components="group:Component Report"/>
            </report>
        </reportpage>
    </jcr:content>
<!-- ... -->
```

개별 열에 대한 디자인을 지정할 필요는 없습니다. 사용 가능한 열은 디자인 모드에서 정의할 수 있습니다.

>[!NOTE]
>
>표준 보고서 디자인은 변경하지 않는 것이 좋습니다. 이는 핫픽스를 업그레이드하거나 설치할 때 변경 사항이 손실되지 않도록 하기 위한 것입니다.
>
>표준 보고서를 사용자 지정하려면 보고서 및 해당 디자인을 복사하십시오.

>[!NOTE]
>
>보고서를 만들 때 기본 열을 자동으로 만들 수 있습니다. 템플릿에서 지정됩니다.

## 보고서 템플릿 {#report-template}

각 보고서 유형은 템플릿을 제공해야 합니다. 표준 버전입니다. [CQ 템플릿](/help/sites-developing/templates.md) 및 를 이와 같이 구성할 수 있습니다.

템플릿은 다음 작업을 수행해야 합니다.

* 설정 `sling:resourceType` 끝 `cq/reporting/components/reportpage`

* 사용할 디자인 표시
* 만들기 `report` 컨테이너를 참조하는 하위 노드( `reportbase`)의 구성 요소 `sling:resourceType` 속성

예제 템플릿 코드 조각(구성 요소 보고서 템플릿에서 가져옴)은 다음과 같습니다.

```xml
<!-- ... -->
    <jcr:content
        cq:designPath="/etc/designs/reports/compreport"
        jcr:primaryType="cq:PageContent"
        sling:resourceType="cq/reporting/components/reportpage">
        <report
            jcr:primaryType="nt:unstructured"
            sling:resourceType="cq/reporting/components/compreport/compreport"/>
    </jcr:content>
<!-- .. -->
```

(사용자 보고서 템플릿에서 가져온) 루트 경로의 정의를 보여 주는 예제 템플릿 스니펫은 다음과 같습니다.

```xml
<!-- ... -->
    <jcr:content
        cq:designPath="/etc/designs/reports/userreport"
        jcr:primaryType="cq:PageContent"
        sling:resourceType="cq/reporting/components/reportpage">
        <report
            jcr:primaryType="nt:unstructured"
            rootPath="/home/users"
            sling:resourceType="cq/reporting/components/compreport/compreport"/>
    </jcr:content>
<!-- .. -->
```

기본 보고 템플릿은 `/libs/cq/reporting/templates`.

그러나 이러한 노드를 업데이트하지 말고 아래에 자체 구성 요소 노드를 만드는 것이 좋습니다 `/apps/cq/reporting/templates` 또는 보다 적절한 경우 `/apps/<yourProject>/reports/templates`.

예(또한 참조) [보고서 구성 요소 위치](#location-of-report-components)):

```xml
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:templates [sling:Folder]
```

이 작업 아래에 템플릿에 대한 루트를 만듭니다.

```xml
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:templates [sling:Folder]
                N:<reportname> [sling:Folder]
```

## 자체 보고서 만들기 - 예제 {#creating-your-own-report-an-example}

### 새 보고서 정의 {#defining-your-new-report}

새 보고서를 정의하려면 다음을 만들고 구성해야 합니다.

1. 보고서 구성 요소의 루트입니다.
1. 보고서 기본 구성 요소입니다.
1. 하나 이상의 열 기본 구성 요소
1. 보고서 디자인입니다.
1. 보고서 템플릿의 루트입니다.
1. 보고서 템플릿입니다.

이러한 단계를 설명하기 위해 다음 예에서는 저장소 내의 모든 OSGi 구성(즉, 의 모든 인스턴스)을 나열하는 보고서를 정의합니다 `sling:OsgiConfig` 노드.

>[!NOTE]
>
>기존 보고서를 복사한 다음 새 버전을 사용자 지정하는 것이 대체 방법입니다.

1. 새 보고서에 대한 루트 노드를 만듭니다.

   예, 다음 `/apps/cq/reporting/components/osgireport`.

   ```xml
   N:cq [nt:folder]
       N:reporting [sling:Folder]
           N:components [sling:Folder]
               N:osgireport [sling:Folder]
   ```

1. 보고서 베이스를 정의합니다. 예 `osgireport[cq:Component]` 아래에 `/apps/cq/reporting/components/osgireport`.

   ```xml
   N:osgireport [sling:Folder]
       N:osgireport [cq:Component]
           P:sling:resourceSuperType [String] = "cq/reporting/components/reportbase"
           N:charting [nt:unstructured]
               N:settings [nt:unstructured]
                   N:active [cq:WidgetCollection]
                       N:0 [nt:unstructured]
                           P:id [String] = "pie"
                       N:1 [nt:unstructured]
                           P:id [String] = "lineseries"
               N:definitions [cq:WidgetCollections]
                   N:0 [nt:unstructured]
                       P:id [String] = "pie"
                       P:maxRadius [Long] = 180
                       P:type [String] = "pie"
                   N:1 [nt:unstructured]
                       P:id [String] = "lineseries"
                       P:type [String] = "lineseries"
           N:dialog [cq:Dialog]
               P:height [Long] = 424
               N:items [cq:WidgetCollection]
                   N:props [cq:Panel]
                       N:items [cq:WidgetCollection]
                           N:title [cq:Widget]
                               P:path [String] = "/libs/cq/reporting/components/commons/title.infinity.json"
                               P:xtype [String] = "cqinclude"
                           N:description [cq:Widget]
                               P:path [String] = "/libs/cq/reporting/components/commons/description.infinity.json"
                               P:xtype [String] = "cqinclude"
                           N:rootPath [cq:Widget]
                               P:fieldLabel [String] = "Root path"
                               P:name [String] = "./report/rootPath"
                               P:xtype [String] = "pathfield"
                           N:processing [cq:Widget]
                               P:path [String] = "/libs/cq/reporting/components/commons/processing.infinity.json"
                               P:xtype [String] = "cqinclude"
                           N:scheduling [cq:Widget]
                               P:path [String] = "/libs/cq/reporting/components/commons/scheduling.infinity.json"
                               P:xtype [String] = "cqinclude"
           N:queryBuilder [nt:unstructured]
               P:nodeTypes [String[]] = "sling:OsgiConfig"
   ```

   다음과 같은 보고서 기반 구성 요소를 정의합니다.

   * 유형의 모든 노드를 검색합니다. `sling:OsgiConfig`
   * 둘 다 표시 `pie` 및 `lineseries` 차트
   * 사용자가 보고서를 구성할 수 있는 대화 상자를 제공합니다

1. 첫 번째 열(columnbase) 구성 요소를 정의합니다. 예 `bundlecol[cq:Component]` 아래에 `/apps/cq/reporting/components/osgireport`.

   ```xml
   N:osgireport [sling:Folder]
       N:bundlecol [cq:Component]
           P:componentGroup [String] = "OSGi Report"
           P:jcr:title = "Bundle"
           P:sling:resourceSuperType [String] = "cq/reporting/components/columnbase"
           N:cq:editConfig [cq:EditConfig]
               P:cq:actions [String[]] = "insert", "delete"
               P:cq:dialogMode [String] = "floating"
               P:cq:layout [String] = "auto"
               N:cq:listeners [cq:EditListenersConfig]
                   P:aftercreate [String] "REFRESH_INSERTED"
                   P:afterdelete [String] "REFRESH_SELF"
                   P:afteredit [String] "REFRESH_SELF"
                   P:afterinsert [String] "REFRESH_INSERTED"
                   P:aftermove [String] "REFRESH_SELF"
                   P:afterremove [String] "REFRESH_SELF"
           N:defaults [nt:unstructured]
               P:aggregate [String] = "count"
           N:definitions [nt:unstructured]
               P:groupable [Boolean] = false
               P:type [String] = "string"
               N:queryBuilder [nt:unstructured]
                   P:property [String] = "jcr:path"
   ```

   이는 다음과 같은 열 기반 구성 요소를 정의합니다.

   * 서버에서 받은 값을 검색하고 반환합니다. 이 경우 속성은 `jcr:path` 마다 `sling:OsgiConfig` 노드
   * 다음을 제공합니다. `count` 합계
   * 그룹화할 수 없음
   * 제목이 있음 `Bundle` (테이블 내 열 제목)
   * 사이드 킥 그룹에 있습니다. `OSGi Report`
   * 지정된 이벤트에서 새로 고침

   >[!NOTE]
   >
   >이 예에는 다음에 대한 정의가 없습니다 `N:data` 및 `P:clientFilter`. 서버에서 받은 값이 기본 동작인 1:1 기준으로 반환되기 때문입니다.
   >
   >이는 정의와 동일합니다.
   >
   >
   ```
   >N:data [nt:unstructured]
   >   P:clientFilter [String] = "function(v) { return v; }"
   >```
   >
   >여기서 함수는 단순히 수신하는 값을 반환합니다.

1. 보고서 디자인을 정의합니다. 예 `osgireport[cq:Page]` 아래에 `/etc/designs/reports`.

   ```xml
   N:osgireport [cq:Page]
       N:jcr:content [nt:unstructured]
           P:jcr:title [String] = "OSGi report"
           P:sling:resourceType [String] = "wcm/core/components/designer"
           N:reportpage [nt:unstructured]
               N:report [nt:unstructured]
                   N:columns [nt:unstructured]
                       P:components [String] = "group:OSGi Report"
                       P:sling:resourceType [String] = "cq/reporting/components/repparsys"
   ```

1. 새 보고서 템플릿에 대한 루트 노드를 만듭니다.

   예, 다음 `/apps/cq/reporting/templates/osgireport`.

   ```xml
   N:cq [nt:folder]
       N:reporting [sling:Folder]
           N:templates [sling:Folder]
               N:osgireport [cq:Template]
   ```

1. 보고서 템플릿을 정의합니다. 예 `osgireport[cq:Template]` 아래에 `/apps/cq/reporting/templates`.

   ```xml
   N:osgireport [cq:Template]
       P:allowedPaths [String[]] = "/etc/reports(/.*)?"
       P:jcr:description [String] = "Use this report generator to create a new OSGi report."
       P:jcr:title [String] = "OSGi Report Template"
       P:ranking [Long] = 100
       P:shortTitle [String] = "OSGi Report"
       N:jcr:content [cq:PageContent]
           P:cq:designPath [String] = "/etc/designs/reports/osgireport"
           P:sling:resourceType [String] = "cq/reporting/components/reportpage"
           N:report [nt:unstructured]
               P:rootPath [String] = "/"
               P:sling:resourceType [String] = "cq/reporting/components/osgireport/osgireport"
       N:thumbnail.png [nt:file]
   ```

   다음과 같은 템플릿을 정의합니다.

   * 다음을 정의합니다. `allowedPaths` 결과 보고서의 경우 - 위의 경우 다음 위치 `/etc/reports`
   * 템플릿에 대한 제목 및 설명을 제공합니다.
   * 템플릿 목록에서 사용할 썸네일 이미지를 제공합니다(이 노드의 전체 정의는 위에 나열되지 않으며, 기존 보고서에서 thumbnail.png 인스턴스를 복사하는 것이 가장 쉽습니다).

### 새 보고서의 인스턴스 만들기 {#creating-an-instance-of-your-new-report}

이제 새 보고서의 인스턴스를 만들 수 있습니다.

1. 를 엽니다. **도구** 콘솔.

1. 선택 **보고서** 왼쪽 창에서 을 클릭합니다.
1. 그러면 **새로 만들기...** 을 클릭합니다. 정의 **제목** 및 **이름**, 새 보고서 유형 선택 (다음 **OSGi 보고서 템플릿**)을 클릭하여 템플릿 목록에서 **만들기**.
1. 새 보고서 인스턴스가 목록에 나타납니다. 열려면 이 아이콘을 두 번 클릭하십시오.
1. 구성 요소 드래그(예: **번들** 다음에서 **OSGi 보고서** group) 을 추가합니다. [보고서 정의 시작](/help/sites-administering/reporting.md#the-basics-of-report-customization).

   >[!NOTE]
   >
   >이 예에는 그룹화할 수 있는 열이 없으므로 차트를 사용할 수 없습니다. 차트를 보려면 을 설정합니다. `groupable` 끝 `true`:
   >
   >
   ```
   >N:osgireport [sling:Folder]
   > N:bundlecol [cq:Component]
   > N:definitions [nt:unstructured]
   > P:groupable [Boolean] = true
   >```

## Report Framework Services 구성 {#configuring-the-report-framework-services}

이 섹션에서는 보고서 프레임워크를 구현하는 OSGi 서비스에 대한 고급 구성 옵션에 대해 설명합니다.

웹 콘솔의 구성 메뉴를 사용하여 볼 수 있습니다(예: `http://localhost:4502/system/console/configMgr`). AEM을 사용하여 작업할 때 이러한 서비스에 대한 구성 설정을 관리하는 방법에는 몇 가지가 있습니다. 다음을 참조하십시오. [OSGi 구성](/help/sites-deploying/configuring-osgi.md) 를 참조하십시오.

### 기본 서비스(일별 CQ 보고 구성) {#basic-service-day-cq-reporting-configuration}

* **시간대** 은 시간대의 내역 데이터가 생성되는 시간을 정의합니다. 이는 기록 차트가 전 세계의 각 사용자에 대해 동일한 데이터를 표시하도록 하기 위한 것입니다.
* **로케일** 와 함께 사용할 로케일을 정의합니다. **시간대** 기록 데이터. 로케일은 로케일별 일정 설정(예: 첫 번째 요일이 일요일인지 또는 월요일인지)을 결정하는 데 사용됩니다.

* **스냅샷 경로** 기록 차트에 대한 스냅샷이 저장되는 루트 경로를 정의합니다.
* **보고서 경로** 보고서가 있는 경로를 정의합니다. 스냅샷 서비스에서 실제로 스냅샷을 생성할 보고서를 결정하는 데 사용됩니다.
* **일별 스냅샷** 일별 스냅숏을 만드는 시간을 정의합니다. 지정한 시간이 서버의 로컬 시간대에 있습니다.
* **시간별 스냅샷** 시간별 스냅샷을 생성할 각 시간의 분을 정의합니다.
* **행 수(최대)** 각 스냅샷에 대해 저장되는 최대 행 수를 정의합니다. 이 값은 합리적으로 선택해야 합니다. 값이 너무 높으면 저장소 크기에 영향을 주고 너무 낮으면 기록 데이터가 처리되는 방식 때문에 데이터가 정확하지 않을 수 있습니다.
* **가짜 데이터**, 활성화된 경우 다음을 사용하여 가짜 내역 데이터를 만들 수 있습니다. `fakedata` 선택기: 비활성화되면 `fakedata` 선택기에서 예외가 발생합니다.

   데이터가 가짜이므로 반드시 *전용* 테스트 및 디버깅 목적으로 사용됩니다.

   사용 `fakedata` 선택기가 보고서를 암묵적으로 완료하므로 기존 데이터가 모두 손실됩니다. 데이터는 수동으로 복원할 수 있지만 시간이 오래 걸릴 수 있습니다.

* **스냅샷 사용자** 는 스냅샷 촬영에 사용할 수 있는 선택적 사용자를 정의합니다.

   기본적으로 보고서를 완료한 사용자에 대해 스냅샷이 작성됩니다. 대신 사용되는 대체 사용자를 지정하려는 상황(예: 게시 시스템에서 해당 사용자가 존재하지 않아 해당 계정이 복제되지 않음)이 있을 수 있습니다.

   또한 사용자를 지정하면 보안 위험이 발생할 수 있습니다.

* **스냅샷 사용자 적용**, 활성화된 경우 아래에 지정된 사용자가 모든 스냅샷을 만듭니다. *스냅샷 사용자*. 이 경우 올바르게 처리되지 않을 경우 심각한 보안 문제가 발생할 수 있습니다.

### 캐시 설정(일별 CQ 보고 캐시) {#cache-settings-day-cq-reporting-cache}

* **사용** 보고서 데이터 캐싱을 활성화하거나 비활성화할 수 있습니다. 보고서 캐시를 활성화하면 여러 요청 중에 보고서 데이터가 메모리에 유지됩니다. 이렇게 하면 성능이 향상되지만 메모리 소비가 증가하여 극단적인 상황에서는 메모리 부족 상황이 발생할 수 있습니다.
* **TL** 보고서 데이터가 캐시되는 시간(초)을 정의합니다. 숫자가 높을수록 성능이 향상되지만 기간 내에 데이터가 변경되면 부정확한 데이터를 반환할 수도 있습니다.
* **최대 항목 수** 는 한 번에 캐시할 최대 보고서 수를 정의합니다.

>[!NOTE]
>
>보고서 데이터는 사용자 및 언어별로 다를 수 있습니다. 따라서 보고서 데이터는 보고서, 사용자 및 언어별로 캐시됩니다. 즉, **최대 항목 수** 값 `2` 실제로 다음 중 하나에 대한 데이터를 캐시합니다.
>
>* 서로 다른 언어 설정을 가진 두 명의 사용자를 위한 하나의 보고서
>* 사용자 1명과 보고서 2명
>

