---
title: 워크플로우 인스턴스 관리
seo-title: 워크플로우 인스턴스 관리
description: 워크플로우 인스턴스를 관리하는 방법을 알아봅니다.
seo-description: 워크플로우 인스턴스를 관리하는 방법을 알아봅니다.
uuid: 81e53ef5-fe62-4ed4-b2d4-132aa986d5aa
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: d9c96e7f-9416-48e1-a6af-47384f7bee92
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 워크플로우 인스턴스 관리{#administering-workflow-instances}

워크플로우 콘솔은 워크플로우 인스턴스가 예상대로 실행되는지 확인하기 위해 워크플로우 인스턴스를 관리하기 위한 여러 도구를 제공합니다.

>[!NOTE]
>
>JMX [콘솔에서는](/help/sites-administering/jmx-console.md#workflow-maintenance) 추가 워크플로우 유지 관리 작업을 제공합니다.

워크플로우 관리에 다양한 콘솔을 사용할 수 있습니다. 전역 탐색 [기능을 사용하여 도구](/help/sites-authoring/basic-handling.md#global-navigation) 창을 연 다음 **** 작업 과정을 **선택합니다**.

* **모델**:워크플로우 정의 관리
* **인스턴스**:실행 중인 워크플로우 인스턴스 보기 및 관리
* **방사기**:워크플로우 실행 방법 관리
* **보관**:성공적으로 완료된 워크플로우 내역 보기
* **실패**:오류와 함께 완료된 워크플로우 내역 보기

## 워크플로우 인스턴스 상태 모니터링 {#monitoring-the-status-of-workflow-instances}

1. 탐색 기능을 사용하여 **도구를**&#x200B;선택한 다음 워크플로우를 **선택합니다**.
1. 인스턴스를 **선택하여** 현재 진행 중인 워크플로우 인스턴스 목록을 표시합니다.

   ![wf-96](assets/wf-96.png)

1. 특정 항목을 선택한 다음 **내역** 열기를 선택하여 자세한 내용을 봅니다.

   ![wf-97](assets/wf-97.png)

## 워크플로우 인스턴스 일시 중단, 재개 및 종료 {#suspending-resuming-and-terminating-a-workflow-instance}

1. 탐색 기능을 사용하여 **도구를**&#x200B;선택한 다음 워크플로우를 **선택합니다**.
1. 인스턴스를 **선택하여** 현재 진행 중인 워크플로우 인스턴스 목록을 표시합니다.

   ![wf-96-1](assets/wf-96-1.png)

1. 특정 항목을 선택한 다음 **종료**, 일시 **중단**&#x200B;또는 **다시 시작을**&#x200B;적절히사용합니다.확인 및/또는 추가 세부 정보가 필요합니다.

   ![wf-97-1](assets/wf-97-1.png)

## 보관된 워크플로우 보기 {#viewing-archived-workflows}

1. 탐색 기능을 사용하여 **도구를**&#x200B;선택한 다음 워크플로우를 **선택합니다**.
1. 보관을 **선택하여** 성공적으로 완료된 워크플로우 인스턴스 목록을 표시합니다.

   ![wf-98](assets/wf-98.png)

   >[!NOTE]
   >
   >중단 상태는 사용자 작업의 결과로 발생할 때 성공적인 종료로 간주됩니다.예를 들면 다음과 같습니다.
   >
   >* 종료 **작업** 사용
   >* 워크플로우의 적용을 받는 페이지가 (강제) 삭제되면 워크플로우가 종료됩니다


1. 특정 항목을 선택한 다음 **내역** 열기를 선택하여 자세한 내용을 봅니다.

   ![wf-99](assets/wf-99.png)

## 워크플로우 인스턴스 오류 수정 {#fixing-workflow-instance-failures}

워크플로우가 실패하면 AEM에서는 원래 **원인을** 처리한 후 적절한 작업을 조사하고 수행할 수 있도록 실패 콘솔을 제공합니다.

* **실패**&#x200B;세부 사항Failure Message, **Step**&#x200B;및 Failure **Stack** 을 표시하는 창을 **엽니다**.

* **작업 내역**&#x200B;열기작업 과정 내역에 대한 세부 사항을 표시합니다.

* **단계** 다시 시도 스크립트 단계 구성 요소 인스턴스를 다시 실행합니다. 원래 오류 원인을 해결한 후 다시 시도 단계 명령을 사용합니다. 예를 들어 프로세스 단계가 실행되는 스크립트에서 버그를 수정한 후 단계를 다시 시도하십시오.
* **종료** 오류로 인해 워크플로우에 대해 인식할 수 없는 상황이 발생한 경우 워크플로우를 종료합니다. 예를 들어, 워크플로우는 워크플로우 인스턴스에 더 이상 유효하지 않은 메모리의 정보와 같은 환경 조건을 사용할 수 있습니다.
* **종료 및 재시도종료** 유사 **종료** (새로운 워크플로우 인스턴스가 원본 페이로드, 제목 및 설명을 사용하여 시작된다는 점을 제외하면)

오류를 조사한 다음 나중에 워크플로우를 다시 시작하거나 종료하려면 다음 단계를 따르십시오.

1. 탐색 기능을 사용하여 **도구를**&#x200B;선택한 다음 워크플로우를 **선택합니다**.
1. 실패를 **선택하여** 성공적으로 완료되지 않은 워크플로우 인스턴스 목록을 표시합니다.
1. 특정 항목을 선택한 다음 적절한 작업을 선택합니다.

   ![wf-47](assets/wf-47.png)

## 워크플로우 인스턴스의 정기적인 제거 {#regular-purging-of-workflow-instances}

워크플로우 인스턴스 수를 최소화하면 워크플로우 엔진의 성능이 향상되므로 저장소에서 완료되었거나 실행 중인 워크플로우 인스턴스를 정기적으로 제거할 수 있습니다.

Adobe **Granite Workflow** Purge Configuration을 구성하여 해당 연령 및 상태에 따라 워크플로우 인스턴스를 삭제합니다. 모든 모델 또는 특정 모델의 워크플로우 인스턴스를 제거할 수도 있습니다.

또한 여러 서비스 구성을 만들어 다른 기준을 충족하는 워크플로우 인스턴스를 제거할 수도 있습니다. 예를 들어, 특정 워크플로우 모델의 인스턴스가 예상 시간보다 오래 실행될 때 해당 인스턴스를 삭제하는 구성을 만듭니다. 특정 일 이후에 완료된 모든 워크플로우를 삭제하는 다른 구성을 만들어 저장소 크기를 최소화할 수 있습니다.

서비스를 구성하려면 웹 콘솔을 사용하거나 [OSGi](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) 구성을 [저장소에](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)추가할 수 있습니다. 다음 표에서는 두 메서드 중 하나에 필요한 속성에 대해 설명합니다.

>[!NOTE]
>
>저장소에 구성을 추가하기 위해 서비스 PID는 다음과 같습니다.
>
>`com.adobe.granite.workflow.purge.Scheduler`
>
>서비스가 공장 서비스이므로, `sling:OsgiConfig` 노드의 이름에는 식별자 접미어가 필요합니다. 예:
>
>`com.adobe.granite.workflow.purge.Scheduler-myidentifier`

<table>
 <tbody>
  <tr>
   <th>속성 이름(웹 콘솔)</th>
   <th>OSGi 속성 이름</th>
   <th>설명</th>
  </tr>
  <tr>
   <td>작업 이름</td>
   <td>scheduledpurge.name</td>
   <td>예약된 삭제를 설명하는 이름입니다.</td>
  </tr>
  <tr>
   <td>워크플로우 상태</td>
   <td>scheduledpurge.workflowStatus</td>
   <td><p>제거할 워크플로우 인스턴스의 상태입니다. 다음 값이 유효합니다.</p>
    <ul>
     <li>완료:완료된 워크플로우 인스턴스가 삭제됩니다.</li>
     <li>실행 중:실행 중인 워크플로우 인스턴스가 삭제됩니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>삭제할 모델</td>
   <td>scheduledpurge.modelIds</td>
   <td><p>제거할 워크플로우 모델의 ID입니다. <br /> ID는 모델 노드의 경로입니다(예:/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model<br /> 모든 워크플로우 모델의 인스턴스를 삭제할 값을 지정하지 않습니다.</p> <p>여러 모델을 지정하려면 웹 콘솔에서 + 단추를 클릭합니다. </p> </td>
  </tr>
  <tr>
   <td>워크플로우 연령</td>
   <td>scheduledpurge.daysale</td>
   <td>삭제할 워크플로우 인스턴스의 기간(일)입니다.</td>
  </tr>
 </tbody>
</table>

## 받은 편지함의 최대 크기 설정 {#setting-the-maximum-size-of-the-inbox}

웹 콘솔을 사용하여 Adobe Granite Workflow Service를 구성하거나 **저장소에** OSGi [구성을](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) [](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)추가하여 받은 편지함의 최대 크기를 설정할 수 있습니다. 다음 표에서는 두 방법 중 하나에 대해 구성하는 속성에 대해 설명합니다.

>[!NOTE]
>
>저장소에 구성을 추가하기 위해 서비스 PID는 다음과 같습니다.
>
>`com.adobe.granite.workflow.core.WorkflowSessionFactory`.

| 속성 이름(웹 콘솔) | OSGi 속성 이름 |
|---|---|
| 최대 받은 편지함 쿼리 크기 | granite.workflow.inboxQuerySize |

