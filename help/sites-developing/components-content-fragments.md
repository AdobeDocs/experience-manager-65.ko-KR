---
title: 컨텐츠 조각용 구성 요소
seo-title: 컨텐츠 조각용 구성 요소
description: AEM 컨텐츠 조각을 페이지 독립적인 자산으로 제작 및 관리
seo-description: AEM 컨텐츠 조각을 페이지 독립적인 자산으로 제작 및 관리
uuid: 81a9e0fe-ed45-4880-b36c-4f49e2598389
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: b7777dc5-a867-4799-9e2c-a1f4bb5dd96a
docset: aem65
pagetitle: Components for Content Fragments
translation-type: tm+mt
source-git-commit: afed13a2f832b91d0df825d1075852cc84443646
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 5%

---


# 컨텐츠 조각용 구성 요소{#components-for-content-fragments}

## 조각 작성 구성 요소 {#components-for-fragment-authoring}

>[!CAUTION]
>
>조각 편집기에서 사용되는 실제 구성 요소는 여전히 변경될 수 있으므로 확장하거나 변경하는 것이 좋습니다.

[컨텐츠 조각 관리 API - Client-Side](/help/sites-developing/customizing-content-fragments.md#the-content-fragment-management-api-client-side)를 참조하십시오.

## 페이지 작성용 구성 요소 {#components-for-page-authoring}

>[!CAUTION]
>
>이제 [컨텐츠 조각 코어 구성 요소](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)가 권장됩니다. 자세한 내용은 [핵심 구성 요소 개발](https://helpx.adobe.com/experience-manager/core-components/using/developing.html)을 참조하십시오.
>
>이 섹션에서는 컨텐츠 조각(**일반** 그룹의 **컨텐츠 조각**&#x200B;과 함께 사용하기 위해 제공된 원래 구성 요소에 대해 자세히 설명합니다.

>[!NOTE]
>
>자세한 내용은 [컨텐츠 조각 렌더링 구성 요소 구성을 참조하십시오.](/help/sites-developing/content-fragments-config-components-rendering.md)

AEM(Adobe Experience Manager) 컨텐츠 조각은 [페이지와 독립된 자산으로 작성 및 관리](/help/assets/content-fragments/content-fragments.md)됩니다. 변형(채널별로 가능)과 함께 이 조각을 사용하여 채널 중립적인 컨텐츠를 만들 수 있습니다. [그런 다음 컨텐츠 페이지를 작성할 때 이러한 조각과 해당 변형을 사용할 수 있습니다](/help/sites-authoring/content-fragments.md). 자산 브라우저에서 페이지](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page)로 [드래그하는 방식으로 기존 컨텐츠 조각 자산을 사용할 수도 있습니다(기본 구성 요소 이미지와 같은 다른 자산 기반 구성 요소의 경우). 곧바로 사용 가능한 컨텐츠 조각 구성 요소는 참조된 컨텐츠 조각에 대해 하나의 [element](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)만 표시합니다. 구성 요소 대화 상자를 사용하여 페이지에 표시할 [요소, 변형 및 조각 단락](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)의 범위를 정의할 수 있습니다.

>[!NOTE]
>
>이 컨텐츠 조각 구성 요소는 더 이상 사용되지 않는 아티클 구성 요소의 향상된 버전으로 AEM 6.2에서 도입되었습니다.

>[!NOTE]
>
>컨텐츠 조각은 클래식 UI에서 지원되지 않습니다.

### 정의 {#definition}

**컨텐츠 조각** 구성 요소는 컨텐츠 조각 자산에 대한 참조를 유지하는 데 사용됩니다(효과적으로 향상된 텍스트 자산). 컨텐츠 조각에 대한 리소스 유형은 다음과 같습니다.

`dam/cfm/components/contentfragment/contentfragment`

속성은 다음과 같이 정의됩니다.

`fileReference`

터치 지원 UI의 편집자만 클라이언트 라이브러리를 포함하는 컨텐츠 조각 구성 요소를 완전히 지원합니다.

`cq.authoring.editor.plugin.cfm`

이 라이브러리에는 컨텐츠 조각에 대한 기능이 편집기에 추가됩니다. 예를 들어 페이지에서 컨텐츠 조각을 추가 및 구성하는 기능, 자산 브라우저에서 컨텐츠 조각 자산을 검색하는 기능 및 사이드 패널에서 연관된 컨텐츠를 검색할 수 있는 기능이 지원됩니다.

### 중간 컨텐츠 {#in-between-content}

**컨텐트 조각** t 구성 요소를 사용하면 표시된 [요소](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)의 다른 단락 사이에 추가 구성 요소를 놓을 수 있습니다. 기본적으로 표시되는 요소는 서로 다른 단락으로 구성됩니다(각 단락은 캐리지 리턴으로 표시됨). 각 단락 사이에 다른 구성 요소를 사용하여 컨텐츠를 삽입할 수 있습니다.

기술 측면에서 볼 때 표시된 요소의 각 단락* *는 자체 parsys에 살고 단락 사이에 추가하는 각 구성 요소는 parsys에 삽입됩니다(백그라운드에서).

즉, 컨텐츠 조각 구성 요소의 인스턴스가 3개의 단락으로 구성된 경우 구성 요소에는 저장소에 3개의 다른 parsys가 있게 됩니다. 컨텐츠 조각에 추가된 중간 컨텐츠 모두 이러한 parsys 내에 실제로 있습니다.

저장소에서는 중간 컨텐츠가 전체 단락 구조 내의 위치를 기준으로 저장됩니다. 즉, 실제 단락 컨텐츠에는 연결되지 않습니다.

이를 설명하기 위해 다음을 고려하겠습니다.

* 3개의 단락으로 구성된 컨텐츠 조각 인스턴스
* 두 번째 단락 뒤에 이미 일부 콘텐츠가 삽입되었습니다.

   * 즉, 컨텐츠가 두 번째 parsys에 저장됩니다.

기본적으로 이 인스턴스의 단락 구조가 변경되는 경우(표시되는 단락의 변형, 요소 또는 범위를 변경하여) 컨텐츠 조각 컨텐츠 시 표시되는 중간 컨텐트에 영향을 줄 수 있습니다.

* 편집되고 두 번째 단락 앞에 다른 단락이 추가됩니다.

   * 중간 컨텐츠는 새로 만든 단락 뒤에 표시됩니다(이제 두 번째 parsys에 새로 만든 단락이 표시됨).

* 편집되고 두 번째 단락이 제거됩니다.

   * 중간 컨텐츠는 이전에 세 번째 단락이었던 단락 뒤에 표시됩니다(이제 두 번째 parsys가 이전 세 번째 단락을 보유함).

* 첫 번째 단락만 표시되도록 구성됩니다.

   * 중간 컨텐츠는 표시되지 않습니다(두 번째 parsys는 새 구성으로 인해 더 이상 렌더링되지 않음).

### 컨텐츠 조각 구성 요소 사용자 지정 {#customizing-the-content-fragment-component}

특별 컨텐츠 조각 구성 요소를 익스텐션의 청사진으로 사용하려면 다음 계약을 존중해야 합니다.

* HTL 렌더링 스크립트와 관련 POJO를 재사용하여 중간 컨텐츠 기능이 구현되는 방식을 확인합니다.
* 컨텐츠 조각 노드 재사용:`cq:editConfig`

   * `afterinsert`/ `afteredit`/ `afterdelete` 리스너는 JS 이벤트를 트리거하는 데 사용됩니다. 이러한 이벤트는 `cq.authoring.editor.plugin.cfm` 클라이언트 라이브러리에서 처리되어 사이드 패널에 관련 컨텐츠를 표시합니다.
   * `cq:dropTargets`은(는) 컨텐츠 조각 자산 드래그를 지원하도록 구성되어 있습니다.
   * `cq:inplaceEditing` 페이지 편집기에서 컨텐츠 조각 작성을 지원하도록 구성되었습니다. 조각 즉석 편집기는 `cq.authoring.editor.plugin.cfm` 클라이언트 라이브러리에 정의되며 빠른 링크를 통해 [조각 편집기](/help/assets/content-fragments/content-fragments-variations.md)에서 현재 [요소/variation](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)를 열 수 있습니다.

### 렌더링 전 에셋 재작성 {#asset-rewriting-before-rendering}

컨텐츠 조각 관리는 내부 렌더링 프로세스를 사용하여 페이지에 대한 최종 HTML 출력을 생성합니다. 컨텐츠 조각 구성 요소에서 내부적으로 사용되지만 참조하는 페이지에서 참조된 조각을 업데이트하는 백그라운드 프로세스도 사용됩니다.

내부적으로 Sling Rewriter가 해당 렌더링에 사용됩니다. 해당 구성은 `/libs/dam/config/rewriter/cfm`에 있으며 필요한 경우 조정할 수 있습니다. 자세한 내용은 [Apache Sling Rewriter](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html)를 참조하십시오.

기본 구성은 다음과 같은 변압기를 사용합니다.

* `transformer-cfm-payloadfilter` - 조각 HTML의  `body` 부분(  `<body>...</body>`)만 검색하기 위해

* `transformer-cfm-parfilter` - 단락 범위가 지정된 경우 원하지 않는 단락을 필터링합니다(컨텐츠 조각 구성 요소에서 수행할 수 있음).
* `transformer-cfm-assetprocessor` - 조각에 포함된 자산 목록을 검색하는 데 내부적으로 사용됩니다.

렌더링 프로세스는 [`com.adobe.cq.dam.cfm.content.FragmentRenderService`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html)을 통해 노출되며 필요한 경우 사용자 지정 구성 요소에서 활용할 수 있습니다.
