---
title: 인터페이스의 글꼴 변경
description: 사용자 인터페이스의 글꼴을 선택적으로 변경하는 방법
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 226f70f0-8eb4-4724-b496-5801dc6b436f
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 1%

---

# 인터페이스의 글꼴 변경{#changing-the-font-on-the-interface}

AEM Forms 작업 영역에 표시되는 글꼴을 변경할 수 있습니다. 사용자 인터페이스의 특정 섹션에서 사용되는 글꼴은 스타일시트의 해당 섹션에서 정의됩니다. 사용자 인터페이스의 글꼴을 선택적으로 변경할 수 있습니다.

[AEM Forms 작업 영역 사용자 지정에 대한 일반 단계](../../forms/using/generic-steps-html-workspace-customization.md)를 따르고 요구 사항에 따라 CSS, HTML 또는 둘 다를 사용자 지정하는 단계를 따릅니다.

1. 기존 스타일로 글꼴-패밀리를 변경하거나 추가합니다.
1. HTML 요소에 대한 font-family 인라인을 변경하거나 추가합니다.
1. 스타일을 추가하고 HTML 요소에 사용합니다.

예를 들어 위쪽 탐색 막대 앵커 텍스트의 글꼴을 Courier New로 변경하려면 다음 단계를 수행합니다.

1. `https://'[server]:[port]'/lc/crx/de/index.jsp`에 액세스하여 CRXDE Lite에 로그인합니다.
1. 다음 중 하나를 수행하십시오.

   1. 기존 스타일의 font-family를 변경하려면 /apps/ws/css의 newStyle.css 파일에 다음을 추가하십시오.

      ```css
      #topnav a {
         font-family: "Courier New";
      }
      ```

   1. HTML 요소에 대해 font-family 인라인을 추가하려면 `/libs/ws/js/runtime/templates/appnavigation.html` 파일을 `/apps/ws/js/runtime/templates/appnavigation.html`에 복사합니다.

      /apps/ws/js/runtime/templates/appnavigation.html 파일을 다음과 같이 업데이트합니다.

      ```jsp
      <li class="process"><a href="#" title="<%= $.t('index.header.topnav.startprocess.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.startprocess.name')%></a></li>
      <li class="todo"><a href="#/todo" title="<%= $.t('index.header.topnav.todo.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.todo.name')%></a></li>
      <li class="track"><a href="#/tracking" title="<%= $.t('index.header.topnav.tracking.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.tracking.name')%></a></li>
      <li class="preference"><a href="#/preferences" title="<%= $.t('index.header.topnav.preferences.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.preferences.name')%></a></li>
      ```

      편집할 /apps/ws/js/registry.js 파일을 열고 `text!/lc/libs/ws/js/runtime/templates/appnavigation.html`을(를) `text!/lc/apps/ws/js/runtime/templates/appnavigation.html`(으)로 바꿉니다.

   1. font-family를 정의하는 스타일을 추가하려면 /apps/ws/css의 newStyle.css 파일에 다음을 추가하십시오.

      ```css
      .myNewFontStyle a {
         font-family: "Courier New";
      }
      ```

      HTML 요소에 대해 font-family 인라인을 추가하려면 /apps/ws/js/runtime/templates의 appnavigation.html 파일에 다음을 추가하십시오.

      ```jsp
      <div id="topnav" class="myNewFontStyle">
          <ul>
              <li class="process"><a href="#" title="<%= $.t('index.header.topnav.startprocess.detail')%>" ><%= $.t('index.header.topnav.startprocess.name')%></a></li>
              <li class="todo"><a href="#/todo" title="<%= $.t('index.header.topnav.todo.detail')%>"><%= $.t('index.header.topnav.todo.name')%></a></li>
              <li class="track"><a href="#/tracking" title="<%= $.t('index.header.topnav.tracking.detail')%>" ><%= $.t('index.header.topnav.tracking.name')%></a></li>
              <li class="preference"><a href="#/preferences" title="<%= $.t('index.header.topnav.preferences.detail')%>" ><%= $.t('index.header.topnav.preferences.name')%></a></li>
          </ul>
      </div>
      ```

1. 작업 영역을 다시 시작하고 브라우저 캐시에서 변경 사항을 지웁니다.

![change_font_before](assets/change_font_before.png)

글꼴 사용자 지정 전 위쪽 탐색 막대

![change_font_after](assets/change_font_after.png)

첫 번째 탭의 글꼴 사용자 지정 후 상단 탐색 막대
