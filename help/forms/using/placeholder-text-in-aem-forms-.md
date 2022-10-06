---
title: AEM Forms의 자리 표시자 텍스트
seo-title: Placeholder text in AEM Forms
description: 자리 표시자 텍스트는 컨트롤에 값이 없을 때 사용자에게 데이터 항목을 제공하기 위한 것입니다. 샘플 값이거나 예상 형식에 대한 간단한 설명일 수 있습니다.
seo-description: Placeholder text is intended to aid the user with data entry when the control has no value. It could be a sample value or a brief description of the expected format.
uuid: 69f80722-93db-4932-9016-4b530e183d4e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: f9ff2cc5-3f0a-4b2f-a206-2fe0985646ea
docset: aem65
feature: Adaptive Forms
exl-id: 6b6e27b5-8b4e-489c-9e72-4d256692c1ca
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---

# AEM Forms의 자리 표시자 텍스트 {#placeholder-text-in-aem-forms}

자리 표시자 텍스트는 단어 또는 짧은 구를 나타냅니다. 컨트롤에 값이 없을 때 사용자에게 데이터 항목을 지원하기 위한 것입니다. 자리 표시자 텍스트는 샘플 값이거나 예상 형식에 대한 간단한 설명일 수 있습니다. 사용자가 값을 입력하기 전에 자리 표시자 텍스트가 표시되며, 사용자가 값을 입력하거나 선택하면 제거됩니다.

>[!NOTE]
>
>지정되는 경우 자리 표시자 텍스트에는 새 줄 문자가 포함되지 않은 값이 있어야 합니다.

![자리 표시자 텍스트가 있는 날짜 구성 요소 및 없는 날짜](assets/dat-picker-place-holder-text.png)

**A.** 자리 표시자 텍스트가 있는 날짜 구성 요소 **B.** 자리 표시자 텍스트가 없는 날짜 구성 요소

AEM Forms에서는 암호 상자, 날짜 선택기, 숫자 상자 및 텍스트 상자 필드에 대한 자리 표시자 텍스트를 지원합니다.\
기본 HTML5 날짜 위젯에는 자리 표시자 텍스트가 지원되지 않습니다. 자리 표시자 텍스트를 지정하려면 다음과 같이 하십시오.

1. 자리 표시자 텍스트를 지원하는 구성 요소를 마우스 오른쪽 단추로 클릭하고 를 클릭합니다 **편집**. 구성 요소 편집 대화 상자가 나타납니다.

1. 를 엽니다. **제목 및 텍스트** 탭.
1. 에서 단어 또는 짧은 구를 지정합니다. **자리 표시자 텍스트 상자**. **확인**&#x200B;을 클릭합니다.

>[!NOTE]
>
>자리 표시자 텍스트는 Microsoft Internet Explorer 9에서 지원되지 않습니다.
