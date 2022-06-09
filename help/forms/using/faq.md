---
title: HTML5 양식에 대한 FAQ(자주 묻는 질문)
seo-title: Frequently asked questions (FAQ) for HTML5 forms
description: 레이아웃, 스크립팅 지원 및 HTML5 양식의 범위에 대한 FAQ(자주 묻는 질문)입니다.
seo-description: Frequently Asked Questions (FAQ) about layout, scripting support, and scope of HTML5 forms.
uuid: 398e31de-3e46-4288-b3cd-39d51fa17abc
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 4b676e7e-191f-4a19-8b8f-fc3e30244b59
docset: aem65
feature: Mobile Forms
exl-id: 85c9315e-1bc8-44a9-937e-af6fc7cf54d1
source-git-commit: 1e301f3991a18a594ac10a6548a0a645327dd4dd
workflow-type: tm+mt
source-wordcount: '1995'
ht-degree: 0%

---

# HTML5 양식에 대한 FAQ(자주 묻는 질문){#frequently-asked-questions-faq-for-html-forms}

레이아웃, 스크립팅 지원 및 HTML5 양식의 범위에 대한 FAQ(자주 묻는 질문)가 있습니다.

## 레이아웃 {#layout}

1. 내 양식에 바코드 및 서명 필드가 표시되지 않는 이유는 무엇입니까?

   답변: 바코드 및 서명 필드는 HTML 또는 모바일 시나리오에서 관련이 없습니다. 이러한 필드는 비대화형 영역으로 표시됩니다. 그러나 AEM Forms 디자이너는 서명 필드 대신 사용할 수 있는 새로운 서명 스크리블 필드를 제공합니다. 또한, [사용자 지정 위젯](../../forms/using/custom-widgets.md) 바코드를 생성하고 통합합니다.

1. XFA 텍스트 필드에 리치 텍스트가 지원됩니까?

   답변: AEM Forms Designer에서 리치 컨텐츠를 허용하는 XFA 필드는 지원되지 않으며 사용자 인터페이스의 텍스트 스타일을 지정하지 않고 일반 텍스트로 렌더링됩니다. 또한 comb 속성이 있는 XFA 필드는 빗자리 값에 따라 허용되는 문자 수에 제한이 있지만 일반 필드로 표시됩니다.

1. 반복 가능한 하위 양식 사용에 대한 제한이 있습니까?

   답변: 반복 가능한 하위 양식에는 초기 개수가 1 이상이어야 합니다. 초기 카운트가 0인 반복 가능한 하위 양식은 지원되지 않습니다. 반복 가능한 하위 폼을 사용하도록 선택하고 양식이 로드될 때 표시할 수 없습니다. 사용 사례를 달성하려면:

   1. 반복 가능한 하위 양식의 초기 개수를 1로 설정합니다.

      ![초기 카운트](assets/intial-count.png)

   1. 폼의 초기화 이벤트를 사용하여 하위 양식의 기본 인스턴스를 숨깁니다. 예를 들어 아래 코드는 양식 초기화에 있는 하위 양식의 기본 인스턴스를 숨깁니다. 또한 앱 유형을 확인하여 스크립트가 클라이언트 측에서만 실행되는지 확인합니다.

      ```javascript
      if ((xfa.host.appType == "HTML 5" || xfa.host.appType == "Exchange-Pro" || xfa.host.appType == "Reader")&&(_RepeatSubform.count == 1)&&(form1.Page1.Subform1.RepeatSubform.Key.rawValue == null)) {
      RepeatSubform.presence = "hidden";
      }
      ```

   1. 편집할 하위 양식의 인스턴스를 추가하는 스크립트를 엽니다. 하위 양식 스크립트의 인스턴스를 추가하려면 다음과 같은 코드를 추가하십시오.

      아래 코드는 하위 양식의 숨겨진 인스턴스를 확인합니다. 하위 양식의 숨겨진 인스턴스가 발견되면 하위 양식의 숨겨진 인스턴스를 삭제하고 하위 양식의 새 인스턴스를 삽입합니다. 하위 양식의 숨겨진 인스턴스를 찾을 수 없으면 하위 양식의 새 인스턴스를 삽입하면 됩니다.

      ```javascript
      if (RepeatSubform.presence == "hidden")
      {
      RepeatSubform.instanceManager.insertInstance(0);
      RepeatSubform.instanceManager.removeInstance(1);
      }
      else
      {
      RepeatSubform.instanceManager.addInstance(1);
      }
      ```

   1. 편집할 하위 양식의 인스턴스를 제거하는 스크립트를 엽니다. 다음과 같은 코드를 추가하여 하위 양식 스크립트의 인스턴스를 제거합니다.

      이 코드는 하위 양식의 수를 확인합니다. 하위 양식의 개수가 1에 도달하면 하위 폼을 삭제하는 대신 해당 하위 폼을 숨깁니다.

      ```javascript
      if (RepeatSubform.instanceManager.count == 1) {
      RepeatSubform.presence = "hidden";
      } else {
      RepeatSubform.instanceManager.removeInstance(RepeatSubform.instanceManager.count - 1);
      }
      ```

   1. 편집할 양식의 사전 제출 이벤트를 엽니다. 편집하기 전에 다음 스크립트를 이벤트에 추가하여 스크립트의 숨겨진 인스턴스를 제거합니다. 제출 시 숨겨진 하위 양식의 데이터를 보낼 수 없습니다.

      ```javascript
      if(RepeatSubform.instanceManager.count == 1 && RepeatSubform.presence == "hidden") {
      RepeatSubform.instanceManager.removeInstance(0);
      }
      ```

1. 숨겨진 하위 양식 사용에 제한이 있습니까?

   답변: 여러 페이지로 분할되는 복잡한 계층 구조를 가진 숨겨진 하위 폼으로 인해 레이아웃 문제가 발생합니다. 해결 방법은 처음에 표시되는 하위 양식을 표시한 다음 일부 논리 또는 데이터를 기반으로 초기화 스크립트에서 해당 하위 양식을 숨기는 것입니다.

1. 일부 텍스트가 잘리거나 HTML5에 잘못 표시되는 이유는 무엇입니까?

   답변: 그리기 또는 캡션 텍스트 요소에 컨텐츠를 표시할 충분한 공간이 없으면 모바일 양식 변환에서 텍스트가 잘림으로 표시됩니다. 이렇게 잘리게 되면 AEM Forms 디자이너의 디자인 보기에서도 표시됩니다. 이러한 잘림은 PDF에서 처리할 수 있지만 HTML5 양식에서 처리할 수 없습니다. 이 문제를 방지하려면 AEM Forms 디자이너의 디자인 모드에서 잘리지 않도록 그리기 또는 캡션 텍스트에 충분한 공간을 제공하십시오.

1. 콘텐츠 누락 또는 콘텐츠 중복 관련 레이아웃 문제가 관찰되었습니다. 이유는 무엇입니까?

   답변: 텍스트 그리기 또는 이미지 그리기 요소와 같은 위치(사각형)에 겹치는 다른 요소가 있는 경우 텍스트 그리기 컨텐츠는 나중에 문서 순서(AEM Forms Designer 계층 보기)로 오면 표시되지 않습니다. PDF은 투명한 레이아웃을 지원하지만 HTML/브라우저는 투명한 레이아웃을 지원하지 않습니다.

1. 일부 글꼴이 양식을 디자인하는 동안 HTML 양식에 표시되는 글꼴과 다른 이유는 무엇입니까?

   답변: HTML5 양식은 글꼴을 포함하지 않습니다(양식 내에 글꼴이 포함된 PDF forms과 대조적으로). 양식의 HTML 버전이 예상대로 렌더링되도록 하려면 XDP에 지정된 글꼴이 서버 및 클라이언트 컴퓨터에서 사용할 수 있는지 확인하십시오. 필요한 글꼴을 서버에서 사용할 수 없으면 폴백 글꼴이 사용됩니다. 또한 클라이언트 장치에서 사용할 수 없는 양식 서식 파일에서 글꼴을 사용하는 경우 브라우저의 기본 글꼴이 텍스트를 렌더링하는 데 사용됩니다.

1. HTML 양식에서 vAlign 및 hAlign 특성이 지원됩니까?

   예. vAlign 및 hAlign 속성이 지원됩니다. vAlign 속성은 Internet Explorer 및 여러 줄 필드에서 지원되지 않습니다.

1. HTML5 양식이 히브리어 문자를 지원합니까?

   HTML5 양식은 Microsoft Internet Explorer를 제외한 모든 브라우저에서 히브리어 문자를 지원합니다.

1. HTML5 양식에 숫자 필드에 제한이 있습니까?

   답변: 예. HTML5 양식에는 몇 가지 제한 사항이 있습니다. 자릿수가 그림 절에 지정된 수보다 많으면 해당 숫자는 현지화되지 않고 영어 로케일에 표시됩니다.

1. HTML 양식의 크기가 PDF forms보다 큰 이유는 무엇입니까?

   XDP를 HTML 양식으로 렌더링하려면 양식 dom, 데이터 dom 및 레이아웃 dom과 같은 많은 중간 데이터 구조와 개체가 필요합니다.

   PDF forms의 경우 Adobe Acrobat에는 중간 데이터 구조 및 개체를 만들기 위한 XTG 엔진이 내장되어 있습니다. Acrobat에서는 레이아웃과 스크립트도 처리합니다.

   HTML5 양식의 경우 브라우저에는 중간 데이터 구조 및 원시 XDP 바이트의 개체를 만드는 기본 제공 XTG 엔진이 없습니다. 따라서 HTML5 양식의 경우 중간 구조가 서버에서 생성되어 클라이언트로 전송됩니다. 클라이언트에서 JavaScript 기반 스크립트 및 레이아웃 엔진은 이러한 중간 구조를 사용합니다.

   중간 구조의 크기는 원래 XDP의 크기와 XDP와 병합된 데이터에 따라 다릅니다.

1. xdp에서 표 사용에 대한 제한 사항이 있습니까?

   답변: 복잡한 표로 인해 렌더링에 문제가 발생합니다.

   * 표 내의 섹션(SubformSet)은 지원되지 않습니다.
   * 일부 테이블의 머리글 또는 바닥글 행은 반복으로 표시됩니다. 여러 페이지에서 이러한 테이블을 분할하면 몇 가지 문제가 발생할 수 있습니다.

1. 액세스 가능한 테이블에 제한 사항이 있습니까?

   답변: 예. 액세스 가능한 테이블에는 다음과 같은 제한 사항이 있습니다.

   * 표 내의 중첩된 표와 하위 폼은 지원되지 않습니다.
   * 머리글은 표의 맨 위 행 또는 왼쪽 열에 대해서만 지원됩니다. 중간 테이블 요소에 대해서는 헤더가 지원되지 않습니다. 테이블의 맨 위 행 또는 맨 왼쪽 열과 함께 모든 행 및 열이 있는 경우 여러 행에 헤더를 적용할 수 있고 열 헤더가 지원됩니다.
   * `Rowspan`및 `colspan`표 내의 임의 위치에서는 지원되지 않습니다.

   * 행 범위 값이 1보다 큰 요소를 포함하는 행의 인스턴스를 동적으로 추가하거나 제거할 수 없습니다.

1. 화면 판독기에 대한 도구 팁과 캡션의 읽기 순서는 무엇입니까?

   * 캡션과 도구 설명이 모두 있으면 캡션만 읽습니다. 캡션을 사용할 수 없으면 도구 설명이 표시됩니다. 양식 디자이너를 사용하여 XDP에서 읽는 우선 순위를 지정할 수도 있습니다
   * 요소를 마우스로 가리키면 도구 설명이 표시됩니다. 도구 설명을 사용할 수 없는 경우 음성 텍스트가 표시됩니다. 음성 텍스트를 사용할 수 없으면 필드 이름이 표시됩니다.

1. 필드를 마우스로 가리키면 도구 설명이 표시됩니다. 비활성화하는 방법

   마우스로 가리키면 도구 설명을 비활성화하려면 디자이너의 액세스 가능성 패널에서 없음 을 선택합니다.

1. 디자이너는 라디오 단추와 확인란에 대한 사용자 지정 모양 속성을 구성할 수 있습니다. 양식을 렌더링하는 동안 HTML5 양식에서 이러한 사용자 지정 모양 속성을 고려합니까?

   답변: HTML5 forms에서는 라디오 단추와 확인란의 사용자 지정 모양 속성을 무시합니다. 라디오 단추 및 확인란은 기본 브라우저의 사양에 따라 표시됩니다.

1. 지원되는 브라우저에서 HTML5 Form을 열면 인접하는 필드의 테두리가 올바르게 정렬되지 않거나 하위 양식이 겹쳐서 표시됩니다. Forms Designer에서 동일한 HTML5 양식을 미리 볼 때 필드 및 레이아웃이 잘못 정렬되지 않고 하위 양식이 올바른 위치에 표시됩니다. 문제를 해결하는 방법

   하위 폼을 콘텐츠 흐름으로 설정하고 하위 폼에 숨겨진 테두리 요소가 있는 경우 인접하는 필드의 테두리가 올바르게 정렬되지 않거나 하위 폼이 겹쳐서 표시됩니다. 이 문제를 해결하려면 숨겨진 내용을 제거하거나 주석을 달 수 있습니다 &lt;border> 해당 XDP의 요소. 예를 들어, 다음 &lt;border> 요소는 주석으로 표시됩니다.

   ```xml
               <!--<border>
                  <edge presence="hidden"/>
                  <corner thickness="0.175mm" presence="hidden"/>
               </border> -->
   ```

1. 날짜/시간 필드 개체에서 화면 판독기가 제대로 작동하지 않는 이유는 무엇입니까?

   화면 판독기는 날짜/시간 필드를 지원하지 않습니다. 그러나 필드에 날짜/시간을 수동으로 입력하여 화면 판독기에서 읽을 수 있도록 할 수 있습니다. 도구 설명 또는 화면 판독기 텍스트를 사용하여 사용자가 필드의 날짜/시간을 수동으로 선택하도록 지시합니다.

1. HTML5 양식은 부동 필드에 대한 표시 패턴을 지원합니까?

   답변: HTML5 양식은 부동 필드에 대한 표시 패턴을 지원하지 않습니다.

1. HTML5 Forms의 날짜 필드 형식은 무엇입니까?

답변: 날짜 필드는 YYYY-MM-DD ISO 형식을 허용합니다. 날짜를 다른 형식으로 지정하는 경우 사용자가 필드를 나올 때까지 날짜 필드에 형식이 적용되지 않습니다.

### 스크립팅 {#scripting}

1. Forms HTML에 대한 JavaScript 구현에 제한이 있습니까?

   답변:

   * xfa.connectionSet 스크립트에 대한 지원이 제한됩니다. connectionSet의 경우 웹 서비스의 서버측 호출만 지원됩니다. 자세한 내용은 [스크립팅 지원](/help/forms/using/scripting-support.md).
   * 클라이언트 측 스크립트에는 $record 및 $data에 대한 지원이 없습니다. 그러나 스크립트가 formReady, layoutReady 블록으로 작성된 경우 이러한 이벤트가 서버 측에서 실행되므로 스크립트는 계속 작동합니다.
   * 그리기 텍스트 변경 등의 XFA 그리기 요소별 스크립트(또는 필드의 경우 캡션 텍스트)는 지원되지 않습니다.

1. formCalc 사용에 제한이 있습니까?

   답변: formCalc 스크립트의 하위 집합만 현재 구현됩니다. 자세한 내용은 [스크립팅 지원](/help/forms/using/scripting-support.md).

1. 권장 이름 지정 규칙이 있으며, 피할 예약된 키워드가 있습니까?

   * AEM Forms 디자이너에서 밑줄(_). 이름 시작 부분에 밑줄을 사용하려면 밑줄 뒤에 접두사를 추가합니다._&lt;prefix>&lt;objectname>.
   * 모든 HTML5 양식 API는 예약된 키워드입니다. 사용자 지정 API/함수의 경우 와 동일하지 않은 이름을 사용하십시오 [HTML5 양식 API](/help/forms/using/scripting-support.md).

1. HTML5 양식이 부동 필드를 지원합니까?

   예. HTML5 Forms은 부동 필드를 지원합니다. 부동 필드를 활성화하려면 렌더링 프로필에 다음 속성을 추가하십시오.

   >[!NOTE]
   >
   >기본적으로 이 필드는 플로팅에 사용할 수 없습니다. Forms 디자이너를 사용하여 필드의 부동 속성을 설정할 수 있습니다.

   1. CRXde Lite를 열고 `/content/xfaforms/profiles/default` 노드 아래에 있어야 합니다.
   1. 속성 추가 `mfDataDependentFloatingField`String 형식으로 설정하고 속성 값을 로 설정합니다. `true`.
   1. 클릭 **모두 저장**. 이제 업데이트된 렌더링 프로필을 사용하여 HTML Forms에 대해 부동 필드를 사용할 수 있습니다.

      >[!NOTE]
      >
      >렌더링 프로필을 업데이트하지 않고 특정 양식에 대해 부동 필드를 활성화하려면 mfDataDependentFloatingField=true 속성을 URL 매개 변수로 전달합니다.

1. HTML5 양식은 초기화 스크립트 및 양식 준비 이벤트를 여러 번 실행합니까?

   예. 초기화 스크립트 및 양식 준비 이벤트는 서버에서 한 번 이상, 클라이언트측에서 한 번 이상 여러 번 실행됩니다. 초기화 또는 양식:준비 이벤트와 같은 스크립트를 작성하여 데이터 및 idempotent(데이터가 동일한 경우)의 상태에 따라 작업이 수행되도록 일부 비즈니스 논리(양식 또는 필드 데이터)를 기반으로 하는 이벤트 순서를 지정하는 것이 좋습니다.

### XDP 디자인 {#designing-xdp}

1. HTML5 양식에 예약된 키워드가 있습니까?

   답변: 모든 HTML5 양식 API는 예약된 키워드입니다. 사용자 지정 API/함수의 경우 와 동일하지 않은 이름을 사용하십시오 [HTML5 양식 API](/help/forms/using/scripting-support.md). 예약된 키워드 외에도 밑줄(_)로 시작하는 개체 이름을 사용하는 경우 밑줄 뒤에 고유한 접두어를 추가하는 것이 좋습니다. 접두사를 추가하면 HTML5 forms 내부 API와 충돌하지 않는 데 도움이 됩니다. 예, `_fpField1`
