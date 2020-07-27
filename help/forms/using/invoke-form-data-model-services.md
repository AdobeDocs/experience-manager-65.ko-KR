---
title: 적응형 양식에서 양식 데이터 모델 서비스를 호출하는 API
seo-title: 적응형 양식에서 양식 데이터 모델 서비스를 호출하는 API
description: 응용 양식 필드 내에서 WSDL로 작성된 웹 서비스를 호출하는 데 사용할 수 있는 invokeWebServices API에 대해 설명합니다.
seo-description: 응용 양식 필드 내에서 WSDL로 작성된 웹 서비스를 호출하는 데 사용할 수 있는 invokeWebServices API에 대해 설명합니다.
uuid: 40561086-e69d-4e6a-9543-1eb2f54cd836
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: aa3e50f1-8f5a-489d-a42e-a928e437ab79
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 0%

---


# 적응형 양식에서 양식 데이터 모델 서비스를 호출하는 API {#api-to-invoke-form-data-model-service-from-adaptive-forms}

## 개요 {#overview}

양식 작성자는 AEM Forms을 사용하여 적응형 양식 필드 내에서 양식 데이터 모델에 구성된 서비스를 호출하여 양식 채우기 환경을 더 단순화하고 향상시킬 수 있습니다. 데이터 모델 서비스를 호출하려면 시각적 편집기에서 규칙을 만들거나 `guidelib.dataIntegrationUtils.executeOperation` 규칙 편집기의 코드 편집기에서 [API를 사용하여 JavaScript를 지정할 수 있습니다](/help/forms/using/rule-editor.md).

이 문서에서는 API를 사용하여 서비스를 호출하는 `guidelib.dataIntegrationUtils.executeOperation` JavaScript를 작성하는 데 중점을 둡니다.

## API 사용 {#using-the-api}

API는 응용 양식 필드 내에서 서비스를 호출합니다. `guidelib.dataIntegrationUtils.executeOperation` API 구문은 다음과 같습니다.

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs)
```

API의 구조는 `guidelib.dataIntegrationUtils.executeOperation` 서비스 작업에 대한 세부 사항을 지정합니다. 구조의 구문은 다음과 같습니다.

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

API 구조는 서비스 작업에 대해 다음과 같은 세부 사항을 지정합니다.

<table>
 <tbody>
  <tr>
   <th>매개 변수</th>
   <th>설명</th>
  </tr>
  <tr>
   <td><code>operationInfo</code></td>
   <td>양식 데이터 모델 식별자, 작업 제목 및 작업 이름을 지정하는 구조</td>
  </tr>
  <tr>
   <td><code>formDataModelId</code></td>
   <td>양식 데이터 모델의 이름을 포함하는 저장소 경로를 지정합니다.</td>
  </tr>
  <tr>
   <td><code>operationName</code></td>
   <td>실행할 서비스 작업의 이름을 지정합니다.</td>
  </tr>
  <tr>
   <td><code>inputs</code></td>
   <td>하나 이상의 양식 개체를 서비스 작업의 입력 인수에 매핑</td>
  </tr>
  <tr>
   <td><code>Outputs</code></td>
   <td>하나 이상의 양식 객체를 서비스 작업에서 출력 값으로 매핑하여 양식 필드 채우기<br /> </td>
  </tr>
  <tr>
   <td><code>success</code></td>
   <td>서비스 작업의 입력 인수를 기반으로 값을 반환합니다. 콜백 함수로 사용되는 선택적 매개 변수입니다.<br /> </td>
  </tr>
  <tr>
   <td><code>failure</code></td>
   <td>성공 콜백 함수에 입력 인수를 기반으로 출력 값이 표시되지 않으면 오류 메시지가 표시됩니다. 콜백 함수로 사용되는 선택적 매개 변수입니다.<br /> </td>
  </tr>
 </tbody>
</table>

## 서비스를 호출하는 샘플 스크립트 {#sample-script-to-invoke-a-service}

다음 샘플 스크립트에서는 `guidelib.dataIntegrationUtils.executeOperation` API를 사용하여 양식 데이터 모델에 구성된 `getAccountById` 서비스 작업을 `employeeAccount` 호출합니다.

공정 `getAccountById` 은 인수 입력으로 `employeeID` 양식 필드의 값을 `empId` 가져와서 해당 사원의 사원명, 계정 번호 및 계정 잔액을 반환합니다. 출력 값은 지정된 양식 필드에 채워집니다. 예를 들어, 인수 `name` 의 값은 양식 요소 `fullName` 에서 채워지고 양식 요소의 `accountNumber` 인수에 대한 값이 `account` 채워집니다.

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

콜백 함수와 함께 `guidelib.dataIntegrationUtils.executeOperation` API를 사용하여 양식 데이터 모델 서비스를 호출할 수도 있습니다. API 구문은 다음과 같습니다.

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, callbackFunction)
```

콜백 함수에는 `success` 및 `failure` 콜백 함수가 있을 수 있습니다.

### 성공 및 실패 콜백 함수가 있는 샘플 스크립트 {#callback-function-success-failure}

다음 샘플 스크립트에서는 `guidelib.dataIntegrationUtils.executeOperation` API를 사용하여 양식 데이터 모델에 구성된 `GETOrder` 서비스 작업을 `employeeOrder` 호출합니다.

이 `GETOrder` 작업은 `Order ID` 양식 필드의 값을 인수용 입력으로 가져와서 콜백 함수에서 주문 수량 값을 `orderId` `success` 반환합니다.  콜백 `success` 함수에서 주문 수량을 반환하지 않으면 `failure` 콜백 함수에 `Error occured` 메시지가 표시됩니다.

>[!NOTE]
>
> 콜백 함수를 사용하는 경우 `success` 출력 값이 지정된 양식 필드에 채워지지 않습니다.

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
