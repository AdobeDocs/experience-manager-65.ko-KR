---
title: "IBM DB2 데이터베이스: 정기 유지 관리를 위한 명령 실행"
description: 이 문서에서는 AEM Forms 데이터베이스의 정기적인 유지 관리에 권장되는 IBM DB2 명령을 나열합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7a4281e7-1544-473a-a471-e9a4c2819a58
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# IBM DB2 데이터베이스: 정기 유지 관리를 위한 명령 실행 {#ibm-db-database-running-commands-for-regular-maintenance}

AEM Forms 데이터베이스를 정기적으로 유지 관리하려면 다음 IBM DB2 명령을 사용하는 것이 좋습니다. DB2 데이터베이스의 유지 관리 및 성능 조정에 대한 자세한 내용은 *IBM DB2 관리 안내서*.

* **runstats:** 이 명령은 관련 인덱스와 함께 데이터베이스 테이블의 물리적 특성을 설명하는 통계를 업데이트합니다. AEM Forms에서 생성된 동적 SQL 문은 이러한 업데이트된 통계를 자동으로 사용하지만 데이터베이스 내에 빌드된 정적 SQL 문에는 `db2rbind` 명령도 실행합니다.
* **db2rbind:** 이 명령은 데이터베이스의 모든 패키지를 다시 바인딩합니다. 를 실행한 후 이 명령 사용 `runstats` 데이터베이스의 모든 패키지를 다시 확인하는 유틸리티입니다.
* **재구성 테이블 또는 색인:** 이 명령은 일부 테이블 및 색인의 재구성이 필요한지 여부를 확인합니다.

  데이터베이스가 증가하고 변경될 때 테이블 통계를 다시 계산하는 것은 데이터베이스 성능을 향상시키는 데 매우 중요하며 정기적으로 수행해야 합니다. 이러한 명령은 스크립트를 사용하거나 cron 작업을 사용하여 수동으로 실행할 수 있습니다.

>[!NOTE]
>
>실행하기 전에 `runstats` 명령에서 데이터베이스에 데이터가 있어야 하며 하나 이상의 디렉터리 동기화가 수행되어야 합니다.

10,000명의 사용자 또는 2,500개의 그룹 등 소규모 데이터베이스의 경우 `runstats` 동기화 시간을 줄이는 명령입니다.

100,000명의 사용자 또는 10,000개의 그룹과 같이 규모가 큰 데이터베이스의 경우 `reorg` 명령을 실행한 후 `runstats` 명령입니다.

## AEM Forms 데이터베이스에서 runstats 명령 사용 {#use-the-runstats-command-on-your-aem-forms-database}

실행 `runstats` 다음 AEM forms 데이터베이스 테이블 및 인덱스에 대한 명령입니다.

>[!NOTE]
>
>다음 `runstats` 명령은 첫 번째 데이터베이스 동기화 중에만 실행해야 합니다. 그러나 이 프로세스는 사용자 및 그룹을 동기화하는 동안 한 번, 그룹 구성원을 동기화하는 동안 두 번 실행해야 합니다. 실행할 때마다 스크립트가 완전히 실행되는지 확인합니다.

올바른 구문 및 사용법은 데이터베이스 제조업체의 설명서를 참조하십시오. 아래, `<schema>` 는 DB2 사용자 이름과 연결된 스키마를 나타내는 데 사용됩니다. 간단한 기본 DB2 설치가 있는 경우 데이터베이스 스키마 이름입니다.

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

## AEM Forms 데이터베이스에서 reorg 명령을 실행합니다 {#run-the-reorg-command-on-your-aem-forms-database}

실행 `reorg` 다음 AEM forms 데이터베이스 테이블 및 인덱스에 대한 명령입니다. 올바른 구문 및 사용법은 데이터베이스 제조업체의 설명서를 참조하십시오.

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
