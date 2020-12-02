---
title: 양식 포털에서 제출된 양식을 사용한 작업 API
seo-title: 양식 포털에서 제출된 양식을 사용한 작업 API
description: AEM Forms은 양식 포털에서 제출된 양식 데이터를 쿼리하고 작업을 수행하는 데 사용할 수 있는 API를 제공합니다.
seo-description: AEM Forms은 양식 포털에서 제출된 양식 데이터를 쿼리하고 작업을 수행하는 데 사용할 수 있는 API를 제공합니다.
uuid: c47c8392-e5a9-4c40-b65e-4a7f379a6b45
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish, developer-reference
discoiquuid: 9457effd-3595-452f-a976-ad9eda6dc909
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 4%

---


# 양식 포털 {#apis-to-work-with-submitted-forms-on-forms-portal}에서 제출된 양식을 사용하여 작업하는 API

AEM Forms은 양식 포털을 통해 제출된 양식 데이터를 쿼리하는 데 사용할 수 있는 API를 제공합니다. 또한 이 문서에 설명된 API를 사용하여 의견을 게시하거나 제출된 양식의 속성을 업데이트할 수 있습니다.

>[!NOTE]
>
>API를 호출하는 사용자는 [제출 검토자를 양식](/help/forms/using/adding-reviewers-form.md)에 연결하는 설명에 따라 검토자 그룹에 추가해야 합니다.

## GET /content/forms/portal/submission.review.json?func=getFormsForSubmissionReview {#get-content-forms-portal-submission-review-json-func-getformsforsubmissionreview-br}

모든 자격 조건을 갖춘 양식 목록을 반환합니다.

### URL 매개 변수 {#url-parameters}

이 API에는 추가 매개 변수가 필요하지 않습니다.

### 응답 {#response}

응답 개체에는 양식 이름과 해당 저장소 경로를 포함하는 JSON 배열이 포함되어 있습니다. 응답의 구조는 다음과 같습니다.

```json
[
 {formName: "<form name>",
 formPath: "<path to the form>" },
 {.....},
 ......]
```

### 예 {#example}

**요청 URL**

```http
https://[host]:[port]/content/forms/portal/submission.review.json?func=getFormsForSubmissionReview
```

**응답**

```json
[{"formPath":"/content/dam/formsanddocuments/forms-review/form2","formName":"form2"},{"formPath":"/content/dam/formsanddocuments/forms-review/form1","formName":"form1"}]
```

## GET /content/forms/portal/submission.review.json?func=getAllSubmissions {#get-content-forms-portal-submission-review-json-func-getallsubmissions}

제출된 모든 양식의 세부 정보를 반환합니다. 그러나 URL 매개 변수를 사용하여 결과를 제한할 수 있습니다.

### URL 매개 변수 {#url-parameters-1}

요청 URL에 다음 매개 변수를 지정합니다.

<table>
 <tbody>
  <tr>
   <th>매개 변수</th>
   <th>설명</th>
  </tr>
  <tr>
   <td><code>formPath</code></td>
   <td>양식이 있는 CRX 저장소 경로를 지정합니다. 양식 경로를 지정하지 않으면 빈 응답이 반환됩니다.<br /> </td>
  </tr>
  <tr>
   <td><code>offset</code> (옵션)</td>
   <td>결과 세트의 인덱스의 시작점을 지정합니다. 기본값은 <strong>0</strong>입니다.</td>
  </tr>
  <tr>
   <td><code>limit</code> (옵션)</td>
   <td>결과 수를 제한합니다. 기본값은 <strong>30</strong>입니다.</td>
  </tr>
  <tr>
   <td><code>orderby</code> <br /> (옵션)</td>
   <td>결과 정렬 속성을 지정합니다. 기본값은 <strong>jcr:lastModified</strong>입니다. 이 값은 마지막으로 수정한 시간을 기준으로 결과를 정렬합니다.</td>
  </tr>
  <tr>
   <td><code>sort</code> <br /> (옵션)</td>
   <td>결과 정렬 순서를 지정합니다. 기본값은 결과를 내림차순으로 정렬하는 <strong>desc</strong>입니다. 결과를 오름차순으로 정렬하려면 <code>asc</code>을 지정할 수 있습니다.</td>
  </tr>
  <tr>
   <td><code>cutPoints</code> <br /> (옵션)</td>
   <td>결과에 포함할 양식 속성의 쉼표로 구분된 목록을 지정합니다. 기본 속성은 다음과 같습니다.<br /> <code>formName</code>, <code>formPath</code>, <code>submitID</code>, <code>formType</code>, <code>jcr:lastModified</code>, <code>owner</code></td>
  </tr>
  <tr>
   <td><code>search</code> <br /> (옵션)</td>
   <td>양식 속성에서 지정된 값을 검색하고 일치하는 값이 있는 양식을 반환합니다. 기본값은 <strong>"</strong>입니다.</td>
  </tr>
 </tbody>
</table>

### 응답 {#response-1}

응답 개체에는 지정된 양식의 세부 사항을 포함하는 JSON 배열이 포함되어 있습니다. 응답의 구조는 다음과 같습니다.

```json
{
 total: "<total number of submissions>",
 items: [{ formName: "<name of the form>", formPath: "<path to the form>", owner: "<owner of the form>"},
 ....]}
```

### 예 {#example-1}

**요청 URL**

```http
https://[host]:[port]/content/forms/portal/submission.review.json?func=getAllSubmissions&formPath=/content/dam/formsanddocuments/forms-review/form2
```

**응답**

```json
{"total":1,"items":[{"formName":"form2","formPath":"/content/dam/formsanddocuments/forms-review/form2","submitID":"1403037413508500","formType":"af","jcr:lastModified":"2015-11-05T17:52:32.243+05:30","owner":"admin"}]}
```

## POST /content/forms/portal/submission.review.json?func=addComment {#post-content-forms-portal-submission-review-json-func-addcomment-br}

지정된 제출 인스턴스에 주석을 추가합니다.

### URL 매개 변수 {#url-parameters-2}

요청 URL에 다음 매개 변수를 지정합니다.

| 매개 변수 | 설명 |
|---|---|
| `submitID` | 제출 인스턴스와 연결된 메타데이터 ID를 지정합니다. |
| `Comment` | 지정된 제출 인스턴스에 추가할 주석 텍스트를 지정합니다. |

### 응답 {#response-2}

댓글을 성공적으로 게시할 때 댓글 ID를 반환합니다.

### 예 {#example-2}

**요청 URL**

```http
https://[host:'port'/content/forms/portal/submission.review.json?func=addComment&submitID=1403037413508500&comment=API+test+comment
```

**응답**

```java
1403873422601300
```

## GET /content/forms/portal/submission.review.json?func=getComments   {#get-content-forms-portal-submission-review-json-func-getcomments-nbsp}

지정된 제출 인스턴스에 게시된 모든 댓글을 반환합니다.

### URL 매개 변수 {#url-parameters-3}

요청 URL에 다음 매개 변수를 지정합니다.

| 매개 변수 | 설명 |
|---|---|
| `submitID` | 제출 인스턴스의 메타데이터 ID를 지정합니다. |

### 응답 {#response-3}

응답 개체에는 지정된 제출 ID와 관련된 모든 주석을 포함하는 JSON 배열이 포함되어 있습니다. 응답의 구조는 다음과 같습니다.

```json
[{
 owner: "<name of the commenter>",
 comment: "<comment text>",
 time: "<time when the comment was posted>"},
 { }......]
```

### 예 {#example-3}

**요청 URL**

```http
https://[host]:'port'/content/forms/portal/submission.review.json?func=getComments&submitID=1403037413508500
```

**응답**

```java
[{"owner":"fr1","comment":"API test comment","time":1446726988250}]
```

## POST /content/forms/portal/submission.review.json?func=update제출 {#post-content-forms-portal-submission-review-json-func-updatesubmission-br}

지정된 제출된 양식 인스턴스의 지정된 속성 값을 업데이트합니다.

### URL 매개 변수 {#url-parameters-4}

요청 URL에 다음 매개 변수를 지정합니다.

| 매개 변수 | 설명 |
|---|---|
| `submitID` | 제출 인스턴스와 연결된 메타데이터 ID를 지정합니다. |
| `property` | 업데이트할 양식 속성을 지정합니다. |
| `value` | 업데이트할 양식 속성의 값을 지정합니다. |

### 응답 {#response-4}

게시된 업데이트에 대한 정보가 있는 JSON 개체를 반환합니다.

### 예 {#example-4}

**요청 URL**

```http
https://[host]:'port'/content/forms/portal/submission.review.json?func=updateSubmission&submitID=1403037413508500&value=sample_value&property=some_new_prop
```

**응답**

```json
{"formName":"form2","owner":"admin","jcr:lastModified":1446727516593,"path":"/content/forms/fp/admin/submit/metadata/1403037413508500.html","submitID":"1403037413508500","status":"submitted"}
```

