---
title: AEM 구성 요소 개발
description: AEM 구성 요소는 웹 페이지에서 사용할 수 있는 콘텐츠를 유지하고, 형식을 지정하며, 렌더링하는 데 사용됩니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
docset: aem65
legacypath: /content/docs/en/aem/6-2/develop/components/components-touch-optimized
exl-id: 573cdc36-e9c3-4803-9c4e-cebd0cf0a56f
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '3246'
ht-degree: 0%

---

# AEM 구성 요소 개발{#developing-aem-components}

AEM 구성 요소는 웹 페이지에서 사용할 수 있는 콘텐츠를 유지하고, 형식을 지정하며, 렌더링하는 데 사용됩니다.

* [페이지 작성](/help/sites-authoring/default-components.md)할 때 작성자는 구성 요소를 사용하여 콘텐츠를 편집하고 구성할 수 있습니다.

   * [Commerce](/help/commerce/cif-classic/administering/ecommerce.md) 사이트를 구성할 때 구성 요소는 카탈로그에서 정보를 수집하고 렌더링할 수 있습니다.
자세한 내용은 [전자 상거래 개발](/help/commerce/cif-classic/developing/ecommerce.md)을 참조하십시오.

   * [커뮤니티](/help/communities/author-communities.md) 사이트를 구성할 때 구성 요소가 정보를 제공하고 방문자로부터 정보를 수집할 수 있습니다.
자세한 내용은 [커뮤니티 개발](/help/communities/communities.md)을 참조하십시오.

* 게시 인스턴스에서 구성 요소는 콘텐츠를 렌더링하여 웹 사이트 방문자에게 필요에 따라 표시합니다.

>[!NOTE]
>
>이 페이지는 [AEM 구성 요소 - 기본 사항](/help/sites-developing/components-basics.md) 문서의 연속입니다.

>[!CAUTION]
>
>`/libs/cq/gui/components/authoring/dialog` 아래의 구성 요소는 편집기(작성의 구성 요소 대화 상자)에서만 사용됩니다. 이러한 매개 변수가 다른 곳(예: 마법사 대화 상자)에서 사용되는 경우 예상대로 작동하지 않을 수 있습니다.

## 코드 샘플 {#code-samples}

이 페이지에서는 AEM용 새 구성 요소를 개발하는 데 필요한 참조 설명서(또는 참조 설명서 링크)를 제공합니다. 실제 예제는 [AEM 구성 요소 개발 - 코드 샘플](/help/sites-developing/developing-components-samples.md)을 참조하십시오.

## 구조 {#structure}

구성 요소의 기본 구조는 [AEM 구성 요소 - 기본 사항](/help/sites-developing/components-basics.md#structure) 페이지에서 다룹니다. 이 문서에서는 터치 지원 UI와 클래식 UI를 모두 다룹니다. 새 구성 요소에서 클래식 설정을 사용할 필요가 없는 경우에도 기존 구성 요소에서 상속할 때 클래식 설정을 인식하는 데 도움이 될 수 있습니다.

## 기존 구성 요소 및 대화 상자 확장 {#extending-existing-components-and-dialogs}

구현하려는 구성 요소에 따라 전체 [구조](#structure)를 처음부터 정의하고 개발하는 대신 기존 인스턴스를 확장하거나 사용자 지정하는 것이 가능할 수 있습니다.

기존 구성 요소나 대화 상자를 확장하거나 사용자 정의할 때, 변경하기 전에 대화 상자에 필요한 구조 또는 전체 구조를 복사하거나 복제할 수 있습니다.

### 기존 구성 요소 확장 {#extending-an-existing-component}

[리소스 유형 계층 구조](/help/sites-developing/components-basics.md#component-hierarchy-and-inheritance) 및 관련 상속 메커니즘을 통해 기존 구성 요소를 확장할 수 있습니다.

>[!NOTE]
>
>검색 경로 논리를 기반으로 오버레이를 사용하여 구성 요소를 다시 정의할 수도 있습니다. 그러나 이 경우 [Sling 리소스 병합](/help/sites-developing/sling-resource-merger.md)이 트리거되지 않으며 `/apps`에서 전체 오버레이를 정의해야 합니다.

>[!NOTE]
>
>[콘텐츠 조각 구성 요소](/help/sites-developing/customizing-content-fragments.md)를 사용자 지정하고 확장할 수도 있지만 Assets과의 전체 구조와 관계를 고려해야 합니다.

### 기존 구성 요소 맞춤화 대화 상자 {#customizing-a-existing-component-dialog}

[Sling 리소스 병합](/help/sites-developing/sling-resource-merger.md)을 사용하고 `sling:resourceSuperType` 속성을 정의하는 *구성 요소 대화 상자*&#x200B;을(를) 재정의할 수도 있습니다.

즉, `sling:resourceSuperType`을(를) 사용하여 전체 대화 상자를 다시 정의하는 대신 필요한 차이점만 다시 정의하면 됩니다. 이제 구성 요소 대화 상자를 확장하는 데 권장되는 방법입니다

자세한 내용은 [Sling 리소스 병합](/help/sites-developing/sling-resource-merger.md)을 참조하십시오.

## 마크업 정의 {#defining-the-markup}

구성 요소가 [HTML](https://www.w3schools.com/htmL/html_intro.asp)(으)로 렌더링됩니다. 구성 요소는 작성자와 게시 환경 모두에서 필요한 콘텐츠를 가져온 다음 필요에 따라 렌더링하는 데 필요한 HTML을 정의해야 합니다.

### HTML 템플릿 언어 사용 {#using-the-html-template-language}

AEM 6.0과 함께 도입된 [HTML 템플릿 언어(HTL)](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=ko)는 HTML을 위한 기본 및 권장 서버측 템플릿 시스템으로 JSP(JavaServer Pages)를 대신합니다. 강력한 엔터프라이즈 웹 사이트를 구축해야 하는 웹 개발자에게 HTL은 향상된 보안 및 개발 효율성을 제공하는 데 도움이 됩니다.

>[!NOTE]
>
>HTL과 JSP는 모두 구성 요소 개발에 사용할 수 있지만 AEM에 권장되는 스크립팅 언어이므로 이 페이지에서는 HTL의 개발에 대해 설명하겠습니다.

## 콘텐츠 논리 개발 {#developing-the-content-logic}

이 선택적 로직은 렌더링할 콘텐츠를 선택 및/또는 계산합니다. 적절한 Use-API 패턴을 사용하여 HTL 표현식에서 호출됩니다.

논리를 외형과 분리하는 메커니즘은 주어진 견해에 대해 호출되는 것을 명확히 하는 데 도움이 된다. 또한 동일한 리소스의 다른 보기에 대해 다른 논리를 사용할 수 있습니다.

### Java 사용 {#using-java}

[HTL Java Use-API를 사용하면 HTL 파일이 사용자 지정 Java 클래스의 도우미 메서드에 액세스할 수 있습니다](https://experienceleague.adobe.com/docs/experience-manager-htl/content/java-use-api.html?lang=ko). 이렇게 하면 Java 코드를 사용하여 구성 요소 콘텐츠를 선택하고 구성하기 위한 논리를 구현할 수 있습니다.

### JavaScript 사용 {#using-javascript}

[HTL JavaScript Use-API를 사용하면 HTL 파일이 JavaScript에서 작성된 도우미 코드에 액세스할 수 있습니다](https://experienceleague.adobe.com/docs/experience-manager-htl/content/java-use-api.html?lang=ko). 이렇게 하면 JavaScript 코드를 사용하여 구성 요소 콘텐츠를 선택하고 구성하는 논리를 구현할 수 있습니다.

### 클라이언트측 HTML 라이브러리 사용 {#using-client-side-html-libraries}

최신 웹 사이트는 복잡한 JavaScript 및 CSS 코드로 구동되는 클라이언트측 처리에 크게 의존합니다. 이 코드의 제공을 구성하고 최적화하는 것은 복잡한 문제가 될 수 있습니다.

이 문제를 해결하기 위해 AEM에서는 클라이언트측 코드를 저장소에 저장하고, 범주로 구성하고, 각 코드 범주가 클라이언트에 제공되는 시기와 방법을 정의할 수 있는 **클라이언트측 라이브러리 폴더**&#x200B;를 제공합니다. 그런 다음 클라이언트측 라이브러리 시스템은 올바른 코드를 로드하기 위해 최종 웹 페이지에서 올바른 링크를 생성합니다.

자세한 내용은 [클라이언트측 HTML 라이브러리 사용](/help/sites-developing/clientlibs.md)을 참조하십시오.

## 비헤이비어 편집 구성 {#configuring-the-edit-behavior}

구성 요소에 사용할 수 있는 작업, 즉석 편집기의 특성, 구성 요소의 이벤트와 관련된 리스너와 같은 속성을 포함하여 구성 요소의 편집 동작을 구성할 수 있습니다. 이 구성은 터치 지원 UI와 클래식 UI에 공통되지만, 특정 차이점이 있습니다.

`cq:Component` 형식의 구성 요소 노드 아래에 `cq:EditConfig` 형식의 `cq:editConfig` 노드를 추가하고 특정 속성 및 자식 노드를 추가하여 구성 요소의 [편집 동작이 구성](/help/sites-developing/components-basics.md#edit-behavior)됩니다.

## 미리 보기 동작 구성 {#configuring-the-preview-behavior}

[WCM 모드](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html) 쿠키는 페이지를 새로 고치지 않은 경우에도 **미리 보기** 모드로 전환할 때 설정됩니다.

렌더링이 WCM 모드에 민감한 구성 요소의 경우, 특별히 자신을 새로 고치도록 정의한 다음 쿠키 값을 사용해야 합니다.

>[!NOTE]
>
>터치 사용 UI에서 값 `EDIT` 및 `PREVIEW`만 [WCM 모드](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html) 쿠키에 사용됩니다.

## 대화 상자 만들기 및 구성 {#creating-and-configuring-a-dialog}

대화 상자는 작성자가 구성 요소와 상호 작용할 수 있도록 하는 데 사용됩니다. 대화 상자를 사용하면 작성자 및/또는 관리자가 콘텐츠를 편집하거나 구성 요소를 구성하거나 디자인 매개 변수를 정의할 수 있습니다([디자인 대화 상자](#creating-and-configuring-a-design-dialog) 사용).

### Coral UI 및 Granite UI {#coral-ui-and-granite-ui}

[Coral UI](https://developer.adobe.com/experience-manager/reference-materials/6-5/coral-ui/coralui3/index.html) 및 [Granite UI](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)은(는) AEM의 현대적인 모양과 느낌을 정의합니다.

[Granite UI는 작성 환경에서 대화 상자를 만드는 데 필요한 다양한 기본 구성 요소(위젯)를 제공합니다](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html). 필요한 경우 이 선택 항목을 확장하고 [고유한 위젯을 만들 수 있습니다](#creatinganewwidget).

자세한 내용은 다음을 참조하십시오.

* Coral UI

   * 모든 클라우드 솔루션에서 일관된 UI 제공
   * [AEM 터치 지원 UI의 개념 - Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Coral UI 안내서](https://developer.adobe.com/experience-manager/reference-materials/6-5/coral-ui/coralui3/index.html)

* Granite UI

   * UI 콘솔 및 대화 상자를 작성하기 위해 Sling 구성 요소에 래핑된 Coral UI 마크업을 제공합니다
   * [AEM 터치 지원 UI - Granite UI의 개념](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Granite UI 설명서](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)

>[!NOTE]
>
>Granite UI 구성 요소의 특성(및 ExtJS 위젯의 차이점)으로 인해 구성 요소가 터치 지원 UI와 [클래식 UI](/help/sites-developing/developing-components-classic.md)와 상호 작용하는 방법에는 몇 가지 차이점이 있습니다.

### 새 대화 상자 만들기 {#creating-a-new-dialog}

터치 지원 UI에 대한 대화 상자:

* 이름이 `cq:dialog`입니다.
* `sling:resourceType` 속성이 설정된 `nt:unstructured` 노드로 정의되어 있습니다.

* 은(는) 해당 `cq:Component` 노드 아래와 구성 요소 정의 옆에 있습니다.
* 콘텐츠 구조 및 `sling:resourceType` 속성에 따라 서버측에서 Sling 구성 요소로 렌더링됩니다.
* granite UI 프레임워크를 사용합니다.
* 대화 상자 내의 필드를 설명하는 노드 구조를 포함합니다.

   * 이 노드는 필수 `sling:resourceType` 속성이 있는 `nt:unstructured`입니다.

노드 구조의 예는 다음과 같습니다.

```xml
newComponent (cq:Component)
  cq:dialog (nt:unstructured)
    content
      layout
      items
        column
          items
            file
            description
```

대화 상자를 사용자 정의하는 것은 대화 상자 자체가 구성 요소이므로 구성 요소를 개발하는 것과 비슷합니다(즉, 클라이언트 라이브러리에서 제공하는 동작/스타일과 함께 구성 요소 스크립트에 의해 렌더링된 마크업).

예를 보려면 다음을 참조하십시오.

* `/libs/foundation/components/text/cq:dialog`
* `/libs/foundation/components/download/cq:dialog`

>[!NOTE]
>
>구성 요소에 터치 사용 UI에 대해 정의된 대화 상자가 없는 경우 클래식 UI 대화 상자는 호환성 레이어 내에서 대체 항목으로 사용됩니다. 이러한 대화 상자를 사용자 정의하려면 클래식 UI 대화 상자를 사용자 정의해야 합니다. 클래식 UI에 대한 [AEM 구성 요소](/help/sites-developing/developing-components-classic.md)를 참조하십시오.

### 대화 상자 필드 사용자 지정 {#customizing-dialog-fields}

>[!NOTE]
>
>다음을 참조하십시오.
>
>* [대화 상자 필드 사용자 지정](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-customizing-dialog-fields-in-touch-ui.html?lang=ko)의 AEM Gems 세션.
>* [코드 샘플 - 대화 상자 필드를 사용자 지정하는 방법](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)에서 다루는 관련 샘플 코드.
>

#### 새 필드 만들기 {#creating-a-new-field}

터치 지원 UI에 대한 위젯은 Granite UI 구성 요소로 구현됩니다.

터치 사용 UI의 구성 요소 대화 상자에서 사용할 위젯을 만들려면 [Granite UI 필드 구성 요소를 만들어야](/help/sites-developing/granite-ui-component.md) 합니다.

>[!NOTE]
>
>Granite UI에 대한 자세한 내용은 [Granite UI 설명서](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)를 참조하십시오.

대화 상자를 양식 요소의 간단한 컨테이너로 간주하면 대화 상자 콘텐츠의 기본 콘텐츠도 양식 필드로 볼 수 있습니다. 양식 필드를 만들려면 리소스 유형을 만들어야 합니다. 이는 구성 요소를 만드는 것과 같습니다. Granite UI는 해당 작업에서 상속할 일반 필드 구성 요소를 제공합니다(`sling:resourceSuperType` 사용).

`/libs/granite/ui/components/coral/foundation/form/field`

특히 Granite UI는 대화 상자(또는 일반적으로 [forms](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/index.html))에서 사용하기에 적합한 다양한 필드 구성 요소를 제공합니다.

>[!NOTE]
>
>이는 위젯이 각각 특정 `xtype`과(와) 함께 `cq:Widgets` 노드로 표시되어 해당 ExtJS 위젯과의 관계를 설정하는 클래식 UI와 다릅니다. 구현 관점에서 이러한 위젯은 ExtJS 프레임워크에 의해 클라이언트측에서 렌더링되었습니다.

리소스 유형을 만든 후에는 대화 상자에서 새 노드를 추가하여 필드를 인스턴스화할 수 있습니다. 속성 `sling:resourceType`은(는) 방금 도입한 리소스 유형을 참조합니다.

#### 스타일 및 비헤이비어를 위한 클라이언트 라이브러리 만들기 {#creating-a-client-library-for-style-and-behavior}

구성 요소의 스타일 및 동작을 정의하려는 경우 사용자 지정 CSS/LESS 및 JS를 정의하는 전용 [클라이언트 라이브러리](/help/sites-developing/clientlibs.md)를 만들 수 있습니다.

구성 요소 대화 상자용으로만 클라이언트 라이브러리를 로드하려면(즉, 다른 구성 요소용으로는 로드되지 않음) 대화 상자의 속성 `extraClientlibs`을(를) 만든 클라이언트 라이브러리의 범주 이름으로 설정해야 합니다. 클라이언트 라이브러리가 상당히 크고/또는 필드가 해당 대화 상자와 관련이 있으며 다른 대화 상자에는 필요하지 않은 경우 이 방법을 사용하는 것이 좋습니다.

모든 대화 상자에 대해 클라이언트 라이브러리를 로드하려면 클라이언트 라이브러리의 category 속성을 `cq.authoring.dialog`(으)로 설정하십시오. 모든 대화 상자를 렌더링할 때 기본적으로 포함되는 클라이언트 라이브러리의 범주 이름입니다. 클라이언트 라이브러리가 작거나 필드가 일반적이고 다른 대화 상자에서 다시 사용할 수 있는 경우 이 작업을 하려고 합니다.

예를 보려면 다음을 참조하십시오.

* `cqgems/customizingfield/components/colorpicker/clientlibs`

   * [코드 샘플](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)에서 제공

#### 필드 확장(상속) {#extending-inheriting-from-a-field}

요구 사항에 따라 다음 중 하나를 수행할 수 있습니다.

* 구성 요소 상속(`sling:resourceSuperType`)으로 주어진 Granite UI 필드 확장
* 위젯 라이브러리 API(JS/CSS 상속)를 따라 기본 위젯 라이브러리(Granite UI가 있는 경우 Coral UI임)에서 주어진 위젯을 확장합니다.

#### 대화 상자 필드 액세스 {#access-to-dialog-fields}

또한 렌더링 조건(`rendercondition`)을 사용하여 대화 상자의 특정 탭/필드에 액세스할 수 있는 사용자를 제어할 수 있습니다. 예:

```xml
+ mybutton
  - sling:resourceType = granite/ui/components/coral/foundation/button
  + rendercondition
    - sling:resourceType = myapp/components/renderconditions/group
    - groups = ["administrators"]
```

### 필드 이벤트 처리 {#handling-field-events}

이제 대화 상자 필드의 이벤트 처리 방법이 사용자 지정 클라이언트 라이브러리의 [리스너](#listeners-in-a-custom-client-library)를 통해 완료되었습니다. 이는 콘텐츠 구조에 [청취자](#listenersinthecontentstructureclassicui)가 있는 이전 메서드의 변경 사항입니다.

#### 사용자 지정 클라이언트 라이브러리의 리스너 {#listeners-in-a-custom-client-library}

필드에 논리를 삽입하려면 다음을 수행해야 합니다.

1. 필드를 지정된 CSS 클래스(*hook*)로 표시하십시오.
1. 클라이언트 라이브러리에서 해당 CSS 클래스 이름에 후크된 JS 수신기를 정의합니다(이렇게 하면 사용자 지정 논리의 범위가 필드에만 지정되며 동일한 유형의 다른 필드에는 영향을 주지 않음).

이를 위해서는 상호 작용하려는 기본 위젯 라이브러리에 대해 알아야 합니다. 반응할 이벤트를 식별하려면 [Coral UI 설명서](https://developer.adobe.com/experience-manager/reference-materials/6-5/coral-ui/coralui3/index.html)를 참조하십시오. 이는 이전에 ExtJS로 수행해야 했던 프로세스와 매우 유사합니다. 특정 위젯의 문서 페이지를 찾은 다음 이벤트 API의 세부 사항을 확인합니다.

예를 보려면 다음을 참조하십시오.

* `cqgems/customizingfield/components/clientlibs/customizingfield`

   * [코드 샘플](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)에서 제공

#### 콘텐츠 구조의 리스너 {#listeners-in-the-content-structure}

ExtJS가 있는 클래식 UI에서는 일반적으로 콘텐츠 구조에 지정된 위젯에 대한 리스너를 보유했습니다. 터치 사용 UI에서 를 구현하는 것은 JS 수신기 코드(또는 모든 코드)가 더 이상 콘텐츠에 정의되지 않음으로써 다릅니다.

콘텐츠 구조는 의미 체계 구조를 설명합니다. 기본 위젯의 특성을 암시해서는 안 됩니다. 콘텐츠 구조에 JS 코드가 없으므로 콘텐츠 구조를 변경하지 않고도 구현 세부 사항을 변경할 수 있습니다. 즉, 콘텐츠 구조를 터치하지 않고도 위젯 라이브러리를 변경할 수 있습니다.

#### 대화 상자의 사용 가능 여부 감지 {#dialog-ready}

대화 상자를 사용할 수 있고 준비가 되었을 때만 실행해야 하는 사용자 지정 JavaScript이 있는 경우 `dialog-ready` 이벤트를 수신해야 합니다.

이 이벤트는 대화 상자가 로드(또는 다시 로드)되고 사용할 준비가 될 때마다 트리거됩니다. 즉, 대화 상자의 DOM에 변경(만들기/업데이트)이 있을 때마다 트리거됩니다.

`dialog-ready`을(를) 사용하여 대화 상자 또는 유사한 작업 내의 필드에 대한 사용자 지정을 수행하는 JavaScript 사용자 지정 코드를 연결할 수 있습니다.

### 필드 유효성 검사 {#field-validation}

#### 필수 필드 {#mandatory-field}

지정된 필드를 필수 항목으로 표시하려면 필드의 콘텐츠 노드에서 다음 속성을 설정합니다.

* 이름: `required`
* 유형: `Boolean`

예를 보려면 다음을 참조하십시오.

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title
```

#### 필드 유효성 검사(Granite UI) {#field-validation-granite-ui}

Granite UI 및 Granite UI 구성 요소(위젯과 동일)의 필드 유효성 검사는 `foundation-validation` API를 사용하여 수행됩니다. [자세한 내용은 `foundation-valdiation` Granite 설명서를 참조하십시오.](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/clientlibs/foundation/js/validation/index.html)

예를 보려면 다음을 참조하십시오.

* `cqgems/customizingfield/components/clientlibs/customizingfield/js/validations.js`

   * [코드 샘플](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)에서 제공

* `/libs/cq/gui/components/authoring/dialog/clientlibs/dialog/js/validations.js`

## 디자인 대화 상자 만들기 및 구성 {#creating-and-configuring-a-design-dialog}

구성 요소에 [디자인 모드](/help/sites-authoring/default-components-designmode.md)에서 편집할 수 있는 디자인 세부 정보가 있으면 디자인 대화 상자가 제공됩니다.

정의는 [콘텐츠 편집에 사용되는 대화 상자](#creating-a-new-dialog)와(과) 매우 유사하지만, 다른 점은 노드로 정의된다는 것입니다.

* 노드 이름: `cq:design_dialog`
* 유형: `nt:unstructured`

## 즉석 편집기 만들기 및 구성 {#creating-and-configuring-an-inplace-editor}

즉석 편집기를 사용하면 대화 상자를 열지 않고도 단락 흐름에서 직접 콘텐츠를 편집할 수 있습니다. 예를 들어 표준 텍스트 및 제목 구성 요소에는 모두 즉석 편집기가 있습니다.

즉석 편집기는 모든 구성 요소 유형에 필요/의미가 없습니다.

자세한 내용은 [페이지 작성 확장 - 새 즉석 편집기 추가](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor)를 참조하십시오.

## 구성 요소 도구 모음 맞춤화 {#customizing-the-component-toolbar}

[구성 요소 도구 모음](/help/sites-developing/touch-ui-structure.md#component-toolbar)을(를) 통해 사용자는 구성 요소에 대한 편집, 구성, 복사, 삭제와 같은 다양한 작업에 액세스할 수 있습니다.

자세한 내용은 [페이지 작성 확장 - 구성 요소 도구 모음에 새 작업 추가](/help/sites-developing/customizing-page-authoring-touch.md#add-new-action-to-a-component-toolbar)를 참조하십시오.

## 참조 레일에 대한 구성 요소 구성(빌린/빌려준) {#configuring-a-component-for-the-references-rail-borrowed-lent}

새 구성 요소가 다른 페이지의 콘텐츠를 참조하는 경우 [**참조**](/help/sites-authoring/basic-handling.md#references) 레일의 **빌려 콘텐츠** 및 **빌려준 콘텐츠** 섹션에 영향을 미치는지 여부를 고려할 수 있습니다.

기본 AEM에서는 참조 구성 요소만 확인합니다. 구성 요소를 추가하려면 OSGi 번들 **WCM 작성 콘텐츠 참조 구성**&#x200B;을 구성해야 합니다.

확인할 속성과 함께 구성 요소를 지정하여 정의에 항목을 만듭니다. 예:

`/apps/<*your-Project*>/components/reference@parentPath`

>[!NOTE]
>
>AEM을 사용하여 작업할 때 이러한 서비스에 대한 구성 설정을 관리하는 방법에는 몇 가지가 있습니다. 자세한 내용 및 권장 사례를 보려면 [OSGi 구성](/help/sites-deploying/configuring-osgi.md)을 참조하십시오.

## 단락 시스템에 구성 요소 활성화 및 추가 {#enabling-and-adding-your-component-to-the-paragraph-system}

구성 요소가 개발되면 적절한 단락 시스템에서 사용할 수 있도록 활성화해야 하므로 필요한 페이지에서 사용할 수 있습니다.

다음 중 하나를 통해 이 작업을 수행할 수 있습니다.

* 특정 페이지를 편집할 때 [디자인 모드](/help/sites-authoring/default-components-designmode.md)를 사용합니다.
* [템플릿의 단락 시스템에서 `components` 속성을 정의](/help/sites-developing/components-basics.md#adding-your-component-to-the-paragraph-system).

## 자산을 드래그하여 구성 요소 인스턴스를 만들도록 단락 시스템 구성 {#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance}

AEM에서는 사용자가 (적절한) 에셋을 [&#128279;](/help/sites-authoring/editing-content.md#insertingacomponenttouchoptimizedui)의 인스턴스로 드래그할 때(항상 빈 구성 요소를 페이지로 드래그할 필요 없이) 새 구성 요소의 인스턴스가 자동으로 만들어지도록 페이지에서 단락 시스템을 구성할 수 있습니다.

이 동작과 필요한 에셋-구성 요소 관계를 구성할 수 있습니다.

1. 페이지 디자인의 단락 정의 아래에 있습니다. 예:

   * `/etc/designs/<myApp>/page/par`

   노드 만들기:

   * 이름: `cq:authoring`
   * 유형: `nt:unstructured`

1. 이 아래에서 모든 자산-구성 요소 매핑을 보유할 노드를 만듭니다.

   * 이름: `assetToComponentMapping`
   * 유형: `nt:unstructured`

1. 각 에셋-구성 요소 매핑에 대해 노드를 만듭니다.

   * 이름: 텍스트. 이름은 에셋 및 관련 구성 요소 유형(예: 이미지)을 나타내는 것이 좋습니다
   * 유형: `nt:unstructured`

   각각 다음 속성을 갖습니다.

   * `assetGroup`:

      * 유형: `String`
      * 값: 관련 자산이 속한 그룹(예: `media`)

   * `assetMimetype`:

      * 유형: `String`
      * 값: 관련 에셋의 MIME 유형(예: `image/*`)

   * `droptarget`:

      * 유형: `String`
      * 값: 드롭 대상(예: `image`)

   * `resourceType`:

      * 유형: `String`
      * 값: 관련 구성 요소 리소스(예: `foundation/components/image`)

   * `type`:

      * 유형: `String`
      * 값: 형식(예: `Images`)

예를 보려면 다음을 참조하십시오.

* `/etc/designs/geometrixx/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-outdoors/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-media/jcr:content/article/article-content-par/cq:authoring`

GITHUB의 코드

GitHub에서 이 페이지의 코드를 확인할 수 있습니다

* [GitHub에서 aem-project-archetype 프로젝트 열기](https://github.com/adobe/aem-project-archetype)
* 프로젝트를 [ZIP 파일](https://github.com/adobe/aem-project-archetype/archive/master.zip)(으)로 다운로드

>[!NOTE]
>
>이제 [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ko-KR) 및 편집 가능한 템플릿을 사용할 때 UI 내에서 구성 요소 인스턴스의 자동 만들기를 쉽게 구성할 수 있습니다. 지정된 미디어 유형과 자동으로 연결되는 구성 요소를 정의하는 방법에 대한 자세한 내용은 [페이지 템플릿 만들기](/help/sites-authoring/templates.md#editing-a-template-structure-template-author)를 참조하십시오.

## AEM Brackets 확장 사용 {#using-the-aem-brackets-extension}

[AEM Brackets 확장](/help/sites-developing/aem-brackets.md)은(는) AEM 구성 요소 및 클라이언트 라이브러리를 편집하는 원활한 워크플로를 제공합니다. [Brackets](https://brackets.io/) 코드 편집기를 기반으로 합니다.

확장:

* 동기화를 쉽게 하여(Maven 또는 File Vault 필요 없음) 개발자 효율성을 높이고 AEM 지식이 부족한 프론트엔드 개발자의 프로젝트 참여도 지원합니다.
* 구성 요소 개발을 단순화하고 보안을 강화하기 위해 고안된 템플릿 언어인 일부 [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=ko) 지원을 제공합니다.

>[!NOTE]
>
>구성 요소를 만드는 데 권장되는 메커니즘은 대괄호 입니다. 클래식 UI에 맞게 디자인된 CRXDE Lite - 구성 요소 만들기 기능을 대체합니다.

## 클래식 구성 요소에서 마이그레이션 {#migrating-from-a-classic-component}

클래식 UI와 함께 사용하도록 설계된 구성 요소를 터치 사용 UI와 함께 사용할 수 있는 구성 요소로 마이그레이션할 때(단독으로 또는 공동으로) 다음 문제를 고려해야 합니다.

* HTL

   * [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=ko)을(를) 사용해야 하는 것은 아니지만 구성 요소를 업데이트해야 하는 경우 [JSP에서 HTL로 마이그레이션](/help/sites-developing/components-basics.md#htl-vs-jsp)하는 것이 좋습니다.

* 구성 요소

   * 클래식 UI 관련 함수를 사용하는 [`cq:listener`](/help/sites-developing/developing-components.md#migrating-cq-listener-code) 코드 마이그레이션
   * RTE 플러그인입니다. 자세한 내용은 [리치 텍스트 편집기 구성](/help/sites-administering/rich-text-editor.md)을 참조하십시오.
   * 클래식 UI와 관련된 함수를 사용하는 [`cq:listener` 코드 마이그레이션](#migrating-cq-listener-code)

* 대화 상자

   * 터치 지원 UI에서 사용할 대화 상자를 만듭니다. 그러나 호환성을 위해 터치 지원 UI에 대한 대화 상자가 정의되지 않은 경우 터치 지원 UI는 클래식 UI 대화 상자 정의를 사용할 수 있습니다.
   * 기존 구성 요소를 확장하는 데 도움이 되는 [AEM 현대화 도구](/help/sites-developing/modernization-tools.md)가 제공됩니다.
   * [Granite UI 구성 요소에 ExtJS 매핑](/help/sites-developing/touch-ui-concepts.md#extjs-and-corresponding-granite-ui-components)은(는) ExtJS xtype 및 노드 유형과 동일한 Granite UI 리소스 유형에 대한 편리한 개요를 제공합니다.
   * 필드 사용자 지정. 자세한 내용은 [대화 상자 필드 사용자 지정](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-customizing-dialog-fields-in-touch-ui.html?lang=ko)에서 AEM Gems 세션을 참조하십시오.
   * vtypes에서 [Granite UI 유효성 검사](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/clientlibs/foundation/js/validation/index.html)(으)로 마이그레이션
   * JS 수신기를 사용하면 자세한 내용은 [필드 이벤트 처리](#handling-field-events) 및 [대화 상자 필드 사용자 지정](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-customizing-dialog-fields-in-touch-ui.html?lang=ko)의 AEM Gems 세션을 참조하세요.

### cq:listener 코드 마이그레이션 {#migrating-cq-listener-code}

클래식 UI용으로 설계된 프로젝트를 마이그레이션하는 경우 `cq:listener` 코드(및 구성 요소 관련 clientlib)에서 클래식 UI에 고유한 함수(예: `CQ.wcm.*`)를 사용할 수 있습니다. 마이그레이션의 경우 터치 지원 UI에서 이와 동등한 오브젝트/함수를 사용하여 이러한 코드를 업데이트해야 합니다.

프로젝트가 터치 지원 UI로 완전히 마이그레이션되는 경우 터치 지원 UI와 관련된 오브젝트 및 기능을 사용하려면 해당 코드를 교체해야 합니다.

그러나 마이그레이션 기간 동안 프로젝트가 클래식 UI와 터치 지원 UI를 모두 충족해야 하는 경우(일반적인 시나리오) 적절한 개체를 참조하는 개별 코드를 차별화하도록 스위치를 구현해야 합니다.

이 스위치 메커니즘은 다음과 같이 구현될 수 있습니다.

```
if (Granite.author) {
    // touch UI
} else {
    // classic UI
}
```

## 구성 요소 문서화 {#documenting-your-component}

개발자는 다음을 빠르게 이해할 수 있도록 구성 요소 설명서에 쉽게 액세스하려고 합니다.

* 설명
* 의도한 사용
* 컨텐츠 구조 및 속성
* 노출된 API 및 확장 지점
* 기타

따라서 구성 요소 자체 내에서 사용할 수 있는 기존 설명서 Markdown을 쉽게 만들 수 있습니다.

구성 요소 구조에 `README.md` 파일을 배치합니다. 이 Markdown은 [구성 요소 콘솔](/help/sites-authoring/default-components-console.md)에 표시됩니다.

![chlimage_1-7](assets/chlimage_1-7.png)

지원되는 Markdown은 [콘텐츠 조각](/help/assets/content-fragments/content-fragments-markdown.md)의 Markdown과 동일합니다.
