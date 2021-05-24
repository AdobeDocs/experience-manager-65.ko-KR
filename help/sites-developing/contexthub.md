---
title: ContextHub
seo-title: ContextHub
description: ContextHub는 컨텍스트 데이터를 저장, 조작 및 제공하기 위한 프레임워크입니다
seo-description: ContextHub는 컨텍스트 데이터를 저장, 조작 및 제공하기 위한 프레임워크입니다
uuid: 14e6ff4f-ffbe-454a-b2ec-a35333526e27
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: acf5c17a-95b7-43ba-9734-241e20f4f374
exl-id: 3fd50655-7461-4900-a3b8-c01b04c7ba7a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 1%

---

# ContextHub{#contexthub}

ContextHub는 컨텍스트 데이터를 저장, 조작 및 제공하기 위한 프레임워크입니다. 클라이언트측 Javascript API를 사용하면 컨텐츠를 개인화하기 위해 데이터에 액세스할 수 있습니다.

>[!NOTE]
>
>[We.Retail 참조 구현](/help/sites-developing/we-retail.md)은 ContextHub를 구현하고 ContextHub를 자신의 프로젝트에 통합할 때 참조 역할을 할 수 있습니다.

>[!CAUTION]
>
>[We.Retail 참조 구현](/help/sites-developing/we-retail.md)( `/libs/settings/cloudsettings/legacy`)에서 사용하는 샘플 ContextHub 구성이 들어 있는 경로는 고유한 구성을 만들기 위한 참조로만 사용해야 합니다.
>
>프로젝트에서 자신의 ContextHub 구성으로 사용해서는 안 됩니다.

## 지속성 {#persistence}

ContextHub는 클라이언트에서 컨텍스트 데이터를 유지합니다. ContextHub Javascript API를 사용하면 필요에 따라 데이터를 생성, 업데이트 및 삭제하기 위해 저장소에 액세스할 수 있습니다. 이와 같이 ContextHub는 페이지의 데이터 계층을 나타냅니다.

각 ContextHub 저장소는 사전 정의된 저장소 유형의 인스턴스입니다.

* ContextHub에서는 몇 가지 [샘플 저장소 유형](/help/sites-developing/ch-samplestores.md)을 제공합니다.
* AEM 콘솔을 사용하여 [저장소를 만듭니다](ch-configuring.md#creating-a-contexthub-store).
* 개발자는 [사용자 지정 저장소 유형](/help/sites-developing/ch-extend.md#creating-custom-store-candidates)을 만들 수 있습니다.
* 개발자는 Javascript를 통해 [스토어 데이터](/help/sites-developing/ch-adding.md#interacting-with-contexthub-stores)에 액세스할 수 있습니다.

## 세그멘테이션 {#segmentation}

ContextHub에는 세그먼트를 관리하고 현재 컨텍스트에 대해 해결된 세그먼트를 결정하는 세그멘테이션 엔진이 포함되어 있습니다. 여러 세그먼트가 정의됩니다. Javascript API를 사용하여 [해결된 세그먼트를 결정할 수 있습니다](/help/sites-developing/ch-adding.md#determining-resolved-contexthub-segments).

## 프레젠테이션 {#presentation}

[ContextHub 도구 모음](/help/sites-authoring/ch-previewing.md)을 사용하면 마케터와 작성자가 페이지를 작성할 때 사용자 경험을 시뮬레이션하기 위해 저장소 데이터를 보고 조작할 수 있습니다. 도구 모음은 ContextHub 저장소에 액세스할 수 있는 UI 모듈 그룹으로 구성됩니다.

각 ContextHub UI 모듈은 사전 정의된 모듈 유형의 인스턴스입니다.

* ContextHub에서는 몇 가지 [샘플 모듈 유형](/help/sites-developing/ch-samplemodules.md)을 제공합니다.
* AEM 콘솔을 사용하여 [UI 모듈](ch-configuring.md#adding-a-ui-module)을 추가하고, [UI 모드](ch-configuring.md#adding-a-ui-mode)로 그룹화합니다.

* 개발자는 [사용자 지정 모듈 유형](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types)을 만들 수 있습니다.

개발자는 [ContextHub 구성 요소를 페이지](/help/sites-developing/ch-adding.md)에 추가해야 합니다.
