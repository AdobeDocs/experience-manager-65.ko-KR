---
title: AEM Content and Commerce 릴리스 노트 2022
description: AEM Content and Commerce 릴리스 노트 2022
exl-id: ec47c5f8-d4dd-469f-94df-5ee28f25d696
source-git-commit: 26df21270e8c586ba21b9bf3e9fc5003facbaade
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 13%

---

# Commerce Integration Framework GitHub 릴리스 개요

## 시스템 요구 사항 개요

현재 사용 중인 CIF 버전 또는 향후 사용할 예정인 최소 시스템 요구 사항을 아래 표에서 검토하십시오.

| 구성 요소 | 시스템 요구 사항 |
|:-------|:-----:|
| CIF 추가 기능 | 최소: AEM 6.5.7, Magento 2.3.5 GraphQL 스키마 |
| CIF 코어 구성 요소 | [시스템 요구 사항](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM Project Archetype | [시스템 요구 사항](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## 릴리스 날짜: 2022년 1월

| 구성 요소 | 버전 | 세부 사항 |
|:-------|:-----:|---------------------:|
| CIF 추가 기능 | 2022.01.20.00 | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.01.20.00.zip) |
| CIF 코어 구성 요소 | 2.5.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.5.0) |
| CIF Venia 참조 사이트 | 2022.01.27 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.01.27) |

### 새로운 기능 {#what-is-new-january}

* 향상된 myAccount 구성 요소
* 제품 권장 사항 구성 요소는 추가 페이지 유형(홈 페이지, 장바구니, 주문 확인)을 지원합니다
* **위시리스트**
   * 로그인한 방문자는 wishlist에 제품을 추가할 수 있습니다
   * myAccount를 통해 Wishlist와 그 제품의 관리 가능
   * &quot;wishlist에 추가&quot; 단추는 정책을 통해 구성 요소 수준에서 활성화/비활성화할 수 있습니다(예: 제품 티저, 제품 세부 사항)
   * 코어 구성 요소 및 AEM Venia Storefront에서 사용할 수 있습니다.

![위시리스트](/help/assets/CIF/wishlist.png)

