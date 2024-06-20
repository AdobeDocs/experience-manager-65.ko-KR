---
title: 제스처 사용자 지정
description: AEM Forms 앱에서 제스처를 사용자 지정하는 방법을 알아봅니다. 제스처를 사용자 정의하여 애플리케이션과 상호 작용하는 고유한 방법을 제공할 수 있습니다.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 6debb1a7-7889-4fdd-87c7-ecb87cc0b1f5
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# 제스처 사용자 지정 {#gesture-customization}

AEM Forms 앱의 제스처를 사용자 정의하여 앱과 상호 작용하는 고유한 방법을 제공할 수 있습니다. 예를 들어 작업 또는 시작 지점을 열거나 닫는 새 제스처를 추가할 수 있습니다.

## AEM Forms 앱에서 제스처를 사용자 지정하려면 {#to-customize-gestures-in-aem-forms-app}

AEM Forms 앱에서 왼쪽 스와이프는 새 작업 또는 시작 지점을 열고 오른쪽 스와이프는 아무 작업도 하지 않습니다. 다음 예제에서는 AEM Forms 앱에서 마우스 오른쪽 버튼으로 스와이프 동작을 수행할 때 새 작업 또는 시작 지점을 여는 단계를 제공합니다.

1. 프로젝트를 엽니다.

   * iOS의 경우 를 엽니다. `Capture.xcodeproj` Xcode에서
   * Android의 경우 Eclipse에서 Android 프로젝트를 엽니다.
   * Windows의 경우 열기 `MWSWindows.sln` Visual Studio에서.

1. 보기 폴더로 이동하고 `task.js` 편집할 파일입니다.

   * Xcode에서 **캡처 > www > wsmobile > js > 런타임 > 보기** 폴더를 삭제합니다.
   * Eclipse에서 **assets > www > wsmobile > js > runtime > 보기** 폴더를 삭제합니다.
   * Visual Studio에서 **MWSWindows > www > wsmobile > js > 런타임 > 보기** 폴더를 삭제합니다.

   >[!NOTE]
   >
   >task.js 파일에는 작업 또는 시작점 목록에 나열된 각 작업 또는 시작점과 연관된 백본 보기가 포함되어 있습니다.

1. 다음에서 `task.js` 파일의 보기에서 events 속성을 검색합니다.

   events 속성은 다음 형식의 각 항목이 있는 맵입니다.

   `"EventName Selector": "Function"`

   라는 JavaScript 이벤트를 트리거할 때 `EventName`에 지정된 HTML 요소에서 `Selector`, `Function`이(가) 호출되었습니다.

1. 찾기

   * &quot;select .taskContentArea&quot; : &quot;onTaskClick&quot;,

     &quot;select .taskOpenArea&quot; : &quot;onTaskClick&quot;,

     &quot;select .task-content&quot; : &quot;onTaskClick&quot;,

     &quot;select .last_empty_div&quot; : &quot;onTaskClick&quot;,

   및 다음으로 바꾸기

   * &quot;swipe .taskContentArea&quot; : &quot;onTaskClick&quot;,

     &quot;swipe .taskOpenArea&quot; : &quot;onTaskClick&quot;,

     &quot;swipe .task-content&quot; : &quot;onTaskClick&quot;,

     &quot;swipe .last_empty_div&quot; : &quot;onTaskClick&quot;,

1. 저장 후 닫기 `task.js` 파일.
1. AEM Forms 앱을 빌드하고 실행합니다. 이제 왼쪽 스와이프와 오른쪽 스와이프로 을(를) 열 수 있습니다.

마찬가지로 제스처, HTML 요소 및 함수의 다양한 조합에 대해 다른 보기를 변경할 수 있습니다.
