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
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# 개발 및 페이지 비교{#developing-and-page-diff}

## 기능 개요 {#feature-overview}

컨텐츠 작성은 반복적 프로세스입니다. 효율적인 작성을 위해서는 한 번 반복할 때마다 변경된 내용을 확인할 수 있어야 합니다. 한 페이지 버전을 확인한 다음, 다른 한 버전을 확인하는 것은 비효율적이며 오류가 발생하기 쉽습니다. 작성자는 현재 페이지를 이전 버전과 비교하고 차이점을 강조 표시하기를 원합니다.

페이지 비교를 사용하면 현재 페이지를 론치, 이전 버전 등과 비교할 수 있습니다. 이 사용자 기능에 대한 자세한 내용은 페이지 [비교를 참조하십시오](/help/sites-authoring/page-diff.md).

## 작업 세부 사항 {#operation-details}

페이지 버전을 비교할 때 사용자가 비교하려는 이전 버전은 비교를 용이하게 하기 위해 백그라운드에서 AEM에 의해 다시 만들어집니다. 이는 컨텐츠를 나란히 놓고 비교할 [수 있도록 렌더링하는 데 필요합니다](/help/sites-developing/pagediff.md#operation-details).

이 레크리에이션 작업은 AEM에서 내부적으로 수행되며 사용자에게 투명하며 개입할 필요가 없습니다. 그러나 CRX DE Lite에서 저장소를 보는 관리자는 컨텐츠 구조 내에서 이러한 재구성된 버전을 보게 됩니다.

컨텐츠를 비교할 때 비교할 페이지까지 전체 트리가 다음 위치에 다시 만들어집니다.

`/tmp/versionhistory/`

정리 작업이 자동으로 실행되어 이 임시 컨텐츠를 정리할 수 있습니다.

## 권한 {#permissions}

이전에는 클래식 UI에서 AEM 차단을 용이하게 하기 위해( `cq:text` 태그 라이브러리 사용 또는 OSGi 서비스를 구성 요소에 통합하는 사용자 지정 등) `DiffService` 특별한 개발 고려가 수행되었습니다. DOM 비교를 통해 클라이언트측에서 비교되므로 새로운 비교 기능에 더 이상 필요하지 않습니다.

그러나 개발자는 고려해야 하는 많은 제한 사항이 있습니다.

* 이 기능은 AEM 제품에 대해 이름이 배치되지 않은 CSS 클래스를 사용합니다. 이름이 같은 다른 사용자 지정 CSS 클래스나 타사 CSS 클래스가 페이지에 포함되어 있는 경우 비교 표시에 영향을 줄 수 있습니다.

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* 비교는 클라이언트측에서 실행되며 페이지 로드에서 실행되므로 클라이언트측 비교 서비스가 실행된 후 DOM에 대한 모든 조정 내용은 계산되지 않습니다. 이 문제는

   * AJAX를 사용하여 컨텐츠를 포함하는 구성 요소
   * 단일 페이지 애플리케이션
   * 사용자 상호 작용에 따라 DOM을 조작하는 Javascript 기반 구성 요소입니다.
