---
title: EMC Documentum 저장소 백업 및 복구
description: 이 문서에서는 AEM Forms 환경에 맞게 구성된 EMC Documentum 저장소를 백업 및 복구하는 데 필요한 작업에 대해 설명합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: bc21659f-88d6-4dff-8baf-12746e1b3ed9
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 0%

---

# EMC Documentum 저장소 백업 및 복구 {#backing-up-and-recovering-the-emc-documentum-repository}

이 섹션에서는 AEM Forms 환경에 대해 구성된 EMC Documentum 저장소를 백업 및 복구하는 데 필요한 작업에 대해 설명합니다.

>[!NOTE]
>
>이 지침에서는 필요에 따라 ECM 및 EMC Documentum Content Server용 커넥터를 사용하는 AEM Forms가 설치 및 구성되어 있다고 가정합니다.

백업 및 복원 프로세스에는 두 가지 주요 작업이 있습니다.

* AEM Forms 환경 백업(또는 복원)
* EMC Documentum Content Server 백업(또는 복원)

>[!NOTE]
>
>EMC Documentum 시스템을 백업하기 전에 AEM Forms 데이터를 백업한 다음 AEM Forms 환경을 복원하기 전에 EMC Documentum 시스템을 복원합니다.

## 소프트웨어 요구 사항 {#software-requirements}

EMC Documentum Content Server에서 필요한 백업 작업을 수행하려면 EMC의 EMC NetWorker 또는 CYA의 CYA SmartRecovery for EMC Documentum과 같은 타사 유틸리티를 구입하십시오. 다음 지침에서는 EMC NetWorker Module 버전 7.2.2를 사용하는 단계에 대해 설명합니다.

다음과 같은 EMC NetWorker 모듈이 필요합니다.

* NetWorker 모듈
* NetWorker 구성 마법사
* NetWorker 디바이스 구성 마법사
* Content Server에서 사용하는 데이터베이스 유형에 대한 NetWorker Module
* NetWorker Module for Documentum

## 백업 및 복구를 위한 EMC Document Content Server 준비 {#preparing-the-emc-document-content-server-for-backup-and-recovery}

이 섹션에서는 Content Server에 EMC NetWorker 소프트웨어를 설치하고 구성하는 방법에 대해 설명합니다.

**백업을 위해 EMC Documentum 서버 준비**

1. EMC Documentum Content Server에 EMC NetWorker 모듈을 설치하고 모든 기본값을 적용합니다.

   설치 프로세스 중에 Content Server 컴퓨터의 서버 이름을 로 입력하라는 메시지가 표시됩니다. *NetWorker Server 이름*. 데이터베이스에 EMC NetWorker Module을 설치할 때 &quot;전체&quot; 설치를 선택합니다.

1. 아래 샘플 콘텐츠를 사용하여 이라는 구성 파일을 만듭니다. *nsrnmd_win.cfg* Content Server의 액세스 가능한 위치에 저장합니다. 이 파일은 백업 및 복원 명령에 의해 호출됩니다.

   다음 텍스트에는 줄 바꿈에 사용할 서식 문자가 포함되어 있습니다. 이 텍스트를 이 문서 외부 위치에 복사하는 경우 새 위치에 붙여넣을 때 한 번에 일부를 복사하고 서식 문자를 제거합니다.

   ```shell
    ################################################
    # NetWorker Module for Documentum v1.2 nsrnmd_win.cfg D5.3+ example with
    # typical set of working parameters.  THIS FILE MUST BE SITE-CUSTOMISED.
    #
    # Parameters not shown can be set in this file (as per site customisation) #or from the command-line.
    #
    # See the user Guides for details on all parameters, including
    # those not listed below.
    # Note: DCTM environment for D6 is slightly different from D5, refer to D6
    # Installation Guide to update the values.
    ################################################
    #Can get values for most of below from doing as the dctm inst owner: cmd> set DOCUMENTUM=C:\Documentum
    DM_HOME=C:\Documentum\product\6.0
    JAVA_HOME=C:\Progra~1\Documentum\java\1.5.0_12
    JAVA_PATH=C:\Progra~1\Documentum\java\1.5.0_12\bin
    PATH=C:\WINNT\system32;C:\WINNT;C:\WINNT\system32\WBEM;C:\Documentum\product\6.0\bin;C:\Documentum\fulltext\fast;C:\Documentum\product\6.0\fusion;C:\Program Files\Documentum\Shared;C:\Program Files\Legato\nsr\bin;C:\Program Files\Microsoft SQL Server\80\Tools\Binn;C:\Program Files\Microsoft SQL Server\90\DTS\Binn\;C:\Program Files\Microsoft SQL Server\90\Tools\binn;C:\Program Files\Microsoft SQL Server\90\Tools\Binn\VSShell\Common7\IDE;C:\Program Files\Documentum\java\1.5.0_12\bin;C:\Documentum\config;C:\Documentum
    #See also manifest dctm.jar file for class path locations
    CLASSPATH=.;C:\Program Files\Legato\nsr\bin;C:\Program Files\Legato\nsr\bin\nsrnmdde.jar;C:\Program Files\Documentum\java\1.5.0_12\lib\tools.jar;C:\Program Files\Documentum\Shared\dfc.jar;C:\Program Files\Documentum\Shared\aspectjrt.jar;C:\Program Files\Documentum\dctm.jar;C:\Program Files\Documentum\Shared\workflow.jar;C:\Program Files\Documentum\Shared\log4j.jar;C:\Program Files\Documentum\java\1.5.0_12\lib\dt.jar;C:\Documentum\config
   
    ################################################
    #If not using nsrnmdsv -m ALL|DB|DB_LOG|FTI|FTI_ALL|ICF|SA|SA_ALL, set #for backup
    NMD_SCOPE=ALL
    #Mandatory when scope (backup or restore) is FTI/SA without -a option
    #NMD_OBJECT_NAME=filestore_01
    ################################################
    NMDDE_DM_DOCBASE=Docbase
    NMDDE_DM_USER=Administrator
    #NMDDE_DM_PASSWD must be set via running: nsrnmdsv -f <nmdcfg> -P <pwd>.
    ################################################
    #DB related hooks to invoke arbitrary scripts:
    #Set if DB is on a remote host
    #NMD_DB_HOST=dbhost
    #Pure basename implies remote host execution; absolute path ... local
    #execution as in NMD v1.0.
    #
    #Remote execution requires script be put in remote nsrexecd bin directory
    #and D5.3+ host be added to remote nsr\res\servers file w/ nsrexecd recycled
    #
    #Refer to user Guides for sample script code.
    NMD_DB_FULL_BACKUP_CMD=C:\DocumentumBackup\Scripts\nsrnmddbf.bat
    NMD_DB_LOG_BACKUP_CMD=C:\DocumentumBackup\Scripts\nsrnmddbl.bat
    NMD_DB_INCR_BACKUP_CMD=C:\DocumentumBackup\Scripts\nsrnmddbi.bat
    ################################################
    #For D5.3+ only: NMD_FTI_INCLUDED, NMD_FTI_HOST, NMD_FTI_USER,
    #NMD_FTI_PASSWD & NMD_FTI_SUBDIRS.
    #Optional for remote D5.3+ FTI server
    NMD_FTI_INCLUDED=no
    #NMD_FTI_HOST=ftihost
    #Recommended for D5.3+ FTI server quiesce/unquiesce
    #NMD_FTI_USER=ftiadmin
    #The index name: optional for D5.3+ FTI server, used with -M FTI_ALL or
    #-M ALL
    #NMD_FTI_NAME=rep_name_ftindex_01
    #Recommended for D5.3+ FTI server quiesce/unquiesce
    #NMDDE_FTI_PASSWD must be set via running: nsrnmdsv -f <nmdcfg> -P <pwd>
    #-M FTI.
    #Pure basename implies remote host execution; absolute path ... local execution
    #as in NMD v1.0.
    #
    #Remote execution requires script be put in remote nsrexecd bin directory
    #and D5.3+ host be added to remote nsr\res\servers file w/ nsrexecd
    #recycled.
    #
    #See example nsrnmdfti*.bat examples.
    #
    #Mandatory for D5.3+
    #NMD_BACKUP_FTI_QUIESCE=nsrnmdftiq.bat
    #NMD_BACKUP_FTI_UNQUIESCE=nsrnmdftiu.bat
    #Used for D5.3+ to get InstallProfile.xml FTI file in multinode
    #discovery.
    #Optional, if not specified, will treat as single-node FTI.
    #NMD_FTI_GET_INSTPROF=nsrnmdfti_instprof.bat
    #Mandatory for D5.3+. No spaces in paths or around comma separators.
    #For remote FTI, paths must be valid at the FTI host.
    #NMD_FTI_SUBDIRS=F:\Documentum_idx\data\fulltext\fixml,F:\Documentum_idx
    #\data\fulltext\index
    ################################################
    #Mandatory. No spaces in paths or before comma
    #separators in NMD_ICF_SUBDIRS_xxx:
    #NMD_ICF_INCLUDED=yes
    #NMD_ICF_SUBDIRS=C:\Documentum\dba,C:\Documentum\product\5.3
    ################################################
    NMD_FILEREPORT_INCLUDED=yes
    NMDDE_METADATA_OUTPUT_DEST=C:\docbase_freports\
    ################################################
    #Other misc recommended NMD_xxx parameters
    #Recommended to get more meaningful saveset names
    NMD_USE_DEFAULT_SAVESET_NAMES=yes
    #Use following to skip unwanted ICF, FTI and non-SnapImage SA dirs/files.
    #For example, "<</>> +skip: dm_ftwork_dir" line will skip non-data
    #files.
    #
    #The path will be the same and must exist on D5.3+, remote FTI host, and
    #RCS hosts correspondingly if used.
    #NMD_DIRECTIVES_FILE=E:\Program Files\Legato\nsr\res\nsrnmddirectives.txt
    #For non-SnapImage SA backup
    #NMD_SA_FULL_NUM_SAVESET=16
    #NMD_SA_INCR_NUM_SAVESET=4
    #NMD_USE_SNAPIMAGE=yes
    ################################################
    # DSA setup
    ################################################
    # Name of the config file at the remote sites;
    # Mandatory, listed in the config file at the primary host.
    # (if skipped, backup is treated as local)
    # NMD_RCS_CFG_FILE=rep_name_rcs.cfg
   
    # SA-host mapping add, optional, will override far-store list info.
    # No space around comma.
    # NMD_HOST_SAS_MAP=host01,sa_01,sa_02
    # NMD_HOST_SAS_MAP=host02,sa_03
    ################################################
    NSR_SERVER=con-dctm
    #NSR_CLIENT=d5svrhost
    NSR_GROUP=Default
    NSR_DATA_VOLUME_POOL=Default
    #NSR_SNAPIMAGE_DATA_VOLUME_POOL=Default
    #Relocation dir will be the same on D5+ and remote FTI/SA hosts.
    NSR_RELOCATION=C:\reloc
    #NSR_PARALLELISM=16
    NSR_DEBUG_FILE=C:\Program Files\Legato\nsr\applogs\nmd.log
    NSR_DEBUG_LEVEL=9
    ################################################
    NMDDE_DM_PASSWD=XAtup9pl
   ```

   구성 파일 암호 필드 유지 `NMDDE_DM_PASSWD` 비어 있음. 다음 단계에서 암호를 설정합니다.

1. 구성 파일 암호를 다음과 같이 설정합니다.

   * 명령 프롬프트를 열고 다음으로 변경 `[NetWorker_root]\Legato\nsr\bin`.
   * 다음 명령을 실행합니다. `-nsrnmdsv.exe -f`*&lt;path_to_cfg_file> -P &lt;password>*

1. 데이터베이스를 백업하는 데 사용되는 실행 가능한 일괄 처리(.bat) 파일을 만듭니다. NetWorker 설명서를 참조하십시오. 설치에 따라 배치 파일에서 세부 사항을 설정합니다.

   * 전체 데이터베이스 백업(nsrnmdbf.bat):

     `NetWorker_database_module_root` `-s`*&lt;networker_server_name>* `-U``[username]` `-P`*[암호&#x200B;]*`-l full`*&lt;database_name>*

   * 증분 데이터베이스 백업(nsrnmdbi.bat):

     `[NetWorker_database_module_root]` `-s`*&lt;NetWorker_Server_Name>* `-U``[username]` `-P``[password]` `-l 1 -R`*&lt;database_name>*

   * 데이터베이스 로그 백업(nsrnmddbl.bat):

     `[NetWorker_database_module_root]` `-s``<NetWorker_Server_Name>` `-U``[username]` `-P``[password]` `-l incr -R`*&lt;database_name>*

     위치:

     `[NetWorker_database_module_root]` 는 NetWorker Module의 설치 디렉토리입니다. 예를 들어 NetWorker Module for SQL Server의 기본 설치 디렉토리는 C:\Program Files\Legato\nsr\bin\nsrsqlsv입니다.

     `NetWorker_Server_Name` 는 NetWorker가 설치된 서버입니다.

     `username` 및 `password` 는 데이터베이스 관리자 사용자의 사용자 이름과 암호입니다.

     `database_name` 는 백업할 데이터베이스의 이름입니다.

**백업 장치 만들기**

1. EMC Documentum 서버에 디렉토리를 만들고 모든 사용자에게 모든 권한을 부여하여 폴더를 공유합니다.
1. EMC NetWorker Administrator 를 시작하고 Media Management > Devices 를 클릭합니다.
1. 장치 를 마우스 오른쪽 단추로 클릭하고 만들기 를 선택합니다.
1. 다음 값을 입력하고 확인을 누릅니다.

   **이름:** 공유 디렉토리의 전체 경로

   **미디어 유형:** `File`

1. 새 장치를 마우스 오른쪽 단추로 클릭하고 작업을 선택합니다.
1. 레이블 을 클릭하고 이름을 입력한 다음 확인 을 클릭하고 마운트 를 클릭합니다.

백업된 파일을 저장할 장치가 추가됩니다. 서로 다른 형식의 여러 장치를 추가할 수 있습니다.

## EMC Documentum Content Server 백업 {#back-up-the-emc-documentum-content-server}

AEM Forms 데이터의 전체 백업을 완료한 후 다음 작업을 수행합니다. (참조: [AEM 양식 데이터 백업](/help/forms/using/admin-help/backing-aem-forms-data.md#backing-up-the-aem-forms-data).)

>[!NOTE]
>
>명령 스크립트는에서 작성한 nsrnmd_win.cfg 파일에 대한 전체 경로가 필요합니다 [백업 및 복구를 위한 EMC Document Content Server 준비](backing-recovering-emc-documentum-repository.md#preparing-the-emc-document-content-server-for-backup-and-recovery).

1. 명령 프롬프트를 열고 다음으로 변경 `[NetWorker_root]\Legato\nsr\bin`.
1. 다음 명령을 실행합니다.

   ```shell
    - nsrnmdsv.exe -f <path_to_cfg_file>
   ```

## EMC Documentum Content Server 복구 {#restore-the-emc-documentum-content-server}

AEM Forms 데이터를 복원하기 전에 다음 작업을 수행하십시오. (참조: [AEM 양식 데이터 복구](/help/forms/using/admin-help/recovering-aem-forms-data.md#recovering-the-aem-forms-data).)

>[!NOTE]
>
>명령 스크립트는에서 작성한 nsrnmd_win.cfg 파일에 대한 전체 경로가 필요합니다 [백업 및 복구를 위한 EMC Document Content Server 준비](backing-recovering-emc-documentum-repository.md#preparing-the-emc-document-content-server-for-backup-and-recovery).

1. 복원 중인 Docbase 서비스를 중지합니다.
1. 데이터베이스 모듈에 대한 NetWorker User 유틸리티를 시작합니다(예: *NetWorker User for SQL Server*).
1. [복원 도구]를 클릭한 다음 [보통]을 선택합니다.
1. 화면 왼쪽에서 Docbase에 대한 데이터베이스를 선택하고 도구 모음에서 시작 단추를 클릭합니다.
1. 데이터베이스가 복원되면 Docbase 서비스를 다시 시작합니다.
1. 명령 프롬프트를 열고 다음으로 변경 *[NetWorker_root]*\Legato\nsr\bin
1. 다음 명령을 실행합니다.

   ```shell
    - nsrnmdrs.exe -B <docbase_name> -f <path_to_cfg_file> -C SA
   ```
