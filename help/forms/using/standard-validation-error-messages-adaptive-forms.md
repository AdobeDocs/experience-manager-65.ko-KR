---
title: 적응형 양식에 대한 표준 유효성 검사 오류 메시지
seo-title: Standard validation error messages for adaptive forms
description: 사용자 정의 오류 핸들러를 사용하여 적응형 양식의 유효성 검사 오류 메시지를 표준 형식으로 변환합니다
seo-description: Transform the validation error messages for adaptive forms into standard format using custom error handlers
uuid: 0d1f9835-3e28-41d3-a3b1-e36d95384328
contentOwner: anujkapo
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
discoiquuid: ec062567-1c6b-497b-a1e7-1dbac2d60852
feature: Adaptive Forms
exl-id: 54a76d5c-d19b-4026-b71c-7b9e862874bc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1108'
ht-degree: 0%

---

# 적응형 양식에 대한 표준 유효성 검사 오류 메시지 {#standard-validation-error-messages}

적응형 양식은 사전 설정된 유효성 검사 기준을 기반으로 필드에 제공하는 입력의 유효성을 검사합니다. 유효성 검사 기준은 적응형 양식의 필드에 허용되는 입력 값을 나타냅니다. 적응형 양식과 함께 사용하는 데이터 소스를 기반으로 유효성 검사 기준을 설정할 수 있습니다. 예를 들어 RESTful 웹 서비스를 데이터 소스로 사용하는 경우 Swagger 정의 파일에 유효성 검사 기준을 정의할 수 있습니다.

입력 값이 유효성 검사 기준을 충족하면 값이 데이터 소스에 제출됩니다. 그렇지 않으면 적응형 양식에 오류 메시지가 표시됩니다.

이 방법과 유사하게, 이제 적응형 양식을 사용자 지정 서비스와 통합하여 데이터 유효성 검사를 수행할 수 있습니다. 입력 값이 유효성 검사 기준을 충족하지 않고 서버에서 반환하는 유효성 검사 오류 메시지가 표준 메시지 형식인 경우 오류 메시지가 양식의 필드 수준에서 표시됩니다.

입력 값이 유효성 검사 기준을 충족하지 않고 서버 유효성 검사 오류 메시지가 표준 메시지 형식이 아닌 경우 적응형 양식은 유효성 검사 오류 메시지를 표준 형식으로 변환하여 양식의 필드 수준에서 표시할 수 있는 메커니즘을 제공합니다. 다음 두 가지 방법 중 하나를 사용하여 오류 메시지를 표준 형식으로 변환할 수 있습니다.

* 적응형 양식 제출 시 사용자 지정 오류 처리기 추가
* 규칙 편집기를 사용하여 서비스 호출 작업에 사용자 지정 핸들러를 추가합니다

이 문서에서는 유효성 검사 오류 메시지에 대한 표준 형식 및 오류 메시지를 사용자 지정에서 표준 형식으로 변환하는 지침에 대해 설명합니다.

## 표준 유효성 검사 오류 메시지 형식 {#standard-validation-message-format}

서버 유효성 검사 오류 메시지가 다음과 같은 표준 형식인 경우 적응형 양식에 필드 수준에서 오류가 표시됩니다.

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
* `errors` 검증 오류 메시지와 함께 유효성 검사 기준에 실패한 필드의 SOM 식 언급
* `originCode` 외부 서비스에서 반환한 오류 코드를 포함합니다
* `originMessage` 외부 서비스에서 반환한 원시 오류 데이터를 포함합니다

## 사용자 지정 핸들러를 추가하도록 적응형 양식 제출 구성 {#configure-adaptive-form-submission}

서버 유효성 검사 오류 메시지가 표준 형식으로 표시되지 않으면 비동기 제출을 활성화하고 적응형 양식 제출 시 사용자 지정 오류 핸들러를 추가하여 메시지를 표준 형식으로 변환할 수 있습니다.

### 비동기 적응형 양식 제출 구성 {#configure-asynchronous-adaptive-form-submission}

사용자 지정 핸들러를 추가하기 전에 비동기 전송을 위해 적응형 양식을 구성해야 합니다. 다음 단계를 실행합니다.

1. 적응형 양식 작성 모드에서 양식 컨테이너 개체를 선택하고 ![적응형 양식 속성](assets/configure_icon.png) 속성을 엽니다.
1. 에서 **[!UICONTROL 제출]** 속성 섹션, 활성화 **[!UICONTROL 비동기 제출 사용]**.
1. 선택 **[!UICONTROL 서버에서 유효성 검사]** 제출하기 전에 서버의 입력 필드 값을 확인하려면 다음을 수행하십시오.
1. 제출 작업을 선택합니다.

   * 선택 **[!UICONTROL 양식 데이터 모델을 사용하여 제출]** RESTful 웹 서비스를 사용하는 경우 적절한 데이터 모델을 선택합니다 [양식 데이터 모델](work-with-form-data-model.md) 를 사용하십시오.
   * 선택 **[!UICONTROL REST 엔드포인트에 제출]** 그리고 **[!UICONTROL 리디렉션 URL/경로]**&#x200B;를 설정하는 것이 좋습니다.

   ![적응형 양식 제출 속성](assets/af_submission_properties.png)

1. 탭 ![저장](assets/save_icon.png) 속성을 저장합니다.

### 적응형 양식 제출 시 사용자 지정 오류 처리기 추가 {#add-custom-error-handler-af-submission}

AEM Forms은 양식 제출을 위한 기본 성공 및 오류 핸들러를 제공합니다. 핸들러는 서버 응답을 기반으로 실행되는 클라이언트측 함수입니다. 양식이 제출되면 데이터가 서버에 전송되어 유효성 검사를 위해 서버에 전송되며, 클라이언트에게 전송하기 위해 성공 또는 오류 이벤트에 대한 정보를 제공합니다. 이 정보는 함수를 실행하기 위해 관련 처리기에 매개 변수로 전달됩니다.

다음 단계를 실행하여 적응형 양식 제출 시 사용자 지정 오류 핸들러를 추가합니다.

1. 작성 모드에서 적응형 양식을 열고 양식 개체를 선택한 다음 <!--![Rule Editor](assets/af_edit_rules.png)--> 규칙 편집기를 엽니다.
1. 선택 **[!UICONTROL 양식]** 양식 객체 트리에서 **[!UICONTROL 만들기]**.
1. 선택 **[!UICONTROL 제출 오류]** 이벤트 드롭다운 목록에서 를 선택합니다.
1. 규칙을 작성하여 사용자 지정 오류 구조를 표준 오류 구조로 변환한 다음 탭합니다. **[!UICONTROL 완료]** 규칙을 저장하려면 을 클릭합니다.

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

다음 `var som_map` 표준 형식으로 변환할 적응형 양식 필드의 SOM 표현식을 나열합니다. 필드를 탭하고 을(를) 선택하여 적응형 양식의 모든 필드의 SOM 표현식을 볼 수 있습니다 **[!UICONTROL SOM 표현식 보기]**.

이 사용자 지정 오류 핸들러를 사용하여 적응형 양식은 다음에 나열된 필드를 변환합니다 `var som_map` 표준 오류 메시지 형식으로 변환. 따라서 유효성 검사 오류 메시지는 적응형 양식의 필드 수준에서 표시됩니다.

## 서비스 호출 작업을 사용하여 사용자 지정 처리기 추가

다음 단계를 실행하여 사용자 지정 오류 구조를 [규칙 편집기의](rule-editor.md) 서비스 호출 작업:

1. 작성 모드에서 적응형 양식을 열고 양식 개체를 선택한 다음 ![규칙 편집기](assets/rule_editor_icon.png) 규칙 편집기를 엽니다.
1. 탭 **[!UICONTROL 만들기]**.
1. 에서 조건 만들기 **[!UICONTROL When]** 섹션에 있는 마지막 항목이 될 필요가 없습니다. 예를 들어[필드 이름] 가 변경되었습니다. 선택 **[!UICONTROL 가 변경되었습니다.]** 에서 **[!UICONTROL 상태 선택]** 드롭다운 목록에서 이러한 조건을 충족합니다.
1. 에서 **[!UICONTROL Then]** 섹션, **[!UICONTROL 서비스 호출]** 에서 **[!UICONTROL 작업 선택]** 드롭다운 목록.
1. Post 서비스와 해당 데이터 바인딩을 **[!UICONTROL 입력]** 섹션을 참조하십시오. 예를 들어 유효성을 검사하려는 경우 **이름**, **ID**, 및 **상태** 적응형 양식의 필드에서 post 서비스(pet)를 선택하고 pet.name, pet.id 및 pet.status를 선택합니다 **[!UICONTROL 입력]** 섹션을 참조하십시오.

이 규칙의 결과로 사용자가 입력하는 값 **이름**, **ID**, 및 **상태** 2단계에서 정의한 필드가 변경되고 양식의 필드 바깥으로 탭이 처리되면 필드의 유효성이 확인됩니다.

1. 선택 **[!UICONTROL 코드 편집기]** 모드 선택 드롭다운 목록에서
1. 탭 **[!UICONTROL 코드 편집]**.
1. 기존 코드에서 다음 줄을 삭제합니다.

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
   ```

1. 규칙을 작성하여 사용자 지정 오류 구조를 표준 오류 구조로 변환한 다음 탭합니다. **[!UICONTROL 완료]** 규칙을 저장하려면 을 클릭합니다.
예를 들어 다음 샘플 코드를 끝에 추가하여 사용자 지정 오류 구조를 표준 오류 구조로 변환합니다.

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

   다음 `var som_map` 표준 형식으로 변환할 적응형 양식 필드의 SOM 표현식을 나열합니다. 필드를 탭하고 을(를) 선택하여 적응형 양식의 모든 필드의 SOM 표현식을 볼 수 있습니다 **[!UICONTROL SOM 표현식 보기]** 변환 전: **[!UICONTROL 추가 옵션]** 메뉴...

   다음 샘플 코드 행을 사용자 지정 오류 처리기에 복사해야 합니다.

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, null, errorHandler);
   ```

   executeOperation API에는 `null` 및 `errorHandler` 새 사용자 지정 오류 핸들러를 기반으로 하는 매개 변수입니다.

   이 사용자 지정 오류 핸들러를 사용하여 적응형 양식은 다음에 나열된 필드를 변환합니다 `var som_map` 표준 오류 메시지 형식으로 변환. 따라서 유효성 검사 오류 메시지는 적응형 양식의 필드 수준에서 표시됩니다.
