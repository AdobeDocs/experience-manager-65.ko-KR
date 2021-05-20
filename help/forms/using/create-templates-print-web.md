---
title: '"자습서:템플릿 만들기"'
seo-title: 대화형 커뮤니케이션용 인쇄 및 웹 템플릿 만들기
description: 대화형 커뮤니케이션용 인쇄 및 웹 템플릿 만들기
seo-description: 대화형 커뮤니케이션용 인쇄 및 웹 템플릿 만들기
uuid: 22256a61-bcf6-4b02-9ee6-0ffb1cc20a6e
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 879ff6ca-e5f3-451d-acc2-f75142101ddd
docset: aem65
feature: 대화형 통신
exl-id: bef1f05e-aea2-433e-b3d5-0b7ad8163fa7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1814'
ht-degree: 0%

---

# 자습서:템플릿 만들기{#tutorial-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

이 자습서는 [첫 번째 대화형 통신 만들기](/help/forms/using/create-your-first-interactive-communication.md) 시리즈의 단계입니다. 전체 자습서 사용 사례를 이해하고, 수행하고, 시연하기 위해 시리즈를 시간 순서대로 따르는 것이 좋습니다.

대화형 커뮤니케이션을 만들려면 인쇄 및 웹 채널용 AEM 서버에서 사용할 수 있는 템플릿이 있어야 합니다.

인쇄 채널의 템플릿은 Adobe Forms Designer에서 만들고 AEM 서버에 업로드됩니다. 그런 다음 대화형 커뮤니케이션을 만드는 동안 이러한 템플릿을 사용할 수 있습니다.

웹 채널에 대한 템플릿은 AEM에서 만들어집니다. 템플릿 작성자 및 관리자는 웹 템플릿을 만들고, 편집하고, 활성화할 수 있습니다. 만들고 활성화하면 대화형 커뮤니케이션을 만드는 동안 이러한 템플릿을 사용할 수 있습니다.

이 자습서에서는 대화형 커뮤니케이션을 만드는 동안 사용할 수 있도록 인쇄 및 웹 채널용 템플릿을 만드는 단계를 안내합니다. 이 자습서를 마치면 다음을 수행할 수 있습니다.

* Adobe Forms 디자이너를 사용하여 인쇄 채널용 XDP 템플릿 만들기
* AEM Forms 서버에 XDP 템플릿 업로드
* 웹 채널용 템플릿 만들기 및 활성화

## 인쇄 채널 {#create-template-for-print-channel}에 사용할 템플릿 만들기

다음 작업을 사용하여 Interactive Communication의 인쇄 채널에 대한 템플릿을 생성 및 관리합니다.

* [Forms 디자이너를 사용하여 XDP 템플릿 만들기](../../forms/using/create-templates-print-web.md#create-xdp-template-using-forms-designer)
* [AEM Forms 서버에 XDP 템플릿 업로드](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server)
* [레이아웃 조각용 XDP 템플릿 만들기](../../forms/using/create-templates-print-web.md#create-xdp-template-for-layout-fragments)

### Forms 디자이너를 사용하여 XDP 템플릿 만들기 {#create-xdp-template-using-forms-designer}

[사용 사례](/help/forms/using/create-your-first-interactive-communication.md) 및 [해부학](/help/forms/using/planning-interactive-communications.md)을 기반으로 XDP 템플릿에서 다음 하위 양식을 만듭니다.

* 청구 상세내역:문서 조각 포함
* 고객 세부 정보:문서 조각 포함
* 청구 요약:문서 조각 포함
* 요약:문서 조각(전하 하위 폼) 및 차트(하위 폼 차트)를 포함합니다
* 항목화된 호출:표(레이아웃 조각)를 포함합니다
* 지금 지불:이미지 포함
* 부가 가치 서비스:이미지 포함

![create_print_template](assets/create_print_template.gif)

이러한 하위 양식은 XDP 파일을 Forms 서버에 업로드한 후 인쇄 템플릿에서 대상 영역으로 표시됩니다. 문서 조각, 차트, 레이아웃 조각 및 이미지와 같은 모든 엔티티는 대화형 커뮤니케이션을 작성하는 동안 대상 영역에 추가됩니다.

다음 단계를 실행하여 인쇄 채널용 XDP 템플릿을 만듭니다.

1. Forms 디자이너를 열고 **파일** > **새로 만들기** > **빈 양식 사용,** **다음**&#x200B;을 탭한 다음, **완료**&#x200B;를 탭하여 템플릿을 만들 양식을 엽니다.

   **Window** 메뉴에서 **개체 라이브러리** 및 **개체** 옵션이 선택되어 있는지 확인합니다.

1. **개체 라이브러리**&#x200B;에서 **하위 양식** 구성 요소를 폼으로 끌어다 놓습니다.
1. 오른쪽 창의 **개체** 창에 하위 양식의 옵션을 표시하려면 하위 폼을 선택합니다.
1. **하위 양식** 탭을 선택하고 **콘텐츠** 드롭다운 목록에서 **흐름**&#x200B;을 선택합니다. 하위 양식의 왼쪽 끝점을 드래그하여 길이를 조정합니다.
1. **바인딩** 탭에서 다음을 수행합니다.

   1. **이름** 필드에 **BillDetails**&#x200B;를 지정합니다.

   1. **데이터 바인딩** 드롭다운 목록에서 **데이터 바인딩 없음**&#x200B;을 선택합니다.

   ![디자이너 하위 양식](assets/forms_designer_subform_new.png)

1. 마찬가지로 루트 하위 양식을 선택하고 **하위 양식** 탭을 선택한 다음 **콘텐츠** 드롭다운 목록에서 **흐름**&#x200B;을 선택합니다. **바인딩** 탭에서 다음을 수행합니다.

   1. **이름** 필드에 **TelecaBill**&#x200B;을 지정합니다.

   1. **데이터 바인딩** 드롭다운 목록에서 **데이터 바인딩 없음**&#x200B;을 선택합니다.

   ![인쇄 템플릿용 하위 양식](assets/root_subform_print_template_new.png)

1. 2 - 5단계를 반복하여 다음 하위 양식을 만듭니다.

   * 청구 상세내역
   * 고객 세부 사항
   * 청구 요약
   * 요약 - **하위 양식** 탭을 선택하고 **이 하위 양식의 컨텐츠** 드롭다운 목록에서 **위치함**&#x200B;을 선택합니다. **Summary** 하위 양식에 다음 하위 폼을 삽입합니다.

      * 요금
      * 차트
   * ItemisedCalls
   * 지금 지불
   * ValueAddedServices

   시간을 절약하기 위해 기존 하위 양식을 복사하여 붙여넣어 새 하위 양식을 만들 수도 있습니다.

   **Charts** 하위 폼을 Charts 하위 폼의 오른쪽으로 이동하려면 왼쪽 창에서 **Charts** 하위 폼을 선택하고 **Layout** 탭을 선택한 다음 **AnchorX** 필드에 값을 지정합니다. 값은 **Charts** 하위 양식의 **Width** 필드 값보다 커야 합니다. **비용** 하위 양식을 선택하고 **레이아웃** 탭을 선택하여 **너비** 필드의 값을 봅니다.

1. **개체 라이브러리**&#x200B;에서 **Text** 개체를 폼으로 끌어다 놓고 **Dial XXXX를 입력하여 상자에** 텍스트를 구독합니다.
1. 왼쪽 창에서 텍스트 개체를 마우스 오른쪽 단추로 클릭하고 **개체 이름 바꾸기**&#x200B;를 선택한 다음 텍스트 개체의 이름을 **가입**&#x200B;으로 입력합니다.

   ![XDP 템플릿](assets/print_xdp_template_subform_new.png)

1. **파일** > **다른 이름으로 저장**&#x200B;을 선택하여 로컬 파일 시스템에 파일을 저장합니다.

   1. 파일을 저장할 위치로 이동하여 이름을 **create_first_ic_print_template**&#x200B;로 지정합니다.
   1. **다른 이름으로 저장 유형** 드롭다운 목록에서 **.xdp** 을 선택합니다.

   1. **저장**&#x200B;을 누릅니다.

### XDP 템플릿을 AEM Forms 서버 {#upload-xdp-template-to-the-aem-forms-server}에 업로드합니다.

Forms 디자이너를 사용하여 XDP 템플릿을 만든 후에는 대화형 커뮤니케이션을 만드는 동안 템플릿을 사용할 수 있도록 AEM Forms 서버에 업로드해야 합니다.

1. **[!UICONTROL Forms]** > **[!UICONTROL Forms 및 문서]**&#x200B;를 선택합니다.
1. **만들기** > **파일 업로드**&#x200B;를 누릅니다.

   **create_first_ic_print_template** 템플릿(XDP)을 탐색하고 선택하고 **열기**&#x200B;를 탭하여 XDP 템플릿을 AEM Forms 서버로 가져옵니다.

### 레이아웃 조각 {#create-xdp-template-for-layout-fragments}에 대한 XDP 템플릿 만들기

대화형 커뮤니케이션의 인쇄 채널에 대한 레이아웃 조각을 만들려면 Forms 디자이너를 사용하여 XDP를 만들고 AEM Forms 서버에 업로드합니다.

1. Forms 디자이너를 열고 **파일** > **새로 만들기** > **빈 양식 사용,** **다음**&#x200B;을 탭한 다음, **완료**&#x200B;를 탭하여 템플릿을 만들 양식을 엽니다.

   **Window** 메뉴에서 **개체 라이브러리** 및 **개체** 옵션이 선택되어 있는지 확인합니다.

1. **Object Library**&#x200B;에서 **Table** 구성 요소를 양식에 드래그하여 놓습니다.
1. 테이블 삽입 대화 상자에서 다음을 수행합니다.

   1. 열 수를 **5**&#x200B;로 지정합니다.
   1. 본문 행 수를 **1**&#x200B;로 지정합니다.
   1. **표에 머리글 행 포함** 확인란을 선택합니다.
   1. **OK** 탭입니다.

1. **Table** 1 옆의 왼쪽 창에서 **+**&#x200B;을 탭하고 **Cell1**&#x200B;을 마우스 오른쪽 단추로 클릭한 다음 **개체 이름 바꾸기**&#x200B;를 **Date**&#x200B;로 선택합니다.

   마찬가지로 **Cell2**, **Cell3**, **Cell4** 및 **Cell5**&#x200B;의 이름을 **Time**, **Number**, **Duration** 및 **각각** 로 바꾸십시오.

1. **디자이너 보기**&#x200B;에서 머리글 텍스트 필드를 클릭하고 **시간**, **숫자**, **기간** 및 **비용**&#x200B;으로 이름을 바꾸십시오.

   ![레이아웃 조각](assets/layout_fragment_print_new.png)

1. 왼쪽 창에서 **행 1**&#x200B;을 선택하고 **개체** > **바인딩** > **각 데이터 항목에 대해 행 반복**&#x200B;을 선택합니다.

   ![레이아웃 조각에 대한 속성 반복](assets/layout_fragment_print_repeat_new.png)

1. **개체 라이브러리**&#x200B;에서 **디자이너 보기**&#x200B;로 **텍스트 필드** 구성 요소를 드래그하여 놓습니다.

   ![레이아웃 조각의 텍스트 필드](assets/layout_fragment_print_text_field_new.png)

   마찬가지로 **텍스트 필드** 구성 요소를 **Time**, **숫자**, **기간** 및 **비용** 행에 끌어다 놓습니다.

1. **파일** > **다른 이름으로 저장**&#x200B;을 선택하여 로컬 파일 시스템에 파일을 저장합니다.

   1. 파일을 저장할 위치로 이동하여 이름을 **table_lf**&#x200B;로 지정합니다.
   1. **다른 이름으로 저장 유형** 드롭다운 목록에서 **.xdp** 을 선택합니다.

   1. **저장**&#x200B;을 누릅니다.
   Forms 디자이너를 사용하여 레이아웃 조각용 XDP 템플릿을 만들면 레이아웃 조각을 만드는 동안 템플릿을 사용할 수 있도록 [업로드](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server)해야 AEM Forms 서버에 업로드합니다.

## 웹 채널 {#create-template-for-web-channel}에 대한 템플릿 만들기

다음 작업을 사용하여 Interactive Communication 웹 채널의 템플릿을 생성 및 관리합니다.

* [템플릿용 폴더 만들기](../../forms/using/create-templates-print-web.md#create-folder-for-templates)
* [템플릿 만들기](../../forms/using/create-templates-print-web.md#create-the-template)
* [템플릿 활성화](../../forms/using/create-templates-print-web.md#enable-the-template)
* [대화형 커뮤니케이션에서 단추 활성화](../../forms/using/create-templates-print-web.md#enabling-buttons-in-interactive-communications)

### 템플릿 {#create-folder-for-templates} 폴더 만들기

웹 채널 템플릿을 만들려면 만든 템플릿을 저장할 수 있는 폴더를 정의합니다. 해당 폴더 내에 템플릿을 만들면 양식 사용자가 템플릿을 기반으로 대화형 커뮤니케이션의 웹 채널을 만들 수 있도록 템플릿을 활성화합니다.

다음 단계를 실행하여 편집 가능한 템플릿의 폴더를 만듭니다.

1. **도구** ![망치-아이콘](assets/hammer-icon.svg) > **구성 브라우저**&#x200B;를 누릅니다.
   * 자세한 내용은 [구성 브라우저](/help/sites-administering/configurations.md) 설명서를 참조하십시오.
1. 구성 브라우저 페이지에서 **만들기**&#x200B;를 누릅니다.
1. **구성 만들기** 대화 상자에서 **Create_First_IC_templates**&#x200B;를 폴더의 제목으로 지정하고 **편집 가능한 템플릿**&#x200B;을 선택하고 **만들기**&#x200B;를 탭합니다.

   ![웹 템플릿 구성](assets/create_first_ic_web_template_new.png)

   **Create_First_IC_templates** 폴더가 생성되고 **구성 브라우저** 페이지에 나열됩니다.

### 템플릿 {#create-the-template} 만들기

[사용 사례](/help/forms/using/create-your-first-interactive-communication.md) 및 [해부학](/help/forms/using/planning-interactive-communications.md)을 기반으로 웹 템플릿에서 다음 패널을 만듭니다.

* 청구 상세내역:문서 조각 포함
* 고객 세부 정보:문서 조각 포함
* 청구 요약:문서 조각 포함
* 비용 요약:문서 조각 및 차트(두 열 레이아웃)를 포함합니다.
* 항목화된 호출:표 포함
* 지금 지불:**지금 지불** 단추와 이미지를 포함합니다
* 부가 가치 서비스:이미지와 **가입** 단추가 포함되어 있습니다.

![create_web_template](assets/create_web_template.gif)

대화형 커뮤니케이션을 만드는 동안 문서 조각, 차트, 표, 이미지 및 단추와 같은 모든 엔티티가 추가됩니다.

다음 단계를 실행하여 **Create_First_IC_templates** 폴더에서 웹 채널에 대한 템플릿을 만듭니다.

1. **도구** > **템플릿** > **Create_First_IC_templates** 폴더를 선택하여 해당 템플릿 폴더로 이동합니다.
1. **만들기**&#x200B;를 누릅니다.
1. **템플릿 유형 선택** 구성 마법사에서 **대화형 통신 - 웹 채널**&#x200B;을 선택하고 **다음**&#x200B;을 탭합니다.
1. **템플릿 세부 정보** 구성 마법사에서 **Create_First_IC_Web_Template**&#x200B;을 템플릿 제목으로 지정합니다. 선택적 설명을 지정하고 **만들기**&#x200B;를 누릅니다.

   **Create_First_IC_Web_Template**&#x200B;이 표시된다는 확인 메시지가 표시됩니다.

1. **열기**&#x200B;를 눌러 템플릿 편집기에서 템플릿을 엽니다.
1. **미리 보기** 옵션 옆에 있는 드롭다운 목록에서 **초기 컨텐츠**&#x200B;를 선택합니다.

   ![템플릿 편집기](assets/template_editor_initial_content_new.png)

1. **루트 패널**&#x200B;을 탭한 다음, **+**&#x200B;를 탭하여 템플릿에 추가할 수 있는 구성 요소 목록을 봅니다.
1. 목록에서 **패널**&#x200B;을 선택하여 **루트 패널** 위에 패널을 추가합니다.
1. 왼쪽 창에서 **Content** 탭을 선택합니다. 8단계에서 추가된 새 패널은 컨텐츠 트리의 **루트 패널** 아래에 표시됩니다.

   ![컨텐츠 트리](assets/content_tree_root_panel_new.png)

1. 패널을 선택하고 ![configure_icon](assets/configure_icon.png) (구성)을 누릅니다.
1. 속성 창에서 다음을 수행합니다.

   1. 이름 필드에 **bildetails**&#x200B;를 지정합니다.
   1. 제목 필드에 **Bill Details**&#x200B;를 지정합니다.
   1. **열 수** 드롭다운 목록에서 **1**&#x200B;을 선택합니다.

   1. 속성을 저장하려면 ![](/help/forms/using/assets/done_icon.png) 을 누릅니다.

   패널의 이름이 컨텐츠 트리에서 **Bill Details**&#x200B;로 업데이트됩니다.

1. 템플릿에 다음 속성을 사용하는 패널을 추가하려면 7~11단계를 반복합니다.

   | 이름 | 제목 | 열 수 |
   |---|---|---|
   | customerdetails | 고객 세부 사항 | 1 |
   | 청구 요약 | 청구서 요약 | 3 |
   | 요약 요금 | 비용 요약 | 2 |
   | itemedcalls | 항목화된 호출 | 3 |
   | paynow | 지금 지불 | 2개 |
   | vas | 부가 가치 서비스 | 3 |

   다음 이미지는 템플릿에 모든 패널을 추가한 후 컨텐츠 트리를 나타냅니다.

   ![모든 패널의 컨텐츠 트리](assets/content_tree_all_panels_new.png)

### 템플릿 {#enable-the-template} 활성화

웹 템플릿을 만든 후에는 대화형 커뮤니케이션을 만드는 동안 템플릿을 사용할 수 있도록 설정해야 합니다.

다음 단계를 실행하여 웹 템플릿을 활성화합니다.

1. **도구** ![해머아이콘](assets/hammer-icon.svg) > **템플릿**&#x200B;을 탭합니다.
1. **Create_First_IC_Web_Template** 템플릿으로 이동하여 **활성화**&#x200B;를 탭합니다.
1. **다시 활성화 를 클릭하여 확인합니다.**

   템플릿이 활성화되고 해당 상태가 사용으로 표시됩니다. 웹 채널용 대화형 커뮤니케이션을 만드는 동안 이 템플릿을 사용할 수 있습니다.

### 대화형 통신 {#enabling-buttons-in-interactive-communications}에서 단추 활성화

사용 사례를 기반으로 Interactive Communication에 **지금 지불** 및 **가입** 단추(적응형 양식 구성 요소)를 포함해야 합니다. Interactive Communication에서 이러한 단추를 사용하려면 다음 단계를 실행합니다.

1. **미리 보기** 옵션 옆에 있는 드롭다운 목록에서 **구조**&#x200B;를 선택합니다.
1. 컨텐츠 트리를 사용하여 **문서 컨테이너** 루트 패널을 선택하고 **정책**&#x200B;을 눌러 대화형 커뮤니케이션에서 사용할 수 있는 구성 요소를 선택합니다.

   ![정책 구성](assets/structure_configure_policy_new.png)

1. **속성** 섹션의 **허용된 구성 요소** 탭에서 **적응형 양식** 구성 요소에서 **단추**&#x200B;를 선택합니다.

   ![허용된 구성 요소](assets/allowed_components_af_new.png)

1. ![done_icon](assets/done_icon.png) 을 탭하여 속성을 저장합니다.
