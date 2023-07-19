---
title: 리치 텍스트 편집기를 구성하여 액세스 가능한 웹 페이지 및 사이트를 만듭니다.
description: 리치 텍스트 편집기를 구성하여 액세스 가능한 웹 페이지 및 사이트를 만듭니다.
contentOwner: AG
exl-id: d2451710-5abf-4816-8052-57d8f04a228e
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 0%

---

# 액세스 가능한 웹 페이지 및 사이트를 생성하도록 RTE 구성 {#configure-rte-for-accessibility}

Adobe Experience Manager은 다양한 접근성 표준에 따라 많은 표준 접근성 기능을 지원합니다. 또한 개발자는 리치 텍스트 편집기(RTE)를 사용하는 Experience Manager 구성 요소를 사용하여 액세스 가능한 컨텐츠를 만드는 데 도움이 되는 기능을 제공하도록 사용자 정의하거나 확장할 수 있습니다.

웹 페이지를 디자인하고 페이지에 컨텐츠를 추가할 때 컨텐츠 개발자와 작성자는 RTE의 기능을 사용하여 접근성 관련 정보를 제공할 수 있습니다. 예를 들어 제목 및 단락 요소를 통해 구조 정보를 추가합니다.

이러한 기능을 구성하고 사용자 정의하려면 [rte 플러그인 구성](#configure-the-plugin-features) 구성 요소에 사용됩니다. 예를 들어 `paraformat` 플러그인을 사용하면 기본 이상으로 지원되는 제목 수준의 수를 확장하는 것을 포함하여 블록 수준 의미 요소를 추가할 수 있습니다 `H1`, `H2`, 및 `H3` 기본적으로 제공됩니다.

RTE는 터치 지원 사용자 인터페이스 및 클래식 사용자 인터페이스를 위한 다양한 구성 요소에서 사용할 수 있습니다. 그러나 RTE를 사용할 주요 구성 요소는 다음과 같습니다. **텍스트** 두 인터페이스에 모두 사용할 수 있는 구성 요소입니다. 다음 이미지는 다양한 플러그인이 활성화된 RTE를 보여 줍니다. `paraformat`:

![터치 지원 UI에서 전체 화면 모드의 텍스트 구성 요소(RTE).](assets/chlimage_1-206.png)

*그림: 터치 사용 사용자 인터페이스의 텍스트 구성 요소*

![클래식 UI에서 텍스트 구성 요소의 편집 대화 상자(RTE).](assets/chlimage_1-207.png)

*그림: 클래식 사용자 인터페이스의 텍스트 구성 요소*

다양한 인터페이스에서 사용할 수 있는 RTE 기능의 차이점을 알아보려면 다음을 참조하십시오. [플러그인 및 해당 기능](/help/sites-administering/rich-text-editor.md#aboutplugins).

## 플러그인 기능 구성 {#configure-the-plugin-features}

RTE 구성에 대한 전체 지침은 [리치 텍스트 편집기 구성](/help/sites-administering/rich-text-editor.md) 페이지를 가리키도록 업데이트하는 중입니다. 주요 단계를 포함하여 모든 문제를 다룹니다.

* [플러그인 및 기능](/help/sites-administering/rich-text-editor.md#aboutplugins).
* [구성 위치](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations).
* [플러그인 활성화 및 기능 속성 구성](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
* [RTE의 다른 기능 구성](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).

적절한 내에서 플러그인을 구성하여 `rtePlugins` CRXDE Lite의 하위 분기에서 해당 플러그인에 대한 모든 기능 또는 특정 기능을 활성화할 수 있습니다.

![rtePlugin 예를 보여 주는 CRXDE Lite.](assets/chlimage_1-208.png)

### 예 - RTE 선택 필드에서 사용할 수 있는 단락 형식 지정 {#example-specifying-paragraph-formats-available-in-rte-selection-field}

다음 방법으로 새로운 의미 체계 블록 형식을 선택할 수 있습니다.

1. RTE에 따라 을(를) 결정하고 다음으로 이동합니다. [구성 위치](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations).
1. [단락 선택 필드 활성화](/help/sites-administering/rich-text-editor.md); 기준 [플러그인 활성화](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
1. [단락 선택 필드에서 사용할 형식을 지정합니다](/help/sites-administering/rich-text-editor.md).
1. 그런 다음 콘텐츠 작성자는 RTE의 선택 필드에서 단락 형식을 사용할 수 있습니다. 다음 방법으로 액세스할 수 있습니다.

   * 터치 지원 UI에서 단락 필크로 아이콘을 사용합니다.
   * 사용 **형식** 클래식 UI의 필드(팝업 선택기).

AEM은 단락 형식 옵션을 통해 RTE에서 사용할 수 있는 구조적 요소를 통해 액세스 가능한 컨텐츠를 개발할 수 있는 좋은 기반을 제공합니다. 콘텐츠 작성자는 RTE를 사용하여 글꼴 크기나 색상 또는 기타 관련 특성의 서식을 지정할 수 없으므로 인라인 서식이 생성되지 않습니다. 대신 제목과 같은 적절한 구조적 요소를 선택하고 스타일 옵션에서 선택한 전역 스타일을 사용해야 합니다. 따라서 사용자가 스타일 시트와 올바르게 구조화된 콘텐츠를 검색할 수 있도록 깔끔한 마크업과 더 많은 옵션을 제공합니다.

## 소스 편집 기능 사용 {#use-of-the-source-edit-feature}

경우에 따라 콘텐츠 작성자는 RTE를 사용하여 만든 HTML 소스 코드를 검사하고 조정할 필요가 있습니다. 예를 들어 RTE 내에서 만들어진 콘텐츠의 한 부분은 WCAG 2.0을 준수하기 위해 추가 마크업이 필요할 수 있습니다. 다음을 사용하여 이 작업을 수행할 수 있습니다. [소스 편집](/help/sites-administering/rich-text-editor.md#aboutplugins) RTE 옵션 다음을 지정할 수 있습니다. [`sourceedit` 의 기능 `misctools` 플러그인](/help/sites-administering/rich-text-editor.md#aboutplugins).

>[!CAUTION]
>
>사용 `sourceedit` 자세히 살펴보십시오. 입력 오류 및/또는 지원되지 않는 기능으로 인해 더 많은 문제가 발생할 수 있습니다.

## 더 많은 HTML 요소 및 속성에 대한 지원 추가 {#add-support-for-more-html-elements-and-attributes}

AEM의 접근성 기능을 추가로 확장하기 위해 RTE를 기반으로 기존 구성 요소를 확장할 수 있습니다(예: **텍스트** 및 **표** 구성 요소)를 참조하십시오.

다음 절차에서는 를 확장하는 방법을 보여 줍니다 **표** 가 있는 구성 요소 **캡션** 보조 기술 사용자에게 데이터 테이블에 대한 정보를 제공하는 요소입니다.

### 예 - 표 속성 대화 상자에 캡션 추가 {#example-adding-the-caption-to-the-table-properties-dialog}

의 생성자에서 `TablePropertiesDialog`캡션 편집에 사용되는 추가 텍스트 입력 필드를 추가합니다. 참고: `itemId` 은(는) 로 설정되어야 합니다. `caption` (즉, DOM 속성 이름) 을 사용하여 콘텐츠를 자동으로 처리할 수 있습니다.

위치 **표**, 를 명시적으로 설정하거나 DOM 요소에서 속성을 제거합니다. 값이 의 대화 상자에 의해 전달됩니다. `config` 개체. DOM 속성은 다음을 사용하여 설정/제거해야 합니다 `CQ.form.rte.Common` 메서드 ( `com` 은(는) 의 단축키입니다. `CQ.form.rte.Common`)를 클릭하여 브라우저 구현에 일반적인 위험을 방지합니다.

>[!NOTE]
>
>이 절차는 Classic 사용자 인터페이스에만 적합합니다.

### 예제 - 텍스트에서 강조를 사용할 때 액세스 가능한 HTML 만들기 {#create-accessible-html-for-text}

RTE는 `strong` 및 `em` 태그 대신 `b` 및 `i`. 다음 노드를 의 형제 노드로 추가 `uiSettings` 및 `rtePlugins` 대화 상자의 노드.

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

1. CRXDE Lite 시작. 예: [http://localhost:4502/crx/de/](http://localhost:4502/crx/de/)
1. 복사:

   `/libs/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`

   끝:

   `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`

   >[!NOTE]
   >
   >중간 폴더가 아직 없는 경우 중간 폴더를 만들어야 합니다.

1. 복사:

   `/libs/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

   끝:

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`.

1. 편집할 다음 파일을 엽니다(두 번 클릭하여 열기).

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

1. 다음에서 `constructor` 메서드, 줄 읽기 전:

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

1. 의 끝에 다음 코드를 추가합니다. `transferConfigToTable` 방법:

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

1. 다음을 사용하여 변경 사항 저장 **모두 저장...**

>[!NOTE]
>
>일반 텍스트 필드만이 캡션 요소 값에 허용되는 입력 유형이 아닙니다. 를 통해 캡션의 값을 제공하는 모든 ExtJS 위젯을 사용할 수 있습니다 `getValue()` 메서드를 사용합니다.
>
>추가 요소 및 속성에 대한 편집 기능을 추가하려면 다음 사항을 모두 확인합니다.
>
>* 다음 `itemId` 각 해당 필드의 속성은 적절한 DOM 속성의 이름( )으로 설정됩니다.`TablePropertiesDialog`).
>* 속성은 DOM 요소에서 명시적으로 설정 및/또는 제거됩니다(`Table`).

>[!MORELIKETHIS]
>
>* [WCAG 2.0에 대한 빠른 안내서](/help/managing/qg-wcag.md)
>* [액세스 가능한 컨텐츠 만들기(WCAG 2.0 적합성)](/help/sites-authoring/creating-accessible-content.md)
