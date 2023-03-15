---
title: ContextHub
seo-title: ContextHub
description: ContextHub는 컨텍스트 데이터를 저장, 조작 및 표시하기 위한 프레임워크입니다
seo-description: ContextHub is a framework for storing, manipulating, and presenting context data
uuid: 14e6ff4f-ffbe-454a-b2ec-a35333526e27
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: acf5c17a-95b7-43ba-9734-241e20f4f374
exl-id: 3fd50655-7461-4900-a3b8-c01b04c7ba7a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 1%

---

# ContextHub{#contexthub}

ContextHub는 컨텍스트 데이터를 저장, 조작 및 표시하기 위한 프레임워크입니다. 클라이언트측 Javascript API를 사용하면 콘텐츠를 개인화하기 위한 데이터에 액세스할 수 있습니다.

>[!NOTE]
>
>다음 [We.Retail 참조 구현](/help/sites-developing/we-retail.md) 는 ContextHub를 구현하고 ContextHub를 자체 프로젝트에 통합할 때 참조 역할을 할 수 있습니다.

>[!CAUTION]
>
>에서 사용하는 샘플 ContextHub 구성이 포함된 경로 [We.Retail 참조 구현](/help/sites-developing/we-retail.md) ( `/libs/settings/cloudsettings/legacy`)는 자체 구성을 만들기 위한 참조로만 사용해야 합니다.
>
>프로젝트에서 고유한 ContextHub 구성으로 사용해서는 안 됩니다.

## 지속성 {#persistence}

ContextHub 저장소는 클라이언트에 컨텍스트 데이터를 유지합니다. ContextHub Javascript API를 사용하면 저장소에 액세스하여 데이터를 필요에 따라 작성, 업데이트 및 삭제할 수 있습니다. 따라서 ContextHub는 페이지의 데이터 계층을 나타냅니다.

각 ContextHub 저장소는 사전 정의된 저장소 유형의 인스턴스입니다.

* ContextHub는 몇 가지 기능을 제공합니다. [샘플 저장소 유형](/help/sites-developing/ch-samplestores.md).
* AEM 콘솔을 사용하여 [스토어 만들기](ch-configuring.md#creating-a-contexthub-store).
* 개발자는 [사용자 지정 저장소 유형 만들기](/help/sites-developing/ch-extend.md#creating-custom-store-candidates).
* 개발자는 [저장소 데이터 액세스](/help/sites-developing/ch-adding.md#interacting-with-contexthub-stores) javascript를 통해.

## 세분화 {#segmentation}

ContextHub에는 세그먼트를 관리하고 현재 컨텍스트에 대해 해결할 세그먼트를 결정하는 세그먼테이션 엔진이 포함되어 있습니다. 여러 개의 세그먼트가 정의됩니다. Javascript API를 사용하여 다음을 수행할 수 있습니다. [해결된 세그먼트 결정](/help/sites-developing/ch-adding.md#determining-resolved-contexthub-segments).

## 프레젠테이션 {#presentation}

다음 [ContextHub 도구 모음](/help/sites-authoring/ch-previewing.md) 마케터와 작성자가 페이지를 작성할 때 사용자 경험을 시뮬레이션하기 위해 스토어 데이터를 보고 조작할 수 있습니다. 도구 모음은 ContextHub 저장소에 대한 액세스를 제공하는 UI 모듈 그룹으로 구성됩니다.

각 ContextHub UI 모듈은 사전 정의된 모듈 유형의 인스턴스입니다.

* ContextHub는 몇 가지 기능을 제공합니다. [샘플 모듈 유형](/help/sites-developing/ch-samplemodules.md).
* AEM 콘솔을 사용하여 [ui 모듈 추가](ch-configuring.md#adding-a-ui-module), 및 까지 [ui 모드로 그룹화합니다.](ch-configuring.md#adding-a-ui-mode).

* 개발자는 [사용자 정의 모듈 유형 만들기](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types).

개발자는 [페이지에 ContextHub 구성 요소 추가](/help/sites-developing/ch-adding.md).
