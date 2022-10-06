---
title: 상거래 경험 작성
description: 작동하는 상거래 경험
exl-id: 2db51bd7-8fc7-4ae8-8d6f-e5035fbe954d
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 0%

---

# 상거래 경험 작성 {#authoring-commerce-experiences}

## 개요 {#overview}

CIF 추가 기능은 전자 상거래 관련 기능으로 AEM 작성을 확장합니다. 이를 통해 작성자는 컨텍스트를 종료하지 않고 제품 데이터 및 콘텐츠에 액세스하여 효율적으로 상거래 관련 경험을 구축하고 관리할 수 있습니다.

## 피커 {#pickers}

제품 및 카테고리 선택기 는 AEM 작성자가 필요할 때 제품이나 카테고리를 편리하게 찾아 선택할 수 있는 모달 UI 대화 상자입니다. 핵심 구성 요소, 컨텐츠 연결 및 제품 템플릿은 제품 카탈로그 데이터가 필요한 구성이 있는 일반적인 영역입니다. 선택기는 다중 선택, 변형 선택 및 값 사전 선택과 같은 다양한 구성 옵션을 지원합니다.

### 제품 선택기 {#product-picker}

이 선택기는 제품을 찾기 위해 카탈로그 구조 또는 전체 텍스트 검색을 통해 검색할 수 있도록 제공합니다. 변형 제품이 &#39;Type&#39; 열에 폴더 아이콘을 제공합니다. 폴더 아이콘을 클릭하면 선택한 제품의 변형이 열립니다.

![제품 선택기](/help/commerce/cif/assets/authoring/product-picker.png)

상위 카테고리를 클릭하면 작성자가 제품 수준으로 돌아갑니다.

![제품 선택기](/help/commerce/cif/assets/authoring/product-picker-variation.png)

**제품 티저 예**

![선택하지 않은 티저 구성 요소](/help/commerce/cif/assets/authoring/teaser_component_without_selection.png)

이 구성 요소의 구성 대화 상자에는 제품이 필요합니다. CIF는 SKU를 제품 식별자로 사용합니다. 작성자는 직접 sku를 입력하거나 폴더 아이콘을 클릭하여 제품 선택기를 열 수 있습니다. 선택기를 선택하고 닫으면 구성 요소 대화 상자에 선택한 제품의 이름이 표시됩니다

![선택한 티저 구성 요소](/help/commerce/cif/assets/authoring/teaser_component_with_selection.png)

### 카테고리 선택기 {#category-picker}

이 선택기는 카테고리를 찾기 위해 카탈로그 구조를 탐색하는 기능을 제공합니다.

![카테고리 선택](/help/commerce/cif/assets/authoring/category-picker.png)

**카테고리 회전판 예**

![선택 없이 회전판 구성 요소](/help/commerce/cif/assets/authoring/carousel_component_without_selection.png)

이 구성 요소의 구성 대화 상자에는 1 이 필요합니다. n 카테고리. CIF는 UID / ID 를 카테고리 식별자로 사용합니다. 작성자는 직접 UID를 입력하거나 폴더 아이콘을 클릭하여 카테고리 선택기를 열 수 있습니다. 선택기를 선택하고 닫으면 구성 요소 대화 상자에 선택한 카테고리의 이름이 표시됩니다.

![선택 영역이 있는 회전 구성 요소](/help/commerce/cif/assets/authoring/carousel_component_with_selection.png)

## 범용 편집기 {#universal-editor}

범용 편집기는 실시간 제품 데이터 및 관련 제품 컨텐츠에 액세스할 수 있는 기능으로 확장됩니다.

### 제품 데이터 액세스 {#access-product-data}

편집기의 사이드 패널에 있는 &#39;자산&#39; 탭에서는 &#39;제품&#39; 유형을 선택하여 제품 데이터에 대한 액세스를 제공합니다. 구성된 상거래 종단점에서 데이터를 실시간으로 가져옵니다. 필터는 특정 제품을 찾기 위한 상거래 종단점의 전체 텍스트 검색입니다.

![제품 데이터 사이드 패널](/help/commerce/cif/assets/authoring/products-side-panel.png)

자산과 유사하게, 제품을 페이지에 찾을 수 있습니다(제품 티저 구성 요소를 기본값으로 생성) 또는 구성 요소(현재 지원됨 제품 티저 및 제품 회전판).

### RTE를 사용하여 텍스트 필드에 링크 추가 {#rte}

CIF 제품 카탈로그 페이지는 즉시 렌더링되는 가상 페이지입니다. 따라서 일반 AEM 페이지용 과 같은 하이퍼링크를 포함할 수 없습니다. CIF는 RTE(리치 텍스트 편집기)에 새 작업 &quot;상거래 링크&quot;를 추가합니다. 이 작업은 일반 &quot;하이퍼링크&quot; 작업과 정확히 유사하지만 작성자가 선택기를 사용하여 제품 또는 카테고리를 선택할 수 있습니다.

![RTE](/help/commerce/cif/assets/authoring/RTE.png)

    >[!NOTE]
    >
    > 카테고리와 제품을 모두 선택하면 제품이 선택됩니다.

페이지가 렌더링될 때 실제 링크로 대체되는 자리 표시자 링크가 만들어집니다.

### 연결된 제품 컨텐츠 액세스 {#associated-content}

범용 편집기가 페이지에서 1:n 제품을 인식하면 사이드 패널에 &quot;연결된 상거래 컨텐츠&quot; 탭이 자동으로 표시됩니다. 이 탭에서는 작성자가 제품에서 태그가 지정된 AEM 컨텐츠에 빠르게 액세스할 수 있습니다( [관련 AEM 콘텐츠으로 제품 데이터 보강](./enrich-product-associated-content.md) 추가 정보). 이 탭에는 페이지에 여러 제품이 있는 경우 콘텐츠 유형 및 특정 제품에 대해 필터링할 수 있는 드롭다운이 제공됩니다. 컨텐츠 사용은 &quot;자산&quot; 탭의 컨텐츠를 사용하는 것과 동일하게 작동합니다.

![제품 데이터 사이드 패널](/help/commerce/cif/assets/authoring/associated-commerce-content-tab.png)

### 미리 보기 준비된 제품 데이터 {#staged-data}

편집기의 타임워프 모드에서는 작성자가 타임워프 날짜를 기반으로 준비된 제품 카탈로그 데이터를 사용하여 AEM 경험을 미리 보고 검색할 수 있습니다.

![타임워프](/help/commerce/cif/assets/authoring/timewarp.png)

사용된 날짜가 스테이징된 경우 구성 요소에 시각적 표시기가 표시됩니다.

![준비된 표시기](/help/commerce/cif/assets/authoring/staged-indicator.png)

## Omnisearch {#omnisearch}

Omnisearch를 사용하면 전문가가 전체 텍스트 검색을 사용하여 AEM 컨텐츠 및 제품 카탈로그 데이터를 쉽게 찾을 수 있습니다. Omnisearch는 AEM 및 상거래 백엔드에서 전체 텍스트 검색을 실행하여 상거래 백엔드 및 AEM 컨텐츠에서 제품 카탈로그 개체를 찾습니다. AEM 결과에는 제품/카테고리 데이터가 태그로 지정된 컨텐츠도 포함됩니다.

![Omnisearch](/help/commerce/cif/assets/authoring/omnisearch.png)

결과는 유형별로 그룹화됩니다.

    >[!NOTE]
    >
    > Omnisearch의 전체 텍스트 검색은 관련 컨텐츠 조각을 지원하지 않습니다. SKU 또는 UID를 사용하여 관련 컨텐츠 조각을 찾습니다.
