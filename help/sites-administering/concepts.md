---
title: 개념
seo-title: 개념
description: AEM을 사용한 e커머스 일반 개념.
seo-description: AEM을 사용한 e커머스 일반 개념.
uuid: 9a4cc154-d82b-43e0-a66c-3edf059e8b75
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: e-commerce
content-type: reference
discoiquuid: 6d595c46-b04e-400b-a014-fbecd2010f5f
docset: aem65
translation-type: tm+mt
source-git-commit: 69dfd6b41b32cb9131fd90fd7039a0c224889db5

---


# 개념{#concepts}

통합 프레임워크는 다음 작업을 위한 메커니즘과 구성 요소를 제공합니다.

* eCommerce 엔진에 연결
* aem에 데이터 가져오기
* 해당 데이터 표시 및 구매자의 응답 수집
* 트랜잭션 상세내역 반환
* 두 시스템의 데이터 검색

즉,

* 쇼핑객들은 기다리지 않고 등록 및 쇼핑을 할 수 있습니다.
* 가격 변경은 지체 없이 쇼핑객들이 볼 수 있을 것이다.
* 필요에 따라 제품을 추가할 수 있습니다.

>[!NOTE]
>
>eCommerce 프레임워크는 다음과 함께 사용할 수 있습니다.
>
>* [마젠토](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md)
>* [SAP Commerce Cloud](/help/sites-administering/sap-commerce-cloud.md)
>* [Salesforce Commerce Cloud](https://github.com/adobe/commerce-salesforce)
>



>[!CAUTION]
>
>eCommerce [통합 프레임워크는](https://www.adobe.com/solutions/web-experience-management/commerce.html) AEM Add-On입니다.
>
>해당 엔진에 따라 영업 담당자가 자세한 내용을 제공할 수 있습니다.

>[!CAUTION]
>
>프레임워크는 프로젝트에 대한 기본 요구 사항을 제공합니다.
>
>특정 양의 개발 작업은 항상 프레임워크를 사양에 맞게 수정해야 합니다.

>[!CAUTION]
>
>표준 AEM 설치에는 일반 AEM(JCR) 전자 상거래 구현이 포함됩니다.
>
>이것은 현재 데모용이거나 사용자의 요구 사항에 따라 사용자 정의 구현을 위한 기본 토대가 되었습니다.

작업을 최적화하기 위해 AEM과 eCommerce 엔진 모두 고유한 전문 분야에 집중합니다. 두 사람 사이에 실시간으로 정보가 전송됩니다.예를 들면 다음과 같습니다.

* AEM은 다음을 수행할 수 있습니다.

   * 요청:

      * 전자 상거래 엔진의 제품 정보.
   * 제공:

      * 사용자 보기 - 제품 정보, 장바구니 및 체크아웃을 참조하십시오.
      * 장바구니 및 체크아웃 정보를 eCommerce 엔진에 제공합니다.
      * 검색 엔진 최적화(SEO 파섹
      * 커뮤니티 기능을 참조하십시오.
      * 비정형 마케팅 상호 작용


* eCommerce 엔진은 다음을 수행할 수 있습니다.

   * 제공:

      * 데이터베이스의 제품 정보.
      * 제품 변형 관리
      * 주문 관리.
      * ERP(Enterprise Resource Planning).
      * 제품 정보 내에서 검색합니다.
   * 프로세스:

      * 장바구니
      * 결제.
      * 주문 처리.


>[!NOTE]
>
>정확한 세부 사항은 eCommerce 엔진 및 프로젝트 구현에 따라 다릅니다.

통합 레이어를 사용할 수 있도록 많은 기본 AEM 구성 요소가 제공됩니다. 현재 다음과 같습니다.

* 제품 정보
* 장바구니
* 체크아웃
* 내 계정

다양한 검색 옵션을 사용할 수도 있습니다.

## 아키텍처 {#architecture}

통합 프레임워크는 기능을 설명하기 위한 다양한 구성 요소 및 연결 방법의 예를 제공하기 위한 여러 확장 기능인 API를 제공합니다.

![chlimage_1-4](assets/chlimage_1-4.png)

프레임워크에서는 다음과 같은 기능을 이용할 수 있습니다.

![chlimage_1-5](assets/chlimage_1-5.png)

### 구현 {#implementations}

AEM eCommerce는 eCommerce 엔진과 함께 구현됩니다.

* eCommerce 통합 프레임워크가 구축되어 eCommerce 엔진을 AEM과 쉽게 통합할 수 있게 되었습니다. 특별히 제작된 e커머스 엔진은 제품 데이터, 장바구니, 체크아웃 및 주문 이행을 제어하는 반면 AEM은 데이터 표시 및 마케팅 캠페인을 제어합니다.


>[!NOTE]
>
>표준 AEM 설치에는 일반 AEM(JCR) 전자 상거래 구현이 포함됩니다.
>
>이것은 현재 데모용이거나 사용자의 요구 사항에 따라 사용자 정의 구현을 위한 기본 토대가 되었습니다.
>
>JCR을 기반으로 하는 일반 개발을 사용하여 AEM 내에서 구현된 AEM eCommerce는 다음과 같습니다.
>
>* API의 사용을 설명하기 위한 독립 실행형 AEM 기본 전자 상거래 예입니다. 기존 데이터 표시 및 마케팅 캠페인과 함께 제품 데이터, 장바구니 및 체크아웃을 제어하는 데 사용할 수 있습니다. 이 경우 제품 데이터베이스가 AEM(Adobe의 JCR 구현)을 기준으로 하는 저장소에 [저장됩니다](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/index.html).
   >  표준 AEM 설치에는 [일반 전자 상거래 구현의 기본 사항이 포함되어 있습니다](/help/sites-administering/generic.md).
>



### 상거래 제공업체 {#commerce-providers}

상거래 엔진에서 AEM eCommerce 사이트로 데이터를 가져올 때 상거래 공급자가 데이터를 가져오자에게 제공하는 데 사용됩니다. 한 상거래 공급자가 여러 가져오기 도구를 지원할 수 있습니다.

상거래 공급자는 다음 중 하나로 사용자 지정된 AEM 코드입니다.

* 백엔드 상거래 엔진에 대한 인터페이스
* jcr 저장소 위에 상거래 시스템 구현

현재 AEM 파섹

* geometrixx-hybris용
* geometrixx-generic(JCR)의 또 다른 기능

일반적으로 프로젝트는 PIM과 제품 데이터 스키마와 관련된 고유한 사용자 지정 상거래 공급자를 개발해야 합니다.

>[!NOTE]
>
>geometrixx 가져오기는 CSV 파일을 사용합니다.구현의 위에 있는 주석에 수락된 스키마에 대한 설명이 있습니다(사용자 지정 속성이 허용됨).

ProductServicesManager [는 OSGi](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/commerce/pim/api/ProductServicesManager.html) 를 [통해](/help/sites-deploying/configuring.md#osgi-configuration-settings)ProductImporter [및 CatalogBlueprintImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/commerce/pim/api/ProductImporter.html) 인터페이스 구현 목록을 [유지](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/commerce/pim/api/CatalogBlueprintImporter.html) 관리합니다. 이러한 항목은 가져오기 **마법사의** 가져오기/상거래 `commerceProvider` 공급자 드롭다운 필드에 나열되어 있습니다(속성을 이름으로 사용).

드롭다운에서 특정 Importer/Commerce 공급자를 사용할 수 있는 경우, 필요한 보충 데이터를 Importer 유형에 따라 다음 중 하나에서 정의해야 합니다.

* `/apps/commerce/gui/content/catalogs/importblueprintswizard/importers`
* `/apps/commerce/gui/content/products/importproductswizard/importers`

해당 폴더 아래의 폴더는 가져오기 `importers` 이름과 일치해야 합니다.예를 들면 다음과 같습니다.

* `.../importproductswizard/importers/geometrixx/.content.xml`

소스 가져오기 파일의 형식은 가져오기가 정의합니다. 또는 가져오기 도구가 상거래 엔진에 대한 연결(예: WebDAV 또는 http)을 설정할 수 있습니다.

## 역할 {#roles}

통합 시스템은 데이터를 유지하기 위해 다음 역할을 제공합니다.

* PIM(제품 정보 관리) 사용자 유지:

   * 제품 정보.
   * 분류, 분류, 승인
   * 디지털 에셋 관리와 상호 작용
   * 가격 - 일반적으로 이는 ERP 시스템에서 비롯되며 상거래 시스템에서 명시적으로 유지되지 않습니다.

* 작성자/마케팅 관리자 - 유지 관리:

   * 모든 채널에 대한 마케팅 콘텐츠
   * 프로모션.
   * 바우처.
   * 캠페인.

* Surfer / Shopper who:

   * 제품 정보를 봅니다.
   * 장바구니에 품목을 넣습니다.
   * 주문 확인
   * 주문 처리 예상

실제 위치는 구현에 따라 달라질 수 있습니다.예를 들어, 일반 또는 eCommerce 엔진에서 다음을 수행합니다.

![chlimage_1-6](assets/chlimage_1-6.png)

## 제품 {#products}

### 제품 데이터 및 마케팅 데이터 {#product-data-versus-marketing-data}

#### 구조 및 마케팅 카테고리 {#structural-versus-marketing-categories}

다음 두 카테고리를 구별할 수 있는 경우 의미 있는 구조(노드 트리)로 URL을 명확히 할 수 있으므로 클래식 AEM 컨텐츠 관리에 매우 근접합니다. `cq:Page`

* *구조적 *카테고리

   제품이란 *것을*&#x200B;정의하는 카테고리 트리예를 들면 다음과 같습니다.

   `/products/mens/shoes/sneakers`

* *마케팅* 카테고리

   모든 기타 *제품 카테고리*;예를 들면 다음과 같습니다.

   `/special-offers/christmas/shoes`)

### 제품 데이터 {#product-data}

제품에 대한 다양한 정보를 보유하고 있어야 합니다.

제품 데이터는 다음과 같습니다.

* aem(일반)에서 바로 유지 관리됩니다.
* 유지 관리되고 AEM에서 사용할 수 있게 되었습니다.

   데이터 유형에 따라 필요에 따라 [동기화되거나](#catalog-maintenance-data-synchronization) 직접 액세스됩니다.예를 들어 제품 가격과 같은 휘발성 및 중요 데이터는 항상 최신 상태로 유지되도록 모든 페이지 요청의 전자 상거래 엔진에서 검색됩니다.

두 경우 모두 제품 데이터를 AEM에 입력/가져오면 제품 **콘솔에서 볼 수** 있습니다. 다음은 제품의 카드 및 목록 보기 정보입니다.

* 이미지
* SKU 코드
* 마지막 수정 날짜

![chlimage_1-7](assets/chlimage_1-7.png)

### 제품 변형 {#product-variants}

적절한 제품에 대한 정보도 저장할 수 있습니다. 예를 들어, 옷 항목의 경우 사용할 수 있는 다른 색상이 변형으로 보유됩니다.

![eommercproducts variants](assets/ecommerceproductvariants.png)

### 제품 속성 {#product-attributes}

각 제품에 대해 보유한 개별 속성은 사용 중인 eCommerce 엔진 및 AEM 구현에 따라 달라질 수 있습니다. 제품 페이지를 보거나 제품 정보를 편집할 때(적절히) 사용할 수 있으며 다음이 포함될 수 있습니다.

* **이미지**

   제품의 이미지입니다.

* **제목**

   제품 이름입니다.

* **설명**

   제품에 대한 텍스트 설명입니다.

* **태그**

   관련 제품을 그룹화하는 데 사용되는 태그입니다.

* **기본 자산 범주**

   자산에 대한 기본 카테고리.

* **ERP 데이터**

   ERP(Enterprise Resource Planning) 정보.

   * **SKU**

      SKU(Stock-Keeping Unit) 정보.

   * **색상**
   * **크기**
   * **가격**

      제품의 단가입니다.

* **요약**

   제품 기능에 대한 요약입니다.

* **기능**

   제품 기능에 대한 자세한 내용

### 제품 자산 {#product-assets}

개별 제품에 대해 다양한 자산을 보유할 수 있습니다. 일반적으로 이미지와 비디오가 포함됩니다.

## 카탈로그 {#catalogs}

카탈로그는 제품 데이터를 함께 그룹화하여 관리가 용이하고 구매자에게 전달할 수 있도록 합니다. 종종 카탈로그는 언어, 지리적 영역, 브랜드, 계절, 취미, 스포츠 등 많은 특성에 따라 구성됩니다.

### 카탈로그 구조 {#catalog-structure}

#### 여러 언어로 된 카탈로그 {#catalogs-in-multiple-languages}

AEM은 여러 언어로 된 제품 컨텐츠를 지원합니다. 데이터를 요청할 때 통합 프레임워크는 현재 트리에서 언어를 검색합니다(예: 아래 `en_US` 페이지의 경우 `/content/geometrixx-outdoors/en_US`).

다중 언어 스토어의 경우 각 언어 트리에 대한 카탈로그를 개별적으로 가져오거나 MSM을 통해 복사할 [수 있습니다](/help/sites-administering/msm.md).

#### 여러 브랜드를 위한 카탈로그 {#catalogs-for-multiple-brands}

언어와 마찬가지로 대형 다국적 기업은 다양한 브랜드의 요구 사항을 충족해야 합니다.

#### 태그별 카탈로그 {#catalogs-by-tags}

태그를 사용하여 제품을 카탈로그로 그룹화할 수도 있습니다. 계절별 오퍼와 같은 동적 카탈로그에 사용할 수 있습니다.

### 카탈로그 설정(초기 가져오기) {#catalog-setup-initial-import}

구현에 따라 기본 카탈로그에 필요한 제품 데이터를 다음 위치에서 AEM으로 가져올 수 있습니다.

* CSV 파일(일반 구현용)
* eCommerce 엔진

### 카탈로그 유지 관리(데이터 동기화) {#catalog-maintenance-data-synchronization}

제품 데이터에 대한 추가 변경은 불가피 합니다.

* for generic implementation these can be managed with [product editor](/help/sites-administering/generic.md#editing-product-information)
* eCommerce [엔진을 사용하는 경우 변경 내용을 동기화해야 합니다.](#data-synchronization-with-an-ecommerce-engine-ongoing)

#### eCommerce 엔진과의 데이터 동기화(진행 중) {#data-synchronization-with-an-ecommerce-engine-ongoing}

초기 가져오기 후 제품 데이터의 변경 사항이 불가피합니다.

eCommerce 엔진을 사용할 때 제품 데이터는 해당 지역에서 유지되며 AEM에서 사용할 수 있어야 합니다. 업데이트가 수행되면 이 제품 데이터를 동기화해야 합니다.

데이터 유형에 따라 달라질 수 있습니다.

* 주기적 [동기화는 변경](/help/sites-developing/sap-commerce-cloud.md#product-synchronization-and-publishing)사항의 데이터 피드와 함께 사용됩니다.

   이 외에도, 익스프레스 업데이트에 대한 특정 업데이트를 선택할 수 있습니다.

* 가격 정보와 같은 휘발성이 높은 데이터는 항상 최신 상태로 유지되도록 각 페이지 요청에 대한 상거래 엔진에서 검색됩니다.

### 카탈로그 - 성능 및 크기 조절 {#catalogs-performance-and-scaling}

eCommerce 엔진(PIM)에서 제품 수가 많은 대형 카탈로그(일반적으로 10만 개 이상)를 가져올 경우 노드의 수가 많기 때문에 시스템에 영향을 줄 수 있습니다. 제품에 연결된 자산(예: 제품 이미지)이 있는 경우 제작 인스턴스를 느려질 수도 있습니다. 이는 이러한 자산의 사후 처리가 CPU와 메모리를 많이 사용하기 때문입니다.

다음과 같은 문제를 해결하기 위해 선택할 수 있는 다양한 전략이 있습니다.

* [Bucketing](#bucketing) - 많은 수의 노드에 대한 요구 사항
* [자산 게시 처리를 전용 인스턴스로 오프로드](#offload-asset-post-processing-to-a-dedicated-instance)
* [제품 데이터만 가져오기](#only-import-product-data)
* [스로틀링 및 일괄 저장 가져오기](#import-throttling-and-batch-saves)
* [성능 테스트](#performance-testing)
* [성능 - 기타](#performance-miscellaneous)

#### 버킷 {#bucketing}

JCR 노드에 많은 직접 하위 노드(예: 1000 이상)가 있는 경우 버킷(phantom 폴더)이 있어야 성능이 영향을 받지 않습니다. 가져올 때 알고리즘에 따라 생성됩니다.

이러한 버킷은 카탈로그 구조에 도입된 팬텀 폴더 형태를 취하지만 공개 URL에서 명확히 보이지 않도록 구성할 수 있습니다.

#### 자산 게시 처리를 전용 인스턴스로 오프로드 {#offload-asset-post-processing-to-a-dedicated-instance}

이 시나리오에는 두 개의 작성자 인스턴스를 설정하는 작업이 포함됩니다.

1. 마스터 작성자 인스턴스

   자산 경로에 대한 사후 처리가 비활성화된 PIM에서 제품 데이터를 가져옵니다.

1. 전용 DAM 작성자 인스턴스

   PIM에서 제품 에셋을 가져오고 사후 처리 한 다음 다시 마스터 작성자 인스턴스로 복제하여 사용할 수 있습니다.

![아키텍처 다이어그램](assets/chlimage_1-8.png)

#### 제품 데이터만 가져오기 {#only-import-product-data}

제품을 가져올 자산(이미지)이 포함되지 않은 경우 자산 사후 처리의 영향을 받지 않고 제품 데이터를 가져올 수 있습니다.

![아키텍처 다이어그램](assets/chlimage_1-9.png)

<!--delete
#### Import Throttling and Batch Saves {#import-throttling-and-batch-saves}

[Import throttling](/help/sites-deploying/scaling.md#import-throttling) and [batch saves](/help/sites-deploying/scaling.md#batch-saves) are two general [scaling](/help/sites-deploying/scaling.md) mechanisms that can help when importing large volumes of data.-->

#### 성능 테스트 {#performance-testing}

성능 테스트는 AEM eCommerce 구현에 대해 고려해야 합니다.

* 작성 환경:

   백그라운드(예: 가져오기) 활동은 일반 사용자 작업(예: 페이지 편집)과 동시에 발생할 수 있으며, 프런트 엔드 성능이 더 높은 우선 순위를 제공하더라도(일반적으로) 온라인 작성자가 본 성능 불량 성능은 라이브 결정을 차단할 수 있는 좌절감을 초래할 수 있습니다.

* 게시 환경:

   복제는 컨텐츠가 빠르고 안전하게 게시되도록 보장하는 중요한 프로세스입니다. 이는 작성자가 게시할 컨텐츠를 그룹화하는 방식에 의해 영향을 받을 수 있습니다.

* 프런트 엔드:

   프런트 엔드와 캐시 무효화가 혼합되면 성능이 저하될 수 있습니다. 테스트를 통해 이러한 문제를 방지할 수 있습니다.

이 성능 테스트를 수행하려면 대상에 대한 지식 및 분석이 필요합니다.

* 컨텐츠 볼륨

   * 자산
   * 현지화된 I18핵심 제품 및 SKU

* 사용자 활동:

   * Bulk edition
   * 일괄 게시
   * 강력한 검색 요청

* 백그라운드 프로세스

   * 가져오기
   * 동기화 업데이트(예: 가격)

* 유지 관리 요구 사항(백업, Tar PM 최적화, 데이터 저장소 가비지 수집 등)

#### 성능 - 기타 {#performance-miscellaneous}

모든 구현의 경우 다음 사항을 염두에 둘 수 있습니다.

* 제품, 재고 관리 단위 및 카테고리는 수가 많을 수 있으므로, 컨텐츠를 모델링하는 데 가능한 최소 노드 수를 사용하십시오.

   노드가 많을수록 컨텐츠가 유연해집니다(예: parsys). 그러나 모든 것은 교환이며 30K 제품을 조작할 때(예: 기본적으로) 개별 유연성이 필요합니까?

* 가능한 한(현지화 참조) 중복을 피하거나 복제할 때 어떤 노드를 가져오는지 생각해 보십시오.
* 쿼리 최적화를 준비하려면 가능한 한 컨텐츠에 태그를 지정해 보십시오.

   예:

   `/content/products/france/fr/shoe/reebok/pump/46 SKU`

   는 컨텐츠 수준당 하나의 태그를 포함해야 합니다(예: 국가, 언어, 카테고리, 브랜드, 제품). 검색

   `//element(*,my:Sku)[@country=’france’ and @language=’fr’`

   및

   `@category=’shoe’ and @brand=’reebok’ and @product=’pump’]`

   검색 속도가

   `/jcr:root/content/france/fr/shoe/reebok/pump/element(*,my:Sku)`

* 기술 스택에서 최적화된 콘텐츠 액세스 모델 및 서비스를 계획하십시오. 이는 일반적인 우수 사례이지만, 최적화 단계에서 자주 읽히는 데이터에 대한 애플리케이션 캐시를 추가합니다(번들 캐시를 채우지 않으려는 경우).

   예를 들어, 속성 관리는 제품 가져오기를 통해 업데이트되는 데이터에 대한 우려 때문에 캐싱하기에 매우 자주 적합합니다.
* 프록시 [페이지의](/help/sites-administering/concepts.md#proxy-pages)사용을 고려합니다.

### 카탈로그 섹션 페이지 {#catalog-section-pages}

카탈로그 섹션에서는 다음과 같은 정보를 제공합니다.

* 범주에 대한 소개(이미지 및/또는 텍스트);배너와 티저가 특별 오퍼를 홍보하는 데 사용할 수도 있습니다.
* 해당 범주의 개별 제품에 대한 링크
* 다른 카테고리에 대한 링크

![ecommerce_categoryrunning](assets/ecommerce_categoryrunning.png)

### 제품 페이지 {#product-pages}

제품 페이지에서는 개별 제품에 대한 포괄적인 정보를 제공합니다. 동적 업데이트도 반영됩니다.예를 들어, eCommerce 엔진에 등록된 가격 변경입니다.

제품 페이지는 제품 구성 요소를 사용하는 **AEM** 페이지입니다.예를 들어 커머스 제품 **템플릿 내에서** 다음을 수행합니다.

![ecommerce_nairobirunly green](assets/ecommerce_nairobirunnersgreen.png)

제품 구성 요소는 다음을 제공합니다.

* 일반 제품 정보;텍스트 및 이미지 포함
* 가격;일반적으로 페이지를 표시하거나 새로 고칠 때마다 eCommerce 엔진에서 검색됩니다.
* 제품 변형 정보;예: 색상 및 크기.

이 정보를 통해 구매자는 장바구니에 품목을 추가할 때 다음을 선택할 수 있습니다.

* 색상 및 크기 변형
* 수량

#### 제품 랜딩 페이지 {#product-landing-pages}

주로 정적 정보를 제공하는 AEM 페이지입니다.예를 들어 기본 제품 페이지에 대한 링크가 포함된 소개 및 개요입니다.

### 제품 구성 요소 {#product-component}

제품 **구성** 요소는 필요한 메타데이터(즉, 및 경로)를 전달하는 상위 페이지가 있는 페이지에 추가할 수 `cartPage` 있습니다 `cartObject`. 데모 사이트의 Geometrixx Outdoors에서는 이 기능이 `UserInfo.jsp`제공됩니다.

제품 **구성** 요소는 개별 요구 사항에 따라 사용자 정의할 수도 있습니다.

### 프록시 페이지 {#proxy-pages}

프록시 페이지는 저장소 구조를 단순화하고 대규모 카탈로그에 대한 저장소를 최적화하는 데 사용됩니다.

카탈로그를 만들면 AEM 내에서 업데이트하고 사용자 지정할 수 있는 각 제품에 대한 개별 구성 요소를 제공하므로 제품당 10개의 노드가 사용됩니다. 카탈로그에 수백 또는 수천 개의 제품이 포함되어 있는 경우 이러한 많은 수의 노드가 문제가 될 수 있습니다. 문제를 방지하기 위해 프록시 페이지를 사용하여 카탈로그를 만들 수 있습니다.

프록시 페이지는 실제 제품 컨텐츠를 포함하지 않는 2노드 구조( `cq:Page` 및 `jcr:content`)를 사용합니다. 요청 시 제품 데이터 및 템플릿 페이지를 참조하여 컨텐츠가 생성됩니다.

그러나, 무역이 있다. AEM 내에서 제품 정보를 사용자 지정할 수 없으며 사이트에 대해 정의된 표준 템플릿이 사용됩니다.

>[!NOTE]
>
>프록시 페이지 없이 큰 카탈로그를 가져오는 경우 문제가 발생하지 않습니다.
>
>한 방법론에서 다른 방법론으로 언제든지 변환할 수 있습니다. 카탈로그의 하위 섹션을 변환할 수도 있습니다.

## 프로모션 및 바우처 {#promotions-and-vouchers}

### 바우처 {#vouchers}

바우처는 구매자를 유도하여 구매하거나 고객의 충성도를 보상하는 데 필요한 할인을 제공하는 시험되고 테스트된 방법입니다.

* 바우처 공급:

   * 구매자가 장바구니에 입력하는 바우처 코드.
   * 할인권 레이블(구매자가 장바구니에 입력한 후 표시됨).
   * 프로모션 경로(바우처가 적용되는 작업을 정의합니다).

* 외부 상거래 엔진은 바우처를 제공할 수도 있습니다.

AEM에서:

* 바우처는 웹 사이트 콘솔에서 만들거나 편집하는 페이지 기반 구성 요소입니다.
* 바우처 **구성** 요소는 다음을 제공합니다.

   * 바우처 관리를 위한 렌더러여기에는 현재 장바구니에 있는 모든 바우처가 표시됩니다.
   * 바우처를 관리(추가/제거)하기 위한 편집 대화 상자(양식)입니다.
   * 장바구니에 바우처를 추가/제거하는 데 필요한 작업

* 바우처에는 설정 및 해제 날짜/시간이 없지만 상위 캠페인의 사용 횟수가 포함됩니다.

>[!NOTE]
>
>AEM에서는 **바우처를**&#x200B;사용하며 쿠폰이라는 용어와 동의어입니다 ****.

### 프로모션 {#promotions}

프로모션은 바우처와 함께 다음과 같은 시나리오를 구현할 수 있습니다.

* 한 회사는 수공예 사용자 목록인 종업원에게 맞춤 가격을 제공한다.
* 장기 고객은 모든 주문에 대해 할인 혜택을 받습니다.
* 잘 정의된 기간 동안 제공되는 판매 가격.
* 이전 주문이 특정 금액을 초과할 경우 고객은 바우처를 받습니다.
* X *제품을 구매하는 고객은* product-Y *(두 개 제품)를 할인* 받을 수 있습니다.

프로모션은 일반적으로 제품 정보 관리자가 관리하는 것이 아니라 마케팅 관리자가 관리합니다.

* 프로모션은 웹 사이트 콘솔에서 작성/편집되는 페이지 기반 구성 요소입니다. ``
* 프로모션 공급:

   * 우선 순위
   * 프로모션 처리기 경로

* 캠페인을 캠페인에 연결하여 온/오프 날짜/시간을 정의할 수 있습니다.
* 판촉을 경험에 연결하여 세그먼트를 정의할 수 있습니다.
* 경험에 연결되지 않은 프로모션은 자체적으로 실행되지 않지만 바우처에 의해 실행될 수 있습니다.
* 프로모션 구성 요소에는 다음이 포함됩니다.

   * 프로모션 관리를 위한 렌더러 및 대화 상자
   * 프로모션 핸들러와 관련된 구성 매개 변수를 렌더링 및 편집하는 하위 구성 요소

AEM에서 프로모션은 캠페인 관리에도 [통합됩니다](/help/sites-authoring/personalization.md).

* [캠페인은](/help/sites-authoring/personalization.md) 설정/해제 시간을 지정합니다
* [캠페인](/help/sites-authoring/personalization.md) 내 ** 경험은

프로모션은 경험 또는 캠페인에서 직접 수행할 수 있습니다.

* 판촉 행사가 경험에서 진행되는 경우 대상 세그먼트에 자동으로 적용할 수 있습니다.

   예를 들어 geometrixx-outdoors 샘플 사이트에서 판촉 행사는 다음과 같습니다.

   `/content/campaigns/geometrixx-outdoors/big-spender/ordervalueover100/free-shipping`

   가 경험에 포함되어 있으므로 세그먼트( `ordervalueover100`)가 확인될 때마다 자동으로 실행됩니다.

* 판촉 행사가 경험 내에 표시되지 않는 경우(캠페인에만 해당) 대상에 자동으로 적용할 수 없습니다. 하지만 구매자가 카트에 바우처를 입력하고 해당 바우처가 프로모션을 참조하는 경우 여전히 실행할 수 있습니다.

   예를 들어 프로모션은 다음과 같습니다.

   `/content/campaigns/geometrixx-outdoors/article/10-bucks-off`

   가 경험 외부에 있으므로 자동으로 실행되지 않습니다(예:를 참조하십시오. 하지만 아티클 캠페인 내 여러 경험에서 찾을 수 있는 바우처가 참조됩니다. 이러한 바우처 코드를 장바구니에 입력하면 프로모션이 시작됩니다.

>[!NOTE]
>
>[hybris 판촉](https://www.hybris.com/modules/promotion) 및 [하이브리스는 장바구니에 영향을 미치는 모든 것과 가격 관련 정보를 제공합니다](https://www.hybris.com/en/modules/voucher) . 프로모션 특정 마케팅 컨텐츠(예: 배너 등)는 하이브리스 프로모션의 일부가 아닙니다.

## 개인화 {#personalization}

### 고객 등록 및 계정 {#customer-registration-and-accounts}

구매자가 등록하면 AEM과 eCommerce 엔진 간에 계정 세부 사항을 동기화해야 합니다. 중요한 데이터는 독립적으로 유지되지만 프로필은 공유됩니다.

![chlimage_1-10](assets/chlimage_1-10.png)

정확한 메커니즘은 시나리오에 따라 달라질 수 있습니다.

1. 사용자 계정은 두 시스템 모두에 있습니다.

   1. 필요한 작업이 없습니다.

1. 사용자 계정은 AEM에만 있습니다.

   1. 사용자는 동일한 계정 ID와 무작위 암호를 사용하여 eCommerce 엔진에서 생성되며 이 암호는 AEM에 저장됩니다.
   1. AEM이 첫 번째 호출(예: 제품 페이지가 요청되고 eCommerce 엔진이 가격에 대해 참조되는 경우)에 eCommerce 엔진에 로그인하려고 할 때 무작위 암호가 필요합니다. 이 문제는 AEM 로그인 후 발생하므로 암호를 사용할 수 없습니다.

1. 사용자 계정은 전자 상거래 엔진에만 있습니다.

   1. 계정은 계정 ID와 암호가 동일한 AEM에서 생성됩니다.

eCommerce 엔진을 사용할 때 AEM은 계정 ID와 암호(사용자 그룹 선택 사항)만 저장합니다. 기타 모든 정보는 eCommerce 엔진에 저장됩니다.

>[!NOTE]
>
>eCommerce 엔진을 사용할 때 AEM 인스턴스에 로그인하는 사용자에 대해 만들어진 계정이 해당 엔진과 통신하는 다른 AEM 인스턴스로 복제되도록 해야 합니다.
>
>그렇지 않으면 이러한 다른 AEM 인스턴스도 엔진에서 동일한 사용자에 대한 계정을 만들려고 시도합니다. 이러한 작업은 엔진에서 `DuplicateUidException` 오가면서 실패합니다.

### 고객 등록 {#customer-sign-up}

쇼핑 카트를 이용하려면 종종 등록이 필요합니다. 이를 위해서는 고객별 계정을 만들 수 있도록 등록(계정 만들기)이 필요합니다.

![chlimage_1-11](assets/chlimage_1-11.png)

>[!NOTE]
>
>익명의 장바구니 및 체크아웃도 지원됩니다.

### 고객 로그인 {#customer-sign-in}

등록 후 구매자는 자신의 계정으로 로그인하여 자신의 작업을 추적하고 주문이 이행되도록 할 수 있습니다.

![chlimage_1-12](assets/chlimage_1-12.png)

### 단일 사인온 {#single-sign-on}

SSO(Single Sign-On)가 제공되므로 작성자가 두 번 로그인하지 않고도 AEM과 eCommerce 시스템에서 모두 알 수 있습니다.

### myAccount {#myaccount}

eCommerce 엔진의 거래 데이터는 구매자에 대한 개인 정보와 결합됩니다. AEM 파섹 AEM에서 양식의 동작은 정보를 다시 전자 상거래 엔진에 기록합니다.

계정 정보를 쉽게 관리할 수 있는 페이지가 있습니다. geometrixx 페이지 **위쪽에서 내 계정을** 클릭하거나 로 이동하여 액세스할 수 `/content/geometrixx-outdoors/en/user/account.html`있습니다.

![chlimage_1-13](assets/chlimage_1-13.png)

### 주소록 {#address-book}

사이트에서 선택한 주소를 저장해야 합니다.배달, 청구 및 대체 주소를 포함합니다. 기본 주소 형식을 기반으로 양식을 사용하여 구현하거나 AEM에서 제공하는 주소록 구성 요소를 사용할 수 있습니다.

이 주소록 구성 요소를 사용하면 다음을 수행할 수 있습니다.

* 책의 주소 편집
* 배송 주소록에서 주소 선택
* 청구 주소록에서 주소를 선택합니다.

원하는 주소를 기본값으로 선택할 수 있습니다.

주소록 구성 요소는 주소록을 **클릭하거나** 로 이동하여 **내 계정** 페이지에서 `/content/geometrixx-outdoors/en/user/account/address-book.html`액세스할 수있습니다.

![chlimage_1-14](assets/chlimage_1-14.png)

**새 주소**&#x200B;추가...를 클릭할 수 있습니다.를 클릭하여 주소록에 새 주소를 추가합니다. 양식을 작성한 다음 주소 추가를 **클릭합니다**.

>[!NOTE]
>
>주소록에 몇 개의 주소를 입력할 수 있습니다.

장바구니를 체크아웃할 때 주소록이 사용됩니다.

![chlimage_1-15](assets/chlimage_1-15.png)

주소는 아래에 `user_home/profile/addresses`있습니다.
예를 들어 Alison Parker의 경우 /home/users/geometrixx/aparker@geometrixx.info/profile/addresses 아래에 있습니다.

원하는 주소를 기본값으로 선택할 수 있습니다. 이 정보는 주소가 아닌 구매자의 프로필에 유지됩니다. 프로필 속성은 값에 대해 선택한 주소의 경로로 `address.default` 설정됩니다.

### 고객별 가격 {#customer-specific-pricing}

eCommerce 엔진은 컨텍스트(기본적으로 구매자 정보)를 사용하여 보유하려는 가격을 결정한 다음 올바른 정보를 다시 AEM에 제공합니다.

## 장바구니 및 주문 {#shopping-cart-and-orders}

쇼핑할 때 구매자는 제품 페이지를 탐색하고 장바구니에 놓을 항목을 선택합니다. 결제 진행 시 주문이 제출될 수 있습니다.

### 익명의 구매자 {#anonymous-shoppers}

익명의 고객은 다음을 수행할 수 있습니다.

* 제품 보기
* 장바구니에 제품 추가
* 주문 시 결제 수행

>[!NOTE]
>
>인스턴스 주소 정보의 구성에 따라 결제 전에 고객 등록이 필요할 수 있습니다.

### 등록된 구매자 {#registered-shoppers}

등록된 고객은 다음을 수행할 수 있습니다.

* 계정에 로그인
* 제품 보기
* 장바구니에 제품 추가
* 주문 시 결제 수행
* 이전 주문 보기 및 추적

### 장바구니 컨텐츠 개요 {#shopping-cart-content-overview}

장바구니는 다음과 같은 이점을 제공합니다.

* 선택한 항목 개요
* 선택한 항목의 제품 페이지에 대한 링크
* 기능:

   * 개별 품목의 수/수량 업데이트
   * 개별 항목 제거

![ecommerce_shoppingcart](assets/ecommerce_shoppingcart.png)

장바구니는 사용되는 엔진에 따라 저장됩니다.

* AEM 일반
* 특정 eCommerce 엔진은 장바구니를 세션에 저장할 수 있습니다.

두 경우 모두 항목이 장바구니에 남아 있고(그리고 복원할 수 있음) 로그인/로그아웃(동일한 컴퓨터/브라우저에서만)에 있습니다. 예:

* 다른 이름으로 `anonymous` 검색하고 장바구니에 제품 추가
* 로그인 `Allison Parker` - 장바구니가 비어 있음
* 장바구니에 제품 추가
* 로그아웃 - 장바구니에 `anonymous`

* 다시 로그인 - `Allison Parker` 그녀의 제품 복원

>[!NOTE]
>
>익명의 장바구니는 동일한 컴퓨터/브라우저에서만 복원할 수 있습니다.

>[!NOTE]
>
>eCommerce 엔진(예: hybris)의 `admin` `admin` 계정과 충돌할 수 있으므로 장바구니 컨텐츠를 계정과 복원하지 않는 것이 좋습니다.

>[!NOTE]
>
>hybris는 지정된 기간 후에 보류 중인 장바구니를 제거하도록 구성할 수 있습니다.

체크아웃 전에 가격 변경 사항이 (두 시스템 모두) 발생할 때 반영됩니다.

### 주문 정보 {#order-information}

주문에 대한 구현 정보가 eCommerce 엔진 또는 AEM에서 보관되는 경우 AEM에서 이 정보를 제공합니다.

다음과 같은 다양한 정보가 저장됩니다.

* **주문 ID**

   주문의 참조 번호입니다.

* **주문 날짜**

   주문하신 날짜입니다.

* **상태**

   주문 현황예: 배송됨

* **통화**

   주문의 통화.

* **컨텐츠 항목**

   주문한 항목 목록입니다.

* **소계**

   주문된 항목의 총 비용.

* **세금**

   주문에 대한 납세의 금액.

* **배송**

   배송 비용.

* **합계**

   주문의 총액주문 품목, 세금 및 할인.

* **청구 주소**

   송장을 발송할 주소.

* **결제 토큰**

   결제 방법

* **결제 상태**

   지불 상태.

* **배송 주소**

   선적할 물품 주소.

* **배송 방법**

   운송방법예를 들어, 토지, 바다 또는 공기.

* **추적 번호**

   운송 회사가 사용하는 모든 추적 번호입니다.

* **추적 링크**

   배송되는 동안 주문 추적에 사용되는 링크입니다.

>[!NOTE]
>
>주문 만들기 마법사에서 사용되는 필드는 해당 위치에 대해 정의된 터치에 적합한 스캐폴딩에 따라 달라집니다. 일반 예에서 다음 위치에서 찾을 수 있습니다.
>`/etc/scaffolding/geometrixx-outdoors/order/jcr:content/cq:dialog`

AEM 내에서 주문이 보류되면 주문 콘솔에 각 주문에 대한 다음 내용이 표시됩니다.

* 장바구니에 있는 항목 수
* 주문의 총 가치
* 주문 제출 시기
* 상태

![chlimage_1-16](assets/chlimage_1-16.png)

### 주문 추적 {#order-tracking}

주문을 하면 구매자는 종종 다음 주소로 돌아옵니다.

* 주문 상태 확인
* 주문에서 제품 제거
* 주문에 제품 추가

주문 배송을 받은 후, 구매자는 일정 기간 동안 이루어진 주문 내역을 보고 싶을 수도 있습니다.

주문 처리 및 추적은 일반적으로 eCommerce 엔진에서 관리합니다. 주문 내역 구성 요소를 사용하여 AEM에서 정보를 표시할 수 있습니다. 이 구성 요소는 적용된 바우처 및 프로모션을 포함하여 모든 관련 세부 사항을 보여줍니다. 예:

![chlimage_1-17](assets/chlimage_1-17.png)

## 체크아웃 {#checkout}

체크아웃은 표준 AEM 양식과 함께 구현됩니다. 이를 통해 마케팅 관리자는 마케팅 컨텐츠로 경험을 사용자 정의할 수 있습니다.

그런 다음 eCommerce는 AEM 양식의 입력을 사용하여 체크아웃 프로세스를 관리합니다.

### 지불 보안 {#payment-security}

신용 카드 정보를 비롯한 결제 세부 사항은 종종 전자 상거래 엔진에서 관리합니다. AEM 파섹

결제 카드 업계(PCI) 규정 준수를 실현할 수 있습니다.

### 주문 확인 {#confirmation-of-order}

주문은 화면에서 확인되고 [주문 추적으로](#order-tracking)추적할 수 있습니다.

## 검색 {#search-features}

![chlimage_1-18](assets/chlimage_1-18.png)

AEM은 제품에 표준 페이지를 사용하므로 표준 검색 구성 요소를 사용하여 검색 페이지를 만들 수 있습니다.

보다 철저한 구현이 필요한 경우 다음 중 하나를 수행할 수 있습니다.

* 필요한 기능으로 기본 검색 구성 요소를 확장합니다.
* 검색 페이지에서 검색 방법을 구현한 `CommerceService` 다음 검색 페이지에서 전자 상거래 검색 구성 요소를 사용합니다.

eCommerce 엔진을 사용할 때 eCommerce 검색 API를 eCommerce 엔진 솔루션에서 완전히 구현할 수 있으므로 즉시 제공되는 eCommerce 검색 구성 요소를 사용할 수 있습니다. 패싯된 검색을 사용하면 JCR 및/또는 엔진을 검색할 수 있습니다.

