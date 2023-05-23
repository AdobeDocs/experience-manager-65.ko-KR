---
title: DSRP - 관계형 데이터베이스 저장소 리소스 제공자
seo-title: DSRP - Relational Database Storage Resource Provider
description: 관계형 데이터베이스를 공통 저장소로 사용하도록 AEM Communities 설정
seo-description: Set up AEM Communities to use a relational database as its common store
uuid: f364e7da-ee54-4ab2-a630-7ec9239005ac
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d23acb18-6761-4290-9e7a-a434582791bd
role: Admin
exl-id: 15b3a594-efde-4702-9233-232ba1c7e5b0
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 2%

---

# DSRP - 관계형 데이터베이스 저장소 리소스 제공자 {#dsrp-relational-database-storage-resource-provider}

## DSRP 정보 {#about-dsrp}

AEM Communities이 관계형 데이터베이스를 공통 저장소로 사용하도록 구성된 경우 UGC(사용자 생성 컨텐츠)는 동기화나 복제 없이 모든 작성자 및 게시 인스턴스에서 액세스할 수 있습니다.

참조: [SRP 옵션의 특성](working-with-srp.md#characteristics-of-srp-options) 및 [권장 토폴로지](topologies.md).

## 요구 사항 {#requirements}

* [MySQL](#mysql-configuration)관계형 데이터베이스입니다.
* [Apache Solr](#solr-configuration)검색 플랫폼입니다.

>[!NOTE]
>
>이제 기본 스토리지 구성이 conf path(`/conf/global/settings/community/srpc/defaultconfiguration`etc 경로 ( ) 대신`/etc/socialconfig/srpc/defaultconfiguration`). 다음을 따르는 것이 좋습니다. [마이그레이션 단계](#zerodt-migration-steps) defaultsrp가 예상대로 작동하도록 합니다.

## 관계형 데이터베이스 구성 {#relational-database-configuration}

### MySQL 구성 {#mysql-configuration}

MySQL 설치는 서로 다른 데이터베이스(스키마) 이름과 서로 다른 연결(server:port)을 사용하여 동일한 연결 풀 내의 지원 기능과 DSRP(공용 저장소) 간에 공유할 수 있습니다.

설치 및 구성에 대한 자세한 내용은 [DSRP에 대한 MySQL 구성](dsrp-mysql.md).

### Solr 구성 {#solr-configuration}

Solr 설치는 다른 컬렉션을 사용하여 노드 저장소(Oak)와 공통 저장소(SRP) 간에 공유할 수 있습니다.

Oak 컬렉션과 SRP 컬렉션을 모두 집중적으로 사용하는 경우 성능상의 이유로 두 번째 Solr을 설치할 수 있습니다.

프로덕션 환경의 경우 SolrCloud 모드는 독립 실행형 모드(단일 로컬 Solr 설정)보다 향상된 성능을 제공합니다.

설치 및 구성에 대한 자세한 내용은 [SRP에 대한 Solr 구성](solr.md).

### DSRP 선택 {#select-dsrp}

다음 [스토리지 구성 콘솔](srp-config.md) 에서는 사용할 SRP 구현을 식별하는 기본 스토리지 구성을 선택할 수 있습니다.

작성자의 경우 스토리지 구성 콘솔에 액세스

* 관리자 권한으로 로그인
* 다음에서 **메인 메뉴**

   * 선택 **[!UICONTROL 도구]** (왼쪽 창에서)
   * 선택 **[!UICONTROL 커뮤니티]**
   * 선택 **[!UICONTROL 스토리지 구성]**

      * 예를 들어 결과 위치는 다음과 같습니다. [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)
      >[!NOTE]
      >
      >이제 기본 스토리지 구성이 conf path(`/conf/global/settings/community/srpc/defaultconfiguration`etc 경로 ( ) 대신`/etc/socialconfig/srpc/defaultconfiguration`). 다음을 따르는 것이 좋습니다. [마이그레이션 단계](#zerodt-migration-steps) defaultsrp가 예상대로 작동하도록 합니다.
   ![dsrp-config](assets/dsrp-config.png)

* 선택 **[!UICONTROL 데이터베이스 저장소 리소스 제공자(DSRP)]**
* **데이터베이스 구성**

   * **[!UICONTROL JDBC 데이터 소스 이름]**

      MySQL 연결에 지정된 이름은 입력한 것과 동일해야 합니다. [JDBC OSGi 구성](dsrp-mysql.md#configurejdbcconnections)

      *기본값*: 커뮤니티

   * **[!UICONTROL 데이터베이스 이름]**

      의 스키마에 지정된 이름 [init_schema.sql](dsrp-mysql.md#obtain-the-sql-script) script

      *기본값*: 커뮤니티

* **SolrConfiguration**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Zookeeper 호스트**

      내부 ZooKeeper를 사용하여 Solr을 실행하는 경우 이 값을 비워 둡니다. Else, 실행 시 [SolrCloud 모드](solr.md#solrcloud-mode) 외부 ZooKeeper를 사용하여 이 값을 ZooKeeper의 URI로 설정합니다. 예: *my.server.com:80*

      *기본값*: *&lt;blank>*

   * **[!UICONTROL Solr URL]**

      *기본값*: https://127.0.0.1:8983/solr/

   * **[!UICONTROL Solr 컬렉션]**

      *기본값*: collection1

* 선택 **[!UICONTROL 제출]**.

### defaultsrp에 대한 다운타임 없는 마이그레이션 단계 {#zerodt-migration-steps}

다음 단계에 따라 defaultsrp 페이지가 [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp) 예상대로 작동합니다.

1. 경로 이름 바꾸기 `/etc/socialconfig` 끝 `/etc/socialconfig_old`시스템 구성이 jsrp(기본값)로 대체됩니다.
1. defaultsrp 페이지로 이동 [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp): 여기서 jsrp는 구성됩니다. 다음을 클릭합니다. **[!UICONTROL 제출]** 새 기본 구성 노드가 다음 위치에 생성되도록 하는 버튼 `/conf/global/settings/community/srpc`.
1. 생성된 기본 구성 삭제 `/conf/global/settings/community/srpc/defaultconfiguration`.
1. 이전 구성 복사 `/etc/socialconfig_old/srpc/defaultconfiguration` 삭제된 노드 대신(`/conf/global/settings/community/srpc/defaultconfiguration`)을 클릭하여 제품에서 사용할 수 있습니다.
1. 이전 etc 노드 삭제 `/etc/socialconfig_old`.

## 구성 게시 {#publishing-the-configuration}

DSRP는 모든 작성자 및 게시 인스턴스에서 공통 저장소로 식별되어야 합니다.

게시 환경에서 동일한 구성을 사용할 수 있도록 하려면 다음을 수행하십시오.

* 작성자:

   * 메인 메뉴에서 다음으로 이동 **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 복제]**
   * 두 번 클릭 **[!UICONTROL 트리 활성화]**
   * **시작 경로**:

      * 다음으로 이동 `/etc/socialconfig/srpc/`
   * 확인 `Only Modified` 이(가) 선택되지 않았습니다.
   * 선택 **[!UICONTROL 활성화]**.


## 사용자 데이터 관리 {#managing-user-data}

에 관한 정보를 위하여 *사용자*, *사용자 프로필* 및 *사용자 그룹*, 종종 게시 환경에 입력됨, 다음을 방문하십시오.

* [사용자 동기화](sync.md)
* [사용자 및 사용자 그룹 관리](users.md)

## DSRP용 Solr 리인덱싱 {#reindexing-solr-for-dsrp}

DSRP Solr을 다시 색인화하려면 다음 설명서를 따르십시오. [MSRP 리인덱싱](msrp.md#msrp-reindex-tool), 그러나 DSRP에 대해 리인덱싱하는 경우 이 URL을 대신 사용하십시오. **/services/social/datastore/rdb/reindex**

예를 들어 DSRP를 다시 색인화하는 curl 명령은 다음과 같습니다.

```shell
curl -u admin:password -X POST -F path=/ https://host:port/services/social/datastore/rdb/reindex
```
