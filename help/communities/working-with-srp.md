---
title: SRP - 커뮤니티 콘텐츠 저장소
description: AEM Communities 6.1부터 UGC(사용자 생성 컨텐츠)는 SRP(저장소 리소스 제공자)가 제공하는 하나의 공통 저장소에 저장됩니다
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: e29aae44-67be-43d2-8004-c986412d9e63
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 0%

---

# SRP - 커뮤니티 콘텐츠 저장소 {#srp-community-content-storage}

## 소개 {#introduction}

AEM Communities 6.1부터 UGC(사용자 생성 컨텐츠)는 SRP(저장소 리소스 제공자)가 제공하는 하나의 공통 저장소에 저장됩니다. ASRP, MSRP 및 JSRP와 같이 선택할 수 있는 여러 SRP 옵션이 있습니다.

이전 릴리스와 달리 AEM 인스턴스에는 UGC의 역방향/순방향 복제가 없습니다. 대신 SRP는 JSRP를 제외하고 모든 작성자 및 게시 인스턴스에서 CRUD(만들기, 읽기, 업데이트 및 삭제) 작업을 위해 UGC에 직접 액세스할 수 있도록 합니다.

다음은 [각 SRP 옵션의 특성](#characteristics-of-srp-options): 적절한 SRP를 선택하고 [기본 배포](/help/communities/topologies.md).

UGC용 SRP 사용에 대한 자세한 내용은 다음을 참조하십시오. [저장소 리소스 공급자 개요](/help/communities/srp.md).

>[!NOTE]
>
>SRP는 커뮤니티 콘텐츠에만 적용됩니다. 사이트 컨텐츠가 저장되는 위치에는 영향을 주지 않습니다([노드 저장소](/help/sites-deploying/data-store-config.md)), 그리고 는 AEM 인스턴스 간의 사용자 등록, 사용자 프로필 및 사용자 그룹의 보안 처리에 영향을 주지 않습니다(참조) [사용자 데이터 관리](#managing-user-data)).

>[!CAUTION]
>
>AEM 6.1부터 [UGC는 복제되지 않음](#ugc-never-replicated).
>
>배포에 기본값과 같은 공통 저장소가 포함되지 않는 경우 [JSRP](/help/communities/topologies.md#jsrp) 토폴로지, UGC는 입력된 AEM 게시 또는 작성자 인스턴스에서만 볼 수 있습니다. 토폴로지에 게시 클러스터가 포함된 경우에만 UGC가 게시 인스턴스에 표시됩니다.

## SRP 옵션의 특성 {#characteristics-of-srp-options}

[ASRP - Adobe 저장소 리소스 제공자](/help/communities/asrp.md)

이 옵션을 사용하면 UGC는 Adobe에서 호스팅 및 관리하는 클라우드 서비스에서 원격으로 유지됩니다. 추가 라이선스가 필요하며 계정 담당자와 협력하여 해당 특정 라이선스에 대한 계정을 프로비저닝해야 합니다. ASRP에는 다음이 필요합니다.

* 커뮤니티 콘텐츠를 저장하기 위해 Adobe이 제공 및 지원하는 관련 클라우드 서비스.
* 특정 지역(미국, EMEA, APAC)에서 데이터 센터 선택

* UGC에 대한 모든 프로그래밍 방식 액세스는 SRP API를 통해 이루어져야 합니다.

ASRP가 적합한 경우:

* TarMK 게시 팜의 경우.
* 로컬 스토리지에 투자할 의사가 없는 경우

>[!NOTE]
>
>ASRP의 게시물(또는 댓글)에 첨부 파일을 업로드하는 데에는 50MB의 제한이 있습니다.

[MSRP - MongoDB 저장소 리소스 공급자](/help/communities/msrp.md)

이 옵션을 사용하면 UGC가 로컬 MongoDB 인스턴스에서 직접 유지됩니다.

MSRP에 필요한 사항:

* 커뮤니티 콘텐츠를 저장할 MongoDB의 사용이 허가된 로컬 설치입니다.
* Apache Solr의 로컬 설치
* UGC에 대한 모든 프로그래밍 방식 액세스는 SRP API를 통해 이루어져야 합니다.

ASRP가 적합한 경우:

* 기존 TarMK 게시 팜의 경우
* MongoMK 또는 RdbMK 클러스터의 경우.
* 대량의 커뮤니티 컨텐츠가 필요한 경우.

[DSRP - 관계형 데이터베이스 저장소 리소스 제공자](/help/communities/dsrp.md)

이 옵션을 사용하면 UGC가 로컬 MySQL 데이터베이스 인스턴스에서 직접 유지됩니다.

DSRP를 사용하려면 다음 요구 사항이 필요합니다.

* 커뮤니티 콘텐츠를 저장할 MySQL의 로컬 설치입니다.
* Apache Solr의 로컬 설치
* UGC에 대한 모든 프로그래밍 방식 액세스는 SRP API를 통해 이루어져야 합니다.

DSRP는 다음 경우에 적합합니다.

* 기존 TarMK 게시 팜의 경우
* MongoMK 또는 RdbMK 클러스터의 경우.
* 대량의 커뮤니티 컨텐츠가 필요한 경우.

[JSRP - JCR 저장소 리소스 제공자](/help/communities/jsrp.md)

기본 옵션을 사용하면 공통 저장소가 없습니다. UGC는 입력된 AEM 인스턴스와 동일한 JCR 저장소에서만 유지됩니다.

JSRP:

* 커뮤니티 콘텐츠가 게시된 AEM 작성자 또는 게시 인스턴스의 JCR 저장소에 커뮤니티 콘텐츠를 저장합니다.
* SRP API를 통해 UGC에 대한 모든 프로그래밍 방식 액세스 필요.
* 둘 이상의 게시 인스턴스가 배포된 경우 게시 클러스터가 필요합니다(TarMK 팜의 게시 인스턴스 간에 복제 메커니즘이 없음).
* 조정은 게시 환경에서만 수행됩니다(작성자와 게시 간에 역방향/순방향 복제 메커니즘이 없음).
* 는 개발, 데모 및 교육에 가장 적합합니다.

## SRP 구성 {#configuring-srp}

기본 배포를 기반으로 기본 저장소 옵션을 지정하는 작업은 [스토리지 구성 콘솔](/help/communities/srp-config.md).

각 옵션에 대한 구성 세부 정보는 다음을 참조하십시오.

* [ASRP - Adobe 저장소 리소스 제공자](/help/communities/asrp.md)
* [MSRP - MongoDB 저장소 리소스 공급자](/help/communities/msrp.md)
* [DSRP - 관계형 데이터베이스 저장소 리소스 제공자](/help/communities/dsrp.md)
* [JSRP - JCR 저장소 리소스 제공자](/help/communities/jsrp.md)

스토리지 옵션을 선택하지 않으면 기본적으로 JSRP가 활성화됩니다.

## 추가 정보 {#additional-information}

### UGC 복제 안 함 {#ugc-never-replicated}

작성 환경에서 작성자는 페이지 콘텐츠를 만들고 게시 환경에 복제합니다. 페이지에 댓글, 리뷰, 포럼, 블로그 또는 QnA와 같은 대화형 AEM Communities 기능이 포함된 경우, 게시 인스턴스에서 멤버(로그인한 사이트 방문자)의 상호 작용으로 인해 UGC(사용자가 생성한 컨텐츠)가 게시 환경에 입력됩니다.

이전에는 이 커뮤니티 콘텐츠가 작성자 인스턴스에 역복제되고 작성자 인스턴스에서 게시 인스턴스에 복제되었습니다. 역방향 및 정방향 복제를 사용하여 AEM 인스턴스 간의 일관성을 유지하는 데 문제가 있었습니다.

AEM Communities 6.1부터는 위에서 설명한 대로 UGC에 공유 스토리지를 사용하여 UGC 복제의 필요성을 제거했습니다.

사이트 콘텐츠가 복제되는 동안 UGC는 복제되지 않습니다.

### 사용자 데이터 관리 {#managing-user-data}

또한 ComunitIes의 관심 분야는 다음과 같습니다. [*사용자*, *사용자 그룹*, 및 *사용자 프로필*](/help/communities/users.md). 게시 환경에서 만들고 업데이트할 때 이 사용자 관련 데이터는 토폴로지가 인 경우 다른 게시 인스턴스에서 사용할 수 있도록 해야 합니다. [팜 게시](/help/sites-deploying/recommended-deploys.md#tarmk-farm).

AEM Communities 6.1부터는 복제 대신 Sling 배포를 사용하여 사용자 관련 데이터가 동기화됩니다. 자세한 내용은 다음을 참조하십시오. [사용자 동기화](/help/communities/sync.md).

### AEM Communities 6.5로 업그레이드 {#upgrading-to-aem-communities}

AEM 6.5 커뮤니티로 업그레이드할 때 기존 UGC를 유지해야 하는 경우 AEM 5.6.1 또는 AEM 6.0 커뮤니티에서 UGC의 Adobe 온디맨드 스토리지를 사용했는지 또는 온프레미스 스토리지를 사용했는지에 따라 단계를 수행해야 합니다.

자세한 내용은 다음을 참조하십시오. [AEM Communities 6.5로 업그레이드](/help/communities/upgrade.md).
