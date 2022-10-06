---
title: "IBM DB2 데이터베이스: 일반 유지 관리를 위한 명령 실행"
seo-title: "IBM DB2 database: Running commands for regular maintenance"
description: 이 문서에서는 AEM Forms 데이터베이스를 정기적으로 유지 관리하는 데 권장되는 IBM DB2 명령을 나열합니다.
seo-description: This document lists IBM DB2 commands that are recommended for regular maintenance of your AEM forms database.
uuid: 235d59df-b9b9-4770-8b7d-00713701c3c2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a62b68b4-7735-49b1-8938-f0d9e4c4a051
exl-id: 7a4281e7-1544-473a-a471-e9a4c2819a58
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# IBM DB2 데이터베이스: 일반 유지 관리를 위한 명령 실행 {#ibm-db-database-running-commands-for-regular-maintenance}

AEM Forms 데이터베이스를 정기적으로 유지 관리할 때는 다음 IBM DB2 명령을 사용하는 것이 좋습니다. DB2 데이터베이스의 유지 관리 및 성능 조정에 대한 자세한 내용은 *IBM DB2 관리 안내서*.

* **runstats:** 이 명령은 데이터베이스 테이블의 물리적 특성을 설명하는 통계를 관련 인덱스와 함께 업데이트합니다. AEM Forms에서 생성된 동적 SQL 문은 이러한 업데이트된 통계를 자동으로 사용하지만 데이터베이스 내에 작성된 정적 SQL 문은 `db2rbind` 명령도 실행할 수 있습니다.
* **db2rbind:** 이 명령은 데이터베이스의 모든 패키지를 다시 바인딩합니다. 실행 후 이 명령 사용 `runstats` 데이터베이스의 모든 패키지의 유효성을 다시 검사하는 유틸리티입니다.
* **테이블 또는 인덱스 재구성:** 이 명령은 일부 테이블 및 인덱스를 재구성해야 하는지 여부를 확인합니다.

   데이터베이스가 늘어나고 변경됨에 따라 테이블 통계를 다시 계산하는 것은 데이터베이스 성능을 향상시키기 위해 매우 중요하므로 정기적으로 수행해야 합니다. 이러한 명령은 스크립트를 사용하거나 크론 작업을 사용하여 수동으로 실행할 수 있습니다.

>[!NOTE]
>
>를 실행하기 전에 `runstats` 명령을 실행하면 데이터베이스에 데이터가 있어야 하며 하나 이상의 디렉터리 동기화가 수행되어야 합니다.

사용자 10,000명 또는 2,500개 그룹과 같은 작은 데이터베이스의 경우 `runstats` 명령을 사용하여 동기화 시간을 줄입니다.

사용자 10만 명 또는 그룹 10,000명과 같은 대규모 데이터베이스의 경우 `reorg` 명령을 실행하기 전에 `runstats` 명령.

## AEM Forms 데이터베이스에서 runstats 명령을 사용합니다 {#use-the-runstats-command-on-your-aem-forms-database}

를 실행합니다. `runstats` 다음 AEM forms 데이터베이스 테이블 및 인덱스에 대한 명령.

>[!NOTE]
>
>다음 `runstats` 명령은 첫 번째 데이터베이스 동기화 동안에만 실행해야 합니다. 그러나 이 프로세스는 다음 프로세스 동안 두 번 실행해야 합니다. 사용자 및 그룹 동기화 중에 한 번, 그룹 구성원 동기화 중에 한 번. 스크립트를 실행할 때마다 스크립트가 완전히 실행되는지 확인합니다.

올바른 구문 및 사용법을 보려면 데이터베이스 제조업체의 설명서를 참조하십시오. 아래, `<schema>` 는 DB2 사용자 이름과 연관된 스키마를 나타내는 데 사용됩니다. 간단한 기본 DB2 설치가 있는 경우 데이터베이스 스키마 이름입니다.

```sql
     TABLE <schema>.EDCPRINCIPALGROUPENTITY
 
     TABLE <schema>.EDCPRINCIPALGRPCTMNTENTITY
 
     TABLE <schema>.EDCPRINCIPALENTITY
 
     TABLE <schema>.EDCPRINCIPALUSERENTITY
 
     TABLE <schema>.EDCPRINCIPALEMAILALIASENTITY
 
     TABLE <schema>.EDCPRINCIPALENTITY FOR INDEXES ALL
 
     TABLE <schema>.EDCPRINCIPALEMAILALIASENTITY FOR INDEXES ALL
 
     TABLE <schema>.EDCPRINCIPALUSERENTITY FOR INDEXES ALL
 
     TABLE <schema>.EDCPRINCIPALGROUPENTITY FOR INDEXES ALL
 
     TABLE <schema>.EDCPRINCIPALGRPCTMNTENTITY FOR INDEXES ALL
```

## AEM Forms 데이터베이스에서 reorg 명령을 실행합니다. {#run-the-reorg-command-on-your-aem-forms-database}

를 실행합니다. `reorg` 다음 AEM forms 데이터베이스 테이블 및 인덱스에 대한 명령. 올바른 구문 및 사용법을 보려면 데이터베이스 제조업체의 설명서를 참조하십시오.

```sql
     TABLE <schema>.EDCPRINCIPALGROUPENTITY
 
     TABLE <schema>.EDCPRINCIPALGRPCTMNTENTITY
 
     TABLE <schema>.EDCPRINCIPALENTITY
 
     TABLE <schema>.EDCPRINCIPALUSERENTITY
 
     TABLE <schema>.EDCPRINCIPALEMAILALIASENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALEMAILALIASENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALUSERENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALGROUPENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALGRPCTMNTENTITY
```
