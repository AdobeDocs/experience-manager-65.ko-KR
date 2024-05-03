---
title: 작업 세부 정보 페이지 사용자 정의
description: AEM Forms 작업 영역에서 작업 세부 정보 페이지를 사용자 정의하여 작업에 대해 표시되는 기본 정보를 수정하는 방법
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 48c24442-22d2-4d1a-9462-0aba78340281
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# 작업 세부 정보 페이지 사용자 정의 {#customizing-the-task-details-page}

작업 세부 정보 페이지에는 작업 및 해당 프로세스에 대한 정보가 포함되어 있습니다. 하지만 작업 세부 정보 페이지를 사용자 정의하여 정보를 추가하거나 삭제할 수 있습니다.

작업 세부 정보 페이지에 다음 정보를 추가할 수 있습니다.

* 작업의 JSON 개체에서 사용할 수 있는 정보(의 작업 섹션) [AEM Forms 작업 영역 JSON 개체 설명](/help/forms/using/html-workspace-json-object-description.md))
* 프로세스 인스턴스의 JSON 개체에서 사용할 수 있는 정보(의 프로세스 인스턴스 섹션) [AEM Forms 작업 영역 JSON 개체 설명](/help/forms/using/html-workspace-json-object-description.md))

작업 세부 정보 페이지를 사용자 정의하려면 다음과 같이 하십시오.

1. 팔로우 [AEM Forms 작업 영역 사용자 정의에 대한 일반 단계입니다.](/help/forms/using/generic-steps-html-workspace-customization.md)
1. 추가 정보를 표시하려면 해당 키-값 쌍을 `translation.json` 파일 위치: `todo`블록 > `details`블록 > `app`블록 > [`required`차단].

   다음 [`required`차단] 은 작업 정보의 작업 블록, 프로세스 정보의 프로세스 블록, 보류 중인 작업 정보의 currentpendingtask 블록 등 사용 가능한 블록을 나타냅니다.

   예를 들어, 작업 세부 정보 페이지에서 경로 선택 필요 정보를 추가하려면 작업 블록에 다음 키-값 쌍을 추가할 수 있습니다.

   ```json
   "todo" : {
       .
       .
       .
       "details" : {
           .
           .
           "task" : {
               .
               .
               "RouteSelectionRequired" : "Route Selection Required"
           }
       }
   }
   ```

   >[!NOTE]
   >
   >지원되는 모든 언어에 해당하는 키-값 쌍을 추가합니다.

1. 복사 `/libs/ws/js/runtime/templates/taskdetails.html` 끝 `/apps/ws/js/runtime/templates/taskdetails.html`.

   새 정보 추가 `/apps/ws/js/runtime/templates/taskdetails.html`. 예:

   ```css
   <div class="detailsContainer">
       .
       .
       <ul>
           .
           .
           <li>
               <label for="routeSelectionRequired" title="<%= $.t('todo.details.task.RouteSelectionRequired')%>"><%= $.t('todo.details.task.RouteSelectionRequired')%></label>
               <div>
                   <span id="routeSelectionRequired"><%= isRouteSelectionRequired != null ? isRouteSelectionRequired : ''%></span>
               </div>
           </li>
           .
           .
       </ul>
   </div>
   ```

1. 편집하려면 /apps/ws/js/registry.js을 여십시오.

   검색 및 바꾸기 `text!/lc/libs/ws/js/runtime/templates/taskdetails.html` 포함 `text!/lc/apps/ws/js/runtime/templates/taskdetails.html`.

>[!NOTE]
>
>에서 생성된 작업으로 작업 세부 정보 페이지를 사용자 정의하려면 **프로세스 시작** AEM Forms 작업 영역의 탭에서 새 정보를 추가할 위치: `/apps/ws/js/runtime/templates/startprocess.html`.
>
>세부 정보 페이지에 추가된 정보에 대한 새 스타일을 추가하려면 다음을 사용하여 CSS 파일을 수정합니다. *사용자 인터페이스 변경 사항* 의 섹션 [작업 영역 사용자 지정](changing-locale-user-interface.md).
