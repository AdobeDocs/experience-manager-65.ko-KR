---
title: AEM 6.5 Communities로 업그레이드
seo-title: AEM 6.5 Communities로 업그레이드
description: 이전 버전에서 AEM 6.4 Communities로 업그레이드하는 방법
seo-description: 이전 버전에서 AEM 6.4 Communities로 업그레이드하는 방법
uuid: 929c3892-1b3b-46a7-8e70-fa6864125911
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: abe5a998-bbe3-4a2b-bcf7-b490a8275219
docset: aem65
translation-type: tm+mt
source-git-commit: 2bcd098ae901070d5e50cd89d06c854884b4e461

---


# AEM 6.5 Communities로 업그레이드 {#upgrading-to-aem-communities}

각 사이트의 토폴로지 및 기능에 따라 AEM Communities 6.5로 업그레이드하거나 최신 기능 팩을 설치하는 경우 다음 작업이 필요할 수 있습니다.

이 섹션은 커뮤니티에만 해당되며 AEM 6.5( [플랫폼)로](/help/sites-deploying/upgrade.md) 업그레이드에 제공된 정보를 보완합니다.

## AEM 6.1 이상에서 업그레이드 {#upgrading-from-aem-or-later}

### 색인 재지정 솔루션 {#reindex-solr}

MSRP로 구성된 배포에 새 커뮤니티 기능 팩을 설치하는 경우 다음을 수행해야 합니다.

1. [최신 기능 팩을](/help/communities/deploy-communities.md#latestfeaturepack)설치합니다.
1. 최신 [Solr 구성 파일을](/help/communities/msrp.md#upgrading)설치합니다.
1. MSRP 다시 색인화 섹션 [MSRP 다시 색인 도구를 참조하십시오](/help/communities/msrp.md#msrp-reindex-tool).

### Enablement 2.0 {#enablement}

AEM 6.3부터 지원 기능이 더 이상 MySQL에 보고 정보를 저장하지 않습니다. MySQL 종속성은 SCORM 콘텐트를 추적하기 위해서만 존재합니다.

Enablement 1.0에서 콘텐츠 마이그레이션에 대한 지원은 [고객 지원](https://helpx.adobe.com/kr/marketing-cloud/contact-support.html) 센터에 문의하십시오.

## AEM 6.0에서 업그레이드 {#upgrading-from-aem}

기존 UGC를 유지해야 하는 경우 배포 방법이 UGC [온프레미스](#on-premise-storage) 또는 Adobe 클라우드에 저장되었는지에 따라 [다릅니다](#adobe-cloud-storage).

### Adobe Cloud 스토리지 {#adobe-cloud-storage}

업그레이드된 사이트가 Adobe 클라우드 스토리지를 사용하도록 구성된 경우, SRP 방법이 이전 위치에서 기존 UGC를 찾을 수 없어 모든 UGC가 손실된 것처럼(잘못) 나타날 수 있습니다.

따라서 ASRP가 UGC에 액세스하도록 하는 `AEM 6.0 compatability-mode` 기능이 있습니다.

모든 AEM 6.3 작성자 및 게시 인스턴스의 경우:

* 관리자 권한으로 로그인합니다.
* ASRP [를 구성합니다](/help/communities/asrp.md).
* 다음 단계에 따라 기존 UGC를 표시합니다.

   * 웹 콘솔로 이동합니다.

      * 예: [https://&lt;host>:&lt;port>/system/console/configMgr](https://localhost:4502/system/console/configMgr)

      * AEM **Communities 유틸리티 구성을** 찾습니다.
      * 구성 패널을 확장하려면 선택합니다.

         * *선택 취소*`Cloud Storage`

         * **저장**&#x200B;을 선택합니다
      ![chlimage_1-176](assets/chlimage_1-176.png)


### 온-프레미스 스토리지 {#on-premise-storage}

업그레이드된 사이트에서 클라우드 스토리지를 사용하지 않는 경우 기존 UGC를 변환하여 AEM 6.1 Communities에서 도입된 새 구조를 준수하도록 해야 합니다.

이를 위해 GitHub에서 오픈 소스 마이그레이션 도구를 사용할 수 있습니다.AEM[Communities UGC 마이그레이션 도구](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### Java API {#java-apis}

AEM 6.0 소셜 커뮤니티에서 AEM 6.3 Communities로 업그레이드할 때 많은 API가 다른 패키지로 재구성되었습니다. 대부분의 사용자는 IDE를 사용하여 커뮤니티 기능을 사용자 정의할 때 쉽게 해결되어야 합니다.

더 이상 사용되지 않는 SocialUtils 패키지에 대한 자세한 내용은 SocialUtils [리팩토링을 참조하십시오](/help/communities/socialutils.md).

커뮤니티에 [대한 Maven 사용을 참조하십시오](/help/communities/maven.md).

### JSP 구성 요소 템플릿 없음 {#no-jsp-component-templates}

SCF( [소셜 구성 요소 프레임워크](/help/communities/scf.md) )는 [AEM 6.0 이전에 사용된 JSP](https://www.handlebarsjs.com/) (Java Server Pages) 대신 HandlebarsJS(HBS) 템플릿 언어를 사용합니다.

AEM 6.0에서 JSP 구성 요소는 일반적으로 &quot;hbs&quot;라는 하위 폴더에 있는 HBS 구성 요소와 함께 동일한 위치의 새 HBS 프레임워크 구성 요소와 함께 남아 있었습니다.

AEM 6.1부터 JSP 구성 요소가 완전히 제거되었습니다. 커뮤니티의 경우 JSP 구성 요소의 모든 사용을 SCF 구성 요소로 대체하는 것이 좋습니다.

## AEM Communities UGC 마이그레이션 도구 {#aem-communities-ugc-migration-tool}

AEM [Communities UGC 마이그레이션](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration) 도구는 GitHub에서 사용할 수 있는 오픈 소스 마이그레이션 도구이며, 이전 버전의 AEM 소셜 커뮤니티에서 UGC를 내보내고 AEM Communities 6.1 이상 버전으로 가져오기 위해 사용자 정의할 수 있습니다.

이전 버전에서 UGC를 이동하는 것 외에도 MSRP에서 DSRP로의 UGC와 [같은](/help/communities/working-with-srp.md) UGC를 다른 SRP로 이동하는 도구를 사용할 수 있습니다.

## AEM 5.6.1 이전 버전에서 업그레이드 {#upgrading-from-aem-or-earlier}

개념적으로, 세 세대의 커뮤니티 구성 요소가 있습니다.

**Gen 1**:CQ 5.4부터 AEM 5.6.0까지 **이러한 구성 요소는** 여러 플랫폼에서 UGC를 동기화하는 수단으로 복제를 사용하여 로컬 저장소에 UGC를 저장한 collab 구성 요소입니다. 다른 차이점에는 Java Server Pages(JSP)를 사용하는 구현과 작성 환경에서만 작성하도록 구성된 블로그 기능이 포함됩니다.

**Gen 2**:AEM 5.6.1부터 AEM 6.1까지 **collab** 및 **소셜** 구성 요소가 혼합되어 있습니다. AEM 6.0에서는 새로운 [소셜 구성 요소 프레임워크](/help/communities/scf.md) (SCF)와 AEM 6.2가 [스토리지 리소스 공급자](/help/communities/working-with-srp.md) (SRP)를 사용하여 UGC에 액세스하는 [공통 UGC 스토어를](/help/communities/srp.md) 도입했습니다.

**Gen 3**:AEM 6.2부터 HBS(Handlebars) 구성 요소로 SCF에 구현된 **소셜** 구성 요소만 UGC에 대해 SRP를 선택해야 합니다.
