---
title: 정지된 작업 및 분기 작업
seo-title: Working with stalled operations and branches
description: 정지된 작업 페이지 및 정지된 분기 페이지에 정지된 프로세스가 표시됩니다.
seo-description: The Stalled Operations page and the Stalled Branches page show the processes that have stalled.
uuid: 5f6202b0-79c2-4c3c-847a-236c0366e60b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8c2567f3-7220-436a-b9f2-2824a98c1ccc
exl-id: c96faae0-2b0f-4334-b61c-f13b2d1ec179
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 0%

---

# 정지된 작업 및 분기 작업 {#working-with-stalled-operations-and-branches}

정지된 작업 페이지 및 정지된 분기 페이지에 정지된 프로세스가 표시됩니다. 작업 실행 중 또는 후에 오류가 발생하거나 프로세스의 계획된 지연 작업으로 인해 프로세스가 중지될 수 있습니다.

* 예상치 못한 오류로 인해 작업이 중지될 수 있습니다. 그러나 프로세스의 Stall Branch 작업은 프로세스가 더 이상 실행되지 않도록 의도적으로 중단하므로 관리자가 개입해야 합니다.
* 분기는 규칙 평가 중에 작업 간에 지연될 수 있습니다.

프로세스가 중단되면 문제가 해결되고 작업 또는 분기가 다시 시작될 때까지 추가 작업이 실행되지 않습니다.

정지된 각 항목에 대해 다음 정보가 목록에 표시됩니다.

**작업 이름 또는 분기 이름:** 작업 또는 분기의 이름입니다.

**상태:** 정지된 항목에 대해 항상 중지됨

**오류:** 문제에 대한 간략한 설명.

**프로세스 ID:** 프로세스가 인스턴스화될 때 Forms Workflow가 지정하는 양의 정수(즉, 사용자 또는 자동화된 단계가 프로세스를 시작할 때)입니다. 이 식별자를 사용하여 해당 라이프 사이클을 통해 프로세스 인스턴스를 추적할 수 있습니다.

**프로세스 이름 - 버전:** Workbench에서 지정된 프로세스의 이름입니다.

**정지된 날짜:** 작업 또는 분기가 정지된 날짜 및 시간입니다.

정지된 작업 또는 정지된 분기 페이지에서 다음 작업을 수행할 수 있습니다.

* 오류를 선택하여 세부 정보를 확인합니다. 오류를 선택하면 오류 세부 정보 페이지가 나타납니다.
* 정지된 작업을 종료 또는 다시 시도하거나 정지된 분기를 다시 시도하십시오.

## 정지된 작업 또는 분기를 종료하거나 다시 시도합니다. {#terminating-or-retrying-stalled-operations-or-branches}

정지된 작업 페이지에서 표시된 프로세스 인스턴스를 종료할 수 있습니다.

프로세스 인스턴스를 종료하면 실행이 중지되고 추가 작업이 수행되지 않습니다. 일반적으로 오류로 인해 프로세스를 차단하거나 사용할 수 없고 고정 및 재시작할 수 없는 경우에만 프로세스를 종료합니다.

정지된 작업 페이지 또는 정지된 분기 페이지에서 작업 또는 분기를 다시 시도할 수 있습니다.

작업을 다시 시도하면 Forms 워크플로우가 작업을 다시 시작하라는 요청을 보냅니다. 프로세스가 지연되는 오류를 해결하고 다시 시도 요청이 성공하면 프로세스가 정지된 지점부터 다시 실행되고 상태가 RUNNING으로 변경됩니다. 작업을 다시 시작할 수 없으면 작업이 STIDED로 유지되므로 작업을 종료해야 할 수 있습니다.

### 정지된 작업을 종료합니다. {#terminate-a-stalled-operation}

1. 관리 콘솔에서 서비스 > 양식 워크플로우 > 정지된 작업 오류를 클릭합니다.
1. 정지된 작업 페이지에서 종료할 항목을 선택하고 종료를 누릅니다.

### 중단된 작업 또는 분기 다시 시도 {#retry-a-stalled-operation-or-branch}

1. 관리 콘솔에서 서비스 > 양식 워크플로우를 클릭한 다음 정지된 작업 오류 또는 정지된 분기 오류를 클릭합니다.
1. 정지된 작업 또는 정지된 분기 페이지에서 다시 시도할 항목을 선택하고 다시 시도를 클릭합니다.

## 정지된 작업 또는 분기에 대한 오류 세부 정보 보기 {#viewing-error-details-about-stalled-operations-or-branches}

[정지된 작업] 또는 [정지된 분기] 페이지의 정지된 항목 목록에서 오류를 선택하면 [오류 세부 정보] 페이지가 나타나고 문제를 해결하는 데 도움이 되는 오류에 대한 세부 정보가 표시됩니다.

페이지 하단 상자에 오류 정보가 있습니다.

[오류 세부 정보] 페이지에서 정지된 작업을 종료하거나 다시 시도하거나 정지된 분기를 다시 시도할 수도 있습니다.

## 에스컬레이션 사용자가 없는 경우 프로세스가 중지되지 않습니다 {#process-does-not-stall-when-escalation-user-does-not-exist}

AEM Forms User Service의 Assign Task 작업이 특정 시간 후에 다른 사용자에게 작업을 에스컬레이션하도록 구성되고 Assign Task 작업이 실행된 후 에스컬레이션 사용자가 삭제되고 Escalation이 발생하기 전에 오류가 발생합니다.

이러한 상황이 발생하면 프로세스 및 작업의 상태가 구성된 에스컬레이션 시간에 변경되지 않고 에스컬레이션 작업이 발생하지 않지만 프로세스가 지연되지 않습니다. 서버 로그에 다음 메시지가 나타납니다.

&quot;escalation에 지정된 주도자가 유효하지 않습니다. taskID: *number*, 지정된 큐: *number*.&quot;

Assign Task 작업이 실행되기 전에 Escalation 사용자가 삭제되면 프로세스가 중단되거나 InvalidPrincipal 예외 이벤트가 발생합니다.

이 문제를 방지하려면 사용자를 삭제할 때 해당 사용자에 속하는 작업을 검색하여 적절하게 처리합니다. (자세한 내용은 [작업](/help/forms/using/admin-help/tasks.md#working-with-tasks))
