---
title: 적응형 양식 표현식
seo-title: 적응형 양식 표현식
description: 적응형 양식 표현식을 사용하여 섹션의 자동 유효성 검사, 계산 및 가시성을 켜거나 끌 수 있습니다.
seo-description: 적응형 양식 표현식을 사용하여 섹션의 자동 유효성 검사, 계산 및 가시성을 켜거나 끌 수 있습니다.
uuid: c274dce5-8b87-472f-bff5-53b246fa6584
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 2fd2276e-cfe3-47ad-94c1-9c7af56b7a17
docset: aem65
translation-type: tm+mt
source-git-commit: 26a65772c43a5176d178bb6625604d18ac91e894
workflow-type: tm+mt
source-wordcount: '2767'
ht-degree: 0%

---


# 적응형 양식 표현식{#adaptive-form-expressions}

적응형 양식은 최종 사용자에게 동적 스크립팅 기능을 제공하는 최적화된 간소화된 양식 채우기 환경을 제공합니다. 표현식을 작성하여 동적 표시/숨기기 필드 및 패널과 같은 다양한 동작을 추가할 수 있습니다. 또한 계산된 필드를 추가하거나, 필드를 읽기 전용으로 만들고, 유효성 검사 논리를 추가하는 등 다양한 작업을 할 수 있습니다. 동적 동작은 사용자 입력 또는 자동 입력 데이터를 기반으로 합니다.

JavaScript는 적응형 양식의 표현식 언어입니다. 모든 표현식은 유효한 JavaScript 표현식이며 적응형 양식 스크립팅 모델 API를 사용합니다. 이러한 표현식은 특정 유형의 값을 반환합니다. 응용 양식 클래스, 이벤트, 개체 및 공용 API의 전체 목록은 응용 양식에 대한 [JavaScript 라이브러리 API 참조를 참조하십시오](https://helpx.adobe.com/experience-manager/6-5/forms/javascript-api/index.html).

## 표현식 작성 우수 사례 {#best-practices-for-writing-expressions}

* 표현식을 작성하는 동안 필드 및 패널에 액세스하려면 필드 또는 패널 이름을 사용할 수 있습니다. 필드의 값에 액세스하려면 값 속성을 사용하십시오. 예, `field1.value`
* 양식에서 필드 및 패널에 고유한 이름을 사용합니다. 표현식을 작성할 때 사용되는 필드 이름과 충돌하지 않도록 해줍니다.
* 여러 줄 표현식을 쓰는 동안 세미콜론을 사용하여 문을 종료합니다.

## 반복되는 패널을 포함하는 표현식에 대한 우수 사례 {#best-practices-for-expressions-involving-repeating-panel}

반복 패널은 스크립팅 API 또는 미리 채워진 데이터를 사용하여 동적으로 추가되거나 제거된 패널의 인스턴스입니다. 반복 패널 사용에 대한 자세한 내용은 반복 가능한 섹션이 있는 양식 [만들기를 참조하십시오](/help/forms/using/creating-forms-repeatable-sections.md).

* 반복되는 패널을 만들려면 패널 대화 상자에서 설정을 열고 최대 개수 필드 값을 1을 이상으로 설정합니다.
* 패널 반복 설정의 최소 카운트 값은 하나 이상 될 수 있지만 최대 카운트 값을 초과할 수 없습니다.
* 표현식이 반복 패널의 필드를 참조하면 표현식의 필드 이름이 가장 가까운 반복 요소로 결정됩니다.
* 적응형 양식은 합계, 카운트, 최소, 최대, 필터 등과 같은 반복적인 패널에 대한 계산을 간소화하는 몇 가지 특수 기능을 제공합니다. 전체 함수 목록은 적응형 양식에 대한 [JavaScript 라이브러리 API 참조를 참조하십시오.](https://helpx.adobe.com/aem-forms/6/javascript-api/af.html)
* 반복 패널의 인스턴스를 조작하기 위한 API는 다음과 같습니다.

   * 패널 인스턴스를 추가하려면: `panel1.instanceManager.addInstance()`
   * 패널 반복 색인을 가져오려면 다음을 수행하십시오. `panel1.instanceIndex`
   * 패널의 instanceManager를 가져오려면 다음을 수행하십시오. `_panel1 or panel1.instanceManager`
   * 패널의 인스턴스를 제거하려면: `_panel1.removeInstance(panel1.instanceIndex)`

## 표현식 유형 {#expression-types}

적응형 양식에서는 표현식을 작성하여 동적 표시/숨기기 필드 및 패널과 같은 동작을 추가할 수 있습니다. 표현식을 작성하여 계산된 필드를 추가하거나 읽기 전용, 유효성 검사 논리 등 다양한 작업을 수행할 수도 있습니다. 적응형 양식은 다음 표현식을 지원합니다.

* **[액세스 표현식](#access-expression-enablement-expression)**:을 클릭하여 필드를 활성화/비활성화합니다.
* **[표현식](#calculate-expression)**&#x200B;계산:을 클릭하여 필드의 값을 자동으로 계산합니다.
* **[표현식을 클릭합니다](#click-expression)**.를 클릭하여 단추의 클릭 이벤트에 대한 작업을 처리합니다.
* **[초기화 스크립트](#initialization-script):** 필드의 초기화 작업을 수행합니다.
* **[옵션 표현식](#options-expression)**:을 클릭하여 드롭다운 목록을 동적으로 채웁니다.
* **[요약 표현식](#summary)**:를 사용하여 아코디언 제목을 동적으로 계산합니다.
* **[표현식 유효성 검사](#validate-expression)**:to validate a field.
* **[값 커밋 스크립트](#value-commit-script):** 필드 값이 변경된 후에 양식의 구성 요소를 변경합니다.
* **[가시성 식](#visibility-expression)**:to control visibility of a field and panel.
* **[단계 완료 표현식](#step-completion-expression)**:사용자가 마법사의 다음 단계로 이동하지 않도록 하려면

### 액세스 표현식(활성 표현식) {#access-expression-enablement-expression}

액세스 표현식을 사용하여 필드를 활성화하거나 비활성화할 수 있습니다. 표현식에서 필드 값을 사용하는 경우 필드 값이 변경될 때마다 표현식이 트리거됩니다.

**적용 대상**:필드

**반환 유형**:표현식은 필드의 활성화 여부를 나타내는 부울 값을 반환합니다. **true** 는 필드가 활성화되어 있고 **false는 필드가 비활성화되었음을** 나타냅니다.

**예**:field1 **값이** X로 설정된 경우에만 필드를 **활성화하려면 액세스 표현식이**&#x200B;다음과 같습니다. `field1.value == "X"`

### 식 계산 {#calculate-expression}

계산 식은 식을 사용하여 필드의 값을 자동으로 계산하는 데 사용됩니다. 일반적으로 이러한 표현식은 다른 필드의 값 속성을 사용합니다. 예, `field2.value + field3.value`. 값 `field2`이 `field3`변경되면 표현식이 트리거되고 값이 다시 계산됩니다.

**적용 대상**:필드

**반환 유형**:표현식은 표현식 결과가 표시되는 필드(예: decimal)와 호환되는 값을 반환합니다.

**예**:field1 **에서 두 필드의 합계를 표시하는 계산** 표현식은 다음과 같습니다.
`field2.value + field3.value`

### 표현식 클릭 {#click-expression}

클릭 표현식은 단추의 클릭 이벤트에 대해 수행된 작업을 처리합니다. 기본적으로 GuideBridge는 API를 제공하여 클릭 표현식과 함께 사용되는 제출, 유효성 검사 등의 다양한 기능을 수행합니다. API의 전체 목록은 [GuideBridge API를 참조하십시오](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html).

**적용 대상**:단추 필드

**반환 유형**:클릭 표현식은 값을 반환하지 않습니다. 표현식이 값을 반환하는 경우 값이 무시됩니다.

**예**:단추의 클릭 동작에 **텍스트 상자** 를 값 **AEM Forms**&#x200B;로 채우려면 단추 클릭 표현식이 `textbox1.value="AEM Forms"`

### 초기화 스크립트 {#initialization-script}

응용 양식이 초기화되면 초기화 스크립트가 실행됩니다. 시나리오에 따라 초기화 스크립트는 다음과 같은 방식으로 동작합니다.

* 데이터 자동 완성 없이 응용 양식이 렌더링되면, 양식이 초기화되면 초기화 스크립트가 실행됩니다.
* 응용 양식이 데이터 자동 완성 상태로 렌더링되면 이 스크립트는 채우기 전 작업이 완료된 후에 실행됩니다.
* 응용 양식의 서버측 재유효성 검사가 트리거되면 초기화 스크립트가 실행됩니다.

**적용 대상:** 필드 및 패널

**반환 유형:** 초기화 스크립트 표현식이 값을 반환하지 않습니다. 표현식이 값을 반환하는 경우 값이 무시됩니다.

**예:** 데이터 사전 채우기 시나리오에서 값이 null로 저장될 `'Adaptive Forms'` 때 기본값으로 필드를 채우려면 초기화 스크립트 표현식은 다음과 같습니다.
`if(this.value==null) this.value='Adaptive Forms';`

### 옵션 표현식 {#options-expression}

옵션 표현식은 드롭다운 목록 필드의 옵션을 동적으로 채우는 데 사용됩니다.

**적용 대상**:드롭다운 목록 필드

**반환 유형**:옵션 표현식은 문자열 값의 배열을 반환합니다. 각 값은 **Male과**&#x200B;같은 간단한 문자열이거나 키=값 쌍 형식(예: **1=Male)일 수 있습니다.**

**예**:다른 필드의 값을 기반으로 필드의 값을 채우려면 간단한 옵션 표현식을 제공합니다. 예를 들어, 다른 필드에 **표시된 혼인**&#x200B;상태 **를** 기반으로 한 필드, 자녀수를 채우려면 다음과 같이 표현해야 합니다.

**`marital_status.value == "married" ? ["1=One", "2=two"] : ["0=Zero"]`.**

mobilly_status **** 필드의 값이 변경될 때마다 표현식이 다시 트리거됩니다. REST 서비스에서 드롭다운을 채울 수도 있습니다. 자세한 내용은 동적으로 드롭다운을 [채우기를 참조하십시오](../../forms/using/dynamically-populate-dropdowns.md).

### 요약 표현식 {#summary}

요약 표현식은 아코디언 레이아웃 패널의 하위 패널 제목을 동적으로 계산합니다. [요약] 표현식을 규칙에 지정하여 양식 필드 또는 사용자 지정 논리를 사용하여 제목을 평가할 수 있습니다. 이 식은 양식이 초기화될 때 실행됩니다. 양식을 프리플링하는 경우, 데이터는 프리플라이트 후 또는 표현식에 사용된 종속 필드의 값이 변경될 때 식이 실행됩니다.

요약 표현식은 일반적으로 각 하위 패널에 의미 있는 제목을 제공하기 위해 아코디언 레이아웃 패널의 하위 항목을 반복되는 데 사용됩니다.

**적용 대상:** 레이아웃이 아코디언(Accordion)으로 구성된 패널의 직접 하위 구성요소인 패널.

**반환 유형:** 표현식은 아코디언 제목이 되는 문자열을 반환합니다.

**예:** &quot;계정 번호:&quot;+ textbox1.value

### 표현식 유효성 검사 {#validate-expression}

유효성 검사 표현식은 주어진 식을 사용하여 필드의 유효성을 검사하는 데 사용됩니다. 일반적으로 이러한 표현식은 필드 값과 함께 정규 표현식을 사용하여 필드의 유효성을 확인합니다. 표현식은 다시 트리거되며 필드의 값이 변경되면 필드의 유효성 검사 상태가 다시 계산됩니다.

**적용 대상**:필드

**반환 유형**:표현식은 필드의 유효성 검사 상태를 나타내는 부울 값을 반환합니다. 값 **false** 는 필드가 잘못되었음을 나타내고 **true** 는 필드가 유효함을 나타냅니다.
**예**:영국의 포스트코드를 나타내는 필드의 경우 유효성 검사 표현식은 다음과 같습니다.

(**this.value** &amp;&amp; `this.value.match(/^(GIR 0AA|[A-Z]{1,2}\d[A-Z0-9]? ?[0-9][A-Z]{2}\s*)$/i) == null) ? false : true`

위의 예에서 비어 있지 않은 값이 패턴과 일치하지 않으면 표현식이 **false를** 반환하여 필드가 유효하지 않음을 나타냅니다.

>[!NOTE]
>
>필수가 아닌 필드 또는 필수 필드에 대한 유효성 검사 표현식을 작성할 경우 필드의 가시성 상태와 관계없이 표현식이 평가됩니다. 숨김 필드에 대한 유효성 검사를 중지하려면 초기화 또는 값 커밋 스크립트에서 validationsDisabled 속성을 true로 설정합니다. 예, `this.validationsDisabled=true`

### valueCommit 스크립트 {#value-commit-script}

값 커밋 스크립트는 다음과 같은 경우에 트리거됩니다.

* 사용자는 UI에서 필드 값을 변경합니다.
* 다른 필드의 변경으로 인해 필드 값이 프로그래밍 방식으로 변경됩니다.

**적용 대상:** 필드

**반환 유형:** 값 커밋 스크립트 식이 값을 반환하지 않습니다. 표현식이 값을 반환하는 경우 값이 무시됩니다.

**예:** 필드에 입력한 알파벳의 대/소문자를 커밋 시 대문자로 변환하려면 값 커밋 표현식은 다음과 같습니다.
`this.value=this.value.toUpperCase()`

>[!NOTE]
>
>필드의 값이 프로그래밍 방식으로 변경되면 값 커밋 스크립트의 실행을 비활성화할 수 있습니다. 이렇게 하려면 https://&#39;[server]:[port]&#39;/system/console/configMgr로 이동하고 **적응형 Forms 버전을 변경하여 호환성을** **** AEM Forms 6.1로 변경합니다. 이후, 값 커밋 스크립트는 사용자가 UI에서 필드 값을 변경할 때만 실행됩니다.

### 가시성 표현식 {#visibility-expression}

가시성 표현식은 필드/패널의 가시성을 제어하는 데 사용됩니다. 일반적으로 가시성 표현식은 필드의 값 속성을 사용하며 해당 값이 변경될 때마다 검색합니다.

**적용 대상**:필드 및 패널

**반환 유형**:표현식은 필드/패널이 표시되거나 표시되지 않음을 나타내는 부울 값을 반환합니다. **false** 는 필드나 패널이 보이지 않고 true는 필드나 패널이 표시되어 있음을 나타냅니다.

**예**:field1 **값이** Male으로 설정된 경우에만 표시되는 패널의 ****&#x200B;경우 가시성 표현식은 다음과 같습니다. `field1.value == "Male"`

### 단계 완료 표현식 {#step-completion-expression}

단계 완료 표현식은 사용자가 마법사 레이아웃의 다음 단계로 이동할 수 없도록 하는 데 사용됩니다. 이러한 표현식은 패널에 마법사 레이아웃(한 번에 한 단계를 보여주는 여러 단계 양식)이 있을 때 사용됩니다. 사용자는 현재 섹션의 필수 값이 모두 채워지고 유효한 경우에만 다음 단계, 패널 또는 하위 섹션으로 이동할 수 있습니다.

**적용 대상**:항목 레이아웃이 마법사로 설정된 패널.

**반환 유형**:표현식은 현재 패널이 유효한지 여부를 나타내는 부울 값을 반환합니다. **True** 는 현재 패널이 유효하며 사용자가 다음 패널로 이동할 수 있음을 나타냅니다.

**예**:다음 패널로 이동하기 전에 다양한 패널로 구성된 양식에서는 현재 패널의 유효성이 확인됩니다. 이 경우 단계 완료 표현식이 사용됩니다. 일반적으로 이러한 표현식은 GuideBridge 유효성 검사 API를 사용합니다. 단계 완료 표현식의 예는 다음과 같습니다.
`window.guideBridge.validate([],this.panel.navigationContext.currentItem.somExpression)`

## 응용 양식의 유효성 검사 {#validations-in-adaptive-form}

적응형 양식에 필드 유효성 검사를 추가하는 방법은 여러 가지가 있습니다. 필드에 유효성 검사가 추가된 경우 **True는** 필드에 입력한 값이 유효함을 나타냅니다. **False는** 값이 잘못되었음을 나타냅니다. 필드 안팎을 탭하면 오류 메시지가 생성되지 않습니다.

필드에 유효성 검사를 추가하는 방법은 다음과 같습니다.

### 필수 {#required}

구성 요소를 필수 구성 요소로 만들려면 구성 요소의 **편집** 대화 상자에서 **제목 및 텍스트 > 필수 옵션을 선택할 수 있습니다**. 적절한 **필수 메시지** (선택 사항)도 추가할 수 있습니다..

### 유효성 검사 패턴 {#validation-patterns}

한 필드에 사용할 수 있는 여러 가지 유효성 검사 패턴이 있습니다. 검증 패턴을 선택하려면 구성 요소의 **편집** 대화 상자에서 **패턴** 섹션을 찾아 **패턴을**&#x200B;선택합니다. 패턴(Pattern) 텍스트 상자에서 사용자 정의 유효성 검사 패턴을 직접 만들 **수** 있습니다. 채워진 데이터가 유효성 검사 패턴을 **준수하면** 유효성 검사 상태가 **True로** 반환되고 그렇지 않으면False가반환됩니다. 사용자 지정 유효성 검사 패턴을 작성하려면 HTML5 양식에 [대한 그림 절 지원을 참조하십시오](/help/forms/using/picture-clause-support.md).

### 유효성 검사 표현식 {#validation-expressions}

필드의 유효성 검사는 다른 필드에 있는 표현식을 사용하여 계산할 수도 있습니다. 이러한 표현식은 구성 요소의 **편집 대화 상자** 의 **스크립트** 탭 **의 유효성 검사 스크립트** 필드내에작성됩니다. 필드의 유효성 검사 상태는 표현식이 반환하는 값에 따라 달라집니다. 이러한 표현식을 쓰는 방법에 대한 자세한 내용은 표현식 유효성 [검사를 참조하십시오](../../forms/using/adaptive-form-expressions.md#p-validate-expression-p).

## 추가 정보 {#additional-information}

### 필드 표시 형식 사용 {#using-field-display-format}

표시 형식을 사용하여 데이터를 다른 형식으로 표시할 수 있습니다. 예를 들어 디스플레이 형식을 사용하여 하이픈, ZIP 코드 형식 지정 또는 날짜 선택기와 함께 전화 번호를 표시할 수 있습니다. 이러한 표시 패턴은 구성 요소의 편집 대화 **상자의 패턴** 섹션에서 선택할 수 있습니다. 위에 언급된 유효성 검사 패턴과 유사한 사용자 지정 표시 패턴을 작성할 수 있습니다.

### GuideBridge - API 및 이벤트 {#guidebridge-apis-and-events}

GuideBridge는 브라우저의 메모리 모델에서 적응형 양식과 상호 작용하는 데 사용할 수 있는 API 모음입니다. 안내서 Bridge API, 클래스 메서드, 노출된 이벤트에 대한 자세한 내용은 적응형 양식에 대한 [JavaScript 라이브러리 API 참조를 참조하십시오](https://helpx.adobe.com/aem-forms/6/javascript-api/).

>[!NOTE]
>
>표현식에서 GuideBridge 이벤트 리스너를 사용하지 않는 것이 좋습니다.

#### 다양한 표현식의 GuideBridge 사용 {#guidebridge-usage-in-various-expressions}

* 양식 필드를 재설정하려면 단추의 클릭 표현식에 `guideBridge.reset()` API를 트리거할 수 있습니다. 마찬가지로 클릭 표현식으로 호출할 수 있는 제출 API도 있습니다 `guideBridge.submit()`**.**

* API를 사용하여 다양한 필드 또는 패널 간에 포커스를 설정할 수 있습니다(패널 포커스는 자동으로 첫 번째 필드로 설정). `setFocus()` `setFocus()`패널 간 탐색, 이전/다음 탐색, 특정 필드로 초점 설정 등과 같이 탐색하는 다양한 옵션을 제공합니다. 예를 들어 다음 패널로 이동하려면 다음을 사용할 수 있습니다. `guideBridge.setFocus(this.panel.somExpression, 'nextItem').`

* 응용 양식 또는 특정 패널의 유효성을 확인하려면 `guideBridge.validate(errorList, somExpression).`

#### 표현식 외부 GuideBridge 사용  {#using-guidebridge-outside-expressions-nbsp}

표현식 외부에서 GuideBridge API를 사용할 수도 있습니다. 예를 들어 GuideBridge API를 사용하여 적응형 양식을 호스팅하는 페이지 HTML과 양식 모델 간의 통신을 설정할 수 있습니다. 또한 양식을 호스팅하는 Iframe의 부모에서 오는 값을 설정할 수 있습니다.

위에서 언급한 예제에 GuideBridge API를 사용하려면 GuideBridge의 인스턴스를 캡처하십시오. 인스턴스를 캡처하려면 `bridgeInitializeStart`객체 `window`이벤트 수신

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
>AEM에서는 clientLib에 코드를 작성하여 페이지에 포함하는 것이 좋습니다(페이지의 header.jsp 또는 footer.jsp).

양식을 초기화한 후(이벤트가 전달됨) GuideBridge를 사용하려면 `bridgeInitializeComplete` 를 사용하여 GuideBridge 인스턴스를 가져옵니다 `window.guideBridge`. API를 사용하여 GuideBridge 초기화 상태를 확인할 수 `guideBride.isConnected` 있습니다.

#### GuideBridge 이벤트 {#guidebridge-events}

GuideBridge는 호스팅 페이지의 외부 스크립트에 대한 특정 이벤트도 제공합니다. 외부 스크립트는 이러한 이벤트를 듣고 다양한 작업을 수행할 수 있습니다. 예를 들어 양식의 사용자 이름이 변경될 때마다 페이지 헤더에 표시되는 이름도 변경됩니다. 이러한 이벤트에 대한 자세한 내용은 적응형 양식에 [대한 JavaScript 라이브러리 API 참조를 참조하십시오](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html).

다음 코드를 사용하여 핸들러를 등록하십시오.

```javascript
guideBridge.on("elementValueChanged", function (event, data)  {

      // execute some logic when value of a field is changed

});
```

### 필드의 사용자 정의 패턴 만들기 {#creating-custom-patterns-for-a-field}

위에서 언급한 바와 같이 적응형 양식을 사용하면 작성자는 유효성 검사 또는 표시 형식에 대한 패턴을 제공할 수 있습니다. 즉시 사용 가능한 패턴 외에도 적응형 양식 구성 요소에 대해 재사용 가능한 사용자 지정 패턴을 정의할 수 있습니다. 예를 들어 텍스트 필드 또는 숫자 필드를 정의할 수 있습니다. 일단 정의되면, 지정된 유형의 구성 요소에 대해 모든 양식에서 이러한 패턴을 사용할 수 있습니다. 예를 들어, 텍스트 필드에 대한 사용자 정의 패턴을 만들어 응용 양식의 텍스트 필드에 사용할 수 있습니다. 구성 요소의 편집 대화 상자에서 패턴 섹션에 액세스하여 사용자 지정 패턴을 선택할 수 있습니다. 패턴 정의 또는 형식에 대한 자세한 내용은 [HTML5 양식에 대한 그림 절 지원을 참조하십시오](/help/forms/using/picture-clause-support.md).

다음 단계를 수행하여 특정 필드 유형에 대한 사용자 지정 패턴을 만들고 동일한 유형의 다른 필드에 재사용합니다.

1. 작성 인스턴스의 CRXDE Lite으로 이동합니다.
1. 사용자 지정 패턴을 유지할 폴더를 만듭니다. /apps 디렉토리에서 sling:folder 유형의 노드를 만듭니다. 예를 들어 이름이 있는 노드를 만듭니다 `customPatterns`. 이 노드 아래에서 다른 노드 `nt:unstructed` 를 만들고 이름을 지정합니다 `textboxpatterns`. 이 노드에는 추가할 다양한 사용자 지정 패턴이 포함되어 있습니다.
1. 생성된 노드의 속성 탭을 엽니다. 예를 들어 의 속성 탭을 엽니다 `textboxpatterns`. 이 노드에 `guideComponentType` 속성을 추가하고 해당 값을 fd/af/components/formatter/guideTextBox *로 설정합니다*.

1. 이 속성의 값은 패턴을 정의할 필드에 따라 달라집니다. 숫자 필드의 경우 `guideComponentType` 속성 값은 *fd/af/components/formatter/guideNumericBox입니다*. Datepicker 필드의 값은 *fd/af/components/formatter/guideDatepicker입니다*.&quot;
1. 노드에 속성을 지정하여 사용자 지정 패턴을 추가할 수 `textboxpatterns` 있습니다. 이름(예: `pattern1`)을 가진 속성을 추가하고 해당 값을 추가하려는 패턴으로 설정합니다. 예를 들어 Fax=text `pattern1` {99-999-9999999} 값이 있는 속성을 추가합니다. 이 패턴은 적응형 Forms에서 사용하는 모든 텍스트 상자에 사용할 수 있습니다.

   ![CrxDe에서 필드에 대한 사용자 정의 패턴 만들기](assets/creating-custom-patterns.png)

   사용자 정의 패턴 만들기

