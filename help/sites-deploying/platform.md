---
title: AEM 플랫폼 소개
description: AEM 플랫폼과 Adobe Experience Manager 6.5 설치 및 배포를 포함한 가장 중요한 구성 요소는 물론 Adobe Managed Services 클라우드 배포를 포함한 아키텍처에 대해 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/introduction-to-oak
exl-id: 8ee5f4ff-648d-45ea-a51e-894cd4385e62
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Developer
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 7%

---


# AEM 플랫폼 소개{#introduction-to-the-aem-platform}

AEM 6의 AEM 플랫폼은 Apache Jackrabbit Oak을 기반으로 합니다.

Apache Jackrabbit Oak은 확장 가능하고 성능이 뛰어난 계층형 콘텐츠 저장소를 구현하여 최신 세계적 수준의 웹 사이트 및 기타 까다로운 콘텐츠 애플리케이션의 기반으로 사용하도록 하기 위한 노력입니다.

Jackrabbit 2의 후속 제품이며 AEM 6에서 컨텐츠 저장소인 CRX의 기본 백엔드로 사용됩니다.

## 설계 원칙 및 목표 {#design-principles-and-goals}

Oak은 [JSR-283](https://jcp.org/en/jsr/detail?id=283)&#x200B;(JCR 2.0) 사양을 구현합니다. 주요 설계 목표는 다음과 같습니다.

* 대형 저장소에 대한 지원 향상
* 고가용성을 위한 여러 분산 클러스터 노드
* 향상된 성능
* 많은 하위 노드 및 액세스 제어 수준 지원

## 아키텍처 개념 {#architecture-concept}

![chlimage_1-84](assets/chlimage_1-84.png)

### 스토리지 {#storage}

스토리지 계층의 목적은 다음과 같습니다.

* 트리 모델 구현
* 스토리지를 플러그할 수 있도록 설정
* 클러스터링 메커니즘 제공

### Oak 코어 {#oak-core}

Oak 코어는 스토리지 레이어에 다음과 같은 여러 계층을 추가합니다.

* 액세스 수준 제어
* 검색 및 색인화
* 관찰

### OAK JS {#oak-jcr}

Oak JCR의 주요 목적은 JCR 의미 체계를 트리 작업으로 변환하는 것입니다. 또한 다음에 대한 책임이 있습니다.

* JCR API 구현
* JCR 제한을 구현하는 커밋 후크 포함

또한 이제 비 Java 구현이 가능하며 Oak JCR 개념의 일부입니다.

## 스토리지 개요 {#storage-overview}

Oak 스토리지 계층은 콘텐츠의 실제 스토리지에 대한 추상화 계층을 제공합니다.

현재 AEM6에는 **Tar 저장소** 및 **MongoDB 저장소**&#x200B;와 같은 두 가지 저장소 구현이 있습니다.

### Tar 스토리지 {#tar-storage}

Tar 저장소는 tar 파일을 사용합니다. 더 큰 세그먼트 내에서 다양한 유형의 레코드로 콘텐츠를 저장합니다. 저널은 저장소의 최신 상태를 추적하는 데 사용됩니다.

이를 중심으로 빌드된 몇 가지 주요 디자인 원칙이 있습니다.

* **변경할 수 없는 세그먼트**

콘텐츠는 최대 256KB의 세그먼트에 저장됩니다. 변경 불가능한 세그먼트로 자주 액세스하는 세그먼트를 쉽게 캐시하고 저장소를 손상시킬 수 있는 시스템 오류를 줄일 수 있습니다.

각 세그먼트는 고유 식별자(UUID)로 식별되며 콘텐츠 트리의 연속 하위 집합을 포함합니다. 또한 세그먼트는 다른 콘텐츠를 참조할 수 있습니다. 각 세그먼트는 다른 참조된 세그먼트의 UUID 목록을 유지합니다.

* **지역**

노드 및 그 바로 아래 하위 노드와 같은 관련 레코드는 동일한 세그먼트에 저장됩니다. 이렇게 하면 저장소를 빠르게 검색할 수 있으며 세션당 두 개 이상의 관련 노드에 액세스하는 일반적인 클라이언트의 캐시 실패를 대부분 방지할 수 있습니다.

* **압축**

레코드의 서식은 크기에 맞게 최적화되어 IO 비용을 줄이고 캐시에 있는 콘텐츠를 최대한 많이 맞출 수 있습니다.

### Mongo 스토리지 {#mongo-storage}

MongoDB 스토리지는 공유 및 클러스터링을 위해 MongoDB를 사용한다. 저장소 트리는 각 노드가 별도의 문서인 하나의 MongoDB 데이터베이스에 보관됩니다.

여기에는 몇 가지 세부 사항이 있습니다.

* 개정

콘텐츠의 각 업데이트(커밋)에 대해 새 수정 버전이 만들어집니다. 개정은 기본적으로 다음 세 가지 요소로 구성된 문자열입니다.

1. 생성된 컴퓨터의 시스템 시간에서 파생된 타임스탬프
1. 동일한 타임스탬프로 생성된 개정을 구분하는 카운터입니다.
1. 수정이 생성된 클러스터 노드 ID

* 분기

분기가 지원되어 클라이언트가 여러 변경 사항을 스테이징하고 단일 병합 호출로 표시할 수 있습니다.

* 이전 문서

MongoDB 스토리지는 매번 수정할 때마다 문서에 데이터를 추가합니다. 그러나 정리 작업이 명시적으로 트리거되는 경우에만 데이터를 삭제합니다. 특정 임계값이 충족되면 이전 데이터가 이동됩니다. 이전 문서에는 변경할 수 없는 데이터만 포함되어 있습니다. 즉, 커밋되고 병합된 개정 버전만 포함됩니다.

* 클러스터 노드 메타데이터

활성 및 비활성 클러스터 노드에 대한 데이터는 클러스터 작업을 용이하게 하기 위해 데이터베이스에 보관됩니다.

MongoDB 스토리지를 사용하는 일반적인 AEM 클러스터 설정:

![chlimage_1-85](assets/chlimage_1-85.png)

## Jackrabbit 2와 다른 점은 무엇입니까? {#what-is-different-from-jackrabbit}

Oak은 JCR 1.0 표준과 하위 호환되므로 사용자 수준에서 거의 변경 사항이 없습니다. 그러나 Oak 기반 AEM 설치를 설정할 때 고려해야 하는 몇 가지 주목할 만한 차이점이 있습니다.

* Oak은 색인을 자동으로 만들지 않습니다. 따라서 필요한 경우 사용자 정의 색인을 만들어야 합니다.
* 세션이 항상 저장소의 최신 상태를 반영하는 Jackrabbit 2와 달리, Oak에서는 세션이 세션이 획득된 시점부터 저장소에 대한 안정적인 보기를 반영합니다. 그 이유는 Oak이 기반으로 하는 마을금고 모델 때문이다.
* Oak에서는 SNS(동일 이름 동일 수준)가 지원되지 않습니다.

## 기타 플랫폼 관련 설명서 {#other-platform-related-documentation}

AEM 플랫폼에 대한 자세한 내용은 아래 기사도 참조하십시오.

* [AEM 6에서 노드 저장소 및 데이터 저장소 구성](/help/sites-deploying/data-store-config.md)
* [Oak 쿼리 및 색인화](/help/sites-deploying/queries-and-indexing.md)
* [AEM 6의 스토리지 요소](/help/sites-deploying/storage-elements-in-aem-6.md)
* [MongoDB를 사용한 AEM](/help/sites-deploying/aem-with-mongodb.md)
