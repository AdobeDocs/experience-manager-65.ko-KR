---
title: SPA 페이지 구성 요소
description: SPA에서 페이지 구성 요소는 하위 구성 요소의 HTML 요소를 제공하지 않고, 대신 SPA 프레임워크에 위임합니다. 이 문서에서는 SPA의 페이지 구성 요소를 고유하게 만드는 방법을 설명합니다.
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
exl-id: 0e9e2350-67ef-45c3-991f-6c1cd98fe93d
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 6%

---

# SPA 페이지 구성 요소{#spa-page-component}

SPA에서 페이지 구성 요소는 하위 구성 요소의 HTML 요소를 제공하지 않고, 대신 SPA 프레임워크에 위임합니다. 이 문서에서는 SPA의 페이지 구성 요소를 고유하게 만드는 방법을 설명합니다.

>[!NOTE]
>
>SPA 편집기는 SPA 프레임워크 기반의 클라이언트측 렌더링(예: React 또는 Angular)이 필요한 프로젝트에 권장되는 솔루션입니다.

## 소개 {#introduction}

SPA에 대한 페이지 구성 요소는 JSP 또는 HTL 파일 및 리소스 오브젝트를 통해 하위 구성 요소의 HTML 요소를 제공하지 않습니다. 이 작업은 SPA 프레임워크에 위임됩니다. 하위 구성 요소의 표현은 JSON 데이터 구조(즉, 모델)로 가져옵니다. 그런 다음 제공된 JSON 모델에 따라 SPA 구성 요소가 페이지에 추가됩니다. 따라서 페이지 구성 요소의 초기 본문 컴포지션은 사전 렌더링된 HTML 구성 요소와 다릅니다.

## 페이지 모델 관리 {#page-model-management}

페이지 모델의 해결 및 관리는 제공된 에게 위임됩니다 [`PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) 모듈. SPA은 와 상호 작용해야 합니다. `PageModelManager` 초기 페이지 모델을 가져오고 모델 업데이트를 등록하기 위해 초기화될 때의 모듈입니다. 대부분 작성자가 페이지 편집기를 통해 페이지를 편집할 때 생성됩니다. 다음 `PageModelManager` 은 SPA 프로젝트에서 npm 패키지로 액세스할 수 있습니다. AEM과 SPA 사이의 인터프리터로서 `PageModelManager` SPA과 동행하기로 되어 있습니다.

페이지를 작성할 수 있도록 클라이언트 라이브러리는 `cq.authoring.pagemodel.messaging` SPA과 페이지 편집기 간 통신 채널을 제공하려면 를 추가해야 합니다. SPA 페이지 구성 요소가 페이지 wcm/핵심 구성 요소에서 상속되는 경우 다음 옵션을 사용하여 다음을 수행할 수 있습니다. `cq.authoring.pagemodel.messaging` 사용 가능한 클라이언트 라이브러리 범주:

* 템플릿을 편집할 수 있는 경우 클라이언트 라이브러리 범주를 페이지 정책에 추가합니다.
* 다음을 사용하여 클라이언트 라이브러리 범주 추가 `customfooterlibs.html` 페이지 구성 요소

포함 제한 사항을 잊지 마십시오. `cq.authoring.pagemodel.messaging` 페이지 편집기 컨텍스트에 대한 카테고리입니다.

## 커뮤니케이션 데이터 유형 {#communication-data-type}

통신 데이터 유형은 를 사용하여 AEM Page 구성 요소 내에서 HTML 요소를 설정합니다. `data-cq-datatype` 특성. 통신 데이터 유형이 JSON으로 설정되면 GET 요청이 구성 요소의 Sling 모델 엔드포인트에 도달합니다. 업데이트가 페이지 편집기에서 발생하면 업데이트된 구성 요소의 JSON 표현식이 페이지 모델 라이브러리에 전송됩니다. 그런 다음 페이지 모델 라이브러리는 업데이트 SPA에 대해 경고합니다.

**SPA 페이지 구성 요소 -`body.html`**

```
<div id="page"></div>
```

SPA 프레임워크는 DOM 생성을 지연하지 않는 것이 좋으며, 본문 끝에 스크립트를 추가해야 합니다.

**SPA 페이지 구성 요소 -`customfooterlibs.html`**

```
<sly data-sly-use.clientLib="${'/libs/granite/sightly/templates/clientlib.html'}"></sly>
<sly data-sly-test="${wcmmode.edit || wcmmode.preview}"
     data-sly-call="${clientLib.js @ categories='cq.authoring.pagemodel.messaging'}"></sly>
<sly data-sly-call="${clientLib.js @ categories='we-retail-journal-react'}"></sly>
```

SPA 콘텐츠를 설명하는 메타 리소스 속성:

**SPA 페이지 구성 요소 -`customheaderlibs.html`**

```
<meta property="cq:datatype" data-sly-test="${wcmmode.edit || wcmmode.preview}" content="JSON"/>
<meta property="cq:wcmmode" data-sly-test="${wcmmode.edit}" content="edit"/>
<meta property="cq:wcmmode" data-sly-test="${wcmmode.preview}" content="preview"/>
<meta property="cq:pagemodel_root_url" data-sly-use.page="com.adobe.cq.sample.spa.journal.models.AppPage" content="${page.rootUrl}"/>
<sly data-sly-use.clientlib="/libs/granite/sightly/templates/clientlib.html">
    <sly data-sly-call="${clientlib.css @ categories='we-retail-journal-react'}"/>
</sly>
```

>[!NOTE]
>
>구성 요소의 슬링 모델 표현을 요청할 때 기본 모델 선택기가 정적으로 설정됩니다.

## 메타 속성 {#meta-properties}

* `cq:wcmmode`: 편집기의 WCM 모드(예: 페이지, 템플릿)
* `cq:pagemodel_root_url`: 앱의 루트 모델 URL 하위 페이지 모델은 앱 루트 모델의 조각이므로 하위 페이지에 직접 액세스할 때 중요합니다. 다음 ` [PageModelManager](/help/sites-developing/spa-page-component.md)` 그런 다음 애플리케이션 초기 모델을 루트 진입점에서 애플리케이션을 입력하는 것으로 체계적으로 재구성합니다.

* `cq:pagemodel_router`: 다음을 활성화 또는 비활성화합니다. ` [ModelRouter](/help/sites-developing/spa-routing.md)` / `PageModelManager` 라이브러리

* `cq:pagemodel_route_filters`: 경로를 제공하는 쉼표로 구분된 목록 또는 정규 표현식 ` [ModelRouter](/help/sites-developing/spa-routing.md)` 무시해야 합니다.

>[!CAUTION]
>
>이 문서에서는 데모용으로만 We.Retail 저널 앱을 사용합니다. 를 프로젝트 작업에 사용하지 마십시오.
>
>모든 AEM 프로젝트는 [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)React 또는 Angular을 사용하여 SPA 프로젝트를 지원하고 SPA SDK를 사용합니다.AEM의 모든 SPA 프로젝트는 SPA Starter Kit용 Maven Archetype을 기반으로 해야 합니다.

## 페이지 편집기 오버레이 동기화 {#page-editor-overlay-synchronization}

오버레이의 동기화는 Mutation Observer에서 제공하는 것과 매우 동일한 Mutation Observer에 의해 보장됩니다. `cq.authoring.page` 범주.

## Sling 모델 JSON 내보낸 구조 구성 {#sling-model-json-exported-structure-configuration}

라우팅 기능이 활성화된 경우 SPA의 JSON 내보내기에 AEM 탐색 구성 요소의 JSON 내보내기 덕분에 다른 애플리케이션 경로가 포함되어 있다고 가정합니다. AEM 탐색 구성 요소의 JSON 출력은 다음 두 가지 속성을 통해 SPA 루트 페이지 콘텐츠 정책에 구성할 수 있습니다.

* `structureDepth`: 내보낸 트리의 깊이에 해당하는 숫자
* `structurePatterns`: 내보낼 페이지에 해당하는 정규 표현식 배열의 정규 표현식

의 SPA 샘플 콘텐츠에서 표시할 수 있습니다. `/conf/we-retail-journal/react/settings/wcm/policies/we-retail-journal/react/components/structure/page/root`.
