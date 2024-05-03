---
title: AEM 양식 데이터 복구
description: 이 문서에서는 AEM Forms 데이터를 복구하는 데 필요한 단계에 대해 설명합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 9e648bab-9284-4fda-abb4-8bd7cd085981
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 0%

---

# AEM 양식 데이터 복구 {#recovering-the-aem-forms-data}

이 섹션에서는 AEM Forms 데이터를 복구하는 데 필요한 단계에 대해 설명합니다. 추가 정보 [백업 및 복구에 대한 특별한 고려 사항](/help/forms/using/admin-help/backup-recovery-strategy-aem-forms.md#special-considerations-for-backup-and-recovery).

>[!NOTE]
>
>데이터베이스, GDS, AEM 저장소 및 Content Storage Root 디렉터리는 원본과 동일한 DNS 이름을 가진 컴퓨터로 복원되어야 합니다.

AEM forms는 다음 실패에서 안정적으로 복구되어야 합니다.

**디스크 오류:** 데이터베이스 콘텐츠를 복구하려면 최신 백업 미디어가 필요합니다.

**데이터 손상:** 파일 시스템은 과거 트랜잭션을 기록하지 않으며 시스템이 필요한 프로세스 데이터를 실수로 덮어쓸 수 있습니다.

**사용자 오류:** 복구는 데이터베이스에서 사용할 수 있는 데이터로 제한됩니다. 데이터가 저장되고 사용 가능한 경우 복구가 간단해집니다.

**정전, 시스템 충돌:** 파일 시스템 API는 예기치 않은 시스템 오류를 방지하는 강력한 방식으로 설계되거나 사용되지 않는 경우가 많습니다. 정전 또는 시스템 충돌이 발생하면 데이터베이스에 저장된 문서 컨텐츠가 파일 시스템에 저장된 컨텐츠보다 최신 상태일 수 있습니다.

롤링 백업 모드를 사용하는 경우 복구 후에도 여전히 백업 모드에 있습니다. 스냅샷 백업 모드를 사용하는 경우 복구 후 백업 모드에 있지 않습니다.

백업에서 새 시스템으로 복원할 때 다음 구성이 다를 수 있습니다. 이 차이는 AEM Forms 응용 프로그램의 성공적인 복구에 영향을 주지 않습니다.

* IP 주소
* 물리적 시스템 구성(CPU, 디스크, 메모리)
* GDS 위치

>[!NOTE]
>
>콘텐츠 저장소 루트 디렉터리의 백업은 콘텐츠 서비스 구성 중에 설정된 대로 해당 디렉터리의 위치로 복원되어야 합니다.

다중 노드 클러스터의 단일 노드가 실패하고 클러스터의 나머지 노드가 제대로 작동하는 경우 클러스터 단일 노드 복구 절차를 수행합니다.

## AEM 양식 데이터 복구 {#recover-the-aem-forms-data}

1. 실행 중인 경우 AEM Forms 서비스 및 응용 프로그램 서버를 중지합니다.
1. 필요한 경우 시스템 이미지에서 물리적 시스템을 다시 만듭니다. 예를 들어, 복구 원인이 데이터베이스 서버에 결함이 있는 경우 이 단계는 필요하지 않을 수 있습니다.
1. 이미지가 생성된 이후 적용된 AEM 양식에 패치 또는 업데이트를 적용합니다. 이 정보는 백업 절차에 기록되었습니다. AEM forms는 시스템을 백업할 때와 동일한 패치 수준으로 패치되어야 합니다.
1. (WebSphere® Application Server) WebSphere® Application Server의 새 인스턴스로 복구하는 경우 restoreConfig.bat/sh 명령을 실행합니다.
1. 먼저 데이터베이스 백업 파일을 사용하여 데이터베이스 복원 작업을 실행한 다음 복구된 데이터베이스에 트랜잭션 리두 로그를 적용하여 AEM Forms 데이터베이스를 복구합니다. (참조: [AEM forms 데이터베이스](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).) 자세한 내용은 다음 기술 자료 문서 중 하나를 참조하십시오.

   * [DB2](/help/forms/using/admin-help/files-back-recover.md#db2)
   * [AEM Forms용 oracle 백업 및 복구](/help/forms/using/admin-help/files-back-recover.md#oracle)
   * [Microsoft](/help/forms/using/admin-help/files-back-recover.md#sql-server)
   * [AEM Forms용 MySQL 백업 및 복구](/help/forms/using/admin-help/files-back-recover.md#mysql)

1. 먼저 기존 AEM Forms 설치에 있는 GDS 디렉토리의 내용을 삭제한 다음 백업된 GDS에서 GDS 디렉토리의 내용을 복사하여 GDS 디렉토리를 복구합니다. GDS 디렉토리 위치를 변경한 경우 [복구하는 동안 GDS 위치 변경](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).
1. 다음 예와 같이 복원할 GDS 백업 디렉토리의 이름을 변경합니다.

   >[!NOTE]
   >
   >/restore 디렉터리가 이미 있으면 최신 데이터가 들어 있는 /backup 디렉터리의 이름을 바꾸기 전에 해당 디렉터리를 백업한 다음 삭제합니다.

   * (JBoss®) 이름 바꾸기 `[appserver root]/server/'server'/svcnative/DocumentStorage/backup` 끝:

     `[appserver root]/server/'server'/svcnative/DocumentStorage/restore`

   * (WebLogic) 이름 바꾸기 `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/backup` 끝:

     `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/restore`

   * (WebSphere®) 이름 바꾸기 `[appserver root]/installedApps/adobe/'server'/DocumentStorage/backup` 끝:

     `[appserver root]/installedApps/adobe/'server'/DocumentStorage/restore`

1. 먼저 AEM Forms의 기존 설치에 있는 Content Storage Root 디렉터리의 내용을 삭제한 다음 독립 실행형 또는 클러스터형 환경에 대한 작업에 따라 내용을 복구하여 Content Storage Root 디렉터리를 복구합니다.

   >[!NOTE]
   >
   >콘텐츠 저장소 루트 디렉터리의 백업은 콘텐츠 서비스(사용되지 않음) 구성 중에 설정된 대로 콘텐츠 저장소 루트 디렉터리의 위치로 복원되어야 합니다.

   **독립형:** 복구 프로세스 중에 백업된 모든 디렉터리를 복원합니다. 이러한 디렉토리가 복원될 때 /backup-lucene-indexes 디렉토리가 있으면 이름을 /lucene-indexes로 바꿉니다. 그렇지 않으면 lucene-indexes 디렉토리가 이미 존재해야 하며 조치가 필요하지 않습니다.

   **클러스터형:** 복구 프로세스 중에 백업된 모든 디렉터리를 복원합니다. 인덱스 루트 디렉토리를 복원하려면 클러스터의 각 노드에서 다음 단계를 수행합니다.

   * 인덱스 루트 디렉터리에서 모든 콘텐츠를 삭제합니다.
   * /backup-lucene-indexes 디렉토리가 있으면 의 내용을 복사합니다. *콘텐츠 저장소 루트 디렉터리*/backup-lucene-indexes 디렉토리를 인덱스 루트 디렉토리로 이동하고 *콘텐츠 저장소 루트 디렉터리*/backup-lucene-indexes 디렉터리입니다.
   * /lucene-indexes 디렉토리가 있으면 의 내용을 복사합니다. *콘텐츠 저장소 루트 디렉터리*/lucene-indexes 디렉토리를 인덱스 루트 디렉토리로 복사합니다.

1. CRX-repository 복원/복구

   * **독립형**

     *작성자 및 게시 인스턴스 복원*: 재해가 발생하면에서 설명하는 단계를 수행하여 저장소를 마지막 백업 상태로 복원할 수 있습니다 [백업 및 복원](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html)

     작성자 노드의 전체 복원은 Forms Manager 및 AEM Forms Workspace 데이터의 복원도 확인합니다.

   * **클러스터형**

     클러스터된 환경에서 복원하려면 다음을 참조하십시오. [클러스터 환경에서의 백업 및 리스토어 전략](/help/forms/using/admin-help/strategy-backup-restore-clustered-environment.md#strategy-for-backup-and-restore-in-a-clustered-environment).

1. java.io.temp 디렉토리 또는 Adobe 임시 디렉토리에서 생성된 AEM forms 임시 파일을 삭제합니다.
1. AEM 양식 시작(참조 [서비스 시작 및 중지](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))<!-- BROKEN LINK and the application server(s) (see [Maintaining the Application Server](/help/forms/using/admin-help/topics/maintaining-the-application-server.md))-->.

## 복구하는 동안 GDS 위치 변경 {#changing-the-gds-location-during-recovery}

GDS가 원래 위치가 아닌 다른 위치로 복원되면 LCSetGDS 스크립트를 실행하여 GDS를 새 위치로 설정합니다. 스크립트는 `[aem-forms root]\sdk\misc\Foundation\SetGDSCommandline` 폴더를 삭제합니다. 스크립트는 두 개의 매개 변수를 사용합니다. `defaultGDS` 및 `newGDS`. 다음을 참조하십시오. `ReadMe.txt` 스크립트 실행 방법에 대한 지침은 같은 폴더에 있는 파일을 참조하십시오.

>[!NOTE]
>
>데이터베이스에서 문서 저장을 활성화한 경우에는 GDS 위치를 변경할 필요가 없습니다.

>[!NOTE]
>
>이 상황은 이 스크립트를 사용하여 GDS 위치를 변경해야 하는 유일한 환경입니다. AEM Forms가 실행되는 동안 GDS 위치를 변경하려면 관리 콘솔을 사용합니다. (참조: [일반 AEM 양식 설정 구성](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).)

>[!NOTE]
>
>GDS 디렉터리가 드라이브 루트(예: D:\)에 있는 경우 Windows에서 구성 요소 배포가 실패합니다. GDS의 경우 디렉터리가 드라이브의 루트에 있지 않고 하위 디렉터리에 있는지 확인해야 합니다. 예를 들어 디렉터리는 D:\GDS이어야 하며 D:\이 아니어야 합니다.

## 클러스터된 환경에 GDS 복구 {#recovering-the-gds-to-a-clustered-environment}

클러스터된 환경에서 GDS 위치를 변경하려면 전체 클러스터를 종료하고 클러스터의 단일 노드에서 LCSetGDS 스크립트를 실행합니다. (참조: [복구하는 동안 GDS 위치 변경](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).) 해당 노드만 시작합니다. 해당 노드가 완전히 시작되면 클러스터의 다른 노드가 안전하게 시작될 수 있으며 올바르게 새 GDS를 가리킵니다.

>[!NOTE]
>
>다른 노드를 시작하기 전에 한 노드를 완전히 시작할 수 없는 경우 클러스터를 시작하기 전에 클러스터의 모든 노드에서 LCSetGDS 스크립트를 실행해야 합니다.
