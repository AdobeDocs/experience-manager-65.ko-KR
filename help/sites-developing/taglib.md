---
title: 태그 라이브러리
seo-title: 태그 라이브러리
description: Granite, CQ 및 Sling 태그 라이브러리를 통해 템플릿 및 구성 요소의 JSP 스크립트에서 사용할 특정 기능에 액세스할 수 있습니다
seo-description: Granite, CQ 및 Sling 태그 라이브러리를 통해 템플릿 및 구성 요소의 JSP 스크립트에서 사용할 특정 기능에 액세스할 수 있습니다
uuid: e622d47b-cfb3-4b4a-b8e3-e1adee294219
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 6678e3c3-fb0f-4300-8838-38f23f14db07
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '2487'
ht-degree: 1%

---


# 태그 라이브러리{#tag-libraries}

Granite, CQ 및 Sling 태그 라이브러리를 사용하면 템플릿 및 구성 요소의 JSP 스크립트에서 사용할 특정 기능에 액세스할 수 있습니다.

## Granite Tag Library {#granite-tag-library}

Granite 태그 라이브러리에는 유용한 함수가 포함되어 있습니다.

Granite UI 구성 요소의 jsp 스크립트를 개발할 때는 스크립트 맨 위에 다음 코드를 포함하는 것이 좋습니다.

```xml
<%@include file="/libs/granite/ui/global.jsp"%>
```

또한 글로벌 버전은 [Sling 라이브러리](/help/sites-developing/taglib.md#sling-tag-library)를 선언합니다.

```xml
<%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling" %>
```

### <ui:includeClientLib> {#ui-includeclientlib}

`<ui:includeClientLib>` 태그는 js, css 또는 테마 라이브러리일 수 있는 AEM html 클라이언트 라이브러리를 포함합니다. js 및 css와 같이 다양한 유형의 여러 포함을 위해 이 태그를 jsp에서 여러 번 사용해야 합니다. 이 태그는 ` [com.adobe.granite.ui.clientlibs.HtmlLibraryManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/ui/clientlibs/HtmlLibraryManager.html)` 서비스 인터페이스의 편의성 래퍼입니다.

여기에는 다음 속성이 있습니다.

**categories**  - 쉼표로 구분된 클라이언트 lib 카테고리 목록입니다. 지정된 범주에 대한 모든 Javascript 및 CSS 라이브러리가 포함됩니다. 테마 이름이 요청에서 추출됩니다.

해당:`com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeIncludes`

**theme**  - 쉼표로 구분된 클라이언트 라이브러리 카테고리 목록입니다. 지정된 범주에 대한 모든 테마 관련 라이브러리(CSS 및 JS 모두)가 포함됩니다. 테마 이름이 요청에서 추출됩니다.

해당:`com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeThemeInclude`

**js**  - 쉼표로 구분된 클라이언트 lib 카테고리 목록입니다. 지정된 범주에 대한 모든 Javascript 라이브러리가 포함됩니다.

해당:`com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeJsInclude`

**css**  - 쉼표로 구분된 클라이언트 lib 카테고리 목록입니다. 지정된 범주에 대한 모든 CSS 라이브러리가 포함됩니다.

해당:`com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeCssInclude`

**테마**  - 테마별 또는 테마되지 않은 라이브러리만 표시하는 플래그를 포함해야 합니다. 생략하면 두 세트가 모두 포함됩니다. 순수 JS 또는 CSS 포함에만 적용됩니다(카테고리 또는 테마 포함에는 적용되지 않음).

`<ui:includeClientLib>` 태그는 jsp에서 다음과 같이 사용할 수 있습니다.

```xml
<%-- all: js + theme (theme-js + css) --%>
<ui:includeClientLib categories="cq.wcm.edit" />

<%-- only js libs --%>
<ui:includeClientLib js="cq.collab.calendar, cq.security" />

<%-- theme only (theme-js + css) --%>
<ui:includeClientLib theme="cq.collab.calendar, cq.security" />

<%-- css only --%>
<ui:includeClientLib css="cq.collab.calendar, cq.security" />
```

## CQ 태그 라이브러리 {#cq-tag-library}

CQ 태그 라이브러리에는 유용한 함수가 포함되어 있습니다.

스크립트에서 CQ 태그 라이브러리를 사용하려면 스크립트가 다음 코드로 시작해야 합니다.

```xml
<%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %>
```

>[!NOTE]
>
>스크립트에 `/libs/foundation/global.jsp` 파일이 포함되어 있으면 taglib는 자동으로 선언됩니다.

AEM 구성 요소의 jsp 스크립트를 개발할 때는 스크립트 맨 위에 다음 코드를 포함하는 것이 좋습니다.

```xml
<%@include file="/libs/foundation/global.jsp"%>
```

sling, CQ 및 jstl taglibs를 선언하며 [ `<cq:defineObjects />`](#amp-lt-cq-defineobjects) 태그에 정의된 정기적으로 사용되는 스크립팅 개체를 표시합니다. 구성 요소의 jsp 코드를 단축하고 단순화합니다.

### <cq:text> {#cq-text}

`<cq:text>` 태그는 JSP에 구성 요소 텍스트를 출력하는 편의 태그입니다.

다음과 같은 선택적 속성이 있습니다.

**속성**  - 사용할 속성의 이름입니다. 이름은 현재 리소스를 기준으로 합니다.

**값**  - 출력에 사용할 값입니다. 이 속성이 있으면 속성 속성의 사용을 덮어씁니다.

**oldValue**  - 비교 출력에 사용할 값입니다. 이 속성이 있으면 속성 속성의 사용을 덮어씁니다.

**escapeXml**  - 결과 문자열의 문자  &lt;>, &amp;, &#39; 및 &quot;를 해당 문자 엔티티 코드로 변환할지 여부를 정의합니다. 기본값은 false입니다. 즉, 서식 지정(선택 사항) 다음에 이스케이프되는 것이 적용됩니다.

**format**  - 텍스트 서식을 지정하는 데 사용할 선택적 java.text.Format.

**차이**  없음 - diff 정보가 있는 경우에도 비교 출력 계산을 하지 않습니다.

**tagClass**  - 비어 있지 않은 출력을 둘러싸는 요소의 CSS 클래스 이름입니다. 비어 있으면 요소가 추가되지 않습니다.

**tagName**  - 비어 있지 않은 출력을 둘러싸는 요소의 이름입니다. 기본값은 DIV입니다.

**자리 표시자**  - 편집 모드에서 null 또는 빈 텍스트(즉, 자리 표시자)에 사용할 기본값입니다. 기본 확인은 선택적인 서식 지정 및 이스케이프 후에 수행됩니다. 즉, 출력 그대로 기록됩니다. 기본값은 다음과 같습니다.

`<div><span class="cq-text-placeholder">&para;</span></div>`

**기본값**  - null 또는 빈 텍스트에 사용할 기본값입니다. 기본 확인은 선택적인 서식 지정 및 이스케이프 처리된 후 수행됩니다. 즉, 출력 그대로 기록됩니다.

`<cq:text>` 태그를 JSP에서 사용하는 몇 가지 예:

```xml
<cq:text property="jcr:title" tagName="h2"/>
<cq:text property="jcr:description" tagName="p"/>

<cq:text value="<%= listItem.getTitle() %>" tagName="h4" placeholder="" />
<cq:text value="<%= listItem.getDescription() %>" tagName="p" placeholder=""/>

<cq:text property="jcr:title" value="<%= title %>" tagName="h3"/><%
    } else if (type.equals("link")) {
        %><cq:text property="jcr:title" value="<%= "\u00bb " + title %>" tagName="p" tagClass="link"/><%
    } else if (type.equals("extralarge")) {
        %><cq:text property="jcr:title" value="<%= title %>" tagName="h1"/><%
    } else {
        %><cq:text property="jcr:title" value="<%= title %>" tagName="h2"/><%

<cq:text property="jcr:description" placeholder="" tagName="small"/>

<cq:text property="tableData"
               escapeXml="false"
               placeholder="<img src=\"/libs/cq/ui/resources/0.gif\" class=\"cq-table-placeholder\" alt=\"\">"
    />

<cq:text property="text"/>

<cq:text property="image/jcr:description" placeholder="" tagName="small"/>
<cq:text property="text" tagClass="text"/>
```

### <cq:setContentBundle> {#cq-setcontentbundle}

`<cq:setContentBundle>` 태그는 i18n 현지화 컨텍스트를 만들고 `javax.servlet.jsp.jstl.fmt.localizationContext` 구성 변수에 저장합니다.

여기에는 다음 속성이 있습니다.

**언어**  - 리소스 번들을 검색할 로케일의 언어입니다.

**소스**  - 로케일을 가져올 소스입니다. 다음 값 중 하나로 설정할 수 있습니다.

* **정적**  - 로케일은  `language` 가능한 경우 속성에서, 그렇지 않은 경우 서버 기본 로케일에서 가져옵니다.

* **페이지**  - 로케일은 현재 페이지 또는 리소스의 언어(있는 경우)에서, 그렇지 않은 경우  `language` 속성(있는 경우)에서, 그렇지 않은 경우 서버 기본 로케일에서 가져옵니다.

* **요청**  - 로케일은 요청 로케일()에서  `request.getLocale()`가져옵니다.

* **자동**  - 로케일은  `language` 가능한 경우 속성에서, 그렇지 않은 경우 현재 페이지 또는 리소스의 언어로부터, 그렇지 않은 경우에는 요청에서 가져옵니다.

`source` 속성이 설정되지 않은 경우:

* `language` 특성이 설정된 경우 `source` 속성의 기본값은 &quot;`static`입니다.

* `language` 특성이 설정되지 않은 경우 `source` 속성의 기본값은 `auto`입니다.

&quot;content bundle&quot;은 표준 JSTL `<fmt:message>` 태그에서 간단하게 사용할 수 있습니다. 키별로 메시지를 조회하는 방법은 2배입니다.

1. 먼저 현재 렌더링된 기본 리소스의 JCR 속성이 번역용으로 검색됩니다. 이렇게 하면 이러한 값을 편집할 수 있는 간단한 구성 요소 대화 상자를 정의할 수 있습니다.
1. 노드에 키와 정확히 같은 속성이 포함되어 있지 않으면 sling 요청( `SlingHttpServletRequest.getResourceBundle(Locale)`)에서 리소스 번들을 로드하는 것이 폴백입니다. 이 번들의 언어 또는 로캘은 `<cq:setContentBundle>` 태그의 언어 및 소스 특성에 의해 정의됩니다.

`<cq:setContentBundle>` 태그는 jsp에서 다음과 같이 사용할 수 있습니다.

언어를 정의하는 페이지의 경우:

```xml
... %><cq:setContentBundle source="page"/><%  %>
<div class="error"><fmt:message key="Hello"/>
</div> ...
```

사용자 맞춤형 페이지의 경우:

```xml
... %><cq:setContentBundle scope="request"/><% %>
<div class="error"><fmt:message key="Hello"/>
</div> ...
```

### <cq:include> {#cq-include}

`<cq:include>` 태그는 현재 페이지에 리소스를 포함합니다.

여기에는 다음 속성이 있습니다.

**flush**

* 대상을 포함하기 전에 출력을 플러시할지 여부를 정의하는 부울 값입니다.

**경로**

* 현재 요청 처리에 포함할 리소스 개체의 경로입니다. 이 경로가 상대적이면 해당 스크립트가 지정된 리소스를 포함하는 현재 리소스의 경로에 추가됩니다. 경로와 resourceType 또는 스크립트를 지정해야 합니다.

**resourceType**

* 포함할 리소스의 리소스 유형입니다. 리소스 유형이 설정된 경우 경로는 리소스 객체의 정확한 경로여야 합니다.이 경우 경로에 매개 변수, 선택기 및 확장을 추가할 수 없습니다.
* 포함할 리소스가 리소스로 확인할 수 없는 경로 특성과 함께 지정된 경우, 태그는 경로로부터 합성 리소스 개체를 만들고 이 리소스 유형을 만들 수 있습니다.
* 경로와 resourceType 또는 스크립트를 지정해야 합니다.

**스크립트**

* 포함할 jsp 스크립트입니다. 경로와 resourceType 또는 스크립트를 지정해야 합니다.

**ignoreComponentHierarchy**

* 스크립트 해상도에 대해 구성 요소 계층을 무시할지 여부를 제어하는 부울 값입니다. true이면 검색 경로만 존중됩니다.

**예:**

```xml
<%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %><%
%><div class="center">
    <cq:include path="trail" resourceType="foundation/components/breadcrumb" />
    <cq:include path="title" resourceType="foundation/components/title" />
    <cq:include script="redirect.jsp"/>
    <cq:include path="par" resourceType="foundation/components/parsys" />
</div>
```

스크립트를 포함하려면 `<%@ include file="myScript.jsp" %>` 또는 `<cq:include script="myScript.jsp" %>`을 사용해야 합니까?

* `<%@ include file="myScript.jsp" %>` 지시문은 JSP 컴파일러에 전체 파일을 현재 파일에 포함하라는 메시지를 표시합니다. 포함된 파일의 내용이 원본 파일에 바로 붙여넣은 것처럼 표시됩니다.
* `<cq:include script="myScript.jsp">` 태그와 함께 파일은 런타임에 포함됩니다.

`<cq:include>` 또는 `<sling:include>`을 사용해야 합니까?

* AEM 구성 요소를 개발할 때 `<cq:include>`을 사용하는 것이 좋습니다.
* `<cq:include>` 스크립트 속성을 사용할 때 스크립트 파일을 이름으로 직접 포함할 수 있습니다. 이 작업은 구성 요소 및 리소스 유형 상속을 고려하며 선택기 및 확장 기능을 사용하여 Sling의 스크립트 해상도를 엄격하게 따르는 것보다 간단합니다.

### <cq:includeClientLib> {#cq-includeclientlib}

>[!CAUTION]
>
>`<cq:includeClientLib>` aem 5.6부터 사용되지 않습니다. 대신  [ `<ui:includeClientLib>`](/help/sites-developing/taglib.md#ui-includeclientlib) 사용해야 합니다.

`<cq:includeClientLib>` 태그는 js, css 또는 테마 라이브러리일 수 있는 AEM html 클라이언트 라이브러리를 포함합니다. js 및 css와 같이 다양한 유형의 여러 포함을 위해 이 태그를 jsp에서 여러 번 사용해야 합니다. 이 태그는 `com.day.cq.widget.HtmlLibraryManager` 서비스 인터페이스의 편의성 래퍼입니다.

여기에는 다음 속성이 있습니다.

**categories**  - 쉼표로 구분된 클라이언트 lib 카테고리 목록입니다. 지정된 범주에 대한 모든 Javascript 및 CSS 라이브러리가 포함됩니다. 테마 이름이 요청에서 추출됩니다.

해당:`com.day.cq.widget.HtmlLibraryManager#writeIncludes`

**theme**  - 쉼표로 구분된 클라이언트 라이브러리 카테고리 목록입니다. 지정된 범주에 대한 모든 테마 관련 라이브러리(CSS 및 JS 모두)가 포함됩니다. 테마 이름이 요청에서 추출됩니다.

해당:`com.day.cq.widget.HtmlLibraryManager#`writeThemeInclude

**js**  - 쉼표로 구분된 클라이언트 lib 카테고리 목록입니다. 지정된 범주에 대한 모든 Javascript 라이브러리가 포함됩니다.

해당:`com.day.cq.widget.HtmlLibraryManager#writeJsInclude`

**css**  - 쉼표로 구분된 클라이언트 lib 카테고리 목록입니다. 지정된 범주에 대한 모든 CSS 라이브러리가 포함됩니다.

해당:`com.day.cq.widget.HtmlLibraryManager#writeCssInclude`

**테마**  - 테마별 또는 테마되지 않은 라이브러리만 표시하는 플래그를 포함해야 합니다. 생략하면 두 세트가 모두 포함됩니다. 순수 JS 또는 CSS 포함에만 적용됩니다(카테고리 또는 테마 포함에는 적용되지 않음).

`<cq:includeClientLib>` 태그는 jsp에서 다음과 같이 사용할 수 있습니다.

```xml
<%-- all: js + theme (theme-js + css) --%>
<cq:includeClientLib categories="cq.wcm.edit" />

<%-- only js libs --%>
<cq:includeClientLib js="cq.collab.calendar, cq.security" />

<%-- theme only (theme-js + css) --%>
<cq:includeClientLib theme="cq.collab.calendar, cq.security" />

<%-- css only --%>
<cq:includeClientLib css="cq.collab.calendar, cq.security" />
```

### <cq:defineObjects> {#cq-defineobjects}

`<cq:defineObjects>` 태그는 개발자가 참조할 수 있는 정기적으로 사용되는 스크립팅 개체를 표시합니다. 또한 [ `<sling:defineObjects>`](#amp-lt-sling-defineobjects) 태그로 정의된 객체를 표시합니다.

**componentContext**

* 요청의 현재 구성 요소 컨텍스트 개체(com.day.cq.wcm.api.components.ComponentContext 인터페이스)입니다.

**구성 요소**

* 현재 리소스의 현재 AEM 구성 요소 개체(com.day.cq.wcm.api.components.Component 인터페이스)입니다.

**currentDesign**

* 현재 페이지의 현재 디자인 개체(com.day.cq.wcm.api.designer.Design 인터페이스)입니다.

**currentPage**

* 현재 AEM WCM 페이지 개체(com.day.cq.wcm.api.Page 인터페이스)를 참조하십시오.

**currentStyle**

* 현재 셀의 현재 스타일 객체(com.day.cq.wcm.api.designer.Style 인터페이스)입니다.

**디자이너**

* 디자인 정보에 액세스하는 데 사용되는 디자이너 개체(com.day.cq.wcm.api.designer.Designer 인터페이스)입니다.

**editContext**

* aem 구성 요소의 edit 컨텍스트 개체(com.day.cq.wcm.api.components.EditContext 인터페이스)입니다.

**pageManager**

* 페이지 수준 작업을 위한 페이지 관리자 개체(com.day.cq.wcm.api.PageManager 인터페이스)입니다.

**pageProperties**

* 현재 페이지의 페이지 속성 개체(org.apache.sling.api.resource.ValueMap)입니다.

**속성**

* 현재 리소스의 속성 객체(org.apache.sling.api.resource.ValueMap)입니다.

**resourceDesign**

* 리소스 페이지의 디자인 개체(com.day.cq.wcm.api.designer.Design 인터페이스)입니다.

**resourcePage**

* 리소스 페이지 개체(com.day.cq.wcm.api.Page 인터페이스)를 참조하십시오.
* 여기에는 다음 속성이 있습니다.

**requestName**

* sling에서 상속됨

**responseName**

* sling에서 상속됨

**resourceName**

* sling에서 상속됨

**nodeName**

* sling에서 상속됨

**logName**

* sling에서 상속됨

**resourceResolverName**

* sling에서 상속됨

**slingName**

* sling에서 상속됨

**componentContextName**

* wcm에 대해

**editContextName**

* wcm에 대해

**propertiesName**

* wcm에 대해

**pageManagerName**

* wcm에 대해

**currentPageName**

* wcm에 대해

**resourcePageName**

* wcm에 대해

**pagePropertiesName**

* wcm에 대해

**componentName**

* wcm에 대해

**designerName**

* wcm에 대해

**currentDesignName**

* wcm에 대해

**resourceDesignName**

* wcm에 대해

**currentStyleName**

* wcm에 대해

**예**

```xml
<%@page session="false" contentType="text/html; charset=utf-8" %><%
%><%@ page import="com.day.cq.wcm.api.WCMMode" %><%
%><%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %><%
%><cq:defineObjects/>
```

>[!NOTE]
>
>`/libs/foundation/global.jsp` 파일이 스크립트에 포함되어 있으면 `<cq:defineObjects />` 태그가 자동으로 포함됩니다.

### <cq:requestURL> {#cq-requesturl}

`<cq:requestURL>` 태그는 현재 요청 URL을 JspWriter에 씁니다. 두 태그 [ `<cq:addParam>`](#amp-lt-cq-addparam) 및 [ `<cq:removeParam>`](#amp-lt-cq-removeparam)는 이 태그의 본문 내에 사용하여 현재 요청 URL을 작성하고 작성을 완료하기 전에 수정할 수 있습니다.

다양한 매개 변수를 사용하여 현재 페이지에 대한 링크를 만들 수 있습니다. 예를 들어 요청을 변형할 수 있습니다.

`mypage.html?mode=view&query=something` 대상 `mypage.html?query=something`.

`addParam` 또는 `removeParam`을 사용하면 지정된 매개 변수의 발생만 변경되며 다른 모든 매개 변수는 영향을 받지 않습니다.

`<cq:requestURL>` 에 속성이 없습니다.

예:

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### <cq:addParam> {#cq-addparam}

`<cq:addParam>` 태그는 지정된 이름과 값을 포함하는 요청 매개 변수를 바깥쪽 [ `<cq:requestURL>`](#amp-lt-cq-requesturl) 태그에 추가합니다.

여기에는 다음 속성이 있습니다.

**이름**

* 추가할 매개 변수의 이름

**정렬 단추**

* 추가할 매개 변수의 값

**예:**

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### <cq:removeParam> {#cq-removeparam}

`<cq:removeParam>` 태그는 바깥쪽 [ `<cq:requestURL>`](#amp-lt-cq-requesturl) 태그에서 지정된 이름과 값을 갖는 요청 매개 변수를 제거합니다. 값을 제공하지 않으면 지정된 이름의 모든 매개 변수가 제거됩니다.

여기에는 다음 속성이 있습니다.

**이름**

* 제거할 매개 변수의 이름

예:

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

## Sling 태그 라이브러리 {#sling-tag-library}

Sling 태그 라이브러리에는 유용한 Sling 함수가 포함되어 있습니다.

스크립트에서 Sling 태그 라이브러리를 사용할 때 스크립트는 다음 코드로 시작해야 합니다.

```xml
<%@ taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %>
```

>[!NOTE]
>
>스크립트에 `/libs/foundation/global.jsp` 파일이 포함되어 있으면 sling taglib가 자동으로 선언됩니다.

### <sling:include> {#sling-include}

`<sling:include>` 태그는 현재 페이지에 리소스를 포함합니다.

여기에는 다음 속성이 있습니다.

**flush**

* 대상을 포함하기 전에 출력을 플러시할지 여부를 정의하는 부울 값입니다.

**리소스**

* 현재 요청 처리에 포함할 리소스 객체입니다. 리소스 또는 경로를 지정해야 합니다. 둘 다 지정되면 리소스가 우선합니다.

**경로**

* 현재 요청 처리에 포함할 리소스 개체의 경로입니다. 이 경로가 상대적이면 해당 스크립트가 지정된 리소스를 포함하는 현재 리소스의 경로에 추가됩니다. 리소스 또는 경로를 지정해야 합니다. 둘 다 지정되면 리소스가 우선합니다.

**resourceType**

* 포함할 리소스의 리소스 유형입니다. 리소스 유형이 설정된 경우 경로는 리소스 객체의 정확한 경로여야 합니다.이 경우 경로에 매개 변수, 선택기 및 확장을 추가할 수 없습니다.
* 포함할 리소스가 리소스로 확인할 수 없는 경로 특성과 함께 지정된 경우, 태그는 경로로부터 합성 리소스 개체를 만들고 이 리소스 유형을 만들 수 있습니다.

**replaceSelectors**

* 전달하면 선택기가 이 속성의 값으로 바뀝니다.

**addSelectors**

* 이 속성을 전달하면 이 속성의 값이 선택기에 추가됩니다.

**replaceSuffix**

* 전달하면 접미사가 이 속성의 값으로 바뀝니다.

>[!NOTE]
>
>`<sling:include>` 태그에 포함된 리소스 및 스크립트의 해상도는 일반적인 슬링 URL 해상도와 동일합니다. 기본적으로 선택기, 확장 등 현재 요청에서 포함된 스크립트도 사용됩니다. 태그 속성을 통해 수정할 수 있습니다.예를 들어 `replaceSelectors="foo.bar"`에서는 선택기를 덮어쓸 수 있습니다.

예:

```xml
<div class="item"><sling:include path="<%= pathtoinclude %>"/></div>
```

```xml
<sling:include resource="<%= par %>"/>
```

```xml
<sling:include addSelectors="spool"/>
```

```xml
<sling:include resource="<%= par %>" resourceType="<%= newType %>"/>
```

```xml
<sling:include resource="<%= par %>" resourceType="<%= newType %>"/>
```

```xml
<sling:include replaceSelectors="content" />
```

### <sling:defineObjects> {#sling-defineobjects}

`<sling:defineObjects>` 태그는 개발자가 참조할 수 있는 정기적으로 사용되는 스크립팅 개체를 표시합니다.

**slingRequest**

* HTTP 요청 헤더 정보에 대한 액세스를 제공하는 SlingHttpServletRequest 객체는 표준 HttpServletRequest를 확장하고 리소스, 경로 정보, 선택기 등과 같은 Sling 관련 항목에 대한 액세스를 제공합니다.

**slingResponse**

* SlingHttpServletResponse 객체를 사용하여 서버에서 만든 HTTP 응답에 대한 액세스를 제공합니다. 이 값은 현재 HttpServletResponse가 확장되는 HttpServletResponse와 동일합니다.**요청**
* 순수 HttpServletRequest인 표준 JSP 요청 객체입니다.**응답**
* 순수 HttpServletResponse인 표준 JSP 응답 객체입니다.

**resourceResolver**

* 현재 ResourceResolver 객체입니다. slingRequest.getResourceResolver()와 같습니다.

.**sling**

* 이 응답 내에 있는 다른 리소스의 응답을 포함하기 위해 주로 sling.include(&#39;/some/other/resource&#39;)를 스크립트에 대한 편의 메서드를 포함하는 SlingScriptHelper 객체입니다(예: 머리글 html 코드 조각)과 sling.getService(foo.bar.Service.class)를 포함하여 Sling에서 사용할 수 있는 OSGi 서비스(스크립팅 언어에 따라 클래스 표기법)를 검색합니다.

**리소스**

* 요청의 URL에 따라 처리할 현재 리소스 객체입니다. slingRequest.getResource()와 동일합니다.

**currentNode**

* 현재 리소스가 JCR 노드(일반적으로 Sling의 경우)를 가리키면 Node 객체에 직접 액세스할 수 있습니다. 그렇지 않으면 이 개체가 정의되지 않습니다.

**로그**

* 스크립트 내에서 Sling 로그 시스템에 기록할 수 있는 SLF4J Logger(예: log.info(&quot;내 스크립트 실행&quot;).

* 여기에는 다음 속성이 있습니다.

**requestName**

**responseName**

**nodeName**

l **ogName resourceResolverName**

**slingName**

**예:**

```xml
<%@page session="false" %><%
%><%@page import="com.day.cq.wcm.foundation.forms.ValidationHelper"%><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/>
```

## JSTL 태그 라이브러리 {#jstl-tag-library}

[JavaServer 페이지 표준 태그 라이브러리](https://www.oracle.com/technetwork/java/index-jsp-135995.html)에는 다양하고 유용한 표준 태그가 포함되어 있습니다. 코어, 형식 지정 및 함수 태그는 다음 조각에 표시된 대로 `/libs/foundation/global.jsp`에 의해 정의됩니다.

### /libs/foundation/global.jsp {#extract-of-libs-foundation-global-jsp} 추출

```xml
<%@taglib prefix="c" uri="https://java.sun.com/jsp/jstl/core" %>
<%@taglib prefix="fmt" uri="https://java.sun.com/jsp/jstl/fmt" %>
<%@taglib prefix="fn" uri="https://java.sun.com/jsp/jstl/functions" %>
```

앞에서 설명한 대로 `/libs/foundation/global.jsp` 파일을 가져온 후 `c`, `fmt` 및 `fn` 접두어를 사용하여 이러한 태그릿에 액세스할 수 있습니다. JSTL의 공식 문서는 [The Java EE 5 Tutorial - JavaServer Pages Standard Tag Library](https://docs.oracle.com/javaee/5/tutorial/doc/bnakc.html)에서 확인할 수 있습니다.
