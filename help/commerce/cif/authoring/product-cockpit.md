---
title: 제품 관리실
description: 제품 조종실 작업
source-git-commit: f3e286c7b5404812655f3b257de17be7bfde7487
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 1%

---

# 제품 관리실 {#product-cockpit}

## 개요 {#overview}

제품 조종실은 연결된 제품 카탈로그 및 관련 컨텐츠에 대한 통합 개요를 제공합니다. 모든 관련 컨텐츠는 조종실로부터 빠르게 액세스할 수 있는 링크를 가지고 있습니다.

스테이징된 제품 데이터에는 새로운 카테고리, 제품 또는 업데이트된 속성과 같은 미래의 돌연변이가 포함됩니다.

>[!NOTE]
>
>제품 카탈로그라는 용어는 상거래 상점, 스토어 보기 및 유사한 표현식과 바꿔서 사용할 수 있습니다.

## 구성 {#configuration}

제품 카탈로그는 AEM에서 구성해야 합니다. 자세한 내용은 [저장 및 카탈로그 구성](/help/commerce/cif/getting-started.md#catalog) 추가 정보.

준비된 카탈로그 기능을 사용하려면 인증이 필요합니다. 자세한 내용은 [시작하기](/help/commerce/cif/getting-started.md) 추가 정보.

>[!NOTE]
>
>스테이징된 카탈로그 기능은 토큰 기반 인증을 지원하는 Adobe Commerce 및 타사 커넥터에서만 사용할 수 있습니다.

## 제품 조종실 열기 {#opening-product-cockpit}

제품 조종실에 액세스하는 가장 쉬운 방법은 AEM 기본 메뉴의 &#39;상거래&#39; 메뉴를 통해서입니다. Omnisearch(상거래 검색) 또는 열기 기능도 사용할 수 있습니다 `https://<yourAEMInstance>/commerce.html`.

![AEM 메뉴](/help/commerce/cif/assets/aem-menu.png)

## 제품 카탈로그 찾아보기 {#browsing-product-catalogs}

제품 조종실은 제품 카탈로그 구조를 따라 계층적으로 구성됩니다. 첫 번째 레벨은 상거래 백엔드의 메타 정보를 포함하여 구성된 모든 제품 카탈로그의 카탈로그 루트 수준을 표시합니다.

![구성된 카탈로그](/help/commerce/cif/assets/catalog-overview.png)

카테고리를 클릭하면 클릭한 카테고리의 하위 항목이 로드됩니다.

![카테고리 하위](/help/commerce/cif/assets/catalog-category-children.png)

가능한 경우 제품을 클릭하면 제품 변형이 로드됩니다.

![제품 변형](/help/commerce/cif/assets/catalog-product-variation.png)

>[!NOTE]
>
>AEM의 제품 카탈로그 데이터는 구성된 상거래 종단점을 통해 실시간으로 검색되는 데이터입니다. AEM에 저장된 제품 카탈로그 데이터가 없습니다.

## 제품 카탈로그 검색 {#searching-product-catalog}

제품 카탈로그를 통한 전체 텍스트 검색은 왼쪽 필터 탭에 제공되어 제품을 빠르게 찾습니다.

![검색을](/help/commerce/cif/assets/search-cockpit.png)

## 준비된 제품 카탈로그 찾아보기 {#staged-product-catalogs}

기본적으로 제품 조종실에는 라이브 제품 카탈로그 데이터가 표시됩니다. 왼쪽 필터 탭의 &quot;준비된 카탈로그&quot;를 사용하면 선택한 날짜에 대한 제품 카탈로그를 로드합니다.

![준비된 카탈로그](/help/commerce/cif/assets/staged-cockpit.png)

## 제품 카탈로그 속성 {#catalog-properties}

제품이나 카테고리의 속성 아이콘을 클릭하면 선택한 객체의 속성 보기가 열립니다. 제품 변형의 열기 속성은 기본 제품 속성을 여는 것과 같습니다.

### 상거래 탭 {#tabs}

일반 및 변형 탭에는 상거래 백엔드에서 가져오는 사전 정의된 상거래 속성이 표시됩니다. 이 데이터(incl. 변형)은 레코드 시스템이 상거래 백엔드이므로 AEM에서 읽기 전용 데이터입니다. 변형 탭은 변형이 있는 제품에 대해서만 나타나며 모든 변형 목록을 표시합니다.

![카탈로그 속성](/help/commerce/cif/assets/catalog-properties.png)

### AEM 컨텐츠 탭 {#content-tabs}

AEM 컨텐츠 유형(경험 조각, 컨텐츠 조각, 관련 자산)별로 그룹화된 이러한 탭에는 상거래 객체와 연관된 AEM 컨텐츠가 표시됩니다. &#39;세부 사항 보기&#39; 작업을 수행하면 선택한 컨텐츠가 있는 새 브라우저 탭이 열립니다.

![콘텐츠 속성](/help/commerce/cif/assets/content-properties.png)
