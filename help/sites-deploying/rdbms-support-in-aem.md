---
title: AEM 6.4의 RDBMS 지원
seo-title: AEM 6.4의 RDBMS 지원
description: AEM 6.4의 관계형 데이터베이스 지속성 지원 및 사용 가능한 구성 옵션에 대해 알아봅니다.
seo-description: AEM 6.4의 관계형 데이터베이스 지속성 지원 및 사용 가능한 구성 옵션에 대해 알아봅니다.
uuid: c8422b0d-c6df-488d-bb6a-af92c9afda50
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 6a754d42-da30-4c2f-8b9c-369e1f1f92b5
docset: aem65
feature: Configuring
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---


# AEM 6.4에서 RDBMS 지원{#rdbms-support-in-aem}

## 개요 {#overview}

AEM에서 관계형 데이터베이스 지속성 지원은 Document Microkernel을 사용하여 구현됩니다. 문서 마이크로커널은 MongoDB 지속성을 구현하는 데에도 사용되는 기본입니다.

Mongo Java API를 기반으로 하는 Java API로 구성됩니다. BlobStore API 구현도 제공됩니다. 기본적으로 블로브는 데이터베이스에 저장됩니다.

구현 세부 정보에 대한 자세한 내용은 [RDBDocumentStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBDocumentStore.html) 및 [RDBBlobStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBBlobStore.html) 설명서를 참조하십시오.

>[!NOTE]
>
>**PostgreSQL 9.4**&#x200B;에 대한 지원도 제공되지만 데모 용도로만 제공됩니다. 제작 환경에서는 사용할 수 없습니다.

## 지원되는 데이터베이스 {#supported-databases}

AEM의 관계형 데이터베이스 지원 수준에 대한 자세한 내용은 [기술 요구 사항 페이지](/help/sites-deploying/technical-requirements.md)를 참조하십시오.

## 구성 단계 {#configuration-steps}

보관소는 `DocumentNodeStoreService` OSGi 서비스를 구성하여 만듭니다. MongoDB 외에도 관계형 데이터베이스 지속성을 지원하도록 확장되었습니다.

이를 수행하려면 AEM으로 데이터 소스를 구성해야 합니다. 이 작업은 `org.apache.sling.datasource.DataSourceFactory.config` 파일을 통해 수행됩니다. 로컬 구성 내의 OSGi 번들로 각 데이터베이스의 JDBC 드라이버를 별도로 제공해야 합니다.

JDBC 드라이버용 OSGi 번들을 만드는 방법에 대한 자세한 내용은 Apache Sling 웹 사이트에서 이 [documentation](https://sling.apache.org/documentation/bundles/datasource-providers.html#convert-driver-jars-to-bundle)을 참조하십시오.

번들이 적절히 준비되면 아래 단계를 수행하여 RDB 지속성을 사용하여 AEM을 구성합니다.

1. 데이터베이스 데몬이 시작되었고 AEM에 사용할 활성 데이터베이스가 있는지 확인합니다.
1. AEM 6.3 jar를 설치 디렉토리로 복사합니다.
1. 설치 디렉토리에 `crx-quickstart\install`라는 폴더를 만듭니다.
1. `crx-quickstart\install` 디렉터리에 다음 이름의 구성 파일을 만들어 문서 노드 저장소를 구성합니다.

   * `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

1. `crx-quickstart\install` 폴더에 다음 이름으로 다른 구성 파일을 만들어 데이터 소스 및 JDBC 매개 변수를 구성합니다.

   * `org.apache.sling.datasource.DataSourceFactory-oak.config`
   >[!NOTE]
   >
   >지원되는 각 데이터베이스의 데이터 소스 구성에 대한 자세한 내용은 [데이터 소스 구성 옵션](/help/sites-deploying/rdbms-support-in-aem.md#data-source-configuration-options)을 참조하십시오.

1. 다음으로 AEM에 사용할 JDBC OSGi 번들을 준비합니다.

   1. `crx-quickstart/install` 폴더에서 `9` 폴더를 만듭니다.

   1. 새 폴더에 JDBC jar를 배치합니다.

1. 마지막으로 AEM을 `crx3` 및 `crx3rdb` 실행 모드로 시작합니다.

   ```java
   java -jar quickstart.jar -r crx3,crx3rdb
   ```

## 데이터 소스 구성 옵션 {#data-source-configuration-options}

`org.apache.sling.datasource.DataSourceFactory-oak.config` OSGi 구성은 AEM 및 데이터베이스 지속성 레이어 간의 통신에 필요한 매개 변수를 구성하는 데 사용됩니다.

다음 구성 옵션을 사용할 수 있습니다.

* `datasource.name:` 데이터 소스 이름입니다. 기본값은 `oak`입니다.

* `url:` JDBC에 사용해야 하는 데이터베이스의 URL 문자열입니다. 각 데이터베이스 유형에는 고유한 URL 문자열 형식이 있습니다. 자세한 내용은 아래 [URL 문자열 형식](/help/sites-deploying/rdbms-support-in-aem.md#url-string-formats)을 참조하십시오.

* `driverClassName:` JDBC 드라이버 클래스 이름입니다. 사용하려는 데이터베이스와 그 후 해당 데이터베이스에 연결하는 데 필요한 드라이버에 따라 다릅니다. 다음은 AEM에서 지원하는 모든 데이터베이스의 클래스 이름입니다.

   * `org.postgresql.Driver` for PostgreSQL;
   * `com.ibm.db2.jcc.DB2Driver` DB2;
   * `oracle.jdbc.OracleDriver` oracle의 경우
   * `com.mysql.jdbc.Driver` for MySQL and MariaDB (실험적);
   * c `om.microsoft.sqlserver.jdbc.SQLServerDriver` for Microsoft SQL Server(시험적)

* `username:` 데이터베이스가 실행되는 사용자 이름입니다.

* `password:` 데이터베이스 암호입니다.

### URL 문자열 형식 {#url-string-formats}

사용해야 하는 데이터베이스 유형에 따라 데이터 소스 구성에서 다른 URL 문자열 형식이 사용됩니다. 다음은 AEM에서 현재 지원하는 데이터베이스의 형식 목록입니다.

* `jdbc:postgresql:databasename` for PostgreSQL;
* `jdbc:db2://localhost:port/databasename` DB2;
* `jdbc:oracle:thin:localhost:port:SID` oracle의 경우
* `jdbc:mysql://localhost:3306/databasename` for MySQL and MariaDB (실험적);
* `jdbc:sqlserver://localhost:1453;databaseName=name` for Microsoft SQL Server(시험적).

## 알려진 제한 사항 {#known-limitations}

단일 데이터베이스가 있는 여러 AEM 인스턴스를 동시에 사용하는 것은 RDBMS 지속성에서 지원되지만 동시 설치는 지원되지 않습니다.

이 문제를 해결하려면 먼저 단일 구성원을 사용하여 설치를 실행하고 설치를 마친 후 다른 구성원을 추가하십시오.

