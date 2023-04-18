---
title: 타깃팅된 컨텐츠를 위한 개발
seo-title: Developing for Targeted Content
description: 콘텐츠 타깃팅에 사용할 구성 요소 개발에 대한 주제입니다
seo-description: Topics about developing components for use with content targeting
uuid: 2449347e-7e1c-427b-a5b0-561055186934
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: bff078cd-c390-4870-ad1d-192807c67ca4
docset: aem65
exl-id: 92b62532-4f79-410d-903e-d2bca6d0fd1c
source-git-commit: fb9363a39ffc9d3929a31a3a19a124b806607ef4
workflow-type: tm+mt
source-wordcount: '1275'
ht-degree: 4%

---

# 타깃팅된 컨텐츠를 위한 개발{#developing-for-targeted-content}

이 섹션에서는 컨텐츠 타깃팅에 사용할 구성 요소 개발에 대해 설명합니다.

* Adobe Target과의 연결에 대한 자세한 내용은 [Adobe Target과 통합](/help/sites-administering/target.md).
* 타깃팅된 컨텐츠 작성에 대한 자세한 내용은 [타깃팅 모드를 사용한 타깃팅된 컨텐츠 작성](/help/sites-authoring/content-targeting-touch.md).

>[!NOTE]
>
>AEM 작성자의 구성 요소를 타겟팅하면 해당 구성 요소는 Adobe Target에 대한 일련의 서버측 호출을 만들어 캠페인을 등록하고, 오퍼를 설정하고, Adobe Target 세그먼트를 검색합니다(구성된 경우). AEM 게시에서 Adobe Target으로는 서버측 호출을 만들 수 없습니다.

## 페이지에서 Adobe Target을 사용하여 타깃팅 활성화 {#enabling-targeting-with-adobe-target-on-your-pages}

Adobe Target과 상호 작용하는 페이지에서 타깃팅된 구성 요소를 사용하려면 다음에 특정 클라이언트측 코드를 포함하십시오 &lt;head> 요소를 생성하지 않습니다.

### 헤드 섹션 {#the-head-section}

다음 코드 블록을 모두 &lt;head> 페이지의 섹션:

```xml
<!--/* Include Context Hub */-->
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

```xml
<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
```

이 코드는 필요한 analytics javascript 개체를 추가하고 웹 사이트와 연결된 클라우드 서비스 라이브러리를 로드합니다. Target 서비스의 경우 라이브러리는 를 통해 로드됩니다 `/libs/cq/analytics/components/testandtarget/headlibs.jsp`

로드된 라이브러리 집합은 Target 구성에 사용되는 target 클라이언트 라이브러리(mbox.js 또는 at.js)의 유형에 따라 다릅니다.

**기본 mbox.js의 경우**

```
<script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/mbox.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/personalization/integrations/commons.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/util.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/init.js"></script>
```

**사용자 지정 mbox.js의 경우**

```
<script type="text/javascript" src="/etc/cloudservices/testandtarget/<CLIENT-CODE>/_jcr_content/public/mbox.js"></script>
        <script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/personalization/integrations/commons.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/util.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/init.js"></script>
```

**at.js의 경우**

```
<script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs-integration.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs.js"></script>
```

>[!NOTE]
>
>버전 `at.js` 제품과 함께 제공되는 제품이 지원됩니다. 버전 `at.js` 제품과 함께 배송되는 것은 `at.js` 위치:
>
>**/libs/cq/testandtarget/clientlibs/testandtarget/atjs/source/at.js**.

**사용자 지정 at.js의 경우**

```
<script type="text/javascript" src="/etc/cloudservices/testandtarget/<CLIENT-CODE>/_jcr_content/public/at.js"></script>
    <script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs-integration.js"></script>
```

클라이언트측의 Target 기능은 `CQ_Analytics.TestTarget` 개체. 따라서 이 페이지에는 다음 예와 같은 일부 init 코드가 포함됩니다.

```
<script type="text/javascript">
            if ( !window.CQ_Analytics ) {
                window.CQ_Analytics = {};
            }
            if ( !CQ_Analytics.TestTarget ) {
                CQ_Analytics.TestTarget = {};
            }
            CQ_Analytics.TestTarget.clientCode = 'my_client_code';
        </script>
      ...

    <div class="cloudservice testandtarget">
  <script type="text/javascript">
  CQ_Analytics.TestTarget.maxProfileParams = 11;

  if (CQ_Analytics.CCM) {
   if (CQ_Analytics.CCM.areStoresInitialized) {
    CQ_Analytics.TestTarget.registerMboxUpdateCalls();
   } else {
    CQ_Analytics.CCM.addListener("storesinitialize", function (e) {
     CQ_Analytics.TestTarget.registerMboxUpdateCalls();
    });
   }
  } else {
   // client context not there, still register calls
   CQ_Analytics.TestTarget.registerMboxUpdateCalls();
  }
  </script>
 </div>
```

JSP는 필요한 Analytics Javascript 개체 및 참조를 클라이언트측 javascript 라이브러리에 추가합니다. testandtarget.js 파일에는 mbox.js 함수가 포함되어 있습니다. 스크립트가 생성하는 HTML은 다음 예와 유사합니다.

```xml
<script type="text/javascript">
        if ( !window.CQ_Analytics ) {
            window.CQ_Analytics = {};
        }
        if ( !CQ_Analytics.TestTarget ) {
            CQ_Analytics.TestTarget = {};
        }
        CQ_Analytics.TestTarget.clientCode = 'MyClientCode';
</script>
<link rel="stylesheet" href="/etc/clientlibs/foundation/testandtarget/testandtarget.css" type="text/css">
<script type="text/javascript" src="/etc/clientlibs/foundation/testandtarget/testandtarget.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/testandtarget/init.js"></script>
```

#### 본문 섹션(시작) {#the-body-section-start}

다음 코드를 &lt;body> 태그에 다음 태그를 추가하여 클라이언트 컨텍스트 기능을 페이지에 추가합니다.

```xml
<cq:include path="clientcontext" resourceType="cq/personalization/components/clientcontext"/>
```

#### 본문 섹션(끝) {#the-body-section-end}

다음 코드를 &lt;/body> 종료 태그:

```xml
<cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
```

이 구성 요소의 JSP 스크립트는 Target Javascript API에 대한 호출을 생성하고 다른 필요한 구성을 구현합니다. 스크립트가 생성하는 HTML은 다음 예와 유사합니다.

```xml
<div class="servicecomponents cloudservices">
  <div class="cloudservice testandtarget">
    <script type="text/javascript">
      CQ_Analytics.TestTarget.maxProfileParams = 11;
      CQ_Analytics.CCM.addListener("storesinitialize", function(e) {
        CQ_Analytics.TestTarget.registerMboxUpdateCalls();
      });
    </script>
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
</div>
```

### 사용자 지정 Target 라이브러리 파일 사용 {#using-a-custom-target-library-file}

>[!NOTE]
>
>DTM이나 다른 target 마케팅 시스템을 사용하지 않는 경우 사용자 지정 target 라이브러리 파일을 사용할 수 있습니다.

>[!NOTE]
>
>기본적으로 mbox는 숨겨지며 mboxDefault 클래스는 이 동작을 결정합니다. mbox를 숨기면 방문자가 교체되기 전에 기본 콘텐츠를 볼 수 없습니다. 그러나 mbox를 숨기면 인식된 성능에 영향을 줍니다.

mbox를 만드는 데 사용되는 기본 mbox.js 파일은 /etc/clientlibs/foundation/testandtarget/mbox/source/mbox.js에 있습니다. 고객 mbox.js 파일을 사용하려면 Target 클라우드 구성에 파일을 추가하십시오. 파일을 추가하려면 파일 시스템에서 mbox.js 파일을 사용할 수 있어야 합니다.

예를 들어 [Marketing Cloud ID 서비스](https://experienceleague.adobe.com/docs/id-service/using/home.html) mbox.js에 대한 올바른 값이 포함되도록 다운로드해야 합니다. `imsOrgID` 변수를 채우는 방법을 설명합니다. 이 변수는 Marketing Cloud ID 서비스와 통합하는 데 필요합니다. 자세한 내용은 [Adobe Target용 보고 소스로서의 Adobe Analytics](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) 및 [구현하기 전에](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/before-implement.html).

>[!NOTE]
>
>사용자 지정 mbox가 Target 구성에 정의된 경우 모든 사용자에게는 **/etc/cloudservices** 게시 서버에 게시되지 않습니다. 이 액세스 권한이 없으면 게시 웹 사이트에 mbox.js 파일을 로드하면 404 오류가 발생합니다.

1. CQ로 이동합니다. **도구** 페이지를 선택하고 **Cloud Services**. ([https://localhost:4502/libs/cq/core/content/tools/cloudservices.html](https://localhost:4502/libs/cq/core/content/tools/cloudservices.html))
1. 트리에서 Adobe Target 를 선택하고 구성 목록에서 Target 구성을 두 번 클릭합니다.
1. 구성 페이지에서 편집을 클릭합니다.
1. 사용자 지정 mbox.js 속성에 대해 찾아보기 를 클릭하고 파일을 선택합니다.
1. 변경 사항을 적용하려면 Adobe Target 계정의 암호를 입력하고 Target에 다시 연결 을 클릭한 다음 연결이 성공하면 확인 을 클릭합니다. 그런 다음 구성 요소 편집 대화 상자에서 확인을 클릭합니다.

Target 구성에 사용자 지정 mbox.js 파일이 포함되어 있습니다. [head 섹션에 필요한 코드](/help/sites-developing/target.md#p-the-head-section-p) 페이지의 는 testandtarget.js 라이브러리에 대한 참조 대신 클라이언트 라이브러리 프레임워크에 파일을 추가합니다.

## 구성 요소에 대한 Target 명령 비활성화 {#disabling-the-target-command-for-components}

대부분의 구성 요소는 컨텍스트 메뉴에서 Target 명령을 사용하여 타깃팅된 구성 요소로 변환할 수 있습니다.

![chlimage_1-21](assets/chlimage_1-21.png)

컨텍스트 메뉴에서 Target 명령을 제거하려면 구성 요소의 cq:editConfig 노드에 다음 속성을 추가하십시오.

* 이름: cq:disableTargeting
* 유형: 부울
* 값: True

예를 들어 Geometrixx 데모 사이트 페이지의 제목 구성 요소에 대한 타깃팅을 비활성화하려면 속성을 /apps/geometrixx/components/title/cq:editConfig 노드에 추가합니다.

![chlimage_1-22](assets/chlimage_1-22.png)

## Adobe Target에 주문 확인 정보 보내기 {#sending-order-confirmation-information-to-adobe-target}

>[!NOTE]
>
>DTM을 사용하지 않는 경우 주문 확인을 Adobe Target에 보냅니다.

웹 사이트의 성능을 추적하려면 주문 확인 페이지에서 Adobe Target으로 구매 정보를 보내십시오. (자세한 내용은 [orderConfirmPage Mbox 만들기](https://developer.adobe.com/target/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager/?lang=en) 및 [주문 확인 Mbox - 사용자 지정 매개 변수를 추가합니다.](https://experienceleaguecommunities.adobe.com/t5/adobe-target-questions/order-confirmation-mbox-add-custom-parameters/m-p/275779)) Adobe Target은 MBox 이름이 인 경우 mbox 데이터를 주문 확인 데이터로 인식합니다 `orderConfirmPage` 에서는 다음과 같은 특정 매개 변수 이름을 사용합니다.

* productPurchasedId: 구입한 제품을 식별하는 ID 목록입니다.
* orderId: 주문 ID입니다.
* orderTotal: 구매의 총 금액입니다.

mbox를 만드는 렌더링된 HTML 페이지의 코드는 다음 예와 유사합니다.

```xml
<script type="text/javascript">
     mboxCreate('orderConfirmPage',
     'productPurchasedId=product1 product2 product3',
     'orderId=order1234',
     'orderTotal=24.54');
</script>
```

각 매개 변수의 값은 각 순서에 대해 다릅니다. 따라서 구매 속성을 기반으로 코드를 생성하는 구성 요소가 필요합니다. CQ [eCommerce Integration Framework](/help/commerce/cif-classic/administering/ecommerce.md) 를 제품 카탈로그와 통합하고 장바구니 및 체크아웃 페이지를 구현할 수 있도록 해줍니다.

방문자가 제품을 구매할 때 Geometrixx Outdoors 샘플에 다음 확인 페이지가 표시됩니다.

![chlimage_1-23](assets/chlimage_1-23.png)

구성 요소의 JSP 스크립트에 대한 다음 코드는 장바구니의 속성에 액세스한 다음 mbox를 만들기 위한 코드를 인쇄합니다.

```java
<%--

  confirmationmbox component.

--%><%
%><%@include file="/libs/foundation/global.jsp"%><%
%><%@page session="false"
          import="com.adobe.cq.commerce.api.CommerceService,
                  com.adobe.cq.commerce.api.CommerceSession,
                  com.adobe.cq.commerce.common.PriceFilter,
                  com.adobe.cq.commerce.api.Product,
                  java.util.List, java.util.Iterator"%><%

/* obtain the CommerceSession object */
CommerceService commerceservice = resource.adaptTo(CommerceService.class);
CommerceSession session = commerceservice.login(slingRequest, slingResponse);

/* obtain the cart items */
List<CommerceSession.CartEntry> entries = session.getCartEntries();
Iterator<CommerceSession.CartEntry> cartiterator = entries.iterator();

/* iterate the items and get the product IDs */
String productIDs = new String();
while(cartiterator.hasNext()){
 CommerceSession.CartEntry entry = cartiterator.next();
 productIDs = productIDs + entry.getProduct().getSKU();
    if (cartiterator.hasNext()) productIDs = productIDs + ", ";
}

/* get the cart price and orderID */
String total = session.getCartPrice(new PriceFilter("CART", "PRE_TAX"));
String orderID = session.getOrderId();

%><div class="mboxDefault"></div>
<script type="text/javascript">
     mboxCreate('orderConfirmPage',
     'productPurchasedId=<%= productIDs %>',
     'orderId=<%= orderID %>',
     'orderTotal=<%= total %>');
</script>
```

구성 요소가 이전 예제의 체크아웃 페이지에 포함되면 페이지 소스에는 mbox를 만드는 다음 스크립트가 포함됩니다.

```
<div class="mboxDefault"></div>
<script type="text/javascript">

     mboxCreate('orderConfirmPage',
     'productPurchasedId=47638-S, 46587',
     'orderId=d03cb015-c30f-4bae-ab12-1d62b4d105ca',
     'orderTotal=US$677.00');

</script>
```

## Target 구성 요소 이해 {#understanding-the-target-component}

Target 구성 요소를 사용하면 작성자가 CQ 컨텐츠 구성 요소에서 다이내믹 mbox를 만들 수 있습니다. (자세한 내용은 [컨텐츠 타깃팅](/help/sites-authoring/content-targeting-touch.md)) Target 구성 요소는 /libs/cq/personalization/components/target에 있습니다.

target.jsp 스크립트는 페이지 속성에 액세스하여 구성 요소에 사용할 타깃팅 엔진을 결정한 다음 적절한 스크립트를 실행합니다.

* Adobe Target: /libs/cq/personalization/components/target/engine_tnt.jsp
* [AT.JS를 사용한 Adobe Target](/help/sites-administering/target.md): /libs/cq/personalization/components/target/engine_atjs.jsp
* [Adobe Campaign](/help/sites-authoring/target-adobe-campaign.md): /libs/cq/personalization/components/target/engine_cq_campaign.jsp
* 클라이언트측 규칙/ContextHub: /libs/cq/personalization/components/target/engine_cq.jsp

### Mbox 만들기 {#the-creation-of-mboxes}

>[!NOTE]
>
>기본적으로 mbox는 숨겨지며 mboxDefault 클래스는 이 동작을 결정합니다. mbox를 숨기면 방문자가 교체되기 전에 기본 콘텐츠를 볼 수 없습니다. 그러나 mbox를 숨기면 인식된 성능에 영향을 줍니다.

Adobe Target에서 컨텐츠 타깃팅을 구동하면 engine_tnt.jsp 스크립트는 타깃팅된 경험의 컨텐츠를 포함하는 mbox를 만듭니다.

* 추가 `div` 의 클래스가 있는 요소 `mboxDefault`를 사용 할 수도 있습니다.

* 내부에 mbox 콘텐츠(타깃팅된 경험의 콘텐츠)를 추가합니다 `div` 요소를 생성하지 않습니다.

다음을 수행합니다 `mboxDefault` div 요소, mbox를 만드는 javascript가 삽입됩니다.

* mbox 이름, ID 및 위치는 구성 요소의 저장소 경로를 기반으로 합니다.
* 스크립트는 Client Context 매개 변수 이름과 값을 가져옵니다.
* mbox를 만들기 위해 mbox.js 및 기타 클라이언트 라이브러리가 정의하는 함수에 대한 호출이 수행됩니다.

#### 컨텐츠 타깃팅을 위한 클라이언트 라이브러리 {#client-libraries-for-content-targeting}

다음은 사용 가능한 clientlib 카테고리입니다.

* testandtarget.mbox
* testandtarget.init
* testandtarget.util
* testandtarget.atjs
* testandtarget.atjs-integration
