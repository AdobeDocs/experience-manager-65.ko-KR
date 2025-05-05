---
title: 다단계 양식 시퀀스 소개
description: AEM Forms을 사용하여 사용자가 적응형 양식을 탐색하고 채울 양식 패널 시퀀스를 정의할 수 있습니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
exl-id: 1333c6cb-15cc-429b-a13e-5d23afdee69a
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 32%

---

# 다단계 양식 시퀀스 소개{#introduction-to-multi-step-form-sequence}

<span class="preview"> [새 적응형 양식 만들기](/help/forms/using/create-an-adaptive-form-core-components.md) 또는 [AEM Sites 페이지에 적응형 양식 추가](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) 작업을 할 때 현대적이고 확장 가능한 데이터 캡처 [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ko)를 사용하는 것이 좋습니다. 이러한 구성 요소는 적응형 양식 만들기 작업이 대폭 개선되어 우수한 사용자 경험을 보장할 수 있게 되었음을 나타냅니다. 이 문서에서는 기초 구성 요소를 사용하여 적응형 Forms을 작성하는 이전 방법에 대해 설명합니다. </span>

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-layout-of-an-adaptive-form/introduction-form-sequence.html?lang=ko) |
| AEM 6.5 | 이 문서 |


적응형 양식을 사용하면 양식 작성자가 매우 쉽게 여러 단계의 데이터 캡처 경험을 만들 수 있습니다. 여러 패널을 만들고 각 패널을 다른 탐색 패턴과 연결하는 기본 제공 지원이 제공됩니다. 양식 작성자는 논리 섹션의 양식 필드를 그룹화하고 그룹을 패널로 나타낼 수 있습니다. 패널 레이아웃을 사용하여 패널 간 전체 탐색을 제어합니다. 작성자는 다른 레이아웃으로 패널을 정렬하도록 선택할 수 있습니다. 예를 들어 마법사 레이아웃을 사용하여 순차적으로 배치하거나 탭 레이아웃을 사용하여 임시로 배치할 수 있습니다. 패널 레이아웃에 대한 자세한 내용은 [적응형 양식의 레이아웃 기능](../../forms/using/layout-capabilities-adaptive-forms.md)을 참조하세요.

일반적인 양식 작성 환경에서는 데이터를 캡처하는 것 이상의 다양한 단계가 포함됩니다. 전체 양식 제출에는 양식에 디지털 서명을 하고, 양식에 입력된 정보를 확인하고, 결제를 처리하는 등의 다른 단계가 포함될 수 있습니다. 상황에 따라 다릅니다.

사용 사례에서 데이터 캡처를 위한 일련의 단계를 의무화하거나 특정 단계를 수행해야 하는 규정이 있는 경우, AEM Forms에서 양식 간에 이러한 일반적인 구조를 적용할 수 있는 방법을 제공합니다. 양식 구조를 미리 구현하면 양식에 대한 단계 순서가 정의됩니다. ![다단계 양식 시퀀스의 예](assets/formpipeline.png)

다단계 양식 시퀀스의 예

양식의 채우기, 확인, 서명 및 확인 단계에 대해 시퀀스를 만들어야 하는 사용 사례를 살펴보겠습니다. 이러한 시퀀스를 만들려면 다음 단계를 수행합니다.

1. 양식 템플릿을 정의하고 필요한 패널을 추가합니다. 시퀀스의 각 단계에는 한 개의 패널이 있어야 합니다. 그러나 패널 내부에 하위 패널을 포함할 수 있습니다.

   이 예에서는 다음 패널을 추가할 수 있습니다.

   * **채우기**: 데이터 캡처에 대한 양식 필드가 포함됩니다. 여기에서 중첩된 하위 패널을 포함하여 개인, 가족 및 금융과 같은 다양한 유형의 정보에 대한 섹션을 만들 수 있습니다.

   * **확인**: XFA 기반 적응형 양식에서 사용할 수 있는 **확인** 구성 요소가 포함되어 있습니다. 확인을 위해 [채우기] 패널에서 캡처한 정보가 읽기 전용 모드로 표시됩니다.

   * **전자 서명**: XFA 기반 적응형 양식에서 사용할 수 있는 **Sign** 구성 요소가 포함되어 있습니다. 다음 서명 서비스를 제공합니다.

      * Adobe Document Cloud eSign 서비스
      * 스크리블 서명

   * **확인**: 사용자가 양식에 서명하고 시퀀스의 확인(요약) 단계에 도달하면 양식 제출 확인 메시지를 표시하는 **요약** 구성 요소가 포함됩니다. 작성자는 요약 구성 요소의 텍스트를 구성하고, 감사 메시지를 표시하고, 생성된 PDF에 대한 링크를 표시하는 등의 작업을 수행할 수 있습니다.

1. 루트 패널의 레이아웃을 **[!UICONTROL 마법사]**&#x200B;로 선택합니다.
1. 양식 템플릿을 만들 수 있도록 나머지 단계를 완료합니다. [사용자 지정 적응형 양식 템플릿 만들기](../../forms/using/custom-adaptive-forms-templates.md)를 참조하세요.

양식 템플릿에서 양식 시퀀스를 정의한 후 이 시퀀스를 사용하여 시퀀스로 정의된 기본 구조가 있는 양식을 만들 수 있습니다. 언제든지 요구 사항에 맞게 양식을 사용자 정의할 수 있습니다.
