---
title: AEM Foundation 및 저장소
description: Adobe Experience Manager 플랫폼 및 저장소의 릴리스 노트입니다.
exl-id: 06938419-392b-432d-ba0c-ba444b3e141c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 54%

---

# AEM Foundation 및 저장소 {#aem-foundation-repository}

## 변경 사항 목록 {#list-of-changes}

### 저장소 {#repository}

* Adobe Experience Manager 6.5의 Foundation은 OSGi 기반 프레임워크(Apache Sling 및 Apache Felix)의 업데이트된 버전과 Java 컨텐츠 리포지토리인 Apache Jackrabbit Oak 1.10.2에 구축됩니다.
* 해결된 문제에 대한 개요는 [Apache Jackrabbit Oak Jira v. 1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt), [Apache Jackrabbit Oak Jira v. 1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt) 및 [Apache Jackrabbit Oak Jira v. 1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt)를 참조하십시오.

>[!CAUTION]
>
>AEM 6.3에는 리포지토리 마이그레이션이 필요하므로 Oak Segment Tar의 새 버전이 표시됩니다. 이전 버전의 TarMK에서 업그레이드하거나 다른 유형의 지속성에서 새 Segment Tar를 전환하려는 경우에는 이 단계가 필수입니다. 새 Segment Tar의 이점에 대한 자세한 내용은 [Oak Segment Tar 마이그레이션 FAQ](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar) 를 참조하십시오.

### Java 지원 {#java-support}

* Java 8에 대한 기존 지원과 함께 Java 11을 새롭게 지원.
* 최적의 성능을 위해 기본 GC 값을 다른 값으로 대체합니다. 자세한 내용은 [설치 및 업데이트](/help/sites-deploying/custom-standalone-install.md) 섹션을 참조하십시오.
* Java 11 및 Java 8 유지 관리 업데이트는 Oracle에서 공개적으로 사용할 수 없는 경우 AEM 관련 프로젝트에서 고객 사용을 위해 Adobe에 의해 배포됩니다.

### OSGI {#osgi}

* OSGi Promises 및 Converter 유틸리티 라이브러리가 추가됨.

### 프로젝트 및 워크플로우 {#projects-and-workflows}

* 6.4에 도입된 새로운 워크플로우 모델 편집기는 워크플로우 단계에서 복사 및 게시, 변수 지원과 같은 추가 작업을 포함하고 `OR` 및 `AND` 분할이 개선되었습니다.

### 검색 {#searching}

* Oak에서의 검색이 이제 동적 패싯을 지원합니다. 예를 들어 자산 검색의 필터 레일은 예상되는 결과 양을 보여줍니다.
* 동적 패싯과 함께 결과를 제공하기 위해 QueryBuilder 확장되었습니다.

### 보안 {#security}

* 관리자 사용자의 암호 만료가 추가되었습니다.

### 사용자 인터페이스 {#user-interface}

UI의 생산성과 사용 편의성을 향상시키기 위해 UI에 다양한 개선 사항이 적용되었습니다.

* AEM 6.5에서는 CRXDE로 이동할 필요 없이 전체 권한 및 제한 사항을 간편하고 확인하고 구성할 수 있는 [사용자 및 그룹]에 대한 새로운 [권한 관리 UI]를 도입합니다.
* 이제 열 보기는 화면에 표시되는 항목만 로드하고 사용자가 스크롤을 시작할 때만 추가로 로드됩니다. 목록 보기 및 카드 보기는 6.0 이후부터 이미 해당 기능이 적용되었습니다(6.4에서 강화됨)..
* 이제 열 보기에는 해당하는 경우 페이지/자산에 대한 워크플로우 상태가 포함됩니다.
* 모두 선택 작업은 동일한 폴더에 있는 모든 페이지/자산에서 작업을 실행하는 빠른 방법입니다.
* 모두 선택 조치는 로드된 페이지/자산이 아니라 모든 페이지/자산에 대해 조치를 시도합니다. 대량 작업을 처리하도록 작업이 업그레이드되지 않으면 경고가 표시됩니다.

>[!CAUTION]
>
>Adobe은 클래식 UI를 추가로 개선하지 않습니다. Experience Manager 6.5에는 이전 버전과의 호환성을 위한 클래식 UI가 포함되어 있습니다. 클래식 UI는 [더 이상 사용되지 않는 동안에도 계속 지원됩니다.](/help/sites-deploying/ui-recommendations.md)

### 업그레이드 {#upgrade}

* 업그레이드 절차는 대부분 6.5에서 동일하게 유지됩니다.
* 6.4에는 이전 버전과의 호환성 , 업그레이드 복잡성 평가 및 지속 가능 업그레이드 기능이 지속적으로 도입되었습니다. 필요한 경우 이러한 영역에 대해 버전별 업데이트가 진행되었습니다.
* Pattern Detector 패키지가 단순화되었으며 사용 가능한 소스 버전에 대한 6.5로의 업그레이드를 평가하는 패키지가 한 가지 있습니다.
* 업그레이드 절차에 대한 자세한 내용은 [업그레이드 설명서](/help/sites-deploying/upgrade.md)를 참조하십시오.

### 웹 서버 {#web-server}

* 빠른 시작 배포는 Eclipse Jetty 9.4.15를 서블릿 엔진(9.3.22와 함께 제공된 AEM 6.4)으로 사용합니다.
