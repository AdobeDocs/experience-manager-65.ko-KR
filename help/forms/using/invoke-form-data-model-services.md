---
title: 적응형 양식에서 양식 데이터 모델 서비스를 호출하는 API
seo-title: API to invoke form data model service from adaptive forms
description: 적응형 양식 필드 내에서 WSDL로 작성된 웹 서비스를 호출하는 데 사용할 수 있는 invokeWebServices API에 대해 설명합니다.
seo-description: Explains the invokeWebServices API that you can use to invoke web services written in WSDL from within an adaptive form field.
uuid: 40561086-e69d-4e6a-9543-1eb2f54cd836
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: aa3e50f1-8f5a-489d-a42e-a928e437ab79
feature: Adaptive Forms
exl-id: cf037174-3153-486f-85b1-c974cd5a1ace
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---

# 적응형 양식에서 양식 데이터 모델 서비스를 호출하는 API {#api-to-invoke-form-data-model-service-from-adaptive-forms}

## 개요 {#overview}

AEM Forms을 사용하면 양식 작성자가 적응형 양식 필드 내에서 양식 데이터 모델로 구성된 서비스를 호출하여 양식 채우기 경험을 더 단순화하고 향상시킬 수 있습니다. 데이터 모델 서비스를 호출하려면 시각적 편집기에서 규칙을 만들거나 `guidelib.dataIntegrationUtils.executeOperation` 의 코드 편집기에서 API [규칙 편집기](/help/forms/using/rule-editor.md).

이 문서는 `guidelib.dataIntegrationUtils.executeOperation` 서비스를 호출하는 API입니다.

## API 사용 {#using-the-api}

다음 `guidelib.dataIntegrationUtils.executeOperation` API는 적응형 양식 필드 내에서 서비스를 호출합니다. API 구문은 다음과 같습니다.

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs)
```

의 구조 `guidelib.dataIntegrationUtils.executeOperation` API는 서비스 작업에 대한 세부 사항을 지정합니다. 구조의 구문은 다음과 같습니다.

```javascript
var operationInfo = {
formDataModelId,
operationTitle,
operationName
};
var inputs = {
inputField1,
inputFieldN
};
var outputs = {
outputField1,
outputFieldN
}
```

API 구조는 서비스 작업에 대한 다음 세부 사항을 지정합니다.

<table>
 <tbody>
  <tr>
   <th>매개변수</th>
   <th>설명</th>
  </tr>
  <tr>
   <td><code>operationInfo</code></td>
   <td>양식 데이터 모델 식별자, 작업 제목 및 작업 이름을 지정하는 구조</td>
  </tr>
  <tr>
   <td><code>formDataModelId</code></td>
   <td>이름이 포함된 양식 데이터 모델의 저장소 경로를 지정합니다</td>
  </tr>
  <tr>
   <td><code>operationName</code></td>
   <td>실행할 서비스 작업의 이름을 지정합니다</td>
  </tr>
  <tr>
   <td><code>inputs</code></td>
   <td>하나 이상의 양식 개체를 서비스 작업의 입력 인수에 매핑합니다</td>
  </tr>
  <tr>
   <td><code>Outputs</code></td>
   <td>하나 이상의 양식 개체를 서비스 작업의 출력 값에 매핑하여 양식 필드를 채웁니다<br /> </td>
  </tr>
  <tr>
   <td><code>success</code></td>
   <td>서비스 작업의 입력 인수를 기반으로 값을 반환합니다. 콜백 함수로 사용되는 선택적 매개 변수입니다.<br /> </td>
  </tr>
  <tr>
   <td><code>failure</code></td>
   <td>성공 콜백 함수에서 입력 인수를 기반으로 출력 값을 표시하지 못하면 오류 메시지가 표시됩니다. 콜백 함수로 사용되는 선택적 매개 변수입니다.<br /> </td>
  </tr>
 </tbody>
</table>

## 서비스를 호출하는 샘플 스크립트 {#sample-script-to-invoke-a-service}

다음 샘플 스크립트는 `guidelib.dataIntegrationUtils.executeOperation` API를 호출하여 `getAccountById` 에서 구성된 서비스 작업 `employeeAccount` 양식 데이터 모델.

다음 `getAccountById` 작업에서 `employeeID` 양식 필드에 대한 입력으로 `empId` 인수와 해당 직원의 사원 이름, 계정 번호 및 계정 잔액을 반환합니다. 출력 값은 지정된 양식 필드에 입력됩니다. 예를 들어 의 값은 `name` 인수가 `fullName` 양식 요소 및 값 `accountNumber` 주장 `account` 양식 요소를 사용할 수 있습니다.

```javascript
var operationInfo = {
"formDataModelId": "/content/dam/formsanddocuments-fdm/employeeAccount",
"operationName": "getAccountDetails"
};
var inputs = {
"empid" : employeeID
};
var outputs = {
"name" : fullName,
"accountNumber" : account,
"balance" : balance
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
```

## 콜백 함수에서 API 사용 {#using-the-api-callback}

를 사용하여 양식 데이터 모델 서비스를 호출할 수도 있습니다 `guidelib.dataIntegrationUtils.executeOperation` 콜백 함수를 사용하는 API. API 구문은 다음과 같습니다.

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, callbackFunction)
```

콜백 함수에는 `success` 및 `failure` 콜백 함수입니다.

### 성공 및 실패 콜백 함수를 사용하는 샘플 스크립트 {#callback-function-success-failure}

다음 샘플 스크립트는 `guidelib.dataIntegrationUtils.executeOperation` API를 호출하여 `GETOrder` 에서 구성된 서비스 작업 `employeeOrder` 양식 데이터 모델.

다음 `GETOrder` 작업에서 `Order ID` 양식 필드에 대한 입력으로 `orderId` 인수 및 반환 주문 수량 값을 `success` 콜백 함수입니다.  만약 `success` callback 함수는 주문 수량, `failure` 콜백 함수는 `Error occured` 메시지를 표시합니다.

>[!NOTE]
>
> 를 사용하는 경우 `success` 콜백 함수에서 출력 값이 지정된 양식 필드에 채워지지 않습니다.

```javascript
var operationInfo = {
    "formDataModelId": "/content/dam/formsanddocuments-fdm/employeeOrder",
    "operationTitle": "GETOrder",
    "operationName": "GETOrder"
};
var inputs = {
    "orderId" : Order ID
};
var outputs = {};
var success = function (wsdlOutput, textStatus, jqXHR) {
order_quantity.value = JSON.parse(wsdlOutput).quantity;
 };
var failure = function(){
alert('Error occured');
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, success, failure);
```
