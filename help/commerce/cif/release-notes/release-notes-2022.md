---
title: 2022년 AEM Content and Commerce 릴리스 노트
description: 2022년 Adobe Experience Manager Content and Commerce 릴리스 노트
exl-id: d0a66e70-c4f1-4051-8161-11f07dad0612
source-git-commit: eaffc71c23c18d26ec5cbb2bbb7524790c4826fe
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 37%

---

# Commerce integration framework GitHub 릴리스 개요

## 시스템 요구 사항 개요

현재 사용 중이거나 향후 사용할 CIF 버전에 대한 아래 표의 최소 시스템 요구 사항을 검토하십시오.

| 구성 요소 | 시스템 요구 사항 |
|:-------|:-----:|
| CIF 추가 기능 | 최소: AEM 6.5.7, Adobe Commerce 2.3.5 GraphQL 스키마 |
| CIF 핵심 구성 요소 | [시스템 요구 사항](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM Project Archetype | [시스템 요구 사항](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## 릴리스 날짜: 2022년 9월

| 구성 요소 | 버전 | 세부 사항 |
|:-------|:-----:|---------------------:|
| CIF 추가 기능 | 2022.09.20.00 | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.09.20.00.zip) |
| CIF 핵심 구성 요소 | 2.11.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.11.0) |
| CIF Venia 참조 사이트 | 2022.09.02 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.09.02) |

### 새로운 기능 {#what-is-new-september}

* 작성자는 경험 조각을 사용하여 제품 목록을 동적으로 보강할 수 있습니다(예: 제품 목록 사이에 배너 배치)
* 목록 구성 요소는 관련 페이지를 동적으로 표시하는 관련 제품/카테고리 페이지를 지원합니다.
* Peregrine 12.5 구성 요소 지원
* 제품 티저 및 캐러셀의 클라이언트측 가격 로드 지원

## 릴리스 날짜: 2022년 7월

| 구성 요소 | 버전 | 세부 사항 |
|:-------|:-----:|---------------------:|
| CIF 추가 기능 | 2022.08.02.00 | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.08.02.00.zip) |

### 새로운 기능 {#what-is-new-july}

* AEM 페이지 속성과 제품 관리실 개요를 통해 AEM 페이지를 제품 및 카테고리에 연결
  ![제품 관리실 페이지 연결](/help/assets/CIF/product_cockpit_page_association.png)

## 릴리스 날짜: 2022년 6월

| 구성 요소 | 버전 | 세부 사항 |
|:-------|:-----:|---------------------:|
| CIF 추가 기능 | 2022.07.05.00 | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.07.05.00.zip) |
| CIF 핵심 구성 요소 | 2.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.10.0) |
| CIF Venia 참조 사이트 | 2022.07.04 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.07.04) |

### 새로운 기능 {#what-is-new-june}

* 제품 카탈로그 보강으로 이제 AEM 페이지가 지원되므로 작성자가 페이지 - 제품 연결을 관리할 수 있습니다.

* 다양한 CIF 핵심 구성 요소 개선

### 버그 수정 {#bug-fixes-june}

* 클라이언트측 가격 가져오기에 로그인 토큰 추가

* 데이터 레이어의 페이지 구성 요소가 잘못되었습니다.

## 릴리스 날짜: 2022년 5월

| 구성 요소 | 버전 | 세부 사항 |
|:-------|:-----:|---------------------:|
| CIF 추가 기능 | 2022.05.31.00 | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.05.31.00.zip) |
| CIF 핵심 구성 요소 | 2.9.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.9.0) |
| CIF Venia 참조 사이트 | 2022.05.30 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.05.30) |

### 새로운 기능 {#what-is-new-may}

* 새롭고 간편해진 개요를 위한 제품 관리실 속성 페이지

![제품 관리실 속성 개요](/help/assets/CIF/product_cockpit_properties_overview.png)

* I/O Runtime의 서드파티 커넥터에 대한 호환성 및 견고성이 개선되었습니다.

* GQL 클라이언트 구성 덮어쓰기(예: 사용자 지정 캐싱 비헤이비어 설정)에 대한 지원 개선

### 버그 수정 {#bug-fixes-may}

* 다중 값 제품 선택기 필드에 두 번째 제품과 추가 제품이 잘못된 것으로 표시됩니다.

* 구성 요소 뒤에 제품 선택기가 숨겨지는 경우가 있습니다.

## 릴리스 날짜: 2022년 4월

| 구성 요소 | 버전 | 세부 사항 |
|:-------|:-----:|---------------------:|
| CIF 추가 기능 | 2022.04.28.00 | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.04.28.00.zip) |
| CIF 핵심 구성 요소 | 2.8.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.8.0) |
| CIF Venia 참조 사이트 | 2022.04.28 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.04.28) |

### 새로운 기능 {#what-is-new-april}

* 제품 관리실에 대한 빠른 액세스: 사이트 편집기에서 한 번의 클릭으로 전체 세부 제품 정보에 쉽게 액세스할 수 있습니다.

  ![위시리스트 사용](/help/assets/CIF/enable-wishlist.png)

* 추가 마케팅 상거래 구성 요소에 대한 지원: 장바구니에 추가 및 위시리스트 콜 투 액션을 표시하도록 구성 요소를 구성할 수 있습니다.

  ![제품 관리실에 대한 사이트 편집기 단축키](/help/assets/CIF/sites-editor-shortcut-to-cockpit.png)

## 릴리스 날짜: 2022년 2월

| 구성 요소 | 버전 | 세부 사항 |
|:-------|:-----:|---------------------:|
| CIF 추가 기능 | 2022.02.24.00 | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.02.24.00.zip) |
| CIF 핵심 구성 요소 | 2.6.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) |
| CIF Venia 참조 사이트 | 2022.02.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.02.24) |

### 새로운 기능 {#what-is-new-march}

* Beta: AEM CIF 검색 핵심 구성 요소 지원 Commerce 라이브 검색
* 다중 스토어 시나리오에 대한 SEO 개선: 이제 PDP/PLP에 대한 URL 형식은 CIF Cloud 구성 속성을 통해 스토어 레벨에서 구성할 수 있습니다.
* 제품 선택기는 사용자 인터페이스의 새 필터 옵션을 통해 스테이징된 제품을 지원합니다. 콘텐츠 제공자가 예정된 제품 출시에 맞춰 제품 콘텐츠 관리를 준비할 수 있도록 지원
* 구성 프록시 URL 대신 CIF Cloud 구성 이름을 시용하여 CIF 구성 관리 및 오류 처리 간소화
* 수동으로 제품 목록 및 슬라이드 구성 요소의 범주 선택. 콘텐츠 제공자는 카탈로그 경험 이외의 콘텐츠 페이지에서 이러한 구성 요소를 사용할 수 있습니다.

## 릴리스 날짜: 2022년 1월

| 구성 요소 | 버전 | 세부 사항 |
|:-------|:-----:|---------------------:|
| CIF 추가 기능 | 2022.01.20.00 | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.01.20.00.zip) |
| CIF 핵심 구성 요소 | 2.5.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.5.0) |
| CIF Venia 참조 사이트 | 2022.01.27 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.01.27) |

### 새로운 기능 {#what-is-new-january}

* 향상된 myAccount 구성 요소
* 제품 추천 구성 요소는 추가 페이지 유형(홈 페이지, 장바구니, 주문 확인)을 지원합니다.
* **위시리스트**
   * 로그인한 방문자는 위시리스트에 제품을 추가할 수 있습니다.
   * myAccount를 통해 위시리스트 및 해당 제품을 관리할 수 있습니다.
   * “위시리스트에 추가” 버튼은 정책을 통해 구성 요소 수준에서 활성화/비활성화할 수 있습니다(예: 제품 티저, 제품 세부 사항).
   * 핵심 구성 요소 및 AEM Venia Storefront에서 사용 가능

![위시리스트](/help/assets/CIF/wishlist.png)
