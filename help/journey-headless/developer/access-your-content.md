---
title: AEM 배달 API를 통해 콘텐츠에 액세스하는 방법
description: AEM 헤드리스 개발자 여정의 이 부분에서 GraphQL 쿼리를 사용하여 컨텐츠 조각 컨텐츠에 액세스하는 방법을 알아봅니다.
source-git-commit: 7f43d9d6b631b26f7b9293aa109498d0c8040436
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 1%

---

# AEM 배달 API를 통해 콘텐츠에 액세스하는 방법 {#access-your-content}

의 이 부분에서 [AEM Headless Developer 여정,](overview.md) GraphQL 쿼리를 사용하여 컨텐츠 조각의 컨텐츠에 액세스하고 이를 앱에 제공하는 방법(헤드리스 게재)을 배울 수 있습니다.

## 지금까지 그 이야기 {#story-so-far}

AEM 헤드리스 여정의 이전 문서에서, [컨텐츠를 모델링하는 방법](model-your-content.md) AEM에서 컨텐츠 모델링의 기본 사항을 배웠으므로 이제 컨텐츠 구조를 모델링하는 방법을 이해하고 AEM 컨텐츠 조각 모델 및 컨텐츠 조각을 사용하여 해당 구조를 실현해야 합니다.

* 컨텐츠 모델링과 관련된 개념과 용어를 인식합니다.
* 헤드리스 컨텐츠 전달에 컨텐츠 모델링이 필요한 이유를 이해합니다.
* AEM 컨텐츠 조각 모델(및 컨텐츠 조각으로 컨텐츠 작성)을 사용하여 이 구조를 구현하는 방법을 이해합니다.
* 컨텐츠를 모델링하는 방법을 이해합니다. 기본 샘플을 사용하는 원칙.

이 문서는 AEM GraphQL API를 사용하여 AEM에서 기존 헤드리스 컨텐츠에 액세스하는 방법을 이해할 수 있도록 이러한 기본 사항을 기반으로 합니다.

* **Audience**: 초보
* **목표**: AEM GraphQL 쿼리를 사용하여 컨텐츠 조각의 컨텐츠에 액세스하는 방법을 알아봅니다.
   * GraphQL 및 AEM GraphQL API를 도입합니다.
   * AEM GraphQL API에 대한 세부 사항을 살펴봅니다.
   * 몇 가지 샘플 쿼리를 보고 실제 작동 방식을 확인합니다.

## 콘텐츠를 액세스하시겠습니까? {#so-youd-like-to-access-your-content}

그래서..이 모든 컨텐츠가 깔끔하게 구조화되어 있으며(컨텐츠 조각에서) 새 앱의 피드를 기다리고 있습니다. 문제는, 어떻게 그것을 그곳에 가져다 놓는가 입니다.

필요한 것은 특정 컨텐츠를 타깃팅하고, 필요한 항목을 선택하고, 추가 처리를 위해 앱에 반환하는 방법입니다.

AEM(Adobe Experience Manager)을 사용하면 AEM GraphQL API를 사용하여 컨텐츠 조각에 선택적으로 액세스하여 필요한 컨텐츠만 반환할 수 있습니다. 즉, 애플리케이션에서 사용할 구조화된 컨텐츠의 헤드리스 전달을 실현할 수 있습니다.

>[!NOTE]
>
>AEM GraphQL API는 표준 GraphQL API 사양을 기반으로 하는 사용자 지정된 구현입니다.

## GraphQL - 소개 {#graphql-introduction}

GraphQL은 다음과 같은 기능을 제공하는 오픈 소스 사양입니다.

* 구조화된 객체에서 특정 컨텐츠를 선택할 수 있는 질의 언어입니다.
* 구조화된 컨텐츠로 이러한 쿼리를 이행하는 런타임.

GraphQL은 *강하게* 형식화된 API. 이것은 *모두* GraphQL이 가능하도록 컨텐츠를 명확하게 구조화하고 유형별로 구성해야 합니다 *이해* 액세스 방법 및 방법. 데이터 필드는 컨텐츠 객체의 구조를 정의하는 GraphQL 스키마 내에 정의됩니다.

그런 다음 GraphQL 종단점은 GraphQL 쿼리에 응답하는 경로를 제공합니다.

즉, AEM에서 사용할 때 필요한 콘텐츠만 앱에서 정확하고 안정적으로 선택할 수 있습니다.

>[!NOTE]
>
>자세한 내용은 *GraphQL*.org 및 *GraphQL*.com

<!--
## AEM and GraphQL {#aem-graphql}

GraphQL is used in various locations in AEM; for example:

* Content Fragments
  * A customized API has been developed for this use-case (Headless Delivery to your app).
    * This is the AEM GraphQL API.
* Commerce
  * AEM Commerce consumes data from a Commerce platform via GraphQL.
  * There are GraphQL integrations between AEM and various third-party commerce solutions, used with the extension hooks provided by the CIF Core Components.
    * This does not use the AEM GraphQL API.

>[!NOTE]
>
>This step of the Headless Journey is only concerned with the AEM GraphQL API and Content Fragments.
-->

## AEM GraphQL API {#aem-graphql-api}

AEM GraphQL API는 컨텐츠 조각에 대해 (복잡한) 쿼리를 수행할 수 있도록 특별히 구성된 표준 GraphQL API 사양을 기반으로 사용자 지정된 버전입니다.

컨텐츠가 컨텐츠 조각 모델에 따라 구조화되므로 컨텐츠 조각이 사용됩니다. GraphQL의 기본 요구 사항을 충족합니다.

* 컨텐츠 조각 모델은 하나 이상의 필드로 구성됩니다.
   * 각 필드는 데이터 유형에 따라 정의됩니다.
* 컨텐츠 조각 모델은 해당 AEM GraphQL 스키마를 생성하는 데 사용됩니다.

GraphQL for AEM(및 컨텐츠)에 실제로 액세스하려면 종단점이 액세스 경로를 제공하는 데 사용됩니다.

AEM GraphQL API를 통해 반환된 콘텐츠는 애플리케이션에서 사용할 수 있습니다.

쿼리를 직접 입력하고 테스트하는 데 도움이 되도록 표준 GraphiQL 인터페이스 구현도 AEM GraphQL에서 사용할 수 있습니다(AEM에서 설치할 수 있음). 여기에는 내역 및 온라인 설명서와 함께 구문 강조, 자동 완료, 자동 제안 등의 기능이 제공됩니다.

>[!NOTE]
>
>AEM GraphQL API 구현은 GraphQL Java 라이브러리를 기반으로 합니다.

<!--
### Use Cases for Author and Publish Environments {#use-cases-author-publish-environments}

The use cases for the AEM GraphQL API can depend on the type of AEMenvironment:

* Publish environment; used to: 
  * Query content for JS application (standard use-case)

* Author environment; used to: 
  * Query content for "content management purposes":
    * GraphQL in AEM is currently a read-only API.
    * The REST API can be used for CR(u)D operations.
-->

## AEM GraphQL API에서 사용할 컨텐츠 조각 {#content-fragments-use-with-aem-graphql-api}

컨텐츠 조각은 다음과 같이 AEM 스키마 및 쿼리를 위한 GraphQL의 기반으로 사용할 수 있습니다.

* 이 구성 요소를 사용하면 헤드라인으로 전달할 수 있는 페이지에 영향을 받지 않는 컨텐츠를 디자인, 제작, 조정 및 게시할 수 있습니다.
* 이 모델은 데이터 유형을 선택하여 결과 조각의 구조를 사전 정의하는 컨텐츠 조각 모델을 기반으로 합니다.
* 모델을 정의할 때 사용할 수 있는 조각 참조 데이터 유형으로 추가 구조 계층을 수행할 수 있습니다.

### 컨텐츠 조각 모델 {#content-fragments-models}

이러한 컨텐츠 조각 모델:

* 스키마를 생성하는 데 한 번 사용됩니다 **활성화됨**.
* GraphQL에 필요한 데이터 유형과 필드를 제공합니다. 이 URL은 응용 프로그램이 가능한 요청만 하고 예상 내용을 수신하도록 합니다.
* 데이터 유형 **조각 참조** 모델에서 다른 컨텐츠 조각을 참조하여 추가 구조 수준을 도입할 수 있습니다.

### 조각 참조 {#fragment-references}

다음 **조각 참조**:

* 컨텐츠 조각 모델을 정의할 때 사용할 수 있는 특정 데이터 유형입니다.
* 특정 컨텐츠 조각 모델에 따라 다른 조각을 참조합니다.
* 구조화된 데이터를 만든 다음 검색할 수 있습니다.

   * 로 정의된 경우 **다중 피드**&#x200B;를 채울 경우 하위 조각에서 여러 하위 조각을 참조(검색)할 수 있습니다.

### JSON 미리 보기 {#json-preview}

컨텐츠 조각 모델을 디자인하고 개발하는 데 도움이 되도록 컨텐츠 조각 편집기에서 JSON 출력을 미리 볼 수 있습니다.

![JSON 미리 보기](assets/cfm-model-json-preview.png "JSON 미리 보기")

<!--
## GraphQL Schema Generation from Content Fragments {#graphql-schema-generation-content-fragments}

GraphQL is a strongly typed API, which means that content must be clearly structured and organized by type. The GraphQL specification provides a series of guidelines on how to create a robust API for interrogating content on a certain instance. To do this, a client needs to fetch the Schema, which contains all the types necessary for a query. 

For Content Fragments, the GraphQL schemas (structure and types) are based on **Enabled** Content Fragment Models and their data types.

>[!CAUTION]
>
>All the GraphQL schemas (derived from Content Fragment Models that have been **Enabled**) are readable through the GraphQL endpoint.
>
>This means that you need to ensure that no sensitive content is available, to ensure that no sensitive data is exposed via GraphQL endpoints; for example, this includes information that could be present as field names in the model definition.

For example, if a user created a Content Fragment Model called `Article`, then AEM generates the object `article` that is of a type `ArticleModel`. The fields within this type correspond to the fields and data types defined in the model.

1. A Content Fragment Model:

   ![Content Fragment Model for use with GraphQL](assets/graphqlapi-cfmodel.png "Content Fragment Model for use with GraphQL")

1. The corresponding GraphQL schema (output from GraphiQL automatic documentation):
   ![GraphQL Schema based on Content Fragment Model](assets/graphqlapi-cfm-schema.png "GraphQL Schema based on Content Fragment Model")

   This shows that the generated type `ArticleModel` contains several [fields](#fields). 
   
   * Three of them have been controlled by the user: `author`, `main` and `referencearticle`.

   * The other fields were added automatically by AEM, and represent helpful methods to provide information about a certain Content Fragment; in this example, `_path`, `_metadata`, `_variations`. These [helper fields](#helper-fields) are marked with a preceding `_` to distinguish between what has been defined by the user and what has been auto-generated.

1. After a user creates a Content Fragment based on the Article model, it can then be interrogated through GraphQL. For examples, see the Sample Queries.md#graphql-sample-queries) (based on a sample Content Fragment structure for use with GraphQL.

In GraphQL for AEM, the schema is flexible. This means that it is auto-generated each and every time a Content Fragment Model is created, updated or deleted. The data schema caches are also refreshed when you update a Content Fragment Model.

The Sites GraphQL service listens (in the background) for any modifications made to a Content Fragment Model. When updates are detected, only that part of the schema is regenerated. This optimization saves time and provides stability.

So for example, if you:

1. Install a package containing `Content-Fragment-Model-1` and `Content-Fragment-Model-2`:
 
   1. GraphQL types for `Model-1` and `Model-2` will be generated.

1. Then modify `Content-Fragment-Model-2`:

   1. Only the `Model-2` GraphQL type will get updated.

   1. Whereas `Model-1` will remain the same. 

>[!NOTE]
>
>This is important to note in case you want to do bulk updates on Content Fragment Models through the REST api, or otherwise.

The schema is served through the same endpoint as the GraphQL queries, with the client handling the fact that the schema is called with the extension `GQLschema`. For example, performing a simple `GET` request on `/content/cq:graphql/global/endpoint.GQLschema` will result in the output of the schema with the Content-type: `text/x-graphql-schema;charset=iso-8859-1`.

### Schema Generation - Unpublished Models {#schema-generation-unpublished-models}

When Content Fragments are nested it can happen that a parent Content Fragment Model is published, but a referenced model is not.

>[!NOTE]
>
>The AEM UI prevents this happening, but if publishing is made programmatically, or with content packages, it can occur.

When this happens, AEM generates an *incomplete* Schema for the parent Content Fragment Model. This means that the Fragment Reference, which is dependent on the unpublished model, is removed from the schema.

## AEM GraphQL Endpoints {#aem-graphql-endpoints}

An endpoint is the path used to access GraphQL for AEM. Using this path you (or your app) can:

* access the GraphQL schemas,
* send your GraphQL queries,
* receive the responses (to your GraphQL queries).

AEM allows for:

* A global endpoint - available for use by all sites.
* Endpoints for specific Sites configurations - that you can configure (in the Configuration Browser), specific to a specified site/project.

## Permissions {#permissions}

The permissions are those required for accessing Assets.

## The AEM GraphiQL Interface {#aem-graphiql-interface}

To help you directly input, and test queries, an implementation of the standard GraphiQL interface is available for use with AEM GraphQL. This can be installed with AEM.

>[!NOTE]
>
>GraphiQL is bound the global endpoint (and does not work with other endpoints for specific Sites configurations).

It provides features such as syntax-highlighting, auto-complete, auto-suggest, together with a history and online documentation.

![GraphiQL Interface](assets/graphiql-interface.png "GraphiQL Interface")
-->

## 실제로 AEM GraphQL API 사용 {#actually-using-aem-graphiql}

### 초기 설정 {#initial-setup}

컨텐츠에 대한 쿼리를 시작하기 전에 다음을 수행해야 합니다.

* 엔드포인트 활성화
   * 도구 -> 자산 -> GraphQL 사용
   * [GraphQL 끝점 활성화](/help/assets/content-fragments/graphql-api-content-fragments.md#enabling-graphql-endpoint)

* GraphiQL 설치(필요한 경우)
   * 전용 패키지로 설치됨
   * [AEM GraphiQL 인터페이스 설치](/help/assets/content-fragments/graphql-api-content-fragments.md#installing-graphiql-interface)

### 샘플 구조 {#sample-structure}

쿼리에서 AEM GraphQL API를 실제로 사용하려면 두 가지 매우 기본적인 컨텐츠 조각 모델 구조를 사용할 수 있습니다.

* 회사
   * 이름 - 텍스트
   * CEO(개인) - 조각 참조
   * 사원(개인) - 조각 참조
* 개인
   * 이름 - 텍스트
   * 이름 - 텍스트

볼 수 있듯이 CEO 및 Employees 필드는 Person 조각을 참조합니다.

조각 모델은 다음과 같이 사용됩니다.

* 컨텐츠 조각 편집기에서 컨텐츠를 만들 때
* 쿼리할 GraphQL 스키마를 생성하기 위해

### 쿼리를 테스트할 위치 {#where-to-test-your-queries}

쿼리는 GraphiQL 인터페이스에 입력할 수 있습니다. 예를 들면 다음과 같습니다.

* `http://localhost:4502/content/graphiql.html`

![GraphiQL 인터페이스](assets/graphiql-interface.png "GraphiQL 인터페이스")

### 쿼리 시작 {#getting-Started-with-queries}

간단한 쿼리는 회사 스키마에 있는 모든 항목의 이름을 반환하는 것입니다. 여기에서 모든 회사 이름 목록을 요청합니다.

```xml
query {
  companyList {
    items {
      name
    }
  }
}
```

약간 더 복잡한 쿼리는 &quot;Jobs&quot;라는 이름이 없는 모든 사람을 선택하는 것입니다. Job이라는 이름이 없는 모든 사용자에 대해 모든 사용자를 필터링합니다. 이는 EQUALS_NOT 연산자로 달성됩니다(더 많은 항목이 있음).

```xml
query {
  personList(filter: {
    name: {
      _expressions: [
        {
          value: "Jobs"
          _operator: EQUALS_NOT
        }
      ]
    }
  }) {
    items {
      name
      firstName
    }
  }
}
```

더 복잡한 쿼리를 작성할 수도 있습니다. 예를 들어 &quot;Smith&quot;라는 이름을 가진 직원이 하나 이상 있는 모든 회사를 질의합니다. 이 쿼리는 이름이 &quot;Smith&quot;인 모든 사용자에 대한 필터링을 보여주며 중첩된 조각에서 정보를 반환합니다.

```xml
query {
  companyList(filter: {
    employees: {
      _match: {
        name: {
          _expressions: [
            {
              value: "Smith"
            }
          ]
        }
      }
    }
  }) {
    items {
      name
      ceo {
        name
        firstName
      }
      employees {
        name
        firstName
      }
    }
  }
}
```

<!-- need code / curl / cli examples-->

AEM GraphQL API 사용에 대한 전체 세부 사항과 필요한 요소 구성에 대해 다음을 참조할 수 있습니다.

* AEM에서 GraphQL을 사용하는 방법 학습
* 샘플 컨텐츠 조각 구조
* AEM에서 GraphQL을 사용하는 방법 학습 - 샘플 컨텐츠 및 쿼리

## 다음은 무엇입니까? {#whats-next}

이제 AEM GraphQL API를 사용하여 헤드리스 컨텐츠에 액세스하고 쿼리하는 방법을 알아보았습니다 [rest API를 사용하여 컨텐츠 조각에 액세스하고 업데이트하는 방법을 알아봅니다](update-your-content.md).

## 추가 리소스 {#additional-resources}

* [GraphQL.org](https://graphql.org)
   * [스키마](https://graphql.org/learn/schema/)
   * [변수](https://graphql.org/learn/queries/#variables)
   * [GraphQL Java 라이브러리](https://graphql.org/code/#java)
* [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql)
* [AEM에서 GraphQL을 사용하는 방법 학습](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * [GraphQL 끝점 활성화](/help/assets/content-fragments/graphql-api-content-fragments.md#enabling-graphql-endpoint)
   * [AEM GraphiQL 인터페이스 설치](/help/assets/content-fragments/graphql-api-content-fragments.md#installing-graphiql-interface)
* [샘플 컨텐츠 조각 구조](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)
* [AEM에서 GraphQL을 사용하는 방법 학습 - 샘플 컨텐츠 및 쿼리](/help/assets/content-fragments/content-fragments-graphql-samples.md)
   * [샘플 쿼리 - 단일 특정 도시 조각](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-specific-city-fragment)
   * [메타데이터에 대한 샘플 쿼리 - GB라는 이름의 시상식에 대한 메타데이터 나열](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb)
   * [샘플 쿼리 - 명명된 변형을 가진 모든 도시](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation)
* [구성 브라우저에서 컨텐츠 조각 기능 활성화](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)
* [컨텐츠 조각을 사용한 작업](/help/assets/content-fragments/content-fragments.md)
   * [컨텐츠 조각 모델](/help/assets/content-fragments/content-fragments-models.md)
   * [JSON 출력](/help/assets/content-fragments/content-fragments-json-preview.md)
* [CORS(원본 간 리소스 공유) 이해](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=en#understand-cross-origin-resource-sharing-(cors))
* [AEM Headless 시작하기](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) - 컨텐츠 모델링 및 GraphQL을 포함하여 AEM 헤드리스 기능을 사용하는 방법에 대한 개요를 제공하는 짧은 비디오 자습서 시리즈입니다.

<!--
* [Generating Access Tokens for Server Side APIs](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)
-->
