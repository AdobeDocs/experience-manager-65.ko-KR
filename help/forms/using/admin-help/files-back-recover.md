---
title: 백업 및 복구할 파일
description: 이 문서에서는 백업해야 하는 애플리케이션 및 데이터 파일을 설명합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: d2dd381d-a7d2-4fec-a8ba-7ca037fd9dc1
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '2029'
ht-degree: 100%

---

# 백업 및 복구할 파일 {#files-to-back-up-and-recover}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

백업해야 하는 애플리케이션 및 데이터 파일은 다음 섹션에 자세히 설명되어 있습니다.

백업 및 복구와 관련하여 다음 사항을 고려하십시오.

* GDS 및 AEM 저장소보다 먼저 데이터베이스를 백업해야 합니다.
* 백업을 위해 클러스터링된 환경에서 노드를 종료해야 하는 경우 보조 노드를 기본 노드보다 먼저 종료해야 합니다. 그렇지 않으면 클러스터나 서버에서 불일치가 발생할 수 있습니다. 또한 기본 노드는 모든 보조 노드보다 먼저 활성화되어야 합니다.
* 클러스터 복원 작업을 수행하려면 클러스터의 각 노드에서 애플리케이션 서버를 중지해야 합니다.

## 전역 문서 스토리지 디렉터리 {#global-document-storage-directory}

GDS는 프로세스 내에서 사용되는 장기 파일을 저장하는 데 사용되는 디렉터리입니다. 장기 파일의 수명은 AEM Forms 시스템을 한 번 이상 실행하는 동안 유지되며, 며칠에서 몇 년까지도 지속될 수 있습니다. 이러한 장기 보관 파일에는 PDF, 정책, 양식 템플릿이 포함될 수 있습니다. 장기 파일은 많은 AEM Forms 배포의 전반적인 상태에서 중요한 부분입니다. 장기 문서 중 일부 또는 전부가 손실되거나 손상되면 Forms 서버가 불안정해질 수 있습니다.

비동기 작업 호출을 위한 입력 문서도 GDS에 저장되며 요청을 처리하는 데 사용할 수 있어야 합니다. 따라서 GDS를 호스팅하는 파일 시스템의 안정성을 고려하고 서비스 품질 및 수준 요구 사항에 적합한 RAID(독립 디스크의 중복 배열)나 기타 기술을 사용하는 것이 중요합니다.

GDS 위치는 AEM Forms 설치 프로세스 도중 또는 나중에 관리 콘솔을 사용하여 결정됩니다. GDS의 고가용성 위치를 유지하는 것 외에도 문서에 대한 데이터베이스 스토리지를 활성화할 수 있습니다. [데이터베이스를 사용하여 문서 저장 시 백업 옵션](files-back-recover.md#backup-options-when-database-is-used-for-document-storage)을 참조하십시오.

### GDS 위치 {#gds-location}

설치 중에 위치 설정을 비워 두면 해당 위치는 기본적으로 애플리케이션 서버 설치 경로 아래의 디렉터리로 설정됩니다. 애플리케이션 서버에 대해 다음 디렉터리를 백업하십시오.

* (JBoss) `[appserver root]/server/'server'/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

GDS 위치를 기본 위치가 아닌 다른 위치로 변경한 경우 다음과 같이 확인할 수 있습니다.

* 관리 콘솔에 로그인하고 설정 > 핵심 시스템 설정 > 구성을 클릭합니다.
* 전역 문서 스토리지 디렉터리 상자에 지정된 위치를 기록합니다.

클러스터링된 환경에서 GDS는 일반적으로 네트워크에서 공유되는 디렉터리를 가리키고 모든 클러스터 노드에서 읽기/쓰기 액세스가 가능합니다.

원래 위치를 더 이상 사용할 수 없는 경우 복구 중에 GDS 위치가 변경될 수 있습니다. ([복구 중 GDS 위치 변경](/help/forms/using/admin-help/recovering-aem-forms-data.md#changing-the-gds-location-during-recovery)을 참조하십시오.)

### 데이터베이스를 사용하여 문서 저장 시 백업 옵션 {#backup-options-when-database-is-used-for-document-storage}

관리 콘솔을 사용하여 AEM Forms 데이터베이스에서 AEM Forms 문서 저장을 활성화할 수 있습니다. 이 옵션을 사용하면 모든 영구 문서가 데이터베이스에 저장되지만, AEM Forms에는 여전히 파일 시스템 기반 GDS 디렉터리가 필요합니다. 해당 디렉터리는 AEM Forms의 세션 및 호출과 관련된 영구 및 임시 파일과 리소스를 저장하는 데 사용되기 때문입니다.

관리 콘솔의 핵심 시스템 설정 또는 구성 관리자를 사용하여 &#39;데이터베이스에 문서 저장 활성화&#39; 옵션을 선택하는 경우 AEM Forms에서는 스냅샷 백업 모드와 롤링 백업 모드를 허용하지 않습니다. 따라서 AEM Forms를 사용하여 백업 모드를 관리할 필요가 없습니다. 이 옵션을 사용하는 경우 옵션을 활성화한 후 GDS를 한 번만 백업해야 합니다. 백업에서 AEM Forms를 복구할 때 GDS의 백업 디렉터리 이름을 바꾸거나 GDS를 복원할 필요가 없습니다.

## AEM 저장소 {#aem-repository}

AEM Forms를 설치하는 동안 crx-repository가 구성되면 AEM 저장소(crx-repository)가 생성됩니다. crx-repository 디렉터리의 위치는 AEM Forms 설치 프로세스 중에 결정됩니다. AEM Forms에서 AEM Forms 데이터의 일관성을 유지하기 위해서는 데이터베이스 및 GDS와 함께 AEM 저장소 백업 및 복원이 필요합니다. AEM 저장소에는 서신 관리 솔루션, Forms Manager 및 AEM Forms Workspace에 대한 데이터가 포함되어 있습니다.

### 서신 관리 솔루션 {#correspondence-management-solution}

서신 관리 솔루션은 안전하고 개인화된 대화형 서신의 생성, 어셈블리 및 전달을 중앙 집중화하고 관리합니다. 이 솔루션을 사용하면 미리 승인된 콘텐츠와 사용자 정의 작성된 콘텐츠 모두에서 서신을 신속하게 어셈블하여 생성부터 보관까지 간소화된 프로세스를 거칠 수 있습니다. 결과적으로 고객은 시기적절하고 정확하며 편리하고 안전하며 관련성 높은 커뮤니케이션을 받을 수 있습니다. 비즈니스 측면에서는 용이성, 속도, 생산성을 위해 간소화된 프로세스를 통해 고객 상호 작용의 가치를 극대화하고 비용과 위험을 최소화합니다.

간단한 서신 관리 솔루션 설정에는 동일한 컴퓨터 또는 다른 컴퓨터에 작성자 인스턴스와 게시 인스턴스가 포함됩니다.

### Forms Manager {#forms-manager}

Forms Manager는 양식을 업데이트하고 관리하며 사용 중지하는 프로세스를 간소화합니다.

### AEM Forms Workspace {#html-workspace}

AEM Forms Workspace는 Flex Workspace(JEE의 AEM Forms에서는 더 이상 사용되지 않음)의 기능과 일치하며 Workspace를 확장하고 통합하여 더욱 사용자 친화적으로 만드는 새로운 기능을 추가합니다.

>[!NOTE]
>
>Flex Workspace는 AEM Forms 릴리스에서 더 이상 사용되지 않습니다.

AEM Forms Workspace를 사용하면 Flash Player와 Adobe Reader가 없는 클라이언트에서도 작업을 관리할 수 있습니다. PDF 양식과 Flex 양식뿐 아니라 HTML 양식의 렌디션도 쉽게 처리할 수 있습니다.

## AEM Forms 데이터베이스 {#aem-forms-database}

AEM Forms 데이터베이스는 양식 아티팩트, 서비스 구성, 프로세스 상태, GDS 및 콘텐츠 스토리지 루트 디렉터리(콘텐츠 서비스용)에 있는 파일에 대한 데이터베이스 참조와 같은 콘텐츠를 저장합니다. 데이터베이스 백업은 서비스 중단 없이 실시간으로 수행할 수 있으며 복구는 특정 시점이나 특정 변경 사항으로 수행할 수 있습니다. 이 섹션에서는 실시간으로 백업할 수 있도록 데이터베이스를 구성하는 방법을 설명합니다.

적절하게 구성된 AEM Forms 시스템에서는 시스템 관리자와 데이터베이스 관리자가 쉽게 공동 작업하여 시스템을 일관되고 알려진 상태로 복구할 수 있습니다.

실시간으로 데이터베이스를 백업하려면 스냅샷 모드를 사용하거나 데이터베이스가 지정된 로그 모드에서 실행되도록 구성해야 합니다. 이렇게 하면 데이터베이스가 열려 있고 사용 가능한 상태에서 데이터베이스 파일을 백업할 수 있습니다. 또한 데이터베이스는 해당 모드에서 실행 중일 때 롤백 및 트랜잭션 로그를 보존합니다.

>[!NOTE]
>
>Adobe® LiveCycle® Content Services ES(더 이상 사용되지 않음)는 LiveCycle과 함께 설치되는 콘텐츠 관리 시스템입니다. 이를 통해 사용자는 인간 중심 프로세스를 설계, 관리, 모니터링 및 최적화할 수 있습니다. 콘텐츠 서비스(더 이상 사용되지 않음)는 2014년 12월 31일에 지원이 종료되었습니다. [Adobe 제품 수명 주기 문서](https://www.adobe.com/kr/support/products/enterprise/eol/eol_matrix.html)를 참조하십시오.

### DB2 {#db2}

DB2 데이터베이스가 아카이브 로그 모드에서 실행되도록 구성합니다.

>[!NOTE]
>
>AEM Forms 환경이 이전 버전의 AEM Forms에서 업그레이드되었고 DB2를 사용하는 경우 온라인 백업은 지원되지 않습니다. 이 경우 AEM Forms를 종료하고 오프라인 백업을 수행해야 합니다. AEM Forms의 향후 버전에서는 업그레이드 고객을 위한 온라인 백업을 지원할 예정입니다.

IBM은 데이터베이스 관리자가 백업 및 복구 작업을 관리하는 데 도움이 되는 도구와 도움말 시스템을 제공합니다.

* IBM DB2 아카이브 로그 가속기
* IBM DB2 데이터 아카이브 전문가

DB2에는 Tivoli Storage Manager에 데이터베이스를 백업하는 기본 제공 기능이 포함되어 있습니다. Tivoli Storage Manager를 사용하면 DB2 백업을 다른 미디어나 로컬 하드 드라이브에 저장할 수 있습니다.

### Oracle {#oracle}

스냅샷 백업을 사용하거나 Oracle 데이터베이스가 아카이브 로그 모드에서 실행되도록 구성합니다. ([Oracle 백업: 소개](https://www.databasedesign-resource.com/oracle-backup.md)를 참조하십시오.) Oracle 데이터베이스 백업 및 복구에 대한 자세한 내용은 다음 사이트를 참조하십시오.

[Oracle 백업 및 복구:](https://www.oracle.com/technetwork/database/features/availability/br-overview-097160.html) 백업 및 복구 개념과 백업, 복구 및 보고를 위해 RMAN(Recovery Manager)을 사용하는 가장 일반적인 기술을 자세히 설명하고 백업 및 복구 전략을 계획하는 방법에 대한 자세한 정보를 제공합니다.

[Oracle 데이터베이스 백업 및 복구 사용자 안내서:](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10642.pdf) RMAN 아키텍처, 백업 및 복구 개념과 메커니즘, 특정 시점 복구 및 데이터베이스 플래시백 기능과 같은 고급 복구 기술, 백업 및 복구 성능 조정에 대한 심층적인 정보를 제공합니다. RMAN 대신 호스트 운영 체제 기능을 사용한 사용자 관리 백업 및 복구도 포함됩니다. 이 안내서는 보다 정교한 데이터베이스 배포의 백업 및 복구와 고급 복구 시나리오에 필수적입니다.

[Oracle 데이터베이스 백업 및 복구 참조:](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10643.pdf) 모든 RMAN 명령의 구문과 의미에 대한 완전한 정보를 제공하고 백업 및 복구 활동 보고에 사용할 수 있는 데이터베이스 보기를 설명합니다.

### SQL 서버 {#sql-server}

스냅샷 백업을 사용하거나 SQL Server 데이터베이스가 트랜잭션 로그 모드에서 실행되도록 구성합니다.

SQL Server는 두 가지 백업 및 복구 도구도 제공합니다.

* SQL Server Management Studio(GUI)
* T-SQL(명령줄)

자세한 내용은 [백업 및 복원](https://msdn.microsoft.com/en-us/library/ms187048(v=SQL.90).aspx)을 참조하십시오.

### MySQL {#mysql}

MySQLAdmin을 사용하거나 Windows의 INI 파일을 수정하여 MySQL 데이터베이스가 이진 로그 모드에서 실행되도록 구성합니다. ([MySQL 이진 로깅](https://dev.mysql.com/doc/refman/5.1/en/binary-log.html)을 참조하십시오. ) InnoBase 소프트웨어에서 MySQL용 핫 백업 도구도 사용할 수 있습니다. ([Innobase 핫 백업](https://www.innodb.com/hot-backup/features.md)을 참조하십시오.)

>[!NOTE]
>
>MySQL의 기본 이진 로깅 모드는 &#39;문&#39;이며 이 문은 콘텐츠 서비스(더 이상 사용되지 않음)에서 사용하는 테이블과 호환되지 않습니다. 이 기본 모드에서 이진 로깅을 사용하면 콘텐츠 서비스(더 이상 사용되지 않음)가 실패합니다. 시스템에 콘텐츠 서비스(더 이상 사용되지 않음)가 포함되어 있는 경우 &#39;혼합&#39; 로깅 모드를 사용하십시오. &#39;혼합&#39; 로깅을 활성화하려면 my.ini 파일에 다음 인수를 추가합니다. `binlog_format=mixed log-bin=logname`

Mysqldump 유틸리티를 사용하면 전체 데이터베이스 백업을 얻을 수 있습니다. 전체 백업이 필요하지만 항상 편리한 것은 아닙니다. 생성되는 백업 파일이 크고 생성하는 데 시간이 걸립니다. 증분 백업을 수행하려면 이전 섹션에서 설명한 대로 - `log-bin` 옵션을 사용하여 서버를 시작해야 합니다. MySQL 서버가 다시 시작될 때마다 현재 이진 로그에 쓰는 것을 중지하고 새 이진 로그를 만듭니다. 그러면 새 이진 로그가 현재 이진 로그가 됩니다. `FLUSH LOGS SQL` 명령을 사용하여 수동으로 강제 전환할 수 있습니다. 첫 번째 전체 백업 후 후속 증분 백업은 mysqladmin 유틸리티의 `flush-logs` 명령을 사용하여 수행되며, 이 명령은 다음 로그 파일을 생성합니다.

[백업 전략 요약](https://dev.mysql.com/doc/refman/5.5/en/backup-strategy-summary.html)을 참조하십시오.

```text
binlog_format=mixed
log-bin=logname
```

## 콘텐츠 스토리지 루트 디렉터리(콘텐츠 서비스 전용) {#content-storage-root-directory-content-services-only}

콘텐츠 스토리지 루트 디렉터리에는 모든 문서, 아티팩트 및 색인이 저장되는 콘텐츠 서비스(더 이상 사용되지 않음) 저장소가 포함되어 있습니다. 콘텐츠 스토리지 루트 디렉터리 트리를 백업해야 합니다. 이 섹션에서는 독립 실행형 환경과 클러스터링된 환경 모두에서 콘텐츠 스토리지 루트 디렉터리의 위치를 확인하는 방법을 설명합니다.

### 콘텐츠 스토리지 루트 위치(독립 실행형 환경) {#content-storage-root-location-stand-alone-environment}

콘텐츠 서비스(더 이상 사용되지 않음)가 설치되면 콘텐츠 스토리지 루트 디렉터리가 생성됩니다. 콘텐츠 스토리지 루트 디렉터리의 위치는 AEM Forms 설치 프로세스 중에 결정됩니다.

콘텐츠 스토리지 루트 디렉터리의 기본 위치는 `[aem-forms root]/lccs_data`입니다.

콘텐츠 스토리지 루트 디렉터리에서 다음 디렉터리를 백업하십시오.

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

/backup-lucene-indexes 디렉터리가 없으면 콘텐츠 스토리지 루트 디렉터리에 있는 /lucene-indexes 디렉터리도 백업합니다. /backup-lucene-indexes 디렉터리가 있는 경우에는 오류가 발생할 수 있으므로 /lucene-indexes 디렉터리를 백업하지 마십시오.

### 콘텐츠 스토리지 루트 위치(클러스터링된 환경) {#content-storage-root-location-clustered-environment}

클러스터링된 환경에 콘텐츠 서비스(더 이상 사용되지 않음)를 설치하면 콘텐츠 스토리지 루트 디렉터리가 두 개의 별도 디렉터리로 분할됩니다.

**콘텐츠 스토리지 루트 디렉터리:** 일반적으로 클러스터의 모든 노드에서 읽기/쓰기 액세스가 가능한 공유 네트워크 디렉터리입니다.

**색인 루트 디렉터리:** 클러스터의 각 노드에 생성되는 디렉터리로, 경로 및 디렉터리 이름이 항상 동일합니다.

콘텐츠 스토리지 루트 디렉터리의 기본 위치는 `[GDS root]/lccs_data`입니다. 여기서 `[GDS root]`는 [GDS 위치](files-back-recover.md#gds-location)에 설명된 위치입니다. 콘텐츠 스토리지 루트 디렉터리에서 다음 디렉터리를 백업하십시오.

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

/backup-lucene-indexes 디렉터리가 없으면 콘텐츠 스토리지 루트 디렉터리에 있는 /lucene-indexes 디렉터리도 백업합니다. /backup-lucene-indexes 디렉터리가 있는 경우에는 오류가 발생할 수 있으므로 /lucene-indexes 디렉터리를 백업하지 마십시오.

색인 루트 디렉터리의 기본 위치는 각 노드의 `[aem-forms root]/lucene-indexes`입니다.

## 고객이 설치한 글꼴 {#customer-installed-fonts}

AEM Forms 환경에 추가 글꼴을 설치한 경우 해당 글꼴을 별도로 백업해야 합니다. 관리 콘솔의 설정 > 핵심 시스템 > 구성에서 지정된 모든 Adobe 및 고객 글꼴 디렉터리를 백업합니다. 글꼴 디렉터리 전체를 백업하십시오.

>[!NOTE]
>
>기본적으로 AEM Forms와 함께 설치된 Adobe 글꼴은 `[aem-forms root]/fonts` 디렉터리에 있습니다.

호스트 컴퓨터에서 운영 체제를 다시 초기화하고 이전 운영 체제의 글꼴을 사용하려는 경우 시스템 글꼴 디렉터리의 콘텐츠도 백업해야 합니다. (구체적인 지침은 해당 운영 체제의 설명서를 참조하십시오.)
