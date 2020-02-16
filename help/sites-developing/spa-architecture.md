---
title: AEM용 SPA 개발
seo-title: AEM용 SPA 개발
description: 이 문서에서는 프런트 엔드 개발자에게 AEM용 SPA를 개발할 때 고려해야 할 중요한 질문을 제시하며, AEM에 개발된 SPA를 배포할 때 염두에 두어야 할 SPA와 관련된 AEM 아키텍처에 대한 개요를 제공합니다.
seo-description: 이 문서에서는 프런트 엔드 개발자에게 AEM용 SPA를 개발할 때 고려해야 할 중요한 질문을 제시하며, AEM에 개발된 SPA를 배포할 때 염두에 두어야 할 SPA와 관련된 AEM 아키텍처에 대한 개요를 제공합니다.
uuid: 6673a041-c557-4968-ae54-4cd5b9f56251
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 9584392a-d8a3-45a4-9cdf-fd211c8e6091
docset: aem65
translation-type: tm+mt
source-git-commit: 2dad220d6593ed542816f8a97b0d4b44f0d57876

---


# AEM용 SPA 개발{#developing-spas-for-aem}

단일 페이지 애플리케이션(SPA)을 통해 웹 사이트 사용자에게 매력적인 경험을 제공할 수 있습니다. 개발자는 SPA 프레임워크를 사용하여 사이트를 구축하고자 하며 작성자는 이러한 프레임워크를 사용하여 구축한 사이트에 대해 AEM 내에서 컨텐츠를 원활하게 편집하고자 합니다.

이 문서에서는 프런트 엔드 개발자에게 AEM용 SPA를 개발할 때 고려해야 할 중요한 질문을 제시하며, AEM에 SPA를 배포하는 것과 관련하여 AEM의 아키텍처에 대한 개요를 제공합니다.

>[!NOTE]
>
>SPA 편집기는 SPA 프레임워크 기반의 클라이언트측 렌더링(예: 반응 또는 각도)이 필요한 프로젝트에 권장되는 솔루션입니다.

## AEM을 위한 SPA 개발 원칙 {#spa-development-principles-for-aem}

AEM에서 단일 페이지 애플리케이션을 개발하는 경우 프런트 엔드 개발자는 SPA를 만들 때 표준 우수 사례를 준수한다고 가정합니다. 프런트 엔드 개발자는 이러한 일반적인 모범 사례와 AEM 전용 원칙을 따르는 경우 AEM 및 컨텐츠 작성 기능을 [통해](/help/sites-developing/spa-walkthrough.md#content-editing-experience-with-spa)SPA를 사용할 수 있습니다.

* **[휴대성](/help/sites-developing/spa-architecture.md#portability)-**모든 구성 요소와 마찬가지로 가능한 한 휴대성을 갖추도록 구축해야 합니다. SPA는 안전하고 재사용 가능한 구성 요소로 구축되어야 합니다.
* **[AEM 드라이브 사이트](/help/sites-developing/spa-architecture.md#aem-drives-site-structure)**구조 - 프런트 엔드 개발자는 구성 요소를 만들고 내부 구조를 소유하지만 AEM을 사용하여 사이트의 컨텐츠 구조를 정의합니다.
* **[동적 렌더링](/help/sites-developing/spa-architecture.md#dynamic-rendering)**- 모든 렌더링은 동적이여야 합니다.
* **[동적 라우팅](#dynamic-routing)-**SPA는 라우팅에 대한 책임을 지고 AEM이 이를 듣고 이에 따라 페치를 수행합니다. 모든 라우팅은 동적이여야 합니다.

SPA를 개발할 때 이러한 원칙을 염두에 두는 경우 지원되는 모든 AEM 작성 기능을 활성화하면서 최대한 유연하고 향후 증거 자료로 활용할 수 있습니다.

AEM 작성 기능을 지원하지 않아도 되는 경우 다른 SPA [디자인 모델을](/help/sites-developing/spa-architecture.md#spa-design-models)고려해야 할 수 있습니다.

### 이식성 {#portability}

구성 요소를 개발할 때와 마찬가지로 이식성을 최대화할 수 있도록 구성 요소를 설계해야 합니다. 구성 요소의 이식성 또는 재사용성에 반하는 모든 패턴은 호환성, 유연성 및 유지 관리 기능을 유지하기 위해 피해야 합니다.

그 결과 SPA는 휴대성이 높고 재사용 가능한 구성 요소로 구축되어야 합니다.

### AEM 드라이브 사이트 구조 {#aem-drives-site-structure}

프런트 엔드 개발자는 앱을 빌드하는 데 사용되는 SPA 구성 요소 라이브러리를 만든 자신의 책임을 스스로 생각해야 합니다. 프런트 엔드 개발자는 구성 요소의 내부 구조를 완벽하게 제어할 수 있습니다. [그러나 AEM은 항상 사이트의 구조를 소유합니다.](/help/sites-developing/spa-overview.md)

즉, 프런트 엔드 개발자는 구성 요소의 시작 지점 전후 고객 컨텐츠를 추가할 수 있으며 구성 요소 내에서 서드 파티 호출을 수행할 수도 있습니다. 그러나 프런트 엔드 개발자는 구성 요소가 중첩되는 방식을 완전히 제어하지 못합니다.

### 동적 렌더링 {#dynamic-rendering}

SPA는 동적 컨텐츠 렌더링에만 의존해야 합니다. 이는 AEM이 컨텐츠 구조의 모든 하위 항목을 가져오고 렌더링하는 기본 예측입니다. [](/help/sites-developing/spa-architecture.md#portability)

특정 컨텐츠를 가리키는 명시적 렌더링은 정적 렌더링으로 간주되며 지원되는 렌더링은 AEM의 컨텐츠 작성 기능과 호환되지 않습니다. 이식성의 원리에 어긋나는 [기준이기도 하다](/help/sites-developing/spa-architecture.md#portability).

### 동적 라우팅 {#dynamic-routing}

렌더링과 마찬가지로 모든 라우팅도 동적이여야 합니다. AEM에서 [SPA는 항상 라우팅을](/help/sites-developing/spa-routing.md) 소유하고 AEM이 이를 듣고 이에 따라 컨텐츠를 전달합니다.

모든 정적 라우팅은 이식성의 [원칙에](/help/sites-developing/spa-architecture.md#portability) 어긋나고 AEM의 컨텐츠 작성 기능과 호환하지 않아 작성자를 제한합니다. 예를 들어, 정적 라우팅을 사용하여 컨텐츠 작성자가 경로를 변경하거나 페이지를 변경하려는 경우 프런트 엔드 개발자에게 요청해야 합니다.

## SPA Starter Kit를 위한 Maven Tranype {#maven-archetype-for-spa-starter-kit}

Adobe에서는 AEM용 SPA [프로젝트를 시작하는 데 도움이 되도록 SPA](https://github.com/adobe/aem-spa-project-archetype) Starter Kit용 Maven Tranype을 활용하는 것이 좋습니다.

## SPA Design Models {#spa-design-models}

AEM에서 SPA 개발 [원칙을](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem) 따르는 경우 지원되는 모든 AEM 컨텐츠 작성 기능과 함께 SPA가 작동합니다. [](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)

그러나 이것이 전적으로 필요하지 않은 경우가 있을 수 있습니다. 다음 표는 다양한 디자인 모델, 그 장점 및 그 단점에 대한 개요를 제공합니다.

<table>
 <tbody>
  <tr>
   <th><strong>디자인 모델<br /> </strong></th>
   <th><strong>장점</strong></th>
   <th><strong>단점</strong></th>
  </tr>
  <tr>
   <td>AEM은 SPA Editor SDK 프레임워크를 사용하지 않고도 헤드리스 <a href="/help/sites-developing/spa-reference-materials.md">CMS로 사용됩니다.</a></td>
   <td>프런트 엔드 개발자는 앱을 완벽하게 제어할 수 있습니다.</td>
   <td><p>컨텐츠 작성자는 AEM의 컨텐츠 작성 경험을 활용할 수 없습니다.</p> <p>정적 참조나 라우팅이 들어 있는 경우 코드를 이식하거나 다시 사용할 수 없습니다.</p> <p>템플릿 편집기를 사용할 수 없으므로 프런트 엔드 개발자는 JCR을 통해 편집 가능한 템플릿을 유지 관리해야 합니다.</p> </td>
  </tr>
  <tr>
   <td>프런트 엔드 개발자는 SPA Editor SDK 프레임워크를 사용하지만 컨텐츠 작성자에게 일부 영역만 엽니다.</td>
   <td>개발자는 앱의 제한된 영역에서만 저작을 활성화하여 앱을 계속 제어합니다.</td>
   <td><p>컨텐츠 작성자는 제한된 AEM의 컨텐츠 작성 경험으로 제한됩니다.</p> <p>정적 참조나 라우팅이 포함되어 있는 경우 코드를 이식하거나 다시 사용할 수 없을 때 위험이 있습니다.</p> <p>템플릿 편집기를 사용할 수 없으므로 프런트 엔드 개발자는 JCR을 통해 편집 가능한 템플릿을 유지 관리해야 합니다.</p> </td>
  </tr>
  <tr>
   <td>프로젝트는 SPA 편집기 SDK를 완전히 활용하며 프런트 엔드 구성 요소는 라이브러리로 개발되고 앱의 콘텐츠 구조는 AEM에 위임됩니다.</td>
   <td><p>이 앱은 다시 사용할 수 있고 휴대할 수 있습니다.</p> <p>콘텐츠 작성자는 AEM의 콘텐츠 제작 환경을 사용하여 앱을 편집할 수 있습니다.<br /> </p> <p>SPA는 템플릿 편집기와 호환됩니다.</p> </td>
   <td><p>개발자는 앱의 구조와 AEM에 위임된 컨텐츠 부분을 제어하지 않습니다.</p> <p>개발자는 여전히 AEM을 사용하여 작성되지 않은 콘텐츠에 대해 앱의 영역을 예약할 수 있습니다.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>모든 모델은 AEM에서 지원되지만 컨텐츠 작성자는 세 번째(AEM의 권장 [SPA 개발 원칙](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)준수)를 구현해야만 AEM에서 SPA의 컨텐츠를 익숙한 대로 인터랙션하고 편집할 수 있습니다.
>[](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)

## 기존 SPA를 AEM으로 마이그레이션 {#migrating-existing-spas-to-aem}

일반적으로 SPA가 AEM의 [SPA 개발 원칙을](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)따르는 경우 AEM에서 작동하며 AEM SPA 편집기를 사용하여 편집할 수 있습니다.

다음 단계에 따라 기존 SPA를 AEM에서 사용할 수 있도록 준비하십시오.

1. **JS 구성 요소를 모듈식으로 만듭니다.**

   원하는 순서대로, 위치 및 크기로 렌더링할 수 있습니다.
1. **Adobe SDK에서 제공하는 컨테이너를 사용하여 구성 요소를 화면에 배치합니다.**

   AEM에서는 사용할 페이지 및 단락 시스템 구성 요소를 제공합니다.
1. **각 JS 구성 요소에 대한 AEM 구성 요소를 만듭니다.**

   AEM 구성 요소는 대화 상자와 JSON 출력을 정의합니다.

## 프런트 엔드 개발자를 위한 지침 {#instructions-for-front-end-developers}

프런트 엔드 개발자에게 AEM용 SPA를 만들기 위한 기본 작업은 구성 요소 및 JSON 모델에 동의해야 합니다.

다음은 AEM용 SPA를 개발할 때 프런트 엔드 개발자가 따라야 하는 단계에 대한 개요입니다.

1. **구성 요소 및 JSON 모델에 동의**

   프런트 엔드 개발자와 백엔드 AEM 개발자는 필요한 구성 요소와 모델에 동의해야 SPA 구성 요소에서 백엔드 구성 요소와 1:1 일치시킬 수 있습니다.

   AEM 구성 요소는 여전히 편집 대화 상자를 제공하고 구성 요소 모델을 내보내는 데 필요합니다.

1. **반응형 컴포넌트에서`this.props.cqModel`**

   구성 요소가 동의되고 JSON 모델이 적용되면 프런트 엔드 개발자는 SPA를 무료로 개발할 수 있으며 JSON 모델을 통해 간편하게 이용할 수 `this.props.cqModel`있습니다.

1. **구성 요소의`render()`메서드 구현**

   프런트 엔드 개발자는 자신이 원하는 대로 `render()` 메서드를 구현하고 `cqModel` 속성 필드를 사용할 수 있습니다. 이렇게 하면 페이지에 삽입할 DOM 및 HTML 조각이 출력됩니다. 이는 React에서 앱을 빌드하는 표준 방법입니다.

1. **구성 요소를`MapTo()`**

   매핑은 구성 요소 클래스를 저장하고 제공된 `Container` 구성 요소에서 지정된 리소스 유형을 기반으로 구성 요소를 검색하고 동적으로 인스턴스화하기 위해 내부적으로 사용됩니다.

   이 기능은 프런트 엔드와 백 엔드 간의 &quot;접착제&quot; 역할을 하므로 편집자는 반응형 구성 요소가 일치하는 구성 요소를 파악할 수 있습니다.

   및 `Page` 는 기본을 확장하는 클래스의 좋은 예입니다 `ResponsiveGrid` `Container`.

1. **Define the component&#39;s`EditConfig`as parameter to`MapTo()`**

   이 매개 변수는 렌더링되지 않았거나 렌더링할 컨텐츠가 없는 경우 구성 요소의 이름을 지정하는 방법을 편집자에게 알려 주는 데 필요합니다.

1. **페이지 및 컨테이너에 대해 제공된`Container`클래스 확장**

   페이지 및 단락 시스템은 내부 구성 요소에 대한 위임이 예상대로 작동하도록 이 클래스를 확장해야 합니다.

1. **HTML5 API를 사용하는 라우팅 솔루션을`History`구현합니다.**

   이 `ModelRouter` 활성화되면 `pushState` 및 `replaceState` `PageModelManager` 함수를 호출하면 모델의 누락된 조각을 가져오라는 요청이 트리거됩니다.

   의 현재 버전은 `ModelRouter` Sling Model 진입점의 실제 리소스 경로를 가리키는 URL의 사용만 지원합니다. 별칭 URL 또는 별칭 사용을 지원하지 않습니다.

   정규 표현식 목록을 무시하도록 `ModelRouter` 하거나 구성할 수 있습니다.

## AEM 지원 {#aem-agnostic}

이러한 코드 블록은 Adobe 또는 AEM별 반응형 구성 요소가 없어도 되는 방법을 보여 줍니다.

* JavaScript 구성 요소 내에 있는 모든 것은 AEM에 관계없이 됩니다.
* 그러나 AEM과 관련된 것은 JS 구성 요소를 MapTo 도우미로 AEM 구성 요소에 매핑해야 한다는 것입니다.

![screen_shot_2018-12-11at144019](assets/screen_shot_2018-12-11at144019.png)

헬퍼는 `MapTo` 백엔드 구성 요소와 프런트엔드 구성 요소를 함께 일치시킬 수 있는 &quot;접착제&quot;입니다.

* JS 컨테이너(또는 JS 단락 시스템)에 JS 구성 요소가 JSON에 있는 각 구성 요소를 렌더링할 책임이 있는지 알려줍니다.
* JS 구성 요소가 렌더링하는 HTML에 HTML 데이터 속성을 추가하여 SPA 편집기가 구성 요소를 편집할 때 작성자에게 표시할 대화 상자를 알 수 있습니다.

일반적으로 AEM용 SPA 사용 `MapTo` 및 빌드에 대한 자세한 내용은 선택한 프레임워크에 대한 시작하기 안내서를 참조하십시오.

* [AEM에서 SPA 시작하기 - 반응](/help/sites-developing/spa-getting-started-react.md)
* [AEM에서 SPA 시작 - Angular](/help/sites-developing/spa-getting-started-angular.md)

## AEM 아키텍처 및 SPA {#aem-architecture-and-spas}

개발, 제작 및 게시 환경을 포함한 AEM의 일반 아키텍처는 SPA를 사용할 때 변경되지 않습니다. 그러나 SPA 개발이 이 아키텍처에 어떻게 적합한지 파악하는 것이 도움이 됩니다.

![screen_shot_2018-12-11at145348](assets/screen_shot_2018-12-11at145348.png)

* **빌드 환경**

   여기에서 SPA 애플리케이션 소스 및 구성 요소 소스의 소스가 체크 아웃됩니다.

   * NPM clientlib 생성기는 SPA 프로젝트에서 클라이언트 라이브러리를 만듭니다.
   * 해당 라이브러리는 Maven에서 가져와 AEM 작성자에게 구성 요소와 함께 Maven Build 플러그인에 의해 배포됩니다.

* **AEM Author**

   컨텐츠는 AEM 작성자에 생성되며 여기에는 SPA 작성도 포함됩니다.

   작성 환경에서 SPA 편집기를 사용하여 SPA를 편집하는 경우

   1. SPA는 외부 HTML을 요청합니다.
   1. CSS가 로드됩니다.
   1. SPA 애플리케이션의 Javascript가 로드됩니다.
   1. SPA 응용 프로그램이 실행되면 JSON이 요청되어 앱이 `cq-data` 속성을 포함한 페이지의 DOM을 빌드할 수 있습니다.
   1. 이 `cq-data` 속성을 사용하면 편집기에서 구성 요소에 사용할 수 있는 편집 구성을 알 수 있도록 추가 페이지 정보를 로드할 수 있습니다.

* **AEM 게시**

   여기에서 제작된 컨텐츠와 SPA 애플리케이션 객체, clientlibs 및 구성 요소를 비롯한 컴파일된 라이브러리가 공개적으로 소비되도록 게시됩니다.

* **발송자/CDN**

   디스패처는 사이트 방문자에 대해 AEM의 캐싱 레이어 역할을 합니다.

   * 요청은 AEM 작성자의 경우와 유사하게 처리되지만 편집자만 필요하므로 페이지 정보에 대한 요청은 없습니다.
   * Javascript, CSS, JSON 및 HTML이 캐시되므로 페이지를 최적화하여 신속하게 전달할 수 있습니다.

>[!NOTE]
>
>AEM 내에서 Javascript 빌드 메커니즘을 실행하거나 Javascript 자체를 실행할 필요가 없습니다. AEM은 SPA 애플리케이션에서 컴파일된 객체만 호스팅합니다.

## 다음 단계 {#next-steps}

AEM의 단순 SPA가 구조화되고 작동 방식에 대한 개요는 React와 Angular 모두에 대한 시작 [안내서를](/help/sites-developing/spa-getting-started-react.md) [참조하십시오](/help/sites-developing/spa-getting-started-angular.md).

자체 SPA를 만드는 단계별 가이드는 AEM SPA 편집기 [- WKND 이벤트 자습서를 참조하십시오](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html).

동적 모델-구성 요소 매핑 및 AEM의 SPA 내에서 작동하는 방식에 대한 자세한 내용은 SPA에 대한 [구성 요소 매핑에 대한 동적 모델을 참조하십시오](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

AEM에서 React 또는 Angular 이외의 프레임워크에 대해 SPA를 구현하거나 AEM용 SPA SDK의 작동 방식을 심층적으로 살펴보려면 SPA Blueprint [문서를 참조하십시오](/help/sites-developing/spa-blueprint.md) .
