---
title: 자산 HTTP API
description: Assets HTTP API의 구현, 데이터 모델 및 기능에 대해 알아봅니다. 자산 HTTP API를 사용하여 자산 관련 다양한 작업을 수행합니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: abc4821ec3720969bf1c2fb068744c07477aca46

---


# 자산 HTTP API {#assets-http-api}

## 개요 {#overview}

자산 HTTP API를 사용하면 이진, 메타데이터, 변환 및 주석을 비롯한 자산에 대해 CRUD(Create-Read-Update-delete) 작업을 AEM 컨텐츠 조각을 사용한 구조화된 컨텐츠와 함께 수행할 수 있습니다. 에 노출되어 REST API로 `/api/assets` 구현됩니다. 컨텐츠 조각에 대한 [지원이 포함되어 있습니다](/help/assets/assets-api-content-fragments.md).

API에 액세스하려면:

1. 에서 API 서비스 문서를 `https://[hostname]:[port]/api.json`엽니다.
1. 다음으로 이어지는 자산 서비스 링크를 `https://[hostname]:[server]/api/assets.json`따르십시오.

API 응답은 일부 MIME 유형에 대한 JSON 파일과 모든 MIME 유형에 대한 응답 코드입니다. JSON 응답은 선택 사항이며 PDF 파일 등의 경우 사용할 수 없습니다. 추가 분석 또는 작업을 위해 응답 코드를 사용합니다.

해제 [!UICONTROL 시간]후에는 자산 웹 인터페이스 또는 HTTP API를 통해 자산 및 표현물을 사용할 수 없습니다. 설정 시간이 미래 또는 [!UICONTROL 해제 시간이] 과거인 경우 API는 404 오류 [!UICONTROL 메시지를] 반환합니다.

## 콘텐츠 조각 {#content-fragments}

컨텐츠 [조각은](/help/assets/content-fragments.md) 특별한 유형의 자산입니다. 텍스트, 숫자, 날짜 등 구조화된 데이터에 액세스하는 데 사용할 수 있습니다. 자산(예: 이미지 또는 문서)에 몇 가지 차이가 있으므로 컨텐츠 조각 처리에 일부 추가 규칙이 적용됩니다. `standard`

자세한 내용은 AEM Assets [HTTP API의 콘텐츠 조각 지원을 참조하십시오](/help/assets/assets-api-content-fragments.md).

## Data model {#data-model}

자산 HTTP API는 두 가지 주요 요소, 폴더 및 자산을 표시합니다(표준 자산의 경우).

또한 컨텐츠 조각에서 구조화된 컨텐츠를 설명하는 사용자 지정 데이터 모델에 대한 보다 자세한 요소를 노출합니다. 자세한 [내용은 컨텐츠 조각](/help/assets/assets-api-content-fragments.md#content-fragments) 데이터 모델을 참조하십시오.

### 폴더 {#folders}

폴더는 기존 파일 시스템의 디렉토리와 같습니다. 다른 폴더 또는 어설션의 컨테이너입니다. 폴더에는 다음 구성 요소가 있습니다.

**개체**:폴더의 엔티티는 폴더 및 자산일 수 있는 하위 요소입니다.

**속성**:
* `name`  — 폴더 이름입니다. URL 경로에서 확장자가 없는 마지막 세그먼트와 같습니다.
* `title` — 이름 대신 표시할 수 있는 폴더의 선택 사항 제목

>[!NOTE]
>
>폴더 또는 자산의 일부 속성이 다른 접두사로 매핑됩니다. 접두어 `jcr` , `jcr:title`및 `jcr:description`접두사가 `jcr:language` `dc` 접두사로 바뀝니다. 따라서 반환된 JSON에 `dc:title` 각각 및 `dc:description` 의 값을 `jcr:title` `jcr:description`포함시킵니다.

**링크** 폴더에는 다음 세 개의 링크가 표시됩니다.
* `self`:자체에 대한 링크
* `parent`:상위 폴더에 대한 링크
* `thumbnail`:(선택 사항) 폴더 축소판 이미지에 대한 링크

### 자산 {#assets}

AEM에서 자산은 다음 요소를 포함합니다.

* 자산의 속성 및 메타데이터
* 원본 변환(원래 업로드된 에셋), 축소판 및 다양한 기타 표현물과 같은 여러 변환 추가 변환은 다양한 크기의 이미지, 서로 다른 비디오 인코딩 또는 PDF 또는 InDesign에서 추출한 페이지일 수 있습니다.
* 선택적 주석

컨텐츠 조각의 요소에 대한 자세한 내용은 AEM Assets HTTP [API의 컨텐츠 조각 지원을 참조하십시오](/help/assets/assets-api-content-fragments.md#content-fragments).

AEM에서 폴더에는 다음 구성 요소가 있습니다.

* 개체:자산의 하위는 표현물입니다.
* 속성
* 링크

자산 HTTP API에는 다음 기능이 포함되어 있습니다.

* 폴더 목록 검색
* 폴더를 만듭니다
* 자산 만들기
* 자산 이진 업데이트
* 자산 메타데이터 업데이트
* 자산 변환 만들기
* 자산 변환 업데이트
* 자산 주석 만들기
* 폴더 또는 자산 복사
* 폴더 또는 자산 이동
* 폴더, 자산 또는 변환 삭제

>[!NOTE]
>
>쉽게 읽을 수 있도록 다음 예제에서는 전체 cURL 표기법을 생략합니다. 실제로 표기법은 스크립트 래퍼인 [Resty](https://github.com/micha/resty) 와 연관됩니다 `cURL`.

**전제 조건**

* 이동 `https://[aem_server]:[port]/system/console/configMgr`.
* Adobe Granite **CSRF 필터로 이동합니다**.
* 속성 필터 **메서드에 다음이 포함되어 있는지 확인합니다** .게시물, 배치, 삭제

## 폴더 목록 검색 {#retrieve-a-folder-listing}

기존 폴더 및 해당 하위 엔티티(하위 폴더 또는 자산)의 Sanner 표현을 검색합니다.

**요청**

```
GET /api/assets/myFolder.json
```

**응답 코드**

```
200 - OK - success
404 - NOT FOUND - folder does not exist or is not accessible
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

**응답**

반환된 엔티티의 클래스는 assets/folder입니다.

포함된 엔티티의 속성은 각 엔티티의 전체 속성 세트의 하위 집합입니다. 엔티티의 전체 표현을 얻으려면 클라이언트가 의 링크가 가리키는 URL의 컨텐츠를 검색해야 `rel` 합니다 `self`.

## Create a Folder {#create-a-folder}

새로 `sling`만듭니다.지정된 `OrderedFolder` 경로에서 노드 이름 대신 *가 주어지면 서블릿은 매개변수 이름을 노드 이름으로 사용합니다. 요청 데이터는 새 폴더의 사이렌 표시 또는 HTML 양식에서 직접 폴더를 만드는 데 유용한 이름-값 쌍 집합입니다. `application/www-form-urlencoded` 또는 `multipart`/ `form``data`로 인코딩되어 있습니다. 또한 폴더의 속성을 URL 쿼리 매개 변수로 지정할 수 있습니다.

지정된 경로의 상위 노드가 없는 경우 `500` 응답 코드가 있으면 작업이 실패합니다. 폴더가 이미 있으면 `409` 응답 코드가 반환됩니다.

**매개 변수**

* `name` - 폴더 이름

**요청**

```
POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"title":"My Folder"}}'
```

또는

```
POST /api/assets/* -F"name=myfolder" -F"title=My Folder"
```

**응답 코드**

```
201 - CREATED - on successful creation
409 - CONFLICT - if folder already exist
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## 자산 만들기 {#create-an-asset}

지정된 파일과 함께 지정된 경로에서 DAM 자산을 만듭니다. 노드 이름 대신 *가 주어지면 서블릿은 매개변수 이름 또는 파일 이름을 노드 이름으로 사용합니다.

**매개 변수**

* `name` - 자산 이름
* `file` - 파일 참조

**요청**

```
POST /api/assets/myFolder/myAsset.png -H"Content-Type: image/png" --data-binary "@myPicture.png"
```

또는

```
POST /api/assets/myFolder/* -F"name=myAsset.png" -F"file=@myPicture.png"
```

**응답 코드**

```
201 - CREATED - if Asset has been created successfully
409 - CONFLICT - if Asset already exist
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## 자산 이진 업데이트 {#update-asset-binary}

자산 이진(원본 이름으로 변환)을 업데이트합니다. 구성된 경우 기본 자산 워크플로우가 트리거됩니다.

**요청**

```
PUT /api/assets/myfolder/myAsset.png -H"Content-Type: image/png" --data-binary @myPicture.png
```

**응답 코드**

```
200 - OK - if Asset has been updated successfully
404 - NOT FOUND - if Asset could not be found or accessed at the provided URI
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## 자산 메타데이터 업데이트 {#update-asset-metadata}

자산 메타데이터 속성을 업데이트합니다. 네임스페이스의 속성을 업데이트하면 API가 `dc:` `jcr` 네임스페이스의 동일한 속성을 업데이트합니다. API 파섹

**요청**

```
PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"dc:title":"My Asset"}}'
```

**응답 코드**

```
200 - OK - if Asset has been updated successfully
404 - NOT FOUND - if Asset could not be found or accessed at the provided URI
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## 자산 변환 만들기 {#create-an-asset-rendition}

자산에 대한 새 자산 변환을 만듭니다. 요청 매개 변수 이름을 제공하지 않으면 파일 이름이 변환 이름으로 사용됩니다.

**매개 변수**

* `name` - 변환 이름
* `file` - 파일 참조

**요청**

```
POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"
```

또는

```
POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"
```

**응답 코드**

```
201 - CREATED - if Rendition has been created successfully
404 - NOT FOUND - if Asset could not be found or accessed at the provided URI
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## 자산 변환 업데이트 {#update-an-asset-rendition}

업데이트는 자산 변환을 새 이진 데이터로 대체합니다.

**요청**

```
PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png
```

**응답 코드**

```
200 - OK - if Rendition has been updated successfully
404 - NOT FOUND - if Asset could not be found or accessed at the provided URI
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## 자산 주석 만들기 {#create-an-asset-comment}

새 자산 주석을 만듭니다.

**매개 변수**

* `message` - 메시지
* `annotationData` - 주석 데이터(JSON)

**요청**

```
POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"
```

**응답 코드**

```
201 - CREATED - if Comment has been created successfully
404 - NOT FOUND - if Asset could not be found or accessed at the provided URI
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## 폴더 또는 자산 복사 {#copy-a-folder-or-asset}

지정된 경로에 있는 폴더 또는 자산을 새 대상에 복사합니다.

**요청 헤더**

```
X-Destination - a new destination URI within the API solution scope to copy the resource to
X-Depth - either 'infinity' or '0'. The value '0' only copies the resource and its properties, no children.
X-Overwrite - 'F' to prevent overwriting an existing destination
```

**요청**

```
COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"
```

**응답 코드**

```
201 - CREATED - if folder/asset has been copied to a non-existing destination
204 - NO CONTENT - if the folder/asset has been copied to an existing destination
412 - PRECONDITION FAILED - if a request header is missing or
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## 폴더 또는 자산 이동 {#move-a-folder-or-asset}

지정된 경로의 폴더 또는 자산을 새 대상으로 이동합니다.

**요청 헤더**

```
X-Destination - a new destination URI within the API solution scope to copy the resource to
X-Depth - either 'infinity' or '0'. The value '0' only copies the resource and its properties, no children.
X-Overwrite - either 'T' to force deletion of existing resources or 'F' to prevent overwriting an existing resource.
```

**요청**

```
MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"
```

**응답 코드**

```
201 - CREATED - if folder/asset has been copied to a non-existing destination
204 - NO CONTENT - if the folder/asset has been copied to an existing destination
412 - PRECONDITION FAILED - if a request header is missing or
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## 폴더, 자산 또는 변환 삭제 {#delete-a-folder-asset-or-rendition}

지정된 경로에서 리소스(-tree)를 삭제합니다.

**요청**

```
DELETE /api/assets/myFolder
```

또는

```
DELETE /api/assets/myFolder/myAsset.png
```

또는

```xml
DELETE /api/assets/myFolder/myAsset.png/renditions/original
```

**응답 코드**

```
200 - OK - if folder has been deleted successfully
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```
