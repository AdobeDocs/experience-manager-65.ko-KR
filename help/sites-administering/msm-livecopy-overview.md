---
title: Live Copy 개요 콘솔
seo-title: Live Copy Overview Console
description: 라이브 카피 개요 콘솔의 기본 사항에 대해 알아봅니다.
seo-description: Learn about the basics of the Live Copy Overview Console.
uuid: 6b1841ec-950e-455b-9b30-b5f5050a67b8
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 3763e985-7dd8-47fd-bfdf-2368b424c270
feature: Multi Site Manager
exl-id: 0c3488bd-5f32-4956-882c-93326a45b379
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 33%

---

# Live Copy 개요 콘솔{#live-copy-overview-console}

다음 **라이브 카피 개요** 을 통해 다음 작업을 수행할 수 있습니다.

* 사이트 전체에 걸쳐 상속을 조회/관리합니다:

   * 블루프린트 트리 및 해당 라이브 카피 구조를 상속 상태와 함께 조회합니다.
   * 상속 상태를 변경합니다(예: 일시 중단, 다시 시작).
   * 블루프린트 및 라이브 카피 속성 보기

* 롤아웃 작업을 수행합니다

## Live Copy 개요 열기 {#opening-the-live-copy-overview}

다음 위치에서 Live Copy 개요를 열 수 있습니다.

* [블루프린트 페이지의 참조 측면 패널(Sites 콘솔)](#opening-live-copy-overview-references-for-a-blueprint-page)
* [블루프린트 페이지 속성](#opening-live-copy-overview-properties-of-a-blueprint-page)

### 라이브 카피 개요 열기 - 블루프린트 페이지에 대한 참조 {#opening-live-copy-overview-references-for-a-blueprint-page}

**사이트** 콘솔의 **참조** 측면 패널에서 **Live Copy 개요**&#x200B;를 열 수 있습니다.

1. **사이트** 콘솔에서 [블루프린트 페이지를 검색한 다음 선택합니다](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).
1. 를 엽니다. **[참조](/help/sites-authoring/basic-handling.md#references)** 패널 및 선택 **라이브 카피**.

   ![참조 패널 - 라이브 카피](assets/chlimage_1-359.png)

   >[!NOTE]
   >
   >먼저 참조 를 연 다음 블루프린트를 선택할 수도 있습니다.

1. 선택 **라이브 카피 개요** 을 클릭하여 선택한 블루프린트와 관련된 모든 라이브 카피의 개요를 표시하고 사용합니다.
1. 종료하고 **사이트** 콘솔로 돌아가려면 **닫기**&#x200B;를 사용합니다.

### 라이브 카피 개요 열기 - 블루프린트 페이지 속성 {#opening-live-copy-overview-properties-of-a-blueprint-page}

블루프린트 페이지 속성을 볼 때 **Live Copy 개요**&#x200B;를 열 수 있습니다.

1. 적절한 블루프린트 페이지에 대한 **속성**&#x200B;을 엽니다.
1. **블루프린트** 탭을 열면 **Live Copy 개요** 옵션이 상단 도구 모음에 표시됩니다.

   ![블루프린트 탭 - 라이브 카피 개요](assets/chlimage_1-360.png)

1. 선택 **라이브 카피 개요** 을 클릭하여 현재 블루프린트와 관련된 모든 라이브 카피의 개요를 표시하고 사용합니다.

   >[!NOTE]
   >
   >자세한 내용은 기술 자료 문서 를 참조하십시오. [라이브 카피 상태 메시지 - 최신/녹색/동기화 중](https://helpx.adobe.com/experience-manager/kb/livecopy-status-message---up-to-date-green-in-sync.html).

1. 종료하고 **사이트** 콘솔로 돌아가려면 **닫기**&#x200B;를 사용합니다.

## Live Copy 개요 사용 {#using-the-live-copy-overview}

다음 **라이브 카피 개요** 는 라이브 카피에서 작업을 수행하는 데 사용할 수도 있습니다.

1. **Live Copy 개요**&#x200B;를 엽니다.
1. 필요한 블루프린트 또는 라이브 카피 페이지를 선택합니다. 사용 가능한 작업을 표시하도록 도구 모음이 업데이트됩니다. 다음 [작업](/help/sites-administering/msm.md#terms-used) 사용 가능 여부는 다음 중 하나를 선택했는지 여부에 따라 다릅니다. [블루프린트](#actions-for-a-blueprint-page) 또는 [live copy](#actions-for-a-live-copy-page) 페이지:

### 블루프린트 페이지에 대한 작업 {#actions-for-a-blueprint-page}

블루프린트 페이지를 선택하면 다음과 같은 작업을 사용할 수 있습니다.

![블루프린트 선택됨 - 사용 가능한 작업](assets/chlimage_1-361.png)

* 편집

   * 편집할 블루프린트 페이지를 엽니다.

* [롤아웃](/help/sites-administering/msm.md#rollout-and-synchronize)

   * 롤아웃을 수행하여 소스에서 라이브 카피로 변경 내용을 푸시합니다.

### Live Copy 페이지에 대한 작업 {#actions-for-a-live-copy-page}

라이브 카피 페이지를 선택하면 다음 작업을 사용할 수 있습니다.

![Live Copy 페이지 선택됨 - 사용 가능한 작업](assets/chlimage_1-362.png)

* 편집

   * 편집할 라이브 카피 페이지를 엽니다.

* [관계 상태](#relationship-status)

   * 상태 및 상속에 대한 정보를 봅니다.

* [동기화](/help/sites-administering/msm.md#rollout-and-synchronize)

   * 라이브 카피를 동기화하여 소스에서 라이브 카피로 변경 내용을 가져올 수 있습니다.

* [재설정](/help/sites-administering/msm-livecopy.md#resetting-a-live-copy-page)

   * 라이브 카피 페이지를 재설정하여 모든 상속 취소를 제거하고 페이지를 소스 페이지와 동일한 상태로 되돌립니다.

* [일시 중단](/help/sites-administering/msm.md#suspending-and-cancelling-inheritance-and-synchronization)

   * 라이브 카피와 블루프린트 페이지 간의 라이브 관계를 일시적으로 비활성화합니다.

* [다시 시작](/help/sites-administering/msm-livecopy.md#resuming-inheritance-for-a-page)

   * 다시 시작을 사용하면 일시 중단된 관계를 복원할 수 있습니다.

* [분리](/help/sites-administering/msm.md#detaching-a-live-copy)

   * 라이브 카피와 블루프린트 페이지 간의 라이브 관계를 영구적으로 제거합니다.

## 관계 상태 {#relationship-status}

**관계 상태** 콘솔에는 다양한 기능을 제공하는 두 가지 탭이 있습니다:

* [관계 상태 정보](#relationship-status-information)
* [Live Copy 정보](#live-copy-information)

### 관계 상태 정보 {#relationship-status-information}

이 탭은 블루프린트와 라이브 카피 간의 관계 상태에 대한 자세한 정보를 제공합니다.

![관계 상태 정보](assets/chlimage_1-363.png)

### Live Copy 정보 {#live-copy-information}

이 탭에서는 라이브 카피 구성을 보고 편집할 수 있습니다.

![Live Copy 정보](assets/chlimage_1-364.png)
