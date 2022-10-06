---
title: 데모 MongoDB를 설정하는 방법
seo-title: How to Setup MongoDB for Demo
description: 하나의 작성자 인스턴스 및 하나의 게시 인스턴스에 대해 MSRP를 설정하는 방법
seo-description: How to setup MSRP for one author instance and one publish instance
uuid: d2035a9e-f05c-4f90-949d-7cdae9646750
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 0b126218-b142-4d33-a28c-a91ab4fe99ac
role: Admin
exl-id: 7e257b34-a0f5-47db-b1a9-e26333c287d9
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '774'
ht-degree: 1%

---

# 데모 MongoDB를 설정하는 방법 {#how-to-setup-mongodb-for-demo}

## 소개 {#introduction}

이 자습서에서는 설정 방법을 설명합니다 [MSRP](msrp.md) 대상 *작성자* 인스턴스 및 *하나의 게시* 인스턴스.

이 설정을 사용하면 UGC(사용자 생성 컨텐츠)를 전달하거나 역복제할 필요 없이 작성자 및 게시 환경 모두에서 커뮤니티 컨텐츠에 액세스할 수 있습니다.

이 구성은 다음 경우에 적합합니다 *비프로덕션* 개발 및/또는 데모 등의 환경.

**A *production* 환경은 다음과 같습니다.**

* 복제본 세트를 사용하여 MongoDB 실행
* SolrCloud 사용
* 여러 게시자 인스턴스 포함

## MongoDB {#mongodb}

### MongoDB 설치 {#install-mongodb}

* MongoDB 다운로드 위치 [https://www.mongodb.org/](https://www.mongodb.org/)

   * OS 선택:

      * Linux
      * Mac 10.8
      * Windows 7
   * 버전 선택:

      * 최소한 버전 2.6 사용


* 기본 구성

   * MongoDB 설치 지침을 따릅니다.
   * 다음에 대한 구성:

      * 관리 또는 공유를 구성할 필요가 없습니다.
   * 설치된 MongoDB 폴더를 &lt;mongo-install>.
   * 정의된 데이터 디렉토리 경로를 &lt;mongo-dbpath>.


* MongoDB는 AEM과 동일한 호스트에서 실행하거나 원격으로 실행할 수 있습니다.

### MongoDB 시작 {#start-mongodb}

* &lt;mongo-install>/bin/mongoom —dbpath &lt;mongo-dbpath>

이렇게 하면 기본 포트 27017을 사용하여 MongoDB 서버가 시작됩니다.

* Mac의 경우 시작 인수 &#39;ulimit -n 2048&#39;로 제한 값을 늘립니다

>[!NOTE]
>
>MongoDB가 시작된 경우 *after* AEM, **다시 시작** 모두 **AEM** 인스턴스를 사용하여 MongoDB에 올바르게 연결합니다.

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

* 솔루션 다운로드 위치 [Apache Lucene](https://archive.apache.org/dist/lucene/solr/):

   * 모든 OS에 적합합니다.
   * 솔루션 버전 7.0.
   * 솔러는 Java 1.7 이상이 필요합니다.

* 기본 구성

   * &#39;example&#39; Solr 설정을 따릅니다.
   * 서비스가 필요하지 않습니다.
   * 설치된 Solr 폴더를 &lt;solr-install>.

### AEM Communities용 솔루션 구성 {#configure-solr-for-aem-communities}

데모 목적으로 MSRP용 Solr 컬렉션을 구성하려면 다음 두 가지 결정을 수행해야 합니다(자세한 내용은 기본 설명서에 대한 링크 선택).

1. 독립형 또는 [SolrCloud 모드](msrp.md#solrcloudmode).
1. 설치 [standard](msrp.md#installingstandardmls) 또는 [고급](msrp.md#installingadvancedmls) 다국어 검색(MLS).

### 독립형 솔루션 {#standalone-solr}

Solr 실행 방법은 설치 버전 및 방식에 따라 다를 수 있습니다. 다음 [솔루션 참조 안내서](https://archive.apache.org/dist/lucene/solr/ref-guide/) 는 권위 있는 문서입니다.

간단히 설명하자면 버전 4.10을 예로 사용하여 Solr를 독립형 모드로 시작합니다.

* cd로 &lt;solrinstall>/예
* java -jar start.jar

기본 포트 8983을 사용하여 Solr HTTP 서버가 시작됩니다. Solr 콘솔로 이동하여 테스트할 Solr 콘솔을 가져올 수 있습니다.

* 기본 콘솔: [http://localhost:8983/solr/](http://localhost:8983/solr/)

>[!NOTE]
>
>Solr Console을 사용할 수 없는 경우 아래의 로그를 확인합니다. &lt;solrinstall>/example/logs SOLR이 확인할 수 없는 특정 호스트 이름(예: &quot;user-macbook-pro&quot;)
이 경우 etc/hosts 파일을 이 호스트 이름의 새 항목(예: 127.0.0.1 user-macbook-pro)으로 업데이트하면 Solr이 제대로 시작됩니다.

### SolrCloud {#solrcloud}

매우 기본적인(프로덕션 아님) solrCloud 설정을 실행하려면 다음을 사용하여 솔루션을 시작합니다.

* `java -Dbootstrap_confdir=./solr/collection1/conf -Dbootstrap_conf=true -DzkRun -jar start.jar`

## MongoDB를 공용 스토어로 식별 {#identify-mongodb-as-common-store}

필요한 경우 작성자 및 게시 AEM 인스턴스를 시작합니다.

AEM이 MongoDB가 시작되기 전에 실행 중이라면 AEM 인스턴스를 다시 시작해야 합니다.

기본 설명서 페이지의 지침을 따르십시오. [MSRP - MongoDB 공용 저장소](msrp.md)

## 테스트 {#test}

MongoDB 공용 저장소를 테스트하고 확인하려면 게시 인스턴스에 주석을 게시하고 작성자 인스턴스에서 보고 MongoDB 및 Solr에서 UGC를 확인합니다.

1. 게시 인스턴스에서 [커뮤니티 구성 요소 안내서](http://localhost:4503/content/community-components/en/comments.html) 페이지를 열고 Comments 구성 요소를 선택합니다.
1. 댓글을 게시하려면 로그인:
1. 주석 텍스트 입력 상자에 텍스트를 입력하고 **[!UICONTROL Post]**

   ![댓글 게시](assets/post-comment.png)

1. 에서 댓글을 확인하기만 하면 됩니다. [작성자 인스턴스](http://localhost:4502/content/community-components/en/comments.html) (관리자/관리자로 계속 로그인 가능).

   ![보기 주석](assets/view-comment.png)

   참고: 에는 JCR 노드가 있지만 *asipath* 작성자는 SCF 프레임워크를 위한 것입니다. 실제 UGC는 JCR에 없으며 MongoDB에 있습니다.

1. mongodb에서 UGC 보기 **[!UICONTROL 커뮤니티]** > **[!UICONTROL 컬렉션]** > **[!UICONTROL 컨텐츠]**

   ![ugc 컨텐츠](assets/ugc-content.png)

1. 솔더에서 UGC 보기:

   * 솔루션 대시보드로 이동합니다. [http://localhost:8983/solr/](http://localhost:8983/solr/).
   * 사용자 `core selector` 을(를) 선택합니다. `collection1`.
   * 선택 `Query`.
   * 선택 `Execute Query`.

   ![ugc-solr](assets/ugc-solr.png)

## 문제 해결 {#troubleshooting}

### UGC가 표시되지 않음 {#no-ugc-appears}

1. MongoDB가 설치되어 제대로 실행 중인지 확인하십시오.

1. MSRP가 기본 공급자로 구성되었는지 확인합니다.

   * 모든 작성 및 게시 AEM 인스턴스에서 을 다시 방문하여 [스토리지 구성 콘솔](srp-config.md) 또는 AEM 저장소를 확인합니다.

   * JCR에서 [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/) 다음을 포함하지 않음 [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) node이면 스토리지 공급자가 JSRP임을 의미합니다.
   * srpc 노드가 존재하며 노드를 포함하는 경우 [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)를 지정하는 경우, 기본 구성의 속성은 MSRP를 기본 공급자로 정의해야 합니다.

1. MSRP를 선택한 후 AEM이 다시 시작되었는지 확인합니다.
