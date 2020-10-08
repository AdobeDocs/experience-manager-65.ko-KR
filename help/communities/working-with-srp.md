---
title: SRP - 커뮤니티 컨텐츠 스토리지
seo-title: SRP - 커뮤니티 컨텐츠 스토리지
description: AEM Communities 6.1부터 사용자가 생성한 컨텐츠(UGC)는 SRP(Storage Resource Provider)가 제공하는 하나의 공용 저장소에 저장됩니다
seo-description: AEM Communities 6.1부터 사용자가 생성한 컨텐츠(UGC)는 SRP(Storage Resource Provider)가 제공하는 하나의 공용 저장소에 저장됩니다
uuid: d45e03c4-378b-4510-a6a0-d48c8cb879d9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 6f13b21a-f4ef-4889-9b8e-4da3f846fa35
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 0%

---


# SRP - 커뮤니티 컨텐츠 스토리지 {#srp-community-content-storage}

## 소개 {#introduction}

AEM Communities 6.1부터 UGC(사용자 생성 컨텐츠)는 SRP(스토리지 리소스 공급자)가 제공하는 단일 공용 저장소에 저장됩니다. ASRP, MSRP 및 JSRP와 같이 선택할 수 있는 여러 SRP 옵션이 있습니다.

이전 릴리스와 달리 AEM 인스턴스 간에 UGC를 역방향/앞으로 복제할 수는 없습니다. 대신 SRP는 JSRP를 제외하고 모든 작성자 및 게시 인스턴스의 CRUD(작성, 읽기, 업데이트 및 삭제) 작업을 위해 UGC에 직접 액세스할 수 있도록 합니다.

다음은 각 SRP 옵션 [의](#characteristics-of-srp-options)특성입니다. 이는 적절한 SRP와 [기본 배포를 선택할 때 의사 결정 프로세스에 필요한 중요한 정보입니다](/help/communities/topologies.md).

UGC 사용에 대한 자세한 내용은 [스토리지 리소스 공급자 개요를 참조하십시오](/help/communities/srp.md).

>[!NOTE]
>
>SRP는 커뮤니티 컨텐츠에만 적용됩니다. 사이트 컨텐츠의 저장 위치([노드 저장소](/help/sites-deploying/data-store-config.md))에는 영향을 주지 않으며 AEM 인스턴스 간 사용자 등록, 사용자 프로필 및 사용자 그룹의 보안 처리에 영향을 주지 않습니다(사용자 데이터 [관리 참조](#managing-user-data)).

>[!CAUTION]
>
>AEM 6.1의 경우 [UGC는 결코 복제되지 않습니다](#ugc-never-replicated).
>
>배포에 기본 JSRP 토폴로지 같은 일반 스토어 [가](/help/communities/topologies.md#jsrp) 포함되지 않으면 UGC는 입력한 AEM 게시 또는 작성자 인스턴스에서만 표시됩니다. 토폴로지에 게시 클러스터가 포함된 경우에만 UGC가 모든 게시 인스턴스에 표시됩니다.

## SRP 옵션 특성 {#characteristics-of-srp-options}

[ASRP - Adobe 저장소 리소스 공급자](/help/communities/asrp.md)

이 옵션을 사용할 경우 UGC는 Adobe에서 호스팅 및 관리되는 클라우드 서비스에 원격으로 유지됩니다. 특정 라이선스에 대한 계정을 제공하려면 추가 라이선스가 필요하며 계정 담당자와 함께 작업해야 합니다. ASRP를 사용하려면 다음이 필요합니다.

* 커뮤니티 콘텐츠를 저장하기 위해 Adobe에서 제공 및 지원하는 관련 클라우드 서비스.
* 특정 지역의 데이터 센터 선택(미국, EMEA, APAC)

* UGC에 대한 모든 프로그래머틱 액세스는 SRP API를 통해 이루어집니다.

ASRP가 적합합니다.

* TarMK 게시 팜의 경우.
* 로컬 스토리지에 투자할 의사가 없는 경우

>[!NOTE]
>
>ASRP의 게시물(또는 댓글)에 첨부 파일을 업로드하는 데는 50MB의 제한이 있습니다.

[MSRP - MongoDB 저장소 리소스 공급자](/help/communities/msrp.md)

이 옵션을 사용하면 UGC가 로컬 MongoDB 인스턴스에 직접 유지됩니다.

MSRP의 요구:

* 커뮤니티 콘텐츠를 저장할 수 있는 MongoDB의 라이센스가 허용하는 로컬 설치입니다.
* Apache Solr의 로컬 설치
* UGC에 대한 모든 프로그래머틱 액세스는 SRP API를 통해 이루어집니다.

ASRP가 적합합니다.

* 기존 TarMK 게시 팜의 경우.
* MongoMK 또는 RdbMK 클러스터의 경우
* 대량의 커뮤니티 컨텐츠가 필요합니다.

[DSRP - 관계형 데이터베이스 저장소 리소스 공급자](/help/communities/dsrp.md)

이 옵션을 사용하면 UGC가 로컬 MySQL 데이터베이스 인스턴스에 직접 유지됩니다.

DSRP의 요구:

* 커뮤니티 콘텐츠를 저장할 MySQL의 로컬 설치
* Apache Solr의 로컬 설치
* UGC에 대한 모든 프로그래머틱 액세스는 SRP API를 통해 이루어집니다.

DSRP가 적절합니다.

* 기존 TarMK 게시 팜의 경우.
* MongoMK 또는 RdbMK 클러스터의 경우
* 대량의 커뮤니티 컨텐츠가 필요합니다.

[JSRP - JCR 스토리지 리소스 공급자](/help/communities/jsrp.md)

기본 옵션을 사용할 경우 일반 스토어가 없습니다. UGC는 입력되는 AEM 인스턴스와 동일한 JCR 보관소에서만 유지됩니다.

JSRP:

* AEM 작성자 또는 게시된 게시 인스턴스의 JCR 저장소에 커뮤니티 컨텐츠를 저장합니다.
* SRP API를 통해 UGC에 대한 모든 프로그래머틱 액세스가 필요합니다.
* 둘 이상의 게시 인스턴스가 배포된 경우 게시 클러스터가 필요합니다(TarMK 팜의 게시 인스턴스 간에 복제 메커니즘이 없음).
* 중재는 게시 환경에서만 수행됩니다(작성자와 게시 간에 역방향/전달 복제 메커니즘이 없음).
* 개발, 데모 및 트레이닝에 가장 적합합니다.

## SRP 구성 {#configuring-srp}

기본 스토리지 옵션 지정은 기본 배포에 따라 [스토리지 구성 콘솔을 통해 수행됩니다](/help/communities/srp-config.md).

각 옵션에 대한 구성 세부 사항은 다음을 참조하십시오.

* [ASRP - Adobe 저장소 리소스 공급자](/help/communities/asrp.md)
* [MSRP - MongoDB 저장소 리소스 공급자](/help/communities/msrp.md)
* [DSRP - 관계형 데이터베이스 저장소 리소스 공급자](/help/communities/dsrp.md)
* [JSRP - JCR 스토리지 리소스 공급자](/help/communities/jsrp.md)

스토리지 옵션을 적극적으로 선택하지 않으면 기본적으로 JSRP가 활성화됩니다.

## 추가 정보 {#additional-information}

### UGC 복제 안 함 {#ugc-never-replicated}

작성 환경에서 작성자는 페이지 컨텐츠를 만들어 게시 환경에 복제합니다. 페이지에 댓글, 검토, 포럼, 블로그 또는 QnA와 같은 인터랙티브한 AEM Communities 기능이 포함되어 있는 경우, 게시 인스턴스에서 멤버(로그인된 사이트 방문자)의 상호 작용으로 인해 게시 환경에 입력된 사용자 생성 컨텐츠(UGC)가 나타납니다.

이전에는 이 커뮤니티 컨텐츠가 작성자 인스턴스로 역복제되었고 작성자가 복제하여 게시 인스턴스로 복제되었습니다. 역 / 전방 복제를 통해 AEM 인스턴스 간의 일관성을 유지하는 것은 문제가 있었습니다.

AEM Communities 6.1부터 위에 설명된 바와 같이 UGC용 공유 스토리지를 사용하여 UGC의 복제 필요성을 제거했습니다.

사이트 컨텐츠가 복제되는 동안 UGC는 복제되지 않습니다.

### 사용자 데이터 관리 {#managing-user-data}

CommunitIes에 대한 관심 [*은 사용자*, *사용자 그룹*&#x200B;및 *사용자 프로필입니다*](/help/communities/users.md). 게시 환경에서 생성 및 업데이트되는 이 사용자 관련 데이터는 토폴로지가 [게시 팜일 때 다른 게시 인스턴스에서 사용할 수 있어야 합니다](/help/sites-deploying/recommended-deploys.md#tarmk-farm).

AEM Communities 6.1부터 사용자 관련 데이터는 복제 대신 Sling 배포를 사용하여 동기화됩니다. 자세한 내용은 [사용자 동기화를 참조하십시오](/help/communities/sync.md).

### Upgrading to AEM Communities 6.5 {#upgrading-to-aem-communities}

AEM 6.5 Communities로 업그레이드할 때 기존 UGC를 보존해야 하는 경우 AEM 5.6.1 또는 AEM 6.0 커뮤니티에서 Adobe on-demand 스토리지 또는 UGC의 온-프레미스 스토리지를 사용하는지 여부에 따라 단계를 수행해야 합니다.

자세한 내용은 AEM Communities [6.5로 업그레이드를 참조하십시오](/help/communities/upgrade.md).
