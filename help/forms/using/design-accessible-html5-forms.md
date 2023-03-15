---
title: 액세스 가능한 HTML 5 양식 디자인
seo-title: Designing accessible HTML5 forms
description: HTML5 양식은 ARIA HTML5 접근성 표준을 사용합니다. 이러한 양식은 탭 탐색을 지원하며 공통 화면 판독기와 호환되도록 인증되었습니다.
seo-description: HTML5 forms use the ARIA HTML5 accessibility standard. These forms support tabbed navigation and are certified to be compatible with common screen readers.
uuid: 1ce5ba39-69ea-4d0e-96ea-e2a38b21d6b7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 8711ad33-396b-4572-b2ee-71e9f45f4ebe
docset: aem65
feature: Mobile Forms
exl-id: fca2f9b2-11a2-4db0-a370-c4046f32be63
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---

# 액세스 가능한 HTML 5 양식 디자인 {#designing-accessible-html-forms}

HTML5 양식은 ARIA HTML5 접근성 표준을 사용하여 액세스 가능한 HTML 양식을 생성합니다. 이러한 양식은 탭 탐색을 지원하며(Mozilla FireFox 제외), 일반 화면 판독기와 호환되도록 인증되었습니다. 접근성 기능이 좋은 HTML5 양식을 생성하려면 몇 가지 기본 디자인 지침을 기반으로 XFA 양식 템플릿을 디자인하십시오. 디자인 지침에는 올바른 탭 순서 구성과 각 양식 컨트롤에 대한 텍스트 말하기 콘텐츠 제공이 포함되어 있습니다. AEM Forms Designer에서는 액세스 가능한 PDF 및 HTML 5 양식을 생성하기 위해 이러한 양식 제어 속성을 설정할 수 있습니다.

*참고:탭 탐색은 값의 합계를 표시하는 계산 필드와 같은 보호된 필드를 포함하지 않습니다. 화면 판독기에서 보호된 필드의 값을 읽으려면 보호된 필드의 위나 옆에 빈 읽기 전용 필드를 배치하십시오. 보호된 필드의 값을 새 읽기 전용 필드에 할당합니다. 화면 판독기 또는 탭 탐색에서 이 읽기 전용 필드를 선택하여 보호된 필드의 값으로 말할 수 있습니다.*

AEM Forms Designer에는 화면 판독기에 전달할 수 있는 다양한 텍스트 말하기 옵션이 포함되어 있습니다. 양식의 각 개체에 대해 화면 판독기 텍스트에 대한 여러 설정 중 하나를 지정할 수 있습니다.

* 접근성 팔레트를 사용하여 설정할 수 있는 사용자 정의 화면 판독기 텍스트입니다. 작성자는 버튼과 필드의 이름과 목적에 주석을 달 수 있습니다.
* 도구 설명. 접근성 팔레트에서 설정할 수 있습니다.
* 양식의 필드 캡션
* 바인딩 탭의 이름 옵션에 지정된 개체의 이름입니다.

![접근성](assets/accessibility.png)

Form 컨트롤에서 도구 설명, 화면 Reader 텍스트 및 캡션과 같은 여러 옵션을 사용할 수 있는 경우 화면 Reader은 이러한 속성 중 하나만 사용합니다. 기본 순서는 사용자 정의 화면 Reader 텍스트, 도구 설명, 캡션 및 이름입니다. 화면 Reader을 사용하여 기본 순서를 재정의할 수 있습니다 **우선 순위** 옵션 을 참조하십시오.
