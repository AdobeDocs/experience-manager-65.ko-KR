---
title: 백업 및 복구할 파일
seo-title: 백업 및 복구할 파일
description: 이 문서에서는 백업해야 하는 응용 프로그램 및 데이터 파일에 대해 설명합니다.
seo-description: 이 문서에서는 백업해야 하는 응용 프로그램 및 데이터 파일에 대해 설명합니다.
uuid: ba04adb9-675a-48f2-ad52-39c1266e423b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6f9a294d-24bd-4e4b-b929-2809f5e6cef9
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '2187'
ht-degree: 0%

---


# 백업 및 복구할 파일 {#files-to-back-up-and-recover}

백업해야 하는 응용 프로그램 및 데이터 파일은 다음 섹션에서 자세히 설명합니다.

백업 및 복구와 관련하여 다음 사항을 고려합니다.

* 데이터베이스는 GDS 및 AEM 저장소 앞에 백업해야 합니다.
* 백업을 위해 클러스터된 환경에서 노드를 종료해야 하는 경우 보조 노드가 기본 노드 앞에 종료되었는지 확인합니다. 그렇지 않으면 클러스터 또는 서버에서 불일치가 발생할 수 있습니다. 또한 보조 노드 이전에 기본 노드를 라이브로 설정해야 합니다.
* 클러스터의 복원 작업을 수행하려면 클러스터의 각 노드에 대해 응용 프로그램 서버를 중지해야 합니다.

## 전역 문서 저장소 디렉터리 {#global-document-storage-directory}

GDS는 프로세스 내에서 사용되는 긴 수명 파일을 저장하는 데 사용되는 디렉토리입니다. 긴 수명 파일의 수명은 AEM 양식 시스템을 하나 이상 실행할 수 있도록 고안된 것으로, 여러 날, 심지어 여러 해 동안 작업할 수 있습니다. 이러한 오래 지속되는 파일에는 PDF, 정책 및 양식 템플릿이 포함될 수 있습니다. 긴 기간 파일은 많은 AEM 양식 배포의 전반적인 상태에 있어 매우 중요한 부분입니다. 긴 문서의 일부 또는 전체가 손실되거나 손상되면 양식 서버가 불안정해질 수 있습니다.

비동기 작업 호출을 위한 입력 문서는 GDS에도 저장되므로 요청을 처리하는 데 사용할 수 있어야 합니다. 따라서 GDS를 호스팅하고 RAID(Independent Disks Array) 또는 기타 기술을 사용하는 파일 시스템의 신뢰성을 서비스 품질과 수준에 맞게 고려하는 것이 중요합니다.

GDS의 위치는 AEM 양식 설치 프로세스 동안 또는 관리 콘솔을 사용하여 결정합니다. GDS의 고가용성 위치를 유지하는 것 외에도 문서의 데이터베이스 저장소를 활성화할 수 있습니다. 문서 저장소](files-back-recover.md#backup-options-when-database-is-used-for-document-storage)에 데이터베이스가 사용되는 경우 [백업 옵션을 참조하십시오.

### GDS 위치 {#gds-location}

설치 중에 위치 설정을 비워 두면 응용 프로그램 서버 설치 아래의 디렉토리가 기본 위치에 설정됩니다. 응용 프로그램 서버에 대해 다음 디렉토리를 백업해야 합니다.

* (JBoss) `[appserver root]/server/'server'/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

GDS 위치를 기본값이 아닌 위치로 변경한 경우 다음과 같이 결정할 수 있습니다.

* 관리 콘솔에 로그인하고 설정 > 핵심 시스템 설정 > 구성을 클릭합니다.
* 전역 문서 저장소 디렉토리 상자에 지정된 위치를 기록합니다.

클러스터된 환경에서 GDS는 일반적으로 네트워크에서 공유되고 모든 클러스터 노드에 대해 읽기/쓰기 액세스 가능한 디렉토리를 가리킵니다.

원래 위치를 더 이상 사용할 수 없는 경우 복구 중에 GDS 위치를 변경할 수 있습니다. (복구 중 [GDS 위치 변경](/help/forms/using/admin-help/recovering-aem-forms-data.md#changing-the-gds-location-during-recovery)을 참조하십시오.)

### 문서 저장소 {#backup-options-when-database-is-used-for-document-storage}에 데이터베이스를 사용하는 경우 백업 옵션

관리 콘솔을 사용하여 AEM 양식 데이터베이스에서 AEM 양식 문서 저장소를 활성화할 수 있습니다. 이 옵션을 사용하면 모든 영구 문서를 데이터베이스에 저장할 수 있지만 AEM 양식은 세션 및 AEM 양식 호출과 관련된 영구 파일 및 임시 파일과 리소스를 저장하는 데 사용되므로 여전히 파일 시스템 기반 GDS 디렉토리가 필요합니다.

관리 콘솔의 핵심 시스템 설정에서 &quot;데이터베이스에서 문서 저장소 사용&quot; 옵션을 선택하거나 Configuration Manager를 사용하여 AEM 양식에서 스냅샷 백업 모드 및 순환 백업 모드를 허용하지 않습니다. 따라서 AEM 양식을 사용하여 백업 모드를 관리할 필요가 없습니다. 이 옵션을 사용하는 경우 옵션을 활성화한 후 GDS를 한 번만 백업해야 합니다. 백업에서 AEM 양식을 복구할 때 GDS에 대한 백업 디렉토리의 이름을 변경하거나 GDS를 복원할 필요가 없습니다.

## AEM 저장소 {#aem-repository}

AEM 저장소(crx-repository)는 AEM 양식을 설치하는 동안 crx-repository가 구성된 경우 생성됩니다. crx-repository 디렉토리의 위치는 AEM 양식 설치 과정에서 결정됩니다. AEM 양식의 AEM 양식 데이터를 일관되게 유지하기 위해 데이터베이스 및 GDS와 함께 AEM 저장소 백업 및 복원이 필요합니다. AEM 저장소에는 Correspondence Management Solution, Forms 관리자 및 AEM Forms Workspace에 대한 데이터가 포함되어 있습니다.

### 통신 관리 솔루션 {#correspondence-management-solution}

Correspondence Management Solution은 안전하고 개인화된 인터랙티브한 통신의 제작, 수집 및 전달을 중앙 집중화하여 관리합니다. 이를 통해 사전 승인된 컨텐츠와 사용자 정의 작성 컨텐츠의 응답을 작성에서부터 보관에 이르는 간소화된 프로세스로 신속하게 취합할 수 있습니다. 따라서 고객은 적시에 정확하고 편리하며 안전하고 연관성 있는 커뮤니케이션을 수행할 수 있습니다. 간편함, 속도 및 생산성을 높여주는 프로세스를 통해 기업은 고객과의 상호 작용의 가치를 극대화하고 비용과 위험을 최소화할 수 있습니다.

단순 통신 관리 솔루션 설정에는 작성자 인스턴스와 게시 인스턴스가 동일한 컴퓨터 또는 다른 컴퓨터에 포함됩니다

### 양식 관리자 {#forms-manager}

양식 관리자가 양식을 업데이트하고, 관리하고, 삭제하는 과정을 간소화합니다.

### AEM Forms 작업 영역 {#html-workspace}

AEM Forms Workspace는 Flex Workspace의 기능(JEE에서 AEM 양식에 대해 더 이상 사용되지 않음)과 일치시키고 새로운 기능을 추가하여 Workspace를 확장 및 통합하며 보다 사용자에게 친숙한 컨텐츠를 만들 수 있습니다.

>[!NOTE]
>
>Flex Workflow는 AEM Forms 릴리스에서 더 이상 사용되지 않습니다.

Flash Player 및 Adobe Reader 없이도 클라이언트의 작업 관리를 수행할 수 있습니다. PDF forms 및 Flex 양식 외에도 HTML Forms 변환이 용이해집니다.

## AEM 양식 데이터베이스 {#aem-forms-database}

AEM 양식 데이터베이스는 양식 객체, 서비스 구성, 프로세스 상태 및 데이터베이스 참조와 같은 컨텐츠를 GDS 및 컨텐츠 저장소 루트 디렉토리(컨텐츠 서비스용)에 있는 파일에 저장합니다. 데이터베이스 백업은 서비스 중단 없이 실시간으로 수행할 수 있으며 특정 시점 또는 특정 변경 사항까지 복구할 수 있습니다. 이 섹션에서는 실시간으로 백업할 수 있도록 데이터베이스를 구성하는 방법에 대해 설명합니다.

올바르게 구성된 AEM 양식 시스템에서 시스템 관리자와 데이터베이스 관리자는 시스템을 일관되고 알려진 상태로 복구하기 위해 손쉽게 협업할 수 있습니다.

실시간으로 데이터베이스를 백업하려면 스냅샷 모드를 사용하거나 지정된 로그 모드에서 실행되도록 데이터베이스를 구성해야 합니다. 이렇게 하면 데이터베이스가 열려 있고 사용할 수 있는 동안 데이터베이스 파일을 백업할 수 있습니다. 또한 이 모드에서 실행 중인 데이터베이스는 롤백 및 트랜잭션 로그를 유지합니다.

>[!NOTE]
>
>Adobe® LiveCycle® Content Services ES(더 이상 사용되지 않음)는 LiveCycle과 함께 설치되는 컨텐츠 관리 시스템입니다. 인간 중심 프로세스를 디자인, 관리, 모니터링 및 최적화할 수 있습니다. 콘텐츠 서비스(더 이상 사용되지 않음) 지원은 12/31/2014에 종료됩니다. [Adobe 제품 라이프사이클 문서](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html)를 참조하십시오. 콘텐츠 서비스 구성에 대해 알아보려면 [콘텐츠 서비스 관리](https://help.adobe.com/en_US/livecycle/9.0/admin_contentservices.pdf)를 참조하십시오.

### DB2 {#db2}

보관 로그 모드에서 실행되도록 DB2 데이터베이스를 구성합니다.

>[!NOTE]
>
>AEM 양식 환경이 이전 버전의 AEM 양식에서 업그레이드되어 DB2를 사용하는 경우 온라인 백업이 지원되지 않습니다. 이 경우 AEM 양식을 종료하고 오프라인 백업을 수행해야 합니다. AEM 양식의 향후 버전은 업그레이드 고객을 위한 온라인 백업을 지원합니다.

IBM에는 데이터베이스 관리자가 백업 및 복구 작업을 관리하는 데 도움이 되는 도구 및 도움말 시스템이 있습니다.

* IBM DB2 아카이브 로그 가속기(z/OS용 [IBM DB2 아카이브 로그 가속기 사용 설명서](https://publib.boulder.ibm.com/infocenter/dzichelp/v2r2/topic/com.ibm.db2tools.alc.doc.ug/alcugb20.pdf?noframes=true) 참조)
* IBM DB2 데이터 아카이브 전문가([IBM DB2 Data Archive Expert 사용 안내서 및 참조](https://publib.boulder.ibm.com/infocenter/mptoolic/v1r0/topic/com.ibm.db2tools.aeu.doc.ug/ahxugb13.pdf?noframes=true) 참조)

DB2에는 데이터베이스를 Tivoli Storage Manager에 백업하는 기능이 내장되어 있습니다. Tivoli Storage Manager를 사용하여 DB2 백업을 다른 미디어 또는 로컬 하드 드라이브에 저장할 수 있습니다.

DB2 데이터베이스 백업 및 복구에 대한 자세한 내용은 [DB2](https://publib.boulder.ibm.com/infocenter/db2luw/v9/index.jsp?topic=/com.ibm.db2.udb.admin.doc/doc/c0005945.htm)에 대한 백업 및 복구 전략 개발을 참조하십시오.

### Oracle {#oracle}

스냅샷 백업을 사용하거나 Oracle 데이터베이스를 구성하여 아카이브 로그 모드로 실행합니다. ( [Oracle 백업 참조:소개](https://www.databasedesign-resource.com/oracle-backup.md).) oracle 데이터베이스 백업 및 복구에 대한 자세한 내용은 다음 사이트를 참조하십시오.

[Oracle 백업 및 복구: 백업 및 복구의 개념과 백업, 복구 및 보고를 위해 RMAN(Recovery Manager)을 사용하는 가장 일반적인 기법과 백업 및 복구 전략을 계획하는 방법에 대한 자세한 정보를 ](https://www.oracle.com/technetwork/database/features/availability/br-overview-097160.html) 제공합니다.

[Oracle 데이터베이스 백업 및 복구 사용자 안내서: RMAN 아키텍처, 백업 및 복구 개념 및 메커니즘에 대한 자세한 정보, ](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10642.pdf) 시점 복구 및 데이터베이스 플래시백 기능과 같은 고급 복구 기술, 백업 및 복구 성능 조정에 대한 자세한 정보를 제공합니다. 또한 RMAN 대신 호스트 운영 체제 시설을 사용하여 사용자 관리 백업 및 복구를 다룹니다. 이 볼륨은 보다 정교한 데이터베이스 배포의 백업 및 복구와 고급 복구 시나리오에서 필요로 합니다.

[Oracle 데이터베이스 백업 및 복구 참조:](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10643.pdf) 모든 RMAN 명령에 대한 구문 및 의미에 대한 자세한 정보를 제공하고 백업 및 복구 작업에 대해 보고하는 데 사용할 수 있는 데이터베이스 뷰를 설명합니다.

### SQL Server {#sql-server}

스냅샷 백업을 사용하거나 트랜잭션 로그 모드에서 실행되도록 SQL Server 데이터베이스를 구성합니다.

SQL Server는 다음과 같은 두 가지 백업 및 복구 도구를 제공합니다.

* SQL Server Management Studio(GUI)
* T-SQL(명령줄)

자세한 내용은 [백업 및 복원](https://msdn.microsoft.com/en-us/library/ms187048(v=SQL.90).aspx)을 참조하십시오.

### MySQL {#mysql}

MySQLAdmin을 사용하거나 Windows에서 INI 파일을 수정하여 이진 로그 모드에서 실행되도록 MySQL 데이터베이스를 구성합니다. ([MySQL 이진 로깅](https://dev.mysql.com/doc/refman/5.1/en/binary-log.html)을 참조하십시오.) MySQL용 핫 백업 도구는 InnoBase 소프트웨어에서도 사용할 수 있습니다. ([기본 핫 백업](https://www.innodb.com/hot-backup/features.md)을 참조하십시오.)

>[!NOTE]
>
>MySQL의 기본 이진 로깅 모드는 콘텐츠 서비스에서 사용하는 테이블과 호환되지 않는 &quot;문&quot;입니다(더 이상 사용되지 않음). 이 기본 모드에서 이진 로깅을 사용하면 컨텐츠 서비스(더 이상 사용되지 않음)가 실패합니다. 시스템에 컨텐츠 서비스(더 이상 사용되지 않음)가 포함되어 있는 경우 &quot;혼합&quot; 로깅 모드를 사용하십시오. &quot;혼합&quot; 로깅을 사용하려면 my.ini 파일에 다음 인수를 추가하십시오.`binlog_format=mixed log-bin=logname`

myqldump 유틸리티를 사용하여 전체 데이터베이스 백업을 얻을 수 있습니다. 전체 백업이 필요하지만 항상 편리하지는 않습니다. 대용량 백업 파일을 생성하고 생성하는 데 시간이 걸립니다. 증분 백업을 수행하려면 이전 섹션에 설명된 대로 - `log-bin` 옵션으로 서버를 시작해야 합니다. MySQL Server가 다시 시작될 때마다 현재 이진 로그에 대한 쓰기가 정지되고 새 이진 로그가 생성되며 이후 새 서버가 현재 로그가 됩니다. `FLUSH LOGS SQL` 명령을 사용하여 수동으로 스위치를 강제 적용할 수 있습니다. 첫 번째 전체 백업 후 다음 로그 파일을 만드는 `flush-logs` 명령과 함께 myqladmin 유틸리티를 사용하여 후속 증분 백업이 수행됩니다.

[백업 전략 요약](https://dev.mysql.com/doc/refman/5.5/en/backup-strategy-summary.html)을 참조하십시오.

```text
binlog_format=mixed
log-bin=logname
```

## 콘텐츠 저장소 루트 디렉터리(콘텐츠 서비스만 해당) {#content-storage-root-directory-content-services-only}

컨텐츠 저장소 루트 디렉토리에는 모든 문서, 객체 및 인덱스가 저장되는 컨텐츠 서비스(더 이상 사용되지 않음) 저장소가 포함되어 있습니다. 콘텐츠 저장소 루트 디렉터리 트리를 백업해야 합니다. 이 섹션에서는 독립형 환경과 클러스터된 환경 모두에 대한 컨텐츠 저장소 루트 디렉토리의 위치를 결정하는 방법에 대해 설명합니다.

### 컨텐츠 저장소 루트 위치(독립 실행형 환경) {#content-storage-root-location-stand-alone-environment}

콘텐츠 서비스(더 이상 사용되지 않음)가 설치되면 콘텐츠 저장소 루트 디렉토리가 만들어집니다. 컨텐츠 저장소 루트 디렉토리의 위치는 AEM 양식 설치 프로세스 중에 결정됩니다.

콘텐츠 저장소 루트 디렉토리의 기본 위치는 `[aem-forms root]/lccs_data`입니다.

콘텐트 저장소 루트 디렉토리에 있는 다음 디렉토리를 백업합니다.

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

/backup-lucene-indexes 디렉토리가 없는 경우 /lucene-indexes 디렉토리를 백업합니다. 이 디렉토리는 컨텐츠 저장소 루트 디렉토리에도 있습니다. /backup-lucene-indexes 디렉토리가 있는 경우 오류가 발생할 수 있으므로 /lucene-indexes 디렉토리를 백업하지 마십시오.

### 콘텐트 저장소 루트 위치(클러스터된 환경) {#content-storage-root-location-clustered-environment}

클러스터된 환경에서 Content Services(더 이상 사용되지 않음)를 설치하면 Content Storage Root 디렉토리는 두 개의 개별 디렉터리로 분할됩니다.

**컨텐츠 저장소 루트 디렉토리:** 일반적으로 클러스터의 모든 노드에 대해 읽기/쓰기 액세스 가능한 공유 네트워크 디렉토리입니다.

**인덱스 루트 디렉토리:** 클러스터의 각 노드에 항상 동일한 경로와 디렉토리 이름을 갖는 디렉토리

컨텐트 저장소 루트 디렉토리의 기본 위치는 `[GDS root]/lccs_data`이며, 여기서 `[GDS root]`은 [GDS 위치](files-back-recover.md#gds-location)에 설명된 위치입니다. 콘텐트 저장소 루트 디렉토리에 있는 다음 디렉토리를 백업합니다.

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

/backup-lucene-indexes 디렉토리가 없는 경우 /lucene-indexes 디렉토리를 백업합니다. 이 디렉토리는 컨텐츠 저장소 루트 디렉토리에도 있습니다. /backup-lucene-indexes 디렉토리가 있는 경우 오류가 발생할 수 있으므로 /lucene-indexes 디렉토리를 백업하지 마십시오.

인덱스 루트 디렉토리의 기본 위치는 각 노드에서 `[aem-forms root]/lucene-indexes`입니다.

## 고객이 설치한 글꼴 {#customer-installed-fonts}

AEM 양식 환경에 추가 글꼴을 설치한 경우 별도로 글꼴을 백업해야 합니다. 설정 > 핵심 시스템 > 구성에서 관리 콘솔에 지정된 모든 Adobe 및 고객 글꼴 디렉토리를 백업합니다. 전체 글꼴 디렉토리를 백업해야 합니다.

>[!NOTE]
>
>기본적으로 AEM 양식에 설치된 Adobe 글꼴은 `[aem-forms root]/fonts` 디렉토리에 있습니다.

호스트 컴퓨터에서 운영 체제를 다시 초기화하여 이전 운영 체제의 글꼴을 사용하려면 시스템 글꼴 디렉토리의 컨텐츠도 백업해야 합니다. (특정 지침은 운영 체제에 대한 설명서를 참조하십시오).
