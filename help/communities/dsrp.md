---
title: DSRP - 관계형 데이터베이스 저장소 리소스 공급자
seo-title: DSRP - 관계형 데이터베이스 저장소 리소스 공급자
description: 관계형 데이터베이스를 공용 스토어로 사용하도록 AEM Communities 설정
seo-description: 관계형 데이터베이스를 공용 스토어로 사용하도록 AEM Communities 설정
uuid: f364e7da-ee54-4ab2-a630-7ec9239005ac
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d23acb18-6761-4290-9e7a-a434582791bd
translation-type: tm+mt
source-git-commit: 29f150215052d61c1e20d25b0c095ea6582e26f7
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 3%

---


# DSRP - 관계형 데이터베이스 저장소 리소스 공급자 {#dsrp-relational-database-storage-resource-provider}

## DSRP 정보 {#about-dsrp}

관계형 데이터베이스를 공통 스토어로 사용하도록 AEM Communities이 구성된 경우 동기화나 복제 없이도 모든 작성자 및 게시 인스턴스에서 UGC(사용자 생성 컨텐츠)에 액세스할 수 있습니다.

SRP 옵션 [및 권장 토폴로지](working-with-srp.md#characteristics-of-srp-options) 의 [특성을 참조하십시오](topologies.md).

## 요구 사항 {#requirements}

* [MySQL](#mysql-configuration), 관계형 데이터베이스입니다.
* [Apache Solr](#solr-configuration), 검색 플랫폼

>[!NOTE]
>
>기본 스토리지 구성은 이제 etc path(경로`/conf/global/settings/community/srpc/defaultconfiguration`) 대신 conf 경로(`/etc/socialconfig/srpc/defaultconfiguration`)에 저장됩니다. 예상대로 기본 [srp를](#zerodt-migration-steps) 작동하도록 하려면 마이그레이션 단계를 따라야 합니다.


## 관계형 데이터베이스 구성 {#relational-database-configuration}

### MySQL 구성 {#mysql-configuration}

다른 데이터베이스(스키마) 이름과 다른 연결(server:port)을 사용하여 동일한 연결 풀 내의 활성 기능과 공용 저장소(DSRP) 간에 MySQL 설치를 공유할 수 있습니다.

설치 및 구성 세부 사항은 DSRP용 [MySQL 구성을 참조하십시오](dsrp-mysql.md).

### Solr 구성 {#solr-configuration}

다른 컬렉션을 사용하여 노드 스토어(Oak)와 공용 스토어(SRP) 간에 솔루션 설치를 공유할 수 있습니다.

Oak 및 SRP 컬렉션이 모두 집중적으로 사용되는 경우 성능상의 이유로 두 번째 솔러를 설치할 수 있습니다.

프로덕션 환경의 경우, SolrCloud 모드는 독립형 모드(단일 로컬 솔루션 설정)에 비해 향상된 성능을 제공합니다.

설치 및 구성 세부 사항은 SRP용 [솔루션 구성을 참조하십시오](solr.md).

### DSRP 선택 {#select-dsrp}

스토리지 [구성 콘솔에서는](srp-config.md) 사용할 SRP 구현을 식별하는 기본 스토리지 구성을 선택할 수 있습니다.

작성자가 스토리지 구성 콘솔에 액세스하려면

* 관리자 권한으로 로그인
* 주 **메뉴에서**

   * 왼쪽 창에서 **[!UICONTROL 도구]** 선택
   * 커뮤니티 **[!UICONTROL 선택]**
   * 스토리지 **[!UICONTROL 구성 선택]**

      * 예를 들어 결과 위치는 다음과 같습니다. [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)
      >[!NOTE]
      >
      >기본 스토리지 구성은 이제 etc path(경로`/conf/global/settings/community/srpc/defaultconfiguration`) 대신 conf 경로(`/etc/socialconfig/srpc/defaultconfiguration`)에 저장됩니다. 예상대로 기본 [srp를](#zerodt-migration-steps) 작동하도록 하려면 마이그레이션 단계를 따라야 합니다.
   ![chlimage_1-128](assets/chlimage_1-128.png)

* Select **[!UICONTROL Database Storage Resource Provider (DSRP)]**
* **데이터베이스 구성**

   * **[!UICONTROL JDBC 데이터 소스 이름]**

      MySQL 연결에 지정된 이름은 [JDBC OSGi 구성에 입력한 이름과 동일해야 합니다.](dsrp-mysql.md#configurejdbcconnections)

      *기본값*: 커뮤니티

   * **[!UICONTROL 데이터베이스 이름]**

      init_schema.sql [](dsrp-mysql.md#obtain-the-sql-script) 스크립트에서 스키마에 지정된 이름

      *기본값*: 커뮤니티

* **SolrConfiguration**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Zookeeper 호스트&#x200B;**

      내부 ZooKeeper를 사용하여 Solr을 실행하는 경우 이 값을 비워 둡니다. 그렇지 않은 경우 외부 [ZooKeeper와 함께 SolrCloud 모드에서](solr.md#solrcloud-mode) 실행할 때 *my.server.com:80과 같은 ZooKeeper의 URI로 이 값을 설정합니다*

      *기본값*: *&lt;공백>*

   * **[!UICONTROL Solr URL]**

      *기본값*: https://127.0.0.1:8983/solr/

   * **[!UICONTROL Solr 컬렉션]**

      *기본값*: collection1

* **[!UICONTROL 제출]**&#x200B;을 선택합니다.

### 기본 srp에 대한 다운타임 마이그레이션 단계 없음 {#zerodt-migration-steps}

다음 단계에 따라 기본 srp 페이지 http://localhost:4502/communities/admin/defaultsrp이 예상대로 [작동하는지](http://localhost:4502/communities/admin/defaultsrp) 확인합니다.

1. 시스템 구성 `/etc/socialconfig` 이 jsrp(기본값)로 `/etc/socialconfig_old`돌아가도록 경로 이름을 다음으로 변경합니다.
1. http://localhost:4502/communities/admin/defaultsrp으로 [이동하여](http://localhost:4502/communities/admin/defaultsrp)jsrp가 구성되어 있습니다. 새 기본 구성 노드가 **[!UICONTROL 작성되도록 전송]** 단추를 클릭합니다 `/conf/global/settings/community/srpc`.
1. 생성된 기본 구성을 삭제합니다 `/conf/global/settings/community/srpc/defaultconfiguration`.
1. 이전 단계 `/etc/socialconfig_old/srpc/defaultconfiguration` 에서 삭제된 노드(`/conf/global/settings/community/srpc/defaultconfiguration`)를 대신하여 이전 구성을 복사합니다.
1. 이전 etc 노드를 삭제합니다 `/etc/socialconfig_old`.

## 구성 게시 {#publishing-the-configuration}

DSRP는 모든 작성자 및 게시 인스턴스에 있는 공통 스토어로 식별되어야 합니다.

게시 환경에서 동일한 구성을 사용할 수 있도록 하려면:

* 작성자:

   * 주 메뉴에서 **[!UICONTROL 도구]** > 작업 **[!UICONTROL >]** 복제 **[!UICONTROL 로이동합니다.]**
   * **[!UICONTROL 트리 활성화]**&#x200B;를 두 번 클릭합니다
   * **시작 경로**:

      * 검색 대상 `/etc/socialconfig/srpc/`
   * 선택하지 `Only Modified` 않았는지 확인합니다.
   * 활성화를 **[!UICONTROL 선택합니다]**.


## 사용자 데이터 관리 {#managing-user-data}

게시 환경에 자주 입력되는 *사용자*, *사용자 프로필* 및 *사용자 그룹에*&#x200B;대한 자세한 내용은 다음을 참조하십시오.

* [사용자 동기화](sync.md)
* [사용자 및 사용자 그룹 관리](users.md)

## DSRP용 색인 재지정 솔루션 {#reindexing-solr-for-dsrp}

DSRP Solr를 다시 색인화하려면 MSRP를 [다시 색인화하려면 설명서를 따르되](msrp.md#msrp-reindex-tool), DSRP에 대해 다시 색인화할 때는 다음 URL을 대신 사용하십시오. **/services/social/datastore/rdb/reindex**

예를 들어 DSRP를 다시 색인화하는 말림 명령은 다음과 같습니다.

```shell
curl -u admin:password -X POST -F path=/ https://host:port/services/social/datastore/rdb/reindex
```

