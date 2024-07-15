---
title: HTML 5 양식용 양식 Bridge API
description: 외부 애플리케이션은 FormBridge API를 사용하여 XFA Mobile Form에 연결합니다. API는 상위 창에서 FormBridgeInitialized 이벤트를 전달합니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: developer-reference
exl-id: b598ef47-49ff-4806-8cc7-4394aa068eaa
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 0%

---

# HTML 5 양식용 양식 Bridge API {#form-bridge-apis-for-html-forms}

Form Bridge API를 사용하여 XFA 기반 HTML 5 양식과 애플리케이션 간의 통신 채널을 열 수 있습니다. 양식 Bridge API는 연결을 만들기 위한 **연결** API를 제공합니다.

**connect** API는 핸들러를 인수로 허용합니다. XFA 기반 HTML5 양식과 양식 Bridge 간에 성공적으로 연결되면 핸들이 호출됩니다.

다음 샘플 코드를 사용하여 연결을 만들 수 있습니다.

```javascript
// Example showing how to connect to FormBridge
window.addEventListener("FormBridgeInitialized",
                                function(event) {
                                    var fb = event.detail.formBridge;
                                    fb.connect(function() {
                                           //use form bridge functions
                         })
                            })
```

>[!NOTE]
>
>formRuntime.jsp 파일을 포함하기 전에 연결을 만들어야 합니다.

## 사용 가능한 양식 Bridge API  {#available-form-bridge-api-nbsp}

**getBridgeVersion()**

스크립팅 라이브러리의 버전 번호를 반환합니다.

* **입력**: 없음
* **출력**: 스크립팅 라이브러리의 버전 번호입니다
* **오류**: 없음

**isConnected()** 양식 상태가 초기화되었는지 확인합니다.

* **입력**: 없음
* XFA 양식 상태가 초기화된 경우 **출력**: **참**

* **오류**: 없음

**connect(handler, context)** FormBridge에 연결하고 연결이 만들어지고 양식 상태가 초기화된 후 함수를 실행합니다.

* **입력**:

   * **handler**: Form Bridge이 연결된 후 실행할 함수입니다.
   * **context**: *handler* 함수의 컨텍스트(this)가 설정된 개체입니다.

* **출력**: 없음
* **오류**: 없음

**getDataXML(options)** 현재 양식 데이터를 XML 형식으로 반환합니다.

* **입력:**

   * **옵션:** 다음 속성이 포함된 JavaScript 개체:

      * **오류**: 오류 처리기 함수
      * **성공**: 성공 처리기 함수입니다. 이 함수는 *data* 속성에 XML이 포함된 개체를 전달합니다.
      * **context**: *success* 함수의 컨텍스트(this)가 설정된 개체입니다.
      * **validationChecker**: 서버에서 받은 유효성 검사 오류를 확인하기 위해 호출할 함수입니다. 유효성 검사 함수에 일련의 오류 문자열이 전달됩니다.
      * **formState**: 데이터 XML을 반환해야 하는 XFA 양식의 JSON 상태입니다. 지정하지 않으면 현재 렌더링된 양식에 대한 데이터 XML이 반환됩니다.

* **출력:** 없음
* **오류:** 없음

**registerConfig(configName, config)** 사용자/포털별 구성을 FormBridge에 등록합니다. 이러한 구성은 기본 구성을 재정의합니다. 지원되는 구성은 구성 섹션에 지정됩니다.

* **입력:**

   * **configName:** 재정의할 구성의 이름입니다.

      * **widgetConfig:** 사용자가 사용자 정의 위젯으로 양식의 기본 위젯을 재정의할 수 있습니다. 구성은 다음과 같이 재정의됩니다.

        *formBridge.registerConfig(&quot;widgetConfig&quot;:{/&amp;ast;configuration&amp;ast;/})*

      * **pagingConfig:** 사용자가 첫 번째 페이지만 렌더링하는 기본 동작을 재정의할 수 있습니다. 구성은 다음과 같이 재정의됩니다.

        *window.formBridge.registerConfig(&quot;pagingConfig&quot;:{pagingDisabled: &lt;true | false>, shrinkPageDisabled: &lt;true | false> }).*

      * **LoggingConfig:** 사용자가 로깅 수준을 재정의하거나, 범주의 로깅을 사용하지 않도록 설정하거나, 로그 콘솔을 표시할지 또는 서버로 전송할지 여부를 지정할 수 있습니다. 구성은 다음과 같이 재정의할 수 있습니다.

     ```javascript
     formBridge.registerConfig{
       "LoggerConfig" : {
     {
     "on":`<true *| *false>`,
     "category":`<array of categories>`,
     "level":`<level of categories>`, "
     type":`<"console"/"server"/"both">`
     }
       }
     ```

      * **SubmitServiceProxyConfig:** 사용자가 제출 및 로거 프록시 서비스를 등록할 수 있도록 허용합니다.

        ```javascript
        window.formBridge.registerConfig("submitServiceProxyConfig",
        {
        "submitServiceProxy" : "`<submitServiceProxy>`",
        "logServiceProxy": "`<logServiceProxy>`",
        "submitUrl" : "`<submitUrl>`"
        });
        ```

   * 구성의 **config:** 값

* **출력:** *data* 속성에 원래 구성 값이 들어 있는 개체입니다.

* **오류:** 없음

**hideFields(fieldArray)** fieldArray에서 Som 식이 제공되는 필드를 숨깁니다. 지정된 필드의 현재 상태 속성을 invisible로 설정합니다

* **입력:**

   * **fieldArray:** 숨길 필드에 대한 Som 식 배열

* **출력:** 없음
* **오류:** 없음

**showFields(fieldArray)** fieldArray에 Som 식이 제공되는 필드를 표시합니다. 제공된 필드의 현재 상태 속성을 &quot;표시&quot;로 설정합니다.

* **입력:**

   * 표시할 필드에 대한 Som 식의 **fieldArray:** 배열

* **출력:** 없음
* **오류:** 없음

**hideSubmitButtons()** 양식의 모든 제출 단추를 숨깁니다.

* **입력**: 없음
* **출력**: 없음
* **오류**: 양식 상태가 초기화되지 않은 경우 예외를 Throw합니다.

**getFormState()** 양식 상태를 나타내는 JSON을 반환합니다.

* **입력:** 없음
* **출력:** *data* 속성에서 현재 양식 상태를 나타내는 JSON이 포함된 개체입니다.

* **오류:** 없음

**restoreFormState(options)** 옵션 개체에 제공된 JSON 상태에서 양식 상태를 복원합니다. 상태가 적용되며 작업이 완료된 후 성공 또는 오류 핸들러가 호출됩니다

* **입력:**

   * **옵션:** 다음 속성이 포함된 JavaScript 개체:

      * **오류**: 오류 처리기 함수
      * **성공**: 성공 처리기 함수
      * **context**: *success* 함수의 컨텍스트(this)가 설정된 개체입니다.
      * **formState**: 양식의 JSON 상태입니다. 양식이 JSON 상태로 복원됩니다.

* **출력:** 없음
* **오류:** 없음

**setFocus(som)** Som 식에 지정된 필드에 포커스를 설정합니다.

* 포커스를 설정할 필드의 **입력:** Som 식
* **출력:** 없음
* **오류:** 잘못된 Som 식이 있는 경우 예외를 발생시킵니다.

**setFieldValue(som, value)** 지정된 Som 식에 대한 필드의 값을 설정합니다.

* **입력:**

   * **som:** 필드의 Som 식을 포함하는 배열입니다. 필드의 값을 설정하는 som 식입니다.
   * **value:** 배열에 **som** 배열에서 제공된 Som 식에 해당하는 값이 들어 있습니다. 값의 데이터 유형이 fieldType과 동일하지 않으면 값이 수정되지 않습니다.

* **출력:** 없음
* **오류:** 잘못된 Som 식이 있는 경우 예외를 발생시킵니다.

**getFieldValue(som)** 지정된 Som 식에 대한 필드 값을 반환합니다.

* **입력:** 값을 검색해야 하는 필드의 일부 식을 포함하는 배열입니다.
* **Output:** 개체에서 **data** 속성에 배열 결과를 포함합니다.

* **오류:** 없음

### getFieldValue() API의 예 {#example-of-nbsp-getfieldvalue-api}

```JavaScript
var a =  formBridge.getFieldValue("xfa.form.form1.Subform1.TextField");
if(a.errors) {
    var err;
     while((err = a.getNextMessage()) != null)
               alert(a.message)
} else {
   alert(a.data[0])
}
```

**getFieldProperties(som, property)** Som 식에 지정된 필드의 지정된 속성에 대한 값 목록을 검색합니다.

* **입력:**

   * **som:** 필드에 대한 Som 식을 포함하는 배열입니다.
   * **property**: 값이 필요한 속성의 이름

* **출력:** *data* 속성에 배열 결과를 포함하는 개체

* **오류:** 없음

**setFieldProperties(som, property, values)** Som 식에 지정된 모든 필드에 대해 지정된 속성의 값을 설정합니다

* **입력:**

   * **som:** 값을 설정해야 하는 필드의 Som 식이 포함된 배열입니다.
   * **property**: 값을 설정해야 하는 속성입니다.
   * **값:** Som 식에 지정된 필드에 대해 지정된 속성의 값을 포함하는 배열입니다.

* **출력:** 없음
* **오류:** 없음

## 양식 Bridge API의 샘플 사용 {#sample-usage-of-form-bridge-api}

```JavaScript
// Example 1: FormBridge.restoreFormState
  function loadFormState() {
    var suc = function(obj) {
             //success
            }
    var err = function(obj) {
           while(var t = obj.getNextMessage()) {
         $("#errorDiv").append("<div>"+t.message+"</div>");
           }
           }
        var _formState = // load form state from storage
    formBridge.restoreFormState({success:suc,error:err,formState:_formState}); // not passing a context means that this will be formBridge itself. Validation errors will be checked.
  }

//--------------------------------------------------------------------------------------------------

//Example 2: FormBridge.submitForm
  function SubmitForm() {
    var suc = function(obj) {
             var data = obj.data;
         // submit the data to a url;
            }
    var err = function(obj) {
           while(var t = obj.getNextMessage()) {
         $("#errorDiv").append("<div>"+t.message+"</div>");
           }
           }
    formBridge.submitForm({success:suc,error:err}); // not passing a context means that this will be formBridge itself. Validation errors will be checked.
  }
```
