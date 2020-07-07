---
title: 개발(일반)
seo-title: 개발(일반)
description: 통합 프레임워크에는 API와 통합 레이어가 포함되어 있으므로 eCommerce 기능을 위한 AEM 구성 요소를 빌드할 수 있습니다
seo-description: 통합 프레임워크에는 API와 통합 레이어가 포함되어 있으므로 eCommerce 기능을 위한 AEM 구성 요소를 빌드할 수 있습니다
uuid: 393bb28a-9744-44f4-9796-09228fcd466f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
discoiquuid: d8ee3b57-633a-425e-bf36-646f0e0bad52
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '1886'
ht-degree: 0%

---


# 개발(일반){#developing-generic}

>[!NOTE]
>
>[API 설명서도](/help/sites-developing/ecommerce.md#api-documentation) 사용할 수 있습니다.

통합 프레임워크에는 API와 통합 레이어가 포함되어 있습니다. 이렇게 하면 특정 eCommerce 엔진과는 상관없이 eCommerce 기능용 AEM 구성 요소를 빌드할 수 있습니다. 또한 내부 CRX 데이터베이스를 사용하거나 eCommerce 시스템을 연결하고 제품 데이터를 AEM에 가져올 수 있습니다.

통합 레이어를 사용할 수 있도록 특별히 제공되는 다양한 AEM 구성 요소가 제공됩니다. 현재 다음과 같습니다.

* 제품 표시 구성 요소
* 장바구니
* 홍보 및 바우처
* 카탈로그 및 섹션 블루프린트
* 체크아웃
* 검색

AEM 검색, 타사 검색(예: Search&amp;Promote) 또는 이들의 조합을 사용할 수 있도록 해주는 통합 후크가 제공됩니다.

## 전자 상거래 엔진 선택 {#ecommerce-engine-selection}

eCommerce 프레임워크를 모든 eCommerce 솔루션에서 사용할 수 있습니다. AEM 범용 엔진을 사용하는 경우에도 사용되는 엔진을 AEM에서 식별해야 합니다.

* eCommerce Engine은 인터페이스를 지원하는 OSGi `CommerceService` 서비스입니다

   * 엔진은 `commerceProvider` 서비스 속성으로 식별할 수 있습니다.

* AEM은 `Resource.adaptTo()` `CommerceService` 및 `Product`

   * 구현은 리소스 계층 구조에서 `adaptTo` `cq:commerceProvider` 속성을 찾습니다.

      * 검색된 경우 이 값은 커머스 서비스 조회를 필터링하는 데 사용됩니다.
      * 찾을 수 없으면 가장 높은 등급의 커머스 서비스가 사용됩니다.
   * 혼합을 `cq:Commerce` 사용하여 강력한 형식의 리소스에 추가할 `cq:commerceProvider` 수 있습니다.


* 이 `cq:commerceProvider` 속성은 적절한 상거래 공장 정의를 참조하는 데에도 사용됩니다.

   * 예를 들어 geometrixx 값이 있는 `cq:commerceProvider` 속성은 Geometrixx-Outdoors **(** )의`com.adobe.cq.commerce.hybris.impl.GeoCommerceServiceFactory`Day CQ Commerce Factory에 대한 OSGi 구성에 상관 관계를 설정하며 매개 변수에도 값이 `commerceProvider` 있습니다 `geometrixx`.
   * 여기에서 추가 속성을 구성할 수 있습니다(해당되는 경우 및 사용 가능).

표준 AEM 설치에서는 다음과 같은 특정 구현이 필요합니다.

|  |  |
|---|---|
| `cq:commerceProvider = geometrixx` | geometrixx 예; 여기에는 일반 API에 대한 최소한의 익스텐션이 포함됩니다. |

### 예 {#example}

```shell
/etc/commerce/products/geometrixx-outdoors
+ cq:commerceProvider = geometrixx
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
>CRXDE Lite를 사용하면 AEM 일반 구현의 제품 구성 요소에서 이 문제가 어떻게 처리되는지 확인할 수 있습니다.
>
>`/apps/geometrixx-outdoors/components/product`

### 세션 처리 {#session-handling}

고객의 장바구니와 관련된 정보를 저장하는 세션입니다.

CommerceSession ****:

* 장바구니 **소유**

   * 추가/제거/기타
   * 장바구니에서 다양한 계산을 수행합니다.

      `commerceSession.getProductPriceInfo(Product product, Predicate filter)`

* 주문 **데이터의 지속** 소유:

   `CommerceSession.getUserContext()`

* 다음을 사용하여 배달 세부 정보를 검색/업데이트할 수 있습니다. `updateOrder(Map<String, Object> delta)`
* 또한 **결제** 처리 연결을 소유합니다.
* 주문 처리 **연결도** 소유

### 아키텍처 {#architecture}

#### 제품 및 변형의 구조 {#architecture-of-product-and-variants}

단일 제품에는 여러 변수가 있을 수 있습니다. 예를 들어 색상 및/또는 크기마다 다를 수 있습니다. 제품은 어떤 속성을 통해 변화를 이끌어내는지 정의해야 합니다. 우리는 이 *변형 도끼를*&#x200B;말합니다.

그러나 일부 속성이 변형 축은 아닙니다. 변형은 다른 속성에도 영향을 줄 수 있습니다. 예를 들어 가격이 크기에 따라 달라질 수 있습니다. 이러한 속성은 구매자가 선택할 수 없으므로 변형 축으로 간주되지 않습니다.

각 제품 및/또는 변형은 리소스로 표현되므로 저장소 노드에 1:1을 매핑합니다. 특정 제품 및/또는 변형이 해당 경로로 고유하게 식별될 수 있다는 것은 필연입니다.

모든 제품 리소스는 한 가지 방법으로 나타낼 수 있습니다 `Product API`. 제품 API의 대부분의 호출은 변형이 고유하지만(변형이 조상에서 공유 값을 상속할 수 있음), 변형 집합(, `getVariantAxes()``getVariants()`등)을 나열하는 호출도 있습니다.

>[!NOTE]
>
>변형 축은 반환되는 모든 것에 의해 `Product.getVariantAxes()` 결정됩니다.
>
>* 일반 구현의 경우 AEM은 제품 데이터( `cq:productVariantAxes`)의 속성에서 이를 읽습니다.
>
>
제품(일반적으로)은 많은 변형 축을 가질 수 있지만, 기본적으로 제공되는 제품 구성 요소는 두 개만 처리합니다.
>
>1. `size`
>1. 하나 더

>
>   
이 추가 변형은 제품 참조의 `variationAxis` 속성을 통해 선택됩니다(일반적으로 Geometrixx Outdoors `color` ).

#### 제품 참조 및 PIM 데이터 {#product-references-and-pim-data}

일반적으로:

* PIM 데이터가 `/etc`

* 제품 참조 `/content`자료

제품 변형과 제품 데이터 노드 간에는 1:1 맵이 있어야 합니다.

제품 참조에도 제시된 각 변형에 대한 노드가 있어야 하지만 모든 변형을 제시할 필요는 없습니다. 예를 들어 제품에 S, M, L 변형이 있는 경우 제품 데이터는 다음과 같습니다.

```shell
etc
  commerce
    products
      shirt
        shirt-s
        shirt-m
        shirt-l
```

&quot;크고 긴&quot; 카탈로그에는 다음이 있을 수 있습니다.

```shell
content
  big-and-tall
    shirt
      shirt-l
```

마지막으로 제품 데이터를 사용할 필요가 없습니다. 카탈로그의 참조 아래에 모든 제품 데이터를 배치할 수 있습니다. 그러나 제품 데이터를 모두 복제하지 않으면 여러 카탈로그를 만들 수 없습니다.

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

#### com.adobe.cq.commerce.api.VariantFilter  {#com-adobe-cq-commerce-api-variantfilter}

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

   * 제품 노드는 구조화되지 않습니다.
   * 제품 노드는 다음 중 하나일 수 있습니다.

      * 제품 데이터가 다른 곳에 저장되는 참조:

         * 제품 참조에는 제품 데이터(일반적으로 아래)를 가리키는 `productData` 속성이 `/etc/commerce/products`포함됩니다.
         * 제품 데이터는 계층적입니다. 제품 속성은 제품 데이터 노드의 상위 항목에서 상속됩니다.
         * 제품 참조에는 제품 데이터에 지정된 속성을 재정의하는 로컬 속성이 포함될 수도 있습니다.
      * 제품 자체:

         * 속성 `productData` 이 없습니다.
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

#### 장바구니 구조 {#architecture-of-the-shopping-cart}

**구성 요소**

* 장바구니는 `CommerceSession:`

   * 이 `CommerceSession` 작업은 추가, 제거 등을 수행합니다.
   * 또한 장바구니에서 다양한 계산을 `CommerceSession` 수행합니다.
   * 또한 `CommerceSession` 장바구니에 실행된 바우처 및 프로모션을 적용합니다.

* 직접 장바구니와 관련되지 않지만, 가격 정보를 카탈로그 가격 정보도 `CommerceSession` 제공해야 합니다(가격은 소유).

   * 가격에 몇 개의 수정자가 있을 수 있습니다.

      * 수량 할인.
      * 다른 통화.
      * VAT 및 VAT 별도
   * 수정자는 다음 인터페이스로 완전히 열린 것입니다.

      * `int CommerceSession.getQuantityBreakpoints(Product product)`
      * `String CommerceSession.getProductPrice(Product product)`


**저장 용량**

* 저장 용량

   * AEM 범용 케이스 카트는 ClientContext에 [저장됩니다](/help/sites-administering/client-context.md)

**개인화**

* 개인화는 항상 [ClientContext를 통해 구현되어야 합니다](/help/sites-administering/client-context.md).
* 장바구니 `/version/` 의 ClientContext는 모든 경우에 만들어집니다.

   * 제품은 `CommerceSession.addCartEntry()` 방법을 사용하여 추가해야 합니다.

* 다음은 ClientContext 장바구니에 있는 장바구니 정보의 예를 보여 줍니다.

![chlimage_1-33](assets/chlimage_1-33a.png)

#### 체크아웃 아키텍처 {#architecture-of-checkout}

**장바구니 및 주문 데이터**

The `CommerceSession` owner the three elements:

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

   그러나 주문 세부 사항은 API에서 *고정되지* 않습니다.

   ```java
       public void updateOrderDetails(Map<String, String> orderDetails);
       public Map<String, String> getOrderDetails();
       public void submitOrder();
   ```

**배송 계산**

* 주문 양식에는 여러 배송 옵션(및 가격)이 필요합니다.
* 가격은 중량 및/또는 배달 주소와 같은 주문 및 세부 사항에 따라 책정될 수 있습니다.
* Adobe `CommerceSession` 는 모든 종속성에 액세스할 수 있으므로 다음과 같이 제품 가격과 유사한 방식으로 처리할 수 있습니다.

   * 운송 가격을 `CommerceSession` 소유합니다.
   * 배달 세부 사항 `updateOrder(Map<String, Object> delta)` 을 검색/업데이트하는 데 사용합니다.

### 검색 정의 {#search-definition}

표준 서비스 API 모델에 따라 eCommerce 프로젝트는 개별 상거래 엔진에서 구현할 수 있는 검색 관련 API 집합을 제공합니다.

>[!NOTE]
>
>현재 hybris 엔진만이 즉시 검색 API를 구현합니다.
>
>그러나 검색 API는 일반적이며 각 CommerceService에서 개별적으로 구현할 수 있습니다.
>
>따라서 기본적으로 제공되는 일반 구현은 이 API를 구현하지 않지만, API를 확장하고 검색 기능을 추가할 수 있습니다.

eCommerce 프로젝트에는 다음과 같은 기본 검색 구성 요소가 포함되어 있습니다.

`/libs/commerce/components/search`

![chlimage_1-34](assets/chlimage_1-34a.png)

이렇게 하면 검색 API를 사용하여 선택한 상거래 엔진을 쿼리할 수 있습니다( [eCommerce Engine 선택 참조](#ecommerce-engine-selection)).

#### 검색 API {#search-api}

핵심 프로젝트에서 제공하는 몇 가지 일반/도우미 클래스가 있습니다.

1. `CommerceQuery`

   검색 쿼리를 설명하는 데 사용됩니다(쿼리 텍스트, 현재 페이지, 페이지 크기, 정렬 및 선택한 패싯에 대한 정보 포함). 검색 API를 구현하는 모든 eCommerce 서비스는 검색을 수행하기 위해 이 클래스의 인스턴스를 수신합니다. 요청 개체()에서 A를 인스턴스화할 `CommerceQuery` 수 `HttpServletRequest`있습니다.

1. `FacetParamHelper`

   패싯 목록과 전환된 값 목록에서 매개 변수 문자열 `toParams` `GET` 을 생성하는 데 사용되는 하나의 정적 메서드를 제공하는 유틸리티 클래스입니다. 이 기능은 UI에서 유용한데, 여기서 사용자가 하이퍼링크를 클릭하면 해당 값이 전환됩니다(즉, 선택한 경우에는 쿼리에서 제거되고, 그렇지 않으면 추가됨). 이는 여러/단일 값이 있는 패싯을 처리하는 모든 논리, 값 무시 등을 처리합니다.

검색 API의 시작 지점은 개체를 반환하는 `CommerceService#search``CommerceResult` 메서드입니다. 이 항목에 대한 자세한 내용은 API 설명서를 참조하십시오.

### 홍보 및 바우처 개발 {#developing-promotions-and-vouchers}

* 바우처:

   * 바우처는 웹 사이트 콘솔에서 작성/편집되고 다음 위치에 저장되는 페이지 기반 구성 요소입니다.

      `/content/campaigns`

   * 바우처 제공:

      * 바우처 코드(구매자가 장바구니에 입력).
      * 할인권 레이블(구매자가 장바구니에 입력한 후 표시됨).
      * 할인권 작업을 정의하는 프로모션 경로.
   * 바우처에는 자체 설정 및 해제 날짜/시간이 없지만 상위 캠페인의 사용 횟수가 있습니다.
   * 외부 상거래 엔진은 바우처를 제공할 수도 있습니다. 최소 요구 사항:

      * 바우처 코드
      * 메서드 `isValid()`
   * 바우처 **구성** 요소()에서 제공하는 `/libs/commerce/components/voucher`이점은 다음과 같습니다.

      * 바우처 관리를 위한 렌더러; 여기에는 현재 장바구니에 있는 모든 바우처가 표시됩니다.
      * 바우처를 관리(추가/제거)하기 위한 편집 대화 상자(양식)입니다.
      * 장바구니에 바우처를 추가/제거하는 데 필요한 작업



* 프로모션:

   * 프로모션은 웹 사이트 콘솔에서 작성/편집되고 다음 위치에 저장되는 페이지 기반 구성 요소입니다.

      `/content/campaigns`

   * 판촉 공급:

      * 우선 순위
      * 프로모션 처리기 경로
   * 판촉 행사를 캠페인에 연결하여 온/오프 날짜/시간을 정의할 수 있습니다.
   * 판촉을 경험에 연결하여 세그먼트를 정의할 수 있습니다.
   * 경험에 연결되지 않은 프로모션은 자체적인 실행은 아니지만 바우처에 의해 실행될 수 있습니다.
   * 프로모션 구성 요소( `/libs/commerce/components/promotion`)에는 다음이 포함됩니다.

      * 프로모션 관리를 위한 렌더러 및 대화 상자
      * 프로모션 핸들러와 관련된 구성 매개 변수를 렌더링하고 편집하는 하위 구성 요소
   * 두 개의 프로모션 핸들러는 기본적으로 제공됩니다.

      * `DiscountPromotionHandler`(장바구니 전체 절대 또는 백분율 할인 적용)
      * `PerfectPartnerPromotionHandler`, 파트너 제품이 장바구니에 있는 경우 제품 절대 또는 백분율 할인 적용
   * ClientContext는 세그먼트 `SegmentMgr` 를 해결하고 ClientContext는 프로모션을 `CartMgr` 해결합니다. 하나 이상의 해결된 세그먼트가 적용되는 각 프로모션은 실행됩니다.

      * 실행된 프로모션은 장바구니를 재계산하기 위해 AJAX 호출을 통해 서버로 다시 전송됩니다.
      * 실행된 판촉 행사(및 추가된 바우처)는 ClientContext 패널에도 표시됩니다.




카트에서 바우처 추가/제거는 `CommerceSession` API를 통해 수행됩니다.

```java
/**
 * Apply a voucher to this session's cart.
 *
 * @param code the voucher's code
 * @throws CommerceException
 */
public void addVoucher(String code) throws CommerceException;

/**
 * Remove a voucher that was previously added with {@link #addVoucher(String)}.
 *
 * @param code the voucher's code
 * @throws CommerceException
 */
public void removeVoucher(String code) throws CommerceException;

/**
 * Get a list of vouchers that were added to this cart via {@link #addVoucher(String)}.
 *
 * @throws CommerceException
 */
public List<Voucher> getVouchers() throws CommerceException;
```

이렇게 하면 할인권 `CommerceSession` 이 존재하는지, 적용할 수 있는지 여부를 확인할 책임이 있습니다. 특정 조건이 충족되는 경우에만 적용할 수 있는 바우처일 수 있습니다. 예를 들어 총 장바구니 가격이 $100보다 큰 경우) 어떤 이유로든 바우처를 적용할 수 없는 경우 `addVoucher` 메서드에서 예외가 발생합니다. 또한, `CommerceSession` 할인권 추가/제거 후 장바구니 가격을 업데이트할 책임이 있습니다.

The `Voucher` is a bean-like class that contains fields for:

* 바우처 코드
* 간략한 설명
* 할인 유형 및 값을 나타내는 관련 판촉 행사 참조

제공된 쿠폰이 `AbstractJcrCommerceSession` 적용될 수 있습니다. 클래스에 의해 반환되는 바우처는 다음 속성 `getVouchers()` 이 있는 jcr:content 노드를 `cq:Page` 포함하는 인스턴스입니다.

* `sling:resourceType` (문자열) - `commerce/components/voucher`

* `jcr:title` (문자열) - 할인권 설명
* `code` (문자열) - 이 바우처를 적용하려면 사용자가 입력해야 하는 코드입니다.
* `promotion` (문자열) - 적용할 판촉 행사 예: `/content/campaigns/geometrixx-outdoors/article/10-bucks-off`

프로모션 처리기는 장바구니를 수정하는 OSGi 서비스입니다. 장바구니는 `PromotionHandler` 인터페이스에 정의될 여러 개의 후크를 지원합니다.

```java
/**
 * Apply promotion to a cart line item. The method returns a discount
 * <code>PriceInfo</code> instance or <code>null</code> if no discount
 * was applied.
 * @param commerceSession The commerce session
 * @param promotion The configured promotion
 * @param cartEntry The cart line item
 * @return A discounted <code>PriceInfo</code> or <code>null</code>
 */
public PriceInfo applyCartEntryPromotion(CommerceSession commerceSession,
                                         Promotion promotion, CartEntry cartEntry)
    throws CommerceException;

/**
 * Apply promotion to an order. The method returns a discount
 * <code>PriceInfo</code> instance or <code>null</code> if no discount
 * was applied.
 * @param commerceSession The commerce session
 * @param promotion The configured promotion
 * @return A discounted <code>PriceInfo</code> or <code>null</code>
 */
public PriceInfo applyOrderPromotion(CommerceSession commerceSession, Promotion promotion)
    throws CommerceException;

public PriceInfo applyShippingPromotion(CommerceSession commerceSession, Promotion promotion)
    throws CommerceException;

/**
 * Allows a promotion handler to define a custom, author-oriented message for a promotion.
 * The {@link com.adobe.cq.commerce.common.promotion.PerfectPartnerPromotionHandler}, for instance,
 * uses this to list the qualifying pairs of products in the current cart.
 * @param commerceSession
 * @param promotion
 * @return A message to display
 * @throws CommerceException
 */
public String getMessage(SlingHttpServletRequest request, CommerceSession commerceSession, Promotion promotion) throws CommerceException;

/**
 * Informs the promotion handler that something under the promotions root has been edited, and the handler
 * should invalidate any caches it might be keeping.
 */
public void invalidateCaches();
```

세 가지 프로모션 핸들러는 기본적으로 제공됩니다.

* `DiscountPromotionHandler` 장바구니 전체 절대 또는 백분율 할인 적용
* `PerfectPartnerPromotionHandler` 제품 파트너가 장바구니에 있는 경우 제품 절대 또는 백분율 할인 적용
* `FreeShippingPromotionHandler` 무료 배송

