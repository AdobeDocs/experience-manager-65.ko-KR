---
title: AEM Assets API를 통해 콘텐츠를 업데이트하는 방법
description: 이 AEM Headless 개발자 여정의 부분에서는 REST API를 통해 콘텐츠 조각의 콘텐츠에 액세스하고 업데이트하는 방법을 대해 알아봅니다.
exl-id: af29cb77-0210-4fc4-8d86-2a833d19b49f
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1066'
ht-degree: 88%

---

# AEM Assets API를 통해 콘텐츠를 업데이트하는 방법 {#update-your-content}

이 [AEM Headless 개발자 여정](overview.md)의 부분에서는 REST API를 통해 콘텐츠 조각의 콘텐츠에 액세스하고 업데이트하는 방법을 대해 알아봅니다.

## 지금까지의 스토리 {#story-so-far}

AEM Headless 번역 여정의 이전 문서인 [AEM Delivery API를 통해 콘텐츠를 액세스하는 방법](access-your-content.md)에서 AEM GraphQL API를 통해 AEM의 Headless 콘텐츠에 액세스하는 방법에 대해 알아보았습니다. 여기에서 알게 된 내용은 다음과 같습니다.

* 고차원의 GraphQL을 이해해야 합니다.
* AEM GraphQL API Target의 작동 방식을 이해할 수 있습니다.
* 몇 가지 실용적인 샘플 쿼리를 이해할 수 있습니다.

이 문서는 해당 기본 사항을 기본으로 하며, 이를 통해 REST API를 사용하여 AEM의 기존 Headless 콘텐츠를 업데이트하는 방법에 대해 살펴볼 수 있습니다.

## 목표 {#objective}

* **대상자**: 고급
* **목표**: REST API를 사용하여 콘텐츠 조각의 콘텐츠에 액세스하고 업데이트하는 방법에 대해 알아보기:
   * AEM Assets HTTP API를 소개합니다.
   * API의 콘텐츠 조각 지원을 소개하고 자세히 설명합니다.
   * API의 세부 정보를 간단히 설명합니다.

<!--
  * Look at sample code to see how things work in practice.
-->

## 콘텐츠 조각에 Assets HTTP API가 필요한 이유는 무엇입니까? {#why-http-api}

Headless 여정의 이전 단계에서는 쿼리를 사용하여 콘텐츠를 검색하는 AEM GraphQL API 사용에 대해 알아보았습니다.

그러면 다른 API가 필요한 이유는 무엇입니까?

Assets HTTP API를 사용하면 다음 작업을 수행할 수 있습니다 **읽기** 콘텐츠를 볼 수 있지만 **만들기**, **업데이트** 및 **삭제** content - GraphQL API로 사용할 수 없는 작업입니다.

Assets REST API는 기본적으로 제공되는 최신 Adobe Experience Manager 버전 설치에서 사용할 수 있습니다.

## Assets HTTP API {#assets-http-api}

Assets HTTP API에는 다음이 포함됩니다.

* Assets REST API
* 콘텐츠 조각의 지원 포함

Assets HTTP API의 현재 구현은 **REST** 아키텍처 스타일을 기반으로 하며 **CRUD** 작업(만들기, 읽기, 업데이트, 삭제)을 통해 콘텐츠(AEM에 저장됨)에 액세스할 수 있습니다.

이러한 작업을 통해 API를 사용하면 JavaScript 프런트 엔드 애플리케이션에 컨텐츠 서비스를 제공하여 Adobe Experience Manager as a Headless CMS(컨텐츠 관리 시스템)를 운영할 수 있습니다. 아니면 HTTP 요청을 실행하고 JSON 응답을 처리할 수 있는 다른 애플리케이션입니다. 예를 들어 단일 페이지 애플리케이션(SPA), 프레임워크 기반 또는 사용자 정의에는 API를 통해 종종 JSON 형식으로 제공되는 콘텐츠가 필요합니다.

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

The Assets REST API exposes access to the properties of a folder; for example, its name, title, and so on. Assets are exposed as child entities of folders, and sub-folders.

>[!NOTE]
>
>Depending on the asset type of the child assets and folders the list of child entities may already contain the full set of properties that defines the respective child entity. Alternatively, only a reduced set of properties may be exposed for an entity in this list of child entities.

### Assets {#assets}

If an asset is requested, the response will return its metadata; such as title, name and other information as defined by the respective asset schema.

The binary data of an asset is exposed as a SIREN link of type `content`.

Assets can have multiple renditions. These are typically exposed as child entities, one exception being a thumbnail rendition, which is exposed as a link of type `thumbnail` ( `rel="thumbnail"`).
-->

## Assets HTTP API 및 콘텐츠 조각 {#assets-http-api-content-fragments}

콘텐츠 조각은 Headless 게재에 사용되고 콘텐츠 조각은 특수 유형의 자산입니다. 텍스트, 숫자, 날짜 등 구조화된 데이터에 액세스하는 데 사용됩니다.

<!--
As there are several differences to *standard* assets (such as images or audio), some additional rules apply to handling them.

### Representation {#representation}

Content fragments:

* Do not expose any binary data.
* Are completely contained in the JSON output (within the `properties` property).

* Are also considered atomic, i.e. the elements and variations are exposed as part of the fragment's properties vs. as links or child entities. This allows for efficient access to the payload of a fragment.

### Content Models and Content Fragments {#content-models-and-content-fragments}

Currently the models that define the structure of a content fragment are not exposed through an HTTP API. Therefore the *consumer* needs to know about the model of a fragment (at least a minimum) - although most information can be inferred from the payload; as data types, and so on. are part of the definition.

To create a content fragment, the (internal repository) path of the model has to be provided.

### Associated Content {#associated-content}

Associated content is currently not exposed.
-->

## Assets REST API 사용 {#using-aem-assets-rest-api}

### 액세스 {#access}

Assets REST API는 `/api/assets`엔드포인트를 사용하여 액세스하려면 자산 경로가 필요합니다(선행 `/content/dam` 없이).

* 즉, 다음 위치에서 자산에 액세스할 수 있습니다.
   * `/content/dam/path/to/asset`
* 다음을 요청해야 합니다.
   * `/api/assets/path/to/asset`

예를 들어 `/content/dam/wknd/en/adventures/cycling-tuscany`에 액세스하기 위해 `/api/assets/wknd/en/adventures/cycling-tuscany.json`을 요청합니다.

>[!NOTE]
>다음을 통한 액세스:
>
>* `/api/assets`는 `.model` 선택기 사용이 필요하지 **않습니다**.
>* `/content/path/to/page`는 `.model` 선택기 사용이 필요&#x200B;**합니다**.

### 작업 {#operation}

HTTP 메서드는 실행할 작업을 결정합니다.

* **GET** - 자산 또는 폴더의 JSON 표현식 검색
* **POST** - 새 자산 또는 폴더 만들기
* **PUT** - 자산 또는 폴더의 속성 업데이트
* **DELETE** - 자산 또는 폴더 삭제

>[!NOTE]
>
>요청 본문 및/또는 URL 매개변수를 사용하여 해당 작업 중 일부를 구성할 수 있습니다(예: **POST** 요청에 의해 폴더 또는 자산이 생성될 수 있도록 정의).

API 참조 설명서에 지원되는 요청의 정확한 형식을 정의합니다.

사용량은 특정 사용 사례와 함께 AEM 작성자 또는 게시 환경 사용 여부에 따라 다를 수 있습니다.

* 작성자 인스턴스에 생성을 바인딩하는 것이 좋습니다(그리고 현재 이 API를 통해 게시할 조각을 복제할 수 없음).
* AEM은 JSON 형식으로만 요청된 콘텐츠를 제공하므로 모두에서 게재할 수 있습니다.

   * AEM 작성자 인스턴스 저장 및 게재는 방화벽 뒤 미디어 라이브러리 애플리케이션에 충분할 수 있습니다.

   * 라이브 웹 게재의 경우 AEM 게시 인스턴스가 권장됩니다.

>[!CAUTION]
>
>AEM 인스턴스의 Dispatcher 구성이 다음에 대한 액세스를 차단할 수 있습니다. `/api`.

>[!NOTE]
>
>자세한 내용은 API 참조를 참조하십시오. 특히, [Adobe Experience Manager Assets API - 콘텐츠 조각](https://www.adobe.io/experience-manager/reference-materials/6-5/assets-api-content-fragments/index.html).

### 읽기/게재 {#read-delivery}

사용은 다음을 통해서입니다.

`GET /{cfParentPath}/{cfName}.json`

예:

`http://<host>/api/assets/wknd/en/adventures/cycling-tuscany.json`

응답은 콘텐츠 조각에서와 같이 구조화된 콘텐츠가 있는 직렬화된 JSON입니다. 참조 URL로 참조를 게재합니다.

다음과 같이 두 가지 유형의 읽기 작업이 가능합니다.

* 경로를 통해 특정 콘텐츠 조각을 읽으면 콘텐츠 조각의 JSON 표현식이 반환됩니다.
* 경로를 통해 콘텐츠 조각의 폴더 읽기: 폴더 내 모든 콘텐츠 조각의 JSON 표현식이 반환됩니다.

### 만들기 {#create}

사용은 다음을 통해서입니다.

`POST /{cfParentPath}/{cfName}`

본문에는 콘텐츠 조각 요소에 설정해야 하는 초기 콘텐츠를 비롯해 생성할 콘텐츠 조각의 JSON 표현식이 포함되어야 합니다. `cq:model` 속성 설정이 필수이며 유효한 콘텐츠 조각 모델을 지정해야 합니다. 지정하지 못하면 오류가 발생합니다. 또한 `application/json`으로 설정된 헤더 `Content-Type`을 추가해야 합니다.

### 업데이트 {#update}

사용은 다음을 통해서입니다.

`PUT /{cfParentPath}/{cfName}`

본문에는 특정 콘텐츠 조각에 업데이트할 항목의 JSON 표현식이 포함되어야 합니다.

이는 간단히 콘텐츠 조각의 제목이나 설명 또는 단일 요소나 모든 요소 값 및/또는 메타데이터일 수 있습니다.

### 삭제 {#delete}

사용은 다음을 통해서입니다.

`DELETE /{cfParentPath}/{cfName}`

AEM Assets REST API 사용에 대한 자세한 내용은 다음 자료를 참조하십시오.

* Adobe Experience Manager Assets HTTP API (추가 리소스)
* AEM Assets HTTP API의 콘텐츠 조각 지원 (추가 리소스)

## 다음 단계 {#whats-next}

AEM Headless 개발자 여정의 한 부분을 완료했으므로,

* AEM Assets HTTP API의 기본 사항을 이해할 수 있습니다.
* 이 API에서 콘텐츠 조각을 지원하는 방법을 이해할 수 있습니다.

<!--
* Have experience with sample code and know how the API works in practice.
-->

<!-- The "How to put it all together" page isn't going to be published until the first public release of the Headless SDK. Temporarily commenting out the reference below. -->

<!--You should continue your AEM headless journey by next reviewing the document [How to Put It All Together - Your App and Your Content in AEM Headless](put-it-all-together.md) where you learn how to take your AEM Headless project and prepare it for going live.-->

다음 문서에서는 AEM Headless 여정을 계속 진행해야 합니다 [Headless 애플리케이션 실행 방법](go-live.md) 여기에서 AEM Headless 프로젝트를 실제로 라이브로 볼 수 있습니다!

## 추가 리소스 {#additional-resources}

* [Assets HTTP API](/help/assets/mac-api-assets.md)
* [콘텐츠 조각 REST API](/help/assets/assets-api-content-fragments.md)
   * [API 참조](/help/assets/assets-api-content-fragments.md#api-reference)
* [Adobe Experience Manager Assets API - 콘텐츠 조각](https://www.adobe.io/experience-manager/reference-materials/6-5/assets-api-content-fragments/index.html)
* [콘텐츠 조각을 사용하여 작업](/help/assets/content-fragments/content-fragments.md)
* [AEM 핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)
* [CORS/AEM 설명](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
* [비디오 - AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)에서 CORS용 개발
* [AEM as a Headless CMS 소개](/help/sites-developing/headless/introduction.md)
* [AEM 개발자 포털](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html)
* [AEM의 Headless 튜토리얼](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html)
