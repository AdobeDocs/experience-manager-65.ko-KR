---
title: AEM 구성 요소 개발
seo-title: AEM 구성 요소 개발
description: AEM 구성 요소는 웹 페이지에서 사용할 수 있도록 만들어진 컨텐츠를 보류, 형식 지정 및 렌더링하는 데 사용됩니다.
seo-description: AEM 구성 요소는 웹 페이지에서 사용할 수 있도록 만들어진 컨텐츠를 보류, 형식 지정 및 렌더링하는 데 사용됩니다.
uuid: 1f39daa6-7277-45a2-adcc-74b58c93b8e4
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 8cdb6db4-adaa-4eda-af7d-310a0b44b80b
docset: aem65
legacypath: /content/docs/en/aem/6-2/develop/components/components-touch-optimized
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# AEM 구성 요소 개발{#developing-aem-components}

AEM 구성 요소는 웹 페이지에서 사용할 수 있도록 만들어진 컨텐츠를 보류, 형식 지정 및 렌더링하는 데 사용됩니다.

* 페이지를 [작성할](/help/sites-authoring/default-components.md)때 구성 요소를 사용하면 작성자가 컨텐츠를 편집하고 구성할 수 있습니다.

   * 커머스 [사이트를](/help/sites-administering/ecommerce.md) 구성할 때 구성 요소는 카탈로그에서 정보를 수집 및 렌더링할 수 있습니다.
See [Developing eCommerce](/help/sites-developing/ecommerce.md) for more information.

   * 커뮤니티 사이트를 구성할 [때](/help/communities/author-communities.md) 구성 요소는 방문자에게 정보를 제공하고 방문자로부터 정보를 수집할 수 있습니다.
See [Developing Communities](/help/communities/communities.md) for more information.

* 게시 인스턴스에서 구성 요소는 컨텐츠를 렌더링하여 웹 사이트 방문자에게 필요한 만큼 제공합니다.

>[!NOTE]
>
>이 페이지는 문서 AEM 구성 요소 - [기본 사항의 연속입니다](/help/sites-developing/components-basics.md).

>[!CAUTION]
>
>아래 구성 요소는 `/libs/cq/gui/components/authoring/dialog` 편집기에서만 사용됩니다(작성의 구성 요소 대화 상자). 예를 들어 마법사 대화 상에서와 같이 다른 곳에서 사용하는 경우 예상대로 동작하지 않을 수 있습니다.

## 코드 샘플 {#code-samples}

이 페이지에서는 AEM용 새 구성 요소를 개발하는 데 필요한 참조 설명서(또는 참조 설명서에 대한 링크)를 제공합니다. 몇 [가지 실용적인 예는 AEM 구성 요소 개발](/help/sites-developing/developing-components-samples.md) - 코드 샘플을 참조하십시오.

## 구조 {#structure}

구성 요소의 기본 구조는 AEM 구성 요소 - 기본 [페이지에서 다룹니다](/help/sites-developing/components-basics.md#structure). 이 문서는 터치 지원 UI와 클래식 UI를 모두 포함합니다. 새 구성 요소에서 클래식 설정을 사용하지 않아도 기존 구성 요소에서 상속할 때 이를 파악하는 데 도움이 됩니다.

## 기존 구성 요소 및 대화 상자 확장 {#extending-existing-components-and-dialogs}

구현하려는 구성 요소에 따라 전체 [구조를](#structure) 처음부터 정의하고 개발하는 대신 기존 인스턴스를 확장하거나 사용자 지정할 수 있습니다.

기존 구성 요소나 대화 상자를 확장하거나 사용자 정의할 때 변경하기 전에 전체 구조나 대화 상자에 필요한 구조를 복사하거나 복제할 수 있습니다.

### 기존 구성 요소 확장 {#extending-an-existing-component}

기존 구성 요소를 확장하려면 리소스 유형 계층 [및 관련](/help/sites-developing/components-basics.md#component-hierarchy-and-inheritance) 상속 메커니즘을 사용합니다.

>[!NOTE]
>
>검색 경로 로직을 기반으로 오버레이로 구성 요소를 재정의할 수도 있습니다. 그러나 이 경우 Sling [리소스](/help/sites-developing/sling-resource-merger.md) 합병은 트리거되지 않으며 전체 오버레이를 정의해야 `/apps` 합니다.

>[!NOTE]
>
>또한 [컨텐츠 조각 구성 요소를](/help/sites-developing/customizing-content-fragments.md) 사용자 정의하고 확장할 수 있지만 자산과의 전체 구조와 관계를 고려해야 합니다.

### 기존 구성 요소 사용자 정의 대화 상자 {#customizing-a-existing-component-dialog}

또한 Sling Resource Commodification을 사용하여 *구성 요소 대화* 상자를 [재정의하고](/help/sites-developing/sling-resource-merger.md) 속성을 정의할 `sling:resourceSuperType`수있습니다.

즉, 전체 대화 상자 재정의(사용 `sling:resourceSuperType`중)가 아니라 필요한 차이만 재정의해야 합니다. 이제 구성 요소 대화 상자를 확장하는 데 권장되는 방법입니다.

자세한 내용은 [Sling Resource](/help/sites-developing/sling-resource-merger.md) Combination을 참조하십시오.

## 마크업 정의 {#defining-the-markup}

구성 요소는 HTML로 렌더링됩니다 [](https://www.w3schools.com/htmL/html_intro.asp). 구성 요소는 필요한 컨텐츠를 가져온 다음 필요에 따라 작성자 및 게시 환경 모두에서 렌더링하는 데 필요한 HTML을 정의해야 합니다.

### HTML 템플릿 언어 사용 {#using-the-html-template-language}

The [HTML Templating Language (HTL)](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html), introduced with AEM 6.0, takes the place of JSP (JavaServer Pages) as the preferred and recommended server-side template system for HTML. 강력한 엔터프라이즈 웹 사이트를 구축해야 하는 웹 개발자를 위해 HTL을 사용하면 보안 및 개발 효율성을 향상시킬 수 있습니다.

>[!NOTE]
>
>HTL과 JSP는 구성 요소 개발에 모두 사용할 수 있지만, AEM에 권장되는 스크립팅 언어이므로 이 페이지에서 HTL을 사용한 개발을 설명합니다.

## 컨텐츠 논리 개발 {#developing-the-content-logic}

이 선택 로직은 렌더링할 컨텐츠를 선택하거나 계산합니다. 적절한 Use-API 패턴을 사용하여 HTL 표현식에서 호출됩니다.

모양과 로직을 구분하는 메커니즘은 지정된 뷰에 대해 호출된 항목을 확인하는 데 도움이 됩니다. 또한 동일한 리소스의 서로 다른 보기에 대해 다른 논리를 사용할 수도 있습니다.

### Java 사용 {#using-java}

[HTL Java Use-API를 사용하면 HTL 파일에서 사용자 지정 Java 클래스의](https://helpx.adobe.com/experience-manager/htl/using/use-api-java.html)도우미 메서드에 액세스할 수 있습니다. 이렇게 하면 Java 코드를 사용하여 구성 요소 컨텐츠를 선택하고 구성하기 위한 논리를 구현할 수 있습니다.

### JavaScript 사용 {#using-javascript}

[HTL JavaScript Use-API를 사용하면 HTL 파일에서 JavaScript로 작성된 헬퍼 코드에 액세스할 수 있습니다](https://helpx.adobe.com/experience-manager/htl/using/use-api-javascript.html). 이렇게 하면 JavaScript 코드를 사용하여 구성 요소 컨텐츠를 선택하고 구성하기 위한 로직을 구현할 수 있습니다.

### 클라이언트측 HTML 라이브러리 사용 {#using-client-side-html-libraries}

최신 웹 사이트에서는 복잡한 JavaScript 및 CSS 코드를 기반으로 하는 클라이언트측 처리에 크게 의존합니다. 이 코드의 제공을 구성하고 최적화하는 것은 복잡한 문제가 될 수 있습니다.

이 문제를 해결하기 위해 AEM에서는 **클라이언트측 코드를**&#x200B;저장소에 저장하고, 카테고리로 구성하고, 각 코드 카테고리가 클라이언트에 제공될 시기와 방법을 정의할 수 있는 클라이언트측 라이브러리 폴더를 제공합니다. 그런 다음 클라이언트측 라이브러리 시스템은 최종 웹 페이지에서 올바른 링크를 만들어 올바른 코드를 로드합니다.

자세한 [내용은 클라이언트측 HTML 라이브러리](/help/sites-developing/clientlibs.md) 사용을 참조하십시오.

## 편집 동작 구성 {#configuring-the-edit-behavior}

구성 요소에 사용할 수 있는 작업, 즉석 편집기의 특성 및 구성 요소의 이벤트와 관련된 리스너와 같은 속성을 포함하는 구성 요소의 편집 동작을 구성할 수 있습니다. 특정 차이점이 있지만 터치 지원 UI와 클래식 UI에 일반적으로 사용됩니다.

구성 요소의 [편집 비헤이비어는 구성 요소 노드](/help/sites-developing/components-basics.md#edit-behavior) (유형 `cq:editConfig` 아래) 아래에 유형 `cq:EditConfig` 노드를 추가하고 특정 속성과 하위 노드를 추가하여 구성됩니다 `cq:Component`.

## 미리 보기 동작 구성 {#configuring-the-preview-behavior}

WCM [모드](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) 쿠키는 페이지를 새로 고치지 않아도 미리 보기 **모드로** 전환할 때 설정됩니다.

WCM 모드에 민감한 렌더링을 사용하는 구성 요소의 경우 특별히 새로 고친 다음 쿠키의 값을 사용해야 합니다.

>[!NOTE]
>
>터치에 적합한 UI에서는 값만 `EDIT` 사용하고 WCM 모드 `PREVIEW` 쿠키에 [사용됩니다](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) .

## 대화 상자 만들기 및 구성 {#creating-and-configuring-a-dialog}

대화 상자는 작성자가 구성 요소와 상호 작용할 수 있도록 하는 데 사용됩니다. 작성자 및/또는 관리자는 대화 상자를 사용하여 컨텐츠를 편집하거나 구성 요소를 구성하거나 디자인 매개 변수를 정의할 [수 있습니다](#creating-and-configuring-a-design-dialog)

### Coral UI 및 Granite UI {#coral-ui-and-granite-ui}

[Coral UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html) 및 [Granite UI는](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) AEM의 최신 모양과 느낌을 정의합니다.

[[MOCK] Granite UI provides a large range of the basic components (widgets)](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) needed to create your dialog on the authoring environment. 필요한 경우 이 선택 사항을 확장하고 자신만의 위젯을 [만들 수 있습니다](#creatinganewwidget).

Coral 및 Granite 리소스 유형을 사용하는 구성 요소 개발에 대한 자세한 내용은 다음을 참조하십시오.Coral/ [Granite 리소스 유형을](https://helpx.adobe.com/experience-manager/using/aem64_coral_resourcetypes.html)사용하여 Experience Manager 구성 요소를 빌드합니다.

자세한 내용은 다음을 참조하십시오.

* Coral UI

   * 모든 클라우드 솔루션에서 일관된 UI 제공
   * [AEM Touch-Enabled UI 개념 - Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Coral UI 안내서](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html)

* Granite UI

   * UI 콘솔 및 대화 상자 작성을 위해 Sling 구성 요소로 래핑된 Coral UI 마크업을 제공합니다.
   * [AEM Touch-Enabled UI 개념 - Granite UI](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Granite UI 설명서](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)

>[!NOTE]
>
>[MOCK] Due to the nature of the Granite UI components (and differences to the ExtJS widgets), there are some differences between how components interact with the touch-enabled UI and the [classic UI](/help/sites-developing/developing-components-classic.md).

### 새 대화 상자 만들기 {#creating-a-new-dialog}

터치 지원 UI에 대한 대화 상자:

* 에 이름이 `cq:dialog`지정되어 있습니다.
* 는 `nt:unstructured` 속성 세트가 있는 `sling:resourceType` 노드로 정의됩니다.

* 는 해당 노드 아래에 `cq:Component` 있으며 구성 요소 정의 옆에 있습니다.
* 는 컨텐츠 구조와 `sling:resourceType` 속성을 기반으로 서버측(Sling 구성 요소)에서 렌더링됩니다.
* granite UI 프레임워크를 사용합니다.
* 대화 상자 내의 필드를 설명하는 노드 구조를 포함합니다.

   * 이러한 노드에는 `nt:unstructured` 필수 `sling:resourceType` 속성이 있습니다.

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

대화 상자 사용자 지정은 대화 상자 자체가 구성 요소이므로 구성 요소(즉, 클라이언트 라이브러리에서 제공하는 동작/스타일과 함께 구성 요소 스크립트로 렌더링된 마크업)를 개발하는 것과 비슷합니다.

예를 보려면 다음을 참조하십시오.

* `/libs/foundation/components/text/cq:dialog`
* `/libs/foundation/components/download/cq:dialog`

>[!NOTE]
>
>구성 요소에 터치 지원 UI에 대해 정의된 대화 상자가 없는 경우, 클래식 UI 대화 상자는 호환성 레이어 내부의 대비책으로 사용됩니다. 이러한 대화 상자를 사용자 정의하려면 클래식 UI 대화 상자를 사용자 정의해야 합니다. 클래식 [UI용 AEM 구성 요소를 참조하십시오](/help/sites-developing/developing-components-classic.md).

### 대화 상자 필드 사용자 정의 {#customizing-dialog-fields}

>[!NOTE]
>
>다음을 참조하십시오.
>
>* 대화 상자 필드 사용자 [지정에 대한 AEM Gems 세션](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html).
>* 코드 샘플 - [대화 상자 필드 사용자 지정 방법을 다루는 관련 샘플 코드](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields).
>



#### 새 필드 만들기 {#creating-a-new-field}

터치 지원 UI에 대한 위젯은 [granite UI] 구성 요소로 구현됩니다.

터치 지원 UI에 대한 구성 요소 대화 상자에서 사용할 새 위젯을 만들려면 [MOCK] To create a new Granite UI field component [](/help/sites-developing/granite-ui-component.md).

>[!NOTE]
>
>Granite UI에 대한 자세한 내용은 Granite UI [설명서를](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)참조하십시오.

대화 상자를 양식 요소에 대한 간단한 컨테이너로 간주하는 경우 대화 내용의 기본 컨텐츠를 양식 필드로 볼 수도 있습니다. 새 양식 필드를 만들려면 리소스 유형을 만들어야 합니다.이는 새 구성 요소를 만드는 것과 같습니다. 해당 작업을 돕기 위해 [granite UI]는 (사용) `sling:resourceSuperType`

`/libs/granite/ui/components/coral/foundation/form/field`

특히 [화강암 UI]는 대화 상자(또는 보다 일반적으로 [양식에서](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/index.html))에 사용할 수 있는 다양한 필드 구성 요소를 제공합니다.

>[!NOTE]
>
>이는 위젯이 `cq:Widgets` 노드로 표시되는 클래식 UI와 다르며, 각각은 해당 ExtJS 위젯과의 관계를 설정하는 `xtype` 데 특별한 역할을 합니다. 구현 시점에서 이러한 위젯은 ExtJS 프레임워크에 의해 클라이언트측에서 렌더링되었습니다.

리소스 유형을 만든 후에는 방금 소개한 리소스 유형을 `sling:resourceType` 참조하는 속성을 사용하여 대화 상자에 새 노드를 추가하여 필드를 인스턴스화할 수 있습니다.

#### 스타일 및 비헤이비어에 대한 클라이언트 라이브러리 만들기 {#creating-a-client-library-for-style-and-behavior}

구성 요소에 대한 스타일 및 동작을 정의하려면 사용자 지정 CSS/LESS 및 JS를 정의하는 전용 [클라이언트 라이브러리를](/help/sites-developing/clientlibs.md) 만들 수 있습니다.

구성 요소 대화 상자용으로만 클라이언트 라이브러리를 불러오려면(즉, 다른 구성 요소용으로 로드되지 않음) 대화 상자의 속성 `extraClientlibs`*** **을 방금 만든 클라이언트 라이브러리의 카테고리 이름으로 설정해야 합니다. 클라이언트 라이브러리가 매우 크고/또는 필드가 해당 대화 상자에 고유하므로 다른 대화 상자에서는 필요하지 않을 경우 권장됩니다.

모든 대화 상자에 대해 클라이언트 라이브러리를 불러오려면 클라이언트 라이브러리의 category 속성을 로 `cq.authoring.dialog`설정합니다. 모든 대화 상자를 렌더링할 때 기본적으로 포함되는 클라이언트 라이브러리의 카테고리 이름입니다. 클라이언트 라이브러리가 작고/또는 필드가 일반적이며 다른 대화 상자에서 다시 사용할 수 있는 경우 이 작업을 수행하려고 합니다.

예를 보려면 다음을 참조하십시오.

* `cqgems/customizingfield/components/colorpicker/clientlibs`

   * 코드 샘플에서 [제공](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### 필드 확장(상속) {#extending-inheriting-from-a-field}

요구 사항에 따라 다음 중 하나를 수행할 수 있습니다.

* 구성 요소 상속으로 지정된 [granite UI] 필드 확장( `sling:resourceSuperType`)
* 위젯 라이브러리 API(JS/CSS 상속)를 따라 기본 위젯 라이브러리(화강암 UI의 경우 Coral UI)에서 지정된 위젯을 확장합니다.

#### 대화 상자 필드에 액세스 {#access-to-dialog-fields}

또한 렌더링 조건( `rendercondition`)을 사용하여 대화 상자의 특정 탭/필드에 액세스할 수 있는 사용자를 제어할 수 있습니다.예를 들면 다음과 같습니다.

```xml
+ mybutton
  - sling:resourceType = granite/ui/components/coral/foundation/button
  + rendercondition
    - sling:resourceType = myapp/components/renderconditions/group
    - groups = ["administrators"]
```

### 필드 이벤트 처리 {#handling-field-events}

이제 대화 상자 필드에서 이벤트를 처리하는 방법이 사용자 정의 클라이언트 라이브러리의 [리스너와](#listeners-in-a-custom-client-library)함께 수행됩니다. 이는 컨텐츠 구조에 [리스너를](#listenersinthecontentstructureclassicui)두는 이전 방식에서 변경된 것입니다.

#### 사용자 지정 클라이언트 라이브러리의 리스너 {#listeners-in-a-custom-client-library}

필드에 논리를 삽입하려면 다음을 수행해야 합니다.

1. 필드를 지정된 CSS 클래스( *후크*)로 표시하십시오.
1. 클라이언트 라이브러리에서 해당 CSS 클래스 이름에 연결된 JS 리스너를 정의합니다. 이렇게 하면 사용자 지정 로직의 범위가 필드로만 지정되고 동일한 유형의 다른 필드에 영향을 주지 않습니다.

이를 위해서는 상호 작용할 기본 위젯 라이브러리에 대해 알아야 합니다. 반응할 [이벤트를 확인하려면 Coral UI 설명서를](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html) 참조하십시오. 이는 이전에 ExtJS를 사용하여 수행해야 했던 프로세스와 매우 유사합니다.해당 위젯의 설명서 페이지를 찾은 다음 해당 이벤트 API의 세부 사항을 확인합니다.

예를 보려면 다음을 참조하십시오.

* `cqgems/customizingfield/components/clientlibs/customizingfield`

   * 코드 샘플에서 [제공](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### 컨텐츠 구조의 리스너 {#listeners-in-the-content-structure}

ExtJS 파섹 터치 지원 UI에서 동일하게 수행되는 것은 JS 리스너 코드(또는 모든 코드)가 더 이상 컨텐츠에 정의되지 않은 것과 다릅니다.

컨텐츠 구조는 의미 구조를 설명합니다.기본 위젯의 특성을 의미하지 않아야 합니다. 컨텐츠 구조에 JS 코드가 없으면 컨텐츠 구조를 변경하지 않고도 구현 세부 사항을 변경할 수 있습니다. 즉, 컨텐츠 구조를 건드리지 않고도 위젯 라이브러리를 변경할 수 있습니다.

### 필드 유효성 검사 {#field-validation}

#### 필수 필드 {#mandatory-field}

지정된 필드를 필수로 표시하려면 필드의 컨텐츠 노드에서 다음 속성을 설정합니다.

* 이름: `required`
* 유형: `Boolean`

예를 보려면 다음을 참조하십시오.

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title
```

#### 필드 유효성 검사(Granite UI) {#field-validation-granite-ui}

[MOCK] Field validation in Granite UI and the Granite UI Components (equivalent to widget), is done by using the API `foundation-validation` . [자세한 내용은 `foundation-valdiation` Granite 설명서를 참조하십시오.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/clientlibs/foundation/js/validation/index.html)

예를 보려면 다음을 참조하십시오.

* `cqgems/customizingfield/components/clientlibs/customizingfield/js/validations.js`

   * 코드 샘플에서 [제공](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `/libs/cq/gui/components/authoring/dialog/clientlibs/dialog/js/validations.js`

## 디자인 대화 상자 만들기 및 구성 {#creating-and-configuring-a-design-dialog}

디자인 대화 상자는 구성 요소에 디자인 모드에서 편집할 수 있는 디자인 세부 사항이 있을 때 [제공됩니다](/help/sites-authoring/default-components-designmode.md).

이 정의는 컨텐츠를 [편집하는 데 사용되는](#creating-a-new-dialog)대화 상자의 정의와 매우 유사하며, 이 정의 값은 노드로 정의되어 있다는 것과 다릅니다.

* Node name: `cq:design_dialog`
* 유형: `nt:unstructured`

## 즉석 편집기 만들기 및 구성 {#creating-and-configuring-an-inplace-editor}

즉석 편집기를 사용하면 대화 상자를 열지 않고도 단락 흐름에서 바로 컨텐츠를 편집할 수 있습니다. 예를 들어 표준 텍스트 및 제목 구성 요소에는 모두 즉석 편집기가 있습니다.

즉석 편집기는 모든 구성 요소 유형에 필요하지 않거나 의미가 없습니다.

자세한 [내용은 페이지 작성 확장 - 새 즉석 편집기](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor) 추가를 참조하십시오.

## 구성 요소 도구 모음 사용자 정의 {#customizing-the-component-toolbar}

구성 [요소](/help/sites-developing/touch-ui-structure.md#component-toolbar) 도구 모음에서는 편집, 구성, 복사 및 삭제와 같은 구성 요소에 대한 작업 범위에 액세스할 수 있습니다.

자세한 [내용은 페이지 작성 확장 - 구성 요소 도구 모음에 새 작업](/help/sites-developing/customizing-page-authoring-touch.md#add-new-action-to-a-component-toolbar) 추가를 참조하십시오.

## 참조 레일에 대한 구성 요소 구성(차입/대여) {#configuring-a-component-for-the-references-rail-borrowed-lent}

새 구성 요소가 다른 페이지의 컨텐츠를 참조하는 경우 참조 레일의 **빌린 컨텐츠** 및 **대여된 컨텐츠** 섹션에 영향을 주는지 [**여부를&#x200B;**](/help/sites-authoring/basic-handling.md#references)고려할 수있습니다.

기본 AEM은 참조 구성 요소만 확인합니다. 구성 요소를 추가하려면 OSGi 번들 WCM 작성 컨텐츠 **참조 구성을 구성해야 합니다**.

확인할 속성과 함께 구성 요소를 지정하여 정의에 새 항목을 만듭니다. 예:

`/apps/<*your-Project*>/components/reference@parentPath`

>[!NOTE]
>
>When working with AEM there are several methods of managing the configuration settings for such services. See [Configuring OSGi](/help/sites-deploying/configuring-osgi.md) for more details and the recommended practices.

## 단락 시스템에 구성 요소 활성화 및 추가 {#enabling-and-adding-your-component-to-the-paragraph-system}

구성 요소가 개발되면 해당 단락 시스템에서 사용하도록 설정해야 필요한 페이지에서 사용할 수 있습니다.

이 작업은 다음 중 한 방법으로 수행할 수 있습니다.

* 특정 [페이지를 편집할 때 디자인 모드](/help/sites-authoring/default-components-designmode.md) 사용.
* [템플릿 `components`](/help/sites-developing/components-basics.md#adding-your-component-to-the-paragraph-system)단락 시스템에서 속성 정의

## Configuring a Paragraph System so that Dragging an Asset Creates a Component Instance {#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance}

AEM에서는 사용자가 (적절한) 자산을 페이지의 [](/help/sites-authoring/editing-content.md#insertingacomponenttouchoptimizedui) 인스턴스로 끌면(항상 빈 구성 요소를 페이지로 드래그하지 않아도) 새 구성 요소의 인스턴스가 자동으로 생성되도록 페이지에 단락 시스템을 구성할 수 있는 가능성을 제공합니다.

이 비헤이비어와 필요한 자산 대 구성 요소 관계를 구성할 수 있습니다.

1. 페이지 디자인의 단락 정의 아래 예:

   * `/etc/designs/<myApp>/page/par`
   새 노드 만들기:

   * 이름: `cq:authoring`
   * 유형: `nt:unstructured`


1. 이 아래에서 모든 자산 대 구성 요소 매핑을 저장할 새 노드를 만듭니다.

   * 이름: `assetToComponentMapping`
   * 유형: `nt:unstructured`

1. 각 자산-구성 요소 매핑에 대해 노드를 만듭니다.

   * 이름:text;에셋 및 관련 구성 요소 유형을 나타내는 것이 좋습니다.예를 들어, image
   * 유형: `nt:unstructured`
   각 속성은 다음과 같습니다.

   * `assetGroup`:

      * 유형: `String`
      * 값:관련 자산이 속하는 그룹;예를 들면 `media`
   * `assetMimetype`:

      * 유형: `String`
      * 값:관련 자산의 MIME 유형;for example `image/*`
   * `droptarget`:

      * 유형: `String`
      * 값:드롭 대상;예를 들면 `image`
   * `resourceType`:

      * 유형: `String`
      * 값:관련 구성 요소 리소스;예를 들면 `foundation/components/image`
   * `type`:

      * 유형: `String`
      * 값:유형(예: `Images`






예를 보려면 다음을 참조하십시오.

* `/etc/designs/geometrixx/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-outdoors/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-media/jcr:content/article/article-content-par/cq:authoring`

GITHUB에 대한 코드

GitHub에서 이 페이지의 코드를 찾을 수 있습니다

* [GitHub에서 aem-project-tranype 프로젝트 열기](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)
* 프로젝트를 ZIP [파일로 다운로드](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype/archive/master.zip)

>[!NOTE]
>
>이제 핵심 구성 요소 및 편집 가능한 템플릿을 사용할 때 UI 내에서 구성 요소 인스턴스를 자동으로 만들 [수](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) 있습니다. 지정된 [미디어 유형에 자동으로](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) 연결되는 구성 요소를 정의하는 방법에 대한 자세한 내용은 페이지 템플릿 만들기를 참조하십시오.

## AEM Brackets 확장 사용 {#using-the-aem-brackets-extension}

AEM [Brackets 익스텐션은](/help/sites-developing/aem-brackets.md) AEM 구성 요소 및 클라이언트 라이브러리를 편집하는 매끄러운 워크플로우를 제공합니다. Brackets 코드 [편집기를 기반으로](https://brackets.io/) 합니다.

확장:

* 개발자 효율성을 높이는 데 도움이 되는 간편한 동기화(Maven 또는 File Vault 필요 없음)를 통해 프런트 엔드 개발자는 제한된 AEM 지식을 활용하여 프로젝트에 참여할 수 있습니다.
* 구성 요소 [개발을](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html) 단순화하고 보안을 강화하기 위해 고안된 템플릿 언어인 HTL 지원을 제공합니다.

>[!NOTE]
>
>Brackets는 구성 요소를 만드는 데 권장되는 메커니즘입니다. 클래식 UI용으로 설계된 CRXDE Lite - 구성 요소 만들기 기능을 대체합니다.

## 클래식 구성 요소에서 마이그레이션 {#migrating-from-a-classic-component}

클래식 UI와 함께 사용하도록 디자인된 구성 요소를 터치 지원 UI와 함께 사용할 수 있는 구성 요소로 마이그레이션할 때(전적인 또는 공동) 다음 문제를 고려해야 합니다.

* HTL

   * HTL [을](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html) 사용하는 것은 강제적이지 않지만 구성 요소를 업데이트해야 하는 경우 JSP에서 HTL로 [마이그레이션하는 것을 고려하는 것이 이상적인 시기입니다](/help/sites-developing/components-basics.md#htl-vs-jsp).

* 구성 요소

   * 클래식 UI별 함수를 사용하는 [ `cq:listener`](/help/sites-developing/developing-components.md#migrating-cq-listener-code) 코드 마이그레이션
   * RTE 플러그인. 자세한 내용은 리치 텍스트 [편집기 구성을 참조하십시오](/help/sites-administering/rich-text-editor.md).
   * [클래식 UI와 관련된 함수를 사용하는 `cq:listener` 코드](#migrating-cq-listener-code) 마이그레이션

* 대화 상자

   * 터치가 활성화된 UI에서 사용할 새 대화 상자를 만들어야 합니다. 하지만 호환성을 위해 터치 지원 UI에 대해 대화 상자가 정의되지 않은 경우 터치 지원 UI는 클래식 UI 대화 상자의 정의를 사용할 수 있습니다.
   * 대화 [상자 변환](/help/sites-developing/dialog-conversion.md) 도구가 제공되어 기존 구성 요소를 확장할 수 있습니다.
   * [ExtJS를 Granite UI 구성 요소에 매핑하면](/help/sites-developing/touch-ui-concepts.md#extjs-and-corresponding-granite-ui-components) 동일한 Granite UI 리소스 유형을 사용하는 ExtJS xtype 및 노드 유형에 대한 편리한 개요를 제공합니다.
   * 필드 사용자 지정을 참조하십시오. 자세한 내용은 대화 상자 필드 사용자 [지정에서 AEM Gems 세션을 참조하십시오](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html).
   * Granite UI [유효성 검사로 유형 마이그레이션](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/clientlibs/foundation/js/validation/index.html)
   * JS 리스너를 사용하는 방법에 대한 자세한 내용은 [필드 이벤트](#handling-field-events) 처리 및 대화 상자 필드 사용자 [지정에서의 AEM Gems 세션을](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html)참조하십시오.

### cq:리스너 코드 마이그레이션 {#migrating-cq-listener-code}

클래식 UI용으로 설계된 프로젝트를 마이그레이션하는 경우 코드(및 구성 요소 관련 클라이언트 `cq:listener` `CQ.wcm.*`)가 클래식 UI에 맞는 기능을 사용할 수 있습니다. 마이그레이션의 경우 터치 지원 UI에서 해당 개체/함수를 사용하여 이러한 코드를 업데이트해야 합니다.

프로젝트가 터치 지원 UI로 완전히 마이그레이션되는 경우 터치 지원 UI와 관련된 개체 및 기능을 사용하려면 이러한 코드를 교체해야 합니다.

그러나 마이그레이션 기간(일반적인 시나리오) 동안 프로젝트가 클래식 UI와 터치 지원 UI를 모두 충족해야 하는 경우 적절한 개체를 참조하는 별도의 코드를 구분하기 위해 스위치를 구현해야 합니다.

이 스위치 메커니즘은 다음과 같이 구현할 수 있습니다.

```
if (Granite.author) {
    // touch UI
} else {
    // classic UI
}
```

## 구성 요소 문서 {#documenting-your-component}

개발자는 구성 요소 설명서에 쉽게 액세스하여 다음 사항을 빠르게 이해할 수 있습니다.

* 설명
* 사용 목적
* 컨텐츠 구조 및 속성
* API 및 확장 지점 노출
* 기타

이러한 이유로 구성 요소 자체 내에서 사용 가능한 기존 문서를 마크업하는 것은 매우 쉽습니다.

구성 요소 구조에 `README.md` 파일을 배치하기만 하면 됩니다. 그러면 [구성 요소 콘솔에](/help/sites-authoring/default-components-console.md)이 마크업이 표시됩니다.

![chlimage_1-7](assets/chlimage_1-7.png)

지원되는 마크다운은 [컨텐츠 조각과](/help/assets/content-fragments-markdown.md)동일합니다.
