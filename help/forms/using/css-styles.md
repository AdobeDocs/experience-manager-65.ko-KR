---
title: HTML5 양식용 CSS 스타일 만들기
description: HTML 양식 요소와 연결된 CSS 클래스를 수정하여 HTML5 양식의 모양을 변경하는 방법에 대해 알아봅니다.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: a8d986ab-2a4c-488b-957e-4606f7391bd3
feature: HTML5 Forms
exl-id: 8cc90ff7-284e-41cd-bfda-7fa09371e270
source-git-commit: 524475c8f9dbd02bae30ecd558a376505fbe0aed
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 2%

---

# HTML5 양식용 CSS 스타일 만들기 {#creating-css-styles-for-html-forms}

XFA 기반 양식 템플릿의 HTML5 렌디션은 여러 HTML 요소로 구성됩니다. 이러한 요소는 순서대로 배열됩니다. 모든 요소에는 잘 정의된 CSS 클래스가 있습니다. 이러한 CSS 클래스를 사용하여 요소의 모양을 선택하고 변경할 수 있습니다.

>[!NOTE]
>
>CSS 클래스에서 너비, 높이, 테두리 두께, 위쪽, 왼쪽, 오른쪽, 아래쪽, 패딩, 여백 및 기타 위치 및 크기 특성의 값을 변경하지 마십시오. 위치 및 크기 특성을 변경하면 양식의 레이아웃이 변경됩니다.

## 요소에 대한 CSS 클래스  {#css-classes-nbsp-for-elements-nbsp}

모든 요소에는 잘 정의된 CSS 클래스가 포함되어 있습니다. 이러한 클래스를 수정하여 요소의 모양을 변경할 수 있습니다. 필드 및 그리기 요소를 제외한 모든 요소에는 두 개의 CSS 클래스(Type 클래스와 Name 클래스)가 있습니다.

* 다음 **Type 클래스** 는 XFA 필드의 유형을 나타냅니다. 다음을 재정의할 수 있습니다. `type` 클래스를 사용하여 특정 형식의 모든 요소의 스타일을 수정할 수 있습니다.

* 다음 **이름 클래스** 는 XFA 필드의 이름에 해당합니다. 다음을 재정의할 수 있습니다. `name` 요소를 수정하고 요소에 사용자 지정 스타일을 적용할 클래스입니다.

>[!NOTE]
>
>일부 XFA 요소에는 이름이 없습니다. 이러한 구성 요소의 스타일을 변경하려면 해당 특정 유형의 모든 구성 요소를 수정합니다.

AEM Forms 디자이너에서 이름이 지정되지 않은 HTML의 경우, page5 폼의 페이지는 숫자가 증가하는 순서로 이름이 지정됩니다. 예를 들어 페이지가 두 개인 HTML 5 양식의 경우 페이지 이름은 Page1, Page2입니다.

## 필드 요소 {#field-element}

필드 요소에는 위젯과 캡션이라는 두 가지 중첩된 요소가 포함되어 있습니다.

**위젯 요소**

위젯 요소에는 사용자와의 상호 작용을 위한 사용자 인터페이스 요소가 포함됩니다. 여기에는 세 개의 CSS 클래스가 있습니다.

* **위젯**: 모든 위젯에는 이 클래스가 있습니다.
* **이름**: AEM과 함께 제공되는 모든 위젯에 위젯 이름 클래스가 포함되어 있습니다. 사용자 정의 위젯의 경우 위젯 개발자는 위젯 이름 클래스를 제공합니다.
* **유형**: 모든 위젯에는 사용자 인터페이스 요소가 있습니다. 이 클래스는 사용자 인터페이스 요소의 유형을 정의합니다.

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

필드 구성 요소에는 type 및 name 클래스 외에 라는 추가 CSS 클래스도 포함됩니다 **하위 유형**. 하위 유형은 NumericField, DateField, TextField와 같이 해당 필드의 유형을 식별합니다. subtype 클래스를 재정의하여 type, subtype의 모든 필드 스타일을 수정할 수 있습니다.

## 다른 구성 요소에 대한 CSS 클래스 {#css-classes-for-different-components}

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
   <td>사용자 정의 이름<br /> 또는<br /> 페이지&lt;pagenumber&gt; (기본값)</td>
  </tr>
  <tr>
   <td>컨텐츠 영역</td>
   <td>contentarea</td>
   <td>사용자 정의 이름</td>
  </tr>
  <tr>
   <td>하위 양식</td>
   <td>하위 양식</td>
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
   <td>캡션</td>
   <td>NA</td>
  </tr>
  <tr>
   <td>위젯</td>
   <td>위젯</td>
   <td>위젯 개발자가 정의합니다(사용자 정의 위젯의 경우 다음 섹션의 표를 참조)</td>
  </tr>
 </tbody>
</table>

## 다른 필드에 대한 CSS 클래스 {#css-classes-for-different-fields}

AEM Forms 디자이너는 NumericField, DecimalField 및 Date Field와 같은 양식에서 다양한 유형의 필드를 지원합니다. HTML의 이러한 모든 필드에는 위에서 언급한 CSS 클래스가 포함되어 있습니다. 또한 필드 유형에 따라 몇 가지 추가 클래스가 포함되어 있습니다.

모든 필드에는 UI 요소를 나타내는 연관된 위젯이 있습니다. 각 필드의 클래스 및 각 필드와 연결된 위젯이 아래에 나열됩니다.

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
   <td>buttonfield위젯<br type="_moz" /> </td>
   <td>입력 유형=단추<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>CheckButton<br type="_moz" /> </td>
   <td>checkboxfield<br /> </td>
   <td>XfaCheckBox<br type="_moz" /> </td>
   <td>checkboxfield위젯<br type="_moz" /> </td>
   <td>입력 유형=checkbox<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DateField<br type="_moz" /> </td>
   <td>일자 필드<br type="_moz" /> </td>
   <td>dateField<br type="_moz" /> </td>
   <td>datefield 위젯<br type="_moz" /> </td>
   <td>입력 유형=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>날짜/시간 필드<br type="_moz" /> </td>
   <td>텍스트 필드<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>텍스트 필드 위젯</td>
   <td>입력 유형=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DecimalField<br type="_moz" /> </td>
   <td>numericfield<br type="_moz" /> </td>
   <td>numericInput<br type="_moz" /> </td>
   <td>numericfield위젯<br type="_moz" /> </td>
   <td>입력 유형=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>드롭다운<br type="_moz" /> </td>
   <td>수상자<br type="_moz" /> </td>
   <td>dropDownListWidget<br type="_moz" /> </td>
   <td>choicelistwidget<br type="_moz" /> </td>
   <td>선택</td>
  </tr>
  <tr>
   <td>ListBox<br type="_moz" /> </td>
   <td>수상자<br type="_moz" /> </td>
   <td>목록 상자 위젯<br type="_moz" /> </td>
   <td>choicelistwidget<br type="_moz" /> </td>
   <td>ol</td>
  </tr>
  <tr>
   <td>NumericField<br type="_moz" /> </td>
   <td>numericfield<br type="_moz" /> </td>
   <td>numericInput<br type="_moz" /> </td>
   <td>numericfield위젯<br type="_moz" /> </td>
   <td>입력 유형=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>암호 필드<br type="_moz" /> </td>
   <td>passwordfield<br type="_moz" /> </td>
   <td>기본 위젯<br type="_moz" /> </td>
   <td>암호 필드 위젯<br type="_moz" /> </td>
   <td>입력 유형=암호<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>라디오 단추<br type="_moz" /> </td>
   <td>방사선원<br type="_moz" /> </td>
   <td>XfaCheckBox<br type="_moz" /> </td>
   <td>방사형 필드 위젯<br type="_moz" /> </td>
   <td>입력 유형=라디오<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>텍스트 필드<br type="_moz" /> </td>
   <td>텍스트 필드<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>텍스트 필드 위젯<br type="_moz" /> </td>
   <td>입력 유형=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>TimeField<br type="_moz" /> </td>
   <td>텍스트 필드<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>텍스트 필드 위젯<br type="_moz" /> </td>
   <td>입력 유형=text<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

## 다른 그리기 요소에 대한 CSS 클래스 {#css-classes-for-different-draw-elements}

AEM Forms Designer를 사용하여 텍스트 및 이미지와 같은 정적 그리기 요소를 삽입할 수 있습니다. 각 그리기 요소에 대해 별도의 CSS 클래스가 해당 요소와 연결됩니다. 그리기 요소의 CSS 클래스 목록은 아래에 나와 있습니다. 모든 그리기 요소에는 그리기 클래스가 연결되어 있습니다.

| **그리기 유형** | **CSS 클래스** |
|---|---|
| 텍스트 | text |
| 이미지 | 이미지 |
| 사각형 | 사각형 |
| Line | line |

## 양식의 다른 부분 스타일링 {#styling-other-parts-of-the-form}

HTML 양식에 UI 구성 요소가 표시되는 것 외에도 인라인 오류, 인라인 경고 및 유효성 검사 오류가 있는 필드와 같은 요소의 스타일을 변경할 수 있습니다.

`Styling Inline Errors`

필드의 유효성 검사에서 오류가 발생하면 필드가 활성 상태일 때 인라인 오류가 표시됩니다. 인라인 오류의 스타일을 변경하려면 CSS ID를 무시하십시오 **error-msg**.

`Styling Inline Warnings`

필드의 유효성 검사로 인해 경고가 발생하면 필드가 활성 상태일 때 인라인 경고가 표시됩니다. 이러한 인라인 경고의 스타일을 변경하려면 CSS ID를 무시하십시오 **warning-msg**.

`Styling Fields with Validation Errors`

필드 유효성 검사가 실패하면 위젯 스타일이 변경됩니다. 이 스타일 변경은 CSS 클래스를 적용하여 수행됩니다. **widgetError** 위젯 구성 요소 기본 스타일을 수정하려면 **widgetError** 클래스.
