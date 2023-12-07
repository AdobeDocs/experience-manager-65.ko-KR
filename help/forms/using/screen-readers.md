---
title: HTML 5 양식용 화면 판독기
description: HTML5 양식에서 지원되는 화면 판독기를 나열합니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
feature: Mobile Forms
exl-id: 07d20c2f-7d13-48ac-8d58-b367eb194558
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# HTML 5 양식용 화면 판독기 {#screen-readers-for-html-forms}

HTML5 양식 구성 요소는 XFA 양식 템플릿을 HTML5 형식으로 렌더링합니다. HTML5를 지원하는 모든 표준 브라우저는 이러한 양식을 렌더링할 수 있습니다. PDF 및 HTML 5 양식에서 유사한 데이터 캡처 환경을 지원하기 위해 PDF forms의 레이아웃은 HTML 5 양식으로 유지됩니다.

HTML5 양식은 표준 HTML 구문을 사용하여 HTML에 대한 일반 접근성 도구를 이러한 양식과 함께 사용할 수 있습니다. 액세스 가능한 양식에 대한 모범 사례에 따라 양식이 디자인된 경우 지원되는 모든 화면 판독기에서 작동합니다. 또한 이러한 양식은 키보드 탐색에 사용할 수 있습니다.

## 접근성 표준 {#accessibility-standards}

HTML5 양식은 알려진 예외를 제외하고 접근성을 위한 섹션 508을 준수합니다. 다음을 참조하십시오 [HTML5 양식용 VPAT](https://www.adobe.com/content/dam/cc1/en/accessibility/compliance/pdfs/adobe-livecycle-es4-section-508-vpat-portfolio.pdf) 을 참조하십시오.

## HTML5 양식용 인증된 화면 판독기 {#certified-screen-readers-for-html-forms}

* Microsoft® Windows의 JAWS 14.0
* macOS X 및 iPad의 VoiceOver

### JAWS {#jaws}

모든 기본 키 입력과 바로 가기는 HTML 5 양식에 대해 작동합니다. JAWS 사용에 대한 자세한 내용은 다음을 참조하십시오. [https://www.freedomscientific.com/jaws-hq.asp](https://www.freedomscientific.com/jaws-hq.asp).

### 보이스오버 {#voiceover}

HTML5 forms는 Voice over의 모든 기본 키 입력과 제스처를 지원합니다. VoiceOver 설정 및 사용에 대한 자세한 내용은 [https://www.apple.com/accessibility/vision/](https://www.apple.com/accessibility/vision/).

## 알려진 문제 {#known-issues}

* **(Internal Explorer 9만 해당)** HTML 5 양식에서 페이지는 요청에 따라(동적으로) 로드됩니다. 온디맨드 페이지 로드로 인해 화면 판독기 기능에 문제가 발생합니다. 화면 판독기의 포커스가 페이지의 마지막 필드에 있고 사용자가 탭을 누르면 화면 판독기는 양식에 있는 첫 번째 페이지의 첫 번째 필드에 포커스를 반환합니다.
* **(Internal Explorer 9만 해당)** 키보드를 사용하여 HTML5 양식의 날짜 선택기 컨트롤에 완전히 액세스할 수 없습니다. Date Picker 컨트롤에서 Up/Down 키를 여러 번 누르면 Date Picker 컨트롤이 닫히고 포커스가 다음/마지막 필드로 이동합니다.

* VoiceOver가 iPad safari에서 날짜 위젯에 대한 화살표 키를 감지할 수 없습니다.
