---
title: SPA 편집기 개요
seo-title: SPA Editor Overview
description: 이 문서에서는 SPA 편집기에 대한 포괄적인 개요를 제공하며 AEM 내에서 SPA 편집기의 상호 작용에 대한 세부 워크플로우를 포함하는 작동 방식을 설명합니다.
seo-description: This article gives a comprehensive overview of the SPA Editor and how it works included detailed workflows of interaction of the SPA Editor within AEM.
uuid: c283abab-f5bc-414a-bc81-bf3bdce38534
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 06b8c0be-4362-4bd1-ad57-ea5503616b17
docset: aem65
exl-id: 7b34be66-bb61-4697-8cc8-428f7c63a887
source-git-commit: a547b2e24205c63284a0e77f2e7f5678ae24968b
workflow-type: tm+mt
source-wordcount: '1657'
ht-degree: 1%

---

# SPA 편집기 개요{#spa-editor-overview}

SPA(단일 페이지 애플리케이션)는 웹 사이트 사용자에게 훌륭한 경험을 제공할 수 있습니다. 개발자는 SPA 프레임워크을 사용하여 사이트를 작성하려고 하며 작성자는 이러한 프레임워크를 사용하여 작성된 사이트의 AEM 내에서 컨텐츠를 원활하게 편집하려고 합니다.

SPA 편집기는 AEM 내에서 SPA을 지원하는 포괄적인 솔루션을 제공합니다. 이 페이지에서는 SPA 지원이 AEM에서 구조화되는 방법, SPA 편집기의 작동 방식, SPA 프레임워크 및 AEM을 동기화하는 방법에 대한 개요를 제공합니다.

>[!NOTE]
>
>SPA 편집기는 SPA 프레임워크 기반 클라이언트측 렌더링(예: React 또는 Angular)이 필요한 프로젝트에 권장되는 솔루션입니다.

## 소개 {#introduction}

React 및 Angular과 같은 일반적인 SPA 프레임워크을 사용하여 작성된 사이트는 다이내믹 JSON을 통해 컨텐츠를 로드하고 AEM 페이지 편집기에서 편집 컨트롤을 배치하는 데 필요한 HTML 구조를 제공하지 않습니다.

AEM 내에서 SPA을 편집할 수 있도록 하려면 SPA의 JSON 출력과 AEM 저장소의 컨텐츠 모델 간의 매핑이 컨텐츠의 변경 사항을 저장해야 합니다.

AEM의 SPA 지원에서는 이벤트를 전송할 수 있는 페이지 편집기에서 로드할 때 SPA JS 코드와 상호 작용하는 가상 JS 계층을 소개하고 편집 컨트롤의 위치를 활성화하여 컨텍스트 내 편집을 허용합니다. 이 기능은 SPA의 컨텐츠를 Content Services를 통해 로드해야 하므로 Content Services API Endpoint 개념을 기반으로 합니다.

AEM에서 SPA에 대한 자세한 내용은 다음 문서를 참조하십시오.

* [SPA 블루프린트](/help/sites-developing/spa-blueprint.md) SPA의 기술 요구 사항
* [AEM에서 SPA 시작하기](/help/sites-developing/spa-getting-started-react.md) 간단한 SPA 투어로

## 디자인 {#design}

SPA용 페이지 구성 요소에서는 JSP 또는 HTL 파일을 통해 하위 구성 요소의 HTML 요소를 제공하지 않습니다. 이 작업은 SPA 프레임워크에 위임됩니다. 하위 구성 요소 또는 모델의 표현은 JCR에서 JSON 데이터 구조로 가져옵니다. 그런 다음 SPA 구성 요소가 해당 구조에 따라 페이지에 추가됩니다. 이 동작은 페이지 구성 요소의 초기 본문 컴포지션과 SPA이 아닌 상대성을 구별합니다.

### 페이지 모델 관리 {#page-model-management}

페이지 모델의 해결 방법 및 관리가 제공된 `PageModel` 라이브러리. SPA Editor에서 초기화하고 작성하려면 SPA에서 페이지 모델 라이브러리를 사용해야 합니다. 페이지 모델 라이브러리는 를 통해 AEM 페이지 구성 요소에 간접적으로 제공됩니다 `aem-react-editable-components` npm. 페이지 모델은 AEM과 SPA 간의 인터프리터이므로 항상 존재해야 합니다. 페이지가 작성되면 추가 라이브러리가 제공됩니다 `cq.authoring.pagemodel.messaging` 페이지 편집기와의 통신을 활성화하려면 를 추가해야 합니다.

SPA 페이지 구성 요소가 페이지 코어 구성 요소에서 상속되는 경우 다음과 같은 두 가지 옵션을 사용할 수 있습니다 `cq.authoring.pagemodel.messaging` 클라이언트 라이브러리 범주 사용 가능:

* 템플릿을 편집할 수 있는 경우 페이지 정책에 추가합니다.
* 또는 `customfooterlibs.html`.

내보낸 모델의 각 리소스에 대해 SPA은 렌더링을 수행할 실제 구성 요소를 매핑합니다. JSON으로 표시되는 모델은 컨테이너 내에서 구성 요소 매핑을 사용하여 렌더링됩니다.
![screen_shot_2018-08-20at144152](assets/screen_shot_2018-08-20at144152.png)

>[!CAUTION]
>
>의 포함 `cq.authoring.pagemodel.messaging` 카테고리는 SPA 편집기의 컨텍스트로 제한되어야 합니다.

### 통신 데이터 유형 {#communication-data-type}

이 `cq.authoring.pagemodel.messaging` 카테고리가 페이지에 추가되면 JSON 통신 데이터 유형을 설정하기 위해 페이지 편집기에 메시지를 보냅니다. 통신 데이터 유형이 JSON으로 설정되면 GET 요청은 구성 요소의 Sling Model 엔드포인트와 통신됩니다. 페이지 편집기에서 업데이트가 발생하면 업데이트된 구성 요소의 JSON 표현이 페이지 모델 라이브러리로 전송됩니다. 그러면 페이지 모델 라이브러리가 SPA에 업데이트를 알려줍니다.

![screen_shot_2018-08-20at143628](assets/screen_shot_2018-08-20at143628.png)

## 워크플로 {#workflow}

SPA Editor를 두 Target의 매개로 하여 SPA과 AEM 간의 상호 작용 흐름을 파악할 수 있습니다.

* 페이지 편집기와 SPA 간의 통신은 HTML 대신 JSON을 사용하여 수행됩니다.
* 페이지 편집기는 iframe 및 messaging API를 통해 SPA에 최신 버전의 페이지 모델을 제공합니다.
* 페이지 모델 관리자는 편집 준비가 되었음을 편집기에 알리고 페이지 모델을 JSON 구조로 전달합니다.
* 편집기는 최신 페이지 모델을 제공하는 것이 아니라 작성 중인 페이지의 DOM 구조를 변경하거나 심지어 액세스하지도 않습니다.

![screen_shot_2018-08-20at144324](assets/screen_shot_2018-08-20at144324.png)

### 기본 SPA 편집기 워크플로우 {#basic-spa-editor-workflow}

SPA 편집기의 주요 요소를 고려하여 AEM 내에서 SPA을 편집하는 높은 수준의 워크플로우가 다음과 같이 작성자에게 표시됩니다.

![제목 없음1](assets/untitled1.gif)

1. SPA 편집기가 로드됩니다.
1. SPA은 별도의 프레임에 로드됩니다.
1. SPA은 JSON 콘텐츠를 요청하고 구성 요소를 클라이언트측에서 렌더링합니다.
1. SPA 편집기는 렌더링된 구성 요소를 감지하고 오버레이를 생성합니다.
1. 작성자가 오버레이를 클릭하여 구성 요소의 편집 도구 모음을 표시합니다.
1. SPA 편집기는 서버에 대한 POST 요청과 함께 편집 내용을 유지합니다.
1. SPA Editor 요청은 SPA Editor로 JSON이 업데이트되어 DOM 이벤트와 함께 SPA으로 전송됩니다.
1. SPA은 관련 구성 요소를 다시 렌더링하여 DOM을 업데이트합니다.

>[!NOTE]
>
>주의 사항:
>
>* SPA은 항상 디스플레이를 담당합니다.
>* SPA 편집기는 SPA 자체에서 분리되어 있습니다.
>* 프로덕션(게시)에서는 SPA 편집기가 로드되지 않습니다.
>


### 클라이언트 서버 페이지 편집 워크플로우 {#client-server-page-editing-workflow}

SPA을 편집할 때 클라이언트-서버 상호 작용에 대한 자세한 개요입니다.

![page_editor_spa_authoringmediator-2](assets/page_editor_spa_authoringmediator-2.png)

1. SPA은 자체 초기화하고 Sling Model Exporter에서 페이지 모델을 요청합니다.
1. Sling 모델 익스포터가 저장소에서 페이지를 구성하는 리소스를 요청합니다.
1. 저장소가 리소스를 반환합니다.
1. Sling 모델 익스포터가 페이지의 모델을 반환합니다.
1. SPA은 페이지 모델을 기반으로 해당 구성 요소를 인스턴스화합니다.
1. **6a** 컨텐츠는 작성 준비가 되었음을 편집기에 알려줍니다.

   **6b** 페이지 편집기가 구성 요소 작성 구성을 요청합니다.

   **6c** 페이지 편집기가 구성 요소 구성을 수신합니다.
1. 작성자가 구성 요소를 편집하면 페이지 편집기가 기본 POST 서블릿에 수정 요청을 게시합니다.
1. 리소스는 리포지토리에서 업데이트됩니다.
1. 업데이트된 리소스가 POST 서블릿에 제공됩니다.
1. 기본 POST 서블릿은 리소스가 업데이트되었음을 페이지 편집기에 알려줍니다.
1. 페이지 편집기가 새 페이지 모델을 요청합니다.
1. 페이지를 구성하는 리소스는 저장소에서 요청됩니다.
1. 페이지를 구성하는 리소스는 저장소에서 Sling 모델 익스포터에 제공됩니다.
1. 업데이트된 페이지 모델이 편집기로 반환됩니다.
1. 페이지 편집기는 SPA의 페이지 모델 참조를 업데이트합니다.
1. SPA은 새 페이지 모델 참조를 기반으로 해당 구성 요소를 업데이트합니다.
1. 페이지 편집기의 구성 요소 구성이 업데이트됩니다.

   **17a** SPA은 페이지 편집기에 컨텐츠가 준비되었음을 알립니다.

   **17b** 페이지 편집기는 SPA에 구성 요소 구성을 제공합니다.

   **17c** SPA은 업데이트된 구성 요소 구성을 제공합니다.

### 작성 워크플로우 {#authoring-workflow}

작성 환경에 중점을 둔 보다 자세한 개요입니다.

![spa_content_authoringmodel](assets/spa_content_authoringmodel.png)

1. SPA은 페이지 모델을 가져옵니다.
1. **2a** 페이지 모델은 작성에 필요한 데이터를 편집기에 제공합니다.

   **2b** 알림 시 구성 요소 오케스트레이터는 페이지의 컨텐츠 구조를 업데이트합니다.
1. 구성 요소 오케스트레이터는 AEM 리소스 유형과 SPA 구성 요소 간의 매핑을 질의합니다.
1. 구성 요소 오케스트레이터는 페이지 모델 및 구성 요소 매핑을 기반으로 SPA 구성 요소를 동적으로 인스턴스화합니다.
1. 페이지 편집기는 페이지 모델을 업데이트합니다.
1. **6a** 페이지 모델은 업데이트된 작성 데이터를 페이지 편집기에 제공합니다.

   **6b** 페이지 모델은 구성 요소 오케스트레이터에 변경 사항을 전달합니다.
1. 구성 요소 오케스트레이터가 구성 요소 매핑을 가져옵니다.
1. 구성 요소 오케스트레이터는 페이지의 컨텐츠를 업데이트합니다.
1. SPA이 페이지의 컨텐츠 업데이트를 완료하면 페이지 편집기가 작성 환경을 로드합니다.

## 요구 사항 및 제한 사항 {#requirements-limitations}

작성자가 페이지 편집기를 사용하여 SPA의 컨텐츠를 편집할 수 있도록 하려면 SPA Editor SDK와 상호 작용하려면 AEM 애플리케이션을 구현해야 합니다. 자세한 내용은 [AEM에서 SPA 시작하기](/help/sites-developing/spa-getting-started-react.md) 실행 중인 문서를 실행하기 위해 알아야 하는 최소 문서를 참조하십시오.

### 지원되는 프레임워크 {#supported-frameworks}

SPA Editor SDK는 다음과 같은 최소 버전을 지원합니다.

* React 16.x 이상
* Angular 6.x 이상

이러한 프레임워크의 이전 버전은 AEM SPA Editor SDK에서 사용할 수 있지만 지원되지 않습니다.

### 추가 프레임워크 {#additional-frameworks}

AEM SPA Editor SDK에서 작동하도록 추가 SPA 프레임워크을 구현할 수 있습니다. 자세한 내용은 [SPA 블루프린트](/help/sites-developing/spa-blueprint.md) AEM SPA Editor에서 작업할 모듈, 구성 요소 및 서비스로 구성된 프레임워크별 레이어를 생성하기 위해 프레임워크가 수행해야 하는 요구 사항에 대한 문서입니다.

### 여러 선택기 사용 {#multiple-selectors}

추가 사용자 지정 선택기는 AEM SPA SDK용으로 개발된 SPA의 일부로 정의하고 사용할 수 있습니다. 그러나 이 지원을 사용하려면 `model` 선택기는 첫 번째 선택기가 되고 확장은 다음 `.json` 로서의 [JSON Exporter에 필요합니다.](json-exporter-components.md#multiple-selectors)

### 텍스트 편집기 요구 사항 {#text-editor-requirements}

SPA에서 만든 텍스트 구성 요소의 즉석 편집기를 사용하려면 추가 구성이 필요합니다.

1. 텍스트 HTML을 포함하는 컨테이너 래퍼 요소에서 속성(임의의 항목일 수 있음)을 설정합니다. WKND Journal 샘플 컨텐츠의 경우, `<div>` 요소 및 사용된 선택기는 `data-rte-editelement`.
1. 구성 설정 `editElementQuery` 해당 AEM 텍스트 구성 요소의 `cq:InplaceEditingConfig` 해당 선택기를 가리킵니다(예: ). `data-rte-editelement`. 이렇게 하면 편집기에서 HTML 텍스트를 래핑하는 HTML 요소를 알 수 있습니다.

이 작업의 예는 를 참조하십시오. [WKND 저널 샘플 컨텐츠.](https://github.com/adobe/aem-sample-we-retail-journal/pull/16/files)

에 대한 추가 정보 `editElementQuery` 속성 및 리치 텍스트 편집기의 구성은 [리치 텍스트 편집기를 구성합니다.](/help/sites-administering/rich-text-editor.md)

### 제한 사항 {#limitations}

AEM SPA Editor SDK에는 AEM 6.4 서비스 팩 2가 도입되었습니다. Adobe에서 완전히 지원되며 지속적으로 향상되고 확장됩니다. 다음 AEM 기능은 아직 SPA 편집기에서 지원되지 않습니다.

* Target 모드
* ContextHub
* 인라인 이미지 편집
* 구성 편집(예: listener)
* 실행 취소/다시 실행
* 페이지 비교 및 시간 비틀기
* 링크 확인, CDN 재작성기 서비스, URL 단축 등과 같이 HTML 재작성을 수행하는 기능입니다.
* 개발자 모드
* AEM 실행
