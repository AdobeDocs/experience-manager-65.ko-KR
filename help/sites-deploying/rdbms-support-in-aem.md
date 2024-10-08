---
title: AEM 6.4의 RDBMS 지원
description: AEM 6.4의 관계형 데이터베이스 지속성 지원 및 사용 가능한 구성 옵션에 대해 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
docset: aem65
feature: Administering
exl-id: 1e34c5ca-9e08-4b2a-901c-ab28aeb4a807
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 0%

---

# AEM 6.4의 RDBMS 지원{#rdbms-support-in-aem}

## 개요 {#overview}

AEM의 관계형 데이터베이스 지속성 지원은 문서 마이크로커널을 사용하여 구현됩니다. Document Microkernel은 MongoDB 지속성을 구현하는 데에도 사용되는 기초이다.

Mongo Java API를 기반으로 하는 Java API로 구성되어 있습니다. BlobStore API 구현도 제공됩니다. 기본적으로 블롭은 데이터베이스에 저장됩니다.

구현 세부 정보에 대한 자세한 내용은 [RDBDocumentStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBDocumentStore.html) 및 [RDBBlobStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBBlobStore.html) 설명서를 참조하십시오.

>[!NOTE]
>
>**PostgreSQL 9.4**&#x200B;에 대한 지원도 제공되지만 데모용으로만 제공됩니다. 프로덕션 환경에서는 사용할 수 없습니다.

## 지원되는 데이터베이스 {#supported-databases}

AEM의 관계형 데이터베이스 지원 수준에 대한 자세한 내용은 [기술 요구 사항 페이지](/help/sites-deploying/technical-requirements.md)를 참조하십시오.

## 구성 단계 {#configuration-steps}

`DocumentNodeStoreService` OSGi 서비스를 구성하여 저장소를 만듭니다. MongoDB 외에도 관계형 데이터베이스 지속성을 지원하는 것으로 확장되었다.

데이터 소스가 작동하려면 AEM으로 데이터 소스를 구성해야 합니다. 이 작업은 `org.apache.sling.datasource.DataSourceFactory.config` 파일을 통해 수행됩니다. 각 데이터베이스의 JDBC 드라이버는 로컬 구성 내에서 OSGi 번들로 별도로 제공되어야 합니다.

JDBC 드라이버용 OSGi 번들을 만드는 단계는 Apache Sling 웹 사이트에서 이 [설명서](https://sling.apache.org/documentation/bundles/datasource-providers.html#convert-driver-jars-to-bundle)를 참조하십시오.

번들이 준비되면 아래 단계에 따라 RDB 지속성을 사용하여 AEM을 구성합니다.

1. 데이터베이스 데몬이 시작되었고 AEM에서 사용할 활성 데이터베이스가 있는지 확인합니다.
1. AEM 6.3 jar를 설치 디렉토리에 복사합니다.
1. 설치 디렉터리에 `crx-quickstart\install` 폴더를 만듭니다.
1. `crx-quickstart\install` 디렉터리에 다음 이름의 구성 파일을 만들어 문서 노드 저장소를 구성합니다.

   * `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

1. `crx-quickstart\install` 폴더에 다음 이름의 다른 구성 파일을 만들어 데이터 원본 및 JDBC 매개 변수를 구성합니다.

   * `org.apache.sling.datasource.DataSourceFactory-oak.config`

   >[!NOTE]
   >
   >지원되는 각 데이터베이스의 데이터 원본 구성에 대한 자세한 내용은 [데이터 Source 구성 옵션](/help/sites-deploying/rdbms-support-in-aem.md#data-source-configuration-options)을 참조하십시오.

1. 다음으로 AEM에 사용할 JDBC OSGi 번들을 준비합니다.

   1. `crx-quickstart/install` 폴더에서 `9` 폴더를 만듭니다.

   1. 새 폴더에 JDBC jar를 넣습니다.

1. 마지막으로 `crx3` 및 `crx3rdb` 실행 모드로 AEM을 시작합니다.

   ```java
   java -jar quickstart.jar -r crx3,crx3rdb
   ```

## 데이터 Source 구성 옵션 {#data-source-configuration-options}

`org.apache.sling.datasource.DataSourceFactory-oak.config` OSGi 구성은 AEM과 데이터베이스 지속성 계층 간의 통신에 필요한 매개 변수를 구성하는 데 사용됩니다.

다음 구성 옵션을 사용할 수 있습니다.

* `datasource.name:` 데이터 원본 이름입니다. 기본값은 `oak`입니다.

* `url:` JDBC와 함께 사용해야 하는 데이터베이스의 URL 문자열입니다. 각 데이터베이스 유형에는 고유한 URL 문자열 형식이 있습니다. 자세한 내용은 아래의 [URL 문자열 형식](/help/sites-deploying/rdbms-support-in-aem.md#url-string-formats)을 참조하십시오.

* `driverClassName:` JDBC 드라이버 클래스 이름입니다. 이는 사용하려는 데이터베이스와 해당 데이터베이스에 연결하는 데 필요한 드라이버에 따라 달라집니다. 다음은 AEM에서 지원하는 모든 데이터베이스의 클래스 이름입니다.

   * PostgreSQL용 `org.postgresql.Driver`;
   * DB2용 `com.ibm.db2.jcc.DB2Driver`;
   * oracle에 대한 `oracle.jdbc.OracleDriver`
   * MySQL 및 MariaDB용 `com.mysql.jdbc.Driver`(실험용);
   * Microsoft SQL Server용 c `om.microsoft.sqlserver.jdbc.SQLServerDriver`(실험용).

* `username:` 데이터베이스가 실행되는 사용자 이름입니다.

* `password:` 데이터베이스 암호입니다.

### URL 문자열 형식 {#url-string-formats}

데이터 소스 구성에서는 사용해야 하는 데이터베이스 유형에 따라 다른 URL 문자열 형식이 사용됩니다. 다음은 AEM이 현재 지원하는 데이터베이스의 형식 목록입니다.

* PostgreSQL용 `jdbc:postgresql:databasename`;
* DB2용 `jdbc:db2://localhost:port/databasename`;
* oracle에 대한 `jdbc:oracle:thin:localhost:port:SID`
* MySQL 및 MariaDB용 `jdbc:mysql://localhost:3306/databasename`(실험용);
* Microsoft SQL Server용 `jdbc:sqlserver://localhost:1453;databaseName=name`(실험용).

## 알려진 제한 사항 {#known-limitations}

RDBMS 지속성에 의해 단일 데이터베이스와 함께 여러 AEM 인스턴스의 동시 사용이 지원되지만 동시 설치는 지원되지 않습니다.

이 문제를 해결하려면 먼저 단일 멤버로 설치를 실행하고 첫 번째 멤버 설치가 완료된 후 다른 멤버를 추가해야 합니다.
