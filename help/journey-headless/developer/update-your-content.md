---
title: AEM Assets API를 통해 콘텐츠를 업데이트하는 방법
description: AEM Headless Developer 여정의 이 부분에서 REST API를 사용하여 컨텐츠 조각의 컨텐츠에 액세스하고 업데이트하는 방법을 알아봅니다.
exl-id: af29cb77-0210-4fc4-8d86-2a833d19b49f
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 3%

---

# AEM Assets API를 통해 콘텐츠를 업데이트하는 방법 {#update-your-content}

의 이 부분에서 [AEM Headless Developer 여정,](overview.md) rest API를 사용하여 컨텐츠 조각에 액세스하고 업데이트하는 방법을 알아봅니다.

## 지금까지의 이야기 {#story-so-far}

AEM 헤드리스 여정의 이전 문서에서, [AEM 배달 API를 통해 콘텐츠에 액세스하는 방법](access-your-content.md) AEM GraphQL API를 통해 AEM에서 헤드리스 컨텐츠에 액세스하는 방법을 배웠으며 이제 다음을 수행해야 합니다.

* GraphQL에 대해 높은 수준의 이해를 제공합니다.
* AEM GraphQL API의 작동 방식을 이해합니다.
* 몇 가지 실용적인 샘플 쿼리를 이해합니다.

이 문서는 REST API를 통해 AEM에서 기존 헤드리스 콘텐츠를 업데이트하는 방법을 이해할 수 있도록 이러한 기본 사항을 기반으로 합니다.

## 목표 {#objective}

* **Audience**: 고급
* **목표**: REST API를 사용하여 컨텐츠 조각의 컨텐츠에 액세스하고 업데이트하는 방법을 알아봅니다.
   * AEM Assets HTTP API 소개.
   * API에서 컨텐츠 조각 지원을 도입하고 논의합니다.
   * API의 세부 사항을 보여줍니다.

<!--
  * Look at sample code to see how things work in practice.
-->

## 컨텐츠 조각에 Assets HTTP API가 필요한 이유는 무엇입니까 {#why-http-api}

헤드리스 여정의 이전 단계에서 AEM GraphQL API를 사용하여 쿼리를 사용하여 콘텐츠를 검색하는 방법을 알아보았습니다.

다른 API가 필요한 이유는 무엇입니까?

자산 HTTP API를 사용하면 다음 작업을 수행할 수 있습니다 **읽기** 사용자의 콘텐츠는 물론 **만들기**, **업데이트** 및 **삭제** 컨텐츠 - GraphQL API에서는 사용할 수 없는 작업입니다.

Assets REST API는 최신 Adobe Experience Manager 버전을 바로 설치할 때마다 사용할 수 있습니다.

## Assets HTTP API {#assets-http-api}

자산 HTTP API는 다음을 포함합니다.

* 자산 REST API
* 컨텐츠 조각에 대한 지원 포함

자산 HTTP API의 현재 구현은 **REST** 아키텍처 스타일 및 를 통해 컨텐츠(AEM에 저장됨)에 액세스할 수 있습니다. **CRUD** 작업(만들기, 읽기, 업데이트, 삭제).

이러한 작업을 사용하여 API를 사용하면 JavaScript 프런트 엔드 애플리케이션에 컨텐츠 서비스를 제공하여 Adobe Experience Manager을 헤드리스 CMS(Content Management System)로 운영할 수 있습니다. 또는 HTTP 요청을 실행하고 JSON 응답을 처리할 수 있는 다른 애플리케이션입니다. 예를 들어, 단일 페이지 애플리케이션(SPA), 프레임워크 기반 또는 사용자 지정 환경에서는 API를 통해 제공되는 컨텐츠가 필요합니다(일반적으로 JSON 형식).

<!--
>[!NOTE]
>
>It is not possible to customize JSON output from the Assets REST API. 

The Assets REST API:

* follows the HATEOAS principle
* implements the SIREN format

## Key Concepts {#key-concepts}

The Assets REST API offers REST-style access to assets stored within an AEM instance. 

It uses the `/api/assets` endpoint and requires the path of the asset to access it (without the leading `/content/dam`). 

* This means that to access the asset at:
  * `/content/dam/path/to/asset`
* You need to request:
  * `/api/assets/path/to/asset` 

For example, to access `/content/dam/wknd/en/adventures/cycling-tuscany`, request `/api/assets/wknd/en/adventures/cycling-tuscany.json` 

>[!NOTE]
>Access over:
>
>* `/api/assets` **does not** need the use of the `.model` selector.
>* `/content/path/to/page` **does** require the use of the `.model` selector.

The HTTP method determines the operation to be executed:

* **GET** - to retrieve a JSON representation of an asset or a folder
* **POST** - to create new assets or folders
* **PUT** - to update the properties of an asset or folder
* **DELETE** - to delete an asset or folder

>[!NOTE]
>
>The request body and/or URL parameters can be used to configure some of these operations; for example, define that a folder or an asset should be created by a **POST** request.

The exact format of supported requests is defined in the API Reference documentation. 

### Transactional Behavior {#transactional-behavior}

All requests are atomic.

This means that subsequent (`write`) requests cannot be combined into a single transaction that could succeed or fail as a single entity.

### Security {#security}

If the Assets REST API is used within an environment without specific authentication requirements, AEM's CORS filter needs to be configured correctly.

>[!NOTE]
>
>For further information see:
>
>* CORS/AEM explained
>* Video - Developing for CORS with AEM

In environments with specific authentication requirements, OAuth is recommended.

## Available Features {#available-features}

Content Fragments are a specific type of Asset, see Working with Content Fragments.

For further information about features available through the API see:

* The Assets REST API (Additional Resources) 
* Entity Types, where the features specific to each supported type (as relevant to Content Fragments) are explained 

### Paging {#paging}

The Assets REST API supports paging (for GET requests) via the URL parameters:

* `offset` - the number of the first (child) entity to retrieve
* `limit` - the maximum number of entities returned

The response will contain paging information as part of the `properties` section of the SIREN output. This `srn:paging` property contains the total number of (child) entities ( `total`), the offset and the limit ( `offset`, `limit`) as specified in the request.

>[!NOTE]
>
>Paging is typically applied on container entities (i.e. folders or assets with renditions), as it relates to the children of the requested entity.

#### Example: Paging {#example-paging}

`GET /api/assets.json?offset=2&limit=3`

```json
...
"properties": {
    ...
    "srn:paging": {
        "total": 7,
        "offset": 2,
        "limit": 3
    }
    ...
}
...
```

## Entity Types {#entity-types}

### Folders {#folders}

Folders act as containers for assets and other folders. They reflect the structure of the AEM content repository.

The Assets REST API exposes access to the properties of a folder; for example its name, title, etc. Assets are exposed as child entities of folders, and sub-folders.

>[!NOTE]
>
>Depending on the asset type of the child assets and folders the list of child entities may already contain the full set of properties that defines the respective child entity. Alternatively, only a reduced set of properties may be exposed for an entity in this list of child entities.

### Assets {#assets}

If an asset is requested, the response will return its metadata; such as title, name and other information as defined by the respective asset schema.

The binary data of an asset is exposed as a SIREN link of type `content`.

Assets can have multiple renditions. These are typically exposed as child entities, one exception being a thumbnail rendition, which is exposed as a link of type `thumbnail` ( `rel="thumbnail"`).
-->

## 자산 HTTP API 및 컨텐츠 조각 {#assets-http-api-content-fragments}

컨텐츠 조각은 헤드리스 게재에 사용되며 컨텐츠 조각 은 특별한 유형의 자산입니다. 텍스트, 숫자, 날짜 등과 같은 구조화된 데이터에 액세스하는 데 사용됩니다.

<!--
As there are several differences to *standard* assets (such as images or audio), some additional rules apply to handling them.

### Representation {#representation}

Content fragments:

* Do not expose any binary data.
* Are completely contained in the JSON output (within the `properties` property).

* Are also considered atomic, i.e. the elements and variations are exposed as part of the fragment's properties vs. as links or child entities. This allows for efficient access to the payload of a fragment.

### Content Models and Content Fragments {#content-models-and-content-fragments}

Currently the models that define the structure of a content fragment are not exposed through an HTTP API. Therefore the *consumer* needs to know about the model of a fragment (at least a minimum) - although most information can be inferred from the payload; as data types, etc. are part of the definition.

To create a new content fragment, the (internal repository) path of the model has to be provided.

### Associated Content {#associated-content}

Associated content is currently not exposed.
-->

## Assets REST API 사용 {#using-aem-assets-rest-api}

### 액세스 {#access}

Assets REST API는 `/api/assets` 엔드포인트 및에 액세스할 자산의 경로가 필요합니다(선행 없이). `/content/dam`).

* 즉, 다음 위치에서 자산에 액세스합니다.
   * `/content/dam/path/to/asset`
* 다음을 요청해야 합니다.
   * `/api/assets/path/to/asset`

예를 들어, `/content/dam/wknd/en/adventures/cycling-tuscany`, 요청 `/api/assets/wknd/en/adventures/cycling-tuscany.json`

>[!NOTE]
>액세스 권한:
>
>* `/api/assets` **포함하지 않음** 의 사용 필요 `.model` 선택기.
>* `/content/path/to/page` **does** 를 사용하려면 `.model` 선택기.


### 작업 {#operation}

HTTP 메서드는 실행할 작업을 결정합니다.

* **GET** - 자산 또는 폴더의 JSON 표현을 검색하려면
* **POST** - 새 자산 또는 폴더를 만들려면
* **PUT** - 자산 또는 폴더의 속성을 업데이트하려면
* **DELETE** - 자산 또는 폴더를 삭제하려면

>[!NOTE]
>
>요청 본문 및/또는 URL 매개 변수를 사용하여 이러한 작업 중 일부를 구성할 수 있습니다. 예를 들어, 폴더 또는 자산을 **POST** 요청.

지원되는 요청의 정확한 형식은 API 참조 설명서에서 정의됩니다.

사용법은 특정 사용 사례와 함께 AEM 작성자 또는 게시 환경을 사용하는지에 따라 다를 수 있습니다.

* 작성은 작성자 인스턴스에 바인딩된 것이 좋습니다(현재 이 API를 사용하여 게시할 조각을 복제할 방법이 없음).
* AEM은 요청된 컨텐츠를 JSON 형식으로만 제공하므로 두 방법 모두에서 게재가 가능합니다.

   * AEM 작성자 인스턴스에서 저장 및 전달하면 방화벽 뒤에서 미디어 라이브러리 응용 프로그램이 충분해야 합니다.

   * 라이브 웹 전달을 위해 AEM 게시 인스턴스가 권장됩니다.

>[!CAUTION]
>
>AEM 인스턴스의 Dispatcher 구성에 대한 액세스가 차단될 수 있음 `/api`.

>[!NOTE]
>
>자세한 내용은 API 참조를 참조하십시오. 특히, [Adobe Experience Manager Assets API - 컨텐츠 조각](https://www.adobe.io/experience-manager/reference-materials/6-5/assets-api-content-fragments/index.html).

### 읽기/전달 {#read-delivery}

사용 방법:

`GET /{cfParentPath}/{cfName}.json`

예:

`http://<host>/api/assets/wknd/en/adventures/cycling-tuscany.json`

응답은 컨텐츠 조각에서와 같이 구조화된 컨텐츠와 함께 일련화된 JSON입니다. 참조는 참조 URL로 전달됩니다.

두 가지 유형의 읽기 작업이 가능합니다.

* 특정 컨텐츠 조각을 경로별로 읽으면 컨텐츠 조각의 JSON 표현이 반환됩니다.
* 경로별 컨텐츠 조각 폴더 읽기: 이렇게 하면 폴더 내에 있는 모든 컨텐츠 조각의 JSON 표현이 반환됩니다.

### 만들기 {#create}

사용 방법:

`POST /{cfParentPath}/{cfName}`

본문에는 컨텐츠 조각 요소에서 설정해야 하는 초기 컨텐츠를 포함하여 만들 컨텐츠 조각의 JSON 표현이 포함되어 있어야 합니다. 을(를) 설정해야 합니다 `cq:model` 속성 및 유효한 컨텐츠 조각 모델을 가리켜야 합니다. 실패하면 오류가 발생합니다. 헤더를 추가해야 합니다 `Content-Type` 설정됨 `application/json`.

### 업데이트 {#update}

사용 방법

`PUT /{cfParentPath}/{cfName}`

본문에는 주어진 컨텐츠 조각에 대해 업데이트할 사항에 대한 JSON 표현이 포함되어 있어야 합니다.

컨텐츠 조각, 단일 요소 또는 모든 요소 값 및/또는 메타데이터의 제목 또는 설명일 수 있습니다.

### 삭제 {#delete}

사용 방법:

`DELETE /{cfParentPath}/{cfName}`

AEM Assets REST API 사용에 대한 자세한 내용은 다음을 참조할 수 있습니다.

* Adobe Experience Manager Assets HTTP API(추가 리소스)
* AEM Assets HTTP API의 컨텐츠 조각 지원(추가 리소스)

## 다음 단계 {#whats-next}

AEM Headless 개발자 여정의 이 부분을 완료했으므로 다음을 수행해야 합니다.

* AEM Assets HTTP API의 기본 사항을 이해합니다.
* 이 API에서 컨텐츠 조각이 지원되는 방식을 이해합니다.

<!--
* Have experience with sample code and know how the API works in practice.
-->

<!-- The "How to put it all together" page isn't going to be published until the first public release of the Headless SDK. Temporarily commenting out the reference below. -->

<!--You should continue your AEM headless journey by next reviewing the document [How to Put It All Together - Your App and Your Content in AEM Headless](put-it-all-together.md) where you learn how to take your AEM Headless project and prepare it for going live.-->

다음에 문서를 검토하여 AEM 헤드리스 여정을 계속해야 합니다 [헤드리스 애플리케이션을 사용하여 라이브로 전환하는 방법](go-live.md) AEM Headless 프로젝트를 라이브로 전환하는 곳!

## 추가 리소스 {#additional-resources}

* [자산 HTTP API](/help/assets/mac-api-assets.md)
* [콘텐츠 조각 REST API](/help/assets/assets-api-content-fragments.md)
   * [API 참조](/help/assets/assets-api-content-fragments.md#api-reference)
* [Adobe Experience Manager Assets API - 컨텐츠 조각](https://www.adobe.io/experience-manager/reference-materials/6-5/assets-api-content-fragments/index.html)
* [콘텐츠 조각을 사용하여 작업](/help/assets/content-fragments/content-fragments.md)
* [AEM 핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)
* [CORS/AEM 설명](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
* [비디오 - AEM을 사용한 CORS용 개발](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)
