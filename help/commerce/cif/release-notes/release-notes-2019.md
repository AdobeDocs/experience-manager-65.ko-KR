---
title: AEM Content and Commerce 릴리스 노트 2021
description: AEM Content and Commerce 릴리스 노트 2021
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '973'
ht-degree: 10%

---

# Commerce Integration Framework GitHub 릴리스 개요

## 릴리스 날짜:2019년 11월

| GitHub | 버전 | 자세한 릴리스 노트 |
|:-------|:-----:|---------------------:|
| CIF 커넥터 | 0.7.1 | [릴리스 정보](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF 코어 구성 요소 | 0.6.0 | [릴리스 정보](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF 원형 | 0.6.2 | [릴리스 정보](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 새로운 기능 {#what-is-new-november}

* 작성자는 사이트 편집기에서 새 &quot;제품/카테고리를 사용한 보기&quot; 옵션을 사용하여 제품 세부 사항 및 제품 목록 페이지를 미리 볼 수 있습니다.

* 작성자는 제품 SKU별로 자산에 태그를 지정하고 SKU별로 제품별 자산을 검색할 수 있습니다.

* 장바구니에 추가된 쿠폰 지원을 추가/제거합니다.

* AEM Venia 스토어 전방에 Braintree 결제 지원이 추가되었습니다.

### 개선 사항 {#what-is-improved-november}

* 카테고리/제품 선택기가 다중 저장소 설정에서 지정된 Magento 저장소 보기를 준수하도록 개선되었습니다.

* npm 패키지로 사용할 수 있는 React 기반 구성 요소. 이를 통해 개발자는 새 React 프로젝트에 대한 종속성으로 React 구성 요소 패키지를 사용하여 기존 구성 요소를 사용자 지정하거나 새로운 React 기반 구성 요소를 개발할 수 있습니다.

* GraphQL 쿼리 사용자 지정이 단순해졌습니다. 이렇게 하면 개발자가 적은 코드로 CIF 코어 구성 요소를 사용자 지정할 수 있습니다.

## 릴리스 날짜:2019년 10월

| GitHub | 버전 | 자세한 릴리스 노트 |
|:-------|:-----:|---------------------:|
| CIF 커넥터 | 0.6.0 | [릴리스 정보](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF 코어 구성 요소 | 0.5.0 | [릴리스 정보](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF 원형 | 0.5.0 | [릴리스 정보](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 새로운 기능 {#what-is-new-october}

* 제품 세부 사항 페이지 및 제품 목록 페이지에 대한 완전히 작성 가능한 템플릿. 이제 작성자가 이러한 템플릿에 대해 새 템플릿을 만들고 제품 목록 및 제품 세부 사항 구성 요소를 드래그하여 놓을 수 있습니다. 작성자는 다른 구성 요소를 추가할 수 있을 뿐만 아니라 이제 이러한 템플릿의 레이아웃을 변경할 수 있으므로 마케팅 및 상거래 콘텐츠를 결합한 놀라운 경험을 만들 수 있는 무제한의 자유를 제공합니다.

* 작성자에게 친숙한 모든 CIF 코어 구성 요소가 [AEM 스타일 시스템](https://helpx.adobe.com/experience-manager/6-5/sites/authoring/using/style-system.html)을 지원하도록 개선되었습니다. 제품 목록 구성 요소에 대한 예제 스타일이 제공되었습니다.

* 계정 관리를 위한 React 기반 클라이언트측 구성 요소. 이 릴리스는 다음과 같은 기능을 지원합니다.로그인, 암호 분실 및 계정 만들기

### 개선 사항 {#what-is-improved-october}

* 제품 세부 사항 및 제품 목록 구성 요소가 향상되어 작성자가 템플릿/페이지에 배치할 때 레이아웃의 미리 보기를 제공할 수 있습니다.

* 이제 Minicart 및 Checkout 구성 요소가 향상된 확장성을 위해 React 후크를 사용합니다.

## 릴리스 날짜:2019년 9월

| GitHub | 버전 | 자세한 릴리스 노트 |
|:-------|:-----:|---------------------:|
| CIF 커넥터 | 0.5.0 | [릴리스 정보](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF 코어 구성 요소 | 0.4.0 | [릴리스 정보](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF 원형 | 0.4.0 | [릴리스 정보](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 새로운 기능 {#what-is-new-september}

* 작성자가 특정 제품 세부 사항 페이지나 제품 목록 페이지를 보강할 수 있는 다중 템플릿 기능입니다. 작성자는 사용자 지정 제품 세부 사항 페이지나 제품 목록 페이지를 쉽게 만들고 제품 또는 카테고리 선택기를 사용하여 특정 제품이나 카테고리에 사용자 지정 페이지를 할당할 수 있습니다.

* 작성자가 AEM 제품 콘솔에서 여러 카탈로그를 바인딩할 수 있는 다중 카탈로그 바인딩. 작성자는 바인딩을 만든 후 카탈로그 바인딩 속성을 편집하고 볼 수도 있습니다.

* GraphQL을 사용하여 React 기반 클라이언트측 체크아웃 및 미니 장바구니에서 전체 기본 쇼핑 여정을 지원합니다.

* 체크아웃 구성 요소에는 주소 양식, 결제 선택 및 운송 방법 선택 등이 포함됩니다.

### 개선 사항 {#what-is-improved-september}

* 제품 티저 및 제품 회전판 구성 요소는 제품 변형을 지원합니다.

## 릴리스 날짜:2019년 8월

| GitHub | 버전 | 자세한 릴리스 노트 |
|:-------|:-----:|---------------------:|
| CIF 커넥터 | 0.4.0 | [릴리스 정보](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF 코어 구성 요소 | 0.3.0 | [릴리스 정보](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF 원형 | 0.3.0 | [릴리스 정보](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 새로운 기능 {#what-is-new-august}

* CIF Tranype에 CIF Connector를 포함하면 개발자에게 더 많은 유연성을 제공할 수 있는 선택 사항이 되었습니다.

* CIF 구성 요소는 개발자가 원하는 CSS 스타일을 적용할 수 있도록 &quot;Venia&quot; 특정 CSS 스타일링에서 분리됩니다.

* 여러 AEM 사이트 구조에서 CIF 코어 구성 요소를 사용할 수 있고 기본 GraphQL 클라이언트 구현에서 다른 Magento 저장소/저장소 보기에 연결할 수 있는 다중 저장소/사이트 기능입니다.

* HTTP GET을 통해 특정 GraphQL 쿼리에 GraphQL 캐싱이 활성화되어 응답 시간을 줄일 수 있습니다.

* AEM 제품 콘솔에서 활성화된 제품 설명 보기.

* Commerce Teaser는 WCM Teaser 구성 요소를 확장하여 작성자가 제품 세부 사항 페이지나 제품 목록 페이지에 CTA 필드를 추가할 수도 있습니다.

* 작성자가 AEM 페이지에 배치하여 AEM 페이지, 제품 세부 사항 페이지, 제품 목록 페이지 또는 외부 링크에 연결할 수 있는 단추입니다.

### 개선 사항 {#what-is-improved-august}

* Magento 저장소 구성이 OSGi에서 AEM 제품 콘솔로 이동되었으므로 통합 설정을 보다 작성자가 친숙한 상태로 만듭니다.

## 릴리스 날짜:2019년 7월

| GitHub | 버전 | 자세한 릴리스 노트 |
|:-------|:-----:|---------------------:|
| CIF 커넥터 | 0.3.0 | [릴리스 정보](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF 코어 구성 요소 | 0.2.0 | [릴리스 정보](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF 원형 | 0.2.0 | [릴리스 정보](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 새로운 기능 {#what-is-new-july}

* 개발자에게 몇 가지 배포 옵션을 제공하는 첫 번째 CIF Archetype입니다.1. AEM Venia storefront 2를 배포합니다. 새 프로젝트 3에 대한 스캐폴딩을 배포합니다. 기존 프로젝트에서 CIF 요소 사용

* 카테고리 및 하위 카테고리를 통한 탐색을 지원하는 다중 수준 카탈로그 탐색.

* 더 나은 UX를 위해 카테고리 페이지의 페이지 매김

* 동적 속성 렌더링을 지원하기 위해 제품 세부 사항 및 제품 목록 구성 요소에 있는 가격 속성의 클라이언트측 렌더링.

* 서버 측 제품 회전판 을 사용하여 추천 제품 목록을 회전판 스타일로 표시합니다.

* 서버측 주요 카테고리 목록 을 사용하여 AEM 페이지에 있는 카테고리 목록을 표시할 수 있습니다.

### 개선 사항 {#what-is-improved-july}

* 제품 속성과 관련된 Magento 2.3.2 및 버그 수정에 대한 지원이 제품 콘솔에 표시됩니다.

## 릴리스 날짜:2019년 6월

| GitHub | 버전 | 자세한 릴리스 노트 |
|:-------|:-----:|---------------------:|
| CIF 커넥터 | 0.2.0 | [릴리스 정보](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF 코어 구성 요소 | 0.1.0 | [릴리스 정보](https://github.com/adobe/aem-core-cif-components/releases) |

### 새로운 기능 {#what-is-new-june}

* AEM B2C 스토어프런트에 모바일 첫 번째 Venia CSS 스타일링, 랜딩 페이지, 제품 및 카테고리 페이지를 통한 동적 카탈로그 탐색, 제품 검색 페이지, 장바구니 기능을 추가하여 상거래 프로젝트를 시작하고 가속화할 수 있습니다.

* CIF 커넥터 및 작성 도구(제품 콘솔, 제품 선택기 및 카테고리 선택기)를 사용하여 작성자가 전자 상거래 컨텐츠가 있는 AEM에서 경험을 만들 수 있습니다.

* Magento 2.3.1과 호환되는 CIF 코어 구성 요소의 첫 번째 버전:
   * 제품 세부 사항
   * 제품 목록
   * 제품 티저
   * 탐색
   * 제품 검색
   * 장바구니(REST)

