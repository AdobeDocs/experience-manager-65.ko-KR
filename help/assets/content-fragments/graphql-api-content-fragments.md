---
title: 콘텐츠 조각과 함께 사용하기 위한 AEM GraphQL API
description: 헤드리스 컨텐츠 전달을 위해 AEM(Adobe Experience Manager)에서 AEM GraphQL API와 함께 컨텐츠 조각을 사용하는 방법을 알아봅니다.
feature: Content Fragments,GraphQL API
exl-id: beae1f1f-0a76-4186-9e58-9cab8de4236d
source-git-commit: 6f3f88ea0f07c97fa8d7ff3bdd1c89114d12a8a1
workflow-type: tm+mt
source-wordcount: '3986'
ht-degree: 91%

---

# 콘텐츠 조각과 함께 사용하기 위한 AEM GraphQL API {#graphql-api-for-use-with-content-fragments}

헤드리스 컨텐츠 전달을 위해 AEM(Adobe Experience Manager)에서 AEM GraphQL API와 함께 컨텐츠 조각을 사용하는 방법을 알아봅니다.

Content Fragments와 함께 사용되는 AEM GraphQL API는 표준 오픈 소스 GraphQL API를 기반으로 합니다.

AEM에서 GraphQL API를 사용하면 Headless CMS 구현에서 JavaScript 클라이언트에 콘텐츠 조각을 효율적으로 전달할 수 있습니다.

* REST에서처럼 반복적인 API 요청 방지,
* 전달이 특정 요구 사항으로 제한되는지 확인,
* 단일 API 쿼리에 대한 응답으로 렌더링에 필요한 것을 정확히 대량으로 전달할 수 있도록 허용.

>[!NOTE]
>
>GraphQL은 현재 Adobe Experience Manager(AEM)의 두 가지(별도) 시나리오에서 사용됩니다.
>
>* [AEM Commerce는 GraphQL을 통해 상거래 플랫폼의 데이터를 사용합니다](/help/commerce/cif/integrating/magento.md).
>* AEM 콘텐츠 조각은 AEM GraphQL API(표준 GraphQL 기반의 맞춤화된 구현)와 함께 작동하여 애플리케이션에서 사용할 구조화된 콘텐츠를 제공합니다.


## GraphQL API {#graphql-api}

GraphQL은

* “*...API용 쿼리 언어 및 기존 데이터로 이러한 쿼리를 수행하기 위한 런타임입니다. GraphQL은 API의 데이터에 대한 완전하고 이해하기 쉬운 설명을 제공하고, 클라이언트가 필요로 하는 것을 정확히 요청할 수 있는 권한을 주고, 시간이 지남에 따라 API를 더 쉽게 발전시킬 수 있으며, 강력한 개발자 도구를 지원합니다.*”.

   [GraphQL.org](https://graphql.org)를 참조하십시오.

* “*...유연한 API 계층을 위한 오픈 사양입니다. 기존 백엔드에 GraphQL을 추가하여 그 어느 때보다 빠르게 제품을 빌드할 수 있습니다.*”

   [GraphQL 살펴보기](https://www.graphql.com)를 참조하십시오.

* *“...2015년에 오픈 소스로 공개되기 전에 2012년 Facebook에서 내부적으로 개발한 데이터 쿼리 언어 및 사양입니다. 개발자 생산성을 높이고 전송되는 데이터 양을 최소화할 목적으로 REST 기반 아키텍처에 대한 대안을 제공합니다. GraphQL은 규모에 관계없이 수백 개의 조직에서 프로덕션에 사용됩니다.”*

   [GraphQL Foundation](https://foundation.graphql.org/)을 참조하십시오.

<!--
"*Explore GraphQL is maintained by the Apollo team. Our goal is to give developers and technical leaders around the world all of the tools they need to understand and adopt GraphQL.*". 
-->

GraphQL API에 대한 추가 정보는 기타 여러 리소스 중에서도 특히 다음 섹션을 참조하십시오.

* [graphql.org](https://graphql.org):

   * [GraphQL 소개](https://graphql.org/learn)

   * [GraphQL 사양](https://spec.graphql.org/)

* [graphql.com](https://graphql.com):

   * [안내서](https://www.graphql.com/guides/)

   * [튜토리얼](https://www.graphql.com/tutorials/)

   * [사례 연구](https://www.graphql.com/case-studies/)

AEM용 GraphQL 구현은 표준 GraphQL Java 라이브러리를 기반으로 합니다. 다음을 참조하십시오.

* [graphQL.org - Java](https://graphql.org/code/#java)

* [GitHub의 GraphQL Java](https://github.com/graphql-java)

### GraphQL 용어 {#graphql-terminology}

GraphQL은 다음 용어를 사용합니다.

* **[쿼리](https://graphql.org/learn/queries/)**

* **[스키마 및 유형](https://graphql.org/learn/schema/)**:

   * 스키마는 콘텐츠 조각 모델을 기반으로 AEM에서 생성됩니다.
   * 스키마를 사용하여 GraphQL은 AEM용 GraphQL 구현에 허용되는 유형 및 작업을 제공합니다.

* **[필드](https://graphql.org/learn/queries/#fields)**

* **[GraphQL 끝점](#graphql-aem-endpoint)**
   * GraphQL 쿼리에 응답하고 GraphQL 스키마에 대한 액세스를 제공하는 AEM의 경로입니다.

   * 자세한 내용은 [GraphQL 끝점 활성화](#enabling-graphql-endpoint)를 참조하십시오.

[모범 사례](https://graphql.org/learn/best-practices/)를 포함한 포괄적인 세부 정보는 [(GraphQL.org) GraphQL 소개](https://graphql.org/learn/)를 참조하십시오.

### GraphQL 쿼리 유형 {#graphql-query-types}

GraphQL을 사용하여 다음 중 하나를 반환하는 쿼리를 수행할 수 있습니다.

* **단일 항목**

* **[항목 목록](https://graphql.org/learn/schema/#lists-and-non-null)**

다음 작업도 수행할 수 있습니다.

* [캐시된 지속 쿼리](#persisted-queries-caching)

>[!NOTE]
>[GraphiQL IDE](#graphiql-interface)를 사용하여 GraphQL 쿼리를 테스트하고 디버그할 수 있습니다.

## AEM 종단점에 대한 GraphQL {#graphql-aem-endpoint}

끝점은 AEM용 GraphQL에 액세스하는 데 사용되는 경로입니다. 이 경로를 사용하여 사용자(또는 앱)는 다음과 같은 작업을 수행할 수 있습니다.

* GraphQL 스키마에 액세스,
* GraphQL 쿼리 보내기,
* (GraphQL 쿼리에 대한) 응답 받기.

AEM에는 두 가지 유형의 끝점이 있습니다.

* 전역
   * 모든 사이트에서 사용할 수 있습니다.
   * 이 끝점은 모든 Sites 구성의 모든 콘텐츠 조각 모델을 사용할 수 있습니다([구성 브라우저](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)에 정의됨).
   * Sites 구성 간에 공유해야 하는 콘텐츠 조각 모델이 있는 경우 전역 Sites 구성에서 생성해야 합니다.
* Sites 구성:
   * [구성 브라우저](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)에 정의된 Sites 구성에 해당합니다.
   * 지정된 사이트/프로젝트에만 해당됩니다.
   * Sites 구성 특정 끝점은 해당 특정 Sites 구성의 콘텐츠 조각 모델을 전역 Sites 구성의 콘텐츠 조각 모델과 함께 사용합니다.

>[!CAUTION]
>
>콘텐츠 조각 편집기는 한 Sites 구성의 콘텐츠 조각이 다른 Sites 구성의 콘텐츠 조각을 참조하도록 허용할 수 있습니다(정책을 통해).
>
>이러한 경우 Sites 구성 특정 끝점을 사용하여 모든 콘텐츠를 검색할 수 있는 것은 아닙니다.
>
>콘텐츠 작성자가 이 시나리오를 제어해야 합니다. 예를 들어 공유 콘텐츠 조각 모델을 전역 Sites 구성 아래에 두는 것이 유용할 수 있습니다.

AEM용 GraphQL 전역 끝점의 저장소 경로는 다음과 같습니다.

`/content/cq:graphql/global/endpoint`

앱이 요청 URL에서 다음 경로를 사용할 수 있는 경우:

`/content/_cq_graphql/global/endpoint.json`

AEM용 GraphQL의 끝점을 활성화하려면 다음 작업을 수행해야 합니다.

* [GraphQL 끝점 활성화](#enabling-graphql-endpoint)
* [GraphQL 끝점 게시](#publishing-graphql-endpoint)

### GraphQL 끝점 활성화하기 {#enabling-graphql-endpoint}

GraphQL 끝점을 활성화하려면 먼저 적절한 구성이 필요합니다. [콘텐츠 조각 - 구성 브라우저](/help/assets/content-fragments/content-fragments-configuration-browser.md)를 참조하십시오.

>[!CAUTION]
>
>[콘텐츠 조각 모델 사용이 활성화되지 않은](/help/assets/content-fragments/content-fragments-configuration-browser.md) 경우 **만들기** 옵션을 사용할 수 없습니다.

해당 끝점을 활성화하려면 다음을 수행하십시오.

1. **도구**, **에셋**&#x200B;으로 이동한 다음 **GraphQL**&#x200B;을 선택합니다.
1. **만들기**&#x200B;를 선택합니다.
1. **새 GraphQL 끝점 만들기** 대화 상자가 열립니다. 여기에서 다음을 지정할 수 있습니다.
   * **이름**: 끝점의 이름입니다. 어떤 텍스트든 입력할 수 있습니다.
   * **다음에서 제공하는 GraphQL 스키마 사용**: 드롭다운을 사용하여 필요한 사이트/프로젝트를 선택합니다.

   >[!NOTE]
   >
   >다음 경고가 대화 상자에 표시됩니다.
   >
   >* *GraphQL 엔드포인트는 신중하게 관리하지 않을 경우 데이터 보안 및 성능 문제를 초래할 수 있습니다. 엔드포인트를 만든 후 적절한 사용 권한을 설정했는지 확인하십시오.*


1. **만들기**&#x200B;를 사용하여 확인합니다.
1. **다음 단계** 대화 상자는 보안 콘솔에 대한 직접 링크를 제공하므로 새로 생성된 끝점에 적절한 권한이 있는지 확인할 수 있습니다.

   >[!CAUTION]
   >
   >끝점은 모든 사용자가 액세스할 수 있습니다. 특히 게시 인스턴스에서, GraphQL 쿼리가 과도한 부하를 줄 수 있으므로 보안 문제가 발생할 수 있습니다.
   >
   >끝점에 사용 사례에 적합한 ACL을 설정할 수 있습니다.

### GraphQL 끝점 게시하기 {#publishing-graphql-endpoint}

새 끝점을 선택하고 **게시**&#x200B;를 선택하여 모든 환경에서 완전히 사용할 수 있도록 합니다.

>[!CAUTION]
>
>끝점은 모든 사용자가 액세스할 수 있습니다.
>
>게시 인스턴스에서 GraphQL 쿼리가 서버에 과부하를 줄 수 있으므로 보안 문제가 발생할 수 있습니다.
>
>끝점에 사용 사례에 적합한 ACL을 설정해야 합니다.

## GraphiQL 인터페이스 {#graphiql-interface}

표준 구현 [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) 인터페이스는 AEM GraphQL에서 사용할 수 있습니다. [AEM으로 설치](#installing-graphiql-interface)할 수 있습니다.

>[!NOTE]
>
>GraphiQL은 전역 끝점에 바인딩되어 있으며 특정 Sites 구성에 대한 다른 끝점에서는 작동하지 않습니다.

이 인터페이스를 사용하면 쿼리를 직접 입력 및 테스트할 수 있습니다.

예:

* `http://localhost:4502/content/graphiql.html`

기록 및 온라인 설명서와 함께 구문 강조, 자동 완성, 자동 제안과 같은 기능을 제공합니다.

![GraphiQL 인터페이스](assets/cfm-graphiql-interface.png "GraphiQL 인터페이스")

### AEM GraphiQL 인터페이스 설치 {#installing-graphiql-interface}

전용 패키지를 사용하여 AEM에 GraphiQL 사용자 인터페이스를 설치할 수 있습니다. a [GraphiQL 컨텐츠 패키지 v0.0.6(2021.3)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-graphql/graphiql-0.0.6.zip) 패키지.

>[!NOTE]
>
>사용 가능한 패키지는 AEM 6.5.10.0 및 AEM as a Cloud Service과 완벽하게 호환됩니다.

## Author 및 Publish 환경의 사용 사례 {#use-cases-author-publish-environments}

사용 사례는 AEM 환경의 유형에 따라 달라질 수 있습니다.

* Publish 환경, 다음과 같은 작업을 수행하는 데 사용됨:
   * JS 애플리케이션용 쿼리 데이터(표준 사용 사례)

* Author 환경, 다음과 같은 작업을 수행하는 데 사용됨:
   * “콘텐츠 관리 목적”용 쿼리 데이터:
      * AEM의 GraphQL은 현재 읽기 전용 API입니다.
      * REST API는 CR(u)D 작업에 사용할 수 있습니다.

## 권한 {#permission}

권한은 Assets에 액세스하는 데 필요한 권한입니다.

## 스키마 생성 {#schema-generation}

GraphQL은 강력한 형식의 API입니다. 즉, 데이터는 유형별로 명확하게 구조화되고 구성되어야 합니다.

GraphQL 사양은 특정 인스턴스에서 데이터의 정보를 얻기 위해 강력한 API를 만드는 방법에 대한 일련의 지침을 제공합니다. 이렇게 하려면 클라이언트가 쿼리에 필요한 모든 유형을 포함하는 [스키마](#schema-generation)를 가져와야 합니다.

콘텐츠 조각의 경우 GraphQL 스키마(구조 및 유형)는 **활성화됨** 상태인 [콘텐츠 조각 모델](/help/assets/content-fragments/content-fragments-models.md) 및 해당 데이터 형식을 기반으로 합니다.

>[!CAUTION]
>
>모든 GraphQL 스키마(**활성화됨**&#x200B;상태인 콘텐츠 조각 모델에서 파생)는 GraphQL 끝점을 통해 읽을 수 있습니다.
>
>즉, 이런 식으로 유출될 수 있기 때문에 민감한 데이터가 없는지 확인해야 합니다. 예를 들어 모델 정의에서 필드 이름으로 나타날 수 있는 정보가 여기에 포함됩니다.

예를 들어 사용자가 `Article`이라는 콘텐츠 조각 모델을 만든 경우 AEM은 `ArticleModel` 유형의 개체인 `article`을 생성합니다. 이 유형 내의 필드는 모델에서 정의된 필드 및 데이터 형식에 해당합니다.

1. 콘텐츠 조각 모델:

   ![GraphQL과 함께 사용하기 위한 콘텐츠 조각 모델](assets/cfm-graphqlapi-01.png "GraphQL과 함께 사용하기 위한 콘텐츠 조각 모델")

1. 해당 GraphQL 스키마(GraphiQL 자동 문서에서 출력):
   ![콘텐츠 조각 모델 기반 GraphQL 스키마](assets/cfm-graphqlapi-02.png "콘텐츠 조각 모델 기반 GraphQL 스키마")

   이는 생성된 유형 `ArticleModel`에 여러 [필드](#fields)가 포함되어 있음을 보여 줍니다.

   * 그 중 `author`, `main`, `referencearticle` 세 가지 필드는 사용자가 제어했습니다.

   * 다른 필드는 AEM에 의해 자동으로 추가되었으며 특정 콘텐츠 조각에 대한 정보를 제공하는 유용한 방법을 표시합니다. 이 예에서는 `_path`, `_metadata`, `_variations`입니다. 이 [도우미 필드](#helper-fields)는 사용자가 정의한 것과 자동 생성된 것을 구별하기 위해 앞에 `_` 로 표시됩니다.

1. 사용자가 Article 모델을 기반으로 콘텐츠 조각을 만든 경우 GraphQL을 통해 정보를 얻을 수 있습니다. 예를 들어 [샘플 쿼리](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries)([GraphQL과 함께 사용하기 위한 샘플 콘텐츠 조각 구조](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql) 기반)를 참조하십시오.

AEM용 GraphQL에서 스키마는 유연합니다. 즉, 콘텐츠 조각 모델이 만들어지거나 업데이트되거나 삭제될 때마다 자동 생성됩니다. 콘텐츠 조각 모델을 업데이트할 때도 데이터 스키마 캐시가 새로 고쳐집니다.

Sites GraphQL 서비스는 콘텐츠 조각 모델에 대한 수정 사항을 백그라운드에서 수신 대기합니다. 업데이트가 감지되면 스키마의 해당 부분만 다시 생성됩니다. 이 최적화는 시간을 절약하고 안정성을 제공합니다.

예를 들어:

1. `Content-Fragment-Model-1` 및 `Content-Fragment-Model-2`가 포함된 패키지를 설치하는 경우:

   1. `Model-1` 및 `Model-2` 에 대한 GraphQL 유형이 생성됩니다.

1. 그리고 `Content-Fragment-Model-2`를 수정하는 경우:

   1. `Model-2` GraphQL 유형만 업데이트됩니다.

   1. `Model-1`은 그대로 유지됩니다.

>[!NOTE]
>
>REST API 또는 다른 방법을 통해 콘텐츠 조각 모델에 대한 대량 업데이트를 수행하려는 경우에 주의해야 합니다.

스키마는 GraphQL 쿼리와 동일한 끝점을 통해 제공되며 스키마가 확장자 `GQLschema`로 호출되는 것을 처리하는 클라이언트가 있습니다. 예를 들어 `/content/cq:graphql/global/endpoint.GQLschema`에 대해 간단한 `GET` 요청을 수행하면 콘텐츠 유형이 있는 스키마의 출력이 됩니다. `text/x-graphql-schema;charset=iso-8859-1`.

### 스키마 생성 - 게시되지 않은 모델 {#schema-generation-unpublished-models}

콘텐츠 조각이 중첩되면 상위 콘텐츠 조각 모델은 게시되지만 참조된 모델은 게시되지 않을 수 있습니다.

>[!NOTE]
>
>AEM UI는 이러한 일이 발생하지 않도록 방지하지만 게시가 프로그래밍 방식으로 또는 콘텐츠 패키지를 사용하여 수행되는 경우 발생할 수 있습니다.

이런 일이 발생하면 AEM은 상위 콘텐츠 조각 모델에 대해 *불완전* 스키마를 생성합니다. 즉, 게시되지 않은 모델에 종속된 조각 참조가 스키마에서 제거됩니다.

## 필드 {#fields}

스키마 내에는 다음과 같은 두 가지 기본 범주의 개별 필드가 있습니다.

* 귀하가 생성하는 필드입니다.

   선택한[필드 유형](#field-types)은 콘텐츠 조각 모델을 구성하는 방법을 기반으로 필드를 만드는 데 사용됩니다. 필드 이름은 **데이터 형식**&#x200B;의 **속성 이름** 필드에서 가져옵니다.

   * 사용자가 특정 데이터 형식을 구성할 수 있기 때문에(예를 들어 한 줄 텍스트 또는 다중 필드로) **Render As** 속성도 고려해야 합니다.

* AEM용 GraphQL은 또한 여러 [도우미 필드](#helper-fields)를 생성합니다.

   도우미 필드는 콘텐츠 조각을 식별하거나 콘텐츠 조각에 대한 자세한 정보를 얻는 데 사용됩니다.

### 필드 유형 {#field-types}

AEM용 GraphQL은 유형 목록을 지원합니다. 지원되는 모든 콘텐츠 조각 모델 데이터 형식 및 해당 GraphQL 유형이 표시됩니다.

| 콘텐츠 조각 모델 - 데이터 형식 | GraphQL 유형 | 설명 |
|--- |--- |--- |
| 한 줄 텍스트 | 문자열, [문자열] |  작성자 이름, 위치 이름 등과 같은 간단한 문자열에 사용됨 |
| 여러 줄 텍스트 | 문자열 |  기사의 본문과 같은 텍스트 출력에 사용됨 |
| 숫자 |  부동, [Float] | 부동 소수점 숫자 및 일반 숫자를 표시하는 데 사용됨 |
| 부울 |  부울 |  확인란을 표시하는 데 사용됨 → 간단한 참/거짓 진술 |
| 날짜 및 시간 | 달력 |  ISO 8086 형식으로 날짜와 시간을 표시하는 데 사용됨. 선택한 유형에 따라 AEM GraphQL에서 세 가지 버전(`onlyDate`, `onlyTime`, `dateTime`)을 사용할 수 있습니다. |
| 열거 |  문자열 |  모델 생성 시 정의된 옵션 목록에서 옵션을 표시하는 데 사용됨 |
|  태그 |  [문자열] |  AEM에서 사용되는 태그를 나타내는 문자열 목록을 표시하는 데 사용됨 |
| 콘텐츠 참조 |  문자열 |  AEM에서 다른 에셋에 대한 경로를 표시하는 데 사용됨 |
| 조각 참조 |  *모델 유형* |  모델이 생성될 때 정의된 특정 모델 유형의 다른 콘텐츠 조각을 참조하는 데 사용됨 |

### 도우미 필드 {#helper-fields}

사용자 생성 필드의 데이터 형식 외에도 AEM용 GraphQL은 콘텐츠 조각 식별을 돕거나 콘텐츠 조각에 대한 추가 정보를 제공하기 위해 많은 *도우미* 필드도 생성합니다.

#### 경로 {#path}

경로 필드는 GraphQL에서 식별자로 사용됩니다. AEM 저장소 내 콘텐츠 조각 에셋의 경로를 나타냅니다. 다음과 같은 이유로 콘텐츠 조각의 식별자로 선택되었습니다.

* AEM 내에서 고유합니다.
* 쉽게 가져올 수 있습니다.

다음 코드는 콘텐츠 조각 모델 `Person`을 기반으로 생성된 모든 콘텐츠 조각의 경로를 표시합니다.

```xml
{
  personList {
    items {
      _path
    }
  }
}
```

특정 유형의 단일 콘텐츠 조각을 검색하려면 먼저 해당 경로도 결정해야 합니다. 예:

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _path
      firstName
      name
    }
  }
}
```

[샘플 쿼리 - 단일 특정 도시 조각](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-specific-city-fragment)을 참조하십시오.

#### 메타데이터 {#metadata}

AEM은 또한 GraphQL을 통해 콘텐츠 조각의 메타데이터를 노출합니다. 메타데이터는 콘텐츠 조각을 설명하는 정보이며, 예를 들어 콘텐츠 조각의 제목, 썸네일 경로, 콘텐츠 조각에 대한 설명, 생성 날짜 등이 있습니다.

메타데이터는 스키마 편집기를 통해 생성되기 때문에 특정한 구조를 가지고 있지 않으므로 콘텐츠 조각의 메타데이터를 노출하기 위해 `TypedMetaData` GraphQL 유형이 구현되었습니다. `TypedMetaData`은 다음 스칼라 유형으로 그룹화된 정보를 노출합니다.

| 필드 |
|--- |
| `stringMetadata:[StringMetadata]!` |
| `stringArrayMetadata:[StringArrayMetadata]!` |
| `intMetadata:[IntMetadata]!` |
| `intArrayMetadata:[IntArrayMetadata]!` |
| `floatMetadata:[FloatMetadata]!` |
| `floatArrayMetadata:[FloatArrayMetadata]!` |
| `booleanMetadata:[BooleanMetadata]!` |
| `booleanArrayMetadata:[booleanArrayMetadata]!`  |
| `calendarMetadata:[CalendarMetadata]!` |
| `calendarArrayMetadata:[CalendarArrayMetadata]!` |

각 스칼라 유형은 단일 이름-값 쌍 또는 이름-값 쌍의 배열을 표시하며, 여기서 해당 쌍의 값은 그룹화된 유형입니다.

예를 들어 콘텐츠 조각의 제목을 검색하려는 경우 이 속성이 문자열 속성이라는 것을 알고 있으므로 모든 문자열 메타데이터를 쿼리합니다.

메타데이터를 쿼리하려면:

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _path
      _metadata {
        stringMetadata {
          name
          value
        }
      }
    }
  }
}
```

생성된 GraphQL 스키마를 보면 모든 메타데이터 GraphQL 유형을 볼 수 있습니다. 모든 모델 유형에는 동일한 `TypedMetaData`가 있습니다.

>[!NOTE]
>
>**일반 메타데이터와 배열 메타데이터의 차이점**
>`StringMetadata` 및 `StringArrayMetadata`는 둘 다 검색 방법을 참조하는 것이 아니라 저장소에 저장된 내용을 참조합니다.
>
>따라서 예를 들어 `stringMetadata` 필드를 호출하면 저장소에 `String`으로 저장된 모든 메타데이터의 배열을 수신하고 `stringArrayMetadata`를 호출하면 저장소에 `String[]`으로 저장된 모든 메타데이터의 배열을 수신하게 됩니다.

[메타데이터에 대한 샘플 쿼리 - GB라는 제목의 상에 대한 메타데이터 나열](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb)을 참조하십시오.

#### 변형 {#variations}

`_variations` 필드는 콘텐츠 조각에 있는 변형 쿼리를 단순화하기 위해 구현되었습니다. 예:

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _variations
    }
  }
}
```

[샘플 쿼리 - 이름이 붙은 변형이 있는 모든 도시](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation)를 참조하십시오.

>[!NOTE]
>
>지정된 변형이 콘텐츠 조각에 존재하지 않는 경우 마스터 변형은 (대체) 기본값으로 반환됩니다.

<!--
## Security Considerations {#security-considerations}
-->

## GraphQL 변수 {#graphql-variables}

GraphQL을 사용하면 쿼리에 변수를 배치할 수 있습니다. 보다 자세한 정보는 [변수에 대한 GraphQL 설명서](https://graphql.org/learn/queries/#variables)를 참조하십시오.

예를 들어 특정 변형이 있는 `Article` 유형의 모든 콘텐츠 조각을 가져오려면 GraphiQL에서 `variation` 변수를 지정할 수 있습니다.

![GraphQL 변수](assets/cfm-graphqlapi-03.png "GraphQL 변수")

```xml
### query
query GetArticlesByVariation($variation: String!) {
    articleList(variation: $variation) {
        items {
            _path
            author
        }
    }
}
 
### in query variables
{
    "variation": "uk"
}
```

## GraphQL 지시문 {#graphql-directives}

GraphQL에서는 GraphQL 지시문이라고 하는 변수를 기반으로 쿼리를 변경할 수 있습니다.

예를 들어 `includePrice` 변수를 기반으로 모든 `AdventureModels`에 대한 쿼리에 `adventurePrice` 필드를 포함할 수 있습니다.

![GraphQL 지시문](assets/cfm-graphqlapi-04.png "GraphQL 지시문")

```xml
### query
query GetAdventureByType($includePrice: Boolean!) {
  adventureList {
    items {
      adventureTitle
      adventurePrice @include(if: $includePrice)
    }
  }
}
 
### in query variables
{
    "includePrice": true
}
```

## 필터링 {#filtering}

GraphQL 쿼리에서 필터링을 사용하여 특정 데이터를 반환할 수도 있습니다.

필터링은 논리 연산자 및 표현식을 기반으로 하는 구문을 사용합니다.

예를 들어 다음(기본) 쿼리는 이름이 `Jobs` 또는 `Smith`인 모든 사람을 필터링합니다.

```xml
query {
  personList(filter: {
    name: {
      _logOp: OR
      _expressions: [
        {
          value: "Jobs"
        },
        {
          value: "Smith"
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

더 많은 예는 다음을 참조하십시오.

* [AEM용 GraphQL 확장](#graphql-extensions)의 세부사항

* [이 샘플 콘텐츠 및 구조를 사용하는 샘플 쿼리](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries-sample-content-fragment-structure)

   * 그리고 샘플 쿼리에 사용하기 위해 준비된 [샘플 콘텐츠 및 구조](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)

* [WKND 프로젝트 기반 샘플 쿼리](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-queries-using-wknd-project)

## AEM용 GraphQL - 확장 요약 {#graphql-extensions}

AEM용 GraphQL을 사용한 쿼리의 기본 작업은 표준 GraphQL 사양을 따릅니다. AEM의 GraphQL 쿼리에 몇 가지 확장이 있습니다.

* 하나의 결과가 필요한 경우:
   * 모델 이름을 사용하십시오. 예: 도시

* 결과 목록을 기대하는 경우:
   * 모델 이름에 `List`를 추가하십시오. 예: `cityList`
   * [샘플 쿼리 - 모든 도시에 대한 모든 정보](#sample-all-information-all-cities)를 참조하십시오

* 논리적 OR을 사용하려는 경우:
   * ` _logOp: OR` 사용
   * [샘플 쿼리 - 이름이 “Jobs” 또는 “Smith”인 모든 사람](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-all-persons-jobs-smith)을 참조하십시오

* 논리적 AND도 존재하지만 (흔히) 암시적

* 콘텐츠 조각 모델 내의 필드에 해당하는 필드 이름을 쿼리할 수 있습니다.
   * [샘플 쿼리 - 회사 CEO 및 직원의 전체 세부 정보](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-full-details-company-ceos-employees)를 참조하십시오

* 모델의 필드 외에도 일부 시스템 생성 필드(앞에 밑줄 표시)가 있습니다.

   * 콘텐츠의 경우:

      * `_locale`: 언어 표시, 언어 관리자 기반
         * [주어진 로케일의 복수 콘텐츠 조각에 대한 샘플 쿼리](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-wknd-multiple-fragments-given-locale)를 참조하십시오
      * `_metadata`: 조각에 대한 메타데이터 표시
         * [메타데이터에 대한 샘플 쿼리 - GB라는 제목의 상에 대한 메타데이터 나열](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb)을 참조하십시오
      * `_model`: 콘텐츠 조각 모델에 대한 쿼리 허용(경로 및 제목)
         * [모델의 콘텐츠 조각 모델에 대한 샘플 쿼리](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-wknd-content-fragment-model-from-model)를 참조하십시오
      * `_path`: 저장소 내의 콘텐츠 조각에 대한 경로
         * [샘플 쿼리 - 단일 특정 도시 조각](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-specific-city-fragment)을 참조하십시오
      * `_reference`: 참조 표시, 서식 있는 텍스트 편집기에 인라인 참조 포함
         * [프리페치된 참조가 포함된 복수 콘텐츠 조각에 대한 샘플 쿼리](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-wknd-multiple-fragments-prefetched-references)를 참조하십시오
      * `_variation`: 콘텐츠 조각 내 특정 변형 표시

         >[!NOTE]
         >
         >지정된 변형이 콘텐츠 조각에 존재하지 않는 경우 마스터 변형은 (대체) 기본값으로 반환됩니다.

         * [샘플 쿼리 - 이름이 붙은 변형이 있는 모든 도시](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation)를 참조하십시오
   * 작업:

      * `_operator`: 특정 연산자 적용 - `EQUALS`, `EQUALS_NOT`, `GREATER_EQUAL`, `LOWER`, `CONTAINS`, `STARTS_WITH`
         * [샘플 쿼리 - 이름이 “Jobs”가 아닌 모든 사람](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-all-persons-not-jobs)을 참조하십시오
         * [샘플 쿼리 - `_path`가 특정 접두사로 시작하는 모든 모험](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-wknd-all-adventures-cycling-path-filter)을 참조하십시오
      * `_apply`: 특정 조건 적용. 예: `AT_LEAST_ONCE`
         * [샘플 쿼리 - 적어도 한 번은 발생해야 하는 항목이 있는 배열 필터링](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-array-item-occur-at-least-once)을 참조하십시오
      * `_ignoreCase`: 쿼리할 때 대소문자 무시
         * [샘플 쿼리 - 대소문자에 관계없이 이름에 SAN이 있는 모든 도시](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-all-cities-san-ignore-case)를 참조하십시오









* GraphQL 공용 구조체 형식이 지원됩니다.

   * `... on` 사용
      * [콘텐츠 참조가 있는 특정 모델의 콘텐츠 조각에 대한 샘플 쿼리](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-wknd-fragment-specific-model-content-reference)를 참조하십시오

* 중첩된 조각 쿼리 시 대체:

   * 요청된 변형이 중첩 조각에 없는 경우 **기본** 변형이 반환됩니다.

## 지속되는 쿼리(캐싱) {#persisted-queries-caching}

POST 요청을 사용하여 쿼리를 작성한 후 HTTP 캐시 또는 CDN에 의해 캐시할 수 있는 GET 요청으로 실행할 수 있습니다.

POST 쿼리는 일반적으로 캐시되지 않으므로 이러한 작업이 필요하며, 쿼리와 함께 GET을 매개 변수로 사용하는 경우 HTTP 서비스 및 중간값에 대해 매개 변수가 너무 커질 위험이 있습니다.

지속 쿼리는 항상 [적절한 Sites 구성](#graphql-aem-endpoint)과 관련된 끝점을 사용해야 합니다. 따라서 다음 중 하나 또는 둘 다를 사용할 수 있습니다.

* 전역 구성 및 끝점
쿼리는 모든 콘텐츠 조각 모델에 액세스할 수 있습니다.
* 특정 Sites 구성 및 끝점
특정 Sites 구성에 대한 지속 쿼리를 만들려면 (관련 콘텐츠 조각 모델에 대한 액세스를 제공하기 위해) 해당 Sites 구성별 끝점이 필요합니다.
예를 들어 WKND Sites 구성을 위해 특별히 지속 쿼리를 만들려면 해당 WKND별 Sites 구성 및 WKND별 끝점을 미리 만들어야 합니다.

>[!NOTE]
>
>자세한 내용은 [구성 브라우저에서 콘텐츠 조각 기능 활성화](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)를 참조하십시오.
>
>적절한 Sites 구성을 위해 **GraphQL 지속 쿼리**&#x200B;를 활성화해야 합니다.

예를 들어 Sites 구성 `my-conf`의 모델 `my-model`을 사용하는 `my-query`라는 특정 쿼리가 있는 경우:

* `my-conf` 특정 끝점을 사용하여 쿼리를 만들 수 있으며 쿼리는 다음과 같이 저장됩니다.
   `/conf/my-conf/settings/graphql/persistentQueries/my-query`
* `global` 끝점을 사용하여 동일한 쿼리를 생성할 수 있지만 쿼리는 다음과 같이 저장됩니다.
   `/conf/global/settings/graphql/persistentQueries/my-query`

>[!NOTE]
>
>이 쿼리들을 서로 다른 경로에 저장된 두 개의 서로 다른 쿼리입니다.
>
>동일한 모델을 사용하기는 하지만 다른 끝점을 통해 발생합니다.


지정된 쿼리를 유지하는 데 필요한 단계는 다음과 같습니다.

1. 쿼리를 새 끝점 URL `/graphql/persist.json/<config>/<persisted-label>`에 PUT하여 준비합니다.

   예를 들어 지속 쿼리를 만듭니다.

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
       }
     }
   }'
   ```

1. 이 시점에서 응답을 확인합니다.

   예를 들어 성공 여부를 확인합니다.

   ```xml
   {
     "action": "create",
     "configurationName": "wknd",
     "name": "plain-article-query",
     "shortPath": "/wknd/plain-article-query",
     "path": "/conf/wknd/settings/graphql/persistentQueries/plain-article-query"
   }
   ```

1. 그런 다음 URL을 사용하여 지속된 쿼리를 재생할 수 있습니다 `/graphql/execute.json/<shortPath>`.

   예를 들어 지속 쿼리를 사용합니다.

   ```xml
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. 이미 존재하는 쿼리 경로에 POST하여 지속 쿼리를 업데이트합니다.

   예를 들어 지속 쿼리를 사용합니다.

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
         referencearticle {
           _path
         }
       }
     }
   }'
   ```

1. 래핑된 일반 쿼리를 만듭니다.

   예:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. 캐시 제어를 사용하여 래핑된 일반 쿼리를 만듭니다.

   예:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. 매개변수를 사용하여 지속 쿼리를 만듭니다.

   예:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-parameters" \
       -d \
   'query GetAsGraphqlModelTestByPath($apath: String!, $withReference: Boolean = true) {
     articleByPath(_path: $apath) {
       item {
         _path
           author
           main {
           plaintext
           }
           referencearticle @include(if: $withReference) {
           _path
           }
         }
       }
     }'
   ```

1. 매개 변수를 사용하여 쿼리를 실행합니다.

   예:

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   
   $ curl -X GET \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   ```

1. 게시 시 쿼리를 실행하려면 관련 영구 트리를 복제해야 합니다

   * 복제를 위해 POST 사용:

      ```xml
      $curl -X POST   http://localhost:4502/bin/replicate.json \
        -H 'authorization: Basic YWRtaW46YWRtaW4=' \
        -F path=/conf/wknd/settings/graphql/persistentQueries/plain-article-query \
        -F cmd=activate
      ```

   * 패키지 사용:
      1. 새 패키지 정의를 만듭니다.
      1. 구성을 포함합니다(예: `/conf/wknd/settings/graphql/persistentQueries`).
      1. 패키지를 빌드합니다.
      1. 패키지를 복제합니다.
   * 복제/배포 도구 사용.
      1. 배포 도구로 이동합니다.
      1. 구성에 대한 트리 활성화를 선택합니다(예: `/conf/wknd/settings/graphql/persistentQueries`).
   * 워크플로 사용(워크플로 시작 관리자 구성을 통해):
      1. 다른 이벤트(예: 만들기, 수정 등)에 대한 구성을 복제하는 워크플로 모델을 실행하기 위한 워크플로 시작 관리자 규칙을 정의합니다.



1. 쿼리 구성이 게시되면 게시 끝점을 사용하기만 해도 동일한 원칙이 적용됩니다.

   >[!NOTE]
   >
   >익명 액세스의 경우 시스템은 ACL에서 “모든 사용자”가 쿼리 구성에 액세스할 수 있도록 허용한다고 가정합니다.
   >
   >그렇지 않은 경우 실행이 불가능합니다.

   >[!NOTE]
   >
   >URL에 있는 모든 세미콜론(“;”)은 인코딩해야 합니다.
   >
   >예를 들어 지속 쿼리 실행 요청에서처럼:
   >
   >
   ```xml
   >curl -X GET \ "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3bapath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   >```

## 외부 웹 사이트에서 GraphQL 끝점 쿼리 {#query-graphql-endpoint-from-external-website}

외부 웹 사이트에서 GraphQL 끝점에 액세스하려면 다음을 구성해야 합니다.

* [CORS 필터](#cors-filter)
* [레퍼러 필터](#referrer-filter)

### CORS 필터 {#cors-filter}

>[!NOTE]
>
>AEM의 CORS 리소스 공유 정책에 대한 자세한 개요는 [CORS(원본 간 리소스 공유) 이해](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=ko-KR#understand-cross-origin-resource-sharing-(cors))를 참조하십시오.

GraphQL 종단점에 액세스하려면 고객 Git 리포지토리에서 CORS 정책을 구성해야 합니다. 원하는 끝점에 대한 적절한 OSGi CORS 구성 파일 추가를 통해 수행됩니다. 

이 구성은 신뢰할 수 있는 웹 사이트 원본을 지정해야 합니다 `alloworigin` 또는 `alloworiginregexp` 액세스 권한을 부여해야 하는 대상.

예를 들어 GraphQL 끝점  및 `https://my.domain`의 지속 쿼리 끝점에 대한 액세스 권한을 부여하려면 다음을 사용할 수 있습니다.

```xml
{
  "supportscredentials":true,
  "supportedmethods":[
    "GET",
    "HEAD",
    "POST"
  ],
  "exposedheaders":[
    ""
  ],
  "alloworigin":[
    "https://my.domain"
  ],
  "maxage:Integer":1800,
  "alloworiginregexp":[
    ""
  ],
  "supportedheaders":[
    "Origin",
    "Accept",
    "X-Requested-With",
    "Content-Type",
    "Access-Control-Request-Method",
    "Access-Control-Request-Headers"
  ],
  "allowedpaths":[
    "/content/_cq_graphql/global/endpoint.json",
    "/graphql/execute.json/.*"
  ]
}
```

끝점에 대해 가상 경로를 구성한 경우 `allowedpaths`에서도 사용할 수 있습니다.

### 레퍼러 필터 {#referrer-filter}

CORS 구성 외에 타사 호스트에서 액세스할 수 있도록 레퍼러 필터를 구성해야 합니다.

이 작업은 다음과 같은 적절한 OSGi 레퍼러 필터 구성 파일을 추가하여 수행합니다.

* 신뢰할 수 있는 웹 사이트 호스트 이름(`allow.hosts` 또는 `allow.hosts.regexp`)을 지정합니다.
* 이 호스트 이름에 대한 액세스 권한을 부여합니다.

예를 들어 레퍼러 `my.domain`이 있는 요청에 대한 액세스 권한을 부여하려면 다음을 수행할 수 있습니다.

```xml
{
    "allow.empty":false,
    "allow.hosts":[
      "my.domain"
    ],
    "allow.hosts.regexp":[
      ""
    ],
    "filter.methods":[
      "POST",
      "PUT",
      "DELETE",
      "COPY",
      "MOVE"
    ],
    "exclude.agents.regexp":[
      ""
    ]
}
```

>[!CAUTION]
>
>다음에 대한 책임은 고객에게 있습니다.
>
>* 신뢰할 수 있는 도메인에만 액세스 권한을 부여하는 것
>* 민감한 정보가 노출되지 않도록 하는 것
>* 와일드카드 [*] 구문을 사용하지 않는 것. 사용하면 GraphQL 끝점에 대한 인증된 액세스가 비활성화되고 전 세계에 노출됩니다.


>[!CAUTION]
>
>모든 GraphQL [스키마](#schema-generation)(**활성화됨** 상태인 콘텐츠 조각 모델에서 파생)는 GraphQL 끝점을 통해 읽을 수 있습니다.
>
>즉, 이런 식으로 유출될 수 있기 때문에 민감한 데이터가 없는지 확인해야 합니다. 예를 들어 모델 정의에서 필드 이름으로 나타날 수 있는 정보가 여기에 포함됩니다.

## 인증 {#authentication}

[콘텐츠 조각의 원격 AEM GraphQL 쿼리 인증](/help/assets/content-fragments/graphql-authentication-content-fragments.md)을 참조하십시오.

<!-- to be addressed later -->

<!--
## Sorting {#sorting}
-->

<!-- to be addressed later -->

<!--
## Paging {#paging}
-->

## FAQ {#faqs}

제기된 질문:

1. **Q**: “*AEM용 GraphQL API는 쿼리 빌더 API와 어떻게 다릅니까?*”

   * **A**:
“*AEM GraphQL API는 JSON 출력에 대한 전체 제어를 제공하며 콘텐츠 쿼리를 위한 업계 표준입니다.
앞으로 AEM은 AEM GraphQL API에 투자할 계획입니다.*”

## 튜토리얼 - AEM Headless 및 GraphQL 시작하기 {#tutorial}

실습형 튜토리얼을 찾고 계십니까? Headless CMS 시나리오에서, AEM의 GraphQL API를 사용하여 콘텐츠를 구축하고 노출하고 외부 앱에서 사용하는 방법을 보여 주는 [AEM Headless 및 GraphQL 시작하기](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html?lang=ko-KR) 엔드투엔드 튜토리얼을 확인하십시오.
