---
title: "자습서: 템플릿 만들기"
description: 대화형 통신을 위한 인쇄 및 웹 템플릿 만들기
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
exl-id: bef1f05e-aea2-433e-b3d5-0b7ad8163fa7
source-git-commit: fd8bb7d3d9040e0a7a6b2f65751445f41aeab73e
workflow-type: tm+mt
source-wordcount: '1819'
ht-degree: 0%

---

# 자습서: 템플릿 만들기{#tutorial-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

이 튜토리얼의 단계는 다음과 같습니다. [첫 번째 대화형 통신 만들기](/help/forms/using/create-your-first-interactive-communication.md) 시리즈. 전체 자습서 사용 사례를 이해하고, 수행하고, 시연하려면 연대순으로 시리즈를 따르는 것이 좋습니다.

대화형 통신을 만들려면 인쇄 및 웹 채널에 대해 AEM 서버에서 사용할 수 있는 템플릿이 있어야 합니다.

인쇄 채널의 템플릿은 Adobe Forms Designer에서 만들고 AEM 서버에 업로드합니다. 그런 다음 대화형 통신을 만드는 동안 이러한 템플릿을 사용할 수 있습니다.

웹 채널에 대한 템플릿은 AEM에서 만들어집니다. 템플릿 작성자 및 관리자는 웹 템플릿을 만들고 편집하고 활성화할 수 있습니다. 이러한 템플릿을 만들고 활성화하면 대화형 통신을 만드는 동안 사용할 수 있습니다.

이 자습서에서는 대화형 통신을 만드는 동안 사용할 수 있도록 인쇄 및 웹 채널용 템플릿을 만드는 단계를 안내합니다. 이 자습서를 마치면 다음을 수행할 수 있습니다.

* Adobe Forms Designer를 사용하여 인쇄 채널용 XDP 템플릿 만들기
* AEM Forms 서버에 XDP 템플릿 업로드
* 웹 채널에 대한 템플릿 만들기 및 활성화

## 인쇄 채널용 템플릿 만들기 {#create-template-for-print-channel}

다음 작업을 사용하여 대화형 통신의 인쇄 채널용 템플릿을 만들고 관리합니다.

* [Forms Designer를 사용하여 XDP 템플릿 만들기](../../forms/using/create-templates-print-web.md#create-xdp-template-using-forms-designer)
* [AEM Forms 서버에 XDP 템플릿 업로드](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server)
* [레이아웃 단편용 XDP 템플릿 만들기](../../forms/using/create-templates-print-web.md#create-xdp-template-for-layout-fragments)

### Forms Designer를 사용하여 XDP 템플릿 만들기 {#create-xdp-template-using-forms-designer}

를 기반으로 함 [사용 사례](/help/forms/using/create-your-first-interactive-communication.md) 및 [해부학](/help/forms/using/planning-interactive-communications.md), XDP 템플릿에서 다음 하위 양식을 만듭니다.

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

1. Forms Designer를 열고 를 선택합니다. **파일** > **신규** > **빈 양식 사용,** 누르기 **다음**&#x200B;을 누른 다음 을 누릅니다 **완료** 템플릿을 만들기 위해 양식을 엽니다.

   다음을 확인합니다. **개체 라이브러리** 및 **오브젝트** 옵션이에서 선택됨 **창** 메뉴 아래의 제품에서 사용할 수 있습니다.

1. 을(를) 드래그 앤 드롭합니다 **하위 양식** 의 구성 요소 **개체 라이브러리** 을 양식으로 변환.
1. 하위 양식에 대한 옵션을에서 확인할 수 있도록 하위 양식을 선택합니다. **오브젝트** 오른쪽 창의 창입니다.
1. 다음 항목 선택 **하위 양식** 탭하고 선택 **흘림** 다음에서 **콘텐츠** 드롭다운 목록입니다. 길이를 조정하려면 하위 양식의 왼쪽 끝점을 드래그합니다.
1. 다음에서 **바인딩** 탭:

   1. 지정 **청구서 세부 정보** 다음에서 **이름** 필드.

   1. 선택 **데이터 바인딩 없음** 다음에서 **데이터 바인딩** 드롭다운 목록입니다.

   ![디자이너 하위 양식](assets/forms_designer_subform_new.png)

1. 마찬가지로 루트 하위 양식을 선택하고 **하위 양식** 탭을 클릭하고 다음을 선택합니다 **흘림** 다음에서 **콘텐츠** 드롭다운 목록입니다. 다음에서 **바인딩** 탭:

   1. 지정 **통신 요금** 다음에서 **이름** 필드.

   1. 선택 **데이터 바인딩 없음** 다음에서 **데이터 바인딩** 드롭다운 목록입니다.

   ![인쇄 서식 파일용 하위 양식](assets/root_subform_print_template_new.png)

1. 2~5단계를 반복하여 다음 하위 양식을 만듭니다.

   * 청구서 세부 정보
   * 고객 세부 정보
   * 청구 요약
   * 요약 - 선택 **하위 양식** 탭하고 선택 **위치함** 다음에서 **콘텐츠** 이 하위 양식의 드롭다운 목록입니다. 에 다음 하위 양식 삽입 **요약** 하위 양식.

      * 청구
      * 차트

   * ItemisedCalls
   * PayNow
   * ValueAddedServices

   시간을 절약하기 위해 기존 하위 양식을 복사하여 붙여 넣어 추가 하위 양식을 만들 수도 있습니다.

   을(를) 이동하려면 **차트** [비용] 하위 양식 오른쪽에 있는 하위 양식을 선택하고 **차트** 왼쪽 창에서 하위 양식을 선택하고 **레이아웃** 탭을 클릭하고 값을 지정합니다. **앵커X** 필드. 값은 의 값보다 커야 합니다. **폭** 필드 **청구** 하위 양식. 다음 항목 선택 **청구** 하위 양식 및 선택 **레이아웃** 탭으로 이동하여 **폭** 필드.

1. 을(를) 드래그 앤 드롭합니다 **텍스트** 의 오브젝트 **개체 라이브러리** 을(를) 양식에 입력하고 **가입하려면 XXXX로 전화 걸기** 상자에 있는 텍스트입니다.
1. 왼쪽 창에서 텍스트 개체를 마우스 오른쪽 단추로 클릭하고 **개체 이름 바꾸기**&#x200B;를 누르고 텍스트 객체의 이름을 다음과 같이 입력합니다. **구독**.

   ![XDP 템플릿](assets/print_xdp_template_subform_new.png)

1. 선택 **파일** > **다른 이름으로 저장** 파일을 로컬 파일 시스템에 저장하려면 다음을 수행합니다.

   1. 파일을 저장할 수 있는 위치로 이동하여 이름을 로 지정합니다. **create_first_ic_print_template**.
   1. 선택 **.xdp** 다음에서 **유형으로 저장** 드롭다운 목록입니다.

   1. 누르기 **저장**.

### AEM Forms 서버에 XDP 템플릿 업로드 {#upload-xdp-template-to-the-aem-forms-server}

Forms Designer를 사용하여 XDP 템플릿을 만든 후에는 대화형 통신을 만드는 동안 템플릿을 사용할 수 있도록 템플릿을 AEM Forms 서버에 업로드해야 합니다.

1. 선택 **[!UICONTROL Forms]** > **[!UICONTROL Forms 및 문서]**.
1. 누르기 **만들기** > **파일 업로드**.

   다음 위치로 이동하여 선택합니다. **create_first_ic_print_template** 템플릿(XDP) 및 탭 **열기** AEM Forms 서버로 XDP 템플릿을 가져옵니다.

### 레이아웃 단편용 XDP 템플릿 만들기 {#create-xdp-template-for-layout-fragments}

대화형 통신의 인쇄 채널에 대한 레이아웃 조각을 만들려면 Forms Designer를 사용하여 XDP를 만들고 AEM Forms 서버에 업로드하십시오.

1. Forms Designer를 열고 를 선택합니다. **파일** > **신규** > **빈 양식 사용,** 누르기 **다음**&#x200B;을 누른 다음 을 누릅니다 **완료** 템플릿을 만들기 위해 양식을 엽니다.

   다음을 확인합니다. **개체 라이브러리** 및 **오브젝트** 옵션이에서 선택됨 **창** 메뉴 아래의 제품에서 사용할 수 있습니다.

1. 을(를) 드래그 앤 드롭합니다 **표** 의 구성 요소 **개체 라이브러리** 을 양식으로 변환.
1. 표 삽입 대화 상자에서 다음을 수행합니다.

   1. 열 수를 다음으로 지정 **5**.
   1. 본문 행 수를 다음으로 지정 **1**.
   1. 다음 항목 선택 **표에 머리글 행 포함** 확인란.
   1. 탭 **확인**.

1. 누르기 **+** 왼쪽 창에서 **표** 1 및 마우스 오른쪽 버튼 클릭 **Cell1** 및 선택 **개체 이름 바꾸기** 끝 **날짜**.

   마찬가지로 이름 바꾸기 **Cell2**, **Cell3**, **셀4**, 및 **셀5** 끝 **시간**, **숫자**, **기간**, 및 **청구** 각각.

1. 에서 머리글 텍스트 필드를 클릭합니다. **디자이너 보기** 이름을 로 변경합니다. **시간**, **숫자**, **기간**, 및 **청구**.

   ![레이아웃 단편](assets/layout_fragment_print_new.png)

1. 선택 **행 1** 왼쪽 창에서 다음을 선택합니다. **오브젝트** > **바인딩** > **각 데이터 항목에 대해 행 반복**.

   ![레이아웃 단편에 대한 반복 속성](assets/layout_fragment_print_repeat_new.png)

1. 을(를) 드래그 앤 드롭합니다 **텍스트 필드** 의 구성 요소 **개체 라이브러리** (으)로 **디자이너 보기**.

   ![레이아웃 단편의 텍스트 필드](assets/layout_fragment_print_text_field_new.png)

   마찬가지로 를 드래그 앤 드롭합니다. **텍스트 필드** 구성 요소를 **시간**, **숫자**, **기간**, 및 **청구** 행.

1. 선택 **파일** > **다른 이름으로 저장** 파일을 로컬 파일 시스템에 저장하려면 다음을 수행합니다.

   1. 파일을 저장할 수 있는 위치로 이동하여 이름을 로 지정합니다. **table_lf**.
   1. 선택 **.xdp** 다음에서 **유형으로 저장** 드롭다운 목록입니다.

   1. 누르기 **저장**.

   Forms Designer를 사용하여 레이아웃 조각에 대한 XDP 템플릿을 만들었으면 다음을 수행해야 합니다. [업로드](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server) 레이아웃 조각을 만드는 동안 템플릿을 사용할 수 있도록 AEM Forms 서버에 연결합니다.

## 웹 채널용 템플릿 만들기 {#create-template-for-web-channel}

다음 작업을 사용하여 대화형 통신의 웹 채널용 템플릿을 만들고 관리합니다.

* [템플릿을 위한 폴더 만들기](../../forms/using/create-templates-print-web.md#create-folder-for-templates)
* [템플릿 만들기](../../forms/using/create-templates-print-web.md#create-the-template)
* [템플릿 활성화](../../forms/using/create-templates-print-web.md#enable-the-template)
* [대화형 통신에서 단추 활성화](../../forms/using/create-templates-print-web.md#enabling-buttons-in-interactive-communications)

### 템플릿을 위한 폴더 만들기 {#create-folder-for-templates}

웹 채널 템플릿을 만들려면 만든 템플릿을 저장할 수 있는 폴더를 정의합니다. 해당 폴더 내에 템플릿을 만든 후에는 해당 템플릿을 활성화하여 양식 사용자가 템플릿을 기반으로 대화형 통신의 웹 채널을 만들 수 있도록 합니다.

편집 가능한 템플릿을 위한 폴더를 만들려면 다음 작업을 수행하십시오.

1. 누르기 **도구** ![망치 아이콘](assets/hammer-icon.svg) > **구성 브라우저**.
   * 다음을 참조하십시오. [구성 브라우저](/help/sites-administering/configurations.md) 설명서 를 참조하십시오.
1. 구성 브라우저 페이지에서 을 누릅니다. **만들기**.
1. 다음에서 **구성 만들기** 대화 상자, 지정 **Create_First_IC_templates** 폴더의 제목으로 을 선택합니다. **편집 가능한 템플릿**, 및 탭 **만들기**.

   ![웹 템플릿 구성](assets/create_first_ic_web_template_new.png)

   다음 **Create_First_IC_templates** 폴더가 만들어지고 목록에 **구성 브라우저** 페이지를 가리키도록 업데이트하는 중입니다.

### 템플릿 만들기 {#create-the-template}

를 기반으로 함 [사용 사례](/help/forms/using/create-your-first-interactive-communication.md) 및 [해부학](/help/forms/using/planning-interactive-communications.md)웹 템플릿에서 다음 패널을 만듭니다.

* 청구 상세내역: 문서 단편 포함
* 고객 세부 정보: 문서 단편 포함
* 청구 요약: 문서 단편 포함
* 비용 요약: 문서 단편 및 차트(2열 레이아웃) 포함
* 항목별 호출: 테이블을 포함합니다.
* 지금 결제: 포함 **지금 결제** 버튼과 이미지
* 부가 가치 서비스: 이미지 및 **구독** 단추를 클릭합니다.

![create_web_template](assets/create_web_template.gif)

문서 조각, 차트, 테이블, 이미지, 단추 등 모든 엔티티는 대화형 통신을 생성하는 동안 추가됩니다.

웹 채널용 템플릿을 만들려면 **Create_First_IC_templates** 폴더에서 다음 단계를 수행합니다.

1. 다음을 선택하여 해당 템플릿 폴더로 이동합니다. **도구** > **템플릿** > **Create_First_IC_templates** 폴더를 삭제합니다.
1. **만들기**&#x200B;를 탭합니다.
1. 다음에서 **템플릿 유형 선택** 구성 마법사, 선택 **대화형 통신 - 웹 채널** 및 탭 **다음**.
1. 다음에서 **템플릿 세부 정보** 구성 마법사, 지정 **Create_First_IC_Web_Template** 를 템플릿 제목으로 사용하십시오. 선택적 설명을 지정하고 을 누릅니다 **만들기**.

   다음을 포함하는 확인 메시지: **Create_First_IC_Web_Template** 이 표시됩니다.

1. 누르기 **열기** 템플릿 편집기에서 템플릿을 엽니다.
1. 선택 **초기 컨텐츠** 다음 옆에 있는 드롭다운 목록에서 **미리 보기** 옵션을 선택합니다.

   ![템플릿 편집기](assets/template_editor_initial_content_new.png)

1. 누르기 **루트 패널** 그런 다음 을 누릅니다 **+** 템플릿에 추가할 수 있는 구성 요소 목록을 봅니다.
1. 패널을 위에 추가하려면 **루트 패널**, 선택 **패널** 목록에서 삭제할 수 있습니다.
1. 다음 항목 선택 **콘텐츠** 왼쪽 창의 탭. 8단계에서 추가된 새 패널은 **루트 패널** 콘텐츠 트리에서.

   ![콘텐츠 트리](assets/content_tree_root_panel_new.png)

1. 패널을 선택하고 을 누릅니다 ![configure_icon](assets/configure_icon.png) (구성).
1. 속성 창에서 다음을 수행합니다.

   1. 지정 **청구 세부 정보** 이름 필드에서 참조할 수 있습니다.
   1. 지정 **청구 세부 정보** 제목 필드에서 참조할 수 있습니다.
   1. 선택 **1** 다음에서 **열 수** 드롭다운 목록입니다.

   1. 속성을 저장하려면 을 누릅니다 ![저장](/help/forms/using/assets/done_icon.png).

   패널 이름이 로 업데이트됩니다. **청구 세부 정보** 콘텐츠 트리에서.

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

1. 누르기 **도구** ![망치 아이콘](assets/hammer-icon.svg) > **템플릿**.
1. 다음 위치로 이동 **Create_First_IC_Web_Template** 템플릿을 선택하고 탭합니다. **사용**.
1. 누르기 **사용** 다시 한 번 확인해 보십시오.

   템플릿이 활성화되고 상태가 활성화됨으로 표시됩니다. 웹 채널용 대화형 통신을 만드는 동안 이 템플릿을 사용할 수 있습니다.

### 대화형 통신에서 단추 활성화 {#enabling-buttons-in-interactive-communications}

사용 사례를 기반으로 다음을 포함해야 합니다. **지금 결제** 및 **구독** 인터랙티브 통신의 버튼(적응형 양식 구성 요소). Interactive Communication에서 이러한 단추를 사용하려면 다음을 수행합니다.

1. 선택 **구조** 다음 옆에 있는 드롭다운 목록에서 **미리 보기** 옵션을 선택합니다.
1. 다음 항목 선택 **문서 컨테이너** 콘텐츠 트리를 사용한 루트 패널 및 탭 **정책** 대화형 통신에서 사용할 수 있는 구성 요소를 선택합니다.

   ![정책 구성](assets/structure_configure_policy_new.png)

1. 다음에서 **허용된 구성 요소** 의 탭 **속성** 섹션, 선택 **단추** 다음에서 **적응형 양식** 구성 요소.

   ![허용된 구성 요소](assets/allowed_components_af_new.png)

1. 속성을 저장하려면 을 누릅니다 ![저장](assets/done_icon.png).
