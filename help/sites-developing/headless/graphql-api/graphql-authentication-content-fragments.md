---
title: 컨텐츠 조각의 원격 Adobe Experience Manager GraphQL 쿼리 인증
description: Headless 콘텐츠 게재를 보호하기 위해 원격 Adobe Experience Manager GraphQL 쿼리에 필요한 인증을 이해합니다.
feature: Content Fragments,GraphQL API
exl-id: 167f3318-7bc7-48fc-aaa9-73da43433f2f
solution: Experience Manager, Experience Manager Sites
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: a642c50e-80eb-4fc1-a5d2-f3762d1f841d
    internal-label: Administration
subfeature_v2:
  - id: e9db7c79-8f65-4281-a439-c9049296d903
    internal-label: Content Fragments
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 41%
---
# 컨텐츠 조각의 원격 Adobe Experience Manager GraphQL 쿼리 인증 {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

콘텐츠 조각 배달을 위한 [Adobe Experience Manager(AEM) GraphQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md)의 주요 사용 사례는 서드파티 응용 프로그램 또는 서비스의 원격 쿼리를 수락하는 것입니다. Headless 콘텐츠 게재를 보호하기 위해 이러한 원격 쿼리에는 인증된 API 액세스가 필요할 수 있습니다.

>[!NOTE]
>
>테스트 및 개발을 위해 [GraphiQL 인터페이스](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#graphiql-interface)를 사용하여 AEM GraphQL API에 직접 액세스할 수도 있습니다.

인증을 위해 서드파티 서비스는 AEM 계정 사용자 이름과 암호를 사용하여 인증해야 합니다.

<!-- 6.5.10.0 - does this content/page need to be migrated? -->

<!--
For authentication the third-party service needs to [retrieve an Access Token](#retrieving-access-token), that can then be [used in the GraphQL Request](#use-access-token-in-graphql-request).

## Retrieving an Access Token {#retrieving-access-token}

See [Generating Access Tokens for Server Side APIs](/help/sites-developing/generating-access-tokens-for-server-side-apis.md) for full details.

## Using the Access Token in a GraphQL Request {#use-access-token-in-graphql-request}

For a third-party service to connect with an AEM instance it needs to have an *Access Token*. The service must then add this token to the `Authorization` header on the POST request. 

For example, a GraphQL Authorization Header:

```xml
Authorization: Bearer <access_token>
```

## Permission Requirements {#permission-requirements}

All requests made using the access token will actually be made *by the user account that generated the token*. 

This means that you need to check that the account has the permissions required to run GraphQL queries. 

You can check this by using GraphiQL on the local instance.
-->
