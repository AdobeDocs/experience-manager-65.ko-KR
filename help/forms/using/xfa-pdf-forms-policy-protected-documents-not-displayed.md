---
title: XFA 기반 PDF forms 및 정책으로 보호된 문서에 대한 문제 표시
description: XFA 기반 PDF forms 및 정책으로 보호된 문서에 대한 문제 표시
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: ebb61f2c5056a780e829e64031f8eba69a8ae25b
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# XFA 기반 PDF forms 및 정책으로 보호된 문서에 대한 문제 표시

Adobe LiveCycle Rights Management를 사용하여 XFA 기반 PDF 양식 또는 정책으로 보호된 문서를 열 수 없는 경우 다음 이유를 확인하십시오.

* XFA 기반 PDF forms 및 정책으로 보호된 문서에는 Adobe® Acrobat® 또는 Adobe® Reader® 버전 8 이상이 필요합니다. 최신 Reader 또는 Acrobat 다운로드는 [Adobe 다운로드](https://www.adobe.com/downloads.html)를 참조하십시오.
* Mozilla Firefox 및 Google Chrome과 같은 브라우저에서는 XFA 기반 PDF forms을 지원하지 않는 내장된 PDF 뷰어를 제공합니다. 이러한 브라우저에서 XFA 기반 PDF forms을 보려면 Acrobat 또는 Reader을 사용하여 PDF를 열도록 을 구성해야 합니다. 자세한 내용은 Mozilla Firefox의 XFA 기반 PDF forms 및 Google Chrome 를 참조하십시오.
* Microsoft® Windows®의 Acrobat 및 Reader을 사용하면 보호된 보기 모드에서 PDF를 열도록 구성할 수 있으므로 XFA 기반 PDF forms 및 정책으로 보호된 문서를 열 수 없습니다. Acrobat 또는 Reader의 보호된 보기 모드가 비활성화되어 있는지 확인합니다. 자세한 내용은 [보호된 보기(Windows만 해당)](https://helpx.adobe.com/acrobat/kb/end-of-support-acrobat-x-reader-x.html)를 참조하십시오.
* 모바일 장치에서 XFA 기반 PDF forms 또는 정책으로 보호된 문서에 액세스하려는 경우 다음 사항을 고려하십시오.

   * 모바일 장치에서 정책으로 보호된 문서를 열려면 모바일용 Adobe Reader가 필요합니다. 자세한 내용은 [Adobe Reader 모바일 앱](https://www.adobe.com/in/acrobat/mobile/acrobat-reader.html)을 참조하십시오.
   * iOS, Android, Blackberry 모바일 디바이스 및 스마트폰은 XFA 양식이 포함된 Adobe Reader 플러그인을 지원하지 않습니다. LiveCycle ES4는 HTML5를 사용하여 모바일 장치를 타깃팅하는 서비스를 제공합니다. 양식 작성자는 해당 서비스를 사용하여 이러한 장치에서 양식을 사용할 수 있도록 해야 합니다.
   * Windows 8 모바일 장치에서 Metro 스타일을 사용하는 경우 클래식 보기로 변경하거나 LiveCycle ES4에서 HTML5를 활용하십시오.

>[!NOTE]
>
>LiveCycle ES4는 HTML5에서 XFA 기반 양식을 렌더링할 수 있도록 지원하므로 iPad과 같은 모바일 디바이스에서 실행되는 양식을 포함하여 HTML5가 지원되는 브라우저에서 양식을 열 수 있습니다. 양식의 HTML5 렌디션은 양식 디자인의 레이아웃을 유지 관리하고 XFA 양식 템플릿에 포함된 대부분의 양식 논리(예: JavaScript, 양식 계산 및 양식 유효성 검사)를 지원합니다. 이렇게 하면 XFA 양식에 대한 기술 투자가 Adobe Reader 플러그인을 실행할 수 없는 디바이스로 쉽게 이월됩니다.
>자세한 내용은 [LiveCycle 제품 설명서로 업그레이드](https://business.adobe.com/products/experience-manager/forms/aem-forms.html)를 참조하십시오.

[법적 고지 사항](https://chl-author-preview.corp.adobe.com/content/help/en/legal/legal-notices.html)    |    [온라인 개인정보 처리방침](https://www.adobe.com/kr/privacy.html)