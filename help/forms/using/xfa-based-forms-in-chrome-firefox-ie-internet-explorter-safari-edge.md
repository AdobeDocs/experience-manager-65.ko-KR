---
title: Google Chrome, Firefox, Microsoft&reg; Edge, Microsoft&reg; Internet Explorer 또는 Apple Safari에서 XFA 기반 PDF forms을 열 수 없음
description: Google Chrome, Firefox, Microsoft&reg; Edge, Microsoft&reg; Internet Explorer 또는 Apple Safari에서 XFA 기반 PDF forms을 열 수 없음
feature: Adaptive Forms,Document Services
exl-id: fdd15315-e0d6-4d80-acb4-2e0ecec716c4
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 2ffd69c153c60ada3fcb586ed5aa5bda48f645fc
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---

# Google Chrome, Firefox, Microsoft® Edge, Microsoft® Internet Explorer 또는 Apple Safari에서 XFA 기반 PDF forms을 열 수 없음{#unable-to-open-XFA-based-PDF-forms-in-Google-Chrome-Firefox-Microsoft-Edge-Microsoft-Internet-Explorer-or-Apple-Safari}

많은 최신 브라우저 버전에는 XFA 기반 PDF forms에 대한 제한된 자체 지원이 포함되어 있습니다. 이러한 브라우저에서는 XFA 기반 PDF forms을 열 수 있지만, 제공되는 기능은 제한됩니다. 최신 브라우저에서 XFA 기반 PDF 양식을 열거나 제출할 수 없는 경우 다음 방법 중 하나를 사용하십시오.

* [Adobe® Acrobat®](https://www.adobe.com/acrobat.html) 또는 [Adobe® Adobe® Reader®](https://get.adobe.com/reader/) 버전 8 이상을 사용하여 XFA 기반 PDF forms을 열고 제출합니다.
* Microsoft® Windows®의 Acrobat 및 Reader을 사용하면 보호된 보기 모드에서 PDF를 열도록 구성하여 XFA 기반 PDF forms을 열 수 없습니다. Acrobat 또는 Reader의 보호된 보기 모드가 비활성화되어 있는지 확인합니다. 자세한 내용은 [보호된 보기(Windows만 해당)](https://helpx.adobe.com/in/reader/using/protected-mode-windows.html)를 참조하십시오.
* (Forms 개발자용) Adobe Experience Manager Forms은 또한 다음을 지원합니다.

   * [XFA 기반 양식을 HTML5 Forms으로 렌더링](https://experienceleague.adobe.com/docs/experience-manager-65/forms/html5-forms/introduction.html?#key-capabilities-of-html-forms-br) 양식을 HTML5에서 지원하는 브라우저에서 열 수 있도록 합니다. 이러한 브라우저에는 iPad과 같은 모바일 장치에서 실행되는 브라우저도 포함됩니다. 양식의 HTML5 렌디션은 양식 디자인의 레이아웃을 유지 관리하고 XFA 양식 템플릿에 포함된 대부분의 양식 논리(예: JavaScript, 양식 계산 및 양식 유효성 검사)를 지원합니다.
   * [XFA 기반 양식을 모바일 반응형 적응형 Forms으로 변환](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html?#create-an-adaptive-form-based-on-an-xfa-form-template). 이러한 양식은 응답형 레이아웃, 개인화 기능을 제공하며 필요에 따라 필드나 섹션을 추가하거나 제거하여 사용자 응답에 동적으로 적응합니다. 또한 다양한 데이터 소스, 기록 문서 기능 및 성능 평가를 위해 Adobe Analytics에 손쉽게 연결할 수 있는 즉시 사용 가능한 커넥터를 제공합니다. 자세한 내용은 [주요 기능](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html?lang=en)을 참조하세요.
이렇게 하면 XFA 양식에 대한 기술 투자가 보호되며 최종 사용자에게 최적의 환경을 계속 제공할 수 있습니다. 자세한 내용은 [Adobe Experience Manager Forms 제품 설명서](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html)를 참조하세요.
