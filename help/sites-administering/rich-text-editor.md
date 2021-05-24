---
title: Adobe Experience Manager에서 컨텐츠를 작성하도록 리치 텍스트 편집기를 구성합니다.
description: Adobe Experience Manager에서 컨텐츠를 작성하도록 Adobe Experience Manager 리치 텍스트 편집기를 구성하는 방법을 알아봅니다.
contentOwner: AG
source-git-commit: 430994c8e9951500378e0a4d56c8004e7e81c24f
workflow-type: tm+mt
source-wordcount: '3022'
ht-degree: 0%

---


# 리치 텍스트 편집기 구성 {#configure-the-rich-text-editor}

리치 텍스트 편집기(RTE)는 작성자가 텍스트 컨텐츠를 편집하는 다양한 기능을 제공합니다. 아이콘, 선택 상자, 도구 모음 및 메뉴는 WYSIWYG 텍스트 편집 환경을 위해 제공됩니다.

작성을 위해 RTE 기능을 사용하는 방법을 알아보려면 [작성을 위한 리치 텍스트 편집기 사용](/help/sites-authoring/rich-text-editor.md)을 참조하십시오. RTE는 작성 구성 요소에서 사용할 수 있는 기능을 활성화, 비활성화 및 확장하도록 구성할 수 있습니다. 다음 워크플로우는 Experience Manager에서 RTE 구성 작업을 완료하는 권장 순서를 보여줍니다.

![RTE 구성 방법을 학습하는 단계 시퀀스](assets/rte_workflow_v1.png)

*그림:RTE 구성 방법을 학습하는 단계 시퀀스*

## 터치 지원 UI 및 클래식 UI {#understand-touch-enabled-ui-and-classic-ui} 이해

터치 활성화 UI는 Experience Manager을 위한 표준 사용자 인터페이스입니다. Adobe에서 작성 환경을 위해 [응답형 디자인](/help/sites-authoring/responsive-layout.md)이 있는 터치 지원 UI를 도입했습니다. 터치 지원 UI는 터치 및 데스크톱 장치용으로 설계되었습니다. 인터페이스는 원래 클래식 UI와 상당히 다릅니다.

![터치 지원 사용자 인터페이스의 리치 텍스트 편집기 도구 모음](assets/chlimage_1-35.png)

*그림:터치 지원 UI의 리치 텍스트 편집기 도구 모음*

![클래식 UI의 리치 텍스트 편집기 도구 모음](assets/rtedefault.png)

*그림:클래식 UI의 리치 텍스트 편집기 도구 모음*

>[!MORELIKETHIS]
>
>* [UI 권장 사항](/help/sites-deploying/ui-recommendations.md)
* 클래식 UI의 사용 중단에 대해서는 [Experience Manager 6.5 릴리스 노트](/help/release-notes/deprecated-removed-features.md) 를 참조하십시오
* UI의 차이에 대해서는 [Touch UI와 클래식 UI](https://aemcq5pedia.wordpress.com/2018/01/05/touch-enabled-ui-aem6-3/) 를 참조하십시오
* 터치 지원 UI를 자세히 이해하려면 [Experience Manager 터치 UI의 개념](/help/sites-developing/touch-ui-concepts.md) 을 참조하십시오


## 다양한 편집 모드 {#editingmodes}

작성자는 다양한 구성 요소 모드를 사용하여 Experience Manager에서 텍스트 컨텐츠를 만들고 편집할 수 있습니다. 컨텐츠 작성 및 서식 지정을 위한 도구 모음 옵션과 다른 편집 모드에서 RTE 지원 구성 요소의 사용자 경험은 RTE 구성에 따라 달라집니다.

| 편집 모드 | 편집 영역 | 활성화할 권장 기능 | Touch UI | 클래식 UI |
|--- |--- |--- |--- |--- |
| 인라인 | 즉석 편집 기능을 통해 간단한 편집 작업을 수행할 수 있습니다.대화 상자를 열지 않은 형식 지정 | 최소 RTE 기능 | Y | Y |
| RTE 전체 화면 | 전체 페이지를 다룹니다. | 필요한 모든 RTE 기능 | Y | N |
| 대화 상자 | 대화 상자는 페이지 컨텐츠 위에 있지만 전체 페이지를 포함하지 않습니다 | 클래식 UI의 모든 필수 RTE 기능Touch UI에서 기능을 신중하게 사용하도록 설정 | Y | Y |
| 대화 상자 전체 화면 | 전체 화면 모드와 동일합니다.RTE와 함께 대화 상자의 필드를 포함합니다. | 필요한 모든 RTE 기능 | Y | N |

>[!NOTE]
터치 지원 UI의 인라인 편집 모드에서는 소스 편집 기능을 사용할 수 없습니다. 전체 화면 모드에서는 이미지를 드래그할 수 없습니다. 다른 모든 기능은 모든 모드에서 작동합니다.

### 인라인 편집 {#inline-editing}

느린 두 번 클릭/탭으로 열리면 페이지 내에서 컨텐츠를 편집할 수 있습니다. 매우 기본적인 옵션이 포함된 작은 도구 모음이 표시됩니다.

![터치 지원 UI에서 기본 도구 모음을 사용하여 인라인 편집](assets/chlimage_1-36.png)

*그림:터치 지원 UI에서 기본 도구 모음을 사용하여 인라인 편집*

클래식 UI에서 구성 요소를 느리게 두 번 클릭하면 인라인 편집할 수 있고 주황색 윤곽선이 컨텐츠를 강조 표시합니다. 컨텐츠 파인더가 열려 있으면 사용 가능한 RTE 서식 옵션이 있는 도구 모음이 창 맨 위에 표시됩니다. 컨텐츠 파인더가 열려 있지 않으면 서식 옵션이 표시되지 않고 기본 텍스트만 편집할 수 있습니다.

### 전체 화면 편집 {#full-screen-editing}

Experience Manager 구성 요소는 페이지 컨텐츠를 숨기고 사용 가능한 화면을 차지하는 전체 화면 보기에서 열 수 있습니다. 가장 많은 편집 옵션을 제공하므로 인라인 편집의 세부 버전을 전체 화면 편집해 보십시오. 인라인 편집 모드를 사용할 때 작은 도구 모음에서 ![rte_fullscreen](assets/rte_fullscreen.png)을 클릭하여 열 수 있습니다.

대화 상자 전체 화면 모드에서 세부 RTE 도구 모음과 함께 대화 상자에서 사용할 수 있는 옵션 및 구성 요소도 사용할 수 있습니다. 이 변수는 다른 구성 요소와 함께 RTE가 포함된 대화 상자에만 적용할 수 있습니다.

![터치 지원 UI에서 전체 화면 모드로 편집할 때 세부 RTE 도구 모음](assets/chlimage_1-37.png)

*그림:터치 지원 UI에서 전체 화면 모드로 편집할 때 세부 RTE 도구 모음*

### 대화 상자 편집 {#dialog-editing}

구성 요소를 두 번 클릭하면 컨텐츠를 편집할 수 있는 대화 상자가 열립니다. 대화 상자가 기존 페이지 맨 위에 열립니다. 일부 특정 시나리오에서는 대화 상자가 팝업 창으로 열립니다. 예를 들어 텍스트 구성 요소가 다중 열 페이지 레이아웃의 열에 속하고 대화 상자에 사용할 수 있는 영역은 더 작아집니다.

![터치 지원 UI의 대화 상자 편집 모드](assets/dialog_editing_modetouchui.png)

*그림:터치 지원 UI의 대화 상자 편집 모드*

![편집을 위한 세부 도구 모음이 포함된 클래식 UI의 대화 상자](assets/chlimage_1-38.png)

*그림:편집을 위한 세부 도구 모음이 포함된 클래식 UI의 대화 상자*

## RTE 플러그인 및 관련 기능 정보 {#aboutplugins}

기능은 각 플러그인을 통해 사용할 수 있으며, 각 플러그인은 다음과 같습니다.

* `features` 속성:

   * 해당 플러그인의 기본 기능을 활성화하거나 비활성화하는 데 사용됩니다.
   * 표준화된 절차를 사용하여 구성할 수 있습니다

* 적절한 경우 별도의 구성을 필요로 하는 추가 속성 및 옵션

해당 플러그인과 관련된 노드의 `features` 속성 값으로 RTE의 기본 기능이 활성화되거나 비활성화됩니다.

다음 표에는 현재 플러그인이 표시되어 있습니다.

* API 설명서에 대한 링크가 있는 플러그인 ID입니다. [플러그인을 활성화](/help/sites-administering/configure-rich-text-editor-plug-ins.md#activateplugin)할 때 ID가 노드 이름으로 사용됩니다.
* `features` 속성에 대해 허용되는 값입니다.
* 플러그인에서 제공하는 기능에 대한 설명입니다.

| 플러그인 ID | 기능 | 설명 |
|--- |--- |--- |
| 편집 | 잘라내기 복사 붙여넣기-기본 붙여넣기-plaintext 붙여넣기-wordhtml | [잘라내기, 복사 및 세 가지 붙여넣기 모드](/help/sites-administering/configure-rich-text-editor-plug-ins.md#textstyles). |
| [칠드레플레이스](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.FindReplacePlugin) | 찾기 바꾸기 | 찾기 및 바꾸기 |
| [포맷](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.FormatPlugin) | 굵게 기울임꼴 밑줄 | [기본 텍스트 서식](/help/sites-administering/configure-rich-text-editor-plug-ins.md#textstyles). |
| [이미지](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.ImagePlugin) | 이미지 | 기본 이미지 지원(컨텐츠 또는 컨텐츠 파인더에서 드래그). 브라우저에 따라 작성자를 위한 다양한 동작이 지원됩니다 |
| [키](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.KeyPlugin) |  | 이 값을 정의하려면 [탭 크기](/help/sites-administering/configure-rich-text-editor-plug-ins.md#tabsize)를 참조하십시오. |
| [정당화](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.JustifyPlugin) | justfyleft justfycenter justfyright | 단락 맞춤. |
| [링크](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.LinkPlugin) | modifylink 연결 해제 앵커 | [하이퍼링크 및 앵커](/help/sites-administering/configure-rich-text-editor-plug-ins.md#linkstyles). |
| [목록](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.ListPlugin) | 순서가 없는 무순서 들여쓰기 내어쓰기 | 이 플러그인은 [들여쓰기 및 목록](/help/sites-administering/configure-rich-text-editor-plug-ins.md#indentmargin) 모두 제어합니다.중첩된 목록을 포함합니다. |
| [misctools](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.MiscToolsPlugin) | specialchars sourceedit | 기타 도구를 사용하여 작성자는 [특수 문자](/help/sites-administering/configure-rich-text-editor-plug-ins.md#spchar)를 입력하거나 HTML 소스를 편집할 수 있습니다. 또한 목록을 정의하려는 경우 전체 [특수 문자](/help/sites-administering/configure-rich-text-editor-plug-ins.md#definerangechar) 범위를 추가할 수 있습니다. |
| Paraformat | paraformat | 기본 단락 형식은 단락, 머리글 1, 제목 2 및 제목 3(`<p>`, `<h1>`, `<h2>` 및 `<h3>`)입니다. [단락 형식](/help/sites-administering/configure-rich-text-editor-plug-ins.md#paraformats)을 더 추가하거나 목록을 확장할 수 있습니다. |
| 맞춤법 검사 | 체크 텍스트 | [언어 인식 맞춤법 검사기입니다](/help/sites-administering/configure-rich-text-editor-plug-ins.md#adddict). |
| 스타일 | 스타일 | CSS 클래스를 사용하는 스타일링을 지원합니다. [텍스트에 사용할 ](/help/sites-administering/configure-rich-text-editor-plug-ins.md#textstyles) 고유한 스타일 범위를 추가(또는 확장)하려면 새 텍스트 스타일을 추가합니다. |
| 아래 첨자 | 아래 첨자 | 기본 형식에 대한 확장, 하위 및 슈퍼 스크립트 추가. |
| 표 | 표 제거 대상 삽입방법 제거항목 제거항목 삽입열 제거열 제거x열 셀prop셀 분할셀 선택열 | 전체 테이블이나 개별 셀에 대한 고유한 스타일을 추가하려면 [표 스타일 구성](/help/sites-administering/configure-rich-text-editor-plug-ins.md#tablestyles) 을 참조하십시오. |
| 실행 취소 | 다시 실행 취소 | [실행 취소 및 다시 실행](/help/sites-administering/configure-rich-text-editor-plug-ins.md#undohistory) 작업의 기록 크기입니다. |

>[!NOTE]
전체 화면 플러그인은 대화 상자 모드에서 지원되지 않습니다. 전체 화면 모드에 대한 도구 모음을 구성하려면 `dialogFullScreen` 설정을 사용합니다.

## 구성 경로 및 위치 {#understand-the-configuration-paths-and-locations} 이해

작성자를 위해 제공하는 RTE 편집의 [모드](#editingmodes)에서 RTE 플러그인](/help/sites-administering/configure-rich-text-editor-plug-ins.md#activateplugin)을(를) 활성화 중일 때 구성 세부 사항의 위치를 결정합니다.[

| 편집 모드 | Touch UI용 위치 | 클래식 UI용 위치 |
|---|---|---|
| 인라인 | `cq:editConfig/cq:inplaceEditing` | `cq:editConfig/cq:inplaceEditing` |
| 전체 화면 | `cq:editConfig/cq:inplaceEditing` | 해당 사항 없음 |
| 대화 상자 | `cq:dialog` | `dialog` |
| 전체 화면 대화 상자 | `cq:dialog` | 해당 사항 없음 |

>[!NOTE]
`cq:inplaceEditing` 아래에 있는 노드의 이름을 `config`(으)로 지정하지 마십시오. `cq:inplaceEditing` 노드에서 다음 속성을 정의합니다.
* **이름**: `configPath`
* **유형**: `String`
* **값**:실제 구성이 들어 있는 노드의 경로

RTE 구성 노드의 이름을 `config`로 지정하지 마십시오. 그렇지 않으면 `content-author` 그룹의 사용자가 아닌 관리자에게만 RTE 구성이 적용됩니다.

Touch UI의 대화 상자 편집 모드에서만 적용되는 다음 속성을 구성합니다.

* `useFixedInlineToolbar`:RTE 노드에 정의된 이 부울 속성(sling:resourceType=  `cq/gui/components/authoring/dialog/richtext`가 있는 속성)을  `True`로 설정하여 부동 대신 RTE 도구 모음을 고정시킵니다.

   이 속성이 true면 Richtext 편집은 기본적으로 &quot;foundation-contentloaded&quot; 이벤트에서 시작됩니다.

   이를 방지하려면 `customStart` 속성을 `True`로 설정하고 &#39;rte-start&#39; 이벤트를 트리거하여 RTE 편집을 시작합니다. 이 속성이 &#39;true&#39;이면 기본 동작인 클릭 시 rte 시작이 작동하지 않습니다.

* `customStart`:이벤트를 트리거하여 RTE를 시작할 시기를  `True`제어하려면 RTE 노드에 정의된 이 부울 속성을 로 설정합니다  `rte-start`.

* `rte-start`:RTE 편집을 시작할  `contenteditable-div` 때 RTE에서 이 이벤트를 트리거합니다. 이 기능은 `customStart`이 true로 설정된 경우에만 작동합니다.

터치 사용 대화 상자에서 RTE를 사용하는 경우, 문제를 방지하기 위해 속성 `useFixedInlineToolbar`을 true로 설정해야 합니다.

## {#customizing-in-place-editing} 편집 시 사용자 지정

다음 속성을 구성하여 텍스트 편집기가 시작되는 HTML 선택기를 정의할 수 있습니다.

* **`editElementQuery`** - 에 정의되 `cq:InplaceEditingConfig`는 이 속성은 텍스트 구성 요소에 대한 인라인 편집을 시작할 HTML 요소의 선택기를 지정하는 데 사용됩니다. 지정하지 않으면 텍스트 구성 요소 HTML에서 인라인 편집이 직접 시작됩니다.
* **`textPropertyName`** - 에 정의되 `cq:InplaceEditingConfig`는 이 속성은 텍스트 구성 요소의 HTML 값이 인라인 편집 후 지속될 컨텐츠 노드에 저장할 속성의 이름을 지정하는 데 사용됩니다.

대화 상자 모드에 대한 해당 속성은 `name`입니다.

## 플러그인 {#enable-rte-functionalities-by-activating-plug-ins}을 활성화하여 RTE 기능 활성화

RTE 기능은 각각 기능 속성이 있는 일련의 플러그인을 통해 사용할 수 있습니다. 각 플러그인의 다양한 기능을 활성화하거나 비활성화하도록 기능 속성을 구성할 수 있습니다.

RTE 플러그인의 자세한 구성은 [RTE 플러그인을 활성화하고 구성하는 방법](/help/sites-administering/configure-rich-text-editor-plug-ins.md)을 참조하십시오.

**샘플**:RTE 구성  [방법을 ](/help/sites-administering/assets/rte-sample-all-features-enabled-10.zip) 보여주는 이 샘플 구성을 다운로드하십시오. 이 패키지에는 모든 기능이 활성화됩니다.

>[!NOTE]
템플릿 편집자는 [코어 구성 요소 텍스트 구성 요소](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor)를 사용하여 GUI에서 많은 RTE 플러그인을 컨텐츠 정책으로서 구성할 수 있으므로 기술 구성이 필요 없습니다. 컨텐츠 정책은 이 문서에 설명된 대로 RTE UI 구성에서 사용할 수 있습니다.
자세한 내용은 이 문서의 [RTE UI 설정 및 컨텐츠 정책](/help/sites-administering/rich-text-editor.md) 섹션과 페이지 템플릿 만들기](/help/sites-authoring/templates.md) 및 [핵심 구성 요소 개발자 설명서](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/developing.html)를 참조하십시오.[

>[!NOTE]
참조용으로 기본 텍스트 구성 요소(표준 설치의 일부로 제공됨)는 다음 위치에서 찾을 수 있습니다.
* `/libs/wcm/foundation/components/text`
* `/libs/foundation/components/text`

자체 텍스트 구성 요소를 만들려면 이러한 구성 요소를 편집하는 대신 위의 구성 요소를 복사하십시오.

## RTE 도구 모음 구성 {#dialogfullscreen}

AEM에서는 다양한 편집 모드에 대해 리치 텍스트 편집기의 인터페이스를 다르게 구성할 수 있습니다. 기본 설정은 아래에 제공됩니다. 요구 사항에 따라 이러한 기본값을 대체할 수 있습니다. 작성자에게 제공할 도구 모음 기능만 사용자 지정합니다. 도구 모음 구성을 모두 지정할 필요는 없습니다.

`dialogFullScreen`에 대한 도구 모음을 구성하려면 다음 샘플 구성을 사용합니다.

```java
<uiSettings jcr:primaryType="nt:unstructured">
  <cui jcr:primaryType="nt:unstructured">
    <inline
      jcr:primaryType="nt:unstructured"
      toolbar="[format#bold,format#italic,format#underline,#justify,#lists,links#modifylink,links#unlink,#paraformat]">
      <popovers jcr:primaryType="nt:unstructured">
        <justify
          jcr:primaryType="nt:unstructured"
          items="[justify#justifyleft,justify#justifycenter,justify#justifyright,justify#justifyjustify]"
          ref="justify"/>
        <lists
          jcr:primaryType="nt:unstructured"
          items="[lists#unordered,lists#ordered,lists#outdent,lists#indent]"
          ref="lists"/>
        <paraformat
          jcr:primaryType="nt:unstructured"
          items="paraformat:getFormats:paraformat-pulldown"
          ref="paraformat"/>
      </popovers>
    </inline>
    <dialogFullScreen
      jcr:primaryType="nt:unstructured"
      toolbar="[format#bold,format#italic,format#underline,justify#justifyleft,justify#justifycenter,justify#justifyright,justify#justifyjustify,lists#unordered,lists#ordered,lists#outdent,lists#indent,links#modifylink,links#unlink,table#createoredit,#paraformat,image#imageProps]">
      <popovers jcr:primaryType="nt:unstructured">
        <paraformat
          jcr:primaryType="nt:unstructured"
          items="paraformat:getFormats:paraformat-pulldown"
          ref="paraformat"/>
      </popovers>
    </dialogFullScreen>
    <tableEditOptions
      jcr:primaryType="nt:unstructured"
      toolbar="[table#insertcolumn-before,table#insertcolumn-after,table#removecolumn,-,table#insertrow-before,table#insertrow-after,table#removerow,-,table#mergecells-right,table#mergecells-down,table#mergecells,table#splitcell-horizontal,table#splitcell-vertical,-,table#selectrow,table#selectcolumn,-,table#ensureparagraph,-,table#modifytableandcell,table#removetable,-,undo#undo,undo#redo,-,table#exitTableEditing,-]">
    </tableEditOptions>
  </cui>
</uiSettings>
```

인라인 모드 및 전체 화면 모드에 다른 UI 설정이 사용됩니다. 도구 모음 속성은 도구 모음의 단추를 지정하는 데 사용됩니다.

예를 들어 단추 자체가 기능(예: `Bold`)인 경우 `PluginName#FeatureName`(예: `links#modifylink`)으로 지정됩니다.

단추가 팝오버인 경우(플러그인의 일부 기능 포함) `#PluginName`(예: `#format`)으로 지정됩니다.

단추 그룹 사이의 구분자(`|`)는 `-`로 지정할 수 있습니다.

인라인 또는 전체 화면 모드 아래의 팝업 노드에는 사용 중인 팝오버 목록이 포함되어 있습니다. &#39;popopoggles&#39; 노드 아래의 각 하위 노드의 이름은 플러그인(예: 형식)의 이름을 따릅니다. 여기에는 플러그인의 기능 목록(예: format#bold)이 포함된 &#39;items&#39; 속성이 있습니다.

## RTE 사용자 인터페이스 설정 및 컨텐츠 정책 {#rtecontentpolicies}

관리자는 위에서 설명한 대로 구성을 수행하는 대신 컨텐츠 정책을 사용하여 RTE 옵션을 제어할 수 있습니다. 컨텐츠 정책은 [편집 가능한 템플릿](/help/sites-authoring/templates.md)의 일부로 사용할 때 구성 요소의 디자인 속성을 정의합니다. 예를 들어 RTE를 사용하는 텍스트 구성 요소를 편집 가능한 템플릿에 사용하는 경우 컨텐츠 정책에 따라 굵게 옵션을 사용할 수 있고 몇 가지 단락 서식 옵션을 사용할 수 있음을 정의할 수 있습니다. 컨텐츠 정책은 재사용 가능하며, 여러 템플릿에 적용할 수 있습니다.

사용자 인터페이스 구성에서 컨텐츠 정책으로의 다운스트림으로 이동하는 RTE에서 사용할 수 있는 옵션입니다.

* 사용자 인터페이스 구성 설정은 컨텐츠 정책에 사용할 수 있는 옵션을 정의합니다.
* RTE의 사용자 인터페이스 구성이 제거되었거나 항목을 활성화하지 않으면 컨텐츠 정책에서 구성할 수 없습니다.
* 작성자는 사용자 인터페이스 구성 및 컨텐츠 정책에 의해 사용 가능한 기능에만 액세스할 수 있습니다.

예를 들어 [텍스트 코어 구성 요소 설명서](https://docs.adobe.com/help/en/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor)가 표시됩니다.

## 도구 모음 아이콘과 명령 간 매핑 사용자 정의 {#iconstoolbar}

RTE 도구 모음에 표시되는 Coral 아이콘과 사용 가능한 명령 간의 매핑을 사용자 지정할 수 있습니다. Coral 아이콘 외에 다른 아이콘은 사용할 수 없습니다.

1. `uiSettings/cui` 아래에 `icons` 노드를 만듭니다.

1. 아래에 개별 아이콘의 노드를 만듭니다.
1. 각 개별 아이콘 노드에서 Coral 아이콘과 아이콘에 매핑할 명령을 지정합니다.

다음은 Bold 명령을 `textItalic`이라는 Coral 아이콘에 매핑하는 샘플 코드 조각입니다.

```java
<text jcr:primaryType="nt:unstructured" sling:resourceType="cq/gui/components/authoring/dialog/richtext" name="./text" useFixedInlineToolbar="{Boolean}true">
    <rtePlugins jcr:primaryType="nt:unstructured">
        <format jcr:primaryType="nt:unstructured" features="bold,italic"/>
    </rtePlugins>
    <uiSettings jcr:primaryType="nt:unstructured">
        <cui jcr:primaryType="nt:unstructured">
            <inline jcr:primaryType="nt:unstructured"
                toolbar="[format#bold,format#italic,format#underline,links#modifylink,links#unlink]">
            </inline>
            <icons jcr:primaryType="nt:unstructured">
                <bold jcr:primaryType="nt:unstructured"
                    command="format#bold"
                    icon="textItalic"/>
            </icons>
        </cui>
    </uiSettings>
</text>
```

## CoralUI 2 리치 텍스트 편집기로 전환 {#switch-to-coralui-rich-text-editor}

페이지에서 CoralUI 2 RTE clientlib 또는 CoralUI 3 RTE clientlib을 포함할 수 있습니다. 기본적으로 리치 텍스트 편집기에는 CoralUI 3 RTE clientlib이 포함됩니다. CoralUI 2 RTE로 전환하려면 다음 단계를 수행하십시오.

>[!NOTE]
Adobe은 권장하지 않습니다. 마지막 수단으로 CoralUI 2 RTE로 전환합니다. CoralUI 2 RTE용 사용자 지정 플러그인은 플러그인이 클래스와 같은 RTE 도메인에 의존하지 않는 경우 CoralUI 3 RTE에서 작동합니다.
CoralUI3 RTE에 사용자 지정 플러그인을 사용하는 경우 `rte.coralui3` 라이브러리를 사용하십시오.


1. `/apps` 아래에 `/libs/cq/gui/components/authoring/editors/clientlibs/core` 노드를 오버레이하고 다음을 수행합니다.

   * 종속성 속성에 대해 `rte.coralui3` 을 `rte.coralui2` 로 바꾸십시오.
   * 포함 속성의 `cq.authoring.editor.core.inlineediting.rte.coralui3` 을 `cq.authoring.editor.core.inlineediting.rte.coralui2` 로 바꿉니다.
   * 포함 속성의 `cq.authoring.rte.coralui3` 을 `cq.authoring.rte.coralui2` 로 바꿉니다.

1. `/apps` 아래에 `/libs/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui3` 및 `/libs/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui2` 노드를 오버레이합니다.

   `/apps/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui3`에서 `cq.authoring.dialog` 카테고리를 제거하고 `/apps/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui2`에 추가합니다.

1. 페이지에 포함된 다른 종속성을 `rte.coralui3`에서 `rte.coralui2`(으)로 변경합니다. 예를 들어, `/apps` 아래에 노드 `/libs/mcm/campaign/components/touch-ui/clientlibs/rte`을 오버레이한 후 그에 대한 종속성을 `rte.coralui3`에서 `rte.coralui2`(으)로 변경합니다.

1. `/apps` 아래에 `cq/ui/widgets` 노드를 오버레이합니다. `/apps/cq/ui/widgets` 노드의 종속성 `cq.rte`을 `cq.coralui2.rte`(으)로 바꿉니다.

>[!NOTE]
CoralUI 2 RTE는 플러그인 대화 상자에 handlebars 템플릿을 사용합니다. 따라서 CoralUI 2 RTE clientlib은 handlebars clientlib에 대한 종속성을 갖습니다. CoralUI 3 RTE는 handlebars 템플릿을 사용하지 않으며 연관된 종속성이 없습니다. 사용자 지정 플러그인이 handlebars 템플릿을 사용하는 경우 웹 페이지에 handlebars clientlib을 포함하십시오.

## 추가 정보 {#further-information}

RTE 구성에 대한 자세한 내용은 [AEM 위젯 API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.RichText) 참조를 참조하십시오.

특히 사용 가능한 플러그인 및 관련 옵션을 보려면 다음을 수행하십시오.

* [CQ.form.RichText](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin) 구성 요소는 스타일이 지정된 텍스트 정보(리치 텍스트)를 편집하는 양식 필드를 제공합니다. 리치 텍스트 양식에 사용할 수 있는 모든 매개 변수를 확인하려면 구성 옵션 을 참조하십시오.
* RichText 구성 요소는 [CQ.form.rte.plugins.Plugin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin) 아래에 나열된 플러그인을 사용하여 다양한 기능을 제공합니다. 각 플러그인에 대해:

   * 기능을 활성화하거나 비활성화할 수 있는 기능에 대한 자세한 내용은 기능 을 참조하십시오
   * 해당 플러그인의 세부 구성에 사용할 수 있는 모든 매개 변수에 대해서는 구성 옵션 을 참조하십시오

* 링크의 HTML 규칙에 대한 자세한 정보도 사용할 수 있습니다.

고유한 RTE를 확장 및 사용자 지정하는 데 사용할 수 있습니다. 예를 들어 링크를 만들 때 페이지에서 사용할 수 있는 앵커를 나열하려면 `LinkPlugin` 의 자체 구현을 제공할 수 있습니다.

## 알려진 제한 사항 {#known-limitations}

AEM RTE 기능에는 다음과 같은 제한 사항이 있습니다.

* RTE 기능은 AEM 구성 요소 대화 상자에서만 지원됩니다. RTE는 터치 지원 UI의 [페이지 속성](/help/sites-developing/page-properties-views.md) 및 [Scaffolding](/help/sites-authoring/scaffolding.md)과 같은 마법사 또는 Foundation 양식에서 지원되지 않습니다.

* AEM은 [하이브리드 장치에서 작동하지 않습니다](/help/release-notes/known-issues.md).

* RTE 구성 노드 `config` 이름을 지정하지 마십시오. 그렇지 않으면 `content-author` 그룹의 사용자가 아닌 관리자에게만 RTE 구성이 적용됩니다.

* RTE는 컨텐츠를 포함하는 인라인 프레임 또는 iframe을 지원하지 않습니다.

## 우수 사례 및 팁 {#best-practices-and-tips}

* 부동 대화 상자에 팝업 없이 플러그인만 활성화합니다. 팝업이 없는 플러그인의 크기는 더 작으며 부동 대화 상자에 가장 적합합니다.
* `Paste` 플러그인과 같은 큰 팝업에서 전체 화면 대화 상자 모드 또는 전체 화면 모드에서만 플러그인을 활성화합니다. 큰 팝업이 있는 플러그인에는 제작 환경을 잘 제공하기 위해 더 많은 화면 부동산이 필요합니다.
* CoralUI3 RTE에 사용자 지정 플러그인을 사용하는 경우 `rte.coralui3` 라이브러리를 사용하십시오.

## RTE {#troubleshoot-issues-with-aem-rich-text-editor}의 자주 발생하는 문제 해결

**여러 테이블 셀을 선택하는 방법**

테이블에서 여러 셀을 선택하려면 `Ctrl` 또는 `Cmd` 키를 누른 다음 테이블 셀을 하나씩 클릭합니다.

이제 선택 영역에 대해 작업을 수행합니다. 즉 선택한 셀의 속성을 설정합니다.

**구성 단추를 사용하여 구성 요소를 편집할 때 하이퍼링크가 손실됩니다**

구성 단추를 사용하여 텍스트 구성 요소를 편집하여 하이퍼링크를 추가합니다. 하이퍼링크를 다시 편집하고 두 번째로 하이퍼링크를 확인할 때 하이퍼링크를 잃을 수 있습니다.

해결 방법은 두 번째로 편집 대화 상자가 표시되면 텍스트 구성 요소를 클릭하여 링크 유효성 검사를 실행하는 것입니다.

이 문제는 AEM 6.3 이상에서 해결되었습니다.

**소스 편집 모드에 추가된 HTML 콘텐츠가 유실됩니다**

XSS 경향이 있는 HTML을 추가하지 마십시오. RTE가 아닌 AEM에서 XSS 광고성 규칙을 준수하기 위해 일부 HTML 콘텐츠를 제거할 수 있습니다.

붙여넣은 HTML이 저장되었는지 확인하려면 CRXDE(컨텐츠 노드)에 저장된 컨텐츠를 확인합니다.

저장하지 않는 경우 HTML은 RTE의 규칙을 준수하지 않으므로 RTE에서 제거했어야 합니다.

CRXDE에 저장되었지만 페이지에서 렌더링되지 않은 경우(렌더링을 확인하려면 페이지의 [미리 보기](/help/sites-authoring/editing-content.md#preview-mode)를 참조하십시오) AEM XSS 규칙으로 제거됩니다.

**다중 필드 구성 요소가 예상대로 작동하지 않습니다**

다중 필드 구성 요소를 만들려면 CoralUI 3만 사용합니다. CoralUI 2 구성 요소 대화 상자를 사용하지 마십시오.

또한 다중 필드 구현 코드와 노드 구조가 올바른지 확인합니다.

**작성자는 관리자가 사용할 수 있는 구성을 사용할 수 없습니다**

인터페이스 구성 업데이트가 관리자에 대해 반영되지만 작성자 계정이 아닌 경우 구성 노드의 이름이 `config`이 아닌지 확인합니다. [`configPath` 속성](/help/sites-developing/components-basics.md#cq-inplaceediting)을 사용하십시오.

>[!MORELIKETHIS]
* [RTE 플러그인 구성](configure-rich-text-editor-plug-ins.md)
* [작성을 위해 리치 텍스트 편집기 사용](../sites-authoring/rich-text-editor.md)
* [액세스 가능한 사이트에 대한 RTE 구성](rte-accessible-content.md)
* [Touch UI 및 클래식 UI 기능 패리티](../release-notes/touch-ui-features-status.md)
* [복합 다중 필드 구성 요소를 만들기 위한 자습서 샘플](https://experience-aem.blogspot.com/2019/05/aem-65-touchui-composite-multifield-with-coral3-rte-rich-text.html)

