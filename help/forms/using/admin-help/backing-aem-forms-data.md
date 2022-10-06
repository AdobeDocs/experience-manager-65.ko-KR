---
title: AEM Forms 데이터 백업
seo-title: Backing up the AEM forms data
description: 이 문서에서는 AEM Forms 데이터베이스, GDS 및 Content Storage Root 디렉토리의 핫 또는 온라인 백업을 완료하는 데 필요한 단계에 대해 설명합니다.
seo-description: This document describes the steps that are required to complete a hot, or online, backup of the AEM forms database, the GDS, and Content Storage Root directories.
uuid: ac7856be-e3b7-4b81-b8b9-fc909b5907b4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 52187196-b091-4683-85ae-cc7c250dee54
exl-id: 536615a4-ab42-4b72-83b1-fad110b011ee
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1540'
ht-degree: 0%

---

# AEM Forms 데이터 백업 {#backing-up-the-aem-forms-data}

이 섹션에서는 AEM Forms 데이터베이스, GDS 및 Content Storage Root 디렉토리의 핫 또는 온라인 백업을 완료하는 데 필요한 단계에 대해 설명합니다.

AEM Forms가 설치되고 프로덕션 영역에 배포되면 데이터베이스 관리자는 데이터베이스의 초기 전체 또는 콜드 백업을 수행해야 합니다. 이 백업을 위해 데이터베이스를 종료해야 합니다. 그런 다음 데이터베이스의 차등 또는 증분(또는 핫) 백업을 정기적으로 수행해야 합니다.

성공적인 백업 및 복구를 위해서는 시스템 이미지 백업을 항상 사용할 수 있어야 합니다. 그런 다음 손실이 발생하면 전체 환경을 일관된 상태로 복구할 수 있습니다.

GDS, AEM 저장소 및 Content Storage Root 디렉토리 백업과 동시에 데이터베이스를 백업하면 복구가 필요한 경우 이러한 시스템을 계속 동기화할 수 있습니다.

이 섹션에 설명된 백업 절차를 수행하려면 AEM Forms 데이터베이스, AEM 저장소, GDS 및 Content Storage Root 디렉토리를 백업하기 전에 안전한 백업 모드를 시작해야 합니다. 백업이 완료되면 안전한 백업 모드를 종료해야 합니다. 안전한 백업 모드는 GDS에 상주하는 장기간 및 영구 문서를 표시하는 데 사용됩니다. 이 모드에서는 안전한 백업 모드가 해제될 때까지 자동 파일 정리 메커니즘(파일 수집기)이 만료된 파일을 삭제하지 않습니다. 데이터베이스 백업과 동기화된 GDS 백업을 유지해야 합니다.

GDS 위치를 백업해야 하는 빈도는 AEM Forms 사용 방법과 백업 창을 사용할 수 있는지에 따라 다릅니다. 백업 기간은 여러 날 동안 실행할 수 있으므로 장기 처리 프로세스의 영향을 받을 수 있습니다. 이 디렉터리에서 파일을 계속 변경, 추가 및 제거하는 경우 GDS 위치를 더 자주 백업해야 합니다.

이전 섹션에 설명된 대로 데이터베이스가 로깅 모드에서 실행 중인 경우 미디어 실패 시 데이터베이스를 복원하는 데 사용할 수 있도록 데이터베이스 로그도 자주 백업해야 합니다.

>[!NOTE]
>
>참조되지 않은 파일은 복구 프로세스 후에 GDS 디렉토리에 유지됩니다. 이는 현재 알려진 제한 사항입니다.

## 데이터베이스, GDS, AEM 저장소 및 컨텐츠 저장 루트 디렉토리 백업 {#back-up-the-database-gds-aem-repository-and-content-storage-root-directories}

AEM Forms를 안전한 백업(스냅샷) 모드 또는 롤링 백업(연속 적용 범위) 모드로 설정해야 합니다. 백업 모드 중 하나를 입력하도록 AEM 양식을 설정하기 전에 다음을 확인하십시오.

* 시스템 버전을 확인하고 마지막 전체 시스템 이미지 백업이 수행된 이후 적용된 패치 또는 업데이트를 기록합니다.
* 롤링 또는 스냅샷 모드 백업을 사용하는 경우 데이터베이스의 핫 백업을 허용하는 올바른 로그 설정으로 데이터베이스가 구성되어 있는지 확인하십시오. (자세한 내용은 [AEM forms 데이터베이스](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database))

백업/복원 프로세스에 대해서는 다음 지침을 따르십시오.

* 사용 가능한 운영 체제나 타사 백업 유틸리티를 사용하여 GDS 디렉토리를 백업합니다. (자세한 내용은 [GDS 위치](/help/forms/using/admin-help/files-back-recover.md#gds-location))
* (선택 사항) 사용 가능한 운영 체제나 타사 백업 및 유틸리티를 사용하여 컨텐츠 스토리지 루트 디렉토리를 백업합니다. (자세한 내용은 [컨텐츠 저장 루트 위치(독립 실행형 환경)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-stand-alone-environment) 또는 [컨텐츠 저장소 루트 위치(클러스터된 환경)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-clustered-environment))
* 작성자 및 게시 인스턴스 백업(crx-repository 백업).

   서신 관리 솔루션 환경을 백업하려면 에 설명된 대로 작성 및 게시 인스턴스에 대한 단계를 수행합니다. [백업 및 복원](/help/sites-administering/backup-and-restore.md).

   작성자 및 게시 인스턴스를 백업할 때는 다음 사항을 고려하십시오.

   * 작성자 및 게시 인스턴스에 대한 백업이 동시에 시작되도록 동기화되어야 합니다.백업이 수행되는 동안 작성자 및 게시 인스턴스를 계속 사용할 수 있지만, 캡처되지 않은 변경 내용을 방지하기 위해 백업 중에 자산을 게시하지 않는 것이 좋습니다. 새 자산을 게시하기 전에 작성자 및 게시 인스턴스 둘 다의 백업이 완료될 때까지 기다립니다.
   * 작성자 노드의 전체 백업에는 Forms Manager 및 AEM Forms Workspace 데이터의 백업이 포함됩니다.
   * Workbench 개발자는 로컬로 프로세스를 계속 작업할 수 있습니다. 백업 단계에서 새로운 프로세스를 구축하면 안 됩니다.
   * 각 백업 세션의 길이(롤링 백업 모드의 경우)에 대한 결정은 AEM Forms(DB, GDS, AEM 저장소 및 기타 추가 사용자 지정 데이터)의 모든 데이터를 백업하는 데 걸린 총 시간을 기반으로 해야 합니다.

트랜잭션 로그를 포함하여 AEM Forms 데이터베이스를 백업해야 합니다. (자세한 내용은 [AEM forms 데이터베이스](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database)) 자세한 내용은 데이터베이스에 대한 해당 기술 자료 문서를 참조하십시오.

* [AEM Forms용 백업 및 복구 oracle](https://www.adobe.com/go/kb403624)
* [AEM Forms용 MySQL 백업 및 복구](https://www.adobe.com/go/kb403625)
* [AEM Forms용 Microsoft SQL Server 백업 및 복구](https://www.adobe.com/go/kb403623)
* [AEM Forms용 DB2 백업 및 복구](https://www.adobe.com/go/kb403626)

이 문서에서는 데이터 백업 및 복구를 위한 기본 데이터베이스 기능에 대한 지침을 제공합니다. 특정 공급업체의 데이터베이스 백업 및 복구 기능에 대한 포괄적인 기술 가이드로는 작성할 수 없습니다. AEM Forms 응용 프로그램 데이터에 대한 안정적인 데이터베이스 백업 전략을 만드는 데 필요한 명령의 개요를 설명합니다.

>[!NOTE]
>
>GDS 백업을 시작하기 전에 데이터베이스 백업을 완료해야 합니다. 데이터베이스 백업이 완료되지 않으면 데이터가 동기화되지 않습니다.

### 백업 모드 입력 {#entering-the-backup-modes}

관리 콘솔, LCBackupMode 명령 또는 AEM Forms 설치 시 사용할 수 있는 API를 사용하여 백업 모드를 시작하고 종료할 수 있습니다. 롤링 백업(연속 적용 범위)의 경우 관리 콘솔 옵션을 사용할 수 없습니다. 명령줄 옵션 또는 API를 사용해야 합니다. <!-- Fix broken link For information about using the API to enter and leave backup modes, see AEM forms API Reference on Help and Tutorials page. -->

>[!NOTE]
>
>Forms 서버에 SSL을 구성한 경우 LCBackupMode.CMD 스크립트를 사용하여 Forms 서버를 백업 모드로 배치할 수 없습니다.

**관리 콘솔을 사용하여 안전한 백업 모드로 전환합니다.**

1. 관리 콘솔에 로그인합니다.
1. 설정 > 핵심 시스템 설정 > 백업 유틸리티를 클릭합니다.
1. [안전한 백업 모드에서 작업]을 선택하고 [확인]을 클릭합니다.

   이 방법을 사용하면 AEM Forms가 무기한 백업 모드로 전환되고(제한 시간 없음) 백업 모드가 롤링되지 않고 스냅샷 모드로 전환됩니다.

**명령줄 옵션을 사용하여 안전한 백업 모드로 들어갑니다.**

명령줄 인터페이스를 사용할 수 있습니다 `LCBackupMode` AEM 양식을 안전한 백업 모드로 전환하는 스크립트

1. ADOBE_LIVECYCLE을 설정하고 응용 프로그램 서버를 시작합니다.
1. 로 이동합니다. `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline` 폴더를 입력합니다.
1. 운영 체제에 따라 `LCBackupMode.cmd` 또는 `LCBackupMode.sh` 스크립트에 적절한 기본값을 제공합니다.
1. 명령 프롬프트에서 다음 명령을 한 줄에 실행합니다.

   * (Windows) `LCBackupMode.cmd enter [-Host=`*호스트 이름* `] [-port=`*portnumber* `] [-user=`*사용자 이름* `] [-password=`*암호* `] [-label=`*labelname* `] [-timeout=`*초* `]`
   * (Linux, UNIX) `LCBackupMode.sh enter [-host=`*호스트 이름* `] [-port=`*portnumber* `] [-user=`*사용자 이름* `] [-password=`*암호* `] [-label=`*labelname* `]`

   이전 명령에서 자리 표시자는 다음과 같이 정의됩니다.

   `Host` 는 AEM Forms가 실행 중인 호스트의 이름입니다.

   `port` AEM Forms가 실행 중인 응용 프로그램 서버의 WebServices 포트입니다.

   `user` AEM forms 관리자의 사용자 이름입니다.

   `password` AEM Forms 관리자의 암호입니다.

   `label` 은 이 백업에 대해 임의의 문자열일 수 있는 텍스트 레이블입니다.

   `timeout` 은 백업 모드가 자동으로 남아 있는 시간(초)입니다. 0~10,080일 수 있습니다. 기본값인 0이면 백업 모드는 시간 제한이 없습니다.

   백업 모드에 대한 명령줄 인터페이스에 대한 자세한 내용은 BackupRestoreCommandline 디렉토리의 Readme 파일을 참조하십시오.

### 백업 모드 종료 {#leaving-backup-modes}

관리 콘솔 또는 명령줄 옵션을 사용하여 백업 모드를 종료할 수 있습니다.

**안전한 백업 모드 종료(스냅샷 모드)**

Administration Console을 사용하여 AEM Forms를 안전한 백업 모드(스냅샷 모드)에서 제거하려면 다음 작업을 수행합니다.

1. 관리 콘솔에 로그인합니다.
1. 설정 > 핵심 시스템 설정 > 백업 유틸리티를 클릭합니다.
1. [안전한 백업 모드로 작업]을 선택 취소하고 [확인]을 클릭합니다.

**모든 백업 모드 유지**

명령줄 인터페이스를 사용하여 AEM Forms를 안전한 백업 모드(스냅샷 모드)에서 꺼내거나 현재 백업 모드 세션(롤링 모드)을 종료할 수 있습니다. 관리 콘솔을 사용하여 롤링 백업 모드를 종료할 수 없습니다. 롤링 백업 모드에서 관리 콘솔의 백업 유틸리티 컨트롤이 비활성화됩니다. API 호출을 사용하거나 LCBackupMode 명령을 사용해야 합니다.

1. 로 이동합니다. `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline` 폴더를 입력합니다.
1. 운영 체제에 따라 `LCBackupMode.cmd` 또는 `LCBackupMode.sh` 스크립트에 적절한 기본값을 제공합니다.

   >[!NOTE]
   >
   >JAVA_HOME 디렉토리는 [AEM 양식 설치 준비](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63)*.*

1. 한 줄에 다음 명령을 실행합니다.

   * (Windows) `LCBackupMode.cmd leaveContinuousCoverage [-Host=`*호스트 이름* `] [-port=`*portnumber* `] [-user=`*사용자 이름* `] [-password=`*암호* `]`
   * (Linux, UNIX) `LCBackupMode.sh leaveContinuousCoverage [-Host=`*호스트 이름* `] [-port=`*portnumber* `] [-user=`*사용자 이름* `] [-password=`*암호* `]`

      이전 명령에서 자리 표시자는 다음과 같이 정의됩니다.

      `Host` 는 AEM Forms가 실행 중인 호스트의 이름입니다.

      `port` 은 애플리케이션 서버에서 AEM Forms가 실행 중인 포트입니다.

      `user` AEM forms 관리자의 사용자 이름입니다.

      `password` AEM Forms 관리자의 암호입니다.

      `leaveContinuousCoverage` 롤링 백업 모드를 완전히 비활성화하려면 이 옵션을 사용합니다.
   >[!NOTE]
   >
   >백업 모드가 꺼져 있는 동안에는 연속 적용 범위를 다시 설정할 수 없습니다. 해당 시간 동안의 모든 변경 사항은 보호되지 않습니다.

   >[!NOTE]
   >
   >데이터베이스에서 문서 저장소를 사용하도록 설정하면 스냅샷 백업 모드 및 롤링 백업 모드를 적용할 수 없습니다.

   백업 모드에 대한 명령줄 인터페이스에 대한 자세한 내용은 BackupRestoreCommandline 디렉토리의 readme 파일을 참조하십시오.
