---
title: 'IBM DB2 데이터베이스: 정기적 유지 관리를 위한 명령 실행'
description: 이 문서에는 AEM Forms 데이터베이스를 정기적으로 유지 관리하는 데 권장되는 IBM DB2 명령이 나열되어 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7a4281e7-1544-473a-a471-e9a4c2819a58
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '391'
ht-degree: 100%

---

# IBM DB2 데이터베이스: 정기적 유지 관리를 위한 명령 실행 {#ibm-db-database-running-commands-for-regular-maintenance}

다음과 같은 IBM DB2 명령은 AEM Forms 데이터베이스를 정기적으로 유지 관리하는 데 권장됩니다. DB2 데이터베이스의 유지 관리 및 성능 조정에 대한 자세한 내용은 *IBM DB2 관리 안내서*&#x200B;를 참조하십시오.

* **runstats:** 이 명령은 데이터베이스 테이블의 물리적 특성을 설명하는 통계와 연결된 색인을 업데이트합니다. AEM Forms에서 생성된 동적 SQL 문은 업데이트된 해당 통계를 자동으로 사용하지만, 데이터베이스 내부에 빌드된 정적 SQL 문은 `db2rbind` 명령도 실행해야 합니다.
* **db2rbind:** 이 명령은 데이터베이스에 있는 모든 패키지를 리바인딩합니다. `runstats` 유틸리티를 실행한 후 이 명령을 사용하면 데이터베이스에 있는 모든 패키지의 유효성을 다시 검사할 수 있습니다.
* **reorg table or index:** 이 명령은 일부 테이블과 색인을 재구성해야 하는지 여부를 확인합니다.

  데이터베이스가 커지고 변경됨에 따라 테이블 통계를 다시 계산하는 작업은 데이터베이스 성능을 향상하는 데 중요하며 정기적으로 수행되어야 합니다. 이러한 명령은 스크립트를 사용하여 수동으로 실행하거나 Cron 작업을 사용하여 실행할 수 있습니다.

>[!NOTE]
>
>`runstats` 명령을 실행하기 전에 데이터베이스에 데이터가 있어야 하며 디렉터리 동기화가 하나 이상 수행되어야 합니다.

사용자 10,000명 또는 그룹 2,500개와 같은 작은 데이터베이스의 경우 `runstats` 명령을 호출하여 동기화 타이밍을 줄이는 것만으로도 충분합니다.

사용자 100,000명 또는 그룹 10,000개와 같은 대규모 데이터베이스의 경우 먼저 `reorg` 명령을 실행한 후에 `runstats` 명령을 실행합니다.

## AEM Forms 데이터베이스에서 runstats 명령 사용 {#use-the-runstats-command-on-your-aem-forms-database}

다음과 같은 AEM Forms 데이터베이스 테이블과 색인에서 `runstats` 명령을 실행합니다.

>[!NOTE]
>
>`runstats` 명령은 첫 번째 데이터베이스 동기화 중에만 실행하면 됩니다. 하지만 해당 프로세스 동안에는 두 번 실행해야 합니다. 첫 번째는 사용자 및 그룹을 동기화하는 동안이고, 두 번째는 그룹 멤버를 동기화하는 동안입니다. 스크립트를 실행할 때마다 스크립트가 완전히 실행되는지 확인하십시오.

올바른 구문과 사용법은 데이터베이스 제조업체의 설명서를 참조하십시오. 아래에서 `<schema>`는 DB2 사용자 이름과 연결된 스키마를 나타내는 데 사용됩니다. 간단한 기본 DB2 설치를 사용하고 있는 경우 이 값이 데이터베이스 스키마 이름이 됩니다.

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

## AEM Forms 데이터베이스에서 reorg 명령 실행 {#run-the-reorg-command-on-your-aem-forms-database}

다음과 같은 AEM Forms 데이터베이스 테이블과 색인에서 `reorg` 명령을 실행합니다. 올바른 구문과 사용법은 데이터베이스 제조업체의 설명서를 참조하십시오.

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
