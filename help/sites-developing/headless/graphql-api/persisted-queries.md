---
title: 지속 GraphQL 쿼리
description: 성능을 최적화하기 위해 Adobe Experience Manager에서 GraphQL 쿼리를 지속하는 방법을 알아봅니다. HTTP GET 방법을 사용하여 클라이언트 응용 프로그램에서 지속되는 쿼리를 요청할 수 있으며 이 응답을 Dispatcher 및 CDN 레이어에서 캐시할 수 있으므로 궁극적으로 클라이언트 응용 프로그램의 성능을 향상시킬 수 있습니다.
source-git-commit: d87b226d846c6d144e8dfe0b06ec4c296edcad05
workflow-type: tm+mt
source-wordcount: '1428'
ht-degree: 73%

---

# 지속 GraphQL 쿼리 {#persisted-queries-caching}

지속 쿼리는 Adobe Experience Manager(AEM) as a Cloud Service 서버에서 생성 및 저장되는 GraphQL 쿼리입니다. 클라이언트 애플리케이션에서 GET 요청을 사용하여 요청할 수 있습니다. GET 요청의 응답은 Dispatcher 및 CDN(Content Delivery Network) 레이어에서 캐시할 수 있으므로 궁극적으로 요청 클라이언트 애플리케이션의 성능을 향상시킬 수 있습니다. 이 경우 응답을 쉽게 캐시할 수 없는 POST 요청을 사용하여 실행되는 표준 GraphQL 쿼리와는 다릅니다.

<!--
>[!NOTE]
>
>Persisted Queries are recommended. See [GraphQL Query Best Practices (Dispatcher)](/help/headless/graphql-api/content-fragments.md#graphql-query-best-practices) for details, and the related Dispatcher configuration.
-->

[프로덕션 환경으로 이전](#transfer-persisted-query-production)하기 전에 GraphQL 쿼리를 개발, 테스트 및 지속할 수 있도록 [GraphiQL IDE](/help/sites-developing/headless/graphql-api/graphiql-ide.md)가 AEM에 제공됩니다. 사용자 지정이 필요한 경우(예: [캐시 사용자 정의](/help/sites-developing/headless/graphql-api/graphiql-ide.md#caching-persisted-queries)) API를 사용할 수 있습니다. 에 제공된 cURL 예를 참조하십시오. [GraphQL 쿼리를 유지하는 방법](#how-to-persist-query).

## 지속 쿼리 및 끝점 {#persisted-queries-and-endpoints}

지속 쿼리는 항상 [적절한 Sites 구성](/help/sites-developing/headless/graphql-api/graphql-endpoint.md)과 관련된 끝점을 사용해야 합니다. 따라서 다음 중 하나 또는 둘 다를 사용할 수 있습니다.

* 전역 구성 및 끝점
쿼리는 모든 콘텐츠 조각 모델에 액세스할 수 있습니다.
* 특정 Sites 구성 및 끝점
특정 Sites 구성에 대한 지속 쿼리를 만들려면 (관련 콘텐츠 조각 모델에 대한 액세스를 제공하기 위해) 해당 Sites 구성별 끝점이 필요합니다.
예를 들어 WKND Sites 구성을 위해 특별히 지속 쿼리를 만들려면 해당 WKND별 Sites 구성 및 WKND별 끝점을 미리 만들어야 합니다.

>[!NOTE]
>
>자세한 내용은 [구성 브라우저에서 콘텐츠 조각 기능 활성화](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)를 참조하십시오.
>
>적절한 사이트 구성을 위해 **GraphQL 지속 쿼리**&#x200B;를 활성화해야 합니다.

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

## GraphQL 쿼리를 지속하는 방법 {#how-to-persist-query}

처음에 AEM 작성 환경에서 쿼리를 지속한 다음 프로덕션 AEM 게시 환경에 [쿼리를 전송](#transfer-persisted-query-production)하여 애플리케이션에서 사용하는 것이 좋습니다.

다양한 방법으로 쿼리를 지속합니다(다음 포함).

* GraphiQL IDE - [지속 쿼리 저장](/help/sites-developing/headless/graphql-api/graphiql-ide.md#saving-persisted-queries) 참조(기본 방법)
* cURL - 다음 예를 참조하십시오.
* 기타 도구, [Postman](https://www.postman.com/) 포함

GraphiQL IDE는 쿼리를 지속할 수 있는 **기본** 방법입니다. 특정 쿼리를 **cURL** 명령줄 도구:

1. 쿼리를 새 끝점 URL `/graphql/persist.json/<config>/<persisted-label>`에 PUT하여 준비합니다.

   예를 들어 지속 쿼리를 만듭니다.

   ```shell
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

   ```json
   {
     "action": "create",
     "configurationName": "wknd",
     "name": "plain-article-query",
     "shortPath": "/wknd/plain-article-query",
     "path": "/conf/wknd/settings/graphql/persistentQueries/plain-article-query"
   }
   ```

1. 그런 다음 URL `/graphql/execute.json/<shortPath>`을 GET하여 지속 쿼리를 요청할 수 있습니다.

   예를 들어 지속 쿼리를 사용합니다.

   ```shell
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. 이미 존재하는 쿼리 경로에 POST하여 지속 쿼리를 업데이트합니다.

   예를 들어 지속 쿼리를 사용합니다.

   ```shell
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

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. 캐시 제어를 사용하여 래핑된 일반 쿼리를 만듭니다.

   예:

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. 매개변수를 사용하여 지속 쿼리를 만듭니다.

   예:

   ```shell
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


## 지속 쿼리 실행 방법 {#execute-persisted-query}

지속 쿼리를 실행하기 위해 클라이언트 애플리케이션은 다음 구문을 사용하여 GET 요청을 수행합니다.

```
GET <AEM_HOST>/graphql/execute.json/<PERSISTENT_PATH>
```

`PERSISTENT_PATH`는 지속 쿼리가 저장되는 위치에 대한 축약된 경로입니다.

1. 예를 들어 `wknd`는 구성 이름이며 `plain-article-query`는 지속 쿼리의 이름입니다. 쿼리를 실행하려면 다음 작업을 수행하십시오.

   ```shell
   $ curl -X GET \
       https://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. 매개변수를 사용하여 쿼리를 실행합니다.

   >[!NOTE]
   >
   > 지속 쿼리를 실행할 때는 쿼리 변수 및 값을 올바르게 [인코딩](#encoding-query-url)해야 합니다.

   예:

   ```bash
   $ curl -X GET \
       "https://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3Bapath%3D%2Fcontent%2Fdam%2Fwknd%2Fen%2Fmagazine%2Falaska-adventure%2Falaskan-adventures%3BwithReference%3Dfalse
   ```

   자세한 내용은 [쿼리 변수](#query-variables) 사용을 참조하십시오.

## 쿼리 변수 사용 {#query-variables}

쿼리 변수를 지속 쿼리와 함께 사용할 수 있습니다. 쿼리 변수는 변수 이름과 값을 사용하여 앞에 세미콜론(`;`)이 붙은 요청에 추가됩니다. 여러 변수는 세미콜론으로 구분됩니다.

패턴은 다음과 같습니다.

```
<AEM_HOST>/graphql/execute.json/<PERSISTENT_QUERY_PATH>;variable1=value1;variable2=value2
```

예를 들어 다음 쿼리에는 활동 값을 기반으로 목록을 필터링하기 위한 변수 `activity`가 포함되어 있습니다.

```graphql
query getAdventuresByActivity($activity: String!) {
      adventureList (filter: {
        adventureActivity: {
          _expressions: [
            {
              value: $activity
            }
          ]
        }
      }){
        items {
          _path
        adventureTitle
        adventurePrice
        adventureTripLength
      }
    }
  }
```

이 쿼리는 경로 `wknd/adventures-by-activity`에서 지속할 수 있습니다. `activity=Camping` 요청이 다음과 같이 표시되는 지속 쿼리를 호출하려면 다음 작업을 수행하십시오.

```
<AEM_HOST>/graphql/execute.json/wknd/adventures-by-activity%3Bactivity%3DCamping
```

`%3B`는 `;`에 대한 UTF-8 인코딩이며 `%3D`는 `=`에 대한 인코딩입니다. 실행할 지속 쿼리에 대해 쿼리 변수 및 특수 문자를 [올바르게 인코딩](#encoding-query-url)해야 합니다.

## 지속 쿼리 캐싱 {#caching-persisted-queries}

지속되는 쿼리는 [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ko) 및 CDN(Content Delivery Network) 레이어를 사용하면 궁극적으로 요청 클라이언트 애플리케이션의 성능을 향상시킬 수 있습니다.

기본적으로 AEM은 TTL(Time To Live) 정의에 따라 캐시를 무효화합니다. 이러한 TTL은 다음 매개 변수로 정의할 수 있습니다. 이러한 매개 변수는 사용된 메커니즘에 따라 이름에 대한 변형을 사용하여 다양한 방법으로 액세스할 수 있습니다.

| 캐시 유형 | [HTTP 헤더](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control)  | cURL  | OSGi 구성  |
|--- |--- |--- |--- |
| 브라우저 | `max-age` | `cache-control : max-age` | `cacheControlMaxAge` |
| CDN | `s-maxage` | `surrogate-control : max-age` | `surrogateControlMaxAge` |
| CDN | `stale-while-revalidate` | `surrogate-control : stale-while-revalidate ` | `surrogateControlStaleWhileRevalidate` |
| CDN | `stale-if-error` | `surrogate-control : stale-if-error` | `surrogateControlStaleIfError` |

### 작성자 인스턴스 {#author-instances}

작성 인스턴스의 경우 기본값은 다음과 같습니다.

* `max-age`  : 60
* `s-maxage` : 60
* `stale-while-revalidate` : 86400
* `stale-if-error` : 86400

다음 중 하나를 수행합니다.

* OSGi 구성으로 덮어쓸 수 없습니다.
* cURL을 사용하여 HTTP 헤더 설정을 정의하는 요청으로 덮어쓸 수 있습니다. 에는 `cache-control` 및/또는 `surrogate-control`; 예를 보려면 [지속되는 쿼리 수준에서 캐시 관리](#cache-persisted-query-level)

<!-- CQDOC-20186 -->
<!-- following entry is only when the GraphiQL IDE is ready; add cross-reference too -->
<!--
* can be overwritten if you specify values in the **Headers** dialog of the [GraphiQL IDE](#http-cache-headers-graphiql-ide)
-->

### 게시 인스턴스 {#publish-instances}

게시 인스턴스의 경우 기본값은 다음과 같습니다.

* `max-age`  : 60
* `s-maxage` : 7200
* `stale-while-revalidate` : 86400
* `stale-if-error` : 86400

덮어쓸 수 있는 항목은 다음과 같습니다.

<!-- CQDOC-20186 -->
<!-- following entry is only when the GraphiQL IDE is ready -->
<!--
* [from the GraphQL IDE](#http-cache-headers-graphiql-ide)
-->

* [지속형 쿼리 수준에서](#cache-persisted-query-level); 이 작업에는 명령줄 인터페이스에서 cURL을 사용하여 AEM에 쿼리를 게시하고 지속된 쿼리를 게시합니다.

* [OSGi 구성 사용](#cache-osgi-configration)

<!-- CQDOC-20186 -->
<!-- keep for future use; check link -->
<!--
### Managing HTTP Cache Headers in the GraphiQL IDE {#http-cache-headers-graphiql-ide}

The GraphiQL IDE - see [Saving Persisted Queries](/help/sites-developing/headless/graphql-api/graphiql-ide.md#managing-cache)
-->

### 지속되는 쿼리 수준에서 캐시 관리 {#cache-persisted-query-level}

이 작업에는 명령줄 인터페이스에서 cURL을 사용하여 AEM에 쿼리를 게시하는 작업이 포함됩니다.

PUT(create) 메서드의 경우:

```bash
curl -u admin:admin -X PUT \
--url "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
--header "Content-Type: application/json" \
--data '{ "query": "{articleList { items { _path author } } }", "cache-control": { "max-age": 300 }, "surrogate-control": {"max-age":600, "stale-while-revalidate":1000, "stale-if-error":1000} }'
```

POST(업데이트) 메서드의 경우

```bash
curl -u admin:admin -X POST \
--url "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
--header "Content-Type: application/json" \
--data '{ "query": "{articleList { items { _path author } } }", "cache-control": { "max-age": 300 }, "surrogate-control": {"max-age":600, "stale-while-revalidate":1000, "stale-if-error":1000} }'
```

`cache-control`은 생성 시간(PUT) 또는 그 이후에 설정될 수 있습니다(예: 인스턴스의 POST 요청을 통해 설정). AEM에서 기본값을 제공하기 때문에 지속 쿼리 생성 시 캐시 제어는 선택 사항입니다. 자세한 내용은 [GraphQL 쿼리를 유지하는 방법](#how-to-persist-query)예: cURL을 사용하여 쿼리를 유지하는 예

### OSGi 구성을 사용하여 캐시 관리 {#cache-osgi-configration}

캐시를 전체적으로 관리하기 위해 다음을 수행할 수 있습니다 [osgI 설정 구성](/help/sites-deploying/configuring-osgi.md) 대상 **지속된 쿼리 서비스 구성**. 그렇지 않으면 이 OSGi 구성은 [게시 인스턴스의 기본값](#publish-instances).

>[!NOTE]
>
>OSGi 구성은 게시 인스턴스에만 적합합니다. 작성자 인스턴스에 구성이 있지만 은 무시됩니다.

## 앱에서 사용할 쿼리 URL 인코딩 {#encoding-query-url}

애플리케이션에서 사용하는 경우 쿼리 변수를 구성할 때 사용되는 모든 특수 문자(예: 세미콜론(`;`), 등호(`=`), 슬래시(`/`))를 해당 UTF-8 인코딩을 사용하도록 변환해야 합니다.

예:

```bash
curl -X GET \ "https://localhost:4502/graphql/execute.json/wknd/adventure-by-path%3BadventurePath%3D%2Fcontent%2Fdam%2Fwknd%2Fen%2Fadventures%2Fbali-surf-camp%2Fbali-surf-camp"
```

URL은 다음과 같은 부분들로 나눌 수 있습니다.

| URL 부분 | 설명 |
|----------| -------------|
| `/graphql/execute.json` | 지속 쿼리 끝점 |
| `/wknd/adventure-by-path` | 지속 쿼리 경로 |
| `%3B` | `;`의 인코딩 |
| `adventurePath` | 쿼리 변수 |
| `%3D` | `=`의 인코딩 |
| `%2F` | `/`의 인코딩 |
| `%2Fcontent%2Fdam...` | 콘텐츠 조각의 인코딩된 경로 |

일반 텍스트에서 요청 URI는 다음과 같습니다.

```plaintext
/graphql/execute.json/wknd/adventure-by-path;adventurePath=/content/dam/wknd/en/adventures/bali-surf-camp/bali-surf-camp
```

클라이언트 앱에서 지속 쿼리를 사용하려면 AEM Headless 클라이언트 SDK는 [JavaScript](https://github.com/adobe/aem-headless-client-js), [Java](https://github.com/adobe/aem-headless-client-java) 또는 [NodeJS](https://github.com/adobe/aem-headless-client-nodejs)용으로 사용해야 합니다. Headless 클라이언트 SDK는 요청에서 모든 쿼리 변수를 자동으로 적절하게 인코딩합니다.

## 프로덕션 환경에 지속 쿼리 전송  {#transfer-persisted-query-production}

지속 쿼리는 항상 AEM 작성자 서비스에서 만든 다음 AEM 게시 서비스에 게시(복제)해야 합니다. 지속 쿼리는 종종 로컬 또는 개발 환경과 같은 하위 수준 환경에서 생성되고 테스트됩니다. 그런 다음 지속 쿼리를 더 높은 수준의 환경으로 승격하여 궁극적으로 클라이언트 애플리케이션이 사용할 수 있도록 프로덕션 AEM 게시 환경에서 사용할 수 있도록 해야 합니다.

### 패키지 지속 쿼리

지속 쿼리를 [AEM 패키지](/help/sites-administering/package-manager.md)에 빌드할 수 있습니다. 그런 다음 AEM 패키지를 다운로드하여 다른 환경에 설치할 수 있습니다. AEM 패키지를 AEM 작성자 환경에서 AEM 게시 환경으로 복제할 수도 있습니다.

패키지를 제작하려면 다음 작업을 수행하십시오.

1. **도구** > **배포** > **패키지**&#x200B;로 이동합니다.
1. **패키지 만들기**&#x200B;를 탭하여 새 패키지를 만듭니다. 이렇게 하면 패키지를 정의하는 대화 상자가 열립니다.
1. 패키지 정의 대화 상자에서 **일반**&#x200B;에 “wknd-persistent-queries”와 같은 **이름**&#x200B;을 입력합니다.
1. “1.0”과 같은 버전 번호를 입력합니다.
1. **필터** 아래에 새 **필터**&#x200B;를 추가합니다. 경로 파인더를 사용하여 구성 아래에서 `persistentQueries` 폴더를 선택합니다. 예를 들어 `wknd` 구성의 경우 전체 경로는 `/conf/wknd/settings/graphql/persistentQueries`입니다.
1. **저장**&#x200B;을 탭하여 새 패키지 정의를 저장하고 대화 상자를 닫습니다.
1. 새로 생성된 패키지 정의에 있는 **빌드** 버튼을 탭합니다.

패키지를 빌드하면 다음과 같은 작업을 수행할 수 있습니다.

* 패키지를 **다운로드**&#x200B;하고 다른 환경에 다시 업로드할 수 있습니다.
* **기타** > **복제**&#x200B;를 탭하여 패키지를 **복제**&#x200B;할 수 있습니다. 이렇게 하면 연결된 AEM 게시 환경에 패키지가 복제됩니다.

<!--
1. Using replication/distribution tool:
   1. Go to the Distribution tool.
   1. Select tree activation for the configuration (for example, `/conf/wknd/settings/graphql/persistentQueries`).

* Using a workflow (via workflow launcher configuration):
  1. Define a workflow launcher rule for executing a workflow model that would replicate the configuration on different events (for example, create, modify, amongst others).
-->
