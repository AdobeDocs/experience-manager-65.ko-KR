---
title: 커뮤니티 배포
description: Adobe Experience Manager에서 커뮤니티 및 커뮤니티 기능을 배포하는 방법에 대해 알아봅니다.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
docset: aem65
exl-id: 5b3d572d-e73d-4626-b664-c985949469c9
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1658'
ht-degree: 0%

---

# 커뮤니티 배포 {#deploying-communities}

## 사전 요구 사항 {#prerequisites}

* [AEM 6.5 플랫폼](/help/sites-deploying/deploy.md)

* AEM Communities 라이선스

* 다음에 대한 선택적 라이선스:

   * [Adobe Analytics for Communities 기능](/help/communities/analytics.md)
   * [MSRP용 MongoDB](/help/communities/msrp.md)
   * [ASRP용 Adobe 클라우드](/help/communities/asrp.md)

## 설치 검사 목록 {#installation-checklist}

[AEM 플랫폼&#x200B;](/help/sites-deploying/deploy.md#what-is-aem)**의**

* 최신 [AEM 6.5 업데이트 설치](#aem64updates)

* 기본 포트(4502, 4503)를 사용하지 않는 경우 [복제 에이전트를 구성합니다](#replication-agents-on-author)
* [암호화 키 복제](#replicate-the-crypto-key)
* 세계화를 지원하는 경우 [자동 번역 설정](/help/sites-administering/translation.md)
(개발을 위해 샘플 설정이 제공됨)

**[커뮤니티 기능](/help/communities/overview.md)**&#x200B;의 경우

* [게시 팜](/help/sites-deploying/recommended-deploys.md#tarmk-farm)을 배포하는 경우 [기본 게시자 식별](#primary-publisher)

* [터널 서비스 활성화](#tunnel-service-on-author)
* [소셜 로그인 활성화](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)
* [Adobe Analytics 구성](/help/communities/analytics.md)
* [기본 전자 메일 서비스 설정](/help/communities/email.md)
* [공유 UGC 저장소](/help/communities/working-with-srp.md)(**SRP**)에 대한 선택 항목 식별

   * MongoDB SRP [(MSRP)](/help/communities/msrp.md)인 경우

      * [MongoDB 설치 및 구성](/help/communities/msrp.md#mongodb-configuration)
      * [Solr 구성](/help/communities/solr.md)
      * [MSRP 선택](/help/communities/srp-config.md)

   * 관계형 데이터베이스 SRP [(DSRP)](/help/communities/dsrp.md)인 경우

      * [MySQL용 JDBC 드라이버 설치](#jdbc-driver-for-mysql)
      * [DSRP용 MySQL 설치 및 구성](/help/communities/dsrp-mysql.md)
      * [Solr 구성](/help/communities/solr.md)
      * [DSRP 선택](/help/communities/srp-config.md)

   * Adobe SRP [(ASRP)](/help/communities/asrp.md)인 경우

      * 계정 담당자에게 프로비저닝을 요청하십시오.
      * [ASRP 선택](/help/communities/srp-config.md)

   * JCR SRP [(JSRP)](/help/communities/jsrp.md)인 경우

      * 공유 UGC(사용자 생성 컨텐츠) 저장소가 아닙니다.

         * UGC는 복제되지 않음
         * UGC는 입력된 AEM 인스턴스 또는 클러스터에서만 볼 수 있습니다.

         * 기본값은 JSRP입니다.

## 최신 릴리스 {#latest-releases}

AEM 6.5 Communities GA에는 Communities 패키지가 포함됩니다. AEM 6.5 [Communities](/help/release-notes/release-notes.md#experiencemanagercommunities)에 대한 업데이트에 대한 자세한 내용은 [AEM 6.5 릴리스 노트](/help/release-notes/release-notes.md#communities-release-notes.html)를 참조하세요.

### AEM 6.5 업데이트 {#aem-updates}

AEM 6.4부터 커뮤니티에 대한 업데이트는 AEM 누적 수정 팩 및 서비스 팩의 일부로 제공됩니다.

AEM 6.5에 대한 최신 업데이트는 [Adobe Experience Manager 6.4 누적 수정 팩 및 서비스 팩](https://experienceleague.adobe.com/kr/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates)을 참조하세요.

### 버전 기록 {#version-history}

AEM 6.4 이상에서와 같이, AEM Communities 기능 및 핫픽스는 AEM Communities 누적 수정 팩 및 서비스 팩의 일부입니다. 따라서 별도의 기능 팩이 없습니다.

### MySQL용 JDBC 드라이버 {#jdbc-driver-for-mysql}

하나의 커뮤니티 기능은 MySQL 데이터베이스를 사용합니다.

* [DSRP](/help/communities/dsrp.md)의 경우: UGC 저장 중

MySQL 커넥터를 별도로 가져와 설치해야 합니다.

필요한 단계는 다음과 같습니다.

1. [https://dev.mysql.com/downloads/connector/j/](https://dev.mysql.com/downloads/connector/j/)에서 ZIP 보관 파일 다운로드

   * 버전은 >= 5.1.38이어야 합니다.

1. 아카이브에서 mysql-connector-java-&lt;version>-bin.jar(번들) 추출
1. 웹 콘솔을 사용하여 번들 을 설치하고 시작합니다.

   * 예: https://localhost:4502/system/console/bundles
   * **`Install/Update`** 선택
   * 찾아보기 ... 다운로드한 ZIP 아카이브에서 추출한 번들을 선택합니다.
   * MySQLcom.mysql.jdbc *에 대한* Oracle 회사의 JDBC 드라이버가 활성 상태인지 확인하고, 그렇지 않은 경우 시작합니다(또는 로그 확인)

1. JDBC가 구성된 후 기존 배포에 설치하는 경우 웹 콘솔에서 JDBC 구성을 복원하여 JDBC를 새 커넥터에 다시 바인딩합니다.
   * 예: https://localhost:4502/system/console/configMgr
   * `Day Commons JDBC Connections Pool` 구성 찾기
   * 열려면 선택하십시오.
   * `Save` 선택

1. 모든 작성자 및 게시 인스턴스에서 3단계와 4단계를 반복합니다

번들 설치에 대한 자세한 내용은 [웹 콘솔](/help/sites-deploying/web-console.md) 페이지에 있습니다.

#### 예 : 설치된 MySQL 커넥터 번들 {#example-installed-mysql-connector-bundle}

![connector-bundle](assets/connector-bundle.png)



### AEM 고급 MLS {#aem-advanced-mls}

SRP 컬렉션(MSRP 또는 DSRP)이 고급 다국어 검색(MLS)을 지원하려면 사용자 지정 스키마 및 Solr 구성 외에 새로운 Solr 플러그인이 필요합니다. 모든 필수 항목은 다운로드 가능한 zip 파일로 패키지됩니다.

고급 MLS 다운로드(`phasetwo`)는 Adobe 리포지토리에서 사용할 수 있습니다.

* AEM-SOLR-MLS-phasetwo

  고급 MLS 패키지를 얻으려면 설명서의 배포 섹션에서 [AEM 고급 MLS](deploy-communities.md#aem-advanced-mls)을(를) 참조하십시오.

   * 버전 1.2.40, 2016년 4월 6일
   * AEM-SOLR-MLS-phasetwo-1.2.40.zip 다운로드

자세한 내용 및 설치 정보는 SRP의 [Solr 구성](/help/communities/solr.md)을 참조하세요.

### 패키지 공유 링크 정보 {#about-links-to-package-share}

**Adobe AEM Cloud에 표시되는 패키지**

`adobeaemcloud.com`의 패키지 공유에 연결되므로 이 페이지의 패키지에 연결되는 링크에는 실행 중인 AEM 인스턴스가 필요하지 않습니다. 패키지를 볼 수 있는 동안 `Install` 단추는 Adobe 호스팅 사이트에 패키지를 설치하기 위한 것입니다. 로컬 AEM 인스턴스에 설치하려면 `Install`을(를) 선택하면 오류가 발생합니다.

**로컬 AEM 인스턴스에 설치하는 방법**

로컬 AEM 인스턴스에 `adobeaemcloud.com`에 표시되는 패키지를 설치하려면 먼저 패키지를 로컬 디스크로 다운로드해야 합니다.

* **Assets** 탭 선택
* **디스크에 다운로드** 선택

로컬 AEM 인스턴스에서 패키지 관리자(예: [https://localhost:4502/crx/packmgr/](https://localhost:4502/crx/packmgr/))를 사용하여 로컬 AEM의 패키지 리포지토리에 업로드합니다.

또는 로컬 AEM 인스턴스(예: [https://localhost:4502/crx/packageshare/](https://localhost:4502/crx/packageshare/))에서 패키지 공유를 사용하여 패키지에 액세스하면 `Download` 단추가 로컬 AEM 인스턴스의 패키지 저장소로 다운로드됩니다.

로컬 AEM 인스턴스의 패키지 저장소에 있는 경우 패키지 관리자를 사용하여 패키지를 설치합니다.

자세한 내용은 [패키지를 사용하여 작업하는 방법](/help/sites-administering/package-manager.md#package-share)을 참조하세요.

## 권장 배포 {#recommended-deployments}

AEM Communities에서 일반 저장소는 UGC를 저장하는 데 사용되며 종종 [SRP(저장소 리소스 공급자)](/help/communities/working-with-srp.md)이라고도 합니다. 권장 배포는 일반 저장소에 대한 SRP 옵션을 선택하는 데 중점을 둡니다.

일반 저장소는 게시 환경에서 UGC의 중재 및 분석을 지원하지만 UGC의 [복제](/help/communities/sync.md)가 필요하지 않습니다.

* [커뮤니티 콘텐츠 저장소](/help/communities/working-with-srp.md) : AEM Communities의 SRP 저장소 옵션에 대해 설명합니다.

* [권장 토폴로지](/help/communities/topologies.md) : 사용 사례 및 SRP 선택에 따라 사용할 토폴로지에 대해 설명합니다.

## 업그레이드 중 {#upgrading}

이전 버전의 AEM에서 AEM 6.5 플랫폼으로 업그레이드할 때는 [AEM 6.5로 업그레이드](/help/sites-deploying/upgrade.md)를 읽어보는 것이 중요합니다.

플랫폼을 업그레이드하는 것 외에 [AEM Communities 6.5로 업그레이드](/help/communities/upgrade.md)를 읽고 커뮤니티 변경 사항에 대해 알아보십시오.

## 구성 {#configurations}

### 기본 게시자 {#primary-publisher}

선택한 배포가 [게시 팜](/help/communities/topologies.md#tarmk-publish-farm)인 경우 모든 인스턴스에서 발생해서는 안 되는 활동의 경우 하나의 AEM 게시 인스턴스를 **`primary publisher`**(으)로 식별해야 합니다. 예를 들어 **알림** 또는 **Adobe Analytics**&#x200B;에 의존하는 기능을 사용할 수 있습니다.

기본적으로 `AEM Communities Publisher Configuration` OSGi 구성은 **`Primary Publisher`** 확인란이 선택된 상태로 구성되므로 게시 팜의 모든 게시 인스턴스가 기본으로 자체 식별됩니다.

따라서 **`Primary Publisher`** 확인란의 선택을 취소하려면 **모든 보조 게시 인스턴스에서 구성을 편집**&#x200B;해야 합니다.

![primary-publisher](assets/primary-publisher.png)

게시 팜의 다른 모든(보조) 게시 인스턴스의 경우:

* 관리자 권한으로 로그인
* [웹 콘솔](/help/sites-deploying/configuring-osgi.md)에 액세스

   * 예: [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* `AEM Communities Publisher Configuration` 찾기
* 편집 아이콘 선택
* **기본 게시자** 상자 선택 취소
* **저장** 선택

### 작성자의 복제 에이전트 {#replication-agents-on-author}

복제는 게시 환경에서 만든 사이트 콘텐츠(예: 커뮤니티 그룹)에 사용되며 [터널 서비스](#tunnel-service-on-author)를 사용하여 작성 환경에서 구성원 및 구성원 그룹을 관리합니다.

기본 게시자의 경우 [복제 에이전트 구성](/help/sites-deploying/replication.md)이 게시 서버 및 인증된 사용자를 올바르게 식별하는지 확인하십시오. 기본 권한 있는 사용자 `admin,`은(는) 이미 적절한 사용 권한을 가지고 있습니다(`Communities Administrators`의 구성원).

일부 다른 사용자가 적절한 사용 권한을 가지려면 해당 사용자를 `administrators` 사용자 그룹(`Communities Administrators`의 구성원)의 구성원으로 추가해야 합니다.

작성 환경에는 전송 구성을 올바르게 구성해야 하는 두 개의 복제 에이전트가 있습니다.

* 작성자의 복제 콘솔 액세스

   * 전역 탐색에서 **[!UICONTROL 도구]** > **[!UICONTROL 배포]** > **[!UICONTROL 복제]** > **[!UICONTROL 작성자의 에이전트]**&#x200B;로 이동합니다.

* 두 에이전트에 대해 동일한 절차를 수행합니다.

   * **기본 에이전트(게시)**
   * **역방향 복제 에이전트(게시 역방향)**

      1. 에이전트 선택
      1. **편집** 선택
      1. **전송** 탭 선택
      1. `4503` 포트가 아닌 경우 **URI**&#x200B;를 편집하여 올바른 포트를 지정하십시오

      1. `admin` 사용자가 아닌 경우 **사용자** 및 **암호**&#x200B;를 편집하여 `administrators` 사용자 그룹의 구성원을 지정하십시오

다음 이미지에서는 포트를 4503에서 6103으로 변경한 결과를 다음과 같이 보여줍니다.

#### 기본 에이전트(게시) {#default-agent-publish}

![default-agent-publish](assets/default-agent-publish.png)

#### 역방향 복제 에이전트(게시 역방향) {#reverse-replication-agent-publish-reverse}

![역방향 복제 에이전트](assets/reverse-replication-agent.png)

### 작성자의 터널 서비스 {#tunnel-service-on-author}

작성자 환경을 사용하여 [사이트 만들기](/help/communities/sites-console.md), [사이트 속성 수정](/help/communities/sites-console.md#modifying-site-properties) 또는 [커뮤니티 구성원 관리](/help/communities/members.md)를 수행하는 경우 작성자에 등록된 사용자가 아닌 게시 환경에 등록된 구성원(사용자)에 액세스해야 합니다.

터널 서비스는 작성자의 복제 에이전트를 사용하여 이 액세스를 제공합니다.

터널 서비스를 활성화하려면

* 작성자 인스턴스에 대한 관리자 권한으로 로그인합니다.
* 게시자가 localhost:4503이 아니거나 전송 사용자가 `admin`이 아니면
[복제 에이전트를 구성합니다](#replication-agents-on-author)

* [웹 콘솔 액세스](/help/sites-deploying/configuring-osgi.md)

   * 예: [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

* `AEM Communities Publish Tunnel Service` 찾기
* 편집 아이콘 선택
* **활성화** 상자를 선택합니다.
* **저장** 선택

  ![터널 서비스](assets/tunnel-service.png)

### 암호화 키 복제 {#replicate-the-crypto-key}

AEM Communities에는 모든 AEM 서버 인스턴스가 동일한 암호화 키를 사용해야 하는 두 가지 기능이 있습니다. [분석](/help/communities/analytics.md) 및 [ASRP](/help/communities/asrp.md)입니다.

AEM 6.3 이상에서는 주요 자료가 파일 시스템에 저장되고 더 이상 저장소에 저장되지 않습니다.

작성자의 주요 자료를 다른 모든 인스턴스로 복사하려면 다음을 수행해야 합니다.

* 복사할 주요 자료가 포함된 AEM 인스턴스(일반적으로 작성자 인스턴스)에 액세스합니다

   * 로컬 파일 시스템에서 `com.adobe.granite.crypto.file` 번들을 찾고
예를 들어,

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`
      * `bundle.info` 파일은 번들을 식별합니다

   * 데이터 폴더로 이동하여
예를 들어,

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

      * hmac 및 기본 노드 파일 복사

* 각 대상 AEM 인스턴스에 대해

   * 데이터 폴더로 이동하여
예를 들어,

      * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

   * 이전에 복사한 두 파일 붙여넣기
   * 대상 AEM 인스턴스가 실행 중인 경우 [Granite Crypto 번들을 새로 고쳐야](#refresh-the-granite-crypto-bundle) 합니다.

>[!CAUTION]
>
>암호화 키를 기반으로 하는 다른 보안 기능이 이미 구성된 경우 암호화 키를 복제하면 구성이 손상될 수 있습니다. 도움이 필요하면 [고객 지원 센터에 문의](https://experienceleague.adobe.com/ko?support-solution=General&support-tab=home#support)하세요.

#### 저장소 복제 {#repository-replication}

AEM 6.2 및 이전 버전의 경우와 마찬가지로 주요 자료를 저장소에 저장할 수 있습니다. 각 AEM 인스턴스(초기 저장소 생성)의 첫 번째 시작 시 시스템 속성 `-Dcom.adobe.granite.crypto.file.disable=true`을(를) 지정하십시오.

>[!NOTE]
>
>작성자[&#128279;](#replication-agents-on-author)의 복제 에이전트가 올바르게 구성되었는지 확인하십시오.

저장소에 저장된 키 자료를 사용하여 작성자의 암호 키를 다른 인스턴스에 복제하는 방식은 다음과 같습니다.

[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) 사용:

* [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de)(으)로 이동
* `/etc/key` 선택
* `Replication` 탭 열기
* `Replicate` 선택

* [Granite Crypto 번들 새로 고침](#refresh-the-granite-crypto-bundle)

  ![replicare-repository](assets/replicare-repository.png)

#### Granite Crypto 번들 새로 고침 {#refresh-the-granite-crypto-bundle}

* 각 게시 인스턴스에서 [웹 콘솔](/help/sites-deploying/configuring-osgi.md)에 액세스합니다.

   * 예: [https://&lt;server>:&lt;port>/system/console/bundles](https://localhost:4503/system/console/bundles)

* `Adobe Granite Crypto Support` 번들 찾기(com.adobe.granite.crypto)
* **새로 고침** 선택

  ![granite-crypto](assets/granite-crypto.png)

* 잠시 후 **성공** 대화 상자가 나타납니다.
  `Operation completed successfully.`

### Apache HTTP 서버 {#apache-http-server}

Apache HTTP 서버를 사용하는 경우 모든 관련 항목에 올바른 서버 이름을 사용해야 합니다.

특히 `RedirectMatch`에서 `localhost`이(가) 아닌 올바른 서버 이름을 사용해야 합니다.

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

Dispatcher을 사용하는 경우 다음을 참조하십시오.

* AEM [Dispatcher](https://experienceleague.adobe.com/kr/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates) 설명서
* [Dispatcher 설치](https://experienceleague.adobe.com/ko/docs/experience-manager-dispatcher/using/getting-started/dispatcher-install)
* [커뮤니티에 대한 Dispatcher 구성](/help/communities/dispatcher.md)
* [알려진 문제](/help/communities/troubleshooting.md#dispatcher-refetch-fails)

## 관련 커뮤니티 설명서 {#related-communities-documentation}

* 커뮤니티 사이트 만들기, 커뮤니티 사이트 템플릿 구성, 커뮤니티 콘텐츠 관리, 구성원 관리 및 메시지 구성에 대해 알아보려면 [커뮤니티 사이트 관리](/help/communities/administer-landing.md)를 방문하십시오.

* SCF(소셜 구성 요소 프레임워크)에 대해 알아보고 커뮤니티 구성 요소와 기능을 사용자 지정하는 방법을 알아보려면 [커뮤니티 개발](/help/communities/communities.md)을 방문하십시오.

* 커뮤니티 구성 요소를 작성하고 구성하는 방법을 배울 수 있는 [커뮤니티 구성 요소 작성](/help/communities/author-communities.md)을 방문하십시오.
