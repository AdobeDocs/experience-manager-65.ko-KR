---
title: SPA에 대한 동적 모델과 구성 요소 간 매핑
seo-title: SPA에 대한 동적 모델과 구성 요소 간 매핑
description: 이 문서에서는 AEM용 Javascript SPA SDK에서 구성 요소에 대한 동적 모델이 발생하는 방법에 대해 설명합니다.
seo-description: 이 문서에서는 AEM용 Javascript SPA SDK에서 구성 요소에 대한 동적 모델이 발생하는 방법에 대해 설명합니다.
uuid: 337b8d90-efd7-442e-9fac-66c33cc26212
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 8b4b0afc-8534-4010-8f34-cb10475a8e79
translation-type: tm+mt
source-git-commit: 4c9a0bd73e8d87d3869c6a133f5d1049f8430cd1
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 5%

---


# SPA에 대한 동적 모델과 구성 요소 간 매핑{#dynamic-model-to-component-mapping-for-spas}

이 문서에서는 AEM용 Javascript SPA SDK에서 구성 요소에 대한 동적 모델 매핑이 발생하는 방법에 대해 설명합니다.

>[!NOTE]
>
>SPA 편집기는 SPA 프레임워크 기반 클라이언트측 렌더링(예: 반응 또는 각도)이 필요한 프로젝트에 권장되는 솔루션입니다.

## ComponentMapping 모듈 {#componentmapping-module}

`ComponentMapping` 모듈은 프런트 엔드 프로젝트에 NPM 패키지로 제공됩니다. 프런트 엔드 구성 요소를 저장하고 단일 페이지 애플리케이션에서 프런트 엔드 구성 요소를 AEM 리소스 유형에 매핑할 수 있는 방법을 제공합니다. 이렇게 하면 응용 프로그램의 JSON 모델을 구문 분석할 때 구성 요소의 동적 확인이 가능합니다.

모델에 있는 각 항목에는 AEM 리소스 유형을 표시하는 `:type` 필드가 포함되어 있습니다. 마운트되면 프런트 엔드 구성 요소는 기본 라이브러리에서 받은 모델 조각을 사용하여 자체 렌더링할 수 있습니다.

모델 구문 분석 및 모델에 대한 프런트 엔드 구성 요소 액세스에 대한 자세한 내용은 [SPA Blueprint](/help/sites-developing/spa-blueprint.md) 문서를 참조하십시오.

npm 패키지를 참조하십시오.[https://www.npmjs.com/package/@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## 모델 기반 단일 페이지 응용 프로그램 {#model-driven-single-page-application}

AEM용 Javascript SPA SDK를 활용하는 단일 페이지 애플리케이션은 모델 기반입니다.

1. 프런트 엔드 구성 요소는 [구성 요소 매핑 스토어](/help/sites-developing/spa-dynamic-model-to-component-mapping.md#componentmapping-module)에 자신을 등록합니다.
1. 그런 다음 [Container](/help/sites-developing/spa-blueprint.md#container)이(가) [Model Provider](/help/sites-developing/spa-blueprint.md#the-model-provider)에서 모델과 함께 제공되면 해당 모델 컨텐트( `:items`)에 대해 반복합니다.

1. 페이지의 경우, 해당 하위( `:children`)는 먼저 [Component Mapping](/help/sites-developing/spa-blueprint.md#componentmapping)에서 구성 요소 클래스를 가져온 다음 인스턴스화합니다.

## 앱 초기화 {#app-initialization}

각 구성 요소는 [ `ModelProvider`](/help/sites-developing/spa-blueprint.md#the-model-provider)의 기능으로 확장됩니다. 따라서 초기화는 다음과 같은 일반 양식을 사용합니다.

1. 각 모델 공급자는 자체적으로 초기화하고 내부 구성 요소에 해당하는 모델 부분의 변경 사항을 수신합니다.
1. [ `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager)은 [초기화 흐름](/help/sites-developing/spa-blueprint.md)으로 표현되어야 합니다.

1. 저장 후 페이지 모델 관리자는 앱의 전체 모델을 반환합니다.
1. 그런 다음 이 모델은 응용 프로그램의 프런트 엔드 루트 [Container](/help/sites-developing/spa-blueprint.md#container) 구성 요소로 전달됩니다.
1. 모델의 일부가 결국 개별 하위 구성 요소에 전파됩니다.

![app_model_initialization](assets/app_model_initialization.png)

