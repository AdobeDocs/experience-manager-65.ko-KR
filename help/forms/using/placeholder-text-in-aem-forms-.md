---
title: AEM Forms의 자리 표시자 텍스트
description: 자리 표시자 텍스트는 컨트롤에 값이 없을 때 사용자에게 데이터 입력을 지원하기 위한 것입니다. 샘플 값이거나 예상 형식에 대한 간략한 설명일 수 있습니다.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms, Foundation Components
exl-id: 6b6e27b5-8b4e-489c-9e72-4d256692c1ca
source-git-commit: d85fc98d9a31bc4014aef4311ba0f838c7ef619a
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 19%

---

# AEM Forms의 자리 표시자 텍스트 {#placeholder-text-in-aem-forms}

<span class="preview"> [새 적응형 양식 만들기](/help/forms/using/create-an-adaptive-form-core-components.md) 또는 [AEM Sites 페이지에 적응형 양식 추가](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) 작업을 할 때 현대적이고 확장 가능한 데이터 캡처 [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)를 사용하는 것이 좋습니다. 이러한 구성 요소는 적응형 양식 만들기 작업이 대폭 개선되어 우수한 사용자 경험을 보장할 수 있게 되었음을 나타냅니다. 이 문서에서는 기초 구성 요소를 사용하여 적응형 양식을 작성하는 이전 접근법에 대해 설명합니다. </span>

자리 표시자 텍스트는 단어 또는 짧은 구를 나타냅니다. 이는 컨트롤에 값이 없을 때 사용자에게 데이터 입력을 지원하기 위한 것입니다. 자리 표시자 텍스트는 샘플 값이거나 예상 형식에 대한 간략한 설명일 수 있습니다. 자리 표시자 텍스트는 사용자가 값을 입력하기 전에 표시되며, 사용자가 값을 입력하거나 선택할 때 제거됩니다.

>[!NOTE]
>
>자리 표시자 텍스트는 지정되는 경우 새 줄 문자가 포함되지 않은 값을 가져야 합니다.

![자리 표시자 텍스트가 있거나 없는 날짜 구성 요소](assets/dat-picker-place-holder-text.png)

**A.** 자리 표시자 텍스트가 있는 날짜 구성 요소 **B.** 자리 표시자 텍스트가 없는 날짜 구성 요소

AEM Forms에서는 암호 상자, 날짜 선택기, 숫자 상자 및 텍스트 상자 필드에 대한 자리 표시자 텍스트를 지원합니다.\
기본 HTML5 날짜 위젯에 대해서는 자리 표시자 텍스트가 지원되지 않습니다. 자리 표시자 텍스트를 지정하려면 다음을 수행합니다.

1. 자리 표시자 텍스트를 지원하는 구성 요소를 마우스 오른쪽 단추로 클릭하고 **편집**. 구성 요소 편집 대화 상자가 나타납니다.

1. 를 엽니다. **제목 및 텍스트** 탭.
1. 다음 위치에 단어 또는 짧은 구 지정 **자리 표시자 텍스트 상자**. **확인**&#x200B;을 클릭합니다.

>[!NOTE]
>
>자리 표시자 텍스트는 Microsoft Internet Explorer 9에서 지원되지 않습니다.
