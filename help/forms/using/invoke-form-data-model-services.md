---
title: 적응형 양식에서 양식 데이터 모델 서비스를 호출하기 위한 API
description: 적응형 양식 필드 내에서 WSDL로 작성된 웹 서비스를 호출하는 데 사용할 수 있는 invokeWebServices API에 대해 설명합니다.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: aa3e50f1-8f5a-489d-a42e-a928e437ab79
feature: Adaptive Forms, Foundation Components
exl-id: cf037174-3153-486f-85b1-c974cd5a1ace
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 10%

---

# 적응형 양식에서 양식 데이터 모델 서비스를 호출하기 위한 API {#api-to-invoke-form-data-model-service-from-adaptive-forms}

<span class="preview"> [새 적응형 양식 만들기](/help/forms/using/create-an-adaptive-form-core-components.md) 또는 [AEM Sites 페이지에 적응형 양식 추가](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) 작업을 할 때 현대적이고 확장 가능한 데이터 캡처 [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)를 사용하는 것이 좋습니다. 이러한 구성 요소는 적응형 양식 만들기 작업이 대폭 개선되어 우수한 사용자 경험을 보장할 수 있게 되었음을 나타냅니다. 이 문서에서는 기초 구성 요소를 사용하여 적응형 양식을 작성하는 이전 접근법에 대해 설명합니다. </span>

## 개요 {#overview}

AEM Forms을 사용하면 양식 작성자가 적응형 양식 필드 내에서 양식 데이터 모델에 구성된 서비스를 호출하여 양식 채우기 경험을 보다 단순화하고 향상시킬 수 있습니다. 데이터 모델 서비스를 호출하려면 비주얼 편집기에서 규칙을 만들거나 `guidelib.dataIntegrationUtils.executeOperation` 의 코드 편집기에서 API [규칙 편집기](/help/forms/using/rule-editor.md).

이 문서는 `guidelib.dataIntegrationUtils.executeOperation` 서비스를 호출하는 API입니다.

## API 사용 {#using-the-api}

다음 `guidelib.dataIntegrationUtils.executeOperation` API는 적응형 양식 필드 내에서 서비스를 호출합니다. API 구문은 다음과 같습니다.

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs)
```

의 구조 `guidelib.dataIntegrationUtils.executeOperation` API는 서비스 작업에 대한 세부 정보를 지정합니다. 구조의 구문은 다음과 같습니다.

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

API 구조는 서비스 작업에 대해 다음 세부 사항을 지정합니다.

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
   <td>양식 데이터 모델의 이름을 포함하는 저장소 경로를 지정합니다.</td>
  </tr>
  <tr>
   <td><code>operationName</code></td>
   <td>실행할 서비스 작업의 이름을 지정합니다.</td>
  </tr>
  <tr>
   <td><code>inputs</code></td>
   <td>하나 이상의 양식 개체를 서비스 작업의 입력 인수에 매핑합니다.</td>
  </tr>
  <tr>
   <td><code>Outputs</code></td>
   <td>하나 이상의 양식 개체를 서비스 작업의 출력 값에 매핑하여 양식 필드를 채웁니다<br /> </td>
  </tr>
  <tr>
   <td><code>success</code></td>
   <td>서비스 작업의 입력 인수를 기준으로 값을 반환합니다. 콜백 함수로 사용되는 선택적 매개 변수입니다.<br /> </td>
  </tr>
  <tr>
   <td><code>failure</code></td>
   <td>성공 콜백 함수가 입력 인수를 기반으로 출력 값을 표시하지 못하는 경우 오류 메시지를 표시합니다. 콜백 함수로 사용되는 선택적 매개 변수입니다.<br /> </td>
  </tr>
 </tbody>
</table>

## 서비스를 호출하는 샘플 스크립트 {#sample-script-to-invoke-a-service}

다음 샘플 스크립트는 `guidelib.dataIntegrationUtils.executeOperation` 를 호출하는 API `getAccountById` 에 구성된 서비스 작업 `employeeAccount` 양식 데이터 모델.

다음 `getAccountById` 작업은 의 값을 가져옵니다. `employeeID` 양식 필드를 다음에 대한 입력으로 `empId` 인수 및 해당 직원의 직원명, 계좌 번호 및 계좌 잔액을 반환합니다. 출력 값은 지정된 양식 필드에 채워집니다. (예: 값: `name` 인수는 `fullName` 양식 요소 및 값 `accountNumber` 의 인수 `account` 양식 요소입니다.

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

## 콜백 함수와 함께 API 사용 {#using-the-api-callback}

다음을 사용하여 양식 데이터 모델 서비스를 호출할 수도 있습니다. `guidelib.dataIntegrationUtils.executeOperation` 콜백 함수를 사용하는 API입니다. API 구문은 다음과 같습니다.

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, callbackFunction)
```

콜백 함수에는 `success` 및 `failure` callback 함수.

### 성공 및 실패 콜백 함수가 있는 샘플 스크립트 {#callback-function-success-failure}

다음 샘플 스크립트는 `guidelib.dataIntegrationUtils.executeOperation` 를 호출하는 API `GETOrder` 에 구성된 서비스 작업 `employeeOrder` 양식 데이터 모델.

다음 `GETOrder` 작업은 의 값을 가져옵니다. `Order ID` 양식 필드를 다음에 대한 입력으로 `orderId` 인수 및 반환 주문 수량 값 `success` callback 함수.  다음과 같은 경우 `success` callback 함수는 주문 수량인 `failure` callback 함수는 `Error occured` 메시지.

>[!NOTE]
>
>를 사용하는 경우 `success` callback 함수, 출력 값이 지정된 양식 필드에 채워지지 않습니다.

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
