---
title: SPA 모델 라우팅
seo-title: SPA 모델 라우팅
description: AEM의 단일 페이지 애플리케이션의 경우, 앱은 라우팅을 담당합니다. 이 문서에서는 사용 가능한 라우팅 메커니즘, 계약 및 옵션에 대해 설명합니다.
seo-description: AEM의 단일 페이지 애플리케이션의 경우, 앱은 라우팅을 담당합니다. 이 문서에서는 사용 가능한 라우팅 메커니즘, 계약 및 옵션에 대해 설명합니다.
uuid: 93b4f85a-a240-42d4-95e2-e8b790df7723
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: d9f1e24e-51a9-4f28-b2cd-2e97aed63a24
exl-id: eaef65ec-2e4d-490f-8158-d48d738e3409
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 2%

---

# SPA 모델 라우팅{#spa-model-routing}

AEM의 단일 페이지 애플리케이션의 경우, 앱은 라우팅을 담당합니다. 이 문서에서는 사용 가능한 라우팅 메커니즘, 계약 및 옵션에 대해 설명합니다.

>[!NOTE]
>
>SPA 편집기는 SPA 프레임워크 기반 클라이언트측 렌더링(예: React 또는 Angular)이 필요한 프로젝트에 권장되는 솔루션입니다.

## 프로젝트 라우팅 {#project-routing}

앱은 라우팅을 소유하며 프로젝트 프런트 엔드 개발자에 의해 구현됩니다. 이 문서에서는 AEM 서버에서 반환한 모델에 대한 라우팅에 대해 설명합니다. 페이지 모델 데이터 구조는 기본 리소스의 URL을 표시합니다. 프런트 엔드 프로젝트는 라우팅 기능을 제공하는 모든 사용자 지정 라이브러리 또는 타사 라이브러리를 사용할 수 있습니다. 경로에 모델 조각이 필요한 경우에는 `PageModelManager.getData()` 함수를 호출할 수 있습니다. 모델 경로가 변경된 경우 페이지 편집기와 같은 수신 라이브러리를 경고하도록 이벤트를 트리거해야 합니다.

## 아키텍처 {#architecture}

자세한 설명은 SPA 블루프린트 문서의 [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager) 섹션을 참조하십시오.

## ModelRouter {#modelrouter}

`ModelRouter` - 활성화되면 HTML5 History API 함수 `pushState` 및 `replaceState`를 캡슐화하여 제공된 모델 조각을 미리 가져오고 액세스할 수 있도록 합니다. 그런 다음 등록된 프런트엔드 구성 요소에 모델이 수정되었음을 알립니다.

## 수동 및 자동 모델 라우팅 {#manual-vs-automatic-model-routing}

`ModelRouter` 은 모델의 조각의 가져오기를 자동화합니다. 그러나 자동화 도구에는 제한이 있습니다. 필요한 경우 메타 속성을 사용하여 경로를 무시하도록 `ModelRouter`을 비활성화하거나 구성할 수 있습니다( [SPA 페이지 구성 요소](/help/sites-developing/spa-page-component.md) 문서의 메타 속성 섹션 참조). 그러면 프런트 엔드 개발자는 `PageModelManager`에 `getData()` 함수를 사용하여 지정된 모델 조각을 로드하도록 요청하여 자체 모델 라우팅 레이어를 구현할 수 있습니다.

>[!NOTE]
>
>현재 We.Retail Journal 샘플 React 프로젝트는 자동화된 접근 방식을 보여주고 Angular 프로젝트는 수동 접근 방식을 보여줍니다. 반자동화된 접근 방식 또한 유효한 사용 사례입니다.

>[!CAUTION]
>
>현재 버전의 `ModelRouter`은(는) Sling 모델 시작 지점의 실제 리소스 경로를 가리키는 URL의 사용만 지원합니다. 별칭 URL 또는 별칭 사용을 지원하지 않습니다.

## 공정순서 계약 {#routing-contract}

현재 구현은 SPA 프로젝트에서 다른 애플리케이션 페이지로 라우팅하기 위해 HTML5 내역 API를 사용한다고 가정 하에 따라 다릅니다.

### 구성 {#configuration}

`ModelRouter`은 모델 조각을 미리 가져오기 위해 `pushState` 및 `replaceState` 호출을 수신하면 모델 라우팅 개념을 지원합니다. 내부적으로 `PageModelManager`을 트리거하여 지정된 URL에 해당하는 모델을 로드하고 다른 모듈에서 수신할 수 있는 `cq-pagemodel-route-changed` 이벤트를 실행합니다.

기본적으로 이 동작은 자동으로 활성화됩니다. 비활성화하려면 SPA에서 다음 메타 속성을 렌더링해야 합니다.

```
<meta property="cq:pagemodel_router" content="disable"\>
```

`PageModelManager`은(는) 경로를 선택하면 해당 페이지 모델을 자동으로 로드하려고 하므로 SPA의 모든 경로는 AEM의 액세스 가능한 리소스(예: &quot; `/content/mysite/mypage"`)에 해당해야 합니다. 그러나 필요한 경우 SPA에서 `PageModelManager`에서 무시해야 하는 경로의 &quot;차단 목록&quot;도 정의할 수 있습니다.

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
