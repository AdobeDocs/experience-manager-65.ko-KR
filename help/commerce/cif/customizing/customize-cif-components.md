---
title: CIF 코어 구성 요소 사용자 지정
description: AEM CIF 코어 구성 요소를 사용자 지정하는 방법을 알아봅니다. 이 자습서에서는 비즈니스 특정 요구 사항을 충족하도록 CIF 코어 구성 요소를 안전하게 확장하는 방법을 설명합니다. GraphQL 쿼리를 확장하여 사용자 지정 속성을 반환하고 CIF 코어 구성 요소에 새 속성을 표시하는 방법을 알아봅니다.
sub-product: Commerce
topics: Development
version: Cloud Service
doc-type: tutorial
activity: develop
audience: developer
feature: Commerce Integration Framework
kt: 4279
thumbnail: customize-aem-cif-core-component.jpg
exl-id: 8933942e-be49-49d3-bf0a-7225257e2803
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '2604'
ht-degree: 2%

---

# AEM CIF 핵심 구성 요소 사용자 지정 {#customize-cif-components}

다음 [CIF 베니아 프로젝트](https://github.com/adobe/aem-cif-guides-venia) 는 를 사용하기 위한 참조 코드 베이스입니다 [CIF 코어 구성 요소](https://github.com/adobe/aem-core-cif-components). 이 자습서에서는 추가 확장을 수행합니다 [제품 티저](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser) 구성 요소를 사용하여 Adobe Commerce의 사용자 지정 속성을 표시할 수 있습니다. 또한 AEM과 Adobe Commerce의 GraphQL 통합과 CIF 코어 구성 요소에서 제공하는 확장 후크 간의 GraphQL에 대해 자세히 알아봅니다.

>[!TIP]
>
> 를 사용하십시오 [AEM 프로젝트 원형](https://github.com/adobe/aem-project-archetype) 고유한 상거래 구현을 시작할 때.

## 빌드할 내용

베니아 브랜드가 최근 지속가능한 소재를 이용해 일부 제품을 제조하기 시작했고 이 회사는 이 제품을 출시하고 싶어한다 **친환경** 배지 를 제품 티저의 일부로 사용합니다. 제품이 **친환경** 재료. 이 사용자 지정 속성은 GraphQL 쿼리의 일부로 추가되고 지정된 제품의 제품 티저에 표시됩니다.

![친환경 배지 최종 구현](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## 사전 요구 사항 {#prerequisites}

이 자습서를 완료하려면 로컬 개발 환경이 필요합니다. 여기에는 Adobe Commerce 인스턴스에 구성 및 연결된 AEM의 실행 인스턴스가 포함됩니다. 다음 요구 사항 및 단계를 검토하십시오 [AEM을 사용하여 로컬 개발 설정](../develop.md). 자습서를 완전히 따르려면 추가 권한이 필요합니다 [제품에 대한 속성](https://docs.magento.com/user-guide/catalog/product-attributes-add.html) Adobe Commerce.

다음과 같은 GraphQL IDE가 필요합니다 [GraphiQL](https://github.com/graphql/graphiql) 또는 브라우저 확장을 사용하여 코드 샘플 및 자습서를 실행할 수 있습니다. 브라우저 확장을 설치하는 경우 요청 헤더를 설정할 수 있는 기능이 있는지 확인하십시오. Google Chrome에서, [Alt GraphQL 클라이언트](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja) 는 작업을 수행할 수 있는 하나의 확장입니다.

## Venia 프로젝트 복제 {#clone-venia-project}

복제 [베니아 프로젝트](https://github.com/adobe/aem-cif-guides-venia) 그런 다음 기본 스타일을 재정의합니다.

>[!NOTE]
>
> **기존 프로젝트를 자유롭게 사용** (CIF가 포함된 AEM Project Archetype에 따라) 이 섹션을 건너뜁니다.

1. 다음 git 명령을 실행하여 프로젝트를 복제합니다.

   ```shell
   $ git clone git@github.com:adobe/aem-cif-guides-venia.git
   ```

1. 프로젝트를 AEM의 로컬 인스턴스에 빌드 및 배포합니다.

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. 필요한 OSGi 구성을 추가하여 AEM 인스턴스를 Adobe Commerce 인스턴스에 연결하거나 구성을 새로 만든 프로젝트에 추가합니다.

1. 이때 Adobe Commerce 인스턴스에 연결된 스토어의 작업 버전이 있어야 합니다. 로 이동합니다 `US` > `Home` 페이지 위치: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

   현재 스토프런트가 Venia 테마를 사용하고 있다는 것을 알 수 있습니다. 스토어의 주 메뉴를 확장하면 Adobe Commerce 연결이 작동하는 것을 나타내는 다양한 카테고리가 표시됩니다.

   ![Venia 테마로 구성된 Storefront](../assets/customize-cif-components/venia-store-configured.png)

## 제품 티저 작성 {#author-product-teaser}

제품 티저 구성 요소는 이 자습서 전체에서 확장됩니다. 첫 번째 단계에서는 홈 페이지에 제품 티저의 새 인스턴스를 추가하여 기준 기능을 이해합니다.

1. 로 이동합니다 **홈 페이지** 사이트: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

2. 새 항목 삽입 **제품 티저** 구성 요소를 페이지의 기본 레이아웃 컨테이너에 추가

   ![제품 티저 삽입](../assets/customize-cif-components/product-teaser-add-component.png)

3. 사이드 패널(아직 전환되지 않은 경우)을 확장하고 자산 파인더 드롭다운을 (으)로 전환합니다. **제품**. 연결된 Adobe Commerce 인스턴스의 사용 가능한 제품 목록이 표시됩니다. 제품 및 **드래그+드롭** 위로 **제품 티저** 구성 요소를 생성하지 않습니다.

   ![드래그 + 제품 티저 놓기](../assets/customize-cif-components/drag-drop-product-teaser.png)

   >[!NOTE]
   >
   > 참고: 대화 상자( 클릭)를 사용하여 구성 요소를 구성하여 표시된 제품을 구성할 수도 있습니다 _렌치_ 아이콘).

4. 이제 제품 티저에 의해 제품 이 표시됩니다. 제품 이름 및 제품 가격 은 표시되는 기본 속성입니다.

   ![제품 티저 - 기본 스타일](../assets/customize-cif-components/product-teaser-default-style.png)

## Adobe Commerce에서 사용자 지정 속성 추가 {#add-custom-attribute}

AEM에 표시되는 제품 및 제품 데이터는 Adobe Commerce에 저장됩니다. 다음에 대한 새 속성을 추가합니다 **친환경** Adobe Commerce UI를 사용하여 설정한 제품 속성의 일부로 제공됩니다.

>[!TIP]
>
> 이미 사용자 지정 항목이 있습니다. **예/아니오** 속성을 제품 속성 세트의 일부로 포함하시겠습니까? 자유롭게 사용하고 이 섹션을 건너뜁니다.

1. Adobe Commerce 인스턴스에 로그인합니다.
1. 다음으로 이동 **카탈로그** > **제품**.
1. 검색 필터를 업데이트하여 **구성 가능한 제품** 이전 연습에서 티저 구성 요소에 추가될 때 사용됩니다. 제품을 편집 모드로 엽니다.

   ![Value 제품 검색](../assets/customize-cif-components/search-valeria-product.png)

1. 제품 보기에서 **속성 추가** > **새 속성 만들기**.
1. 을(를) 입력합니다. **새 속성** 다음 값이 있는 양식(다른 값에 대한 기본 설정 남기기)

   | 필드 세트 | 필드 레이블 | 값 |
   | ----------------------------- | ------------------ | ---------------- |
   | 속성 속성 | 속성 레이블 | **친환경** |
   | 속성 속성 | 카탈로그 입력 유형 | **예/아니오** |
   | 고급 속성 속성 | 속성 코드 | **eco_friendly** |

   ![새 속성 양식](../assets/customize-cif-components/attribute-new-form.png)

   클릭 **속성 저장** 완료됨.

1. 제품 하단으로 스크롤하여 **속성** 제목. 새로운 기능이 표시됩니다 **친환경** 필드. 토글을 다음으로 전환 **예**.

   ![yes로 전환](../assets/customize-cif-components/eco-friendly-toggle-yes.png)

   **저장** 제품에 대한 변경 사항입니다.

   >[!TIP]
   >
   > 관리에 대한 자세한 내용 [제품 속성은 Adobe Commerce 사용 안내서에서 확인할 수 있습니다](https://docs.magento.com/user-guide/catalog/attribute-best-practices.html).

1. 다음으로 이동 **시스템** > **도구** > **캐시 관리**. 데이터 스키마가 업데이트되었으므로 Adobe Commerce의 일부 캐시 유형을 무효화해야 합니다.
1. 옆에 있는 상자를 선택합니다. **구성** 캐시 유형을 **새로 고침**

   ![구성 캐시 유형 새로 고침](../assets/customize-cif-components/refresh-configuration-cache-type.png)

   >[!TIP]
   >
   > 에 대한 자세한 내용 [캐시 관리 는 Adobe Commerce 사용 안내서에서 찾을 수 있습니다](https://docs.magento.com/user-guide/system/cache-management.html).

## GraphQL IDE를 사용하여 속성 확인 {#use-graphql-ide}

AEM 코드로 이동하기 전에 다음을 탐색하는 것이 유용합니다 [Adobe Commerce GraphQL](https://devdocs.magento.com/guides/v2.4/graphql/) GraphQL IDE 사용. AEM과의 Adobe Commerce 통합은 주로 일련의 GraphQL 쿼리를 통해 수행됩니다. GraphQL 쿼리를 이해하고 수정하는 것은 CIF 코어 구성 요소를 확장할 수 있는 주요 방법 중 하나입니다.

그런 다음 GraphQL IDE를 사용하여 `eco_friendly` 속성이 제품 속성 세트에 추가되었습니다. 이 자습서의 스크린샷은 [Alt GraphQL 클라이언트](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja).

1. GraphQL IDE를 열고 URL을 입력합니다 `http://<server>/graphql` ( IDE 또는 확장의 URL 표시줄)을 참조하십시오.
2. 다음을 추가합니다 [제품 쿼리](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html) 여기서 `YOUR_SKU` 은 **SKU** 이전 연습에서 사용된 제품의 경우:

   ```json
     {
       products(
       filter: { sku: { eq: "YOUR_SKU" } }
       ) {
           items {
           name
           sku
           eco_friendly
           }
       }
   }
   ```

3. 쿼리를 실행하면 다음과 같은 응답을 받게 됩니다.

   ```json
   {
     "data": {
       "products": {
         "items": [
           {
             "name": "Valeria Two-Layer Tank",
             "sku": "VT11",
             "eco_friendly": 1
           }
         ]
       }
     }
   }
   ```

   ![샘플 GraphQL 응답](../assets/customize-cif-components/sample-graphql-query.png)

   다음 값이 **예** 의 정수입니다 **1**. 이 기능은 Java로 GraphQL 쿼리를 작성할 때 유용합니다.

   >[!TIP]
   >
   > 에 대한 자세한 설명서 [Adobe Commerce GraphQL은 여기에서 찾을 수 있습니다](https://devdocs.magento.com/guides/v2.4/graphql/index.html).

## 제품 티저에 대한 Sling 모델 업데이트 {#updating-sling-model-product-teaser}

다음으로, Sling 모델을 구현하여 제품 티저의 비즈니스 논리를 확장합니다. [Sling 모델](https://sling.apache.org/documentation/bundles/models.html)는 구성 요소에 필요한 비즈니스 로직을 구현하는 주석 기반 &quot;POJO&quot;(일반 이전 Java 개체)입니다. Sling 모델은 HTL 스크립트와 함께 구성 요소의 일부로 사용됩니다. 우리는 [Sling 모델에 대한 위임 패턴](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) 기존 제품 티저 모델의 일부를 확장할 수 있습니다.

Sling 모델은 Java로 구현되며 **코어** 생성된 프로젝트의 모듈입니다.

사용 [원하는 IDE](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#set-up-the-development-ide) 벤 프로젝트를 가져오기 위해 사용된 스크린샷은 [Visual Studio 코드 IDE](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#microsoft-visual-studio-code).

1. IDE에서 **코어** 모듈 대상: `core/src/main/java/com/venia/core/models/commerce/MyProductTeaser.java`.

   ![핵심 위치 IDE](../assets/customize-cif-components/core-location-ide.png)

   `MyProductTeaser.java` 는 CIF를 확장하는 Java 인터페이스입니다 [ProductTeaser](https://github.com/adobe/aem-core-cif-components/blob/master/bundles/core/src/main/java/com/adobe/cq/commerce/core/components/models/productteaser/ProductTeaser.java) 인터페이스.

   이미 새로운 메서드를 추가했습니다. `isShowBadge()` 를 추가하여 제품이 &quot;신규&quot;로 간주되는 경우 배지를 표시할 수 있습니다.

1. 새 메서드 추가, `isEcoFriendly()` 인터페이스:

   ```java
   @ProviderType
   public interface MyProductTeaser extends ProductTeaser {
       // Extend the existing interface with the additional properties which you
       // want to expose to the HTL template.
       public Boolean isShowBadge();
   
       public Boolean isEcoFriendly();
   }
   ```

   이 방법은 해당 제품에 가 있는지 여부를 나타내는 논리를 캡슐화하는 새로운 방법입니다 `eco_friendly` 속성 설정 **예** 또는 **아니요**.

1. 다음으로, `MyProductTeaserImpl.java` at `core/src/main/java/com/venia/core/models/commerce/MyProductTeaserImpl.java`.

   다음 [Sling 모델에 대한 위임 패턴](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) 허용 `MyProductTeaserImpl` 를 참조합니다. `ProductTeaser` 를 통해 모델 `sling:resourceSuperType` 속성:

   ```java
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductTeaser productTeaser;
   ```

   무시하거나 변경하지 않으려는 모든 방법에 대해 `ProductTeaser` 를 반환합니다. 예:

   ```java
   @Override
   public String getImage() {
       return productTeaser.getImage();
   }
   ```

   이렇게 하면 구현에서 작성해야 하는 Java 코드의 양이 최소화됩니다.

1. AEM CIF 코어 구성 요소에서 제공하는 추가 확장 포인트 중 하나는 `AbstractProductRetriever` 특정 제품 속성에 대한 액세스를 제공합니다. Inspect `initModel()` 메서드:

   ```java
   import javax.annotation.PostConstruct;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
       ...
       private AbstractProductRetriever productRetriever;
   
       /* add this method to intialize the proudctRetriever */
       @PostConstruct
       public void initModel() {
           productRetriever = productTeaser.getProductRetriever();
   
           if (productRetriever != null) {
               productRetriever.extendProductQueryWith(p -> p.createdAt());
           }
   
       }
   ...
   ```

   다음 `@PostConstruct` 주석을 사용하면 Sling 모델이 초기화되는 즉시 이 메서드가 호출됩니다.

   제품 GraphQL 쿼리가 `extendProductQueryWith` 추가 검색 방법 `created_at` 속성을 사용합니다. 이 속성은 나중에 의 일부로 사용됩니다 `isShowBadge()` 메서드를 사용합니다.

1. GraphQL 쿼리를 업데이트하여 `eco_friendly` 부분 쿼리의 속성:

   ```java
   //MyProductTeaserImpl.java
   
   private static final String ECO_FRIENDLY_ATTRIBUTE = "eco_friendly";
   
   @PostConstruct
   public void initModel() {
       productRetriever = productTeaser.getProductRetriever();
   
       if (productRetriever != null) {
           productRetriever.extendProductQueryWith(p -> p
               .createdAt()
               .addCustomSimpleField(ECO_FRIENDLY_ATTRIBUTE)
           );
       }
   }
   ```

   에 추가 `extendProductQueryWith` 메서드는 추가적인 제품 속성을 모델의 나머지 부분에서 사용할 수 있도록 하는 강력한 방법입니다. 또한 실행된 쿼리 수를 최소화합니다.

   위의 코드에서`addCustomSimpleField` 는 를 검색하는 데 사용됩니다 `eco_friendly` 속성을 사용합니다. Adobe Commerce 스키마에 포함된 모든 사용자 지정 속성을 쿼리할 수 있는 방법을 보여 줍니다.

   >[!NOTE]
   >
   > 다음 `createdAt()` 메서드는 실제로 의 일부로 구현되었습니다 [제품 인터페이스](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java). 일반적으로 발견되는 대부분의 스키마 특성이 구현되었으므로 `addCustomSimpleField` 참조하십시오.

1. Java 코드를 디버깅하는 데 도움이 되도록 로거를 추가합니다.

   ```java
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
   
   private static final Logger LOGGER = LoggerFactory.getLogger(MyProductTeaserImpl.class);
   ```

1. 다음으로, 를 구현합니다 `isEcoFriendly()` 메서드:

   ```java
   @Override
   public Boolean isEcoFriendly() {
   
       Integer ecoFriendlyValue;
       try {
           ecoFriendlyValue = productRetriever.fetchProduct().getAsInteger(ECO_FRIENDLY_ATTRIBUTE);
           if(ecoFriendlyValue != null && ecoFriendlyValue.equals(Integer.valueOf(1))) {
               LOGGER.info("*** Product is Eco Friendly**");
               return true;
           }
       } catch (SchemaViolationError e) {
           LOGGER.error("Error retrieving eco friendly attribute");
       }
       LOGGER.info("*** Product is not Eco Friendly**");
       return false;
   }
   ```

   위의 메서드에서 `productRetriever` 는 제품 및 `getAsInteger()` 메서드를 사용하여 `eco_friendly` 속성을 사용합니다. 앞서 실행한 GraphQL 쿼리를 기반으로 할 경우 `eco_friendly` 속성이 &quot;(으)로 설정되어 있습니다.**예**&quot;은 실제로 의 정수입니다 **1**.

   Sling 모델이 업데이트되었으므로 의 표시기를 실제로 표시하려면 구성 요소 마크업을 업데이트해야 합니다. **친환경** Sling 모델을 기반으로 합니다.

## 제품 티저의 마크업 사용자 정의 {#customize-markup-product-teaser}

AEM 구성 요소의 일반적인 확장은 구성 요소에서 생성한 마크업을 수정하는 것입니다. 이 작업은 [HTL 스크립트](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html) 구성 요소가 태그를 렌더링하는 데 사용하는 것입니다. HTL(HTML 템플릿 언어)은 AEM 구성 요소가 작성된 컨텐츠를 기반으로 마크업을 동적으로 렌더링하는 데 사용하는 간단한 템플릿 언어이며, 구성 요소를 다시 사용할 수 있습니다. 예를 들어 제품 티저를 반복해서 사용하여 서로 다른 제품을 표시할 수 있습니다.

이 경우 티저 위에 배너를 렌더링하여 제품이 사용자 지정 속성에 따라 &quot;친환경&quot;임을 표시하려고 합니다. 디자인 패턴 [마크업 사용자 정의](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/customizing.html#customizing-the-markup) 구성 요소의 표준은 AEM CIF 핵심 구성 요소뿐만 아니라 모든 AEM 구성 요소에 대해서도 표준입니다.

>[!NOTE]
>
> 이 제품 티저 또는 CIF 페이지 구성 요소와 같은 CIF 제품 및 카테고리 선택기를 사용하여 구성 요소를 사용자 지정하는 경우 필요한 를 포함해야 합니다 `cif.shell.picker` clientlib 을 구성 요소 대화 상자에 추가합니다. 자세한 내용은 [CIF 제품 및 카테고리 선택기 사용](use-cif-pickers.md) 자세한 내용

1. IDE에서 `ui.apps` 폴더 계층 구조를 모듈로 확장하고 다음을 수행합니다. `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser` 그리고 검사 `.content.xml` 파일.

   ![제품 티저 ui.apps](../assets/customize-cif-components/product-teaser-ui-apps-ide.png)

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:description="Product Teaser Component"
       jcr:primaryType="cq:Component"
       jcr:title="Product Teaser"
       sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"
       componentGroup="Venia - Commerce"/>
   ```

   이상은 프로젝트의 제품 티저 구성 요소에 대한 구성 요소 정의입니다. 속성에 주목합니다. `sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"`. 다음은 를 만드는 예제입니다 [프록시 구성 요소](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/get-started/using.html#create-proxy-components). AEM CIF 코어 구성 요소에서 모든 제품 티저 HTL 스크립트를 복사하여 붙여넣는 대신, `sling:resourceSuperType` 를 상속하여 모든 기능을 상속합니다.

1. 파일을 엽니다. `productteaser.html`. 이 사본은 `productteaser.html` 파일에서 [CIF 제품 티저](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/productteaser.html)

   ```html
   <!--/* productteaser.html */-->
   <sly
     data-sly-use.product="com.venia.core.models.commerce.MyProductTeaser"
     data-sly-use.templates="core/wcm/components/commons/v1/templates.html"
     data-sly-use.actionsTpl="actions.html"
     data-sly-test.isConfigured="${properties.selection}"
     data-sly-test.hasProduct="${product.url}"
   ></sly>
   ```

   에 대한 Sling 모델 `MyProductTeaser` 이 사용되고 `product` 변수를 채우는 방법을 설명합니다.

1. 수정 `productteaser.html` 를 호출하다 `isEcoFriendly` 이전 연습에서 구현된 방법:

   ```html
   ...
   <div
     data-sly-test="${isConfigured && hasProduct}"
     class="item__root"
     data-cmp-is="productteaser"
     data-virtual="${product.virtualProduct}"
   >
     <div data-sly-test="${product.showBadge}" class="item__badge">
       <span>${properties.text || 'New'}</span>
     </div>
     <!--/* Insert call to Eco Friendly here */-->
     <div data-sly-test="${product.ecoFriendly}" class="item__eco">
       <span>Eco Friendly</span>
     </div>
     ...
   </div>
   ```

   HTL에서 Sling 모델 메서드를 호출할 때 `get` 및 `is` 메서드 일부가 삭제되고 첫 번째 문자는 소문자입니다. 그래서 `isShowBadge()` 다음과 같이 `.showBadge` 및 `isEcoFriendly` 다음과 같이 `.ecoFriendly`. 다음에서 반환된 부울 값 기반 `.isEcoFriendly()` 는 다음 여부를 결정합니다 `<span>Eco Friendly</span>` 이 표시됩니다.

   에 대한 추가 정보 `data-sly-test` 및 기타 [HTL 블록 문은 여기에서 찾을 수 있습니다](https://docs.adobe.com/content/help/en/experience-manager-htl/using/htl/block-statements.html#test).

1. 명령줄 터미널에서 Maven 기술을 사용하여 변경 사항을 저장하고 AEM에 업데이트를 배포합니다.

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. 새 브라우저 창을 열고 AEM 및 으로 이동합니다. **OSGi 콘솔** > **상태** > **Sling 모델**: [http://localhost:4502/system/console/status-slingmodels](http://localhost:4502/system/console/status-slingmodels)

1. 검색 대상 `MyProductTeaserImpl` 다음과 같은 줄이 표시됩니다.

   ```plain
   com.venia.core.models.commerce.MyProductTeaserImpl - venia/components/commerce/productteaser
   ```

   이는 Sling 모델이 제대로 배포되어 올바른 구성 요소에 매핑되었음을 나타냅니다.

1. 에 새로 고침 **Venia 홈 페이지** at [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html) 여기서 제품 티저가 추가되었습니다.

   ![친환경 메시지 표시](../assets/customize-cif-components/eco-friendly-text-displayed.png)

   제품에 `eco_friendly` 속성 설정 **예**&#x200B;페이지에 &quot;친환경&quot; 텍스트가 표시됩니다. 동작 변경을 보려면 다른 제품으로 전환해 보십시오.

1. 다음으로 AEM 열기 `error.log` 추가한 로그 명령문을 확인합니다. 다음 `error.log` 에 있습니다. `<AEM SDK Install Location>/crx-quickstart/logs/error.log`.

   AEM 로그를 검색하여 Sling 모델에 추가된 로그 문을 확인합니다.

   ```plain
   2020-08-28 12:57:03.114 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is Eco Friendly**
   ...
   2020-08-28 13:01:00.271 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is not Eco Friendly**
   ...
   ```

   >[!CAUTION]
   >
   > Teaser에 사용된 제품에 가 없는 경우에도 일부 스택 추적이 표시될 수 있습니다 `eco_friendly` 속성 세트의 일부로 속성이 사용됩니다.

## 친환경 배지에 대한 스타일 추가 {#add-styles}

이때 다음을 표시할 시점에 대한 논리를 **친환경** 배지가 작동하지만 일반 텍스트에서 일부 스타일을 사용할 수 있습니다. 다음으로 아이콘 및 스타일을 `ui.frontend` 모듈 을 클릭하여 구현을 완료합니다.

1. 다운로드 [eco_friendly.svg](../assets/customize-cif-components/eco_friendly.svg) 파일. 이 항목은 **친환경** 배지.
1. IDE로 돌아가서 `ui.frontend` 폴더를 입력합니다.
1. 추가 `eco_friendly.svg` 파일 `ui.frontend/src/main/resources/images` 폴더:

   ![친환경 SVG 추가](../assets/customize-cif-components/eco-friendly-svg-added.png)

1. 파일을 엽니다. `productteaser.scss` at `ui.frontend/src/main/styles/commerce/_productteaser.scss`.
1. 다음 Sass 규칙을 `.productteaser` 클래스:

   ```scss
   .productteaser {
       ...
       .item__eco {
           width: 60px;
           height: 60px;
           left: 0px;
           overflow: hidden;
           position: absolute;
           padding: 5px;
   
       span {
           display: block;
           position: absolute;
           width: 45px;
           height: 45px;
           text-indent: -9999px;
           background: no-repeat center center url('../resources/images/eco_friendly.svg');
           }
       }
   ...
   }
   ```

   >[!NOTE]
   >
   > 체크 아웃 [스타일 지정 CIF 코어 구성 요소](./style-cif-component.md) 프런트엔드 워크플로우에 대한 자세한 내용을 참조하십시오.

1. 명령줄 터미널에서 Maven 기술을 사용하여 변경 사항을 저장하고 AEM에 업데이트를 배포합니다.

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. 에 새로 고침 **Venia 홈 페이지** at [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html) 여기서 제품 티저가 추가되었습니다.

   ![친환경 배지 최종 구현](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## 축하합니다 {#congratulations}

첫 번째 AEM CIF 구성 요소를 사용자 지정했을 뿐입니다. 다운로드 [여기에서는 솔루션 파일 완료](../assets/customize-cif-components/customize-cif-component-SOLUTION_FILES.zip).

## 보너스 챌린지 {#bonus-challenge}

의 기능을 검토합니다 **새로 만들기** 배지 제품 티저에 이미 구현되어 있습니다. 작성자가 **친환경** 배지가 표시됩니다. 에서 구성 요소 대화 상자를 업데이트해야 합니다. `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser/_cq_dialog/.content.xml`.

![새로운 배지 구현 문제](../assets/customize-cif-components/new-badge-implementation-challenge.png)

## 추가 리소스 {#additional-resources}

- [AEM Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)
- [AEM CIF 코어 구성 요소](https://github.com/adobe/aem-core-cif-components)
- [AEM CIF 핵심 구성 요소 사용자 정의](https://github.com/adobe/aem-core-cif-components/wiki/Customizing-CIF-Core-Components)
- [핵심 구성 요소 사용자 정의](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html)
- [AEM Sites 시작하기](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)
- [CIF 제품 및 카테고리 선택기 사용](use-cif-pickers.md)
