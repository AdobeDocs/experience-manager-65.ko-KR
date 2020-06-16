---
title: 액세스 가능한 웹 페이지 및 사이트를 만들려면 리치 텍스트 편집기를 구성합니다.
description: 액세스 가능한 웹 페이지 및 사이트를 만들려면 리치 텍스트 편집기를 구성합니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: df992fc0204519509c4662a7d4315939af2fc92c
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---


# 액세스 가능한 웹 페이지 및 사이트를 만들도록 RTE 구성 {#configure-rte-for-accessibility}

Adobe Experience Manager은 다양한 액세서빌러티 표준에 따라 인간의 표준 액세서빌러티 기능을 지원합니다. 또한 개발자는 RTE(Rich Text Editor)를 사용하는 Experience Manager 구성 요소를 사용하여 액세스 가능한 컨텐츠를 제작하는 데 도움이 되는 기능을 사용자 정의하거나 확장할 수 있습니다.

웹 페이지를 디자인하고 페이지에 컨텐츠를 추가할 때 컨텐츠 개발자와 작성자는 RTE의 기능을 사용하여 접근성 관련 정보를 제공할 수 있습니다. 예를 들어 머리글과 단락 요소를 통해 구조적 정보를 추가합니다.

이러한 기능을 구성하고 사용자 정의하려면 구성 요소에 [대한 RTE 플러그인을](#configure-the-plugin-features) 구성합니다. 예를 들어, 이 `paraformat` 플러그인을 사용하면 기본, 기본 제공 외에 지원되는 머리글 수준 `H1`의 수를 확장하는 등 추가적인 블록 수준 의미 요소 `H2``H3` 를 추가할 수 있습니다.

RTE는 터치 지원 사용자 인터페이스 및 클래식 사용자 인터페이스에 대한 다양한 구성 요소에서 사용할 수 있습니다. 그러나 RTE를 사용하는 기본 구성 요소는 두 인터페이스 모두에서 사용할 수 있는 **텍스트** 구성 요소입니다. 다음 이미지는 다음을 포함하여 다양한 플러그인이 활성화된 RTE를 보여 줍니다. `paraformat`:

![터치 지원 UI의 전체 화면 모드에서 텍스트 구성 요소(RTE).](assets/chlimage_1-206.png)

*그림: 터치 지원 사용자 인터페이스의 텍스트 구성 요소입니다.*

![클래식 UI에서 텍스트 구성 요소의 편집 대화 상자(RTE)를 참조하십시오.](assets/chlimage_1-207.png)

*그림: 클래식 사용자 인터페이스의 텍스트 구성 요소입니다.*

다양한 인터페이스에서 사용할 수 있는 RTE 기능 간의 차이점은 [Plugins 및 해당 기능을 참조하십시오](/help/sites-administering/rich-text-editor.md#aboutplugins).

## 플러그인 기능 구성 {#configure-the-plugin-features}

RTE 구성에 대한 전체 지침은 리치 텍스트 편집기 [페이지 구성을 참조하십시오](/help/sites-administering/rich-text-editor.md) . 여기에는 주요 단계를 비롯한 모든 문제가 포함됩니다.

* [Plugins and the features](/help/sites-administering/rich-text-editor.md#aboutplugins).
* [구성 위치](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations).
* [플러그인을 활성화하고 기능 속성을 구성합니다](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
* [RTE의 다른 기능을 구성합니다](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).

CRXDE Lite의 해당 하위 `rtePlugins` 분기 내에 플러그인을 구성하면 해당 플러그인에 대한 모든 또는 특정 기능을 활성화할 수 있습니다.

![rtePlugin 예를 보여주는 CRXDE Lite.](assets/chlimage_1-208.png)

### 예 - RTE 선택 필드에서 사용할 수 있는 단락 서식 지정 {#example-specifying-paragraph-formats-available-in-rte-selection-field}

다음 방법을 통해 선택할 수 있는 새로운 의미 체계 블록 형식을 만들 수 있습니다.

1. RTE에 따라 [구성 위치를 확인하고 탐색합니다](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations).
1. [단락 선택 필드를 활성화합니다](/help/sites-administering/rich-text-editor.md). 플러그인을 [활성화함으로써](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
1. [단락 선택 필드에서 사용할 형식을 지정합니다](/help/sites-administering/rich-text-editor.md).
1. 그런 다음 RTE의 선택 필드에서 컨텐츠 작성자가 단락 포맷을 사용할 수 있습니다. 액세스 가능한 항목:

   * 터치 가능 UI에서 단락 패턴 아이콘 사용
   * 클래식 UI에서 **형식** 필드(팝업 선택기) 사용

AEM에서는 단락 형식 옵션을 통해 RTE에서 구조적 요소를 사용할 수 있으므로 액세스 가능한 컨텐츠를 개발할 수 있는 적절한 기반을 제공합니다. 컨텐츠 작성자는 RTE를 사용하여 글꼴 크기 또는 색상 또는 기타 관련 속성의 서식을 지정할 수 없으므로 인라인 서식을 만들 수 없습니다. 대신 머리글과 같은 적절한 구조 요소를 선택하고 스타일 옵션에서 선택한 전역 스타일을 사용해야 합니다. 이렇게 하면 자신만의 스타일 시트와 올바르게 구조화된 컨텐츠로 찾아보는 사용자에게 보다 향상된 마크업 기능과 깔끔한 마크업이 보장됩니다.

## 소스 편집 기능 사용 {#use-of-the-source-edit-feature}

경우에 따라 컨텐츠 작성자는 RTE를 사용하여 만든 HTML 소스 코드를 검토하고 조정할 필요가 있습니다. 예를 들어 RTE 내에서 만들어진 컨텐츠는 WCAG 2.0을 준수하기 위해 추가 마크업을 필요로 할 수 있습니다. 이 작업은 RTE의 [소스 편집](/help/sites-administering/rich-text-editor.md#aboutplugins) 옵션을 사용하여 수행할 수 있습니다. 플러그인에서 [ 기능을 `sourceedit` 지정할 수 `misctools` 있습니다](/help/sites-administering/rich-text-editor.md#aboutplugins).

>[!CAUTION]
>
>이 기능을 `sourceedit` 주의해서 사용하십시오. 입력 오류 및/또는 지원되지 않는 기능을 사용하면 더 많은 문제가 발생할 수 있습니다.

## 추가 HTML 요소 및 속성 지원 {#add-support-for-more-html-elements-and-attributes}

AEM의 액세서빌러티 기능을 추가로 확장하려면 추가 요소 및 특성을 사용하여 RTE( **텍스트** 및 **표** 구성 요소 등)를 기반으로 기존 구성 요소를 확장할 수 있습니다.

다음 절차에서는 보조 기술 사용자에게 데이터 테이블에 대한 정보를 제공하는 **캡션** **** 요소를 사용하여 표 구성 요소를 확장하는 방법을 보여 줍니다.

### 예 - 표 속성 대화 상자에 캡션 추가 {#example-adding-the-caption-to-the-table-properties-dialog}

의 생성자에서 캡션 편집에 사용되는 추가 텍스트 입력 필드 `TablePropertiesDialog`를 추가합니다. 컨텐츠를 자동으로 처리하려면 DOM 속성 이름 `itemId` (예: DOM 속성 이름)으로 설정해야 `caption` 합니다.

표 **에서** DOM 요소의 속성을 명시적으로 설정하거나 제거합니다. 이 값은 `config` 개체의 대화 상자로 전달됩니다. DOM 속성은 해당 `CQ.form.rte.Common` 방법(바로 가기)을 사용하여 설정/제거해야 브라우저 구현의 일반적인 문제 `com` 를 방지할 수 `CQ.form.rte.Common`있습니다.

>[!NOTE]
>
>이 절차는 클래식 사용자 인터페이스에만 적합합니다.

### 예 - 텍스트에 강조 표시 사용 시 액세스 가능한 HTML 만들기 {#create-accessible-html-for-text}

RTE는 `strong` 및 `em` 태그 대신 `b` 및 태그를 사용할 수 `i`있습니다. 다음 노드를 대화 상자의 노드 및 `uiSettings` 노드에 동위 `rtePlugins` 로 추가합니다.

```HTML
<htmlRules jcr:primaryType="nt:unstructured">
    <docType jcr:primaryType="nt:unstructured">
        <typeConfig jcr:primaryType="nt:unstructured"
                useSemanticMarkup="{Boolean}true">
            <semanticMarkupMap
                    b="strong"
                    i="em"/>
        </typeConfig>
    </docType>
</htmlRules>
```

### 단계별 지침 {#step-by-step-instructions}

1. CRXDE Lite를 시작합니다. 예: [http://localhost:4502/crx/de/](http://localhost:4502/crx/de/)
1. 복사:

   `/libs/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`

   끝:

   `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`

   >[!NOTE]
   >
   >중간 폴더가 아직 없는 경우 폴더를 만들어야 할 수도 있습니다.

1. 복사:

   `/libs/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

   끝:

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`.

1. 편집할 다음 파일을 엽니다(두 번 클릭하여 열기).

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

1. 메서드, 줄 읽기 `constructor` 전:

   ```
   var dialogRef = this;
   ```

   다음 코드를 추가합니다.

   ```
   editItems.push({
       "itemId": "caption",
       "name": "caption",
       "xtype": "textfield",
       "fieldLabel": CQ.I18n.getMessage("Caption"),
       "value": (this.table && this.table.caption ? this.table.caption.textContent : "")
   });
   ```

1. 다음 파일을 엽니다.

   `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`.

1. 메서드 끝에 다음 코드를 `transferConfigToTable` 추가합니다.

   ```
   /**
    * Adds Caption Element
   */
   var captionElement;
   if (dom.firstChild && dom.firstChild.tagName.toLowerCase() == "caption")
   {
      captionElement = dom.firstChild;
   }
   if (config.caption)
   {
       var captionTextNode = document.createTextNode(config.caption)
       if (captionElement)
       {
          dom.replaceNode(captionElement.firstChild,captionTextNode);
       } else
       {
           captionElement = document.createElement("caption");
           captionElement.appendChild(captionTextNode);
           if (dom.childNodes.length>0)
           {
              dom.insertBefore(captionElement, dom.firstChild);
           } else
           {
              dom.appendChild(captionElement);
           }
       }
   } else if (captionElement)
   {
     dom.removeChild(captionElement);
   }
   ```

1. 모두 **저장...을 사용하여 변경 내용을 저장합니다.**

>[!NOTE]
>
>일반 텍스트 필드는 캡션 요소의 값에 대해 허용되는 입력 유형만 아닙니다. 해당 메서드를 통해 캡션의 값을 제공하는 ExtJS 위젯을 사용할 수 `getValue()` 있습니다.
>
>추가 요소 및 속성에 대한 편집 기능을 추가하려면 다음 두 가지 모두 확인합니다.
>
>* 각 해당 필드의 `itemId` 속성은 해당 DOM 속성(`TablePropertiesDialog`)의 이름으로 설정됩니다.
>* 속성이 명시적으로 DOM 요소에서 설정 및/또는 제거됩니다(`Table`).


>[!MORELIKETHIS]
>
>* [WCAG 2.0에 대한 빠른 안내서](/help/managing/qg-wcag.md)
>* [액세스 가능한 컨텐츠 만들기(WCAG 2.0 준수)](/help/sites-authoring/creating-accessible-content.md)

