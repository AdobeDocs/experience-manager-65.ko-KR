---
title: '"자습서:대화형 통신 만들기 "'
seo-title: 인쇄 및 웹용 인터랙티브한 커뮤니케이션 제작
description: 모든 구성 요소를 사용하여 대화형 통신 만들기
seo-description: 모든 구성 요소를 사용하여 대화형 통신 만들기
uuid: 5ffaa86f-87c7-4673-8b41-63ec61421be2
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ac5d8d4f-fc13-4e8d-819c-c5db07fa6870
docset: aem65
translation-type: tm+mt
source-git-commit: e545fc5e2ea139bd8ebb7f84138ba68e03d71d19

---


# 자습서:인터랙티브한 커뮤니케이션 제작 {#tutorial-create-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

이 자습서는 첫 번째 인터랙티브 커뮤니케이션 [시리즈 만들기의 단계입니다](/help/forms/using/create-your-first-interactive-communication.md) . 전체 자습서 사용 사례를 이해하고, 실행하고, 시연하기 위해 시리즈를 시간 순서대로 따르는 것이 좋습니다.

양식 데이터 모델, 문서 조각, 템플릿 및 웹 버전에 대한 테마와 같은 모든 구성 요소를 만들었으면 대화형 통신을 만들기 시작할 수 있습니다.

인터랙티브 커뮤니케이션은 다음 두 가지 채널을 통해 제공할 수 있습니다.인쇄 및 웹 또한 인쇄 채널을 사용하여 대화형 통신을 마스터로 만들 수도 있습니다. 웹 채널에 대한 마스터 옵션으로 인쇄하면 웹 채널의 컨텐츠, 상속 및 데이터 바인딩이 인쇄 채널에서 파생됩니다. 또한 인쇄 채널에서 수행한 변경 사항이 웹 채널에서 동기화되도록 합니다. 그러나 대화형 통신 작성자는 웹 채널의 특정 구성 요소에 대한 상속을 끊을 수 있습니다.

이 자습서에서는 인쇄 및 웹 채널을 위한 대화형 통신을 만드는 단계를 안내합니다. 이 튜토리얼의 끝에서 다음 작업을 수행할 수 있습니다.

* 인쇄 채널용 대화형 통신 만들기
* 웹 채널에 대한 대화형 통신 만들기
* 마스터로 인쇄하여 인쇄 및 웹 인터랙티브한 커뮤니케이션 제작

## 동기화 없이 인쇄 및 웹용 인터랙티브한 커뮤니케이션 제작 {#create-interactive-communications-for-print-and-web-with-no-synchronization}

### 인쇄 채널용 인터랙티브한 커뮤니케이션 제작 {#create-interactive-communication-for-print-channel}

다음은 이 자습서에서 이미 작성된 리소스 목록이며 인쇄 채널용 대화형 통신을 만드는 동안 필요합니다.

**인쇄 템플릿:**[create_first_ic_print_template](../../forms/using/create-templates-print-web.md)

**양식 데이터 모델:** FDM_ [Create_First_IC](../../forms/using/create-form-data-model0.md)

**문서 조각:**[bill_details_first_ic, customer_details_first_ic, bill_summary_first_ic, summary_charges_first_ic](../../forms/using/create-document-fragments.md)

**레이아웃 조각:**[table_lf](../../forms/using/create-templates-print-web.md)

**이미지:** PayNow 및 ValueAddedServices

1. AEM 작성자 인스턴스에 로그인하고 Adobe Experience Manager > **[!UICONTROL 양식]** > **[!UICONTROL 양식]** 및 **[!UICONTROL 문서로 이동합니다]**.
1. 만들기를 **누르고** 대화형 **통신을 선택합니다**. 대화형 **통신 만들기** 마법사가 표시됩니다.
1. 제목 및 이름 **필드에 create_first_ic****를** **지정합니다** . 양식 **데이터 모델로 FDM_Create_First_IC를** 선택하고 다음을 **누릅니다**.
1. 채널 **마법사에서** 다음을 수행합니다.

   1. 인쇄 템플릿으로 **create_first_ic_print_template** 을 지정하고 선택을 **누릅니다**. [웹 채널에 **마스터로 인쇄] 확인란이** 선택되어 있지 않은지 확인합니다.

   1. Create_ **First_IC_templates** 폴더 > **Create_First_IC_Web_Template** 을 웹 템플릿으로 지정하고 선택을 **탭합니다**.

   1. 만들기를 **누릅니다**.
   대화형 통신이 성공적으로 만들어졌다는 확인 메시지가 표시됩니다.

1. 편집을 **눌러** 오른쪽 창에서 대화형 통신을 엽니다.
1. 자산 **탭으로** 이동하고 필터를 적용하여 왼쪽 창에 문서 조각만 표시합니다.
1. 다음 문서 조각을 인터랙티브 커뮤니케이션의 대상 영역에 드래그하여 놓습니다.

   | 문서 단편 | 대상 영역 |
   |---|---|
   | bill_details_first_ic | BillDetails |
   | customer_details_first_ic | 고객 세부 사항 |
   | bill_summary_first_ic | BillSummary |
   | summary_charts_first_interactive_communication | 요금 |

   ![인터랙티브 커뮤니케이션을 위한 문서 조각](assets/create_first_ic_doc_fragments_new.png)

1. 차트 **대상** 영역을 누르고 **+** 을 눌러 차트 **구성 요소를 추가합니다** .
1. 차트 구성 요소를 누르고 ![](assets/configure_icon.png) (구성)을 선택합니다. 차트 등록 정보는 왼쪽 창에 표시됩니다.

   1. 차트의 이름을 지정합니다.
   1. 차트 **유형** **드롭다운 목록에서** 파이를 선택합니다.
   1. X축 **섹션의** 호출 **데이터 모델 객체 유형에서** calltype **속성을** 선택합니다. 탭하기 ![](assets/done_icon.png).
   1. 함수 **드롭다운** 목록에서 **빈도를** 선택합니다.
   1. Y축 **섹션의** 호출 **데이터 모델 객체 유형에서** calltype **속성을** 선택합니다. 탭하기 ![](assets/done_icon.png).
   1. 차트 속성을 ![](assets/done_icon.png) 저장하려면 을 누릅니다.

1. 자산 **탭으로** 이동하고 필터를 적용하여 왼쪽 창에 레이아웃 조각만 표시합니다. table_lf **레이아웃 조각을 항목별 호출** 대상 **영역으로 드래그하여** 놓습니다.
1. 날짜 열에서 텍스트 **필드를** 선택하고 ![](assets/configure_icon.png) (구성)을 누릅니다.
1. 바인딩 **유형** 드롭다운 목록에서 데이터 모델 **개체를** 선택하고 **호출** > **calldateEvent를**&#x200B;선택합니다. 두 ![](assets/done_icon.png) 번 눌러 속성을 저장합니다.

   마찬가지로, **호출 시간**, **호출**&#x200B;번호 **,**&#x200B;호출 지속 **시간** , 그리고 The Charts The The The The TimeTimeCharts, NumberBeging Number **************** , Features, Binding Duration, Charges열을 각각 만듭니다.

1. PayNow **대상** 영역을 누르고 **+** 를 눌러 이미지 **구성 요소를 추가합니다** .
1. 이미지 구성 요소를 누르고 ![](assets/configure_icon.png) (구성)을 선택합니다. 왼쪽 창에 이미지 속성이 표시됩니다.

   1. 이름 **필드에** 이미지 이름으로 PayNow를 **지정합니다** .
   1. 업로드를 **누르고**&#x200B;로컬 파일 시스템에 저장된 이미지를 선택한 다음 열기를 **누릅니다**.
   1. 을 ![](assets/done_icon.png) 눌러 이미지 속성을 저장합니다.

1. 13단계와 14단계를 반복하여 **ValueAddedServices** 이미지를 **ValueAddedServices** 대상 영역에 추가합니다.

### Create Interactive Communication for Web channel {#create-interactive-communication-for-web-channel}

다음은 이 자습서에서 이미 만들어진 리소스 목록이며 웹 채널에 대한 대화형 통신을 만드는 동안 필요합니다.

**웹 템플릿:** Create_ [First_IC_Web_Template](../../forms/using/create-templates-print-web.md)

**양식 데이터 모델:** FDM_ [Create_First_IC](../../forms/using/create-form-data-model0.md)

**문서 조각:**[bill_details_first_ic, customer_details_first_ic, bill_summary_first_ic, summary_charges_first_ic](../../forms/using/create-document-fragments.md)

**이미지:** PayNowWeb 및 ValueAddedServicesWeb

1. AEM 작성자 인스턴스에 로그인하고 Adobe Experience Manager > **[!UICONTROL 양식]** > **[!UICONTROL 양식]** 및 **[!UICONTROL 문서로 이동합니다]**.
1. 만들기를 **누르고** 대화형 **통신을 선택합니다**. 대화형 **통신 만들기** 마법사가 표시됩니다.
1. 제목 및 이름 **필드에 create_first_ic****를** **지정합니다** . 양식 **데이터 모델로 FDM_Create_First_IC를** 선택하고 다음을 **누릅니다**.
1. 채널 **마법사에서** 다음을 수행합니다.

   1. 인쇄 템플릿으로 **create_first_ic_print_template** 을 지정하고 선택을 **누릅니다**. [웹 채널에 **마스터로 인쇄] 확인란이** 선택되어 있지 않은지 확인합니다.

   1. Create_ **First_IC_templates** 폴더 > **Create_First_IC_Web_Template** 을 웹 템플릿으로 지정하고 선택을 **탭합니다**.

   1. 만들기를 **누릅니다**.
   대화형 통신이 성공적으로 만들어졌다는 확인 메시지가 표시됩니다.

1. 편집을 **눌러** 오른쪽 창에서 대화형 통신을 엽니다.
1. 왼쪽 **창에서 채널** 탭을 누르고 웹을 **누릅니다**.
1. 자산 **탭으로** 이동하고 필터를 적용하여 왼쪽 창에 문서 조각만 표시합니다.
1. 다음 문서 조각을 인터랙티브 커뮤니케이션의 대상 영역에 드래그하여 놓습니다.

   | 문서 단편 | 대상 영역 |
   |---|---|
   | bill_details_first_ic | BillDetails |
   | customer_details_first_ic | 고객 세부 사항 |
   | bill_summary_first_ic | BillSummary |
   | summary_charts_first_interactive_communication | 요금 |

1. 비용 **요약** 대상 영역을 누르고 **+** 을 눌러 차트 **구성 요소를 추가합니다** .
1. 차트 구성 요소를 누르고 ![](assets/configure_icon.png) (구성)을 선택합니다. 차트 등록 정보는 왼쪽 창에 표시됩니다.

   1. 차트의 이름을 지정합니다.
   1. 차트 **유형** **드롭다운 목록에서** 파이를 선택합니다.

   1. X축 **섹션의** 호출 **데이터 모델 객체 유형에서** calltype **속성을** 선택합니다. 탭하기 ![](assets/done_icon.png).

   1. 함수 **드롭다운** 목록에서 **빈도를** 선택합니다.

   1. Y축 **섹션의** 호출 **데이터 모델 객체 유형에서** calltype **속성을** 선택합니다. 탭하기 ![](assets/done_icon.png).

   1. 차트 속성을 ![](assets/done_icon.png) 저장하려면 을 누릅니다.

1. 왼쪽 **창에서 Data** Sources 탭을 선택하고 **호출** 데이터 모델 개체를 항목별 호출 **대상 영역으로 드래그하여** 놓습니다. 호출 **데이터 모델 개체의 모든 속성은 오른쪽 창의 항목별 호출** 대상 **** 영역에 테이블 열로 표시됩니다.

   사용 사례에 따라 표의 호출 날짜, 호출 시간, 호출 번호, 호출 기간 및 호출 비용 열이 필요합니다.

   ![대화형 통신을 위한 표](assets/table_ic_web_new.png)

1. Mobilenum **표** 열 제목을 선택하고 추가 옵션 **>** 열 **삭제를**&#x200B;선택합니다. 마찬가지로 Calltype **열을** 삭제합니다.
1. Caldate **테이블** 열 제목을 선택하고 ![편집](assets/edit.png) (편집)을 탭하여 텍스트 이름을 Call Date로 **변경합니다**. 마찬가지로 테이블에서 다른 열 머리글의 이름을 변경합니다.
1. 사용 사례에 따라, **Interactive** Communication에 단추를 눌러 결제 옵션을 제공하는 지금 지불 단추를 삽입합니다. 다음 단계를 실행하여 단추를 삽입합니다.

   1. 지금 **지불** 타겟 영역을 누르고 **+** 를 눌러 텍스트 **구성 요소를 추가합니다** .

   1. 텍스트 구성 요소를 누르고 ![편집](assets/edit.png) (편집)을 누릅니다.
   1. 텍스트 이름을 지금 지불로 **변경합니다**.
   1. 텍스트를 선택하고 하이퍼링크 아이콘을 누릅니다.
   1. [경로] 필드에 결제 URL을 **지정합니다** .
   1. 타겟 **드롭다운** 목록에서 **새** 탭을 선택합니다.

   1. 을 ![](assets/done_icon.png) 눌러 하이퍼링크 속성을 저장합니다.

1. 미리 **보기** 옵션 옆에 있는 드롭다운 목록에서 스타일을 **선택합니다** .

   ![인터랙티브 커뮤니케이션의 스타일 모드 선택](assets/select_style_ic_web_new.png)

1. 다음 단계를 사용하여 대화형 통신에 하이퍼링크 텍스트의 스타일을 단추로 표시합니다.

   1. 텍스트 구성 요소를 누르고 ![편집](assets/edit.png) (편집)을 선택합니다.
   1. 테두리 **섹션에서** 1.5를 **** 테두리 **, 단색**&#x200B;선택 **스타일,** 단색 선택 ******** ****&#x200B;테두리 스타일, 46pxAsBorder Radius와 같이 지정합니다.

   1. 배경 섹션에서 단추의 배경색으로 빨간색을 **선택합니다** .
   1. [차원 및 위치] **에** 대한 **필드** 섹션에서 **[편집** ] **아이콘을 누르고 RightMargin** 50pxRightMargin **을 동시에** RightMargin 40px Along으로 설정합니다. 위쪽, 아래쪽 및 왼쪽 필드는 공백으로 설정됩니다.
   ![대화형 통신에 하이퍼링크 삽입](assets/ic_web_hyperlink_new.png)

1. 지금 **지불** 타겟 영역을 누르고 **+** 를 눌러 이미지 **구성 요소를 추가합니다** .
1. 이미지 구성 요소를 누르고 ![](assets/configure_icon.png) (구성)을 선택합니다. 왼쪽 창에 이미지 속성이 표시됩니다.

   1. 이름 **필드에** 이미지 이름으로 PayNow를 **지정합니다** .

   1. 업로드를 **누르고**&#x200B;로컬 파일 **시스템에** 저장된 PayNow 웹 이미지를 선택한 다음 열기를 **누릅니다**.

   1. 을 ![](assets/done_icon.png) 눌러 이미지 속성을 저장합니다.

1. 사용 사례에 따라, **단추를** 클릭하여 부가가치 서비스에 가입할 수 있는 옵션을 제공하는 대화형 통신에 구독 단추를 삽입합니다.

   13 - 17단계를 반복하여 **Value Added** Services **대상** 영역에 **구독** 단추를 추가하고 ValueAddedServices 웹이미지를추가합니다.

## 자동 동기화를 통해 인쇄 및 웹용 인터랙티브한 커뮤니케이션 제작 {#create-interactive-communications-for-print-and-web-with-auto-synchronization}

인쇄 및 웹 채널 간의 자동 동기화를 활성화하여 대화형 통신을 만들 수도 있습니다. 자동 동기화를 활성화하려면 대화형 통신을 만드는 동안 [마스터로 인쇄] 옵션을 선택합니다. 마스터로 인쇄 옵션을 선택하면 웹 채널의 컨텐츠, 상속 및 데이터 바인딩이 인쇄 채널에서 파생됩니다. 또한 인쇄 채널에서 수행한 변경 사항이 웹 채널에 반영되도록 합니다.

인쇄 채널을 사용하여 웹 채널 컨텐츠를 파생하려면 다음 단계를 수행하십시오.

1. AEM 작성자 인스턴스에 로그인하고 Adobe Experience Manager > **[!UICONTROL 양식]** > **[!UICONTROL 양식]** 및 **[!UICONTROL 문서로 이동합니다]**.
1. 만들기를 **누르고** 대화형 **통신을 선택합니다**. 대화형 **통신 만들기** 마법사가 표시됩니다.
1. 제목 및 이름 **필드에 create_first_ic****를** **지정합니다** . 양식 **데이터 모델로 FDM_Create_First_IC를** 선택하고 다음을 **누릅니다**.
1. 채널 **마법사에서** 다음을 수행합니다.

   1. 인쇄 템플릿으로 **create_first_ic_print_template** 을 지정하고 선택을 **누릅니다**.

   1. [웹 **채널에 대해 마스터로 인쇄 사용] 확인란을** 선택합니다.
   1. Create_ **First_IC_templates** 폴더 > **Create_First_IC_Web_Template** 을 웹 템플릿으로 지정하고 선택을 **탭합니다**.

   1. 만들기를 **누릅니다**.
   대화형 통신이 성공적으로 만들어졌다는 확인 메시지가 표시됩니다.

1. 편집을 **눌러** 오른쪽 창에서 대화형 통신을 엽니다.
1. 인쇄 채널용 [대화형 통신 만들기 섹션의 6-15단계를](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-print-channel) 실행합니다.
1. 왼쪽 **창에서 채널** 탭을 누르고 **웹을 눌러** 인쇄 채널에서 웹 채널에 대한 컨텐츠를 자동으로 생성합니다.
1. 4단계에서 **[웹 채널에 대해 마스터로 인쇄** 사용] 확인란을 선택하면 컨텐츠 및 바인딩이 인쇄 채널에서 웹 채널에 대해 자동으로 생성됩니다.

   인쇄 채널 컨텐츠는 웹 채널 템플릿 컨텐츠 아래에 삽입됩니다. 인쇄 채널에서 자동으로 생성된 웹 채널 컨텐츠를 수정하려면 대상 영역에 대한 상속을 취소할 수 있습니다.

   웹 채널에서 관련 대상 영역 위로 마우스를 가져간 후 ![상속](assets/cancelinheritance.png) 취소(상속 취소)를 선택한 다음 상속 **취소 대화** 상자에서 예를 **탭합니다**.

   ![상속 취소](assets/cancel_inheritance_web_channel_new.png)

   구성 요소의 상속을 취소한 경우 다시 활성화할 수 있습니다. 상속을 다시 활성화하려면 구성 요소를 포함하는 관련 대상 영역의 경계를 가리키고 ![상속을](assets/reenableinheritance.png)탭합니다.

1. 왼쪽 **창에서** 콘텐트 탭을 선택합니다.
1. 컨텐츠 트리를 사용하여 자동 생성된 웹 채널 컨텐츠를 웹 템플릿의 기존 패널에 드래그하여 놓습니다. 다음은 다시 정렬해야 하는 구성 요소 목록입니다.

   * 청구 상세내역 구성 요소를 청구 상세내역 패널에 추가
   * 고객 세부 정보 패널에 대한 고객 세부 사항 구성 요소
   * 청구 요약 구성 요소를 청구 요약 패널에 추가
   * 비용 구성 요소 요약에서 비용 패널 요약
   * 항목별 호출 패널에 대한 레이아웃 조각(테이블)
   ![웹 컨텐츠 트리](assets/ic_web_content_tree_new.png)

1. 웹 채널에 [대한 대화형 통신 만들기](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-web-channel) 13 - 18단계를 반복하여 대화형 **커뮤니케이션의 웹 채널에** 지금 **지불 및** 구독하이퍼링크를 삽입합니다.

