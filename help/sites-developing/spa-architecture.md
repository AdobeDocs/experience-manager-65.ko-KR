---
title: AEM용 SPA 개발
seo-title: AEM용 SPA 개발
description: 이 문서에서는 AEM용 SPA을 개발하기 위해 프런트 엔드 개발자와 함께 AEM용를 개발할 때 고려해야 할 중요한 질문을 제시하며 AEM에 개발한 SPA을 배포할 때 염두에 두어야 할 SPA 아키텍처에 대한 개요를 제공합니다.
seo-description: 이 문서에서는 AEM용 SPA을 개발하기 위해 프런트 엔드 개발자와 함께 AEM용를 개발할 때 고려해야 할 중요한 질문을 제시하며 AEM에 개발한 SPA을 배포할 때 염두에 두어야 할 SPA 아키텍처에 대한 개요를 제공합니다.
uuid: 6673a041-c557-4968-ae54-4cd5b9f56251
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 9584392a-d8a3-45a4-9cdf-fd211c8e6091
docset: aem65
translation-type: tm+mt
source-git-commit: 590dc4464182d4baf8293e7bb0774ce92971c0af
workflow-type: tm+mt
source-wordcount: '2122'
ht-degree: 2%

---


# AEM용 SPA 개발{#developing-spas-for-aem}

단일 페이지 애플리케이션(SPA)을 통해 웹 사이트 사용자에게 매력적인 경험을 제공할 수 있습니다. 개발자는 SPA 프레임워크을 사용하여 사이트를 구축하고자 하며, 작성자는 이러한 프레임워크를 사용하여 구축된 사이트에서 AEM의 컨텐츠를 매끄럽게 편집하고자 합니다.

이 문서에서는 AEM용 SPA을 개발하기 위해 프런트 엔드 개발자와 계약을 맺을 때 고려해야 할 중요한 질문에 대해 설명하고 AEM에 SPA을 배포하는 것과 관련하여 AEM 아키텍처를 개괄적으로 설명합니다.

>[!NOTE]
>
>SPA 편집기는 SPA 프레임워크 기반의 클라이언트측 렌더링(예: 반응형 또는 각도)이 필요한 프로젝트에 권장되는 솔루션입니다.

## AEM {#spa-development-principles-for-aem}에 대한 SPA 개발 원칙

AEM에서 단일 페이지 애플리케이션을 개발하는 경우 프런트 엔드 개발자가 SPA을 만들 때 표준 우수 사례를 관찰한다고 가정합니다. 프런트 엔드 개발자는 이러한 일반적인 모범 사례와 몇 가지 AEM 관련 원칙을 따르는 경우, SPA은 [AEM 및 그 컨텐트 작성 기능](/help/sites-developing/spa-walkthrough.md#content-editing-experience-with-spa)과 함께 사용할 수 있습니다.

* **[휴대성](/help/sites-developing/spa-architecture.md#portability) -** 어떠한 구성 요소와 마찬가지로, 그 구성 요소는 가능한 한 휴대할 수 있도록 만들어져야 한다. SPA은 안전하고 재사용 가능한 구성 요소로 구축되어야 합니다.
* **[AEM 드라이브 사이트 구조](/help/sites-developing/spa-architecture.md#aem-drives-site-structure)**  - 프런트 엔드 개발자는 구성 요소를 만들고 내부 구조를 소유하지만, AEM을 사용하여 사이트의 컨텐츠 구조를 정의합니다.
* **[동적 렌더링](/help/sites-developing/spa-architecture.md#dynamic-rendering)**  - 모든 렌더링이 동적이여야 합니다.
* **[동적 라우팅](#dynamic-routing) -** SPA은 라우팅 책임을 지고 AEM은 라우팅 및 페치를 수신합니다. 모든 라우팅도 동적입니다.

SPA을 개발할 때 이러한 원칙을 염두에 두면 지원되는 모든 AEM 저작 기능을 활성화하면서 가능한 한 유연하고 향후 저작 수단이 될 수 있습니다.

AEM 저작 기능을 지원할 필요가 없는 경우 다른 [SPA 디자인 모델](/help/sites-developing/spa-architecture.md#spa-design-models)을 고려해야 할 수 있습니다.

### 이식성 {#portability}

구성 요소를 개발할 때처럼 휴대성을 극대화하는 방식으로 구성 요소를 설계해야 합니다. 구성 요소의 이식성 또는 재사용성에 어긋나는 모든 패턴은 향후 호환성, 유연성 및 유지 관리를 위해 피하는 것이 좋습니다.

그 결과 SPA은 휴대성과 재사용 가능한 구성 요소로 구축되어야 합니다.

### AEM 드라이브 사이트 구조 {#aem-drives-site-structure}

프런트 엔드 개발자는 앱을 빌드하는 데 사용되는 SPA 구성 요소 라이브러리를 만든 자신의 책임을 스스로 생각해야 합니다. 프런트 엔드 개발자는 구성 요소의 내부 구조를 완벽하게 제어할 수 있습니다. [그러나 AEM은 항상 사이트의 구조를 소유합니다.](/help/sites-developing/spa-overview.md)

즉, 프런트 엔드 개발자는 구성 요소의 시작 지점 전후에 고객 컨텐츠를 추가할 수 있으며 구성 요소 내에서 제3자를 호출할 수도 있습니다. 그러나 프런트 엔드 개발자는 구성 요소가 중첩되는 방식을 완전히 제어하지는 못합니다.

### 동적 렌더링 {#dynamic-rendering}

SPA은 컨텐츠의 동적 렌더링에만 의존해야 합니다. 이는 AEM이 컨텐츠 구조의 모든 하위 항목을 가져오고 렌더링하는 기본 예측입니다.[](/help/sites-developing/spa-architecture.md#portability)

특정 컨텐츠를 가리키는 명시적 렌더링은 정적 렌더링으로 간주되며 지원되는 것은 AEM 컨텐츠 제작 기능과 호환되지 않습니다. 이것은 [이식성](/help/sites-developing/spa-architecture.md#portability)의 원칙과도 반대됩니다.

### 동적 라우팅 {#dynamic-routing}

렌더링과 마찬가지로 모든 라우팅도 동적입니다. AEM에서 [SPA은 항상 라우팅](/help/sites-developing/spa-routing.md)을 소유해야 하며 AEM은 수신 후 전달에 따라 내용을 가져옵니다.

모든 정적 라우팅은 [이식성 원칙](/help/sites-developing/spa-architecture.md#portability)에 반대되며 AEM의 컨텐츠 작성 기능과 호환되지 않아 작성자를 제한합니다. 예를 들어 정적 라우팅을 사용하여 컨텐츠 작성자가 경로를 변경하거나 페이지를 변경하려는 경우 프런트 엔드 개발자에게 해당 작업을 수행하도록 요청해야 합니다.

## AEM 프로젝트 전형 {#aem-project-archetype}

모든 AEM 프로젝트는 React 또는 Angular를 사용하여 SPA 프로젝트를 지원하고 SPA SDK를 활용하는 [AEM Project Tranype](https://docs.adobe.com/content/help/ko-KR/experience-manager-core-components/using/developing/archetype/overview.html)을 활용해야 합니다.

## SPA 디자인 모델 {#spa-design-models}

AEM](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)에서 SPA을 개발하는 [의 원칙을 준수하면 SPA이 지원되는 모든 AEM 컨텐츠 제작 기능과 함께 작동합니다.[](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)

이러한 경우가 전적으로 필요하지 않을 수도 있습니다. 다음 표는 다양한 디자인 모델, 그 이점 및 단점에 대한 개요를 제공합니다.

<table>
 <tbody>
  <tr>
   <th><strong>디자인 모델<br /> </strong></th>
   <th><strong>이점</strong></th>
   <th><strong>단점</strong></th>
  </tr>
  <tr>
   <td>AEM은 <a href="/help/sites-developing/spa-reference-materials.md">SPA 편집기 SDK 프레임워크를 사용하지 않고 헤드리스 CMS로 사용됩니다.</a></td>
   <td>프런트 엔드 개발자는 앱을 완벽하게 제어할 수 있습니다.</td>
   <td><p>컨텐츠 작성자는 AEM 컨텐츠 작성 경험을 활용할 수 없습니다.</p> <p>이 코드가 정적 참조나 라우팅이 포함된 경우 이식하거나 다시 사용할 수 없습니다.</p> <p>템플릿 편집기를 사용할 수 없으므로 프런트 엔드 개발자가 JCR을 통해 편집 가능한 템플릿을 유지 관리해야 합니다.</p> </td>
  </tr>
  <tr>
   <td>프런트 엔드 개발자는 SPA Editor SDK 프레임워크를 사용하지만 컨텐츠 작성자에게 일부 영역만 엽니다.</td>
   <td>개발자는 앱의 제한된 영역에서만 제작할 수 있게 함으로써 앱을 계속 제어합니다.</td>
   <td><p>컨텐츠 작성자는 제한된 AEM 컨텐츠 작성 경험으로 제한됩니다.</p> <p>정적 참조나 라우팅이 포함되어 있는 경우 코드를 이식하거나 다시 사용할 수 없을 때 위험합니다.</p> <p>템플릿 편집기를 사용할 수 없으므로 프런트 엔드 개발자가 JCR을 통해 편집 가능한 템플릿을 유지 관리해야 합니다.</p> </td>
  </tr>
  <tr>
   <td>프로젝트는 SPA 편집기 SDK를 완벽하게 활용하며 프런트 엔드 구성 요소를 라이브러리로 개발하여 앱의 콘텐츠 구조를 AEM에 위임합니다.</td>
   <td><p>이 앱은 다시 사용할 수 있고 휴대할 수 있습니다.</p> <p>콘텐츠 제작자는 AEM 콘텐츠 제작 환경을 사용하여 앱을 편집할 수 있습니다.<br /> </p> <p>SPA은 템플릿 편집기와 호환됩니다.</p> </td>
   <td><p>개발자는 앱의 구조와 AEM에 위임된 컨텐츠 부분을 제어하지 않습니다.</p> <p>개발자는 AEM을 사용하여 제작할 계획이 없는 콘텐츠에 대해 앱의 영역을 계속 예약할 수 있습니다.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>모든 모델은 AEM에서 지원되지만, 컨텐츠 작성자는 3차(그리고 AEM](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)에서 권장 [SPA 개발 원칙을 준수함)를 구현해야만 익숙함과 동시에 AEM에서 SPA 컨텐츠를 사용하고 편집할 수 있습니다.
>[](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)

## 기존 SPA을 AEM {#migrating-existing-spas-to-aem}으로 마이그레이션

일반적으로 SPA이 AEM](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)에 대한 [SPA 개발 원칙을 따르는 경우, SPA은 AEM에서 작동하며 AEM SPA 편집기를 사용하여 편집할 수 있습니다.

다음 단계에 따라 기존 SPA에서 AEM을 사용할 수 있도록 준비하십시오.

1. **JS 구성 요소를 모듈식으로 만듭니다.**

   원하는 순서, 위치 및 크기로 렌더링할 수 있습니다.
1. **SDK에서 제공하는 컨테이너를 사용하여 구성 요소를 화면에 배치합니다.**

   AEM에서는 사용할 수 있는 페이지 및 단락 시스템 구성 요소를 제공합니다.
1. **각 JS 구성 요소에 대해 AEM 구성 요소를 만듭니다.**

   AEM 구성 요소는 대화 상자와 JSON 출력을 정의합니다.

## 프런트 엔드 개발자를 위한 지침 {#instructions-for-front-end-developers}

프런트 엔드 개발자에게 AEM용 SPA을 만들기 위한 기본 작업은 구성 요소 및 JSON 모델에 동의해야 합니다.

다음은 AEM용 SPA을 개발할 때 프런트 엔드 개발자가 따라야 하는 단계에 대한 개요입니다.

1. **구성 요소 및 JSON 모델에 동의**

   프런트 엔드 개발자와 백엔드 AEM 개발자는 필요한 구성 요소와 모델에 동의해야 SPA 구성 요소와 백엔드 구성 요소에 대한 1대1 일치를 볼 수 있습니다.

   AEM 구성 요소는 여전히 편집 대화 상자를 제공하고 구성 요소 모델을 내보내는 데 필요합니다.

1. **반응형 구성 요소에서`this.props.cqModel`**

   구성 요소가 동의되고 JSON 모델이 지정되면 프런트 엔드 개발자는 SPA을 무료로 개발할 수 있고 `this.props.cqModel`을(를) 통해 JSON 모델에 간편하게 액세스할 수 있습니다.

1. **구성 요소의 메서드  `render()` 구현**

   프런트 엔드 개발자는 `render()` 메서드를 사용자가 적절하다고 판단하여 구현하고 `cqModel` 속성의 필드를 사용할 수 있습니다. 페이지에 삽입할 DOM 및 HTML 조각을 출력합니다. 이는 React에서 앱을 빌드하는 표준 방법입니다.

1. **구성 요소를`MapTo()`**

   매핑은 구성 요소 클래스를 저장하고 제공된 `Container` 구성 요소에서 내부적으로 사용하여 주어진 리소스 유형에 따라 구성 요소를 검색하고 동적으로 인스턴스화합니다.

   이 기능은 프런트 엔드와 백 엔드 간 &quot;접착제&quot; 역할을 하므로 편집자는 반응형 구성 요소가 일치하는 구성 요소를 파악할 수 있습니다.

   `Page` 및 `ResponsiveGrid`은 기본 `Container`을 확장하는 클래스의 좋은 예입니다.

1. **구성 요소의 매개 변수 `EditConfig` 로 정의`MapTo()`**

   이 매개 변수는 렌더링할 컨텐츠가 없거나 렌더링되지 않는 한 구성 요소의 이름을 지정하는 방법을 편집자에게 알려 주기 위해 필요합니다.

1. **페이지 및 컨테이너에 대해 제공된  `Container` 클래스를 확장합니다.**

   페이지 및 단락 시스템은 내부 구성 요소에 대한 위임이 예상대로 작동하도록 이 클래스를 확장해야 합니다.

1. **HTML5  `History` API를 사용하는 라우팅 솔루션을 구현합니다.**

   `ModelRouter`이(가) 활성화되면 `pushState` 및 `replaceState` 함수를 호출하면 `PageModelManager`에 대한 요청이 트리거되어 모델의 누락된 조각을 가져옵니다.

   `ModelRouter`의 현재 버전은 Sling 모델 진입점의 실제 리소스 경로를 가리키는 URL만 사용할 수 있습니다. 별칭 URL 또는 별칭 사용을 지원하지 않습니다.

   정규 표현식 목록을 무시하도록 `ModelRouter`을 비활성화하거나 구성할 수 있습니다.

## AEM-독립적인 {#aem-agnostic}

이러한 코드 블록은 [반응] 및 [각] 구성 요소에 Adobe 또는 AEM 관련 항목이 필요하지 않음을 보여 줍니다.

* JavaScript 구성 요소 내에 있는 모든 것은 AEM에 관계없이 모든 것입니다.
* 그러나 AEM에만 특화된 것은 JS 구성 요소를 MapTo 도우미로 AEM 구성 요소에 매핑해야 한다는 것입니다.

![screen_shot_2018-12-11at144019](assets/screen_shot_2018-12-11at144019.png)

`MapTo` 도우미는 백엔드 구성 요소와 프런트 엔드 구성 요소를 함께 일치시킬 수 있는 &quot;접착제&quot;입니다.

* JS 컨테이너(또는 JS 단락 시스템)에 JSON에 있는 각 구성 요소를 렌더링할 책임이 있는 JS 구성 요소를 알려줍니다.
* JS 구성 요소가 렌더링하는 HTML에 HTML 데이터 속성을 추가하여 SPA 편집자는 구성 요소를 편집할 때 작성자에게 표시할 대화 상자를 알 수 있습니다.

일반적으로 AEM용 `MapTo` 사용 및 SPA 제작에 대한 자세한 내용은 선택한 프레임워크에 대한 시작하기 안내서를 참조하십시오.

* [AEM에서 SPA 시작하기 - React](/help/sites-developing/spa-getting-started-react.md)
* [AEM에서 SPA 시작하기 - Angular](/help/sites-developing/spa-getting-started-angular.md)

## AEM 아키텍처 및 SPA {#aem-architecture-and-spas}

개발, 저작 및 출판 환경을 포함한 AEM의 일반 아키텍처는 SPA을 사용할 때 변경되지 않습니다. 그러나 SPA 개발이 이 아키텍처에 어떻게 적합한지 이해하는 것이 도움이 됩니다.

![screen_shot_2018-12-11at145348](assets/screen_shot_2018-12-11at145348.png)

* **빌드 환경**

   SPA 애플리케이션 소스 및 구성 요소 소스의 소스가 체크 아웃되는 곳입니다.

   * NPM clientlib 생성기는 SPA 프로젝트에서 클라이언트 라이브러리를 만듭니다.
   * 해당 라이브러리는 Maven이 가져다가 Maven Build 플러그인과 함께 AEM Author에 배포됩니다.

* **AEM Author**

   컨텐츠는 SPA 저작을 포함하여 AEM 작성자에 의해 만들어집니다.

   제작 환경에서 SPA 편집기를 사용하여 SPA을 편집하는 경우:

   1. SPA에서 외부 HTML을 요청합니다.
   1. CSS가 로드됩니다.
   1. SPA 응용 프로그램의 Javascript가 로드됩니다.
   1. SPA 응용 프로그램이 실행되면 JSON이 요청되므로 앱이 `cq-data` 속성을 포함하는 페이지의 DOM을 빌드할 수 있습니다.
   1. 이 `cq-data` 속성을 사용하면 편집자가 구성 요소에 사용할 수 있는 편집 구성을 알 수 있도록 추가 페이지 정보를 로드할 수 있습니다.

* **AEM 게시**

   여기서는 SPA 응용 프로그램 객체, clientlibs 및 구성 요소를 비롯한 제작된 컨텐츠와 컴파일된 라이브러리를 공개 소비에 대해 게시합니다.

* **발송자/CDN**

   디스패처는 사이트 방문자에게 AEM의 캐싱 레이어 역할을 합니다.

   * 요청은 AEM 작성자에 있는 방식과 유사하게 처리되지만 편집자만 필요하므로 페이지 정보에 대한 요청은 없습니다.
   * Javascript, CSS, JSON 및 HTML이 캐시되므로 페이지를 최적화하여 신속하게 전달할 수 있습니다.

>[!NOTE]
>
>AEM 내에서는 Javascript 빌드 메커니즘을 실행하거나 Javascript 자체를 실행할 필요가 없습니다. AEM은 SPA 응용 프로그램에서 컴파일된 가공물만 호스팅합니다.

## 다음 단계 {#next-steps}

AEM에서 단순 SPA의 구조 및 작동 방식에 대한 개요는 [반응](/help/sites-developing/spa-getting-started-react.md) 및 [각](/help/sites-developing/spa-getting-started-angular.md) 모두에 대한 시작 안내서를 참조하십시오.

직접 SPA을 만드는 단계별 안내는 [AEM SPA Editor 시작하기 - WKND 이벤트 자습서](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html)를 참조하십시오.

동적 모델을 구성 요소로 매핑하는 방법 및 AEM에서 작동하는 방식에 대한 자세한 내용은 SPA[의 구성 요소 매핑에 대한 동적 모델 집필을 참조하십시오.](/help/sites-developing/spa-dynamic-model-to-component-mapping.md)

React 또는 Angular 이외의 프레임워크를 위해 AEM에서 SPA을 구현하거나 AEM용 SPA SDK의 작동 방식을 자세히 살펴보려면 [SPA Blueprint](/help/sites-developing/spa-blueprint.md) 문서를 참조하십시오.
