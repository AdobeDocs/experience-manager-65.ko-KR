---
title: 적응형 양식에서 사용자 정의 함수 만들기 및 추가
description: AEM Forms은 사용자가 규칙 편집기 내에서 자체 함수를 만들고 사용할 수 있도록 하는 사용자 지정 함수를 지원합니다.
keywords: 사용자 지정 함수를 추가하고, 사용자 지정 함수를 사용하고, 사용자 지정 함수를 만들고, 규칙 편집기에서 사용자 지정 함수를 사용합니다.
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms,Core Components
exl-id: a328b4a8-e8dd-42a0-b73b-94e76c7692a8
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 5%

---


# 적응형 Forms(핵심 구성 요소)의 사용자 지정 기능

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/kr/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/create-and-use-custom-functions) |
| AEM 6.5 | 이 문서 |

## 소개

AEM Forms 6.5에는 규칙 편집기를 사용하여 복잡한 비즈니스 규칙을 정의하는 데 사용할 수 있는 JavaScript 함수를 정의하는 기능이 도입되었습니다. AEM Forms에서는 이러한 다양한 사용자 정의 함수를 기본적으로 제공하지만, 사용자 정의 함수를 정의하고 여러 양식에서 사용해야 합니다.

사용자 지정 함수는 지정된 요구 사항을 충족하도록 입력된 데이터의 조작 및 처리를 용이하게 하여 양식의 기능을 확장합니다. 또한 사전 정의된 기준에 따라 양식 동작을 동적으로 변경할 수 있습니다.
적응형 Forms에서는 적응형 양식의 [규칙 편집기](/help/forms/using/rule-editor.md) 내에서 사용자 지정 함수를 사용하여 양식 필드에 대한 특정 유효성 검사 규칙을 만들 수 있습니다.
사용자가 이메일 주소를 입력하는 사용자 정의 함수의 사용을 이해하고 입력된 이메일 주소가 특정 형식(&quot;@&quot; 기호 및 도메인 이름 포함)을 따르는지 확인하겠습니다. 이메일 주소를 입력으로 사용하고 유효한 경우 true를 반환하고 그렇지 않은 경우 false를 반환하는 사용자 지정 함수를 &quot;ValidateEmail&quot;로 만듭니다.

```javascript
function ValidateEmail(inputText)
{
    var email = /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/;
    if(inputText.value.match(email))
        {
            alert("Valid email address!");
            return true;
        }
    else
    {
        alert("Invalid email address!");
        return false;
    }
}
```

위의 예에서 사용자가 양식을 제출하려고 하면 사용자 지정 함수 &quot;ValidateEmail&quot;이 호출되어 입력한 이메일 주소가 유효한지 확인합니다.

## 사용자 정의 함수 사용 {#uses-of-custom-function}

적응형 Forms에서 사용자 정의 함수를 사용할 때의 장점은 다음과 같습니다.

* **데이터 조작**: 사용자 지정 함수는 양식 필드에 입력된 데이터를 조작하고 처리합니다.
* **데이터 유효성 검사**: 사용자 지정 기능을 사용하면 양식 입력에 대한 사용자 지정 검사를 수행하고 지정된 오류 메시지를 제공할 수 있습니다.
* **동적 동작**: 사용자 지정 함수를 사용하면 특정 조건에 따라 양식의 동적 동작을 제어할 수 있습니다. 예를 들어 필드를 표시/숨기거나, 필드 값을 수정하거나, 양식 논리를 동적으로 조정할 수 있습니다.
* **통합**: 사용자 지정 함수를 사용하여 외부 API 또는 서비스와 통합할 수 있습니다. 외부 소스에서 데이터를 가져오거나 외부 Rest 끝점으로 데이터를 전송하거나 외부 이벤트를 기반으로 사용자 지정 작업을 수행하는 데 도움이 됩니다.

## 지원되는 JS 주석

작성한 사용자 지정 함수에는 위에 `jsdoc`이(가) 있어야 합니다. 이 경우 사용자 지정 구성 및 설명이 필요합니다. `JavaScript,`에서 함수를 선언하는 방법에는 여러 가지가 있으며 주석을 사용하여 함수를 추적할 수 있습니다. 자세한 내용은 [usejsdoc.org](https://jsdoc.app/)을(를) 참조하십시오.

지원되는 `jsdoc`개 태그:

* **비공개**
구문: `@private`
비공개 함수는 사용자 지정 함수로 포함되지 않습니다.

* **이름**
구문: `@name funcName <Function Name>`
또는 `,`을(를) 사용할 수 있습니다. `@function funcName <Function Name>` **또는** `@func` `funcName <Function Name>`.
  `funcName`은(는) 함수 이름입니다(공백은 허용되지 않음).
  `<Function Name>`은(는) 함수의 표시 이름입니다.

* **구성원**
구문: `@memberof namespace`
네임스페이스를 함수에 연결합니다.

* **매개 변수**
구문: `@param {type} name <Parameter Description>`
또는 다음을 사용할 수 있습니다. `@argument` `{type} name <Parameter Description>` **또는** `@arg` `{type}` `name <Parameter Description>`.
함수에서 사용하는 매개 변수를 표시합니다. 함수는 여러 매개 변수 태그를 가질 수 있으며, 발생 순서로 각 매개 변수에 대해 하나의 태그가 있습니다.
  `{type}`은(는) 매개 변수 형식을 나타냅니다. 허용되는 매개 변수 유형은 다음과 같습니다.

   1. 문자열
   2. 숫자
   3. 부울
   4. 범위

  범위는 적응형 양식의 참조 필드에 사용됩니다. 폼에서 소극적 로드를 사용하는 경우 `scope`을(를) 사용하여 해당 필드에 액세스할 수 있습니다. 필드가 로드될 때 또는 필드가 전역으로 표시될 때 필드에 액세스할 수 있습니다.

  다른 모든 매개변수 유형은 위의 한 가지 유형에 따라 분류됩니다. 지원되지 않습니다. 위의 유형 중 하나를 선택해야 합니다. 유형은 대/소문자를 구분하지 않습니다. `name` 매개 변수에는 공백을 사용할 수 없습니다. `<Parameter Descrption>` `<parameter>  can have multiple words. </parameter>`

* **반환 형식**
구문: `@return {type}`
또는 `@returns {type}`을(를) 사용할 수 있습니다.
함수 목적 등 함수에 대한 정보를 추가합니다.
{type}은(는) 함수의 반환 형식을 나타냅니다. 허용되는 반환 유형은 다음과 같습니다.

   1. 문자열
   1. 숫자
   1. 부울

  다른 모든 반환 유형은 위의 한 가지 유형에 따라 분류됩니다. 지원되지 않습니다. 위의 유형 중 하나를 선택해야 합니다. 반환 유형은 대/소문자를 구분하지 않습니다.

* **이**
구문: `@this currentComponent`

  규칙@this 작성된 적응형 양식 구성 요소를 참조하려면 AEM을 사용하십시오.

  다음 예제는 필드 값을 기반으로 합니다. 다음 예에서 규칙은 양식의 필드를 숨깁니다. `this.value`의 `this` 부분이 규칙이 작성된 기본 적응형 양식 구성 요소를 참조합니다.

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
  >사용자 지정 함수 이전의 댓글은 요약에 사용됩니다. 요약은 태그가 발견될 때까지 여러 줄로 확장할 수 있습니다. 규칙 빌더에서 간단한 설명을 보려면 크기를 하나로 제한하십시오.

## 함수 선언 지원 유형 {#function-declaration-supported-types}

**Function 문**

```javascript
function area(len) {
    return len*len;
}
```

이 함수는 `jsdoc`개의 댓글 없이 포함됩니다.

**함수 식**

```javascript
var area;
//Some codes later
/** */
area = function(len) {
    return len*len;
};
```

**함수 식 및 문**

```javascript
var b={};
/** */
b.area = function(len) {
    return len*len;
}
```

**변수로 함수 선언**

```javascript
/** */
var x1,
    area = function(len) {
        return len*len;
    },
    x2 =5, x3 =true;
```

제한 사항: 사용자 지정 함수는 함께 있는 경우 변수 목록에서 첫 번째 함수 선언만 선택합니다. 선언된 모든 함수에 함수 표현식을 사용할 수 있습니다.

**개체로 함수 선언**

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

## 사용자 지정 함수 만들기 {#create-custom-function}

사용자 지정 함수를 만들려면 다음 단계를 수행하십시오.

1. `http://server:port/crx/de/index.jsp#`에 로그인합니다.
1. `/apps` 폴더 아래에 폴더를 만듭니다. 예를 들어 `experience-league`(으)로 이름이 지정된 폴더를 만듭니다.
1. 변경 사항을 저장합니다.
1. 만든 폴더로 이동하여 `cq:ClientLibraryFolder` 유형의 노드를 `clientlibs`(으)로 만듭니다.
1. 새로 만든 `clientlibs` 폴더로 이동하여 `allowProxy` 및 `categories` 속성을 추가하십시오.

   ![사용자 지정 라이브러리 노드 속성](/help/forms/using/assets/customlibrary-catproperties.png)

   >[!NOTE]
   >
   > `customfunctionsdemo` 대신 모든 이름을 제공할 수 있습니다.

1. 변경 사항을 저장합니다.

1. `clientlibs` 폴더 아래에 `js` 폴더를 만듭니다.
1. `js` 폴더 아래에 `functions.js`(이)라는 JavaScript 파일을 만듭니다.
1. `clientlibs` 폴더 아래에 `js.txt` 파일을 만듭니다.
1. 변경 사항을 저장합니다.
생성된 폴더 구조 형태는 다음과 같습니다.

   ![클라이언트 라이브러리 폴더 구조가 생성됨](/help/forms/using/assets/clientlibrary_folderstructure.png)
1. `functions.js` 파일을 두 번 클릭하여 편집기를 엽니다. 이 파일은 사용자 지정 함수에 대한 코드로 구성됩니다.
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

1. `function.js`을(를) 저장합니다.
1. `js.txt`(으)로 이동하여 다음 코드를 추가합니다.

   ```javascript
       #base=js
       functions.js
   ```

1. `js.txt` 파일을 저장합니다.

다음 [사용자 지정 함수](/help/forms/using/assets/customfunction.zip) 폴더를 참조할 수 있습니다. 이 폴더를 다운로드하여 AEM 인스턴스에 설치합니다.

이제 클라이언트 라이브러리를 추가하여 적응형 양식에서 사용자 지정 기능을 사용할 수 있습니다.

## 적응형 양식에 클라이언트 라이브러리 추가{#use-custom-function}

클라이언트 라이브러리를 Forms CS 환경에 배포한 후에는 적응형 양식에서 해당 기능을 사용하십시오. 적응형 양식에 클라이언트 라이브러리를 추가하려면

1. 편집 모드에서 양식을 엽니다. 편집 모드에서 양식을 열려면 양식을 선택하고 **[!UICONTROL 편집]**&#x200B;을 선택합니다.
1. 콘텐츠 브라우저를 열고 적응형 양식의 **[!UICONTROL 안내서 컨테이너]** 구성 요소를 선택합니다.
1. 안내서 컨테이너 속성 아이콘을 클릭합니다. 적응형 양식 컨테이너 대화 상자가 열립니다.
1. **[!UICONTROL 기본]** 탭을 열고 드롭다운 목록에서 **[!UICONTROL 클라이언트 라이브러리 범주]**&#x200B;의 이름을 선택합니다(이 경우 `customfunctionscategory` 선택).

   ![사용자 지정 함수 클라이언트 라이브러리를 추가](/help/forms/using//assets/custom-function-category-name-core-component.png)

1. **[!UICONTROL 완료]** 를 클릭합니다.

이제 규칙 편집기에서 사용자 정의 함수를 사용하는 규칙을 만들 수 있습니다.

![사용자 지정 함수 클라이언트 라이브러리를 추가](/help/forms/using//assets/calculateage-customfunction.png)

이제 AEM Forms에서 [규칙 편집기의 호출 서비스](/help//forms/using/rule-editor.md)를 사용하여 사용자 지정 함수를 구성하고 사용하는 방법에 대해 알아보겠습니다.
