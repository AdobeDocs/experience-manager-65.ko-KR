---
title: 저장소 리소스 공급자 개요
seo-title: 저장소 리소스 공급자 개요
description: 커뮤니티를 위한 공용 스토리지
seo-description: 커뮤니티를 위한 공용 스토리지
uuid: abdf4e5a-767b-428f-9aa4-0dc06819a26e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 63abeda4-6ea1-4b45-b188-f9c6b44ca0cd
translation-type: tm+mt
source-git-commit: 3296db289b2e2f4ca0d1981597ada6ca1310bd46

---


# 저장소 리소스 공급자 개요 {#storage-resource-provider-overview}

## 소개 {#introduction}

AEM Communities 6.1부터 UGC(사용자 생성 콘텐츠)라고 하는 커뮤니티 컨텐츠는 [스토리지 리소스 공급자](working-with-srp.md) (SRP)가 제공하는 단일 공용 저장소에 저장됩니다.

SRP 옵션에는 여러 가지가 있습니다. 이 옵션에는 모두 새로운 AEM Communities 인터페이스, SRP [API](srp-and-ugc.md) (SocialResourceProvider API)를 통해 UGC에 액세스할 수 있으며 여기에는 모든 CRD(만들기, 읽기, 업데이트 및 삭제) 작업이 포함됩니다.

모든 SCF 구성 요소는 SRP API를 사용하여 구현되므로 [기본 토폴로지](topologies.md) 또는 UGC 위치에 대한 지식 없이도 코드를 개발할 수 있습니다.

***SocialResourceProvider API 파섹***

>[!NOTE]
>
>**사용자 지정 구성 요소**:AEM Communities의 라이센스 고객의 경우, SRP API는 기본 토폴로지와 관계없이 UGC에 액세스할 수 있도록 사용자 지정 구성 요소의 개발자가 사용할 수 있습니다. SRP [및 UGC Essentials를 참조하십시오](srp-and-ugc.md).

참고 항목:

* [SRP 및 UGC Essentials](srp-and-ugc.md) - SRP 유틸리티 방법 및 예
* [SRP를 사용하여 UGC에](accessing-ugc-with-srp.md) 액세스 - 코딩 지침
* [SocialUtils 리팩토링](socialutils.md) - 사용되지 않는 유틸리티 메서드를 현재 SRP 유틸리티 메서드에 매핑합니다.

## 저장소 정보 {#about-the-repository}

SRP를 이해하려면 AEM 커뮤니티 사이트에서 AEM 리포지토리(OAK)의 역할을 이해하는 데 유용합니다.

**Java 컨텐츠 저장소(JCR)**&#x200B;이 표준은 컨텐츠 저장소에 대한 데이터 모델 및 JCR[API](https://jackrabbit.apache.org/jcr/jcr-api.html)(응용 프로그램 프로그래밍 인터페이스)를 정의합니다. 기존 파일 시스템의 특징과 관계형 데이터베이스의 특성을 결합하고 컨텐츠 애플리케이션에 자주 필요한 다양한 추가 기능을 추가합니다.

JCR의 한 가지 구현은 AEM 리포지토리, OAK입니다.

**OAK(Apache Jackrabbit Oak)**[](../../help/sites-deploying/platform.md) 은 컨텐츠 중심 애플리케이션을 위해 특별히 설계된 데이터 스토리지 시스템인 JCR 2.0의 구현입니다. 비정형 및 반정형 데이터를 위해 설계된 계층적 데이터베이스 유형입니다. 저장소에는 사용자 중심의 컨텐츠뿐만 아니라 애플리케이션에서 사용되는 모든 코드, 템플릿 및 내부 데이터가 저장됩니다. 컨텐츠에 액세스하기 위한 UI는 CRXDE Lite [입니다](../../help/sites-developing/developing-with-crxde-lite.md).

JCR과 OAK 모두 일반적으로 AEM 저장소를 참조하는 데 사용됩니다.

비공개 작성 환경에서 사이트 컨텐츠를 개발한 후 공개 게시 환경에 복사해야 합니다. 이는 종종 *[복제라는](deploy-communities.md#replication-agents-on-author)*작업을 통해 수행됩니다. 이 문제는 작성자/개발자/관리자가 제어합니다.

UGC의 경우 컨텐츠는 공개 게시 환경에서 등록된 사이트 방문자(커뮤니티 구성원)에 의해 입력됩니다. 이것은 무작위로 발생합니다.

관리 및 보고를 위해 비공개 작성 환경에서 UGC에 액세스하는 것이 유용합니다. SRP를 사용하면 작성자가 UGC에 액세스할 수 있으므로 제작 시 역복제가 필요하지 않으므로 더욱 일관되고 성능이 향상됩니다.

## SRP 정보 {#about-srp}

UGC가 공유 스토리지에 저장되면 대부분의 배포에서 작성 환경과 게시 환경 모두에서 액세스할 수 있는 단일 멤버 컨텐츠 인스턴스가 있습니다. SRP 선택(MSRP, ASRP, JSRP)에 상관없이 SRP API를 사용하여 프로그래밍 방식으로 모두 액세스해야 합니다.

>[!NOTE]
>
>샘플 [코드 및 자세한 내용은 SRP](srp-and-ugc.md) 및 UGC Essentials를 참조하십시오.
>
>코딩 [시 모범 사례를 보려면 SRP를](accessing-ugc-with-srp.md) 사용하여 UGC 액세스를 참조하십시오.


### ASRP {#asrp}

ASRP의 경우 UGC는 JCR에 저장되지 않으며 Adobe에서 호스팅 및 관리하는 클라우드 서비스에 저장됩니다. ASRP 파섹

ASRP [- Adobe Storage Resource Provider를 참조하십시오](asrp.md).

개발자는 UGC에 직접 액세스할 수 없습니다.

ASRP 파섹

### MSRP {#msrp}

MSRP의 경우 UGC는 JCR에 저장되지 않고 MongoDB에 저장됩니다. MSRP에 저장된 UGC는 CRXDE Lite에서 볼 수 없으며 JCR API를 사용하여 액세스할 수 없습니다.

MSRP [- MongoDB 저장소 리소스 공급자를 참조하십시오](msrp.md).

MSRP는 ASRP와 비교할 수 있지만 모든 AEM 서버 인스턴스가 동일한 UGC에 액세스하고 있으므로 공통 도구를 사용하여 MongoDB에 저장된 UGC에 직접 액세스할 수 있습니다.

MSRP 파섹

### JSRP {#jsrp}

JSRP는 단일 AEM 인스턴스에서 모든 UGC에 액세스하는 기본 공급자입니다. MSRP 또는 ASRP를 설정하지 않고도 AEM Communities 6.1을 빠르게 경험할 수 있습니다.

JSRP [- JCR 스토리지 리소스 공급자를 참조하십시오](jsrp.md).

JSRP의 경우 UGC는 JCR에 저장되어 CRXDE Lite 및 JCR API를 통해 액세스할 수 있지만 JCR API를 사용하지 않는 것이 좋습니다. 그렇지 않으면 향후 변경 사항이 사용자 지정 코드에 영향을 줄 수 있습니다.

또한 작성 및 게시 환경에 대한 저장소가 공유되지 않습니다. 게시 인스턴스의 클러스터로 인해 공유 게시 저장소가 만들어지지만, 게시에 입력된 UGC는 작성자에 표시되지 않으므로 작성자의 UGC를 관리할 수 없습니다. UGC는 AEM 저장소가 입력된 인스턴스의 JCR(JCR)에만 보관됩니다.

JSRP는 쿼리에 Oak 색인을 사용합니다.

## JCR의 그림자 노드 정보 {#about-shadow-nodes-in-jcr}

UGC 경로를 모방하는 그림자 노드는 다음 두 가지 목적을 위해 로컬 저장소에 있습니다.

1. [액세스 제어(ACL)](#for-access-control-acls)
1. [기존 리소스 없음(NER)](#for-non-existing-resources-ners)

SRP 구현과 관계없이 실제 UGC는 그림자 노드와 동일한 위치에 표시되지 않습니다.

### ACL(액세스 제어) {#for-access-control-acls}

ASRP 및 MSRP와 같은 일부 SRP 구현은 ACL 확인을 제공하지 않는 데이터베이스에 커뮤니티 컨텐츠를 저장합니다. 섀도 노드는 로컬 리포지토리에서 ACL을 적용할 수 있는 위치를 제공합니다.

SRP API를 사용하는 모든 SRP 옵션은 모든 CRUD 작업 전에 그림자 위치를 동일하게 확인합니다.

ACL 검사는 리소스의 UGC에 적용된 권한을 확인하는 데 적합한 경로를 반환하는 유틸리티 메서드를 사용합니다.

샘플 [코드는 SRP 및 UGC](srp-and-ugc.md) Essentials를 참조하십시오.

### 존재하지 않는 리소스(NER) {#for-non-existing-resources-ners}

일부 Communities 구성 요소는 스크립트 내에서 포함할 수 있으므로 Sling 지정 가능 노드가 Communities 기능을 지원해야 합니다. [포함된 구성 요소는](scf.md#add-or-include-a-communities-component) 존재하지 않는 리소스(NER)라고 합니다.

섀도 노드는 저장소에서 Sling 지정 가능 위치를 제공합니다.

>[!CAUTION]
>
>그림자 노드에 여러 가지 사용이 있으므로 그림자 노드가 존재한다고 해서 구성 요소가 NER임을 의미하지는 *않습니다* .


### 저장소 위치 {#storage-location}

다음은 커뮤니티 구성 요소 안내서의 [댓글 구성 요소를](http://localhost:4502/content/community-components/en/comments.html) 사용하는 [그림자 노드의 예입니다](components-guide.md).

* 구성 요소는 다음 위치에 로컬 저장소에 있습니다.

   `/content/community-components/en/comments/jcr:content/content/includable/comments`

* 해당 섀도 노드는 다음 로컬 저장소에 있습니다.

   `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

그림자 노드 아래에 UGC가 없습니다.

기본 동작은 관련 하위 트리가 읽기 또는 쓰기에 대해 참조될 때마다 게시 인스턴스에 섀도 노드를 설정하는 것입니다.

예를 들어 배포가 TarMK [게시](msrp.md) 팜과 함께 MSRP라고 가정합니다.

한 [멤버가](users.md) pub1에 UGC를 게시하면(MongoDB에 저장됨), pub1의 JCR에 섀도 노드가 만들어집니다.

pub2에서 UGC를 처음 읽을 때 아무 것도 설정되지 않은 경우 기본 동작은 섀도 노드를 만드는 것입니다.

기본 비헤이비어가 필요한 경우 작성 인스턴스에서 설정하고 모든 게시 인스턴스로 롤포워드해야 합니다. 이 인스턴스는 일반적으로 수동 프로세스입니다.
