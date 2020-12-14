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
translation-type: tm+mt
source-git-commit: b29945dc73e85504cd42102eafb9e2bf6198c9cc
workflow-type: tm+mt
source-wordcount: '1898'
ht-degree: 1%

---


# 커뮤니티 배포{#deploying-communities}

## 전제 조건 {#prerequisites}

* [AEM 6.5 Platform](/help/sites-deploying/deploy.md)

* AEM Communities 라이선스

* 옵션 라이선스:

   * [커뮤니티를 위한 Adobe Analytics 기능](/help/communities/analytics.md)
   * [MSRP용 MongoDB](/help/communities/msrp.md)
   * [ASRP용 Adobe 클라우드](/help/communities/asrp.md)

## 설치 검사 목록 {#installation-checklist}

**AEM  [플랫폼용](/help/sites-deploying/deploy.md#what-is-aem)**

* 최신 [AEM 6.5 업데이트 설치](#aem64updates)

* 기본 포트를 사용하지 않는 경우(4502, 4503) [복제 에이전트 구성](#replication-agents-on-author)
* [암호화 키 복제](#replicate-the-crypto-key)
* 전역화를 지원하는 경우 [자동 번역 설정](/help/sites-administering/translation.md)
(개발에 대한 샘플 설정이 제공됨)

**커뮤니티  [기능](/help/communities/overview.md)**

* [게시 팜](/help/sites-deploying/recommended-deploys.md#tarmk-farm)을 배포하는 경우 [기본 게시자](#primary-publisher)를 식별합니다.

* [터널 서비스 사용](#tunnel-service-on-author)
* [소셜 로그인 활성화](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)
* [Adobe Analytics 구성](/help/communities/analytics.md)
* [기본 이메일 서비스](/help/communities/email.md) 설정
* [공유 UGC 저장소](/help/communities/working-with-srp.md)(**SRP**)에 대한 선택 사항 식별

   * MongoDB SRP [(MSRP)](/help/communities/msrp.md)인 경우

      * [MongoDB 설치 및 구성](/help/communities/msrp.md#mongodb-configuration)
      * [솔루션 구성](/help/communities/solr.md)
      * [MSRP 선택](/help/communities/srp-config.md)
   * 관계형 데이터베이스 SRP [(DSRP)](/help/communities/dsrp.md)

      * [MySQL용 JDBC 드라이버 설치](#jdbc-driver-for-mysql)
      * [DSRP용 MySQL 설치 및 구성](/help/communities/dsrp-mysql.md)
      * [솔루션 구성](/help/communities/solr.md)
      * [DSRP 선택](/help/communities/srp-config.md)
   * Adobe SRP [(ASRP)](/help/communities/asrp.md)

      * 프로비저닝 작업을 위해 계정 담당자와 작업
      * [ASRP 선택](/help/communities/srp-config.md)
   * JCR SRP [(JSRP)](/help/communities/jsrp.md)

      * 공유 UGC 저장소가 아님:

         * UGC는 결코 복제되지 않습니다.
         * UGC는 AEM 인스턴스나 클러스터에 입력된 경우에만 표시됩니다.

         * 기본값은 JSRP입니다.
   **[지원 기능](/help/communities/overview.md#enablement-community)**&#x200B;의 경우

   * [FFmpeg 설치 및 구성](/help/communities/ffmpeg.md)
   * [MySQL용 JDBC 드라이버 설치](#jdbc-driver-for-mysql)
   * [AEM Communities SCORM-Engine 설치](#scorm-package)
   * [MySQL 지원 설치 및 구성](/help/communities/mysql.md)





## 최신 릴리스 {#latest-releases}

AEM 6.5 Communities GA에는 커뮤니티 패키지가 포함됩니다. AEM 6.5 [커뮤니티](/help/release-notes/release-notes.md#experiencemanagercommunities)에 대한 업데이트에 대해 알려면 [AEM 6.5 릴리스 노트](/help/release-notes/release-notes.md#communities-release-notes.html)를 참조하십시오.

### AEM 6.5 업데이트 {#aem-updates}

AEM 6.4부터 AEM 누적 수정 팩 및 서비스 팩의 일부로 커뮤니티 업데이트가 제공됩니다.

AEM 6.5에 대한 최신 업데이트는 [Adobe Experience Manager 6.4 누적 수정 팩 및 서비스 팩](https://helpx.adobe.com/kr/experience-manager/aem-releases-updates.html)을 참조하십시오.

### 버전 내역 {#version-history}

AEM 6.4 이상의 AEM Communities 기능과 핫픽스는 AEM Communities 누적 수정 팩 및 서비스 팩의 일부입니다. 따라서 별도의 기능 팩이 없습니다.

### MySQL {#jdbc-driver-for-mysql}에 대한 JDBC 드라이버

두 개의 커뮤니티 기능은 MySQL 데이터베이스를 사용합니다.

* [지원](/help/communities/enablement.md)의 경우:SCORM 활동 및 학습자 기록
* [DSRP](/help/communities/dsrp.md)의 경우:사용자 생성 컨텐츠 저장(UGC)

MySQL 커넥터를 별도로 다운로드하여 설치해야 합니다.

필요한 단계는 다음과 같습니다.

1. [https://dev.mysql.com/downloads/connector/j/](https://dev.mysql.com/downloads/connector/j/)에서 ZIP 보관 파일을 다운로드합니다.

   * 버전은 5.1.38 이상이어야 합니다.

1. 보관에서 mysql-connector-java-&lt;버전>-bin.jar(번들)를 추출합니다.
1. 웹 콘솔을 사용하여 번들을 설치하고 시작합니다.

   * 예: https://localhost:4502/system/console/bundles
   * 선택 **`Install/Update`**
   * 찾아보기...를 클릭하여 다운로드한 ZIP 보관 파일에서 추출한 번들을 선택합니다.
   * MySQLcom.mysql.jdbc *용* Oracle Corporation의 JDBC 드라이버가 활성화되어 있는지 확인하고 활성 상태가 아니면(또는 로그) 시작합니다.

1. JDBC가 구성된 후 기존 배포에 설치하는 경우 웹 콘솔에서 JDBC 구성을 다시 저장하여 JDBC를 새 커넥터에 다시 바인딩합니다.
   * 예: https://localhost:4502/system/console/configMgr
   * `Day Commons JDBC Connections Pool` 구성을 찾습니다.
   * 열도록 선택
   * 선택 `Save`

1. 모든 작성자 및 게시 인스턴스에 대해 3단계와 4단계를 반복합니다.

번들 설치에 대한 자세한 내용은 [웹 콘솔](/help/sites-deploying/web-console.md) 페이지에 있습니다.

#### 예:설치된 MySQL Connector 번들 {#example-installed-mysql-connector-bundle}

![chlimage bundles](assets/chlimage-bundles.png)

### SCORM 패키지 {#scorm-package}

SCORM(Shareable Content Object Reference Model)은 e러닝의 표준 및 사양 컬렉션입니다. SCORM은 양도 가능한 ZIP 파일로 콘텐트를 패키지하는 방법도 정의합니다.

AEM Communities SCORM 엔진은 [지원](/help/communities/overview.md#enablement-community) 기능에 필요합니다. AEM 6.5 Communities에서 지원되는 Scorm 패키지:

* [cq-social-scorm-package, 버전 2.3.7](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/social/scorm/cq-social-scorm-pkg) ( [SCORM 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/)  엔진 포함)

**SCORM 패키지를 설치하려면**

1. 패키지 공유에서 [cq-social-scorm-package, 버전 2.3.7](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/social/scorm/cq-social-scorm-pkg)을 설치합니다.
1. cq 인스턴스에서 `/libs/social/config/scorm/database_scormengine_data.sql`을 다운로드하고 mysql 서버에서 실행하여 업그레이드된 scormEngineDB 스키마를 만듭니다.
1. 게시자의 `https://<hostname>:<port>/system/console/configMgr`에서 CSRF 필터의 제외된 경로 속성에 `/content/communities/scorm/RecordResults`을(를) 추가합니다.


#### SCORM 로깅 {#scorm-logging}

설치되면 모든 활성 활동이 시스템 콘솔에 로그인되어 있습니다.

원하는 경우 로그 수준을 `RusticiSoftware.*` 패키지에 대해 WARN으로 설정할 수 있습니다.

로그 작업에 대해서는 [감사 레코드 및 로그 파일 작업](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files)을 참조하십시오.

### AEM 고급 MLS {#aem-advanced-mls}

SRP 컬렉션(MSRP 또는 DSRP)에서 고급 다국어 검색(MLS)을 지원하려면 사용자 정의 스키마 및 솔루션 구성 외에 새로운 솔루션 플러그인이 필요합니다. 모든 필수 항목은 다운로드 가능한 zip 파일로 패키지됩니다.

고급 MLS 다운로드(일명 &#39;사진 모음&#39;이라고도 함)는 Adobe 저장소에서 사용할 수 있습니다.

* [AEM-SOLR-MLS-phasetoo](https://repo.adobe.com/nexus/content/repositories/releases/com/adobe/tat/AEM-SOLR-MLS-phasetwo/1.2.40/)

   * 버전 1.2.40, 2016년 4월 6일
   * AEM-SOLR-MLS-phasetoo-1.2.40.zip 다운로드

자세한 내용 및 설치 정보는 SRP에 대한 [Solr Configuration](/help/communities/solr.md)을 참조하십시오.

### 패키지 공유 링크 정보 {#about-links-to-package-share}

**Adobe AEM Cloud에 표시되는 패키지**

이 페이지에서 패키지에 대한 링크는 `adobeaemcloud.com`에서 공유하는 패키징이므로 AEM 인스턴스를 실행할 필요가 없습니다. 패키지가 볼 수 있는 동안 `Install` 단추는 Adobe 호스팅 사이트에 패키지를 설치하는 것입니다. 로컬 AEM 인스턴스에 설치하려면 `Install`을 선택하면 오류가 발생합니다.

**로컬 AEM 인스턴스에 설치하는 방법**

로컬 AEM 인스턴스의 `adobeaemcloud.com`에 표시되는 패키지를 설치하려면 먼저 패키지를 로컬 디스크에 다운로드해야 합니다.

* **자산** 탭을 선택합니다.
* **디스크**&#x200B;에 다운로드를 선택합니다.

로컬 AEM 인스턴스에서 패키지 관리자(예: [https://localhost:4502/crx/packmgr/](https://localhost:4502/crx/packmgr/))를 사용하여 로컬 AEM 패키지 리포지토리에 업로드합니다.

또는 로컬 AEM 인스턴스에서 패키지 공유를 사용하여 패키지에 액세스하면(예: [https://localhost:4502/crx/packageshare/](https://localhost:4502/crx/packageshare/)) `Download` 버튼이 로컬 AEM 인스턴스의 패키지 저장소로 다운로드됩니다.

로컬 AEM 인스턴스의 패키지 리포지토리에 있는 패키지 관리자를 사용하여 패키지를 설치합니다.

자세한 내용은 [패키지 작업 방법](/help/sites-administering/package-manager.md#package-share)을 참조하십시오.

## 권장 배포 {#recommended-deployments}

AEM Communities에서 공용 저장소는 사용자가 생성한 콘텐츠(UGC)를 저장하는 데 사용되며 종종 [SRP(storage resource provider)](/help/communities/working-with-srp.md)이라고 합니다. 권장되는 배포 센터는 일반 스토어에 대해 SRP 옵션을 선택하는 것입니다.

공용 저장소는 게시 환경에서 UGC를 조정 및 분석하면서 UGC를 [복제](/help/communities/sync.md)할 필요가 없습니다.

* [커뮤니티 콘텐츠 스토어](/help/communities/working-with-srp.md) :aem 커뮤니티를 위한 SRP 스토리지 옵션에 대해 설명합니다.

* [권장 토폴로지](/help/communities/topologies.md) :사용 사례 및 SRP 선택에 따라 사용할 토폴로지에 대해 설명합니다.

## 업그레이드 {#upgrading}

이전 버전의 AEM에서 AEM 6.5 플랫폼으로 업그레이드할 때 [AEM 6.5로 업그레이드](/help/sites-deploying/upgrade.md)를 읽어야 합니다.

플랫폼 업그레이드 외에도 [AEM Communities 6.5](/help/communities/upgrade.md)로 업그레이드하여 커뮤니티 변경 사항에 대해 알아보십시오.

## 구성 {#configurations}

### 기본 게시자 {#primary-publisher}

선택한 배포가 [게시 팜](/help/communities/topologies.md#tarmk-publish-farm)인 경우 **notifications** 또는 **Adobe Analytics**&#x200B;에 의존하는 기능과 같이 모든 인스턴스에서 발생해서는 안 되는 활동의 경우 AEM 게시 인스턴스 하나를 **`primary publisher`**&#x200B;로 식별해야 합니다.

기본적으로 `AEM Communities Publisher Configuration` OSGi 구성은 **`Primary Publisher`** 체크 상자를 선택하여 게시 팜의 모든 게시 인스턴스가 자체적으로 기본 인스턴스로 식별되도록 구성됩니다.

따라서 **모든 보조 게시 인스턴스**&#x200B;의 구성을 편집하여 **`Primary Publisher`** 확인란의 선택을 취소해야 합니다.

![chlimage_1-411](assets/chlimage_1-411.png)

게시 팜에 있는 다른(보조) 게시 인스턴스의 경우:

* 관리자 권한으로 로그인
* [웹 콘솔](/help/sites-deploying/configuring-osgi.md)에 액세스

   * 예: [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* `AEM Communities Publisher Configuration` 찾기
* 편집 아이콘 선택
* **기본 게시자** 상자의 선택을 취소합니다.
* **저장**&#x200B;을 선택합니다

### 작성자 {#replication-agents-on-author}의 복제 에이전트

복제는 [터널 서비스](#tunnel-service-on-author)를 사용하여 작성 환경에서 구성원 및 구성원 그룹을 관리하는 것은 물론, 커뮤니티 그룹과 같은 게시 환경에서 만들어진 사이트 컨텐츠에 사용됩니다.

기본 게시자의 경우 [복제 에이전트 구성](/help/sites-deploying/replication.md)이 게시 서버와 승인된 사용자를 올바르게 식별하는지 확인하십시오. 기본 권한이 부여된 사용자인 `admin,`은(는) 이미 적절한 권한을 가지고 있습니다(`Communities Administrators` 구성원).

다른 사용자가 적절한 권한을 가지려면 해당 권한을 `administrators` 사용자 그룹(또한 `Communities Administrators`의 구성원)에 구성원으로 추가해야 합니다.

작성 환경에 전송 구성을 올바르게 구성해야 하는 복제 에이전트가 2개 있습니다.

* 작성자의 복제 콘솔 액세스

   * 전역 탐색에서 **[!UICONTROL 도구]** > **[!UICONTROL 배포]** > **[!UICONTROL 복제]** > **[!UICONTROL 작성자]**&#x200B;에이전트

* 두 에이전트 모두에 대해 동일한 절차를 수행합니다.

   * **기본 에이전트(게시)**
   * **역방향 복제 에이전트(다시 게시)**

      1. 에이전트 선택
      1. **편집**&#x200B;을 선택합니다.
      1. **전송** 탭을 선택합니다.
      1. `4503`을(를) 포팅하지 않으면 **URI**&#x200B;를 편집하여 올바른 포트를 지정합니다

      1. `admin` 사용자가 아닌 경우 **사용자** 및 **암호**&#x200B;를 편집하여 `administrators` 사용자 그룹의 구성원을 지정합니다.

다음 이미지는 다음과 같이 포트 변경 결과를 4503에서 6103으로 보여 줍니다.

#### 기본 에이전트(게시) {#default-agent-publish}

![chlimage_1-412](assets/chlimage_1-412.png)

#### 역방향 복제 에이전트(반대로 게시) {#reverse-replication-agent-publish-reverse}

![chlimage_1-413](assets/chlimage_1-413.png)

### 작성자 {#tunnel-service-on-author}의 터널 서비스

작성 환경을 사용하여 [사이트 만들기](/help/communities/sites-console.md), [사이트 속성 수정](/help/communities/sites-console.md#modifying-site-properties) 또는 [커뮤니티 구성원 관리](/help/communities/members.md)할 때 작성자에 등록된 사용자가 아닌 게시 환경에 등록된 구성원(사용자)에 액세스해야 합니다.

터널 서비스는 작성자의 복제 에이전트를 사용하여 이 액세스를 제공합니다.

터널 서비스를 활성화하려면:

* 작성자 인스턴스에 대한 관리 권한으로 로그인합니다.
* 게시자가 localhost:4503이 아니거나 전송 사용자가 `admin`이(가) 아닌 경우,
그런 다음 [복제 에이전트 구성](#replication-agents-on-author)

* [웹 콘솔](/help/sites-deploying/configuring-osgi.md)에 액세스

   * 예: [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

* `AEM Communities Publish Tunnel Service` 찾기
* 편집 아이콘 선택
* **enable** 상자를 선택합니다.
* **저장**&#x200B;을 선택합니다

   ![chlimage_1-414](assets/chlimage_1-414.png)

### 암호화 키 {#replicate-the-crypto-key} 복제

모든 AEM 서버 인스턴스에서 동일한 암호화 키를 사용해야 하는 AEM Communities의 두 가지 기능이 있습니다. 이것은 [Analytics](/help/communities/analytics.md) 및 [ASRP](/help/communities/asrp.md)입니다.

AEM 6.3의 경우 주요 자료가 파일 시스템에 저장되고 더 이상 저장소에 저장되지 않습니다.

작성자에서 다른 모든 인스턴스로 주요 자료를 복사하려면 다음을 수행해야 합니다.

* 복사할 주요 자료가 들어 있는 AEM 인스턴스(일반적으로 작성자 인스턴스)에 액세스합니다.

   * 로컬 파일 시스템에서 `com.adobe.granite.crypto.file` 번들을 찾습니다.
예를 들어

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`
      * `bundle.info` 파일은 번들을 식별합니다
   * 데이터 폴더,
예를 들어

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

      * hmac 및 기본 노드 파일 복사


* 각 대상 AEM 인스턴스에 대해

   * 데이터 폴더,
예를 들어

      * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * 이전에 복사한 2개 파일 붙여넣기
   * 대상 AEM 인스턴스가 현재 실행 중인 경우 [Granite Crypto 번들](#refresh-the-granite-crypto-bundle)을 새로 고쳐야 합니다.


>[!CAUTION]
>
>암호화 키를 기반으로 하는 다른 보안 기능이 이미 구성된 경우 암호화 키를 복제하면 구성이 손상될 수 있습니다. 도움이 필요하면 [고객 지원 센터](https://helpx.adobe.com/kr/marketing-cloud/contact-support.html)에 문의하십시오.

#### 저장소 복제 {#repository-replication}

AEM 6.2 및 이전 버전의 경우와 같이 저장소에 주요 자료를 저장하도록 하면 각 AEM 인스턴스의 처음 시작 시 다음 시스템 속성을 지정하여(초기 저장소를 만드는 경우) 보존할 수 있습니다.

* `-Dcom.adobe.granite.crypto.file.disable=true`

>[!NOTE]
>
>작성자](#replication-agents-on-author)의 [복제 에이전트가 올바르게 구성되어 있는지 확인해야 합니다.

저장소에 저장된 주요 자료를 사용하면 작성자에서 다른 인스턴스로 암호화 키를 복제하는 방법은 다음과 같습니다.

[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) 사용:

* [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de)
* 선택 `/etc/key`
* `Replication` 탭 열기
* 선택 `Replicate`

* [Granite Crypto 번들 새로 고침](#refresh-the-granite-crypto-bundle)

   ![chlimage_1-415](assets/chlimage_1-415.png)

#### Granite Crypto 번들 {#refresh-the-granite-crypto-bundle} 새로 고침

* 각 게시 인스턴스에서 [웹 콘솔](/help/sites-deploying/configuring-osgi.md)에 액세스합니다.

   * 예: [https://&lt;server>:&lt;port>/system/console/bundles](https://localhost:4503/system/console/bundles)

* `Adobe Granite Crypto Support` 번들(com.adobe.granite.crypto)을 찾습니다.
* **새로 고침** 선택

   ![chlimage_1-416](assets/chlimage_1-416.png)

* 잠시 후 **성공** 대화 상자가 나타나야 합니다.
   `Operation completed successfully.`

### Apache HTTP Server {#apache-http-server}

Apache HTTP Server를 사용하는 경우 모든 관련 항목에 올바른 서버 이름을 사용해야 합니다.

특히 `RedirectMatch`에서 `localhost`이 아닌 올바른 서버 이름을 사용해야 합니다.

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

디스패처를 사용하는 경우 다음을 참조하십시오.

* AEM [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) 설명서
* [Dispatcher 설치](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-install.html)
* [커뮤니티용 Dispatcher 구성](/help/communities/dispatcher.md)
* [알려진 문제](/help/communities/troubleshooting.md#dispatcher-refetch-fails)

## 관련 커뮤니티 설명서 {#related-communities-documentation}

* 커뮤니티 사이트 만들기, 커뮤니티 사이트 템플릿 구성, 커뮤니티 콘텐츠 중재, 구성원 관리 및 메시지 구성에 대해 알려면 [커뮤니티 사이트 관리](/help/communities/administer-landing.md)를 참조하십시오.

* SCF(소셜 구성 요소 프레임워크)에 대해 알아보고 커뮤니티 구성 요소 및 기능을 사용자 지정하려면 [커뮤니티 개발](/help/communities/communities.md)을 방문하십시오.

* 커뮤니티 구성 요소로 작성하고 구성하는 방법을 알아보려면 [커뮤니티 구성 요소 작성](/help/communities/author-communities.md)을 방문하십시오.

