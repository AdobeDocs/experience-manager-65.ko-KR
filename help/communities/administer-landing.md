---
title: 커뮤니티 사이트
seo-title: 커뮤니티 사이트
description: AEM Communities 설명서 개요
seo-description: AEM Communities 설명서 개요
uuid: 9842ce6c-1af8-4b27-b199-07410e797ab2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 8799386a-c3b8-43cf-9f71-580ff2a81abc
role: Administrator
exl-id: e3ffc73e-2bc5-492d-b64b-750cc7d8ab9b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 5%

---

# 커뮤니티 사이트 {#communities-sites}

이 섹션은 AEM Communities을 관리하고 AEM Communities 기능에 익숙하다고 가정합니다.

## 개요 {#overview}

개요 및 시작 자습서는 다음을 참조하십시오.

* [AEM Communities 개요](overview.md)
* [AEM Communities 시작하기](getting-started.md)
* [AEM Communities for Enablement 시작하기](getting-started-enablement.md)

## 관리 및 구성 항목 {#administration-and-configuration-topics}

### 커뮤니티 사이트 만들기 및 관리 {#communities-site-creation-and-management}

* 커뮤니티 [콘솔](consoles.md)

   * [사이트](sites-console.md)

      * [그룹(하위 커뮤니티)](groups.md)
   * [중재](moderation.md)
   * [구성원 및 그룹 관리](members.md)
   * [사용 리소스](resources.md)
   * [보고서](reports.md)


* 커뮤니티 [*도구*](tools.md):

   * [사이트 템플릿](sites.md)
   * [그룹 템플릿](tools-groups.md)
   * [커뮤니티 기능](functions.md)
   * [저장소 구성](srp-config.md)
   * [구성 요소 가이드](components-guide.md)
   * [배지](badges.md)


### 사용자 생성 콘텐츠 {#user-generated-content}

AEM Communities의 주요 기능은 로그인한 사이트 방문자(구성원)가 사용자 생성 콘텐츠(UGC)를 생성하는 것입니다. UGC 방문 작업에 대해 자세히 알아보려면:

* [일반 UGC 저장소](working-with-srp.md):UGC 공유 스토리지를 위한 SRP 선택
* [UGC 중재](moderate-ugc.md):신뢰할 수 있는 구성원은 UGC를 벌크 또는 컨텍스트 내 중재 가능
* [UGC 태깅](tag-ugc.md):구성원이 컨텐츠에 태그를 지정할 수 있도록 기능을 구성할 수 있습니다
* [UGC 번역](translate-ugc.md):모든 UGC를 번역하거나 구성원이 선택한 게시물을 번역하도록 기능을 구성할 수 있습니다
* [Analytics 구성](analytics.md):Adobe Analytics 활성화 구성원 활동과 관련된 다양한 지표에 대해 보고합니다.

### 커뮤니티 구성원 {#community-members}

* [사용자 및 사용자 그룹 관리](users.md):권한이 있는 구성원을 포함한 커뮤니티 구성원 및 구성원 그룹의 세부 정보입니다.
* [기여도 제한](limits.md):새 구성원의 게시를 제한할 수 있습니다.
* [터널 서비스](deploy-communities.md#tunnel-service-on-author):작성 환경에서 게시 측 구성원 및 구성원 그룹에 액세스할 수 있습니다.
* [구성원 및 그룹 콘솔](members.md):작성 환경에서 게시 측 구성원 및 구성원 그룹을 만들고 관리할 수 있습니다.
* [사용자 동기화](sync.md):여러 게시 인스턴스에서 구성원 및 구성원 그룹을 동기화하는 것입니다.
* [facebook 및 Twitter을 사용하여 소셜 로그인](social-login.md):사이트 방문자가 Facebook 또는 Twitter 자격 증명을 사용하여 커뮤니티 구성원이 될 수 있는 기능입니다.
* [점수 및 배지](implementing-scoring.md):구성원의 역할을 식별하는 배지가 할당되고, 구성원들이 커뮤니티에 참여하여 배지를 얻을 수 있는 능력.
* [알림](notifications.md):구성원이 따르는 활동에 대한 알림을 받을 수 있는 기능.
* [구독](subscriptions.md):구성원이 외부 이메일을 사용하여 커뮤니티와 상호 작용할 수 있는 기능입니다.
* [메시징](messaging.md):내부 메시지를 사용하여 구성원이 커뮤니티와 상호 작용할 수 있는 기능.

### 사용 기능 {#enablement-features}

* [지원 구성](enablement.md):사용 기능을 올바르게 설정하는 데 필요한 정보입니다.
* [Analytics 구성](analytics.md):communities용 Adobe Analytics 기능을 활성화하는 데 필요한 정보입니다.
* [태깅 지원 리소스](tag-resources.md):활성화 카탈로그를 만드는 데 필요합니다.

### 배포 {#deployment}

배포 섹션에는 AEM Communities에 대한 정보가 들어 있습니다.

커뮤니티 컨텐츠 작업의 특성은 배포 구조에 영향을 줍니다.

* [커뮤니티에 대한 권장 토폴로지](topologies.md)

AEM 플랫폼에 최신 Communities 릴리스를 설치하는 것이 중요합니다.

* [최신 커뮤니티 기능 팩](deploy-communities.md#latestfeaturepack)

[업그레이드](upgrade.md), [Dispatcher](dispatcher.md) 및 [복제](deploy-communities.md#replication-agents-on-author)와 같은 다른 커뮤니티 관련 정보는 배포 페이지를 참조하십시오.

## 관련 커뮤니티 설명서 {#related-communities-documentation}

* 권장 배포에 대해 알아보려면 [Communities 배포](deploy-communities.md)를 방문하십시오.

* SCF(소셜 구성 요소 프레임워크)에 대해 알아보고 커뮤니티 구성 요소 및 기능을 사용자 지정하려면 [커뮤니티 개발](communities.md)을 방문하십시오.

* 커뮤니티 구성 요소를 사용하여 작성하고 구성하는 방법을 배우려면 [커뮤니티 구성 요소 작성](author-communities.md)을 방문하십시오.
