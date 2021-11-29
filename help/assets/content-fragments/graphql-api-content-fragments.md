---
title: 컨텐츠 조각에 사용할 AEM GraphQL API
description: 헤드리스 컨텐츠 전달을 위해 AEM(Adobe Experience Manager)에서 AEM GraphQL API와 함께 컨텐츠 조각을 사용하는 방법을 알아봅니다.
feature: Content Fragments,GraphQL API
exl-id: beae1f1f-0a76-4186-9e58-9cab8de4236d
source-git-commit: 6c75af3957c319c38177cd62c90e781a982ba91b
workflow-type: tm+mt
source-wordcount: '3919'
ht-degree: 2%

---

# 컨텐츠 조각에 사용할 AEM GraphQL API {#graphql-api-for-use-with-content-fragments}

헤드리스 컨텐츠 전달을 위해 AEM(Adobe Experience Manager)에서 AEM GraphQL API와 함께 컨텐츠 조각을 사용하는 방법을 알아봅니다.

컨텐츠 조각에 사용되는 AEM GraphQL API는 오픈 소스 GraphQL API에 주로 의존합니다.

AEM에서 GraphQL API를 사용하면 헤드리스 CMS 구현에서 컨텐츠 조각을 JavaScript 클라이언트에 효율적으로 전달할 수 있습니다.

* REST와 같이 반복 API 요청 방지,
* 게재가 특정 요구 사항에 한정되어 있는지 확인하고
* 단일 API 쿼리에 대한 응답으로 렌더링하는 데 필요한 내용을 정확히 대량 배달할 수 있도록 허용합니다.

>[!NOTE]
>
>GraphQL은 현재 Adobe Experience Manager(AEM)의 두 가지(별도) 시나리오에서 사용됩니다.
>
>* [AEM Commerce에서는 GraphQL을 통해 상거래 플랫폼에서 데이터를 사용합니다](/help/commerce/cif/integrating/magento.md).
>* AEM 컨텐츠 조각은 AEM GraphQL API(표준 GraphQL을 기반으로 하는 사용자 정의 구현)와 함께 작동하여 애플리케이션에서 사용할 수 있도록 구조화된 컨텐츠를 제공합니다.


## GraphQL API {#graphql-api}

GraphQL은 다음과 같습니다.

* &quot;*...api에 대한 쿼리 언어 및 기존 데이터를 사용하여 이러한 쿼리를 수행하기 위한 런타임. GraphQL은 API에서 데이터에 대한 완전하고 이해할 수 있는 설명을 제공하고, 고객에게 필요한 사항과 더 이상 필요하지 않은 정보를 정확하게 요청하고, 시간에 따라 API를 쉽게 발전시키며, 강력한 개발자 도구를 활성화합니다.*&quot;.

   자세한 내용은 [GraphQL.org](https://graphql.org)

* &quot;*...유연한 API 레이어에 대한 개방형 사양입니다. GraphQL을 기존 백엔드에 배치하여 보다 신속하게 제품을 구축할 수 있습니다..*&quot;.

   자세한 내용은 [GraphQL 탐색](https://www.graphql.com).

* *&quot;...2015년 공개적으로 오픈 소싱되기 전에 Facebook이 2012년 내부적으로 개발한 데이터 쿼리 언어 및 사양입니다. REST 기반 아키텍처에 대한 대안으로서, 개발자 생산성을 높이고 데이터 전송량을 최소화합니다. GraphQL은 모든 규모의 수백 개의 조직에서 프로덕션에 사용됩니다.*

   자세한 내용은 [GraphQL 기초](https://foundation.graphql.org/).

<!--
"*Explore GraphQL is maintained by the Apollo team. Our goal is to give developers and technical leaders around the world all of the tools they need to understand and adopt GraphQL.*". 
-->

GraphQL API에 대한 자세한 내용은 다음 섹션(다른 많은 리소스 중)을 참조하십시오.

* at [graphql.org](https://graphql.org):

   * [GraphQL 소개](https://graphql.org/learn)

   * [GraphQL 사양](https://spec.graphql.org/)

* at [graphql.com](https://graphql.com):

   * [안내서](https://www.graphql.com/guides/)

   * [튜토리얼](https://www.graphql.com/tutorials/)

   * [사례 연구](https://www.graphql.com/case-studies/)

GraphQL for AEM 구현은 표준 GraphQL Java 라이브러리를 기반으로 합니다. 다음을 참조하십시오.

* [graphQL.org - Java](https://graphql.org/code/#java)

* [GitHub의 GraphQL Java](https://github.com/graphql-java)

### GraphQL 용어 {#graphql-terminology}

GraphQL은 다음을 사용합니다.

* **[쿼리](https://graphql.org/learn/queries/)**

* **[스키마 및 유형](https://graphql.org/learn/schema/)**:

   * 스키마가 컨텐츠 조각 모델을 기반으로 AEM에서 생성됩니다.
   * GraphQL은 스키마를 사용하여 GraphQL for AEM 구현에 허용되는 유형 및 작업을 제공합니다.

* **[필드](https://graphql.org/learn/queries/#fields)**

* **[GraphQL 끝점](#graphql-aem-endpoint)**
   * GraphQL 쿼리에 응답하고 GraphQL 스키마에 대한 액세스를 제공하는 AEM의 경로입니다.

   * 자세한 내용은 [GraphQL 끝점 활성화](#enabling-graphql-endpoint) 자세한 내용

자세한 내용은 [(GraphQL.org) GraphQL 소개](https://graphql.org/learn/) 다음을 포함한 포괄적인 세부 사항 [우수 사례](https://graphql.org/learn/best-practices/).

### GraphQL 쿼리 유형 {#graphql-query-types}

GraphQL을 사용하여 다음 중 하나를 반환하기 위한 쿼리를 수행할 수 있습니다.

* A **단일 항목**

* A **[항목 목록](https://graphql.org/learn/schema/#lists-and-non-null)**

다음을 수행할 수도 있습니다.

* [캐시된 지속적인 쿼리](#persisted-queries-caching)

>[!NOTE]
>GraphQL 쿼리를 [GraphiQL IDE](#graphiql-interface).

## AEM 종단점에 대한 GraphQL {#graphql-aem-endpoint}

끝점은 AEM용 GraphQL에 액세스하는 데 사용되는 경로입니다. 이 경로 사용(또는 앱)은 다음 작업을 수행할 수 있습니다.

* GraphQL 스키마 액세스,
* GraphQL 쿼리 전송,
* 응답을 받습니다(GraphQL 쿼리에 대한).

AEM에는 두 가지 유형의 엔드포인트가 있습니다.

* 전역
   * 모든 사이트에서 사용할 수 있습니다.
   * 이 종단점은 모든 사이트 구성(에 정의됨)의 모든 컨텐츠 조각 모델을 사용할 수 있습니다 [구성 브라우저](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)).
   * 사이트 구성 간에 공유해야 하는 컨텐츠 조각 모델이 있는 경우 글로벌 사이트 구성 아래에 만들어야 합니다.
* 사이트 구성:
   * 에 정의된 대로 Sites 구성에 해당합니다 [구성 브라우저](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser).
   * 지정된 사이트/프로젝트에 특정합니다.
   * 사이트 구성 특정 종단점은 전역 사이트 구성의 컨텐츠 조각 모델과 함께 해당 특정 사이트 구성의 컨텐츠 조각 모델을 사용합니다.

>[!CAUTION]
>
>컨텐츠 조각 편집기를 사용하면 한 사이트 구성의 컨텐츠 조각이 다른 사이트 구성의 컨텐츠 조각(정책을 통해)을 참조할 수 있습니다.
>
>이러한 경우 사이트 구성 특정 종단점을 사용하여 일부 컨텐츠를 검색할 수 있는 것은 아닙니다.
>
>컨텐츠 작성자는 이 시나리오를 제어해야 합니다. 예를 들어, 글로벌 사이트 구성에 공유 컨텐츠 조각 모델을 적용하는 것이 유용할 수 있습니다.

AEM용 GraphQL 글로벌 끝점의 저장소 경로는 다음과 같습니다.

`/content/cq:graphql/global/endpoint`

요청 URL에서 다음 경로를 사용할 수 있는 앱의 경우:

`/content/_cq_graphql/global/endpoint.json`

GraphQL for AEM에 대해 끝점을 활성화하려면 다음을 수행해야 합니다.

* [GraphQL 끝점 활성화](#enabling-graphql-endpoint)
* [GraphQL 끝점 게시](#publishing-graphql-endpoint)

### GraphQL 끝점 활성화 {#enabling-graphql-endpoint}

GraphQL 종단점을 사용하려면 먼저 적절한 구성이 있어야 합니다. 자세한 내용은 [컨텐츠 조각 - 구성 브라우저](/help/assets/content-fragments/content-fragments-configuration-browser.md).

>[!CAUTION]
>
>[컨텐츠 조각 모델 사용이 활성화되지 않은](/help/assets/content-fragments/content-fragments-configuration-browser.md) 경우 **만들기** 옵션을 사용할 수 없습니다.

해당 끝점을 활성화하려면

1. 다음으로 이동 **도구**, **자산**&#x200B;를 선택하고 을 선택합니다. **GraphQL**.
1. **만들기**&#x200B;를 선택합니다.
1. 다음 **새 GraphQL 끝점 만들기** 대화 상자가 열립니다. 여기에서 다음을 지정할 수 있습니다.
   * **이름**: 끝점의 이름; 텍스트를 입력할 수 있습니다.
   * **GraphQL 스키마에서 제공되는 스키마 사용**: 드롭다운을 사용하여 필요한 사이트/프로젝트를 선택합니다.

   >[!NOTE]
   >
   >대화 상자에 다음 경고가 표시됩니다.
   >
   >* *GraphQL 엔드포인트는 신중하게 관리하지 않을 경우 데이터 보안 및 성능 문제를 초래할 수 있습니다. 엔드포인트를 만든 후 적절한 사용 권한을 설정했는지 확인하십시오.*


1. 다음으로 확인 **만들기**.
1. 다음 **다음 단계** 대화 상자에서는 새로 만든 끝점에 적절한 권한이 있는지 확인할 수 있도록 보안 콘솔에 직접 링크를 제공합니다.

   >[!CAUTION]
   >
   >엔드포인트는 모든 사람이 액세스할 수 있습니다. GraphQL 쿼리는 서버에 많은 로드를 부과할 수 있으므로 특히 게시 인스턴스에서 보안에 문제가 발생할 수 있습니다.
   >
   >사용 사례에 적합한 ACL을 엔드포인트에서 설정할 수 있습니다.

### GraphQL 끝점 게시 {#publishing-graphql-endpoint}

새 끝점을 선택하고 **게시** 모든 환경에서 완전히 사용할 수 있도록 합니다.

>[!CAUTION]
>
>엔드포인트는 모든 사람이 액세스할 수 있습니다.
>
>GraphQL 쿼리는 서버에 많은 로드를 부과할 수 있으므로 게시 인스턴스에서 이 기능은 보안 문제가 될 수 있습니다.
>
>엔드포인트의 사용 사례에 적합한 ACL을 설정해야 합니다.

## GraphiQL 인터페이스 {#graphiql-interface}

표준 구현 [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) 인터페이스는 AEM GraphQL에서 사용할 수 있습니다. 다음 중 하나일 수 있습니다 [AEM에 설치](#installing-graphiql-interface).

>[!NOTE]
>
>GraphiQL이 전역 끝점에 바인딩되어 있으며 특정 사이트 구성에 대한 다른 끝점에서는 작동하지 않습니다.

이 인터페이스를 사용하면 쿼리를 직접 입력 및 테스트할 수 있습니다.

예:

* `http://localhost:4502/content/graphiql.html`

여기에는 내역 및 온라인 설명서와 함께 구문 강조, 자동 완료, 자동 제안 등의 기능이 제공됩니다.

![GraphiQL 인터페이스](assets/cfm-graphiql-interface.png "GraphiQL 인터페이스")

### AEM GraphiQL 인터페이스 설치 {#installing-graphiql-interface}

전용 패키지를 사용하여 AEM에 GraphiQL 사용자 인터페이스를 설치할 수 있습니다. a [GraphiQL 컨텐츠 패키지 v0.0.6(2021.3)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-graphql/graphiql-0.0.6.zip) 패키지.

>[!NOTE]
>
>사용 가능한 패키지는 AEM 6.5.10.0 및 AEM as a Cloud Service과 완벽하게 호환됩니다.

## 작성 및 게시 환경에 대한 사용 사례 {#use-cases-author-publish-environments}

사용 사례는 AEM 환경의 유형에 따라 달라질 수 있습니다.

* 게시 환경; 다음 작업에 사용됩니다.
   * JS 애플리케이션에 대한 쿼리 데이터(표준 사용 사례)

* 작성 환경 다음 작업에 사용됩니다.
   * &quot;컨텐츠 관리 목적&quot;을 위한 쿼리 데이터:
      * AEM의 GraphQL은 현재 읽기 전용 API입니다.
      * REST API는 CR(u)D 작업에 사용할 수 있습니다.

## 권한 {#permission}

권한은 자산에 액세스하는 데 필요한 권한입니다.

## 스키마 생성 {#schema-generation}

GraphQL은 강력한 형식의 API이며, 이는 데이터를 유형별로 명확하게 구조화하고 구성해야 함을 의미합니다.

GraphQL 사양은 특정 인스턴스에 대한 데이터 조사를 위한 강력한 API를 만드는 방법에 대한 일련의 지침을 제공합니다. 이를 수행하려면 클라이언트가 [스키마](#schema-generation): 쿼리에 필요한 모든 유형을 포함합니다.

컨텐츠 조각의 경우 GraphQL 스키마(구조 및 유형)는 **활성화됨** [컨텐츠 조각 모델](/help/assets/content-fragments/content-fragments-models.md) 및 해당 데이터 유형을 확인합니다.

>[!CAUTION]
>
>모든 GraphQL 스키마(컨텐츠 조각 모델에서 파생됨) **활성화됨**)은 GraphQL 종단점을 통해 읽을 수 있습니다.
>
>이는 민감한 데이터가 이러한 방식으로 유출될 수 있으므로 사용할 수 없도록 해야 함을 의미합니다. 예를 들어 모델 정의에서 필드 이름으로 존재할 수 있는 정보가 포함됩니다.

예를 들어 사용자가 `Article`로 설정되면 AEM에서 개체를 생성합니다 `article` 그것은 타입에 불과하다 `ArticleModel`. 이 유형 내의 필드는 모델에 정의된 필드 및 데이터 유형에 해당합니다.

1. 컨텐츠 조각 모델:

   ![GraphQL에서 사용할 컨텐츠 조각 모델](assets/cfm-graphqlapi-01.png "GraphQL에서 사용할 컨텐츠 조각 모델")

1. 해당 GraphQL 스키마(GraphiQL 자동 설명서에서 출력):
   ![컨텐츠 조각 모델을 기반으로 하는 GraphQL 스키마](assets/cfm-graphqlapi-02.png "컨텐츠 조각 모델을 기반으로 하는 GraphQL 스키마")

   생성된 유형이 표시됩니다 `ArticleModel` 여러 개 포함 [필드](#fields).

   * 이 중 3개는 사용자가 제어했습니다. `author`, `main` 및 `referencearticle`.

   * 다른 필드는 AEM에 의해 자동으로 추가되었으며 특정 컨텐츠 조각에 대한 정보를 제공하는 유용한 방법을 나타냅니다. 이 예에서 `_path`, `_metadata`, `_variations`. 다음 [도우미 필드](#helper-fields) 이전 `_` 사용자가 정의한 내용과 자동 생성된 항목을 구분하기 위해.

1. 사용자가 문서 모델을 기반으로 컨텐츠 조각을 만든 후 GraphQL을 통해 질문할 수 있습니다. 예를 보려면 [샘플 쿼리](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries) (기준 [GraphQL에서 사용할 컨텐츠 조각 구조 샘플](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)).

AEM용 GraphQL에서 스키마가 유연합니다. 즉, 컨텐츠 조각 모델이 생성, 업데이트 또는 삭제될 때마다 자동으로 생성됩니다. 컨텐츠 조각 모델을 업데이트할 때도 데이터 스키마 캐시가 새로 고쳐집니다.

Sites GraphQL 서비스는 컨텐츠 조각 모델에 수행된 수정 사항을 수신합니다(백그라운드에서). 업데이트가 감지되면 해당 스키마 부분만 다시 생성됩니다. 이 최적화는 시간을 절약하고 안정성을 제공합니다.

따라서 다음과 같은 경우:

1. 포함된 패키지 설치 `Content-Fragment-Model-1` 및 `Content-Fragment-Model-2`:

   1. GraphQL 유형 `Model-1` 및 `Model-2` 가 생성됩니다.

1. 그런 다음 수정합니다 `Content-Fragment-Model-2`:

   1. 전용 `Model-2` GraphQL 유형이 업데이트됩니다.

   1. 반면에 `Model-1` 는 동일하게 유지됩니다.

>[!NOTE]
>
>REST api를 통해 컨텐츠 조각 모델에 대해 벌크 업데이트를 수행하거나 수행하려는 경우 메모하는 것이 중요합니다.

스키마는 GraphQL 쿼리와 동일한 종단점을 통해 제공되며 클라이언트는 확장을 사용하여 스키마가 호출된다는 사실을 처리합니다 `GQLschema`. 예를 들어, `GET` 요청 시 `/content/cq:graphql/global/endpoint.GQLschema` 그러면 Content-type으로 스키마 출력이 생성됩니다. `text/x-graphql-schema;charset=iso-8859-1`.

### 스키마 생성 - 게시 취소된 모델 {#schema-generation-unpublished-models}

컨텐츠 조각이 중첩되면 상위 컨텐츠 조각 모델이 게시되지만 참조된 모델은 게시되지 않을 수 있습니다.

>[!NOTE]
>
>AEM UI는 이러한 문제가 발생하지 않도록 하지만 게시가 프로그래밍 방식으로 또는 컨텐츠 패키지로 만들어지는 경우 발생할 수 있습니다.

이런 경우 AEM에서 를 생성합니다 *불완전* 상위 컨텐츠 조각 모델의 스키마입니다. 즉, 게시되지 않은 모델에 종속된 조각 참조가 스키마에서 제거됩니다.

## 필드 {#fields}

스키마 내에는 두 가지 기본 카테고리 중 개별 필드가 있습니다.

* 생성하는 필드입니다.

   선택 항목 [필드 유형](#field-types) 컨텐츠 조각 모델을 구성하는 방법에 따라 필드를 만드는 데 사용됩니다. 필드 이름은 **속성 이름** 필드 **데이터 유형**.

   * 또한 **다음으로 렌더링** 사용자가 특정 데이터 유형을 구성할 수 있으므로 고려해야 할 속성입니다. 예를 들어, 단일 행 텍스트 또는 다중 필드로 사용할 수 있습니다.

* AEM용 GraphQL도 여러 개의 [도우미 필드](#helper-fields).

   컨텐츠 조각을 식별하거나 컨텐츠 조각에 대한 자세한 정보를 가져오는 데 사용됩니다.

### 필드 유형 {#field-types}

AEM용 GraphQL은 유형 목록을 지원합니다. 지원되는 모든 컨텐츠 조각 모델 데이터 유형과 해당 GraphQL 유형이 표시됩니다.

| 컨텐츠 조각 모델 - 데이터 유형 | GraphQL 유형 | 설명 |
|--- |--- |--- |
| 한 줄 텍스트 | 문자열, [문자열] |  작성자 이름, 위치 이름 등과 같은 간단한 문자열에 사용됩니다. |
| 여러 줄 텍스트 | String |  문서 본문 등의 텍스트를 출력하는 데 사용됩니다. |
| 번호 |  이동, [부동] | 부동 소수점 번호와 일반 숫자를 표시하는 데 사용됩니다. |
| 부울 |  부울 |  확인란→ 단순 true/false 문을 표시하는 데 사용됩니다 |
| 날짜 및 시간 | 달력 |  날짜와 시간을 ISO 8086 형식으로 표시하는 데 사용됩니다. 선택한 유형에 따라 AEM GraphQL에서 사용할 수 있는 세 가지 방식이 있습니다. `onlyDate`, `onlyTime`, `dateTime` |
| 열거 |  String |  모델 생성 시 정의된 옵션 목록에서 옵션을 표시하는 데 사용됩니다. |
|  태그 |  [String] |  AEM에 사용된 태그를 나타내는 문자열 목록을 표시하는 데 사용됩니다. |
| 컨텐츠 참조 |  문자열 |  AEM에서 다른 자산을 향해 경로를 표시하는 데 사용됩니다 |
| 조각 참조 |  *모델 유형* |  모델을 만들 때 정의된 특정 모델 유형의 다른 컨텐츠 조각을 참조하는 데 사용됩니다. |

### 도우미 필드 {#helper-fields}

GraphQL for AEM은 사용자 생성 필드에 대한 데이터 유형 외에도 많은 수의 필드를 생성합니다 *도우미* 컨텐츠 조각을 식별하거나 컨텐츠 조각에 대한 추가 정보를 제공하기 위한 필드입니다.

#### 경로 {#path}

경로 필드는 GraphQL에서 식별자로 사용됩니다. AEM 저장소 내의 컨텐츠 조각 자산의 경로를 나타냅니다. 이 변수는 다음과 같은 이유로 컨텐츠 조각의 식별자로 선택했습니다.

* AEM 내에서 고유하며
* 쉽게 가져올 수 있습니다.

다음 코드는 컨텐츠 조각 모델을 기반으로 만들어진 모든 컨텐츠 조각의 경로를 표시합니다 `Person`.

```xml
{
  personList {
    items {
      _path
    }
  }
}
```

특정 유형의 단일 컨텐츠 조각을 검색하려면 먼저 해당 경로를 결정해야 합니다. 예:

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

자세한 내용은 [샘플 쿼리 - 단일 특정 도시 조각](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-specific-city-fragment).

#### 메타데이터 {#metadata}

GraphQL을 통해 AEM은 컨텐츠 조각의 메타데이터도 노출합니다. 메타데이터는 컨텐츠 조각의 제목, 축소판 경로, 컨텐츠 조각의 설명, 컨텐츠 조각의 생성일 등과 같은 컨텐츠 조각을 설명하는 정보입니다.

메타데이터는 스키마 편집기를 통해 생성되며 특정 구조가 없으므로 `TypedMetaData` 컨텐츠 조각의 메타데이터를 노출하도록 GraphQL 유형이 구현되었습니다. `TypedMetaData` 다음 스칼라 유형별로 그룹화된 정보를 표시합니다.

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

각 스칼라 형식은 단일 이름-값 쌍 또는 이름-값 쌍의 배열을 나타냅니다. 여기서 해당 쌍의 값은 그룹화된 형식의 값입니다.

예를 들어 컨텐츠 조각의 제목을 검색하려는 경우 이 속성이 String 속성임을 알고 있으므로 모든 문자열 메타데이터를 쿼리합니다.

메타데이터에 대해 쿼리하려면:

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

생성된 GraphQL 스키마를 볼 경우 모든 메타데이터 GraphQL 유형을 볼 수 있습니다. 모든 모델 유형은 동일합니다 `TypedMetaData`.

>[!NOTE]
>
>**일반 메타데이터와 배열 메타데이터 간의 차이점**
>주의 사항 `StringMetadata` 및 `StringArrayMetadata` 둘 다 검색 방법이 아니라 저장소에 저장된 항목을 참조합니다.
>
>예를 들어 `stringMetadata` 필드에서는 리포지토리에 저장된 모든 메타데이터의 배열을 `String` , 및 `stringArrayMetadata` 리포지토리에 저장된 모든 메타데이터의 배열을 `String[]`.

자세한 내용은 [메타데이터에 대한 샘플 쿼리 - GB라는 이름의 시상식에 대한 메타데이터 나열](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb).

#### 변형 {#variations}

다음 `_variations` 필드가 구현되어 컨텐츠 조각에 있는 변형을 쿼리합니다. 예:

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _variations
    }
  }
}
```

자세한 내용은 [샘플 쿼리 - 명명된 변형을 가진 모든 도시](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation).

<!--
## Security Considerations {#security-considerations}
-->

## GraphQL 변수 {#graphql-variables}

GraphQL은 변수를 쿼리에 배치할 수 있도록 허용합니다. 자세한 내용은 [변수에 대한 GraphQL 설명서](https://graphql.org/learn/queries/#variables).

예를 들어 모든 컨텐츠 조각 유형 `Article` 특정 변형이 있는 변수에는 `variation` GraphiQL에서 생성합니다.

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

## GraphQL 지시어 {#graphql-directives}

GraphQL에서는 GraphQL 지시문이라는 변수를 기반으로 쿼리를 변경할 수 있습니다.

예를 들어 다음을 포함할 수 있습니다 `adventurePrice` 모든 `AdventureModels`, 변수 기반 `includePrice`.

![GraphQL 지시어](assets/cfm-graphqlapi-04.png "GraphQL 지시어")

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

예를 들어 다음(기본) 쿼리는 이름이 인 모든 사람을 필터링합니다 `Jobs` 또는 `Smith`:

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

자세한 예는 다음을 참조하십시오.

* 세부 정보 [AEM 확장을 위한 GraphQL](#graphql-extensions)

* [이 샘플 컨텐츠 및 구조를 사용한 샘플 쿼리](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries-sample-content-fragment-structure)

   * 그리고 [샘플 컨텐츠 및 구조](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql) 샘플 쿼리에 사용 준비

* [WKND 프로젝트를 기반으로 하는 샘플 쿼리](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-queries-using-wknd-project)

## GraphQL for AEM - 확장 요약 {#graphql-extensions}

GraphQL for AEM을 사용하는 쿼리의 기본 작업은 표준 GraphQL 사양을 준수합니다. AEM을 사용하는 GraphQL 쿼리의 경우 몇 가지 확장이 있습니다.

* 단일 결과가 필요한 경우:
   * 모델 이름 사용; g city

* 결과 목록이 예상되면:
   * 추가 `List` 모델 이름을 지정합니다. 예  `cityList`
   * 자세한 내용은 [샘플 쿼리 - 모든 도시에 대한 모든 정보](#sample-all-information-all-cities)

* 논리 OR를 사용하려면
   * use ` _logOp: OR`
   * 자세한 내용은 [샘플 쿼리 - &quot;Job&quot; 또는 &quot;Smith&quot;라는 이름을 가진 모든 개인](#sample-all-persons-jobs-smith)

* 논리 AND도 존재하지만 (종종) 암시적

* 컨텐츠 조각 모델 내의 필드에 해당하는 필드 이름을 쿼리할 수 있습니다
   * 자세한 내용은 [샘플 질의 - 회사 CEO 및 직원의 전체 상세내역](#sample-full-details-company-ceos-employees)

* 모델의 필드 외에도 시스템에서 생성한 필드(앞에 밑줄)가 있습니다.

   * 컨텐츠의 경우:

      * `_locale` : 언어를 공개하다; 언어 관리자 기반
         * 자세한 내용은 [지정된 로케일의 여러 컨텐츠 조각에 대한 샘플 쿼리](#sample-wknd-multiple-fragments-given-locale)
      * `_metadata` : 조각에 대한 메타데이터를 표시하려면 다음을 수행하십시오.
         * 자세한 내용은 [메타데이터에 대한 샘플 쿼리 - GB라는 이름의 시상식에 대한 메타데이터 나열](#sample-metadata-awards-gb)
      * `_model` : 컨텐츠 조각 모델(경로 및 제목)에 대한 쿼리 허용
         * 자세한 내용은 [모델의 컨텐츠 조각 모델에 대한 샘플 쿼리](#sample-wknd-content-fragment-model-from-model)
      * `_path` : 리포지토리 내의 컨텐츠 조각 경로
         * 자세한 내용은 [샘플 쿼리 - 단일 특정 도시 조각](#sample-single-specific-city-fragment)
      * `_reference` : 참조를 표시합니다. 리치 텍스트 편집기에서 인라인 참조 포함
         * 자세한 내용은 [프리페치된 참조가 있는 여러 컨텐츠 조각에 대한 샘플 쿼리](#sample-wknd-multiple-fragments-prefetched-references)
      * `_variation` : 컨텐츠 조각 내의 특정 변형을 노출하려면
         * 자세한 내용은 [샘플 쿼리 - 명명된 변형을 가진 모든 도시](#sample-cities-named-variation)
   * 및 작업:

      * `_operator` : 특정 연산자 적용 `EQUALS`, `EQUALS_NOT`, `GREATER_EQUAL`, `LOWER`, `CONTAINS`, `STARTS_WITH`
         * 자세한 내용은 [샘플 쿼리 - &quot;Job&quot;이라는 이름이 없는 모든 개인](#sample-all-persons-not-jobs)
         * 자세한 내용은 [샘플 쿼리 - `_path` 특정 접두사로 시작](#sample-wknd-all-adventures-cycling-path-filter)
      * `_apply` : 특정 조건을 적용하는 경우 예  `AT_LEAST_ONCE`
         * 자세한 내용은 [샘플 쿼리 - 한 번 이상 발생해야 하는 항목이 있는 배열에 필터링](#sample-array-item-occur-at-least-once)
      * `_ignoreCase` : 쿼리 시 대/소문자를 무시하려면
         * 자세한 내용은 [샘플 쿼리 - 사례에 상관없이 이름에 SAN이 있는 모든 도시](#sample-all-cities-san-ignore-case)









* GraphQL 결합 유형이 지원됩니다.

   * 사용 `... on`
      * 자세한 내용은 [컨텐츠 참조가 있는 특정 모델의 컨텐츠 조각에 대한 샘플 쿼리](#sample-wknd-fragment-specific-model-content-reference)

## 지속되는 쿼리(캐싱) {#persisted-queries-caching}

POST 요청을 사용하여 쿼리를 작성한 후 HTTP 캐시 또는 CDN에 의해 캐시할 수 있는 GET 요청으로 실행할 수 있습니다.

POST 쿼리는 일반적으로 캐시되지 않으므로 이러한 작업이 필요하며, 쿼리와 함께 GET을 매개 변수로 사용하는 경우 HTTP 서비스 및 중간값에 대해 매개 변수가 너무 커질 위험이 있습니다.

지속형 쿼리는 항상 [적절한 사이트 구성](#graphql-aem-endpoint); 둘 중 하나 또는 둘 다 사용할 수 있습니다.

* 전역 구성 및 엔드포인트 쿼리는 모든 컨텐츠 조각 모델에 액세스할 수 있습니다.
* 특정 사이트 구성 및 끝점 특정 사이트 구성에 대해 지속적인 쿼리를 만들려면 관련 사이트 구성 관련 엔드포인트가 필요합니다(관련 컨텐츠 조각 모델에 대한 액세스 권한을 제공).
예를 들어 WKND Sites 구성을 위해 특별히 지속된 쿼리를 만들려면 해당 WKND별 Sites 구성 및 WKND별 종단점을 미리 만들어야 합니다.

>[!NOTE]
>
>자세한 내용은 [구성 브라우저에서 컨텐츠 조각 기능 활성화](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser) 자세한 내용
>
>다음 **GraphQL 지속성 쿼리** 적절한 사이트 구성에 대해 를 활성화해야 합니다.

예를 들어 `my-query`- 모델을 사용합니다 `my-model` 사이트 구성에서 `my-conf`:

* 을 사용하여 쿼리를 만들 수 있습니다 `my-conf` 특정 종단점 및 다음과 같이 쿼리가 저장됩니다.
   `/conf/my-conf/settings/graphql/persistentQueries/my-query`
* 을 사용하여 동일한 쿼리를 만들 수 있습니다 `global` 엔드포인트. 그러면 다음과 같이 쿼리가 저장됩니다.
   `/conf/global/settings/graphql/persistentQueries/my-query`

>[!NOTE]
>
>이 두 쿼리는 서로 다른 경로에 저장됩니다.
>
>우연히 동일한 모델을 사용하지만 다른 끝점을 통해 사용됩니다.


지정된 쿼리를 유지하는 데 필요한 단계는 다음과 같습니다.

1. 새 끝점 URL에 넣어 쿼리를 준비합니다 `/graphql/persist.json/<config>/<persisted-label>`.

   예를 들어 지속적인 쿼리를 만듭니다.

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

   예를 들어, 성공을 확인합니다.

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

   예를 들어, 지속된 쿼리를 사용합니다.

   ```xml
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. POSTing을 통해 지속된 쿼리를 이미 존재하는 쿼리 경로로 업데이트합니다.

   예를 들어, 지속된 쿼리를 사용합니다.

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

1. 매개 변수를 사용하여 지속적인 쿼리를 만듭니다.

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

1. 매개 변수를 사용하여 쿼리 실행

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

   * 복제에 POST 사용:

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
   * 워크플로우 사용(워크플로우 런처 구성을 통해):
      1. 다른 이벤트에서 구성을 복제하는 워크플로우 모델을 실행하기 위한 워크플로우 실행 관리자 규칙을 정의합니다(예: 만들기, 수정 등).



1. 쿼리 구성이 게시되면 게시 끝점을 사용하기만 해도 동일한 원칙이 적용됩니다.

   >[!NOTE]
   >
   >익명 액세스의 경우 시스템은 ACL을 통해 &quot;모든 사용자&quot;가 쿼리 구성에 액세스할 수 있다고 가정합니다.
   >
   >그렇지 않으면 실행할 수 없습니다.

   >[!NOTE]
   >
   >URL의 모든 세미콜론(&quot;;&quot;)을 인코딩해야 합니다.
   >
   >예를 들어, 지속형 쿼리 실행 요청에서와 같습니다.
   >
   >
   ```xml
   >curl -X GET \ "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3bapath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   >```

## 외부 웹 사이트에서 GraphQL 끝점 쿼리 {#query-graphql-endpoint-from-external-website}

외부 웹 사이트에서 GraphQL 종단점에 액세스하려면 다음을 구성해야 합니다.

* [CORS 필터](#cors-filter)
* [레퍼러 필터](#referrer-filter)

### CORS 필터 {#cors-filter}

>[!NOTE]
>
>AEM에서 CORS 리소스 공유 정책에 대한 자세한 개요는 다음을 참조하십시오 [CORS(원본 간 리소스 공유) 이해](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html#understand-cross-origin-resource-sharing-(cors)).

GraphQL 종단점에 액세스하려면 고객 Git 리포지토리에서 CORS 정책을 구성해야 합니다. 이 작업은 원하는 엔드포인트에 대한 적절한 OSGi CORS 구성 파일을 추가하여 수행합니다.

이 구성은 신뢰할 수 있는 웹 사이트 원본을 지정해야 합니다 `alloworigin` 또는 `alloworiginregexp` 액세스 권한을 부여해야 하는 대상.

예를 들어, GraphQL 종단점에 대한 액세스 권한을 부여하고 `https://my.domain` 다음을 사용할 수 있습니다.

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

엔드포인트에 대한 별칭 경로를 구성한 경우, 이를 에서도 사용할 수 있습니다. `allowedpaths`.

### 레퍼러 필터 {#referrer-filter}

CORS 구성 외에 타사 호스트에서 액세스할 수 있도록 레퍼러 필터를 구성해야 합니다.

이 작업은 다음과 같은 적절한 OSGi 레퍼러 필터 구성 파일을 추가하여 수행합니다.

* 신뢰할 수 있는 웹 사이트 호스트 이름을 지정합니다. 둘 중 하나 `allow.hosts` 또는 `allow.hosts.regexp`,
* 이 호스트 이름에 대한 액세스 권한을 부여합니다.

예를 들어 레퍼러가 있는 요청에 대한 액세스 권한을 부여하려면 `my.domain` 다음을 수행할 수 있습니다.

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
>고객이 다음 작업을 수행할 책임이 있습니다.
>
>* 신뢰할 수 있는 도메인에 대한 액세스 권한만 부여
>* 중요한 정보가 노출되지 않도록 합니다.
>* 와일드카드 사용 안 함 [*] 구문; 이렇게 하면 GraphQL 종단점에 대한 인증된 액세스를 비활성화하고 전체 세계에 노출됩니다.


>[!CAUTION]
>
>모든 GraphQL [스키마](#schema-generation) (컨텐츠 조각 모델에서 파생됨 **활성화됨**)은 GraphQL 종단점을 통해 읽을 수 있습니다.
>
>이는 민감한 데이터가 이러한 방식으로 유출될 수 있으므로 사용할 수 없도록 해야 함을 의미합니다. 예를 들어 모델 정의에서 필드 이름으로 존재할 수 있는 정보가 포함됩니다.

## 인증 {#authentication}

자세한 내용은 [컨텐츠 조각에 대한 원격 AEM GraphQL 쿼리에 대한 인증](/help/assets/content-fragments/graphql-authentication-content-fragments.md).

<!-- to be addressed later -->

<!--
## Sorting {#sorting}
-->

<!-- to be addressed later -->

<!--
## Paging {#paging}
-->

## FAQ {#faqs}

발생한 질문:

1. **Q**: &quot;*AEM용 GraphQL API는 Query Builder API와 어떻게 다릅니까?*&quot;

   * **A**: &quot;*AEM GraphQL API는 JSON 출력에 대한 전체 제어 기능을 제공하며 컨텐츠를 쿼리하는 업계 표준입니다.
앞으로 AEM에서는 AEM GraphQL API에 투자할 계획입니다.*&quot;

## 자습서 - AEM 헤드리스 및 GraphQL 시작하기 {#tutorial}

실습 자습서를 찾고 계십니까? 체크 아웃 [AEM 헤드리스 및 GraphQL 시작하기](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) 헤드리스 CMS 시나리오에서 AEM GraphQL API를 사용하여 컨텐츠를 작성하고 노출하는 방법을 소개하는 종단간 자습서입니다.
