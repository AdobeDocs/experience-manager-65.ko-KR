---
title: SAP와 함께 AEM 사용 Commerce Cloud
description: SAP Commerce Cloud과 함께 Adobe Experience Manager을 사용하는 방법을 알아봅니다.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
exl-id: c342f789-2ff7-4802-99c7-c3699218fe47
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '1574'
ht-degree: 2%

---

# SAP COMMERCE CLOUD{#sap-commerce-cloud}

설치 후 인스턴스를 구성할 수 있습니다.

1. [Geometrixx Outdoors에 대한 패싯된 검색을 구성](#configure-the-facetted-search-for-geometrixx-outdoors)합니다.
1. [카탈로그 버전을 구성](#configure-the-catalog-version)합니다.
1. [가져오기 구조를 구성합니다](#configure-the-import-structure).
1. [로드할 제품 특성을 구성하십시오](#configure-the-product-attributes-to-load).
1. [제품 데이터를 가져오는 중](#importing-the-product-data).
1. [카탈로그 가져오기를 구성합니다](#configure-the-catalog-importer).
1. [가져오기를 사용하여 &#x200B;](#catalog-import) 카탈로그를 AEM의 특정 위치로 가져옵니다.

## Geometrixx Outdoors에 대한 면처리 검색 구성 {#configure-the-facetted-search-for-geometrixx-outdoors}

>[!NOTE]
>
>hybris 5.3.0.1 이상에서는 필요하지 않습니다.

1. 브라우저에서 다음 위치의 **하이브리드 관리 콘솔**(으)로 이동합니다.

   [http://localhost:9001/hmc/hybris](http://localhost:9001/hmc/hybris)

1. 사이드바에서 **시스템**, **패싯 검색**, **패싯 검색 구성**&#x200B;을 선택하십시오.
1. **clothescatalog에 대한 샘플 Solr 구성**&#x200B;에 대해 **편집기 열기**&#x200B;를 참조하십시오.

1. **카탈로그 버전**&#x200B;에서 **카탈로그 버전 추가**&#x200B;를 사용하여 `outdoors-Staged` 및 `outdoors-Online`을(를) 목록에 추가합니다.
1. 구성을 **저장**&#x200B;합니다.
1. `ClothesVariantProduct`에 **SOLR 정렬**&#x200B;을(를) 추가하려면 **SOLR 항목 형식**&#x200B;을 여십시오.

   * 관련성(&quot;관련성&quot;, 점수)
   * name-asc (&quot;Name (ascending)&quot;, name)
   * name-desc (&quot;이름(내림차순)&quot;, 이름)
   * price-asc(&quot;가격(오름차순)&quot;, priceValue)
   * price-desc(&quot;가격(내림차순)&quot;, priceValue)

   >[!NOTE]
   >
   >컨텍스트 메뉴(보통 마우스 오른쪽 단추 클릭)를 사용하여 `Create Solr sort`을(를) 선택합니다.
   >
   >Hybris 5.0.0의 경우 `Indexed Types` 탭을 열고 `ClothesVariantProduct`을(를) 두 번 클릭한 다음 `SOLR Sort` 탭을 클릭합니다.

   ![chlimage_1-36](/help/sites-administering/assets/chlimage_1-36a.png)

1. **인덱싱된 형식** 탭에서 **작성된 형식**&#x200B;을(를) 다음으로 설정합니다.

   `Product - Product`

1. **인덱싱된 형식** 탭에서 `full`에 대한 **인덱서 쿼리**&#x200B;를 조정하십시오.

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}})
   ```

1. **인덱싱된 형식** 탭에서 `incremental`에 대한 **인덱서 쿼리**&#x200B;를 조정하십시오.

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}}) AND {modifiedtime} <= ?lastIndexTime
   ```

1. **인덱싱된 형식** 탭에서 `category` 패싯을 조정합니다. 범주 목록의 마지막 항목을 두 번 클릭하여 **인덱싱된 속성** 탭을 엽니다.

   >[!NOTE]
   >
   >hybris 5.2의 경우 아래 스크린샷에 따라 속성 테이블의 `Facet` 특성이 선택되어 있는지 확인하십시오.

   ![chlimage_1-37](/help/sites-administering/assets/chlimage_1-37a.png) ![chlimage_1-38](/help/sites-administering/assets/chlimage_1-38a.png)

1. **Facet 설정** 탭을 열고 필드 값을 조정합니다.

   ![chlimage_1-39](/help/sites-administering/assets/chlimage_1-39a.png)

1. 변경 내용을 **저장**&#x200B;합니다.
1. **SOLR 항목 형식**&#x200B;에서 다시 다음 스크린샷에 따라 `price` 패싯을 조정하십시오. `category`과(와) 마찬가지로 `price`을(를) 두 번 클릭하여 **인덱싱된 속성** 탭을 엽니다.

   ![chlimage_1-40](/help/sites-administering/assets/chlimage_1-40a.png)

1. **Facet 설정** 탭을 열고 필드 값을 조정합니다.

   ![chlimage_1-41](/help/sites-administering/assets/chlimage_1-41a.png)

1. 변경 내용을 **저장**&#x200B;합니다.
1. **시스템**, **패싯 검색**&#x200B;을 연 다음 **인덱서 작업 마법사**&#x200B;를 엽니다. cronjob 시작:

   * **인덱서 작업**: `full`
   * **Solr 구성**: `Sample Solr Config for Clothes`

## 카탈로그 버전 구성 {#configure-the-catalog-version}

가져온 **카탈로그 버전**(`hybris.catalog.version`)은(는) OSGi 서비스에 대해 구성할 수 있습니다.

**일 CQ Commerce Hybris 구성**
( `com.adobe.cq.commerce.hybris.common.DefaultHybrisConfigurationService`)

**카탈로그 버전**&#x200B;이(가) `Online` 또는 `Staged`(기본값)으로 설정되어 있습니다.

>[!NOTE]
>
>AEM을 사용하여 작업할 때 이러한 서비스에 대한 구성 설정을 관리할 수 있는 방법에는 몇 가지가 있습니다. 자세한 내용은 [OSGi 구성](/help/sites-deploying/configuring-osgi.md)을 참조하십시오. 또한 구성 가능한 매개 변수와 해당 기본값의 전체 목록이 필요하면 콘솔을 참조하십시오.

로그 출력은 생성된 페이지 및 구성 요소에 대한 피드백을 제공하며 잠재적인 오류를 보고합니다.

## 가져오기 구조 구성 {#configure-the-import-structure}

다음 목록은 기본적으로 생성되는 (에셋, 페이지 및 구성 요소의) 샘플 구조를 보여 줍니다.

```shell
+ /content/dam/path/to/images
  + 12345.jpg (dam:Asset)
    + ...
  + ...
+ /content/site/en
  - cq:commerceProvider = "hybris"
  - cq:hybrisBaseStore = "basestore"
  - cq:hybrisCatalogId = "catalog"
  + category1 (cq:Page)
    + jcr:content (cq:PageContent)
      - jcr:title = "Category 1"
    + category11 (cq:Page)
      + jcr:content (cq:PageContent)
        - jcr:title = "Category 1.1"
      + 12345 (cq:Page)
        + jcr:content (cq:PageContent)
          + par
            + product (nt:unstructured)
              - cq:hybrisProductId = "12345"
              - sling:resourceType = "commerce/components/product"
              + image (nt:unstructured)
                - sling:resourceType = "commerce/components/product/image"
                - fileReference = "/content/dam/path/to/images/12345.jpg"
              + 12345.1-S (nt:unstructured)
                - cq:hybrisProductId = "12345.1-S"
                - sling:resourceType = "commerce/components/product"
                + image (nt:unstructured)
                  - sling:resourceType = "commerce/components/product/image"
                  - fileReference = "/content/dam/path/to/images/12345.1-S.jpg"
              + ...
```

이러한 구조는 `ImportHandler` 인터페이스를 구현하는 OSGi 서비스 `DefaultImportHandler`에 의해 만들어집니다. 실제 가져오기는 가져오기 핸들러를 호출하여 제품, 제품 변형, 카테고리, 에셋 등을 만듭니다.

>[!NOTE]
>
>[자신의 가져오기 처리기를 구현하여 이 프로세스를 사용자 지정할 수 있습니다](#configure-the-import-structure).

가져올 때 생성될 구조는 다음에 대해 구성할 수 있습니다.

&quot;**일 CQ Commerce Hybris 기본 가져오기 처리기**
`(com.adobe.cq.commerce.hybris.importer.DefaultImportHandler`)

AEM을 사용하여 작업할 때 이러한 서비스에 대한 구성 설정을 관리할 수 있는 방법에는 몇 가지가 있습니다. 자세한 내용은 [OSGi 구성](/help/sites-deploying/configuring-osgi.md)을 참조하십시오. 또한 구성 가능한 매개 변수와 해당 기본값의 전체 목록이 필요하면 콘솔을 참조하십시오.

## 로드할 제품 속성 구성 {#configure-the-product-attributes-to-load}

(변형) 제품에 대해 로드할 속성 및 속성을 정의하도록 응답 파서를 구성할 수 있습니다.

1. OSGi 번들을 구성합니다.

   **일 CQ Commerce Hybris 기본 응답 파서**
(`com.adobe.cq.commerce.hybris.impl.importer.DefaultResponseParser`)

   여기에서 로드 및 매핑에 필요한 다양한 옵션과 속성을 정의할 수 있습니다.

   >[!NOTE]
   >
   >AEM을 사용하여 작업할 때 이러한 서비스에 대한 구성 설정을 관리할 수 있는 방법에는 몇 가지가 있습니다. 자세한 내용은 [OSGi 구성](/help/sites-deploying/configuring-osgi.md)을 참조하십시오. 또한 구성 가능한 매개 변수와 해당 기본값의 전체 목록이 필요하면 콘솔을 참조하십시오.

## 제품 데이터 가져오기 {#importing-the-product-data}

제품 데이터를 가져오는 방법에는 여러 가지가 있습니다. 처음 환경을 설정할 때 또는 hybris 데이터가 변경된 후에 제품 데이터를 가져올 수 있습니다.

* [전체 가져오기](#full-import)
* [증분 가져오기](#incremental-import)
* [빠른 업데이트](#express-update)

hybris에서 가져온 실제 제품 정보는 다음 저장소의 저장소에 보관됩니다.

`/etc/commerce/products`

다음 속성은 hybris와의 링크를 나타냅니다.

* `commerceProvider`
* `cq:hybrisCatalogId`
* `cq:hybrisProductID`

>[!NOTE]
>
>hybris 구현(즉, `geometrixx-outdoors/en_US`)은 `/etc/commerce`에 제품 ID와 기타 기본 정보만 저장합니다.
>
>하이브리드 서버는 제품에 대한 정보가 요청될 때마다 참조됩니다.

### 전체 가져오기 {#full-import}

1. 필요한 경우 CRXDE Lite을 사용하여 기존 제품 데이터를 모두 삭제합니다.

   1. 제품 데이터를 포함하는 하위 트리로 이동합니다.

      `/etc/commerce/products`

      예:

      [`http://localhost:4502/crx/de/index.jsp#/etc/commerce/products`](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

   1. 제품 데이터가 들어 있는 노드를 삭제합니다(예: `outdoors`).
   1. 변경 내용을 유지하려면 **모두 저장**&#x200B;하세요.

1. AEM에서 hybris importer를 엽니다.

   `/etc/importers/hybris.html`

   예:

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. 필요한 매개 변수를 구성합니다. 예를 들면 다음과 같습니다.

   ![chlimage_1-42](/help/sites-administering/assets/chlimage_1-42a.png)

1. 가져오기를 시작하려면 **카탈로그 가져오기**&#x200B;를 클릭하세요.

   완료되면 가져온 데이터를 확인할 수 있습니다.

   ```
       /etc/commerce/products/outdoors
   ```

   CRXDE Lite에서 열 수 있습니다. 예를 들면 다음과 같습니다.

   `[http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)`

### 증분 가져오기 {#incremental-import}

1. 아래의 해당 하위 트리에서 AEM에 있는 관련 제품 정보를 확인하십시오.

   `/etc/commerce/products`

   CRXDE Lite에서 열 수 있습니다. 예를 들면 다음과 같습니다.

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. hybris에서 관련 제품에 대한 정보를 업데이트합니다.

1. AEM에서 hybris importer를 엽니다.

   `/etc/importers/hybris.html`

   예:

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. **증분 가져오기** 확인란을 선택합니다.
1. 가져오기를 시작하려면 **카탈로그 가져오기**&#x200B;를 클릭하세요.

   완료되면 아래 AEM에서 업데이트된 데이터를 확인할 수 있습니다.

   ```
       /etc/commerce/products
   ```


### 빠른 업데이트 {#express-update}

가져오기 프로세스에 시간이 오래 걸릴 수 있으므로 제품 동기화 를 확장하여 수동으로 트리거되는 빠른 업데이트에 대해 카탈로그의 특정 영역을 선택할 수 있습니다. 표준 속성 구성과 함께 내보내기 피드를 사용합니다.

1. 아래의 해당 하위 트리에서 AEM에 있는 관련 제품 정보를 확인하십시오.

   `/etc/commerce/products`

   CRXDE Lite에서 열 수 있습니다. 예를 들면 다음과 같습니다.

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. hybris에서 관련 제품에 대한 정보를 업데이트합니다.

1. hybris에서 Express Queue에 하나 이상의 제품을 추가합니다. 예를 들면 다음과 같습니다.

   ![chlimage_1-43](/help/sites-administering/assets/chlimage_1-43a.png)

1. AEM에서 hybris importer를 엽니다.

   `/etc/importers/hybris.html`

   예:

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. **빠른 업데이트** 확인란을 선택하십시오.
1. 가져오기를 시작하려면 **카탈로그 가져오기**&#x200B;를 클릭하세요.

   완료되면 아래 AEM에서 업데이트된 데이터를 확인할 수 있습니다.

   ```
       /etc/commerce/products
   ```

## 카탈로그 Importer 구성 {#configure-the-catalog-importer}

hybris 카탈로그는 hybris 카탈로그, 범주 및 제품에 대한 배치 가져오기를 사용하여 AEM으로 가져올 수 있습니다.

가져오기에서 사용하는 매개 변수는 다음에 대해 구성할 수 있습니다.

**일 CQ Commerce Hybris 카탈로그 가져오기**
( `com.adobe.cq.commerce.hybris.impl.importer.DefaultHybrisImporter`)

AEM을 사용하여 작업할 때 이러한 서비스에 대한 구성 설정을 관리할 수 있는 방법에는 몇 가지가 있습니다. 자세한 내용은 [OSGi 구성](/help/sites-deploying/configuring-osgi.md)을 참조하십시오. 또한 구성 가능한 매개 변수와 해당 기본값의 전체 목록이 필요하면 콘솔을 참조하십시오.

## 카탈로그 가져오기 {#catalog-import}

hybris 패키지에는 초기 페이지 구조를 설정하는 카탈로그 임포터가 제공됩니다.

다음에서 사용할 수 있습니다.

`http://localhost:4502/etc/importers/hybris.html`

![ecommerceimportconsole](/help/sites-administering/assets/ecommerceimportconsole.png)

다음 정보를 제공해야 합니다.

* **기본 저장소**
hybris에 구성된 기본 저장소의 식별자입니다.

* **카탈로그**
가져올 카탈로그의 식별자입니다.

* **루트 경로**
카탈로그를 가져올 경로입니다.

## 카탈로그에서 제품 제거 {#removing-a-product-from-the-catalog}

카탈로그에서 하나 이상의 제품을 제거하려면 다음 작업을 수행하십시오.

1. [OSGi 서비스에 대한 을(를) 구성합니다](/help/sites-deploying/configuring-osgi.md) **일 CQ Commerce Hybris 카탈로그 가져오기**. [카탈로그 가져오기 구성](#configure-the-catalog-importer)도 참조하십시오.

   다음 속성을 활성화합니다.

   * **제품 제거 사용**
   * **제품 자산 제거 사용**

   >[!NOTE]
   >
   >AEM을 사용하여 작업할 때 이러한 서비스에 대한 구성 설정을 관리할 수 있는 방법에는 몇 가지가 있습니다. 자세한 내용은 [OSGi 구성](/help/sites-deploying/configuring-osgi.md)을 참조하십시오. 또한 구성 가능한 매개 변수와 해당 기본값의 전체 목록이 필요하면 콘솔을 참조하십시오.

1. 두 번의 증분 업데이트를 수행하여 가져오기를 초기화합니다([카탈로그 가져오기](#catalog-import) 참조).

   * 처음 실행하면 변경된 제품 세트가 로그 목록에 표시됩니다.
   * 두 번째로, 어떤 제품도 업데이트해서는 안 됩니다.

   >[!NOTE]
   >
   >첫 번째 가져오기는 제품 정보를 초기화하는 것입니다. 두 번째 가져오기는 모든 것이 작동했으며 은(는) 제품 세트가 준비되었는지 확인합니다.

1. 제거할 제품이 포함된 범주 페이지를 확인합니다. 제품 세부 사항이 표시됩니다.

   예를 들어, 다음 카테고리는 Cajamara 제품에 대한 세부 정보를 보여줍니다.

   [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

1. hybris 콘솔에서 제품을 제거합니다. **승인 상태 변경** 옵션을 사용하여 상태를 `unapproved`(으)로 설정하십시오. 제품이 라이브 피드에서 제거됩니다.

   예:

   * [http://localhost:9001/productcockpit](http://localhost:9001/productcockpit) 페이지 열기
   * 카탈로그 `Outdoors Staged` 선택
   * `Cajamara` 검색
   * 이 제품을 선택하고 승인 상태를 `unapproved`(으)로 변경합니다.

1. 다른 증분 업데이트를 수행합니다([카탈로그 가져오기](#catalog-import) 참조). 로그에는 삭제된 제품이 나열됩니다.
1. 적절한 카탈로그를 [롤아웃](/help/commerce/cif-classic/administering/generic.md#rolling-out-a-catalog)합니다. 제품 및 제품 페이지가 AEM 내에서 제거되었습니다.

   예:

   * 열기:

     [http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris](http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris)

   * `Hybris Base` 카탈로그 롤아웃
   * 열기:

     [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

   * `Cajamara` 제품이 `Bike` 범주에서 제거되었습니다.

1. 제품을 복원하려면 다음을 수행하십시오.

   1. hybris에서 승인 상태를 **승인됨**(으)로 다시 설정합니다.
   1. AEM:

      1. 증분 업데이트 수행
      1. 해당 카탈로그 다시 롤아웃
      1. 해당 범주 페이지 새로 고침

## 클라이언트 컨텍스트에 주문 내역 트레이트 추가 {#add-order-history-trait-to-the-client-context}

[클라이언트 컨텍스트](/help/sites-developing/client-context.md)에 주문 내역을 추가하려면:

1. 다음 방법 중 하나를 사용하여 [클라이언트 컨텍스트 디자인 페이지](/help/sites-administering/client-context.md)를 엽니다.

   * 편집할 페이지를 연 다음 **Ctrl-Alt-c**(windows) 또는 **control-option-c**(Mac)을 사용하여 클라이언트 컨텍스트를 엽니다. 클라이언트 컨텍스트의 왼쪽 상단 모서리에 있는 연필 아이콘을 사용하여 **ClientContext 디자인 페이지를 엽니다**.
   * [http://localhost:4502/etc/clientcontext/default/content.html](http://localhost:4502/etc/clientcontext/default/content.html)(으)로 직접 이동

1. [클라이언트 컨텍스트의 **Shopping Car** t 구성 요소에 **주문 내역** 구성 요소 추가](/help/sites-administering/client-context.md#adding-a-property-component).
1. Client Context에 주문 내역의 세부 사항이 표시되는지 확인할 수 있습니다. 예:

   1. [클라이언트 컨텍스트](/help/sites-administering/client-context.md)를 엽니다.
   1. 장바구니에 항목을 추가합니다.
   1. 체크아웃을 완료합니다.
   1. 클라이언트 컨텍스트를 확인합니다.
   1. 장바구니에 다른 항목을 추가합니다.
   1. 체크아웃 페이지로 이동합니다.

      * Client Context에는 주문 내역의 요약이 표시됩니다.
      * &quot;재방문 고객입니다&quot;라는 메시지가 표시됩니다.

   >[!NOTE]
   >
   >이 메시지는 다음 방법으로 실현됩니다.
   >
   >* [http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html](http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html)(으)로 이동
   >
   >  이 캠페인은 하나의 경험으로 구성됩니다.
   >
   >* 세그먼트([http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html](http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html))를 클릭합니다
   >
   >* 세그먼트는 **주문 내역 속성** 특성을 사용하여 작성됩니다.
