---
title: 권장 배포
seo-title: Recommended Deployments
description: 이 문서에서는 AEM에 권장되는 토폴로지를 설명합니다.
seo-description: This article describes the recommended topologies for AEM.
uuid: bc638121-c531-43eb-9ec6-3283a33519f8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 66d351e1-87f1-4006-bf8a-3cbbd33db9ed
docset: aem65
exl-id: baec7fc8-d48c-4bc6-b12b-4bf4eff695ea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1792'
ht-degree: 1%

---

# 권장 배포{#recommended-deployments}

>[!NOTE]
>
>이 페이지는 AEM에 권장되는 토폴로지를 참조합니다. 클러스터링 기능 및 구성 방법에 대한 자세한 내용은 [Apache Sling Discovery API 설명서](https://sling.apache.org/documentation/bundles/discovery-api-and-impl.html).

MicroKernels는 AEM 6.2부터 지속성 관리자로 작동합니다. 필요에 맞게 하나를 선택하는 것은 인스턴스의 목적과 고려하고 있는 배포 유형에 따라 다릅니다.

아래 예제는 가장 일반적인 AEM 설정에서 권장 사항을 나타내는 것입니다.

## 배포 시나리오 {#deployment-scenarios}

### 단일 TarMK 인스턴스 {#single-tarmk-instance}

이 시나리오에서는 단일 TarMK 인스턴스가 단일 서버에서 실행됩니다.

**작성자 인스턴스에 대한 기본 배포입니다.**

![chlimage_1-15](assets/chlimage_1-15.png)

장점:

* 간단
* 간편한 유지 관리
* 뛰어난 성능

단점:

* 서버 용량 한계를 넘어서는 확장 불가능
* 페일오버 용량 없음

### TarMK 콜드 대기 {#tarmk-cold-standby}

하나의 TarMK 인스턴스가 기본 인스턴스로 작동합니다. 운영 시스템의 리포지토리는 대기 페일오버 시스템으로 복제됩니다.

전체 리포지토리는 항상 페일오버 서버에 복제되므로 콜드 대기 메커니즘 또한 백업으로 사용할 수 있습니다. 장애 조치(failover) 서버가 콜드 대기 모드로 실행 중입니다. 즉, 인스턴스의 HttpReceiver만 실행되고 있습니다.

![chlimage_1-16](assets/chlimage_1-16.png)

장점:

* 단순성
* 유지 관리
* 공연
* 페일오버

단점:

* 서버 용량의 한계를 넘어서는 확장 불가능
* 서버 하나가 대부분의 시간 동안 유휴 상태입니다
* 페일오버가 자동으로 수행되지 않습니다. 페일오버 시스템이 요청 서비스를 시작하기 전에 외부에서 감지해야 합니다.

>[!NOTE]
>
>TarMK Cold Standby를 사용하여 AEM을 구성하는 방법에 대한 자세한 내용은 다음을 참조하십시오 [이](/help/sites-deploying/tarmk-cold-standby.md) 문서.

>[!NOTE]
>
>이 TarMK 예제의 콜드 대기 배포에서는 페일오버 서버에 대한 지속적인 복제가 있으므로 기본 인스턴스와 대기 인스턴스 둘 다 별도로 라이센스를 받아야 합니다. 라이센스에 대한 자세한 내용은 [Adobe 일반 라이선스 약관](https://www.adobe.com/kr/legal/terms/enterprise-licensing.html).

### TarMK 팜 {#tarmk-farm}

여러 Oak 인스턴스는 각각 하나의 TarMK 인스턴스로 실행됩니다. TarMK 리포지토리는 독립적이며 동기화 상태여야 합니다.

리포지토리를 동기식으로 유지하는 것은 작성자 서버가 각 팜 구성원에게 동일한 컨텐츠를 게시한다는 사실과 함께 제공됩니다. 자세한 내용은 [복제](/help/sites-deploying/replication.md).

AEM Communities의 경우 사용자 생성 콘텐츠(UGC)는 복제되지 않습니다. TarMK 팜에서 UGC를 지원하려면 다음을 참조하십시오 [AEM Communities에 대한 고려 사항](#considerations-for-aem-communities).

**게시 환경을 위한 기본 배포입니다.**

![chlimage_1-17](assets/chlimage_1-17.png)

장점:

* 공연
* 읽기 액세스를 위한 확장성
* 페일오버

### 단일 데이터 센터에서 고가용성을 위한 MongoMK 페일오버가 포함된 Oak 클러스터 {#oak-cluster-with-mongomk-failover-for-high-availability-in-a-single-datacenter}

이 방법은 단일 데이터 센터 내에 있는 MongoDB 복제본 세트에 액세스하는 여러 Oak 인스턴스에 액세스하여 AEM 작성자 환경에 대해 활성 클러스터를 만드는 것을 의미합니다. MongoDB의 복제본 세트는 하드웨어 또는 네트워크 장애 발생 시 고가용성과 중복성을 제공하는 데 사용됩니다.

![chlimage_1-18](assets/chlimage_1-18.png)

장점:

* 새로운 AEM 작성자 인스턴스를 사용하여 가로 크기 조절 기능
* 데이터 계층의 고가용성, 이중화 및 자동 페일오버

단점:

* 일부 시나리오에 대해서는 TarMK보다 성능이 낮을 수 있습니다

### 여러 데이터 센터에서 MongoMK 장애 조치(failover)가 포함된 Oak 클러스터 {#oak-cluster-with-mongomk-failover-across-multiple-datacenters}

이 접근 방식은 여러 데이터 센터에 있는 MongoDB 복제본 세트에 액세스하는 여러 Oak 인스턴스에 액세스하여 AEM 작성자 환경에 대해 활성 클러스터를 만드는 것을 의미합니다. 여러 데이터 센터를 통해 MongoDB 복제는 동일한 고가용성 및 이중화 기능을 제공하지만 이제 데이터 센터 가동 중단을 처리할 수 있는 기능이 포함됩니다.

![ockclustermongofailover2datacenter](assets/oakclustermongofailover2datacenters.png)

장점:

* 새로운 AEM 작성자 인스턴스를 사용하여 가로 크기 조절 기능
* 데이터 계층의 고가용성, 이중화 및 자동 페일오버(데이터 센터 가동 중단 포함)

>[!NOTE]
>
>위의 다이어그램에서 AEM Server 3과 AEM Server 4는 Data Center 2의 AEM 서버와 Data Center 1의 MongoDB 기본 노드 사이의 네트워크 지연이 문서화된 요구 사항보다 높다고 가정할 때 비활성 상태로 표시됩니다 [여기](/help/sites-deploying/aem-with-mongodb.md#checklists). 예를 들어 가용성 영역을 사용하여 최대 지연이 요구 사항과 호환되는 경우 데이터 센터 2의 AEM 서버도 활성화될 수 있으므로 여러 데이터 센터에서 활성 AEM 클러스터를 만들 수 있습니다.

>[!NOTE]
>
>이 섹션에 설명된 MongoDB 아키텍처 개념에 대한 자세한 내용은 [MongoDB 복제](https://docs.mongodb.org/manual/replication/).

## 마이크로커널: 어떤 걸 사용하죠 {#microkernels-which-one-to-use}

사용 가능한 두 개의 마이크로 커널 중 하나를 선택할 때 고려해야 하는 기본 규칙은 TarMK가 성능용으로 설계된 반면 MongoMK는 확장성에 사용됩니다.

이러한 의사 결정 행렬을 사용하여 요구 사항에 맞는 최적의 배포 유형을 설정할 수 있습니다.

Adobe은 아래에 요약된 사용 사례를 제외하고, 모든 배포 시나리오에서 고객이 사용하는 기본 지속성 기술로 TarMK를 AEM 작성자 및 게시 인스턴스 둘 다에 사용할 것을 권장합니다.

### 작성자 인스턴스에서 TarMK보다 AEM MongoMK를 선택하기 위한 예외 {#exceptions-for-choosing-aem-mongomk-over-tarmk-on-author-instances}

TarMK보다 MongoMK 지속성 백엔드를 선택하는 주된 이유는 인스턴스를 가로로 크기 조절하기 위한 것입니다. 즉, 두 개 이상의 활성 작성자 인스턴스가 항상 실행되고 MongoDB를 지속성 스토리지 시스템으로 사용합니다. 일반적으로 두 개 이상의 작성 인스턴스를 실행해야 하는 이유는 모든 동시 작성 활동을 지원하는 단일 서버의 CPU 및 메모리 용량이 더 이상 지속되지 않기 때문입니다.

새로운 사이트가 라이브로 전환된 후 정확한 동시 시청 모델이 어떤 모습일지 예측하는 것은 거의 불가능하다. 따라서 Adobe은 MongoMK 및 두 개 이상의 작성자 활성 노드를 사용할지 여부를 평가할 때 다음 기준을 고려해 보는 것이 좋습니다.

1. 하루에 연결된 명명된 사용자 수: 수천, 혹은 그 이상의.
1. 동시 사용자 수: 100명 이상입니다.
1. 일별 자산 수집 볼륨: 수십만이나 그 이상에서요
1. 일별 페이지 편집 볼륨: 수십만 개 이상(예: 다중 사이트 관리자 또는 뉴스 피드 섭취 시 자동 업데이트 포함).
1. 일일 검색 양: 수만이나 그 이상에서요

>[!NOTE]
>
>어려운 날은 배포된 하드웨어 구성 컨텍스트에서 고객의 애플리케이션 성능을 평가하는 데 사용할 수 있습니다. 이 도구에 대한 자세한 내용을 확인할 수 있습니다. [여기](/help/sites-developing/tough-day.md).

MongoDB를 사용하는 최소 배포에는 일반적으로 다음 토폴로지가 포함됩니다.

* 하나의 주 노드, 각 노드에서 15밀리초 미만의 지연 시간이 있는 가용 영역에서 실행되는 각 MongoDB 인스턴스가 있는 두 개의 보조 노드로 구성된 MongoDB 복제본 세트
* MongoDB 기본 및 보조 인스턴스가 실행 중인 각 데이터 센터에서 실행되는 각 작성자 인스턴스를 사용하여 한 명의 지시선 노드, 한 개의 비지시선 노드 및 두 개의 노드가 항상 활성 상태인 작성 인스턴스의 클러스터입니다.

또한 자산 또는 바이너리가 MongoDB 내에 저장되지 않도록 공유 파일 시스템 또는 Amazon S3에서 데이터 저장소를 구성하는 것이 좋습니다. 이렇게 하면 배포 내에서 최적의 성능이 보장됩니다.

두 개 이상의 작성자 인스턴스로 구성된 클러스터로 MongoDB 복제본 세트를 배포함으로써 얻을 수 있는 추가적인 이점 중 하나는 작성자 인스턴스, MongoDB 복제본 또는 완전한 데이터 센터 장애 발생 시 다운타임이 최소화되는 자동 복구 시나리오를 가지는 것입니다. 그럼에도 불구하고 TarMK는 제어 페일오버 메커니즘을 통해 최소한의 다운타임 솔루션을 제공할 수 있으므로 TarMK보다 MongoMK의 선택이 복구 요구 사항으로만 추진되지는 않습니다.

위의 기준이 처음 18개월 배포 동안 충족되지 않을 것으로 예상되면, 먼저 TarMK를 사용하여 AEM을 배포하고, 위의 기준이 적용되는 나중에 구성을 다시 평가하고, 마지막으로 TarMK에 남아 있는지, MongoMK로 마이그레이션할지 여부를 결정하는 것이 좋습니다.

### 게시 인스턴스의 TarMK보다 AEM MongoMK를 선택하기 위한 예외 {#exceptions-for-choosing-aem-mongomk-over-tarmk-on-publish-instances}

게시 인스턴스에 MongoMK를 배포하지 않는 것이 좋습니다. 배포의 게시 계층은 거의 항상 TarMK를 실행하는 완전 독립 게시 인스턴스의 팜으로 배포되며, 작성자 인스턴스에서 컨텐츠를 복제하여 계속 동기화됩니다. 게시 인스턴스에 적합한 이 &quot;공유 없음&quot; 아키텍처를 사용하면 게시 계층의 배포가 선형 방식으로 가로로 확장할 수 있습니다. 팜 토폴로지는 또한 롤링 기반으로 게시 인스턴스에 업데이트 또는 업그레이드를 적용하여 게시 계층에 변경 시 다운타임이 필요하지 않도록 하는 이점이 있습니다.

게시자가 두 개 이상 있을 때마다 게시 계층에서 MongoMK 클러스터를 사용하는 AEM Communities에는 적용되지 않습니다. JSRP를 선택하는 경우(참조) [커뮤니티 컨텐츠 저장소](/help/communities/working-with-srp.md))이면 MongoMK 클러스터와 같이, MongoDB 또는 RDB와 같이 선택한 MK에 관계없이 모든 게시 측 클러스터와 마찬가지로 적절합니다.

### MongoMK와 함께 AEM을 배포할 때의 사전 요구 사항 및 Recommendations {#prerequisites-and-recommendations-when-deploying-aem-with-mongomk}

AEM용 MongoMK 배포를 고려하고 있는 경우, 사전 요구 사항 및 권장 사항 세트를 사용할 수 있습니다.

**MongoDB 배포를 위한 필수 사전 요구 사항:**

1. AEM에 익숙한 MongoDB Architects 또는 Adobe Consulting의 도움을 받아 MongoDB 배포 아키텍처 및 크기 조정이 프로젝트 구현의 일부여야 합니다.
1. 기존 또는 새로운 MongoDB 환경을 유지 관리하고 유지할 수 있다는 확신을 얻으려면 파트너 또는 고객 팀 내에 MongoDB 전문 지식이 있어야 합니다.
1. MongoDB의 상용 또는 오픈 소스 버전(AEM은 둘 다 지원)을 배포하도록 선택할 수 있지만, MongoDB Inc.에서 직접 MongoDB Maintenance and Support 계약을 구입해야 합니다.
1. 전체 AEM 및 MongoDB 아키텍처 및 인프라스트럭처는 Adobe AEM Architect에 의해 잘 정의되고 검증되어야 합니다.
1. MongoDB를 포함하는 AEM 배포에 대한 지원 모델을 검토해야 합니다.

**MongoDB 배포에 대한 강력한 권장 사항:**

* Adobe Experience Manager에 대한 MongoDB를 참조하십시오 [문서](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager);
* MongoDB 프로덕션 검토 [검사 목록](https://docs.mongodb.org/manual/administration/production-checklist/);
* 온라인으로 사용 가능한 MongoDB의 인증 클래스에 참석하십시오 [여기](https://university.mongodb.com/).

>[!NOTE]
>
>이러한 지침, 사전 요구 사항 및 권장 사항에 대한 모든 추가 질문이 있으면 [고객 지원 Adobe](https://helpx.adobe.com/kr/marketing-cloud/contact-support.html).

### AEM Communities에 대한 고려 사항 {#considerations-for-aem-communities}

배포하려는 사이트의 경우 [AEM Communities](/help/communities/overview.md)를 설정하는 것이 좋습니다 [배포 선택](/help/communities/working-with-srp.md#characteristicsofstorageoptions) 게시 환경의 커뮤니티 구성원이 게시한 UGC 처리를 위해 최적화되었습니다.

를 사용하여 [일반 상점](/help/communities/working-with-srp.md), UGC의 일관된 보기를 가져오기 위해 작성자와 다른 게시 인스턴스 간에 UGC를 복제할 필요가 없습니다.

다음은 배포에 가장 적합한 지속성 유형을 선택하는 데 도움이 되는 의사 결정 행렬 세트입니다.

#### 작성자 인스턴스에 대한 배포 유형 선택 {#choosing-the-deployment-type-for-author-instances}

![chlimage_1-19](assets/chlimage_1-19.png)

#### 게시 인스턴스에 대한 배포 유형 선택 {#choosing-the-deployment-type-for-publish-instances}

![chlimage_1-20](assets/chlimage_1-20.png)

>[!NOTE]
>
>MongoDB는 타사 소프트웨어이며 AEM 라이선스 패키지에 포함되어 있지 않습니다. 자세한 내용은 [MongoDB 라이선스 정책](https://www.mongodb.org/about/licensing/) 페이지.
>
>AEM을 최대한 활용하려면 MongoDB Enterprise 버전의 라이센스를 취득하여 전문 지원을 받는 것이 좋습니다.
>
>라이센스에는 작성자나 게시 배포에 사용할 수 있는 하나의 기본 인스턴스와 두 개의 보조 인스턴스로 구성된 표준 복제 세트가 포함되어 있습니다.
>
>MongoDB에서 작성자와 게시를 모두 실행하려면 두 개의 별도 라이센스를 구입해야 합니다.
>
>자세한 내용은 [Adobe Experience Manager용 MongoDB 페이지](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager).
