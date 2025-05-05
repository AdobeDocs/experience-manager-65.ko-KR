---
title: 적응형 양식의 레이아웃 기능
description: 다양한 디바이스에서 적응형 양식의 레이아웃 및 모습은 레이아웃 설정의 적용을 받습니다. 다양한 레이아웃과 적용 방법을 이해합니다.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
feature: Adaptive Forms,Foundation Components
discoiquuid: 9459c414-eac9-4bd9-a773-cceaeb736c56
docset: aem65
exl-id: 3db623a4-f1ad-4b7f-97e8-0be138aa8b26
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1193'
ht-degree: 5%

---

# 적응형 양식의 레이아웃 기능{#layout-capabilities-of-adaptive-forms}

<span class="preview"> [새 적응형 양식 만들기](/help/forms/using/create-an-adaptive-form-core-components.md) 또는 [AEM Sites 페이지에 적응형 양식 추가](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) 작업을 할 때 현대적이고 확장 가능한 데이터 캡처 [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ko)를 사용하는 것이 좋습니다. 이러한 구성 요소는 적응형 양식 만들기 작업이 대폭 개선되어 우수한 사용자 경험을 보장할 수 있게 되었음을 나타냅니다. 이 문서에서는 기초 구성 요소를 사용하여 적응형 양식을 작성하는 이전 접근법에 대해 설명합니다. </span>

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-layout-of-an-adaptive-form/layout-capabilities-adaptive-forms.html?lang=ko) |
| AEM 6.5 | 이 문서 |


Adobe Experience Manager(AEM)를 사용하면 최종 사용자에게 동적 경험을 제공하는 사용하기 쉬운 적응형 양식을 만들 수 있습니다. 양식 레이아웃은 항목 또는 구성 요소가 적응형 양식에 표시되는 방식을 제어합니다.

## 전제 조건 지식 {#prerequisite-knowledge}

적응형 양식의 다양한 레이아웃 기능에 대해 알아보려면 다음 문서를 참조하여 적응형 양식에 대해 자세히 알아보십시오.

[AEM Forms 소개](../../forms/using/introduction-aem-forms.md)

[작성 양식 소개](../../forms/using/introduction-forms-authoring.md)

## 레이아웃 유형 {#types-of-layouts}

적응형 양식은 다음과 같은 유형의 레이아웃을 제공합니다.

**패널 레이아웃** 패널 내의 항목 또는 구성 요소가 장치에 표시되는 방식을 제어합니다.

**모바일 레이아웃** 모바일 장치에서 양식 탐색을 제어합니다. 디바이스 너비가 768픽셀 이상인 경우, 레이아웃은 모바일 레이아웃으로 간주되고 모바일 디바이스에 최적화된다.

**도구 모음 레이아웃** 폼에서 도구 모음이나 패널 도구 모음의 작업 단추 배치를 제어합니다.

이러한 패널 레이아웃은 모두 다음 위치에 정의되어 있습니다.

`/libs/fd/af/layouts`

>[!NOTE]
>
>적응형 양식의 레이아웃을 변경하려면 AEM에서 작성 모드를 사용하십시오.

![CRX 저장소의 레이아웃 위치](assets/layouts_location_in_crx.png)

## 패널 레이아웃 {#panel-layout}

양식 작성자는 레이아웃을 루트 패널을 포함하여 적응형 양식의 각 패널과 연결할 수 있습니다.

패널 레이아웃은 `/libs/fd/af/layouts/panel` 위치에서 사용할 수 있습니다.

![적응형 양식의 루트 패널에 대한 패널 레이아웃 목록](assets/layouts.png)

적응형 양식의 패널 레이아웃 목록

### 반응형 - 탐색 없이 한 페이지에 모두 표시 {#responsive-everything-on-one-page-without-navigation-br}

이 패널 레이아웃을 사용하여 전문 탐색을 수행하지 않고도 디바이스의 화면 크기에 맞게 조정되는 응답형 레이아웃을 만들 수 있습니다.

이 레이아웃을 사용하면 패널 내부에 여러 **[!UICONTROL 패널 적응형 양식]** 구성 요소를 차례로 배치할 수 있습니다.

![작은 화면에 표시된 응답형 레이아웃을 사용하는 양식입니다](assets/responsive_layout_seen_on_small_screen.png)

반응형 레이아웃을 사용하는 양식입니다(작은 화면에 표시됨).

![반응형 레이아웃을 사용하는 양식이 큰 화면에 표시됨](assets/responsive_layout_seen_on_large_screen.png)

큰 화면에 표시된 것처럼 응답형 레이아웃을 사용하는 양식입니다.

### 마법사 - 한 번에 한 단계씩 표시되는 여러 단계 양식 {#wizard-a-multi-step-form-showing-one-step-at-a-time}

이 패널 레이아웃을 사용하여 양식 내에서 안내식 탐색을 제공할 수 있습니다. 예를 들어 사용자를 단계별로 안내하면서 양식의 필수 정보를 캡처하려는 경우 이 레이아웃을 사용하십시오.

`Panel adaptive form` 구성 요소를 사용하여 패널 내에서 단계별로 탐색할 수 있습니다. 이 레이아웃을 사용하는 경우 사용자는 현재 단계가 완료된 후에만 다음 단계로 이동합니다

```javascript
window.guideBridge.validate([], this.panel.navigationContext.currentItem.somExpression)
```

![마법사 레이아웃에서 여러 단계 양식에 대한 단계 완료 식](assets/layout-sidebar.png)

마법사 레이아웃의 여러 단계 양식에 대한 단계 완료 표현식

![마법사 레이아웃을 사용하는 양식입니다](assets/wizard-layout.png)

마법사를 사용한 양식

### 아코디언 디자인을 위한 레이아웃 {#layout-for-accordion-design}

이 레이아웃을 사용하면 아코디언 스타일 탐색으로 패널에 `Panel adaptive form` 구성 요소를 배치할 수 있습니다. 이 레이아웃을 사용하여 반복 가능한 패널을 만들 수도 있습니다. 반복 가능한 패널을 사용하면 필요에 따라 패널을 동적으로 추가하거나 제거할 수 있습니다. 패널이 반복되는 최소 및 최대 횟수를 정의할 수 있습니다. 또한 패널 항목에 제공된 정보에 따라 패널의 제목을 동적으로 결정할 수 있습니다.

요약 표현식을 사용하여 최소화된 패널의 제목에 최종 사용자가 제공한 값을 표시할 수 있습니다.

![적응형 양식에서 아코디언 레이아웃을 사용하는 반복 가능한 패널](assets/repeatable_panels_using_accordion_layout.png)

아코디언 레이아웃을 사용하여 만든 반복 가능한 패널

### 탭 레이아웃 - 왼쪽에 탭이 나타납니다. {#tabbed-layout-tabs-appear-on-the-left}

이 레이아웃을 사용하면 탭 탐색이 있는 패널에 `Panel adaptive form` 구성 요소를 배치할 수 있습니다. 탭은 패널 콘텐츠의 왼쪽에 배치됩니다.

![탭 레이아웃에서 탭이 왼쪽에 나타납니다](assets/tabbed_layout_left.png)

패널 왼쪽에 표시되는 탭

### 탭 레이아웃 - 맨 위에 탭이 표시됨 {#tabbed-layout-tabs-appear-on-the-top}

이 레이아웃을 사용하면 탭 탐색이 있는 패널에 `Panel adaptive form` 구성 요소를 배치할 수 있습니다. 탭은 패널 콘텐츠의 맨 위에 배치됩니다.

![맨 위에 탭이 있는 적응형 양식의 탭 레이아웃](assets/tabbed_layout_top.png)

패널 상단에 표시되는 탭

## 모바일 레이아웃 {#mobile-layouts}

모바일 레이아웃은 상대적으로 더 작은 화면들로 모바일 디바이스들 상에서 사용자 친화적인 탐색을 허용한다. 모바일 레이아웃에서는 양식 탐색에 탭 스타일이나 마법사 스타일을 사용합니다. 모바일 레이아웃을 적용하면 전체 양식에 대해 단일 레이아웃이 제공됩니다.

이 레이아웃은 탐색 모음과 탐색 메뉴를 사용하여 탐색을 제어합니다. 탐색 표시줄에 양식의 **next** 및 **previous** 탐색 단계를 나타내는 **&lt;** 및 **>** 아이콘이 표시됩니다.

모바일 레이아웃은 `/libs/fd/af/layouts/mobile/` 위치에서 사용할 수 있습니다. 다음 모바일 레이아웃은 기본적으로 적응형 양식에서 사용할 수 있습니다.

![적응형 양식의 모바일 레이아웃 목록](assets/mobile-navigation.png)

적응형 양식의 모바일 레이아웃 목록

모바일 레이아웃을 사용하는 경우 ![aem6forms_form_menu](assets/aem6forms_form_menu.png) 아이콘을 탭하여 다양한 양식 패널에 액세스하는 양식 메뉴를 사용할 수 있습니다.

### 양식 헤더에 패널 제목이 있는 레이아웃 {#layout-with-panel-titles-in-the-form-header}

이름에서 알 수 있듯이 이 레이아웃은 탐색 메뉴 및 탐색 모음과 함께 패널 제목을 표시합니다. 이 레이아웃은 탐색에 다음 및 이전 아이콘도 제공합니다.

![양식 헤더에서 패널 제목을 사용하는 모바일 레이아웃](assets/mobile_layout_with.png)

양식 머리글에 패널 제목이 있는 모바일 레이아웃

### 양식 헤더에 패널 제목이 없는 레이아웃 {#layout-without-panel-titles-in-the-form-header}

이 레이아웃은 이름에서 알 수 있듯이 패널 제목 없이 탐색 메뉴와 탐색 막대만 표시합니다. 이 레이아웃은 탐색에 다음 및 이전 아이콘도 제공합니다.

![양식 머리글에 패널 제목이 없는 모바일 레이아웃](assets/mobile_layout_without.png)

양식 머리글에 패널 제목이 없는 모바일 레이아웃

## 도구 모음 레이아웃 {#toolbar-layouts}

도구 모음 레이아웃은 적응형 양식에 추가하는 모든 작업 버튼의 위치 지정 및 표시를 제어합니다. 레이아웃은 양식 수준 또는 패널 수준에서 추가할 수 있습니다.

![단추 레이아웃을 제어할 적응형 양식의 도구 모음 레이아웃 목록](assets/toolbar-layouts.png)

적응형 양식의 도구 모음 레이아웃 목록

`/libs/fd/af/layouts/toolbar` 위치에서 도구 모음 레이아웃을 사용할 수 있습니다. 적응형 양식은 기본적으로 다음과 같은 도구 모음 레이아웃을 제공합니다.

### 도구 모음의 기본 레이아웃 {#default-layout-for-toolbar}

이 레이아웃은 적응형 양식에 작업 단추를 추가할 때 기본 레이아웃으로 선택됩니다. 이 레이아웃을 선택하면 데스크탑 장치와 모바일 장치 모두에 대해 동일한 레이아웃이 표시됩니다.

또한 이 레이아웃으로 구성된 작업 단추가 포함된 여러 도구 모음을 추가할 수 있습니다. 작업 단추는 양식 컨트롤과 연결되어 있습니다. 도구 모음을 패널 앞 또는 뒤로 구성할 수 있습니다.

![도구 모음의 기본 보기](assets/toolbar_layout_default.png)

도구 모음의 기본 보기

### 도구 모음에 대한 모바일 고정 레이아웃 {#mobile-fixed-layout-for-toolbar}

데스크탑 및 모바일 장치에 대한 대체 레이아웃을 제공하려면 이 레이아웃을 선택하십시오.

데스크탑 레이아웃의 경우 일부 특정 레이블을 사용하여 작업 버튼을 추가할 수 있습니다. 이 레이아웃으로 하나의 도구 모음만 구성할 수 있습니다. 이 레이아웃으로 두 개 이상의 도구 모음을 구성하는 경우 모바일 장치에 대해 겹치면서 도구 모음이 하나만 표시됩니다. 예를 들어, 양식의 맨 아래나 맨 위에 도구 모음이 있거나, 양식의 패널 뒤 또는 앞에 있는 경우

모바일 레이아웃의 경우 아이콘을 사용하여 작업 버튼을 추가할 수 있습니다.

![도구 모음에 대한 모바일 고정 레이아웃](assets/toolbar_layout_mobile_fixed.png)

도구 모음에 대한 모바일 고정 레이아웃
