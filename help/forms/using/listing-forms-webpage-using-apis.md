---
title: API를 사용하여 웹 페이지에 양식 나열
seo-title: API를 사용하여 웹 페이지에 양식 나열
description: Forms Manager를 프로그래밍 방식으로 쿼리하여 필터링된 양식 목록을 검색하고 웹 페이지에 표시할 수 있습니다.
seo-description: Forms Manager를 프로그래밍 방식으로 쿼리하여 필터링된 양식 목록을 검색하고 웹 페이지에 표시할 수 있습니다.
uuid: e51cb2d4-816f-4e6d-a081-51e4999b00ba
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 515ceaf6-c132-4e1a-b3c6-5d2c1ccffa7c
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 1%

---


# API {#listing-forms-on-a-web-page-using-apis}를 사용하여 웹 페이지에 양식 나열

AEM Forms은 웹 개발자가 검색 조건에 맞는 양식 세트를 쿼리하고 검색하는 데 사용할 수 있는 REST 기반 검색 API를 제공합니다. API를 사용하여 다양한 필터를 기반으로 양식을 검색할 수 있습니다. 응답 객체에는 양식 특성, 속성 및 양식의 끝점 렌더링이 포함됩니다.

REST API를 사용하여 양식을 검색하려면 아래에 설명된 쿼리 매개 변수와 함께 `https://'[server]:[port]'/libs/fd/fm/content/manage.json`의 서버에 GET 요청을 보내십시오.

## 쿼리 매개 변수 {#query-parameters}

<table>
 <tbody>
  <tr>
   <td><strong>속성 이름<br /> </strong></td>
   <td><strong>설명<br /> </strong></td>
  </tr>
  <tr>
   <td>func<br /> </td>
   <td><p>호출할 함수를 지정합니다. 양식을 검색하려면 <code>func </code>속성 값을 <code>searchForms</code>로 설정합니다.</p> <p>예, <code class="code">
       URLParameterBuilder entityBuilder=new URLParameterBuilder ();
       entityBuilder.add("func", "searchForms");</code></p> <p><strong>참고: </strong> <em>이 매개 변수는 필수입니다.</em><br /> </p> </td>
  </tr>
  <tr>
   <td>appPath<br /> </td>
   <td><p>양식을 검색할 응용 프로그램 경로를 지정합니다. 기본적으로 appPath 속성은 루트 노드 수준에서 사용할 수 있는 모든 응용 프로그램을 검색합니다.<br /> </p> <p>단일 검색 쿼리에서 여러 응용 프로그램 경로를 지정할 수 있습니다. 파이프(|) 문자로 여러 패스를 구분합니다. </p> </td>
  </tr>
  <tr>
   <td>cutPoints<br /> </td>
   <td><p>에셋으로 가져올 속성을 지정합니다. 별표(*)를 사용하여 모든 속성을 한 번에 가져올 수 있습니다. 파이프(|) 연산자를 사용하여 여러 속성을 지정합니다. </p> <p>예, <code>cutPoints=propertyName1|propertyName2|propertyName3</code></p> <p><strong>메모</strong>: </p>
    <ul>
     <li><em>id, 경로 및 이름과 같은 속성은 항상 가져오는 것이 좋습니다. </em></li>
     <li><em>모든 에셋에는 다른 속성 세트가 있습니다. formUrl, pdfUrl 및 guideUrl과 같은 속성은 cutpoints 속성에 따라 다릅니다. 이러한 속성은 자산 유형에 따라 다르며 그에 따라 가져옵니다. </em></li>
    </ul> </td>
  </tr>
  <tr>
   <td>relation<br /> </td>
   <td>검색 결과와 함께 가져올 관련 자산을 지정합니다. 다음 옵션 중 하나를 선택하여 관련 자산을 가져올 수 있습니다.
    <ul>
     <li><strong>NO_RELATION</strong>:관련 자산을 가져오지 마십시오.</li>
     <li><strong>즉시</strong>:검색 결과와 직접 관련된 자산을 가져옵니다.</li>
     <li><strong>모두</strong>:직간접적으로 관련 자산을 가져옵니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>maxSize</td>
   <td>가져올 최대 양식 수를 지정합니다.</td>
  </tr>
  <tr>
   <td>오프셋</td>
   <td>처음부터 건너뛸 양식 수를 지정합니다.</td>
  </tr>
  <tr>
   <td>returnCount</td>
   <td>지정된 기준과 일치하는 검색 결과를 반환할지 여부를 지정합니다. </td>
  </tr>
  <tr>
   <td>statements</td>
   <td><p>문 목록을 지정합니다. 쿼리는 JSON 형식으로 지정된 문 목록에서 실행됩니다. </p> <p>예,</p> <p><code class="code">JSONArray statementArray=new JSONArray();
       JSONObject statement=new JSONObject();
       statement.put("name", "title");
       statement.put("value", "SimpleSurveyAF");
       statement.put("operator", "EQ"); statementArray.put(statement);</code></p> <p>위의 예에서 </p>
    <ul>
     <li><strong>이름</strong>:검색할 속성의 이름을 지정합니다.</li>
     <li><strong>값</strong>:검색할 속성의 값을 지정합니다.</li>
     <li><strong>연산자</strong>:검색하는 동안 적용할 연산자를 지정합니다. 다음 연산자가 지원됩니다.
      <ul>
       <li>EQ - 같음 </li>
       <li>NEQ - 같지 않음</li>
       <li>GT - 보다 큼</li>
       <li>LT - 보다 작음</li>
       <li>GTEQ - 크거나 같음</li>
       <li>LTEQ - 작거나 같음</li>
       <li>포함 - B가 A의 일부인 경우 A는 B를 포함합니다.</li>
       <li>전체 텍스트 - 전체 텍스트 검색</li>
       <li>STARTSWITH - A가 A의 시작 부분인 경우 B로 시작</li>
       <li>ENDSWITH - B가 A의 끝 부분인 경우 A는 B로 끝납니다.</li>
       <li>LIKE - LIKE 연산자를 구현합니다.</li>
       <li>AND - 여러 문 결합</li>
      </ul> <p><strong>참고: </strong> <em>GT, LT, GTEQ 및 LTEQ 연산자는 LONG, DOUBLE 및 DATE와 같은 선형 유형의 속성에 적용할 수 있습니다.</em></p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>ordering<br /> </td>
   <td><p>검색 결과에 대한 주문 기준을 지정합니다. 기준은 JSON 형식으로 정의됩니다. 둘 이상의 필드에서 검색 결과를 정렬할 수 있습니다. 쿼리에 필드가 나타나면 결과가 순서대로 정렬됩니다.</p> <p>예,</p> <p>제목 속성별로 정렬된 쿼리 결과를 오름차순으로 검색하려면 다음 매개 변수를 추가합니다. </p> <p><code class="code">JSONArray orderingsArray=new JSONArray();
       JSONObject orderings=new JSONObject();
       orderings.put("name", "title");
       orderings.put("criteria", "ASC");
       orderingsArray.put(orderings);
       entityBuilder.add("orderings", orderingsArray.toString());</code></p>
    <ul>
     <li><strong>이름</strong>:검색 결과를 정렬하는 데 사용할 속성의 이름을 지정합니다.</li>
     <li><strong>기준</strong>:결과의 순서를 지정합니다. order 속성에는 다음 값이 사용됩니다.
      <ul>
       <li>ASC - ASC를 사용하여 결과를 오름차순으로 정렬합니다.<br /> </li>
       <li>DES - 결과를 내림차순으로 정렬하려면 DES를 사용합니다.</li>
      </ul> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>includeXdp</td>
   <td>이진 내용을 검색할지 여부를 지정합니다. <code>includeXdp</code> 속성은 <code>FORM</code>, <code>PDFFORM</code> 및 <code>PRINTFORM</code> 유형의 자산에 적용할 수 있습니다.</td>
  </tr>
  <tr>
   <td>assetType</td>
   <td>게시된 모든 자산에서 검색할 자산 유형을 지정합니다. 파이프(|) 연산자를 사용하여 여러 자산 유형을 지정합니다. 유효한 에셋 유형은 FORM, PDFFORM, PRINTFORM, RESOURCE 및 GUIDE입니다.</td>
  </tr>
 </tbody>
</table>

## 샘플 요청 {#sample-request}

```json
func : searchForms
appPath : /content/dam/formsanddocuments/MyApplication23
cutPoints : title|description|author|status|creationDate|lastModifiedDate|activationDate|expiryDate|tags|allowedRenderFormat|formmodel
relation : NO_RELATION
includeXdp : false
maxSize : 10
offset : 0
returnCount : true
statements: [{"name":"name","value":"*Claim.xdp","operator":"CONTAINS"},
                {"name":"","value":"Expense","operator":"FULLTEXT"},
                {"name":"description","value":"ABCD*","operator":"CONTAINS"},
                {"name":"status","value":"false","operator":"EQ"},
                {"name":"lastModifiedDate","value":"01/09/2013","operator":"GTEQ"},
                {"name":"lastModifiedDate","value":"01/18/2013","operator":"LTEQ"}]
orderings:[{"name" :“lastModifiedDate“:”order”:”ASC”}]
```

## 샘플 응답 {#sample-response}

```json
[
{"resultCount":2},
    {"assetType":"FORM","name":"ExpenseClaim.xdp","id":"509fa2d5-e3c9-407b-b8dc-fa0ba08eb0ce",
       "path":"/content/dam/formsanddocuments/MyApplication23/1.0/ExpenseClaim.xdp",
       "title":"Expense Report","description":"ABCDEFGIJK","author":"Frank Bowman",
       "tags":[],"formUrl":"/content/dam/formsanddocuments/MyApplication23/1.0/ExpenseClaim.xdp/jcr:content",
       "pdfUrl":"/content/dam/formsanddocuments/MyApplication23/1.0/ExpenseClaim.xdp/jcr:content?type=pdf",
       "references":[],"images":[{"assetType":"resource","name":"Image.gif","id":"5477a127-8bbf-4cec-8f81-2689e5cb4a15",
       "path":"/content/dam/formsanddocuments/MyApplication23/1.0/Image.gif","resourceSize":0}],
       "status":false,"creationDate":1358429845623,"lastModifiedDate":1358429846771},
{"assetType":"FORM","name":"ExpenseClaim.xdp","id":"4312239b-b666-4d36-95bc-641b3a39ddd4",
       "path":"/content/dam/formsanddocuments/MyApplication23/ExpenseClaim.xdp",
       "title":"Expense Report","description":"ABCDefghijklm","author":"Frank Bowman",
       "tags":[],"formUrl":"/content/dam/formsanddocuments/MyApplication23/ExpenseClaim.xdp/jcr:content",
       "pdfUrl":"/content/dam/formsanddocuments/MyApplication23/ExpenseClaim.xdp/jcr:content?type=pdf",
       "references":[],"images":[{"assetType":"resource","name":"Image.gif","id":"118a2e3f-7097-4d8c-85d1-651306de284a",
       "path":"/content/dam/formsanddocuments/MyApplication23/Image.gif","resourceSize":0}],"status":false,
       "creationDate":1358429856690,"lastModifiedDate":1358430109023}
]
```

## 관련 문서

* [양식 포털 구성 요소 활성화](/help/forms/using/enabling-forms-portal-components.md)
* [양식 포털 페이지 만들기](/help/forms/using/creating-form-portal-page.md)
* [API를 사용하여 웹 페이지에 양식 목록 표시](/help/forms/using/listing-forms-webpage-using-apis.md)
* [초안 및 제출 구성 요소 사용](/help/forms/using/draft-submission-component.md)
* [초안 및 제출된 양식의 저장 영역 사용자 정의](/help/forms/using/draft-submission-component.md)
* [초안 및 제출 구성 요소를 데이터베이스와 통합하는 샘플](/help/forms/using/integrate-draft-submission-database.md)
* [양식 포털 구성 요소에 대한 템플릿 사용자 정의](/help/forms/using/customizing-templates-forms-portal-components.md)
* [포털에서 양식 게시 소개](/help/forms/using/introduction-publishing-forms.md)