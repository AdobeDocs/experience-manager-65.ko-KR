---
title: 적응형 및 HTML5 양식용 외관 프레임워크
description: Mobile Forms은 양식 템플릿을 HTML 5 양식으로 렌더링합니다. 이러한 양식에서는 외형에 jQuery, Backbone.js 및 Underscore.js 파일을 사용하여 스크립팅을 활성화합니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
exl-id: 3458471a-9815-463e-8044-68631073863c
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 2%

---

# 적응형 및 HTML5 양식용 외관 프레임워크 {#appearance-framework-for-adaptive-and-html-forms}

Forms(적응형 양식 및 HTML 5 양식) 사용 [jQuery](https://jquery.com/), [Backbone.js](https://backbonejs.org/) 및 [Underscore.js](https://underscorejs.org/) 모양 및 스크립팅용 라이브러리. 양식에서는 [jQuery UI](https://jqueryui.com/) **위젯** 양식의 모든 대화형 요소(예: 필드 및 버튼)에 대한 아키텍처입니다. 이 아키텍처를 통해 양식 개발자는 Forms에서 사용 가능한 다양한 jQuery 위젯 및 플러그인을 사용할 수 있습니다. 또한 leadDigits/trailDigits 제한 사항이나 그림 절 구현과 같은 사용자의 데이터를 캡처하는 동안 양식별 논리를 구현할 수도 있습니다. 양식 개발자는 사용자 정의 응용 프로그램을 만들고 사용하여 데이터 캡처 환경을 개선하고 보다 사용자 친화적으로 만들 수 있습니다.

이 문서는 jQuery 및 jQuery 위젯에 대한 지식이 풍부한 개발자를 위한 것입니다. 모양 프레임워크에 대한 통찰력을 제공하고 개발자가 양식 필드에 대한 대체 모양을 만들 수 있도록 합니다.

모양 프레임워크는 다양한 옵션, 이벤트(트리거) 및 함수를 사용하여 양식과의 사용자 상호 작용을 캡처하고 모델 변경 사항에 대응하여 최종 사용자에게 알립니다. 또한

* 프레임워크는 필드 모양을 위한 옵션 세트를 제공합니다. 이러한 옵션은 키-값 쌍이며 공통 옵션 및 필드 유형별 옵션의 두 가지 범주로 나뉩니다.
* 계약의 일부로 외관이 Enter 및 Exit와 같은 이벤트 세트를 트리거합니다.
* 기능 세트를 구현하려면 모양새가 필요합니다. 일부 함수는 공통되지만 다른 함수는 필드 유형 함수에만 적용됩니다.

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
   <td>스크립트 표현식에서 이 개체 또는 이벤트를 지정하는 데 사용되는 식별자입니다. 예를 들어 이 속성은 호스트 응용 프로그램의 이름을 지정합니다.</td>
  </tr>
  <tr>
   <td>값</td>
   <td>필드의 실제 값. </td>
  </tr>
  <tr>
   <td>displayValue</td>
   <td>이 필드 값이 표시됩니다. </td>
  </tr>
  <tr>
   <td>screenReaderText</td>
   <td>화면 Reader은 이 값을 사용하여 필드에 대한 정보를 내레이팅합니다. 양식에서 값을 제공하며 사용자는 값을 재정의할 수 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>tabIndex</td>
   <td>양식의 탭 시퀀스에서 필드의 위치입니다. 양식의 기본 탭 순서를 변경하려는 경우에만 tabIndex를 재정의합니다.</td>
  </tr>
  <tr>
   <td>역할</td>
   <td>요소의 역할(예: 제목 또는 테이블).</td>
  </tr>
  <tr>
   <td>높이</td>
   <td>위젯의 높이입니다. 픽셀로 지정됩니다. </td>
  </tr>
  <tr>
   <td>폭</td>
   <td>위젯의 폭입니다. 픽셀로 지정됩니다.</td>
  </tr>
  <tr>
   <td>액세스</td>
   <td>하위 폼과 같은 컨테이너 개체의 내용에 액세스하는 데 사용되는 컨트롤입니다.</td>
  </tr>
  <tr>
   <td>paraStyle</td>
   <td>위젯에 대한 XFA 요소의 para 속성입니다.</td>
  </tr>
  <tr>
   <td>dir</td>
   <td>텍스트 방향. 가능한 값은 ltr(왼쪽에서 오른쪽) 및 rtl(오른쪽에서 왼쪽)입니다.</td>
  </tr>
 </tbody>
</table>

이러한 옵션 외에도 프레임워크는 필드 유형에 따라 달라지는 몇 가지 다른 옵션을 제공합니다. 필드별 옵션에 대한 세부 사항은 아래에 나와 있습니다.

### 양식 프레임워크와의 상호 작용 {#interaction-with-forms-framework}

Forms 프레임워크와 상호 작용하기 위해 위젯은 일부 이벤트를 트리거하여 양식 스크립트가 작동할 수 있도록 합니다. 위젯에서 이러한 이벤트를 발생시키지 않는 경우 해당 필드에 대한 양식으로 작성된 일부 스크립트가 작동하지 않습니다.

#### 위젯에 의해 트리거된 이벤트 {#events-triggered-by-widget}

<table>
 <tbody>
  <tr>
   <th>이벤트 </th>
   <th>설명</th>
  </tr>
  <tr>
   <td>XFA_ENTER_EVENT</td>
   <td>이 이벤트는 필드가 포커스에 있을 때마다 트리거됩니다. 필드에서 "enter" 스크립트를 실행할 수 있습니다. 이벤트를 트리거하는 구문은 다음과 같습니다<br /> (위젯)._trigger(xfalib.ut.XfaUtil.prototype.XFA_ENTER_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_EXIT_EVENT</td>
   <td>이 이벤트는 사용자가 필드를 떠날 때마다 트리거됩니다. 이 옵션을 통해 엔진은 필드의 값을 설정하고 "종료" 스크립트를 실행할 수 있습니다. 이벤트를 트리거하는 구문은 다음과 같습니다<br /> (위젯)._trigger(xfalib.ut.XfaUtil.prototype.XFA_EXIT_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_CHANGE_EVENT</td>
   <td>이 이벤트는 엔진이 필드에 작성된 "변경" 스크립트를 실행할 수 있도록 트리거됩니다. 이벤트를 트리거하는 구문은 다음과 같습니다<br /> (위젯)._trigger(xfalib.ut.XfaUtil.prototype.XFA_CHANGE_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_CLICK_EVENT</td>
   <td>이 이벤트는 필드를 클릭할 때마다 트리거됩니다. 이 옵션을 통해 엔진은 필드에 쓰여진 "click" 스크립트를 실행할 수 있습니다. 이벤트를 트리거하는 구문은 다음과 같습니다<br /> (위젯)._trigger(xfalib.ut.XfaUtil.prototype.XFA_CLICK_EVENT)<br /> </td>
  </tr>
 </tbody>
</table>

#### 위젯으로 구현된 API {#apis-implemented-by-widget}

모양 프레임워크는 사용자 정의 위젯에서 구현되는 위젯의 일부 기능을 호출합니다. 위젯은 다음 기능을 구현해야 합니다.

<table>
 <tbody>
  <tr>
   <th>함수</th>
   <th>설명</th>
  </tr>
  <tr>
   <td>focus: function()</td>
   <td>필드에 초점을 맞춥니다.</td>
  </tr>
  <tr>
   <td>click: function()</td>
   <td>필드에 포커스를 두고 XFA_CLICK_EVENT를 호출합니다.</td>
  </tr>
  <tr>
   <td><p>markError:function(errorMessage, errorType)<br /> <br /> <em>오류 메시지: 문자열 </em>오류 표시<br /> <em>errorType: 문자열("warning"/"error")</em></p> <p><strong>참고</strong>: HTML 5 양식에만 적용됩니다.</p> </td>
   <td>위젯에 오류 메시지와 오류 유형을 보냅니다. 위젯에 오류가 표시됩니다.</td>
  </tr>
  <tr>
   <td><p>clearError: function()</p> <p><strong>참고</strong>: HTML 5 양식에만 적용됩니다.</p> </td>
   <td>필드의 오류가 수정된 경우 호출됩니다. 위젯은 오류를 숨깁니다.</td>
  </tr>
 </tbody>
</table>

## 필드 유형별 옵션 {#options-specific-to-type-of-field}

모든 사용자 정의 위젯은 위의 사양을 준수해야 합니다. 다양한 필드의 기능을 사용하려면 위젯이 해당 특정 필드에 대한 지침을 준수해야 합니다.

### TextEdit: 텍스트 필드 {#textedit-text-field}

<table>
 <tbody>
  <tr>
   <th>옵션</th>
   <th>설명</th>
  </tr>
  <tr>
   <td>여러 행</td>
   <td>필드가 줄 바꿈 문자 입력을 지원하는 경우 true이고, 그렇지 않으면 false입니다.</td>
  </tr>
  <tr>
   <td>maxChars</td>
   <td>필드에 입력할 수 있는 최대 문자 수.</td>
  </tr>
  <tr>
   <td><p>limitLengthToVisibleArea</p> <p><strong>참고</strong>: HTML 5 양식에만 적용됩니다.</p> </td>
   <td>텍스트 너비가 위젯의 너비를 초과할 때의 텍스트 필드 동작을 지정합니다.</td>
  </tr>
 </tbody>
</table>

### 선택 목록: DropDownList, ListBox {#choicelist-dropdownlist-listbox}

<table>
 <tbody>
  <tr>
   <th>옵션</th>
   <th>설명</th>
  </tr>
  <tr>
   <td>값<br /> </td>
   <td>선택한 값의 배열입니다.<br /> </td>
  </tr>
  <tr>
   <td>개 항목<br /> </td>
   <td>옵션으로 표시할 개체의 배열입니다. 각 객체에는 두 개의 속성 -<br /> 저장: 저장할 값, 표시할 값: 표시할 값입니다.<br /> <br /> </td>
  </tr>
  <tr>
   <td><p>편집 가능</p> <p><strong>참고</strong>: HTML 5 양식에만 적용됩니다.<br /> </p> </td>
   <td>값이 true이면 위젯에서 사용자 정의 텍스트 항목을 사용할 수 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>displayValue<br /> </td>
   <td>표시할 값의 배열입니다.<br /> </td>
  </tr>
  <tr>
   <td>다중 선택<br /> </td>
   <td>다중 선택이 허용되면 true이고, 그렇지 않으면 false입니다.<br /> </td>
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
   <td><p>추가 항목:<em> function(itemValues)<br /> itemValues: 표시 및 저장 값이 포함된 객체 <br /> {sDisplayVal: &lt;displayvalue&gt;, sSaveVal: &lt;save value=""&gt;}</em></p> </td>
   <td>항목을 목록에 추가합니다.</td>
  </tr>
  <tr>
   <td>deleteItem<em>: function(nIndex)<br /> nIndex: 목록에서 제거할 항목의 색인<br /> </em><br /> <br /> </td>
   <td>목록에서 옵션을 삭제합니다.</td>
  </tr>
  <tr>
   <td>지우기 항목:<code> function()</code></td>
   <td>목록에서 모든 옵션을 지웁니다.</td>
  </tr>
 </tbody>
</table>

### NumericEdit: NumericField, DecimalField {#numericedit-numericfield-decimalfield}

| 옵션 | 설명 |
|---|---|
| dataType | 필드의 데이터 형식을 나타내는 문자열입니다(정수/십진수). |
| leadDigits | 소수점 이하 최대 선행 자릿수입니다. |
| fracDigits | 소수점에 허용되는 최대 소수 자릿수입니다. |
| 0 | 필드의 로케일에서 0을 나타내는 문자열 표현입니다. |
| decimal | 필드의 로케일에서 십진수를 나타내는 문자열 표현입니다. |

### CheckButton: RadioButton, CheckBox {#checkbutton-radiobutton-checkbox}

<table>
 <tbody>
  <tr>
   <th>옵션</th>
   <th>설명</th>
  </tr>
  <tr>
   <td>값</td>
   <td><p>값 배열(설정/해제/중립).</p> <p>checkButton의 다양한 상태에 대한 값 배열입니다. values[0] 은 상태가 ON일 때의 값이고 values[1] 은 상태가 OFF일 때의 값입니다.<br /> values[2] 는 상태가 NEUTRAL일 때의 값입니다. 값 배열의 길이는 상태 옵션의 값과 같습니다.<br /> </p> </td>
  </tr>
  <tr>
   <td>상태</td>
   <td><p>허용되는 상태 수. </p> <p>적응형 양식에 대해 2개(켜기, 끄기) 및 HTML 5 양식에 대해 3개(켜기, 끄기, 중립).</p> </td>
  </tr>
  <tr>
   <td>시/도</td>
   <td><p>요소의 현재 상태입니다.</p> <p>적응형 양식에 대해 2개(켜기, 끄기) 및 HTML 5 양식에 대해 3개(켜기, 끄기, 중립).</p> </td>
  </tr>
 </tbody>
</table>

### DateTimeEdit: (날짜 필드) {#datetimeedit-datefield}

| 옵션 | 설명 |
|---|---|
| 일 | 해당 필드에 대한 지역화된 일 수. |
| 개월 | 해당 필드의 지역화된 월 이름. |
| 0 | 숫자 0에 대한 지역화된 텍스트입니다. |
| clearText | 지우기 단추에 대한 지역화된 텍스트입니다. |
