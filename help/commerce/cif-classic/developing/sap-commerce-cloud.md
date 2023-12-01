---
title: SAP Commerce Cloud를 사용하여 개발
description: SAP Commerce Cloud 통합 프레임워크는 API와 통합 계층을 포함합니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
exl-id: b3de1a4a-f334-44bd-addc-463433204c99
source-git-commit: 5e56441d2dc9b280547c91def8d971e7b1dfcfe3
workflow-type: tm+mt
source-wordcount: '2288'
ht-degree: 1%

---

# SAP Commerce Cloud를 사용하여 개발 {#developing-with-sap-commerce-cloud}

>[!NOTE]
>
>eCommerce 프레임워크는 모든 eCommerce 솔루션에서 사용할 수 있습니다. 여기에서 다루는 특정 세부 사항 및 예는 다음을 참조하십시오. [hybris](https://www.sap.com/products/crm.html) 해결책.

통합 프레임워크는 API와의 통합 계층을 포함합니다. 이렇게 하면 다음 작업을 수행할 수 있습니다.

* eCommerce 시스템에 연결하고 제품 데이터를 Adobe Experience Manager(AEM)로 가져옵니다

* 특정 eCommerce 엔진과 독립적인 상거래 기능을 위한 AEM 구성 요소 빌드

![chlimage_1-11](/help/sites-developing/assets/chlimage_1-11a.png)

>[!NOTE]
>
>[API 설명서](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) 을 사용할 수도 있습니다.

통합 레이어를 사용할 수 있도록 몇 가지 기본 AEM 구성 요소가 제공됩니다. 현재는 다음과 같습니다.

* 제품 표시 구성 요소
* 장바구니
* 체크아웃

검색의 경우 AEM 검색, 전자 상거래 시스템의 검색, 서드파티 검색 또는 이들의 조합을 사용할 수 있는 통합 후크가 제공됩니다.

## 전자 상거래 엔진 선택 {#ecommerce-engine-selection}

eCommerce 프레임워크는 모든 eCommerce 솔루션에서 사용할 수 있으며, 사용되는 엔진은 AEM에서 식별해야 합니다.

* 전자 상거래 엔진은 다음을 지원하는 OSGi 서비스입니다. `CommerceService` 인터페이스

   * 엔진은 다음을 통해 구별될 수 있습니다. `commerceProvider` 서비스 속성

* AEM 지원 `Resource.adaptTo()` 대상 `CommerceService` 및 `Product`

   * 다음 `adaptTo` 구현에서 다음을 찾습니다. `cq:commerceProvider` 리소스의 계층 구조에 있는 속성:

      * 검색되면 이 값을 사용하여 상거래 서비스 조회를 필터링합니다.

      * 검색되지 않는 경우, 가장 높은 등급의 상거래 서비스가 사용됩니다.

   * A `cq:Commerce` mixin을 사용하여 `cq:commerceProvider` 강력한 형식의 리소스에 추가할 수 있습니다.

* 다음 `cq:commerceProvider` 속성을 사용하여 해당 상거래 공장 정의를 참조할 수도 있습니다.

   * 예: `cq:commerceProvider` 값이 있는 속성 `hybris` 에 대한 OSGi 구성과 관련이 있습니다. **Day CQ Commerce Factory for Hybris** (com.adobe.cq.commerce.hybris.impl.HybrisServiceFactory) - 매개 변수 `commerceProvider` 값도 있습니다. `hybris`.

   * 여기에서 추가 속성, 예: **카탈로그 버전** 를 구성할 수 있습니다(적절한 경우 사용 가능).

아래 예를 참조하십시오.

| `cq:commerceProvider = geometrixx` | 표준 AEM 설치에서 특정 구현이 필요합니다. 예를 들어 일반 API에 대한 최소 확장을 포함하는 Geometrixx 예입니다 |
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
>CRXDE Lite을 사용하면 hybris 구현을 위한 제품 구성 요소에서 이 문제가 어떻게 처리되는지 확인할 수 있습니다.
>
>`/apps/geometrixx-outdoors/components/hybris/product/product.jsp`

### hybris용 개발 4 {#developing-for-hybris}

Hybris 4와의 이전 버전과의 호환성을 유지하면서 Hybris 5를 지원하도록 eCommerce Integration Framework의 hybris 확장이 업데이트되었습니다.

코드의 기본 설정은 Hybris 5에 대해 조정됩니다.

Hybris 4에 대해 개발하려면 다음이 필요합니다.

* Maven을 호출할 때 다음 명령줄 인수를 명령에 추가합니다.

  `-P hybris4`

  사전 구성된 Hybris 4 배포를 다운로드하고 번들에 임베드합니다 `cq-commerce-hybris-server`.

* OSGi 구성 관리자에서:

   * 기본 응답 파서 서비스에 대한 Hybris 5 지원을 사용하지 않도록 설정합니다.

   * Hybris Basic Authentication Handler 서비스의 서비스 순위가 Hybris OAuth Handler 서비스의 서비스 순위보다 낮은지 확인합니다.

### 세션 처리 {#session-handling}

hybris는 사용자 세션을 사용하여 고객의 장바구니와 같은 정보를 저장합니다. 의 hybris에서 세션 ID가 반환됩니다. `JSESSIONID` hybris에 대한 후속 요청 시 전송해야 하는 쿠키입니다. 저장소에 세션 ID를 저장하지 않도록 하기 위해 쇼퍼의 브라우저에 저장된 다른 쿠키에 인코딩됩니다. 다음 단계를 수행합니다.

* 첫 번째 요청에서 구매자의 요청에 쿠키가 설정되지 않으므로 세션을 만들도록 hybris 인스턴스에 요청이 전송됩니다.

* 세션 쿠키는 응답에서 추출되고 새 쿠키로 인코딩됩니다(예: `hybris-session-rest`)을 설정하고 쇼핑객에 대한 응답을 설정합니다. 원래 쿠키는 특정 경로에 대해서만 유효하고, 그렇지 않으면 후속 요청에서 브라우저에서 다시 전송되지 않으므로 새 쿠키의 인코딩이 필요합니다. 경로 정보를 쿠키 값에 추가해야 합니다.

* 이후 요청에서 쿠키는 `hybris-session-<*xxx*>` hybris에서 데이터를 요청하는 데 사용되는 HTTP 클라이언트에 설정된 쿠키입니다.

>[!NOTE]
>
>원래 세션이 더 이상 유효하지 않을 때 새로운 익명 세션이 만들어집니다.

#### Commerce 세션 {#commercesession}

* 이 세션은 다음을 &quot;소유&quot;합니다. **장바구니**

   * 추가/제거/등 수행

   * 장바구니에서 다양한 계산을 수행합니다.

     `commerceSession.getProductPrice(Product product)`

* 다음 소유 *저장소 위치* 대상: **주문** 데이터

  `CommerceSession.getUserContext()`

* 다음 소유 **결제** 연결 처리 중

* 다음 소유 **이행** 연결

### 제품 동기화 및 게시 {#product-synchronization-and-publishing}

하이브리드에서 유지 관리되는 제품 데이터는 AEM에서 사용할 수 있어야 합니다. 다음 메커니즘이 구현되었습니다.

* ID의 초기 로드는 hybris에서 피드로 제공됩니다. 이 피드에 업데이트가 있을 수 있습니다.
* hybris는 피드(AEM이 폴링함)를 통해 업데이트 정보를 제공합니다.
* AEM은 제품 데이터를 사용할 때 현재 데이터에 대한 요청을 다시 hybris로 보냅니다(마지막 수정 날짜를 사용하는 조건부 get 요청).
* Hybris에서는 선언적 방식으로 피드 콘텐츠를 지정할 수 있습니다.
* 피드 구조를 AEM 콘텐츠 모델에 매핑하면 AEM 측의 피드 어댑터에서 수행됩니다.

![chlimage_1-12](/help/sites-developing/assets/chlimage_1-12a.png)

* 가져오기(b)는 카탈로그용 AEM에서 페이지 트리 구조의 초기 설정에 사용됩니다.
* hybris의 카탈로그 변경 사항은 피드를 통해 AEM에 표시된 다음 AEM으로 전파됩니다(b)

   * 카탈로그 버전에 대한 제품 추가/삭제/변경.

   * 제품이 승인되었습니다.

* hybris 확장은 지정된 간격(예: 간격이 초 단위로 지정된 경우 24시간마다)으로 AEM에 변경 사항을 가져오도록 구성할 수 있는 폴링 가져오기(&quot;hybris&quot; 체계&quot;)를 제공합니다.

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

* AEM의 카탈로그 구성은 을 인식합니다 **스테이징됨** 및 **온라인** 카탈로그 버전.

* 카탈로그 버전 간의 제품 동기화를 사용하려면 해당 AEM 페이지의 활성화 또는 비활성화가 필요합니다(a, c)

   * 에 제품 추가 **온라인** 카탈로그 버전을 사용하려면 제품 페이지를 활성화해야 합니다.

   * 제품을 제거하려면 비활성화해야 합니다.

* AEM (c)에서 페이지를 활성화하려면 확인 (b)이 필요하며, 다음 경우에만 가능합니다.

   * 제품이 다음 위치에 있습니다. **온라인** 제품 페이지의 카탈로그 버전.

   * 참조된 제품은에서 사용할 수 있습니다 **온라인** 다른 페이지(예: 캠페인 페이지)의 카탈로그 버전.

* 활성화된 제품 페이지는 제품 데이터의 **온라인** 버전 (d).

* AEM Publish 인스턴스를 사용하려면 제품 및 개인화된 데이터(d)를 검색하기 위해 hybris에 액세스해야 합니다.

### 아키텍처 {#architecture}

#### 제품 및 변형 아키텍처 {#architecture-of-product-and-variants}

단일 제품에는 여러 변형이 있을 수 있습니다. 예를 들어 색상 및/또는 크기에 따라 달라질 수 있습니다. 제품은 변형을 유도하는 속성을 정의해야 합니다. Adobe 용어는 다음과 같습니다 *변형 축*.

그러나 모든 속성이 변형 축인 것은 아닙니다. 변형은 다른 속성에도 영향을 줄 수 있습니다. 예를 들어 가격은 크기에 따라 달라질 수 있습니다. 이러한 속성은 구매자가 선택할 수 없으므로 변형 축으로 간주되지 않습니다.

각 제품 및/또는 변형은 리소스로 표시되므로 1:1을 저장소 노드에 매핑합니다. 특정 제품 및/또는 변형이 해당 경로에 의해 고유하게 식별될 수 있다는 것이 중요합니다.

제품/변형 리소스에 실제 제품 데이터가 항상 있는 것은 아닙니다. 다른 시스템에 보관된 데이터(예: hybris)를 나타냅니다. 예를 들어 제품 설명 및 요금은 AEM에 저장되지 않고 eCommerce 엔진에서 실시간으로 검색됩니다.

모든 제품 리소스는 `Product API`. 제품 API의 대부분의 호출은 변형별로 다르지만(변형이 상위 항목에서 공유 값을 상속할 수 있음), 변형 세트를 나열하는 호출도 있습니다( `getVariantAxes()`, `getVariants()`등).

>[!NOTE]
>
>사실상 변형 축은 무엇에 의해서든 결정됩니다 `Product.getVariantAxes()` 반환:
>* hybris는 hybris 구현에 대해 이를 정의합니다.
>
>제품(일반적으로)에는 여러 변형 축이 있을 수 있지만 기본 제품 구성 요소는 다음 두 가지 요소만 처리합니다.
>
>1. `size`
>
>1. + 개 더
>
>이 추가 변형은 `variationAxis` 제품 참조의 속성(일반적으로 `color` Geometrixx Outdoors).

#### 제품 참조 및 제품 데이터 {#product-references-and-product-data}

일반적으로 제품 데이터는 아래에 있습니다. `/etc`, 및 제품 참조 `/content`.

제품 변형과 제품 데이터 노드 사이에 1:1 맵이 있어야 합니다.

제품 참조에는 표시된 각 변형에 대한 노드도 있어야 하지만, 모든 변형을 표시할 필요는 없습니다. 예를 들어 제품에 S, M, L 변형이 있는 경우 제품 데이터는 다음과 같을 수 있습니다.

```shell
etc
|──commerce
|  |──products
|     |──shirt
|       |──shirt-s
|       |──shirt-m
|       |──shirt-l
```

반면 &quot;Big and Tall&quot; 카탈로그는 다음 항목만 포함할 수 있습니다.

```shell
content
|──big-and-tall
|  |──shirt
|     |──shirt-l
```

마지막으로 제품 데이터를 사용할 필요가 없습니다. 모든 제품 데이터를 카탈로그의 참조 아래에 배치할 수 있지만, 모든 제품 데이터를 복제하지 않으면 여러 개의 카탈로그를 가질 수 없습니다.

**API**

#### com.adobe.cq.commerce.api.Product 인터페이스 {#com-adobe-cq-commerce-api-product-interface}

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

#### com.adobe.cq.commerce.api.VariantFilter  {#com-adobe-cq-commerce-api-variantfilter}

```java
/**
 * Interface for filtering variants and AxisFilter provided as common implementation
 *
 * The <code>VariantFilter</code> is used to filter variants,
 * for example, when using {@link Product#getVariants(VariantFilter filter)}.
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

* **일반 저장 메커니즘**

   * 제품 노드는 `nt:unstructured`.

   * 제품 노드는 다음 중 하나일 수 있습니다.

      * 제품 데이터가 다른 곳에 저장된 참조:

         * 제품 참조에 `productData` 제품 데이터를 가리키는 속성(일반적으로 `/etc/commerce/products`).

         * 제품 데이터는 계층적입니다. 제품 속성은 제품 데이터 노드의 상위 항목에서 상속됩니다.

         * 제품 참조에는 제품 데이터에 지정된 속성을 재정의하는 로컬 속성도 포함될 수 있습니다.

      * 제품 자체:

         * 없이 `productData` 속성.

         * 모든 속성을 로컬로 보유하는(productData 속성을 포함하지 않는) 제품 노드는 자체 상위 항목에서 직접 제품 속성을 상속합니다.

* **AEM 일반 제품 구조**

   * 각 변형에는 자체 리프 노드가 있어야 합니다.

   * 제품 인터페이스는 제품 및 변형을 모두 나타내지만 관련 저장소 노드는 제품 및 변형에 대해 구체적입니다.

   * 제품 노드는 제품 속성 및 변형 축에 대해 설명합니다.

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

#### 장바구니의 아키텍처 {#architecture-of-the-shopping-cart}

**구성 요소**

* 장바구니 소유자는 `CommerceSession:`

   * 다음 `CommerceSession` 추가 또는 제거 등을 수행합니다.
   * 다음 `CommerceSession` 또한 장바구니에서 다양한 계산을 수행합니다. &quot;

* 직접 장바구니와 관련되지 않는 `CommerceSession` 은(는) 가격표를 소유하므로 카탈로그 가격 정보도 제공해야 합니다.

   * 가격책정에는 다음과 같은 몇 가지 수정자가 있을 수 있습니다.

      * 수량 할인.
      * 다른 통화.
      * 부가세 부담 및 부가세 무료.

   * 수정자는 다음 인터페이스로 끝이 열립니다.

      * `int CommerceSession.getQuantityBreakpoints(Product product)`
      * `String CommerceSession.getProductPrice(Product product)`

**스토리지**

* 스토리지

   * hybris의 경우 hybris 서버는 장바구니를 소유합니다.
   * AEM의 경우 의 장바구니는에 저장됩니다. [ClientContext](/help/sites-administering/client-context.md).

**개인화**

* 다음을 통해 항상 개인화 촉진 [ClientContext](/help/sites-administering/client-context.md).
* ClientContext `/version/` 의 장바구니가 모든 경우에 만들어집니다.

   * 제품을 추가하려면 `CommerceSession.addCartEntry()` 메서드를 사용합니다.

* 다음은 ClientContext 장바구니에 있는 장바구니 정보의 예를 보여줍니다.

![chlimage_1-13](/help/sites-developing/assets/chlimage_1-13a.png)

#### 체크아웃 아키텍처 {#architecture-of-checkout}

**장바구니 및 주문 데이터**

다음 `CommerceSession` 은(는) 다음 세 가지 요소를 소유합니다.

1. 장바구니 콘텐츠
1. 가격 책정
1. 주문 세부 사항

1. **장바구니 콘텐츠**

   장바구니 콘텐츠 스키마는 API에 의해 수정됩니다.

   ```java
   public void addCartEntry(Product product, int quantity);
   public void modifyCartEntry(int entryNumber, int quantity);
   public void deleteCartEntry(int entryNumber);
   ```

1. **가격 책정**

   가격 책정 스키마도 API에 의해 수정됩니다.

   ```java
   public String getCartPreTaxPrice();
   public String getCartTax();
   public String getCartTotalPrice();
   public String getOrderShipping();
   public String getOrderTotalTax();
   public String getOrderTotalPrice();
   ```

1. **주문 세부 사항**

   하지만 주문 세부 사항은 다음과 같습니다 *아님* api에 의해 수정됨:

   ```java
   public void updateOrderDetails(Map<String, String> orderDetails);
   public Map<String, String> getOrderDetails();
   public void submitOrder();
   ```

**운송 계산**

* 주문 양식에는 종종 여러 배송 옵션(및 가격)이 있어야 합니다.
* 가격은 중량 및/또는 배송 주소와 같은 품목 및 주문 세부 사항을 기반으로 할 수 있습니다.
* 다음 `CommerceSession` 은 모든 종속성에 액세스할 수 있으므로 제품 가격과 유사한 방식으로 처리할 수 있습니다.

   * 다음 `CommerceSession` 배송 가격을 소유합니다.
   * 을 사용하여 게재 세부 사항을 검색/업데이트할 수 있습니다. `updateOrder(Map<String, Object> delta)`

>[!NOTE]
>
>예를 들어 배송 선택기를 구현할 수 있습니다.
>
>`yourProject/commerce/components/shippingpicker`:
>
>* 기본적으로 이는 `foundation/components/form/radio`에 대한 콜백이 있는 `CommerceSession` 대상:
>
>* 메서드를 사용할 수 있는지 확인
>* 가격 정보 추가
>* 관련 정보를 노출할 수 있는 제어권을 계속 보유하면서 구매자가 AEM에서 주문 페이지(운송 방법의 상위 집합과 이를 설명하는 텍스트 포함)를 업데이트할 수 있도록 합니다 `CommerceSession` 정보.

**결제 처리**

* 다음 `CommerceSession` 또한 결제 처리 연결도 소유합니다.

* 구현자는 선택한 결제 처리 서비스에 특정 호출을 추가해야 합니다. `CommerceSession` 구현.

**주문 이행**

* 다음 `CommerceSession` 이행 연결도 소유합니다.
* 구현자는 선택한 결제 처리 서비스에 특정 호출을 추가해야 합니다. `CommerceSession` 구현.

### 검색 정의 {#search-definition}

표준 서비스 API 모델에 따라 eCommerce 프로젝트는 개별 상거래 엔진에서 구현할 수 있는 검색 관련 API 세트를 제공합니다.

>[!NOTE]
>
>현재는 hybris 엔진만 검색 API를 즉시 구현합니다.
>
>그러나 검색 API는 일반적이며 각 CommerceService에서 개별적으로 구현할 수 있습니다.

eCommerce 프로젝트는에 기본 검색 구성 요소가 포함되어 있습니다.

`/libs/commerce/components/search`

![chlimage_1-14](/help/sites-developing/assets/chlimage_1-14a.png)

검색 API를 사용하여 선택한 상거래 엔진을 쿼리합니다(참조). [전자 상거래 엔진 선택](#ecommerce-engine-selection)):

#### 검색 API {#search-api}

핵심 프로젝트에서 제공하는 몇 가지 일반/도우미 클래스가 있습니다.

1. `CommerceQuery`

   검색 쿼리에 대해 설명합니다(쿼리 텍스트, 현재 페이지, 페이지 크기, 정렬 및 선택한 패싯에 대한 정보를 포함합니다). 검색 API를 구현하는 모든 전자 상거래 서비스는 이 클래스의 인스턴스를 수신하여 검색을 수행합니다. A `CommerceQuery` 은 요청 개체에서 인스턴스화할 수 있습니다( `HttpServletRequest`).

1. `FacetParamHelper`

   하나의 정적 메서드를 제공하는 유틸리티 클래스입니다. `toParams` - 를 생성하는 데 사용됩니다. `GET` 패싯 및 전환된 하나의 값 목록의 매개 변수 문자열. 이 기능은 사용자가 하이퍼링크를 클릭할 때 해당 값이 전환되도록 각 패싯의 각 값에 대한 하이퍼링크를 표시해야 하는 UI 측면에서 유용합니다. 즉, 이 옵션을 선택하면 쿼리에서 제거되고 그렇지 않으면 추가됩니다. 이는 여러/단일 값 패싯을 처리하고 값을 재정의하는 등의 모든 논리를 처리합니다.

검색 API의 진입점은 입니다. `CommerceService#search` 를 반환하는 메서드 `CommerceResult` 개체. 다음을 참조하십시오. [API 설명서](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) 을 참조하십시오.

### 사용자 통합 {#user-integration}

AEM과 다양한 eCommerce 시스템 간에 통합이 제공됩니다. 이를 위해서는 AEM 관련 코드만 AEM에 대해 알고 있고 이와 반대로 알 수 있도록 다양한 시스템 간에 쇼핑객을 동기화하는 전략이 필요합니다.

* 인증

  AEM은 *전용* 웹 프런트엔드를 통한 성능 향상 *모두* 인증.

* Hybris의 계정

  AEM은 각 쇼핑객에 대해 hybris에 해당 (하위) 계정을 만듭니다. 이 계정의 사용자 이름은 AEM 사용자 이름과 같습니다. 암호화 임의 암호는 AEM에서 자동 생성되고 저장(암호화)됩니다.

#### 기존 사용자 {#pre-existing-users}

AEM 프론트 엔드는 기존 hybris 구현 앞에 위치할 수 있습니다. 또한 기존 AEM 설치에 hybris 엔진을 추가할 수 있습니다. 이렇게 하려면 시스템에서 다음 두 시스템 중 하나에서 기존 사용자를 정상적으로 처리할 수 있어야 합니다.

* AEM -> hybris

   * hybris에 로그인할 때 AEM 사용자가 없는 경우:

      * 암호학적으로 무작위 암호를 사용하여 hybris 사용자 만들기
      * AEM 사용자의 사용자 디렉토리에 hybris 사용자 이름을 저장합니다.

   * 자세한 내용은: `com.adobe.cq.commerce.hybris.impl.HybrisSessionImpl#login()`

* hybris -> AEM

   * AEM에 로그인할 때 시스템에서 사용자를 인식하는 경우:

      * 제공된 사용자 이름/pwd로 hybris에 로그인 시도
      * 성공하면 동일한 암호로 AEM에서 사용자를 만듭니다(AEM 특정 솔트 결과로 AEM 특정 해시가 표시됨).

   * 위의 알고리즘은 Sling으로 구현됩니다 `AuthenticationInfoPostProcessor`

      * 자세한 내용은: `com.adobe.cq.commerce.hybris.impl.user.LazyUserImporter.java`

### 가져오기 프로세스 사용자 정의 {#customizing-the-import-process}

기존 기능을 기반으로 사용자 정의 가져오기 핸들러를 빌드하려면:

* 을(를) 구현해야 함 `ImportHandler` 인터페이스

* 를 확장할 수 있습니다. `DefaultImportHandler`.

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
  * @param parentPath    Path of parent category or base path of import if there is a root category
  * @return Path of created category
  */
  public String createCategory(ImporterContext ctx, ValueMap values, String parentCategoryPath) throws Exception;
}
```

사용자 지정 처리기를 가져오기가 인식하도록 하려면 사용자 지정 처리기에 `service.ranking`값이 0보다 큰 속성(예: )

```java
@Component
@Service
@Property(name = "service.ranking", value = 100)
public class MyImportHandler extends DefaultImportHandler
{
...
}
```
