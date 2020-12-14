---
title: SPA 편집기 개요
seo-title: SPA 편집기 개요
description: 이 문서에서는 SPA 편집기에 대한 포괄적인 개요 및 AEM에서 SPA 편집기의 인터랙션 워크플로우에 대한 자세한 내용을 제공합니다.
seo-description: 이 문서에서는 SPA 편집기에 대한 포괄적인 개요 및 AEM에서 SPA 편집기의 인터랙션 워크플로우에 대한 자세한 내용을 제공합니다.
uuid: c283abab-f5bc-414a-bc81-bf3bdce38534
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 06b8c0be-4362-4bd1-ad57-ea5503616b17
docset: aem65
translation-type: tm+mt
source-git-commit: 4c9a0bd73e8d87d3869c6a133f5d1049f8430cd1
workflow-type: tm+mt
source-wordcount: '1691'
ht-degree: 1%

---


# SPA 편집기 개요{#spa-editor-overview}

단일 페이지 애플리케이션(SPA)을 통해 웹 사이트 사용자에게 매력적인 경험을 제공할 수 있습니다. 개발자는 SPA 프레임워크을 사용하여 사이트를 구축하고자 하며, 작성자는 이러한 프레임워크를 사용하여 구축된 사이트에서 AEM의 컨텐츠를 매끄럽게 편집하고자 합니다.

SPA Editor는 AEM 내에서 SPA을 지원하는 포괄적인 솔루션을 제공합니다. 이 페이지에서는 SPA 지원이 AEM에서 구조화되는 방식, SPA 편집기의 작동 방식, SPA 프레임워크과 AEM의 동기화 방식을 대략적으로 설명합니다.

>[!NOTE]
>
>SPA 편집기는 SPA 프레임워크 기반의 클라이언트측 렌더링(예: 반응형 또는 각도)이 필요한 프로젝트에 권장되는 솔루션입니다.

## 소개 {#introduction}

동적 JSON을 통해 React 및 Angular Load와 같은 일반적인 SPA 프레임워크을 사용하여 구축한 사이트는 컨텐츠를 작성하고 AEM 페이지 편집기가 편집 컨트롤을 배치하는 데 필요한 HTML 구조를 제공하지 않습니다.

AEM 내에서 SPA을 편집하려면 컨텐트에 대한 변경 내용을 저장하려면 SPA의 JSON 출력과 AEM 저장소의 컨텐츠 모델 간 매핑이 필요합니다.

AEM의 SPA 지원은 페이지 편집기에서 로드할 때 SPA JS 코드와 상호 작용하는 가상 JS 레이어를 도입하며, 여기서 이벤트를 전송할 수 있고 편집 컨트롤의 위치를 상황에 맞는 편집을 허용할 수 있습니다. 이 기능은 SPA의 컨텐츠를 컨텐츠 서비스를 통해 로드해야 하므로 Content Services API 끝점 개념을 기반으로 구축됩니다.

AEM에서 SPA에 대한 자세한 내용은 다음 문서를 참조하십시오.

* [SPA ](/help/sites-developing/spa-blueprint.md) Blueprinting - SPA의 기술 요구 사항
* [AEM에서 SPA ](/help/sites-developing/spa-getting-started-react.md) 시작하기 간단한 SPA 둘러보기

## 디자인 {#design}

SPA용 페이지 구성 요소는 JSP 또는 HTL 파일을 통해 하위 구성 요소의 HTML 요소를 제공하지 않습니다. 이 작업은 SPA 프레임워크에 위임됩니다. 하위 구성 요소 또는 모델의 표시는 JCR에서 JSON 데이터 구조로 가져옵니다. 그런 다음 SPA 구성 요소가 해당 구조에 따라 페이지에 추가됩니다. 이 동작은 페이지 구성 요소의 초기 본문 컴포지션을 SPA이 아닌 것과 구별합니다.

### 페이지 모델 관리 {#page-model-management}

페이지 모델의 해상도 및 관리는 제공된 `PageModel` 라이브러리에 위임됩니다. SPA 편집기에서 초기화하여 제작하려면 SPA에서 페이지 모델 라이브러리를 사용해야 합니다. 페이지 모델 라이브러리는 `aem-react-editable-components` npm을 통해 AEM 페이지 구성 요소에 간접적으로 제공됩니다. 페이지 모델은 AEM과 SPA 간의 인터프리터이므로 항상 존재해야 합니다. 페이지를 작성할 때 페이지 편집기와의 통신을 활성화하려면 추가 라이브러리 `cq.authoring.pagemodel.messaging`을(를) 추가해야 합니다.

SPA 페이지 구성 요소가 페이지 핵심 구성 요소에서 상속되는 경우 `cq.authoring.pagemodel.messaging` 클라이언트 라이브러리 범주를 사용할 수 있도록 하는 두 가지 옵션이 있습니다.

* 템플릿을 편집할 수 있는 경우 페이지 정책에 추가합니다.
* 또는 `customfooterlibs.html`을 사용하여 카테고리를 추가합니다.

내보낸 모델의 각 리소스에 대해 SPA은
렌더링. 그런 다음 JSON으로 표현되는 모델은 컨테이너 내의 구성 요소 매핑을 사용하여 렌더링됩니다.
![screen_shot_2018-08-20at144152](assets/screen_shot_2018-08-20at144152.png)

>[!CAUTION]
>
>`cq.authoring.pagemodel.messaging` 카테고리의 포함은 SPA 편집기의 컨텍스트에 한정되어야 합니다.

### 통신 데이터 유형 {#communication-data-type}

`cq.authoring.pagemodel.messaging` 카테고리가 페이지에 추가되면 JSON 커뮤니케이션 데이터 유형을 설정하기 위해 페이지 편집기에 메시지를 보냅니다. 통신 데이터 유형이 JSON으로 설정되면 GET 요청은 구성 요소의 Sling Model 끝점과 통신합니다. 페이지 편집기에서 업데이트가 발생하면 업데이트된 구성 요소의 JSON 표현이 페이지 모델 라이브러리로 전송됩니다. 그런 다음 페이지 모델 라이브러리가 SPA에 업데이트를 알려줍니다.

![screen_shot_2018-08-20at143628](assets/screen_shot_2018-08-20at143628.png)

## 워크플로우 {#workflow}

두 프로그램 간의 중재자로 SPA Editor를 생각하여 SPA과 AEM 간의 상호 작용의 흐름을 파악할 수 있습니다.

* 페이지 편집기와 SPA 간의 통신은 HTML 대신 JSON을 사용하여 수행됩니다.
* 페이지 편집기는 iframe 및 messaging API를 통해 최신 버전의 페이지 모델을 SPA에 제공합니다.
* 페이지 모델 관리자는 편집할 준비가 되었음을 편집자에게 알리고 페이지 모델을 JSON 구조로 전달합니다.
* 편집기는 최신 페이지 모델을 제공하는 대신 작성 중인 페이지의 DOM 구조를 변경하거나 심지어 액세스할 수도 없습니다.

![screen_shot_2018-08-20at144324](assets/screen_shot_2018-08-20at144324.png)

### 기본 SPA 편집기 워크플로 {#basic-spa-editor-workflow}

SPA Editor의 주요 요소를 염두에 두면 AEM에서 SPA을 편집하는 고급 워크플로우가 다음과 같이 작성자에게 표시됩니다.

![제목 없음1](assets/untitled1.gif)

1. SPA 편집기가 로드됩니다.
1. SPA은 별도의 프레임으로 로드됩니다.
1. SPA은 JSON 콘텐츠를 요청하고 구성 요소를 클라이언트측에서 렌더링합니다.
1. SPA 편집기는 렌더링된 구성 요소를 감지하고 오버레이를 생성합니다.
1. 작성자가 오버레이를 클릭하고 구성 요소의 편집 도구 모음을 표시합니다.
1. SPA 편집기는 서버에 대한 POST 요청과 함께 편집한 내용을 유지합니다.
1. SPA 편집기 요청이 SPA 편집기에 업데이트된 JSON을 요청합니다. 이 요청은 DOM 이벤트가 있는 SPA으로 전송됩니다.
1. SPA은 관련 구성 요소를 다시 렌더링하여 DOM을 업데이트합니다.

>[!NOTE]
>
>주의 사항:
>
>* SPA은 항상 그 디스플레이를 담당한다.
>* SPA 편집기는 SPA 자체에서 분리됩니다.
>* 제작(게시)에서는 SPA 편집기가 로드되지 않습니다.

>



### 클라이언트-서버 페이지 편집 워크플로 {#client-server-page-editing-workflow}

SPA을 편집할 때 클라이언트-서버 상호 작용에 대한 자세한 개요입니다.

![page_editor_spa_authoringmediator-2](assets/page_editor_spa_authoringmediator-2.png)

1. SPA은 자체적으로 초기화하고 Sling 모델 내보내기 도구에서 페이지 모델을 요청합니다.
1. Sling 모델 익스포터는 저장소에서 페이지를 구성하는 리소스를 요청합니다.
1. 저장소가 리소스를 반환합니다.
1. Sling Model Exporter는 페이지의 모델을 반환합니다.
1. SPA에서는 페이지 모델을 기반으로 구성 요소를 인스턴스화합니다.
1. **6** a컨텐츠는 편집기에 작성할 준비가 되었음을 알려줍니다.

   **6** b페이지 편집기가 구성 요소 작성 구성을 요청합니다.

   **6** c페이지 편집기는 구성 요소 구성을 수신합니다.
1. 작성자가 구성 요소를 편집할 때 페이지 편집기는 수정 요청을 기본 POST 서블릿에 게시합니다.
1. 리소스가 저장소에서 업데이트됩니다.
1. 업데이트된 리소스가 POST 서블릿에 제공됩니다.
1. 기본 POST 서블릿은 리소스가 업데이트되었음을 페이지 편집기에 알려줍니다.
1. 페이지 편집기가 새 페이지 모델을 요청합니다.
1. 페이지를 구성하는 리소스는 저장소에서 요청됩니다.
1. 페이지를 구성하는 리소스는 저장소에서 Sling 모델 내보내기 도구에 의해 제공됩니다.
1. 업데이트된 페이지 모델이 편집기에 반환됩니다.
1. 페이지 편집기는 SPA의 페이지 모델 참조를 업데이트합니다.
1. SPA은 새 페이지 모델 참조를 기반으로 구성 요소를 업데이트합니다.
1. 페이지 편집기의 구성 요소 구성이 업데이트됩니다.

   **17** aSPA은 페이지 편집기에 컨텐츠가 준비되었음을 알립니다.

   **17** b페이지 편집기는 SPA에 구성 요소 구성을 제공합니다.

   **17** cSPA은 업데이트된 구성 요소 구성을 제공합니다.

### 작성 워크플로 {#authoring-workflow}

작성 환경에 초점을 둔 자세한 개요입니다.

![spa_content_authoringmodel](assets/spa_content_authoringmodel.png)

1. SPA은 페이지 모델을 가져옵니다.
1. **2** a페이지 모델은 작성에 필요한 데이터를 편집기에 제공합니다.

   **2** b알림을 받으면 구성 요소 오케스트레이터는 페이지의 컨텐츠 구조를 업데이트합니다.
1. 구성 요소 오케스트레이터는 AEM 리소스 유형과 SPA 구성 요소 간의 매핑을 쿼리합니다.
1. 구성 요소 오케스트레이터는 페이지 모델 및 구성 요소 매핑을 기반으로 SPA 구성 요소를 동적으로 인스턴스화합니다.
1. 페이지 편집기가 페이지 모델을 업데이트합니다.
1. **6** a페이지 모델은 페이지 편집기에 업데이트된 작성 데이터를 제공합니다.

   **6** b페이지 모델은 구성 요소 오케스트레이터에 변경 사항을 전달합니다.
1. 구성 요소 오케스트레이터는 구성 요소 매핑을 가져옵니다.
1. 구성 요소 오케스트레이터는 페이지의 컨텐츠를 업데이트합니다.
1. SPA에서 페이지의 컨텐츠 업데이트를 완료하면 페이지 편집기가 작성 환경을 로드합니다.

## 요구 사항 및 제한 사항 {#requirements-limitations}

작성자가 페이지 편집기를 사용하여 SPA의 컨텐츠를 편집할 수 있도록 하려면 AEM SPA 편집기 SDK와 상호 작용하기 위해 SPA 애플리케이션을 구현해야 합니다. SPA의 ](/help/sites-developing/spa-getting-started-react.md) 시작에서 [AEM을 사용하여 시작하기를 참조하십시오.

### 지원되는 프레임워크 {#supported-frameworks}

SPA 편집기 SDK는 다음과 같은 최소 버전을 지원합니다.

* 16.x 이상 반응
* 각 6.x 이상

이러한 프레임워크의 이전 버전은 AEM SPA Editor SDK에서 사용할 수 있지만 지원되지 않습니다.

### 추가 프레임워크 {#additional-frameworks}

AEM SPA Editor SDK에서 작동하도록 추가 SPA 프레임워크을 구현할 수 있습니다. AEM SPA Editor에서 사용할 모듈, 구성 요소 및 서비스로 구성된 프레임워크별 레이어를 만들기 위해 프레임워크가 충족해야 하는 요구 사항은 [SPA Blueprint](/help/sites-developing/spa-blueprint.md) 문서를 참조하십시오.

### 여러 선택기 사용 {#multiple-selectors}

추가 사용자 정의 선택기를 정의하고 AEM SPA SDK용으로 개발된 SPA의 일부로 사용할 수 있습니다. 그러나 이 지원을 사용하려면 `model` 선택기가 첫 번째 선택기이고 JSON 내보내기 기능에서 [가 필요하므로 확장명이 `.json`이어야 합니다.](json-exporter-components.md#multiple-selectors)

### 텍스트 편집기 요구 사항 {#text-editor-requirements}

SPA에서 만든 텍스트 구성 요소의 즉석 편집기를 사용하려면 추가 구성이 필요합니다.

1. 텍스트 HTML이 포함된 컨테이너 래퍼 요소에 속성을 설정합니다(모두 가능). WKND Journal 샘플 컨텐츠의 경우 `<div>` 요소이고 사용된 선택기는 `data-rte-editelement`입니다.
1. 해당 선택기를 가리키는 해당 AEM 텍스트 구성 요소의 `cq:InplaceEditingConfig`에서 `editElementQuery` 구성을 설정합니다(예:).`data-rte-editelement`. 이를 통해 편집자는 HTML 텍스트를 래핑하는 HTML 요소를 알 수 있습니다.

이러한 방법에 대한 예제는 [WKND 저널 샘플 컨텐츠를 참조하십시오.](https://github.com/adobe/aem-sample-we-retail-journal/pull/16/files)

`editElementQuery` 속성 및 리치 텍스트 편집기의 구성에 대한 자세한 내용은 [리치 텍스트 편집기 구성을 참조하십시오.](/help/sites-administering/rich-text-editor.md)

### 제한 사항 {#limitations}

AEM SPA Editor SDK는 AEM 6.4 서비스 팩 2와 함께 도입되었습니다. 이 기능은 Adobe에서 완벽하게 지원되며 새로운 기능으로 계속 향상되고 확장됩니다. 다음 AEM 기능은 SPA 편집기에서 아직 지원되지 않습니다.

* Target 모드
* ContextHub
* 인라인 이미지 편집
* 구성 편집(예: 리스너)
* 스타일 시스템
* 실행 취소/다시 실행
* 페이지 비교 및 시간 변형
* 링크 검사기, CDN 리작성기 서비스, URL 단축 등과 같은 HTML 재작성 서버측 기능을 수행하는 기능
* 개발자 모드
* AEM 실행
