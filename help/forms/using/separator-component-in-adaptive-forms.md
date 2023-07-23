---
title: 적응형 양식의 분리자 구성 요소
seo-title: Separator component in adaptive forms
description: 분리자 구성 요소를 사용하여 양식의 단면을 시각적으로 분리할 수 있습니다.
seo-description: You can use the separator component to visually segregate sections of a form.
uuid: f8d2aed3-52aa-437f-bfe3-0c8779e7986c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: a8aa77fe-5880-4c4e-9e1b-3c5a8772c29d
docset: aem65
feature: Adaptive Forms
exl-id: 11cbf865-c8e2-4833-b0b8-a3cb5e42f5cd
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 4%

---

# 적응형 양식의 분리자 구성 요소{#separator-component-in-adaptive-forms}

<span class="preview"> Adobe은 현대적이고 확장 가능한 데이터 캡처를 사용할 것을 권장합니다 [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) 대상 [새 적응형 Forms 만들기](/help/forms/using/create-an-adaptive-form-core-components.md) 또는 [AEM Sites 페이지에 적응형 Forms 추가](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). 이러한 구성 요소는 적응형 Forms 작성의 중요한 발전을 나타내어 인상적인 사용자 경험을 보장합니다. 이 문서에서는 기초 구성 요소를 사용하여 적응형 Forms을 작성하는 이전 방법에 대해 설명합니다. </span>

분리자 구성 요소를 사용하여 폼의 패널을 시각적으로 분리할 수 있습니다. 분리자 구성 요소의 다음 속성을 지정하여 분리자 구성 요소의 전체 모양과 스타일을 정의할 수 있습니다.

* **요소 이름:** 구성 요소의 이름을 지정합니다. SOM 표현식은 요소 이름 필드에 지정된 값으로 구성 요소를 해결합니다.
* **두께:** 분리자 구성 요소의 두께를 픽셀 단위로 지정합니다.

* **CSS 클래스:** 구분 기호 구성 요소에 대한 사용자 지정 CSS 클래스를 지정합니다.

* **인라인 스타일:** 이제 AEM Forms을 사용하여 인라인 CSS 스타일을 개별 적응형 양식 구성 요소에 적용하고 변경 사항을 실시간으로 미리 볼 수 있습니다.

레이아웃 모드를 사용하여 구분자 구성 요소가 걸쳐 있는 열의 수를 정의할 수 있습니다. 자세한 내용은 [레이아웃 모드를 사용하여 구성 요소의크기 조정](../../forms/using/resize-using-layout-mode.md)을 참조하십시오.

분리자 구성 요소의 속성을 지정하려면 다음을 수행합니다.

1. 분리자 구성 요소를 선택하고 을 누릅니다 ![cmppr](assets/cmppr.png). 사이드바에서 속성이 열립니다.
1. 인라인 CSS 속성 섹션에서 탭을 클릭하여 CSS 속성을 지정합니다. 예: a. 필드 탭에서 **항목 추가**. 필드가 두 개인 행이 추가됩니다.
1. 왼쪽의 첫 번째 필드에 적용할 CSS3 속성을 지정합니다. 예를 들어, **테두리**. 아래쪽 화살표 단추를 클릭하여 속성을 선택할 수도 있습니다. 드롭다운 목록은 완전하지 않으며 이 필드에 지원되는 CSS3 속성 이름을 지정할 수 있습니다.
1. 인접 필드에서 지정된 CSS3 속성에 유효한 값을 지정합니다. 예를 들어, **3px 단색 검정**.
1. 클릭 **항목 추가** 다른 속성과 해당 값을 지정합니다.
1. 클릭 **미리 보기** 을 클릭하여 양식의 변경 사항을 미리 봅니다.
1. 클릭 **확인** 변경 사항을 확인하거나 **취소** 변경하지 않고 대화 상자를 종료합니다.
