---
title: MongoDB for Demo 설정 방법
seo-title: MongoDB for Demo 설정 방법
description: 하나의 작성자 인스턴스 및 하나의 게시 인스턴스에 대해 MSRP를 설정하는 방법
seo-description: 하나의 작성자 인스턴스 및 하나의 게시 인스턴스에 대해 MSRP를 설정하는 방법
uuid: d2035a9e-f05c-4f90-949d-7cdae9646750
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 0b126218-b142-4d33-a28c-a91ab4fe99ac
translation-type: tm+mt
source-git-commit: d6c8bbb9aa763a2eb6660b6b6755aba75241e394

---


# MongoDB for Demo 설정 방법 {#how-to-setup-mongodb-for-demo}

## 소개 {#introduction}

이 자습서에서는 [하나의 작성자](msrp.md) 인스턴스와 *하나의 게시* 인스턴스에 대해 MSRP를 설정하는 방법에 대해 설명합니다 ** .

이 설정을 통해 UGC(사용자 생성 콘텐츠)를 전달 또는 역복제할 필요 없이 작성 및 게시 환경에서 커뮤니티 콘텐츠에 액세스할 수 있습니다.

이 구성은 개발 및/또는 데모와 같은 *비프로덕션* 환경에 적합합니다.

**제작&#x200B;*환경에서는*다음 작업을 수행해야 합니다.**

* 복제본 세트로 MongoDB 실행
* SolrCloud 사용
* 여러 게시자 인스턴스 포함

## MongoDB {#mongodb}

### MongoDB 설치 {#install-mongodb}

* https://www.mongodb.org/에서 MongoDB [다운로드](https://www.mongodb.org/)

   * OS 선택:

      * Linux
      * Mac 10.8
      * Windows 7
   * 버전 선택:

      * 버전 2.6은 최소


* 기본 구성

   * MongoDB 설치 지침을 따르십시오.
   * Configure for mongod

      * No need to configure mongos or sharding
   * 설치된 MongoDB 폴더는 &lt;mongo-install>이라고 합니다.
   * 정의된 데이터 디렉토리 경로는 &lt;mongo-dbpath>라고 합니다.


* MongoDB는 AEM과 동일한 호스트에서 실행되거나 원격으로 실행될 수 있습니다.

### MongoDB 시작 {#start-mongodb}

* &lt;mongo-install>/bin/mongod —dbpath &lt;mongo-dbpath>

기본 포트 27017을 사용하여 MongoDB 서버를 시작합니다.

* Mac의 경우 시작 인수 &#39;ulimit -n 2048&#39;을 사용하여 제한 증가

>[!NOTE]
>
>AEM *이후에* MongoDB가 시작된 경우 모든 AEM **인스턴스를 다시** **** 시작하여MongoDB에올바르게 연결합니다.

### 데모 제작 옵션:MongoDB 복제본 세트 설정 {#demo-production-option-setup-mongodb-replica-set}

다음 명령은 localhost에서 노드가 3개인 복제본 세트를 설정하는 예입니다.

* bin/mongod —port 27017 —dbpath data —replSet rs0&amp;
* bin/mongo

   * cfg = {&quot;_id&quot;:&quot;rs0&quot;,&quot;version&quot;:1, &quot;구성원&quot;: [{&quot;_id&quot;:0,&quot;호스트&quot;:&quot;127.0.0.1:27017&quot;}]}
   * rs.initiate(cfg)

* bin/mongod —port 27018 —dbpath data1 —replSet rs0&amp;
* bin/mongod —port 27019 —dbpath data2 —replSet rs0&amp;
* bin/mongo

   * rs.add(&quot;127.0.0.1:27018&quot;)
   * rs.add(&quot;127.0.0.1:27019&quot;)
   * rs.status()

## Solr {#solr}

### 솔루션 설치 {#install-solr}

* Apache Lucene에서 [솔루션 다운로드](https://archive.apache.org/dist/lucene/solr/):

   * 모든 OS에 적합
   * 버전 4.10 또는 버전 5 사용
   * 솔러에는 Java 1.7 이상이 필요합니다.

* 기본 구성

   * &#39;예&#39; 솔루션 설정
   * 서비스가 필요하지 않습니다.
   * 설치된 Solr 폴더를 &lt;solr-install>이라고 합니다.

### AEM Communities용 솔루션 구성 {#configure-solr-for-aem-communities}

데모를 위해 MSRP용 Solr 컬렉션을 구성하려면 다음 두 가지 결정을 해야 합니다(자세한 내용은 기본 설명서에 대한 링크 선택).

1. 독립형 또는 SolrCloud [모드에서 Solr 실행](msrp.md#solrcloudmode)
1. 표준 [또는](msrp.md#installingstandardmls) 고급 [](msrp.md#installingadvancedmls) 다국어 검색(MLS) 설치

### 독립 실행형 솔루션 {#standalone-solr}

Solr 실행 방법은 설치 버전 및 방법에 따라 다를 수 있습니다. 솔루션 [참조 안내서는](https://archive.apache.org/dist/lucene/solr/ref-guide/) 신뢰할 수 있는 문서입니다.

간단하게 4.10 버전을 예로 사용하여 Solr를 독립 실행형 모드로 시작합니다.

* cd to &lt;solrinstall>/example
* java -jar start.jar

기본 포트 8983을 사용하여 Solr HTTP 서버가 시작됩니다. Solr Console에서 테스트를 위한 솔루션 콘솔을 가져올 수 있습니다.

* 기본 솔루션 콘솔: [http://localhost:8983/solr/](http://localhost:8983/solr/)

>[!NOTE]
>
>Solr Console을 사용할 수 없는 경우 &lt;solrinstall>/example/logs 아래에서 로그를 확인하십시오. SOLR이 확인할 수 없는 특정 호스트 이름(예:&quot;user-macbook-pro&quot;).
이 경우 이 호스트 이름(예: 127.0.0.1 user-macbook-pro)에 대한 새 항목으로 etc/hosts 파일을 업데이트하고 Solr이 제대로 시작됩니다.

### SolrCloud {#solrcloud}

프로덕션이 아닌 매우 기본적인 솔루션을 실행하려면 다음을 사용하여 시작합니다.

* java -Dbootstrap_confdir=./solr/collection1/conf -Dbootstrap_conf=true -DzkRun -jar start.jar

## MongoDB를 일반 스토어로 식별 {#identify-mongodb-as-common-store}

필요한 경우 작성자를 실행하고 AEM 인스턴스를 게시합니다.

MongoDB를 시작하기 전에 AEM이 실행 중이면 AEM 인스턴스를 다시 시작해야 합니다.

기본 설명서 페이지의 지침을 따르십시오.MSRP [- MongoDB 공용 스토어](msrp.md)

## 테스트 {#test}

MongoDB 공용 저장소를 테스트하고 확인하려면 게시 인스턴스에 주석을 게시하고 작성자 인스턴스에서 보고 MongoDB 및 Solr에서 UGC를 확인합니다.

1. 게시 인스턴스에서 커뮤니티 구성 요소 [안내서](http://localhost:4503/content/community-components/en/comments.html) 페이지로 이동하여 주석 구성 요소를 선택합니다.
1. 로그인하여 댓글 게시:
1. 댓글 텍스트 입력 상자에 텍스트를 입력하고 게시물을 **[!UICONTROL 클릭합니다]**

   ![chlimage_1-191](assets/chlimage_1-191.png)

1. 주석을 [작성자 인스턴스에서](http://localhost:4502/content/community-components/en/comments.html) 볼 수 있습니다(여전히 admin / admin으로 로그인됨).

   ![chlimage_1-192](assets/chlimage_1-192.png)

   참고:author의 Asipath 아래에 JCR *노드가* 있는 동안 SCF 프레임워크에 사용됩니다. 실제 UGC는 JCR에 있지 않고 MongoDB에 있습니다.

1. mongodb Communities > Collections **[!UICONTROL > Content에서 UGC 보기]**

   ![chlimage_1-193](assets/chlimage_1-193.png)

1. 솔어에서 UGC 보기:

   * Solr 대시보드 찾아보기: [http://localhost:8983/solr/](http://localhost:8983/solr/)
   * 선택할 `core selector` 사용자 `collection1`
   * 선택 `Query`
   * 선택 `Execute Query`
   ![chlimage_1-194](assets/chlimage_1-194.png)

## 문제 해결 {#troubleshooting}

### UGC 표시 안 함 {#no-ugc-appears}

1. MongoDB가 설치되어 제대로 실행되고 있는지 확인합니다.

1. MSRP 파섹

   * 모든 작성 및 게시 AEM 인스턴스에서 스토리지 구성 [콘솔 다시 방문](srp-config.md)
   또는 AEM 리포지토리 확인:

   * JCR에서, if/etc/socialconfig [](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)

      * srpc [노드를 포함하지](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) 않음, 즉 스토리지 공급자가 JSRP임을 의미합니다.
      * srpc 노드가 존재하고 노드 [기본 구성을](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)포함하는 경우 기본 구성의 속성은 MSRP를 기본 공급자로 정의해야 합니다


1. MSRP를 선택한 후 AEM이 다시 시작되었는지 확인합니다.
