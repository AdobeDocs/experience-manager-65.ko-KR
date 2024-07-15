---
title: 개발(일반)
description: 통합 프레임워크는 API와의 통합 계층을 포함하므로 eCommerce 기능을 위한 AEM 구성 요소를 빌드할 수 있습니다.
contentOwner: Guillaume Carlino
exl-id: 1138a548-d112-4446-b0e1-b7a9ea7c7604
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '1856'
ht-degree: 0%

---

# 개발(일반){#developing-generic}

>[!NOTE]
>
>[API 설명서](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation)도 사용할 수 있습니다.

통합 프레임워크는 API와의 통합 계층을 포함합니다. 이를 통해 특정 eCommerce 엔진과 관계없이 eCommerce 기능을 위한 AEM 구성 요소를 빌드할 수 있습니다. 또한 내부 CRX 데이터베이스를 사용하거나 eCommerce 시스템을 연결하고 제품 데이터를 AEM으로 가져올 수 있습니다.

통합 레이어를 사용할 수 있도록 몇 가지 기본 AEM 구성 요소가 제공됩니다. 현재는 다음과 같습니다.

* 제품 표시 구성 요소
* 장바구니
* 프로모션 및 바우처
* 카탈로그 및 섹션 블루프린트
* 체크아웃
* 검색

검색의 경우 AEM(Adobe Experience Manager) 검색, 서드파티 검색 또는 이들의 조합을 사용할 수 있는 통합 후크가 제공됩니다.

## 전자 상거래 엔진 선택 {#ecommerce-engine-selection}

eCommerce 프레임워크는 모든 eCommerce 솔루션에서 사용할 수 있으며, AEM 일반 엔진을 사용하는 경우에도 사용되는 엔진을 AEM에서 식별해야 합니다.

* 전자 상거래 엔진은 `CommerceService` 인터페이스를 지원하는 OSGi 서비스입니다.

   * 엔진은 `commerceProvider` 서비스 속성으로 구분할 수 있습니다.

* AEM은 `CommerceService` 및 `Product`에 대해 `Resource.adaptTo()`을(를) 지원합니다.

   * `adaptTo` 구현은 리소스의 계층에서 `cq:commerceProvider` 속성을 찾습니다.

      * 검색되면 이 값을 사용하여 상거래 서비스 조회를 필터링합니다.
      * 검색되지 않는 경우, 가장 높은 등급의 상거래 서비스가 사용됩니다.

   * `cq:Commerce` mixin을 사용하므로 `cq:commerceProvider`을(를) 강력한 형식의 리소스에 추가할 수 있습니다.

* `cq:commerceProvider` 속성은 적절한 상거래 팩터리 정의를 참조하는 데에도 사용됩니다.

   * 예를 들어, 값이 Geometrixx인 `cq:commerceProvider` 속성은 **Day CQ Commerce Factory for Geometrixx-Outdoors**(`com.adobe.cq.commerce.hybris.impl.GeoCommerceServiceFactory`)의 OSGi 구성과 상관 관계가 있습니다. 여기서 매개 변수 `commerceProvider`은(는) 값 `geometrixx`도 가집니다.
   * 여기에서 추가 속성을 구성할 수 있습니다(적절하고 사용 가능한 경우).

표준 AEM 설치에서 특정 구현이 필요합니다. 예를 들면 다음과 같습니다.

|  |  |
|---|---|
| `cq:commerceProvider = geometrixx` | geometrixx 예제. 여기에는 일반 API에 대한 최소 확장이 포함됩니다 |

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
>CRXDE Lite을 사용하면 AEM 일반 구현의 제품 구성 요소에서 이 문제가 어떻게 처리되는지 확인할 수 있습니다.
>
>`/apps/geometrixx-outdoors/components/product`

### 세션 처리 {#session-handling}

고객의 장바구니와 관련된 정보를 저장하는 세션입니다.

**CommerceSession**:

* **장바구니** 소유

   * 추가/제거/등 수행
   * 장바구니에서 다양한 계산을 수행합니다.

     `commerceSession.getProductPriceInfo(Product product, Predicate filter)`

* **order** 데이터의 지속성을 소유합니다.

  `CommerceSession.getUserContext()`

* `updateOrder(Map<String, Object> delta)`을(를) 사용하여 게재 세부 정보를 검색/업데이트할 수 있습니다.
* **결제** 처리 연결 소유
* **이행** 연결 소유

### 아키텍처 {#architecture}

#### 제품 및 변형 아키텍처 {#architecture-of-product-and-variants}

단일 제품에는 여러 변형이 있을 수 있습니다. 예를 들어 색상 및/또는 크기에 따라 달라질 수 있습니다. 제품은 변형을 유도하는 속성을 정의해야 합니다. Adobe은 다음 *변형 축*&#x200B;을 의미합니다.

그러나 모든 속성이 변형 축인 것은 아닙니다. 변형은 다른 속성에도 영향을 줄 수 있습니다. 예를 들어 가격은 크기에 따라 달라질 수 있습니다. 이러한 속성은 구매자가 선택할 수 없으므로 변형 축으로 간주되지 않습니다.

각 제품 및/또는 변형은 리소스로 표시되므로 1:1을 저장소 노드에 매핑합니다. 특정 제품 및/또는 변형이 해당 경로에 의해 고유하게 식별될 수 있다는 것이 중요합니다.

모든 제품 리소스는 `Product API`(으)로 표시할 수 있습니다. 제품 API의 대부분의 호출은 변형별로 다르지만(변형이 상위 항목에서 공유 값을 상속할 수 있음), 변형 집합(`getVariantAxes()`, `getVariants()` 등)을 나열하는 호출도 있습니다.

>[!NOTE]
>
>사실상 변형 축은 `Product.getVariantAxes()`이(가) 반환하는 모든 것에 의해 결정됩니다.
>
>* 제네릭 구현의 경우 AEM은 제품 데이터(`cq:productVariantAxes`)의 속성에서 이를 읽습니다.
>
>제품(일반적으로)에는 여러 변형 축이 있을 수 있지만 기본 제품 구성 요소는 다음 두 가지 요소만 처리합니다.
>
>1. `size`
>1. + 개 더
>
>   이 추가 변형은 제품 참조의 `variationAxis` 속성을 통해 선택됩니다(일반적으로 Geometrixx Outdoors의 경우 `color`).

#### 제품 참조 및 PIM 데이터 {#product-references-and-pim-data}

일반적으로

* PIM 데이터는 `/etc` 아래에 있습니다.

* `/content`의 제품 참조.

제품 변형과 제품 데이터 노드 사이에 1:1 맵이 있어야 합니다.

제품 참조에는 표시된 각 변형에 대한 노드도 있어야 하지만, 모든 변형을 표시할 필요는 없습니다. 예를 들어 제품에 S, M, L 변형이 있는 경우 제품 데이터는 다음과 같을 수 있습니다.

```shell
etc
  commerce
    products
      shirt
        shirt-s
        shirt-m
        shirt-l
```

반면 &quot;Big and Tall&quot; 카탈로그는 다음 항목만 포함할 수 있습니다.

```shell
content
  big-and-tall
    shirt
      shirt-l
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

   * 제품 노드는 구조화되지 않았습니다.
   * 제품 노드는 다음 중 하나일 수 있습니다.

      * 제품 데이터가 다른 곳에 저장된 참조:

         * 제품 참조에는 제품 데이터(일반적으로 `/etc/commerce/products` 아래)를 가리키는 `productData` 속성이 있습니다.
         * 제품 데이터는 계층적입니다. 제품 속성은 제품 데이터 노드의 상위 항목에서 상속됩니다.
         * 제품 참조에는 제품 데이터에 지정된 속성을 재정의하는 로컬 속성도 포함될 수 있습니다.

      * 제품 자체:

         * `productData` 속성이 없습니다.
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

* 장바구니를 `CommerceSession:`이(가) 소유하고 있습니다.

   * `CommerceSession`은(는) 추가, 제거 등을 수행합니다.
   * `CommerceSession`은(는) 장바구니에서 다양한 계산도 수행합니다.
   * `CommerceSession`은(는) 장바구니에 실행된 바우처 및 프로모션도 적용합니다.

* 장바구니와 직접 관련되지는 않지만 `CommerceSession`은(는) 가격 정보를 소유하므로 카탈로그 가격 정보도 제공해야 합니다.

   * 가격책정에는 다음과 같은 몇 가지 수정자가 있을 수 있습니다.

      * 수량 할인.
      * 다른 통화.
      * 부가세 부담 및 부가세 무료.

   * 수정자는 다음 인터페이스로 끝이 열립니다.

      * `int CommerceSession.getQuantityBreakpoints(Product product)`
      * `String CommerceSession.getProductPrice(Product product)`

**스토리지**

* 스토리지

   * AEM 일반적인 경우 장바구니는 [ClientContext](/help/sites-administering/client-context.md)에 저장됩니다

**개인화**

* [ClientContext](/help/sites-administering/client-context.md)을 통해 항상 개인화를 촉진하십시오.
* 장바구니의 ClientContext `/version/`이(가) 모든 경우에 만들어집니다.

   * 제품은 `CommerceSession.addCartEntry()` 메서드를 사용하여 추가해야 합니다.

* 다음은 ClientContext 장바구니에 있는 장바구니 정보의 예를 보여줍니다.

![chlimage_1-33](/help/sites-developing/assets/chlimage_1-33a.png)

#### 체크아웃 아키텍처 {#architecture-of-checkout}

**장바구니 및 주문 데이터**

`CommerceSession`은(는) 다음 세 가지 요소를 소유합니다.

1. **장바구니 내용**

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

1. **주문 세부 정보**

   그러나 주문 세부 사항은 API로 수정되지 *않습니다*.

   ```java
       public void updateOrderDetails(Map<String, String> orderDetails);
       public Map<String, String> getOrderDetails();
       public void submitOrder();
   ```

**배송 계산**

* 주문 양식에는 종종 여러 배송 옵션(및 가격)이 있어야 합니다.
* 가격은 중량 및/또는 배송 주소와 같은 품목 및 주문 세부 사항을 기반으로 할 수 있습니다.
* `CommerceSession`은(는) 모든 종속성에 액세스할 수 있으므로 제품 가격과 유사한 방식으로 처리할 수 있습니다.

   * `CommerceSession`이(가) 배송 가격을 소유합니다.
   * `updateOrder(Map<String, Object> delta)`을(를) 사용하여 게재 세부 정보를 검색/업데이트하십시오.

### 검색 정의 {#search-definition}

표준 서비스 API 모델에 따라 eCommerce 프로젝트는 개별 상거래 엔진에서 구현할 수 있는 검색 관련 API 세트를 제공합니다.

>[!NOTE]
>
>현재는 hybris 엔진만 검색 API를 즉시 구현합니다.
>
>그러나 검색 API는 일반적이며 각 CommerceService에서 개별적으로 구현할 수 있습니다.
>
>따라서 기본적으로 제공되는 일반 구현은 이 API를 구현하지 않지만 이를 확장하고 검색 기능을 추가할 수 있습니다.

eCommerce 프로젝트는에 기본 검색 구성 요소가 포함되어 있습니다.

`/libs/commerce/components/search`

![chlimage_1-34](/help/sites-developing/assets/chlimage_1-34a.png)

검색 API를 사용하여 선택한 상거래 엔진을 쿼리합니다([전자 상거래 엔진 선택](#ecommerce-engine-selection) 참조).

#### 검색 API {#search-api}

핵심 프로젝트에서 제공하는 몇 가지 일반/도우미 클래스가 있습니다.

1. `CommerceQuery`

   검색 쿼리를 설명하는 데 사용됩니다(쿼리 텍스트, 현재 페이지, 페이지 크기, 정렬 및 선택한 패싯에 대한 정보가 포함됨). 검색 API를 구현하는 모든 전자 상거래 서비스는 이 클래스의 인스턴스를 수신하여 검색을 수행합니다. `CommerceQuery`은(는) 요청 개체(`HttpServletRequest`)에서 인스턴스화할 수 있습니다.

1. `FacetParamHelper`

   패싯 및 전환된 값 목록에서 `GET` 매개 변수 문자열을 생성하는 데 사용되는 정적 메서드 `toParams`을(를) 제공하는 유틸리티 클래스입니다. 이 기능은 사용자가 하이퍼링크를 클릭할 때 해당 값이 전환되도록 각 패싯의 각 값에 대한 하이퍼링크를 표시해야 하는 UI 측면에서 유용합니다. 즉, 이 필드를 선택한 경우 쿼리에서 제거되고 그렇지 않은 경우 추가됩니다. 이는 여러/단일 값 패싯을 처리하고 값을 재정의하는 등의 모든 논리를 처리합니다.

검색 API의 진입점은 `CommerceResult` 개체를 반환하는 `CommerceService#search` 메서드입니다. 이 항목에 대한 자세한 내용은 API 설명서 를 참조하십시오.

### 프로모션 및 바우처 개발 {#developing-promotions-and-vouchers}

* 바우처:

   * 바우처는 웹 사이트 콘솔로 생성/편집하고 아래에 저장되는 페이지 기반 구성 요소입니다.

     `/content/campaigns`

   * 바우처 공급:

      * 바우처 코드(구매자가 장바구니에 입력).
      * 바우처 레이블(쇼핑객이 장바구니에 입력한 후 표시됨).
      * 프로모션 경로(바우처가 적용되는 작업을 정의함).

   * 바우처는 날짜/시간 및 시간이 다르지만 부모 캠페인의 항목을 사용합니다.
   * 외부 상거래 엔진은 바우처를 제공할 수도 있습니다. 여기에는 최소 다음 항목이 필요합니다.

      * 바우처 코드
      * `isValid()` 메서드

   * **Voucher** 구성 요소(`/libs/commerce/components/voucher`)가 제공하는 항목:

      * 바우처 관리를 위한 렌더러입니다. 현재 장바구니에 있는 바우처가 표시됩니다.
      * 바우처를 관리(추가/제거)하기 위한 편집 대화 상자(양식).
      * 장바구니에서 바우처를 추가/제거하는 데 필요한 작업입니다.

* 프로모션:

   * 프로모션은 웹 사이트 콘솔로 생성/편집하고 다음 위치에 저장하는 페이지 기반 구성 요소입니다.

     `/content/campaigns`

   * 판촉 공급:

      * 우선 순위
      * 프로모션 핸들러 경로

   * 프로모션을 캠페인에 연결하여 설정/해제 날짜/시간을 정의할 수 있습니다.
   * 프로모션을 경험에 연결하여 세그먼트를 정의할 수 있습니다.
   * 경험에 연결되지 않은 프로모션은 저절로 실행되지는 않지만 바우처로 실행할 수 있습니다.
   * 승격 구성 요소(`/libs/commerce/components/promotion`)에 다음이 포함되어 있습니다.

      * 프로모션 관리용 렌더러 및 대화 상자
      * 프로모션 핸들러와 관련된 구성 매개 변수를 렌더링 및 편집하기 위한 하위 구성 요소

   * 두 개의 프로모션 핸들러가 즉시 제공됩니다.

      * `DiscountPromotionHandler`: 장바구니 전체 절대 또는 백분율 할인을 적용합니다.
      * `PerfectPartnerPromotionHandler`: 파트너 제품도 장바구니에 있는 경우 제품 절대 또는 비율 할인을 적용합니다.

   * `SegmentMgr` ClientContext이 세그먼트를 확인하고 `CartMgr` ClientContext이 프로모션을 확인합니다. 하나 이상의 해결된 세그먼트에 속하는 각 프로모션이 실행됩니다.

      * 실행된 프로모션은 AJAX 호출을 통해 서버로 다시 전송되어 장바구니를 다시 계산합니다.
      * 실행된 프로모션(및 추가된 바우처)도 ClientContext 패널에 표시됩니다.

`CommerceSession` API를 통해 장바구니에서 바우처를 추가/제거합니다.

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

이렇게 하면 `CommerceSession`이(가) 바우처가 있는지, 적용 가능한지 여부를 확인하는 역할을 합니다. 특정 조건이 충족되는 경우에만 적용할 수 있는 바우처에 대한 것일 수 있습니다. 예를 들어 총 장바구니 가격이 $100보다 큰 경우. 어떤 이유로든 바우처를 적용할 수 없는 경우 `addVoucher` 메서드에서 예외가 발생합니다. 또한 `CommerceSession`은(는) 바우처를 추가/제거한 후 장바구니의 가격을 업데이트할 책임이 있습니다.

`Voucher`은(는) 다음에 대한 필드를 포함하는 Bean과 유사한 클래스입니다.

* 바우처 코드
* 간단한 설명
* 할인 유형 및 값을 나타내는 관련 판촉 참조

입력한 `AbstractJcrCommerceSession`은(는) 바우처를 적용할 수 있습니다. 클래스 `getVouchers()`에서 반환된 바우처는 다음 속성이 포함된 jcr:content 노드가 포함된 `cq:Page`의 인스턴스입니다(다른 인스턴스 포함).

* `sling:resourceType`(문자열) - `commerce/components/voucher`이어야 합니다.

* `jcr:title`(문자열) - 바우처 설명에 사용됩니다.
* `code`(문자열) - 이 바우처를 적용하려면 사용자가 입력해야 하는 코드
* `promotion`(문자열) - 적용할 프로모션. 예: `/content/campaigns/geometrixx-outdoors/article/10-bucks-off`

프로모션 핸들러는 장바구니를 수정하는 OSGi 서비스입니다. 장바구니는 `PromotionHandler` 인터페이스에 정의된 여러 개의 후크를 지원합니다.

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

기본적으로 3개의 프로모션 핸들러가 제공됩니다.

* `DiscountPromotionHandler`이(가) 장바구니 전체 절대 또는 백분율 할인을 적용합니다.
* `PerfectPartnerPromotionHandler`은(는) 제품 파트너가 장바구니에도 있는 경우 제품 절대 또는 비율 할인을 적용합니다.
* `FreeShippingPromotionHandler` 무료 배송 적용
