---
title: 프로세스 보고에서 사전 정의된 보고서
description: 장기 실행 프로세스, 프로세스 기간 및 워크플로우 볼륨에 대한 보고서를 만들기 위해 JEE의 AEM Forms 프로세스 데이터를 쿼리합니다.
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
exl-id: 34e55676-6332-4616-aecc-bcc8cc1e8a29
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 0%

---

# 프로세스 보고에서 사전 정의된 보고서 {#pre-defined-reports-in-process-reporting}

## 프로세스 보고에서 사전 정의된 보고서 {#pre-defined-reports-in-process-reporting-1}

AEM Forms Process Reporting은 다음과 함께 제공됩니다 *즉시 사용 가능해* 보고서:

* **[장기 실행 프로세스](#long-running-processes)**: 완료되는 데 지정된 시간 이상 걸린 모든 AEM Forms 프로세스에 대한 보고서
* **[프로세스 기간 차트](#process-duration-report)**: 기간별로 지정된 AEM Forms 프로세스에 대한 보고서
* **[워크플로 볼륨](#workflow-volume-report)**: 지정된 프로세스의 실행 중인 인스턴스 및 완료된 인스턴스의 날짜별 보고서

## 장기 실행 프로세스 {#long-running-processes}

장기 실행 프로세스 보고서는 완료되는 데 지정된 시간 이상 걸린 AEM Forms 프로세스를 표시합니다.

### 장기 실행 프로세스 보고서를 실행하려면 {#to-execute-a-long-running-process-report}

1. 프로세스 보고에서 사전 정의된 보고서 목록을 보려면 **프로세스 보고** 트리 보기에서 **보고서** 노드.
1. 다음을 클릭합니다. **장기 실행 프로세스** 보고서 노드입니다.

   ![long_running_node](assets/long_running_node.png)

   보고서를 선택하면 **보고서 매개 변수** [트리 보기] 오른쪽에 패널이 표시됩니다.

   ![장기 실행 프로세스 보고서 매개 변수 패널](assets/report_parameters_panel.png)

   매개 변수:

   * **기간** (*필수*): 기간 및 시간 단위를 지정합니다. 지정된 기간 이상 실행된 모든 AEM Forms 프로세스를 표시합니다.
   * **다음 이후 시작됨** (*선택 사항*): 날짜를 선택합니다. 보고서를 필터링하여 지정된 날짜 이후에 시작된 프로세스 인스턴스를 표시합니다.
   * **다음 시간 이전에 시작됨** (*선택 사항*): 날짜를 선택합니다. 보고서를 필터링하여 지정된 날짜 이전에 시작된 프로세스 인스턴스를 표시합니다.

1. 클릭 **이동** 보고서를 실행합니다.

   보고서는 **보고서** 의 오른쪽에 있는 패널 **프로세스 보고** 창.

   ![long_running_processes](assets/long_running_processes.png)

   의 오른쪽 위 모서리에 있는 옵션을 사용합니다. **보고서** 패널 을 사용하여 보고서에서 다음 작업을 수행할 수 있습니다.

   * **새로 고침**: 저장소에 있는 최신 데이터로 보고서를 새로 고칩니다.
   * **범례 색상 변경**: 보고서 범례 색상을 선택 및 변경합니다
   * **CSV로 내보내기**: 보고서에서 쉼표로 구분된 파일로 데이터 내보내기 및 다운로드

## 프로세스 기간 보고서  {#process-duration-report}

프로세스 기간 보고서는 Forms 프로세스의 인스턴스 수를 각 인스턴스가 실행된 일수별로 표시합니다.

### 프로세스 기간 보고서를 실행하려면 {#to-execute-a-process-duration-report}

1. 프로세스 보고에서 사전 정의된 보고서를 보려면 **프로세스 보고** 트리 보기에서 **보고서** 노드.
1. 다음을 클릭합니다. **프로세스 기간** 보고서 노드입니다.

   ![process_duration_node](assets/process_duration_node.png)

   보고서를 선택하면 **보고서 매개 변수** [트리 보기] 오른쪽에 패널이 표시됩니다.

   ![장기 실행 프로세스 보고서 매개 변수 패널](assets/process_duration_params.png)

   매개 변수:

   * **프로세스 선택** (*필수*): AEM Forms 프로세스를 선택합니다.

1. 클릭 **이동** 보고서를 실행합니다.

   보고서는 **보고서** [프로세스 보고] 창의 오른쪽에 있는 패널.

   ![process_duration_report](assets/process_duration_report.png)

   의 오른쪽 위 모서리에 있는 옵션을 사용합니다. **보고서** 패널 을 사용하여 보고서에서 다음 작업을 수행할 수 있습니다.

   * **새로 고침**: 저장소에 있는 최신 데이터로 보고서를 새로 고칩니다.
   * **범례 색상 변경**: 보고서 범례 색상을 선택 및 변경합니다
   * **CSV로 내보내기**: 보고서에서 쉼표로 구분된 파일로 데이터 내보내기 및 다운로드

## 워크플로우 볼륨 보고서 {#workflow-volume-report}

워크플로 볼륨 보고서는 현재 실행 중이며 완료된 AEM Forms 프로세스 인스턴스 수를 일별로 표시합니다.

### 워크플로우 볼륨 보고서를 실행하려면 {#to-execute-a-workflow-volume-report}

1. 프로세스 보고에서 사전 정의된 보고서를 보려면 **프로세스 보고** 트리 보기에서 **보고서** 노드.
1. 다음을 클릭합니다. **워크플로 볼륨** 보고서 노드입니다.

   ![workflow_volume_node](assets/workflow_volume_node.png)

   보고서를 선택하면 **보고서 매개 변수** [트리 보기] 오른쪽에 패널이 표시됩니다.

   ![장기 실행 프로세스 보고서 매개 변수 패널](assets/workflow_volume_params.png)

   매개 변수:

   * **프로세스 선택** (*필수*): AEM Forms 프로세스를 선택합니다.

   * **다음 이후 시작됨** (*선택 사항*): 날짜를 선택합니다. 보고서를 필터링하여 지정된 날짜 이후에 시작된 프로세스 인스턴스를 표시합니다.

   * **다음 시간 이전에 시작됨** (*선택 사항*): 날짜를 선택합니다. 보고서를 필터링하여 지정된 날짜 이전에 시작된 프로세스 인스턴스를 표시합니다.

1. 클릭 **이동** 보고서를 실행합니다.

   보고서는 **보고서** 의 오른쪽에 있는 패널 **프로세스 보고** 창.

   ![workflow_volume_report](assets/workflow_volume_report.png)

   의 오른쪽 위 모서리에 있는 옵션을 사용합니다. **보고서** 패널 을 사용하여 보고서에서 다음 작업을 수행할 수 있습니다.

   * **새로 고침**: 저장소에 있는 최신 데이터로 보고서를 새로 고칩니다.
   * **범례 색상 변경**: 보고서 범례 색상을 선택 및 변경합니다
   * **CSV로 내보내기**: 보고서에서 쉼표로 구분된 파일로 데이터 내보내기 및 다운로드
