---
title: 적응형 양식에서 사용자 정의 함수 만들기 및 추가
description: AEM Forms은 사용자가 규칙 편집기 내에서 자체 함수를 만들고 사용할 수 있도록 하는 사용자 지정 함수를 지원합니다.
keywords: 사용자 지정 함수를 추가하고, 사용자 지정 함수를 사용하고, 사용자 지정 함수를 만들고, 규칙 편집기에서 사용자 지정 함수를 사용합니다.
content-type: reference
feature: Adaptive Forms, Core Components
source-git-commit: f633fdfda531cc29ce6274e0367708cc4909a0cd
workflow-type: tm+mt
source-wordcount: '3385'
ht-degree: 2%

---

# 적응형 Forms 핵심 구성 요소의 사용자 정의 기능

이 문서에서는 다음과 같은 최신 기능이 포함된 최신 적응형 양식 핵심 구성 요소로 사용자 정의 기능을 만드는 방법에 대해 설명합니다.
* 사용자 정의 기능을 위한 캐싱 기능
* 사용자 지정 함수에 대한 전역 범위 개체 및 필드 개체 지원
* let 및 arrow 함수와 같은 최신 JavaScript 기능 지원(ES10 지원)

을(를) 설정하십시오. [최신 양식 버전](https://github.com/adobe/aem-core-forms-components/tree/release/650) 사용자 지정 함수의 최신 기능을 사용하려면 AEM Forms 핵심 구성 요소 환경에서 을 참조하십시오. </span>


| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM 6.5 | 이 문서 |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/kr/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/create-and-use-custom-functions) |

## 소개

AEM Forms 6.5에는 규칙 편집기를 사용하여 복잡한 비즈니스 규칙을 정의할 수 있는 JavaScript 함수가 포함되어 있습니다. AEM Forms에서는 다양한 기본 사용자 정의 함수를 제공하지만, 많은 사용 사례에서는 여러 양식에서 사용할 사용자 정의 함수를 정의해야 합니다. 이러한 사용자 지정 기능은 특정 요구 사항을 충족하도록 입력된 데이터를 조작 및 처리할 수 있도록 함으로써 양식의 기능을 향상시킵니다. 또한 사전 정의된 기준에 따라 양식 동작을 동적으로 변경할 수 있습니다.

### 사용자 정의 함수 사용 {#uses-of-custom-function}

적응형 Forms 핵심 구성 요소에서 사용자 지정 기능을 사용할 때의 장점은 다음과 같습니다.


* **데이터 관리**: 사용자 정의 기능은 양식 필드에 입력된 데이터를 관리하고 처리합니다.
* **데이터 처리**: 사용자 정의 기능은 양식 필드에 입력된 데이터를 처리하는 데 도움이 됩니다.
* **데이터 유효성 검사**: 사용자 정의 기능을 사용하면 양식 입력에 대한 사용자 정의 검사를 수행하고 지정된 오류 메시지를 제공할 수 있습니다.
* **동적 동작**: 사용자 정의 기능을 사용하면 특정 조건에 따라 양식의 동적 동작을 제어할 수 있습니다. 예를 들어 필드를 표시/숨기거나, 필드 값을 수정하거나, 양식 논리를 동적으로 조정할 수 있습니다.
* **통합**: 사용자 지정 함수를 사용하여 외부 API 또는 서비스와 통합할 수 있습니다. 외부 소스에서 데이터를 가져오거나 외부 Rest 끝점으로 데이터를 전송하거나 외부 이벤트를 기반으로 사용자 지정 작업을 수행하는 데 도움이 됩니다.

사용자 지정 함수는 기본적으로 JavaScript 파일에 추가되는 클라이언트 라이브러리입니다. 사용자 지정 함수를 만들면 규칙 편집기에서 적응형 양식에서 사용자가 선택할 수 있게 됩니다. 사용자 지정 함수는 규칙 편집기의 JavaScript 주석으로 식별됩니다.

### 사용자 지정 함수에 대해 지원되는 JavaScript 주석 {#js-annotations}

**JavaScript 주석은 JavaScript 코드에 대한 메타데이터를 제공합니다**. 여기에는 다음과 같은 특정 기호로 시작하는 주석이 포함됩니다. `/**` 및 `@`. 주석은 함수, 변수 및 코드의 기타 요소에 대한 중요한 정보를 제공합니다. 적응형 양식은 사용자 정의 기능에 대한 다음 JavaScript 주석을 지원합니다.

#### 이름

다음 **이름** 적응형 양식의 규칙 편집기에서 사용자 지정 기능을 식별하는 데 사용됩니다. 다음 구문을 사용하여 사용자 지정 함수의 이름을 지정합니다.

* `@name [functionName] <Function Name>`
* `@function [functionName] <Function Name>`
* `@func [functionName] <Function Name>`

>[!NOTE]
>`[functionName]` 는 함수의 이름입니다. 공백은 허용되지 않습니다.
>`<Function Name>` 는 적응형 Forms 규칙 편집기에 있는 함수의 표시 이름입니다.
>함수 이름이 함수 자체의 이름과 동일한 경우 를 생략할 수 있습니다 `[functionName]` 구문을 통해 알 수 있습니다.

#### 매개변수

다음 **매개 변수** 는 사용자 지정 함수에서 사용하는 인수 목록입니다. 함수는 여러 매개 변수를 지원할 수 있습니다. 다음 구문을 사용하여 사용자 지정 함수에서 매개 변수를 정의할 수 있습니다.

* `@param {type} name <Parameter Description>`
* `@argument` `{type} name <Parameter Description>`
* `@arg` `{type}` `name <Parameter Description>`

  `{type}` 매개 변수 유형을 나타냅니다. 허용되는 매개 변수 유형은 다음과 같습니다.

   * string: 단일 문자열 값을 나타냅니다.
   * number: 단일 숫자 값을 나타냅니다.
   * 부울: 단일 부울 값(true 또는 false)을 나타냅니다.
   * 문자열[]: 문자열 값의 배열을 나타냅니다.
   * 숫자[]: 숫자 값의 배열을 나타냅니다.
   * 부울[]: 부울 값의 배열을 나타냅니다.
   * date: 단일 날짜 값을 나타냅니다.
   * 날짜[]: 날짜 값의 배열을 나타냅니다.
   * array: 다양한 유형의 값을 포함하는 일반 배열을 나타냅니다.
   * object: 값을 직접 전달하는 대신 사용자 지정 함수에 전달되는 양식 개체를 나타냅니다.
   * 범위: 사용자 지정 함수 내에서 양식 수정을 수행하는 방법, 양식 인스턴스, 대상 필드 인스턴스와 같은 읽기 전용 변수를 포함하는 globals 개체를 나타냅니다. 이 매개 변수는 JavaScript 주석에서 마지막 매개 변수로 선언되며 적응형 양식의 규칙 편집기에 표시되지 않습니다. 범위 매개 변수는 양식 또는 구성 요소의 개체에 액세스하여 양식 처리에 필요한 규칙이나 이벤트를 트리거합니다. Globals 개체 및 사용 방법에 대한 자세한 내용은 [여기를 클릭하십시오](/help/forms/using/create-and-use-custom-functions-core-components.md#field-and-global-scope-objects-in-custom-functions-support-field-and-global-objects)

매개변수 유형은 다음과 같습니다. **대/소문자를 구분하지 않음** 매개 변수 이름에는 및 공백을 사용할 수 없습니다.

`<Parameter Description>` 에는 매개 변수의 용도에 대한 세부 사항이 포함되어 있습니다. 여러 단어가 있을 수 있습니다.

<!--

**Optional Parameters**
By default, all parameters are mandatory. You can define a parameter as optional by either adding `=` after the parameter type or enclosing the parameter name in `[]`. Parameters defined as optional in JavaScript annotations are displayed as optional in the rule editor.
To define a variable as an optional parameter, you can use the any of the following syntaxes:
  
* `@param {type=} Input1`

In the above line of code, `Input1` is an optional parameter without any default value. To declare optional parameter with default value:

`@param {string=<value>} input1`
        
`input1` as an optional parameter with the default value set to `value`. 

* `@param {type} [Input1]`

In the above line of code, `Input1` is an optional parameter without any default value. To declare optional parameter with default value:

`@param {array} [input1=<value>]`

    `input1` is an optional parameter of array type with the default value set to `value`. 
    Ensure that the parameter type is enclosed in curly brackets {} and the parameter name is enclosed in square brackets []. 

Consider the following code snippet, where input2 is defined as an optional parameter:

```javascript

        /**
         * optional parameter function
         * @name OptionalParameterFunction
         * @param {string} input1 
         * @param {string=} input2 
         * @return {string}
        */
        function OptionalParameterFunction(input1, input2) {
        let result = "Result: ";
        result += input1;
        if (input2 !== null) {
            result += " " + input2;
        }
        return result;
        }
```

The following illustration displays using the `OptionalParameterFunction` csutom function in the rule editor:

![Optional or required parameters ](/help/forms/using/assets/optional-default-params.png)

You can save the rule without specifying a value for required parameters, but the rule is not executed and displays a warning message as:

![incomplete rule warning](/help/forms/using/assets/incomplete-rule.png)

When user leaves the optional parameter empty, then the "Undefined" value is passed to the custom function for the optional parameter.

To learn more about how to define optional parameters in JSDocs, [click here](https://jsdoc.app/tags-param).

-->

#### 반환 유형

반환 형식은 사용자 지정 함수가 실행 후 반환하는 값의 형식을 지정합니다. 다음 구문을 사용하여 사용자 지정 함수에서 반환 유형을 정의합니다.

* `@return {type}`
* `@returns {type}`
  `{type}` 함수의 반환 형식을 나타냅니다. 허용되는 반환 유형은 다음과 같습니다.
* string: 단일 문자열 값을 나타냅니다.
* number: 단일 숫자 값을 나타냅니다.
* 부울: 단일 부울 값(true 또는 false)을 나타냅니다.
* 문자열[]: 문자열 값의 배열을 나타냅니다.
* 숫자[]: 숫자 값의 배열을 나타냅니다.
* 부울[]: 부울 값의 배열을 나타냅니다.
* date: 단일 날짜 값을 나타냅니다.
* 날짜[]: 날짜 값의 배열을 나타냅니다.
* array: 다양한 유형의 값을 포함하는 일반 배열을 나타냅니다.
* object: 값 대신 양식 개체를 직접 나타냅니다.

반환 형식은 대/소문자를 구분하지 않습니다.

#### 비공개

private으로 선언된 사용자 지정 함수는 적응형 양식의 규칙 편집기에서 사용자 지정 함수 목록에 표시되지 않습니다. 기본적으로 사용자 지정 함수는 공개입니다. 사용자 지정 함수를 private으로 선언하는 구문은 다음과 같습니다. `@private`.

<!--
#### Member

  Syntax: `@memberof namespace`
  Attaches a namespace to the function.
-->

<!--

#### This

   Syntax: `@this currentComponent`

   Use @this to refer to the Adaptive Form component on which the rule is written. 
  
   The following example is based on the field value. In the following example, the rule hides a field in the form. The `this` portion of `this.value` refers to underlying Adaptive Form component, on which the rule is written.

   ```
      /**
      * @function myTestFunction
      * @this currentComponent
      * @param {scope} scope in which code inside function will be executed.
      */
      myTestFunction = function (scope) {
         if(this.value == "O"){
               scope.age.visible = true;
         } else {
            scope.age.visible = false;
         }
      }

   ```

    >[!NOTE]
    >
    >Comments before custom function are used for summary. Summary can extend to multiple lines until a tag is encountered. Limit the size to a single for a concise description in the rule builder.

-->

<!--

## Function declaration supported types {#function-declaration-supported-types}

**Function Statement**

```javascript
function area(len) {
    return len*len;
}
```

This function is included without `jsdoc` comments.

**Function Expression**

```javascript
var area;
//Some codes later
/** */
area = function(len) {
    return len*len;
};
```

**Function Expression and Statement**

```javascript
var b={};
/** */
b.area = function(len) {
    return len*len;
}
```

**Function Declaration as Variable**

```javascript
/** */
var x1,
    area = function(len) {
        return len*len;
    },
    x2 =5, x3 =true;
```

Limitation: custom function picks only the first function declaration from the variable list, if together. You can use function expression for every function declared.

**Function Declaration as Object**

```javascript
var c = {
    b : {
        /** */
        area : function(len) {
            return len*len;
        }
    }
};
```
-->

## 사용자 정의 함수를 만드는 동안 지침 {#considerations}

규칙 편집기에 사용자 정의 함수를 나열하려면 다음 형식 중 하나를 사용할 수 있습니다.

### jsdoc 주석이 있거나 없는 Function 문

jsdoc 주석을 사용하거나 사용하지 않고 사용자 지정 함수를 만들 수 있습니다.

```javascript
    function functionName(parameters) 
        {
            // code to be executed
        }
```

사용자가 사용자 정의 함수에 JavaScript 주석을 추가하지 않으면 함수 이름으로 규칙 편집기에 나열됩니다. 그러나 사용자 정의 함수의 가독성을 높이기 위해 JavaScript 주석을 포함하는 것이 좋습니다.


### 필수 JavaScript 주석 또는 주석이 있는 화살표 함수

화살표 함수 구문을 사용하여 사용자 지정 함수를 만들 수 있습니다.

```javascript
    /**
    * test function
    * @name testFunction 
    * @param {string} a parameter description
    * @param {string=} b parameter description
    * @return {string}
    */
    testFunction = (a, b) => {
    return a + b;
    };
    /** */
    testFunction1=(a) => (return a)
    /** */
    testFunction2 = a => a + 100;
    
```

사용자가 사용자 정의 함수에 JavaScript 주석을 추가하지 않으면 사용자 정의 함수가 적응형 양식의 규칙 편집기에 나열되지 않습니다.

### 필수 JavaScript 주석 또는 주석이 있는 함수 표현식

적응형 양식의 규칙 편집기에 사용자 정의 함수를 나열하려면 다음 형식으로 사용자 정의 함수를 만듭니다.

```javascript
    /**
    * test function
    * @name testFunction 
    * @param {string} input1 parameter description
    * @param {string=} input2 parameter description
    * @return {string}
    */
    testFunction = function(input1,input2)
        {
            // code to be executed
        }
```

사용자가 사용자 정의 함수에 JavaScript 주석을 추가하지 않으면 사용자 정의 함수가 적응형 양식의 규칙 편집기에 나열되지 않습니다.

### 사용자 지정 함수를 만들기 위한 사전 요구 사항

적응형 Forms에 사용자 정의 기능을 추가하기 전에 시스템에 다음 소프트웨어가 설치되어 있는지 확인하십시오.

* **일반 텍스트 편집기(IDE)**: 모든 일반 텍스트 편집기가 작동할 수 있지만 Microsoft Visual Studio Code와 같은 IDE(통합 개발 환경)는 쉽게 편집할 수 있는 고급 기능을 제공합니다.

* **Git:** 이 버전 제어 시스템은 코드 변경을 관리하는 데 필요합니다. 설치되지 않은 경우 https://git-scm.com에서 다운로드하십시오.


## 사용자 정의 함수 만들기 {#create-custom-function}

사용자 정의 함수를 만드는 단계는 다음과 같습니다.
1. [AEM Project Archetype을 사용하여 클라이언트측 라이브러리를 만들고 사용자 정의 함수 추가](#create-client-library-archetype)
또는
   [CRXDE를 통해 맞춤형 기능 만들기](#create-add-custom-function)
1. [적응형 양식에 클라이언트 라이브러리 추가](#add-client-library)
1. [적응형 양식에서 사용자 정의 함수 사용](#use-custom-functions)


### AEM Project Archetype을 사용하여 클라이언트 라이브러리 만들기{#create-client-library-archetype}

작성된 프로젝트에 클라이언트 라이브러리를 추가하여 사용자 정의 함수를 추가할 수 있습니다 [AEM Project Archetype 사용](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/developing/archetype/using#getting-started).
기존 프로젝트가 있는 경우 <!--and have already the project structure as shown in the image below,--> 직접 추가할 수 있습니다. [사용자 정의 함수](#create-add-custom-function) 을 로컬 프로젝트에 추가합니다.

<!--![custom fuction folder structure](assets/custom-library-folder-structure.png)-->

Archetype 프로젝트를 만들거나 기존 프로젝트를 사용한 후에 클라이언트 라이브러리를 만듭니다. 클라이언트 라이브러리를 만들려면 다음 단계를 수행하십시오.

**클라이언트 라이브러리 폴더 추가**

새 클라이언트 라이브러리 폴더를 [AEM 프로젝트 디렉터리]를 클릭하고 다음 단계를 수행합니다.

1. 를 엽니다. [AEM 프로젝트 디렉터리] 를 입력합니다.

   ![사용자 정의 함수 폴더 구조](assets/custom-library-folder-structure.png)

1. 찾기 `ui.apps`.
1. 새 폴더를 추가합니다. 예를 들어 이라는 폴더를 `experience-league`.
1. 다음으로 이동 `/experience-league/` 폴더 및 추가 `ClientLibraryFolder`. 예를 들어 이라는 클라이언트 라이브러리 폴더를 만듭니다. `customclientlibs`.

   위치: `[AEM project directory]/ui.apps/src/main/content/jcr_root/apps/`

**클라이언트 라이브러리 폴더에 파일 및 폴더 추가**

추가된 클라이언트 라이브러리 폴더에 다음을 추가합니다.

* `.content.xml` 파일
* `js.txt` 파일
* `js` 폴더

`Location is: [AEMaaCS project directory]/ui.apps/src/main/content/jcr_root/apps/experience-league/customclientlibs/`

1. 다음에서 `.content.xml` 다음 코드 행을 추가합니다.

   ```javascript
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
   jcr:primaryType="cq:ClientLibraryFolder"
   categories="[customfunctionscategory]"/>
   ```

   >[!NOTE]
   >
   > 다음에 대한 모든 이름을 선택할 수 있습니다. `client library folder` 및 `categories` 속성.

1. 다음에서 `js.txt` 다음 코드 행을 추가합니다.

   ```javascript
         #base=js
       function.js
   ```

1. 다음에서 `js` 폴더, javascript 파일 추가 `function.js` 사용자 정의 함수를 포함합니다.

   ```javascript
   /**
       * Calculates Age
       * @name calculateAge
       * @param {object} field
       * @return {string} 
   */
   
   function calculateAge(field) {
   var dob = new Date(field);
   var now = new Date();
   
   var age = now.getFullYear() - dob.getFullYear();
   var monthDiff = now.getMonth() - dob.getMonth();
   
   if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
   age--;
   }
   
   return age;
   }
   ```

1. 파일을 저장합니다.

![사용자 정의 함수 폴더 구조](assets/custom-function-added-files.png)

**filter.xml에 새 폴더 포함**:

1. 다음 위치로 이동 `/ui.apps/src/main/content/META-INF/vault/filter.xml` 파일 위치: [AEMaaCS 프로젝트 디렉터리].

1. 파일을 열고 끝에 다음 줄을 추가합니다.

   `<filter root="/apps/experience-league" />`
1. 파일을 저장합니다.

   ![사용자 정의 함수 필터 xml](assets/custom-function-filterxml.png)

1. 에 지정된 단계에 따라 새로 만든 클라이언트 라이브러리 폴더를 AEM 환경에 빌드합니다. [빌드 방법 섹션](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype#how-to-build).

## CRXDE를 통해 사용자 정의 함수 만들기 및 배포{#create-add-custom-function}

최신 AEM Forms 및 Forms 추가 기능을 사용하는 경우 CRXDE를 통해 사용자 정의 함수를 만들어 사용자 정의 함수의 최신 업데이트를 사용할 수 있습니다. 이렇게 하려면 다음 단계를 수행합니다.

<!--![custom fuction folder structure](assets/custom-library-folder-structure.png)-->


1. 에 로그인 `http://server:port/crx/de/index.jsp#`.
1. `/apps` 폴더 아래에 폴더를 만듭니다. 예를 들어 이라는 폴더를 만듭니다. `experience-league`.
1. 변경 사항을 저장합니다.
1. 생성된 폴더로 이동하고 유형의 노드를 만듭니다. `cq:ClientLibraryFolder` 다음으로: `clientlibs`.
1. 새로 생성된 로 이동합니다. `clientlibs` 폴더 및 추가 `allowProxy` 및 `categories` 속성:

   ![사용자 지정 라이브러리 노드 속성](/help/forms/using/assets/customlibrary-catproperties.png)

   >[!NOTE]
   >
   > 대신 모든 이름을 제공할 수 있습니다. `customfunctionsdemo`.

1. 변경 사항을 저장합니다.

1. 라는 폴더 만들기 `js` 다음 아래에 `clientlibs` 폴더를 삭제합니다.
1. 라는 JavaScript 파일 만들기 `functions.js` 다음 아래에 `js` 폴더를 삭제합니다.
1. 라는 파일 만들기 `js.txt` 다음 아래에 `clientlibs` 폴더를 삭제합니다.
1. 변경 사항을 저장합니다.
생성된 폴더 구조 형태는 다음과 같습니다.

   ![클라이언트 라이브러리 폴더 구조가 생성됨](/help/forms/using/assets/clientlibrary_folderstructure.png)
1. 를 두 번 클릭합니다. `functions.js` 파일을 입력하여 편집기를 엽니다. 이 파일은 사용자 지정 함수에 대한 코드로 구성됩니다.
JavaScript 파일에 다음 코드를 추가하여 생년월일(YYYY-MM-DD)을 기준으로 연령을 계산해 보겠습니다.

   ```javascript
       /**
            * Calculates Age
            * @name calculateAge 
            * @return {string} 
       */
   
       function calculateAge(dateOfBirthString) {
       var dob = new Date(dateOfBirthString);
       var now = new Date();
   
       var age = now.getFullYear() - dob.getFullYear();
       var monthDiff = now.getMonth() - dob.getMonth();
   
       if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
       age--;
       }
   
       return age;
       }
   ```

1. 저장 `function.js`.
1. 다음으로 이동 `js.txt` 및 다음 코드를 추가합니다.

   ```javascript
       #base=js
       functions.js
   ```

1. `js.txt` 파일을 저장합니다.

다음을 참조하십시오 [사용자 정의 함수](/help/forms/using/assets/customfunction.zip) 폴더를 삭제합니다. 이 폴더를 다운로드하여 AEM 인스턴스에 설치합니다.

이제 클라이언트 라이브러리를 추가하여 적응형 양식에서 사용자 지정 기능을 사용할 수 있습니다.

## 적응형 양식에 클라이언트 라이브러리 추가{#add-client-library}

클라이언트 라이브러리를 AEM Forms 환경에 배포한 후에는 적응형 양식에서 해당 기능을 사용하십시오. 적응형 양식에 클라이언트 라이브러리를 추가하려면

1. 편집 모드에서 양식을 엽니다. 편집 모드에서 양식을 열려면 양식을 선택하고 을 선택합니다 **[!UICONTROL 편집]**.
1. 콘텐츠 브라우저를 열고 적응형 양식의 **[!UICONTROL 안내서 컨테이너]** 구성 요소를 선택합니다.
1. 안내서 컨테이너 속성 아이콘을 클릭합니다. 적응형 양식 컨테이너 대화 상자가 열립니다.
1. 를 엽니다. **[!UICONTROL 기본]** 탭을 클릭하고 이름 선택 **[!UICONTROL 클라이언트 라이브러리 범주]** 드롭다운 목록에서(이 경우 `customfunctionscategory`).

   ![사용자 정의 함수 클라이언트 라이브러리 추가](/help/forms/using//assets/custom-function-category-name-core-component.png)

1. **[!UICONTROL 완료]**&#x200B;를 클릭합니다.

이제 규칙 편집기에서 사용자 정의 함수를 사용하는 규칙을 만들 수 있습니다.

![사용자 정의 함수 클라이언트 라이브러리 추가](/help/forms/using//assets/calculateage-customfunction.png)

이제 를 사용하여 사용자 지정 기능을 구성하고 사용하는 방법을 이해하겠습니다. [AEM Forms 6.5의 규칙 편집기 호출 서비스](/help/forms/using/rule-editor-core-components.md#invoke-form-data-model-service-invoke)

## 적응형 양식에서 사용자 정의 함수 사용 {#use-custom-functions}

적응형 양식에서 다음을 사용할 수 있습니다 [규칙 편집기 내의 사용자 지정 함수](/help/forms/using/rule-editor-core-components.md).
JavaScript 파일에 다음 코드를 추가하겠습니다(`Function.js` file) - 생년월일(YYYY-MM-DD)을 기반으로 연령을 계산합니다. 사용자 정의 함수 만들기 `calculateAge()` 입력 시 생년월일을 사용하고 연령을 반환합니다.

```javascript
    /**
        * Calculates Age
        * @name calculateAge
        * @param {object} field
        * @return {string} 
    */

    function calculateAge(field) {
    var dob = new Date(field);
    var now = new Date();

    var age = now.getFullYear() - dob.getFullYear();
    var monthDiff = now.getMonth() - dob.getMonth();

    if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
    age--;
    }

    return age;
    }
```

위의 예에서 사용자가 생년월일을 형식(YYYY-MM-DD)으로 입력하면 사용자 지정 함수가 `calculateAge` 가 호출되고 월령을 반환합니다.

![규칙 편집기의 연령 사용자 정의 함수 계산](/help/forms/using/assets/custom-function-calculate-age.png)

이제 양식을 미리 보기하여 사용자 정의 함수가 규칙 편집기를 통해 어떻게 구현되는지 살펴보겠습니다.

![규칙 편집기 양식 미리 보기에서 연령 사용자 정의 함수 계산](/help/forms/using/assets/custom-function-age-calculate-form.png)

>[!NOTE]
>
> 다음을 참조하십시오 [사용자 정의 함수](/help/forms/using/assets/customfunctions.zip) 폴더를 삭제합니다. 를 사용하여 AEM 인스턴스에 이 폴더를 다운로드하고 설치합니다. [패키지 관리자](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager).

### 사용자 지정 함수에서 비동기 함수 지원 {#support-of-async-functions}

비동기 사용자 지정 함수는 규칙 편집기 목록에 표시되지 않습니다. 그러나 동기 함수 표현식을 사용하여 만든 사용자 지정 함수 내에서 비동기 함수를 호출할 수 있습니다.

![동기화 및 비동기 사용자 지정 기능](/help/forms/using/assets/workflow-for-sync-async-custom-fumction.png)

>[!NOTE]
>
> 사용자 지정 함수에서 비동기 함수를 호출하는 경우 비동기 함수를 사용하면 사용자 지정 함수 내에서 각 함수가 사용된 결과를 사용하여 여러 작업을 동시에 실행할 수 있다는 이점이 있습니다.

사용자 지정 함수를 사용하여 비동기 함수를 호출하는 방법은 아래 코드를 참조하십시오.

```javascript
    
    async function asyncFunction() {
    const response = await fetch('https://petstore.swagger.io/v2/store/inventory');
    const data = await response.json();
    return data;
    }

    /**
    * callAsyncFunction
    * @name callAsyncFunction callAsyncFunction
    */
    function callAsyncFunction() {
    asyncFunction()
        .then(responseData => {
        console.log('Response data:', responseData);
        })
        .catch(error => {
         console.error('Error:', error);
    });
}
```

위의 예에서 asyncFunction 함수는 `asynchronous function`. 비동기 작업은 다음을 만들어 수행합니다. `GET` 요청 대상 `https://petstore.swagger.io/v2/store/inventory`. 다음을 사용하여 응답을 기다립니다. `await`는 다음을 사용하여 응답 본문을 JSON으로 구문 분석합니다. `response.json()`를 클릭한 다음 데이터를 반환합니다. 다음 `callAsyncFunction` 함수는 를 호출하는 동기 사용자 지정 함수입니다. `asyncFunction` 콘솔에서 응답 데이터를 표시합니다. 하지만 `callAsyncFunction` 이 함수는 synchronous이고, 비동기 asyncFunction 함수를 호출하고, 결과를 `then` 및 `catch` 명령문입니다.

작동 여부를 확인하려면 단추를 추가하고 단추 클릭 시 비동기 함수를 호출하는 단추에 대한 규칙을 만들어 보겠습니다.

![비동기 함수에 대한 규칙 만들기](/help/forms/using/assets/rule-for-async-funct.png)

사용자가 를 클릭할 때 표시되는 콘솔 창의 그림을 참조하십시오. `Fetch` 단추, 사용자 지정 함수 `callAsyncFunction` 가 호출되어 비동기 함수를 호출합니다. `asyncFunction`. 버튼 클릭 시 응답을 볼 수 있는 콘솔 창 Inspect:

![콘솔 창](/help/forms/using/assets/async-custom-funct-console.png)

사용자 정의 함수의 기능에 대해 자세히 살펴보겠습니다.

## 사용자 정의 기능을 위한 다양한 기능

사용자 지정 함수를 사용하여 양식에 개인화된 기능을 추가할 수 있습니다. 이러한 기능은 특정 필드 작업, 전역 필드 사용 또는 캐싱과 같은 다양한 기능을 지원합니다. 이러한 유연성을 통해 조직의 요구 사항에 따라 양식을 사용자 정의할 수 있습니다.

### 사용자 지정 함수의 필드 및 전역 범위 개체 {#support-field-and-global-objects}

필드 개체는 텍스트 필드, 확인란 등 양식 내의 개별 구성 요소나 요소를 나타냅니다. Globals 개체에는 사용자 지정 함수 내에서 양식을 수정하는 방법, 대상 필드 인스턴스 및 양식 인스턴스와 같은 읽기 전용 변수가 포함되어 있습니다.

>[!NOTE]
>
> 다음 `param {scope} globals` 은 마지막 매개 변수여야 하며 적응형 양식의 규칙 편집기에 표시되지 않습니다.

<!-- Let us look at the following code snippet:

```JavaScript
   
    /**
    * updateDateTime
    * @name updateDateTime
    * @param {object} field
    * @param {scope} globals
    */
    function updateDateTime(field, globals) {
    // Accessing the Date object from the global scope
    var currentDate = new Date();
    // Formatting the date and time
    var formattedDateTime = currentDate.toLocaleString();
    // Updating the field value with the formatted date and time using setProperty.
    globals.functions.setProperty(field, {value: formattedDateTime});
    }
```

In the above code snippet, a custom function named `updateDateTime` takes parameters such as a field object and a global object. The field represents the textbox object where the formatted date and time value is displayed within the form. -->

사용자 지정 함수에서 필드를 사용하고 전역 개체를 사용하는 방법에 대해 알아보겠습니다. `Contact Us` 다른 사용 사례를 사용하는 양식입니다.

![연락처 양식](/help/forms/using/assets/contact-us-form.png)

#### **사용 사례**: 다음을 사용하여 패널 표시 `SetProperty` 규칙

에 설명된 대로 사용자 지정 함수에 다음 코드를 추가합니다. [create-custom-function](#create-custom-function) 섹션, 양식 필드를 다음으로 설정 `Required`.

```javascript
    
    /**
    * enablePanel
    * @name enablePanel
    * @param {object} field1
    * @param {object} field2
    * @param {scope} globals 
    */

    function enablePanel(field1,field2, globals)
    {
       if(globals.functions.validate(field1).length === 0)
       {
       globals.functions.setProperty(field2, {visible: true});
       }
    }
```

>[!NOTE]
>
> * 에 있는 사용 가능한 속성을 사용하여 필드 속성을 구성할 수 있습니다. `[form-path]/jcr:content/guideContainer.model.json`.
> * 을 사용하여 양식에 수정한 사항 `setProperty` Globals 개체의 메서드는 기본적으로 비동기이며 사용자 지정 함수를 실행하는 동안에는 반영되지 않습니다.

이 예에서 의 유효성 검사 `personaldetails` 단추를 클릭하면 패널이 표시됩니다. 패널에서 오류가 감지되지 않으면 다른 패널에서 `feedback` 단추 클릭 시 패널이 표시됩니다.

다음에 대한 규칙을 만들겠습니다. `Next` 단추, 유효성 검사 `personaldetails` 패널 및 만들기 `feedback`  사용자가 패널을 클릭하면 표시되는 `Next` 단추를 클릭합니다.

![속성 설정](/help/forms/using/assets/custom-function-set-property.png)

다음 그림을 참조하여 의 위치를 확인하십시오. `personaldetails` 패널을 클릭하면 유효성이 검사됩니다. `Next` 단추를 클릭합니다. 대소문자 구분 안 함 내의 모든 필드 `personaldetails` 유효성 검사됨, `feedback` 패널이 표시됩니다.

![속성 양식 미리 보기 설정](/help/forms/using/assets/set-property-form-preview.png)

의 필드에 오류가 있는 경우 `personaldetails` 패널 - 다음을 클릭하면 필드 수준에서 표시됩니다. `Next` 단추 및 `feedback` 패널은 계속 표시되지 않습니다.

![속성 양식 미리 보기 설정](/help/forms/using/assets/set-property-panel.png)

#### **사용 사례**: 필드의 유효성 검사

에 설명된 대로 사용자 지정 함수에 다음 코드를 추가합니다. [create-custom-function](#create-custom-function) 섹션의 유효성 검사를 참조하십시오.

```javascript
    /**
    * validateField
    * @name validateField
    * @param {object} field
    * @param {scope} globals
    */
    function validateField(field,globals)
    {
    
        globals.functions.validate(field);
    
    }   
```

>[!NOTE]
>
> 에 인수가 전달되지 않으면 `validate()` 함수, 양식의 유효성을 검사합니다.

이 예에서는 사용자 정의 유효성 검사 패턴이 `contact` 필드. 사용자는 다음으로 시작하는 전화 번호를 입력해야 합니다. `10` 뒤에 오는 `8` 숫자. 사용자가 다음으로 시작하지 않는 전화 번호를 입력하는 경우 `10` 또는 보다 많거나 적은 포함 `8` 숫자로 표시된 경우 단추를 클릭하면 유효성 검사 오류 메시지가 나타납니다.

![이메일 주소 유효성 검사 패턴](/help/forms/using/assets/custom-function-validation-pattern.png)

이제 다음 단계에서는 다음에 대한 규칙을 만듭니다. `Next` 의 유효성을 검사하는 버튼 `contact` 단추 클릭 시 필드.

![유효성 검사 패턴](/help/forms/using/assets/custom-function-validate.png)

사용자가 다음으로 시작하지 않는 전화 번호를 입력하는 경우 아래 그림을 참조하십시오. `10`필드 수준에 다음과 같은 오류 메시지가 나타납니다.

![이메일 주소 유효성 검사 패턴](/help/forms/using/assets/custom-function-validate-error-message.png)

사용자가 유효한 전화 번호와 `personaldetails` 패널의 유효성이 검사됩니다. `feedback` 패널이 화면에 표시됩니다.

![이메일 주소 유효성 검사 패턴](/help/forms/using/assets/validate-form-preview-form.png)

#### **사용 사례**: 패널 재설정

에 설명된 대로 사용자 지정 함수에 다음 코드를 추가합니다. [create-custom-function](#create-custom-function) 섹션, 패널을 재설정합니다.

```javascript
    /**
    * resetField
    * @name  resetField
    * @param {string} input1
    * @param {object} field
    * @param {scope} globals 
    */
    function  resetField(field,globals)
    {
    
        globals.functions.reset(field);
    
    }
```

>[!NOTE]
>
> 에 인수가 전달되지 않으면 `reset()` 함수, 양식의 유효성을 검사합니다.

이 예에서는 `personaldetails` 패널을 클릭하면 재설정됩니다. `Clear` 단추를 클릭합니다. 다음 단계는 다음에 대한 규칙을 만드는 것입니다. `Clear` 단추를 클릭하면 패널이 재설정됩니다.

![지우기 단추](/help/forms/using/assets/custom-function-reset-field.png)

사용자가 를 클릭할 경우 이를 표시하려면 아래 그림을 참조하십시오. `clear` 단추, `personaldetails` 패널 재설정:

![양식 재설정](assets/custom-function-reset-form.png)

#### **사용 사례**: 필드 수준에서 사용자 정의 메시지를 표시하고 필드를 유효하지 않은 것으로 표시

다음을 사용할 수 있습니다. `markFieldAsInvalid()` 필드를 유효하지 않은 것으로 정의하고 필드 수준에서 사용자 지정 오류 메시지를 설정하는 함수입니다. 다음 `fieldIdentifier` 값은 다음과 같을 수 있습니다. `fieldId`, 또는 `field qualifiedName`, 또는 `field dataRef`. 이름이 인 개체의 값 `option` 다음이 될 수 있음: `{useId: true}`, `{useQualifiedName: true}`, 또는 `{useDataRef: true}`.
필드를 유효하지 않은 것으로 표시하고 사용자 정의 메시지를 설정하는 데 사용되는 구문은 다음과 같습니다.

* `globals.functions.markFieldAsInvalid(field.$id,"[custom message]",{useId: true});`
* `globals.functions.markFieldAsInvalid(field.$qualifiedName, "[custom message]", {useQualifiedName: true});`
* `globals.functions.markFieldAsInvalid(field.$dataRef, "[custom message]", {useDataRef: true});`

에 설명된 대로 사용자 지정 함수에 다음 코드를 추가합니다. [create-custom-function](#create-custom-function) 섹션에 있는 마지막 항목이 될 필요가 없습니다.

```javascript
    /**
    * customMessage
    * @name customMessage
    * @param {object} field
    * @param {scope} globals 
    */
    function customMessage(field, globals) {
    const minLength = 15;
    const comments = field.$value.trim();
    if (comments.length < minLength) {
        globals.functions.markFieldAsInvalid(field.$id, "Comments must be at least 15 characters long.", { useId: true });
    }
}
```

이 예제에서 사용자가 주석 입력란에 15자 미만을 입력하면 사용자 정의 메시지가 필드 수준에 나타납니다.

다음 단계는 다음에 대한 규칙을 만드는 것입니다. `comments` 필드:

![필드를 유효하지 않은 것으로 표시](/help/forms/using/assets/custom-function-invalid-field.png)

에 부정적인 피드백을 입력했음을 표시하려면 아래 데모를 참조하십시오. `comments` 필드는 필드 수준에서 사용자 지정 메시지 표시를 트리거합니다.

![필드를 잘못된 미리보기 양식으로 표시](/help/forms/using/assets/custom-function-invalidfield-form.png)

사용자가 댓글 텍스트 상자에 15자 이상을 입력하면 필드의 유효성이 검사되고 양식이 제출됩니다.

![필드를 유효한 미리 보기 양식으로 표시](/help/forms/using/assets/custom-function-validfield-form.png)


#### **사용 사례**: 변경된 데이터를 서버에 제출

다음 코드 줄:
`globals.functions.submitForm(globals.functions.exportData(), false);` 은 조작 후 양식 데이터를 제출하는 데 사용됩니다.
* 첫 번째 인수는 제출할 데이터입니다.
* 두 번째 인수는 제출 전에 양식의 유효성을 검사할지 여부를 나타냅니다. 다음과 같습니다. `optional` 및 로 설정 `true` 기본적으로.
* 세 번째 인수는 `contentType` 제출 서류 - 기본값과 함께 선택 사항입니다. `multipart/form-data`. 다른 값은 다음과 같습니다. `application/json` 및 `application/x-www-form-urlencoded`.

에 설명된 대로 사용자 지정 함수에 다음 코드를 추가합니다. [create-custom-function](#create-custom-function) 섹션에서 조작된 데이터를 서버에 제출하려면 다음을 수행합니다.

```javascript
    /**
    * submitData
    * @name submitData
    * @param {object} field
    * @param {scope} globals 
    */
    function submitData(globals)
    {
    
    var data = globals.functions.exportData();
    if(!data.comments) {
    data.comments = 'NA';
    }
    console.log('After update:{}',data);
    globals.functions.submitForm(data, false);
    }
```

이 예에서 사용자가 `comments` 텍스트 상자가 비어 있음, `NA` 양식 제출 시 서버에 제출됩니다.

이제 다음에 대한 규칙을 만듭니다. `Submit` 데이터를 전송하는 단추:

![데이터 제출](/help/forms/using/assets/custom-function-submit-data.png)

의 그림을 참조하십시오 `console window` 사용자가 `comments` textbox가 비어 있는 경우 값이 `NA` 은(는) 서버에서 제출됩니다.

![콘솔 창에서 데이터 제출](/help/forms/using/assets/custom-function-submit-data-form.png)

또한 콘솔 창을 검사하여 서버에 제출된 데이터를 볼 수도 있습니다.

![콘솔 창의 Inspect 데이터](/help/forms/using/assets/custom-function-submit-data-console-data.png)

<!--

#### **Use Case**: Display form submission and failure messages for custom submit action 

Add the following line of code as explained in the [create-custom-function ](#create-custom-function) section, to customize the submission or failure message for form submissions and display the form submission messages in a modal box:

```javascript
/**
 * Handles the success response after a form submission.
 *
 * @param {scope} globals - This object contains a read-only form instance, target field instance, triggered event, and methods for performing form modifications within custom functions.
 * @returns {void}
 */
function customSubmitSuccessHandler(globals) {
    var event = globals.event;
    var submitSuccessResponse = event.payload.body;
    var form = globals.form;

    if (submitSuccessResponse) {
        if (submitSuccessResponse.redirectUrl) {
            window.location.href = encodeURI(submitSuccessResponse.redirectUrl);
        } else if (submitSuccessResponse.thankYouMessage) {
            showModal("success", submitSuccessResponse.thankYouMessage);
        }
    }
}

/**
 * Handles the error response after a form submission.
 *
 * @param {string} customSubmitErrorMessage - The custom error message.
 * @param {scope} globals - This object contains a read-only form instance, target field instance, triggered event, and methods for performing form modifications within custom functions.
 * @returns {void}
 */
function customSubmitErrorHandler(customSubmitErrorMessage, globals) {
    showModal("error", customSubmitErrorMessage);
}
function showModal(type, message) {
    // Remove any existing modals
    var existingModal = document.getElementById("modal");
    if (existingModal) {
        existingModal.remove();
    }

    // Create the modal dialog
    var modal = document.createElement("div");
    modal.setAttribute("id", "modal");
    modal.setAttribute("class", "modal");

    // Create the modal content
    var modalContent = document.createElement("div");
    modalContent.setAttribute("class", "modal-content");

    // Create the modal header
    var modalHeader = document.createElement("div");
    modalHeader.setAttribute("class", "modal-header");
    modalHeader.innerHTML = "<h2>" + (type === "success" ? "Thank You" : "Error") + "</h2>";

    // Create the modal body
    var modalBody = document.createElement("div");
    modalBody.setAttribute("class", "modal-body");
    modalBody.innerHTML = "<p class='" + type + "-message'>" + message + "</p>";

    // Create the modal footer
    var modalFooter = document.createElement("div");
    modalFooter.setAttribute("class", "modal-footer");

    // Create the close button
    var closeButton = document.createElement("button");
    closeButton.setAttribute("class", "close-button");
    closeButton.innerHTML = "Close";
    closeButton.onclick = function() {
        modal.remove();
    };

    // Append the elements to the modal content
    modalFooter.appendChild(closeButton);
    modalContent.appendChild(modalHeader);
    modalContent.appendChild(modalBody);
    modalContent.appendChild(modalFooter);

    // Append the modal content to the modal
    modal.appendChild(modalContent);

    // Append the modal to the document body
    document.body.appendChild(modal);
}
```

In this example, when the user uses the `customSubmitSuccessHandler` and `customSubmitErrorHandler` custom functions, the success and failure messages are displayed in a modal. The JavaScript function `showModal(type, message)` is used to dynamically create and display a modal dialog box on a screen.

Now, create a rule for successful form submission:

![Form submission success](/help/forms/using/assets/form-submission-success.png)

Refer to the illustration below to demonstrate that when the form is submitted successfully, the success message is displayed in a modal:

![Form submission success message](/help/forms/using/assets/form-submission-success-message.png )
 
Similarly, let us create a rule for failed form submissions:

![Form submission fail](/help/forms/using/assets/form-submission-fail.png)

Refer to the illustration below to demonstrate that when the form submission fails, the error message is displayed in a modal:

![Form submission fail message](/help/forms/using/assets/form-submission-fail-message.png )

To display form submission success and failure in a default manner, the `Default submit Form Success Handler` and `Default submit Form Error Handler` functions are available out of the box.

In case, the custom submit action fails to perform as expected in existing AEM projects or forms, refer to the [troubleshooting](#troubleshooting) section.

-->

## 사용자 지정 기능에 대한 캐싱 지원

적응형 Forms은 규칙 편집기에서 사용자 지정 함수 목록을 검색하는 동안 응답 시간을 개선하기 위해 사용자 지정 함수에 대한 캐싱을 구현합니다. 다음으로 메시지: `Fetched following custom functions list from cache` 에 표시 `error.log` 파일.

![캐시 지원을 통한 사용자 정의 기능](/help/forms/using/assets/custom-function-cache-error.png)

사용자 지정 함수가 수정되면 캐싱이 무효화되고 구문 분석됩니다.

## 문제 해결 {#troubleshooting}

* 사용자는 [핵심 구성 요소 및 사양 버전이 최신 버전으로 설정되어 있습니다.](https://github.com/adobe/aem-core-forms-components/tree/release/650). 그러나 기존 AEM 프로젝트 및 양식의 경우 따라야 할 추가 단계가 있습니다.

   * AEM 프로젝트의 경우 사용자는 의 모든 인스턴스를 `submitForm('custom:submitSuccess', 'custom:submitError')` 포함 `submitForm()` 프로젝트를 배포합니다.

   * 기존 양식의 경우 사용자 정의 제출 핸들러가 제대로 작동하지 않으면 를 열고 저장해야 합니다 `submitForm` 에 대한 규칙 **제출** 규칙 편집기를 사용하는 단추입니다. 이 작업은 의 기존 규칙을 대체합니다. `submitForm('custom:submitSuccess', 'custom:submitError')` 포함 `submitForm()` 폼에서.


* 사용자 지정 함수에 대한 코드가 포함된 JavaScript 파일에 오류가 있는 경우 사용자 지정 함수가 적응형 양식의 규칙 편집기에 나열되지 않습니다. 사용자 지정 함수 목록을 확인하려면 `error.log` 파일에 오류가 표시됩니다. 오류가 발생하면 사용자 지정 함수 목록이 비어 있습니다.

  ![오류 로그 파일](/help/forms/using/assets/custom-function-list-error-file.png)

  오류가 없는 경우 사용자 지정 함수를 가져와서 `error.log` 파일. 다음으로 메시지: `Fetched following custom functions list` 에 표시 `error.log` 파일:

  ![적절한 사용자 정의 기능이 있는 오류 로그 파일](/help/forms/using/assets/custom-function-list-fetched-in-error.png)

## 고려 사항

* 다음 `parameter type` 및 `return type` 지원 안 함 `None`.

* 사용자 지정 함수 목록에서 지원되지 않는 함수는 다음과 같습니다.
   * 생성기 함수
   * 비동기/대기 함수
   * 메서드 정의
   * 클래스 메서드
   * 기본 매개 변수
   * 나머지 매개 변수

