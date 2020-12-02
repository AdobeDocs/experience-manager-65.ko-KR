---
title: '"자습서:대화형 통신 만들기 "'
seo-title: 인쇄 및 웹용 인터랙티브한 커뮤니케이션 제작
description: 모든 구성 요소를 사용하여 인터랙티브한 커뮤니케이션 제작
seo-description: 모든 구성 요소를 사용하여 인터랙티브한 커뮤니케이션 제작
uuid: 5ffaa86f-87c7-4673-8b41-63ec61421be2
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ac5d8d4f-fc13-4e8d-819c-c5db07fa6870
docset: aem65
translation-type: tm+mt
source-git-commit: bd70508b361ac8b62ebc0344538a18369a075f3e
workflow-type: tm+mt
source-wordcount: '2020'
ht-degree: 0%

---


# 자습서:대화형 통신 만들기 {#tutorial-create-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

이 자습서는 [첫 번째 대화형 통신 만들기](/help/forms/using/create-your-first-interactive-communication.md) 시리즈의 한 단계입니다. 전체 자습서 사용 사례를 이해하고, 실행하고, 시연하려면 연순의 순서로 시리즈를 따르는 것이 좋습니다.

양식 데이터 모델, 문서 조각, 템플릿 및 웹 버전에 대한 테마와 같은 모든 구성 요소를 만들었으면 대화형 통신 만들기를 시작할 수 있습니다.

인터랙티브 커뮤니케이션은인쇄 및 웹. 또한 인쇄 채널이 있는 대화형 통신을 마스터로 만들 수도 있습니다. 웹 채널에 대한 마스터 옵션으로 인쇄하면 웹 채널의 컨텐츠, 상속 및 데이터 바인딩이 인쇄 채널에서 파생됩니다. 또한 인쇄 채널에서 수행한 변경 사항이 웹 채널에서 동기화되도록 합니다. 그러나 대화형 통신 작성자는 웹 채널의 특정 구성 요소에 대한 상속을 끊을 수 있습니다.

이 자습서에서는 인쇄 및 웹 채널용 대화형 통신을 만드는 단계를 안내합니다. 이 튜토리얼의 끝에서 다음 작업을 수행할 수 있습니다.

* 인쇄 채널용 대화형 통신 만들기
* 웹 채널을 위한 대화형 통신 만들기
* 인쇄물로 인쇄 및 웹 인터랙티브 커뮤니케이션 기본 제작

## 동기화 없이 인쇄 및 웹용 대화형 통신 만들기 {#create-interactive-communications-for-print-and-web-with-no-synchronization}

### 인쇄 채널용 대화형 통신 만들기 {#create-interactive-communication-for-print-channel}

다음은 이 자습서에서 이미 만들어진 리소스 목록으로, 인쇄 채널용 대화형 통신을 만드는 동안 필요합니다.

**인쇄 템플릿:** [create_first_ic_print_template](../../forms/using/create-templates-print-web.md)

**양식 데이터 모델:** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**문서 조각:** [bill_details_first_ic, customer_details_first_ic, bill_summary_first_ic, summary_charts_first_ic](../../forms/using/create-document-fragments.md)

**레이아웃 조각:** [table_lf](../../forms/using/create-templates-print-web.md)

**이미지:** PayNow 및 ValueAddedServices

1. AEM 작성자 인스턴스에 로그인하고 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms 및 문서]**&#x200B;로 이동합니다.
1. **만들기**&#x200B;를 누르고 **대화형 통신**&#x200B;을 선택합니다. **대화형 통신 만들기** 마법사가 표시됩니다.
1. **제목**&#x200B;과 **이름** 필드에 **create_first_ic**&#x200B;을 지정합니다. 양식 데이터 모델로 **FDM_Create_First_IC**&#x200B;을 선택하고 **다음**&#x200B;을 누릅니다.
1. **채널** 마법사에서:

   1. 인쇄 템플릿으로 **create_first_ic_print_template**&#x200B;을 지정하고 **선택**&#x200B;을 누릅니다. **웹 채널에 대해 인쇄 기본 사용** 확인란이 선택되지 않았는지 확인합니다.

   1. **Create_First_IC_templates** 폴더 > **Create_First_IC_Web_Template**&#x200B;을 웹 템플릿으로 지정하고 **Select**&#x200B;를 누릅니다.

   1. **만들기**&#x200B;를 누릅니다.

   대화형 통신이 성공적으로 만들어졌다는 확인 메시지가 표시됩니다.

1. **편집**&#x200B;을 눌러 오른쪽 창에서 대화형 통신을 엽니다.
1. **자산** 탭으로 이동한 다음 필터를 적용하여 왼쪽 창에 문서 조각만 표시합니다.
1. 다음 문서 조각을 인터랙티브 커뮤니케이션의 대상 영역에 드래그하여 놓습니다.

   | 문서 단편 | 대상 영역 |
   |---|---|
   | bill_details_first_ic | BillDetails |
   | customer_details_first_ic | 고객 세부 사항 |
   | bill_summary_first_ic | BillSummary |
   | summary_charts_first_interactive_communication | 요금 |

   ![인터랙티브 커뮤니케이션을 위한 문서 조각](assets/create_first_ic_doc_fragments_new.png)

1. **차트** 대상 영역을 누르고 **+**&#x200B;을 눌러 **차트** 구성 요소를 추가합니다.
1. 차트 구성 요소를 누르고 ![configure_icon](assets/configure_icon.png) (구성)을 선택합니다. 왼쪽 창에 차트 속성이 표시됩니다.

   1. 차트의 이름을 지정합니다.
   1. **차트 유형** 드롭다운 목록에서 **파이**&#x200B;를 선택합니다.
   1. **X-axis** 섹션의 **호출** 데이터 모델 개체 유형에서 **calltype** 속성을 선택합니다. ![done_icon](assets/done_icon.png)을 누릅니다.
   1. **함수** 드롭다운 목록에서 **빈도**&#x200B;를 선택합니다.
   1. **Y-axis** 섹션의 **호출** 데이터 모델 개체 유형에서 **calltype** 속성을 선택합니다. ![done_icon](assets/done_icon.png)을 누릅니다.
   1. 차트 속성을 저장하려면 ![done_icon](assets/done_icon.png)을 누릅니다.

1. **자산** 탭으로 이동한 후 필터를 적용하여 왼쪽 창에 레이아웃 조각만 표시합니다. **table_lf** 레이아웃 조각을 **항목별 호출** 대상 영역으로 드래그하여 놓습니다.
1. **날짜** 열에서 텍스트 필드를 선택하고 ![configure_icon](assets/configure_icon.png)(구성)을 누릅니다.
1. **바인딩 유형** 드롭다운 목록에서 **데이터 모델 개체**&#x200B;을 선택하고 **호출** > **caldate**&#x200B;을 선택합니다. ![done_icon](assets/done_icon.png)을 두 번 눌러 속성을 저장합니다.

   마찬가지로 **Time**, **Number**, &lt;a11/>의 텍스트 필드에 대해 **calnumber**, **calcharts** 및 **calcharts**&#x200B;으로 바인딩을 만듭니다. 2/>지속 시간&#x200B;**및**&#x200B;요금&#x200B;**열 각각.******

1. **PayNow** 대상 영역을 누르고 **+**&#x200B;을 눌러 **이미지** 구성 요소를 추가합니다.
1. 이미지 구성 요소를 누르고 ![configure_icon](assets/configure_icon.png) (구성)을 선택합니다. 왼쪽 창에 이미지 속성이 표시됩니다.

   1. **이름** 필드에 이미지의 이름으로 **PayNow**&#x200B;를 지정합니다.
   1. **업로드**&#x200B;를 누르고 로컬 파일 시스템에 저장된 이미지를 선택한 다음 **열기**&#x200B;를 누릅니다.
   1. ![done_icon](assets/done_icon.png)을 눌러 이미지 속성을 저장합니다.

1. 13단계와 14단계를 반복하여 **ValueAddedServices** 이미지를 &lt;a2/>ValueAddedServices **대상 영역에 추가합니다.**

### 웹 채널 {#create-interactive-communication-for-web-channel} 대화형 통신 만들기

다음은 이 자습서에서 이미 만들어진 리소스 목록으로, 웹 채널에 대한 대화형 통신을 만드는 동안 필요합니다.

**웹 템플릿:** [Create_First_IC_Web_Template](../../forms/using/create-templates-print-web.md)

**양식 데이터 모델:** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**문서 조각:** [bill_details_first_ic, customer_details_first_ic, bill_summary_first_ic, summary_charts_first_ic](../../forms/using/create-document-fragments.md)

**이미지:** PayNowWeb 및 ValueAddedServicesWeb

1. AEM 작성자 인스턴스에 로그인하고 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms 및 문서]**&#x200B;로 이동합니다.
1. **만들기**&#x200B;를 누르고 **대화형 통신**&#x200B;을 선택합니다. **대화형 통신 만들기** 마법사가 표시됩니다.
1. **제목**&#x200B;과 **이름** 필드에 **create_first_ic**&#x200B;을 지정합니다. 양식 데이터 모델로 **FDM_Create_First_IC**&#x200B;을 선택하고 **다음**&#x200B;을 누릅니다.
1. **채널** 마법사에서:

   1. 인쇄 템플릿으로 **create_first_ic_print_template**&#x200B;을 지정하고 **선택**&#x200B;을 누릅니다. **웹 채널에 대해 인쇄 기본 사용** 확인란이 선택되지 않았는지 확인합니다.

   1. **Create_First_IC_templates** 폴더 > **Create_First_IC_Web_Template**&#x200B;을 웹 템플릿으로 지정하고 **Select**&#x200B;를 누릅니다.

   1. **만들기**&#x200B;를 누릅니다.

   대화형 통신이 성공적으로 만들어졌다는 확인 메시지가 표시됩니다.

1. **편집**&#x200B;을 눌러 오른쪽 창에서 대화형 통신을 엽니다.
1. 왼쪽 창에서 **채널** 탭을 누르고 **웹**&#x200B;을 누릅니다.
1. **자산** 탭으로 이동한 다음 필터를 적용하여 왼쪽 창에 문서 조각만 표시합니다.
1. 다음 문서 조각을 인터랙티브 커뮤니케이션의 대상 영역에 드래그하여 놓습니다.

   | 문서 단편 | 대상 영역 |
   |---|---|
   | bill_details_first_ic | BillDetails |
   | customer_details_first_ic | 고객 세부 사항 |
   | bill_summary_first_ic | BillSummary |
   | summary_charts_first_interactive_communication | 요금 |

1. **요금 요약** 대상 영역을 누르고 **+**&#x200B;을 눌러 **차트** 구성 요소를 추가합니다.
1. 차트 구성 요소를 누르고 ![configure_icon](assets/configure_icon.png) (구성)을 선택합니다. 왼쪽 창에 차트 속성이 표시됩니다.

   1. 차트의 이름을 지정합니다.
   1. **차트 유형** 드롭다운 목록에서 **파이**&#x200B;를 선택합니다.

   1. **X-axis** 섹션의 **호출** 데이터 모델 개체 유형에서 **calltype** 속성을 선택합니다. ![done_icon](assets/done_icon.png)을 누릅니다.

   1. **함수** 드롭다운 목록에서 **빈도**&#x200B;를 선택합니다.

   1. **Y-axis** 섹션의 **호출** 데이터 모델 개체 유형에서 **calltype** 속성을 선택합니다. ![done_icon](assets/done_icon.png)을 누릅니다.

   1. 차트 속성을 저장하려면 ![done_icon](assets/done_icon.png)을 누릅니다.

1. 왼쪽 창에서 **Data Sources** 탭을 선택하고 **호출** 데이터 모델 개체를 **항목별 호출** 대상 영역으로 드래그하여 놓습니다. **호출** 데이터 모델 개체의 모든 속성은 오른쪽 창의 **항목별 호출** 대상 영역에 테이블 열로 표시됩니다.

   사용 사례에 따라 테이블에 호출 날짜, 호출 시간, 호출 번호, 호출 기간 및 호출 요금 열이 필요합니다.

   ![대화형 통신을 위한 표](assets/table_ic_web_new.png)

1. **Mobilenum** 표 열 머리글을 선택하고 **기타 옵션** > **열 삭제**&#x200B;를 선택합니다. 마찬가지로 **Caltype** 열을 삭제합니다.
1. **Caldate** 표 열 제목을 선택하고 ![edit](assets/edit.png)(편집)을 눌러 텍스트 이름을 **호출 날짜**&#x200B;로 변경합니다. 마찬가지로 테이블의 다른 열 머리글의 이름을 변경합니다.
1. 사용 사례에 따라, 단추를 클릭하여 결제를 수행할 수 있는 옵션을 제공하는 대화형 통신에 **지금 지불** 단추를 삽입합니다. 다음 단계를 실행하여 단추를 삽입합니다.

   1. **지금 지불** 대상 영역을 누르고 **+**&#x200B;을 눌러 **텍스트** 구성 요소를 추가합니다.

   1. 텍스트 구성 요소를 누르고 ![edit](assets/edit.png)(편집)을 누릅니다.
   1. 텍스트 이름을 **지금 지불**&#x200B;으로 변경합니다.
   1. 텍스트를 선택하고 하이퍼링크 아이콘을 누릅니다.
   1. **경로** 필드에 지불 URL을 지정합니다.
   1. **Target** 드롭다운 목록에서 **새 탭**&#x200B;을 선택합니다.

   1. 하이퍼링크 속성을 저장하려면 ![done_icon](assets/done_icon.png)을 누릅니다.

1. **미리 보기** 옵션 옆의 드롭다운 목록에서 **스타일**&#x200B;을 선택합니다.

   ![인터랙티브 커뮤니케이션을 위한 스타일 모드 선택](assets/select_style_ic_web_new.png)

1. 다음 단계에 따라 대화형 통신에 하이퍼링크 텍스트에 스타일을 지정하여 단추로 표시합니다.

   1. 텍스트 구성 요소를 누르고 ![edit](assets/edit.png) (편집)을 선택합니다.
   1. **테두리** 섹션에서 **1.5px**&#x200B;을 **테두리 너비**&#x200B;로 지정하고 **단색**&#x200B;을 **테두리 스타일**&#x200B;로 선택하고 **46px**&#x200B;를 **테두리 반경**.

   1. **배경** 섹션에서 단추의 배경색으로 [빨간색]을 선택합니다.
   1. **Dimension 및 위치** 섹션의 **여백** 필드에서 **동시에 편집** 아이콘을 누르고 **오른쪽** 여백을 **450px**&#x200B;로 설정합니다. 위쪽, 아래쪽 및 왼쪽 필드는 공백으로 설정됩니다.

   ![인터랙티브 커뮤니케이션에 하이퍼링크 삽입](assets/ic_web_hyperlink_new.png)

1. **지금 지불** 대상 영역을 누르고 **+**&#x200B;을 눌러 **이미지** 구성 요소를 추가합니다.
1. 이미지 구성 요소를 누르고 ![configure_icon](assets/configure_icon.png) (구성)을 선택합니다. 왼쪽 창에 이미지 속성이 표시됩니다.

   1. **이름** 필드에 이미지의 이름으로 **PayNow**&#x200B;를 지정합니다.

   1. **업로드**&#x200B;를 누르고 로컬 파일 시스템에 저장된 **PayNowWeb** 이미지를 선택하고 **열기**&#x200B;를 누릅니다.

   1. ![done_icon](assets/done_icon.png)을 눌러 이미지 속성을 저장합니다.

1. 사용 사례에 따라, 단추를 클릭하여 부가가치 서비스에 가입할 수 있는 옵션을 제공하는 대화형 통신에 **구독** 단추를 삽입합니다.

   **부가 가치 서비스** 대상 영역에 **구독** 단추를 추가하고 **ValueAddedServicesWeb** 이미지를 추가하려면 13 - 17단계를 반복합니다.

## 자동 동기화를 사용하여 인쇄 및 웹용 대화형 통신 만들기 {#create-interactive-communications-for-print-and-web-with-auto-synchronization}

인쇄 및 웹 채널 간의 자동 동기화를 활성화하여 대화형 통신을 만들 수도 있습니다. 자동 동기화를 활성화하려면 대화형 통신을 생성하는 동안 마스터로 인쇄 옵션을 선택합니다. 마스터로 인쇄 옵션을 선택하면 웹 채널의 컨텐츠, 상속 및 데이터 바인딩이 인쇄 채널에서 파생됩니다. 또한 인쇄 채널에서 수행한 변경 사항이 웹 채널에 반영되도록 합니다.

인쇄 채널을 사용하여 웹 채널 컨텐츠를 도출하려면 다음 단계를 수행하십시오.

1. AEM 작성자 인스턴스에 로그인하고 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms 및 문서]**&#x200B;로 이동합니다.
1. **만들기**&#x200B;를 누르고 **대화형 통신**&#x200B;을 선택합니다. **대화형 통신 만들기** 마법사가 표시됩니다.
1. **제목**&#x200B;과 **이름** 필드에 **create_first_ic**&#x200B;을 지정합니다. 양식 데이터 모델로 **FDM_Create_First_IC**&#x200B;을 선택하고 **다음**&#x200B;을 누릅니다.
1. **채널** 마법사에서:

   1. 인쇄 템플릿으로 **create_first_ic_print_template**&#x200B;을 지정하고 **선택**&#x200B;을 누릅니다.

   1. **웹 채널용으로 인쇄 기본 사용** 확인란을 선택합니다.
   1. **Create_First_IC_templates** 폴더 > **Create_First_IC_Web_Template**&#x200B;을 웹 템플릿으로 지정하고 **Select**&#x200B;를 누릅니다.

   1. **만들기**&#x200B;를 누릅니다.

   대화형 통신이 성공적으로 만들어졌다는 확인 메시지가 표시됩니다.

1. **편집**&#x200B;을 눌러 오른쪽 창에서 대화형 통신을 엽니다.
1. [인쇄 채널용 대화형 통신 만들기](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-print-channel) 섹션 중 6 - 15단계를 실행합니다.
1. 왼쪽 창에서 **채널** 탭을 누르고 **웹**&#x200B;을 눌러 인쇄 채널에서 웹 채널에 대한 컨텐츠를 자동으로 생성합니다.
1. 4단계에서 **웹 채널에 대해 인쇄 기본 사용** 확인란이 선택되면 인쇄 채널에서 웹 채널에 대해 컨텐츠 및 바인딩이 자동으로 생성됩니다.

   인쇄 채널 컨텐츠는 웹 채널 템플릿 컨텐츠 아래에 삽입됩니다. 인쇄 채널에서 자동으로 생성된 웹 채널 컨텐츠를 수정하려면 대상 영역에 대한 상속을 취소할 수 있습니다.

   웹 채널에서 관련 대상 영역 위로 마우스를 가져간 다음 ![취소 상속](assets/cancelinheritance.png)(상속 취소)을 선택한 다음 **상속 취소** 대화 상자에서 **Yes**&#x200B;를 누릅니다.

   ![상속 취소](assets/cancel_inheritance_web_channel_new.png)

   구성 요소의 상속을 취소한 경우 다시 활성화할 수 있습니다. 상속을 다시 활성화하려면 구성 요소를 포함하는 관련 대상 영역의 경계를 가리키고 ![reenableinheritance](assets/reenableinheritance.png)를 누릅니다.

1. 왼쪽 창에서 **콘텐츠** 탭을 선택합니다.
1. 컨텐츠 트리를 사용하여 자동 생성된 웹 채널 컨텐츠를 웹 템플릿의 기존 패널에 드래그하여 놓습니다. 다음은 다시 정렬해야 하는 구성 요소 목록입니다.

   * 청구 상세내역 구성 요소를 청구 상세내역 패널에 추가
   * 고객 세부 정보 패널에 대한 고객 세부 사항 구성 요소
   * 청구 요약 구성 요소를 청구 요약 패널에 표시
   * 비용 구성 요소의 요약 - 비용 패널
   * 항목별 호출 패널에 대한 레이아웃 조각(테이블)

   ![웹 컨텐츠 트리](assets/ic_web_content_tree_new.png)

1. [웹 채널에 대한 대화형 통신 만들기](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-web-channel)의 13 - 18단계를 반복하여 대화형 커뮤니케이션의 웹 채널에서 **지금 지불** 및 **구독** 하이퍼링크를 삽입합니다.

