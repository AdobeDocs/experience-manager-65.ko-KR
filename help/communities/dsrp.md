---
title: DSRP - 관계형 데이터베이스 저장소 리소스 제공자
description: 관계형 데이터베이스를 공통 저장소로 사용하도록 AEM Communities 설정
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 15b3a594-efde-4702-9233-232ba1c7e5b0
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---

# DSRP - 관계형 데이터베이스 저장소 리소스 제공자 {#dsrp-relational-database-storage-resource-provider}

## DSRP 정보 {#about-dsrp}

AEM Communities이 관계형 데이터베이스를 공통 저장소로 사용하도록 구성된 경우 UGC(사용자 생성 컨텐츠)는 동기화나 복제 없이 모든 작성자 및 게시 인스턴스에서 액세스할 수 있습니다.

[SRP 옵션의 특성](working-with-srp.md#characteristics-of-srp-options) 및 [권장 토폴로지](topologies.md)도 참조하세요.

## 요구 사항 {#requirements}

* 관계형 데이터베이스인 [MySQL](#mysql-configuration).
* 검색 플랫폼인 [Apache Solr](#solr-configuration).

>[!NOTE]
>
>이제 기본 저장소 구성이 `etc` 경로(`/etc/socialconfig/srpc/defaultconfiguration`) 대신 conf 경로(`/conf/global/settings/community/srpc/defaultconfiguration`)에 저장됩니다. [마이그레이션 단계](#zerodt-migration-steps)를 따라 defaultsrp가 예상대로 작동하도록 하는 것이 좋습니다.

## 관계형 데이터베이스 구성 {#relational-database-configuration}

### MySQL 구성 {#mysql-configuration}

MySQL 설치는 서로 다른 데이터베이스(스키마) 이름과 서로 다른 연결(server:port)을 사용하여 동일한 연결 풀 내의 지원 기능과 DSRP(공용 저장소) 간에 공유할 수 있습니다.

설치 및 구성에 대한 자세한 내용은 [DSRP에 대한 MySQL 구성](dsrp-mysql.md)을 참조하십시오.

### Solr 구성 {#solr-configuration}

Solr 설치는 다른 컬렉션을 사용하여 노드 저장소(Oak)와 공통 저장소(SRP) 간에 공유할 수 있습니다.

Oak 및 SRP 컬렉션을 모두 집중적으로 사용하는 경우 성능상의 이유로 두 번째 Solr을 설치할 수 있습니다.

프로덕션 환경의 경우 SolrCloud 모드는 독립 실행형 모드(단일 로컬 Solr 설정)보다 향상된 성능을 제공합니다.

설치 및 구성에 대한 자세한 내용은 [SRP에 대한 Solr 구성](solr.md)을 참조하십시오.

### DSRP 선택 {#select-dsrp}

[저장소 구성 콘솔](srp-config.md)에서 사용할 SRP 구현을 식별하는 기본 저장소 구성을 선택할 수 있습니다.

작성자의 경우 스토리지 구성 콘솔에 액세스

* 관리자 권한으로 로그인
* **기본 메뉴**&#x200B;에서

   * 왼쪽 창에서 **[!UICONTROL 도구]** 선택
   * **[!UICONTROL 커뮤니티]** 선택
   * **[!UICONTROL 저장소 구성]** 선택

      * 예를 들어 결과 위치는 [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)입니다.

     >[!NOTE]
     >
     >이제 기본 저장소 구성이 conf 경로(`/conf/global/settings/community/srpc/defaultconfiguration`)에 저장됩니다.      `etc` 경로(`/etc/socialconfig/srpc/defaultconfiguration`) 대신 [마이그레이션 단계](#zerodt-migration-steps)를 따라 defaultsrp가 예상대로 작동하도록 하는 것이 좋습니다.

  ![dsrp-config](assets/dsrp-config.png)

* **[!UICONTROL 데이터베이스 저장소 리소스 공급자(DSRP) 선택]**
* **데이터베이스 구성**

   * **[!UICONTROL JDBC 데이터 원본 이름]**

     MySQL 연결에 지정된 이름은 [JDBC OSGi 구성](dsrp-mysql.md#configurejdbcconnections)에 입력한 이름과 같아야 합니다.

     *기본값*: 커뮤니티

   * **[!UICONTROL 데이터베이스 이름]**

     [init_schema.sql](dsrp-mysql.md#obtain-the-sql-script) 스크립트에서 스키마에 지정한 이름

     *기본값*: 커뮤니티

* **SolrConfiguration**

   * **[Zookeeper](https://solr.apache.org/guide/6_6/using-zookeeper-to-manage-configuration-files.html) Host**

     내부 ZooKeeper를 사용하여 Solr을 실행하는 경우 이 값을 비워 둡니다. 또는 외부 ZooKeeper를 사용하여 [SolrCloud 모드](solr.md#solrcloud-mode)에서 실행할 때 이 값을 ZooKeeper의 URI(예: *my.server.com:80*)로 설정하십시오.

     *기본값*: *&lt;비어 있음>*

   * **[!UICONTROL Solr URL]**

     *기본값*: https://127.0.0.1:8983/solr/

   * **[!UICONTROL Solr 컬렉션]**

     *기본값*: collection1

* **[!UICONTROL 제출]**&#x200B;을 선택합니다.

### defaultsrp에 대한 다운타임 없는 마이그레이션 단계 {#zerodt-migration-steps}

defaultsrp 페이지 [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)이(가) 예상대로 작동하는지 확인하려면 다음 단계를 수행하십시오.

1. 시스템 구성이 jsrp(기본값)로 대체되도록 경로 이름을 `/etc/socialconfig`에서 `/etc/socialconfig_old`(으)로 바꾸십시오.
1. jsrp가 구성된 defaultsrp 페이지 [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)(으)로 이동합니다. **[!UICONTROL 제출]** 단추를 클릭하여 `/conf/global/settings/community/srpc`에 새 기본 구성 노드를 만듭니다.
1. 만든 기본 구성 `/conf/global/settings/community/srpc/defaultconfiguration`을(를) 삭제합니다.
1. 이전 단계에서 삭제된 노드(`/conf/global/settings/community/srpc/defaultconfiguration`) 대신 이전 구성 `/etc/socialconfig_old/srpc/defaultconfiguration`을(를) 복사합니다.
1. 이전 `etc` 노드 `/etc/socialconfig_old`을(를) 삭제합니다.

## 구성 게시 {#publishing-the-configuration}

DSRP는 모든 작성자 및 게시 인스턴스에서 공통 저장소로 식별되어야 합니다.

게시 환경에서 동일한 구성을 사용할 수 있도록 하려면 다음을 수행하십시오.

* 작성자:

   * 메인 메뉴에서 **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 복제]**(으)로 이동
   * **[!UICONTROL 트리 활성화]**&#x200B;를 두 번 클릭
   * **시작 경로**:

      * `/etc/socialconfig/srpc/`(으)로 이동

   * `Only Modified`이(가) 선택되어 있지 않은지 확인하십시오.
   * **[!UICONTROL 활성화]**&#x200B;를 선택합니다.

## 사용자 데이터 관리 {#managing-user-data}

게시 환경에 종종 입력된 *사용자*, *사용자 프로필* 및 *사용자 그룹*&#x200B;에 대한 자세한 내용을 보려면 다음을 방문하십시오.

* [사용자 동기화](sync.md)
* [사용자 및 사용자 그룹 관리](users.md)

## DSRP용 Solr 리인덱싱 {#reindexing-solr-for-dsrp}

DSRP Solr을 다시 인덱싱하려면 [MSRP 다시 인덱싱](msrp.md#msrp-reindex-tool)에 대한 설명서를 따르지만 DSRP를 다시 인덱싱할 때는 이 URL을 대신 사용하십시오. **/services/social/datastore/rdb/reindex**

예를 들어 DSRP를 다시 색인화하는 curl 명령은 다음과 같습니다.

```shell
curl -u admin:password -X POST -F path=/ https://host:port/services/social/datastore/rdb/reindex
```
