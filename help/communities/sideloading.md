---
title: 구성 요소 사이드로딩
seo-title: 구성 요소 사이드로딩
description: 커뮤니티 구성 요소 사이드로드는 웹 페이지가 사이트 방문자가 선택한 항목에 따라 표시되는 내용을 동적으로 변경하는 간단한 단일 페이지 앱으로 디자인될 때 유용합니다
seo-description: 커뮤니티 구성 요소 사이드로드는 웹 페이지가 사이트 방문자가 선택한 항목에 따라 표시되는 내용을 동적으로 변경하는 간단한 단일 페이지 앱으로 디자인될 때 유용합니다
uuid: 8c9a5fde-26a3-4610-bc14-f8b665059015
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a9cb5294-e5ab-445b-b7c2-ffeecda91c50
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---


# 구성 요소 사이드로드 {#component-sideloading}

## 개요 {#overview}

커뮤니티 구성 요소 사이드 로드는 사이트 방문자가 선택한 항목에 따라 표시되는 내용을 동적으로 변경하는 간단한 단일 페이지 앱으로 웹 페이지를 디자인할 때 유용합니다.

이 작업은 커뮤니티 구성 요소가 페이지 템플릿에 없을 때 수행되지만 사이트 방문자가 선택한 후에 동적으로 추가됩니다.

SCF(소셜 구성 요소 프레임워크)에 작은 크기의 존재가 있으므로 초기 페이지 로드 시 존재하는 SCF 구성 요소만 등록됩니다. 페이지를 로드한 후 동적으로 추가된 SCF 구성 요소를 등록하려면 SCF를 구성 요소의 &quot;사이드로드&quot;로 호출해야 합니다.

페이지가 커뮤니티 구성 요소를 사이드로드하도록 설계되면 전체 페이지를 캐시할 수 있습니다.

SCF 구성 요소를 동적으로 추가하는 단계는 다음과 같습니다.

1. [DOM에 구성 요소 추가](#dynamically-add-component-to-dom)

1. [다음 두 가지 방법 ](#sideload-by-invoking-scf) 중 하나를 사용하여 구성 요소를 사이드 로드합니다.

* [동적 포함](#dynamic-inclusion)
   * 동적으로 추가된 모든 구성 요소 부스트링
* [동적 로드](#dynamic-loading)
   * 특정 구성 요소 on-demand 추가

>[!NOTE]
>
>[기존 리소스](scf.md#add-or-include-a-communities-component)의 사이드로드는 지원되지 않습니다.

## DOM {#dynamically-add-component-to-dom}에 구성 요소 동적으로 추가

구성 요소가 동적으로 포함되어 있는지 동적으로 로드되는지 여부에 관계없이 먼저 DOM에 추가해야 합니다.

SCF 구성 요소를 추가할 때 사용하는 가장 일반적인 태그는 DIV 태그이지만 다른 태그도 사용할 수 있습니다. SCF는 페이지가 처음에 로드될 때 DOM만 검사하므로 SCF가 명시적으로 호출될 때까지 DOM에 추가되는 것은 눈에 띄지 않습니다.

태그를 어떤 태그로 사용하든, 요소는 다음과 같은 두 속성을 포함함으로써 일반적인 SCF 루트 요소 패턴을 준수해야 합니다.

* **data-component-id**

   추가된 구성 요소에 대한 유효 경로입니다.

* **data-scf-component**

   구성 요소의 resourceType입니다.

다음은 추가된 주석 구성 요소의 한 예입니다.

```xml
<div
    class="scf-commentsystem scf translation-commentsystem"
    data-component-id="<%= currentPage.getPath()%>/jcr:content/content-left/comments"
    data-scf-component="social/commons/components/hbs/comments"
>
</div>
```

## SCF 호출 시 사이드 로드({#sideload-by-invoking-scf})

### 동적 포함 {#dynamic-inclusion}

동적 포함은 SCF가 페이지에 있는 모든 SCF 구성 요소를 부트스트래핑하고 DOM을 검사하도록 하는 부스트랩 요청을 사용합니다.

페이지를 로드한 후 언제든지 SCF 구성 요소를 초기화하려면 다음과 같은 JQuery 이벤트를 실행하기만 하면 됩니다.

`$(document).trigger(SCF.events.BOOTSTRAP_REQUEST);`

### 동적 로드 {#dynamic-loading}

동적 로드는 SCF 구성 요소 로드를 제어합니다.

DOM에 있는 모든 SCF 구성 요소를 부트스트래핑하는 대신 이 JavaScript 메서드를 사용하여 로드할 특정 SCF 구성 요소를 지정할 수 있습니다.

`SCF.addComponent(document.getElementById(*someId*));`

여기서 `someId`은 `data-component-id` 속성의 값입니다.
