---
title: HTML5 양식의 CSS 스타일 만들기
seo-title: HTML5 양식의 CSS 스타일 만들기
description: HTML 양식 요소와 연결된 CSS 클래스를 수정하여 HTML5 양식의 모양을 변경하는 방법을 알아봅니다.
seo-description: HTML 양식 요소와 연결된 CSS 클래스를 수정하여 HTML5 양식의 모양을 변경하는 방법을 알아봅니다.
uuid: 43c689b4-243c-43de-a8be-1eef10d75295
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: a8d986ab-2a4c-488b-957e-4606f7391bd3
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 3%

---


# HTML5 양식에 대한 CSS 스타일 만들기 {#creating-css-styles-for-html-forms}

XFA 기반 양식 템플릿의 HTML5 변환은 여러 HTML 요소로 구성됩니다. 이러한 요소는 순서대로 배열됩니다. 모든 요소에는 잘 정의된 CSS 클래스가 있습니다. 이러한 CSS 클래스를 사용하여 요소의 모양을 선택하고 변경할 수 있습니다.

>[!NOTE]
>
>CSS 클래스에서 폭, 높이, 테두리 두께, 위쪽, 왼쪽, 오른쪽, 아래쪽, 패딩, 여백, 기타 위치 및 크기 특성 값을 변경하지 마십시오. 위치 및 크기 특성이 변경되면 양식의 레이아웃이 변경됩니다.

## CSS 클래스  요소  {#css-classes-nbsp-for-elements-nbsp}

모든 요소에는 잘 정의된 CSS 클래스가 포함되어 있습니다. 이러한 클래스를 수정하여 요소의 모양을 변경할 수 있습니다. 필드 및 그리기 요소를 제외한 모든 요소에는 Type 클래스와 Name 클래스 등 2개의 CSS 클래스가 있습니다.

* **Type 클래스**&#x200B;는 XFA 필드의 유형을 나타냅니다. `type` 클래스를 재정의하여 특정 유형의 모든 요소의 스타일을 수정할 수 있습니다.

* **Name 클래스**&#x200B;는 XFA 필드의 이름에 해당합니다. `name` 클래스를 재정의하여 요소를 수정하고 사용자 지정 스타일을 적용할 수 있습니다.

>[!NOTE]
>
>일부 XFA 요소에는 이름이 없습니다. 이러한 구성 요소의 스타일을 변경하려면 해당 특정 유형의 모든 구성 요소를 수정합니다.

AEM Forms Designer에서 이름이 지정되지 않은 페이지의 경우 HTML5 양식의 페이지 이름은 페이지 수의 증가순으로 지정됩니다. 예를 들어, 두 페이지가 있는 HTML5 양식의 경우 페이지 이름은 Page1, Page2입니다.

## 필드 요소 {#field-element}

필드 요소에는 두 개의 중첩된 요소가 있습니다.위젯 및 캡션

**위젯 요소**

위젯 요소에는 사용자와 상호 작용하기 위한 사용자 인터페이스 요소가 포함되어 있습니다. 3개의 CSS 클래스가 있습니다.

* **위젯**:모든 위젯에는 이 클래스가 있습니다.
* **이름**:AEM과 함께 제공되는 모든 위젯에는 위젯 이름 클래스가 포함되어 있습니다. 사용자 정의 위젯의 경우 위젯 개발자는 위젯 이름 클래스를 제공합니다.
* **유형**:모든 위젯에는 사용자 인터페이스 요소가 있습니다. 이 클래스는 사용자 인터페이스 요소의 유형을 정의합니다.

```xml
<!--field with caption-->
<div class="field numericfield NumericField3 ">
     <div class="caption">
        caption content
     </div>
     <div class="widget numericfieldwidget numericInput">
       widget content
     </div>
</div>

<!--field without caption-->
<div class="widget numericfieldwidget numericInput">
   widget content
</div>
```

유형 및 이름 클래스 외에도 필드 구성 요소에는 **subtype**&#x200B;이라는 추가 CSS 클래스가 포함되어 있습니다. 하위 유형은 필드의 유형(예: NumericField, DateField, TextField)을 식별합니다. 하위 유형 클래스를 재정의하여 유형, 하위 유형의 모든 필드의 스타일을 수정할 수 있습니다.

## 다른 구성 요소 {#css-classes-for-different-components}에 대한 CSS 클래스

<table>
 <tbody>
  <tr>
   <td><strong>구성 요소</strong></td>
   <td><strong>유형</strong></td>
   <td><strong>이름</strong></td>
  </tr>
  <tr>
   <td>페이지</td>
   <td>페이지</td>
   <td>사용자 정의 이름<br /> 또는<br /> 페이지&lt;pageNumber&gt;(기본값)</td>
  </tr>
  <tr>
   <td>컨텐츠 영역</td>
   <td>컨텐트 영역</td>
   <td>사용자 정의 이름</td>
  </tr>
  <tr>
   <td>하위 폼</td>
   <td>하위</td>
   <td>사용자 정의 이름</td>
  </tr>
  <tr>
   <td>제외 그룹</td>
   <td>exclgroup</td>
   <td>사용자 정의 이름</td>
  </tr>
  <tr>
   <td>Draw</td>
   <td>draw</td>
   <td>사용자 정의 이름</td>
  </tr>
  <tr>
   <td>필드</td>
   <td>필드</td>
   <td>사용자 정의 이름</td>
  </tr>
  <tr>
   <td>캡션</td>
   <td>caption</td>
   <td>NA</td>
  </tr>
  <tr>
   <td>위젯</td>
   <td>widget</td>
   <td>위젯 개발자가 정의합니다(사용자 정의 위젯의 경우 다음 섹션의 표 참조).</td>
  </tr>
 </tbody>
</table>

## 다른 필드 {#css-classes-for-different-fields}에 대한 CSS 클래스

AEM Forms Designer는 NumericField, DecimalField 및 Date Field와 같은 형식으로 서로 다른 유형의 필드를 지원합니다. HTML의 이러한 모든 필드에는 위에 언급된 CSS 클래스가 포함되어 있습니다. 또한 필드 유형에 따라 일부 추가 클래스가 들어 있습니다.

모든 필드에는 UI 요소를 나타내는 연관된 위젯이 있습니다. 각 필드의 클래스 및 각 필드와 관련된 위젯이 아래에 나열되어 있습니다.

<table>
 <tbody>
  <tr>
   <td><strong>필드 유형</strong></td>
   <td><strong>하위 유형</strong></td>
   <td><strong>위젯 이름</strong></td>
   <td><strong>위젯 유형</strong></td>
   <td><strong>HTML UI 태그</strong></td>
  </tr>
  <tr>
   <td>단추<br type="_moz" /> </td>
   <td>NA</td>
   <td>xfaButton<br type="_moz" /> </td>
   <td>buttonfieldwidget<br type="_moz" /> </td>
   <td>input type=button<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>CheckButton<br type="_moz" /> </td>
   <td>checkboxfield<br /> </td>
   <td>XfaCheckBox<br type="_moz" /> </td>
   <td>checkboxfieldwidget<br type="_moz" /> </td>
   <td>입력 유형=checkbox<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DateField<br type="_moz" /> </td>
   <td>datefield<br type="_moz" /> </td>
   <td>dateField<br type="_moz" /> </td>
   <td>datefieldwidget<br type="_moz" /> </td>
   <td>입력 유형=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DateTimeField<br type="_moz" /> </td>
   <td>texfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget</td>
   <td>입력 유형=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DecimalField<br type="_moz" /> </td>
   <td>numicfield<br type="_moz" /> </td>
   <td>numericInput<br type="_moz" /> </td>
   <td>numericfieldwidget<br type="_moz" /> </td>
   <td>입력 유형=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DropDown<br type="_moz" /> </td>
   <td>choicelist<br type="_moz" /> </td>
   <td>dropDownListWidget<br type="_moz" /> </td>
   <td>choicelistwidget<br type="_moz" /> </td>
   <td>select</td>
  </tr>
  <tr>
   <td>ListBox<br type="_moz" /> </td>
   <td>choicelist<br type="_moz" /> </td>
   <td>listBoxWidget<br type="_moz" /> </td>
   <td>choicelistwidget<br type="_moz" /> </td>
   <td>ol</td>
  </tr>
  <tr>
   <td>NumericField<br type="_moz" /> </td>
   <td>numicfield<br type="_moz" /> </td>
   <td>numericInput<br type="_moz" /> </td>
   <td>numericfieldwidget<br type="_moz" /> </td>
   <td>입력 유형=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>PasswordField<br type="_moz" /> </td>
   <td>passwordfield<br type="_moz" /> </td>
   <td>defaultWidget<br type="_moz" /> </td>
   <td>passwordfieldwidget&lt;a0/<br type="_moz" /> </td>
   <td>입력 유형=password<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>라디오 단추<br type="_moz" /> </td>
   <td>라디오 필드<br type="_moz" /> </td>
   <td>XfaCheckBox<br type="_moz" /> </td>
   <td>radifieldwidget<br type="_moz" /> </td>
   <td>input type=radio<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>TextField<br type="_moz" /> </td>
   <td>texfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget<br type="_moz" /> </td>
   <td>입력 유형=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>TimeField<br type="_moz" /> </td>
   <td>texfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget<br type="_moz" /> </td>
   <td>입력 유형=text<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

## 다른 그리기 요소에 대한 CSS 클래스 {#css-classes-for-different-draw-elements}

AEM Forms Designer를 사용하여 텍스트 및 이미지와 같은 정적 그리기 요소를 삽입할 수 있습니다. 각 그리기 요소에 대해 별도의 CSS 클래스가 해당 요소와 연결됩니다. 그리기 요소에 대한 CSS 클래스 목록은 아래에 나열되어 있습니다. 모든 그리기 요소에는 해당 그리기 클래스와 연결된 그리기 클래스가 있습니다.

| **드로잉 유형** | **CSS 클래스** |
|---|---|
| 텍스트 | text |
| 이미지 | 이미지 |
| 사각형 | 사각형 |
| Line | line |

## {#styling-other-parts-of-the-form} 양식의 다른 부분 스타일 지정

HTML 양식에 있는 UI 구성 요소의 모양 외에도 인라인 오류, 인라인 경고 및 유효성 검사 오류가 있는 필드와 같은 요소 스타일을 변경할 수 있습니다.

`Styling Inline Errors`

필드의 유효성 검사 결과 오류가 발생하면 필드가 활성 상태일 때 인라인 오류가 표시됩니다. 인라인 오류 스타일을 변경하려면 CSS ID **error-msg**&#x200B;을 재정의합니다.

`Styling Inline Warnings`

필드의 유효성 검사 결과 경고가 발생하면 필드가 활성 상태일 때 인라인 경고가 표시됩니다. 이러한 인라인 경고의 스타일을 변경하려면 CSS ID **warning-msg**&#x200B;를 무시합니다.

`Styling Fields with Validation Errors`

필드에 대한 유효성 검사가 실패하면 위젯 스타일이 변경됩니다. 이 스타일 변경은 위젯 구성 요소에 CSS 클래스 **widgetError**&#x200B;을 적용하여 수행됩니다. 기본 스타일을 수정하려면 **widgetError** 클래스를 재정의합니다.
