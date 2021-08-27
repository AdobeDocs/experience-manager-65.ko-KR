---
title: 컨텐츠 조각에 대한 원격 AEM GraphQL 쿼리 인증
description: 헤드리스 콘텐츠 전달을 보호하기 위해 Remote AEM GraphQL 쿼리에 필요한 인증을 이해합니다.
feature: Content Fragments,GraphQL API
source-git-commit: 2f647fc640d3809dc684bce397831ab37fb94b07
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# 컨텐츠 조각에 대한 원격 AEM GraphQL 쿼리 인증 {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

[Adobe Experience Manager(AEM) GraphQL API for Content Fragment Delivery](/help/assets/content-fragments/graphql-api-content-fragments.md)에 대한 기본 사용 사례는 타사 애플리케이션 또는 서비스의 원격 쿼리를 수락하는 것입니다. 이러한 원격 쿼리는 헤드리스 콘텐츠 전달을 보호하기 위해 인증된 API 액세스가 필요할 수 있습니다.

>[!NOTE]
>
>테스트 및 개발을 위해 [GraphiQL 인터페이스](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface) 인터페이스를 사용하여 AEM GraphQL API에 직접 액세스할 수도 있습니다.

인증을 위해 타사 서비스는 [액세스 토큰](#retrieving-access-token)을 검색해야 하며, 이 토큰은 GraphQL 요청](#use-access-token-in-graphql-request)에 사용될 수 있습니다.[

## 액세스 토큰 검색 {#retrieving-access-token}

<!-- 6.5.10.0 - does this page need to be migrated? -->

<!--
See [Generating Access Tokens for Server Side APIs](/help/sites-developing/generating-access-tokens-for-server-side-apis.md) for full details.
-->

## GraphQL 요청에서 액세스 토큰 사용 {#use-access-token-in-graphql-request}

타사 서비스가 AEM 인스턴스와 연결하려면 *액세스 토큰*&#x200B;이 있어야 합니다. 그런 다음 서비스는 이 토큰을 POST 요청의 `Authorization` 헤더에 추가해야 합니다.

예를 들어 GraphQL 인증 헤더:

```xml
Authorization: Bearer <access_token>
```

## 권한 요구 사항 {#permission-requirements}

액세스 토큰을 사용하여 수행한 모든 요청은 실제로 토큰&#x200B;*을 생성한 사용자 계정에 의해*&#x200B;됩니다.

즉, GraphQL 쿼리를 실행하는 데 필요한 권한이 계정에 있는지 확인해야 합니다.

로컬 인스턴스에서 GraphiQL을 사용하여 이를 확인할 수 있습니다.
