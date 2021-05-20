---
title: HTML5 양식에 대한 화면 판독기
seo-title: HTML5 양식에 대한 화면 판독기
description: HTML5 양식에서 지원되는 화면 판독기를 나열합니다.
seo-description: HTML5 양식에서 지원되는 화면 판독기를 나열합니다.
uuid: 035354e2-957f-4eb6-bc16-4ca96ec7ac74
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 53c57180-7004-4534-9146-603f7770a6fe
feature: Mobile Forms
exl-id: 07d20c2f-7d13-48ac-8d58-b367eb194558
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 1%

---

# HTML5 양식에 대한 화면 판독기 {#screen-readers-for-html-forms}

HTML5 양식 구성 요소는 XFA 양식 템플릿을 HTML5 형식으로 렌더링합니다. HTML5를 지원하는 모든 표준 브라우저는 이러한 양식을 렌더링할 수 있습니다. PDF 및 HTML5 양식에서 유사한 데이터 캡처 경험을 지원하기 위해 PDF forms 레이아웃은 HTML5 양식으로 유지됩니다.

HTML5 양식은 이러한 양식에서 HTML에 대한 일반적인 액세서빌러티 도구를 사용할 수 있도록 하는 표준 HTML 구문을 사용합니다. 액세스 가능한 양식에 대한 우수 사례에 따라 양식을 디자인하면 지원되는 모든 화면 판독기에서 작동합니다. 또한 이러한 양식은 키보드 탐색을 위해 활성화됩니다.

## 액세스 가능성 표준 {#accessibility-standards}

HTML5 양식은 알려진 예외 사항에 대한 액세스 가능성을 위해 섹션 508을 준수합니다. 자세한 내용은 [HTML5 양식의 VPAT](https://www.adobe.com/mena_en/accessibility/compliance/livecycle-mobile-forms-es4-section-508-vpat.html)를 참조하십시오.

## HTML5 양식에 대해 인증된 화면 판독기 {#certified-screen-readers-for-html-forms}

* Microsoft Windows의 JAWS 14.0
* Mac OS X 및 iPad의 VoiceOver

### 죠스 {#jaws}

모든 기본 키 입력과 단축키는 HTML5 양식에 대해 작동합니다. JAWS 사용에 대한 자세한 내용은 [https://www.freedomscientific.com/jaws-hq.asp](https://www.freedomscientific.com/jaws-hq.asp)을 참조하십시오.

### VoiceOver {#voiceover}

HTML5 양식은 음성의 모든 기본 키 입력과 제스처를 지원합니다. VoiceOver 설정 및 사용에 대한 자세한 내용은 [https://www.apple.com/accessibility/voiceover/](https://www.apple.com/accessibility/voiceover/)을 참조하십시오.

## 알려진 문제 {#known-issues}

* **(내부 Explorer 9만 해당)**  HTML5 양식에서 페이지가 필요할 때(동적으로) 로드됩니다. 온디맨드 페이지 로드로 인해 화면 판독기가 작동하는 문제가 발생합니다. 화면 판독기의 포커스가 페이지의 마지막 필드에 있고 사용자가 탭을 누르는 경우, 다음 페이지의 첫 번째 필드에 포커스를 설정하는 대신 화면 판독기는 양식의 첫 번째 페이지의 첫 번째 필드에 포커스를 반환합니다.
* **(내부 탐색기 9만 해당)**  HTML5 양식의 날짜 선택기 컨트롤은 키보드를 사용하여 완전히 액세스할 수 없습니다. Date Picker 컨트롤에서 Up/Down 키를 여러 번 누르면 Date Picker 컨트롤이 닫히고 포커스가 다음/마지막 필드로 이동합니다.

* VoiceOver에서 iPad safari의 날짜 위젯에서 화살표 키를 감지할 수 없습니다.
