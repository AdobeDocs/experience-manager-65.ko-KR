---
title: AEM 6.5 Communities로 업그레이드
seo-title: Upgrading to AEM 6.5 Communities
description: 이전 버전에서 AEM 6.5 Communities로 업그레이드하는 방법
seo-description: How to upgrade from an earlier version to AEM 6.5 Communities
uuid: 929c3892-1b3b-46a7-8e70-fa6864125911
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: abe5a998-bbe3-4a2b-bcf7-b490a8275219
docset: aem65
exl-id: ea41d35c-967c-4606-b4ec-377e817902e4
source-git-commit: 07f8a9f629122102d30676926b225d57e542147d
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 2%

---

# AEM 6.5 Communities로 업그레이드 {#upgrading-to-aem-communities}

각 사이트의 토폴로지 및 기능에 따라 AEM Communities 6.5로 업그레이드하거나 최신 기능 팩을 설치할 때 다음 작업이 필요할 수 있습니다.

이 섹션은 지역 사회 및 [AEM 6.5로 업그레이드](/help/sites-deploying/upgrade.md) (플랫폼).

## AEM 6.1 이상에서 업그레이드 {#upgrading-from-aem-or-later}

### Solr 다시 색인화 {#reindex-solr}

MSRP로 구성된 배포에 새 커뮤니티 기능 팩을 설치할 때 다음이 필요합니다.

1. 설치 [최신 기능 팩](/help/communities/deploy-communities.md#latestfeaturepack).
1. 설치 [최신 솔루션 구성 파일](/help/communities/msrp.md#upgrading).
1. MSRP 다시 색인화 참조 섹션 [MSRP 재색인 도구](/help/communities/msrp.md#msrp-reindex-tool).

### 사용 2.0 {#enablement}

AEM 6.3부터 사용 기능은 더 이상 MySQL에 보고 정보를 저장하지 않습니다. MySQL 종속성은 SCORM 컨텐츠를 추적하기 위해서만 있습니다.

연락처 [고객 지원 센터](https://helpx.adobe.com/kr/marketing-cloud/contact-support.html) 을 참조하십시오.

## AEM 6.0에서 업그레이드 {#upgrading-from-aem}

기존 UGC를 유지해야 하는 경우 배포 저장 UGC에 따라 그에 대한 방법이 달라집니다 [온-프레미스](#on-premise-storage) 또는 [Adobe 클라우드](#adobe-cloud-storage).

### 클라우드 스토리지 Adobe {#adobe-cloud-storage}

업그레이드된 사이트가 Adobe 클라우드 저장소를 사용하도록 구성된 경우 SRP 메서드가 이전 위치에서 기존 UGC를 찾을 수 없어서 모든 UGC가 손실된 것처럼(잘못) 표시될 수 있습니다.

따라서, ASRP가 사용할 수 있도록 지시하는 기능이 있습니다 `AEM 6.0 compatability-mode` UGC에 액세스하려면 다음을 수행하십시오.

모든 AEM 6.3 작성자 및 게시 인스턴스의 경우:

* 관리자 권한으로 로그인합니다.
* 구성 [ASRP](/help/communities/asrp.md).
* 기존 UGC를 표시하려면 다음 단계를 따르십시오.

   * 웹 콘솔 탐색:

      * 예, [https://&lt;host>:&lt;port>/system/console/configMgr](https://localhost:4502/system/console/configMgr)

      * 찾기 **AEM Communities 유틸리티** 구성.
      * 구성 패널을 확장하려면 을(를) 선택합니다.

         * *선택을 취소합니다* `Cloud Storage`

         * **저장**&#x200B;을 선택합니다

      ![유틸리티](assets/utilities.png)


### 온-프레미스 스토리지 {#on-premise-storage}

업그레이드된 사이트에서 클라우드 저장소를 사용하지 않는 경우 기존 UGC를 AEM 6.1 Communities에 도입된 새로운 구조를 준수하도록 변환해야 공통 스토어를 지원합니다.

이를 위해 GitHub에서 오픈 소스 마이그레이션 도구를 사용할 수 있습니다.
[AEM Communities UGC 마이그레이션 도구](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### Java API {#java-apis}

AEM 6.0 소셜 커뮤니티에서 AEM 6.3 Communities로 업그레이드할 때 많은 API가 다른 패키지로 재구성되었습니다. 커뮤니티 기능 사용자 지정에 IDE를 사용할 때 대부분의 문제를 쉽게 해결해야 합니다.

더 이상 사용되지 않는 SocialUtils 패키지에 대한 자세한 내용은 [SocialUtils 리팩터링](/help/communities/socialutils.md).

참조 - [커뮤니티에 Maven 사용](/help/communities/maven.md).

### JSP 구성 요소 템플릿 없음 {#no-jsp-component-templates}

다음 [소셜 구성 요소 프레임워크](/help/communities/scf.md) (SCF)에서는 [HandlebarsJS](https://handlebarsjs.com/) (HBS) AEM 6.0 이전에 사용된 JSP(Java Server Page) 대신 템플릿 언어

AEM 6.0에서 JSP 구성 요소는 일반적으로 &quot;hbs&quot;라는 하위 폴더에 있는 HBS 구성 요소를 사용하여 같은 위치에서 새 HBS 프레임워크 구성 요소와 함께 남아 있습니다.

AEM 6.1부터 JSP 구성 요소가 완전히 제거되었습니다. Communities에서는 JSP 구성 요소의 모든 사용을 SCF 구성 요소로 대체하는 것이 좋습니다.

## AEM Communities UGC 마이그레이션 도구 {#aem-communities-ugc-migration-tool}

다음 [AEM Communities UGC 마이그레이션 도구](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration) 는 GitHub에서 사용할 수 있는 오픈 소스 마이그레이션 도구이며, 이전 버전의 AEM social communities에서 UGC를 내보내고 AEM Communities 6.1 이상으로 가져올 수 있도록 사용자 지정할 수 있습니다.

이전 버전에서 UGC를 이동하는 것 외에도 도구를 사용하여 UGC를 한 버전에서 이동할 수도 있습니다 [SRP](/help/communities/working-with-srp.md) MSRP에서 DSRP로 등의 다른 변수로 이동합니다.

## AEM 5.6.1 또는 이전 버전에서 업그레이드 {#upgrading-from-aem-or-earlier}

개념적으로, 세 세대의 커뮤니티 구성 요소 가 있습니다.

**1세대**: 대략 CQ 5.4에서 AEM 5.6.0까지, 이것은 다음과 같습니다 **collab** 플랫폼 간에 UGC를 동기화하는 방법으로 복제를 사용하여 로컬 저장소에 UGC를 저장하는 구성 요소입니다. 다른 차이점은 작성 환경에서만 작성으로 구성된 블로그 기능뿐만 아니라 Java Server Pages(JSP)를 사용하는 구현과 관련되어 있습니다.

**2세대**: AEM 5.6.1부터 AEM 6.1까지입니다. **collab** 및 **소셜** 구성 요소. AEM 6.0에서는 새로운 [소셜 구성 요소 프레임워크](/help/communities/scf.md) (SCF) 및 AEM 6.2는 [일반 UGC 저장소](/help/communities/working-with-srp.md) 여기서 UGC는 [저장소 리소스 공급자](/help/communities/srp.md) (SRP).

**3세대**: AEM 6.2 이상에서 **소셜** SCF에서 UGC에 대한 SRP를 선택해야 하는 HBS(Handlebars) 구성 요소로 구현된 구성 요소.
