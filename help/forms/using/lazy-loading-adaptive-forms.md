---
title: 소극적 로드 옵션이 있는 대용량 양식의 성능 향상
description: 지연 로드는 양식 조각이 표시될 때까지 양식 조각의 초기화 및 로드를 지연하여 크고 복잡한 적응형 양식의 성능을 크게 향상시킵니다.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms, Foundation Components
exl-id: f7e3e2cd-0cbe-4b26-9e55-7afc6dc3af63
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 7%

---

# 소극적 로드 옵션이 있는 대용량 양식의 성능 향상{#improve-performance-of-large-forms-with-lazy-loading}

<span class="preview"> [새 적응형 양식 만들기](/help/forms/using/create-an-adaptive-form-core-components.md) 또는 [AEM Sites 페이지에 적응형 양식 추가](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) 작업을 할 때 현대적이고 확장 가능한 데이터 캡처 [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)를 사용하는 것이 좋습니다. 이러한 구성 요소는 적응형 양식 만들기 작업이 대폭 개선되어 우수한 사용자 경험을 보장할 수 있게 되었음을 나타냅니다. 이 문서에서는 기초 구성 요소를 사용하여 적응형 양식을 작성하는 이전 접근법에 대해 설명합니다. </span>

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/lazy-loading-adaptive-forms.html) |
| AEM 6.5 | 이 문서 |

## 소극적 로드 소개 {#introduction-to-lazy-loading}

양식이 수백, 수천 개의 필드로 복잡해지고 커지면 런타임 시 양식을 렌더링할 때 최종 사용자가 긴 응답 시간을 경험하게 됩니다. 응답 시간을 최소화하기 위해 적응형 양식을 논리적 조각으로 나누고 조각을 표시해야 할 때까지 조각의 초기화 또는 로드를 지연하도록 구성할 수 있습니다. 이를 지연 로드라고 합니다. 또한 사용자가 양식의 다른 섹션으로 이동한 후 조각이 더 이상 표시되지 않으면 지연 로드를 위해 구성된 조각이 언로드됩니다.

레이지 로드를 구성하기 전에 먼저 요구 사항과 준비 단계를 이해하겠습니다.

## 레이지 로드 구성 준비 중 {#preparing-to-configure-lazy-loading}

적응형 양식에서 조각의 소극적 로드를 구성하기 전에 조각을 만드는 전략을 정의하고, 스크립트에서 사용되거나 다른 조각에서 참조되는 값을 식별하고, 소극적으로 로드된 조각의 필드 가시성을 제어하는 규칙을 정의하는 것이 중요합니다.

* **조각 식별 및 만들기**
소극적 로드를 위해 적응형 양식 조각만 구성할 수 있습니다. 조각은 적응형 양식 외부에 있는 독립형 세그먼트로, 여러 양식에서 재사용할 수 있습니다. 따라서 소극적 로드를 구현하는 첫 번째 단계는 양식의 논리적 섹션을 식별하고 조각으로 변환하는 것입니다. 처음부터 조각을 만들거나 기존 양식 패널을 조각으로 저장할 수 있습니다.

  조각 만들기에 대한 자세한 내용은 [적응형 양식 단편](../../forms/using/adaptive-form-fragments.md).

* **글로벌 값 식별 및 표시**
Forms 기반 트랜잭션에는 동적 요소가 포함되어 사용자로부터 관련 데이터를 캡처하고 이를 처리하여 양식 채우기 경험을 단순화합니다. 예를 들어 양식에 다른 조각의 필드 B의 유효성을 결정하는 값이 조각 X에 필드 A가 있습니다. 이 경우 조각 X가 지연 로드로 표시된 경우 조각 X가 로드되지 않은 경우에도 필드 B의 유효성을 검사하기 위해 필드 A의 값을 사용할 수 있어야 합니다. 이를 위해 필드 A를 글로벌로 표시하여 조각 X가 로드되지 않을 때 필드 B의 유효성 검사에 해당 값을 사용할 수 있도록 할 수 있습니다.

  필드 값을 전역으로 만드는 방법에 대한 자세한 내용은 [레이지 로드 구성](../../forms/using/lazy-loading-adaptive-forms.md#p-configuring-lazy-loading-p).

* **필드의 가시성을 제어하는 규칙 작성**
Forms에는 모든 사용자 및 조건에 적용할 수 없는 일부 필드 및 섹션이 포함되어 있습니다. Forms 작성자 및 개발자는 가시성 또는 표시 숨기기 규칙을 사용하여 사용자 입력에 따라 가시성을 제어합니다. 예를 들어, Office 주소 필드는 Employment Status 필드에서 실업을 선택한 사용자에게 양식으로 표시되지 않습니다. 규칙 작성에 대한 자세한 내용은 [규칙 편집기 사용](../../forms/using/rule-editor.md).

  느리게 로드된 조각에서 가시성 규칙을 사용하여 조건부 필드가 필요한 경우에만 표시할 수 있습니다. 또한 느리게 로드된 조각의 가시성 표현식에서 참조하도록 조건부 필드를 전역으로 표시합니다.

## 레이지 로드 구성 {#configuring-lazy-loading}

적응형 양식 조각에 대한 소극적 로드를 활성화하려면 다음 단계를 수행하십시오.

1. 소극적 로드를 위해 활성화할 조각이 포함된 적응형 양식을 작성 모드에서 엽니다.
1. 적응형 양식 조각을 선택하고 ![cmppr](assets/cmppr.png).
1. 사이드바에서 활성화 **[!UICONTROL 느리게 단편 로드]** 및 선택 **완료**.

   ![적응형 양식 조각에 대한 소극적 로드 활성화](assets/lazy-loading-fragment.png)

   이제 조각이 소극적 로드에 대해 활성화됩니다.

포함된 조각이 로드되지 않은 경우 스크립트에서 사용할 수 있도록 느리게 로드된 조각의 개체 값을 전역으로 표시할 수 있습니다. 다음 작업을 수행합니다.

1. 작성 모드에서 적응형 양식 조각을 엽니다.
1. 값으로 글로벌로 표시할 필드를 선택한 다음 을 선택합니다 ![cmppr](assets/cmppr.png).
1. 사이드바에서 활성화 **지연 로드 중 값 사용**.

   ![사이드바의 레이지 로딩 필드](assets/enable-lazy-loading.png)

   이제 값이 전역으로 표시되며 포함된 조각이 언로드된 경우에도 스크립트에서 사용할 수 있습니다.

## 소극적 로드 구성을 위한 고려 사항 및 모범 사례 {#considerations-and-best-practices-for-configuring-lazy-loading}

소극적 로드 작업을 수행할 때 기억해야 할 몇 가지 제한 사항, 권장 사항 및 중요 사항은 다음과 같습니다.

* 대규모 양식에서 소극적 로드를 구성하려면 XFA 기반 적응형 양식보다 XSD 스키마 기반 적응형 양식을 사용하십시오. XFA 기반 적응형 양식의 소극적 로드 구현으로 인한 성능 향상은 XSD 기반 적응형 양식의 향상보다 상대적으로 적습니다.
* 을 사용하는 적응형 양식에서 조각에 대한 소극적 로드 구성 안 함 **[!UICONTROL 응답형 - 탐색 없이 한 페이지에 모두 표시]** 루트 패널에 대한 레이아웃입니다. 응답형 레이아웃 구성의 결과 모든 조각이 적응형 양식에서 동시에 로드됩니다. 또한 성능이 저하될 수 있습니다.
* 적응형 양식의 첫 번째 조각에서 소극적 로드를 구성하지 않는 것이 좋습니다.
* 적응형 양식 로드 시 렌더링되는 첫 번째 패널의 조각에 대해 소극적 로드를 구성하지 않는 것이 좋습니다.
* 소극적 로드는 조각 계층에서 최대 두 수준까지 지원됩니다.
* 글로벌로 표시된 필드가 적응형 양식에서 고유한지 확인합니다.
* 조건을 기반으로 표시하거나 숨겨야 하는 조각에 대한 가시성 규칙을 작성하는 것이 좋습니다. 예를 들어 사용자가 지정한 결혼 상태에 따라 배우자 세부 정보 조각을 표시하거나 숨길 수 있습니다.
* 느리게 로드된 조각에서 파일 첨부 및 약관 구성 요소가 지원되지 않습니다.

### 소극적 로드 구성을 위한 스크립팅 모범 사례 {#scripting-best-practices-for-configuring-lazy-loading}

소극적 로드 패널용 스크립트를 개발하는 동안 기억해야 할 중요한 사항은 다음과 같습니다.

* 지연 로드된 조각의 필드에 사용된 초기화 및 계산 스크립트가 기본적으로 멱등 요소인지 확인합니다. 멱등 스크립트는 여러 번 실행된 후에도 동일한 효과를 갖는 스크립트입니다.
* 필드의 전역적으로 사용 가능한 속성을 사용하여 소극적 로드 패널의 필드 값을 양식의 다른 모든 패널에서 사용할 수 있도록 합니다.
* 필드가 조각 간에 전역적으로 표시되는지 여부에 관계없이 레이지 패널 내의 필드 참조 값을 전달하지 마십시오.
* 다음 클릭 표현식을 사용하여 패널에 표시되는 모든 것을 재설정하려면 패널 재설정 기능을 사용하십시오.\
  guideBridge.resolveNode(guideBridge.getFocus({&quot;focusOption&quot;: &quot;navigablePanel&quot;}).resetData()
