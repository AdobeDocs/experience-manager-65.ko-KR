---
title: 활성 기능을 위한 MySQL 구성
seo-title: 활성 기능을 위한 MySQL 구성
description: MySQL 서버 연결
seo-description: MySQL 서버 연결
uuid: e02d9404-de75-4fdb-896c-ea3f64f980a3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 9222bc93-c231-4ac8-aa28-30d784a4ca3b
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1093'
ht-degree: 2%

---


# 활성 기능을 위한 MySQL 구성 {#mysql-configuration-for-enablement-features}

MySQL은 활성 리소스에 대한 SCORM 추적 및 보고 데이터에 주로 사용되는 관계형 데이터베이스입니다. 비디오 일시 중지/재개 추적과 같은 다른 기능에 대한 표도 포함되어 있습니다.

다음 지침은 MySQL Server에 연결하고 활성 데이터베이스를 설정하고 초기 데이터로 데이터베이스를 채우는 방법을 설명합니다.

## 요구 사항 {#requirements}

MySQL for Communities 지원 기능을 구성하기 전에

* MySQL [Server](https://dev.mysql.com/downloads/mysql/) Community Server 버전 5.6 설치:
   * 버전 5.7은 SCORM에서 지원되지 않습니다.
   * 작성자 AEM 인스턴스와 동일한 서버일 수 있습니다.
* 모든 AEM 인스턴스에서 MySQL용 공식 [JDBC 드라이버를 설치합니다](deploy-communities.md#jdbc-driver-for-mysql).
* MySQL [워크벤치를 설치합니다](https://dev.mysql.com/downloads/tools/workbench/).
* 모든 AEM 인스턴스에서 [SCORM 패키지를 설치합니다](enablement.md#scorm).

## MySQL 설치 {#installing-mysql}

대상 OS에 대한 지침에 따라 MySQL을 다운로드하여 설치해야 합니다.

### 소문자 표 이름 {#lower-case-table-names}

대/소문자 구분 운영 체제의 경우 SQL은 대/소문자를 구분하지 않으므로 모든 테이블 이름을 소문자로 시작하는 설정을 포함해야 합니다.

예를 들어, Linux OS에서 모든 소문자 표 이름을 지정하려면:

* 파일 편집 `/etc/my.cnf`
* 섹션에서 `[mysqld]` 다음 줄을 추가합니다. `lower_case_table_names = 1`

### UTF8 문자 집합 {#utf-character-set}

더 나은 다국어 지원을 제공하려면 UTF8 문자 집합을 사용해야 합니다.

MySQL을 문자 집합으로 UTF8로 변경합니다.
* mysql > SET NAMES &#39;utf8&#39;;

MySQL 데이터베이스를 기본적으로 UTF8로 변경합니다.
* 파일 편집 `/etc/my.cnf`
* 섹션에서 다음을 `[client]` 추가합니다. `default-character-set=utf8`
* 섹션에서 다음을 `[mysqld]` 추가합니다. `character-set-server=utf8`

## MySQL Workbench 설치 {#installing-mysql-workbench}

MySQL Workbench는 스키마 및 초기 데이터를 설치하는 SQL 스크립트를 실행하기 위한 UI를 제공합니다.

대상 OS에 대한 지침에 따라 MySQL Workbench를 다운로드하고 설치해야 합니다.

## 활성 연결 {#enablement-connection}

MySQL Workbench가 처음 실행될 때, 이미 다른 용도로 사용되지 않는 한, 어떠한 연결도 아직 표시되지 않습니다.

![myqlconnection](assets/mysqlconnection.png)

### 새 연결 설정 {#new-connection-settings}

1. 오른쪽의 &#39;+&#39; 아이콘을 선택합니다 `MySQL Connections`.
1. 대화 상자 `Setup New Connection`에서 동일한 서버에 작성자 AEM 인스턴스와 MySQL을 사용하여 데모 목적으로 플랫폼에 적합한 값을 입력합니다.
   * 연결 이름: `Enablement`
   * 연결 방법: `Standard (TCP/IP)`
   * Hostname: `127.0.0.1`
   * 사용자 이름: `root`
   * 암호: `no password by default`
   * 기본 스키마: `leave blank`
1. 실행 중인 MySQL 서비스 `Test Connection` 에 대한 연결을 확인하려면 선택합니다.

**메모**:
* 기본 포트는 입니다 `3306`.
* 선택한 `Connection Name` 항목은 JDBC OSGi 구성에 `datasource` 이름으로 [입력됩니다](#configure-jdbc-connections).

#### 연결 성공 {#successful-connection}

![mysqlconnection1](assets/mysqlconnection1.png)

#### 새 활성 연결 {#new-enablement-connection}

![mysqlconnection2](assets/mysqlconnection2.png)

## 데이터베이스 설정 {#database-setup}

새 활성화 연결을 열면 테스트 스키마와 기본 사용자 계정이 있습니다.

![database-setup](assets/database-setup.png)

### SQL 스크립트 가져오기 {#obtain-sql-scripts}

SQL 스크립트는 작성자 인스턴스의 CRXDE Lite을 사용하여 얻습니다. SCORM [패키지가](deploy-communities.md#scorm) 설치되어 있어야 합니다.

1. CRXDE Lite 찾아보기:
   * 예: [http://localhost:4502/crx/de](http://localhost:4502/crx/de)
1. 폴더 `/libs/social/config/scorm/` 확장
1. 다운로드 `database_scormengine.sql`
1. 다운로드 `database_scorm_integration.sql`

![sqlscripts](assets/sqlscripts.png)

스키마를 다운로드하는 방법 중 하나는 다음과 같습니다.

* sql 파일의 `jcr:content` 노드를 선택합니다.
* 속성 값은 보기 링크입니다 `jcr:data` .
* 보기 링크를 선택하여 데이터를 로컬 파일에 저장합니다.

### SCORM 데이터베이스 만들기 {#create-scorm-database}

생성할 활성 SCORM 데이터베이스:

* 이름: `ScormEngineDB`
* 스크립트에서 생성:
   * 스키마: `database_scormengine.sql`
   * data: `database_scorm_integration.sql`
Follow the steps below (
[각](#step-open-sql-file)SQL 스크립트 [를](#step-execute-sql-script)설치하려면 [열기 [, 실행]](#obtain-sql-scripts) 을 선택합니다. [스크립트 실행 결과를 보기 위해 필요한 경우 새로 고칩니다](#refresh) .

데이터를 설치하기 전에 스키마를 설치해야 합니다.

>[!CAUTION]
>
>데이터베이스 이름이 변경된 경우 다음 위치에 올바로 지정해야 합니다.
>
>* [JDBC 구성](#configure-jdbc-connections)
>* [SCORM 구성](#configure-scorm)


#### 1단계:SQL 파일 열기 {#step-open-sql-file}

MySQL Workbench

* 파일 풀다운 메뉴에서
* 선택 `Open SQL Script ...`
* 이 순서대로 다음 중 하나를 선택합니다.
   1. `database_scormengine.sql`
   1. `database_scorm_integration.sql`

![scrom-database](assets/scrom-database.png)

#### 2단계:SQL 스크립트 실행 {#step-execute-sql-script}

1단계에서 연 파일의 워크벤치 창에서 스크립트를 실행할 `lightening (flash) icon` 을 선택합니다.

SCORM 데이터베이스를 만드는 `database_scormengine.sql` 스크립트 실행을 완료하는 데 1분이 걸릴 수 있습니다.

![scrom-database1](assets/scrom-database1.png)

#### 새로 고침 {#refresh}

스크립트가 실행되면 새 데이터베이스를 보기 위해 `SCHEMAS` `Navigator` 의 섹션을 새로 고쳐야 합니다. &#39;SCHEMAS&#39; 오른쪽에 새로 고침 아이콘을 사용합니다.

![scrom-database2](assets/scrom-database2.png)

#### 결과:형식 엔진 edb {#result-scormenginedb}

SCHEMAS를 설치하고 새로 고치면 이 항목이 `scormenginedb` 표시됩니다.

![scrom-database3](assets/scrom-database3.png)

## JDBC 연결 구성 {#configure-jdbc-connections}

일 공용 JDBC 연결 풀에 대한 **OSGi 구성은 MySQL JDBC 드라이버를** 구성합니다.

모든 게시 및 작성자 AEM 인스턴스는 동일한 MySQL 서버를 가리킵니다.

AEM과 다른 서버에서 MySQL을 실행하는 경우 JDBC 커넥터의 &#39;localhost&#39; 대신 서버 호스트 이름을 지정해야 합니다(ScormEngine 구성을 채우는 [JDBC 커넥터](#configurescormengineservice) ).

* 각 작성자 및 게시 AEM 인스턴스
* 관리자 권한으로 로그인
* 웹 [콘솔 액세스](../../help/sites-deploying/configuring-osgi.md)
   * 예: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
* Locate the `Day Commons JDBC Connections Pool`
* 새 구성을 만들려면 `+` 아이콘을 선택합니다.

   ![jdbcconnection1](assets/jdbcconnection1.png)

* 다음 값을 입력합니다.
   * **[!UICONTROL JDBC 드라이버 클래스]**: `com.mysql.jdbc.Driver`
   * **DBC 연결 URIJ**: `jdbc:mysql://localhost:3306/aem63reporting` MySQL 서버가 &#39;this&#39; AEM 서버와 같지 않을 경우 localhost 대신 서버를 지정합니다.
   * **[!UICONTROL 사용자 이름]**:&#39;root&#39;가 아닌 경우 MySQL Server에 대해 구성된 사용자 이름을 입력하거나 루트를 입력합니다.
   * **[!UICONTROL 암호]**:MySQL에 대해 설정된 암호가 없으면 이 필드를 지우거나 MySQL 사용자 이름에 대해 구성된 암호를 입력합니다.
   * **[!UICONTROL 데이터 소스 이름]**:MySQL 연결에 대해 입력한 이름( [예: &#39;enablement](#new-connection-settings)&#39;).
* **[!UICONTROL 저장]**&#x200B;을 선택합니다.

## Scorm 구성 {#configure-scorm}

### AEM Communities ScormEngine 서비스 {#aem-communities-scormengine-service}

AEM Communities ScormEngine 서비스에 대한 OSGi 구성은 **역량 강화 커뮤니티에서 MySQL** 서버를 사용하도록 SCORM을 구성합니다.

이 구성은 SCORM 패키지 [가](deploy-communities.md#scorm-package) 설치될 때 나타납니다.

모든 게시 및 작성 인스턴스는 동일한 MySQL 서버를 가리킵니다.

AEM과 다른 서버에서 MySQL을 실행하는 경우 ScormEngine 서비스의 &#39;localhost&#39; 대신 서버 호스트 이름을 지정해야 합니다. 이 호스트 이름은 일반적으로 [JDBC 연결](#configure-jdbc-connections) 구성에서 채워집니다.

* 각 작성자 및 게시 AEM 인스턴스
* 관리자 권한으로 로그인
* 웹 [콘솔 액세스](../../help/sites-deploying/configuring-osgi.md)
   * 예: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
* Locate the `AEM Communities ScormEngine Service`
* 편집 아이콘 선택

   ![chlimage_1-337](assets/chlimage_1-337.png)

* 다음 매개 변수 값이 [JDBC 연결 구성과 일치하는지](#configurejdbcconnectionspool) 확인합니다.
   * **[!UICONTROL JDBC 연결 URI]**: `jdbc:mysql://localhost:3306/ScormEngineDB` *SCORMEngineDB는* SQL 스크립트의 기본 데이터베이스 이름입니다
   * **[!UICONTROL 사용자 이름]**:&#39;root&#39;가 아닌 경우 MySQL Server에 대해 구성된 사용자 이름을 입력하거나 루트를 입력합니다.
   * **[!UICONTROL 암호]**:MySQL에 대해 설정된 암호가 없으면 이 필드를 지우거나 MySQL 사용자 이름에 대해 구성된 암호를 입력하십시오.
* 다음 매개 변수에 대해:
   * **[!UICONTROL Scorm 사용자 암호]**:편집 안 함

      내부용으로만 사용:이는 AEM Communities이 scorm 엔진과 통신하는 데 사용하는 특수 서비스 사용자를 위한 것입니다.
* **[!UICONTROL 저장]**&#x200B;을 선택합니다

### Adobe Granite CSRF 필터 {#adobe-granite-csrf-filter}

활성 강좌가 모든 브라우저에서 제대로 작동하는지 확인하려면 CSRF 필터에서 확인하지 않은 사용자 에이전트로 Mozilla를 추가해야 합니다.

* 관리자 권한으로 AEM 게시 인스턴스에 로그인합니다.
* 웹 [콘솔 액세스](../../help/sites-deploying/configuring-osgi.md)
   * 예: [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)
* 위치 `Adobe Granite CSRF Filter`확인
* 편집 아이콘을 선택합니다.

   ![jdbcconnection2](assets/jdbcconnection2.png)

* 안전 사용자 에이전트를 추가하려면 `[+]` 아이콘을 선택합니다.
* Enter `Mozilla/*`.
* **[!UICONTROL 저장]**&#x200B;을 선택합니다.

