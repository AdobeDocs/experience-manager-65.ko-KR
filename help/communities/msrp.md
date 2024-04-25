---
title: MSRP - MongoDB 저장소 리소스 공급자
description: 관계형 데이터베이스를 공통 저장소로 사용하도록 AEM Communities 설정
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 799d5ae1-caac-4c92-8835-696ad25de553
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1142'
ht-degree: 0%

---

# MSRP - MongoDB 저장소 리소스 공급자 {#msrp-mongodb-storage-resource-provider}

## MSRP 정보 {#about-msrp}

AEM Communities이 MSRP를 공통 저장소로 사용하도록 구성된 경우 UGC(사용자 생성 컨텐츠)는 동기화나 복제 없이 모든 작성자 및 게시 인스턴스에서 액세스할 수 있습니다.

참조: [SRP 옵션의 특성](working-with-srp.md#characteristics-of-srp-options) 및 [권장 토폴로지](topologies.md).

## 요구 사항 {#requirements}

* [몽고DB](https://www.mongodb.org/):

   * 버전 2.6 이상
   * 몽고 또는 분할을 구성할 필요가 없음
   * 의 강력한 사용 권장 [복제 데이터베이스 집합](#mongoreplicaset)
   * AEM과 동일한 호스트에서 실행되거나 원격으로 실행될 수 있음

* [Apache Solr](https://lucene.apache.org/solr/):

   * Solr 버전 7.0
   * Solr에는 Java 1.7 이상이 필요합니다.
   * 서비스가 필요하지 않습니다.
   * 실행 모드 선택:
      * 독립형 모드
      * [SolrCloud 모드](solr.md#solrcloud-mode) (프로덕션 환경에 권장)
   * 다국어 검색(MLS) 선택:
      * [표준 MLS 설치](solr.md#installing-standard-mls)
      * [고급 MLS 설치](solr.md#installing-advanced-mls)

## MongoDB 구성 {#mongodb-configuration}

### MSRP 선택 {#select-msrp}

다음 [스토리지 구성 콘솔](srp-config.md) 에서는 사용할 SRP 구현을 식별하는 기본 스토리지 구성을 선택할 수 있습니다.

작성자의 경우 스토리지 구성 콘솔에 액세스하려면 다음을 수행하십시오.

* 전역 탐색에서 을 선택합니다. **[!UICONTROL 도구]** > **[!UICONTROL 커뮤니티]** > **[!UICONTROL 스토리지 구성]**.

![msrp](assets/msrp.png)

* 선택 **[!UICONTROL MongoDB 저장소 리소스 제공자(MSRP)]**
* **[!UICONTROL mongoDB 구성]**

   * **[!UICONTROL mongoDB URI]**

     *기본값*: mongodb://localhost/?maxPoolSize=10&amp;waitQueueMultiple=5&amp;readPreference=secondaryPreferred

   * **[!UICONTROL mongoDB 데이터베이스]**

     *기본값*: 커뮤니티

   * **[!UICONTROL mongoDB UGC 컬렉션]**

     *기본값*: 콘텐츠

   * **[!UICONTROL mongoDB 첨부 파일 컬렉션]**

     *기본값*: 첨부 파일

* **[!UICONTROL SolrConfiguration]**

   * **[Zookeeper](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files) 호스트**

     에서 실행할 때 [SolrCloud 모드](solr.md#solrcloud-mode) 외부 ZooKeeper를 사용하여 이 값을 `HOST:PORT` ZooKeeper의 경우 다음과 같습니다. *my.server.com:2181*

     Zookeeper Ensemble의 경우 쉼표로 구분하여 입력합니다. `HOST:PORT` 값(예: ) *host1:2181,host2:2181*

     내부 ZooKeeper를 사용하여 Solr을 독립 실행형 모드로 실행하는 경우 비워 둡니다.
     *기본값*: *&lt;blank>*

      * **[!UICONTROL Solr URL]**
독립 실행형 모드에서 Solr과 통신하는 데 사용되는 URL입니다.
SolrCloud 모드에서 실행하는 경우 비워 둡니다.
        *기본값*: https://127.0.0.1:8983/solr/

      * **[!UICONTROL Solr 컬렉션]**
Solr 컬렉션 이름입니다.
        *기본값*: collection1

* 선택 **[!UICONTROL 제출]**

>[!NOTE]
>
>mongoDB 데이터베이스, 기본값: `communities`를 사용 중인 데이터베이스 이름으로 설정하면 안 됩니다. [노드 저장소 또는 데이터(바이너리) 저장소](../../help/sites-deploying/data-store-config.md). 참조: [AEM 6.5의 저장소 요소](../../help/sites-deploying/storage-elements-in-aem-6.md).

### MongoDB 복제본 집합 {#mongodb-replica-set}

운영 환경의 경우 주-보조 복제 및 자동 장애 조치를 구현하는 MongoDB 서버의 클러스터인 복제본 세트를 설정하는 것이 좋습니다.

복제본 세트에 대한 자세한 내용은 MongoDB의 [복제](https://docs.mongodb.org/manual/replication/) 설명서를 참조하십시오.

복제본 세트로 작업하고 애플리케이션과 MongoDB 인스턴스 간의 연결을 정의하는 방법을 알아보려면 MongoDB의 [연결 문자열 URI 형식](https://docs.mongodb.org/manual/reference/connection-string/) 설명서를 참조하십시오.

#### 복제본 세트에 연결하기 위한 예제 Url  {#example-url-for-connecting-to-a-replica-set}

```shell
# Example url for:
# servers "mongoserver1", "mongoserver2", "mongoserver3"
# replica set 'rs0'
# port numbers only necessary if not default port 27017
mongodb://mongoserver1:<mongoport1>,mongoserver2:<mongoport2>,mongoserver3:<mongoport3>/?replicaSet=rs0&maxPoolSize=100&waitQueueMultiple=50&readPreference=secondaryPreferred
```

## Solr 구성 {#solr-configuration}

Solr 설치는 다른 컬렉션을 사용하여 노드 저장소(Oak)와 공통 저장소(MSRP) 간에 공유할 수 있습니다.

Oak 컬렉션과 MSRP 컬렉션을 모두 집중적으로 사용하는 경우 성능상의 이유로 두 번째 Solr을 설치할 수 있습니다.

프로덕션 환경의 경우 [SolrCloud 모드](solr.md#solrcloud-mode) 는 독립형 모드(단일 로컬 Solr 설정)보다 향상된 성능을 제공합니다.

구성에 대한 자세한 내용은 [SRP에 대한 Solr 구성](solr.md).

### 업그레이드 중 {#upgrading}

MSRP로 구성된 이전 버전에서 업그레이드하는 경우 다음을 수행해야 합니다.

1. 다음을 수행합니다. [AEM Communities으로 업그레이드](upgrade.md)
1. 새 Solr 구성 파일 설치
   * 대상 [표준 MLS](solr.md#installing-standard-mls)
   * 대상 [고급 MLS](solr.md#installing-advanced-mls)
1. MSRP 색인 재지정 섹션 참조 [MSRP 색인 재지정 도구](#msrp-reindex-tool)

## 구성 게시 {#publishing-the-configuration}

MSRP는 모든 작성자 및 게시 인스턴스에서 공통 저장소로 식별되어야 합니다.

게시 환경에서 동일한 구성을 사용할 수 있도록 하려면 작성자 인스턴스에 로그인하고 단계를 수행합니다.

* 메인 메뉴에서 다음으로 이동 **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 복제]**.
* 선택 **[!UICONTROL 트리 활성화]**
* **[!UICONTROL 시작 경로]**:
   * 다음으로 이동 `/etc/socialconfig/srpc/`
* 선택 **[!UICONTROL 활성화]**

## 사용자 데이터 관리 {#managing-user-data}

에 관한 정보를 위하여 *사용자*, *사용자 프로필* 및 *사용자 그룹*, 종종 게시 환경에 입력됨, 방문

* [사용자 동기화](sync.md)
* [사용자 및 사용자 그룹 관리](users.md)

## MSRP 색인 재지정 도구 {#msrp-reindex-tool}

새 구성 파일을 설치하거나 손상된 Solr 인덱스를 복구할 때 MSRP용 Solr을 다시 인덱싱하기 위한 HTTP 끝점이 있습니다.

이 도구를 사용하는 경우 MongoDB는 *진실* msrp의 경우, 백업은 MongoDB에서만 수행할 수 있습니다.

전체 UGC 트리는 *path *data 매개 변수에 지정된 대로 다시 인덱싱되거나 특정 하위 트리만 다시 인덱싱될 수 있습니다.

이 도구는 cURL 또는 기타 HTTP 도구를 사용하여 명령줄에서 실행할 수 있습니다.

리인덱싱할 때 일괄 처리당 얼마나 많은 UGC 레코드가 리인덱싱되는지를 지정하는 *batchSize *data 매개 변수에 의해 제어되는 성능과 메모리 간에 트레이드오프가 발생합니다.

적절한 기본값은 5000입니다.

* 메모리에 문제가 있는 경우 더 작은 숫자를 지정하십시오
* 속도가 문제인 경우 더 큰 숫자를 지정하여 속도를 높입니다.

### cURL 명령을 사용하여 MSRP 색인 재지정 도구 실행 {#running-msrp-reindex-tool-using-curl-command}

다음 cURL 명령은 HTTP 요청이 MSRP에 저장된 UGC를 다시 인덱싱하는 데 필요한 사항을 보여줍니다.

기본 형식은 다음과 같습니다.

cURL -u *로그인* -d *데이터* *reindex-url*

*로그인* = administrator-id:password 예: admin:admin

*데이터* = &quot;batchSize=*크기*&#x200B;경로(&amp;path=)*경로&quot;*

*크기* = 작업당 다시 인덱싱할 UGC 항목 수
`/content/usergenerated/asi/mongo/`

*경로* = 다시 인덱싱할 UGC 트리의 루트 위치

* 모든 UGC를 다시 인덱싱하려면 `asipath`다음의 속성
  `/etc/socialconfig/srpc/defaultconfiguration`
* 인덱스를 일부 UGC로 제한하려면 다음 중 하위 트리를 지정하십시오. `asipath`

*reindex-url* = SRP 리인덱싱의 끝점
`http://localhost:4503/services/social/datastore/mongo/reindex`

>[!NOTE]
>
>다음과 같은 경우 [DSRP Solr 리인덱싱](dsrp.md), URL은 **/services/social/datastore/rdb/reindex**

### MSRP 색인 재지정 예 {#msrp-reindex-example}

```shell
curl -s -u admin:admin -d 'batchSize=10000&path=/content/usergenerated/asi/mongo/' http://localhost:4503/services/social/datastore/mongo/reindex
```

## MSRP 데모 방법 {#how-to-demo-msrp}

데모 또는 개발 환경에 대한 MSRP를 설정하려면 다음을 참조하십시오. [데모용 MongoDB를 설정하는 방법](demo-mongo.md).

## 문제 해결 {#troubleshooting}

### UGC가 MongoDB에 표시되지 않음 {#ugc-not-visible-in-mongodb}

저장소 옵션의 구성을 확인하여 MSRP가 기본 공급자로 구성되었는지 확인하십시오. 기본적으로 저장소 리소스 공급자는 JSRP입니다.

모든 작성자 및 게시 AEM 인스턴스에서 [스토리지 구성 콘솔](srp-config.md) 또는 AEM 저장소를 확인합니다.

* JCR에서, [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)

   * 다음을 포함하지 않음 [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) 즉, 스토리지 공급자가 JSRP입니다.
   * srpc 노드가 존재하고 노드를 포함하는 경우 [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration), defaultconfiguration 의 속성은 MSRP를 기본 공급자로 정의해야 합니다.

### 업그레이드 후 UGC가 사라짐 {#ugc-disappears-after-upgrade}

기존 AEM Communities 6.0 사이트에서 업그레이드할 경우, 기존 UGC는 다음에 필요한 구조에 맞게 변환해야 합니다. [SRP](srp.md) AEM Communities 6.3으로 업그레이드한 후 API.

GitHub에는 이러한 목적으로 사용할 수 있는 오픈 소스 도구가 있습니다.

* [AEM Communities UGC 마이그레이션 도구](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

이전 버전의 AEM 소셜 커뮤니티에서 UGC를 내보내 AEM Communities 6.1 이상으로 가져오도록 마이그레이션 도구를 사용자 지정할 수 있습니다.

### 오류 - 정의되지 않은 필드 provider_id {#error-undefined-field-provider-id}

다음 오류가 로그에 표시되면 Solr 스키마 파일이 제대로 구성되지 않은 것입니다.

#### JsonMappingException: 정의되지 않은 필드 provider_id {#jsonmappingexception-undefined-field-provider-id}

```xml
Caused by: com.fasterxml.jackson.databind.JsonMappingException: undefined field provider_id
at com.fasterxml.jackson.databind.ser.DefaultSerializerProvider.serializeValue(DefaultSerializerProvider.java:129)
at com.fasterxml.jackson.databind.ObjectMapper.writeValue(ObjectMapper.java:1819)
at com.adobe.cq.social.scf.core.BaseSocialComponent.toJSONString(BaseSocialComponent.java:196)
... 124 common frames omitted
```

다음 지침에 따라 오류를 해결하려면 다음을 수행합니다 [표준 MLS 설치](solr.md#installing-standard-mls), 다음을 확인합니다.

* XML 구성 파일이 올바른 Solr 위치에 복사되었습니다.
* 새 구성 파일이 기존 구성 파일을 대체한 후 Solr이 다시 시작되었습니다.

### MongoDB에 대한 보안 연결 실패 {#secure-connection-to-mongodb-fails}

클래스 정의가 누락되어 MongoDB 서버에 보안 연결을 시도하지 못한 경우 MongoDB 드라이버 번들을 업데이트해야 합니다. `mongo-java-driver`공용 maven 저장소에서 사용할 수 있습니다.

1. 에서 드라이버 다운로드 [https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar](https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar) (버전 2.13.2 이상).
1. AEM 인스턴스의 &quot;crx-quickstart/install&quot; 폴더에 번들을 복사합니다.
1. AEM 인스턴스를 다시 시작합니다.

## 리소스 {#resources}

* [MongoDB와 AEM](../../help/sites-deploying/aem-with-mongodb.md)
* [MongoDB 설명서](https://docs.mongodb.org/)
