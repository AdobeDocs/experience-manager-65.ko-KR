---
title: 구성 요소 테스트용 로드
description: 커뮤니티 구성 요소 사이드로드는 웹 페이지가 사이트 방문자가 선택한 항목에 따라 표시되는 내용을 동적으로 변경하는 간단한 단일 페이지 앱으로 디자인될 때 유용합니다
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 960e132c-b370-43d1-bd8f-e7d0ded7c0b3
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# 구성 요소 사이드로드 {#component-sideloading}

## 개요 {#overview}

커뮤니티 구성 요소 사이드로드는 웹 페이지가 사이트 방문자가 선택한 항목에 따라 표시되는 내용을 동적으로 변경하는 간단한 단일 페이지 앱으로 디자인될 때 유용합니다.

이 작업은 Communities 구성 요소가 페이지 템플릿에 없지만 대신 사이트 방문자 선택에 따라 동적으로 추가되는 경우에 수행됩니다.

SCF(소셜 구성 요소 프레임워크)는 존재감이 낮기 때문에 초기 페이지 로드 시 존재하는 SCF 구성 요소만 등록됩니다. 동적으로 추가된 SCF 구성 요소를 페이지 로드 후 등록하려면 SCF를 호출하여 구성 요소를 &quot;테스트용으로 로드&quot;해야 합니다.

페이지가 Communities 구성 요소를 테스트용으로 로드하도록 디자인된 경우 전체 페이지를 캐시할 수 있습니다.

SCF 구성 요소를 동적으로 추가하는 단계는 다음과 같습니다.

1. [DOM에 구성 요소 추가](#dynamically-add-component-to-dom)

1. [다음 두 가지 방법 중 하나를 사용하여 구성 요소를](#sideload-by-invoking-scf) 테스트용으로 로드합니다.

* [동적 포용](#dynamic-inclusion)
   * 동적으로 추가된 모든 성분 Boostrap
* [동적 로드](#dynamic-loading)
   * 주문형 구성 요소 1개 추가

>[!NOTE]
>
>존재하지 않는 리소스](scf.md#add-or-include-a-communities-component)의 [테스트용 로드는 지원되지 않습니다.

## 동적으로 DOM에 구성 요소 추가 {#dynamically-add-component-to-dom}

구성 요소가 동적으로 포함되든 동적으로 로드되든 먼저 DOM에 추가해야 합니다.

SCF 구성 요소를 추가할 때 사용하는 가장 일반적인 태그는 DIV 태그이지만 다른 태그도 사용할 수 있습니다. SCF는 페이지 처음 로드될 때만 DOM을 검사하기 때문에 SCF가 명시적으로 호출될 때까지 DOM에 대한 이러한 추가는 눈에 띄지 않습니다.

어떤 태그 사용하든 최소한 요소는 다음 두 가지 특성을 포함하여 일반 SCF 루트 요소 패턴을 따라야 합니다.

* **데이터 구성 요소 ID**

  추가된 구성 요소에 대한 유효 경로입니다.

* **data-scf-component**

  구성 요소의 resourceType.

다음은 추가된 주석 구성 요소의 한 예입니다.

```xml
<div
    class="scf-commentsystem scf translation-commentsystem"
    data-component-id="<%= currentPage.getPath()%>/jcr:content/content-left/comments"
    data-scf-component="social/commons/components/hbs/comments"
>
</div>
```

## SCF를 호출하여 사이드로드 {#sideload-by-invoking-scf}

### 동적 포용 {#dynamic-inclusion}

동적 포함은 SCF가 DOM을 검사하고 페이지 상의 모든 SCF 구성요소를 부트랩하도록 하는 부스트랩 요청 기능을 사용합니다.

로드 후 언제든지 SCF 구성 요소를 초기화페이지 다음과 좋아요 JQuery 이벤트를 실행하기만 하면 됩니다.

`$(document).trigger(SCF.events.BOOTSTRAP_REQUEST);`

### 동적 로딩 {#dynamic-loading}

동적 로드를 통해 SCF 구성 요소 로드를 제어할 수 있습니다.

DOM에 있는 모든 SCF 구성 요소를 부트스트랩하는 대신 다음 JavaScript 메서드를 사용하여 로드할 특정 SCF 구성 요소를 지정할 수 있습니다.

`SCF.addComponent(document.getElementById(*someId*));`

여기서 `someId` 는 속성 값입니다 `data-component-id` .
