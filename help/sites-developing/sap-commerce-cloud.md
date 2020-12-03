---
title: SAP Commerce Cloud를 사용하여 개발
seo-title: SAP Commerce Cloud를 사용하여 개발
description: SAP Commerce Cloud 통합 프레임워크에는 API와 통합 레이어가 포함됩니다
seo-description: SAP Commerce Cloud 통합 프레임워크에는 API와 통합 레이어가 포함됩니다
uuid: a780dd17-027a-4a61-af8f-3e2f600524c7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
discoiquuid: 96dc0c1a-b21d-480a-addf-c3d0348bd3ad
translation-type: tm+mt
source-git-commit: 2dad235c94c73c1c624fa05ff86a7260d4d4a01b
workflow-type: tm+mt
source-wordcount: '2329'
ht-degree: 1%

---


# SAP Commerce Cloud를 사용하여 개발 {#developing-with-sap-commerce-cloud}

>[!NOTE]
>
>전자 상거래 프레임워크는 모든 전자 상거래 솔루션에서 사용할 수 있습니다. 여기에서 다뤄지는 특정 세부 사항과 예제는 [hybris](https://www.hybris.com/) 솔루션을 의미합니다.

통합 프레임워크에는 API와 통합 레이어가 포함되어 있습니다. 이를 통해 다음을 수행할 수 있습니다.

* e커머스 시스템을 연결하고 AEM에 제품 데이터 가져오기

* 특정 eCommerce 엔진과 독립적인 상거래 기능을 위한 AEM 구성 요소 구축

![chlimage_1-11](assets/chlimage_1-11a.png)

>[!NOTE]
>
>[API ](/help/sites-developing/ecommerce.md#api-documentation) 설명서도 사용할 수 있습니다.

통합 레이어를 사용할 수 있는 다양한 기본 AEM 구성 요소가 제공됩니다. 현재 다음과 같습니다.

* 제품 표시 구성 요소
* 장바구니
* 체크아웃

AEM 검색, 전자 상거래 시스템 검색, 타사 검색(Search &amp; Promote 등) 또는 이러한 조합을 사용할 수 있도록 해주는 통합 후크가 제공됩니다.

## 전자 상거래 엔진 선택 {#ecommerce-engine-selection}

eCommerce 프레임워크는 모든 eCommerce 솔루션에서 사용할 수 있으며, 사용되는 엔진은 AEM에서 확인해야 합니다.

* eCommerce Engine은 `CommerceService` 인터페이스를 지원하는 OSGi 서비스입니다.

   * 엔진은 `commerceProvider` 서비스 속성으로 식별할 수 있습니다.

* AEM은 `CommerceService` 및 `Product`에 대해 `Resource.adaptTo()`을 지원합니다.

   * `adaptTo` 구현은 리소스 계층 구조에서 `cq:commerceProvider` 속성을 찾습니다.

      * 검색된 경우 이 값은 커머스 서비스 조회를 필터링하는 데 사용됩니다.

      * 찾을 수 없으면 가장 높은 등급의 커머스 서비스가 사용됩니다.
   * `cq:Commerce` 혼합이 사용되므로 강력한 형식의 리소스에 `cq:commerceProvider`을(를) 추가할 수 있습니다.


* `cq:commerceProvider` 속성은 적절한 상거래 팩토리 정의를 참조하는 데에도 사용됩니다.

   * 예를 들어 값 `hybris`의 `cq:commerceProvider` 속성은 Hybris **(com.adobe.cq.commerce.hybris.impl.HybrisServiceFactory)에 대한 OSGi 구성에 상관 관계가 있습니다. 여기서 매개 변수 `commerceProvider`에 값 `hybris`이(가) 있습니다.**

   * 여기에서 **카탈로그 버전**&#x200B;과 같은 추가 속성을 구성할 수 있습니다(해당되는 경우 및 사용 가능).

아래의 예를 참조하십시오.

| `cq:commerceProvider = geometrixx` | 표준 AEM 설치에서는 특정 구현이 필요합니다.예를 들어, geometrixx 예제(일반 API에 대한 최소 확장 기능 포함) |
|--- |--- |
| `cq:commerceProvider = hybris` | hybris 구현 |

### 예 {#example}

```shell
/content/store
+ cq:commerceProvider = hybris
  + mens
    + polo-shirt-1
    + polo-shirt-2
    + employee
+ cq:commerceProvider = jcr
  + adobe-logo-shirt
    + cq:commerceType = product
    + price = 12.50
  + adobe-logo-shirt_S
    + cq:commerceType = variant
    + size = S
  + adobe-logo-shirt_XL
    + cq:commerceType = variant
    + size = XL
    + price = 14.50
```

>[!NOTE]
>
>CRXDE Lite을 사용하면 하이브리스 구현에 대한 제품 구성 요소에서 이 작업이 어떻게 처리되는지 확인할 수 있습니다.
>
>`/apps/geometrixx-outdoors/components/hybris/product/product.jsp`

### hybris 4 {#developing-for-hybris} 개발

e커머스 통합 프레임워크의 하이브리스 확장은 하이브리스 4와 이전 버전과의 호환성을 유지하면서 Hybris 5를 지원하도록 업데이트되었습니다.

코드의 기본 설정은 Hybris 5에 맞게 조정됩니다.

Hybris 4를 개발하기 위해서는 다음이 필요합니다.

* 마벤을 호출할 때 다음 명령줄 인수를 명령에 추가합니다.

   `-P hybris4`

   사전 구성된 Hybris 4 배포를 다운로드하고 번들 `cq-commerce-hybris-server`에 포함합니다.

* OSGi 구성 관리자에서:

   * 기본 응답 파서 서비스에 대한 Hybris 5 지원을 비활성화합니다.

   * Hybris Basic Authentication Handler 서비스가 Hybris OAuth Handler 서비스보다 서비스 순위가 낮은지 확인하십시오.

### 세션 처리 {#session-handling}

hybris는 사용자 세션을 사용하여 고객의 장바구니와 같은 정보를 저장합니다. 세션 ID는 이후 요청 시 하이브리스로 전송해야 하는 `JSESSIONID` 쿠키의 하이브리스에서 반환됩니다. 세션 ID를 저장소에 저장하지 않게 하려면 구매자의 브라우저에 저장된 다른 쿠키로 인코딩됩니다. 다음 단계가 수행됩니다.

* 첫 번째 요청에서는 구매자의 요청에 쿠키가 설정되지 않습니다.따라서 세션을 만들기 위해 hybris 인스턴스로 요청이 전송됩니다.

* 세션 쿠키는 응답에서 추출되며 새 쿠키(예: `hybris-session-rest`)로 인코딩되어 구매자에 대한 응답을 설정합니다. 원래 쿠키는 특정 경로에만 유효하고 이후 요청에서는 브라우저에서 다시 전송되지 않으므로 새 쿠키의 인코딩이 필요합니다. 경로 정보도 쿠키의 값에 추가해야 합니다.

* 후속 요청에서 쿠키는 `hybris-session-<*xxx*>` 쿠키에서 디코딩되고 하이브리스의 데이터를 요청하는 데 사용되는 HTTP 클라이언트에 설정됩니다.

>[!NOTE]
>
>원본 세션이 더 이상 유효하지 않을 때 새로운 익명 세션이 만들어집니다.

#### 상거래 세션 {#commercesession}

* 이 세션은 **장바구니**&#x200B;를 &quot;소유&quot;합니다.

   * 추가/제거/기타

   * 장바구니에서 다양한 계산을 수행합니다.

      `commerceSession.getProductPrice(Product product)`

* **order** 데이터에 대한 *저장소 위치*&#x200B;를 소유합니다.

   `CommerceSession.getUserContext()`

* 또한 **payment** 처리 연결을 소유합니다.

* **fulfillment** 연결도 소유합니다.

### 제품 동기화 및 게시 {#product-synchronization-and-publishing}

하이브리스로 유지되는 제품 데이터를 AEM에서 사용할 수 있어야 합니다. 다음 메커니즘이 구현되었습니다.

* ID의 초기 로드는 하이브리스에서 피드로 제공됩니다. 이 피드에 대한 업데이트가 있을 수 있습니다.
* hybris는 피드(AEM 투표)를 통해 업데이트 정보를 제공합니다.
* AEM에서 제품 데이터를 사용하는 경우 현재 데이터에 대한 요청을 hybris로 다시 보냅니다(마지막 수정 날짜를 사용한 조건부 가져오기 요청).
* 하이브리스에서는 선언적 방식으로 피드 컨텐츠를 지정할 수 있습니다.
* AEM 컨텐트 모델에 피드 구조를 매핑하는 작업은 AEM 측의 피드 어댑터에서 이루어집니다.

![chlimage_1-12](assets/chlimage_1-12a.png)

* 가져오기 도구(b)는 카탈로그의 AEM에서 페이지 트리 구조의 초기 설정에 사용됩니다.
* 하이브리스의 카탈로그 변경 사항은 피드를 통해 AEM에 표시된 다음 AEM(b)에 전파됩니다.

   * 카탈로그 버전과 관련하여 추가/삭제/변경된 제품

   * 제품 승인됨.

* hybris 확장자는 지정된 간격(예: 간격을 초 단위로 지정하는 24시간마다)에 변경 내용을 AEM으로 가져오도록 구성할 수 있는 투표 가져오기(&quot;hybris&quot; scheme&quot;)를 제공합니다.

   ```JavaScript
       http://localhost:4502/content/geometrixx-outdoors/en_US/jcr:content.json
        {
        * "jcr:mixinTypes": ["cq:PollConfig"],
        * "enabled": true,
        * "source": "hybris:outdoors",
        * "jcr:primaryType": "cq:PageContent",
        * "interval": 86400
        }
   ```

* AEM의 카탈로그 구성은 **Staged** 및 **Online** 카탈로그 버전을 인식합니다.

* 카탈로그 버전 간 제품을 동기화하려면 해당 AEM 페이지(a, c)의 (비)정품 인증이 필요합니다.

   * **온라인** 카탈로그 버전에 제품을 추가하려면 제품 페이지를 활성화해야 합니다.

   * 제품을 제거하려면 비정품 인증이 필요합니다.

* AEM(c)에서 페이지를 활성화하려면 확인(b)이 필요하며,

   * 제품은 제품 페이지의 **온라인** 카탈로그 버전입니다.

   * 참조된 제품은 다른 페이지(예: 캠페인 페이지)에 대한 **온라인** 카탈로그 버전에서 사용할 수 있습니다.

* 활성화된 제품 페이지는 제품 데이터의 **온라인** 버전(d)에 액세스해야 합니다.

* AEM 게시 인스턴스에서는 제품 및 개인화된 데이터(d)를 검색하기 위해 하이브리스에 액세스해야 합니다.

### 아키텍처 {#architecture}

#### 제품 및 변형 구조 {#architecture-of-product-and-variants}

단일 제품에는 여러 변수가 있을 수 있습니다.예를 들어 색상 및/또는 크기마다 다를 수 있습니다. 제품은 어떤 속성을 통해 변화를 이끌어내는지 정의해야 합니다.이러한 *변형 축*&#x200B;을 지칭합니다.

그러나 일부 속성이 변형 축은 아닙니다. 변형은 다른 속성에도 영향을 줄 수 있습니다.예를 들어 가격이 크기에 따라 달라질 수 있습니다. 이러한 속성은 구매자가 선택할 수 없으므로 변형 축으로 간주되지 않습니다.

각 제품 및/또는 변형은 리소스로 표현되므로 저장소 노드에 1:1을 매핑합니다. 특정 제품 및/또는 변형이 해당 경로로 고유하게 식별될 수 있다는 것은 필연입니다.

제품/변형 리소스가 항상 실제 제품 데이터를 가지고 있는 것은 아니므로 다른 시스템(예: hybris)에 실제로 들어 있는 데이터를 나타내는 것일 수 있습니다. 예를 들어 제품 설명, 가격 등은 AEM에 저장되지는 않지만 eCommerce 엔진에서 실시간으로 검색됩니다.

모든 제품 리소스는 `Product API`으로 나타낼 수 있습니다. 제품 API의 대부분의 호출은 변형이 고유하지만(변형이 조상에서 공유 값을 상속할 수 있음), 변형 집합( `getVariantAxes()`, `getVariants()` 등)을 나열하는 호출도 있습니다.

>[!NOTE]
>
>사실상 변형 축은 `Product.getVariantAxes()`이 반환하는 모든 것에 의해 결정됩니다.
>* hybris는 hybris 구현을 위해 정의합니다.
>
>
제품(일반적으로)은 많은 변형 축을 가질 수 있지만, 기본적으로 제공되는 제품 구성 요소는 두 개만 처리합니다.
>
>1. `size`
   >
   >
1. 하나 더
>
>
이 추가 변형은 제품 참조의 `variationAxis` 속성(일반적으로 Geometrixx Outdoors의 경우 `color`)을 통해 선택됩니다.

#### 제품 참조 및 제품 데이터 {#product-references-and-product-data}

일반적으로:

* 제품 데이터는 `/etc` 아래에 있습니다.

* 및 제품 참조는 `/content` 아래에 있습니다.

제품 변형과 제품 데이터 노드 간에는 1:1 맵이 있어야 합니다.

제품 참조에도 제시된 각 변형에 대한 노드가 있어야 하지만 모든 변형을 제시할 필요는 없습니다. 예를 들어 제품에 S, M, L 변형이 있는 경우 제품 데이터는 다음과 같습니다.

```shell
etc
|──commerce
|  |──products
|     |──shirt
|       |──shirt-s
|       |──shirt-m
|       |──shirt-l
```

&quot;크고 긴&quot; 카탈로그에는 다음이 있을 수 있습니다.

```shell
content
|──big-and-tall
|  |──shirt
|     |──shirt-l
```

마지막으로 제품 데이터를 사용할 필요가 없습니다. 카탈로그의 참조 아래에 모든 제품 데이터를 배치할 수 있습니다.그러나 제품 데이터를 모두 복제하지 않으면 여러 카탈로그를 만들 수 없습니다.

**API**

#### com.adobe.cq.commerce.api.제품 인터페이스 {#com-adobe-cq-commerce-api-product-interface}

```java
public interface Product extends Adaptable {

    public String getPath();            // path to specific variation
    public String getPagePath();        // path to presentation page for all variations
    public String getSKU();             // unique ID of specific variation

    public String getTitle();           // shortcut to getProperty(TITLE)
    public String getDescription();     // shortcut to getProperty(DESCRIPTION)
    public String getImageUrl();        // shortcut to getProperty(IMAGE_URL)
    public String getThumbnailUrl();    // shortcut to getProperty(THUMBNAIL_URL)

    public <T> T getProperty(String name, Class<T> type);

    public Iterator<String> getVariantAxes();
    public boolean axisIsVariant(String axis);
    public Iterator<Product> getVariants(VariantFilter filter) throws CommerceException;
}
```

#### com.adobe.cq.commerce.api.VariantFilter {#com-adobe-cq-commerce-api-variantfilter}

```java
/**
 * Interface for filtering variants and AxisFilter provided as common implementation
 *
 * The <code>VariantFilter</code> is used to filter variants,
 * e.g. when using {@link Product#getVariants(VariantFilter filter)}.
 */
public interface VariantFilter {
    public boolean includes(Product product);
}

/**
 * A {@link VariantFilter} for filtering variants by the given
 * axis and value. The following example returns a list of
 * variant products that have a value of <i>blue</i> on the
 * <i>color</i> axis.
 *
 * <p>
 * <code>product.getVariants(new AxisFilter("color", "blue"));</code>
 */
public class AxisFilter implements VariantFilter {

    private String axis;
    private String value;

    public AxisFilter(String axis, String value) {
        this.axis = axis;
        this.value = value;
    }

    /**
     * {@inheritDoc}
     */
    public boolean includes(Product product) {
        ValueMap values = product.adaptTo(ValueMap.class);

        if(values != null) {
            String v = values.get(axis, String.class);

            return v != null && v == value;
        }

        return false;
    }
}
```

* **일반 스토리지 메커니즘**

   * 제품 노드는 `nt:unstructured`입니다.

   * 제품 노드는 다음 중 하나일 수 있습니다.

      * 제품 데이터가 다른 곳에 저장되는 참조:

         * 제품 참조에는 제품 데이터를 가리키는 `productData` 속성이 포함됩니다(일반적으로 `/etc/commerce/products` 아래).

         * 제품 데이터는 계층적입니다.제품 속성은 제품 데이터 노드의 상위 항목에서 상속됩니다.

         * 제품 참조에는 제품 데이터에 지정된 속성을 재정의하는 로컬 속성이 포함될 수도 있습니다.
      * 제품 자체:

         * `productData` 속성이 없습니다.

         * 모든 속성을 로컬로 보유하며 productData 속성을 포함하지 않는 제품 노드는 해당 상위 제품에서 바로 제품 특성을 상속합니다.


* **AEM-일반 제품 구조**

   * 각 변형에는 자체 리프 노드가 있어야 합니다.

   * 제품 인터페이스는 제품 및 변형을 모두 표시하지만 관련 저장소 노드는 그에 따라 다릅니다.

   * 제품 노드는 제품 속성과 변형 축에 대해 설명합니다.

#### 예 {#example-1}

```shell
+ banyan_shirt
    - cq:commerceType = product
    - cq:productAttributes = [jcr:title, jcr:description, size, price, color]
    - cq:productVariantAxes = [color, size]
    - jcr:title = Banyan Shirt
    - jcr:description = Flowery, all-cotton shirt.
    - price = 14.00
    + banyan_shirt_s
        - cq:commerceType = variant
        - size = S
        + banyan_shirt_s_red
            - cq:commerceType = variant
            - color = red
        + banyan_shirt_s_blue
            - cq:commerceType = variant
            - color = blue
    + banyan_shirt_m
        - cq:commerceType = variant
        - size = M
        + banyan_shirt_m_red
            - cq:commerceType = variant
            - color = red
        + banyan_shirt_m_blue
            - cq:commerceType = variant
            - color = blue
    + banyan_shirt_l
        - cq:commerceType = variant
        - size = L
        + banyan_shirt_l_red
            - cq:commerceType = variant
            - color = red
        + banyan_shirt_l_blue
            - cq:commerceType = variant
            - color = blue
    + banyan_shirt_xl
        - cq:commerceType = variant
        - size = XL
        - price = 18.00
```

#### 장바구니 아키텍처 {#architecture-of-the-shopping-cart}

**구성 요소**

* 장바구니는 `CommerceSession:` 소유입니다.

   * `CommerceSession`은 추가/제거 등을 수행합니다.
   * `CommerceSession`도 장바구니에서 다양한 계산을 수행합니다.&quot;

* 직접 장바구니와 관련되지 않지만, `CommerceSession`은(는) 가격을 소유하기 때문에) 카탈로그 가격 정보도 제공해야 합니다.

   * 가격에 몇 개의 수정자가 있을 수 있습니다.

      * 수량 할인.
      * 다른 통화.
      * VAT 및 VAT 별도
   * 수정자는 다음 인터페이스로 완전히 열린 것입니다.

      * `int CommerceSession.getQuantityBreakpoints(Product product)`
      * `String CommerceSession.getProductPrice(Product product)`


**저장 용량**

* 저장 용량

   * 하이브리스의 경우, 하이브리스 서버가 장바구니를 소유한다.
   * AEM-일반 케이스 카트는 [ClientContext](/help/sites-administering/client-context.md)에 저장됩니다.

**개인화**

* 개인화는 항상 [ClientContext](/help/sites-administering/client-context.md)을 통해 구현되어야 합니다.
* 모든 경우 장바구니의 ClientContext `/version/`이 만들어집니다.

   * `CommerceSession.addCartEntry()` 메서드를 사용하여 제품을 추가해야 합니다.

* 다음은 ClientContext 장바구니에 있는 장바구니 정보의 예를 보여 줍니다.

![chlimage_1-13](assets/chlimage_1-13a.png)

#### 체크아웃 {#architecture-of-checkout} 아키텍처

**장바구니 및 주문 데이터**

`CommerceSession`은 다음 세 요소를 소유합니다.

1. 장바구니 내용
1. 가격
1. 주문 세부 정보

1. **장바구니 내용**

   장바구니 콘텐츠 스키마가 API에 의해 수정되었습니다.

   ```java
   public void addCartEntry(Product product, int quantity);
   public void modifyCartEntry(int entryNumber, int quantity);
   public void deleteCartEntry(int entryNumber);
   ```

1. **가격**

   가격 스키마는 API에서도 수정되었습니다.

   ```java
   public String getCartPreTaxPrice();
   public String getCartTax();
   public String getCartTotalPrice();
   public String getOrderShipping();
   public String getOrderTotalTax();
   public String getOrderTotalPrice();
   ```

1. **주문 세부 사항**

   하지만 주문 세부 사항은 API에서 수정되지 않은 *입니다.*

   ```java
   public void updateOrderDetails(Map<String, String> orderDetails);
   public Map<String, String> getOrderDetails();
   public void submitOrder();
   ```

**배송 계산**

* 주문 양식에는 여러 배송 옵션(및 가격)이 필요합니다.
* 가격은 중량 및/또는 배달 주소와 같은 주문 및 세부 사항에 따라 책정될 수 있습니다.
* `CommerceSession`은(는) 모든 종속성에 액세스할 수 있으므로 제품 가격과 비슷한 방식으로 처리할 수 있습니다.

   * `CommerceSession`은 배송 가격을 소유합니다.
   * `updateOrder(Map<String, Object> delta)`을 사용하여 배달 세부 사항을 검색/업데이트할 수 있습니다.

>[!NOTE]
>
>배송 선택기를 구현할 수 있습니다.예를 들면 다음과 같습니다.
>
>`yourProject/commerce/components/shippingpicker`:
>
>* 기본적으로 이것은 `foundation/components/form/radio`의 사본일 수 있지만 다음에 대한 콜백으로`CommerceSession`
   >
   >
* 메서드를 사용할 수 있는지 확인
>* 가격 정보 추가
>* 고객이 AEM에서 주문 페이지를 업데이트하도록 하려면(배송 방법의 상위 세트와 이에 대해 설명하는 텍스트 포함), 관련 `CommerceSession` 정보를 표시하는 컨트롤을 여전히 가지고 있어야 합니다.


**결제 처리**

* `CommerceSession`도 결제 처리 연결을 소유합니다.

* 구현자는 특정 호출(선택한 결제 처리 서비스에)을 `CommerceSession` 구현에 추가해야 합니다.

**주문 처리**

* `CommerceSession`도 주문 처리 연결을 소유합니다.
* 구현자는 특정 호출(선택한 결제 처리 서비스에)을 `CommerceSession` 구현에 추가해야 합니다.

### 검색 정의 {#search-definition}

표준 서비스 API 모델에 따라 eCommerce 프로젝트는 개별 상거래 엔진에서 구현할 수 있는 검색 관련 API 집합을 제공합니다.

>[!NOTE]
>
>현재 hybris 엔진만이 즉시 검색 API를 구현합니다.
>
>그러나 검색 API는 일반적이며 각 CommerceService에서 개별적으로 구현할 수 있습니다.

eCommerce 프로젝트에는 다음과 같은 기본 검색 구성 요소가 포함되어 있습니다.

`/libs/commerce/components/search`

![chlimage_1-14](assets/chlimage_1-14a.png)

이렇게 하면 검색 API를 사용하여 선택한 상거래 엔진을 쿼리할 수 있습니다([eCommerce Engine Selection](#ecommerce-engine-selection) 참조).

#### 검색 API {#search-api}

핵심 프로젝트에서 제공하는 몇 가지 일반/도우미 클래스가 있습니다.

1. `CommerceQuery`

   검색 쿼리를 설명하는 데 사용됩니다(쿼리 텍스트, 현재 페이지, 페이지 크기, 정렬 및 선택한 패싯에 대한 정보 포함). 검색 API를 구현하는 모든 eCommerce 서비스는 검색을 수행하기 위해 이 클래스의 인스턴스를 수신합니다. 요청 개체( `HttpServletRequest`)에서 `CommerceQuery`을(를) 인스턴스화할 수 있습니다.

1. `FacetParamHelper`

   패싯 목록과 전환된 값 목록에서 `GET` 매개 변수 문자열을 생성하는 데 사용되는 하나의 정적 메서드 `toParams`를 제공하는 유틸리티 클래스입니다. 이 기능은 UI에서 유용한데, 여기서 사용자가 하이퍼링크를 클릭하면 해당 값이 전환됩니다(즉, 선택한 경우에는 쿼리에서 제거되고, 그렇지 않으면 추가됨). 이는 여러/단일 값이 있는 패싯을 처리하는 모든 논리, 값 무시 등을 처리합니다.

검색 API의 시작 지점은 `CommerceResult` 개체를 반환하는 `CommerceService#search` 메서드입니다. 이 항목에 대한 자세한 내용은 [API 설명서](/help/sites-developing/ecommerce.md#api-documentation)를 참조하십시오.

### 사용자 통합 {#user-integration}

AEM 및 다양한 e커머스 시스템 간에 통합이 제공됩니다. 이를 위해서는 AEM 관련 코드만 AEM에 대해 알고 있을 수 있도록 다양한 시스템 간의 구매자를 동기화하는 전략을 수행해야 합니다.

* 인증

   AEM은 *만 웹 프런트 엔드로 간주되므로*&#x200B;모든&#x200B;*인증을 수행합니다.*

* 하이브리스의 고객

   AEM은 각 구매자를 위한 하이브리스에 해당하는(하위) 계정을 만듭니다. 이 계정의 사용자 이름은 AEM 사용자 이름과 동일합니다. 암호화 임의 암호는 AEM에서 자동으로 생성되고 저장(암호화)됩니다.

#### 기존 사용자 {#pre-existing-users}

AEM 프런트 엔드는 기존 hybris 구현 앞에 배치할 수 있습니다. 또한 기존 AEM 설치에 하이브리스 엔진을 추가할 수 있습니다. 이렇게 하려면 시스템에서 두 시스템 중 하나의 시스템에서 기존 사용자를 정상적으로 처리할 수 있어야 합니다.

* AEM -> hybris

   * 하이브리스에 로그인할 때 AEM 사용자가 아직 존재하지 않는 경우:

      * 암호화 임의의 암호로 새 hybris 사용자 생성
      * aem 사용자의 사용자 디렉토리에 hybris 사용자 이름 저장
   * 참조:`com.adobe.cq.commerce.hybris.impl.HybrisSessionImpl#login()`


* hybris -> AEM

   * AEM에 로그인할 때 시스템이 사용자를 인식하면 다음과 같이 됩니다.

      * 제공한 사용자 이름/pwd로 하이브리스에 로그인하려고 함
      * 성공하면 같은 암호로 AEM에서 새 사용자를 만듭니다(AEM 특정 소금은 AEM 특정 해시로 이어질 수 있음).
   * 위 알고리즘은 Sling `AuthenticationInfoPostProcessor`에서 구현됩니다.

      * 참조:`com.adobe.cq.commerce.hybris.impl.user.LazyUserImporter.java`


### 가져오기 프로세스 사용자 지정 {#customizing-the-import-process}

기존 기능을 기반으로 구축하려면 사용자 지정 가져오기 처리기가 필요합니다.

* `ImportHandler` 인터페이스를 구현해야 합니다.

* `DefaultImportHandler`을(를) 확장할 수 있습니다.

```java
/**
 * Services implementing the <code>ImportHandler</code> interface are
 * called by the {@link HybrisImporter} to create actual commerce entities
 * such as products.
 */
public interface ImportHandler {

  /**
  * Not used.
  */
  public void createTaxonomie(ImporterContext ctx);

  /**
  * Creates a catalog with the given name.
  * @param ctx   The importer context
  * @param name  The catalog's name
  * @return Path of created catalog
  */
  public String createCatalog(ImporterContext ctx, String name) throws Exception;

  /**
  * Creates a product from the given values.
  * @param ctx                The importer context
  * @param values             The product's properties
  * @param parentCategoryPath The containing category's path
  * @return Path of created product
  */
  public String createProduct(ImporterContext ctx, ValueMap values, String parentCategoryPath) throws Exception;

  /**
  * Creates a variant product from the given values.
  * @param ctx             The importer context
  * @param values          The product's properties
  * @param baseProductPath The base product's path
  * @return Path of created product
  */
  public String createVariantProduct(ImporterContext ctx, ValueMap values, String baseProductPath) throws Exception;

  /**
  * Creates an asset for a product. This is usually a product
  * image.
  * @param ctx             The importer context
  * @param values          The product's properties
  * @param baseProductPath The product's path
  * @return Path of created asset
  */
  public String createAsset(ImporterContext ctx, ValueMap values, String productPath) throws Exception;

  /**
  * Creates a category from the given values.
  * @param ctx           The importer context
  * @param values        The category's properties
  * @param parentPath    Path of parent category or base path of import in case of root category
  * @return Path of created category
  */
  public String createCategory(ImporterContext ctx, ValueMap values, String parentCategoryPath) throws Exception;
}
```

사용자 지정 핸들러를 가져오기에서 인식하려면 값이 0보다 큰 `service.ranking`속성을 지정해야 합니다.예를 들면 다음과 같습니다.

```java
@Component
@Service
@Property(name = "service.ranking", value = 100)
public class MyImportHandler extends DefaultImportHandler
{
...
}
```
