---
title: 자산 템플릿
description: ' [!DNL Adobe Experience Manager Assets] 의 자산 템플릿 및 자산 템플릿을 사용하여 마케팅 자료를 만드는 방법에 대해 알아봅니다.'
contentOwner: AG
role: Business Practitioner
feature: 자산 관리,개발자 도구
exl-id: 12c92aad-3a1d-486e-a830-31de2fc6d07b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1548'
ht-degree: 1%

---

# 자산 템플릿 {#asset-templates}

자산 템플릿은 디지털 및 인쇄 미디어에 대해 시각적으로 풍부한 컨텐츠를 빠르게 재활용할 수 있는 특별한 자산 클래스입니다. 자산 템플릿에는 고정 메시징 섹션과 편집 가능 섹션의 두 부분이 포함되어 있습니다. 고정 메시징 섹션에는 편집을 위해 비활성화된 브랜드 로고 및 저작권 정보와 같은 독점 컨텐츠가 포함될 수 있습니다. 편집 가능한 섹션에는 메시지를 사용자 지정하기 위해 편집할 수 있는 필드에 시각적 및 텍스트 컨텐츠가 포함될 수 있습니다.

전역 사이니지를 보호하는 동시에 제한된 편집 작업을 수행할 수 있는 유연성으로 자산 템플릿은 다양한 기능의 컨텐츠 아티팩트로 빠른 컨텐츠 적응 및 배포를 위한 이상적인 구성 요소를 제공합니다. 컨텐츠를 재활용하면 인쇄 및 디지털 채널을 관리하는 데 드는 비용을 절감하고 이러한 채널에서 전체적이고 일관된 경험을 제공할 수 있습니다.

마케터는 [!DNL Experience Manager Assets] 내에 템플릿을 저장하고 관리할 수 있으며, 단일 기본 템플릿을 사용하여 개인화된 여러 인쇄 경험을 손쉽게 만들 수 있습니다. 브로셔, 전단, 엽서, 명함 등을 비롯한 다양한 유형의 마케팅 자료를 만들어 고객에게 마케팅 메시지를 신속하게 전달할 수 있습니다. 기존 인쇄 출력이나 새 인쇄 출력에서 다중 페이지 인쇄 출력을 어셈블할 수도 있습니다. 무엇보다도 디지털 환경과 인쇄 경험을 모두 간편하게 동시에 제공하여 일관된 통합 환경을 사용자에게 제공할 수 있습니다.

자산 템플릿이 대부분 [!DNL Adobe InDesign] 파일이지만 [!DNL Adobe InDesign]에 대한 숙련도는 별의 아티팩트를 만드는 장벽은 아닙니다. [!DNL Adobe InDesign] 템플릿의 필드를 제품 필드에 매핑할 필요가 없습니다. 웹 인터페이스에서 직접 WYSIWYG 모드에서 템플릿을 편집할 수 있습니다. 그러나 [!DNL Adobe InDesign] 이 편집 변경 사항을 처리하려면 먼저 [!DNL Experience Manager Assets]을 [!DNL Adobe InDesign Server]와 통합하도록 구성해야 합니다.

웹 인터페이스에서 [!DNL Adobe InDesign] 템플릿을 편집하는 기능은 크리에이티브 및 마케팅 담당자 간의 협업을 강화하도록 도와줍니다. 컨텐츠 속도가 증가하면 마케팅 자료 출시 시간이 줄어듭니다.

자산 템플릿으로 다음을 수행할 수 있습니다.

* 웹 인터페이스에서 편집 가능한 템플릿 필드를 수정합니다.
* 글꼴 크기, 스타일, 태그 수준 문자 등 텍스트의 기본 스타일을 제어합니다.
* 컨텐츠 선택기를 사용하여 템플릿 내에서 이미지를 변경합니다.
* 템플릿 편집 내용을 미리 봅니다.
* 여러 템플릿 파일을 병합하여 여러 페이지 아티팩트를 만듭니다.

담보물에 대한 템플릿을 선택하면 [!DNL Experience Manager Assets]에서 편집할 수 있는 템플릿의 사본을 만듭니다. 원본 템플릿이 유지되므로 글로벌 사이니지가 그대로 유지되며 브랜드 일관성을 적용하는 데 재사용할 수 있습니다.

업데이트된 파일을 상위 폴더 내에서 INDD, PDF 또는 JPG 형식으로 내보낼 수 있습니다. 이러한 형식의 출력을 로컬 파일 시스템에 다운로드할 수도 있습니다.

## 자료 {#creating-a-collateral} 만들기

향후 캠페인을 위해 브로셔, 홍보물 및 광고와 같은 디지털 인쇄 가능한 자료를 만들고 전 세계 아웃렛 스토어와 공유하는 시나리오를 생각해 보십시오. 템플릿을 기반으로 자료를 만들면 채널 간에 통합된 고객 경험을 전달할 수 있습니다. 디자이너는 [!DNL InDesign] 과 같은 크리에이티브 솔루션을 사용하여 캠페인 템플릿(단일 페이지 또는 다중 페이지)을 만들고 템플릿을 [!DNL Experience Manager Assets]에 업로드할 수 있습니다. 담보를 만들기 전에 하나 이상의 INDD 템플릿을 업로드하여 [!DNL Experience Manager]에서 미리 사용할 수 있도록 하십시오.

1. [!DNL Experience Manager] 인터페이스에서 [!UICONTROL Assets]를 클릭합니다.

1. 옵션에서 **[!UICONTROL 템플릿]**&#x200B;을 선택합니다.

   ![chlimage_1-101](assets/chlimage_1-306.png)

1. **[!UICONTROL 만들기]**&#x200B;를 클릭한 다음 메뉴에서 만들 자료를 선택합니다. 예를 들어 **[!UICONTROL 브로셔]**&#x200B;를 선택합니다.

   ![chlimage_1-102](assets/chlimage_1-307.png)

1. 하나 이상의 INDD 템플릿이 업로드되어 [!DNL Experience Manager]에서 미리 사용할 수 있습니다. 브로셔에 사용할 템플릿을 선택하고 **[!UICONTROL 다음]**&#x200B;을 클릭합니다.
1. 브로셔에 대한 이름과 선택적 설명을 지정합니다.

   ![chlimage_1-104](assets/chlimage_1-309.png)

1. (선택 사항) **[!UICONTROL 태그]**&#x200B;를 클릭하고 브로셔에 사용할 태그를 하나 이상 선택합니다. **[!UICONTROL 확인]**&#x200B;을 클릭하여 선택 내용을 확인합니다.
1. **[!UICONTROL 만들기]**&#x200B;를 클릭합니다. 새 브로셔가 작성되었음을 확인하는 대화 상자가 표시됩니다. **[!UICONTROL 열기]**&#x200B;를 클릭하여 편집 모드에서 브로셔를 엽니다.

   <!--![chlimage_1-106](assets/.png) -->

   또는 대화 상자를 닫고 시작한 템플릿 페이지의 폴더로 이동하여 생성한 브로셔를 확인합니다. 카드 보기에서 해당 축소판에 자료 유형이 나타납니다. 예를 들어, 축소판 그림에는 [!UICONTROL 브로셔]라는 단어가 표시됩니다.

   ![chlimage_1-107](assets/chlimage_1-312.png)

## 자료 {#editing-a-collateral} 편집

담보물을 작성한 후 바로 편집할 수 있습니다. 또는 [!UICONTROL 템플릿] 페이지나 자산 페이지에서 엽니다.

1. 편집할 자료를 열려면 다음 중 하나를 수행합니다.

   * [자료 만들기](/help/assets/asset-templates.md#creating-a-collateral)의 7단계에서 만든 자료(이 경우 브로셔)를 엽니다.
   * 템플릿 페이지에서 자료를 만든 폴더로 이동한 다음, 자료의 축소판에서 [!UICONTROL 편집] 빠른 작업을 클릭합니다.
   * 자료의 자산 페이지에서 도구 모음에서 **[!UICONTROL 편집]**&#x200B;을 클릭합니다.
   * 자료를 선택하고 도구 모음에서 **[!UICONTROL 편집]**&#x200B;을 클릭합니다.

   <!--![chlimage_1-108](assets/chlimage_1-313.png) -->

   자산 파인더와 텍스트 편집기가 페이지 왼쪽에 표시됩니다. 텍스트 편집기는 기본적으로 열립니다.

   텍스트 편집기를 사용하여 텍스트 필드에 표시할 텍스트를 수정할 수 있습니다. 태그 수준에서 글꼴 크기, 스타일, 색상 및 유형을 수정할 수 있습니다.

   자산 파인더를 사용하여 [!DNL Experience Manager Assets] 내에서 이미지를 찾거나 검색하고 템플릿의 편집 가능한 이미지를 선택한 이미지로 바꿀 수 있습니다.

   ![chlimage_1-109](assets/chlimage_1-314.png)

   편집 가능한 페이지가 오른쪽에 표시됩니다. [!DNL Experience Manager Assets]에서 필드를 편집할 수 있으려면 [!DNL InDesign]에서 템플릿의 해당 필드에 태그를 지정해야 합니다. 즉, [!DNL InDesign]에서 편집 가능으로 표시되어야 합니다.

   >[!NOTE]
   >
   >[!DNL Experience Manager] 배포가 [!DNL InDesign Server]과 통합되어 [!DNL InDesign] 템플릿에서 데이터를 추출하고 편집할 수 있도록 합니다. [!DNL Experience Manager Assets] 자세한 내용은 [Experience Manager 자산과 InDesign Server](/help/assets/indesign.md)을(를) 참조하십시오.

1. 편집 가능한 필드에서 텍스트를 수정하려면 편집 가능한 필드 목록에서 텍스트 필드를 클릭하고 필드에서 텍스트를 편집합니다.

   ![chlimage_1-111](assets/chlimage_1-316.png)

   제공된 옵션을 사용하여 텍스트 속성(예: 글꼴 스타일, 색상 및 크기)을 편집할 수 있습니다.

1. **[!UICONTROL 미리 보기]**&#x200B;를 클릭하여 텍스트 변경 사항을 미리 봅니다.

1. 이미지를 교체하려면 **[!UICONTROL 자산 파인더]** ![chlimage_1-113](assets/chlimage_1-318.png)을 클릭합니다.

1. 편집 가능한 필드 목록에서 이미지 필드를 선택한 다음 자산 선택기에서 원하는 이미지를 편집 가능한 필드로 드래그합니다.

   ![chlimage_1-114](assets/chlimage_1-319.png)

   키워드, 태그 및 게시 상태에 따라 이미지를 검색할 수도 있습니다. [!DNL Experience Manager Assets] 저장소를 탐색하고 원하는 이미지의 위치로 이동할 수 있습니다.

   ![chlimage_1-115](assets/chlimage_1-320.png)

1. **[!UICONTROL 미리 보기]**&#x200B;를 클릭하여 이미지를 미리 봅니다.
1. 다중 페이지 자료의 특정 페이지를 편집하려면 하단에 있는 페이지 탐색기를 사용합니다.

1. 도구 모음에서 **[!UICONTROL 미리 보기]** 를 클릭하여 모든 변경 사항을 미리 봅니다. **[!UICONTROL 완료]**&#x200B;를 클릭하여 편집 변경 내용을 담보물에 저장합니다.

   >[!NOTE]
   >
   >미리 보기 및 완료 옵션은 자료 내의 편집 가능한 이미지 필드에 누락된 아이콘이 없는 경우에만 활성화됩니다. 자료에 아이콘이 없는 경우 [!DNL Experience Manager]에서 [!DNL InDesign] 템플릿의 이미지를 확인할 수 없기 때문입니다. 일반적으로 [!DNL Experience Manager]은(는) 다음 경우에 이미지를 확인할 수 없습니다.
   >
   >* 이미지가 기본 [!DNL InDesign] 템플릿에 포함되지 않습니다.
   >* 이미지는 로컬 파일 시스템에서 연결됩니다.

   >
   >[!DNL Experience Manager]에서 이미지를 확인하려면 다음을 수행하십시오.
   >
   >* [!DNL InDesign] 템플릿을 만드는 동안 이미지 포함([링크 및 포함된 그래픽 정보](https://helpx.adobe.com/indesign/using/graphics-links.html) 참조).
   >* [!DNL Experience Manager]을 로컬 파일 시스템에 마운트한 다음 누락된 아이콘을 [!DNL Experience Manager]의 기존 자산에 매핑합니다.

   >
   >[!DNL InDesign] 문서 작업에 대한 자세한 내용은 [Experience Manager](https://helpx.adobe.com/experience-manager/kb/best-practices-idd-docs-aem.html)에서 InDesign 문서를 사용하기 위한 우수 사례를 참조하십시오.

1. 브로셔에 대한 PDF 변환을 생성하려면 대화 상자에서 Acrobat 옵션을 선택한 다음 **[!UICONTROL 계속]**&#x200B;을 클릭합니다.
1. 자료는 시작한 폴더에 생성됩니다. 표현물을 보려면 자료를 열고 GlobalNav 목록에서 **[!UICONTROL 표현물]**&#x200B;을 선택합니다.

   ![chlimage_1-118](assets/chlimage_1-323.png)

1. 변환 목록에서 PDF 변환을 클릭하여 PDF 파일을 다운로드합니다. PDF 파일을 열어 자료를 검토합니다.

   ![chlimage_1-119](assets/chlimage_1-324.png)

## 자료 병합 {#merge-collateral}

1. [!DNL Experience Manager] 인터페이스에서 탐색 페이지에서 [!UICONTROL Assets]를 클릭합니다.

1. 옵션에서 **[!UICONTROL 템플릿]**&#x200B;을 선택합니다.

1. **[!UICONTROL 만들기]**&#x200B;를 클릭하고 메뉴에서 **[!UICONTROL 병합]**&#x200B;을 선택합니다.

   ![chlimage_1-120](assets/chlimage_1-325.png)

1. [!UICONTROL 템플릿 병합] 페이지에서 **[!UICONTROL 병합]** ![자산 추가](assets/do-not-localize/assets_add_icon.png)를 클릭합니다.

1. 병합할 자료의 위치로 이동하고 병합할 자료의 축소판을 클릭하여 선택합니다.

   ![chlimage_1-122](assets/chlimage_1-327.png)

   Omnisearch 상자에서 템플릿을 검색할 수도 있습니다.

   [!DNL Experience Manager Assets] 저장소 또는 컬렉션을 탐색하고 원하는 템플릿의 위치로 이동한 다음 병합할 템플릿을 선택할 수 있습니다.

   다양한 필터를 적용하여 원하는 템플릿을 검색할 수 있습니다. 예를 들어 파일 유형 또는 태그를 기반으로 템플릿을 검색할 수 있습니다.

1. 도구 모음에서 **[!UICONTROL 다음]**&#x200B;을 클릭합니다.
1. **[!UICONTROL 미리 보기 및 재정렬]** 화면에서 필요한 경우 템플릿을 다시 정렬하고 병합할 템플릿 선택을 미리 봅니다. 그런 다음 도구 모음에서 **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

   ![chlimage_1-126](assets/chlimage_1-331.png)

1. [!UICONTROL 템플릿 구성] 화면에서 담보의 이름을 지정합니다. 선택적으로, 적절하다고 간주하는 태그를 지정합니다. PDF 형식으로 출력을 내보내려면 **[!UICONTROL Acrobat (.PDF)]**&#x200B;을 선택합니다. 기본적으로 자료는 JPG 및 [!DNL InDesign] 형식으로 내보내집니다. 다중 페이지 자료의 표시 축소판을 변경하려면 **[!UICONTROL 축소판 변경]**&#x200B;을 클릭합니다.

   ![chlimage_1-127](assets/chlimage_1-332.png)

1. **[!UICONTROL 저장]**&#x200B;을 클릭한 다음 대화 상자에서 **[!UICONTROL 확인]**&#x200B;을 클릭하여 대화 상자를 닫습니다. 여러 페이지로 구성된 자료가 시작된 폴더에 생성됩니다.

   >[!NOTE]
   >
   >병합된 자료를 나중에 편집하거나 다른 자료를 만들 때 사용할 수 없습니다.

## 우수 사례 및 제한 사항 {#best-practices-limitations-tips}

* [!DNL Experience Manager]의 [!DNL InDesign] 편집기는 태그 수준에서 작동하며, 단일 태그 아래의 모든 텍스트는 단일 엔티티로 간주됩니다. 편집할 때 텍스트 서식 및 스타일을 유지하려면 각 단락 또는 스타일이 다른 텍스트에 개별적으로 태그를 지정합니다.
