---
title: '"자습서:문서 조각 만들기"'
seo-title: 대화형 커뮤니케이션용 문서 조각 만들기
description: 대화형 커뮤니케이션용 문서 조각 만들기
seo-description: 대화형 커뮤니케이션용 문서 조각 만들기
uuid: 677d717e-e92e-434e-8266-6fbbf94f3867
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8ae97a21-83af-4615-9be3-61e2f8065081
docset: aem65
feature: 대화형 통신
exl-id: 81429735-cd52-4621-8dc2-10dd89df3052
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1684'
ht-degree: 2%

---

# 자습서:문서 조각 만들기{#tutorial-create-document-fragments}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

이 자습서는 [첫 번째 대화형 통신 만들기](/help/forms/using/create-your-first-interactive-communication.md) 시리즈의 단계입니다. 전체 자습서 사용 사례를 이해하고, 수행하고, 시연하기 위해 시리즈를 시간 순서대로 따르는 것이 좋습니다.

문서 조각은 대화형 커뮤니케이션을 작성하는 데 사용되는 서신의 재사용 가능한 구성 요소입니다. 문서 조각은 다음 유형의 조각입니다.

* 텍스트 - 텍스트 자산은 하나 이상의 텍스트 단락으로 구성된 컨텐츠의 일부입니다. 단락은 정적 또는 동적일 수 있습니다.
* 목록 - 목록은 텍스트, 목록, 조건 및 이미지를 포함한 문서 조각 그룹입니다.
* 조건 - 조건을 사용하면 양식 데이터 모델에서 수신한 데이터를 기반으로 Interactive Communication에 포함되는 컨텐츠를 정의할 수 있습니다.

이 자습서에서는 [대화형 통신 계획](/help/forms/using/planning-interactive-communications.md) 섹션에 제공된 해부도를 기반으로 여러 텍스트 문서 조각을 만드는 단계를 안내합니다. 이 자습서를 마치면 다음을 수행할 수 있습니다.

* 문서 조각 만들기
* 변수 만들기
* 규칙 만들기 및 적용

![text_document_fragments](assets/text_document_fragments.gif)

다음은 이 자습서에서 만든 문서 조각 목록입니다.

* [청구서 세부 사항](../../forms/using/create-document-fragments.md#step-create-bill-details-text-document-fragment)
* [고객 세부 사항](../../forms/using/create-document-fragments.md#step-create-customer-details-text-document-fragment)
* [청구서 요약](../../forms/using/create-document-fragments.md#step-create-bill-summary-text-document-fragment)
* [비용 요약](../../forms/using/create-document-fragments.md#step-create-summary-of-charges-text-document-fragment)

각 문서 조각에는 정적 텍스트, 양식 데이터 모델에서 수신된 데이터 및 에이전트 UI를 사용하여 입력한 데이터가 있는 필드가 포함됩니다. 이러한 모든 필드는 [대화형 통신 계획](/help/forms/using/planning-interactive-communications.md) 섹션에 설명되어 있습니다.

이 자습서에서 문서 조각을 만드는 동안 에이전트 UI를 사용하여 데이터를 받는 필드에 대한 변수가 만들어집니다.

[양식 데이터 모델 만들기](../../forms/using/create-form-data-model0.md) 섹션에 설명된 대로 **FDM_Create_First_IC**&#x200B;을 이 자습서에서 문서 조각을 만드는 양식 데이터 모델로 사용합니다.

## 1단계:BOM 상세내역 텍스트 문서 조각 생성 {#step-create-bill-details-text-document-fragment}

BOM 상세내역 문서 조각에는 다음 필드가 포함됩니다.

| 필드 | 데이터 소스 |
|---|---|
| 송장 번호 | 에이전트 UI |
| 청구 기간 | 에이전트 UI |
| 청구서 날짜 | 에이전트 UI |
| 플랜 | 양식 데이터 모델 |

다음 단계를 실행하여 에이전트 UI를 데이터 소스로 사용하는 필드에 대한 변수를 만들고 정적 텍스트를 생성하고 문서 조각에서 양식 데이터 모델 요소를 사용합니다.

1. **[!UICONTROL Forms]** > **[!UICONTROL 문서 조각]**&#x200B;을 선택합니다.

1. **만들기** > **텍스트**&#x200B;를 선택합니다.
1. 다음 정보를 지정합니다.

   1. **bill_details_first_ic**&#x200B;을 **제목** 필드에 이름으로 입력합니다. 제목은 **이름** 필드에 자동으로 채워집니다.

   1. **데이터 모델** 섹션에서 **양식 데이터 모델**&#x200B;을 선택합니다.

   1. 양식 데이터 모델로 **FDM_Create_First_IC**&#x200B;을 선택하고 **선택**&#x200B;을 누릅니다.

   1. **다음**&#x200B;을 누릅니다.

1. 왼쪽 창에서 **변수** 탭을 선택하고 **만들기**&#x200B;를 탭합니다.
1. **변수 만들기** 섹션에서 다음을 수행합니다.

   1. 변수 이름으로 **Invoicenumber**&#x200B;를 입력합니다.
   1. **문자열**&#x200B;을 유형으로 선택합니다.
   1. **만들기**&#x200B;를 누릅니다.

   ![문자열 유형의 변수 만들기](assets/variable_create_string_new.png)

   4~5단계를 반복하여 다음 변수를 만듭니다.

   * 청구 기간:문자열 유형
   * 청구 일자:날짜 유형

   ![청구 상세내역](assets/variable_bill_details_new.png)

1. 오른쪽 창을 사용하여 다음 필드에 대한 정적 텍스트를 만듭니다.

   * 송장 번호
   * 청구 기간
   * 청구서 날짜
   * 플랜

   ![정적 텍스트](assets/variable_bill_details_static_text_new.png)

1. **Invoice No** 필드 옆에 커서를 놓고 왼쪽 창의 **Variables** 탭에서 **InvoiceNumber** 변수를 두 번 클릭합니다.
1. **청구 기간** 필드 옆에 커서를 놓고 **청구 기간** 변수를 두 번 클릭합니다.
1. **Bill Date** 필드 옆에 커서를 놓고 **Bill Date** 변수를 두 번 클릭합니다.
1. 왼쪽 창에서 **데이터 모델 개체** 탭을 선택합니다.
1. **계획** 필드 옆에 커서를 놓고 **고객** > **customerplan** 속성을 두 번 클릭합니다.

   ![bill_details_customerplan_fdm](assets/bill_details_customerplan_fdm.png)

1. **저장**&#x200B;을 클릭하여 BOM 상세내역 텍스트 문서 조각을 생성합니다.

## 2단계:고객 세부 사항 텍스트 문서 조각 만들기 {#step-create-customer-details-text-document-fragment}

고객 세부 사항 문서 조각에는 다음 필드가 포함되어 있습니다.

| 필드 | 데이터 소스 |
|---|---|
| 고객 이름 | 양식 데이터 모델 |
| 주소 | 양식 데이터 모델 |
| 공급 장소 | 에이전트 UI |
| 상태 코드 | 에이전트 UI |
| 모바일 번호 | 양식 데이터 모델 |
| 대체 연락처 번호 | 양식 데이터 모델 |
| 관계 번호 | 양식 데이터 모델 |
| 연결 수 | 에이전트 UI |

다음 단계를 실행하여 에이전트 UI를 데이터 소스로 사용하는 필드에 대한 변수를 만들고 정적 텍스트를 생성하고 문서 조각에서 양식 데이터 모델 요소를 사용합니다.

1. **[!UICONTROL Forms]** > **[!UICONTROL 문서 조각]**&#x200B;을 선택합니다.
1. **만들기** > **텍스트**&#x200B;를 선택합니다.
1. 다음 정보를 지정합니다.

   1. **customer_details_first_ic** 필드를 **제목** 필드에 이름으로 입력합니다. 제목은 **이름** 필드에 자동으로 채워집니다.

   1. **데이터 모델** 섹션에서 **양식 데이터 모델**&#x200B;을 선택합니다.

   1. 양식 데이터 모델로 **FDM_Create_First_IC**&#x200B;을 선택하고 **선택**&#x200B;을 누릅니다.

   1. **다음**&#x200B;을 누릅니다.

1. 왼쪽 창에서 **변수** 탭을 선택하고 **만들기**&#x200B;를 탭합니다.
1. **변수 만들기** 섹션에서 다음을 수행합니다.

   1. 변수 이름으로 **배치**&#x200B;를 입력합니다.
   1. **문자열**&#x200B;을 유형으로 선택합니다.
   1. **만들기**&#x200B;를 누릅니다.

   4~5단계를 반복하여 다음 변수를 만듭니다.

   * 상태 코드:숫자 유형
   * 번호 연결:숫자 유형


1. **데이터 모델 개체** 탭을 선택하고 오른쪽 창에 커서를 놓고 **customer** > **name** 속성을 두 번 클릭합니다.
1. Enter 키를 눌러 다음 행으로 커서를 이동하고 **customer** > **address** 속성을 두 번 클릭합니다.
1. 오른쪽 창을 사용하여 다음 필드에 대한 정적 텍스트를 만듭니다.

   * 모바일 번호
   * 대체 연락처 번호
   * 공급 장소
   * 관계 번호
   * 상태 코드
   * 연결 수

   ![고객 세부 사항 정적 텍스트](assets/customer_details_static_text_new.png)

1. **모바일 번호** 필드 옆에 커서를 놓고 **customer** > **mobilenum** 속성을 두 번 클릭합니다.
1. **대체 연락처 번호** 필드 옆에 커서를 놓고 ** customer** > **alternatemobilenumber** 속성을 두 번 클릭합니다.
1. **관계 번호** 필드 옆에 커서를 놓고 **customer** > **relationshipnumber** 속성을 두 번 클릭합니다.
1. **변수** 탭을 선택하고 **공급 장소** 필드 옆에 커서를 놓고 **배치** 변수를 두 번 클릭합니다.
1. **상태 코드** 필드 옆에 커서를 놓고 **상태 코드** 변수를 두 번 클릭합니다.
1. **연결 수** 필드 옆에 커서를 놓고 **Numberconnections** 변수를 두 번 클릭합니다.

   ![고객 세부 사항](assets/customer_details_df2_new.png)

1. **저장**&#x200B;을 클릭하여 고객 세부 사항 텍스트 문서 조각을 만듭니다.

## 3단계:청구 요약 텍스트 문서 조각 생성 {#step-create-bill-summary-text-document-fragment}

BOM 요약 문서 조각은 다음 필드를 포함합니다.

| 필드 | 데이터 소스 |
|---|---|
| 이전 잔액 | 에이전트 UI |
| 결제 | 에이전트 UI |
| 조정 | 에이전트 UI |
| 현재 청구 기간 | 양식 데이터 모델 |
| 만기 금액 | 에이전트 UI |
| 기한 | 에이전트 UI |

다음 단계를 실행하여 에이전트 UI를 데이터 소스로 사용하는 필드에 대한 변수를 만들고 정적 텍스트를 생성하고 문서 조각에서 양식 데이터 모델 요소를 사용합니다.

1. **[!UICONTROL Forms]** > **[!UICONTROL 문서 조각]**&#x200B;을 선택합니다.
1. **만들기** > **텍스트**&#x200B;를 선택합니다.
1. 다음 정보를 지정합니다.

   1. **bill_summary_first_ic**&#x200B;을 **제목** 필드에 이름으로 입력합니다. 제목은 **이름** 필드에 자동으로 채워집니다.

   1. **데이터 모델** 섹션에서 **양식 데이터 모델**&#x200B;을 선택합니다.

   1. 양식 데이터 모델로 **FDM_Create_First_IC**&#x200B;을 선택하고 **선택**&#x200B;을 누릅니다.

   1. **다음**&#x200B;을 누릅니다.

1. 왼쪽 창에서 **변수** 탭을 선택하고 **만들기**&#x200B;를 탭합니다.
1. **변수 만들기** 섹션에서 다음을 수행합니다.

   1. 변수 이름으로 **Previousbalance**&#x200B;를 입력합니다.
   1. **숫자**&#x200B;를 유형으로 선택합니다.
   1. **만들기**&#x200B;를 누릅니다.

   4~5단계를 반복하여 다음 변수를 만듭니다.

   * 결제:숫자 유형
   * 조정:숫자 유형
   * 금액:숫자 유형
   * 중복:날짜 유형


1. 오른쪽 창을 사용하여 다음 필드에 대한 정적 텍스트를 만듭니다.

   * 이전 잔액
   * 결제
   * 조정
   * 현재 청구 기간
   * 만기 금액
   * 기한
   * 만기 일자 이후의 연체료: $20

   ![청구 요약 정적 텍스트](assets/bill_summary_static_new.png)

1. **이전 잔액** 필드 옆에 커서를 놓고 **이전 잔액** 변수를 두 번 클릭합니다.
1. **Payments** 필드 옆에 커서를 놓고 **Payments** 변수를 두 번 클릭합니다.
1. **조정** 필드 옆에 커서를 놓고 **조정** 변수를 두 번 클릭합니다.
1. **Amountdue** 필드 옆에 커서를 놓고 **Amountdue** 변수를 두 번 클릭합니다.
1. **기한** 필드 옆에 커서를 놓고 **중복** 변수를 두 번 클릭합니다.
1. **데이터 모델 개체** 탭을 선택하고 오른쪽 창의 **현재 청구 기간** 필드 옆에 커서를 놓고 **bom** > **usagecharges** 속성을 두 번 클릭합니다.

   ![청구서 요약](assets/bill_summary_static_variables_new.png)

1. **저장**&#x200B;을 클릭하여 고객 세부 사항 텍스트 문서 조각을 만듭니다.

## 4단계:비용 텍스트 문서 조각 요약 생성 {#step-create-summary-of-charges-text-document-fragment}

비용 문서 조각의 요약에는 다음 필드가 포함됩니다.

| 필드 | 데이터 소스 |
|---|---|
| 전화 요금 | 양식 데이터 모델 |
| 전화 회의 요금 | 양식 데이터 모델 |
| SMS 요금 | 양식 데이터 모델 |
| 모바일 인터넷 요금 | 양식 데이터 모델 |
| 국가 로밍 요금 | 양식 데이터 모델 |
| 국제 로밍 요금 | 양식 데이터 모델 |
| 부가 서비스 요금 | 양식 데이터 모델 |
| 총 요금 | 양식 데이터 모델 |
| AP 총액 | 양식 데이터 모델 |

다음 단계를 실행하여 정적 텍스트를 생성하고 문서 조각에서 양식 데이터 모델 요소를 사용합니다.

1. **[!UICONTROL Forms]** > **[!UICONTROL 문서 조각]**&#x200B;을 선택합니다.
1. **만들기** > **텍스트**&#x200B;를 선택합니다.
1. 다음 정보를 지정합니다.

   1. **제목** 필드에 이름으로 **summary_charts_first_ic**&#x200B;을 입력합니다. 이름 필드에 제목이 자동으로 채워집니다.

   1. **데이터 모델** 섹션에서 **양식 데이터 모델**&#x200B;을 선택합니다.

   1. 양식 데이터 모델로 **FDM_Create_First_IC**&#x200B;을 선택하고 **선택**&#x200B;을 누릅니다.

   1. **다음**&#x200B;을 누릅니다.

1. 오른쪽 창을 사용하여 다음 필드에 대한 정적 텍스트를 만듭니다.

   * 전화 요금
   * 전화 회의 요금
   * SMS 요금
   * 모바일 인터넷 요금
   * 국가 로밍 요금
   * 국제 로밍 요금
   * 부가 서비스 요금
   * 총 요금
   * AP 총액

   ![요약 비용](assets/summary_charges_static_new.png)

1. **데이터 모델 개체** 탭을 선택합니다.
1. **호출 비용** 필드 옆에 커서를 놓고 **bom** > **호출** 속성을 두 번 클릭합니다.
1. **전화 회의 요금** 필드 옆에 커서를 놓고 **bom** > **concallcharts** 속성을 두 번 클릭합니다.
1. **SMS Charts** 필드 옆에 커서를 놓고 **bills** > **smcharts** 속성을 두 번 클릭합니다.
1. **모바일 인터넷 요금** 필드 옆에 커서를 놓고 **청구서** > **인터넷 요금** 속성을 두 번 클릭합니다.
1. **국가 로밍 요금** 필드 옆에 커서를 놓고 **bills** > **로밍 국가** 속성을 두 번 클릭합니다.
1. **국제 로밍 요금** 필드 옆에 커서를 놓고 **bills** > **roamingnl** 속성을 두 번 클릭합니다.
1. **Value Added Services Charts** 필드 옆에 커서를 놓고 **bls** > **vas** 속성을 두 번 클릭합니다.
1. **총 비용** 필드 옆에 커서를 놓고 **bom** > **usagecharges** 속성을 두 번 클릭합니다.
1. **TOTAL PAYABLE** 필드 옆에 커서를 놓고 **bills** > **usagecharges** 속성을 두 번 클릭합니다.

   ![비용 요약](assets/summary_charges_static_fdm_new.png)

1. **Value Added Services Charts** 행에서 텍스트를 선택하고 **Create Rule** 을 눌러 Interactive Communication에 행이 표시되는 조건을 만듭니다.
1. **규칙 만들기** 팝업 창에서 다음을 수행합니다.

   1. **데이터 모델 및 변수**&#x200B;를 선택한 다음 **bom** > **호출**&#x200B;을 선택합니다.

   1. **이**&#x200B;보다 작음을 연산자로 선택합니다.
   1. **숫자**&#x200B;를 선택하고 값을 **60**&#x200B;로 입력합니다.

   이 조건에 따라 통화 비용 필드의 값이 60보다 작은 경우에만 부가 서비스 비용 행이 표시됩니다.

   ![create_rules_caption](assets/create_rules_caption.gif)

1. **저장**&#x200B;을 클릭하여 비용 텍스트 문서 조각의 요약을 생성합니다.
