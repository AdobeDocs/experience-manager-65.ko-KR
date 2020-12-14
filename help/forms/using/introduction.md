---
title: HTML5 양식 소개
seo-title: HTML5 양식 소개
description: HTML5 양식은 HTML5 형식으로 XFA 양식 템플릿을 렌더링하는 Adobe Experience Manager 6.0(AEM 6.0) 소프트웨어의 새로운 기능입니다.
seo-description: HTML5 양식은 HTML5 형식으로 XFA 양식 템플릿을 렌더링하는 Adobe Experience Manager 6.0(AEM 6.0) 소프트웨어의 새로운 기능입니다.
uuid: 63a2f000-c4c5-40e8-ab3f-c7c44c79ec09
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 672ee050-63d1-46ed-bef2-f55800208d78
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---


# HTML5 양식 소개{#introduction-to-html-forms}

HTML5 양식은 HTML5 형식으로 XFA 양식 템플릿을 렌더링하는 Adobe Experience Manager 6.0(AEM 6.0) 소프트웨어의 새로운 기능입니다. 이 기능을 사용하면 XFA 기반 PDF가 지원되지 않는 모바일 장치 및 데스크탑 브라우저에서 양식을 렌더링할 수 있습니다. HTML5 양식은 XFA 양식 템플릿의 기존 기능을 지원할 뿐만 아니라 모바일 장치에 대한 스크리블 서명과 같은 새로운 기능을 추가합니다.

HTML5 양식은 표준 HTML5 구문을 기반으로 문서를 생성합니다. HTML5를 지원하는 최신 브라우저에서 HTML5 양식을 볼 수 있습니다. 브라우저용 추가 브라우저 플러그인을 설치하지 않아도 됩니다. 지원되는 브라우저에 대한 자세한 내용은 [지원되는 클라이언트 플랫폼](https://adobe.com/go/learn_aemforms_supportedplatforms_63)을 참조하십시오.

![](do-not-localize/mobile_form_on_an_ipad_date_14.png)

## HTML5 양식의 주요 기능 {#key-capabilities-of-html-forms-br}

* 호환되는 모든 브라우저에서 지원되는 HTML5의 기존 XFA 양식을 렌더링합니다.
* 표준 XFA 양식 디자인 기능을 활용하여 모바일 디바이스용 양식을 타깃팅합니다.
* HTML5 형식의 동적 XFA 기능을 사용합니다.
* PDF 텍스트 레이아웃과 일치하도록 매우 정확한 SVG 텍스트 레이아웃(SVG 1.1)을 사용합니다.
* JavaScript 및 FormCalc 지원을 제공합니다.
* 데이터 기반의 이벤트 또는 사용자 입력을 기반으로 조각을 인터랙티브한 양식으로 동적으로 취합할 수 있습니다.
* 기업 표준에 따라 양식의 모양에 맞게 사용자 지정 CSS를 지원합니다.
* 사용자 정의 위젯을 사용하여 풍부한 데이터 캡처 환경을 제공할 수 있습니다.
* 웹 앱과의 통합을 지원합니다.

### 다중 채널 게시 {#multichannel-publishing}

양식 개발자는 XFA 템플릿을 사용하여 PDF 및 HTML5 형식으로 양식을 렌더링할 수 있습니다. 이 기능은 HTML5 양식 디자인 사례에 맞게 최소한의 변경을 요구하는 많은 XFA 양식 세트가 있는 시나리오에서 유용합니다. XFA 기반 PDF가 아직 지원되지 않는 다양한 장치를 대상으로 기존 XFA 양식을 HTML5로 렌더링할 수 있습니다.

## HTML5 양식 관리 {#manage-html-forms}

또한 AEM은 AEM Forms UI를 사용하여 모든 양식 템플릿을 나열하고 관리할 수 있는 통합 뷰를 제공합니다. 양식을 활성화, 비활성화, 게시 및 미리 볼 수 있습니다. 자세한 내용은 [양식 관리 소개](../../forms/using/introduction-managing-forms.md)를 참조하십시오.

### Forms 사용자 정의 {#forms-customization}

HTML5 양식은 표준 HTML5 구문을 사용하여 양식 템플릿을 렌더링합니다. 따라서 웹 기술, 주로 CSS 및 JavaScript를 사용하여 HTML5 형식으로 양식을 간단하게 사용자 정의하고 확장할 수 있습니다. 기존 위젯의 모양을 손쉽게 사용자 정의하거나 고유한 사용자 정의 위젯을 만들거나 양식에 사용자 정의 스타일을 사용할 수 있습니다. 사용자 정의 위젯을 만들고 기존 위젯을 사용자 정의하는 방법에 대한 자세한 내용은 [HTML5 양식](../../forms/using/custom-widgets.md)으로 사용자 정의 위젯 플러그인을 참조하십시오.
