---
title: 제스처 사용자 정의
description: AEM Forms 앱에서 제스처를 사용자 지정하는 방법을 알아봅니다. 제스처를 사용자 정의하여 애플리케이션과 상호 작용하는 고유한 방법을 제공할 수 있습니다.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 6debb1a7-7889-4fdd-87c7-ecb87cc0b1f5
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 4d0fdb4b3128272d50252b52e5eda1b78cd7cae9
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 1%

---

# 제스처 사용자 정의 {#gesture-customization}

>[!NOTE]
>
>AEM Forms 앱은 현재 더 이상 사용되지 않습니다. 질문이 있거나 도움이 필요하면 [aemformsapp-android@adobe.com](mailto:aemformsapp-android@adobe.com)에 문의하십시오.

AEM Forms 앱의 제스처를 사용자 정의하여 앱과 상호 작용하는 고유한 방법을 제공할 수 있습니다. 예를 들어 작업 또는 시작 지점을 열거나 닫는 새 제스처를 추가할 수 있습니다.

## AEM Forms 앱에서 제스처를 사용자 지정하려면 {#to-customize-gestures-in-aem-forms-app}

AEM Forms 앱에서 왼쪽 스와이프는 새 작업 또는 시작 지점을 열고 오른쪽 스와이프는 아무 작업도 하지 않습니다. 다음 예제에서는 AEM Forms 앱에서 마우스 오른쪽 버튼으로 스와이프 동작을 수행할 때 새 작업 또는 시작 지점을 여는 단계를 제공합니다.

1. 프로젝트를 엽니다.

   * iOS의 경우 Xcode에서 `Capture.xcodeproj` 열기
   * Android의 경우 Eclipse에서 Android 프로젝트를 엽니다.
   * Windows의 경우 Visual Studio에서 `MWSWindows.sln`을(를) 엽니다.

1. 보기 폴더로 이동하여 편집할 `task.js` 파일을 엽니다.

   * Xcode에서 **캡처 > www > wsmobile > js > 런타임 > 보기** 폴더로 이동합니다.
   * Eclipse에서 **자산 > www > wsmobile > js > 런타임 > 보기** 폴더로 이동합니다.
   * Visual Studio에서 **MWSWindows > www > wsmobile > js > runtime > views** 폴더로 이동합니다.

   >[!NOTE]
   >
   >task.js 파일에는 작업 또는 시작점 목록에 나열된 각 작업 또는 시작점과 연관된 백본 보기가 포함되어 있습니다.

1. `task.js` 파일에서 보기의 이벤트 속성을 검색합니다.

   events 속성은 다음 형식의 각 항목이 있는 맵입니다.

   `"EventName Selector": "Function"`

   `Selector`에서 지정한 HTML 요소에서 이름이 `EventName`인 JavaScript 이벤트를 트리거하면 `Function`이(가) 호출됩니다.

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

1. `task.js` 파일을 저장하고 닫습니다.
1. AEM Forms 앱을 빌드하고 실행합니다. 이제 왼쪽 스와이프와 오른쪽 스와이프로 을(를) 열 수 있습니다.

마찬가지로 다른 보기에서 다양한 제스처, HTML 요소 및 함수 조합을 변경할 수 있습니다.
