---
title: 적응형 양식의 스타일 지정 구문
seo-title: 적응형 양식의 스타일 지정 구문
description: LESS 프레임워크를 사용하여 적응형 양식의 모양을 사용자 정의합니다.
seo-description: LESS 프레임워크를 사용하여 적응형 양식의 모양을 사용자 정의합니다.
uuid: d2e45ad9-7322-43ce-a1dd-ad97e2eea742
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: ed50fa70-a8dd-4cc6-82a9-d59de0fa417d
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2324'
ht-degree: 3%

---


# 적응형 양식의 스타일 구문{#styling-constructs-for-adaptive-forms}

## 전제 조건 {#prerequisites}

CSS 및 LESS 프레임워크에 대한 지식

## {#what-can-be-customized} 사용자 정의할 수 있는 항목

이 문서에서는 응용 양식의 공개적으로 사용 가능한 css 클래스를 나열합니다. 이러한 클래스를 활용하여 적응형 양식의 다양한 구성 요소에 스타일을 지정할 수 있습니다. 경고를 표시하는 대화 상자 및 상태 막대와 같은 제작 구성 요소의 스타일링은 이 문서의 범위를 벗어납니다. [테마 편집기](https://helpx.adobe.com/experience-manager/6-3/forms/using/themes.html)를 사용하여 구성 요소의 스타일을 지정할 수 없는 경우에만 이러한 스타일 구문을 사용하여 스타일(CSS 또는 Less 사용)을 만듭니다.

## 적응형 양식의 스타일 사용자 지정 {#customizing-styles-in-adaptive-forms}

LESS 프레임워크를 사용하면 응용 양식의 스타일을 사용자 정의하는 사용 사례를 간소화할 수 있습니다. 이 프레임워크를 사용하면 변수 및 함수(mixins) 세트를 사용하여 스타일을 정의할 수 있습니다. LESS 프레임워크는 번들로 묶은 코드의 크기를 줄이고 재사용성을 높이는 데 도움이 됩니다.

다음과 같은 방법으로 응용 양식 스타일을 사용자 정의할 수 있습니다.

* 테마 변경
* 구성 요소의 스타일 변경

## 테마 {#changing-theme} 변경

적응형 양식의 테마를 변경하여 해당 모양이 적응형 양식이 포함된 웹 페이지와 일치하는지 확인할 수 있습니다.

CSS 속성을 사용하는 응용 양식의 전체 모양 변경 사항은 일반적으로 테마 변경의 일부입니다. 레이아웃 변경 및 구성 요소 배치 변경과 같은 &quot;적용 양식의 확인 및 느낌&quot;에 대한 주요 변경 사항은 테마 변경 사항으로 간주되지 않습니다.

부트스트랩을 기반으로 하는 다음 CSS 속성 세트는 웹 페이지의 테마를 정의합니다.

* 배경색
* 테두리(문자, 색상, 두께)
* 글꼴 색상
* 사진 간격
* 여백
* 글꼴 크기
* 선 높이

현재, LESS 변수는 적응형 양식의 다양한 요소의 이러한 속성에 대해서만 정의됩니다.

## 구성 요소 스타일 {#changing-component-style} 변경

요소의 모양, 레이아웃, 배치 및 가시성을 변경할 수 있습니다. 이 작업을 수행하려면 이 문서에 나열된 스타일 구절을 포함하도록 사용자 지정 .css 파일을 만들거나 업데이트합니다.

적응형 양식에 스타일을 적용하려면 응용 양식을 열어 편집할 수 있고 적응형 양식 컨테이너의 속성을 열 수 있으며 기본 탭에서 사용자 지정 CSS 파일 경로를 지정합니다. 적응형 양식의 스타일 구문을 정의하고 사용자 지정 .css 파일에 나열된 구문으로 재정의됩니다.

## 구성 요소 {#components}

이 문서에서 설명한 구성 요소에는 미리 정의된 CSS 클래스가 있습니다. 변수를 편집하여 CSS 클래스의 스타일을 수정할 수 있습니다. 또는 전체 클래스를 다시 작성할 수 있습니다. 이 섹션에서는 변수를 사용하여 수정할 수 있는 구성 요소 및 스타일 내의 클래스에 대해 설명합니다.

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
   <td><p>컨테이너 패딩</p> </td>
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

적응형 양식에는 다양한 유형의 필드가 포함됩니다. 각 필드에는 고유한 클래스 이름이 있으며, 이 이름은 필드의 이름입니다. 이 필드에는 공통 클래스 이름 `guideFieldNode`도 있습니다.

필드에는 레이블, 위젯, 도움말 설명(긴 설명 및 짧은 설명 모두) 및 필드 도움말 아이콘(물음표)이 있습니다.

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
   <td><p>필드의 오류 메시지의 글꼴 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>field-error-font-size</code></p> </td>
   <td><p>필드의 오류 메시지의 글꼴 크기</p> </td>
  </tr>
 </tbody>
</table>

## 레이블 스타일 지정 {#label-styling}

필드에 사용되는 HTML 요소 **label**&#x200B;에는 레이블이 맨 위나 왼쪽에 있는지 여부에 따라 클래스 **left** 또는 **top**&#x200B;이 포함됩니다.

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
   <td>필드 레이블의 CSS 행 높이 속성 </td>
  </tr>
  <tr>
   <td><p><code>label-font-weight</code></p> </td>
   <td>필드 레이블에 대한 CSS 글꼴 두께 속성 </td>
  </tr>
  <tr>
   <td><p><code>label-margin</code></p> </td>
   <td><p>필드 레이블의 여백</p> </td>
  </tr>
 </tbody>
</table>

레이블의 CSS 규칙은 **guideFieldLabel** 레이블을 사용하여 적용됩니다. 작성자인 경우 이 규칙을 무시하여 사용자 지정 변경 사항을 표시합니다.

## 위젯 스타일 지정 {#widgets-styling}

위젯은 유형에 따라 클래스도 포함합니다. 일반적으로 위젯에는 `guideFieldWidget` 클래스가 포함됩니다. 일반적으로 HTML과 함께 제공되는 위젯은 표준 HTML 요소 입력을 사용하고 선택합니다. 스타일링은 그에 따라 수행됩니다. 변수를 변경하여 사용자 정의 위젯의 스타일을 지정할 수 없습니다.

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
   <td>위젯의 배경색(확인란 및 라디오 단추 사용 안 함)</td>
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
   <td><p>위젯의 테두리 유형</p> </td>
  </tr>
  <tr>
   <td><p><code>widget-border-focus-type</code></p> </td>
   <td><p>위젯 테두리의 초점 유형</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border</code></p> </td>
   <td><p>위젯의 통합된 테두리 스타일</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-font-color</code></p> </td>
   <td><p>위젯 내의 텍스트 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-font-size</code></p> </td>
   <td><p>위젯 내의 텍스트 크기</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-line-height</code></p> </td>
   <td>위젯의 CSS 줄 높이 속성 </td>
  </tr>
  <tr>
   <td><p><code>widgets-padding</code></p> </td>
   <td><p>위젯의 CSS 패딩 속성</p> </td>
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
   <td><p>필드를 사용할 수 없을 때 위젯의 배경색</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-font-color</code></p> </td>
   <td><p>필드를 사용할 수 없을 때 위젯의 글꼴 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-border-color</code></p> </td>
   <td><p>필드를 사용할 수 없을 때 위젯의 테두리 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>widget-height</code></p> </td>
   <td>위젯의 높이(체크 상자 및 라디오 단추에 대해 작동하지 않음)</td>
  </tr>
  <tr>
   <td><p><code>checkbutton-height</code></p> </td>
   <td><p>확인란 및 라디오 단추의 높이입니다.</p> </td>
  </tr>
  <tr>
   <td><p><code>listboxwidget-height</code></p> </td>
   <td><p>다중 선택 드롭다운의 최대 높이</p> </td>
  </tr>
 </tbody>
</table>

### 위젯 스타일 지정 제한 사항 {#limitations-in-widget-styling}

중점, 필수 및 비활성화 필드의 스타일링은 변수를 사용하여 제한됩니다. 그러나 스타일을 재정의하여 변경할 수 있습니다. 변수의 사용 제한은 주로 변수의 수를 확인하기 위해 제공됩니다. 이전에 논의된 모든 주에 있기 때문에 필드의 모양이 크게 변경되면 제한이 완화될 수 있습니다.

## 도움말 설명 {#help-description}

작성자는 짧은 및 긴 설명 구성 요소를 사용하여 필드에 도움말 컨텐츠를 지정할 수 있습니다. 두 구성 요소 모두 설명 유형에 따라 공통 클래스 `.guideHelpDescription` 및 다른 클래스 `.long`/ `.short`가 있습니다. 도움말 내용은 설명 스타일을 재정의하기 위한 단락 요소에 포함되어 있습니다. 도움말 설명(긴 및 짧은 모두)은 다음 표에 설명된 대로 widgetshelp로 시작하는 변수를 사용하여 수정합니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>변수 </strong></p> </td>
   <td><p><strong>설명</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-bg-color</code></p> </td>
   <td><p>위젯 긴 도움말의 배경색</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-border-color</code></p> </td>
   <td><p>위젯 긴 도움말의 테두리 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-border-indicator-color</code></p> </td>
   <td><p>위젯의 긴 도움말의 왼쪽 표시기 테두리 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-bg-color</code></p> </td>
   <td><p>위젯의 배경색 짧은 도움말</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-color</code></p> </td>
   <td><p>위젯 짧은 도움말의 글꼴 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-tooltip-bg-color</code></p> </td>
   <td><p>위젯의 짧은 도구 설명 배경색 도움말</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-tooltip-color</code></p> </td>
   <td><p>위젯의 짧은 도구 설명 글꼴 색상 도움말</p> </td>
  </tr>
 </tbody>
</table>

## 사용 약관 {#terms-and-conditions}

약관(TnC `` ``) 위젯을 사용하면 조건을 지정할 수 있습니다. 다음 표에 설명된 변수를 사용하여 위젯을 사용자 정의할 수 있습니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>변수 </strong></p> </td>
   <td><p><strong>설명</strong></p> </td>
  </tr>
  <tr>
   <td><code>tnc-unvisited</code></td>
   <td>방문하지 않은 tnc 링크의 글꼴 색상입니다.</td>
  </tr>
  <tr>
   <td><code>tnc-visited</code></td>
   <td>방문한 tnc 링크의 글꼴 색상입니다.</td>
  </tr>
 </tbody>
</table>

## 단추 {#button}

버튼도 위젯입니다. 그러나 위젯과 스타일이 약간 다릅니다. 적응형 양식에서는 다음 중 하나가 단추를 구성합니다.

* input[type = text]
* 단추
* .button 클래스가 있는 요소

버튼용 HTML 코드:

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
   <td><p>단추용 아이콘을 제공합니다.</p> </td>
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
   <td><p>버튼의 CSS 패딩 속성</p> </td>
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
   <td><p>큰 단추 패딩(클래스 .buttonlarge의 단추)</p> </td>
  </tr>
  <tr>
   <td><p><code>button-large-font-size</code></p> </td>
   <td><p>큰 단추의 글꼴 크기</p> </td>
  </tr>
  <tr>
   <td><p><code>button-small-padding</code></p> </td>
   <td><p>작은 단추 패딩(.buttonsmall 클래스의 단추)</p> </td>
  </tr>
  <tr>
   <td><p><code>button-small-font-size</code></p> </td>
   <td><p>작은 단추의 글꼴 크기</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-background-color</code></p> </td>
   <td><p>유용한 정보 단추용 배경색(.buttoninvestive 클래스의 단추)</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-font-color</code></p> </td>
   <td><p>유용한 정보를 제공하는 버튼의 글꼴 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-border-color</code></p> </td>
   <td><p>정보 단추 테두리의 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-background-color</code></p> </td>
   <td><p>경고 스타일이 적용된 단추에 대한 배경색(클래스 .buttonwarning이 있는 단추)</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-font-color</code></p> </td>
   <td><p>경고 스타일 단추에 대한 글꼴 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-border-color</code></p> </td>
   <td><p>경고 스타일 단추에 대한 테두리 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>button-alert-background-color</code></p> </td>
   <td><p>경고 단추에 대한 배경색(클래스 .buttonalert가 있는 단추)</p> </td>
  </tr>
  <tr>
   <td><p><code>button-alert-font-color</code></p> </td>
   <td><p>경고 단추용 글꼴 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>button-alert-border-color</code></p> </td>
   <td><p>경고 단추에 대한 테두리 색상</p> </td>
  </tr>
 </tbody>
</table>

## 물음표 {#question-mark}

위젯의 경우 작성자가 도움말 컨텐츠에 긴 설명을 추가할 때 questionMark가 표시됩니다. 부트스트랩에 제공된 기본 아이콘이 사용됩니다. 사용자 정의 아이콘을 사용하려면 부트스트랩 아이콘을 사용자 정의할 수 있습니다.

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
   <td><p>마우스가 마우스로 마우스로 가리킬 때 아이콘의 색상</p> </td>
  </tr>
 </tbody>
</table>

## 표 {#table}

다음 변수를 사용하여 표의 머리글 및 본문 행에 대한 색상 테마를 변경할 수 있습니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>변수 </strong></p> </td>
   <td><p><strong>설명</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>table-header-bg-color</code></p> </td>
   <td><p>머리글 행의 배경색입니다. 기본값은 <code>#333</code>입니다.<br /> </p> </td>
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

적응형 양식의 [첨부 파일] 위젯을 사용하면 파일을 업로드할 수 있습니다. 변수를 사용하여 위젯을 사용자 정의할 수도 있습니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>변수 </strong></p> </td>
   <td><p><strong>설명</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemPadding</code></p> </td>
   <td><p>위젯에 표시되는 파일의 패딩</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemBackground</code></p> </td>
   <td><p>파일 항목의 배경색</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemBorderColor</code></p> </td>
   <td><p>위쪽 테두리의 테두리 색상</p> </td>
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
   <td><p>파일 항목의 주석 높이</p> </td>
  </tr>
 </tbody>
</table>

## 내비게이터 스타일 {#navigator-styles}

4가지 유형의 네비게이터 탭이 있습니다. 여기에는 마법사 및 아코디언을 사용하여 왼쪽, 위쪽, 아래쪽 등의 탭이 포함됩니다. 각 네비게이터에는 다른 클래스가 있습니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>내비게이터</strong></p> </td>
   <td><p><strong>CSS 클래스</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>Accordion</code></p> </td>
   <td><p>.accordion 탐색자</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs on the left</code></p> </td>
   <td><p>.tab-navigator-vertical</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs on the top</code></p> </td>
   <td><p>.tab-navigator</p> </td>
  </tr>
  <tr>
   <td><p><code>Wizard</code></p> </td>
   <td><p>.wizard-탐색자</p> </td>
  </tr>
 </tbody>
</table>

탭 탐색기 요소의 HTML 코드는 다음과 같습니다(부트스트랩 탭과 유사).

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

**하위** 선택기를 사용하여 요소를 선택하는 CSS 규칙을 사용하여 탐색기의 스타일을 변경할 수 있습니다. 예를 들어 앵커 태그에 텍스트 장식 스타일을 추가하려면 다음을 수행하십시오.

위쪽 탭 탐색기:

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

또한 중첩된/자식/하위 탐색기가 있는지 여부에 따라 탭 탐색자의 스타일 지정(왼쪽 및 위쪽 모두)할 클래스가 있습니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 클래스</strong></p> </td>
   <td><p><strong>설명</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>nested_true</code></p> </td>
   <td><p>중첩된/자식/하위 탐색자가 있는 탭 탐색자(왼쪽 및 위쪽)</p> </td>
  </tr>
  <tr>
   <td><p><code>nested_false</code></p> </td>
   <td><p>중첩된/자식/하위 탐색자가 없는 탭 탐색자(왼쪽 및 위쪽)</p> </td>
  </tr>
 </tbody>
</table>

guideNavIcon 클래스는 탭 내비게이터(왼쪽 및 상단 모두)와 마법사 탐색기에 기본 아이콘을 제공합니다.

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
>작성의 패널에 CSS 클래스를 제공하여 특정 탐색기의 아이콘을 변경할 수 있습니다(예: &lt;CLASS_NAME>). 탐색기의 아이콘에 **&lt;CLASS_NAME>_nav**&#x200B;을(를) 추가합니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>변수 </strong></p> </td>
   <td><p><strong>설명</strong></p> </td>
  </tr>
  <tr>
   <td><p><strong>탭 내비게이터</strong></p> </td>
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
   <td><p>마우스로 가리키는 탭의 글꼴 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-active-bg-color</code></p> </td>
   <td><p>패널에 초점이 있을 때 배경색(활성)</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-active-font-color</code></p> </td>
   <td><p>패널에 포커스가 있는 경우 글꼴 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-completed-bg-color</code></p> </td>
   <td><p>패널의 완료 표현식이 true를 반환하는 경우 배경색</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-completed-font-color</code></p> </td>
   <td><p>패널의 완료 표현식이 true를 반환하는 경우 글꼴 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-stepped-bg-color</code></p> </td>
   <td>패널에 포커스가 한 번 있어도 완료 표현식에서 false를 반환하는 경우의 배경색 </td>
  </tr>
  <tr>
   <td><p><code>tabs-stepped-font-color</code></p> </td>
   <td>패널에 포커스가 한 번 있어도 완료 표현식에서 false를 반환하는 경우 글꼴 색상입니다. </td>
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
   <td><p>탭 패딩</p> </td>
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
   <td><p><strong>마법사 탐색자</strong></p> </td>
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
   <td><p>패널에 초점이 있을 때 배경색(활성)</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-active-font-color</code></p> </td>
   <td><p>패널에 초점이 있을 때 글꼴 색상(집중)</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-completed-bg-color</code></p> </td>
   <td><p>패널의 완료 표현식이 true를 반환하는 경우 배경색</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-completed-font-color</code></p> </td>
   <td><p>패널의 완료 표현식이 true를 반환하는 경우 글꼴 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-stepped-bg-color</code></p> </td>
   <td>패널에 포커스가 있는 상태에서 완료 표현식이 false를 반환하는 경우 배경색</td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-stepped-font-color</code></p> </td>
   <td><p>패널에 한 번 초점이 맞춰졌지만 완료 표현식에서 false를 반환하는 경우 글꼴 색상입니다.</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-border-color</code></p> </td>
   <td><p>마법사의 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-font-size</code></p> </td>
   <td><p>마법사의 글꼴 크기</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-padding</code></p> </td>
   <td><p>마법사 패딩</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-border-thickness</code></p> </td>
   <td><p>마법사의 테두리 크기</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-nav-bullet-border</code></p> </td>
   <td><p>마법사 탐색기 글머리 기호(캡션/레이블 미리 고정)의 테두리 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-progress-bg-color</code></p> </td>
   <td><p>마법사 탐색기 진행률 표시줄의 배경색</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-progress-color</code></p> </td>
   <td><p>진행률 표시줄용 채우기 색상</p> </td>
  </tr>
  <tr>
   <td><p><strong>아코디언 내비게이터</strong></p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p><code>accordion-tabs-padding</code></p> </td>
   <td><p>아코디언 패딩</p> </td>
  </tr>
 </tbody>
</table>

## 패널 스타일 {#panel-styling}

패널에는 선택 사항 도구 모음과 해당 컨텐츠가 포함되어 있습니다.

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
   <td><p>패널 텍스트<br />의 글꼴 색상 </p> </td>
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
   <td><p>패널 설명 패딩</p> </td>
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

패널 노드는 내비게이터와 컨텐츠로 구분됩니다. 콘텐츠에 대한 별도의 스타일 구성 요소가 `` ``에 없습니다. 설명된 변수는 컨텐츠뿐만 아니라 네비게이터에 적용됩니다.

맨 위의 패널(RootPanel)에 이 클래스가 없습니다.

## 모바일 스타일 {#mobile-styling}

## 헤더 막대 {#header-bar}

이러한 변수는 모바일 장치 또는 패널 제목과 다음 및 뒤로 내비게이터가 포함된 작은 화면 장치에 표시되는 헤더 막대에 영향을 줍니다.

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
   <td><p>머리글 막대의 패딩</p> </td>
  </tr>
 </tbody>
</table>

## 스크롤 표시기 {#scroll-indicator}

이러한 변수는 모바일 장치 또는 작은 화면 장치에 표시되는 주황색 화살표인 스크롤 표시기에 영향을 줍니다. 스크롤 표시기는 화면에서 볼 수 있는 부분 이외의 내용이 있음을 나타냅니다. 아래로 스크롤하여 볼 수 있습니다. 컨텐츠 끝을 누르면 화살표가 사라집니다.

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
   <td><p>아래쪽의 스크롤라인표시기 위치가 수정되었습니다.</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorRight</code></p> </td>
   <td><p>오른쪽에서 스크롤리표시기 위치 수정</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorWidth</code></p> </td>
   <td><p>스크롤리디케이터 너비</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorHeight</code></p> </td>
   <td><p>스크롤리디케이터의 높이</p> </td>
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
   <td><p>도구 모음, 모바일 장치, 아래쪽에서 고정 위치</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarTop</code></p> </td>
   <td><p>도구 모음, 모바일 장치, 맨 위에서 고정 위치</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarLeft</code></p> </td>
   <td><p>모바일 장치에서 왼쪽에서 도구 모음 위치를 수정했습니다.</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarRight</code></p> </td>
   <td><p>모바일 장치에서 오른쪽의 도구 모음 위치를 수정했습니다.</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileButtonIconTopMargin</code></p> </td>
   <td><p>도구 모음 단추 아이콘의 맨 위에서 위치를 수정했습니다.</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileButtonIconWidth</code></p> </td>
   <td><p>모바일 장치에서 도구 모음 단추 아이콘의 너비</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileButtonIconHeight</code></p> </td>
   <td><p>모바일 장치에서 도구 모음 단추 아이콘의 높이</p> </td>
  </tr>
  <tr>
   <td><p><code>mobilefixedtoolbarbgcolor</code></p> </td>
   <td><p>모바일 디바이스의 툴바 배경색</p> </td>
  </tr>
 </tbody>
</table>

## 테마별 변수 {#theme-specific-variable}

/etc/clientlibs/fd/af/guitertheme/simpleEnrollment 및 `guide.theme.simpleEnrollment` 범주의 **간단한 등록** 테마도 몇 가지 변수를 소개합니다. 간단한 등록을 향상시키는 테마를 만들려면 &quot;추가 변수:

<table>
 <tbody>
  <tr>
   <td><p><strong>변수 </strong></p> </td>
   <td><p><strong>설명</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>button-focus-bg-color</code></p> </td>
   <td><p>초점 단추에 대한 배경색</p> </td>
  </tr>
  <tr>
   <td><p><code>button-hover-bg-color</code></p> </td>
   <td><p>마우스를 가져가면 단추에 대한 배경색</p> </td>
  </tr>
  <tr>
   <td><p><code>button-radius</code></p> </td>
   <td><p>단추 반경</p> </td>
  </tr>
  <tr>
   <td><p><code>navigation-button-bg-color</code></p> </td>
   <td><p>내비게이션 버튼의 배경색(뒤/다음)</p> </td>
  </tr>
  <tr>
   <td><p><code>navigation-button-bg-hover-color</code></p> </td>
   <td><p>마우스를 가져가면 내비게이션 단추(뒤로/다음)를 위한 배경색</p> </td>
  </tr>
  <tr>
   <td><p><code>initial-nav-color</code></p> </td>
   <td><p>처음 렌더링할 때 마법사 탐색자 및 해당 진행률 표시줄을 위한 배경색입니다.</p> </td>
  </tr>
  <tr>
   <td><p><code>active-nav-color</code></p> </td>
   <td>현재/활성 마법사 탐색기 및 해당 진행률 표시줄을 위한 배경색 </td>
  </tr>
  <tr>
   <td><p><code>visited-nav-color</code></p> </td>
   <td><p>마법사 탐색자 및 방문한 해당 진행률 표시줄을 위한 배경색입니다.</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-bifercating-border-color</code></p> </td>
   <td><p>내비게이터 및 패널로 테두리 색상 혼합 컨테이너</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-navigator-separator-color</code></p> </td>
   <td><p>왼쪽(탭 내비게이터)의 탭을 구분하는 아래쪽 테두리 색상</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-child-nav-bg-color</code></p> </td>
   <td><p>탐색기의 중첩/하위/하위 탐색기를 위한 배경색</p> </td>
  </tr>
 </tbody>
</table>

