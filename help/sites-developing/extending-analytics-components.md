---
title: 구성 요소에 Adobe Analytics 추적 추가
seo-title: 구성 요소에 Adobe Analytics 추적 추가
description: 'null'
seo-description: 'null'
uuid: 447b140c-678c-428d-a1c9-ecbdec75cd42
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: a11c39b4-c23b-4207-8898-33aea25f2ad0
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835
workflow-type: tm+mt
source-wordcount: '1263'
ht-degree: 2%

---


# 구성 요소에 Adobe Analytics 추적 추가{#adding-adobe-analytics-tracking-to-components}

## 페이지 구성 요소 {#including-the-adobe-analytics-module-in-a-page-component}에 Adobe Analytics 모듈 포함

페이지 템플릿 구성 요소(예:`head.jsp, body.jsp`) ContextHub 및 Adobe Analytics 통합(Cloud Services의 일부인)을 로드하려면 JSP가 포함되어야 합니다. 모든 파일에는 로드 JavaScript 파일이 포함됩니다.

ContextHub 항목은 `<head>` 태그 바로 아래에 포함되어야 하지만 Cloud Services은 `<head>` 및 `</body>` 섹션 앞에 포함되어야 합니다.예를 들면 다음과 같습니다.

```xml
<head>
   <sling:include path="contexthub" resourceType="granite/contexthub/components/contexthub" />
...
   <cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
...
</head>
<body>
...
    <cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
</body>
```

`<head>` 요소 뒤에 삽입하는 `contexthub` 스크립트는 페이지에 ContextHub 기능을 추가합니다.

`<head>` 및 `<body>` 섹션에 추가하는 `cloudservices` 스크립트는 페이지에 추가된 클라우드 서비스 구성에 적용됩니다. 페이지가 두 개 이상의 Cloud Services 구성을 사용하는 경우 ContextHub jsp 및 Cloud Services jsp를 한 번만 포함해야 합니다.

페이지에 Adobe Analytics 프레임워크이 추가되면 `cloudservices` 스크립트는 Adobe Analytics 관련 javascript를 생성하고 다음 예제와 유사한 클라이언트측 라이브러리에 대한 참조를 생성합니다.

```xml
<div class="sitecatalyst cloudservice">
<script type="text/javascript" src="/etc/clientlibs/foundation/sitecatalyst/sitecatalyst.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/sitecatalyst/util.js"></script>
<script type="text/javascript" src="/content/geometrixx-outdoors/_jcr_content/analytics.sitecatalyst.js"></script>
<script type="text/javascript" src="/etc/clientlibs/mac/mac-sc.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/sitecatalyst/plugins.js"></script>
<script type="text/javascript">
<!--
CQ_Analytics.Sitecatalyst.frameworkComponents = ['foundation/components/page'];
/**
 * Sets Adobe Analytics variables accordingly to mapped components. If <code>options</code>
 * object is provided only variables matching the options.componentPath are set.
 *
 * @param {Object} options Parameter object from CQ_Analytics.record() call. Optional.
 */
CQ_Analytics.Sitecatalyst.updateEvars = function(options) {
    this.frameworkMappings = [];
 this.frameworkMappings.push({scVar:"pageName",cqVar:"pagedata.title",resourceType:"foundation/components/page"});
    for (var i=0; i<this.frameworkMappings.length; i++){
  var m = this.frameworkMappings[i];
  if (!options || options.compatibility || (options.componentPath == m.resourceType)) {
   CQ_Analytics.Sitecatalyst.setEvar(m);
  }
    }
}

CQ_Analytics.CCM.addListener("storesinitialize", function(e) {
 var collect = true;
    var lte = s.linkTrackEvents;
    s.pageName="content:geometrixx-outdoors:en";
    CQ_Analytics.Sitecatalyst.collect(collect);
    if (collect) {
  CQ_Analytics.Sitecatalyst.updateEvars();
     /************* DO NOT ALTER ANYTHING BELOW THIS LINE ! **************/
     var s_code=s.t();if(s_code)document.write(s_code);
     s.linkTrackEvents = lte;
     if(s.linkTrackVars.indexOf('events')==-1){delete s.events};
     $CQ(document).trigger("sitecatalystAfterCollect");
    }
});
//-->
</script>
<script type="text/javascript">
<!--
if(navigator.appVersion.indexOf('MSIE')>=0)document.write(unescape('%3C')+'\!-'+'-')
//-->
</script>
<noscript><img src="https://daydocumentation.112.2o7.net/b/ss/daydocumentation/1/H.25--NS/1380120772954?cdp=3&gn=content%3Ageometrixx-outdoors%3Aen" height="1" width="1" border="0" alt=""/></noscript>
<span data-tracking="{event:'pageView', values:{}, componentPath:'foundation/components/page'}"></span>
<div id="cq-analytics-texthint" style="background:white; padding:0 10px; display:none;">
 <h3 class="cq-texthint-placeholder">Component clientcontext is missing or misplaced.</h3>
</div>
<script type="text/javascript">
$CQ(function(){
 if( CQ_Analytics &&
  CQ_Analytics.ClientContextMgr &&
  !CQ_Analytics.ClientContextMgr.isConfigLoaded )
  {
   $CQ("#cq-analytics-texthint").show();
  }
});
</script>
</div>
```

Geometrixx Outdoors과 같은 모든 AEM 샘플 사이트에는 이 코드가 포함되어 있습니다.

### sitecatalystAfterCollect 이벤트 {#the-sitecatalystaftercollect-event}

`cloudservices` 스크립트는 `sitecatalystAfterCollect` 이벤트를 트리거합니다.

```
$CQ(document).trigger("sitecatalystAfterCollect");
```

이 이벤트는 페이지 추적이 완료되었음을 나타내는 트리거입니다. 이 페이지에서 추가 추적 작업을 수행하는 경우 문서 로드 또는 문서 준비 이벤트 대신 이 이벤트를 수신해야 합니다. `sitecatalystAfterCollect` 이벤트를 사용하면 충돌이나 다른 예측 불가능한 행동을 피할 수 있습니다.

>[!NOTE]
>
>`/libs/cq/analytics/clientlibs/sitecatalyst/sitecatalyst.js` 라이브러리에는 Adobe Analytics `s_code.js` 파일의 코드가 포함되어 있습니다.

## 사용자 지정 구성 요소에 대한 Adobe Analytics 추적 구현 {#implementing-adobe-analytics-tracking-for-custom-components}

AEM 구성 요소가 Adobe Analytics 프레임워크과 상호 작용할 수 있도록 합니다. 그런 다음 Adobe Analytics이 구성 요소 데이터를 추적하도록 프레임워크를 구성합니다.

Adobe Analytics 프레임워크과 상호 작용하는 구성 요소는 프레임워크를 편집할 때 SideKick에 나타납니다. 구성 요소를 프레임워크로 드래그하면 구성 요소 속성이 표시되고 이를 Adobe Analytics 속성에 매핑할 수 있습니다. ([기본 추적에 대한 프레임워크 설정](/help/sites-administering/adobeanalytics-connect.md#creating-a-adobe-analytics-framework)을 참조하십시오.)

구성 요소에 `analytics`이라는 하위 노드가 있으면 구성 요소는 Adobe Analytics 프레임워크과 상호 작용할 수 있습니다. `analytics` 노드에는 다음 속성이 있습니다.

* `cq:trackevents`:구성 요소에서 노출하는 CQ 이벤트를 식별합니다. 사용자 지정 이벤트를 참조하십시오.
* `cq:trackvars`:Adobe Analytics 속성과 매핑되는 CQ 변수의 이름을 지정합니다.
* `cq:componentName`:사이드 킥에 나타나는 구성 요소의 이름입니다.
* `cq:componentGroup`:구성 요소를 포함하는 사이드 킥의 그룹입니다.

구성 요소 JSP의 코드는 추적을 트리거하는 페이지에 javascript를 추가하고 추적되는 데이터를 정의합니다. javascript에 사용되는 이벤트 이름 및 데이터 이름은 `analytics` 노드 속성의 해당 값과 일치해야 합니다.

* 데이터 추적 속성을 사용하여 페이지가 로드될 때 이벤트 데이터를 추적합니다. ([페이지 로드 시 사용자 지정 이벤트 추적](/help/sites-developing/extending-analytics.md#tracking-custom-events-on-page-load)을 참조하십시오.)
* 사용자가 페이지 기능과 상호 작용할 때 이벤트 데이터를 추적하려면 CQ_Analytics.record 함수를 사용합니다. ([페이지 로드 후 사용자 지정 이벤트 추적](/help/sites-developing/extending-analytics.md#tracking-custom-events-after-page-load)을 참조하십시오.)

이러한 데이터 추적 방법을 사용하면 Adobe Analytics 통합 모듈은 자동으로 Adobe Analytics 호출을 수행하여 이벤트와 데이터를 기록합니다.

### 예:탐색 도구 클릭 {#example-tracking-topnav-clicks}

Adobe Analytics이 페이지 상단의 탐색 링크를 클릭하도록 기본 탐색 구성 요소를 확장합니다. 탐색 링크를 클릭하면 Adobe Analytics은 클릭한 링크 및 클릭한 페이지를 기록합니다.

다음 절차는 이미 다음 작업을 수행해야 합니다.

* CQ 응용 프로그램을 만들었습니다.
* Adobe Analytics 구성 및 Adobe Analytics 프레임워크을 만들었습니다.

#### topnav 구성 요소 {#copy-the-topnav-component} 복사

CQ 애플리케이션에 topnav 구성 요소를 복사합니다. 이 절차를 수행하려면 애플리케이션이 CRXDE Lite에 설정되어 있어야 합니다.

1. `/libs/foundation/components/topnav` 노드를 마우스 오른쪽 단추로 클릭하고 복사를 클릭합니다.
1. 응용 프로그램 폴더 아래의 구성 요소 폴더를 마우스 오른쪽 단추로 클릭하고 붙여넣기를 클릭합니다.
1. 모두 저장을 클릭합니다.

#### Adobe Analytics 프레임워크 {#integrating-topnav-with-the-adobe-analytics-framework}과(와) topnav 통합

topnav 구성 요소를 구성하고 JSP 파일을 편집하여 추적 이벤트 및 데이터를 정의합니다.

1. topnav 노드를 마우스 오른쪽 단추로 클릭하고 만들기 > 노드 만들기를 클릭합니다. 다음 속성 값을 지정하고 확인을 클릭합니다.

   * 이름: `analytics`
   * 유형: `nt:unstructured`

1. 추적 이벤트의 이름을 지정하려면 분석 노드에 다음 속성을 추가하십시오.

   * 이름:cq:trackevents
   * 유형:문자열
   * 값:topnavClick

1. 데이터 변수의 이름을 지정하려면 분석 노드에 다음 속성을 추가합니다.

   * 이름:cq:trackvars
   * 유형:문자열
   * 값:topnavTarget,topnavLocation

1. 사이드 킥에 대한 구성 요소의 이름을 지정하려면 분석 노드에 다음 속성을 추가합니다.

   * 이름:cq:componentName
   * 유형:문자열
   * 값:topnav(추적)

1. 사이드 킥에 대한 구성 요소 그룹 이름을 지정하려면 분석 노드에 다음 속성을 추가합니다.

   * 이름:cq:componentGroup
   * 유형:문자열
   * 값:일반

1. 모두 저장을 클릭합니다.
1. `topnav.jsp` 파일을 엽니다.
1. 요소에서 다음 속성을 추가합니다.

   ```xml
   onclick = "tracknav('<%= child.getPath() %>.html')"
   ```

1. 페이지 하단에서 다음 javascript 코드를 추가합니다.

   ```xml
   <script type="text/javascript">
       function tracknav(target) {
               if (CQ_Analytics.Sitecatalyst) {
                   CQ_Analytics.record({
                       event: 'topnavClick',
                       values: {
                           topnavTarget: target,
                           topnavLocation:'<%=currentPage.getPath() %>.html'
                       },
                       componentPath: '<%=resource.getResourceType()%>'
                   });
               }
       }
   </script>
   ```

1. 모두 저장을 클릭합니다.

`topnav.jsp` 파일의 내용은 다음과 같이 표시됩니다.

```xml
<%@page session="false"%><%--
  Copyright 1997-2008 Day Management AG
  Barfuesserplatz 6, 4001 Basel, Switzerland
  All Rights Reserved.

  This software is the confidential and proprietary information of
  Day Management AG, ("Confidential Information"). You shall not
  disclose such Confidential Information and shall use it only in
  accordance with the terms of the license agreement you entered into
  with Day.

  ==============================================================================

  Top Navigation component

  Draws the top navigation

--%><%@include file="/libs/foundation/global.jsp"%><%
%><%@ page import="java.util.Iterator,
        com.day.text.Text,
        com.day.cq.wcm.api.PageFilter,
        com.day.cq.wcm.api.Page,
        com.day.cq.commons.Doctype,
        org.apache.commons.lang3.StringEscapeUtils" %><%

    // get starting point of navigation
    long absParent = currentStyle.get("absParent", 2L);
    String navstart = Text.getAbsoluteParent(currentPage.getPath(), (int) absParent);

    //if not deep enough take current node
    if (navstart.equals("")) navstart=currentPage.getPath();

    Resource rootRes = slingRequest.getResourceResolver().getResource(navstart);
    Page rootPage = rootRes == null ? null : rootRes.adaptTo(Page.class);
    String xs = Doctype.isXHTML(request) ? "/" : "";
    if (rootPage != null) {
        Iterator<Page> children = rootPage.listChildren(new PageFilter(request));
        while (children.hasNext()) {
            Page child = children.next();
            %><a onclick = "tracknav('<%= child.getPath() %>.html')"  href="<%= child.getPath() %>.html"><%
            %><img alt="<%= StringEscapeUtils.escapeXml(child.getTitle()) %>" src="<%= child.getPath() %>.navimage.png"<%= xs %>></a><%
        }
    }
%><script type="text/javascript">
    function tracknav(target) {
            if (CQ_Analytics.Sitecatalyst) {
                CQ_Analytics.record({
                    event: 'topnavClick',
                    values: {
                        topnavTarget:target,
                        topnavLocation:'<%=currentPage.getPath() %>.html'
                    },
                    componentPath: '<%=resource.getResourceType()%>'
                });
            }
    }
</script>
```

>[!NOTE]
>
>ContextHub에서 데이터를 추적하는 것이 바람직합니다. javascript를 사용하여 이 정보를 얻는 방법에 대한 자세한 내용은 ContextHub[에서 값 액세스를 참조하십시오.](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub)

#### 사이드 킥에 추적 구성 요소 추가 {#adding-the-tracking-component-to-sidekick}

프레임워크에 추가할 수 있도록 Adobe Analytics에서 추적할 수 있는 구성 요소를 사이드 킥에 추가합니다.

1. Adobe Analytics 구성에서 Adobe Analytics 프레임워크을 엽니다. ([http://localhost:4502/etc/cloudservices/sitecatalyst.html](http://localhost:4502/etc/cloudservices/sitecatalyst.html))
1. 사이드 킥에서 디자인 단추를 클릭합니다.

   ![](assets/chlimage_1a.png)

1. 링크 추적 구성 영역에서 상속 구성을 클릭합니다.

   ![chlimage_1](assets/chlimage_1aa.png)

1. 허용된 구성 요소 목록에서 일반 섹션에서 탐색함(추적)을 선택한 다음 확인을 클릭합니다.
1. 사이드 킥을 확장하여 편집 모드로 전환합니다. 이제 일반 그룹에서 구성 요소를 사용할 수 있습니다.

#### 프레임워크 {#adding-the-topnav-component-to-your-framework}에 topnav 구성 요소 추가

topnav 구성 요소를 Adobe Analytics 프레임워크으로 드래그하고 구성 요소 변수와 이벤트를 Adobe Analytics 변수 및 이벤트에 매핑합니다. ([기본 추적에 대한 프레임워크 설정](/help/sites-administering/adobeanalytics-connect.md)을 참조하십시오.)

![chlimage_1-1](assets/chlimage_1-1a.png)

topnav 구성 요소는 이제 Adobe Analytics 프레임워크과 통합되었습니다. 구성 요소를 페이지에 추가할 때 상단 탐색 막대의 항목을 클릭하면 추적 데이터가 Adobe Analytics으로 전송됩니다.

### s.products 데이터를 Adobe Analytics {#sending-s-products-data-to-adobe-analytics}에 전송

구성 요소는 Adobe Analytics으로 전송된 s.products 변수에 대한 데이터를 생성할 수 있습니다. s.products 변수에 기여하도록 구성 요소를 디자인합니다.

* 특정 구조의 `product`이라는 값을 기록합니다.
* Adobe Analytics 프레임워크에서 Adobe Analytics 변수와 매핑할 수 있도록 `product` 값의 데이터 멤버를 노출합니다.

Adobe Analytics s.products 변수는 다음 구문을 사용합니다.

```
s.products="category;product;quantity;price;eventY={value}|eventZ={value};evarA={value}|evarB={value}"
```

Adobe Analytics 통합 모듈은 AEM 구성 요소가 생성하는 `product` 값을 사용하여 `s.products` 변수를 생성합니다. AEM 구성 요소가 생성하는 javascript의 `product` 값은 다음과 같은 구조를 가진 값의 배열입니다.

```
"product": [{
    "category": "",
    "sku"     : "path to product node",
    "quantity": quantity,
    "price"   : price,
    "events   : {
      "eventName1": "eventValue1",
      "eventName_n": "eventValue_n"
    }
    "evars"   : {
      "eVarName1": "eVarValue1",
      "eVarName_n": "eVarValue_n"
    }
}]
```

데이터 항목이 `product` 값에서 생략되면 s.products에서 빈 문자열로 전송됩니다.

>[!NOTE]
>
>제품 값과 연결된 이벤트가 없으면 기본적으로 Adobe Analytics에서는 `prodView` 이벤트를 사용합니다.

구성 요소의 `analytics` 노드는 `cq:trackvars` 속성을 사용하여 변수 이름을 노출해야 합니다.

* product.category
* product.sku
* product.quantity
* product.price
* product.events.eventName1
* product.events.eventName_n
* product.evars.eVarName1
* product.evars.eVarName_n

eCommerce 모듈은 s.products 변수 데이터를 생성하는 여러 구성 요소를 제공합니다. 예를 들어 제출 순서 구성 요소([http://localhost:4502/crx/de/index.jsp#/libs/commerce/components/submitorder/submitorder.jsp](http://localhost:4502/crx/de/index.jsp#/libs/commerce/components/submitorder/submitorder.jsp))는 다음 예와 유사한 javascript를 생성합니다.

```
<script type="text/javascript">
    function trackCartPurchase() {
        if (CQ_Analytics.Sitecatalyst) {
            CQ_Analytics.record({
                "event": ["productsCartPurchase"],
                "values": {
                    "product": [
                        {
                            "category": "",
                            "sku"     : "/path/to/prod/1",
                            "quantity": 3,
                            "price"   : 179.7,
                            "evars"   : {
                                "childSku": "/path/to/prod/1/green/xs",
                                "size"    : "XS"
                            }
                        },
                        {
                            "category": "",
                            "sku"     : "/path/to/prod/2",
                            "quantity": 10,
                            "price"   : 150,
                            "evars"   : {
                                "childSku": "/path/to/prod/2",
                                "size"    : ""
                            }
                        },
                        {
                            "category": "",
                            "sku"     : "/path/to/prod/3",
                            "quantity": 2,
                            "price"   : 102,
                            "evars"   : {
                                "childSku": "/path/to/prod/3/m",
                                "size"    : "M"
                            }
                        }
                    ]
                },
                "componentPath": "commerce/components/submitorder"
            });
            CQ_Analytics.record({
                "event": ["discountRedemption"],
                "values": {
                    "discount": "/path/to/discount/1 - /path/to/discount/2",
                    "product" : [{
                        "category": "",
                        "sku"     : "Promotional Discount",
                        "events"  : {"discountRedemption": 20.00}
                    }]
                },
                "componentPath": "commerce/components/submitorder"
            });
            CQ_Analytics.record({
                "event": ["cartPurchase"],
                "values": {
                    "orderId"       : "00e40e2d-13a2-4a00-a8ee-01a9ebb0bf68",
                    "shippingMethod": "overnight",
                    "paymentMethod" : "Amex",
                    "billingState"  : "NY",
                    "billingZip"    : "10458",
                    "product"       : [{"category": "", "sku": "", "quantity": "", "price": ""}]
                },
                "componentPath": "commerce/components/submitorder"
            });
        }
        return true;
    }
</script>
```

#### 추적 호출 크기 제한 {#limiting-the-size-of-tracking-calls}

일반적으로 웹 브라우저는 GET 요청의 크기를 제한합니다. CQ 제품 및 SKU 값은 저장소 경로이므로 여러 값을 포함하는 제품 배열은 요청 크기 제한을 초과할 수 있습니다. 따라서 구성 요소는 각 `CQ_Analytics.record function`의 `product` 배열에 있는 항목 수를 제한해야 합니다. 추적해야 하는 항목 수가 제한을 초과할 수 있는 경우 여러 함수를 만듭니다.

예를 들어 eCommerce 제출 명령 구성 요소는 호출에서 4개 항목의 `product` 항목 수를 제한합니다. 장바구니에 4개 이상의 제품이 포함되어 있으면 여러 개의 `CQ_Analytics.record` 함수를 생성합니다.
