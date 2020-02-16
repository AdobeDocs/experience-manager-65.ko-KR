---
title: SPA 모델 라우팅
seo-title: SPA 모델 라우팅
description: AEM의 단일 페이지 애플리케이션의 경우 앱이 라우팅에 대한 책임을 집니다. 이 문서에서는 라우팅 메커니즘, 계약 및 사용 가능한 옵션에 대해 설명합니다.
seo-description: AEM의 단일 페이지 애플리케이션의 경우 앱이 라우팅에 대한 책임을 집니다. 이 문서에서는 라우팅 메커니즘, 계약 및 사용 가능한 옵션에 대해 설명합니다.
uuid: 93b4f85a-a240-42d4-95e2-e8b790df7723
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: d9f1e24e-51a9-4f28-b2cd-2e97aed63a24
translation-type: tm+mt
source-git-commit: 2dad220d6593ed542816f8a97b0d4b44f0d57876

---


# SPA 모델 라우팅{#spa-model-routing}

AEM의 단일 페이지 애플리케이션의 경우 앱이 라우팅에 대한 책임을 집니다. 이 문서에서는 라우팅 메커니즘, 계약 및 사용 가능한 옵션에 대해 설명합니다.

>[!NOTE]
>
>SPA 편집기는 SPA 프레임워크 기반의 클라이언트측 렌더링(예: 반응 또는 각도)이 필요한 프로젝트에 권장되는 솔루션입니다.

## 프로젝트 라우팅 {#project-routing}

앱은 라우팅을 소유하며 프로젝트 프런트 엔드 개발자가 구현합니다. 이 문서에서는 AEM 서버에서 반환된 모델에 대한 라우팅에 대해 설명합니다. 페이지 모델 데이터 구조는 기본 리소스의 URL을 표시합니다. 프런트 엔드 프로젝트는 라우팅 기능을 제공하는 사용자 정의 라이브러리 또는 타사 라이브러리를 사용할 수 있습니다. 루트에 모델 조각이 필요한 경우 함수를 호출할 수 `PageModelManager.getData()` 있습니다. 모델 경로가 변경된 경우 페이지 편집기와 같은 의견 수렴 라이브러리를 경고하도록 이벤트를 트리거해야 합니다.

## 아키텍처 {#architecture}

자세한 설명은 SPA Blueprint [문서의 PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager) 섹션을 참조하십시오.

## ModelRouter {#modelrouter}

- `ModelRouter` 활성화되면 - HTML5 History API 함수를 캡슐화하고 모델의 특정 조각을 사전 반입하고 액세스할 수 있도록 `pushState` `replaceState` 보장합니다. 그런 다음 등록된 프런트 엔드 구성 요소에 모델이 수정되었음을 알립니다.

## 수동 및 자동 모델 라우팅 {#manual-vs-automatic-model-routing}

모델의 조각 `ModelRouter` 가져오기를 자동화합니다. 그러나 자동화된 툴은 제한 사항이 있습니다. 필요할 `ModelRouter` 때 메타 속성을 사용하여 경로를 무시하도록 설정하거나 해제할 수 있습니다(SPA 페이지 구성 요소 [문서의 메타 속성 섹션](/help/sites-developing/spa-page-component.md) 참조). 그런 다음 프런트 엔드 개발자는 해당 기능을 사용하여 모델의 지정된 부분을 `PageModelManager` 로드하도록 요청하여 자체 모델 라우팅 레이어를 구현할 수 `getData()` 있습니다.

>[!NOTE]
>
>현재 We.Retail 분개 응답 샘플 프로젝트는 자동화된 접근 방식을 보여주고 각 프로젝트는 수동 프로젝트를 보여줍니다. 반자동 접근 방식은 또한 유효한 사용 사례입니다.

>[!CAUTION]
>
>의 현재 버전은 `ModelRouter` Sling Model 진입점의 실제 리소스 경로를 가리키는 URL의 사용만 지원합니다. 별칭 URL 또는 별칭 사용을 지원하지 않습니다.

## 계약 라우팅 {#routing-contract}

현재 구현은 SPA 프로젝트에서 HTML5 내역 API를 사용하여 다른 애플리케이션 페이지로 라우팅한다는 가정을 기반으로 합니다.

### 구성 {#configuration}

는 모델 조각을 `ModelRouter` 수신하고 프리페치 모델 조각을 호출할 때 모델 `pushState` `replaceState` 라우팅 개념을 지원합니다. 내부적으로 해당 URL에 해당하는 모델을 `PageModelManager` 로드하도록 트리거하고 다른 모듈이 들을 수 있는 `cq-pagemodel-route-changed` 이벤트를 실행합니다.

기본적으로 이 동작은 자동으로 활성화됩니다. 비활성화하려면 SPA에서 다음 메타 속성을 렌더링해야 합니다.

```
<meta property="cq:pagemodel_router" content="disable"\>
```

SPA의 모든 경로는 AEM에서 액세스 가능한 리소스(예: &quot;&quot; `/content/mysite/mypage"`)에 해당됩니다. `PageModelManager` 경로 선택 후 해당 페이지 모델을 자동으로 로드하려고 합니다. 하지만, 필요한 경우, SPA는 `PageModelManager`다음과 같이 무시해야 하는 경로의 &quot;블랙 목록&quot;을 정의할 수도 있습니다.

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
