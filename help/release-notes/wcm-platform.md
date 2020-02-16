---
title: AEM Foundation 및 리포지토리
description: Adobe Experience Manager 6.3 AEM 플랫폼 및 리포지토리에 관한 릴리스 노트입니다.
uuid: 70626eda-c514-44bd-9f28-ff7abdc22f53
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: 66ecf4c5-6d0f-4586-880d-7d1c8a5a5614
docset: aem65
translation-type: tm+mt
source-git-commit: 4dc4a518c212555b7833ac27de02087a403d3517

---


# AEM Foundation 및 리포지토리{#aem-foundation-repository}

## 변경 사항 목록 {#list-of-changes}

### 보관소 {#repository}

* Adobe Experience Manager 6.5의 Foundation은 OSGi 기반 프레임워크(Apache Sling 및 Apache Felix)의 업데이트된 버전과 Java 컨텐츠 리포지토리인 Apache Jackrabbit Oak 1.10.2에 구축됩니다.
* Please see [Apache Jackrabbit Oak Jira v. 1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt), [Apache Jackrabbit Oak Jira v. 1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt) and [Apache Jackrabbit Oak Jira v. 1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt) for a full overview of fixed issues.

>[!CAUTION]
>
>* AEM 6.3에는 리포지토리 마이그레이션이 필요하므로 Oak Segment Tar의 새 버전이 표시됩니다. 이전 버전의 TarMK에서 업그레이드하거나 다른 유형의 지속성에서 새 세그먼트 Tar를 전환하려는 경우 이 단계는 필수입니다. For more information on what the benefits of the new Segment Tar are, see the [Migrating to Oak Segment Tar FAQ](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar).
>



### Java 지원 {#java-support}

* Java 8에 대한 기존 지원과 함께 Java 11을 새롭게 지원
* 최적의 성능을 위해 기본 GC 값을 다른 값으로 대체합니다. 자세한 내용은 [설치 및 업데이트](/help/sites-deploying/custom-standalone-install.md) 섹션을 참조하십시오.
* Oracle에서 공개적으로 사용할 수 없는 경우 Java 11 및 Java 8 유지 관리 업데이트는 AEM 관련 프로젝트에서 고객의 활용을 위해 Adobe에서 배포합니다.

### OSGI {#osgi}

* OSGi Promises 및 Converter 유틸리티 라이브러리가 추가됨

### 프로젝트 및 워크플로우 {#projects-and-workflows}

* 6.4에 도입된 새로운 워크플로우 모델 편집기는 워크플로우 단계에서 복사 및 게시, 변수 지원과 같은 다양한 작동과 개선된 OR 및 AND 분할이 포함되도록 개선되었습니다.

### 검색 {#searching}

* Oak에서의 검색이 이제 동적 패싯을 지원합니다. 예를 들어 자산 검색의 필터 레일은 예상 결과 양을 보여줍니다.
* 동적 패싯과 함께 결과를 제공하기 위해 QueryBuilder 확장되었습니다.

### 보안 {#security}

* 관리자 사용자의 암호 만료가 추가되었습니다.

### 사용자 인터페이스 {#user-interface}

UI의 생산성과 사용 편의성을 향상시키기 위해 UI에 다양한 개선 사항이 적용되었습니다.

* AEM 6.5에서는 CRXDE로 이동할 필요 없이 전체 권한 및 제한 사항을 간편하고 확인하고 구성할 수 있는 [사용자 및 그룹]에 대한 새로운 [권한 관리 UI]를 도입합니다.
* 이제 열 보기는 화면에 표시되는 항목만 로드하고 사용자가 스크롤을 시작할 때만 추가로 로드됩니다. 목록 보기 및 카드 보기는 6.0 이후부터 이미 해당 기능이 적용되었습니다(6.4에서 강화됨).
* 이제 열 보기에는 해당하는 경우 페이지/자산에 대한 워크플로우 상태가 포함됩니다.
* [모두 선택] 조치는 동일한 폴더에 있는 모든 페이지/자산에서 조치를 실행하는 빠른 방법입니다.
* [모두 선택] 조치는 로드된 페이지/자산이 아니라 모든 페이지/자산에 대해 조치를 시도합니다. 대량 작업을 처리하도록 조치가 업그레이드되지 않은 경우 경고 대화 상자가 표시됩니다.

>[!CAUTION]
>
>* Adobe는 향후 클래식 UI를 개선할 계획이 없습니다. AEM 6.5에는 클래식 UI가 포함되어 있으며 이전 릴리스에서 업그레이드하는 고객은 있는 그대로 사용할 수 있습니다. Note that Classic UI remains fully supported while being deprecated [Read more](/help/sites-deploying/ui-recommendations.md).
>



### 업그레이드 {#upgrade}

* 업그레이드 절차는 대부분 6.5에서 동일하게 유지됩니다.
* 6.4에는 이전 버전과의 호환성 , 업그레이드 복잡성 평가 및 지속 가능 업그레이드 기능이 지속적으로 도입되었습니다. 필요한 경우 이러한 영역에 대해 버전별 업데이트가 진행되었습니다.
* Pattern Detector 패키지가 단순화되었으며 사용 가능한 소스 버전에 대한 6.5로의 업그레이드를 평가하는 패키지가 한 가지 있습니다.
* Please see the [Upgrade documentation](/help/sites-deploying/upgrade.md) for more details on upgrade procedure.

### 웹 서버 {#web-server}

* Quickstart 배포는 Eclipse Jetty 9.4.15를 servlet 엔진(9.3.22와 함께 제공된 AEM 6.4)으로 사용합니다.

