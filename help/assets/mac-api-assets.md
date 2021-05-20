---
title: '[!DNL Assets] HTTP API.'
description: ' [!DNL Adobe Experience Manager Assets]에서 HTTP API를 사용하여 디지털 자산을 생성, 읽기, 업데이트, 삭제 및 관리합니다.'
contentOwner: AG
role: Developer
feature: API,Assets HTTP API,개발자 도구
exl-id: 6bc10f4e-a951-49ba-9c71-f568a7f2e40d
source-git-commit: 15f83387629687994bc2ffee4156d7d42dc1c537
workflow-type: tm+mt
source-wordcount: '1729'
ht-degree: 1%

---

# [!DNL Assets] HTTP API {#assets-http-api}

## 개요 {#overview}

[!DNL Assets] HTTP API를 사용하면 메타데이터, 변환 및 주석 등을 포함한 디지털 자산에 대해 [!DNL Experience Manager] 컨텐츠 조각을 사용하여 구조화된 컨텐츠와 함께 CRUD(create-read-update-delete) 작업을 수행할 수 있습니다. 이 변수는 `/api/assets`에 노출되며 REST API로 구현됩니다. 여기에는 [컨텐츠 조각](/help/assets/assets-api-content-fragments.md)에 대한 지원이 포함됩니다.

API에 액세스하려면:

1. `https://[hostname]:[port]/api.json`에서 API 서비스 문서를 엽니다.
1. `https://[hostname]:[server]/api/assets.json` 로 연결되는 [!DNL Assets] 서비스 링크를 따르십시오.

API 응답은 일부 MIME 유형에 대한 JSON 파일이며 모든 MIME 유형에 대한 응답 코드입니다. JSON 응답은 선택 사항이며 PDF 파일과 같이 사용할 수 없습니다. 추가적인 분석 또는 작업을 위해서는 응답 코드를 사용하십시오.

[!UICONTROL 해제 시간] 이후에는 [!DNL Assets] 웹 인터페이스와 HTTP API를 통해 자산 및 해당 표현물을 사용할 수 없습니다. [!UICONTROL On Time]이 미래 또는 [!UICONTROL Off Time]이 과거 상태인 경우 API는 404 오류 메시지를 반환합니다.

>[!CAUTION]
>
>[HTTP API는 네임스페이스의 메타데이터 ](#update-asset-metadata) 속성을  `jcr` 업데이트합니다. 그러나 Experience Manager 사용자 인터페이스는 `dc` 네임스페이스의 메타데이터 속성을 업데이트합니다.

## 콘텐츠 조각 {#content-fragments}

[컨텐츠 조각](/help/assets/content-fragments/content-fragments.md)은 특별한 유형의 자산입니다. 텍스트, 숫자, 날짜 등과 같은 구조화된 데이터에 액세스하는 데 사용할 수 있습니다. `standard` 자산(이미지 또는 문서 등)에 몇 가지 차이점이 있으므로 일부 추가 규칙이 컨텐츠 조각 처리에 적용됩니다.

자세한 내용은 Experience Manager 자산 HTTP API](/help/assets/assets-api-content-fragments.md)에서 [컨텐츠 조각 지원 을 참조하십시오.

## 데이터 모델 {#data-model}

[!DNL Assets] HTTP API는 두 개의 주요 요소, 폴더 및 자산(표준 자산의 경우)을 표시합니다.

또한 컨텐츠 조각에 구조화된 컨텐츠를 설명하는 사용자 지정 데이터 모델에 대해 더 자세한 요소를 노출합니다. 자세한 내용은 [컨텐츠 조각 데이터 모델](/help/assets/assets-api-content-fragments.md#content-fragments)을 참조하십시오.

### 폴더 {#folders}

폴더는 기존 파일 시스템의 디렉토리와 같습니다. 다른 폴더 또는 어설션의 컨테이너입니다. 폴더에는 다음 구성 요소가 있습니다.

**엔티티**:폴더의 엔티티는 폴더 및 자산일 수 있는 하위 요소입니다.

**속성**:

* `name` 은 폴더의 이름입니다. 확장 없이 URL 경로에 있는 마지막 세그먼트와 동일합니다.
* `title` 은 폴더 이름 대신 표시할 수 있는 폴더의 선택적 제목입니다.

>[!NOTE]
>
>폴더 또는 자산의 일부 속성이 다른 접두사에 매핑됩니다. `jcr:title`, `jcr:description` 및 `jcr:language`의 `jcr` 접두사가 `dc` 접두사로 대체됩니다. 따라서 반환된 JSON에서 `dc:title` 및 `dc:description`에 각각 `jcr:title` 및 `jcr:description`의 값이 포함됩니다.

**** LinksFolders에 세 개의 링크가 표시됩니다.

* `self`:직접 연결합니다.
* `parent`:상위 폴더에 연결합니다.
* `thumbnail`:(선택 사항) 폴더 축소판 이미지에 연결된 링크입니다.

### 자산 {#assets}

Experience Manager 시 자산에 다음 요소가 포함됩니다.

* 자산의 속성 및 메타데이터입니다.
* 원본 표현물(원래 업로드된 자산), 축소판 및 기타 표현물과 같은 여러 표현물이 있습니다. 추가 표현물은 다양한 크기, 다양한 비디오 인코딩 또는 PDF 또는 [!DNL Adobe InDesign] 파일에서 추출된 페이지의 이미지일 수 있습니다.
* 선택적 주석입니다.

컨텐츠 조각의 요소에 대한 자세한 내용은 Experience Manager 자산 HTTP API](/help/assets/assets-api-content-fragments.md#content-fragments)의 컨텐츠 조각 지원 을 참조하십시오.[

[!DNL Experience Manager]에는 폴더에 다음 구성 요소가 있습니다.

* 엔터티:자산의 자식은 표현물입니다.
* 속성.
* 링크.

[!DNL Assets] HTTP API에는 다음 기능이 포함되어 있습니다.

* [폴더 목록을 검색합니다](#retrieve-a-folder-listing).
* [폴더를 만듭니다](#create-a-folder).
* [자산 만들기](#create-an-asset).
* [자산 바이너리를 업데이트합니다](#update-asset-binary).
* [자산 메타데이터를 업데이트합니다](#update-asset-metadata).
* [자산 표현물을 만듭니다](#create-an-asset-rendition).
* [자산 표현물을 업데이트합니다](#update-an-asset-rendition).
* [자산 주석](#create-an-asset-comment) 만들기
* [폴더 또는 자산을 복사합니다](#copy-a-folder-or-asset).
* [폴더 또는 자산을 이동합니다](#move-a-folder-or-asset).
* [폴더, 자산 또는 표현물을 삭제합니다](#delete-a-folder-asset-or-rendition).

>[!NOTE]
>
>가독성을 쉽게 하기 위해 다음 예에는 전체 cURL 표기법을 생략합니다. 실제로 표기법은 `cURL`에 대한 스크립트 래퍼인 [Resty](https://github.com/micha/resty)과 상호 연결됩니다.

**전제 조건**

* 액세스 `https://[aem_server]:[port]/system/console/configMgr`.
* **[!UICONTROL Granite CSRF Adobe 필터]**&#x200B;로 이동합니다.
* **[!UICONTROL 필터 메서드]**&#x200B;에 다음이 포함되어 있는지 확인하십시오.`POST`, `PUT`, `DELETE`.

## {#retrieve-a-folder-listing} 목록을 포함하는 폴더 검색

기존 폴더 및 하위 엔티티(하위 폴더 또는 자산)의 Similar 표현을 검색합니다.

**요청**:  `GET /api/assets/myFolder.json`

**응답 코드**:응답 코드는 다음과 같습니다.

* 200 - OK - 성공.
* 404 - 찾을 수 없음 - 폴더가 없거나 액세스할 수 없습니다.
* 500 - 내부 서버 오류 - 다른 오류가 발생한 경우

**응답**:반환된 엔티티의 클래스는 자산 또는 폴더입니다. 포함된 엔티티의 등록 정보는 각 엔티티의 전체 등록 정보 집합의 하위 집합입니다. 엔티티의 전체 표현을 가져오려면 클라이언트가 `self` 의 `rel` 링크가 가리키는 URL의 컨텐츠를 검색해야 합니다.

## 폴더를 만듭니다 {#create-a-folder}

새 `sling`을 만듭니다.지정된 경로에서 `OrderedFolder`. 노드 이름 대신 `*`이 제공되면 서블릿은 매개 변수 이름을 노드 이름으로 사용합니다. 요청 데이터가 `application/www-form-urlencoded` 또는 `multipart`/ `form`- `data`(으)로 인코딩된 새 폴더 또는 이름-값 쌍 집합의 Shanner 표현 중 하나로 허용되므로 HTML 양식에서 직접 폴더를 만드는 데 유용합니다. 또한 폴더의 속성을 URL 쿼리 매개 변수로 지정할 수 있습니다.

제공된 경로의 상위 노드가 없는 경우 API 호출이 `500` 응답 코드로 실패합니다. 폴더가 이미 있으면 호출에서 응답 코드 `409`을 반환합니다.

**매개 변수**: `name` 는 폴더 이름입니다.

**요청**

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"title=My Folder"`

**응답 코드**:응답 코드는 다음과 같습니다.

* 201 - 생성됨 - 성공적으로 만들 때.
* 409 - 충돌 - 폴더가 이미 있는 경우.
* 412 - 전제 조건 실패 - 루트 컬렉션을 찾을 수 없거나 액세스할 수 없는 경우.
* 500 - 내부 서버 오류 - 다른 오류가 발생한 경우

## 자산 만들기 {#create-an-asset}

제공된 파일을 제공된 경로에 놓아 DAM 저장소에 자산을 만듭니다. 노드 이름 대신 `*`이 제공되는 경우 서블릿은 매개 변수 이름이나 파일 이름을 노드 이름으로 사용합니다.

**매개 변수**:매개 변수 `name` 는 자산 이름 및 파일 참조 `file` 에 대한 것입니다.

**요청**

* `POST /api/assets/myFolder/myAsset.png -H"Content-Type: image/png" --data-binary "@myPicture.png"`
* `POST /api/assets/myFolder/* -F"name=myAsset.png" -F"file=@myPicture.png"`

**응답 코드**:응답 코드는 다음과 같습니다.

* 201 - 작성됨 - 자산이 성공적으로 생성된 경우.
* 409 - 충돌 - 자산이 이미 있는 경우.
* 412 - 전제 조건 실패 - 루트 컬렉션을 찾을 수 없거나 액세스할 수 없는 경우.
* 500 - 내부 서버 오류 - 다른 오류가 발생한 경우

## 자산 이진 {#update-asset-binary} 업데이트

자산의 바이너리(이름이 원래 표현물)를 업데이트합니다. 구성된 경우 업데이트는 실행할 기본 자산 처리 워크플로우를 트리거합니다.

**요청**:  `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: image/png" --data-binary @myPicture.png`

**응답 코드**:응답 코드는 다음과 같습니다.

* 200 - 확인 - 자산이 성공적으로 업데이트된 경우.
* 404 - 찾을 수 없음 - 제공된 URI에서 자산을 찾거나 액세스할 수 없는 경우.
* 412 - 전제 조건 실패 - 루트 컬렉션을 찾을 수 없거나 액세스할 수 없는 경우.
* 500 - 내부 서버 오류 - 다른 오류가 발생한 경우

## 자산 메타데이터 {#update-asset-metadata} 업데이트

자산 메타데이터 속성을 업데이트합니다. `dc:` 네임스페이스에서 속성을 업데이트하면 API는 `jcr` 네임스페이스에서 동일한 속성을 업데이트합니다. API는 두 네임스페이스 아래의 속성을 동기화하지 않습니다.

**요청**:  `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"jcr:title":"My Asset"}}'`

**응답 코드**:응답 코드는 다음과 같습니다.

* 200 - 확인 - 자산이 성공적으로 업데이트된 경우.
* 404 - 찾을 수 없음 - 제공된 URI에서 자산을 찾거나 액세스할 수 없는 경우.
* 412 - 전제 조건 실패 - 루트 컬렉션을 찾을 수 없거나 액세스할 수 없는 경우.
* 500 - 내부 서버 오류 - 다른 오류가 발생한 경우

### `dc` 및 `jcr` 네임스페이스 {#sync-metadata-between-namespaces} 간의 동기화 메타데이터 업데이트

API 메서드는 `jcr` 네임스페이스의 메타데이터 속성을 업데이트합니다. 사용자 인터페이스를 사용하여 업데이트하면 `dc` 네임스페이스의 메타데이터 속성이 변경됩니다. 메타데이터 값을 `dc` 과 `jcr` 네임스페이스 간에 동기화하려면 워크플로우를 만들고 Experience Manager을 구성하여 자산 편집 시 워크플로우를 실행할 수 있습니다. ECMA 스크립트를 사용하여 필요한 메타데이터 속성을 동기화합니다. 다음 샘플 스크립트는 `dc:title` 와 `jcr:title` 사이에 제목 문자열을 동기화합니다.

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

## 자산 표현물 {#create-an-asset-rendition} 만들기

자산에 대한 새 자산 표현물을 만듭니다. 요청 매개 변수 이름을 제공하지 않으면 파일 이름이 변환 이름으로 사용됩니다.

**매개 변수**:매개 변수 `name` 는 표현물 이름과 파일 참조 `file` 로 사용됩니다.

**요청**

* `POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"`
* `POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"`

**응답 코드**:응답 코드는 다음과 같습니다.

* 201 - CREATED - Rendition이 성공적으로 작성된 경우.
* 404 - 찾을 수 없음 - 제공된 URI에서 자산을 찾거나 액세스할 수 없는 경우.
* 412 - 전제 조건 실패 - 루트 컬렉션을 찾을 수 없거나 액세스할 수 없는 경우.
* 500 - 내부 서버 오류 - 다른 오류가 발생한 경우

## 자산 표현물 {#update-an-asset-rendition} 업데이트

업데이트는 자산 표현물을 새 이진 데이터로 바꿉니다.

**요청**:  `PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png`

**응답 코드**:응답 코드는 다음과 같습니다.

* 200 - 확인 - 렌디션이 성공적으로 업데이트된 경우.
* 404 - 찾을 수 없음 - 제공된 URI에서 자산을 찾거나 액세스할 수 없는 경우.
* 412 - 전제 조건 실패 - 루트 컬렉션을 찾을 수 없거나 액세스할 수 없는 경우.
* 500 - 내부 서버 오류 - 다른 오류가 발생한 경우

## 자산 {#create-an-asset-comment}에 주석 추가

새 자산 설명을 만듭니다.

**매개 변수**:매개 변수 `message` 는 댓글의 메시지 본문 및 JSON 형식 `annotationData` 의 주석 데이터에 대한 것입니다.

**요청**:  `POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"`

**응답 코드**:응답 코드는 다음과 같습니다.

* 201 - CREATED - 설명이 성공적으로 작성된 경우
* 404 - 찾을 수 없음 - 제공된 URI에서 자산을 찾거나 액세스할 수 없는 경우.
* 412 - 전제 조건 실패 - 루트 컬렉션을 찾을 수 없거나 액세스할 수 없는 경우.
* 500 - 내부 서버 오류 - 다른 오류가 발생한 경우

## 폴더 또는 자산 {#copy-a-folder-or-asset} 복사

제공된 경로에서 사용할 수 있는 폴더 또는 자산을 새 대상에 복사합니다.

**요청 헤더**:매개 변수는 다음과 같습니다.

* `X-Destination` - 리소스를 복사할 API 솔루션 범위 내의 새 대상 URI입니다.
* `X-Depth` - 또 `infinity` 는  `0`. `0`을 사용하면 리소스와 해당 속성만 복사되며 하위 항목은 복사되지 않습니다.
* `X-Overwrite` - 기존 대상 `F` 의 자산을 덮어쓰지 않도록 하려면 을 사용하십시오.

**요청**:  `COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**응답 코드**:응답 코드는 다음과 같습니다.

* 201 - 작성됨 - 폴더/자산이 존재하지 않는 대상에 복사된 경우
* 204 - 컨텐츠 없음 - 폴더/자산이 기존 대상에 복사된 경우
* 412 - 전제 조건 실패 - 요청 헤더가 누락된 경우.
* 500 - 내부 서버 오류 - 다른 오류가 발생한 경우

## 폴더 또는 자산 {#move-a-folder-or-asset} 이동

지정된 경로의 폴더 또는 자산을 새 대상으로 이동합니다.

**요청 헤더**:매개 변수는 다음과 같습니다.

* `X-Destination` - 리소스를 복사할 API 솔루션 범위 내의 새 대상 URI입니다.
* `X-Depth` - 또 `infinity` 는  `0`. `0`을 사용하면 리소스와 해당 속성만 복사되며 하위 항목은 복사되지 않습니다.
* `X-Overwrite` - 기존 리소스 `T` 를 강제로 삭제하거나 기존 리소스를 덮어쓰지  `F` 않도록 하려면 다음 중 하나를 사용합니다.

**요청**:  `MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"`

URL에서 `/content/dam`을 사용하지 마십시오. 자산을 이동하고 기존 자산을 덮어쓰는 샘플 명령은 다음과 같습니다.

```shell
curl -u admin:admin -X MOVE https://[aem_server]:[port]/api/assets/source/file.png -H "X-Destination: http://[aem_server]:[port]/api/assets/destination/file.png" -H "X-Overwrite: T"
```

**응답 코드**:응답 코드는 다음과 같습니다.

* 201 - 작성됨 - 폴더/자산이 존재하지 않는 대상에 복사된 경우
* 204 - 컨텐츠 없음 - 폴더/자산이 기존 대상에 복사된 경우
* 412 - 전제 조건 실패 - 요청 헤더가 누락된 경우.
* 500 - 내부 서버 오류 - 다른 오류가 발생한 경우

## 폴더, 자산 또는 표현물 {#delete-a-folder-asset-or-rendition} 삭제

제공된 경로에서 리소스(-tree)를 삭제합니다.

**요청**

* `DELETE /api/assets/myFolder`
* `DELETE /api/assets/myFolder/myAsset.png`
* `DELETE /api/assets/myFolder/myAsset.png/renditions/original`

**응답 코드**:응답 코드는 다음과 같습니다.

* 200 - 확인 - 폴더가 성공적으로 삭제된 경우
* 412 - 전제 조건 실패 - 루트 컬렉션을 찾을 수 없거나 액세스할 수 없는 경우.
* 500 - 내부 서버 오류 - 다른 오류가 발생한 경우

## 팁 및 제한 사항 {#tips-best-practices-limitations}

* [HTTP API는 네임스페이스의 메타데이터 ](#update-asset-metadata) 속성을  `jcr` 업데이트합니다. 그러나 Experience Manager 사용자 인터페이스는 `dc` 네임스페이스의 메타데이터 속성을 업데이트합니다.

* Assets HTTP API는 전체 메타데이터를 반환하지 않습니다. 네임스페이스는 하드코딩되며 이러한 네임스페이스만 반환됩니다. 전체 메타데이터에 대해서는 자산 경로 `/jcr_content/metadata.json`을 참조하십시오.
