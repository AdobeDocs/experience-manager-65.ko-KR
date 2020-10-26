---
title: '"자습서:템플릿 만들기"'
seo-title: 인터랙티브한 커뮤니케이션을 위한 인쇄 및 웹 템플릿 제작
description: 인터랙티브한 커뮤니케이션을 위한 인쇄 및 웹 템플릿 제작
seo-description: 인터랙티브한 커뮤니케이션을 위한 인쇄 및 웹 템플릿 제작
uuid: 22256a61-bcf6-4b02-9ee6-0ffb1cc20a6e
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 879ff6ca-e5f3-451d-acc2-f75142101ddd
docset: aem65
translation-type: tm+mt
source-git-commit: ce64b148ba96cc64670aaf96c1b201bafa282b98
workflow-type: tm+mt
source-wordcount: '1812'
ht-degree: 0%

---


# 자습서:템플릿 만들기{#tutorial-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

이 자습서는 첫 번째 [대화형 통신](/help/forms/using/create-your-first-interactive-communication.md) 시리즈 만들기의 단계입니다. 전체 자습서 사용 사례를 이해하고, 실행하고, 시연하려면 연순의 순서로 시리즈를 따르는 것이 좋습니다.

대화형 통신을 만들려면 AEM 서버에서 인쇄 및 웹 채널용 템플릿을 사용할 수 있어야 합니다.

인쇄 채널의 템플릿은 Adobe Forms 디자이너에서 만들고 AEM 서버에 업로드됩니다. 그런 다음 대화형 통신을 만드는 동안 이러한 템플릿을 사용할 수 있습니다.

웹 채널의 템플릿은 AEM에서 만듭니다. 템플릿 작성자 및 관리자는 웹 템플릿을 만들고 편집하고 활성화할 수 있습니다. 작성 및 활성화된 템플릿은 대화형 통신을 만드는 동안 사용할 수 있습니다.

이 자습서에서는 대화형 통신을 만드는 동안 사용할 수 있도록 인쇄 및 웹 채널용 템플릿을 만드는 단계를 안내합니다. 이 튜토리얼의 끝에서 다음 작업을 수행할 수 있습니다.

* Adobe Forms 디자이너를 사용하여 인쇄 채널용 XDP 템플릿 만들기
* XDP 템플릿을 AEM Forms 서버에 업로드
* 웹 채널에 대한 템플릿 만들기 및 활성화

## 인쇄 채널용 템플릿 만들기 {#create-template-for-print-channel}

다음 작업을 사용하여 인터랙티브 커뮤니케이션의 인쇄 채널용 템플릿을 만들고 관리할 수 있습니다.

* [Forms 디자이너를 사용하여 XDP 템플릿 만들기](../../forms/using/create-templates-print-web.md#create-xdp-template-using-forms-designer)
* [AEM Forms 서버에 XDP 템플릿 업로드](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server)
* [레이아웃 조각에 대한 XDP 템플릿 만들기](../../forms/using/create-templates-print-web.md#create-xdp-template-for-layout-fragments)

### Forms 디자이너를 사용하여 XDP 템플릿 만들기 {#create-xdp-template-using-forms-designer}

사용 사례 [및](/help/forms/using/create-your-first-interactive-communication.md) 구조에 [](/help/forms/using/planning-interactive-communications.md)따라 XDP 템플릿에서 다음 하위 양식을 만듭니다.

* 청구 상세내역:문서 조각 포함
* 고객 세부 정보:문서 조각 포함
* 청구 요약:문서 조각 포함
* 요약:문서 조각(요금 하위 폼) 및 차트(차트 하위 폼) 포함
* 항목별 호출:표 포함(레이아웃 조각)
* 지금 지불:이미지 포함
* 부가 가치 서비스:이미지 포함

![create_print_template](assets/create_print_template.gif)

이러한 하위 양식은 XDP 파일을 Forms 서버에 업로드한 후 인쇄 템플릿에서 타겟 영역으로 표시됩니다. 문서 조각, 차트, 레이아웃 조각 및 이미지와 같은 모든 개체가 인터랙티브 커뮤니케이션을 만드는 동안 대상 영역에 추가됩니다.

인쇄 채널용 XDP 템플릿을 만들려면 다음 단계를 수행하십시오.

1. Forms 디자이너를 열고 **파일** > **새로 만들기** > **빈 양식** 사용 **을 선택하고 다음****** 을 탭한 다음 Finish를 탭한 다음 템플릿을 만들 양식을 엽니다.

   [창] 메뉴에서 **개체 라이브러리** 및 **개체** 옵션 **을** 선택해야합니다.

1. 개체 라이브러리에서 **하위** 폼 구성 요소를 **폼으로** 드래그하여 놓습니다.
1. 오른쪽 창의 **개체** 창에 하위 폼의 옵션을 표시하려면 하위 폼을 선택합니다.
1. 하위 **폼** 탭 **을 선택하고** 콘텐츠 **드롭다운 목록에서** 흐름을선택합니다. 하위 폼의 왼쪽 끝점을 드래그하여 길이를 조정합니다.
1. 바인딩 **탭에서 다음을** 수행합니다.

   1. 이름 **필드에 BillDetails** 를 **지정합니다** .

   1. 데이터 **바인딩** 드롭다운 목록에서 **데이터 바인딩** 없음을선택합니다.

   ![디자이너 하위 폼](assets/forms_designer_subform_new.png)

1. 마찬가지로 루트 하위 양식을 선택하고 하위 **폼** 탭을 선택한 다음 **콘텐츠** 드롭다운 목록에서 **** Prohed를선택합니다. 바인딩 **탭에서 다음을** 수행합니다.

   1. 이름 **필드에 텔레카** 빌을 **지정합니다** .

   1. 데이터 **바인딩** 드롭다운 목록에서 **데이터 바인딩** 없음을선택합니다.

   ![인쇄 템플릿용 하위 폼](assets/root_subform_print_template_new.png)

1. 2 - 5단계를 반복하여 다음 하위 양식을 만듭니다.

   * BillDetails
   * 고객 세부 사항
   * BillSummary
   * 요약 - 하위 **폼** 탭 **을** 선택하고 **이 하위** 폼의콘텐츠 드롭다운 목록에서 위치를선택합니다. 요약 하위 양식에 다음 하위 **양식을** 삽입합니다.

      * 요금
      * 차트
   * ItemisedCalls
   * PayNow
   * ValueAddedServices

   시간을 절약하기 위해 기존 하위 양식을 복사하여 붙여넣어 새 하위 양식을 만들 수도 있습니다.

   차트 **** 를 [비용] 오른쪽의 **오른쪽으로 이동하려면 왼쪽 창에서** 차트 **를 선택하고 [** 레이아웃 **] 탭을 선택한 다음, AnchorX 하위 폼 하위 폼 필드 값을** 지정합니다. 값은 Charts 하위 폼의 **Width** 필드 값보다 **커야** 합니다. Charts **하위** 폼 **을** 선택하고 **레이아웃** 탭을 선택하여Width필드 값을봅니다.

1. 개체 라이브러리에서 **텍스트** 개체를 드래그하여 **폼으로** 끌어 **놓고** 전화 접속 XXXX를 입력하여 상자에 텍스트를 구독합니다.
1. 왼쪽 창에서 텍스트 개체를 마우스 오른쪽 단추로 클릭하고 **개체**&#x200B;이름 변경을 선택한 다음 텍스트 개체의 이름을 **구독으로 입력합니다**.

   ![XDP 템플릿](assets/print_xdp_template_subform_new.png)

1. 파일 **** > **다른 이름으로** 저장을 선택하여 로컬 파일 시스템에 파일을 저장합니다.

   1. 파일을 저장할 위치로 이동하고 이름을 **create_first_ic_print_template로 지정합니다**.
   1. 다른 **이름으로** **저장 유형** 드롭다운 목록에서.xdp를 선택합니다.

   1. 저장을 **누릅니다**.

### AEM Forms 서버에 XDP 템플릿 업로드 {#upload-xdp-template-to-the-aem-forms-server}

Forms 디자이너를 사용하여 XDP 템플릿을 만든 후, 대화형 통신을 만드는 동안 템플릿을 사용할 수 있도록 AEM Forms 서버에 업로드해야 합니다.

1. [ **[!UICONTROL Forms]** ] > [ **[!UICONTROL Forms 및 문서]를 선택합니다]**.
1. 만들기 **> 파일** **업로드를**&#x200B;누릅니다.

   XDP( **create_first_ic_print_template** 템플릿)를 탐색하여 선택하고 **열기를** 눌러 XDP 템플릿을 AEM Forms 서버로 가져옵니다.

### 레이아웃 조각에 대한 XDP 템플릿 만들기 {#create-xdp-template-for-layout-fragments}

대화형 커뮤니케이션의 인쇄 채널에 대한 레이아웃 조각을 만들려면 Forms 디자이너를 사용하여 XDP를 만들고 AEM Forms 서버에 업로드합니다.

1. Forms 디자이너를 열고 **파일** > **새로 만들기** > **빈 양식** 사용 **을 선택하고 다음****** 을 탭한 다음 Finish를 탭한 다음 템플릿을 만들 양식을 엽니다.

   [창] 메뉴에서 **개체 라이브러리** 및 **개체** 옵션 **을** 선택해야합니다.

1. 개체 라이브러리의 **표** 구성 요소를 **폼으로** 드래그하여 놓습니다.
1. 표 삽입 대화 상자에서 다음을 수행합니다.

   1. 열 수를 **5로 지정합니다**.
   1. 본문 행 수를 **1로 지정합니다**.
   1. 테이블에 **머리글 행 포함 확인란을** 선택합니다.
   1. Tab **OK**.

1. 표1 옆에 있는 왼쪽 창 **에서** **셀** 1 **을 마우스 오른쪽 단추로 클릭하고** 개체 이름 바꾸기를 **** ****&#x200B;선택하여 FacebookDate를 선택합니다.

   유사하게, Cell2 **,** Cell3 **,** Cell4 **, Cell4**, Cell5 To Time **** **************** Rename, Rename Time, Rename Number, Vertising Number, Duration Duration, and CompaniesCharts 각각.

1. 디자이너 보기에서 **[** 디자이너 보기 **]를 클릭하고 이름을 변경하여**&#x200B;시간 **,**&#x200B;번호 **,**&#x200B;기간 **,**&#x200B;기간, 및HeaderCharts로 변경합니다.

   ![레이아웃 조각](assets/layout_fragment_print_new.png)

1. 왼쪽 창에서 **행 1을** 선택하고 **개체** > **바인딩** ****> 각 데이터 항목에 대해반복 행을 선택합니다.

   ![레이아웃 조각에 대한 반복 속성](assets/layout_fragment_print_repeat_new.png)

1. 개체 라이브러리의 **텍스트 필드** 구성 요소를 **디자이너** 보기 **로**&#x200B;드래그하여놓습니다.

   ![레이아웃 조각에 대한 텍스트 필드](assets/layout_fragment_print_text_field_new.png)

   마찬가지로 **텍스트 필드** 구성 요소를 **시간**, **숫자**, 지속 시간 **,****** 및ChartsRows 행에 드래그하여 놓습니다.

1. 파일 **** > **다른 이름으로** 저장을 선택하여 로컬 파일 시스템에 파일을 저장합니다.

   1. 파일을 저장할 위치로 이동하고 이름을 **table_lf로 지정합니다**.
   1. 다른 **이름으로** **저장 유형** 드롭다운 목록에서.xdp를 선택합니다.

   1. 저장을 **누릅니다**.
   Forms 디자이너를 사용하여 레이아웃 조각에 대한 XDP 템플릿을 만든 후에는 레이아웃 조각을 만드는 동안 템플릿을 사용할 수 있도록 AEM Forms 서버에 [업로드해야](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server) 합니다.

## 웹 채널용 템플릿 만들기 {#create-template-for-web-channel}

다음 작업을 사용하여 인터랙티브 커뮤니케이션의 웹 채널에 대한 템플릿을 만들고 관리할 수 있습니다.

* [템플릿 폴더 만들기](../../forms/using/create-templates-print-web.md#create-folder-for-templates)
* [템플릿 만들기](../../forms/using/create-templates-print-web.md#create-the-template)
* [템플릿 활성화](../../forms/using/create-templates-print-web.md#enable-the-template)
* [인터랙티브 커뮤니케이션에서 단추 활성화](../../forms/using/create-templates-print-web.md#enabling-buttons-in-interactive-communications)

### 템플릿 폴더 만들기 {#create-folder-for-templates}

웹 채널 템플릿을 만들려면 만든 템플릿을 저장할 수 있는 폴더를 정의합니다. 해당 폴더 내에 템플릿을 만들면 양식 사용자가 템플릿을 기반으로 대화형 커뮤니케이션의 웹 채널을 만들 수 있도록 템플릿을 활성화합니다.

편집 가능한 템플릿의 폴더를 만들려면 다음 단계를 수행하십시오.

1. 도구 **망치** 아이콘 ![>](assets/hammer-icon.svg) 구성 브라우저 **를 누릅니다**.
   * See the [Configuration Browser](/help/sites-administering/configurations.md) documentation for more information.
1. 구성 브라우저 페이지에서 만들기를 **누릅니다**.
1. 구성 **만들기 대화** 상자에서 **Create_First_IC_templates** 를 폴더 **의 제목으로 지정하고 편집 가능한 템플릿**&#x200B;을 선택한 다음 **만들기를**&#x200B;누릅니다.

   ![웹 템플릿 구성](assets/create_first_ic_web_template_new.png)

   Create_ **First_IC_templates** 폴더가 생성되어 **구성 브라우저** 페이지에 나열됩니다.

### 템플릿 만들기 {#create-the-template}

사용 [사례](/help/forms/using/create-your-first-interactive-communication.md) 및 [구조에](/help/forms/using/planning-interactive-communications.md)따라 웹 템플릿에서 다음 패널을 만듭니다.

* 청구 상세내역:문서 조각 포함
* 고객 세부 정보:문서 조각 포함
* 청구 요약:문서 조각 포함
* 비용 요약:문서 조각 및 차트(두 열 레이아웃) 포함
* 항목별 호출:표 포함
* 지금 지불:지금 **지불** 단추 및 이미지 포함
* 부가 가치 서비스:이미지와 [구독] **단추를** 포함합니다.

![create_web_template](assets/create_web_template.gif)

대화형 통신을 만드는 동안 문서 조각, 차트, 표, 이미지 및 버튼과 같은 모든 개체가 추가됩니다.

다음 단계를 실행하여 Create_First_IC_templates **** 폴더에서 웹 채널에 대한 템플릿을 생성합니다.

1. 도구 > 템플릿 **>** 만들기 **>** Create **_First_IC_templates** 폴더를 선택하여 해당 템플릿 폴더로 이동합니다.
1. 만들기를 **누릅니다**.
1. 템플릿 유형 **선택** 구성 마법사에서 **대화형 통신 - 웹 채널** 을 선택하고 **다음을**&#x200B;누릅니다.
1. 템플릿 **세부 사항** 구성 마법사에서 **Create_First_IC_Web_Template** 을 템플릿 제목으로 지정합니다. 선택적 설명을 지정하고 만들기를 **누릅니다**.

   Create_First_ **IC_Web_Template이 표시된다는** 확인 메시지가 표시됩니다.

1. 열기 **를** 눌러 템플릿 편집기에서 템플릿을 엽니다.
1. 미리 **보기** 옵션 옆에 있는 드롭다운 목록에서 **초기 컨텐츠를** 선택합니다.

   ![템플릿 편집기](assets/template_editor_initial_content_new.png)

1. [ **루트 패널** ]을 누른 다음 **+** 을 눌러 템플릿에 추가할 수 있는 구성 요소 목록을 봅니다.
1. 목록에서 **패널** 을 선택하여 **루트 패널**&#x200B;위에 패널을 추가합니다.
1. 왼쪽 창에서 **콘텐트** 탭을 선택합니다. 8단계에서 추가된 새 패널은 컨텐츠 트리의 **루트 패널** 아래에 표시됩니다.

   ![컨텐츠 트리](assets/content_tree_root_panel_new.png)

1. 패널을 선택하고 ![configure_icon](assets/configure_icon.png) (구성)을 누릅니다.
1. 속성 창에서:

   1. 이름 **필드에 청구** 정보를 지정합니다.
   1. 제목 **필드에 청구 상세내역을** 지정합니다.
   1. 열 수 **드롭다운** 목록에서 **1을** 선택합니다.

   1. 속성을 ![](/help/forms/using/assets/done_icon.png) 저장하려면 을 누릅니다.

   패널의 이름이 컨텐츠 트리의 **청구 세부** 사항으로 업데이트됩니다.

1. 템플릿에 다음 속성이 있는 패널을 추가하려면 7 - 11단계를 반복합니다.

   | 이름 | 제목 | 열 수 |
   |---|---|---|
   | 고객 정보 | 고객 세부 정보 | 1 |
   | 청구 요약 | 청구 요약 | 1 |
   | 요약 수수료 | 비용 요약 | 2 |
   | itemisedcalls | 항목별 호출 | 1 |
   | paynow | 지금 지불 | 2 |
   | vas | 부가 가치 서비스 | 1 |

   다음 이미지는 템플릿에 모든 패널을 추가한 후 컨텐츠 트리를 보여 줍니다.

   ![모든 패널의 컨텐츠 트리](assets/content_tree_all_panels_new.png)

### 템플릿 활성화 {#enable-the-template}

웹 템플릿을 만든 후에는 대화형 통신을 만드는 동안 템플릿을 사용하도록 설정해야 합니다.

웹 템플릿을 활성화하려면 다음 단계를 실행합니다.

1. 도구 **망치** 아이콘 ![> 템플릿](assets/hammer-icon.svg) 을 **누릅니다**.
1. Create_ **First_IC_Web_Template** 템플릿으로 이동하여 선택한 다음 활성화를 **누릅니다**.
1. Tab **다시** 활성화하여 확인합니다.

   템플릿이 활성화되고 상태는 활성화됨으로 표시됩니다. 웹 채널에 대한 대화형 통신을 만드는 동안 이 템플릿을 사용할 수 있습니다.

### 인터랙티브 커뮤니케이션에서 단추 활성화 {#enabling-buttons-in-interactive-communications}

사용 사례에 따라 Interactive Communication에 **지금** 지불 및 **구독** 버튼(적응형 양식 구성 요소)을 포함해야 합니다. 대화형 통신에서 이러한 단추를 사용할 수 있도록 하려면 다음 단계를 수행하십시오.

1. 미리 **보기** 옵션 옆의 드롭다운 목록에서 **구조를** 선택합니다.
1. 컨텐츠 트리를 사용하여 **문서 컨테이너** 루트 패널을 선택하고 **정책을** 눌러 대화형 통신에서 사용할 수 있는 구성 요소를 선택합니다.

   ![정책 구성](assets/structure_configure_policy_new.png)

1. 속성 **의** 허용된 구성 요소 ******탭** 의 응용 **양식 구성 요소** 구성 요소에서단추를선택합니다.

   ![허용된 구성 요소](assets/allowed_components_af_new.png)

1. done_icon ![을](assets/done_icon.png) 눌러 속성을 저장합니다.