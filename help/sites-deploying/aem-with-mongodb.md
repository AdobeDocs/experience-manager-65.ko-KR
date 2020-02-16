---
title: AEM with MongoDB
seo-title: AEM with MongoDB
description: MongoDB 배포를 통한 성공적인 AEM에 필요한 작업 및 고려 사항에 대해 알아봅니다.
seo-description: MongoDB 배포를 통한 성공적인 AEM에 필요한 작업 및 고려 사항에 대해 알아봅니다.
uuid: 8028832d-10de-4811-a769-fab699c162ec
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: cd3b979f-53d4-4274-b4eb-a9533329192a
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# AEM with MongoDB{#aem-with-mongodb}

이 문서는 MongoDB와 함께 Adobe Experience Manager를 성공적으로 배포하는 데 필요한 작업 및 고려 사항에 대한 지식을 향상시키는 데 목적이 있습니다.

배포 관련 자세한 내용은 설명서의 [배포 및 유지](/help/sites-deploying/deploy.md) 관리 섹션을 참조하십시오.

## AEM에서 MongoDB를 사용해야 하는 경우 {#when-to-use-mongodb-with-aem}

MongoDB는 일반적으로 다음 기준 중 하나가 충족되는 AEM 작성자 배포를 지원하는 데 사용됩니다.

* 하루 1,000명 이상의 고유 사용자
* 동시 사용자 100명 이상
* 많은 양의 페이지 편집;
* 대규모 롤아웃 또는 활성화.

위의 기준은 작성자 인스턴스에만 해당되며 TarMK 기반이어야 하는 모든 게시 인스턴스에 대해서는 해당되지 않습니다. 작성자 인스턴스는 인증되지 않은 액세스를 허용하지 않으므로 인증된 사용자를 참조하는 사용자 수입니다.

기준이 충족되지 않으면 가용성을 해결하기 위해 TarMK 활성/대기 배포를 권장합니다. 일반적으로 MongoDB는 단일 하드웨어 항목을 통해 얻을 수 있는 것보다 크기 조정 요구 사항이 많은 경우에 고려해야 합니다.

>[!NOTE]
>
>작성자 인스턴스 크기 조정 및 동시 사용자 정의에 대한 추가 정보는 하드웨어 크기 [조정 가이드라인에 있습니다](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel).

### AEM에 대한 최소 MongoDB 배포 {#minimal-mongodb-deployment-for-aem}

다음은 MongoDB의 AEM에 대한 최소 배포입니다. 간단히 말하자면, SSL 종료 및 HTTP 프록시 구성 요소가 일반화되었습니다. 1개의 기본 복제본과 2개의 보조 복제본을 포함한 단일 MongoBD 복제본 세트로 구성됩니다.

![chlimage_1-4](assets/chlimage_1-4.png)

최소 배포에는 복제본 세트로 구성된 3개의 `mongod` 인스턴스가 필요합니다. 한 인스턴스는 주 단위로 선택되고 다른 인스턴스는 보조 인스턴스가 되며, 선택 항목은 에 의해 관리됩니다 `mongod`. 각 인스턴스에 연결된 로컬 디스크입니다. 클러스터가 로드를 지원하려면 IOPS(초당 I/O 작업 수)가 3,000개를 초과하는 최소 12MB/s의 처리량을 권장합니다.

AEM 작성자는 각 AEM 작성자가 세 가지 인스턴스 모두에 연결되면서 `mongod` `mongod` 인스턴스에 연결됩니다. 쓰기는 기본으로 전송되며 모든 인스턴스에서 읽을 수 있습니다. 트래픽은 디스패처가 활성 AEM 작성자 인스턴스 중 하나에 대한 로드를 기반으로 배포됩니다. OAK 데이터 저장소는 `FileDataStore`이며, MMS 또는 MongoDB Ops Manager는 배포 위치에 따라 제공됩니다. 운영 체제 수준 및 로그 모니터링은 Splunk 또는 Ganglia와 같은 타사 솔루션을 통해 제공됩니다.

이 배포에서는 성공적인 구현을 위해 모든 구성 요소가 필요합니다. 누락된 구성 요소는 구현이 작동하지 않게 됩니다.

### 운영 체제 {#operating-systems}

AEM 6에서 지원되는 운영 체제 목록은 기술 요구 [사항 페이지를](/help/sites-deploying/technical-requirements.md)참조하십시오.

### 환경 {#environments}

프로젝트를 실행하는 다른 기술 팀 간의 원활한 커뮤니케이션이 있는 경우 가상화 환경이 지원됩니다. 여기에는 AEM을 실행 중인 팀, 운영 체제를 소유하고 있는 팀, 가상 인프라를 관리하는 팀이 포함됩니다.

가상 환경을 관리하는 팀에서 관리해야 하는 MongoDB 인스턴스의 I/O 용량에 대한 구체적인 요구 사항이 있습니다. 프로젝트가 Amazon Web Services와 같은 클라우드 배포를 사용하는 경우, MongoDB 인스턴스를 지원하기 위해 충분한 입출력 용량과 일관성을 가진 인스턴스가 프로비저닝되어야 합니다. 그렇지 않으면 MongoDB 프로세스와 Oak 리포지토리는 불안정하고 잘못 수행됩니다.

가상화된 환경에서 MongoDB는 VMWare 리소스 할당 정책에 의해 MongoDB의 스토리지 엔진이 장애되지 않도록 하기 위해 특정 입출력 및 VM 구성이 필요합니다. 구현이 성공하면 다양한 팀 사이에 장벽은 없고 모든 팀원은 필요한 성능을 제공하기 위해 등록됩니다.

## 하드웨어 고려 사항 {#hardware-considerations}

### 저장 용량 {#storage}

MongoDB는 일반적으로 SSD와 같은 성능을 가진 SSD 스토리지 또는 스토리지를 필요로 하므로, Read와 Write Throughput을 사용하여 성능을 최대화합니다.

### RAM {#ram}

MMAP 저장소 엔진을 사용하는 MongoDB 버전 2.6 및 3.0에서는 데이터베이스의 작업 세트와 해당 인덱스가 RAM에 맞아야 합니다.

RAM이 부족하면 성능이 크게 저하됩니다. 작업 세트와 데이터베이스의 크기는 애플리케이션에 따라 다릅니다. 일부 추정은 가능하지만, 필요한 RAM의 양을 결정할 수 있는 가장 안정적인 방법은 AEM 애플리케이션을 빌드하고 이를 로드 테스트하는 것입니다.

로드 테스트 프로세스를 지원하기 위해 전체 데이터베이스 크기에 대해 다음 작업 세트 비율을 가정할 수 있습니다.

* SSD 스토리지의 경우 1:10
* 하드 디스크 저장용 1:3

즉, SSD 배포의 경우 2TB 데이터베이스의 경우 200GB RAM이 필요합니다.

MongoDB 3.0의 WiredTiger 스토리지 엔진에도 동일한 제한 사항이 적용되지만 WiredTiger가 MMAP 스토리지 엔진과 동일한 방식으로 메모리 매핑을 사용하지 않으므로 작업 세트, RAM 및 페이지 장애 간의 상관관계는 그리 강력하지 않습니다.

>[!NOTE]
>
>Adobe에서는 MongoDB 3.0을 사용하는 AEM 6.1 배포용 WiredTiger 스토리지 엔진을 사용하는 것이 좋습니다.

### Data Store {#data-store}

MongoDB 작업 세트 제한 사항으로 인해 데이터 저장소는 MongoDB와 독립적으로 유지하는 것이 좋습니다. 대부분의 환경에서 모든 AEM 인스턴스에서 사용할 수 있는 NAS `FileDataStore` 를 사용해야 합니다. Amazon Web Services가 사용되는 상황에서는 Amazon Web Services도 `S3 DataStore`있습니다. 어떤 이유로든 데이터 저장소가 MongoDB 내에서 유지되는 경우 데이터 저장소의 크기를 총 데이터베이스 크기에 추가해야 하며 작업 집합 계산은 적절하게 조정됩니다. 따라서 페이지 장애 없이 성능을 유지하기 위해 더 많은 RAM을 프로비저닝할 수 있습니다.

## 모니터링 {#monitoring}

성공적인 프로젝트 구현을 위해서는 모니터링을 해야 합니다. 충분한 지식이 있으면 모니터링 없이 MongoDB에서 AEM을 실행할 수 있지만, 이러한 지식은 일반적으로 배포의 각 섹션에 대해 전문 엔지니어에게 제공됩니다.

일반적으로 Apache Oak Core 및 MongoDB 전문가가 작업하는 R&amp;D 엔지니어가 여기에 포함됩니다.

문제를 진단하려면 모든 수준의 세부 코드 베이스에 대한 지식이 필요합니다. 적절한 모니터링과 주요 통계에 대한 적절한 지침을 통해 구현 팀은 예외 항목에 적절히 대응할 수 있습니다.

명령줄 툴을 사용하여 클러스터 작업의 빠른 스냅샷을 얻을 수 있지만 많은 호스트에서 실시간으로 스냅샷을 생성하는 것은 거의 불가능합니다. 명령줄 도구는 몇 분 이상 내역 정보를 제공하지 않으며 서로 다른 유형의 지표 간에 상호 상관 관계를 허용하지 않습니다. 백그라운드 `mongod` 동기화 속도가 느린 짧은 기간 동안 I/O 대기 시간 또는 연결되지 않은 가상 시스템의 공유 스토리지 리소스에 대한 과도한 쓰기 수준의 상관 관계를 유지해야 합니다.

### MongoDB Cloud Manager {#mongodb-cloud-manager}

MongoDB Cloud Manager는 MongoDB 인스턴스를 모니터링하고 관리할 수 있는 MongoDB에서 제공하는 무료 서비스입니다. MongoDB 클러스터의 성능 및 상태를 실시간으로 볼 수 있습니다. 인스턴스가 Cloud Manager 모니터링 서버에 도달할 수 있는 경우 클라우드 및 개인 호스팅 인스턴스를 모두 관리합니다.

모니터링 서버에 연결하는 MongoDB 인스턴스에 에이전트가 설치되어 있어야 합니다. 다음과 같은 세 가지 수준의 에이전트가 있습니다.

* MongoDB 서버의 모든 것을 완벽하게 자동화할 수 있는 자동화 에이전트
* 인스턴스를 모니터링할 수 있는 모니터링 `mongod` 에이전트,
* 데이터의 예약된 백업을 수행할 수 있는 백업 에이전트입니다.

MongoDB 클러스터의 유지 관리 자동화를 위해 Cloud Manager를 사용하더라도 반복적인 작업 중 많은 수가 더 쉬워지고, 필요하지 않으며, 둘 다 백업에 사용하고 있지 않습니다. 모니터링하려면 Cloud Manager를 선택하면 모니터링이 필요합니다.

MongoDB Cloud Manager에 대한 자세한 내용은 MongoDB [설명서를](https://docs.cloud.mongodb.com/)참조하십시오.

### MongoDB Ops Manager {#mongodb-ops-manager}

MongoDB Ops Manager는 MongoDB Cloud Manager와 동일한 소프트웨어입니다. 등록하면 Ops Manager를 개인 데이터 센터나 다른 랩탑 또는 데스크탑 시스템에 로컬로 다운로드하여 설치할 수 있습니다. 로컬 MongoDB 데이터베이스를 사용하여 데이터를 저장하고 관리 대상 서버와 Cloud Manager와 동일한 방식으로 통신합니다. 모니터링 에이전트를 금지하는 보안 정책이 있는 경우 MongoDB Ops Manager를 사용해야 합니다.

### 운영 체제 모니터링 {#operating-system-monitoring}

AEM MongoDB 클러스터를 실행하려면 운영 체제 수준 모니터링이 필요합니다.

Ganglia는 이러한 시스템의 좋은 예이며, CPU, 로드 평균 및 여유 디스크 공간과 같은 기본적인 상태 측정 기준을 넘어서는 필요한 정보의 범위와 세부 정보에 대한 그림을 제공합니다. 문제를 진단하려면 엔트로피 풀 수준, CPU I/O 대기, FIN_WAIT2 상태의 소켓 등과 같은 낮은 수준의 정보가 필요합니다.

### 로그 집계 {#log-aggregation}

여러 서버로 구성된 클러스터를 사용하는 경우 운영 시스템의 경우 중앙 로그 집계가 필요합니다. Splunk와 같은 소프트웨어는 로그 집계를 지원하고 팀이 로그를 수동으로 수집하지 않고도 애플리케이션의 동작 패턴을 분석할 수 있도록 합니다.

## 검사 목록 {#checklists}

이 섹션에서는 프로젝트를 구현하기 전에 AEM 및 MongoDB 배포가 올바르게 설정되도록 하기 위해 수행해야 하는 다양한 단계를 다룹니다.

### 네트워크 {#network}

1. 먼저 모든 호스트에 DNS 항목이 있는지 확인합니다.
1. 모든 호스트는 다른 라우팅 가능한 모든 호스트에서 DNS 항목으로 확인할 수 있어야 합니다.
1. 모든 MongoDB 호스트는 동일한 클러스터의 다른 모든 MongoDB 호스트에서 라우팅할 수 있습니다.
1. MongoDB 호스트는 패킷을 MongoDB Cloud Manager 및 기타 모니터링 서버로 라우팅할 수 있습니다
1. AEM Server는 모든 MongoDB 서버로 패킷을 라우팅할 수 있습니다.
1. 모든 AEM 서버와 MongoDB 서버 간의 패킷 지연은 2밀리초 미만이며 패킷 손실 없이 1밀리초 이하의 표준 배포가 가능합니다.
1. AEM과 MongoDB 서버 사이에 둘 이상의 홉이 없는지 확인합니다.
1. 두 MongoDB 서버 사이에 두 홉이 없습니다.
1. 코어 서버(MongoDB 또는 AEM 또는 조합) 간에 OSI 레벨 3보다 높은 라우터가 없습니다.
1. VLAN 트렁킹 또는 어떤 형태의 네트워크 터널링이 사용되는 경우 패킷 대기 시간 검사를 준수해야 합니다.

### AEM 구성 {#aem-configuration}

#### 노드 저장소 구성 {#node-store-configuration}

AEM 인스턴스는 MongoMK와 함께 AEM을 사용하도록 구성해야 합니다. AEM의 MongoMK 구현의 기반이 문서 노드 저장소입니다.

노드 저장소를 구성하는 방법에 대한 자세한 내용은 AEM의 [노드 저장소 및 데이터 저장소 구성을 참조하십시오](/help/sites-deploying/data-store-config.md).

다음은 최소한의 MongoDB 배포를 위한 Document Node Store 구성의 예입니다.

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
AEM에서 연결해야 하는 MongoDB 서버입니다. 기본 복제본 세트의 알려진 모든 구성원에 연결됩니다. MongoDB 클라우드 관리자를 사용하는 경우 서버 보안이 활성화됩니다. 따라서 연결 문자열에는 적절한 사용자 이름과 암호가 포함되어야 합니다. 비기업 버전의 MongoDB는 사용자 이름 및 암호 인증만 지원합니다. 연결 문자열 구문에 대한 자세한 내용은 [설명서를 참조하십시오](https://docs.mongodb.org/manual/reference/connection-string/).

* `db`
데이터베이스의 이름입니다. AEM의 기본값은 `aem-author`입니다.

* `customBlobStore`
배포가 데이터베이스에 이진 파일을 저장하는 경우 작업 세트의 일부가 됩니다. 따라서 NAS의 데이터 저장소처럼 대체 데이터 저장소를 수행하는 MongoDB 내에 바이너리를 저장하지 않는 것이 좋습니다. `FileSystem`

* `cache`
캐시 크기(MB)입니다. 이는 InDesign에서 사용되는 다양한 캐시 간에 배포됩니다 `DocumentNodeStore`. 기본값은 256MB입니다. 그러나 Oak 읽기 성능은 더 큰 캐시를 통해 이점을 얻을 수 있습니다.

* `blobCacheSize`
AEM에서 자주 사용되는 BLOB를 캐시하여 데이터 저장소에서 리플로우하지 않을 수 있습니다. 이는 특히 MongoDB 데이터베이스에 블로그를 저장할 때 성능에 더 많은 영향을 줍니다. 모든 파일 시스템 기반 데이터 저장소는 운영 체제 수준 디스크 캐시를 통해 이점을 얻을 수 있습니다.

#### 데이터 저장소 구성 {#data-store-configuration}

데이터 저장소는 임계값보다 큰 크기의 파일을 저장하는 데 사용됩니다. 이 임계값 아래로 파일은 Document Node Store 내에 속성으로 저장됩니다. 이 `MongoBlobStore` 속성을 사용하는 경우 MongoDB에서 전용 컬렉션이 생성되어 blob을 저장합니다. 이 컬렉션은 `mongod` 인스턴스의 작업 세트에 기여하며 성능 문제를 방지하기 위해 더 많은 RAM이 `mongod` 필요합니다. 이러한 이유로, 권장 구성은 프로덕션 `MongoBlobStore` 배포 및 모든 AEM 인스턴스 간에 공유된 NAS의 `FileDataStore` 백업 사용을 방지하는 것입니다. 운영 체제 수준 캐시는 파일을 관리하는 데 효율적이기 때문에 디스크의 블록 크기에 가깝게 디스크의 최소 파일 크기를 설정해야 파일 시스템이 효율적으로 사용되고 많은 작은 문서가 `mongod` 인스턴스의 작업 세트에 과도하게 기여하지 않습니다.

다음은 MongoDB를 사용한 최소 AEM 배포를 위한 일반적인 데이터 저장소 구성입니다.

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
크기(바이트)입니다. 이 크기 이하의 바이너리는 문서 노드 저장소에 저장됩니다. blob의 ID를 저장하지 않고 바이너리의 컨텐츠가 저장됩니다. 이 크기보다 큰 바이너리의 경우 바이너리의 ID는 노드 컬렉션에 Document의 속성으로 저장되고 바이너리의 본문은 `FileDataStore` on Disk에 저장됩니다. 4096바이트는 일반적인 파일 시스템 블록 크기입니다.

* `path`
데이터 저장소의 루트에 대한 경로입니다. MongoMK 배포의 경우 모든 AEM 인스턴스에서 사용할 수 있는 공유 파일 시스템이어야 합니다. 일반적으로 NAS(Network Attached Storage) 서버가 사용됩니다. Amazon Web Services와 같은 클라우드 배포의 경우 `S3DataFileStore` 를 사용할 수도 있습니다.

* `cacheSizeInMB`
이진 캐시의 전체 크기(MB)입니다. 이진 파일을 `maxCacheBinarySize` 설정보다 적게 캐시하는 데 사용됩니다.

* `maxCachedBinarySize`
바이너리 캐시에 캐시된 바이너리의 최대 크기(바이트)입니다. 파일 시스템 기반 데이터 저장소를 사용하는 경우 바이너리는 운영 체제에서 이미 캐시되므로 데이터 저장소 캐시에 높은 값을 사용하지 않는 것이 좋습니다.

#### 쿼리 힌트 비활성화 {#disabling-the-query-hint}

속성을 추가하여 모든 쿼리와 함께 전송된 쿼리 힌트를 비활성화하는 것이 좋습니다

`-Doak.mongo.disableIndexHint=true`

aem을 시작할 때 이렇게 하면 MongoDB는 내부 통계를 기반으로 사용할 가장 적합한 색인을 계산합니다.

쿼리 힌트가 비활성화되지 않으면 인덱스의 성능 조정은 AEM 성능에 영향을 주지 않습니다.

#### MongoMK에 대한 영구 캐시 사용 {#enable-persistent-cache-for-mongomk}

OnLocation은 MongoDB 배포에 대해 지속적인 캐시 구성을 사용하는 것이 좋습니다. 따라서 I/O 읽기 성능이 뛰어난 환경에 대한 속도를 최대화할 수 있습니다. 자세한 내용은 Jackrabbit Oak [설명서를](https://jackrabbit.apache.org/oak/docs/nodestore/persistent-cache.html)참조하십시오.

## MongoDB 운영 체제 최적화 {#mongodb-operating-system-optimizations}

### 운영 체제 지원 {#operating-system-support}

MongoDB 2.6은 RAM과 디스크 간의 운영 체제 수준 관리의 일부 측면에 민감한 메모리 매핑 스토리지 엔진을 사용합니다. MongoDB 인스턴스의 쿼리 및 읽기 성능은 종종 페이지 오류라고 하는 느린 입출력 작업을 방지하거나 제거하는데 의존합니다. 특히 프로세스에 적용되는 페이지 `mongod` 오류입니다. 운영 체제 수준 페이지 오류와 혼동하지 마십시오.

빠른 작업을 위해 MongoDB 데이터베이스는 이미 RAM에 있는 데이터만 액세스해야 합니다. 액세스해야 하는 데이터는 인덱스와 데이터로 구성됩니다. 이 인덱스 및 데이터 컬렉션을 작업 집합이라고 합니다. 작업 세트가 사용 가능한 RAM MongoDB보다 큰 경우 I/O 비용이 발생하는 디스크에서 해당 데이터를 페이징하여 메모리에 이미 다른 데이터를 제거합니다. 제거 작업으로 인해 디스크 페이지 오류에서 데이터가 다시 로드되면 성능이 저하됩니다. 작업 세트가 동적 및 변수인 경우 작업을 지원하기 위해 더 많은 페이지 오류가 발생합니다.

MongoDB는 다양한 Linux 버전, Windows 및 Mac OS를 비롯한 다양한 운영 체제에서 실행됩니다. 자세한 [내용은](https://docs.mongodb.com/manual/installation/#supported-platforms) https://docs.mongodb.com/manual/installation/#supported-platforms을 참조하십시오. 운영 체제 선택에 따라 MongoDB의 운영 체제 수준 권장 사항이 다릅니다. 편의를 위해 https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration [에](https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration) 문서화되고 요약되어 있습니다.

#### Linux {#linux}

* 투명한 페이지 및 조각 모음을 끕니다. 자세한 [내용은 투명 큰](https://docs.mongodb.com/manual/tutorial/transparent-huge-pages/) 페이지 설정을 참조하십시오.
* [사용 사례에 맞게 데이터베이스 파일을 저장하는 디바이스에서 미리 보기 설정을](https://docs.mongodb.com/manual/administration/production-notes/#readahead) 조정합니다.

   * MMAPv1 스토리지 엔진의 경우 작업 세트가 사용 가능한 RAM보다 크고 문서 액세스 패턴이 무작위이면 가전을 32 또는 16으로 낮추는 것이 좋습니다. 다른 설정을 평가하여 상주 메모리를 최대화하고 페이지 오류 수를 낮추는 최적의 값을 찾습니다.
   * WiredTiger 스토리지 엔진의 경우 스토리지 미디어 유형(스피닝, SSD 등)에 상관없이 미리 보기를 0으로 설정합니다. 일반적으로, 보다 높은 가독성이 있는 값에서 측정 가능하고 반복 가능하며 안정적인 이점이 없는 한, 권장 가독성 설정을 사용하십시오. [MongoDB Professional](https://docs.mongodb.com/manual/administration/production-notes/#readahead) Support는 사전 설정이 필요 없는 구성에 대한 조언 및 지침을 제공할 수 있습니다.

* 가상 환경에서 RHEL 7/CentOS 7을 실행하는 경우 조정된 도구를 비활성화합니다.
* RHEL 7/CentOS 7이 가상 환경에서 실행될 때, 조정된 도구는 성능 처리량에서 파생된 성능 프로필을 자동으로 불러오며, 이것은 자동으로 가독성 설정을 4MB로 설정합니다. 이는 성능에 부정적인 영향을 줄 수 있습니다.
* SSD 드라이브에 대해 위쪽 또는 최종 디스크 스케줄러를 사용합니다.
* 게스트 VM에서 가상 드라이브를 위한 Noop 디스크 스케줄러 사용
* NUMA를 비활성화하거나 vm.zone_reflecing_mode를 0으로 설정하고 노드 인터리빙을 사용하여 [Mongod](https://docs.mongodb.com/manual/administration/production-notes/#readahead) 인스턴스를 실행합니다. 참조:MongoDB [및 NUMA](https://docs.mongodb.com/manual/administration/production-notes/#readahead) 하드웨어를 참조하십시오.

* 사용 사례에 맞게 하드웨어의 제한 값을 조정합니다. 여러 [번](https://docs.mongodb.com/manual/reference/program/mongod/#bin.mongod) 또는 [몽고](https://docs.mongodb.com/manual/reference/program/mongos/#bin.mongos) 인스턴스가 동일한 사용자 아래에서 실행 중인 경우 그에 따라 ulimit 값을 조정합니다. 참조:UNIX [제한](https://docs.mongodb.com/manual/reference/ulimit/) 설정을 참조하십시오.

* dbPath [마운트 지점에 대한](https://docs.mongodb.com/manual/reference/configuration-options/#storage.dbPath) 이름을 사용합니다.
* 배포에 필요한 충분한 파일 핸들(fs.file-max), 커널 pid 제한(kernel.pid_max) 및 프로세스당 최대 스레드(kernel.threads-max)를 구성합니다. 큰 시스템의 경우 다음 값을 사용하면 좋은 시작점이 됩니다.

   * fs.file-max 값 98000,
   * kernel.pid_max 값: 64000,
   * andkernel.threads-max 값 64000

* 시스템에 스왑 공간이 구성되어 있는지 확인합니다. 적절한 크기에 대한 자세한 내용은 운영 체제 설명서를 참조하십시오.
* 시스템 기본 TCP keepalive가 올바르게 설정되어 있는지 확인합니다. 300 값은 복제본 세트 및 공유 클러스터에 대한 더 나은 성능을 제공하는 경우가 많습니다. 참조:TCP [사용 가능 시간이 MongoDB 배포에 영향을 줍니까?](https://docs.mongodb.com/manual/faq/diagnostics/#faq-keepalive) 를 참조하십시오.

#### Windows {#windows}

* NTFS &quot;마지막 액세스 시간&quot; 업데이트를 비활성화하는 것이 좋습니다. 이는 Unix와 같은 시스템에서 비활성화하는 것과 유사합니다.

### WiredTiger {#wiredtiger}

MongoDB 3.2부터 MongoDB의 기본 스토리지 엔진은 WiredTiger 스토리지 엔진입니다. 이 엔진은 강력하고 확장 가능한 많은 기능을 제공하므로 전반적인 일반 데이터베이스 워크로드에 훨씬 적합합니다. 다음 섹션에서는 이러한 기능에 대해 설명합니다.

#### 문서 수준 동시 사용 {#document-level-concurrency}

WiredTiger는 쓰기 작업을 위해 문서 수준의 동시 시청 제어 기능을 사용합니다. 따라서 여러 클라이언트가 한 컬렉션의 여러 문서를 동시에 수정할 수 있습니다.

대부분의 읽기 및 쓰기 작업을 위해 WiredTiger는 낙관적 동시 시청 제어 기능을 사용합니다. WiredTiger는 전역, 데이터베이스 및 컬렉션 수준에서 의도 잠금만 사용합니다. 스토리지 엔진이 두 작업 간의 충돌을 감지하면 쓰기 충돌이 발생하여 MongoDB가 해당 작업을 투명하게 재시도합니다.일반적으로 여러 데이터베이스를 포함하는 짧은 작업 중 일부 전역 작업은 여전히 전역 &quot;인스턴스 전체&quot; 잠금이 필요합니다.

컬렉션 삭제 등 일부 다른 작업은 여전히 전용 데이터베이스 잠금이 필요합니다.

#### 스냅샷 및 체크포인트 {#snapshots-and-checkpoints}

WiredTiger는 MVCC(MultiVersion Concurrency Control)를 사용합니다. 작업이 시작되면 WiredTiger는 데이터에 대한 트랜잭션 시점 스냅샷을 제공합니다. 스냅샷은 메모리 내 데이터를 일관되게 표시합니다.

WiredTiger는 디스크에 쓸 때 모든 데이터 파일을 일관성 있게 디스크에 기록합니다. 현재 [내구성이](https://docs.mongodb.com/manual/reference/glossary/#term-durable) 있는 데이터는 데이터 파일의 체크포인트 역할을 합니다. 체크포인트는 데이터 파일이 마지막 체크포인트까지 일관되고 포함되도록 합니다.즉, 체크포인트는 복구 포인트로 작동할 수 있습니다.

MongoDB는 60초 또는 2GB의 저널 데이터 간격으로 체크포인트(즉, 디스크에 스냅샷 데이터 쓰기)를 만들도록 WiredTiger를 구성합니다.

새 체크포인트를 쓰는 동안 이전 체크포인트가 여전히 유효합니다. 따라서 MongoDB가 종료되거나 새 체크포인트를 쓰는 동안 오류가 발생하더라도 다시 시작하면 MongoDB가 마지막 유효한 체크포인트에서 복구할 수 있습니다.

WiredTiger의 메타데이터 테이블이 새로운 체크포인트를 참조하도록 자동 업데이트되면 새로운 체크포인트에 액세스하고 영구적으로 액세스할 수 있습니다. 새로운 체크포인트에 액세스하면 WiredTiger는 페이지를 이전 체크포인트에서 해제합니다.

WiredTiger를 사용하면 [저널링](https://docs.mongodb.com/manual/reference/glossary/#term-durable)없이 마지막 체크포인트에서 MongoDB를 복구할 수 있습니다.그러나 마지막 체크포인트 이후 수행된 변경 사항을 복구하려면 [저널링을](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal)사용하여 실행하십시오.

#### 저널 {#journal}

WiredTiger는 [체크포인트와](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-checkpoints) 함께 사전 쓰기 트랜잭션 로그를 사용하여 데이터 내구성을 확인합니다.

WiredTiger 저널은 체크포인트 간 모든 데이터 수정을 유지합니다. MongoDB가 체크포인트 사이에 종료되면 저널을 사용하여 마지막 체크포인트 이후 수정된 모든 데이터를 재생합니다. MongoDB가 저널 데이터를 디스크에 기록하는 빈도에 대한 자세한 내용은 저널링 [프로세스를 참조하십시오](https://docs.mongodb.com/manual/core/journaling/#journal-process).

WiredTiger 저널은 [일관성 있는](https://docs.mongodb.com/manual/core/journaling/#journal-process) 압축 라이브러리를 사용하여 압축됩니다. 대체 압축 알고리즘을 지정하거나 압축을 사용하지 않으려면 [storage.wiredTiger.engineConfig.journalCompressor 설정을](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.journalCompressor) 사용합니다.

자세한 내용은 다음을 참조하십시오.WiredTiger [의 저널링](https://docs.mongodb.com/manual/core/journaling/#journaling-wiredtiger).

>[!NOTE]
>
>WiredTiger의 최소 로그 레코드 크기는 128바이트입니다. 로그 레코드가 128바이트 이하인 경우 WiredTiger는 해당 레코드를 압축하지 않습니다.
>
>저널링 기능을 비활성화하려면 [storage.journal.enabled](https://docs.mongodb.com/manual/reference/configuration-options/#storage.journal.enabled) 를 false로 설정하여 저널링 유지 관리 오버헤드를 줄일 수 있습니다.
>
>독립 [실행형](https://docs.mongodb.com/manual/reference/glossary/#term-standalone) 인스턴스의 경우 저널을 사용하지 않으면 MongoDB가 체크포인트 사이에 예기치 않게 종료될 때 일부 데이터 수정이 손실됩니다. 복제 [세트의](https://docs.mongodb.com/manual/reference/glossary/#term-replica-set)구성원에 대해 복제 프로세스는 충분한 내구성 보장을 제공할 수 있습니다.

#### 압축 {#compression}

WiredTiger를 사용하면 MongoDB는 모든 컬렉션 및 인덱스에 대한 압축을 지원합니다. 압축은 추가 CPU의 비용으로 스토리지 사용을 최소화합니다.

기본적으로 WiredTiger는 모든 컬렉션에 대한 [일관성](https://docs.mongodb.com/manual/reference/glossary/#term-snappy) 압축 라이브러리와 모든 인덱스에 대한 [접두사 압축을](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression) 사용하여 블록 압축을 사용합니다.

컬렉션의 [zlib](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) 블록 압축도 사용할 수 있습니다. 대체 압축 알고리즘을 지정하거나 압축을 사용하지 않으려면 [storage.wiredTiger.collectionConfig.blockCompressor 설정을](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) 사용하십시오.

인덱스의 경우 [prefix 압축을](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression)비활성화하려면 [storage.wiredTiger.indexConfig.prefixCompression](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.indexConfig.prefixCompression) 설정을 사용합니다.

또한 컬렉션 및 색인을 만드는 동안 컬렉션별 및 색인별로 압축 설정을 구성할 수 있습니다. 저장소 [엔진 옵션 지정](https://docs.mongodb.com/manual/reference/method/db.createCollection/#create-collection-storage-engine-options) 및 [db.collection.createIndex() storageEngine](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/#createindex-options) 옵션을 참조하십시오.

대부분의 워크로드에 대해 기본 압축 설정은 저장소 효율성과 처리 요구 사항의 균형을 조정합니다.

WiredTiger 저널은 기본적으로 압축되어 있습니다. 저널 압축에 대한 자세한 내용은 저널을 [참조하십시오](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### 메모리 사용 {#memory-use}

WiredTiger를 사용하는 MongoDB는 WiredTiger 내부 캐시와 파일 시스템 캐시를 모두 사용합니다.

기본적으로 3.4부터 WiredTiger 내부 캐시는 다음 중 큰 것을 사용합니다.

* 50% RAM - 1GB 또는
* 256MB

기본적으로 WiredTiger는 모든 컬렉션에 대해 Snappy 블록 압축을 사용하고 모든 색인에 대해 접두사 압축을 사용합니다. 압축 기본값은 전역 수준에서 구성할 수 있으며 컬렉션 및 색인 작성 동안 컬렉션별 및 인덱스별로 설정할 수도 있습니다.

WiredTiger 내부 캐시에 있는 데이터와 디스크에 있는 포맷의 데이터에 서로 다른 표현이 사용됩니다.

* 파일 시스템 캐시에 있는 데이터는 데이터 파일에 대한 압축을 비롯한 On-Disk 포맷과 동일합니다. 운영 체제에서 디스크 입출력을 줄이기 위해 파일 시스템 캐시를 사용합니다.

WiredTiger 내부 캐시에 로드된 인덱스는 디스크 포맷에 대해 다른 데이터 표현을 가지지만 여전히 인덱스 접두사 압축을 활용하여 RAM 사용을 줄일 수 있습니다.

색인 접두사 압축은 인덱스 필드에서 일반적인 접두사를 중복 제거합니다.

WiredTiger 내부 캐시의 수집 데이터는 압축되지 않고 디스크 상의 형식과 다른 표현을 사용합니다. 블록 압축은 디스크 상의 저장 공간을 크게 절약할 수 있지만 서버가 데이터를 조작하려면 압축하지 않아야 합니다.

파일 시스템 캐시를 통해 MongoDB는 WiredTiger 캐시 또는 다른 프로세스에서 사용되지 않는 모든 여유 메모리를 자동으로 사용합니다.

WiredTiger 내부 캐시 크기를 조정하려면 [storage.wiredTiger.engineConfig.cacheSizeGB 및](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.cacheSizeGB) —wiredTigerCacheSizeGB를 [참조하십시오](https://docs.mongodb.com/manual/reference/program/mongod/#cmdoption-wiredtigercachesizegb). WiredTiger 내부 캐시 크기를 기본값 이상으로 늘리지 마십시오.

### NUMA {#numa}

NUMA(Non Uniform Memory Access)를 사용하면 커널이 메모리를 프로세서 코어에 매핑하는 방식을 관리할 수 있습니다. 이렇게 하면 코어가 필요한 데이터에 액세스할 수 있도록 메모리 액세스를 보다 빠르게 설정하려고 하지만 NUMA는 읽기를 예측할 수 없는 추가 지연을 MMAP에 적용합니다. 따라서 기능이 있는 모든 운영 체제에서 `mongod` 프로세스를 위해 NUMA를 비활성화해야 합니다.

기본적으로 NUMA 아키텍처 메모리는 CPU에 연결되고 CPU는 버스에 연결됩니다. SMP 또는 UMA 아키텍처에서 메모리를 버스에 연결하여 CPU에서 공유합니다. 스레드가 NUMA CPU에 메모리를 할당하면 정책에 따라 메모리를 할당합니다. 기본값은 사용 가능한 공간이 없는 한 스레드의 로컬 CPU에 연결된 메모리를 할당하여 사용 가능한 CPU의 메모리를 더 높은 비용으로 사용합니다. 할당된 메모리는 CPU 간에 이동하지 않습니다. 할당은 상위 스레드에서 상속된 정책에 의해 수행되며, 이는 궁극적으로 프로세스를 시작한 스레드입니다.

시스템을 다중 코어 동일 메모리 아키텍처로 보는 많은 데이터베이스에서, 이 경우 초기 CPU가 먼저 가득 차며, 특히 중앙 스레드가 메모리 버퍼를 할당해야 하는 경우 나중에 보조 CPU가 채워집니다. 솔루션은 `mongod` 프로세스를 시작하는 데 사용되는 기본 스레드의 NUMA 정책을 변경하는 것입니다.

이 작업은 다음 명령을 실행하여 수행할 수 있습니다.

```shell
numactl --interleaved=all <mongod> -f config
```

이 정책은 모든 CPU 노드에 대해 메모리를 라운드 로빈 방식으로 할당하므로 모든 노드에 균등하게 배포됩니다. 다중 CPU 하드웨어가 장착된 시스템처럼 메모리에 대한 최고 성능 액세스를 생성할 수 없습니다. 메모리 작업 중 약 절반이 버스를 통해 느려지지만 최적의 방식으로 NUMA를 타겟팅하도록 `mongod` 작성되지 않았으므로 합리적인 타협이 가능합니다.

### NUMA 문제 {#numa-issues}

이 `mongod` 프로세스가 `/etc/init.d` 폴더 이외의 위치에서 시작된 경우 올바른 NUMA 정책으로 시작하지 않을 수 있습니다. 기본 정책이 무엇인지에 따라 문제가 발생할 수 있습니다. 이것은 MongoDB용 다양한 Linux 패키지 관리자 설치 프로그램이 위에 설명된 단계를 수행하는 구성 파일이 있는 서비스를 설치할 `/etc/init.d` 수도 있기 때문입니다. 아카이브( `.tar.gz`)에서 직접 MongoDB를 설치하고 실행하는 경우 `numactl` 프로세스에서 수동으로 실행해야 합니다.

>[!NOTE]
>
>사용 가능한 NUMA 정책에 대한 자세한 내용은 [숫자 설명서를](https://linux.die.net/man/8/numactl)참조하십시오.

MongoDB 프로세스는 다른 할당 정책에 따라 다르게 동작합니다.

```

```

* `-membind=<nodes>`
나열된 노드에만 할당합니다. Mongod는 나열된 노드에 메모리를 할당하지 않으며 사용 가능한 메모리를 모두 사용하지 않을 수 있습니다.

* `-cpunodebind=<nodes>`
노드에서만 실행합니다. Mongod는 지정된 노드에서만 실행되며 해당 노드에서만 사용할 수 있는 메모리만 사용합니다.

* `-physcpubind=<nodes>`
나열된 CPU(코어)에서만 실행됩니다. Mongod는 나열된 CPU에서만 실행되고 해당 CPU에서 사용할 수 있는 메모리만 사용합니다.

* `--localalloc`
항상 현재 노드에 메모리를 할당하지만 스레드가 실행되는 모든 노드를 사용합니다. 한 스레드에서 할당을 수행하면 해당 CPU에 사용할 수 있는 메모리만 사용됩니다.

* `--preferred=<node>`
노드보다 할당을 선호하지만 기본 노드가 가득 찬 경우 다른 사람에게 다시 할당됩니다. 노드 정의에 대한 상대 표기법을 사용할 수 있습니다. 또한 스레드가 모든 노드에서 실행됩니다.

정책 중 일부는 `mongod` 프로세스에 제공되는 모든 RAM보다 적을 수 있습니다. MySQL과 달리 MongoDB는 운영 체제 수준 페이징을 적극적으로 방지하므로, 결과적으로 사용 가능한 것으로 보이는 메모리 양이 줄어들 수 있습니다. `mongod`

#### 교환 {#swapping}

데이터베이스의 메모리 집약적인 특성으로 인해 운영 체제 레벨 스와핑을 사용하지 않도록 설정해야 합니다. MongoDB 프로세스는 디자인별로 교환하지 않습니다.

#### 원격 파일 시스템 {#remote-filesystems}

NFS와 같은 원격 파일 시스템은 MongoDB의 내부 데이터 파일(Mongod 프로세스 데이터베이스 파일)에 너무 많은 지연을 발생시키므로 권장되지 않습니다. NFS가 권장되는 Oak Blob(FileDataStore)의 스토리지에 필요한 공유 파일 시스템과 혼동하지 마십시오.

#### 미리 보기 {#read-ahead}

임의 읽기를 사용하여 페이지를 페이징할 때 불필요한 블록을 디스크에서 읽을 수 없으므로 I/O 대역폭이 불필요한 상태로 소비되도록 미리 보기를 조정해야 합니다.

### Linux 요구 사항 {#linux-requirements}

#### 최소 커널 버전 {#minimum-kernel-versions}

* **2.6.23** `ext4` 파일 시스템의 경우

* **2.6.25** ( `xfs` 파일 시스템)

#### 데이터베이스 디스크에 대한 권장 설정 {#recommended-settings-for-database-disks}

**작업 끄기**

데이터베이스를 포함할 디스크에 대해 `atime` 비활성화하는 것이 좋습니다.

**NOOP 디스크 스케줄러 설정**

다음을 통해 이 작업을 수행할 수 있습니다.

먼저 현재 설정된 입출력 스케줄러를 선택합니다. 이 작업은 다음 명령을 실행하여 수행할 수 있습니다.

```shell
cat /sys/block/sdg/queue/scheduler
```

응답이 `noop` 있으면 더 이상 할 필요가 없습니다.

NOOP가 설정된 입출력 스케줄러가 아닌 경우 다음을 실행하여 변경할 수 있습니다.

```shell
echo noop > /sys/block/sdg/queue/scheduler
```

**미리 보기 값 조정**

MongoDB 데이터베이스가 실행되는 디스크에 32의 값을 사용하는 것이 좋습니다. 이것은 16킬로바이트에 해당한다. 다음을 실행하여 설정할 수 있습니다.

```shell
sudo blockdev --setra <value> <device>
```

#### NTP 활성화 {#enable-ntp}

MongoDB 데이터베이스를 호스팅하는 컴퓨터에 NTP가 설치되어 실행되고 있는지 확인합니다. 예를 들어 CentOS 컴퓨터에서 yum 패키지 관리자를 사용하여 설치할 수 있습니다.

```shell
sudo yum install ntp
```

NTP 데몬이 설치되고 성공적으로 시작되면 서버의 시간 오프셋을 위해 드리프트 파일을 확인할 수 있습니다.

#### 투명 큰 페이지 비활성화 {#disable-transparent-huge-pages}

Red Hat Linux는 THP(Transparent Huge Pages)라는 메모리 관리 알고리즘을 사용합니다. 데이터베이스 워크로드에 운영 체제를 사용하는 경우 비활성화하는 것이 좋습니다.

아래 절차에 따라 비활성화할 수 있습니다.

1. 원하는 텍스트 편집기에서 파일을 엽니다 `/etc/grub.conf` .
1. grub.conf 파일에 다음 줄을 추가합니다.

   ```xml
   transparent_hugepage=never
   ```

1. 마지막으로 다음을 실행하여 설정이 적용되었는지 확인합니다.

   ```shell
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   THP가 비활성화된 경우 위 명령의 출력은 다음과 같아야 합니다.

   ```xml
   always madvise [never]
   ```

>[!NOTE]
>
>투명한 대형 페이지에 대한 자세한 내용은 이 [문서를](https://access.redhat.com/solutions/46111)참조하십시오.

#### NUMA 비활성화 {#disable-numa}

NUMA가 활성화된 대부분의 설치에서 MongoDB 데몬은 `/etc/init.d` 폴더에서 서비스로 실행되면 자동으로 비활성화됩니다.

이 경우 프로세스당 수준에서 NUMA를 비활성화할 수 있습니다. 비활성화하려면 다음 명령을 실행합니다.

```shell
numactl --interleave=all <path_to_process>
```

몬신 `<path_to_process>` 과정의 경로는 어디입니까?

그런 다음 다음을 실행하여 영역 재사용을 비활성화합니다.

```shell
echo 0 > /proc/sys/vm/zone_reclaim_mode
```

#### 모신 프로세스에 대한 제한 설정 조정 {#tweak-the-ulimit-settings-for-the-mongod-process}

Linux에서는 `ulimit` 명령을 통해 리소스 할당을 구성 가능한 방식으로 제어할 수 있습니다. 이 작업은 사용자 또는 프로세스별로 수행할 수 있습니다.

MongoDB 권장 제한 설정에 따라 통화 프로세스에 대한 [제한을 구성하는 것이 좋습니다](https://docs.mongodb.org/manual/reference/ulimit/#recommended-ulimit-settings).

#### MongoDB I/O 성능 테스트 {#test-mongodb-i-o-performance}

MongoDB는 I/O 성능을 테스트하도록 설계된 `mongoperf` 도구를 제공합니다. 인프라를 구성하는 모든 MongoDB 인스턴스의 성능을 테스트하는 데 사용하는 것이 좋습니다.

사용 방법에 대한 자세한 내용은 `mongoperf`MongoDB [설명서를](https://docs.mongodb.org/manual/reference/program/mongoperf/)참조하십시오.

>[!NOTE]
>
>이 `mongoperf` 기능은 실행되는 플랫폼에서 MongoDB 성능을 나타내는 표시기로 설계되었습니다. 이로 인해, 결과는 생산 시스템의 성능에 대한 최종적인 것으로 간주되어서는 안 됩니다.
>
>보다 정확한 성능 결과를 얻으려면 Linux 툴을 사용하여 보완 테스트를 실행할 수 `fio` 있습니다.

**배포를 구성하는 가상 시스템에서 읽기 성능 테스트**

도구를 설치한 후 테스트를 실행하기 위해 MongoDB 데이터베이스 디렉토리로 전환합니다. 그런 다음 이 `mongoperf`구성으로 첫 번째 테스트를 시작합니다.

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true}" | mongoperf
```

원하는 출력은 모든 MongoDB 인스턴스에 대해 32개의 스레드에서 실행되는 초당 최대 2GB(2GB/s) 및 500.000 IOPS에 도달해야 합니다.

이번에는 `mmf:true` 매개 변수를 설정하여 메모리 매핑 파일을 사용하여 두 번째 테스트를 실행합니다.

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true,mmf:true}" | mongoperf
```

두 번째 테스트의 출력은 메모리 전송 성능을 나타내는 첫 번째 테스트보다 상당히 높아야 합니다.

>[!NOTE]
>
>테스트를 수행할 때 운영 체제 모니터링 시스템의 해당 가상 컴퓨터에 대한 I/O 사용량 통계를 확인하십시오. 입출력 읽기 값이 100% 미만인 경우 가상 시스템에 문제가 있을 수 있습니다.

**기본 MongoDB 인스턴스의 쓰기 성능 테스트**

그런 다음 동일한 설정으로 MongoDB 데이터베이스 디렉토리에서 실행하여 기본 MongoDB 인스턴스의 I/O 쓰기 성능을 `mongoperf` 확인합니다.

```shell
echo "{nThreads:32,fileSizeMB:1000,w:true}" | mongoperf
```

원하는 출력은 초당 12MB이며 3000 IOPS에 도달해야 하며 스레드 수는 거의 변하지 않습니다.

## 가상화 환경을 위한 단계 {#steps-for-virtualised-environments}

### VMWare {#vmware}

WMWare ESX를 사용하여 가상화된 환경을 관리 및 배포하는 경우 ESX 콘솔에서 다음 설정을 수행하여 MongoDB 작업을 수용할 수 있습니다.

1. 메모리 열기구 끄기
1. MongoDB 데이터베이스를 호스팅할 가상 컴퓨터에 대한 메모리 사전 할당 및 예약
1. 스토리지 입출력 제어를 사용하여 `mongod` 프로세스에 충분한 입출력을 할당할 수 있습니다.
1. CPU 예약 설정을 통해 MongoDB를 호스팅하는 시스템의 CPU [리소스 보장](https://pubs.vmware.com/vsphere-4-esx-vcenter/index.jsp?topic=/com.vmware.vsphere.vmadmin.doc_41/vsp_vm_guide/configuring_virtual_machines/t_allocate_cpu_resources.html)

1. ParaVirtual I/O 드라이버를 사용하는 것이 좋습니다. 이 방법에 대한 자세한 내용은 이 [기술 자료를](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=1010398)참조하십시오.

### Amazon Web Services {#amazon-web-services}

Amazon Web Services를 사용하여 MongoDB를 설정하는 방법에 대한 설명서는 MongoDB 웹 사이트에서 [AWS 통합](https://docs.cloud.mongodb.com/tutorial/configure-aws-settings/) 구성 문서를 참조하십시오.

## 배포 전 MongoDB 보안 {#securing-mongodb-before-deployment}

배포하기 전에 데이터베이스의 구성을 보호하는 방법에 대한 자세한 내용은 [MongoDB를](https://blogs.adobe.com/security/2015/07/securely-deploying-mongodb-3-0.html) 안전하게 배포하는 이 게시물을 참조하십시오.

## Dispatcher {#dispatcher}

### 발송자용 운영 체제 선택 {#choosing-the-operating-system-for-the-dispatcher}

MongoDB 배포를 제대로 사용하려면 디스패처를 호스팅하는 운영 체제에서 Apache httpd **버전 2.** 4 **이상을 실행해야 합니다.**

또한 보안 문제를 최소화하기 위해 빌드에 사용된 모든 라이브러리가 최신 상태로 유지되는지 확인하십시오.

### Dispatcher Configuration {#dispatcher-configuration}

일반적인 디스패처 구성은 단일 AEM 인스턴스의 요청 처리량을 10배에서 20배 더 많이 제공합니다.

Dispatcher는 주로 상태 비저장 장치이므로 손쉽게 가로로 확장할 수 있습니다. 일부 배포에서는 작성자가 특정 리소스에 액세스하지 못하도록 제한해야 합니다. 따라서 작성자 인스턴스와 함께 디스패처를 사용하는 것이 좋습니다.

디스패처 없이 AEM을 실행하려면 다른 애플리케이션에서 SSL 종료 및 로드 밸런싱을 수행해야 합니다. 이는 세션이 만들어진 AEM 인스턴스와 관련성이 있어야 하기 때문에 필요합니다. 고정 연결이라고 하는 개념입니다. 이 방법은 컨텐츠 업데이트가 지연 시간을 최소화하도록 하기 위한 것입니다.

구성 [방법에 대한 자세한 내용은 Dispatcher 설명서를](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) 참조하십시오.

### 추가 구성 {#additional-configuration}

#### 고정 연결 {#sticky-connections}

고정 연결을 통해 한 사용자에 대한 개인화된 페이지와 세션 데이터가 모두 동일한 AEM 인스턴스에서 작성되도록 할 수 있습니다. 이 데이터는 인스턴스에 저장되므로 동일한 사용자의 후속 요청은 동일한 인스턴스로 반환됩니다.

모든 내부 레이어 라우팅 요청에 대해 AEM 인스턴스로 고정 연결을 활성화하여 후속 요청이 동일한 AEM 인스턴스에 도달하도록 하는 것이 좋습니다. 이렇게 하면 인스턴스 간에 컨텐츠가 업데이트될 때 감지되는 지연을 최소화할 수 있습니다.

#### 긴 만료 {#long-expires}

기본적으로 AEM 디스패처에서 발송된 컨텐츠에는 컨텐츠 만료의 표시가 없는 마지막 수정 및 태그 머리글이 있습니다. 이렇게 하면 사용자 인터페이스가 항상 최신 버전의 리소스를 얻을 수 있지만, 이는 브라우저가 리소스가 변경되었는지 확인하기 위해 GET 작업을 수행한다는 것을 의미합니다. 이로 인해 페이지 로드에 따라 HTTP 응답이 304(수정되지 않음)인 여러 요청이 발생할 수 있습니다. 만료되지 않는 것으로 알려진 리소스의 경우 만료일 헤더를 설정하고 마지막으로 수정한 날짜 및 ETag 헤더를 제거하면 콘텐츠가 캐시되고 만료일 헤더의 날짜가 충족될 때까지 추가 업데이트 요청이 수행되지 않습니다.

그러나 이 방법을 사용하면 만료 헤더가 만료되기 전에 브라우저에서 리소스가 만료되도록 하는 합리적인 방법이 없음을 의미합니다. 이를 줄이기 위해 HtmlClientLibraryManager를 클라이언트 라이브러리에 대해 변경할 수 없는 URL을 사용하도록 구성할 수 있습니다.

이러한 URL은 변경되지 않습니다. URL에 포함된 리소스의 본문이 변경되면 브라우저가 리소스의 올바른 버전을 요청하도록 URL에 변경 내용이 자동으로 반영됩니다.

기본 구성은 선택기를 HtmlClientLibraryManager에 추가합니다. 선택기가 되면 리소스가 디스패처에 캐시되고 선택기는 그대로 유지됩니다. 또한 이 선택기를 사용하여 올바른 만료 동작을 보장할 수 있습니다. 기본 선택기는 `lc-.*?-lc` 패턴을 따릅니다. 다음 Apache httpd 구성 지시문은 해당 패턴과 일치하는 모든 요청이 적절한 만료 시간과 함께 제공되도록 합니다.

```xml
Header set Expires "Tue, 20 Jan 2037 04:20:42 GMT" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header set Cache-Control "public, no-transform, max-age=267840000" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset ETag "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Last-Modified "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Pragma "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
```

#### Sniff 없음 {#no-sniff}

컨텐츠 유형 없이 컨텐츠를 전송하는 경우 많은 브라우저에서는 컨텐츠의 처음 몇 바이트를 읽음으로써 컨텐츠의 유형을 추측하려고 시도합니다. 이를 &quot;snipping&quot;이라고 합니다. 저장소에 쓸 수 있는 사용자가 컨텐츠 유형이 없는 악성 컨텐츠를 업로드할 수 있으므로 Snipping은 보안 취약점을 엽니다.

이러한 이유로 디스패처가 제공하는 리소스에 `no-sniff` 헤더를 추가하는 것이 좋습니다. 그러나 디스패처는 헤더를 캐시하지 않습니다. 즉, 로컬 파일 시스템에서 제공되는 모든 컨텐츠는 AEM 원본 서버에서 원본 컨텐츠 유형 헤더를 사용하지 않고 확장명으로 결정된 컨텐츠 유형을 갖게 됩니다.

웹 응용 프로그램이 파일 형식 없이 캐시된 리소스를 제공하지 않는 것으로 알려진 경우 Sniff를 안전하게 활성화할 수 없습니다.

다음을 포괄적으로 스프라이드 없음을 활성화할 수 있습니다.

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

#### 콘텐츠 보안 정책 {#content-security-policy}

기본 디스패처 설정은 CSP라고도 하는 개방형 컨텐츠 보안 정책을 허용합니다. 이렇게 하면 페이지가 브라우저 샌드박스의 기본 정책을 따르는 모든 도메인의 리소스를 로드할 수 있습니다.

신뢰할 수 없거나 확인되지 않은 외부 서버에서 JavaScript 엔진에 코드를 로드하지 않도록 리소스를 로드할 수 있는 위치를 제한하는 것이 좋습니다.

CSP를 사용하면 정책을 세밀하게 조정할 수 있습니다. 그러나 복잡한 응용 프로그램 CSP 헤더는 너무 제한적인 정책이 사용자 인터페이스의 일부분을 손상시킬 수 있으므로 주의하여 개발해야 합니다.

>[!NOTE]
>
>이 작동 방법에 대한 자세한 내용은 Content Security [정책의 OWASP 페이지를 참조하십시오](https://www.owasp.org/index.php/Content_Security_Policy).

### 크기 조정 {#sizing}

크기 조정에 대한 자세한 내용은 하드웨어 [크기 조정 지침을 참조하십시오](/help/managing/hardware-sizing-guidelines.md).

### MongoDB 성능 최적화 {#mongodb-performance-optimization}

MongoDB 성능에 대한 일반 정보는 MongoDB [성능 분석을 참조하십시오](https://docs.mongodb.org/manual/administration/analyzing-mongodb-performance/).

## 알려진 제한 사항 {#known-limitations}

### 동시 설치 {#concurrent-installations}

단일 데이터베이스를 가진 여러 AEM 인스턴스를 동시에 사용하는 것은 MongoMK에서 지원되지만 동시 설치는 지원되지 않습니다.

이 문제를 해결하려면 먼저 단일 구성원을 사용하여 설치를 실행하고 설치를 완료한 후 다른 구성원을 추가하십시오.

### 페이지 이름 길이 {#page-name-length}

If AEM is running on a MongoMK persistence manager deployment, [page names are limited to 150 characters.](/help/sites-authoring/managing-pages.md)

>[!NOTE]
>
>[MongoDB 설명서의](https://docs.mongodb.com/manual/reference/limits/) 알려진 제한 사항과 MongoDB 자체에 대한 임계값에 대해 잘 알고 계시기 바랍니다.

