---
title: CIF 제품 및 카테고리 선택기 사용
description: 고객 상거래 구성 요소에서 CIF 제품 및 범주 선택기를 사용하여 작성자와 마케터가 상거래 제품 및 카탈로그 데이터를 효율적으로 사용할 수 있도록 지원하는 방법에 대해 알아봅니다.
sub-product: Commerce
topics: Development
version: Experience Manager as a Cloud Service
activity: develop
audience: developer
feature: Commerce Integration Framework
exl-id: 1e7c3748-92b5-45f1-8dd9-f1816e3e34aa
solution: Experience Manager,Commerce
role: Admin, Developer
source-git-commit: a45b09c52d780a954e606d4cae73a3a02a8a6aa4
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---

# AEM 컨텐츠 및 Commerce 작성 선택기 {#cif-pickers}

AEM 컨텐츠 및 Commerce 작성은 AEM 작성자 및 마케터가 상거래 제품 데이터 및 카탈로그를 효율적으로 작업하는 데 도움이 되는 작성 도구 세트를 제공합니다. 제품 선택기 및 카테고리 선택기는 CIF 추가 기능의 일부이며 CIF 핵심 구성 요소에서 사용됩니다. 프로젝트는 구성 요소 대화 상자에서 이러한 선택기를 사용하여 제품이나 범주를 선택할 수 있습니다.

## 제품 선택기 {#product-picker}

프로젝트 구성 요소에서 제품 선택기를 사용하려면 개발자가 구성 요소 대화 상자에 `commerce/gui/components/common/cifproductfield`을(를) 추가해야 합니다. 예를 들어 `cq:dialog`에 대해 다음을 사용합니다.

```xml
<product jcr:primaryType="nt:unstructured"
    sling:resourceType="commerce/gui/components/common/cifproductfield"
    fieldDescription="The product or product variant displayed by the teaser"
    fieldLabel="Select Product"
    filter="folderOrProductOrVariant"
    name="./selection"
    selectionId="sku"/>
```

제품 필드에서는 사용자가 다른 보기를 통해 선택하려는 제품을 탐색할 수 있습니다. 기본적으로 제품 필드는 제품의 ID를 반환하지만 `selectionId` 특성을 사용하여 구성할 수 있습니다.

제품 선택기 필드는 다음과 같은 선택적 속성을 지원합니다.

- selectionId(id, uid, sku, slug, combinedSlug, combinedSku) - 선택기에서 반환할 제품 속성을 선택할 수 있습니다(기본값 = id). sku를 사용하면 선택한 제품의 sku를 반환하고, combinedSku를 사용하면 기본 제품의 sku와 선택한 변형이 포함된 base#variant와 같은 문자열을 반환하거나 기본 제품이 선택된 경우 단일 sku를 반환합니다.
- filter (folderOrProduct, folderOrProductOrVariant) - 제품 트리를 탐색하는 동안 선택기에서 렌더링할 콘텐츠를 필터링합니다. folderOrProduct - 폴더 및 제품을 렌더링합니다. folderOrProductOrVariant - 폴더, 제품 및 제품 변형을 렌더링합니다. 제품 또는 제품 변형이 렌더링되면 선택기에서 선택할 수도 있습니다. (기본값 = folderOrProduct)
- 다중(true, false) - 하나 이상의 제품을 선택할 수 있습니다(기본값 = false).
- emptyText - 선택기 필드의 빈 텍스트 값을 구성합니다.

또한 `name`, `fieldLabel` 또는 `fieldDescription`과(와) 같은 표준 대화 상자 필드 속성도 지원됩니다.

>[!CAUTION]
>
>`cifproductfield` 구성 요소에는 `cif.shell.picker` clientlib이 필요합니다. 대화 상자에 clientlib을 추가하려면 extraClientlibs 속성을 사용합니다.
>[!CAUTION]
>
>CIF 핵심 구성 요소 버전 2.0.0부터 `id`에 대한 지원이 제거되고 `uid`(으)로 대체되었습니다. Adobe에서는 `sku` 또는 `slug`을(를) 제품 식별자로 사용하는 것이 좋습니다. Adobe은 CIF 핵심 구성 요소 버전 1.x를 사용하는 프로젝트에 대해서만 `id`을(를) 계속 지원합니다.

`cifproductfield`의 전체 작동 예는 [CIF 핵심 구성 요소](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/_cq_dialog/.content.xml) 프로젝트에서 찾을 수 있습니다. AEM 핵심 구성 요소 설명서의 [대화 상자 사용자 지정](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html#customizing-dialogs)도 참조하십시오.

## 범주 선택기 {#category-picker}

카테고리 선택기는 제품 선택기와 유사한 방식으로 구성 요소 대화 상자에서도 사용할 수 있습니다.

cq:dialog 구성에서 다음 코드 조각을 사용할 수 있습니다.

```xml
<category jcr:primaryType="nt:unstructured" 
    sling:resourceType="commerce/gui/components/common/cifcategoryfield" 
    fieldLabel="Category" 
    name="./categoryId" 
    selectionId="uid" />
```

카테고리 선택기 필드는 다음과 같은 옵션 속성을 지원합니다.

- selectionId(id, uid, slug, urlPath, idAndUrlPath _(더 이상 사용되지 않음)_, uidAndUrlPath _(더 이상 사용되지 않음)_) - 선택기에서 반환할 범주 특성을 선택할 수 있습니다(기본값 = id).
- 다중(true, false) - 하나 이상의 카테고리를 선택할 수 있습니다(기본값 = false).

또한 `name`, `fieldLabel` 또는 `fieldDescription`과(와) 같은 표준 대화 상자 필드 속성도 지원됩니다.

>[!CAUTION]
>
>`cifproductfield` 구성 요소와 마찬가지로 `cifcategoryfield` 구성 요소에도 `cif.shell.picker` clientlib이 필요합니다. 대화 상자에 clientlib을 추가하려면 `extraClientlibs` 속성을 사용합니다. AEM 핵심 구성 요소 설명서의 [대화 상자 사용자 지정](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html#customizing-dialogs)을 참조하십시오.
>[!CAUTION]
>
>CIF 핵심 구성 요소 버전 2.0.0부터 `id`에 대한 지원이 제거되고 `uid`(으)로 대체되었습니다. Adobe에서는 `uid` 또는 `urlPath`을(를) 범주 식별자로 사용하는 것이 좋습니다. Adobe은 CIF 핵심 구성 요소 버전 1.x를 사용하는 프로젝트에 대해서만 `id` 및 `idAndUrlPath`을(를) 계속 지원합니다.

`cifcategoryfield`의 전체 작동 예는 [CIF 핵심 구성 요소](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/featuredcategorylist/v1/featuredcategorylist/_cq_dialog/.content.xml) 프로젝트에서 찾을 수 있습니다.
