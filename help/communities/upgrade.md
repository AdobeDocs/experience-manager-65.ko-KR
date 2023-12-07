---
title: AEM 6.5 커뮤니티로 업그레이드
description: 이전 버전에서 AEM 6.5 Communities로 업그레이드하는 방법
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
docset: aem65
exl-id: ea41d35c-967c-4606-b4ec-377e817902e4
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 0%

---

# AEM 6.5 커뮤니티로 업그레이드 {#upgrading-to-aem-communities}

각 사이트의 토폴로지 및 기능에 따라 AEM Communities 6.5로 업그레이드하거나 최신 기능 팩을 설치할 때 다음 작업이 필요할 수 있습니다.

이 섹션은 커뮤니티에만 해당되며 제공된 정보가 보완됩니다. [AEM 6.5로 업그레이드](/help/sites-deploying/upgrade.md) (플랫폼).

## AEM 6.1 이상에서 업그레이드 {#upgrading-from-aem-or-later}

### Solr 다시 인덱싱 {#reindex-solr}

MSRP로 구성된 배포에 새 커뮤니티 기능 팩을 설치할 때 다음을 수행해야 합니다.

1. 설치 [최신 기능 팩](/help/communities/deploy-communities.md#latestfeaturepack).
1. 설치 [최신 Solr 구성 파일](/help/communities/msrp.md#upgrading).
1. MSRP 색인 재지정(섹션 참조) [MSRP 색인 재지정 도구](/help/communities/msrp.md#msrp-reindex-tool).

## AEM 6.0에서 업그레이드 {#upgrading-from-aem}

기존 UGC를 유지해야 하는 경우, 그렇게 하는 방법은 배포가 UGC를 저장했는지 여부에 따라 달라집니다 [온-프레미스](#on-premise-storage) 또는 [Adobe 클라우드](#adobe-cloud-storage).

### Adobe 클라우드 스토리지 {#adobe-cloud-storage}

업그레이드된 사이트가 Adobe 클라우드 스토리지를 사용하도록 구성된 경우 SRP 메서드가 이전 위치에서 기존 UGC를 찾을 수 없어 모든 UGC가 손실된 것처럼 표시될 수 있습니다(잘못 표시됨).

따라서 ASRP에 다음을 사용하도록 지시할 수 있습니다. `AEM 6.0 compatability-mode` ugc에 액세스

모든 AEM 6.3 작성자 및 게시 인스턴스의 경우:

* 관리자 권한으로 로그인합니다.
* 구성 [ASRP](/help/communities/asrp.md).
* 기존 UGC를 표시하려면 다음 단계를 따르십시오.

   * 웹 콘솔로 이동합니다.

      * 예를 들어, [https://&lt;host>:&lt;port>/system/console/configMgr](https://localhost:4502/system/console/configMgr)

      * 찾기 **AEM Communities 유틸리티** 구성.
      * 구성 패널을 확장하려면 선택하십시오.

         * *선택 취소* `Cloud Storage`

         * 선택 **저장**

     ![유틸리티](assets/utilities.png)

### On-Premise 스토리지 {#on-premise-storage}

업그레이드된 사이트에서 클라우드 스토리지를 사용하지 않은 경우, 기존 UGC를 변환하여 일반 스토어를 지원하는 AEM 6.1 Communities에 도입된 새로운 구조를 준수해야 합니다.

이를 위해 GitHub에서 오픈 소스 마이그레이션 도구를 사용할 수 있습니다.
[AEM Communities UGC 마이그레이션 도구](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### Java API {#java-apis}

AEM 6.0 소셜 커뮤니티에서 AEM 6.3 커뮤니티로 업그레이드할 때 많은 API가 다른 패키지로 재구성되었습니다. 커뮤니티 기능을 맞춤화하기 위해 IDE를 사용할 때 대부분의 문제를 쉽게 해결해야 합니다.

더 이상 사용되지 않는 SocialUtils 패키지에 대한 자세한 내용은 다음을 참조하십시오. [SocialUtils 리팩터링](/help/communities/socialutils.md).

참조: [Maven for Communities 사용](/help/communities/maven.md).

### JSP 구성 요소 템플릿 없음 {#no-jsp-component-templates}

다음 [소셜 구성 요소 프레임워크](/help/communities/scf.md) (SCF)는 [HandlebarsJs](https://handlebarsjs.com/) (HBS) AEM 6.0 이전에 사용된 Java Server Pages(JSP) 대신 언어를 템플릿화합니다.

AEM 6.0에서 JSP 구성 요소는 동일한 위치에서 새 HBS 프레임워크 구성 요소와 함께 유지되었으며, 일반적으로 HBS 구성 요소는 &quot;hbs&quot;라는 하위 폴더에 있습니다.

AEM 6.1부터 JSP 구성 요소가 완전히 제거되었습니다. 커뮤니티의 경우 모든 JSP 구성 요소 사용을 SCF 구성 요소로 대체하는 것이 좋습니다.

## AEM Communities UGC 마이그레이션 도구 {#aem-communities-ugc-migration-tool}

다음 [AEM Communities UGC 마이그레이션 도구](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration) 는 GitHub에서 사용할 수 있는 오픈 소스 마이그레이션 도구로서, 이전 버전의 AEM 소셜 커뮤니티에서 UGC를 내보내고 AEM Communities 6.1 이상으로 가져오도록 사용자 지정할 수 있습니다.

이전 버전에서 UGC를 이동하는 것 외에도 도구를 사용하여 UGC를 이동할 수도 있습니다 [SRP](/help/communities/working-with-srp.md) MSRP에서 DSRP로 등 다른 이름으로

## AEM 5.6.1 또는 이전 버전에서 업그레이드 {#upgrading-from-aem-or-earlier}

개념적으로 커뮤니티 구성 요소에는 3세대 가 있습니다.

**1세대**: 대략 CQ 5.4 ~ AEM 5.6.0이며 다음과 같습니다. **콜랩** 플랫폼 간에 UGC를 동기화하는 수단으로 복제를 사용하여 로컬 저장소에 UGC를 저장한 구성 요소입니다. 다른 차이점은 JSP(Java Server Pages)를 사용한 구현과 작성 환경에서만 작성하도록 구성된 블로그 기능과 관련이 있습니다.

**2세대**: AEM 5.6.1부터 AEM 6.1까지, **콜랩** 및 **소셜** 구성 요소. AEM 6.0은 새로운 [소셜 구성 요소 프레임워크](/help/communities/scf.md) (SCF) 및 AEM 6.2에서 [일반 UGC 저장소](/help/communities/working-with-srp.md) 여기서 UGC는 [저장소 리소스 공급자](/help/communities/srp.md) (SRP).

**3세대**: AEM 6.2 이상에서는 **소셜** SCF에서 UGC에 SRP를 선택해야 하는 HBS(Handlebars) 구성 요소로 구현된 구성 요소입니다.
