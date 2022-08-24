---
title: AEM과 MongoDB
seo-title: AEM with MongoDB
description: MongoDB 배포를 통한 성공적인 AEM에 필요한 작업 및 고려 사항에 대해 알아봅니다.
seo-description: Learn about the tasks and considerations needed for a successful AEM with MongoDB deployment.
uuid: 8028832d-10de-4811-a769-fab699c162ec
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: cd3b979f-53d4-4274-b4eb-a9533329192a
docset: aem65
exl-id: 70a39462-8584-4c76-a097-05ee436247b7
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '6496'
ht-degree: 0%

---

# AEM과 MongoDB{#aem-with-mongodb}

이 문서는 MongoDB와 함께 Adobe Experience Manager을 배포하는 데 필요한 작업 및 고려 사항에 대한 지식을 개선하기 위한 것입니다.

배포 관련 자세한 내용은 [배포 및 유지 관리](/help/sites-deploying/deploy.md) 섹션에 자세히 설명되어 있습니다.

## AEM에서 MongoDB를 사용해야 하는 경우 {#when-to-use-mongodb-with-aem}

MongoDB는 일반적으로 다음 기준 중 하나가 충족되는 AEM 작성자 배포를 지원하는 데 사용됩니다.

* 하루에 1000명 이상의 고유 사용자
* 동시 사용자 100명 이상
* 많은 양의 페이지 편집
* 큰 롤아웃 또는 활동.

위의 기준은 작성자 인스턴스에만 해당되며, TarMK 기반의 모든 게시 인스턴스는 아닙니다. 작성자 인스턴스는 인증되지 않은 액세스를 허용하지 않으므로 인증된 사용자를 참조하는 사용자 수입니다.

기준이 충족되지 않으면 가용성을 해결하기 위해 TarMK 활성/대기 배포를 권장합니다. 일반적으로 MongoDB는 단일 하드웨어 항목으로 확장 요구 사항이 달성할 수 있는 것보다 많은 경우에 고려해야 합니다.

>[!NOTE]
>
>작성 인스턴스 크기 조정 및 동시 사용자 정의에 대한 추가 정보는 [하드웨어 크기 조정 지침](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel).

### AEM용 최소 MongoDB 배포 {#minimal-mongodb-deployment-for-aem}

다음은 MongoDB의 AEM에 대한 최소 배포입니다. 단순함을 위해 SSL 종료 및 HTTP 프록시 구성 요소가 일반화되었습니다. 이 ID는 하나의 MongoDB 복제본 세트로 구성되며, 운영 복제본과 2개의 보조 복제본이 있습니다.

![chlimage_1-4](assets/chlimage_1-4.png)

최소 배포에는 3이 필요합니다. `mongod` 복제본 세트로 구성된 인스턴스 한 인스턴스는 주 인스턴스로 선택되고 다른 인스턴스는 보조 인스턴스가 되고, 선택 항목은 `mongod`. 각 인스턴스에 연결된 로컬 디스크입니다. 클러스터를 통해 로드를 지원하려면 최소 12MB/s의 처리량을 3000개 이상의 IOPS(I/O Operations Per Second)가 권장됩니다.

AEM 작성자는 `mongod` 인스턴스, 각 AEM 작성자가 세 개 모두에 연결된 경우 `mongod` 인스턴스. 쓰기는 기본 인스턴스로 전송되고 읽기는 어느 인스턴스에서도 읽을 수 있습니다. 트래픽은 Dispatcher가 활성 AEM 작성자 인스턴스 중 하나에 대한 로드를 기반으로 배포됩니다. OAK 데이터 저장소는 `FileDataStore`및 MongoDB 모니터링은 배포의 위치에 따라 MMS 또는 MongoDB Ops Manager에서 제공합니다. 운영 체제 수준 및 로그 모니터링은 Splunk 또는 Ganglia와 같은 타사 솔루션에서 제공됩니다.

이 배포에서는 성공적인 구현을 위해 모든 구성 요소가 필요합니다. 구성 요소가 없으면 구현이 작동하지 않습니다.

### 운영 체제 {#operating-systems}

AEM 6에서 지원되는 운영 체제 목록을 보려면 [기술 요구 사항 페이지](/help/sites-deploying/technical-requirements.md).

### 환경 {#environments}

가상화 환경은 프로젝트를 실행하는 여러 기술 팀 간에 원활한 통신이 가능한 경우 지원됩니다. 여기에는 AEM을 실행 중인 팀, 운영 체제를 보유한 팀 및 가상화 인프라를 관리하는 팀이 포함됩니다.

가상화 환경을 관리하는 팀에서 관리해야 하는 MongoDB 인스턴스의 I/O 용량에 대해 구체적인 요구 사항이 있습니다. 프로젝트에서 Amazon Web Services과 같은 클라우드 배포를 사용하는 경우 MongoDB 인스턴스를 지원하려면 인스턴스에 충분한 I/O 용량과 일관성을 제공해야 합니다. 그렇지 않으면 MongoDB 프로세스 및 Oak 리포지토리가 불안정하고 잘못 수행됩니다.

가상화 환경에서는 MongoDB의 스토리지 엔진이 VMWare 리소스 할당 정책에 의해 장애되지 않도록 하기 위해 특정 I/O 및 VM 구성이 필요합니다. 성공적인 구현으로 다양한 팀 간에 장벽은 없으며 모든 팀이 필요한 성능을 제공하기 위해 등록됩니다.

## 하드웨어 고려 사항 {#hardware-considerations}

### 저장 용량 {#storage}

MongoDB는 일반적으로 SSD와 동등한 성능을 갖춘 SSD 스토리지 또는 스토리지를 필요로 하므로, 적절한 가로 크기 조절이 필요 없이 최상의 성능을 위해 읽기 및 쓰기 처리량을 달성할 수 있습니다.

### RAM {#ram}

MMAP 저장소 엔진을 사용하는 MongoDB 버전 2.6 및 3.0을 사용하려면 데이터베이스의 작업 세트와 해당 인덱스가 RAM에 맞아야 합니다.

RAM이 부족하면 성능이 크게 저하됩니다. 작업 세트와 데이터베이스의 크기는 응용 프로그램에 따라 크게 다릅니다. 몇 가지 추정이 가능하지만, 필요한 RAM의 양을 결정하는 가장 안정적인 방법은 AEM 애플리케이션을 빌드하고 로드하는 것입니다.

로드 테스트 프로세스를 지원하기 위해 전체 데이터베이스 크기에 대한 작업 집합의 다음 비율을 가정할 수 있습니다.

* SSD 스토리지용 1:10
* 하드 디스크 스토리지용 1:3

즉, SSD 배포의 경우 2TB 데이터베이스에 200GB의 RAM이 필요합니다.

MongoDB 3.0의 WiredTiger 저장 엔진에도 동일한 제한 사항이 적용되지만, WiredTiger가 MMAP 저장 엔진과 동일한 방식으로 메모리 매핑을 사용하지 않으므로 작업 세트, RAM 및 페이지 장애 간의 상관 관계는 그리 크지 않습니다.

>[!NOTE]
>
>Adobe은 MongoDB 3.0을 사용하는 AEM 6.1 배포에 WiredTiger 저장 엔진을 사용하는 것을 권장합니다.

### 데이터 저장소 {#data-store}

MongoDB 작업 세트 제한 사항으로 인해 데이터 저장소는 MongoDB와 독립적으로 유지하는 것이 좋습니다. 대부분의 환경에서 `FileDataStore` 모든 AEM 인스턴스에서 사용할 수 있는 NAS 를 사용해야 합니다. Amazon Web Services을 사용하는 경우 `S3 DataStore`. 어떤 이유로든 데이터 저장소가 MongoDB 내에서 유지된다면 데이터 저장소의 크기를 적절하게 조정된 총 데이터베이스 크기와 작업 집합 계산에 추가해야 합니다. 따라서 페이지 장애 없이 성능을 유지하기 위해 RAM을 훨씬 더 많이 프로비저닝할 수 있습니다.

## 모니터링 {#monitoring}

성공적인 프로젝트 구현을 위해서는 모니터링이 필수적이다. 충분한 지식을 가지고 모니터링 없이 MongoDB에서 AEM을 실행할 수 있지만, 이러한 지식은 일반적으로 배포의 각 부분에 대해 전문 엔지니어에서 발견됩니다.

일반적으로 Apache Oak Core에서 일하는 R&amp;D 엔지니어와 MongoDB 전문가가 여기에 포함됩니다.

모든 수준에서 모니터링하지 않으면 문제를 진단하려면 코드 베이스에 대한 자세한 정보가 필요합니다. 적절한 모니터링과 주요 통계에 대한 적절한 지침을 통해 구현 팀은 예외 항목에 적절하게 대응할 수 있습니다.

명령줄 도구를 사용하여 클러스터 작업의 빠른 스냅샷을 얻을 수 있지만 많은 호스트에서 실시간으로 이 작업을 수행하는 것은 거의 불가능합니다. 명령줄 도구는 몇 분 이상 내역 정보를 거의 제공하지 않으며 서로 다른 유형의 지표 간에 상호 상관 관계를 허용하지 않습니다. 짧은 배경 `mongod` 동기화는 I/O Wait와 상관 관계를 맺거나 연결된 가상 시스템의 공유 스토리지 자원에 과도한 쓰기 수준을 상호 연계하기 위해 상당한 수작업이 필요합니다.

### MongoDB Cloud Manager {#mongodb-cloud-manager}

MongoDB Cloud Manager는 MongoDB 인스턴스를 모니터링하고 관리할 수 있는 MongoDB에서 제공하는 무료 서비스입니다. MongoDB 클러스터의 성능 및 상태를 실시간으로 볼 수 있습니다. 인스턴스가 Cloud Manager 모니터링 서버에 도달할 수 있는 경우 클라우드 및 비공개 호스팅 인스턴스를 모두 관리합니다.

모니터링 서버에 연결하는 MongoDB 인스턴스에 에이전트가 설치되어 있어야 합니다. 에이전트 수준은 다음과 같습니다.

* MongoDB 서버의 모든 작업을 완벽하게 자동화할 수 있는 자동화 에이전트
* 모니터링 에이전트 `mongod` 인스턴스,
* 데이터의 예약된 백업을 수행할 수 있는 백업 에이전트입니다.

MongoDB 클러스터의 유지 관리 자동화를 위해 Cloud Manager를 사용하더라도 일상적인 작업 중 많은 작업을 쉽게 수행할 수 있으며, 필요하지 않으며, 둘 다 백업에 사용하고 있지 않습니다. 모니터링할 Cloud Manager를 선택할 때는 모니터링이 필요합니다.

MongoDB Cloud Manager에 대한 자세한 내용은 [MongoDB 설명서](https://docs.cloud.mongodb.com/).

### MongoDB Ops Manager {#mongodb-ops-manager}

MongoDB Ops Manager는 MongoDB Cloud Manager와 동일한 소프트웨어입니다. 등록되면 개인 데이터 센터 또는 다른 랩톱 또는 데스크탑 시스템에 로컬로 Ops Manager를 다운로드하여 설치할 수 있습니다. 로컬 MongoDB 데이터베이스를 사용하여 데이터를 저장하고 관리되는 서버와 Cloud Manager와 동일한 방식으로 통신합니다. 모니터링 에이전트를 금지하는 보안 정책이 있는 경우 MongoDB Ops Manager를 사용해야 합니다.

### 운영 체제 모니터링 {#operating-system-monitoring}

AEM MongoDB 클러스터를 실행하려면 운영 체제 수준 모니터링이 필요합니다.

Ganglia는 이러한 시스템의 좋은 예이며 CPU, 로드 평균 및 사용 가능한 디스크 공간과 같은 기본적인 상태 지표를 넘어서는 필요한 정보의 범위와 세부 정보를 보여줍니다. 문제를 진단하려면 엔트로피 풀 레벨, CPU I/O 대기, FIN_WAIT2 상태의 소켓을 사용해야 합니다.

### 로그 집계 {#log-aggregation}

여러 서버의 클러스터를 사용하는 경우 중앙 로그 집합은 운영 시스템의 요구 사항입니다. Splunk와 같은 소프트웨어는 로그 집계를 지원하고 팀이 로그를 수동으로 수집하지 않고도 애플리케이션의 동작 패턴을 분석할 수 있도록 합니다.

## 확인 목록 {#checklists}

이 섹션에서는 프로젝트를 구현하기 전에 AEM 및 MongoDB 배포가 제대로 설정되도록 하기 위해 수행해야 하는 다양한 단계를 다룹니다.

### 네트워크 {#network}

1. 먼저 모든 호스트에 DNS 항목이 있는지 확인합니다
1. 모든 호스트는 다른 라우팅 가능한 모든 호스트의 DNS 항목에 의해 확인할 수 있어야 합니다
1. 모든 MongoDB 호스트는 동일한 클러스터의 다른 모든 MongoDB 호스트에서 라우팅할 수 있습니다
1. MongoDB 호스트는 패킷을 MongoDB Cloud Manager 및 기타 모니터링 서버로 라우팅할 수 있습니다
1. AEM 서버는 모든 MongoDB 서버로 패킷을 라우팅할 수 있습니다
1. 모든 AEM 서버와 MongoDB 서버 사이의 패킷 지연은 2밀리초보다 작으며, 패킷 손실 및 1밀리초 이하의 표준 배포는 없습니다.
1. AEM과 MongoDB 서버 사이에 둘 이상의 홉이 있는지 확인합니다.
1. 두 MongoDB 서버 사이에 둘 이상의 홉이 없습니다
1. 코어 서버(MongoDB 또는 AEM 또는 모든 조합) 간에 OSI 레벨 3보다 높은 라우터가 없습니다.
1. VLAN 트렁킹 또는 네트워크 터널링을 사용하는 경우 패킷 지연 검사를 준수해야 합니다.

### AEM 구성 {#aem-configuration}

#### 노드 저장소 구성 {#node-store-configuration}

AEM 인스턴스는 MongoMK와 함께 AEM을 사용하도록 구성해야 합니다. AEM의 MongoMK 구현의 기반이 문서 노드 저장소입니다.

노드 저장소를 구성하는 방법에 대한 자세한 내용은 [AEM에서 노드 저장소 및 데이터 저장소 구성](/help/sites-deploying/data-store-config.md).

다음은 최소 MongoDB 배포를 위한 문서 노드 저장소 구성의 예입니다.

```xml
# org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config
#MongoDB server details
mongodburi=mongodb://aem:aempassword@mongodbserver1.customer.com:27000,mongodbserver2.customer.com:27000

#Name of MongoDB database to use
db=aem

#Store binaries in custom BlobStore e.g. FileDataStore
customBlobStore=true

cache=2048
blobCacheSize=1024
```

위치:

* `mongodburi`
AEM에서 연결해야 하는 MongoDB 서버 입니다. 기본 복제본 세트의 알려진 모든 구성원에 대한 연결이 이루어집니다. MongoDB Cloud Manager를 사용하는 경우 서버 보안이 활성화됩니다. 따라서 연결 문자열에는 적절한 사용자 이름과 암호가 포함되어야 합니다. MongoDB의 비엔터프라이즈 버전은 사용자 이름과 암호 인증만 지원합니다. 연결 문자열 구문에 대한 자세한 내용은 [설명서](https://docs.mongodb.org/manual/reference/connection-string/).

* `db`
데이터베이스의 이름입니다. AEM의 기본값은 입니다. 
`aem-author`.

* `customBlobStore`
배포가 데이터베이스에 바이너리를 저장하는 경우 작업 집합의 일부가 됩니다. 이러한 이유로 다음과 같은 대체 데이터 저장소를 수행하여 MongoDB 내에 바이너리를 저장하지 않는 것이 좋습니다. 
`FileSystem` NAS의 데이터 저장소

* `cache`
캐시 크기(MB)입니다. 이 기능은 
`DocumentNodeStore`. 기본값은 256MB입니다. 그러나 Oak 읽기 성능은 더 큰 캐시를 통해 이점이 있습니다.

* `blobCacheSize`
자주 사용되는 BLOB은 데이터 저장소에서 새로 고쳐지지 않도록 AEM에서 캐시할 수 있습니다. 이는 특히 MongoDB 데이터베이스에 blob을 저장할 때 성능에 더 많은 영향을 줍니다. 모든 파일 시스템 기반 데이터 저장소는 운영 체제 수준 디스크 캐시를 통해 이점을 얻을 수 있습니다.

#### 데이터 저장소 구성 {#data-store-configuration}

데이터 저장소는 임계값보다 크기가 큰 파일을 저장하는 데 사용됩니다. 해당 임계값 아래에서는 파일이 문서 노드 저장소 내에 속성으로 저장됩니다. 만약 `MongoBlobStore` 를 사용하면 MongoDB에서 전용 컬렉션을 만들어 blob을 저장합니다. 이 컬렉션은 `mongod` 인스턴스 및 는 `mongod` 성능 문제를 방지하기 위해 더 많은 RAM을 사용합니다. 이러한 이유로 권장되는 구성은 `MongoBlobStore` 프로덕션 배포 및 사용 `FileDataStore` 모든 AEM 인스턴스 간에 공유된 NAS에 의해 지원됩니다. 운영 체제 레벨 캐시는 파일 관리를 효율적으로 하기 때문에, 파일 시스템이 효율적으로 사용되고, 작은 문서가 많은 경우, 디스크 상의 파일의 최소 크기를 디스크의 블록 크기에 가깝게 설정하여 파일의 작업 세트에 과도하게 기여하지 않도록 한다 `mongod` 인스턴스.

다음은 MongoDB를 사용하여 최소한의 AEM 배포를 위한 일반적인 데이터 저장소 구성입니다.

```xml
# org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config
# The minimum size of an object that should be stored in this data store.
minRecordLength=4096
path=/datastore
maxCachedBinarySize=4096
cacheSizeInMB=128
```

위치:

* `minRecordLength`
크기(바이트)입니다. 이 크기보다 작거나 같은 바이너리는 문서 노드 저장소와 함께 저장됩니다. Blob의 ID를 저장하지 않고 바이너리의 콘텐츠가 저장됩니다. 이 크기보다 큰 바이너리의 경우 바이너리의 ID가 노드 컬렉션의 Document 속성으로 저장되고 바이너리의 본문은 
`FileDataStore` 디스크에 4096바이트는 일반적인 파일 시스템 블록 크기입니다.

* `path`
데이터 저장소의 루트에 대한 경로입니다. MongoMK 배포의 경우, 모든 AEM 인스턴스에 사용할 수 있는 공유 파일 시스템이어야 합니다. 일반적으로 NAS(Network Attached Storage) 서버가 사용됩니다. Amazon Web Services과 같은 클라우드 배포를 위해 
`S3DataFileStore` 도 사용할 수 있습니다.

* `cacheSizeInMB`
이진 캐시의 총 크기(MB)입니다. 바이너리를 보다 적게 캐시하는 데 사용됩니다 
`maxCacheBinarySize` 설정

* `maxCachedBinarySize`
이진 캐시에서 캐시된 바이너리의 최대 크기(바이트)입니다. 파일 시스템 기반 데이터 저장소를 사용하는 경우 운영 체제에 의해 바이너리가 이미 캐시되므로 데이터 저장소 캐시에 높은 값을 사용하지 않는 것이 좋습니다.

#### 쿼리 힌트 비활성화 {#disabling-the-query-hint}

속성을 추가하여 모든 쿼리와 함께 전송된 쿼리 힌트를 비활성화하는 것이 좋습니다

`-Doak.mongo.disableIndexHint=true`

AEM을 시작할 때 . 이렇게 하면 MongoDB가 내부 통계를 기반으로 사용할 가장 적절한 인덱스를 계산합니다.

쿼리 힌트가 비활성화되지 않으면 인덱스의 성능 튜닝은 AEM 성능에 영향을 주지 않습니다.

#### MongoMK용 영구 캐시 활성화 {#enable-persistent-cache-for-mongomk}

MongoDB 배포에 대해 영구 캐시 구성을 사용하여 I/O 읽기 성능이 뛰어난 환경의 속도를 극대화하는 것이 좋습니다. 자세한 내용은 [Jackrabbit Oak 설명서](https://jackrabbit.apache.org/oak/docs/nodestore/persistent-cache.html).

## MongoDB 운영 체제 최적화 {#mongodb-operating-system-optimizations}

### 운영 체제 지원 {#operating-system-support}

MongoDB 2.6은 RAM과 디스크 간의 운영 체제 수준 관리의 일부 측면에 민감한 메모리 매핑 스토리지 엔진을 사용합니다. MongoDB 인스턴스의 쿼리 및 읽기 성능은 종종 페이지 오류라고 하는 느린 I/O 작업을 회피하거나 제거하는데 의존합니다. 이것은 페이지에 적용되는 페이지 장애입니다 `mongod` 특히 프로세스를 진행합니다. 운영체제 수준 페이지 장애와 혼동해서는 안 됩니다.

빠른 작업을 위해 MongoDB 데이터베이스는 이미 RAM에 있는 데이터만 액세스해야 합니다. 액세스해야 하는 데이터는 인덱스와 데이터로 구성됩니다. 이 인덱스 및 데이터 컬렉션을 작업 집합이라고 합니다. 작업 세트가 사용 가능한 RAM MongoDB보다 큰 경우 I/O 비용이 발생하는 디스크에서 해당 데이터를 페이징하여 메모리에 이미 있는 다른 데이터를 제거해야 합니다. 제거로 인해 디스크 페이지 오류에서 데이터가 다시 로드되면 성능이 제어되고 성능이 저하됩니다. 작업 세트가 동적 및 변수인 경우 작업을 지원하기 위해 더 많은 페이지 오류가 발생합니다.

MongoDB는 다양한 Linux, Windows 및 Mac OS를 포함한 다양한 운영 체제에서 실행됩니다. 자세한 내용은 [https://docs.mongodb.com/manual/installation/#supported-platforms](https://docs.mongodb.com/manual/installation/#supported-platforms) 추가 세부 정보. 선택한 운영 체제에 따라 MongoDB에는 다른 운영 체제 수준 권장 사항이 있습니다. 문서는에 있습니다. [https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration](https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration) 편의를 위해 여기에 요약해 놓았습니다

#### Linux {#linux}

* 투명한 페이지 및 조각 사기를 끕니다. 자세한 내용은 [투명한 큰 페이지 설정](https://docs.mongodb.com/manual/tutorial/transparent-huge-pages/) 추가 정보.
* [미리 읽기 설정 조정](https://docs.mongodb.com/manual/administration/production-notes/#readahead) 사용 사례에 맞게 데이터베이스 파일을 저장하는 디바이스

   * MMAPv1 스토리지 엔진의 경우 작업 세트가 사용 가능한 RAM보다 크고 문서 액세스 패턴이 무작위이면 사전 설정을 32 또는 16으로 낮추는 것이 좋습니다. 다른 설정을 평가하여 상주 메모리를 극대화하고 페이지 장애 수를 줄이는 최적의 값을 찾습니다.
   * WiredTiger 스토리지 엔진의 경우 스토리지 미디어 유형(회전, SSD 등)에 상관없이 가독성을 0으로 설정합니다. 일반적으로, 보다 높은 읽기 능력 값에서 측정 가능하고 반복적이며 안정적인 이점을 나타내는 테스트가 없는 한 권장되는 사전 설정을 사용하십시오. [MongoDB Professional 지원](https://docs.mongodb.com/manual/administration/production-notes/#readahead) 사전 검토가 없는 구성에 대한 조언 및 지침을 제공할 수 있습니다.

* 가상 환경에서 RHEL 7/CentOS 7을 실행하는 경우 조정된 도구를 비활성화합니다.
* 가상 환경에서 RHEL 7/CentOS 7을 실행하면 튜닝된 툴은 성능 처리량에서 파생된 성능 프로필을 자동으로 호출하여 미리 읽기 설정을 4MB로 자동 설정합니다. 이는 성능에 부정적인 영향을 줄 수 있습니다.
* SSD 드라이브에 대해 노드 또는 최종 디스크 스케줄러를 사용합니다.
* 게스트 VM에서 가상 드라이브를 위한 noop 디스크 스케줄러를 사용하십시오.
* NUMA를 사용하지 않거나 vm.zone_replace_mode를 0으로 설정하고 실행합니다. [단신](https://docs.mongodb.com/manual/administration/production-notes/#readahead) 노드 인터리빙이 있는 인스턴스. 다음을 참조하십시오. [MongoDB 및 NUMA 하드웨어](https://docs.mongodb.com/manual/administration/production-notes/#readahead) 추가 정보.

* 사용 사례에 맞게 하드웨어의 제한 값을 조정합니다. 여러 개일 경우 [단신](https://docs.mongodb.com/manual/reference/program/mongod/#bin.mongod) 또는 [몬고](https://docs.mongodb.com/manual/reference/program/mongos/#bin.mongos) 인스턴스가 동일한 사용자 아래에서 실행 중이어서 ulimit 값을 적절하게 조정합니다. 다음을 참조하십시오. [UNIX 제한 설정](https://docs.mongodb.com/manual/reference/ulimit/) 추가 정보.

* 에 참고 사용 [dbPath](https://docs.mongodb.com/manual/reference/configuration-options/#storage.dbPath) 마운트 지점
* 배포에 대해 충분한 파일 핸들(fs.file-max), 커널 pid 제한(kernel.pid_max) 및 프로세스당 최대 스레드(kernel.threads-max)를 구성합니다. 큰 시스템의 경우 다음 값이 좋은 시작점을 제공합니다.

   * fs.file-max 값 98000,
   * kernel.pid_max 값 64000,
   * andkernel.threads-max 값 64000

* 시스템에 스왑 공간이 구성되어 있는지 확인합니다. 적절한 크기 조정에 대한 자세한 내용은 운영 체제 설명서를 참조하십시오.
* 시스템 기본 TCP keepalive가 올바르게 설정되었는지 확인합니다. 값이 300이면 복제본 세트 및 공유 클러스터에 대해 성능이 향상됩니다. 다음을 참조하십시오. [TCP 보존 시간이 MongoDB 배포에 영향을 줍니까?](https://docs.mongodb.com/manual/faq/diagnostics/#faq-keepalive) 를 참조하십시오.

#### Windows {#windows}

* NTFS &quot;마지막 액세스 시간&quot; 업데이트를 사용하지 않도록 설정하는 것이 좋습니다. 이는 Unix와 같은 시스템에서 작업을 비활성화하는 것과 유사합니다.

### WiredTiger {#wiredtiger}

MongoDB 3.2부터 MongoDB의 기본 스토리지 엔진은 WiredTiger 스토리지 엔진입니다. 이 엔진은 여러 가지 강력하고 확장 가능한 기능을 제공하므로 전반적인 데이터베이스 워크로드에 훨씬 적합합니다. 다음 섹션에서는 이러한 기능에 대해 설명합니다.

#### 문서 수준 동시성 {#document-level-concurrency}

WiredTiger는 쓰기 작업에 문서 수준의 동시 시청 제어를 사용합니다. 따라서 여러 클라이언트가 한 컬렉션의 여러 문서를 동시에 수정할 수 있습니다.

대부분의 읽기 및 쓰기 작업을 위해 WiredTiger는 낙관적 동시 시청 제어를 사용합니다. WiredTiger는 글로벌, 데이터베이스 및 수집 수준에서 의도 잠금만 사용합니다. 스토리지 엔진이 두 작업 간의 충돌을 감지하면 쓰기 충돌이 발생하여 MongoDB가 해당 작업을 투명하게 다시 시도할 수 있습니다. 일반적으로 여러 데이터베이스를 포함하는 단기 작업 상태인 일부 전역 작업은 여전히 전역 &quot;인스턴스 전체&quot; 잠금이 필요합니다.

컬렉션을 삭제하는 등의 일부 다른 작업은 여전히 전용 데이터베이스 잠금이 필요합니다.

#### 스냅샷 및 체크포인트 {#snapshots-and-checkpoints}

WiredTiger는 MVCC(MultiVersion Concurrency Control)를 사용합니다. 작업이 시작되면 WiredTiger는 트랜잭션 데이터에 대한 시점 스냅샷을 제공합니다. 스냅샷은 메모리 내 데이터를 일관되게 표시합니다.

WiredTiger는 디스크에 쓸 때 스냅샷의 모든 데이터를 모든 데이터 파일에 일관된 방식으로 디스크에 기록합니다. 지금 [내구성](https://docs.mongodb.com/manual/reference/glossary/#term-durable) 데이터는 데이터 파일에서 체크포인트 역할을 합니다. 체크포인트는 데이터 파일이 마지막 체크포인트를 포함하여 일관되도록 합니다. 즉, 체크포인트가 복구 지점으로 사용될 수 있습니다.

MongoDB는 60초 또는 2GB의 저널 데이터 간격으로 체크포인트(즉, 디스크에 스냅샷 데이터를 기록)를 생성하도록 WiredTiger를 구성합니다.

새 체크포인트를 쓰는 동안 이전 체크포인트가 여전히 유효합니다. 따라서 MongoDB가 종료되거나 새 검사점을 쓰는 동안 오류가 발생하더라도 다시 시작하면 MongoDB는 마지막으로 유효한 검사점에서 복구할 수 있습니다.

WiredTiger의 메타데이터 테이블이 새 검사점을 참조하도록 자동으로 업데이트되면 새로운 검사점에 액세스할 수 있고 영구적이 됩니다. 새 체크포인트에 액세스할 수 있으면 WiredTiger는 페이지를 이전 체크포인트에서 분리합니다.

WiredTiger 사용, [저널링](https://docs.mongodb.com/manual/reference/glossary/#term-durable), MongoDB는 마지막 체크포인트에서 복구할 수 있습니다. 그러나 마지막 체크포인트 이후에 수행된 변경 내용을 복구하려면 [저널링](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### 저널 {#journal}

WiredTiger는 [체크포인트](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-checkpoints) 데이터 내구성을 보장합니다.

WiredTiger 저널은 체크포인트 간 모든 데이터 수정 사항을 유지합니다. MongoDB가 체크포인트 사이에 종료되면 저널을 사용하여 마지막 체크포인트 이후 수정된 모든 데이터를 재생합니다. MongoDB가 저널 데이터를 디스크에 기록하는 빈도에 대한 자세한 내용은 [저널링 프로세스](https://docs.mongodb.com/manual/core/journaling/#journal-process).

WiredTiger 저널은 [간장](https://docs.mongodb.com/manual/core/journaling/#journal-process) 압축 라이브러리. 압축이 없거나 대체 압축 알고리즘을 지정하려면 [storage.wiredTiger.engineConfig.journalCompressor](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.journalCompressor) 설정

자세한 내용은 다음을 참조하십시오. [WiredTiger로 저널링](https://docs.mongodb.com/manual/core/journaling/#journaling-wiredtiger).

>[!NOTE]
>
>WiredTiger의 최소 로그 레코드 크기는 128바이트입니다. 로그 레코드가 128바이트 이하인 경우 WiredTiger는 해당 레코드를 압축하지 않습니다.
>
>다음을 설정하여 저널링을 비활성화할 수 있습니다 [storage.journal.enabled](https://docs.mongodb.com/manual/reference/configuration-options/#storage.journal.enabled) false로 설정하면 분개 유지 관리 오버헤드가 줄어듭니다.
>
>대상 [독립형](https://docs.mongodb.com/manual/reference/glossary/#term-standalone) 인스턴스를 사용하지 않으면 MongoDB가 체크포인트 간에 예기치 않게 종료될 때 일부 데이터 수정 사항이 손실됩니다. 멤버 [복제본 세트](https://docs.mongodb.com/manual/reference/glossary/#term-replica-set)복제 프로세스는 충분한 내구성을 보장할 수 있습니다.

#### 압축 {#compression}

WiredTiger를 사용하면 MongoDB에서 모든 컬렉션 및 인덱스에 대한 압축을 지원합니다. 압축은 추가 CPU의 비용으로 스토리지 사용을 최소화합니다.

기본적으로 WiredTiger는 [간장](https://docs.mongodb.com/manual/reference/glossary/#term-snappy) 모든 컬렉션 및 [접두사 압축](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression) 모든 인덱스에 대해.

컬렉션의 경우 다음 방법으로 압축 차단 [zlib](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) 도 사용할 수 있습니다. 압축이 없거나 대체 압축 알고리즘을 지정하려면 [storage.wiredTiger.collectionConfig.blockCompressor](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) 설정

인덱스의 경우 [접두사 압축](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression)를 사용하려면 [storage.wiredTiger.indexConfig.prefixCompression](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.indexConfig.prefixCompression) 설정

또한 압축 설정은 컬렉션 및 인덱스를 만드는 동안 컬렉션별 및 인덱스별로 구성할 수 있습니다. 자세한 내용은 [스토리지 엔진 옵션 지정](https://docs.mongodb.com/manual/reference/method/db.createCollection/#create-collection-storage-engine-options) 및 [db.collection.createIndex() storageEngine](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/#createindex-options) 선택 사항입니다.

대부분의 워크로드의 경우 기본 압축 설정은 저장 효율성 및 처리 요구 사항에 균형을 맞춥니다.

WiredTiger 저널도 기본적으로 압축됩니다. 저널 압축에 대한 자세한 내용은 [저널](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### 메모리 사용 {#memory-use}

WiredTiger를 사용하는 MongoDB는 WiredTiger 내부 캐시와 파일 시스템 캐시를 모두 사용합니다.

3.4부터 WiredTiger 내부 캐시는 기본적으로 다음 중 큰 것을 사용합니다.

* 50%의 RAM - 1GB 또는
* 256MB

기본적으로 WiredTiger는 모든 인덱스에 대해 Snappy 블록 압축 및 접두사 압축을 사용합니다. 압축 기본값은 전역 수준에서 구성할 수 있으며, 수집 및 색인 작성 중에 컬렉션별 및 인덱스별로 설정할 수도 있습니다.

WiredTiger 내부 캐시 및 On-Disk 형식의 데이터에 다른 표현이 사용됩니다.

* 파일 시스템 캐시의 데이터는 데이터 파일을 압축할 때 얻을 수 있는 이점을 포함하여 디스크 상의 형식과 동일합니다. 운영 체제에서 디스크 입출력을 줄이기 위해 파일 시스템 캐시를 사용합니다.

WiredTiger 내부 캐시에 로드된 인덱스의 데이터 표현은 온디스크 형식에 다른 표시이지만 여전히 인덱스 접두사 압축을 사용하여 RAM 사용을 줄일 수 있습니다.

인덱스 접두사 압축은 인덱스 필드에서 공통 접두사를 중복 제거합니다.

WiredTiger 내부 캐시의 수집 데이터가 압축되지 않으며 온 디스크 형식과 다른 표현을 사용합니다. 블록 압축은 디스크 상의 스토리지 비용을 크게 절감할 수 있지만 서버에서 데이터를 조작하려면 압축하지 않아야 합니다.

파일 시스템 캐시를 통해 MongoDB는 WiredTiger 캐시 또는 다른 프로세스에서 사용하지 않는 모든 사용 가능한 메모리를 자동으로 사용합니다.

WiredTiger 내부 캐시의 크기를 조정하려면 다음을 참조하십시오 [storage.wiredTiger.engineConfig.cacheSizeGB](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.cacheSizeGB) 및 [—wiredTigerCacheSizeGB](https://docs.mongodb.com/manual/reference/program/mongod/#cmdoption-wiredtigercachesizegb). WiredTiger 내부 캐시 크기를 기본값으로 늘리지 마십시오.

### NUMA {#numa}

NUMA(Non Uniform Memory Access)를 사용하면 커널에서 프로세서 코어에 메모리를 매핑하는 방법을 관리할 수 있습니다. 이 경우 코어 액세스 속도를 높여 필요한 데이터에 액세스할 수 있게 하지만, NUMA는 읽기를 예측할 수 없으므로 추가적인 지연을 가져오는 MMAP을 방해합니다. 따라서 NUMA를 `mongod` 기능이 있는 모든 운영 체제에 대해 처리합니다.

기본적으로 NUMA 아키텍처 메모리는 CPU에 연결되고 CPU는 버스에 연결됩니다. SMP 또는 UMA 아키텍처에서는 메모리가 버스에 연결되고 CPU에서 공유됩니다. 스레드가 NUMA CPU에 메모리를 할당하면 정책에 따라 메모리를 할당합니다. 기본값은 사용 가능한 메모리가 없는 한 스레드의 로컬 CPU에 연결된 메모리를 할당하는 것입니다. 이 경우 추가 비용으로 사용 가능한 CPU의 메모리를 사용합니다. 할당된 메모리는 CPU 간에 이동되지 않습니다. 할당은 상위 스레드에서 상속된 정책에 의해 수행되며, 이는 궁극적으로 프로세스를 시작한 스레드입니다.

시스템을 멀티 코어 단일 메모리 아키텍처로 보는 많은 데이터베이스에서, 이는 초기 CPU가 가득 차면서 나중에 보조 CPU가 충진되도록 합니다. 특히 중앙 스레드가 메모리 버퍼를 할당하는 경우 이 문제가 발생합니다. 해결 방법은 를 시작하는 데 사용되는 기본 스레드의 NUMA 정책을 변경하는 것입니다 `mongod` 프로세스.

이 작업은 다음 명령을 실행하여 수행할 수 있습니다.

```shell
numactl --interleaved=all <mongod> -f config
```

이 정책은 모든 CPU 노드에 대해 라운드 로빈 방식으로 메모리를 할당하여 모든 노드에 균일한 분포를 보장합니다. 여러 CPU 하드웨어가 있는 시스템처럼 메모리에 대한 최고의 성능 액세스를 생성하지 않습니다. 약 절반 정도의 메모리 작업이 느릴 것이고 버스를 넘어가면 됩니다. `mongod` 이 최적의 방법으로 NUMA를 타겟으로 쓰지 않았으므로 합리적인 절충이 가능합니다.

### NUMA 문제 {#numa-issues}

만약 `mongod` 프로세스가 `/etc/init.d` 폴더에서 올바른 NUMA 정책으로 시작하지 않을 수 있습니다. 기본 정책의 내용에 따라 문제가 발생할 수 있습니다. MongoDB의 다양한 Linux 패키지 관리자 설치 프로그램이 `/etc/init.d` 위에 요약된 단계를 수행하는 작업입니다. 아카이브( `.tar.gz`)을 클릭하여 수동으로 monobody를 실행해야 합니다 `numactl` 프로세스.

>[!NOTE]
>
>사용 가능한 NUMA 정책에 대한 자세한 내용은 [numactl 설명서](https://linux.die.net/man/8/numactl).

MongoDB 프로세스는 다른 할당 정책에 따라 다르게 동작합니다.

```

```

* `-membind=<nodes>`
나열된 노드에만 할당하십시오. Mongoth는 나열된 노드에 메모리를 할당하지 않으며 사용 가능한 메모리를 모두 사용하지 못할 수 있습니다.

* `-cpunodebind=<nodes>`
노드에서만 실행됩니다. Mongod는 지정된 노드에서만 실행되며 해당 노드에서만 사용할 수 있는 메모리만 사용합니다.

* `-physcpubind=<nodes>`
나열된 CPU(코어)에서만 실행됩니다. Mongo신 은 나열된 CPU에서만 실행되며 해당 CPU에서 사용할 수 있는 메모리만 사용합니다.

* `--localalloc`
항상 현재 노드에 메모리를 할당하지만 스레드가 실행되는 모든 노드를 사용합니다. 한 스레드에서 할당을 수행하는 경우 해당 CPU에 사용할 수 있는 메모리만 사용됩니다.

* `--preferred=<node>`
노드보다 할당을 선호하지만, 기본 설정 노드가 가득 찬 경우 다른 노드에게 다시 적용됩니다. 노드 정의를 위한 상대 표기법을 사용할 수 있습니다. 또한 스레드는 모든 노드에서 실행됩니다.

정책 중 일부는 사용 가능한 모든 RAM보다 적은 RAM을 `mongod` 프로세스. MySQL과 달리 MongoDB는 운영 체제 수준 페이징을 적극적으로 방지하여 결과적으로 `mongod` 프로세스에 사용 가능한 메모리가 거의 없을 수 있습니다.

#### 교환 {#swapping}

데이터베이스의 메모리 집약적인 특성으로 인해 운영 체제 수준 바꾸기를 사용하지 않도록 설정해야 합니다. MongoDB 프로세스는 디자인에 의한 교환을 피합니다.

#### 원격 파일 시스템 {#remote-filesystems}

NFS와 같은 원격 파일 시스템은 MongoDB의 내부 데이터 파일(단일 프로세스 데이터베이스 파일)에 너무 많은 지연을 발생하므로 권장되지 않습니다. 이는 NFS가 권장되는 Oak Blob(FileDataStore)의 저장소에 필요한 공유 파일 시스템과 혼동하지 않도록 합니다.

#### 미리 보기 {#read-ahead}

미리 읽기 작업을 수행하여 페이지를 임의의 읽기를 사용하여 페이지를 호출할 때 불필요한 블록을 디스크에서 읽지 않아 입출력 대역폭을 불필요한 소모하도록 해야 합니다.

### Linux 요구 사항 {#linux-requirements}

#### 최소 커널 버전 {#minimum-kernel-versions}

* **2.6.23** 대상 `ext4` 파일

* **2.6.25** 대상 `xfs` 파일

#### 데이터베이스 디스크에 대한 권장 설정 {#recommended-settings-for-database-disks}

**작업 해제**

권장 사항 `atime` 데이터베이스를 포함할 디스크에 대해 이 해제되어 있습니다.

**NOOP 디스크 스케줄러 설정**

다음을 통해 이 작업을 수행할 수 있습니다.

먼저 현재 설정된 입출력 스케줄러를 확인합니다. 이 작업은 다음 명령을 실행하여 수행할 수 있습니다.

```shell
cat /sys/block/sdg/queue/scheduler
```

응답이 `noop` 네가 더 할 필요가 없다.

NOOP가 설정된 입출력 스케줄러가 아닌 경우 다음을 실행하여 변경할 수 있습니다.

```shell
echo noop > /sys/block/sdg/queue/scheduler
```

**미리 읽기 값을 조정합니다**

MongoDB 데이터베이스가 실행되는 디스크에 32값을 사용하는 것이 좋습니다. 이것은 16킬로바이트에 해당한다. 다음을 실행하여 설정할 수 있습니다.

```shell
sudo blockdev --setra <value> <device>
```

#### NTP 사용 {#enable-ntp}

MongoDB 데이터베이스를 호스팅하는 시스템에 NTP가 설치되어 실행 중인지 확인하십시오. 예를 들어 CentOS 시스템에서 yum 패키지 관리자를 사용하여 설치할 수 있습니다.

```shell
sudo yum install ntp
```

NTP 데몬이 설치되고 성공적으로 시작되면 서버의 시간 오프셋을 사용하여 드리프트 파일을 확인할 수 있습니다.

#### 투명한 큰 페이지 비활성화 {#disable-transparent-huge-pages}

Red Hat Linux는 THP(Transparent Large Pages)라는 메모리 관리 알고리즘을 사용합니다. 데이터베이스 작업 로드에 운영 체제를 사용하는 경우에는 비활성화하는 것이 좋습니다.

아래 절차에 따라 비활성화할 수 있습니다.

1. 를 엽니다. `/etc/grub.conf` 원하는 텍스트 편집기에 파일을 넣을 수 있습니다.
1. grub.conf 파일에 다음 줄을 추가합니다.

   ```xml
   transparent_hugepage=never
   ```

1. 마지막으로 다음을 실행하여 설정이 적용되었는지 확인합니다.

   ```shell
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   THP가 비활성화된 경우 위의 명령의 출력은 다음과 같습니다.

   ```xml
   always madvise [never]
   ```

>[!NOTE]
>
>투명한 큰 페이지에 대한 자세한 내용은 다음을 참조하십시오 [문서](https://access.redhat.com/solutions/46111).

#### NUMA 사용 안 함 {#disable-numa}

NUMA가 활성화된 대부분의 설치에서는 MongoDB 데몬이 NUMA에서 서비스로 실행되는 경우 자동으로 비활성화됩니다 `/etc/init.d` 폴더를 입력합니다.

이 경우 프로세스 수준별로 NUMA를 비활성화할 수 있습니다. 비활성화하려면 다음 명령을 실행합니다.

```shell
numactl --interleave=all <path_to_process>
```

위치 `<path_to_process>` 은(는) 단신 프로세스의 경로입니다.

그런 다음 다음을 실행하여 영역 재사용을 비활성화합니다.

```shell
echo 0 > /proc/sys/vm/zone_reclaim_mode
```

#### 단신 프로세스에 대한 제한 설정 조정 {#tweak-the-ulimit-settings-for-the-mongod-process}

Linux를 사용하면 를 통해 리소스 할당을 구성할 수 있습니다. `ulimit` 명령. 이 작업은 사용자 또는 프로세스에 따라 수행할 수 있습니다.

다음에 따라 Monody 프로세스에 대한 제한을 구성하는 것이 좋습니다 [MongoDB 권장 제한 설정](https://docs.mongodb.org/manual/reference/ulimit/#recommended-ulimit-settings).

#### MongoDB I/O 성능 테스트 {#test-mongodb-i-o-performance}

MongoDB는 `mongoperf` I/O 성능을 테스트하도록 설계되었습니다. 인프라를 구성하는 모든 MongoDB 인스턴스의 성능을 테스트하는 데 사용하는 것이 좋습니다.

사용 방법에 대한 자세한 정보 `mongoperf`, 보기 [MongoDB 설명서](https://docs.mongodb.org/manual/reference/program/mongoperf/).

>[!NOTE]
>
>참고 사항 `mongoperf` 는 실행 중인 플랫폼에서 MongoDB 성능을 나타내는 표시기로 설계되었습니다. 이로 인해 생산시스템의 성능에 대한 최종 결정이라고 판단해서는 안 된다.
>
>보다 정확한 성능 결과를 위해 `fio` Linux 도구.

**배포를 구성하는 가상 시스템에서 읽기 성능을 테스트합니다**

도구를 설치한 후 테스트를 실행하기 위해 MongoDB 데이터베이스 디렉터리로 전환합니다. 그런 다음 를 실행하여 첫 번째 테스트를 시작합니다 `mongoperf`이 구성을 사용하여 다음을 수행합니다.

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true}" | mongoperf
```

원하는 출력은 모든 MongoDB 인스턴스에 대해 32개의 스레드에서 실행되는 최대 2GB(2GB/s) 및 500.000 IOPS에 도달해야 합니다.

이번에는 메모리 매핑된 파일을 사용하여 두 번째 테스트를 실행합니다. `mmf:true` 매개 변수:

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true,mmf:true}" | mongoperf
```

제2 테스트의 출력은 메모리 전송 성능을 나타내는 제1 테스트보다 상당히 높아야 합니다.

>[!NOTE]
>
>테스트를 수행할 때 운영 체제 모니터링 시스템에서 해당 가상 시스템에 대한 I/O 사용량 통계를 확인합니다. 입출력 읽기의 값이 100% 미만인 경우 가상 시스템에 문제가 있을 수 있습니다.

**기본 MongoDB 인스턴스의 쓰기 성능을 테스트합니다.**

그런 다음 실행으로 기본 MongoDB 인스턴스의 I/O 쓰기 성능을 확인합니다 `mongoperf` 동일한 설정을 사용하는 MongoDB 데이터베이스 디렉터리에서

```shell
echo "{nThreads:32,fileSizeMB:1000,w:true}" | mongoperf
```

원하는 출력은 초당 12MB로 약 3000 IOPS에 도달해야 하며 스레드 수는 거의 변화하지 않습니다.

## 가상화 환경을 위한 단계 {#steps-for-virtualised-environments}

### VMWare {#vmware}

WMWare ESX를 사용하여 가상화된 환경을 관리하고 배포할 경우 MongoDB 작업을 수용하려면 ESX 콘솔에서 다음 설정을 수행해야 합니다.

1. 메모리 부풀림 해제
1. MongoDB 데이터베이스를 호스트할 가상 컴퓨터에 대한 메모리를 미리 할당하고 예약합니다.
1. 스토리지 입출력 제어를 사용하여 `mongod` 프로세스.
1. MongoDB를 호스팅하는 시스템의 CPU 리소스 보장 [CPU 예약](https://pubs.vmware.com/vsphere-4-esx-vcenter/index.jsp?topic=/com.vmware.vsphere.vmadmin.doc_41/vsp_vm_guide/configuring_virtual_machines/t_allocate_cpu_resources.html)

1. ParaVirtual I/O 드라이버 사용을 고려해 보십시오. 이 작업을 수행하는 방법에 대한 자세한 내용은 다음을 확인하십시오 [기술 자료 문서](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&amp;cmd=displayKC&amp;externalId=1010398).

### Amazon Web Services {#amazon-web-services}

Amazon Web Services과 MongoDB를 설정하는 방법에 대한 설명서는 다음을 확인하십시오. [AWS 통합 구성](https://docs.cloud.mongodb.com/tutorial/configure-aws-settings/) MongoDB 웹 사이트의 문서

## 배포 전 MongoDB 보안 {#securing-mongodb-before-deployment}

다음에서 이 게시물 보기 [MongoDB 보안 배포](https://blogs.adobe.com/security/2015/07/securely-deploying-mongodb-3-0.html) 배포하기 전에 데이터베이스 구성을 보호하는 방법에 대한 자세한 내용을 제공합니다.

## Dispatcher {#dispatcher}

### Dispatcher에 대한 운영 체제 선택 {#choosing-the-operating-system-for-the-dispatcher}

MongoDB 배포를 제대로 수행하려면 디스패처를 호스트할 운영 체제가 실행 중이어야 합니다 **Apache httpd** **버전 2.4 이상.**

또한 보안 영향을 최소화하기 위해 빌드에 사용된 모든 라이브러리가 최신 상태인지 확인하십시오.

### Dispatcher 구성 {#dispatcher-configuration}

일반적인 Dispatcher 구성은 단일 AEM 인스턴스의 요청 처리량을 10~20배 더 많이 처리합니다.

Dispatcher는 주로 상태를 저장하지 않으므로 쉽게 가로로 확장할 수 있습니다. 일부 배포의 경우 작성자가 특정 리소스에 액세스하지 못하도록 제한해야 합니다. 이러한 이유로 작성자 인스턴스와 함께 디스패처를 사용하는 것이 좋습니다.

디스패처 없이 AEM을 실행하려면 다른 애플리케이션에서 SSL 종료 및 로드 밸런싱을 수행해야 합니다. 고정 연결이라는 개념인 세션이 생성된 AEM 인스턴스에 대한 친화성을 가져야 하므로 필요합니다. 목적은 컨텐츠에 대한 업데이트로 최소한의 지연 시간이 발생하도록 보장하는 것입니다.

을(를) 확인합니다. [Dispatcher 설명서](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) 구성 방법에 대한 자세한 내용을 참조하십시오.

### 추가 구성 {#additional-configuration}

#### 고정 연결 {#sticky-connections}

고정 연결은 한 명의 사용자에 대한 개인화된 페이지와 세션 데이터를 모두 AEM의 동일한 인스턴스에서 구성하도록 합니다. 이 데이터는 인스턴스에 저장되므로 동일한 사용자의 후속 요청은 동일한 인스턴스에 반환됩니다.

AEM 인스턴스로 요청을 라우팅하는 모든 내부 레이어에 대해 고정 연결을 활성화하여 후속 요청이 동일한 AEM 인스턴스에 연결되도록 하는 것이 좋습니다. 이렇게 하면 인스턴스 간에 컨텐츠를 업데이트할 때 특히 주목할 만한 지연을 최소화할 수 있습니다.

#### 긴 만료 {#long-expires}

기본적으로 AEM Dispatcher에서 전송된 컨텐츠에는 컨텐츠 만료가 표시되지 않고 마지막 수정 및 태그 헤더가 있습니다. 이렇게 하면 사용자 인터페이스가 항상 최신 버전의 리소스를 가져올 수 있지만 이는 또한 브라우저가 리소스가 변경되었는지 확인하기 위해 GET 작업을 수행함을 의미합니다. 이로 인해 페이지 로드에 따라 HTTP 응답이 304(수정되지 않음)인 여러 요청이 발생할 수 있습니다. 만료되지 않은 것으로 알려진 리소스의 경우 만료 헤더를 설정하고 마지막으로 수정한 날짜 및 ETag 헤더를 제거하면 콘텐츠가 캐시되고 만료 헤더의 날짜가 충족될 때까지 추가 업데이트 요청이 수행되지 않습니다.

그러나 이 방법을 사용하면 리소스가 만료 헤더가 만료되기 전에 브라우저에서 만료되도록 하는 합리적인 방법이 없음을 의미합니다. 이를 완화하기 위해 클라이언트 라이브러리에 변경할 수 없는 URL을 사용하도록 HtmlClientLibraryManager를 구성할 수 있습니다.

이러한 URL은 변경되지 않을 것입니다. URL에 포함된 리소스의 본문이 변경되면 브라우저가 해당 리소스의 올바른 버전을 요청하도록 해당 변경 사항이 URL에 자동으로 반영됩니다.

기본 구성은 HtmlClientLibraryManager에 선택기를 추가합니다. 선택기가 되면 리소스는 선택기가 온전한 상태로 디스패처에서 캐시됩니다. 또한 이 선택기를 사용하여 올바른 만료 동작을 확인할 수 있습니다. 기본 선택기는 `lc-.*?-lc` 패턴. 다음 Apache httpd 구성 지시문은 해당 패턴과 일치하는 모든 요청이 적절한 만료 시간으로 제공되도록 합니다.

```xml
Header set Expires "Tue, 20 Jan 2037 04:20:42 GMT" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header set Cache-Control "public, no-transform, max-age=267840000" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset ETag "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Last-Modified "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Pragma "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
```

#### 냄새 없음 {#no-sniff}

콘텐츠 유형이 없이 콘텐츠가 전송되는 경우, 많은 브라우저는 콘텐츠의 처음 몇 바이트를 읽어서 콘텐츠 유형을 추측하려고 합니다. 이를 &quot;snieping&quot;이라고 합니다. 저장소에 쓸 수 있는 사용자가 콘텐츠 유형이 없는 악의적인 콘텐츠를 업로드할 수 있으므로 Sniffing에서는 보안 취약성이 발생합니다.

이러한 이유로 를 추가하는 것이 좋습니다 `no-sniff` 헤더 를 디스패처에서 제공하는 리소스에 추가합니다. 하지만 디스패처는 헤더를 캐시하지 않습니다. 즉, 로컬 파일 시스템에서 제공되는 컨텐츠는 Origin AEM 서버의 원래 컨텐츠 유형 헤더를 사용하는 대신 확장으로 결정되는 컨텐츠 유형이 있습니다.

파일 형식 없이 캐시된 리소스를 제공하지 않는 것으로 알려진 웹 응용 프로그램의 경우 Sniff를 안전하게 활성화할 수 없습니다.

No Sniff를 포함 가능하게 할 수 있습니다.

```xml
Header set X-Content-Type-Options "nosniff"
```

선택적으로 활성화할 수도 있습니다.

```xml
RewriteCond %{REQUEST_URI} \.(?:js|jsonp)$ [OR]
RewriteCond %{QUERY_STRING} (callback|jsonp|cb)=\w+
RewriteRule .* - [E=jsonp_request:1]
Header set X-Content-Type-Options "nosniff"  env=jsonp_request
Header setifempty Content-Type application/javascript env=jsonp_request
```

#### 컨텐츠 보안 정책 {#content-security-policy}

기본 디스패처 설정을 사용하면 CSP라고도 하는 개방형 컨텐츠 보안 정책을 사용할 수 있습니다. 이렇게 하면 페이지가 브라우저 샌드박스의 기본 정책을 기준으로 하는 모든 도메인의 리소스를 로드할 수 있습니다.

신뢰할 수 없거나 확인되지 않은 외부 서버에서 javascript 엔진에 코드를 로드하지 않도록 리소스를 로드할 수 있는 위치를 제한하는 것이 좋습니다.

CSP를 사용하면 정책을 세밀하게 조정할 수 있습니다. 그러나 너무 제한적인 정책이 사용자 인터페이스의 일부를 손상시킬 수 있으므로 복잡한 애플리케이션에서 CSP 헤더를 신중하게 개발해야 합니다.

>[!NOTE]
>
>이 작동 방식에 대한 자세한 내용은 [컨텐츠 보안 정책의 OWASP 페이지](https://www.owasp.org/index.php/Content_Security_Policy).

### 크기 조정 {#sizing}

크기 조정에 대한 자세한 내용은 [하드웨어 크기 조정 지침](/help/managing/hardware-sizing-guidelines.md).

### MongoDB 성능 최적화 {#mongodb-performance-optimization}

MongoDB 성능에 대한 일반 정보는 [MongoDB 성능 분석](https://docs.mongodb.org/manual/administration/analyzing-mongodb-performance/).

## 알려진 제한 사항 {#known-limitations}

### 동시 설치 {#concurrent-installations}

단일 데이터베이스와 함께 여러 AEM 인스턴스를 동시에 사용하는 것은 MongoMK에서 지원되지만 동시 설치는 지원되지 않습니다.

이 문제를 해결하려면 먼저 단일 멤버로 설치를 실행하고 설치가 완료된 후 다른 멤버를 추가합니다.

### 페이지 이름 길이 {#page-name-length}

AEM이 MongoMK 지속성 관리자 배포에서 실행 중인 경우, [페이지 이름은 150자로 제한됩니다.](/help/sites-authoring/managing-pages.md)

>[!NOTE]
>
>[MongoDB 설명서를 참조하십시오](https://docs.mongodb.com/manual/reference/limits/) MongoDB 자체의 알려진 제한 사항과 임계값을 잘 알고 있습니다.
