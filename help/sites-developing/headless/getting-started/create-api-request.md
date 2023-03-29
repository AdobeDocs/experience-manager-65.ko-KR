---
title: 컨텐츠 조각 액세스 및 제공 헤드리스 빠른 시작 안내서
description: AEM Assets REST API를 사용하여 컨텐츠 조각 및 컨텐츠 조각 컨텐츠의 헤드리스 전달을 위한 GraphQL API를 관리하는 방법을 알아봅니다.
exl-id: 4664b3a4-4873-4f42-b59d-aadbfaa6072f
source-git-commit: 7355c149500f9e5044c9ff78af208d36ee681f56
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 66%

---

# 컨텐츠 조각 액세스 및 제공 헤드리스 빠른 시작 안내서 {#accessing-delivering-content-fragments}

AEM Assets REST API를 사용하여 컨텐츠 조각 및 컨텐츠 조각 컨텐츠의 헤드리스 전달을 위한 GraphQL API를 관리하는 방법을 알아봅니다.

## GraphQL 및 Assets REST API란 무엇입니까? {#what-are-the-apis}

[일부 콘텐츠 조각을 만들었으므로](create-content-fragment.md) 이제 AEM의 API를 사용하여 Headless 방식으로 전달할 수 있습니다.

* [GraphQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md)를 사용하면 콘텐츠 조각에 액세스하고 전달하기 위한 요청을 생성할 수 있습니다.
   * 이 기능 집합을 사용하려면 [끝점을 AEM에서 정의하고 활성화해야 하며](/help/sites-developing/headless/graphql-api/graphql-endpoint.md#enabling-graphql-endpoint), 필요한 경우 [GraphiQL 인터페이스가 설치되어야 합니다](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#installing-graphiql-interface).
* [Assets REST API](/help/assets/assets-api-content-fragments.md)를 사용하면 콘텐츠 조각(및 기타 에셋)을 만들고 수정할 수 있습니다.

이 안내서의 나머지 부분에서는 GraphQL 액세스 및 콘텐츠 조각 전달에 중점을 둡니다.

## GraphQL을 사용하여 컨텐츠 조각을 제공하는 방법 {#how-to-deliver-a-content-fragment}

정보 설계자는 콘텐츠를 전달하기 위해 채널 끝점에 대한 쿼리를 설계해야 합니다. 일반적으로 이러한 쿼리는 모델당 끝점당 한 번만 고려하면 됩니다. 이 시작 안내서에서는 하나만 만들면 됩니다.

1. AEM에 로그인하고 [GraphiQL 인터페이스](/help/sites-developing/headless/graphql-api/graphiql-ide.md):
   * 예: `http://<host>:<port>/aem/graphiql.html`.

1. GraphiQL은 GraphQL용 브라우저 내 쿼리 편집기입니다. 이를 사용하여 콘텐츠 조각을 검색하는 쿼리를 작성하여 JSON으로 Headless 방식으로 전달할 수 있습니다.
   * 왼쪽 패널에서 쿼리를 작성할 수 있습니다.
   * 오른쪽 패널에 결과가 표시됩니다.
   * 쿼리 편집기는 쿼리를 쉽게 실행할 수 있는 코드 완성 기능과 단축키를 제공합니다.
      ![GraphiQL 편집기](assets/graphiql.png)

1. 우리가 만든 모델이 `firstName`, `lastName`, `position` 필드가 있는 `person`이라고 가정하면 콘텐츠 조각의 콘텐츠를 검색하는 간단한 쿼리를 작성할 수 있습니다.

   ```text
   query 
   {
     personList {
       items {
         _path
         firstName
         lastName
         position
       }
     }
   }
   ```

1. 쿼리를 왼쪽 패널에 입력합니다.

<!--
   ![GraphiQL query](assets/graphiql-query.png)
-->

1. 을(를) 클릭합니다. **쿼리 실행** (오른쪽 화살표) 아이콘을 클릭하거나 `Ctrl-Enter` 핫키 및 결과가 오른쪽 패널에 JSON으로 표시됩니다.
   ![GraphiQL 결과](assets/graphiql-results.png)

1. 클릭:
   * **문서** 페이지 오른쪽 상단에서 컨텍스트 내 설명서를 표시하여 자신의 모델에 맞는 쿼리를 작성할 수 있습니다.
   * **기록** 맨 위 도구 모음에서 이전 쿼리를 표시합니다.
   * **다른 이름으로 저장** 및 **저장** 쿼리를 저장한 후 **지속되는 쿼리** 패널 및 **게시**.
      ![GraphiQL 설명서](assets/graphiql-documentation.png)

GraphQL은 특정 데이터 세트 또는 개별 데이터 개체를 대상으로 할 수 있을 뿐만 아니라, 개체의 특정 요소, 중첩된 결과를 전달할 수 있는 구조화된 쿼리를 가능하게 하고, 쿼리 변수 등에 대한 지원을 제공합니다.

GraphQL은 반복적인 API 요청과 초과 전달을 방지할 수 있으며 대신 단일 API 쿼리에 대한 응답으로 렌더링에 필요한 것을 정확히 대량으로 전달할 수 있도록 허용합니다. 결과 JSON은 데이터를 다른 사이트나 앱으로 전달하는 데 사용할 수 있습니다.

## 다음 단계 {#next-steps}

이번 단계가 끝났습니다! 이제 AEM의 Headless 콘텐츠 관리에 대한 기본 사항을 이해했습니다. 물론 사용 가능한 기능을 포괄적으로 이해하기 위해 더 깊이 파고들 수 있는 더 많은 리소스가 있습니다.

* **[구성 브라우저](create-configuration.md)** - AEM 구성 브라우저에 대한 세부 정보
* **[콘텐츠 조각](/help/assets/content-fragments/content-fragments.md)** - 콘텐츠 조각 생성 및 관리에 대한 자세한 내용
* **[GraphiQL IDE](/help/sites-developing/headless/graphql-api/graphiql-ide.md)** GraphiQL IDE 사용에 대한 자세한 내용
* **[지속되는 쿼리](/help/sites-developing/headless/graphql-api/persisted-queries.md)** 지속형 쿼리의 자세한 내용은
* **[AEM Assets HTTP API의 콘텐츠 조각 지원](/help/assets/assets-api-content-fragments.md)** - CRUD(만들기, 읽기, 업데이트, 삭제) 작업을 통해 HTTP API로 직접 AEM 콘텐츠에 액세스하는 방법에 대한 자세한 내용
* **[GraphQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md)** - 콘텐츠 조각을 Headless 방식으로 전달하는 방법에 대한 자세한 내용
