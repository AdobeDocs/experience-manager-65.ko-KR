---
title: 에서 비동기 작업을 [!DNL Adobe Experience Manager]구성합니다.
description: 리소스를 많이 사용하는 작업을 비동기적으로 완료하여 성능을 최적화할 수 [!DNL Experience Manager Assets]있습니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 18b81ba3fcf15838ac9bebd451f4ad8b0b6e3bbb
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 1%

---


# 비동기 작업 {#asynchronous-operations}

성능에 대한 부정적인 영향을 줄이기 위해 장시간 실행되는 특정 리소스 중심 자산 작업을 비동기적으로 [!DNL Adobe Experience Manger Assets] 처리합니다. 비동기 처리에는 여러 작업을 대기열에 넣고 시스템 리소스의 가용성에 따라 여러 작업을 연속으로 실행하는 작업이 포함됩니다. 이러한 작업에는 다음이 포함됩니다.

* 많은 자산을 삭제하는 중입니다.
* 많은 참조가 있는 많은 자산 또는 자산 이동
* 에셋 메타데이터를 일괄적으로 내보내기 및 가져오기
* 설정된 임계값 제한을 초과하는 원격 [!DNL Experience Manager] 배포에서 자산을 가져오는 중입니다. 자산 수에는 제한이 있습니다.

비동기 작업 상태 **** 페이지에서 비동기 작업의 상태를 볼 수 있습니다.

>[!NOTE]
>
>기본적으로 [!DNL Assets] 작업은 동시에 실행됩니다. CPU 코어 수 `N` 의 경우 기본적으로 작업을 동시에 실행할 수 `N/2` 있습니다. 작업 큐에 대한 사용자 지정 설정을 사용하려면 **[!UICONTROL 웹 콘솔에서]** 비동기 작업 기본 큐 [!UICONTROL 구성을]수정하십시오. 자세한 내용은 [큐 구성을 참조하십시오](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#queue-configurations).

## 비동기 작업 상태 모니터링 {#monitoring-the-status-of-asynchronous-operations}

작업을 비동기적으로 [!DNL Assets] 처리할 때마다 받은 편지함 [!DNL Experience Manager] 및 이메일을 통해 알림을 [받습니다](/help/sites-authoring/inbox.md) . 비동기 작업의 상태를 자세히 보려면 **[!UICONTROL 비동기 작업 상태]** 페이지로 이동합니다.

1. 인터페이스에서 작업 [!DNL Experience Manager] > 작업 **[!UICONTROL 을]** 클릭합니다 ****.

1. [ **[!UICONTROL 비동기 작업 상태]** ] 페이지에서 작업 세부 사항을 검토하십시오.

   ![비동기 작업의 상태 및 세부 정보](assets/AsyncOperation-status.png)

   작업 진행 상태를 확인하려면 상태 **[!UICONTROL 열을]** 참조하십시오. 진행 상태에 따라 다음 상태 중 하나가 표시됩니다.

   * **[!UICONTROL 활성]**: 작업이 처리되는 중입니다.
   * **[!UICONTROL 성공]**: 작업이 완료되었습니다.
   * **[!UICONTROL 실패]** 또는 **[!UICONTROL 오류]**: 작업을 처리할 수 없습니다.
   * **[!UICONTROL 예약됨]**: 작업은 나중에 처리하도록 예약되어 있습니다.

1. 활성 작업을 중지하려면 목록에서 해당 작업을 선택하고 도구 모음에서 **[!UICONTROL 중지]** 아이콘 ![을](assets/do-not-localize/stop_icon.svg) 클릭합니다.

1. 설명 및 로그와 같은 추가 세부 사항을 보려면 작업을 선택하고 도구 모음에서 **[!UICONTROL 열기]** ![](assets/do-not-localize/edit_icon.svg) _아이콘을 클릭합니다. 작업 세부 사항 페이지가 표시됩니다.

   ![메타데이터 가져오기 작업 세부 사항](assets/job_details.png)

1. 목록에서 작업을 삭제하려면 도구 모음에서 **[!UICONTROL 삭제를]** 선택합니다. CSV 파일로 세부 사항을 다운로드하려면 **[!UICONTROL 다운로드를 클릭합니다]**.

   >[!NOTE]
   >
   >상태가 활성 또는 큐에 있는 경우 작업을 삭제할 수 없습니다.

## 완료된 작업 제거 {#purge-completed-tasks}

[!DNL Experience Manager Assets] 하루 100시간에 매일 제거 작업을 실행하여 하루 이상 오래된 완료된 비동기 작업을 삭제합니다.

<!-- TBD: Find out from the engineering team and mention the time zone of this 1:00 am task.
-->

삭제 작업에 대한 일정 및 완료된 작업의 세부 사항이 삭제되기 전에 보존되는 기간을 수정할 수 있습니다. 특정 시점에 세부 사항이 유지되도록 완료된 작업의 최대 수를 구성할 수도 있습니다.

1. 인터페이스에서 [!DNL Experience Manager] 도구 **[!UICONTROL > 작업]** > **[!UICONTROL 웹 콘솔]** 을 클릭합니다 ****.
1. Adobe **[!UICONTROL CQ DAM 비동기 작업 제거 예약]** 작업을 엽니다.
1. 완료된 작업을 삭제한 후 남은 기간(일)과 작업 내역에 세부 사항이 유지되는 최대 작업 수를 지정합니다. 변경 사항을 저장합니다.

   ![비동기 작업의 제거를 예약하기 위한 구성](assets/configmgr_purge_asyncjobs.png)

## 비동기 삭제 작업에 대한 임계값 구성 {#configure-thresholds-for-asynchronous-delete-operations}

삭제할 자산 또는 폴더의 수가 설정된 임계값 수를 초과하는 경우 삭제 작업이 비동기적으로 수행됩니다.

1. 인터페이스에서 [!DNL Experience Manager] 도구 **[!UICONTROL > 작업]** > **[!UICONTROL 웹 콘솔]** 을 클릭합니다 ****.
1. 웹 [!UICONTROL 콘솔에서]**[!UICONTROL 비동기 삭제 작업 처리]** 구성을 엽니다.
1. [자산 **[!UICONTROL 임계값]** ] 상자에서 자산, 폴더 또는 참조를 비동기적으로 삭제할 임계값 수를 지정합니다. 변경 사항을 저장합니다.

   ![에셋을 삭제하도록 작업의 한도 설정](assets/delete_threshold.png)

## 비동기 이동 작업의 임계값 구성 {#configure-thresholds-for-asynchronous-move-operations}

이동할 자산, 폴더 또는 참조 수가 설정된 임계값 수를 초과하는 경우 이동 작업이 비동기식으로 수행됩니다.

1. 인터페이스에서 [!DNL Experience Manager] 도구 **[!UICONTROL > 작업]** > **[!UICONTROL 웹 콘솔]** 을 클릭합니다 ****.
1. 웹 [!UICONTROL 콘솔에서]**[!UICONTROL 비동기 이동 작업 처리]** 구성을 엽니다.
1. 자산/참조 **[!UICONTROL 임계값]** 상자에서 자산, 폴더 또는 참조를 비동기적으로 이동할 임계값 수를 지정합니다. 변경 사항을 저장합니다.

   ![자산을 이동할 작업의 임계값 제한 설정](assets/move_threshold.png)

>[!MORELIKETHIS]
>
>* [Experience Manager에서 이메일을 구성합니다](/help/sites-administering/notification.md).
>* [에셋 메타데이터를 일괄](/help/assets/metadata-import-export.md)가져오거나 내보낼 수 있습니다.
>* [연결된 자산을 사용하여 원격 배포에서 DAM 자산을 공유할 수 있습니다](/help/assets/use-assets-across-connected-assets-instances.md).

