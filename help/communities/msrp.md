---
title: MSRP - MongoDB 저장소 리소스 공급자
seo-title: MSRP - MongoDB 저장소 리소스 공급자
description: 관계형 데이터베이스를 공용 저장소로 사용하도록 AEM Communities 설정
seo-description: 관계형 데이터베이스를 공용 저장소로 사용하도록 AEM Communities 설정
uuid: 9fc06d4f-a60f-4ce3-8586-bcc836aa7de6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 048f7b30-20c3-4567-bd32-38cf2643cf39
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 1%

---


# MSRP - MongoDB 저장소 리소스 공급자 {#msrp-mongodb-storage-resource-provider}

## MSRP {#about-msrp} 정보

AEM Communities이 MSRP를 공용 저장소로 사용하도록 구성된 경우 동기화 또는 복제 없이도 모든 작성자 및 게시 인스턴스에서 사용자 생성 콘텐츠(UGC)에 액세스할 수 있습니다.

[SRP 옵션](working-with-srp.md#characteristics-of-srp-options) 및 [권장 토폴로지](topologies.md)도 참조하십시오.

## 요구 사항 {#requirements}

* [MongoDB](https://www.mongodb.org/):

   * 버전 2.6 이상
   * 관리 구성 또는 공유 필요 없음
   * [복제본 세트](#mongoreplicaset)의 사용을 적극 권장합니다.
   * AEM과 동일한 호스트에서 실행하거나 원격으로 실행할 수 있습니다.

* [Apache Solr](https://lucene.apache.org/solr/):

   * Solr 버전 7.0
   * 솔러는 Java 1.7 이상이 필요합니다.
   * 서비스가 필요하지 않습니다.
   * 실행 모드 선택:
      * 독립 실행형 모드
      * [SolrCloud 모드](solr.md#solrcloud-mode) (프로덕션 환경에 권장)
   * MLS(Multilingual Search) 선택:
      * [표준 MLS 설치](solr.md#installing-standard-mls)
      * [고급 MLS 설치](solr.md#installing-advanced-mls)

## MongoDB 구성 {#mongodb-configuration}

### MSRP {#select-msrp} 선택

[스토리지 구성 콘솔](srp-config.md)에서는 사용할 SRP 구현을 식별하는 기본 스토리지 구성을 선택할 수 있습니다.

작성자가 스토리지 구성 콘솔에 액세스하려면

* 전역 탐색에서 **[!UICONTROL 도구]** > **[!UICONTROL 커뮤니티]** > **[!UICONTROL 스토리지 구성]**&#x200B;을 선택합니다.

![msrp](assets/msrp.png)

* **[!UICONTROL MongoDB MSRP(저장소 리소스 공급자)]** 선택
* **[!UICONTROL mongoDB 구성]**

   * **[!UICONTROL mongoDB URI]**

      *기본값*:mongodb://localhost/?maxPoolSize=10&amp;waitQueueMultiple=5&amp;readPreference=secondaryPreferred

   * **[!UICONTROL mongoDB 데이터베이스]**

      *기본값*:커뮤니티

   * **[!UICONTROL mongoDB UGC 컬렉션]**

      *기본값*:콘텐트

   * **[!UICONTROL mongoDB 첨부 파일 컬렉션]**

      *기본값*:첨부 파일

* **[!UICONTROL SolrConfiguration]**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Zookeeper 호스트**

      외부 ZooKeeper와 함께 [SolrCloud 모드](solr.md#solrcloud-mode)에서 실행할 때 이 값을 *my.server.com:2181* 등 ZooKeeper의 `HOST:PORT`로 설정합니다.

      ZooKeeper Ensemble의 경우 *host1:2181,host2:2181* 등의 쉼표로 구분된 `HOST:PORT` 값을 입력합니다.

      내부 ZooKeeper를 사용하여 독립형 모드로 Solr를 실행하는 경우 비워 둡니다.
      *기본값*:  *&lt;blank>*

      * **[!UICONTROL 솔루션]**
URL독립 실행형 모드에서 Solr와 통신하는 데 사용되는 URL입니다.
SolrCloud 모드에서 실행되는 경우 비워 둡니다.

         *기본값*:https://127.0.0.1:8983/solr/

      * **[!UICONTROL Solr]**
CollectionSolr 컬렉션 이름입니다.

         *기본값*:collection1

* **[!UICONTROL 제출]**&#x200B;을 선택합니다

>[!NOTE]
>
>기본적으로 `communities`이라는 이름으로 설정되는 mongoDB 데이터베이스는 [노드 저장소 또는 데이터(이진) 스토어에 사용되는 데이터베이스의 이름으로 설정하면 안 됩니다](../../help/sites-deploying/data-store-config.md). AEM 6.5](../../help/sites-deploying/storage-elements-in-aem-6.md)의 [스토리지 요소를 참조하십시오.

### MongoDB 복제본 세트 {#mongodb-replica-set}

운영 환경의 경우 운영-보조 복제 및 자동 페일오버 기능을 구현하는 MongoDB 서버 클러스터인 복제본 세트를 설정하는 것이 좋습니다.

복제본 세트에 대한 자세한 내용은 MongoDB의 [Replication](https://docs.mongodb.org/manual/replication/) 설명서를 참조하십시오.

복제본 세트로 작업하고 응용 프로그램과 MongoDB 인스턴스 간 연결을 정의하는 방법을 알아보려면 MongoDB의 [연결 문자열 URI 형식](https://docs.mongodb.org/manual/reference/connection-string/) 설명서를 참조하십시오.

#### 복제본 세트 {#example-url-for-connecting-to-a-replica-set}에 연결하기 위한 예제 URL

```shell
# Example url for:
# servers "mongoserver1", "mongoserver2", "mongoserver3"
# replica set 'rs0'
# port numbers only necessary if not default port 27017
mongodb://mongoserver1:<mongoport1>,mongoserver2:<mongoport2>,mongoserver3:<mongoport3>/?replicaSet=rs0&maxPoolSize=100&waitQueueMultiple=50&readPreference=secondaryPreferred
```

## Solr 구성 {#solr-configuration}

다른 컬렉션을 사용하여 노드 스토어(Oak)와 공용 스토어(MSRP) 간에 솔루션 설치를 공유할 수 있습니다.

Oak 및 MSRP 컬렉션을 모두 집중적으로 사용하는 경우 성능상의 이유로 두 번째 솔러를 설치할 수 있습니다.

제작 환경의 경우, [SolrCloud 모드](solr.md#solrcloud-mode)는 독립 실행형 모드(단일 로컬 Solr 설정)를 통해 향상된 성능을 제공합니다.

구성에 대한 자세한 내용은 [SRP](solr.md)에 대한 솔루션 구성을 참조하십시오.

### 업그레이드 {#upgrading}

MSRP로 구성된 이전 버전에서 업그레이드하는 경우 다음을 수행해야 합니다.

1. AEM Communities](upgrade.md)로 [업그레이드 수행
1. 새 Solr 구성 파일 설치
   * [표준 MLS](solr.md#installing-standard-mls)의 경우
   * [고급 MLS](solr.md#installing-advanced-mls)의 경우
1. MSRP 색인 재지정
섹션 [MSRP 다시 인덱스 도구](#msrp-reindex-tool) 참조

## 구성 {#publishing-the-configuration} 게시

MSRP는 모든 작성자 및 게시 인스턴스에서 공용 스토어로 식별되어야 합니다.

게시 환경에서 동일한 구성을 사용할 수 있도록 하려면 작성 인스턴스에 로그인하고 다음 단계를 수행합니다.

* 주 메뉴에서 **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 복제]**&#x200B;로 이동합니다.
* **[!UICONTROL 트리 활성화]** 선택
* **[!UICONTROL 시작 경로]**:
   * `/etc/socialconfig/srpc/` 찾아보기
* **[!UICONTROL 활성화]** 선택

## 사용자 데이터 관리 {#managing-user-data}

게시 환경에 종종 입력되는 *사용자*, *사용자 프로필* 및 *사용자 그룹*&#x200B;에 대한 자세한 내용은 을 참조하십시오.

* [사용자 동기화](sync.md)
* [사용자 및 사용자 그룹 관리](users.md)

## MSRP 다시 인덱스 도구 {#msrp-reindex-tool}

새 구성 파일을 설치하거나 손상된 Solr 인덱스를 복구할 때 MSRP용 Solr를 다시 색인화하기 위한 HTTP 끝점이 있습니다.

이 도구를 사용하면 MongoDB가 MSRP에 대한 *truth*&#x200B;의 소스입니다.백업은 MongoDB에서만 사용할 수 있습니다.

*path *data 매개 변수에 의해 지정된 대로 전체 UGC 트리가 재인덱싱되거나 특정 하위 트리만 재인덱싱될 수 있습니다.

이 도구는 cURL 또는 다른 HTTP 도구를 사용하여 명령줄에서 실행할 수 있습니다.

다시 색인화할 때, UGC 레코드 수를 일괄 처리당 재인덱싱하는 것을 지정하는 *batchSize *data 매개 변수로 제어되는 메모리 및 성능 간의 상쇄 상황이 있습니다.

적절한 기본값은 5000입니다.

* 메모리가 문제인 경우 더 작은 숫자를 지정하십시오.
* 속도가 문제가 되는 경우 속도를 높이려면 더 큰 숫자를 지정하십시오.

### cURL 명령 {#running-msrp-reindex-tool-using-curl-command}을 사용하여 MSRP 다시 인덱스 도구 실행

다음 cURL 명령은 MSRP에 저장된 UGC를 다시 색인화하는 HTTP 요청에 필요한 사항을 보여줍니다.

기본 형식은 다음과 같습니다.

cURL -u *sigin* -d *data* *reindex-url*

*signing* = administrator-id:password 예:관리:관리

*data* = &quot;batchSize=*size*&amp;path=*path&quot;*

*size* = 작업당 다시 색인화할 UGC 항목 수 
`/content/usergenerated/asi/mongo/`

*path* = 다시 색인화할 UGC 트리의 루트 위치

* 모든 UGC를 다시 색인화하려면`asipath`
   `/etc/socialconfig/srpc/defaultconfiguration`
* 인덱스를 일부 UGC로 제한하려면 `asipath` 하위 트리를 지정합니다.

*reindex-url* = SRP의 다시 색인화를 위한 끝점 
`http://localhost:4503/services/social/datastore/mongo/reindex`

>[!NOTE]
>
>[DSRP Solr](dsrp.md)을(를) 다시 색인화하는 경우 URL은 **/services/social/datastore/rdb/reindex**&#x200B;입니다.

### MSRP 다시 인덱스 예 {#msrp-reindex-example}

```shell
curl -s -u admin:admin -d 'batchSize=10000&path=/content/usergenerated/asi/mongo/' http://localhost:4503/services/social/datastore/mongo/reindex
```

## MSRP 데모 방법 {#how-to-demo-msrp}

데모 또는 개발 환경에 대한 MSRP를 설정하려면 [HowTo Setup MongoDB for Demo](demo-mongo.md)을 참조하십시오.

## 문제 해결 {#troubleshooting}

### MongoDB {#ugc-not-visible-in-mongodb}에 UGC가 표시되지 않음

저장소 옵션의 구성을 확인하여 MSRP가 기본 공급자로 구성되었는지 확인합니다. 기본적으로 저장소 리소스 공급자는 JSRP입니다.

모든 작성자 및 게시 AEM 인스턴스에서 [스토리지 구성 콘솔](srp-config.md)을 다시 방문하거나 AEM 저장소를 확인합니다.

* JCR에서 [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)

   * [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) 노드가 포함되어 있지 않습니다. 이는 스토리지 공급자가 JSRP임을 의미합니다.
   * srpc 노드가 있고 노드 [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)을 포함하는 경우 기본 구성의 속성은 MSRP를 기본 공급자로 정의해야 합니다.

### 업그레이드 {#ugc-disappears-after-upgrade} 후 UGC가 사라짐

기존 AEM Communities 6.0 사이트에서 업그레이드하는 경우, AEM Communities 6.3으로 업그레이드한 후 기존 UGC를 [SRP](srp.md) API에 필요한 구조에 맞게 변환해야 합니다.

이러한 목적으로 GitHub에서 사용할 수 있는 오픈 소스 도구가 있습니다.

* [AEM Communities UGC 마이그레이션 도구](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

AEM Communities 6.1 이상 버전으로 가져오기 위해 AEM 소셜 커뮤니티의 이전 버전에서 UGC를 내보내도록 마이그레이션 도구를 사용자 지정할 수 있습니다.

### 오류 - 정의되지 않은 필드 provider_id {#error-undefined-field-provider-id}

로그에 다음 오류가 표시되면 Solr 스키마 파일이 제대로 구성되지 않았음을 나타냅니다.

#### JsonMappingException:정의되지 않은 필드 공급자_id {#jsonmappingexception-undefined-field-provider-id}

```xml
Caused by: com.fasterxml.jackson.databind.JsonMappingException: undefined field provider_id
at com.fasterxml.jackson.databind.ser.DefaultSerializerProvider.serializeValue(DefaultSerializerProvider.java:129)
at com.fasterxml.jackson.databind.ObjectMapper.writeValue(ObjectMapper.java:1819)
at com.adobe.cq.social.scf.core.BaseSocialComponent.toJSONString(BaseSocialComponent.java:196)
... 124 common frames omitted
```

오류를 해결하려면 [표준 MLS 설치](solr.md#installing-standard-mls)에 대한 지침을 따를 때 다음을 확인하십시오.

* XML 구성 파일이 올바른 솔루션 위치에 복사되었습니다.
* 새 구성 파일이 기존 구성 파일을 바꾼 후 솔러를 다시 시작했습니다.

### MongoDB에 대한 보안 연결 실패 {#secure-connection-to-mongodb-fails}

클래스 정의가 누락되어 MongoDB 서버에 대한 보안 연결을 시도하지 못하는 경우 공용 maven 저장소에서 사용할 수 있는 MongoDB 드라이버 번들 `mongo-java-driver`을(를) 업데이트해야 합니다.

1. [https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar](https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar)(버전 2.13.2 이상)에서 드라이버를 다운로드합니다.
1. AEM 인스턴스의 &quot;crx-quickstart/install&quot; 폴더에 번들을 복사합니다.
1. AEM 인스턴스를 다시 시작합니다.

## 리소스 {#resources}

* [AEM(MongoDB 포함)](../../help/sites-deploying/aem-with-mongodb.md)
* [MongoDB 설명서](https://docs.mongodb.org/)

