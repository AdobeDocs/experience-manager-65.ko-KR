---
title: AEM Content and Commerce 릴리스 노트 2022
description: AEM Content and Commerce 릴리스 노트 2022
exl-id: d0a66e70-c4f1-4051-8161-11f07dad0612
source-git-commit: 1a82930d9f0aa84cea590782aba2e70ec23b41c3
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 27%

---

# Commerce Integration Framework GitHub 릴리스 개요

## 시스템 요구 사항 개요

현재 사용 중인 CIF 버전 또는 향후 사용할 예정인 최소 시스템 요구 사항을 아래 표에서 검토하십시오.

| 구성 요소 | 시스템 요구 사항 |
|:-------|:-----:|
| CIF 추가 기능 | 최소: AEM 6.5.7, Magento 2.3.5 GraphQL 스키마 |
| CIF 코어 구성 요소 | [시스템 요구 사항](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM Project Archetype | [시스템 요구 사항](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## 릴리스 날짜: 2022년 3월

| 구성 요소 | 버전 | 세부 사항 |
|:-------|:-----:|---------------------:|
| CIF 추가 기능 | 2022.02.24.00 | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.02.24.00.zip) |
| CIF 코어 구성 요소 | 2.6.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) |
| CIF Venia 참조 사이트 | 2022.02.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.02.24) |

### 새로운 기능 {#what-is-new-march}

* 베타: AEM CIF Search 핵심 구성 요소 지원 Commerce LiveSearch
* 다중 저장소 시나리오에 대한 SEO가 개선되었습니다. 이제 CIF 클라우드 구성 속성을 통해 저장소 수준에서 PDP/PLP의 URL 형식을 구성할 수 있습니다
* 제품 선택기는 UI에서 새 필터 옵션을 통해 준비된 제품을 지원합니다.  이를 통해 컨텐츠 전문가가 향후 제품 출시에 대한 제품 컨텐츠 관리를 준비할 수 있습니다
* 구성 프록시 URL 대신 CIF 클라우드 구성 이름을 사용하여 CIF 구성 관리 및 오류 처리를 단순화했습니다
* 제품 목록 및 회전 메뉴 구성 요소에 대한 수동 카테고리 선택. 이를 통해 컨텐츠 전문가가 카탈로그 경험 외부의 컨텐츠 페이지에서 이러한 구성 요소를 사용할 수 있습니다

## 릴리스 날짜: 2022년 1월

| 구성 요소 | 버전 | 세부 사항 |
|:-------|:-----:|---------------------:|
| CIF 추가 기능 | 2022.01.20.00 | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.01.20.00.zip) |
| CIF 코어 구성 요소 | 2.5.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.5.0) |
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
