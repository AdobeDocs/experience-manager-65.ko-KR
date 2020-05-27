---
title: 비동기 작업
description: Adobe Experience Manager Assets는 리소스를 많이 사용하는 일부 작업을 비동기식으로 완료하여 성능을 최적화합니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 1%

---


# 비동기 작업 {#asynchronous-operations}

성능에 대한 부정적인 영향을 줄이기 위해 Adobe Experience Manager Assets는 장시간 실행되는 특정 리소스 집약적인 에셋 작업을 비동기적으로 처리합니다.

이러한 작업에는 다음이 포함됩니다.

* 많은 자산 삭제
* 많은 참조가 있는 많은 자산 또는 자산 이동
* 자산 메타데이터를 일괄 내보내기/가져옵니다.
* Remote Experience Manager 배포에서 임계값 설정 이상인 자산을 가져오는 중입니다.

비동기 처리에는 여러 작업을 대기열에 넣고 시스템 리소스의 가용성에 따라 이러한 작업을 순차적으로 실행합니다.

비동기 작업 상태 **** 페이지에서 비동기 작업의 상태를 볼 수 있습니다.

>[!NOTE]
>
>기본적으로 자산의 작업은 동시에 실행됩니다. N이 CPU 코어 개수인 경우 기본적으로 N/2 작업은 동시에 실행할 수 있습니다. 작업 큐에 대한 사용자 지정 설정을 사용하려면 웹 콘솔에서 **[!UICONTROL 비동기 작업 기본 큐]** 구성을 수정하십시오. 자세한 내용은 [큐 구성을 참조하십시오](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#queue-configurations).

## 비동기 작업 상태 모니터링 {#monitoring-the-status-of-asynchronous-operations}

자산이 비동기적으로 작업을 처리할 때마다 받은 편지함과 이메일을 통해 알림을 받게 됩니다.

비동기 작업의 상태를 자세히 보려면 **[!UICONTROL 비동기 작업 상태]** 페이지로 이동합니다.

1. Experience Manager 인터페이스에서 작업 **** > **[!UICONTROL 작업을 클릭합니다]**.

1. [ **[!UICONTROL 비동기 작업 상태]** ] 페이지에서 작업 세부 사항을 검토하십시오.

   ![비동기 작업의 상태 및 세부 정보](assets/AsyncOperation-status.png)

   특정 작업의 진행 상태를 확인하려면 상태 **[!UICONTROL 열의 값을]** 참조하십시오. 진행 상태에 따라 다음 상태 중 하나가 표시됩니다.

   * **[!UICONTROL 활성]**: 작업을 처리 중입니다.

   * **[!UICONTROL 성공]**: 작업이 완료되었습니다.

   * **[!UICONTROL 실패]** 또는 **[!UICONTROL 오류]**: 작업을 처리할 수 없습니다.

   * **[!UICONTROL 예약됨]**: 작업이 나중에 처리하도록 예약되었습니다.

1. 활성 작업을 중지하려면 목록에서 해당 작업을 선택하고 도구 모음에서 **[!UICONTROL 중지]** 를 클릭합니다.

   ![stop_icon](assets/stop_icon.png)

1. 설명 및 로그 등 추가 세부 사항을 보려면 작업을 선택하고 도구 모음에서 **[!UICONTROL 열기]** 를 클릭합니다.

   ![open_icon](assets/open_icon.png)

   작업 세부 사항 페이지가 표시됩니다.

   ![job_details](assets/job_details.png)

1. 목록에서 작업을 삭제하려면 도구 모음에서 **[!UICONTROL 삭제를]** 선택합니다. CSV 파일로 세부 사항을 다운로드하려면 **[!UICONTROL 다운로드를 클릭합니다]**.

   >[!NOTE]
   >
   >상태가 활성 또는 큐에 있는 경우 작업을 삭제할 수 없습니다.

## 완료된 작업 제거 {#purging-completed-jobs}

Adobe Experience Manager Assets는 매일 오전 1시에 제거 작업을 실행하여 하루 이상 오래된 완료된 비동기 작업을 삭제합니다.

삭제 작업에 대한 일정 및 완료된 작업의 세부 사항이 삭제되기 전에 보존되는 기간을 수정할 수 있습니다. 특정 시점에 세부 사항이 유지되도록 완료된 작업의 최대 수를 구성할 수도 있습니다.

1. Adobe Experience Manager 인터페이스에서 **[!UICONTROL 도구]** > 작업 **[!UICONTROL >]** 웹 콘솔 **[!UICONTROL 을 클릭합니다]**.
1. Adobe **[!UICONTROL CQ DAM 비동기 작업 제거 예약된]** 작업을 엽니다.
1. 완료된 작업을 삭제한 후 남은 한계일 수와 내역에 남아 있는 최대 작업 수를 지정합니다.

   ![비동기 작업 제거를 예약하기 위한 구성](assets/configmgr_purge_asyncjobs.png)

1. 변경 사항을 저장합니다.

## 비동기 처리를 위한 임계값 구성 {#configuring-thresholds-for-asynchronous-processing}

특정 작업을 비동기적으로 처리하도록 자산에 대한 자산 또는 참조의 임계값 수를 구성할 수 있습니다.

### 비동기 삭제 작업에 대한 임계값 구성 {#configuring-thresholds-for-asynchronous-delete-operations}

삭제할 자산 또는 폴더의 수가 임계값 수를 초과할 경우 삭제 작업이 비동기적으로 수행됩니다.

1. Adobe Experience Manager 인터페이스에서 **[!UICONTROL 도구]** > 작업 **[!UICONTROL >]** 웹 콘솔 **[!UICONTROL 을 클릭합니다]**.
1. 웹 콘솔에서 **[!UICONTROL 비동기 삭제 작업 처리]** 구성을 엽니다.
1. 자산 **[!UICONTROL 임계값]** 상자에서 삭제 작업의 비동기 처리를 위한 자산/폴더의 임계값 수를 지정합니다.

   ![delete_threshold](assets/delete_threshold.png)

1. 변경 사항을 저장합니다.

### 비동기 이동 작업에 대한 임계값 구성 {#configuring-thresholds-for-asynchronous-move-operations}

이동할 자산/폴더 또는 참조 수가 임계값을 초과할 경우 이동 작업이 비동기식으로 수행됩니다.

1. Adobe Experience Manager 인터페이스에서 **[!UICONTROL 도구]** > 작업 **[!UICONTROL >]** 웹 콘솔 **[!UICONTROL 을 클릭합니다]**.
1. 웹 콘솔에서 **[!UICONTROL 비동기 이동 작업 처리]** 구성을 엽니다.
1. 자산/참조 **[!UICONTROL 임계값]** 상자에서 이동 작업의 비동기 처리를 위한 자산/폴더 또는 참조의 임계값을 지정합니다.

   ![move_threshold](assets/move_threshold.png)

1. 변경 사항을 저장합니다.
