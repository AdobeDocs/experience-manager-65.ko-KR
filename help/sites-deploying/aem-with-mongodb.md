---
title: Adobe Experience Manager 및 MongoDB
description: MongoDB를 사용한 Adobe Experience Manager의 성공적인 배포에 필요한 작업 및 고려 사항에 대해 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
exl-id: 70a39462-8584-4c76-a097-05ee436247b7
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: 8f638eb384bdca59fb6f4f8990643e64f34622ce
workflow-type: tm+mt
source-wordcount: '6216'
ht-degree: 0%

---

# Adobe Experience Manager 및 MongoDB{#aem-with-mongodb}

이 문서에서는 MongoDB와 함께 AEM(Adobe Experience Manager)를 성공적으로 배포하는 데 필요한 작업 및 고려 사항에 대한 지식을 향상하고자 합니다.

배포와 관련된 자세한 내용은 설명서의 [배포 및 유지 관리](/help/sites-deploying/deploy.md) 섹션을 참조하십시오.

## AEM에서 MongoDB를 사용해야 하는 경우 {#when-to-use-mongodb-with-aem}

MongoDB는 일반적으로 다음 기준 중 하나가 충족되는 AEM 작성자 배포를 지원하는 데 사용됩니다.

* 하루에 1000명 이상의 고유 사용자
* 100명 이상의 동시 사용자
* 대량의 페이지 편집
* 대규모 롤아웃 또는 활성화.

위의 기준은 작성자 인스턴스용일 뿐이며 TarMK 기반이어야 하는 모든 게시 인스턴스에 대한 것은 아닙니다. 작성자 인스턴스는 인증되지 않은 액세스를 허용하지 않으므로 사용자 수는 인증된 사용자를 참조합니다.

기준을 충족하지 않으면 가용성을 해결하기 위해 TarMK 활성/대기 배포를 사용하는 것이 좋습니다. 일반적으로 MongoDB는 단일 하드웨어 항목으로 확장 요구 사항을 달성할 수 있는 것보다 더 많은 상황에서 고려되어야 합니다.

>[!NOTE]
>
>작성자 인스턴스 크기 조정 및 동시 사용자 정의에 대한 추가 정보는 [하드웨어 크기 조정 지침](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel)에서 찾을 수 있습니다.

### AEM용 MongoDB 배포 최소화 {#minimal-mongodb-deployment-for-aem}

다음은 MongoDB의 AEM에 대한 최소 배포입니다. 간소화를 위해 SSL 종료 및 HTTP 프록시 구성 요소가 일반화되었습니다. MongoDB 복제본 세트 하나로 구성되며, 기본 복제본 세트와 보조 복제본 세트 두 개가 있습니다.

![chlimage_1-4](assets/chlimage_1-4.png)

최소 배포에는 복제본 집합으로 구성된 `mongod` 인스턴스 3개가 필요합니다. 한 인스턴스는 기본 인스턴스로, 다른 인스턴스는 보조 인스턴스로, 선택은 `mongod`에서 관리합니다. 각 인스턴스에 로컬 디스크가 연결되어 있습니다. 따라서 클러스터가 로드를 지원할 수 있으므로 최소 처리량은 초당 12MB이며 초당 3000회 이상의 입출력 작업(IOPS)을 수행하는 것이 좋습니다.

AEM 작성자는 `mongod` 인스턴스에 연결되고 각 AEM 작성자는 세 개의 `mongod` 인스턴스에 모두 연결됩니다. 쓰기 작업은 운영 시스템으로 전송되며 읽기는 모든 인스턴스에서 읽을 수 있습니다. 트래픽은 Dispatcher에 의한 로드를 기반으로 활성 AEM 작성자 인스턴스 중 하나로 분산됩니다. Oak 데이터 저장소는 `FileDataStore`이며 MongoDB 모니터링은 배포 위치에 따라 MMS 또는 MongoDB Ops Manager에서 제공합니다. 운영 체제 수준 및 로그 모니터링은 Splunk 또는 Ganglia와 같은 타사 솔루션에서 제공합니다.

이 배포에서는 성공적인 구현을 위해 모든 구성 요소가 필요합니다. 누락된 구성 요소는 구현을 작동하지 않습니다.

### 운영 체제 {#operating-systems}

AEM 6에서 지원되는 운영 체제 목록은 [기술 요구 사항 페이지](/help/sites-deploying/technical-requirements.md)를 참조하십시오.

### 환경 {#environments}

프로젝트를 실행하는 여러 기술 팀 간에 원활한 의사 소통이 이루어지는 경우 가상화 환경이 지원됩니다. 이 지원에는 AEM을 실행하는 팀, 운영 체제를 사용하는 팀 및 가상 인프라를 관리하는 팀이 포함됩니다.

가상화 환경을 관리하는 팀이 관리해야 하는 MongoDB 인스턴스의 I/O 용량에 대한 특정 요구 사항이 있습니다. 프로젝트에서 Amazon Web Services과 같은 클라우드 배포를 사용하는 경우 MongoDB 인스턴스를 지원하려면 충분한 I/O 용량과 일관성으로 인스턴스를 프로비저닝해야 합니다. 그렇지 않으면 MongoDB 프로세스 및 Oak 저장소가 불안정하고 비정상적으로 수행합니다.

가상화된 환경에서 MongoDB의 스토리지 엔진이 VMWare 리소스 할당 정책에 의해 손상되지 않도록 하려면 MongoDB는 특정 I/O 및 VM 구성이 필요합니다. 성공적인 구현은 다양한 팀 사이에 장벽을 없애고 모든 팀이 필요한 성능을 제공하기 위해 등록하도록 보장합니다.

## 하드웨어 고려 사항 {#hardware-considerations}

### 스토리지 {#storage}

MongoDB는 일반적으로 SSD 스토리지 또는 SSD와 동등한 성능을 갖춘 스토리지를 필요로 하지 않고 최상의 성능을 제공하기 위해 읽기 및 쓰기 처리량을 구현합니다.

### RAM {#ram}

MMAP 스토리지 엔진을 사용하는 MongoDB 버전 2.6 및 3.0을 사용하려면 데이터베이스 및 해당 인덱스의 작업 집합이 RAM에 적합해야 합니다.

RAM이 부족하면 성능이 크게 저하됩니다. 작업 집합 및 데이터베이스의 크기는 응용 프로그램에 따라 크게 달라집니다. 몇 가지 예상이 가능하지만 필요한 RAM의 양을 결정하는 가장 안정적인 방법은 AEM 애플리케이션을 빌드하고 부하 테스트하는 것입니다.

로드 테스트 프로세스를 지원하기 위해 전체 데이터베이스 크기에 대한 작업 집합의 비율을 다음과 같이 가정할 수 있습니다.

* SSD 스토리지용 1:10
* 하드 디스크 스토리지용 1:3

이러한 비율은 SSD 배포의 경우 2TB 데이터베이스에 200GB의 RAM이 필요함을 의미합니다.

MongoDB 3.0의 WiredTiger 스토리지 엔진에도 동일한 제한 사항이 적용되지만 작업 세트, RAM 및 페이지 폴트 간의 상관 관계는 그리 강력하지 않습니다. WiredTiger는 MMAP 스토리지 엔진과 동일한 방식으로 메모리 매핑을 사용하지 않습니다.

>[!NOTE]
>
>Adobe에서는 MongoDB 3.0을 사용하는 AEM 6.1 배포에 WiredTiger 스토리지 엔진을 사용하는 것이 좋습니다.

### 데이터 저장소 {#data-store}

MongoDB 작업 세트 제한 사항으로 인해 데이터 저장소는 MongoDB와 독립적으로 유지되는 것이 좋습니다. 대부분의 환경에서는 모든 AEM 인스턴스에서 사용할 수 있는 NAS를 사용하는 `FileDataStore`을(를) 사용해야 합니다. Amazon Web Services을 사용하는 상황의 경우 `S3 DataStore`도 있습니다. 어떤 이유로든 데이터 저장소는 MongoDB 내에서 유지되며, 데이터 저장소의 크기를 전체 데이터베이스 크기에 추가하고, 작업 집합 계산을 적절히 조정해야 합니다. 이 크기 조정은 페이지 오류 없이 성능을 유지하기 위해 더 많은 RAM을 프로비저닝하는 것을 의미할 수 있습니다.

## 모니터링 {#monitoring}

프로젝트의 성공적인 구현을 위해서는 모니터링이 필수적이다. 충분한 지식이 있으면 모니터링 없이 MongoDB에서 AEM을 실행할 수 있습니다. 그러나 이러한 지식은 일반적으로 배포의 각 섹션에 특화된 엔지니어에서 발견됩니다.

이 전문 지식에는 일반적으로 Apache Oak Core에서 근무하는 R&amp;D 엔지니어와 MongoDB 전문가가 포함됩니다.

모든 수준에서 모니터링하지 않으면 문제를 진단하기 위해 코드 베이스에 대한 자세한 지식이 필요합니다. 적절한 모니터링과 주요 통계에 대한 적절한 지침을 통해 구현 팀은 예외 항목에 적절히 대응할 수 있습니다.

명령줄 도구를 사용하여 클러스터 작업에 대한 빠른 스냅샷을 얻을 수 있지만 많은 호스트에서 실시간으로 수행하는 것은 거의 불가능합니다. 명령줄 도구는 몇 분 이상의 내역 정보를 제공하는 경우가 거의 없으며 서로 다른 유형의 지표 간에 상호 연관성을 허용하지 않습니다. 느린 백그라운드 `mongod` 동기화 기간이 짧으면 I/O 대기 또는 연결되지 않은 가상 컴퓨터의 공유 저장소 리소스에 대한 과도한 쓰기 수준과 상관 관계를 맺기 위해 상당한 수작업이 필요합니다.

### MongoDB Cloud Manager {#mongodb-cloud-manager}

MongoDB Cloud Manager은 MongoDB가 제공하는 무료 서비스로 MongoDB 인스턴스의 모니터링과 관리가 가능하다. MongoDB 클러스터의 성능과 상태를 실시간으로 확인할 수 있습니다. 인스턴스가 Cloud Manager 모니터링 서버에 도달할 수 있는 경우 클라우드와 비공개 호스팅 인스턴스를 모두 관리합니다.

모니터링 서버에 연결하는 MongoDB 인스턴스에 에이전트가 설치되어 있어야 합니다. 세 가지 수준의 에이전트가 있습니다.

* MongoDB 서버의 모든 것을 완전히 자동화할 수 있는 자동화 에이전트,
* `mongod` 인스턴스를 모니터링할 수 있는 모니터링 에이전트입니다.
* 데이터의 스케줄 지정 백업을 수행할 수 있는 백업 에이전트입니다.

Cloud Manager을 MongoDB 클러스터의 유지 관리 자동화에 사용하면 많은 일상적인 작업이 더 쉬워지지만 필요하지 않으며 둘 다 백업에 사용하지 않습니다. 모니터링할 Cloud Manager을 선택할 때는 모니터링이 필요합니다.

MongoDB Cloud Manager에 대한 자세한 내용은 [MongoDB 설명서](https://docs.cloud.mongodb.com/)를 참조하세요.

### MongoDB 운영 관리자 {#mongodb-ops-manager}

MongoDB Ops Manager는 MongoDB Cloud Manager과 동일한 소프트웨어입니다. 등록되면 Ops Manager를 로컬로 다운로드하여 개인 데이터 센터 또는 기타 랩톱 또는 데스크톱 시스템에 설치할 수 있습니다. 로컬 MongoDB 데이터베이스를 사용하여 데이터를 저장하고 관리되는 서버와 Cloud Manager과 동일한 방식으로 통신합니다. 모니터링 에이전트를 금지하는 보안 정책이 있는 경우 MongoDB Ops Manager를 사용해야 합니다.

### 운영 체제 모니터링 {#operating-system-monitoring}

AEM MongoDB 클러스터를 실행하려면 운영 체제 수준 모니터링이 필요합니다.

Ganglia는 이러한 시스템의 좋은 예이며 CPU, 로드 평균 및 사용 가능한 디스크 공간과 같은 기본 상태 지표를 뛰어넘는 필요한 정보의 범위와 세부 정보를 제공합니다. 문제를 진단하려면 엔트로피 풀 수준, CPU I/O 대기, FIN_WAIT2 상태의 소켓과 같은 하위 수준 정보가 필요합니다.

### 로그 집계 {#log-aggregation}

여러 서버로 구성된 클러스터에서 중앙 로그 집선은 운영 시스템의 요구 사항입니다. Splunk과 같은 소프트웨어는 로그 집계를 지원하고 팀이 로그를 수동으로 수집하지 않고도 애플리케이션의 동작 패턴을 분석할 수 있도록 합니다.

## 체크리스트 {#checklists}

이 섹션에서는 프로젝트를 구현하기 전에 AEM 및 MongoDB 배포가 제대로 설정되었는지 확인하기 위해 수행해야 하는 다양한 단계를 설명합니다.

### 네트워크 {#network}

1. 먼저 모든 호스트에 DNS 항목이 있는지 확인합니다.
1. 모든 호스트는 라우팅 가능한 다른 모든 호스트의 DNS 항목으로 확인할 수 있어야 합니다.
1. 모든 MongoDB 호스트는 동일한 클러스터의 다른 모든 MongoDB 호스트에서 라우팅할 수 있습니다
1. MongoDB 호스트는 MongoDB Cloud Manager 및 다른 모니터링 서버로 패킷을 라우팅할 수 있습니다
1. AEM 서버는 모든 MongoDB 서버로 패킷을 라우팅할 수 있습니다
1. AEM 서버와 MongoDB 서버 간의 패킷 지연 시간은 2밀리초 미만이며 패킷 손실이 없으며 표준 분포는 1밀리초 이하입니다.
1. AEM과 MongoDB 서버 간에 최대 2개의 홉이 있는지 확인합니다.
1. MongoDB 서버 두 대 사이에는 두 개 이상의 홉이 없습니다
1. 코어 서버(MongoDB 또는 AEM 또는 그 조합) 간에 OSI 레벨 3보다 높은 라우터가 없습니다.
1. VLAN 트렁킹 또는 모든 형태의 네트워크 터널링을 사용하는 경우 패킷 지연 검사를 준수해야 합니다.

### AEM 구성 {#aem-configuration}

#### 노드 저장소 구성 {#node-store-configuration}

AEM 인스턴스는 MongoMK와 함께 AEM을 사용하도록 구성해야 합니다. AEM에서 MongoMK 구현의 기본은 문서 노드 저장소입니다.

노드 저장소를 구성하는 방법에 대한 자세한 내용은 [AEM에서 노드 저장소 및 데이터 저장소 구성](/help/sites-deploying/data-store-config.md)을 참조하십시오.

다음은 최소 MongoDB 배포에 대한 문서 노드 저장소 구성의 예입니다.

```xml
# org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config
#MongoDB server details
mongodburi=mongodb://aem:aempassword@mongodbserver1.customer.com:27000,mongodbserver2.customer.com:27000

#Name of MongoDB database to use
db=aem

#Store binaries in custom BlobStore for example, FileDataStore
customBlobStore=true

cache=2048
blobCacheSize=1024
```

위치:

* `mongodburi`
MongoDB 서버 AEM이에 연결해야 합니다. 기본 복제 데이터베이스 집합의 알려진 모든 구성원에 연결됩니다. MongoDB Cloud Manager을 사용하는 경우 서버 보안이 활성화됩니다. 따라서 연결 문자열에는 적절한 사용자 이름과 암호가 포함되어야 합니다. 엔터프라이즈 버전이 아닌 MongoDB는 사용자 이름 및 암호 인증만 지원합니다. 연결 문자열 구문에 대한 자세한 내용은 [설명서](https://docs.mongodb.org/manual/reference/connection-string/)를 참조하세요.

* `db`
데이터베이스의 이름입니다. AEM 기본값은 `aem-author`입니다.

* `customBlobStore`
배포가 데이터베이스에 바이너리를 저장하는 경우 이 바이너리는 작업 세트의 일부를 형성합니다. 이러한 이유로 NAS의 `FileSystem` 데이터 저장소와 같은 대체 데이터 저장소를 선호하여 MongoDB 내에 바이너리를 저장하지 않는 것이 좋습니다.

* `cache`
캐시 크기(MB)입니다. 이 공간은 `DocumentNodeStore`에서 사용되는 다양한 캐시에 분산됩니다. 기본값은 256MB입니다. 그러나 Oak은 캐시가 커지면 읽기 성능이 향상됩니다.

* `blobCacheSize`
자주 사용되는 블롭은 데이터 저장소에서 다시 식각되지 않도록 AEM에 의해 캐시될 수 있습니다. 이렇게 하면 특히 MongoDB 데이터베이스에 Blob을 저장할 때 성능에 더 많은 영향을 줍니다. 모든 파일 시스템 기반 데이터 저장소는 운영 체제 수준의 디스크 캐시를 통해 이점을 얻을 수 있습니다.

#### 데이터 저장소 구성 {#data-store-configuration}

데이터 저장소는 임계값보다 큰 크기의 파일을 저장하는 데 사용됩니다. 이 임계값보다 낮으면 파일이 문서 노드 저장소 내에 속성으로 저장됩니다. `MongoBlobStore`을(를) 사용하면 MongoDB에 전용 컬렉션을 만들어 BLOB를 저장합니다. 이 컬렉션은 `mongod` 인스턴스의 작업 집합에 기여하므로 성능 문제를 방지하려면 `mongod`에 더 많은 RAM이 있어야 합니다. 따라서 프로덕션 배포에 대해 `MongoBlobStore`을(를) 피하고 모든 AEM 인스턴스 간에 공유된 NAS에서 지원하는 `FileDataStore`을(를) 사용하는 것이 좋습니다. 운영 체제 수준 캐시는 파일 관리에 효율적이므로 디스크에 있는 파일의 최소 크기를 디스크의 블록 크기에 가깝게 설정해야 합니다. 이렇게 하면 파일 시스템을 효율적으로 사용할 수 있으며, 많은 작은 문서가 `mongod` 인스턴스의 작업 집합에 과도하게 기여하지 않습니다.

다음은 MongoDB를 사용하는 최소 AEM 배포를 위한 일반적인 데이터 저장소 구성입니다.

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
크기(바이트)입니다. 이 크기보다 작거나 같은 바이너리는 문서 노드 저장소와 함께 저장됩니다. Blob의 ID를 저장하는 대신, 바이너리의 콘텐츠가 저장됩니다. 이 크기보다 큰 바이너리를 사용하면 바이너리의 ID가 노드 컬렉션에 Document의 속성으로 저장됩니다. 그리고 바이너리의 본문은 디스크의 `FileDataStore`에 저장됩니다. 4096바이트는 일반적인 파일 시스템 블록 크기입니다.

* `path`
데이터 저장소의 루트에 대한 경로입니다. MongoMK 배포의 경우 이 경로는 모든 AEM 인스턴스에서 사용할 수 있는 공유 파일 시스템이어야 합니다. 일반적으로 NAS(Network Attached Storage) 서버가 사용됩니다. Amazon Web Services과 같은 클라우드 배포의 경우 `S3DataFileStore`도 사용할 수 있습니다.

* `cacheSizeInMB`
이진 캐시의 총 크기(MB)입니다. `maxCacheBinarySize` 설정보다 적은 바이너리를 캐시하는 데 사용됩니다.

* `maxCachedBinarySize`
이진 캐시에 캐시된 이진의 최대 크기(바이트)입니다. 파일 시스템 기반 데이터 저장소를 사용하는 경우 운영 체제에 의해 바이너리가 이미 캐시되므로 데이터 저장소 캐시에 높은 값을 사용하지 않는 것이 좋습니다.

#### 쿼리 힌트 비활성화 {#disabling-the-query-hint}

AEM을 시작할 때 `-Doak.mongo.disableIndexHint=true` 속성을 추가하여 모든 쿼리와 함께 전송된 쿼리 힌트를 비활성화하는 것이 좋습니다. 이렇게 하면 MongoDB가 내부 통계를 기반으로 사용할 가장 적절한 색인을 계산합니다.

쿼리 힌트를 비활성화하지 않으면 인덱스 성능 튜닝이 AEM 성능에 영향을 주지 않습니다.

#### MongoMK에 대한 영구 캐시 활성화 {#enable-persistent-cache-for-mongomk}

MongoDB 배포에 대해 영구 캐시 구성을 활성화하여 I/O 읽기 성능이 높은 환경의 속도를 최대화하는 것이 좋습니다. 자세한 내용은 [Jackrabbit Oak 설명서](https://jackrabbit.apache.org/oak/docs/nodestore/persistent-cache.html)를 참조하세요.

## MongoDB 운영 체제 최적화 {#mongodb-operating-system-optimizations}

### 운영 체제 지원 {#operating-system-support}

MongoDB 2.6은 RAM과 디스크 간의 운영 체제 수준 관리에 민감한 메모리 매핑 스토리지 엔진을 사용합니다. MongoDB 인스턴스의 쿼리 및 읽기 성능은 종종 페이지 오류라고 하는 느린 I/O 작업을 방지하거나 제거하는 데 의존합니다. 이러한 문제는 특히 `mongod` 프로세스에 적용되는 페이지 오류입니다. 이를 운영 체제 수준의 페이지 오류와 혼동하지 마십시오.

빠른 작업을 위해 MongoDB 데이터베이스는 이미 RAM에 있는 데이터에만 액세스해야 합니다. 액세스해야 하는 데이터는 인덱스 및 데이터로 구성됩니다. 이러한 인덱스 및 데이터 컬렉션을 작업 세트라고 합니다. 작업 세트가 사용 가능한 RAM MongoDB보다 큰 경우 디스크에서 해당 데이터를 페이징해야 I/O 비용이 발생하여 메모리에 이미 있는 다른 데이터를 제거할 수 있습니다. 데이터가 디스크에서 다시 로드되는 경우 페이지 장애가 우세하고 성능이 저하됩니다. 작업 세트가 동적이고 가변적인 경우 작업을 지원하기 위해 더 많은 페이지 오류가 발생합니다.

MongoDB는 다양한 Linux® 버전, Windows 및 macOS을 포함한 여러 운영 체제에서 실행됩니다. 자세한 내용은 [https://docs.mongodb.com/manual/installation/#supported-platforms](https://docs.mongodb.com/manual/installation/#supported-platforms)을(를) 참조하십시오. 선택한 운영 체제에 따라 MongoDB에는 다른 운영 체제 수준의 권장 사항이 있습니다. [https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration](https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration)에 문서화되어 있으며 편의상 여기에 요약되어 있습니다.

#### Linux® {#linux}

* 투명 조각 및 조각 모음을 끕니다. 자세한 내용은 [투명 대용량 페이지 설정](https://docs.mongodb.com/manual/tutorial/transparent-huge-pages/)을 참조하십시오.
* 사용 사례에 맞게 데이터베이스 파일을 저장하는 장치에서 [미리 보기 설정을 조정](https://docs.mongodb.com/manual/administration/production-notes/#readahead)합니다.

   * MMAPv1 스토리지 엔진의 경우 작업 집합이 사용 가능한 RAM보다 크고 문서 액세스 패턴이 임의인 경우 미리 보기를 32 또는 16으로 낮추는 것이 좋습니다. 다른 설정을 평가하여 상주 메모리를 최대화하고 페이지 폴트 수를 낮추는 최적의 값을 찾을 수 있습니다.
   * WiredTiger 스토리지 엔진의 경우 저장 매체 유형(회전, SSD 등)에 관계없이 readahead를 0으로 설정합니다. 일반적으로, 테스트에서 더 높은 미리 읽기 가치에서 측정 가능하고 반복 가능하며 신뢰할 수 있는 이점을 표시하지 않는 한 권장되는 미리 읽기 설정을 사용하십시오. [MongoDB Professional 지원](https://docs.mongodb.com/manual/administration/production-notes/#readahead)에서 0이 아닌 미리 읽기 구성에 대한 조언과 지침을 제공할 수 있습니다.

* 가상 환경에서 RHEL 7/CentOS 7을 실행하는 경우 튜닝된 도구를 비활성화합니다.
* 가상 환경에서 RHEL 7/CentOS 7을 실행하면 튜닝된 툴이 자동으로 성능 처리량에서 파생된 성능 프로필을 호출하여 미리 보기 설정을 4MB로 자동 설정합니다. 이 설정은 성능에 부정적인 영향을 줄 수 있습니다.
* SSD 드라이브용 noop 또는 최종 기한 디스크 스케줄러를 사용하십시오.
* 게스트 VM의 가상 드라이브에 대해 noop 디스크 스케줄러를 사용합니다.
* NUMA를 사용하지 않도록 설정하거나 `vm.zone_reclaim_mode`을(를) 0으로 설정하고 노드 인터리빙으로 [mongod](https://docs.mongodb.com/manual/administration/production-notes/#readahead) 인스턴스를 실행합니다. 자세한 내용은 [MongoDB 및 NUMA 하드웨어](https://docs.mongodb.com/manual/administration/production-notes/#readahead)를 참조하십시오.

* 사용 사례에 맞게 하드웨어의 제한 값을 조정합니다. 여러 [mongod](https://docs.mongodb.com/manual/reference/program/mongod/#bin.mongod) 또는 [mongos](https://docs.mongodb.com/manual/reference/program/mongos/#bin.mongos) 인스턴스가 동일한 사용자에서 실행 중인 경우 그에 따라 ulimit 값의 크기를 조정하십시오. 자세한 내용은 [UNIX® 제한 설정](https://docs.mongodb.com/manual/reference/ulimit/)을 참조하십시오.

* [dbPath](https://docs.mongodb.com/manual/reference/configuration-options/#storage.dbPath) 탑재 지점에 대해 noatime을 사용하십시오.
* 배포에 필요한 충분한 파일 핸들(fs.file-max), 커널 pid 제한(kernel.pid_max) 및 프로세스당 최대 스레드(kernel.threads-max)를 구성합니다. 대규모 시스템의 경우 다음 값이 좋은 시작점을 제공합니다.

   * fs.file-max 값 98000,
   * kernel.pid_max 값 64000,
   * andkernel.threads-최대 64000 값

* 시스템에 스왑 공간이 구성되어 있는지 확인합니다. 적절한 크기 조정에 대한 자세한 내용은 운영 체제의 설명서를 참조하십시오.
* 시스템 기본 TCP keepalive가 올바르게 설정되어 있는지 확인합니다. 값이 300이면 복제본 세트 및 공유 클러스터에 대해 성능이 향상되는 경우가 많습니다. [TCP keepalive 시간이 MongoDB 배포에 영향을 줍니까?자세한 내용은 FAQ의 &#x200B;](https://docs.mongodb.com/manual/faq/diagnostics/#faq-keepalive)을(를) 참조하십시오.

#### Windows {#windows}

* NTFS &quot;마지막 액세스 시간&quot; 업데이트를 사용하지 않도록 설정하십시오. 이 설정은 Unix 유사 시스템에서 atime을 비활성화하는 것과 유사합니다.

### 와이어드타이거 {#wiredtiger}

MongoDB 3.2부터 MongoDB의 기본 스토리지 엔진은 WiredTiger 스토리지 엔진입니다. 이 엔진은 강력하고 확장 가능한 기능을 제공하므로 전반적인 일반 데이터베이스 워크로드에 훨씬 적합합니다. 다음 섹션에서는 이러한 기능에 대해 설명합니다.

#### 문서 수준 동시 실행 {#document-level-concurrency}

WiredTiger는 쓰기 작업을 위해 문서 수준의 동시성 제어를 사용합니다. 따라서 여러 클라이언트가 컬렉션의 서로 다른 문서를 동시에 수정할 수 있습니다.

대부분의 읽기 및 쓰기 작업에서 WiredTiger는 낙관적인 동시성 제어를 사용합니다. WiredTiger는 글로벌, 데이터베이스 및 수집 수준에서 의도 잠금만 사용합니다. 스토리지 엔진이 두 작업 간의 충돌을 감지하면 쓰기 충돌이 발생하여 MongoDB가 해당 작업을 투명하게 다시 시도합니다. 일반적으로 여러 데이터베이스를 포함하는 단기 작업인 일부 글로벌 작업은 여전히 글로벌 &quot;인스턴스 전체&quot; 잠금이 필요합니다.

컬렉션 삭제와 같은 다른 일부 작업에는 전용 데이터베이스 잠금이 필요합니다.

#### 스냅샷 및 체크포인트 {#snapshots-and-checkpoints}

WiredTiger는 MVCC(MultiVersion Concurrency Control)를 사용합니다. 작업을 시작하면 WiredTiger는 데이터의 시점 스냅샷을 트랜잭션에 제공합니다. 스냅샷은 메모리 내 데이터의 일관된 보기를 제공합니다.

디스크에 쓸 때 WiredTiger는 스냅샷의 모든 데이터를 모든 데이터 파일에서 일관된 방식으로 디스크에 기록합니다. 이제- [지속형](https://docs.mongodb.com/manual/reference/glossary/#term-durable) 데이터는 데이터 파일에서 검사점 역할을 합니다. 체크포인트는 데이터 파일이 마지막 체크포인트를 포함하여 최신 상태로 일관되도록 합니다. 즉, 체크포인트가 복구 지점 역할을 할 수 있습니다.

MongoDB는 60초 또는 2GB의 저널 데이터 간격으로 체크포인트를 생성(즉, 스냅샷 데이터를 디스크에 쓰기)하도록 WiredTiger를 구성합니다.

새 체크포인트를 작성하는 동안 이전 체크포인트는 여전히 유효합니다. 따라서 MongoDB가 종료되거나 새 체크포인트를 작성하는 동안 오류가 발생하더라도 재시작 시 MongoDB는 마지막으로 유효한 체크포인트에서 복구할 수 있습니다.

WiredTiger의 메타데이터 테이블이 새 체크포인트를 참조하도록 자동으로 업데이트되면 새 체크포인트에 액세스하고 영구적으로 유지됩니다. 새 체크포인트에 액세스하면 WiredTiger는 이전 체크포인트에서 페이지를 해제합니다.

WiredTiger를 사용하면 [저널링](https://docs.mongodb.com/manual/reference/glossary/#term-durable)이 없어도 MongoDB는 마지막 체크포인트에서 복구할 수 있습니다. 그러나 마지막 체크포인트 이후에 변경된 내용을 복구하려면 [저널링](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal)을 사용하여 실행하십시오.

#### 저널 {#journal}

WiredTiger는 데이터 내구성을 보장하기 위해 [체크포인트](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-checkpoints)와 함께 미리 쓰기 트랜잭션 로그온 조합을 사용합니다.

WiredTiger 저널은 체크포인트 간에 모든 데이터 수정 사항을 유지합니다. MongoDB가 체크포인트 사이에 종료되면 저널을 사용하여 마지막 체크포인트 이후 수정된 모든 데이터를 재생합니다. MongoDB가 저널 데이터를 디스크에 쓰는 빈도에 대한 자세한 내용은 [저널링 프로세스](https://docs.mongodb.com/manual/core/journaling/#journal-process)를 참조하십시오.

WiredTiger 저널은 [snappy](https://docs.mongodb.com/manual/core/journaling/#journal-process) 압축 라이브러리를 사용하여 압축됩니다. 대체 압축 알고리즘을 지정하거나 압축을 해제하려면 [storage.wiredTiger.engineConfig.journalCompressor](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.journalCompressor) 설정을 사용하십시오.

[WiredTiger로 저널링](https://docs.mongodb.com/manual/core/journaling/#journaling-wiredtiger)을 참조하십시오.

>[!NOTE]
>
>WiredTiger의 최소 로그 레코드 크기는 128바이트입니다. 로그 레코드가 128바이트 이하이면 WiredTiger는 해당 레코드를 압축하지 않습니다.
>
>[storage.journal.enabled](https://docs.mongodb.com/manual/reference/configuration-options/#storage.journal.enabled)을(를) false로 설정하여 저널링을 비활성화할 수 있으므로 저널 유지 관리 오버헤드가 줄어들 수 있습니다.
>
>[독립 실행형](https://docs.mongodb.com/manual/reference/glossary/#term-standalone) 인스턴스의 경우 저널을 사용하지 않으면 MongoDB가 체크포인트 사이에 예기치 않게 종료될 때 일부 데이터 수정 사항이 손실됩니다. [복제본 집합](https://docs.mongodb.com/manual/reference/glossary/#term-replica-set)의 구성원의 경우 복제 프로세스를 통해 충분한 내구성을 보장할 수 있습니다.

#### 압축 {#compression}

MongoDB는 WiredTiger를 사용하여 모든 컬렉션 및 인덱스에 대한 압축을 지원합니다. 압축은 추가 CPU을 희생하여 스토리지 사용을 최소화합니다.

기본적으로 WiredTiger는 모든 컬렉션에 대해 [snappy](https://docs.mongodb.com/manual/reference/glossary/#term-snappy) 압축 라이브러리와 함께 블록 압축을 사용하고 모든 인덱스에 대해 [접두사 압축](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression)을 사용합니다.

컬렉션의 경우 [zlib](https://docs.mongodb.com/manual/reference/glossary/#term-zlib)을(를) 사용한 블록 압축도 사용할 수 있습니다. 대체 압축 알고리즘을 지정하거나 압축을 해제하려면 [storage.wiredTiger.collectionConfig.blockCompressor](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) 설정을 사용하십시오.

인덱스의 경우 [접두사 압축](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression)을 비활성화하려면 [storage.wiredTiger.indexConfig.prefixCompression](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.indexConfig.prefixCompression) 설정을 사용하십시오.

압축 설정은 또한 수집 및 색인 생성 중 수집 및 색인 단위로 구성할 수 있습니다. [저장소 엔진 옵션 지정](https://docs.mongodb.com/manual/reference/method/db.createCollection/#create-collection-storage-engine-options) 및 [db.collection.createIndex() storageEngine](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/#createindex-options) 옵션을 참조하십시오.

대부분의 워크로드에서 기본 압축 설정은 스토리지 효율성과 처리 요구 사항의 균형을 유지합니다.

또한 WiredTiger 저널은 기본적으로 압축되어 있습니다. 저널 압축에 대한 자세한 내용은 [저널](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal)을 참조하세요.

#### 메모리 사용 {#memory-use}

MongoDB는 WiredTiger를 사용하여 WiredTiger 내부 캐시와 파일 시스템 캐시를 모두 사용합니다.

3.4부터 WiredTiger 내부 캐시는 기본적으로 다음 중 큰 것을 사용합니다.

* RAM의 50% - 1GB 또는
* 256메가바이트

기본적으로 WiredTiger는 모든 컬렉션에 대해 스냅 블록 압축을 사용하고 모든 인덱스에 대해 접두사 압축을 사용합니다. 압축 기본값은 글로벌 수준에서 구성할 수 있으며, 수집 및 색인 생성 중에 수집 및 색인별로 설정할 수도 있습니다.

다른 표현은 On-Disk 포맷과 WiredTiger 내부 캐시의 데이터에 사용됩니다.

* 파일 시스템 캐시의 데이터는 디스크 상의 포맷과 동일하며 데이터 파일에 대한 압축의 이점도 포함됩니다. 운영 체제에서 디스크 I/O를 줄이기 위해 파일 시스템 캐시를 사용합니다.

WiredTiger 내부 캐시에 로드된 인덱스의 데이터 표현은 디스크 포맷과 다르지만 인덱스 접두사 압축을 사용하여 RAM 사용을 줄일 수 있습니다.

인덱스 접두사 압축은 인덱싱된 필드에서 일반 접두사를 중복 제거합니다.

WiredTiger 내부 캐시의 컬렉션 데이터는 압축되어 있지 않으며 디스크 형식과는 다른 표현을 사용합니다. 블록 압축을 사용하면 디스크 상의 스토리지 용량을 크게 절약할 수 있지만 서버에서 데이터를 조작하려면 압축이 해제되어야 합니다.

파일 시스템 캐시를 통해 MongoDB는 WiredTiger 캐시 또는 다른 프로세스에서 사용하지 않는 모든 사용 가능한 메모리를 자동으로 사용합니다.

WiredTiger 내부 캐시의 크기를 조정하려면 [storage.wiredTiger.engineConfig.cacheSizeGB](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.cacheSizeGB) 및 [—wiredTigerCacheSizeGB](https://docs.mongodb.com/manual/reference/program/mongod/#cmdoption-wiredtigercachesizegb)을(를) 참조하십시오. WiredTiger 내부 캐시 크기를 기본값 이상으로 늘리지 마십시오.

### 누마 {#numa}

NUMA(Non-Uniform Memory Access)를 사용하면 커널이 프로세서 코어에 메모리를 매핑하는 방법을 관리할 수 있습니다. 이 프로세스는 코어가 필요한 데이터에 액세스할 수 있도록 메모리 액세스를 더 빠르게 만들려고 시도하지만 NUMA는 읽기를 예측할 수 없어 추가적인 지연을 초래하는 MMAP을 방해합니다. 따라서 모든 운영 체제에서 `mongod` 프로세스에 대해 NUMA를 사용하지 않도록 설정해야 합니다.

본질적으로, NUMA 아키텍처에서 메모리는 CPU에 연결되고, CPU는 버스에 연결된다. SMP 또는 UMA 아키텍처에서 메모리는 버스에 연결되고 CPU에 의해 공유된다. 스레드는 NUMA CPU에 메모리를 할당할 때 정책에 따라 할당합니다. 기본적으로 스레드의 로컬 CPU에 연결된 메모리는 사용 가능한 공간이 없는 한 할당하는 것입니다. 이 시점에서 더 높은 비용으로 사용 가능한 CPU의 메모리를 사용합니다. 일단 할당되면, 메모리는 CPU들 사이에서 이동하지 않는다. 할당은 상위 스레드에서 상속된 정책에 의해 수행되며, 상위 스레드는 궁극적으로 프로세스를 시작한 스레드입니다.

컴퓨터를 멀티코어 균일 메모리 아키텍처로 보는 많은 데이터베이스에서 이 시나리오는 먼저 CPU이 가득 차고 나중에 보조 CPU이 채워지는 것으로 이어집니다. 특히 중앙 스레드가 메모리 버퍼를 할당하는 경우 더욱 그렇습니다. 해결 방법은 다음 명령을 실행하여 `mongod` 프로세스를 시작하는 데 사용되는 기본 스레드의 NUMA 정책을 변경하는 것입니다.

```shell
numactl --interleaved=all <mongod> -f config
```

이 정책은 모든 CPU 노드에 대해 메모리를 라운드 로빈 방식으로 할당하여 모든 노드에 대해 균등한 분배를 보장합니다. 여러 CPU 하드웨어가 있는 시스템에서처럼 메모리에 대한 최고의 성능 액세스를 생성하지 않습니다. 메모리 작업의 약 절반이 느리고 버스를 사용하지만 `mongod`이(가) 최적의 방법으로 NUMA를 대상으로 작성되지 않았으므로 적절한 절충안입니다.

### NUMA 문제 {#numa-issues}

`mongod` 프로세스가 `/etc/init.d` 폴더 이외의 위치에서 시작된 경우 올바른 NUMA 정책으로 시작되지 않았을 수 있습니다. 디폴트 정책이 무엇인지에 따라 문제가 발생할 수 있다. 그 이유는 MongoDB의 다양한 Linux® Package Manager 설치 프로그램이 위에 설명된 단계를 수행하는 `/etc/init.d`에 구성 파일이 있는 서비스를 설치하기 때문입니다. 아카이브(`.tar.gz`)에서 직접 MongoDB를 설치하여 실행하는 경우 `numactl` 프로세스에서 Mongod를 수동으로 실행해야 합니다.

>[!NOTE]
>
>사용 가능한 NUMA 정책에 대한 자세한 내용은 [numactl 설명서](https://linux.die.net/man/8/numactl)를 참조하세요.

MongoDB 프로세스는 서로 다른 할당 정책에 따라 다르게 동작합니다.

```

```

* `-membind=<nodes>`
나열된 노드에만 할당합니다. Mongod는 나열된 노드에 메모리를 할당하지 않으며 사용 가능한 모든 메모리를 사용하지 않을 수 있습니다.

* `-cpunodebind=<nodes>`
노드에서만 실행합니다. Mongod는 지정된 노드에서만 실행되며 해당 노드에서 사용 가능한 메모리만 사용합니다.

* `-physcpubind=<nodes>`
나열된 CPU(코어)에서만 실행됩니다. Mongod는 나열된 CPU에서만 실행되며 해당 CPU에서 사용 가능한 메모리만 사용합니다.

* `--localalloc`
항상 현재 노드에 메모리를 할당하지만 스레드가 실행되는 모든 노드를 사용하십시오. 하나의 스레드가 할당을 수행하는 경우 해당 CPU에서 사용할 수 있는 메모리만 사용됩니다.

* `--preferred=<node>`
노드보다 할당을 선호하지만, 기본 설정 노드가 가득 찬 경우 다른 노드보다 폴백됩니다. 노드를 정의하기 위한 상대 표기법(relative notation)이 사용될 수 있다. 또한 스레드는 모든 노드에서 실행됩니다.

일부 정책으로 인해 `mongod` 프로세스에 사용 가능한 RAM이 모두 제공되지 않을 수 있습니다. MySQL과 달리 MongoDB는 운영 체제 수준 페이징을 적극적으로 사용하지 않으므로 `mongod` 프로세스에서 사용 가능한 메모리를 줄일 수 있습니다.

#### 스와핑 {#swapping}

데이터베이스의 메모리 집약적 특성으로 인해 운영 체제 수준 스와핑을 비활성화해야 합니다. MongoDB 프로세스는 디자인으로 인한 스와핑을 방지합니다.

#### 원격 파일 시스템 {#remote-filesystems}

MongoDB의 내부 데이터 파일(Mongod 프로세스 데이터베이스 파일)은 지연 시간이 너무 길기 때문에 NFS와 같은 원격 파일 시스템은 사용하지 않는 것이 좋습니다. NFS가 권장되는 Oak Blob(FileDataStore)의 스토리지에 필요한 공유 파일 시스템과 혼동하지 마십시오.

#### 미리 읽기 {#read-ahead}

임의 읽기를 사용하여 페이지가 페이징될 때 디스크에서 불필요한 블록을 읽지 않도록 미리 읽기 조정 이러한 결과는 불필요한 I/O 대역폭 소비를 의미합니다.

### Linux® 요구 사항 {#linux-requirements}

#### 최소 커널 버전 {#minimum-kernel-versions}

* `ext4` 파일 시스템용 **2.6.23**

* `xfs` 파일 시스템용 **2.6.25**

#### 데이터베이스 디스크에 대한 권장 설정 {#recommended-settings-for-database-disks}

**시간 끄기**

데이터베이스가 포함된 디스크에 대해 `atime`을(를) 사용하지 않도록 설정하는 것이 좋습니다.

**NOOP 디스크 스케줄러 설정**

다음 작업을 수행합니다.

먼저 다음 명령을 실행하여 설정된 I/O 스케줄러를 확인합니다.

```shell
cat /sys/block/sdg/queue/scheduler
```

응답이 `noop`이면 더 이상 수행할 작업이 없습니다.

NOOP가 설정된 I/O 스케줄러가 아닌 경우 다음을 실행하여 변경할 수 있습니다.

```shell
echo noop > /sys/block/sdg/queue/scheduler
```

**미리 읽기 값 조정**

MongoDB 데이터베이스가 실행되는 디스크에는 32 값을 사용하는 것이 좋습니다. 이 값은 16KB입니다. 다음을 실행하여 설정할 수 있습니다.

```shell
sudo blockdev --setra <value> <device>
```

#### NTP 활성화 {#enable-ntp}

MongoDB 데이터베이스를 호스팅하는 시스템에 NTP가 설치되어 실행 중인지 확인하십시오. 예를 들어 CentOS 컴퓨터에서 yum 패키지 관리자를 사용하여 설치할 수 있습니다.

```shell
sudo yum install ntp
```

NTP 데몬이 설치되고 성공적으로 시작되면 서버의 시간 오프셋에 대한 드리프트 파일을 확인할 수 있습니다.

#### 투명한 대용량 페이지 비활성화 {#disable-transparent-huge-pages}

Red Hat® Linux®는 THP(Transparent Huge Pages)라는 메모리 관리 알고리즘을 사용합니다. 데이터베이스 워크로드에 운영 체제를 사용하는 경우 비활성화하는 것이 좋습니다.

아래 절차에 따라 비활성화할 수 있습니다.

1. 선택한 텍스트 편집기에서 `/etc/grub.conf` 파일을 엽니다.
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
>투명 대용량 페이지에 대한 자세한 내용은 Red Hat® 고객 포털에서 다음 문서를 참조하십시오. [Red Hat Enterprise Linux 6, 7 및 8에서 투명 Hugepage를 사용, 모니터링 및 비활성화하는 방법](https://access.redhat.com/solutions/46111)

#### NUMA 비활성화 {#disable-numa}

NUMA가 활성화된 대부분의 설치에서는 MongoDB 데몬이 `/etc/init.d` 폴더에서 서비스로 실행되는 경우 이 데몬을 자동으로 사용하지 않도록 설정합니다.

그렇지 않은 경우 프로세스 수준별로 NUMA를 비활성화할 수 있습니다. 비활성화하려면 다음 명령을 실행합니다.

```shell
numactl --interleave=all <path_to_process>
```

여기서 `<path_to_process>`은(는) Mongod 프로세스의 경로입니다.

그런 다음 다음을 실행하여 영역 재확보를 비활성화합니다.

```shell
echo 0 > /proc/sys/vm/zone_reclaim_mode
```

#### Mongod 프로세스에 대한 제한 설정 수정 {#tweak-the-ulimit-settings-for-the-mongod-process}

Linux®를 사용하면 `ulimit` 명령을 통해 리소스 할당을 구성 가능한 방식으로 제어할 수 있습니다. 이 구성은 사용자 또는 프로세스별로 수행될 수 있습니다.

[MongoDB 권장 제한 설정](https://docs.mongodb.org/manual/reference/ulimit/#recommended-ulimit-settings)에 따라 Mongod 프로세스에 대한 제한 설정을 구성하는 것이 좋습니다.

#### MongoDB I/O 성능 테스트 {#test-mongodb-i-o-performance}

MongoDB는 I/O 성능을 테스트하도록 설계된 `mongoperf` 도구를 제공합니다. 인프라를 구성하는 모든 MongoDB 인스턴스의 성능을 테스트하는 데 사용하는 것이 좋습니다.

`mongoperf`을(를) 사용하는 방법에 대한 자세한 내용은 [MongoDB 설명서](https://docs.mongodb.org/manual/reference/program/mongoperf/)를 참조하세요.

>[!NOTE]
>
>`mongoperf`은(는) 실행 중인 플랫폼에서 MongoDB 성능을 나타냅니다. 결과적으로, 결과는 생산 시스템의 성능에 대한 결정적인 것으로 간주되어서는 안 된다.
>
>보다 정확한 성능 결과를 위해 `fio` Linux® 도구를 사용하여 보완 테스트를 실행할 수 있습니다.

**배포를 구성하는 가상 컴퓨터에서 읽기 성능을 테스트합니다**

도구를 설치한 후 MongoDB 데이터베이스 디렉터리로 전환하여 테스트를 실행합니다. 그런 다음 이 구성으로 `mongoperf`을(를) 실행하여 첫 번째 테스트를 시작합니다.

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true}" | mongoperf
```

원하는 출력은 모든 MongoDB 인스턴스에 대해 32개 스레드에서 실행되는 초당 최대 2GB(2GB/s) 및 500.000 IOPS에 도달해야 합니다.

이번에는 `mmf:true` 매개 변수를 설정하여 메모리 매핑 파일을 사용하여 두 번째 테스트를 실행하십시오.

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true,mmf:true}" | mongoperf
```

제2 테스트의 출력은 제1 테스트보다 상당히 높아야 하며, 이는 메모리 전송 성능을 나타낸다.

>[!NOTE]
>
>테스트를 수행할 때 운영 체제 모니터링 시스템에서 해당 가상 시스템에 대한 I/O 사용 통계를 확인합니다. 입출력 읽기에 대해 100%보다 낮은 값을 표시하는 경우 가상 시스템에 문제가 있을 수 있습니다.

**기본 MongoDB 인스턴스의 쓰기 성능을 테스트합니다**

그런 다음 동일한 설정으로 MongoDB 데이터베이스 디렉터리에서 `mongoperf`을(를) 실행하여 기본 MongoDB 인스턴스의 I/O 쓰기 성능을 확인합니다.

```shell
echo "{nThreads:32,fileSizeMB:1000,w:true}" | mongoperf
```

원하는 출력은 초당 12MB여야 하며 약 3000 IOPS에 도달해야 하며 스레드 수에 따른 변동은 거의 없습니다.

## 가상화 환경을 위한 단계 {#steps-for-virtualised-environments}

### VMWare {#vmware}

WMWare ESX를 사용하여 가상화 환경을 관리하고 배포하는 경우 ESX 콘솔에서 MongoDB 작업에 맞게 다음 설정을 수행해야 합니다.

1. 메모리 벌루닝 끄기
1. MongoDB 데이터베이스를 호스팅하는 가상 시스템에 대한 메모리를 미리 할당하고 예약합니다.
1. 저장소 I/O 컨트롤을 사용하여 `mongod` 프로세스에 충분한 I/O를 할당하십시오.
1. [CPU 예약](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.hostclient.doc/GUID-6C9023B2-3A8F-48EB-8A36-44E3D14958F6.html?hWord=N4IghgNiBc4RB7AxmALgUwAQGEAKBVTAJ3QGcEBXIpMkAXyA)을 설정하여 MongoDB를 호스팅하는 컴퓨터의 CPU 리소스를 보장합니다.

1. ParaVirtual I/O 드라이버 사용을 고려해 보십시오. <!-- URL is a 404 See [knowledgebase article](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=1010398).-->

### Amazon Web Services {#amazon-web-services}

Amazon Web Services을 사용하여 MongoDB를 설정하는 방법에 대한 설명서는 MongoDB 웹 사이트에서 [AWS 통합 구성](https://www.mongodb.com/docs/cloud-manager/tutorial/configure-aws-integration/) 문서를 확인하십시오.

## 배포 전 MongoDB 보안 {#securing-mongodb-before-deployment}

배포 전 데이터베이스 구성을 보호하는 방법에 대한 자세한 내용은 [MongoDB를 안전하게 배포](https://blogs.adobe.com/security/2015/07/securely-deploying-mongodb-3-0.html)할 때 이 게시물을 참조하십시오.

## Dispatcher {#dispatcher}

### Dispatcher 운영 체제 선택 {#choosing-the-operating-system-for-the-dispatcher}

MongoDB 배포를 올바르게 처리하려면 Dispatcher을 호스팅하는 운영 체제에서 **Apache httpd** **버전 2.4 이상을 실행해야 합니다.**

또한 빌드에 사용된 모든 라이브러리가 최신 상태인지 확인하여 보안 관련 사항을 최소화하십시오.

### Dispatcher 구성 {#dispatcher-configuration}

일반적인 Dispatcher 구성은 단일 AEM 인스턴스의 10배에서 20배 더 많은 요청 처리량을 제공합니다.

Dispatcher은 상태를 저장하지 않으므로 쉽게 가로로 확장할 수 있습니다. 일부 배포에서는 작성자가 특정 리소스에 액세스하지 못하도록 제한해야 합니다. 작성자 인스턴스와 함께 Dispatcher을 사용하는 것이 좋습니다.

Dispatcher 없이 AEM을 실행하려면 다른 애플리케이션에서 SSL 종료 및 로드 밸런싱을 수행해야 합니다. 세션이 만들어지는 AEM 인스턴스(고정 연결이라고 함)에 대한 친화성을 가져야 하므로 필요합니다. 그 이유는 콘텐츠에 대한 업데이트가 최소한의 지연을 보이도록 하기 위해서입니다.

구성 방법에 대한 자세한 내용은 [Dispatcher 설명서](https://experienceleague.adobe.com/ko/docs/experience-manager-dispatcher/using/dispatcher)를 참조하세요.

### 추가 구성 {#additional-configuration}

#### 고정 연결 {#sticky-connections}

고정 연결은 한 명의 사용자에 대한 개인화된 페이지 및 세션 데이터가 모두 AEM의 동일한 인스턴스에서 구성되도록 합니다. 이 데이터는 인스턴스에 저장되므로 동일한 사용자의 후속 요청은 동일한 인스턴스로 돌아갑니다.

모든 내부 레이어에서 AEM 인스턴스로 요청을 라우팅하는 고정 연결을 활성화하여 후속 요청이 동일한 AEM 인스턴스에 도달하도록 유도하는 것이 좋습니다. 이렇게 하면 인스턴스 간에 콘텐츠가 업데이트될 때 표시되는 지연을 최소화하는 데 도움이 됩니다.

#### 장기 만료 {#long-expires}

기본적으로 AEM Dispatcher에서 전송된 컨텐츠에는 마지막 수정 날짜 및 Etag 헤더가 있으며 컨텐츠의 만료는 표시되지 않습니다. 이 흐름을 사용하면 사용자 인터페이스가 항상 최신 버전의 리소스를 가져옵니다. 또한 브라우저가 GET 작업을 수행하여 리소스가 변경되었는지 확인하는 것을 의미합니다. 따라서 페이지 로드에 따라 HTTP 응답이 304(수정되지 않음)인 여러 요청이 발생할 수 있습니다. 만료되지 않는 리소스의 경우 만료 헤더를 설정하고 Last-Modified 및 ETag 헤더를 제거하면 콘텐츠가 캐시됩니다. 또한 Expires 헤더의 날짜가 충족될 때까지 추가 업데이트 요청이 수행되지 않습니다.

그러나 이 방법을 사용하면 Expires 헤더가 만료되기 전에 리소스가 브라우저에서 만료되는 합리적인 방법이 없음을 의미합니다. 이 워크플로를 완화하기 위해 클라이언트 라이브러리에 변경 불가능한 URL을 사용하도록 HtmlClientLibraryManager를 구성할 수 있습니다.

이러한 URL은 변경되지 않습니다. URL에 포함된 리소스의 본문이 변경되면 변경 사항이 URL에 반영되어 브라우저가 리소스의 올바른 버전을 요청하도록 합니다.

기본 구성은 선택기를 HtmlClientLibraryManager에 추가합니다. 선택기가 되면 리소스는 선택기가 그대로 있는 Dispatcher에 캐시됩니다. 또한 이 선택기를 사용하여 올바른 만료 동작을 확인할 수 있습니다. 기본 선택기는 `lc-.*?-lc` 패턴을 따릅니다. 다음 Apache httpd 구성 지시문은 해당 패턴과 일치하는 모든 요청이 적절한 만료 시간과 함께 제공되도록 합니다.

```xml
Header set Expires "Tue, 20 Jan 2037 04:20:42 GMT" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header set Cache-Control "public, no-transform, max-age=267840000" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset ETag "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Last-Modified "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Pragma "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
```

#### 검색 결과 없음 {#no-sniff}

컨텐츠가 컨텐츠 유형 없이 전송되는 경우 많은 브라우저는 컨텐츠의 처음 몇 바이트를 읽어 컨텐츠 유형을 추측하려고 합니다. 이 방법을 &quot;스니핑&quot;이라고 합니다. 스니핑은 저장소에 쓸 수 있는 사용자가 콘텐츠 유형이 없는 악성 콘텐츠를 업로드할 수 있으므로 보안 취약점이 발생합니다.

따라서 Dispatcher에서 제공하는 리소스에 `no-sniff` 헤더를 추가하는 것이 좋습니다. 그러나 Dispatcher은 헤더를 캐시하지 않습니다. 따라서 AEM 원본 서버의 원래 콘텐츠 유형 헤더를 사용하는 대신 로컬 파일 시스템에서 제공되는 모든 콘텐츠의 콘텐츠 유형이 확장에 의해 결정됩니다.

웹 애플리케이션이 파일 유형 없이 캐시된 리소스를 절대 제공하지 않는 것으로 알려진 경우 스니프를 안전하게 활성화할 수 없습니다.

[캡처 없음]을 활성화할 수 있습니다.

```xml
Header set X-Content-Type-Options "nosniff"
```

또한 다음을 선택적으로 활성화할 수 있습니다.

```xml
RewriteCond %{REQUEST_URI} \.(?:js|jsonp)$ [OR]
RewriteCond %{QUERY_STRING} (callback|jsonp|cb)=\w+
RewriteRule .* - [E=jsonp_request:1]
Header set X-Content-Type-Options "nosniff"  env=jsonp_request
Header setifempty Content-Type application/javascript env=jsonp_request
```

#### 콘텐츠 보안 정책 {#content-security-policy}

기본 Dispatcher 설정을 사용하면 CSP라고도 하는 컨텐츠 보안 정책을 열 수 있습니다. 이 설정을 사용하면 페이지가 브라우저 샌드박스의 기본 정책을 준수하는 모든 도메인에서 리소스를 로드할 수 있습니다.

신뢰할 수 없거나 확인되지 않은 외부 서버에서 JavaScript 엔진에 코드를 로드하는 것을 방지하기 위해 리소스를 로드할 수 있는 위치를 제한하는 것이 좋습니다.

CSP를 사용하면 정책을 미세 조정할 수 있습니다. 그러나 복잡한 응용 프로그램에서는 너무 제한적인 정책으로 인해 사용자 인터페이스의 일부가 손상될 수 있으므로 CSP 헤더를 주의 깊게 개발해야 합니다.

>[!NOTE]
>
>이 작동 방식에 대한 자세한 내용은 [CSP(콘텐츠 보안 정책)의 OWASP 페이지](https://cheatsheetseries.owasp.org/cheatsheets/Content_Security_Policy_Cheat_Sheet.html)를 참조하십시오.

### 크기 조정 {#sizing}

크기 조정에 대한 자세한 내용은 [하드웨어 크기 조정 지침](/help/managing/hardware-sizing-guidelines.md)을 참조하세요.

### MongoDB 성능 최적화 {#mongodb-performance-optimization}

MongoDB 성능에 대한 일반 정보는 [MongoDB 성능 분석](https://docs.mongodb.org/manual/administration/analyzing-mongodb-performance/)을 참조하십시오.

## 알려진 제한 사항 {#known-limitations}

### 동시 설치 {#concurrent-installations}

MongoMK는 단일 데이터베이스와 함께 여러 AEM 인스턴스의 동시 사용을 지원하지만 동시 설치는 지원되지 않습니다.

이 문제를 해결하려면 먼저 단일 멤버로 설치를 실행하고 첫 번째 멤버 설치가 완료된 후 다른 멤버를 추가해야 합니다.

### 페이지 이름 길이 {#page-name-length}

AEM이 MongoMK 지속성 관리자 배포에서 실행 중인 경우 [페이지 이름은 150자로 제한됩니다.](/help/sites-authoring/managing-pages.md)

>[!NOTE]
>
>MongoDB의 알려진 제한 사항 및 임계값을 숙지할 수 있도록 [MongoDB 설명서](https://docs.mongodb.com/manual/reference/limits/)를 참조하세요.
