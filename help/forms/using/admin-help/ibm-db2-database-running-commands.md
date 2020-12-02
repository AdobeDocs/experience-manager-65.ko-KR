---
title: '"IBM DB2 데이터베이스:유지 관리를 위한 명령 실행"'
seo-title: '"IBM DB2 데이터베이스:유지 관리를 위한 명령 실행"'
description: 이 문서에서는 AEM 양식 데이터베이스를 정기적으로 유지 관리하는 데 권장되는 IBM DB2 명령을 나열합니다.
seo-description: 이 문서에서는 AEM 양식 데이터베이스를 정기적으로 유지 관리하는 데 권장되는 IBM DB2 명령을 나열합니다.
uuid: 235d59df-b9b9-4770-8b7d-00713701c3c2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a62b68b4-7735-49b1-8938-f0d9e4c4a051
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---


# IBM DB2 데이터베이스:일반 유지 관리를 위한 명령 실행 중 {#ibm-db-database-running-commands-for-regular-maintenance}

AEM 양식 데이터베이스를 정기적으로 유지 관리하는 경우 다음 IBM DB2 명령을 사용하는 것이 좋습니다. DB2 데이터베이스의 유지 관리 및 성능 조정에 대한 자세한 내용은 *IBM DB2 관리 가이드*&#x200B;를 참조하십시오.

* **runstats:** 이 명령은 데이터베이스 테이블의 물리적 특성을 설명하는 통계와 관련 인덱스를 업데이트합니다. AEM 양식에 의해 생성된 동적 SQL 문은 이러한 업데이트된 통계를 자동으로 사용하지만 데이터베이스 내에 구축된 정적 SQL 문은 `db2rbind` 명령도 실행해야 합니다.
* **db2rbind:** 이 명령은 데이터베이스의 모든 패키지를 다시 바인딩합니다. `runstats` 유틸리티를 실행한 후 이 명령을 사용하여 데이터베이스의 모든 패키지의 유효성을 다시 확인하십시오.
* **테이블 또는 인덱스 재구성:** 이 명령은 일부 테이블과 색인의 재구성이 필요한지 여부를 확인합니다.

   데이터베이스가 증가하고 변경됨에 따라 테이블 통계를 다시 계산하면 데이터베이스 성능을 향상하는 데 매우 중요하므로 정기적으로 수행해야 합니다. 이러한 명령은 스크립트를 사용하거나 복제 작업을 사용하여 수동으로 실행할 수 있습니다.

>[!NOTE]
>
>`runstats` 명령을 실행하기 전에 데이터베이스에 데이터가 있어야 하며 하나 이상의 디렉터리 동기화를 수행해야 합니다.

사용자 10,000명 또는 2,500개 그룹과 같은 작은 데이터베이스의 경우 `runstats` 명령을 호출하여 동기화 시간을 줄이는 것이 충분합니다.

사용자 100,000명 또는 그룹 10,000개 등과 같은 대용량 데이터베이스의 경우 `reorg` 명령을 실행한 후 `runstats` 명령을 실행합니다.

## AEM 양식 데이터베이스 {#use-the-runstats-command-on-your-aem-forms-database}에서 runstats 명령을 사용합니다.

다음 AEM 양식 데이터베이스 테이블 및 인덱스에서 `runstats` 명령을 실행합니다.

>[!NOTE]
>
>`runstats` 명령은 첫 번째 데이터베이스 동기화 동안에만 실행해야 합니다. 그러나 이 프로세스 동안 두 번 실행해야 합니다.사용자 및 그룹을 동기화한 다음 그룹 구성원을 동기화하는 동안 한 번 스크립트를 실행할 때마다 스크립트가 완전히 실행되도록 합니다.

올바른 구문 및 사용법을 보려면 데이터베이스 제조업체 설명서를 참조하십시오. 아래에서 `<schema>`은 DB2 사용자 이름과 연결된 스키마를 나타내는 데 사용됩니다. 간단한 기본 DB2 설치가 있는 경우 데이터베이스 스키마 이름입니다.

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

## AEM 양식 데이터베이스 {#run-the-reorg-command-on-your-aem-forms-database}에서 reorg 명령을 실행합니다.

다음 AEM 양식 데이터베이스 테이블 및 인덱스에서 `reorg` 명령을 실행합니다. 올바른 구문 및 사용법을 보려면 데이터베이스 제조업체 설명서를 참조하십시오.

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

