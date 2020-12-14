---
title: 검색 기능 확장.
description: ' [!DNL Adobe Experience Manager Assets] 의 검색 기능을 기본값 이상으로 확장합니다.'
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 8%

---


# 자산 검색 확장 {#extending-assets-search}

[!DNL Adobe Experience Manager Assets] 검색 기능을 확장할 수 있습니다. 기본적으로 [!DNL Experience Manager Assets]은 문자열을 기준으로 자산을 검색합니다.

검색은 QueryBuilder 인터페이스를 통해 수행되므로 여러 예측자로 검색을 사용자 정의할 수 있습니다. 다음 디렉토리에 기본 예측 세트를 오버레이할 수 있습니다.`/apps/dam/content/search/searchpanel/facets`.

[!DNL Assets] 관리 패널에 탭을 더 추가할 수도 있습니다.

>[!CAUTION]
>
>[!DNL Experience Manager] 6.4부터 클래식 UI는 더 이상 사용되지 않습니다. 자세한 내용은 [사용되지 않음 및 제거된 기능](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/deprecated-removed-features.html)을 참조하십시오. Adobe에서는 터치 지원 UI를 사용하는 것이 좋습니다. 사용자 지정을 보려면 [검색 패싯](/help/assets/search-facets.md)을 참조하십시오.

## 오버레이 {#overlaying}

사전 구성된 조건자를 오버레이하려면 `facets` 노드를 `/libs/dam/content/search/searchpanel`에 복사하거나 `facetURL` 구성에서 다른 `/apps/dam/content/search/searchpanel/` 속성을 지정하십시오(기본값은 `searchpanel`에 해당).`/libs/dam/content/search/searchpanel/facets.overlay.infinity.json`

![screen_shot_2012-06-05at113619am](assets/screen_shot_2012-06-05at113619am.png)

>[!NOTE]
>
>기본적으로 `/apps` 아래의 디렉토리 구조가 없으므로 만듭니다. 노드 유형이 `/libs` 아래의 유형과 일치하는지 확인합니다.

## 탭 {#adding-tabs} 추가

[!DNL Assets] 관리 인터페이스에서 검색 탭을 구성하여 추가 검색 탭을 추가할 수 있습니다. 추가 탭을 만들려면:

1. 폴더 구조 `/apps/wcm/core/content/damadmin/tabs,`이(가) 없는 경우 폴더 구조를 만들고 `/libs/wcm/core/content/damadmin`에서 `tabs` 노드를 복사하여 붙여넣습니다.
1. 원하는 대로 두 번째 탭을 만들고 구성합니다.

   >[!NOTE]
   >
   >두 번째 `siteadminsearchpanel`을 만들 때는 양식 충돌을 방지하기 위해 `id` 속성을 설정해야 합니다.

## 사용자 정의 설명 만들기 {#creating-custom-predicates}

[!DNL Assets] 에셋 공유 페이지를 사용자 지정하는 데 사용할 수 있는 미리 정의된 설명 세트가 포함되어 있습니다. 이러한 방식으로 자산 공유 사용자 지정은 [자산 공유 페이지 만들기 및 구성에서 다룹니다](/help/assets/assets-finder-editor.md#creating-and-configuring-an-asset-share-page).

기존 예측자를 사용하는 것 외에도 [!DNL Experience Manager] 개발자는 [Query Builder API](/help/sites-developing/querybuilder-api.md)를 사용하여 자체 설명을 만들 수 있습니다.

사용자 정의 설명을 만들려면 [위젯 프레임워크](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html)에 대한 기본적인 지식이 필요합니다.

가장 좋은 방법은 기존 조건자를 복사하고 조정하는 것입니다. 샘플 예측자는 **/libs/cq/search/components/predicates**&#x200B;에 있습니다.

### 예:단순 속성 설명 {#example-build-a-simple-property-predicate} 만들기

속성 조건자를 작성하려면 다음을 수행하십시오.

1. 프로젝트 디렉토리에 구성 요소 폴더를 만듭니다(예: **/apps/geometrixx/components/title설명**).
1. **content.xml** 추가:

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

1. 구성 요소를 사용할 수 있게 하려면 해당 구성 요소를 편집할 수 있어야 합니다. 구성 요소를 편집 가능하도록 하려면 CRXDE에서 기본 유형 **cq:EditConfig**&lt;a1/> 노드를 추가합니다.**** 단락을 제거할 수 있도록 단일 값 **DELETE**&#x200B;으로 다중 값 속성 **cq:actions**&#x200B;을 추가합니다.
1. 브라우저로 이동하고 샘플 페이지(예: **press.html**)에서 디자인 모드로 전환하고 설명 단락 시스템에 대한 새 구성 요소를 활성화합니다(예: **left**).

1. **편집** 모드에서 이제 새 구성 요소를 사이드킥에서 사용할 수 있습니다(**검색** 그룹에 있음). **예측** 열에 구성 요소를 삽입하고 **다이아몬드**&#x200B;와 같이 검색 단어를 입력하고 확대경을 클릭하여 검색을 시작합니다.

   >[!NOTE]
   >
   >검색할 때는 올바른 대소문자를 포함하여 정확하게 용어를 입력해야 합니다.

### 예:단순 그룹 설명 {#example-build-a-simple-group-predicate} 만들기

그룹 조건자를 작성하려면 다음을 수행하십시오.

1. 프로젝트 디렉토리에 구성 요소 폴더를 만듭니다(예: **/apps/geometrixx/components/picspredicate).**
1. **content.xml** 추가:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Image Formats"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Search"/>
   ```

1. **titledepredicate.jsp** 추가:

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

1. 구성 요소를 사용할 수 있게 하려면 해당 구성 요소를 편집할 수 있어야 합니다. 구성 요소를 편집 가능하도록 하려면 CRXDE에서 기본 유형 **cq:EditConfig**&lt;a1/> 노드를 추가합니다.**** 단락을 제거할 수 있도록 단일 값 **DELETE**&#x200B;으로 다중 값 속성 **cq:actions**&#x200B;을 추가합니다.
1. 브라우저로 이동하고 샘플 페이지(예: **press.html**)에서 디자인 모드로 전환하고 설명 단락 시스템에 대한 새 구성 요소를 활성화합니다(예: **left**).
1. **편집** 모드에서 이제 새 구성 요소를 사이드킥에서 사용할 수 있습니다(**검색** 그룹에 있음). **예측** 열에 구성 요소를 삽입합니다.

## 설치된 설명 위젯 {#installed-predicate-widgets}

다음 예측자는 사전 구성된 ExtJS 위젯으로 사용할 수 있습니다.

### 전체 텍스트 설명 {#fulltextpredicate}

| 속성 | 유형 | 설명 |
|---|---|---|
| predicateName | 문자열 | 조건자의 이름입니다. 기본값은 입니다.`fulltext` |
| searchCallback | 함수 | 이벤트 `keyup`에 대한 검색을 트리거하기 위한 콜백입니다. 기본값은 입니다.`CQ.wcm.SiteAdmin.doSearch` |

### 속성 설명 {#propertypredicate}

| 속성 | 유형 | 설명 |
|---|---|---|
| predicateName | 문자열 | 조건자의 이름입니다. 기본값은 입니다.`property` |
| propertyName | 문자열 | JCR 속성의 이름입니다. 기본값은 입니다.`jcr:title` |
| defaultValue | 문자열 | 사전 채워진 기본값. |

### 경로 설명 {#pathpredicate}

| 속성 | 유형 | 설명 |
|---|---|---|
| predicateName | 문자열 | 조건자의 이름입니다. 기본값은 입니다.`path` |
| rootPath | 문자열 | 조건자의 루트 경로입니다. 기본값은 입니다.`/content/dam` |
| pathFieldPredicateName | 문자열 | 기본값은 입니다.`folder` |
| showFlatOption | 부울 | 확인란 `search in subfolders`을(를) 표시하는 플래그. 기본값은 true입니다. |

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
| 축소 | 문자열 | 레벨을 축소합니다. 기본값은 입니다.`level1` |
| triggerSearch | 부울 | 확인 시 검색을 트리거하는 플래그. 기본값은 false입니다. |
| searchCallback | 함수 | 검색을 트리거하기 위한 콜백입니다. 기본값은 입니다.`CQ.wcm.SiteAdmin.doSearch` |
| searchTimeoutTime | 번호 | searchCallback이 실행되기 전에 시간이 초과되었습니다. 기본값은 800ms입니다. |

## 검색 결과 사용자 지정 {#customizing-search-results}

[자산 공유] 페이지의 검색 결과 프레젠테이션은 선택한 렌즈에 의해 제어됩니다. [!DNL Experience Manager Assets] 에셋 공유 페이지를 사용자 지정하는 데 사용할 수 있는 미리 정의된 렌즈 세트가 포함되어 있습니다. 이러한 방식으로 자산 공유 사용자 지정은 [자산 공유 페이지 만들기 및 구성에서 다룹니다](/help/assets/assets-finder-editor.md#creating-and-configuring-an-asset-share-page).

기존 렌즈를 사용하는 것 외에도 [!DNL Experience Manager] 개발자는 자체 렌즈를 만들 수도 있습니다.
