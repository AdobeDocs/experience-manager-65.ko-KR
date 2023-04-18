---
title: AEM과 SAP Commerce Cloud 사용
description: AEM과 SAP Commerce Cloud을 함께 사용하는 방법을 알아봅니다.
uuid: cee1a781-fcba-461e-a0a4-c561a1dbcbf3
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
exl-id: c342f789-2ff7-4802-99c7-c3699218fe47
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '1717'
ht-degree: 2%

---

# SAP Commerce Cloud{#sap-commerce-cloud}

설치 후 인스턴스를 구성할 수 있습니다.

1. [Geometrixx Outdoors에 대한 인증된 검색 구성](#configure-the-facetted-search-for-geometrixx-outdoors).
1. [카탈로그 버전 구성](#configure-the-catalog-version).
1. [가져오기 구조 구성](#configure-the-import-structure).
1. [로드할 제품 속성 구성](#configure-the-product-attributes-to-load).
1. [제품 데이터 가져오기](#importing-the-product-data).
1. [카탈로그 가져오기 구성](#configure-the-catalog-importer).
1. 를 사용하십시오 [카탈로그를 가져오기 위한 가져오기](#catalog-import) 를 AEM의 특정 위치에 배치합니다.

## Geometrixx Outdoors에 대한 인증된 검색 구성 {#configure-the-facetted-search-for-geometrixx-outdoors}

>[!NOTE]
>
>hybris 5.3.0.1 이상에는 필요하지 않습니다.

1. 브라우저에서 **hybris 관리 콘솔** at:

   [http://localhost:9001/hmc/hybris](http://localhost:9001/hmc/hybris)

1. 사이드바에서 **시스템**, 그런 다음 **패싯 검색**, 그런 다음 **패싯 검색 구성**.
1. **편집기 열기** 대상 **Clothescatalog에 대한 샘플 Solr 구성**.

1. 아래 **카탈로그 버전** 사용 **카탈로그 버전 추가** 를 추가하려면 `outdoors-Staged` 및 `outdoors-Online` 목록에 추가합니다.
1. **구성을 저장합니다.**
1. 열기 **SOLR 항목 유형** 를 추가하려면 **SOLR 정렬** to `ClothesVariantProduct`:

   * 관련성 (&quot;관련성&quot;, 점수)
   * name-asc(&quot;이름(오름차순)&quot;, 이름)
   * name-desc(&quot;이름(내림차순)&quot;, 이름)
   * price-asc(&quot;가격(오름차순)&quot;, priceValue)
   * price-desc(&quot;가격(내림차순)&quot;, priceValue)

   >[!NOTE]
   >
   >컨텍스트 메뉴(일반적으로 마우스 오른쪽 단추 클릭)를 사용하여 선택 `Create Solr sort`.
   >
   >Hybris 5.0.0의 경우 `Indexed Types` 탭에서 두 번 클릭합니다. `ClothesVariantProduct`를 입력한 다음 탭을 클릭합니다 `SOLR Sort`.

   ![chlimage_1-36](/help/sites-administering/assets/chlimage_1-36a.png)

1. 에서 **인덱싱된 유형** 탭 설정 **작성된 유형** 변환:

   `Product - Product`

1. 에서 **인덱싱된 유형** 탭 조정 **인덱서 쿼리** 대상 `full`:

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}})
   ```

1. 에서 **인덱싱된 유형** 탭 조정 **인덱서 쿼리** 대상 `incremental`:

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}}) AND {modifiedtime} <= ?lastIndexTime
   ```

1. 에서 **인덱싱된 유형** 탭 조정 `category` 패싯. 범주 목록의 마지막 항목을 두 번 클릭하여 **인덱싱된 속성** 탭:

   >[!NOTE]
   >
   >hybris 5.2의 경우 `Facet` 속성 테이블의 속성은 아래 스크린샷에 따라 선택됩니다.

   ![chlimage_1-37](/help/sites-administering/assets/chlimage_1-37a.png) ![chlimage_1-38](/help/sites-administering/assets/chlimage_1-38a.png)

1. 를 엽니다. **패싯 설정** 탭 및 필드 값 조정:

   ![chlimage_1-39](/help/sites-administering/assets/chlimage_1-39a.png)

1. **변경 사항을 저장합니다.**
1. 다음에서 다시 **SOLR 항목 유형**, 조정 `price` 패싯은 다음 스크린샷에 따라 다릅니다. 과 함께 `category`를 두 번 클릭합니다. `price` 열다 **인덱싱된 속성** 탭:

   ![chlimage_1-40](/help/sites-administering/assets/chlimage_1-40a.png)

1. 를 엽니다. **패싯 설정** 탭 및 필드 값 조정:

   ![chlimage_1-41](/help/sites-administering/assets/chlimage_1-41a.png)

1. **변경 사항을 저장합니다.**
1. 열기 **시스템**, **패싯 검색**, 그런 다음 **인덱서 작업 마법사**. cronjob 시작:

   * **색인 작업**: `full`
   * **솔루션 구성**: `Sample Solr Config for Clothes`

## 카탈로그 버전 구성 {#configure-the-catalog-version}

다음 **카탈로그 버전** ( `hybris.catalog.version`) OSGi 서비스에 대해 구성할 수 있습니다.

**Day CQ Commerce Hybris 구성**
( `com.adobe.cq.commerce.hybris.common.DefaultHybrisConfigurationService`)

**카탈로그 버전** 일반적으로 다음 중 하나로 설정됩니다. `Online` 또는 `Staged` (기본값)

>[!NOTE]
>
>AEM을 사용하여 작업하는 경우 이러한 서비스에 대한 구성 설정을 관리하는 방법에는 몇 가지가 있습니다. 참조 [OSGi 구성](/help/sites-deploying/configuring-osgi.md) 자세한 내용 구성 가능한 매개 변수와 그 기본값은 전체 목록이 필요하면 콘솔 을 참조하십시오.

로그 출력은 생성된 페이지 및 구성 요소에 대한 피드백을 제공하고 잠재적인 오류를 보고합니다.

## 가져오기 구조 구성 {#configure-the-import-structure}

다음 목록은 기본적으로 생성되는 샘플 구조(자산, 페이지 및 구성 요소)를 보여줍니다.

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

이러한 구조는 OSGi 서비스에 의해 만들어집니다 `DefaultImportHandler` 구현된 `ImportHandler` 인터페이스. 제품, 제품 변형, 카테고리, 자산 등을 만들기 위해 실제 가져오기에서 가져오기 처리기를 호출합니다.

>[!NOTE]
>
>다음을 수행할 수 있습니다 [고유한 가져오기 처리기를 구현하여 이 프로세스를 사용자 지정합니다](#configure-the-import-structure).

가져올 때 생성할 구조를 구성할 수 있습니다.

&quot;**일 CQ Commerce Hybris 기본 가져오기 처리기**
`(com.adobe.cq.commerce.hybris.importer.DefaultImportHandler`)

AEM을 사용하여 작업하는 경우 이러한 서비스에 대한 구성 설정을 관리하는 방법에는 몇 가지가 있습니다. 참조 [OSGi 구성](/help/sites-deploying/configuring-osgi.md) 자세한 내용 구성 가능한 매개 변수와 그 기본값은 전체 목록이 필요하면 콘솔 을 참조하십시오.

## 로드할 제품 속성 구성 {#configure-the-product-attributes-to-load}

응답 파서는 (변형) 제품에 로드할 속성과 속성을 정의하도록 구성할 수 있습니다.

1. OSGi 번들을 구성합니다.

   **Day CQ Commerce Hybris 기본 응답 파서**
(`com.adobe.cq.commerce.hybris.impl.importer.DefaultResponseParser`)

   여기에서 로드 및 매핑에 필요한 다양한 옵션과 속성을 정의할 수 있습니다.

   >[!NOTE]
   >
   >AEM을 사용하여 작업하는 경우 이러한 서비스에 대한 구성 설정을 관리하는 방법에는 몇 가지가 있습니다. 참조 [OSGi 구성](/help/sites-deploying/configuring-osgi.md) 자세한 내용 구성 가능한 매개 변수와 그 기본값은 전체 목록이 필요하면 콘솔 을 참조하십시오.

## 제품 데이터 가져오기 {#importing-the-product-data}

제품 데이터를 가져오는 방법은 다양합니다. 제품 데이터는 처음 환경을 설정할 때 또는 hybris 데이터에서 변경된 후에 가져올 수 있습니다.

* [전체 가져오기](#full-import)
* [증분 가져오기](#incremental-import)
* [빠른 업데이트](#express-update)

hybris에서 가져온 실제 제품 정보는 다음 보관소에 보관됩니다.

`/etc/commerce/products`

다음 속성은 hybris가 있는 링크를 나타냅니다.

* `commerceProvider`
* `cq:hybrisCatalogId`
* `cq:hybrisProductID`

>[!NOTE]
>
>hybris 구현(즉, `geometrixx-outdoors/en_US`)에는 제품 ID 및 기타 기본 정보만 `/etc/commerce`.
>
>제품에 대한 정보가 요청될 때마다 hybris 서버가 참조됩니다.

### 전체 가져오기 {#full-import}

1. 필요한 경우 CRXDE Lite을 사용하여 기존 제품 데이터를 모두 삭제합니다.

   1. 제품 데이터를 포함하는 하위 트리로 이동합니다.

      `/etc/commerce/products`

      예:

      [`http://localhost:4502/crx/de/index.jsp#/etc/commerce/products`](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

   1. 제품 데이터를 포함하는 노드를 삭제합니다. 예 `outdoors`.
   1. **모두 저장** 변경 사항을 유지하려면

1. AEM에서 hybris 가져오기를 엽니다.

   `/etc/importers/hybris.html`

   예:

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. 필요한 매개 변수를 구성합니다. 예:

   ![chlimage_1-42](/help/sites-administering/assets/chlimage_1-42a.png)

1. 클릭 **카탈로그 가져오기** 가져오기를 시작하려면 다음을 수행하십시오.

   완료되면 다음 위치에서 가져온 데이터를 확인할 수 있습니다.

   ```
       /etc/commerce/products/outdoors
   ```

   CRXDE Lite에서 열 수 있습니다. 예:

   `[http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)`

### 증분 가져오기 {#incremental-import}

1. 아래의 해당 하위 트리에서 관련 제품에 대해 AEM에 저장된 정보를 확인하십시오.

   `/etc/commerce/products`

   CRXDE Lite에서 열 수 있습니다. 예:

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. hybris에서 잔잔한 제품에 담긴 정보를 업데이트합니다.

1. AEM에서 hybris 가져오기를 엽니다.

   `/etc/importers/hybris.html`

   예:

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. 클릭 상자를 선택합니다 **증분 가져오기**.
1. 클릭 **카탈로그 가져오기** 가져오기를 시작하려면 다음을 수행하십시오.

   완료되면 다음 위치에서 AEM에서 업데이트된 데이터를 확인할 수 있습니다.

   ```
       /etc/commerce/products
   ```


### 빠른 업데이트 {#express-update}

가져오기 프로세스는 시간이 오래 걸릴 수 있으므로 제품 동기화에 대한 확장으로 수동으로 트리거되는 빠른 업데이트를 위해 카탈로그의 특정 영역을 선택할 수 있습니다. 여기서는 표준 특성 구성과 함께 내보내기 피드를 사용합니다.

1. 아래의 해당 하위 트리에서 관련 제품에 대해 AEM에 저장된 정보를 확인하십시오.

   `/etc/commerce/products`

   CRXDE Lite에서 열 수 있습니다. 예:

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. hybris에서 잔잔한 제품에 담긴 정보를 업데이트합니다.

1. hybris에서 Express Queue에 제품을 추가합니다. 예:

   ![chlimage_1-43](/help/sites-administering/assets/chlimage_1-43a.png)

1. AEM에서 hybris 가져오기를 엽니다.

   `/etc/importers/hybris.html`

   예:

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. 클릭 상자를 선택합니다 **빠른 업데이트**.
1. 클릭 **카탈로그 가져오기** 가져오기를 시작하려면 다음을 수행하십시오.

   완료되면 다음 위치에서 AEM에서 업데이트된 데이터를 확인할 수 있습니다.

   ```
       /etc/commerce/products
   ```

## 카탈로그 가져오기 구성 {#configure-the-catalog-importer}

hybris 카탈로그를 Hybris 카탈로그, 카테고리 및 제품에 대한 배치 가져오기를 사용하여 AEM으로 가져올 수 있습니다.

가져오기에서 사용하는 매개 변수는 다음과 같은 경우에 구성할 수 있습니다.

**Day CQ Commerce Hybris 카탈로그 가져오기**
( `com.adobe.cq.commerce.hybris.impl.importer.DefaultHybrisImporter`)

AEM을 사용하여 작업하는 경우 이러한 서비스에 대한 구성 설정을 관리하는 방법에는 몇 가지가 있습니다. 참조 [OSGi 구성](/help/sites-deploying/configuring-osgi.md) 자세한 내용 구성 가능한 매개 변수와 그 기본값은 전체 목록이 필요하면 콘솔 을 참조하십시오.

## 카탈로그 가져오기 {#catalog-import}

hybris 패키지에는 초기 페이지 구조를 설정하기 위한 카탈로그 가져오기가 포함되어 있습니다.

다음 제품에서 사용할 수 있습니다.

`http://localhost:4502/etc/importers/hybris.html`

![ecommerceimportconsole](/help/sites-administering/assets/ecommerceimportconsole.png)

다음 정보를 제공해야 합니다.

* **기본 스토어**
hybris에 구성된 기본 저장소의 식별자입니다.

* **카탈로그**
가져올 카탈로그의 식별자입니다.

* **루트 경로**
카탈로그를 가져와야 하는 경로입니다.

## 카탈로그에서 제품 제거 {#removing-a-product-from-the-catalog}

카탈로그에서 하나 이상의 제품을 제거하려면

1. [OSGi 서비스에 대한 를 구성합니다](/help/sites-deploying/configuring-osgi.md) **Day CQ Commerce Hybris 카탈로그 가져오기**; 참조 [카탈로그 가져오기 구성](#configure-the-catalog-importer).

   다음 속성을 활성화합니다.

   * **제품 제거 활성화**
   * **제품 자산 제거 활성화**

   >[!NOTE]
   >
   >AEM을 사용하여 작업하는 경우 이러한 서비스에 대한 구성 설정을 관리하는 방법에는 몇 가지가 있습니다. 참조 [OSGi 구성](/help/sites-deploying/configuring-osgi.md) 자세한 내용 구성 가능한 매개 변수와 그 기본값은 전체 목록이 필요하면 콘솔 을 참조하십시오.

1. 두 개의 증분 업데이트를 수행하여 가져오기를 초기화합니다( [카탈로그 가져오기](#catalog-import)):

   * 첫 번째 실행은 변경된 제품 세트가 발생하며 로그 목록에 표시됩니다.
   * 두 번째로 제품을 업데이트하지 않아야 합니다.

   >[!NOTE]
   >
   >첫 번째 가져오기는 제품 정보를 초기화하는 것입니다. 두 번째 가져오기는 모든 작업이 작동되고 이 제품 세트가 준비되었는지 확인합니다.

1. 제거할 제품이 포함된 카테고리 페이지를 확인합니다. 제품 세부 사항이 표시됩니다.

   예를 들어 다음 카테고리는 Cajamara 제품에 대한 세부 정보를 보여줍니다.

   [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

1. hybris 콘솔에서 제품을 제거합니다. 옵션을 사용합니다 **승인 상태 변경** 상태를 로 설정하려면 `unapproved`. 제품이 라이브 피드에서 제거됩니다.

   예:

   * 페이지를 엽니다. [http://localhost:9001/productcockpit](http://localhost:9001/productcockpit)
   * 카탈로그를 선택합니다 `Outdoors Staged`
   * 검색 대상 `Cajamara`
   * 이 제품을 선택하고 승인 상태를 로 변경합니다. `unapproved`

1. 다른 증분 업데이트 수행( [카탈로그 가져오기](#catalog-import)). 로그에 삭제된 제품이 나열됩니다.
1. [롤아웃](/help/commerce/cif-classic/administering/generic.md#rolling-out-a-catalog) 적절한 카탈로그 제품 및 제품 페이지가 AEM 내에서 제거되었습니다.

   예:

   * 열기:

      [http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris](http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris)

   * 롤아웃 `Hybris Base` 카탈로그
   * 열기:

      [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

   * 다음 `Cajamara` 제품이 `Bike` 카테고리

1. 제품을 다시 설치하려면

   1. hybris에서 승인 상태를 다시 로 설정합니다. **승인됨**
   1. AEM에서:

      1. 증분 업데이트 수행
      1. 적절한 카탈로그를 다시 롤아웃
      1. 적절한 카테고리 페이지 새로 고침

## Client Context에 주문 내역 특성 추가 {#add-order-history-trait-to-the-client-context}

주문 내역을 [클라이언트 컨텍스트](/help/sites-developing/client-context.md):

1. 를 엽니다. [클라이언트 컨텍스트 디자인 페이지](/help/sites-administering/client-context.md)다음 방법 중 하나로 묶습니다.

   * 편집할 페이지를 연 다음 **Ctrl-Alt-c** (windows) 또는 **control-option-c** (Mac). 클라이언트 컨텍스트의 왼쪽 위 모서리에 있는 연필 아이콘을 사용하여 다음을 수행할 수 있습니다 **ClientContext 디자인 페이지를 엽니다.**.
   * 로 바로 이동 [http://localhost:4502/etc/clientcontext/default/content.html](http://localhost:4502/etc/clientcontext/default/content.html)

1. [추가 **주문 내역** 구성 요소](/help/sites-administering/client-context.md#adding-a-property-component) 변환 후 **쇼핑 카**&#x200B;클라이언트 컨텍스트의 구성 요소입니다.
1. Client Context가 주문 내역에 대한 세부 사항을 표시하는지 확인할 수 있습니다. 예:

   1. 를 엽니다. [클라이언트 컨텍스트](/help/sites-administering/client-context.md).
   1. 장바구니에 항목을 추가합니다.
   1. 체크아웃을 완료합니다.
   1. 클라이언트 컨텍스트를 확인합니다.
   1. 장바구니에 다른 항목을 추가합니다.
   1. 체크아웃 페이지로 이동합니다.

      * 클라이언트 컨텍스트는 주문 내역의 요약을 표시합니다.
      * &quot;재방문 고객입니다&quot;라는 메시지가 표시됩니다.

   >[!NOTE]
   >
   >메시지는 다음 방법으로 실현됩니다.
   >
   >* 다음으로 이동 [http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html](http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html)
   >
   >  캠페인은 한 개의 경험으로 구성됩니다.
   >
   >* 세그먼트를 클릭합니다([http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html](http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html))
   >
   >* 세그먼트는 **주문 내역 속성** 트레이트.

