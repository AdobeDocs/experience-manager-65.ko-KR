---
title: 클러스터 환경에서의 백업 및 리스토어 전략
description: AEM Forms 구현에서 추가 사용자 정의 데이터를 다른 데이터베이스에 저장하는 경우, AEM Forms 데이터와 계속 동기화되도록 이 데이터를 백업하는 전략을 구현해야 합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 98c96349-f253-475f-b646-352269814a38
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1396'
ht-degree: 0%

---

# 클러스터 환경에서의 백업 및 리스토어 전략 {#strategy-for-backup-and-restore-in-a-clustered-environment}

>[!NOTE]
>
>AEM Forms 구현에서 추가 사용자 정의 데이터를 다른 데이터베이스에 저장하는 경우, AEM Forms 데이터와 계속 동기화되도록 이 데이터를 백업하는 전략을 구현해야 합니다. 또한 추가 데이터베이스가 동기화되지 않는 시나리오를 처리할 수 있을 만큼 강력하도록 애플리케이션을 설계해야 합니다. 수행되는 모든 데이터베이스 작업은 일관된 상태를 유지하는 데 도움이 되도록 트랜잭션 컨텍스트에서 수행하는 것이 좋습니다.

오류를 복구하려면 AEM Forms 시스템의 다음 부분을 백업해야 합니다.

* AEM Forms에서 사용하는 데이터베이스
* 오래 지속된 데이터 및 기타 영구 문서가 있는 GDS
* AEM 데이터베이스(crx-repository)

>[!NOTE]
>
>고객 글꼴, 커넥터 데이터 등과 같이 AEM Forms 설정에서 사용 중인 다른 모든 데이터를 백업해야 합니다.

## 클러스터된 환경 백업 {#back-up-a-clustered-environment}

이 항목에서는 AEM Forms 클러스터된 환경을 백업하는 다음 전략에 대해 설명합니다.

* 다운타임이 있는 오프라인 백업
* 다운타임 없이 오프라인 백업(종료된 보조 노드 백업)
* 다운타임 없이 응답이 지연되는 온라인 백업
* Bootstrap 속성 파일 백업

### 다운타임이 있는 오프라인 백업 {#offline-backup-with-downtime}

1. 전체 클러스터 및 관련 서비스를 종료합니다. (참조 [서비스 시작 및 중지](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. 모든 노드에서 데이터베이스, GDS 및 커넥터를 백업합니다. (참조 [백업 및 복구할 파일](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. AEM 저장소를 오프라인으로 백업하려면 다음 단계를 수행하십시오.

   1. 각 클러스터 노드에 대해 클러스터 노드 ID가 포함된 파일을 백업합니다.
   1. 하위 디렉토리를 포함하여 모든 보조 클러스터 노드의 모든 파일을 백업합니다.
   1. 각 클러스터 노드의 저장소/시스템 ID를 별도로 백업합니다.

   자세한 단계는 를 참조하십시오. [백업 및 복원](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

1. 고객 글꼴과 같은 다른 모든 데이터를 백업합니다.
1. 클러스터를 다시 시작합니다.

### 다운타임 없는 오프라인 백업 {#offline-backup-with-no-downtime}

1. 롤링 백업 모드로 들어갑니다. (참조 [백업 모드 시작](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes))

   복구 후 롤링 백업 모드를 둡니다.

1. AEM과 관련하여 클러스터의 보조 노드를 종료합니다. (참조 [서비스 시작 및 중지](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. 모든 노드에서 데이터베이스, GDS 및 커넥터를 백업합니다. (참조 [백업 및 복구할 파일](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. AEM 저장소를 오프라인으로 백업하려면 다음 단계를 수행하십시오.

   1. 각 클러스터 노드에 대해 클러스터 노드 ID가 포함된 파일을 백업합니다.
   1. 하위 디렉토리를 포함하여 모든 보조 클러스터 노드의 모든 파일을 백업합니다.
   1. 각 클러스터 노드의 repository/system.id 를 별도로 백업합니다.

   자세한 단계는 를 참조하십시오. [백업 및 복원](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

1. 고객 글꼴과 같은 다른 모든 데이터를 백업합니다.
1. 클러스터를 다시 시작합니다.

### 다운타임 없이 응답이 지연되는 온라인 백업 {#online-backup-with-no-downtime-but-delay-in-response}

1. 롤링 백업 모드로 들어갑니다. (참조 [백업 모드 시작](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes))

   복구 후 롤링 백업 모드를 둡니다.

1. AEM과 관련하여 클러스터의 보조 노드를 종료합니다. (참조 [서비스 시작 및 중지](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. 모든 노드에서 데이터베이스, GDS 및 커넥터를 백업합니다. (참조 [백업 및 복구할 파일](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. AEM 저장소를 온라인으로 백업하려면 다음 단계를 수행합니다.

   1. 각 클러스터 노드에 대해 cluster_node.id가 포함된 파일을 백업합니다.
   1. 각 클러스터 노드의 repository/system.id 를 별도로 백업합니다.
   1. 보조 노드에서 저장소의 온라인 백업을 수행하여 자세한 단계를 보려면 온라인 백업을 참조하십시오.

1. 고객 글꼴과 같은 다른 모든 데이터를 백업합니다.
1. 클러스터를 다시 시작합니다.

### Bootstrap 속성 파일 백업 {#back-up-the-bootstrap-properties-file}

AEM 클러스터를 생성하면 모든 보조 노드에 대한 등록 정보 파일이 응용 프로그램 서버에 생성됩니다. Bootstrap 속성 파일을 백업하는 것이 좋습니다. 응용 프로그램 서버의 다음 위치에서 파일을 찾을 수 있습니다.

* JBoss®: BIN 디렉토리
* WebLogic: 도메인 디렉토리
* WebSphere®: 프로필 디렉토리

AEM 보조 노드의 재해 복구 시나리오에 사용할 파일을 백업하고 복원할 경우 응용 프로그램 서버의 지정된 위치에 파일을 바꿉니다.

## 클러스터된 환경에서 복구 {#recovery-in-a-clustered-environment}

전체 클러스터 또는 단일 노드에 오류가 있는 경우 백업을 사용하여 복원합니다.

단일 노드 복구의 경우 단일 노드를 종료하고 단일 노드 복구 절차를 실행합니다.

데이터베이스 충돌과 같은 실패로 인해 전체 클러스터가 실패하는 경우 다음 단계를 수행합니다. 복원은 사용된 백업 방법에 따라 다릅니다.

### 단일 노드 복원 {#restoring-a-single-node}

1. 손상된 노드를 중지합니다.

   >[!NOTE]
   >
   >손상된 노드가 AEM 기본 노드인 경우 전체 클러스터 노드를 종료합니다.

1. 시스템 이미지에서 물리적 시스템을 다시 만듭니다.
1. 이미지가 생성된 이후 적용된 AEM 양식에 패치 또는 업데이트를 적용합니다. 이 정보는 백업 절차 중에 기록되었습니다. AEM forms는 시스템을 백업할 때와 동일한 패치 수준으로 복구해야 합니다.
1. (*선택 사항*) 다른 모든 노드가 제대로 작동하는 경우 AEM 저장소도 손상되었을 수 있습니다. 이 경우 AEM 저장소의 error.log 파일에 저장소 동기화 해제 메시지가 표시됩니다.

   저장소를 복원하려면 다음 단계를 수행하십시오.

   >[!NOTE]
   >
   >압축된 crx-repository 백업을 온라인으로 가져온 경우 원하는 위치에서 압축을 풀고 오프라인 복원 프로세스를 따르십시오.

   1. 노드의 clusterNode 디렉토리에서 저장소, 공유, 버전 및 작업 공간 디렉토리를 삭제합니다.
   1. 클러스터 노드(하위 디렉터리 포함)의 백업을 노드에 복원합니다.
   1. 노드에서 파일 clusterNode/revision.log 을 삭제합니다.
   1. 존재하는 경우 노드에서 .lock을 삭제합니다.
   1. 존재하는 경우 노드에서 repository/system.id을 삭제합니다.
   1. 존재하는 경우 노드에서 파일 &amp;ast;&amp;ast;/listener.properties을 삭제합니다.
   1. 개별 클러스터 노드의 경우 repository/cluster_node.id을 복원합니다.

>[!NOTE]
>
>다음 사항을 고려하십시오.

* 실패한 노드가 AEM 주 노드인 경우 보조 저장소 폴더(crx-repository\crx.0000 여기서 0000은 임의의 숫자일 수 있음)의 모든 컨텐츠를 crx-repository\ repository 폴더로 복사하고 보조 저장소 폴더를 삭제합니다.
* 클러스터 노드를 다시 시작하기 전에 기본 노드에서 저장소 /clustered.txt 를 삭제해야 합니다.
* 기본 노드가 먼저 시작되었는지 확인하고 작동한 후 다른 노드를 시작합니다.

### 전체 클러스터 복원 {#restoring-the-entire-cluster}

1. 모든 클러스터 노드를 중지합니다.
1. 시스템 이미지에서 물리적 시스템을 다시 만듭니다.
1. 이미지 작성 이후 적용된 AEM formsAEM 양식에 패치 또는 업데이트를 적용합니다. 이 정보는 백업 절차의 1단계에서 기록되었다. AEM forms는 시스템을 백업할 때와 동일한 패치 수준으로 복구해야 합니다.
1. 데이터베이스, GDS 및 커넥터를 복원합니다.
1. 다음을 수행하여 AEM 저장소를 오프라인으로 복구합니다.

   >[!NOTE]
   >
   >압축된 crx-repository 백업을 온라인으로 가져온 경우 원하는 위치에서 압축을 풀고 오프라인 복원 프로세스를 따르십시오.

   1. 모든 클러스터 노드에서 clusterNode 디렉토리의 저장소, 공유, 버전 및 작업 공간 디렉토리를 삭제합니다.
   1. 공유 디렉터리에서 모든 파일과 디렉터리를 삭제합니다.
   1. 클러스터 노드(하위 디렉터리 포함)의 백업을 하나의 클러스터 노드로 복원합니다.
   1. 복원된 클러스터 노드의 모든 파일을 다른 모든 클러스터 노드에 복사합니다. 완료되면 각 클러스터 노드에 동일한 데이터가 포함됩니다.
   1. 모든 클러스터 노드에서 파일 clusterNode/revision.log 을 삭제합니다.
   1. 존재하는 경우 모든 클러스터 노드에서 .lock을 삭제합니다.
   1. 존재하는 경우 repository/system.id 모든 클러스터 노드를 삭제합니다.
   1. 모든 클러스터 노드에서 파일 &amp;ast;&amp;ast;/listener.properties(있는 경우)를 삭제합니다.
   1. 개별 클러스터 노드의 경우 repository/cluster_node.id을 복원합니다.

>[!NOTE]
>
>다음 사항을 고려하십시오.

* 실패한 노드가 AEM 주 노드인 경우, 보조 저장소 폴더(crx-repository\crx.0000처럼 보이며, 0000은 임의의 숫자일 수 있음)의 모든 컨텐츠를 crx-repository\ repository 폴더로 복사합니다.
* 클러스터 노드를 다시 시작하기 전에 기본 노드에서 저장소 /clustered.txt 를 삭제해야 합니다.
* 기본 노드가 먼저 시작되었는지 확인하고 작동한 후 다른 노드를 시작합니다.

## 서신 관리 솔루션 게시 노드 백업 및 복원 {#back-up-and-restore-correspondence-management-solution-publish-node}

클러스터된 환경에 게시자 노드에 기본-보조 관계가 없습니다. 다음을 수행하여 모든 게시자 노드를 백업할 수 있습니다. [백업 및 복원](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

### 단일 게시자 노드 복구 {#recover-a-single-publisher-node}

1. 복구해야 하는 노드를 종료하고 노드가 다시 시작될 때까지 게시 활동을 수행하지 않습니다.
1. 다음을 사용하여 게시 노드 복원 [백업 복원](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

### 클러스터 복구 {#recover-a-cluster}

1. 클러스터를 종료합니다.
1. 다음을 사용하여 게시 노드 복원 [백업 복원](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).
1. 주 노드 다음에 작성자 클러스터의 보조 노드가 올 때 시작합니다.
