---
title: 인터랙티브 커뮤니케이션 및 문자에서 인라인 조건 및 반복
seo-title: 인터랙티브 커뮤니케이션 및 문자에서 인라인 조건 및 반복
description: 인라인 조건을 사용하고 인터랙티브한 커뮤니케이션 및 문자에 반복하면 문맥과 구조가 매우 좋은 커뮤니케이션을 만들 수 있습니다.
seo-description: 인라인 조건을 사용하고 인터랙티브한 커뮤니케이션 및 문자에 반복하면 문맥과 구조가 매우 좋은 커뮤니케이션을 만들 수 있습니다.
uuid: 32b48a8b-431d-4f9c-9f51-8e7e9ac624a0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4
topic-tags: interactive-communications
discoiquuid: bbaba39b-e15a-4143-b6fc-7789fa2917b4
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1694'
ht-degree: 0%

---


# 인터랙티브 커뮤니케이션 및 문자에서 인라인 조건 및 반복{#inline-condition-and-repeat-in-interactive-communications-and-letters}

## 인라인 조건 {#inline-conditions}

AEM Forms을 사용하면 텍스트 모듈의 인라인 조건을 사용하여 양식 데이터 모델(대화형 통신)이나 데이터 사전(문자 단위)과 연결된 컨텍스트 또는 데이터에 의존하는 텍스트 렌더링을 자동화할 수 있습니다. 인라인 조건은 true 또는 false인 조건 평가를 기반으로 특정 컨텐츠를 표시합니다.

조건은 양식 데이터 모델/데이터 사전 또는 최종 사용자가 제공하는 데이터 값에 대해 계산을 수행합니다. 인라인 조건을 사용하면 시간을 절약하고 오류를 줄일 수 있을 뿐만 아니라 상황에 맞게 개인화된 인터랙티브 커뮤니케이션/문자를 만들 수 있습니다.

자세한 내용은 다음을 참조하십시오.

* [인터랙티브한 커뮤니케이션 제작](../../forms/using/create-interactive-communication.md)
* [통신 관리 개요](/help/forms/using/cm-overview.md)
* [인터랙티브 커뮤니케이션의 텍스트](../../forms/using/texts-interactive-communications.md)

### 예: 규칙을 사용하여 인터랙티브 커뮤니케이션에서 인라인 텍스트 조건부 지정 {#example-using-rules-to-conditionalize-inline-text-in-interactive-communication}

Interactive Communication에서 문장, 단락 또는 텍스트 문자열을 조건부 지정하려면 해당 텍스트 문서 조각에서 규칙을 생성할 수 있습니다. 다음 예제는 무료 전화 번호를 대화형 통신 미국 수신자에게만 표시하는 규칙을 사용합니다.

자세한 내용은 Interactive Communications에서 텍스트 [에서 텍스트로 규칙 만들기를 참조하십시오](../../forms/using/texts-interactive-communications.md).

대화형 통신 및 에이전트에 텍스트 조각을 포함하면 에이전트 UI를 사용하여 대화형 통신을 준비하면 받는 사람에 대한 (양식 데이터 모델) 데이터가 평가되고 텍스트는 미국의 수신자에게만 표시됩니다.

### 예: 편지에 인라인 조건을 사용하여 적절한 주소 렌더링  {#example-using-inline-condition-in-a-letter-to-render-the-appropriate-address}

해당 텍스트 모듈에 인라인 조건을 삽입하여 문자에 인라인 조건을 삽입할 수 있습니다. 다음 예에서는 두 가지 조건을 사용하여 DD 요소 성별을 기준으로 적절한 주소인 Sir 또는 Ma&#39;am을 평가하고 표시합니다. 유사한 단계를 사용하여 다른 조건을 만들 수 있습니다.

>[!NOTE]
>
>기존 에셋에 이전 조건/반복 표현식(6.2 SP1 CFP 4 이전)이 포함되어 있는 경우 에셋에는 이전 조건 구문이 표시되고 반복됩니다. 하지만, 이전 상태/반복은 작동합니다. 새 표현식과 이전 조건/반복 표현식은 이전 표현식과 새 조건/반복 표현식의 중첩된 혼합을 만들기 위해 서로 호환됩니다.

1. 관련 텍스트 모듈에서 조건을 지정할 텍스트 부분을 선택하고 조건을 **누릅니다**.

   ![1_selecttext](assets/1_selecttext.png)

   조건 대화 상자가 빈 상태로 나타납니다.

   ![2_conditiondialog](assets/2_conditiondialog.png)

   >[!NOTE]
   >
   >비어 있거나 잘못된 조건부 식은 저장할 수 없습니다. 표현식을 저장하려면 안에 유효한 조건식이 있어야 `${}` 합니다.

1. 선택한/조건부 텍스트가 편지에 나타나는지 여부를 평가하는 조건을 구성한 다음 확인 표시를 눌러 표현식을 저장합니다.

   DD 요소를 두 번 눌러 조건에 삽입합니다. 적절한 연산자를 삽입하고 대화 상자에 다음 조건을 구성합니다.

   ```javascript
   ${DD_creditcard_Gender=="Male"}
   ```

   표현식 만들기에 대한 자세한 내용은 **표현식 빌더에서 표현식 빌더를** 사용하여 표현식 및 원격 함수 [만들기를 참조하십시오](../../forms/using/expression-builder.md). 식에 지정된 값은 데이터 사전의 요소에 대해 지원되어야 합니다. 자세한 내용은 [데이터 사전을 참조하십시오](../../forms/using/data-dictionary.md).

   조건이 삽입되면 조건 왼쪽에 있는 핸들 위로 마우스를 가져가면 조건을 볼 수 있습니다. 핸들을 눌러 조건의 팝업 메뉴를 보고 조건을 편집하거나 제거할 수 있습니다.

   ![3_hoverhandle](assets/3_hoverhandle.png) ![4_editconditremoveconditionpopup](assets/4_editconditionremoveconditionpopup.png)

1. 텍스트를 선택하여 유사한 조건을 삽입합니다 `Ma'am`.

   ```javascript
   ${DD_creditcard_Gender == "Female"}
   ```

1. 관련 편지를 미리 보고 텍스트가 인라인 조건에 따라 렌더링된다는 것을 확인합니다. 다음을 사용하여 DD 요소 성별 값을 입력할 수 있습니다.

   * 샘플 데이터가 있는 문자를 미리 보는 동안 관련 데이터 사전을 기반으로 만들어진 샘플 XML 데이터 파일입니다.
   * 관련 데이터 사전에 첨부된 XML 데이터 파일입니다.

   자세한 내용은 [데이터 사전을 참조하십시오](../../forms/using/data-dictionary.md).

   ![5_letter 출력](assets/5_letteroutput.png)

## 반복 {#repeat}

인스턴스 또는 발생이 생성된 각 문자로 계속 변경될 수 있는 신용 카드 명세서의 거래 등 대화형 통신/서신에 동적 정보가 있을 수 있습니다. 반복을 사용하여 텍스트 문서 조각에서 이러한 동적 정보의 형식을 지정하고 구조화할 수 있습니다.

또한 반복 구배 내에서 규칙/조건을 지정하여 대화형 통신/서신에 렌더링되는 정보/항목을 조건화할 수 있습니다.

### 예: Interactive Communication에서 반복 사용을 사용하여 신용 카드 거래 목록 서식, 구조 및 표시 {#example-using-repeat-in-an-interactive-communication-to-format-structure-and-display-a-list-of-credit-card-transactions}

다음 예에서는 반복 사용을 사용하여 인터랙티브 커뮤니케이션에서 신용 카드 거래를 구조화하고 렌더링하는 단계를 보여 줍니다.

1. 양식 데이터 모델 기반 텍스트 문서 조각에서 관련 양식 데이터 모델 객체(및 레이블에 필요한 포함 텍스트)를 삽입합니다.

   ![1_elementstext](assets/1_elementstext.png)

   >[!NOTE]
   >
   >반복 가능한 콘텐츠에는 컬렉션 유형의 속성이 하나 이상 포함되어야 합니다.

1. 반복을 적용할 컨텐츠를 선택합니다.

   ![2_selection](assets/2_selection.png)

1. 반복을 누릅니다.

   반복 대화 상자가 나타납니다.

   ![3_repeatdialog](assets/3_repeatdialog.png)

1. 줄 바꿈을 구분 문자로 선택하고 필요한 경우 조건 추가를 눌러 규칙을 만듭니다. 텍스트를 구분 문자로 사용하고 구분 문자로 사용할 텍스트 문자를 지정할 수도 있습니다.

   규칙 만들기 대화 상자가 나타납니다.

1. 2018년 2월 28일 이후의 트랜잭션을 표시하는 규칙을 생성하여 3월 동안의 거래만 대화형 통신에 포함시킵니다.

   >[!NOTE]
   >
   >이 예에서는 에이전트가 2018년 3월 말에 문을 만들 것이라고 가정합니다. 그렇지 않은 경우 2018-04-01 이전에 트랜잭션을 포함하여 2018년 3월 이후 트랜잭션을 제외할 다른 규칙을 만들 수 있습니다.

   ![4_createle](assets/4_createrule.png)

1. 조건/규칙을 저장한 다음 반복을 저장합니다. 선택한 컨텐츠에 조건부 반복이 적용됩니다.

   ![5_onmouseoverconditionrule](assets/5_onmouseoverconditionrule.png)

   마우스 위로 마우스를 가져가면 텍스트 문서 조각에 조건 및 컨텐츠에 적용된 반복에 사용된 구분 기호가 표시됩니다.

1. 텍스트 문서 조각을 저장하고 관련 대화형 통신을 미리 봅니다. 양식 데이터 모델의 데이터에 따라 요소에 적용된 반복은 미리 보기의 다음과 유사한 트랜잭션 세부 사항을 렌더링합니다.

   ![screen_shot_2018-03-09at15516copy](assets/screen_shot_2018-03-09at155516copy.png)

### 예: 서신의 반복 사용을 통해 신용 카드 거래 목록 서식, 구조 및 표시 {#example-using-repeat-in-a-letter-to-format-structure-and-display-a-list-of-credit-card-transactions}

다음 예에서는 반복적인 방법으로 신용 카드 거래를 구조화하고 렌더링하는 단계를 제공합니다. 유사한 단계를 사용하여 다른 시나리오에서 반복을 사용할 수 있습니다.

1. 반복/동적 데이터를 렌더링하고 DD 요소 주위에 필요한 텍스트를 포함하는 DD 요소가 있는 텍스트 모듈을 열고(편집 또는 만드는 동안) 예를 들어, 텍스트 모듈에는 신용카드 거래 명세서를 작성할 수 있는 다음과 같은 DD 요소가 있습니다.

   ```javascript
   {^DD_creditcard_TransactionDate^} {^DD_creditcard_TransactionAmount^}
   {^DD_creditcard_TransactionType^}
   ```

   이러한 DD 요소는 신용 카드에서 이루어진 거래 목록을 다음과 같은 정보로 렌더링합니다.

   거래 일자, 거래 금액 및 거래 유형(차변 또는 대변)

1. 다음과 같이 DD 요소 내에 텍스트를 포함하여 문을 보다 읽기 쉽게 만듭니다.

   ![1_repeat](assets/1_repeat.png)

   ```javascript
   Date: {^DD_creditcard_TransactionDate^} Amount (USD): {^DD_creditcard_TransactionAmount^} Transaction Type: {^DD_creditcard_TransactionType^}
   ```

   그러나 형식이 좋은 문을 렌더링하는 작업은 아직 완료되지 않았습니다. 지금까지 수행한 작업을 기반으로 편지를 렌더링하면 다음과 같이 표시됩니다.

   ![1_1렌더아웃반복](assets/1_1renderwithoutrepeat.png)

   정적 텍스트를 DD 요소와 함께 반복하려면 추가 단계에 설명된 대로 반복을 적용해야 합니다.

1. 아래에서 보듯이 반복할 DD 요소와 정적 텍스트를 선택합니다.

   ![2_repeat_selecttext](assets/2_repeat_selecttext.png)

1. 반복을 **누릅니다**. 빈 인라인 조건이 있는 반복 대화 상자가 나타납니다.

   ![3_repeat_dialog](assets/3_repeat_dialog.png)

1. 필요한 경우 조건을 삽입하여 50센트 이상의 거래 금액을 렌더링하는 것과 같이 선택적으로 트랜잭션을 렌더링합니다.

   ```javascript
   ${DD_creditcard_TransactionAmount > 0.5}
   ```

   그렇지 않으면 정보(여기서 트랜잭션)를 선택적으로 렌더링할 필요가 없으면 대화 상자에서 다음을 삭제하여 조건을 비워 둡니다. `${}`. 반복 표현식 저장은 반복 표현식 창이 비어 있거나(반복이 필요하지 않은 경우 ${} 없이) 반복할 수 있는 유효한 조건이 포함되어 있을 때 활성화됩니다.

1. 동적 텍스트의 서식을 지정할 구분 기호를 선택하고 체크 표시를 눌러 저장합니다.

   * **줄 바꿈**: 출력 서신의 각 트랜잭션 입력 뒤에 줄 바꿈을 삽입합니다.
   * **텍스트**: 출력 서신의 각 트랜잭션 입력 뒤에 지정된 텍스트 문자를 삽입합니다.

   조건이 삽입되면 반복이 있는 텍스트가 빨간색으로 강조 표시되고 핸들이 왼쪽에 나타납니다. 반복의 왼쪽에 있는 핸들 위로 마우스를 가져가면 반복 구절을 볼 수 있습니다.

   ![4_repeat_hoverdetail](assets/4_repeat_hoverdetail.png)

   핸들을 눌러 반복 구절을 편집하거나 제거할 수 있는 반복 팝업 메뉴를 볼 수 있습니다.

   ![5_repeateditremove](assets/5_repeateditremove.png)

1. 관련 편지를 미리 보고 반복에 따라 텍스트가 렌더링됩니다. 다음을 사용하여 DD 요소의 값을 입력할 수 있습니다.

   * 샘플 데이터가 있는 문자를 미리 보는 동안 관련 데이터 사전을 기반으로 만들어진 샘플 XML 데이터 파일입니다.
   * 관련 데이터 사전에 첨부된 XML 데이터 파일입니다.

   자세한 내용은 [데이터 사전을 참조하십시오](https://helpx.adobe.com/aem-forms/6-2/data-dictionary.html).

   ![6_repeatutputpreview](assets/6_repeatoutputpreview.png)

   정적 텍스트는 트랜잭션 세부 사항과 반복됩니다. 반복적인 정적 텍스트는 이 절차의 텍스트에 적용된 반복으로 촉진됩니다. 조건 ${DD_creditcard_TransactionAmount > 0.5}은(는) USD .5 아래의 거래가 서신에 렌더링되지 않도록 합니다.

   >[!NOTE]
   >
   >관련 텍스트 모듈을 만들거나 편집하는 동안에만 조건을 삽입하고 반복할 수 있습니다. 문자를 미리 보는 동안 텍스트 모듈을 편집할 수는 있지만 조건을 삽입하거나 반복할 수는 없습니다.

## 인라인 조건 및 반복 사용 - 일부 사용 사례  {#using-inline-condition-and-repeat-some-use-cases}

### 조건 내에서 반복 {#repeat-within-condition}

조건 내에서 반복을 사용해야 할 수도 있습니다. 통신 관리를 사용하면 인라인 조건 구문 내에서 반복을 사용할 수 있습니다.

예를 들어, 다음은 조건(녹색 형식)에서 반복(빨간색 형식 지정)입니다.

이 조건이 신용 카드 트랜잭션을 렌더링하는 동안 ${DD_credit_nooftransactions > 0} 조건이 하나 이상의 트랜잭션이 있는 경우에만 반복 구절이 렌더링되도록 합니다.

![반복 조건](assets/repeatwitincondition.png)

마찬가지로 요구 사항에 따라 다음을 만들 수 있습니다.

* 조건 내에 하나 이상의 조건
* 반복 내의 하나 이상의 조건
* 조건 또는 반복 내에서 조건 및 반복

### 빈 인라인 조건 {#empty-inline-condition}

빈 인라인 조건을 삽입하고 나중에 텍스트와 DD 요소를 삽입해야 할 수도 있습니다. 통신 관리에서는 그렇게 할 수 있습니다.

![빈 조건](assets/emptycondition.png)

하지만 가능하면 텍스트 모듈에 글머리 기호와 같은 의도된 서식을 먼저 삽입하고 이후에 인라인 조건을 적용하는 것이 좋습니다.
