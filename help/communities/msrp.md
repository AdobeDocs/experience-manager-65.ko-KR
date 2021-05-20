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
role: Administrator
exl-id: 799d5ae1-caac-4c92-8835-696ad25de553
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 1%

---

# MSRP - MongoDB 저장소 리소스 공급자 {#msrp-mongodb-storage-resource-provider}

## MSRP {#about-msrp} 정보

AEM Communities이 MSRP를 일반 스토어로 사용하도록 구성된 경우, 동기화 또는 복제 없이 모든 작성자 및 게시 인스턴스에서 사용자 생성 컨텐츠(UGC)에 액세스할 수 있습니다.

[SRP 옵션](working-with-srp.md#characteristics-of-srp-options) 및 [권장 토폴로지](topologies.md)도 참조하십시오.

## 요구 사항 {#requirements}

* [MongoDB](https://www.mongodb.org/):

   * 버전 2.6 이상
   * 관리 또는 공유를 구성할 필요가 없음
   * [복제본 세트](#mongoreplicaset)를 사용하는 것이 좋습니다.
   * AEM과 동일한 호스트에서 실행하거나 원격으로 실행할 수 있음

* [Apache 솔루션](https://lucene.apache.org/solr/):

   * 솔루션 버전 7.0
   * 솔루션이 Java 1.7 이상 필요
   * 서비스가 필요하지 않습니다
   * 실행 모드 선택:
      * 독립형 모드
      * [SolrCloud 모드](solr.md#solrcloud-mode) (프로덕션 환경에 권장)
   * 다국어 검색(MLS) 선택:
      * [표준 MLS 설치](solr.md#installing-standard-mls)
      * [고급 MLS 설치](solr.md#installing-advanced-mls)

## MongoDB 구성 {#mongodb-configuration}

### MSRP {#select-msrp} 선택

[스토리지 구성 콘솔](srp-config.md)에서는 사용할 SRP 구현을 식별하는 기본 스토리지 구성을 선택할 수 있습니다.

작성자가 스토리지 구성 콘솔에 액세스하려면

* 전역 탐색에서 **[!UICONTROL 도구]** > **[!UICONTROL 커뮤니티]** > **[!UICONTROL 저장소 구성]**&#x200B;을 선택합니다.

![msrp](assets/msrp.png)

* **[!UICONTROL MongoDB Storage Resource Provider(MSRP)]** 선택
* **[!UICONTROL mongoDB 구성]**

   * **[!UICONTROL mongoDB URI]**

      *기본값*:mongodb://localhost/?maxPoolSize=10&amp;waitQueueMultiple=5&amp;readPreference=secondaryPreferred

   * **[!UICONTROL mongoDB 데이터베이스]**

      *기본값*:커뮤니티

   * **[!UICONTROL mongoDB UGC 컬렉션]**

      *기본값*:콘텐츠

   * **[!UICONTROL mongoDB 첨부 파일 컬렉션]**

      *기본값*:첨부 파일

* **[!UICONTROL SolrConfiguration]**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Zookeeper 호스트**

      외부 동물원 Keeper와 함께 [SolrCloud 모드](solr.md#solrcloud-mode)에서 실행할 때 이 값을 *my.server.com:2181*&#x200B;와 같이 동물원은 Keeper에 대해 `HOST:PORT`로 설정합니다.

      동물원 관리자 Ensemble의 경우 *host1:2181,host2:2181*&#x200B;와 같이 쉼표로 구분된 `HOST:PORT` 값을 입력합니다.

      내부 동물원 Keeper를 사용하여 독립 실행형 모드로 Solr을 실행하는 경우 비워 둡니다.
      *기본값*:  *&lt;blank>*

      * **[!UICONTROL 솔루션]**
URL독립형 모드에서 Solr와 통신하는 데 사용되는 URL입니다.
SolrCloud 모드에서 실행 중인 경우 비워 둡니다.

         *기본값*:https://127.0.0.1:8983/solr/

      * **[!UICONTROL Solr]**
CollectionSolr 컬렉션 이름입니다.

         *기본값*:collection1

* **[!UICONTROL 제출]**&#x200B;을 선택합니다

>[!NOTE]
>
>[노드 저장소 또는 데이터(이진)에 사용되는 데이터베이스 이름으로 기본적으로 이름 `communities`인 mongoDB 데이터베이스를 설정하지 않아야 합니다](../../help/sites-deploying/data-store-config.md). AEM 6.5의 [스토리지 요소](../../help/sites-deploying/storage-elements-in-aem-6.md)도 참조하십시오.

### MongoDB 복제본 세트 {#mongodb-replica-set}

운영 환경의 경우 운영-보조 복제 및 자동 페일오버를 구현하는 MongoDB 서버 클러스터인 복제본 세트를 설정하는 것이 좋습니다.

복제본 세트에 대한 자세한 내용은 MongoDB의 [Replication](https://docs.mongodb.org/manual/replication/) 설명서를 참조하십시오.

복제본 세트로 작업하고 응용 프로그램과 MongoDB 인스턴스 간 연결을 정의하는 방법을 알아보려면 MongoDB의 [연결 문자열 URI 형식](https://docs.mongodb.org/manual/reference/connection-string/) 설명서를 참조하십시오.

#### 복제본 세트 {#example-url-for-connecting-to-a-replica-set}에 연결하는 예제 Url

```shell
# Example url for:
# servers "mongoserver1", "mongoserver2", "mongoserver3"
# replica set 'rs0'
# port numbers only necessary if not default port 27017
mongodb://mongoserver1:<mongoport1>,mongoserver2:<mongoport2>,mongoserver3:<mongoport3>/?replicaSet=rs0&maxPoolSize=100&waitQueueMultiple=50&readPreference=secondaryPreferred
```

## Solr 구성 {#solr-configuration}

다른 컬렉션을 사용하여 노드 저장소(Oak)와 공용 저장소(MSRP) 간에 솔루션 설치를 공유할 수 있습니다.

Oak 및 MSRP 컬렉션을 모두 집중적으로 사용하는 경우 성능상의 이유로 두 번째 솔러를 설치할 수 있습니다.

프로덕션 환경의 경우 [SolrCloud 모드](solr.md#solrcloud-mode)는 독립 실행형 모드(단일 로컬 솔루션 설정)보다 향상된 성능을 제공합니다.

구성 세부 사항은 [SRP용 솔루션 구성](solr.md)을 참조하십시오.

### 업그레이드 {#upgrading}

MSRP로 구성된 이전 버전에서 업그레이드하는 경우 다음을 수행해야 합니다.

1. [AEM Communities으로 업그레이드](upgrade.md) 수행
1. 새 Solr 구성 파일 설치
   * [표준 MLS](solr.md#installing-standard-mls)의 경우
   * [고급 MLS](solr.md#installing-advanced-mls)의 경우
1. MSRP 다시 색인화
섹션 [MSRP 재인덱스 도구](#msrp-reindex-tool)를 참조하십시오.

## 구성 {#publishing-the-configuration} 게시

MSRP는 모든 작성자 및 게시 인스턴스에서 공용 스토어로 식별되어야 합니다.

게시 환경에서 동일한 구성을 사용할 수 있도록 하려면 작성자 인스턴스에 로그인하고 다음 단계를 수행합니다.

* 기본 메뉴에서 **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 복제]**&#x200B;로 이동합니다.
* **[!UICONTROL 트리 활성화]** 선택
* **[!UICONTROL 시작 경로]**:
   * `/etc/socialconfig/srpc/` 로 이동합니다.
* **[!UICONTROL 활성화]** 선택

## 사용자 데이터 관리 {#managing-user-data}

게시 환경에 자주 입력되는 *사용자*, *사용자 프로필* 및 *사용자 그룹*&#x200B;에 대한 자세한 내용은 를 참조하십시오.

* [사용자 동기화](sync.md)
* [사용자 및 사용자 그룹 관리](users.md)

## MSRP 재인덱스 도구 {#msrp-reindex-tool}

새 구성 파일을 설치하거나 손상된 Solr 인덱스를 복구할 때 MSRP용 Solr를 다시 인덱싱하기 위한 HTTP 끝점이 있습니다.

이 도구를 사용하는 MongoDB는 MSRP용 *truth*&#x200B;의 소스입니다.MongoDB에서만 백업을 수행할 수 있습니다.

전체 UGC 트리는 *path *data 매개 변수에 의해 지정된 대로 다시 인덱싱되거나 지정된 하위 트리만 재인덱싱될 수 있습니다.

이 도구는 cURL 또는 다른 HTTP 도구를 사용하여 명령줄에서 실행할 수 있습니다.

재색인화할 때 배치당 재색인화되는 UGC 레코드 수를 지정하는 *batchSize *데이터 매개 변수에 의해 제어되는 메모리와 성능 간의 트레이드오프가 있습니다.

합리적인 기본값은 5000입니다.

* 메모리가 문제가 되는 경우 더 작은 숫자를 지정합니다
* 속도가 문제가 되는 경우 더 큰 숫자를 지정하여 속도를 늘리십시오

### cURL 명령을 사용하여 MSRP 재인덱스 도구 실행 {#running-msrp-reindex-tool-using-curl-command}

다음 cURL 명령은 MSRP에 저장된 UGC를 다시 색인화하는 HTTP 요청에 필요한 사항을 보여줍니다.

기본 형식은 다음과 같습니다.

cURL -u *signin* -d *data* *reindex-url*

*signin*  = administrator-id:password 예:admin:admin

*data*  = &quot;batchSize=*size*&amp;path=*path&quot;*

*size*  = 작업당 다시 색인화할 UGC 항목 수 
`/content/usergenerated/asi/mongo/`

*path*  = 다시 색인화할 UGC 트리의 루트 위치

* 모든 UGC를 다시 색인화하려면`asipath`
   `/etc/socialconfig/srpc/defaultconfiguration`
* 인덱스를 일부 UGC로 제한하려면 `asipath` 하위 트리를 지정합니다.

*reindex url*  = SRP의 재색인화를 위한 끝점입니다. 
`http://localhost:4503/services/social/datastore/mongo/reindex`

>[!NOTE]
>
>DSRP Solr](dsrp.md)을(를) 다시 인덱싱하는 경우 URL은 **/services/social/datastore/rdb/reindex**&#x200B;입니다.[

### MSRP 재인덱스 예 {#msrp-reindex-example}

```shell
curl -s -u admin:admin -d 'batchSize=10000&path=/content/usergenerated/asi/mongo/' http://localhost:4503/services/social/datastore/mongo/reindex
```

## MSRP {#how-to-demo-msrp} 데모 방법

데모 또는 개발 환경에 대한 MSRP를 설정하려면 [HowTo Setup MongoDB for Demo](demo-mongo.md)을 참조하십시오.

## 문제 해결 {#troubleshooting}

### MongoDB에 UGC가 표시되지 않음 {#ugc-not-visible-in-mongodb}

저장소 옵션의 구성을 확인하여 MSRP가 기본 공급자로 구성되었는지 확인하십시오. 기본적으로 저장소 리소스 공급자는 JSRP입니다.

모든 작성자 및 게시 AEM 인스턴스에서 [스토리지 구성 콘솔을 다시 방문하거나 AEM 리포지토리를 확인합니다.](srp-config.md)

* JCR에서 [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)인 경우

   * [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) 노드를 포함하지 않습니다. 즉, 스토리지 공급자가 JSRP입니다.
   * srpc 노드가 있고 [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration) 노드가 포함된 경우 기본 구성의 속성은 MSRP를 기본 공급자로 정의해야 합니다.

### {#ugc-disappears-after-upgrade} 업그레이드 후 UGC가 사라짐

기존 AEM Communities 6.0 사이트에서 업그레이드하는 경우 AEM Communities 6.3으로 업그레이드한 후 기존 UGC를 [SRP](srp.md) API에 필요한 구조를 준수하도록 변환해야 합니다.

GitHub에서 사용할 수 있는 개방형 소스 도구는 다음과 같습니다.

* [AEM Communities UGC 마이그레이션 도구](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

AEM Communities 6.1 이상으로 가져오기 위해 이전 버전의 AEM 소셜 커뮤니티에서 UGC를 내보내도록 마이그레이션 도구를 사용자 지정할 수 있습니다.

### 오류 - 정의되지 않은 필드 provider_id {#error-undefined-field-provider-id}

로그에 다음 오류가 표시되면 Solr 스키마 파일이 제대로 구성되지 않은 것입니다.

#### JsonMappingException:정의되지 않은 필드 provider_id {#jsonmappingexception-undefined-field-provider-id}

```xml
Caused by: com.fasterxml.jackson.databind.JsonMappingException: undefined field provider_id
at com.fasterxml.jackson.databind.ser.DefaultSerializerProvider.serializeValue(DefaultSerializerProvider.java:129)
at com.fasterxml.jackson.databind.ObjectMapper.writeValue(ObjectMapper.java:1819)
at com.adobe.cq.social.scf.core.BaseSocialComponent.toJSONString(BaseSocialComponent.java:196)
... 124 common frames omitted
```

오류를 해결하려면 [표준 MLS 설치](solr.md#installing-standard-mls)에 대한 지침을 따르는 경우 다음을 확인합니다.

* XML 구성 파일이 올바른 솔루션 위치에 복사되었습니다.
* 새 구성 파일이 기존 구성 파일을 교체한 후 솔러가 다시 시작되었습니다.

### MongoDB에 대한 보안 연결이 실패함 {#secure-connection-to-mongodb-fails}

클래스 정의가 누락되어 MongoDB 서버에 보안 연결을 시도하지 못한 경우 공용 maven 저장소에서 사용할 수 있는 MongoDB 드라이버 번들 `mongo-java-driver`을 업데이트해야 합니다.

1. [https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar](https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar)(버전 2.13.2 이상)에서 드라이버를 다운로드합니다.
1. AEM 인스턴스에 대한 &quot;crx-quickstart/install&quot; 폴더에 번들을 복사합니다.
1. AEM 인스턴스를 다시 시작합니다.

## 리소스 {#resources}

* [AEM과 MongoDB](../../help/sites-deploying/aem-with-mongodb.md)
* [MongoDB 설명서](https://docs.mongodb.org/)
