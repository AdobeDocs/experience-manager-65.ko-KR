---
title: AEM 양식 데이터 복구
seo-title: AEM 양식 데이터 복구
description: 이 문서에서는 AEM 양식 데이터를 복구하는 데 필요한 단계를 설명합니다.
seo-description: 이 문서에서는 AEM 양식 데이터를 복구하는 데 필요한 단계를 설명합니다.
uuid: b5735196-5a8d-4358-884f-e9b8d8f4f682
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4e093114-219b-4018-9530-9002eb665448
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 0%

---


# AEM 양식 데이터 {#recovering-the-aem-forms-data} 복구

이 섹션에서는 AEM 양식 데이터를 복구하는 데 필요한 단계를 설명합니다. 백업 및 복구에 대한 [특별한 고려 사항](/help/forms/using/admin-help/backup-recovery-strategy-aem-forms.md#special-considerations-for-backup-and-recovery)을 참조하십시오.

>[!NOTE]
>
>데이터베이스, GDS, AEM 저장소 및 콘텐츠 저장소 루트 디렉토리는 원본과 동일한 DNS 이름을 가진 컴퓨터로 복원해야 합니다.

AEM 양식은 다음 오류로부터 안전하게 복구되어야 합니다.

**디스크 실패:** 데이터베이스 콘텐트를 복구하려면 최신 백업 미디어가 필요합니다.

**데이터 손상:** 파일 시스템은 이전 트랜잭션을 기록하지 않으며 시스템이 실수로 필요한 프로세스 데이터를 덮어쓸 수 있습니다.

**사용자 오류:** 복구는 데이터베이스에서 사용할 수 있는 데이터로 제한됩니다. 데이터가 저장되고 사용 가능한 경우 복구가 간소화됩니다.

**정전, 시스템 충돌:** 파일 시스템 API는 예상치 못한 시스템 오류를 방지하는 강력한 방식으로 설계 또는 사용되지 않는 경우가 많습니다. 정전 또는 시스템 충돌이 발생하면 데이터베이스에 저장된 문서 내용이 파일 시스템에 저장된 내용보다 최신 내용이 될 수 있습니다.

롤링 백업 모드를 사용하는 경우 복구 후에도 여전히 백업 모드에 있습니다. 스냅샷 백업 모드를 사용하는 경우 복구 후 백업 모드가 아닙니다.

백업에서 새 시스템으로 복원할 때 다음 구성이 다를 수 있습니다. 이 차이는 AEM 양식 응용 프로그램의 성공적인 복구에는 영향을 주지 않습니다.

* IP 주소
* 물리적 시스템 구성(CPU, 디스크, 메모리)
* GDS 위치

>[!NOTE]
>
>콘텐츠 저장소 루트 디렉토리의 백업은 Content Services 구성 중에 설정된 디렉토리 위치로 복원되어야 합니다.

다중 노드 클러스터의 단일 노드가 실패했으며 클러스터의 나머지 노드가 제대로 작동하는 경우에는 클러스터 단일 노드 복구 절차를 수행합니다.

## AEM 양식 데이터 {#recover-the-aem-forms-data} 복구

1. 실행 중인 경우 AEM 양식 서비스 및 응용 프로그램 서버를 중지합니다.
1. 필요한 경우 시스템 이미지에서 물리적 시스템을 다시 생성합니다. 예를 들어 복구 원인이 잘못된 데이터베이스 서버인 경우 이 단계를 수행하지 않아도 됩니다.
1. 이미지가 만들어진 이후에 적용된 AEM 양식에 패치 또는 업데이트를 적용할 수 있습니다. 이 정보는 백업 절차에 기록되었습니다. AEM 양식은 시스템을 백업할 때와 동일한 패치 수준으로 패치해야 합니다.
1. (WebSphere 응용 프로그램 서버) WebSphere 응용 프로그램 서버의 새 인스턴스로 복구하는 경우 restoreConfig.bat/sh 명령을 실행합니다.
1. 먼저 데이터베이스 백업 파일을 사용하여 데이터베이스 복원 작업을 실행한 다음 트랜잭션 다시 실행 로그를 복구된 데이터베이스에 적용하여 AEM 양식 데이터베이스를 복구합니다. ([AEM 양식 데이터베이스](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database) 참조) 자세한 내용은 다음 기술 자료 문서 중 하나를 참조하십시오.

   * [AEM 양식을 위한 oracle 백업 및 복구](https://www.adobe.com/go/kb403624)
   * [AEM용 MySQL 백업 및 복구 양식](https://www.adobe.com/go/kb403625)
   * [AEM 양식용 Microsoft SQL Server 백업 및 복구](https://www.adobe.com/go/kb403623)
   * [AEM 양식을 위한 DB2 백업 및 복구](https://www.adobe.com/go/kb403626)

1. AEM 양식의 기존 설치에서 GDS 디렉토리의 컨텐츠를 먼저 삭제한 다음 백업된 GDS 디렉토리에서 GDS 디렉토리의 컨텐츠를 복사하여 GDS 디렉토리를 복구합니다. GDS 디렉토리 위치를 변경한 경우 복구 중 [GDS 위치 변경](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery)을 참조하십시오.
1. 다음 예와 같이 복원할 GDS 백업 디렉토리의 이름을 변경합니다.

   >[!NOTE]
   >
   >/restore 디렉토리가 이미 있는 경우 최신 데이터가 포함된 /backup 디렉토리의 이름을 바꾸기 전에 해당 디렉토리를 백업한 후 삭제합니다.

   * (JBoss) `[appserver root]/server/'server'/svcnative/DocumentStorage/backup`의 이름을 다음으로 바꿉니다.

      `[appserver root]/server/'server'/svcnative/DocumentStorage/restore`.

   * (WebLogic) `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/backup`의 이름을 다음으로 바꿉니다.

      `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/restore`.

   * (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage/backup`의 이름을 다음으로 바꿉니다.

      `[appserver root]/installedApps/adobe/'server'/DocumentStorage/restore`.

1. AEM 양식의 기존 설치에서 Content Storage Root 디렉토리의 컨텐츠를 먼저 삭제한 다음 독립형 환경 또는 클러스터된 환경에 대한 작업을 수행하여 내용을 복구함으로써 Content Storage Root 디렉토리를 복구합니다.

   >[!NOTE]
   >
   >콘텐츠 저장소 루트 디렉토리의 백업은 콘텐츠 서비스(더 이상 사용되지 않음) 구성 중에 설정된 대로 컨텐츠 저장소 루트 디렉토리의 위치로 복원되어야 합니다.

   **독립 실행형:** 복구 프로세스 동안 백업된 모든 디렉터리를 복원합니다. 이러한 디렉토리가 복원되면 /backup-lucene-indexes 디렉토리가 있는 경우 이름을 /lucene-indexes로 변경합니다. 그렇지 않으면 lucene-indexes 디렉토리가 이미 존재해야 하며 작업이 필요하지 않습니다.

   **클러스터됨:** 복구 프로세스 동안 백업된 모든 디렉터리를 복원합니다. 인덱스 루트 디렉토리를 복원하려면 클러스터의 각 노드에서 다음 단계를 수행합니다.

   * 색인 루트 디렉터리의 모든 콘텐츠를 삭제합니다.
   * /backup-lucene-indexes 디렉토리가 있는 경우 *Content Storage Root 디렉토리*/backup-lucene-indexes 디렉토리의 내용을 인덱스 루트 디렉토리에 복사하고 *Content Storage Root 디렉토리*/backup-lucene-indexes 디렉토리를 삭제합니다.
   * /lucene-indexes 디렉토리가 있는 경우 *Content Storage Root 디렉토리*/lucene-indexes 디렉토리의 내용을 인덱스 루트 디렉토리에 복사합니다.

1. CRX 저장소를 복구/복구합니다.

   * **독립 실행형**

      *작성자 및 게시 인스턴스 복원*:재해가 발생하면 백업 및 복원에 설명된 단계를 수행하여 저장소를 마지막  [백업 상태로 복원할 수 있습니다.](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html)

      작성자 노드를 완전히 복원하면 Forms Manager 및 AEM Forms Workspace 데이터도 복원됩니다.

   * **클러스터됨**

      클러스터된 환경에서 복원하려면 [클러스터된 환경에서 백업 및 복원 전략을 참조하십시오](/help/forms/using/admin-help/strategy-backup-restore-clustered-environment.md#strategy-for-backup-and-restore-in-a-clustered-environment).

1. java.io.temp 디렉토리 또는 Adobe 임시 디렉토리에서 만든 AEM 양식 임시 파일을 삭제합니다.
1. AEM 양식을 시작합니다([서비스 시작 및 중지 참조](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))<!-- BROKEN LINK and the application server(s) (see [Maintaining the Application Server](/help/forms/using/admin-help/topics/maintaining-the-application-server.md))-->.

## 복구 중 GDS 위치 변경 {#changing-the-gds-location-during-recovery}

GDS가 원래 있던 위치가 아닌 다른 위치로 복원되는 경우 LCSetGDS 스크립트를 실행하여 GDS를 새 위치로 설정합니다. 스크립트가 `[aem-forms root]\sdk\misc\Foundation\SetGDSCommandline` 폴더에 있습니다. 스크립트에는 `defaultGDS` 및 `newGDS` 매개 변수가 2개 사용됩니다. 스크립트를 실행하는 방법에 대한 자세한 내용은 같은 폴더의 `ReadMe.txt` 파일을 참조하십시오.

>[!NOTE]
>
>데이터베이스에서 문서 저장소를 사용하도록 설정한 경우 GDS 위치를 변경할 필요가 없습니다.

>[!NOTE]
>
>이 상황에서 이 스크립트를 사용하여 GDS 위치를 변경할 수 있습니다. AEM 양식을 실행하는 동안 GDS 위치를 변경하려면 관리 콘솔을 사용합니다. 자세한 내용은 [일반 AEM 양식 설정 구성](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)을 참조하십시오.

>[!NOTE]
>
>GDS 디렉토리가 드라이브 루트(예: D:\)에 있는 경우 Windows에서 구성 요소 배포가 실패합니다. GDS의 경우 디렉토리가 드라이브의 루트에 있지 않지만 하위 디렉토리에 있어야 합니다. 예를 들어 디렉토리는 D:\GDS and not simply D:\ 이어야 합니다.

## GDS를 클러스터된 환경 {#recovering-the-gds-to-a-clustered-environment}으로 복구하는 중

클러스터 환경에서 GDS 위치를 변경하려면 전체 클러스터를 종료하고 클러스터의 단일 노드에서 LCSetGDS 스크립트를 실행하십시오. (복구 중 [GDS 위치 변경](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery)을 참조하십시오.) 해당 노드만 시작합니다. 해당 노드가 완전히 시작되면 클러스터의 다른 노드가 안전하게 시작될 수 있으며 새 GDS를 올바로 가리키게 됩니다.

>[!NOTE]
>
>다른 노드를 시작하기 전에 한 노드를 완전히 시작할 수 없는 경우 클러스터를 시작하기 전에 클러스터의 모든 노드에서 LCSetGDS 스크립트를 실행해야 합니다.

