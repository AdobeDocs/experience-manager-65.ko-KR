---
title: 개발 및 페이지 비교
description: 개발 및 페이지 비교
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: b07134b2-074a-4d52-8d0c-7e7abe51fc3a
source-git-commit: 1ef5593495b4bf22d2635492a360168bccc1725d
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 14%

---

# 개발 및 페이지 비교{#developing-and-page-diff}

## 기능 개요 {#feature-overview}

콘텐츠 작성은 반복적 프로세스입니다. 효율적인 작성을 위해서는 한 번 반복할 때마다 변경된 내용을 확인할 수 있어야 합니다. 한 페이지 버전을 확인한 다음, 다른 한 버전을 확인하는 것은 비효율적이며 오류가 발생하기 쉽습니다. 작성자는 현재 페이지를 이전 버전과 나란히 비교할 수 있고 차이점이 강조 표시되기를 원합니다.

페이지 차이를 사용하면 현재 페이지를 시작, 이전 버전 등과 비교할 수 있습니다. 이 사용자 기능에 대한 자세한 내용은 [페이지 비교](/help/sites-authoring/page-diff.md).

## 작업 세부 정보 {#operation-details}

페이지의 버전을 비교할 때 쉽게 비교할 수 있도록 사용자가 비교하려는 이전 버전이 백그라운드에 AEM에 의해 다시 생성됩니다. 콘텐츠를 렌더링할 수 있어야 합니다. [나란히 비교용](/help/sites-developing/pagediff.md#operation-details).

이 레크리에이션 작업은 내부적으로 AEM에 의해 수행되며 사용자에게 투명하며 개입이 필요하지 않습니다. 그러나 예를 들어 CRXDE Lite에서 저장소를 보는 관리자는 콘텐츠 구조 내에서 이러한 재생성된 버전을 보게 됩니다.

콘텐츠를 비교할 때 비교할 페이지까지의 전체 트리가 다음 위치에 다시 만들어집니다.

`/tmp/versionhistory/`

정리 작업은 이 임시 콘텐츠를 정리하기 위해 자동으로 실행됩니다.

## 권한 {#permissions}

이전에는 클래식 UI에서 AEM 확산을 용이하게 하기 위해 특별한 개발을 고려해야 했습니다(예: 사용) `cq:text` 태그 라이브러리 또는 `DiffService` 구성 요소에 대한 OSGi 서비스). diff는 DOM 비교를 통해 클라이언트측에서 발생하므로 새 diff 기능에 더 이상 필요하지 않습니다.

그러나 개발자가 반드시 고려해야 하는 몇 가지 제한 사항이 있습니다.

* 이 기능은 AEM 제품에 대해 네임스페이스가 지정되지 않은 CSS 클래스를 사용합니다. 동일한 이름을 가진 다른 사용자 지정 CSS 클래스 또는 서드파티 CSS 클래스가 페이지에 포함된 경우 차이점 표시에 영향을 줄 수 있습니다.

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* diff는 클라이언트측이며 페이지 로드 시 실행되므로, 클라이언트측 diff 서비스가 실행된 후 DOM에 대한 모든 조정은 계산되지 않습니다. 이는 다음 항목에 영향을 줄 수 있습니다.

   * AJAX을 사용하여 컨텐츠를 포함하는 구성 요소
   * SPA (Single Page Applications)
   * 사용자 상호 작용 시 DOM을 조작하는 JavaScript 기반 구성 요소입니다.

>[!NOTE]
>
>페이지 비교 비교는 유효한 cq:editConfig 노드가 있는 구성 요소에만 작동합니다.
