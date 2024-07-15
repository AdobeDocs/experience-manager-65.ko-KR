---
title: AEM 6.5 커뮤니티로 업그레이드
description: 이전 버전에서 AEM 6.5 Communities로 업그레이드하는 방법
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
docset: aem65
exl-id: ea41d35c-967c-4606-b4ec-377e817902e4
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 0%

---

# AEM 6.5 커뮤니티로 업그레이드 {#upgrading-to-aem-communities}

각 사이트의 토폴로지 및 기능에 따라 AEM Communities 6.5로 업그레이드하거나 최신 기능 팩을 설치할 때 다음 작업이 필요할 수 있습니다.

이 섹션은 커뮤니티에만 해당되며 [AEM 6.5로 업그레이드](/help/sites-deploying/upgrade.md)(플랫폼)에 제공된 정보를 보완합니다.

## AEM 6.1 이상에서 업그레이드 {#upgrading-from-aem-or-later}

### Solr 다시 인덱싱 {#reindex-solr}

MSRP로 구성된 배포에 새 커뮤니티 기능 팩을 설치할 때 다음을 수행해야 합니다.

1. [최신 기능 팩](/help/communities/deploy-communities.md#latestfeaturepack)을 설치하십시오.
1. [최신 Solr 구성 파일](/help/communities/msrp.md#upgrading)을 설치하십시오.
1. MSRP 색인 재지정
[MSRP 색인 재지정 도구](/help/communities/msrp.md#msrp-reindex-tool) 섹션을 참조하십시오.

## AEM 6.0에서 업그레이드 {#upgrading-from-aem}

기존 UGC를 유지해야 하는 경우, 방법은 배포가 UGC [온-프레미스](#on-premise-storage)를 저장했는지 또는 [Adobe 클라우드](#adobe-cloud-storage)에 저장했는지에 따라 다릅니다.

### Adobe 클라우드 스토리지 {#adobe-cloud-storage}

업그레이드된 사이트가 Adobe 클라우드 스토리지를 사용하도록 구성된 경우 SRP 메서드가 이전 위치에서 기존 UGC를 찾을 수 없어 모든 UGC가 손실된 것처럼 표시될 수 있습니다(잘못 표시됨).

따라서 ASRP에 `AEM 6.0 compatability-mode`을(를) 사용하여 UGC에 액세스하도록 지시할 수 있습니다.

모든 AEM 6.3 작성자 및 게시 인스턴스의 경우:

* 관리자 권한으로 로그인합니다.
* [ASRP](/help/communities/asrp.md) 구성.
* 기존 UGC를 표시하려면 다음 단계를 따르십시오.

   * 웹 콘솔로 이동합니다.

      * 예: [https://&lt;host>:&lt;port>/system/console/configMgr](https://localhost:4502/system/console/configMgr)

      * **AEM Communities 유틸리티** 구성을 찾습니다.
      * 구성 패널을 확장하려면 선택하십시오.

         * *선택 취소* `Cloud Storage`

         * **저장** 선택

     ![유틸리티](assets/utilities.png)

### On-Premise 스토리지 {#on-premise-storage}

업그레이드된 사이트에서 클라우드 스토리지를 사용하지 않은 경우, 기존 UGC를 변환하여 일반 스토어를 지원하는 AEM 6.1 Communities에 도입된 새로운 구조를 준수해야 합니다.

이를 위해 GitHub에서 오픈 소스 마이그레이션 도구를 사용할 수 있습니다.
[AEM Communities UGC 마이그레이션 도구](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### Java API {#java-apis}

AEM 6.0 소셜 커뮤니티에서 AEM 6.3 커뮤니티로 업그레이드할 때 많은 API가 다른 패키지로 재구성되었습니다. 커뮤니티 기능을 맞춤화하기 위해 IDE를 사용할 때 대부분의 문제를 쉽게 해결해야 합니다.

더 이상 사용되지 않는 SocialUtils 패키지에 대한 자세한 내용은 [SocialUtils 리팩터링](/help/communities/socialutils.md)을(를) 참조하십시오.

[커뮤니티용 Maven 사용](/help/communities/maven.md)도 참조하세요.

### JSP 구성 요소 템플릿 없음 {#no-jsp-component-templates}

[소셜 구성 요소 프레임워크](/help/communities/scf.md)(SCF)에서는 AEM 6.0 이전에 사용된 JSP(Java Server Pages) 대신 [HandlebarsJS](https://handlebarsjs.com/)(HBS) 템플릿 언어를 사용합니다.

AEM 6.0에서 JSP 구성 요소는 동일한 위치에서 새 HBS 프레임워크 구성 요소와 함께 유지되었으며, 일반적으로 HBS 구성 요소는 &quot;hbs&quot;라는 하위 폴더에 있습니다.

AEM 6.1부터 JSP 구성 요소가 완전히 제거되었습니다. 커뮤니티의 경우 모든 JSP 구성 요소 사용을 SCF 구성 요소로 대체하는 것이 좋습니다.

## AEM Communities UGC 마이그레이션 도구 {#aem-communities-ugc-migration-tool}

[AEM Communities UGC 마이그레이션 도구](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)는 GitHub에서 사용할 수 있는 오픈 소스 마이그레이션 도구로서, 이전 버전의 AEM 소셜 커뮤니티에서 UGC를 내보내고 AEM Communities 6.1 이상으로 가져오도록 사용자 지정할 수 있습니다.

이전 버전에서 UGC를 이동하는 것 외에도 도구를 사용하여 UGC를 한 [SRP](/help/communities/working-with-srp.md)에서 다른 MSRP로(예: MSRP에서 DSRP로) 이동할 수도 있습니다.

## AEM 5.6.1 또는 이전 버전에서 업그레이드 {#upgrading-from-aem-or-earlier}

개념적으로 커뮤니티 구성 요소에는 3세대 가 있습니다.

**Gen 1**: 대략 CQ 5.4부터 AEM 5.6.0까지, 플랫폼 간에 UGC를 동기화하는 수단으로 복제를 사용하여 로컬 리포지토리에 UGC를 저장한 **collab** 구성 요소입니다. 다른 차이점은 JSP(Java Server Pages)를 사용한 구현과 작성 환경에서만 작성하도록 구성된 블로그 기능과 관련이 있습니다.

**Gen 2**: AEM 5.6.1부터 AEM 6.1까지 **collab**&#x200B;과(와) **social** 구성 요소가 혼합되어 있습니다. AEM 6.0에는 새 [SCF(소셜 구성 요소 프레임워크)](/help/communities/scf.md)이 도입되었고 AEM 6.2에는 [저장소 리소스 공급자](/help/communities/srp.md)(SRP)를 사용하여 UGC에 액세스하는 [공통 UGC 저장소](/help/communities/working-with-srp.md)가 도입되었습니다.

**Gen 3**: AEM 6.2부터 UGC에 대해 SRP를 선택해야 하는 HBS(Handlebars) 구성 요소로 SCF에 구현된 구성 요소는 **social**&#x200B;뿐입니다.
