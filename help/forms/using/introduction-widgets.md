---
title: 적응형 및 HTML5 양식을 위한 모양 프레임워크
seo-title: 적응형 및 HTML5 양식을 위한 모양 프레임워크
description: 모바일 Forms에서 양식 템플릿을 HTML5 양식으로 렌더링할 수 있습니다. 이러한 양식은 모양을 위해 jQuery, Background.js 및 밑줄.js 파일을 사용하고 스크립팅을 활성화합니다.
seo-description: 모바일 Forms에서 양식 템플릿을 HTML5 양식으로 렌더링할 수 있습니다. 이러한 양식은 모양을 위해 jQuery, Background.js 및 밑줄.js 파일을 사용하고 스크립팅을 활성화합니다.
uuid: 183b8d71-44fc-47bf-8cb2-1cf920ffd23a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 3c2a44a7-24e7-49ee-bf18-eab0e44efa42
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 2%

---


# 응용 및 HTML5 양식의 모양 프레임워크 {#appearance-framework-for-adaptive-and-html-forms}

Forms(적응형 양식 및 HTML5 양식)은 모양과 스크립팅을 위해 [jQuery](https://jquery.com/), [Background.js](https://backbonejs.org/) 및 [밑줄.js](https://underscorejs.org/) 라이브러리를 사용합니다. 양식에서 모든 대화형 요소(예: 필드 및 단추)에 대해 [jQuery UI](https://jqueryui.com/) **위젯** 아키텍처를 사용합니다. 이 아키텍처를 통해 양식 개발자는 Forms에서 사용 가능한 다양한 jQuery 위젯 및 플러그인을 사용할 수 있습니다. leadDigits/trailDigits 제한 또는 그림 조항 구현과 같은 사용자의 데이터를 캡처하는 동안 양식별 로직을 구현할 수도 있습니다. 양식 개발자는 사용자 정의 api를 만들어 사용하여 데이터 캡처 경험을 향상시키고 사용자에게 더 친숙하게 만들 수 있습니다.

이 문서는 jQuery 및 jQuery 위젯에 대한 충분한 지식이 있는 개발자를 위한 것입니다. 모양 프레임워크에 대한 통찰력을 제공하고 개발자는 양식 필드에 대한 대체 모양을 만들 수 있습니다.

모양 프레임워크는 다양한 옵션, 이벤트(트리거) 및 기능에 의존하여 양식과 사용자 상호 작용을 캡처하고 모델 변경에 응답하여 최종 사용자에게 알립니다. 추가:

* 프레임워크에서는 필드 모양을 위한 일련의 옵션을 제공합니다. 이러한 옵션은 키-값 쌍이며 두 가지 범주로 구분됩니다.공통 옵션 및 필드 유형별 옵션.
* 계약의 일부로 나타나는 모양은 출입과 종료와 같은 일련의 이벤트를 트리거합니다.
* 함수 집합을 구현하려면 모양이 필요합니다. 일부 함수는 일반적으로 사용되는 반면 다른 함수는 필드 유형 함수와 관련이 있습니다.

## 일반 옵션 {#common-options}

다음은 글로벌 옵션 설정입니다. 이러한 옵션은 모든 필드에 사용할 수 있습니다.

<table>
 <tbody>
  <tr>
   <th>속성 </th>
   <th>설명</th>
  </tr>
  <tr>
   <td>이름</td>
   <td>스크립트 표현식에서 이 개체나 이벤트를 지정하는 데 사용되는 식별자입니다. 예를 들어 이 속성은 호스트 응용 프로그램의 이름을 지정합니다.</td>
  </tr>
  <tr>
   <td>정렬 단추</td>
   <td>필드의 실제 값. </td>
  </tr>
  <tr>
   <td>displayValue</td>
   <td>이 필드 값이 표시됩니다. </td>
  </tr>
  <tr>
   <td>screenReaderText</td>
   <td>화면 Reader은 이 값을 사용하여 필드에 대한 정보를 나레이트합니다. 양식에서 값을 제공하고 값을 재정의할 수 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>tabIndex</td>
   <td>양식의 탭 시퀀스에 있는 필드의 위치입니다. 양식의 기본 탭 순서를 변경하려는 경우에만 tabIndex를 무시합니다.</td>
  </tr>
  <tr>
   <td>역할</td>
   <td>요소의 역할(예: 제목 또는 표).</td>
  </tr>
  <tr>
   <td>높이</td>
   <td>위젯의 높이입니다. 픽셀 단위로 지정됩니다. </td>
  </tr>
  <tr>
   <td>너비</td>
   <td>위젯의 폭입니다. 픽셀 단위로 지정됩니다.</td>
  </tr>
  <tr>
   <td>access</td>
   <td>하위 폼과 같이 컨테이너 개체의 콘텐츠에 액세스하는 데 사용되는 컨트롤입니다.</td>
  </tr>
  <tr>
   <td>paraStyles</td>
   <td>위젯에 대한 XFA 요소의 para 속성입니다.</td>
  </tr>
  <tr>
   <td>dir</td>
   <td>텍스트 방향 가능한 값은 ltr(왼쪽에서 오른쪽) 및 rtl(오른쪽에서 왼쪽) 입니다.</td>
  </tr>
 </tbody>
</table>

이러한 옵션 외에도 프레임워크에서는 필드 유형에 따라 다양한 다른 옵션을 제공합니다. 필드별 옵션에 대한 자세한 내용은 아래에 나와 있습니다.

### 양식 프레임워크 {#interaction-with-forms-framework}과의 상호 작용

양식 프레임워크와 상호 작용하기 위해 위젯은 양식 스크립트가 작동하도록 일부 이벤트를 트리거합니다. 위젯이 이러한 이벤트를 throw하지 않으면 해당 필드에 대해 양식에 작성된 스크립트 중 일부가 작동하지 않습니다.

#### 위젯 {#events-triggered-by-widget}에 의해 트리거된 이벤트

<table>
 <tbody>
  <tr>
   <th>이벤트 </th>
   <th>설명</th>
  </tr>
  <tr>
   <td>XFA_ENTER_EVENT</td>
   <td>이 이벤트는 필드가 포커스될 때마다 트리거됩니다. 필드에서 "enter" 스크립트를 실행할 수 있습니다. 이벤트를 트리거하는 구문은<br />(widget)입니다._trigger(xfalib.ut.XfaUtil.prototype.XFA_ENTER_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_EXIT_EVENT</td>
   <td>이 이벤트는 사용자가 필드를 떠날 때마다 트리거됩니다. 엔진은 필드의 값을 설정하고 해당 "종료" 스크립트를 실행할 수 있습니다. 이벤트를 트리거하는 구문은<br />(widget)입니다._trigger(xfalib.ut.XfaUtil.prototype.XFA_EXIT_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_CHANGE_EVENT</td>
   <td>이 이벤트는 엔진이 필드에 작성된 "변경" 스크립트를 실행할 수 있도록 트리거됩니다. 이벤트를 트리거하는 구문은<br />(widget)입니다._trigger(xfalib.ut.XfaUtil.prototype.XFA_CHANGE_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_CLICK_EVENT</td>
   <td>이 이벤트는 필드를 클릭할 때마다 트리거됩니다. 이를 통해 엔진은 필드에 작성된 "click" 스크립트를 실행할 수 있습니다. 이벤트를 트리거하는 구문은<br />(widget)입니다._trigger(xfalib.ut.XfaUtil.prototype.XFA_CLICK_EVENT)<br /> </td>
  </tr>
 </tbody>
</table>

#### 위젯 {#apis-implemented-by-widget}에 의해 구현된 API

모양 프레임워크는 사용자 정의 위젯에 구현된 위젯의 일부 기능을 호출합니다. 위젯은 다음 기능을 구현해야 합니다.

<table>
 <tbody>
  <tr>
   <th>함수</th>
   <th>설명</th>
  </tr>
  <tr>
   <td>focus:function()</td>
   <td>현장 집중</td>
  </tr>
  <tr>
   <td>클릭:function()</td>
   <td>필드에 초점을 맞추고 XFA_CLICK_EVENT를 호출합니다.</td>
  </tr>
  <tr>
   <td><p>markError:function(errorMessage, errorType)<br /> <br /> <em>rMessage:문자열 </em>오류<br /> <em>errorType:string ("warning"/"error")</em></p> <p><strong>참고</strong>:HTML5 양식에만 해당됩니다.</p> </td>
   <td>위젯에 오류 메시지와 오류 유형을 전송합니다. 위젯에 오류가 표시됩니다.</td>
  </tr>
  <tr>
   <td><p>clearError:function()</p> <p><strong>참고</strong>:HTML5 양식에만 해당됩니다.</p> </td>
   <td>필드의 오류가 수정된 경우 호출됩니다. 위젯이 오류를 숨깁니다.</td>
  </tr>
 </tbody>
</table>

## 필드 {#options-specific-to-type-of-field} 유형에 대한 옵션

모든 사용자 정의 위젯은 위의 사양을 따라야 합니다. 서로 다른 필드의 기능을 사용하려면 위젯이 특정 필드에 대한 지침을 따라야 합니다.

### 텍스트 편집:텍스트 필드 {#textedit-text-field}

<table>
 <tbody>
  <tr>
   <th>옵션</th>
   <th>설명</th>
  </tr>
  <tr>
   <td>다중 라인</td>
   <td>필드가 새 행 문자 입력을 지원하는 경우 true, 그렇지 않으면 false입니다.</td>
  </tr>
  <tr>
   <td>maxChars</td>
   <td>필드에 입력할 수 있는 최대 문자 수입니다.</td>
  </tr>
  <tr>
   <td><p>limitLengthToVisibleArea</p> <p><strong>참고</strong>:HTML5 양식에만 적용 가능</p> </td>
   <td>텍스트 너비가 위젯의 너비를 초과할 때 텍스트 필드의 동작을 지정합니다.</td>
  </tr>
 </tbody>
</table>

### 선택 목록:DropDownList, ListBox {#choicelist-dropdownlist-listbox}

<table>
 <tbody>
  <tr>
   <th>옵션</th>
   <th>설명</th>
  </tr>
  <tr>
   <td>정렬 단추<br /> </td>
   <td>선택한 값의 배열.<br /> </td>
  </tr>
  <tr>
   <td>항목<br /> </td>
   <td>옵션으로 표시할 개체의 배열입니다. 각 개체에는 <br /> save라는 두 가지 속성이 있습니다.저장할 값, 표시 값:표시할 값<br /> <br /> </td>
  </tr>
  <tr>
   <td><p>편집</p> <p><strong>참고</strong>:HTML5 양식에만 해당됩니다.<br /> </p> </td>
   <td>값이 true이면 위젯에서 사용자 지정 텍스트 항목이 활성화됩니다.<br /> </td>
  </tr>
  <tr>
   <td>displayValue<br /> </td>
   <td>표시할 값의 배열입니다.<br /> </td>
  </tr>
  <tr>
   <td>multiselect<br /> </td>
   <td>복수 선택이 허용되는 경우 true이고, 그렇지 않은 경우 false입니다.<br /> </td>
  </tr>
 </tbody>
</table>

#### API {#api}

<table>
 <tbody>
  <tr>
   <th>함수</th>
   <th>설명</th>
  </tr>
  <tr>
   <td><p>addItem:<em> function(itemValues)<br /> itemValues:표시 및 저장 값 <br /> {sDisplayVal을 포함하는 개체:&lt;displayValue&gt;, sSaveVal:&lt;save value&gt;}</em></p> </td>
   <td>목록에 항목을 추가합니다.</td>
  </tr>
  <tr>
   <td>deleteItem<em>:function(nIndex)<br /> nIndex:목록에서 제거할 항목의 인덱스<br /> </em><br /> <br /> </td>
   <td>목록에서 옵션을 삭제합니다.</td>
  </tr>
  <tr>
   <td>clearItems:<code> function()</code></td>
   <td>목록에서 모든 옵션을 지웁니다.</td>
  </tr>
 </tbody>
</table>

### 숫자 편집:NumericField, DecimalField {#numericedit-numericfield-decimalfield}

| 옵션 | 설명 |
|---|---|
| dataType | 필드의 데이터 유형을 나타내는 문자열(정수/소수). |
| leadDigits | 소수 자릿수에 허용되는 최대 행간 자리수입니다. |
| frcDigits | 소수 자릿수에 허용되는 최대 분수. |
| zero | 필드의 로케일에서 0의 문자열 표현. |
| 소수 | 필드의 로케일에서 소수점을 나타내는 문자열. |

### 확인 단추:RadioButton, CheckBox {#checkbutton-radiobutton-checkbox}

<table>
 <tbody>
  <tr>
   <th>옵션</th>
   <th>설명</th>
  </tr>
  <tr>
   <td>values</td>
   <td><p>값 배열(온/오프/중립).</p> <p>checkButton의 다른 상태에 대한 값 배열입니다. values[0]은 상태가 ON일 때의 값입니다. values[1]은 상태가 OFF일 때의 값입니다.<br /> values[2]는 상태가 NEUTRAL일 때의 값입니다. 값 배열의 길이가 state 옵션의 값과 같습니다.<br /> </p> </td>
  </tr>
  <tr>
   <td>states</td>
   <td><p>허용되는 상태 수입니다. </p> <p>적응형 양식(켜기, 끄기)과 HTML5 양식(켜기, 끄기, 중립)의 경우 2입니다.</p> </td>
  </tr>
  <tr>
   <td>상태</td>
   <td><p>요소의 현재 상태입니다.</p> <p>적응형 양식(켜기, 끄기)과 HTML5 양식(켜기, 끄기, 중립)의 경우 2입니다.</p> </td>
  </tr>
 </tbody>
</table>

### DateTimeEdit:(DateField) {#datetimeedit-datefield}

| 옵션 | 설명 |
|---|---|
| 일 | 해당 필드에 대한 현지화된 일 이름입니다. |
| 개월 | 해당 필드에 대한 지역화된 월 이름. |
| zero | 숫자 0에 대한 지역화된 텍스트입니다. |
| clearText | 지우기 단추를 위한 현지화된 텍스트입니다. |
