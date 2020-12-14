---
title: 테마 맞춤화
seo-title: 테마 맞춤화
description: AEM Forms 앱의 테마를 사용자 지정하는 방법
seo-description: AEM Forms 앱의 테마를 사용자 지정하는 방법
uuid: 36632e67-1cc6-416d-ae80-d84bbabab4bd
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: c72f608e-052a-4bf9-b7bc-ddf57483af35
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# 테마 사용자 지정 {#theme-customization}

HTML 코드 및 CSS 파일을 사용자 지정하여 AEM Forms 앱에 고유한 룩앤필을 제공할 수 있습니다. 예를 들어 작업의 배경색과 높이를 변경하거나 시작점을 변경할 수 있습니다. 다음 예제에서는 변경 지침을 제공합니다.

* 설명 대신 표시 지침
* 표시 경로 수
* 배경 그레이디언트 색상

## 단계 {#steps}

1. 프로젝트를 엽니다.

   * iOS의 경우 Xcode에서 `Capture.xcodeproj`을(를) 엽니다.
   * Android의 경우 Eclipse에서 Android 프로젝트를 엽니다.
   * Windows의 경우 Visual Studio에서 `MWSWindows.sln`을 엽니다.

1. 템플릿 폴더로 이동합니다.

   * Xcode에서 **캡처 > www > 모바일 > js > 런타임 > templates** 폴더로 이동합니다.
   * Eclipse에서 **자산 > www > 모바일 > js > 런타임 > templates** 폴더로 이동합니다.
   * Visual Studio에서 **MWSWindows > www > Mobile > js > 런타임 > templates** 폴더로 이동합니다.

1. 편집할 `template.html` 파일을 엽니다.
1. 다음 문자열을 찾습니다.

   ```jsp
   <%if ( (task.description !== "") && (task.description !== null) && (typeof task.description !== null) && (typeof task.description !== 'undefined') ) {%>
                  <div class="description_details">
                    <%= task.description %>
                  </div>
                 <%} else
   ```

   `<%`으로 대체합니다.

1. `template.html` 파일에서 다음 코드를 찾습니다.

   ```jsp
   <ul id="task_menu_list">
                                   <li class="approve" title="<%= task.availableCommands.directCommands[0]%>" data-routename="<%= task.availableCommands.directCommands[0]%>">
                                       <%= task.availableCommands.directCommands[0]%>
                                   </li>
                                   <li class="reject last" title="<%= task.availableCommands.directCommands[1]%>" data-routename="<%= task.availableCommands.directCommands[1]%>">
                                       <%= task.availableCommands.directCommands[1]%>
                                   </li>
   ```

1. 다음 줄의 주석을 달고 파일을 저장합니다.

   ```jsp
   task.availableCommands.directCommands[1]%>">
   <%= task.availableCommands.directCommands[1]%>
   </li>
   ```

1. css 폴더로 이동합니다.

   * Xcode에서 **캡처 > www > 동영상 > css**&#x200B;로 이동합니다.
   * Eclipse에서 **자산 > www > 모바일 > css**&#x200B;로 이동합니다.
   * Visual Studio에서 **MWSWindows > www > Mobile > css**&#x200B;로 이동합니다.

1. 편집할 `_style.css` 파일을 엽니다.
1. 배경 이미지의 경우 `#323232`을 `#fff`(으)로 변경합니다.
1. 변경 내용을 저장하고 `_style.css` 파일을 닫습니다.
1. AEM Forms 앱을 엽니다.

   이제 AEM Forms 앱에 설명 대신 지침이 표시됩니다.
