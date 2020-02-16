---
title: Live Copy 개요 콘솔
seo-title: Live Copy 개요 콘솔
description: Live Copy 개요 콘솔의 기본 사항에 대해 알아봅니다.
seo-description: Live Copy 개요 콘솔의 기본 사항에 대해 알아봅니다.
uuid: 6b1841ec-950e-455b-9b30-b5f5050a67b8
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 3763e985-7dd8-47fd-bfdf-2368b424c270
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Live Copy 개요 콘솔{#live-copy-overview-console}

Live **Copy** 개요를 사용하면 다음 작업을 수행할 수 있습니다.

* 사이트 간 상속 보기/관리:

   * 상속 상태와 함께 블루프린트 트리 및 해당 Live Copy 구조 보기
   * 상속 상태 변경;예를 들어 일시 중단, 재개
   * 블루프린트 및 Live Copy 속성 보기

* 롤아웃 작업 수행

## Live Copy 개요 열기 {#opening-the-live-copy-overview}

Live Copy 개요는

* [블루프린트 페이지의 측면 패널 참조(사이트 콘솔)](#opening-live-copy-overview-references-for-a-blueprint-page)
* [블루프린트 페이지의 속성](#opening-live-copy-overview-properties-of-a-blueprint-page)

### Live Copy 개요 열기 - 블루프린트 페이지에 대한 참조 {#opening-live-copy-overview-references-for-a-blueprint-page}

Live **Copy** 개요는 사이트 **콘솔의 참조** 사이드 패널에서 열 수 **있습니다** .

1. 사이트 **콘솔에서** 블루프린트 페이지로 [이동하여 선택합니다](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).
1. Open the **[References](/help/sites-authoring/basic-handling.md#references)**panel and select **Live Copies**.

   ![chlimage_1-359](assets/chlimage_1-359.png)

   >[!NOTE]
   >
   >먼저 참조를 연 다음 블루프린트를 선택할 수도 있습니다.

1. Live **Copy** 개요를 선택하여 선택한 블루프린트와 관련된 모든 Live Copy 개요를 표시하고 사용합니다.
1. 닫기를 **사용하여** 종료한 후 사이트 **콘솔로 돌아갑니다** .

### Live Copy 개요 열기 - 블루프린트 페이지의 속성 {#opening-live-copy-overview-properties-of-a-blueprint-page}

Live **Copy** 개요는 블루프린트 페이지의 속성을 볼 때 열 수 있습니다.

1. 해당 **블루프린트** 페이지의 속성을 엽니다.
1. 블루프린트 **탭을 엽니다** . **Live Copy** 개요 옵션이 상단 도구 모음에 표시됩니다.

   ![chlimage_1-360](assets/chlimage_1-360.png)

1. Live **Copy** 개요를 선택하여 현재 블루프린트와 관련된 모든 Live Copy 개요를 표시하고 사용합니다.

   >[!NOTE]
   >
   >자세한 내용은 기술 자료 문서 Livecopy [상태 메시지(최신/녹색/동기화)를 참조하십시오](https://helpx.adobe.com/experience-manager/kb/livecopy-status-message---up-to-date-green-in-sync.html).

1. 닫기를 **사용하여** 종료한 후 사이트 **콘솔로 돌아갑니다** .

## Live Copy 개요 사용 {#using-the-live-copy-overview}

Live **Copy** 개요를 사용하여 Live Copy에서 작업을 수행할 수도 있습니다.

1. Open the **Live Copy Overview**.
1. 필요한 블루프린트 또는 Live Copy 페이지를 선택합니다. 도구 모음이 업데이트되어 사용 가능한 작업이 표시됩니다. 사용 가능한 [작업은](/help/sites-administering/msm.md#terms-used) [블루프린트](#actions-for-a-blueprint-page) 또는 [Live Copy](#actions-for-a-live-copy-page) 페이지를 선택하는지에 따라 다릅니다.

### 블루프린트 페이지에 대한 작업 {#actions-for-a-blueprint-page}

블루프린트 페이지를 선택하면 다음 작업을 사용할 수 있습니다.

![chlimage_1-361](assets/chlimage_1-361.png)

* 편집

   * 편집할 블루프린트 페이지를 엽니다.

* [롤아웃](/help/sites-administering/msm.md#rollout-and-synchronize)

   * 소스에서 Live Copy로 변경 내용을 푸시하는 롤아웃을 수행합니다.

### Live Copy 페이지에 대한 작업 {#actions-for-a-live-copy-page}

Live Copy 페이지를 선택하면 다음 작업을 사용할 수 있습니다.

![chlimage_1-362](assets/chlimage_1-362.png)

* 편집

   * 편집할 Live Copy 페이지를 엽니다.

* [관계 상태](#relationship-status)

   * 상태 및 상속에 대한 정보를 봅니다.

* [동기화](/help/sites-administering/msm.md#rollout-and-synchronize)

   * Live Copy를 동기화하여 소스에서 Live Copy로 변경 내용을 가져옵니다.

* [재설정](/help/sites-administering/msm-livecopy.md#resetting-a-live-copy-page)

   * Live Copy 페이지를 재설정하여 모든 상속 취소를 제거하고 페이지를 소스 페이지와 동일한 상태로 되돌립니다.

* [일시 중단](/help/sites-administering/msm.md#suspending-and-cancelling-inheritance-and-synchronization)

   * Live Copy와 해당 블루프린트 페이지 간의 라이브 관계를 일시적으로 비활성화합니다.

* [다시 시작](/help/sites-administering/msm-livecopy.md#resuming-inheritance-for-a-page)

   * 다시 시작을 사용하면 일시 중단된 관계를 복원할 수 있습니다.

* [분리](/help/sites-administering/msm.md#detaching-a-live-copy)

   * Live Copy와 블루프린트 페이지 간의 라이브 관계를 영구적으로 제거합니다.

## 관계 상태 {#relationship-status}

관계 **상태** 콘솔에는 두 개의 탭이 있어 다양한 기능이 제공됩니다.

* [관계 상태 정보](#relationship-status-information)
* [Live Copy 정보](#live-copy-information)

### 관계 상태 정보 {#relationship-status-information}

이 탭에서는 블루프린트와 Live Copy 간의 관계 상태에 대한 자세한 정보를 제공합니다.

![chlimage_1-363](assets/chlimage_1-363.png)

### Live Copy 정보 {#live-copy-information}

이 탭에서는 Live Copy 구성을 보고 편집할 수 있습니다.

![chlimage_1-364](assets/chlimage_1-364.png)

