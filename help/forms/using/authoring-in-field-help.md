---
title: 양식 필드에 대한 컨텍스트 내 도움말 작성
seo-title: 양식 필드에 대한 컨텍스트 내 도움말 작성
description: AEM Forms에서는 비디오를 포함한 텍스트 또는 리치 미디어로 적응형 양식 필드 및 패널에 컨텍스트 내 도움말을 추가할 수 있습니다.
seo-description: AEM Forms에서는 비디오를 포함한 텍스트 또는 리치 미디어로 적응형 양식 필드 및 패널에 컨텍스트 내 도움말을 추가할 수 있습니다.
uuid: 1865bf7b-66fc-4f89-bd98-904daa409320
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 78000342-a6a7-4c2e-acab-a88851b82c2a
docset: aem65
feature: 적응형 양식
exl-id: 6569bfba-9af5-4060-8640-e51d7af46614
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 1%

---

# 양식 필드에 대한 컨텍스트 내 도움말 작성{#authoring-in-context-help-for-form-fields}

## 소개 {#introduction}

양식에 입력하는 최종 사용자가 특정 양식 필드에 세부 사항을 채우는 방법을 모를 때 발생합니다. 이러한 문제를 해결하기 위해 적응형 양식은 양식 필드에 텍스트나 풍부한 컨텍스트 내 도움말을 추가할 수 있도록 지원합니다. 양식 채우기 경험을 개선하는 데 도움이 되며 최종 사용자의 모호성을 방지할 수 있습니다.

이 문서에서는 양식 작성자가 적응형 Forms을 작성하는 동안 컨텍스트 내 도움말을 추가하는 방법에 대해 설명합니다.

## 컨텍스트 내 도움말 {#add-in-context-help} 추가

사이드바의 속성 탭에 있는 도움말 컨텐츠 섹션에서 다음 옵션을 사용하여 컨텍스트 내 도움말을 지정할 수 있습니다.

* [간단한 설명입니다](../../forms/using/authoring-in-field-help.md#p-short-description-p)
* [긴 설명](../../forms/using/authoring-in-field-help.md#p-long-description-p)

![양식 필드에 대한 컨텍스트 내 도움말](assets/descriptions.png)

>[!NOTE]
>
>긴 설명은 짧은 설명을 무시합니다. 둘 다 지정한 경우 긴 설명만 표시됩니다.

### 간단한 설명입니다 {#short-description}

간단한 설명 필드는 양식 필드 채우기에 대한 빠른 힌트와 짧은 힌트를 제공하는 것입니다. [짧은 설명] 필드에 지정된 텍스트는 마우스로 필드를 가리키면 도구 설명으로 표시됩니다.

![양식 필드에 대한 컨텍스트 내 도움말 추가에 대한 간단한 설명](assets/tooltip.png)

>[!NOTE]
>
>**항상 짧은 설명 표시**&#x200B;를 선택하여 필드 아래에 도움말 텍스트를 영구적으로 표시합니다.

![필드 아래에 영구적인 간단한 컨텍스트 내 도움말](assets/short1.png)

### 긴 설명 {#long-description}

긴 설명 필드를 사용하여 컨텍스트 내의 도움말처럼 긴 텍스트를 지정하거나 비디오를 포함한 리치 미디어 컨텐츠를 포함할 수 있습니다. 예를 들어 다음 이미지는 컨텍스트 내 도움말로 비디오를 포함할 수 있는 방법을 보여줍니다.

![양식 필드에 대한 컨텍스트 내 도움말로 리치 미디어 추가](assets/long-descriptions.png)

긴 설명을 추가하면 **?가 표시됩니다.** 아이콘 을 클릭하여 제품에서 사용할 수 있습니다. 아이콘을 클릭하면 긴 설명 섹션에 추가된 컨텐츠가 표시됩니다.

![리치 미디어 in-context 도움말 예](assets/photoshop.png)

### 패널 수준 도움말 {#panel-level-help}

양식 필드에 대한 컨텍스트 내 도움말 외에도, 패널 편집 대화 상자의 도움말 콘텐츠 탭에서 패널 수준에서 도움말을 지정할 수 있습니다.

![양식 패널에 대한 컨텍스트 내 도움말 추가](assets/panel-level-help.png)

패널에 대한 도움말을 추가하면 **이 표시됩니까?** 아이콘 위로 이동합니다. 아이콘을 클릭하면 패널 편집 대화 상자의 도움말 컨텐츠 섹션에 추가된 컨텐츠가 표시됩니다.

![양식 패널 수준의 컨텍스트 내 도움말 예](assets/photoshop-1.png)
