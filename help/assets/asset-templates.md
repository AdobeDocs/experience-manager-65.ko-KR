---
title: 자산 템플릿
description: 에서 에셋 템플릿에 대해 알아보기 [!DNL Adobe Experience Manager Assets] 에셋 템플릿을 사용하여 마케팅 자료를 만드는 방법에 대해 알아봅니다.
contentOwner: AG
role: User
feature: Asset Management,Developer Tools
exl-id: 12c92aad-3a1d-486e-a830-31de2fc6d07b
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '1552'
ht-degree: 1%

---

# 자산 템플릿 {#asset-templates}

에셋 템플릿은 디지털 및 인쇄 미디어용 시각적으로 풍부한 콘텐츠를 신속하게 재활용할 수 있는 특별한 에셋 클래스입니다. 에셋 템플릿에는 고정 메시징 섹션과 편집 가능 섹션의 두 부분이 포함되어 있습니다. 고정 메시징 섹션에는 편집할 수 없는 브랜드 로고 및 저작권 정보와 같은 독점 콘텐츠가 포함될 수 있습니다. 편집 가능 섹션에는 메시징을 사용자 지정하기 위해 편집할 수 있는 필드에 시각적 및 텍스트 콘텐츠가 포함될 수 있습니다.

글로벌 사이니지의 보안을 유지하면서 제한적인 편집 작업을 할 수 있는 유연성은 자산 템플릿을 다양한 기능의 콘텐츠 아티팩트로 빠른 콘텐츠 적응 및 배포에 이상적인 빌딩 블록으로 만듭니다. 콘텐츠의 용도를 다시 지정하면 인쇄 및 디지털 채널 관리 비용을 절감하고 이러한 채널 전반에 걸쳐 전체적이고 일관된 환경을 제공할 수 있습니다.

마케터는 내에서 템플릿을 저장하고 관리할 수 있습니다. [!DNL Experience Manager Assets] 단일 기본 템플릿을 사용하여 개인화된 여러 인쇄 경험을 손쉽게 제작할 수 있습니다. 브로셔, 전단지, 엽서, 명함 등 다양한 유형의 마케팅 자료를 만들어 고객에게 마케팅 메시지를 잘 전달할 수 있습니다. 기존 또는 새 인쇄 출력에서 다중 페이지 인쇄 출력을 조합할 수도 있습니다. 무엇보다도 디지털 및 인쇄 환경을 동시에 쉽게 제공하여 사용자에게 일관되고 통합된 환경을 제공할 수 있습니다.

반면에 자산 템플릿은 대부분 [!DNL Adobe InDesign] 파일, 숙련도 [!DNL Adobe InDesign] 는 항성 아티팩트를 만드는 데 장애가 되지 않습니다. 의 필드를 매핑할 필요는 없습니다. [!DNL Adobe InDesign] 카탈로그를 만들 때 필요한 제품 필드가 있는 템플릿입니다. 웹 인터페이스에서 직접 WYSIWYG 모드로 템플릿을 편집할 수 있습니다. 단, 의 경우 [!DNL Adobe InDesign] 편집 변경 사항을 처리하려면 먼저 다음을 구성해야 합니다. [!DNL Experience Manager Assets] 을 와 통합하려면 [!DNL Adobe InDesign Server].

편집 기능 [!DNL Adobe InDesign] 웹 인터페이스의 템플릿은 크리에이티브 직원과 마케팅 직원 간의 협업을 강화하는 데 도움이 됩니다. 콘텐츠 속도가 증가하면 마케팅 자료의 마켓 출시 시간이 단축됩니다.

에셋 템플릿으로 다음을 수행할 수 있습니다.

* 웹 인터페이스에서 편집 가능한 템플릿 필드를 수정합니다.
* 태그 수준에서 글꼴 크기, 스타일 및 문자 등 텍스트의 기본 스타일을 제어합니다.
* 콘텐츠 선택기를 사용하여 템플릿 내에서 이미지를 변경합니다.
* 템플릿 편집 내용을 미리 봅니다.
* 여러 템플릿 파일을 병합하여 다중 페이지 아티팩트를 만듭니다.

담보에 대한 템플리트를 선택할 때 [!DNL Experience Manager Assets] 는 편집할 수 있는 템플릿의 사본을 만듭니다. 원본 템플릿은 그대로 유지되므로 글로벌 사이니지가 그대로 유지되고 브랜드 일관성을 유지하는 데 다시 사용할 수 있습니다.

상위 폴더 내에서 업데이트된 파일을 INDD, PDF 또는 JPG 형식으로 내보낼 수 있습니다. 이러한 형식의 출력을 로컬 파일 시스템에 다운로드할 수도 있습니다.

## 자료 만들기 {#creating-a-collateral}

예정된 캠페인에 대한 브로셔, 전단지 및 광고와 같은 디지털 인쇄 가능한 자료를 만들고 전 세계 아울렛 매장과 공유하는 시나리오를 생각해 보십시오. 템플릿을 기반으로 자료를 만들면 여러 채널에 통합된 고객 경험을 제공할 수 있습니다. 디자이너는 다음과 같은 크리에이티브 솔루션을 사용하여 캠페인 템플릿(단일 페이지 또는 다중 페이지)을 만들 수 있습니다. [!DNL InDesign] 및 템플릿 업로드 [!DNL Experience Manager Assets] 당신을 위해. 자료를 만들기 전에에 하나 이상의 INDD 템플릿을에 업로드하고에서 사용할 수 있도록 하십시오. [!DNL Experience Manager] 미리.

1. 위치 [!DNL Experience Manager] 인터페이스 클릭 [!UICONTROL 에셋].

1. 옵션에서 을 선택합니다. **[!UICONTROL 템플릿]**.

   ![chlimage_1-101](assets/chlimage_1-306.png)

1. 클릭 **[!UICONTROL 만들기]**&#x200B;을 클릭하고 메뉴에서 만들려는 자료를 선택합니다. 예를 들어, **[!UICONTROL 브로셔]**.

   ![chlimage_1-102](assets/chlimage_1-307.png)

1. 하나 이상의 INDD 템플릿을에 업로드하고에서 사용할 수 있습니다. [!DNL Experience Manager] 미리. 브로셔의 템플릿을 선택하고 **[!UICONTROL 다음]**.
1. 브로셔의 이름과 선택적 설명을 지정합니다.

   ![chlimage_1-104](assets/chlimage_1-309.png)

1. (선택 사항) **[!UICONTROL 태그]** 브로셔에 사용할 태그를 하나 이상 선택합니다. 클릭 **[!UICONTROL 확인]** 을 클릭하여 선택 항목을 확인합니다.
1. **[!UICONTROL 만들기]**&#x200B;를 클릭합니다. 대화 상자에서 새 브로셔가 생성되었음을 확인합니다. 클릭 **[!UICONTROL 열기]** 를 클릭하여 브로셔를 편집 모드로 엽니다.

   <!--![chlimage_1-106](assets/.png) -->

   또는 대화 상자를 닫고 시작한 템플릿 페이지의 폴더로 이동하여 작성한 브로셔를 확인합니다. 자료 유형이 카드 보기의 썸네일에 나타납니다. 예를 들어, 이 경우 [!UICONTROL 브로셔] 이 썸네일에 표시됩니다.

   ![chlimage_1-107](assets/chlimage_1-312.png)

## 자료 편집 {#editing-a-collateral}

담보를 생성한 후 바로 편집할 수 있습니다. 또는 [!UICONTROL 템플릿] 또는 에셋 페이지를 참조하십시오.

1. 편집할 자료를 열려면 다음 중 하나를 수행합니다.

   * 의 7단계에서 생성한 자료(이 경우 브로셔)를 엽니다. [자료 만들기](/help/assets/asset-templates.md#creating-a-collateral).
   * 템플릿 페이지에서 자료를 생성한 폴더로 이동한 다음 [!UICONTROL 편집] 보충 자료의 썸네일에 대한 빠른 조치.
   * 담보에 대한 자산 페이지에서 를 클릭합니다. **[!UICONTROL 편집]** 을 클릭합니다.
   * 자료를 선택하고 **[!UICONTROL 편집]** 을 클릭합니다.

   <!--![chlimage_1-108](assets/chlimage_1-313.png) -->

   에셋 파인더 및 텍스트 편집기는 페이지 왼쪽에 표시됩니다. 텍스트 편집기는 기본적으로 열려 있습니다.

   텍스트 편집기를 사용하여 텍스트 필드에 표시할 텍스트를 수정할 수 있습니다. 태그 수준에서 글꼴 크기, 스타일, 색상 및 문자를 수정할 수 있습니다.

   에셋 파인더를 사용하여 내에서 이미지를 찾아보거나 검색할 수 있습니다. [!DNL Experience Manager Assets] 템플릿에서 편집 가능한 이미지를 선택한 이미지로 바꿉니다.

   ![chlimage_1-109](assets/chlimage_1-314.png)

   편집 가능 항목이 오른쪽에 표시됩니다. 에서 편집할 수 있는 필드 [!DNL Experience Manager Assets]: 템플릿의 해당 필드에 태그를 지정해야 합니다. [!DNL InDesign]. 즉, 에서 편집 가능으로 표시되어야 합니다. [!DNL InDesign].

   >[!NOTE]
   >
   >다음을 확인합니다. [!DNL Experience Manager] 배포가 [!DNL InDesign Server] 활성화하려면 [!DNL Experience Manager Assets] 에서 데이터를 추출하려면 [!DNL InDesign] 템플릿을 사용하고 편집할 수 있도록 만듭니다. 자세한 내용은 [Experience Manager Assets과 InDesign Server 통합](/help/assets/indesign.md).

1. 편집 가능한 필드의 텍스트를 수정하려면 편집 가능한 필드 목록에서 텍스트 필드를 클릭하고 필드의 텍스트를 편집합니다.

   ![chlimage_1-111](assets/chlimage_1-316.png)

   제공된 옵션을 사용하여 글꼴 스타일, 색상 및 크기와 같은 텍스트 속성을 편집할 수 있습니다.

1. 클릭 **[!UICONTROL 미리 보기]** 텍스트 변경 내용을 미리 봅니다.

1. 이미지를 바꾸려면 **[!UICONTROL 자산 파인더]** ![chlimage_1-113](assets/chlimage_1-318.png).

1. 편집 가능한 필드 목록에서 이미지 필드를 선택한 다음 에셋 선택기에서 원하는 이미지를 편집 가능한 필드로 드래그합니다.

   ![chlimage_1-114](assets/chlimage_1-319.png)

   키워드, 태그 및 게시 상태를 기반으로 이미지를 검색할 수도 있습니다. 다음을 통해 검색할 수 있습니다. [!DNL Experience Manager Assets] 저장소를 탐색하고 원하는 이미지의 위치로 이동합니다.

   ![chlimage_1-115](assets/chlimage_1-320.png)

1. 클릭 **[!UICONTROL 미리 보기]** 이미지를 미리 봅니다.
1. 여러 페이지로 구성된 자료의 특정 페이지를 편집하려면 맨 아래에 있는 페이지 탐색기를 사용하십시오.

1. 클릭 **[!UICONTROL 미리 보기]** 을 클릭하여 모든 변경 내용을 미리 봅니다. 클릭 **[!UICONTROL 완료]** 를 클릭하여 편집 변경 사항을 자료에 저장합니다.

   >[!NOTE]
   >
   >자료 내의 편집 가능한 이미지 필드에 누락된 아이콘이 없는 경우에만 미리 보기 및 완료 옵션이 활성화됩니다. 담보에 누락된 아이콘이 있는 경우 다음과 같습니다. [!DNL Experience Manager] 에서 이미지를 확인할 수 없습니다. [!DNL InDesign] 템플릿. 일반적으로, [!DNL Experience Manager] 은(는) 다음 경우에 이미지를 확인할 수 없습니다.
   >
   >* 이미지가 기본 이미지에 포함되지 않음 [!DNL InDesign] 템플릿.
   >* 이미지는 로컬 파일 시스템에서 연결됩니다.
   >
   >활성화하려면 [!DNL Experience Manager] 이미지를 해결하려면 다음을 수행합니다.
   >
   >* 만드는 동안 이미지 포함 [!DNL InDesign] 템플릿(참조) [링크 및 포함된 그래픽 정보](https://helpx.adobe.com/indesign/using/graphics-links.html)).
   >* 마운트 [!DNL Experience Manager] 누락된 아이콘을 기존 에셋에 매핑합니다. [!DNL Experience Manager].
   >
   >작업에 대한 자세한 내용 [!DNL InDesign] 문서, 참조 [Experience Manager에서 InDesign 문서 작업 모범 사례](https://helpx.adobe.com/experience-manager/kb/best-practices-idd-docs-aem.html).

1. 브로셔에 대한 PDF 렌디션을 생성하려면 대화 상자에서 Acrobat 옵션을 선택한 다음 를 클릭합니다 **[!UICONTROL 계속]**.
1. 담보는 시작한 폴더에 생성됩니다. 렌디션을 보려면 자료를 열고 을 선택합니다 **[!UICONTROL 표현물]** GlobalNav 목록에서

   ![chlimage_1-118](assets/chlimage_1-323.png)

1. 렌디션 목록에서 PDF 렌디션을 클릭하여 PDF 파일을 다운로드합니다. PDF 파일을 열어 자료를 검토하십시오.

   ![chlimage_1-119](assets/chlimage_1-324.png)

## 자료 병합 {#merge-collateral}

1. 다음에서 [!DNL Experience Manager] 인터페이스 클릭 [!UICONTROL 에셋] 탐색 페이지에서 참조할 수 있습니다.

1. 옵션에서 을 선택합니다. **[!UICONTROL 템플릿]**.

1. 클릭 **[!UICONTROL 만들기]** 및 선택 **[!UICONTROL 병합]** 메뉴에서 삭제할 수 있습니다.

   ![chlimage_1-120](assets/chlimage_1-325.png)

1. 다음에서 [!UICONTROL 템플릿 병합] 페이지, 클릭 **[!UICONTROL 병합]** ![에셋 추가](assets/do-not-localize/assets_add_icon.png).

1. 병합할 담보의 위치로 이동하고 병합할 담보의 썸네일을 클릭하여 선택합니다.

   ![chlimage_1-122](assets/chlimage_1-327.png)

   Omnisearch 상자에서 템플릿을 검색할 수도 있습니다.

   다음을 통해 검색할 수 있습니다. [!DNL Experience Manager Assets] 리포지토리 또는 컬렉션을 선택하고 원하는 템플릿의 위치로 이동한 다음 병합할 템플릿을 선택합니다.

   다양한 필터를 적용하여 원하는 템플릿을 검색할 수 있습니다. 예를 들어 파일 유형 또는 태그를 기반으로 템플릿을 검색할 수 있습니다.

1. 클릭 **[!UICONTROL 다음]** 을 클릭합니다.
1. 다음에서 **[!UICONTROL 미리 보기 및 재정렬]** 화면을 표시하고 필요한 경우 템플릿을 다시 정렬한 다음 병합할 템플릿 선택을 미리 봅니다. 그런 다음 을 클릭합니다. **[!UICONTROL 다음]** 을 클릭합니다.

   ![chlimage_1-126](assets/chlimage_1-331.png)

1. 다음에서 [!UICONTROL 템플릿 구성] 화면에서 담보의 이름을 지정합니다. 필요한 경우 적합하다고 판단되는 태그를 지정합니다. 출력을 PDF 형식으로 내보내려면 **[!UICONTROL Acrobat (.PDF)]**. 기본적으로 자료는 JPG 및 [!DNL InDesign] 포맷. 다중 페이지 자료에 대한 표시 썸네일을 변경하려면 **[!UICONTROL 썸네일 변경]**.

   ![chlimage_1-127](assets/chlimage_1-332.png)

1. 클릭 **[!UICONTROL 저장]** 그런 다음 을 클릭합니다. **[!UICONTROL 확인]** 을 클릭하여 대화 상자를 닫습니다. 다중 페이지 자료가 시작한 폴더에 만들어집니다.

   >[!NOTE]
   >
   >나중에 병합된 자료를 편집하거나 다른 자료를 생성하는 데 사용할 수 없습니다.

## 우수 사례 및 제한 사항 {#best-practices-limitations-tips}

* 다음 [!DNL InDesign] 편집기: [!DNL Experience Manager] 는 태그 수준에서 작동하며 단일 태그 아래의 모든 텍스트는 단일 엔티티로 간주됩니다. 편집할 때 텍스트 서식과 스타일을 유지하려면 각 단락(또는 스타일이 다른 텍스트)에 개별적으로 태그를 지정합니다.
