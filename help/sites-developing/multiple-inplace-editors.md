---
title: 여러 즉석 편집기 구성
seo-title: 여러 즉석 편집기 구성
description: 여러 즉석 편집기가 있도록 구성 요소를 구성할 수 있습니다
seo-description: 여러 즉석 편집기가 있도록 구성 요소를 구성할 수 있습니다
uuid: 4abbfcd5-fe1b-4c02-b115-97db20e60e1e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 0fac1e4a-f08f-4c46-b070-cb1d5a05b6e0
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71

---


# 여러 즉석 편집기 구성{#configuring-multiple-in-place-editors}

터치 지원 UI 내에 여러 명의 즉석 편집기가 있도록 구성 요소를 구성할 수 있습니다.

구성되면 적절한 컨텐츠를 선택하고 적절한 편집기를 열 수 있습니다. 예:

![chlimage_1-8](assets/chlimage_1-8a.png)

## 여러 편집기 구성 {#configuring-multiple-editors}

여러 즉석 편집기를 사용하기 위해 노드 유형의 구조가 `cq:InplaceEditingConfig` `cq:ChildEditorConfig` 노드 유형의 정의로 개선되었습니다.

예:

```
   /**
       * Configures inplace editing of a component.
       *
       * @prop active true to activate inplace editing for the component
       * @prop editorType ID of inplace editor to use
       * @prop cq:childEditors collection of {@link cq:ChildEditorConfig} nodes.
       * @prop configPath path to editor's config (optional)
       * @node config editor's config (used if no configPath is specified; optional)
     */
    [cq:InplaceEditingConfig] > nt:unstructured
      - active (boolean)
      - editorType (string)
      + cq:childEditors (nt:base) = nt:unstructured
      - configPath (string)
      + config (nt:unstructured) = nt:unstructured

    /**
      * Configures one child editor for a subcomponent. The name of the this node will
      * be used as DD id.
      *
      * @prop type type of the inline editor. eg: ["image"]
      * @prop title totle od the inline editor
      * @prop icon icon to represent the inline editor
    */
    [cq:ChildEditorConfig] > nt:unstructured
      orderable
      - type (string)
      - title (string)
```

여러 편집기를 구성하려면:

1. 노드에서 `cq:inplaceEditing` (유형 `cq:InplaceEditingConfig`) 속성을 정의합니다.

   * 이름:`editorType`
   * 유형: `String`
   * 값: `hybrid`

1. 이 노드에서 새 노드를 만듭니다.

   * 이름: `cq:ChildEditors`
   * 유형: `nt:unstructured`

1. 노드 아래에서 `cq:childEditors` 각 즉석 편집기에 대해 새 노드를 만듭니다.

   * 이름:각 노드의 이름은 해당 노드가 나타내는 속성의 이름이어야 합니다(드롭 대상의 경우와 마찬가지로). 예, `image`, `text`.
   * 유형:cq: `ChildEditorConfig`
   >[!NOTE]
   >
   >정의된 드롭 대상과 하위 편집기 간에는 상관 관계가 있습니다. 노드의 이름은 `cq:ChildEditorConfig` 드롭 대상 ID로 간주되어 선택한 하위 편집기의 매개 변수로 사용됩니다. 편집 가능한 하위 영역에 드롭 대상(예: 텍스트 구성 요소와 같은)이 없는 경우 하위 편집기의 이름은 여전히 해당 편집 가능 영역을 식별하는 ID로 간주됩니다.

1. 이러한 각 노드( `cq:ChildEditorConfig`)에서 속성을 정의합니다.

   * 이름: `type`
   * 값:등록된 즉석 편집기의 이름;예를 들어, `image``text`

   * 이름: `title`
   * 값:구성 요소 선택 목록(사용 가능한 편집기)에 표시할 제목;예를 들어, `Image``Text`

### 리치 텍스트 편집기를 위한 추가 구성 {#additional-configuration-for-rich-text-editors}

각 개별 RTE 인스턴스를 개별적으로 구성할 수 있으므로 여러 리치 텍스트 편집기의 구성은 약간 다릅니다.

>[!NOTE]
>
>자세한 내용은 리치 텍스트 [편집기 구성을 참조하십시오](/help/sites-administering/rich-text-editor.md).

여러 RTE를 사용하려면 각 즉석 RTE에 대한 구성이 필요합니다.

* Under `cq:InplaceEditingConfig` define a `config` node.

   * 노드 아래에서 `config` 개별 RTE 구성을 정의합니다.

```xml
    texttext
        cq:dialog
        cq:editConfig
            cq:inplaceEditing
                cq:childEditors
                    config
                        text1
                            rtePlugins
                        text2
                            rtePlugins
```

>[!NOTE]
>
>각 개별 RTE에 다른 구성이 있을 수 `config` `cq:InplaceEditingConfig` 있으므로 노드를 정의하는 것이 좋습니다.
>
>그러나 RTE의 경우, 구성 요소에 텍스트 편집기(편집 가능한 하위 영역)의 인스턴스가 하나만 있을 때 `configPath` 속성이 지원됩니다. 이 사용은 구성 요소의 이전 UI 대화 상자와 이전 버전과의 호환성을 지원하기 위해 `configPath` 제공됩니다.

## 코드 샘플 {#code-samples}

**GITHUB에 대한 코드**

GitHub에서 이 페이지의 코드를 찾을 수 있습니다

* [GitHub에서 aem-authoring-hybrideditors 프로젝트 열기](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors)
* 프로젝트를 ZIP [파일로 다운로드](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors/archive/master.zip)

## 즉석 편집기 추가 {#adding-an-in-place-editor}

즉석 편집기 추가에 대한 일반 정보는 페이지 작성 사용자 [지정을 참조하십시오](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor).
