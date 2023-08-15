---
title: 개념
description: Adobe Experience Manager과 함께 전자 상거래에 대한 일반 개념.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: 290b2af6-257f-42f2-b809-1248227a4795
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '4478'
ht-degree: 2%

---

# 개념{#concepts}

통합 프레임워크는 다음을 위한 메커니즘 및 구성 요소를 제공합니다.

* eCommerce 엔진에 연결
* Adobe Experience Manager(AEM)로 데이터 가져오기
* 해당 데이터 표시 및 구매자의 응답 수집
* 거래 세부 정보 반환
* 두 시스템의 데이터 검색

이 의미는 다음과 같습니다.

* 쇼핑객들은 기다리지 않고 등록하고 쇼핑할 수 있다.
* 가격 변동은 쇼핑객들이 지체 없이 보게 된다.
* 필요에 따라 제품을 추가할 수 있습니다.

>[!NOTE]
>
>eCommerce 프레임워크는 다음과 함께 사용할 수 있습니다.
>
>* [Adobe Commerce](/help/commerce/cif/integrating/magento.md)
>* [SAP COMMERCE CLOUD](/help/commerce/cif-classic/administering/sap-commerce-cloud.md)
>* [Salesforce Commerce Cloud](https://github.com/adobe/commerce-salesforce)
>

>[!CAUTION]
>
>다음 [eCommerce 통합 프레임워크](https://business.adobe.com/products/experience-manager/sites/ecommerce-integrations.html) 는 AEM 추가 기능입니다.
>
>영업 담당자가 해당 엔진에 따라 세부 정보를 제공할 수 있습니다.

>[!CAUTION]
>
>프레임워크는 자체 프로젝트에 대한 기본 요구 사항을 제공합니다.
>
>사용자 사양에 맞게 프레임워크를 조정하려면 항상 일정한 양의 개발 작업이 필요합니다.

>[!CAUTION]
>
>표준 AEM 설치에는 일반 AEM(JCR) eCommerce 구현이 포함됩니다.
>
>이는 데모 목적이거나 요구 사항에 따라 사용자 지정 구현을 위한 기본 토대입니다.

운영을 최적화하기 위해 AEM과 eCommerce 엔진은 모두 자신의 전문 분야에 집중합니다. 정보는 실시간으로 양사 간에 전송됩니다. 예를 들면 다음과 같습니다.

* AEM은 다음 작업을 수행할 수 있습니다.

   * 요청:

      * eCommerce 엔진의 제품 정보.

   * 제공:

      * 제품 정보, 장바구니 및 체크아웃에 대한 사용자 보기.
      * 전자 상거래 엔진에 대한 장바구니 및 체크아웃 정보.
      * SEO(검색 엔진 최적화).
      * 커뮤니티 기능.
      * 구조화되지 않은 마케팅 상호 작용.

* eCommerce 엔진은 다음을 수행할 수 있습니다.

   * 제공:

      * 데이터베이스의 제품 정보.
      * 제품 변형 관리.
      * Order Management
      * ERP(전사적 자원 관리).
      * 제품 정보 내에서 검색합니다.

   * 프로세스:

      * 장바구니.
      * 체크아웃이요.
      * 주문 처리.

>[!NOTE]
>
>정확한 세부 정보는 eCommerce 엔진 및 프로젝트 구현에 따라 다릅니다.

통합 레이어를 사용할 수 있도록 몇 가지 기본 AEM 구성 요소가 제공됩니다. 현재 여기에는 다음이 포함됩니다.

* 제품 정보
* 장바구니
* 체크아웃
* 내 계정

다양한 검색 옵션도 제공됩니다.

## 아키텍처 {#architecture}

통합 프레임워크는 API, 기능을 보여 주는 다양한 구성 요소 및 연결 방법의 예를 제공하는 몇 가지 확장을 제공합니다.

![chlimage_1-4](/help/sites-administering/assets/chlimage_1-4.png)

프레임워크를 통해 다음과 같은 기능에 액세스할 수 있습니다.

![chlimage_1-5](/help/sites-administering/assets/chlimage_1-5.png)

### 구현 {#implementations}

AEM eCommerce는 eCommerce 엔진을 사용하여 구현됩니다.

* eCommerce 통합 프레임워크를 구축하여 eCommerce 엔진을 AEM과 쉽게 통합할 수 있습니다. 특수 목적으로 구축된 eCommerce 엔진은 제품 데이터, 장바구니, 체크아웃 및 주문 이행을 제어하고, AEM은 데이터 표시 및 마케팅 캠페인을 제어합니다.


>[!NOTE]
>
>표준 AEM 설치에는 일반 AEM(JCR) eCommerce 구현이 포함됩니다.
>
>이는 데모 목적이거나 요구 사항에 따라 사용자 지정 구현을 위한 기본 토대입니다.
>
>AEM eCommerce는 JCR을 기반으로 한 일반 개발을 사용하여 AEM 내에서 구현됩니다.
>
>* API 사용을 보여주는 독립 실행형 AEM 네이티브 전자 상거래 예입니다. 기존 데이터 표시 및 마케팅 캠페인으로 제품 데이터, 장바구니 및 체크아웃을 제어하는 데 사용할 수 있습니다. 이 경우 제품 데이터베이스는 AEM(Adobe의 구현) 고유의 저장소에 저장됩니다. [JCR](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/index.html)).
>
>  표준 AEM 설치에는 다음과 같은 기본 사항이 포함되어 있습니다. [일반 eCommerce 구현](/help/commerce/cif-classic/administering/generic.md).

### 상거래 공급자 {#commerce-providers}

상거래 엔진에서 AEM eCommerce 사이트로 데이터를 가져올 때 상거래 공급자를 사용하여 가져오기에 데이터를 제공합니다. 한 상거래 공급자가 여러 수입업체를 지원할 수 있습니다.

상거래 공급자는 다음 중 하나로 사용자 지정된 AEM 코드입니다.

* 백엔드 상거래 엔진에 대한 인터페이스
* jcr 저장소 위에 상거래 시스템 구현

현재 AEM에 사용할 수 있는 두 가지 상거래 공급자의 예는 다음과 같습니다.

* geometrixx-hybris용 1개
* geometrixx-generic(JCR)용 다른 솔루션

일반적으로 프로젝트는 PIM 및 제품 데이터 스키마에 맞는 고유한 맞춤화된 상거래 공급자를 개발해야 합니다.

>[!NOTE]
>
>Geometrixx 가져오기는 CSV 파일을 사용합니다. 구현 위의 주석에 허용되는 스키마(허용된 사용자 지정 속성 포함)에 대한 설명이 있습니다.

다음 [제품 서비스 관리자](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/commerce/pim/api/ProductServicesManager.html) 유지(에서 까지) [OSGi](/help/sites-deploying/configuring.md#osgi-configuration-settings)) 의 구현 목록 [제품 가져오기](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/commerce/pim/api/ProductImporter.html) 및 [카탈로그 블루프린트 가져오기](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/commerce/pim/api/CatalogBlueprintImporter.html) 인터페이스. 다음 목록에 나열되어 있습니다 **가져오기/상거래 공급자** importer 마법사의 드롭다운 필드( `commerceProvider` 속성을 이름)으로 사용할 수 있습니다.

드롭다운에서 특정 Importer/Commerce 공급자를 사용할 수 있는 경우 다음 중 하나에서 필요한 보조 데이터를 정의해야 합니다(Importer 유형에 따라 다름).

* `/apps/commerce/gui/content/catalogs/importblueprintswizard/importers`
* `/apps/commerce/gui/content/products/importproductswizard/importers`

해당 폴더 `importers` 폴더는 가져오기 이름과 일치해야 합니다. 예:

* `.../importproductswizard/importers/geometrixx/.content.xml`

소스 가져오기 파일의 형식은 가져오기에서 정의합니다. 또는 임포터가 상거래 엔진에 연결(예: WebDAV 또는 http)을 설정할 수 있습니다.

## 역할 {#roles}

통합 시스템은 데이터를 유지 관리하기 위해 다음 역할을 충족합니다.

* PIM(Product Information Management) 사용자가 유지 관리:

   * 제품 정보.
   * 분류, 분류, 승인.
   * 디지털 자산 관리와 상호 작용합니다.
   * 가격 책정 - 일반적으로 ERP 시스템에서 발생하며 상거래 시스템에서는 명시적으로 관리되지 않습니다.

* 유지 관리하는 작성자/마케팅 관리자:

   * 모든 채널에 대한 마케팅 콘텐츠.
   * 프로모션.
   * 바우처.
   * 캠페인.

* 서퍼/쇼핑객:

   * 제품 정보를 조회합니다.
   * 장바구니에 항목을 배치합니다.
   * 주문을 확인합니다.
   * 주문 이행 예상.

실제 위치는 구현에 따라 달라질 수 있지만(예: 일반 또는 eCommerce 엔진 사용):

![chlimage_1-6](/help/sites-administering/assets/chlimage_1-6.png)

## 제품 {#products}

### 제품 데이터 대 마케팅 데이터 {#product-data-versus-marketing-data}

#### 구조 및 마케팅 범주 {#structural-versus-marketing-categories}

다음 두 카테고리를 구분할 수 있으면 의미 있는 구조(의 트리)를 가진 명확한 URL을 만들 수 있습니다. `cq:Page` 노드) 및 따라서 클래식 AEM 컨텐츠 관리에 매우 가까움):

* *구조적 *범주

  범주 트리 정의 *제품이란?*; 예:

  `/products/mens/shoes/sneakers`

* *마케팅* 카테고리

  다음 위치에 있는 다른 모든 범주: *제품이 속할 수 있음*; 예:

  `/special-offers/christmas/shoes`)

### 제품 데이터 {#product-data}

제품을 표시하고 관리하기 위해 해당 제품에 대한 다양한 정보를 보유할 수 있습니다.

제품 데이터는 다음과 같을 수 있습니다.

* AEM(일반)에서 직접 유지 관리됩니다.
* eCommerce 엔진에서 유지 관리되고 AEM에서 사용할 수 있습니다.

  데이터 유형에 따라 다음과 같습니다. [동기화됨](#catalog-maintenance-data-synchronization) 필요에 따라 또는 직접 액세스합니다. 예를 들어, 제품 가격과 같은 휘발성이 높고 중요한 데이터는 모든 페이지 요청 시 전자 상거래 엔진에서 검색하여 항상 최신 상태로 유지됩니다.

두 경우 모두, 제품 데이터를 AEM에 입력/가져온 경우에서 볼 수 있습니다. **제품** 콘솔. 다음은 제품의 카드 및 목록 보기에 다음과 같은 정보가 표시됩니다.

* 이미지
* sku 코드
* 마지막 수정 날짜

![chlimage_1-7](/help/sites-administering/assets/chlimage_1-7.png)

### 제품 변형 {#product-variants}

적절한 제품의 경우 변형에 대한 정보도 보유할 수 있습니다. 예를 들어 의류 품목의 경우 사용할 수 있는 다양한 색상이 변형으로 유지됩니다.

![ecommerceproductvariants](/help/sites-administering/assets/ecommerceproductvariants.png)

### 제품 속성 {#product-attributes}

각 제품에 대해 보유하고 있는 개별 속성은 사용 중인 eCommerce 엔진 및 AEM 구현에 따라 달라질 수 있습니다. 제품 페이지를 보거나 제품 정보를 편집할 때 적절히 사용할 수 있으며 다음 항목을 포함할 수 있습니다.

* **이미지**

  제품 이미지.

* **제목**

  제품 이름입니다.

* **설명**

  제품에 대한 텍스트 설명.

* **태그**

  관련 제품을 그룹화하는 데 사용되는 태그.

* **기본 자산 범주**

  에셋의 기본 카테고리입니다.

* **ERP 데이터**

  ERP(전사적 자원 관리) 정보

   * **SKU**

     SKU(Stock Keeping Unit) 정보.

   * **컬러**
   * **크기**
   * **가격**

     제품의 단가입니다.

* **요약**

  제품 기능에 대한 요약입니다.

* **기능**

  제품 기능에 대한 세부 정보.

### 제품 자산 {#product-assets}

개별 제품에 대해 다양한 자산을 보유할 수 있습니다. 일반적으로 여기에는 이미지와 비디오가 포함됩니다.

## 카탈로그 {#catalogs}

카탈로그는 손쉬운 관리와 쇼핑객의 표상을 위해 제품 데이터를 함께 그룹화합니다. 종종 카탈로그는 언어, 지리적 영역, 브랜드, 시즌, 취미, 스포츠 등의 속성에 따라 구성됩니다.

### 카탈로그 구조 {#catalog-structure}

#### 여러 언어의 카탈로그 {#catalogs-in-multiple-languages}

AEM은 여러 언어로 제품 콘텐츠를 지원합니다. 데이터를 요청할 때 통합 프레임워크는 현재 트리에서 언어를 검색합니다(예: `en_US` 아래 페이지의 경우 `/content/geometrixx-outdoors/en_US`).

다국어 저장소의 경우 각 언어 트리에 대한 카탈로그를 개별적으로 가져오거나 다음을 사용하여 복사할 수 있습니다. [MSM](/help/sites-administering/msm.md)).

#### 여러 브랜드에 대한 카탈로그 {#catalogs-for-multiple-brands}

언어와 마찬가지로, 대규모 다국적 기업은 여러 브랜드를 만족시켜야 합니다.

#### 태그별 카탈로그 {#catalogs-by-tags}

태그를 사용하여 제품을 카탈로그로 그룹화할 수도 있습니다. 시즌 오퍼와 같은 보다 동적인 카탈로그에 사용할 수 있습니다.

### 카탈로그 설정(초기 가져오기) {#catalog-setup-initial-import}

구현에 따라, 기본 카탈로그에 필요한 제품 데이터를 다음에서 AEM으로 가져올 수 있습니다.

* CSV 파일(일반 구현용)
* eCommerce 엔진

### 카탈로그 유지 관리(데이터 동기화) {#catalog-maintenance-data-synchronization}

제품 데이터의 추가 변경은 불가피합니다.

* 일반 구현의 경우 [제품 편집기](/help/commerce/cif-classic/administering/generic.md#editing-product-information)
* 를 사용할 때 [eCommerce 엔진 변경 사항을 동기화해야 함](#data-synchronization-with-an-ecommerce-engine-ongoing)

#### eCommerce 엔진을 사용한 데이터 동기화 (진행 중) {#data-synchronization-with-an-ecommerce-engine-ongoing}

최초 가져오기 이후에는 제품 데이터가 변경될 수 없습니다.

eCommerce 엔진을 사용하는 경우 제품 데이터가 유지되므로 AEM에서 사용할 수 있어야 합니다. 이 제품 데이터는 업데이트 시 동기화되어야 합니다.

이는 데이터 유형에 따라 달라질 수 있습니다.

* A [주기적 동기화는 변경 사항의 데이터 피드와 함께 사용됩니다](/help/commerce/cif-classic/developing/sap-commerce-cloud.md#product-synchronization-and-publishing).

  이 외에도 빠른 업데이트에 대한 특정 업데이트를 선택할 수 있습니다.

* 가격 정보와 같이 휘발성이 강한 데이터는 각 페이지 요청에 대해 상거래 엔진에서 검색되므로 항상 최신 상태로 유지됩니다.

### 카탈로그 - 성능 및 확장 {#catalogs-performance-and-scaling}

PIM(eCommerce 엔진)에서 제품(10만 개 이상)이 많은 대형 카탈로그를 가져오면 노드 수가 많아 시스템에 영향을 줄 수 있습니다. 제품에 연결된 에셋(예: 제품 이미지)이 있는 경우 작성 인스턴스 속도가 느려질 수도 있습니다. 이러한 에셋의 사후 처리가 CPU와 메모리를 많이 사용하기 때문입니다.

이러한 문제를 해결하기 위해 선택할 수 있는 다양한 전략이 있습니다.

* [버킷팅](#bucketing) - 많은 수의 노드를 충족하는 방법
* [자산 사후 처리를 전용 인스턴스로 오프로드합니다.](#offload-asset-post-processing-to-a-dedicated-instance)
* [제품 데이터만 가져오기](#only-import-product-data)
* [가져오기 조절 및 일괄 저장](#import-throttling-and-batch-saves)
* [성능 테스트](#performance-testing)
* [성능 - 기타](#performance-miscellaneous)

#### 버킷팅 {#bucketing}

JCR 노드에 직접 하위 노드가 많은 경우(예: 1000개 이상), 성능에 영향을 주지 않도록 버킷(가상 폴더)이 필요합니다. 가져올 때 알고리즘에 따라 생성됩니다.

이러한 버킷은 카탈로그 구조에 도입된 팬텀 폴더 형태를 취하지만 공개 URL에서 명확하지 않도록 구성할 수 있습니다.

#### 자산 사후 처리를 전용 인스턴스로 오프로드합니다. {#offload-asset-post-processing-to-a-dedicated-instance}

이 시나리오에는 두 작성자 인스턴스 설정이 포함됩니다.

1. 기본 작성자 인스턴스

   자산 경로에 대한 사후 처리가 비활성화된 PIM에서 제품 데이터를 가져옵니다.

1. 전용 DAM 작성자 인스턴스

   PIM에서 제품 자산을 가져오고 사후 처리한 다음 마스터 작성자 인스턴스에 다시 복제하여 사용합니다.

![아키텍처 다이어그램](/help/sites-administering/assets/chlimage_1-8.png)

#### 제품 데이터만 가져오기 {#only-import-product-data}

제품에 가져올 에셋(이미지)이 없는 경우 에셋 후처리의 영향을 받지 않고 제품 데이터를 가져올 수 있습니다.

![아키텍처 다이어그램](/help/sites-administering/assets/chlimage_1-9.png)

#### 성능 테스트 {#performance-testing}

AEM eCommerce 구현에서 성능 테스트를 고려해야 합니다.

* 작성자 환경:

  배경(예: 가져오기) 활동은 일반 사용자 활동(예: 페이지 편집)과 동시에 발생할 수 있으며, 프론트엔드 성능이 일반적으로 높더라도 온라인 작성자가 볼 수 있는 좋지 않은 성능은 Go-Live 결정을 차단할 수 있는 불편을 초래할 수 있습니다.

* 게시 환경:

  복제는 콘텐츠가 빠르고 안정적으로 게시되도록 하는 중요한 프로세스입니다. 이는 작성자가 게시할 콘텐츠를 그룹화하는 방식에 의해 영향을 받을 수 있습니다.

* 프론트엔드:

  프런트엔드와 캐시 무효화가 혼합되어 성능이 저하될 수 있습니다. 테스트는 이러한 문제를 방지하는 데 도움이 됩니다.

이 성능 테스트를 수행하려면 타겟에 대한 지식과 분석이 필요합니다.

* 컨텐츠 볼륨

   * 자산
   * 현지화된 I18ned 제품 및 SKU

* 사용자 활동:

   * 일괄 편집
   * 벌크 게시
   * 집중 검색 요청

* 백그라운드 프로세스

   * 가져오기
   * 동기화 업데이트(예: 가격 책정)

* 유지 관리 요구 사항(백업, Tar PM 최적화, 데이터스토어 가비지 수집 등)

#### 성능 - 기타 {#performance-miscellaneous}

모든 구현의 경우 다음 사항을 염두에 둘 수 있습니다.

* 제품, 재고 유지 단위 및 범주가 많을 수 있으므로 콘텐츠를 모델링하는 데 가능한 최소 노드 수를 사용하려고 합니다.

  노드가 많을수록 콘텐츠가 더 유연해집니다(예: parsys). 그러나 모든 것이 상충되는 것이며 (예:) 30K 제품을 조작할 때 기본적으로 개별 유연성이 필요합니까?

* 가능한 한 중복을 피하십시오(현지화 참조). 또는 중복을 피하는 경우 중복이 연결되는 노드 수를 생각해 보십시오.
* 쿼리 최적화를 준비하기 위해 가능한 한 콘텐츠에 태깅해 보십시오.

  예를 들면 다음과 같습니다.

  `/content/products/france/fr/shoe/reebok/pump/46 SKU`

  는 콘텐츠 수준(즉, 국가, 언어, 카테고리, 브랜드, 제품)당 하나의 태그를 가져야 합니다. 검색 중

  `//element(*,my:Sku)[@country='france' and @language='fr'`

  및

  `@category='shoe' and @brand='reebok' and @product='pump']`

  검색보다 훨씬 빠릅니다.

  `/jcr:root/content/france/fr/shoe/reebok/pump/element(*,my:Sku)`

* 기술 스택에서 팩터화된 콘텐츠 액세스 모델 및 서비스를 계획합니다. 이는 일반적인 모범 사례이지만 여기서는 최적화 단계에서 자주 읽는(그리고 번들 캐시를 채우지 않으려는) 데이터에 대한 애플리케이션 캐시를 추가할 수 있으므로 더욱 중요합니다.

  예를 들어 속성 관리는 제품 가져오기를 통해 업데이트되는 데이터와 관련이 있으므로 캐싱에 좋은 후보인 경우가 많습니다.
* 사용 고려 [프록시 페이지](#proxy-pages).

### 카탈로그 섹션 페이지 {#catalog-section-pages}

카탈로그 섹션에는 예를 들어 다음과 같은 내용이 있습니다.

* 카테고리에 대한 소개(이미지 및/또는 텍스트). 이는 배너 및 티저가 특별 오퍼를 홍보하는 데 사용할 수도 있습니다.
* 해당 카테고리의 개별 제품에 대한 링크
* 다른 범주에 대한 링크

![ecommerce_categoryrunning](/help/sites-administering/assets/ecommerce_categoryrunning.png)

### 제품 페이지 {#product-pages}

제품 페이지는 개별 제품에 대한 포괄적인 정보를 제공합니다. 의 동적 업데이트도 반영됩니다(예: eCommerce 엔진에 등록된 가격 변경).

제품 페이지는 다음을 사용하는 AEM 페이지입니다. **제품** 구성 요소(예: **상거래 제품** 템플릿:

![ecommerce_nairobirunnersgreen](/help/sites-administering/assets/ecommerce_nairobirunnersgreen.png)

제품 구성 요소는 다음을 제공합니다.

* 텍스트 및 이미지를 포함한 일반 제품 정보.
* 가격 책정: 페이지가 표시/새로 고쳐질 때마다 eCommerce 엔진에서 검색됩니다.
* 색상 및 크기와 같은 제품 변형 정보.

이 정보를 통해 장바구니에 품목을 추가할 때 구매자는 다음을 선택할 수 있습니다.

* 색상 및 크기 변형
* 수량

#### 제품 랜딩 페이지 {#product-landing-pages}

이러한 페이지는 주로 정적 정보를 제공하는 AEM 페이지입니다(예: 기본 제품 페이지에 대한 링크가 포함된 소개 및 개요).

### 제품 구성 요소 {#product-component}

다음 **제품** 구성 요소는 필요한 메타데이터(즉, 경로)를 제공하는 상위 페이지가 있는 모든 페이지에 추가할 수 있습니다. `cartPage` 및 `cartObject`). 데모 사이트, Geometrixx Outdoors에서 다음에서 제공합니다. `UserInfo.jsp`.

다음 **제품** 개별 요구 사항에 따라 구성 요소를 사용자 정의할 수도 있습니다.

### 프록시 페이지 {#proxy-pages}

프록시 페이지는 저장소 구조를 단순화하고 대형 카탈로그의 저장소를 최적화하는 데 사용됩니다.

AEM 내에서 업데이트하고 사용자 정의할 수 있는 각 제품에 대한 개별 구성 요소를 제공하므로 카탈로그를 만들려면 제품당 10개의 노드가 사용됩니다. 카탈로그에 수백 개 또는 수천 개의 제품이 포함된 경우 이러한 많은 수의 노드가 문제가 될 수 있습니다. 문제를 방지하기 위해 프록시 페이지를 사용하여 카탈로그를 만들 수 있습니다.

프록시 페이지는 2노드 구조( `cq:Page` 및 `jcr:content`) 실제 제품 컨텐츠를 포함하지 않습니다. 요청 시 제품 데이터와 템플릿 페이지를 참조하여 콘텐츠가 생성됩니다.

그러나, 상충되는 것이 있다. AEM 내에서 제품 정보를 사용자 정의할 수 없습니다. 표준 템플릿(사이트에 대해 정의됨)이 사용됩니다.

>[!NOTE]
>
>프록시 페이지 없이 큰 카탈로그를 가져오면 문제가 발생하지 않습니다.
>
>언제든지 한 방법론에서 다른 방법론으로 변환할 수 있습니다. 카탈로그의 하위 섹션을 변환할 수도 있습니다.

## 프로모션 및 바우처 {#promotions-and-vouchers}

### 바우처 {#vouchers}

바우처는 구매 고객을 유도하고 고객의 충성도에 대한 보상을 제공하기 위해 노력하고 테스트된 할인 제공 방법입니다.

* 바우처 공급:

   * 바우처 코드(구매자가 장바구니에 입력).
   * 바우처 레이블(쇼핑객이 장바구니에 입력한 후 표시됨).
   * 프로모션 경로(바우처가 적용되는 작업을 정의함).

* 외부 상거래 엔진은 바우처를 제공할 수도 있다.

AEM:

* 바우처는 웹 사이트 콘솔로 생성/편집되는 페이지 기반 구성 요소입니다.
* 다음 **바우처** 구성 요소는 다음을 제공합니다.

   * 바우처 관리를 위한 렌더러입니다. 현재 장바구니에 있는 바우처가 표시됩니다.
   * 바우처를 관리(추가/제거)하기 위한 편집 대화 상자(양식).
   * 장바구니에서 바우처를 추가/제거하는 데 필요한 작업입니다.

* 바우처는 날짜/시간 및 시간이 다르지만 부모 캠페인의 항목을 사용합니다.

>[!NOTE]
>
>AEM에서는 **바우처**, 이는 용어와 동의어입니다 **쿠폰**.

### 프로모션 {#promotions}

바우처와 함께 프로모션을 통해 다음과 같은 시나리오를 실현할 수 있습니다.

* 회사는 직원을 위해 사용자 지정 가격을 제공하며, 이는 수작업으로 만들어진 사용자 목록입니다.
* 장기 고객은 모든 주문에 대해 할인을 받습니다.
* 잘 정의된 기간 동안 제공되는 판매 가격.
* 고객은 이전 주문이 특정 금액을 초과하는 경우 바우처를 받습니다.
* 구입하는 고객 *product-X* 은(는) 다음에 대한 할인을 제공합니다. *product-Y* (제품 쌍).

프로모션은 제품 정보 관리자가 아닌 마케팅 관리자가 관리합니다.

* 프로모션은 웹 사이트 콘솔로 생성/편집되는 페이지 기반 구성 요소입니다. &quot;
* 판촉 공급:

   * 우선 순위
   * 프로모션 핸들러 경로

* 프로모션을 캠페인에 연결하여 설정/해제 날짜/시간을 정의할 수 있습니다.
* 프로모션을 경험에 연결하여 세그먼트를 정의할 수 있습니다.
* 경험에 연결되지 않은 프로모션은 저절로 실행되지는 않지만 바우처로 실행할 수 있습니다.
* 프로모션 구성 요소에는 다음이 포함됩니다.

   * 프로모션 관리용 렌더러 및 대화 상자
   * 프로모션 핸들러와 관련된 구성 매개 변수를 렌더링 및 편집하기 위한 하위 구성 요소

AEM에서 프로모션도 [Campaign Management](/help/sites-authoring/personalization.md):

* a [campaign](/help/sites-authoring/personalization.md) 설정/해제 시간 지정
* [경험](/help/sites-authoring/personalization.md) *다음 범위 내* 캠페인은 에셋이 해당되는 대상 세그먼트에 따라 에셋(티저 페이지, 프로모션 등)을 그룹화하는 데 사용됩니다

프로모션은 경험 또는 캠페인에서 직접 수행할 수 있습니다.

* 프로모션이 경험에 유지되면 대상 세그먼트에 자동으로 적용할 수 있습니다.

  예를 들어 geometrixx-outdoors 샘플 사이트에서 프로모션은 다음과 같습니다.

  `/content/campaigns/geometrixx-outdoors/big-spender/ordervalueover100/free-shipping`

  가 경험에 있으므로 세그먼트( `ordervalueover100`)가 해결됩니다.

* 프로모션이 경험 내에 표시되지 않는 경우(캠페인에서만) 대상에 자동으로 적용할 수 없습니다. 그러나 구매자가 장바구니에 바우처를 입력하고 해당 바우처가 프로모션을 참조하는 경우 여전히 실행될 수 있습니다.

  예를 들어 프로모션:

  `/content/campaigns/geometrixx-outdoors/article/10-bucks-off`

  은 경험 외부에 있으므로 자동으로 실행되지 않습니다(즉, 세그멘테이션에 따라). 그러나 문서 캠페인 내의 여러 경험에서 찾을 수 있는 바우처에서 참조됩니다. 이러한 바우처 코드를 장바구니에 입력하면 프로모션이 실행됩니다.

>[!NOTE]
>
>[hybris 프로모션](https://www.hybris.com/modules/promotion) 및 [hybris 바우처](https://www.hybris.com/en/modules/voucher) 장바구니에 영향을 주고 가격과 관련된 모든 항목을 다룹니다. 프로모션별 마케팅 콘텐츠(배너 등) 은 hybris 프로모션의 일부가 아닙니다.

## 개인화 {#personalization}

### 고객 등록 및 계정 {#customer-registration-and-accounts}

쇼핑객이 등록할 때 계정 세부 사항을 AEM과 eCommerce 엔진 간에 동기화해야 합니다. 중요한 데이터는 독립적으로 유지되지만 프로필은 공유됩니다.

![chlimage_1-10](/help/sites-administering/assets/chlimage_1-10.png)

정확한 메커니즘은 시나리오에 따라 달라질 수 있습니다.

1. 사용자 계정은 두 시스템 모두에 있습니다.

   1. 필요한 작업이 없습니다.

1. 사용자 계정은 AEM에만 존재합니다.

   1. 사용자는 AEM에 저장될 동일한 계정 ID와 임의의 암호로 eCommerce 엔진에서 생성됩니다.
   1. AEM이 첫 번째 호출 시 eCommerce 엔진에 로그인하려고 하므로 무작위 암호가 필요합니다(예: 제품 페이지가 요청되고 가격에 대해 eCommerce 엔진이 참조되는 경우). 이 문제는 AEM 로그인 후에 발생하므로 암호를 사용할 수 없습니다.

1. 사용자 계정은 eCommerce 엔진에만 존재합니다.

   1. 계정은 계정 ID와 암호가 동일한 AEM에서 만들어집니다.

eCommerce 엔진을 사용하는 경우 AEM은 계정 ID와 암호(선택적으로 사용자 그룹)만 저장합니다. 다른 모든 정보는 eCommerce 엔진에 저장됩니다.

>[!NOTE]
>
>eCommerce 엔진을 사용하는 경우 AEM 인스턴스에 로그인하는 사용자에 대해 생성된 계정이 해당 엔진과 통신하는 다른 AEM 인스턴스에 (예: 워크플로우를 통해) 복제되도록 해야 합니다.
>
>그렇지 않으면 이러한 다른 AEM 인스턴스도 엔진에서 동일한 사용자에 대한 계정을 만들려고 합니다. 이 작업은 실패하고 `DuplicateUidException` 엔진에서 오고있어

### 고객 등록 {#customer-sign-up}

쇼핑객이 장바구니에 액세스하려면 종종 가입해야 합니다. 이렇게 하려면 고객별 계정을 만들 수 있도록 등록(계정 만들기)이 필요합니다.

![chlimage_1-11](/help/sites-administering/assets/chlimage_1-11.png)

>[!NOTE]
>
>익명 장바구니 및 체크아웃도 지원됩니다.

### 고객 로그인 {#customer-sign-in}

가입 후 구매자는 자신의 행동을 추적하고 주문을 이행할 수 있도록 자신의 계정으로 로그인할 수 있습니다.

![chlimage_1-12](/help/sites-administering/assets/chlimage_1-12.png)

### 단일 사인온 {#single-sign-on}

SSO(Single Sign-On)가 제공되므로 작성자는 두 번 로그인할 필요 없이 AEM과 전자 상거래 시스템 모두에서 알 수 있습니다.

### myAccount {#myaccount}

전자 상거래 엔진의 거래 데이터는 쇼핑객에 대한 개인 정보와 결합됩니다. AEM은 이 데이터 중 일부를 프로필 데이터로 사용합니다. AEM의 양식 작업은 eCommerce 엔진에 정보를 다시 기록합니다.

계정 정보를 쉽게 관리할 수 있는 페이지가 있습니다. 다음을 클릭하여 액세스할 수 있습니다. **내 계정** Geometrixx 페이지 맨 위에서 또는 로 이동하여 `/content/geometrixx-outdoors/en/user/account.html`.

![chlimage_1-13](/help/sites-administering/assets/chlimage_1-13.png)

### 주소록 {#address-book}

사이트에는 게재, 청구 및 대체 주소를 포함하여 다양한 주소를 저장해야 합니다. 기본 주소 형식을 기반으로 하는 양식을 사용하여 구현하거나 AEM에서 제공하는 주소록 구성 요소를 사용할 수 있습니다.

이 주소록 구성 요소를 사용하여 다음을 수행할 수 있습니다.

* 장부의 주소 편집
* 배송 주소 장부에서 주소 선택
* 청구 주소 장부에서 주소 선택

기본으로 원하는 주소를 선택할 수 있습니다.

주소록 구성 요소는 **내 계정** 클릭하여 페이지 만들기 **주소록** 또는 로 이동하여 `/content/geometrixx-outdoors/en/user/account/address-book.html`.

![chlimage_1-14](/help/sites-administering/assets/chlimage_1-14.png)

다음을 클릭할 수 있습니다. **새 주소 추가...** 주소록에 주소를 추가합니다. 양식을 열고 을 입력한 다음 **주소 추가**.

>[!NOTE]
>
>주소록에 여러 개의 주소를 입력할 수 있습니다.

주소록은 장바구니를 &quot;체크아웃&quot;할 때 사용됩니다.

![chlimage_1-15](/help/sites-administering/assets/chlimage_1-15.png)

주소는 아래에 유지됩니다. `user_home/profile/addresses`.
예를 들어 Alison Parker의 경우 /home/users/geometrixx/aparker@geometrixx.info/profile/addresses 아래에 있습니다.

원하는 주소를 기본값으로 선택할 수 있습니다. 이 정보는 주소가 아닌 구매자 프로필에서 유지됩니다. 프로필 속성 `address.default` 값에 대해 선택한 주소의 경로로 설정됩니다.

### 고객별 가격 {#customer-specific-pricing}

전자 상거래 엔진은 컨텍스트(기본적으로 쇼핑객 정보)를 사용하여 보유 중인 가격을 결정한 다음 올바른 정보를 AEM에 다시 제공합니다.

## 장바구니 및 주문 {#shopping-cart-and-orders}

쇼핑할 때, 쇼핑객은 제품 페이지를 열람하고 장바구니에 넣을 항목을 선택합니다. 체크아웃을 진행할 때 주문을 넣을 수 있습니다.

### 익명 쇼핑객 {#anonymous-shoppers}

익명의 고객은 다음과 같은 작업을 수행할 수 있습니다.

* 제품 보기
* 장바구니에 제품 추가
* 체크아웃을 수행하여 주문

>[!NOTE]
>
>인스턴스 주소 정보의 구성에 따라 체크아웃하기 전에 고객 등록이 필요할 수 있습니다.

### 등록된 쇼핑객 {#registered-shoppers}

등록된 고객은 다음과 같은 작업을 수행할 수 있습니다.

* 해당 계정에 로그인
* 제품 보기
* 장바구니에 제품 추가
* 체크아웃을 수행하여 주문
* 이전 주문 보기 및 추적

### 장바구니 컨텐츠 개요 {#shopping-cart-content-overview}

장바구니에서 제공하는 사항:

* 선택한 항목에 대한 개요
* 선택한 항목에 대한 제품 페이지 링크
* 기능:

   * 개별 품목의 수/수량을 업데이트합니다.
   * 개별 항목 제거

![ecommerce_shoppingcart](/help/sites-administering/assets/ecommerce_shoppingcart.png)

장바구니는 사용 중인 엔진에 따라 저장됩니다.

* AEM 일반은 쿠키에 장바구니를 저장합니다.
* 특정 전자 상거래 엔진은 장바구니를 세션에 저장할 수 있습니다.

두 경우 모두, 항목이 로그인/로그아웃(동일한 컴퓨터/브라우저에만 있음) 동안 장바구니에 유지되며(및 복원할 수 있음), 예를 들면 다음과 같습니다.

* 다음으로 찾아보기 `anonymous` 장바구니에 제품 추가
* 다음으로 로그인 `Allison Parker` - 앨리슨의 카트가 비어 있음
* 앨리슨의 장바구니에 제품 추가
* 로그아웃 - 장바구니에 의 제품이 표시됩니다. `anonymous`

* 다음으로 다시 로그인 `Allison Parker` - 앨리슨의 제품이 복원되었습니다.

>[!NOTE]
>
>익명 장바구니는 동일한 컴퓨터/브라우저에서만 복원할 수 있습니다.

>[!NOTE]
>
>를 사용하여 장바구니 콘텐츠를 복원하지 않는 것이 좋습니다. `admin` 계정과 충돌할 수 있으므로 `admin` eCommerce 엔진의 계정(예: hybris).

>[!NOTE]
>
>지정된 기간 후에 보류 중인 카트를 제거하도록 hybris를 구성할 수 있습니다.

체크아웃 전에는 가격 변경이 발생할 때 두 시스템에 모두 반영됩니다.

### 주문 정보 {#order-information}

eCommerce 엔진 또는 AEM에 보관된 주문에 대한 구현 정보에 따라 이 정보는 AEM에 의해 렌더링됩니다.

다음과 같은 다양한 정보가 저장됩니다.

* **주문 ID**

  주문에 대한 참조 번호입니다.

* **주문 날짜**

  주문이 이루어진 날짜.

* **상태**

  주문 상태(예: 출하됨)

* **통화**

  주문 통화입니다.

* **컨텐츠 항목**

  주문한 항목 목록입니다.

* **소계**

  주문한 항목의 총 비용.

* **세금**

  주문에 대해 납부해야 하는 세금 금액.

* **배송**

  배송비.

* **합계**

  주문의 총 금액(주문 품목, 세금 및 배송).

* **청구 주소**

  송장을 보낼 주소.

* **결제 토큰**

  결제 방법.

* **결제 상태**

  결제 상태.

* **배송 주소**

  상품을 선적해야 하는 주소.

* **배송 방법**

  운송 방법(예: 육상, 해상 또는 항공).

* **추적 번호**

  배송 회사에서 사용하는 모든 추적 번호.

* **추적 링크**

  배송 중 주문 추적에 사용되는 링크입니다.

>[!NOTE]
>
>순서 만들기 마법사에 사용되는 필드는 해당 위치에 대해 정의된 터치에 적합한 스캐폴딩이 있는지에 따라 다릅니다. 일반적인 예에서 찾을 수 있는 위치:
>`/etc/scaffolding/geometrixx-outdoors/order/jcr:content/cq:dialog`

주문이 AEM 내에서 보류되면 주문 콘솔에는 각 주문에 대한 다음 사항이 표시됩니다.

* 장바구니에 있는 항목 수
* 주문의 총 값
* 주문 날짜
* 상태

![chlimage_1-16](/help/sites-administering/assets/chlimage_1-16.png)

### 주문 추적 {#order-tracking}

주문 후 쇼핑객은 종종 다음 주소로 돌아옵니다.

* 주문 상태 확인
* 주문에서 제품 제거
* 주문에 제품 추가

주문 배송을 받은 후 구매자는 일정 기간 동안 이루어진 주문 내역을 확인하고자 할 수도 있습니다.

주문 이행 및 추적은 eCommerce 엔진에서 관리합니다. 적용된 바우처 및 프로모션을 포함하여 모든 관련 세부 정보가 표시되는 주문 내역 구성 요소를 사용하여 AEM에서 정보를 표시할 수 있습니다. 예를 들면 다음과 같습니다.

![chlimage_1-17](/help/sites-administering/assets/chlimage_1-17.png)

## 체크아웃 {#checkout}

체크아웃은 표준 AEM Forms를 사용하여 구현됩니다. 이렇게 하면 마케팅 관리자는 마케팅 콘텐츠를 사용하여 경험을 사용자 지정할 수 있습니다.

그런 다음 eCommerce에서는 AEM Forms의 입력을 통해 체크아웃 프로세스를 관리합니다.

### 결제 보안 {#payment-security}

신용 카드 정보를 포함한 결제 세부 사항은 종종 eCommerce 엔진에서 관리합니다. AEM은 이러한 트랜잭션 정보를 엔진에 전달합니다(여기서 결제 처리 서비스로 전달됨).

PCI(Payment Card Industry) 규정을 준수할 수 있습니다.

### 주문 확인 {#confirmation-of-order}

주문이 화면에서 확인되며 [주문 추적](#order-tracking).

## 검색 {#search-features}

![chlimage_1-18](/help/sites-administering/assets/chlimage_1-18.png)

AEM은 제품에 표준 페이지를 사용하므로 표준 검색 구성 요소를 사용하여 검색 페이지를 만들 수 있습니다.

보다 철저한 구현이 필요한 경우 다음 중 하나를 수행할 수 있습니다.

* 필요한 기능을 사용하여 기본 검색 구성 요소를 확장합니다.
* 에서 검색 방법 구현 `CommerceService` 그런 다음 검색 페이지에서 eCommerce 검색 구성 요소를 사용합니다.

eCommerce 엔진을 사용하는 경우 eCommerce 검색 API가 eCommerce 엔진 솔루션에서 완전히 구현될 수 있으므로 즉시 사용할 수 있도록 제공되는 eCommerce 검색 구성 요소를 사용할 수 있습니다. 면처리 검색을 사용하여 JCR 및/또는 엔진을 검색할 수 있습니다.
