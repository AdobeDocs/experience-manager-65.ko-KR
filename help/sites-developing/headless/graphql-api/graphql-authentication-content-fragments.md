---
title: 콘텐츠 조각의 원격 AEM GraphQL 쿼리 인증
description: Headless 콘텐츠 전송을 보호하기 위해 원격 AEM GraphQL 쿼리에 필요한 인증을 이해합니다.
feature: Content Fragments,GraphQL API
exl-id: 167f3318-7bc7-48fc-aaa9-73da43433f2f
source-git-commit: ad0f0bd8b0c230e002c734adca87da22bfa3a7cd
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 61%

---

# 콘텐츠 조각의 원격 AEM GraphQL 쿼리 인증 {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

에 대한 기본 사용 사례 [Adobe Experience Manager (AEM) GraphQL API for Content Fragment Delivery](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) 는 타사 응용 프로그램 또는 서비스의 원격 쿼리를 수락하는 것입니다. Headless 콘텐츠 전송을 보호하기 위해 이러한 원격 쿼리에는 인증된 API 액세스가 필요할 수 있습니다.

>[!NOTE]
>
>테스트 및 개발을 위해 [GraphiQL 인터페이스](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#graphiql-interface) 인터페이스를 사용하여 AEM GraphQL API에 직접 액세스할 수도 있습니다.

인증을 위해 타사 서비스는 AEM 계정 사용자 이름과 암호를 사용하여 인증해야 합니다.

<!-- 6.5.10.0 - does this content/page need to be migrated? -->

<!--
For authentication the third party service needs to [retrieve an Access Token](#retrieving-access-token), that can then be [used in the GraphQL Request](#use-access-token-in-graphql-request).

## Retrieving an Access Token {#retrieving-access-token}

See [Generating Access Tokens for Server Side APIs](/help/sites-developing/generating-access-tokens-for-server-side-apis.md) for full details.

## Using the Access Token in a GraphQL Request {#use-access-token-in-graphql-request}

For a third party service to connect with an AEM instance it needs to have an *Access Token*. The service must then add this token to the `Authorization` header on the POST request. 

For example, a GraphQL Authorization Header:

```xml
Authorization: Bearer <access_token>
```

## Permission Requirements {#permission-requirements}

All requests made using the access token will actually be made *by the user account that generated the token*. 

This means that you need to check that the account has the permissions required to run GraphQL queries. 

You can check this by using GraphiQL on the local instance.
-->
