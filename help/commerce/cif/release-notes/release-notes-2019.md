---
title: AEM Content 및 Commerce 릴리스 노트 2019
description: 2019년 Adobe Experience Manager 컨텐츠 및 Commerce 릴리스 노트.
exl-id: 7e61a75d-6b35-46ee-b88a-444c10b2708f
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 7%

---

# Commerce integration framework GitHub 릴리스 개요

## 릴리스 날짜: 2019년 11월

| GitHub | 버전 | 자세한 릴리스 정보 |
|:-------|:-----:|---------------------:|
| CIF 커넥터 | 0.7.1 | [릴리스 정보](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF 핵심 구성 요소 | 0.6.0 | [릴리스 정보](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Archetype | 0.6.2 | [릴리스 정보](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 새로운 기능 {#what-is-new-november}

* 작성자는 Sites 편집기에서 새로운 &quot;제품/범주로 보기&quot; 옵션을 사용하여 제품/범주가 있는 제품 세부 사항 및 제품 목록 페이지를 미리 볼 수 있습니다.

* 작성자는 제품 SKU별로 자산에 태그를 지정하고 SKU별로 제품별 자산을 검색할 수 있습니다.

* 장바구니에 추가된 쿠폰 지원 추가/제거.

* AEM Venia 스토어 전면에 Braintree 결제 지원이 추가되었습니다.

### 개선 사항 {#what-is-improved-november}

* 다중 스토어 설정에서 지정된 Adobe Commerce 스토어 보기를 준수하도록 카테고리/제품 선택기가 개선되었습니다.

* React 기반 구성 요소는 npm 패키지로 사용할 수 있습니다. 이를 통해 개발자는 새 React 프로젝트에 대한 종속성으로 React 구성 요소 패키지를 사용하여 기존 구성 요소를 사용자 정의하거나 새 React 기반 구성 요소를 개발할 수 있습니다.

* GraphQL 쿼리 사용자 지정이 단순해졌습니다. 이를 통해 개발자는 더 적은 코드로 CIF 핵심 구성 요소를 사용자 정의할 수 있습니다.

## 릴리스 날짜: 2019년 10월

| GitHub | 버전 | 자세한 릴리스 정보 |
|:-------|:-----:|---------------------:|
| CIF 커넥터 | 0.6.0 | [릴리스 정보](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF 핵심 구성 요소 | 0.5.0 | [릴리스 정보](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Archetype | 0.5.0 | [릴리스 정보](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 새로운 기능 {#what-is-new-october}

* 제품 세부 사항 페이지 및 제품 목록 페이지에 대한 완전히 작성 가능한 템플릿. 이제 작성자가 템플릿을 만들고 이러한 템플릿에서 제품 목록 및 제품 세부 사항 구성 요소를 드래그하여 놓을 수 있습니다. 이제 다른 구성 요소를 추가할 수 있을 뿐만 아니라 작성자도 이러한 템플릿의 레이아웃을 변경하여 마케팅 및 상거래 콘텐츠를 결합한 놀라운 경험을 자유롭게 만들 수 있습니다.

* 작성자에게 친숙한 모든 CIF 핵심 구성 요소가 [AEM의 스타일 시스템](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/siteandpage/style-system.html)을 지원하도록 개선되었습니다. 제품 목록 구성 요소에 예제 스타일이 제공되었습니다.

* 계정 관리를 위한 React 기반 클라이언트측 구성 요소입니다. 이 릴리스는 로그인, 암호 분실 및 계정 만들기 기능을 지원합니다.

### 개선 사항 {#what-is-improved-october}

* 제품 세부 사항 및 제품 목록 구성 요소가 템플릿/페이지에 배치되면 작성자에게 레이아웃 미리보기를 제공하기 위해 더미 데이터를 표시하도록 개선되었습니다.

* 이제 Minicart 및 Checkout 구성 요소는 확장성을 개선하기 위해 React 후크를 사용합니다.

## 릴리스 날짜: 2019년 9월

| GitHub | 버전 | 자세한 릴리스 정보 |
|:-------|:-----:|---------------------:|
| CIF 커넥터 | 0.5.0 | [릴리스 정보](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF 핵심 구성 요소 | 0.4.0 | [릴리스 정보](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Archetype | 0.4.0 | [릴리스 정보](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 새로운 기능 {#what-is-new-september}

* 다중 템플릿 기능을 사용하면 작성자가 특정 제품 세부 사항 페이지나 제품 목록 페이지를 보강할 수 있습니다. 작성자는 사용자 정의 제품 세부 사항 페이지 또는 제품 목록 페이지를 쉽게 만들고 제품 또는 카테고리 선택기를 사용하여 사용자 정의 페이지를 특정 제품 또는 카테고리에 할당할 수 있습니다.

* 작성자가 AEM 제품 콘솔에서 여러 카탈로그를 바인딩할 수 있도록 하는 다중 카탈로그 바인딩. 작성자는 바인딩을 만든 후 카탈로그 바인딩 속성을 편집하고 볼 수도 있습니다.

* GraphQL을 사용하는 React 기반 클라이언트측 체크아웃 및 미니 장바구니로 완벽한 기본 쇼핑 여정을 지원합니다.

* 체크아웃 구성 요소에는 주소 양식, 결제 선택 및 배송 방법 선택이 포함됩니다.

### 개선 사항 {#what-is-improved-september}

* 제품 티저 및 제품 슬라이드 구성 요소는 제품 변형을 지원합니다.

## 릴리스 날짜: 2019년 8월

| GitHub | 버전 | 자세한 릴리스 정보 |
|:-------|:-----:|---------------------:|
| CIF 커넥터 | 0.4.0 | [릴리스 정보](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF 핵심 구성 요소 | 0.3.0 | [릴리스 정보](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Archetype | 0.3.0 | [릴리스 정보](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 새로운 기능 {#what-is-new-august}

* 개발자에게 보다 많은 유연성을 제공하기 위해 CIF Archetype에 CIF 커넥터 임베딩이 선택 사항입니다.

* CIF 구성 요소는 &quot;Venia&quot; 특정 CSS 스타일링과 분리되어 개발자가 원하는 CSS 스타일링을 적용할 수 있습니다.

* 여러 AEM 사이트 구조에서 CIF 핵심 구성 요소를 사용하고 기본 GraphQL 클라이언트 구현이 다른 Adobe Commerce 스토어/스토어 보기에 연결할 수 있도록 하는 다중 스토어/사이트 기능입니다.

* GraphQL 캐싱은 응답 시간을 줄이기 위해 HTTP GET을 통해 특정 GraphQL 쿼리에 대해 활성화됩니다.

* 제품 설명 보기는 AEM 제품 콘솔에서 활성화됩니다.

* Commerce 티저는 작성자가 CTA 필드를 제품 세부 사항 페이지 또는 제품 목록 페이지에 추가할 수도 있도록 WCM 티저 구성 요소를 확장합니다.

* 작성자가 AEM 페이지에 배치하고 AEM 페이지, 제품 세부 사항 페이지, 제품 목록 페이지 또는 외부 링크에 연결할 수 있는 단추입니다.

### 개선 사항 {#what-is-improved-august}

* 통합 설정을 보다 작성자 친화적으로 만들기 위해 Adobe Commerce 스토어 구성이 OSGi에서 AEM 제품 콘솔로 이동되었습니다.

## 릴리스 날짜: 2019년 7월

| GitHub | 버전 | 자세한 릴리스 정보 |
|:-------|:-----:|---------------------:|
| CIF 커넥터 | 0.3.0 | [릴리스 정보](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF 핵심 구성 요소 | 0.2.0 | [릴리스 정보](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Archetype | 0.2.0 | [릴리스 정보](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 새로운 기능 {#what-is-new-july}

* 개발자에게 여러 배포 옵션을 제공하는 첫 번째 CIF Archetype: 1.Deploy AEM Venia storefront 2. 새 프로젝트에 대한 스캐폴딩 배포 3. 기존 프로젝트에서 CIF 요소 사용

* 범주 및 하위 범주를 통한 탐색을 지원하는 다중 레벨 카탈로그 탐색.

* 더 나은 UX를 위해 카테고리 페이지의 페이지 매김.

* 동적 특성 렌더링을 지원하기 위한 제품 세부 사항 및 제품 목록 구성 요소의 가격 특성에 대한 클라이언트측 렌더링.

* 서버측 제품 슬라이드 - 주요 제품 목록을 슬라이드 스타일로 표시합니다.

* AEM 페이지에 카테고리 목록을 표시하는 서버측 추천 카테고리 목록입니다.

### 개선 사항 {#what-is-improved-july}

* Adobe Commerce 2.3.2에 대한 지원 및 제품 속성과 관련된 버그 수정이 제품 콘솔에 표시됩니다.

## 릴리스 날짜: 2019년 6월

| GitHub | 버전 | 자세한 릴리스 정보 |
|:-------|:-----:|---------------------:|
| CIF 커넥터 | 0.2.0 | [릴리스 정보](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF 핵심 구성 요소 | 0.1.0 | [릴리스 정보](https://github.com/adobe/aem-core-cif-components/releases) |

### 새로운 기능 {#what-is-new-june}

* 모바일 최초 Venia CSS 스타일링, 랜딩 페이지, 제품 및 카테고리 페이지를 통한 동적 카탈로그 탐색, 제품 검색 페이지, 장바구니 기능을 갖춘 AEM B2C 스토어프론트로 상거래 프로젝트를 시작하고 가속화합니다.

* CIF 커넥터 및 작성 도구(제품 콘솔, 제품 선택기 및 카테고리 선택기)를 사용하여 작성자는 상거래 콘텐츠가 있는 AEM에서 경험을 만들 수 있습니다.

* Adobe Commerce 2.3.1과 호환되는 CIF 핵심 구성 요소의 첫 번째 버전:
   * 제품 세부 사항
   * 제품 목록
   * 제품 티저
   * 탐색
   * 제품 검색
   * 장바구니(REST)
