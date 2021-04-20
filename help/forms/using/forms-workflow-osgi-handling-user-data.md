---
title: OSGi 기반의 Forms 워크플로우 | 사용자 데이터 처리
seo-title: OSGi 기반의 Forms 워크플로우 | 사용자 데이터 처리
description: OSGi 기반의 Forms 워크플로우 | 사용자 데이터 처리
uuid: 6eefbe84-6496-4bf8-b065-212aa50cd074
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9f400560-8152-4d07-a946-e514e9b9cedf
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 1%

---


# OSGi 기반의 Forms 워크플로우 | 사용자 데이터 처리 {#forms-centric-workflows-on-osgi-handling-user-data}

Forms 중심의 AEM 워크플로우를 통해 실제 Forms 중심의 비즈니스 프로세스를 자동화할 수 있습니다. 워크플로우는 연결된 워크플로우 모델에서 지정된 순서대로 실행되는 일련의 단계로 구성됩니다. 각 단계에서는 사용자에게 작업을 할당하거나 이메일 메시지를 보내는 등 특정 작업을 수행합니다. 워크플로우는 저장소의 자산, 사용자 계정 및 서비스와 상호 작용할 수 있습니다. 따라서 워크플로우는 Experience Manager의 모든 측면을 포함하는 복잡한 활동을 조정할 수 있습니다.

양식 중심의 워크플로우는 다음 방법 중 하나를 통해 트리거하거나 실행할 수 있습니다.

* AEM 받은 편지함에서 응용 프로그램 제출
* AEM [!DNL Forms] 앱에서 애플리케이션 제출
* 적응형 양식 제출
* 감시 폴더 사용
* 대화형 통신 또는 편지 제출

Forms 중심의 AEM 워크플로우 및 기능에 대한 자세한 내용은 OSGi](/help/forms/using/aem-forms-workflow.md)Forms 중심의 WORKFLOW를 참조하십시오.[

## 사용자 데이터 및 데이터는 {#user-data-and-data-stores} 저장

워크플로우가 트리거되면 워크플로우 인스턴스에 대해 페이로드가 자동으로 생성됩니다. 각 워크플로우 인스턴스에는 고유 인스턴스 ID 및 관련 페이로드 ID가 할당됩니다. 페이로드에는 워크플로우 인스턴스와 연관된 사용자 및 양식 데이터의 저장소 위치가 포함되어 있습니다. 또한 워크플로우 인스턴스에 대한 초안 및 내역 데이터도 AEM 저장소에 저장됩니다.

워크플로우 인스턴스의 페이로드, 초안 및 내역이 있는 기본 저장소 위치는 다음과 같습니다.

>[!NOTE]
>
>워크플로우 또는 애플리케이션을 만들 때 페이로드, 초안 및 내역 데이터를 저장하도록 다른 위치를 구성할 수 있습니다. 워크플로우 또는 애플리케이션에서 데이터를 저장한 위치를 식별하려면 워크플로우를 검토합니다.

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><b>AEM 6.4 [!DNL Forms]</b></td>
   <td><b>AEM 6.3 [!DNL Forms]</b></td>
  </tr>
  <tr>
   <td><strong>워크플로 <br /> 인스턴스</strong></td>
   <td>/var/workflow/instances/[server_id]/&lt;date&gt;/[workflow-instance]/</td>
   <td>/etc/workflow/instances/[server_id]/[date]/[workflow-instance]/</td>
  </tr>
  <tr>
   <td><strong>페이로드</strong></td>
   <td>/var/fd/dashboard/payload/[server_id]/[date]/<br /> [payload-id]/</td>
   <td>/etc/fd/dashboard/payload/[server_id]/[date]/<br /> [payload-id]/</td>
  </tr>
  <tr>
   <td><strong>초안</strong></td>
   <td>/var/fd/dashboard/instances/[server_id]/<br /> [date]/[workflow-instance]/draft/[workitem]/</td>
   <td>/etc/fd/dashboard/instances/[server_id]/<br /> [date]/[workflow-instance]/draft/[workitem]/</td>
  </tr>
  <tr>
   <td><strong>역사</strong></td>
   <td>/var/fd/dashboard/instances/[server_id]/<br /> [date]/[workflow_instance]/history/</td>
   <td>/etc/fd/dashboard/instances/[server_id]/<br /> [date]/[workflow_instance]/history/</td>
  </tr>
 </tbody>
</table>

## 사용자 데이터 {#access-and-delete-user-data} 액세스 및 삭제

저장소의 워크플로우 인스턴스에서 사용자 데이터에 액세스하고 삭제할 수 있습니다. 이를 수행하려면 사용자와 연결된 워크플로우 인스턴스의 인스턴스 ID를 알고 있어야 합니다. 워크플로우 인스턴스를 시작한 사용자 또는 워크플로우 인스턴스의 현재 할당자인 사용자의 사용자 이름을 사용하여 워크플로우 인스턴스의 인스턴스 ID를 찾을 수 있습니다.

그러나 다음 시나리오에서 이니시에이터와 연결된 워크플로우를 식별할 때 결과가 모호하거나 식별할 수는 없습니다.

* **감시 폴더를 통해 트리거된 워크플로우**:워크플로우가 감시 폴더에 의해 트리거되는 경우 해당 이니시에이터를 사용하여 워크플로우 인스턴스를 식별할 수 없습니다. 이 경우 사용자 정보는 저장된 데이터로 인코딩됩니다.
* **게시 AEM 인스턴스에서 시작된 워크플로**:모든 워크플로우 인스턴스는 AEM 게시 인스턴스에서 응용 양식, 대화형 통신 또는 문자를 제출할 때 서비스 사용자를 사용하여 만듭니다. 이 경우 로그인한 사용자의 사용자 이름이 워크플로 인스턴스 데이터에서 캡처되지 않습니다.

### 사용자 데이터 {#access} 액세스

워크플로우 인스턴스에 대해 저장된 사용자 데이터를 식별하고 액세스하려면 다음 단계를 수행하십시오.

1. AEM 작성자 인스턴스에서 `https://'[server]:[port]'/crx/de`으로 이동하여 **[!UICONTROL 도구 > 쿼리]**&#x200B;로 이동합니다.

   **[!UICONTROL 유형]** 드롭다운에서 **[!UICONTROL SQL2]**&#x200B;을 선택합니다.

1. 사용 가능한 정보에 따라 다음 쿼리 중 하나를 실행합니다.

   * 워크플로 개시자가 알려진 경우 다음을 실행합니다.

   `SELECT &ast; FROM [cq:Workflow] AS s WHERE ISDESCENDANTNODE([path-to-workflow-instances]) and s.[initiator]='*initiator-ID*'`

   * 검색 중인 데이터의 사용자가 현재 워크플로우 할당자인 경우 다음을 실행합니다.

   `SELECT &ast; FROM [cq:WorkItem] AS s WHERE ISDESCENDANTNODE([path-to-workflow-instances]) and s.[assignee]='*assignee-id*'`

   쿼리는 지정된 워크플로우 개시자 또는 현재 워크플로우 할당자에 대한 모든 워크플로우 인스턴스의 위치를 반환합니다.

   예를 들어 다음 쿼리는 워크플로 개시자가 `srose`인 `/var/workflow/instances` 노드에서 두 개의 워크플로 인스턴스 경로를 반환합니다.

   ![workflow-instance](assets/workflow-instance.png)

1. 쿼리에서 반환된 워크플로 인스턴스 경로로 이동합니다. status 속성은 워크플로 인스턴스의 현재 상태를 표시합니다.

   ![상태](assets/status.png)

1. 워크플로우 인스턴스 노드에서 `data/payload/`으로 이동합니다. `path` 속성은 워크플로 인스턴스의 페이로드 경로를 저장합니다. 페이로드에 저장된 데이터에 액세스할 수 있는 경로로 이동할 수 있습니다.

   ![payload-path](assets/payload-path.png)

1. 워크플로우 인스턴스에 대한 초안 및 작업 내역의 위치로 이동합니다.

   예:

   `/var/fd/dashboard/instances/server0/2018-04-09/_var_workflow_instances_server0_2018-04-09_basicmodel_54/draft/`

   `/var/fd/dashboard/instances/server0/2018-04-09/_var_workflow_instances_server0_2018-04-09_basicmodel_54/history/`

1. 2단계에서 쿼리에서 반환된 모든 워크플로우 인스턴스에 대해 3 - 5단계를 반복합니다.

   >[!NOTE]
   >
   >AEM [!DNL Forms] 앱도 오프라인 모드에서 데이터를 저장합니다. 워크플로 인스턴스의 데이터는 개별 장치에 로컬로 저장되고 앱이 서버와 동기화될 때 [!DNL Forms] 서버에 전송될 수 있습니다.

### 사용자 데이터 {#delete-user-data} 삭제

다음 단계를 수행하여 워크플로우 인스턴스에서 사용자 데이터를 삭제하려면 AEM 관리자여야 합니다.

1. [사용자 데이터 액세스](/help/forms/using/forms-workflow-osgi-handling-user-data.md#access)의 지침을 따르고 다음 사항을 메모하십시오.

   * 사용자와 연결된 워크플로우 인스턴스 경로
   * 워크플로우 인스턴스의 상태
   * 워크플로우 인스턴스에 대한 페이로드 경로
   * 워크플로우 인스턴스에 대한 초안 및 작업 내역 경로

1. **RUNNING**, **SUSPENDED** 또는 **STALE** 상태의 워크플로우 인스턴스에 대해 이 단계를 수행합니다.

   1. `https://'[server]:[port]'/aem/start.html`으로 이동하여 관리자 자격 증명으로 로그인합니다.
   1. **[!UICONTROL 도구 > 워크플로> 인스턴스]**&#x200B;로 이동합니다.
   1. 사용자에 대한 관련 워크플로우 인스턴스를 선택하고 **[!UICONTROL 종료]**&#x200B;를 눌러 실행 중인 인스턴스를 종료합니다.

      워크플로우 인스턴스 작업에 대한 자세한 내용은 [워크플로우 인스턴스 관리](/help/sites-administering/workflows-administering.md)를 참조하십시오.

1. [!DNL CRXDE Lite] 콘솔로 이동하여 워크플로우 인스턴스에 대한 페이로드 경로로 이동한 다음 `payload` 노드를 삭제합니다.
1. 워크플로우 인스턴스의 초안 경로로 이동하고 `draft` 노드를 삭제합니다.
1. 워크플로 인스턴스의 작업 내역 경로로 이동하고 `history` 노드를 삭제합니다.
1. 워크플로우 인스턴스의 워크플로우 인스턴스 경로로 이동하고 워크플로우에 대한 `[workflow-instance-ID]` 노드를 삭제합니다.

   >[!NOTE]
   >
   >워크플로우 인스턴스 노드를 삭제하면 모든 워크플로우 참가자에 대한 워크플로우 인스턴스가 제거됩니다.

1. 사용자에 대해 식별된 모든 워크플로우 인스턴스에 대해 2 - 6단계를 반복합니다.
1. 워크플로 참가자의 AEM [!DNL Forms] 앱 옵트박스에서 오프라인 초안 및 제출 데이터를 식별하고 삭제하여 서버에 제출되지 않습니다.

API를 사용하여 노드 및 속성에 액세스하고 제거할 수도 있습니다. 자세한 내용은 다음 문서를 참조하십시오.

* [프로그래밍 방식으로 AEM JCR에 액세스하는 방법](/help/sites-developing/access-jcr.md)
* [노드 및 속성 제거](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.9%20Removing%20Nodes%20and%20Properties)
* [API 참조](https://helpx.adobe.com/experience-manager/6-3/sites-developing/reference-materials/javadoc/overview-summary.html)

