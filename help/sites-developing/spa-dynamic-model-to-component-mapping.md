---
title: SPA용 동적 모델과 구성 요소 간 매핑
description: Adobe Experience Manager용 JavaScript SPA SDK에서 동적 모델과 구성 요소 간 매핑이 어떻게 수행되는지 알아보십시오.
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
exl-id: 5b2ccac0-bf1d-4f06-8743-7fce6fb68378
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---

# SPA용 동적 모델과 구성 요소 간 매핑{#dynamic-model-to-component-mapping-for-spas}

이 문서에서는 Adobe Experience Manager(AEM)용 JavaScript SPA SDK에서 동적 모델과 구성 요소 간 매핑이 발생하는 방법을 설명합니다.

>[!NOTE]
>
>SPA 편집기는 SPA 프레임워크 기반의 클라이언트측 렌더링(예: React 또는 Angular)이 필요한 프로젝트에 권장되는 솔루션입니다.

## ComponentMapping 모듈 {#componentmapping-module}

`ComponentMapping` 모듈은 프론트엔드 프로젝트에 NPM 패키지로 제공됩니다. 프론트엔드 구성 요소를 저장하고, 단일 페이지 애플리케이션 이 프론트엔드 구성 요소를 AEM 리소스 유형에 매핑하는 방법을 제공합니다. 이렇게 하면 애플리케이션의 JSON 모델을 구문 분석할 때 구성 요소를 동적으로 확인할 수 있습니다.

모델에 있는 각 항목에는 AEM 리소스 형식을 노출하는 `:type` 필드가 있습니다. 마운트되면 프론트엔드 구성 요소는 기본 라이브러리에서 받은 모델 조각을 사용하여 자신을 렌더링할 수 있습니다.

모델 구문 분석 및 모델에 대한 프런트 엔드 구성 요소 액세스에 대한 자세한 내용은 [SPA 블루프린트](/help/sites-developing/spa-blueprint.md)를 참조하십시오.

또한 npm 패키지를 참조하십시오. [https://www.npmjs.com/package/@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## 모델 기반 단일 페이지 애플리케이션 {#model-driven-single-page-application}

AEM용 JavaScript SPA SDK를 사용하는 단일 페이지 애플리케이션은 모델 기반의 애플리케이션입니다.

1. 프론트엔드 구성 요소가 [구성 요소 매핑 저장소](/help/sites-developing/spa-dynamic-model-to-component-mapping.md#componentmapping-module)에 등록됩니다.
1. [모델 공급자](/help/sites-developing/spa-blueprint.md#the-model-provider)에서 모델을 제공하면 [컨테이너](/help/sites-developing/spa-blueprint.md#container)이(가) 해당 모델 콘텐츠(`:items`)를 반복합니다.

1. 페이지가 있으면 자식(`:children`)이 먼저 [구성 요소 매핑](/help/sites-developing/spa-blueprint.md#componentmapping)에서 구성 요소 클래스를 가져온 다음 인스턴스화합니다.

## 앱 초기화 {#app-initialization}

각 구성 요소는 [`ModelProvider`](/help/sites-developing/spa-blueprint.md#the-model-provider)의 기능을 사용하여 확장됩니다. 따라서 초기화는 다음과 같은 일반적인 형식을 사용합니다.

1. 각 모델 공급자는 자신을 초기화하고 내부 구성 요소에 해당하는 모델 부분에 대한 변경 내용을 수신합니다.
1. [`PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager)은(는) [초기화 흐름](/help/sites-developing/spa-blueprint.md)에 표시된 대로 초기화되어야 합니다.

1. 저장되면 페이지 모델 관리자는 앱의 전체 모델을 반환합니다.
1. 그런 다음 이 모델은 응용 프로그램의 프런트 엔드 루트 [컨테이너](/help/sites-developing/spa-blueprint.md#container) 구성 요소로 전달됩니다.
1. 모델 조각이 최종적으로 각 개별 자 컴포넌트로 전파됩니다.

![app_model_initialization](assets/app_model_initialization.png)
