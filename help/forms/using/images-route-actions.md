---
title: 경로 작업에 사용된 이미지 사용자 지정
seo-title: Customize images used in route actions
description: AEM Forms 작업 영역 LiveCycle에서 경로 작업에 사용되는 이미지를 사용자 지정하는 방법.
seo-description: How-to customize the images used in route actions in LiveCycle AEM Forms workspace.
uuid: 42608376-587e-4b57-a9d5-8f9ebd981426
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 10158c13-47b4-43e3-ac47-690f3cbab158
exl-id: 687c6569-7189-4039-9c7a-bc29658a7756
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# 경로 작업에 사용된 이미지 사용자 지정 {#customize-images-used-in-route-actions}

경로 작업에 사용되는 이미지를 사용자 정의하려면 다음에 설명된 단계를 수행합니다 [사용자 지정의 일반 단계](/help/forms/using/generic-steps-html-workspace-customization.md) 이 문서에 설명된 단계를 따릅니다.

## 경로 작업에 대한 이미지 {#images-for-route-actions}

1. CSS의 이미지를 정의하는 스타일을 새 경로 작업의 다음 위치에 추가합니다.

   `/apps/ws/css/newStyle.css`

   예: 라는 새 스타일 추가 `myStyle1`아래 그림과 같이 이미지 파일을 업로드합니다 `myStyleIcon1.png` (으)로 `/apps/ws/image`WebDAV 클라이언트를 사용하는 폴더입니다.

   >[!NOTE]
   >
   >WebDAV 액세스에 대한 자세한 내용은 [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html).

   >[!NOTE]
   >
   >스타일 이름을 경로 작업 이름과 동일하게 사용하십시오.

   ```css
   .myStyle1{
   
           background-image: url('../images/myStyleIcon1.png');
   
       }
   ```

## 작업 목록 작업 작업 팝업 {#task-list-task-action-popup}

1. 작업 목록 작업 팝업을 만듭니다. 다음을 참조하십시오. [AEM Forms 작업 공간 코드 작성](introduction-customizing-html-workspace.md#building-html-workspace-code). 개발 패키지를 사용해야 합니다.

1. 복사 `/libs/ws/js/runtime/templates/task.html` 끝 `/apps/ws/js/runtime/templates/task.html`.

1. CSS 스타일의 이름이 서버에서 들어오는 경로 작업 이름과 같으면 다음 코드를에서 수정합니다 `/apps/ws/js/runtime/templates/task.html`:

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

1. CSS 스타일의 이름이 서버에서 들어오는 경로 작업 이름과 다른 경우 `/apps/ws/js/runtime/templates/task.html`. 이 옵션은 `if-else` 스타일을 경로 작업 이름과 매핑하는 서블릿 조건

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

## 작업 세부 사항 작업 작업 팝업 {#task-details-task-action-popup}

1. 복사 `/libs/ws/js/runtime/templates/taskdetails.html` 끝 `/apps/ws/js/runtime/templates/taskdetails.html`.

1. CSS 스타일의 이름이 서버에서 들어오는 경로 작업 이름과 같으면 다음 코드를에서 수정합니다 `/apps/ws/js/runtime/templates/taskdetails.html`:

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

1. CSS 스타일의 이름이 서버에서 들어오는 경로 작업 이름과 다른 경우 `/apps/ws/js/runtime/templates/taskdetails.html`. 다음을 추가합니다. `if-else` 스타일을 경로 작업 이름과 매핑하는 서블릿 조건

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

1. 열기 `/apps/ws/js/registry.js` 를 편집하고 다음 텍스트를 찾습니다.
   `"text!/lc/libs/ws/js/runtime/templates/taskdetails.html"`

1. 텍스트를 다음과 같이 바꿉니다.
   `"text!/lc/apps/ws/js/runtime/templates/taskdetails.html"`
