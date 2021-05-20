---
title: 저장소 리소스 공급자 개요
seo-title: 저장소 리소스 공급자 개요
description: 커뮤니티의 공통 스토리지
seo-description: 커뮤니티의 공통 스토리지
uuid: abdf4e5a-767b-428f-9aa4-0dc06819a26e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 63abeda4-6ea1-4b45-b188-f9c6b44ca0cd
exl-id: 5f313274-1a2a-4e83-9289-60a4729b99b4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 0%

---

# 저장소 리소스 공급자 개요 {#storage-resource-provider-overview}

## 소개 {#introduction}

AEM Communities 6.1부터, 일반적으로 UGC(사용자 생성 컨텐츠)라고 하는 커뮤니티 컨텐츠는 [스토리지 리소스 공급자](working-with-srp.md) (SRP)가 제공하는 단일 공통 저장소에 저장됩니다.

여러 가지 SRP 옵션이 있으며, 이러한 모든 옵션 중 하나가 새 AEM Communities 인터페이스를 통해 UGC에 액세스합니다. [SocialResourceProvider API](srp-and-ugc.md)(SRP API), 여기에는 모든 생성, 읽기, 업데이트 및 삭제(CRUD) 작업이 포함됩니다.

모든 SCF 구성 요소는 SRP API를 사용하여 구현되므로 [기본 토폴로지](topologies.md) 또는 UGC의 위치를 알지 않고도 코드를 개발할 수 있습니다.

***SocialResourceProvider API는 AEM Communities의 라이선스가 있는 고객만 사용할 수 있습니다.***

>[!NOTE]
>
>**사용자 지정 구성 요소**:AEM Communities의 라이선스가 있는 고객의 경우 SRP API는 기본 토폴로지에 관계없이 UGC에 액세스할 목적으로 사용자 지정 구성 요소 개발자가 사용할 수 있습니다. [SRP 및 UGC 필수 패키지](srp-and-ugc.md)를 참조하십시오.

참고 항목:

* [SRP 및 UGC Essentials](srp-and-ugc.md)  - SRP 유틸리티 메서드 및 예제.
* [SRP를 사용하여 UGC 액세스](accessing-ugc-with-srp.md)  - 코딩 지침.
* [SocialUtils 리팩터링](socialutils.md)  - 사용 중단된 유틸리티 메서드를 현재 SRP 유틸리티 메서드에 매핑합니다.

## 저장소 {#about-the-repository} 정보

SRP를 이해하려면 AEM 커뮤니티 사이트에서 AEM 저장소(OAK)의 역할을 이해하는 데 유용합니다.

**JCR(Java Content Repository)**
이 표준은 컨텐츠 저장소에 대한 데이터 모델 및 JCR [API](https://jackrabbit.apache.org/jcr/jcr-api.html)(응용 프로그램 프로그래밍 인터페이스)를 정의합니다. 기존 파일 시스템의 특징과 관계형 데이터베이스의 특성을 결합하고 컨텐츠 응용 프로그램에서 자주 필요로 하는 많은 추가 기능을 추가합니다.

JCR의 한 구현은 AEM 저장소인 OAK입니다.

**Apache Jackrabbit Oak(OAK)**
[](../../help/sites-deploying/platform.md) 는 컨텐츠 중심의 애플리케이션용으로 특별히 설계된 데이터 스토리지 시스템인 JCR 2.0의 구현입니다. 비정형 데이터와 반정형 데이터를 위해 설계된 계층적 데이터베이스 유형입니다. 저장소는 사용자 대상 컨텐츠뿐만 아니라 애플리케이션에서 사용하는 모든 코드, 템플릿 및 내부 데이터도 저장합니다. 컨텐츠에 액세스하기 위한 UI는 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)입니다.

JCR과 OAK 모두 일반적으로 AEM 저장소를 참조하는 데 사용됩니다.

비공개 작성 환경에서 사이트 컨텐츠를 작성한 후 공개 게시 환경에 복사해야 합니다. 이 작업은 종종 *[replication](deploy-communities.md#replication-agents-on-author)*&#x200B;이라는 작업을 통해 수행됩니다. 이 작업은 작성자/개발자/관리자가 제어합니다.

UGC의 경우 공개 게시 환경에서 등록된 사이트 방문자(커뮤니티 구성원)가 콘텐츠를 입력합니다. 이 작업은 임의로 수행됩니다.

관리 및 보고를 위해 개인 작성 환경에서 UGC에 액세스할 수 있는 것이 유용합니다. SRP를 사용하면 게시에서 작성자로 역 복제가 필요하지 않으므로 작성자의 UGC에 대한 액세스가 보다 일관되고 성능이 향상됩니다.

## SRP {#about-srp} 정보

UGC가 공유 저장소에 저장되면 대부분의 배포에서 작성자와 게시 환경 모두에서 액세스할 수 있는 멤버 컨텐츠의 단일 인스턴스가 있습니다. SRP 선택(MSRP, ASRP, JSRP)에 관계없이 모두 SRP API를 사용하여 프로그래밍 방식으로 액세스해야 합니다.

>[!NOTE]
>
>샘플 코드 및 추가 세부 정보는 [SRP 및 UGC Essentials](srp-and-ugc.md) 를 참조하십시오.
>
>코딩 시 모범 사례가 필요하면 [SRP](accessing-ugc-with-srp.md)로 UGC 액세스 를 참조하십시오.

### ASRP {#asrp}

ASRP의 경우 UGC는 JCR에 저장되지 않고 Adobe에서 호스팅 및 관리하는 클라우드 서비스에 저장됩니다. ASRP에 저장된 UGC는 CRXDE Lite을 사용하여 보거나 JCR API를 사용하여 액세스할 수 없습니다.

[ASRP - Adobe 저장소 리소스 공급자](asrp.md)를 참조하십시오.

개발자가 UGC에 직접 액세스할 수는 없습니다.

ASRP는 쿼리에 Adobe 클라우드를 사용합니다.

### MSRP {#msrp}

MSRP의 경우 UGC는 JCR에 저장되지 않고 MongoDB에 저장됩니다. MSRP에 저장된 UGC는 CRXDE Lite을 사용하여 보거나 JCR API를 사용하여 액세스할 수 없습니다.

[MSRP - MongoDB 저장소 리소스 공급자](msrp.md)를 참조하십시오.

MSRP는 ASRP와 비교할 수 있지만 모든 AEM 서버 인스턴스가 동일한 UGC에 액세스하고 있으므로, 일반적인 도구를 사용하여 MongoDB에 저장된 UGC에 직접 액세스할 수 있습니다.

MSRP는 쿼리에 Solr을 사용합니다.

### JSRP {#jsrp}

JSRP는 단일 AEM 인스턴스의 모든 UGC에 액세스하는 기본 공급자입니다. MSRP 또는 ASRP를 설정하지 않고도 AEM Communities 6.1을 빠르게 경험할 수 있는 기능을 제공합니다.

[JSRP - JCR 저장소 리소스 공급자](jsrp.md)를 참조하십시오.

JSRP의 경우, UGC가 JCR에 저장되고 CRXDE Lite 및 JCR API를 모두 통해 액세스할 수 있는 경우, JCR API를 사용하지 않는 것이 좋습니다. 그렇지 않으면 향후 변경 사항이 사용자 지정 코드에 영향을 줄 수 있습니다.

또한 작성 및 게시 환경에 대한 리포지토리는 공유되지 않습니다. 게시 인스턴스 클러스터는 공유 게시 리포지토리를 생성하지만 게시에 입력한 UGC는 작성자에게 표시되지 않으므로 작성자의 UGC를 관리할 수 없습니다. UGC는 인스턴스가 입력된 인스턴스의 AEM 저장소(JCR)에만 유지됩니다.

JSRP는 쿼리에 Oak 인덱스를 사용합니다.

## JCR의 섀도 노드 정보 {#about-shadow-nodes-in-jcr}

UGC의 경로를 모방하는 그림자 노드는 두 가지 목적을 위해 로컬 저장소에 있습니다.

1. [액세스 제어(ACL)](#for-access-control-acls)
1. [존재하지 않는 리소스(NER)](#for-non-existing-resources-ners)

SRP 구현에 관계없이 실제 UGC는 섀도 노드와 동일한 위치에 *표시되지 않습니다.

### ACL(액세스 제어)의 경우 {#for-access-control-acls}

ASRP 및 MSRP와 같은 일부 SRP 구현은 ACL 확인을 제공하지 않는 데이터베이스에 커뮤니티 콘텐츠를 저장합니다. 섀도 노드는 ACL을 적용할 수 있는 로컬 저장소의 위치를 제공합니다.

SRP API를 사용하여 모든 SRP 옵션은 모든 CRUD 작업 전에 섀도 위치를 동일한 검사를 수행합니다.

ACL 확인에서는 리소스의 UGC에 적용된 권한을 확인하는 데 적합한 경로를 반환하는 유틸리티 메서드를 사용합니다.

샘플 코드가 필요하면 [SRP 및 UGC Essentials](srp-and-ugc.md)를 참조하십시오.

### 존재하지 않는 리소스(NER)의 경우 {#for-non-existing-resources-ners}

일부 Communities 구성 요소는 스크립트 내에 포함할 수 있으므로 커뮤니티 기능을 지원하려면 Sling 주소 지정 가능 노드가 필요합니다. [포함된 ](scf.md#add-or-include-a-communities-component) 구성 요소는 존재하지 않는 리소스(NER)라고 합니다.

섀도 노드는 저장소에서 Sling 주소 지정 가능 위치를 제공합니다.

>[!CAUTION]
>
>섀도 노드의 사용이 여러 개인 경우 섀도 노드의 존재 여부는 *not*&#x200B;구성 요소가 NER임을 의미합니다.

### 저장소 위치 {#storage-location}

다음은 [커뮤니티 구성 요소 안내서](components-guide.md)에서 [Comments 구성 요소](http://localhost:4502/content/community-components/en/comments.html)를 사용하는 섀도 노드의 예입니다.

* 구성 요소는 다음과 같은 로컬 저장소에 있습니다.

   `/content/community-components/en/comments/jcr:content/content/includable/comments`

* 해당 섀도 노드는 다음 로컬 저장소에 있습니다.

   `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

섀도 노드 아래에 UGC가 없습니다.

기본 동작은 관련 하위 트리가 읽기 또는 쓰기에 대해 참조될 때마다 게시 인스턴스에 섀도 노드를 설정하는 것입니다.

예를 들어 배포가 TarMK 게시 팜이 있는 [MSRP](msrp.md)라고 가정해 보겠습니다.

[member](users.md)가 pub1(MongoDB에 저장됨)에 UGC를 게시하면 pub1의 JCR에서 섀도 노드가 생성됩니다.

pub2에서 UGC를 처음 읽을 때 아무 것도 설정되지 않은 경우 기본 동작은 섀도 노드를 만드는 것입니다.

기본 동작 이외의 작업을 원하는 경우 작성 인스턴스에서 설정하고 일반적으로 수동 프로세스인 모든 게시 인스턴스로 롤포워드해야 합니다.
