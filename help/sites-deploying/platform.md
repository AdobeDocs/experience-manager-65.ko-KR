---
title: AEM 플랫폼 소개
seo-title: AEM 플랫폼 소개
description: 이 문서에서는 AEM 플랫폼과 가장 중요한 구성 요소에 대한 전반적인 개요를 제공합니다.
seo-description: 이 문서에서는 AEM 플랫폼과 가장 중요한 구성 요소에 대한 전반적인 개요를 제공합니다.
uuid: 214d4c49-1f5c-432c-a2c0-c1fbdceee716
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: fccf9a0f-ebab-45ab-8460-84c86b3c4192
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/introduction-to-oak
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 0%

---


# AEM 플랫폼 소개{#introduction-to-the-aem-platform}

AEM 6의 AEM 플랫폼은 아파치 잭래빗 오크를 기반으로 합니다.

Apache Jackrabbit Oak은 세계적인 웹 사이트 및 기타 까다로운 컨텐츠 애플리케이션의 기초로 사용할 수 있는 확장 가능하고 성능 높은 계층 컨텐츠 저장소를 구현하기 위한 노력입니다.

Jackrabbit 2의 후속 프로그램으로 AEM 6에서 컨텐츠 저장소 CRX의 기본 백엔드로 사용됩니다.

## 디자인 원칙 및 목표 {#design-principles-and-goals}

Oak는 [JSR-283](https://www.day.com/day/en/products/jcr/jsr-283.html)(JCR 2.0) 사양을 구현합니다. 주요 디자인 목표는 다음과 같습니다.

* 대규모 저장소 지원 향상
* 고가용성을 위한 다중 분산 클러스터 노드
* 향상된 성능
* 많은 하위 노드 및 액세스 제어 수준 지원

## 아키텍처 개념 {#architecture-concept}

![chlimage_1-84](assets/chlimage_1-84.png)

### 저장 용량 {#storage}

스토리지 레이어의 목적은 다음과 같습니다.

* 트리 모델 구현
* 스토리지 플러그 가능
* 클러스터링 메커니즘 제공

### Oak Core {#oak-core}

Oak Core는 스토리지 레이어에 여러 레이어를 추가합니다.

* 액세스 수준 컨트롤
* 검색 및 인덱싱
* 관찰

### Oak JCR {#oak-jcr}

Oak JCR의 주요 목표는 JCR 의미론을 나무 작업으로 바꾸는 것입니다. 다음과 같은 책임도 있습니다.

* JCR API 구현
* JCR 제약 조건을 구현하는 커밋 후크 포함

또한 이제 비 Java 구현이 가능하고 Oak JCR 개념의 일부도 가능합니다.

## 저장소 개요 {#storage-overview}

Oak 저장소 레이어는 컨텐츠의 실제 저장을 위한 추상화 레이어를 제공합니다.

현재 AEM6에서는 두 가지 스토리지 구현을 사용할 수 있습니다.**Tar 저장소** 및 **MongoDB 저장소**.

### Tar 저장소 {#tar-storage}

Tar 저장소는 tar 파일을 사용합니다. 컨텐츠는 큰 세그먼트 내에 다양한 유형의 레코드로 저장됩니다. 분개는 저장소의 최신 상태를 추적하는 데 사용됩니다.

Adobe가 구축하는 몇 가지 주요 디자인 원칙이 있습니다.

* **변경 불가능한 세그먼트**

컨텐츠는 최대 256KiB 크기의 세그먼트에 저장됩니다. 변경 불가능하므로 자주 액세스하는 세그먼트를 쉽게 캐시하고 저장소가 손상될 수 있는 시스템 오류를 줄일 수 있습니다.

각 세그먼트는 UUID(고유 식별자)로 식별되며 컨텐츠 트리의 연속 하위 집합을 포함합니다. 또한 세그먼트는 다른 컨텐츠를 참조할 수 있습니다. 각 세그먼트는 다른 참조된 세그먼트의 UUID 목록을 유지합니다.

* **지역**

노드 및 해당 직계 자식과 같은 관련 레코드는 일반적으로 동일한 세그먼트에 저장됩니다. 따라서 저장소를 매우 빠르게 검색할 수 있으며 세션당 두 개 이상의 관련 노드에 액세스하는 일반적인 클라이언트에 대한 대부분의 캐시 놓치는 것을 방지할 수 있습니다.

* **컴팩트함**

레코드 서식은 크기가 IO 비용을 줄이고 캐시에 있는 컨텐츠에 최대한 맞게 최적화됩니다.

### Mongo 저장소 {#mongo-storage}

MongoDB 스토리지는 공유 및 클러스터링을 위해 MongoDB를 활용합니다. 저장소 트리는 각 노드가 별도의 문서인 하나의 MongoDB 데이터베이스에 보관됩니다.

여기에는 몇 가지 특정 부분이 있습니다.

* 수정 사항

컨텐츠의 각 업데이트(커밋)에 대해 새 개정이 생성됩니다. 개정은 기본적으로 세 가지 요소로 구성된 문자열입니다.

1. 생성된 시스템의 시스템 시간에서 파생된 타임스탬프
1. 동일한 타임스탬프로 만든 수정 내용을 구분하는 카운터
1. 개정이 만들어진 클러스터 노드 ID

* 분기

분기가 지원되므로 클라이언트가 여러 변경 사항을 스테이징하고 단일 병합 호출을 통해 볼 수 있습니다.

* 이전 문서

MongoDB 스토리지는 수정할 때마다 문서에 데이터를 추가합니다. 하지만 정리가 명시적으로 트리거된 경우에만 데이터를 삭제합니다. 특정 임계값이 충족되면 이전 데이터가 이동됩니다. 이전 문서에는 변경 불가능한 데이터만 포함되어 있으므로 커밋된 수정된 부분과 병합된 수정만 포함됩니다.

* 클러스터 노드 메타데이터

활성 및 비활성 클러스터 노드에 대한 데이터는 클러스터 작업을 용이하게 하기 위해 데이터베이스에 보관됩니다.

MongoDB 저장소가 있는 일반적인 AEM 클러스터 설정:

![chlimage_1-85](assets/chlimage_1-85.png)

## 잭래빗 2와 뭐가 다르죠?{#what-is-different-from-jackrabbit}

Oak는 JCR 1.0 표준과 역호환되도록 설계되었으므로 사용자 수준은 거의 변경되지 않습니다. 하지만 Oak 기반 AEM 설치를 설정할 때 고려해야 하는 몇 가지 중요한 차이점이 있습니다.

* Oak는 색인을 자동으로 만들지 않습니다. 이 때문에 필요할 때 사용자 지정 색인을 만들어야 합니다.
* 세션이 항상 저장소의 최신 상태를 반영하는 Jackrabbit 2와 달리 Oak a 세션은 세션이 확보된 시점부터 저장소의 안정적인 보기를 반영합니다. 이것은 Oak가 기반으로 하는 MVCC 모델 때문이다.
* Oak에서는 동일한 이름 형제(SNS)가 지원되지 않습니다.

## 기타 플랫폼 관련 문서 {#other-platform-related-documentation}

AEM 플랫폼에 대한 자세한 내용은 아래 기술문서를 참조하십시오.

* [AEM 6에서 노드 저장소 및 데이터 저장소 구성](/help/sites-deploying/data-store-config.md)
* [Oak 쿼리 및 색인](/help/sites-deploying/queries-and-indexing.md)
* [AEM 6의 스토리지 요소](/help/sites-deploying/storage-elements-in-aem-6.md)
* [AEM with MongoDB](/help/sites-deploying/aem-with-mongodb.md)

