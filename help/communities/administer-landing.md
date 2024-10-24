---
title: 커뮤니티 사이트
description: 기본 기능에 이미 익숙한 관리자를 위한 AEM(Adobe Experience Manager) Communities의 기본 사항에 대해 알아봅니다.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: e3ffc73e-2bc5-492d-b64b-750cc7d8ab9b
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 4%

---

# 커뮤니티 사이트 {#communities-sites}

이 섹션은 AEM Communities을 관리하고 AEM Communities 기능에 익숙하다고 가정하는 사용자를 위한 것입니다.

## 개요 {#overview}

개요 및 시작 튜토리얼을 보려면 다음을 방문하십시오.

* [AEM Communities 개요](overview.md)
* [AEM Communities 시작하기](getting-started.md)

## 관리 및 구성 항목 {#administration-and-configuration-topics}

### 커뮤니티 사이트 생성 및 관리 {#communities-site-creation-and-management}

* 커뮤니티 [콘솔](consoles.md)

   * [Sites](sites-console.md)

      * [그룹(하위 커뮤니티)](groups.md)

   * [관리](moderation.md)
   * [구성원 및 그룹 관리](members.md)
   * [보고서](reports.md)

* 커뮤니티 [*도구*](tools.md):

   * [사이트 템플릿](sites.md)
   * [그룹 템플릿](tools-groups.md)
   * [커뮤니티 기능](functions.md)
   * [스토리지 구성](srp-config.md)
   * [구성 요소 가이드](components-guide.md)
   * [배지](badges.md)


### 사용자 생성 콘텐츠 {#user-generated-content}

AEM Communities의 주요 기능은 로그인한 사이트 방문자(멤버)가 사용자 생성 컨텐츠(UGC)를 생성하는 것입니다. UGC 작업에 대해 자세히 알아보려면 다음을 방문하십시오.

* [일반 UGC 저장소](working-with-srp.md): UGC의 공유 저장소에 대한 SRP 선택
* [UGC 중재](moderate-ugc.md): 신뢰할 수 있는 구성원이 일괄 또는 컨텍스트에서 UGC를 중재할 수 있습니다.
* [UGC에 태그 지정](tag-ugc.md): 구성원이 콘텐츠에 태그를 지정할 수 있도록 기능이 구성될 수 있습니다.
* [UGC 번역](translate-ugc.md): 모든 UGC를 번역하도록 기능을 구성하거나 구성원이 선택한 게시물을 번역하도록 할 수 있습니다.
* [Analytics 구성](analytics.md): Adobe Analytics에서 구성원 활동과 관련된 다양한 지표에 대해 보고할 수 있도록 설정

### 커뮤니티 구성원 {#community-members}

* [사용자 및 사용자 그룹 관리](users.md): 권한이 있는 구성원을 포함하여 커뮤니티 구성원 및 구성원 그룹에 대한 세부 정보.
* [기여도 제한](limits.md): 새 구성원의 게시를 제한하는 기능.
* [터널 서비스](deploy-communities.md#tunnel-service-on-author): 작성자 환경에서 게시측 구성원 및 구성원 그룹에 액세스할 수 있도록 허용합니다.
* [구성원 및 그룹 콘솔](members.md): 작성자 환경에서 게시측 구성원 및 구성원 그룹을 만들고 관리할 수 있습니다.
* [사용자 동기화](sync.md): 여러 게시 인스턴스 간에 구성원 및 구성원 그룹을 동기화합니다.
* [Facebook 및 Twitter으로 소셜 로그인](social-login.md): 사이트 방문자가 Facebook 또는 Twitter 자격 증명을 사용하여 커뮤니티 회원이 될 수 있는 기능입니다.
* [채점 및 배지](implementing-scoring.md): 배지를 할당하여 구성원의 역할을 식별하고 구성원이 커뮤니티에 참여하여 배지를 획득할 수 있습니다.
* [알림](notifications.md): 구성원이 팔로우하는 활동에 대한 알림을 받는 기능입니다.
* [구독](subscriptions.md): 구성원이 외부 전자 메일을 사용하여 커뮤니티와 상호 작용할 수 있는 기능입니다.
* [메시징](messaging.md): 구성원이 내부 메시지를 사용하여 커뮤니티와 상호 작용할 수 있는 기능입니다.

### 배포 {#deployment}

배포 섹션에는 AEM Communities 관련 정보가 포함되어 있습니다.

커뮤니티 콘텐츠 작업 특성은 배포 구조에 영향을 줍니다.

* [커뮤니티에 대해 권장되는 토폴로지](topologies.md)

AEM 플랫폼에 최신 Communities 릴리스를 설치하는 것이 중요합니다.

* [최신 커뮤니티 기능 팩](deploy-communities.md#latestfeaturepack)

[업그레이드](upgrade.md), [Dispatcher](dispatcher.md) 및 [복제](deploy-communities.md#replication-agents-on-author)와 같은 다른 커뮤니티별 정보는 배포 페이지를 참조하세요.

## 관련 커뮤니티 설명서 {#related-communities-documentation}

* 권장 배포에 대해 알아볼 수 있는 [커뮤니티 배포](deploy-communities.md)를 방문하십시오.

* SCF(소셜 구성 요소 프레임워크)에 대해 알아보고 커뮤니티 구성 요소와 기능을 사용자 지정하는 방법을 알아보려면 [커뮤니티 개발](communities.md)을 방문하십시오.

* 커뮤니티 구성 요소를 작성하고 구성하는 방법을 배울 수 있는 [커뮤니티 구성 요소 작성](author-communities.md)을 방문하십시오.
