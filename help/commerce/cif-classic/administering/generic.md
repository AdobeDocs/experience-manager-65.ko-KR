---
title: 일반 전자 상거래 관리
description: AEM 일반 솔루션은 저장소 내에 있는 상거래 정보를 관리하는 방법을 제공합니다.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: c29f6213-1df6-45af-91c8-14b255276d82
source-git-commit: b00ed4ed146b89aece9af1d267c890a360a236e9
workflow-type: tm+mt
source-wordcount: '2929'
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

제품을 만들기 전에 다음을 정의합니다. [스캐폴드](/help/sites-authoring/scaffolding.md). 정의해야 하는 필드, 제품 및 편집 방법을 지정합니다.

각각의 개별 제품 유형에 대한 스캐폴드가 필요합니다. 적절한 스캐폴드는 다음 중 하나를 통해 제품과 연계됩니다.

* path
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

1. 다음 위치로 이동 **제품** 콘솔, 를 통해 **상거래**.
1. 사용 **제품** 콘솔이 필요한 위치로 이동합니다.
1. 사용 **제품 가져오기** 아이콘을 클릭하여 마법사를 엽니다.

   ![제품 가져오기 아이콘](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. 지정:

   * **가져오기**

     특정 항목 가져오기 [상거래 공급자](/help/commerce/cif-classic/administering/concepts.md#commerce-providers), 기본적으로 `Geometrixx`.

   * **소스**

     가져올 파일로, 브라우저를 사용하여 파일을 선택할 수 있습니다.

   * **증분 가져오기**

     증분 가져오기인지 여부를 나타냅니다(전체와 반대).

   >[!NOTE]
   >
   >(샘플 geometrixx-outdoor 가져오기의) 증분 가져오기는 제품 수준에서 작동합니다.
   >
   >필요에 따라 작동하도록 맞춤형 임포터를 정의할 수 있습니다.

1. 선택 **다음** 제품을 가져오려면 수행한 작업의 로그가 표시됩니다.

   >[!NOTE]
   >
   >제품을 현재 위치로 가져오거나 현재 위치에 대해 가져옵니다.

   >[!NOTE]
   >
   >반복 사용 **다음** 및 **뒤로** 제품 정의를 반복적으로 가져옵니다. 그러나 동일한 SKU를 포함하므로 저장소에 있는 정보를 덮어씁니다.

1. 선택 **완료** 마법사를 닫습니다.

#### 제품 가져오기 - 클래식 UI {#importing-products-classic-ui}

1. 사용 **도구** 콘솔 열기 **상거래** 폴더를 삭제합니다.
1. 두 번 클릭하여 열기 **제품 가져오기**:

   ![제품 Importer 콘솔](/help/sites-administering/assets/chlimage_1-22.jpeg)

1. 지정:

   * **저장소 이름**

     제품을 다음 위치로 가져옵니다.

     `/etc/commerce/products/<*store name*>/`

   * **상거래 공급자**

     에 대한 가져오기 [상거래 공급자](/help/commerce/cif-classic/administering/concepts.md#commerce-providers); 기본적으로 Geometrixx.

   * **소스 파일**

     가져오려는 파일의 저장소 위치입니다.

   * **증분 가져오기**

     증분 가져오기인지 여부를 나타냅니다(전체와 반대).

1. 클릭 **제품 가져오기**.

### 제품 정보 만들기 {#creating-product-information}

>[!NOTE]
>
>Geometrixx-Outdoors 제품 세트가 기본적으로 유지되므로 표준 제품 관리는 기본입니다. 복잡성은 제품을 기반으로 합니다 [스캐폴딩](/help/sites-authoring/scaffolding.md), 따라서 자체 제품 스캐폴딩으로 보다 정교한 편집이 가능합니다.

#### 제품 정보 만들기 - 터치에 적합한 UI {#creating-product-information-touch-optimized-ui}

1. 사용 **제품** 콘솔(를 통해) **상거래**) 필요한 위치로 이동합니다.
1. 사용 **만들기** 아이콘 을 클릭하여 구조와 위치에 따라 다음 중 하나를 선택합니다.

   * **제품 만들기**
   * **제품 변형 만들기**

   ![플러스 모양 만들기 아이콘](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. 마법사가 열립니다. 사용 **기본** 및 **제품 탭** 을(를) 입력하려면 [제품 속성](/help/commerce/cif-classic/administering/concepts.md#product-attributes) (새 제품 또는 제품 변형)

   >[!NOTE]
   >
   >**제목** 및 **SKU** 는 제품 또는 변형을 만드는 데 필요한 최소값입니다.

1. 선택 **만들기** 을 클릭하여 정보를 저장합니다.

>[!NOTE]
>
>다양한 색상 및/또는 크기로 제공되는 제품이 많습니다. 기본 제품 및 관련 제품 변형에 대한 정보는 모두 **제품** 콘솔.
>
>제품 및 해당 변형은 트리 구조로 저장되고 제품 정보는 맨 위에 있으며 변형은 맨 아래에 있습니다(이 구조는 UI에 의해 적용됨).

### 제품 정보 편집 {#editing-product-information}

>[!NOTE]
>
>geometrixx-outdoors의 제품 이미지는 다음 위치에서 제공됩니다.
>
>`/etc/commerce/products/...`
>
>즉, 기본적으로 [디스패처](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html)필요한 경우 를 구성합니다.

#### 제품 정보 편집 - 터치에 적합한 UI {#editing-product-information-touch-optimized-ui}

1. 사용 **제품** 콘솔(를 통해) **상거래**) 제품 정보로 이동합니다.
1. 다음 중 하나를 사용합니다.

   * [빠른 작업](/help/sites-authoring/basic-handling.md#quick-actions)
   * [선택 모드](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   다음 항목 선택 **제품 데이터 보기** 아이콘:

   ![제품 데이터 보기 아이콘 - 정보 아이콘](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. 다음 [제품 속성](/help/commerce/cif-classic/administering/concepts.md#product-attributes) 이 표시됩니다. 사용 **편집** 및 **완료** 원하는 대로 변경할 수 있습니다.

### 제품 참조 표시 {#showing-product-references}

#### 제품 참조 표시 - 터치에 적합한 UI {#showing-product-references-touch-optimized-ui}

1. 사용 **제품** 콘솔(를 통해) **상거래**) 제품 정보로 이동합니다.
1. 아이콘을 사용하여 참조에 대한 보조 레일을 엽니다.

   ![이중 화살표 아이콘](/help/sites-administering/do-not-localize/chlimage_1-16.png)

1. 필요한 제품(보조 레일 업데이트)을 선택하면 사용 가능한 참조 유형이 표시됩니다.

   ![참조가 열려 있는 제품 콘솔](/help/sites-administering/assets/chlimage_1-88.png)

1. 참조 유형(예: 제품 페이지)을 클릭/탭하여 목록을 확장합니다.
1. 옵션을 표시할 수 있도록 특정 참조를 선택합니다.

   * 제품 페이지로 이동
   * 제품 페이지 편집

   ![제품 콘솔 참조 패널](/help/sites-administering/assets/chlimage_1-89.png)

### 제품 검색 {#search-for-products}

1. 다음 위치로 이동 **제품** 콘솔, 를 통해 **상거래**.
1. 아이콘을 사용하여 검색할 보조 레일을 엽니다.

   ![돋보기 아이콘](/help/sites-administering/do-not-localize/chlimage_1-17.png)

1. 몇 가지 패싯을 사용하여 제품을 검색할 수 있습니다. 검색에 하나 또는 여러 패싯만 사용할 수 있습니다. 발견된 제품이 표시됩니다.

   ![제품 콘솔의 제품 데이터](/help/sites-administering/assets/chlimage_1-90.png)

1. 제품을 클릭/탭하면 제품이 열립니다. 게시하거나 제품 데이터를 볼 수도 있습니다.

#### 검색 확장 {#extending-search}

CRXDE Lite을 사용하여 기존 패싯을 수정하거나 새 패싯을 추가할 수 있습니다.

1. 다음으로 이동합니다.

   `http://localhost:4502/crx/de/index.jsp#/libs/commerce/gui/content/products/aside/items/search/items/searchpanel/facets`

1. 예를 들어 제품 검색 페이지에 나타나는 크기를 편집할 수 있습니다. 다음을 클릭합니다. `sizegroup` 노드.
1. 클릭 `items` 노드를 클릭한 다음 `propertypredicate` 노드.
1. 다음을 편집할 수 있습니다. `propertyValues`. 예를 들어 XS 또는 XXL을 추가하거나 크기를 제거할 수 있습니다.
1. 클릭 **모두 저장** 제품 검색 페이지로 이동합니다. 변경 사항이 표시됩니다.

### 여러 자산 {#multiple-assets}

제품 구성 요소에 여러 에셋을 추가한 다음 제품 페이지에 표시하려는 에셋을 지정할 수 있습니다.

>[!NOTE]
>
>여러 에셋과 관련된 모든 작업은 터치에 적합한 UI로 수행됩니다.

#### 여러 자산 추가 {#adding-multiple-assets}

1. 다음 위치로 이동 **제품** 콘솔, 를 통해 **상거래**.
1. 사용 **제품** 콘솔에서 필요한 제품으로 이동합니다.

   >[!NOTE]
   >
   >변형 수준이 아닌 제품 수준에 있어야 합니다.

1. 다음 항목 선택 **제품 데이터 보기** 선택 모드 또는 빠른 작업이 포함된 아이콘.
1. 편집 아이콘을 선택합니다.
1. 다음으로 스크롤 **추가**.

   ![제품 데이터 스크린샷 추가](/help/sites-administering/assets/chlimage_1-91.png)

1. 선택 **추가**. 새 자산 자리 표시자가 나타납니다.
1. 선택 **변경** 자산을 선택할 수 있는 대화 상자를 엽니다.
1. 추가할 자산을 선택합니다.

   >[!NOTE]
   >
   >선택할 수 있는 에셋은 출신입니다. [에셋](/help/assets/assets.md).

1. 완료 아이콘을 선택합니다.

이제 두 개의 자산이 제품 구성 요소에 저장됩니다. 제품 페이지에 표시될 항목을 구성할 수 있습니다. 카테고리 시스템과 함께 작동합니다. 먼저 개별 자산에 범주를 추가해야 합니다.

1. 선택 **제품 데이터 보기**.
1. 입력 **자산 범주** 에셋 아래(예: ) `cat1` 및 `cat2`.

   >[!NOTE]
   >
   >카테고리에 태그를 사용할 수도 있습니다.

1. 완료 아이콘을 선택합니다. 이제 다음을 수행해야 합니다. [롤아웃](#rolling-out-a-catalog) 변경 사항.

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
1. **편집** 제품 구성 요소입니다.
1. 을(를) 입력합니다 **이미지 범주** 선택한 항목( `cat1` 예).
1. 선택 **완료**. 페이지가 새로 고침되고 올바른 에셋이 표시되어야 합니다.

#### 카탈로그  {#catalog}

1. 카탈로그로 이동합니다.
1. 선택 **속성 보기**.
1. **편집**&#x200B;을 선택합니다.
1. 다음 항목 선택 **에셋** 탭.
1. 필수 입력 **제품 자산 범주**.
1. 선택 **완료**.
1. [롤아웃](#rolling-out-a-catalog) 변경 사항.

#### 제품 콘솔 {#products-console}

1. 사용 **제품** 콘솔에서 필요한 제품으로 이동합니다.
1. 선택 **제품 데이터 보기**.
1. **편집**&#x200B;을 선택합니다.
1. Type a **기본 자산 범주**.
1. 선택 **완료**.
1. [롤아웃](#rolling-out-a-catalog) 변경 사항.

### 제품 정보 게시/게시 취소 {#publishing-unpublishing-product-information}

#### 제품 정보 게시/게시 취소 - 터치에 적합한 UI {#publishing-unpublishing-product-information-touch-optimized-ui}

>[!NOTE]
>
>종종 제품 정보는 해당 정보를 참조하는 페이지를 통해 게시됩니다. 예를 들어 제품 Y를 참조하는 페이지 X를 게시할 때 AEM은 제품 Y도 게시할지를 묻는 메시지를 표시합니다.
>
>특수한 경우 AEM은 제품 데이터에서 직접 게시도 지원합니다.

1. 사용 **제품** 콘솔(를 통해) **상거래**) 제품 정보로 이동합니다.
1. 다음 중 하나를 사용합니다.

   * [빠른 작업](/help/sites-authoring/basic-handling.md#quick-actions)
   * [선택 모드](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   다음 항목 선택 **게시** 또는 **게시 취소** 아이콘(필요한 경우):

   ![세계 아이콘](/help/sites-administering/do-not-localize/chlimage_1-18.png) ![십자가가 있는 세계 아이콘 - 기호 없음](/help/sites-administering/do-not-localize/chlimage_1-19.png)

   제품 정보는 적절하게 게시되거나 게시 취소됩니다.

<!-- Search&Promote is end of life as of September 1, 2022 ### Product Feed {#product-feed} -->

<!-- Search&Promote is end of life as of September 1, 2022 The Search&Promote integration lets you: -->

<!-- Search&Promote is end of life as of September 1, 2022 * use the eCommerce API, independently of the underlying repository structure and commerce platform. -->
<!-- Search&Promote is end of life as of September 1, 2022 * leverage the Index Connector feature of Search&Promote to provide a product feed in XML format. -->
<!-- Search&Promote is end of life as of September 1, 2022 * leverage the Remote Control feature of Search&Promote to perform on-demand or scheduled requests of the product feed -->
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

의 경우 `PRODUCT_*` 이벤트에서 경로는 의 기본 제품을 가리킵니다. `/etc/commerce/products`. 의 경우 `PRODUCT_PAGE_*` events, 경로는 `cq:Page` 노드.

OSGI 이벤트의 웹 콘솔에서 이러한 이벤트를 볼 수 있습니다( `/system/console/events`) 예를 들면 다음과 같습니다.

![OSGI 이벤트 예](/help/sites-administering/do-not-localize/chlimage_1-20.png)

>[!NOTE]
>
>읽기 전용 [AEM에서의 이벤트 처리](https://blogs.adobe.com/experiencedelivers/experience-management/event_handling_incq/).

### 장바구니에 추가 링크가 있는 이미지 {#image-with-add-to-cart-links}

장바구니에 추가 링크가 있는 이미지 구성 요소를 사용하면 이미지에 제품과 연결된 핫스팟을 만들어 제품을 장바구니에 빠르게 추가할 수 있습니다.

핫스팟을 클릭하면 제품의 크기와 수량을 선택할 수 있는 대화 상자가 열립니다.

1. 구성 요소를 추가하려는 페이지로 이동합니다.
1. 구성 요소를 페이지에 끌어다 놓습니다.
1. 에서 구성 요소에 이미지를 드래그하여 놓습니다. [에셋 브라우저](/help/sites-authoring/author-environment-tools.md#assets-browser).
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
1. 찾아보기 아이콘을 클릭하면 [자산 선택기](/help/assets/search-assets.md#assetpicker).

   >[!NOTE]
   >
   >또는 변형 수준이 아닌 제품 수준에 있어야 하는 제품 경로를 직접 입력할 수 있습니다.

   ![경로 입력](/help/sites-administering/assets/chlimage_1-94.png)

1. 확인 아이콘을 두 번 클릭한 다음 전체 화면 종료 를 클릭합니다.
1. 구성 요소 옆에 있는 페이지의 아무 곳이나 클릭합니다. 페이지가 새로 고침되고 이미지에 다음 기호가 표시됩니다.

   ![더하기 기호](/help/sites-administering/do-not-localize/chlimage_1-22.png)

1. 다음으로 전환 [미리보기](/help/sites-authoring/editing-content.md#previewingpagestouchoptimizedui) 모드.
1. + 핫스팟을 클릭합니다. 입력한 제품의 크기와 수량을 선택할 수 있는 대화 상자가 열립니다 **경로**.

   ![제품 예: poncho](/help/sites-administering/assets/chlimage_1-95.png)

1. 크기와 수량을 입력합니다.
1. 장바구니에 추가 단추를 클릭합니다. 대화 상자가 닫힙니다.
1. 장바구니로 이동합니다. 제품이 여기에 있어야 합니다.

#### 구성 옵션 {#configuration-options}

핫스팟을 클릭할 때의 대화 상자 모양을 구성할 수 있습니다.

1. 구성 요소를 클릭하고 구성 아이콘을 클릭합니다.

   ![구성 아이콘](/help/sites-administering/assets/chlimage_1-96.png)

1. 아래로 스크롤. 다음 항목이 있습니다. **장바구니에 추가** 탭.

   ![장바구니에 추가 탭](/help/sites-administering/assets/chlimage_1-97.png)

1. 클릭 **장바구니에 추가**. 사용할 수 있는 구성 옵션에는 세 가지가 있습니다.

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
1. 옵션 목록을 열려면 **만들기** 아이콘:

   ![create-icon](/help/sites-administering/do-not-localize/chlimage_1-23.png)

1. 목록에서 를 선택합니다. **카탈로그 만들기**. 카탈로그 만들기 마법사가 열립니다.

   ![카탈로그 만들기 마법사](/help/sites-administering/assets/chlimage_1-99.png)

1. 필요한 카탈로그 블루프린트로 이동합니다.
1. 다음 항목 선택 **선택** 버튼을 클릭하고 필요한 카탈로그 블루프린트를 탭/클릭합니다.
1. **다음**&#x200B;을 선택합니다.

   ![카탈로그 속성 마법사](/help/sites-administering/assets/chlimage_1-100.png)

1. Type a **제목** 및 a **이름**.
1. **만들기** 버튼을 선택합니다. 카탈로그가 생성되고 대화 상자가 열립니다.

   ![카탈로그 생성 대화 상자](/help/sites-administering/assets/chlimage_1-101.png)

1. 선택 **완료** 버튼을 클릭하면 카탈로그를 볼 수 있는 사이트 콘솔로 돌아갑니다.

   탭/클릭 **카탈로그 열기** 버튼을 누르면 카탈로그가 열립니다(예: `http://localhost:4502/editor.html/content/test-catalog.html`).

#### 카탈로그 생성 - 클래식 UI {#generating-a-catalog-classic-ui}

>[!NOTE]
>
>카탈로그가 다음을 참조합니다. [제품 데이터](#products-and-product-variants).

1. 사용 **웹 사이트** 콘솔, 다음으로 이동 **카탈로그 블루프린트**&#x200B;를 클릭한 다음 기본 카탈로그를 클릭합니다.

   예:

   `http://localhost:4502/siteadmin#/content/catalogs/geometrixx-outdoors/base-catalog`

1. 를 사용하여 페이지 만들기 **섹션 블루프린트** 템플릿.

   예: `Swimwear`

1. 새 항목 열기 `Swimwear` 페이지를 클릭한 다음 **블루프린트 편집**. 다음 **속성** 대화 상자가 열리고 **제품** 선택 항목.

   예를 들어 **태그/키워드** 활동(Activity), 수영(Swimming) 순으로 선택할 필드입니다. Geometrixx-야외(Outdoors) 섹션.

1. 클릭 **확인** 속성을 저장합니다. 예제 제품은 **제품 선택 기준** 블루프린트 페이지에서 확인할 수 있습니다.
1. 클릭 **롤아웃 변경...**, 선택 **롤아웃 페이지 및 모든 하위 페이지**&#x200B;을 클릭한 다음 을 클릭합니다 **다음** 그러면 **롤아웃**. 롤아웃이 성공적으로 완료되면 **상태** 표시기가 녹색으로 표시됩니다.
1. 이제 다음을 클릭할 수 있습니다. **닫기** 새 카탈로그 섹션(예: on 및 under)을 확인합니다.

   `http://localhost:4502/cf#/content/geometrixx-outdoors/en/swimwear.html`

1. 다시 블루프린트 페이지에서 **블루프린트 편집** 및 **속성** 대화 상자 열기 **생성된 페이지** 탭. 배너 목록 필드에서 표시할 이미지를 선택합니다(예: ). `summer.jpg`
1. 클릭 **확인** 이렇게 하면 속성이 저장되고 배너 정보는 **제품 선택 기준** 블루프린트 페이지에서 확인할 수 있습니다.
1. 이러한 새 변경 사항을 롤아웃합니다.

### 카탈로그 롤아웃 {#rolling-out-a-catalog}

#### 카탈로그 롤아웃 - 터치에 적합한 UI {#rolling-out-a-catalog-touch-optimized-ui}

카탈로그를 롤아웃하려면 다음 작업을 수행하십시오.

1. 다음 위치로 이동 **카탈로그** 콘솔, 를 통해 **상거래**.
1. 롤아웃할 카탈로그로 이동합니다.
1. 다음 중 하나를 사용합니다.

   * [빠른 작업](/help/sites-authoring/basic-handling.md#quick-actions)
   * [선택 모드](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   다음 항목 선택 **롤아웃 변경 사항** 아이콘:

   ![롤아웃](/help/sites-administering/do-not-localize/chlimage_1-24.png)

1. 마법사에서 필요에 따라 롤아웃을 설정한 다음 탭/클릭합니다 **롤아웃 변경 사항**.
1. 대화 상자가 열립니다. 선택 **완료** 프로세스가 완료되면 발생합니다.

#### 카탈로그 롤아웃 - 클래식 UI {#rolling-out-a-catalog-classic-ui}

카탈로그를 롤아웃하려면 다음 작업을 수행하십시오.

1. 롤아웃할 카탈로그로 이동합니다. 예:

   `http://localhost:4502/cf#/content/catalogs/geometrixx-outdoors/base-catalog.html`

1. 클릭 **롤아웃 변경...**
1. 필요에 따라 롤아웃을 설정합니다.
1. 클릭 **롤아웃**.

### 블루프린트 가져오기 {#blueprint-importer}

#### 블루프린트 가져오기 - 터치에 적합한 UI {#blueprint-importer-touch-optimized-ui}

1. 다음 위치로 이동 **카탈로그** 콘솔, 를 통해 **상거래**.
1. 카탈로그 블루프린트를 가져올 위치로 이동합니다.
1. 다음 항목 선택 **블루프린트 가져오기** 아이콘.

   ![블루프린트 가져오기 아이콘](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. 마법사에서 필요에 따라 소스를 선택하고 탭/클릭합니다 **다음**.

   ![블루프린트 마법사](/help/sites-administering/assets/chlimage_1-102.png)

1. 선택 **완료** 가져오기가 완료되면.

#### 블루프린트 Importer - 클래식 UI {#blueprint-importer-classic-ui}

1. 사용 **도구** 콘솔, 다음으로 이동 **상거래**.

   예:

   `http://localhost:4502/miscadmin#/etc/commerce`

1. 를 엽니다. **Catalog Bluprint Importer**.
1. 필요에 따라 가져오기를 설정합니다.
1. 클릭 **카탈로그 블루프린트 가져오기**.

## 프로모션 {#promotions}

### 프로모션 생성 {#creating-a-promotion}

#### 프로모션 만들기 - 클래식 UI {#creating-a-promotion-classic-ui}

>[!NOTE]
>
>다음 예제에서는 에서 직접 보유하는 프로모션에 대해 다룹니다 [campaign](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md), 바우처에 사용됩니다.
>
>프로모션은에 있을 수도 있습니다. [경험](/help/sites-authoring/personalization.md) 캠페인에서.
>
>자세한 내용은 [프로모션 및 바우처](#promotions-and-vouchers).

1. 를 엽니다. **웹 사이트** 작성자 인스턴스의 콘솔.
1. 왼쪽 창에서 원하는 을 선택합니다 **캠페인**.
1. 클릭 **신규**&#x200B;를 선택하고 **프로모션** 템플릿을 선택한 다음 **제목** (및 **이름** 필요한 경우)를 사용하십시오.
1. **만들기**&#x200B;를 클릭합니다. 오른쪽 창에 새 프로모션 페이지가 표시됩니다.

1. 편집 **속성** 다음 중 하나를 통해:

   * 페이지를 연 다음 편집 단추를 클릭하여 속성 대화 상자를 엽니다
   * 웹 사이트 콘솔에서 페이지를 선택한 다음 컨텍스트 메뉴(일반적으로 오른쪽 마우스 버튼)를 사용하여 선택 **속성...** 속성 대화 상자를 엽니다

   다음을 지정합니다. **프로모션 유형**, **할인 유형**, **할인 값** 및 기타 모든 필드를 필요에 따라 추가합니다.

1. 클릭 **확인** 저장.

1. 이제 쇼퍼가 게시 인스턴스에서 볼 수 있도록 프로모션을 활성화할 수 있습니다.

## 바우처 {#vouchers}

### 바우처 만들기 {#creating-a-voucher}

#### 바우처 만들기 - 클래식 UI {#creating-a-voucher-classic-ui}

1. 를 엽니다. **웹 사이트** 작성자 인스턴스의 콘솔.
1. 왼쪽 창에서 원하는 을 선택합니다 **캠페인**.
1. 클릭 **신규**&#x200B;를 선택하고 **바우처** 템플릿을 선택한 다음 **제목** (및 **이름** 필요한 경우)를 사용하십시오.
1. **만들기**&#x200B;를 클릭합니다. 오른쪽 창에 새 바우처 페이지가 표시됩니다.

1. 두 번 클릭하여 새 바우처 페이지를 연 다음 **편집** 필요에 따라 정보를 구성합니다.
1. 클릭 **확인** 저장.

1. 이제 구매자가 게시 인스턴스의 카트에서 사용할 수 있도록 바우처를 활성화할 수 있습니다.

### 바우처 제거 {#removing-vouchers}

#### 바우처 제거 - 클래식 UI {#removing-vouchers-classic-ui}

고객이 바우처를 사용할 수 없도록 하려면 다음 중 하나를 수행할 수 있습니다.

* 바우처를 비활성화합니다. 나중에 다시 활성화할 수 있도록 작성자 환경에서 사용할 수 있습니다.
* 완전히 삭제하십시오.

두 작업은 다음 위치에서 수행할 수 있습니다. **웹 사이트** 콘솔.

### 바우처 수정 {#modifying-vouchers}

#### 바우처 수정 - 클래식 UI {#modifying-vouchers-classic-ui}

바우처나 프로모션의 속성을 변경하려면 **웹 사이트** 콘솔 및 클릭 **편집**. 저장한 후 변경 사항이 게시 인스턴스로 푸시되도록 활성화해야 합니다.

### 장바구니에 바우처 추가 {#adding-vouchers-to-a-cart}

사용자가 장바구니에 바우처를 추가할 수 있도록 하려면 기본 제공 기능을 사용합니다 **바우처** 구성 요소(상거래 범주). 장바구니가 표시되는 페이지와 동일한 페이지에 추가합니다(하지만 필수 페이지는 아님). 바우처 구성 요소는 사용자가 바우처 코드를 입력할 수 있는 형식일 뿐이며, 실제로 적용된 바우처 목록과 할인을 보여 주는 장바구니 구성 요소입니다.

데모 사이트(Geometrixx Outdoors - 영어)의 장바구니 페이지에 있는 실제 장바구니 아래의 바우처 양식을 볼 수 있습니다.

## 주문 {#orders}

>[!NOTE]
>
>즉시 사용 가능한 AEM에는 반품, 주문 상태 업데이트, 이행, 포장 명세서 생성과 같은 주문과 관련된 표준 기능에 필요한 작업이 없습니다. 주로 기술 미리보기 목적으로 사용됩니다.
>
>AEM의 일반 Order Management는 기본적으로 유지되므로 마법사에서 사용할 수 있는 필드는 스캐폴드에 따라 다릅니다.
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

1. 사용 **주문 수** 콘솔이 필요한 위치로 이동합니다.
1. 사용 **만들기** 선택할 아이콘 **주문 만들기**.

   ![플러스 모양 만들기 아이콘](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. 마법사가 열립니다. 사용 **기본**, **콘텐츠**, **결제**, 및 **이행** 탭 입력 [새 주문에 대한 정보](/help/commerce/cif-classic/administering/concepts.md#order-information).

1. 선택 **만들기** 을 클릭하여 정보를 저장합니다.

### 주문 정보 편집 {#editing-order-information}

#### 주문 정보 편집 - 터치에 적합한 UI {#editing-order-information-touch-optimized-ui}

1. 사용 **주문 수** 콘솔은 주문으로 이동합니다.
1. 다음 중 하나를 사용합니다.

   * [빠른 작업](/help/sites-authoring/basic-handling.md#quick-actions)
   * [선택 모드](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   다음 항목 선택 **주문 데이터 보기** 아이콘:

   ![정보 아이콘](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. 다음 [주문 정보](/help/commerce/cif-classic/administering/concepts.md#order-information) 이 표시됩니다. 사용 **편집** 및 **완료** 원하는 대로 변경할 수 있습니다.

