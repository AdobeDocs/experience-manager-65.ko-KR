---
title: Firefox 및 Chrome에서 XFA 기반 PDF forms을 여는 방법
description: Firefox 및 Chrome에서 XFA 기반 PDF forms을 여는 방법
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: ebb61f2c5056a780e829e64031f8eba69a8ae25b
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 1%

---

# Firefox 및 Chrome에서 XFA 기반 PDF forms을 여는 방법

## 문제

Mozilla Firefox 및 Google Chrome과 함께 도입된 내장 PDF 뷰어는 XFA 기반 PDF forms을 지원하지 않습니다. 따라서 XFA 기반 PDF forms은 최신 버전의 Firefox 및 Chrome에서 열리지 않습니다.

## 솔루션

Firefox 및 Chrome에서 XFA 기반 PDF forms을 사용하려면 다음 단계를 수행하여 Adobe Reader 또는 Adobe Acrobat을 사용하여 PDF를 열도록 Firefox 및 Chrome을 구성합니다.

>[!NOTE]
> 
> 시스템에 Adobe Reader 또는 Adobe Acrobat이 설치되어 있는지 확인합니다.

### Firefox 구성

1. Firefox에서 **도구 > 옵션**&#x200B;을 선택합니다.

1. 옵션 대화 상자에서 **응용 프로그램**&#x200B;을 클릭합니다.

1. 애플리케이션 탭의 검색 필드에 PDF을 입력합니다.

1. 검색 결과의 Portable Document Format(PDF) 컨텐츠 유형에 대해 작업 드롭다운 목록에서 **Adobe Acrobat 사용(Firefox에서)**&#x200B;을 선택합니다.
   ![use-adobe-acrobat](/help/forms/using/assets/use-adobe-acrobat.png)
1. 확인을 클릭합니다.

1. Firefox를 다시 시작합니다.

### Chrome 구성

1. Chrome에서 chrome://plugins/으로 이동합니다.

1. Chrome PDF 뷰어 아래에서 비활성화 를 클릭하고 Adobe PDF 플러그인 아래에서 활성화 를 클릭합니다.
   ![chrome-pdf-viewer](/help/forms/using/assets/chrome-image.png)
자세한 내용은 Google의 [Adobe PDF 플러그인](https://support.google.com/chrome/?hl=en&amp;visit_id=638803785294106945-2276548125&amp;rd=4&amp;topic=3421431#topic=7439538) 설명서를 참조하십시오.

>[!NOTE]
> 
> LiveCycle ES4는 HTML5에서 XFA 기반 양식을 렌더링할 수 있도록 지원하므로 iPad과 같은 모바일 디바이스에서 실행되는 양식을 포함하여 HTML5가 지원되는 브라우저에서 양식을 열 수 있습니다. 양식의 HTML5 렌디션은 양식 디자인의 레이아웃을 유지 관리하고 XFA 양식 템플릿에 포함된 대부분의 양식 논리(예: JavaScript, 양식 계산 및 양식 유효성 검사)를 지원합니다. 이러한 방식으로 XFA 양식에 대한 기술 투자는 Adobe Reader 플러그인의 실행이 불가능한 장치로 쉽게 이전됩니다.
>자세한 내용은 [LiveCycle 제품 설명서](https://business.adobe.com/products/experience-manager/forms/aem-forms.html)를 참조하십시오.

[법적 고지 사항](https://chl-author-preview.corp.adobe.com/content/help/en/legal/legal-notices.html)    |    [온라인 개인정보 처리방침](https://www.adobe.com/kr/privacy.html)