---
title: 커뮤니티에 대한 권장 토폴로지
seo-title: Recommended Topologies for Communities
description: UGC(사용자 생성 컨텐츠)를 처리하는 방법
seo-description: How to approach the handling of user-generated content (UGC)
uuid: 4bc1c423-0ba9-4f2e-b11c-4d6824f45641
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: 46f135de-a0bf-451d-bdcc-fb29188250aa
exl-id: b6658330-d862-44e3-aac0-824fb91cd087
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 1%

---

# 커뮤니티에 대한 권장 토폴로지 {#recommended-topologies-for-communities}

AEM Communities 6.1부터는 게시 환경에서 사이트 방문자(구성원)가 제출한 사용자 생성 콘텐츠(UGC)를 처리하는 데 고유한 접근 방식이 채택되었습니다.

이 접근 방식은 AEM 플랫폼이 작성 환경에서 일반적으로 관리되는 사이트 컨텐츠를 처리하는 방식과 근본적으로 다릅니다.

AEM 플랫폼에서는 작성자에서 게시로 사이트 컨텐츠를 복제하는 노드 저장소를 사용하는 반면, AEM Communities에서는 복제되지 않은 UGC용 단일 공통 저장소를 사용합니다.

일반 UGC 스토어의 경우 [저장소 리소스 공급자(SRP)](working-with-srp.md). 권장되는 선택 사항은 다음과 같습니다.

* [DSRP - 관계형 데이터베이스 저장소 리소스 공급자](dsrp.md)
* [MSRP - MongoDB 저장소 리소스 공급자](msrp.md)
* [ASRP - Adobe 저장소 리소스 공급자](asrp.md)

다른 SRP 옵션 [JSRP - JCR 저장소 리소스 공급자](jsrp.md)에서는 두 액세스 모두에 대한 작성자 및 게시 환경을 위한 일반적인 UGC 저장소를 지원하지 않습니다.

공통 저장소를 필요로 하면 다음과 같은 권장 토폴로지가 표시됩니다.

>[!NOTE]
>
>AEM Communities의 경우, [UGC는 복제되지 않습니다.](working-with-srp.md#ugc-never-replicated).
>
>배포에 이 포함되어 있지 않은 경우 [일반 상점](working-with-srp.md), UGC는 입력한 AEM 게시 또는 작성자 인스턴스에만 표시됩니다.

>[!NOTE]
>
>AEM 플랫폼에 대한 자세한 내용은 [권장 배포](../../help/sites-deploying/recommended-deploys.md) 및 [AEM Platform 소개](../../help/sites-deploying/data-store-config.md).

## 프로덕션 {#for-production}

UGC를 위한 공용 스토어를 구축하는 것은 필수이며 따라서 기본 배포는 일반 스토어를 지원하는 기능에 따라 달라집니다.

두 가지 예:

1. 예상 UGC 볼륨이 크고 로컬 MongoDB 인스턴스가 가능한 경우 이 옵션을 선택합니다 [MSRP](msrp.md).

1. 페이지 컨텐츠에 대한 최적의 성능을 위해 [팜 게시](../../help/sites-deploying/recommended-deploys.md#tarmk-farm) 및 [ASRP](asrp.md) 은 비교적 간단한 작업으로 UGC를 최적의 스케일링을 제공합니다.

두 가지 모두에 대해 배포는 OAK 마이크로 커널을 기반으로 할 수 있습니다.

적절한 공통 스토어를 선택하려면 고유한 사항을 고려하십시오 [특성](working-with-srp.md#characteristics-of-srp-options) 각 URL에 대해 설명합니다.

Oak 마이크로 커널에 대한 자세한 내용은 [권장 배포](../../help/sites-deploying/recommended-deploys.md).

### TarMK 게시 팜 {#tarmk-publish-farm}

토폴로지가 게시 팜인 경우 관련 중요도 항목은 다음과 같습니다.

* [사용자 동기화](sync.md)
* [사용자 및 사용자 그룹 관리](users.md)

### 권장 사항: DSRP, MSRP 또는 ASRP {#recommended-dsrp-msrp-or-asrp}

| 마이크로 커널 | 사이트 컨텐트 저장소 | 사용자가 생성한 컨텐츠 저장소 | 저장소 리소스 공급자 | 공용 스토어 |
|-------------|------------------------|----------------------------------|---------------------------|---------------|
| 임의 | JCR | MySQL | DSRP | 예 |
| 임의 | JCR | MongoDB | MSRP | 예 |
| 임의 | JCR | 온디맨드 스토리지 Adobe | ASRP | 예 |

### JSRP {#jsrp}


| 배포 | 사이트 컨텐트 저장소 | 사용자가 생성한 컨텐츠 저장소 | 저장소 리소스 공급자 | 공용 스토어 |
|----------------------|------------------------|----------------------------------|---------------------------|---------------------------------|
| TarMK 팜(기본값) | JCR | JCR | JSRP | 아니요 |
| Oak 클러스터 | JCR | JCR | JSRP | 게시 환경에만 예 |

## 개발용 {#for-development}

비프로덕션 환경의 경우 [JSRP](jsrp.md) 작성자 인스턴스 하나와 게시 인스턴스 하나를 사용하여 개발 환경을 설정하는 간단한 방법을 제공합니다.

선택한 경우 [ASRP](asrp.md), [DSRP](dsrp.md) 또는 [MSRP](msrp.md) 프로덕션의 경우 Adobe 온디맨드 스토리지 또는 MongoDB를 사용하여 유사한 개발 환경을 설정할 수도 있습니다. 예를 보려면 [데모 MongoDB를 설정하는 방법](demo-mongo.md).

## 참조 {#references}

* [사용자 동기화](sync.md)

   게시 팜 인스턴스 간의 사용자 데이터 동기화를 설명합니다.

* [사용자 및 사용자 그룹 관리](users.md)

   작성 및 게시 환경에서 사용자 및 사용자 그룹의 역할에 대해 설명합니다.

* UGC [일반 상점](working-with-srp.md)

   사이트 컨텐츠와 별도로 구성된 커뮤니티 컨텐츠의 저장소에 대해 설명합니다.

* [노드 저장소 및 데이터 저장소](../../help/sites-deploying/data-store-config.md)

   기본적으로 사이트 컨텐츠는 노드 저장소에 저장됩니다. Assets의 경우 이진 데이터를 저장하도록 데이터 저장소를 구성할 수 있습니다. 커뮤니티의 경우 SRP를 선택하도록 공통 저장소를 구성해야 합니다.

* [저장소 요소](../../help/sites-deploying/storage-elements-in-aem-6.md)

   두 노드 스토리지 구현에 대해 설명합니다. Tar 및 MongoDB입니다.
