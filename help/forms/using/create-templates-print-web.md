---
title: "자습서: 템플릿 만들기"
description: 대화형 통신을 위한 인쇄 및 웹 템플릿 만들기
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
exl-id: bef1f05e-aea2-433e-b3d5-0b7ad8163fa7
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1790'
ht-degree: 1%

---

# 자습서: 템플릿 만들기{#tutorial-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

이 자습서는 [첫 번째 대화형 통신 만들기](/help/forms/using/create-your-first-interactive-communication.md) 시리즈의 단계입니다. 전체 자습서 사용 사례를 이해하고, 수행하고, 시연하려면 연대순으로 시리즈를 따르는 것이 좋습니다.

대화형 통신을 만들려면 인쇄 및 웹 채널에 대해 AEM 서버에서 사용할 수 있는 템플릿이 있어야 합니다.

인쇄 채널의 템플릿은 Forms Designer Adobe에서 만들어 AEM 서버에 업로드됩니다. 그런 다음 대화형 통신을 만드는 동안 이러한 템플릿을 사용할 수 있습니다.

웹 채널에 대한 템플릿은 AEM에서 만들어집니다. 템플릿 작성자 및 관리자는 웹 템플릿을 만들고 편집하고 활성화할 수 있습니다. 이러한 템플릿을 만들고 활성화하면 대화형 통신을 만드는 동안 사용할 수 있습니다.

이 자습서에서는 대화형 통신을 만드는 동안 사용할 수 있도록 인쇄 및 웹 채널용 템플릿을 만드는 단계를 안내합니다. 이 자습서를 마치면 다음을 수행할 수 있습니다.

* Forms Designer Adobe을 사용하여 인쇄 채널용 XDP 템플릿 만들기
* AEM Forms 서버에 XDP 템플릿 업로드
* 웹 채널에 대한 템플릿 만들기 및 활성화

## 인쇄 채널용 템플릿 만들기 {#create-template-for-print-channel}

다음 작업을 사용하여 대화형 통신의 인쇄 채널용 템플릿을 만들고 관리합니다.

* [Forms Designer을 사용하여 XDP 템플릿 만들기](../../forms/using/create-templates-print-web.md#create-xdp-template-using-forms-designer)
* [AEM Forms 서버에 XDP 템플릿 업로드](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server)
* [레이아웃 단편용 XDP 템플릿 만들기](../../forms/using/create-templates-print-web.md#create-xdp-template-for-layout-fragments)

### Forms Designer을 사용하여 XDP 템플릿 만들기 {#create-xdp-template-using-forms-designer}

[사용 사례](/help/forms/using/create-your-first-interactive-communication.md) 및 [구조](/help/forms/using/planning-interactive-communications.md)를 기반으로 XDP 템플릿에서 다음 하위 양식을 만드십시오.

* 청구 상세내역: 문서 단편 포함
* 고객 세부 정보: 문서 단편 포함
* 청구 요약: 문서 단편 포함
* 요약: 문서 단편(비용 하위 양식) 및 차트(차트 하위 양식)가 포함됩니다.
* 항목별 호출: 테이블(레이아웃 단편)을 포함합니다.
* 지금 결제: 이미지 포함
* 부가 가치 서비스: 이미지 포함

![create_print_template](assets/create_print_template.gif)

이러한 하위 양식은 XDP 파일을 Forms 서버에 업로드한 후 인쇄 템플릿의 대상 영역으로 표시됩니다. 문서 조각, 차트, 레이아웃 조각 및 이미지와 같은 모든 엔티티는 대화형 통신을 생성하는 동안 대상 영역에 추가됩니다.

인쇄 채널용 XDP 템플릿을 만들려면 다음 작업을 수행하십시오.

1. Forms Designer을 열고 **파일** > **새로 만들기** > **빈 양식 사용,** **다음**&#x200B;을 선택한 다음 **마침**&#x200B;을 선택하여 템플릿 만들기 양식을 엽니다.

   **창** 메뉴에서 **개체 라이브러리** 및 **개체** 옵션이 선택되어 있는지 확인하십시오.

1. **개체 라이브러리**&#x200B;에서 **하위 양식** 구성 요소를 양식으로 드래그 앤 드롭하십시오.
1. 오른쪽 창의 **개체** 창에서 하위 양식에 대한 옵션을 볼 수 있도록 하위 양식을 선택하십시오.
1. **하위 양식** 탭을 선택하고 **콘텐츠** 드롭다운 목록에서 **흐름**&#x200B;을(를) 선택합니다. 길이를 조정하려면 하위 양식의 왼쪽 끝점을 드래그합니다.
1. **바인딩** 탭에서:

   1. **이름** 필드에 **BillDetails**&#x200B;을(를) 지정하십시오.

   1. **데이터 바인딩** 드롭다운 목록에서 **데이터 바인딩 없음**&#x200B;을 선택합니다.

   ![Designer 하위 양식](assets/forms_designer_subform_new.png)

1. 마찬가지로 루트 하위 양식을 선택하고 **하위 양식** 탭을 선택한 다음 **콘텐츠** 드롭다운 목록에서 **흐름**&#x200B;을 선택합니다. **바인딩** 탭에서:

   1. **이름** 필드에 **TelecaBill**&#x200B;을(를) 지정하십시오.

   1. **데이터 바인딩** 드롭다운 목록에서 **데이터 바인딩 없음**&#x200B;을 선택합니다.

   ![인쇄 서식 파일용 하위 양식](assets/root_subform_print_template_new.png)

1. 2~5단계를 반복하여 다음 하위 양식을 만듭니다.

   * 청구서 세부 정보
   * 고객 세부 정보
   * 청구 요약
   * 요약 - **하위 양식** 탭을 선택하고 이 하위 양식의 **콘텐츠** 드롭다운 목록에서 **위치**&#x200B;를 선택합니다. **요약** 하위 양식에 다음 하위 양식을 삽입합니다.

      * 청구
      * 차트

   * ItemisedCalls
   * PayNow
   * ValueAddedServices

   시간을 절약하기 위해 기존 하위 양식을 복사하여 붙여 넣어 추가 하위 양식을 만들 수도 있습니다.

   **Charts** 하위 양식을 Charges 하위 양식의 오른쪽으로 이동하려면 왼쪽 창에서 **Charts** 하위 양식을 선택하고 **Layout** 탭을 선택한 다음 **AnchorX** 필드의 값을 지정하십시오. 값은 **Charges** 하위 양식의 **Width** 필드 값보다 커야 합니다. **너비** 필드의 값을 볼 수 있도록 **청구** 하위 양식을 선택하고 **레이아웃** 탭을 선택하십시오.

1. **개체 라이브러리**&#x200B;에서 **Text** 개체를 양식으로 드래그 앤 드롭한 다음 상자에 **가입하려면 전화 걸기** 텍스트를 입력하십시오.
1. 왼쪽 창에서 텍스트 개체를 마우스 오른쪽 단추로 클릭하고 **개체 이름 바꾸기**&#x200B;를 선택한 다음 텍스트 개체의 이름을 **구독**(으)로 입력합니다.

   ![XDP 템플릿](assets/print_xdp_template_subform_new.png)

1. 로컬 파일 시스템에 파일을 저장하려면 **파일** > **다른 이름으로 저장**&#x200B;을 선택합니다.

   1. 파일을 저장할 수 있는 위치로 이동하여 이름을 **create_first_ic_print_template**(으)로 지정합니다.
   1. **다른 형식으로 저장** 드롭다운 목록에서 **.xdp**&#x200B;을(를) 선택합니다.

   1. **저장**&#x200B;을 선택합니다.

### AEM Forms 서버에 XDP 템플릿 업로드 {#upload-xdp-template-to-the-aem-forms-server}

Forms Designer을 사용하여 XDP 템플릿을 만든 후에는 대화형 통신을 만드는 동안 템플릿을 사용할 수 있도록 템플릿을 AEM Forms 서버에 업로드해야 합니다.

1. **[!UICONTROL Forms]** > **[!UICONTROL Forms 및 문서]**&#x200B;를 선택합니다.
1. **만들기** > **파일 업로드**&#x200B;를 선택합니다.

   **create_first_ic_print_template** 템플릿(XDP)으로 이동하여 선택한 다음 **열기**&#x200B;를 선택하여 XDP 템플릿을 AEM Forms 서버로 가져옵니다.

### 레이아웃 단편용 XDP 템플릿 만들기 {#create-xdp-template-for-layout-fragments}

대화형 통신의 인쇄 채널에 대한 레이아웃 조각을 만들려면 Forms Designer을 사용하여 XDP를 만들고 AEM Forms 서버에 업로드하십시오.

1. Forms Designer을 열고 **파일** > **새로 만들기** > **빈 양식 사용,** **다음**&#x200B;을 선택한 다음 **마침**&#x200B;을 선택하여 템플릿 만들기 양식을 엽니다.

   **창** 메뉴에서 **개체 라이브러리** 및 **개체** 옵션이 선택되어 있는지 확인하십시오.

1. **개체 라이브러리**&#x200B;에서 **테이블** 구성 요소를 양식으로 드래그 앤 드롭하십시오.
1. 표 삽입 대화 상자에서 다음을 수행합니다.

   1. 열 수를 **5**(으)로 지정하십시오.
   1. 본문 행 수를 **1**(으)로 지정하십시오.
   1. **표에 머리글 행 포함** 확인란을 선택합니다.
   1. **확인** 탭입니다.

1. **테이블** 1 옆의 왼쪽 창에서 **+**&#x200B;을(를) 선택하고 **셀1**&#x200B;을(를) 마우스 오른쪽 단추로 클릭한 다음 **개체 이름 바꾸기**&#x200B;를 선택하여 **날짜**&#x200B;를 선택합니다.

   마찬가지로 **Cell2**, **Cell3**, **Cell4**, **Cell5**&#x200B;의 이름을 각각 **Time**, **Number**, **Duration**, **Charges**&#x200B;로 바꾸십시오.

1. **Designer 보기**&#x200B;에서 머리글 텍스트 필드를 클릭하고 이름을 **Time**, **Number**, **Duration** 및 **Charges**&#x200B;로 바꾸십시오.

   ![레이아웃 단편](assets/layout_fragment_print_new.png)

1. 왼쪽 창에서 **행 1**&#x200B;을 선택하고 **개체** > **바인딩** > **각 데이터 항목에 대해 행 반복**&#x200B;을 선택합니다.

   ![레이아웃 단편에 대한 속성 반복](assets/layout_fragment_print_repeat_new.png)

1. **개체 라이브러리**&#x200B;에서 **Designer 보기**(으)로 **텍스트 필드** 구성 요소를 드래그 앤 드롭하십시오.

   ![레이아웃 단편의 텍스트 필드](assets/layout_fragment_print_text_field_new.png)

   마찬가지로 **텍스트 필드** 구성 요소를 **Time**, **Number**, **Duration** 및 **Charges** 행으로 끌어서 놓습니다.

1. 로컬 파일 시스템에 파일을 저장하려면 **파일** > **다른 이름으로 저장**&#x200B;을 선택합니다.

   1. 파일을 저장할 수 있는 위치로 이동하여 이름을 **table_lf**(으)로 지정하십시오.
   1. **다른 형식으로 저장** 드롭다운 목록에서 **.xdp**&#x200B;을(를) 선택합니다.

   1. **저장**&#x200B;을 선택합니다.

   Forms Designer을 사용하여 레이아웃 조각에 대한 XDP 템플릿을 만든 후에는 레이아웃 조각을 만드는 동안 템플릿을 사용할 수 있도록 템플릿을 AEM Forms 서버에 [업로드](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server)해야 합니다.

## 웹 채널용 템플릿 만들기 {#create-template-for-web-channel}

다음 작업을 사용하여 대화형 통신의 웹 채널용 템플릿을 만들고 관리합니다.

* [템플릿을 위한 폴더 만들기](../../forms/using/create-templates-print-web.md#create-folder-for-templates)
* [템플릿 만들기](../../forms/using/create-templates-print-web.md#create-the-template)
* [템플릿 활성화](../../forms/using/create-templates-print-web.md#enable-the-template)
* [대화형 통신에서 단추 활성화](../../forms/using/create-templates-print-web.md#enabling-buttons-in-interactive-communications)

### 템플릿을 위한 폴더 만들기 {#create-folder-for-templates}

웹 채널 템플릿을 만들려면 만든 템플릿을 저장할 수 있는 폴더를 정의합니다. 해당 폴더 내에 템플릿을 만든 후에는 해당 템플릿을 활성화하여 양식 사용자가 템플릿을 기반으로 대화형 통신의 웹 채널을 만들 수 있도록 합니다.

편집 가능한 템플릿을 위한 폴더를 만들려면 다음 작업을 수행하십시오.

1. **도구** ![hammer-icon](assets/hammer-icon.svg) > **구성 브라우저**&#x200B;를 선택합니다.
   * 자세한 내용은 [구성 브라우저](/help/sites-administering/configurations.md) 설명서를 참조하십시오.
1. [구성 브라우저] 페이지에서 **만들기**&#x200B;를 선택합니다.
1. **구성 만들기** 대화 상자에서 폴더의 제목으로 **Create_First_IC_templates**&#x200B;을(를) 지정하고 **편집 가능한 템플릿**&#x200B;을(를) 확인한 다음 **만들기**&#x200B;를 선택합니다.

   ![웹 템플릿 구성](assets/create_first_ic_web_template_new.png)

   **Create_First_IC_templates** 폴더가 만들어지고 **구성 브라우저** 페이지에 나열됩니다.

### 템플릿 만들기 {#create-the-template}

[사용 사례](/help/forms/using/create-your-first-interactive-communication.md) 및 [구조](/help/forms/using/planning-interactive-communications.md)를 기반으로 웹 템플릿에 다음 패널을 만드십시오.

* 청구 상세내역: 문서 단편 포함
* 고객 세부 정보: 문서 단편 포함
* 청구 요약: 문서 단편 포함
* 비용 요약: 문서 단편 및 차트(2열 레이아웃) 포함
* 항목별 호출: 테이블을 포함합니다.
* 지금 결제: **지금 결제** 단추 및 이미지 포함
* 부가 가치 서비스: 이미지 및 **구독** 버튼을 포함합니다.

![create_web_template](assets/create_web_template.gif)

문서 조각, 차트, 테이블, 이미지, 단추 등 모든 엔티티는 대화형 통신을 생성하는 동안 추가됩니다.

**Create_First_IC_templates** 폴더에 웹 채널의 템플릿을 만들려면 다음 단계를 수행하십시오.

1. **도구** > **템플릿** > **Create_First_IC_templates** 폴더를 선택하여 적절한 템플릿 폴더로 이동합니다.
1. **만들기**&#x200B;를 선택합니다.
1. **템플릿 유형 선택** 구성 마법사에서 **대화형 통신 - 웹 채널**&#x200B;을 선택하고 **다음**&#x200B;을 선택합니다.
1. **템플릿 세부 정보** 구성 마법사에서 **Create_First_IC_Web_Template**&#x200B;을(를) 템플릿 제목으로 지정합니다. 선택적 설명을 지정하고 **만들기**&#x200B;를 선택하십시오.

   **Create_First_IC_Web_Template**&#x200B;을(를) 확인하는 메시지가 표시됩니다.

1. 템플릿 편집기에서 템플릿을 열려면 **열기**&#x200B;를 선택합니다.
1. **미리 보기** 옵션 옆에 있는 드롭다운 목록에서 **초기 콘텐츠**&#x200B;를 선택합니다.

   ![템플릿 편집기](assets/template_editor_initial_content_new.png)

1. 템플릿에 추가할 수 있는 구성 요소 목록을 보려면 **루트 패널**&#x200B;을(를) 선택한 다음 **+**&#x200B;을(를) 선택하십시오.
1. **루트 패널** 위에 패널을 추가하려면 목록에서 **패널**&#x200B;을 선택하십시오.
1. 왼쪽 창에서 **콘텐츠** 탭을 선택합니다. 8단계에서 추가된 새 패널은 콘텐츠 트리의 **루트 패널** 아래에 표시됩니다.

   ![콘텐츠 트리](assets/content_tree_root_panel_new.png)

1. 패널을 선택하고 ![configure_icon](assets/configure_icon.png)(구성)을 선택합니다.
1. 속성 창에서 다음을 수행합니다.

   1. 이름 필드에 **billdetails**&#x200B;을(를) 지정합니다.
   1. 제목 필드에 **청구서 세부 정보**&#x200B;를 지정합니다.
   1. **열 수** 드롭다운 목록에서 **1**&#x200B;을(를) 선택합니다.

   1. 속성을 저장하려면 ![저장](/help/forms/using/assets/done_icon.png)을 선택합니다.

   패널 이름이 콘텐츠 트리에서 **청구서 세부 정보**(으)로 업데이트되었습니다.

1. 7 - 11단계를 반복하여 템플릿에 다음 속성이 있는 패널을 추가합니다.

   | 이름 | 제목 | 열 수 |
   |---|---|---|
   | customerdetails | 고객 세부 정보 | 1 |
   | billsummary | 청구 요약 | 1 |
   | 즉석 충전 | 청구 요약 | 2 |
   | itemisedcalls | 항목별 호출 | 1 |
   | paynow | 지금 결제 | 2 |
   | vas | 부가 가치 서비스 | 1 |

   다음 이미지는 모든 패널을 템플릿에 추가한 후의 콘텐츠 트리를 보여 줍니다.

   ![모든 패널의 콘텐츠 트리](assets/content_tree_all_panels_new.png)

### 템플릿 활성화 {#enable-the-template}

웹 템플릿을 만든 후에는 대화형 통신을 만드는 동안 해당 템플릿을 사용할 수 있도록 설정해야 합니다.

웹 템플릿을 활성화하려면 다음 작업을 수행하십시오.

1. **도구** ![망치 아이콘](assets/hammer-icon.svg) > **서식 파일**&#x200B;을 선택합니다.
1. **Create_First_IC_Web_Template** 템플릿으로 이동하여 선택한 다음 **활성화**&#x200B;를 선택합니다.
1. 확인하려면 **사용**&#x200B;을 다시 선택하십시오.

   템플릿이 활성화되고 상태가 활성화됨으로 표시됩니다. 웹 채널용 대화형 통신을 만드는 동안 이 템플릿을 사용할 수 있습니다.

### 대화형 통신에서 단추 활성화 {#enabling-buttons-in-interactive-communications}

사용 사례에 따라 대화형 통신에 **지금 결제** 및 **구독** 단추(적응형 양식 구성 요소)를 포함해야 합니다. Interactive Communication에서 이러한 단추를 사용하려면 다음을 수행합니다.

1. **미리 보기** 옵션 옆에 있는 드롭다운 목록에서 **구조**&#x200B;를 선택합니다.
1. 콘텐츠 트리를 사용하여 **문서 컨테이너** 루트 패널을 선택하고 **정책**&#x200B;을(를) 선택하여 대화형 통신에서 사용할 수 있는 구성 요소를 선택합니다.

   ![정책 구성](assets/structure_configure_policy_new.png)

1. **속성** 섹션의 **허용된 구성 요소** 탭에서 **적응형 양식** 구성 요소에서 **단추**&#x200B;를 선택합니다.

   ![허용된 구성 요소](assets/allowed_components_af_new.png)

1. 속성을 저장하려면 ![저장](assets/done_icon.png)을 선택하세요.
