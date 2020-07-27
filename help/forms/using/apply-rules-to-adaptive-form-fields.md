---
title: '"자습서를 게시하지 마십시오. 적응형 양식 필드에 규칙 적용"'
seo-title: 적응형 양식 필드에 규칙 적용
description: 적응형 양식에 인터랙티브한 요소, 비즈니스 논리 및 스마트 유효성 검사를 추가하는 규칙을 만듭니다.
seo-description: 적응형 양식에 인터랙티브한 요소, 비즈니스 논리 및 스마트 유효성 검사를 추가하는 규칙을 만듭니다.
page-status-flag: de-activated
uuid: 60f142aa-81ca-4333-8614-85a01e23e917
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 982eddba-2350-40e7-8a42-db02d28cf133
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 0%

---


# 자습서: 적응형 양식 필드에 규칙 적용 {#tutorial-apply-rules-to-adaptive-form-fields}

![06-apply-rules-to-adaptive-form_main](assets/06-apply-rules-to-adaptive-form_main.png)

이 자습서는 첫 번째 적응형 양식 [만들기 시리즈의 한 단계입니다](/help/forms/using/create-your-first-adaptive-form.md) . 전체 자습서 사용 사례를 이해하고, 실행하고, 시연하기 위해 시리즈를 시간순으로 따르는 것이 좋습니다.

## 자습서 정보 {#about-the-tutorial}

규칙을 사용하여 적응형 양식에 인터랙션, 비즈니스 논리 및 스마트 유효성 검사를 추가할 수 있습니다. 적응형 양식에는 내장된 규칙 편집기가 있습니다. 규칙 편집기는 가이드 투어와 유사한 드래그 앤 드롭 기능을 제공합니다. 드래그 앤 드롭 방법은 규칙을 만드는 데 가장 빠르고 쉬운 방법입니다. 또한 규칙 편집기에서는 코딩 기술을 테스트하거나 규칙을 한 단계 끌어올리는 데 관심이 있는 사용자가 코드 창을 제공합니다.

적응형 양식 규칙 편집기에서 규칙 [편집기에 대해 자세히 알아볼 수 있습니다](/help/forms/using/rule-editor.md).

튜토리얼이 종료될 때까지 다음과 같은 규칙을 만드는 방법을 학습합니다.

* 데이터베이스에서 데이터를 검색하려면 양식 데이터 모델 서비스를 호출합니다.
* 데이터 모델 서비스를 호출하여 데이터베이스에 데이터 추가
* 유효성 검사 실행 및 오류 메시지 표시

자습서의 각 섹션 끝에 있는 인터랙티브한 GIF 이미지는 작성 중인 양식의 기능을 신속하게 확인하고 확인하는 데 도움이 됩니다.

## 1단계: 데이터베이스에서 고객 레코드 검색 {#retrieve-customer-record}

양식 데이터 모델 [만들기 아티클에 따라 양식 데이터 모델을](/help/forms/using/create-form-data-model.md) 만들었습니다. 이제 규칙 편집기를 사용하여 Forms 데이터 모델 서비스를 호출하여 정보를 검색하고 데이터베이스에 추가할 수 있습니다.

모든 고객에게 고유한 고객 ID 번호가 할당되어 데이터베이스에서 관련 고객 데이터를 식별할 수 있습니다. 아래 절차에서는 고객 ID를 사용하여 데이터베이스에서 정보를 검색합니다.

1. 편집을 위해 응용 양식을 엽니다.

   [http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)

1. 고객 **[!UICONTROL ID]** 필드를 누르고 규칙 **[!UICONTROL 편집]** 아이콘을 누릅니다. 규칙 편집기 창이 열립니다.
1. 규칙을 추가하려면 **[!UICONTROL + 만들기]** 아이콘을 누릅니다. 시각적 편집기를 엽니다.

   시각적 편집기에서 기본적으로 **[!UICONTROL WHEN]** 문이 선택됩니다. 또한, 규칙 편집기를 실행한 양식 객체(이 경우 **[!UICONTROL 고객 ID]**)는 **[!UICONTROL WHEN]** 문에 지정됩니다.

1. 상태 **[!UICONTROL 선택]** 드롭다운을 누르고 **[!UICONTROL 변경됨을 선택합니다]**.

   ![사용자 지정](assets/whencustomeridischanged.png)

1. THEN **** 문 **[!UICONTROL 의 작업]** 선택 **[!UICONTROL 드롭다운에서 서비스]** 호출을선택합니다.
1. 선택 **[!UICONTROL 드롭다운에서 배송 주소]** 서비스 **[!UICONTROL 검색을]** 선택합니다.
1. 양식 개체 탭에서 **[!UICONTROL 고객 ID]** 필드를 **[!UICONTROL 드롭 개체로 드래그하여 놓거나 입력]** 상자 **[!UICONTROL 에서 여기]** 필드를선택하십시오.

   ![dropbjectstoinputfield-retrieval데이터](assets/dropobjectstoinputfield-retrievedata.png)

1. 양식 개체 탭의 **[!UICONTROL 고객 ID, 이름, 배송 주소, 상태 및 우편 번호]** 필드를 **[!UICONTROL 드롭 개체로 드래그하여 놓거나]** 출력 **[!UICONTROL 상자에서]** 여기필드를 선택하십시오.

   ![dropbjectstoutpfield-retrieval데이터](assets/dropobjectstooutputfield-retrievedata.png)

   완료를 **[!UICONTROL 눌러]** 규칙을 저장합니다. 규칙 편집기 창에서 **[!UICONTROL 닫기를 누릅니다]**.

1. 적응형 양식을 미리 봅니다. 고객 ID 필드에 **[!UICONTROL ID를]** 입력합니다. 이제 양식에서 데이터베이스에서 고객 세부 사항을 검색할 수 있습니다.

   ![검색 정보](assets/retrieve-information.gif)

## 2단계: 데이터베이스에 업데이트된 고객 주소 추가 {#updated-customer-address}

데이터베이스에서 고객 세부 정보를 검색한 후 배송 주소, 상태 및 우편 번호를 업데이트할 수 있습니다. 아래의 절차에서는 데이터 모델 양식 서비스를 호출하여 고객 정보를 데이터베이스로 업데이트합니다.

1. 제출 **[!UICONTROL 필드를]** 선택하고 규칙 **[!UICONTROL 편집]** 아이콘을 누릅니다. 규칙 편집기 창이 열립니다.
1. 제출 **[!UICONTROL - 규칙을]** 클릭하고 **[!UICONTROL 편집]** 아이콘을누릅니다. 전송 규칙을 편집하는 옵션이 나타납니다.

   ![제출 규칙](assets/submit-rule.png)

   WHEN(WHEN) 옵션에서 **[!UICONTROL 제출]** 및 **[!UICONTROL 클릭]** 옵션이 이미 선택되어 있습니다.

   ![submit-is-click](assets/submit-is-clicked.png)

1. THEN **[!UICONTROL 옵션]** 에서 **[!UICONTROL + 문 추가]** 옵션을 누릅니다. 작업 **[!UICONTROL 선택]** 드롭다운에서 서비스 **[!UICONTROL 호출]** 을선택합니다.
1. 선택 **[!UICONTROL 드롭다운에서 배송 주소]** 서비스 **** 업데이트를선택합니다.

   ![update-shipping-address](assets/update-shipping-address.png)

1. ![dropbjectstoinputfield-updatedata](assets/dropobjectstoinputfield-updatedata.png)

   양식 개체 탭에서 **[!UICONTROL 배송 주소, 상태 및 우편 번호]** 필드를 **[!UICONTROL 드롭 개체의 해당 태블릿 이름 .property(예: customerdetails .shippingAddress)로 드래그하여 놓거나]** INPUT **[!UICONTROL 상자에서 여기]** 필드를 선택하십시오. 테이블 이름(예: 이 사용 사례의 사용자 지정 세부 사항)이 접두사로 추가된 모든 필드는 업데이트 서비스에 대한 입력 데이터로 사용됩니다. 이러한 필드에 제공된 모든 컨텐츠는 데이터 소스에서 업데이트됩니다.

   >[!NOTE]
   >
   >이름 및 **[!UICONTROL 고객 ID]** 필드를 해당 tabename.property(예: customerdetails.name)로 드래그하여 **** 놓지 마십시오. 실수로 고객의 이름과 ID를 업데이트하지 않는 데 도움이 됩니다.

1. 양식 개체 탭의 **[!UICONTROL 고객 ID]** 필드를 입력 **[!UICONTROL 상자]** 의 id 필드로 드래그하여 놓습니다. 사전 고정된 태블릿 이름(예: 이 사용 사례의 사용자 지정 세부 사항)이 없는 필드는 업데이트 서비스에 대한 검색 매개 변수로 사용됩니다. 이 **[!UICONTROL 사용 사례의 id]** 필드는 사용자 지정 세부 사항 테이블의 레코드를 고유하게 식별합니다.
1. 완료를 **[!UICONTROL 눌러]** 규칙을 저장합니다. 규칙 편집기 창에서 **[!UICONTROL 닫기를 누릅니다]**.
1. 적응형 양식을 미리 봅니다. 고객의 세부 정보를 검색하고 배송 주소를 업데이트한 다음 양식을 제출합니다. 동일한 고객의 세부 사항을 다시 검색하면 업데이트된 배송 주소가 표시됩니다.

## 3단계: (보너스 섹션) 코드 편집기를 사용하여 유효성 검사를 실행하고 오류 메시지를 표시합니다. {#step-bonus-section-use-the-code-editor-to-run-validations-and-display-error-messages}

양식에 입력된 데이터가 올바른지, 잘못된 데이터의 경우 오류 메시지가 표시되는지 확인하려면 양식에서 유효성 검사를 실행해야 합니다. 예를 들어, 존재하지 않는 고객 ID를 양식에 입력한 경우 오류 메시지가 표시됩니다.

적응형 양식은 여러 구성 요소에 내장된 유효성 검사 기능(예: 이메일 및 숫자 필드)을 제공하므로 일반적인 사용 사례에 사용할 수 있습니다. 예를 들어, 고급 사용 사례에는 규칙 편집기를 사용하여 데이터베이스가 0(0) 레코드(레코드 없음)를 반환할 때 오류 메시지를 표시합니다.

다음 절차에서는 양식에 입력한 고객 ID가 데이터베이스에 없는 경우 오류 메시지를 표시하는 규칙을 만드는 방법을 보여 줍니다. 또한 규칙은 포커스를 가져와서 고객 ID 필드를 재설정합니다. 이 규칙 [은 양식 데이터 모델 서비스의 dataIntegrationUtils API를 사용하여](/help/forms/using/invoke-form-data-model-services.md) 고객 ID가 데이터베이스에 있는지 확인합니다.

1. 고객 **[!UICONTROL ID]** 필드를 누르고 `Edit Rules` 아이콘을 누릅니다. 규칙 편집기 창이 열립니다.
1. 규칙을 추가하려면 **[!UICONTROL + 만들기]** 아이콘을 누릅니다. 시각적 편집기를 엽니다.

   시각적 편집기에서 기본적으로 **[!UICONTROL WHEN]** 문이 선택됩니다. 또한, 규칙 편집기를 실행한 양식 객체(이 경우 **[!UICONTROL 고객 ID]**)는 **[!UICONTROL WHEN]** 문에 지정됩니다.

1. 상태 **[!UICONTROL 선택]** 드롭다운을 누르고 **[!UICONTROL 변경됨을 선택합니다]**.

   ![사용자 지정](assets/whencustomeridischanged.png)

   THEN **** 문 **[!UICONTROL 의 작업]** 선택 **[!UICONTROL 드롭다운에서 서비스]** 호출을선택합니다.

1. 시각적 **[!UICONTROL 편집기에서]** 코드 **[!UICONTROL 편집기로]**&#x200B;전환합니다. 창 오른쪽에 스위치 컨트롤이 있습니다. 코드 편집기가 열리고 다음과 유사한 코드가 표시됩니다.

   ![코드 편집기](assets/code-editor.png)

1. 입력 변수 섹션을 다음 코드로 바꿉니다.

   ```javascript
   var inputs = {
       "id" : this
   };
   ```

1. guidelib.dataIntegrationUtils.executeOperation(operationInfo, 입력, 출력) 섹션을 다음 코드로 바꿉니다.

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, function (result) {
     if (result) {
         result = JSON.parse(result);
       customer_Name.value = result.name;
       customer_Shipping_Address = result.shippingAddress;
     } else {
       if(window.confirm("Invalid Customer ID. Provide a valid customer ID")) {
             customer_Name.value = " ";
            guideBridge.setFocus(customer_ID);
       }
     }
   });
   ```

1. 적응형 양식을 미리 봅니다. 잘못된 고객 ID를 입력합니다. 오류 메시지가 나타납니다.

   ![display-validation-error](assets/display-validation-error.gif)

