---
title: AEM Content 및 Commerce 릴리스 노트 2024
description: Adobe Experience Manager Content 및 Commerce 릴리스 노트 2024.
exl-id: 372e6a46-72bb-4db4-ad01-534ca723ae58
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 1788e5f77d4c46a548710361e9e5dae3c6daab28
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 26%

---

# Commerce integration framework GitHub 릴리스 개요

## 시스템 요구 사항 개요

현재 사용 중이거나 향후 사용할 CIF 버전에 대한 아래 표의 최소 시스템 요구 사항을 검토하십시오.

| 구성 요소 | 시스템 요구 사항 |
|:-------|:-----------------------------------------------------------------------------------------------:|
| CIF 추가 기능 | 최소: AEM 6.5.18, Adobe Commerce 2.3.5 GraphQL 스키마 |
| CIF 핵심 구성 요소 | [시스템 요구 사항](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM Project Archetype | [시스템 요구 사항](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## 릴리스 날짜: 2024년 10월

| 구성 요소 | 버전 | 세부 사항 |
|:-------|:-------:|-----------------------------------------------------------------------------------------------------------:|
| CIF 핵심 구성 요소 | 2.15.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.15.0) |

### 버그 수정 {#bug-fixes-October}

* 핵심 CIF 구성 요소에서 UI 테스트가 제대로 작동하지 않는 문제가 해결되었습니다.
* 카테고리 URL 형식이 클라우드 인스턴스에서 예상대로 작동하지 않는 문제를 해결했습니다.

## 릴리스 날짜: 2024년 9월

| 구성 요소 | 버전 | 세부 사항 |
|:-------|:-------:|-----------------------------------------------------------------------------------------------------------:|
| CIF 핵심 구성 요소 | 2.14.2 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.14.2) |

### 개선 사항 {#improvements-September}

* 카테고리 제한을 사용자 정의할 수 있습니다.

### 버그 수정 {#bug-fixes-September}

* Commerce 필드가 자산 메타데이터 스키마 편집기와 제대로 통합되지 않았습니다.
* 드래그 앤 드롭을 위한 슬라이드 제품 다중 필드 관련 문제.
* 드래그 앤 드롭에 대한 회전 메뉴 범주 다중 필드 문제
* 카테고리 및 제품 편집기 페이지의 페이지 정보에 있는 메뉴에서 클릭 기능이 작동하지 않습니다.
* 주문 확인 페이지에 주문 번호가 표시되지 않습니다.

## 릴리스 날짜: 2024년 1월

| 구성 요소 | 버전 | 세부 사항 |
|:-------|:-------:|-----------------------------------------------------------------------------------------------------------:|
| CIF 핵심 구성 요소 | 2.12.6 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.12.6) |

### 버그 수정 {#bug-fixes-january}

* 제품 컬렉션 구성 요소에서 장바구니에 추가 버튼 및 위시리스트에 추가 버튼을 수정했습니다.
