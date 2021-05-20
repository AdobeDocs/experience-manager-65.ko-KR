---
title: AEM Content and Commerce 릴리스 노트 2021
description: AEM Content and Commerce 릴리스 노트 2021
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 15%

---

# Commerce Integration Framework GitHub 릴리스 개요

## 시스템 요구 사항 개요

현재 사용 중인 CIF 버전 또는 향후 사용할 예정인 최소 시스템 요구 사항을 아래 표에서 검토하십시오.

**이제  [Adobe 소프트웨어 배포를 통해 CIF 추가 기능을 사용할 수 있습니다](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). 이전 AEM CIF 커넥터가 유지 관리 모드로 전환되고 있으므로 더 이상 사용하지 않아야 합니다. 새 CIF 추가 기능으로 마이그레이션하십시오.**

| 구성 요소 | 시스템 요구 사항 |
|:-------|:-----:|
| CIF 추가 기능 | 최소:AEM 6.5.7, Magento 2.3.5 GraphQL 스키마 |
| CIF 코어 구성 요소 | [시스템 요구 사항](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM 프로젝트 전형 | [시스템 요구 사항](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## 릴리스 날짜:2021년 4월

| 구성 요소 | 버전 | 세부 사항 |
|:-------|:-----:|---------------------:|
| CIF 추가 기능 | 2021.04.22 | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.04.22.zip) |
| CIF 코어 구성 요소 | 1.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia 참조 사이트 | 2021.04.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 새로운 기능 {#what-is-new-april}

* 카테고리 UID 지원 - 카테고리 ID에 문자열을 사용하는 시스템에 대한 타사 상거래 통합을 잠금 해제합니다

* PWA Studio에 대한 AEM 확장 예제 통합

* WCM 탐색 코어 구성 요소를 확장하는 새 CIF 탐색 코어 구성 요소

* AEM storefront의 스테이지된 카탈로그 데이터에 대한 시각적 표시기

### 버그 수정 {#bug-fixes-april}

* 카테고리 페이지의 페이지 속성에 있는 상거래 탭 아래에 루트 카테고리 필드가 표시되지 않았습니다

## 릴리스 날짜:2021년 3월 {#what-is-new-march}

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

## 릴리스 날짜:2021년 2월

| GitHub | 버전 | 자세한 릴리스 노트 |
|:-------|:-----:|---------------------:|
| CIF 커넥터 | 1.8.0 | [릴리스 정보](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF 코어 구성 요소 | 1.8.0 | [릴리스 정보](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia 참조 사이트 | 2021.02.24 | [릴리스 정보](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 새로운 기능 {#what-is-new-february}

* 제품 경험 관리:경험 조각을 사용하여 제품 카탈로그 페이지를 개별적으로 보강합니다.

* 연결된 컨텐츠로 빠르게 이동하는 작업을 포함하여 연결된 자산 및 경험 조각을 표시하도록 확장된 제품 콘솔 속성입니다.

### 개선 사항 {#what-is-improved-february}

* 제품 이미지 URL 및 카테고리 정보로 향상된 클라이언트측 데이터 레이어.

* 여러 버그 수정.

## 릴리스 날짜:2021년 1월

| GitHub | 버전 | 자세한 릴리스 노트 |
|:-------|:-----:|---------------------:|
| CIF 커넥터 | 1.7.0 | [릴리스 정보](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF 코어 구성 요소 | 1.7.0 | [릴리스 정보](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia 참조 사이트 | 2021.02.02 | [릴리스 정보](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 새로운 기능 {#what-is-new-january}

* 제품 경험 관리:자산 및 경험 조각에 대한 새 &#39;상거래&#39; 속성 탭입니다. 이 탭에서는 자산 및 경험 조각을 제품 및 카테고리에 연결할 수 있습니다. 또한 탭에는 연결된 상거래 개체에 대한 실시간 데이터와 제품 콘솔에 세부 정보를 표시하는 링크도 표시됩니다.

### 개선 사항 {#what-is-improved-january}

* 인증 후 Adobe 클라이언트 데이터 레이어로 사용자 데이터를 보냅니다.

* 여러 버그 수정.
