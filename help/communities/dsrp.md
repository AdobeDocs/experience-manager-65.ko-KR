---
title: DSRP - 관계형 데이터베이스 저장소 리소스 공급자
seo-title: DSRP - 관계형 데이터베이스 저장소 리소스 공급자
description: 관계형 데이터베이스를 공통 스토어로 사용하도록 AEM Communities 설정
seo-description: 관계형 데이터베이스를 공통 스토어로 사용하도록 AEM Communities 설정
uuid: f364e7da-ee54-4ab2-a630-7ec9239005ac
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d23acb18-6761-4290-9e7a-a434582791bd
translation-type: tm+mt
source-git-commit: b7c790681034e9950aa43738310f7af8b1dd0085

---


# DSRP - 관계형 데이터베이스 저장소 리소스 공급자 {#dsrp-relational-database-storage-resource-provider}

## DSRP 정보 {#about-dsrp}

AEM Communities가 관계형 데이터베이스를 공통 저장소로 사용하도록 구성된 경우 동기화 또는 복제 없이도 모든 작성자 및 게시 인스턴스에서 사용자 생성 콘텐츠(UGC)에 액세스할 수 있습니다.

SRP [옵션 및 권장 토폴로지의](working-with-srp.md#characteristics-of-srp-options) 특성을 [참조하십시오](topologies.md).

## 요구 사항 {#requirements}

* [MySQL](#mysql-configuration), 관계형 데이터베이스
* [검색 플랫폼](#solr-configuration)Apache Solr

>[!NOTE]
>
>기본 스토리지 구성은 이제 etc 경로 (`/conf/global/settings/community/srpc/defaultconfiguration`) 대신 conf 경로(`/etc/socialconfig/srpc/defaultconfiguration`)에 저장됩니다. 기본 [트립 작업을 예상대로 수행하려면 마이그레이션 단계를](#zerodt-migration-steps) 따라야 합니다.


## 관계형 데이터베이스 구성 {#relational-database-configuration}

### MySQL 구성 {#mysql-configuration}

MySQL 설치는 다른 데이터베이스(스키마) 이름과 다른 연결(server:port)을 사용하여 동일한 연결 풀 내의 활성 기능과 공용 저장소(DSRP) 간에 공유할 수 있습니다.

설치 및 구성 세부 정보는 DSRP [용 MySQL 구성을 참조하십시오](dsrp-mysql.md).

### Solr 구성 {#solr-configuration}

다른 컬렉션을 사용하여 노드 스토어(Oak)와 공용 스토어(SRP) 간에 솔루션 설치를 공유할 수 있습니다.

Oak 컬렉션과 SRP 컬렉션이 모두 집중적으로 사용되는 경우 성능상의 이유로 두 번째 Solr를 설치할 수 있습니다.

프로덕션 환경의 경우 SolrCloud 모드는 독립형 모드(단일 로컬 솔루션 설정)보다 향상된 성능을 제공합니다.

설치 및 구성 세부 정보는 SRP [용 솔루션 구성을 참조하십시오](solr.md).

### DSRP 선택 {#select-dsrp}

스토리지 [구성 콘솔을](srp-config.md) 사용하면 사용할 SRP 구현을 식별하는 기본 스토리지 구성을 선택할 수 있습니다.

작성자가 스토리지 구성 콘솔에 액세스하려면

* 관리자 권한으로 로그인
* 기본 **메뉴에서**

   * 왼쪽 **[!UICONTROL 창에서]** 도구 선택
   * 커뮤니티 **[!UICONTROL 선택]**
   * 스토리지 **[!UICONTROL 구성 선택]**

      * 예를 들어 결과 위치는 다음과 같습니다. [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)
      >[!NOTE]
      >
      >기본 스토리지 구성은 이제 etc 경로 (`/conf/global/settings/community/srpc/defaultconfiguration`) 대신 conf 경로(`/etc/socialconfig/srpc/defaultconfiguration`)에 저장됩니다. 기본 [트립 작업을 예상대로 수행하려면 마이그레이션 단계를](#zerodt-migration-steps) 따라야 합니다.

![chlimage_1-128](assets/chlimage_1-128.png)

* Select **[!UICONTROL Database Storage Resource Provider (DSRP)]**
* **데이터베이스 구성**

   * **[!UICONTROL JDBC 데이터 소스 이름]**

      MySQL 연결에 지정된 이름은 JDBC OSGi 구성에 입력한 이름과 [같아야 합니다.](dsrp-mysql.md#configurejdbcconnections)

      *기본값*:커뮤니티

   * **[!UICONTROL 데이터베이스 이름]**

      [init_schema.sql](dsrp-mysql.md#obtain-the-sql-script) 스크립트의 스키마에 지정된 이름

      *기본값*:커뮤니티

* **SolrConfiguration**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Zookeeper 호스트&#x200B;**

      내부 ZooKeeper를 사용하여 Solr를 실행하는 경우 이 값을 비워 둡니다. 또는 외부 ZooKeeper [를 사용하여 SolrCloud 모드에서](solr.md#solrcloud-mode) 실행할 때 *my.server.com:80과 같이 ZooKeeper의 URI로 이 값을 설정합니다*

      *기본값*: *&lt;공백>*

   * **[!UICONTROL Solr URL]**

      *기본값*:https://127.0.0.1:8983/solr/

   * **[!UICONTROL Solr 컬렉션]**

      *기본값*:collection1

* **[!UICONTROL 제출]**&#x200B;을 선택합니다.

### 기본 SRP에 대한 다운타임 제거 단계 {#zerodt-migration-steps}

다음 단계에 따라 기본 srp 페이지 http://localhost:4502/communities/admin/defaultsrp [이](http://localhost:4502/communities/admin/defaultsrp) 예상대로 작동하는지 확인합니다.

1. 시스템 구성이 다시 jsrp(기본값) `/etc/socialconfig` 로 돌아갈 수 `/etc/socialconfig_old`있도록 경로 이름을 다음으로 변경합니다.
1. 기본 SRP 페이지 http://localhost:4502/communities/admin/defaultsrp [로 이동합니다](http://localhost:4502/communities/admin/defaultsrp). 여기서 jsrp는 구성됩니다. 새 기본 구성 노드가 에 생성되도록 **[!UICONTROL 전송]** 단추를 클릭합니다 `/conf/global/settings/community/srpc`.
1. 생성된 기본 구성을 `/conf/global/settings/community/srpc/defaultconfiguration`삭제합니다.
1. 이전 단계에서 삭제된 노드( `/etc/socialconfig_old/srpc/defaultconfiguration``/conf/global/settings/community/srpc/defaultconfiguration`) 대신 이전 구성을 복사합니다.
1. 이전 etc 노드를 `/etc/socialconfig_old`삭제합니다.

## 구성 게시 {#publishing-the-configuration}

DSRP는 모든 작성자 및 게시 인스턴스에서 공용 스토어로 식별되어야 합니다.

게시 환경에서 동일한 구성을 사용할 수 있도록 하려면:

* 작성자:

   * 주 메뉴에서 도구 > **[!UICONTROL 작업 > 복제로 이동합니다.]**
   * **트리 활성화&#x200B;**를 두 번 클릭합니다
   * **시작 경로:**

      * 탐색 `/etc/socialconfig/srpc/`
   * 선택하지 `Only Modified` 않았는지 확인합니다.
   * 활성화 **[!UICONTROL 선택]**


## 사용자 데이터 관리 {#managing-user-data}

게시 환경에 자주 입력되는 *사용자*, *사용자 프로필* 및 *사용자 그룹에*&#x200B;대한 자세한 내용은

* [사용자 동기화](sync.md)
* [사용자 및 사용자 그룹 관리](users.md)

## DSRP용 색인 재지정 솔루션 {#reindexing-solr-for-dsrp}

DSRP Solr를 다시 색인화하려면 MSRP [를 다시 색인화할](msrp.md#msrp-reindex-tool)수 있는 문서를 따르지만 DSRP에 대해 다시 색인화할 때는 이 URL을 대신 사용하십시오. **/services/social/datastore/rdb/reindex**

예를 들어 DSRP를 다시 색인화하는 curl 명령은 다음과 같습니다.

```shell
curl -u admin:password -X POST -F path=/ https://host:port/services/social/datastore/rdb/reindex
```

