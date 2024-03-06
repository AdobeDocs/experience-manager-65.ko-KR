---
title: Adobe Experience Manager에서 컨텐츠를 작성하도록 리치 텍스트 편집기를 구성합니다.
description: Adobe Experience Manager에서 컨텐츠를 작성하도록 Adobe Experience Manager 리치 텍스트 편집기를 구성하는 방법에 대해 알아봅니다.
contentOwner: AG
exl-id: 2e7ec22f-0856-44c4-bb15-1086dae0b85a
source-git-commit: 0aa929021aa724e4ec18d49fea26f8c0b0538bdc
workflow-type: tm+mt
source-wordcount: '2887'
ht-degree: 0%

---

# 리치 텍스트 편집기 구성 {#configure-the-rich-text-editor}

리치 텍스트 편집기(RTE)는 작성자가 텍스트 콘텐츠를 편집할 수 있는 다양한 기능을 제공합니다. WYSIWYG 텍스트 편집 환경을 위해 아이콘, 선택 상자, 도구 모음 및 메뉴가 제공됩니다.

작성을 위해 RTE 기능을 사용하는 방법은 다음을 참조하십시오. [작성을 위해 리치 텍스트 편집기 사용](/help/sites-authoring/rich-text-editor.md). 작성 구성 요소에서 사용할 수 있는 기능을 활성화, 비활성화 및 확장하도록 RTE를 구성할 수 있습니다. 다음 워크플로우는 Experience Manager에서 RTE 구성 작업을 완료하는 권장 순서를 보여 줍니다.

![RTE를 구성하는 방법을 알아보는 단계 순서](assets/rte_workflow_v1.png)

*그림: RTE를 구성하는 방법을 알아보는 단계 순서*

## 터치 지원 UI 및 클래식 UI 이해 {#understand-touch-enabled-ui-and-classic-ui}

터치 지원 UI는 Experience Manager을 위한 표준 사용자 인터페이스입니다. Adobe에 터치 지원 UI 도입 [반응형 디자인](/help/sites-authoring/responsive-layout.md) 작성 환경용입니다. 터치 지원 UI는 터치 및 데스크탑 디바이스용으로 설계되었습니다. 인터페이스는 기존 클래식 UI와 상당히 다릅니다.

![터치 지원 사용자 인터페이스의 리치 텍스트 편집기 도구 모음](assets/chlimage_1-35.png)

*그림: 터치 지원 UI의 리치 텍스트 편집기 도구 모음*

![클래식 UI의 리치 텍스트 편집기 도구 모음](assets/rtedefault.png)

*그림: 클래식 UI의 리치 텍스트 편집기 도구 모음*

>[!MORELIKETHIS]
>
>* [UI 권장 사항](/help/sites-deploying/ui-recommendations.md)
>* 클래식 UI 사용 중단에 대한 자세한 내용은 [Experience Manager 6.5 릴리스 노트](/help/release-notes/deprecated-removed-features.md)
>* UI 간의 차이점은 을 참조하십시오. [Touch UI 및 클래식 UI](https://aemcq5pedia.wordpress.com/2018/01/05/touch-enabled-ui-aem6-3/)
>* 터치 지원 UI에 대한 자세한 내용은 [Experience Manager 터치 UI의 개념](/help/sites-developing/touch-ui-concepts.md)

## 다양한 편집 모드 {#editingmodes}

작성자는 다양한 구성 요소 모드를 사용하여 Experience Manager에서 텍스트 콘텐츠를 만들고 편집할 수 있습니다. 다른 편집 모드에서 RTE 사용 구성 요소의 사용자 경험 및 컨텐츠를 작성하고 형식을 지정하기 위한 도구 모음 옵션은 RTE 구성에 따라 다릅니다.

| 편집 모드 | 편집 영역 | 활성화할 권장 기능 | Touch UI | 클래식 UI |
|--- |--- |--- |--- |--- |
| 인라인 | 빠르고 사소한 편집을 위한 즉석 편집, 대화 상자를 열지 않은 포맷 | 최소 RTE 기능 | Y | Y |
| RTE 전체 화면 | 전체 페이지 포함 | 필요한 모든 RTE 기능 | Y | N |
| 대화 상자 | 페이지 컨텐츠 위에 있지만 전체 페이지를 다루지 않는 대화 상자 | 클래식 UI에 필요한 모든 RTE 기능, 터치 UI에 신중하게 기능 활성화 | Y | Y |
| 대화 상자 전체 화면 | 전체 화면 모드와 동일; RTE와 함께 대화 상자의 필드를 포함 | 필요한 모든 RTE 기능 | Y | N |

>[!NOTE]
>
>터치 지원 UI의 인라인 편집 모드에서는 소스 편집 기능을 사용할 수 없습니다. 전체 화면 모드에서는 이미지를 드래그할 수 없습니다. 다른 모든 기능은 모든 모드에서 작동합니다.

### 인라인 편집 {#inline-editing}

열면(느리게 두 번 클릭) 페이지 내에서 콘텐츠를 편집할 수 있습니다. 매우 기본적인 옵션이 있는 작은 도구 모음이 표시됩니다.

![터치 지원 UI에서 기본 도구 모음을 사용하여 인라인 편집](assets/chlimage_1-36.png)

*그림: 터치 지원 UI에서 기본 도구 모음을 사용하여 인라인 편집*

클래식 UI에서 구성 요소를 천천히 더블 클릭하면 인라인 편집이 가능하고 주황색 윤곽선이 콘텐츠를 강조 표시합니다. 컨텐츠 파인더가 열려 있으면 사용 가능한 RTE 서식 옵션이 있는 도구 모음이 창 맨 위에 표시됩니다. 컨텐츠 파인더가 열리지 않으면 서식 옵션이 표시되지 않으며 기본 텍스트 편집만 수행할 수 있습니다.

### 전체 화면 편집 {#full-screen-editing}

Experience Manager 구성 요소를 전체 화면 보기에서 열어 페이지 콘텐츠를 숨기고 사용 가능한 화면을 차지할 수 있습니다. 인라인 편집은 가장 많은 편집 옵션을 제공하므로 전체 화면 편집을 고려하십시오. 다음을 클릭하여 열 수 있습니다. ![rte_fullscreen](assets/rte_fullscreen.png)인라인 편집 모드를 사용할 때 압축 도구 모음에서 를 클릭합니다.

대화 상자 전체 화면 모드에서는 세부 RTE 도구 모음과 함께 대화 상자에서 사용할 수 있는 옵션 및 구성 요소도 사용할 수 있습니다. 다른 구성 요소와 함께 RTE가 포함된 대화 상자에만 적용됩니다.

![터치 지원 UI에서 전체 화면 모드로 편집할 때 자세한 RTE 도구 모음](assets/chlimage_1-37.png)

*그림: 터치 지원 UI에서 전체 화면 모드로 편집할 때 자세한 RTE 도구 모음*

### 대화 상자 편집 {#dialog-editing}

구성 요소를 두 번 클릭하면 콘텐츠를 편집할 수 있는 대화 상자가 열립니다. 대화 상자가 기존 페이지 위에 열립니다. 일부 특정 시나리오에서는 대화 상자가 팝업 창으로 열립니다. 예를 들어 텍스트 구성 요소가 다중 열 페이지 레이아웃의 열에 속하고 대화 상자에 사용할 수 있는 영역이 적은 경우.

![터치 지원 UI의 대화 상자 편집 모드](assets/dialog_editing_modetouchui.png)

*그림: 터치 지원 UI의 대화 상자 편집 모드*

![편집을 위한 세부 도구 모음이 포함된 클래식 UI의 대화 상자](assets/chlimage_1-38.png)

*그림: 편집을 위한 세부 도구 모음이 포함된 클래식 UI의 대화 상자*

## RTE 플러그인 및 관련 기능 정보 {#aboutplugins}

이 기능은 각각 다음과 같은 일련의 플러그인을 통해 사용할 수 있습니다.

* A `features` 속성:

   * 해당 플러그인의 기본 기능을 활성화 또는 비활성화하는 데 사용됩니다.
   * 표준화된 절차를 사용하여 구성할 수 있습니다

* 필요한 경우 추가 속성 및 옵션을 사용하여 특수 구성을 수행해야 합니다.

RTE의 기본 기능은 의 값에 따라 활성화되거나 비활성화됩니다. `features` 적절한 플러그인과 관련된 노드의 속성입니다.

다음 표에는 현재 플러그인이 나열되어 있습니다.

* API 설명서 링크가 있는 플러그인 ID. ID는 다음과 같은 경우에 노드 이름으로 사용됩니다. [플러그인 활성화](/help/sites-administering/configure-rich-text-editor-plug-ins.md#activateplugin).
* 에 대해 허용되는 값 `features` 속성.
* 플러그인에서 제공하는 기능에 대한 설명입니다.

| 플러그인 ID | 기능 | 설명 |
|--- |--- |--- |
| 편집 | 잘라내기 복사 붙여넣기-기본 붙여넣기-일반 텍스트 붙여넣기-단어 html | [잘라내기, 복사 및 세 가지 붙여넣기 모드](/help/sites-administering/configure-rich-text-editor-plug-ins.md#textstyles). |
| 핀드레플레이스 | 바꾸기 찾기 | 찾아 바꾸기. |
| 형식 | 굵은 기울임꼴 밑줄 | [기본 텍스트 서식](/help/sites-administering/configure-rich-text-editor-plug-ins.md#textstyles). |
| 이미지 | 이미지 | 기본 이미지 지원(콘텐츠 또는 콘텐츠 파인더에서 드래그). 브라우저에 따라 작성자에 대한 지원 동작이 다릅니다 |
| 키 |  | 이 값을 정의하려면 다음을 참조하십시오 [탭 크기](/help/sites-administering/configure-rich-text-editor-plug-ins.md#tabsize). |
| 양쪽 맞춤 | justifyleft justifycenter justifyright | 단락 정렬. |
| 링크 | modifylink 연결 해제 앵커 | [하이퍼링크 및 앵커](/help/sites-administering/configure-rich-text-editor-plug-ins.md#linkstyles). |
| 목록 | 순서가 지정되지 않은 들여쓰기 내어쓰기 | 이 플러그인은 두 가지 작업을 모두 제어합니다. [들여쓰기 및 목록](/help/sites-administering/configure-rich-text-editor-plug-ins.md#indentmargin); 중첩된 목록 포함. |
| misctools | specialchars sourceedit | 기타 도구를 사용하면 작성자가 입력할 수 있습니다 [특수 문자](/help/sites-administering/configure-rich-text-editor-plug-ins.md#spchar) 또는 HTML 소스를 편집합니다. 또한 전체를 추가할 수도 있습니다 [특수 문자 범위](/help/sites-administering/configure-rich-text-editor-plug-ins.md#definerangechar) 고유한 목록을 정의하려는 경우 |
| Paraformat | paraformat | 기본 단락 형식은 단락, 제목 1, 제목 2 및 제목 3 입니다(`<p>`, `<h1>`, `<h2>`, 및 `<h3>`). 다음을 수행할 수 있습니다. [더 많은 단락 형식 추가](/help/sites-administering/configure-rich-text-editor-plug-ins.md#paraformats) 또는 목록을 확장합니다. |
| 맞춤법 검사 | checktext | [언어 인식 맞춤법 검사기](/help/sites-administering/configure-rich-text-editor-plug-ins.md#adddict). |
| 스타일 | 스타일 | CSS 클래스를 사용한 스타일링을 지원합니다. [새 텍스트 스타일 추가](/help/sites-administering/configure-rich-text-editor-plug-ins.md#textstyles) 텍스트에서 사용할 고유한 스타일 범위를 추가(또는 확장)하려는 경우 |
| 부분 위 첨자 | 아래 첨자 위 첨자 | 기본 형식에 대한 확장, 하위 스크립트 및 슈퍼 스크립트 추가. |
| 표 | 테이블 제거 가능 삽입행 제거열 제거열 제거셀 병합splitcell selectrow 선택열 | 다음을 참조하십시오 [표 스타일 구성](/help/sites-administering/configure-rich-text-editor-plug-ins.md#tablestyles)전체 표 또는 개별 셀에 고유한 스타일을 추가하려면 를 선택합니다. |
| 실행 취소 | 다시 실행 취소 | 기록 크기 [실행 취소 및 다시 실행](/help/sites-administering/configure-rich-text-editor-plug-ins.md#undohistory) 작업. |

>[!NOTE]
>
>대화 상자 모드에서는 전체 화면 플러그인이 지원되지 않습니다. 사용 `dialogFullScreen` 을 설정하여 전체 화면 모드에 대한 도구 모음을 구성합니다.

## 구성 경로 및 위치 이해 {#understand-the-configuration-paths-and-locations}

다음 [RTE 편집 모드(및 UI)](#editingmodes) 작성자를 위해 제공한 는 다음과 같은 상황에서 구성 세부 정보의 위치를 결정합니다. [RTE 플러그인 활성화](/help/sites-administering/configure-rich-text-editor-plug-ins.md#activateplugin):

| 편집 모드 | Touch UI 위치 | 클래식 UI 위치 |
|---|---|---|
| 인라인 | `cq:editConfig/cq:inplaceEditing` | `cq:editConfig/cq:inplaceEditing` |
| 전체 화면 | `cq:editConfig/cq:inplaceEditing` | 해당되지 않음 |
| 대화 상자 | `cq:dialog` | `dialog` |
| 전체 화면 대화 상자 | `cq:dialog` | 해당되지 않음 |

>[!NOTE]
>
>아래에 노드의 이름을 지정하지 마십시오. `cq:inplaceEditing` 다음으로: `config`. 날짜 `cq:inplaceEditing` 노드를 정의하고 다음 속성을 정의합니다.
>* **이름**: `configPath`
>* **유형**: `String`
>* **값**: 실제 구성이 포함된 노드의 경로
>
>RTE 구성 노드의 이름을 로 지정하지 마십시오. `config`. 그렇지 않으면 RTE 구성은 관리자에게만 적용되며 그룹의 사용자에게는 적용되지 않습니다 `content-author`.

Touch UI의 대화 상자 편집 모드에서만 적용되는 다음 속성을 구성합니다.

* `useFixedInlineToolbar`: RTE 노드에 정의된 이 부울 속성(sling:resourceType=가 있는 속성)을 설정합니다. `cq/gui/components/authoring/dialog/richtext`) 받는 사람 `True`를 클릭하여 RTE 도구 모음을 부동 대신 고정하도록 할 수 있습니다.

  이 속성이 true이면 기본적으로 Richtext 편집이 &quot;foundation-contentloaded&quot; 이벤트에서 시작됩니다.

  이를 방지하려면 속성을 설정합니다 `customStart` 끝 `True`및 &#39;rte-start&#39; 이벤트를 트리거하여 RTE 편집을 시작합니다. 이 속성이 &#39;true&#39;이면 기본 동작인 클릭 시 rte가 작동하지 않습니다.

* `customStart`: RTE 노드에 정의된 이 부울 속성을 다음으로 설정 `True`이벤트를 트리거하여 RTE를 시작할 시기를 제어합니다. `rte-start`.

* `rte-start`: 다음에서 이 이벤트 트리거 `contenteditable-div` RTE의 경우 RTE 편집을 시작할 때입니다. 이 기능은 다음과 같은 경우에만 작동합니다. `customStart` 이(가) true로 설정되었습니다.

터치 사용 대화 상자에서 RTE를 사용하는 경우, 속성을 설정합니다. `useFixedInlineToolbar` 문제를 방지하려면 true로 설정해야 합니다.

## 즉석 편집 사용자 지정 {#customizing-in-place-editing}

다음 속성을 구성하여 텍스트 편집기가 시작되는 HTML 선택기를 정의할 수 있습니다.

* **`editElementQuery`** - 정의 날짜 `cq:InplaceEditingConfig`, 이 속성은 텍스트 구성 요소에 대한 인라인 편집을 시작할 HTML 요소의 선택기를 지정하는 데 사용됩니다. 지정하지 않으면 인라인 편집이 텍스트 구성 요소 HTML에서 직접 시작됩니다.
* **`textPropertyName`** - 정의 날짜 `cq:InplaceEditingConfig`, 이 속성은 인라인 편집 후 텍스트 구성 요소의 HTML 값이 유지되는 콘텐츠 노드에 저장될 속성의 이름을 지정하는 데 사용됩니다.

대화 상자 모드의 해당 속성은 다음과 같습니다. `name`.

## 플러그인을 활성화하여 RTE 기능 활성화 {#enable-rte-functionalities-by-activating-plug-ins}

RTE 기능은 기능 속성이 있는 일련의 플러그인을 통해 사용할 수 있습니다. 각 플러그인의 다양한 기능을 활성화하거나 비활성화하도록 기능 속성을 구성할 수 있습니다.

RTE 플러그인의 자세한 구성은 다음을 참조하십시오. [rte 플러그인을 활성화하고 구성하는 방법](/help/sites-administering/configure-rich-text-editor-plug-ins.md).

**샘플**: 다운로드 [이 샘플 구성](/help/sites-administering/assets/rte-sample-all-features-enabled-10.zip) 는 RTE를 구성하는 방법을 보여 줍니다. 이 패키지에서는 모든 기능이 활성화됩니다.

>[!NOTE]
>
>다음 [코어 구성 요소 텍스트 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor) 템플릿 편집자는 GUI에서 많은 RTE 플러그인을 콘텐츠 정책으로 구성할 수 있으므로 기술 구성이 필요하지 않습니다. 콘텐츠 정책은 이 문서에 설명된 대로 RTE UI 구성에서 작동할 수 있습니다.
>
>자세한 내용은 [RTE UI 설정 및 콘텐츠 정책](/help/sites-administering/rich-text-editor.md) 이 문서의 섹션 및 [페이지 템플릿 만들기](/help/sites-authoring/templates.md) 및 [핵심 구성 요소 개발자 설명서](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/developing.html).

>[!NOTE]
>
>참조용으로 기본 텍스트 구성 요소(표준 설치의 일부로 제공)는 다음에서 찾을 수 있습니다.
>
>* `/libs/wcm/foundation/components/text`
>* `/libs/foundation/components/text`
>
>고유한 텍스트 구성 요소를 만들려면 이러한 구성 요소를 편집하는 대신 위의 구성 요소를 복사하십시오.

## RTE 도구 모음 구성 {#dialogfullscreen}

AEM을 사용하면 리치 텍스트 편집기에 대한 인터페이스를 다양한 편집 모드에 대해 다르게 구성할 수 있습니다. 기본 설정은 아래에 제공됩니다. 요구 사항에 따라 이러한 기본값을 재정의할 수 있습니다. 작성자에게 제공할 도구 모음 기능만 사용자 지정합니다. 모든 도구 모음 구성을 지정할 필요는 없습니다.

다음에 대한 도구 모음을 구성하려면 `dialogFullScreen`, 다음 샘플 구성을 사용하십시오.

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

인라인 모드와 전체 화면 모드에서는 서로 다른 UI 설정이 사용됩니다. toolbar 속성은 도구 모음의 단추를 지정하는 데 사용됩니다.

예를 들어 버튼이 그 자체인 경우 (예: `Bold`)으로 지정됩니다. `PluginName#FeatureName` (예: `links#modifylink`).

단추가 팝오버(플러그인의 일부 기능 포함)이면 다음과 같이 지정됩니다. `#PluginName` (예: `#format`).

구분 기호(`|`) 단추 그룹 사이에 을 사용하여 지정할 수 있습니다. `-`.

인라인 또는 전체 화면 모드 아래의 팝업 노드에는 사용 중인 팝오버 목록이 포함됩니다. &#39;popovers&#39; 노드 아래의 각 하위 노드의 이름은 플러그인(예: format) 이름을 따서 지정합니다. 여기에는 플러그인의 기능 목록을 포함하는 속성 &#39;items&#39;가 있습니다(예: format#bold).

## RTE 사용자 인터페이스 설정 및 콘텐츠 정책 {#rtecontentpolicies}

관리자는 위에서 설명한 대로 구성을 수행하는 대신 콘텐츠 정책을 사용하여 RTE 옵션을 제어할 수 있습니다. 콘텐츠 정책은 의 일부로 사용할 때 구성 요소의 디자인 속성을 정의합니다. [편집 가능한 템플릿](/help/sites-authoring/templates.md). 예를 들어 RTE를 사용하는 텍스트 구성 요소를 편집 가능한 템플릿과 함께 사용하는 경우 콘텐츠 정책에서 굵게 옵션을 사용할 수 있고 몇 가지 단락 서식 옵션을 사용할 수 있도록 정의할 수 있습니다. 콘텐츠 정책은 재사용이 가능하며 여러 템플릿에 적용할 수 있습니다.

RTE에서 사용할 수 있는 옵션은 사용자 인터페이스 구성에서 콘텐츠 정책으로 다운스트림됩니다.

* 사용자 인터페이스 구성 설정은 콘텐츠 정책에 사용할 수 있는 옵션을 정의합니다.
* RTE의 사용자 인터페이스 구성이 제거되었거나 항목을 사용할 수 없는 경우 콘텐츠 정책이 항목을 구성할 수 없습니다.
* 작성자는 사용자 인터페이스 구성 및 콘텐츠 정책에 의해 제공되는 기능에만 액세스할 수 있습니다.

예를 들어 다음을 볼 수 있습니다. [텍스트 핵심 구성 요소 설명서](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/text.html#the-text-component-and-the-rich-text-editor).

## 도구 모음 아이콘과 명령 간의 매핑 사용자 정의 {#iconstoolbar}

RTE 도구 모음에 표시되는 Coral 아이콘과 사용 가능한 명령 간의 매핑을 사용자 정의할 수 있습니다. 코랄 아이콘 이외의 다른 아이콘은 사용할 수 없습니다.

1. 다음 이름의 노드 만들기 `icons` 아래에 `uiSettings/cui`.

1. 아래에 개별 아이콘에 대한 노드를 만듭니다.
1. 각 개별 아이콘 노드에서 Coral 아이콘과 해당 아이콘에 매핑할 명령을 지정합니다.

다음은 Bold 명령을 Coral 아이콘에 매핑하는 샘플 코드 조각입니다. `textItalic`.

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
>
>Adobe은 모범 사례로 권장하지 않습니다. 마지막 수단으로 CoralUI 2 RTE로 전환하십시오. CoralUI 2 RTE에 대한 사용자 지정 플러그인은 플러그인이 클래스와 같은 RTE 내부에 의존하지 않는 경우 CoralUI 3 RTE에서 작동합니다.
>
>CoralUI3 RTE에 대한 사용자 지정 플러그인을 사용하는 경우 다음을 사용하십시오. `rte.coralui3` 라이브러리입니다.


1. 노드 오버레이 `/libs/cq/gui/components/authoring/editors/clientlibs/core` 아래에 `/apps`을 클릭하고 다음을 수행합니다.

   * 바꾸기 `rte.coralui3` 포함 `rte.coralui2` 종속성 속성.
   * 바꾸기 `cq.authoring.editor.core.inlineediting.rte.coralui3` 포함 `cq.authoring.editor.core.inlineediting.rte.coralui2` 포함 속성용.
   * 바꾸기 `cq.authoring.rte.coralui3` 포함 `cq.authoring.rte.coralui2` 포함 속성용.

1. 노드 오버레이 `/libs/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui3` 및 `/libs/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui2` 아래에 `/apps`.

   범주 제거 `cq.authoring.dialog` 출처: `/apps/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui3` 및 추가 `/apps/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui2`.

1. 다음에서 페이지에 포함되는 다른 종속성 변경 `rte.coralui3` 끝 `rte.coralui2`. 예를 들어 노드를 오버레이한 후 `/libs/mcm/campaign/components/touch-ui/clientlibs/rte` 아래에 `/apps`, 모든 종속성을 다음으로 변경 `rte.coralui3` 끝 `rte.coralui2`.

1. 노드 오버레이 `cq/ui/widgets` 아래에 `/apps`. 종속성 바꾸기 `cq.rte` 노드에서 `/apps/cq/ui/widgets` 포함 `cq.coralui2.rte`.

>[!NOTE]
>
>CoralUI 2 RTE는 플러그인 대화 상자에 핸들바 템플릿을 사용합니다. 따라서 CoralUI 2 RTE clientlib은 handlebars clientlib에 종속되었습니다. CoralUI 3 RTE는 핸들바 템플릿을 사용하지 않으며 관련 종속성이 없습니다. 사용자 지정 플러그인이 Handlebars 템플릿을 사용하는 경우 웹 페이지에 handlebars clientlib을 포함합니다.

## 추가 정보 {#further-information}

RTE 구성에 대한 자세한 내용은 [AEM 위젯 API](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.RichText) 참조.

특히, 사용 가능한 플러그인 및 관련 옵션을 보려면 다음과 같이 하십시오.

* 다음 [CQ.form.RichText](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.RichText) 구성 요소는 스타일이 지정된 텍스트 정보(서식 있는 텍스트)를 편집하는 데 사용할 양식 필드를 제공합니다. 리치 텍스트 양식에 사용할 수 있는 모든 매개 변수를 알아보려면 구성 옵션 을 참조하십시오.
* RichText 구성 요소는 아래에 나열된 플러그인을 사용하여 다양한 기능을 제공합니다. [CQ.form.rte.plugins.Plugin](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin). 각 플러그인의 경우:

   * 활성화(또는 비활성화)할 수 있는 기능에 대한 자세한 내용은 기능 을 참조하십시오
   * 적절한 플러그인의 세부 구성에 사용할 수 있는 모든 매개 변수에 대한 구성 옵션 을 참조하십시오

* 링크의 HTML 규칙에 대한 자세한 정보도 사용할 수 있습니다.

RTE를 확장하거나 사용자 지정하는 데 사용할 수 있습니다. 예를 들어 링크를 만들 때 페이지에서 사용할 수 있는 앵커를 나열하려면 의 고유한 구현을 제공할 수 있습니다. `LinkPlugin`.

## 알려진 제한 사항 {#known-limitations}

AEM RTE 기능에는 다음과 같은 제한 사항이 있습니다.

* RTE 기능은 AEM 구성 요소 대화 상자에서만 지원됩니다. RTE는 다음과 같은 마법사 또는 Foundation 양식에서 지원되지 않습니다. [페이지 속성](/help/sites-developing/page-properties-views.md) 및 [스캐폴딩](/help/sites-authoring/scaffolding.md) 터치 지원 UI에서.

* AEM이 작동하지 않음 [하이브리드 장치](/help/release-notes/release-notes.md).

* RTE 구성 노드의 이름을 지정하지 마십시오 `config`. 그렇지 않으면 RTE 구성은 관리자에게만 적용되며 그룹의 사용자에게는 적용되지 않습니다 `content-author`.

* RTE는 컨텐츠를 포함할 인라인 프레임 또는 iframe을 지원하지 않습니다.

## 모범 사례 및 팁 {#best-practices-and-tips}

* 부동 대화 상자에 대한 팝업 없이 플러그인만 활성화합니다. 팝업이 없는 플러그인은 크기가 더 작으며 부동 대화 상자에 가장 적합합니다.
* 다음과 같이 큰 팝업으로 플러그인을 활성화합니다. `Paste` 플러그인은 전체 화면 대화 상자 모드 또는 전체 화면 모드에서만 사용할 수 있습니다. 팝업이 큰 플러그인은 좋은 작성 환경을 제공하기 위해 더 많은 화면 실제가 필요합니다.
* CoralUI3 RTE에 대한 사용자 지정 플러그인을 사용하는 경우 다음을 사용하십시오. `rte.coralui3` 라이브러리입니다.

## RTE의 빈번한 문제 해결 {#troubleshoot-issues-with-aem-rich-text-editor}

**여러 테이블 셀을 선택하는 방법**

테이블에서 여러 셀을 선택하려면 `Ctrl` 또는 `Cmd` 키를 누른 다음 테이블 셀을 하나씩 클릭합니다.

이제 선택한 셀의 속성을 설정하여 선택 항목에 대한 작업을 수행합니다.

**구성 단추를 사용하여 구성 요소를 편집할 때 하이퍼링크가 손실됩니다.**

구성 단추를 사용하여 텍스트 구성 요소를 편집하여 하이퍼링크를 추가합니다. 하이퍼링크를 다시 편집하고 두 번째로 유효성을 검사할 때 하이퍼링크가 손실될 수 있습니다.

해결 방법은 편집 대화 상자가 두 번째로 표시될 때 텍스트 구성 요소를 클릭한 다음 링크 유효성 검사를 실행하는 것입니다.

이 문제는 AEM 6.3 이상에서 해결되었습니다.

**소스 편집 모드에 추가된 HTML 컨텐츠가 손실됩니다.**

XSS 유발 HTML을 추가하지 마십시오. RTE가 아닌 AEM은 XSS antisamy 규칙을 준수하도록 일부 HTML 콘텐츠를 제거할 수 있습니다.

붙여넣은 HTML이 저장되었는지 확인하려면 CRXDE(콘텐츠 노드)에 저장된 콘텐츠를 확인합니다.

저장하지 않았다면 HTML이 RTE의 규칙을 준수하지 않아 RTE에서 제거했어야 합니다.

CRXDE에 저장되었지만 페이지에서 렌더링되지 않은 경우 렌더링을 확인하려면 페이지 [미리보기](/help/sites-authoring/editing-content.md#preview-mode), AEM XSS 규칙에 의해 제거됩니다.

**다중 필드 구성 요소가 예상대로 작동하지 않음**

다중 필드 구성 요소를 만들려면 CoralUI 3만 사용하십시오. CoralUI 2 구성 요소 대화 상자를 사용하지 마십시오.

또한 다중 필드 구현 코드와 노드 구조가 올바른지 확인하십시오.

**관리자가 사용할 수 있는 구성은 작성자가 사용할 수 없습니다.**

인터페이스 구성 업데이트가 관리자에 대해 반영되지만 작성자 계정에 대해서는 반영되지 않는 경우 구성 노드의 이름이 지정되지 않았는지 확인합니다 `config`. 사용 [`configPath` 속성](/help/sites-developing/components-basics.md#cq-inplaceediting).

>[!MORELIKETHIS]
>
>* [RTE 플러그인 구성](configure-rich-text-editor-plug-ins.md)
>* [작성을 위해 리치 텍스트 편집기 사용](../sites-authoring/rich-text-editor.md)
>* [액세스 가능한 사이트에 대한 RTE 구성](rte-accessible-content.md)
>* [Touch UI 및 클래식 UI 기능 패리티](../release-notes/touch-ui-features-status.md)
>* [복합 다중 필드 구성 요소를 만드는 튜토리얼 샘플](https://experience-aem.blogspot.com/2019/05/aem-65-touchui-composite-multifield-with-coral3-rte-rich-text.html)
