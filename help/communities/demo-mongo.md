---
title: 데모용 MongoDB를 설정하는 방법
description: 한 작성자 인스턴스 및 한 게시 인스턴스에 대해 MSRP를 설정하는 방법
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 7e257b34-a0f5-47db-b1a9-e26333c287d9
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 0%

---

# 데모용 MongoDB를 설정하는 방법 {#how-to-setup-mongodb-for-demo}

## 소개 {#introduction}

이 자습서에서는 *한 작성자* 인스턴스 및 *한 게시* 인스턴스에 대해 [MSRP](msrp.md)을(를) 설정하는 방법에 대해 설명합니다.

이 설정을 사용하면 사용자 생성 콘텐츠(UGC)를 전달하거나 역복제할 필요 없이 작성자 및 게시 환경 모두에서 커뮤니티 콘텐츠에 액세스할 수 있습니다.

이 구성은 개발 및/또는 데모와 같은 *비프로덕션* 환경에 적합합니다.

***프로덕션* 환경은 다음과 같아야 합니다.**

* 복제본 세트로 MongoDB 실행
* SolrCloud 사용
* 여러 게시자 인스턴스 포함

## 몽고DB {#mongodb}

### MongoDB 설치 {#install-mongodb}

* [https://www.mongodb.com/](https://www.mongodb.com/)에서 MongoDB 다운로드

   * OS 선택:

      * Linux®
      * Mac 10.8
      * 윈도우

   * 버전 선택:

      * 최소한 버전 2.6 사용

* 기본 구성

   * MongoDB 설치 지침을 따릅니다.
   * Mongod에 대한 구성:

      * 몽고나 분할을 구성할 필요가 없습니다.

   * 설치된 MongoDB 폴더를 &lt;mongo-install>이라고 합니다.
   * 정의된 데이터 디렉터리 경로를 &lt;mongo-dbpath>라고 합니다.

* MongoDB는 AEM과 동일한 호스트에서 실행되거나 원격으로 실행될 수 있습니다.

### MongoDB 시작 {#start-mongodb}

* &lt;mongo-install>/bin/mongod —dbpath &lt;mongo-dbpath>

이렇게 하면 기본 포트 유형을 사용하여 MongoDB 서버가 27017.

* Mac의 경우 시작 인수 &#39;ulimit -n 2048&#39;을 사용하여 ulimit을 늘립니다.

>[!NOTE]
>
>MongoDB가 *after* AEM에서 시작된 경우 **다시 시작** 모든 **AEM** 인스턴스가 MongoDB에 올바르게 연결하도록 합니다.

### 데모 프로덕션 옵션: MongoDB 복제본 세트 설정 {#demo-production-option-setup-mongodb-replica-set}

다음 명령은 localhost에 3개의 노드가 있는 복제본 세트를 설정하는 예제입니다.

* `bin/mongod --port 27017 --dbpath data --replSet rs0&`
* `bin/mongo`

   * `cfg = {"_id": "rs0","version": 1,"members": [{"_id": 0,"host": "127.0.0.1:27017"}]}`
   * `rs.initiate(cfg)`

* `bin/mongod --port 27018 --dbpath data1 --replSet rs0&`
* `bin/mongod --port 27019 --dbpath data2 --replSet rs0&`
* `bin/mongo`

   * `rs.add("127.0.0.1:27018")`
   * `rs.add("127.0.0.1:27019")`
   * `rs.status()`

## Solr {#solr}

### Solr 설치 {#install-solr}

* [Apache Lucene](https://archive.apache.org/dist/lucene/solr/)에서 Solr 다운로드:

   * 모든 OS에 적합합니다.
   * Solr 버전 7.0.
   * Solr에는 Java™ 1.7 이상이 필요합니다.

* 기본 구성

   * &#39;example&#39; Solr 설정을 따르십시오.
   * 서비스가 필요하지 않습니다.
   * 설치된 Solr 폴더를 &lt;solr-install>이라고 합니다.

### AEM Communities용 Solr 구성 {#configure-solr-for-aem-communities}

데모용 MSRP에 대한 Solr 컬렉션을 구성하려면 두 가지 결정을 내려야 합니다(자세한 내용은 기본 설명서에 대한 링크 선택).

1. 독립 실행형 또는 [SolrCloud 모드](msrp.md#solrcloudmode)에서 Solr을 실행합니다.
1. [표준](msrp.md#installingstandardmls) 또는 [고급](msrp.md#installingadvancedmls) 다국어 검색(MLS)을 설치하십시오.

### 독립형 Solr {#standalone-solr}

Solr 실행 방법은 버전 및 설치 방식에 따라 다를 수 있습니다. [Solr 참조 안내서](https://archive.apache.org/dist/lucene/solr/ref-guide/)은(는) 신뢰할 수 있는 문서입니다.

간소화를 위해 버전 4.10을 예로 사용하여 독립 실행형 모드에서 Solr을 시작하십시오.

* &lt;solrinstall>/example로 cd
* Java™ -jar start.jar

이 프로세스는 기본 포트 8983을 사용하여 Solr HTTP 서버를 시작합니다. Solr 콘솔로 이동하여 테스트할 Solr 콘솔을 가져올 수 있습니다.

* 기본 Solr 콘솔: [http://localhost:8983/solr/](http://localhost:8983/solr/)

>[!NOTE]
>
>Solr 콘솔을 사용할 수 없는 경우 &lt;solrinstall>/example/logs 아래의 로그를 확인하십시오. SOLR이 해결할 수 없는 특정 호스트 이름에 바인딩하려고 하는지 확인합니다(예: &quot;user-macbook-pro&quot;).
>
이 경우 `etc/hosts` 파일을 이 호스트 이름에 대한 새 항목(예: 127.0.0.1 user-macbook-pro)으로 업데이트하여 Solr을 올바르게 시작합니다.

### SolrCloud {#solrcloud}

프로덕션이 아닌 기본 solrCloud 설정을 실행하려면 다음 명령을 사용하여 Solr을 시작하십시오.

* `java -Dbootstrap_confdir=./solr/collection1/conf -Dbootstrap_conf=true -DzkRun -jar start.jar`

## MongoDB를 일반 저장소로 식별 {#identify-mongodb-as-common-store}

필요한 경우 작성자를 실행하고 AEM 인스턴스를 게시합니다.

MongoDB가 시작되기 전에 AEM이 실행 중이었다면 AEM 인스턴스를 다시 시작해야 합니다.

기본 설명서 페이지의 지침을 따르십시오. [MSRP - MongoDB 일반 저장소](msrp.md)

## 테스트 {#test}

MongoDB 일반 스토어를 테스트하고 확인하려면 게시 인스턴스에 댓글을 게시하고 작성자 인스턴스에서 보고 MongoDB 및 Solr에서 UGC를 봅니다.

1. 게시 인스턴스에서 [커뮤니티 구성 요소 안내서](http://localhost:4503/content/community-components/en/comments.html) 페이지로 이동하여 댓글 구성 요소를 선택합니다.
1. 댓글을 게시하려면 로그인하십시오.
1. 댓글 텍스트 입력 상자에 텍스트를 입력하고 **[!UICONTROL Post]**&#x200B;을(를) 클릭합니다.

   ![댓글 게시](assets/post-comment.png)

1. [작성자 인스턴스](http://localhost:4502/content/community-components/en/comments.html)에서 댓글을 확인하기만 하면 됩니다(관리자/관리자로 로그인했을 수 있음).

   ![댓글 보기](assets/view-comment.png)

   참고: 작성자의 *asipath* 아래에 JCR 노드가 있지만 이러한 노드는 SCF 프레임워크용입니다. 실제 UGC는 JCR에 있지 않습니다. MongoDB에 있습니다.

1. mongodb **[!UICONTROL 커뮤니티]** > **[!UICONTROL 컬렉션]** > **[!UICONTROL 컨텐츠]**&#x200B;에서 UGC 보기

   ![ugc-content](assets/ugc-content.png)

1. Solr에서 UGC 보기:

   * Solr 대시보드로 이동합니다. [http://localhost:8983/solr/](http://localhost:8983/solr/).
   * `core selector` 사용자가 `collection1`을(를) 선택할 수 있습니다.
   * `Query`을(를) 선택합니다.
   * `Execute Query`을(를) 선택합니다.

   ![ugc-solr](assets/ugc-solr.png)

## 문제 해결 {#troubleshooting}

### UGC가 나타나지 않음 {#no-ugc-appears}

1. MongoDB가 설치되어 제대로 실행 중인지 확인하십시오.

1. MSRP가 기본 공급자로 구성되었는지 확인합니다.

   * 모든 작성자 및 게시 AEM 인스턴스에서 [저장소 구성 콘솔](srp-config.md)을 다시 방문하거나 AEM 저장소를 확인하십시오.

   * JCR에서 [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)에 [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) 노드가 없으면 저장소 공급자가 JSRP입니다.
   * srpc 노드가 존재하고 [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration) 노드를 포함하는 경우 defaultconfiguration의 속성은 MSRP를 기본 공급자로 정의해야 합니다.

1. MSRP를 선택한 후 AEM이 다시 시작되었는지 확인하십시오.
