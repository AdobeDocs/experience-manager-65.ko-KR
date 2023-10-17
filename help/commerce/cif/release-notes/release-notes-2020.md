---
title: AEM Content and Commerce 릴리스 노트 2020
description: Adobe Experience Manager Content and Commerce 릴리스 노트 2020.
exl-id: 440ecd8e-55dc-4606-8678-c65cda1d2b3a
source-git-commit: eaffc71c23c18d26ec5cbb2bbb7524790c4826fe
workflow-type: tm+mt
source-wordcount: '1354'
ht-degree: 15%

---

# Commerce integration framework GitHub 릴리스 개요

## 릴리스 날짜: 2020년 11월

| GitHub | 버전 | 자세한 릴리스 정보 |
|:-------|:-----:|---------------------:|
| CIF 커넥터 | 1.6.0 | [릴리스 정보](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF 핵심 구성 요소 | 1.6.0 | [릴리스 정보](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia 참조 사이트 | 2020.12.01 | [릴리스 정보](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 새로운 기능 {#what-is-new-november}

* 템플릿 상속이 특정 카테고리 페이지에 추가되었습니다. 이 기능을 사용하면 모든 하위 범주가 특정 상위 범주에 대해 만들어진 템플릿을 상속할 수 있으므로 비즈니스 사용자 효율이 향상됩니다.

* Venia 참조 상점이 바닥글에 경험 조각을 사용하도록 업데이트되었습니다. 비즈니스 사용자는 AEM 작성 도구를 사용하여 페이지 바닥글을 편집할 수 있습니다.

### 개선 사항 {#what-is-improved-november}

* 체크아웃 구성 요소를 개선하여 쇼핑객이 미국 이외의 국가에서 청구/배송 주소를 허용할 수 있도록 대상 국가를 입력할 수 있습니다.

* Adobe 클라이언트 데이터 레이어 하이드레이션하기 위해 확장된 탐색 구성 요소입니다.

* 여러 버그 수정.

## 릴리스 날짜: 2020년 10월

| GitHub | 버전 | 자세한 릴리스 정보 |
|:-------|:-----:|---------------------:|
| CIF 커넥터 | 1.5.0 | [릴리스 정보](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF 핵심 구성 요소 | 1.5.0 | [릴리스 정보](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia 참조 사이트 | 2020.10.27 | [릴리스 정보](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 새로운 기능 {#what-is-new-october}

* 비즈니스 사용자가 AEM 콘텐츠 페이지에서 이 구성 요소를 드래그 앤 드롭하여 상거래 데이터로 콘텐츠 페이지를 보강할 수 있도록 새 카테고리 캐러셀 구성 요소를 추가했습니다.

* 상거래 데이터를 전송하여 Adobe 클라이언트 데이터 레이어를 하이드레이션하도록 확장된 CIF 핵심 구성 요소입니다. Adobe 클라이언트 데이터 계층 은 데이터를 수집하고 데이터를 Digital Analytics 및 보고 서버에 전달하는 표준화된 방법입니다. 자세한 내용은 다음을 참조하십시오. [Adobe 클라이언트 데이터 레이어](https://github.com/adobe/adobe-client-data-layer/wiki).

* Adobe Commerce 관리 UI 내에서 구성된 SEO 메타데이터(예: 제목, 메타 설명, 메타 키워드)를 자동으로 채우도록 제품 세부 사항 및 제품 목록 페이지가 확장되었습니다

* Commerce 티저 구성 요소 버그가 수정되었습니다.

## 릴리스 날짜: 2020년 9월

| GitHub | 버전 | 자세한 릴리스 정보 |
|:-------|:-----:|---------------------:|
| CIF 커넥터 | 1.4.0 | [릴리스 정보](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF 핵심 구성 요소 | 1.4.0 | [릴리스 정보](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia 참조 사이트 | 2020.10.2 | [릴리스 정보](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 새로운 기능 {#what-is-new-september}

* Adobe Commerce 2.4.0 스키마에 대한 쿼리를 지원합니다.

* 구매자가 개인 정보를 업데이트할 수 있도록 계정 정보 기능이 추가되었습니다.

* 제품 목록 및 검색 결과 페이지에 대해 소극적 로드 페이지 매김 스타일이 구현되어 개발자가 이러한 구성 요소를 구성하여 &quot;추가 로드&quot; 단추를 페이지 매김 스타일로 표시할 수 있습니다.

* 암호 재설정 페이지는 구매자가 계정 암호를 업데이트/재설정할 수 있도록 구현되었습니다.

* 번들 제품 유형에 대한 지원을 사용할 수 있습니다.

* 개발자는 SEO 모범 사례를 따르도록 제품 캐러셀, 관련 제품 및 주요 카테고리 목록 구성 요소에 대한 HTML 태그를 구성할 수 있습니다.

* 내 계정 버그가 수정되었습니다.

* 여러 버그 수정.

## 릴리스 날짜: 2020년 8월

| GitHub | 버전 | 자세한 릴리스 정보 |
|:-------|:-----:|---------------------:|
| CIF 커넥터 | 1.3.0 | [릴리스 정보](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF 핵심 구성 요소 | 1.3.0 | [릴리스 정보](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia 참조 사이트 | 2020.9.2 | [릴리스 정보](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 새로운 기능 {#what-is-new-august}

* 콘텐츠 및 상거래 페이지를 지원하기 위해 이동 경로 구성 요소가 추가되었습니다.

* 랜딩 페이지 및 경험 조각에 대한 CIF 속성을 노출하기 위해 페이지 속성에 상거래 탭이 추가되었습니다.

* 자리 표시자 텍스트를 표시하는 옵션을 지원하도록 검색 막대 구성 요소가 개선되었습니다

* 제품 및 제품 티저 구성 요소에 유연성을 추가하여 간편한 맞춤화를 지원합니다.

* 제품 티저 구성 요소에 대한 기본 CTA 버튼 레이블을 재정의하고 구성할 수 있는 유연성이 추가되었습니다.

* 주소록 구성 요소는 체크아웃 중에 등록된 구매자가 주소록에 저장된 배송 및 청구 주소를 선택할 수 있도록 개선되었습니다.

* 여러 버그 수정.

## 릴리스 날짜: 2020년 7월

| GitHub | 버전 | 자세한 릴리스 정보 |
|:-------|:-----:|---------------------:|
| CIF 커넥터 | 1.2.0 | [릴리스 정보](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF 핵심 구성 요소 | 1.2.0 | [릴리스 정보](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia 참조 사이트 | 2020.8.14 | [릴리스 정보](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 새로운 기능 {#what-is-new-july}

* CIF Venia 참조 사이트는 CIF Archetype 저장소에서 추출되었으며 이제 독립 실행형 GitHub 저장소입니다.

* CIF Archetype이 AEM Project Archetype과 병합됩니다. 새 프로젝트의 경우 다음을 사용하십시오. [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) 을(를) 시작점으로 선택합니다.

* 로그인한 사용자가 주소를 관리할 수 있도록 주소록 관리가 추가되었습니다.

* CIF Cloud 구성 UI는 게시/게시 취소 작업을 지원합니다.

### 개선 사항 {#what-is-improved-july}

* 쉽게 액세스할 수 있도록 로그인 구성 요소가 사용자 드롭다운으로 이동되었습니다.

* Aem-core-cif-react-components 패키지를 간소화했습니다.

* 여러 버그 수정.

## 릴리스 날짜: 2020년 6월

| GitHub | 버전 | 자세한 릴리스 정보 |
|:-------|:-----:|---------------------:|
| CIF 커넥터 | 1.1.0 | [릴리스 정보](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF 핵심 구성 요소 | 1.1.1 | [릴리스 정보](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Archetype | 0.11.0 | [릴리스 정보](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 새로운 기능 {#what-is-new-june}

Adobe Experience Manager에서 지원되는 CIF 핵심 구성 요소의 첫 번째 버전입니다.

* 구매자가 관련성, 가격 및 제품 이름을 기준으로 정렬할 수 있도록 제품 목록 페이지 및 검색 결과 페이지에 제품 정렬을 추가했습니다.

* 쇼핑객이 카테고리를 기준으로 필터링할 수 있도록 카테고리 필터링을 패싯으로 추가했습니다.

* ACL을 직접 조작하지 않고 서비스 사용자를 통해 /conf에 액세스할 수 있도록 하는 보안 요구 사항의 일부로 서비스 사용자 매핑을 추가했습니다. 이제 CIF 핵심 구성 요소는 서비스 사용자를 사용하여 구성에 액세스해야 합니다.

### 개선 사항 {#what-is-improved-june}

* 제품 목록 페이지와 검색 결과 페이지에 총 항목 수가 표시됩니다. 항목 수는 쇼핑객이 필터를 적용하면 업데이트됩니다.

* 패싯된 검색은 카테고리 쿼리를 제품 검색 쿼리와 결합하여 최적화됩니다.

* 페이지 미리보기에 대한 범주/제품 선택기는 cq:catalogPath를 수행합니다.

* 여러 버그 수정.

## 릴리스 날짜: 2020년 5월

| GitHub | 버전 | 자세한 릴리스 정보 |
|:-------|:-----:|---------------------:|
| CIF 커넥터 | 1.0.0 | [릴리스 정보](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF 핵심 구성 요소 | 1.0.0 | [릴리스 정보](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Archetype | 0.11.0 | [릴리스 정보](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 새로운 기능 {#what-is-new-may}

* Adobe Commerce 2.3.5 스키마에 대한 쿼리를 지원합니다.

* 구매자가 제품 패싯을 기반으로 검색 결과를 필터링할 수 있도록 검색 페이지 및 제품 목록 페이지에 패싯된 검색 지원이 추가되었습니다.

* SEO 목적으로 PDP/PLP URL을 사용자 정의하기 위해 새 OSGi 서비스가 추가되었습니다. 자세한 내용은 [설명서](https://github.com/adobe/aem-core-cif-components).

* 클라우드 구성이 생성되면 제품 바인딩이 자동으로 생성됩니다.

### 개선 사항

* 클라우드 구성이 확장되어 &quot;폴더 만들기&quot; 작업이 표시됩니다.

* 여러 버그 수정이 적용되었습니다.

## 릴리스 날짜: 2020년 4월

| GitHub | 버전 | 자세한 릴리스 정보 |
|:-------|:-----:|---------------------:|
| CIF 커넥터 | 0.10.0 | [릴리스 정보](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF 핵심 구성 요소 | 0.10.0 | [릴리스 정보](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Archetype | 0.10.0 | [릴리스 정보](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 새로운 기능 {#what-is-new-april}

* CIF Connector에 대한 구성 설정이 통합 및 단순화되었습니다. 자세한 내용은 체크아웃을 참조하십시오 [시작](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/home.html) 또는 [새 AEM CIF 프로젝트 설정](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/home.html)

### 개선 사항 {#what-is-improved-april}

* 장바구니 및 체크아웃 흐름은 등록된 쇼핑객을 지원하도록 확장되었습니다.

* 모든 구성 요소에 대해 확장된 다국어화 지원

* 그룹화된 제품 및 가상 제품에 대한 지원을 사용할 수 있습니다.

* 관련 제품, 제품 캐러셀 및 주요 카테고리 구성 요소를 개선하여 선택적 제목을 지원합니다.

* 여러 버그 수정이 적용되었습니다.

## 릴리스 날짜: 2020년 2월

| GitHub | 버전 | 자세한 릴리스 정보 |
|:-------|:-----:|---------------------:|
| CIF 커넥터 | 0.9.0 | [릴리스 정보](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF 핵심 구성 요소 | 0.9.0 | [릴리스 정보](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Archetype | 0.9.0 | [릴리스 정보](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 새로운 기능 {#what-is-new-february}

* Adobe Commerce 2.3.4 스키마에 대한 쿼리를 지원합니다.

* 범주 선택기에 검색 지원이 추가되었습니다.

* 큰 카탈로그 집합을 지원하는 범주 목록 구성 요소의 페이지 매김.

### 개선 사항 {#what-is-improved-february}

* 장바구니가 할인율을 표시하도록 개선되었습니다.

* 제품 세부 사항, 제품 티저 및 제품 목록 구성 요소는 고급 가격 정보 표시를 지원합니다.

* 제품 콘솔 및 제품 선택기의 제품 검색이 개선되었습니다.

* 여러 버그 수정이 적용되었습니다.

## 릴리스 날짜: 2020년 1월

| GitHub | 버전 | 자세한 릴리스 정보 |
|:-------|:-----:|---------------------:|
| CIF 커넥터 | 0.8.0 | [릴리스 정보](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF 핵심 구성 요소 | 0.8.0 | [릴리스 정보](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Archetype | 0.7.0 | [릴리스 정보](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 새로운 기능 {#what-is-new-january}

* 고객이 상거래 프로젝트에서 XF를 만들 수 있도록 XF(경험 조각) 구성 요소가 추가되었습니다.

* 내 계정에서 사용할 수 있는 암호 기능을 변경합니다.

* AEM CIF 서버측 핵심 구성 요소에 대한 i18n 지원.

* 범용 관련 제품 구성 요소를 사용할 수 있습니다.

### 개선 사항 {#what-is-improved-january}

* 제품 티저에 CTA 버튼을 표시하도록 지원합니다.

* 추천 카테고리 목록 구성 요소에서 이미지를 변경/선택하는 옵션입니다.

* 제품 목록 구성 요소에서 제목/배너를 숨기거나 표시하는 옵션.

* 제품 슬라이드 구성 요소에 적용된 끌어서 놓기 기능입니다.

* 여러 버그 수정이 적용되었습니다.
