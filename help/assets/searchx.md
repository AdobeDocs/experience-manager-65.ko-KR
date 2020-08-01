---
title: 의 검색 기능을 [!DNL Adobe Experience Manager Assets]확장합니다.
description: 기본값 [!DNL Adobe Experience Manager Assets] 을 벗어나는 검색 기능을 확장합니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 7%

---


# 자산 검색 확장 {#extending-assets-search}

검색 기능을 확장할 수 [!DNL Adobe Experience Manager Assets] 있습니다. 기본적으로 문자열별로 자산을 [!DNL Experience Manager Assets] 검색합니다.

검색은 QueryBuilder 인터페이스를 통해 수행되므로 여러 예측자로 검색을 사용자 정의할 수 있습니다. 다음 디렉토리에 기본 예측 세트를 오버레이할 수 있습니다. `/apps/dam/content/search/searchpanel/facets`.

관리 패널에 탭을 더 추가할 수도 [!DNL Assets] 있습니다.

>[!CAUTION]
>
>6.4부터 클래식 UI는 더 이상 사용되지 않습니다. [!DNL Experience Manager] 자세한 내용은 [더 이상 사용되지 않는 기능 및 제거된 기능을 참조하십시오](https://docs.adobe.com/content/help/en/experience-manager-64/release-notes/deprecated-removed-features.html). Adobe은 터치 지원 UI를 사용하는 것이 좋습니다. 사용자 정의에 대해서는 [검색 패싯을 참조하십시오](/help/assets/search-facets.md).

## 오버레이 {#overlaying}

사전 구성된 조건자를 오버레이하려면 `facets` 노드를 다음으로 복사하거나 구성 `/libs/dam/content/search/searchpanel` 에서 다른 `/apps/dam/content/search/searchpanel/` 속성 `facetURL` 을 지정합니다(기본값 `searchpanel` `/libs/dam/content/search/searchpanel/facets.overlay.infinity.json`).

![screen_shot_2012-06-05at113619am](assets/screen_shot_2012-06-05at113619am.png)

>[!NOTE]
>
>기본적으로 아래 디렉토리 구조가 `/apps` 없으므로 만듭니다. 노드 유형이 아래 유형과 일치하는지 `/libs`확인합니다.

## 탭 추가 {#adding-tabs}

관리 인터페이스에서 검색 탭을 구성하여 추가 검색 탭을 추가할 수 [!DNL Assets] 있습니다. 추가 탭을 만들려면

1. 폴더 구조가 없는 `/apps/wcm/core/content/damadmin/tabs,`경우 폴더 구조를 만들고, `tabs` 노드를 복사한 후 붙여넣습니다 `/libs/wcm/core/content/damadmin` .
1. 원하는 대로 두 번째 탭을 만들고 구성합니다.

   >[!NOTE]
   >
   >두 번째 `siteadminsearchpanel`를 만들 때는 양식 충돌을 방지하기 위해 `id` 속성을 설정해야 합니다.

## 사용자 정의 설명 만들기 {#creating-custom-predicates}

[!DNL Assets] 에셋 공유 페이지를 사용자 지정하는 데 사용할 수 있는 사전 정의된 예측 세트가 포함되어 있습니다. 이렇게 자산 공유 사용자 지정은 자산 공유 페이지 [를 만들고 구성하는 데 포함됩니다](/help/assets/assets-finder-editor.md#creating-and-configuring-an-asset-share-page).

개발자는 기존 예측자를 사용하는 것 외에도 [!DNL Experience Manager] 쿼리 빌더 API를 사용하여 [고유한 설명](/help/sites-developing/querybuilder-api.md)을 만들 수 있습니다.

사용자 정의 설명을 만들려면 [Widgets 프레임워크에 대한 기본적인 지식이 필요합니다](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html).

가장 좋은 방법은 기존 술어를 복사하고 조정하는 것입니다. 샘플 예측자는 /libs/cq/search/components/ **예측자에 있습니다**.

### 예: 간단한 속성 설명 만들기 {#example-build-a-simple-property-predicate}

속성 조건자를 빌드하려면

1. 프로젝트 디렉토리에 구성 요소 폴더를 만듭니다(예: **/apps/geometrixx/components/title설명**).
1. content.xml **추가**:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Title Predicate"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Search"/>
   ```

1. 페이지 URL에 `titlepredicate.jsp`.

   ```java
   <%--
   
     Sample title predicate component
   
   --%><%@ page import="java.util.Calendar" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       // A unique id is necessary in case this predicate is inserted multiple times on the same page
       String elemId = "cq-predicate-" +  Long.toString(Calendar.getInstance().getTimeInMillis());
   
   %><div class="predicatebox">
   
       <div class="title">Title</div>
   
       <%-- The wrapper for the form elements. All items will be append to this wrapper. --%>
       <div id="<%= elemId %>" class="content"></div>
   
   </div><script type="text/javascript">
   
       CQ.Ext.onLoad(function() {
   
           var predicateName = "property";
           var propertyName = "jcr:content/metadata/dc:title";
           var elemId = "<%= elemId %>";
   
           // Get the page wide available QueryBuilder.
           var qb = CQ.search.Util.getQueryBuilder();
   
           // createId adds a counter to the predicate name - useful in case this predicate
           // is inserted multiple times on the same page.
           var id = qb.createId(predicateName);
   
           // Hidden field that defines the property to search for; in our case this
           // is the "dc:title" metadata. The name "property" (or "1_property", "2_property" etc.)
           // indicates the server to use the property predicate
           // (com.day.cq.search.eval.JcrPropertyPredicateEvaluator).
           qb.addField({
               "xtype": "hidden",
               "renderTo": elemId,
               "name": id,
               "value": propertyName
           });
   
           // The visible text field. The name has to be like the one of the hidden field above
           // plus the ".value" suffix.
           qb.addField({
               "xtype": "textfield",
               "renderTo": elemId,
               "name": id + ".value"
           });
   
           // Depending on the predicate additional parameters allow to configure the
           // predicate. Here we add an operation parameter to create a "like" query.
           // Again note the name set to the id and a suffix.
           qb.addField({
               "xtype": "hidden",
               "renderTo": elemId,
               "name": id + ".operation",
               "value": "like"
           });
       });
   </script>
   ```

1. 구성 요소를 사용할 수 있게 하려면 구성 요소를 편집할 수 있어야 합니다. 구성 요소를 편집 가능하게 만들려면 CRXDE에서 기본 유형의 **cq:editConfig** 노드를 **추가합니다**. 단락을 제거할 수 있도록 단일 값 **의 DELETE으로 다중 값 속성 cq:액션** 을 추가할 수 **있습니다**.
1. 브라우저로 이동하고 샘플 페이지(예: **press.html**)에서 디자인 모드로 전환하고 설명 단락 시스템(예: **왼쪽)에 대한 새 구성 요소를 활성화합니다**.

1. 이제 **편집** 모드에서 새 구성 요소를 사이드 킥에서 사용할 수 있습니다( **검색** 그룹에 있음). 설명 열에 구성 요소 **를** 삽입하고 검색 단어(예: **다이아몬드** )를 입력하고 확대경을 클릭하여 검색을 시작합니다.

   >[!NOTE]
   >
   >검색할 때는 올바른 경우를 포함하여 정확하게 용어를 입력해야 합니다.

### 예: 단순 그룹 설명 작성 {#example-build-a-simple-group-predicate}

그룹 조건자를 빌드하려면 다음을 수행하십시오.

1. 프로젝트 디렉토리에서 구성 요소 폴더(예: **/apps/geometrixx/components/picspredicate)를 만듭니다.**
1. content.xml **추가**:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Image Formats"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Search"/>
   ```

1. title **조건자.jsp 추가**:

   ```java
   <%--
   
     Sample group predicate component
   
   --%><%@ page import="java.util.Calendar" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       // A unique id is necessary in case this predicate is inserted multiple times on the same page.
       String elemId = "cq-predicate-" +  Long.toString(Calendar.getInstance().getTimeInMillis());
   
   %><div class="predicatebox">
   
       <div class="title">Image Formats</div>
   
       <%-- The wrapper for the form elements. All items will be append to this wrapper. --%>
       <div id="<%= elemId %>" class="content"></div>
   
   </div><script type="text/javascript">
   
       CQ.Ext.onLoad(function() {
   
           var predicateName = "property";
           var propertyName = "jcr:content/metadata/dc:format";
           var elemId = "<%= elemId %>";
   
           // Get the page wide available QueryBuilder.
           var qb = CQ.search.Util.getQueryBuilder();
   
           // Create a unique group ID; will return e.g. "1_group".
           var groupId = qb.createGroupId();
   
           // Hidden field that defines the property to search for  - in our case "dc:format" -
           // and declares the group of predicates. "property" in the name ("1_group.property")
           // indicates to the server to use the "property predicate"
           // (com.day.cq.search.eval.JcrPropertyPredicateEvaluator).
           qb.addField({
               "xtype": "hidden",
               "renderTo": "<%= elemId %>",
               "name": groupId + "." + predicateName, // 1_group.property
               "value": propertyName
           });
   
           // Declare to combine the multiple values using OR.
           qb.add(new CQ.Ext.form.Hidden({
               "name": groupId + ".p.or",  // 1_group.p.or
               "value": "true"
           }));
   
           // The options
           var options = [
               { "label":"JPEG", "value":"image/jpeg"},
               { "label":"PNG",  "value":"image/png" },
               { "label":"GIF",  "value":"image/gif" }
           ];
   
           // Build a checkbox for each option.
           for (var i = 0; i < options.length; i++) {
               qb.addField({
                   "xtype": "checkbox",
                   "renderTo": "<%= elemId %>",
                   // 1_group.property.0_value, 1_group.property.1_value etc.
                   "name": groupId + "." +  predicateName + "." + i + "_value",
                   "inputValue": options[i].value,
                   "boxLabel": options[i].label,
                   "listeners": {
                       "check": function() {
                           // Submit the search form when checking/unchecking a checkbox.
                           qb.submit();
                       }
                   }
               });
           }
       });
   ```

1. 구성 요소를 사용할 수 있게 하려면 구성 요소를 편집할 수 있어야 합니다. 구성 요소를 편집 가능하게 만들려면 CRXDE에서 기본 유형의 **cq:editConfig** 노드를 **추가합니다**. 단락을 제거할 수 있도록 단일 값 **의 DELETE으로 다중 값 속성 cq:액션** 을 추가할 수 **있습니다**.
1. 브라우저로 이동하고 샘플 페이지(예: **press.html**)에서 디자인 모드로 전환하고 설명 단락 시스템(예: **왼쪽)에 대한 새 구성 요소를 활성화합니다**.
1. 이제 **편집** 모드에서 새 구성 요소를 사이드 킥에서 사용할 수 있습니다( **검색** 그룹에 있음). 설명 열에 구성 요소를 **삽입합니다** .

## 설치된 설명 위젯 {#installed-predicate-widgets}

다음 예제는 미리 구성된 ExtJS 위젯으로 사용할 수 있습니다.

### 전체 텍스트 설명 {#fulltextpredicate}

| 속성 | 유형 | 설명 |
|---|---|---|
| 조건자 이름 | 문자열 | 술어의 이름입니다. 기본값은 입니다.`fulltext` |
| searchCallback | 함수 | 이벤트 시 검색을 트리거하기 위한 콜백입니다 `keyup`. 기본값은 입니다.`CQ.wcm.SiteAdmin.doSearch` |

### 속성 설명 {#propertypredicate}

| 속성 | 유형 | 설명 |
|---|---|---|
| 조건자 이름 | 문자열 | 술어의 이름입니다. 기본값은 입니다.`property` |
| propertyName | 문자열 | JCR 속성의 이름입니다. 기본값은 입니다.`jcr:title` |
| defaultValue | 문자열 | 사전 채워진 기본값. |

### 경로 설명 {#pathpredicate}

| 속성 | 유형 | 설명 |
|---|---|---|
| 조건자 이름 | 문자열 | 술어의 이름입니다. 기본값은 입니다.`path` |
| rootPath | 문자열 | 술어의 루트 경로입니다. 기본값은 입니다.`/content/dam` |
| pathFieldPredictiveName | 문자열 | 기본값은 입니다.`folder` |
| showFlatOption | 부울 | 확인란을 표시하는 플래그 `search in subfolders`. 기본값은 true입니다. |

### 날짜 설명 {#datepredicate}

| 속성 | 유형 | 설명 |
|---|---|---|
| 조건자 이름 | 문자열 | 술어의 이름입니다. 기본값은 입니다.`daterange` |
| propertyname | 문자열 | JCR 속성의 이름입니다. 기본값은 입니다.`jcr:content/jcr:lastModified` |
| defaultValue | 문자열 | 미리 채워진 기본값 |

### 옵션설명 {#optionspredicate}

| 속성 | 유형 | 설명 |
|---|---|---|
| 제목 | 문자열 | 추가 상위 제목 추가 |
| 조건자 이름 | 문자열 | 술어의 이름입니다. 기본값은 입니다.`daterange` |
| propertyname | 문자열 | JCR 속성의 이름입니다. 기본값은 입니다.`jcr:content/metadata/cq:tags` |
| 축소 | 문자열 | 축소 수준. 기본값은 입니다.`level1` |
| triggerSearch | 부울 | 확인 시 검색을 트리거하는 플래그. 기본값은 false입니다. |
| searchCallback | 함수 | 검색을 트리거하는 콜백입니다. 기본값은 입니다.`CQ.wcm.SiteAdmin.doSearch` |
| searchTimeoutTime | 번호 | searchCallback이 실행되기 전에 시간이 초과되었습니다. 기본값은 800ms입니다. |

## 검색 결과 사용자 정의 {#customizing-search-results}

자산 공유 페이지의 검색 결과 프레젠테이션은 선택한 렌즈에 의해 제어됩니다. [!DNL Experience Manager Assets] 에는 자산 공유 페이지를 사용자 지정하는 데 사용할 수 있는 미리 정의된 렌즈 세트가 포함되어 있습니다. 이렇게 자산 공유 사용자 지정은 자산 공유 페이지 [만들기 및 구성에서 다룹니다](/help/assets/assets-finder-editor.md#creating-and-configuring-an-asset-share-page).

기존 렌즈를 사용하는 것 외에도, [!DNL Experience Manager] 개발자들은 자신들의 렌즈를 만들 수 있습니다.
