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
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Communities Sites {#communities-sites}

이 섹션은 AEM Communities를 관리하고 AEM Communities 기능에 익숙하다고 가정합니다.

## 개요 {#overview}

개요 및 시작 자습서는 다음을 참조하십시오.

* [AEM Communities 개요](overview.md)
* [AEM Communities 시작하기](getting-started.md)
* [활성화를 위한 AEM Communities 시작하기](getting-started-enablement.md)

## 관리 및 구성 항목 {#administration-and-configuration-topics}

### 커뮤니티 사이트 제작 및 관리 {#communities-site-creation-and-management}

* 커뮤니티 [콘솔](consoles.md)

   * [사이트](sites-console.md)

      * [그룹(하위 커뮤니티)](groups.md)
   * [중재](moderation.md)
   * [구성원 및 그룹 관리](members.md)
   * [지원 리소스](resources.md)
   * [보고서](reports.md)


* 커뮤니티 [*도구&#x200B;*](tools.md):

   * [사이트 템플릿](sites.md)
   * [그룹 템플릿](tools-groups.md)
   * [커뮤니티 기능](functions.md)
   * [저장소 구성](srp-config.md)
   * [구성 요소 가이드](components-guide.md)
   * [배지](badges.md)


### 사용자 생성 콘텐츠 {#user-generated-content}

AEM Communities의 주요 기능은 로그인된 사이트 방문자(구성원)가 사용자 생성 콘텐츠(UGC)입니다. UGC 작업에 대한 자세한 내용은

* [일반 UGC 스토어](working-with-srp.md):UGC의 공유 스토리지를 위한 SRP 선택
* [UGC 중재](moderate-ugc.md):신뢰할 수 있는 멤버는 일괄 또는 컨텍스트 내에서 UGC를 중재할 수 있습니다.
* [태그 지정 UGC](tag-ugc.md):구성원이 컨텐츠에 태그를 지정할 수 있도록 기능을 구성할 수 있습니다.
* [UGC 번역](translate-ugc.md):모든 UGC를 번역하거나 멤버가 선택한 게시물을 변환할 수 있도록 기능을 구성할 수 있습니다.
* [분석 구성](analytics.md):adobe Analytics를 사용하여 멤버 활동과 관련된 다양한 지표에 대해 보고할 수 있습니다.

### 커뮤니티 구성원 {#community-members}

* [사용자 및 사용자 그룹 관리](users.md):권한이 있는 구성원을 포함하여 커뮤니티 구성원 및 구성원 그룹의 세부 사항
* [기여도 제한](limits.md):새 구성원의 게시 제한
* [터널 서비스](deploy-communities.md#tunnel-service-on-author):게시 측 구성원 및 구성원 그룹이 작성 환경에서 액세스할 수 있도록 허용
* [구성원 및 그룹 콘솔](members.md):게시 측 구성원 및 구성원 그룹을 작성 환경에서 만들고 관리할 수 있습니다.
* [사용자 동기화](sync.md):여러 게시 인스턴스에서 구성원 및 구성원 그룹을 동기화하는 방법
* [Facebook 및 Twitter를 사용한 소셜 로그인](social-login.md):사이트 방문자가 Facebook 또는 Twitter 자격 증명을 사용하여 커뮤니티 회원이 되는 기능
* [점수 및 배지](implementing-scoring.md):구성원의 역할을 식별하기 위해 배지가 할당되고 커뮤니티 참여를 통해 배지가 적립되는 기능
* [알림](notifications.md):구성원이 팔로우하는 활동에 대한 알림을 받을 수 있는 기능
* [구독](subscriptions.md):구성원이 외부 이메일을 사용하여 커뮤니티와 교류할 수 있는 기능
* [메시지](messaging.md):구성원이 내부 메시지를 사용하여 커뮤니티와 교류할 수 있는 기능

### 지원 기능 {#enablement-features}

* [지원 구성](enablement.md):활성화 기능을 올바르게 설정하는 데 필요한 정보
* [분석 구성](analytics.md):adobe Analytics for Communities 기능 활성화에 필요한 정보
* [태깅 지원 리소스](tag-resources.md):활성화 카탈로그 만들기

### 배포 {#deployment}

배포 섹션에는 AEM Communities 관련 정보가 포함되어 있습니다.

커뮤니티 컨텐츠를 사용한 작업의 성격이 배포 구조에 영향을 줍니다.

* [커뮤니티를 위한 권장 토폴로지](topologies.md)

AEM 플랫폼에 최신 커뮤니티 릴리스를 설치해야 합니다.

* [최신 커뮤니티 기능 팩](deploy-communities.md#latestfeaturepack)

업그레이드, 디스패처 및 복제와 같은 다른 커뮤니티 관련 정보는 [배포](upgrade.md)[](dispatcher.md) 페이지를 [](deploy-communities.md#replication-agents-on-author)참조하십시오.

## 관련 커뮤니티 설명서 {#related-communities-documentation}

* 권장 [배포에 대해](deploy-communities.md) 알려면 커뮤니티 배포를 참조하십시오.

* SCF [](communities.md) (소셜 구성 요소 프레임워크)에 대해 알아보고 커뮤니티 구성 요소 및 기능을 사용자 정의하려면 커뮤니티 개발을 참조하십시오.

* 커뮤니티 [구성 요소를](author-communities.md) 사용하여 작성하고 구성하는 방법을 알아보려면 커뮤니티 구성 요소를 참조하십시오.
