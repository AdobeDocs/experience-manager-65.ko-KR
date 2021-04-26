---
title: AEM 컨텐츠 및 상거래 릴리스 노트 2021
description: AEM 컨텐츠 및 상거래 릴리스 노트 2021
translation-type: tm+mt
source-git-commit: c2fb9af056fa4be13cfd7e60e8a44485e8712c0b
workflow-type: tm+mt
source-wordcount: '973'
ht-degree: 11%

---

# Commerce Integration Framework GitHub 릴리스 개요

## 릴리스 날짜:2019년 11월

| GitHub | 버전 | 자세한 릴리스 노트 |
|:-------|:-----:|---------------------:|
| CIF 커넥터 | 0.7.1 | [릴리스 정보](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF 핵심 구성 요소 | 0.6.0 | [릴리스 정보](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF 원형 | 0.6.2 | [릴리스 정보](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 새로운 기능 {#what-is-new-november}

* 작성자는 사이트 편집기에서 새로운 &quot;제품/카테고리로 보기&quot; 옵션을 사용하여 제품 세부 사항 및 제품 목록 페이지와 제품/카테고리가 포함된 페이지를 미리 볼 수 있습니다.

* 작성자는 제품 SKU로 자산에 태그를 지정하고 SKU로 제품별 자산을 검색할 수 있습니다.

* 장바구니에 쿠폰 지원 추가/제거 추가

* AEM Venia 스토어 전방에 Braintree 결제 지원 추가

### 개선 사항 {#what-is-improved-november}

* 카테고리/제품 선택기가 다중 저장소 설정의 지정된 Magento 저장소 보기를 준수하도록 개선되었습니다.

* npm 패키지로 사용할 수 있는 반응형 기반 구성 요소 이를 통해 개발자는 React Components 패키지를 새로운 React 프로젝트에 대한 종속성으로 사용하여 기존 구성 요소를 사용자 정의하거나 새로운 React 기반 구성 요소를 개발할 수 있습니다.

* GraphQL 쿼리 사용자 지정이 간소화되었습니다. 이를 통해 개발자는 더 적은 코드로 CIF 핵심 구성 요소를 사용자 정의할 수 있습니다.

## 릴리스 날짜:2019년 10월

| GitHub | 버전 | 자세한 릴리스 노트 |
|:-------|:-----:|---------------------:|
| CIF 커넥터 | 0.6.0 | [릴리스 정보](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF 핵심 구성 요소 | 0.5.0 | [릴리스 정보](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF 원형 | 0.5.0 | [릴리스 정보](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 새로운 기능 {#what-is-new-october}

* 제품 세부 정보 페이지 및 제품 목록 페이지에 대한 완성도 가능한 템플릿입니다. 이제 작성자는 이러한 템플릿에서 새 템플릿을 만들고 제품 목록 및 제품 세부 사항 구성 요소를 드래그하여 놓을 수 있습니다. 작성자는 다른 구성 요소를 추가할 수 있을 뿐만 아니라 이러한 템플릿의 레이아웃을 자유롭게 변경할 수 있으므로 마케팅과 상거래 콘텐츠를 결합하는 탁월한 경험을 제작할 수 있습니다.

* 작성자에게 친숙한 모든 CIF 핵심 구성 요소가 [AEM Style System](https://helpx.adobe.com/experience-manager/6-5/sites/authoring/using/style-system.html)을 지원하도록 개선되었습니다. 제품 목록 구성 요소에 대한 예제 스타일이 제공됩니다.

* 계정 관리를 위한 반응형 기반 클라이언트측 구성 요소 이 릴리스는 다음 기능을 지원합니다.로그인, 암호 분실 및 계정 만들기

### 개선 사항 {#what-is-improved-october}

* 제품 세부 사항 및 제품 목록 구성 요소가 템플릿/페이지에 배치되면 작성자에게 레이아웃 미리 보기를 제공하기 위해 더미 데이터를 표시하도록 개선되었습니다.

* 이제 미니 아트 및 체크 아웃 구성 요소에서 향상된 확장성을 위해 후크 반응을 사용합니다.

## 릴리스 날짜:2019년 9월

| GitHub | 버전 | 자세한 릴리스 노트 |
|:-------|:-----:|---------------------:|
| CIF 커넥터 | 0.5.0 | [릴리스 정보](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF 핵심 구성 요소 | 0.4.0 | [릴리스 정보](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF 원형 | 0.4.0 | [릴리스 정보](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 새로운 기능 {#what-is-new-september}

* 작성자가 특정 제품 세부 정보 페이지 또는 제품 목록 페이지를 보강할 수 있도록 하는 다중 템플릿 기능입니다. 작성자는 사용자 정의 제품 세부 사항 페이지 또는 제품 목록 페이지를 쉽게 만들고 제품 또는 카테고리 선택기를 사용하여 특정 제품 또는 카테고리에 사용자 정의 페이지를 지정할 수 있습니다.

* 작성자가 AEM 제품 콘솔에서 여러 카탈로그를 바인딩할 수 있도록 다중 카탈로그 바인딩. 또한 작성자는 바인딩을 만든 후 카탈로그 바인딩 속성을 편집하고 볼 수 있습니다.

* GraphQL을 사용하여 반응형 클라이언트측 체크아웃과 미니 카트를 사용하여 전체 기본 쇼핑 여정을 지원합니다.

* 체크아웃 구성 요소에는 주소 양식, 결제 선택 및 배송 방법 선택 사항이 포함되어 있습니다.

### 개선 사항 {#what-is-improved-september}

* 제품 티저 및 제품 회전판 구성 요소는 제품 변형을 지원합니다.

## 릴리스 날짜:2019년 8월

| GitHub | 버전 | 자세한 릴리스 노트 |
|:-------|:-----:|---------------------:|
| CIF 커넥터 | 0.4.0 | [릴리스 정보](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF 핵심 구성 요소 | 0.3.0 | [릴리스 정보](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF 원형 | 0.3.0 | [릴리스 정보](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 새로운 기능 {#what-is-new-august}

* CIF Tranype에 CIF Connector를 내보냈을 때 개발자에게 보다 유연하게 배포할 수 있었습니다.

* CIF 구성 요소는 &quot;Venia&quot; 특정 CSS 스타일링에서 분리되므로 개발자는 원하는 CSS 스타일링을 적용할 수 있습니다.

* 여러 AEM 사이트 구조에서 CIF 핵심 구성 요소를 사용할 수 있도록 하고 기본 GraphQL 클라이언트 구현을 통해 다른 Magento 저장소/스토어 보기에 연결할 수 있도록 하는 멀티 스토어/사이트 기능

* GraphQL 캐싱은 HTTP GET을 통해 특정 GraphQL 쿼리에 대해 활성화되므로 응답 시간을 줄일 수 있습니다.

* AEM 제품 콘솔에서 제품 설명 보기를 활성화했습니다.

* 커머스 티저는 작성자가 제품 세부 사항 페이지 또는 제품 목록 페이지에 CTA 필드를 추가할 수 있도록 WCM 티저 구성 요소를 확장합니다.

* 작성자가 AEM 페이지에 배치하여 AEM 페이지, 제품 세부 사항 페이지, 제품 목록 페이지 또는 외부 링크에 연결할 수 있는 단추입니다.

### 개선 사항 {#what-is-improved-august}

* Magento 저장소 구성이 OSGi에서 AEM 제품 콘솔로 이동되었으므로 통합 설정이 작성자에게 더 친숙해집니다.

## 릴리스 날짜:2019년 7월

| GitHub | 버전 | 자세한 릴리스 노트 |
|:-------|:-----:|---------------------:|
| CIF 커넥터 | 0.3.0 | [릴리스 정보](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF 핵심 구성 요소 | 0.2.0 | [릴리스 정보](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF 원형 | 0.2.0 | [릴리스 정보](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 새로운 기능 {#what-is-new-july}

* 개발자에게 다음과 같은 다양한 배포 옵션을 제공하는 최초의 CIF Lianype1.AEM Venia 스토어 프런트 2를 배포합니다. 새 프로젝트에 대한 Scaffolding 배포 3. 기존 프로젝트에서 CIF 요소 사용

* 카테고리 및 하위 카테고리 간의 탐색을 지원하는 여러 수준의 카탈로그 탐색.

* 카테고리 페이지에서 페이지 매김을 통해 UX를 향상시킬 수 있습니다.

* 동적 속성 렌더링을 지원하기 위해 제품 세부 사항 및 제품 목록 구성 요소에 있는 가격 특성의 클라이언트측 렌더링입니다.

* 서버 측 제품 Carousel을 사용하여 추천 제품 목록을 회전판 스타일로 표시합니다.

* AEM 페이지에 카테고리 목록을 표시하는 서버측 주요 카테고리 목록.

### 개선 사항 {#what-is-improved-july}

* 제품 속성과 관련된 Magento 2.3.2 지원 및 버그 수정이 제품 콘솔에 표시됩니다.

## 릴리스 날짜:2019년 6월

| GitHub | 버전 | 자세한 릴리스 노트 |
|:-------|:-----:|---------------------:|
| CIF 커넥터 | 0.2.0 | [릴리스 정보](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF 핵심 구성 요소 | 0.1.0 | [릴리스 정보](https://github.com/adobe/aem-core-cif-components/releases) |

### 새로운 기능 {#what-is-new-june}

* 커머스 프로젝트를 시작 및 가속화하는 AEM B2C 스토어를 통해 모바일 퍼스트 Venia CSS 스타일, 랜딩 페이지, 제품 및 카테고리 페이지를 통한 다이내믹한 카탈로그 내비게이션, 제품 검색 페이지, 장바구니 기능을 이용할 수 있습니다.

* CIF 커넥터 및 제작 도구(제품 콘솔, 제품 피커 및 카테고리 선택기)를 사용하여 작성자가 전자 상거래 컨텐츠가 있는 AEM에서 경험을 만들 수 있습니다.

* Magento 2.3.1과 호환되는 CIF 핵심 구성 요소의 첫 번째 버전:
   * 제품 세부 사항
   * 제품 목록
   * 제품 티저
   * 탐색
   * 제품 검색
   * 장바구니(REST)

