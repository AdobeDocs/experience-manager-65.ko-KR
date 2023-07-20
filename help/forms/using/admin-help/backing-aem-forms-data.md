---
title: Adobe Experience Manager Forms 데이터 백업
description: 이 문서에서는 AEM(Adobe Experience Manager) 양식 데이터베이스, GDS 및 콘텐츠 저장소 루트 디렉터리의 핫 백업 또는 온라인 백업을 완료하는 데 필요한 단계에 대해 설명합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 536615a4-ab42-4b72-83b1-fad110b011ee
source-git-commit: 3885cc51f7e821cdb352737336a29f9c4f0c2f41
workflow-type: tm+mt
source-wordcount: '1535'
ht-degree: 0%

---

# Adobe Experience Manager(AEM) Forms 데이터 백업 {#backing-up-the-aem-forms-data}

<!-- back up is two words when used as a verb; backup is one word when used as an adjective or noun. -->

이 섹션에서는 AEM Forms 데이터베이스, GDS 및 Content Storage Root 디렉토리의 핫 백업 또는 온라인 백업을 완료하는 데 필요한 단계에 대해 설명합니다.

AEM Forms이 설치되고 프로덕션 영역에 배포된 후 데이터베이스 관리자는 초기 전체 또는 콜드 백업을 수행해야 합니다. 이 백업을 수행하려면 데이터베이스를 종료해야 합니다. 그런 다음 데이터베이스의 차등 또는 증분(또는 핫) 백업을 정기적으로 수행해야 합니다.

성공적인 백업 및 복구를 위해서는 시스템 이미지 백업을 항상 사용할 수 있어야 합니다. 그런 다음 손실이 발생하면 전체 환경을 일관된 상태로 복구할 수 있습니다.

GDS, AEM 저장소 및 Content Storage Root 디렉터리 백업과 동시에 데이터베이스를 백업하면 복구가 필요한 경우 이러한 시스템을 계속 동기화할 수 있습니다.

이 섹션에 설명된 백업 절차를 수행하려면 AEM Forms 데이터베이스, AEM 저장소, GDS 및 Content Storage Root 디렉토리를 백업하기 전에 안전 백업 모드로 들어가야 합니다. 백업이 완료되면 안전 백업 모드를 종료해야 합니다. 안전 백업 모드는 GDS에 상주하는 장기 및 영구 문서를 표시하는 데 사용됩니다. 이 모드에서는 안전 백업 모드가 해제될 때까지 자동 파일 정리 메커니즘(파일 수집기)이 만료된 파일을 삭제하지 않습니다. GDS 백업을 데이터베이스 백업과 동기화해야 합니다.

GDS 위치를 백업해야 하는 빈도는 AEM Forms 사용 방법과 사용 가능한 백업 윈도우에 따라 다릅니다. 백업 창은 며칠 동안 실행될 수 있으므로 장기 보존된 프로세스의 영향을 받을 수 있습니다. 이 디렉터리에서 파일을 계속 변경, 추가 및 제거하는 경우 GDS 위치를 더 자주 백업해야 합니다.

데이터베이스가 로깅 모드에서 실행 중인 경우 이전 섹션에서 설명한 대로 미디어 오류가 있는 경우 데이터베이스를 복원하는 데 사용할 수 있도록 데이터베이스 로그도 자주 백업해야 합니다.

>[!NOTE]
>
>참조되지 않은 파일은 복구 프로세스 후 GDS 디렉토리에 지속될 수 있습니다. 이는 현재 알려진 제한 사항입니다.

## 데이터베이스, GDS, AEM 저장소 및 Content Storage Root 디렉터리 백업 {#back-up-the-database-gds-aem-repository-and-content-storage-root-directories}

AEM Forms을 안전 백업(스냅샷) 모드 또는 롤링 백업(연속 적용 범위) 모드로 설정해야 합니다. AEM Forms에서 백업 모드 중 하나를 시작하도록 설정하기 전에 다음을 확인하십시오.

* 시스템 버전을 확인하고 마지막으로 전체 시스템 이미지 백업이 수행된 이후 적용된 패치 또는 업데이트를 기록합니다.
* 롤링 또는 스냅샷 모드 백업을 사용하는 경우 데이터베이스의 핫 백업을 허용하는 올바른 로그 설정으로 데이터베이스가 구성되어 있는지 확인하십시오. (참조: [AEM Forms 데이터베이스](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).)

이 외에도 백업/복원 프로세스에 대해 다음 지침을 준수하십시오.

* 사용 가능한 운영 체제 또는 타사 백업 유틸리티를 사용하여 GDS 디렉토리를 백업합니다. (참조: [GDS 위치](/help/forms/using/admin-help/files-back-recover.md#gds-location).)
* (선택 사항) 사용 가능한 운영 체제나 타사 백업 및 유틸리티를 사용하여 Content Storage Root 디렉터리를 백업합니다. (참조: [콘텐츠 저장소 루트 위치(독립형 환경)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-stand-alone-environment) 또는 [콘텐츠 저장소 루트 위치(클러스터된 환경)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-clustered-environment).)
* 작성자 및 게시 인스턴스 백업(crx -repository backup).

  서신 관리 솔루션 환경을 백업하려면에 설명된 대로 작성자 및 게시 인스턴스에 대한 단계를 수행합니다 [백업 및 복원](/help/sites-administering/backup-and-restore.md).

  작성자 및 게시 인스턴스를 백업할 때 다음 사항을 고려하십시오.

   * 작성자 및 게시 인스턴스에 대한 백업이 동시에 시작되도록 동기화되어야 합니다. 백업이 수행되는 동안 작성자 및 게시 인스턴스를 계속 사용할 수 있지만 캡처되지 않은 변경 사항을 방지하기 위해 백업 중에 자산을 게시하지 않는 것이 좋습니다. 새 자산을 게시하기 전에 작성자 및 게시 인스턴스의 백업이 종료될 때까지 기다립니다.
   * 작성자 노드의 전체 백업에는 Forms Manager 및 AEM Forms Workspace 데이터의 백업이 포함됩니다.
   * Workbench 개발자는 로컬에서 계속 프로세스를 작업할 수 있습니다. 백업 단계에서 새로운 프로세스를 배포해서는 안 됩니다.
   * 각 백업 세션의 길이(롤링 백업 모드)에 대한 결정은 AEM Forms의 모든 데이터(DB, GDS, AEM 저장소 및 기타 추가 사용자 정의 데이터)를 백업하는 데 소요되는 총 시간을 기반으로 해야 합니다.

트랜잭션 로그를 포함하여 AEM Forms 데이터베이스를 백업합니다. 다음을 참조하십시오 [AEM Forms 데이터베이스](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).

자세한 내용은 데이터베이스에 대한 적절한 기술 자료 문서를 참조하십시오.
<!-- The four URLs below are all 404s; checked July 19, 2023 -->
* [AEM Forms용 oracle 백업 및 복구](https://www.adobe.com/go/kb403624)
* [AEM Forms용 MySQL 백업 및 복구](https://www.adobe.com/go/kb403625)
* [Microsoft® AEM Forms용 SQL Server 백업 및 복구](https://www.adobe.com/go/kb403623)
* [AEM Forms용 DB2® 백업 및 복구](https://www.adobe.com/go/kb403626)

이 문서에서는 데이터 백업 및 복구를 위한 기본 데이터베이스 기능에 대한 지침을 제공합니다. 특정 공급업체의 데이터베이스 백업 및 복구 기능에 대한 포괄적인 기술 가이드는 아닙니다. AEM Forms 애플리케이션 데이터에 대한 안정적인 데이터베이스 백업 전략을 만드는 데 필요한 명령에 대해 간략히 설명합니다.

>[!NOTE]
>
>GDS 백업을 시작하기 전에 데이터베이스 백업을 완료해야 합니다. 데이터베이스 백업이 완료되지 않으면 데이터가 동기화되지 않습니다.

### 백업 모드 시작 {#entering-the-backup-modes}

관리 콘솔, LCBackupMode 명령 또는 AEM Forms 설치 시 사용할 수 있는 API를 사용하여 백업 모드를 시작 및 종료할 수 있습니다. 롤링 백업(연속 적용 범위)의 경우 관리 콘솔 옵션을 사용할 수 없습니다. 명령줄 옵션 또는 API를 사용해야 합니다. <!-- Fix broken link For information about using the API to enter and leave backup modes, see AEM Forms API Reference on Help and Tutorials page. -->

>[!NOTE]
>
>Forms 서버에 SSL을 구성한 경우 LCBackupMode.CMD 스크립트를 사용하여 Forms 서버를 백업 모드에 둘 수 없습니다.

**관리 콘솔을 사용하여 안전 백업 모드 시작**

1. 관리 콘솔에 로그인합니다.
1. 설정 > 핵심 시스템 설정 > 백업 유틸리티 를 클릭합니다.
1. 안전 백업 모드에서 작동 을 선택하고 확인 을 클릭합니다.

   이 방법을 사용하면 AEM Forms이 시간 제한 없이 무기한 백업 모드로 전환되고 롤링 백업 모드가 아닌 스냅샷 모드로 전환됩니다.

**명령줄 옵션을 사용하여 안전 백업 모드로 전환**

명령줄 인터페이스를 사용할 수 있습니다 `LCBackupMode` AEM Forms을 안전한 백업 모드로 전환하는 스크립트.

1. Application_Server를 설정하고 ADOBE LIVECYCLE을 시작합니다.
1. 로 이동 `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline` 폴더를 삭제합니다.
1. 운영 체제에 따라 `LCBackupMode.cmd` 또는 `LCBackupMode.sh` 시스템에 적합한 기본값을 제공하는 스크립트입니다.
1. 명령 프롬프트에서 다음 명령을 한 줄에 실행합니다.

   * (Windows) `LCBackupMode.cmd enter [-Host=`*호스트 이름* `] [-port=`*portnumber* `] [-user=`*사용자 이름* `] [-password=`*암호* `] [-label=`*labelname* `] [-timeout=`*초* `]`
   * (Linux®, UNIX®) `LCBackupMode.sh enter [-host=`*호스트 이름* `] [-port=`*portnumber* `] [-user=`*사용자 이름* `] [-password=`*암호* `] [-label=`*labelname* `]`

   이전 명령에서 자리 표시자는 다음과 같이 정의됩니다.

   `Host` 는 AEM Forms이 실행 중인 호스트의 이름입니다.

   `port` 는 AEM Forms이 실행 중인 애플리케이션 서버의 WebServices 포트입니다.

   `user` 는 AEM Forms 관리자의 사용자 이름입니다.

   `password` 는 AEM Forms 관리자의 암호입니다.

   `label` 는 이 백업에 대한 모든 문자열일 수 있는 텍스트 레이블입니다.

   `timeout` 백업 모드를 자동으로 종료하는 시간(초)입니다. 0~10,080일 수 있습니다. 기본값인 0이면 백업 모드가 시간 초과되지 않습니다.

   백업 모드의 명령줄 인터페이스에 대한 자세한 내용은 BackupRestoreCommandline 디렉터리의 추가 정보 파일을 참조하십시오.

### 백업 모드 종료 {#leaving-backup-modes}

관리 콘솔 또는 명령줄 옵션을 사용하여 백업 모드를 종료할 수 있습니다.

**안전 백업 모드(스냅샷 모드) 종료**

관리 콘솔을 사용하여 AEM Forms을 안전 백업 모드(스냅샷 모드)에서 벗어나게 하려면 다음 작업을 수행하십시오.

1. 관리 콘솔에 로그인합니다.
1. 설정 > 핵심 시스템 설정 > 백업 유틸리티 를 클릭합니다.
1. [안전한 백업 모드에서 작동]을 선택 취소하고 [확인]을 클릭합니다.

**모든 백업 모드 종료**

명령줄 인터페이스를 사용하여 AEM Forms을 안전 백업 모드(스냅샷 모드)에서 해제하거나 현재 백업 모드 세션(롤링 모드)을 종료할 수 있습니다. 관리 콘솔을 사용하여 롤링 백업 모드를 종료할 수는 없습니다. 롤링 백업 모드에 있는 동안 관리 콘솔의 백업 유틸리티 컨트롤이 비활성화됩니다. API 호출을 사용하거나 LCBackupMode 명령을 사용합니다.

1. 로 이동 `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline` 폴더를 삭제합니다.
1. 운영 체제에 따라 `LCBackupMode.cmd` 또는 `LCBackupMode.sh` 시스템에 적합한 기본값을 제공하는 스크립트입니다.

   >[!NOTE]
   >
   >의 애플리케이션 서버에 대한 해당 장에 설명된 대로 JAVA_HOME 디렉토리를 설정해야 합니다 [AEM Forms 설치 준비](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63)*.*

1. 한 줄에서 다음 명령을 실행합니다.

   * (Windows) `LCBackupMode.cmd leaveContinuousCoverage [-Host=`*호스트 이름* `] [-port=`*portnumber* `] [-user=`*사용자 이름* `] [-password=`*암호* `]`
   * (Linux®, UNIX®) `LCBackupMode.sh leaveContinuousCoverage [-Host=`*호스트 이름* `] [-port=`*portnumber* `] [-user=`*사용자 이름* `] [-password=`*암호* `]`

     이전 명령에서 자리 표시자는 다음과 같이 정의됩니다.

     `Host` 는 AEM Forms이 실행 중인 호스트의 이름입니다.

     `port` 는 애플리케이션 서버에서 AEM Forms이 실행 중인 포트입니다.

     `user` 는 AEM Forms 관리자의 사용자 이름입니다.

     `password` 는 AEM Forms 관리자의 암호입니다.

     `leaveContinuousCoverage` 이 옵션을 사용하여 롤링 백업 모드를 완전히 비활성화합니다.

   >[!NOTE]
   >
   >백업 모드가 해제되어 있는 동안에는 지속적인 적용 범위를 다시 설정할 수 없습니다. 해당 시간 동안의 모든 변경 사항은 보호되지 않습니다.

   >[!NOTE]
   >
   >데이터베이스에서 문서 저장을 활성화한 경우 스냅샷 백업 모드와 순환 백업 모드를 적용할 수 없습니다.

   백업 모드의 명령줄 인터페이스에 대한 자세한 내용은 BackupRestoreCommandline 디렉터리의 추가 정보 파일을 참조하십시오.
