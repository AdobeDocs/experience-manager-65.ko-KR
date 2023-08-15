---
title: Assets HTTP API의 Adobe Experience Manager 콘텐츠 조각 지원
description: AEM Headless 게재 기능의 중요한 부분인 Assets HTTP API의 콘텐츠 조각에 대한 지원에 대해 알아봅니다.
feature: Content Fragments,Assets HTTP API
role: Developer
exl-id: 0f9efb47-a8d1-46d9-b3ff-a6c0741ca138
hide: true
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1956'
ht-degree: 24%

---

# AEM Assets HTTP API의 콘텐츠 조각 지원 {#content-fragments-support-in-aem-assets-http-api}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/assets-api-content-fragments.html?lang=ko) |
| AEM 6.5 | 이 문서 |


## 개요 {#overview}

AEM Headless 게재 기능의 중요한 부분인 Assets HTTP API의 콘텐츠 조각에 대한 지원에 대해 알아봅니다.

>[!NOTE]
>
>다음 [Assets HTTP API](/help/assets/mac-api-assets.md) 는 다음을 포함합니다.
>
>* Assets REST API
>* 콘텐츠 조각의 지원 포함
>
>Assets HTTP API의 현재 구현은 [나머지](https://en.wikipedia.org/wiki/Representational_state_transfer) 아키텍처 스타일입니다.

다음 [Assets REST API](/help/assets/mac-api-assets.md) 개발자는 Adobe Experience Manager에서 CRUD(만들기, 읽기, 업데이트, 삭제) 작업을 통해 HTTP API를 통해 직접 콘텐츠(AEM에 저장됨)에 액세스할 수 있습니다.

API를 사용하면 JavaScript 프런트 엔드 애플리케이션에 컨텐츠 서비스를 제공하여 Adobe Experience Manager as a Headless CMS(컨텐츠 관리 시스템)를 운영할 수 있습니다. 아니면 HTTP 요청을 실행하고 JSON 응답을 처리할 수 있는 다른 애플리케이션입니다.

예를 들어 프레임워크 기반 또는 사용자 지정 SPA(단일 페이지 애플리케이션)에서는 HTTP API를 통해 제공되는 콘텐츠(종종 JSON 형식)가 필요합니다.

While [AEM 핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 이를 위해 필요한 읽기 작업을 수행할 수 있는 유연하고 사용자 지정 가능한 API를 제공하며, JSON 출력을 사용자 지정할 수 있습니다. 전용 AEM 템플릿을 기반으로 하는 페이지에서 호스팅해야 하므로 구현에 AEM WCM(Web Content Management) 노하우가 필요합니다. 모든 SPA 개발 조직이 이러한 지식에 직접 액세스할 수 있는 것은 아닙니다.

이때 Assets REST API를 사용할 수 있습니다. 이를 통해 개발자는 페이지에 에셋을 먼저 임베드할 필요 없이 에셋(예: 이미지 및 콘텐츠 조각)에 직접 액세스하고 콘텐츠를 직렬화된 JSON 형식으로 전달할 수 있습니다.

>[!NOTE]
>
>Assets REST API에서 JSON 출력을 사용자 정의할 수 없습니다.

Assets REST API를 사용하면 개발자가 기존 에셋, 콘텐츠 조각 및 폴더를 새로 만들거나 업데이트하거나 삭제하여 콘텐츠를 수정할 수도 있습니다.

Assets REST API:

* 다음 [하테오아스의 원리](https://en.wikipedia.org/wiki/HATEOAS)

* 를 구현합니다. [SIREN 형식](https://github.com/kevinswiber/siren)

## 사전 요구 사항 {#prerequisites}

Assets REST API는 최신 AEM 버전의 각 기본 설치에서 사용할 수 있습니다.

## 주요 개념 {#key-concepts}

자산 REST API 오퍼 [나머지](https://en.wikipedia.org/wiki/Representational_state_transfer)- AEM 인스턴스 내에 저장된 자산에 대한 스타일 액세스.

다음을 사용합니다. `/api/assets` 끝점 및 이에 액세스하려면 자산의 경로가 필요합니다(행간 제외). `/content/dam`).

* 즉, 다음 위치에서 에셋에 액세스할 수 있습니다.
   * `/content/dam/path/to/asset`
* 다음을 요청해야 합니다.
   * `/api/assets/path/to/asset`

예를 들어 `/content/dam/wknd/en/adventures/cycling-tuscany`에 액세스하기 위해 `/api/assets/wknd/en/adventures/cycling-tuscany.json`을 요청합니다.

>[!NOTE]
>다음을 통한 액세스:
>
>* `/api/assets`는 `.model` 선택기 사용이 필요하지 **않습니다**.
>* `/content/path/to/page`는 `.model` 선택기 사용이 필요&#x200B;**합니다**.

HTTP 메서드는 실행할 작업을 결정합니다.

* **GET** - 에셋 또는 폴더의 JSON 표현식 검색
* **POST** - 새 에셋 또는 폴더 만들기
* **PUT** - 에셋 또는 폴더의 속성 업데이트
* **DELETE** - 에셋 또는 폴더 삭제

>[!NOTE]
>
>요청 본문 및/또는 URL 매개변수를 사용하여 해당 작업 중 일부를 구성할 수 있습니다(예: **POST** 요청에 의해 폴더 또는 에셋이 생성될 수 있도록 정의).

지원되는 요청의 정확한 형식은 [API 참조](/help/assets/assets-api-content-fragments.md#api-reference) 설명서를 참조하십시오.

### 트랜잭션 동작 {#transactional-behavior}

모든 요청은 원자입니다.

즉, 다음 (`write`) 요청은 단일 엔티티로 성공하거나 실패할 수 있는 단일 트랜잭션으로 결합할 수 없습니다.

### AEM (Assets) REST API 및 AEM 구성 요소 {#aem-assets-rest-api-versus-aem-components}

<table>
 <thead>
  <tr>
   <td>Aspect</td>
   <td>Assets REST API<br/> </td>
   <td>AEM 구성 요소<br/> (Sling 모델을 사용하는 구성 요소)</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>지원되는 사용 사례</td>
   <td>일반적인 목적.</td>
   <td><p>단일 페이지 애플리케이션(SPA) 또는 기타(콘텐츠 소비) 컨텍스트에서 사용하도록 최적화되었습니다.</p> <p>레이아웃 정보를 포함할 수도 있습니다.</p> </td>
  </tr>
  <tr>
   <td>지원되는 작업</td>
   <td><p>만들기, 읽기, 업데이트, 삭제.</p> <p>엔터티 유형에 따라 추가 작업 포함</p> </td>
   <td>읽기 전용.</td>
  </tr>
  <tr>
   <td>액세스</td>
   <td><p>직접 액세스할 수 있습니다.</p> <p>를 사용합니다. <code>/api/assets </code>끝점, 매핑됨 <code>/content/dam</code> (저장소에서).</p> 
   <p>예제 경로는 다음과 같습니다. <code>/api/assets/wknd/en/adventures/cycling-tuscany.json</code></p>
   </td>
    <td><p>AEM 페이지에서 AEM 구성 요소를 통해 참조되어야 합니다.</p> <p>를 사용합니다. <code>.model</code> JSON 표현식을 만드는 선택기입니다.</p> <p>예제 경로는 다음과 같습니다.<br/> <code>/content/wknd/language-masters/en/adventures/cycling-tuscany.model.json</code></p> 
   </td>
  </tr>
  <tr>
   <td>보안</td>
   <td><p>여러 옵션이 가능합니다.</p> <p>OAuth가 제안됩니다. 표준 설정과 별도로 구성할 수 있습니다.</p> </td>
   <td>AEM 표준 설정을 사용합니다.</td>
  </tr>
  <tr>
   <td>아키텍처 설명</td>
   <td><p>쓰기 액세스는 일반적으로 작성자 인스턴스를 해결합니다.</p> <p>읽기는 게시 인스턴스로 진행될 수도 있습니다.</p> </td>
   <td>이 접근 방식은 읽기 전용이므로 일반적으로 게시 인스턴스에 사용됩니다.</td>
  </tr>
  <tr>
   <td>출력</td>
   <td>JSON 기반 SIREN 출력: 자세한 정보지만 강력한. 콘텐츠 내에서 탐색할 수 있습니다.</td>
   <td>JSON 기반 소유 출력, Sling 모델을 통해 구성 가능. 콘텐츠 구조를 탐색하는 것은 구현하기 어렵습니다(하지만 반드시 불가능하지는 않음).</td>
  </tr>
 </tbody>
</table>

### 보안 {#security}

Assets REST API가 특정 인증 요구 사항 없이 환경 내에서 사용되는 경우 AEM CORS 필터를 올바르게 구성해야 합니다.

>[!NOTE]
>
>자세한 내용은 다음을 참조하십시오.
>
>* [CORS/AEM 설명](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html)
>* [비디오 - AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/develop-for-cross-origin-resource-sharing.html)에서 CORS용 개발
>

특정 인증 요구 사항이 있는 환경에서는 OAuth가 권장됩니다.

## 사용 가능한 기능 {#available-features}

컨텐츠 조각은 특정 유형의 자산입니다. 다음을 참조하십시오. [컨텐츠 조각을 사용한 작업](/help/assets/content-fragments/content-fragments.md).

API를 통해 사용할 수 있는 기능에 대한 자세한 내용은 다음을 참조하십시오.

* 다음 [Assets REST API](/help/assets/mac-api-assets.md)
* [엔티티 유형](/help/assets/assets-api-content-fragments.md#entity-types)지원되는 각 유형과 관련된 기능(콘텐츠 조각과 관련)이 설명되어 있습니다

### 페이징 {#paging}

Assets REST API는 URL 매개 변수를 통해 (GET 요청에 대한) 페이징을 지원합니다.

* `offset` - 검색할 첫 번째(하위) 엔티티 수
* `limit` - 반환되는 최대 엔티티 수

응답에는 페이징 정보가 `properties` SIREN 출력의 섹션입니다. 이 `srn:paging` 속성에는 (하위) 엔티티의 총 수( `total`), 오프셋 및 제한( `offset`, `limit`)을 추가합니다.

>[!NOTE]
>
>페이징은 요청된 엔티티의 하위 항목과 관련이 있으므로 일반적으로 컨테이너 엔티티(예: 렌디션이 있는 폴더 또는 에셋)에 적용됩니다.

#### 예: 페이징 {#example-paging}

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

## 엔티티 유형 {#entity-types}

### 폴더 {#folders}

폴더는 에셋 및 기타 폴더의 컨테이너 역할을 합니다. 이는 AEM 콘텐츠 저장소의 구조를 반영합니다.

Assets REST API는 이름, 제목 등과 같은 폴더의 속성에 대한 액세스를 노출합니다. 에셋은 폴더 및 하위 폴더의 하위 엔티티로 표시됩니다.

>[!NOTE]
>
>하위 에셋 및 폴더의 에셋 유형에 따라 하위 엔티티 목록에는 각 하위 엔티티를 정의하는 전체 속성 세트가 이미 포함되어 있을 수 있습니다. 대안적으로, 이러한 자식 엔티티들의 목록에 있는 엔티티에 대해 감소된 속성 세트만이 노출될 수 있다.

### 자산 {#assets}

에셋이 요청되면 응답은 해당 에셋 스키마에서 정의한 제목, 이름 및 기타 정보와 같은 메타데이터를 반환합니다.

에셋의 이진 데이터는 유형의 SIREN 링크로 노출됩니다 `content`.

자산은 여러 변환을 가질 수 있습니다. 이러한 렌디션은 일반적으로 하위 엔티티로 노출되는데, 한 가지 예외는 썸네일 렌디션이며 유형의 링크로 노출됩니다 `thumbnail` ( `rel="thumbnail"`).

### 콘텐츠 조각 {#content-fragments}

A [컨텐츠 조각](/help/assets/content-fragments/content-fragments.md) 는 특별한 유형의 자산입니다. 텍스트, 숫자, 날짜 등 구조화된 데이터에 액세스하는 데 사용할 수 있습니다.

다음과 같은 몇 가지 차이점이 있습니다. *표준* 에셋(예: 이미지 또는 오디오), 일부 추가 규칙이 에셋 처리에 적용됩니다.

#### 표시 {#representation}

컨텐츠 조각:

* 이진 데이터를 노출하지 마십시오.
* JSON 출력에 완전히 포함됨( `properties` 속성)을 참조하십시오.

* 또한 원자로도 간주됩니다. 즉, 요소 및 변형은 조각 속성의 일부로 노출되고 링크 또는 하위 엔티티로 노출됩니다. 이를 통해 조각의 페이로드에 효율적으로 액세스할 수 있습니다.

#### 콘텐츠 모델 및 콘텐츠 조각 {#content-models-and-content-fragments}

현재 콘텐츠 조각의 구조를 정의하는 모델은 HTTP API를 통해 노출되지 않습니다. 따라서 *소비자* 조각 모델에 대해 알아야 함(최소 이상) - 페이로드에서 대부분의 정보를 데이터 유형 등으로 유추할 수 있음 정의의 일부입니다.

새 콘텐츠 조각을 만들려면 모델의 (내부 저장소) 경로를 제공해야 합니다.

#### 관련 콘텐츠 {#associated-content}

연결된 콘텐츠는 현재 노출되지 않습니다.

## 사용 {#using}

사용량은 특정 사용 사례와 함께 AEM 작성자 또는 게시 환경 사용 여부에 따라 다를 수 있습니다.

* 작성자 인스턴스에 바인딩하는 것이 좋습니다([현재 이 API를 사용하여 게시할 조각을 복제하는 방법은 없습니다](/help/assets/assets-api-content-fragments.md#limitations)).
* AEM은 JSON 형식으로만 요청된 콘텐츠를 제공하므로 모두에서 게재할 수 있습니다.

   * AEM 작성자 인스턴스 저장 및 게재는 방화벽 뒤 미디어 라이브러리 애플리케이션에 충분할 수 있습니다.

   * 라이브 웹 게재의 경우 AEM 게시 인스턴스가 권장됩니다.

>[!CAUTION]
>
>AEM 인스턴스의 Dispatcher 구성이 다음에 대한 액세스를 차단할 수 있습니다. `/api`.

>[!NOTE]
>
>자세한 내용은 [API 참조](/help/assets/assets-api-content-fragments.md#api-reference). 특히, [Adobe Experience Manager Assets API - 콘텐츠 조각](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/assets-api-content-fragments/index.html).

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

## 제한 사항 {#limitations}

몇 가지 제한 사항이 있습니다.

* **컨텐츠 조각 모델은 현재 지원되지 않습니다**: 읽거나 만들 수 없습니다. 새 콘텐츠 조각을 만들거나 기존 콘텐츠 조각을 업데이트하려면 개발자가 콘텐츠 조각 모델에 대한 올바른 경로를 알고 있어야 합니다. 현재 이러한 기능에 대한 개요를 얻는 유일한 방법은 관리 UI를 사용하는 것입니다.
* **참조는 무시됩니다.**. 현재 기존 콘텐츠 조각이 참조되는지 여부에 대한 검사가 없습니다. 따라서 예를 들어 콘텐츠 조각을 삭제하면 삭제된 콘텐츠 조각에 대한 참조가 포함된 페이지에 문제가 발생할 수 있습니다.
* **JSON 데이터 유형** 의 REST API 출력 *JSON 데이터 유형* 현재 *문자열 기반 출력*.

## 상태 코드 및 오류 메시지 {#status-codes-and-error-messages}

관련 상황에서 다음 상태 코드를 볼 수 있습니다.

* **20** (OK) 다음과 같은 경우에 반환됨:

   * 다음을 통해 콘텐츠 조각 요청 `GET`
   * 다음을 통해 콘텐츠 조각 업데이트 성공 `PUT`

* **201** (생성됨) 다음과 같은 경우에 반환됨:

   * 을(를) 통해 콘텐츠 조각을 성공적으로 만들기 `POST`

* **404** (찾을 수 없음) 다음 경우에 반환됨:

   * 요청한 콘텐츠 조각이 존재하지 않습니다.

* **500** (내부 서버 오류)

  >[!NOTE]
  >
  >이 오류가 반환됩니다.
  >
  >* 특정 코드로 식별할 수 없는 오류가 발생한 경우
  >* 지정된 페이로드가 유효하지 않은 경우

  다음은 생성된 오류 메시지(단공간)와 함께 이 오류 상태가 반환될 때의 일반적인 시나리오를 나열합니다.

   * 상위 폴더가 없습니다(을 통해 콘텐츠 조각을 만들 때). `POST`)
   * 제공된 콘텐츠 조각 모델이 없거나(cq:model이 누락됨), 잘못된 경로 또는 권한 문제로 인해 읽을 수 없거나, 유효한 조각 모델이 없습니다.

      * `No content fragment model specified`
      * `Cannot create a resource of given model '/foo/bar/qux'`

   * 콘텐츠 조각을 만들 수 없습니다(권한 문제일 수 있음).

      * `Could not create content fragment`

   * 제목 및/또는 설명을 업데이트할 수 없습니다.

      * `Could not set value on content fragment`

   * 메타데이터를 설정할 수 없음:

      * `Could not set metadata on content fragment`

   * 콘텐츠 요소를 찾을 수 없거나 업데이트할 수 없습니다.

      * `Could not update content element`
      * `Could not update fragment data of element`

  자세한 오류 메시지는 일반적으로 다음과 같은 방식으로 반환됩니다.

  ```xml
  {
    "class": "core/response",
    "properties": {
      "path": "/api/assets/foo/bar/qux",
      "location": "/api/assets/foo/bar/qux.json",
      "parentLocation": "/api/assets/foo/bar.json",
      "status.code": 500,
      "status.message": "...{error message}.."
    }
  }
  ```

## API 참조 {#api-reference}

자세한 API 참조는 여기를 참조하십시오.

* [Adobe Experience Manager Assets API - 콘텐츠 조각](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/assets-api-content-fragments/index.html)
* [Assets HTTP API](/help/assets/mac-api-assets.md)

   * [사용 가능한 기능](/help/assets/mac-api-assets.md#assets)

## 추가 리소스 {#additional-resources}

자세한 내용은 다음을 참조하십시오.

* [Assets HTTP API 설명서](/help/assets/mac-api-assets.md)
* [AEM Gem 세션: OAuth](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-oauth-server-functionality-in-aem.html)
