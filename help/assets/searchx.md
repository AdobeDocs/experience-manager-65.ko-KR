---
title: 검색 기능 확장
description: 의 검색 기능 확장 [!DNL Adobe Experience Manager Assets] 기본값 이상.
contentOwner: AG
role: Developer
feature: Search
exl-id: 9e33d1c0-232b-458a-ad6a-f595aa541a5a
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 19%

---

# 에셋 검색 확장 {#extending-assets-search}

를 확장할 수 있습니다. [!DNL Adobe Experience Manager Assets] 검색 기능. 기본, [!DNL Experience Manager Assets] 문자열로 에셋을 검색합니다.

검색은 QueryBuilder 인터페이스를 통해 수행되므로 여러 술어로 검색을 사용자 지정할 수 있습니다. 다음 디렉터리에 기본 술어 세트를 오버레이할 수 있습니다. `/apps/dam/content/search/searchpanel/facets`.

에 탭을 더 추가할 수도 있습니다. [!DNL Assets] 관리 패널.

>[!CAUTION]
>
>기준: [!DNL Experience Manager] 6.4. 클래식 UI는 더 이상 사용되지 않습니다. Adobe 터치 지원 UI를 사용하는 것이 좋습니다. 사용자 지정에 대해서는 [검색 패싯](/help/assets/search-facets.md).

## 오버레이 {#overlaying}

사전 구성된 술어를 오버레이하려면 다음을 복사합니다. `facets` 노드: 부터 `/libs/dam/content/search/searchpanel` 끝 `/apps/dam/content/search/searchpanel/` 또는 다른 항목 지정 `facetURL` 의 속성 `searchpanel` 구성(기본값은 입니다.) `/libs/dam/content/search/searchpanel/facets.overlay.infinity.json`).

![screen_shot_2012-06-05at113619am](assets/screen_shot_2012-06-05at113619am.png)

>[!NOTE]
>
>기본적으로 디렉터리 구조는 `/apps` 이(가) 존재하지 않으므로 만드십시오. 노드 유형이 다음 노드 유형과 일치하는지 확인합니다. `/libs`.

## 탭 추가 {#adding-tabs}

에서 검색 탭을 구성하여 추가 검색 탭을 추가할 수 있습니다. [!DNL Assets] 관리 인터페이스. 추가 탭을 만들려면 다음 작업을 수행하십시오.

1. 폴더 구조 만들기 `/apps/wcm/core/content/damadmin/tabs,`아직 존재하지 않는 경우 `tabs` 노드: 부터 `/libs/wcm/core/content/damadmin` 붙여 넣으세요.
1. 원하는 대로 두 번째 탭을 만들고 구성합니다.

   >[!NOTE]
   >
   >두 번째 항목을 만들 때 `siteadminsearchpanel`, 다음을 설정하십시오. `id` 속성을 사용하여 양식 충돌을 방지합니다.

## 사용자 지정 술어 만들기 {#creating-custom-predicates}

[!DNL Assets] 에는 자산 공유 페이지를 사용자 지정하는 데 사용할 수 있는 사전 정의된 조건자 집합이 포함되어 있습니다. 이러한 방식으로 자산 공유 사용자 지정은에서 다룹니다 [자산 공유 페이지 만들기 및 구성](/help/assets/assets-finder-editor.md#creating-and-configuring-an-asset-share-page).

기존 술어를 사용하는 것 외에도 [!DNL Experience Manager] 개발자는 를 사용하여 고유한 술어를 만들 수도 있습니다. [Query Builder API](/help/sites-developing/querybuilder-api.md).

사용자 지정 술어를 만들려면 다음에 대한 기본 지식이 필요합니다. [위젯 프레임워크](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html).

가장 좋은 방법은 기존 술어를 복사하여 조정하는 것입니다. 샘플 조건자는에 있습니다. **/libs/cq/search/components/predicates**.

### 예: 간단한 속성 설명 작성 {#example-build-a-simple-property-predicate}

속성 술어를 작성하려면 다음을 수행합니다.

1. 프로젝트 디렉터리에 구성 요소 폴더 만들기(예: ) **/apps/weretail/components/titlepredicate**.
1. 추가 **content.xml**:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Title Predicate"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Search"/>
   ```

1. 추가 `titlepredicate.jsp`.

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

1. To make the component available, you need to be able to edit it. To make a component editable, in CRXDE, add a node **cq:editConfig** of primary type **cq:EditConfig**. So that you can remove paragraphs, add a multi-value property **cq:actions** with a single value of **DELETE**.
1. 브라우저로 이동한 다음 샘플 페이지에서 찾습니다(예: **press.html**) 디자인 모드로 전환하고 술어 단락 시스템에 대한 새 구성 요소를 활성화합니다(예: **left**).

1. 위치 **편집** 모드에서 새 구성 요소를 사이드 킥( **검색** group). 에 구성 요소 삽입 **술어** 열 및 검색어 입력(예: ) **다이아몬드** 그리고 돋보기를 클릭하여 검색을 시작합니다.

   >[!NOTE]
   >
   >검색할 때는 반드시 정확한 대/소문자를 포함하여 용어를 입력해야 합니다.

### 예: 간단한 그룹 설명 작성 {#example-build-a-simple-group-predicate}

그룹 설명을 작성하려면 다음을 수행합니다.

1. 프로젝트 디렉터리에 구성 요소 폴더 만들기(예: ) **/apps/weretail/components/picspredicate**.
1. 추가 **content.xml**:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Image Formats"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Search"/>
   ```

1. 추가 **titlepredicate.jsp**:

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
   
           // Create a unique group ID; will return for example, "1_group".
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

1. To make the component available, you need to be able to edit it. To make a component editable, in CRXDE, add a node **cq:editConfig** of primary type **cq:EditConfig**. So that you can remove paragraphs, add a multi-value property **cq:actions** with a single value of **DELETE**.
1. 브라우저로 이동한 다음 샘플 페이지에서 찾습니다(예: **press.html**) 디자인 모드로 전환하고 술어 단락 시스템에 대한 새 구성 요소를 활성화합니다(예: **left**).
1. 위치 **편집** 모드에서 새 구성 요소를 사이드 킥( **검색** group). 에 구성 요소 삽입 **술어** 열.

## 설치된 술어 위젯 {#installed-predicate-widgets}

다음 조건자는 사전 구성된 ExtJS 위젯으로 사용할 수 있습니다.

### 전체 텍스트 조건자 {#fulltextpredicate}

| 속성 | 유형 | 설명 |
|---|---|---|
| predicateName | 문자열 | 술어 이름. 기본값은 입니다.`fulltext` |
| searchCallback | 함수 | 이벤트에서 검색을 트리거하기 위한 콜백 `keyup`. 기본값은 입니다.`CQ.wcm.SiteAdmin.doSearch` |

### 속성 조건자 {#propertypredicate}

| 속성 | 유형 | 설명 |
|---|---|---|
| predicateName | 문자열 | 술어 이름. 기본값은 입니다.`property` |
| propertyName | 문자열 | JCR 속성의 이름입니다. 기본값은 입니다.`jcr:title` |
| defaultValue | 문자열 | 기본값이 미리 채워져 있습니다. |

### 경로 조건자 {#pathpredicate}

| 속성 | 유형 | 설명 |
|---|---|---|
| predicateName | 문자열 | 술어 이름. 기본값은 입니다.`path` |
| rootPath | 문자열 | 술어의 루트 경로. 기본값은 입니다.`/content/dam` |
| pathFieldPredicateName | 문자열 | 기본값은 입니다.`folder` |
| showFlatOption | 부울 | 확인란을 표시하는 플래그 `search in subfolders`. 기본값은 true입니다. |

### 날짜 조건자 {#datepredicate}

| 속성 | 유형 | 설명 |
|---|---|---|
| predicateName | 문자열 | 술어 이름. 기본값은 입니다.`daterange` |
| propertyname | 문자열 | JCR 속성의 이름입니다. 기본값은 입니다.`jcr:content/jcr:lastModified` |
| defaultValue | 문자열 | 미리 채워진 기본값 |

### 옵션 조건자 {#optionspredicate}

| 속성 | 유형 | 설명 |
|---|---|---|
| 제목 | 문자열 | 상단 제목 추가 |
| predicateName | 문자열 | 술어 이름. 기본값은 입니다.`daterange` |
| propertyname | 문자열 | JCR 속성의 이름입니다. 기본값은 입니다.`jcr:content/metadata/cq:tags` |
| 접기 | 문자열 | 수준을 접습니다. 기본값은 입니다.`level1` |
| triggerSearch | 부울 | 검사 시 검색을 트리거하기 위한 플래그입니다. 기본값은 false입니다. |
| searchCallback | 함수 | 검색을 트리거하기 위한 콜백입니다. 기본값은 입니다.`CQ.wcm.SiteAdmin.doSearch` |
| searchTimeoutTime | 숫자 | searchCallback이 실행되기 전에 시간이 초과되었습니다. 기본값은 800ms입니다. |

## 검색 결과 사용자 지정 {#customizing-search-results}

자산 공유 페이지에 대한 검색 결과 표시에는 선택한 렌즈가 적용됩니다. [!DNL Experience Manager Assets] 는 자산 공유 페이지를 사용자 지정하는 데 사용할 수 있는 사전 정의된 렌즈 세트와 함께 제공됩니다. 이러한 방식으로 자산 공유 사용자 지정은에서 다룹니다 [자산 공유 페이지 만들기 및 구성](/help/assets/assets-finder-editor.md#creating-and-configuring-an-asset-share-page).

기존 렌즈를 사용하는 것 외에도, [!DNL Experience Manager] 개발자는 자신만의 렌즈를 만들 수도 있습니다.
