---
title: 대시보드
description: 새 AEM 대시보드를 만들고, 구성하고, 개발하는 방법에 대해 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: 5b934e3a-f554-46ec-a913-8d570abb1503
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 4%

---

# 대시보드{#dashboards}

AEM을 사용할 때 다양한 유형의 수많은 콘텐츠(예: 페이지, 에셋)를 관리할 수 있습니다. AEM 대시보드는 통합된 데이터를 표시하는 페이지를 정의하는 사용하기 쉽고 사용자 정의 가능한 방법을 제공합니다.

>[!NOTE]
>
>AEM 대시보드는 사용자별로 생성되므로 사용자는 자신의 대시보드에만 액세스할 수 있습니다.
>
>그러나 [대시보드 템플릿](#creating-a-dashboard-template)을(를) 사용하여 공통 구성과 대시보드 레이아웃을 공유할 수 있습니다.

![chlimage_1-22](assets/chlimage_1-22.jpeg)

## 대시보드 관리 {#administering-dashboards}

### 대시보드 만들기 {#creating-a-dashboard}

1. **도구** 섹션에서 **구성 콘솔**&#x200B;을 클릭합니다.
1. 트리에서 **대시보드**&#x200B;를 두 번 클릭합니다.
1. **새 대시보드**&#x200B;를 클릭합니다.
1. **제목**(예: 내 대시보드)과 **이름**&#x200B;을(를) 입력하십시오.
1. **만들기**&#x200B;를 클릭합니다.

### 대시보드 복제 {#cloning-a-dashboard}

여러 대시보드를 사용하여 서로 다른 보기에서 콘텐츠에 대한 정보를 빠르게 볼 수 있습니다. 새 대시보드를 만드는 데 도움이 되도록 AEM에서는 기존 대시보드를 복제하는 데 사용할 수 있는 복제 기능을 제공합니다. 대시보드를 복제하려면 다음과 같이 진행합니다.

1. **도구** 섹션에서 **구성 콘솔**&#x200B;을 클릭합니다.

1. 트리에서 **대시보드**&#x200B;를 클릭합니다.
1. 복제할 대시보드를 클릭합니다.

1. **복제**&#x200B;를 클릭합니다.

1. 새 대시보드의 **이름**&#x200B;을(를) 입력하십시오.

### 대시보드 제거 {#removing-a-dashboard}

1. **도구** 섹션에서 **구성 콘솔**&#x200B;을 클릭합니다.

1. 트리에서 **대시보드**&#x200B;를 클릭합니다.
1. 삭제할 대시보드에서 를 클릭합니다.

1. **제거**&#x200B;를 클릭합니다.

1. **예**&#x200B;를 클릭하여 확인합니다.

## 대시보드 구성 요소 {#dashboard-components}

### 개요 {#overview}

대시보드 구성 요소는 일반 [AEM 구성 요소](/help/sites-developing/developing-components-samples.md)에 불과합니다. 이 섹션에서는 AEM과 함께 제공되는 보고 구성 요소에 대해 설명합니다.

### 웹 분석 보고 구성 요소 {#web-analytics-reporting-components}

AEM에는 [SiteCatalyst](/help/sites-administering/adobeanalytics.md) 데이터의 여러 지표를 렌더링하는 구성 요소 집합이 포함되어 있습니다. 이러한 구성 요소는 **대시보드** 섹션 아래의 Sidekick에 나열됩니다.

각 보고 구성 요소에는 세 개 이상의 탭이 있습니다.

* **기본**: 기본 구성을 포함합니다.

* **보고서:**&#x200B;에는 각 보고서에 대한 구성이 포함됩니다.
* **스타일**: 차트 크기 및 여백과 같은 스타일 구성이 포함됩니다.

보고 구성 요소는 대시보드를 빠르게 설정할 수 있는 기본 구성으로 초기화됩니다.

#### 기본 구성 {#basic-configuration}

**기본** 탭에서는 다음 구성 항목에 액세스할 수 있습니다.

**제목** 대시보드에 표시된 제목입니다.

**요청 유형** 데이터가 요청되는 방식입니다.

**SiteCatalyst 구성(선택 사항)** SiteCatalyst 연결에 사용할 구성입니다. 제공되지 않으면 구성은 대시보드 페이지에 구성된 것으로 간주됩니다(페이지 속성을 통해).

**보고서 세트 ID(선택 사항)** 그래프를 생성하는 데 사용할 SiteCatalyst 보고서 세트입니다.

#### 보고서 구성 {#report-configuration}

웹 통계를 표시하려면 채울 데이터의 날짜 범위를 정의해야 합니다. **보고서** 탭에는 해당 범위를 정의하는 두 개의 필드가 있습니다.

>[!NOTE]
>
>날짜 범위를 크게 설정하면 대시보드의 응답성이 저하될 수 있습니다.

**시작 날짜** 데이터를 가져오는 절대 또는 상대 날짜입니다.

**종료 날짜** 데이터를 가져오는 절대 또는 상대 날짜입니다.

각 구성 요소는 특정 설정도 정의합니다.

#### 초과 근무 보고서 {#overtime-report}

![chlimage_1-26](assets/chlimage_1-26a.png)

**날짜 세부 기간** X축의 시간 단위(예: 일, 시간)입니다.

**지표** 표시할 이벤트 목록입니다.

**요소** 그래프에서 지표 데이터를 분류하는 요소 목록입니다.

#### 등급 목록 보고서 {#ranked-list-report}

![chlimage_1-27](assets/chlimage_1-27a.png)

**요소** 그래프에서 지표 데이터를 분류하는 요소입니다.

**지표** 표시할 이벤트입니다.

**아니요. of top items** 보고서에 표시된 항목 수입니다.

#### 등급 보고서 {#ranked-report}

![chlimage_1-28](assets/chlimage_1-28a.png)

**지표** 표시할 이벤트입니다.

**요소** 그래프에서 지표 데이터를 분류하는 요소입니다.

#### 인기 사이트 섹션 보고서 {#top-site-section-report}

이 구성 요소는 다음 구성에 따라 웹 사이트의 방문 횟수가 더 많은 섹션을 보여 주는 그래프를 표시합니다.

![chlimage_1-29](assets/chlimage_1-29a.png)

**아니요. 보고서에 표시되는 상위 항목** 섹션의 수입니다.

#### 트렌드 보고서 {#trended-report}

![chlimage_1-30](assets/chlimage_1-30a.png)

**날짜 세부 기간** X축의 시간 단위(예: 일, 시간)입니다.

**지표** 표시할 이벤트입니다.

**요소** 그래프에서 지표 데이터를 분류하는 요소입니다.

## 대시보드 확장 {#extending-dashboard}

### 개요 {#overview-1}

대시보드는 일반 페이지(`cq:Page`)이므로 모든 구성 요소를 사용하여 대시보드를 어셈블할 수 있습니다.

기본적으로 템플릿에 활성화되어 있는 분석 보고 구성 요소를 포함하는 기본 구성 요소 그룹 `Dashboard`이(가) 있습니다.

### 대시보드 템플릿 만들기 {#creating-a-dashboard-template}

템플릿은 새 대시보드의 기본 콘텐츠를 정의합니다. 여러 유형의 대시보드를 만드는 데 여러 템플릿을 사용할 수 있습니다.

대시보드 템플릿은 `/libs/cq/dashboards/templates/`에 저장된다는 점을 제외하면 다른 페이지 템플릿과 같이 만들어집니다. [Contentpage 템플릿 만들기](/help/sites-developing/website.md#creating-the-contentpage-template) 섹션을 참조하십시오.

>[!NOTE]
>
>대시보드 템플릿은 사용자 간에 공유됩니다.

### 대시보드 구성 요소 개발 {#developing-a-dashboard-component}

대시보드 구성 요소 개발은 일반 AEM 구성 요소 생성으로 구성됩니다. 이 섹션에서는 상위 10개의 기여자를 표시하는 구성 요소의 예를 설명합니다.

![chlimage_1-31](assets/chlimage_1-31a.png)

최상위 작성자 구성 요소는 `/apps/geometrixx-outdoors/components/reporting`의 저장소에 저장되며 다음으로 구성됩니다.

1. jcr 데이터를 읽고 `html` 자리 표시자를 정의하는 `jsp` 파일입니다.

1. 데이터를 가져와서 정렬한 다음 `html` 자리 표시자를 채우는 하나의 `js` 파일이 들어 있는 클라이언트측 라이브러리입니다.

![chlimage_1-32](assets/chlimage_1-32a.png)

다음 JavaScript 파일이 `geout.reporting.topauthors` [클라이언트 라이브러리](/help/sites-developing/clientlibs.md)에 구성 요소 자체의 하위 항목으로 정의되어 있습니다.

[QueryBuilder](/help/sites-developing/querybuilder-api.md)은(는) 저장소를 쿼리하여 `cq:AuditEvent`개의 노드를 읽는 데 사용됩니다. 쿼리 결과는 작성자 기여도가 추출되는 JSON 개체입니다.

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

`JSP`에 `global.jsp`과(와) `clientlib`이(가) 모두 포함되어 있습니다.

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
