---
title: '"자습서를 게시하지 마십시오.적응형 양식 필드에 규칙 적용"'
seo-title: 적응형 양식 필드에 규칙 적용
description: 적응형 양식에 상호 작용, 비즈니스 논리 및 스마트 유효성 검사를 추가하는 규칙을 만듭니다.
seo-description: 적응형 양식에 상호 작용, 비즈니스 논리 및 스마트 유효성 검사를 추가하는 규칙을 만듭니다.
page-status-flag: de-activated
uuid: 60f142aa-81ca-4333-8614-85a01e23e917
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 982eddba-2350-40e7-8a42-db02d28cf133
translation-type: tm+mt
source-git-commit: e3ecf724cdfcd20ef4c089605e644ad10ef1221b
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 0%

---


# 자습서:적응형 양식 필드 {#tutorial-apply-rules-to-adaptive-form-fields}에 규칙 적용

![06-apply-rules-to-adaptive-form_main](assets/06-apply-rules-to-adaptive-form_main.png)

이 자습서는 [첫 번째 적응형 양식 만들기](/help/forms/using/create-your-first-adaptive-form.md) 시리즈의 한 단계입니다. Adobe은 전체 자습서 사용 사례를 이해하고, 수행하고, 시연하기 위해 연순으로 시리즈를 따르는 것이 좋습니다.

## 자습서 {#about-the-tutorial} 정보

규칙을 사용하여 적응형 양식에 상호 작용, 비즈니스 논리 및 스마트 유효성 검사를 추가할 수 있습니다. 적응형 양식에는 내장된 규칙 편집기가 있습니다. 규칙 편집기에서는 가이드 투어와 유사한 드래그 앤 드롭 기능을 제공합니다. 드래그 앤 드롭 방법은 규칙을 만드는 가장 빠르고 쉬운 방법입니다. 또한 규칙 편집기에서는 코딩 기술을 테스트하거나 규칙을 한 단계 발전시키는 데 관심이 있는 사용자가 코드 창을 제공합니다.

규칙 편집기에 대한 자세한 내용은 [적응형 Forms 규칙 편집기](/help/forms/using/rule-editor.md)에서 참조할 수 있습니다.

튜토리얼이 끝나면 다음 작업을 위한 규칙을 만드는 방법을 알아봅니다.

* 데이터베이스에서 데이터를 검색하려면 양식 데이터 모델 서비스를 호출합니다.
* 양식 데이터 모델 서비스를 호출하여 데이터베이스에 데이터를 추가합니다.
* 유효성 검사 실행 및 오류 메시지 표시

자습서의 각 섹션 끝에 있는 대화형 GIF 이미지는 작성 중인 양식의 기능을 신속하게 배우고 확인하는 데 도움이 됩니다.

## 1단계:데이터베이스 {#retrieve-customer-record}에서 고객 레코드 검색

[양식 데이터 모델 만들기](/help/forms/using/create-form-data-model.md) 아티클을 따라 양식 데이터 모델을 만들었습니다. 이제 규칙 편집기를 사용하여 Forms 데이터 모델 서비스를 호출하여 정보를 검색하고 데이터베이스에 추가할 수 있습니다.

모든 고객에게 고유한 고객 ID 번호가 할당되므로 데이터베이스에서 관련 고객 데이터를 식별할 수 있습니다. 아래 절차에서는 고객 ID를 사용하여 데이터베이스에서 정보를 검색합니다.

1. 편집할 적응형 양식을 엽니다.

   [http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)

1. **[!UICONTROL 고객 ID]** 필드를 누르고 **[!UICONTROL 규칙 편집]** 아이콘을 누릅니다. 규칙 편집기 창이 열립니다.
1. **[!UICONTROL + 만들기]** 아이콘을 눌러 규칙을 추가합니다. 시각적 편집기를 엽니다.

   시각적 편집기에서 기본적으로 **[!UICONTROL WHEN]** 문이 선택됩니다. 또한, 규칙 편집기를 실행한 양식 개체(이 경우 **[!UICONTROL 고객 ID]**)는 **[!UICONTROL WHEN]** 문에 지정됩니다.

1. **[!UICONTROL 상태 선택]** 드롭다운을 누르고 **[!UICONTROL 가 변경됨]**&#x200B;을 선택합니다.

   ![사용자 지정이 변경된 시기](assets/whencustomeridischanged.png)

1. **[!UICONTROL THEN]** 문의 **[!UICONTROL 작업 선택]** 드롭다운에서 **[!UICONTROL 호출 서비스]**&#x200B;를 선택합니다.
1. **[!UICONTROL 선택]** 드롭다운에서 **[!UICONTROL 배송 주소 검색]** 서비스를 선택합니다.
1. 양식 개체 탭의 **[!UICONTROL 고객 ID]** 필드를 **[!UICONTROL 드롭 개체로 드래그하여 놓거나**[!UICONTROL  INPUT ]**상자에 있는]** 필드를 선택하십시오.

   ![dropbjectstoinputfield-retriedata](assets/dropobjectstoinputfield-retrievedata.png)

1. 양식 개체 탭의 **[!UICONTROL 드롭 개체로**[!UICONTROL &#x200B;고객 ID, 이름, 배송 주소, 주 및 우편번호&#x200B;]**필드를 드래그하여 놓거나**[!UICONTROL  OUTPUT ]**상자에 있는 here]** 필드를 선택합니다.

   ![dropbjectstoutpfield-retriedata](assets/dropobjectstooutputfield-retrievedata.png)

   **[!UICONTROL 완료]**&#x200B;를 눌러 규칙을 저장합니다. 규칙 편집기 창에서 **[!UICONTROL 닫기]**&#x200B;를 탭합니다.

1. 적응형 양식을 미리 봅니다. **[!UICONTROL 고객 ID]** 필드에 ID를 입력합니다. 이제 양식에서 데이터베이스에서 고객 세부 정보를 검색할 수 있습니다.

   ![검색 정보](assets/retrieve-information.gif)

## 2단계:업데이트된 고객 주소를 데이터베이스 {#updated-customer-address}에 추가합니다.

데이터베이스에서 고객 세부 정보를 검색한 후 배송 주소, 상태 및 우편 번호를 업데이트할 수 있습니다. 아래 절차에서는 양식 데이터 모델 서비스를 호출하여 고객 정보를 데이터베이스로 업데이트합니다.

1. **[!UICONTROL 제출]** 필드를 선택하고 **[!UICONTROL 규칙 편집]** 아이콘을 누릅니다. 규칙 편집기 창이 열립니다.
1. **[!UICONTROL 제출 -]** 규칙을 선택하고 **[!UICONTROL 편집]** 아이콘을 누릅니다. 제출 규칙을 편집하는 옵션이 나타납니다.

   ![제출 규칙](assets/submit-rule.png)

   WHEN 옵션에서 **[!UICONTROL 제출]** 및 **[!UICONTROL 을(를) 클릭한 경우]** 옵션이 이미 선택되어 있습니다.

   ![submit-is-click](assets/submit-is-clicked.png)

1. **[!UICONTROL THEN]** 옵션에서 **[!UICONTROL + 문 추가]** 옵션을 누릅니다. **[!UICONTROL 작업 선택]** 드롭다운에서 **[!UICONTROL 서비스 호출]**&#x200B;을 선택합니다.
1. **[!UICONTROL 선택]** 드롭다운에서 **[!UICONTROL 배송 주소 업데이트]** 서비스를 선택합니다.

   ![update-shipping-address](assets/update-shipping-address.png)

   ![dropbjectstoinputfield-updatedata](assets/dropobjectstoinputfield-updatedata.png)

1. **[!UICONTROL Drop 개체의 [!UICONTROL 양식 개체] 탭에서**[!UICONTROL &#x200B;배송 주소, 주 및 우편 번호&#x200B;]**필드를 &lt;a4/>INPUT&lt;a7>INPUT&lt;a7>의 해당 태블릿 이름 .property(예: customerdetails .shippingAddress)로 드래그하여 놓거나**[!UICONTROL  INPUT ]**상자를 엽니다.]** 태블릿 이름이 접두사로 추가된 모든 필드(예: 이 사용 사례의 고객 세부 사항)는 업데이트 서비스에 대한 입력 데이터로 사용됩니다. 이러한 필드에 제공된 모든 컨텐츠는 데이터 소스에서 업데이트됩니다.

   >[!NOTE]
   >
   >**[!UICONTROL 이름]** 및 **[!UICONTROL 고객 ID]** 필드를 해당 tabename.property(예: customerdetails.name)로 드래그 앤 드롭하지 마십시오. 실수로 고객의 이름과 ID를 업데이트하지 않는 데 도움이 됩니다.

1. [!UICONTROL 양식 개체] 탭의 **[!UICONTROL 고객 ID]** 필드를 **[!UICONTROL INPUT]** 상자의 id 필드로 드래그하여 놓습니다. 사전 고정된 태블릿 이름(예: 이 사용 사례의 사용자 지정 정보)이 없는 필드는 업데이트 서비스에 대한 검색 매개 변수로 사용됩니다. 이 사용 사례의 **[!UICONTROL id]** 필드는 **customerdetails** 테이블의 레코드를 고유하게 식별합니다.
1. **[!UICONTROL 완료]**&#x200B;를 눌러 규칙을 저장합니다. 규칙 편집기 창에서 **[!UICONTROL 닫기]**&#x200B;를 탭합니다.
1. 적응형 양식을 미리 봅니다. 고객의 세부 정보를 검색하고 배송 주소를 업데이트한 다음 양식을 제출합니다. 동일한 고객의 상세내역을 다시 검색하면 업데이트된 배송 주소가 표시됩니다.

## 3단계:(보너스 섹션) 코드 편집기를 사용하여 유효성 검사를 실행하고 오류 메시지 {#step-bonus-section-use-the-code-editor-to-run-validations-and-display-error-messages} 표시

양식에 입력된 데이터가 올바른지, 잘못된 데이터의 경우 오류 메시지가 표시되는지 확인하려면 양식에서 유효성 검사를 실행해야 합니다. 예를 들어, 존재하지 않는 고객 ID를 양식에 입력하면 오류 메시지가 표시됩니다.

적응형 양식은 일반적인 사용 사례에 사용할 수 있는 내장 유효성 검사, 이메일 및 숫자 필드 등의 여러 구성 요소를 제공합니다. 예를 들어, 고급 사용 사례에는 규칙 편집기를 사용하여 데이터베이스가 0(0) 레코드(레코드 없음)를 반환할 때 오류 메시지를 표시합니다.

다음 절차에서는 양식에 입력한 고객 ID가 데이터베이스에 없는 경우 오류 메시지를 표시하는 규칙을 만드는 방법을 보여 줍니다. 또한 규칙은 포커스를 가져오고 **[!UICONTROL 고객 ID]** 필드를 재설정합니다. 규칙은 데이터 모델 서비스](/help/forms/using/invoke-form-data-model-services.md)의 dataIntegrationUtils API를 사용하여 고객 ID가 데이터베이스에 있는지 확인합니다.[

1. **[!UICONTROL 고객 ID]** 필드를 누르고 `Edit Rules` 아이콘을 누릅니다. [!UICONTROL 규칙 편집기] 창이 열립니다.
1. **[!UICONTROL + 만들기]** 아이콘을 눌러 규칙을 추가합니다. 시각적 편집기를 엽니다.

   시각적 편집기에서 기본적으로 **[!UICONTROL WHEN]** 문이 선택됩니다. 또한, 규칙 편집기를 실행한 양식 개체(이 경우 **[!UICONTROL 고객 ID]**)는 **[!UICONTROL WHEN]** 문에 지정됩니다.

1. **[!UICONTROL 상태 선택]** 드롭다운을 누르고 **[!UICONTROL 가 변경됨]**&#x200B;을 선택합니다.

   ![사용자 지정이 변경된 시기](assets/whencustomeridischanged.png)

   **[!UICONTROL THEN]** 문의 **[!UICONTROL 작업 선택]** 드롭다운에서 **[!UICONTROL 호출 서비스]**&#x200B;를 선택합니다.

1. **[!UICONTROL 시각적 편집기]**&#x200B;에서 **[!UICONTROL 코드 편집기]**&#x200B;로 전환합니다. 스위치 컨트롤이 창의 오른쪽에 있습니다. 다음과 유사한 코드를 표시하는 코드 편집기가 열립니다.

   ![코드 편집기](assets/code-editor.png)

1. 입력 변수 섹션을 다음 코드로 바꿉니다.

   ```javascript
   var inputs = {
       "id" : this
   };
   ```

1. `guidelib.dataIntegrationUtils.executeOperation (operationInfo, inputs, outputs)` 섹션을 다음 코드로 바꿉니다.

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

