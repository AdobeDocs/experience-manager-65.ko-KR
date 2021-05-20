---
title: JSON 스키마를 사용하여 적응형 Forms을 만드는 방법
description: JSON 스키마를 양식 모델로 사용하여 적응형 양식을 만드는 방법을 알아보십시오. 기존 JSON 스키마를 사용하여 적응형 양식을 만들 수 있습니다. JSON 스키마 샘플을 사용하여 자세히 분석하고, JSON 스키마 정의에서 필드를 사전 구성하고, 적응형 양식 구성 요소에 대해 허용 가능한 값을 제한하며, 지원되지 않는 구문을 학습합니다.
feature: 적응형 양식
role: Business Practitioner, Developer
level: Beginner, Intermediate
exl-id: 1b402aef-a319-4d32-8ada-cadc86f5c872
source-git-commit: ad67634278088f8f953fde61a3543acdd70537dd
workflow-type: tm+mt
source-wordcount: '1450'
ht-degree: 5%

---

# JSON 스키마를 사용하여 적응형 양식 만들기 {#creating-adaptive-forms-using-json-schema}

## 전제 조건 {#prerequisites}

JSON 스키마를 양식 모델로 사용하여 적응형 양식을 작성하려면 JSON 스키마에 대한 기본적인 이해가 필요합니다. 이 문서 전에 다음 내용을 읽는 것이 좋습니다.

* [적응형 양식 만들기](creating-adaptive-form.md)
* [JSON 스키마](https://json-schema.org/)

## JSON 스키마를 양식 모델 {#using-a-json-schema-as-form-model} 로 사용

[!DNL Adobe Experience Manager Forms] 에서는 기존 JSON 스키마를 양식 모델로 사용하여 적응형 양식 생성을 지원합니다. 이 JSON 스키마는 조직의 백엔드 시스템에서 데이터를 생성하거나 사용하는 구조를 나타냅니다. 사용하는 JSON 스키마는 [v4 사양](https://json-schema.org/draft-04/schema)과 호환되어야 합니다.

JSON 스키마 사용의 주요 기능은 다음과 같습니다.

* 적응형 양식의 작성 모드에서 컨텐츠 파인더 탭에 JSON의 구조가 트리로 표시됩니다. JSON 계층 구조에서 요소를 적응형 양식에 드래그하여 추가할 수 있습니다.
* 연관된 스키마와 호환되는 JSON을 사용하여 양식을 미리 채울 수 있습니다.
* 제출 시 사용자가 입력한 데이터는 관련 스키마에 맞게 JSON으로 제출됩니다.

JSON 스키마는 간단하고 복잡한 요소 유형으로 구성됩니다. 요소에는 요소에 규칙을 추가하는 특성이 있습니다. 이러한 요소와 속성을 적응형 양식으로 드래그하면 해당 적응형 양식 구성 요소에 자동으로 매핑됩니다.

적응형 양식 구성 요소가 있는 JSON 요소 매핑은 다음과 같습니다.

```json
"birthDate": {
              "type": "string",
              "format": "date",
              "pattern": "date{DD MMMM, YYYY}",
              "aem:affKeyword": [
                "DOB",
                "Date of Birth"
              ],
              "description": "Date of birth in DD MMMM, YYYY",
              "aem:afProperties": {
                "displayPictureClause": "date{DD MMMM, YYYY}",
                "displayPatternType": "date{DD MMMM, YYYY}",
                "validationPatternType": "date{DD MMMM, YYYY}",
                "validatePictureClause": "date{DD MMMM, YYYY}",
                "validatePictureClauseMessage": "Date must be in DD MMMM, YYYY format."
              }
```

<table>
 <tbody>
  <tr>
   <th><strong>JSON 요소, 속성 또는 속성</strong></th>
   <th><strong>적응형 양식 구성 요소</strong></th>
  </tr>
  <tr>
   <td><p>열거형 및 enumNames 제약 조건이 있는 문자열 속성.</p> <p>구문,</p> <p> <code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"enum" : ["M", "F"]</code></p> <p><code>"enumNames" : ["Male", "Female"]</code></p> <p><code>}</code></p> <p> </p> </td>
   <td><p>드롭다운 구성 요소:</p>
    <ul>
     <li>enumNames에 나열된 값이 드롭 상자에 표시됩니다.</li>
     <li>열거형에 나열된 값은 계산에 사용됩니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>형식 제약 조건이 있는 문자열 속성입니다. 예를 들어, 이메일 및 날짜입니다.</p> <p>구문,</p> <p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"format" : "email"</code></p> <p><code>}</code></p> <p> </p> </td>
   <td>
    <ul>
     <li>이메일 구성 요소는 유형이 문자열이고 형식이 이메일인 경우 매핑됩니다.</li>
     <li>형식이 문자열이고 형식이 호스트 이름이면 유효성 검사가 있는 Textbox 구성 요소가 매핑됩니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>}</code></p> </td>
   <td><br /> <br /> 텍스트 필드<br /> <br /> <br /> </td>
  </tr>
  <tr>
   <td>number 속성<br /> </td>
   <td>하위 유형이 float<br />으로 설정된 숫자 필드 </td>
  </tr>
  <tr>
   <td>정수 속성<br /> </td>
   <td>하위 유형이 정수<br />로 설정된 숫자 필드 </td>
  </tr>
  <tr>
   <td>부울 속성<br /> </td>
   <td>전환<br /> </td>
  </tr>
  <tr>
   <td>개체 속성<br /> </td>
   <td>패널<br /> </td>
  </tr>
  <tr>
   <td>배열 속성</td>
   <td>최소 및 최대 값이 minItems 및 maxItems와 동일한 반복 가능한 패널. 단일 배열만 지원됩니다. 따라서 항목 제약 조건은 배열이 아닌 개체여야 합니다.<br /> </td>
  </tr>
 </tbody>
</table>

### 일반 스키마 속성 {#common-schema-properties}

적응형 양식은 JSON 스키마에서 사용할 수 있는 정보를 사용하여 생성된 각 필드를 매핑합니다. 특히

* `title` 속성은 적응형 양식 구성 요소에 대한 레이블로 사용됩니다.
* `description` 속성은 적응형 양식 구성 요소에 대한 긴 설명으로 설정됩니다.
* `default` 속성은 적응형 양식 필드의 초기 값으로 사용됩니다.
* `maxLength` 속성이 텍스트 필드 구성 요소의 `maxlength` 특성으로 설정됩니다.
* `minimum`, `maximum`, `exclusiveMinimum` 및 `exclusiveMaximum` 속성은 숫자 상자 구성 요소에 사용됩니다.
* `DatePicker component` 추가 JSON 스키마 속성 `minDate` 및 `maxDate`에 대한 범위를 지원하기 위해 가 제공됩니다.
* `minItems` 및 `maxItems` 속성은 패널 구성 요소에서 추가 또는 제거할 수 있는 항목/필드의 수를 제한하는 데 사용됩니다.
* `readOnly` 속성은 적응형 양식 구성 요소의 `readonly` 속성을 설정합니다.
* `required` 속성은 적응형 양식 필드를 필수로 표시하지만 패널(유형이 객체)에서는 마지막으로 제출된 JSON 데이터에 해당 객체에 해당하는 빈 값이 있는 필드가 있습니다.
* `pattern` 속성은 적응형 양식의 유효성 검사 패턴(정규 표현식)으로 설정됩니다.
* JSON 스키마 파일 확장자는 .schema.json으로 유지해야 합니다. 예: &lt;filename>.schema.json.

## 샘플 JSON 스키마 {#sample-json-schema}

다음은 JSON 스키마의 예입니다.

```json
{
 "$schema": "https://json-schema.org/draft-04/schema#",
 "definitions": {
  "employee": {
   "type": "object",
   "properties": {
    "userName": {
     "type": "string"
    },
    "dateOfBirth": {
     "type": "string",
     "format": "date"
    },
    "email": {
     "type": "string",
     "format": "email"
    },
    "language": {
     "type": "string"
    },
    "personalDetails": {
     "$ref": "#/definitions/personalDetails"
    },
    "projectDetails": {
     "$ref": "#/definitions/projectDetails"
    }
   },
   "required": [
    "userName",
    "dateOfBirth",
    "language"
   ]
  },
  "personalDetails": {
   "type": "object",
   "properties": {
    "GeneralDetails": {
     "$ref": "#/definitions/GeneralDetails"
    },
    "Family": {
     "$ref": "#/definitions/Family"
    },
    "Income": {
     "$ref": "#/definitions/Income"
    }
   }
  },
  "projectDetails": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     },
     "projects": {
      "$ref": "#/definitions/projects"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "projects": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     },
     "projectsAdditional": {
      "$ref": "#/definitions/projectsAdditional"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "projectsAdditional": {
   "type": "array",
   "items": {
    "properties": {
     "Additional_name": {
      "type": "string"
     },
     "Additional_areacode": {
      "type": "number"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "GeneralDetails": {
   "type": "object",
   "properties": {
    "age": {
     "type": "number"
    },
    "married": {
     "type": "boolean"
    },
    "phone": {
     "type": "number",
     "aem:afProperties": {
      "sling:resourceType": "/libs/fd/af/components/guidetelephone",
      "guideNodeClass": "guideTelephone"
     }
    },
    "address": {
     "type": "string"
    }
   }
  },
  "Family": {
   "type": "object",
   "properties": {
    "spouse": {
     "$ref": "#/definitions/spouse"
    },
    "kids": {
     "$ref": "#/definitions/kids"
    }
   }
  },
  "Income": {
   "type": "object",
   "properties": {
    "monthly": {
     "type": "number"
    },
    "yearly": {
     "type": "number"
    }
   }
  },
  "spouse": {
   "type": "object",
   "properties": {
    "name": {
     "type": "string"
    },
    "Income": {
     "$ref": "#/definitions/Income"
    }
   }
  },
  "kids": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  }
 },
 "type": "object",
 "properties": {
  "employee": {
   "$ref": "#/definitions/employee"
  }
 }
}
```

### 재사용 가능한 스키마 정의 {#reusable-schema-definitions}

정의 키는 재사용 가능한 스키마를 식별하는 데 사용됩니다. 재사용 가능한 스키마 정의는 조각을 만드는 데 사용됩니다. XSD에서 복합 형식을 식별하는 것과 비슷합니다. 정의가 있는 샘플 JSON 스키마는 아래에 나와 있습니다.

```json
{
  "$schema": "https://json-schema.org/draft-04/schema#",

  "definitions": {
    "address": {
      "type": "object",
      "properties": {
        "street_address": { "type": "string" },
        "city":           { "type": "string" },
        "state":          { "type": "string" }
      },
      "required": ["street_address", "city", "state"]
    }
  },

  "type": "object",

  "properties": {
    "billing_address": { "$ref": "#/definitions/address" },
    "shipping_address": { "$ref": "#/definitions/address" }
  }
}
```

위의 예에서는 고객 레코드를 정의합니다. 여기서 각 고객은 배송 주소와 청구 주소를 모두 갖습니다. 두 주소의 구조는 동일합니다. 주소는 주소, 도시 및 주지가 있으므로 주소를 중복하지 않는 것이 좋습니다. 또한 나중에 변경할 수 있도록 필드를 손쉽게 추가 및 삭제할 수 있습니다.

## JSON 스키마 정의 {#pre-configuring-fields-in-json-schema-definition}에 있는 필드 사전 구성

**aem:afProperties** 속성을 사용하여 JSON 스키마 필드를 사전 구성하여 사용자 지정 적응형 양식 구성 요소에 매핑할 수 있습니다. 예는 아래에 나와 있습니다.

```json
{
    "properties": {
        "sizeInMB": {
            "type": "integer",
            "minimum": 16,
            "maximum": 512,
            "aem:afProperties" : {
                 "sling:resourceType" : "/apps/fd/af/components/guideTextBox",
                 "guideNodeClass" : "guideTextBox"
             }
        }
    },
    "required": [ "sizeInMB" ],
    "additionalProperties": false
}
```

## 양식 개체 {#configure-scripts-or-expressions-for-form-objects}에 대한 스크립트 또는 표현식을 구성합니다

JavaScript는 적응형 양식의 표현식 언어입니다. 모든 표현식은 유효한 JavaScript 표현식이며, 적응형 양식 스크립팅 모델 API를 사용합니다. 양식 개체를 미리 구성하여 양식 이벤트에서 ](adaptive-form-expressions.md)식을 평가할 수 있습니다.[

aem:afproperties 속성을 사용하여 적응형 양식 구성 요소에 대한 적응형 양식 표현식 또는 스크립트를 미리 구성합니다. 예를 들어 초기화 이벤트가 트리거되면 아래 코드는 전화 필드의 값을 설정하고 값을 로그에 인쇄합니다.

```json
"telephone": {
  "type": "string",
  "pattern": "/\\d{10}/",
  "aem:affKeyword": ["phone", "telephone","mobile phone", "work phone", "home phone", "telephone number", "telephone no", "phone number"],
  "description": "Telephone Number",
  "aem:afProperties" : {
    "sling:resourceType" : "fd/af/components/guidetelephone",
    "guideNodeClass" : "guideTelephone",
    "events": {
      "Initialize" : "this.value = \"1234567890\"; console.log(\"ef:gh\") "
    }
  }
}
```

양식 개체에 대한 스크립트나 식을 구성하려면 [forms-power-user 그룹](forms-groups-privileges-tasks.md)의 구성원이어야 합니다. 아래 표에는 적응형 양식 구성 요소에 대해 지원되는 모든 스크립트 이벤트가 나열되어 있습니다.

<table>
 <tbody>
  <tr>
   <th><strong></strong>구성 요소 \ 이벤트</th>
   <th><br /> 초기화 </th>
   <td>연산</td>
   <td>가시성</td>
   <td>유효성 검사</td>
   <td>활성화됨</td>
   <td>valueCommit</td>
   <td>클릭 </td>
   <td>옵션</td>
  </tr>
  <tr>
   <td>텍스트 필드</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>숫자 필드</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>숫자 스텝퍼</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>라디오 단추</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>전화 번호</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>전환</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>단추</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
  </tr>
  <tr>
   <td>체크 상자</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>드롭다운</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>이미지 선택</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>데이터 입력 필드</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>날짜 선택</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>이메일</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>첨부 파일</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>이미지</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Draw</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>패널</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

JSON에서 이벤트를 사용하는 일부 예제는 초기화 이벤트 시 필드를 숨기고 값 커밋 이벤트에서 다른 필드의 값을 구성하는 것입니다. 스크립트 이벤트에 대한 표현식 만들기에 대한 자세한 내용은 [적응형 양식 표현식](adaptive-form-expressions.md)을 참조하십시오.

다음은 이전에 언급된 예에 대한 샘플 JSON 코드입니다.

### 초기화 이벤트 {#hiding-a-field-on-initialize-event} 시 필드 숨기기

```json
"name": {
    "type": "string",
    "aem:afProperties": {
        "events" : {
            "Initialize" : "this.visible = false;"
        }
    }
}
```

#### 값 커밋 이벤트 {#configure-value-of-another-field-on-value-commit-event}에 대한 다른 필드의 값 구성

```json
"Income": {
    "type": "object",
    "properties": {
        "monthly": {
            "type": "number",
            "aem:afProperties": {
                "events" : {
                    "Value Commit" : "IncomeYearly.value = this.value * 12;"
                }
            }
        },
        "yearly": {
            "type": "number",
            "aem:afProperties": {
                "name": "IncomeYearly"
            }
        }
    }
}
```

## 적응형 양식 구성 요소 {#limit-acceptable-values-for-an-adaptive-form-component} 의 허용 가능한 값 제한

JSON 스키마 요소에 다음 제한 사항을 추가하여 적응형 양식 구성 요소에 허용 가능한 값을 제한할 수 있습니다.

<table>
 <tbody>
  <tr>
   <td><p><strong> 스키마 속성</strong></p> </td>
   <td><p><strong>데이터 유형</strong></p> </td>
   <td><p><strong>설명</strong></p> </td>
   <td><p><strong>구성 요소</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>maximum</code></p> </td>
   <td><p>문자열</p> </td>
   <td><p>숫자 값 및 날짜에 대한 상한을 지정합니다. 기본적으로 최대값이 포함됩니다.</p> </td>
   <td>
    <ul>
     <li>숫자 상자</li>
     <li>숫자 스텝퍼<br /> </li>
     <li>날짜 선택</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minimum</code></p> </td>
   <td><p>문자열</p> </td>
   <td><p>숫자 값 및 날짜에 대해 하한 값을 지정합니다. 기본적으로 최소값이 포함됩니다.</p> </td>
   <td>
    <ul>
     <li>숫자 상자</li>
     <li>숫자 스텝퍼</li>
     <li>날짜 선택</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMaximum</code></p> </td>
   <td><p>부울</p> </td>
   <td><p>true일 경우 양식의 구성 요소에 지정된 숫자 값 또는 날짜는 최대 속성에 지정된 숫자 값 또는 날짜보다 작아야 합니다.</p> <p>false인 경우 양식의 구성 요소에 지정된 숫자 값 또는 날짜가 최대 속성에 대해 지정된 숫자 값 또는 날짜보다 작거나 같아야 합니다.</p> </td>
   <td>
    <ul>
     <li>숫자 상자</li>
     <li>숫자 스텝퍼</li>
     <li>날짜 선택</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMinimum</code></p> </td>
   <td><p>부울</p> </td>
   <td><p>true일 경우 양식의 구성 요소에 지정된 숫자 값 또는 날짜는 최소 속성에 지정된 숫자 값 또는 날짜보다 커야 합니다.</p> <p>false인 경우 양식의 구성 요소에 지정된 숫자 값 또는 날짜가 최소 속성에 지정된 숫자 값 또는 날짜보다 크거나 같아야 합니다.</p> </td>
   <td>
    <ul>
     <li>숫자 상자</li>
     <li>숫자 스텝퍼</li>
     <li>날짜 선택</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minLength</code></p> </td>
   <td><p>문자열</p> </td>
   <td><p>구성 요소에 허용되는 최소 문자 수를 지정합니다. 최소 길이는 0보다 크거나 같아야 합니다.</p> </td>
   <td>
    <ul>
     <li>텍스트 상자</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>maxLength</code></td>
   <td>문자열</td>
   <td>구성 요소에서 허용되는 최대 문자 수를 지정합니다. 최대 길이는 0보다 크거나 같아야 합니다.</td>
   <td>
    <ul>
     <li>텍스트 상자</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>pattern</code></p> </td>
   <td><p>문자열</p> </td>
   <td><p>문자의 시퀀스를 지정합니다. 구성 요소는 문자가 지정된 패턴을 준수하는 경우 문자를 허용합니다.</p> <p>패턴 속성은 해당 적응형 양식 구성 요소의 유효성 검사 패턴에 매핑됩니다.</p> </td>
   <td>
    <ul>
     <li>XSD 스키마에 매핑되는 모든 적응형 양식 구성 요소 </li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>maxItems</code></td>
   <td>문자열</td>
   <td>배열에 있는 최대 항목 수를 지정합니다. 최대 항목은 0보다 크거나 같아야 합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>minItems</code></td>
   <td>문자열</td>
   <td>배열에 있는 최소 항목 수를 지정합니다. 최소 항목은 0보다 크거나 같아야 합니다.</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 지원되지 않는 구문 {#non-supported-constructs}

적응형 양식은 다음 JSON 스키마 구문을 지원하지 않습니다.

* Null 유형
* 및 와 같은 결합 유형
* 하나, 임의, 모두, 아님
* 단일 배열만 지원됩니다. 따라서 항목 제약 조건은 개체가 되고 배열이 아니어야 합니다.

## FAQ {#frequently-asked-questions}

**반복 가능한 하위 양식(minOccourse 또는 maxOccurts 값이 1보다 큼)에 대해 하위 양식의 개별 요소(복잡한 형식에서 생성된 구조)를 드래그할 수 없는 이유는 무엇입니까?**

반복 가능한 하위 양식에서는 전체 하위 폼을 사용해야 합니다. 선택적 필드만 원하는 경우 전체 구조를 사용하고 원하지 않는 필드를 삭제합니다.

**컨텐츠 파인더에는 구조가 매우 복잡합니다. 특정 요소를 찾으려면 어떻게 해야 합니까?**

다음 두 가지 옵션이 있습니다.

* 트리 구조를 스크롤합니다.
* 검색 상자를 사용하여 요소를 찾습니다

**JSON 스키마 파일의 확장명은 무엇입니까?**

JSON 스키마 파일 확장명은 .schema.json이어야 합니다. 예: &lt;filename>.schema.json.
