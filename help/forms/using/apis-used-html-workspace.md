---
title: AEM Forms 작업 영역에서 사용되는 API
description: 공용 Java&trade 및 JavaScript API와 AEM Forms 작업 영역 LiveCycle 방법으로, 사용자 정의 및 자동화에 노출됩니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 9034f73a-83f3-498e-b6a6-ad6577aa1a3a
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 1%

---

# AEM Forms 작업 영역에서 사용되는 API {#apis-used-in-aem-forms-workspace}

AEM Forms 작업 영역에서는 다음 API가 사용됩니다.

<table>
 <tbody>
  <tr>
   <td><strong>JavaScript 메서드</strong></td>
   <td><strong>서비스 이름</strong></td>
   <td><strong>API 이름</strong></td>
   <td><strong>댓글</strong></td>
  </tr>
  <tr>
   <td>getGroups</td>
   <td>프로세스 관리 사용자 프록시 서비스</td>
   <td>getGroups</td>
   <td>그룹을 검색합니다. 지정하지 않으면 모든 그룹의 목록을 반환하고, 지정하지 않으면 지정한 이름의 그룹을 반환합니다.</td>
  </tr>
  <tr>
   <td>getUsersAndGroups</td>
   <td>프로세스 관리 사용자 프록시 서비스</td>
   <td>getUsersAndGroups</td>
   <td>사용자 및 그룹을 검색합니다. 지정된 내용이 없는 경우 모든 사용자 및 그룹 목록을 반환하고, 지정된 이름의 사용자 및 그룹을 반환합니다.</td>
  </tr>
  <tr>
   <td>prepareForSubmit</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>prepareForSubmit</td>
   <td>DocumentSubmitServlet을 통해 양식을 제출하기 전에 호출됩니다. 실제 제출 중에 검색되는 세션 변수(만료 시간과 함께)에 작업 ID를 설정합니다.</td>
  </tr>
  <tr>
   <td>submitTask</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>제출</td>
   <td>작업과 연결된 문서 객체를 제출합니다(및 제출 프로세스를 차례로).</td>
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
   <td>카테고리에 대한 모든 직접 하위 항목을 가져옵니다.</td>
  </tr>
  <tr>
   <td>getAllStartpoints</td>
   <td>ProcessManagementStartpointService</td>
   <td>getAllStartpoints</td>
   <td>모든 카테고리의 서버에 있는 모든 시작 지점을 가져옵니다.</td>
  </tr>
  <tr>
   <td>invokeStartpoint</td>
   <td>ProcessManagementStartpointService</td>
   <td>invokeStartpoint</td>
   <td>시작점을 호출하고 시작점에 해당하는 작업을 만듭니다.</td>
  </tr>
  <tr>
   <td>getAllTask</td>
   <td>ProcessManagementTaskService</td>
   <td>getAllActionTasks</td>
   <td>로그인한 사용자에 대해 생성 및 전달 또는 상담, 저장, 할당, 할당 및 저장되는 모든 작업을 가져옵니다.</td>
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
   <td>작업을 렌더링하고 필요한 경우 양식 url, 양식 유형, 데이터 url과 같은 양식을 렌더링하는 데 필요한 정보를 반환합니다.</td>
  </tr>
  <tr>
   <td>submitWithPriorData</td>
   <td>ProcessManagementTaskService</td>
   <td>submitWithPriorData</td>
   <td>결과 키를 사용하여 TaskManager의 제출 API 결과를 반환합니다.</td>
  </tr>
  <tr>
   <td>submitWithdata</td>
   <td>ProcessManagementTaskService</td>
   <td>submitWithdata</td>
   <td>이 코드는 TaskManager의 submit API를 사용하여 작업과 연결된 양식 데이터(문자열로 전달됨)를 제출합니다. 이 변수는 callTaskManager의 submit API가 아닌 Flex Forms에 사용됩니다.</td>
  </tr>
  <tr>
   <td>저장</td>
   <td>ProcessManagementTaskService</td>
   <td>저장</td>
   <td>서버에 작업이 저장됩니다.</td>
  </tr>
  <tr>
   <td>완료</td>
   <td>ProcessManagementTaskService</td>
   <td>완료</td>
   <td>이 플러그인은 작업을 완료하고 프로세스 설계에 따라 다음 단계로 작업을 전달합니다.</td>
  </tr>
  <tr>
   <td>getAttachment</td>
   <td>ProcessManagementTaskService</td>
   <td>getAttachment</td>
   <td>첨부 파일을 사용할 수 있는 첨부 파일의 URL을 반환합니다.</td>
  </tr>
  <tr>
   <td>모든 첨부 파일 가져오기</td>
   <td>ProcessManagementTaskService</td>
   <td>getAllActionableAttachments</td>
   <td>작업에 대한 모든 첨부 파일과 메모를 가져옵니다.</td>
  </tr>
  <tr>
   <td>공유</td>
   <td>ProcessManagementTaskService</td>
   <td>공유</td>
   <td>다른 사용자와 작업을 공유합니다. 다른 사용자가 작업을 요청할 수 있으며 작업의 소유자가 됩니다.</td>
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
   <td>다른 사용자와 작업을 참조합니다.</td>
  </tr>
  <tr>
   <td>클레임</td>
   <td>ProcessManagementTaskService</td>
   <td>클레임</td>
   <td>공유 큐에서 사용할 수 있는 작업을 요구합니다.</td>
  </tr>
  <tr>
   <td>잠금 해제</td>
   <td>ProcessManagementTaskService</td>
   <td>잠금 해제</td>
   <td>작업의 잠금을 해제합니다.</td>
  </tr>
  <tr>
   <td>잠금</td>
   <td>ProcessManagementTaskService</td>
   <td>잠금</td>
   <td>작업을 잠그고 공유 시 다른 사용자가 작업을 요청할 수 없습니다.</td>
  </tr>
  <tr>
   <td>거부</td>
   <td>ProcessManagementTaskService</td>
   <td>거부</td>
   <td>작업의 이전 소유자에게 작업을 반환합니다.</td>
  </tr>
  <tr>
   <td>중단</td>
   <td>ProcessManagementTaskService</td>
   <td>중단</td>
   <td>작업이 삭제됩니다.</td>
  </tr>
  <tr>
   <td>setVisible</td>
   <td>ProcessManagementTaskService</td>
   <td>setVisible</td>
   <td>작업의 가시성을 설정합니다. 가시성이 false로 설정된 경우 나중에 작업이 사용자에게 표시되지 않습니다.</td>
  </tr>
  <tr>
   <td>getUsers</td>
   <td>프로세스 관리 사용자 프록시 서비스</td>
   <td>getUsers</td>
   <td>사용자 검색에 사용됩니다. 이름이 지정되지 않으면 모든 사용자를 반환하고, 그렇지 않으면 지정된 이름의 사용자를 반환합니다.</td>
  </tr>
  <tr>
   <td>getUsersInGroup</td>
   <td>프로세스 관리 사용자 프록시 서비스</td>
   <td>getUsersInGroupByName</td>
   <td>그룹의 모든 사용자를 반환합니다.</td>
  </tr>
  <tr>
   <td>grantQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>grantQueueAccess</td>
   <td>로그인한 사용자의 대기열에 대한 액세스 권한을 지정된 사용자에게 부여합니다. 기본적으로 자신의 큐를 다른 사용자와 공유하고 있습니다.</td>
  </tr>
  <tr>
   <td>requestQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>requestQueueAccess</td>
   <td>로그인한 사용자에 대해 지정된 사용자의 큐에 대한 액세스 요청을 수행합니다. 사용자가 요청을 승인하면 사용자의 큐가 로그인한 사용자와 공유됩니다.</td>
  </tr>
  <tr>
   <td>getGrantedUsers</td>
   <td>ProcessManagementQueueService</td>
   <td>getGrantedUsers</td>
   <td>로그인한 사용자의 대기열에 액세스할 수 있는 모든 사용자가 반환됩니다.</td>
  </tr>
  <tr>
   <td>getUsersForAccessibleQueues</td>
   <td>ProcessManagementQueueService</td>
   <td>getUsersForAccessibleQueues</td>
   <td>사용자가 대기열에 액세스할 수 있는 모든 사용자가 반환됩니다.</td>
  </tr>
  <tr>
   <td>revokeQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>revokeQueueAccess</td>
   <td>로그인한 사용자의 대기열에 액세스할 수 있는 사용자 목록에서 사용자를 제거합니다.</td>
  </tr>
  <tr>
   <td>removeQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>removeQueueAccess</td>
   <td>로그인한 사용자가 대기열에 액세스할 수 있는 사용자 목록에서 사용자를 제거합니다.</td>
  </tr>
  <tr>
   <td>getAllQueues<br /> </td>
   <td>ProcessManagementQueueService<br /> </td>
   <td>getAllQueues<br /> </td>
   <td>로그인한 사용자가 액세스할 수 있는 모든 대기열(소유, 공유 및 그룹 대기열)을 가져옵니다.<br /> </td>
  </tr>
  <tr>
   <td>getOutOfOfficeSettings</td>
   <td>ProcessManagementOutOfOfficeService</td>
   <td>getOutOfOfficeSettings</td>
   <td>사용자의 부재 중 설정을 가져옵니다.</td>
  </tr>
  <tr>
   <td>saveOutOfOfficeSettingsJson</td>
   <td>ProcessManagementOutOfOfficeService</td>
   <td>saveOutOfOfficeSettingsJson</td>
   <td>사용자의 부재 중 설정을 저장합니다.</td>
  </tr>
  <tr>
   <td>getAllProcesses</td>
   <td>ProcessManagementProcessService</td>
   <td>getAllProcesses</td>
   <td>모든 프로세스의 목록을 반환합니다.</td>
  </tr>
  <tr>
   <td>getParticipedProcesses</td>
   <td>ProcessManagementProcessService</td>
   <td>getParticipedProcesses</td>
   <td>로그인한 사용자가 참여한 모든 프로세스 이름 목록을 반환합니다.</td>
  </tr>
  <tr>
   <td>getProcessInstance<br /> </td>
   <td>ProcessManagementProcessService<br /> </td>
   <td>getProcessInstance<br /> </td>
   <td>프로세스 인스턴스의 세부 정보를 가져옵니다.<br /> </td>
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
   <td>작업에 대한 모든 할당을 가져옵니다. 예를 들어 사용자가 다른 사용자와 작업을 전달하거나 상담하는 경우, 이 작업은 작업에 대한 할당입니다.</td>
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
   <td>필요한 경우 어설션을 갱신합니다. 사용자를 인증합니다. 서버/클라이언트 정보에 대한 세션 매개 변수를 설정합니다. 사용자 정보 및 폴링 간격을 반환합니다.</td>
  </tr>
  <tr>
   <td>getTasksForDirectReports</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>getTasksForDirectReports</td>
   <td>로그인한 관리자의 직접 보고 작업을 모두 반환합니다.</td>
  </tr>
  <tr>
   <td>getTaskOfDirectReport<br /> </td>
   <td>ProcessManagementTeamTasksService</td>
   <td>getDirectReportTask</td>
   <td>로그인한 관리자에 대해 지정된 직접 보고서의 작업을 반환합니다.</td>
  </tr>
  <tr>
   <td>정방향 작업</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>정방향 작업</td>
   <td>직접 보고서의 작업을 다른 사용자에게 전달합니다.</td>
  </tr>
  <tr>
   <td>rejectTaskOfDirectReport</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>rejectTaskOfDirectReport</td>
   <td>이전 사용자에게 직접 보고 작업을 반환합니다.</td>
  </tr>
  <tr>
   <td>getProperty</td>
   <td>WorkspacePropertyService</td>
   <td>getProperty</td>
   <td>사용자의 작업 영역 속성을 가져옵니다.</td>
  </tr>
  <tr>
   <td>removeProperty</td>
   <td>WorkspacePropertyService</td>
   <td>삭제</td>
   <td>사용자의 작업 영역 속성을 제거합니다.</td>
  </tr>
  <tr>
   <td>getProperties</td>
   <td>WorkspacePropertyService</td>
   <td>getPropertiesAsMap</td>
   <td>사용자의 모든 작업 영역 속성을 반환합니다.</td>
  </tr>
  <tr>
   <td>setProperty</td>
   <td>WorkspacePropertyService</td>
   <td>setProperty</td>
   <td>사용자의 작업 영역 속성을 설정합니다.</td>
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
   <td>지정된 사용자에 대한 사용자의 이미지 URL을 가져옵니다.</td>
  </tr>
  <tr>
   <td>uploadNote</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>uploadNote</td>
   <td>서버에 작업에 대한 메모를 업로드합니다.</td>
  </tr>
  <tr>
   <td>uploadRMAToServer(html 템플릿에서도 직접 호출됩니다.)<br /> </td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>uploadAttachment</td>
   <td>서버에 작업에 대한 첨부 파일을 업로드합니다.</td>
  </tr>
  <tr>
   <td>getImageURL(HTML 템플릿에서도 직접 호출됨)</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>getImage</td>
   <td>프로세스에 대한 이미지를 가져옵니다.</td>
  </tr>
 </tbody>
</table>
