---
title: 상태 모니터 개요
description: 이 문서에서는 상태 모니터에 대한 개요와 상태 모니터에 액세스하는 방법에 대한 세부 정보를 제공합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 05f8b430-141e-4921-98b1-a0d8f636e478
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '296'
ht-degree: 100%

---

# 상태 모니터 개요 {#overview-of-health-monitor}

상태 모니터는 서버 정보, 메모리 사용량, 프로세서 사용량과 같이 AEM Forms 시스템에 대한 중요한 정보를 제공합니다. 대기열에 있는 작업 항목 또는 작업 수 및 해당 상태와 같은 작업 관리자 통계도 사용할 수 있습니다. 상태 모니터를 사용하여 다음 작업을 수행할 수 있습니다.

* 시스템이 제대로 실행되고 있는지 확인합니다.
* 시스템 문제가 발생할 때 이를 진단하는 데 도움이 되는 정보를 확인합니다.
* 문제가 표시되는 작업 항목 또는 작업에 대한 작업을 수행합니다.
* 작업 관리자 데이터베이스에서 더 이상 사용되지 않는 레코드를 제거합니다.

관리 콘솔의 상태 모니터 페이지에는 다음과 같은 세 가지 탭이 있습니다.

* 시스템 탭에는 리소스 모니터링 차트와 Forms 서버(또는 클러스터링된 환경의 노드)에 대한 정보가 표시됩니다. ([시스템 정보 보기](/help/forms/using/admin-help/view-system-information.md#view-system-information)를 참조하십시오.)
* 작업 관리자 탭에는 작업 관리자 대기열에 있는 작업 항목 수와 같이 작업 관리자와 관련된 데이터가 표시됩니다. 다양한 기준을 사용하여 정보를 필터링하거나 작업 도구를 사용하여 개별 작업 항목을 관리할 수 있습니다. ([작업 관리자와 관련된 통계 보기](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager)를 참조하십시오.)
* 제거 작업 스케줄러 탭을 사용하면 작업 관리자 데이터베이스에서 더 이상 사용되지 않는 레코드를 제거할 수 있습니다. ([작업 관리자 데이터베이스에서 레코드 제거](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database)를 참조하십시오.)

상태 모니터 웹 페이지는 Gemfire API를 통해 수집된 통계로 채워져 있습니다. 이 API는 클러스터의 모든 노드를 자동으로 검색합니다. 프록시 서버나 로드 밸런서 뒤에서 통계를 수집할 때 발생하는 보안 문제도 해결합니다. Java 옵션을 사용하면 상태 모니터를 세부 조정하여 AEM Forms 환경 성능에 미치는 영향을 줄일 수 있습니다. ([상태 모니터 성능 세부 조정](/help/forms/using/admin-help/fine-tuning-health-monitor-performance.md#fine-tuning-health-monitor-performance)을 참조하십시오.)

**상태 모니터 액세스**

1. 관리 콘솔에서 페이지 오른쪽 상단에 있는 상태 모니터를 클릭합니다.
