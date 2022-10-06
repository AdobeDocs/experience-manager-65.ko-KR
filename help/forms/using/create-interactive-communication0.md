---
title: "자습서: 대화형 통신 만들기 "
seo-title: Create an Interactive Communication for Print and Web
description: 모든 빌딩 블록을 사용하여 대화형 통신 만들기
seo-description: Create an Interactive Communication using all building blocks
uuid: 5ffaa86f-87c7-4673-8b41-63ec61421be2
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ac5d8d4f-fc13-4e8d-819c-c5db07fa6870
docset: aem65
feature: Interactive Communication
exl-id: aaacee66-6bbe-498b-91b1-3a9545ff1aeb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2004'
ht-degree: 0%

---

# 자습서: 대화형 통신 만들기 {#tutorial-create-interactive-communication}

![09 스타일-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

이 자습서는 [첫 번째 대화형 통신 만들기](/help/forms/using/create-your-first-interactive-communication.md) 시리즈. 전체 자습서 사용 사례를 이해하고, 수행하고, 시연하기 위해 시리즈를 시간 순서대로 따르는 것이 좋습니다.

양식 데이터 모델, 문서 조각, 템플릿 및 웹 버전에 대한 테마 등의 모든 구성 요소를 만들었으면 대화형 통신 만들기를 시작할 수 있습니다.

대화형 커뮤니케이션은 다음 두 가지 채널을 통해 전달될 수 있습니다. 인쇄 및 웹 또한 인쇄 채널을 마스터로 사용하여 대화형 커뮤니케이션을 만들 수도 있습니다. 웹 채널에 대한 마스터 옵션으로 인쇄하면 웹 채널의 콘텐츠, 상속 및 데이터 바인딩이 인쇄 채널에서 파생됩니다. 또한 인쇄 채널에서 수행한 변경 사항이 웹 채널에서 동기화되도록 합니다. 그러나 대화형 통신 작성자는 웹 채널의 특정 구성 요소에 대한 상속을 중단할 수 있습니다.

이 자습서에서는 인쇄 및 웹 채널을 위한 대화형 커뮤니케이션을 만드는 단계를 안내합니다. 이 자습서를 마치면 다음을 수행할 수 있습니다.

* 인쇄 채널용 대화형 통신 만들기
* 웹 채널용 대화형 통신 만들기
* 인쇄 및 웹 대화형 커뮤니케이션 제작(기본)

## 동기화 없이 인쇄 및 웹용 대화형 커뮤니케이션 만들기 {#create-interactive-communications-for-print-and-web-with-no-synchronization}

### 인쇄 채널용 대화형 통신 만들기 {#create-interactive-communication-for-print-channel}

다음은 이 자습서에서 이미 만들어진 리소스 목록이며 인쇄 채널용 대화형 커뮤니케이션을 만드는 동안 필요한 리소스입니다.

**인쇄 템플릿:** [create_first_ic_print_template](../../forms/using/create-templates-print-web.md)

**양식 데이터 모델:** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**문서 조각:** [bill_details_first_ic, customer_details_first_ic, bill_summary_first_ic, summary_charge_first_ic](../../forms/using/create-document-fragments.md)

**레이아웃 조각:** [table_lf](../../forms/using/create-templates-print-web.md)

**이미지:** PayNow 및 ValueAddedServices

1. AEM 작성자 인스턴스에 로그인하고 다음 위치로 이동합니다. **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms 및 문서]**.
1. 탭 **만들기** 을(를) 선택합니다. **대화형 통신**. 다음 **대화형 통신 만들기** 마법사가 표시됩니다.
1. 지정 **create_first_ic** 에서 **제목** 그리고 **이름** 필드. 선택 **FDM_Create_First_IC** 을 양식 데이터 모델로 사용하고 **다음**.
1. 에서 **채널** 마법사:

   1. 지정 **create_first_ic_print_template** 인쇄 템플릿으로 사용 및 탭 **선택**. 다음을 확인합니다. **웹 채널용 기본으로 인쇄 사용** 확인란이 선택되어 있지 않습니다.

   1. 지정 **Create_First_IC_templates** 폴더 > **Create_First_IC_Web_Template** 을 웹 템플릿으로 사용하고 **선택**.

   1. 탭 **만들기**.

   대화형 커뮤니케이션이 성공적으로 만들어졌다는 확인 메시지가 표시됩니다.

1. 탭 **편집** 오른쪽 창에서 대화형 커뮤니케이션을 엽니다.
1. 로 이동합니다. **자산** 탭을 선택하고 필터를 적용하여 왼쪽 창에 문서 조각만 표시합니다.
1. 다음 문서 조각을 대화형 커뮤니케이션의 대상 영역으로 끌어다 놓습니다.

   | 문서 단편 | 대상 영역 |
   |---|---|
   | bill_details_first_ic | 청구 상세내역 |
   | customer_details_first_ic | 고객 세부 사항 |
   | bill_summary_first_ic | 청구 요약 |
   | summary_charge_first_interactive_communication | 요금 |

   ![대화형 커뮤니케이션용 문서 조각](assets/create_first_ic_doc_fragments_new.png)

1. 탭 **차트** 대상 영역 및 탭 **+** 를 추가하려면 **차트** 구성 요소.
1. 차트 구성 요소를 탭하고 을 선택합니다 ![configure_icon](assets/configure_icon.png) (구성). 차트 등록 정보는 왼쪽 창에 표시됩니다.

   1. 차트의 이름을 지정합니다.
   1. 선택 **파이** 에서 **차트 유형** 드롭다운 목록.
   1. 을(를) 선택합니다 **호출 유형** 속성 **호출** 데이터 모델 개체 형식 **X축** 섹션을 참조하십시오. 탭 ![done_icon](assets/done_icon.png).
   1. 선택 **빈도** 에서 **함수** 드롭다운 목록.
   1. 을(를) 선택합니다 **호출 유형** 속성 **호출** 데이터 모델 개체 형식 **Y축** 섹션을 참조하십시오. 탭 ![done_icon](assets/done_icon.png).
   1. 탭 ![done_icon](assets/done_icon.png) 차트 등록 정보를 저장합니다.

1. 로 이동합니다. **자산** 탭을 선택하고 필터를 적용하여 왼쪽 창에 레이아웃 조각만 표시합니다. 드래그 앤 드롭 **table_lf** 레이아웃 조각을 **항목화된 호출** 대상 영역.
1. 에서 텍스트 필드를 선택합니다 **날짜** 열 및 탭 ![configure_icon](assets/configure_icon.png) (구성).
1. 선택 **데이터 모델 개체** 에서 **바인딩 유형** 드롭다운 목록 및 선택 **호출** > **호출 날짜**. 탭 ![done_icon](assets/done_icon.png) 속성을 두 번 저장합니다.

   마찬가지로, **호출 시간**, **호출 번호**, **호출 기간**, 및 **통화 요금** 의 텍스트 필드 **시간**, **숫자**, **기간**, 및 **요금** 열을 각각 지정합니다.

1. 탭 **지금 지불** 대상 영역 및 탭 **+** 를 추가하려면 **이미지** 구성 요소.
1. 이미지 구성 요소를 탭하고 을 선택합니다 ![configure_icon](assets/configure_icon.png) (구성). 이미지 속성은 왼쪽 창에 표시됩니다.

   1. 지정 **지금 지불** 에서 이미지의 이름으로 **이름** 필드.
   1. 탭 **업로드**&#x200B;로컬 파일 시스템에 저장된 이미지를 선택하고 **열기**.
   1. 탭 ![done_icon](assets/done_icon.png) 를 눌러 이미지 속성을 저장합니다.

1. 추가하려면 13단계와 14단계를 반복합니다 **ValueAddedServices** 이미지를 **ValueAddedServices** 대상 영역.

### 웹 채널용 대화형 통신 만들기 {#create-interactive-communication-for-web-channel}

다음은 이 자습서에서 이미 만들어진 리소스 목록이며, 웹 채널을 위한 대화형 커뮤니케이션을 만드는 동안 필요한 리소스입니다.

**웹 템플릿:** [Create_First_IC_Web_Template](../../forms/using/create-templates-print-web.md)

**양식 데이터 모델:** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**문서 조각:** [bill_details_first_ic, customer_details_first_ic, bill_summary_first_ic, summary_charge_first_ic](../../forms/using/create-document-fragments.md)

**이미지:** PayNowWeb 및 ValueAddedServicesWeb

1. AEM 작성자 인스턴스에 로그인하고 다음 위치로 이동합니다. **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms 및 문서]**.
1. 탭 **만들기** 을(를) 선택합니다. **대화형 통신**. 다음 **대화형 통신 만들기** 마법사가 표시됩니다.
1. 지정 **create_first_ic** 에서 **제목** 그리고 **이름** 필드. 선택 **FDM_Create_First_IC** 을 양식 데이터 모델로 사용하고 **다음**.
1. 에서 **채널** 마법사:

   1. 지정 **create_first_ic_print_template** 인쇄 템플릿으로 사용 및 탭 **선택**. 다음을 확인합니다. **웹 채널용 기본으로 인쇄 사용** 확인란이 선택되어 있지 않습니다.

   1. 지정 **Create_First_IC_templates** 폴더 > **Create_First_IC_Web_Template** 을 웹 템플릿으로 사용하고 **선택**.

   1. 탭 **만들기**.

   대화형 커뮤니케이션이 성공적으로 만들어졌다는 확인 메시지가 표시됩니다.

1. 탭 **편집** 오른쪽 창에서 대화형 커뮤니케이션을 엽니다.
1. 탭하기 **채널** 왼쪽 창에서 탭을 선택하고 탭하기 **웹**.
1. 로 이동합니다. **자산** 탭을 선택하고 필터를 적용하여 왼쪽 창에 문서 조각만 표시합니다.
1. 다음 문서 조각을 대화형 커뮤니케이션의 대상 영역으로 끌어다 놓습니다.

   | 문서 단편 | 대상 영역 |
   |---|---|
   | bill_details_first_ic | 청구 상세내역 |
   | customer_details_first_ic | 고객 세부 사항 |
   | bill_summary_first_ic | 청구 요약 |
   | summary_charge_first_interactive_communication | 요금 |

1. 탭 **비용 요약** 대상 영역 및 탭 **+** 를 추가하려면 **차트** 구성 요소.
1. 차트 구성 요소를 탭하고 을 선택합니다 ![configure_icon](assets/configure_icon.png) (구성). 차트 등록 정보는 왼쪽 창에 표시됩니다.

   1. 차트의 이름을 지정합니다.
   1. 선택 **파이** 에서 **차트 유형** 드롭다운 목록.

   1. 을(를) 선택합니다 **호출 유형** 속성 **호출** 데이터 모델 개체 형식 **X축** 섹션을 참조하십시오. 탭 ![done_icon](assets/done_icon.png).

   1. 선택 **빈도** 에서 **함수** 드롭다운 목록.

   1. 을(를) 선택합니다 **호출 유형** 속성 **호출** 데이터 모델 개체 형식 **Y축** 섹션을 참조하십시오. 탭 ![done_icon](assets/done_icon.png).

   1. 탭 ![done_icon](assets/done_icon.png) 차트 등록 정보를 저장합니다.

1. 을(를) 선택합니다 **데이터 소스** 왼쪽 창에서 탭을 선택하고 을(를) 끌어서 놓습니다 **호출** 데이터 모델 개체를 **항목화된 호출** 대상 영역. 의 모든 속성 **호출** 데이터 모델 개체는 표 열로 표시됩니다 **항목화된 호출** 오른쪽 창의 대상 영역.

   사용 사례를 기반으로 테이블에 통화 날짜, 통화 시간, 통화 번호, 통화 기간 및 통화 요금 열이 필요합니다.

   ![대화형 커뮤니케이션용 테이블](assets/table_ic_web_new.png)

1. 선택 **Mobilenum** 테이블 열 머리글과 **더 많은 옵션** > **열 삭제**. 마찬가지로 **Calltype** 열.
1. 을(를) 선택합니다 **호출 날짜** 표 열 제목 및 탭 ![편집](assets/edit.png) (편집) 텍스트 이름을 바꿀 **호출 날짜**. 마찬가지로 테이블에서 다른 열 머리글의 이름을 변경합니다.
1. 사용 사례에 따라 **지금 지불** 버튼을 클릭하여 결제할 수 있는 옵션을 제공하는 대화형 커뮤니케이션의 버튼을 클릭합니다. 다음 단계를 실행하여 버튼을 삽입합니다.

   1. 탭 **지금 지불** 대상 영역 및 탭 **+** 를 추가하려면 **텍스트** 구성 요소.

   1. 텍스트 구성 요소를 탭하고 탭합니다 ![편집](assets/edit.png) (편집).
   1. 텍스트 이름을 다음으로 변경합니다. **지금 지불**.
   1. 텍스트를 선택하고 하이퍼링크 아이콘을 누릅니다.
   1. 에서 지급 URL을 지정합니다. **경로** 필드.
   1. 선택 **새 탭** 변환 전: **Target** 드롭다운 목록.

   1. 탭 ![done_icon](assets/done_icon.png) 하이퍼링크 속성을 저장하려면

1. 선택 **스타일** 다음 옆에 있는 드롭다운 목록에서 **미리 보기** 선택 사항입니다.

   ![대화형 커뮤니케이션에 대한 스타일 모드 선택](assets/select_style_ic_web_new.png)

1. 다음 단계를 사용하여 Interactive Communication에서 하이퍼링크 텍스트 스타일을 단추로 표시합니다.

   1. 텍스트 구성 요소를 탭하고 을 선택합니다 ![편집](assets/edit.png) (편집).
   1. 에서 **테두리** 섹션, **1.5px** 로서의 **테두리 너비**, 선택 **솔리드** 로서의 **테두리 스타일**, 및 을 지정합니다. **46px** 로서의 **테두리 반경**.

   1. 단추의 배경색으로 빨간색 을 선택합니다 **배경** 섹션을 참조하십시오.
   1. 에서 **여백** 필드 **Dimension 및 위치** 섹션에서 **동시에 편집** 아이콘을 클릭하고 **Right** 여백 **450px**. 상위, 하위 및 왼쪽 필드는 공백으로 설정됩니다.

   ![대화형 커뮤니케이션에 하이퍼링크 삽입](assets/ic_web_hyperlink_new.png)

1. 탭 **지금 지불** 대상 영역 및 탭 **+** 를 추가하려면 **이미지** 구성 요소.
1. 이미지 구성 요소를 탭하고 을 선택합니다 ![configure_icon](assets/configure_icon.png) (구성). 이미지 속성은 왼쪽 창에 표시됩니다.

   1. 지정 **지금 지불** 에서 이미지의 이름으로 **이름** 필드.

   1. 탭 **업로드**&#x200B;에서 을(를) 선택합니다. **PayNowWeb** 로컬 파일 시스템에 저장된 이미지를 탭하고 **열기**.

   1. 탭 ![done_icon](assets/done_icon.png) 를 눌러 이미지 속성을 저장합니다.

1. 사용 사례에 따라 **구독** 버튼을 클릭하여 추가된 값에 가입할 수 있는 옵션을 제공하는 Interactive Communication의 버튼.

   13 - 17단계를 반복하여 **구독** 버튼 **부가 가치 서비스** 타겟 영역 및 추가 **ValueAddedServicesWeb** 이미지.

## 자동 동기화를 사용하여 인쇄 및 웹용 대화형 커뮤니케이션 만들기 {#create-interactive-communications-for-print-and-web-with-auto-synchronization}

인쇄와 웹 채널 간의 자동 동기화를 활성화하여 대화형 커뮤니케이션을 만들 수도 있습니다. 자동 동기화를 활성화하려면 대화형 커뮤니케이션을 만드는 동안 마스터로 인쇄 옵션을 선택합니다. 마스터로 인쇄 옵션을 선택하면 웹 채널의 내용, 상속 및 데이터 바인딩이 인쇄 채널에서 파생됩니다. 또한 인쇄 채널에서 수행한 변경 사항이 웹 채널에 반영되도록 합니다.

인쇄 채널을 사용하여 웹 채널 컨텐츠를 파생하려면 다음 단계를 실행합니다.

1. AEM 작성자 인스턴스에 로그인하고 다음 위치로 이동합니다. **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms 및 문서]**.
1. 탭 **만들기** 을(를) 선택합니다. **대화형 통신**. 다음 **대화형 통신 만들기** 마법사가 표시됩니다.
1. 지정 **create_first_ic** 에서 **제목** 그리고 **이름** 필드. 선택 **FDM_Create_First_IC** 을 양식 데이터 모델로 사용하고 **다음**.
1. 에서 **채널** 마법사:

   1. 지정 **create_first_ic_print_template** 인쇄 템플릿으로 사용 및 탭 **선택**.

   1. 을(를) 선택합니다 **웹 채널용 기본으로 인쇄 사용** 확인란을 선택합니다.
   1. 지정 **Create_First_IC_templates** 폴더 > **Create_First_IC_Web_Template** 을 웹 템플릿으로 사용하고 **선택**.

   1. 탭 **만들기**.

   대화형 커뮤니케이션이 성공적으로 만들어졌다는 확인 메시지가 표시됩니다.

1. 탭 **편집** 오른쪽 창에서 대화형 커뮤니케이션을 엽니다.
1. 단계 6 - 15단계 실행 [인쇄 채널용 대화형 통신 만들기](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-print-channel) 섹션을 참조하십시오.
1. 탭하기 **채널** 왼쪽 창에서 탭을 선택하고 탭하기 **웹** 인쇄 채널에서 웹 채널에 대한 컨텐츠를 자동으로 생성합니다.
1. 로서의 **웹 채널용 기본으로 인쇄 사용** 4단계에서 확인란이 선택되어 있으면 인쇄 채널에서 웹 채널에 대해 컨텐츠 및 바인딩이 자동으로 생성됩니다.

   인쇄 채널 컨텐츠는 웹 채널 템플릿 컨텐츠 아래에 삽입됩니다. 인쇄 채널에서 자동으로 생성된 웹 채널 컨텐츠를 수정하려면 대상 영역에 대한 상속을 취소할 수 있습니다.

   웹 채널에서 관련 대상 영역을 마우스로 가리킨 다음 을 선택합니다 ![취소 상속](assets/cancelinheritance.png) (상속 취소) 및 **상속 취소** 대화 상자, 탭 **예**.

   ![상속 취소](assets/cancel_inheritance_web_channel_new.png)

   구성 요소의 상속을 취소한 경우 다시 활성화할 수 있습니다. 상속을 다시 사용하려면 구성 요소를 포함하는 관련 대상 영역의 경계를 마우스로 가리킨 다음 탭합니다 ![상속](assets/reenableinheritance.png).

1. 을(를) 선택합니다 **컨텐츠** 왼쪽 창에서 탭을 클릭합니다.
1. 컨텐츠 트리를 사용하여 자동 생성된 웹 채널 컨텐츠를 웹 템플릿의 기존 패널에 드래그하여 놓습니다. 다음은 재배열해야 하는 구성 요소 목록입니다.

   * BOM 상세내역 구성 요소를 BOM 상세내역 패널에 추가
   * 고객 세부 사항 패널의 고객 세부 사항 구성 요소
   * 청구 요약 구성품을 청구 요약 패널에 추가
   * 비용 구성 요소 요약 - 비용 패널 요약
   * 항목화된 호출 패널에 레이아웃 조각(테이블)

   ![웹 컨텐츠 트리](assets/ic_web_content_tree_new.png)

1. 13~18단계를 반복합니다 [웹 채널용 대화형 통신 만들기](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-web-channel) 를 삽입하려면 **지금 지불** 및 **구독** 대화형 커뮤니케이션의 웹 채널에 있는 하이퍼링크.
