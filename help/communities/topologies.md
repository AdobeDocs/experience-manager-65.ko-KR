---
title: 커뮤니티를 위한 권장 토폴로지
seo-title: 커뮤니티를 위한 권장 토폴로지
description: 사용자 생성 컨텐츠(UGC)의 처리에 접근하는 방법
seo-description: 사용자 생성 컨텐츠(UGC)의 처리에 접근하는 방법
uuid: 4bc1c423-0ba9-4f2e-b11c-4d6824f45641
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: 46f135de-a0bf-451d-bdcc-fb29188250aa
translation-type: tm+mt
source-git-commit: 612d102b5925704ce459ad818554e487ec0d5355
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---


# 커뮤니티 권장 토폴로지 {#recommended-topologies-for-communities}

AEM Communities 6.1부터는 게시 환경에서 사이트 방문자(구성원)가 제출한 사용자 생성 컨텐츠(UGC)를 처리하기 위한 고유한 방식이 채택되었습니다.

이 방법은 기본적으로 AEM 플랫폼이 작성 환경에서 일반적으로 관리되는 사이트 컨텐츠를 처리하는 방법과 다릅니다.

AEM 플랫폼은 사이트 컨텐츠를 작성자에서 게시로 복제하는 노드 스토어를 사용하는 반면, AEM Communities은 복제되지 않은 UGC용 단일 공용 스토어를 사용합니다.

일반적인 UGC 스토어의 경우 [SRP(저장소 리소스 공급자)](working-with-srp.md)을(를) 선택해야 합니다. 권장되는 방법은 다음과 같습니다.

* [DSRP - 관계형 데이터베이스 저장소 리소스 공급자](dsrp.md)
* [MSRP - MongoDB 저장소 리소스 공급자](msrp.md)
* [ASRP - Adobe 저장소 리소스 공급자](asrp.md)

다른 SRP 옵션인 [JSRP - JCR 저장소 리소스 공급자](jsrp.md)는 작성자 및 두 액세스 모두에 대한 게시 환경을 위한 공통 UGC 저장소를 지원하지 않습니다.

공통 스토어를 요구하면 다음 권장 토폴로지가 나타납니다.

>[!NOTE]
>
>AEM Communities의 경우 [UGC는 결코 복제되지 않습니다](working-with-srp.md#ugc-never-replicated).
>
>배포가 [공통 스토어](working-with-srp.md)를 포함하지 않으면 UGC는 입력한 AEM 게시 또는 작성자 인스턴스에서만 표시됩니다.


>[!NOTE]
>
>AEM 플랫폼에 대한 자세한 내용은 [권장 배포](../../help/sites-deploying/recommended-deploys.md) 및 [AEM 플랫폼 소개](../../help/sites-deploying/data-store-config.md)를 참조하십시오.

## 프로덕션 {#for-production}

UGC를 위한 공용 스토어를 구축하는 것은 필수적이며, 이에 따라 기본 배포는 일반 스토어를 지원할 수 있는 능력에 달려 있습니다.

두 가지 예:

1. 예상 UGC 볼륨이 높고 로컬 MongoDB 인스턴스가 가능한 경우 선택 사항은 [MSRP](msrp.md)입니다.

1. 페이지 컨텐츠에 대한 최적의 성능을 위해 [게시 팜](../../help/sites-deploying/recommended-deploys.md#tarmk-farm) 및 [ASRP](asrp.md)을 선택하면 상대적으로 간단한 작업으로 UGC를 최적의 배율로 확장할 수 있습니다.

두 가지 경우 모두 OAK 마이크로 커널을 기반으로 배포될 수 있습니다.

적절한 공용 스토어를 선택하려면 각 스토어의 고유한 [특성](working-with-srp.md#characteristics-of-srp-options)을 신중하게 고려하십시오.

Oak 마이크로케널에 대한 자세한 내용은 [권장 배포](../../help/sites-deploying/recommended-deploys.md)를 참조하십시오.

### TarMK 게시 팜 {#tarmk-publish-farm}

토폴로지가 게시 팜인 경우 관련 중요 주제는 다음과 같습니다.

* [사용자 동기화](sync.md)
* [사용자 및 사용자 그룹 관리](users.md)

### 권장:DSRP, MSRP 또는 ASRP {#recommended-dsrp-msrp-or-asrp}

| 마이크로 커널 | 사이트 컨텐트 저장소 | 사용자가 생성한 콘텐츠 저장소 | 저장소 리소스 공급자 | 공용 스토어 |
|-------------|------------------------|----------------------------------|---------------------------|---------------|
| 임의 | JCR | MySQL | DSRP | 예 |
| 임의 | JCR | MongoDB | MSRP | 예 |
| 임의 | JCR | Adobe on-demand 스토리지 | ASRP | 예 |

### JSRP {#jsrp}


| 배포 | 사이트 컨텐트 저장소 | 사용자가 생성한 콘텐츠 저장소 | 저장소 리소스 공급자 | 공용 스토어 |
|----------------------|------------------------|----------------------------------|---------------------------|---------------------------------|
| TarMK Farm(기본값) | JCR | JCR | JSRP | 아니오 |
| Oak 클러스터 | JCR | JCR | JSRP | 게시 환경에만 예됨 |

## 개발 {#for-development}

비프로덕션 환경의 경우, 작성자 인스턴스 한 개와 게시 인스턴스 한 개로 개발 환경을 간단히 설정할 수 있는 [JSRP](jsrp.md) 제공

프로덕션에 대해 [ASRP](asrp.md), [DSRP](dsrp.md) 또는 [MSRP](msrp.md)를 선택하는 경우 Adobe 온디맨드 스토리지 또는 MongoDB를 사용하여 유사한 개발 환경을 설정할 수도 있습니다. 예를 보려면 [HowTo Setup MongoDB for Demo](demo-mongo.md)을 참조하십시오.

## 참조 {#references}

* [사용자 동기화](sync.md)

   게시 팜 인스턴스 간의 사용자 데이터 동기화를 설명합니다.

* [사용자 및 사용자 그룹 관리](users.md)

   작성 및 게시 환경에서 사용자 및 사용자 그룹의 역할에 대해 설명합니다.

* UGC [일반 스토어](working-with-srp.md)

   사이트 컨텐츠와 별개의 커뮤니티 콘텐츠의 저장소를 설명합니다.

* [노드 저장소 및 데이터 저장소](../../help/sites-deploying/data-store-config.md)

   기본적으로 사이트 컨텐츠는 노드 스토어에 저장됩니다. 자산에 대해 이진 데이터를 저장하도록 데이터 저장소를 구성할 수 있습니다. 커뮤니티의 경우 SRP를 선택하도록 공용 스토어를 구성해야 합니다.

* [스토리지 요소](../../help/sites-deploying/storage-elements-in-aem-6.md)

   두 노드 스토리지 구현에 대해 설명합니다.Tar와 MongoDB.
