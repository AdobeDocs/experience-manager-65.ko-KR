---
title: AEM 구성 요소 개발
seo-title: Developing AEM Components
description: AEM 구성 요소는 웹 페이지에서 사용할 수 있는 콘텐츠를 유지하고, 형식을 지정하며, 렌더링하는 데 사용됩니다.
seo-description: AEM components are used to hold, format, and render the content made available on your webpages.
uuid: 1f39daa6-7277-45a2-adcc-74b58c93b8e4
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 8cdb6db4-adaa-4eda-af7d-310a0b44b80b
docset: aem65
legacypath: /content/docs/en/aem/6-2/develop/components/components-touch-optimized
exl-id: 573cdc36-e9c3-4803-9c4e-cebd0cf0a56f
source-git-commit: 823e756f470b0599f7d53a3e08fdf650b4e892d1
workflow-type: tm+mt
source-wordcount: '3454'
ht-degree: 2%

---

# AEM 구성 요소 개발{#developing-aem-components}

AEM 구성 요소는 웹 페이지에서 사용할 수 있는 콘텐츠를 유지하고, 형식을 지정하며, 렌더링하는 데 사용됩니다.

* 날짜 [페이지 작성](/help/sites-authoring/default-components.md), 구성 요소를 사용하여 작성자는 콘텐츠를 편집하고 구성할 수 있습니다.

   * 를 구성할 때 [상거래](/help/commerce/cif-classic/administering/ecommerce.md) 예를 들어 카탈로그에서 정보를 수집하고 렌더링할 수 있는 구성 요소를 사이트화합니다.
다음을 참조하십시오 [eCommerce 개발](/help/commerce/cif-classic/developing/ecommerce.md) 추가 정보.

   * 를 구성할 때 [커뮤니티](/help/communities/author-communities.md) 사이트 구성 요소는 방문자에게 정보를 제공하고 방문자로부터 정보를 수집할 수 있습니다.
다음을 참조하십시오 [개발 커뮤니티](/help/communities/communities.md) 추가 정보.

* 게시 인스턴스에서 구성 요소는 콘텐츠를 렌더링하여 웹 사이트 방문자에게 필요에 따라 표시합니다.

>[!NOTE]
>
>이 페이지는 문서의 연속입니다. [AEM 구성 요소 - 기본 사항](/help/sites-developing/components-basics.md).

>[!CAUTION]
>
>아래 구성 요소 `/libs/cq/gui/components/authoring/dialog` 는 편집기(작성의 구성 요소 대화 상자)에서만 사용됩니다. 이러한 매개 변수가 다른 곳(예: 마법사 대화 상자)에서 사용되는 경우 예상대로 작동하지 않을 수 있습니다.

## 코드 샘플 {#code-samples}

이 페이지에서는 AEM용 새 구성 요소를 개발하는 데 필요한 참조 설명서(또는 참조 설명서 링크)를 제공합니다. 다음을 참조하십시오 [AEM 구성 요소 개발 - 코드 샘플](/help/sites-developing/developing-components-samples.md) 몇 가지 실제적인 예를 들어 보겠습니다.

## 구조 {#structure}

구성 요소의 기본 구조는 페이지에서 다룹니다 [AEM 구성 요소 - 기본 사항](/help/sites-developing/components-basics.md#structure). 이 문서에서는 터치 지원 UI와 클래식 UI를 모두 다룹니다. 새 구성 요소에서 클래식 설정을 사용할 필요가 없는 경우에도 기존 구성 요소에서 상속할 때 클래식 설정을 인식하는 데 도움이 될 수 있습니다.

## 기존 구성 요소 및 대화 상자 확장 {#extending-existing-components-and-dialogs}

구현하려는 구성 요소에 따라 전체를 정의하고 개발하는 대신 기존 인스턴스를 확장하거나 사용자 정의하는 것이 가능할 수 있습니다 [구조](#structure) 처음부터.

기존 구성 요소나 대화 상자를 확장하거나 사용자 정의할 때, 변경하기 전에 대화 상자에 필요한 구조 또는 전체 구조를 복사하거나 복제할 수 있습니다.

### 기존 구성 요소 확장 {#extending-an-existing-component}

기존 구성 요소 확장은 다음을 통해 수행할 수 있습니다. [리소스 유형 계층](/help/sites-developing/components-basics.md#component-hierarchy-and-inheritance) 및 관련 상속 메커니즘.

>[!NOTE]
>
>검색 경로 논리를 기반으로 오버레이를 사용하여 구성 요소를 다시 정의할 수도 있습니다. 그러나 이러한 경우 [Sling 리소스 병합](/help/sites-developing/sling-resource-merger.md) 이(가) 트리거되지 않고 `/apps` 전체 오버레이를 정의해야 합니다.

>[!NOTE]
>
>다음 [콘텐츠 조각 구성 요소](/help/sites-developing/customizing-content-fragments.md) 를 사용자 정의하고 확장할 수도 있지만 Assets와의 전체 구조 및 관계를 고려해야 합니다.

### 기존 구성 요소 맞춤화 대화 상자 {#customizing-a-existing-component-dialog}

다음을 재정의할 수도 있습니다. *구성 요소 대화 상자* 사용 [Sling 리소스 병합](/help/sites-developing/sling-resource-merger.md) 및 속성 정의 `sling:resourceSuperType`.

즉, 전체 대화상자를 다시 정의하는 대신 필요한 차이점만 재정의하면 됩니다(사용) `sling:resourceSuperType`). 이제 구성 요소 대화 상자를 확장하는 데 권장되는 방법입니다

다음을 참조하십시오. [Sling 리소스 병합](/help/sites-developing/sling-resource-merger.md) 을 참조하십시오.

## 마크업 정의 {#defining-the-markup}

구성 요소는 다음으로 렌더링됩니다. [HTML](https://www.w3schools.com/htmL/html_intro.asp). 구성 요소는 작성자와 게시 환경 모두에서 필요한 콘텐츠를 가져온 다음 필요에 따라 렌더링하는 데 필요한 HTML을 정의해야 합니다.

### HTML 템플릿 언어 사용 {#using-the-html-template-language}

다음 [HTML 템플릿 언어(HTL)](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html)AEM 6.0과 함께 도입된 는 HTML을 위한 기본 및 권장 서버측 템플릿 시스템으로서 JSP(JavaServer Pages)를 대신합니다. 강력한 엔터프라이즈 웹 사이트를 구축해야 하는 웹 개발자에게 HTL은 향상된 보안 및 개발 효율성을 제공하는 데 도움이 됩니다.

>[!NOTE]
>
>HTL과 JSP는 모두 구성 요소 개발에 사용할 수 있지만 AEM에 권장되는 스크립팅 언어이므로 이 페이지에서는 HTL의 개발에 대해 설명하겠습니다.

## 콘텐츠 논리 개발 {#developing-the-content-logic}

이 선택적 로직은 렌더링할 콘텐츠를 선택 및/또는 계산합니다. 적절한 Use-API 패턴을 사용하여 HTL 표현식에서 호출됩니다.

논리를 외형과 분리하는 메커니즘은 주어진 견해에 대해 호출되는 것을 명확히 하는 데 도움이 된다. 또한 동일한 리소스의 다른 보기에 대해 다른 논리를 사용할 수 있습니다.

### Java 사용 {#using-java}

[HTL Java Use-API를 사용하면 HTL 파일이 사용자 지정 Java 클래스의 도우미 메서드에 액세스할 수 있습니다](https://experienceleague.adobe.com/docs/experience-manager-htl/content/java-use-api.html?lang=en). 이렇게 하면 Java 코드를 사용하여 구성 요소 콘텐츠를 선택하고 구성하기 위한 논리를 구현할 수 있습니다.

### JavaScript 사용 {#using-javascript}

[HTL JavaScript Use-API를 사용하면 HTL 파일이 JavaScript로 작성된 도우미 코드에 액세스할 수 있습니다](https://experienceleague.adobe.com/docs/experience-manager-htl/content/java-use-api.html?lang=en). 이렇게 하면 JavaScript 코드를 사용하여 구성 요소 콘텐츠를 선택하고 구성하는 논리를 구현할 수 있습니다.

### 클라이언트측 HTML 라이브러리 사용 {#using-client-side-html-libraries}

최신 웹 사이트는 복잡한 JavaScript 및 CSS 코드로 구동되는 클라이언트측 처리에 크게 의존합니다. 이 코드의 제공을 구성하고 최적화하는 것은 복잡한 문제가 될 수 있습니다.

이 문제를 해결하기 위해 AEM은 다음을 제공합니다 **클라이언트 측 라이브러리 폴더**&#x200B;를 사용하면 클라이언트측 코드를 저장소에 저장하고, 카테고리로 구성한 다음 각 코드 카테고리가 클라이언트에 제공되는 시기와 방법을 정의할 수 있습니다. 그런 다음 클라이언트측 라이브러리 시스템은 올바른 코드를 로드하기 위해 최종 웹 페이지에서 올바른 링크를 생성합니다.

읽기 [클라이언트측 HTML 라이브러리 사용](/help/sites-developing/clientlibs.md) 추가 정보.

## 비헤이비어 편집 구성 {#configuring-the-edit-behavior}

구성 요소에 사용할 수 있는 작업, 즉석 편집기의 특성, 구성 요소의 이벤트와 관련된 리스너와 같은 속성을 포함하여 구성 요소의 편집 동작을 구성할 수 있습니다. 이 구성은 터치 지원 UI와 클래식 UI에 공통되지만, 특정 차이점이 있습니다.

다음 [구성 요소의 편집 비헤이비어가 구성되었습니다.](/help/sites-developing/components-basics.md#edit-behavior) 를 추가하여 `cq:editConfig` 유형의 노드 `cq:EditConfig` (유형의) 구성 요소 노드 아래 `cq:Component`) 특정 속성 및 하위 노드를 추가합니다.

## 미리 보기 동작 구성 {#configuring-the-preview-behavior}

다음 [WCM 모드](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html) 쿠키는으로 전환할 때 설정됩니다. **미리 보기** 페이지를 새로 고치지 않는 경우에도 모드 로 전환됩니다.

렌더링이 WCM 모드에 민감한 구성 요소의 경우, 특별히 자신을 새로 고치도록 정의한 다음 쿠키 값을 사용해야 합니다.

>[!NOTE]
>
>터치 활성화 UI에서는 값만 `EDIT` 및 `PREVIEW` 다음에 사용됩니다. [WCM 모드](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html) 쿠키.

## 대화 상자 만들기 및 구성 {#creating-and-configuring-a-dialog}

대화 상자는 작성자가 구성 요소와 상호 작용할 수 있도록 하는 데 사용됩니다. 작성자 및/또는 관리자는 대화 상자를 사용하여 콘텐츠를 편집하고, 구성 요소를 구성하거나 디자인 매개 변수를 정의할 수 있습니다( 사용). [디자인 대화 상자](#creating-and-configuring-a-design-dialog))

### Coral UI 및 Granite UI {#coral-ui-and-granite-ui}

[Coral UI](https://developer.adobe.com/experience-manager/reference-materials/6-5/coral-ui/coralui3/index.html) 및 [Granite UI](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) AEM의 현대적인 모양과 느낌을 정의합니다.

[Granite UI는 다양한 기본 구성 요소(위젯)를 제공합니다](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) 작성 환경에서 대화 상자를 만드는 데 필요합니다. 필요한 경우 이 선택 항목을 확장하고 [나만의 위젯 만들기](#creatinganewwidget).

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
>Granite UI 구성 요소의 특성(및 ExtJS 위젯에 대한 차이점)으로 인해 구성 요소가 터치 지원 UI와 상호 작용하는 방식과 에는 몇 가지 차이점이 있습니다. [클래식 UI](/help/sites-developing/developing-components-classic.md).

### 새 대화 상자 만들기 {#creating-a-new-dialog}

터치 지원 UI에 대한 대화 상자:

* 이름이 지정됨 `cq:dialog`.
* 다음 항목으로 정의됨: `nt:unstructured` 이 있는 노드 `sling:resourceType` 속성 집합.

* 아래에 위치 `cq:Component` 노드 및 구성 요소 정의 옆에 있습니다.
* 는 콘텐츠 구조 및 를 기반으로 하여 서버측에서 Sling 구성 요소로 렌더링됩니다. `sling:resourceType` 속성.
* granite UI 프레임워크를 사용합니다.
* 대화 상자 내의 필드를 설명하는 노드 구조를 포함합니다.

   * 이 노드들은 `nt:unstructured` (필수 포함) `sling:resourceType` 속성.

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
>구성 요소에 터치 사용 UI에 대해 정의된 대화 상자가 없는 경우 클래식 UI 대화 상자는 호환성 레이어 내에서 대체 항목으로 사용됩니다. 이러한 대화 상자를 사용자 정의하려면 클래식 UI 대화 상자를 사용자 정의해야 합니다. 다음을 참조하십시오 [클래식 UI용 AEM 구성 요소](/help/sites-developing/developing-components-classic.md).

### 대화 상자 필드 사용자 지정 {#customizing-dialog-fields}

>[!NOTE]
>
>다음을 참조하십시오.
>
>* 의 AEM Gems 세션 [대화 상자 필드 사용자 지정](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-customizing-dialog-fields-in-touch-ui.html?lang=en).
>* 관련 샘플 코드는에서 다룹니다 [코드 샘플 - 대화 상자 필드를 사용자 지정하는 방법](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields).
>

#### 새 필드 만들기 {#creating-a-new-field}

터치 지원 UI에 대한 위젯은 Granite UI 구성 요소로 구현됩니다.

터치 사용 UI의 구성 요소 대화 상자에서 사용할 새 위젯을 생성하려면 다음을 수행해야 합니다. [새로운 Granite UI 필드 구성 요소 만들기](/help/sites-developing/granite-ui-component.md).

>[!NOTE]
>
>Granite UI에 대한 자세한 내용은 [Granite UI 설명서](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html).

대화 상자를 양식 요소의 간단한 컨테이너로 간주하면 대화 상자 콘텐츠의 기본 콘텐츠도 양식 필드로 볼 수 있습니다. 새 양식 필드를 만들려면 리소스 유형을 만들어야 합니다. 이는 새 구성 요소를 만드는 것과 같습니다. Granite UI는 이러한 작업에서 상속할 일반 필드 구성 요소를 제공합니다(사용). `sling:resourceSuperType`):

`/libs/granite/ui/components/coral/foundation/form/field`

보다 구체적으로, Granite UI는 대화 상자에 사용하기 적합한 다양한 필드 구성 요소를 제공합니다 [양식](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/index.html)).

>[!NOTE]
>
>위젯은 로 표시되는 클래식 UI와 다릅니다. `cq:Widgets` 각각 특정 노드가 있는 노드 `xtype` 를 사용하여 해당 ExtJS 위젯과의 관계를 설정합니다. 구현 관점에서 이러한 위젯은 ExtJS 프레임워크에 의해 클라이언트측에서 렌더링되었습니다.

리소스 유형을 만든 후에는 속성을 사용하여 대화 상자에 새 노드를 추가하여 필드를 인스턴스화할 수 있습니다 `sling:resourceType` 방금 소개한 리소스 유형을 참조합니다.

#### 스타일 및 비헤이비어를 위한 클라이언트 라이브러리 만들기 {#creating-a-client-library-for-style-and-behavior}

구성 요소에 대해 스타일 및 비헤이비어를 정의하려면 전용 을 만들 수 있습니다 [클라이언트 라이브러리](/help/sites-developing/clientlibs.md) 사용자 지정 CSS/LESS 및 JS를 정의합니다.

구성 요소 대화 상자용으로만 클라이언트 라이브러리를 로드하려면(즉, 다른 구성 요소용으로는 로드되지 않음) 속성을 설정해야 합니다 `extraClientlibs` 방금 만든 클라이언트 라이브러리의 범주 이름으로 대화 상자를 엽니다. 클라이언트 라이브러리가 상당히 크고/이거나 필드가 해당 대화 상자와 관련이 있어 다른 대화 상자에 필요하지 않은 경우 이 방법을 사용하는 것이 좋습니다.

모든 대화 상자에 대해 클라이언트 라이브러리를 로드하려면 클라이언트 라이브러리의 category 속성을 로 설정합니다. `cq.authoring.dialog`. 모든 대화 상자를 렌더링할 때 기본적으로 포함되는 클라이언트 라이브러리의 범주 이름입니다. 클라이언트 라이브러리가 작거나 필드가 일반적이고 다른 대화 상자에서 다시 사용할 수 있는 경우 이 작업을 하려고 합니다.

예를 보려면 다음을 참조하십시오.

* `cqgems/customizingfield/components/colorpicker/clientlibs`

   * 에서 제공 [코드 샘플](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### 필드 확장(상속) {#extending-inheriting-from-a-field}

요구 사항에 따라 다음 중 하나를 수행할 수 있습니다.

* 구성 요소 상속으로 주어진 Granite UI 필드 확장( `sling:resourceSuperType`)
* 위젯 라이브러리 API(JS/CSS 상속)를 따라 기본 위젯 라이브러리(Granite UI의 경우 Coral UI임)에서 주어진 위젯을 확장합니다.

#### 대화 상자 필드 액세스 {#access-to-dialog-fields}

렌더링 조건( `rendercondition`) 대화 상자의 특정 탭/필드에 액세스할 수 있는 사용자를 제어합니다. 예를 들면 다음과 같습니다.

```xml
+ mybutton
  - sling:resourceType = granite/ui/components/coral/foundation/button
  + rendercondition
    - sling:resourceType = myapp/components/renderconditions/group
    - groups = ["administrators"]
```

### 필드 이벤트 처리 {#handling-field-events}

이제 대화 상자 필드에서의 이벤트 처리 방법이 [사용자 지정 클라이언트 라이브러리의 리스너](#listeners-in-a-custom-client-library). 이는 이전의 다음과 같은 방식에서의 변화입니다. [콘텐츠 구조의 리스너](#listenersinthecontentstructureclassicui).

#### 사용자 지정 클라이언트 라이브러리의 리스너 {#listeners-in-a-custom-client-library}

필드에 논리를 삽입하려면 다음을 수행해야 합니다.

1. 필드를 지정된 CSS 클래스로 표시합니다(다음 *후크*).
1. 클라이언트 라이브러리에서 해당 CSS 클래스 이름에 후크된 JS 수신기를 정의합니다(이렇게 하면 사용자 지정 논리의 범위가 필드에만 지정되며 동일한 유형의 다른 필드에는 영향을 주지 않음).

이를 위해서는 상호 작용하려는 기본 위젯 라이브러리에 대해 알아야 합니다. 다음을 참조하십시오. [Coral UI 설명서](https://developer.adobe.com/experience-manager/reference-materials/6-5/coral-ui/coralui3/index.html) 반응할 이벤트를 식별합니다. 이는 이전에 ExtJS로 수행해야 했던 프로세스와 매우 유사합니다. 특정 위젯의 문서 페이지를 찾은 다음 이벤트 API의 세부 사항을 확인합니다.

예를 보려면 다음을 참조하십시오.

* `cqgems/customizingfield/components/clientlibs/customizingfield`

   * 에서 제공 [코드 샘플](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### 콘텐츠 구조의 리스너 {#listeners-in-the-content-structure}

ExtJS가 있는 클래식 UI에서는 일반적으로 콘텐츠 구조에 지정된 위젯에 대한 리스너를 보유했습니다. 터치 사용 UI에서 를 구현하는 것은 JS 수신기 코드(또는 모든 코드)가 더 이상 콘텐츠에 정의되지 않음으로써 다릅니다.

콘텐츠 구조는 의미 체계 구조를 설명합니다. 기본 위젯의 특성을 암시해서는 안 됩니다. 콘텐츠 구조에 JS 코드가 없으므로 콘텐츠 구조를 변경하지 않고도 구현 세부 사항을 변경할 수 있습니다. 즉, 콘텐츠 구조를 터치하지 않고도 위젯 라이브러리를 변경할 수 있습니다.

#### 대화 상자의 사용 가능 여부 감지 {#dialog-ready}

대화 상자를 사용할 수 있고 준비가 되었을 때만 실행해야 하는 사용자 지정 JavaScript가 있는 경우 `dialog-ready` 이벤트.

이 이벤트는 대화 상자가 로드(또는 다시 로드)되고 사용할 준비가 될 때마다 트리거됩니다. 즉, 대화 상자의 DOM에 변경(만들기/업데이트)이 있을 때마다 트리거됩니다.

`dialog-ready` 대화 상자 또는 유사한 작업 내의 필드에 대한 사용자 지정을 수행하는 JavaScript 사용자 지정 코드를 후크하는 데 사용할 수 있습니다.

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

Granite UI 및 Granite UI 구성 요소(위젯과 동일)의 필드 유효성 검사는 다음을 사용하여 수행됩니다. `foundation-validation` API. [다음을 참조하십시오. `foundation-valdiation` 자세한 내용은 Granite 설명서 를 참조하십시오.](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/clientlibs/foundation/js/validation/index.html)

예를 보려면 다음을 참조하십시오.

* `cqgems/customizingfield/components/clientlibs/customizingfield/js/validations.js`

   * 에서 제공 [코드 샘플](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `/libs/cq/gui/components/authoring/dialog/clientlibs/dialog/js/validations.js`

## 디자인 대화 상자 만들기 및 구성 {#creating-and-configuring-a-design-dialog}

디자인 대화 상자는 구성 요소에서 편집할 수 있는 디자인 세부 사항이 있을 때 제공됩니다. [디자인 모드](/help/sites-authoring/default-components-designmode.md).

이 정의는 의 정의와 매우 유사합니다 [콘텐츠 편집에 사용되는 대화 상자](#creating-a-new-dialog)를 노드 로 정의한다는 차이점이 있습니다.

* 노드 이름: `cq:design_dialog`
* 유형: `nt:unstructured`

## 즉석 편집기 만들기 및 구성 {#creating-and-configuring-an-inplace-editor}

즉석 편집기를 사용하면 대화 상자를 열지 않고도 단락 흐름에서 직접 콘텐츠를 편집할 수 있습니다. 예를 들어 표준 텍스트 및 제목 구성 요소에는 모두 즉석 편집기가 있습니다.

즉석 편집기는 모든 구성 요소 유형에 필요/의미가 없습니다.

다음을 참조하십시오 [페이지 작성 확장 - 새 즉석 편집기 추가](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor) 추가 정보.

## 구성 요소 도구 모음 맞춤화 {#customizing-the-component-toolbar}

다음 [구성 요소 도구 모음](/help/sites-developing/touch-ui-structure.md#component-toolbar) 는 사용자에게 구성 요소에 대한 편집, 구성, 복사 및 삭제와 같은 작업 범위에 대한 액세스 권한을 제공합니다.

다음을 참조하십시오 [페이지 작성 확장 - 구성 요소 도구 모음에 새 작업 추가](/help/sites-developing/customizing-page-authoring-touch.md#add-new-action-to-a-component-toolbar) 추가 정보.

## 참조 레일에 대한 구성 요소 구성(빌린/빌려준) {#configuring-a-component-for-the-references-rail-borrowed-lent}

새 구성 요소가 다른 페이지의 콘텐츠를 참조하는 경우 **빌려 온 컨텐츠** 및 **빌려 온 컨텐츠** 의 섹션 [**참조**](/help/sites-authoring/basic-handling.md#references) 레일.

기본 AEM에서는 참조 구성 요소만 확인합니다. 구성 요소를 추가하려면 OSGi 번들을 구성해야 합니다 **WCM 작성 콘텐츠 참조 구성**.

확인할 속성과 함께 구성 요소를 지정하여 정의에 새 항목을 만듭니다. 예:

`/apps/<*your-Project*>/components/reference@parentPath`

>[!NOTE]
>
>AEM을 사용하여 작업할 때 이러한 서비스에 대한 구성 설정을 관리할 수 있는 방법에는 몇 가지가 있습니다. 자세한 내용 및 권장 사례를 확인하려면 [OSGi 구성](/help/sites-deploying/configuring-osgi.md)을 참조하십시오.

## 단락 시스템에 구성 요소 활성화 및 추가 {#enabling-and-adding-your-component-to-the-paragraph-system}

구성 요소가 개발되면 적절한 단락 시스템에서 사용할 수 있도록 활성화해야 하므로 필요한 페이지에서 사용할 수 있습니다.

다음 중 하나를 통해 이 작업을 수행할 수 있습니다.

* 사용 [디자인 모드](/help/sites-authoring/default-components-designmode.md) 특정 페이지를 편집할 때.
* [정의 `components` 템플릿의 단락 시스템에 있는 속성](/help/sites-developing/components-basics.md#adding-your-component-to-the-paragraph-system).

## 자산을 드래그하여 구성 요소 인스턴스를 만들도록 단락 시스템 구성 {#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance}

AEM에서는 페이지에서 단락 시스템을 구성할 수 있으므로 [사용자가 (적절한) 에셋을 해당 페이지의 인스턴스로 드래그하면 새 구성 요소의 인스턴스가 자동으로 만들어집니다](/help/sites-authoring/editing-content.md#insertingacomponenttouchoptimizedui) (항상 빈 구성 요소를 페이지로 드래그해야 하는 대신).

이 동작과 필요한 에셋-구성 요소 관계를 구성할 수 있습니다.

1. 페이지 디자인의 단락 정의 아래에 있습니다. 예:

   * `/etc/designs/<myApp>/page/par`

   새 노드 만들기:

   * 이름: `cq:authoring`
   * 유형: `nt:unstructured`

1. 이 아래에 모든 자산-구성 요소 매핑을 보유할 새 노드를 만듭니다.

   * 이름: `assetToComponentMapping`
   * 유형: `nt:unstructured`

1. 각 에셋-구성 요소 매핑에 대해 노드를 만듭니다.

   * 이름: 텍스트. 이름은 에셋 및 관련 구성 요소 유형(예: 이미지)을 나타내는 것이 좋습니다
   * 유형: `nt:unstructured`

   각각 다음 속성을 갖습니다.

   * `assetGroup`:

      * 유형: `String`
      * 값: 관련 자산이 속한 그룹(예: ) `media`

   * `assetMimetype`:

      * 유형: `String`
      * 값: 관련 에셋의 mime 유형(예: ) `image/*`

   * `droptarget`:

      * 유형: `String`
      * 값: 드롭 대상. 예: `image`

   * `resourceType`:

      * 유형: `String`
      * 값: 관련 구성 요소 리소스(예: ) `foundation/components/image`

   * `type`:

      * 유형: `String`
      * 값: 예: 유형 `Images`

예를 보려면 다음을 참조하십시오.

* `/etc/designs/geometrixx/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-outdoors/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-media/jcr:content/article/article-content-par/cq:authoring`

GITHUB의 코드

이 페이지의 코드는 GitHub에서 확인할 수 있습니다

* [GitHub에서 AEM-project-Archetype 프로젝트 열기](https://github.com/adobe/aem-project-archetype)
* 다음으로 프로젝트 다운로드 [ZIP 파일](https://github.com/adobe/aem-project-archetype/archive/master.zip)

>[!NOTE]
>
>이제 를 사용할 때 UI 내에서 구성 요소 인스턴스의 자동 생성을 쉽게 구성할 수 있습니다 [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 편집 가능한 템플릿 다음을 참조하십시오 [페이지 템플릿 만들기](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) 지정된 미디어 유형과 자동으로 연결되는 구성 요소를 정의하는 방법에 대한 자세한 정보.

## AEM Brackets 확장 사용 {#using-the-aem-brackets-extension}

다음 [AEM Brackets 확장](/help/sites-developing/aem-brackets.md) 는 AEM 구성 요소 및 클라이언트 라이브러리를 편집하는 매끄러운 워크플로를 제공합니다. 다음을 기반으로 합니다. [대괄호](https://brackets.io/) 코드 편집기.

확장:

* 동기화를 쉽게 하여(Maven 또는 File Vault 필요 없음) 개발자 효율성을 높이고 AEM 지식이 부족한 프론트엔드 개발자의 프로젝트 참여도 지원합니다.
* 일부 제공 [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) 구성 요소 개발을 단순화하고 보안을 강화하기 위해 고안된 템플릿 언어입니다.

>[!NOTE]
>
>구성 요소를 만드는 데 권장되는 메커니즘은 대괄호 입니다. 클래식 UI에 맞게 디자인된 CRXDE Lite - 구성 요소 만들기 기능을 대체합니다.

## 클래식 구성 요소에서 마이그레이션 {#migrating-from-a-classic-component}

클래식 UI와 함께 사용하도록 설계된 구성 요소를 터치 사용 UI와 함께 사용할 수 있는 구성 요소로 마이그레이션할 때(단독으로 또는 공동으로) 다음 문제를 고려해야 합니다.

* HTL

   * 사용 [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) 은(는) 필수는 아니지만 구성 요소를 업데이트해야 하는 경우 고려하기에 이상적인 시간입니다 [jsp에서 HTL로의 마이그레이션](/help/sites-developing/components-basics.md#htl-vs-jsp).

* 구성 요소

   * 마이그레이션 [`cq:listener`](/help/sites-developing/developing-components.md#migrating-cq-listener-code) 클래식 UI 관련 함수를 사용하는 코드
   * RTE 플러그인, 자세한 내용은 [리치 텍스트 편집기 구성](/help/sites-administering/rich-text-editor.md).
   * [마이그레이션 `cq:listener` 코드](#migrating-cq-listener-code) 클래식 UI에 특정된 함수를 사용하는 경우

* 대화 상자

   * 터치 지원 UI에서 사용할 대화 상자를 만듭니다. 그러나 호환성을 위해 터치 지원 UI에 대한 대화 상자가 정의되지 않은 경우 터치 지원 UI는 클래식 UI 대화 상자 정의를 사용할 수 있습니다.
   * 다음 [AEM 현대화 도구](/help/sites-developing/modernization-tools.md) 는 기존 구성 요소를 확장하는 데 도움이 됩니다.
   * [Granite UI 구성 요소에 ExtJS 매핑](/help/sites-developing/touch-ui-concepts.md#extjs-and-corresponding-granite-ui-components) 는 ExtJS xtype 및 노드 유형과 동일한 Granite UI 리소스 유형에 대한 편리한 개요를 제공합니다.
   * 필드 사용자 정의. 자세한 내용은 의 AEM Gems 세션 을 참조하십시오. [대화 상자 필드 사용자 지정](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-customizing-dialog-fields-in-touch-ui.html?lang=en).
   * 유형에서 (으)로 마이그레이션 [Granite UI 유효성 검사](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/clientlibs/foundation/js/validation/index.html)
   * JS 리스너 사용. 자세한 내용은 [필드 이벤트 처리](#handling-field-events) 및 의 AEM Gems 세션 [대화 상자 필드 사용자 지정](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-customizing-dialog-fields-in-touch-ui.html?lang=en).

### cq:listener 코드 마이그레이션 {#migrating-cq-listener-code}

클래식 UI용으로 설계된 프로젝트를 마이그레이션하는 경우 `cq:listener` 코드(및 구성 요소와 관련된 clientlibs)는 클래식 UI에 고유한 함수(예: `CQ.wcm.*`). 마이그레이션의 경우 터치 지원 UI에서 이와 동등한 오브젝트/함수를 사용하여 이러한 코드를 업데이트해야 합니다.

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

배치 `README.md` 구성 요소 구조의 파일입니다. 이 Markdown은에 표시됩니다. [구성 요소 콘솔](/help/sites-authoring/default-components-console.md).

![chlimage_1-7](assets/chlimage_1-7.png)

지원되는 Markdown은 의 경우와 동일합니다 [컨텐츠 조각](/help/assets/content-fragments/content-fragments-markdown.md).
