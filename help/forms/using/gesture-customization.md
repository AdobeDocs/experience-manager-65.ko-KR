---
title: 제스처 사용자 정의
seo-title: 제스처 사용자 정의
description: AEM Forms 앱에서 제스처 사용자 정의
seo-description: AEM Forms 앱에서 제스처 사용자 정의
uuid: 117e0e21-66bd-42f1-879c-6c1443991974
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 747d13d3-e7cc-4aa1-bcc8-4b57157e71ed
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 제스처 사용자 정의 {#gesture-customization}

AEM Forms 앱의 제스처를 사용자 지정하여 앱과 상호 작용하는 별개의 방법을 제공할 수 있습니다. 예를 들어 새 제스처를 추가하여 작업 또는 시작점을 열거나 닫을 수 있습니다.

## AEM Forms 앱에서 제스처를 사용자 정의하려면 {#to-customize-gestures-in-aem-forms-app}

AEM Forms 앱에서 왼쪽 스와이프는 새 작업 또는 시작점을 열고 오른쪽 스와이프는 아무 작업도 수행하지 않습니다. 다음 예제에서는 AEM Forms 앱에서 마우스 오른쪽 단추 스와이프 제스처를 수행하는 새 작업 또는 시작점을 여는 단계를 제공합니다.

1. 프로젝트를 엽니다.

   * iOS의 경우 Xcode `Capture.xcodeproj` 에서 열기
   * Android의 경우 Eclipse에서 Android 프로젝트를 엽니다.
   * Windows의 경우 Visual Studio `MWSWindows.sln` 에서 엽니다.

1. 보기 폴더로 이동하여 편집할 `task.js` 파일을 엽니다.

   * Xcode에서 Capture > **www > Mobile > js > 런타임 > 보기** 폴더로 이동합니다.
   * Eclipse에서 **자산 > www > 모바일 > js > 런타임 > 보기** 폴더로 이동합니다.
   * Visual Studio에서 MWSWindows > **www > mobile > js > 런타임 > 보기** 폴더로 이동합니다.
   >[!NOTE]
   >
   >task.js 파일에는 각 작업이나 Startpoint 목록에 나열된 Startpoint와 연관된 백본 보기가 포함되어 있습니다.

1. 파일에서 뷰의 events 속성을 `task.js` 검색합니다.

   events 속성은 각 항목이 형식으로 표시된 맵입니다.

   `"EventName Selector": "Function"`

   에 의해 지정된 HTML `EventName`요소에 대해 이름이 지정된 Javascript 이벤트를 트리거하면 `Selector`이 `Function`호출됩니다.

1. 찾기

   * &quot;tap .taskContentArea&quot; :&quot;onTaskClick&quot;,

      &quot;tap .taskOpenArea&quot; :&quot;onTaskClick&quot;,

      &quot;tap .task-content&quot; :&quot;onTaskClick&quot;,

      &quot;tap .last_empty_div&quot; :&quot;onTaskClick&quot;,
   다음으로 바꾸기

   * &quot;swipe .taskContentArea&quot; :&quot;onTaskClick&quot;,

      &quot;swipe .taskOpenArea&quot; :&quot;onTaskClick&quot;,

      &quot;swipe .task-content&quot; :&quot;onTaskClick&quot;,

      &quot;swipe .last_empty_div&quot; :&quot;onTaskClick&quot;,


1. 파일을 저장하고 `task.js` 닫습니다.
1. AEM Forms 앱을 빌드하고 실행합니다. 이제 마우스 왼쪽 버튼을 누르고 마우스 오른쪽 버튼으로 스와이프하면 Adobe Sign을 열 수 있습니다.

마찬가지로 제스처, HTML 요소 및 함수의 다양한 조합에 대해 다른 보기를 변경할 수 있습니다.
