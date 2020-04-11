---
title: 경로 작업에 사용되는 이미지 사용자 정의
seo-title: 경로 작업에 사용되는 이미지 사용자 정의
description: LiveCycle AEM Forms 작업 영역의 라우트 작업에 사용되는 이미지를 사용자 지정하는 방법.
seo-description: LiveCycle AEM Forms 작업 영역의 라우트 작업에 사용되는 이미지를 사용자 지정하는 방법.
uuid: 42608376-587e-4b57-a9d5-8f9ebd981426
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 10158c13-47b4-43e3-ac47-690f3cbab158
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 경로 작업에 사용되는 이미지 사용자 정의 {#customize-images-used-in-route-actions}

경로 작업에 사용되는 이미지를 사용자 정의하려면 사용자 [정의](/help/forms/using/generic-steps-html-workspace-customization.md) 일반 단계에 설명된 단계에 따라 이 문서에 설명된 단계를 수행합니다.

## 경로 지정을 위한 이미지 {#images-for-route-actions}

1. CSS에서 이미지를 정의하는 스타일을 새 경로 작업에 대해 다음 위치에 추가합니다.

   `/apps/ws/css/newStyle.css`

   예:아래와 `myStyle1`같이 새 스타일을 추가하고 WebDAV 클라이언트를 사용하여 이미지 파일을 `myStyleIcon1.png` `/apps/ws/image`s 폴더에 업로드합니다.

   >[!NOTE]
   >
   >WebDAV 액세스에 대한 자세한 내용은 https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html을 [참조하십시오](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html).

   >[!NOTE]
   >
   >경로 작업 이름과 같도록 스타일 이름을 사용합니다.

   ```css
   .myStyle1{
   
           background-image: url('../images/myStyleIcon1.png');
   
       }
   ```

## 작업 목록 작업 팝업 {#task-list-task-action-popup}

1. 작업 목록 작업 팝업을 만듭니다. AEM [Forms 작업 영역 코드](/help/forms/using/introduction-customizing-html-workspace.md#main-pars-heading-3)작성을 참조하십시오. 개발 패키지를 사용해야 합니다.

1. 복사 `/libs/ws/js/runtime/templates/task.html` 대상 `/apps/ws/js/runtime/templates/task.html`.

1. CSS 스타일의 이름이 서버에서 오는 경로 작업 이름과 같은 경우 다음 코드를 수정합니다. `/apps/ws/js/runtime/templates/task.html`:

   ```
   <%if(routeList == null){%>
               <li>
                   <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
               </li>
               <%}else{%>
               <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
               <li>
                   <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
               </li>
               <%}%>
               <%}%>
   
   To
   
   <%if(routeList == null){%>
               <li class="<%= availableCommands.directCommands[0]%>" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0]+'.value')%>">
                   <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
               </li>
               <%}else{%>
               <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
               <li class="<%= availableCommands.directCommands[i]%>" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[i]+'.value')%>">
                   <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
               </li>
               <%}%>
               <%}%>
   ```

1. CSS 스타일의 이름이 서버에서 오는 경로 작업 이름과 다른 경우 에서 다음 코드를 수정합니다 `/apps/ws/js/runtime/templates/task.html`. 그러면 `if-else` 서블릿 조건 스택을 추가하여 스타일을 경로 작업 이름과 매핑합니다.

```
<%if(routeList == null){%>
            <li>
                <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
            </li>
            <%}else{%>
            <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
            <li>
                <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
            </li>
            <%}%>
            <%}%>

To

<%if(routeList == null){%>
            <li class="<%= availableCommands.directCommands[0]%>" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0]+'.value')%>">
                <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
            </li>
            <%}else{%>
            <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
                <%if(availableCommands.directCommands[i].equals("myAction1")){%>
                     <li class="myStyle1" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[i]+'.value')%>">
                         <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                     </li>
                <%}else if(availableCommands.directCommands[i].equals("myAction2")){%>
                     <li class="myStyle2" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[i]+'.value')%>">
                         <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                     </li>
                <%}%>
            <%}%>
            <%}%>
```

## 작업 세부 정보 작업 팝업 {#task-details-task-action-popup}

1. 복사 `/libs/ws/js/runtime/templates/taskdetails.html` 대상 `/apps/ws/js/runtime/templates/taskdetails.html`.

1. CSS 스타일의 이름이 서버에서 오는 경로 작업 이름과 같은 경우 다음 코드를 수정합니다. `/apps/ws/js/runtime/templates/taskdetails.html`:

   ```
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                           <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                           </li>
                       <%}%>
   
   To
   
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                           <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route">
                               <i class="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"/>
                               </a>
                           </li>
                       <%}%>
   ```

1. CSS 스타일의 이름이 서버에서 오는 경로 작업 이름과 다른 경우 에서 다음 코드를 수정합니다 `/apps/ws/js/runtime/templates/taskdetails.html`. 그러면 `if-else` 서블릿 조건 스택을 추가하여 스타일을 경로 작업 이름과 매핑합니다.

   ```
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                           <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                           </li>
                       <%}%>
   
   To
   
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                   <%if(availableCommands.directCommands[i].equals("myAction1")){%>
                       <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route">
                               <i class="myStyle1" value="<%= availableCommands.directCommands[i]%>" data-action="route"/>
                               </a>
                           </li>
                   <%}else if(availableCommands.directCommands[i].equals("myAction2")){%>
                       <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route">
                               <i class="myStyle2" value="<%= availableCommands.directCommands[i]%>" data-action="route"/>
                               </a>
                           </li>
                   <%}%>
               <%}%>
   ```

1. 편집을 `/apps/ws/js/registry.js` 위해 열고 다음 텍스트를 찾습니다.
   `"text!/lc/libs/ws/js/runtime/templates/taskdetails.html"`

1. 텍스트를 다음으로 바꿉니다.
   `"text!/lc/apps/ws/js/runtime/templates/taskdetails.html"`
