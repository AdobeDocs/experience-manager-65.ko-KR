---
title: 적응형 양식에 대한 스타일 구성
description: 적응형 양식의 모양을 사용자 지정하려면 LESS 프레임워크를 사용하십시오.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms,Foundation Components
exl-id: 691608a6-be82-4d81-b876-427de997e5be
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2352'
ht-degree: 5%

---

# 적응형 양식에 대한 스타일 구성{#styling-constructs-for-adaptive-forms}

<span class="preview"> [새 적응형 양식 만들기](/help/forms/using/create-an-adaptive-form-core-components.md) 또는 [AEM Sites 페이지에 적응형 양식 추가](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) 작업을 할 때 현대적이고 확장 가능한 데이터 캡처 [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)를 사용하는 것이 좋습니다. 이러한 구성 요소는 적응형 양식 만들기 작업이 대폭 개선되어 우수한 사용자 경험을 보장할 수 있게 되었음을 나타냅니다. 이 문서에서는 기초 구성 요소를 사용하여 적응형 양식을 작성하는 이전 접근법에 대해 설명합니다. </span>

## 사전 요구 사항 {#prerequisites}

CSS 및 LESS 프레임워크에 대한 지식.

## 사용자 정의 가능한 사항 {#what-can-be-customized}

이 문서에는 적응형 양식의 공개적으로 사용 가능한 css 클래스가 나열되어 있습니다. 이러한 클래스를 사용하여 적응형 양식의 다양한 구성 요소에 스타일을 지정할 수 있습니다. 경고를 표시하는 대화 상자 및 상태 표시줄과 같은 작성 구성 요소의 스타일은 이 문서의 범위를 벗어납니다. 다음 스타일 구문을 사용하여 구성 요소의 스타일을 지정할 수 없는 경우에만 스타일을 만듭니다(CSS 또는 그 이하 사용). [테마 편집기](https://helpx.adobe.com/experience-manager/6-3/forms/using/themes.html).

## 적응형 양식에서 스타일 맞춤화 {#customizing-styles-in-adaptive-forms}

LESS 프레임워크를 통해 사용 사례를 간소화하여 적응형 양식에서 스타일을 사용자 지정할 수 있습니다. 프레임워크를 사용하면 변수 및 함수 집합(mixin)을 사용하여 스타일을 정의할 수 있습니다. LESS 프레임워크는 번들형 코드의 크기를 줄이고 재사용성을 높이는 데 도움이 됩니다.

다음 방법으로 적응형 양식 스타일을 사용자 지정할 수 있습니다.

* 테마 변경
* 구성 요소의 스타일 변경

## 테마 변경 {#changing-theme}

적응형 양식의 모양을 적응형 양식이 포함된 웹 페이지와 일치하도록 적응형 양식의 테마를 변경할 수 있습니다.

CSS 속성을 사용한 적응형 양식의 전체 모양 변경은 일반적으로 테마 변경의 일부입니다. 적응형 양식의 &quot;확인 및 느낌&quot;에 대한 주요 변경 사항(예: 레이아웃 및 구성 요소 배치 변경 사항)은 테마 변경으로 간주되지 않습니다.

부트스트랩을 기반으로 다음 CSS 속성 세트는 웹 페이지의 테마를 정의합니다.

* 배경색
* 테두리(유형, 색상, 두께)
* 글꼴 색상
* 사진 간격
* 여백
* 글꼴 크기
* 선 높이

현재 LESS 변수는 적응형 양식에 있는 다양한 요소의 이러한 속성에 대해서만 정의됩니다.

## 구성 요소 스타일 변경 {#changing-component-style}

요소의 모양, 레이아웃, 위치 및 가시성을 변경할 수 있습니다. 이 작업을 수행하려면 이 문서에 나열된 스타일 구문을 포함하도록 사용자 지정 .css 파일을 만들거나 업데이트합니다.

적응형 양식에 스타일을 적용하려면 편집할 적응형 양식을 열고 적응형 양식 컨테이너의 속성을 열고 기본 탭에서 사용자 지정 CSS 파일의 경로를 지정합니다. 적응형 양식의 기본 스타일 구문이며 사용자 지정 .css 파일에 나열된 구문으로 재정의됩니다.

## 구성 요소 {#components}

이 문서에서 설명하는 구성 요소에는 사전 정의된 CSS 클래스가 있습니다. 변수를 편집하여 CSS 클래스의 스타일을 수정할 수 있습니다. 또는 전체 클래스를 다시 작성할 수 있습니다. 이 단원에서는 변수를 사용하여 수정할 수 있는 구성 요소 및 스타일 내의 클래스에 대해 설명합니다.

## 컨테이너 스타일 지정 {#container-styling}

컨테이너는 최상위 구성 요소입니다. 다른 패널과 필드는 컨테이너 구성 요소 아래에 있습니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 클래스 </strong></p> </td>
   <td><p><code>guideContainerNode</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>변수 설명</strong></p> </td>
   <td><p><strong>변수 설명</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>container-bgColor</code></p> </td>
   <td><p>컨테이너의 배경색</p> </td>
  </tr>
  <tr>
   <td><p><code>container-padding</code></p> </td>
   <td><p>컨테이너의 패딩</p> </td>
  </tr>
  <tr>
   <td><p><code>container-margin</code></p> </td>
   <td><p>컨테이너의 여백</p> </td>
  </tr>
  <tr>
   <td><p><code>container-fontColor</code></p> </td>
   <td><p>컨테이너의 글꼴 색상</p> </td>
  </tr>
 </tbody>
</table>

## 필드 스타일 지정 {#field-styling}

적응형 양식에는 다양한 유형의 필드가 포함됩니다. 각 필드에는 필드 이름인 고유한 클래스 이름이 있습니다. 필드에는 일반적인 클래스 이름도 있습니다 `guideFieldNode`.

필드에는 레이블, 위젯, 도움말 설명(긴 설명 및 짧은 설명 모두) 및 필드 도움말 아이콘(물음표)이 포함됩니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 클래스 </strong></p> </td>
   <td><p><code>guideFieldNode</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>변수 </strong></p> </td>
   <td><p><strong>설명</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>field-padding</code><strong></strong></p> </td>
   <td><p>필드 패딩</p> </td>
  </tr>
  <tr>
   <td><p><code>field-error-font-color</code></p> </td>
   <td><p>필드 오류 메시지의 글꼴 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>field-error-font-size</code></p> </td>
   <td><p>필드 오류 메시지의 글꼴 크기</p> </td>
  </tr>
 </tbody>
</table>

## 레이블 스타일 지정 {#label-styling}

HTML 요소 **레이블** 필드에는 클래스가 포함됩니다. **left** 또는 **top** 레이블이 맨 위에 있는지 아니면 왼쪽에 있는지에 따라 다릅니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 클래스 </strong></p> </td>
   <td><p><code>guideFieldLabel</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>변수 </strong></p> </td>
   <td><p><strong>설명</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>label-font-color</code></p> </td>
   <td><p>필드 레이블의 글꼴 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>label-font-size</code></p> </td>
   <td><p>필드 레이블의 글꼴 크기</p> </td>
  </tr>
  <tr>
   <td><p><code>label-line-height</code></p> </td>
   <td>필드 레이블의 CSS 라인 높이 속성 </td>
  </tr>
  <tr>
   <td><p><code>label-font-weight</code></p> </td>
   <td>필드 레이블의 CSS 글꼴 두께 속성 </td>
  </tr>
  <tr>
   <td><p><code>label-margin</code></p> </td>
   <td><p>필드 레이블의 여백</p> </td>
  </tr>
 </tbody>
</table>

레이블의 CSS 규칙은 **guideFieldLabel** 레이블. 작성자인 경우 이 규칙을 재정의하여 사용자 지정 변경 사항을 표시합니다.

## 위젯 스타일 {#widgets-styling}

유형에 따라 위젯에도 클래스가 포함됩니다. 일반적으로 위젯에는 `guideFieldWidget` 클래스. HTML과 함께 제공되는 위젯은 일반적으로 표준 HTML 요소 입력을 사용하고 선택합니다. 그에 따라 스타일링이 수행됩니다. 변수를 변경하여 사용자 정의 위젯의 스타일을 지정할 수 없습니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 클래스 </strong></p> </td>
   <td><p><code>guideFieldWidget</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>변수 <code></code></strong></p> </td>
   <td><p><strong>설명</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-bg-color</code></p> </td>
   <td>위젯의 배경색(확인란 및 라디오 버튼에 대해 작동하지 않음)</td>
  </tr>
  <tr>
   <td><p><code>widgets-border-color</code></p> </td>
   <td><p>위젯의 테두리 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-thickness</code></p> </td>
   <td><p>위젯의 테두리 크기</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-radius</code></p> </td>
   <td><p>위젯의 테두리 반경</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-type</code></p> </td>
   <td><p>위젯에 대한 테두리 유형</p> </td>
  </tr>
  <tr>
   <td><p><code>widget-border-focus-type</code></p> </td>
   <td><p>위젯 테두리에 대한 포커스 유형</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border</code></p> </td>
   <td><p>위젯의 통합 테두리 스타일</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-font-color</code></p> </td>
   <td><p>위젯 내부의 텍스트 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-font-size</code></p> </td>
   <td><p>위젯 내부의 텍스트 크기</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-line-height</code></p> </td>
   <td>위젯에 대한 CSS lineheight 속성 </td>
  </tr>
  <tr>
   <td><p><code>widgets-padding</code></p> </td>
   <td><p>위젯에 대한 CSS 패딩 속성</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-focus-border-color</code></p> </td>
   <td><p>위젯에 포커스가 있을 때의 테두리 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-mandatory-border-color</code></p> </td>
   <td><p>필수 필드에 대한 위젯의 테두리 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-mandatory-bg-color</code></p> </td>
   <td><p>필수 필드에 대한 위젯의 배경색</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-bg-color</code></p> </td>
   <td><p>필드가 비활성화될 때 위젯의 배경색</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-font-color</code></p> </td>
   <td><p>필드가 비활성화될 때 위젯의 글꼴 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-border-color</code></p> </td>
   <td><p>필드가 비활성화될 때 위젯의 테두리 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>widget-height</code></p> </td>
   <td>위젯 높이(확인란 및 라디오 버튼에 대해 작동하지 않음)</td>
  </tr>
  <tr>
   <td><p><code>checkbutton-height</code></p> </td>
   <td><p>확인란 및 라디오 버튼의 높이입니다.</p> </td>
  </tr>
  <tr>
   <td><p><code>listboxwidget-height</code></p> </td>
   <td><p>다중 선택 드롭다운의 최대 높이</p> </td>
  </tr>
 </tbody>
</table>

### 위젯 스타일의 제한 사항 {#limitations-in-widget-styling}

집중, 필수 및 비활성화 필드의 스타일이 변수를 사용하여 제한됩니다. 그러나 스타일을 재정의하여 변경할 수 있습니다. 변수를 사용하는 제한은 주로 변수의 수를 확인하기 위해 제공됩니다. 필드의 외형이 크게 바뀌는 경우, 그 제한은 앞서 논의한 주 중 어느 곳에서든 있기 때문에 완화될 수 있다.

## 도움말 설명 {#help-description}

작성자는 짧은 설명 및 긴 설명 구성 요소를 사용하여 필드에 도움말 콘텐츠를 지정할 수 있습니다. 두 구성 요소에는 공통 클래스가 있습니다 `.guideHelpDescription` 외 클래스 `.long`/ `.short`설명 유형에 따라 다릅니다. 도움말 콘텐츠는 단락 요소에 포함되어 설명의 스타일을 재정의합니다. 도움말 설명(긴 설명 및 짧은 설명 모두)은 다음 표에 설명된 대로 widgetshelp로 시작하는 변수를 사용하여 수정됩니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>변수 </strong></p> </td>
   <td><p><strong>설명</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-bg-color</code></p> </td>
   <td><p>위젯의 긴 도움말의 배경색</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-border-color</code></p> </td>
   <td><p>위젯의 긴 도움말의 테두리 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-border-indicator-color</code></p> </td>
   <td><p>위젯의 긴 도움말의 왼쪽 표시기 테두리 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-bg-color</code></p> </td>
   <td><p>위젯의 짧은 도움말의 배경색</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-color</code></p> </td>
   <td><p>위젯의 짧은 도움말의 글꼴 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-tooltip-bg-color</code></p> </td>
   <td><p>위젯의 짧은 도구 설명의 배경색입니다. 도움말</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-tooltip-color</code></p> </td>
   <td><p>위젯의 짧은 도구 설명의 글꼴 색상 도움말</p> </td>
  </tr>
 </tbody>
</table>

## 약관 {#terms-and-conditions}

약관(TnC) `` ``) 위젯을 사용하여 약관을 지정할 수 있습니다. 다음 표에 설명된 변수를 사용하여 위젯을 사용자 정의할 수 있습니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>변수 </strong></p> </td>
   <td><p><strong>설명</strong></p> </td>
  </tr>
  <tr>
   <td><code>tnc-unvisited</code></td>
   <td>방문하지 않은 tnc 링크의 글꼴 색입니다.</td>
  </tr>
  <tr>
   <td><code>tnc-visited</code></td>
   <td>방문한 tnc 링크의 글꼴 색입니다.</td>
  </tr>
 </tbody>
</table>

## 버튼 {#button}

버튼은 위젯이기도 합니다. 하지만 그들의 스타일은 위젯과 약간 다릅니다. 적응형 양식에서는 다음 중 하나가 버튼을 구성합니다.

* 입력[type = text]
* 단추
* 클래스 .button이 있는 요소

단추에 대한 HTML 코드:

`<button type="button" >`

`<span class="iconButtonicon"></`

`span>`

`<span class="iconButtonlabel"></`

`span>`

`</button>`

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 클래스</strong></p> </td>
   <td><p><strong>설명</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>iconButton-icon</code></p> </td>
   <td><p>버튼의 아이콘을 제공합니다.</p> </td>
  </tr>
  <tr>
   <td><p><code>iconButton-label</code></p> </td>
   <td><p>스타일 단추 레이블/캡션</p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>변수 <code></code></strong></p> </td>
   <td><p><strong>설명</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>button-border-size</code></p> </td>
   <td><p>단추의 테두리 크기</p> </td>
  </tr>
  <tr>
   <td><p><code>button-border-type</code></p> </td>
   <td><p>테두리 유형</p> </td>
  </tr>
  <tr>
   <td><p><code>button-padding</code></p> </td>
   <td><p>단추의 CSS 패딩 속성</p> </td>
  </tr>
  <tr>
   <td><p><code>button-font-size</code></p> </td>
   <td><p>단추의 글꼴 크기</p> </td>
  </tr>
  <tr>
   <td><p><code>button-background-color</code></p> </td>
   <td><p>단추의 배경색</p> </td>
  </tr>
  <tr>
   <td><p><code>button-font-color</code></p> </td>
   <td><p>단추의 글꼴 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>button-border-color</code></p> </td>
   <td><p>단추의 테두리 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>button-large-padding</code></p> </td>
   <td><p>큰 단추 패딩(클래스 .buttonlarge가 있는 단추)</p> </td>
  </tr>
  <tr>
   <td><p><code>button-large-font-size</code></p> </td>
   <td><p>큰 단추의 글꼴 크기</p> </td>
  </tr>
  <tr>
   <td><p><code>button-small-padding</code></p> </td>
   <td><p>작은 단추 패딩(클래스 .buttonsmall이 있는 단추)</p> </td>
  </tr>
  <tr>
   <td><p><code>button-small-font-size</code></p> </td>
   <td><p>작은 단추의 글꼴 크기</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-background-color</code></p> </td>
   <td><p>정보 제공 단추의 배경색(클래스 .buttoninformative가 있는 단추)</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-font-color</code></p> </td>
   <td><p>정보 제공 단추의 글꼴 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-border-color</code></p> </td>
   <td><p>정보 제공 단추의 테두리 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-background-color</code></p> </td>
   <td><p>경고 스타일이 지정된 단추의 배경색입니다(.buttonwarning 클래스가 있는 단추).</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-font-color</code></p> </td>
   <td><p>경고 스타일이 지정된 단추의 글꼴 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-border-color</code></p> </td>
   <td><p>경고 스타일이 지정된 단추의 테두리 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>button-alert-background-color</code></p> </td>
   <td><p>경고 단추의 배경색(클래스 .buttonalert가 있는 단추)</p> </td>
  </tr>
  <tr>
   <td><p><code>button-alert-font-color</code></p> </td>
   <td><p>경고 단추의 글꼴 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>button-alert-border-color</code></p> </td>
   <td><p>경고 단추의 테두리 색상</p> </td>
  </tr>
 </tbody>
</table>

## 물음표 {#question-mark}

위젯의 경우 작성자가 도움말 콘텐츠에 긴 설명을 추가하면 물음표가 표시됩니다. 부트스트랩에 제공된 기본 아이콘이 사용됩니다. 사용자 지정 아이콘을 사용하려면 부트스트랩 아이콘을 사용자 지정할 수 있습니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 클래스 </strong></p> </td>
   <td><p><code>guideHelpQuestionMark</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>변수 </strong></p> </td>
   <td><p><strong>설명</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>questionmark-font-color</code></p> </td>
   <td><p>아이콘 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>questionmark-hover-font-color</code></p> </td>
   <td><p>마우스를 아이콘 위로 가져간 경우의 아이콘 색상</p> </td>
  </tr>
 </tbody>
</table>

## 표 {#table}

다음 변수를 사용하여 테이블의 머리글 및 본문 행에 대한 색상 테마를 변경할 수 있습니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>변수 </strong></p> </td>
   <td><p><strong>설명</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>table-header-bg-color</code></p> </td>
   <td><p>머리글 행의 배경색입니다. 기본값은 입니다. <code>#333</code>.<br /> </p> </td>
  </tr>
  <tr>
   <td><p><code>table-odd-row-bg-color</code></p> </td>
   <td><p>홀수 본문 행의 배경색입니다. 기본값은 <code>rgb(255, 255, 255)</code>입니다.</p> </td>
  </tr>
  <tr>
   <td><p><code>table-even-row-bg-color</code></p> </td>
   <td><p>짝수 본문 행의 배경색입니다. 기본값은 <code>#eee</code>입니다.</p> </td>
  </tr>
 </tbody>
</table>

## 첨부 파일 {#file-attachment}

적응형 양식의 파일 첨부 파일 위젯을 사용하여 파일을 업로드할 수 있습니다. 변수를 사용하여 위젯을 사용자 정의할 수도 있습니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>변수 </strong></p> </td>
   <td><p><strong>설명</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemPadding</code></p> </td>
   <td><p>위젯에 표시된 파일의 패딩</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemBackground</code></p> </td>
   <td><p>파일 항목의 배경색</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemBorderColor</code></p> </td>
   <td><p>상단 테두리의 테두리 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemColor</code></p> </td>
   <td><p>파일 항목의 글꼴 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>filePreviewIconColor</code></p> </td>
   <td><p>위젯의 미리 보기 아이콘(Bootstrap 아이콘)에 대한 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemCommentHeight</code></p> </td>
   <td><p>파일 항목에 대한 주석 높이</p> </td>
  </tr>
 </tbody>
</table>

## 네비게이터 스타일 {#navigator-styles}

네비게이터 탭에는 네 가지 유형이 있습니다. 여기에는 왼쪽, 상단, 마법사 및 아코디언의 탭이 포함됩니다. 각 네비게이터에는 서로 다른 분류가 있습니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>네비게이터</strong></p> </td>
   <td><p><strong>CSS 클래스</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>Accordion</code></p> </td>
   <td><p>.accordion-navigators</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs on the left</code></p> </td>
   <td><p>.tab-navigators-vertical</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs on the top</code></p> </td>
   <td><p>.tab-navigators</p> </td>
  </tr>
  <tr>
   <td><p><code>Wizard</code></p> </td>
   <td><p>.wizard-navigators</p> </td>
  </tr>
 </tbody>
</table>

다음은 부트스트랩 탭과 유사한 탭 네비게이터 요소에 대한 HTML 코드입니다.

`<li>`

`<a>tab title</a>`

`</li>`

`Accordion navigator is an exception, it has following barebone`

`structure:`

`<div class="accordion.navigators">`

`<div>`

`<div class = "guideHeader">`

`<a>`

`<span class = "guideSummary" ></code>`

`........................... repeatable buttons, if the repeatable configuration is set ................................`

`<div class = "repeatableButtons">`

`<button name="Add" class="Add"/>`

`<button name="Remove" class="Remove"/>`

`</div>`

`</a>`

`</div>`

`................................ panel content ..................................`

`</div>`

`</div>`

다음을 사용하여 요소를 선택하는 CSS 규칙을 사용하여 탐색기의 스타일을 변경할 수 있습니다. **하위 항목** 선택기. 예를 들어 앵커 태그에 텍스트 장식 스타일을 추가하려면 다음을 수행합니다.

상단의 탭 탐색기:

`.tab-navigators`

`li a {`

`text-decoration:`

`underline;`

`}`

`Tab navigator on left:`

`.tab-navigators-vertical`

`li a {`

`text-decoration:`

`underline;`

`}`

`Accordion navigator:`

`.accordion-navigators .guideHeader a .guideSummary {`

`text-decoration:`

`underline;`

`}`

`Wizard navigator:`

`.wizard-navigators`

`li a {`

`text-decoration:`

`underline;`

`}`

또한 중첩된/하위/하위 탐색기가 있는지 여부에 따라 탭 탐색기의 스타일을 지정하는 클래스(왼쪽 및 위쪽 모두)가 있습니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 클래스</strong></p> </td>
   <td><p><strong>설명</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>nested_true</code></p> </td>
   <td><p>중첩된/하위/하위 탐색기가 있는 탭 탐색기(왼쪽 및 위쪽)</p> </td>
  </tr>
  <tr>
   <td><p><code>nested_false</code></p> </td>
   <td><p>중첩된/하위/하위 탐색기가 없는 탭 탐색기(왼쪽 및 위쪽)</p> </td>
  </tr>
 </tbody>
</table>

guideNavIcon 클래스는 탭 탐색기(왼쪽 및 위쪽 모두)와 마법사 탐색기에 기본 아이콘을 제공합니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 클래스 </strong></p> </td>
   <td><p><code>guideNavIcon</code></p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>작성 중인 패널에 CSS 클래스를 제공하여 특정 탐색기의 아이콘을 변경할 수 있습니다(예: 양식 ) &lt;class_name>. 을(를) 추가합니다. **&lt;class_name>_nav** 네비게이터 아이콘.

<table>
 <tbody>
  <tr>
   <td><p><strong>변수 </strong></p> </td>
   <td><p><strong>설명</strong></p> </td>
  </tr>
  <tr>
   <td><p><strong>탭 네비게이터</strong></p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p><code>navigator-bg-color</code></p> </td>
   <td><p>전체 탭 탐색기의 배경색</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-bg-color</code></p> </td>
   <td><p>탭의 배경색</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-font-color</code></p> </td>
   <td><p>탭의 글꼴 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-hover-bg-color</code></p> </td>
   <td><p>마우스로 가리키면 탭의 배경색</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-hover-font-color</code></p> </td>
   <td><p>마우스로 가리키면 탭의 글꼴 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-active-bg-color</code></p> </td>
   <td><p>패널이 포커스에 있을 때의 배경색(활성)</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-active-font-color</code></p> </td>
   <td><p>패널이 포커스에 있을 때의 글꼴 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-completed-bg-color</code></p> </td>
   <td><p>패널의 완료 표현식이 true를 반환하는 경우의 배경색</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-completed-font-color</code></p> </td>
   <td><p>패널의 완료 표현식이 true를 반환하는 경우 글꼴 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-stepped-bg-color</code></p> </td>
   <td>패널이 한 번 포커스에 있지만 완료 표현식이 false를 반환하는 경우 배경색입니다. </td>
  </tr>
  <tr>
   <td><p><code>tabs-stepped-font-color</code></p> </td>
   <td>패널이 한 번 포커스에 있었으나 완료 표현식이 false를 반환하는 경우 글꼴 색상 </td>
  </tr>
  <tr>
   <td><p><code>tabs-border-color</code></p> </td>
   <td><p>탭의 테두리 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-font-size</code></p> </td>
   <td><p>탭의 글꼴 크기</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-padding</code></p> </td>
   <td><p>탭의 패딩</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-margin</code></p> </td>
   <td><p>탭의 여백</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-vertical-margin</code></p> </td>
   <td><p>세로 탭의 여백</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-border-thickness</code></p> </td>
   <td><p>탭의 테두리 크기</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-min-height</code></p> </td>
   <td><p>탭의 최소 높이</p> </td>
  </tr>
  <tr>
   <td><p><code>heirarichal-indent</code></p> </td>
   <td><p>중첩된 탭의 들여쓰기</p> </td>
  </tr>
  <tr>
   <td><p><strong>마법사 탐색기</strong></p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-navigator-bg-color</code></p> </td>
   <td>전체 마법사 탐색기의 배경색</td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-bg-color</code></p> </td>
   <td><p>마법사의 배경색</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-font-color</code></p> </td>
   <td><p>마법사의 글꼴 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-active-bg-color</code></p> </td>
   <td><p>패널이 포커스에 있을 때의 배경색(활성)</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-active-font-color</code></p> </td>
   <td><p>패널이 포커스에 있을 때의 글꼴 색상(포커스 지정)</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-completed-bg-color</code></p> </td>
   <td><p>패널의 완료 표현식이 true를 반환하는 경우의 배경색</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-completed-font-color</code></p> </td>
   <td><p>패널의 완료 표현식이 true를 반환하는 경우 글꼴 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-stepped-bg-color</code></p> </td>
   <td>패널이 한 번 포커스에 있지만 완료 표현식이 false를 반환하는 경우 배경색입니다.</td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-stepped-font-color</code></p> </td>
   <td><p>패널에 한 번 포커스를 설정했지만 완료 표현식이 false를 반환하는 경우 글꼴 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-border-color</code></p> </td>
   <td><p>마법사 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-font-size</code></p> </td>
   <td><p>마법사의 글꼴 크기</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-padding</code></p> </td>
   <td><p>마법사의 패딩</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-border-thickness</code></p> </td>
   <td><p>마법사의 테두리 크기</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-nav-bullet-border</code></p> </td>
   <td><p>마법사 네비게이터 글머리 기호의 테두리 색상(캡션/레이블 접두사 사용)</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-progress-bg-color</code></p> </td>
   <td><p>마법사 탐색기 진행률 표시줄의 배경색</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-progress-color</code></p> </td>
   <td><p>진행률 표시줄의 채우기 색상</p> </td>
  </tr>
  <tr>
   <td><p><strong>어코디언 탐색기</strong></p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p><code>accordion-tabs-padding</code></p> </td>
   <td><p>아코디언에 대한 패딩</p> </td>
  </tr>
 </tbody>
</table>

## 패널 스타일 지정 {#panel-styling}

패널 에는 선택적 도구 모음 및 그 컨텐츠가 포함되어 있습니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 클래스 </strong></p> </td>
   <td><p><code>guidePanelNode</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>변수 </strong></p> </td>
   <td><p><strong>설명</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>panel-background-color</code></p> </td>
   <td><p>패널의 배경색</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-font-size</code></p> </td>
   <td><p>패널 텍스트의 글꼴 크기</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-font-color</code></p> </td>
   <td><p>패널 텍스트의 글꼴 색상<br /> </p> </td>
  </tr>
  <tr>
   <td><p><code>panel-padding</code></p> </td>
   <td><p>패널 내부 패딩</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-description-font-size</code></p> </td>
   <td><p>패널 설명의 글꼴 크기</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-description-padding</code></p> </td>
   <td><p>패널 설명의 패딩</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-help-bg-color</code></p> </td>
   <td><p>패널 도움말의 배경색</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-help-border-indicator-color</code></p> </td>
   <td><p>패널 도움말의 표시기 테두리 색상</p> </td>
  </tr>
 </tbody>
</table>

패널 노드는 탐색기와 콘텐츠로 나뉩니다. 거기 `` `` 콘텐츠에 대한 별도의 스타일 구성 요소가 없습니다. 설명된 변수는 네비게이터 및 콘텐츠에 적용됩니다.

최상위 패널(RootPanel)에 이 클래스가 없습니다.

## 모바일 스타일링 {#mobile-styling}

## 헤더 막대 {#header-bar}

이러한 변수는 패널 제목과 다음 및 뒤로 탐색기가 포함된 모바일 장치나 작은 화면 장치에 표시되는 헤더 막대에 영향을 줍니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 클래스 </strong></p> </td>
   <td><p><code>guide-header-bar</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>변수 </strong></p> </td>
   <td><p><strong>설명</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>headerbar-background-color</code></p> </td>
   <td><p>헤더 막대의 배경색</p> </td>
  </tr>
  <tr>
   <td><p><code>headerbar-font-color</code></p> </td>
   <td><p>헤더 막대 내의 텍스트에 대한 글꼴 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>headerbar-padding</code></p> </td>
   <td><p>헤더 막대에 대한 패딩</p> </td>
  </tr>
 </tbody>
</table>

## 스크롤 표시기 {#scroll-indicator}

이러한 변수는 모바일 장치나 작은 화면 장치에 표시되는 주황색 화살표인 스크롤 표시기에 영향을 줍니다. 스크롤 표시기는 화면에 표시되는 부분 너머에 콘텐츠가 있음을 나타냅니다. 아래로 스크롤하여 볼 수 있습니다. 콘텐츠의 끝에 도달하면 화살표가 사라집니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 클래스 </strong></p> </td>
   <td><p><code>mobileScrollIndicator</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>변수 </strong></p> </td>
   <td><p><strong>설명</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorBottom</code></p> </td>
   <td><p>아래에서 scrollindicator의 위치가 고정됨</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorRight</code></p> </td>
   <td><p>오른쪽에서 scrollindicator 고정 위치</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorWidth</code></p> </td>
   <td><p>scrollindicator 폭</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorHeight</code></p> </td>
   <td><p>스크롤 제한기 높이</p> </td>
  </tr>
 </tbody>
</table>

## 모바일 고정 도구 모음 레이아웃 관련 변수 {#mobile-fixed-toolbar-layout-specific-variables}

다음 표의 이러한 변수는 모바일 고정 도구 모음 레이아웃에 영향을 줍니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 클래스 </strong></p> </td>
   <td><p><code>mobileToolbar</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>변수 </strong></p> </td>
   <td><p><strong>설명</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarBottom</code></p> </td>
   <td><p>모바일 장치에서 아래쪽에서 도구 모음 위치 고정</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarTop</code></p> </td>
   <td><p>모바일 장치에서 위에서 도구 모음의 위치가 수정되었습니다.</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarLeft</code></p> </td>
   <td><p>모바일 장치에서 왼쪽에서 도구 모음의 위치가 수정되었습니다.</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarRight</code></p> </td>
   <td><p>모바일 장치에서 오른쪽에서 도구 모음 위치 고정</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileButtonIconTopMargin</code></p> </td>
   <td><p>도구 모음 단추 아이콘의 위치를 위에서 수정했습니다.</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileButtonIconWidth</code></p> </td>
   <td><p>모바일 장치에서 도구 모음의 버튼 아이콘 폭</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileButtonIconHeight</code></p> </td>
   <td><p>모바일 장치에서 도구 모음의 버튼 아이콘 높이</p> </td>
  </tr>
  <tr>
   <td><p><code>mobilefixedtoolbarbgcolor</code></p> </td>
   <td><p>모바일 장치에서 도구 모음의 배경색</p> </td>
  </tr>
 </tbody>
</table>

## 테마별 변수 {#theme-specific-variable}

다음 **단순 등록** /etc/clientlibs/fd/af/guidetheme/simpleEnrollment의 테마 및 카테고리 `guide.theme.simpleEnrollment` 몇 가지 변수도 소개합니다. 단순 등록을 개선하는 테마를 만들려면 다음 &quot;추가 변수&quot;를 사용할 수 있습니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>변수 </strong></p> </td>
   <td><p><strong>설명</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>button-focus-bg-color</code></p> </td>
   <td><p>포커스 단추 배경색</p> </td>
  </tr>
  <tr>
   <td><p><code>button-hover-bg-color</code></p> </td>
   <td><p>마우스로 가리키면 단추의 배경색</p> </td>
  </tr>
  <tr>
   <td><p><code>button-radius</code></p> </td>
   <td><p>단추 반경</p> </td>
  </tr>
  <tr>
   <td><p><code>navigation-button-bg-color</code></p> </td>
   <td><p>탐색 단추의 배경색(뒤/다음)</p> </td>
  </tr>
  <tr>
   <td><p><code>navigation-button-bg-hover-color</code></p> </td>
   <td><p>마우스로 가리키면 탐색 단추(뒤/다음)의 배경색</p> </td>
  </tr>
  <tr>
   <td><p><code>initial-nav-color</code></p> </td>
   <td><p>마법사 탐색기의 배경색 및 해당 진행률 표시줄(처음 렌더링될 때).</p> </td>
  </tr>
  <tr>
   <td><p><code>active-nav-color</code></p> </td>
   <td>현재/활성 마법사 탐색기 및 해당 진행률 표시줄의 배경색입니다. </td>
  </tr>
  <tr>
   <td><p><code>visited-nav-color</code></p> </td>
   <td><p>방문한 마법사 탐색기와 해당 진행률 표시줄의 배경색입니다.</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-bifercating-border-color</code></p> </td>
   <td><p>탐색기와 패널에 테두리 색상 분기 컨테이너</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-navigator-separator-color</code></p> </td>
   <td><p>왼쪽 탭의 하단 테두리 색상 분리 탭(탭 탐색기).</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-child-nav-bg-color</code></p> </td>
   <td><p>네비게이터의 중첩/하위/하위 네비게이터의 배경색</p> </td>
  </tr>
 </tbody>
</table>
