---
title: 제스처 사용자 지정
seo-title: Gesture customization
description: AEM Forms 앱에서 제스처 사용자 지정
seo-description: Customize the gestures on your AEM Forms app
uuid: 117e0e21-66bd-42f1-879c-6c1443991974
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 747d13d3-e7cc-4aa1-bcc8-4b57157e71ed
exl-id: 6debb1a7-7889-4fdd-87c7-ecb87cc0b1f5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# 제스처 사용자 지정 {#gesture-customization}

AEM Forms 앱의 제스처를 사용자 지정하여 앱과 상호 작용하는 별개의 방법을 제공할 수 있습니다. 예를 들어 새 제스처를 추가하여 작업이나 시작점을 열거나 닫을 수 있습니다.

## AEM Forms 앱에서 제스처를 사용자 지정하려면 {#to-customize-gestures-in-aem-forms-app}

AEM Forms 앱에서 왼쪽 살짝 밀면 새 작업이나 시작점이 열리고 오른쪽 밀기는 아무 작업도 하지 않습니다. 다음 예제에서는 AEM Forms 앱에서 마우스 오른쪽 단추 밀기 동작을 수행할 때 새 작업 또는 시작점을 여는 단계를 제공합니다.

1. 프로젝트를 엽니다.

   * iOS의 경우 `Capture.xcodeproj` in Xcode
   * Android의 경우 Eclipse에서 Android 프로젝트를 엽니다.
   * Windows의 경우 `MWSWindows.sln` 입니다.

1. 보기 폴더로 이동하고 `task.js` 편집할 파일입니다.

   * Xcode에서 **캡처 > www > mobile > js > runtime > 보기** 폴더를 입력합니다.
   * Eclipse에서 **assets > www > mobile > js > runtime > 보기** 폴더를 입력합니다.
   * Visual Studio에서 **MWSWindows > www > webmobile > js > runtime > views** 폴더를 입력합니다.

   >[!NOTE]
   >
   >task.js 파일에는 작업 또는 시작점 목록에 나열된 각 작업 또는 시작점과 연관된 백본 보기가 포함됩니다.

1. 에서 `task.js` 파일에서 뷰의 events 속성을 검색합니다.

   events 속성은 각 항목이 형식으로 표시된 맵입니다.

   `"EventName Selector": "Function"`

   라는 Javascript 이벤트를 트리거할 때 `EventName`에 의해 지정된 HTML 요소에서 `Selector`, `Function`가 호출됩니다.

1. 찾기

   * &quot;tap .taskContentArea&quot; : &quot;onTaskClick&quot;,

      &quot;tap .taskOpenArea&quot; : &quot;onTaskClick&quot;,

      &quot;tap .task-content&quot; : &quot;onTaskClick&quot;,

      &quot;tap .last_empty_div&quot; : &quot;onTaskClick&quot;,
   다음으로 바꾸기

   * &quot;swipe.taskContentArea&quot; : &quot;onTaskClick&quot;,

      &quot;swipe.taskOpenArea&quot; : &quot;onTaskClick&quot;,

      &quot;swipe.task-content&quot; : &quot;onTaskClick&quot;,

      &quot;swipe.last_empty_div&quot; : &quot;onTaskClick&quot;,


1. 저장 후 닫기 `task.js` 파일.
1. AEM Forms 앱을 빌드하고 실행합니다. 이제 왼쪽으로 밀거나 오른쪽으로 밀면 을(를) 열 수 있습니다.

마찬가지로, 다양한 제스처, HTML 요소 및 함수 조합을 위한 다른 보기를 변경할 수 있습니다.
