---
title: 대시보드
seo-title: 대시보드
description: 새 AEM 대시보드를 만들고, 구성하고, 개발하는 방법을 알아봅니다.
seo-description: 새 AEM 대시보드를 만들고, 구성하고, 개발하는 방법을 알아봅니다.
uuid: 3eadbba2-0ce1-41be-a9f8-e6cafa109893
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 40560e06-2508-45a4-a648-39629ed54f28
translation-type: tm+mt
source-git-commit: 69dfd6b41b32cb9131fd90fd7039a0c224889db5
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 59%

---


# 대시보드{#dashboards}

AEM 사용하면 다른 유형의 많은 컨텐트(예: 페이지, 자산)를 관리할 수 있습니다. AEM 대시보드에서는 통합된 데이터를 표시하는 페이지를 정의하는 사용하기 쉽고 사용자 지정 가능한 방법을 제공합니다.

>[!NOTE]
>
>AEM 대시보드는 사용자 기준별로 만들어지므로 사용자는 자신의 대시보드에만 액세스할 수 있습니다.
>
>그러나 [대시보드 템플릿](#creating-a-dashboard-template)은 일반적인 구성 및 대시보드 레이아웃을 공유하는 데 사용할 수 있습니다.

![chlimage_1-22](assets/chlimage_1-22.jpeg)

## 대시보드 관리 {#administering-dashboards}

### 대시보드 만들기 {#creating-a-dashboard}

새 대시보드를 만들려면, 다음과 같이 진행하십시오.

1. **도구** 섹션에서 **구성 콘솔**&#x200B;을 클릭합니다.
1. 트리에서 **대시보드**&#x200B;를 두 번 클릭합니다.
1. **새로운 대시보드**&#x200B;를 클릭합니다.
1. **제목**(예: 내 대시보드) 및 **이름**&#x200B;을 입력합니다.
1. **만들기**&#x200B;를 클릭합니다.

### 대시보드 복제 {#cloning-a-dashboard}

다른 보기의 컨텐트에 관한 정보를 빠르게 보기 위한 여러 대시보드를 원할 수 있습니다. 새로운 대시보드의 작성을 돕고자 AEM에서는 기존 대시보드를 복제하는 데 사용할 수 있는 복제 기능을 제공합니다. 대시보드를 복제하려면, 다음과 같이 진행하십시오.

1. **도구** 섹션에서 **구성 콘솔**&#x200B;을 클릭합니다.

1. 트리에서 **대시보드**&#x200B;를 클릭합니다.
1. 복제할 대시보드를 클릭합니다.

1. **복제**&#x200B;를 클릭합니다.

1. 새 대시보드의 **이름**&#x200B;을 입력합니다.

### 대시보드 제거  {#removing-a-dashboard}

1. **도구** 섹션에서 **구성 콘솔**&#x200B;을 클릭합니다.

1. 트리에서 **대시보드**&#x200B;를 클릭합니다.
1. 삭제할 대시보드를 클릭합니다.

1. **제거**&#x200B;를 클릭합니다.

1. **예**&#x200B;를 클릭하여 확인합니다.

## 대시보드 구성 요소  {#dashboard-components}

### 개요 {#overview}

대시보드 구성 요소는 일반 [AEM 구성 요소](/help/sites-developing/developing-components-samples.md)에 지나지 않습니다. 이 섹션에서는 AEM과 함께 제공되는 보고 구성 요소에 대해 설명합니다.

### 웹 분석 보고 구성 요소  {#web-analytics-reporting-components}

AEM에는 [SiteCatalyst](/help/sites-administering/adobeanalytics.md) 데이터의 여러 지표를 렌더링하는 구성 요소 세트가 포함되어 있습니다. 이러한 구성 요소들은 **대시보드** 섹션 아래의 사이드킥에 나열되어 있습니다.

각 보고 구성 요소에서는 최소한 세 개 이상의 탭을 제공합니다.

* **기본**: 기본 구성이 들어 있습니다.

* **보고서:** 각 보고서별 구성이 들어 있습니다.
* **스타일**: 차트 크기 및 여백과 같은 스타일 지정 구성이 들어 있습니다.

보고 구성 요소는 대시보드를 신속히 설정할 수 있도록 도와주는 기본 구성으로 초기화됩니다.

#### 기본 구성  {#basic-configuration}

**기본** 탭에서는 다음 구성 항목을 이용할 수 있습니다.

**** 제목대시보드에 표시되는 제목입니다.

**요청** 유형데이터를 요청하는 방법입니다.

**SiteCatalyst 구성(선택 사항)** SiteCatalyst에 연결하는 데 사용할 구성입니다. 제공되지 않을 경우 구성은 대시보드 페이지에서(페이지 속성을 통해) 구성되는 것으로 가정됩니다.

**보고서 세트 ID(선택 사항)** 그래프를 생성하는 데 사용할 SiteCatalyst 보고서 세트입니다.

#### 보고서 구성 {#report-configuration}

웹 통계를 표시하려면, 가져올 데이터의 날짜 범위를 정의해야 합니다. **보고서** 탭에서는 이 범위를 정의하는 두 개의 필드를 제공합니다.

>[!NOTE]
>
>날짜 범위를 크게 설정하면 대시보드의 응답이 느려질 수 있습니다.

**데이터** 를 가져오는 날짜의 절대 또는 상대 날짜입니다.

**데이터** 를 가져오는 날짜: 까지 또는 데이터가 가져오는 상대 날짜입니다.

각 구성 요소는 특정 설정도 정의합니다.

#### 초과 근무 보고서  {#overtime-report}

![chlimage_1-26](assets/chlimage_1-26a.png)

**날짜** 세부기간X축의 시간 단위(예: 일, 시간).

**지표** 표시할 이벤트 목록입니다.

**요소** 그래프에서 지표 데이터를 분류하는 요소 목록입니다.

#### 등급 목록 보고서 {#ranked-list-report}

![chlimage_1-27](assets/chlimage_1-27a.png)

**요소** 그래프에서 지표 데이터를 분류하는 요소입니다.

**지표** 표시할 이벤트입니다.

**아니오. 상위 항목** 보고서에 표시되는 항목 수입니다.

#### 등급 보고서 {#ranked-report}

![chlimage_1-28](assets/chlimage_1-28a.png)

**지표** 표시할 이벤트입니다.

**요소** 그래프에서 지표 데이터를 분류하는 요소입니다.

#### 인기 사이트 섹션 보고서 {#top-site-section-report}

이 구성 요소에는 다음 구성에 따라 웹 사이트에 있는 방문 섹션을 더 많이 보여 주는 그래프가 표시됩니다.

![chlimage_1-29](assets/chlimage_1-29a.png)

**아니오. 상위 항목** 보고서에 표시되는 섹션 수입니다.

#### 트렌드 보고서 {#trended-report}

![chlimage_1-30](assets/chlimage_1-30a.png)

**날짜** 세부기간X축의 시간 단위(예: 일, 시간).

**지표** 표시할 이벤트입니다.

**요소** 그래프에서 지표 데이터를 분류하는 요소입니다.

## 대시보드 확장 {#extending-dashboard}

### 개요 {#overview-1}

대시보드는 일반적인 페이지(`cq:Page`)이므로, 대시보드를 만드는 데 모든 구성 요소를 사용할 수 있습니다.

기본적으로 템플릿에서 활성화된 분석 보고 구성 요소를 포함하는 기본 구성 요소 그룹 `Dashboard`이 있습니다.

### 대시보드 템플릿 만들기 {#creating-a-dashboard-template}

템플릿은 새로운 대시보드의 기본 컨텐트를 정의합니다. 다양한 유형의 대시보드를 만드는 데 여러 개의 템플릿을 사용할 수 있습니다.

대시보드 템플릿은 `/libs/cq/dashboards/templates/` 아래에 저장된다는 점을 제외하고 다른 페이지 템플릿과 마찬가지로 만들어집니다. [컨텐트 페이지 템플릿 만들기](/help/sites-developing/website.md#creating-the-contentpage-template) 섹션을 참조하십시오.

>[!NOTE]
>
>대시보드 템플릿은 사용자 간에 공유됩니다.

### 대시보드 구성 요소 개발  {#developing-a-dashboard-component}

대시보드 구성 개발은 일반적인 AEM 구성 요소를 만드는 것으로 이루어집니다. 이 섹션에서는 기여 요소 중 상위 10개를 표시하는 구성 요소의 예에 대해 설명합니다.

![chlimage_1-31](assets/chlimage_1-31a.png)

상위 작성자 구성 요소는 `/apps/geometrixx-outdoors/components/reporting`의 저장소에 저장되고 다음과 같이 구성됩니다.

1. jcr 데이터를 읽고 `jsp` 자리 표시자를 정의하는 `html` 파일입니다.

1. 데이터를 가져오고 순서를 지정한 다음 `js` 자리 표시자를 채우는 `html` 파일 하나가 들어 있는 클라이언트측 라이브러리입니다.

![chlimage_1-32](assets/chlimage_1-32a.png)

다음 Javascript 파일은 `geout.reporting.topauthors` [클라이언트 라이브러리](/help/sites-developing/clientlibs.md)에 구성 요소 자체의 하위로 정의됩니다.

[QueryBuilder](/help/sites-developing/querybuilder-api.md)는 저장소를 쿼리하여 `cq:AuditEvent` 노드를 읽는 데 사용됩니다. 쿼리 결과는 작성한 기고물이 추출되는 JSON 개체입니다.

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

`JSP`에는 `global.jsp` 및 `clientlib`가 모두 포함되어 있습니다.

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

