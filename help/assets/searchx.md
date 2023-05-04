---
title: 검색 기능 확장
description: 검색 기능 확장 [!DNL Adobe Experience Manager Assets] 기본값 초과.
contentOwner: AG
role: Developer
feature: Search
exl-id: 9e33d1c0-232b-458a-ad6a-f595aa541a5a
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 19%

---

# 자산 검색 확장 {#extending-assets-search}

확장 가능 [!DNL Adobe Experience Manager Assets] 검색 기능. 즉시 [!DNL Experience Manager Assets] 문자열로 자산을 검색합니다.

검색은 QueryBuilder 인터페이스를 통해 수행되므로 몇 가지 조건자로 검색을 사용자 지정할 수 있습니다. 다음 디렉토리에 기본 설명 세트를 오버레이할 수 있습니다. `/apps/dam/content/search/searchpanel/facets`.

또한 [!DNL Assets] 관리 패널.

>[!CAUTION]
>
>기준 [!DNL Experience Manager] 6.4, 클래식 UI는 더 이상 사용되지 않습니다. Adobe은 터치 지원 UI를 사용하는 것을 권장합니다. 사용자 지정에 대해서는 다음을 참조하십시오 [검색 패싯](/help/assets/search-facets.md).

## 오버레이 {#overlaying}

사전 구성된 조건자를 오버레이하려면 `facets` 노드 `/libs/dam/content/search/searchpanel` to `/apps/dam/content/search/searchpanel/` 또는 다른 `facetURL` 속성( `searchpanel` 구성(기본값은 임) `/libs/dam/content/search/searchpanel/facets.overlay.infinity.json`).

![screen_shot_2012-06-05at113619am](assets/screen_shot_2012-06-05at113619am.png)

>[!NOTE]
>
>기본적으로 아래의 디렉토리 구조는 다음과 같습니다 `/apps` 존재하지 않으므로 만듭니다. 노드 유형이 `/libs`.

## 탭 추가 {#adding-tabs}

에서 검색 탭을 구성하여 검색 탭을 추가할 수 있습니다 [!DNL Assets] 관리 인터페이스. 추가 탭을 만들려면 다음을 수행하십시오.

1. 폴더 구조 만들기 `/apps/wcm/core/content/damadmin/tabs,`아직 존재하지 않는 경우 를 복사하여 `tabs` 노드 `/libs/wcm/core/content/damadmin` 붙여넣어
1. 원하는 대로 두 번째 탭을 만들고 구성합니다.

   >[!NOTE]
   >
   >두 번째 `siteadminsearchpanel`를 설정하는 경우 `id` 양식 충돌을 방지하기 위한 속성입니다.

## 사용자 지정 설명 만들기 {#creating-custom-predicates}

[!DNL Assets] 은 자산 공유 페이지를 사용자 지정하는 데 사용할 수 있는 사전 정의된 설명 세트와 함께 제공됩니다. 이러한 방식으로 자산 공유 사용자 지정은 [자산 공유 페이지 만들기 및 구성](/help/assets/assets-finder-editor.md#creating-and-configuring-an-asset-share-page).

기존 설명을 사용하는 것 외에도 [!DNL Experience Manager] 개발자는 을 사용하여 자체 설명을 만들 수도 있습니다 [Query Builder API](/help/sites-developing/querybuilder-api.md).

사용자 지정 설명을 만들려면 [위젯 프레임워크](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html).

가장 좋은 방법은 기존 설명을 복사하고 조정하는 것입니다. 샘플 조건자는 **/libs/cq/search/components/predicate**.

### 예: 단순 속성 설명 작성 {#example-build-a-simple-property-predicate}

속성 설명을 빌드하려면 다음을 수행하십시오.

1. 프로젝트 디렉토리에서 구성 요소 폴더를 만듭니다(예: ) **/apps/weretail/components/titledec**.
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
1. 브라우저 및 샘플 페이지로 이동합니다(예: **press.html**) 디자인 모드로 전환하고 설명 단락 시스템의 새 구성 요소를 활성화합니다(예: **왼쪽**).

1. in **편집** 모드에서는 이제 사이드 킥에서 새 구성 요소를 사용할 수 있습니다( **검색** 그룹)에 속해 있어야 합니다. 구성 요소를 **설명** 열 및 검색어 입력(예: **다이아몬드** 확대경을 클릭하여 검색을 시작합니다.

   >[!NOTE]
   >
   >검색할 때 올바른 대/소문자를 포함하여 정확히 단어를 입력해야 합니다.

### 예: 단순 그룹 설명 작성 {#example-build-a-simple-group-predicate}

그룹 설명을 작성하려면 다음을 수행하십시오.

1. 프로젝트 디렉토리에서 구성 요소 폴더를 만듭니다(예: ) **/apps/weretail/components/picspredicate**.
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

1. 추가 **titledec.jsp**:

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

1. To make the component available, you need to be able to edit it. To make a component editable, in CRXDE, add a node **cq:editConfig** of primary type **cq:EditConfig**. So that you can remove paragraphs, add a multi-value property **cq:actions** with a single value of **DELETE**.
1. 브라우저 및 샘플 페이지로 이동합니다(예: **press.html**) 디자인 모드로 전환하고 설명 단락 시스템의 새 구성 요소를 활성화합니다(예: **왼쪽**).
1. in **편집** 모드에서는 이제 사이드 킥에서 새 구성 요소를 사용할 수 있습니다( **검색** 그룹)에 속해 있어야 합니다. 구성 요소를 **설명** 열.

## 설치된 설명 위젯 {#installed-predicate-widgets}

다음 설명은 사전 구성된 ExtJS 위젯으로 사용할 수 있습니다.

### 전체 텍스트 설명 {#fulltextpredicate}

| 속성 | 유형 | 설명 |
|---|---|---|
| predicateName | 문자열 | 조건자의 이름입니다. 기본값은 입니다.`fulltext` |
| searchCallback | 함수 | 이벤트에서 검색을 트리거하기 위한 콜백 `keyup`. 기본값은 입니다.`CQ.wcm.SiteAdmin.doSearch` |

### PropertyPredicate {#propertypredicate}

| 속성 | 유형 | 설명 |
|---|---|---|
| predicateName | 문자열 | 조건자의 이름입니다. 기본값은 입니다.`property` |
| propertyName | 문자열 | JCR 속성의 이름입니다. 기본값은 입니다.`jcr:title` |
| defaultValue | 문자열 | 미리 채워진 기본값. |

### 경로 설명 {#pathpredicate}

| 속성 | 유형 | 설명 |
|---|---|---|
| predicateName | 문자열 | 조건자의 이름입니다. 기본값은 입니다.`path` |
| rootPath | 문자열 | 조건부의 루트 경로입니다. 기본값은 입니다.`/content/dam` |
| pathFieldPredicateName | 문자열 | 기본값은 입니다.`folder` |
| showFlatOption | 부울 | 확인란을 표시할 플래그 `search in subfolders`. 기본값은 true입니다. |

### DatePredicate {#datepredicate}

| 속성 | 유형 | 설명 |
|---|---|---|
| predicateName | 문자열 | 조건자의 이름입니다. 기본값은 입니다.`daterange` |
| propertyname | 문자열 | JCR 속성의 이름입니다. 기본값은 입니다.`jcr:content/jcr:lastModified` |
| defaultValue | 문자열 | 미리 채워진 기본값 |

### OptionsPredicate {#optionspredicate}

| 속성 | 유형 | 설명 |
|---|---|---|
| 제목 | 문자열 | 추가 상위 제목 추가 |
| predicateName | 문자열 | 조건자의 이름입니다. 기본값은 입니다.`daterange` |
| propertyname | 문자열 | JCR 속성의 이름입니다. 기본값은 입니다.`jcr:content/metadata/cq:tags` |
| 축소 | 문자열 | 수준을 축소합니다. 기본값은 입니다.`level1` |
| triggerSearch | 부울 | 확인 시 검색을 트리거하기 위한 플래그입니다. 기본값은 false입니다. |
| searchCallback | 함수 | 검색을 트리거하기 위한 콜백입니다. 기본값은 입니다.`CQ.wcm.SiteAdmin.doSearch` |
| searchTimeoutTime | 숫자 | searchCallback이 실행되기 전의 시간 제한. 기본값은 800ms입니다. |

## 검색 결과 사용자 지정 {#customizing-search-results}

자산 공유 페이지의 검색 결과 프레젠테이션은 선택한 렌즈가 제어합니다. [!DNL Experience Manager Assets] 에는 자산 공유 페이지를 사용자 지정하는 데 사용할 수 있는 사전 정의된 렌즈 세트가 포함되어 있습니다. 이러한 방식으로 자산 공유 사용자 지정은 [자산 공유 페이지 만들기 및 구성](/help/assets/assets-finder-editor.md#creating-and-configuring-an-asset-share-page).

기존 렌즈를 사용하는 것 외에도 [!DNL Experience Manager] 개발자들이 자신만의 렌즈를 만들 수도 있다.
