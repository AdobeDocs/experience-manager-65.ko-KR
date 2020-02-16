---
title: Interactive Communications에서 차트 사용
seo-title: Interactive Communications의 차트 구성 요소
description: 인터랙티브한 커뮤니케이션의 차트를 사용하면 대량의 정보를 손쉽게 분석할 수 있는 시각적 포맷으로 통합할 수 있습니다
seo-description: AEM Forms는 대화형 통신에서 차트를 만드는 데 사용할 수 있는 차트 구성 요소를 제공합니다. 이 문서에서는 차트 구성 요소의 기본 및 에이전트 구성에 대해 설명합니다.
uuid: 978aa431-9a5b-4964-b37c-7bfa8c3f49b9
content-type: reference
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e21714ad-d445-4aff-b0db-d577061e0907
docset: aem65
translation-type: tm+mt
source-git-commit: 44eb94b917fe88b7c90c29ec7da553e15be391db

---


# Interactive Communications에서 차트 사용{#using-charts-in-interactive-communications}

차트나 그래프는 데이터를 시각적으로 나타냅니다. 이는 대량의 정보를 이해하기 쉬운 시각적 형식으로 요약하여, 인터랙티브 커뮤니케이션의 수신자가 복잡한 데이터를 보다 시각화, 해석 및 분석할 수 있도록 합니다.

대화형 통신을 만드는 동안 차트를 추가하여 Interactive Communication의 양식 데이터 모델에서 2차원 데이터를 시각적으로 나타낼 수 있습니다. 차트 구성 요소를 사용하면 다음 유형의 차트를 추가하고 구성할 수 있습니다.파이, 열, 도넛, 막대, 선, 선 및 점, 점, 영역 및 Quadrant입니다.

## 대화형 통신에서 차트 추가 및 구성 {#add-and-configure-chart-in-an-interactive-communication}

대화형 통신에서 차트를 추가하고 구성하려면 다음 단계를 수행하십시오.

1. 대화형 **커뮤니케이션의** 사이드 킥에서 구성 요소를 누릅니다.
1. 차트 구성 요소를 **다음** 구성 요소 중 하나로 드래그하여 놓습니다.

   * 인쇄 채널:대상 영역 또는 이미지 필드
   * 웹 채널:패널 또는 대상 영역

1. Interactive Communication Editor에서 차트 구성 요소를 누르고 구성 요소 **[!UICONTROL 도구 모음에서]** 구성( ![configure_icon](assets/configure_icon.png))을 선택합니다.

   차트 등록 정보가 왼쪽 창에 표시됩니다.

   ![인쇄 채널에서 라인 유형 차트의 기본 속성](assets/chart_properties_print_new.png)

   인쇄 채널에서 라인 유형 차트의 기본 속성

   ![웹 채널의 라인 유형 차트의 기본 속성](assets/chart_properties_web_new.png)

   웹 채널의 라인 유형 차트의 기본 속성

1. 채널 유형을 기반으로 [차트 속성을](../../forms/using/chart-component-interactive-communications.md#configure-chart-properties) 구성합니다.
1. (인쇄 채널만 해당) **[!UICONTROL 에이전트 설정에서]**&#x200B;에이전트가 이 차트를 반드시 사용해야 하는지 지정합니다. [에이전트가 이 차트 사용 필수] **[!UICONTROL 옵션을 선택하지 않으면 에이전트는 [에이전트 UI의 [콘텐트]]** 탭에서 차트에 **[!UICONTROL 대한 눈 아이콘을 탭하여 차트를]** 표시하거나 숨길 수 있습니다.

   ![chart_agentproperties](assets/chart_agentproperties.png)

1. done_icon ![을](assets/done_icon.png) 눌러 차트 속성을 저장합니다.

   미리 **[!UICONTROL 보기를]** 눌러 차트와 연결된 모양 및 데이터를 봅니다. 편집을 **[!UICONTROL 눌러]** 차트의 속성을 다시 구성합니다.

## 차트 속성 구성 {#configure-chart-properties}

인쇄 및 웹 채널에 대한 차트를 만들 때 다음 속성을 구성합니다.

<table>
 <tbody>
  <tr>
   <td>필드</td>
   <td>설명</td>
   <td>채널 유형</td>
  </tr>
  <tr>
   <td>이름</td>
   <td>차트 요소의 식별자입니다. 이 필드에 지정된 차트의 이름이 차트에 표시되지 않습니다. 다른 구성 요소, 스크립트 및 SOM 표현식에서 요소를 참조할 때 사용됩니다.</td>
   <td>인쇄 및 웹</td>
  </tr>
  <tr>
   <td>차트 유형</td>
   <td>생성할 차트 유형입니다. 사용 가능한 옵션은 파이, 열, 도넛, 막대, 선, 선 및 점, 점 및 영역입니다.</td>
   <td>인쇄 및 웹</td>
  </tr>
  <tr>
   <td>시리즈 &gt; 여러 시리즈</td>
   <td>X축 및 Y축에 표시된 양식 데이터 모델 수집 항목에 대해 여러 시리즈를 추가하려면 선택합니다.</td>
   <td>인쇄 및 웹</td>
  </tr>
  <tr>
   <td>시리즈 &gt; 데이터 모델 개체</td>
   <td>차트에 여러 시리즈를 추가할 양식 데이터 모델 수집 항목의 이름입니다.<br /> X축 및 Y축에 표시된 속성의 상위 양식 데이터 모델 개체 속성을 선택하여 의미 있는 시리즈를 형성합니다. 바인딩하는 데이터 모델 개체는 Number, String 또는 Date 유형이어야 합니다.</td>
   <td>인쇄 및 웹</td>
  </tr>
  <tr>
   <td>겹쳐서 표시</td>
   <td>각 시리즈의 값을 차례대로 겹치도록 선택하십시오.</td>
   <td>인쇄 및 웹</td>
  </tr>
  <tr>
   <td>X축 &gt; 제목</td>
   <td>X축의 제목입니다.</td>
   <td>인쇄 및 웹</td>
  </tr>
  <tr>
   <td>X축 &gt; 데이터 모델 개체</td>
   <td><p>X축에 표시할 양식 데이터 모델 수집 항목의 이름입니다.</p> <p>차트의 X축과 Y축에서 플롯할 수 있는 동일한 상위 데이터 모델 개체의 모음/배열 유형 속성을 두 개 선택합니다. 바인딩하는 데이터 모델 개체는 Number, String 또는 Date 유형이어야 합니다.</p> </td>
   <td>인쇄 및 웹</td>
  </tr>
  <tr>
   <td>Y축 &gt; 제목</td>
   <td>Y축의 제목입니다. </td>
   <td>인쇄 및 웹</td>
  </tr>
  <tr>
   <td>Y축 &gt; 데이터 모델 개체</td>
   <td><p>Y축에 표시할 양식 데이터 모델 수집 항목입니다. 인쇄 채널에서 Y축에 대한 데이터 모델 개체는 숫자 유형이어야 합니다.</p> <p>차트의 X축과 Y축에서 플롯할 수 있는 동일한 상위 데이터 모델 개체의 모음/배열 유형 속성을 두 개 선택합니다. </p> </td>
   <td>인쇄 및 웹</td>
  </tr>
  <tr>
   <td>Y축 &gt; 함수</td>
   <td>y축에서 값을 계산하는 데 사용할 통계/사용자 지정 함수입니다.</td>
   <td>인쇄 및 웹</td>
  </tr>
  <tr>
   <td>개체 숨기기</td>
   <td>최종 출력에서 차트를 숨기려면 선택합니다.</td>
   <td>인쇄 및 웹</td>
  </tr>
  <tr>
   <td>제목</td>
   <td>차트의 제목입니다. </td>
   <td>인쇄</td>
  </tr>
  <tr>
   <td>높이</td>
   <td>차트의 픽셀 단위 높이입니다.</td>
   <td>인쇄</td>
  </tr>
  <tr>
   <td>너비</td>
   <td>차트의 픽셀 단위 폭입니다. 스타일 레이어를 사용하거나 테마를 적용하여 웹 채널에서 차트의 너비를 제어할 수 있습니다.</td>
   <td>인쇄</td>
  </tr>
  <tr>
   <td>이전 필수 페이지 나누기</td>
   <td>차트 앞에 필수 페이지 나누기를 추가하고 새 페이지의 맨 위에 차트를 배치하려면 선택합니다. </td>
   <td>인쇄</td>
  </tr>
  <tr>
   <td>다음 이후 필수 페이지 나누기</td>
   <td>차트 뒤에 필수 페이지 나누기를 추가하고 새 페이지 맨 위에 차트 다음에 있는 콘텐츠를 배치하려면 선택합니다. </td>
   <td>인쇄</td>
  </tr>
  <tr>
   <td>들여쓰기</td>
   <td>페이지 왼쪽의 차트 들여쓰기 </td>
   <td>인쇄</td>
  </tr>
  <tr>
   <td>툴팁</td>
   <td><p>웹 채널의 차트에 있는 데이터 포인트 위에 도구 설명이 표시되는 형식입니다. 기본값은 ${x}(${y})입니다. 차트 유형에 따라 차트의 점, 막대 또는 슬라이스에 마우스를 가리키면 ${x}및 ${y} 변수가 X축 및 Y축에 해당하는 값으로 동적으로 대체되고 도구 설명에 표시됩니다.</p> <p>도구 설명을 비활성화하려면 도구 설명 <span class="uicontrol">필드를</code> 비워 둡니다. 이 옵션은 라인 및 영역 차트에 적용되지 않습니다. 예를 들어 예제 <a href="../../forms/using/chart-component-interactive-communications.md#main-pars-header-e1f6">1을 참조하십시오.인쇄 및 웹에서</a>차트 출력</code></p> </td>
   <td>웹</td>
  </tr>
  <tr>
   <td>차트별 구성</td>
   <td><p>일반적인 구성 외에도 다음과 같은 차트별 구성을 사용할 수 있습니다.</p>
    <ul>
     <li><strong>범례 표시:활성화되면 파이 또는 도넛 차트에 대한 범례를 </strong>표시합니다.</li>
     <li><strong>범례 위치:차트에 </strong>대한 범례 위치를 지정합니다. 사용 가능한 옵션은 오른쪽, 왼쪽, 위쪽 및 아래입니다. 인쇄 채널에서 오른쪽 범례를 사용하는 것이 좋습니다.</li>
     <li><strong>내부 반경</strong>:도넛형 차트는 차트에 있는 내부 원의 반경(픽셀 단위)을 지정할 수 있습니다.</li>
     <li><strong>선 색상</strong>:라인, 선 및 점, 영역 차트에서 차트의 라인 색상을 지정할 수 있습니다.</li>
     <li><strong>포인트 색상</strong>:점 및 선 및 점 차트에서 차트의 점에 대한 색상을 지정할 수 있습니다.<br /> </li>
     <li><strong>영역 색상</strong>:영역 차트에서 차트의 라인 아래 영역에 대한 색상을 지정할 수 있습니다.</li>
     <li><strong>참조점 &gt; 바인딩 유형:Quadrant </strong>차트에서 참조 포인트에 대한<strong> 바인딩 유형을 </strong>지정할 수 있습니다. 정적 텍스트 또는 데이터 모델 개체 속성을 사용하여 참조점의 값을 정의합니다.</li>
     <li><strong>참조점 &gt; X축:바인딩 유형 드롭다운 </strong>목록에서 정적을 <span class="uicontrol">선택하여</code> 참조점에 대한X축 값을 지정하는 경우 Quadrant 차트에 사용할 수 있습니다.</code></li>
     <li><strong>참조점 &gt; Y축:바인딩 유형 드롭다운 </strong>목록에서 정적을 <span class="uicontrol">선택하여</code> 참조점에 대한Y축 값을 지정하는 경우 Quadrant 차트에 사용할 수 있습니다.</code></li>
     <li><strong>참조 점 &gt; 계열에 대한 데이터 모델 개체:바인딩 </strong>유형 드롭다운 목록에서 데이터 모델 <span class="uicontrol">객체를</code> 선택한 경우 여러 시리즈 Quadrant 차트에 사용할 수 있습니다. 참조 점에 대한 시리즈를 식별하는 양식 데이터 모델 개체 속성을 정의합니다. </code></li>
     <li><strong>참조 점 &gt; 계열에 대한 데이터 모델 개체 값:바인딩 </strong>유형 드롭다운 목록에서 데이터 모델 <span class="uicontrol">객체를</code> 선택한 경우 여러 시리즈 Quadrant 차트에 사용할 수 있습니다. 계열에 대한 양식 데이터 모델 개체 속성과 이 필드에 정의된 값을 사용하여 참조점에 대한 계열을 식별합니다.</code></li>
     <li><strong>참조점(Reference Point) &gt; 참조점에 대한 데이터 모델 개체(Data Model Object):바인딩 </strong>유형 드롭다운 목록에서 <span class="uicontrol">데이터 모델</code> 개체를 선택하는 경우 Quadrant 차트에 사용할 수 있습니다. X축 및 Y축에 표시된 속성의 동위 요소인 양식 데이터 모델 개체 속성을 정의합니다. 또한 여러 계열에 대해 해당 계열에 대해 정의된 데이터 모델 개체 속성의 자식 엔티티인 데이터 모델 개체 속성을 정의합니다.</code></li>
     <li><strong>참조점(Reference Point) &gt; 참조점의 데이터 모델 개체 값(Data Model Object Value):바인딩 </strong>유형 드롭다운 목록에서 <span class="uicontrol">데이터 모델</code> 개체를 선택하는 경우 Quadrant 차트에 사용할 수 있습니다. 참조점에 대한 양식 데이터 모델 객체 속성과 이 필드에 정의된 값을 사용하여 차트의 참조점을 식별합니다.<br /><strong> Quadrant </strong>레이블 &gt; 왼쪽 위:Quadrant 차트에서 왼쪽 상단 쿼드런트의 이름을 지정할 수 있습니다.</code></li>
     <li><strong></strong> Quadrant 레이블 &gt; 오른쪽 위:Quadrant 차트에서 Top Right Quadrant의 이름을 지정할 수 있습니다.</li>
     <li><strong>Quadrant 레이블 &gt; 오른쪽 아래:Quadrant </strong>차트에서 오른쪽 하단의 이름을 지정할 수 있습니다.</li>
     <li><strong>Quadrant 레이블 &gt; 왼쪽 아래:Quadrant </strong>차트에서 왼쪽 하단 사분면의 이름을 지정할 수 있습니다.</li>
    </ul> </td>
   <td>인쇄 및 웹</td>
  </tr>
 </tbody>
</table>

## 차트에 함수 사용 {#use-functions-in-chart}

통계적 함수를 사용하여 차트에 플로팅할 소스 데이터의 값을 계산하도록 차트를 구성할 수 있습니다. 차트에 함수를 적용하면 양식 데이터 모델에서 직접 제공하지 않는 데이터를 플롯할 수 있습니다.

![차트의 기능](assets/functions_charts_new.png)

차트 구성 요소에는 일부 내장 함수가 포함되어 있지만, [사용자 지정 함수를](../../forms/using/chart-component-interactive-communications.md#main-pars-header-473010287) 작성하여 웹 채널의 차트 구성에서 사용할 수 있도록 만들 수 있습니다.

차트 구성 요소에서는 기본적으로 다음 기능을 사용할 수 있습니다.

**평균(평균)** X축 또는 Y축에 있는 값의 평균을 다른 축에 반환합니다.

**합계** X축 또는 Y축에 있는 다른 축에 있는 주어진 값에 대한 모든 값의 합계를 반환합니다.

**최대값지정된** 값이 다른 축에 있는 X축 또는 Y축에서 최대값을 반환합니다.

**빈도다른** 축에 지정된 값에 대한 X축 또는 Y축에 있는 값의 수를 반환합니다.

**범위** X축이나 Y축에 있는 값의 최대값과 최소값 간의 차이를 다른 축에 반환합니다.

**중간값이** X축이나 Y축에서 더 높은 값과 낮은 값을 다른 축에 지정하는 값을 반환합니다.

**최소값은** X축이나 Y축에 있는 값의 최소값을 다른 축에 반환합니다.

**모드** X축이나 Y축에 나타나는 값이 다른 축에 있는 지정된 값으로 반환됩니다.

자세한 내용은 예제 [2:라인 차트에](../../forms/using/chart-component-interactive-communications.md#main-pars-header-ae38)합계 및 빈도 함수 적용

### 웹 채널의 사용자 정의 함수 {#customfunctionsweb}

차트에 기본 함수를 사용하는 것 외에도 JavaScript™에서 사용자 정의 함수를 작성하여 웹 채널에 대한 차트 구성 요소의 함수 목록에서 사용할 수 있도록 할 수 있습니다.

함수는 배열 또는 값과 범주 이름을 입력으로 가져와서 값을 반환합니다. 예:

```
Multiply(valueArray, category) {
 var val = 1;
 _.each(valueArray, function(value) {
 val = val * value;
 });
 return val;
}
```

사용자 지정 함수를 작성했으면 다음을 수행하여 차트 구성에서 사용할 수 있도록 합니다.

1. 관련 대화형 통신과 연결된 클라이언트 라이브러리에서 사용자 지정 함수를 추가합니다. 자세한 내용은 제출 [작업](/help/forms/using/configuring-submit-actions.md) 구성 및 클라이언트측 라이브러리 [사용을 참조하십시오](/help/sites-developing/clientlibs.md).

1. 함수 드롭다운에 사용자 지정 함수를 표시하려면 CRXDe Lite에서 다음 속성을 사용하여 앱 폴더에 `nt:unstructured` 노드를 만듭니다.

   * 값으로 속성을 `guideComponentType` 추가합니다 `fd/af/reducer`. (mandatory)

   * 사용자 지정 JavaScript™ 함수의 정규화된 이름에 속성을 `value` 추가합니다. (필수) 값을 곱하기 등의 사용자 지정 함수의 이름으로 설정합니다.
   * 함수 드롭다운에 표시되는 사용자 지정 함수의 이름으로 표시할 값과 `jcr:description` 함께 속성을 추가합니다. 예를 들어 곱하기를 **참조하십시오**.

   * 사용자 지정 함수에 대한 간단한 설명이 될 값이 있는 속성을 `qtip` 추가합니다. 함수 드롭다운 목록에서 함수 이름 위에 포인터를 두면 도구 **팁으로** 표시됩니다.

1. 모두 **저장을** 클릭하여 구성을 저장합니다.

이제 이 함수를 차트에서 사용할 수 있습니다.

## 예 1:인쇄 및 웹의 차트 출력 {#chartoutputprintweb}

기본 탭에서 차트 유형, 데이터가 들어 있는 소스 양식 데이터 모델 속성, 차트의 X축 및 Y축에 플로팅할 레이블, 차트에서 플로팅할 값을 계산하는 통계적 함수를 정의합니다(선택 사항).

대화형 통신을 사용하여 생성된 카드 문의 도움으로 기본 속성에 필요한 최소 정보를 자세히 알아보겠습니다. 명세서에서 서로 다른 비용의 양을 설명하는 차트를 생성하려는 경우를 고려하십시오. 인터랙티브 커뮤니케이션의 인쇄 및 웹 출력을 위해 다양한 유형의 차트를 사용하려고 합니다.

### 인쇄용 열 차트 {#columnchartprint}

이를 수행하려면 다음 속성을 지정합니다.

* **[!UICONTROL 이름]** - 차트의 이름을 지정합니다.
* **[!UICONTROL 차트]** 유형 - **드롭다운** 목록에서 열을 선택합니다.
* **[!UICONTROL 제목]** - X축에 대한 비용 유형 및 Y축에 대한 거래 금액을 지정합니다.
* **[!UICONTROL 데이터 모델 객체]** - 데이터 모델 객체 속성을 선택하여 X축(비용 유형) 및 Y축(트랜잭션 금액)에 대한 데이터 바인딩을 생성합니다.

![대화형 통신 인쇄 채널의 열 차트](assets/sample_chart_print_column_new.png)

대화형 통신 인쇄 채널의 열 차트

### 웹용 도넛 차트 {#donutchartweb}

이를 수행하려면 다음 속성을 지정합니다.

* **[!UICONTROL 이름]** - 차트의 이름을 지정합니다.
* **[!UICONTROL 차트]** 유형 - **[!UICONTROL 드롭다운]** 목록에서 도넛을 선택합니다.
* **[!UICONTROL 데이터 모델 객체]** - 데이터 모델 객체 속성을 선택하여 X축(비용 유형) 및 Y축(트랜잭션 금액)에 대한 데이터 바인딩을 생성합니다.
* **[!UICONTROL 내부 반경]** - 내부 반지름 값을 150으로 지정하여 차트에 있는 내부 원의 반경(픽셀 단위)을 지정합니다.
* **[!UICONTROL 도구 설명]** - ${x}(${y}) 기본 형식을 사용하여 도구 설명을 표시합니다. 도구 설명이 다음과 같이 표시됩니다.비용 유형(거래 금액). 예:비트코인 차변(10000).

![인터랙티브 커뮤니케이션의 웹 채널에 있는 도넛 차트](assets/sample_chart_web_new.png)

인터랙티브 커뮤니케이션의 웹 채널에 있는 도넛 차트

## 예 2:라인 차트의 합계 및 빈도 함수 적용 {#applicationsumfrequency}

차트에 함수를 적용하면 양식 데이터 모델에서 직접 제공하지 않는 데이터를 플롯할 수 있습니다. 이 예에서는 신용 카드 명세서 예를 사용하여 Sum 및 Frequency 함수를 차트에 적용할 수 있는 방법을 파악했습니다.

![두 개의 &quot;AirBnB&quot; 거래가 있는 기능이 없는 라인 차트](assets/line_chart_web_new.png)

두 개의 &quot;AirBnB&quot; 거래가 있는 기능이 없는 라인 차트

### Sum 함수 {#sum-function}

합계 함수를 적용하여 동일한 데이터 속성의 여러 인스턴스 값을 추가하고 한 번만 표시할 수 있습니다. 예를 들어 다음 그래프에서 합계 함수는 Y축에 적용하여 AirBnB 트랜잭션(2050 및 1050)에 대해 두 개의 차변 값을 추가하고 하나의 트랜잭션(3100)만 표시합니다.

Sum 함수는 동일한 데이터 속성의 여러 인스턴스에 대해 합계를 모으고 표시하려는 경우 그래프를 보다 유용하게 만들 수 있습니다.

![라인 차트 합계](assets/line_chart_web_sum_new.png)

### 주파수 함수 {#frequency-function}

주파수 함수는 다른 축에 있는 주어진 값에 대한 Y축 값의 수를 반환합니다. Y축(트랜잭션 금액)에 주파수 기능을 적용하면 AirBnB 트랜잭션에 대해 두 번 체크아웃이 발생했고 나머지 트랜잭션 유형도 한 번 발생했음을 그래프가 표시합니다.

![라인 차트 빈도](assets/line_chart_web_functions_frequency_new.png)

## 예 3:웹의 Multi-series Quadrant 차트 {#example-multi-series-quadrant-chart-in-web}

차트는 특정 날짜 범위에서 수행된 거래의 금액을 표시합니다. Quadrant 차트는 차트 영역을 4개의 레이블이 지정된 섹션으로 나눌 수 있는 기능을 제공합니다. 이 문자는 X축 및 Y축에 정적 참조점을 사용합니다. 여러 시리즈 기능을 사용하여 은행 이름에 따라 데이터를 구분합니다.

이를 수행하려면 다음 속성을 지정합니다.

* **** 이름:차트의 이름을 지정합니다.
* **** 차트 유형:드롭다운 **목록에서 Quadrant** 를 선택합니다.

* 복수 시리즈 **확인란을** 선택합니다.
* **데이터 모델 개체**:계열에 대한 데이터 모델 개체 속성을 지정합니다. 은행 이름에 대한 데이터 모델 개체 속성은 X축 및 Y축에 표시되는 데이터 모델 개체 속성의 상위 속성입니다.
* **** 데이터 모델 개체:데이터 모델 객체 속성을 선택하여 X축(트랜잭션 날짜) 및 Y축(트랜잭션 금액)에 대한 데이터 바인딩을 생성합니다.
* 참조점 **섹션에서** 바인딩 **유형으로** 정적을 선택합니다.

* X축 및 Y축 참조점의 값을 지정합니다.
* 왼쪽 상단, 오른쪽 상단, 오른쪽 하단 및 왼쪽 하단 사분기에 대한 사분면 레이블을 지정합니다.
* 은행 **이름에 대한 색상 코드를 표시하려면 범례** 표시 확인란을 선택합니다.

![Quadrant 차트](assets/charts_quadrant_example_new.png)

