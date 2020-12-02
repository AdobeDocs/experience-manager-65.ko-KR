---
title: 경로 작업에 사용되는 이미지 사용자 정의
seo-title: 경로 작업에 사용되는 이미지 사용자 정의
description: LiveCycle AEM Forms 작업 영역의 경로 작업에 사용되는 이미지를 사용자 지정하는 방법
seo-description: LiveCycle AEM Forms 작업 영역의 경로 작업에 사용되는 이미지를 사용자 지정하는 방법
uuid: 42608376-587e-4b57-a9d5-8f9ebd981426
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 10158c13-47b4-43e3-ac47-690f3cbab158
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---


# 경로 작업 {#customize-images-used-in-route-actions}에 사용되는 이미지 사용자 정의

경로 작업에 사용되는 이미지를 사용자 정의하려면 [사용자 정의 일반 단계](/help/forms/using/generic-steps-html-workspace-customization.md)에 설명된 단계에 따라 이 문서에 설명된 단계를 수행하십시오.

## 경로 작업 {#images-for-route-actions}에 대한 이미지

1. 새로운 경로 작업에 대해 다음 위치에 CSS에서 이미지를 정의하는 스타일을 추가합니다.

   `/apps/ws/css/newStyle.css`

   예:아래와 같이 `myStyle1`이라는 새 스타일을 추가하고 WebDAV 클라이언트를 사용하여 이미지 파일 `myStyleIcon1.png`을 `/apps/ws/image`s 폴더에 업로드합니다.

   >[!NOTE]
   >
   >WebDAV 액세스에 대한 자세한 내용은 [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html)을 참조하십시오.

   >[!NOTE]
   >
   >경로 작업 이름과 같도록 스타일 이름을 사용하는 것이 좋습니다.

   ```css
   .myStyle1{
   
           background-image: url('../images/myStyleIcon1.png');
   
       }
   ```

## 작업 목록 작업 팝업 {#task-list-task-action-popup}

1. 작업 목록 작업 팝업을 만듭니다. [AEM Forms 작업 공간 코드 작성](introduction-customizing-html-workspace.md#building-html-workspace-code)을 참조하십시오. 개발 패키지를 사용해야 합니다.

1. `/libs/ws/js/runtime/templates/task.html`을(를) `/apps/ws/js/runtime/templates/task.html`에 복사합니다.

1. CSS 스타일의 이름이 서버에서 오는 경로 작업 이름과 같은 경우 `/apps/ws/js/runtime/templates/task.html`에서 다음 코드를 수정하십시오.

   ```jsp
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

1. CSS 스타일의 이름이 서버에서 오는 경로 작업 이름과 다른 경우 `/apps/ws/js/runtime/templates/task.html`에서 다음 코드를 수정하십시오. 그러면 `if-else` 서블릿 조건 스택을 추가하여 스타일을 경로 작업 이름과 매핑합니다.

```jsp
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

1. `/libs/ws/js/runtime/templates/taskdetails.html`을(를) `/apps/ws/js/runtime/templates/taskdetails.html`에 복사합니다.

1. CSS 스타일의 이름이 서버에서 오는 경로 작업 이름과 같은 경우 `/apps/ws/js/runtime/templates/taskdetails.html`에서 다음 코드를 수정하십시오.

   ```jsp
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

1. CSS 스타일의 이름이 서버에서 오는 경로 작업 이름과 다른 경우 `/apps/ws/js/runtime/templates/taskdetails.html`에서 다음 코드를 수정하십시오. 루트 작업 이름에 스타일을 매핑하기 위해 `if-else` 서블릿 조건 스택을 추가합니다.

   ```jsp
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

1. 편집할 `/apps/ws/js/registry.js`을(를) 열고 다음 텍스트를 찾습니다.
   `"text!/lc/libs/ws/js/runtime/templates/taskdetails.html"`

1. 텍스트를 다음으로 바꿉니다.
   `"text!/lc/apps/ws/js/runtime/templates/taskdetails.html"`
