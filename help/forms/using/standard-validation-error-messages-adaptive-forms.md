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
source-git-commit: cd6d9b4d019e24002e4fe1cc8679d270b24c2934
workflow-type: tm+mt
source-wordcount: '1131'
ht-degree: 0%

---

# 적응형 양식에 대한 표준 유효성 검사 오류 메시지 {#standard-validation-error-messages}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM 6.5 | 이 문서 |
| AEM as a Cloud Service | [여기를 클릭하십시오.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/add-custom-error-handler-adaptive-forms.html) |

적응형 양식은 사전 설정된 유효성 검사 기준에 따라 필드에 입력한 내용을 확인합니다. 유효성 검사 기준은 적응형 양식의 필드에 입력할 수 있는 입력 값을 나타냅니다. 적응형 양식에 사용하는 데이터 소스를 기반으로 유효성 검사 기준을 설정할 수 있습니다. 예를 들어 RESTful 웹 서비스를 데이터 소스로 사용하는 경우 Swagger 정의 파일에 유효성 검사 기준을 정의할 수 있습니다.

입력 값이 유효성 검사 기준을 충족하면 해당 값이 데이터 소스에 제출됩니다. 그렇지 않으면 적응형 양식에 오류 메시지가 표시됩니다.

이 접근 방식과 마찬가지로 이제 적응형 양식을 사용자 정의 서비스와 통합하여 데이터 유효성 검사를 수행할 수 있습니다. 입력 값이 유효성 검사 기준을 충족하지 않고 서버가 반환하는 유효성 검사 오류 메시지가 표준 메시지 형식이면 오류 메시지가 양식의 필드 수준에서 표시됩니다.

입력 값이 유효성 검사 기준을 충족하지 않고 서버 유효성 검사 오류 메시지가 표준 메시지 형식이 아닌 경우 적응형 양식은 유효성 검사 오류 메시지를 표준 형식으로 변환하여 양식의 필드 수준에서 표시할 수 있는 메커니즘을 제공합니다. 다음 두 가지 방법 중 하나를 사용하여 오류 메시지를 표준 형식으로 변환할 수 있습니다.

* 적응형 양식 제출에 사용자 정의 오류 핸들러 추가
* 규칙 편집기를 사용하여 서비스 작업을 호출하는 사용자 지정 처리기 추가

이 문서에서는 유효성 검사 오류 메시지의 표준 형식과 오류 메시지를 사용자 지정에서 표준 형식으로 변환하는 방법에 대해 설명합니다.

## 표준 유효성 검사 오류 메시지 형식 {#standard-validation-message-format}

서버 유효성 검사 오류 메시지가 다음 표준 형식인 경우 적응형 양식에 필드 수준에서 오류가 표시됩니다.

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
* `errors` 유효성 검사 오류 메시지와 함께 유효성 검사 기준에 실패한 필드의 SOM 표현식 언급
* `originCode` 외부 서비스에서 반환한 오류 코드를 포함합니다.
* `originMessage` 외부 서비스에서 반환한 원시 오류 데이터를 포함합니다.

## 사용자 지정 처리기를 추가하도록 적응형 양식 제출 구성 {#configure-adaptive-form-submission}

서버 유효성 검사 오류 메시지가 표준 형식으로 표시되지 않는 경우 비동기 제출을 활성화하고 적응형 양식 제출에 사용자 지정 오류 핸들러를 추가하여 메시지를 표준 형식으로 변환할 수 있습니다.

### 비동기 적응형 양식 제출 구성 {#configure-asynchronous-adaptive-form-submission}

사용자 지정 처리기를 추가하기 전에 비동기 제출을 위한 적응형 양식을 구성해야 합니다. 다음 단계를 실행합니다.

1. 적응형 양식 작성 모드에서 양식 컨테이너 개체를 선택하고 을 누릅니다 ![적응형 양식 속성](assets/configure_icon.png) 속성을 엽니다.
1. 다음에서 **[!UICONTROL 제출]** 속성 섹션, 활성화 **[!UICONTROL 비동기 제출 사용]**.
1. 선택 **[!UICONTROL 서버에서 다시 유효성 검사]** 제출 전에 서버의 입력 필드 값을 확인합니다.
1. 제출 액션을 선택합니다.

   * 선택 **[!UICONTROL 양식 데이터 모델을 사용하여 제출]** RESTful 웹 서비스 기반 을 사용하는 경우 적절한 데이터 모델을 선택합니다 [양식 데이터 모델](work-with-form-data-model.md) 를 데이터 소스로 사용합니다.
   * 선택 **[!UICONTROL REST 끝점에 제출]** 및 지정 **[!UICONTROL 리디렉션 URL/경로]** RESTful 웹 서비스를 데이터 소스로 사용하는 경우 입니다.

   ![적응형 양식 제출 속성](assets/af_submission_properties.png)

1. 누르기 ![저장](assets/save_icon.png) 속성을 저장합니다.

### 적응형 양식 제출에 사용자 정의 오류 핸들러 추가 {#add-custom-error-handler-af-submission}

AEM Forms은 양식 제출을 위해 기본 성공 및 오류 핸들러를 제공합니다. 핸들러는 서버 응답을 기반으로 실행되는 클라이언트측 함수입니다. 양식을 제출하면 유효성 검사를 위해 데이터가 서버로 전송되며, 이 서버는 제출에 대한 성공 또는 오류 이벤트에 대한 정보와 함께 응답을 클라이언트에 반환합니다. 정보는 관련 핸들러에 매개 변수로 전달되어 함수를 실행합니다.

다음 단계를 실행하여 적응형 양식 제출 시 사용자 지정 오류 핸들러를 추가합니다.

1. 작성 모드에서 적응형 양식을 열고 양식 개체를 선택한 다음 을 누릅니다 <!--![Rule Editor](assets/af_edit_rules.png)--> 규칙 편집기를 엽니다.
1. 선택 **[!UICONTROL 양식]** 양식 개체 트리에서 다음을 누릅니다 **[!UICONTROL 만들기]**.
1. 선택 **[!UICONTROL 제출 중 오류]** 이벤트 드롭다운 목록에서 선택합니다.
1. 사용자 지정 오류 구조를 표준 오류 구조로 변환하는 규칙을 작성하고 탭합니다. **[!UICONTROL 완료]** 을 눌러 규칙을 저장합니다.

다음은 사용자 지정 오류 구조를 표준 오류 구조로 변환하는 샘플 코드입니다.

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

다음 `var som_map` 표준 형식으로 변환할 적응형 양식 필드의 SOM 식을 나열합니다. 필드를 탭하고 을(를) 선택하여 적응형 양식으로 필드의 SOM 표현식을 볼 수 있습니다 **[!UICONTROL SOM 표현식 보기]**.

이 사용자 지정 오류 핸들러를 사용하여에 나열된 필드를 적응형 양식에서 변환합니다. `var som_map` 표준 오류 메시지 형식으로 변환. 그 결과, 유효성 검사 오류 메시지는 적응형 양식의 필드 수준에서 표시됩니다.

## 서비스 호출 작업을 사용하여 사용자 지정 처리기 추가

다음 단계를 실행하여 오류 처리기를 추가하여 사용자 지정 오류 구조를 표준 오류 구조로 변환합니다. [규칙 편집기](rule-editor.md) 서비스 호출 작업:

1. 작성 모드에서 적응형 양식을 열고 양식 개체를 선택한 다음 을 누릅니다 ![규칙 편집기](assets/rule_editor_icon.png) 규칙 편집기를 엽니다.
1. 누르기 **[!UICONTROL 만들기]**.
1. 에서 조건 만들기 **[!UICONTROL 날짜]** 규칙 섹션에 자세히 설명되어 있습니다. 예를 들어 다음과 같은 경우:[필드 이름] 이(가) 변경되었습니다. 선택 **[!UICONTROL 변경됨]** 다음에서 **[!UICONTROL 상태 선택]** 드롭다운 목록을 통해 이 조건을 달성할 수 있습니다.
1. 다음에서 **[!UICONTROL 그러면]** 섹션, 선택 **[!UICONTROL 서비스 호출]** 다음에서 **[!UICONTROL 작업 선택]** 드롭다운 목록입니다.
1. 에서 Post 서비스 및 해당 데이터 바인딩을 선택합니다. **[!UICONTROL 입력]** 섹션. 예를 들어 을 검증하려는 경우 **이름**, **ID**, 및 **상태** 적응형 양식에서 pet(게시물 서비스)를 선택하고 다음에서 pet.name, pet.id 및 pet.status를 선택합니다 **[!UICONTROL 입력]** 섹션.

이 규칙의 결과로, 사용자가 입력하는 값은 **이름**, **ID**, 및 **상태** 2단계에서 정의된 필드가 변경되고 양식에서 필드 밖으로 탭하면 필드의 유효성이 검사됩니다.

1. 선택 **[!UICONTROL 코드 편집기]** 모드 선택 드롭다운 목록에서 선택합니다.
1. 누르기 **[!UICONTROL 코드 편집]**.
1. 기존 코드에서 다음 줄을 삭제합니다.

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
   ```

1. 사용자 지정 오류 구조를 표준 오류 구조로 변환하는 규칙을 작성하고 탭합니다. **[!UICONTROL 완료]** 을 눌러 규칙을 저장합니다.
예를 들어 끝에 다음 샘플 코드를 추가하여 사용자 지정 오류 구조를 표준 오류 구조로 변환합니다.

   ```javascript
   var errorHandler = function(jqXHR, data) {
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
   };
   
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, null, errorHandler);
   ```

   다음 `var som_map` 표준 형식으로 변환할 적응형 양식 필드의 SOM 식을 나열합니다. 필드를 탭하고 을(를) 선택하여 적응형 양식으로 필드의 SOM 표현식을 볼 수 있습니다 **[!UICONTROL SOM 표현식 보기]** 출처: **[!UICONTROL 추가 옵션]** (...) 메뉴 아래의 제품에서 사용할 수 있습니다.

   샘플 코드의 다음 행을 사용자 지정 오류 처리기에 복사해야 합니다.

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, null, errorHandler);
   ```

   executeOperation API에는 `null` 및 `errorHandler` 새로운 사용자 지정 오류 핸들러를 기반으로 한 매개 변수.

   이 사용자 지정 오류 핸들러를 사용하여에 나열된 필드를 적응형 양식에서 변환합니다. `var som_map` 표준 오류 메시지 형식으로 변환. 그 결과, 유효성 검사 오류 메시지는 적응형 양식의 필드 수준에서 표시됩니다.
