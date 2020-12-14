---
title: HTML5 양식에 대한 스크립팅 지원
seo-title: HTML5 양식에 대한 스크립팅 지원
description: JavaScript, FormCalc 속성 및 HTML5 Forms에서 지원되는 기타 메서드입니다.
seo-description: JavaScript, FormCalc 속성 및 HTML5 Forms에서 지원되는 기타 메서드입니다.
uuid: 697d5ec4-c818-41e4-b813-883c01b7ff3a
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 4ef78c8c-783f-4aac-a499-692cd4acef75
translation-type: tm+mt
source-git-commit: c74d9e86727f2deda62b8d1eb105b28ef4b6d184
workflow-type: tm+mt
source-wordcount: '3909'
ht-degree: 6%

---


# HTML5 양식 {#scripting-support-for-html-forms} 스크립팅 지원

HTML5 양식에 지원되는 JavaScript, FormCalc 속성 및 메서드는 다음과 같습니다.

## $event {#event}

<table>
 <tbody>
  <tr>
   <th>속성 </th>
   <th>설명<br /> </th>
   <th>예외</th>
  </tr>
  <tr>
   <td><code>prevText</code></td>
   <td>사용자의 작업에 대한 응답으로 변경하기 전에 필드의 내용을 지정합니다. 실행 취소 기능과 유사하게 이 값을 호출할 수 있습니다.</td>
   <td><p>드롭다운 및 목록 상자에 대해 작동하지 않습니다. <code>PrevText </code>다음 경우 제대로 작동하지 않습니다.</p>
    <ul>
     <li>iPad의 숫자 필드에 특수 문자 키(예: $, (,), &amp;, @ 등)를 입력할 때 </li>
     <li>날짜 필드(달력을 통해 날짜가 입력되는 경우)에 대해 <br /> </li>
    </ul> <p>스크립트를 통한 값 설정이 지원되지 않습니다.</p> </td>
  </tr>
  <tr>
   <td><code>target</code></td>
   <td>이벤트가 실행되는 객체를 지정합니다.</td>
   <td>스크립트를 통한 값 설정이 지원되지 않습니다.<br /> </td>
  </tr>
  <tr>
   <td><code>newtext</code></td>
   <td>사용자 작업에 대한 응답으로 필드가 변경된 후 필드의 내용을 지정합니다.</td>
   <td><p>다음 경우 <code>newText</code> 속성이 제대로 작동하지 않습니다.</p>
    <ul>
     <li>텍스트 선택 바꾸기 시</li>
     <li>텍스트 삭제, 복사 및 붙여넣기 시</li>
     <li>숫자 필드에 특수 문자 키(예: $, (, ), &amp;, @ 등)를 입력할 때<br /> </li>
     <li>shift+영숫자 조합을 사용하는 경우 </li>
     <li>날짜/시간 필드를 사용할 때.</li>
    </ul>
    <div>
      스크립트를 통한 값 설정이 지원되지 않습니다.
    </div> </td>
  </tr>
  <tr>
   <td>변경</td>
   <td>사용자가 작업을 수행한 직후 필드에 입력하거나 붙여넣는 값을 지정합니다. </td>
   <td><p>다음과 같은 경우 change 속성이 제대로 작동하지 않습니다.</p>
    <ul>
     <li>텍스트 선택 바꾸기 시</li>
     <li>텍스트 삭제, 복사 및 붙여넣기 시</li>
     <li>숫자 필드에 특수 문자 키(예: $, (,), &amp;, @ 등)를 입력할 때<br /> </li>
     <li>shift+영숫자 조합을 사용하는 경우 </li>
     <li>날짜/시간 필드를 사용할 때.</li>
    </ul> <p>스크립트를 통한 값 설정이 지원되지 않습니다.</p> </td>
  </tr>
  <tr>
   <td>키 아래로</td>
   <td>사용자가 화살표 키를 눌러 선택할지 여부를 결정합니다. 이 속성은 목록 상자 및 드롭다운 목록에만 사용할 수 있습니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>수정자</td>
   <td>특정 이벤트가 실행될 때 수정자 키(예: Microsoft® Windows®의 Ctrl 키)를 눌렀는지 여부를 결정합니다.</td>
   <td>없음</td>
  </tr>
 </tbody>
</table>

### $host {#host}

<table>
 <tbody>
  <tr>
   <th>속성</th>
   <th>설명</th>
   <th>예외</th>
  </tr>
  <tr>
   <td><code>apptype</code></td>
   <td>호스트의 응용 프로그램 유형을 반환합니다. 클라이언트 응용 프로그램에만 사용할 수 있습니다.</td>
   <td><code>HTML 5</code>을(를) 반환합니다.</td>
  </tr>
  <tr>
   <td><code>name</code></td>
   <td>현재 응용 프로그램의 이름을 반환합니다.</td>
   <td>브라우저 이름과 해당 버전을 반환합니다. 예를 들어 Chrome 브라우저에서 반환된 값은 <code>Chrome &lt;version&gt;.</code></td>
  </tr>
  <tr>
   <td><code>numPages</code></td>
   <td>문서의 페이지 수를 반환합니다.</td>
   <td>HTML5 양식의 페이지 매김 정책이 PDF forms 페이지 매김 정책과 동일하지 않습니다. 따라서 numPages API는 두 경우 모두에서 다른 값을 반환할 수 있습니다.</td>
  </tr>
  <tr>
   <td><code>platform</code></td>
   <td>스크립트를 실행하는 컴퓨터의 플랫폼을 나타내는 문자열을 반환합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td><code>title</code></td>
   <td>문서의 제목을 지정합니다. 클라이언트 응용 프로그램에만 사용할 수 있습니다.</td>
   <td>PDF forms의 경우처럼 양식 메타데이터 제목이 아닌 형태로 HTML 문서의 제목을 반환합니다.</td>
  </tr>
  <tr>
   <td><code>version</code></td>
   <td>현재 응용 프로그램의 버전 번호를 나타내는 문자열을 반환합니다.</td>
   <td>양식의 버전을 반환합니다.</td>
  </tr>
  <tr>
   <td><code>calculationsEnabled</code></td>
   <td>계산 스크립트가 실행되는지 여부를 지정합니다.<br /> </td>
   <td>없음</td>
  </tr>
  <tr>
   <td><code>validationsEnabled</code></td>
   <td>유효성 검사 스크립트가 실행되는지 여부를 지정합니다.<br /> </td>
   <td>없음</td>
  </tr>
  <tr>
   <td><code>pageUp</code></td>
   <td>이전 페이지로 이동합니다.</td>
   <td>HTML5 양식은 PDF 양식과 동일한 페이지 지정 정책을 따르지 않으므로 HTML5 양식의 이전 페이지는 PDF 양식의 이전 페이지와 다릅니다.</td>
  </tr>
  <tr>
   <td><code>pageDown</code></td>
   <td>양식의 다음 페이지로 이동합니다. 런타임에 pageDown 메서드를 사용합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>setFocus</code></td>
   <td>키보드 포커스를 지정된 필드에 설정합니다. 필드는 개체로 지정되거나 필드의 SOM 표현식으로 지정됩니다. 클라이언트 응용 프로그램에만 사용할 수 있습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>resetdata</code></td>
   <td>필드를 문서 내의 기본값으로 재설정합니다.</td>
   <td>기본 값으로 복원하는 대신 병합된 데이터가 있는 양식의 모든 데이터를 지웁니다.</td>
  </tr>
  <tr>
   <td><code>messageBox</code></td>
   <td>화면에 대화 상자를 표시합니다. 클라이언트 응용 프로그램에만 사용할 수 있습니다.</td>
   <td>예/아니요 유형의 메시지 상자가 확인/취소로 변환됩니다. 단추가 3개인 메시지 상자는 지원되지 않습니다.</td>
  </tr>
  <tr>
   <td>currentPage</td>
   <td><p>런타임에 문서의 현재 활성 페이지를 설정합니다.</p> <p>페이지 값은 0을 기반으로 하므로 문서의 첫 번째 페이지에서 값 0을 반환합니다.</p> <p>layout:ready가 클라이언트에서 실행될 때 currentPage 속성을 사용할 수 있습니다. 그러나 레이아웃:ready가 서버에서 실행되는 경우에는 양식 레이아웃이 실행되기 전까지 속성이 실행되지 않으므로 사용할 수 없습니다.</p> </td>
   <td>없음</td>
  </tr>
 </tbody>
</table>

### 필드 {#field}

<table>
 <tbody>
  <tr>
   <th><strong><span>속성</span></strong></th>
   <th><strong><span>설명<br /> </span></strong></th>
   <th><strong><span>예외</span></strong></th>
  </tr>
  <tr>
   <td><code>presence</code></td>
   <td>처리 과정의 여러 단계에서 연관된 객체의 기여도를 제어합니다. 객체가 컨테이너인 경우 컨테이너의 내용은 이 컨트롤이 적용되는 모든 제한을 상속합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td><code>access</code></td>
   <td>콘텐츠에 대한 사용자 액세스를 제어합니다.</td>
   <td>제외 그룹에 대해 작동하지 않습니다. 또한 HTML5 양식은 비대화형 및 보호된 개체에 동일한 처리를 제공합니다.<br /> </td>
  </tr>
  <tr>
   <td><code>name</code></td>
   <td>스크립트 표현식에서 이 요소를 식별하는 데 사용되는 식별자입니다.</td>
   <td>HTML5 양식에서는 개체의 이름 속성을 설정할 수 없습니다. HTML5 양식에 대한 읽기 전용 속성입니다.</td>
  </tr>
  <tr>
   <td><code>value</code></td>
   <td>단일 데이터 콘텐츠 단위를 포함하는 콘텐츠 요소입니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td><code>rawValue</code></td>
   <td>이 필드의 서식 없는 값을 지정합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td><code>formattedValue</code></td>
   <td>이 필드의 서식 있는 값을 지정합니다.</td>
   <td>스크립트를 통해 <code>formattedValue</code> 설정이 지원되지 않습니다.</td>
  </tr>
  <tr>
   <td><code>editValue</code></td>
   <td>이 필드의 편집 값을 지정합니다.</td>
   <td>스크립트를 통해 <code>editValue </code>을(를) 설정할 수 없습니다.</td>
  </tr>
  <tr>
   <td><code>formatMessage</code></td>
   <td>이 필드의 형식 유효성 검사 메시지 문자열을 지정합니다.</td>
   <td>스크립트를 통해 <code>formatMessage </code>을(를) 설정할 수 없습니다.</td>
  </tr>
  <tr>
   <td><code>fillcolor</code></td>
   <td>이 필드의 배경색 값을 지정합니다. border.fill.presence 속성을 별도로 표시되도록 설정해야 합니다.</td>
   <td>필드의 기본 색상이 올바로 반환되지 않습니다.</td>
  </tr>
  <tr>
   <td><code>border</code></td>
   <td>border 객체는 객체를 둘러싸는 테두리에 대해 설명합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>ui</code></td>
   <td>ui 객체에는 양식 객체의 사용자 인터페이스 설명이 포함됩니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>mandatory</code></td>
   <td>필드의 nullTest 값을 지정합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>borderColor</code></td>
   <td>이 필드의 테두리 색상 값을 지정합니다. border.edge.presence 속성을 별도로 표시되도록 설정해야 합니다.</td>
   <td>필드의 기본 테두리 색상을 올바로 반환하지 않습니다.</td>
  </tr>
  <tr>
   <td><code>length</code></td>
   <td>목록의 항목 수입니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td><code>addItem</code></td>
   <td>현재 필드에 새 항목을 추가합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td><code>clearItem</code></td>
   <td>필드에서 모든 항목을 제거합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td><code>boundItem</code></td>
   <td>드롭다운 목록 또는 목록 상자의 특정 표시 항목의 바인딩 값을 가져옵니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td><code>execCalculate</code></td>
   <td>필드의 계산 스크립트를 실행합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td><code>execValidate</code></td>
   <td>필드의 유효성 검사 스크립트를 실행합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td><code>execEvent</code></td>
   <td>객체의 이벤트 스크립트를 실행합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td><code>getItemState</code></td>
   <td>지정된 항목의 선택 상태를 반환합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td><code>setItemState</code></td>
   <td>지정된 항목의 선택 상태를 설정합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td><code>getDisplayItem</code></td>
   <td>지정된 항목 인덱스에 대한 항목 표시 텍스트를 검색합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td><code>getSaveItem</code></td>
   <td>지정된 항목 인덱스에 대한 데이터 값을 검색합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td><code>deleteItem</code></td>
   <td>지정된 인덱스의 항목을 삭제합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td><code>setItems</code></td>
   <td>현재 필드에 지정된 항목을 설정합니다. 기존 항목을 대체합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>h</td>
   <td>레이아웃의 높이 측정입니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>쓰기</td>
   <td>레이아웃의 너비를 지정하는 측정입니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>x</td>
   <td>배치된 레이아웃으로 배치할 때 부모 컨테이너의 왼쪽 위 모서리를 기준으로 컨테이너 기준점의 x 좌표를 지정합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>y</td>
   <td>배치된 레이아웃으로 배치할 때 부모 컨테이너의 왼쪽 위 모서리를 기준으로 한 컨테이너 기준점의 y 좌표를 지정합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>caption</td>
   <td>캡션 개체는 양식 디자인 개체와 관련된 설명 레이블을 설명합니다.<br /> </td>
   <td>없음</td>
  </tr>
  <tr>
   <td>유효성 검사</td>
   <td>유효성 검사 객체는 사용자가 제공한 양식의 데이터의 유효성 검사를 제어합니다. 양식 수명 동안 유효성 검사 객체를 여러 번 활성화할 수 있습니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>parentSubform</td>
   <td>이 필드의 상위 하위 양식(페이지)을 지정합니다.</td>
   <td>미리 코딩되지 않은 첫 번째 하위 폼을 반환하는 대신 항상 부모 하위 폼을 반환합니다.<br /> </td>
  </tr>
  <tr>
   <td>selectedIndex</td>
   <td>처음 선택한 항목의 인덱스입니다.</td>
   <td>없음</td>
  </tr>
 </tbody>
</table>

## 양식 {#form}

| **속성** | **설명** | **예외** |
|---|---|---|
| formNodes | 지정된 데이터 개체에 바인딩된 모든 양식 모델 개체의 목록을 반환합니다. |  |

## InstanceManager {#instancemanager}

| 속성 | 설명 |
|---|---|
| `name` | 스크립트 표현식에서 이 요소를 식별하는 데 사용되는 식별자입니다. |
| `occur` | 포함하는 컨테이너에 대해 허용되는 인스턴스 수에 대한 제약 조건을 설명합니다. |
| `min` | 인스턴스화할 수 있는 최소 인스턴스 수를 지정합니다. |
| `max` | 인스턴스화할 수 있는 최대 인스턴스 수를 지정합니다. |
| `count` | 인스턴스화된 현재 인스턴스 수를 지정합니다. |
| `setInstances` | 이 노드에서 지정된 하위 양식 또는 하위 양식 세트를 추가하거나 제거합니다. |
| `addInstance` | 이 노드에 설정된 하위 폼 또는 하위 양식의 새 인스턴스를 추가합니다. |
| `removeInstance` | 이 노드에서 하위 폼 또는 하위 폼 집합을 제거합니다. |
| `moveInstance` | 양식 모델 개체의 자식 개체를 양식 모델 내의 다른 지정된 위치로 이동합니다. 개체에 대한 해당 데이터 모델 정보도 데이터 모델 내에서 재배치됩니다. |
| `insertInstance` | 이 노드에 설정된 하위 폼 또는 하위 양식의 새 인스턴스를 삽입합니다. |

## list {#list}

| 속성 | 설명 |
|---|---|
| `length` | 목록의 요소 수입니다. |
| `item` | 컬렉션에 0부터 시작하는 인덱스입니다. |
| `append` | 노드 목록의 끝에 노드를 추가합니다. |
| `remove` | 노드 목록에서 노드를 제거합니다. |
| `insert` | 노드 목록의 특정 노드 앞에 노드를 삽입합니다. |

## node {#node}

| 속성 | 설명 | 예외 |
|---|---|---|
| createNode | 유효한 클래스 이름을 기반으로 새 노드를 만듭니다. | 없음 |
| `isContainer` | 이 객체가 컨테이너 객체인지 여부를 지정합니다. | 없음 |
| `isNull` | 현재 데이터 값이 null 값인지 여부를 나타냅니다. | 없음 |
| `resolveNode` | 현재 XML 양식 객체 모델 객체로 시작하여 지정된 SOM 표현식을 평가하고 SOM 표현식에 지정된 객체의 값을 반환합니다. | 없음 |
| `resolveNodes` | 현재 XML 양식 객체 모델 객체로 시작하여 지정된 SOM 표현식을 평가하고 SOM 표현식에 지정된 객체의 값을 반환합니다. | 없음 |
| oneOfChild | 유효한 클래스 이름을 기반으로 새 노드를 만듭니다. | 없음 |
| getElement | 지정된 자식 객체를 반환합니다. | 없음 |
| getAttribute | 지정된 속성 값을 가져옵니다. | 없음 |
| setAttribute | 지정된 속성의 값을 설정합니다. | 없음 |

## 모델 {#model}

| 속성 | 설명 | 예외 |
|---|---|---|
| NA | NA | NA |

## 하위 양식 {#subform}

<table>
 <tbody>
  <tr>
   <th>속성</th>
   <th>설명</th>
   <th>예외</th>
  </tr>
  <tr>
   <td>instanceIndex</td>
   <td>인스턴스화된 다른 인스턴스를 기준으로 개체의 인덱스를 지정합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>execEvent</td>
   <td>객체의 이벤트 스크립트를 실행합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>getInvalidObjects</td>
   <td>유효성 검사 테스트에 실패한 하위 폼(포함) 내에 포함된 노드 목록을 반환합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>국경</td>
   <td>border 객체는 객체를 둘러싸는 테두리에 대해 설명합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>borderColor</td>
   <td>이 필드의 테두리 색상 값을 지정합니다. border.edge.presence 속성을 별도로 표시되도록 설정해야 합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>h</td>
   <td>레이아웃의 높이 측정입니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>쓰기</td>
   <td>레이아웃의 너비를 지정하는 측정입니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>x</td>
   <td>배치된 레이아웃으로 배치할 때 부모 컨테이너의 왼쪽 위 모서리를 기준으로 컨테이너 기준점의 x 좌표를 지정합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>y</td>
   <td>배치된 레이아웃으로 배치할 때 부모 컨테이너의 왼쪽 위 모서리를 기준으로 한 컨테이너 기준점의 y 좌표를 지정합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>유효성 검사</td>
   <td>유효성 검사 객체는 사용자가 제공한 양식의 데이터의 유효성 검사를 제어합니다. 양식 수명 동안 유효성 검사 객체를 여러 번 활성화할 수 있습니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>이름</td>
   <td>스크립트 표현식에서 이 요소를 식별하는 데 사용되는 식별자입니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>presence</td>
   <td>개체의 가시성을 지정합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>access</td>
   <td>하위 폼과 같은 컨테이너 개체의 콘텐츠에 대한 사용자 액세스를 제어합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>execValidate</td>
   <td>같은 양식 개체의 다른 인스턴스를 기준으로 하위 폼이나 하위 폼 집합의 인덱스를 계산합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>instanceManager</td>
   <td>instanceManager 개체는 양식 모델 개체의 인스턴스 만들기, 제거 및 이동을 관리합니다.<br /> </td>
   <td>없음</td>
  </tr>
 </tbody>
</table>

### 제출 {#submit}

| 속성 | 설명 |
|---|---|
| target | 데이터가 제출되는 URL. 이 속성을 생략하면 XFA 처리 응용 프로그램에서 구성 객체의 제품별 정보에 액세스하는 것과 같은 제품 특정 기술을 사용하여 URI를 얻습니다. |

## 트리 {#tree}

<table>
 <tbody>
  <tr>
   <th>속성</th>
   <th>설명</th>
   <th>예외</th>
  </tr>
  <tr>
   <td>nodes</td>
   <td>현재 객체의 모든 자식 객체 목록을 반환합니다.</td>
   <td>
    <ul>
     <li>xfa.nodes, desc에 대해 지원되지 않음</li>
     <li>PDF 및 HTML에 대해 보고된 노드 수가 다릅니다. </li>
    </ul> </td>
  </tr>
  <tr>
   <td>이름</td>
   <td>이 노드의 이름을 지정합니다.</td>
   <td>스크립트를 사용하여 이름을 설정할 수 없습니다.</td>
  </tr>
  <tr>
   <td>parent</td>
   <td>이 노드의 상위를 가져옵니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>index</td>
   <td>이름이 지정된 인스코프 하위 관계 노드 집합에서 이 노드의 위치를 반환합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>somExpression</td>
   <td>이 노드의 SOM 표현식을 가져옵니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>resolveNode</td>
   <td>현재 XML 양식 객체 모델 객체로 시작하여 지정된 SOM 표현식을 평가하고 SOM 표현식에 지정된 객체의 값을 반환합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>resolveNodes</td>
   <td>현재 XML 양식 객체 모델 객체로 시작하여 지정된 SOM 표현식을 평가하고 SOM 표현식에 지정된 객체의 값을 반환합니다.</td>
   <td>없음</td>
  </tr>
 </tbody>
</table>

## subformset {#subformset}

| 속성 | 설명 | 예외 |
|---|---|---|
| instanceManager | instanceManager 객체는 양식 모델 객체의 인스턴스 생성, 제거 및 이동을 관리합니다. | 없음 |

## content {#content}

| **속성** | **설명** | **예외** |
|---|---|---|
| isNull | 현재 데이터 값이 null 값인지 여부를 나타냅니다. |  |

## dataValue {#datavalue}

| **속성** | **설명** | **예외** |
|---|---|---|
| isNull | 현재 데이터 값이 null 값인지 여부를 나타냅니다. |  |

## edge {#edge}

<table>
 <tbody>
  <tr>
   <td><strong>속성 </strong></td>
   <td><strong>설명</strong></td>
   <td><strong>예외</strong></td>
  </tr>
  <tr>
   <td>컬러</td>
   <td>color 속성은 패턴 객체의 고유한 색상을 설명합니다.</td>
   <td>
    <ul>
     <li>기본값을 검색할 수 없습니다. </li>
     <li>변경 사항은 모델에 반영되며 스크립팅에는 사용할 수 있지만 HTML 요소와 동기화되지 않습니다. 따라서 변경 사항이 UI에 반영되지 않습니다.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## fill {#fill}

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>설명</strong></td>
   <td><strong>예외</strong></td>
  </tr>
  <tr>
   <td>컬러</td>
   <td>색상 속성은 고유한 칠 색상을 정의합니다.</td>
   <td>
    <ul>
     <li>기본값을 검색할 수 없습니다. </li>
     <li>변경 사항은 모델에 반영되며 스크립팅에는 사용할 수 있지만 HTML 요소와 동기화되지 않습니다. 따라서 변경 사항이 UI에 반영되지 않습니다.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 선형 {#linear}

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>설명</strong></td>
   <td><strong>예외</strong></td>
  </tr>
  <tr>
   <td>컬러</td>
   <td>color 속성은 양식의 선형 그레이디언트 채우기에 대한 고유한 색상을 설명합니다.</td>
   <td>
    <ul>
     <li>기본값을 검색할 수 없습니다. </li>
     <li>변경 사항은 모델에 반영되며 스크립팅에는 사용할 수 있지만 HTML 요소와 동기화되지 않습니다. 따라서 변경 사항이 UI에 반영되지 않습니다.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## line {#line}

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>설명</strong></td>
   <td><strong>예외</strong></td>
  </tr>
  <tr>
   <td>edge</td>
   <td>가장자리 개체는 테두리 또는 사각형의 호, 선 또는 한 면을 설명합니다.<br /> </td>
   <td>색상, 대문자 등과 같은 속성은 지원되지 않습니다.<br /> </td>
  </tr>
 </tbody>
</table>

## pattern {#pattern}

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>설명</strong></td>
   <td><strong>예외</strong></td>
  </tr>
  <tr>
   <td>컬러</td>
   <td>color 속성은 패턴 객체의 고유한 색상을 설명합니다. </td>
   <td>
    <ul>
     <li>기본값을 검색할 수 없습니다. </li>
     <li>변경 사항은 모델에 반영되며 스크립팅에는 사용할 수 있지만 HTML 요소와 동기화되지 않습니다. 따라서 변경 사항이 UI에 반영되지 않습니다.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 방사형 {#radial}

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>설명</strong></td>
   <td><strong>예외</strong></td>
  </tr>
  <tr>
   <td>컬러</td>
   <td>color 속성은 방사형 객체의 고유한 색상을 설명합니다</td>
   <td>
    <ul>
     <li>기본값을 검색할 수 없습니다. </li>
     <li>변경 사항은 모델에 반영되며 스크립팅에는 사용할 수 있지만 HTML 요소와 동기화되지 않습니다. 따라서 변경 사항이 UI에 반영되지 않습니다.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 점각 {#stipple}

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>설명</strong></td>
   <td><strong>예외</strong></td>
  </tr>
  <tr>
   <td>컬러</td>
   <td>color 속성은 stipple 객체의 고유한 색상을 설명합니다.</td>
   <td>
    <ul>
     <li>기본값을 검색할 수 없습니다. </li>
     <li>변경 사항은 모델에 반영되며 스크립팅에는 사용할 수 있지만 HTML 요소와 동기화되지 않습니다. 따라서 변경 사항이 UI에 반영되지 않습니다.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## draw {#draw}

<table>
 <tbody>
  <tr>
   <td>속성</td>
   <td>설명</td>
   <td>예외</td>
  </tr>
  <tr>
   <td>ui</td>
   <td>ui 개체에 양식 개체의 사용자 인터페이스 설명이 포함됩니다.<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>캡션</td>
   <td>캡션 개체는 양식 디자인 개체와 관련된 설명 레이블을 설명합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td>presence</td>
   <td>개체의 가시성을 지정합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td>이름</td>
   <td>스크립트 표현식에서 이 개체나 이벤트를 지정하는 데 사용할 수 있는 식별자를 지정합니다.</td>
   <td>런타임에 값을 설정할 수 없습니다.</td>
  </tr>
  <tr>
   <td>정렬 단추</td>
   <td>값 개체에 데이터 내용의 단일 단위가 포함됩니다.<br /> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

## corner {#corner}

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>설명</strong></td>
   <td><strong>예외</strong></td>
  </tr>
  <tr>
   <td>컬러</td>
   <td>color 속성은 모서리 객체의 고유한 색상을 설명합니다.</td>
   <td>
    <ul>
     <li>기본값을 검색할 수 없습니다. </li>
     <li>변경 사항은 모델에 반영되며 스크립팅에는 사용할 수 있지만 HTML 요소와 동기화되지 않습니다. 따라서 변경 사항이 UI에 반영되지 않습니다.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## checkButton {#checkbutton}

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>설명</strong></td>
   <td><strong>예외</strong></td>
  </tr>
  <tr>
   <td>국경</td>
   <td>border 객체는 checkButton 객체를 둘러싼 테두리에 대해 설명합니다. </td>
   <td>변경 사항은 모델에 반영되며 스크립팅에는 사용할 수 있지만 HTML 요소와 동기화되지 않습니다. 따라서 변경 내용이 UI에 반영되지 않습니다.<br /> </td>
  </tr>
 </tbody>
</table>

## choiceList {#choicelist}

<table>
 <tbody>
  <tr>
   <td><strong>속성<br /> </strong></td>
   <td><strong>설명</strong></td>
   <td><strong>예외</strong></td>
  </tr>
  <tr>
   <td>국경</td>
   <td>border 객체는 choiceList 오브젝트 주변의 테두리에 대해 설명합니다.</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## dateTimeEdit {#datetimeedit}

| **속성** | **설명** | **예외** |
|---|---|---|
| 국경 | border 객체는 날짜TimeEdit 객체의 테두리를 설명합니다. |  |

## 이미지 {#image}

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>설명</strong></td>
   <td><strong>예외</strong></td>
  </tr>
  <tr>
   <td>contentType</td>
   <td>참조된 문서의 내용 유형을 MIME 유형으로 지정합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>이름<br /> </td>
   <td>스크립트 표현식에서 이 요소를 식별하는 데 사용되는 식별자입니다.</td>
   <td>없음</td>
  </tr>
 </tbody>
</table>

## imageEdit {#imageedit}

| **속성** | **설명** | **예외** |
|---|---|---|
| 국경 | border 객체는 imageEdit 객체를 둘러싼 테두리에 대해 설명합니다. |  |

## numericEdit {#numericedit}

| **속성** | **설명** | **예외** |
|---|---|---|
| 국경 | border 객체는 객체를 둘러싸는 테두리에 대해 설명합니다. | 없음 |

## 개체 {#object}

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>설명</strong></td>
   <td><strong>예외</strong></td>
  </tr>
  <tr>
   <td>className</td>
   <td>이 개체의 클래스 이름을 결정합니다.<br /> </td>
   <td>없음</td>
  </tr>
 </tbody>
</table>

## 직사각형 {#rectangle}

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>설명</strong></td>
   <td><strong>예외</strong></td>
  </tr>
  <tr>
   <td>edge</td>
   <td>가장자리 개체는 테두리 또는 사각형의 호, 선 또는 한 면을 설명합니다.<br /> </td>
   <td>색상, 단면 등과 같은 속성은 지원되지 않습니다.</td>
  </tr>
 </tbody>
</table>

## textEdit {#textedit}

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>설명</strong></td>
   <td><strong>예외</strong></td>
  </tr>
  <tr>
   <td>국경</td>
   <td>border 개체는 개체를 둘러싼 테두리에 대해 설명합니다.<br /> </td>
   <td>없음</td>
  </tr>
 </tbody>
</table>

## excelGroup {#exclgroup}

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>설명</strong></td>
   <td><strong>예외</strong></td>
  </tr>
  <tr>
   <td>레이아웃</td>
   <td>이 개체에 사용할 레이아웃 전략을 지정합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>국경</td>
   <td>이 필드 주위의 테두리를 지정합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>mandatory</td>
   <td>필드의 nullTest 값을 지정합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>borderColor</td>
   <td>이 필드의 테두리 색상 값을 지정합니다.스크립팅을 통해 색상을 변경하려면 먼저 테두리를 정의해야 합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>borderWidth</td>
   <td>이 필드의 테두리 너비를 지정합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>h</td>
   <td>레이아웃의 높이 측정입니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>과도하</td>
   <td>처리 응용 프로그램에서 양식 제출 또는 저장 작업의 일부로 제외 그룹의 값을 저장할지 여부를 지정합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>쓰기</td>
   <td>레이아웃의 너비를 지정하는 측정입니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>x</td>
   <td>배치된 레이아웃으로 배치할 때 부모 컨테이너의 왼쪽 위 모서리를 기준으로 컨테이너 기준점의 x 좌표를 지정합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>y</td>
   <td>배치된 레이아웃으로 배치할 때 부모 컨테이너의 왼쪽 위 모서리를 기준으로 한 컨테이너 기준점의 y 좌표를 지정합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>캡션</td>
   <td>캡션 개체는 양식 디자인 개체와 관련된 설명 레이블을 설명합니다.<br /> </td>
   <td>없음</td>
  </tr>
  <tr>
   <td>유효성 검사</td>
   <td>유효성 검사 객체는 사용자가 제공한 양식의 데이터의 유효성 검사를 제어합니다. 양식 수명 동안 유효성 검사 객체를 여러 번 활성화할 수 있습니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>dataNode</td>
   <td>병합 후 양식 노드가 바인딩되는 데이터 노드를 가져옵니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>presence</td>
   <td>개체의 가시성을 지정합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td>access</td>
   <td>하위 폼과 같은 컨테이너 개체의 콘텐츠에 대한 사용자 액세스를 제어합니다.</td>
   <td>exclgrp의 개별 항목에 대해서는 항상 open을 반환합니다. </td>
  </tr>
  <tr>
   <td>이름</td>
   <td>스크립트 표현식에서 이 개체나 이벤트를 지정하는 데 사용할 수 있는 식별자를 지정합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>구성원</td>
   <td>제외 그룹의 구성원을 지정합니다. </td>
   <td>없음</td>
  </tr>
  <tr>
   <td>selectedMember</td>
   <td>제외 그룹의 선택된 구성원을 반환합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>execCalculate</td>
   <td>지정된 객체와 모든 하위 객체의 calculate 이벤트에 대한 스크립트를 실행합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>계산</td>
   <td>계산 개체는 필드 값 계산을 제어합니다.<br /> </td>
   <td>없음</td>
  </tr>
 </tbody>
</table>

## arc {#arc}

<table>
 <tbody>
  <tr>
   <td><strong>속성<strong></strong></strong></td>
   <td><strong>설명<strong></strong></strong></td>
   <td><strong>예외<strong></strong></strong></td>
  </tr>
  <tr>
   <td>edge</td>
   <td>가장자리 개체는 테두리 또는 사각형의 호, 선 또는 한 면을 설명합니다.<br /> </td>
   <td>색상, 단면 등과 같은 속성은 지원되지 않습니다. </td>
  </tr>
 </tbody>
</table>

## border {#border}

<table>
 <tbody>
  <tr>
   <td><strong>속성<strong></strong></strong></td>
   <td><strong>설명<strong></strong></strong></td>
   <td><strong>예외<strong></strong></strong></td>
  </tr>
  <tr>
   <td>edge</td>
   <td>가장자리 개체는 테두리 또는 사각형의 호, 선 또는 한 면을 설명합니다.<br /> </td>
   <td>색상, 단면 등과 같은 속성은 지원되지 않습니다. </td>
  </tr>
 </tbody>
</table>

## $레이아웃 {#layout}

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>설명</strong></td>
   <td><strong>예외</strong></td>
  </tr>
  <tr>
   <td>h</td>
   <td>지정된 양식 디자인 개체의 높이를 결정합니다.<br /> </td>
   <td>
    <ul>
     <li>높이(h) 속성은 페이지 영역 및 컨텐츠 영역에 대해 지원되지 않습니다. </li>
     <li>매개 변수 'XFA-Form 객체가 발생하는 첫 번째 컨텐츠 영역에서 오프셋'은 지원되지 않습니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>쓰기</td>
   <td>지정된 양식 디자인 개체의 너비를 결정합니다.</td>
   <td>
    <ul>
     <li>폭(w) 속성은 페이지 영역 및 컨텐츠 영역에 대해 지원되지 않습니다. </li>
     <li>매개 변수 'XFA-Form 객체가 발생하는 첫 번째 컨텐츠 영역에서 오프셋'은 지원되지 않습니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>x</td>
   <td>부모 개체를 기준으로 지정된 양식 디자인 개체의 x 좌표를 결정합니다.</td>
   <td>
    <ul>
     <li>x 좌표(x) 속성은 페이지 영역 및 컨텐츠 영역에 대해 지원되지 않습니다. </li>
     <li>매개 변수 'XFA-Form 객체가 발생하는 첫 번째 컨텐츠 영역에서 오프셋'은 지원되지 않습니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>y</td>
   <td>부모 개체를 기준으로 지정된 양식 디자인 개체의 y 좌표를 결정합니다.</td>
   <td>
    <ul>
     <li>y 좌표(y) 속성은 페이지 영역 및 컨텐츠 영역에 대해 지원되지 않습니다. </li>
     <li>매개 변수 'XFA-Form 객체가 발생하는 첫 번째 컨텐츠 영역에서 오프셋'은 지원되지 않습니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>pagecount</td>
   <td>현재 양식의 페이지 수를 결정합니다.</td>
   <td>
    <ul>
     <li>layout.pageCount() 메서드는 PDF 및 HTML 양식에 대해 다른 값을 반환합니다.</li>
     <li>개체를 숨겨 페이지 수를 줄이는 경우 abspageccount 메서드가 잘못된 값을 반환합니다.<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>pagecontent</td>
   <td>양식의 지정된 페이지에서 양식 디자인 개체의 유형을 검색합니다.</td>
   <td>없음</td>
  </tr>
  <tr>
   <td>absPageCount</td>
   <td>현재 양식의 페이지 수를 결정합니다.</td>
   <td>
    <ul>
     <li>layout.pageCount() 메서드는 PDF 및 HTML 양식에 대해 다른 값을 반환합니다.</li>
     <li>개체를 숨겨 페이지 수를 줄이는 경우 abspageccount 메서드는 잘못된 값을 반환합니다.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 항목 {#items}

| **속성** | **설명** | **예외** |
|---|---|---|
| presence | 개체의 가시성을 지정합니다. | 없음 |

## FormCalc {#formcalc}

FormCalc는 전자 양식 중심 논리 및 계산 루트를 만들기 위한 XFA 특정 언어입니다. FormCalculation은 강력한 빌드 함수 집합을 제공합니다.

### FormCalc 지원되는 함수 {#formcalc-supported-functions}

### FormCalc 표현식 지원 {#formcalc-expression-support}

<table>
 <tbody>
  <tr>
   <td><strong>카테고리 </strong></td>
   <td><strong>설명 </strong></td>
   <td><strong>샘플 </strong></td>
  </tr>
  <tr>
   <td>단순 표현식</td>
   <td>추가, 빼기, 곱하기, 나누기 및 괄호</td>
   <td>(a+b)*3</td>
  </tr>
  <tr>
   <td>변수 선언</td>
   <td>변수 정의</td>
   <td>var a<br /> var a=3<br /> a=3</td>
  </tr>
  <tr>
   <td>논리 표현식</td>
   <td>
    <ul>
     <li>논리(및/또는)</li>
     <li>비교(보다 크거나 같음/)</li>
    </ul> </td>
   <td>A 또는 1<br /> 1 &lt;&gt; 2<br /> A NE B<br /> A 또는 1<br /> 1 &lt;&gt; 2<br /> A NE B</td>
  </tr>
  <tr>
   <td>표현식</td>
   <td><br type="_moz" /> </td>
   <td>if (a&gt;b) then 2 endif</td>
  </tr>
  <tr>
   <td>while</td>
   <td><br type="_moz" /> </td>
   <td>while (i lt 5) do i = i + 1 endwhile</td>
  </tr>
  <tr>
   <td>대상</td>
   <td><br type="_moz" /> </td>
   <td>i = 100을 1로 다운로드하면 do s = s + i endfor<br /></td>
  </tr>
  <tr>
   <td>각</td>
   <td><br type="_moz" /> </td>
   <td>각 i in (1, 2, 3) <br /> do s = s + i endfor</td>
  </tr>
  <tr>
   <td>함수 선언</td>
   <td>FormCalc에서 사용자 지정 함수 정의</td>
   <td>func foo(n) do var f = n endfunc</td>
  </tr>
 </tbody>
</table>

### Acrobat API 지원 {#acrobat-api-support}

1. **산술 함수**

   1. Abs()
   1. Avg()
   1. Ceil()
   1. 횟수()
   1. Floor()
   1. 최대()
   1. 최소()
   1. Mod()
   1. Round()
   1. 합계()

1. **과학 기능**

   1. Acos()
   1. Asin()
   1. Atan()
   1. Atan2()
   1. Cos()
   1. Sin()
   1. Tan()
   1. Exp()
   1. 로그()
   1. Pow()
   1. Sqrt()
   1. Deg2Rad()
   1. Rad2Deg()
   1. Pi()

1. **재무 기능**

   1. 4월()
   1. Term()
   1. Fv()
   1. Ipmt()
   1. Npv()
   1. Pmt()
   1. ppmt()
   1. Pv()
   1. Rate()
   1. 용어()

1. **논리 함수**

   1. 선택()
   1. If()
   1. Oneof()
   1. Within()

1. **문자열 함수**

   1. At()
   1. Concat()
   1. 왼쪽()
   1. Len()
   1. Lower()
   1. Ltrim()
   1. 바꾸기()
   1. 오른쪽()
   1. Rtrim()
   1. 공백()
   1. Stuff()
   1. Substr()
   1. Upper()
   1. WordNum()

1. **날짜 및 시간**

   1. 날짜()
   1. num2date()
   1. DateFmt()

<table>
 <tbody>
  <tr>
   <td><strong>API</strong></td>
   <td><strong>설명</strong></td>
   <td><strong>수차</strong></td>
  </tr>
  <tr>
   <td>console.println()</td>
   <td>이 acrobat API는 출력을 JavaScript 콘솔에 덤프합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.alert()</td>
   <td>이 acrobat API는 JavaScript 팝업을 통해 경고 메시지를 전송합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.beep()</td>
   <td>시스템이 사운드를 재생하도록 합니다.</td>
   <td>작업이 수행되지 않습니다.</td>
  </tr>
  <tr>
   <td>app.execDialog()</td>
   <td>사용자에게 모달 대화 상자를 표시합니다. 호스트 애플리케이션을 다시 직접 사용하려면 먼저 모달 대화 상자를 닫아야 합니다.</td>
   <td>작업이 수행되지 않습니다.<br /> </td>
  </tr>
  <tr>
   <td>app.launchURL()</td>
   <td>브라우저 창에서 URL을 실행합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.setInterval()</td>
   <td>JavaScript 스크립트 및 기간을 지정합니다. 스크립트가 기간이 경과할 때마다 실행됩니다. 이 메서드의 반환 값은 JavaScript 변수에 포함해야 합니다. 그렇지 않으면 간격 객체가 가비지 수집을 따르므로 시간이 중지됩니다. 주기적 실행을 종료하려면 반환된 간격 객체를 clearInterval에 전달합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.setTimeOut()</td>
   <td>JavaScript 스크립트 및 기간을 지정합니다. 스크립트가 마침표가 경과 후 한 번만 실행됩니다.이 메서드의 반환 값은 JavaScript 변수에서 유지되어야 합니다. 그렇지 않으면 시간 초과 객체가 가비지 수집을 따르므로 시간이 중지됩니다. 시간 초과 이벤트를 취소하려면 반환된 시간 초과 객체를 clearTimeOut으로 전달합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.clearInterval()</td>
   <td>setInterval 메서드에서 처음에 설정한 이전에 등록된 간격을 취소합니다.</td>
   <td>HTML5 양식에서는 API가 올바르게 작동하지 않습니다.</td>
  </tr>
  <tr>
   <td>app.clearTimeOut()</td>
   <td>이전에 등록한 시간 초과 간격을 취소합니다. 이러한 간격은 처음에는 setTimeOut으로 설정됩니다.</td>
   <td>HTML5 양식에서 API가 올바르게 작동하지 않습니다.<br /> </td>
  </tr>
  <tr>
   <td>app.eval()</td>
   <td>지정된 스크립트를 실행합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.activeDocs</td>
   <td>각 활성 문서에 대한 Doc 객체를 포함하는 배열입니다. 활성 문서가 없으면 activeDocs는 아무 것도 반환하지 않습니다.즉, 코어 JavaScript의 d = new Array(0)와 동일한 비헤이비어를 갖습니다.</td>
   <td>HTMl5 양식에 대한 빈 배열을 반환합니다.</td>
  </tr>
  <tr>
   <td>app.calculate</td>
   <td>true(기본값)이면 계산을 수행할 수 있습니다. false이면 계산이 허용되지 않습니다.</td>
   <td>HTMl5 Forms의 경우 항상 true입니다.</td>
  </tr>
  <tr>
   <td>app.constants</td>
   <td>다양한 상수 값을 보유하기 위한 래퍼 객체입니다. 현재 이 속성은 단일 속성을 갖는 객체를 반환하고, align을 반환합니다.</td>
   <td>HTML5 양식은 빈 정렬 개체를 반환합니다.</td>
  </tr>
  <tr>
   <td>app.focusRect</td>
   <td>포커스 사각형을 켜거나 끕니다. 포커스 사각형은 단추, 확인란, 라디오 단추 및 서명 주위에 있는 희미한 점선으로 양식 필드에 키보드 포커스가 있음을 나타냅니다. true 값을 사용하면 포커스 사각형이 설정됩니다.</td>
   <td>HTML5 양식의 경우 항상 true입니다.</td>
  </tr>
  <tr>
   <td>app.formsVersion</td>
   <td>뷰어 양식 소프트웨어의 버전 번호입니다. 스크립트에서 이전 버전과의 호환성을 유지하려면 이 속성을 확인하여 새 버전의 소프트웨어에서 객체, 속성 또는 메서드를 사용할 수 있는지 확인합니다.</td>
   <td>항상 11.001입니다.</td>
  </tr>
  <tr>
   <td>app.language</td>
   <td>실행 중인 Acrobat 뷰어의 언어입니다.</td>
   <td>HTMl5 양식의 경우 항상 "ENU"를 선택합니다.</td>
  </tr>
 </tbody>
</table>

## 지원되는 XFA 이벤트 {#supported-xfa-events}

다음 클라이언트측 XFA 이벤트가 지원됩니다.

* 초기화
* 유효성 검사
* 연산
* 클릭
* Enter 키
* 종료
* 변경
* 유효성 검사 상태

>[!NOTE]
>
>HTML5 양식은 클라이언트측(브라우저)에서 렌더링됩니다. 서버측 스크립트 대신 클라이언트측 **validate** 및 **calculate** 스크립트를 사용하는 것이 좋습니다.
