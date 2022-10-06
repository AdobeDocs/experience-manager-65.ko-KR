---
title: 업그레이드 프로시저
seo-title: Upgrade Procedure
description: AEM을 업그레이드하기 위해 수행해야 하는 절차에 대해 알아봅니다.
seo-description: Learn about the procedure you need to follow in order to upgrade AEM.
uuid: 81126a70-c082-4f01-a1ad-7152182da88b
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: 5c035d4c-6e03-48b6-8404-800b52d659b8
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
exl-id: 5242600c-2281-46f9-a347-d985b4e319b3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 0%

---

# 업그레이드 프로시저 {#upgrade-procedure}

>[!NOTE]
>
>대부분의 AEM 업그레이드가 제자리에서 수행되므로 업그레이드는 작성 계층에 대한 다운타임이 필요합니다. 이러한 Best Practice를 통해 게시 계층 다운타임을 최소화하거나 제거할 수 있습니다.

AEM 환경을 업그레이드할 때 작성자와 최종 사용자 모두의 다운타임을 최소화하기 위해 작성자 환경을 업그레이드하거나 게시 환경을 업그레이드하는 방법 간의 차이점을 고려해야 합니다. 이 페이지에서는 AEM 6.x 버전에서 현재 실행 중인 AEM 토폴로지를 업그레이드하는 높은 수준의 절차에 대해 설명합니다. Mongo 및 TarMK 기반 배포는 물론 작성 계층과 게시 계층 간에 프로세스가 다르므로, 각 계층 및 마이크로커널이 별도의 섹션에 나열됩니다. 배포를 실행할 때는 먼저 작성 환경을 업그레이드하고 성공을 확인한 다음 게시 환경으로 이동하는 것이 좋습니다.

<!--
>[!IMPORTANT]
>
>The downtime during the upgrade can be significally reduced by indexing the repository before performing the upgrade. For more information, see [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)
-->

## TarMK 작성자 계층 {#tarmk-author-tier}

### 토폴로지 시작 {#starting-topology}

이 섹션에 대해 가정된 토폴로지는 콜드 대기 상태인 TarMK에서 실행 중인 작성자 서버로 구성됩니다. 작성자 서버에서 TarMK 게시 팜으로 복제가 발생합니다. 여기서는 다루지 않지만, 이 접근 방식은 오프로드를 사용하는 배포에 활용할 수도 있습니다. 작성자 인스턴스에서 복제 에이전트를 비활성화한 후 다시 활성화하기 전에 새 버전에서 오프로딩 인스턴스를 업그레이드하거나 다시 빌드해야 합니다.

![tarmk_starting_topology](assets/tarmk_starting_topology.jpg)

### 업그레이드 준비 {#upgrade-preparation}

![upgrade-preparation-author](assets/upgrade-preparation-author.png)

1. 컨텐츠 작성 중지

1. 대기 인스턴스를 중지합니다.

1. 작성자에서 복제 에이전트 비활성화

1. 를 실행합니다. [유지 관리 작업 사전 업그레이드](/help/sites-deploying/pre-upgrade-maintenance-tasks.md).

### 업그레이드 실행 {#upgrade-execution}

![execute_upgrade](assets/execute_upgrade.jpg)

1. 를 실행합니다. [즉석 업그레이드](/help/sites-deploying/in-place-upgrade.md)
1. 디스패처 모듈 업데이트 *필요한 경우*

1. QA가 업그레이드를 확인합니다

1. 작성자 인스턴스를 종료합니다.

### 성공한 경우 {#if-successful}

![if_successful](assets/if_successful.jpg)

1. 업그레이드된 인스턴스를 복사하여 새 Cold Standby 생성

1. 작성자 인스턴스 시작

1. 대기 인스턴스를 시작합니다.

### 실패한 경우(롤백) {#if-unsuccessful-rollback}

![롤백](assets/rollback.jpg)

1. 콜드 대기 인스턴스를 새 기본 인스턴스로 시작

1. 콜드 대기에서 작성 환경을 다시 빌드합니다.

## MongoMK 작성자 클러스터 {#mongomk-author-cluster}

### 토폴로지 시작 {#starting-topology-1}

이 섹션에 대해 가정된 토폴로지는 두 개 이상의 MongoMK 데이터베이스가 지원하는 두 개 이상의 AEM 작성자 인스턴스가 있는 MongoMK 작성자 클러스터로 구성됩니다. 모든 작성자 인스턴스는 데이터 저장소를 공유합니다. 이러한 단계는 S3 및 파일 데이터 저장소 모두에 적용됩니다. 작성자 서버에서 TarMK 게시 팜으로 복제가 발생합니다.

![mongo 토폴로지](assets/mongo-topology.jpg)

### 업그레이드 준비 {#upgrade-preparation-1}

![mongo-upgrade_prep](assets/mongo-upgrade_prep.jpg)

1. 컨텐츠 작성 중지
1. 백업할 데이터 저장소 복제
1. AEM 작성자 인스턴스인 기본 작성자를 제외한 모든 중지
1. 복제본 세트에서 MongoDB 노드를 제외한 모든 노드를 제거합니다. 기본 Mongo 인스턴스입니다
1. 업데이트 `DocumentNodeStoreService.cfg` 단일 멤버 복제본 세트를 반영하도록 주 작성자의 파일
1. 기본 작성자를 다시 시작하여 제대로 다시 시작되는지 확인합니다
1. 기본 작성자에서 복제 에이전트 비활성화
1. 실행 [유지 관리 작업 사전 업그레이드](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) 기본 작성자 인스턴스에서
1. 필요한 경우 기본 Mongo 인스턴스의 MongoDB를 WiredTiger를 사용하여 버전 3.2로 업그레이드하십시오

### 업그레이드 실행 {#Upgrade-execution-1}

![mongo 실행](assets/mongo-execution.jpg)

1. 실행 [즉석 업그레이드](/help/sites-deploying/in-place-upgrade.md) 기본 작성자
1. 디스패처 또는 웹 모듈 업데이트 *필요한 경우*
1. QA가 업그레이드를 확인합니다

### 성공한 경우 {#if-successful-1}

![mongo 보조](assets/mongo-secondaries.jpg)

1. 업그레이드된 Mongo 인스턴스에 연결된 새 6.5 작성자 인스턴스를 만듭니다.

1. 클러스터에서 제거된 MongoDB 노드를 다시 빌드합니다.

1. 업데이트 `DocumentNodeStoreService.cfg` 전체 복제본 세트를 반영하기 위한 파일

1. 작성자 인스턴스를 한 번에 하나씩 다시 시작합니다

1. 복제된 데이터 저장소를 제거합니다.

### 실패한 경우(롤백)  {#if-unsuccessful-rollback-2}

![mongo-rollback](assets/mongo-rollback.jpg)

1. 복제된 데이터 저장소에 연결하기 위해 보조 작성자 인스턴스 다시 구성

1. 업그레이드된 작성자 기본 인스턴스를 종료합니다.

1. 업그레이드된 Mongo 기본 인스턴스를 종료합니다.

1. 보조 Mongo 인스턴스를 첫 번째 인스턴스로 시작

1. 구성 `DocumentNodeStoreService.cfg` 아직 업그레이드되지 않은 Mongo 인스턴스의 복제 세트를 가리키도록 보조 작성자 인스턴스의 파일

1. 보조 작성자 인스턴스 시작

1. 업그레이드된 작성자 인스턴스, Mongo 노드 및 데이터 저장소를 정리합니다.

## TarMK 게시 팜 {#tarmk-publish-farm}

### TarMK 게시 팜 {#tarmk-publish-farm-1}

이 섹션에 대해 가정된 토폴로지는 로드 밸런서에서 차례대로 앞에 있는 Dispatcher에 의해 앞에 있는 두 개의 TarMK 게시 인스턴스로 구성됩니다. 작성자 서버에서 TarMK 게시 팜으로 복제가 발생합니다.

![tarmk-pub-farmv5](assets/tarmk-pub-farmv5.png)

### 업그레이드 실행 {#upgrade-execution-2}

![upgrade-publish2](assets/upgrade-publish2.png)

1. 로드 밸런서에서 게시 2 인스턴스에 대한 트래픽 중지
1. 실행 [업그레이드 전 유지 관리](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) 게시 2
1. 실행 [즉석 업그레이드](/help/sites-deploying/in-place-upgrade.md) 게시 2
1. 디스패처 또는 웹 모듈 업데이트 *필요한 경우*
1. Dispatcher 캐시 초기화
1. QA는 방화벽 뒤에 있는 Dispatcher를 통해 게시 2의 유효성을 검사합니다
1. 게시 종료 2
1. 게시 2 인스턴스 복사
1. 게시 2 시작

### 성공한 경우 {#if-successful-2}

![upgrade-publish1](assets/upgrade-publish1.png)

1. 2에 게시할 트래픽 활성화
1. 게시 1에 대한 트래픽 중지
1. 게시 1 인스턴스 중지
1. Publish 1 인스턴스를 Publish 2 사본으로 바꾸기
1. 디스패처 또는 웹 모듈 업데이트 *필요한 경우*
1. 게시 1에 대한 Dispatcher 캐시 초기화
1. 게시 1 시작
1. QA는 방화벽 뒤에 있는 Dispatcher를 통해 게시 1의 유효성을 검사합니다

### 실패한 경우(롤백) {#if-unsuccessful-rollback-1}

![pub_rollback](assets/pub_rollback.jpg)

1. 게시 1 사본 만들기
1. Publish 2 인스턴스를 Publish 1 복사본으로 바꿉니다
1. 게시 2에 대한 Dispatcher 캐시 초기화
1. 게시 2 시작
1. QA는 방화벽 뒤에 있는 Dispatcher를 통해 게시 2의 유효성을 검사합니다
1. 2에 게시할 트래픽 활성화

## 최종 업그레이드 단계 {#final-upgrade-steps}

1. 게시할 트래픽 활성화 1
1. QA는 공개 URL에서 최종 유효성 검사를 수행합니다
1. 작성 환경에서 복제 에이전트 활성화
1. 컨텐츠 작성 다시 시작
1. 수행 [업그레이드 후 확인](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md).

![최종](assets/final.jpg)
