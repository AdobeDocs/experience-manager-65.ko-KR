---
title: 'AEM Forms의 자리 표시자 텍스트 '
seo-title: 'AEM Forms의 자리 표시자 텍스트 '
description: 자리 표시자 텍스트는 컨트롤에 값이 없을 때 데이터 항목이 있는 사용자를 돕기 위한 것입니다. 샘플 값 또는 예상 형식에 대한 간단한 설명일 수 있습니다.
seo-description: 자리 표시자 텍스트는 컨트롤에 값이 없을 때 데이터 항목이 있는 사용자를 돕기 위한 것입니다. 샘플 값 또는 예상 형식에 대한 간단한 설명일 수 있습니다.
uuid: 69f80722-93db-4932-9016-4b530e183d4e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: f9ff2cc5-3f0a-4b2f-a206-2fe0985646ea
docset: aem65
feature: 적응형 양식
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 1%

---


# AEM Forms {#placeholder-text-in-aem-forms}의 자리 표시자 텍스트

자리 표시자 텍스트는 단어 또는 짧은 구를 나타냅니다. 컨트롤에 값이 없을 때 데이터 항목이 있는 사용자를 돕기 위한 것입니다. 자리 표시자 텍스트는 샘플 값이거나 예상 형식에 대한 간단한 설명일 수 있습니다. 사용자가 값을 입력하기 전에 자리 표시자 텍스트가 표시되고, 사용자가 값을 입력하거나 선택하면 해당 텍스트가 제거됩니다.

>[!NOTE]
>
>자리 표시자 텍스트에는 새 줄 문자가 포함되지 않은 값이 있어야 합니다.

![자리 표시자 텍스트가 있는 날짜 구성 요소 및 없는 날짜](assets/dat-picker-place-holder-text.png)

**자리 표시자 텍스트** B. **Date 구성 요소가 있는 A.** Date 구성 요소(자리 표시자 텍스트 없음)

AEM Forms은 암호 상자, 날짜 선택기, 숫자 상자 및 텍스트 상자 필드에 대한 자리 표시자 텍스트를 지원합니다.\
자리 표시자 텍스트는 기본 HTML5 날짜 위젯에 대해 지원되지 않습니다. 자리 표시자 텍스트를 지정하려면:

1. 자리 표시자 텍스트를 지원하는 구성 요소를 마우스 오른쪽 단추로 클릭하고 **편집**&#x200B;을 클릭합니다. 구성 요소 편집 대화 상자가 나타납니다.

1. **제목 및 텍스트** 탭을 엽니다.
1. **자리 표시자 텍스트 상자**&#x200B;에 단어나 짧은 구를 지정합니다. **확인**&#x200B;을 클릭합니다.

>[!NOTE]
>
>자리 표시자 텍스트는 Microsoft Internet Explorer 9에서 지원되지 않습니다.

