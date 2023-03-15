---
title: 테마 맞춤화
seo-title: Theme Customization
description: AEM Forms 앱의 테마를 맞춤화하는 방법
seo-description: How to customize the theme of your AEM Forms app.
uuid: 36632e67-1cc6-416d-ae80-d84bbabab4bd
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: c72f608e-052a-4bf9-b7bc-ddf57483af35
exl-id: 9b8c5933-b783-48f9-b463-15a01e06ee98
source-git-commit: 6bc228866aca785ec768daefb73970fc24568ef0
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# 테마 맞춤화 {#theme-customization}

HTML 코드 및 CSS 파일을 사용자 정의하여 AEM Forms 앱에 고유한 조직별 모양과 느낌을 제공할 수 있습니다. 예를 들어 작업 또는 시작점의 배경색 및 높이를 변경할 수 있습니다. 다음 예에서는 변경 지침을 제공합니다.

* 설명 대신 지침 표시
* 표시 경로 수
* 배경 그라데이션 색상

## 단계 {#steps}

1. 프로젝트를 엽니다.

   * iOS의 경우 를 엽니다. `Capture.xcodeproj` Xcode에서
   * Android의 경우 Eclipse에서 Android 프로젝트를 엽니다.
   * Windows의 경우 열기 `MWSWindows.sln` Visual Studio에서.

1. 템플릿 폴더로 이동합니다.

   * Xcode에서 **캡처 > www > wsmobile > js > 런타임 > 템플릿** 폴더를 삭제합니다.
   * Eclipse에서 **assets > www > wsmobile > js > 런타임 > 템플릿** 폴더를 삭제합니다.
   * Visual Studio에서 **MWSWindows > www > wsmobile > js > 런타임 > 템플릿** 폴더를 삭제합니다.

1. 를 엽니다. `template.html` 편집할 파일입니다.
1. 다음 문자열을 찾습니다.

   ```jsp
   <%if ( (task.description !== "") && (task.description !== null) && (typeof task.description !== null) && (typeof task.description !== 'undefined') ) {%>
                  <div class="description_details">
                    <%= task.description %>
                  </div>
                 <%} else
   ```

   다음으로 바꾸기 `<%`.

1. 에서 다음 코드를 찾습니다. `template.html` 파일:

   ```jsp
   <ul id="task_menu_list">
                                   <li class="approve" title="<%= task.availableCommands.directCommands[0]%>" data-routename="<%= task.availableCommands.directCommands[0]%>">
                                       <%= task.availableCommands.directCommands[0]%>
                                   </li>
                                   <li class="reject last" title="<%= task.availableCommands.directCommands[1]%>" data-routename="<%= task.availableCommands.directCommands[1]%>">
                                       <%= task.availableCommands.directCommands[1]%>
                                   </li>
   ```

1. 다음 줄을 주석 처리하고 파일을 저장합니다.

   ```jsp
   task.availableCommands.directCommands[1]%>">
   <%= task.availableCommands.directCommands[1]%>
   </li>
   ```

1. css 폴더로 이동합니다.

   * Xcode에서 다음으로 이동합니다. **Capture > www > wsmobile > css**.
   * Eclipse에서 다음으로 이동 **assets > www > wsmobile > css**.
   * Visual Studio에서 다음으로 이동합니다. **MWSWindows > www > wsmobile > css**.

1. 를 엽니다. `_style.css` 편집할 파일입니다.
1. 배경 이미지의 경우 변경 `#323232` 끝 `#fff`.
1. 변경 내용을 저장하고 닫기 `_style.css` 파일.
1. AEM Forms 앱을 엽니다.

   이제 AEM Forms 앱에 설명 대신 지침이 표시됩니다.
