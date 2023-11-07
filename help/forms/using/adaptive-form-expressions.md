---
title: 적응형 양식 표현식
seo-title: Adaptive Form Expressions
description: 적응형 양식 표현식을 사용하여 자동 유효성 검사, 계산을 추가하고 섹션의 가시성을 켜거나 끕니다.
seo-description: Use adaptive forms expressions to add automatic validation, calculation, and turn visibility of a section on or off.
uuid: c274dce5-8b87-472f-bff5-53b246fa6584
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 2fd2276e-cfe3-47ad-94c1-9c7af56b7a17
docset: aem65
feature: Adaptive Forms
exl-id: 048bd9e8-ef34-40fb-9f46-73743d7b47c8
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2802'
ht-degree: 2%

---

# 적응형 양식 표현식{#adaptive-form-expressions}

<span class="preview"> [새 적응형 양식 만들기](/help/forms/using/create-an-adaptive-form-core-components.md) 또는 [AEM Sites 페이지에 적응형 양식 추가](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) 작업을 할 때 현대적이고 확장 가능한 데이터 캡처 [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)를 사용하는 것이 좋습니다. 이러한 구성 요소는 적응형 양식 만들기 작업이 대폭 개선되어 우수한 사용자 경험을 보장할 수 있게 되었음을 나타냅니다. 이 문서에서는 기초 구성 요소를 사용하여 적응형 양식을 작성하는 이전 접근법에 대해 설명합니다. </span>

적응형 양식은 동적 스크립팅 기능을 갖춘 최종 사용자에게 최적화되고 간소화된 양식 작성 환경을 제공합니다. 동적 표시/숨기기 필드 및 패널과 같은 다양한 동작을 추가하는 표현식을 작성할 수 있습니다. 또한 계산된 필드를 추가하고, 필드를 읽기 전용으로 만들고, 유효성 검사 논리를 추가하는 등 다양한 작업을 수행할 수 있습니다. 동적 동작은 사용자 입력 또는 미리 채워진 데이터를 기반으로 합니다.

JavaScript는 적응형 양식의 표현식 언어입니다. 모든 표현식은 유효한 JavaScript 표현식이며 적응형 양식 스크립팅 모델 API를 사용합니다. 이 표현식은 특정 유형의 값을 반환합니다. 적응형 양식 클래스, 이벤트, 개체 및 공개 API의 전체 목록은 다음을 참조하십시오. [적응형 양식을 위한 JavaScript 라이브러리 API 참조](https://helpx.adobe.com/experience-manager/6-5/forms/javascript-api/index.html).

## 표현식 작성 모범 사례 {#best-practices-for-writing-expressions}

* 표현식을 작성하는 동안 필드 및 패널에 액세스하려면 필드 또는 패널의 이름을 사용할 수 있습니다. 필드의 값에 액세스하려면 value 속성을 사용합니다. 예, `field1.value`
* 양식에서 필드 및 패널에 고유한 이름을 사용하십시오. 표현식을 작성하는 동안 사용되는 필드 이름과의 충돌을 방지하는 데 도움이 됩니다.
* 여러 줄 식을 작성하는 동안 세미콜론을 사용하여 문을 종료합니다.

## 반복 패널을 포함하는 표현식에 대한 우수 사례 {#best-practices-for-expressions-involving-repeating-panel}

반복 패널은 스크립팅 API 또는 미리 채워진 데이터를 사용하여 동적으로 추가되거나 제거되는 패널의 인스턴스입니다. 반복 패널 사용에 대한 자세한 내용은 [반복 가능한 섹션이 있는 양식 만들기](/help/forms/using/creating-forms-repeatable-sections.md).

* 반복 패널을 만들려면 패널 대화 상자에서 설정을 열고 최대 개수 필드의 값을 1 이상으로 설정합니다.
* 패널 반복 설정의 최소 개수 값은 하나 이상일 수 있지만 최대 개수 값보다 클 수 없습니다.
* 표현식이 반복 패널의 필드를 참조하는 경우 표현식의 필드 이름은 가장 가까운 반복 요소로 확인됩니다.
* 적응형 양식은 sum, count, min, max, filter 등과 같은 반복 가능한 패널의 계산을 단순화하는 몇 가지 특수 기능을 제공합니다. 전체 함수 목록은 다음을 참조하십시오. [적응형 양식을 위한 JavaScript 라이브러리 API 참조](https://helpx.adobe.com/aem-forms/6/javascript-api/af.html)
* 반복 패널의 인스턴스를 조작하기 위한 API는 다음과 같습니다.

   * 패널 인스턴스를 추가하려면: `panel1.instanceManager.addInstance()`
   * 패널 반복 인덱스를 가져오려면 다음을 수행합니다. `panel1.instanceIndex`
   * 패널의 instanceManager를 가져오려면 다음을 수행합니다. `_panel1 or panel1.instanceManager`
   * 패널의 인스턴스를 제거하려면 다음 작업을 수행하십시오. `_panel1.removeInstance(panel1.instanceIndex)`

## 표현식 유형 {#expression-types}

적응형 양식에서는 표현식을 작성하여 동적 표시/숨기기 필드 및 패널과 같은 동작을 추가할 수 있습니다. 식을 작성하여 계산된 필드를 추가하고, 필드를 읽기 전용으로 만들고, 유효성 검사 논리 등을 더 많이 사용할 수도 있습니다. 적응형 양식은 다음 표현식을 지원합니다.

* **[표현식 액세스](#access-expression-enablement-expression)**: 필드를 활성화/비활성화합니다.
* **[표현식 계산](#calculate-expression)**: 필드의 값을 자동으로 계산합니다.
* **[표현식 클릭](#click-expression)**: 버튼의 클릭 이벤트에 대한 작업을 처리합니다.
* **[초기화 스크립트](#initialization-script):** 필드의 초기화에 대한 작업을 수행합니다.
* **[Options 표현식](#options-expression)**: 드롭다운 목록을 동적으로 채웁니다.
* **[요약 표현식](#summary)**: 아코디언의 제목을 동적으로 계산합니다.
* **[표현식 유효성 검사](#validate-expression)**: 필드의 유효성 검사.
* **[값 커밋 스크립트](#value-commit-script):** 필드 값이 변경된 후 양식의 구성 요소를 변경합니다.
* **[가시성 표현식](#visibility-expression)**: 필드 및 패널의 가시성을 제어합니다.
* **[단계 완료 표현식](#step-completion-expression)**: 사용자가 마법사의 다음 단계로 이동할 수 없도록 합니다.

### 액세스 표현식(지원 표현식) {#access-expression-enablement-expression}

액세스 표현식을 사용하여 필드를 활성화하거나 비활성화할 수 있습니다. 표현식에서 필드 값을 사용하는 경우 필드 값이 변경될 때마다 표현식이 다시 시도됩니다.

**적용 대상**: 필드

**반환 유형**: 표현식이 필드의 활성화 또는 비활성화 여부를 나타내는 부울 값을 반환합니다. **true** 필드가 활성화되었음을 나타냅니다. **false** 필드가 비활성화되었음을 나타냅니다.

**예**: 값이 인 경우에만 필드를 활성화합니다. **field1** 이(가) (으)로 설정됨 **X**, 액세스 표현식은 다음과 같습니다. `field1.value == "X"`

### 표현식 계산 {#calculate-expression}

계산 표현식은 표현식을 사용하여 필드의 값을 자동 계산하는 데 사용됩니다. 일반적으로 이러한 표현식은 다른 필드의 값 속성을 사용합니다. 예, `field2.value + field3.value`. 값 `field2`또는 `field3`를 변경하면 표현식이 다시 시도되고 값이 다시 계산됩니다.

**적용 대상**: 필드

**반환 유형**: 표현식이 표현식 결과가 표시되는 필드(예: 십진수)와 호환되는 값을 반환합니다.

**예**: 의 두 필드 합계를 표시하는 계산 표현식 **field1** 은(는)
`field2.value + field3.value`

### 표현식 클릭 {#click-expression}

클릭 표현식은 단추의 클릭 이벤트에 수행된 작업을 처리합니다. 기본적으로 GuideBridge는 클릭 표현식과 함께 사용되는 제출, 유효성 검사 등의 다양한 기능을 수행하기 위한 API를 제공합니다. API의 전체 목록은 다음을 참조하십시오. [GuideBridge API](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html).

**적용 대상**: 단추 필드

**반환 유형**: 클릭 표현식이 값을 반환하지 않습니다. 표현식이 값을 반환하면 값이 무시됩니다.

**예**: 텍스트 상자 채우기 **textbox1** 값을 가진 단추의 클릭 동작 **AEM Forms**, 버튼의 클릭 표현식은 입니다. `textbox1.value="AEM Forms"`

### 초기화 스크립트 {#initialization-script}

초기화 스크립트는 적응형 양식이 초기화되면 트리거됩니다. 시나리오에 따라 초기화 스크립트는 다음과 같은 방식으로 동작합니다.

* 적응형 양식이 데이터 미리 채우기 없이 렌더링되면 양식이 초기화된 후 초기화 스크립트가 실행됩니다.
* 적응형 양식이 데이터 미리 채우기로 렌더링되면 미리 채우기 작업이 완료된 후 스크립트가 실행됩니다.
* 적응형 양식의 서버측 유효성 재검사가 트리거되면 초기화 스크립트가 실행됩니다.

**적용 대상:** 필드 및 패널

**반환 유형:** 초기화 스크립트 표현식이 값을 반환하지 않습니다. 표현식이 값을 반환하면 값이 무시됩니다.

**예:** 데이터 미리 채우기 시나리오에서 필드를 기본값으로 채우기 `'Adaptive Forms'` 해당 값이 null로 저장되면 초기화 스크립트 표현식은 다음과 같습니다.
`if(this.value==null) this.value='Adaptive Forms';`

### 옵션 표현식 {#options-expression}

옵션 표현식은 드롭다운 목록 필드의 옵션을 동적으로 채우는 데 사용됩니다.

**적용 대상**: 드롭다운 목록 필드

**반환 유형**: 옵션 표현식은 문자열 값의 배열을 반환합니다. 각 값은 다음과 같은 간단한 문자열일 수 있습니다. **남성**&#x200B;또는 키=값 쌍 형식(예: ) **1=남성**

**예**: 다른 필드의 값을 기준으로 필드의 값을 채우려면 간단한 옵션 표현식을 제공합니다. 예를 들어 필드를 채우려면 **자녀 수**, 를 기반으로 함 **결혼 상태** 다른 필드에 표현되면 표현식은 다음과 같습니다.

**`marital_status.value == "married" ? ["1=One", "2=two"] : ["0=Zero"]`.**

다음 값 때마다: **marital_status** 필드가 변경되면 표현식이 다시 시도됩니다. REST 서비스에서 드롭다운을 채울 수도 있습니다. 자세한 내용은 [드롭다운을 동적으로 채우기](../../forms/using/dynamically-populate-dropdowns.md).

### 요약 표현식 {#summary}

요약 표현식은 아코디언 레이아웃 패널의 하위 패널 제목을 동적으로 계산합니다. 양식 필드 또는 사용자 지정 논리를 사용하여 제목을 평가하는 규칙에 요약 표현식을 지정할 수 있습니다. 이 식은 폼이 초기화될 때 실행됩니다. 양식을 미리 채우는 경우 데이터가 미리 채워진 후 또는 표현식에 사용된 종속 필드의 값이 변경될 때 표현식이 실행됩니다.

요약 표현식은 일반적으로 아코디언 레이아웃 패널의 하위 항목을 반복하여 각 하위 패널에 의미 있는 제목을 제공하는 데 사용됩니다.

**적용 대상:** 레이아웃이 아코디언으로 구성된 패널의 직접 하위 패널입니다.

**반환 유형:** 이 표현식은 아코디언의 제목이 되는 String을 반환합니다.

**예:** &quot;계정 번호: &quot; + textbox1.value

### 표현식 유효성 검사 {#validate-expression}

유효성 검사 표현식은 주어진 표현식을 사용하여 필드의 유효성을 검사하는 데 사용됩니다. 일반적으로 이러한 표현식은 필드 값과 함께 정규 표현식을 사용하여 필드의 유효성을 검사합니다. 표현식이 다시 시도되고 필드 값이 변경되면 필드의 유효성 검사 상태가 다시 계산됩니다.

**적용 대상**: 필드

**반환 유형**: 표현식이 필드의 유효성 검사 상태를 나타내는 부울 값을 반환합니다. 값 **false** 필드가 잘못되었음을 나타내고 **true** 는 필드가 유효함을 나타냅니다.
**예**: 영국의 우편 번호를 나타내는 필드의 경우 유효성 검사 표현식은 다음과 같습니다.

(**this.value** &amp;&amp; `this.value.match(/^(GIR 0AA|[A-Z]{1,2}\d[A-Z0-9]? ?[0-9][A-Z]{2}\s*)$/i) == null) ? false : true`

위의 예에서, 비어 있지 않은 값이 패턴과 일치하지 않으면 표현식이 를 반환합니다 **false** 필드가 유효하지 않음을 나타냅니다.

>[!NOTE]
>
>비필수 또는 필수 필드에 대한 검증 표현식을 작성하는 경우 해당 표현식은 필드의 가시성 상태와 관계없이 평가됩니다. 숨겨진 필드의 유효성 검사를 중지하려면 Initialization 또는 Value Commit Script에서 validationsDisabled 속성을 true로 설정합니다. 예, `this.validationsDisabled=true`

### valueCommit 스크립트 {#value-commit-script}

다음과 같은 경우 값 커밋 스크립트가 트리거됩니다.

* 사용자가 UI에서 필드의 값을 변경합니다.
* 다른 필드의 변경으로 인해 필드의 값이 프로그래밍 방식으로 변경됩니다.

**적용 대상:** 필드

**반환 유형:** 값 커밋 스크립트 표현식은 값을 반환하지 않습니다. 표현식이 값을 반환하면 값이 무시됩니다.

**예:** 커밋 시 필드에 입력한 알파벳의 대소문자를 대문자로 변환하려면 commit 표현식 값을 다음과 같이 설정합니다.
`this.value=this.value.toUpperCase()`

>[!NOTE]
>
>필드의 값이 프로그래밍 방식으로 변경되는 경우 값 커밋 스크립트 실행을 비활성화할 수 있습니다. 이렇게 하려면 https://&#39;으로 이동하십시오.[server]:[포트]&#39;/system/console/configMgr 및 변경 **호환성을 위한 적응형 Forms 버전** 끝 **AEM Forms 6.1**. 이후, 사용자가 UI에서 필드의 값을 변경할 때만 값 커밋 스크립트가 실행됩니다.

### 가시성 표현식 {#visibility-expression}

가시성 표현식은 필드/패널의 가시성을 제어하는 데 사용됩니다. 일반적으로 가시성 표현식은 필드의 값 속성을 사용하며 해당 값이 변경될 때마다 재시도됩니다.

**적용 대상**: 필드 및 패널

**반환 유형**: 필드/패널이 표시되는지 여부를 나타내는 부울 값을 표현식에서 반환합니다. **false** 는 필드 또는 패널이 표시되지 않음을 나타내고 true는 필드 또는 패널이 표시됨을 나타냅니다.

**예**: 값이 인 경우에만 표시되는 패널용 **field1** 이(가) (으)로 설정됨 **남성**, 가시성 표현식은 다음과 같습니다. `field1.value == "Male"`

### 단계 완료 표현식 {#step-completion-expression}

단계 완료 표현식은 사용자가 마법사 레이아웃의 다음 단계로 이동할 수 없도록 하는 데 사용됩니다. 이러한 표현식은 패널에 마법사 레이아웃(한 번에 한 단계씩 표시되는 여러 단계 양식)이 있는 경우 사용됩니다. 현재 섹션의 모든 필수 값이 채워지고 유효한 경우에만 다음 단계, 패널 또는 하위 섹션으로 이동할 수 있습니다.

**적용 대상**: 항목 레이아웃이 마법사로 설정된 패널입니다.

**반환 유형**: 표현식이 현재 패널이 적합한지 여부를 나타내는 부울 값을 반환합니다. **True** 는 현재 패널이 유효하고 사용자가 다음 패널로 이동할 수 있음을 나타냅니다.

**예**: 여러 패널로 구성된 양식에서 다음 패널로 이동하기 전에 현재 패널의 유효성이 검사됩니다. 이러한 경우 단계 완료 표현식이 사용됩니다. 일반적으로 이러한 표현식은 GuideBridge 유효성 검사 API를 사용합니다. 단계 완료 표현식의 예는 다음과 같습니다.
`window.guideBridge.validate([],this.panel.navigationContext.currentItem.somExpression)`

## 적응형 양식의 유효성 검사 {#validations-in-adaptive-form}

적응형 양식에 필드 유효성 검사를 추가하는 방법에는 여러 가지가 있습니다. 필드에 유효성 검사가 추가되면 **True** 필드에 입력한 값이 유효함을 나타냅니다. **False** 값이 잘못되었음을 나타냅니다. 필드 안팎을 탭하면 오류 메시지가 생성되지 않습니다.

필드에 유효성 검사를 추가하는 방법은 다음과 같습니다.

### 필수 {#required}

구성 요소를 필수 항목으로 만들려면 **편집** 구성 요소의 대화 상자에서 옵션을 선택할 수 있습니다 **제목 및 텍스트 > 필수**. 적절한 항목을 추가할 수도 있습니다 **필수 메시지** (선택 사항) 또한. .

### 유효성 검사 패턴 {#validation-patterns}

필드에 사용할 수 있는 기본 유효성 검사 패턴이 여러 개 있습니다. 검증 패턴을 선택하려면 **편집** 구성 요소의 대화 상자에서 **패턴** 섹션 및 선택 **패턴**. 에서 사용자 지정 유효성 검사 패턴을 만들 수 있습니다. **패턴** 텍스트 상자입니다. 유효성 검사 상태가 반환됩니다 **True** 채워진 데이터가 유효성 검사 패턴을 준수하는 경우에만 **False** 가 반환됩니다. 자신만의 사용자 지정 유효성 검사 패턴을 작성하려면 다음을 참조하십시오. [HTML5 양식에 대한 그림 절 지원](/help/forms/using/picture-clause-support.md).

### 유효성 검사 표현식 {#validation-expressions}

필드 유효성 검사는 다른 필드의 표현식을 사용하여 계산할 수도 있습니다. 이러한 표현식은 내부에 작성됩니다. **유효성 검사 스크립트** 필드 **스크립트** 탭 / **편집** 구성 요소 대화 상자 필드의 유효성 검사 상태는 표현식이 반환하는 값에 따라 다릅니다. 이러한 표현식을 작성하는 방법에 대한 내용은 [표현식 유효성 검사](../../forms/using/adaptive-form-expressions.md#p-validate-expression-p).

## 추가 정보 {#additional-information}

### 필드 표시 형식 사용 {#using-field-display-format}

표시 형식 을 사용하여 데이터를 다른 형식으로 표시할 수 있습니다. 예를 들어 표시 형식을 사용하여 하이픈, 우편번호 형식 또는 날짜 선택기가 있는 전화 번호를 표시할 수 있습니다. 이러한 표시 패턴은 다음에서 선택할 수 있습니다. **패턴** 구성 요소의 편집 대화 상자 섹션에 있는 섹션을 참조하십시오. 위에서 언급한 유효성 검사 패턴과 유사한 맞춤형 표시 패턴을 작성할 수 있습니다.

### GuideBridge - API 및 이벤트 {#guidebridge-apis-and-events}

GuideBridge는 브라우저의 메모리 모델에서 적응형 양식과 상호 작용하는 데 사용할 수 있는 API의 컬렉션입니다. Guide Bridge API, 클래스 메서드, 이벤트 노출에 대한 자세한 소개는 다음을 참조하십시오. [적응형 양식을 위한 JavaScript 라이브러리 API 참조](https://helpx.adobe.com/aem-forms/6/javascript-api/).

>[!NOTE]
>
>표현식에서 GuideBridge 이벤트 리스너를 사용하지 않는 것이 좋습니다.

#### 다양한 표현식의 GuideBridge 사용 {#guidebridge-usage-in-various-expressions}

* 양식 필드를 재설정하려면 다음을 트리거할 수 있습니다 `guideBridge.reset()` 버튼의 클릭 표현식에 대한 API입니다. 마찬가지로 클릭 표현식으로 호출할 수 있는 제출 API가 있습니다 `guideBridge.submit()`**.**

* 다음을 사용할 수 있습니다. `setFocus()` 다양한 필드 또는 패널에 포커스를 설정하기 위한 API 입니다(패널 포커스의 경우 첫 번째 필드로 자동 설정됨). `setFocus()`는 패널 간 탐색, 이전/다음 트래버스, 특정 필드에 대한 포커스 설정 등과 같은 다양한 탐색 옵션을 제공합니다. 예를 들어 다음 패널로 이동하려면 다음을 사용할 수 있습니다. `guideBridge.setFocus(this.panel.somExpression, 'nextItem').`

* 적응형 양식 또는 특정 패널의 유효성을 검사하려면 `guideBridge.validate(errorList, somExpression).`

#### 표현식 외부에서 GuideBridge 사용  {#using-guidebridge-outside-expressions-nbsp}

표현식 외부에서 GuideBridge API를 사용할 수도 있습니다. 예를 들어 GuideBridge API를 사용하여 적응형 양식을 호스팅하는 페이지 HTML과 양식 모델 간의 통신을 설정할 수 있습니다. 또한 양식을 호스팅하는 Iframe의 상위 항목에서 오는 값을 설정할 수 있습니다.

위의 예에서 GuideBridge API를 사용하려면 GuideBridge 인스턴스를 캡처합니다. 인스턴스를 캡처하려면 `bridgeInitializeStart`이벤트 `window`개체:

```javascript
window.addEventListener("bridgeInitializeStart", function(evnt) {

     // get hold of the guideBridge object

     var gb = evnt.detail.guideBridge;

     //wait for the completion of AF

     gb.connect(function (){

        //this function will be called after Adaptive Form is initialized

     })

})
```

>[!NOTE]
>
>AEM에서는 clientLib에 코드를 작성하여 페이지(페이지의 header.jsp 또는 footer.jsp)에 포함하는 것이 좋습니다

양식이 초기화된 후 GuideBridge를 사용하려면 `bridgeInitializeComplete` 이벤트가 발송됨), 다음을 사용하여 GuideBridge 인스턴스 가져오기 `window.guideBridge`. 다음을 사용하여 GuideBridge 초기화 상태를 확인할 수 있습니다 `guideBride.isConnected` API.

#### GuideBridge 이벤트 {#guidebridge-events}

GuideBridge는 또한 호스팅 페이지의 외부 스크립트에 대한 특정 이벤트를 제공합니다. 외부 스크립트는 이러한 이벤트를 수신하고 다양한 작업을 수행할 수 있습니다. 예를 들어 양식의 사용자 이름이 변경될 때마다 페이지 헤더에 표시된 이름도 변경됩니다. 이러한 이벤트에 대한 자세한 내용은 [적응형 양식을 위한 JavaScript 라이브러리 API 참조](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html).

다음 코드를 사용하여 처리기를 등록합니다.

```javascript
guideBridge.on("elementValueChanged", function (event, data)  {

      // execute some logic when value of a field is changed

});
```

### 필드에 대한 사용자 정의 패턴 만들기 {#creating-custom-patterns-for-a-field}

위에서 언급했듯이 적응형 양식을 사용하여 작성자는 유효성 검사 또는 디스플레이 형식에 대한 패턴을 제공할 수 있습니다. 즉시 사용 가능한 패턴을 사용할 수 있을 뿐만 아니라 적응형 양식 구성 요소에 대해 재사용 가능한 사용자 정의 패턴을 정의할 수 있습니다. 예를 들어 텍스트 필드나 숫자 필드를 정의할 수 있습니다. 정의된 후에는 모든 양식에서 지정된 유형의 구성 요소에 이러한 패턴을 사용할 수 있습니다. 예를 들어 텍스트 필드에 대한 사용자 정의 패턴을 만들어 적응형 양식의 텍스트 필드에 사용할 수 있습니다. 구성 요소의 편집 대화 상자에서 패턴 섹션에 액세스하여 사용자 정의 패턴을 선택할 수 있습니다. 패턴 정의 또는 형식에 대한 자세한 내용은 [HTML5 양식에 대한 그림 절 지원](/help/forms/using/picture-clause-support.md).

특정 필드 유형에 대한 사용자 정의 패턴을 만들고 동일한 유형의 다른 필드에 다시 사용하려면 다음 단계를 수행하십시오.

1. 작성 인스턴스의 CRXDE Lite으로 이동합니다.
1. 사용자 정의 패턴을 유지 관리할 폴더를 만듭니다. /apps 디렉터리 아래에 sling:folder 유형의 노드를 만듭니다. 예를 들어, 라는 이름의 노드를 만듭니다 `customPatterns`. 이 노드 아래에서 유형의 다른 노드를 만듭니다. `nt:unstructed` 이름을 지정합니다. `textboxpatterns`. 이 노드에는 추가하려는 다양한 사용자 정의 패턴이 포함되어 있습니다.
1. 작성된 노드의 속성 탭을 엽니다. 예를 들어 의 속성 탭을 엽니다. `textboxpatterns`. 추가 `guideComponentType` 속성을 이 노드로 설정하고 값을 로 설정합니다. *fd/af/components/formatter/guideTextBox*.

1. 이 속성의 값은 패턴을 정의하려는 필드에 따라 달라집니다. 숫자 필드의 경우 값 `guideComponentType` 속성은 입니다. *fd/af/components/formatter/guideNumericBox*. Datepicker 필드의 값은 *fd/af/components/formatter/guideDatepicker*. &quot;
1. 에 속성을 할당하여 사용자 지정 패턴을 추가할 수 있습니다. `textboxpatterns` 노드. 이름이 있는 속성 추가(예: `pattern1`)을 클릭하고 값을 추가하려는 패턴으로 설정합니다. 예를 들어 속성을 추가합니다 `pattern1` (값: 팩스=text{99-999-)9999999}. 패턴은 적응형 Forms에서 사용하는 모든 텍스트 상자에 사용할 수 있습니다.

   ![CrxDe의 필드에 대한 사용자 정의 패턴 만들기](assets/creating-custom-patterns.png)

   사용자 정의 패턴 만들기
