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
source-git-commit: c190d5f223c85f6c49fea1391d8a3d2baff20192
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 2%

---


# AEM 6.5 Communities로 업그레이드 {#upgrading-to-aem-communities}

각 사이트의 토폴로지 및 기능에 따라 AEM Communities 6.5로 업그레이드하거나 최신 기능 팩을 설치하는 경우 다음 작업이 필요할 수 있습니다.

이 섹션은 커뮤니티에 한정되며 AEM 6.5(플랫폼)로 [업그레이드 시 제공되는 정보를 보완합니다](/help/sites-deploying/upgrade.md) .

## AEM 6.1 이상에서 업그레이드 {#upgrading-from-aem-or-later}

### 색인 재지정 솔루션 {#reindex-solr}

MSRP로 구성된 배포에 새 커뮤니티 기능 팩을 설치하는 경우 다음을 수행해야 합니다.

1. [최신 기능 팩을 설치합니다](/help/communities/deploy-communities.md#latestfeaturepack).
1. 최신 [Solr 구성 파일을 설치합니다](/help/communities/msrp.md#upgrading).
1. MSRP 다시 색인화 섹션 [MSRP 다시 색인 도구를 참조하십시오](/help/communities/msrp.md#msrp-reindex-tool).

### Enablement 2.0 {#enablement}

AEM 6.3의 경우 활성 기능은 MySQL에 보고 정보를 더 이상 저장하지 않습니다. MySQL 종속성은 SCORM 콘텐트를 추적하기 위해서만 존재합니다.

Enablement 1.0에서 콘텐츠 마이그레이션에 대한 지원은 [고객 지원](https://helpx.adobe.com/kr/marketing-cloud/contact-support.html) 센터에 문의하십시오.

## AEM 6.0에서 업그레이드 {#upgrading-from-aem}

사전 기존 UGC를 유지해야 하는 경우 배포 [가 UGC를 온-프레미스](#on-premise-storage) 또는 [Adobe 클라우드](#adobe-cloud-storage)에 저장했는지에 따라 그렇게 하는 방법이 달라집니다.

### Adobe 클라우드 스토리지 {#adobe-cloud-storage}

업그레이드된 사이트가 Adobe 클라우드 스토리지를 사용하도록 구성된 경우, SRP 방법이 이전 위치에서 기존 UGC를 찾을 수 없어 모든 UGC가 손실된 것처럼(잘못) 나타날 수 있습니다.

따라서 ASRP가 UGC에 액세스하도록 지시하는 기능 `AEM 6.0 compatability-mode` 이 있습니다.

모든 AEM 6.3 작성자 및 게시 인스턴스의 경우:

* 관리자 권한으로 로그인합니다.
* ASRP [를 구성합니다](/help/communities/asrp.md).
* 기존 UGC를 표시하려면 다음 단계를 따르십시오.

   * 웹 콘솔 찾아보기:

      * 예: [https://&lt;host>:&lt;port>/system/console/configMgr](https://localhost:4502/system/console/configMgr)

      * AEM Communities **유틸리티** 구성을 찾습니다.
      * 구성 패널을 확장하려면 선택합니다.

         * *선택 취소* `Cloud Storage`

         * **저장**&#x200B;을 선택합니다

      ![utilities](assets/utilities.png)


### 온프레미스 스토리지 {#on-premise-storage}

업그레이드된 사이트에서 클라우드 스토리지를 사용하지 않은 경우 기존 UGC를 변환하여 AEM 6.1 Communities에서 도입된 새로운 구조를 준수하고 공통 스토어를 지원해야 합니다.

이를 위해 GitHub에서 오픈 소스 마이그레이션 도구를 사용할 수 있습니다.[AEM Communities UGC 마이그레이션 도구](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### Java API {#java-apis}

AEM 6.0 소셜 커뮤니티에서 AEM 6.3 Communities로 업그레이드할 때 많은 API가 다른 패키지로 재구성되었습니다. 대부분의 경우 커뮤니티 기능을 사용자 지정하기 위해 IDE를 사용할 때 손쉽게 해결해야 합니다.

더 이상 사용되지 않는 SocialUtils 패키지에 대한 자세한 내용은 [SocialUtils 리팩토링을 참조하십시오](/help/communities/socialutils.md).

커뮤니티에 대한 [마비사항 사용을 참조하십시오](/help/communities/maven.md).

### JSP 구성 요소 템플릿 없음 {#no-jsp-component-templates}

SCF( [소셜 구성 요소 프레임워크](/help/communities/scf.md) )는 AEM 6.0 이전에 사용된 JSP(Java Server Pages)를 대신하여 [HandlebarsJS](https://www.handlebarsjs.com/) (HBS) 템플릿 언어를 사용합니다.

AEM 6.0에서는 JSP 구성 요소가 동일한 위치에 있는 새 HBS 프레임워크 구성 요소와 함께 남아 있었습니다. 이 구성 요소는 일반적으로 &quot;hbs&quot;라는 하위 폴더에 있습니다.

AEM 6.1의 경우 JSP 구성 요소가 완전히 제거되었습니다. 커뮤니티의 경우 JSP 구성 요소의 모든 사용을 SCF 구성 요소로 대체하는 것이 좋습니다.

## AEM Communities UGC 마이그레이션 도구 {#aem-communities-ugc-migration-tool}

[AEM Communities UGC 마이그레이션 도구는](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration) GitHub에서 사용할 수 있는 오픈 소스 마이그레이션 툴로, 이전 버전의 AEM 소셜 커뮤니티에서 UGC를 내보내고 AEM Communities 6.1 이상으로 가져올 수 있도록 사용자 정의할 수 있습니다.

이전 버전에서 UGC를 이동하는 것 외에도 이 도구를 사용하여 MSRP에서 DSRP로 [](/help/communities/working-with-srp.md) 등의 UGC를 이동할 수도 있습니다.

## AEM 5.6.1 이전 버전에서 업그레이드 {#upgrading-from-aem-or-earlier}

개념적으로는 세 세대의 커뮤니티 구성 요소가 있습니다.

**1**&#x200B;세대:거의 CQ 5.4부터 AEM 5.6.0까지, 이러한 구성 요소는 여러 플랫폼에서 UGC를 동기화하는 수단으로 복제를 사용하여 로컬 저장소에 UGC를 저장한 **collab** 구성 요소입니다. 다른 차이점에는 작성 환경에서만 작성하는 블로그 기능뿐만 아니라 JSP(Java Server Pages)를 사용하는 구현도 포함됩니다.

**2세대**:AEM 5.6.1부터 AEM 6.1까지 **collab** 및 **소셜** 구성 요소가 혼합되어 있습니다. AEM 6.0은 새로운 [소셜 구성 요소 프레임워크](/help/communities/scf.md) (SCF)와 AEM 6.2를 도입하여 [SRP(Storage Resource Provider](/help/communities/working-with-srp.md) )를 사용하여 UGC를 액세스하는 [공통 UGC 스토어를](/help/communities/srp.md) 도입했습니다.

**3세대**:AEM 6.2부터 UGC에 대해 SRP를 선택해야 하는 HBS(Handlebars) 구성 요소로 SCF에 구현된 **소셜** 구성 요소만 있습니다.
