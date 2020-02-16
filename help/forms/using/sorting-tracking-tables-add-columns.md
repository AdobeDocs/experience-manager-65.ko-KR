---
title: 추적 테이블 사용자 정의
seo-title: 추적 테이블 사용자 정의
description: AEM Forms 작업 영역의 추적 탭에 표시되는 작업 테이블에서 사용자 프로세스의 세부 사항 표시를 사용자 지정하는 방법.
seo-description: AEM Forms 작업 영역의 추적 탭에 표시되는 작업 테이블에서 사용자 프로세스의 세부 사항 표시를 사용자 지정하는 방법.
uuid: 13d6ebf2-99d5-434f-85f9-b0cba5f5751a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: bb7a6e9f-4f28-4d97-8a0c-949259fd6857
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 추적 테이블 사용자 정의{#customize-tracking-tables}

AEM Forms 작업 영역의 추적 탭은 로그인한 사용자가 관련된 프로세스 인스턴스의 세부 사항을 표시하는 데 사용됩니다. 추적 테이블을 보려면 먼저 왼쪽 창에서 프로세스 이름을 선택하여 가운데 창에 인스턴스 목록을 표시합니다. 오른쪽 창에서 이 인스턴스에서 생성된 작업 테이블을 보려면 프로세스 인스턴스를 선택합니다. 기본적으로 테이블 열에는 다음 작업 속성이 표시됩니다(작업 모델의 해당 속성이 괄호 안에 표시됨).

* ID ( `taskId`)
* 이름 ( `stepName`)
* 지침 ( `instructions`)
* 선택된 동작 ( `selectedRoute`)
* 작성 시간( `createTime`)
* 완료 시간( `completeTime`)
* 소유자 ( `currentAssignment.queueOwner`)

작업 테이블에 표시할 수 있는 작업 모델의 나머지 속성은 다음과 같습니다.

<table>
 <tbody>
  <tr>
   <td><p>actionInstanceId</p> </td>
   <td><p>isOpenFullScreen</p> </td>
   <td><p>reminderCount</p> </td>
  </tr>
  <tr>
   <td><p>classOfTask</p> </td>
   <td><p>isOwner</p> </td>
   <td><p>routeList</p> </td>
  </tr>
  <tr>
   <td><p>consultGroupId</p> </td>
   <td><p>isRouteSelectionRequired</p> </td>
   <td><p>savedFormCount</p> </td>
  </tr>
  <tr>
   <td><p>contentType</p> </td>
   <td><p>isShowAttachments</p> </td>
   <td><p>serializedImageTicket</p> </td>
  </tr>
  <tr>
   <td><p>createTime</p> </td>
   <td><p>isStartTask</p> </td>
   <td><p>serviceName</p> </td>
  </tr>
  <tr>
   <td><p>creationId</p> </td>
   <td><p>isVisible</p> </td>
   <td><p>serviceTitle</p> </td>
  </tr>
  <tr>
   <td><p>currentAssignment</p> </td>
   <td><p>nextReminder</p> </td>
   <td><p>showACLActions</p> </td>
  </tr>
  <tr>
   <td><p>기한</p> </td>
   <td><p>numForms</p> </td>
   <td><p>showDirectActions</p> </td>
  </tr>
  <tr>
   <td><p>설명</p> </td>
   <td><p>numFormsToBeSaved</p> </td>
   <td><p>상태</p> </td>
  </tr>
  <tr>
   <td><p>displayName</p> </td>
   <td><p>outOfOfficeUserId</p> </td>
   <td><p>summaryUrl</p> </td>
  </tr>
  <tr>
   <td><p>forwardGroupId</p> </td>
   <td><p>outOfOfficeUserName</p> </td>
   <td><p>supportsSave</p> </td>
  </tr>
  <tr>
   <td><p>isApprovalUI</p> </td>
   <td><p>우선 순위</p> </td>
   <td><p>taskACL</p> </td>
  </tr>
  <tr>
   <td><p>isCustomUI</p> </td>
   <td><p>processInstanceId</p> </td>
   <td><p>taskFormType</p> </td>
  </tr>
  <tr>
   <td><p>isDefaultImage</p> </td>
   <td><p>processInstanceStatus</p> </td>
   <td><p>taskUserInfo</p> </td>
  </tr>
  <tr>
   <td><p>isLocked</p> </td>
   <td><p>processVariables</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p>isMustOpenToComplete</p> </td>
   <td><p>readerSubmitOptions</p> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

작업 테이블에서 다음 사용자 지정을 수행하려면 소스 코드에서 의미 변경을 수행해야 합니다. 작업 [공간 SDK를 사용하여 의미 체계 변경을 수행하고 변경된 소스에서 축소된 패키지를 생성하는 방법은 AEM Forms 작업 영역](/help/forms/using/introduction-customizing-html-workspace.md) 사용자 지정 소개를 참조하십시오.

## 표 열 및 해당 순서 변경 {#changing-table-columns-and-their-order}

1. 테이블 및 해당 주문에 표시된 작업 속성을 수정하려면 /ws/js/runtime/templates/processinstancehistory.html 파일을 구성합니다.

   ```as3
   <table>
       <thead>
           <tr>
               <!-- put the column headings in order here, for example-->
               <th><%= $.t('history.fixedTaskTableHeader.taskName')%></th>
               <th><%= $.t('history.fixedTaskTableHeader.taskInstructions')%></th>
               <th><%= $.t('history.fixedTaskTableHeader.taskRoute')%></th>
               <th><%= $.t('history.fixedTaskTableHeader.taskCreateTime')%></th>
               <th><%= $.t('history.fixedTaskTableHeader.taskCompleteTime')%></th>
           </tr>
       </thead>
   </table>
   ```

   ```as3
   <table>
       <tbody>
           <%_.each(obj, function(task){%>
           <tr>
               <!-- Put the task attributes in the order of headings, for example -->
               <td><%= task.stepName %></td>
               <td><%= task.instructions %></td>
               <td><%= !task.selectedRoute?'':(task.selectedRoute=='null'?'Default':task.selectedRoute) %></td>
               <td><%= task.createTime?task.formattedCreateTime:'' %></td>
               <td><%= task.completeTime? task.formattedCompleteTime:'' %></td>
           </tr>
           <%});%>
       </tbody>
   </table>
   ```

## 추적 테이블 정렬 {#sorting-a-tracking-table}

열 머리글을 클릭할 때 작업 목록 테이블을 정렬하려면 다음을 수행합니다.

1. 파일에서 에 대한 클릭 핸들러를 `.fixedTaskTableHeader th` 등록합니다 `js/runtime/views/processinstancehistory.js`.

   ```as3
   events: {
       //other handlers
       "click .fixedTaskTableHeader th": "onTaskTableHeaderClick",
       //other handlers
   }
   ```

   처리기에서 의 `onTaskTableHeaderClick` 함수를 `js/runtime/util/history.js`호출합니다.

   ```as3
   onTaskTableHeaderClick: function (event) {
           history.onTaskTableHeaderClick(event);
   }
   ```

1. 메서드를 `TaskTableHeaderClick` 표시합니다 `js/runtime/util/history.js`.

   이 메서드는 클릭 이벤트에서 작업 속성을 찾고, 해당 속성에 대한 작업 목록을 정렬하고, 정렬된 작업 목록과 함께 작업 테이블을 렌더링합니다.

   비교자 함수를 제공하여 작업 목록 컬렉션의 백본 정렬 기능을 사용하여 정렬이 수행됩니다.

   ```as3
       return {
           //other methods
           onTaskTableHeaderClick  : onTaskTableHeaderClick,
           //other methods
       };
   ```

   ```as3
   onTaskTableHeaderClick = function (event) {
           var target = $(event.target),
            comparator,
               attribute;
           if(target.hasClass('taskName')){
            attribute = 'stepName';
           } else if(target.hasClass('taskInstructions')){
               attribute = 'instructions';
           } else if(target.hasClass('taskRoute')){
               attribute = 'selectedRoute';
           } else if(target.hasClass('taskCreateTime')){
               attribute = 'createTime';
           } else if(target.hasClass('taskCompleteTime')){
               attribute = 'completeTime';
           }
           taskList.comparator = function (task) {
            return task.get(attribute);
           };
           taskList.sort();
           render();
       };
   ```

**[지원 문의](https://www.adobe.com/account/sign-in.supportportal.html)**
