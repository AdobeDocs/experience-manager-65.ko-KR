---
title: 작업 세부 사항 페이지 사용자 정의
seo-title: 작업 세부 사항 페이지 사용자 정의
description: AEM Forms 작업 영역의 작업 세부 사항 페이지를 사용자 지정하여 작업에 대해 표시되는 기본 정보를 수정하는 방법입니다.
seo-description: AEM Forms 작업 영역의 작업 세부 사항 페이지를 사용자 지정하여 작업에 대해 표시되는 기본 정보를 수정하는 방법입니다.
uuid: d85fae55-8e66-4595-8560-5485622b6841
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 16e57cf6-aaa1-406d-a6ad-71ec60b15386
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 작업 세부 사항 페이지 사용자 정의 {#customizing-the-task-details-page}

작업 세부 정보 페이지에는 작업 및 해당 프로세스에 대한 정보가 들어 있습니다. 그러나 작업 세부 정보 페이지를 사용자 지정하여 정보를 추가하거나 삭제할 수 있습니다.

다음 정보를 작업 세부 사항 페이지에 추가할 수 있습니다.

* 작업의 JSON 개체에서 사용할 수 있는 정보(AEM Forms 작업 영역 JSON [개체 설명의 작업 섹션](/help/forms/using/html-workspace-json-object-description.md))
* 프로세스 인스턴스의 JSON 개체에서 사용할 수 있는 정보(AEM Forms 작업 영역의 [프로세스 인스턴스 섹션 JSON 개체 설명](/help/forms/using/html-workspace-json-object-description.md))

작업 세부 사항 페이지를 사용자 정의하려면

1. AEM [Forms 작업 영역 사용자 지정에 대한 일반 단계를 수행합니다.](/help/forms/using/generic-steps-html-workspace-customization.md)
1. 추가 정보를 표시하려면 해당 키-값 쌍을 `translation.json` 블록 > `todo`블록 > `details`블록 > `app`블록에 있는 파일에 추가합니다 [ `required`].

   이 [ 블록은 `required`] 작업 정보의 작업 블록, 프로세스 정보의 프로세스 블록, 보류 중인 작업 정보에 대한 현재 보류 중인 작업 블록과 같은 사용 가능한 블록을 참조합니다.

   예를 들어, 작업 세부 사항 페이지에서 경로 선택 필수 정보에 대한 정보를 추가하려면 작업 블록에 다음 키-값 쌍을 추가할 수 있습니다.

   ```
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

1. 복사 `/libs/ws/js/runtime/templates/taskdetails.html` 대상 `/apps/ws/js/runtime/templates/taskdetails.html`.

   새 정보를 에 `/apps/ws/js/runtime/templates/taskdetails.html`추가합니다. 예:

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

1. /apps/ws/js/registry.js편집을 위해 엽니다.

   검색 및 `text!/lc/libs/ws/js/runtime/templates/taskdetails.html` 바꾸기 `text!/lc/apps/ws/js/runtime/templates/taskdetails.html`기능

>[!NOTE]
>
>AEM Forms 작업 영역의 **프로세스 시작** 탭에서 만든 작업을 작업 세부 정보 페이지에 사용자 정의하려면 새 정보를 에 추가합니다 `/apps/ws/js/runtime/templates/startprocess.html`.
>
>세부 사항 페이지에 추가된 정보에 대한 새 스타일을 추가하려면 작업 영역 사용자 정의 *의 사용자 인터페이스 변경* 섹션을 사용하여 CSS 파일을 [수정합니다](/help/forms/using/changing-locale-user-interface.md#main-pars-header-3).
