---
title: 여러 즉석 편집기에 대한 RTE를 구성합니다.
description: 리치 텍스트 편집기를 구성하여 Adobe Experience Manager에서 여러 즉석 편집기를 만들 수 있습니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: e49411a99a80e91c983afc103a8ea826e75569b8
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 2%

---


# 여러 즉석 편집기 구성 {#configure-multiple-in-place-editors}

여러 개의 즉석 편집기가 있도록 Adobe Experience Manager에서 리치 텍스트 편집기를 구성할 수 있습니다. 구성 시 적절한 컨텐츠를 선택하고 적절한 편집기를 열 수 있습니다.

![특정 즉석 편집기](assets/rte-inplace-editor.png)

## 여러 편집기 구성 {#configure-multiple-editors}

여러 즉석 편집기를 사용하도록 하기 위해 `cq:InplaceEditingConfig` 노드 유형의 구조가 `cq:ChildEditorConfig` 노드 유형의 정의로 개선되었습니다.

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

여러 편집기를 구성하려면 다음 단계를 따르십시오.

1. 노드 `cq:inplaceEditing`(유형 `cq:InplaceEditingConfig`)에서 다음 속성을 정의합니다.

   * 이름:`editorType`
   * 유형: `String`
   * 값: `hybrid`

1. Under this node, create a node:

   * 이름: `cq:ChildEditors`
   * 유형: `nt:unstructured`

1. `cq:childEditors` 노드 아래에서 각 즉석 편집기에 대한 노드를 만듭니다.

   * 이름:각 노드의 이름은 드롭 대상의 경우와 마찬가지로 나타내는 속성의 이름입니다. 예: `image` 및 `text`.
   * 유형: `cq:ChildEditorConfig`

   >[!NOTE]
   >
   >정의된 드롭 대상과 하위 편집기 간에는 상관 관계가 있습니다. `cq:ChildEditorConfig` 노드의 이름은 드롭 대상 ID로 간주되므로 선택한 하위 편집기의 매개 변수로 사용됩니다. 편집 가능한 하위 영역에 드롭 대상이 없는 경우(예: 텍스트 구성 요소에서) 하위 편집기의 이름은 해당 편집 가능 영역을 식별하기 위한 ID로 계속 간주됩니다.

1. 이러한 각 노드(`cq:ChildEditorConfig`)에서 속성을 정의합니다.

   * 이름: `type`.
   * 값:등록된 즉석 편집기의 이름예: `image` 및 `text`.

   * 이름: `title`.
   * 값:사용 가능한 편집기의 구성 요소 선택 목록에 표시되는 제목입니다. 예: `Image` 및 `Text`.

### 리치 텍스트 편집기에 대한 추가 구성 {#additional-configuration-for-rich-text-editors}

각 개별 RTE 인스턴스를 개별적으로 구성할 수 있으므로 여러 리치 텍스트 편집기의 구성은 약간 다릅니다. 자세한 내용은 [리치 텍스트 편집기 구성](/help/sites-administering/rich-text-editor.md)을 참조하십시오. 여러 RTE를 만들려면 각 즉석 RTE에 대한 구성을 만듭니다. 각 개별 RTE의 구성이 다를 수 있으므로 Adobe은 `cq:InplaceEditingConfig` 아래에 새 구성 노드를 만드는 것이 좋습니다. 새 노드 아래에서 각 개별 RTE 구성을 만듭니다.

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
>그러나 RTE의 경우, 구성 요소에 텍스트 편집기(편집 가능한 하위 영역)의 인스턴스가 하나만 있는 경우 `configPath` 속성이 지원됩니다. 이러한 `configPath` 사용은 구성 요소의 이전 사용자 인터페이스 대화 상자와의 호환성을 지원하기 위해 제공됩니다.

>[!CAUTION]
>
>RTE 구성 노드의 이름을 `config`으로 지정하지 마십시오. 그렇지 않은 경우 RTE 구성은 관리자만 사용할 수 있고 그룹 `content-author`의 사용자는 사용할 수 없습니다.

## 코드 샘플 {#code-samples}

이 페이지의 코드는 GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors)에서 [aem-authoring-hybrideditors project에서 찾을 수 있습니다. 전체 프로젝트를 [ZIP 아카이브](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors/archive/master.zip)로 다운로드할 수 있습니다.

## 즉석 편집기 {#add-an-in-place-editor} 추가

즉석 편집기 추가에 대한 일반적인 내용은 [사용자 지정 페이지 작성](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor) 문서를 참조하십시오.

>[!MORELIKETHIS]
>
>* [Experience Manager에서 리치 텍스트 편집기를 구성합니다](/help/sites-administering/rich-text-editor.md).

