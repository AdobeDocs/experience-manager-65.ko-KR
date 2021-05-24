---
title: 액세스 가능한 웹 페이지 및 사이트를 생성하도록 리치 텍스트 편집기를 구성합니다.
description: 액세스 가능한 웹 페이지 및 사이트를 생성하도록 리치 텍스트 편집기를 구성합니다.
contentOwner: AG
exl-id: d2451710-5abf-4816-8052-57d8f04a228e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---

# 액세스 가능한 웹 페이지 및 사이트 {#configure-rte-for-accessibility}를 만들도록 RTE를 구성합니다

Adobe Experience Manager은 다양한 접근성 표준에 따라 표준 접근성 기능을 지원합니다. 또한 개발자는 RTE(리치 텍스트 편집기)를 사용하는 Experience Manager 구성 요소를 사용하여 액세스 가능한 컨텐츠를 만드는 데 도움이 되는 기능을 사용자 정의하거나 확장하여 제공할 수 있습니다.

웹 페이지를 디자인하고 페이지에 컨텐츠를 추가할 때 컨텐츠 개발자와 작성자는 RTE의 기능을 사용하여 접근성 관련 정보를 제공할 수 있습니다. 예를 들어, 제목 및 단락 요소를 통해 구조적 정보를 추가합니다.

이러한 기능을 구성하고 사용자 지정하려면 [구성 요소에 대해 RTE 플러그인](#configure-the-plugin-features)을 구성합니다. 예를 들어 `paraformat` 플러그인을 사용하면 기본 `H1`, `H2` 및 기본적으로 제공되는 `H3` 이상으로 지원되는 제목 수준 수를 확장하는 등 블록 수준 의미 요소를 추가할 수 있습니다.

RTE는 터치 지원 사용자 인터페이스 및 클래식 사용자 인터페이스에 대한 다양한 구성 요소에서 사용할 수 있습니다. 그러나 RTE를 사용하는 기본 구성 요소는 두 인터페이스 모두에서 사용할 수 있는 **Text** 구성 요소입니다. 다음 이미지는 `paraformat` 을 포함하여 플러그인 범위가 활성화된 RTE를 보여줍니다.

![터치 지원 UI의 전체 화면 모드의 텍스트 구성 요소(RTE)입니다.](assets/chlimage_1-206.png)

*그림:터치 지원 사용자 인터페이스의 텍스트 구성 요소입니다.*

![클래식 UI에 있는 텍스트 구성 요소의 편집 대화 상자(RTE)](assets/chlimage_1-207.png)

*그림:클래식 사용자 인터페이스의 텍스트 구성 요소입니다.*

다양한 인터페이스에서 사용할 수 있는 RTE 기능 간의 차이점은 [플러그인 및 해당 기능](/help/sites-administering/rich-text-editor.md#aboutplugins)을 참조하십시오.

## 플러그인 기능 {#configure-the-plugin-features} 구성

RTE를 구성하는 전체 지침은 [리치 텍스트 편집기 구성](/help/sites-administering/rich-text-editor.md) 페이지를 참조하십시오. 여기서는 주요 단계를 포함한 모든 문제를 다룹니다.

* [플러그인 및 기능](/help/sites-administering/rich-text-editor.md#aboutplugins).
* [구성 위치](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations).
* [플러그인을 활성화하고 기능 속성을 구성합니다](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
* [RTE의 다른 기능 구성](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).

CRXDE Lite의 적절한 `rtePlugins` 하위 분기 내에 플러그인을 구성하면 해당 플러그인에 대한 모든 또는 특정 기능을 활성화할 수 있습니다.

![rtePlugin 예를 보여주는 CRXDE Lite.](assets/chlimage_1-208.png)

### 예 - RTE 선택 필드 {#example-specifying-paragraph-formats-available-in-rte-selection-field}에서 사용할 수 있는 단락 형식을 지정합니다

다음 방법으로 선택할 수 있는 새로운 시맨틱 블록 포맷이 제공될 수 있습니다.

1. RTE에 따라 [구성 위치](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations)를 결정하고 이동합니다.
1. [단락 선택 필드를 활성화합니다](/help/sites-administering/rich-text-editor.md).플러그인 [을 활성화하여 ](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
1. [단락 선택 필드에서 사용할 수 있는 형식을 지정합니다](/help/sites-administering/rich-text-editor.md).
1. 그런 다음 RTE의 선택 필드에서 컨텐츠 작성자가 단락 형식을 사용할 수 있습니다. 액세스 가능한 항목은 다음과 같습니다.

   * 터치 지원 UI에서 단락 줄바꿈 아이콘 사용.
   * 클래식 UI에서 **형식** 필드(팝업 선택기) 사용.

AEM에서는 단락 형식 옵션을 통해 RTE에서 구조적 요소를 사용할 수 있으므로 액세스 가능한 컨텐츠를 개발할 수 있는 좋은 기반을 제공합니다. 컨텐츠 작성자는 RTE를 사용하여 글꼴 크기 또는 색상 또는 기타 관련 속성의 서식을 지정할 수 없으므로 인라인 서식이 생성되지 않습니다. 대신 제목 등의 적절한 구조적 요소를 선택하고 스타일 옵션에서 선택한 전역 스타일을 사용해야 합니다. 이렇게 하면 고유한 스타일 시트와 올바르게 구조화된 컨텐츠를 찾아보는 사용자에게 더 나은 옵션과 깨끗한 마크업이 보장됩니다.

## 소스 편집 기능 {#use-of-the-source-edit-feature} 사용

경우에 따라 컨텐츠 작성자는 RTE를 사용하여 만든 HTML 소스 코드를 검사하고 조정해야 합니다. 예를 들어 RTE 내에서 만들어진 컨텐츠는 WCAG 2.0을 준수하도록 추가 마크업이 필요할 수 있습니다. 이 작업은 RTE의 [소스 편집](/help/sites-administering/rich-text-editor.md#aboutplugins) 옵션을 사용하여 수행할 수 있습니다. `misctools` 플러그인](/help/sites-administering/rich-text-editor.md#aboutplugins)에 [ `sourceedit` 기능을 지정할 수 있습니다.

>[!CAUTION]
>
>`sourceedit` 기능을 신중하게 사용하십시오. 입력 오류 및/또는 지원되지 않는 기능을 사용하면 더 많은 문제가 발생할 수 있습니다.

## 추가 HTML 요소 및 특성 지원 추가 {#add-support-for-more-html-elements-and-attributes}

AEM의 액세스 가능성 기능을 추가로 확장하기 위해 RTE(예: **텍스트** 및 **표** 구성 요소)를 기반으로 추가 요소 및 특성을 사용하여 기존 구성 요소를 확장할 수 있습니다.

다음 절차는 보조 기술 사용자에게 데이터 테이블에 대한 정보를 제공하는 **Caption** 요소로 **Table** 구성 요소를 확장하는 방법을 보여 줍니다.

### 예 - 표 속성 대화 상자에 캡션 추가 {#example-adding-the-caption-to-the-table-properties-dialog}

`TablePropertiesDialog` 생성자에서 캡션을 편집하는 데 사용되는 추가 텍스트 입력 필드를 추가합니다. 해당 컨텐츠를 자동으로 처리하려면 `itemId`을 `caption`(즉, DOM 속성의 이름)로 설정해야 합니다.

**Table**&#x200B;에서 속성을 DOM 요소로 명시적으로 설정하거나 제거합니다. 이 값은 `config` 개체의 대화 상자에 의해 전달됩니다. DOM 속성은 해당 `CQ.form.rte.Common` 메서드를 사용하여 설정/제거해야 합니다( `com` 는 `CQ.form.rte.Common` 의 바로 가기 임).

>[!NOTE]
>
>이 절차는 Classic 사용자 인터페이스에만 적합합니다.

### 예 - 텍스트 {#create-accessible-html-for-text}에 강조를 사용할 때 액세스 가능한 HTML을 만드십시오

RTE는 `b` 및 `i` 대신 `strong` 및 `em` 태그를 사용할 수 있습니다. 다음 노드를 대화 상자의 `uiSettings` 및 `rtePlugins` 노드에 동위 노드로 추가합니다.

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

1. CRXDE Lite 시작. 예:[http://localhost:4502/crx/de/](http://localhost:4502/crx/de/)
1. 복사:

   `/libs/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`

   끝:

   `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`

   >[!NOTE]
   >
   >중간 폴더가 없는 경우 중간 폴더를 만들어야 할 수도 있습니다.

1. 복사:

   `/libs/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

   끝:

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`.

1. 편집할 다음 파일을 엽니다(두 번 클릭하여 열기).

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

1. `constructor` 메서드에서 다음 줄 읽기 전에:

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

1. `transferConfigToTable` 메서드 끝에 다음 코드를 추가합니다.

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

1. **모두 저장..**&#x200B;을 사용하여 변경 내용을 저장합니다.

>[!NOTE]
>
>일반 텍스트 필드만 캡션 요소의 값에 대해 허용되는 입력 유형은 아닙니다. `getValue()` 메서드를 통해 캡션의 값을 제공하는 ExtJS 위젯을 사용할 수 있습니다.
>
>추가 요소 및 속성에 대한 편집 기능을 추가하려면 다음을 모두 확인합니다.
>
>* 각 해당 필드에 대한 `itemId` 속성은 적절한 DOM 속성(`TablePropertiesDialog`)의 이름으로 설정됩니다.
>* 특성이 명시적으로 DOM 요소에서 설정 및/또는 제거됩니다(`Table`).


>[!MORELIKETHIS]
>
>* [WCAG 2.0에 대한 빠른 안내서](/help/managing/qg-wcag.md)
* [액세스 가능한 컨텐츠 만들기(WCAG 2.0 적합성)](/help/sites-authoring/creating-accessible-content.md)

