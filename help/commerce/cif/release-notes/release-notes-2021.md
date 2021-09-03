---
title: AEM Content and Commerce 릴리스 노트 2021
description: AEM Content and Commerce 릴리스 노트 2021
exl-id: ec47c5f8-d4dd-469f-94df-5ee28f25d696
source-git-commit: fd973cb3693872e4850f860a625cab70553d2754
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 11%

---

# Commerce Integration Framework GitHub 릴리스 개요

## 시스템 요구 사항 개요

현재 사용 중인 CIF 버전 또는 향후 사용할 예정인 최소 시스템 요구 사항을 아래 표에서 검토하십시오.

**4월 릴리스에서는 GitHub의 CIF 커넥터를** Adobe 소프트웨어 배포 [에서 사용할 수 있는 CIF 추가 ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)기능으로교체했습니다. 추가 기능으로 전환하면 프로젝트에 큰 이점이 있습니다.

* 대부분의 새로운 기능은 AEM 6.5에서 즉시 사용할 수 있습니다(기능 사이드 포트를 기다리지 않음).
* 새로운 추가 기능 버전으로 쉽게 업그레이드 가능
* Cloud Service 준비

이전 AEM CIF 커넥터가 유지 관리 모드로 전환되고 있으므로 더 이상 사용하지 않아야 합니다. CIF 커넥터를 새 CIF 추가 기능으로 바꾸십시오. 대부분의 프로젝트에 대해 단순히 패키지를 대체할 수 있어야 합니다.

| 구성 요소 | 시스템 요구 사항 |
|:-------|:-----:|
| CIF 추가 기능 | 최소: AEM 6.5.7, Magento 2.3.5 GraphQL 스키마 |
| CIF 코어 구성 요소 | [시스템 요구 사항](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM 프로젝트 전형 | [시스템 요구 사항](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## 릴리스 날짜: 2021년 8월

| 구성 요소 | 버전 | 세부 사항 |
|:-------|:-----:|---------------------:|
| CIF 추가 기능 | 2021.09.02 | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.09.02.zip) |
| CIF 코어 구성 요소 | 2.1.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.1.0) |
| CIF Venia 참조 사이트 | 2021.08.27 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.08.27) |

### 새로운 기능 {#what-is-new-august}

* 향상된 사용자 환경, 향상된 효율성 및 복잡한 제품 카탈로그에 대한 향상된 지원을 제공하는 새로운 카테고리 선택기 UI

   ![새 카테고리 선택기](/help/assets/CIF/category-picker.png)

* CIF A11Y 구성 요소에 대한 지원 개선

### 버그 수정 {#bug-fixes-august}

* 카테고리 필터 아코디언을 열고 닫을 수 없습니다

* 제품 티저에 &#39;Call to action text&#39; 속성이 손상되었습니다.

* AEM CS 배포 단계 중 CIF JS 오류

* 매핑된 제품 목록 항목에 대한 원시 제품 액세스 수정

## 릴리스 날짜: 2021년 7월

| 구성 요소 | 버전 | 세부 사항 |
|:-------|:-----:|---------------------:|
| CIF 추가 기능 | 2021.07.21 | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.07.21.zip) |
| CIF 코어 구성 요소 | 2.0.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.0.0) |
| CIF Venia 참조 사이트 | 2021.07.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.07.22) |

### 새로운 기능 {#what-is-new-july}

* CIF 코어 구성 요소 v2
   * PDP/PLP URL 및 SEO를 위한 간소화된 구성 및 개선
   * 예정된 변경 사항을 더 잘 파악하기 위해 작성 모드에서 준비된 제품 데이터에 대한 시각적 지표
   * 컨텐츠 및 상거래 페이지를 위한 새 사이트 맵 구성 요소

* 사전 정의된 권장 또는 즉석에서 만든 추천을 사용하여 AEM Storefront에서 Adobe Sensei](https://business.adobe.com/products/magento/product-recommendations.html)에서 제공하는 [Adobe Commerce Sensei 제품 권장 사항을 지원합니다

## 릴리스 날짜: 2021년 6월

| 구성 요소 | 버전 | 세부 사항 |
|:-------|:-----:|---------------------:|
| CIF 추가 기능 | 2021.06.18 | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.06.18.zip) |
| CIF 코어 구성 요소 | 1.12.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.12.0) |
| CIF Venia 참조 사이트 | 2021.06.12 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.06.17) |

### 새로운 기능 {#what-is-new-june}

* 컨텐츠 조각에 대한 새 CIF 제품 및 카테고리 참조 데이터 유형(Incl) 제품/카테고리 선택기 UI 지원)
* 새 상거래 컨텐츠 조각 코어 구성 요소
* AEM 백엔드에서 지원되는 전체 텍스트 상거래 검색
* 상거래 핵심 구성 요소 지원 Adobe Commerce Sensei Recs 데이터 수집
* 카테고리 페이지의 SEO 기반 URL이 개선되었습니다
* 사이트/구성당 사용자 지정 HTTP 헤더 지원

## 릴리스 날짜: 2021년 5월

| 구성 요소 | 버전 | 세부 사항 |
|:-------|:-----:|---------------------:|
| CIF 추가 기능 | 2021.05.26 | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.05.26.zip) |
| CIF 코어 구성 요소 | 1.11.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.11.0) |
| CIF Venia 참조 사이트 | 2021.05.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.05.24) |

### 새로운 기능 {#what-is-new-may}

* 제품 콘솔 속성의 관련 콘텐츠에 대한 페이지 매김 지원

### 버그 수정 {#bug-fixes-may}

* 제품 속성의 자산 탭에 자산 축소판이 표시되지 않음

* 탐색 표시 는 제품 콘솔에서 미리 보기 데이터를 재설정합니다

## 릴리스 날짜: 2021년 4월

| 구성 요소 | 버전 | 세부 사항 |
|:-------|:-----:|---------------------:|
| CIF 추가 기능 | 2021.04.22 | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.04.22.zip) |
| CIF 코어 구성 요소 | 1.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia 참조 사이트 | 2021.04.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 새로운 기능 {#what-is-new-april}

* 카테고리 UID 지원 - 카테고리 ID에 문자열을 사용하는 시스템에 대한 타사 상거래 통합을 잠금 해제합니다

* PWA Studio에 대한 AEM 확장 예제 통합

* WCM 탐색 코어 구성 요소를 확장하는 새 CIF 탐색 코어 구성 요소

### 버그 수정 {#bug-fixes-april}

* 카테고리 페이지의 페이지 속성에 있는 상거래 탭 아래에 루트 카테고리 필드가 표시되지 않았습니다

## 릴리스 날짜: 2021년 3월 {#what-is-new-march}

| GitHub | 버전 | 자세한 릴리스 노트 |
|:-------|:-----:|---------------------:|
| CIF 커넥터 | 1.9.0 | [릴리스 정보](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF 코어 구성 요소 | 1.9.0 | [릴리스 정보](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia 참조 사이트 | 2021.03.25 | [릴리스 정보](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 새로운 기능

* Magento 2.4.2 지원

### 개선 사항

* 컨텐츠 기반 페이지에 대한 제품 세부 사항 구성 요소의 재유용성 개선

* PDP에 대한 캐싱 향상 및 백엔드 호출 감소

* 여러 버그 수정.

## 릴리스 날짜: 2021년 2월

| GitHub | 버전 | 자세한 릴리스 노트 |
|:-------|:-----:|---------------------:|
| CIF 커넥터 | 1.8.0 | [릴리스 정보](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF 코어 구성 요소 | 1.8.0 | [릴리스 정보](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia 참조 사이트 | 2021.02.24 | [릴리스 정보](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 새로운 기능 {#what-is-new-february}

* 제품 경험 관리: 경험 조각을 사용하여 제품 카탈로그 페이지를 개별적으로 보강합니다.

* 연결된 컨텐츠로 빠르게 이동하는 작업을 포함하여 연결된 자산 및 경험 조각을 표시하도록 확장된 제품 콘솔 속성입니다.

### 개선 사항  {#what-is-improved-february}

* 제품 이미지 URL 및 카테고리 정보로 향상된 클라이언트측 데이터 레이어.

* 여러 버그 수정.

## 릴리스 날짜: 2021년 1월

| GitHub | 버전 | 자세한 릴리스 노트 |
|:-------|:-----:|---------------------:|
| CIF 커넥터 | 1.7.0 | [릴리스 정보](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF 코어 구성 요소 | 1.7.0 | [릴리스 정보](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia 참조 사이트 | 2021.02.02 | [릴리스 정보](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 새로운 기능 {#what-is-new-january}

* 제품 경험 관리: 자산 및 경험 조각에 대한 새 &#39;상거래&#39; 속성 탭입니다. 이 탭에서는 자산 및 경험 조각을 제품 및 카테고리에 연결할 수 있습니다. 또한 탭에는 연결된 상거래 개체에 대한 실시간 데이터와 제품 콘솔에 세부 정보를 표시하는 링크도 표시됩니다.

### 개선 사항  {#what-is-improved-january}

* 인증 후 Adobe 클라이언트 데이터 레이어로 사용자 데이터를 보냅니다.

* 여러 버그 수정.
