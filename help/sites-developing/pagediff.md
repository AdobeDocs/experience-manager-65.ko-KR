---
title: 개발 및 페이지 비교
seo-title: 개발 및 페이지 비교
description: 'null'
seo-description: 'null'
uuid: 06f27bc2-f42a-4176-ab94-255e721c6933
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 6612f89d-c518-4e5a-8df1-6487cc330a9a
docset: aem65
translation-type: tm+mt
source-git-commit: c51ba167d9b3d37de649c59526e74d9728c677c6
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 14%

---


# 개발 및 페이지 비교{#developing-and-page-diff}

## 기능 개요 {#feature-overview}

컨텐츠 작성은 반복적 프로세스입니다. 효율적인 작성을 위해서는 한 번 반복할 때마다 변경된 내용을 확인할 수 있어야 합니다. 한 페이지 버전을 확인한 다음, 다른 한 버전을 확인하는 것은 비효율적이며 오류가 발생하기 쉽습니다. 작성자는 현재 페이지를 이전 버전과 비교하여 강조 표시된 차이점을 나란히 비교하기를 원합니다.

페이지 비교를 통해 사용자가 현재 페이지를 시작, 이전 버전 등과 비교할 수 있습니다. 이 사용자 기능에 대한 자세한 내용은 [페이지 비교](/help/sites-authoring/page-diff.md)를 참조하십시오.

## 작업 세부 정보 {#operation-details}

페이지 버전을 비교할 때, 사용자가 비교하려는 이전 버전은 비교를 용이하게 하기 위해 백그라운드에서 AEM에 의해 다시 만들어집니다. 이 값은 [을(를) 나란히 비교](/help/sites-developing/pagediff.md#operation-details)하기 위해 렌더링할 수 있어야 합니다.

이 레크리에이티브 작업은 AEM 내부에서 수행되며 사용자에게 투명하게 진행되며 개입할 필요가 없습니다. 그러나 저장소(예: CRX DE Lite)를 보는 관리자는 컨텐츠 구조 내에서 이러한 재구성된 버전을 보게 됩니다.

컨텐츠를 비교할 때 비교할 전체 트리가 다음 위치에 다시 만들어집니다.

`/tmp/versionhistory/`

이 임시 콘텐트를 정리하기 위해 정리 작업이 자동으로 실행됩니다.

## 권한 {#permissions}

이전에는 클래식 UI에서 AEM의 차단을 용이하게 하기 위해(예: `cq:text` 태그 lib 사용 또는 `DiffService` OSGi 서비스를 구성 요소에 통합하는 사용자 지정) 특별한 개발 고려 사항을 고려해야 했습니다. 이러한 비교 작업은 더 이상 DOM 비교를 통해 클라이언트측에서 수행되므로 새로운 비교 기능에 필요하지 않습니다.

그러나 개발자는 많은 제한 사항을 고려해야 합니다.

* 이 기능은 AEM 제품에 이름이 배치되지 않은 CSS 클래스를 사용합니다. 이름이 같은 다른 사용자 지정 CSS 클래스 또는 타사 CSS 클래스가 페이지에 포함된 경우 비교 표시가 영향을 받을 수 있습니다.

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* 비교는 클라이언트측이며 페이지 로드 시 실행되므로 클라이언트측 비교 서비스가 실행된 후 DOM에 대한 모든 조정 내용은 고려되지 않습니다. 이 문제는

   * AJAX을 사용하여 컨텐츠를 포함하는 구성 요소
   * SPA(Single Page Applications)
   * 사용자 상호 작용에 따라 DOM을 조작하는 Javascript 기반 구성 요소입니다.
