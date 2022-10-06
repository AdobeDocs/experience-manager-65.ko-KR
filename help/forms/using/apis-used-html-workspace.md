---
title: AEM Forms 작업 공간에 사용되는 API
seo-title: APIs used in AEM Forms workspace
description: 사용자 지정 및 자동화를 위해 노출되는 AEM Forms 작업 영역의 공개 Java 및 JavaScript API 및 메서드.
seo-description: Public Java and JavaScript APIs and methods of LiveCycle AEM Forms workspace, exposed for customization and automation.
uuid: 9602990e-8ac7-42eb-b507-50b3594055ba
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 4a73a973-fccf-466b-b4a0-47652a14a080
exl-id: 9034f73a-83f3-498e-b6a6-ad6577aa1a3a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 1%

---

# AEM Forms 작업 공간에 사용되는 API {#apis-used-in-aem-forms-workspace}

다음 API는 AEM Forms 작업 영역에서 사용됩니다.

<table>
 <tbody>
  <tr>
   <td><strong>Javascript 메서드</strong></td>
   <td><strong>서비스 이름</strong></td>
   <td><strong>API 이름</strong></td>
   <td><strong>댓글</strong></td>
  </tr>
  <tr>
   <td>getGroups</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getGroups</td>
   <td>그룹을 검색합니다. 지정하지 않은 경우 모든 그룹의 목록을 반환하고 지정된 이름을 가진 그룹을 반환합니다.</td>
  </tr>
  <tr>
   <td>getUsersAndGroups</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsersAndGroups</td>
   <td>사용자 및 그룹을 검색합니다. 아무 것도 지정하지 않은 경우 모든 사용자 및 그룹 목록을 반환하고, 지정된 이름을 가진 사용자 및 그룹을 반환합니다.</td>
  </tr>
  <tr>
   <td>prepareForSubmit</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>prepareForSubmit</td>
   <td>이 호출은 DocumentSubmitServlet을 통해 양식을 제출하기 전에 호출됩니다. 실제 제출 중에 검색된 세션 변수(만료 시간 및 함께)에 작업 ID를 설정합니다.</td>
  </tr>
  <tr>
   <td>submitTask</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>제출</td>
   <td>작업과 연관된 문서 객체를 제출합니다(그리고 프로세스를 차례로 제출).</td>
  </tr>
  <tr>
   <td>getRootEndpointCategories</td>
   <td>ProcessManagementStartpointService</td>
   <td>getRootEndpointCategories</td>
   <td>서버에 있는 모든 루트 카테고리를 가져옵니다.</td>
  </tr>
  <tr>
   <td>getDirectChildCategories</td>
   <td>ProcessManagementStartpointService</td>
   <td>getDirectChildCategories2</td>
   <td>카테고리의 모든 직접 하위를 가져옵니다.</td>
  </tr>
  <tr>
   <td>getAllStartpoints</td>
   <td>ProcessManagementStartpointService</td>
   <td>getAllStartpoints</td>
   <td>모든 카테고리의 서버에 있는 모든 시작점을 가져옵니다.</td>
  </tr>
  <tr>
   <td>invokeStartpoint</td>
   <td>ProcessManagementStartpointService</td>
   <td>invokeStartpoint</td>
   <td>이렇게 하면 시작점이 호출되고 시작점에 해당하는 새 작업이 만들어집니다</td>
  </tr>
  <tr>
   <td>getAllTasks</td>
   <td>ProcessManagementTaskService</td>
   <td>getAllActionableTasks</td>
   <td>이 플러그인은 로그인된 사용자를 위해 작성 및 전달, 상담, 저장, 할당, 할당 및 저장된 모든 작업을 가져옵니다.</td>
  </tr>
  <tr>
   <td>getTask</td>
   <td>ProcessManagementTaskService</td>
   <td>getTask</td>
   <td>특정 작업을 가져옵니다.</td>
  </tr>
  <tr>
   <td>renderTask</td>
   <td>ProcessManagementTaskService</td>
   <td>렌더링</td>
   <td>이 메서드는 작업을 렌더링하고 양식 url, 양식 유형, 필요한 경우 데이터 url과 같은 양식을 렌더링하는 데 필요한 정보를 반환합니다.</td>
  </tr>
  <tr>
   <td>submitWithPriorData</td>
   <td>ProcessManagementTaskService</td>
   <td>submitWithPriorData</td>
   <td>결과 키를 사용하여 TaskManager의 제출 API 결과를 반환합니다.</td>
  </tr>
  <tr>
   <td>submitWithData</td>
   <td>ProcessManagementTaskService</td>
   <td>submitWithData</td>
   <td>TaskManager의 제출 API를 사용하여 작업과 연결된 양식 데이터(문자열로 전달됨)를 제출합니다. TaskManager의 제출 API를 호출하지 않는 Flex 양식에 사용됩니다.</td>
  </tr>
  <tr>
   <td>저장</td>
   <td>ProcessManagementTaskService</td>
   <td>저장</td>
   <td>서버에 작업을 저장합니다.</td>
  </tr>
  <tr>
   <td>complete</td>
   <td>ProcessManagementTaskService</td>
   <td>complete</td>
   <td>작업을 완료하고 프로세스 설계에 따라 다음 단계로 작업이 전달됩니다.</td>
  </tr>
  <tr>
   <td>getAttachment</td>
   <td>ProcessManagementTaskService</td>
   <td>getAttachment</td>
   <td>첨부 파일을 사용할 수 있는 첨부 파일의 URL을 반환합니다.</td>
  </tr>
  <tr>
   <td>getAllAttachments</td>
   <td>ProcessManagementTaskService</td>
   <td>getAllActionableAttachments</td>
   <td>작업에 대한 모든 첨부 파일과 메모를 가져옵니다.</td>
  </tr>
  <tr>
   <td>공유</td>
   <td>ProcessManagementTaskService</td>
   <td>공유</td>
   <td>다른 사용자와 작업을 공유합니다. 다른 사용자가 작업을 요청하고 작업 소유자가 될 수 있습니다.</td>
  </tr>
  <tr>
   <td>앞으로</td>
   <td>ProcessManagementTaskService</td>
   <td>앞으로</td>
   <td>작업을 다른 사용자에게 전달합니다.</td>
  </tr>
  <tr>
   <td>참조</td>
   <td>ProcessManagementTaskService</td>
   <td>참조</td>
   <td>다른 사용자와 작업을 협의합니다.</td>
  </tr>
  <tr>
   <td>청구</td>
   <td>ProcessManagementTaskService</td>
   <td>청구</td>
   <td>공유 큐에서 사용할 수 있는 작업이 요청됩니다.</td>
  </tr>
  <tr>
   <td>잠금 해제</td>
   <td>ProcessManagementTaskService</td>
   <td>잠금 해제</td>
   <td>작업이 잠금 해제됩니다.</td>
  </tr>
  <tr>
   <td>잠금</td>
   <td>ProcessManagementTaskService</td>
   <td>잠금</td>
   <td>공유된 경우 작업을 잠금으로 설정하여 다른 사용자가 작업을 요구할 수 없습니다.</td>
  </tr>
  <tr>
   <td>거부</td>
   <td>ProcessManagementTaskService</td>
   <td>거부</td>
   <td>작업의 이전 소유자에게 작업을 반환합니다.</td>
  </tr>
  <tr>
   <td>포기</td>
   <td>ProcessManagementTaskService</td>
   <td>포기</td>
   <td>작업이 삭제됩니다.</td>
  </tr>
  <tr>
   <td>setVisibility</td>
   <td>ProcessManagementTaskService</td>
   <td>setVisibility</td>
   <td>작업의 가시성을 설정합니다. 가시성을 false 로 설정하면 나중에 작업이 표시되지 않습니다.</td>
  </tr>
  <tr>
   <td>getUsers</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsers</td>
   <td>사용자 검색에 사용됩니다. 이름이 지정되지 않은 경우 모든 사용자가 반환되고, 지정된 이름의 사용자가 반환됩니다.</td>
  </tr>
  <tr>
   <td>getUsersInGroup</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsersInGroupByName</td>
   <td>그룹에 있는 모든 사용자를 반환합니다.</td>
  </tr>
  <tr>
   <td>grantQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>grantQueueAccess</td>
   <td>지정된 사용자에게 로그인한 사용자의 큐에 대한 액세스 권한을 부여합니다. 기본적으로 다른 사용자와 자체 큐를 공유합니다.</td>
  </tr>
  <tr>
   <td>requestQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>requestQueueAccess</td>
   <td>로그인한 사용자에 대해 지정된 사용자의 큐에 대한 액세스 요청을 수행합니다. 사용자가 요청을 승인하면 사용자의 큐는 로그인한 사용자와 공유됩니다.</td>
  </tr>
  <tr>
   <td>getGrantedUsers</td>
   <td>ProcessManagementQueueService</td>
   <td>getGrantedUsers</td>
   <td>로그인한 사용자의 큐에 액세스할 수 있는 모든 사용자를 반환합니다.</td>
  </tr>
  <tr>
   <td>getUsersForAccessibleQueues</td>
   <td>ProcessManagementQueueService</td>
   <td>getUsersForAccessibleQueues</td>
   <td>사용자가 큐에 액세스할 수 있는 모든 사용자를 반환합니다.</td>
  </tr>
  <tr>
   <td>revokeQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>revokeQueueAccess</td>
   <td>로그인한 사용자 큐에 액세스할 수 있는 사용자 목록에서 사용자를 제거합니다.</td>
  </tr>
  <tr>
   <td>removeQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>removeQueueAccess</td>
   <td>로그인한 사용자가 큐에 액세스할 수 있는 사용자 목록에서 사용자를 제거합니다.</td>
  </tr>
  <tr>
   <td>getAllQueues<br /> </td>
   <td>ProcessManagementQueueService<br /> </td>
   <td>getAllQueues<br /> </td>
   <td>로그인한 사용자가 액세스할 수 있는 모든 큐(자체, 공유 및 그룹 큐)를 가져옵니다.<br /> </td>
  </tr>
  <tr>
   <td>getOutOfOfficeSettings</td>
   <td>ProcessManagementOutOfOfficeService</td>
   <td>getOutOfOfficeSettings</td>
   <td>사용자의 사무실 설정을 벗어납니다.</td>
  </tr>
  <tr>
   <td>saveOutOfOfficeSettingsJson</td>
   <td>ProcessManagementOutOfOfficeService</td>
   <td>saveOutOfOfficeSettingsJson</td>
   <td>사용자의 부재 설정을 저장합니다.</td>
  </tr>
  <tr>
   <td>getAllProcesses</td>
   <td>ProcessManagementProcessService</td>
   <td>getAllProcesses</td>
   <td>모든 프로세스 목록을 반환합니다.</td>
  </tr>
  <tr>
   <td>getParticipatedProcesses</td>
   <td>ProcessManagementProcessService</td>
   <td>getParticipatedProcesses</td>
   <td>로그인한 사용자가 참여한 모든 프로세스 이름의 목록을 반환합니다.</td>
  </tr>
  <tr>
   <td>getProcessInstance<br /> </td>
   <td>ProcessManagementProcessService<br /> </td>
   <td>getProcessInstance<br /> </td>
   <td>프로세스 인스턴스의 세부 사항을 가져옵니다.<br /> </td>
  </tr>
  <tr>
   <td>getProcessInstances</td>
   <td>ProcessManagementQueryService</td>
   <td>getProcessInstances</td>
   <td>프로세스에 대한 모든 프로세스 인스턴스를 가져옵니다.</td>
  </tr>
  <tr>
   <td>getPendingTasksForProcessInstance</td>
   <td>ProcessManagementQueryService</td>
   <td>getPendingTasksForProcessInstance</td>
   <td>프로세스 인스턴스에 대해 보류 중인 작업을 가져옵니다.</td>
  </tr>
  <tr>
   <td>getTasksForProcessInstance</td>
   <td>ProcessManagementQueryService</td>
   <td>getTasksForProcessInstance</td>
   <td>프로세스 인스턴스에 대한 모든 작업을 가져옵니다.</td>
  </tr>
  <tr>
   <td>getAllSearchTemplates</td>
   <td>ProcessManagementQueryService</td>
   <td>getAllSearchTemplates</td>
   <td>모든 검색 템플릿 목록을 반환합니다.</td>
  </tr>
  <tr>
   <td>getTemplate</td>
   <td>ProcessManagementQueryService</td>
   <td>getTemplate</td>
   <td>검색 템플릿에 대한 컨텐츠를 반환합니다.</td>
  </tr>
  <tr>
   <td>findTasksJson<br /> </td>
   <td>ProcessManagementQueryService</td>
   <td>findTasksJson</td>
   <td>검색 템플릿의 모든 조건을 충족하는 모든 작업을 검색하고 반환합니다.</td>
  </tr>
  <tr>
   <td>getAssignmentsForTask</td>
   <td>ProcessManagementTaskService</td>
   <td>getAssignmentsForTask</td>
   <td>작업에 대한 모든 과제를 가져옵니다. 예: - 사용자가 작업을 전달하거나 다른 사용자와 협의한 경우 작업에 대한 할당입니다.</td>
  </tr>
  <tr>
   <td>deleteAttachment </td>
   <td>작업 관리자 서비스</td>
   <td>deleteAttachment</td>
   <td>첨부 파일이 삭제됩니다.</td>
  </tr>
  <tr>
   <td>초기화</td>
   <td>ProcessManagementClientSessionService</td>
   <td>초기화</td>
   <td>그것은 필요하다면 주장을 다시 보도한다. 사용자를 인증합니다. 서버/클라이언트 정보에 대한 세션 매개 변수를 설정합니다. 사용자 정보 및 폴링 간격을 반환합니다.</td>
  </tr>
  <tr>
   <td>getTasksForDirectReports</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>getTasksForDirectReports</td>
   <td>로그인한 관리자의 모든 직접 보고서 작업을 반환합니다.</td>
  </tr>
  <tr>
   <td>getTaskOfDirectReport<br /> </td>
   <td>ProcessManagementTeamTasksService</td>
   <td>getDirectReportTask</td>
   <td>로그인한 관리자의 지정된 직접 보고서 작업을 반환합니다.</td>
  </tr>
  <tr>
   <td>forwardTaskOfDirectReport</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>forwardTaskOfDirectReport</td>
   <td>다른 사용자에게 직접 보고서 작업을 전달합니다.</td>
  </tr>
  <tr>
   <td>rejectTaskOfDirectReport</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>rejectTaskOfDirectReport</td>
   <td>이전 사용자에게 직접 보고서의 작업을 반환합니다.</td>
  </tr>
  <tr>
   <td>getProperty</td>
   <td>작업 공간 속성 서비스</td>
   <td>getProperty</td>
   <td>사용자에 대한 Workspace 속성을 가져옵니다.</td>
  </tr>
  <tr>
   <td>removeProperty</td>
   <td>작업 공간 속성 서비스</td>
   <td>삭제</td>
   <td>사용자의 Workspace 속성을 제거합니다.</td>
  </tr>
  <tr>
   <td>getProperties</td>
   <td>작업 공간 속성 서비스</td>
   <td>getPropertiesAsMap</td>
   <td>사용자에 대한 모든 작업 공간 속성을 반환합니다.</td>
  </tr>
  <tr>
   <td>setProperty</td>
   <td>작업 공간 속성 서비스</td>
   <td>setProperty</td>
   <td>사용자에 대한 작업 공간 속성을 설정합니다.</td>
  </tr>
  <tr>
   <td>getCurrentUserImageUrl</td>
   <td>ProcessManagementClientSessionService</td>
   <td>getCurrentUserImageUrl</td>
   <td>로그인한 사용자의 이미지 URL을 가져옵니다.</td>
  </tr>
  <tr>
   <td>getUserImageUrl</td>
   <td>ProcessManagementClientSessionService</td>
   <td>getUserImageUrl</td>
   <td>지정된 사용자의 이미지 URL을 가져옵니다.</td>
  </tr>
  <tr>
   <td>uploadNote</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>uploadNote</td>
   <td>작업에 대한 메모를 서버에 업로드합니다.</td>
  </tr>
  <tr>
   <td>uploadRMAToServer(html 템플릿에서 직접 호출되기도 함)<br /> </td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>uploadAttachment</td>
   <td>작업을 위해 서버에 첨부 파일을 업로드합니다.</td>
  </tr>
  <tr>
   <td>getImageURL(html 템플릿에서도 직접 호출됨)</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>getImage</td>
   <td>프로세스에 대한 이미지를 가져옵니다.</td>
  </tr>
 </tbody>
</table>
