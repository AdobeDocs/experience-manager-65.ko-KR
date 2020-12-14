---
title: '[!DNL Assets] HTTP API.'
description: ' [!DNL Adobe Experience Manager Assets]의 HTTP API를 사용하여 디지털 에셋을 만들고, 읽고, 업데이트하고, 삭제하고, 관리할 수 있습니다.'
contentOwner: AG
translation-type: tm+mt
source-git-commit: c3ae4447581d946554d792c68d31b47a6b67d5df
workflow-type: tm+mt
source-wordcount: '1727'
ht-degree: 1%

---


# [!DNL Assets] HTTP API {#assets-http-api}

## 개요 {#overview}

[!DNL Assets] HTTP API를 사용하면 [!DNL Experience Manager] 컨텐츠 조각을 사용하여 구조화된 컨텐츠와 함께 메타데이터, 변환 및 주석을 비롯한 디지털 자산에 대해 CRUD(create-read-update-delete) 작업을 수행할 수 있습니다. 이것은 `/api/assets`에 노출되며 REST API로 구현됩니다. 여기에는 [컨텐츠 조각 지원](/help/assets/assets-api-content-fragments.md)이 포함됩니다.

API에 액세스하려면:

1. `https://[hostname]:[port]/api.json`에서 API 서비스 문서를 엽니다.
1. `https://[hostname]:[server]/api/assets.json`으로 이어지는 [!DNL Assets] 서비스 링크를 따릅니다.

API 응답은 일부 MIME 유형에 대한 JSON 파일이며 모든 MIME 유형에 대한 응답 코드입니다. JSON 응답은 선택 사항이며 PDF 파일 등의 경우 사용할 수 없습니다. 추가 분석 또는 작업을 위해 응답 코드를 사용합니다.

[!UICONTROL 해제 시간] 이후에는 [!DNL Assets] 웹 인터페이스와 HTTP API를 통해 에셋 및 해당 변환을 사용할 수 없습니다. [!UICONTROL On Time]이(가) 미래 또는 [!UICONTROL Off Time]이(가) 과거이면 API는 404 오류 메시지를 반환합니다.

>[!CAUTION]
>
>[HTTP API는 네임스페이스의 메타데이터 ](#update-asset-metadata) 속성을  `jcr` 업데이트합니다. 그러나 Experience Manager 사용자 인터페이스는 `dc` 네임스페이스의 메타데이터 속성을 업데이트합니다.

## 콘텐츠 조각 {#content-fragments}

[컨텐츠 조각](/help/assets/content-fragments/content-fragments.md)은 특수한 유형의 자산입니다. 텍스트, 숫자, 날짜 등 구조화된 데이터에 액세스하는 데 사용할 수 있습니다. `standard` 자산(예: 이미지 또는 문서)에 몇 가지 차이가 있으므로 컨텐츠 조각 처리에 일부 추가 규칙이 적용됩니다.

자세한 내용은 Experience Manager 자산 HTTP API](/help/assets/assets-api-content-fragments.md)의 [콘텐츠 조각 지원을 참조하십시오.

## 데이터 모델 {#data-model}

[!DNL Assets] HTTP API는 2개의 주요 요소, 폴더 및 자산(표준 에셋의 경우)을 표시합니다.

또한 컨텐츠 조각에서 구조화된 컨텐츠를 설명하는 사용자 지정 데이터 모델에 대한 보다 자세한 요소를 노출합니다. 자세한 내용은 [컨텐츠 조각 데이터 모델](/help/assets/assets-api-content-fragments.md#content-fragments)을 참조하십시오.

### 폴더 {#folders}

폴더는 기존 파일 시스템의 디렉토리와 같습니다. 다른 폴더 또는 어설션의 컨테이너입니다. 폴더에는 다음 구성 요소가 있습니다.

**개체**:폴더 엔티티는 폴더 및 자산일 수 있는 하위 요소입니다.

**속성**:

* `name` 은 폴더의 이름입니다. 이는 확장자가 없는 URL 경로의 마지막 세그먼트와 같습니다.
* `title` 은 이름 대신 표시할 수 있는 폴더의 선택 제목입니다.

>[!NOTE]
>
>폴더 또는 자산의 일부 속성이 다른 접두사에 매핑됩니다. `jcr:title`, `jcr:description` 및 `jcr:language`의 `jcr` 접두어가 `dc` 접두어로 바뀝니다. 따라서 반환된 JSON에서 `dc:title` 및 `dc:description`은 각각 `jcr:title` 및 `jcr:description`의 값을 포함합니다.

**링크** 폴더에는 3개의 링크가 표시됩니다.

* `self`:링크.
* `parent`:상위 폴더에 연결합니다.
* `thumbnail`:(선택 사항) 폴더 축소판 이미지에 연결합니다.

### 자산 {#assets}

Experience Manager에서 자산은 다음 요소를 포함합니다.

* 자산의 속성 및 메타데이터입니다.
* 원본 변환(원래 업로드된 에셋), 축소판 및 다양한 기타 표현물과 같은 여러 표현물. 추가 변환은 서로 다른 크기의 이미지, 다른 비디오 인코딩 또는 PDF 또는 [!DNL Adobe InDesign] 파일에서 추출된 페이지일 수 있습니다.
* 선택적 주석.

컨텐츠 조각의 요소에 대한 자세한 내용은 Experience Manager 에셋 HTTP API[의 컨텐츠 조각 지원을 참조하십시오.](/help/assets/assets-api-content-fragments.md#content-fragments)

[!DNL Experience Manager]에 폴더에 다음 구성 요소가 있습니다.

* 개체:자산의 하위는 표현물입니다.
* 속성.
* 링크.

[!DNL Assets] HTTP API에는 다음 기능이 포함되어 있습니다.

* [폴더 목록을 검색합니다](#retrieve-a-folder-listing).
* [폴더를 만듭니다](#create-a-folder).
* [자산을 만듭니다](#create-an-asset).
* [자산 이진](#update-asset-binary) 업데이트
* [자산 메타데이터를 업데이트합니다](#update-asset-metadata).
* [자산 표현물을 만듭니다](#create-an-asset-rendition).
* [자산 변환을 업데이트합니다](#update-an-asset-rendition).
* [자산 주석을 만듭니다](#create-an-asset-comment).
* [폴더 또는 자산을 복사합니다](#copy-a-folder-or-asset).
* [폴더 또는 자산을 이동합니다](#move-a-folder-or-asset).
* [폴더, 자산 또는 변환을 삭제합니다](#delete-a-folder-asset-or-rendition).

>[!NOTE]
>
>쉽게 읽을 수 있도록 다음 예제에서는 전체 cURL 표기법을 생략합니다. 사실상 표기법은 `cURL`의 스크립트 래퍼인 [Resty](https://github.com/micha/resty)과 상호 연관됩니다.

**전제 조건**

* 액세스 `https://[aem_server]:[port]/system/console/configMgr`.
* **[!UICONTROL Adobe Granite CSRF 필터]**&#x200B;로 이동합니다.
* **[!UICONTROL 필터 메서드]** 속성에 다음이 포함되는지 확인하십시오.`POST`, `PUT`, `DELETE`.

## {#retrieve-a-folder-listing} 목록이 있는 폴더 검색

기존 폴더 및 하위 엔티티(하위 폴더 또는 에셋)의 Sannes 표현을 검색합니다.

**요청**:  `GET /api/assets/myFolder.json`

**응답 코드**:응답 코드는 다음과 같습니다.

* 200 - OK - success.
* 404 - 찾을 수 없음 - 폴더가 없거나 액세스할 수 없습니다.
* 500 - 내부 서버 오류 - 다른 문제가 있는 경우

**응답**:반환된 엔티티의 클래스는 에셋 또는 폴더입니다. 포함된 엔티티의 속성은 각 엔티티의 전체 속성 세트의 하위 집합입니다. 엔티티의 전체 표현을 얻으려면 클라이언트는 `self`의 `rel`이 있는 링크를 통해 가리키는 URL의 내용을 검색해야 합니다.

## 폴더를 만듭니다 {#create-a-folder}

새 `sling`을(를) 만듭니다.지정된 경로에서 `OrderedFolder`. 노드 이름 대신 `*`이 제공되면 서블릿은 매개 변수 이름을 노드 이름으로 사용합니다. 요청 데이터는 새 폴더의 사이렌 표시 또는 `application/www-form-urlencoded` 또는 `multipart`/ `form`- `data`(으)로 인코딩된 이름-값 쌍 집합으로 수락되며 HTML 양식에서 직접 폴더를 만드는 데 유용합니다. 또한 폴더의 속성은 URL 쿼리 매개 변수로 지정할 수 있습니다.

제공된 경로의 상위 노드가 없는 경우 API 호출이 `500` 응답 코드와 함께 실패합니다. 폴더가 이미 있는 경우 호출에서 응답 코드 `409`을 반환합니다.

**매개 변수**: `name` 은 폴더 이름입니다.

**요청**

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"title=My Folder"`

**응답 코드**:응답 코드는 다음과 같습니다.

* 201 - 생성됨 - 만들기 성공 시
* 409 - CONFLICT - 폴더가 이미 있는 경우
* 412 - 사전 조건 실패 - 루트 컬렉션을 찾을 수 없거나 액세스할 수 없는 경우
* 500 - 내부 서버 오류 - 다른 문제가 있는 경우

## 자산 {#create-an-asset} 만들기

제공된 파일을 제공된 경로에 배치하여 DAM 저장소에 자산을 만듭니다. 노드 이름 대신 `*`이 제공되면 서블릿은 매개 변수 이름 또는 파일 이름을 노드 이름으로 사용합니다.

**매개 변수**:매개 변수 `name` 는 에셋 이름 및 파일 참조 `file` 에 사용됩니다.

**요청**

* `POST /api/assets/myFolder/myAsset.png -H"Content-Type: image/png" --data-binary "@myPicture.png"`
* `POST /api/assets/myFolder/* -F"name=myAsset.png" -F"file=@myPicture.png"`

**응답 코드**:응답 코드는 다음과 같습니다.

* 201 - 생성됨 - 자산이 성공적으로 생성되었다면
* 409 - 충돌 - 자산이 이미 존재하는 경우.
* 412 - 사전 조건 실패 - 루트 컬렉션을 찾을 수 없거나 액세스할 수 없는 경우
* 500 - 내부 서버 오류 - 다른 문제가 있는 경우

## 자산 이진 {#update-asset-binary} 업데이트

자산의 이진(이름 원본으로 변환)을 업데이트합니다. 업데이트가 구성된 경우 기본 자산 처리 작업 과정이 실행됩니다.

**요청**:  `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: image/png" --data-binary @myPicture.png`

**응답 코드**:응답 코드는 다음과 같습니다.

* 200 - 확인 - 자산이 성공적으로 업데이트된 경우
* 404 - 찾을 수 없음 - 제공된 URI에서 자산을 찾거나 액세스할 수 없는 경우
* 412 - 사전 조건 실패 - 루트 컬렉션을 찾을 수 없거나 액세스할 수 없는 경우
* 500 - 내부 서버 오류 - 다른 문제가 있는 경우

## 자산 메타데이터 업데이트 {#update-asset-metadata}

자산 메타데이터 속성을 업데이트합니다. `dc:` 네임스페이스에 있는 속성을 업데이트하면 API가 `jcr` 네임스페이스에 있는 동일한 속성을 업데이트합니다. API는 두 네임스페이스 아래의 속성을 동기화하지 않습니다.

**요청**:  `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"jcr:title":"My Asset"}}'`

**응답 코드**:응답 코드는 다음과 같습니다.

* 200 - 확인 - 자산이 성공적으로 업데이트된 경우
* 404 - 찾을 수 없음 - 제공된 URI에서 자산을 찾거나 액세스할 수 없는 경우
* 412 - 사전 조건 실패 - 루트 컬렉션을 찾을 수 없거나 액세스할 수 없는 경우
* 500 - 내부 서버 오류 - 다른 문제가 있는 경우

### `dc`과 `jcr` 네임스페이스 {#sync-metadata-between-namespaces} 간의 메타데이터 업데이트 동기화

API 메서드는 `jcr` 네임스페이스의 메타데이터 속성을 업데이트합니다. 사용자 인터페이스를 사용하여 수행한 업데이트는 `dc` 네임스페이스의 메타데이터 속성을 변경합니다. `dc`과 `jcr` 네임스페이스 간의 메타데이터 값을 동기화하려면 워크플로우를 만들고 자산 편집 시 워크플로우를 실행하도록 Experience Manager을 구성할 수 있습니다. ECMA 스크립트를 사용하여 필요한 메타데이터 속성을 동기화할 수 있습니다. 다음 샘플 스크립트는 `dc:title`과 `jcr:title` 사이에 제목 문자열을 동기화합니다.

```javascript
var workflowData = workItem.getWorkflowData();
if (workflowData.getPayloadType() == "JCR_PATH")
{
 var path = workflowData.getPayload().toString();
 var node = workflowSession.getSession().getItem(path);
 var metadataNode = node.getNode("jcr:content/metadata");
 var jcrcontentNode = node.getNode("jcr:content");
if (jcrcontentNode.hasProperty("jcr:title"))
{
 var jcrTitle = jcrcontentNode.getProperty("jcr:title");
 metadataNode.setProperty("dc:title", jcrTitle.toString());
 metadataNode.save();
}
}
```

## 자산 변환 만들기 {#create-an-asset-rendition}

자산에 대한 새 자산 변환을 만듭니다. 요청 매개 변수 이름을 제공하지 않으면 파일 이름이 변환 이름으로 사용됩니다.

**매개 변수**:매개 변수 `name` 는 변환의 이름과 파일 참조 `file` 로 사용됩니다.

**요청**

* `POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"`
* `POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"`

**응답 코드**:응답 코드는 다음과 같습니다.

* 201 - CREATED - 변환이 성공적으로 생성되었다면
* 404 - 찾을 수 없음 - 제공된 URI에서 자산을 찾거나 액세스할 수 없는 경우
* 412 - 사전 조건 실패 - 루트 컬렉션을 찾을 수 없거나 액세스할 수 없는 경우
* 500 - 내부 서버 오류 - 다른 문제가 있는 경우

## 자산 변환 {#update-an-asset-rendition} 업데이트

업데이트는 각각 에셋 변환을 새 이진 데이터로 대체합니다.

**요청**:  `PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png`

**응답 코드**:응답 코드는 다음과 같습니다.

* 200 - 확인 - 변환이 성공적으로 업데이트된 경우
* 404 - 찾을 수 없음 - 제공된 URI에서 자산을 찾거나 액세스할 수 없는 경우
* 412 - 사전 조건 실패 - 루트 컬렉션을 찾을 수 없거나 액세스할 수 없는 경우
* 500 - 내부 서버 오류 - 다른 문제가 있는 경우

## 자산 {#create-an-asset-comment}에 주석 추가

새 자산 주석을 만듭니다.

**매개 변수**:매개 변수 `message` 는 주석의 메시지 본문과 JSON 형식 `annotationData` 의 주석 데이터에 대한 것입니다.

**요청**:  `POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"`

**응답 코드**:응답 코드는 다음과 같습니다.

* 201 - CREATED - 댓글이 성공적으로 작성된 경우
* 404 - 찾을 수 없음 - 제공된 URI에서 자산을 찾거나 액세스할 수 없는 경우
* 412 - 사전 조건 실패 - 루트 컬렉션을 찾을 수 없거나 액세스할 수 없는 경우
* 500 - 내부 서버 오류 - 다른 문제가 있는 경우

## 폴더 또는 자산 {#copy-a-folder-or-asset} 복사

제공된 경로에서 사용할 수 있는 폴더 또는 자산을 새 대상에 복사합니다.

**요청 헤더**:매개 변수는 다음과 같습니다.

* `X-Destination` - 리소스를 복사할 API 솔루션 범위 내의 새 대상 URI입니다.
* `X-Depth` -  `infinity` 또는 `0`. `0`을(를) 사용하면 리소스와 해당 속성만 복사되며 하위 항목은 복사하지 않습니다.
* `X-Overwrite` - 기존 대상 `F` 에서 자산을 덮어쓰지 않도록 하려면 사용합니다.

**요청**:  `COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**응답 코드**:응답 코드는 다음과 같습니다.

* 201 - CREATED - 폴더/자산이 존재하지 않는 대상에 복사되는 경우
* 204 - 콘텐츠 없음 - 폴더/자산이 기존 대상에 복사되는 경우
* 412 - 전제 조건 실패 - 요청 헤더가 없는 경우
* 500 - 내부 서버 오류 - 다른 문제가 있는 경우

## 폴더 또는 자산 {#move-a-folder-or-asset} 이동

지정된 경로의 폴더 또는 자산을 새 대상으로 이동합니다.

**요청 헤더**:매개 변수는 다음과 같습니다.

* `X-Destination` - 리소스를 복사할 API 솔루션 범위 내의 새 대상 URI입니다.
* `X-Depth` -  `infinity` 또는 `0`. `0`을(를) 사용하면 리소스와 해당 속성만 복사되며 하위 항목은 복사하지 않습니다.
* `X-Overwrite` - 기존 리소스 `T` 를 강제로 삭제하거나 기존 리소스 `F` 를 덮어쓰지 않도록 하려면 다음 중 하나를 사용합니다.

**요청**:  `MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"`

URL에 `/content/dam`을 사용하지 마십시오. 에셋을 이동하고 기존 에셋을 덮어쓰는 샘플 명령은 다음과 같습니다.

```shell
curl -u admin:admin -X MOVE https://[aem_server]:[port]/api/assets/source/file.png -H "X-Destination: http://[aem_server]:[port]/api/assets/destination/file.png" -H "X-Overwrite: T"
```

**응답 코드**:응답 코드는 다음과 같습니다.

* 201 - CREATED - 폴더/자산이 존재하지 않는 대상에 복사되는 경우
* 204 - 콘텐츠 없음 - 폴더/자산이 기존 대상에 복사되는 경우
* 412 - 전제 조건 실패 - 요청 헤더가 없는 경우
* 500 - 내부 서버 오류 - 다른 문제가 있는 경우

## 폴더, 자산 또는 변환 {#delete-a-folder-asset-or-rendition} 삭제

제공된 경로에서 리소스(-트리)를 삭제합니다.

**요청**

* `DELETE /api/assets/myFolder`
* `DELETE /api/assets/myFolder/myAsset.png`
* `DELETE /api/assets/myFolder/myAsset.png/renditions/original`

**응답 코드**:응답 코드는 다음과 같습니다.

* 200 - 확인 - 폴더가 성공적으로 삭제된 경우
* 412 - 사전 조건 실패 - 루트 컬렉션을 찾을 수 없거나 액세스할 수 없는 경우
* 500 - 내부 서버 오류 - 다른 문제가 있는 경우

## 팁 및 제한 사항 {#tips-best-practices-limitations}

* [HTTP API는 네임스페이스의 메타데이터 ](#update-asset-metadata) 속성을  `jcr` 업데이트합니다. 그러나 Experience Manager 사용자 인터페이스는 `dc` 네임스페이스의 메타데이터 속성을 업데이트합니다.

* 자산 API는 전체 메타데이터를 반환하지 않습니다. API에서 네임스페이스는 하드 코딩되며, 네임스페이스만 반환됩니다. 전체 메타데이터가 필요한 경우 자산 경로 `/jcr_content/metadata.json`을 봅니다.
