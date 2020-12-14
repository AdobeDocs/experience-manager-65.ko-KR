---
title: DSRP - 관계형 데이터베이스 저장소 리소스 공급자
seo-title: DSRP - 관계형 데이터베이스 저장소 리소스 공급자
description: 관계형 데이터베이스를 공용 저장소로 사용하도록 AEM Communities 설정
seo-description: 관계형 데이터베이스를 공용 저장소로 사용하도록 AEM Communities 설정
uuid: f364e7da-ee54-4ab2-a630-7ec9239005ac
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d23acb18-6761-4290-9e7a-a434582791bd
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 3%

---


# DSRP - 관계형 데이터베이스 저장소 리소스 공급자 {#dsrp-relational-database-storage-resource-provider}

## DSRP {#about-dsrp} 정보

AEM Communities이 관계형 데이터베이스를 공용 저장소로 사용하도록 구성된 경우 동기화나 복제 없이도 모든 작성자 및 게시 인스턴스에서 사용자 생성 컨텐츠(UGC)에 액세스할 수 있습니다.

[SRP 옵션](working-with-srp.md#characteristics-of-srp-options) 및 [권장 토폴로지](topologies.md)도 참조하십시오.

## 요구 사항 {#requirements}

* [MySQL](#mysql-configuration), 관계형 데이터베이스입니다.
* [Apache Solr](#solr-configuration), 검색 플랫폼.

>[!NOTE]
>
>기본 스토리지 구성은 이제 등의 경로(`/etc/socialconfig/srpc/defaultconfiguration`) 대신 conf 경로(`/conf/global/settings/community/srpc/defaultconfiguration`)에 저장됩니다. [마이그레이션 단계](#zerodt-migration-steps)에 따라 기본 스크립트가 예상대로 작동되도록 하는 것이 좋습니다.

## 관계형 데이터베이스 구성 {#relational-database-configuration}

### MySQL 구성 {#mysql-configuration}

다른 데이터베이스(스키마) 이름과 다른 연결(server:port)을 사용하여 동일한 연결 풀 내의 활성 기능과 공용 저장소(DSRP) 간에 MySQL 설치를 공유할 수 있습니다.

설치 및 구성 세부 정보는 [DSRP](dsrp-mysql.md)에 대한 MySQL 구성을 참조하십시오.

### Solr 구성 {#solr-configuration}

다른 컬렉션을 사용하여 노드 스토어(Oak)와 공용 스토어(SRP) 간에 솔루션 설치를 공유할 수 있습니다.

Oak 컬렉션과 SRP 컬렉션을 모두 집중적으로 사용하는 경우 성능상의 이유로 두 번째 솔러를 설치할 수 있습니다.

프로덕션 환경의 경우 SolrCloud 모드는 독립형 모드(단일 로컬 솔루션 설정)에 비해 향상된 성능을 제공합니다.

설치 및 구성 세부 정보는 [SRP](solr.md)용 솔루션 구성을 참조하십시오.

### DSRP {#select-dsrp} 선택

[스토리지 구성 콘솔](srp-config.md)에서는 사용할 SRP 구현을 식별하는 기본 스토리지 구성을 선택할 수 있습니다.

작성자가 스토리지 구성 콘솔에 액세스하려면

* 관리자 권한으로 로그인
* **주 메뉴**&#x200B;에서

   * 왼쪽 창에서 **[!UICONTROL 도구]** 선택
   * **[!UICONTROL 커뮤니티]** 선택
   * **[!UICONTROL 스토리지 구성]** 선택

      * 예를 들어 결과 위치는 다음과 같습니다.[http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)
      >[!NOTE]
      >
      >이제 기본 스토리지 구성이 conf 경로(`/conf/global/settings/community/srpc/defaultconfiguration`)에 저장됩니다.      를 사용하여 새 경로를 찾습니다(`/etc/socialconfig/srpc/defaultconfiguration`). [마이그레이션 단계](#zerodt-migration-steps)에 따라 기본 스크립트가 예상대로 작동되도록 하는 것이 좋습니다.
   ![dsrp-config](assets/dsrp-config.png)

* **[!UICONTROL DSRP(데이터베이스 저장소 리소스 공급자)]** 선택
* **데이터베이스 구성**

   * **[!UICONTROL JDBC 데이터 소스 이름]**

      MySQL 연결에 지정된 이름은 [JDBC OSGi 구성](dsrp-mysql.md#configurejdbcconnections)에 입력한 이름과 같아야 합니다.

      *기본값*:커뮤니티

   * **[!UICONTROL 데이터베이스 이름]**

      [init_schema.sql](dsrp-mysql.md#obtain-the-sql-script) 스크립트에서 스키마에 지정된 이름

      *기본값*:커뮤니티

* **SolrConfiguration**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Zookeeper 호스트**

      내부 ZooKeeper를 사용하여 Solr을 실행하는 경우 이 값을 비워 둡니다. 그렇지 않은 경우 외부 ZooKeeper와 함께 [SolrCloud 모드](solr.md#solrcloud-mode)에서 실행할 때 이 값을 *my.server.com:80* 등 ZooKeeper의 URI로 설정합니다.

      *기본값*:  *&lt;blank>*

   * **[!UICONTROL Solr URL]**

      *기본값*:https://127.0.0.1:8983/solr/

   * **[!UICONTROL Solr 컬렉션]**

      *기본값*:collection1

* **[!UICONTROL 제출]**&#x200B;을 선택합니다.

### 기본 srp {#zerodt-migration-steps}에 대한 다운타임 마이그레이션 단계 없음

다음 단계에 따라 기본 srp 페이지 [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)이(가) 예상대로 작동하는지 확인합니다.

1. 시스템 구성이 다시 jsrp(기본값)로 돌아가도록 `/etc/socialconfig`에서 `/etc/socialconfig_old`로 경로 이름을 변경합니다.
1. 기본 srp 페이지 [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)로 이동합니다. 여기서 jsrp는 구성되어 있습니다. `/conf/global/settings/community/srpc`에 새 기본 구성 노드가 만들어지도록 **[!UICONTROL submit]** 단추를 클릭합니다.
1. 생성된 기본 구성 `/conf/global/settings/community/srpc/defaultconfiguration`을(를) 삭제합니다.
1. 이전 단계에서 삭제된 노드(`/conf/global/settings/community/srpc/defaultconfiguration`) 대신 이전 구성 `/etc/socialconfig_old/srpc/defaultconfiguration`을 복사합니다.
1. 이전 etc 노드 `/etc/socialconfig_old`을(를) 삭제합니다.

## 구성 {#publishing-the-configuration} 게시

DSRP는 모든 작성자 및 게시 인스턴스에서 공용 스토어로 식별되어야 합니다.

게시 환경에서 동일한 구성을 사용할 수 있도록 하려면:

* 작성자:

   * 주 메뉴에서 **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 복제]**&#x200B;로 이동합니다.
   * **[!UICONTROL 트리 활성화]**&#x200B;를 두 번 클릭합니다
   * **시작 경로**:

      * `/etc/socialconfig/srpc/` 찾아보기
   * `Only Modified`이(가) 선택되지 않았는지 확인합니다.
   * **[!UICONTROL 활성화]**&#x200B;를 선택합니다.


## 사용자 데이터 관리 {#managing-user-data}

게시 환경에 종종 입력되는 *사용자*, *사용자 프로필* 및 *사용자 그룹*&#x200B;에 대한 자세한 내용은 다음을 참조하십시오.

* [사용자 동기화](sync.md)
* [사용자 및 사용자 그룹 관리](users.md)

## DSRP {#reindexing-solr-for-dsrp}에 대한 색인 다시 지정

DSRP Solr를 다시 색인화하려면 [MSRP](msrp.md#msrp-reindex-tool)에 대한 색인 재지정 설명서를 따르되, DSRP에 대해 다시 색인화할 때에는 다음 URL을 대신 사용하십시오.**/services/social/datastore/rdb/reindex**

예를 들어 DSRP를 다시 색인화하는 말림 명령은 다음과 같습니다.

```shell
curl -u admin:password -X POST -F path=/ https://host:port/services/social/datastore/rdb/reindex
```

