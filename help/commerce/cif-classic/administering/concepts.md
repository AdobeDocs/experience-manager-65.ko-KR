---
title: 개념
description: AEM을 사용한 eCommerce의 일반 개념.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: 290b2af6-257f-42f2-b809-1248227a4795
source-git-commit: 1cef6f87fa66fd78d439c23e6ac907f9531b8fd6
workflow-type: tm+mt
source-wordcount: '4525'
ht-degree: 2%

---

# 개념{#concepts}

통합 프레임워크는 다음을 위한 메커니즘 및 구성 요소를 제공합니다.

* eCommerce 엔진에 연결
* AEM에 데이터 가져오기
* 해당 데이터 표시 및 쇼핑객의 응답 수집
* 트랜잭션 세부 정보 반환
* 두 시스템에서 데이터를 검색합니다.

이것의 의미는 다음과 같습니다.

* 쇼핑객들은 기다리지 않고 등록 및 쇼핑을 할 수 있습니다.
* 가격 변경은 바로 쇼핑객들이 볼 수 있을 것이다.
* 필요에 따라 제품을 추가할 수 있습니다.

>[!NOTE]
>
>eCommerce 프레임워크는 다음과 같이 사용할 수 있습니다.
>
>* [Magento](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md)
>* [SAP Commerce Cloud](/help/commerce/cif-classic/administering/sap-commerce-cloud.md)
* [Salesforce Commerce Cloud](https://github.com/adobe/commerce-salesforce)



>[!CAUTION]
[eCommerce 통합 프레임워크](https://www.adobe.com/solutions/web-experience-management/commerce.html)는 AEM 추가 기능입니다.
영업 담당자는 해당 엔진에 따라 자세한 내용을 제공할 수 있습니다.

>[!CAUTION]
프레임워크는 사용자 자신의 프로젝트에 대한 기본 요구 사항을 제공합니다.
프레임워크를 사양에 맞게 조정하려면 항상 특정 양의 개발 작업이 필요합니다.

>[!CAUTION]
표준 AEM 설치에는 일반 AEM(JCR) eCommerce 구현이 포함되어 있습니다.
현재 데모 목적으로 사용하거나 요구 사항에 따라 사용자 지정 구현을 위한 기본 기반으로 사용됩니다.

운영을 최적화하기 위해 AEM과 eCommerce 엔진은 모두 고유한 전문 분야에 주력합니다. 실시간으로 양국 간에 정보가 전달된다.예:

* AEM의 기능은 다음과 같습니다.

   * 요청:

      * eCommerce 엔진의 제품 정보.
   * 제공:

      * 제품 정보, 장바구니 및 체크아웃에 대한 사용자 보기.
      * 장바구니 및 체크아웃 정보를 eCommerce 엔진에 제공합니다.
      * SEO(검색 엔진 최적화).
      * 커뮤니티 기능.
      * 구조화되지 않은 마케팅 상호 작용


* eCommerce 엔진은 다음 작업을 수행할 수 있습니다.

   * 제공:

      * 데이터베이스의 제품 정보입니다.
      * 제품 변형 관리.
      * 주문 관리.
      * ERP(Enterprise Resource Planning).
      * 제품 정보 내에서 검색합니다.
   * 프로세스:

      * 장바구니.
      * 체크아웃입니다.
      * 주문 이행.


>[!NOTE]
정확한 세부 사항은 eCommerce 엔진 및 프로젝트 구현에 따라 다릅니다.

통합 레이어를 사용하기 위해 즉시 사용 가능한 여러 AEM 구성 요소가 제공됩니다. 현재는 다음과 같습니다.

* 제품 정보
* 장바구니
* 체크아웃
* 내 계정

다양한 검색 옵션도 사용할 수 있습니다.

## 아키텍처 {#architecture}

통합 프레임워크는 기능을 보여주는 다양한 구성 요소인 API와 연결 방법의 예를 제공하기 위한 여러 확장을 제공합니다.

![chlimage_1-4](/help/sites-administering/assets/chlimage_1-4.png)

프레임워크를 통해 다음과 같은 기능에 액세스할 수 있습니다.

![chlimage_1-5](/help/sites-administering/assets/chlimage_1-5.png)

### 구현 {#implementations}

AEM eCommerce는 eCommerce 엔진을 사용하여 구현됩니다.

* eCommerce 통합 프레임워크를 AEM과 쉽게 통합할 수 있도록 빌드되었습니다. 기본 제공 eCommerce 엔진은 제품 데이터, 장바구니, 체크아웃 및 주문 이행을 제어하는 반면, AEM은 데이터 표시 및 마케팅 캠페인을 제어합니다.


>[!NOTE]
표준 AEM 설치에는 일반 AEM(JCR) eCommerce 구현이 포함되어 있습니다.
현재 데모 목적으로 사용하거나 요구 사항에 따라 사용자 지정 구현을 위한 기본 기반으로 사용됩니다.
JCR을 기반으로 하는 일반 개발을 사용하여 AEM 내에 구현된 AEM eCommerce는 다음과 같습니다.
* API의 사용을 보여주는 독립형 AEM 기본 eCommerce 예입니다. 기존 데이터 디스플레이 및 마케팅 캠페인과 함께 제품 데이터, 장바구니 및 체크아웃을 제어하는 데 사용할 수 있습니다. 이 경우 제품 데이터베이스는 AEM이 아닌 저장소에 저장됩니다(Adobe의 [JCR](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/index.html) 구현).

표준 AEM 설치에는 [일반 eCommerce 구현](/help/commerce/cif-classic/administering/generic.md)의 기본 사항이 포함되어 있습니다.

### 상거래 공급자 {#commerce-providers}

상거래 엔진에서 AEM eCommerce 사이트로 데이터를 가져오는 경우 상거래 공급자가 데이터를 가져오기 위해 사용됩니다. 한 전자 상거래 공급자가 여러 가져오기 프로그램을 지원할 수 있습니다.

전자 상거래 공급자는 다음 중 하나로 사용자 지정된 AEM 코드입니다.

* 백엔드 상거래 엔진에 대한 인터페이스
* JCR 저장소 위에 상거래 시스템 구현

현재 AEM에 두 가지 전자 상거래 공급자를 사용할 수 있습니다.

* geometrixx hybris용 one
* geometrixx-generic(JCR)의 또 다른 기능입니다

일반적으로 프로젝트는 PIM 및 제품 데이터 스키마와 관련된 고유한 사용자 지정 상거래 공급자를 개발해야 합니다.

>[!NOTE]
geometrixx 가져오기 프로그램은 CSV 파일을 사용합니다.스키마 구현 위의 주석에는 수락된(사용자 지정 속성이 허용됨)에 대한 설명이 있습니다.

[ProductServicesManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/commerce/pim/api/ProductServicesManager.html)는 [ProductImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/commerce/pim/api/ProductImporter.html) 및 [CatalogBlueprintImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/commerce/pim/api/CatalogBlueprintImporter.html) 인터페이스의 구현 목록을 유지 관리합니다([OSGi](/help/sites-deploying/configuring.md#osgi-configuration-settings) 사용). 이러한 항목은 가져오기 마법사의 **Importer/Commerce Provider** 드롭다운 필드에 나열되어 있습니다( `commerceProvider` 속성을 이름으로 사용).

드롭다운에서 특정 가져오기/상거래 공급자를 사용할 수 있는 경우, 다음 중 하나에서 필요한 모든 보충 데이터를(가져오기 유형에 따라) 정의해야 합니다.

* `/apps/commerce/gui/content/catalogs/importblueprintswizard/importers`
* `/apps/commerce/gui/content/products/importproductswizard/importers`

적절한 `importers` 폴더 아래의 폴더는 가져오기 이름;과 일치해야 합니다.예:

* `.../importproductswizard/importers/geometrixx/.content.xml`

소스 가져오기 파일의 형식은 가져오기가 정의합니다. 또는 가져오기를 통해 상거래 엔진에 연결(예: WebDAV 또는 http)을 설정할 수 있습니다.

## 역할 {#roles}

통합 시스템은 데이터를 유지 관리하기 위해 다음 역할을 제공합니다.

* PIM(제품 정보 관리) 사용자:

   * 제품 정보.
   * 분류, 분류, 승인
   * 디지털 자산 관리와 상호 작용합니다.
   * 가격 책정 - 대개 ERP 시스템에서 비롯되며 상거래 시스템에서 명시적으로 유지되지 않습니다.

* 다음을 유지 관리하는 작성자/마케팅 관리자

   * 모든 채널에 대한 마케팅 콘텐츠입니다.
   * 프로모션.
   * 바우처.
   * 캠페인.

* 서퍼/쇼핑객:

   * 제품 정보를 봅니다.
   * 장바구니에 항목을 넣습니다.
   * 그들의 주문을 체크아웃합니다.
   * 주문 이행 예상

그러나 실제 위치는 구현에 따라 달라질 수 있습니다.예를 들어, 일반 또는 eCommerce 엔진을 사용하는 경우

![chlimage_1-6](/help/sites-administering/assets/chlimage_1-6.png)

## 제품 {#products}

### 제품 데이터 및 마케팅 데이터 {#product-data-versus-marketing-data}

#### 구조적 및 마케팅 카테고리 {#structural-versus-marketing-categories}

다음 두 카테고리를 구별할 수 있는 경우 의미 있는 구조(`cq:Page` 노드의 트리)로 명확한 URL을 만들 수 있으므로 클래식 AEM 컨텐츠 관리에 매우 근접할 수 있습니다.

* *구조 *카테고리

   *제품*&#x200B;을 정의하는 카테고리 트리예:

   `/products/mens/shoes/sneakers`

* ** 마케팅 카테고리

   *제품이*&#x200B;에 속할 수 있는 다른 모든 카테고리예:

   `/special-offers/christmas/shoes`)

### 제품 데이터 {#product-data}

제품을 표시 및 관리하기 위해서는 제품에 대한 다양한 정보를 보유해야 합니다.

제품 데이터는 다음과 같습니다.

* AEM(일반)에서 직접 유지
* 는 eCommerce 엔진에서 유지, AEM에서 사용 가능하게 되었습니다.

   데이터 유형에 따라 필요에 따라 [동기화된](#catalog-maintenance-data-synchronization)이거나 직접 액세스됩니다.예를 들어 제품 가격과 같은 휘발성 및 중요 데이터는 항상 최신 상태인지 확인하기 위해 모든 페이지 요청 시 전자 상거래 엔진에서 검색됩니다.

어느 경우든지 제품 데이터를 AEM에 입력/가져온 경우 **Products** 콘솔에서 볼 수 있습니다. 다음은 다음과 같은 제품 표시 정보의 카드 및 목록 보기입니다.

* 이미지
* SKU 코드
* 마지막으로 수정한 날짜

![chlimage_1-7](/help/sites-administering/assets/chlimage_1-7.png)

### 제품 변형 {#product-variants}

적절한 제품 정보에 대해 변형을 저장할 수도 있습니다. 예를 들어, 의류 항목의 경우 사용할 수 있는 다양한 색상을 변형으로 보유합니다.

![ecommerceproductvariants](/help/sites-administering/assets/ecommerceproductvariants.png)

### 제품 속성 {#product-attributes}

각 제품에 대한 개별 속성은 사용되는 eCommerce 엔진 및 AEM 구현에 따라 달라질 수 있습니다. 제품 페이지를 보거나 제품 정보를 편집할 때 적절히 사용할 수 있으며 다음이 포함될 수 있습니다.

* **이미지**

   제품의 이미지입니다.

* **제목**

   제품 이름입니다.

* **설명**

   제품에 대한 텍스트 설명입니다.

* **태그**

   관련 제품을 그룹화하는 데 사용되는 태그.

* **기본 자산 카테고리**

   자산에 대한 기본 카테고리입니다.

* **ERP 데이터**

   ERP(전사적 자원 관리) 정보

   * **SKU**

      재고 관리 단위(SKU) 정보.

   * **색상**
   * **크기**
   * **가격**

      제품의 단가입니다.

* **요약**

   제품 기능에 대한 요약입니다.

* **기능**

   제품 기능에 대한 전체 세부 사항입니다.

### 제품 자산 {#product-assets}

개별 제품에 대해 다양한 자산을 보유할 수 있습니다. 일반적으로 여기에는 이미지와 비디오가 포함됩니다.

## 카탈로그 {#catalogs}

카탈로그에서는 간편한 관리와 소비자에 대한 표현을 위해 제품 데이터를 함께 그룹화합니다. 종종 카탈로그는 언어, 지리적 지역, 브랜드, 시즌, 취미, 스포츠 등과 같은 속성들에 따라 구성되어 있습니다.

### 카탈로그 구조 {#catalog-structure}

#### 여러 언어로 된 카탈로그 {#catalogs-in-multiple-languages}

AEM은 여러 언어로 제품 콘텐츠를 지원합니다. 데이터를 요청할 때 통합 프레임워크는 현재 트리에서 언어를 검색합니다(예: `/content/geometrixx-outdoors/en_US` 아래의 페이지에 대해 `en_US`).

다국어 저장소의 경우 각 언어 트리에 대한 카탈로그를 개별적으로 가져오거나 [MSM](/help/sites-administering/msm.md)을 통해 복사할 수 있습니다.

#### 여러 브랜드에 대한 카탈로그 {#catalogs-for-multiple-brands}

언어에서와 마찬가지로, 대형 다국적 기업은 여러 브랜드를 대상으로 해야 할 수 있습니다.

#### 태그별 카탈로그 {#catalogs-by-tags}

태그를 사용하여 제품을 카탈로그로 그룹화할 수도 있습니다. 이러한 매개 변수는 계절별 오퍼와 같은 보다 다이내믹한 카탈로그에 사용할 수 있습니다.

### 카탈로그 설정(초기 가져오기) {#catalog-setup-initial-import}

구현에 따라 기본 카탈로그에 필요한 제품 데이터를 다음에서 AEM으로 가져올 수 있습니다.

* CSV 파일(일반 구현용)
* eCommerce 엔진

### 카탈로그 유지 관리(데이터 동기화) {#catalog-maintenance-data-synchronization}

제품 데이터에 대한 추가 변경은 불가피하다.

* 일반 구현의 경우 [제품 편집기](/help/commerce/cif-classic/administering/generic.md#editing-product-information)로 관리할 수 있습니다.
* [eCommerce 엔진을 사용하는 경우 변경 사항을 동기화해야 합니다](#data-synchronization-with-an-ecommerce-engine-ongoing)

#### 전자 상거래 엔진과 데이터 동기화(진행 중) {#data-synchronization-with-an-ecommerce-engine-ongoing}

초기 가져오기 후 제품 데이터를 변경하는 것은 필수입니다.

eCommerce 엔진을 사용하는 경우 제품 데이터가 여기에서 유지되므로 AEM에서 사용할 수 있어야 합니다. 업데이트가 있을 때 이 제품 데이터를 동기화해야 합니다.

이는 데이터 유형에 따라 달라질 수 있습니다.

* [주기적 동기화는 ](/help/commerce/cif-classic/developing/sap-commerce-cloud.md#product-synchronization-and-publishing)의 데이터 피드와 함께 사용됩니다.

   이 외에도 빠른 업데이트를 위한 특정 업데이트를 선택할 수 있습니다.

* 가격 정보와 같은 휘발성이 높은 데이터는 항상 최신 상태가 되도록 각 페이지 요청에 대해 상거래 엔진에서 검색됩니다.

### 카탈로그 - 성능 및 비율 {#catalogs-performance-and-scaling}

PIM(eCommerce Engine)에서 많은 제품(일반적으로 10만 개 이상)이 있는 큰 카탈로그를 가져오는 것은 많은 노드로 인해 시스템에 영향을 줄 수 있습니다. 제품에 연결된 자산(예: 제품 이미지)이 있는 경우 작성 인스턴스의 속도를 저하할 수도 있습니다. 이는 이러한 자산의 사후 처리가 CPU와 메모리를 많이 사용하기 때문입니다.

이러한 문제를 해결하기 위해 선택할 수 있는 다양한 전략이 있습니다.

* [버킷](#bucketing)  - 많은 수의 노드를 처리하기 위한 것입니다.
* [전용 인스턴스로 자산 사후 처리 오프로드](#offload-asset-post-processing-to-a-dedicated-instance)
* [제품 데이터만 가져오기](#only-import-product-data)
* [전송률 조절 및 배치 저장 가져오기](#import-throttling-and-batch-saves)
* [성능 테스트](#performance-testing)
* [성능 - 기타](#performance-miscellaneous)

#### 그룹 {#bucketing}

JCR 노드에 많은 직접 하위 노드(예: 1000 이상)가 있는 경우 성능에 영향을 주지 않도록 버킷(phantom 폴더)이 필요합니다. 가져올 때 알고리즘에 따라 생성됩니다.

이러한 버킷은 카탈로그 구조에 도입된 팬텀 폴더 형태를 취하지만 공개 URL에서 잘 보이지 않도록 구성할 수 있습니다.

#### 자산 사후 처리를 전용 인스턴스 {#offload-asset-post-processing-to-a-dedicated-instance}로 오프로드합니다.

이 시나리오에는 두 개의 작성자 인스턴스를 설정하는 작업이 포함됩니다.

1. 기본 작성자 인스턴스

   자산 경로에 대한 사후 처리가 비활성화된 PIM에서 제품 데이터를 가져옵니다.

1. 전용 DAM 작성자 인스턴스

   PIM에서 제품 자산을 가져오고 사후 처리한 다음 다시 마스터 작성자 인스턴스에 복제하여 사용할 수 있습니다.

![아키텍처 다이어그램](/help/sites-administering/assets/chlimage_1-8.png)

#### 제품 데이터 {#only-import-product-data}만 가져오기

제품에 가져올 자산(이미지)이 포함되지 않은 경우 자산 사후 처리의 영향을 받지 않고 제품 데이터를 가져올 수 있습니다.

![아키텍처 다이어그램](/help/sites-administering/assets/chlimage_1-9.png)

#### 성능 테스트 {#performance-testing}

성능 테스트는 AEM eCommerce 구현에서 고려해야 합니다.

* 작성자 환경:

   배경(예: 가져오기) 활동은 일반 사용자 활동과 동시에 발생할 수 있으며(예: 페이지 편집) 프런트엔드 성능이 우선순위가 더 높더라도(일반적으로) 온라인 작성자가 나타내는 잘못된 성능이 불량하여, 라이브 결정을 차단할 수 있는 좌절감이 발생할 수 있습니다.

* 게시 환경:

   복제는 컨텐츠가 빠르고 안정적으로 게시되도록 하는 중요한 프로세스입니다. 이는 작성자가 게시할 컨텐츠를 그룹화하는 방식의 영향을 받을 수 있습니다.

* 프런트엔드:

   프런트 엔드와 캐시 무효화를 혼합하면 성능에 놀라운 결과를 초래할 수 있습니다. 테스트는 이러한 문제를 방지하는 데 도움이 됩니다.

이 성능 테스트에는 대상에 대한 지식과 분석이 필요합니다.

* 컨텐츠 볼륨

   * 자산
   * 현지화, I18end 제품 및 SKU

* 사용자 활동:

   * 벌크 편집
   * 벌크 게시
   * 강력한 검색 요청

* 백그라운드 프로세스

   * 가져오기
   * 동기화 업데이트(예: 가격 책정)

* 유지 관리 요구 사항(백업, Tar PM 최적화, 데이터 저장소 가비지 수집 등)

#### 성능 - 기타 {#performance-miscellaneous}

모든 구현의 경우 다음 사항을 염두에 둘 수 있습니다.

* 제품, 재고 관리 단위 및 카테고리는 다양할 수 있으므로 컨텐츠를 모델링하는 데 가능한 최소 수의 노드를 사용해 보십시오.

   노드가 클수록 컨텐츠가 유연해집니다(예: parsys). 그러나 모든 것은 트레이드오프이며, 30K 제품을 조작할 때 기본적으로 개별 유연성이 필요합니까(예: )?

* 가능한 한 중복하지 않도록(로컬라이제이션 참조) 하거나 복제할 때 복제할 노드 수에 대해 생각해 보십시오.
* 쿼리 최적화를 준비하기 위해 가능한 한 콘텐츠에 태그를 지정해 보십시오.

   예:

   `/content/products/france/fr/shoe/reebok/pump/46 SKU`

   컨텐츠 수준당 하나의 태그가 있어야 합니다(즉, 국가, 언어, 카테고리, 브랜드, 제품). 검색 중

   `//element(*,my:Sku)[@country=’france’ and @language=’fr’`

   및

   `@category=’shoe’ and @brand=’reebok’ and @product=’pump’]`

   검색할 때보다 훨씬 빠릅니다.

   `/jcr:root/content/france/fr/shoe/reebok/pump/element(*,my:Sku)`

* 기술 스택에서 매우 중요한 컨텐츠 액세스 모델 및 서비스를 계획합니다. 이 방법은 일반적인 우수 사례이지만, 최적화 단계에서 자주 읽히는 데이터의 애플리케이션 캐시를 추가(번들 캐시를 로 채우지 않음)할 수 있으므로 이 방법은 보다 중요합니다.

   예를 들어 속성 관리는 제품 가져오기를 통해 업데이트되는 데이터에 대해 우려하므로 캐싱에 적합한 후보입니다.
* [프록시 페이지](#proxy-pages)를 사용하는 것이 좋습니다.

### 카탈로그 섹션 페이지 {#catalog-section-pages}

카탈로그 섹션은 다음과 같은 정보를 제공합니다.

* 카테고리에 대한 소개(이미지 및/또는 텍스트)이 기능은 배너 및 티저에 사용되어 특별 오퍼를 홍보할 수도 있습니다
* 해당 카테고리의 개별 제품에 대한 링크
* 다른 카테고리에 대한 링크

![ecommerce_categoryrunning](/help/sites-administering/assets/ecommerce_categoryrunning.png)

### 제품 페이지 {#product-pages}

제품 페이지에서는 개별 제품에 대한 포괄적인 정보를 제공합니다. 의 동적 업데이트도 반영됩니다.예를 들어, eCommerce 엔진에 등록된 가격 변경입니다.

제품 페이지는 **Product** 구성 요소를 사용하는 AEM 페이지입니다.예를 들어 **Commerce Product** 템플릿 내에서 다음을 수행합니다.

![ecommerce_nairobirdian-green](/help/sites-administering/assets/ecommerce_nairobirunnersgreen.png)

제품 구성 요소는 다음을 제공합니다.

* 일반 제품 정보텍스트 및 이미지 포함.
* 가격 책정일반적으로 페이지를 표시/새로 고칠 때마다 eCommerce 엔진에서 검색됩니다.
* 제품 변형 정보예를 들어 색상 및 크기가 있습니다.

이 정보를 통해 구매자는 품목을 장바구니에 추가할 때 다음 사항을 선택할 수 있습니다.

* 색상 및 크기 변형
* 수량

#### 제품 랜딩 페이지 {#product-landing-pages}

주로 정적 정보를 제공하는 AEM 페이지입니다.예를 들어, 기본 제품 페이지에 대한 링크가 있는 소개 및 개요입니다.

### 제품 구성 요소 {#product-component}

**제품** 구성 요소를 필요한 메타데이터(즉, `cartPage` 및 `cartObject`에 대한 경로)를 전달하는 상위 페이지가 있는 모든 페이지에 추가할 수 있습니다. 데모 사이트에서 Geometrixx Outdoors은 `UserInfo.jsp`에서 제공합니다.

**제품** 구성 요소는 개별 요구 사항에 따라 사용자 지정할 수도 있습니다.

### 프록시 페이지 {#proxy-pages}

프록시 페이지는 저장소의 구조를 단순화하고 대형 카탈로그에 대한 저장소를 최적화하는 데 사용됩니다.

카탈로그를 만들면 AEM 내에서 업데이트하고 사용자 지정할 수 있는 각 제품에 대한 개별 구성 요소를 제공하므로 제품당 10개의 노드가 사용됩니다. 카탈로그에 수백 또는 수천 개의 제품이 포함된 경우 이러한 많은 수의 노드가 문제가 될 수 있습니다. 문제를 방지하기 위해 프록시 페이지를 사용하여 카탈로그를 만들 수 있습니다.

프록시 페이지는 실제 제품 콘텐츠를 포함하지 않는 두 노드 구조( `cq:Page` 및 `jcr:content`)를 사용합니다. 요청 시 제품 데이터 및 템플릿 페이지를 참조하여 컨텐츠가 생성됩니다.

그러나, 무역이 있다. AEM 내에서 제품 정보를 사용자 지정할 수 없습니다. 표준 템플릿(사이트에 대해 정의됨)이 사용됩니다.

>[!NOTE]
프록시 페이지 없이 큰 카탈로그를 가져오면 문제가 발생하지 않습니다.
한 방법론에서 다른 방법론으로 언제든지 변환할 수 있습니다. 카탈로그의 하위 섹션을 변환할 수도 있습니다.

## 프로모션 및 바우처 {#promotions-and-vouchers}

### 바우처 {#vouchers}

바우처는 구매자들을 유도하여 구매하거나 고객의 충성도를 보상하기 위해 할인을 제공하는 시험되고 테스트된 방법입니다.

* 바우처 공급:

   * 구매 대행자가 장바구니에 입력할 바우처 코드.
   * 구매자가 장바구니에 입력한 후 표시되는 바우처 레이블입니다.
   * 프로모션 경로(바우처가 적용되는 작업을 정의합니다.)

* 외부 상거래 엔진도 바우처를 제공할 수 있습니다.

AEM에서:

* 바우처는 웹 사이트 콘솔을 사용하여 만들거나 편집하는 페이지 기반 구성 요소입니다.
* **바우처** 구성 요소는 다음을 제공합니다.

   * 바우처 관리를 위한 렌더러여기에는 현재 장바구니에 있는 모든 바우처가 표시됩니다.
   * 바우처를 관리(추가/제거)하기 위한 편집 대화 상자(양식)입니다.
   * 장바구니에 바우처를 추가/제거하는 데 필요한 작업.

* 바우처는 설정 및 해제 날짜/시간이 없지만 상위 캠페인의 바우처를 사용합니다.

>[!NOTE]
AEM에서는 **바우처**&#x200B;라는 용어를 사용하는데, 이것은 **쿠폰**&#x200B;이라는 용어와 동의어입니다.

### 프로모션 {#promotions}

프로모션과 바우처는 다음과 같은 시나리오를 실현하도록 해줍니다.

* 한 회사가 수작업으로 만들어진 사용자 목록인 종업원들에게 맞춤 가격을 제공한다.
* 장기 고객은 모든 주문에 대해 할인을 받습니다.
* 잘 정의된 기간 동안 제공되는 판매 가격.
* 고객은 이전 주문이 특정 금액을 초과하면 바우처를 받습니다.
* *product-X*&#x200B;를 구입하는 고객은 *product-Y* (한 쌍의 제품)에서 할인을 받을 수 있습니다.

프로모션은 일반적으로 제품 정보 관리자가 관리하는 것이 아니라 마케팅 관리자가 관리합니다.

* 프로모션은 웹 사이트 콘솔에서 생성/편집되는 페이지 기반 구성 요소입니다. &quot;
* 프로모션 공급:

   * 우선 순위
   * 프로모션 처리기 경로

* 프로모션을 캠페인에 연결하여 해당 설정/해제 날짜/시간을 정의할 수 있습니다.
* 프로모션을 경험에 연결하여 세그먼트를 정의할 수 있습니다.
* 경험에 연결되어 있지 않은 프로모션은 자체적으로 실행되지 않지만 바우처가 여전히 실행할 수 있습니다.
* 프로모션 구성 요소는 다음과 같습니다.

   * 프로모션 관리를 위한 렌더러 및 대화 상자
   * 프로모션 핸들러와 관련된 구성 매개 변수를 렌더링하고 편집하는 하위 구성 요소

AEM에서는 프로모션이 [캠페인 관리](/help/sites-authoring/personalization.md)에도 통합됩니다.

* [campaign](/help/sites-authoring/personalization.md) 은 설정/해제 시간을 지정합니다
* [](/help/sites-authoring/personalization.md) ** 캠페인 내에서는에 해당하는 대상 세그먼트에 따라 자산(teaser 페이지, 프로모션 등)을 그룹화하는 데 사용됩니다

프로모션은 경험이나 캠페인에서 직접 가질 수 있습니다.

* 프로모션이 경험에 유지되면 대상 세그먼트에 자동으로 적용할 수 있습니다.

   예를 들어 geometrixx-outdoors 샘플 사이트에서는 다음과 같이 프로모션을 수행합니다.

   `/content/campaigns/geometrixx-outdoors/big-spender/ordervalueover100/free-shipping`

   은 경험에 있으므로 세그먼트( `ordervalueover100`)가 확인될 때마다 자동으로 실행됩니다.

* 프로모션이 경험 내에 나타나지 않으면(캠페인에서만) 대상에 자동으로 적용할 수 없습니다. 그러나 구매자가 바우처를 장바구니에 입력하고 해당 바우처가 프로모션을 참조하는 경우 여전히 실행할 수 있습니다.

   예를 들어 판촉 행사

   `/content/campaigns/geometrixx-outdoors/article/10-bucks-off`

   은 경험 외부에 있으므로 자동으로 실행되지 않습니다(예:세분화 기반). 하지만 문서 캠페인 내의 여러 경험에서 찾을 수 있는 바우처가 참조합니다. 이러한 바우처 코드를 장바구니에 입력하면 프로모션이 실행됩니다.

>[!NOTE]
[hybris ](https://www.hybris.com/modules/promotion) 프로모션 및  [hybris](https://www.hybris.com/en/modules/voucher) 는 장바구니에 영향을 주고 가격과 관련된 모든 것을 보증합니다. 판촉 특정 마케팅 컨텐츠(예: 배너 등)는 hybris 프로모션의 일부가 아닙니다.

## 개인화 {#personalization}

### 고객 등록 및 계정 {#customer-registration-and-accounts}

쇼핑객이 등록할 때 계정 세부 사항을 AEM과 eCommerce 엔진 간에 동기화해야 합니다. 중요한 데이터는 독립적으로 유지되지만 프로필은 공유됩니다.

![chlimage_1-10](/help/sites-administering/assets/chlimage_1-10.png)

정확한 메커니즘은 시나리오에 따라 달라질 수 있습니다.

1. 사용자 계정은 두 시스템에 모두 있습니다.

   1. 필요한 작업이 없습니다.

1. 사용자 계정은 AEM에만 있습니다.

   1. 사용자는 동일한 계정 ID와 AEM에 저장되는 임의의 암호를 사용하는 eCommerce 엔진에서 만들어집니다.
   1. 첫 번째 호출 시 AEM이 eCommerce 엔진에 로그인하려고 하므로(예: 제품 페이지가 요청되고 eCommerce 엔진이 가격 기준으로 참조되는 경우), 임의 암호가 필요합니다. 이 문제는 AEM 로그인 후 발생하므로 암호를 사용할 수 없습니다.

1. 사용자 계정은 eCommerce 엔진에만 있습니다.

   1. 계정은 계정 ID와 암호가 동일한 AEM에서 생성됩니다.

eCommerce 엔진을 사용하는 경우 AEM은 계정 ID 및 암호(선택적으로 사용자 그룹)만 저장합니다. 다른 모든 정보는 eCommerce 엔진에 저장됩니다.

>[!NOTE]
eCommerce 엔진을 사용하는 경우 AEM 인스턴스에 로그인한 사용자를 위해 만든 계정이 해당 엔진과 통신하는 다른 AEM 인스턴스로 복제되는지(예: 워크플로우를 통해)확인해야 합니다.
그렇지 않으면 이러한 다른 AEM 인스턴스는 엔진에서 동일한 사용자에 대한 계정을 만들려고 합니다. 이러한 작업은 엔진에서 `DuplicateUidException` 이(가) 생성되면 실패합니다.

### 고객 등록 {#customer-sign-up}

쇼핑객이 장바구니에 액세스해야 하는 경우가 많습니다. 이를 위해서는 고객별 계정을 만들 수 있도록 등록 (계정 만들기)이 필요합니다.

![chlimage_1-11](/help/sites-administering/assets/chlimage_1-11.png)

>[!NOTE]
익명 장바구니 및 체크아웃도 지원됩니다.

### 고객 로그인 {#customer-sign-in}

등록 후에 쇼핑객이 자신의 계정으로 로그인할 수 있으므로 해당 작업을 추적하고 주문이 이행되도록 할 수 있습니다.

![chlimage_1-12](/help/sites-administering/assets/chlimage_1-12.png)

### 단일 사인온 {#single-sign-on}

SSO(Single-Sign-On)가 제공되므로 작성자가 두 번 로그인하지 않아도 AEM 및 eCommerce 시스템에서 모두 알 수 있습니다.

### myAccount {#myaccount}

eCommerce 엔진의 거래 데이터는 구매자에 대한 개인 정보와 결합됩니다. AEM에서는 이 데이터 중 일부를 프로필 데이터로 사용합니다. AEM에서 양식의 작업으로 정보가 전자 상거래 엔진에 다시 기록됩니다.

계정 정보를 쉽게 관리할 수 있는 페이지가 있습니다. geometrixx 페이지의 상단에 있는 **내 계정**&#x200B;을 클릭하거나 `/content/geometrixx-outdoors/en/user/account.html`로 이동하여 액세스할 수 있습니다.

![chlimage_1-13](/help/sites-administering/assets/chlimage_1-13.png)

### 주소록 {#address-book}

사이트는 선택한 주소를 저장해야 합니다.게재, 청구 및 대체 주소를 포함합니다. 기본 주소 형식을 기반으로 하여 양식을 사용하여 구현하거나 AEM에서 제공하는 주소록 구성 요소를 사용할 수 있습니다.

이 주소록 구성 요소를 사용하면 다음 작업을 수행할 수 있습니다.

* 책의 주소 편집
* 배송 주소록에서 주소를 선택합니다
* 청구 주소록에서 주소를 선택합니다.

기본값으로 원하는 주소를 선택할 수 있습니다.

주소록 구성 요소는 **주소록**&#x200B;을 클릭하거나 `/content/geometrixx-outdoors/en/user/account/address-book.html`로 이동하여 **내 계정** 페이지에서 연결할 수 있습니다.

![chlimage_1-14](/help/sites-administering/assets/chlimage_1-14.png)

**새 주소 추가... 를 클릭할 수 있습니다.** 을(를) 사용하여 주소록에 새 주소를 추가합니다. 입력한 다음 **주소 추가**&#x200B;를 클릭합니다.

>[!NOTE]
주소록에 몇 개의 주소를 입력할 수 있습니다.

장바구니를 체크아웃할 때 주소록 이 사용됩니다.

![chlimage_1-15](/help/sites-administering/assets/chlimage_1-15.png)

주소는 `user_home/profile/addresses` 아래에 유지됩니다.
예를 들어 Alison Parker의 경우 /home/users/geometrixx/aparker@geometrixx.info/profile/addresses 아래에 있습니다.

기본값으로 사용할 주소를 선택할 수 있습니다. 이 정보는 주소가 아닌 쇼핑객의 프로필에 유지됩니다. 프로필 속성 `address.default`은(는) 값에 대해 선택한 주소의 경로로 설정됩니다.

### 고객별 가격 {#customer-specific-pricing}

eCommerce 엔진은 컨텍스트(기본적으로 구매자 정보)를 사용하여 보유한 가격을 결정한 다음 올바른 정보를 AEM에 다시 제공합니다.

## 장바구니 및 주문 {#shopping-cart-and-orders}

쇼핑할 때 구매자는 제품 페이지를 탐색하고 품목을 선택하여 장바구니에 배치합니다. 체크아웃을 진행할 때 주문을 제출할 수 있습니다.

### 익명 쇼핑객 {#anonymous-shoppers}

익명의 고객은 다음을 수행할 수 있습니다.

* 제품 보기
* 장바구니에 제품 추가
* 주문을 배치하려면 체크아웃을 수행합니다

>[!NOTE]
인스턴스 주소 정보의 구성이나 고객 등록에 따라 체크아웃 전에 이 필요할 수 있습니다.

### 등록된 구매자 {#registered-shoppers}

등록된 고객은 다음을 수행할 수 있습니다.

* 계정에 로그인합니다.
* 제품 보기
* 장바구니에 제품 추가
* 주문을 배치하려면 체크아웃을 수행합니다
* 이전 주문 보기 및 추적

### 장바구니 컨텐츠 개요 {#shopping-cart-content-overview}

장바구니에는 다음이 제공됩니다.

* 선택한 항목 개요
* 선택한 항목의 제품 페이지에 대한 링크
* 기능:

   * 개별 품목의 수/수량을 갱신합니다.
   * 개별 항목 제거

![ecommerce_shoppingcart](/help/sites-administering/assets/ecommerce_shoppingcart.png)

장바구니는 사용 중인 엔진에 따라 저장됩니다.

* AEM 일반 은 쿠키에 장바구니를 저장합니다.
* 특정 eCommerce 엔진은 세션에서 카트를 저장할 수 있습니다.

어느 경우든, 항목은 로그인/로그아웃(동일한 시스템/브라우저에서만)에서 장바구니에 있고 복원할 수 있습니다. 예:

* `anonymous` 로 탐색하고 장바구니에 제품 추가
* `Allison Parker`으로 로그인 - 장바구니가 비어 있습니다.
* 장바구니에 제품 추가
* 로그아웃 - 장바구니에 `anonymous`용 제품이 표시됩니다.

* `Allison Parker`(으)로 다시 로그인 - 그녀의 제품이 복원됨

>[!NOTE]
익명 장바구니는 동일한 컴퓨터/브라우저에서만 복원할 수 있습니다.

>[!NOTE]
eCommerce 엔진의 `admin` 계정(예: hybris)과 충돌할 수 있으므로, `admin` 계정으로 장바구니 컨텐츠 복원을 테스트하지 않는 것이 좋습니다.

>[!NOTE]
hybris는 정의된 기간 후에 보류 중인 장바구니를 제거하도록 구성할 수 있습니다.

체크 아웃 전에 가격 변경 사항이 발생할 때 두 시스템 모두에 반영됩니다.

### 주문 정보 {#order-information}

주문에 대한 구현 정보에 따라 eCommerce 엔진 또는 AEM에서 이 정보를 제공합니다. AEM

다음과 같은 다양한 정보가 저장됩니다.

* **주문 ID**

   주문에 대한 참조 번호입니다.

* **주문 날짜**

   주문이 이루어진 날짜입니다.

* **상태**

   주문 현황예: 배송됨

* **통화**

   주문의 통화.

* **콘텐츠 항목**

   주문된 항목 목록입니다.

* **소계**

   주문된 품목의 총 원가.

* **세금**

   주문에 따른 세금 금액입니다.

* **배송**

   배송비.

* **합계**

   주문 총액주문품, 세금 및 파쇄

* **청구 주소**

   송장을 보낼 주소입니다.

* **결제 토큰**

   결제 방법.

* **결제 상태**

   지급 상태입니다.

* **배송 주소**

   화물이 배송될 주소.

* **배송 방법**

   운송 방법예를 들면, 육지, 바다 또는 공기와 같습니다.

* **추적 번호**

   운송 회사에서 사용하는 모든 추적 번호입니다.

* **추적 링크**

   배송 중 주문 추적에 사용되는 링크입니다.

>[!NOTE]
순서 만들기 마법사에 사용되는 필드는 해당 위치에 대해 정의된 터치에 적합한 스캐폴딩에 따라 달라집니다. 일반 예제에서 찾을 수 있는 위치는 다음과 같습니다.
`/etc/scaffolding/geometrixx-outdoors/order/jcr:content/cq:dialog`

AEM 내에서 주문이 유지되면 주문 콘솔에 각 주문에 대해 다음 내용이 표시됩니다.

* 장바구니에 있는 항목 수
* 주문의 총 값
* 주문이 이루어진 시기
* 상태

![chlimage_1-16](/help/sites-administering/assets/chlimage_1-16.png)

### 주문 추적 {#order-tracking}

주문을 하면 쇼핑객들은 종종 다음 주소로 돌아옵니다.

* 주문 상태를 확인합니다
* 주문에서 제품 제거
* 주문에 제품 추가

주문 배송을 받은 후, 구매자들은 일정 기간 동안 이루어진 주문 내역도 보고 싶을 수 있습니다.

주문 처리 및 추적은 일반적으로 eCommerce 엔진에서 관리합니다. Order History 구성 요소를 사용하여 AEM에서 정보를 표시할 수 있습니다. 이 구성 요소는 적용된 바우처와 프로모션을 포함하여 모든 관련 세부 사항을 표시합니다. 예:

![chlimage_1-17](/help/sites-administering/assets/chlimage_1-17.png)

## 체크아웃 {#checkout}

체크아웃은 표준 AEM 양식을 사용하여 구현됩니다. 이를 통해 마케팅 관리자는 마케팅 컨텐츠로 경험을 사용자 지정할 수 있습니다.

그런 다음 eCommerce는 AEM Forms의 입력을 사용하여 체크아웃 프로세스를 관리합니다.

### 지급 보안 {#payment-security}

신용 카드 정보를 포함한 결제 세부 사항은 종종 전자 상거래 엔진에서 관리합니다. AEM은 이러한 트랜잭션 정보를 엔진으로 전달합니다(그런 다음 결제 처리 서비스로 전달됨).

결제 카드 업계(PCI) 규정 준수를 달성할 수 있습니다.

### 주문 확인 {#confirmation-of-order}

순서는 화면에서 확인되며 [주문 추적](#order-tracking)으로 추적할 수 있습니다.

## 검색 {#search-features}

![chlimage_1-18](/help/sites-administering/assets/chlimage_1-18.png)

AEM은 제품에 표준 페이지를 사용하므로 표준 검색 구성 요소를 사용하여 검색 페이지를 만들 수 있습니다.

보다 완벽한 구현이 필요한 경우 다음 중 하나를 수행할 수 있습니다.

* 기본 검색 구성 요소를 필요한 기능으로 확장합니다.
* `CommerceService`에서 검색 방법을 구현한 다음 검색 페이지에서 eCommerce 검색 구성 요소를 사용하십시오.

eCommerce 엔진을 사용하는 경우 eCommerce 검색 API를 eCommerce 엔진 솔루션에서 완전히 구현할 수 있으므로, 기본 제공되는 eCommerce 검색 구성 요소를 사용할 수 있습니다. 면처리 검색을 사용하면 JCR 및/또는 엔진을 검색할 수 있습니다.
