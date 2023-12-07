---
title: HTML 5 양식 소개
description: HTML5 forms는 Adobe Experience Manager 6.0(AEM 6.0) 소프트웨어의 새로운 기능으로, XFA 양식 템플릿을 HTML5 형식으로 렌더링할 수 있습니다.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: Mobile Forms
exl-id: 0facca18-ffa1-420c-859a-6f1f2c449d71
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# HTML 5 양식 소개{#introduction-to-html-forms}

HTML5 forms는 Adobe Experience Manager 6.0(AEM 6.0) 소프트웨어의 새로운 기능으로, XFA 양식 템플릿을 HTML5 형식으로 렌더링할 수 있습니다. 이 기능을 사용하면 XFA 기반 PDF이 지원되지 않는 모바일 장치 및 데스크탑 브라우저에서 양식을 렌더링할 수 있습니다. HTML5 양식은 XFA 양식 템플릿의 기존 기능을 지원할 뿐만 아니라 모바일 장치에 대한 스크리블 서명과 같은 새로운 기능을 추가합니다.

HTML5 forms는 표준 HTML5 구문을 기반으로 문서를 생성합니다. HTML5를 지원하는 모든 최신 브라우저에서 HTML5 양식을 볼 수 있습니다. 브라우저에 대한 추가 브라우저 플러그인을 설치할 필요가 없습니다. 지원되는 브라우저에 대한 자세한 내용은 [지원되는 클라이언트 플랫폼](https://adobe.com/go/learn_aemforms_supportedplatforms_63).

![HTML5 양식 미리 보기](do-not-localize/mobile_form_on_an_ipad_date_14.png)

## HTML 5 Forms의 주요 기능 {#key-capabilities-of-html-forms-br}

* 모든 호환 브라우저에서 지원되는 HTML5의 기존 XFA 양식을 렌더링합니다.
* 모바일 장치용 대상 양식에 표준 XFA 양식 디자인 기능을 활용합니다.
* HTML5 형식의 동적 XFA 기능을 사용합니다.
* 매우 정확한 SVG 텍스트 레이아웃(SVG 1.1)을 사용하여 PDF 텍스트 레이아웃과 일치합니다.
* JavaScript 및 FormCalc를 지원합니다.
* 데이터 기반 이벤트 또는 사용자 입력을 기반으로 조각을 대화형 양식으로 동적으로 어셈블합니다.
* 엔터프라이즈 표준에 따라 양식의 모양을 일치시키기 위해 사용자 지정 CSS를 지원합니다.
* 사용자 정의 위젯이 풍부한 데이터 캡처 경험을 제공할 수 있도록 합니다.
* 웹 앱과의 통합을 지원합니다.

### 멀티채널 게시 {#multichannel-publishing}

양식 개발자는 XFA 템플릿을 사용하여 양식을 PDF 및 HTML5 형식으로 렌더링할 수 있습니다. 이 기능은 HTML5 양식 디자인 사례에 맞게 최소한의 변경이 필요한 대규모 XFA 양식 세트가 있는 시나리오에서 유용합니다. XFA 기반 PDF이 아직 지원되지 않는 다양한 디바이스를 타깃팅하기 위해 기존 XFA 양식을 HTML5에 렌더링할 수 있습니다.

## HTML 5 양식 관리 {#manage-html-forms}

또한 AEM에서는 AEM Forms UI를 사용하여 모든 양식 템플릿을 나열하고 관리할 수 있는 통합 보기를 제공합니다. 양식을 활성화, 비활성화, 게시 및 미리 볼 수 있습니다. 자세한 내용은 [양식 관리 소개](../../forms/using/introduction-managing-forms.md).

### Forms 사용자 지정 {#forms-customization}

HTML5 forms는 표준 HTML5 구문을 사용하여 양식 템플릿을 렌더링합니다. 따라서 주로 CSS와 JavaScript와 같은 웹 기술을 사용하여 양식을 HTML5 형식으로 간편하게 사용자 지정하고 확장할 수 있습니다. 기존 위젯의 모양을 손쉽게 사용자 정의하거나, 사용자 정의 위젯을 직접 만들거나, 양식의 사용자 정의 스타일을 사용할 수 있습니다. 사용자 정의 위젯 만들기 및 기존 위젯 사용자 정의에 대한 자세한 내용은 [HTML5 양식으로 사용자 정의 위젯 연결](../../forms/using/custom-widgets.md).
