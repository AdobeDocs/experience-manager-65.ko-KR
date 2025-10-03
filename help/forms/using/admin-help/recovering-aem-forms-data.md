---
title: AEM Forms 데이터 복구
description: 이 문서에서는 AEM Forms 데이터를 복구하는 데 필요한 단계를 설명합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 9e648bab-9284-4fda-abb4-8bd7cd085981
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '1118'
ht-degree: 100%

---

# AEM Forms 데이터 복구 {#recovering-the-aem-forms-data}

이 섹션에서는 AEM Forms 데이터를 복구하는 데 필요한 단계를 설명합니다. 또한 [백업 및 복구에 대한 특별 고려 사항](/help/forms/using/admin-help/backup-recovery-strategy-aem-forms.md#special-considerations-for-backup-and-recovery)을 참조하십시오.

>[!NOTE]
>
>데이터베이스, GDS, AEM 저장소 및 콘텐츠 스토리지 루트 디렉터리는 DNS 이름이 원본과 동일한 컴퓨터로 복원해야 합니다.

AEM Forms는 다음과 같은 오류 발생 시 안정적으로 복구되어야 합니다.

**디스크 오류:** 데이터베이스 콘텐츠를 복구하려면 최신 백업 미디어가 필요합니다.

**데이터 손상:** 파일 시스템에서 이전 트랜잭션을 기록하지 않으며 실수로 필수 프로세스 데이터를 덮어쓸 수 있습니다.

**사용자 오류:** 복구는 데이터베이스에서 제공되는 데이터로 제한됩니다. 데이터가 저장되어 있고 사용 가능하다면 복구가 더 쉬워집니다.

**정전, 시스템 충돌:** 파일 시스템 API는 예기치 않은 시스템 오류에 대비할 수 있도록 견고한 방식으로 설계되거나 사용되지 않는 경우가 많습니다. 정전이나 시스템 충돌이 발생하는 경우 데이터베이스에 저장된 문서 콘텐츠는 파일 시스템에 저장된 콘텐츠보다 최신 상태일 가능성이 높습니다.

롤링 백업 모드를 사용하는 경우 복구 후에도 계속 백업 모드가 유지됩니다. 스냅샷 백업 모드를 사용하는 경우 복구 후에는 백업 모드가 아닙니다.

백업에서 새 시스템으로 복원할 때 다음 구성이 다를 수 있습니다. 이러한 차이는 AEM Forms 애플리케이션이 성공적으로 복구되는 데 영향을 미치지 않습니다.

* IP 주소
* 물리적 시스템 구성(CPU, 디스크, 메모리)
* GDS 위치

>[!NOTE]
>
>콘텐츠 스토리지 루트 디렉터리의 백업은 콘텐츠 서비스 구성 중에 설정된 대로 해당 디렉터리의 위치로 복원되어야 합니다.

다중 노드 클러스터의 단일 노드가 실패하고 클러스터의 나머지 노드는 제대로 작동하는 경우 클러스터 단일 노드 복구 절차를 수행합니다.

## AEM Forms 데이터 복구 {#recover-the-aem-forms-data}

1. AEM Forms 서비스와 애플리케이션 서버가 실행 중이면 이를 중지합니다.
1. 필요한 경우 시스템 이미지에서 물리적 시스템을 다시 만듭니다. 예를 들어 데이터베이스 서버에 오류가 발생하여 복구하는 것이라면 이 단계는 필요하지 않을 수도 있습니다.
1. 이미지가 만들어진 이후 적용된 AEM Forms에 패치나 업데이트를 적용합니다. 이 정보는 백업 절차에 기록되었습니다. AEM Forms는 시스템이 백업되었을 당시와 동일한 패치 수준으로 패치되어야 합니다.
1. (WebSphere® Application Server) WebSphere® Application Server의 새 인스턴스로 복구하는 경우 restoreConfig.bat/sh 명령을 실행합니다.
1. 먼저 데이터베이스 백업 파일을 사용하여 데이터베이스 복원 작업을 실행한 후 복구된 데이터베이스에 트랜잭션 다시 실행 로그를 적용하여 AEM Forms 데이터베이스를 복구합니다. ([AEM Forms 데이터베이스](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database)를 참조하십시오.) 자세한 내용은 다음과 같은 기술 자료 문서 중 하나를 참조하십시오.

   * [DB2](/help/forms/using/admin-help/files-back-recover.md#db2)
   * [AEM Forms용 Oracle 백업 및 복구](/help/forms/using/admin-help/files-back-recover.md#oracle)
   * [Microsoft](/help/forms/using/admin-help/files-back-recover.md#sql-server)
   * [AEM Forms용 MySQL 백업 및 복구](/help/forms/using/admin-help/files-back-recover.md#mysql)

1. 먼저 기존 AEM Forms 설치에서 GDS 디렉터리 콘텐츠를 삭제한 후 백업된 GDS에서 GDS 디렉터리 콘텐츠를 복사하여 GDS 디렉터리를 복구합니다. GDS 디렉터리 위치를 변경한 경우 [복구 중 GDS 위치 변경](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery)을 참조하십시오.
1. 다음 예와 같이 복원할 GDS 백업 디렉터리의 이름을 바꿉니다.

   >[!NOTE]
   >
   >/restore 디렉터리가 이미 존재하는 경우 해당 디렉터리를 백업해서 삭제한 후 최신 데이터가 포함된 /backup 디렉터리의 이름을 바꿉니다.

   * (JBoss®) `[appserver root]/server/'server'/svcnative/DocumentStorage/backup`의 이름을 다음으로 바꿉니다.

     `[appserver root]/server/'server'/svcnative/DocumentStorage/restore`

   * (WebLogic) `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/backup`의 이름을 다음으로 바꿉니다.

     `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/restore`

   * (WebSphere®) `[appserver root]/installedApps/adobe/'server'/DocumentStorage/backup`의 이름을 다음으로 바꿉니다.

     `[appserver root]/installedApps/adobe/'server'/DocumentStorage/restore`

1. 먼저 기존 AEM Forms 설치에서 콘텐츠 스토리지 루트 디렉터리의 콘텐츠를 삭제한 후 독립 실행형 환경 또는 클러스터링된 환경에 맞는 작업을 따라 콘텐츠를 복구하여 콘텐츠 스토리지 루트 디렉터리를 복구합니다.

   >[!NOTE]
   >
   >콘텐츠 스토리지 루트 디렉터리의 백업은 콘텐츠 서비스(더 이상 사용되지 않음) 구성 중에 설정된 콘텐츠 스토리지 루트 디렉터리의 위치로 복원되어야 합니다.

   **독립 실행형:** 복구 프로세스 중에 백업된 모든 디렉터리를 복원합니다. 해당 디렉터리가 복원될 때 /backup-lucene-indexes 디렉터리가 있다면 해당 디렉터리의 이름을 /lucene-indexes로 바꿉니다. 그렇지 않은 경우 lucene-indexes 디렉터리가 이미 존재해야 하며 아무런 조치도 필요하지 않습니다.

   **클러스터링됨:** 복구 프로세스 중에 백업된 모든 디렉터리를 복원합니다. 색인 루트 디렉터리를 복원하려면 클러스터의 각 노드에서 다음 단계를 수행하십시오.

   * 색인 루트 디렉터리의 모든 콘텐츠를 삭제합니다.
   * /backup-lucene-indexes 디렉터리가 있는 경우 *콘텐츠 스토리지 루트 디렉터리*/backup-lucene-indexes 디렉터리의 콘텐츠를 색인 루트 디렉터리에 복사하고 *콘텐츠 스토리지 루트 디렉터리*/backup-lucene-indexes 디렉터리를 삭제합니다.
   * /lucene-indexes 디렉터리가 있는 경우 *콘텐츠 스토리지 루트 디렉터리*/lucene-indexes 디렉터리의 콘텐츠를 색인 루트 디렉터리에 복사합니다.

1. CRX 저장소를 복원/복구합니다.

   * **독립 실행형**

     *작성자 인스턴스 및 게시 인스턴스 복원*: 재해가 발생하면 [백업 및 복원](https://helpx.adobe.com/kr/experience-manager/kb/CRXBackupAndRestoreProcedure.html)에 설명된 단계를 수행하여 저장소를 마지막으로 백업된 상태로 복원할 수 있습니다.

     작성자 노드를 완전히 복원하면 Forms Manager와 AEM Forms Workspace 데이터도 복원됩니다.

   * **클러스터링됨**

     클러스터링된 환경에서 복원하는 경우 [클러스터링된 환경에서의 백업 및 복원 전략](/help/forms/using/admin-help/strategy-backup-restore-clustered-environment.md#strategy-for-backup-and-restore-in-a-clustered-environment)을 참조하십시오.

1. java.io.temp 디렉터리나 Adobe 임시 디렉터리에 생성된 AEM Forms 임시 파일을 삭제합니다.
1. AEM Forms를 시작합니다([서비스 시작 및 중지](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)를 참조하십시오)<!-- BROKEN LINK and the application server(s) (see [Maintaining the Application Server](/help/forms/using/admin-help/topics/maintaining-the-application-server.md))-->.

## 복구 중 GDS 위치 변경 {#changing-the-gds-location-during-recovery}

GDS가 원래 위치가 아닌 다른 위치로 복원되는 경우 LCSetGDS 스크립트를 실행하여 GDS를 새 위치로 설정합니다. 이 스크립트는 `[aem-forms root]\sdk\misc\Foundation\SetGDSCommandline` 폴더에 있으며 `defaultGDS` 및 `newGDS`의 두 가지 매개변수를 사용합니다. 스크립트를 실행하는 방법에 대한 지침은 같은 폴더에 있는 `ReadMe.txt` 파일을 참조하십시오.

>[!NOTE]
>
>데이터베이스에서 문서 저장을 활성화한 경우 GDS 위치를 변경할 필요가 없습니다.

>[!NOTE]
>
>이러한 상황에서만 해당 스크립트를 사용하여 GDS 위치를 변경해야 합니다. AEM Forms가 실행되는 동안 GDS 위치를 변경하려면 관리 콘솔을 사용하십시오. ([일반 AEM Forms 설정 구성](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)을 참조하십시오.)

>[!NOTE]
>
>GDS 디렉터리가 드라이브 루트(예: D:\)에 있는 경우 Windows에서 구성 요소 배포가 실패합니다. GDS의 경우 디렉터리가 드라이브 루트에 위치하지 않고 하위 디렉터리에 있어야 합니다. 예를 들어 디렉터리는 D:\GDS여야 하며 단순히 D:\가 아닙니다.

## GDS를 클러스터링된 환경으로 복구 {#recovering-the-gds-to-a-clustered-environment}

클러스터링된 환경에서 GDS 위치를 변경하려면 전체 클러스터를 종료하고 클러스터의 단일 노드에서 LCSetGDS 스크립트를 실행합니다. ([복구 중 GDS 위치 변경](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery)을 참조하십시오. ) 해당 노드만 시작합니다. 해당 노드가 완전히 시작되면 클러스터의 다른 노드도 안전하게 시작될 수 있으며 새 GDS를 올바르게 가리킵니다.

>[!NOTE]
>
>다른 노드를 시작하기 전에 한 노드를 완전히 시작할 수 없는 경우 클러스터를 시작하기 전에 클러스터의 모든 노드에서 LCSetGDS 스크립트를 실행해야 합니다.
