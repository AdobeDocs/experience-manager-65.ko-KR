---
title: 저장소 리소스 공급자 개요
description: UGC(사용자 생성 컨텐츠)라고 하는 커뮤니티 컨텐츠가 SRP(저장소 리소스 제공자)에서 제공하는 간단한 공통 저장소에 저장되는 방법에 대해 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 5f313274-1a2a-4e83-9289-60a4729b99b4
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 0%

---

# 저장소 리소스 공급자 개요 {#storage-resource-provider-overview}

## 소개 {#introduction}

AEM(Adobe Experience Manager) 커뮤니티 6.1부터 일반적으로 UGC(사용자 생성 컨텐츠)라고 하는 커뮤니티 컨텐츠는 [SRP(저장소 리소스 공급자](working-with-srp.md))에서 제공하는 하나의 공통 저장소에 저장됩니다.

CRUD(만들기, 읽기, 업데이트 및 삭제) 작업을 모두 포함하는 새로운 AEM Communities 인터페이스인 [SocialResourceProvider API](srp-and-ugc.md)(SRP API)를 통해 UGC에 액세스하는 몇 가지 SRP 옵션이 있습니다.

모든 SCF 구성 요소는 SRP API를 사용하여 구현되므로 [기본 토폴로지](topologies.md) 또는 UGC의 위치를 몰라도 코드를 개발할 수 있습니다.

***SocialResourceProvider API는 라이선스가 있는 AEM Communities 고객에게만 제공됩니다.***

>[!NOTE]
>
>**사용자 지정 구성 요소**: 사용 허가된 AEM Communities 고객의 경우 SRP API는 기본 토폴로지에 관계없이 UGC에 액세스하기 위해 사용자 지정 구성 요소 개발자가 사용할 수 있습니다. [SRP 및 UGC 필수 패키지](srp-and-ugc.md)를 참조하세요.

추가 참조:

* [SRP 및 UGC Essentials](srp-and-ugc.md) - SRP 유틸리티 메서드 및 예제.
* [SRP를 사용하여 UGC에 액세스](accessing-ugc-with-srp.md) - 코딩 지침.
* [SocialUtils 리팩터링](socialutils.md) - 더 이상 사용되지 않는 유틸리티 메서드를 현재 SRP 유틸리티 메서드에 매핑합니다.

## 저장소 정보 {#about-the-repository}

SRP를 이해하려면 AEM 커뮤니티 사이트에서 AEM 저장소(Oak)의 역할을 이해하는 것이 좋습니다.

**JCR(Java™ Content Repository)**
이 표준은 콘텐츠 저장소에 대한 데이터 모델 및 응용 프로그램 프로그래밍 인터페이스([JCR API](https://jackrabbit.apache.org/jcr/jcr-api.html))를 정의합니다. 기존 파일 시스템의 특성과 관계형 데이터베이스의 특성을 결합하며, 컨텐츠 애플리케이션에 자주 필요한 몇 가지 추가 기능을 제공합니다.

JCR의 구현 중 하나는 AEM 저장소인 Oak입니다.

**Apache Jackrabbit Oak**
[Oak](../../help/sites-deploying/platform.md)은(는) 콘텐츠 중심 애플리케이션용으로 설계된 데이터 스토리지 시스템인 JCR 2.0의 구현입니다. 비정형 데이터와 반정형 데이터를 위해 설계된 계층적 데이터베이스의 일종이다. 저장소는 사용자 대면 콘텐츠뿐만 아니라 애플리케이션에서 사용하는 모든 코드, 템플릿 및 내부 데이터를 저장합니다. 콘텐츠에 액세스하기 위한 UI는 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)입니다.

JCR과 Oak은 모두 일반적으로 AEM 저장소를 참조하는 데 사용됩니다.

비공개 작성 환경에서 사이트 콘텐츠를 개발한 후 공개 게시 환경에 복사해야 합니다. 이 작업은 대개 *[복제](deploy-communities.md#replication-agents-on-author)*&#x200B;라는 작업을 통해 수행됩니다. 이 작업은 작성자/개발자/관리자의 제어에 따라 수행됩니다.

UGC의 경우 컨텐츠는 공개 게시 환경에 등록된 사이트 방문자(커뮤니티 구성원)가 입력합니다. 이 작업은 임의로 수행됩니다.

관리 및 보고의 목적으로 개인 작성 환경에서 UGC에 액세스하는 것은 유용합니다. SRP를 사용하면 Publish에서 Author로 역복제가 필요하지 않으므로 Author에서 UGC에 대한 액세스가 더 일관되고 성능이 향상됩니다.

## SRP 정보 {#about-srp}

UGC가 공유 스토리지에 저장될 때 대부분의 배포에서 작성자 및 게시 환경 모두에서 액세스할 수 있는 단일 멤버 컨텐츠 인스턴스가 있습니다. SRP 선택 사항(MSRP, ASRP, JSRP)에 관계없이 모든 SRP API를 사용하여 프로그래밍 방식으로 액세스해야 합니다.

>[!NOTE]
>
>샘플 코드 및 추가 정보는 [SRP 및 UGC 필수 패키지](srp-and-ugc.md)를 참조하십시오.
>
>코딩할 때의 모범 사례는 [SRP를 사용하여 UGC에 액세스](accessing-ugc-with-srp.md)를 참조하십시오.

### ASRP {#asrp}

ASRP가 있는 경우 UGC는 JCR에 저장되지 않고 Adobe이 호스팅 및 관리하는 클라우드 서비스에 저장됩니다. ASRP에 저장된 UGC는 CRXDE Lite으로 보거나 JCR API를 사용하여 액세스할 수 없습니다.

[ASRP - Adobe 저장소 리소스 공급자](asrp.md)를 참조하십시오.

개발자가 UGC에 직접 액세스하는 것은 불가능합니다.

ASRP는 쿼리에 Adobe 클라우드를 사용합니다.

### MSRP {#msrp}

있는 경우 MSRP, UGC는 JCR에 저장되지 않고 MongoDB에 저장됩니다. MSRP에 저장된 UGC는 CRXDE Lite으로 보거나 JCR API를 사용하여 액세스할 수 없습니다.

[MSRP - MongoDB 저장소 리소스 공급자](msrp.md)를 참조하세요.

MSRP는 ASRP와 비슷하지만 모든 AEM 서버 인스턴스가 동일한 UGC에 액세스하고 있으므로 일반적인 도구를 사용하여 MongoDB에 저장된 UGC에 직접 액세스할 수 있습니다.

MSRP는 쿼리에 Solr을 사용합니다.

### JSRP {#jsrp}

JSRP는 단일 AEM 인스턴스의 모든 UGC에 액세스하는 기본 공급자입니다. MSRP 또는 ASRP를 설정할 필요 없이 AEM Communities 6.1을 빠르게 경험할 수 있습니다.

[JSRP - JCR 저장소 리소스 공급자](jsrp.md)를 참조하십시오.

UGC가 JCR에 저장되고 CRXDE Lite 및 JCR API에서 액세스할 수 있는 동안 JSRP가 있는 경우, Adobe은 JCR API를 사용하여 이 작업을 수행하지 않는 것을 권장합니다. 이 경우 향후 변경 사항이 사용자 지정 코드에 영향을 줄 수 있습니다.

또한 작성자 및 Publish 환경에 대한 저장소는 공유되지 않습니다. 게시 인스턴스 클러스터가 공유 게시 리포지토리를 생성하지만 Publish에 입력된 UGC는 작성자에게 표시되지 않으므로 작성자의 UGC를 관리할 수 없습니다. UGC는 입력된 인스턴스의 JCR(AEM repository)에서만 유지됩니다.

JSRP는 쿼리에 Oak 색인을 사용합니다.

## JCR의 섀도우 노드 정보 {#about-shadow-nodes-in-jcr}

UGC 경로를 모방하는 그림자 노드는 로컬 리포지토리에 존재하여 두 가지 용도로 사용됩니다.

1. [액세스 제어(ACL)](#for-access-control-acls)
1. [존재하지 않는 리소스(NER)](#for-non-existing-resources-ners)

SRP 구현에 관계없이 실제 UGC는 그림자 노드와 같은 위치에 *표시되지 않음*&#x200B;입니다.

### 액세스 제어(ACL)용 {#for-access-control-acls}

ASRP 및 MSRP와 같은 일부 SRP 구현은 ACL 확인을 제공하지 않는 데이터베이스에 커뮤니티 콘텐츠를 저장합니다. 그림자 노드는 ACL을 적용할 수 있는 로컬 저장소 위치를 제공합니다.

SRP API를 사용하면 모든 SRP 옵션이 모든 CRUD 작업 전에 섀도 위치에 대한 동일한 검사를 수행합니다.

ACL 검사는 리소스의 UGC에 적용된 권한을 확인하는 데 적합한 경로를 반환하는 유틸리티 메서드를 사용합니다.

샘플 코드는 [SRP 및 UGC Essentials](srp-and-ugc.md)을(를) 참조하십시오.

### 존재하지 않는 리소스(NER)의 경우 {#for-non-existing-resources-ners}

일부 Communities 구성 요소는 스크립트 내에 포함될 수 있으므로 Communities 기능을 지원하기 위해 Sling 주소 지정 가능한 노드가 필요합니다. [포함된 구성 요소](scf.md#add-or-include-a-communities-component)은(는) 존재하지 않는 리소스(NER)라고 합니다.

그림자 노드는 저장소에서 Sling 주소 지정 가능 위치를 제공합니다.

>[!CAUTION]
>
>그림자 노드에 여러 용도가 있으므로 그림자 노드가 있으면 구성 요소가 NER임을 *아님*&#x200B;합니다.

### 저장소 위치 {#storage-location}

다음은 [커뮤니티 구성 요소 안내서](components-guide.md)에서 [댓글 구성 요소](http://localhost:4502/content/community-components/en/comments.html)를 사용하는 그림자 노드의 예입니다.

* 구성 요소는 다음 위치의 로컬 저장소에 있습니다.

  `/content/community-components/en/comments/jcr:content/content/includable/comments`

* 해당 섀도우 노드는 다음 위치의 로컬 저장소에 있습니다.

  `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

그림자 노드 아래에 UGC가 없습니다.

기본 동작은 관련 하위 트리가 읽기 또는 쓰기에 참조될 때마다 게시 인스턴스에 그림자 노드를 설정하는 것입니다.

예를 들어 배포가 TarMK 게시 팜이 있는 [MSRP](msrp.md)라고 가정합니다.

[member](users.md)이(가) pub1에 UGC를 게시하면(MongoDB에 저장됨) 그림자 노드가 pub1의 JCR에 만들어집니다.

pub2에서 UGC를 처음 읽을 때 아무것도 설정되지 않으면 기본 동작은 그림자 노드를 만드는 것입니다.

기본 비헤이비어 이외의 비헤이비어를 원하는 경우 작성자 인스턴스에서 설정하고 모든 게시 인스턴스로 롤포워드해야 합니다(일반적으로 수동 프로세스).
