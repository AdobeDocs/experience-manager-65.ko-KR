---
title: OSGi의 Forms 중심 워크플로 | 사용자 데이터 처리
description: OSGi의 Forms 중심 워크플로 | 사용자 데이터 처리
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Admin,User
exl-id: fd0e17d7-c3e9-4dec-ad26-ed96a1881f42
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on OSGi
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 1%

---

# OSGi의 Forms 중심 워크플로 | 사용자 데이터 처리 {#forms-centric-workflows-on-osgi-handling-user-data}

Forms 중심 AEM 워크플로우를 통해 실제 Forms 중심 비즈니스 프로세스를 자동화할 수 있습니다. 워크플로우는 연결된 워크플로 모델에 지정된 순서로 실행되는 일련의 단계로 구성됩니다. 각 단계는 사용자에게 작업을 할당하거나 이메일 메시지를 보내는 등의 특정 작업을 수행합니다. 워크플로우는 저장소, 사용자 계정 및 서비스의 에셋과 상호 작용할 수 있습니다. 따라서 워크플로우는 Experience Manager의 모든 측면을 포함하는 복잡한 활동을 조정할 수 있습니다.

양식 중심 워크플로우는 다음 방법 중 하나를 통해 트리거하거나 시작할 수 있습니다.

* AEM 받은 편지함에서 애플리케이션 제출
* AEM [!DNL Forms] 앱에서 응용 프로그램을 제출하는 중
* 적응형 양식 제출
* 감시 폴더 사용
* 대화형 통신 또는 편지 제출

Forms 중심 AEM 워크플로 및 기능에 대한 자세한 내용은 [OSGi의 Forms 중심 워크플로](/help/forms/using/aem-forms-workflow.md)를 참조하십시오.

## 사용자 데이터 및 데이터 저장소 {#user-data-and-data-stores}

워크플로가 트리거되면 워크플로 인스턴스에 대해 페이로드가 자동으로 생성됩니다. 각 워크플로우 인스턴스에는 고유한 인스턴스 ID와 관련 페이로드 ID가 지정됩니다. 페이로드에는 워크플로 인스턴스와 연결된 사용자 및 양식 데이터의 저장소 위치가 포함됩니다. 또한 워크플로 인스턴스에 대한 초안 및 이전 데이터도 AEM 저장소에 저장됩니다.

페이로드, 초안 및 워크플로 인스턴스 내역이 있는 기본 저장소 위치는 다음과 같습니다.

>[!NOTE]
>
>워크플로우나 응용 프로그램을 만들 때 페이로드, 초안 및 내역 데이터를 저장하도록 여러 위치를 구성할 수 있습니다. 워크플로우나 응용 프로그램에서 데이터를 저장한 위치를 식별하려면 워크플로우를 검토합니다.

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
   <td><strong>이력</strong></td>
   <td>/var/fd/dashboard/instances/[server_id]/<br /> [date]/[workflow_instance]/history/</td>
   <td>/etc/fd/dashboard/instances/[server_id]/<br /> [date]/[workflow_instance]/history/</td>
  </tr>
 </tbody>
</table>

## 사용자 데이터 액세스 및 삭제 {#access-and-delete-user-data}

저장소의 워크플로 인스턴스에서 사용자 데이터에 액세스하고 삭제할 수 있습니다. 이를 위해서는 사용자와 연결된 워크플로 인스턴스의 인스턴스 ID를 알고 있어야 합니다. 워크플로 인스턴스를 시작했거나 워크플로 인스턴스의 현재 할당자인 사용자의 사용자 이름을 사용하여 워크플로 인스턴스의 인스턴스 ID를 찾을 수 있습니다.

하지만 다음 시나리오에서 초기자와 연결된 워크플로우를 식별할 수 없거나 결과가 모호할 수 있습니다.

* **감시 폴더를 통해 워크플로우가 트리거됨**: 감시 폴더에서 워크플로우를 트리거하는 경우 해당 초기자를 사용하여 워크플로우 인스턴스를 식별할 수 없습니다. 이 때, 사용자 정보는 저장된 데이터에 부호화된다.
* **게시 AEM 인스턴스에서 시작된 워크플로**: 적응형 양식, 대화형 통신 또는 편지를 AEM 게시 인스턴스에서 제출하면 모든 워크플로 인스턴스가 서비스 사용자를 사용하여 만들어집니다. 이러한 경우 로그인한 사용자의 사용자 이름은 워크플로우 인스턴스 데이터에 캡처되지 않습니다.

### 사용자 데이터 액세스 {#access}

워크플로 인스턴스에 대해 저장된 사용자 데이터를 식별하고 액세스하려면 다음 단계를 수행하십시오.

1. AEM 작성자 인스턴스에서 `https://'[server]:[port]'/crx/de`(으)로 이동하여 **[!UICONTROL 도구 > 쿼리]**(으)로 이동합니다.

   **[!UICONTROL Type]** 드롭다운에서 **[!UICONTROL SQL2]**&#x200B;을(를) 선택합니다.

1. 사용 가능한 정보에 따라 다음 쿼리 중 하나를 실행합니다.

   * 워크플로우 개시자를 알고 있는 경우 다음을 실행합니다.

   `SELECT &ast; FROM [cq:Workflow] AS s WHERE ISDESCENDANTNODE([path-to-workflow-instances]) and s.[initiator]='*initiator-ID*'`

   * 데이터를 찾는 사용자가 현재 워크플로우 피할당자인 경우 다음을 실행합니다.

   `SELECT &ast; FROM [cq:WorkItem] AS s WHERE ISDESCENDANTNODE([path-to-workflow-instances]) and s.[assignee]='*assignee-id*'`

   쿼리는 지정된 워크플로 개시자 또는 현재 워크플로 할당자에 대한 모든 워크플로 인스턴스의 위치를 반환합니다.

   예를 들어 다음 쿼리는 워크플로 개시자가 `srose`인 `/var/workflow/instances` 노드에서 두 개의 워크플로 인스턴스 경로를 반환합니다.

   ![워크플로 인스턴스](assets/workflow-instance.png)

1. 쿼리에서 반환된 워크플로우 인스턴스 경로로 이동합니다. status 속성은 워크플로 인스턴스의 현재 상태를 표시합니다.

   ![상태](assets/status.png)

1. 워크플로 인스턴스 노드에서 `data/payload/`(으)로 이동합니다. `path` 속성은 워크플로 인스턴스의 페이로드에 대한 경로를 저장합니다. 경로로 이동하여 페이로드에 저장된 데이터에 액세스할 수 있습니다.

   ![페이로드 경로](assets/payload-path.png)

1. 워크플로 인스턴스의 내역 및 초안의 위치로 이동합니다.

   예:

   `/var/fd/dashboard/instances/server0/2018-04-09/_var_workflow_instances_server0_2018-04-09_basicmodel_54/draft/`

   `/var/fd/dashboard/instances/server0/2018-04-09/_var_workflow_instances_server0_2018-04-09_basicmodel_54/history/`

1. 2단계에서 쿼리가 반환한 모든 워크플로 인스턴스에 대해 3~5단계를 반복합니다.

   >[!NOTE]
   >
   >AEM [!DNL Forms] 앱은 오프라인 모드로도 데이터를 저장합니다. 워크플로 인스턴스의 데이터는 개별 장치에 로컬로 저장되고 앱이 서버와 동기화될 때 [!DNL Forms] 서버에 제출될 수 있습니다.

### 사용자 데이터 삭제 {#delete-user-data}

다음 단계를 수행하여 워크플로우 인스턴스에서 사용자 데이터를 삭제하려면 AEM 관리자여야 합니다.

1. [사용자 데이터 액세스](/help/forms/using/forms-workflow-osgi-handling-user-data.md#access)의 지침을 따르고 다음 사항에 유의하십시오.

   * 사용자와 연결된 워크플로 인스턴스의 경로
   * 워크플로 인스턴스 상태
   * 워크플로 인스턴스의 페이로드 경로
   * 워크플로 인스턴스의 초안 및 내역 경로

1. **실행 중**, **일시 중단** 또는 **부실** 상태의 워크플로 인스턴스에 대해 이 단계를 수행합니다.

   1. `https://'[server]:[port]'/aem/start.html`(으)로 이동하여 관리자 자격 증명으로 로그인합니다.
   1. **[!UICONTROL 도구 > 워크플로 > 인스턴스]**(으)로 이동합니다.
   1. 사용자의 관련 워크플로 인스턴스를 선택하고 **[!UICONTROL 종료]**&#x200B;를 선택하여 실행 중인 인스턴스를 종료합니다.

      워크플로 인스턴스 작업에 대한 자세한 내용은 [워크플로 인스턴스 관리](/help/sites-administering/workflows-administering.md)를 참조하십시오.

1. [!DNL CRXDE Lite] 콘솔로 이동하고 워크플로 인스턴스의 페이로드 경로로 이동한 다음 `payload` 노드를 삭제합니다.
1. 워크플로 인스턴스의 초안 경로로 이동한 다음 `draft` 노드를 삭제합니다.
1. 워크플로 인스턴스의 내역 경로로 이동한 다음 `history` 노드를 삭제합니다.
1. 워크플로 인스턴스의 워크플로 인스턴스 경로로 이동하고 워크플로의 `[workflow-instance-ID]` 노드를 삭제합니다.

   >[!NOTE]
   >
   >워크플로 인스턴스 노드를 삭제하면 모든 워크플로 참가자에 대한 워크플로 인스턴스가 제거됩니다.

1. 사용자에 대해 식별된 모든 워크플로 인스턴스에 대해 2~6단계를 반복합니다.
1. 서버에 제출하지 않도록 워크플로우 참가자의 AEM [!DNL Forms] 앱 보낼 편지함에서 오프라인 초안 및 제출 데이터를 식별하고 삭제합니다.

API를 사용하여 노드 및 속성에 액세스하고 제거할 수도 있습니다. 자세한 내용은 다음 문서를 참조하십시오.

* [프로그래밍 방식으로 AEM JCR에 액세스하는 방법](/help/sites-developing/access-jcr.md)
* [노드 및 속성 제거](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/10_Writing.html#10.9%20Removing%20Nodes%20and%20Properties)
* [API 참조](https://helpx.adobe.com/experience-manager/6-3/sites-developing/reference-materials/javadoc/overview-summary.html)
