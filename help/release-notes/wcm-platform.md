---
title: AEM Foundation 및 리포지토리
description: Adobe Experience Manager 플랫폼 및 저장소에 대한 릴리스 노트입니다.
translation-type: tm+mt
source-git-commit: 8d60e064ab50f24016c049c8d5d0fceb784c99a3
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 54%

---


# AEM Foundation 및 리포지토리 {#aem-foundation-repository}

## 변경 사항 목록 {#list-of-changes}

### 저장소 {#repository}

* Adobe Experience Manager 6.5의 Foundation은 OSGi 기반 프레임워크(Apache Sling 및 Apache Felix)의 업데이트된 버전과 Java 컨텐츠 리포지토리인 Apache Jackrabbit Oak 1.10.2에 구축됩니다.
* 수정된 문제에 대한 개요는 [Apache Jackrabbit Oak Jira v. 1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt), [Apache Jackrabbit Oak Jira v. 1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt) 및 [Apache Jackrabbit Oak Jira v. 1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt)를 참조하십시오.

>[!CAUTION]
>
>AEM 6.3에는 리포지토리 마이그레이션이 필요하므로 Oak Segment Tar의 새 버전이 표시됩니다. 이전 버전의 TarMK에서 업그레이드하거나 다른 유형의 지속성에서 새 Segment Tar를 전환하려는 경우에는 이 단계가 필수입니다. 새 세그먼트 타르의 이점에 대한 자세한 내용은 [Oak 세그먼트 Tar로 마이그레이션 FAQ](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar)을 참조하십시오.

### Java 지원 {#java-support}

* Java 8에 대한 기존 지원과 함께 Java 11을 새롭게 지원.
* 최적의 성능을 위해 기본 GC 값을 다른 값으로 대체합니다. 자세한 내용은 [설치 및 업데이트](/help/sites-deploying/custom-standalone-install.md) 섹션을 참조하십시오.
* Java 11 및 Java 8 유지 관리 업데이트는 Adobe에서 공개적으로 사용할 수 없는 경우 AEM 관련 프로젝트에서 고객이 사용하도록 Oracle에 의해 배포됩니다.

### OSGI {#osgi}

* OSGi Promises 및 Converter 유틸리티 라이브러리가 추가됨.

### 프로젝트 및 워크플로우 {#projects-and-workflows}

* 복사 및 게시, 워크플로우 단계의 변수 지원 및 향상된 `OR` 및 `AND` 분할과 같은 추가 작업을 포함하도록 6.4에 도입된 새로운 워크플로우 모델 편집기가 개선되었습니다.

### 검색 {#searching}

* Oak에서의 검색이 이제 동적 패싯을 지원합니다. 예를 들어 자산 검색의 필터 레일은 예상 결과 양을 보여줍니다.
* 동적 패싯이 있는 결과를 제공하도록 QueryBuilder가 확장되었습니다.

### 보안 {#security}

* 관리자 사용자의 암호 만료가 추가되었습니다.

### 사용자 인터페이스 {#user-interface}

UI의 생산성과 사용 편의성을 향상시키기 위해 UI에 다양한 개선 사항이 적용되었습니다.

* AEM 6.5에서는 CRXDE로 이동할 필요 없이 전체 권한 및 제한 사항을 간편하고 확인하고 구성할 수 있는 [사용자 및 그룹]에 대한 새로운 [권한 관리 UI]를 도입합니다.
* 이제 열 보기는 화면에 표시되는 항목만 로드하고 사용자가 스크롤을 시작할 때만 추가로 로드됩니다. 목록 보기 및 카드 보기는 6.0 이후부터 이미 해당 기능이 적용되었습니다(6.4에서 강화됨)..
* 이제 열 보기에는 해당하는 경우 페이지/자산에 대한 워크플로우 상태가 포함됩니다.
* 모두 선택 작업은 동일한 폴더에 있는 모든 페이지/자산을 사용하여 작업을 실행하는 빠른 방법입니다.
* 모두 선택 조치는 로드된 페이지/자산이 아니라 모든 페이지/자산에 대해 조치를 시도합니다. 일괄 작업을 처리하도록 작업이 업그레이드되지 않으면 경고가 표시됩니다.

>[!CAUTION]
>
>Adobe은 클래식 UI를 더 이상 개선하지 않습니다. Experience Manager 6.5에는 이전 버전과의 호환성을 위한 클래식 UI가 포함되어 있습니다. 클래식 UI는 [더 보기](/help/sites-deploying/ui-recommendations.md)에서 더 이상 사용하지 않는 동안 완전히 지원되는 상태로 유지됩니다.

### 업그레이드 {#upgrade}

* 업그레이드 절차는 대부분 6.5에서 동일하게 유지됩니다.
* 6.4에는 이전 버전과의 호환성 , 업그레이드 복잡성 평가 및 지속 가능 업그레이드 기능이 지속적으로 도입되었습니다. 필요한 경우 이러한 영역에 대해 버전별 업데이트가 진행되었습니다.
* Pattern Detector 패키지가 단순화되었으며 사용 가능한 소스 버전에 대한 6.5로의 업그레이드를 평가하는 패키지가 한 가지 있습니다.
* 업그레이드 절차에 대한 자세한 내용은 [업그레이드 설명서](/help/sites-deploying/upgrade.md)를 참조하십시오.

### 웹 서버 {#web-server}

* Quickstart 배포에서는 Eclipse Jetty 9.4.15을 servlet 엔진(AEM 6.49.3.22 포함)으로 사용합니다.
