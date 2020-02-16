---
title: AEM Assets HTTP API의 컨텐츠 조각 지원
seo-title: AEM Assets HTTP API의 컨텐츠 조각 지원
description: AEM Assets HTTP API의 콘텐츠 조각 지원에 대해 알아봅니다.
seo-description: AEM Assets HTTP API의 콘텐츠 조각 지원에 대해 알아봅니다.
uuid: c500d71e-ceee-493a-9e4d-7016745c544c
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
topic-tags: extending-assets
discoiquuid: 03502b41-b448-47ab-9729-e0a66a3389fa
docset: aem65
translation-type: tm+mt
source-git-commit: eb36f8fe6b08e03eb25e96ed1c31957f7d5aff27

---


# AEM Assets HTTP API의 컨텐츠 조각 지원{#content-fragments-support-in-aem-assets-http-api}

## 개요 {#overview}

>[!NOTE]
>
>자산 [HTTP API에는](/help/assets/mac-api-assets.md) 다음 항목이 포함됩니다.
>
>* 자산 REST API
>* 컨텐츠 조각 지원 포함
>
>
AEM Assets HTTP API의 현재 구현은 REST입니다.

AEM(Adobe Experience Manager) [자산 REST](/help/assets/mac-api-assets.md) API를 통해 개발자는 CRUD 작업(만들기, 읽기, 업데이트, 삭제)을 통해 HTTP API를 통해 직접 컨텐츠(AEM에 저장됨)에 액세스할 수 있습니다.

API를 사용하면 JavaScript 프런트 엔드 애플리케이션에 컨텐츠 서비스를 제공하여 헤드리스 CMS(콘텐츠 관리 시스템)로 AEM을 운영할 수 있습니다. 또는 HTTP 요청을 실행하고 JSON 응답을 처리할 수 있는 기타 모든 애플리케이션

예를 들어, 단일 페이지 애플리케이션(SPA), 프레임워크 기반 또는 사용자 정의 등은 HTTP API를 통해 제공된 컨텐츠를 주로 JSON 형식으로 요구합니다.

AEM 코어 구성 요소는 이러한 목적으로 필요한 읽기 작업을 제공할 수 있고 JSON 출력을 사용자 정의할 수 있는 매우 포괄적이고 유연한 사용자 정의 가능한 API를 제공하지만 전용 AEM 템플릿을 기반으로 하는 (API) 페이지에서 호스팅되어야 하는 AEM WCM(웹 컨텐츠 관리) 노하우가 필요합니다. 모든 SPA 개발 조직이 이러한 리소스를 이용할 수 있는 것은 아닙니다.

이것은 자산 REST API를 사용할 수 있는 때입니다. 이를 통해 개발자는 에셋(예: 이미지 및 컨텐츠 조각)을 페이지에 먼저 임베드할 필요 없이 직접 액세스할 수 있으며, 이를 직렬화된 JSON 포맷으로 제공할 수 있습니다. (자산 REST API에서 JSON 출력을 사용자 지정할 수 없습니다.) 또한 Assets REST API를 사용하면 개발자는 기존 자산, 컨텐츠 조각 및 폴더를 새로 만들거나 업데이트하거나 삭제하여 컨텐츠를 수정할 수 있습니다.

자산 REST API:

* hateoas [원칙을 따르다](https://en.wikipedia.org/wiki/HATEOAS)

* 사이렌 [형식 구현](https://github.com/kevinswiber/siren)

## 전제 조건 {#prerequisites}

Assets REST API는 최신 AEM 버전의 각 즉시 설치할 수 있습니다.

## 주요 개념 {#key-concepts}

자산 REST API는 [AEM](https://en.wikipedia.org/wiki/Representational_state_transfer)인스턴스 내에 저장된 자산에 대한 REST 스타일 액세스를 제공합니다. 종단점을 사용하고 `/api/assets` 이에 액세스하려면 자산의 경로가 필요합니다(행간 `/content/dam`없음).

HTTP 메서드는 실행할 작업을 결정합니다.

* **GET** - 자산 또는 폴더의 JSON 표현 가져오기
* **POST** - 새 자산 또는 폴더를 만들려면
* **PUT** - 자산 또는 폴더의 속성을 업데이트하려면
* **삭제** - 자산 또는 폴더 삭제

>[!NOTE]
>
>요청 본문 및/또는 URL 매개 변수를 사용하여 이러한 작업 중 일부를 구성할 수 있습니다.예를 들어 폴더 또는 자산을 POST 요청에 의해 만들어야 함을 **정의합니다** .

지원되는 요청의 정확한 형식은 API 참조 [설명서에](/help/assets/assets-api-content-fragments.md#api-reference) 정의되어 있습니다.

### 트랜잭션 동작 {#transactional-behavior}

모든 요청은 원자입니다.

즉, 후속(`write`) 요청은 단일 엔티티로 성공하거나 실패할 수 있는 단일 트랜잭션으로 결합할 수 없습니다.

### AEM(자산) REST API와 AEM 구성 요소 {#aem-assets-rest-api-versus-aem-components}

<table>
 <tbody>
  <tr>
   <td>종횡비</td>
   <td>자산 REST API<br /> </td>
   <td>AEM 구성 요소<br /> (슬링 모델을 사용하는 구성 요소)</td>
  </tr>
  <tr>
   <td>지원되는 사용 사례</td>
   <td>일반적인 목적</td>
   <td><p>단일 페이지 애플리케이션(SPA) 또는 기타(컨텐츠 소비) 컨텍스트에서 사용하도록 최적화되었습니다.</p> <p>레이아웃 정보를 포함할 수도 있습니다.</p> </td>
  </tr>
  <tr>
   <td>지원되는 작업</td>
   <td><p>만들기, 읽기, 업데이트, 삭제</p> <p>엔티티 유형에 따라 추가 작업이 제공됩니다.</p> </td>
   <td>읽기 전용.</td>
  </tr>
  <tr>
   <td>액세스</td>
   <td><p>직접 액세스할 수 있습니다.</p> <p>저장소에 매핑되는 <code>/api/assets </code>끝점을 <code>/content/dam</code> 사용합니다.</p> <p><code class="code">
       /content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten</code><br /> 예를 들어 다음 항목에 액세스합니다.요청:<br /> <code>/api/assets/we-retail/en/experiences/arctic-surfing-in-lofoten.model.json</code></p> </td>
   <td><p>AEM 페이지의 AEM 구성 요소를 통해 참조되어야 합니다.</p> <p>선택기를 <code>.model</code> 사용하여 JSON 표현을 만듭니다.</p> <p>예제 URL은 다음과 같습니다.<br /> <code>https://localhost:4502/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.model.json</code></p> </td>
  </tr>
  <tr>
   <td>보안</td>
   <td><p>다양한 옵션이 가능합니다.</p> <p>OA 파섹표준 설정과 별도로 구성할 수 있습니다.</p> </td>
   <td>AEM의 표준 설정을 사용합니다.</td>
  </tr>
  <tr>
   <td>건축주의</td>
   <td><p>쓰기 액세스는 일반적으로 작성자 인스턴스를 처리합니다.</p> <p>또한 읽기가 게시 인스턴스로 연결될 수 있습니다.</p> </td>
   <td>이 방법은 읽기 전용이므로 일반적으로 게시 인스턴스에 사용됩니다.</td>
  </tr>
  <tr>
   <td>출력</td>
   <td>JSON 기반 SIRN 출력:장황하지만 강력한 기능 컨텐츠 내에서 탐색할 수 있습니다.</td>
   <td>JSON 기반의 독점 출력;Sling Models를 통해 구성 가능합니다. 콘텐츠 구조를 탐색하는 것은 구현(반드시 불가능한 것은 아님)하기가 어렵습니다.</td>
  </tr>
 </tbody>
</table>

### 보안 {#security}

특정 인증 요구 사항 없이 환경 내에서 자산 REST API를 사용하는 경우 AEM의 CORS 필터를 올바르게 구성해야 합니다.

>[!NOTE]
>
>자세한 내용은 다음을 참조하십시오.
>
>* [CORS/AEM 설명](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
>* [비디오 - AEM을 사용한 CORS용 개발](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)
>



특정 인증 요구 사항이 있는 환경에서는 OAuth를 사용하는 것이 좋습니다.

## 사용 가능한 기능 {#available-features}

컨텐츠 조각은 특정 유형의 자산입니다. 컨텐츠 조각 [작업을 참조하십시오](/help/assets/content-fragments.md).

API 파섹

* [자산 REST](/help/assets/mac-api-assets.md#available-features) API의 사용 가능한 기능
* [엔티티 유형](/help/assets/assets-api-content-fragments.md#entity-types)

### 페이징 {#paging}

자산 REST API는 URL 매개 변수를 통한 페이징(GET 요청의 경우)을 지원합니다.

* `offset` - 검색할 첫 번째(하위) 엔티티의 수
* `limit` - 반환된 최대 개체 수

응답에는 SEARN 출력 `properties` 섹션의 일부로서 페이징 정보가 포함됩니다. 이 `srn:paging` 속성에는 요청에 지정된 총 (자식) 개체 수( `total`), 오프셋 및 제한( `offset`, `limit`)이 포함됩니다.

>[!NOTE]
>
>페이징은 요청된 엔티티의 자식과 관련이 있으므로 일반적으로 컨테이너 엔티티(즉, 폴더 또는 표현물이 있는 자산)에 적용됩니다.

#### 예:페이징 {#example-paging}

`GET /api/assets.json?offset=2&limit=3`

```
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

폴더는 자산 및 기타 폴더의 컨테이너 역할을 합니다. AEM 컨텐츠 저장소의 구조를 반영합니다.

Assets REST API는 폴더의 속성에 대한 액세스를 노출합니다.예를 들어 이름, 제목 등이 있습니다. 자산은 폴더의 하위 엔티티로 표시됩니다.

>[!NOTE]
>
>자산 유형에 따라 하위 엔티티 목록에 해당 하위 엔티티를 정의하는 전체 속성 세트가 이미 포함되어 있을 수 있습니다. 또는 이 자식 엔티티 목록의 엔티티에 대해 축소된 속성 집합만 노출될 수 있습니다.

### 자산 {#assets}

자산이 요청되면 응답에서 해당 메타데이터를 반환합니다.제목, 이름 및 해당 자산 스키마에서 정의된 기타 정보 등.

자산의 이진 데이터는 유형( `content` 라고도 함)의 SIRN 링크로 노출됩니다 `rel attribute`.

자산에 여러 표현물이 있을 수 있습니다. 이러한 항목은 일반적으로 하위 엔티티로 노출되며, 한 가지 예외는 축소판 변환이며 `thumbnail` ( `rel="thumbnail"`) 유형의 링크로 표시됩니다.

### 컨텐츠 조각 {#content-fragments}

컨텐츠 [조각은](/help/assets/content-fragments.md) 특별한 유형의 자산입니다. 텍스트, 숫자, 날짜 등 구조화된 데이터에 액세스하는 데 사용할 수 있습니다.

이미지 또는 오디오와 같은 *표준* 에셋에 몇 가지 차이점이 있기 때문에 처리를 위해 몇 가지 추가 규칙이 적용됩니다.

#### 표현 {#representation}

컨텐츠 조각:

* 이진 데이터를 노출하지 마십시오.
* JSON 출력( `properties` 속성 내)에 완전히 포함되어 있습니다.

* 요소, 즉 요소 및 변형을 조각 속성의 일부로, 링크 또는 하위 엔티티로 노출됩니다. 이렇게 하면 조각의 페이로드에 효율적으로 액세스할 수 있습니다.

#### 컨텐츠 모델 및 컨텐츠 조각 {#content-models-and-content-fragments}

현재 컨텐츠 조각 구조를 정의하는 모델은 HTTP API를 통해 노출되지 않습니다. 따라서 *소비자는* 페이로드에서 대부분의 정보를 유추할 수 있지만 적어도 조각 모델에 대해 알아야 합니다.데이터 유형 등에 는 정의의 일부입니다.

새 컨텐츠 조각을 만들려면(내부 저장소) 경로를 제공해야 합니다.

#### 관련 컨텐츠 {#associated-content}

연결된 콘텐츠는 현재 노출되지 않습니다.

## 사용 {#using}

사용 방법은 특정 사용 사례와 함께 AEM 작성자 또는 게시 환경을 사용하는지에 따라 다를 수 있습니다.

* 작성은 작성자 인스턴스에 엄격하게 바인딩되며[현재 이 API를 사용하여 게시할 조각을 복제할 방법이 없습니다](/help/assets/assets-api-content-fragments.md#limitations).
* AEM은 요청된 컨텐츠를 JSON 형식으로만 제공하므로 두 가지 방법 모두에서 제공할 수 있습니다.

   * AEM 작성자 인스턴스의 저장 및 배달은 방화벽 뒤에 있는 미디어 라이브러리 애플리케이션이면 충분합니다.
   * 라이브 웹 전달의 경우 AEM 게시 인스턴스가 권장됩니다.

>[!CAUTION]
>
>AEM 클라우드 인스턴스의 디스패처 구성이 액세스 권한을 차단할 수 `/api`있습니다.

>[!NOTE]
>
>자세한 내용은 API [참조를 참조하십시오](/help/assets/assets-api-content-fragments.md#api-reference). 특히 Adobe Experience [Manager Assets API - 콘텐츠 조각](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/assets-api-content-fragments/index.html).

### 읽기/전달 {#read-delivery}

사용 방법:

`GET /{cfParentPath}/{cfName}.json`

예:

`https://localhost:4502/api/assets/we-retail/en/experiences/arctic-surfing-in-lofoten.json`

응답은 컨텐츠 조각에서와 같이 구조화된 컨텐츠가 포함된 JSON을 직렬화합니다. 참조는 참조 URL로 제공됩니다.

두 가지 유형의 읽기 작업이 가능합니다.

* 경로별로 특정 컨텐츠 조각을 읽으면 컨텐츠 조각의 JSON 표현이 반환됩니다.
* 경로별 컨텐츠 조각 폴더 읽기:그러면 폴더 내의 모든 컨텐츠 조각에 대한 JSON 표현이 반환됩니다.

### 만들기 {#create}

사용 방법:

`POST /{cfParentPath}/{cfName}`

본문에는 컨텐츠 조각 요소에 설정되어야 하는 초기 컨텐츠를 포함하여 만들 컨텐츠 조각에 대한 JSON 표현이 포함되어야 합니다. 속성을 설정해야 하며 `cq:model` 올바른 컨텐츠 조각 모델을 가리켜야 합니다. 이렇게 하지 않으면 오류가 발생합니다. 으로 설정된 헤더를 추가해야 `Content-Type` 합니다 `application/json`.

### 업데이트 {#update}

사용 방법은

`PUT /{cfParentPath}/{cfName}`

본문에는 주어진 컨텐츠 조각에 대해 업데이트될 JSON 표현을 포함해야 합니다.

컨텐츠 조각, 단일 요소 또는 모든 요소 값 및/또는 메타데이터의 제목 또는 설명일 수 있습니다. 또한 업데이트에 유효한 `cq:model` 속성을 제공해야 합니다.

### 삭제 {#delete}

사용 방법:

`DELETE /{cfParentPath}/{cfName}`

## 제한 사항 {#limitations}

몇 가지 제한 사항이 있습니다.

* **변형은 작성하고 업데이트할 수 없습니다.** 이러한 변형을 페이로드에 추가하면(예: 업데이트) 무시됩니다. 그러나 변형은 배달( `GET`)을 통해 제공됩니다.

* **컨텐츠 조각 모델은 현재 지원되지**&#x200B;않습니다.읽거나 만들 수 없습니다. 개발자는 새 컨텐츠 조각을 만들거나 기존 컨텐츠 조각을 업데이트하려면 컨텐츠 조각 모델의 올바른 경로를 알아야 합니다. 현재 이러한 기능에 대한 개요를 얻는 유일한 방법은 관리 UI를 통한 것입니다.
* **참조는 무시됩니다**. 현재 기존 컨텐츠 조각이 참조되는지 여부를 확인하지 않습니다. 예를 들어 컨텐츠 조각을 삭제하면 참조가 포함된 페이지에 문제가 발생할 수 있습니다.

## 상태 코드 및 오류 메시지 {#status-codes-and-error-messages}

관련 상황에서 다음 상태 코드를 볼 수 있습니다.

1. 202 (확인)

   반환 시기:

   * 컨텐츠 조각 요청 `GET`

   * 을(를) `PUT`

1. 201(제작)

   반환 시기:

   * 을(를) 통해 컨텐츠 조각을 성공적으로 생성했습니다. `POST`

1. 404(찾을 수 없음)

   반환 시기:

   * 요청한 컨텐츠 조각이 없습니다.

1. 500(내부 서버 오류)

   >[!NOTE]
   >
   >이 오류가 반환됩니다.
   >
   >
   >
   >    * 특정 코드로 식별할 수 없는 오류가 발생한 경우
   >    * 지정된 페이로드가 유효하지 않은 경우


   다음은 이 오류 상태가 반환될 때의 일반적인 시나리오와 생성된 오류 메시지(모노스페이스)를 나열합니다.

   * 상위 폴더가 없습니다(다음을 통해 컨텐츠 조각을 만들 때 `POST`).
   * 컨텐츠 조각 모델이 제공되지 않음(null 값), 리소스가 Null(권한 문제일 수 있음) 또는 리소스가 올바른 조각 템플릿이 아닙니다.

      * `No content fragment model specified`
      * `Cannot create a resource of given model '/foo/bar/qux'`
      * `Cannot adapt the resource '/foo/bar/qux' to a content fragment template`
   * 컨텐츠 조각을 만들 수 없습니다(권한 문제일 수 있음).

      * `Could not create content fragment`
   * 제목 및 설명을 업데이트할 수 없습니다.

      * `Could not set value on content fragment`
   * 메타데이터를 설정할 수 없습니다.

      * `Could not set metadata on content fragment`
   * 콘텐츠 요소를 찾을 수 없거나 업데이트할 수 없습니다.

      * `Could not update content element`
      * `Could not update fragment data of element`
   자세한 오류 메시지는 일반적으로 다음과 같은 방법으로 반환됩니다.

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

## API Reference {#api-reference}

자세한 API 참조는 여기를 참조하십시오.

* [Adobe Experience Manager Assets API - 콘텐츠 조각](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/assets-api-content-fragments/index.html)
* [자산 HTTP API](/help/assets/mac-api-assets.md)

   * [사용 가능한 기능](/help/assets/mac-api-assets.md#available-features)

## 추가 리소스 {#additional-resources}

자세한 내용은 다음을 참조하십시오.

* [자산 HTTP API 설명서](/help/assets/mac-api-assets.md)
* [AEM Gem 세션:OAuth](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-oauth-server-functionality-in-aem.html)

