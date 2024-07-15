---
title: 위젯 사용 및 확장(클래식 UI)
description: Adobe Experience Manager의 웹 기반 인터페이스는 AJAX 및 기타 최신 브라우저 기술을 사용하여 웹 페이지에서 작성자가 컨텐츠를 바로 WYSIWYG로 편집하고 형식을 지정할 수 있도록 합니다
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
docset: aem65
exl-id: 56a9591c-cd78-42e8-a5d7-6b48581d6af6
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '4896'
ht-degree: 0%

---

# 위젯 사용 및 확장(클래식 UI){#using-and-extending-widgets-classic-ui}

>[!NOTE]
>
>이 페이지에서는 AEM 6.4에서 더 이상 사용되지 않는 클래식 UI 내의 위젯 사용에 대해 설명합니다.
>
>Adobe은 [Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui) 및 [Granite UI](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components)를 기반으로 하는 최신 [터치 사용 UI](/help/sites-developing/touch-ui-concepts.md)을(를) 사용할 것을 권장합니다.

Adobe Experience Manager(AEM) 웹 기반 인터페이스는 AJAX 및 기타 최신 브라우저 기술을 사용하여 웹 페이지에서 작성자가 컨텐츠를 바로 WYSIWYG로 편집하고 형식을 지정할 수 있도록 합니다.

AEM은 가장 중요한 모든 브라우저에서 작동하며 데스크톱 수준의 UI 경험을 만들 수 있는 고도로 다듬어진 사용자 인터페이스 요소를 제공하는 [ExtJS](https://www.sencha.com/) 위젯 라이브러리를 사용합니다.

이러한 위젯은 AEM 내에 포함되며, AEM 자체에서 사용할 수 있을 뿐만 아니라 AEM을 사용하여 빌드된 모든 웹 사이트에서 사용할 수 있습니다.

AEM에서 사용 가능한 모든 위젯에 대한 전체 참조는 [위젯 API 설명서](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) 또는 [기존 xtype 목록](/help/sites-developing/xtypes.md)을 참조하십시오. 또한 프레임워크 소유자인 [Sencha](https://examples.sencha.com/extjs/7.6.0/) 사이트에서 ExtJS 프레임워크를 사용하는 방법을 보여 주는 많은 예제를 사용할 수 있습니다.

이 페이지에서는 위젯 사용 및 확장 방법에 대한 통찰력을 제공합니다. 먼저 [페이지에 클라이언트측 코드를 포함](#including-the-client-sided-code-in-a-page)하는 방법을 설명합니다. 그런 다음 몇 가지 기본 사용 및 확장을 설명하기 위해 만들어진 몇 가지 샘플 구성 요소에 대해 설명합니다. 이러한 구성 요소는 **패키지 공유**&#x200B;의 **ExtJS 위젯 사용** 패키지에서 사용할 수 있습니다.

이 패키지에는 다음과 같은 예가 포함됩니다.

* 기본 위젯으로 빌드된 [기본 대화 상자](#basic-dialogs).
* 기본 제공 위젯과 사용자 지정된 JavaScript 논리로 빌드된 [동적 대화 상자](#dynamic-dialogs).
* [사용자 지정 위젯](#custom-widgets)을 기반으로 한 대화 상자.
* 지정된 경로 아래에 JCR 트리를 표시하는 [트리 패널](#tree-overview).
* 데이터를 표 형식으로 표시하는 [표 패널](#grid-overview).

>[!NOTE]
>
>Adobe Experience Manager의 클래식 UI는 [ExtJS 3.4.0](https://extjs.cachefly.net/ext-3.4.0/docs/)을 기반으로 빌드되었습니다.

## 페이지에 클라이언트측 코드 포함 {#including-the-client-sided-code-in-a-page}

클라이언트측 JavaScript 및 스타일 시트 코드는 클라이언트 라이브러리에 배치해야 합니다.

클라이언트 라이브러리를 만들려면 다음을 수행하십시오.

1. 다음 속성을 사용하여 `/apps/<project>` 아래에 노드를 만드십시오.

   * name=&quot;clientlib&quot;
   * jcr:mixinTypes=&quot;[mix:lockable]&quot;
   * jcr:primaryType=&quot;cq:ClientLibraryFolder&quot;
   * sling:resourceType=&quot;widgets/clientlib&quot;
   * categories=&quot;[&lt;category-name>]&quot;
   * 종속성=&quot;[cq.widgets]&quot;

   `Note: <category-name> is the name of the custom library (for example, "cq.extjstraining") and is used to include the library on the page.`

1. `clientlib` 아래에서 `css` 및 `js` 폴더(nt:folder)를 만듭니다.

1. `clientlib` 아래에서 `css.txt` 및 `js.txt` 파일(nt:files)을 만듭니다. 이러한 .txt 파일에는 라이브러리에 포함된 파일이 나열됩니다.

1. `js.txt` 편집: &#39; `#base=js`&#39;(으)로 시작해야 하며 그 뒤에는 CQ 클라이언트 라이브러리 서비스에서 집계한 파일 목록이 와야 합니다. 예:

   ```
   #base=js
    components.js
    exercises.js
    CustomWidget.js
    CustomBrowseField.js
    InsertTextPlugin.js
   ```

1. `css.txt` 편집: &#39; `#base=css`&#39;(으)로 시작해야 하며 그 뒤에는 CQ 클라이언트 라이브러리 서비스에서 집계한 파일 목록이 와야 합니다. 예:

   ```
   #base=css
    components.css
   ```

1. `js` 폴더 아래에 라이브러리에 속하는 JavaScript 파일을 배치합니다.

1. `css` 폴더 아래에 `.css` 파일과 css 파일에서 사용하는 리소스를 배치합니다(예: `my_icon.png`).

>[!NOTE]
>
>이전에 설명한 스타일 시트의 처리는 선택 사항입니다.

페이지 구성 요소 jsp에 클라이언트 라이브러리를 포함하려면 다음을 수행하십시오.

* JavaScript 코드와 스타일 시트를 모두 포함하려면 다음 작업을 수행하십시오.
  `<ui:includeClientLib categories="<category-name1>, <category-name2>, ..."/>`
여기서 `<category-nameX>`은(는) 클라이언트측 라이브러리의 이름입니다.

* JavaScript 코드만 포함하려면 다음 작업을 수행하십시오.
  `<ui:includeClientLib js="<category-name>"/>`

자세한 내용은 태그 설명을 [&lt;ui:includeClientLib>](/help/sites-developing/taglib.md#lt-ui-includeclientlib) 참조하십시오.&lt;/ui:includeClientLib>

경우에 따라 클라이언트 라이브러리는 작성자 모드에서만 사용할 수 있어야 하며 게시 모드에서는 제외해야 합니다. 다음과 같이 달성할 수 있습니다.

```xml
    if (WCMMode.fromRequest(request) != WCMMode.DISABLED) {
        %><ui:includeClientLib categories="cq.collab.blog"/><%
    }
```

### 샘플로 시작 {#getting-started-with-the-samples}

이 페이지의 튜토리얼을 따르려면 로컬 AEM 인스턴스에 패키지 **ExtJS 위젯 사용**&#x200B;을(를) 설치하고 구성 요소가 포함된 샘플 페이지를 만드십시오. 이렇게 하려면 다음을 수행합니다.

1. AEM 인스턴스에서 패키지 공유에서 **ExtJS 위젯(v01) 사용** 패키지를 다운로드하고 패키지를 설치합니다. 저장소에서 `/apps` 아래에 `extjstraining` 프로젝트를 만듭니다.
1. 스크립트(js) 및 스타일 시트(css)가 포함된 클라이언트 라이브러리를 Geometrixx 페이지 jsp의 head 태그에 포함합니다. **Geometrixx** 분기의 새 페이지에 샘플 구성 요소를 포함하려 합니다.
**CRXDE Lite**&#x200B;에서 `/apps/geometrixx/components/page/headlibs.jsp` 파일을 열고 다음과 같이 기존 `<ui:includeClientLib>` 태그에 `cq.extjstraining` 범주를 추가합니다.
   `%><ui:includeClientLib categories="apps.geometrixx-main, cq.extjstraining"/><%`
1. `/content/geometrixx/en/products` 아래의 **Geometrixx** 분기에서 페이지를 만들고 **ExtJS 위젯 사용**&#x200B;이라고 합니다.
1. 디자인 모드로 전환하고 **ExtJS 위젯 사용** 그룹의 모든 구성 요소를 Geometrixx 디자인에 추가하십시오.
1. 편집 모드로 돌아가기: **ExtJS 위젯 사용** 그룹의 구성 요소를 Sidekick에서 사용할 수 있습니다.

>[!NOTE]
>
>이 페이지의 예는 더 이상 AEM과 함께 제공되지 않고 We.Retail로 대체된 Geometrixx 샘플 콘텐츠를 기반으로 합니다. Geometrixx 다운로드 및 설치 방법은 [We.Retail 참조 구현](/help/sites-developing/we-retail.md#we-retail-geometrixx)을 참조하세요.

### 기본 대화 상자 {#basic-dialogs}

대화 상자는 일반적으로 콘텐츠를 편집하는 데 사용되지만 정보를 표시할 수도 있습니다. 전체 대화 상자를 쉽게 볼 수 있는 방법은 json 형식으로 해당 표현에 액세스하는 것입니다. 이렇게 하려면 브라우저가 다음을 수행하도록 지정합니다.

`https://localhost:4502/<path-to-dialog>.-1.json`

Sidekick에서 **ExtJS 위젯 사용** 그룹의 첫 번째 구성 요소를 **1이라고 합니다. 대화 상자 기본 사항**&#x200B;에는 사용자 지정된 JavaScript 논리 없이 기본 위젯으로 빌드된 4개의 기본 대화 상자가 포함되어 있습니다. 대화 상자가 `/apps/extjstraining/components/dialogbasics` 아래에 저장되어 있습니다. 기본 대화 상자는 다음과 같습니다.

* 전체 대화 상자( `full` 노드): 세 개의 탭이 있는 창이 표시되고 각 탭에는 두 개의 텍스트 필드가 있습니다.
* 단일 패널 대화 상자( `singlepanel` 노드): 한 탭에 두 개의 텍스트 필드가 있는 창이 표시됩니다.
* 다중 패널 대화 상자( `multipanel` 노드): 전체 대화 상자와 표시와 동일하지만 다르게 작성되었습니다.
* 디자인 대화 상자( `design` 노드): 두 개의 탭이 있는 창을 표시합니다. 첫 번째 탭에는 텍스트 필드, 드롭다운 메뉴 및 축소 가능한 텍스트 영역이 있습니다. 두 번째 탭에는 4개의 텍스트 필드로 이루어진 필드 세트와 2개의 텍스트 필드로 이루어진 축소 가능한 필드 세트가 있습니다.

**1을(를) 포함합니다. 샘플 페이지의 대화 상자 기본 사항** 구성 요소:

1. **1 추가.** Sidekick **의** ExtJS 위젯 사용&#x200B;**탭에서 샘플 페이지에 대한 대화 상자 기본 사항** 구성 요소입니다.
1. 구성 요소에 제목, 일부 텍스트 및 **PROPERTIES** 링크가 표시됩니다. 링크를 선택하면 저장소에 저장된 단락의 속성이 표시됩니다. 속성을 숨기려면 링크를 다시 선택합니다.

구성 요소는 다음과 같이 표시됩니다.

![chlimage_1-60](assets/chlimage_1-60.png)

#### 예제 1: 전체 대화 상자 {#example-full-dialog}

**전체** 대화 상자에는 세 개의 탭이 있는 창이 표시되며 각 탭에는 두 개의 텍스트 필드가 있습니다. **대화 상자 기본 사항** 구성 요소의 기본 대화 상자입니다. 특징은 다음과 같습니다.

* 노드에 의해 정의됩니다. 노드 유형 = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`.
* 세 개의 탭을 표시합니다(노드 유형 = `cq:Panel`).
* 각 탭에는 두 개의 텍스트 필드가 있습니다(노드 유형 = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`).
* 은 노드에 의해 정의됩니다.
  `/apps/extjstraining/components/dialogbasics/full`
* 은(는) 다음을 요청하여 JSON 형식으로 렌더링됩니다.
  `https://localhost:4502/apps/extjstraining/components/dialogbasics/full.-1.json`

대화 상자가 다음과 같이 표시됩니다.

![screen_shot_2012-01-31at45411pm](assets/screen_shot_2012-01-31at45411pm.png)

#### 예제 2: 단일 패널 대화 상자 {#example-single-panel-dialog}

**단일 패널** 대화 상자에 두 개의 텍스트 필드가 있는 탭 하나가 있는 창이 표시됩니다. 특징은 다음과 같습니다.

* 탭 하나를 표시합니다(노드 유형 = `cq:Dialog`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`).
* 탭에 두 개의 텍스트 필드가 있습니다(노드 유형 = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`).
* 은 노드에 의해 정의됩니다.
  `/apps/extjstraining/components/dialogbasics/singlepanel`
* 은(는) 다음을 요청하여 json 형식으로 렌더링됩니다.
  `https://localhost:4502/apps/extjstraining/components/dialogbasics/singlepanel.-1.json`
* **전체 대화 상자**&#x200B;에 비해 한 가지 이점은 구성이 덜 필요하다는 것입니다.
* 권장 사용: 정보를 표시하거나 일부 필드만 있는 간단한 대화 상자의 경우.

단일 패널 대화 상자를 사용하려면 다음을 수행합니다.

1. **대화 상자 기본 사항** 구성 요소의 대화 상자를 **단일 패널** 대화 상자로 바꿉니다.
   1. **CRXDE Lite**&#x200B;에서 노드를 삭제하십시오. `/apps/extjstraining/components/dialogbasics/dialog`
   1. 변경 내용을 저장하려면 **모두 저장**&#x200B;을 클릭하세요.
   1. 노드 복사: `/apps/extjstraining/components/dialogbasics/singlepanel`
   1. 복사한 노드를 아래에 붙여 넣습니다. `/apps/extjstraining/components/dialogbasics`
   1. `/apps/extjstraining/components/dialogbasics/Copy of singlepanel` 노드를 선택하고 `dialog` 이름을 바꾸십시오.
1. 구성 요소를 편집합니다. 대화 상자는 다음과 같이 표시됩니다.

![screen_shot_2012-01-31at45952pm](assets/screen_shot_2012-01-31at45952pm.png)

#### 예제 3: 다중 패널 대화 상자 {#example-multi-panel-dialog}

**다중 패널** 대화 상자의 디스플레이는 **전체** 대화 상자와 동일하지만 다르게 작성되었습니다. 특징은 다음과 같습니다.

* 노드에 의해 정의됩니다(노드 유형 = `cq:Dialog`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`).
* 세 개의 탭을 표시합니다(노드 유형 = `cq:Panel`).
* 각 탭에는 두 개의 텍스트 필드(노드 유형 = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`)가 있습니다.
* 노드:
  `/apps/extjstraining/components/dialogbasics/multipanel`
* 은(는) 다음을 요청하여 json 형식으로 렌더링됩니다.
  `https://localhost:4502/apps/extjstraining/components/dialogbasics/multipanel.-1.json`
* **전체 대화 상자**&#x200B;에 비해 한 가지 장점은 구조가 단순하다는 것입니다.
* 권장 사용: 다중 탭 대화 상자의 경우.

[다중 패널] 대화 상자를 사용하려면 다음을 수행합니다.

1. **대화 상자 기본 사항** 구성 요소의 대화 상자를 **다중 패널** 대화 상자로 바꿉니다.
[예제 2: 단일 패널 대화 상자](#example-single-panel-dialog)에 설명된 단계를 따릅니다.
1. 구성 요소를 편집합니다. 대화 상자는 다음과 같이 표시됩니다.

![screen_shot_2012-01-31at50119pm](assets/screen_shot_2012-01-31at50119pm.png)

#### 예제 4: 리치 대화 상자 {#example-rich-dialog}

**리치** 대화 상자에 두 개의 탭이 있는 창이 표시됩니다. 첫 번째 탭에는 텍스트 필드, 드롭다운 메뉴 및 축소 가능한 텍스트 영역이 있습니다. 두 번째 탭에는 4개의 텍스트 필드로 이루어진 필드 세트와 2개의 텍스트 필드로 이루어진 축소 가능한 필드 세트가 있습니다. 특징은 다음과 같습니다.

* 노드에 의해 정의됩니다(노드 유형 = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* 두 개의 탭을 표시합니다(노드 유형 = `cq:Panel`).
* 첫 번째 탭에는 ` [textfield](/help/sites-developing/xtypes.md#textfield)`과(와) 세 가지 옵션이 있는 ` [selection](/help/sites-developing/xtypes.md#selection)` 위젯이 포함된 ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` 위젯과 ` [textarea](/help/sites-developing/xtypes.md#textarea)` 위젯이 포함된 축소 가능한 ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)`이(가) 있습니다.
* 두 번째 탭에는 4개의 ` [textfield](/help/sites-developing/xtypes.md#textfield)` 위젯이 포함된 ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` 위젯과 2개의 ` [textfield](/help/sites-developing/xtypes.md#textfield)` 위젯이 포함된 축소 가능한 `dialogfieldset`이(가) 있습니다.
* 은 노드에 의해 정의됩니다.
  `/apps/extjstraining/components/dialogbasics/rich`
* 은(는) 다음을 요청하여 json 형식으로 렌더링됩니다.
  `https://localhost:4502/apps/extjstraining/components/dialogbasics/rich.-1.json`

**리치** 대화 상자를 사용하려면:

1. **대화 상자 기본 사항** 구성 요소의 대화 상자를 **리치** 대화 상자로 바꿉니다.
[예제 2: 단일 패널 대화 상자](#example-single-panel-dialog)에 설명된 단계를 따릅니다.
1. 구성 요소를 편집합니다. 대화 상자는 다음과 같이 표시됩니다.

![screen_shot_2012-01-31at50429pm](assets/screen_shot_2012-01-31at50429pm.png) ![screen_shot_2012-01-31at50519pm](assets/screen_shot_2012-01-31at50519pm.png)

### 동적 대화 상자 {#dynamic-dialogs}

Sidekick에서 **ExtJS 위젯 사용** 그룹의 두 번째 구성 요소를 **2이라고 합니다. 동적 대화 상자** 및 기본 제공 위젯으로 빌드된 3개의 동적 대화 상자와 사용자 지정된 JavaScript 논리로 빌드된 **을(를) 포함합니다**. 대화 상자가 `/apps/extjstraining/components/dynamicdialogs` 아래에 저장되어 있습니다. 동적 대화 상자는 다음과 같습니다.

* 탭 전환 대화 상자(`switchtabs` 노드): 두 개의 탭이 있는 창이 표시됩니다. 첫 번째 탭에는 세 가지 옵션이 있는 라디오 선택 항목이 있습니다. 옵션을 선택하면 해당 옵션과 관련된 탭이 표시됩니다. 두 번째 탭에는 두 개의 텍스트 필드가 있습니다.
* 임의 대화 상자( `arbitrary` 노드): 탭 하나가 있는 창을 표시합니다. 탭에는 에셋을 삭제하거나 업로드할 수 있는 필드와 포함 페이지에 대한 일부 정보 및 에셋을 참조하는 경우 에셋에 대한 정보를 표시하는 필드가 있습니다.
* 필드 전환 대화 상자(`togglefield` 노드): 탭 하나가 있는 창을 표시합니다. 탭에는 확인란이 있습니다. 확인란이 선택되어 있으면 두 개의 텍스트 필드가 있는 필드 세트가 표시됩니다.

**2을(를) 포함합니다. 샘플 페이지의 동적 대화 상자** 구성 요소:

1. **2을(를) 추가합니다.** Sidekick **의** ExtJS 위젯 사용&#x200B;**탭에서 샘플 페이지에 대한 동적 대화 상자** 구성 요소
1. 구성 요소에 제목, 일부 텍스트 및 **PROPERTIES** 링크가 표시됩니다. 링크를 선택하면 저장소에 저장된 단락의 속성이 표시됩니다. 속성을 숨기려면 링크를 다시 선택합니다.

구성 요소는 다음과 같이 표시됩니다.

![chlimage_1-61](assets/chlimage_1-61.png)

#### 예제 1: 탭 전환 대화 상자 {#example-switch-tabs-dialog}

**탭 전환** 대화 상자에 두 개의 탭이 있는 창이 표시됩니다. 첫 번째 탭에는 세 가지 옵션이 있는 라디오 선택 항목이 있습니다. 옵션을 선택하면 해당 옵션과 관련된 탭이 표시됩니다. 두 번째 탭에는 두 개의 텍스트 필드가 있습니다.

주요 특징은 다음과 같습니다.

* 노드에 의해 정의됩니다(노드 유형 = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* 두 개의 탭을 표시합니다(노드 유형 = `cq:Panel`). 한 개의 선택 탭과 두 번째 탭은 첫 번째 탭의 선택 사항에 따라 다릅니다(세 가지 옵션).
* 세 개의 선택적 탭(노드 유형 = `cq:Panel`)이 있고 각 탭에는 두 개의 텍스트 필드(노드 유형 = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`)가 있습니다. 한 번에 하나의 선택 탭만 표시됩니다.
* `switchtabs` 노드에 의해 정의된 위치:
  `/apps/extjstraining/components/dynamicdialogs/switchtabs`
* 은(는) 다음을 요청하여 json 형식으로 렌더링됩니다.
  `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/switchtabs.-1.json`

논리는 다음과 같이 이벤트 리스너와 JavaScript 코드를 통해 구현됩니다.

* 대화 상자 노드에는 대화 상자가 표시되기 전에 선택적 탭을 모두 숨기는 &quot; `beforeshow`&quot; 수신기가 있습니다.
  `beforeshow="function(dialog){Ejst.x2.manageTabs(dialog.items.get(0));}"`
  `dialog.items.get(0)`은(는) 선택 패널과 세 개의 선택 패널이 포함된 `tabpanel`을(를) 가져옵니다.
* `Ejst.x2` 개체가 `exercises.js` 파일의 다음 위치에 정의되어 있습니다.
  `/apps/extjstraining/clientlib/js/exercises.js`
* `Ejst.x2.manageTabs()` 메서드에서 `index`의 값이 -1이므로 모든 선택적 탭이 숨겨집니다(1에서 3까지).
* 선택 탭에는 두 개의 리스너가 있습니다. 하나는 대화 상자가 로드될 때 선택한 탭을 표시하는 것이고(&quot; `loadcontent`&quot; 이벤트), 다른 하나는 선택 내용이 변경될 때 선택한 탭을 표시하는 것입니다(&quot; `selectionchanged`&quot; 이벤트).
  `loadcontent="function(field,rec,path){Ejst.x2.showTab(field);}"`
  `selectionchanged="function(field,value){Ejst.x2.showTab(field);}"`
* `Ejst.x2.showTab()` 메서드의 경우
  `field.findParentByType('tabpanel')`이(가) 모든 탭을 포함하는 `tabpanel`을(를) 가져옵니다(`field`은(는) 선택 위젯을 나타냄).
  `field.getValue()`은(는) 선택 항목의 값(예: tab2)을 가져옵니다.
  `Ejst.x2.manageTabs()`에 선택한 탭이 표시됩니다.
* 각 선택적 탭에는 &quot; `render`&quot; 이벤트에서 탭을 숨기는 수신기가 있습니다.
  `render="function(tab){Ejst.x2.hideTab(tab);}"`
* `Ejst.x2.hideTab()` 메서드의 경우
  `tabPanel``tabpanel` 는 모든 탭을 포함하는 것입니다.
  `index` 는 선택적 탭
  `tabPanel.hideTabStripItem(index)` 탭 숨기기

다음과 같이 표시됩니다.

![screen_shot_2012-02-01at114745am](assets/screen_shot_2012-02-01at114745am.png)

#### 예제 2: 임의의 대화 상자 {#example-arbitrary-dialog}

종종 대화 상자에 기본 구성 요소의 콘텐츠가 표시됩니다. 여기에 설명된 대화 상자(**임의** 대화 상자)는 다른 구성 요소에서 콘텐츠를 가져옵니다.

**임의** 대화 상자에 탭 하나가 있는 창이 표시됩니다. 탭에는 에셋을 삭제하거나 업로드하는 필드와 포함된 페이지에 대한 일부 정보와 에셋을 참조한 경우 에셋에 대한 정보를 표시하는 두 개의 필드가 있습니다.

주요 특징은 다음과 같습니다.

* 노드에 의해 정의됩니다(노드 유형 = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* 패널(노드 유형 = `cq:Panel`)이 하나인 `tabpanel` 위젯(노드 유형 = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`)을 표시합니다.
* 패널에 smartfile 위젯(노드 유형 = `cq:Widget`, xtype = ` [smartfile](/help/sites-developing/xtypes.md#smartfile)`)과 ownerdraw 위젯(노드 유형 = `cq:Widget`, xtype = ` [ownerdraw](/help/sites-developing/xtypes.md#ownerdraw)`)이 있습니다.
* `arbitrary` 노드에 의해 정의된 위치:
  `/apps/extjstraining/components/dynamicdialogs/arbitrary`
* 은(는) 다음을 요청하여 json 형식으로 렌더링됩니다.
  `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/arbitrary.-1.json`

논리는 다음과 같이 이벤트 리스너와 JavaScript 코드를 통해 구현됩니다.

* `ownerdraw` 위젯에는 구성 요소가 포함된 페이지에 대한 정보를 표시하는 &quot; `loadcontent`&quot; 수신기가 있습니다. 즉, 콘텐츠가 로드될 때 smartfile 위젯에서 참조하는 자산입니다.
  `loadcontent="function(field,rec,path){Ejst.x2.showInfo(field,rec,path);}"`
  `field`이(가) `ownerdraw` 개체로 설정되어 있습니다.
  `path`이(가) 구성 요소의 콘텐츠 경로로 설정되어 있습니다(예: `/content/geometrixx/en/products/triangle/ui-tutorial/jcr:content/par/dynamicdialogs`).
* `Ejst.x2` 개체가 `exercises.js` 파일의 다음 위치에 정의되어 있습니다.
  `/apps/extjstraining/clientlib/js/exercises.js`
* `Ejst.x2.showInfo()` 메서드의 경우
  `pagePath`은(는) 구성 요소가 포함된 페이지의 경로입니다.
  `pageInfo`은(는) 페이지 속성을 json 형식으로 나타냅니다.
  `reference`은(는) 참조된 자산의 경로입니다.
  `metadata`은(는) 자산의 메타데이터를 json 형식으로 나타냅니다.
  `ownerdraw.getEl().update(html);` 대화 상자에 생성된 html을 표시합니다.

**임의** 대화 상자를 사용하려면:

1. Dynamic Dialog **구성 요소의 대화 상자를** Arbitrary **대화 상자로**바꾸기:
예제 2: 단일 패널 대화 상자에 설명된 [단계를 팔로우](#example-single-panel-dialog)
1. 구성 요소 편집: 대화 상자는 다음과 같이 표시됩니다.

![screen_shot_2012-02-01at115300am](assets/screen_shot_2012-02-01at115300am.png)

#### 예제 3: 필드 전환 대화 상자 {#example-toggle-fields-dialog}

**필드 전환** 대화 상자에 탭 하나가 있는 창이 표시됩니다. 탭 에는 확인란이 있습니다. 체크하면 두 개의 텍스트 필드로 설정된 필드가 표시됩니다.

주요 특징은 다음과 같습니다.

* 노드(노드 유형 = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`)에 의해 정의됩니다.
* 하나의 `tabpanel` 위젯(노드 유형 = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#textpanel)`)과 하나의 패널(노드 유형 = `cq:Panel`)을 표시합니다.
* 패널에는 선택/확인란 위젯(노드 유형 = `cq:Widget`, xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`, 유형 = ` [checkbox](/help/sites-developing/xtypes.md#checkbox)`)과 기본적으로 숨김 가능한 대화 상자 세트 위젯(노드 유형 = `cq:Widget`, xtype = )과 두 개의 텍스트 필드 위젯(노드 유형 = `cq:Widget`, xtype = ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)`` [textfield](/help/sites-developing/xtypes.md#textfield)`)이 있습니다.
* `togglefields` 노드에 의해 정의된 위치:
  `/apps/extjstraining/components/dynamicdialogs/togglefields`
* 은(는) 다음을 요청하여 json 형식으로 렌더링됩니다.
  `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/togglefields.-1.json`

논리는 다음과 같이 이벤트 리스너와 JavaScript 코드를 통해 구현됩니다.

* 선택 탭에는 두 개의 리스너가 있습니다. 하나는 콘텐츠가 로드될 때 대화 상자 집합을 표시하는 것이고(&quot; `loadcontent`&quot; 이벤트), 다른 하나는 선택 내용이 변경될 때 대화 상자 집합을 표시하는 것입니다(&quot; `selectionchanged`&quot; 이벤트).
  `loadcontent="function(field,rec,path){Ejst.x2.toggleFieldSet(field);}"`
  `selectionchanged="function(field,value){Ejst.x2.toggleFieldSet(field);}"`
* `Ejst.x2` 개체가 `exercises.js` 파일의 다음 위치에 정의되어 있습니다.
  `/apps/extjstraining/clientlib/js/exercises.js`
* `Ejst.x2.toggleFieldSet()` 메서드의 경우
  `box`은(는) 선택 개체입니다.
  `panel`은(는) 선택 항목 및 대화 상자 세트 위젯이 포함된 패널입니다.
  `fieldSet`은(는) 대화 상자 필드 집합 개체입니다.
  `show`은(는) 선택 값(true 또는 false)입니다.
&#39; `show`&#39;을(를) 기반으로 대화 상자 세트가 표시되거나 표시되지 않습니다.

**필드 전환** 대화 상자를 사용하려면 다음을 수행하십시오.

1. **동적 대화 상자** 구성 요소의 대화 상자를 **필드 전환** 대화 상자로 바꿉니다.
[예제 2: 단일 패널 대화 상자](#example-single-panel-dialog)에 설명된 단계를 따릅니다.
1. 구성 요소를 편집합니다. 대화 상자는 다음과 같이 표시됩니다.

![screen_shot_2012-02-01at115518am](assets/screen_shot_2012-02-01at115518am.png)

### 사용자 정의 위젯 {#custom-widgets}

AEM과 함께 제공되는 기본 위젯은 대부분의 사용 사례를 다룹니다. 하지만 프로젝트별 요구 사항을 충족하기 위해 사용자 정의 위젯을 만들어야 하는 경우가 있습니다. 기존 위젯을 확장하여 사용자 정의 위젯을 만들 수 있습니다. 이러한 맞춤화를 시작하기 위해 **`Using ExtJS Widgets`** 패키지에는 세 개의 서로 다른 사용자 지정 위젯을 사용하는 세 개의 대화 상자가 포함되어 있습니다.

* 다중 필드 대화 상자(`multifield` 노드)에는 탭이 하나인 창이 표시됩니다. 탭에는 두 개의 필드가 있는 사용자 지정된 다중 필드 위젯이 있습니다. 두 개의 옵션이 있는 드롭다운 메뉴와 텍스트 필드입니다. 기본 `multifield` 위젯(텍스트 필드만 있음)을 기반으로 하므로 `multifield` 위젯의 모든 기능이 있습니다.
* 트리 찾아보기 대화 상자( `treebrowse` 노드)에는 경로 찾아보기 위젯이 포함된 탭이 있는 창이 표시됩니다. 화살표를 클릭하면 계층을 찾아보고 항목을 선택할 수 있는 창이 열립니다. 그런 다음 항목의 경로가 경로 필드에 추가되고 대화 상자를 닫아도 유지됩니다.
* 사용자 지정 단추를 리치 텍스트 편집기에 추가하여 일부 사용자 지정 텍스트를 기본 텍스트에 삽입하는 리치 텍스트 편집기 플러그인 기반 대화 상자(`rteplugin` 노드)입니다. 이 템플릿은 `richtext` 위젯(RTE)과 RTE 플러그인 메커니즘을 통해 추가된 사용자 지정 기능으로 구성됩니다.

사용자 지정 위젯과 플러그인은 **3이라는 구성 요소에 포함되어 있습니다. Using ExtJS Widgets** 패키지의 **사용자 정의 위젯**. 이 구성 요소를 샘플 페이지에 포함하려면 다음을 수행하십시오.

1. 3을 **추가합니다. 사용자 지정 위젯** 구성 요소를 사이드 킥&#x200B;**의** ExtJS 위젯&#x200B;**사용 탭에서 샘플 페이지**&#x200B;열어야 합니다.
1. 이 구성 요소는 제목, 일부 텍스트 및 PROPERTIES **링크 클릭**시 저장소에 저장된 단락의 속성을 표시합니다. 다시 클릭하면 속성이 숨겨집니다.
구성 요소는 다음과 같이 표시됩니다.

![chlimage_1-62](assets/chlimage_1-62.png)

#### 예제 1: 사용자 정의 다중 필드 위젯 {#example-custom-multifield-widget}

**사용자 지정 다중 필드** 위젯 기반 대화 상자에 탭 하나가 있는 창이 표시됩니다. 탭에는 하나의 필드가 있는 표준 위젯과 달리 두 개의 필드, 즉 두 개의 옵션이 있는 드롭다운 메뉴와 텍스트 필드가 있는 사용자 정의된 다중 필드 위젯이 있습니다.

**사용자 지정 다중 필드** 위젯 기반 대화 상자:

* 노드에 의해 정의됩니다(노드 유형 = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* 패널(노드 유형 = `cq:Widget`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`)이 포함된 `tabpanel` 위젯(노드 유형 = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`)을 표시합니다.
* 패널에 `multifield` 위젯이 있습니다(노드 유형 = `cq:Widget`, xtype = ` [multifield](/help/sites-developing/xtypes.md#multifield)`).
* `multifield` 위젯에 사용자 지정 xtype &#39; `ejstcustom`&#39;을(를) 기반으로 하는 fieldconfig(노드 유형 = `nt:unstructured`, xtype = `ejstcustom`, optionsProvider = `Ejst.x3.provideOptions`)가 있습니다.
   * &#39; `fieldconfig`&#39;은(는) ` [CQ.form.MultiField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.MultiField)` 개체의 구성 옵션입니다.
   * &#39; `optionsProvider`&#39;은(는) `ejstcustom` 위젯의 구성입니다. 다음에서 `exercises.js`에 정의된 `Ejst.x3.provideOptions` 메서드로 설정됩니다.
     `/apps/extjstraining/clientlib/js/exercises.js`
두 개의 옵션을 반환합니다.
* `multifield` 노드에 의해 정의된 위치:
  `/apps/extjstraining/components/customwidgets/multifield`
* 은(는) 다음을 요청하여 json 형식으로 렌더링됩니다.
  `https://localhost:4502/apps/extjstraining/components/customwidgets/multifield.-1.json`

사용자 지정 `multifield` 위젯(xtype = `ejstcustom`):

* 이름이 `Ejst.CustomWidget`인 JavaScript 개체입니다.
* 다음 위치의 `CustomWidget.js` JavaScript 파일에 정의되어 있습니다.
  `/apps/extjstraining/clientlib/js/CustomWidget.js`
* ` [CQ.form.CompositeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.CompositeField)` 위젯을 확장합니다.
* 에는 `hiddenField`(Textfield), `allowField`(ComboBox) 및 `otherField`(Textfield)의 세 필드가 있습니다.
* `CQ.Ext.Component#initComponent`을(를) 재정의하여 세 개의 필드를 추가합니다.
   * `allowField`은(는) &#39;select&#39; 형식의 [CQ.form.Selection](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.Selection) 개체입니다. optionsProvider는 대화 상자에 정의된 CustomWidget의 optionsProvider 구성으로 인스턴스화된 Selection 개체의 구성입니다.
   * `otherField`은(는) [CQ.Ext.form.TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TextField) 개체입니다.
* CQ.form.CompositeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.CompositeField)의 [, `setValue``getValue`, 및 `getRawValue` 메서드를 재정의하여 포맷 CustomWidget의 값을 설정하고 검색합니다.
  `<allowField value>/<otherField value>, for example: 'Bla1/hello'`
* 자신을 &#39;`ejstcustom`&#39; xtype으로 등록:
  `CQ.Ext.reg('ejstcustom', Ejst.CustomWidget);`

**사용자 지정 다중 필드** 위젯 기반 대화 상자가 다음과 같이 표시됩니다.

![screen_shot_2012-02-01at115840am](assets/screen_shot_2012-02-01at115840am.png)

#### 예제 2: 사용자 지정 `Treebrowse` 위젯 {#example-custom-treebrowse-widget}

사용자 지정 **`Treebrowse`** 위젯 기반 대화 상자에는 사용자 지정 경로 찾아보기 위젯이 포함된 하나의 탭 있는 창이 표시됩니다. 화살표를 선택하면 계층 구조를 탐색하고 항목을 선택할 수 있는 창이 열립니다. 그런 다음 항목의 경로가 경로 필드에 추가되고 대화 상자를 닫아도 유지됩니다.

사용자 지정 `treebrowse` 대화 상자는 다음과 같습니다.

* 노드(노드 유형 = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`)에 의해 정의됩니다.
* 패널(노드 유형 = `cq:Widget`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`)이 포함된 `tabpanel` 위젯(노드 유형 = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`)을 표시합니다.
* 패널에 사용자 지정 위젯이 있습니다(노드 유형 = `cq:Widget`, xtype = `ejstbrowse`).
* `treebrowse` 노드에 의해 정의된 위치:
  `/apps/extjstraining/components/customwidgets/treebrowse`
* 은(는) 다음을 요청하여 json 형식으로 렌더링됩니다.
  `https://localhost:4502/apps/extjstraining/components/customwidgets/treebrowse.-1.json`

사용자 지정 트리찾아보기 위젯(xtype = `ejstbrowse`):

* 이름이 `Ejst.CustomWidget`인 JavaScript 개체입니다.
* 다음 위치의 `CustomBrowseField.js` JavaScript 파일에 정의되어 있습니다.
  `/apps/extjstraining/clientlib/js/CustomBrowseField.js`
* ` [CQ.Ext.form.TriggerField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TriggerField)`을(를) 확장합니다.
* `browseWindow`(이)라는 찾아보기 창을 정의합니다.
* 화살표를 클릭할 때 찾아보기 창을 표시하도록 ` [CQ.Ext.form.TriggerField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TriggerField)#onTriggerClick`을(를) 재정의합니다.
* [CQ.Ext.tree.TreePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.tree.TreePanel) 개체를 정의합니다.
   * `/bin/wcm/siteadmin/tree.json`에 등록된 서블릿을 호출하여 데이터를 가져옵니다.
   * 루트는 &quot; `apps/extjstraining`&quot;입니다.
* `window` 개체(` [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Window)`)를 정의합니다.
   * 사전 정의된 패널을 기반으로 합니다.
   * 선택한 경로의 값을 설정하고 패널을 숨기는 **OK** 단추가 있습니다.
* 창이 **경로** 필드 아래에 고정되어 있습니다.
* 선택한 경로가 검색 필드에서 `show` 이벤트의 창으로 전달됩니다.
* 자신을 &#39;`ejstbrowse`&#39; xtype으로 등록:
  `CQ.Ext.reg('ejstbrowse', Ejst.CustomBrowseField);`

**사용자 지정 트리 찾아보기** 위젯 기반 대화 상자를 사용하려면:

1. **사용자 지정 위젯** 구성 요소의 대화 상자를 **사용자 지정 트리 찾아보기** 대화 상자로 바꿉니다.
[예제 2: 단일 패널 대화 상자](#example-single-panel-dialog)에 설명된 단계를 따릅니다.
1. 구성 요소를 편집합니다. 대화 상자는 다음과 같이 표시됩니다.

![screen_shot_2012-02-01at120104pm](assets/screen_shot_2012-02-01at120104pm.png)

#### 예 3: 리치 텍스트 편집기(RTE) 플러그인 {#example-rich-text-editor-rte-plug-in}

**리치 텍스트 편집기(RTE) 플러그인** 기반 대화 상자는 리치 텍스트 편집기 기반 대화 상자로, 대괄호 안에 일부 사용자 지정 텍스트를 삽입하는 사용자 지정 버튼 이 있습니다. 사용자 지정 텍스트는 일부 서버측 논리(이 예제에서는 구현되지 않음)로 구문 분석하여 지정된 경로에 정의된 일부 텍스트를 추가할 수 있습니다.

RTE **플러그인** 기반 대화 상자:

* 는 rteplugin 노드에 의해 다음 위치에서 정의됩니다.
  `/apps/extjstraining/components/customwidgets/rteplugin`
* 은(는) 다음을 요청하여 json 형식으로 렌더링됩니다.
  `https://localhost:4502/apps/extjstraining/components/customwidgets/rteplugin.-1.json`
* `rtePlugins` 노드의 자식 노드 `inserttext`(노드 유형 = `nt:unstructured`)이(가) 플러그 인 다음에 지정되었습니다. 여기에는 RTE에서 사용할 수 있는 플러그 인 기능을 정의하는 `features` 속성이 있습니다.

RTE 플러그인:

* 이름이 `Ejst.InsertTextPlugin`인 JavaScript 개체입니다.
* 다음 위치의 `InsertTextPlugin.js` JavaScript 파일에 정의되어 있습니다.
  `/apps/extjstraining/clientlib/js/InsertTextPlugin.js`
* ` [CQ.form.rte.plugins.Plugin](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)` 개체를 확장합니다.
* 다음 메서드는 ` [CQ.form.rte.plugins.Plugin](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)` 개체를 정의하고 구현 플러그인에서 재정의됩니다.
   * `getFeatures()`은(는) 플러그인이 사용할 수 있도록 하는 모든 기능의 배열을 반환합니다.
   * `initializeUI()`이(가) 새 단추를 RTE 도구 모음에 추가합니다.
   * `notifyPluginConfig()`은(는) 단추를 가리킬 때 제목과 텍스트를 표시합니다.
   * `execute()`은(는) 단추를 클릭하고 플러그 인 작업을 수행할 때 호출됩니다. 포함할 텍스트를 정의하는 데 사용되는 창을 표시합니다.
* `insertText()`이(가) 해당 대화 상자 개체 `Ejst.InsertTextPlugin.Dialog`을(를) 사용하여 텍스트를 삽입합니다(이후 참조).
* **OK** 단추를 클릭하면 트리거되는 대화 상자의 `apply()` 메서드에서 `executeInsertText()`을(를) 호출합니다.
* 자신을 &#39;`inserttext`&#39; 플러그 인으로 등록합니다.
  `CQ.form.rte.plugins.PluginRegistry.register("inserttext", Ejst.InsertTextPlugin);`
* `Ejst.InsertTextPlugin.Dialog` 개체는 플러그 인 단추를 클릭할 때 열리는 대화 상자를 정의합니다. 대화 상자는 패널, 양식, 텍스트 필드 및 두 개의 단추(**확인** 및 **취소**)로 구성됩니다.

**리치 텍스트 편집기(RTE) 플러그 인** 기반 대화 상자를 사용하려면:

1. **사용자 지정 위젯** 구성 요소의 대화 상자를 **리치 텍스트 편집기(RTE) 플러그인** 기반 대화 상자로 바꿉니다.
[예제 2: 단일 패널 대화 상자](#example-single-panel-dialog)에 설명된 단계를 따릅니다.
1. 구성 요소를 편집합니다.
1. 오른쪽(네 개의 화살표가 있는 아이콘)의 마지막 아이콘을 클릭합니다. 경로를 입력하고 **확인**을 클릭하세요.
대괄호([) 안에 경로가 표시됩니다. ]).
1. 서식 있는 텍스트 편집기를 닫으려면 **확인**&#x200B;을 클릭하세요.

리치 **텍스트 편집기(RTE) 플러그인** 기반 대화 상자는 다음과 같이 표시됩니다.

![screen_shot_2012-02-01시간120254오후](assets/screen_shot_2012-02-01at120254pm.png)

>[!NOTE]
>
>이 예제는 로직의 클라이언트측 부분을 구현하는 방법만을 보여줍니다: 그런 다음 자리 표시자(*[텍스트]*)를 서버측에서 명시적으로 구문 분석해야 합니다(예: 컴포넌트 JSP).

### 트리 개요 {#tree-overview}

기본 제공 ` [CQ.Ext.tree.TreePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)` 개체는 트리 구조 데이터의 트리 구조 UI 표현을 제공합니다. ExtJS 위젯&#x200B;**사용 패키지에**&#x200B;포함된 트리 개요 구성 요소는 개체를 사용하여 `TreePanel` 지정된 경로 아래에 JCR 트리를 표시하는 방법을 보여줍니다. 창 자체는 도킹/도킹 해제할 수 있습니다. 이 예에서 창 로직은 태그 사이의 &lt;script> 구성 요소 jsp에 포함됩니다.

샘플 페이지 트리 개요&#x200B;**구성 요소를 포함**&#x200B;하려면 다음을 수행하십시오.

1. 4를 **추가합니다. 트리 개요** 구성 요소를 사이드 킥&#x200B;**의** ExtJS 위젯&#x200B;**사용 탭에서 샘플 페이지**&#x200B;열어야 합니다.
1. 구성 요소가 표시됩니다.
   * 텍스트가 포함된 제목
   * **속성** 링크: 저장소에 저장된 단락의 속성을 표시하려면 클릭합니다. 속성을 숨기려면 다시 클릭합니다.
   * 확장할 수 있는 저장소의 트리 표현이 있는 부동 창입니다.

구성 요소는 다음과 같이 표시됩니다.

![screen_shot_2012-02-01at120639pm](assets/screen_shot_2012-02-01at120639pm.png)

트리 개요 구성 요소:

* 다음에서 정의됩니다.
  `/apps/extjstraining/components/treeoverview`

* 대화 상자에서 창 크기를 설정하고 창을 고정 또는 고정 해제할 수 있습니다(아래 세부 사항 참조).

구성 요소 jsp:

* 저장소에서 너비, 높이 및 도킹된 속성을 검색합니다.
* 트리 개요 데이터 형식에 대한 일부 텍스트를 표시합니다.
* JavaScript 태그 간 구성 요소 jsp에 창 로직을 임베드합니다.
* 다음에서 정의됩니다.
  `apps/extjstraining/components/treeoverview/content.jsp`

구성 요소에 포함된 JavaScript 코드 jsp:

* 페이지에서 트리 창을 검색하여 `tree` 개체를 정의합니다.
* 트리를 표시하는 창이 없으면 `treePanel`([CQ.Ext.tree.TreePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.tree.TreePanel))이 만들어집니다.
   * `treePanel`에 창을 만드는 데 사용되는 데이터가 있습니다.
   * 다음 위치에 등록된 서블릿을 호출하여 데이터를 검색합니다.
     `/bin/wcm/siteadmin/tree.json`
* `beforeload` 수신기에서 선택한 노드가 로드되었는지 확인합니다.
* `root` 개체는 경로 `apps/extjstraining`을(를) 트리 루트로 설정합니다.
* `tree`( ` [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Window)`)은(는) 사전 정의된 `treePanel`을(를) 기반으로 설정되며 다음과 함께 표시됩니다.
  `tree.show();`
* 창이 있으면 저장소에서 검색한 너비, 높이 및 도킹된 속성에 따라 표시됩니다.

구성 요소 대화 상자:

* 트리 개요 창의 크기(너비 및 높이)를 설정하는 두 개의 필드와 창을 고정/고정 해제할 한 개의 필드가 있는 한 개의 탭을 표시합니다
* 노드에 의해 정의됩니다(노드 유형 = `cq:Dialog`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`).
* 패널에 두 가지 옵션(true/false)이 있는 크기 필드 위젯(노드 유형 = `cq:Widget`, xtype = ` [sizefield](/help/sites-developing/xtypes.md#sizefield)`)과 선택 위젯(노드 유형 = `cq:Widget`, xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`, 유형 = `radio`)이 있습니다
* 대화 상자 노드에서 정의됩니다.
  `/apps/extjstraining/components/treeoverview/dialog`
* 은(는) 다음을 요청하여 json 형식으로 렌더링됩니다.
  `https://localhost:4502/apps/extjstraining/components/treeoverview/dialog.-1.json`
* 다음과 같이 표시됩니다.

![screen_shot_2012-02-01at120745pm](assets/screen_shot_2012-02-01at120745pm.png)

### 격자 개요 {#grid-overview}

그리드 패널은 데이터를 행과 열의 테이블 형식으로 나타냅니다. 이는 다음과 같이 구성됩니다.

* 저장소 : 데이터 레코드(행)를 포함하는 모델입니다.
* 열 모델 : 열 구성.
* 보기 : 사용자 인터페이스를 캡슐화합니다.
* 선택 모델 : 선택 비헤이비어

**ExtJS 위젯 사용** 패키지에 포함된 그리드 개요 구성 요소는 데이터를 표 형식으로 표시하는 방법을 보여 줍니다.

* 예제 1은 정적 데이터를 사용합니다.
* 예제 2는 저장소에서 검색한 데이터를 사용합니다.

표 개요 구성 요소를 샘플 페이지에 포함하려면 다음을 수행하십시오.

1. **5을(를) 추가합니다.** Sidekick **의** ExtJS 위젯 사용&#x200B;**탭에서 샘플 페이지에 대한 그리드 개요** 구성 요소
1. 구성 요소가 표시됩니다.
   * 텍스트가 있는 제목
   * **속성** 링크: 저장소에 저장된 단락의 속성을 표시하려면 클릭합니다. 속성을 숨기려면 다시 클릭합니다.
   * 테이블 형식의 데이터가 포함된 부동 창입니다.

구성 요소는 다음과 같이 표시됩니다.

![screen_shot_2012-02-01at121109pm](assets/screen_shot_2012-02-01at121109pm.png)

#### 예제 1: 기본 그리드 {#example-default-grid}

기본 버전 **에서 그리드 개요** 구성 요소는 정적 데이터가 있는 창을 테이블 형식 포맷 형식으로 표시합니다. 이 예에서 로직은 다음 두 가지 방법으로 구성 요소 jsp에 포함됩니다.

* 일반 로직은 태그 사이에 &lt;script> 정의됩니다
* 특정 논리는 별도의 .js 파일에서 사용할 수 있으며 jsp에서 연결됩니다. 이 설정을 사용하면 원하는 &lt;script> 태그에 주석을 달아 두 논리(정적/동적) 간을 전환할 수 있습니다.

그리드 개요 구성 요소:

* 정의 위치:
  `/apps/extjstraining/components/gridoverview`
* 이 대화상자에서는 창의 크기를 설정하고 창을 고정하거나 고정 해제할 수 있습니다.

구성 요소 jsp:

* 저장소에서 너비, 높이 및 고정된 속성을 검색합니다.
* 그리드 개요 데이터 포맷 소개로 일부 텍스트를 표시합니다.
* GridPanel 개체를 정의하는 JavaScript 코드를 참조합니다.
  `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script>`
  `defaultgrid.js`은(는) 일부 정적 데이터를 GridPanel 개체의 기본으로 정의합니다.
* GridPanel 개체를 사용하는 Window 개체를 정의하는 JavaScript 태그 사이에 JavaScript 코드를 포함합니다.
* 다음에서 정의됩니다.
  `apps/extjstraining/components/gridoverview/content.jsp`

구성 요소에 포함된 JavaScript 코드 jsp:

* 페이지에서 창 구성 요소를 검색하여 `grid` 개체를 정의합니다.
  `var grid = CQ.Ext.getCmp("<%= node.getName() %>-grid");`
* `grid`이(가) 없으면 `getGridPanel()` 메서드를 호출하여 [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) 개체(`gridPanel`)를 정의합니다(아래 참조). 이 메서드는 `defaultgrid.js`에 정의되어 있습니다.
* `grid`은(는) 사전 정의된 GridPanel을 기반으로 하는 ` [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Window)` 개체이며 `grid.show();`이(가) 표시됩니다.
* `grid`이(가) 있으면 저장소에서 검색한 너비, 높이 및 도킹된 속성을 기준으로 표시됩니다.

구성 요소 jsp에서 참조된 JavaScript 파일(`defaultgrid.js`)은 JSP에 포함된 스크립트에 의해 호출되는 `getGridPanel()` 메서드를 정의하고 정적 데이터를 기반으로 ` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` 개체를 반환합니다. 논리는 다음과 같습니다.

* `myData`은(는) 다섯 개의 열과 네 개의 행으로 이루어진 테이블 형식의 정적 데이터 배열입니다.
* `store`은(는) `myData`을(를) 사용하는 `CQ.Ext.data.Store` 개체입니다.
* `store`이(가) 메모리에 로드되었습니다.
  `store.load();`
* `gridPanel`은(는) `store`을(를) 사용하는 ` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` 개체입니다.
   * 열 너비는 항상 재비례합니다.
     `forceFit: true`
   * 한 번에 하나의 행만 선택할 수 있습니다.
     `singleSelect:true`

#### 예제 2: 참조 검색 그리드 {#example-reference-search-grid}

패키지를 설치하면 **그리드 개요** 구성 요소의 `content.jsp`에 정적 데이터를 기반으로 하는 그리드가 표시됩니다. 다음과 같은 특성을 가진 격자선을 표시하도록 컴포넌트를 수정할 수 있습니다.

* 3개의 열이 있습니다.
* 서블릿을 호출하여 저장소에서 검색한 데이터를 기반으로 합니다.
* 마지막 열의 셀을 편집할 수 있습니다. 값은 첫 번째 열에 표시된 경로에 의해 정의된 노드 아래의 `test` 속성에서 유지됩니다.

앞 절에서 설명한 대로 Window 개체는 `/apps/extjstraining/components/gridoverview/defaultgrid.js`에 `defaultgrid.js` 파일에 정의된 `getGridPanel()` 메서드를 호출하여 해당 ` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` 개체를 가져옵니다. **그리드 개요**구성 요소는 `/apps/extjstraining/components/gridoverview/referencesearch.js`의 `referencesearch.js` 파일에 정의된 `getGridPanel()` 메서드에 대해 다른 구현을 제공합니다. 구성 요소 jsp에서 참조되는 .js 파일을 전환함으로써 그리드는 저장소에서 검색된 데이터를 기반으로 합니다.

구성 요소 jsp에서 참조되는 .js 파일 전환:

1. 구성 요소의 `content.jsp` 파일에 있는 **CRXDE Lite**&#x200B;에서 `defaultgrid.js` 파일을 포함하는 줄을 다음과 같이 주석 처리합니다.
   `<!-- script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script-->`
1. `referencesearch.js` 파일이 포함된 줄에서 주석을 제거하여 다음과 같이 표시합니다.
   `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/referencesearch.js"></script>`
1. 변경 사항을 저장합니다.
1. 샘플 페이지를 새로 고칩니다.

구성 요소는 다음과 같이 표시됩니다.

![screen_shot_2012-02-01at121429pm](assets/screen_shot_2012-02-01at121429pm.png)

구성 요소 jsp(`referencesearch.js`)에서 참조된 JavaScript 코드는 구성 요소 jsp에서 호출된 `getGridPanel()` 메서드를 정의하고 저장소에서 동적으로 검색된 데이터를 기반으로 ` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` 개체를 반환합니다. `referencesearch.js`의 논리는 일부 동적 데이터를 GridPanel의 기반으로 정의합니다.

* `reader`은(는) 세 개의 열에 대해 json 형식의 서블릿 응답을 읽는 ` [CQ.Ext.data.JsonReader](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.data.JsonReader)` 개체입니다.
* `cm`은(는) 세 개의 열에 대한 ` [CQ.Ext.grid.ColumnModel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.ColumnModel)` 개체입니다.
&quot;Test&quot; 열 셀은 편집기로 정의된 대로 편집할 수 있습니다.
  `editor: new [CQ.Ext.form.TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TextField)({})`
* 열을 정렬할 수 있습니다.
  `cm.defaultSortable = true;`
* `store`은(는) ` [CQ.Ext.data.GroupingStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.data.GroupingStore)` 개체입니다.
   * 쿼리를 필터링하는 데 사용되는 몇 가지 매개 변수와 함께 &quot; `/bin/querybuilder.json`&quot;에 등록된 서블릿을 호출하여 해당 데이터를 가져옵니다.
   * 미리 정의된 `reader`을(를) 기반으로 합니다.
   * 테이블이 오름차순으로 &#39;**jcr:path**&#39; 열에 따라 정렬됩니다.
* `gridPanel`은(는) 편집할 수 있는 ` [CQ.Ext.grid.EditorGridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.EditorGridPanel)` 개체입니다.
   * 미리 정의된 `store` 및 열 모델 `cm`을(를) 기반으로 합니다.
   * 한 번에 하나의 행만 선택할 수 있습니다.
     `sm: new [CQ.Ext.grid.RowSelectionModel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.RowSelectionModel)({singleSelect:true})`
   * `afteredit` 수신자는 &quot;**Test**&quot; 열의 셀이 편집되었는지 확인합니다.
      * &quot;**jcr:path**&quot; 열에 정의된 경로에 있는 노드의 속성 &#39;`test`&#39;이(가) 셀 값으로 저장소에 설정되어 있습니다.
      * POST이 성공하면 값이 `store` 개체에 추가되고 그렇지 않으면 거부됩니다
