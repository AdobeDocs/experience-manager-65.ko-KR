---
title: 권장 배포
seo-title: 권장 배포
description: 이 문서에서는 AEM에 대해 권장되는 토폴로지에 대해 설명합니다.
seo-description: 이 문서에서는 AEM에 대해 권장되는 토폴로지에 대해 설명합니다.
uuid: bc638121-c531-43eb-9ec6-3283a33519f8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 66d351e1-87f1-4006-bf8a-3cbbd33db9ed
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 권장 배포{#recommended-deployments}

>[!NOTE]
>
>이 페이지는 AEM에 대해 권장되는 토폴로지를 참조합니다. 클러스터링 기능과 구성 방법에 대한 자세한 내용은 Apache Sling Discovery [API 설명서를](https://sling.apache.org/documentation/bundles/discovery-api-and-impl.html)참조하십시오.

MicroKernels는 AEM 6.2에서 시작하는 지속성 관리자 역할을 합니다.요구 사항에 맞게 하나를 선택하는 것은 인스턴스의 목적과 고려하고 있는 배포 유형에 따라 달라집니다.

아래 예제는 가장 일반적인 AEM 설정에서 권장되는 용도를 나타내는 것입니다.

## 배포 시나리오 {#deployment-scenarios}

### 단일 TarMK 인스턴스 {#single-tarmk-instance}

이 시나리오에서는 단일 TarMK 인스턴스가 단일 서버에서 실행됩니다.

**작성자 인스턴스의 기본 배포입니다.**

![chlimage_1-15](assets/chlimage_1-15.png)

장점:

* 간단
* 간편한 유지 관리
* 뛰어난 성능

단점:

* 서버 용량 한계를 뛰어넘을 수 없음
* 장애 복구 용량 없음

### TarMK Cold Standby {#tarmk-cold-standby}

하나의 TarMK 인스턴스가 기본 인스턴스로 작동합니다. 기본 저장소에서 대기 페일오버 시스템으로 복제됩니다.

전체 저장소가 장애 조치(failover) 서버에 지속적으로 복제되므로 콜드 대기 메커니즘도 백업으로 사용할 수 있습니다. 장애 조치(failover) 서버가 콜드 대기 모드에서 실행 중이기 때문에 인스턴스의 HttpReceiver만 실행 중입니다.

![chlimage_1-16](assets/chlimage_1-16.png)

장점:

* 단순성
* 유지 관리
* 공연
* 장애 조치

단점:

* 서버 용량 한계를 넘어 확장 불가능
* 대부분의 시간에 한 대의 서버가 유휴 상태입니다.
* 페일오버가 자동으로 수행되지 않습니다. 장애 조치 시스템이 요청 제공을 시작하기 전에 외부에서 감지해야 합니다.

>[!NOTE]
>
>TarMK Cold Standby를 사용하여 AEM을 구성하는 방법에 대한 자세한 내용은 [이](/help/sites-deploying/tarmk-cold-standby.md) 문서를 참조하십시오.

>[!NOTE]
>
>이 TarMK 예제의 Cold Standby Deployment에서는 장애 조치 서버에 대한 지속적인 복제가 있으므로 기본 인스턴스와 대기 인스턴스 모두에 개별적으로 라이센스가 부여되어야 합니다. 라이선스에 대한 자세한 내용은 Adobe 일반 라이선스 [약관을 참조하십시오](https://www.adobe.com/legal/terms/enterprise-licensing.html).

### TarMK Farm {#tarmk-farm}

여러 Oak 인스턴스가 하나의 TarMK 인스턴스로 각각 실행됩니다. TarMK 리포지토리는 독립적이며 동기화되어야 합니다.

작성자 서버가 각 팜 구성원에게 동일한 컨텐츠를 게시하고 있다는 사실과 함께 저장소를 동기화할 수 있습니다. 자세한 내용은 복제를 [참조하십시오](/help/sites-deploying/replication.md).

AEM Communities의 경우 사용자 생성 콘텐츠(UGC)는 복제되지 않습니다. TarMK 팜에서 UGC를 지원하려면 AEM Communities에 대한 [고려 사항을 참조하십시오](#considerations-for-aem-communities).

**게시 환경을 위한 기본 배포입니다.**

![chlimage_1-17](assets/chlimage_1-17.png)

장점:

* 공연
* 읽기 액세스를 위한 확장성
* 장애 조치

### 단일 데이터 센터에서 고가용성을 위한 MongoMK 장애 조치가 포함된 Oak 클러스터 {#oak-cluster-with-mongomk-failover-for-high-availability-in-a-single-datacenter}

이 접근 방식은 단일 데이터 센터 내에서 MongoDB 복제본 세트에 액세스하는 여러 Oak 인스턴스를 의미하며, 실제로 AEM 작성자 환경에 대해 활성 상태의 클러스터를 만듭니다. MongoDB의 복제본 세트는 하드웨어 또는 네트워크 장애 발생 시 고가용성 및 중복성을 제공하는 데 사용됩니다.

![chlimage_1-18](assets/chlimage_1-18.png)

장점:

* 새로운 AEM 작성자 인스턴스를 사용하여 가로로 크기 조절
* 데이터 레이어의 고가용성, 이중화 및 자동 장애 복구

단점:

* 일부 시나리오의 경우 TarMK보다 성능이 낮을 수 있습니다.

### 여러 데이터 센터에서 MongoMK 장애 조치를 제공하는 Oak 클러스터 {#oak-cluster-with-mongomk-failover-across-multiple-datacenters}

이 접근 방식은 여러 데이터 센터에 걸쳐 MongoDB 복제본 세트에 액세스하는 여러 Oak 인스턴스를 의미하며, 실제로는 AEM 작성자 환경에 대해 활성 상태의 클러스터를 만듭니다. 여러 데이터 센터를 보유한 MongoDB 복제는 동일한 고가용성과 중복성을 제공하지만 이제 데이터 센터 운영 중단을 처리할 수 있습니다.

![oakclustermongofailover2datacenters](assets/oakclustermongofailover2datacenters.png)

장점:

* 새로운 AEM 작성자 인스턴스를 사용하여 가로로 크기 조절
* 데이터 레이어의 고가용성, 중복성 및 자동 페일오버(데이터 센터 운영 중단 포함)

>[!NOTE]
>
>위의 다이어그램에서 AEM Server 3 및 AEM Server 4는 [여기에](/help/sites-deploying/aem-with-mongodb.md#checklists)설명된 요구 사항보다 높은 데이터 센터 2의 AEM Server와 데이터 센터 1의 MongoDB 기본 노드 사이의 네트워크 지연을 가정할 때 비활성 상태로 표시됩니다. 예를 들어 가용 영역 사용을 통해 최대 지연이 요구 사항과 호환하는 경우 데이터 센터 2의 AEM 서버도 활성화하여 여러 데이터 센터에 활성 상태의 AEM 클러스터를 만들 수 있습니다.

>[!NOTE]
>
>이 섹션에 설명된 MongoDB 아키텍처 개념에 대한 자세한 내용은 MongoDB [복제를 참조하십시오](https://docs.mongodb.org/manual/replication/).

## 마이크로커널:사용 {#microkernels-which-one-to-use}

두 개의 사용 가능한 마이크로 커널 중에서 선택할 때 고려해야 하는 기본 규칙은 TarMK가 성능용으로 설계된 반면 MongoMK는 확장성을 위해 사용됩니다.

이러한 의사 결정 행렬을 사용하여 요구 사항에 가장 적합한 배포 유형을 설정할 수 있습니다.

Adobe에서는 아래 설명된 사용 사례를 제외하고 모든 배포 시나리오에서 고객이 사용하는 기본 지속성 기술로 TarMK를 권장합니다.

### 작성자 인스턴스에서 TarMK보다 AEM MongoMK를 선택하는 경우의 예외 {#exceptions-for-choosing-aem-mongomk-over-tarmk-on-author-instances}

TarMK보다 MongoMK 지속성 백엔드를 선택하는 주된 이유는 인스턴스를 가로로 크기 조절하기 위함입니다. 즉, 두 개 이상의 활성 작성자 인스턴스가 항상 실행되고 MongoDB를 지속성 스토리지 시스템으로 사용할 수 있습니다. 일반적으로 모든 동시 작성 활동을 지원하는 단일 서버의 CPU 및 메모리 용량이 더 이상 지속 가능하지 않다는 사실에서 두 개 이상의 작성자 인스턴스를 실행해야 합니다.

새로운 사이트가 가동된 후 정확한 동시 시청 모델이 어떤 모습일지 예측하는 것은 거의 불가능하다. 따라서 Adobe에서는 MongoMK와 두 개 이상의 작성자 활성 노드를 사용할지 여부를 평가할 때 다음 기준을 고려할 것을 권장합니다.

1. 하루에 연결된 지정된 사용자 수:수천 개 이상의
1. 동시 사용자 수:수백 개 이상의
1. 일별 자산 인제션 볼륨:수십만 개 이상의
1. 일일 페이지 편집 볼륨:수 십만 개 이상의 파일(예: 다중 사이트 관리자를 통한 자동 업데이트 또는 뉴스 피드 포함)을 만들 수 있습니다.
1. 일일 검색 볼륨:수만 개 이상의

>[!NOTE]
>
>어려운 날은 배포된 하드웨어 구성 컨텍스트에서 고객의 애플리케이션 성능을 평가하는 데 사용할 수 있습니다. 이 도구에 대한 자세한 내용은 [여기에서](/help/sites-developing/tough-day.md)확인할 수 있습니다.

MongoDB를 사용한 최소 배포에는 일반적으로 다음 토폴로지가 포함됩니다.

* 하나의 기본 노드, 각 노드에서 15밀리초 미만의 지연과 함께 각 MongoDB 인스턴스가 가용성 영역에서 실행되는 두 개의 보조 노드로 구성된 MongoDB 복제본 세트
* MongoDB 기본 및 보조 인스턴스가 실행 중인 각 데이터 센터에서 각 작성자 인스턴스가 실행되는 단일 지시형 노드, 비지시형 노드 및 두 개의 활성 상태의 작성자 인스턴스 클러스터입니다.

또한 자산 또는 바이너리가 MongoDB 내에 저장되지 않도록 공유 파일 시스템 또는 Amazon S3에 데이터 저장소를 구성하는 것이 좋습니다. 이렇게 하면 배포 내에서 최적의 성능을 보장할 수 있습니다.

두 개 이상의 작성자 인스턴스 클러스터로 구성된 MongoDB 복제본 세트를 배포하면 추가로 얻을 수 있는 이점 중 하나는 작성자 인스턴스, MongoDB 복제본 또는 전체 데이터 센터 장애 발생 시 다운타임을 최소화하는 자동 복구 시나리오를 통해 얻을 수 있다는 것입니다. 그럼에도 불구하고 TarMK가 TarMK보다 MongoMK를 선택하는 것은 복구 요구 사항에만 국한되지 않습니다. TarMK는 제어된 장애 조치 메커니즘으로 최소한의 다운타임 솔루션을 제공할 수 있습니다.

배포 후 처음 18개월 동안 위의 기준이 충족되지 않을 경우 먼저 TarMK를 사용하여 AEM을 배포한 다음, 위의 기준이 적용되는 이후 날짜에 구성을 다시 평가한 다음, 마지막으로 TarMK에 남을 것인지 MongoMK로 마이그레이션할 것인지 결정할 수 있습니다.

### 게시 인스턴스에서 TarMK보다 AEM MongoMK를 선택하는 경우의 예외 {#exceptions-for-choosing-aem-mongomk-over-tarmk-on-publish-instances}

게시 인스턴스에 대해 MongoMK를 배포하는 것은 권장되지 않습니다. 배포의 게시 계층은 거의 항상 TarMK를 실행하는 완전 독립 게시 인스턴스의 팜으로 배포되며, 작성자 인스턴스의 컨텐츠를 복제하여 동기화 상태로 유지됩니다. 게시 인스턴스에 적합한 이 &quot;공유 없음&quot; 아키텍처는 선형 방식으로 게시 계층의 배포를 가로로 확장할 수 있도록 합니다. 팜 토폴로지는 또한 업데이트 또는 업그레이드를 적용하여 인스턴스를 롤링 기반으로 게시함으로써 혜택을 제공합니다. 따라서 게시 계층에 대한 변경 사항에는 다운타임이 필요하지 않습니다.

게시자가 두 개 이상 있을 때마다 게시 계층에서 MongoMK 클러스터를 사용하는 AEM Communities에는 적용되지 않습니다. JSRP를 선택하는 경우( [커뮤니티 콘텐츠 저장소](/help/communities/working-with-srp.md)참조), MongoDB 또는 RDB와 같이 선택한 MK에 상관없이 모든 게시 측 클러스터와 마찬가지로 MongoMK 클러스터가 적절합니다.

### MongoMK를 사용하여 AEM을 배포할 때의 사전 요구 사항 및 권장 사항 {#prerequisites-and-recommendations-when-deploying-aem-with-mongomk}

AEM용 MongoMK 배포를 고려하고 있는 경우 사전 요구 사항 및 권장 사항 세트를 사용할 수 있습니다.

**MongoDB 배포를 위한 필수 사전 요구 사항:**

1. MongoDB 배포 아키텍처 및 크기 조정은 AEM에 익숙한 Adobe Consulting 또는 MongoDB Architects의 지원을 통해 프로젝트 구현의 일부여야 합니다.
1. 기존 또는 새로운 MongoDB 환경을 유지 관리하고 유지 관리할 수 있도록 파트너 또는 고객 팀 내에 MongoDB 전문 지식이 있어야 합니다.
1. MongoDB의 상업용 또는 오픈 소스 버전(AEM 지원 모두)을 배포할 수 있지만 MongoDB Inc.에서 직접 MongoDB 유지 관리 및 지원 계약을 구입해야 합니다.
1. 전체 AEM 및 MongoDB 아키텍처 및 인프라스트럭처는 Adobe AEM Architect에 의해 잘 정의되고 검증되어야 합니다.
1. MongoDB 파섹

**MongoDB 배포에 대한 강력한 권장 사항:**

* Adobe Experience Manager에 대한 MongoDB [문서를](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)참조하십시오.
* MongoDB 프로덕션 [검사 목록을](https://docs.mongodb.org/manual/administration/production-checklist/)검토합니다.
* MongoDB의 인증 강좌는 [여기에서](https://university.mongodb.com/)온라인으로 이용할 수 있습니다.

>[!NOTE]
>
>이러한 지침, 사전 요구 사항 및 권장 사항에 대한 추가 질문이 있으면 Adobe 고객 지원 센터에 [문의하십시오](https://helpx.adobe.com/marketing-cloud/contact-support.html).

### AEM Communities 고려 사항 {#considerations-for-aem-communities}

AEM Communities를 배포하려는 [사이트의](/help/communities/overview.md)경우 게시 환경에서 커뮤니티 구성원이 게시한 UGC를 처리하기 위해 [최적화된 배포를](/help/communities/working-with-srp.md#characteristicsofstorageoptions) 선택하는 것이 좋습니다.

UGC를 일관되게 보려면 [공용 저장소를](/help/communities/working-with-srp.md)사용하여 작성자와 다른 게시 인스턴스 간에 UGC를 복제할 필요가 없습니다.

다음은 배포의 최상의 지속성 유형을 선택할 수 있도록 지원하는 일련의 의사 결정 매트릭스입니다.

#### 작성자 인스턴스의 배포 유형 선택 {#choosing-the-deployment-type-for-author-instances}

![chlimage_1-19](assets/chlimage_1-19.png)

#### 게시 인스턴스에 대한 배포 유형 선택 {#choosing-the-deployment-type-for-publish-instances}

![chlimage_1-20](assets/chlimage_1-20.png)

>[!NOTE]
>
>MongoDB 파섹 자세한 내용은 MongoDB [라이선스 정책](https://www.mongodb.org/about/licensing/) 페이지를 참조하십시오.
>
>AEM 배포를 최대한 활용하려면 Adobe에서 전문 지원을 받으려면 MongoDB Enterprise 버전의 라이선스를 부여하는 것이 좋습니다.
>
>라이센스에는 표준 복제본 세트가 포함되어 있습니다. 표준 복제본 세트는 작성자나 게시 배포에 사용할 수 있는 기본 인스턴스 1개와 보조 인스턴스 2개로 구성됩니다.
>
>MongoDB에서 작성자와 게시를 모두 실행하려면 별도의 두 개의 라이선스를 구입해야 합니다.
>
>자세한 내용은 Adobe Experience Manager [용 MongoDB 페이지를](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)참조하십시오.

