---
title: 워크플로우 인스턴스 관리
seo-title: Administering Workflow Instances
description: 워크플로우 인스턴스를 관리하는 방법을 알아봅니다.
seo-description: Lear how to administer Workflow Instances.
uuid: 81e53ef5-fe62-4ed4-b2d4-132aa986d5aa
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: d9c96e7f-9416-48e1-a6af-47384f7bee92
exl-id: 90923d39-3ac5-4028-976c-d011f0404476
source-git-commit: 8b4459c69b73159ce5afd819dfb772df5c51cd16
workflow-type: tm+mt
source-wordcount: '1136'
ht-degree: 1%

---

# 워크플로우 인스턴스 관리{#administering-workflow-instances}

워크플로우 콘솔은 워크플로우 인스턴스가 예상대로 실행되는지 확인하기 위해 워크플로우 인스턴스를 관리하는 몇 가지 도구를 제공합니다.

>[!NOTE]
>
>다음 [JMX 콘솔](/help/sites-administering/jmx-console.md#workflow-maintenance) 추가 워크플로우 유지 관리 작업을 제공합니다.

워크플로우를 관리하는 데 다양한 콘솔을 사용할 수 있습니다. 를 사용하십시오 [전역 탐색](/help/sites-authoring/basic-handling.md#global-navigation) 열다 **도구** 창을 선택한 다음 **워크플로우**:

* **모델**: 워크플로우 정의 관리
* **인스턴스**: 실행 중인 워크플로우 인스턴스 보기 및 관리
* **런처**: 워크플로우를 시작하는 방법 관리
* **아카이브**: 성공적으로 완료된 워크플로우의 기록 보기
* **실패**: 오류와 함께 완료된 워크플로우의 내역 보기
* **자동 지정**: 템플릿에 워크플로우 자동 할당 구성

## 워크플로우 인스턴스 상태 모니터링 {#monitoring-the-status-of-workflow-instances}

1. 탐색 사용 선택 **도구**, 그런 다음 **워크플로우**.
1. 선택 **인스턴스** 을 클릭하여 현재 진행 중인 워크플로우 인스턴스 목록을 표시합니다.

   ![wf-96](assets/wf-96.png)


## 검색 워크플로우 인스턴스 {#search-workflow-instances}

1. 탐색 사용 선택 **도구**, 그런 다음 **워크플로우**.
1. 선택 **인스턴스** 을 클릭하여 현재 진행 중인 워크플로우 인스턴스 목록을 표시합니다. 상단 레일의 왼쪽 모서리에서 을(를) 선택합니다 **필터**. 또는 키 입력을 alt+1로 사용할 수 있습니다. 다음 대화 상자가 표시됩니다.

   ![wf-99-1](assets/wf-99-1.png)

1. 필터 대화 상자에서 워크플로우 검색 기준을 선택합니다. 다음 입력을 기준으로 검색할 수 있습니다.

   * 페이로드 경로: 특정 경로 선택
   * 워크플로우 모델: 워크플로우 모델 선택
   * 할당자: 워크플로 할당자 선택
   * 유형: 작업, 워크플로우 항목 또는 워크플로우 실패
   * 작업 상태: 활성, 완료 또는 종료됨
   * 내 위치: 소유자 및 할당자, 소유자만, 할당자만
   * 시작 날짜: 지정된 날짜 이전 또는 이후의 시작 날짜
   * 종료 날짜: 지정한 날짜 이전 또는 이후의 종료 날짜
   * 기한: 지정한 날짜 이전 또는 이후의 기한
   * 업데이트 날짜: 지정된 날짜 이전 또는 이후의 업데이트 날짜

## 워크플로우 인스턴스 일시 중단, 다시 시작 및 종료 {#suspending-resuming-and-terminating-a-workflow-instance}

1. 탐색 사용 선택 **도구**, 그런 다음 **워크플로우**.
1. 선택 **인스턴스** 을 클릭하여 현재 진행 중인 워크플로우 인스턴스 목록을 표시합니다.

   ![wf-96-1](assets/wf-96-1.png)

1. 특정 항목을 선택한 다음 **종료**, **일시 중단**, 또는 **다시 시작**, 적절합니다. 확인 및/또는 자세한 내용은 다음과 같습니다.

   ![wf-97-1](assets/wf-97-1.png)

## 보관된 워크플로우 보기 {#viewing-archived-workflows}

1. 탐색 사용 선택 **도구**, 그런 다음 **워크플로우**.
1. 선택 **아카이브** 성공적으로 완료된 워크플로우 인스턴스 목록을 표시합니다.

   ![wf-98](assets/wf-98.png)

   >[!NOTE]
   >
   >abort 상태는 사용자 작업의 결과로 발생할 때 성공한 종료로 간주됩니다. 예:
   >
   >* 의 사용 **종료** 작업
   >* 워크플로우의 적용을 받는 페이지가 (강제) 삭제되면 워크플로우가 종료됩니다


1. 특정 항목을 선택한 다음 **기록 열기** 자세한 내용을 보려면 다음을 수행하십시오.

   ![wf-99](assets/wf-99.png)

## 워크플로우 인스턴스 오류 수정 {#fixing-workflow-instance-failures}

워크플로우가 실패하면 AEM에서는 **실패** 콘솔에서는 원래 원인을 처리한 후 적절한 작업을 조사하고 수행할 수 있습니다.

* **실패 세부 정보**
창을 열어 
**오류 메시지**, **단계** 및 **실패 스택**.

* **기록 열기**
워크플로우 내역의 세부 사항을 표시합니다.

* **단계 다시 시도** 스크립트 단계 구성 요소 인스턴스를 다시 실행합니다. 원래 오류 원인을 해결한 후 Retry Step 명령을 사용합니다. 예를 들어 프로세스 단계가 실행되는 스크립트에서 버그를 수정한 후 단계를 다시 시도하십시오.
* **종료** 오류로 인해 워크플로우가 인식할 수 없는 상황이 발생한 경우 워크플로우를 종료합니다. 예를 들어, 워크플로우는 워크플로우 인스턴스에 더 이상 유효하지 않은 저장소의 정보와 같은 환경 조건을 사용할 수 있습니다.
* **종료 및 다시 시도** 과 유사함 **종료** 원래 페이로드, 제목 및 설명을 사용하여 새 워크플로우 인스턴스가 시작된다는 점을 제외하고.

오류를 조사하려면 나중에 워크플로우를 다시 시작하거나 종료하려면 다음 단계를 사용합니다.

1. 탐색 사용 선택 **도구**, 그런 다음 **워크플로우**.
1. 선택 **실패** 완료되지 않은 워크플로우 인스턴스 목록을 표시합니다.
1. 특정 항목을 선택한 다음, 적절한 작업을 선택합니다.

   ![wf-47](assets/wf-47.png)

## 워크플로우 인스턴스 일반 삭제 {#regular-purging-of-workflow-instances}

워크플로우 인스턴스 수를 최소화하면 워크플로우 엔진의 성능이 높아지므로 리포지토리에서 완료되거나 실행되는 워크플로우 인스턴스를 정기적으로 제거할 수 있습니다.

구성 **Adobe Granite 워크플로우 제거 구성** 나이 및 상태에 따라 워크플로우 인스턴스를 삭제합니다. 모든 모델 또는 특정 모델의 워크플로우 인스턴스를 삭제할 수도 있습니다.

서비스의 여러 구성을 만들어 다양한 기준을 충족하는 워크플로우 인스턴스를 삭제할 수도 있습니다. 예를 들어, 예상 시간보다 오래 실행되는 특정 워크플로우 모델의 인스턴스를 삭제하는 구성을 만듭니다. 특정 일 이후에 완료된 모든 워크플로우를 지우는 다른 구성을 만들어 저장소 크기를 최소화합니다.

서비스를 구성하려면 [웹 콘솔](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) 또는 [저장소에 OSGi 구성 추가](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository). 다음 표에서는 두 방법 중 하나에 필요한 속성에 대해 설명합니다.

>[!NOTE]
>
>저장소에 구성을 추가하기 위해 서비스 PID는 다음과 같습니다.
>
>`com.adobe.granite.workflow.purge.Scheduler`
>
>서비스가 공장 서비스이므로 `sling:OsgiConfig` 노드에는 식별자 접미사가 필요합니다. 예를 들면 다음과 같습니다.
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
     <li>완료됨: 완료된 워크플로우 인스턴스가 삭제됩니다.</li>
     <li>실행 중: 실행 중인 워크플로우 인스턴스가 삭제됩니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>삭제할 모델</td>
   <td>scheduledpurge.modelIds</td>
   <td><p>제거할 워크플로우 모델의 ID입니다. ID는 모델 노드의 경로입니다(예:<br /> /conf/global/settings/workflow/models/dam/update_asset/jcr:content/model<br /> 모든 워크플로우 모델의 인스턴스를 삭제할 값을 지정하지 않습니다.</p> <p>여러 모델을 지정하려면 웹 콘솔에서 + 단추를 클릭합니다. </p> </td>
  </tr>
  <tr>
   <td>워크플로우 연령</td>
   <td>scheduledpurge.daysold</td>
   <td>제거할 워크플로우 인스턴스 기간(일 단위)입니다.</td>
  </tr>
 </tbody>
</table>

## 받은 편지함의 최대 크기 설정 {#setting-the-maximum-size-of-the-inbox}

를 구성하여 받은 편지함의 최대 크기를 설정할 수 있습니다 **Granite Workflow 서비스 Adobe**&#x200B;를 사용 [웹 콘솔](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) 또는 [저장소에 OSGi 구성 추가](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository). 다음 표에서는 두 방법 중 하나에 대해 구성하는 속성에 대해 설명합니다.

>[!NOTE]
>
>저장소에 구성을 추가하기 위해 서비스 PID는 다음과 같습니다.
>
>`com.adobe.granite.workflow.core.WorkflowSessionFactory`.

| 속성 이름(웹 콘솔) | OSGi 속성 이름 |
|---|---|
| 최대 받은 편지함 쿼리 크기 | granite.workflow.inboxQuerySize |

## 고객이 소유한 데이터 저장소에 대한 워크플로우 변수 사용 {#using-workflow-variables-customer-datastore}

워크플로우에 의해 처리된 데이터는 Adobe 제공 저장소(JCR)에 저장됩니다. 이 데이터는 본질적으로 민감할 수 있습니다. Adobe 제공 저장소 대신 사용자가 정의한 메타데이터/데이터를 모두 관리 저장소에 저장할 수 있습니다. 이러한 섹션에서는 외부 스토리지에 대해 이러한 변수를 설정하는 방법을 설명합니다.

### 메타데이터의 외부 저장소를 사용하도록 모델 설정 {#set-model-for-external-storage}

워크플로우 모델 수준에서 모델(및 런타임 인스턴스)에 메타데이터의 외부 저장소가 있음을 나타내는 플래그가 제공됩니다. 워크플로우 변수는 외부 스토리지로 표시된 모델의 워크플로우 인스턴스에 대해 JCR에 지속되지 않습니다.

속성 *userMetadataPersistenceEnabled* 은 *jcr:content node* 워크플로우 모델의 예입니다. 이 플래그는 워크플로우 메타데이터에서 *cq:userMetaDataCustomPersistenceEnabled*.

아래 그림은 워크플로우에 플래그를 설정해야 합니다.

![workflow-externalize-config](assets/workflow-externalize-config.png)

### 외부 저장소의 메타데이터에 대한 API {#apis-for-metadata-external-storage}

변수를 외부에 저장하려면 워크플로우가 노출하는 API를 구현해야 합니다.

UserMetaDataPersistenceContext

다음 샘플은 API를 사용하는 방법을 보여 줍니다.

```
@ProviderType
public interface UserMetaDataPersistenceContext {
 
    /**
     * Gets the workflow for persistence
     * @return workflow
     */
    Workflow getWorkflow();
 
    /**
     * Gets the workflow id for persistence
     * @return workflowId
     */
    String getWorkflowId();
 
    /**
     * Gets the user metadata persistence id
     * @return userDataId
     */
    String getUserDataId();
}
```

UserMetaDataPersistenceProvider

```
/**
 * This provider can be implemented to store the user defined workflow-data metadata in a custom storage location
 */
@ConsumerType
public interface UserMetaDataPersistenceProvider {
 
   /**
    * Retrieves the metadata using a unique identifier
    * @param userMetaDataPersistenceContext
    * @param metaDataMap of user defined workflow data metaData
    * @throws WorkflowException
    */
   void get(UserMetaDataPersistenceContext userMetaDataPersistenceContext, MetaDataMap metaDataMap) throws WorkflowException;
 
   /**
    * Stores the given metadata to the custom storage location
    * @param userMetaDataPersistenceContext
    * @param metaDataMap metadata map
    * @return the unique identifier that can be used to retrieve metadata. If null is returned, then workflowId is used.
    * @throws WorkflowException
    */
   String put(UserMetaDataPersistenceContext userMetaDataPersistenceContext, MetaDataMap metaDataMap) throws WorkflowException;
} 
```
