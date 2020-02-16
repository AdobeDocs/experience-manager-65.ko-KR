---
title: 상태 모니터 개요
seo-title: 상태 모니터 개요
description: 이 문서에서는 상태 모니터의 개요와 이 모니터에 액세스할 수 있는 방법에 대한 세부 정보를 제공합니다.
seo-description: 이 문서에서는 상태 모니터의 개요와 이 모니터에 액세스할 수 있는 방법에 대한 세부 정보를 제공합니다.
uuid: 5934fd2d-80a5-4c6d-b3ee-882c2865705b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c303e967-944d-40b0-96ca-f91e2f42a0d0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 상태 모니터 개요 {#overview-of-health-monitor}

상태 모니터는 서버 정보, 메모리 사용 및 프로세서 사용과 같은 AEM 양식 시스템에 대한 중요한 정보를 제공합니다. 또한 대기열에 있는 작업 항목 또는 작업 수 및 상태 등의 작업 관리자 통계도 사용할 수 있습니다. 상태 모니터를 사용하여 다음 작업을 수행할 수 있습니다.

* 시스템이 제대로 실행되고 있는지 확인
* 시스템 문제가 발생할 때 진단하는 데 도움이 되는 정보 보기
* 문제를 표시하는 작업 항목 또는 작업에 대해 작업 수행
* 작업 관리자 데이터베이스에서 오래된 레코드 제거

관리 콘솔의 상태 모니터 페이지에는 다음 세 개의 탭이 있습니다.

* [시스템] 탭은 리소스 모니터링 차트와 양식 서버(또는 클러스터된 환경의 노드)에 대한 정보를 표시합니다. 자세한 내용은 [시스템 정보](/help/forms/using/admin-help/view-system-information.md#view-system-information)보기를 참조하십시오.
* 작업 관리자 탭에는 작업 관리자 큐의 작업 항목 수와 같이 작업 관리자와 관련된 데이터가 표시됩니다. 다양한 기준을 사용하여 정보를 필터링하거나 작업 도구를 사용하여 개별 작업 항목을 관리할 수 있습니다. (작업 [관리자와 관련된 통계 보기를 참조하십시오](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager).)
* [작업 제거 스케줄러] 탭을 사용하여 작업 관리자 데이터베이스에서 오래된 레코드를 제거할 수 있습니다. 작업 [관리자 데이터베이스에서](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database)레코드 제거를 참조하십시오.

상태 모니터 웹 페이지는 Gemfire API를 통해 수집한 통계로 채워집니다. 이 API는 클러스터의 모든 노드를 자동으로 검색합니다. 또한 프록시 서버 또는 로드 밸런서 뒤에서 통계를 수집할 때 발생하는 보안 문제를 해결합니다. Java 옵션을 사용하여 상태 모니터를 세밀하게 조정하여 AEM 양식 환경의 성능에 미치는 영향을 줄일 수 있습니다. 자세한 [내용은 상태 모니터 성능을](/help/forms/using/admin-help/fine-tuning-health-monitor-performance.md#fine-tuning-health-monitor-performance)참조하십시오.

**상태 모니터 액세스**

1. 관리 콘솔에서 페이지의 오른쪽 위 모서리에 있는 상태 모니터를 클릭합니다.

