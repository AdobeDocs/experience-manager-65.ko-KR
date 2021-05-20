---
title: 커뮤니티 배포
seo-title: 커뮤니티 배포
description: AEM Communities 배포 방법
seo-description: AEM Communities 배포 방법
uuid: 18d9b424-004d-43b2-968a-318e27a93759
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: c8d7355f-5a70-40d1-bf22-62fab8002ea0
docset: aem65
exl-id: 5b3d572d-e73d-4626-b664-c985949469c9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1898'
ht-degree: 1%

---

# 커뮤니티 배포 중 {#deploying-communities}

## 전제 조건 {#prerequisites}

* [AEM 6.5 Platform](/help/sites-deploying/deploy.md)

* AEM Communities 라이선스

* 옵션 라이센스:

   * [커뮤니티를 위한 Adobe Analytics 기능](/help/communities/analytics.md)
   * [MSRP용 MongoDB](/help/communities/msrp.md)
   * [ASRP용 Adobe 클라우드](/help/communities/asrp.md)

## 설치 검사 목록 {#installation-checklist}

**[AEM 플랫폼용](/help/sites-deploying/deploy.md#what-is-aem)**

* 최신 [AEM 6.5 업데이트 설치](#aem64updates)

* 기본 포트(4502, 4503)를 사용하지 않는 경우 [복제 에이전트 구성](#replication-agents-on-author)
* [암호화 키 복제](#replicate-the-crypto-key)
* 전역화를 지원하는 경우 [자동화된 번역 설정](/help/sites-administering/translation.md)
(개발을 위한 샘플 설정이 제공됨)

**커뮤니티  [기능](/help/communities/overview.md)**

* [게시 팜](/help/sites-deploying/recommended-deploys.md#tarmk-farm)을 배포하는 경우 [기본 게시자](#primary-publisher)를 식별합니다

* [터널 서비스 활성화](#tunnel-service-on-author)
* [소셜 로그인 활성화](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)
* [Adobe Analytics 구성](/help/communities/analytics.md)
* [기본 이메일 서비스](/help/communities/email.md) 설정
* [공유 UGC 저장소](/help/communities/working-with-srp.md)(**SRP**)에 대한 선택을 식별합니다

   * MongoDB SRP [(MSRP)](/help/communities/msrp.md)

      * [MongoDB 설치 및 구성](/help/communities/msrp.md#mongodb-configuration)
      * [솔루션 구성](/help/communities/solr.md)
      * [MSRP 선택](/help/communities/srp-config.md)
   * 관계형 데이터베이스 SRP [(DSRP)](/help/communities/dsrp.md)

      * [MySQL용 JDBC 드라이버 설치](#jdbc-driver-for-mysql)
      * [DSRP용 MySQL 설치 및 구성](/help/communities/dsrp-mysql.md)
      * [솔루션 구성](/help/communities/solr.md)
      * [DSRP 선택](/help/communities/srp-config.md)
   * Adobe SRP [(ASRP)](/help/communities/asrp.md)

      * 프로비저닝을 위해 계정 담당자에게 문의하십시오
      * [ASRP 선택](/help/communities/srp-config.md)
   * JCR SRP [(JSRP)](/help/communities/jsrp.md)

      * 공유 UGC 저장소가 아님:

         * UGC는 복제되지 않습니다.
         * UGC가 입력된 AEM 인스턴스 또는 클러스터에만 표시됩니다

         * 기본값은 JSRP입니다.
   **[지원 기능](/help/communities/overview.md#enablement-community)**&#x200B;에 대해

   * [FFmpeg 설치 및 구성](/help/communities/ffmpeg.md)
   * [MySQL용 JDBC 드라이버 설치](#jdbc-driver-for-mysql)
   * [AEM Communities SCORM-Engine 설치](#scorm-package)
   * [MySQL 설치 및 구성 지원](/help/communities/mysql.md)





## 최신 릴리스 {#latest-releases}

AEM 6.5 Communities GA에 커뮤니티 패키지가 포함되어 있습니다. AEM 6.5 [Communities](/help/release-notes/release-notes.md#experiencemanagercommunities)에 대한 업데이트에 대해 알려면 [AEM 6.5 릴리스 노트](/help/release-notes/release-notes.md#communities-release-notes.html)를 참조하십시오.

### AEM 6.5 업데이트 {#aem-updates}

AEM 6.4부터 커뮤니티에 대한 업데이트는 AEM 누적 수정 팩 및 서비스 팩의 일부로 제공됩니다.

AEM 6.5에 대한 최신 업데이트는 [Adobe Experience Manager 6.4 누적 수정 팩 및 서비스 팩](https://helpx.adobe.com/kr/experience-manager/aem-releases-updates.html)을 참조하십시오.

### 버전 기록 {#version-history}

AEM 6.4 이상에서 AEM Communities 기능 및 핫픽스는 AEM Communities 누적 수정 팩 및 서비스 팩의 일부입니다. 따라서 별도의 기능 팩이 없습니다.

### MySQL용 JDBC 드라이버 {#jdbc-driver-for-mysql}

두 가지 커뮤니티 기능은 MySQL 데이터베이스를 사용합니다.

* [지원](/help/communities/enablement.md)의 경우:scorm 활동 및 학습자 기록
* [DSRP](/help/communities/dsrp.md)의 경우:사용자 생성 컨텐츠 저장(UGC)

MySQL 커넥터를 별도로 가져와서 설치해야 합니다.

필요한 단계는 다음과 같습니다.

1. [https://dev.mysql.com/downloads/connector/j/](https://dev.mysql.com/downloads/connector/j/)에서 ZIP 아카이브를 다운로드합니다

   * 버전은 5.1.38보다 커야 합니다.

1. 보관 위치에서 mysql-connector-java-&lt;version>-bin.jar(번들) 추출
1. 웹 콘솔을 사용하여 번들을 설치하고 시작합니다.

   * 예: https://localhost:4502/system/console/bundles
   * 선택 **`Install/Update`**
   * 찾아보기... 를 클릭하여 다운로드한 ZIP 보관함에서 추출한 번들을 선택합니다
   * *MySQLcom.mysql.jdbc*&#x200B;용 Oracle Corporation의 JDBC 드라이버가 활성화되어 있는지 확인하고 없는 경우(또는 로그를 확인) 시작합니다

1. JDBC가 구성된 후에 기존 배포에 설치하는 경우 웹 콘솔에서 JDBC 구성을 다시 저장하여 새 커넥터에 JDBC를 다시 바인딩합니다.
   * 예: https://localhost:4502/system/console/configMgr
   * `Day Commons JDBC Connections Pool` 구성을 찾습니다.
   * 열려면 선택하십시오.
   * 선택 `Save`

1. 모든 작성자 및 게시 인스턴스에서 3~4단계를 반복합니다

번들 설치에 대한 자세한 내용은 [웹 콘솔](/help/sites-deploying/web-console.md) 페이지에 있습니다.

#### 예 :설치된 MySQL 커넥터 번들 {#example-installed-mysql-connector-bundle}

![커넥터 번들](assets/connector-bundle.png)

### SCORM 패키지 {#scorm-package}

SCORM(Shareable Content Object Reference Model)은 e-learning을 위한 표준 및 사양 모음입니다. 또한 SCORM은 컨텐츠를 전송 가능한 ZIP 파일로 패키지하는 방법을 정의합니다.

AEM Communities SCORM 엔진은 [지원](/help/communities/overview.md#enablement-community) 기능에 필요합니다. AEM 6.5 Communities에서 지원되는 Scorm 패키지:

* [SCORM 2017.1 엔진을 포함하는 cq-social-scorm-package, 버전 ](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/social/scorm/cq-social-scorm-pkg) 2.3.7 [ ](https://rusticisoftware.com/blog/scorm-engine-2017-released/) .

**SCORM 패키지를 설치하려면**

1. 패키지 공유에서 [cq-social-scorm-package, 버전 2.3.7](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/social/scorm/cq-social-scorm-pkg)을 설치합니다.
1. cq 인스턴스에서 `/libs/social/config/scorm/database_scormengine_data.sql` 을 다운로드하여 mysql 서버에서 실행하여 업그레이드된 scormEngineDB 스키마를 만듭니다.
1. 게시자의 `https://<hostname>:<port>/system/console/configMgr`에서 CSRF 필터의 제외된 경로 속성에 `/content/communities/scorm/RecordResults`을 추가합니다.


#### SCORM 로깅 {#scorm-logging}

설치된 경우 모든 사용 활동이 시스템 콘솔에 로깅됩니다.

원하는 경우 로그 수준을 `RusticiSoftware.*` 패키지에 대해 WARN으로 설정할 수 있습니다.

로그 작업에 대해서는 [감사 레코드 및 로그 파일 작업](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files)을 참조하십시오.

### AEM 고급 MLS {#aem-advanced-mls}

SRP 컬렉션(MSRP 또는 DSRP)에서 고급 다국어 검색(MLS)을 지원하는 경우 사용자 지정 스키마 및 솔루션 구성 외에 새로운 솔루션 플러그인이 필요합니다. 필요한 모든 항목은 다운로드 가능한 zip 파일에 패키지됩니다.

고급 MLS 다운로드(&#39;경로&#39;라고도 함)는 Adobe 저장소에서 사용할 수 있습니다.

* [AEM-SOLR-MLS-phasetw](https://repo.adobe.com/nexus/content/repositories/releases/com/adobe/tat/AEM-SOLR-MLS-phasetwo/1.2.40/)

   * 버전 1.2.40, 2016년 4월 6일
   * AEM-SOLR-MLS-phasetwo-1.2.40.zip 다운로드

자세한 내용 및 설치 정보는 SRP용 [Solr 구성](/help/communities/solr.md)을 참조하십시오.

### 패키지 공유 링크 정보 {#about-links-to-package-share}

**Adobe AEM Cloud에 표시되는 패키지**

이 페이지의 패키지에 대한 링크에서는 `adobeaemcloud.com`에서 공유하는 패키지를 만들 수 있으므로 AEM의 실행 중인 인스턴스가 필요하지 않습니다. 패키지를 볼 수 있는 동안 `Install` 단추는 Adobe 호스팅 사이트에 패키지를 설치하는 것입니다. 로컬 AEM 인스턴스에 설치하려는 경우 `Install`을 선택하면 오류가 발생합니다.

**로컬 AEM 인스턴스에 설치하는 방법**

로컬 AEM 인스턴스에 `adobeaemcloud.com`에 표시되는 패키지를 설치하려면 먼저 패키지를 로컬 디스크에 다운로드해야 합니다.

* **Assets** 탭을 선택합니다
* **디스크에 다운로드**&#x200B;를 선택합니다.

로컬 AEM 인스턴스에서 패키지 관리자(예: [https://localhost:4502/crx/packmgr/](https://localhost:4502/crx/packmgr/))를 사용하여 로컬 AEM 패키지 리포지토리에 업로드합니다.

또는 로컬 AEM 인스턴스(예: [https://localhost:4502/crx/packageshare/](https://localhost:4502/crx/packageshare/))에서 패키지 공유를 사용하여 패키지에 액세스하면 `Download` 단추가 로컬 AEM 인스턴스의 패키지 리포지토리에 다운로드됩니다.

로컬 AEM 인스턴스의 패키지 저장소에 있는 경우 패키지 관리자를 사용하여 패키지를 설치합니다.

자세한 내용은 [패키지 작업 방법](/help/sites-administering/package-manager.md#package-share)을 참조하십시오.

## 권장 배포 {#recommended-deployments}

AEM Communities에서 공용 저장소는 UGC(사용자 생성 컨텐츠)를 저장하는 데 사용되며 종종 [SRP(저장소 리소스 제공자)](/help/communities/working-with-srp.md)라고 합니다. 권장 배포 중심은 공용 저장소에 대한 SRP 옵션을 선택하는 것입니다.

일반 저장소는 게시 환경에서 UGC를 조정하고 분석하는 것을 지원하지만 UGC의 [replication](/help/communities/sync.md)이 필요하지 않습니다.

* [커뮤니티 콘텐츠 저장소](/help/communities/working-with-srp.md) :AEM 커뮤니티의 SRP 스토리지 옵션에 대해 설명합니다.

* [권장 토폴로지](/help/communities/topologies.md) :사용 사례 및 SRP 선택에 따라 사용할 토폴로지에 대해 설명합니다.

## 업그레이드 {#upgrading}

이전 AEM 버전에서 AEM 6.5 플랫폼으로 업그레이드할 때 [AEM 6.5로 업그레이드](/help/sites-deploying/upgrade.md)를 읽는 것이 중요합니다.

플랫폼 업그레이드 외에 [AEM Communities 6.5로 업그레이드](/help/communities/upgrade.md)를 읽고 커뮤니티 변경에 대해 알아보십시오.

## 구성 {#configurations}

### 기본 게시자 {#primary-publisher}

선택한 배포가 [게시 팜](/help/communities/topologies.md#tarmk-publish-farm)인 경우, 하나의 AEM 게시 인스턴스를 **notifications** 또는 **Adobe Analytics**&#x200B;에 의존하는 기능과 같이 모든 인스턴스에서 발생해서는 안 되는 활동의 **`primary publisher`**&#x200B;로 식별해야 합니다.

기본적으로 `AEM Communities Publisher Configuration` OSGi 구성은 **`Primary Publisher`** 확인란을 선택하여 구성되므로 게시 팜의 모든 게시 인스턴스가 주 인스턴스로 자체 식별됩니다.

따라서 **모든 보조 게시 인스턴스에서 구성을 편집**&#x200B;하여 **`Primary Publisher`** 확인란을 선택 취소해야 합니다.

![기본 게시자](assets/primary-publisher.png)

게시 팜의 다른 모든(보조) 게시 인스턴스의 경우:

* 관리자 권한으로 로그인
* [웹 콘솔](/help/sites-deploying/configuring-osgi.md)에 액세스

   * 예: [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* `AEM Communities Publisher Configuration` 찾기
* 편집 아이콘을 선택합니다
* **기본 게시자** 상자의 선택을 취소합니다
* **저장**&#x200B;을 선택합니다

### 작성자의 복제 에이전트 {#replication-agents-on-author}

복제 는 [터널 서비스](#tunnel-service-on-author)를 사용하여 작성 환경의 구성원 및 구성원 그룹을 관리할 뿐만 아니라 커뮤니티 그룹과 같은 게시 환경에서 생성된 사이트 컨텐츠에 사용됩니다.

기본 게시자의 경우 [복제 에이전트 구성](/help/sites-deploying/replication.md)이 게시 서버와 인증된 사용자를 올바르게 식별하는지 확인하십시오. 기본 권한이 있는 사용자 `admin,`에게 이미 적절한 권한이 있습니다( `Communities Administrators`의 구성원).

일부 다른 사용자가 적절한 권한을 가지려면 `administrators` 사용자 그룹(`Communities Administrators`의 구성원)에 구성원으로 추가되어야 합니다.

작성 환경에는 전송 구성을 올바르게 구성해야 하는 두 개의 복제 에이전트가 있습니다.

* 작성자의 복제 콘솔에 액세스

   * 전역 탐색에서 **[!UICONTROL 도구]** > **[!UICONTROL 배포]** > **[!UICONTROL 복제]** > **[!UICONTROL 작성자]**&#x200B;에이전트 로 이동합니다.

* 두 에이전트에 대해 동일한 절차를 따릅니다.

   * **기본 에이전트(게시)**
   * **역방향 복제 에이전트(게시 취소)**

      1. 에이전트를 선택합니다
      1. **편집** 선택
      1. **전송** 탭을 선택합니다
      1. 포트 `4503`를 지정하지 않으면 **URI**&#x200B;를 편집하여 올바른 포트를 지정합니다

      1. 사용자 `admin`이 아닌 경우 **사용자** 및 **암호**&#x200B;를 편집하여 `administrators` 사용자 그룹의 구성원을 지정합니다

다음 이미지는 4503에서 6103으로 포트를 변경한 결과를 보여 줍니다.

#### 기본 에이전트(게시) {#default-agent-publish}

![default-agent-publish](assets/default-agent-publish.png)

#### 역방향 복제 에이전트(게시 역방향) {#reverse-replication-agent-publish-reverse}

![reverse-replication-agent](assets/reverse-replication-agent.png)

### 작성자 {#tunnel-service-on-author}의 터널 서비스

작성 환경을 사용하여 [사이트 만들기](/help/communities/sites-console.md), [사이트 속성 수정](/help/communities/sites-console.md#modifying-site-properties) 또는 [커뮤니티 구성원 관리](/help/communities/members.md)할 때는 작성자에 등록된 사용자가 아니라 게시 환경에 등록된 구성원(사용자)에 액세스해야 합니다.

터널 서비스는 작성자의 복제 에이전트를 사용하여 이 액세스를 제공합니다.

터널 서비스를 사용하려면

* 작성자 인스턴스에 대한 관리자 권한으로 로그인합니다.
* 게시자가 localhost:4503이 아니거나 전송 사용자가 `admin`이 아닌 경우,
그런 다음 [복제 에이전트 구성](#replication-agents-on-author)

* [웹 콘솔](/help/sites-deploying/configuring-osgi.md)에 액세스

   * 예: [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

* `AEM Communities Publish Tunnel Service` 찾기
* 편집 아이콘을 선택합니다
* **enable** 상자를 선택합니다.
* **저장**&#x200B;을 선택합니다

   ![터널 서비스](assets/tunnel-service.png)

### 암호화 키 {#replicate-the-crypto-key} 복제

모든 AEM 서버 인스턴스가 동일한 암호화 키를 사용해야 하는 AEM Communities의 두 가지 기능이 있습니다. [Analytics](/help/communities/analytics.md) 및 [ASRP](/help/communities/asrp.md)입니다.

AEM 6.3 이상에서 주요 자료는 파일 시스템에 저장되고 더 이상 저장소에 없습니다.

작성자의 주요 자료를 다른 모든 인스턴스로 복사하려면 다음을 수행해야 합니다.

* 복사할 주요 자료가 포함된 AEM 인스턴스(일반적으로 작성자 인스턴스)에 액세스합니다

   * 로컬 파일 시스템에서 `com.adobe.granite.crypto.file` 번들을 찾습니다.
예

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`
      * `bundle.info` 파일은 번들을 식별합니다
   * 데이터 폴더로 이동하고,
예

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

      * hmac 및 기본 노드 파일 복사


* 각 target AEM 인스턴스에 대해

   * 데이터 폴더로 이동하고,
예

      * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * 이전에 복사한 2개 파일 붙여넣기
   * Target AEM 인스턴스가 현재 실행 중인 경우 [Granite Crypto 번들](#refresh-the-granite-crypto-bundle)을(를) 새로 고쳐야 합니다


>[!CAUTION]
>
>암호화 키를 기반으로 하는 다른 보안 기능이 이미 구성된 경우 암호화 키를 복제하면 구성이 손상될 수 있습니다. 도움이 필요하면 [고객 지원 센터에 문의](https://helpx.adobe.com/kr/marketing-cloud/contact-support.html)하십시오.

#### 저장소 복제 {#repository-replication}

AEM 6.2 및 이전 버전의 경우와 마찬가지로, 저장소에 키 자료를 저장하는 경우, 각 AEM 인스턴스의 처음 시작 시 다음 시스템 속성을 지정하여(초기 리포지토리를 생성) 유지할 수 있습니다.

* `-Dcom.adobe.granite.crypto.file.disable=true`

>[!NOTE]
>
>작성자](#replication-agents-on-author)의 [복제 에이전트가 올바르게 구성되었는지 확인하는 것이 중요합니다.

저장소에 저장된 주요 자료를 사용하여 작성자에서 다른 인스턴스로 암호화 키를 복제하는 방법은 다음과 같습니다.

[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) 사용:

* [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de) 로 이동합니다.
* 선택 `/etc/key`
* `Replication` 탭을 엽니다.
* 선택 `Replicate`

* [Granite Crypto 번들 새로 고침](#refresh-the-granite-crypto-bundle)

   ![replication-repository](assets/replicare-repository.png)

#### Granite Crypto 번들 {#refresh-the-granite-crypto-bundle} 새로 고침

* 각 게시 인스턴스에서 [웹 콘솔](/help/sites-deploying/configuring-osgi.md)에 액세스합니다

   * 예: [https://&lt;server>:&lt;port>/system/console/bundles](https://localhost:4503/system/console/bundles)

* `Adobe Granite Crypto Support` 번들 찾기(com.adobe.granite.crypto)
* **새로 고침** 선택

   ![granite crypto](assets/granite-crypto.png)

* 잠시 후 **성공** 대화 상자가 나타나야 합니다.
   `Operation completed successfully.`

### Apache HTTP 서버 {#apache-http-server}

Apache HTTP 서버를 사용하는 경우 관련 모든 항목에 올바른 서버 이름을 사용해야 합니다.

특히 `RedirectMatch`에서 `localhost`이 아닌 올바른 서버 이름을 사용하도록 주의하십시오.

#### httpd.conf 샘플 {#httpd-conf-sample}

```shell
<IfModule alias_module>
     # XAMPP does not have a favicon; this prevents any 404 errors which may arise.
     Redirect 404 /favicon.ico
     <Location /favicon.ico>
         ErrorDocument 404 "No favicon"
     </Location>

    # Return from "Sign Out" generates response header directing you to "/", generating a 404 error
    # The RedirectMatch resolves it correctly when modified for the target Community Site :
    RedirectMatch ^/$ https://[server name]/content/sites/engage/en.html
 ...
 </IfModule>
```

### Dispatcher {#dispatcher}

Dispatcher를 사용하는 경우 다음을 참조하십시오.

* AEM [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) 설명서
* [Dispatcher 설치](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-install.html)
* [커뮤니티에 대한 Dispatcher 구성](/help/communities/dispatcher.md)
* [알려진 문제](/help/communities/troubleshooting.md#dispatcher-refetch-fails)

## 관련 커뮤니티 설명서 {#related-communities-documentation}

* 커뮤니티 사이트 만들기, 커뮤니티 사이트 템플릿 구성, 커뮤니티 콘텐츠 중재, 구성원 관리 및 메시징 구성에 대해 알려면 [커뮤니티 사이트 관리](/help/communities/administer-landing.md)를 방문하십시오.

* SCF(소셜 구성 요소 프레임워크)에 대해 알아보고 커뮤니티 구성 요소 및 기능을 사용자 지정하려면 [커뮤니티 개발](/help/communities/communities.md)을 방문하십시오.

* 커뮤니티 구성 요소를 사용하여 작성하고 구성하는 방법을 배우려면 [커뮤니티 구성 요소 작성](/help/communities/author-communities.md)을 방문하십시오.
