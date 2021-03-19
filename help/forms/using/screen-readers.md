---
title: HTML5 양식의 화면 판독기
seo-title: HTML5 양식의 화면 판독기
description: HTML5 양식에 지원되는 화면 판독기를 나열합니다.
seo-description: HTML5 양식에 지원되는 화면 판독기를 나열합니다.
uuid: 035354e2-957f-4eb6-bc16-4ca96ec7ac74
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 53c57180-7004-4534-9146-603f7770a6fe
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 1%

---


# HTML5 양식 {#screen-readers-for-html-forms} 화면 판독기

HTML5 양식 구성 요소는 XFA 양식 템플릿을 HTML5 형식으로 렌더링합니다. HTML5를 지원하는 모든 표준 브라우저는 이러한 양식을 렌더링할 수 있습니다. PDF 및 HTML5 양식에 있는 유사한 데이터 캡처 환경을 지원하기 위해 PDF forms 레이아웃은 HTML5 양식에 그대로 유지됩니다.

HTML5 양식은 표준 HTML 구문을 사용하여 HTML을 이러한 양식에 사용할 수 있도록 합니다. 액세스 가능한 양식에 대한 모범 사례에 따라 양식을 설계하면 지원되는 모든 화면 판독기에서 작동합니다. 또한 이러한 양식은 키보드 탐색을 위해 활성화됩니다.

## 접근성 표준 {#accessibility-standards}

HTML5 양식은 알려진 예외에 대한 접근성을 위해 조항 508을 준수합니다. 자세한 내용은 [VPAT for HTML5 양식](https://www.adobe.com/mena_en/accessibility/compliance/livecycle-mobile-forms-es4-section-508-vpat.html)을 참조하십시오.

## HTML5 양식에 대한 인증된 화면 판독기 {#certified-screen-readers-for-html-forms}

* Microsoft Windows 기반의 JAWS 14.0
* Mac OS X 및 iPad의 VoiceOver

### JAWS {#jaws}

모든 기본 키 입력과 단축키는 HTML5 양식에 대해 작동합니다. JAWS 사용에 대한 자세한 내용은 [https://www.freedomscientific.com/jaws-hq.asp](https://www.freedomscientific.com/jaws-hq.asp)을 참조하십시오.

### VoiceOver {#voiceover}

HTML5 양식은 음성의 모든 기본 키 입력과 제스처를 지원합니다. VoiceOver 설정 및 사용에 대한 자세한 내용은 [https://www.apple.com/accessibility/voiceover/](https://www.apple.com/accessibility/voiceover/)을 참조하십시오.

## 알려진 문제 {#known-issues}

* **(내부 탐색기 9에만 해당)** HTML5 양식에서는 페이지가 필요할 때 로드됩니다(동적으로). 주문형 페이지 로드로 인해 화면 판독기 기능 문제가 발생합니다. 화면 판독기의 포커스가 페이지의 마지막 필드에 있고 사용자가 탭을 누르면 화면 판독기가 다음 페이지의 첫 번째 필드에 포커스를 설정하는 대신 화면의 첫 번째 페이지에 포커스를 반환합니다.
* **(내부 탐색기 9에만 해당)** HTML5 양식의 날짜 선택기 컨트롤은 키보드에서 완전히 액세스할 수 없습니다. 날짜 선택기 컨트롤에서 위쪽/아래쪽 키를 여러 번 누르면 날짜 선택기 컨트롤이 닫히고 포커스가 다음/마지막 필드로 이동합니다.

* VoiceOver가 iPad Safari의 날짜 위젯에서 화살표 키를 감지할 수 없습니다.
