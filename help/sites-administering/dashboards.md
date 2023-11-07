---
title: 대시보드
seo-title: Dashboards
description: 새 AEM 대시보드를 만들고, 구성하고, 개발하는 방법에 대해 알아봅니다.
seo-description: Learn how to create, configure and develop new AEM dashboards.
uuid: 3eadbba2-0ce1-41be-a9f8-e6cafa109893
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 40560e06-2508-45a4-a648-39629ed54f28
exl-id: 5b934e3a-f554-46ec-a913-8d570abb1503
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 4%

---

# 대시보드{#dashboards}

AEM을 사용할 때 다양한 유형의 콘텐츠(예: 페이지, 에셋)를 관리할 수 있습니다. AEM 대시보드는 통합된 데이터를 표시하는 페이지를 정의하는 사용하기 쉽고 사용자 정의 가능한 방법을 제공합니다.

>[!NOTE]
>
>AEM 대시보드는 사용자별로 생성되므로 사용자는 자신의 대시보드에만 액세스할 수 있습니다.
>
>그러나 [대시보드 템플릿](#creating-a-dashboard-template) 를 사용하여 공통 구성 및 대시보드 레이아웃을 공유할 수 있습니다.

![chlimage_1-22](assets/chlimage_1-22.jpeg)

## 대시보드 관리 {#administering-dashboards}

### 대시보드 만들기 {#creating-a-dashboard}

1. 다음에서 **도구** 섹션, 클릭 **구성 콘솔**.
1. 트리에서 를 두 번 클릭합니다 **대시보드**.
1. 클릭 **새 대시보드**.
1. 을(를) 입력합니다 **제목** (예: 내 대시보드) 및 **이름**.
1. **만들기**&#x200B;를 클릭합니다.

### 대시보드 복제 {#cloning-a-dashboard}

여러 대시보드를 사용하여 서로 다른 보기에서 콘텐츠에 대한 정보를 빠르게 볼 수 있습니다. 새 대시보드를 만드는 데 도움이 되도록 AEM에서는 기존 대시보드를 복제하는 데 사용할 수 있는 복제 기능을 제공합니다. 대시보드를 복제하려면 다음과 같이 진행합니다.

1. 다음에서 **도구** 섹션, 클릭 **구성 콘솔**.

1. 트리에서 **대시보드**.
1. 복제할 대시보드를 클릭합니다.

1. 클릭 **복제**.

1. 을(를) 입력합니다 **이름** 새 대시보드에 대한 액세스 권한을 부여했습니다.

### 대시보드 제거 {#removing-a-dashboard}

1. 다음에서 **도구** 섹션, 클릭 **구성 콘솔**.

1. 트리에서 **대시보드**.
1. 삭제할 대시보드에서 를 클릭합니다.

1. **제거**&#x200B;를 클릭합니다.

1. **예**&#x200B;를 클릭하여 확인합니다.

## 대시보드 구성 요소 {#dashboard-components}

### 개요 {#overview}

대시보드 구성 요소는 일반에 불과합니다. [AEM 구성 요소](/help/sites-developing/developing-components-samples.md). 이 섹션에서는 AEM과 함께 제공되는 보고 구성 요소에 대해 설명합니다.

### 웹 분석 보고 구성 요소 {#web-analytics-reporting-components}

AEM은 의 여러 지표를 렌더링하는 구성 요소 세트와 함께 제공됩니다. [SiteCatalyst](/help/sites-administering/adobeanalytics.md) 데이터. 이러한 구성 요소는 아래 Sidekick에 나열되어 있습니다. **대시보드** 섹션.

각 보고 구성 요소에는 세 개 이상의 탭이 있습니다.

* **기본**: 기본 구성을 포함합니다.

* **보고서:** 각 보고서에 대한 구성을 포함합니다.
* **스타일**: 차트 크기 및 여백과 같은 스타일 구성이 포함됩니다.

보고 구성 요소는 대시보드를 빠르게 설정할 수 있는 기본 구성으로 초기화됩니다.

#### 기본 구성 {#basic-configuration}

다음 **기본** 탭에서는 다음 구성 항목에 액세스할 수 있습니다.

**제목** 대시보드에 표시된 제목입니다.

**요청 유형** 데이터 요청 방식.

**SiteCatalyst 구성(선택 사항)** SiteCatalyst에 연결하는 데 사용할 구성입니다. 제공되지 않으면 구성은 대시보드 페이지에 구성된 것으로 간주됩니다(페이지 속성을 통해).

**보고서 세트 ID (선택 사항)** 그래프를 생성하는 데 사용할 SiteCatalyst 보고서 세트입니다.

#### 보고서 구성 {#report-configuration}

웹 통계를 표시하려면 채울 데이터의 날짜 범위를 정의해야 합니다. 다음 **보고서** 탭은 해당 범위를 정의하는 두 개의 필드를 제공합니다.

>[!NOTE]
>
>날짜 범위를 크게 설정하면 대시보드의 응답성이 저하될 수 있습니다.

**시작 날짜** 데이터를 가져오는 절대 또는 상대적 날짜.

**종료 날짜** 데이터를 가져오는 절대 또는 상대적 날짜.

각 구성 요소는 특정 설정도 정의합니다.

#### 초과 근무 보고서 {#overtime-report}

![chlimage_1-26](assets/chlimage_1-26a.png)

**날짜 세부기간** X축의 시간 단위(예: 일, 시간)입니다.

**지표** 표시할 이벤트 목록입니다.

**요소** 그래프에서 지표 데이터를 분류하는 요소 목록입니다.

#### 등급 목록 보고서 {#ranked-list-report}

![chlimage_1-27](assets/chlimage_1-27a.png)

**요소** 그래프에서 지표 데이터를 분류하는 요소입니다.

**지표** 표시할 이벤트입니다.

**아니요. 상위 항목 중** 보고서에 표시된 항목 수입니다.

#### 등급 보고서 {#ranked-report}

![chlimage_1-28](assets/chlimage_1-28a.png)

**지표** 표시할 이벤트입니다.

**요소** 그래프에서 지표 데이터를 분류하는 요소입니다.

#### 인기 사이트 섹션 보고서 {#top-site-section-report}

이 구성 요소는 다음 구성에 따라 웹 사이트의 방문 횟수가 더 많은 섹션을 보여 주는 그래프를 표시합니다.

![chlimage_1-29](assets/chlimage_1-29a.png)

**아니요. 상위 항목 중** 보고서에 표시되는 섹션 수.

#### 트렌드 보고서 {#trended-report}

![chlimage_1-30](assets/chlimage_1-30a.png)

**날짜 세부기간** X축의 시간 단위(예: 일, 시간)입니다.

**지표** 표시할 이벤트입니다.

**요소** 그래프에서 지표 데이터를 분류하는 요소입니다.

## 대시보드 확장 {#extending-dashboard}

### 개요 {#overview-1}

대시보드는 일반 페이지임( `cq:Page`) 따라서 모든 구성 요소를 사용하여 대시보드를 어셈블할 수 있습니다.

기본 구성 요소 그룹이 있습니다. `Dashboard` 기본적으로 템플릿에 활성화되어 있는 analytics 보고 구성 요소를 포함합니다.

### 대시보드 템플릿 만들기 {#creating-a-dashboard-template}

템플릿은 새 대시보드의 기본 콘텐츠를 정의합니다. 여러 유형의 대시보드를 만드는 데 여러 템플릿을 사용할 수 있습니다.

대시보드 템플릿은 아래에 저장된다는 점을 제외하면 다른 페이지 템플릿과 같이 생성됩니다. `/libs/cq/dashboards/templates/`. 다음을 참조하십시오. [Contentpage 템플릿 만들기](/help/sites-developing/website.md#creating-the-contentpage-template) 섹션.

>[!NOTE]
>
>대시보드 템플릿은 사용자 간에 공유됩니다.

### 대시보드 구성 요소 개발 {#developing-a-dashboard-component}

대시보드 구성 요소 개발은 일반 AEM 구성 요소 생성으로 구성됩니다. 이 섹션에서는 상위 10개의 기여자를 표시하는 구성 요소의 예를 설명합니다.

![chlimage_1-31](assets/chlimage_1-31a.png)

상위 작성자 구성 요소는 다음 위치의 저장소에 저장됩니다. `/apps/geometrixx-outdoors/components/reporting` 및 는 로 구성됩니다.

1. a `jsp` jcr 데이터를 읽고 다음을 정의하는 파일 `html` 자리 표시자.

1. 클라이언트 측 라이브러리 `js` 데이터를 가져오고 정렬한 다음 `html` 자리 표시자.

![chlimage_1-32](assets/chlimage_1-32a.png)

다음 JavaScript 파일은에 정의되어 있습니다. `geout.reporting.topauthors` [클라이언트 라이브러리](/help/sites-developing/clientlibs.md) 구성 요소 자체의 하위 항목으로 사용됩니다.

다음 [QueryBuilder](/help/sites-developing/querybuilder-api.md) 은 읽을 저장소를 쿼리하는 데 사용됩니다. `cq:AuditEvent` 노드. 쿼리 결과는 작성자 기여도가 추출되는 JSON 개체입니다.

#### top_authors.js {#top-authors-js}

```
$.ajax({
  url: "/bin/querybuilder.json",
  cache: false,
  data: {
       "orderby": "cq:time",
       "orderby.sort": "desc",
       "p.hits": "full",
       "p.limit": 100,
       "path": "/var/audit/com.day.cq.wcm.core.page/",
       "type": "cq:AuditEvent"
   },
  dataType: "json"
}).done(function( res ) {
    var authors = {};
    // from JSON to Object
    for(var r in res.hits) {
        var userId = res.hits[r].userId;
        if(userId == undefined) {
            continue;
        }
        var auth = authors[userId] || {userId : userId};
        auth.contrib = (auth.contrib || 0) +1;

        authors[userId] = auth;
    }

    // order by contribution
    var orderedByContrib = [];
    for(var a in authors) {
        orderedByContrib.push(authors[a]);
    }
    orderedByContrib.sort(function(a,b){return b.contrib - a.contrib});

    // produce the list
    for (var i=0, tot=orderedByContrib.length; i < tot; i++) {
        var current = orderedByContrib[i];
        $("<div> #" + (i + 1) +" "+ current.userId + " (" + current.contrib +" contrib.)</div>").appendTo("#authors-list");

    }
});
```

다음 `JSP` 모두 포함 `global.jsp` 및 `clientlib`.

#### top_authors.jsp {#top-authors-jsp}

```java
<%@page session="false" contentType="text/html; charset=utf-8" %><%
%><%
%><%@include file="/libs/foundation/global.jsp" %><%
%>
<ui:includeClientLib categories="geout.reporting.topauthors" />
<%
String reportletTitle = properties.get("title", "Top Authors");
%>
<html>
     <h3><%=xssAPI.encodeForHTML(reportletTitle) %></h3>
     <div id="authors-list"></div>
</html>
```
