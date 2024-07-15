---
title: 컨텐츠 조각용 구성 요소
description: Adobe Experience Manager(AEM) 컨텐츠 조각은 페이지에 영향을 받지 않는 자산으로 제작되고 관리됩니다
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
docset: aem65
pagetitle: Components for Content Fragments
exl-id: f2edd9b2-f231-42f3-a25e-428cd1d96c2a
solution: Experience Manager, Experience Manager Sites
feature: Developing,Content Fragments
role: Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 0%

---

# 컨텐츠 조각용 구성 요소{#components-for-content-fragments}

## 조각 작성을 위한 구성 요소 {#components-for-fragment-authoring}

>[!CAUTION]
>
>조각 편집기에 사용된 실제 구성 요소는 여전히 변경될 수 있으므로 확장하거나 변경하지 않는 것이 좋습니다.

[콘텐츠 조각 관리 API - 클라이언트측](/help/sites-developing/customizing-content-fragments.md#the-content-fragment-management-api-client-side)을 참조하십시오.

## 페이지 작성을 위한 구성 요소 {#components-for-page-authoring}

>[!CAUTION]
>
>이제 [콘텐츠 조각 핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html)를 사용하는 것이 좋습니다. 자세한 내용은 [핵심 구성 요소 개발](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html)을 참조하십시오.
>
>이 섹션에서는 콘텐츠 조각(**일반** 그룹의 **콘텐츠 조각**)에 사용하기 위해 전달된 원래 구성 요소에 대해 자세히 설명합니다.

>[!NOTE]
>
>자세한 내용은 [콘텐츠 조각 렌더링용 구성 요소 구성](/help/sites-developing/content-fragments-config-components-rendering.md)을 참조하십시오.

Adobe Experience Manager(AEM) 콘텐츠 조각은 [페이지에 영향을 받지 않는 자산으로 만들고 관리됩니다](/help/assets/content-fragments/content-fragments.md). 변형(채널별로 가능)과 함께 이 조각을 사용하여 채널 중립적인 콘텐츠를 만들 수 있습니다. [콘텐츠 페이지를 작성할 때 이러한 조각과 변형을 사용할 수 있습니다](/help/sites-authoring/content-fragments.md). 기존 콘텐츠 조각 에셋을 [에셋 브라우저에서 페이지로 드래그](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page)하여 사용할 수도 있습니다(기초 구성 요소 이미지와 같은 다른 에셋 기반 구성 요소의 경우). 기본 제공 콘텐츠 조각 구성 요소는 참조된 콘텐츠 조각 중 하나의 [요소](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)만 표시합니다. 구성 요소 대화 상자를 사용하여 페이지에 표시할 [요소, 변형 및 조각 단락 범위](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)를 정의할 수 있습니다.

>[!NOTE]
>
>이 콘텐츠 조각 구성 요소는 더 이상 사용되지 않는 문서 구성 요소의 향상된 버전으로 AEM 6.2에 도입되었습니다.

>[!NOTE]
>
>컨텐츠 조각은 클래식 UI에서 지원되지 않습니다.

### 정의 {#definition}

**콘텐츠 조각** 구성 요소는 콘텐츠 조각 에셋(효과적으로 향상된 텍스트 에셋)에 대한 참조를 보유하는 데 사용됩니다. 콘텐츠 조각의 리소스 유형은 다음과 같습니다.

`dam/cfm/components/contentfragment/contentfragment`

참조는 속성에 정의됩니다.

`fileReference`

터치 지원 UI의 편집기만 클라이언트 라이브러리를 포함하는 콘텐츠 조각 구성 요소를 완전히 지원합니다.

`cq.authoring.editor.plugin.cfm`

이 라이브러리는 콘텐츠 조각과 관련된 기능을 편집기에 추가합니다. 예를 들어 페이지에서 콘텐츠 조각을 추가 및 구성하는 기능, 에셋 브라우저에서 콘텐츠 조각 에셋을 검색하는 기능 및 사이드 패널에서 관련 콘텐츠에 대한 지원을 사용할 수 있습니다.

### 중간 콘텐츠 {#in-between-content}

**콘텐츠 조각** t 구성 요소를 사용하여 표시된 [요소](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)의 다른 단락 사이에 추가 구성 요소를 놓을 수 있습니다. 기본적으로 표시되는 요소는 서로 다른 단락으로 구성됩니다(각 단락은 캐리지 리턴으로 표시됨). 각 단락 사이에 다른 구성 요소를 사용하여 콘텐츠를 삽입할 수 있습니다.

기술적 관점에서 표시된 요소의 각 단락은 자체 parsys에 있으며 단락 사이에 추가하는 각 구성 요소는 parsys에 삽입됩니다(후드 아래).

즉, 콘텐츠 조각 구성 요소의 인스턴스가 세 개의 단락으로 구성된 경우 구성 요소에는 저장소에 세 개의 다른 parsys가 있습니다. 콘텐츠 조각에 추가되는 모든 중간 콘텐츠는 실제로 이러한 parsys 내에 있습니다.

중간 콘텐츠는 저장소의 전체 단락 구조 내의 위치를 기준으로 저장됩니다. 즉, 실제 단락 콘텐츠에는 첨부되지 않습니다.

이를 설명하기 위해 다음과 같은 항목이 있다고 가정해 보겠습니다.

* 세 개의 단락으로 구성된 콘텐츠 조각의 인스턴스
* 그리고 일부 콘텐츠는 두 번째 단락 뒤에 이미 삽입되었습니다.

   * 즉, 콘텐츠가 두 번째 parsys에 저장됩니다.

기본적으로 이 인스턴스의 단락 구조가 변경되는 경우(표시된 단락의 변형, 요소 또는 범위 변경), 콘텐츠 조각 콘텐츠 시 표시되는 중간 콘텐츠에 영향을 줄 수 있습니다.

* 가 편집되고 다른 단락이 두 번째 단락 앞에 추가됩니다.

   * 중간 콘텐츠는 새로 만든 단락 뒤에 표시됩니다(이제 두 번째 단락에 새로 만든 단락이 포함됨).

* 가 편집되고 두 번째 단락이 제거됩니다.

   * 중간 콘텐츠는 이전에 세 번째 단락이었던 단락 뒤에 표시됩니다(이제 두 번째 단락에 이전 세 번째 단락이 포함됨).

* 첫 번째 단락만 표시되도록 가 구성됩니다.

   * 중간 콘텐츠가 표시되지 않습니다(새 구성으로 인해 두 번째 parsys가 더 이상 렌더링되지 않음).

### 콘텐츠 조각 구성 요소 맞춤화 {#customizing-the-content-fragment-component}

기본 제공 콘텐츠 조각 구성 요소를 확장에 대한 블루프린트로 사용하려면 다음 계약을 준수해야 합니다.

* HTL 렌더링 스크립트와 관련 POJO를 재사용하여 중간 콘텐츠 기능이 구현되는 방식을 확인할 수 있습니다.
* 콘텐츠 조각 노드 재사용: `cq:editConfig`

   * `afterinsert`/ `afteredit`/ `afterdelete` 리스너는 JS 이벤트를 트리거하는 데 사용됩니다. 이러한 이벤트는 `cq.authoring.editor.plugin.cfm` 클라이언트 라이브러리에서 처리되어 관련 콘텐츠를 사이드 패널에 표시합니다.
   * `cq:dropTargets`이(가) 콘텐츠 조각 에셋 드래그를 지원하도록 구성되었습니다.
   * `cq:inplaceEditing`은(는) 페이지 편집기에서 콘텐츠 조각 작성을 지원하도록 구성되어 있습니다. 조각 원본 위치 편집기는 `cq.authoring.editor.plugin.cfm` 클라이언트 라이브러리에 정의되어 있으며 빠른 링크를 통해 [조각 편집기](/help/assets/content-fragments/content-fragments-variations.md)에서 현재 [요소/변형](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)을(를) 열 수 있습니다.

### 렌더링 전 자산 재작성 {#asset-rewriting-before-rendering}

컨텐츠 조각 관리는 내부 렌더링 프로세스를 사용하여 페이지에 대한 최종 HTML 출력을 생성합니다. 콘텐츠 조각 구성 요소에서 내부적으로 사용되지만 참조 페이지에서 참조된 조각을 업데이트하는 백그라운드 프로세스에서도 사용됩니다.

내부적으로 해당 렌더링에는 Sling 재작성기가 사용됩니다. 각 구성은 `/libs/dam/config/rewriter/cfm`에서 찾을 수 있으며 필요한 경우 조정할 수 있습니다. 자세한 내용은 [Apache Sling 재작성기](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html)를 참조하십시오.

>[!CAUTION]
>
>재작성기의 구성을 조정/오버레이하는 경우:
>
>* `/libs/dam/config/rewriter/cfm`
>
>`serializerType` **must**&#x200B;을(를) 업데이트하여 다음 작업을 수행합니다.
>
>* `serializerType="html5-serializer"`

기본 구성에서는 다음 변환기를 사용합니다.

* `transformer-cfm-payloadfilter` - 조각 HTML의 `body` 부분(`<body>...</body>`)만 검색하는 경우

* `transformer-cfm-parfilter` - 단락 범위가 지정된 경우 원하지 않는 단락을 필터링합니다(콘텐츠 조각 구성 요소로 수행할 수 있음).
* `transformer-cfm-assetprocessor` - 조각에 포함된 자산 목록을 검색하는 데 내부적으로 사용됩니다.

렌더링 프로세스는 [`com.adobe.cq.dam.cfm.content.FragmentRenderService`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html)을(를) 통해 노출되며 필요한 경우 사용자 지정 구성 요소에서 사용할 수 있습니다.
