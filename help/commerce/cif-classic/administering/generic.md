---
title: 일반 전자 상거래 관리
description: AEM 일반 솔루션은 저장소 내에 있는 상거래 정보를 관리하는 방법을 제공합니다.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: c29f6213-1df6-45af-91c8-14b255276d82
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '2907'
ht-degree: 2%

---

# 일반 전자 상거래 관리 {#administering-generic-ecommerce}

Adobe Experience Manager(AEM) 일반 솔루션은 외부 전자 상거래 엔진을 사용하는 대신 저장소 내에 있는 상거래 정보를 관리하는 방법을 제공합니다. 여기에는 다음이 포함됩니다.

* [제품](/help/commerce/cif-classic/administering/concepts.md#products)
* [제품 변형](/help/commerce/cif-classic/administering/concepts.md#product-variants)
* [카탈로그](/help/commerce/cif-classic/administering/concepts.md#catalogs)
* [프로모션](/help/commerce/cif-classic/administering/concepts.md#promotions)
* [바우처](/help/commerce/cif-classic/administering/concepts.md#vouchers)
* [주문](/help/commerce/cif-classic/administering/concepts.md#shopping-cart-and-orders)
* [프록시 페이지](/help/commerce/cif-classic/administering/concepts.md#proxy-pages)

>[!NOTE]
>
>표준 AEM 설치에는 일반 AEM(JCR) eCommerce 구현이 포함됩니다.
>
>이는 데모 목적이거나 요구 사항에 따라 사용자 지정 구현을 위한 기본 토대입니다.

## 제품 및 제품 변형 {#products-and-product-variations}

>[!NOTE]
>
>다음 절차는 제품 및 제품 변형에 모두 적용됩니다.

제품을 만들기 전에 [scaffold](/help/sites-authoring/scaffolding.md)를 정의하십시오. 정의해야 하는 필드, 제품 및 편집 방법을 지정합니다.

각각의 개별 제품 유형에 대한 스캐폴드가 필요합니다. 적절한 스캐폴드는 다음 중 하나를 통해 제품과 연계됩니다.

* 경로
* 제품은 스캐폴드를 참조할 수 있습니다

>[!NOTE]
>
>Geometrixx-Outdoors 스토어에는 단일 제품 유형(따라서 단일 스캐폴드)이 있습니다.
>
>`/etc/scaffolding/geometrixx-outdoors`
>
>Geometrixx-Outdoors 제품 유형이 활성화된 위치:
>
>`/etc/commerce/products/geometrixx-outdoors`
>
>추가 설정 없이 그 아래 어디에서든 제품 정의를 생성할 수 있습니다.

### 제품 가져오기 {#importing-products}

#### 제품 가져오기 - 터치에 적합한 UI {#importing-products-touch-optimized-ui}

1. **Commerce**&#x200B;을(를) 통해 **제품** 콘솔로 이동합니다.
1. **제품** 콘솔을 사용하여 필요한 위치로 이동합니다.
1. **제품 가져오기** 아이콘을 사용하여 마법사를 엽니다.

   ![제품 가져오기 아이콘](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. 지정:

   * **가져오기**

     기본적으로 [상거래 공급자](/help/commerce/cif-classic/administering/concepts.md#commerce-providers)에 대한 가져오기는 `Geometrixx`입니다.

   * **소스**

     가져올 파일로, 브라우저를 사용하여 파일을 선택할 수 있습니다.

   * **증분 가져오기**

     증분 가져오기인지 여부를 나타냅니다(전체와 반대).

   >[!NOTE]
   >
   >(샘플 geometrixx-outdoor 가져오기의) 증분 가져오기는 제품 수준에서 작동합니다.
   >
   >필요에 따라 작동하도록 맞춤형 임포터를 정의할 수 있습니다.

1. **다음**&#x200B;을(를) 선택하여 제품을 가져오면 수행한 작업의 로그가 표시됩니다.

   >[!NOTE]
   >
   >제품을 현재 위치로 가져오거나 현재 위치에 대해 가져옵니다.

   >[!NOTE]
   >
   >**다음** 및 **뒤로**&#x200B;를 반복적으로 사용하면 제품 정의를 가져올 수 있습니다. 그러나 동일한 SKU를 포함하므로 저장소에 있는 정보를 덮어씁니다.

1. 마법사를 닫으려면 **완료**&#x200B;를 선택하십시오.

#### 제품 가져오기 - 클래식 UI {#importing-products-classic-ui}

1. **도구** 콘솔을 사용하여 **Commerce** 폴더를 엽니다.
1. **제품 가져오기**&#x200B;를 열려면 두 번 클릭하세요.

   ![제품 가져오기 콘솔](/help/sites-administering/assets/chlimage_1-22.jpeg)

1. 지정:

   * **저장소 이름**

     제품을 다음 위치로 가져옵니다.

     `/etc/commerce/products/<*store name*>/`

   * **Commerce 공급자**

     [상거래 공급자](/help/commerce/cif-classic/administering/concepts.md#commerce-providers)에 대한 가져오기(기본 Geometrixx).

   * **Source 파일**

     가져오려는 파일의 저장소 위치입니다.

   * **증분 가져오기**

     증분 가져오기인지 여부를 나타냅니다(전체와 반대).

1. **제품 가져오기**&#x200B;를 클릭합니다.

### 제품 정보 만들기 {#creating-product-information}

>[!NOTE]
>
>Geometrixx-Outdoors 제품 세트가 기본적으로 유지되므로 표준 제품 관리는 기본입니다. 복잡성은 제품 [스캐폴딩](/help/sites-authoring/scaffolding.md)을 기반으로 하므로 제품 스캐폴딩으로 보다 정교한 편집을 수행할 수 있습니다.

#### 제품 정보 만들기 - 터치에 적합한 UI {#creating-product-information-touch-optimized-ui}

1. **Commerce**&#x200B;을 통해 **제품** 콘솔을 사용하여 필요한 위치로 이동합니다.
1. 구조 및 위치에 따라 **만들기** 아이콘을 사용하여 다음 중 하나를 선택하십시오.

   * **제품 만들기**
   * **제품 변형 만들기**

   ![더하기 모양의 만들기 아이콘](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. 마법사가 열립니다. **기본** 및 **제품 탭**&#x200B;을 사용하여 새 제품 또는 제품 변형에 대한 [제품 특성](/help/commerce/cif-classic/administering/concepts.md#product-attributes)을(를) 입력하십시오.

   >[!NOTE]
   >
   >**Title** 및 **SKU**&#x200B;은(는) 제품이나 변형을 만드는 데 필요한 최소값입니다.

1. **만들기**&#x200B;를 선택하여 정보를 저장합니다.

>[!NOTE]
>
>다양한 색상 및/또는 크기로 제공되는 제품이 많습니다. 기본 제품 및 관련 제품 변형에 대한 정보는 모두 **제품** 콘솔에서 관리할 수 있습니다.
>
>제품 및 해당 변형은 트리 구조로 저장되고 제품 정보는 맨 위에 있으며 변형은 맨 아래에 있습니다(이 구조는 UI에 의해 적용됨).

### 제품 정보 편집 {#editing-product-information}

>[!NOTE]
>
>geometrixx-outdoors의 제품 이미지는 다음 위치에서 제공됩니다.
>
>`/etc/commerce/products/...`
>
>즉, 기본적으로 [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html)에 의해 차단되므로 필요에 따라 구성합니다.

#### 제품 정보 편집 - 터치에 적합한 UI {#editing-product-information-touch-optimized-ui}

1. **Commerce**&#x200B;을 통해 **제품** 콘솔을 사용하여 제품 정보로 이동합니다.
1. 다음 중 하나를 사용합니다.

   * [빠른 작업](/help/sites-authoring/basic-handling.md#quick-actions)
   * [선택 모드](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   **제품 데이터 보기** 아이콘을 선택합니다.

   ![제품 데이터 보기 아이콘 - 정보 아이콘](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. [제품 특성](/help/commerce/cif-classic/administering/concepts.md#product-attributes)이 표시됩니다. 변경하려면 **편집** 및 **완료**&#x200B;를 사용하세요.

### 제품 참조 표시 {#showing-product-references}

#### 제품 참조 표시 - 터치에 적합한 UI {#showing-product-references-touch-optimized-ui}

1. **Commerce**&#x200B;을 통해 **제품** 콘솔을 사용하여 제품 정보로 이동합니다.
1. 아이콘을 사용하여 참조에 대한 보조 레일을 엽니다.

   ![양방향 화살표 아이콘](/help/sites-administering/do-not-localize/chlimage_1-16.png)

1. 필요한 제품(보조 레일 업데이트)을 선택하면 사용 가능한 참조 유형이 표시됩니다.

   참조가 열려 있는 ![제품 콘솔](/help/sites-administering/assets/chlimage_1-88.png)

1. 참조 유형(예: 제품 페이지)을 클릭하여 목록을 확장합니다.
1. 옵션을 표시할 수 있도록 특정 참조를 선택합니다.

   * 제품 페이지로 이동
   * 제품 페이지 편집

   ![제품 콘솔 참조 패널](/help/sites-administering/assets/chlimage_1-89.png)

### 제품 검색 {#search-for-products}

1. **Commerce**&#x200B;을(를) 통해 **제품** 콘솔로 이동합니다.
1. 아이콘을 사용하여 검색할 보조 레일을 엽니다.

   ![돋보기 아이콘](/help/sites-administering/do-not-localize/chlimage_1-17.png)

1. 몇 가지 패싯을 사용하여 제품을 검색할 수 있습니다. 검색에 하나 또는 여러 패싯만 사용할 수 있습니다. 발견된 제품이 표시됩니다.

   ![제품 콘솔의 제품 데이터](/help/sites-administering/assets/chlimage_1-90.png)

1. 제품을 클릭/탭하면 제품이 열립니다. 게시하거나 제품 데이터를 볼 수도 있습니다.

#### 검색 확장 {#extending-search}

CRXDE Lite을 사용하여 기존 패싯을 수정하거나 새 패싯을 추가할 수 있습니다.

1. 다음으로 이동합니다.

   `http://localhost:4502/crx/de/index.jsp#/libs/commerce/gui/content/products/aside/items/search/items/searchpanel/facets`

1. 예를 들어 제품 검색 페이지에 나타나는 크기를 편집할 수 있습니다. `sizegroup` 노드를 클릭합니다.
1. `items` 노드를 클릭한 다음 `propertypredicate` 노드를 클릭합니다.
1. `propertyValues`을(를) 편집할 수 있습니다. 예를 들어 XS 또는 XXL을 추가하거나 크기를 제거할 수 있습니다.
1. **모두 저장**&#x200B;을 클릭하고 제품 검색 페이지로 이동합니다. 변경 사항이 표시됩니다.

### 여러 Assets {#multiple-assets}

제품 구성 요소에 여러 에셋을 추가한 다음 제품 페이지에 표시하려는 에셋을 지정할 수 있습니다.

>[!NOTE]
>
>여러 에셋과 관련된 모든 작업은 터치에 적합한 UI로 수행됩니다.

#### 여러 Assets 추가 {#adding-multiple-assets}

1. **Commerce**&#x200B;을(를) 통해 **제품** 콘솔로 이동합니다.
1. **제품** 콘솔을 사용하여 필요한 제품으로 이동합니다.

   >[!NOTE]
   >
   >변형 수준이 아닌 제품 수준에 있어야 합니다.

1. 선택 모드 또는 빠른 작업으로 **제품 데이터 보기** 아이콘을 선택합니다.
1. 편집 아이콘을 선택합니다.
1. **추가**(으)로 스크롤합니다.

   ![제품 데이터 스크린샷 추가](/help/sites-administering/assets/chlimage_1-91.png)

1. **추가**&#x200B;를 선택합니다. 새 자산 자리 표시자가 나타납니다.
1. **변경**&#x200B;을 선택하면 에셋을 선택할 수 있는 대화 상자가 열립니다.
1. 추가할 자산을 선택합니다.

   >[!NOTE]
   >
   >선택할 수 있는 자산은 [Assets](/help/assets/assets.md)에서 가져온 것입니다.

1. 완료 아이콘을 선택합니다.

이제 두 개의 자산이 제품 구성 요소에 저장됩니다. 제품 페이지에 표시될 항목을 구성할 수 있습니다. 카테고리 시스템과 함께 작동합니다. 먼저 개별 자산에 범주를 추가해야 합니다.

1. **제품 데이터 보기**&#x200B;를 선택합니다.
1. 자산 아래에 **자산 범주**&#x200B;을(를) 입력하십시오(예: `cat1` 및 `cat2`).

   >[!NOTE]
   >
   >카테고리에 태그를 사용할 수도 있습니다.

1. 완료 아이콘을 선택합니다. 이제 변경 내용을 [롤아웃](#rolling-out-a-catalog)해야 합니다.

이제 제품 구성 요소의 에셋에 카테고리가 있습니다. 세 가지 다른 수준에 표시할 카테고리를 구성할 수 있습니다.

* [제품 페이지](#product-page)
* [카탈로그](#catalog)
* [제품 콘솔](#products-console)

>[!NOTE]
>
>카테고리를 설정하지 않으면 첫 번째 에셋이 제품 페이지에 표시됩니다.

표시할 이미지를 선택하는 메커니즘은 다음과 같습니다.

1. 제품 페이지에 대해 범주가 설정되어 있는지 확인합니다.
1. 그렇지 않으면 카탈로그에 대한 범주가 설정되어 있는지 확인하십시오.
1. 그렇지 않으면 제품 콘솔에 대해 범주가 설정되어 있는지 확인하십시오.

>[!NOTE]
>
>카탈로그 수준과 제품 콘솔 수준 모두에 대해 변경 사항을 롤아웃하여 수정 사항을 적용하고 제품 페이지에서 차이점을 확인해야 합니다.

#### 제품 페이지 {#product-page}

1. 제품 페이지로 이동합니다.
1. 제품 구성 요소를 **편집**&#x200B;합니다.
1. 선택한 **이미지 범주**&#x200B;을(를) 입력하십시오(예: `cat1`).
1. **완료**&#x200B;를 선택합니다. 페이지가 새로 고침되고 올바른 에셋이 표시되어야 합니다.

#### 카탈로그  {#catalog}

1. 카탈로그로 이동합니다.
1. **속성 보기**&#x200B;를 선택합니다.
1. **편집**&#x200B;을 선택합니다.
1. **자산** 탭을 선택합니다.
1. 필요한 **제품 자산 범주**&#x200B;를 입력하십시오.
1. **완료**&#x200B;를 선택합니다.
1. 변경 내용을 [롤아웃](#rolling-out-a-catalog)합니다.

#### 제품 콘솔 {#products-console}

1. **제품** 콘솔을 사용하여 필요한 제품으로 이동합니다.
1. **제품 데이터 보기**&#x200B;를 선택합니다.
1. **편집**&#x200B;을 선택합니다.
1. **기본 자산 범주**&#x200B;를 입력하십시오.
1. **완료**&#x200B;를 선택합니다.
1. 변경 내용을 [롤아웃](#rolling-out-a-catalog)합니다.

### 제품 정보 게시/게시 취소 {#publishing-unpublishing-product-information}

#### 제품 정보 게시/게시 취소 - 터치에 적합한 UI {#publishing-unpublishing-product-information-touch-optimized-ui}

>[!NOTE]
>
>종종 제품 정보는 해당 정보를 참조하는 페이지를 통해 게시됩니다. 예를 들어 제품 Y를 참조하는 페이지 X를 게시할 때 AEM은 제품 Y도 게시할지를 묻는 메시지를 표시합니다.
>
>특수한 경우 AEM은 제품 데이터에서 직접 게시도 지원합니다.

1. **Commerce**&#x200B;을 통해 **제품** 콘솔을 사용하여 제품 정보로 이동합니다.
1. 다음 중 하나를 사용합니다.

   * [빠른 작업](/help/sites-authoring/basic-handling.md#quick-actions)
   * [선택 모드](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   필요에 따라 **Publish** 또는 **게시 취소** 아이콘을 선택하십시오.

   ![세계 아이콘](/help/sites-administering/do-not-localize/chlimage_1-18.png) ![십자가가 있는 세계 아이콘 - 기호 없음](/help/sites-administering/do-not-localize/chlimage_1-19.png)

   제품 정보는 적절하게 게시되거나 게시 취소됩니다.

<!-- Search&Promote is end of life as of September 1, 2022 ### Product Feed {#product-feed} -->

<!-- Search&Promote is end of life as of September 1, 2022 The Search&Promote integration lets you: -->

<!-- Search&Promote is end of life as of September 1, 2022 * use the eCommerce API, independently of the underlying repository structure and commerce platform. -->
<!-- Search&Promote is end of life as of September 1, 2022 * use the Index Connector feature of Search&Promote to provide a product feed in XML format. -->
<!-- Search&Promote is end of life as of September 1, 2022 * use the Remote Control feature of Search&Promote to perform on-demand or scheduled requests of the product feed -->
<!-- Search&Promote is end of life as of September 1, 2022 * feed generation for different Search&Promote accounts, configured as cloud services configurations. -->

<!-- Search&Promote is end of life as of September 1, 2022 For more information, read [Product Feed](/help/sites-administering/product-feed.md). -->

### 제품 업데이트에 대한 이벤트 핸들러 {#event-handler-for-product-updates}

이벤트 핸들러는 제품이 추가, 편집 또는 삭제되고 제품 페이지가 추가, 편집 또는 삭제될 때 이벤트를 기록합니다. 다음 OSGi 이벤트가 있습니다.

* `com/adobe/cq/commerce/pim/PRODUCT_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_DELETED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_DELETED`

`PRODUCT_*` 이벤트의 경우 경로는 `/etc/commerce/products`의 기본 제품을 가리킵니다. `PRODUCT_PAGE_*` 이벤트의 경우 경로는 `cq:Page` 노드를 가리킵니다.

예를 들어 OSGI 이벤트(`/system/console/events`)의 웹 콘솔에서 볼 수 있습니다.

![OSGI 이벤트 예](/help/sites-administering/do-not-localize/chlimage_1-20.png)

>[!NOTE]
>
>[AEM의 이벤트 처리](https://blogs.adobe.com/experiencedelivers/experience-management/event_handling_incq/)도 읽어 보십시오.

### 장바구니에 추가 링크가 있는 이미지 {#image-with-add-to-cart-links}

장바구니에 추가 링크가 있는 이미지 구성 요소를 사용하면 이미지에 제품과 연결된 핫스팟을 만들어 제품을 장바구니에 빠르게 추가할 수 있습니다.

핫스팟을 클릭하면 제품의 크기와 수량을 선택할 수 있는 대화 상자가 열립니다.

1. 구성 요소를 추가하려는 페이지로 이동합니다.
1. 구성 요소를 페이지에 끌어다 놓습니다.
1. [자산 브라우저](/help/sites-authoring/author-environment-tools.md#assets-browser)에서 구성 요소에 이미지를 끌어다 놓습니다.
1. 다음과 같은 작업을 수행할 수 있습니다.

   * 구성 요소를 클릭한 다음, 편집 아이콘을 클릭합니다
   * 느리게 두 번 클릭

1. 전체 화면 아이콘을 클릭합니다.

   ![전체 화면 아이콘](/help/sites-administering/assets/chlimage_1-92.png)

1. Launch Map 아이콘을 클릭합니다.

   ![맵 시작 아이콘](/help/sites-administering/assets/chlimage_1-93.png)

1. 모양 아이콘 중 하나를 클릭합니다.

   ![모양 아이콘](/help/sites-administering/do-not-localize/chlimage_1-21.png)

1. 필요에 따라 모양을 수정하고 이동합니다.
1. 모양을 클릭합니다.
1. 찾아보기 아이콘을 클릭하면 [자산 선택기](/help/assets/search-assets.md#assetpicker)가 열립니다.

   >[!NOTE]
   >
   >또는 변형 수준이 아닌 제품 수준에 있어야 하는 제품 경로를 직접 입력할 수 있습니다.

   ![유형 경로](/help/sites-administering/assets/chlimage_1-94.png)

1. 확인 아이콘을 두 번 클릭한 다음 전체 화면 종료 를 클릭합니다.
1. 구성 요소 옆에 있는 페이지의 아무 곳이나 클릭합니다. 페이지가 새로 고침되고 이미지에 다음 기호가 표시됩니다.

   ![더하기 기호](/help/sites-administering/do-not-localize/chlimage_1-22.png)

1. [미리 보기](/help/sites-authoring/editing-content.md#previewingpagestouchoptimizedui) 모드로 전환합니다.
1. &#x200B;+ 핫스팟을 클릭합니다. **경로**&#x200B;에서 입력한 제품의 크기와 수량을 선택할 수 있는 대화 상자가 열립니다.

   ![제품 예: poncho](/help/sites-administering/assets/chlimage_1-95.png)

1. 크기와 수량을 입력합니다.
1. 장바구니에 추가 단추를 클릭합니다. 대화 상자가 닫힙니다.
1. 장바구니로 이동합니다. 제품이 여기에 있어야 합니다.

#### 구성 옵션 {#configuration-options}

핫스팟을 클릭할 때의 대화 상자 모양을 구성할 수 있습니다.

1. 구성 요소를 클릭하고 구성 아이콘을 클릭합니다.

   ![구성 아이콘](/help/sites-administering/assets/chlimage_1-96.png)

1. 아래로 스크롤합니다. **장바구니에 추가** 탭이 있습니다.

   ![장바구니 탭에 추가](/help/sites-administering/assets/chlimage_1-97.png)

1. **장바구니에 추가**&#x200B;를 클릭합니다. 사용할 수 있는 구성 옵션에는 세 가지가 있습니다.

   ![구성 옵션](/help/sites-administering/assets/chlimage_1-98.png)

1. 완료 아이콘을 클릭합니다.

## 카탈로그 {#catalogs}

### 카탈로그 생성 {#generating-a-catalog}

#### 카탈로그 생성 - 터치에 적합한 UI {#generating-a-catalog-touch-optimized-ui}

>[!NOTE]
>
>카탈로그가 제품 데이터를 참조합니다.

카탈로그를 생성하려면:

1. 사이트 콘솔을 엽니다(예: [http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content)).
1. 페이지를 만들려는 위치로 이동합니다.
1. 옵션 목록을 열려면 **만들기** 아이콘을 사용합니다.

   ![create-icon](/help/sites-administering/do-not-localize/chlimage_1-23.png)

1. 목록에서 **카탈로그 만들기**&#x200B;를 선택합니다. 카탈로그 만들기 마법사가 열립니다.

   ![카탈로그 만들기 마법사](/help/sites-administering/assets/chlimage_1-99.png)

1. 필요한 카탈로그 블루프린트로 이동합니다.
1. **선택** 단추를 선택하고 필요한 카탈로그 블루프린트를 클릭합니다.
1. **다음**&#x200B;을 선택합니다.

   ![카탈로그 속성 마법사](/help/sites-administering/assets/chlimage_1-100.png)

1. **제목**&#x200B;과(와) **이름**&#x200B;을(를) 입력하십시오.
1. **만들기** 단추를 선택하십시오. 카탈로그가 생성되고 대화 상자가 열립니다.

   ![카탈로그 만들기 대화 상자](/help/sites-administering/assets/chlimage_1-101.png)

1. **완료** 단추를 선택하면 카탈로그를 볼 수 있는 사이트 콘솔로 돌아갑니다.

   **카탈로그 열기** 단추를 탭하거나 클릭하면 카탈로그가 열립니다(예: `http://localhost:4502/editor.html/content/test-catalog.html`).

#### 카탈로그 생성 - 클래식 UI {#generating-a-catalog-classic-ui}

>[!NOTE]
>
>카탈로그가 [제품 데이터](#products-and-product-variants)를 참조합니다.

1. **웹 사이트** 콘솔을 사용하여 **카탈로그 블루프린트**&#x200B;로 이동한 다음 기본 카탈로그로 이동합니다.

   예:

   `http://localhost:4502/siteadmin#/content/catalogs/geometrixx-outdoors/base-catalog`

1. **섹션 블루프린트** 템플릿을 사용하여 페이지를 만드십시오.

   예: `Swimwear`

1. 새 `Swimwear` 페이지를 연 다음 **블루프린트 편집**&#x200B;을 클릭합니다. **제품** 선택을 설정할 수 있도록 **속성** 대화 상자가 열립니다.

   예를 들어 **태그/키워드** 필드를 열어 활동, Geometrixx-Outdoors 섹션에서 수영 순으로 선택합니다.

1. 속성을 저장하려면 **확인**&#x200B;을 클릭하세요. 예제 제품은 블루프린트 페이지의 **제품 선택 기준** 아래에 표시됩니다.
1. **롤아웃 변경...**&#x200B;을 클릭하고 **롤아웃 페이지와 모든 하위 페이지**&#x200B;을 선택한 다음 **다음**, **롤아웃**&#x200B;을 클릭합니다. 롤아웃이 완료되면 **상태** 표시기가 녹색으로 표시됩니다.
1. 이제 **닫기**&#x200B;를 클릭하고 새 카탈로그 섹션을 확인할 수 있습니다(예: 다음 중/아래에서).

   `http://localhost:4502/cf#/content/geometrixx-outdoors/en/swimwear.html`

1. 블루프린트 페이지에서 다시 **블루프린트 편집**&#x200B;을 클릭하고 **속성** 대화 상자에서 **생성된 페이지** 탭을 엽니다. 배너 목록 필드에서 표시할 이미지를 선택합니다(예: `summer.jpg`)
1. 속성이 저장되도록 **확인**&#x200B;을 클릭하세요. 배너 정보는 블루프린트 페이지의 **제품 선택 기준** 아래에 표시됩니다.
1. 이러한 새 변경 사항을 롤아웃합니다.

### 카탈로그 롤아웃 {#rolling-out-a-catalog}

#### 카탈로그 롤아웃 - 터치에 적합한 UI {#rolling-out-a-catalog-touch-optimized-ui}

카탈로그를 롤아웃하려면 다음 작업을 수행하십시오.

1. **Commerce**&#x200B;을(를) 통해 **카탈로그** 콘솔로 이동합니다.
1. 롤아웃할 카탈로그로 이동합니다.
1. 다음 중 하나를 사용합니다.

   * [빠른 작업](/help/sites-authoring/basic-handling.md#quick-actions)
   * [선택 모드](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   **롤아웃 변경 내용** 아이콘을 선택합니다.

   ![롤아웃](/help/sites-administering/do-not-localize/chlimage_1-24.png)

1. 마법사에서 필요에 따라 롤아웃을 설정한 다음 **변경 내용 롤아웃**&#x200B;을 클릭합니다.
1. 대화 상자가 열립니다. 프로세스가 완료되면 **완료**&#x200B;를 선택합니다.

#### 카탈로그 롤아웃 - 클래식 UI {#rolling-out-a-catalog-classic-ui}

카탈로그를 롤아웃하려면 다음 작업을 수행하십시오.

1. 롤아웃할 카탈로그로 이동합니다. 예:

   `http://localhost:4502/cf#/content/catalogs/geometrixx-outdoors/base-catalog.html`

1. **롤아웃 변경...**&#x200B;을 클릭합니다.
1. 필요에 따라 롤아웃을 설정합니다.
1. **롤아웃**&#x200B;을 클릭합니다.

### 블루프린트 가져오기 {#blueprint-importer}

#### 블루프린트 가져오기 - 터치에 적합한 UI {#blueprint-importer-touch-optimized-ui}

1. **Commerce**&#x200B;을(를) 통해 **카탈로그** 콘솔로 이동합니다.
1. 카탈로그 블루프린트를 가져올 위치로 이동합니다.
1. **블루프린트 가져오기** 아이콘을 선택합니다.

   ![블루프린트 가져오기 아이콘](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. 마법사에서 필요에 따라 Source을 선택하고 **다음**&#x200B;을 클릭합니다.

   ![블루프린트 마법사](/help/sites-administering/assets/chlimage_1-102.png)

1. 가져오기가 완료되면 **완료**&#x200B;를 선택합니다.

#### 블루프린트 Importer - 클래식 UI {#blueprint-importer-classic-ui}

1. **도구** 콘솔을 사용하여 **Commerce**(으)로 이동합니다.

   예:

   `http://localhost:4502/miscadmin#/etc/commerce`

1. **카탈로그 블루프린트 가져오기**&#x200B;를 엽니다.
1. 필요에 따라 가져오기를 설정합니다.
1. **카탈로그 블루프린트 가져오기**&#x200B;를 클릭합니다.

## 프로모션 {#promotions}

### 프로모션 생성 {#creating-a-promotion}

#### 프로모션 만들기 - 클래식 UI {#creating-a-promotion-classic-ui}

>[!NOTE]
>
>다음 예제에서는 [campaign](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)에서 직접 진행되는 프로모션을 다루며, 바우처에 사용됩니다.
>
>캠페인의 [경험](/help/sites-authoring/personalization.md)에서도 프로모션을 사용할 수 있습니다.
>
>자세한 내용은 [프로모션 및 바우처](#promotions-and-vouchers)를 참조하십시오.

1. 작성자 인스턴스의 **웹 사이트** 콘솔을 엽니다.
1. 왼쪽 창에서 필요한 **Campaign**&#x200B;을(를) 선택합니다.
1. **새로 만들기**&#x200B;를 클릭하고 **홍보** 템플릿을 선택한 다음 새 바우처에 대해 **제목**(필요한 경우 **이름**)을 지정하십시오.
1. **만들기**&#x200B;를 클릭합니다. 오른쪽 창에 새 프로모션 페이지가 표시됩니다.

1. 다음 방법 중 하나로 **속성**&#x200B;을 편집합니다.

   * 페이지를 연 다음 편집 단추를 클릭하여 속성 대화 상자를 엽니다
   * 웹 사이트 콘솔에서 페이지를 선택한 다음 컨텍스트 메뉴(보통 오른쪽 마우스 단추)를 사용하여 **속성...**&#x200B;을 선택하고 속성 대화 상자를 엽니다

   필요에 따라 **프로모션 유형**, **할인 유형**, **할인 값** 및 기타 필드를 지정하십시오.

1. 저장하려면 **확인**&#x200B;을 클릭하세요.

1. 이제 쇼퍼가 게시 인스턴스에서 볼 수 있도록 프로모션을 활성화할 수 있습니다.

## 바우처 {#vouchers}

### 바우처 만들기 {#creating-a-voucher}

#### 바우처 만들기 - 클래식 UI {#creating-a-voucher-classic-ui}

1. 작성자 인스턴스의 **웹 사이트** 콘솔을 엽니다.
1. 왼쪽 창에서 필요한 **Campaign**&#x200B;을(를) 선택합니다.
1. **새로 만들기**&#x200B;를 클릭하고 **바우처** 템플릿을 선택한 다음 새 바우처에 대한 **제목**(필요한 경우 **이름**)을 지정하십시오.
1. **만들기**&#x200B;를 클릭합니다. 오른쪽 창에 새 바우처 페이지가 표시됩니다.

1. 새 바우처 페이지를 두 번 클릭하여 연 다음 **편집**&#x200B;을 클릭하고 필요에 따라 정보를 구성합니다.
1. 저장하려면 **확인**&#x200B;을 클릭하세요.

1. 이제 구매자가 게시 인스턴스의 카트에서 사용할 수 있도록 바우처를 활성화할 수 있습니다.

### 바우처 제거 {#removing-vouchers}

#### 바우처 제거 - 클래식 UI {#removing-vouchers-classic-ui}

고객이 바우처를 사용할 수 없도록 하려면 다음 중 하나를 수행할 수 있습니다.

* 바우처를 비활성화합니다. 나중에 다시 활성화할 수 있도록 작성자 환경에서 사용할 수 있습니다.
* 완전히 삭제하십시오.

두 작업은 **웹 사이트** 콘솔에서 수행할 수 있습니다.

### 바우처 수정 {#modifying-vouchers}

#### 바우처 수정 - 클래식 UI {#modifying-vouchers-classic-ui}

바우처 또는 프로모션의 속성을 변경하려면 **웹 사이트** 콘솔에서 두 번 클릭한 다음 **편집**&#x200B;을 클릭합니다. 저장한 후 변경 사항이 게시 인스턴스로 푸시되도록 활성화해야 합니다.

### 장바구니에 바우처 추가 {#adding-vouchers-to-a-cart}

사용자가 장바구니에 바우처를 추가할 수 있도록 하려면 기본 제공 **바우처** 구성 요소(Commerce 범주)를 사용할 수 있습니다. 장바구니가 표시되는 페이지와 동일한 페이지에 추가합니다(하지만 필수 페이지는 아님). 바우처 구성 요소는 사용자가 바우처 코드를 입력할 수 있는 형식일 뿐이며, 실제로 적용된 바우처 목록과 할인을 보여 주는 장바구니 구성 요소입니다.

데모 사이트(Geometrixx Outdoors - 영어)의 장바구니 페이지에 있는 실제 장바구니 아래의 바우처 양식을 볼 수 있습니다.

## 주문 {#orders}

>[!NOTE]
>
>즉시 사용 가능한 AEM에는 반품, 주문 상태 업데이트, 이행, 포장 명세서 생성과 같은 주문과 관련된 표준 기능에 필요한 작업이 없습니다. 주로 기술 미리보기 목적으로 사용됩니다.
>
>AEM의 일반 Order Management은 기본적으로 유지됩니다. 마법사에서 사용할 수 있는 필드는 스캐폴드에 따라 다릅니다.
>`/etc/scaffolding/geometrixx-outdoors/order/jcr:content/cq:dialog`
>
>맞춤형 scaffold를 생성하면 더 많은 주문 정보를 저장할 수 있습니다.

>[!NOTE]
>
>주문 콘솔은 게시되지 않는 공급업체 주문 정보를 노출합니다.
>
>고객 주문 정보는 홈 디렉토리에 보관되며 계정의 주문 내역에 표시됩니다. 이 정보는 홈 디렉터리의 나머지 부분과 함께 게시됩니다.

### 주문 정보 생성 {#creating-order-information}

#### 주문 정보 만들기 - 터치에 적합한 UI {#creating-order-information-touch-optimized-ui}

1. **주문** 콘솔을 사용하여 필요한 위치로 이동합니다.
1. **만들기** 아이콘을 사용하여 **순서 만들기**&#x200B;를 선택하십시오.

   ![더하기 모양의 만들기 아이콘](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. 마법사가 열립니다. **기본**, **콘텐츠**, **결제** 및 **이행** 탭을 사용하여 [새 주문에 대한 정보](/help/commerce/cif-classic/administering/concepts.md#order-information)를 입력하십시오.

1. **만들기**&#x200B;를 선택하여 정보를 저장합니다.

### 주문 정보 편집 {#editing-order-information}

#### 주문 정보 편집 - 터치에 적합한 UI {#editing-order-information-touch-optimized-ui}

1. **주문** 콘솔을 사용하여 주문으로 이동합니다.
1. 다음 중 하나를 사용합니다.

   * [빠른 작업](/help/sites-authoring/basic-handling.md#quick-actions)
   * [선택 모드](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   **주문 데이터 보기** 아이콘을 선택합니다.

   ![정보 아이콘](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. [주문 정보](/help/commerce/cif-classic/administering/concepts.md#order-information)가 표시됩니다. 변경하려면 **편집** 및 **완료**&#x200B;를 사용하세요.

