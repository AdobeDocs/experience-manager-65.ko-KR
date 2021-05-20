---
title: CIF 코어 구성 요소 사용자 지정
description: AEM CIF 코어 구성 요소를 사용자 지정하는 방법을 알아봅니다. 이 자습서에서는 비즈니스 특정 요구 사항을 충족하도록 CIF 코어 구성 요소를 안전하게 확장하는 방법을 설명합니다. GraphQL 쿼리를 확장하여 사용자 지정 속성을 반환하고 CIF 코어 구성 요소에 새 속성을 표시하는 방법을 알아봅니다.
sub-product: 상거래
topics: Development
version: cloud-service
doc-type: tutorial
activity: develop
audience: developer
feature: 전자 상거래 통합 프레임워크
kt: 4279
thumbnail: customize-aem-cif-core-component.jpg
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '2541'
ht-degree: 1%

---

# AEM CIF 코어 구성 요소 사용자 지정 {#customize-cif-components}

[CIF Venia Project](https://github.com/adobe/aem-cif-guides-venia)는 [CIF Core Components](https://github.com/adobe/aem-core-cif-components)를 사용하기 위한 참조 코드 베이스입니다. 이 자습서에서는 [제품 티저](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser) 구성 요소를 추가로 확장하여 Magento의 사용자 지정 속성을 표시합니다. 또한 AEM과 Magento의 GraphQL 통합과 CIF 코어 구성 요소에서 제공하는 확장 후크 간의 GraphQL에 대해 자세히 알아봅니다.

>[!TIP]
>
> 고유한 상거래 구현을 시작할 때 [AEM Project Archetype](https://github.com/adobe/aem-project-archetype)을 사용하십시오.

## 빌드할 내용

Venia 브랜드는 최근 지속 가능한 재료를 사용하여 일부 제품을 제조하기 시작했고, Product Teaser의 일부로서 **Eco Friendly** 배지를 표시하고자 합니다. Magento에 새로운 사용자 지정 속성이 생성되어 제품에서 **친환경** 자료를 사용하는지 여부를 나타냅니다. 이 사용자 지정 속성은 GraphQL 쿼리의 일부로 추가되고 지정된 제품의 제품 티저에 표시됩니다.

![친환경 배지 최종 구현](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## 전제 조건 {#prerequisites}

이 자습서를 완료하려면 로컬 개발 환경이 필요합니다. 여기에는 Magento 인스턴스에 구성 및 연결된 AEM의 실행 인스턴스가 포함됩니다. [AEM](../develop.md)을 사용하여 로컬 개발을 설정하는 요구 사항과 단계를 검토하십시오. 자습서를 완전히 따르려면 Magento에서 [속성을 제품](https://docs.magento.com/user-guide/catalog/product-attributes-add.html)에 추가할 수 있는 권한이 있어야 합니다.

또한 코드 샘플 및 자습서를 실행하려면 [GraphiQL](https://github.com/graphql/graphiql) 또는 브라우저 확장과 같은 GraphQL IDE가 필요합니다. 브라우저 확장을 설치하는 경우 요청 헤더를 설정할 수 있는 기능이 있는지 확인하십시오. Google Chrome에서 [Alt GraphQL 클라이언트](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja)는 작업을 수행할 수 있는 하나의 확장입니다.

## Venia 프로젝트 복제 {#clone-venia-project}

[Venia Project](https://github.com/adobe/aem-cif-guides-venia)를 복제한 다음 기본 스타일을 재정의합니다.

>[!NOTE]
>
> **CIF가 포함된 AEM Project Archetype에 따라 언제든지 기존 프로젝트를**  사용할 수 있으며, 이 섹션을 건너뜁니다.

1. 다음 git 명령을 실행하여 프로젝트를 복제합니다.

   ```shell
   $ git clone git@github.com:adobe/aem-cif-guides-venia.git
   ```

1. 프로젝트를 AEM의 로컬 인스턴스에 빌드 및 배포합니다.

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. 필요한 OSGi 구성을 추가하여 AEM 인스턴스를 Magento 인스턴스에 연결하거나 구성을 새로 만든 프로젝트에 추가합니다.

1. 이때 Magento 인스턴스에 연결된 스토어의 작업 버전이 있어야 합니다. 다음 위치에서 `US` > `Home` 페이지로 이동합니다.[http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)

   현재 스토프런트가 Venia 테마를 사용하고 있다는 것을 알 수 있습니다. 스토어의 주 메뉴를 확장하면 연결 Magento이 작동하는지 나타내는 다양한 범주가 표시됩니다.

   ![Venia 테마로 구성된 Storefront](../assets/customize-cif-components/venia-store-configured.png)

## 제품 티저 {#author-product-teaser} 작성

제품 티저 구성 요소는 이 자습서 전체에서 확장됩니다. 첫 번째 단계에서는 홈 페이지에 제품 티저의 새 인스턴스를 추가하여 기준 기능을 이해합니다.

1. 사이트의 **홈 페이지**&#x200B;로 이동합니다.[http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

2. 페이지의 기본 레이아웃 컨테이너에 새 **제품 티저** 구성 요소를 삽입합니다.

   ![제품 티저 삽입](../assets/customize-cif-components/product-teaser-add-component.png)

3. 사이드 패널(아직 전환되지 않은 경우)을 확장하고 자산 파인더 드롭다운을 **Products**&#x200B;로 전환합니다. 연결된 Magento 인스턴스의 사용 가능한 제품 목록이 표시됩니다. 제품을 선택하고 **드래그하여**&#x200B;페이지의 **제품 티저** 구성 요소에 놓으십시오.

   ![드래그 + 제품 티저 놓기](../assets/customize-cif-components/drag-drop-product-teaser.png)

   >[!NOTE]
   >
   > 참고: 대화 상자를 사용하여 구성 요소를 구성하여 표시된 제품을 구성할 수도 있습니다( _렌치_ 아이콘 클릭).

4. 이제 제품 티저에 의해 제품 이 표시됩니다. 제품 이름 및 제품 가격 은 표시되는 기본 속성입니다.

   ![제품 티저 - 기본 스타일](../assets/customize-cif-components/product-teaser-default-style.png)

## Magento {#add-custom-attribute}에 사용자 지정 속성 추가

AEM에 표시되는 제품 및 제품 데이터는 Magento에 저장됩니다. 그런 다음 Magento UI를 사용하여 설정한 제품 속성의 일부로 **Eco Friendly**&#x200B;에 대한 새 속성을 추가합니다.

>[!TIP]
>
> 이미 제품 속성 집합의 일부로 사용자 지정 **Yes/No** 특성이 있습니까? 자유롭게 사용하고 이 섹션을 건너뜁니다.

1. Magento 인스턴스에 로그인합니다.
1. **카탈로그** > **제품**&#x200B;으로 이동합니다.
1. 검색 필터를 업데이트하여 이전 연습의 Teaser 구성 요소에 추가할 때 사용되는 **구성 가능한 제품**&#x200B;을 찾습니다. 제품을 편집 모드로 엽니다.

   ![Value 제품 검색](../assets/customize-cif-components/search-valeria-product.png)

1. 제품 보기에서 **속성 추가** > **새 속성 만들기**&#x200B;를 클릭합니다.
1. 다음 값으로 **새 속성** 양식을 채웁니다(다른 값에 대한 기본 설정 유지)

   | 필드 세트 | 필드 레이블 | 값 |
   | ----------------------------- | ------------------ | ---------------- |
   | 속성 속성 | 속성 레이블 | **친환경** |
   | 속성 속성 | 카탈로그 입력 유형 | **예/아니오** |
   | 고급 속성 속성 | 속성 코드 | **eco_friendly** |

   ![새 속성 양식](../assets/customize-cif-components/attribute-new-form.png)

   완료되면 **속성 저장**&#x200B;을 클릭합니다.

1. 제품 하단으로 스크롤하여 **Attributes** 제목을 확장합니다. 새 **친환경** 필드가 표시됩니다. 전환을 **Yes**&#x200B;로 전환합니다.

   ![yes로 전환](../assets/customize-cif-components/eco-friendly-toggle-yes.png)

   **** 변경 사항을 제품에 저장합니다.

   >[!TIP]
   >
   > [제품 속성 관리에 대한 자세한 내용은 Magento 사용 안내서](https://docs.magento.com/user-guide/catalog/attribute-best-practices.html)에서 확인할 수 있습니다.

1. **시스템** > **도구** > **캐시 관리**&#x200B;로 이동합니다. 데이터 스키마를 업데이트했으므로 Magento의 일부 캐시 유형을 무효화해야 합니다.
1. **구성** 옆의 확인란을 선택하고 **새로 고침**&#x200B;에 대한 캐시 유형을 제출합니다.

   ![구성 캐시 유형 새로 고침](../assets/customize-cif-components/refresh-configuration-cache-type.png)

   >[!TIP]
   >
   > [캐시 관리에 대한 자세한 내용은 Magento 사용 안내서](https://docs.magento.com/user-guide/system/cache-management.html)에서 확인할 수 있습니다.

## GraphQL IDE를 사용하여 속성 {#use-graphql-ide} 확인

AEM 코드로 이동하기 전에 GraphQL IDE를 사용하여 [Magento GraphQL](https://devdocs.magento.com/guides/v2.4/graphql/)을 탐색하는 것이 유용합니다. AEM과의 Magento 통합은 주로 일련의 GraphQL 쿼리를 통해 수행됩니다. GraphQL 쿼리를 이해하고 수정하는 것은 CIF 코어 구성 요소를 확장할 수 있는 주요 방법 중 하나입니다.

그런 다음 GraphQL IDE를 사용하여 `eco_friendly` 속성이 제품 속성 세트에 추가되었는지 확인합니다. 이 자습서의 스크린샷은 [Alt GraphQL 클라이언트](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja)를 사용합니다.

1. GraphQL IDE를 열고 IDE 또는 확장의 URL 표시줄에 URL `http://<magento-server>/graphql`을 입력합니다.
2. 다음 [products 쿼리](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html)을 추가합니다. 여기서 `YOUR_SKU`은 이전 연습에서 사용되는 제품의 **SKU**&#x200B;입니다.

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

   **Yes** 값은 **1**&#x200B;의 정수입니다. 이 기능은 Java로 GraphQL 쿼리를 작성할 때 유용합니다.

   >[!TIP]
   >
   > [Magento GraphQL에 대한 자세한 설명서는 여기에서 찾을 수 있습니다](https://devdocs.magento.com/guides/v2.4/graphql/index.html).

## 제품 Teaser {#updating-sling-model-product-teaser}에 대한 Sling 모델 업데이트

다음으로, Sling 모델을 구현하여 제품 티저의 비즈니스 논리를 확장합니다. [Sling 모델](https://sling.apache.org/documentation/bundles/models.html) 은 구성 요소에 필요한 비즈니스 로직을 구현하는 주석 기반의 &quot;POJO&quot;(일반 이전 Java 개체)입니다. Sling 모델은 HTL 스크립트와 함께 구성 요소의 일부로 사용됩니다. Sling 모델](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models)에 대한 [위임 패턴을 따르므로 기존 제품 티저 모델의 일부를 확장할 수 있습니다.

Sling 모델은 Java로 구현되며 생성된 프로젝트의 **core** 모듈에서 찾을 수 있습니다.

선택한 IDE의 [IDE를 사용하여 Venia 프로젝트를 가져옵니다. ](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#set-up-the-development-ide) 사용된 스크린샷은 [Visual Studio Code IDE](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#microsoft-visual-studio-code)에서 가져옵니다.

1. IDE에서 **core** 모듈 아래에서 다음 위치로 이동합니다.`core/src/main/java/com/venia/core/models/commerce/MyProductTeaser.java`

   ![핵심 위치 IDE](../assets/customize-cif-components/core-location-ide.png)

   `MyProductTeaser.java` 는 CIF ProductTeaser 인터페이스를 확장하는 Java  [](https://github.com/adobe/aem-core-cif-components/blob/master/bundles/core/src/main/java/com/adobe/cq/commerce/core/components/models/productteaser/ProductTeaser.java) 인터페이스입니다.

   제품이 &quot;New&quot;로 간주되는 경우 배지를 표시하기 위해 이미 `isShowBadge()` 이라는 새로운 방법이 추가되었습니다.

1. 인터페이스에 새 메서드 `isEcoFriendly()`을 추가합니다.

   ```java
   @ProviderType
   public interface MyProductTeaser extends ProductTeaser {
       // Extend the existing interface with the additional properties which you
       // want to expose to the HTL template.
       public Boolean isShowBadge();
   
       public Boolean isEcoFriendly();
   }
   ```

   이 메서드는 제품의 `eco_friendly` 속성이 **Yes** 또는 **No**&#x200B;로 설정되어 있는지 여부를 나타내는 논리를 캡슐화하는 새로운 방법을 제안합니다.

1. 그런 다음 `core/src/main/java/com/venia/core/models/commerce/MyProductTeaserImpl.java`에서 `MyProductTeaserImpl.java`을 검사합니다.

   Sling 모델](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models)에 대한 [위임 패턴을 사용하면 `MyProductTeaserImpl`에서 `sling:resourceSuperType` 속성을 통해 `ProductTeaser` 모델을 참조할 수 있습니다.

   ```java
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductTeaser productTeaser;
   ```

   재정의하거나 변경하지 않으려는 모든 방법에 대해 `ProductTeaser`이 반환하는 값을 반환하면 됩니다. 예:

   ```java
   @Override
   public String getImage() {
       return productTeaser.getImage();
   }
   ```

   이렇게 하면 구현에서 작성해야 하는 Java 코드의 양이 최소화됩니다.

1. AEM CIF 코어 구성 요소에서 제공하는 추가 확장 포인트 중 하나는 특정 제품 속성에 대한 액세스를 제공하는 `AbstractProductRetriever`입니다. Inspect `initModel()` 메서드:

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

   `@PostConstruct` 주석을 사용하면 Sling 모델이 초기화되는 즉시 이 메서드가 호출됩니다.

   제품 GraphQL 쿼리가 추가 `created_at` 속성을 검색하기 위해 `extendProductQueryWith` 메서드를 사용하여 이미 확장되었습니다. 이 속성은 나중에 `isShowBadge()` 메서드의 일부로 사용됩니다.

1. 부분 쿼리에 `eco_friendly` 속성을 포함하도록 GraphQL 쿼리를 업데이트합니다.

   ```java
   //MyProductTeaserImpl.java
   
   private static final String ECO_FRIENDLY_ATTRIBUTE = "eco_friendly";
   
   @PostConstruct
   public void initModel() {
       productRetriever = productTeaser.getProductRetriever();
   
       if (productRetriever != null) {
           productRetriever.extendProductQueryWith(p ->
                productRetriever.extendProductQueryWith(p -> p
                   .createdAt()
                   .addCustomSimpleField(ECO_FRIENDLY_ATTRIBUTE)
               );
           );
       }
   }
   ```

   `extendProductQueryWith` 메서드에 를 추가하는 것은 추가 제품 특성을 나머지 모델에 사용할 수 있도록 하는 강력한 방법입니다. 또한 실행된 쿼리 수를 최소화합니다.

   위의 코드에서는 `eco_friendly` 속성을 검색하는 데`addCustomSimpleField`이 사용됩니다. Magento 스키마에 속하는 모든 사용자 지정 속성을 쿼리하는 방법을 보여 줍니다.

   >[!NOTE]
   >
   > `createdAt()` 메서드는 실제로 [제품 인터페이스](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java)의 일부로 구현되었습니다. 일반적으로 발견되는 대부분의 스키마 특성이 구현되었으므로 실제 사용자 지정 속성에 `addCustomSimpleField`만 사용하십시오.

1. Java 코드를 디버깅하는 데 도움이 되도록 로거를 추가합니다.

   ```java
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
   
   private static final Logger LOGGER = LoggerFactory.getLogger(MyProductTeaserImpl.class);
   ```

1. 다음으로 `isEcoFriendly()` 메서드를 구현합니다.

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

   위의 메서드에서 `productRetriever` 를 사용하여 제품을 가져오고 `getAsInteger()` 메서드를 사용하여 `eco_friendly` 속성 값을 가져옵니다. 앞서 실행한 GraphQL 쿼리를 기준으로 `eco_friendly` 속성이 &quot;**Yes**&quot;로 설정된 경우 예상되는 값이 실제로 **1**&#x200B;의 정수임을 알 수 있습니다.

   Sling 모델이 업데이트되었으므로 Sling 모델을 기반으로 **Eco Friendly**&#x200B;의 표시기를 실제로 표시하려면 구성 요소 마크업을 업데이트해야 합니다.

## 제품 티저 {#customize-markup-product-teaser} 마크업 사용자 정의

AEM 구성 요소의 일반적인 확장은 구성 요소에서 생성한 마크업을 수정하는 것입니다. 이 작업은 구성 요소가 태그를 렌더링하는 데 사용하는 [HTL 스크립트](https://docs.adobe.com/content/help/ko-KR/experience-manager-htl/using/overview.html)를 재정의하여 수행됩니다. HTL(HTML Template Language)은 AEM 구성 요소가 작성된 컨텐츠를 기반으로 마크업을 동적으로 렌더링하는 데 사용하는 간단한 템플릿 언어로서 구성 요소를 다시 사용할 수 있도록 합니다. 예를 들어 제품 티저를 반복해서 사용하여 서로 다른 제품을 표시할 수 있습니다.

이 경우 티저 위에 배너를 렌더링하여 제품이 사용자 지정 속성에 따라 &quot;친환경&quot;임을 표시하려고 합니다. 구성 요소의 [마크업](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/customizing.html#customizing-the-markup)에 대한 디자인 패턴은 AEM CIF 코어 구성 요소뿐만 아니라 모든 AEM 구성 요소에 실제로 표준입니다.

1. IDE에서 `ui.apps` 모듈을 탐색하고 확장하고 폴더 계층 구조를 다음으로 확장합니다.`ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser` 및 `.content.xml` 파일을 검사합니다.

   ![제품 티저 ui.apps](../assets/customize-cif-components/product-teaser-ui-apps-ide.png)

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:description="Product Teaser Component"
       jcr:primaryType="cq:Component"
       jcr:title="Product Teaser"
       sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"
       componentGroup="Venia - Commerce"/>
   ```

   이상은 프로젝트의 제품 티저 구성 요소에 대한 구성 요소 정의입니다. `sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"` 속성을 확인합니다. [프록시 구성 요소](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/get-started/using.html#create-proxy-components)를 만드는 예입니다. AEM CIF 코어 구성 요소에서 모든 제품 티저 HTL 스크립트를 복사하여 붙여넣는 대신 `sling:resourceSuperType` 을 사용하여 모든 기능을 상속할 수 있습니다.

1. `productteaser.html` 파일을 엽니다. [CIF 제품 티저](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/productteaser.html)의 `productteaser.html` 파일 사본입니다.

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

   `MyProductTeaser`에 대한 Sling 모델이 사용되고 `product` 변수에 할당됩니다.

1. 이전 연습에서 구현된 `isEcoFriendly` 메서드를 호출하려면 `productteaser.html` 을 수정합니다.

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

   HTL에서 Sling Model 메서드를 호출할 때 메서드의 `get` 및 `is` 부분이 삭제되고 첫 번째 문자가 소문자로 표시됩니다. 따라서 `isShowBadge()`은 `.showBadge`이 되고 `isEcoFriendly`는 `.ecoFriendly`이 됩니다. `.isEcoFriendly()`에서 반환된 부울 값을 기반으로 하여 `<span>Eco Friendly</span>`이 표시되는지 확인합니다.

   `data-sly-test` 및 기타 [HTL 블록 문에 대한 자세한 내용은 여기](https://docs.adobe.com/content/help/en/experience-manager-htl/using/htl/block-statements.html#test)에서 확인할 수 있습니다.

1. 명령줄 터미널에서 Maven 기술을 사용하여 변경 사항을 저장하고 AEM에 업데이트를 배포합니다.

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. 새 브라우저 창을 열고 AEM 및 **OSGi 콘솔** > **상태** > **Sling 모델**&#x200B;으로 이동합니다.[http://localhost:4502/system/console/status-slingmodels](http://localhost:4502/system/console/status-slingmodels)

1. `MyProductTeaserImpl`을 검색하면 다음과 같은 줄이 표시됩니다.

   ```plain
   com.venia.core.models.commerce.MyProductTeaserImpl - venia/components/commerce/productteaser
   ```

   이는 Sling 모델이 제대로 배포되어 올바른 구성 요소에 매핑되었음을 나타냅니다.

1. [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)에서 제품 티저가 추가된 **Venia 홈 페이지**&#x200B;로 새로 고칩니다.

   ![친환경 메시지 표시](../assets/customize-cif-components/eco-friendly-text-displayed.png)

   제품의 `eco_friendly` 속성이 **Yes**&#x200B;로 설정된 경우 페이지에 &quot;Eco Friendly&quot; 텍스트가 표시됩니다. 동작 변경을 보려면 다른 제품으로 전환해 보십시오.

1. 다음으로 AEM `error.log`을 열어 추가한 로그 문을 확인합니다. `error.log`은 `<AEM SDK Install Location>/crx-quickstart/logs/error.log`에 있습니다.

   AEM 로그를 검색하여 Sling 모델에 추가된 로그 문을 확인합니다.

   ```plain
   2020-08-28 12:57:03.114 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is Eco Friendly**
   ...
   2020-08-28 13:01:00.271 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is not Eco Friendly**
   ...
   ```

   >[!CAUTION]
   >
   > Teaser에 사용된 제품에 속성 집합의 일부로 `eco_friendly` 속성이 없는 경우 일부 스택 추적이 표시될 수도 있습니다.

## 친환경 배지 {#add-styles}에 대한 스타일 추가

이때 **친환경** 배지를 표시할 시점에 대한 논리가 작동하지만 일반 텍스트에서는 일부 스타일을 사용할 수 있습니다. 그런 다음 `ui.frontend` 모듈에 아이콘 및 스타일을 추가하여 구현을 완료합니다.

1. [eco_friendly.svg](../assets/customize-cif-components/eco_friendly.svg) 파일을 다운로드합니다. 이 배지는 **친환경** 배지로 사용됩니다.
1. IDE로 돌아가서 `ui.frontend` 폴더로 이동합니다.
1. `ui.frontend/src/main/resources/images` 폴더에 `eco_friendly.svg` 파일을 추가합니다.

   ![친환경 SVG 추가](../assets/customize-cif-components/eco-friendly-svg-added.png)

1. `ui.frontend/src/main/styles/commerce/_productteaser.scss`에서 `productteaser.scss` 파일을 엽니다.
1. `.productteaser` 클래스 내에 다음 Sass 규칙을 추가합니다.

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
   > 프런트 엔드 워크플로우에 대한 자세한 내용은 [CIF 코어 구성 요소 스타일 지정](./style-cif-component.md)을 참조하십시오.

1. 명령줄 터미널에서 Maven 기술을 사용하여 변경 사항을 저장하고 AEM에 업데이트를 배포합니다.

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)에서 제품 티저가 추가된 **Venia 홈 페이지**&#x200B;로 새로 고칩니다.

   ![친환경 배지 최종 구현](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## 축하합니다 {#congratulations}

첫 번째 AEM CIF 구성 요소를 사용자 지정했을 뿐입니다. 완료된 솔루션 파일을 여기](../assets/customize-cif-components/customize-cif-component-SOLUTION_FILES.zip)에 다운로드하십시오.[

## 보너스 챌린지 {#bonus-challenge}

제품 티저에 이미 구현된 **새** 배지의 기능을 검토하십시오. 작성자가 **친환경** 배지가 표시되는 시기를 제어할 수 있도록 추가 확인란을 추가해 보십시오. `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser/_cq_dialog/.content.xml`에서 구성 요소 대화 상자를 업데이트해야 합니다.

![새로운 배지 구현 문제](../assets/customize-cif-components/new-badge-implementation-challenge.png)

## 추가 리소스 {#additional-resources}

- [AEM Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)
- [AEM CIF 코어 구성 요소](https://github.com/adobe/aem-core-cif-components)
- [AEM CIF 핵심 구성 요소 사용자 정의](https://github.com/adobe/aem-core-cif-components/wiki/Customizing-CIF-Core-Components)
- [핵심 구성 요소 사용자 정의](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html)
- [AEM Sites 시작하기](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)
