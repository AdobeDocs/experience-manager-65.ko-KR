---
title: AEM Assets HTTP API의 컨텐츠 조각 지원
seo-title: AEM Assets HTTP API의 컨텐츠 조각 지원
description: AEM Assets HTTP API의 컨텐츠 조각 지원에 대해 알아봅니다.
seo-description: AEM Assets HTTP API의 컨텐츠 조각 지원에 대해 알아봅니다.
uuid: c500d71e-ceee-493a-9e4d-7016745c544c
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
topic-tags: extending-assets
discoiquuid: 03502b41-b448-47ab-9729-e0a66a3389fa
docset: aem65
feature: Content Fragments
role: Business Practitioner, Administrator
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '1864'
ht-degree: 3%

---


# AEM Assets HTTP API의 컨텐츠 조각 지원{#content-fragments-support-in-aem-assets-http-api}

## 개요 {#overview}

>[!NOTE]
>
>[자산 HTTP API](/help/assets/mac-api-assets.md)은 다음을 포함합니다.
>
>* 자산 REST API
>* 컨텐츠 조각 지원 포함

>
>
AEM Assets HTTP API의 현재 구현은 REST입니다.

Adobe Experience Manager(AEM) [Assets REST API](/help/assets/mac-api-assets.md)를 사용하면 개발자는 CRUD 작업(만들기, 읽기, 업데이트, 삭제)을 통해 HTTP API를 통해 직접 컨텐츠(AEM에 저장)에 액세스할 수 있습니다.

API를 사용하면 JavaScript 프런트 엔드 애플리케이션에 컨텐츠 서비스를 제공하여 헤드리스 CMS(Content Management System)로 AEM을 운영할 수 있습니다. 또는 HTTP 요청을 실행하고 JSON 응답을 처리할 수 있는 다른 애플리케이션입니다.

예를 들어 단일 페이지 애플리케이션(SPA), 프레임워크 기반 또는 사용자 정의 등은 HTTP API를 통해 제공된 컨텐츠가 필요합니다(주로 JSON 형식).

AEM 코어 구성 요소는 이러한 목적으로 필요한 읽기 작업을 제공할 수 있고 JSON 출력을 사용자 정의할 수 있는 매우 포괄적이고 유연하며 사용자 정의 가능한 API를 제공하지만 전용 AEM 템플릿을 기반으로 하는 (API) 페이지에서 호스팅되어야 하는 JSON(Web Content Management) 구현에 대한 노하우가 필요합니다. 모든 SPA 개발 조직은 이러한 리소스에 액세스할 수 있습니다.

이것은 자산 REST API를 사용할 수 있는 때입니다. 이를 통해 개발자는 에셋(예: 이미지 및 컨텐츠 조각)을 페이지에 먼저 포함시키지 않고도 직접 액세스할 수 있으며, JSON 포맷으로 컨텐츠를 전달할 수 있습니다. (자산 REST API에서 JSON 출력을 사용자 정의할 수 없습니다.) 또한 에셋 REST API를 사용하면 개발자는 기존 에셋, 컨텐츠 조각 및 폴더를 새로 만들거나 업데이트하거나 삭제하여 컨텐츠를 수정할 수 있습니다.

자산 REST API:

* [HATEOAS 원칙](https://en.wikipedia.org/wiki/HATEOAS)을 따릅니다.

* [SHANNES 형식](https://github.com/kevinswiber/siren)을 구현합니다.

## 전제 조건 {#prerequisites}

Assets REST API는 최신 AEM 버전의 각 곧바로 설치할 수 있습니다.

## 주요 개념 {#key-concepts}

자산 REST API는 AEM 인스턴스 내에 저장된 자산에 대한 [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) 스타일 액세스를 제공합니다. `/api/assets` 끝점을 사용하고, 이 끝점에 액세스하려면 자산의 경로가 필요합니다(맨 앞의 `/content/dam` 없이).

HTTP 메서드는 실행할 작업을 결정합니다.

* **GET**  - 에셋 또는 폴더의 JSON 표현 가져오기
* **POST**  - 새 에셋 또는 폴더 만들기
* **PUT**  - 자산 또는 폴더의 속성을 업데이트하는 방법
* **DELETE**  - 자산 또는 폴더 삭제

>[!NOTE]
>
>요청 본문 및/또는 URL 매개 변수를 사용하여 이러한 작업 중 일부를 구성할 수 있습니다.예를 들어 **POST** 요청에 의해 폴더 또는 자산을 만들어야 함을 정의합니다.

지원되는 요청의 정확한 형식은 [API 참조](/help/assets/assets-api-content-fragments.md#api-reference) 설명서에 정의되어 있습니다.

### 트랜잭션 동작 {#transactional-behavior}

모든 요청은 원자입니다.

즉, 후속(`write`) 요청은 단일 엔티티로 성공하거나 실패할 수 있는 단일 트랜잭션으로 결합할 수 없습니다.

### AEM(자산) REST API와 AEM 구성 요소 {#aem-assets-rest-api-versus-aem-components}

<table>
 <tbody>
  <tr>
   <td>Aspect</td>
   <td>자산 REST API<br /> </td>
   <td>AEM 구성 요소<br />(Sling 모델을 사용하는 구성 요소)</td>
  </tr>
  <tr>
   <td>지원되는 사용 사례</td>
   <td>일반적인 목적.</td>
   <td><p>단일 페이지 애플리케이션(SPA) 또는 기타(컨텐츠 소비) 컨텍스트에서의 소비를 위해 최적화되었습니다.</p> <p>레이아웃 정보를 포함할 수도 있습니다.</p> </td>
  </tr>
  <tr>
   <td>지원되는 작업</td>
   <td><p>만들기, 읽기, 업데이트, 삭제</p> <p>엔티티 유형에 따라 추가 작업이 제공됩니다.</p> </td>
   <td>읽기 전용.</td>
  </tr>
  <tr>
   <td>액세스</td>
   <td><p>직접 액세스할 수 있습니다.</p> <p>저장소에서 <code>/content/dam</code>에 매핑된 <code>/api/assets </code>끝점을 사용합니다.</p> <p>예를 들어 액세스:<code class="code">
       /content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten</code><br /> 요청:<br /> <code>/api/assets/we-retail/en/experiences/arctic-surfing-in-lofoten.model.json</code></p> </td>
   <td><p>AEM 페이지의 AEM 구성 요소를 통해 참조되어야 합니다.</p> <p><code>.model</code> 선택기를 사용하여 JSON 표현을 만듭니다.</p> <p>예제 URL은 다음과 같습니다.<br /> <code>https://localhost:4502/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.model.json</code></p> </td>
  </tr>
  <tr>
   <td>보안</td>
   <td><p>여러 옵션이 가능합니다.</p> <p>OAuth가 제안됨;표준 설정과 별도로 구성할 수 있습니다.</p> </td>
   <td>AEM 표준 설정을 사용합니다.</td>
  </tr>
  <tr>
   <td>건축주의</td>
   <td><p>쓰기 액세스는 일반적으로 작성자 인스턴스의 주소를 지정합니다.</p> <p>또한 읽기가 게시 인스턴스로 연결될 수도 있습니다.</p> </td>
   <td>이 방법은 읽기 전용이므로 일반적으로 게시 인스턴스에 사용됩니다.</td>
  </tr>
  <tr>
   <td>출력</td>
   <td>JSON 기반 사이렌 출력:자세한 정보를 제공하고 강력합니다. 컨텐츠 내에서 탐색할 수 있습니다.</td>
   <td>JSON 기반의 독점 출력;Sling 모델을 통해 구성할 수 있습니다. 컨텐츠 구조를 탐색하는 것은 구현하기가 어렵지만 꼭 불가능한 것은 아닙니다.</td>
  </tr>
 </tbody>
</table>

### 보안 {#security}

특정 인증 요구 사항이 없는 환경에서 자산 REST API를 사용하는 경우 AEM CORS 필터를 올바르게 구성해야 합니다.

>[!NOTE]
>
>자세한 내용은 다음을 참조하십시오.
>
>* [CORS/AEM 설명](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
>* [비디오 - AEM을 사용한 CORS 개발](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)

>



특정 인증 요구 사항이 있는 환경에서는 OAuth가 권장됩니다.

## 사용 가능한 기능 {#available-features}

컨텐츠 조각은 특정 유형의 자산입니다. [컨텐츠 조각 작업](/help/assets/content-fragments/content-fragments.md)을 참조하십시오.

API를 통해 사용할 수 있는 기능에 대한 자세한 내용은 다음을 참조하십시오.

* [자산 ](/help/assets/mac-api-assets.md#assets) REST API의 사용 가능한 기능
* [엔티티 유형](/help/assets/assets-api-content-fragments.md#entity-types)

### {#paging} 호출

자산 REST API는 URL 매개 변수를 통해 페이지(GET 요청에 대해)를 지원합니다.

* `offset` - 검색할 첫 번째(자식) 엔티티의 수
* `limit` - 반환된 최대 개체 수

응답에는 SANNES 출력에서 `properties` 섹션의 일부로서 페이징 정보가 포함됩니다. 이 `srn:paging` 속성에는 요청에 지정된 총 개체 수( `total`), 오프셋 및 한도( `offset`, `limit`)가 포함됩니다.

>[!NOTE]
>
>페이징은 요청된 엔티티의 자식과 관련된 컨테이너 엔티티(즉, 표현물과 함께 폴더 또는 자산)에 일반적으로 적용됩니다.

#### 예:{#example-paging} 호출

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

폴더는 자산 및 기타 폴더에 대한 컨테이너 역할을 합니다. AEM 컨텐츠 저장소의 구조를 반영합니다.

자산 REST API는 폴더의 속성에 대한 액세스 권한을 표시합니다.예를 들어 이름, 제목 등이 있습니다. 자산은 폴더 하위 엔티티로 표시됩니다.

>[!NOTE]
>
>자산 유형에 따라 자식 엔티티 목록에 해당 자식 엔티티를 정의하는 전체 속성 세트가 이미 포함되어 있을 수 있습니다. 또는 이 자식 엔티티 목록의 엔티티에 대해 축소된 속성 세트만 노출될 수 있습니다.

### 에셋 {#assets}

자산이 요청되면 응답에서 해당 메타데이터를 반환합니다.제목, 이름 및 해당 자산 스키마에 의해 정의된 기타 정보 등.

자산의 이진 데이터는 `content` 유형의 SANNES 링크로 노출됩니다(`rel attribute` 라고도 함).

자산에 여러 표현물이 있을 수 있습니다. 이러한 항목은 일반적으로 하위 엔티티로 노출되며, 한 가지 예외는 축소판 변환이며 이 변환은 `thumbnail` 유형의 링크로 표시됩니다( `rel="thumbnail"`).

### 콘텐츠 조각 {#content-fragments}

[컨텐츠 조각](/help/assets/content-fragments/content-fragments.md)은 특수한 유형의 자산입니다. 텍스트, 숫자, 날짜 등 구조화된 데이터에 액세스하는 데 사용할 수 있습니다.

*standard* 자산(예: 이미지 또는 오디오)에 차이가 여러 개 있으므로 처리 시 일부 추가 규칙이 적용됩니다.

#### 표현 {#representation}

컨텐츠 조각:

* 이진 데이터를 노출하지 마십시오.
* JSON 출력(`properties` 속성 내)에 완전히 포함됩니다.

* 요소 및 변형을 원자성으로 간주합니다. 즉, 요소 및 변형을 링크 또는 하위 엔티티보다 조각 속성의 일부로 노출됩니다. 이렇게 하면 조각의 페이로드에 대한 효율적인 액세스를 할 수 있습니다.

#### 컨텐트 모델 및 컨텐츠 조각 {#content-models-and-content-fragments}

현재 컨텐츠 조각 구조를 정의하는 모델은 HTTP API를 통해 노출되지 않습니다. 따라서 대부분의 정보를 페이로드에서 유추할 수 있지만, *consumer*&#x200B;는 조각 모델에 대해 알아야 합니다(최소 최소).데이터 유형 등에 는 정의의 일부입니다.

새 컨텐츠 조각을 만들려면(내부 저장소) 경로를 제공해야 합니다.

#### 관련 컨텐츠 {#associated-content}

연관된 컨텐츠는 현재 노출되지 않습니다.

## 사용 {#using}

AEM 작성자 환경을 사용하는지 게시 환경을 사용하는지에 따라 특정 사용 사례와 함께 사용법이 다를 수 있습니다.

* 만들기는 작성자 인스턴스([에 엄격하게 구속되며 현재 이 API](/help/assets/assets-api-content-fragments.md#limitations)를 사용하여 게시할 조각을 복제할 방법이 없습니다.
* AEM은 요청된 컨텐츠를 JSON 형식으로만 제공하므로 두 가지 방식 모두에서 전달할 수 있습니다.

   * AEM 작성 인스턴스에서 저장 및 전달하면 방화벽 뒤의 미디어 라이브러리 애플리케이션에 충분해야 합니다.
   * 라이브 웹 전달의 경우 AEM 게시 인스턴스가 권장됩니다.

>[!CAUTION]
>
>AEM 클라우드 인스턴스의 디스패처 구성은 `/api`에 대한 액세스를 차단할 수 있습니다.

>[!NOTE]
>
>자세한 내용은 [API 참조](/help/assets/assets-api-content-fragments.md#api-reference)를 참조하십시오. 특히 [Adobe Experience Manager Assets API - 콘텐츠 조각](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/assets-api-content-fragments/index.html).

### 읽기/배달 {#read-delivery}

사용 방법:

`GET /{cfParentPath}/{cfName}.json`

예:

`https://localhost:4502/api/assets/we-retail/en/experiences/arctic-surfing-in-lofoten.json`

응답은 컨텐츠 조각에서와 같이 구조화된 컨텐츠와 함께 JSON에 직렬화됩니다. 참조는 참조 URL로 제공됩니다.

두 가지 유형의 읽기 작업이 가능합니다.

* 경로별로 특정 컨텐츠 조각을 읽으면 컨텐츠 조각의 JSON 표현을 반환합니다.
* 경로별로 컨텐츠 조각 폴더 읽기:폴더 내의 모든 컨텐츠 조각에 대한 JSON 표현을 반환합니다.

### 만들기 {#create}

사용 방법:

`POST /{cfParentPath}/{cfName}`

본문에는 컨텐츠 조각 요소에 설정되어야 하는 초기 컨텐츠를 포함하여 작성할 컨텐츠 조각에 대한 JSON 표현이 포함되어야 합니다. `cq:model` 속성을 설정해야 하며 올바른 컨텐츠 조각 모델을 가리켜야 합니다. 그렇게 하지 않으면 오류가 발생합니다. 또한 `application/json`으로 설정된 헤더 `Content-Type`을 추가해야 합니다.

### 업데이트 {#update}

사용 방법은

`PUT /{cfParentPath}/{cfName}`

본문에는 주어진 컨텐츠 조각에 대해 업데이트할 JSON 표현을 포함해야 합니다.

컨텐츠 조각 또는 단일 요소 또는 모든 요소 값 및/또는 메타데이터의 제목 또는 설명일 수 있습니다. 또한 업데이트에 유효한 `cq:model` 속성을 제공해야 합니다.

### 삭제 {#delete}

사용 방법:

`DELETE /{cfParentPath}/{cfName}`

## 제한 사항 {#limitations}

몇 가지 제한 사항이 있습니다.

* **변형은 작성하고 업데이트할 수 없습니다.** 이러한 변형이 페이로드에 추가되면(예: 업데이트) 무시됩니다. 그러나 변형은 배달( `GET`)을 통해 제공됩니다.

* **컨텐츠 조각 모델은 현재 지원되지 않습니다**.읽거나 만들 수 없습니다. 새 컨텐츠를 만들거나 기존 컨텐츠 조각을 업데이트하려면 개발자는 컨텐츠 조각 모델의 올바른 경로를 알아야 합니다. 현재 이러한 UI의 개요를 얻는 유일한 방법은 관리 UI를 이용하는 것입니다.
* **참조는 무시됩니다**. 현재 기존 컨텐츠 조각이 참조되는지 여부를 확인할 수 없습니다. 예를 들어 컨텐츠 조각을 삭제하면 참조가 포함된 페이지에 문제가 발생할 수 있습니다.

## 상태 코드 및 오류 메시지 {#status-codes-and-error-messages}

관련 상황에서는 다음 상태 코드를 볼 수 있습니다.

* **200 (확인)**

   다음 경우에 반환:

   * `GET`을(를) 통해 컨텐츠 조각 요청

   * `PUT`을(를) 통해 컨텐츠 조각을 성공적으로 업데이트

* **201(작성일)**

   다음 경우에 반환:

   * `POST`을(를) 통해 컨텐츠 조각을 성공적으로 만들기

* **404(찾을 수 없음)**

   다음 경우에 반환:

   * 요청한 컨텐츠 조각이 존재하지 않습니다.

* **500(내부 서버 오류)**

   >[!NOTE]
   >
   >이 오류가 반환됩니다.
   >
   >
   >
   >    * 특정 코드로 식별할 수 없는 오류가 발생한 경우
   >    * 지정된 페이로드가 유효하지 않은 시기


   다음은 이 오류 상태가 반환되는 일반적인 시나리오와 생성된 오류 메시지(모노스페이스)를 함께 나열합니다.

   * 상위 폴더가 없습니다(`POST`을(를) 통해 컨텐츠 조각을 만들 때).
   * 컨텐츠 조각 모델이 제공되지 않음(null 값), 리소스가 null(권한 문제일 수 있음) 또는 리소스가 유효한 조각 템플릿이 아닙니다.

      * `No content fragment model specified`
      * `Cannot create a resource of given model '/foo/bar/qux'`
      * `Cannot adapt the resource '/foo/bar/qux' to a content fragment template`
   * 컨텐츠 조각을 만들 수 없습니다(권한 문제가 있을 수 있음).

      * `Could not create content fragment`
   * 제목 및 설명을 업데이트할 수 없습니다.

      * `Could not set value on content fragment`
   * 메타데이터를 설정할 수 없습니다.

      * `Could not set metadata on content fragment`
   * 콘텐츠 요소를 찾을 수 없거나 업데이트할 수 없습니다.

      * `Could not update content element`
      * `Could not update fragment data of element`

   세부 오류 메시지는 일반적으로 다음과 같은 방식으로 반환됩니다.

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
* [자산 HTTP API](/help/assets/mac-api-assets.md)

   * [사용 가능한 기능](/help/assets/mac-api-assets.md#assets)

## 추가 리소스 {#additional-resources}

자세한 내용은 다음을 참조하십시오.

* [에셋 HTTP API 설명서](/help/assets/mac-api-assets.md)
* [AEM Gem 세션:OAuth](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-oauth-server-functionality-in-aem.html)

