---
title: 2021년 Adobe Experience Manager Content and Commerce 릴리스 노트
description: 2021년 Adobe Experience Manager Content and Commerce 릴리스 노트
exl-id: ec47c5f8-d4dd-469f-94df-5ee28f25d696
source-git-commit: 2810e34f642f4643fa4dc24b31a57a68e9194e39
workflow-type: tm+mt
source-wordcount: '1318'
ht-degree: 14%

---

# Commerce Integration Framework GitHub 릴리스 개요

## 시스템 요구 사항 개요

현재 사용 중이거나 향후 사용할 CIF 버전에 대한 아래 표의 최소 시스템 요구 사항을 검토하십시오.

| 구성 요소 | 시스템 요구 사항 |
|:-------|:-----:|
| CIF 추가 기능 | 최소: Adobe Experience Manager(AEM) 6.5.7, Adobe Commerce 2.3.5 GraphQL 스키마 |
| CIF 핵심 구성 요소 | [시스템 요구 사항](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM Project Archetype | [시스템 요구 사항](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## 릴리스 날짜: 2021년 11월

| 구성 요소 | 버전 | 세부 사항 |
|:-------|:-----:|---------------------:|
| CIF 추가 기능 | 2021.11.18.00 | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.11.18.00.zip) |
| CIF 핵심 구성 요소 | 2.4.2 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.4.2) |
| CIF Venia 참조 사이트 | 2021.12.01 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.12.01) |

### 새로운 기능 {#what-is-new-november}

* Commerce의 확장 가능한 Peregrine 구성 요소를 기반으로 하는 확장 myAccount 구성 요소

![확장 myAccount 구성 요소](/help/assets/CIF/extended-myAccount-components.png)

* 작성자는 추가 권장 사항 유형을 사용하여 애드혹 Commerce 제품 권장 사항을 생성할 수 있습니다.

* AEM 상점에서의 기프트 카드 지원

## 릴리스 날짜: 2021년 10월

| 구성 요소 | 버전 | 세부 사항 |
|:-------|:-----:|---------------------:|
| CIF 추가 기능 | 2021.10.20.02 | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.10.20.02.zip) |
| CIF 핵심 구성 요소 | 2.4.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.4.0) |
| CIF Venia 참조 사이트 | 2021.11.01 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.11.01) |

### 새로운 기능 {#what-is-new-october}

* CIF 추가 기능은 새 GraphQL API 및 스키마가 포함된 최신 Commerce v2.4.3을 지원합니다

* 작성자는 리치 텍스트 편집기(RTE)를 사용하여 텍스트 필드의 제품 및 카탈로그 페이지에 링크를 추가할 수 있습니다. RTE 도구 모음에 CIF 아이콘이 추가되어 선택기를 열어 컨텍스트를 종료하지 않고도 제품이나 카테고리를 빠르게 검색하고 선택할 수 있습니다.

* 기존 팝업 장바구니 및 체크아웃이 전용 AEM 장바구니 및 체크아웃 페이지로 대체되었습니다. 이러한 페이지의 구성 요소는 Adobe Commerce의 확장 가능한 Peregrine 구성 요소를 사용하여 빌드됩니다

* 판매자는 Commerce 백엔드를 사용하여 탐색에서 특정 제품 카탈로그 범주를 숨길 수 있습니다. CIF 탐색 핵심 구성 요소는 탐색에서 범주를 표시하거나 숨기기 위해 상거래 백엔드 구성 &quot;메뉴에 포함&quot;을 준수합니다

* 범주 또는 제품 페이지를 찾을 수 없는 경우 AEM Storefront Venia가 HTTP 404 오류를 반환합니다.

## 릴리스 날짜: 2021년 9월

| 구성 요소 | 버전 | 세부 사항 |
|:-------|:-----:|---------------------:|
| CIF 추가 기능 | 2021.09.27 | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.09.27.zip) |
| CIF 핵심 구성 요소 | 2.2.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.2.0) |
| CIF Venia 참조 사이트 | 2021.09.23 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.09.23) |

### 새로운 기능 {#what-is-new-september}

* 사이트 편집기의 새로운 &quot;연결된 상거래 콘텐츠&quot; 탭은 현재 컨텍스트에 대한 관련 AEM 제품 콘텐츠에 빠르게 액세스하여 작성자의 효율성을 높입니다

  ![연계된 상거래 콘텐츠](/help/assets/CIF/associated-commerce-content.png)

* 향상된 사용자 경험, 향상된 효율성 및 복잡한 제품 카탈로그에 대한 지원을 위해 제품 선택기 UI가 개선되었습니다

  ![새 제품 선택기](/help/assets/CIF/product-picker.png)

* 탐색 구성 요소에서 &quot;include_in_menu&quot; 속성 준수

### 버그 수정 {#bug-fixes-september}

* 메뉴 캐시 플러시가 예상대로 작동하지 않습니다.

* AEM CS 배포 단계 중 및 클라이언트측 구성 요소를 사용하지 않는 경우 JS 오류 발생

* sling:configs 노드가 있는 폴더에 CIF 클라우드 구성을 만들 수 없음

## 릴리스 날짜: 2021년 8월

| 구성 요소 | 버전 | 세부 사항 |
|:-------|:-----:|---------------------:|
| CIF 추가 기능 | 2021.09.02 | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.09.02.zip) |
| CIF 핵심 구성 요소 | 2.1.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.1.0) |
| CIF Venia 참조 사이트 | 2021.08.27 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.08.27) |

### 새로운 기능 {#what-is-new-august}

* 향상된 사용자 경험, 향상된 효율성 및 복잡한 제품 카탈로그에 대한 더 나은 지원을 위한 새로운 카테고리 선택기 UI

  ![새 범주 선택기](/help/assets/CIF/category-picker.png)

* CIF 핵심 구성 요소에 대한 A11Y 지원 개선

### 버그 수정 {#bug-fixes-august}

* 범주 필터 아코디언이 열린 후에는 닫을 수 없습니다.

* 제품 티저에서 &#39;클릭 유도 문안&#39; 속성이 끊어짐

* AEM CS 배포 단계 중 CIF JS 오류

* 매핑된 제품 목록 항목에 대한 원시 제품 액세스 수정

## 릴리스 날짜: 2021년 7월

| 구성 요소 | 버전 | 세부 사항 |
|:-------|:-----:|---------------------:|
| CIF 추가 기능 | 2021.07.21 | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.07.21.zip) |
| CIF 핵심 구성 요소 | 2.0.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.0.0) |
| CIF Venia 참조 사이트 | 2021.07.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.07.22) |

### 새로운 기능 {#what-is-new-july}

* CIF 코어 구성 요소 v2
   * PDP/PLP URL 및 SEO에 대한 간소화된 개선된 구성
   * 향후 변경 사항에 대한 가시성을 개선하기 위해 작성 모드에서 스테이징된 제품 데이터에 대한 시각적 표시기
   * 콘텐츠 및 상거래 페이지를 위한 새 사이트맵 구성 요소

* 지원 대상 [Adobe Commerce Sensei 제품 추천, Adobe Sensei 제공](https://business.adobe.com/products/magento/product-recommendations.html) 미리 정의되거나 즉석에서 생성된 권장 사항을 사용하는 AEM Storefront에서

## 릴리스 날짜: 2021년 6월

| 구성 요소 | 버전 | 세부 사항 |
|:-------|:-----:|---------------------:|
| CIF 추가 기능 | 2021.06.18 | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.06.18.zip) |
| CIF 핵심 구성 요소 | 1.12.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.12.0) |
| CIF Venia 참조 사이트 | 2021.06.12 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.06.17) |

### 새로운 기능 {#what-is-new-june}

* 콘텐츠 조각에 대한 새로운 CIF 제품 및 카테고리 참조 데이터 유형(포함) 제품/카테고리 선택기 UI 지원)
* 새 Commerce 콘텐츠 조각 핵심 구성 요소
* AEM 백엔드에서 전체 텍스트 상거래 검색 지원
* 상거래 핵심 구성 요소는 Adobe Commerce Sensei Recs 데이터 수집
* 범주 페이지에 대한 SEO 친화적인 URL이 개선되었습니다
* 사이트/구성당 사용자 지정 HTTP 헤더 지원

## 릴리스 날짜: 2021년 5월

| 구성 요소 | 버전 | 세부 사항 |
|:-------|:-----:|---------------------:|
| CIF 추가 기능 | 2021.05.26 | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.05.26.zip) |
| CIF 핵심 구성 요소 | 1.11.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.11.0) |
| CIF Venia 참조 사이트 | 2021.05.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.05.24) |

### 새로운 기능 {#what-is-new-may}

* 제품 콘솔 속성에서 관련 콘텐츠에 대한 페이지 매김 지원

### 버그 수정 {#bug-fixes-may}

* 제품 속성의 에셋 탭에 에셋 썸네일이 표시되지 않음

* 이동 경로는 제품 콘솔의 미리 보기 데이터를 재설정합니다.

## 릴리스 날짜: 2021년 4월

| 구성 요소 | 버전 | 세부 사항 |
|:-------|:-----:|---------------------:|
| CIF 추가 기능 | 2021.04.22 | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.04.22.zip) |
| CIF 핵심 구성 요소 | 1.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia 참조 사이트 | 2021.04.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 새로운 기능 {#what-is-new-april}

* 범주 UID 지원 - 범주 ID에 문자열을 사용하는 시스템에 대한 서드파티 상거래 통합을 잠금 해제합니다.

* PWA Studio에 대한 AEM 확장에는 다음이 포함됩니다. 통합 예

* WCM 탐색 핵심 구성 요소를 확장하는 새로운 CIF 탐색 핵심 구성 요소

### 버그 수정 {#bug-fixes-april}

* 범주 페이지의 페이지 속성에서 상거래 탭 아래에 루트 범주 필드가 표시되지 않았습니다

## 릴리스 날짜: 2021년 3월 {#what-is-new-march}

| GitHub | 버전 | 자세한 릴리스 정보 |
|:-------|:-----:|---------------------:|
| CIF 커넥터 | 1.9.0 | [릴리스 정보](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF 핵심 구성 요소 | 1.9.0 | [릴리스 정보](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia 참조 사이트 | 2021.03.25 | [릴리스 정보](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 새로운 기능

* Adobe Commerce 2.4.2 지원

### 개선 사항

* 컨텐츠 기반 페이지에 대한 제품 세부 사항 구성 요소의 재사용성 개선

* PDP에 대한 캐싱 및 백엔드 호출 감소

* 여러 버그 수정.

## 릴리스 날짜: 2021년 2월

| GitHub | 버전 | 자세한 릴리스 정보 |
|:-------|:-----:|---------------------:|
| CIF 커넥터 | 1.8.0 | [릴리스 정보](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF 핵심 구성 요소 | 1.8.0 | [릴리스 정보](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia 참조 사이트 | 2021.02.24 | [릴리스 정보](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 새로운 기능 {#what-is-new-february}

* 제품 경험 관리: 경험 조각을 사용하여 제품 카탈로그 페이지를 개별적으로 풍성하게 만듭니다.

* 연결된 콘텐츠로 빠르게 이동하는 작업을 포함하여 연결된 에셋 및 경험 조각을 표시하도록 제품 콘솔 속성을 확장했습니다.

### 개선 사항  {#what-is-improved-february}

* 제품 이미지 URL 및 카테고리 정보로 클라이언트측 데이터 계층을 개선했습니다.

* 여러 버그 수정.

## 릴리스 날짜: 2021년 1월

| GitHub | 버전 | 자세한 릴리스 정보 |
|:-------|:-----:|---------------------:|
| CIF 커넥터 | 1.7.0 | [릴리스 정보](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF 핵심 구성 요소 | 1.7.0 | [릴리스 정보](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia 참조 사이트 | 2021.02.02 | [릴리스 정보](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 새로운 기능 {#what-is-new-january}

* 제품 경험 관리: 에셋 및 경험 조각에 대한 새로운 &#39;Commerce&#39; 속성 탭입니다. 이 탭에서는 에셋 및 경험 조각을 제품 및 카테고리에 연결할 수 있습니다. 탭에는 연결된 상거래 개체에 대한 실시간 데이터와 제품 콘솔에 세부 정보를 표시하는 링크도 표시됩니다.

### 개선 사항  {#what-is-improved-january}

* 인증 후 사용자 데이터를 Adobe 클라이언트 데이터 레이어에 보냅니다.

* 여러 버그 수정.
