---
title: 인라인 조건 및 인터랙티브 통신 및 문자에서 반복
seo-title: 인라인 조건 및 인터랙티브 통신 및 문자에서 반복
description: 인라인 조건을 사용하고 인터랙티브한 커뮤니케이션과 편지에서 반복하면 상황에 맞는 구조화된 커뮤니케이션을 만들 수 있습니다.
seo-description: 인라인 조건을 사용하고 인터랙티브한 커뮤니케이션과 편지에서 반복하면 상황에 맞는 구조화된 커뮤니케이션을 만들 수 있습니다.
uuid: 32b48a8b-431d-4f9c-9f51-8e7e9ac624a0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4
topic-tags: interactive-communications, correspondence-management
discoiquuid: bbaba39b-e15a-4143-b6fc-7789fa2917b4
docset: aem65
feature: 서신 관리
exl-id: bc5d6c5b-c833-4849-aace-e07f8a522b32
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1696'
ht-degree: 0%

---

# 인라인 조건 및 대화형 통신 및 문자{#inline-condition-and-repeat-in-interactive-communications-and-letters}에서 반복

## 인라인 조건 {#inline-conditions}

AEM Forms을 사용하면 텍스트 모듈에서 인라인 조건을 사용하여 양식 데이터 모델(Interactive Communication에서) 또는 데이터 사전(편지로)과 연관된 컨텍스트 또는 데이터에 따라 달라지는 텍스트 렌더링을 자동화할 수 있습니다. 인라인 조건은 true 또는 false인 조건 평가를 기반으로 특정 콘텐츠를 표시합니다.

조건은 양식 데이터 모델/데이터 사전 또는 최종 사용자가 제공하는 데이터 값에 대한 계산을 수행합니다. 인라인 조건을 사용하면 시간을 절약하고 실수를 줄일 수 있을 뿐만 아니라 상황에 맞는 개인화된 인터랙티브 통신/문자를 만들 수 있습니다.

자세한 내용은 다음을 참조하십시오.

* [대화형 통신 만들기](../../forms/using/create-interactive-communication.md)
* [서신 관리 개요](/help/forms/using/cm-overview.md)
* [대화형 커뮤니케이션의 텍스트](../../forms/using/texts-interactive-communications.md)

### 예:규칙을 사용하여 대화형 통신 {#example-using-rules-to-conditionalize-inline-text-in-interactive-communication}에서 인라인 텍스트 조건부 구현

Interactive Communication에서 문장, 단락 또는 텍스트 문자열을 조건부 구현하기 위해 적절한 텍스트 문서 조각에서 규칙을 생성할 수 있습니다. 다음 예제에서는 규칙을 사용하여 Interactive Communication의 미국 수신자에게만 무료 전화 번호를 표시합니다.

자세한 내용은 [대화형 커뮤니케이션의 텍스트 ](../../forms/using/texts-interactive-communications.md)에서 텍스트로 규칙 만들기 를 참조하십시오.

Interactive Communication에 텍스트 조각을 포함시키고 Agent UI를 사용하여 대화형 커뮤니케이션을 준비하면 수신자에 대한 (양식 데이터 모델) 데이터가 평가되고 텍스트는 미국의 수신자에게만 표시됩니다.

### 예:편지에 인라인 조건을 사용하여 적절한 주소 {#example-using-inline-condition-in-a-letter-to-render-the-appropriate-address} 렌더링

인라인 조건을 해당 텍스트 모듈에 삽입하여 편지에 삽입할 수 있습니다. 다음 예제에서는 두 가지 조건을 사용하여 DD 요소 Gender를 기반으로 한 편지에서 해당 주소인 Sir 또는 Ma&#39;am을 평가하고 표시합니다. 유사한 단계를 사용하여 다른 조건을 만들 수 있습니다.

>[!NOTE]
>
>기존 자산에 이전 조건/반복 표현식(6.2 SP1 CFP 4 이전)이 포함되어 있으면, 자산에는 이전 조건 구문이 표시되고 반복이 표시됩니다. 그러나 이전 조건/반복은 작동합니다. 새 표현식과 이전 조건/반복 표현식은 이전 표현식과 새 조건/반복 표현식의 중첩된 혼합을 만들기 위해 서로 호환됩니다.

1. 관련 텍스트 모듈에서 조건을 지정할 텍스트 부분을 선택하고 **Condition**&#x200B;을 누릅니다.

   ![1_selecttext](assets/1_selecttext.png)

   조건 대화 상자가 빈 조건과 함께 나타납니다.

   ![2_conditiondialog](assets/2_conditiondialog.png)

   >[!NOTE]
   >
   >비어 있거나 잘못된 조건부 식을 저장할 수 없습니다. 표현식을 저장하려면 `${}` 내에 유효한 조건식이 있어야 합니다.

1. 선택한/조건부 텍스트가 편지에 나타나는지 여부를 평가하는 조건을 구성하려면 다음을 수행한 다음 확인 표시를 눌러 표현식을 저장합니다.

   DD 요소를 두 번 탭하여 조건에 삽입합니다. 적절한 연산자를 삽입하고 대화 상자에 다음 조건을 구성합니다.

   ```javascript
   ${DD_creditcard_Gender=="Male"}
   ```

   표현식 만들기에 대한 자세한 내용은 [표현식 빌더](../../forms/using/expression-builder.md)에서 **표현식 빌더**&#x200B;을 사용하여 표현식 및 원격 함수 만들기 를 참조하십시오. 데이터 사전의 요소에 대해 표현식에 지정된 값이 지원되어야 합니다. 자세한 내용은 [데이터 사전](../../forms/using/data-dictionary.md)을 참조하십시오.

   조건이 삽입되면 조건 왼쪽의 핸들을 마우스로 가리키면 조건을 볼 수 있습니다. 핸들을 탭하여 조건의 팝업 메뉴를 볼 수 있습니다. 이 경우 조건을 편집하거나 제거할 수 있습니다.

   ![3_hoverhandle](assets/3_hoverhandle.png) ![4_editconditionremoveonditionpopup](assets/4_editconditionremoveconditionpopup.png)

1. `Ma'am` 텍스트를 선택하여 유사한 조건을 삽입합니다.

   ```javascript
   ${DD_creditcard_Gender == "Female"}
   ```

1. 관련 편지를 미리 보고 텍스트가 인라인 조건에 따라 렌더링된다는 것을 확인합니다. 다음을 사용하여 DD 요소 성별 값을 입력할 수 있습니다.

   * 샘플 데이터가 있는 문자를 미리 보는 동안 관련 데이터 사전을 기반으로 만들어진 샘플 XML 데이터 파일입니다.
   * 관련 데이터 사전에 첨부된 XML 데이터 파일입니다.

   자세한 내용은 [데이터 사전](../../forms/using/data-dictionary.md)을 참조하십시오.

   ![5_letteroutput](assets/5_letteroutput.png)

## 반복 {#repeat}

Interactive Communication/letter에 동적 정보가 있을 수 있습니다. 예를 들어, 인스턴스나 항목이 생성된 각 문자로 계속 변경될 수 있습니다. 반복을 사용하여 텍스트 문서 조각에서 이러한 동적 정보의 형식을 지정하고 구조를 구성할 수 있습니다.

또한 반복 구성 내에 규칙/조건을 지정하여 대화형 통신/편지에 렌더링되는 정보/항목을 조건부 구현할 수 있습니다.

### 예:Interactive Communication에서 반복을 사용하여 신용 카드 트랜잭션 목록을 포맷, 구조 및 표시합니다. {#example-using-repeat-in-an-interactive-communication-to-format-structure-and-display-a-list-of-credit-card-transactions}

다음 예에서는 Interactive Communication에서 반복 을 사용하여 신용 카드 트랜잭션을 구성하고 렌더링하는 단계를 제공합니다.

1. 양식 데이터 모델 기반 텍스트 문서 조각에서 관련 양식 데이터 모델 개체(및 이 예제와 같이 레이블에 필요한 포함된 텍스트)를 삽입합니다.

   ![1_elementstext](assets/1_elementstext.png)

   >[!NOTE]
   >
   >반복 가능한 콘텐츠는 Collection 형식의 속성을 하나 이상 포함해야 합니다.

1. 반복을 적용할 컨텐츠를 선택합니다.

   ![2_selection](assets/2_selection.png)

1. 반복 을 누릅니다.

   반복 대화 상자가 나타납니다.

   ![3_repeatdialog](assets/3_repeatdialog.png)

1. 구분자로 줄 바꿈을 선택하고 필요한 경우 조건 추가 를 탭하여 규칙을 만듭니다. 텍스트를 구분자로 사용하고 구분자로 사용할 텍스트 문자를 지정할 수도 있습니다.

   규칙 만들기 대화 상자가 나타납니다.

1. Interactive Communication에서 3월 한 달에 대한 트랜잭션만 포함하도록 2018년 2월 28일 이후 일자를 지정한 트랜잭션을 표시하는 규칙을 만듭니다.

   >[!NOTE]
   >
   >이 예에서는 에이전트가 2018년 3월 말에 문을 작성할 것으로 가정합니다. 그렇지 않으면 2018년 3월 이후 트랜잭션을 제외하도록 2018-04-01 전에 트랜잭션을 포함하는 다른 규칙을 만들 수 있습니다.

   ![4_createurl](assets/4_createrule.png)

1. 조건/규칙을 저장한 다음 반복을 저장합니다. 조건부 반복은 선택한 컨텐츠에 적용됩니다.

   ![5_onmouseoverconditionrule](assets/5_onmouseoverconditionrule.png)

   마우스를 위에 놓으면 텍스트 문서 조각에 조건에 사용된 구분 기호와 조건이 컨텐츠에 적용된 반복에 사용됩니다.

1. 텍스트 문서 조각을 저장하고 관련 대화형 커뮤니케이션을 미리 봅니다. 양식 데이터 모델의 데이터에 따라 요소에 적용된 반복은 미리 보기에서 다음과 유사한 트랜잭션 세부 정보를 렌더링합니다.

   ![screen_shot_2018-03-09at155516copy](assets/screen_shot_2018-03-09at155516copy.png)

### 예:편지에 반복을 사용하여 신용 카드 트랜잭션 목록을 형식 지정, 구조 및 표시합니다. {#example-using-repeat-in-a-letter-to-format-structure-and-display-a-list-of-credit-card-transactions}

다음 예에서는 반복을 사용하여 신용 카드 트랜잭션을 편지에 구조화하고 렌더링하는 단계를 제공합니다. 유사한 단계를 사용하면 다른 시나리오에서 반복을 사용할 수 있습니다.

1. 반복되는/동적 데이터를 렌더링하고 DD 요소 주위에 필요한 텍스트를 포함하는 DD 요소가 있는 텍스트 모듈을 열거나 편집하는 동안 엽니다. 예를 들어, 텍스트 모듈에는 다음과 같은 DD 요소가 있어 신용 카드에서 거래 명세서를 만들 수 있습니다.

   ```javascript
   {^DD_creditcard_TransactionDate^} {^DD_creditcard_TransactionAmount^}
   {^DD_creditcard_TransactionType^}
   ```

   이러한 DD 요소는 신용 카드에서 수행된 트랜잭션 목록을 다음과 같은 정보로 렌더링합니다.

   거래 일자, 거래 금액 및 거래 유형(차변 또는 대변)

1. 다음과 같이 DD 요소 내에 텍스트를 포함하여 문을 보다 읽기 쉽게 만듭니다.

   ![1_repeat](assets/1_repeat.png)

   ```javascript
   Date: {^DD_creditcard_TransactionDate^} Amount (USD): {^DD_creditcard_TransactionAmount^} Transaction Type: {^DD_creditcard_TransactionType^}
   ```

   그러나 형식이 잘 지정된 문을 렌더링하는 작업은 아직 완료되지 않았습니다. 지금까지 수행한 작업에 따라 편지를 렌더링하면 다음과 같이 표시됩니다.

   ![1_1renderwithoutrepeat](assets/1_1renderwithoutrepeat.png)

   정적 텍스트를 DD 요소와 함께 반복하려면 추가 단계에서 설명한 대로 반복을 적용해야 합니다.

1. 반복할 DD 요소와 정적 텍스트를 아래와 같이 선택합니다.

   ![2_repeat_selecttext](assets/2_repeat_selecttext.png)

1. **반복**&#x200B;을 누릅니다. 빈 인라인 조건이 있는 반복 대화 상자가 나타납니다.

   ![3_repeat_dialog](assets/3_repeat_dialog.png)

1. 필요한 경우 50센트보다 큰 트랜잭션 금액을 렌더링하는 것과 같이 트랜잭션을 선택적으로 렌더링하는 조건을 삽입합니다.

   ```javascript
   ${DD_creditcard_TransactionAmount > 0.5}
   ```

   그렇지 않으면 정보(여기서 트랜잭션)를 선택적으로 렌더링할 필요가 없는 경우 대화 상자에서 다음을 삭제하여 조건을 비워 둡니다.`${}` 반복 표현식 저장 기능은 반복 표현식 창이 비어 있거나(반복이 필요하지 않은 경우 ${} 없이) 반복에 유효한 조건이 포함된 경우 활성화됩니다.

1. 다이내믹 텍스트 서식을 지정할 구분자를 선택하고 확인 표시를 눌러 저장합니다.

   * **줄 바꿈**:출력 편지의 각 트랜잭션 입력 뒤에 줄바꿈을 삽입합니다.
   * **텍스트**:출력 문자의 각 트랜잭션 항목 뒤에 지정된 텍스트 문자를 삽입합니다.

   조건이 삽입되면 반복이 있는 텍스트가 빨간색으로 강조 표시되고 핸들이 왼쪽에 나타납니다. 반복의 왼쪽에 있는 핸들을 마우스로 가리키면 반복 구성을 볼 수 있습니다.

   ![4_repeat_hoverdetail](assets/4_repeat_hoverdetail.png)

   핸들을 눌러 반복의 팝업 메뉴를 볼 수 있습니다. 이 경우 반복 구성을 편집하거나 제거할 수 있습니다.

   ![5_repeateditremove](assets/5_repeateditremove.png)

1. 관련 편지를 미리 보고 반복에 따라 텍스트가 렌더링된다는 것을 확인합니다. 다음을 사용하여 DD 요소의 값을 입력할 수 있습니다.

   * 샘플 데이터가 있는 문자를 미리 보는 동안 관련 데이터 사전을 기반으로 만들어진 샘플 XML 데이터 파일입니다.
   * 관련 데이터 사전에 첨부된 XML 데이터 파일입니다.

   자세한 내용은 [데이터 사전](https://helpx.adobe.com/aem-forms/6-2/data-dictionary.html)을 참조하십시오.

   ![6_repeatoutputpreview](assets/6_repeatoutputpreview.png)

   정적 텍스트는 트랜잭션 세부 정보와 함께 반복됩니다. 정적 텍스트 반복은 이 절차의 텍스트에 적용된 반복을 통해 촉진됩니다. ${DD_credcard_TransactionAmount > 0.5} 조건은 USD .5 아래의 트랜잭션이 편지에 렌더링되지 않도록 합니다.

   >[!NOTE]
   >
   >관련 텍스트 모듈을 만들거나 편집하는 동안에만 조건을 삽입하고 반복할 수 있습니다. 문자를 미리 보는 동안 텍스트 모듈을 편집할 수 있지만 조건을 삽입하거나 반복할 수는 없습니다.

## 인라인 조건 및 반복 사용 - 일부 사용 사례 {#using-inline-condition-and-repeat-some-use-cases}

### 조건 {#repeat-within-condition} 내에서 반복합니다.

조건 내에서 반복을 사용해야 할 수 있습니다. 서신 관리를 사용하면 인라인 조건 구성 내에서 반복을 사용할 수 있습니다.

예를 들어 조건(녹색으로 표시됨) 내에서 반복됩니다(빨간색으로 표시됨).

이 단계를 반복하여 신용 카드 트랜잭션을 렌더링하는 동안 ${DD_creditcard_nooftransactions > 0} 조건은 하나 이상의 트랜잭션이 있는 경우에만 반복 구성이 렌더링되도록 합니다.

![repeatwitincondition](assets/repeatwitincondition.png)

마찬가지로, 요구 사항에 따라 다음을 만들 수 있습니다.

* 조건 내에 하나 이상의 조건
* 반복 내에 하나 이상의 조건
* 조건 또는 반복 내에서 조건 및 반복의 조합

### 빈 인라인 조건 {#empty-inline-condition}

빈 인라인 조건을 삽입하고 나중에 텍스트 및 DD 요소를 포함해야 할 수도 있습니다. 서신 관리를 통해 이 작업을 수행할 수 있습니다.

![emptycondition](assets/emptycondition.png)

그러나 가능한 경우 텍스트 모듈에서 글머리 기호와 같은 의도한 서식과 함께 텍스트 및 DD 요소를 먼저 삽입하고 나중에 인라인 조건을 적용하는 것이 좋습니다.
