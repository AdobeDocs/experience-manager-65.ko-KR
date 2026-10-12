---
title: 작업 세부 정보 페이지 사용자 정의
description: AEM Forms 작업 영역에서 작업 세부 정보 페이지를 사용자 정의하여 작업에 대해 표시되는 기본 정보를 수정하는 방법
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 48c24442-22d2-4d1a-9462-0aba78340281
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 4%
---
# 작업 세부 정보 페이지 사용자 정의 {#customizing-the-task-details-page}

작업 세부 정보 페이지에는 작업 및 해당 프로세스에 대한 정보가 포함되어 있습니다. 하지만 작업 세부 정보 페이지를 사용자 정의하여 정보를 추가하거나 삭제할 수 있습니다.

작업 세부 정보 페이지에 다음 정보를 추가할 수 있습니다.

* 작업의 JSON 개체에서 사용할 수 있는 정보([AEM Forms 작업 영역 JSON 개체 설명](/help/forms/using/html-workspace-json-object-description.md)의 작업 섹션)
* 프로세스 인스턴스의 JSON 개체에서 사용할 수 있는 정보([AEM Forms 작업 영역 JSON 개체 설명](/help/forms/using/html-workspace-json-object-description.md)의 프로세스 인스턴스 섹션)

작업 세부 정보 페이지를 사용자 정의하려면 다음과 같이 하십시오.

1. [AEM Forms 작업 영역 사용자 지정에 대한 일반 단계를 따르십시오.](/help/forms/using/generic-steps-html-workspace-customization.md)
1. 추가 정보를 표시하려면 `todo`블록 > `details`블록 > `app`블록 > [`required`블록]에서 해당 키-값 쌍을 `translation.json` 파일에 추가하십시오.

   [`required`block]은(는) 작업 정보에 대한 작업 블록, 프로세스 정보에 대한 프로세스 블록, 보류 중인 작업 정보에 대한 currentpendingtask 블록 등 사용 가능한 블록을 나타냅니다.

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

1. `/libs/ws/js/runtime/templates/taskdetails.html`을(를) `/apps/ws/js/runtime/templates/taskdetails.html`에 복사합니다.

   `/apps/ws/js/runtime/templates/taskdetails.html`에 새 정보를 추가합니다. 예:

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

   `text!/lc/libs/ws/js/runtime/templates/taskdetails.html`을(를) 검색하여 `text!/lc/apps/ws/js/runtime/templates/taskdetails.html`(으)로 바꾸십시오.

>[!NOTE]
>
>AEM Forms 작업 영역의 **프로세스 시작** 탭에서 만든 작업으로 작업 세부 정보 페이지를 사용자 지정하려면 `/apps/ws/js/runtime/templates/startprocess.html`에 새 정보를 추가하십시오.
>
>세부 정보 페이지에 추가된 정보에 새 스타일을 추가하려면 [Workspace 사용자 지정](changing-locale-user-interface.md)의 *사용자 인터페이스 변경* 섹션을 사용하여 CSS 파일을 수정하십시오.
