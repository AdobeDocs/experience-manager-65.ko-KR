---
title: 여러 즉석 편집기에 대한 RTE를 구성합니다.
description: 리치 텍스트 편집기를 구성하여 Adobe Experience Manager에서 여러 즉석 편집기를 만들 수 있습니다.
contentOwner: AG
exl-id: 03030317-8b7d-408a-bdfd-619824d7260c
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 1%

---

# 여러 즉석 편집기 구성 {#configure-multiple-in-place-editors}

여러 개의 즉석 편집기가 생기도록 Adobe Experience Manager에서 리치 텍스트 편집기를 구성할 수 있습니다. 구성된 경우 적절한 콘텐츠를 선택하고 적절한 편집기를 열 수 있습니다.

![특정 즉석 편집기](assets/rte-inplace-editor.png)

## 여러 편집기 구성 {#configure-multiple-editors}

여러 즉석 편집기를 활성화하려면 `cq:InplaceEditingConfig` 노드 유형이 의 정의로 향상되었습니다. `cq:ChildEditorConfig` 노드 유형.

예:

```js
   /**
       * Configures in-place editing of a component.
       *
       * @prop active true to activate in-place editing for the component.
       * @prop editorType ID of in-place editor to use.
       * @prop cq:childEditors collection of {@link cq:ChildEditorConfig} nodes.
       * @prop configPath path to editor's config (optional).
       * @node config editor's config (used if no configPath is specified; optional).
     */
    [cq:InplaceEditingConfig] > nt:unstructured
      - active (boolean)
      - editorType (string)
      + cq:childEditors (nt:base) = nt:unstructured
      - configPath (string)
      + config (nt:unstructured) = nt:unstructured

    /**
      * Configures one child editor for a sub-component. The name of the this node is
      * used as DD ID.
      *
      * @prop type type of the inline editor. For example, ["image"].
      * @prop title Title of the inline editor.
      * @prop icon Icon to represent the inline editor.
    */
    [cq:ChildEditorConfig] > nt:unstructured
      orderable
      - type (string)
      - title (string)
```

여러 편집기를 구성하려면 다음 단계를 수행합니다.

1. 노드에서 `cq:inplaceEditing` (유형의) `cq:InplaceEditingConfig`) 다음 속성을 정의합니다.

   * 이름:`editorType`
   * 유형: `String`
   * 값: `hybrid`

1. 이 노드 아래에서 노드를 만듭니다.

   * 이름: `cq:ChildEditors`
   * 유형: `nt:unstructured`

1. 아래 `cq:childEditors` 노드, 각 즉석 편집기에 대한 노드를 만듭니다.

   * 이름: 각 노드의 이름은 대상 삭제의 경우와 마찬가지로 나타내는 속성의 이름입니다. 예를 들어, `image` 및 `text`.
   * 유형: `cq:ChildEditorConfig`

   >[!NOTE]
   >
   >정의된 드롭 대상과 하위 편집기 사이에는 상관 관계가 있습니다. 의 이름입니다. `cq:ChildEditorConfig` 노드는 선택한 하위 편집기의 매개 변수로 사용할 수 있는 드롭 대상 ID로 간주됩니다. 편집 가능한 하위 영역에 드롭 대상이 없는 경우(예: 텍스트 구성 요소) 하위 편집기의 이름은 여전히 해당 편집 가능한 영역을 식별하는 ID로 간주됩니다.

1. 이러한 각 노드에서 (`cq:ChildEditorConfig`) 속성을 정의합니다.

   * 이름: `type`.
   * 값: 등록된 즉석 편집기의 이름(예: ) `image` 및 `text`.

   * 이름: `title`.
   * 값: 사용 가능한 편집기의 구성 요소 선택 목록에 표시되는 제목입니다. 예를 들어, `Image` 및 `Text`.

### 리치 텍스트 편집기에 대한 추가 구성 {#additional-configuration-for-rich-text-editors}

각 개별 RTE 인스턴스를 개별적으로 구성할 수 있으므로 여러 리치 텍스트 편집기에 대한 구성은 약간 다릅니다. 자세한 내용은 [리치 텍스트 편집기 구성](/help/sites-administering/rich-text-editor.md). 여러 RTE를 통해 각 즉석 RTE에 대한 구성을 만들 수 있습니다. Adobe은 아래에 새 구성 노드를 만들 것을 권장합니다. `cq:InplaceEditingConfig` 각 개별 RTE가 다른 구성을 가질 수 있으므로. 새 노드 아래에 각 개별 RTE 구성을 만듭니다.

```xml
    texttext
        cq:dialog
        cq:editConfig
            cq:inplaceEditing
                cq:childEditors
                    someconfig
                        text1
                            rtePlugins
                        text2
                            rtePlugins
```

>[!NOTE]
>
>그러나 RTE의 경우 `configPath` 구성 요소에 텍스트 편집기 인스턴스(편집 가능한 하위 영역)가 하나만 있는 경우 속성이 지원됩니다. 의 이 사용 `configPath` 구성 요소의 이전 사용자 인터페이스 대화 상자와 이전 버전과의 호환성을 지원하기 위해 제공됩니다.

>[!CAUTION]
>
>RTE 구성 노드의 이름을 로 지정하지 마십시오. `config`. 그렇지 않으면 RTE 구성은 관리자만 사용할 수 있고 그룹의 사용자에게는 사용할 수 없습니다 `content-author`.

## 코드 샘플 {#code-samples}

이 페이지의 코드는에서 찾을 수 있습니다. [GitHub의 aem-authoring-hybrideditors 프로젝트](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors). 전체 프로젝트를 다음으로 다운로드할 수 있습니다. [ZIP 아카이브](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors/archive/master.zip).

## 즉석 편집기 추가 {#add-an-in-place-editor}

즉석 편집기 추가에 대한 일반적인 내용은 문서를 참조하십시오 [페이지 작성 사용자 지정](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor).

>[!MORELIKETHIS]
>
>* [Experience Manager에서 리치 텍스트 편집기 구성](/help/sites-administering/rich-text-editor.md).
