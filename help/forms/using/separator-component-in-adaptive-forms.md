---
title: 적응형 양식의 구분 기호 구성 요소
seo-title: 적응형 양식의 구분 기호 구성 요소
description: 구분 기호 구성 요소를 사용하여 양식의 섹션을 시각적으로 분리할 수 있습니다.
seo-description: 구분 기호 구성 요소를 사용하여 양식의 섹션을 시각적으로 분리할 수 있습니다.
uuid: f8d2aed3-52aa-437f-bfe3-0c8779e7986c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: a8aa77fe-5880-4c4e-9e1b-3c5a8772c29d
docset: aem65
feature: 적응형 양식
exl-id: 11cbf865-c8e2-4833-b0b8-a3cb5e42f5cd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 3%

---

# 적응형 양식의 구분 기호 구성 요소{#separator-component-in-adaptive-forms}

구분 기호 구성 요소를 사용하여 양식의 패널을 시각적으로 분리할 수 있습니다. 구분 기호 구성 요소의 다음 속성을 지정하여 구분 기호 구성 요소의 전체 모양과 스타일을 정의할 수 있습니다.

* **요소 이름:** 구성 요소의 이름을 지정합니다. SOM 표현식은 요소 이름 필드에 지정된 값으로 구성 요소를 해결합니다.
* **두께:** 구분 기호 구성 요소의 두께(픽셀)를 지정합니다.

* **CSS 클래스:** 구분 기호 구성 요소에 대한 사용자 지정 CSS 클래스를 지정합니다

* **인라인 스타일:**  이제 AEM Forms을 사용하여 인라인 CSS 스타일을 개별 적응형 양식 구성 요소에 적용하고 실시간으로 변경 사항을 미리 볼 수 있습니다.

레이아웃 모드를 사용하여 구분 기호 구성 요소가 속하는 열 수를 정의할 수 있습니다. 자세한 내용은 [레이아웃 모드를 사용하여 구성 요소의크기 조정](../../forms/using/resize-using-layout-mode.md)을 참조하십시오.

구분 기호 구성 요소의 속성을 지정하려면

1. 구분 기호 구성 요소를 선택하고 ![cmppr](assets/cmppr.png)을 누릅니다. 속성은 사이드바에서 열립니다.
1. 인라인 CSS 속성 섹션에서 탭을 클릭하여 CSS 속성을 지정합니다. 예:a.필드 탭에서 **항목 추가**&#x200B;를 클릭합니다. 필드가 두 개인 행이 추가됩니다.
1. 왼쪽의 첫 번째 필드에서 적용할 CSS3 속성을 지정합니다. 예: **border** 아래쪽 화살표 단추를 클릭하여 속성을 선택할 수도 있습니다. 드롭다운 목록은 완전하지 않으며 이 필드에 지원되는 CSS3 속성 이름을 지정할 수 있습니다.
1. 인접 필드에서 지정된 CSS3 속성에 유효한 값을 지정합니다. 예를 들어, **3px 솔리드 블랙**&#x200B;입니다.
1. **항목 추가**&#x200B;를 클릭하여 다른 속성과 해당 값을 지정합니다.
1. **미리 보기**&#x200B;를 클릭하여 양식의 변경 사항을 미리 봅니다.
1. **확인**&#x200B;을 클릭하여 변경 내용을 확인하거나 **취소**&#x200B;를 클릭하여 변경 없이 대화 상자를 종료합니다.
