---
title: 적응형 양식에 대한 표준 유효성 검사 오류 메시지
seo-title: Standard validation error messages for adaptive forms
description: 사용자 지정 오류 처리기를 사용하여 적응형 양식에 대한 유효성 검사 오류 메시지를 표준 형식으로 변환
seo-description: Transform the validation error messages for adaptive forms into standard format using custom error handlers
uuid: 0d1f9835-3e28-41d3-a3b1-e36d95384328
contentOwner: anujkapo
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
discoiquuid: ec062567-1c6b-497b-a1e7-1dbac2d60852
feature: Adaptive Forms
exl-id: 54a76d5c-d19b-4026-b71c-7b9e862874bc
source-git-commit: fbc371e59c4f80195fe90da5f635267141c8849e
workflow-type: tm+mt
source-wordcount: '2346'
ht-degree: 4%

---

# 적응형 Forms의 오류 핸들러 {#error-handlers-in-adaptive-form}

<span class="preview"> [새 적응형 양식 만들기](/help/forms/using/create-an-adaptive-form-core-components.md) 또는 [AEM Sites 페이지에 적응형 양식 추가](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) 작업을 할 때 현대적이고 확장 가능한 데이터 캡처 [코어 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)를 사용하는 것이 좋습니다. 이러한 구성 요소는 적응형 양식 만들기 작업이 대폭 개선되어 우수한 사용자 경험을 보장할 수 있게 되었음을 나타냅니다. 이 문서에서는 기초 구성 요소를 사용하여 적응형 양식을 작성하는 이전 접근법에 대해 설명합니다. </span>

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/add-custom-error-handler-adaptive-forms.html) |
| AEM 6.5 | 이 문서 |


AEM Forms은 양식 제출을 위해 기본 성공 및 오류 핸들러를 제공합니다. 또한 오류 처리기 함수를 사용자 지정하는 기능도 제공합니다. 예를 들어 특정 오류 코드의 백엔드에서 사용자 정의 워크플로를 호출하거나 서비스가 중단되었음을 고객에게 알려 줄 수 있습니다. 핸들러는 서버 응답을 기반으로 실행되는 클라이언트측 함수입니다. API를 사용하여 외부 서비스를 호출하면 유효성 검사를 위해 데이터가 서버로 전송되며, 이 데이터는 제출에 대한 성공 또는 오류 이벤트에 대한 정보와 함께 클라이언트에 응답을 반환합니다. 정보는 관련 핸들러에 매개 변수로 전달되어 함수를 실행합니다. 오류 처리기는 발생한 오류 또는 유효성 검사 문제를 관리하고 표시하는 데 도움이 됩니다.

![양식에 사용자 지정 오류 핸들러를 추가하는 방법을 이해하는 오류 핸들러 워크플로](/help/forms/using/assets/error-handler-workflow.png)

적응형 양식은 미리 설정된 유효성 검사 기준에 따라 필드에 입력한 내용을 확인하고 외부 서비스를 호출하도록 구성된 REST 끝점에서 반환되는 다양한 오류를 확인합니다. 적응형 양식에 사용하는 데이터 소스를 기반으로 유효성 검사 기준을 설정할 수 있습니다. 예를 들어 RESTful 웹 서비스를 데이터 소스로 사용하는 경우 Swagger 정의 파일에 유효성 검사 기준을 정의할 수 있습니다.

입력 값이 유효성 검사 기준을 충족하고 값이 다른 데이터 소스에 제출되면 적응형 양식에 오류 처리기를 사용하여 오류 메시지가 표시됩니다. 이 접근 방식과 유사하게, 적응형 Forms은 사용자 지정 오류 핸들러와 통합하여 데이터 유효성 검사를 수행합니다. 입력 값이 유효성 검사 기준을 충족하지 않으면 오류 메시지가 적응형 양식의 필드 수준에 표시됩니다. 이 문제는 서버에서 반환된 유효성 검사 오류 메시지가 표준 메시지 형식일 때 발생합니다.


## 오류 처리기 사용 {#uses-of-error-handler}

오류 핸들러는 다양한 용도로 사용됩니다. 다음은 오류 처리기 함수의 사용 목록입니다.
* **유효성 검사 수행**: 오류 처리는 사전 정의된 규칙 또는 기준에 따라 사용자 입력을 확인하는 것으로 시작합니다. 사용자가 적응형 양식을 작성할 때 오류 처리기는 입력의 유효성을 검사하여 필요한 형식, 길이 또는 기타 제약 조건을 충족하는지 확인합니다.

* **실시간 피드백 제공**: 오류가 감지되면 오류 처리기는 해당 양식 필드 아래에 인라인 오류 메시지와 같은 즉각적인 피드백을 사용자에게 표시합니다. 이 피드백은 사용자가 양식을 제출하고 응답을 기다릴 필요 없이 오류를 식별하고 수정하는 데 도움이 됩니다.


* **오류 메시지 표시**: 적응형 양식 제출에 유효성 검사 오류가 발생하면 오류 처리기에 적절한 오류 메시지가 표시됩니다. 오류 메시지는 명확하고 간결하며 주의가 필요한 특정 필드를 강조해야 합니다.

* **잘못된 필드를 강조 표시합니다.**: 잘못된 특정 필드에 사용자의 주의를 끌기 위해 오류 처리기는 해당 필드를 강조 표시하거나 시각적으로 구분합니다. 이 작업은 사용자가 오류를 빠르게 찾고 해결하는 데 도움이 되는 배경색 변경, 아이콘 또는 테두리 또는 기타 시각적 큐를 추가하여 수행됩니다.


## 실패/오류 응답 형식 {#failure-response-format}

서버 유효성 검사 오류 메시지가 다음 표준 형식인 경우 적응형 양식에 필드 수준에서 오류가 표시됩니다.
아래 코드는 기존 실패 응답 구조를 보여 줍니다.

```javascript
   {
    errorCausedBy : "SERVER_SIDE_VALIDATION/SERVICE_INVOCATION_FAILURE"
    errors : [
        {
             somExpression  : <somexpr>
             errorMessage / errorMessages : <validationMsg> / [<validationMsg>, <validationMsg>]
        }
    ]
    originCode : <target error Code>
    originMessage : <unstructured error message returned by service>
    }
```


위치:

* `errorCausedBy` 실패 이유를 설명합니다.
* `errors` 유효성 검사 오류 메시지와 함께 유효성 검사 기준에 실패한 필드의 SOM 식을 언급하십시오.
* `originCode` AEM에서 추가한 필드이며 외부 서비스에서 반환한 http 상태 코드를 포함합니다.
* `originMessage` AEM에서 추가한 필드에 외부 서비스에서 반환한 원시 오류 데이터가 포함되어 있습니다.

AEM Forms 버전의 기능 및 후속 업데이트의 개선으로, 기존 오류 응답 구조가 기존 오류 응답 구조와 이전 버전과 호환되는 RFC7807에 따라 새 형식으로 변경되었습니다.

```javascript
    {
        "type": "SERVER_SIDE_VALIDATION/FORM_SUBMISSION/SERVICE_INVOCATION/FAILURE/VALIDATION_ERROR", (required)
        "title": "Server side validation failed/Third party service invocation failed", (optional)
        "detail": "", (optional)
        "instance": "", (optional)
        "validationErrors" : [ (required)
            {
                "fieldName":"<SOM expression of the field whose data sent is invalid>",
                "dataRef":<JSONPath (or XPath) of the data element which is invalid>
                "details": ["Error Message(s) for the field"] (required)
    
            }
        ],
        "originCode": <Origin http status code>, (optional - in case of SERVER_SIDE_VALIDATION)
        "originMessage" : "<unstructured error message returned by service>" (optional - in case of SERVER_SIDE_VALIDATION)
    }
```


>[!NOTE]
>
> * 오류 응답 구조에 다음 중 하나가 포함되어 있는지 확인합니다. **fieldName** 또는 **dataRef**.
> * 다음을 확인합니다. **ContentType** 헤더: **application/문제+json**.

위치:
* `type (required)` 실패 유형을 지정합니다. 다음 값 중 하나일 수 있습니다.
   * `SERVER_SIDE_VALIDATION` 서버측 유효성 검사로 인한 실패를 나타냅니다.
   * `FORM_SUBMISSION` 양식 제출 중 실패를 나타냅니다.
   * `SERVICE_INVOCATION` 서드파티 서비스 호출 중 실패를 나타냅니다.
   * `FAILURE` 일반 오류를 나타냅니다.
   * `VALIDATION_ERROR` 유효성 검사 오류로 인한 실패를 나타냅니다.

* `title (optional)` 오류의 제목이나 간단한 설명을 제공합니다.
* `detail (optional)` 필요한 경우 실패에 대한 추가 세부 정보를 제공합니다.
* `instance (optional)` 실패와 연관된 인스턴스 또는 식별자를 나타내며 실패의 특정 발생을 추적하거나 식별하는 데 도움이 됩니다.
* `validationErrors (required)` 유효성 검사 오류에 대한 정보를 포함합니다. 여기에는 다음 필드가 포함됩니다.
   * `fieldname` 은 유효성 검사 기준에 실패한 필드의 SOM 식을 언급합니다.
   * `dataRef` 유효성 검사에 실패한 필드의 JSON 경로 또는 XPath를 나타냅니다.
   * `details` 유효성 검사 오류 메시지와 잘못된 필드를 포함합니다.
* `originCode (optional)` AEM에서 추가한 필드이며 외부 서비스에서 반환한 http 상태 코드를 포함합니다.
* `originMessage (optional)` AEM에서 추가한 필드에 외부 서비스에서 반환한 원시 오류 데이터가 포함되어 있습니다.

### 샘플 오류 응답 형식 {#sample-error-response-format}

오류 응답을 표시하는 옵션 중 일부는 다음과 같습니다.

+++  적응형 양식 fieldName 속성 기반


* **`Header:`** `content-type:application/problem+json`
* **`Response:`**

  ```javascript
          {
              "type": "VALIDATION_ERROR",
              "validationErrors": [
              {
              "fieldName": "guide[0].guide1[0].guideRootPanel[0].textbox1686647736683[0]",
              "dataRef": "",
              "details": [
              "Invalid ID supplied. Provided value is not correct!"
          ]
          }
          ]}
  ```

  필드를 탭하고 을(를) 선택하여 적응형 양식에 있는 모든 필드의 SOM 표현식을 볼 수 있습니다. **[!UICONTROL SOM 표현식 보기]**.

  ![사용자 지정 오류 처리기의 오류 응답을 표시하는 적응형 양식 필드의 일부 표현식](/help/forms/using/assets/custom-error-handler-somexpression.png)

+++


+++ 적응형 양식 dataRef 속성 기반

* **`Header:`** `content-type:application/problem+json`
* **`Response:`**

  ```javascript
      {
          "type": "VALIDATION_ERROR",
          "validationErrors": [
          {
              "fieldName": "",
              "dataRef": "/Pet/id",
              "details": [
              "Invalid ID supplied. Provided value is not correct!"
              ]
              }
      ]}
  ```

  ![사용자 지정 오류 처리기에서 오류 응답을 표시하는 적응형 양식 필드의 데이터 참조](/help/forms/using/assets/custom-errorhandler-dataref.png)

에서 dataRef의 값을 볼 수 있습니다. **[!UICONTROL 속성]** 양식 구성 요소 창

+++

## 사전 요구 사항 {#prerequisites}

적응형 Forms에서 사용자 지정 오류 핸들러를 사용하기 전에

* 에 대한 기본 지식 [사용자 지정 함수 만들기](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/adaptive-forms/custom-functions-aem-forms.html?lang=en#:~:text=AEM%20Forms%206.5%20introduced%20the,use%20them%20across%20multiple%20forms.).
* 의 최신 릴리스 설치 [Apache Maven](https://maven.apache.org/download.cgi).


## 규칙 편집기를 사용하여 오류 처리기 추가 {#add-error-handler-using-rule-editor}

사용 [규칙 편집기의 호출 서비스](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=en#invoke) 작업에서는 적응형 양식에 사용하는 데이터 소스를 기반으로 유효성 검사 기준을 정의합니다. RESTful 웹 서비스를 데이터 소스로 사용하는 경우 Swagger 정의 파일에 유효성 검사 기준을 정의할 수 있습니다. 적응형 Forms에서 오류 처리기 함수와 규칙 편집기를 사용하면 오류 처리를 효과적으로 관리하고 사용자 지정할 수 있습니다. 규칙 편집기를 사용하여 조건을 정의하고, 규칙이 트리거될 때 수행할 작업을 구성합니다. 적응형 양식은 사전 설정된 유효성 검사 기준에 따라 필드에 입력한 내용을 확인합니다. 입력 값이 유효성 검사 기준을 충족하지 않는 경우 오류 메시지가 적응형 양식의 필드 수준에 표시됩니다.

>[!NOTE]
>
> * 규칙 편집기의 서비스 호출 작업에서 오류 처리기를 사용하려면 양식 데이터 모델로 적응형 Forms을 구성하십시오.
> * 오류 응답이 표준 스키마에 있는 경우 필드에 오류 메시지를 표시하도록 기본 오류 핸들러가 제공됩니다. 사용자 지정 오류 처리기 함수에서 기본 오류 처리기를 호출할 수도 있습니다.

규칙 편집기를 사용하여 다음과 같은 작업을 수행할 수 있습니다.

* [기본 오류 처리기 함수 추가](#add-default-errror-handler)
* [사용자 지정 오류 처리기 함수 추가](#add-custom-errror-handler)


### 기본 오류 처리기 함수 추가 {#add-default-errror-handler}

오류 응답이 표준 스키마 또는 서버측 유효성 검사 실패에 있는 경우 필드에 오류 메시지를 표시하는 기본 오류 처리기가 지원됩니다.
을(를) 사용하여 기본 오류 핸들러를 사용하는 방법을 이해하려면 [규칙 편집기의 호출 서비스](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=en#invoke) 작업, 두 개의 필드가 있는 간단한 적응형 양식의 예 사용, **Pet ID** 및 **애완동물 이름** 및 의 기본 오류 처리기 사용 **Pet ID** 외부 서비스를 호출하도록 구성된 REST 끝점에서 반환되는 다양한 오류를 확인할 필드(예: ) `200 - OK`,`404 - Not Found`, `400 - Bad Request`. 규칙 편집기의 서비스 호출 작업을 사용하여 기본 오류 처리기를 추가하려면 다음 단계를 실행합니다.

1. 작성 모드에서 적응형 양식을 열고 양식 구성 요소를 선택하고 을 누릅니다 **[!UICONTROL 규칙 편집기]** 규칙 편집기를 엽니다.
1. **[!UICONTROL 만들기]**&#x200B;를 탭합니다.
1. 에서 조건 만들기 **날짜** 규칙 섹션에 자세히 설명되어 있습니다. 예를 들어, **날짜[Pet ID 필드 이름]** 이(가) 변경되었습니다. 다음에서 선택 항목이 변경되었습니다. **상태 선택** 드롭다운 목록입니다.
1. 다음에서 **그러면** 섹션, 선택 **[!UICONTROL 서비스 호출]** 다음에서 **작업 선택** 드롭다운 목록입니다.
1. 선택 **Post 서비스** 및 의 해당 데이터 바인딩 **입력** 섹션. 예를 들어, 유효성을 검사하려면 **Pet ID**, 선택 **Post 서비스** 다음으로: **GET /pet/{petId}** 및 선택 **Pet ID** 다음에서 **입력** 섹션.
1. 에서 데이터 바인딩 선택 **출력** 섹션. 선택 **애완동물 이름** 다음에서 **출력** 섹션.
1. 선택 **[!UICONTROL 기본 오류 처리기]** 다음에서 **오류 처리기** 섹션.
1. **[!UICONTROL 완료]**&#x200B;를 클릭합니다.

![양식의 필드 유효성 검사에 대한 기본 오류 처리기 추가](/help/forms/using/assets/default-error-handler.png)

이 규칙의 결과로 사용자가 입력하는 값은 **Pet ID** 유효성 검사 확인 **애완동물 이름** REST 끝점에서 호출한 외부 서비스 사용. 데이터 소스를 기반으로 한 유효성 검사 기준에 실패하면 필드 수준에 오류 메시지가 표시됩니다.

![오류 응답을 처리하기 위해 양식에 기본 오류 처리기를 추가할 때 기본 오류 메시지를 표시합니다](/help/forms/using/assets/default-error-message.png)

### 사용자 지정 오류 처리기 함수 추가 {#add-custom-errror-handler}

사용자 지정 오류 처리기 함수를 추가하여 다음과 같은 일부 작업을 수행할 수 있습니다.

* 비표준 또는 표준 오류 응답을 사용하는 오류 응답을 처리합니다. 이러한 비표준 오류 응답은 다음을 준수하지 않습니다. [오류 응답의 표준 스키마](#failure-response-format).
* analytics 이벤트를 모든 analytics 플랫폼으로 전송합니다. (예: Adobe Analytics)
* 오류 메시지가 표시된 양식 대화 상자를 표시합니다.

언급된 작업 외에도 사용자 지정 오류 처리기를 사용하여 특정 사용자 요구 사항을 충족하는 사용자 지정된 함수를 실행할 수 있습니다.

사용자 지정 오류 처리기는 외부 서비스에서 반환한 오류에 응답하고 사용자 지정된 응답을 최종 사용자에게 전달하도록 설계된 함수(클라이언트 라이브러리)입니다. 주석이 있는 모든 클라이언트 라이브러리 `@errorHandler` 는 사용자 지정 오류 핸들러 함수로 간주됩니다. 이 주석은에 지정된 오류 처리기 함수를 식별하는 데 도움이 됩니다. `.js` 파일.

을(를) 사용하여 사용자 지정 오류 핸들러를 만들고 사용하는 방법을 이해하려면 [규칙 편집기의 호출 서비스](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=en#invoke) 작업, 두 개의 필드가 있는 적응형 양식의 예를 살펴보겠습니다. **Pet ID** 및 **애완동물 이름** 및 의 사용자 지정 오류 처리기 사용 **Pet ID** 외부 서비스를 호출하도록 구성된 REST 끝점에서 반환되는 다양한 오류를 확인할 필드(예: ) `200 - OK`,`404 - Not Found`, `400 - Bad Request`.

적응형 양식에서 사용자 지정 오류 핸들러를 추가하고 사용하려면 다음 단계를 수행하십시오.

1. [사용자 지정 오류 처리기 만들기](#create-custom-error-message)
1. [규칙 편집기를 사용하여 사용자 지정 오류 핸들러를 구성합니다.](#use-custom-error-handler)

#### 1. 사용자 지정 오류 처리기 만들기 {#create-custom-error-message}

사용자 지정 오류 함수를 만들려면 다음 단계를 수행하십시오.

1. 에 로그인 `http://server:port/crx/de/index.jsp#`.
1. 아래에 폴더 만들기 `/apps` 폴더를 삭제합니다. 예를 들어 이라는 폴더를 만듭니다. `experience-league`.
1. 변경 사항을 저장합니다.
1. 생성된 폴더로 이동하고 유형의 노드를 만듭니다. `cq:ClientLibraryFolder` 다음으로: `clientlibs`.
1. 새로 생성된 로 이동합니다. `clientlibs` 폴더 및 추가 `allowProxy` 및 `categories` 속성:

   ![사용자 지정 라이브러리 노드 속성](/help/forms/using/assets/customlibrary-properties.png)

   >[!NOTE]
   >
   > 대신 모든 이름을 제공할 수 있습니다. `customfunctionsdemo`.

1. 변경 사항을 저장합니다.

1. 라는 폴더 만들기 `js` 다음 아래에 `clientlibs` 폴더를 삭제합니다.
1. 라는 JavaScript 파일 만들기 `functions.js` 다음 아래에 `js` 폴더
1. 라는 파일 만들기 `js.txt` 다음 아래에 `clientlibs` 폴더를 삭제합니다.
1. 변경 사항을 저장합니다.
생성된 폴더 구조는 다음과 같습니다.

   ![클라이언트 라이브러리 폴더 구조를 만들었습니다.](/help/forms/using/assets/customclientlibrary_folderstructure.png)
1. 를 두 번 클릭합니다. `functions.js` 파일을 입력하여 편집기를 엽니다. 이 파일은 사용자 지정 오류 처리기의 코드로 구성됩니다.
다음 코드를 JavaScript 파일에 추가하여 REST 서비스 끝점에서 받은 응답 및 헤더를 브라우저 콘솔에 표시해 보겠습니다.

   ```javascript
       /**
       * Custom Error handler
       * @name customErrorHandler Custom Error Handler Function
       * @errorHandler
       */
       function customErrorHandler(response, headers)
       {
           console.log("Custom Error Handler processing start...");
           console.log("response:"+JSON.stringify(response));
           console.log("headers:"+JSON.stringify(headers));
           guidelib.dataIntegrationUtils.defaultErrorHandler(response, headers);
           console.log("Custom Error Handler processing end...");
       }
   ```

   사용자 지정 오류 처리기에서 기본 오류 처리기를 호출하려면 샘플 코드의 다음 행을 사용합니다.
   `guidelib.dataIntegrationUtils.defaultErrorHandler(response, headers) `


1. 저장 `function.js`.
1. 다음으로 이동 `js.txt` 및 다음 코드를 추가합니다.

   ```javascript
       #base=js
       functions.js
   ```

1. 저장 `js.txt` 파일.

이제 AEM Forms에서 규칙 편집기의 호출 서비스를 사용하여 사용자 지정 오류 핸들러를 구성하고 사용하는 방법을 살펴보겠습니다.

#### 2. 규칙 편집기를 사용하여 사용자 지정 오류 핸들러를 구성합니다 {#use-custom-error-handler}

적응형 양식에서 사용자 지정 오류 처리기를 구현하려면 먼저 클라이언트 라이브러리 이름이 **[!UICONTROL 클라이언트 라이브러리 범주]** 은 의 카테고리 옵션에 지정된 이름과 일치합니다. `.content.xml` 파일.

![적응형 양식 컨테이너 구성에 클라이언트 라이브러리 이름 추가](/help/forms/using/assets/client-library-category-name.png)

이 경우 클라이언트 라이브러리 이름은 다음과 같이 제공됩니다. `customfunctionsdemo` 다음에서 `.content.xml` 파일.

을 사용하여 사용자 지정 오류 핸들러를 사용하려면 **[!UICONTROL 규칙 편집기의 호출 서비스]** 작업:

1. 작성 모드에서 적응형 양식을 열고 양식 구성 요소를 선택하고 을 누릅니다 **[!UICONTROL 규칙 편집기]** 규칙 편집기를 엽니다.
1. **[!UICONTROL 만들기]**&#x200B;를 탭합니다.
1. 에서 조건 만들기 **날짜** 규칙 섹션에 자세히 설명되어 있습니다. 예를 들어 다음과 같은 경우: **[Pet ID 필드 이름]** 이(가) 변경되었습니다. 다음을 선택합니다. **변경됨** 다음에서 **상태 선택** 드롭다운 목록입니다.
1. 다음에서 **그러면** 섹션, 선택 **[!UICONTROL 서비스 호출]** 다음에서 **작업 선택** 드롭다운 목록입니다.
1. 선택 **Post 서비스** 및 의 해당 데이터 바인딩 **입력** 섹션. 예를 들어, 유효성을 검사하려면 **Pet ID**, 선택 **Post 서비스** 다음으로: **GET /pet/{petId}** 및 선택 **Pet ID** 다음에서 **입력** 섹션.
1. 에서 데이터 바인딩 선택 **출력** 섹션. 예를 들어, **애완동물 이름** 다음에서 **출력** 섹션.
1. 선택 **[!UICONTROL 사용자 지정 오류 핸들러]** 다음에서 **[!UICONTROL 오류 처리기]** 섹션.
1. **[!UICONTROL 완료]**&#x200B;를 클릭합니다.

![오류 응답을 처리하기 위해 양식에 사용자 지정 오류 처리기 추가](/help/forms/using/assets/custom-error-handler.png)

이 규칙의 결과로 사용자가 입력하는 값은 **Pet ID** 유효성 검사 확인 **애완동물 이름** REST 끝점에서 호출한 외부 서비스 사용. 데이터 소스를 기반으로 한 유효성 검사 기준에 실패하면 필드 수준에 오류 메시지가 표시됩니다.

![오류 응답을 처리하기 위해 양식에 사용자 지정 오류 처리기 추가](/help/forms/using/assets/custom-error-handler-message.png)

브라우저 콘솔을 열고 REST 서비스 끝점에서 받은 응답과 헤더에서 유효성 검사 오류 메시지를 확인합니다.

사용자 지정 오류 처리기 함수는 오류 응답을 기반으로 모달 대화 상자 표시 또는 Analytics 이벤트 전송과 같은 추가 작업을 실행합니다. 사용자 지정 오류 처리기 함수는 특정 사용자 요구 사항에 맞게 오류 처리를 조정할 수 있는 유연성을 제공합니다.

<!-- 

## Configure Adaptive Form submission to add custom handlers {#configure-adaptive-form-submission}

If the server validation error message does not display in the standard format, you can enable asynchronous submission and add a custom error handler on Adaptive Form submission to convert the message into a standard format.

### Configure asynchronous Adaptive Form submission {#configure-asynchronous-adaptive-form-submission}

Before adding custom handler, you must configure the adaptive form for asynchronous submission. Execute the following steps:

1. In adaptive form authoring mode, select the Form Container object and tap ![adaptive form properties](assets/configure_icon.png) to open its properties.
1. In the **[!UICONTROL Submission]** properties section, enable **[!UICONTROL Use asynchronous submission]**.
1. Select **[!UICONTROL Revalidate on server]** to validate the input field values on server before submission.
1. Select the Submit Action:

    * Select **[!UICONTROL Submit using Form Data Model]** and select the appropriate data model, if you are using RESTful web service based [form data model](work-with-form-data-model.md) as the data source.
    * Select **[!UICONTROL Submit to REST Service endpoint]** and specify the **[!UICONTROL Redirect URL/Path]**, if you are using RESTful web services as the data source.

    ![adaptive form submission properties](assets/af_submission_properties.png)

1. Tap ![Save](assets/save_icon.png) to save the properties.

### Add custom error handler on Adaptive Form submission {#add-custom-error-handler-af-submission}

AEM Forms provides out-of-the-box success and error handlers for form submissions. Handlers are client-side functions that execute based on the server response. When an Adaptive Form is submitted, the data is transmitted to the server for validation, which returns a response to the client with information about the success or error event for the submission. The information is passed as parameters to the relevant handler to execute the function.

Execute the following steps to add custom error handler on Adaptive Form submission:

1. Open an Adaptive Form in authoring mode, select any form object, and tap  to open the rule editor.
1. Select **[!UICONTROL Form]** in the Form Objects tree and tap **[!UICONTROL Create]**.
1. Select **[!UICONTROL Error in Submission]** from the Event drop-down list.
1. Write a rule to convert custom error structure to the standard error structure and tap **[!UICONTROL Done]** to save the rule.

The following is a sample code to convert a custom error structure to the standard error structure:

```javascript
var data = $event.data;
var som_map = {
    "id": "guide[0].guide1[0].guideRootPanel[0].Pet[0].id_1[0]",
    "name": "guide[0].guide1[0].guideRootPanel[0].Pet[0].name_2[0]",
    "status": "guide[0].guide1[0].guideRootPanel[0].Pet[0].status[0]"
};

var errorJson = {};
errorJson.errors = [];

if (data) {
    if (data.originMessage) {
        var errorData;
        try {
            errorData = JSON.parse(data.originMessage);
        } catch (err) {
            // not in json format
        }

        if (errorData) {
            Object.keys(errorData).forEach(function(key) {
                var som_key = som_map[key];
                if (som_key) {
                    var error = {};
                    error.somExpression = som_key;
                    error.errorMessage = errorData[key];
                    errorJson.errors.push(error);
                }
            });
        }
        window.guideBridge.handleServerValidationError(errorJson);
    } else {
        window.guideBridge.handleServerValidationError(data);
    }
}
```

The `var som_map` lists the SOM expression of the Adaptive Form fields that you want to transform into the standard format. You can view the SOM expression of any field in an adaptive form by tapping the field and selecting **[!UICONTROL View SOM Expression]**.

Using this custom error handler, the adaptive form converts the fields listed in `var som_map` to standard error message format. As a result, the validation error messages display at field-level in the adaptive form.

 -->