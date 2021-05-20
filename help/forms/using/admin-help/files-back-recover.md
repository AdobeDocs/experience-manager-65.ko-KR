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
exl-id: d2dd381d-a7d2-4fec-a8ba-7ca037fd9dc1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2187'
ht-degree: 0%

---

# 백업 및 복구할 파일 {#files-to-back-up-and-recover}

백업해야 하는 응용 프로그램 및 데이터 파일은 다음 섹션에서 자세히 설명합니다.

백업 및 복구에 대해 다음 사항을 고려하십시오.

* GDS 및 AEM 저장소 전에 데이터베이스를 백업해야 합니다.
* 백업을 위해 클러스터형 환경의 노드를 종료해야 하는 경우 주 노드가 종료되기 전에 보조 노드가 종료되었는지 확인하십시오. 그렇지 않으면 클러스터 또는 서버에서 불일치가 발생할 수 있습니다. 또한, 주 노드는 보조 노드 앞에 라이브로 설정되어야 합니다.
* 클러스터의 복원 작업을 수행하려면 클러스터의 각 노드에 대해 응용 프로그램 서버를 중지해야 합니다.

## 글로벌 문서 저장소 디렉토리 {#global-document-storage-directory}

GDS는 프로세스 내에서 사용되는 오래 지속되는 파일을 저장하는 데 사용되는 디렉토리입니다. 긴 기간 파일의 수명은 AEM Forms 시스템을 하나 이상 실행하기 위한 것으로, 일 수 및 여러 해에 걸쳐 있을 수 있습니다. 이러한 긴 기간 파일에는 PDF, 정책 및 양식 템플릿이 포함될 수 있습니다. 긴 기간 파일은 많은 AEM forms 배포의 전체 상태에 중요한 부분입니다. 일부 또는 모든 장기간 문서가 손실되거나 손상된 경우 Forms 서버가 불안정해질 수 있습니다.

비동기 작업 호출을 위한 입력 문서는 GDS에도 저장되며 요청을 처리하는 데 사용할 수 있어야 합니다. 따라서 GDS를 호스팅하고 RAID(Redundant Array of Independent Disks) 또는 기타 기술을 사용하는 파일 시스템의 신뢰성을 서비스 품질 및 수준에 맞게 고려하는 것이 중요합니다.

GDS의 위치는 AEM Forms 설치 프로세스 동안 또는 나중에 관리 콘솔을 사용하여 결정됩니다. GDS의 고가용성 위치를 유지할 뿐만 아니라 문서에 대한 데이터베이스 저장소를 활성화할 수도 있습니다. 문서 저장소에 데이터베이스가 사용되는 경우 [백업 옵션](files-back-recover.md#backup-options-when-database-is-used-for-document-storage)을 참조하십시오.

### GDS 위치 {#gds-location}

설치 중에 위치 설정을 비워 두면 기본값은 응용 프로그램 서버 설치 아래의 디렉터리로 설정됩니다. 애플리케이션 서버에 대해 다음 디렉토리를 백업해야 합니다.

* (JBoss) `[appserver root]/server/'server'/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

GDS 위치를 기본값이 아닌 위치로 변경한 경우 다음과 같이 결정할 수 있습니다.

* 관리 콘솔에 로그인하고 설정 > 핵심 시스템 설정 > 구성을 클릭합니다.
* 글로벌 문서 저장 디렉토리 상자에 지정된 위치를 기록합니다.

클러스터된 환경에서 GDS는 일반적으로 네트워크에서 공유되고 모든 클러스터 노드에 대해 읽기/쓰기 액세스 가능한 디렉토리를 가리킵니다.

원래 위치를 더 이상 사용할 수 없는 경우 복구 중에 GDS 위치를 변경할 수 있습니다. (](/help/forms/using/admin-help/recovering-aem-forms-data.md#changing-the-gds-location-during-recovery) 복구 중 GDS 위치 변경 을 참조하십시오.)[

### 문서 저장 영역 {#backup-options-when-database-is-used-for-document-storage}에 데이터베이스를 사용하는 경우 백업 옵션

관리 콘솔을 사용하여 AEM Forms 데이터베이스에서 AEM Forms 문서 저장소를 활성화할 수 있습니다. 이 옵션은 모든 영구 문서를 데이터베이스에 보관하지만 AEM Forms는 AEM Forms의 세션 및 호출과 관련된 영구 파일 및 임시 파일과 리소스를 저장하는 데 사용되므로 파일 시스템 기반 GDS 디렉토리가 필요합니다.

관리 콘솔의 핵심 시스템 설정에서 &quot;데이터베이스에서 문서 저장 영역 활성화&quot; 옵션을 선택하거나 구성 관리자를 사용하여 선택하면 AEM Forms에서 스냅샷 백업 모드 및 롤링 백업 모드를 허용하지 않습니다. 따라서 AEM Forms를 사용하여 백업 모드를 관리할 필요가 없습니다. 이 옵션을 사용하는 경우 옵션을 활성화한 후 GDS를 한 번만 백업해야 합니다. 백업에서 AEM Forms를 복구하는 경우 GDS에 대한 백업 디렉토리의 이름을 바꾸거나 GDS를 복원할 필요가 없습니다.

## AEM 저장소 {#aem-repository}

AEM Forms를 설치하는 동안 crx-repository가 구성된 경우 AEM 저장소(crx-repository)가 생성됩니다. crx-repository 디렉토리의 위치는 AEM Forms 설치 프로세스 중에 결정됩니다. AEM forms에서 일관된 AEM 양식 데이터를 사용하려면 데이터베이스 및 GDS와 함께 AEM 저장소 백업 및 복원이 필요합니다. AEM 저장소에는 서신 관리 솔루션, Forms 관리자 및 AEM Forms Workspace에 대한 데이터가 포함되어 있습니다.

### 서신 관리 솔루션 {#correspondence-management-solution}

서신 관리 솔루션은 안전하고 개인화된 인터랙티브한 통신의 작성, 수집 및 전달을 중앙 집중화하고 관리합니다. 이를 통해 작성에서 보관에 이르는 간소화된 프로세스를 통해 사전 승인된 컨텐츠와 사용자 정의 작성 컨텐츠에서 서신을 신속하게 취합할 수 있습니다. 따라서 고객은 적시에 정확하고 편리하며 안전한 적절한 커뮤니케이션을 얻을 수 있습니다. 기업은 고객 상호 작용의 가치를 극대화하고 비용 및 위험을 최소화하여 업무 편의성, 속도 및 생산성을 높일 수 있는 프로세스를 제공합니다.

단순 서신 관리 솔루션 설정에는 동일한 컴퓨터 또는 다른 컴퓨터에 대한 작성자 인스턴스 및 게시 인스턴스가 포함됩니다

### 양식 관리자 {#forms-manager}

forms manager를 사용하면 양식의 업데이트, 관리 및 폐기 프로세스를 간소화할 수 있습니다.

### AEM Forms 작업 공간 {#html-workspace}

AEM Forms Workspace는 (JEE에서 AEM Forms에 대해 더 이상 사용되지 않음) Flex 작업 공간의 기능과 일치하고 새 기능을 추가하여 작업 공간을 확장 및 통합하며 사용자에게 더 친숙한 형식으로 만듭니다.

>[!NOTE]
>
>Flex Workspace는 AEM Forms 릴리스에서 더 이상 사용되지 않습니다.

Flash Player 및 Adobe Reader 없이 클라이언트에서 작업을 관리할 수 있습니다. PDF forms 및 Flex 양식 외에도 HTML Forms 렌디션이 용이해집니다.

## AEM Forms 데이터베이스 {#aem-forms-database}

AEM Forms 데이터베이스는 GDS 및 Content Storage Root 디렉토리(Content Services용)에 있는 파일에 대한 양식 객체, 서비스 구성, 프로세스 상태 및 데이터베이스 참조와 같은 컨텐츠를 저장합니다. 데이터베이스 백업은 서비스 중단 없이 실시간으로 수행할 수 있으며 특정 시점 또는 특정 변경 시점까지 복구할 수 있습니다. 이 섹션에서는 실시간으로 백업할 수 있도록 데이터베이스를 구성하는 방법에 대해 설명합니다.

제대로 구성된 AEM Forms 시스템에서 시스템 관리자와 데이터베이스 관리자는 시스템을 일관되고 알려진 상태로 복구하기 위해 쉽게 공동으로 작업할 수 있습니다.

데이터베이스를 실시간으로 백업하려면 스냅샷 모드를 사용하거나 지정된 로그 모드에서 실행되도록 데이터베이스를 구성해야 합니다. 이렇게 하면 데이터베이스가 열려 있고 사용할 수 있는 동안 데이터베이스 파일을 백업할 수 있습니다. 또한 이 모드에서 실행 중일 때는 데이터베이스가 롤백 및 트랜잭션 로그를 유지합니다.

>[!NOTE]
>
>Adobe® LiveCycle® Content Services ES(사용 중지)는 LiveCycle과 함께 설치된 컨텐츠 관리 시스템입니다. 이를 통해 사용자가 인간 중심 프로세스를 설계, 관리, 모니터링 및 최적화할 수 있습니다. 컨텐츠 서비스(더 이상 사용되지 않음) 지원은 12/31/2014에 종료됩니다. [Adobe 제품 라이프사이클 문서](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html)를 참조하십시오. 컨텐츠 서비스 구성(사용 중지)에 대한 자세한 내용은 [컨텐츠 서비스 관리](https://help.adobe.com/en_US/livecycle/9.0/admin_contentservices.pdf)를 참조하십시오.

### DB2 {#db2}

아카이브 로그 모드에서 실행되도록 DB2 데이터베이스를 구성합니다.

>[!NOTE]
>
>AEM Forms 환경이 이전 버전의 AEM Forms에서 업그레이드되어 DB2를 사용하는 경우 온라인 백업이 지원되지 않습니다. 이 경우 AEM Forms를 종료하고 오프라인 백업을 수행해야 합니다. 향후 버전의 AEM Forms는 업그레이드 고객을 위한 온라인 백업을 지원합니다.

IBM에는 데이터베이스 관리자가 백업 및 복구 작업을 관리하는 데 도움이 되는 툴과 도움말 시스템이 포함되어 있습니다.

* IBM DB2 Archive Log Accelerator( [IBM DB2 Archive Log Accelerator for z/OS User&#39;s Guide](https://publib.boulder.ibm.com/infocenter/dzichelp/v2r2/topic/com.ibm.db2tools.alc.doc.ug/alcugb20.pdf?noframes=true) 참조)
* IBM DB2 데이터 아카이브 전문가([IBM DB2 Data Archive Expert User&#39;s Guide and Reference](https://publib.boulder.ibm.com/infocenter/mptoolic/v1r0/topic/com.ibm.db2tools.aeu.doc.ug/ahxugb13.pdf?noframes=true) 참조)

DB2에는 데이터베이스를 Tivoli Storage Manager에 백업할 수 있는 기능이 내장되어 있습니다. Tivoli Storage Manager를 사용하여 DB2 백업을 다른 미디어 또는 로컬 하드 드라이브에 저장할 수 있습니다.

DB2 데이터베이스 백업 및 복구에 대한 자세한 내용은 [DB2](https://publib.boulder.ibm.com/infocenter/db2luw/v9/index.jsp?topic=/com.ibm.db2.udb.admin.doc/doc/c0005945.htm)백업 및 복구 전략 개발 을 참조하십시오.

### Oracle {#oracle}

스냅샷 백업을 사용하거나 아카이브 로그 모드에서 실행하도록 Oracle 데이터베이스를 구성합니다. ( [Oracle 백업 참조:소개](https://www.databasedesign-resource.com/oracle-backup.md). oracle 데이터베이스 백업 및 복구에 대한 자세한 내용은 다음 사이트를 참조하십시오.

[Oracle 백업 및 복구: ](https://www.oracle.com/technetwork/database/features/availability/br-overview-097160.html)  백업 및 복구의 개념과 RMAN(Recovery Manager)을 사용하여 백업, 복구 및 보고를 수행하는 가장 일반적인 기술에 대해 설명하고 백업 및 복구 전략을 계획하는 방법에 대한 자세한 정보를 제공합니다.

[Oracle 데이터베이스 백업 및 복구 사용 설명서:](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10642.pdf)  RMAN 아키텍처, 백업 및 복구 개념 및 메커니즘, 시점 복구 및 데이터베이스 플래시백 기능과 같은 고급 복구 기법, 백업 및 복구 성능 조정에 대한 자세한 정보를 제공합니다. 또한 RMAN 대신 호스트 운영 체제 설비를 사용하여 사용자가 관리하는 백업 및 복구를 다룹니다. 이 볼륨은 보다 정교한 데이터베이스 구축 및 고급 복구 시나리오에 필요한 백업 및 복구에 필요합니다.

[Oracle 데이터베이스 백업 및 복구 참조: ](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10643.pdf) 모든 RMAN 명령의 구문 및 의미에 대한 전체 정보를 제공하고, 백업 및 복구 작업에 대해 보고하는 데 사용할 수 있는 데이터베이스 보기를 설명합니다.

### SQL Server {#sql-server}

스냅샷 백업을 사용하거나 트랜잭션 로그 모드에서 실행하도록 SQL Server 데이터베이스를 구성합니다.

SQL Server는 또한 두 가지 백업 및 복구 도구를 제공합니다.

* SQL Server Management Studio(GUI)
* T-SQL(명령줄)

자세한 내용은 [백업 및 복원](https://msdn.microsoft.com/en-us/library/ms187048(v=SQL.90).aspx)을 참조하십시오.

### MySQL {#mysql}

MySQLAdmin을 사용하거나 Windows에서 INI 파일을 수정하여 이진 로그 모드에서 실행할 MySQL 데이터베이스를 구성합니다. ( [MySQL 이진 로깅](https://dev.mysql.com/doc/refman/5.1/en/binary-log.html) 참조). MySQL용 핫 백업 툴은 InnoBase 소프트웨어에서도 사용할 수 있습니다. ([Innobase 핫 백업](https://www.innodb.com/hot-backup/features.md) 참조)

>[!NOTE]
>
>MySQL의 기본 이진 로깅 모드는 Content Services에서 사용하는 테이블과 호환되지 않는 &quot;문&quot;입니다(사용되지 않음). 이 기본 모드에서 이진 로깅을 사용하면 Content Services(사용 중지)에 실패합니다. 시스템에 Content Services(사용 중지)가 포함되어 있는 경우 &quot;혼합&quot; 로깅 모드를 사용하십시오. &quot;혼합&quot; 로깅을 사용하려면 my.ini 파일에 다음 인수를 추가하십시오.`binlog_format=mixed log-bin=logname`

myqldump 유틸리티를 사용하여 전체 데이터베이스 백업을 얻을 수 있습니다. 전체 백업이 필요하지만 항상 편리하지는 않습니다. 대용량 백업 파일을 만들고 생성하는 데 시간이 걸립니다. 증분 백업을 수행하려면 이전 섹션에 설명된 대로 - `log-bin` 옵션으로 서버를 시작해야 합니다. MySQL Server가 다시 시작될 때마다 현재 이진 로그에 대한 쓰기를 중단하고 새 이진 로그를 만든 후 이후에 새 서버가 현재 이진 로그가 됩니다. `FLUSH LOGS SQL` 명령을 사용하여 수동으로 스위치를 강제 적용할 수 있습니다. 첫 번째 전체 백업 후 다음 로그 파일을 생성하는 `flush-logs` 명령과 함께 myqladmin 유틸리티를 사용하여 후속 증분 백업을 수행합니다.

[백업 전략 요약](https://dev.mysql.com/doc/refman/5.5/en/backup-strategy-summary.html)을 참조하십시오.

```text
binlog_format=mixed
log-bin=logname
```

## 컨텐츠 저장소 루트 디렉토리(Content Services만 해당) {#content-storage-root-directory-content-services-only}

Content Storage Root 디렉토리에는 모든 문서, 객체 및 인덱스가 저장되는 Content Services(사용되지 않음) 저장소가 있습니다. 컨텐츠 저장소 루트 디렉토리 트리를 백업해야 합니다. 이 섹션에서는 독립 실행형 환경과 클러스터된 환경 모두에 대한 컨텐츠 저장소 루트 디렉토리의 위치를 결정하는 방법을 설명합니다.

### 컨텐츠 저장소 루트 위치(독립형 환경) {#content-storage-root-location-stand-alone-environment}

컨텐츠 서비스(사용되지 않음)가 설치되면 컨텐츠 저장소 루트 디렉토리가 생성됩니다. 컨텐츠 저장소 루트 디렉토리의 위치는 AEM Forms 설치 프로세스 중에 결정됩니다.

컨텐츠 저장소 루트 디렉토리의 기본 위치는 `[aem-forms root]/lccs_data`입니다.

컨텐츠 저장소 루트 디렉토리에 있는 다음 디렉토리를 백업합니다.

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

/backup-lucene-indexes 디렉터리가 없으면 Content Storage Root 디렉터리에 있는 /lucene-indexes 디렉터리를 백업합니다. /backup-lucene-indexes 디렉터리가 있는 경우 오류가 발생할 수 있으므로 /lucene-indexes 디렉터리를 백업하지 마십시오.

### 컨텐츠 저장소 루트 위치(클러스터된 환경) {#content-storage-root-location-clustered-environment}

클러스터형 환경에 Content Services(사용되지 않음)를 설치하면 Content Storage Root 디렉토리가 두 개의 개별 디렉토리로 분할됩니다.

**컨텐츠 저장소 루트 디렉토리:**  일반적으로 클러스터의 모든 노드에 대해 읽기/쓰기 액세스 가능한 공유 네트워크 디렉토리입니다

**인덱스 루트 디렉토리:**  클러스터의 각 노드에 만들어지는 디렉토리로서 항상 동일한 경로 및 디렉토리 이름을 갖습니다

컨텐츠 저장소 루트 디렉토리의 기본 위치는 `[GDS root]/lccs_data`입니다. 여기서 `[GDS root]`은 [GDS 위치](files-back-recover.md#gds-location)에 설명된 위치입니다. 컨텐츠 저장소 루트 디렉토리에 있는 다음 디렉토리를 백업합니다.

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

/backup-lucene-indexes 디렉터리가 없으면 Content Storage Root 디렉터리에 있는 /lucene-indexes 디렉터리를 백업합니다. /backup-lucene-indexes 디렉터리가 있는 경우 오류가 발생할 수 있으므로 /lucene-indexes 디렉터리를 백업하지 마십시오.

인덱스 루트 디렉토리의 기본 위치는 각 노드의 `[aem-forms root]/lucene-indexes`입니다.

## 고객이 설치한 글꼴 {#customer-installed-fonts}

AEM Forms 환경에 추가 글꼴을 설치한 경우 별도로 글꼴을 백업해야 합니다. 설정 > 핵심 시스템 > 구성에서 관리 콘솔에 지정된 모든 Adobe 및 고객 글꼴 디렉토리를 백업합니다. 전체 글꼴 디렉토리를 백업해야 합니다.

>[!NOTE]
>
>기본적으로 AEM Forms와 함께 설치된 Adobe 글꼴은 `[aem-forms root]/fonts` 디렉토리에 있습니다.

호스트 컴퓨터의 운영 체제를 다시 초기화하고 이전 운영 체제의 글꼴을 사용하려면 시스템 fonts 디렉토리의 컨텐츠도 백업해야 합니다. (특정 지침은 운영 체제에 대한 설명서를 참조하십시오.)
