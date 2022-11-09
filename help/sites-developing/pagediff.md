---
title: 개발 및 페이지 비교
seo-title: Developing and Page Diff
description: 개발 및 페이지 비교
seo-description: null
uuid: 06f27bc2-f42a-4176-ab94-255e721c6933
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 6612f89d-c518-4e5a-8df1-6487cc330a9a
docset: aem65
exl-id: b07134b2-074a-4d52-8d0c-7e7abe51fc3a
source-git-commit: 85895215904b8706830d20f7714de5512b2c3ec2
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 13%

---

# 개발 및 페이지 비교{#developing-and-page-diff}

## 기능 개요 {#feature-overview}

콘텐츠 작성은 반복적 프로세스입니다. 효율적인 작성을 위해서는 한 번 반복할 때마다 변경된 내용을 확인할 수 있어야 합니다. 한 페이지 버전을 확인한 다음, 다른 한 버전을 확인하는 것은 비효율적이며 오류가 발생하기 쉽습니다. 작성자는 현재 페이지를 이전 버전과 비교하여 강조 표시된 차이점을 나란히 비교하려고 합니다.

페이지 차이를 사용하면 사용자가 현재 페이지를 실행, 이전 버전 등과 비교할 수 있습니다. 이 사용자 기능에 대한 자세한 내용은 [페이지 비교](/help/sites-authoring/page-diff.md).

## 작업 세부 정보 {#operation-details}

페이지 버전을 비교할 때 사용자가 비교하려는 이전 버전은 비교를 쉽게 하기 위해 백그라운드에서 AEM에 의해 다시 생성됩니다. 콘텐츠를 렌더링하려면 다음이 필요합니다 [을 참조하십시오](/help/sites-developing/pagediff.md#operation-details).

이 레크리에이션 작업은 AEM에서 내부적으로 수행되며 사용자에게 투명하며 간섭이 필요하지 않습니다. 그러나 CRX DE Lite와 같이 리포지토리를 보는 관리자는 컨텐츠 구조 내에서 이러한 재구성된 버전을 볼 수 있습니다.

컨텐츠를 비교할 때 비교할 페이지까지의 전체 트리가 다음 위치에 다시 만들어집니다.

`/tmp/versionhistory/`

이 임시 콘텐츠를 정리하기 위해 정리 작업이 자동으로 실행됩니다.

## 권한 {#permissions}

이전에는 클래식 UI에서 AEM을 쉽게 하기 위해(예: 사용) 특수 개발 고려 사항을 적용했습니다 `cq:text` 태그 라이브러리 또는 사용자 정의 통합 `DiffService` 구성 요소에 OSGi 서비스 참조). 이러한 diff는 DOM 비교를 통해 클라이언트측에서 수행되므로 더 이상 새로운 diff 기능에 필요하지 않습니다.

그러나 개발자는 많은 제한 사항을 고려해야 합니다.

* 이 기능은 AEM Product에 간격이 있지 않은 CSS 클래스를 사용합니다. 이름이 같은 다른 사용자 지정 CSS 클래스나 타사 CSS 클래스가 페이지에 포함되어 있는 경우 비교 표시가 영향을 받을 수 있습니다.

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* 비교는 클라이언트측이며 페이지 로드 시 실행되므로 클라이언트측 차이 서비스가 실행된 후 DOM에 대한 모든 조정은 계산되지 않습니다. 영향을 줄 수 있습니다

   * AJAX을 사용하여 컨텐츠를 포함하는 구성 요소
   * SPA (Single Page Applications)
   * 사용자 상호 작용 시 DOM을 조작하는 Javascript 기반 구성 요소입니다.

>[!NOTE]
>
>페이지 비교 비교는 유효한 cq:editConfig 노드가 있는 구성 요소에만 작동합니다.
