---
title: 백업 및 복구할 파일
description: 이 문서에서는 백업해야 하는 응용 프로그램 및 데이터 파일에 대해 설명합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: d2dd381d-a7d2-4fec-a8ba-7ca037fd9dc1
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '2072'
ht-degree: 0%

---

# 백업 및 복구할 파일 {#files-to-back-up-and-recover}

백업해야 하는 응용 프로그램 및 데이터 파일은 다음 섹션에서 자세히 설명합니다.

백업 및 복구와 관련하여 다음 사항을 고려하십시오.

* 데이터베이스는 GDS 및 AEM 저장소 전에 백업해야 합니다.
* 백업을 위해 클러스터된 환경의 노드를 종료해야 하는 경우 주 노드 전에 보조 노드가 종료되었는지 확인하십시오. 그렇지 않으면 클러스터 또는 서버에 불일치가 발생할 수 있습니다. 또한 기본 노드는 보조 노드보다 먼저 라이브로 만들어야 합니다.
* 클러스터의 복원 작업을 수행하려면 클러스터의 각 노드에 대해 응용 프로그램 서버를 중지해야 합니다.

## 글로벌 문서 스토리지 디렉터리 {#global-document-storage-directory}

GDS는 프로세스 내에서 사용되는 장기 파일을 저장하는 데 사용되는 디렉토리입니다. 오래 지속되는 파일의 수명은 AEM Forms 시스템을 한 번 이상 시작하기 위한 것이며 며칠 및 심지어 몇 년에 걸쳐 실행될 수 있습니다. 이러한 장기 보존 파일에는 PDF, 정책 및 양식 템플릿이 포함될 수 있습니다. 장기 파일은 여러 AEM Forms 배포의 전체 상태에서 중요한 부분입니다. 일부 또는 모든 장기 문서가 손실되거나 손상되면 Forms 서버가 불안정해질 수 있습니다.

비동기 작업 호출을 위한 입력 문서는 GDS에도 저장되며 요청을 처리하는 데 사용할 수 있어야 합니다. 따라서 GDS를 호스팅하는 파일 시스템의 안정성을 고려하고 RAID(Redundant Array of Independent Disks) 또는 기타 기술을 사용자의 품질 및 서비스 요구 사항에 맞게 사용하는 것이 중요합니다.

GDS의 위치는 AEM Forms 설치 프로세스 또는 그 이후에 관리 콘솔을 사용하여 결정됩니다. GDS에 대한 고가용성 위치를 유지하는 것 외에도 문서에 대한 데이터베이스 스토리지를 활성화할 수도 있습니다. 다음을 참조하십시오 [데이터베이스를 문서 저장소로 사용할 때의 백업 옵션](files-back-recover.md#backup-options-when-database-is-used-for-document-storage).

### GDS 위치 {#gds-location}

설치하는 동안 위치 설정을 비워 두면 기본적으로 응용 프로그램 서버 설치 아래의 디렉토리가 됩니다. 응용 프로그램 서버에 대해 다음 디렉터리를 백업해야 합니다.

* (JBoss) `[appserver root]/server/'server'/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

GDS 위치를 기본값이 아닌 위치로 변경한 경우 다음과 같이 확인할 수 있습니다.

* 관리 콘솔에 로그인하고 설정 > 핵심 시스템 설정 > 구성 을 클릭합니다.
* 글로벌 문서 저장 디렉토리 상자에 지정된 위치를 기록합니다.

클러스터된 환경에서 GDS는 일반적으로 네트워크에서 공유되고 모든 클러스터 노드에 대해 읽기/쓰기 가능한 디렉토리를 가리킵니다.

GDS의 위치는 원래 위치가 더 이상 이용 가능하지 않은 경우 복구 중에 변경될 수 있다. (참조: [복구하는 동안 GDS 위치 변경](/help/forms/using/admin-help/recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).)

### 데이터베이스를 문서 저장소로 사용할 때의 백업 옵션 {#backup-options-when-database-is-used-for-document-storage}

관리 콘솔을 사용하여 AEM forms 데이터베이스에서 AEM forms 문서 저장소를 활성화할 수 있습니다. 이 옵션은 모든 영구 문서를 데이터베이스에 유지하지만 AEM Forms의 세션 및 호출과 관련된 영구 및 임시 파일 및 리소스를 저장하는 데 사용되므로 AEM Forms에는 파일 시스템 기반 GDS 디렉토리가 필요합니다.

관리 콘솔의 핵심 시스템 설정에서 또는 Configuration Manager를 사용하여 &quot;데이터베이스에서 문서 스토리지 활성화&quot; 옵션을 선택하면 AEM Forms에서 스냅샷 백업 모드 및 롤링 백업 모드를 허용하지 않습니다. 따라서 AEM Forms를 사용하여 백업 모드를 관리할 필요가 없습니다. 이 옵션을 사용하는 경우 옵션을 활성화한 후 GDS를 한 번만 백업해야 합니다. 백업에서 AEM 양식을 복구할 때 GDS에 대한 백업 디렉토리 이름을 바꾸거나 GDS를 복원할 필요가 없습니다.

## AEM 저장소 {#aem-repository}

AEM forms를 설치하는 동안 crx-repository가 구성된 경우 AEM 저장소(crx-repository)가 생성됩니다. crx-repository 디렉토리의 위치는 AEM Forms 설치 프로세스 중에 결정됩니다. AEM forms에서 일관된 AEM 양식 데이터를 사용하려면 AEM 저장소 백업 및 복원이 데이터베이스 및 GDS와 함께 필요합니다. AEM 저장소에는 서신 관리 솔루션, Forms manager 및 AEM Forms Workspace에 대한 데이터가 포함되어 있습니다.

### 서신 관리 솔루션 {#correspondence-management-solution}

서신 관리 솔루션은 안전하고 개인화된 인터랙티브한 통신의 작성, 수집 및 전달을 중앙 집중화하여 관리합니다. 이를 통해 사전 승인된 콘텐츠와 맞춤형 제작 콘텐츠에서 서신을 작성에서 보관에 이르는 프로세스를 간소화하여 신속하게 취합할 수 있습니다. 따라서 고객은 시기 적절하고 정확하며 편리하고 안전하며 적절한 커뮤니케이션을 얻을 수 있습니다. 고객 상호 작용의 가치를 극대화하고 비용과 위험을 최소화하는 프로세스를 간소화하여 간편성과 속도, 생산성을 높일 수 있습니다.

단순 서신 관리 솔루션 설정에는 동일한 컴퓨터 또는 다른 컴퓨터의 작성자 인스턴스와 게시 인스턴스가 포함됩니다

### forms 관리자 {#forms-manager}

forms manager는 양식의 업데이트, 관리 및 중단 프로세스를 간소화합니다.

### AEM Forms 작업 공간 {#html-workspace}

AEM Forms Workspace는 (JEE에서는 AEM Forms가 더 이상 사용되지 않음) Flex Workspace의 기능과 일치하며, Workspace를 확장 및 통합하고 보다 사용하기 쉬운 새로운 기능을 추가합니다.

>[!NOTE]
>
>Flex Workspace는 AEM Forms 릴리스에서 더 이상 사용되지 않습니다.

Flash Player 및 Adobe Reader 없이 클라이언트에서 작업을 관리할 수 있습니다. PDF forms 및 Flex 양식 외에도 HTML Forms의 렌디션을 용이하게 합니다.

## AEM forms 데이터베이스 {#aem-forms-database}

AEM Forms 데이터베이스는 양식 객체, 서비스 구성, 프로세스 상태 및 파일에 대한 데이터베이스 참조와 같은 컨텐츠를 GDS 및 Content Storage Root 디렉터리(Content Services의 경우)에 저장합니다. 데이터베이스 백업은 서비스 중단 없이 실시간으로 수행할 수 있으며, 특정 시점 또는 특정 변경 사항으로의 복구가 가능합니다. 이 섹션에서는 실시간으로 백업할 수 있도록 데이터베이스를 구성하는 방법에 대해 설명합니다.

올바르게 구성된 AEM Forms 시스템에서는 시스템 관리자와 데이터베이스 관리자가 쉽게 협력하여 시스템을 알려진 일관된 상태로 복구할 수 있습니다.

실시간으로 데이터베이스를 백업하려면 스냅샷 모드를 사용하거나 지정된 로그 모드에서 실행되도록 데이터베이스를 구성해야 합니다. 이렇게 하면 데이터베이스가 열려 있고 사용할 수 있는 동안 데이터베이스 파일을 백업할 수 있습니다. 또한 데이터베이스는 이러한 모드에서 실행될 때 롤백 및 트랜잭션 로그를 유지합니다.

>[!NOTE]
>
>Adobe® LiveCycle® Content Services ES(더 이상 사용되지 않음)는 LiveCycle과 함께 설치된 컨텐츠 관리 시스템입니다. 이를 통해 사용자는 인간 중심 프로세스를 설계, 관리, 모니터링 및 최적화할 수 있습니다. 콘텐츠 서비스(더 이상 사용되지 않음) 지원은 2014년 12월 31일에 종료됩니다. 다음을 참조하십시오 [제품 라이프사이클 문서 Adobe](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html).

### DB2 {#db2}

아카이브 로그 모드에서 실행되도록 DB2 데이터베이스를 구성합니다.

>[!NOTE]
>
AEM Forms 환경이 이전 버전의 AEM Forms에서 업그레이드되고 DB2를 사용하는 경우 온라인 백업이 지원되지 않습니다. 이 경우 AEM Forms를 종료하고 오프라인 백업을 수행해야 합니다. 향후 버전의 AEM Forms는 업그레이드 고객을 위한 온라인 백업을 지원합니다.

IBM에는 데이터베이스 관리자가 백업 및 복구 작업을 관리하는 데 도움이 되는 다양한 툴과 도움말 시스템이 있습니다.

* IBM DB2 아카이브 로그 가속기
* IBM DB2 데이터 아카이브 전문가

DB2에는 Tivoli Storage Manager에 데이터베이스를 백업하는 기능이 내장되어 있습니다. Tivoli Storage Manager를 사용하면 DB2 백업을 다른 미디어 또는 로컬 하드 드라이브에 저장할 수 있습니다.

### Oracle {#oracle}

스냅샷 백업을 사용하거나 아카이브 로그 모드에서 실행되도록 Oracle 데이터베이스를 구성합니다. (참조: [Oracle 백업: 소개](https://www.databasedesign-resource.com/oracle-backup.md).) oracle 데이터베이스 백업 및 복구에 대한 자세한 내용은 다음 사이트를 참조하십시오.

[Oracle 백업 및 복구:](https://www.oracle.com/technetwork/database/features/availability/br-overview-097160.html) 백업 및 복구의 개념과 백업, 복구 및 보고를 위해 RMAN(복구 관리자)을 사용하는 가장 일반적인 기술에 대해 자세히 설명하고 백업 및 복구 전략을 계획하는 방법에 대한 자세한 정보를 제공합니다.

[Oracle 데이터베이스 백업 및 복구 사용 설명서:](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10642.pdf) RMAN 아키텍처, 백업 및 복구 개념과 메커니즘, 시점 복구 및 데이터베이스 플래시백 기능과 같은 고급 복구 기술, 백업 및 복구 성능 튜닝에 대한 심층적인 정보를 제공합니다. 또한 RMAN 대신 호스트 운영 체제 기능을 사용하는 사용자 관리 백업 및 복구도 포함됩니다. 이 볼륨은 보다 정교한 데이터베이스 배포의 백업 및 복구와 고급 복구 시나리오에 필수적입니다.

[Oracle 데이터베이스 백업 및 복구 참조:](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10643.pdf) 모든 RMAN 명령의 구문과 의미에 대한 전체 정보를 제공하고 백업 및 복구 작업에 대한 보고에 사용할 수 있는 데이터베이스 보기에 대해 설명합니다.

### SQL 서버 {#sql-server}

스냅샷 백업을 사용하거나 트랜잭션 로그 모드에서 실행되도록 SQL Server 데이터베이스를 구성합니다.

SQL Server는 두 가지 백업 및 복구 도구도 제공합니다.

* SQL Server Management Studio(GUI)
* T-SQL(명령줄)

자세한 내용은 [백업 및 복원](https://msdn.microsoft.com/en-us/library/ms187048(v=SQL.90).aspx).

### MySQL {#mysql}

MySQLAdmin을 사용하거나 Windows에서 INI 파일을 수정하여 이진 로그 모드에서 실행되도록 MySQL 데이터베이스를 구성합니다. (참조: [MySQL 이진 로깅](https://dev.mysql.com/doc/refman/5.1/en/binary-log.html).) MySQL용 핫 백업 툴은 InnoBase 소프트웨어도 사용할 수 있습니다. (참조: [Innobase 핫 백업](https://www.innodb.com/hot-backup/features.md).)

>[!NOTE]
>
MySQL의 기본 바이너리 로깅 모드는 &quot;문&quot;으로, Content Services에서 사용하는 테이블과 호환되지 않습니다(더 이상 사용되지 않음). 이 기본 모드에서 바이너리 로깅을 사용하면 Content Services(더 이상 사용되지 않음)가 실패합니다. 시스템에 컨텐츠 서비스(사용 중단됨)가 포함되어 있는 경우 &quot;혼합&quot; 로깅 모드를 사용하십시오. &quot;혼합&quot; 로깅을 활성화하려면 my.ini 파일에 다음 인수를 추가합니다. `binlog_format=mixed log-bin=logname`

mysqldump 유틸리티를 사용하여 전체 데이터베이스 백업을 가져올 수 있습니다. 전체 백업이 필요하지만 항상 편리한 것은 아닙니다. 대용량 백업 파일을 생성하고 생성하는 데 시간이 걸립니다. 증분 백업을 수행하려면 -를 사용하여 서버를 시작해야 합니다. `log-bin` 이전 섹션에 설명된 대로 옵션입니다. MySQL Server가 다시 시작될 때마다 현재 이진 로그로의 쓰기가 중지되고 새 이진 로그가 만들어지며 그때부터 새 이진 로그는 현재 이진 로그가 됩니다. 를 사용하여 스위치를 수동으로 강제 적용할 수 있습니다. `FLUSH LOGS SQL` 명령입니다. 첫 번째 전체 백업 후 후속 증분 백업은 mysqladmin 유틸리티를 `flush-logs` 다음 로그 파일을 만드는 명령입니다.

다음을 참조하십시오 [백업 전략 요약](https://dev.mysql.com/doc/refman/5.5/en/backup-strategy-summary.html).

```text
binlog_format=mixed
log-bin=logname
```

## 콘텐츠 저장소 루트 디렉터리(Content Services만 해당) {#content-storage-root-directory-content-services-only}

Content Storage Root 디렉토리에는 모든 문서, 객체 및 인덱스가 저장되는 Content Services(사용되지 않음) 저장소가 있습니다. 콘텐츠 저장소 루트 디렉터리 트리를 백업해야 합니다. 이 섹션에서는 독립형 환경과 클러스터형 환경 모두에 대한 Content Storage Root 디렉토리의 위치를 확인하는 방법에 대해 설명합니다.

### 콘텐츠 저장소 루트 위치(독립형 환경) {#content-storage-root-location-stand-alone-environment}

Content Services(더 이상 사용되지 않음)를 설치하면 콘텐츠 저장소 루트 디렉터리가 만들어집니다. 컨텐트 저장 영역 루트 디렉토리의 위치는 AEM Forms 설치 프로세스 중에 결정됩니다.

콘텐츠 저장소 루트 디렉토리의 기본 위치는 입니다. `[aem-forms root]/lccs_data`.

Content Storage Root 디렉터리에 있는 다음 디렉터리를 백업합니다.

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

/backup-lucene-indexes 디렉토리가 없으면 Content Storage Root 디렉토리에도 있는 /lucene-indexes 디렉토리를 백업합니다. /backup-lucene-indexes 디렉터리가 있으면 오류가 발생할 수 있으므로 /lucene-indexes 디렉터리를 백업하지 마십시오.

### 콘텐츠 저장소 루트 위치(클러스터된 환경) {#content-storage-root-location-clustered-environment}

클러스터된 환경에 Content Services(사용되지 않음)를 설치하면 Content Storage Root 디렉터리는 두 개의 개별 디렉터리로 분할됩니다.

**콘텐츠 저장소 루트 디렉터리:** 일반적으로 클러스터의 모든 노드에 대해 읽기/쓰기 액세스 가능한 공유 네트워크 디렉토리입니다

**인덱스 루트 디렉터리:** 클러스터의 각 노드에 생성되며 항상 동일한 경로와 디렉토리 이름을 갖는 디렉토리

콘텐츠 저장소 루트 디렉토리의 기본 위치는 입니다. `[GDS root]/lccs_data`, 여기서 `[GDS root]` 는에 설명된 위치입니다. [GDS 위치](files-back-recover.md#gds-location). Content Storage Root 디렉터리에 있는 다음 디렉터리를 백업합니다.

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

/backup-lucene-indexes 디렉토리가 없으면 Content Storage Root 디렉토리에도 있는 /lucene-indexes 디렉토리를 백업합니다. /backup-lucene-indexes 디렉터리가 있으면 오류가 발생할 수 있으므로 /lucene-indexes 디렉터리를 백업하지 마십시오.

인덱스 루트 디렉토리의 기본 위치는 다음과 같습니다. `[aem-forms root]/lucene-indexes` 각 노드에서

## 고객 설치 글꼴 {#customer-installed-fonts}

AEM Forms 환경에 추가 글꼴을 설치한 경우 별도로 백업해야 합니다. 설정 > 핵심 시스템 > 구성 아래의 관리 콘솔에 지정된 모든 Adobe 및 고객 글꼴 디렉터리를 백업합니다. 전체 글꼴 디렉터리를 백업해야 합니다.

>[!NOTE]
>
기본적으로 AEM Forms와 함께 설치된 Adobe 글꼴은에 있습니다. `[aem-forms root]/fonts` 디렉토리.

호스트 컴퓨터에서 운영 체제를 다시 초기화하고 이전 운영 체제의 글꼴을 사용하려면 시스템 글꼴 디렉터리의 내용도 백업해야 합니다. 자세한 지침은 해당 운영 체제 설명서를 참조하십시오.
