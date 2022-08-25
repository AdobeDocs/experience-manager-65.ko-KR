---
title: 컨텐츠 조각용 구성 요소
seo-title: Components for Content Fragments
description: AEM 컨텐츠 조각은 페이지에 영향을 받지 않는 자산으로 작성 및 관리됩니다
seo-description: AEM content fragments are created and managed as page-independent assets
uuid: 81a9e0fe-ed45-4880-b36c-4f49e2598389
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: b7777dc5-a867-4799-9e2c-a1f4bb5dd96a
docset: aem65
pagetitle: Components for Content Fragments
exl-id: f2edd9b2-f231-42f3-a25e-428cd1d96c2a
source-git-commit: de774bec7440805273928267ea6c09669720ea24
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 5%

---

# 컨텐츠 조각용 구성 요소{#components-for-content-fragments}

## 조각 작성을 위한 구성 요소 {#components-for-fragment-authoring}

>[!CAUTION]
>
>조각 편집기에서 사용되는 실제 구성 요소는 여전히 변경될 수 있으므로 확장 또는 변경하지 않는 것이 좋습니다.

자세한 내용은 [컨텐츠 조각 관리 API - 클라이언트측](/help/sites-developing/customizing-content-fragments.md#the-content-fragment-management-api-client-side).

## 페이지 작성용 구성 요소 {#components-for-page-authoring}

>[!CAUTION]
>
>다음 [컨텐츠 조각 코어 구성 요소](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html) 이제 이 권장됩니다. 자세한 내용은 [핵심 구성 요소 개발](https://helpx.adobe.com/experience-manager/core-components/using/developing.html) 자세한 내용
>
>이 섹션에서는 컨텐츠 조각에 사용하기 위해 제공된 원래 구성 요소에 대해 자세히 설명합니다(**컨텐츠 조각** 에서 **일반** 그룹)에 속해 있어야 합니다.

>[!NOTE]
>
>참조 - [컨텐츠 조각 렌더링용 구성 요소 구성](/help/sites-developing/content-fragments-config-components-rendering.md) 추가 정보.

Adobe Experience Manager (AEM) content fragments are [created and managed as page-independent assets](/help/assets/content-fragments/content-fragments.md). 변형(채널별로 가능)과 함께 이 조각을 사용하여 채널 중립적인 콘텐츠를 만들 수 있습니다. [그런 다음 콘텐츠 페이지를 작성할 때 이러한 조각과 해당 변형을 사용할 수 있습니다](/help/sites-authoring/content-fragments.md). 기존 컨텐츠 조각 자산을 [자산 브라우저에서 페이지로 드래그](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page) (기본 구성 요소 이미지 등의 다른 자산 기반 구성 요소의 경우) 즉시 사용 가능한 컨텐츠 조각 구성 요소는 하나만 표시합니다 [요소](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) 참조한 컨텐츠 조각의 예입니다. 구성 요소 대화 상자를 사용하여 [요소, 변형 및 조각 단락 범위](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) 클릭합니다.

>[!NOTE]
>
>이 컨텐츠 조각 구성 요소는 더 이상 사용되지 않는 향상된 문서 구성 요소 버전으로 AEM 6.2에 도입되었습니다.

>[!NOTE]
>
>컨텐츠 조각은 클래식 UI에서 지원되지 않습니다.

### 정의 {#definition}

다음 **컨텐츠 조각** 구성 요소는 컨텐츠 조각 자산(효과적으로 향상된 텍스트 자산)에 대한 참조를 보유하는 데 사용됩니다. 컨텐츠 조각의 리소스 유형은 다음과 같습니다.

`dam/cfm/components/contentfragment/contentfragment`

참조가 속성에 정의됩니다.

`fileReference`

터치 지원 UI의 편집기만 클라이언트 라이브러리를 포함하는 컨텐츠 조각 구성 요소를 완전히 지원합니다.

`cq.authoring.editor.plugin.cfm`

이 라이브러리는 컨텐츠 조각에 관련된 기능을 편집기에 추가합니다. 예를 들어, 페이지에서 컨텐츠 조각을 추가 및 구성하는 기능, 자산 브라우저에서 컨텐츠 조각 자산을 검색하는 기능 및 사이드 패널의 관련 컨텐츠를 지원할 수 있습니다.

### 중간 컨텐츠 {#in-between-content}

다음 **컨텐츠 조각**&#x200B;구성 요소로 표시된 각 단락의 다른 사이에 추가 구성 요소를 놓을 수 있습니다 [요소](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment). 기본적으로 표시되는 요소는 다른 단락으로 구성됩니다. 각 단락은 캐리지 리턴으로 표시됩니다. 이러한 각 단락 사이에 다른 구성 요소를 사용하여 컨텐츠를 삽입할 수 있습니다.

기술적 관점에서 볼 때, 표시된 요소의 각 단락* *은 자체 parsys에 있으며, 단락 사이에 추가하는 각 구성 요소는 parsys에 삽입됩니다(후드 아래).

즉, 컨텐츠 조각 구성 요소의 인스턴스가 세 개의 단락으로 구성된 경우 구성 요소에는 저장소에 세 개의 다른 parsys가 있습니다. 컨텐츠 조각에 추가된 모든 중간 컨텐츠는 실제로 이러한 parsys 내에 있습니다.

저장소에서 중간 컨텐츠는 전체 단락 구조 내의 위치를 기준으로 하여 저장됩니다. 즉, 이 컨텐츠는 실제 단락 컨텐츠에 첨부되지 않습니다.

이를 설명하기 위해 다음과 같은 내용이 있습니다.

* 세 단락으로 구성된 컨텐츠 조각의 인스턴스
* 그리고 일부 컨텐츠는 두 번째 단락 뒤에 이미 삽입되었습니다

   * 즉, 컨텐츠가 두 번째 parsys에 저장됩니다.

기본적으로 이 인스턴스의 단락 구조가 변경되는 경우(변형, 요소 또는 표시된 단락 범위를 변경함) 컨텐츠 조각 컨텐츠에 표시될 때 표시되는 중간 컨텐츠에 영향을 줄 수 있습니다.

* 가 편집되고 두 번째 단락 앞에 다른 단락이 추가됩니다.

   * 새로 만든 단락 뒤에 중간 컨텐츠가 표시됩니다(이제 두 번째 parsys에 새로 만든 단락이 표시됨).

* 가 편집되고 두 번째 단락이 제거됩니다.

   * 앞의 세 번째 단락 뒤에 중간 컨텐츠가 표시됩니다(이제 두 번째 parsys가 이전 세 번째 단락을 보유함).

* 첫 번째 단락만 표시되도록 구성됩니다.

   * 중간 컨텐츠가 표시되지 않습니다(새 구성으로 인해 두 번째 parsys가 더 이상 렌더링되지 않음).

### 컨텐츠 조각 구성 요소 사용자 지정 {#customizing-the-content-fragment-component}

기본 컨텐츠 조각 구성 요소를 확장에 대한 블루프린트로 사용하려면 다음 계약을 준수해야 합니다.

* HTL 렌더링 스크립트 및 관련 POJO를 다시 사용하여 중간 컨텐츠 기능이 구현되는 방식을 확인합니다.
* 컨텐츠 조각 노드를 재사용합니다. `cq:editConfig`

   * 다음 `afterinsert`/ `afteredit`/ `afterdelete` 리스너는 JS 이벤트를 트리거하는 데 사용됩니다. 이러한 이벤트는 `cq.authoring.editor.plugin.cfm` 클라이언트 라이브러리 를 사용하여 사이드 패널에 관련 컨텐츠를 표시합니다.
   * 다음 `cq:dropTargets` 컨텐츠 조각 자산 드래그를 지원하도록 구성되었습니다.
   * `cq:inplaceEditing` 는 페이지 편집기에서 컨텐츠 조각 작성을 지원하도록 구성되어 있습니다. 조각 즉석 편집기는 `cq.authoring.editor.plugin.cfm` 클라이언트 라이브러리 및 현재 링크를 여는 빠른 링크 허용 [요소/변형](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) 에서 [조각 편집기](/help/assets/content-fragments/content-fragments-variations.md).

### 렌더링 전 자산 재작성 {#asset-rewriting-before-rendering}

컨텐츠 조각 관리는 내부 렌더링 프로세스를 사용하여 페이지에 대한 최종 HTML 출력을 생성합니다. 컨텐츠 조각 구성 요소에서 내부적으로 사용되지만, 참조하는 페이지에서 참조된 조각을 업데이트하는 백그라운드 프로세스에서도 사용됩니다.

내부적으로 Sling 재작성기가 해당 렌더링에 사용됩니다. 각 구성은 `/libs/dam/config/rewriter/cfm` 필요한 경우 조정할 수 있습니다. 자세한 내용은 [Apache Sling 재작성기](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) 추가 정보.

>[!CAUTION]
>
>재작성자의 구성을 조정/오버레이하는 경우:
>
>* `/libs/dam/config/rewriter/cfm`
>
>그러면 `serializerType` **반드시** 업데이트 대상:
>
>* `serializerType="html5-serializer"`


기본 구성에서는 다음 트랜스포머를 사용합니다.

* `transformer-cfm-payloadfilter` - 검색 `body` 부분( `<body>...</body>`) 조각 HTML만 포함합니다

* `transformer-cfm-parfilter` - 단락 범위가 지정된 경우(컨텐츠 조각 구성 요소로 수행할 수 있음) 원하지 않는 단락을 필터링합니다.
* `transformer-cfm-assetprocessor` - 조각에 포함된 자산 목록을 검색하는 데 내부적으로 사용됩니다

렌더링 프로세스는 [`com.adobe.cq.dam.cfm.content.FragmentRenderService`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html) 필요한 경우 사용자 지정 구성 요소에서 활용할 수 있습니다(예: ).
