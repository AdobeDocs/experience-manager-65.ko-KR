---
title: 프로세스 보고의 사전 정의된 보고서
seo-title: 프로세스 보고의 사전 정의된 보고서
description: JEE의 AEM Forms 프로세스 데이터를 쿼리하여 장기 실행 프로세스, 프로세스 기간 및 워크플로우 볼륨에 대한 보고서를 만듭니다.
seo-description: JEE의 AEM Forms 프로세스 데이터를 쿼리하여 장기 실행 프로세스, 프로세스 기간 및 워크플로우 볼륨에 대한 보고서를 만듭니다.
uuid: 704a8886-90ea-4793-a3fc-f998f878c928
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3d93375e-ec37-4445-96ea-d315676787b4
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 0%

---


# 프로세스 보고에서 사전 정의된 보고서 {#pre-defined-reports-in-process-reporting}

## 프로세스 보고 중인 사전 정의된 보고서 {#pre-defined-reports-in-process-reporting-1}

AEM Forms 프로세스 보고는 다음 *즉시 사용* 보고서와 함께 제공됩니다.

* **[긴 실행 프로세스](#long-running-processes)**:지정된 시간 이상 경과된 모든 AEM Forms 프로세스에 대한 보고서
* **[프로세스 기간 차트](#process-duration-report)**:기간별 지정된 AEM Forms 프로세스 보고서
* **[워크플로우 볼륨](#workflow-volume-report)**:날짜별 지정된 프로세스의 실행 및 완료 인스턴스에 대한 보고서

## 긴 실행 프로세스 {#long-running-processes}

장기 실행 프로세스 보고서는 완료하는 데 지정된 시간 이상 걸린 AEM Forms 프로세스를 표시합니다.

### 긴 실행 프로세스 보고서를 실행하려면 {#to-execute-a-long-running-process-report}

1. 프로세스 보고에서 사전 정의된 보고서 목록을 보려면 **프로세스 보고** 트리 보기에서 **보고서** 노드를 클릭합니다.
1. **긴 실행 프로세스** 보고서 노드를 클릭합니다.

   ![long_running_node](assets/long_running_node.png)

   보고서를 선택하면 **보고서 매개 변수** 패널이 트리 보기 오른쪽에 표시됩니다.

   ![장기 실행 프로세스 보고서 매개 변수 패널](assets/report_parameters_panel.png)

   매개 변수:

   * **기간** (*필수*):지속 시간 및 시간 단위를 지정합니다. 지정된 기간 이상 실행된 모든 AEM Forms 프로세스를 표시합니다.
   * **시작 후** (*선택 사항*):날짜를 선택합니다. 지정된 날짜 이후에 시작된 프로세스 인스턴스를 표시하도록 보고서를 필터링합니다.
   * **시작하기 전** (*선택 사항*):날짜를 선택합니다. 지정된 날짜 이전에 시작된 프로세스 인스턴스를 표시하도록 보고서를 필터링합니다.

1. **Go**&#x200B;을 클릭하여 보고서를 실행합니다.

   보고서는 **프로세스 보고** 창 오른쪽의 **보고서** 패널에 표시됩니다.

   ![long_running_processes](assets/long_running_processes.png)

   보고서에서 다음 작업을 수행하려면 **보고서** 패널의 오른쪽 위 모서리에 있는 옵션을 사용합니다.

   * **새로 고침**:최신 데이터가 저장소에 있는 보고서를 새로 고칩니다.
   * **범례 색상 변경**:보고서 범례 색상 선택 및 변경
   * **CSV로 내보내기**:보고서의 데이터를 쉼표로 구분된 파일로 내보내기 및 다운로드

## 프로세스 기간 보고서 {#process-duration-report}

프로세스 기간 보고서에는 각 인스턴스가 실행된 일수로 Forms 프로세스의 인스턴스 수가 표시됩니다.

### 프로세스 기간 보고서를 실행하려면 {#to-execute-a-process-duration-report}

1. 프로세스 보고에서 미리 정의된 보고서를 보려면 **프로세스 보고** 트리 보기에서 **보고서** 노드를 클릭합니다.
1. **프로세스 기간** 보고서 노드를 클릭합니다.

   ![process_duration_node](assets/process_duration_node.png)

   보고서를 선택하면 **보고서 매개 변수** 패널이 트리 보기 오른쪽에 표시됩니다.

   ![장기 실행 프로세스 보고서 매개 변수 패널](assets/process_duration_params.png)

   매개 변수:

   * **프로세스** (*필수*) 선택:AEM Forms 프로세스를 선택합니다.

1. **Go**&#x200B;을 클릭하여 보고서를 실행합니다.

   보고서는 프로세스 보고 창 오른쪽의 **보고서** 패널에 표시됩니다.

   ![process_duration_report](assets/process_duration_report.png)

   보고서에서 다음 작업을 수행하려면 **보고서** 패널의 오른쪽 위 모서리에 있는 옵션을 사용합니다.

   * **새로 고침**:최신 데이터가 저장소에 있는 보고서를 새로 고칩니다.
   * **범례 색상 변경**:보고서 범례 색상 선택 및 변경
   * **CSV로 내보내기**:보고서의 데이터를 쉼표로 구분된 파일로 내보내기 및 다운로드

## 워크플로 볼륨 보고서 {#workflow-volume-report}

워크플로우 볼륨 보고서는 일별 현재 실행 중인 AEM Forms 프로세스 및 완료된 인스턴스의 수를 표시합니다.

### 워크플로우 볼륨 보고서 {#to-execute-a-workflow-volume-report}를 실행하려면

1. 프로세스 보고에서 미리 정의된 보고서를 보려면 **프로세스 보고** 트리 보기에서 **보고서** 노드를 클릭합니다.
1. **워크플로우 볼륨** 보고서 노드를 클릭합니다.

   ![workflow_volume_node](assets/workflow_volume_node.png)

   보고서를 선택하면 **보고서 매개 변수** 패널이 트리 보기 오른쪽에 표시됩니다.

   ![장기 실행 프로세스 보고서 매개 변수 패널](assets/workflow_volume_params.png)

   매개 변수:

   * **프로세스** (*필수*) 선택:AEM Forms 프로세스를 선택합니다.

   * **시작 후** (*선택 사항*):날짜를 선택합니다. 지정된 날짜 이후에 시작된 프로세스 인스턴스를 표시하도록 보고서를 필터링합니다.

   * **시작하기 전** (*선택 사항*):날짜를 선택합니다. 지정된 날짜 이전에 시작된 프로세스 인스턴스를 표시하도록 보고서를 필터링합니다.

1. **Go**&#x200B;을 클릭하여 보고서를 실행합니다.

   보고서는 **프로세스 보고** 창 오른쪽의 **보고서** 패널에 표시됩니다.

   ![workflow_volume_report](assets/workflow_volume_report.png)

   보고서에서 다음 작업을 수행하려면 **보고서** 패널의 오른쪽 위 모서리에 있는 옵션을 사용합니다.

   * **새로 고침**:최신 데이터가 저장소에 있는 보고서를 새로 고칩니다.
   * **범례 색상 변경**:보고서 범례 색상 선택 및 변경
   * **CSV로 내보내기**:보고서의 데이터를 쉼표로 구분된 파일로 내보내기 및 다운로드
