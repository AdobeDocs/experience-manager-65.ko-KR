---
title: 선택 사항 - AEM을 사용하여 단일 페이지 애플리케이션(SPA)을 만드는 방법
description: AEM Headless Developer 여정의 이 선택적 연속에서 AEM에서 기존의 전체 스택 CMS 기능과 헤드리스 게재를 결합하는 방법과 AEM SPA Editor 프레임워크를 사용하여 편집 가능한 SPA을 만드는 방법을 알아봅니다.
exl-id: d74848f2-683e-49e1-9374-32596ca5d7d7
source-git-commit: 7b97bc0ffb0df6641ae71fa36c459f1368052e12
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 5%

---

# AEM을 사용하여 단일 페이지 애플리케이션(SPA)을 만드는 방법 {#create-spa}

이 선택적 연속 [AEM Headless Developer 여정,](overview.md) AEM에서 헤드리스 게재를 기존의 전체 스택 CMS 기능과 결합하는 방법과 AEM SPA Editor 프레임워크를 사용하여 편집 가능한 SPA을 만들고 외부 SPA을 통합하여 필요에 따라 편집 기능을 활성화하는 방법을 살펴볼 수 있습니다.

## 지금까지의 이야기 {#story-so-far}

이 시점에서 전체 [AEM Headless Developer 여정](overview.md) 다음을 이해할 수 있도록 AEM에서 헤드리스 전달의 기본 사항을 이해합니다.

* 헤드리스와 제목이 없는 콘텐츠 전달 간의 차이입니다.
* AEM 헤드리스 기능.
* Headless 프로젝트를 구성하고 AEM 하는 방법입니다.
* AEM에서 헤드리스 컨텐츠를 만드는 방법.
* AEM에서 헤드리스 콘텐츠를 검색하고 업데이트하는 방법입니다.
* AEM Headless 프로젝트를 사용하여 라이브로 전환하는 방법

따라서 이제 첫 번째 AEM Headless 프로젝트로 라이브로 전환되거나 그렇게 하는 데 필요한 모든 지식이 제공됩니다. 축하합니다!

그렇다면 왜 이 여정의 추가적인 선택적 연속 내용을 읽고 있습니까? 아마 당신은 [시작하기](getting-started.md#integration-levels) AEM에서 헤드리스 게재 및 기존의 전체 스택 모델을 지원할 뿐만 아니라 두 가지 장점을 결합하는 하이브리드 모델을 지원하는 방법에 대해 간략하게 설명합니다. 기존의 헤드리스 모델은 아니지만 이러한 하이브리드 모델은 특정 프로젝트에 전례 없는 유연성을 제공할 수 있습니다.

이 문서는 AEM에서 실제로 편집할 수 있는 고유한 단일 페이지 애플리케이션(SPA)을 만드는 방법을 심층적으로 탐색하여 AEM Headless에 대한 지식을 기반으로 합니다. 이러한 방식으로 컨텐츠를 만들고 헤딩 없이 SPA으로 전달할 수 있지만, 해당 SPA은 AEM에서 편집할 수 있습니다.

## 목표 {#objective}

이 문서는 AEM SPA 편집기 프레임워크를 사용하여 단일 페이지 애플리케이션을 개발하는 방법을 이해하는 데 도움이 됩니다. 이 문서를 읽고 나면

* SPA 편집기의 기본 기능을 이해합니다.
* 편집 가능한 SPA for AEM을 빌드하기 위한 요구 사항을 알아봅니다.
* 외부 SPA을 AEM에 통합하는 방법을 이해합니다.
* 서버 측 렌더링을 구현하거나 구현하지 않아야 하는 방법을 이해합니다.

## 요구 사항 및 사전 요구 사항 {#requirements-prerequisites}

AEM에서 SPA 작업을 시작하기 전에 많은 요구 사항이 있습니다.

### 지식 {#knowledge}

* React 또는 Angular 프레임워크을 사용하여 SPA을 만드는 개발 경험
* 컨텐츠 조각을 만들고 편집기를 사용하는 기본 AEM 기술
* 반드시 문서를 검토하세요 [AEM의 헤드리스 및 헤드리스](/help/sites-developing/headful-headless.md) SPA 통합의 다양한 수준을 이해하기 위해 사용할 수 있습니다.

### 도구 {#tools}

* 프로젝트 배포를 테스트하는 샌드박스 액세스
* 데이터 모델링 및 테스트를 위한 로컬 개발 인스턴스
* 기존 외부 SPA(선택한 통합 모델에 따라 선택 사항)
* AEM Project Archetype

## SPA란? {#what-is-a-spa}

단일 페이지 애플리케이션(SPA)은 클라이언트측에서 렌더링되고 주로 Javascript 기반이라는 기존 페이지와 다르며, Ajax 호출에 의존하여 데이터를 로드하고 페이지를 동적으로 업데이트합니다. 대부분의 또는 모든 컨텐츠는 페이지와의 사용자 상호 작용에 따라 필요에 따라 비동기식으로 로드되는 추가 리소스와 함께 단일 페이지 로드에서 한 번 검색됩니다.

이를 통해 페이지를 새로 고칠 필요가 줄어들고 사용자에게 매끄럽고 빠르며 기본 앱 환경과 같은 경험을 제공할 수 있습니다.

프런트엔드 개발자는 AEM SPA 편집기를 사용하여 AEM 사이트에 통합할 수 있는 SPA을 만들어 컨텐츠 작성자가 다른 AEM 컨텐츠처럼 쉽게 SPA 컨텐츠를 편집할 수 있습니다.

## 왜 SPA인가? {#why-spa}

빠르고 유동적이며 네이티브 애플리케이션과 유사하게 SPA은 웹 페이지의 방문자뿐만 아니라 SPA 작동 방식의 특성으로 인해 마케터와 개발자에게도 매우 매력적인 경험이 됩니다.

SPA에 대한 전체 설명 및를 사용하는 이유는 다음을 참조하십시오. [추가 리소스](#additional-resources) 섹션을 참조하십시오.

## AEM에서 SPA을 처리하는 방법

AEM에서 단일 페이지 애플리케이션을 개발하는 경우 프런트 엔드 개발자는 SPA을 만들 때 표준 우수 사례를 관찰한다고 가정합니다. 프런트 엔드 개발자로서 이러한 일반 모범 사례와 몇 가지 AEM 관련 원칙을 따르는 경우 SPA은 AEM 및 콘텐츠 작성 기능을 통해 사용할 수 있습니다.

* **휴대성** - 모든 컴포넌트와 마찬가지로 SPA 컴포넌트를 최대한 휴대할 수 있도록 제작해야 합니다. SPA은 휴대용 및 재사용 가능한 구성 요소로 구축되어야 합니다.
* **AEM 드라이브 사이트 구조** - 프런트 엔드 개발자는 구성 요소를 만들고 내부 구조를 소유하지만, AEM을 사용하여 사이트의 컨텐츠 구조를 정의합니다.
* **동적 렌더링** - 모든 렌더링은 동적이여야 합니다.
* **동적 라우팅** - SPA은 라우팅을 담당하고 AEM은 이를 바탕으로 라우팅을 수신합니다. 모든 라우팅도 동적이여야 합니다.

AEM에서 SPA을 처리하는 방법에 대한 자세한 내용은 [추가 리소스](#additional-resources) 섹션을 참조하십시오.

## AEM SPA 편집기 {#aem-spa-editor}

React 및 Angular과 같은 일반적인 SPA 프레임워크을 사용하여 작성된 사이트는 다이내믹 JSON을 통해 컨텐츠를 로드하고 AEM 페이지 편집기에서 편집 컨트롤을 배치하는 데 필요한 HTML 구조를 제공하지 않습니다.

AEM 내에서 SPA을 편집할 수 있도록 하려면 SPA의 JSON 출력과 AEM 저장소의 컨텐츠 모델 간의 매핑이 컨텐츠의 변경 사항을 저장해야 합니다.

AEM의 SPA 지원에서는 이벤트를 전송할 수 있는 페이지 편집기에서 로드할 때 SPA JS 코드와 상호 작용하는 가상 JS 계층을 소개하고 편집 컨트롤의 위치를 활성화하여 컨텍스트 내 편집을 허용합니다. 이 기능은 SPA의 컨텐츠를 Content Services를 통해 로드해야 하므로 Content Services API Endpoint 개념을 기반으로 합니다.

AEM SPA 편집기에 대한 전체 설명은 [추가 리소스](#additional-resources) 섹션을 참조하십시오.

## 기존 SPA 수용 {#existing-spas}

기존 SPA이 있는 경우 AEM에서는 AEM에 포함할 수 있으므로 AEM 편집기에서 컨텐츠 작성자가 볼 수 있습니다. 이 기능은 사용할 최종 애플리케이션 컨텍스트에서 컨텐츠 조각을 통해 만드는 컨텐츠를 보는 데 매우 유용합니다.

또한 작은 변경 사항만 있으면 AEM 편집기 내에서 외부 SPA에 대해 특정 편집 기능을 활성화할 수 있습니다.

RemotePage 구성 요소를 사용하면 AEM에서 외부 SPA을 렌더링할 수 있습니다.

AEM에서 외부 SPA을 편집 가능하게 만드는 방법에 대한 전체 설명은 다음을 참조하십시오. [추가 리소스](#additional-resources) 섹션을 참조하십시오.

## 다음 단계 {#what-is-next}

고유한 SPA for AEM 개발을 시작하려면 다음 문서를 검토하십시오.

* [SPA WKND 튜토리얼](/help/sites-developing/spa-wknd.md)
* [React 사용 시작](/help/sites-developing/spa-getting-started-react.md)
* [angular 사용 시작](/help/sites-developing/spa-getting-started-angular.md)

AEM에서 사용하려면 기존 SPA을 조정해야 하는 경우 다음 문서를 검토하십시오.

* [RemotePage 구성 요소](/help/sites-developing/spa-remote-page.md)
* [AEM에서 외부 SPA 편집](/help/sites-developing/spa-edit-external.md)

아래 참조: [추가 리소스](#additional-resources) AEM의 SPA 주제를 자세히 살펴봅니다.

## 추가 리소스 {#additional-resources}

다음은 이 문서에서 언급한 몇 가지 개념에 대해 자세히 설명하는 몇 가지 추가 리소스입니다.

* [AEM의 헤드리스 및 헤드리스](/help/sites-developing/headful-headless.md) - AEM에서 사용할 수 있는 다양한 게재 모델에 대한 설명입니다
* [SPA 소개 및 워크스루.](/help/sites-developing/spa-walkthrough.md) AEM에서 SPA을 잘 소개하다
* [SPA for AEM 개발](/help/sites-developing/spa-architecture.md) - SPA for AEM 개발 지침
* [SPA 편집기 개요](/help/sites-developing/spa-overview.md) - SPA 편집기 작동 방식 세부 사항
* [서버 측 렌더링](/help/sites-developing/spa-ssr.md) - AEM SPA용 SSR을 구성하는 방법
* [SPA 참조 문서](/help/sites-developing/spa-reference-materials.md) - JavaScript API가 열려 있는 소스 AEM SPA GitHub 프로젝트에 대한 참조 및 링크
* [컨텐츠 조각](/help/assets/content-fragments/content-fragments.md) - 컨텐츠 조각을 만드는 방법
* [AEM 프로젝트 원형](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) - 웹 사이트의 시작점으로 최소한의 우수 사례 기반 Adobe Experience Manager(AEM) 프로젝트를 만드는 Maven 템플릿
