---
title: 업그레이드 절차
seo-title: 업그레이드 절차
description: AEM을 업그레이드하기 위해 따라야 하는 절차에 대해 알아봅니다.
seo-description: AEM을 업그레이드하기 위해 따라야 하는 절차에 대해 알아봅니다.
uuid: 81126a70-c082-4f01-a1ad-7152182da88b
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: 5c035d4c-6e03-48b6-8404-800b52d659b8
docset: aem65
targetaudience: target-audience upgrader
translation-type: tm+mt
source-git-commit: d3a69bbbc9c3707538be74fd05f94f20a688d860
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 0%

---


# 업그레이드 절차 {#upgrade-procedure}

>[!NOTE]
>
>대부분의 AEM 업그레이드가 적소에 수행되므로 업그레이드 시 작성자 계층의 가동 중지 시간이 필요합니다. 이러한 모범 사례를 통해 게시 계층 다운타임을 최소화하거나 제거할 수 있습니다.

AEM 환경을 업그레이드할 때 작성자와 최종 사용자 모두의 다운타임을 최소화하기 위해 작성자 환경 또는 게시 환경 간의 접근 방식의 차이점을 고려해야 합니다. 이 페이지에서는 현재 AEM 6.x 버전에서 실행 중인 AEM 토폴로지를 업그레이드하는 높은 수준의 절차에 대해 설명합니다. 작성 및 게시 계층과 Mongo 및 TarMK 기반 배포 간에 프로세스가 다르므로 각 계층과 마이크로커널이 별도의 섹션에 나열되어 있습니다. 배포를 실행할 때 먼저 작성 환경을 업그레이드하고 성공을 확인한 다음 게시 환경으로 진행하는 것이 좋습니다.

>[!IMPORTANT]
>
>업그레이드를 수행하기 전에 저장소를 인덱싱하여 업그레이드 중 다운타임을 크게 줄일 수 있습니다. 자세한 내용은 오프라인 [재색인 사용을 통해 업그레이드 중 다운타임을 줄이기를 참조하십시오.](/help/sites-deploying/upgrade-offline-reindexing.md)

## TarMK Author Tier {#tarmk-author-tier}

### 토폴로지 시작 {#starting-topology}

이 섹션에 대해 가정된 토폴로지는 Cold Standby를 사용하여 TarMK에서 실행되는 작성자 서버로 구성됩니다. 복제는 작성자 서버에서 TarMK 게시 팜으로 수행됩니다. 여기에 설명된 것은 아니지만 오프로드를 사용하는 배포에 이 접근 방법을 활용할 수도 있습니다. 작성 인스턴스에서 복제 에이전트를 비활성화한 후 다시 활성화하기 전에 새 버전에서 오프로드 인스턴스를 업그레이드하거나 다시 빌드해야 합니다.

![tarmk_starting_topology](assets/tarmk_starting_topology.jpg)

### 업그레이드 준비 {#upgrade-preparation}

![upgrade-preparation-author](assets/upgrade-preparation-author.png)

1. 콘텐츠 제작 중지

1. 대기 인스턴스 중지

1. 작성자의 복제 에이전트 비활성화

1. 업그레이드 [전 유지 관리 작업을 실행합니다](/help/sites-deploying/pre-upgrade-maintenance-tasks.md).

### 업그레이드 실행 {#upgrade-execution}

![execute_upgrade](assets/execute_upgrade.jpg)

1. 업그레이드 [실행](/help/sites-deploying/in-place-upgrade.md)
1. 필요한 *경우 디스패처 모듈 업데이트*

1. QA에서 업그레이드 확인

1. 작성자 인스턴스를 종료합니다.

### 성공한 경우 {#if-successful}

![if_successful](assets/if_successful.jpg)

1. 업그레이드된 인스턴스를 복사하여 새 Cold Standby 생성

1. 작성자 인스턴스 시작

1. 대기 인스턴스를 시작합니다.

### 실패할 경우(롤백) {#if-unsuccessful-rollback}

![롤백](assets/rollback.jpg)

1. Cold Standby 인스턴스를 새 기본 인스턴스로 시작

1. Cold Standby에서 작성 환경을 다시 작성합니다.

## MongoMK 작성자 클러스터 {#mongomk-author-cluster}

### 토폴로지 시작 {#starting-topology-1}

이 섹션에 대해 가정된 토폴로지는 두 개 이상의 MongoMK 데이터베이스가 지원하는 두 개 이상의 AEM 작성자 인스턴스가 있는 MongoMK 작성자 클러스터로 구성됩니다. 모든 작성자 인스턴스는 데이터 저장소를 공유합니다. 이러한 단계는 S3 및 파일 데이터 저장소 모두에 적용됩니다. 복제는 작성자 서버에서 TarMK 게시 팜으로 수행됩니다.

![mongo-topology](assets/mongo-topology.jpg)

### 업그레이드 준비 {#upgrade-preparation-1}

![mongo-upgrade_prep](assets/mongo-upgrade_prep.jpg)

1. 콘텐츠 제작 중지
1. 백업을 위해 데이터 저장소 복제
1. 하나의 AEM 작성자 인스턴스만 제외하고 모든 AEM 작성자 중지
1. 복제본 세트, 기본 Mongo 인스턴스에서 MongoDB 노드를 하나만 제외하고 모두 제거
1. 단일 멤버 복제본 세트를 반영하도록 주 작성자의 `DocumentNodeStoreService.cfg` 파일을 업데이트합니다.
1. 기본 작성자가 올바르게 다시 시작되도록 다시 시작합니다.
1. 기본 작성자의 복제 에이전트 비활성화
1. 기본 작성자 인스턴스에서 [업그레이드 전 유지 관리 작업](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) 실행
1. 필요한 경우 기본 Mongo 인스턴스의 MongoDB를 WiredTiger와 함께 버전 3.2로 업그레이드하십시오

### 업그레이드 실행 {#Upgrade-execution-1}

![mongo-execution](assets/mongo-execution.jpg)

1. 기본 작성자 [에서 업그레이드](/help/sites-deploying/in-place-upgrade.md) 실행
1. 필요한 *경우 Dispatcher 또는 웹 모듈 업데이트*
1. QA에서 업그레이드 확인

### 성공한 경우 {#if-successful-1}

![mongo 보조](assets/mongo-secondaries.jpg)

1. 업그레이드된 Mongo 인스턴스에 연결된 새로운 6.5 작성자 인스턴스 만들기

1. 클러스터에서 제거된 MongoDB 노드를 다시 빌드합니다.

1. 전체 복제본 세트를 반영하도록 `DocumentNodeStoreService.cfg` 파일 업데이트

1. 작성자 인스턴스를 한 번에 하나씩 다시 시작합니다.

1. 복제된 데이터 저장소를 제거합니다.

### 실패할 경우(롤백)  {#if-unsuccessful-rollback-2}

![mongo-rollback](assets/mongo-rollback.jpg)

1. 복제된 데이터 저장소에 연결할 보조 작성자 인스턴스 다시 구성

1. 업그레이드된 작성자 기본 인스턴스를 종료합니다.

1. 업그레이드된 Mongo 기본 인스턴스를 종료합니다.

1. 보조 Mongo 인스턴스를 새 기본 인스턴스로 시작

1. 아직 업그레이드되지 않은 Mongo 인스턴스의 복제본 세트를 가리키도록 보조 작성자 인스턴스의 `DocumentNodeStoreService.cfg` 파일을 구성합니다.

1. 보조 작성자 인스턴스 시작

1. 업그레이드된 작성자 인스턴스, Mongo 노드 및 데이터 저장소를 정리합니다.

## TarMK Publish Farm {#tarmk-publish-farm}

### TarMK Publish Farm {#tarmk-publish-farm-1}

이 섹션에 대해 가정된 토폴로지는 로드 밸런서에 의해 다시 시작되는 Dispatcher에 의해 앞에 있는 두 개의 TarMK 게시 인스턴스로 구성됩니다. 복제는 작성자 서버에서 TarMK 게시 팜으로 수행됩니다.

![tarmk-pub-farmv5](assets/tarmk-pub-farmv5.png)

### 업그레이드 실행 {#upgrade-execution-2}

![upgrade-publish2](assets/upgrade-publish2.png)

1. 로드 밸런서에서 게시 2 인스턴스에 대한 트래픽 중지
1. 게시 2에서 [업그레이드 전 유지](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) 관리 실행
1. 게시 2 [에서 업그레이드](/help/sites-deploying/in-place-upgrade.md) 실행
1. 필요한 *경우 Dispatcher 또는 웹 모듈 업데이트*
1. Dispatcher 캐시 플러시
1. QA는 Dispatcher를 통해 방화벽 뒤에서 게시 2를 검증합니다.
1. 종료 게시 2
1. 게시 2 인스턴스 복사
1. 게시 시작 2

### 성공한 경우 {#if-successful-2}

![upgrade-publish1](assets/upgrade-publish1.png)

1. 게시할 트래픽 활성화 2
1. 게시 1에 대한 트래픽 중지
1. 게시 1 인스턴스 중지
1. 게시 1 인스턴스를 게시 2 복사본으로 바꾸기
1. 필요한 *경우 Dispatcher 또는 웹 모듈 업데이트*
1. 게시 1에 대한 발송자 캐시 플러시
1. 게시 1 시작
1. QA는 Dispatcher를 통해 방화벽 뒤에서 게시 1을 검증합니다.

### 실패할 경우(롤백) {#if-unsuccessful-rollback-1}

![pub_rollback](assets/pub_rollback.jpg)

1. 게시 1 사본 만들기
1. Publish 2 인스턴스를 Publish 1 복사본으로 바꾸기
1. 게시 2에 대한 발송자 캐시 플러시
1. 게시 시작 2
1. QA는 Dispatcher를 통해 방화벽 뒤에서 게시 2를 검증합니다.
1. 게시할 트래픽 활성화 2

## 최종 업그레이드 단계 {#final-upgrade-steps}

1. 게시할 트래픽 활성화 1
1. QA는 공개 URL에서 최종 유효성 검사를 수행합니다.
1. 작성 환경에서 복제 에이전트 사용
1. 컨텐츠 작성 다시 시작
1. 업그레이드 [후 확인을 수행합니다](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md).

![final](assets/final.jpg)

